# Round 31 — Track 6: Replacement opportunities (re-founding $1B-$100B software companies for an agent-dominated world)

Date: 2026-10-06. Searches used: 12 of 20. All URLs below came back in search results; claims attributed to secondary blogs are marked (secondary). Nothing was fetched (WebFetch blocked), so quotes are taken from search snippets only.

## Method
For each of 24 incumbents: "If founded today for a world dominated by AI agents, would it look like this?" Short screen:

| Incumbent | Would it look the same? | Note |
|---|---|---|
| Datadog / Splunk / Sumo / Elastic | **No.** Dashboards and per-GB ingest assume humans read telemetry, and that volume grows at human speed | -> Thesis 1 |
| PagerDuty | Partly. Paging a human is the core assumption, but AI SRE (Resolve $1.5B, Traversal, Cleric) is already funded | Folded into 1 |
| ServiceNow / Zendesk | **No.** The ticket assumes a human requester and a human resolver | -> Thesis 2 (Zendesk is half-converted to per-resolution pricing) |
| Atlassian / GitLab | **No.** The issue is a unit of work for humans. Agents need specs, verification and budgets | -> Thesis 3 |
| Zuora / Coupa (billing and procurement side) | **No.** Seat and subscription billing assume per-employee buying | -> Thesis 4 |
| Segment / HubSpot / Salesforce data layer | **No.** The CDP feeds human marketers and dashboards. Agents need live, writable customer context | -> Thesis 5 |
| Okta / Workday | **No.** Identity is tied to the HR record of an employee | -> Thesis 6 |
| Twilio | Already re-founding itself (voice AI +49% YoY, Conversation Memory) | Incumbent is adapting well, so skip |
| Snowflake / MongoDB | Mostly yes. Agents still need storage. The semantic layer is the new piece, and Snowflake/Databricks shipped it (GA Mar/Apr 2026) | Skip |
| LaunchDarkly | Already adapting with AgentControl (May 2026). Matches killed thesis H8 | Skip |
| Postman | Becomes an MCP tool registry. Overlaps killed thesis P2 / T4 | Skip |
| CrowdStrike / Zscaler / JFrog | Mostly yes. Endpoints and artifacts still exist. Agent-specific pieces were killed earlier (H10, F, I) | Skip |

---

## Thesis 1 — "Telemetry for machine readers": observability rebuilt for agent consumers and agent-scale volume
**Shape:** A ~$50B observability category charges per GB ingested and shows the data on dashboards because it assumed humans read telemetry and code grows at human speed. AI agents now write 3-5x more services and are the main readers (AI SRE). So the category must be rebuilt as cheap raw-event storage with an agent-native query and causality API, priced per question answered rather than per GB.

- **Existing category:** Observability and log analytics (Datadog, Splunk/Cisco, Elastic, Sumo, New Relic).
- **Market size:** About $50B+ TAM. Datadog alone is about $3B+ revenue (inferred, not re-verified this round).
- **Old assumption:** Humans look at dashboards. Ingest volume tracks headcount.
- **Why AI breaks it:** Agent-written code logs heavily, and services multiply. Telemetry is forecast at 5-10x current volume. The main reader is becoming an AI SRE that runs thousands of queries, not a person scrolling a dashboard.
- **New category:** An agent-native observability store. Everything goes to object storage, with no index-at-ingest. A query planner is tuned for LLM questions ("what changed before X"). Change/deploy/causality graph built in. Billed per investigation.
- **Product (CTO-simple):** "Send all your OTel here. It costs 10x less, and your AI SRE gets better answers than it does from Datadog."
- **Buyer:** VP Infrastructure / Head of Platform; CFO pressure on the Datadog bill.
- **Pain:** The Datadog renewal grows faster than revenue. Multi-year contracts were sized on pre-agent volume.
- **Recent evidence:**
  1. Datadog renamed LLM Observability to "Agent Observability" with Sep 2026 pricing changes (secondary): https://www.truefoundry.com/blog/datadog-llm-observability-pricing
  2. "AI Coding Agents Will 10x Your Datadog Bill", Feb 2026 (vendor blog): https://oneuptime.com/blog/post/2026-02-12-ai-coding-agents-will-10x-your-datadog-bill/markdown
  3. 2026 procurement guidance warns of a 5-10x telemetry volume trajectory (secondary, OpenObserve): https://openobserve.ai/blog/datadog-pricing.md
  4. Resolve AI at a $1.5B valuation, Apr 2026, founded by ex-Splunk executives: https://techcrunch.com/2026/02/04/ai-sre-resolve-ai-confirms-125m-raise-unicorn-valuation/
  5. Traversal positions itself as working across mixed observability stacks (secondary): https://metoro.io/comparisons/ai-sre/traversal-ai-alternatives
  6. PagerDuty SRE Agent / AI agent suite: https://www.businesswire.com/news/home/20251008279706/en/PagerDuty-Launches-Industry%E2%80%99s-First-End-to-End-AI-Agent-Suite-Slashing-Incident-Response-Times-and-Empowering-Teams-to-Innovate
