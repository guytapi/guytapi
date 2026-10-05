# Round 7: Agent production runtime and reliability (pain mining)

Researcher slice: long-running agents, durable execution, idempotency, retries and timeouts, runaway loops, on-call for agents, handoffs, job scheduling and 429 backpressure, provider outages and failover, model upgrades changing behavior, canarying, replay.
Date: 2026-10-05. Searches used: 39 of 40 (one failed because reddit.com is blocked for the search tool, so **no Reddit evidence is included**). WebFetch was blocked, so every quote and claim below comes from search-result snippets, not from reading the full pages. Where a date is not visible in the snippet, it is marked "date not verified".

Excluded per STATUS.md (not re-proposed): generic observability, generic evals, agent undo/rollback, agent simulation, generic orchestration.

**Signal-quality warning.** This slice has a lot of synthetic or low-independence content. tianpan.co publishes daily "agent reliability" essays. gravitee.io/corpus pages look machine-generated. Many small GitHub repos read like AI-written proofs of concept: "prove unguarded retry doubles a side effect", receipt ledgers, approval-expiry issues. I counted these as weak signals at most. Vendor-forum threads (OpenAI community, Google AI forum, Microsoft Q&A, UiPath forum) and framework issue trackers (LangGraph, stripe/ai, MCP spec) count as the strongest signals.

---

## Ranking summary

| Rank | Problem | Avg score | Verdict |
|---|---|---|---|
| 1 | Forced model migrations break production agents (behavior parity on retirement deadlines) | 6.5 | Strongest pain and timing in the slice. Close to "generic evals", and eval vendors and model providers can absorb it. |
| 2 | Voice-agent model retirement (realtime/live models with no equivalent successor) | 5.9 | Narrower, sharper version of #1. Voice QA vendors are well funded. |
| 3 | Exactly-once side effects and "unknown outcome" reconciliation for agent tool calls | 5.5 | Real bug class. The protocol (MCP SEP-3182), frameworks and Temporal/Restate ($570M raised in 16 days) are absorbing it. |
| 4 | Durable human-approval gates for long-running agents (stale or orphaned approvals) | 4.9 | Every team rebuilds it. Feature-sized. |
| 5 | Fleet-scale LLM capacity scheduling (429s, quota, provider incidents, deprecation throttling) | 4.3 | Gateways have made this a commodity. |
| 6 | Multi-agent shared-state concurrency control | 4.0 | Pre-demand; mostly academic and hobby projects so far. |

None clears the bar (8.5 average, no category below 7). The best is #1 at about 6.5.

---

## 1. Forced model migrations break production agents

**Problem.** Providers now retire model snapshots every 3 to 9 months, and Azure auto-upgrades deployments. The successor model is not a drop-in replacement for an agent. Tool-calling propensity changes, forced `tool_choice` gets rejected, thinking blocks appear, sampling parameters are refused, and output formats shift. Teams have a hard deadline, no behavioral-parity test built from their own production traffic, and prompts that were tuned to the old model's quirks.

