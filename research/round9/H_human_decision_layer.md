# Thesis H: The human decision layer ("control tower for every decision your agents need from a human")

*Round 9 deep dive. 2026-10-05. Red-team analyst. 38 web searches. WebFetch and Reddit were blocked, so every fact below comes from search-result snippets. [unverified] means no primary source could be opened. No URL below was invented; all appeared in search results.*

**One-line verdict: KILL (avg 4.5 on METHOD, 4.9 on the original bar).** The symptom is real: humans are the slow step in agent workflows. But the product is wrong for three reasons. (1) The queues that hurt are bottlenecked on *judgment and context*, not on *routing*. (2) The "learn to auto-approve" wedge is being shipped natively, for free, by the vendors that hold the context: Anthropic auto mode became the default on Aug 14 2026, Ramp Policy Agent learns from approval history, and GitHub enterprise-managed agent permissions shipped Sep 9 2026. (3) The cross-vendor routing and inbox position is already claimed by ServiceNow AI Control Tower, Microsoft Agent 365 plus Teams approvals, UiPath Action Center, Credal and Runlayer, and below them by a long tail of developer SDKs. Most damning: **HumanLayer, the YC company that coined "human-in-the-loop for agents", deprecated its approvals SDK and pivoted to a coding IDE (CodeLayer).** The category's founding company could not make a business of it.

This is an expanded version of round 7 #4 (stale human-approval queues, 4.9, "feature-sized"). Expanding the scope to "every decision, cross-vendor" makes the pain bigger, but it walks straight into platform territory.

---

## Problem
Agents produce work at machine speed and humans approve it at human speed. Queues build up: PR reviews, tool-call permission prompts, finance exceptions, support escalations, Slack pings. Agents stall, or humans rubber-stamp. Each agent vendor has its own approval surface, so a manager may get decision requests from 5 to 10 places.

## Recent evidence (is human approval actually the bottleneck?)
**Yes for code review, partly yes elsewhere. But the evidence points to "review less, with AI" rather than "route better".**
1. **LinearB 2026 Software Engineering Benchmarks.** Agentic-AI PRs have **5.3x longer pickup time** than unassisted PRs; AI-assisted PRs 2.47x (via stack-archive.com, a secondary source; the primary report was not opened).
2. **Faros AI "Acceleration Whiplash" (2026 telemetry, 22,000 developers, 4,000+ teams).** Median PR review time **+441.5%**, incidents per PR +242.7%, bugs per developer +54%, churn +861% (faros.ai/ai-productivity-paradox; vibegraveyard.ai).
3. **Rubber-stamping is measured.** Anthropic: users approve **~93%** of Claude Code permission prompts. In a controlled test, humans caught a disguised dangerous command **13.6%** of the time versus 89% for the auto-mode classifier. Serious unintended harm occurred in 6.3% of manually approved sessions versus 2.4% with auto mode (anthropic.com/engineering/claude-code-auto-mode; shellypalmer.com; devops.com). A separate 2026 study (tianpan.co, details [unverified]) says reviewers missed about 1 in 3 harmful agent requests.
4. **"Approval fatigue" is now a named problem.** WorkOS ("approval-fatigue-agent-governance" and "curating queues beats approving actions"), fullstack.com ("Gate Fatigue"), buildmvpfast, a DeepMind "agent traps" taxonomy, and a March 2026 threat rule for "Human Approval Fatigue Exploitation" [unverified]. Note that the *industry's prescribed fix is fewer approvals* (classifiers, batch curation), not better routing.
5. **Agents stalling on humans.** A case study (tianpan.co "The approval queue that became your critical path", June 2026) reports 23% of paused runs expiring unanswered, falling to 1.4% after redesign [unverified; the blog looks AI-assisted]. Quote: "The team that designs the agent does not own the queue."
6. **Finance.** Production AP touchless rates sit at 65-75%. Kognitos argues the remaining 30% of exceptions are *context* problems (master-data drift 35%, document gaps 25%, variance reasoning 20%, lifecycle mismatch 20%), not routing problems (kognitos.com/blog/agentic-ap-pilot-stalled-70-percent-touchless). 20-35% of AI-processed ops, finance and support tasks need human review (stealthagents.com, [unverified, low-quality source]).
7. **Operator sentiment.** PostHog's "Stop being the code review bottleneck" ("review less", not faster); "85% say code review is the new bottleneck" [unverified]; Martin Monperrus argues human review of agent code is an artificial bottleneck.