- **Current workaround:** Sampling, dropping logs, Cribl pipelines, ClickHouse-based self-hosting (SigNoz, OpenObserve, HyperDX).
- **Competitors:** Direct: ClickHouse/HyperDX, OpenObserve, Grafana (Loki/Tempo), Chronosphere (now Palo Alto), Observe (now Snowflake). Adjacent: Resolve, Traversal, Cleric, Datadog Bits AI.
- **Why incumbents may lose:** Datadog's gross margin and stock price depend on per-GB/per-host pricing. Moving to cheap storage plus per-investigation pricing cannibalizes that revenue (innovator's dilemma).
- **Wedge:** Dual-write the logs from the noisiest 20% of services. Show the cost reduction and an AI-SRE answer-quality benchmark.
- **Integration:** Hours (OTel collector fork).
- **30-day pilot:** Mirror 1 cluster. Replay 10 past incidents through an AI SRE on both stores and compare answer quality and cost.
- **Pricing:** $/TB stored (low) plus $/investigation. Target 50-70% below the Datadog line item.
- **Expansion:** Metrics, traces, security logs (SIEM) and a built-in AI SRE.
- **Moat:** 10 customers: none. 100: an incident-causality corpus that improves planners. 1,000: data gravity and the default store for third-party AI SREs.
- **$10B case:** Take 10% of a $50B+ category during a forced re-platforming.
- **CTO one-liner:** "Datadog for robots, at S3 prices."
- **Kill risks:** Very crowded with OSS cost-down players. ClickHouse, Grafana and Snowflake (Observe) can each claim "agent-native". The differentiation could be just a cheaper store.

| Mkt | Transf | Urg | Why-now | Reach | Pilot | Integ | Opening | Diff | Expand | Moat | VC | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 9 | 7 | 7 | 7 | 7 | 8 | 8 | 4 | 4 | 8 | 5 | 6 | **6.7** |

---

## Thesis 2 — "Service desk with no tickets": ITSM rebuilt as agent-executed intents
**Shape:** ITSM (~$15B+ for ServiceNow) works like a ticket queue because it assumed a human requester and a human fixer. Agents now file and fix most L1 work. So it must be rebuilt as a policy-bound intent executor, where the ticket is the exception and not the unit of work.

- **Existing category:** ITSM / ESM (ServiceNow, Atlassian JSM, BMC, Freshservice, Zendesk for IT).
- **Market size:** ServiceNow at about $13B revenue (inferred). ITSM plus ESM is $20B+.
- **Old assumption:** A human creates and resolves each ticket. Pricing is per fulfiller seat.
- **Why AI breaks it:** L1 is resolved autonomously. Requesters are increasingly agents (coding agents asking for access, infra). Seats shrink as resolution is automated.
- **New category:** An intent ledger plus executor. Requests (human or agent) arrive as structured intents. Pre-approved runbooks run automatically under policy. Only exceptions reach humans. Billed per executed intent.
- **Product:** "Your Okta, Jamf, AWS and GitHub requests get done in seconds with a full audit trail. Humans see only 5%."
- **Buyer:** CIO / VP IT; Head of IT Ops at 500-5,000-employee companies.
- **Pain:** ServiceNow cost and implementation time. Agent-originated requests flood the queues.
- **Recent evidence:**
  1. ServiceNow acquired Moveworks for $2.85B. Autonomous Workforce, Feb 2026 (secondary): https://www.ksolves.com/blog/servicenow/servicenow-ai-implementation-guide
  2. L1 Service Desk AI Specialist gated behind the Prime tier (secondary, same source).
  3. Plotch.ai raised $25M (Khosla, Battery) for agentic workforce/IT (secondary via rezolve.ai): https://www.rezolve.ai/blog/best-servicenow-alternatives-capabilities-pricing-and-what-to-consider
  4. "The agents are coming for ServiceNow" (substack): https://sandhya.substack.com/p/the-agents-are-coming-for-servicenow
  5. Zendesk bills per verified automated resolution ($1.50-$2.00) (secondary): https://www.voiceflow.com/blog/zendesk-pricing
  6. Market split described as bolt-on (ServiceNow, Atlassian, BMC, Freshworks) vs AI-native (Atomicwork, Aisera) (secondary): https://www.eesel.ai/blog/ai-powered-itsm