**Recent evidence (independent signals):**
1. OpenAI community, "gpt-realtime-2.1: production tool invocation regression — model answers instead of calling available tools" (community.openai.com/t/.../1398438). A controlled test reports about 25% of commands executed on 2.1 against 98-100% on gpt-realtime-2025-08-28, with the same app, instructions and tools. Date not verified; it sits in the deprecation wave, so roughly Aug-Oct 2026.
2. OpenAI community, "Follow-up: gpt-realtime-2.1 shows a critical shift from tool-driven to reasoning-driven behavior in our production AI agent" (/1396083, Deprecations category).
3. OpenAI community, "Model gpt-realtime-2.1-mini not calling function tools in SIP Realtime, while gpt-realtime-mini works with the same prompt/tools" (/1386141).
4. OpenAI community, "Gpt-realtime now shows 'Deprecated'… Please do not deprecate" (/1387746) and "Please Don't Deprecate GPT-Realtime Before a True Replacement Exists" (/1387635). Shutdown date: Jan 20, 2027.
5. Google AI forum, "Gemini 2.5 Flash deprecated without warning earlier than shutdown date" (discuss.ai.google.dev/t/174217). Google rolled it back and called it a config error. Separately, "Gemini-2.5-pro returns 'no longer available to new users' — contradicts official deprecation date (Oct 16, 2026)" (/176380).
6. Google AI forum, "Gemini 2.5 Live (Vertex) is being deprecated: v3.1/3.5 lack grounding" (/182720). EOL is Dec 13, 2026. Prompt-injected grounding was "insufficient for production".
7. GitHub, tomcounsell/ai #3570: "Migrate SONNET model constant to claude-sonnet-5-5 (thinking, max_tokens, and JSON-parse fixes at four call sites)". A Sonnet 5.5 PR in dofastted/vm2api #174 notes that forced tool use returns 400 and must become `auto`, which means "the model could then answer in text instead of calling a tool".
8. GitHub, EdGojara/hoa-doc-search #12, "Sonnet 4.5 retirement — Trusted model dependency + migration impact audit". dimagi/open-chat-studio #4684 tracks retirement on Nov 24, 2026, with reduced availability and rate errors from Oct 30. bradbrok/PinkyBot #1363 covers the same deadline. Deprecated 2026-09-30.
9. Microsoft Q&A: several threads on GPT-4o retirement and auto-upgrade behavior (learn.microsoft.com/answers/questions/5828138, 5815361 "Auto upgrade gpt4o to 5.1 as a standard deployment", 5770339). Teams are confused about when production silently moves to a new model.
10. UiPath forum: "Community LLM Models Deprecation — Agent Update and Redeployment Required". Every agent had to be re-pointed and redeployed in every environment by Aug 31, 2026. A separate "September 2026 updates checklist: LLM model removals" exists. This shows the pain reaching enterprise RPA buyers.
11. OpenAI deprecations: gpt-4o-2024-05-13 and gpt-4.1-nano shut down Oct 23, 2026. A transcription-model removal was announced Aug 26, 2026. The Assistants API shut down Aug 26, 2026. A "winding down the fine-tuning API" thread exists, which strands fine-tunes.

That is 11 signals across 4 providers plus 1 platform (UiPath), concentrated in Aug-Oct 2026.

**Who has the pain.** Teams running customer-facing or ops agents in production, especially regulated ones such as healthcare and finance, voice agents, and enterprise RPA/agent-builder users. The owner is the AI platform or AI engineering lead, plus the product owner who has to sign off that behavior did not change.

**What they do today.** Spreadsheet inventories of model IDs, grep for model strings, a handful of manual spot checks, and forum pleas asking providers not to deprecate. Some build a custom eval set under deadline pressure. Some pin through OpenRouter or Bedrock to buy time. Tools in use include Anthropic's `/claude-api migrate` skill (parameter fixes only), LLM Status (finds model IDs in code and tracks deprecation dates), and Braintrust/LangSmith datasets if those are already set up.

**Why current products fail.** Eval platforms assume you already have a curated golden set and judges. Most agent teams do not, and building one is the real cost. Nothing replays recorded production agent trajectories (multi-turn, with tool results stubbed) against the candidate model and reports behavioral deltas such as tool-call rate, tool order, refusals, format and cost. Nothing proposes prompt and tool-schema changes that restore parity. Provider migration guides cover API parameters, not behavior.

**Why now.** Retirement cadence plus forced parameter changes: Sonnet 4.5 retires Nov 24-30, 2026; Gemini 2.5 on Oct 16; gpt-4o snapshots on Oct 23; gpt-realtime on Jan 20, 2027; Gemini 2.5 Live on Dec 13. Newer models also reject old request shapes (forced tool_choice, temperature) and add thinking blocks by default. Agents multiply the blast radius because one changed tool-call decision cascades through a whole run.

**Potential product.** A "migration certificate" service. Import production traces (OTel / LangSmith / Braintrust export). The service builds a replay harness with tool responses stubbed from the recording, runs old vs. new model, and diffs agent behavior per workflow. It then auto-searches prompt and tool-description edits to close the gap and emits a sign-off report plus a canary plan. It sells per migration event, with a subscription for continuous "next deprecation" readiness.

**Time to value.** 1-2 weeks if traces exist; 3-4 weeks if instrumentation has to be added first.

**Pilot (14-30 days).** Pick one customer with a live Sonnet 4.5 or gpt-4o-2024-05-13 dependency. Replay 1,000-5,000 recorded runs against the successor model, deliver a delta report and prompt fixes, and have the customer cut over on the parity evidence. Success means the cutover ships before the deadline and post-migration incidents stay at or below baseline.

**Willingness to pay.** Medium. The deadline makes it urgent, but the budget is episodic: $10-50k per migration for mid-market and enterprise. It sits closer to a services budget than a platform budget.

