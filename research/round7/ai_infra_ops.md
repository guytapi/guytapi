# Round 7 — Slice: AI Infrastructure Operations (AI-native teams)

Researcher run: 2026-10-05. 38 web searches (cap 40). Reddit is blocked to our search agent, so the evidence comes from Hacker News, GitHub issues/PRs, the Google AI developer forum, and engineering blogs.
**Dating caveat:** WebSearch returns titles and snippets, not post dates. Where a date is stated it comes from the snippet text. GitHub issue numbers and model names (Opus 5, Fable 5.1, Mythos 5.1, Gemini 3.1) place most signals in mid/late 2026, but I could not confirm each item sits inside Aug–Oct 2026. Treat "recent" as "2026, likely last ~90 days" unless a date is given.

**Bottom line:** No candidate clears the 8.5 bar. The strongest is #1 (prompt-cache regression control), with the densest homegrown-fix evidence in the slice (~18 independent signals). It still dies on (a) adjacency to the killed AI-spend category, (b) the observability vendors already showing hit rate, and (c) providers starting to expose cache-miss reasons natively. Every other candidate in this slice falls into crowded categories (gateways, durable execution, eval platforms, GPU schedulers) or is low-severity.

---

## Ranked candidates

| Rank | Problem | Avg score |
|---|---|---|
| 1 | Prompt-cache regressions silently multiply agent cost/latency | 5.6 |
| 2 | Forced model retirements: inventory + re-validation of pinned model IDs | 5.5 |
| 3 | Safe mid-run provider failover (side-effect-safe resume during outages) | 4.9 |
| 4 | Fleet-level quota pooling across keys/accounts/providers | 4.5 |
| 5 | Batch-vs-realtime routing for async agent work | 4.5 |
| 6 | Embedding-model change → silent vector index corruption / re-embed ops | 4.4 |
| 7 | GPU bin-packing for self-hosted multi-model inference | 4.5 (ranked last: thin practitioner evidence) |

---

## 1. Prompt-cache regressions silently multiply agent cost and latency

**Problem.** Agent workloads depend on prompt caching (cache reads cost about 10% of the input price). The cache key is an exact prefix match. Small harness changes silently drop the hit rate from roughly 90% toward zero, and cost and TTFT multiply while outputs look correct. Examples: tool-list reordering, tool_search adding deferred tools, a timestamp in the system prompt, compaction rewriting tool defs, per-session URLs, hook-injected context. Nobody notices until the bill arrives. Many usage parsers also drop `cache_read_input_tokens`, so the dashboards are wrong too.

**Recent evidence (independent signals):**
1. microsoft/vscode #321551: "Prompt cache expires during active agent sessions, causing 10x cost spikes on gaps > 5 min."
2. QwenLM/qwen-code Discussion #4065: DeepSeek V4 Flash cache hit rate fell from ~98% to ~81% after v0.15.10 (ToolSearch). Uncached tokens went from ~3M to 12.9M (4.3x).
3. zed-industries/zed #65144: asks to surface cache hit rate in the Agent Panel, calling it "the single biggest cost driver"; zed #59528: prompt-based compaction is not cache-friendly because it modifies tool definitions.
4. openclaw/openclaw #156977: "Prompt cache invalidated every turn: tool-set membership change + dynamic system-prompt suffix wipe the cached prefix."
5. apache/maka #5879: tool_search activation invalidates the prompt cache on long sessions.
6. anthropics/claude-code #87137: Bash tool description embeds a per-session URL, so every `/resume` invalidates the whole cache; #83913: hook additionalContext changes invalidate the cache.
7. anomalyco/opencode PR #14743: improves Anthropic cache hit rate with a system split and tool stability; topcheer/ggcode PR #2445: deterministic tool ordering to preserve the prompt/KV cache; platform-q-ai/quecto #2406: "keep tool-set changes from breaking the prompt cache (measure, then fix)."
8. TauricResearch/TradingAgents #750: "Zero LLM API prompt cache hit rate due to prompt construction architecture."
9. Measurement is broken too: clairun/clai #155 (cache_read_input_tokens dropped), langfuse/langfuse #11979 (input tokens become 0 when cache_read is larger), github/gh-aw-firewall #9350 (proxy drops cache-read tokens from OpenRouter message_delta), agentic-os-org/ANOLISA #4244 / #6006, rashidrazak/opencode-cmd-provider #158 ("costs inflated up to 12.7x"). Snippet: a displayed cache-hit rate "reads 0% on long sessions that are actually ~96% cache reads."
10. Provider-side default change: Anthropic's cache TTL went from 1h to 5min around March 2026 with no announcement (The Register, 2026-04-13, "claude code cache confusion"; anthropics/claude-code #32671; dev.to write-ups citing a 17–26% cost increase and 30–60% for some workloads).
11. tianpan.co blog (2026-04-20), "Prompt Cache Hit Rate: The Production Metric Your Cost Dashboard Is Missing": an example of hit rate falling from 72% to 18% over three months with no deliberate change.
12. Homegrown tools are appearing: OsmnvAslan/promptcachelint ("explain why your LLM prompt cache missed: prefix diffs, silent invalidators"), CacheCatch (npm; audits traces for "recoverable cache loss" and "top leaking routes"), the mdskills "audit-prompt-caching" skill, Arlieeee/Dura-Agent PR #2 (cache measurement cut per-task cost 7–13%), Particle-Academy/prism-opentelemetry #2 (OTel capture can't diff a cached prefix because tool defs are missing), and Anthropic's own April 2026 postmortem naming a caching-optimization bug.