- **Workaround:** Moveworks on ServiceNow, Slack bots, Okta Workflows, scripts.
- **Competitors:** Atomicwork, Aisera, Rezolve.ai, Serval (unverified), Console (unverified), Moveworks/ServiceNow, Atlassian Rovo.
- **Why incumbents may lose:** Fulfiller-seat revenue, and SI-heavy CMDB complexity, give them reasons not to collapse the ticket.
- **Wedge:** Access requests (agent and human) at mid-market companies without ServiceNow.
- **Integration:** Days (Okta/Entra, Slack, Jamf, GitHub, AWS).
- **30-day pilot:** Take over access plus software requests. Measure % auto-executed and time to fulfil.
- **Pricing:** $/executed intent plus a platform fee.
- **Expansion:** HR/finance ops, change management, CMDB built from observed state.
- **Moat:** 10: none. 100: runbook/policy library. 1,000: system of record for operations intents and audit.
- **$10B case:** Displace ServiceNow below the Fortune 500, as ServiceNow displaced Remedy.
- **CTO one-liner:** "ServiceNow, minus the tickets and minus the 18-month rollout."
- **Kill risks:** Already a crowded AI-native field with funded players, so the opening is narrow. Mid-market buyers are reached through slow IT cycles.

| Mkt | Transf | Urg | Why-now | Reach | Pilot | Integ | Opening | Diff | Expand | Moat | VC | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 9 | 8 | 6 | 7 | 6 | 7 | 6 | 4 | 5 | 8 | 6 | 6 | **6.5** |

---

## Thesis 3 — "Mission control for agent labor": work management rebuilt when most assignees are agents
**Shape:** Work management (~$10B+: Atlassian, Asana, Monday) is organized around human issues, sprints and story points, because humans did the work at human speed. When agents do most implementation, the unit becomes spec, budget, verification and acceptance. So it must be rebuilt as a dispatch-and-verify system for agent labor.

- **Existing category:** Project/issue tracking (Jira, Linear, Asana, GitLab Plan).
- **Market size:** Atlassian at about $5B+ revenue (inferred). Category $10-15B.
- **Old assumption:** A human picks up a ticket, takes days, and coordinates in comments.
- **Why AI breaks it:** Agents finish tickets in minutes. The bottlenecks become specs, parallel dispatch across vendors (Claude Code, Codex, Devin), cost and human acceptance.
- **New category:** An agent-labor control plane. Specs go in, are dispatched to the best or cheapest agent, verified against acceptance tests, and humans accept. Ledger of cost, quality and rework per agent.
- **Product:** "Write the spec. We run it on 3 agents, test the results, and you approve the winner."
- **Buyer:** VP Engineering.
- **Pain:** Many agents, no single queue, unclear cost/quality, review overload.
- **Recent evidence:**
  1. Agents in Jira GA, Feb 2026; agentic automation +30% MoM: https://techcrunch.com/2026/02/25/jiras-latest-update-allows-ai-agents-and-humans-to-work-side-by-side
  2. Atlassian press release on agents in Jira via MCP: https://businesswire.com/news/home/20260224033792/en/Atlassian-Introduces-Agents-in-Jira-to-Drive-Human-AI-Collaboration-at-Enterprise-Scale
  3. Linear CEO declared "issue tracking is dead", Mar 2026: https://www.devclass.com/development/2026/03/27/linear-moves-sideways-to-agentic-ai-as-ceo-declares-issue-tracking-dead/5211661
  4. Linear says AI revenue is growing about 500%/quarter and MCP traffic is up 50% MoM (Sep 2026, secondary): https://enterprisedna.co/resources/ai-pulse/ai-pulse-2026-09-04-linear-says-its-ai-driven-revenue-is-growing-roughly-500-a-q
  5. "Why your next Jira assignee might not be human": https://www.uctoday.com/project-management/why-your-next-jira-assignee-might-not-be-human/