**Expansion.** Every provider retirement. Model-cost downgrades ("can we move to the cheaper model?"). Provider switches. Continuous canarying of prompt changes.

**Competition (honest).** Braintrust, LangSmith, Arize, Galileo, Opik and Langfuse all market "compare models on your dataset", and any of them can ship a migration report in a quarter. OpenRouter publishes "AI agent regression testing after a prompt or model change". Anthropic ships `/claude-api migrate`, and providers are motivated to automate migration themselves. Voice: Hamming (YC S24) markets production call replay, Coval raised a $28M Series A, plus Cekura and Bluejay. Arthur.ai has published on model deprecation and version drift in agents. This is the "generic evals" category (killed in STATUS) wearing a deadline-driven costume.

**Moat.** At 10 customers: a library of provider-pair behavioral deltas ("Sonnet 4.5 to 5.5: forced tool_choice cases flip to text 12% of the time"). At 100: a cross-customer model-transition prior that predicts breakage before replay. At 1,000: arguably the industry's "model compatibility matrix", but providers and eval platforms can match it.

**CTO test sentence.** "Before Sonnet 4.5 shuts off on Nov 24, we replay your last 5,000 agent runs on Sonnet 5.5, show you exactly which tool decisions changed, and hand you the prompt fixes, so you cut over with evidence instead of hope."

**Kill test question.** Ask 10 AI platform leads who have a retirement deadline in the next 90 days: "Would you pay $20k for a parity certificate and fixes, or will you use Braintrust/LangSmith or the provider's migration tool?" If fewer than 3 say they would pay, or most already have a golden set, kill it.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC |
|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 9 | 9 | 7 | 6 | 7 | 6 | 4 | 4 | 6 | 5 |
Average: 6.5

---

## 2. Voice-agent model retirement (realtime/live models without an equivalent successor)

**Problem.** Voice agents depend on one speech-to-speech model's tool-calling determinism, pronunciation and grounding. Providers are retiring these models (gpt-realtime, realtime-mini, Gemini 2.5 Live, native-audio previews), and the successors regress on exactly those properties. Voice companies cannot swap in a different provider without re-engineering latency and audio.

**Recent evidence.** Signals 1-4 and 6 above. In addition:
- OpenAI community, "Realtime regression in non-English production voice agents: gpt-realtime-mini vs gpt-realtime-mini-2025-10-06" (/1380643).
- OpenAI community, "GPT Realtime 2.1 exhibits language drift" (/1386953).
- OpenAI community, "GPT-Realtime 1.5 — Major regression in voice expressiveness and accent quality" (/1377222).
- Google AI forum, "Critical Regression in native-audio-preview & Deprecation Confusion" (/110364; older, Dec 2025).
- Google AI forum, "Gemini 3.x Live never returns groundingMetadata for Google Search" (/186848).

About 9 signals in total, with heavy overlap of authors and forums.

**Who has the pain.** Voice-AI startups and contact-center deployments: SIP telephony, booking and ordering bots.

**What they do today.** Post on forums asking providers to delay, stay on the deprecated model until shutdown, re-prompt by hand, and run voice QA tools.

**Why current products fail.** Voice QA tools detect regressions but cannot make the old behavior survive the shutdown. The realistic fixes are architectural: a hybrid of a cascaded STT, LLM and TTS pipeline with a deterministic tool router, or a provider switch.

**Why now.** Hard shutdown dates Dec 13, 2026 (Gemini 2.5 Live) and Jan 20, 2027 (gpt-realtime).

**Potential product.** A voice-agent "compatibility layer". It sits between the speech model and tools and enforces deterministic tool invocation through an intent classifier plus forced routing, independent of which realtime model is underneath. It comes with migration replay of recorded calls.

**Time to value.** 2-4 weeks. **Pilot.** Port one production voice flow to the successor model behind the layer and match the old command success rate (for example, 98% against the 25% reported). **WTP.** High per customer, since revenue stops when the agent stops calling tools, but the buyer pool is a few hundred voice companies. **Expansion.** Any realtime-model change; telephony reliability.

**Competition.** Hamming, Coval ($28M A), Cekura, Bluejay on testing. Vapi, Retell, LiveKit Agents and Pipecat own the runtime layer and will ship this abstraction themselves. **Moat.** Weak. A runtime vendor can absorb it.