About 18 independent signals in all, most of them GitHub issues/PRs from engineers fixing this by hand.

**Who has the pain.** AI-native product teams and agent platforms spending $50k–$1M+/month on Anthropic/OpenAI/DeepSeek with long-context agent loops. Heaviest for coding-agent vendors, agent-platform startups, and internal agent teams at software companies.

**What they do today.** They grep for timestamps, sort tool lists, hand-place cache breakpoints, and fix usage parsers one PR at a time. Some write one-off scripts that diff request prefixes. A few have tried tiny OSS linters. In most teams nobody owns it.

**Why current products fail.** Portkey, Helicone and Langfuse show hit-rate *time series* (Portkey has a cache-hit-rate analytics API), and Datadog has a "monitor prompt caching" blog and feature. None of them (a) diff consecutive request prefixes to name the byte that broke the cache, (b) gate a PR in CI on a cache/cost regression from a replayed agent trace, or (c) attribute the loss to a code change. The trace capture often omits tool definitions (prism-otel #2), so a prefix diff isn't possible from their data.

**Why now.** Agents moved to long sessions with dynamic tool loading (tool_search/deferred tools shipped across harnesses in 2026). The TTL cut made idle gaps expensive. Model prices for frontier "5.x" tiers keep caching as the dominant lever.

**Potential product.** A "cache CI" tool: an SDK/proxy tap that records full request prefixes, a prefix-diff explainer ("cache broke at tool #14: schema reordered by PR #812"), and a GitHub check that replays a golden agent trace and fails the build if hit rate or $/task regresses. It would add a TTL/idle-gap advisor (when to pay for the 1h TTL or keep-warm).

**Time to value.** Under 1 day: point it at existing traces or a proxy and get a "recoverable $/month" number.

**Pilot (14–30 days).** Install on one agent service, establish a baseline hit rate and $/task, ship 2–3 fixes, add a CI gate. Success means a ≥20% input-token cost reduction plus one caught regression.

**Willingness to pay.** It demonstrates savings quickly (percent-of-savings is plausible), but it reads as a feature or a one-time fix. Once the prefix is stable, the value is mostly "insurance." Likely $500–$3k/month per team, unless it is bundled into broader cost/perf CI.

**Expansion.** Broader "agent performance CI" (tokens/task, TTFT, tool-call count), KV-cache-aware routing for self-hosted inference, and context-compaction tuning.

**Competition.** Portkey, Helicone, Langfuse, Datadog LLM Obs and Arize show hit rate. OSS: promptcachelint, CacheCatch. Providers: a Classmethod article ("detecting the causes of Claude's prompt cache failures") suggests Anthropic now returns cache diagnostics in the API response. **That is the kill risk:** the provider names the miss reason natively, and the observability vendors add a "why" panel within a quarter. No funded pure-play found.

**Moat.** 10 customers: none (prefix diffing is simple). 100: a corpus of invalidation patterns per harness/framework and auto-fix PRs. 1,000: benchmark data on $/task by harness, plus a position in CI. All of it is weak against Datadog/Portkey adding the feature.

**CTO test sentence.** "Your agents' cache hit rate fell from 85% to 30% after last Tuesday's tool-registry change; that's $41k/month. Here's the one-line fix and a CI check so it can't happen again."

**Kill test question.** "If Langfuse/Datadog showed you *why* each cache miss happened, would you still pay a separate vendor to gate it in CI?" (Ask 10 AI-native CTOs; a "no" from more than 6 kills it.)

**Scores.** Pain 6 · Urgency 6 · Timing 7 · Speed to pilot 9 · Integration 8 · Reach 6 · WTP 5 · Competition 4 · Moat 3 · Market size 4 · VC attractiveness 4 → **avg 5.6**

---

## 2. Forced model retirements: pinned-model inventory and re-validation

**Problem.** Providers retire models on 60-day to roughly 4-month windows, sometimes earlier than announced. Model IDs are pinned in many places (code, configs, sub-agent profiles, gateway registries) with no owner. Each forced migration means re-validating every prompt and agent on the new model, and the new model often regresses.

**Recent evidence:**
1. Gemini 2.5 Pro/Flash/Flash-Lite shut down Oct 16, 2026 (Developer API) and Oct 20 (Vertex). Developers report measured regressions on Gemini 3 Flash "even after tweaking prompting."
2. Google AI dev forum: gemini-2.5-flash/flash-lite returned 404 "no longer available" on July 9, 2026, months before the stated date. Google said a config change caused it and rolled it back. Separate threads report "no longer available to new users" and models.get advertising generateContent while it 404s.
3. OpenAI (announced 2026-06-03): Evals goes read-only Oct 31 and shuts down with Agent Builder and reusable prompt objects on Nov 30, 2026. Multiple migration guides exist (developersdigest, qaskills, chatforest, mcp.directory). 15 OpenAI model entries shut down July 23, 2026.
4. Anthropic Claude Opus 4.1 retired Aug 5, 2026.
5. Helicone/helicone #5820: 21 priced models in the registry are already retired at their provider (as of 2026-09-15). Portkey-AI/gateway #1814: 95 of 126 matched models are already past shutdown.
6. Hmbown/Codewhale #6035: "Model pins don't propagate" — 14 of 19 DeepSeek pins named retired IDs, and sub-agents kept running on a retired ID. atomantic/PortOS #7327 and pollinations #15719 (expose retirementDate); jovandyaz/knowtis-app PR #681 (watch platform models and alert on breakage).
7. Blogs: TrueFoundry, "model deprecations: virtual models, staged cutovers"; tianpan.co, "The Model Deprecation Cliff" (2026-04-13) and "model end of life took your prompt" (2026-05-17).
8. HN 44839975: "it's impossible to prevent regression on 100% of prompts, especially if tuned to the quirks of the older model."

About 10 independent signals.

**Who.** Any team with production LLM features, worst for those running many prompts or agents across 2+ providers.

**What they do today.** A spreadsheet of model IDs, grep, manual re-runs of eval sets, and a scramble near the deadline. A few tiny OSS scanners.

**Why current products fail.** The scanners (model-eol, depdesk, model-rot, LLM Status, @llmintel/cli, isitdeprecated MCP, ai-model-retirement-lint) find IDs but don't re-validate. Eval platforms (Braintrust, Promptfoo, LangSmith) re-validate but don't own the deprecation calendar or the cutover. AWS Bedrock Advanced Prompt Optimization (2026-05-14) and AWS Transform model-to-model *do* the re-tune plus comparison, but only inside Bedrock.

**Why now.** Release cadence of about 3–4 months per frontier family, the OpenAI Evals shutdown orphaning eval suites (Oct 31 export deadline), and Gemini's double migration within roughly 4.5 months.

**Potential product.** "Dependabot + migration autopilot for models": inventory pins across repos and infra, watch provider lifecycles, then open a PR that swaps the model, re-tunes prompts, runs the team's evals plus shadow traffic, and reports diffs.

**Time to value.** Inventory in 1 hour. The first auto-migration PR in about 1 week.

**Pilot.** Migrate one Gemini 2.5 or GPT-4.x workload end to end before its deadline.

**WTP.** Moderate, and spiky: it peaks around deadlines. Hard to justify between them.

**Expansion.** Cost-driven model swaps (move to a cheaper model whenever quality allows), and multi-provider portability.

**Competition.** Crowded: about 7 OSS scanners, AWS Bedrock migration tooling, TrueFoundry/Portkey virtual models, FutureAGI shadow experiments, and every eval vendor adding "compare models."

**Moat.** 10 customers: none. 100: a prompt-migration corpus (old→new model rewrites that worked). 1,000: cross-customer regression priors per model pair. That is moderate, but eval vendors could build the same.

**CTO test sentence.** "Gemini 2.5 dies on the 16th; we found 37 call sites, re-tuned the prompts, and here's the eval diff and a mergeable PR."

**Kill test question.** "Did your last forced migration take more than 2 engineer-weeks, and would you have paid $20k to make it 2 days?"

**Scores.** Pain 6 · Urgency 7 · Timing 7 · Speed to pilot 6 · Integration 6 · Reach 6 · WTP 5 · Competition 4 · Moat 4 · Market size 5 · VC 5 → **avg 5.5**

---

## 3. Safe mid-run provider failover for long-running agents

**Problem.** Provider reliability in 2026 is poor (Claude below 99% uptime in Q1; multi-provider cascades in September). When a provider fails mid-run, naive retry or failover replays tool calls with side effects, orphans tool_call IDs, or drops partial work.

**Evidence:**
1. HN 47543189: "Claude loses its >99% uptime in Q1 2026." A commenter spending more than $200k/month on the enterprise tier cites "only a single 9." Quoted 99.56% vs OpenAI 99.96%.
2. HN 49551096 and threads (Sep 3, 2026): OpenAI, Claude and Grok down at once. The theory is OpenAI's 15-minute outage pushed load onto the others ("OpenAI goes down, everyone rushes over to Claude. Claude promptly chokes").
3. HN 49102150 ("Elevated errors across all models") and 49056194 ("Elevated Errors for Opus 5"); "Agent terminated early due to an API error."
4. HN thread on 529s: when a provider fails mid-agent run, "the second provider starts without knowing which tool calls have already been written," so idempotency keys are needed.
5. dapr/dapr-agents #861 (call_llm not idempotent; orphaned tool_calls), openclaw #119222 (duplicate side effects after a provider switch), acupof-ai/tileRL #677, daniel-ospina/agent-infra #497 (resume-with-checkpoint for mid-run 402 deaths), microsoft/agent-framework #8140, Ultimate-Multisite #2681, datakurre/graph-agent #117.

About 9 signals.

**Who.** Teams running long autonomous agents in production (ops agents, coding agents, back-office automation).

**Today.** Hand-rolled idempotency keys, outbox tables, checkpoint/replay rules per framework.

**Why products fail.** Gateways (LiteLLM, Portkey, OpenRouter) fail over *requests* but are blind to tool side effects. Durable execution (Temporal, Restate, Inngest, DBOS, LangGraph checkpointers) solves it if you rewrite onto them.

**Why now.** Longer agent runs, more providers, and correlated outages.

**Product.** Drop-in "agent run ledger": tool-call idempotency, cross-provider transcript translation, and resume-from-checkpoint.

**TTV** 1–2 weeks. **Pilot:** wrap one long-running agent; measure runs saved during the next outage. **WTP:** low to moderate (felt only during outages). **Expansion:** agent reliability SRE.

**Competition.** Heavy: durable-execution vendors are funded and pivoting to agents (Temporal, Restate, Inngest, DBOS), plus gateways.

**Moat.** Weak at every scale.

**CTO test.** "When Anthropic dropped for 40 minutes, 0 of your 1,200 in-flight agent runs double-charged a customer and all resumed on Bedrock."

**Kill test.** "Have you had a duplicated side effect from an agent retry in the last 90 days?"

**Scores.** Pain 6 · Urgency 5 · Timing 7 · Speed 5 · Integration 4 · Reach 5 · WTP 5 · Competition 3 · Moat 3 · Size 6 · VC 5 → **avg 4.9**

---

## 4. Fleet-level quota pooling across keys, accounts and providers

**Problem.** Agent fleets exhaust per-key TPM/RPM limits and subscription windows. Teams pool keys and accounts and rotate them, with storm control so failover doesn't cascade.

**Evidence.** KarpelesLab/teamclaude (pools Claude Max, Codex and API accounts and rotates on quota, with "fleet-level storm control"); thedotmack/claude-mem PR #3941; RooCodeInc/Roo-Code Discussion #6833; openclaw #44477; kravchenski/switchyard PR #101; NousResearch/hermes-agent PR #4188 (credential pools, least_used strategy); Alishahryar1/free-claude-code #1301; xalgorix PR #687. HN threads on weekly limits and "Pro Max 5x quota exhausted in 1.5 hours." About 9 signals.

**Who.** Mostly individual and small-team coding-agent users. Enterprises negotiate limits instead.

**Today.** OSS proxies and key-rotation code inside each agent.

**Why products fail.** Gateways already do key load-balancing. Much of the pooling of *subscriptions* is a ToS violation.

**Why now.** Weekly and session limits, plus agents running 24/7.

**Product.** Capacity broker with quota forecasting.

**Pilot / TTV.** Days.

**WTP.** Low, and buyers skew toward individuals.

**Competition.** LiteLLM, Portkey, OpenRouter, Bedrock cross-region inference.

**Moat.** None.

**CTO test.** "Your 300 agents never hit a 429 again."

**Kill test.** "Is this a capacity problem or a pricing problem you'd solve by buying Priority Tier?"

**Scores.** Pain 5 · Urgency 5 · Timing 6 · Speed 8 · Integration 7 · Reach 5 · WTP 3 · Competition 2 · Moat 2 · Size 4 · VC 3 → **avg 4.5**

---

## 5. Batch-vs-realtime routing for async agent work

**Problem.** Cron or scheduled agent jobs pay realtime prices (batch is 50% off), and they share rate-limit pools with interactive traffic.

**Evidence.** openclaw #70606 ("cron jobs billed at full real-time rates… same rate-limit pool"); oxageninc/product PR #5572; Embassy-of-the-Free-Mind/sourcelibrary-v2 #4681 (about $978 backlog at realtime) and #5244; mnfst/manifest Discussion #1597; opsnlops/creature-console #201; Canonry #1201; agamm/batchata and venkatk1801/claude-batch-pipeline (homegrown wrappers). About 8 signals.

**Who / today.** Teams with bulk or async LLM work, routing by hand per job.

**Why products fail.** Gateways rarely make batch a transparent route. Async semantics also leak into app code.

**Product.** Deadline-aware router: declare an SLA per job and it picks batch, flex or realtime.

**WTP.** Low (a feature).

**Competition.** OpenRouter batch, provider flex tiers, gateways.

**Moat.** None.

**CTO test.** "Half your token bill is jobs nobody waits on; we moved them to batch automatically."

**Kill test.** "Is batch-eligible spend more than 20% of your bill?"

**Scores.** Pain 4 · Urgency 4 · Timing 6 · Speed 8 · Integration 7 · Reach 5 · WTP 4 · Competition 3 · Moat 2 · Size 4 · VC 3 → **avg 4.5**

---

## 6. Embedding-model change → silent index corruption and re-embed operations

**Problem.** Changing the embedding model silently invalidates the vector index (mixed vector spaces, dimension mismatches), and re-embedding large corpora takes days.

**Evidence.** volcengine/OpenViking #1066 (auto-detect model change and rebuild); inful/ragabast #19 ("silent index corruption on model swap"); shubh209 #25 (dimension change breaks reindex); Thoth-Software/cake #283; nicklecoder/requiem PR #49 (one vector set per model); besessener/Archivist #173; devdaviddr nextjs-rag #56. About 7 signals, mostly small projects.

**Who.** RAG and agent-memory teams.

**Today.** Version stamps on chunks, dual indexes, resumable re-ingest scripts.

**Why products fail.** Vector DBs (Pinecone, Weaviate, Turbopuffer, LanceDB) increasingly support namespaces and versioned collections, so the gap is shrinking.

**Product.** Zero-downtime re-embedding and index migration service.

**WTP.** Low to moderate, and episodic.

**Competition.** Vector DB vendors and ETL vendors (Unstructured, etc.).

**Moat.** Weak.

**CTO test.** "Swap to the new embedding model across 400M chunks with no mixed-space queries and no downtime."

**Kill test.** "How many times did you change embedding models in the last year?"

**Scores.** Pain 5 · Urgency 4 · Timing 5 · Speed 6 · Integration 5 · Reach 4 · WTP 4 · Competition 4 · Moat 3 · Size 4 · VC 4 → **avg 4.4**

---

## 7. GPU bin-packing for self-hosted multi-model inference

**Problem.** Self-hosted inference clusters waste 30–50% of their compute. Whole-GPU-per-pod Kubernetes scheduling leaves heterogeneous models under 15% busy. Cold starts run 50–300 seconds for large models.

**Evidence.** tianpan.co, "GPU Scheduling for Mixed LLM Workloads: The Bin-Packing Problem Nobody Solves Well" (2026-04-14); Spheron citing Cast AI's 2026 report (~5% average SM utilization); Vertex AI co-hosting blog; NVIDIA Run:ai + NIM blog; many 2026 arXiv papers on cold start and autoscaling (e.g., 2606.07362 on vLLM cold start, 2609.20874). Practitioner (non-vendor) evidence is thin. About 5 signals, mostly vendor or academic.

**Who.** The minority of AI-native teams running their own inference.

**Competition.** Very crowded: Run:ai (NVIDIA), CAST AI, Modal, Baseten, Fireworks, llm-d / KServe, Anyscale.

**Moat / WTP.** Large market, but owned by funded players.

**CTO test.** "Same traffic, 40% fewer H100s."

**Kill test.** "Do you run more than 64 GPUs of inference yourself?"

**Scores.** Pain 6 · Urgency 5 · Timing 5 · Speed 4 · Integration 4 · Reach 4 · WTP 6 · Competition 2 · Moat 3 · Size 6 · VC 5 → **avg 4.5** (ranked last on evidence quality)

---

## Signals that didn't make it

- **Per-run token budgets / runaway-loop caps.** Lots of pain: $47k from an 11-day loop (cited in tokencap); microsoft/agent-framework #8862; swenyai/sweny #449; nexu-io/open-design #8077; reactive-agents-ts #231; dify Discussion #35778; judgevet #56. Dropped because this is the killed AI-spend-caps category (thesis B), and OSS tokencap plus native provider caps cover it.
- **Cost-per-task attribution in multi-agent pipelines.** Traigent #1598 / PR #2363; hiveplane #370 (tag every event with tenant/team/agent/run). Same killed FinOps category.
- **Prompt/agent config versioning and rollback.** archestra-ai #5076, andtii/agentic #169, llmgateway PR #4440, foundry-prompt-agent-cicd-accelerator #12. Crowded prompt-management market (LangSmith, PromptLayer, Langfuse, Portkey). And OpenAI is *removing* hosted prompts (Nov 30), which pushes prompts back into code.
- **Eval/regression gating for model upgrades.** Real, but it is "generic evals," which the method excludes (Braintrust, Promptfoo, LangSmith, FutureAGI, Fruxon).
- **Latency SLOs for agents.** TTFT grows with transcript length: pacifio/atlas #291 (median 5.3s; also notes Claude reporting zero cache reads); oh-my-openagent #8825 (2.7–3.6x slower at 320K tokens); kubernetes-sigs/inference-perf #717 (time-to-first-user-token metric). Largely a symptom of #1 (cache) plus context growth. No distinct buyer.
- **Provider outage frequency.** Strong evidence (see #3), but the response is multi-provider gateways, which are crowded.
- **Rate-limit negotiation / priority tiers.** HN shows quota frustration, mostly on consumer subscriptions. Enterprise quota negotiation is a sales conversation, not a software gap.
- **KV-cache-aware routing (self-hosted).** llm-d / KServe and academic work. An infra-vendor category.

## Notes for the war room

- The slice confirms structural conclusion #1. Every operational AI-infra gap with public pain already has OSS homegrown tools *and* a gateway or observability vendor one feature away.
- #1 is the only item where engineers repeatedly hand-fix the same failure mode across dozens of repos with no owner. If any follow-up happens, run the kill-test question on 10 AI-native CTOs with more than $100k/month token spend. Also check whether Anthropic/OpenAI cache-miss diagnostics in the API response are already general availability (a Classmethod article suggests Anthropic exposes them). If they are, #1 is dead.