- **Workaround:** Jira/Linear plus GitHub Actions plus vendor agent dashboards.
- **Competitors:** Linear (strong, moving fast), Atlassian Rovo, GitHub Agent HQ / Copilot coding agent, Cursor background agents, Factory.
- **Why incumbents may lose:** Seat pricing and human-centric data models. But Linear is native enough to win, and this overlaps killed theses "Minions-in-a-box" (5.7) and T3.
- **Wedge:** Multi-vendor dispatch plus an acceptance ledger for teams running 2+ coding agents.
- **Integration:** Hours to days.
- **30-day pilot:** Route 100 backlog tickets. Measure merged %, cost per merged PR and reviewer hours.
- **Pricing:** % of agent spend routed, or a per-accepted-task fee.
- **Expansion:** Non-engineering agent work (ops, marketing).
- **Moat:** Agent-performance dataset across vendors at 1,000 customers.
- **$10B case:** Becomes the Jira of agent labor.
- **CTO one-liner:** "Jira where the assignees are agents and the done column is verified."
- **Kill risks:** Linear, GitHub and Atlassian already cover most of it. Near-repeat of killed work.

| Mkt | Transf | Urg | Why-now | Reach | Pilot | Integ | Opening | Diff | Expand | Moat | VC | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 8 | 6 | 8 | 8 | 8 | 8 | 3 | 4 | 7 | 4 | 6 | **6.5** |

---

## Thesis 4 — "Zuora for outcomes": monetization infra when software is sold per resolution or action
**Shape:** Subscription billing (~$10B+ incl. Zuora, Chargebee, Stripe Billing, Salesforce CPQ) works on seats and plans because companies bought software per employee. Agents make the unit of value an outcome (resolution, action, task). So billing must be rebuilt around metering verified outcomes, disputes and outcome-based contracts.

- **Existing category:** Subscription billing / CPQ / revenue recognition.
- **Market size:** About $8-12B (inferred).
- **Old assumption:** Price = seats x plan. Value is not measured.
- **Why AI breaks it:** Zendesk ($1.50-$2/resolution), Salesforce ($2/conversation, Flex Credits) and HubSpot ($0.50/resolution) moved to outcome pricing. Disputes arise over what counts as an outcome, and buyers want independent verification.
- **New category:** An outcome-metering plus contract engine. Defines outcomes, verifies them with evaluator models, handles credits and disputes, and does revenue recognition for outcome contracts.
- **Product:** "Charge per resolved ticket without arguing with customers about it."
- **Buyer:** CFO / VP Monetization at AI-native SaaS.
- **Pain:** Revenue leakage, disputes, revenue-recognition complexity.
- **Recent evidence:**
  1. Zendesk per-resolution pricing with independent AI evaluation (secondary): https://www.voiceflow.com/blog/zendesk-pricing
  2. Futurum on outcome-based/hybrid pricing reshaping vendor playbooks: https://futurumgroup.com/press-release/are-outcome-based-and-hybrid-ai-pricing-models-rewriting-the-vendor-playbook/
  3. HubSpot $0.50/resolution, Apr 2026 (secondary, same Voiceflow source)
  4. Seat to usage/outcome renewal shifts: https://www.softwareseni.com/saas-pricing-is-shifting-from-per-seat-to-usage-and-outcome-what-changes-at-your-next-renewal/
  5. "AI agents are killing seat-based SaaS pricing": https://www.mpt.solutions/ai-agents-are-killing-seat-based-saas-pricing-heres-whats-replacing-it/