**CTO test sentence.** "Your voice agent keeps its 98% tool-call success after gpt-realtime shuts off, whichever model is underneath."
**Kill test question.** Do Vapi, Retell or LiveKit already offer deterministic tool routing that makes the model swap a non-event? If yes, kill it.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC |
|---|---|---|---|---|---|---|---|---|---|---|
| 9 | 9 | 8 | 6 | 5 | 6 | 7 | 4 | 3 | 4 | 4 |
Average: 5.9

---

## 3. Exactly-once side effects and "unknown outcome" reconciliation for agent tool calls

**Problem.** A tool call times out after the side effect has already committed (a charge, an email, a ticket). The agent loop, the framework, or a crash-and-resume then re-executes the call. Framework checkpoints re-run failed nodes by design, and per-session SDK idempotency keys do not survive agent-level retries.

**Recent evidence:**
1. LangGraph #9185, "[BUG] Resuming after a tool error re-runs the tool node, repeating a side effect that already happened". The repro is a fake payment provider that ends up charged twice while the thread history shows one charge.
2. LangGraph #8039, "durability='sync': put_writes/put persistence order is unenforced, so post-crash recovery (replay vs re-execute) is host-dependent".
3. LangGraph #9006 (resume after tool timeout), #9002 (error_handler re-executed on resume), #9183 (resumed writes stored twice). There is also a public repro repo, xbstack/langgraph-timeout-resume-side-effect-repro (LangGraph 1.2.11). Caveat: these issues may share an author or a research campaign, and dates are not verified.
4. stripe/ai #402, "Agent-level retry creates duplicate charges — no idempotency guard above the tool layer" (about 5 months old, around May 2026).
5. MCP spec PR SEP-3182, "Request Idempotency": an optional `idempotencyKey` on tools/call plus a `tools.idempotency` capability.
6. Show HN: SafeAgent (news.ycombinator.com/item?id=47294291), an exactly-once execution guard with receipts.
7. A crowd of OSS clones: akosidencio/agent-effects, assafbar2/receipt ("The agent crashed. Did the action happen?"), teresaliu90/AgentTrustOps, ideator-labs/mcpeffectreceipt, and JaredKlopstein/provenant (which even has an issue mapping "2026 agent-receipt competitors"). Issues in Noveum/orbit #407, SzamosiMate/tapir-archicad-MCP #23 and Da-Mikey/hermes-agent-evolution #173. Low independence; many look AI-generated.
8. An arXiv catalog of 63 LLM-agent budget-overrun incidents (2606.04056), which is adjacent: retry loops.

About 8 signal groups, but several are low-quality.

**Who has the pain.** Teams whose agents write to payments, CRM, ticketing or email, especially those on LangGraph or homegrown loops without Temporal.

**What they do today.** Hand-rolled request-ID tables in Postgres or Redis, passing InjectedToolCallId through to providers, approval gates before writes, or moving to Temporal or Restate.

**Why current products fail.** Durable-execution engines guarantee exactly-once activity completion only if you adopt their programming model. They do not reconcile against the third-party system ("did Stripe actually charge?"). Framework checkpoints re-execute failed nodes. Most SaaS APIs other than Stripe lack idempotency keys.

**Why now.** Long-running agents with real write access are going to production, and MCP is standardizing the hook (SEP-3182).

**Potential product.** An effect-ledger proxy for agent tool calls. It derives a stable intent key, claims it durably, and for an UNKNOWN outcome queries the target system through per-connector reconciliation probes (Stripe, Zendesk, Salesforce, Gmail) before allowing a retry or handing off to a human.

**Time to value.** Days for a single connector. **Pilot.** Wrap the write tools of one support or billing agent and measure duplicates prevented and UNKNOWN outcomes resolved. **WTP.** Low to medium; buyers see it as a library or feature. **Expansion.** An audit trail of every external effect, which shades into the governance space already crowded with Zenity and others.

**Competition.** Temporal ($550M Series E at $12.55B on Sep 14, 2026), Restate ($20M Series A about 16 days later), Inngest, DBOS, Hatchet, Trigger.dev. Anthropic Managed Agents (append-only event log, wake(sessionId)). LangGraph will likely fix this in docs or code. MCP SEP-3182 moves the guarantee into the protocol. Plus many free OSS clones.

**Moat.** A library of reconciliation connectors, which is thin.