**Reading.** The pain is real and best documented in code review. But code review is the T3 territory (autonomous merge) that GitHub, Cursor and Greptile shipped in Sep 2026. Outside code, the evidence is thinner and mostly vendor blogs.

## Who has the pain
Engineering managers and staff engineers (PR queues), AP managers (exception queues), support ops leads (escalations), and platform teams running agents with tool-call gates. Each pain sits *inside a different system of action*.

## What they do today
Native approvals in each tool: Copilot Studio tool-approval toggles (GA Sep 2026), Teams and Slack interactive buttons, UiPath Action Center, Agentforce Command Center, Ramp Policy Agent, GitHub managed permissions, Claude Code auto mode. Plus homegrown Slack buttons, a DB table and cron expiry (round 7 #4).

## Why current products fail
Fragmentation is real: decisions come from many surfaces. But no evidence was found of buyers asking for *one cross-vendor decision inbox*. The pain people describe is "too many low-value approvals" (fixed by auto-approval) and "approvals without enough context" (fixed inside the system that holds the context). A neutral layer receives a thin JSON payload, which makes the context problem *worse* and rubber-stamping more likely.

## Why now
Real: agent volume, auto mode becoming the default, Copilot Studio approvals GA, Agent 365 GA (May 1 2026). But every one of those "why now" events is a *platform* shipping the capability.

## Competition (the killer)
| Layer | Player | What they ship | Funding / traction |
|---|---|---|---|
| **Learned auto-approve (the thesis's core "you approved 400 like this" feature)** | Anthropic Claude Code auto mode | Classifier approves safe tool calls; default for Pro/Max/Team from Aug 14 2026; Enterprise/API next | Free (classifier tokens no longer billed from Aug 7) |
| | Ramp Policy Agent | Learns "messy exceptions hidden in historical approvals"; escalates only 10-15% of expenses | Ramp |
| | GitHub Copilot enterprise-managed permissions | Admins set block / require-approval / allow per agent operation (Sep 9 2026) | GitHub |
| | Microsoft Copilot Studio | Per-tool "require human approval", approve-for-session; approvals inline in Teams/M365 Copilot; GA Sep 2026 | Microsoft |
| **Cross-vendor control tower** | ServiceNow AI Control Tower | Governs agents "regardless of which vendor built it" (Anthropic, Microsoft...); drafts decisions and routes for human approval | Knowledge 2026 headline |
| | Microsoft Agent 365 | Agent registry, Entra Agent ID, governance; $15/user/mo or in E7 ($99) | GA May 1 2026 |
| | Workday Agent System of Record | Authority, audit and ROI per agent; human approval steps | Mar 2026 |
| | Salesforce Agentforce Service Command Center / Slack | Supervisor view of AI and human agents; approvals routed in Slack threads; Slack Code approve-before-ship | Salesforce |
| **Routing by workload / expertise (the thesis's routing feature)** | UiPath Action Center + Maestro | HITL tasks across agents, BPMN and RPA; **assignment by Workload, Round Robin, All-in-group, LLM-inferred recipient**; actionable notifications from Slack, Teams and Outlook (Sep 2026) | Public company |
| | Credal | Cross-platform approvals "no matter where an agent shows up" (Claude, ChatGPT, Cursor, Slack); registry, audit log | ~$10.3M [unverified] |
| | Runlayer | MCP gateway with approval workflows and audit; Gusto 3,000+ workers | $42M total ($30M A, Jun 2026) |
| **Developer HITL APIs** | HumanLayer (YC) | **Approvals SDK deprecated; pivoted to CodeLayer IDE** | ~$500K disclosed [unverified] |
| | gotoHuman, hiloop (YC S26, pre-GA), Heed, Impri, Aprobo (OSS), Pushary, AgentMail approval inbox ($6M, GC), Courier Journeys (HITL escalation), Permit.io Access Request MCP, Auth0 Async Authorization/CIBA (GA Nov 2025), Zapier HITL, LangGraph Agent Inbox, Temporal (free waits for days), Agno and Relevance AI Slack approvals, Workato approval bot | Commodity |
| **Agent supervision** | Overmind (£2M), FriskAI ($3.6M pre-seed), Swept AI ($1.4M) | Runtime supervision | Seed |
| **Adjacent signal** | Relay.app (human-in-the-loop automation) shutting down Aug-Sep 2026 | | Weak negative signal |

## Neutral cross-vendor position, or does each vendor own its approvals?
**Each vendor owns its approvals, and has strong reasons to.** (a) The approval needs the agent's context (diff, transcript, ERP record), which lives in the vendor's system. (b) Fewer escalations is the vendor's margin: Sierra and Decagon bill per resolved ticket, and Anthropic sells auto mode as a safety feature. (c) The only credible neutral aggregators are the systems of record that already have the org chart, identity and authority data: ServiceNow, Microsoft (Entra plus Teams), Workday and Salesforce/Slack. A startup has none of that graph on day one.

**Sprint test: fails.** An inbox plus a Slack/Teams card plus a rules engine plus expiry is a sprint for a platform team (round 7 #4 found teams already doing it). UiPath's coding agent now *generates* HITL tasks from a description.

## Potential product
A cross-vendor decision API and inbox: ingest via API, MCP, Slack or email; route by authority graph; batch; learned delegation; SLA escalation; decision ledger.

## Time to value
Days for one integration. Value needs *many* agent sources connected, and most vendors expose no "decision needed" webhook, so you depend on their cooperation.

## Pilot (14-30 days)
Connect one team's agent approvals (for example, tool-call gates of internal agents plus one SaaS agent). Metrics: median decision latency, % of runs expired, approvals per human-hour, auto-approval rate, errors caught. **Problem:** in a coding pilot you are compared against free auto mode and GitHub managed permissions. In an AP pilot, the AP vendor's own exception agent wins because it has the context.

## Willingness to pay
Low to moderate. Approvals are a feature line in ServiceNow, Coupa, UiPath and Microsoft. The "human attention" cost is real but hard to attribute. Estimated ACV $25-80K for mid-market; enterprises buy from ServiceNow or Microsoft. [estimate]

## Expansion
The "system of record for human judgment" and "org chart for human+agent work" story is attractive, but it is the *stated roadmap* of Workday (Agent System of Record), ServiceNow (AI Control Tower) and Microsoft (Agent 365 + Entra Agent ID).

## Moat
- **10 customers:** none; SDK-grade code.
- **100 customers:** per-customer delegation policies, which do not transfer across customers. Decision history is only useful inside each tenant.
- **1,000 customers:** a cross-tenant "risk prior" for action types could exist, but frontier labs already train classifiers on far more tool-call data (Anthropic auto mode). The authority graph is owned by HRIS and IdP vendors.

## CTO test sentence
"Every decision any of your agents needs from a human, in one place, routed to the right person, with 80% auto-approved by policies learned from your own history."
**Likely CTO reply:** "Claude Code and Copilot already auto-approve; ServiceNow or Teams handles our business approvals; our platform team built the rest."

## Kill test question
Will a buyer pay for a neutral decision layer when (a) the agent vendors auto-approve natively and for free, (b) ServiceNow, Microsoft and UiPath route cross-vendor approvals inside platforms they already own, and (c) the category's founding startup abandoned it? **Evidence says no. Killed.**

## Scores: METHOD template (1-10)
| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC |
|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 5 | 6 | 7 | 4 | 4 | 3 | 2 | 3 | 5 | 4 |
**Average: 4.5**

## Scores: original bar (8.5 avg needed, none below 7)
| Pain | Urgency | ROI clarity | Customer accessibility | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position |
|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 5 | 4 | 4 | 6 | 6 | 6 | 5 | 3 | 7 | 2 |
**Average: 4.9.** Six categories are below 7.

## Buyer, number of companies, ACV
- **Buyer:** unclear, which is itself a kill signal. A COO doesn't buy developer infrastructure. A CTO or platform lead builds it. A Head of AI or CIO buys governance from ServiceNow or Microsoft. Engineering managers buy code-review tools (T3, killed).
- **Companies:** perhaps 3,000-8,000 firms worldwide run agents from multiple vendors at a scale where cross-vendor decision volume hurts (2026-27) [estimate].
- **ACV:** $25-100K [estimate].

## Market math
- **$10M ARR:** ~200 customers at $50K. Plausible only as an SMB/mid-market developer tool, where gotoHuman, Impri and Pushary compete on price.
- **$50M ARR:** ~700 at $70K. Requires winning enterprises against ServiceNow, Microsoft and UiPath bundles.
- **$100M ARR:** ~1,000 at $100K. Requires being the authority graph, which is Workday/Entra/ServiceNow territory.
- **$10B outcome?** Only if "system of record for human judgment" becomes a category *and* the incumbents fail to claim it. They have claimed it out loud. No standalone "approvals" company has historically reached that scale; approvals have stayed a feature of ERP, ITSM and procurement suites [analyst judgment].

## Five simulated buyers
1. **VP Eng, 400-engineer SaaS company (Claude Code + Copilot + Cursor):** **NO.** "Auto mode and GitHub managed permissions cut our prompts. The PR queue is an AI-review problem, and we bought Greptile/Bugbot."
2. **CIO, Fortune 1000 on ServiceNow + M365:** **NO.** "AI Control Tower and Agent 365 are already in our ELA. I won't add a third control plane."
3. **Controller, mid-market company using Ramp + an AP agent:** **NO.** "Ramp's Policy Agent auto-approves; my exceptions need the vendor master and the contract, not a better inbox."
4. **Head of AI Platform, fintech with 40 internal agents on LangGraph/Temporal:** **MAYBE.** "We built a Slack approval service in two weeks. I'd pay $20-30K if you handled expiry, audit and delegation, but it's a nice-to-have."
5. **COO, 150-person AI-native startup with many SaaS agents (support, sales, ops):** **MAYBE.** "The pings are annoying. But I can't name a budget line, and half my agents can't send you their decisions anyway."
Result: 0 YES, 2 MAYBE, 3 NO.

## VC committee view
- **For:** the story is great ("human attention is the scarce resource"; "org chart for human+agent work"), there's a clear why-now, and it's easy to pitch.
- **Against (wins):** "This is a feature of ServiceNow, Microsoft and UiPath, and the agent labs are removing approvals via classifiers. HumanLayer, the obvious winner, pivoted out. Where's the data moat when Anthropic trains on a million times more tool calls? Pass unless the founders show 10 paying design partners with multi-vendor decision volume."
- **Committee outcome:** pass at seed. Maybe a small pre-seed bet on a vertical variant.

## Red team (strongest case FOR, and why it still fails)
- *"Platforms only see their own agents; someone must see across them."* ServiceNow explicitly governs other vendors' agents; Credal and Runlayer already sit across Claude, ChatGPT, Cursor and Slack; Microsoft owns Teams, where most approvals land anyway.
- *"Decision history is the moat."* Per-tenant history doesn't create network effects. Frontier labs hold the cross-tenant priors.
- *"Rubber-stamping proves the need for smart batching and prioritization."* Yes, but Anthropic's data shows the fix is *removing* humans from 90%+ of decisions at the agent layer, not a better inbox.
- *Surviving sliver:* a regulated-industry "delegation-of-authority ledger" (insurance claims limits, bank credit authority, where AptlyDone-style DoA matrices already exist [unverified]) where a regulator demands a decision record. That is a dull vertical compliance product, not the $10B horizontal story. Score it separately if wanted; expect about 5.5-6.

## Kill signals (all found)
1. The category founder (HumanLayer) deprecated its approvals SDK and pivoted.
2. Learned auto-approval shipped natively: Anthropic auto mode (default Aug 14 2026), Ramp Policy Agent, GitHub managed permissions (Sep 9 2026), Copilot Studio approvals (GA Sep 2026).
3. Cross-vendor approval routing shipped: UiPath Action Center (Workload/Round-robin/LLM-inferred routing, Slack/Teams/Outlook actions, Sep 2026), ServiceNow AI Control Tower, Credal, Runlayer ($42M).
4. More than 15 developer HITL tools; an OSS self-hosted inbox (Aprobo); Relay.app shutting down.
5. No identifiable budget owner; passes neither the "build in a sprint" test nor the "vendor will ship it" test.
6. The industry's prescribed answer to approval overload is "review less" (WorkOS, PostHog, Anthropic), which shrinks the TAM of the decision layer over time.

## VERDICT: KILL
The pain is real (5.3x pickup delay, +441% review time, 93% rubber-stamp rate), but it belongs to the system that holds the context, and those systems shipped the fix in Aug-Sep 2026. Structural conclusion #1 holds again: the control layer over AI gets shipped by the platforms. Thesis H is round 7 #4 with a bigger story, and it dies the same way.

## Sources (from search results; most could not be opened)
- LinearB 5.3x via https://stack-archive.com/blog/agentic-ai-pr-review-bottleneck-5x-longer-2026
- Faros: https://www.faros.ai/ai-productivity-paradox ; https://vibegraveyard.ai/story/faros-ai-acceleration-whiplash-study/
- Anthropic auto mode: https://anthropic.com/engineering/claude-code-auto-mode ; https://devops.com/anthropic-makes-claude-codes-auto-mode-the-default-betting-automation-beats-manual-review/ ; https://www.infoworld.com/article/4207959/anthropic-makes-claude-codes-auto-mode-default-for-paid-users.html ; https://www.implicator.ai/anthropic-claude-code-auto-mode-default/
- Approval fatigue: https://tianpan.co/blog/2026-06-25-approval-fatigue-how-human-in-the-loop-gates-decay-into-rubber-stamps ; https://workos.com/blog/approval-fatigue-agent-governance ; https://workos.com/blog/curating-queues-beats-approving-actions ; https://www.fullstack.com/labs/resources/blog/gate-fatigue-when-human-approval-stops-meaning-anything ; https://tianpan.co/blog/2026-06-01-the-approval-queue-that-became-your-critical-path
- HumanLayer: https://ycombinator.com/launches/M8e-humanlayer-human-in-the-loop-for-ai-agents-and-beyond ; https://humanlayer.dev ; https://pushary.com/ar/vs/humanlayer (pivot / deprecation claim, secondary)
- gotoHuman: https://glama.ai/mcp/servers/@gotohuman/gotohuman-mcp-server/blob/8728e2b8449c78c5245a91d71cccd59b411fc0b3/README.md
- hiloop: https://app.dealroom.co/companies/hiloop_yc_s26
- Heed: https://pypi.org/project/heed/
- ServiceNow: https://www.bankinfosecurity.net/servicenows-new-platform-also-governs-everyone-elses-ai-a-31631 ; https://www.efficientlyconnected.com/servicenow-knowledge-2026-agentic-ai-platform/
- Microsoft: https://mc.merill.net/message/RM570434 ; https://rencore.com/en/blog/understanding-microsoft-agent-365-pricing
- GitHub: https://github.blog/changelog/2026-09-09-enterprise-managed-permissions-for-github-copilot-agent-operations
- UiPath: https://docs.uipath.com/action-center/automation-cloud/latest/release-notes/september-2026 ; https://docs.uipath.com/agents/automation-suite/2.2510/user-guide/agent-escalations
- Salesforce: https://www.constellationr.com/blog-news/insights/salesforce-launches-agentforce-3-command-center-visibility
- Workday: https://www.channelinsider.com/managed-services/workday-agent-system-of-record/
- Ramp: https://support.ramp.com/hc/en-us/articles/47618318137875-Use-Policy-Agent-for-approvals ; https://ramp.com/blog/ramp-agents-announcement
- Credal: https://credal.ai/ ; https://credal.ai/blog/how-does-credal-create-secure-scalable-actions
- Runlayer: https://www.runlayer.com/mcp-gateway ; https://techcrunch.com/2025/11/17/mcp-ai-agent-security-startup-runlayer-launches-with-8-unicorns-11m-from-khoslas-keith-rabois-and-felicis
- Permit.io: https://docs.permit.io/ai-security/access-request-mcp/overview
- Auth0: https://auth0.com/blog/auth0-for-ai-agents-generally-available/
- Zapier: https://zapier.com/blog/human-in-the-loop-guide/ ; Relay shutdown via https://www.usecarly.com/blog/human-in-the-loop-automation-tools/
- Temporal/LangGraph: https://temporal.io/blog/temporal-langgraph-plugin-durable-execution
- Courier: https://www.courier.com/blog/human-in-the-loop-ai-agent-notifications
- AgentMail: https://www.agentmail.to/blog/agentmail-seed-launch
- Kognitos AP: https://www.kognitos.com/blog/agentic-ap-pilot-stalled-70-percent-touchless/
- Overmind: https://tech.eu/2026/02/11/overmind-launches-with-2m-in-seed-funding-to-support-development-of-agentic-ai/
- Relevance AI Slack approvals: https://relevanceai.com/changelog/slack-tool-approvals-approve-or-reject-agent-tools
- AptlyDone DoA: https://coverager.com/building-a-delegation-of-authority-matrix-for-agentic-agents-and-humans-via-aptlydone-governance-software/