- **Workaround:** Metronome/Orb usage billing plus spreadsheets for outcome definitions.
- **Competitors:** Stripe (Metronome acquisition), Orb, Paid.ai (unverified), Chargebee, Zuora.
- **Why incumbents may lose:** Weak. Stripe/Metronome already own usage metering. Outcome verification overlaps killed T2 (4.7) and T4 (4.5).
- **Wedge, integration, pilot:** Event SDK (days). Pilot: shadow-bill one product line on outcomes.
- **Pricing:** % of billed outcome revenue.
- **Moat:** Outcome-definition benchmarks across vendors.
- **$10B case:** If outcome pricing becomes the default for agent software.
- **CTO one-liner:** "Stripe Billing for 'per job done'."
- **Kill risks:** Stripe absorbs it. Same death as T2/T4.

| Mkt | Transf | Urg | Why-now | Reach | Pilot | Integ | Opening | Diff | Expand | Moat | VC | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 7 | 5 | 7 | 6 | 7 | 7 | 3 | 3 | 6 | 4 | 5 | **5.6** |

---

## Thesis 5 — "Shared customer memory": the CDP rebuilt as a read/write context layer for every customer-facing agent
**Shape:** CDPs (~$5-10B: Segment, mParticle, Salesforce Data Cloud, HubSpot) collect events in batch for human marketers' segments. When sales, support and success agents each talk to the customer, the need is a live, writable, consistent memory across agents. So the CDP must be rebuilt as a customer memory with conflict resolution and permissions.

- **Existing category:** CDP / customer data infrastructure.
- **Market size:** About $5-10B (inferred), expanding into CRM data layers.
- **Old assumption:** Humans read segments. Data flows one way into tools.
- **Why AI breaks it:** Many agents act on the same customer. Each forgets or contradicts the others. Agents write new facts (commitments, preferences) that must propagate.
- **New category:** Customer memory. Unified facts with provenance, read/write APIs for agents (MCP), and contradiction checks.
- **Product:** "Every agent that talks to a customer knows what every other agent said and promised."
- **Buyer:** CTO / Head of CX platforms / VP Data.
- **Pain:** Agents contradict each other and repeat questions.
- **Recent evidence:**
  1. Twilio SIGNAL 2026 launched Conversation Memory / Orchestrator (secondary): https://futurumgroup.com/insights/twilio-q2-fy-2026-ai-communications-gain-commercial-traction/
  2. Twilio says CDP plus dedicated AI memory layer is the 2026 stack: https://twilio.com/en-us/blog/insights/top-customer-data-platform
  3. Mem0 raised $24M: https://pulse2.com/mem0-24-million-raised-for-powering-memory-layer-for-ai-agents/
  4. Cognee raised $7.5M, Feb 2026: https://dealroom.co/news/125999-cognee-raises-7-5m-to-build-memory-layer-for-ai-agents/
  5. Twilio voice AI +49% YoY drives more agent-customer conversations: https://thenextweb.com/news/twilio-q1-2026-voice-ai-revenue
- **Workaround:** Each agent vendor keeps its own memory, and Salesforce Data Cloud for Salesforce shops.
- **Competitors:** Twilio (Segment + Memory), Salesforce Data Cloud, Mem0, Zep, Cognee, Sierra/Decagon internal memory.
- **Why incumbents may lose:** Moderate. Batch architectures and per-MTU pricing. But Twilio is moving directly into this, and this overlaps killed "Commitment ledger" (4.6) and B+ (4.5).
- **Wedge:** Companies with 2+ customer agent vendors.
- **Integration:** Days to weeks.
- **30-day pilot:** Connect support plus sales agents. Measure contradiction rate and repeat questions.
- **Pricing:** Per profile or per memory operation.
- **Moat:** System of record for customer facts at 1,000 customers.
- **$10B case:** Becomes the Segment of the agent era.
- **CTO one-liner:** "One brain about each customer for all your agents."
- **Kill risks:** Twilio/Salesforce bundle it. Agent vendors refuse to give up their memory.

| Mkt | Transf | Urg | Why-now | Reach | Pilot | Integ | Opening | Diff | Expand | Moat | VC | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 7 | 5 | 7 | 6 | 6 | 5 | 4 | 5 | 7 | 7 | 6 | **6.0** |

---

## Thesis 6 — "Identity where agents outnumber people 80:1": IAM rebuilt from the workload up
**Shape:** Workforce IAM (~$20B+: Okta, Entra, SailPoint, CyberArk) is built on the HR record of an employee because humans were the actors. Machine identities now outnumber humans by more than 80:1, and agents act with delegated, task-scoped intent. So IAM must be rebuilt with short-lived, task-scoped credentials issued per action, plus delegation chains.