**CTO test sentence.** "Your agent can crash mid-refund and never refund twice. We check Stripe before any retry."
**Kill test question.** Once SEP-3182 lands and LangGraph passes tool_call_id as the key by default, is anything left that a customer would pay for? Probably not, so kill it.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC |
|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 6 | 7 | 8 | 7 | 5 | 4 | 3 | 3 | 6 | 5 |
Average: 5.5

---

## 4. Durable human-approval gates for long-running agents

**Problem.** Agents pause for human approval for minutes to days. When the process restarts, the session crashes or the run ends, approvals are orphaned, stay "pending" forever, or get approved against stale context. Teams rebuild approval queues with expiry, audit and resume logic.

**Recent evidence (GitHub, mostly small projects, dates not verified).** use-agent-os/agent-os #1987 ("expired approvals with no waiter stay pending forever"); dkritarth/scopewatch #135; bytefolk/roleweave #392 ("lock stale pending approvals when their deadline passes"); NousResearch/hermes-agent #128437 (multiple pending approvals misreport run state); lindayi/hermes-mobile #22; andrewjpyle/agent_action_approvals (a durable HITL queue as a Django app); 5dive-ai/5dive PR #1099; google/adk-go #1658 (a consent reply restarts the graph instead of resuming). That is 8 signals, but they come from low-traction repos.

**Who has the pain.** Builders of ops and finance agents that need sign-off. **Today.** Slack buttons plus a database table plus cron expiry. **Why products fail.** Framework interrupts (LangGraph interrupt, Temporal signals) supply the primitive but not the queue, expiry, delegation, mobile UX or audit. **Why now.** Agents now run for hours. **Product.** An approval inbox API with TTLs, context-diff-on-approve ("what changed since the agent asked"), escalation routing and resume webhooks. **TTV.** Days. **Pilot.** Replace one team's homegrown Slack approval flow. **WTP.** Low. **Competition.** HumanLayer, Permit.io, Okta/Auth0 async authorization (CIBA), Slack/Teams native agent approvals, Temporal, LangGraph Platform. **Moat.** Low.
**CTO test sentence.** "Every agent approval in one inbox, with expiry, and the approver sees what changed since the agent asked."
**Kill test question.** Does Slack or Teams native agent approval plus a framework interrupt cover 80% of needs? Likely yes.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC |
|---|---|---|---|---|---|---|---|---|---|---|
| 5 | 4 | 6 | 8 | 7 | 5 | 4 | 3 | 3 | 5 | 4 |
Average: 4.9

---

## 5. Fleet-scale LLM capacity scheduling (429s, quotas, outages, deprecation throttling)

**Problem.** Running hundreds or thousands of concurrent agent jobs hits TPM/RPM limits and provider incidents. Retiring models are also deliberately throttled: Anthropic warned of "reduced availability and rate errors" on Sonnet 4.5 from Oct 30. Long runs die mid-way.

**Evidence.** OpenHands #9259 (org rate limit of 20,000 input TPM); "Concurrency Rate Limiting: A $10,000 Issue" (OpenAI community, older); gateway PRs implementing token-bucket TPM limits (mozilla-ai/otari #1906, AndrewTtofi/llm-gateway #5, DevOm-AI/Tollgate #7); at least 6 Claude incidents in Sep 2026 (Sep 3 multi-model, Sep 29 about 1 hour, per BleepingComputer and others); the Sonnet 4.5 deprecation throttling notice (dimagi #4684). About 6 signals.

**Who.** Batch and agent platforms, coding-agent fleets. **Today.** LiteLLM/Portkey, multiple API keys, backoff. **Why products fail.** Gateways do per-request failover but not run-level scheduling: they do not reserve capacity for a 3-hour run or checkpoint and resume on another provider. **Product.** A run-aware capacity scheduler. **Competition.** Portkey, LiteLLM, OpenRouter, Cloudflare AI Gateway, TrueFoundry, Kong, Braintrust gateway, provider batch APIs and priority tiers. **Moat.** Low. **WTP.** Low.
**CTO test sentence.** "Your 2,000 overnight agent runs finish even when Anthropic throttles. Capacity is reserved per run, and runs move providers mid-flight."
**Kill test question.** Will a customer pay beyond LiteLLM plus a provider priority tier? Unlikely.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC |
|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 5 | 6 | 6 | 5 | 5 | 4 | 2 | 2 | 5 | 2 |
Average: 4.3

---

## 6. Multi-agent shared-state concurrency control

**Problem.** Parallel agents read stale shared state and overwrite each other with no errors; one agent passes malformed state to another, which then acts destructively.

**Evidence.** HN "Ask HN: How are you orchestrating multi-agent AI workflows in production?" (47660705) and "How are people debugging multi-agent AI workflows in production?" (47358618). Snippets describe state collision ("zero errors but wrong results"). Also microsoft/autogen discussion #7240 (Network-AI race prevention), github/spec-kit #4128 (multi-agent isolation), theimaginaryfoundation/what-iff #254, and arXiv 2606.17182 and 2605.17076 (S-Bus). About 6 signals, mostly academic.

**Who.** Teams experimenting with multi-agent systems. **Today.** Locks, single-writer designs, avoiding multi-agent altogether. **Product.** A transactional state store for agents (optimistic concurrency, read-set validation). **Competition.** Databases already solve this; Letta, Zep and mem0 own agent memory; frameworks will add it. **WTP.** Low. Pre-demand.
**CTO test sentence.** "Your agents can share state without silently overwriting each other."
**Kill test question.** Are more than 10% of production agent deployments truly multi-writer? Probably not yet.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC |
|---|---|---|---|---|---|---|---|---|---|---|
| 4 | 3 | 4 | 5 | 5 | 4 | 3 | 5 | 4 | 4 | 3 |
Average: 4.0

---

## Signals that didn't make it

- **Durable execution / crash-resume for long-running agents.** The pain is real, but it is the most heavily funded corner of the slice. Temporal raised $550M at $12.55B on Sep 14, 2026 (thenextweb), and Restate raised a $20M Series A about 16 days later. Inngest, DBOS, Hatchet and Trigger.dev compete. Anthropic Managed Agents (Apr 8, 2026) bundles long-running sessions with an event log and wake() for $0.08 per session-hour. Dead on arrival.
- **Provider failover and outage resilience.** Claude had at least 6 incidents in Sep 2026, but the gateways (Portkey, LiteLLM, OpenRouter, TrustGate, Perpetuo on HN 46769611) already cover it.
- **Runaway agents and token-budget overruns.** HN "Burned $250 in tokens on Day 1" (47162495), "Ask HN: How are you keeping AI coding agents from burning money?" (47559293), the sub-agents burning budget comment (48883796), and the 63-incident arXiv catalog. This overlaps killed thesis B (FinOps for AI) plus native caps.
- **Agent-to-human handoff context loss in support.** The pain is documented (Twilio blog, CMSWire, alhena.ai, and a claim that "68% of bot-to-agent handoffs lose critical context", which is a vendor-cited stat). It is owned by CCaaS and AI-support vendors: Sierra, Decagon, Zendesk, Intercom, Twilio.
- **On-call, incident debugging and replay of multi-hour runs.** HN "Ask HN: In agent/automation incidents, what slows recovery?" (46790611) reports poor logs, no reproduction environment and unclear ownership. The answers land in generic observability (killed): Arize, LangSmith, Braintrust, Datadog, Diagrid.
- **Canarying prompt and model changes.** There are many playbooks (FeatBit, TrueFoundry, futureagi, agentpatterns) but little practitioner pain. Feature-flag vendors plus eval platforms cover it. It folds into #1 as an expansion.
- **ChatGPT tool-enabled runs capped at about 25-26 minutes since Aug 20** (OpenAI community /1397358, /1391943). This is consumer product behavior, not a B2B runtime gap.
- **Model deprecation inventory scanners** (LLM Status, the burin-labs/harn retirement metadata work, and many "stop offering retired models" PRs). Too thin on its own; a feature inside #1.

## Bottom line

The freshest and most forceful pain in this slice is **forced model migrations breaking production agents**. It has 11 independent signals across OpenAI, Google, Anthropic, Azure and UiPath, with hard deadlines on Oct 16, Oct 23 and Nov 24-30, 2026, and Dec 13, 2026 / Jan 20, 2027 for voice. Practitioners show strong distress, including measured regressions such as 98% falling to 25% tool success. But a product here is structurally an eval or replay product. Braintrust, LangSmith and the voice-QA vendors are already positioned for it, and the providers themselves have every reason to make migration easy. That is why it scores about 6.5, below the 8.5 bar. If the founders want a 14-day test, the kill test for #1 is cheap: interview 10 teams with a retirement deadline in the next 90 days.