- **Existing category:** IAM / IGA / PAM.
- **Market size:** $20B+ (inferred).
- **Old assumption:** Identity = employee. Joiner/mover/leaver comes from Workday. Credentials are long-lived.
- **Why AI breaks it:** 80:1 machine-to-human ratio. 78% of organisations have no policy for agent identities. Only 20% revoke keys when agents retire.
- **New category:** Task-scoped identity issuance. Every agent action gets a just-in-time credential bound to the delegating human, the task and a TTL. Revocation by default.
- **Product:** "No standing keys for agents. Each task gets a credential that dies when the task ends."
- **Buyer:** CISO / Head of IAM.
- **Pain:** Key sprawl, agent incidents, audit.
- **Recent evidence:**
  1. Defakto raised $30.75M Series B for NHI/AI agent identity: https://www.govinfosecurity.com/defakto-raises-3075m-to-lead-non-human-identity-space-a-29767
  2. KPMG 80:1 machine-to-human ratio (secondary): https://ud.hk/en/blogs/insight/article/non-human-identity-ai-agents-2026-08-25
  3. CSA 2026: 78% have no agent-identity policy, 20% revoke (secondary, same source)
  4. MEF Agentic AI ID paper, Feb 2026: https://mobileecosystemforum.com/wp-content/uploads/2026/02/MEF-Agentic-AI-ID-Paper.pdf
  5. Atlassian agents get "same permissions, audit trails" as humans, which is the old model extended: https://techcrunch.com/2026/02/25/jiras-latest-update-allows-ai-agents-and-humans-to-work-side-by-side
- **Workaround:** Vaults, service accounts, Okta for AI Agents, Entra Agent ID.
- **Competitors:** Okta, Microsoft Entra Agent ID, CyberArk (Palo Alto), Astrix, Oasis, Aembit, Defakto, Clutch, Keycard (unverified).
- **Why incumbents may lose:** Weak. Okta and Microsoft ship agent identity and own the IdP. Overlaps killed T4 and H10.
- **Wedge, integration, pilot:** Replace static keys for coding agents in CI and cloud (days). Pilot: 1 team, % standing keys eliminated.
- **Pricing:** Per agent or per issued credential.
- **Moat:** Policy graph. Distribution is held by the IdPs.
- **$10B case:** Plausible only as a CyberArk-style category leader, which is contested.
- **CTO one-liner:** "Okta for agents with no permanent passwords."
- **Kill risks:** The most crowded of the six.

| Mkt | Transf | Urg | Why-now | Reach | Pilot | Integ | Opening | Diff | Expand | Moat | VC | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 9 | 7 | 7 | 8 | 6 | 7 | 6 | 3 | 4 | 7 | 5 | 6 | **6.3** |

---

## Ranking and verdict
| # | Thesis | Avg | Weakest |
|---|---|---|---|
| 1 | Telemetry for machine readers (Datadog/Splunk replacement) | 6.7 | Opening 4, Diff 4 |
| 2 | Service desk with no tickets (ServiceNow replacement) | 6.5 | Opening 4 |
| 3 | Mission control for agent labor (Jira replacement) | 6.5 | Opening 3 |
| 6 | Task-scoped agent identity (Okta replacement) | 6.3 | Opening 3 |
| 5 | Shared customer memory (Segment replacement) | 6.0 | Integ 5, Urg 5 |
| 4 | Zuora for outcomes | 5.6 | Opening 3, Diff 3 |

**None reaches 8.5.** There is a structural pattern in this track. The incumbents most clearly invalidated by agents (Jira, ServiceNow, Twilio, LaunchDarkly, Zendesk) are re-founding themselves fast, with AI-native challengers already funded. The strongest remaining opening is where the **incumbent's pricing model is the thing AI breaks** (per-GB observability, per-fulfiller ITSM), because the incumbent cannot follow without cutting its own revenue. If anything is deep-dived, take Thesis 1. Narrow it to the "agent-scale telemetry cost crisis" and test whether buyers will dual-write. Red-team it against ClickHouse/HyperDX and Observe-in-Snowflake.
