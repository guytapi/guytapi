# Round 31 — Track 1: Category destruction (human-actor SaaS categories)

Date: 2026-10-06. 11 web searches used. URLs below appeared in search results; content was read only as search snippets (WebFetch blocked), so all claims are **snippet-level, unverified in full**. Items marked (U) are reasoning or memory with no source found this round.

## Cross-cutting evidence (shared by several theses)
1. Salesforce Agentforce moved to Flex Credits ($0.10/action) and $2/resolution; Zendesk $1.50-2.00 per automated resolution; HubSpot $0.50/resolved conversation (Apr 2026); ServiceNow says ~50% of net new business is non-seat. — https://beri.net/article/salesforce-saasacre-2026-seat-based-pricing-crisis , https://helply.com/blog/per-seat-saas-pricing-dying
2. UiPath down ~87% from ATH and >35% in 2026; ARR $1.85B, +11%; repositioned as "agentic automation". — https://finance.yahoo.com/markets/stocks/articles/got-1-000-agentic-ai-232000349.html , https://wwwhatsnew.com/2026/07/03/uipath-primer-beneficio-gaap-agentes-ia-2026/
3. Omni raised $120M Series C at $1.51B (Apr 23 2026) as "the semantic layer for AI agents"; OpenAI Frontier (Feb 2026) pitched as an enterprise semantic layer; Tableau shipped an Agentic Analytics platform plus an MCP server. — https://dealroom.co/news/127583-omni-raises-120m-series-c-at-1-5b-to-become-the-semantic-layer-for-ai-ag/ , https://www.beri.net/article/tableau-33m-semantic-models-power-bi-copilot-agentic-2026
4. Linear CEO said "issue tracking is dead"; Linear Agent in beta (Mar 2026); Claude Code, Devin, Cursor and Copilot appear as workspace teammates. — https://theregister.com/2026/03/26/linear_agent
5. Non-human identity funding: NewCore $66M (Jun 15 2026), Astrix $45M, Defakto $30.75M, Archestra $10M seed; five NHI/agent-control deals Jul 27-31 2026. — https://ecosistemastartup.com/?p=88953 , https://www.healthcare.digital/single-post/the-enterprise-identity-paradigm-shift-how-five-transactions-in-seven-days-priced-ai-agent-governan
6. Workday "Agent System of Record" (via Sana, 2026R1). — https://enterprisedna.co/resources/news/workday-agent-system-of-record-sana-2026
7. Day AI raised a $20M Series A led by Sequoia (Feb 2026), pitched as "the Cursor of CRM"; Attio has raised $116M in total. — https://finder.techleap.nl/news/feed/day-ai-raises-20m-from-sequoia-to-build-the-cursor-of-crm
8. Atlassian terms effective Aug 17 2026 allow training on Confluence content; Falconer markets "context sovereignty" migration; puppyone sells an agent workspace layer with diffs, audit and rollback. — https://falconer.com/guides/context-sovereignty-atlassian-data-policy/ , https://www.puppyone.ai/en/alternatives/puppyone-vs-confluence.md
9. Slack restricts conversations.history for non-Marketplace apps (1 req/min, 15 objects, from Mar 3 2026). This gates agents reading the human collaboration layer. — https://hexdocs.pm/slack_bot_ws/rate_limiting.html (snippet)
10. Agent-to-agent customer service is predicted to push conversation volume up 3-5x. — https://sinch.com/blog/customer-communications-predictions/ (prediction, not data)

**Pattern:** every category incumbent is already re-pricing and adding agents (evidence 1, 3, 4, 6). A "rebuild" thesis survives only where the change is on the **other side of the wire**: the counterparty, the data producer or the reader is now an agent, and the incumbent's data model cannot represent that.

---

## Thesis 1 — Inbound Agent Desk (helpdesk where the *customer* is an agent)
- **Existing category:** Helpdesk / CX platforms (Zendesk, Salesforce Service Cloud, Intercom, Freshdesk). Market size: ~$15-20B software (U), plus $300B+ contact-centre labour.
- **Old assumption:** the person contacting support is a human, using chat, email or voice, one conversation at a time.
- **Why AI breaks it:** buyers' agents (ChatGPT/Claude/Gemini assistants, procurement agents) arrive in bulk, retry, run in parallel, and need structured outcomes such as a refund issued, a slot booked or an RMA created. Conversational AI on the vendor side (Sierra, Decagon, Zendesk AI) still talks *natural language to a human-shaped endpoint*.
- **New category:** a support endpoint for machine callers: published resolution actions (MCP/API), caller-agent verification plus delegation proof, policy limits, idempotency and receipts.
- **Product:** "an MCP server for your support policy": refund, exchange, reschedule and status as typed actions with eligibility rules, rate limits per principal, and a signed receipt.
- **Buyer:** VP CX / Head of Support Ops at D2C, travel, telco or SaaS.
- **Pain:** volume and fraud from bot traffic; AI-resolution fees ($1.50-2/resolution) charged on machine-to-machine chats that could be a $0.01 API call.
- **Evidence:** 1, 10; Sierra/Decagon growth (U); round 12 caller-verification wedge (internal); OpenAI/Google agent checkout pushes (U); HubSpot price cut to $0.50 (1).
- **Workaround:** CAPTCHA, blocking bots, or routing them to the same LLM agent.
- **Competitors:** direct: none clearly identified (U). Adjacent: Sierra, Decagon, Zendesk, Salesforce Agentforce, Cloudflare bot management / Web Bot Auth, Stripe/OpenAI agentic commerce.
- **Why incumbents may lose:** per-resolution pricing gives them an incentive to keep machine traffic conversational, which is the innovator's dilemma in their pricing.
- **Wedge:** returns/refund API for Shopify-scale D2C. **Integration:** days (order system plus policy). **30-day pilot:** expose 3 actions; measure the share of agent-originated contacts deflected and the cost per resolution.
- **Pricing:** per verified action ($0.02-0.10) plus platform fee. **Expansion:** B2B order status, warranty, billing disputes, then a full "agent storefront".
- **Moat:** 10 customers: policy templates. 100: a cross-merchant reputation graph of caller agents and principals. 1,000: the default verification network that assistants integrate once.
- **$10B case:** if half of consumer service contacts become agent-originated, the endpoint becomes payments-like infrastructure.
- **CTO one-liner:** "Our support queue gets an API for robots, so robots stop chatting with our chatbot."
- **Risk / kill vector:** agent-originated volume is still a prediction (evidence 10); Zendesk can ship an "actions API"; overlaps killed thesis A (supplier sellable to agents) and T4.
- **Scores:** Market 8, Transformation 8, Urgency 5, Why-now 6, Buyer reach 7, Pilot speed 7, Integration 7, Opening 6, Differentiation 6, Expansion 8, Moat 6, VC 7 → **Avg 6.75**

## Thesis 2 — Context Compiler (Confluence/Notion rebuilt for agent readers)
- **Existing category:** wiki and knowledge management (Confluence, Notion, Guru, Glean on the search side), ~$10-15B (U).
- **Old assumption:** humans read docs, tolerate staleness, and resolve contradictions by asking someone.
- **Why AI breaks it:** coding and ops agents now read docs most often. They act on stale or contradictory pages literally and at scale. The doc becomes executable context, so wrong docs become production incidents.
- **New category:** a versioned, tested context layer: claims extracted from docs, code and tickets, each with an owner, an expiry and a check against the live system, and served to agents through MCP with provenance.
- **Product:** a "CI for company knowledge": every agent-facing fact carries a test, and failing facts get flagged or auto-PR'd.
- **Buyer:** VP Platform Engineering / Head of AI enablement.
- **Pain:** agents (Claude Code, Cursor, internal bots) repeat bad patterns because of an outdated runbook or ADR. Atlassian's training-terms change adds sovereignty worry.
- **Evidence:** 8 (Atlassian terms, Falconer, puppyone); ClickUp Knowledge Mgmt launch (search result); Graphify YC S26 and the DeepWiki/Code Wiki codebase-knowledge cluster (STATUS, killed); Rovo (4); AGENTS.md/skills proliferation (U).
- **Workaround:** CLAUDE.md/AGENTS.md files plus RAG over Confluence.
- **Competitors:** Glean, Atlassian Rovo, Notion AI, Falconer, puppyone, Tessl (skills), Graphify, DeepWiki.
- **Why incumbents may lose:** wikis optimise for authoring UX and seats, not for truth-maintenance. Weak structural reasons; Glean can add freshness tests.
- **Wedge:** runbooks and ADRs for SRE agents. **Integration:** hours (repo plus wiki connectors). **Pilot:** find stale or contradictory facts that agents used; count incidents or PR rework avoided.
- **Pricing:** per repo/source plus agent query volume. **Expansion:** policy, sales and support knowledge.
- **Moat:** weak at 10; at 100, cross-tool fact graphs; at 1,000, still copyable.
- **$10B case:** becomes the "source of truth API" every agent hits first.
- **CTO one-liner:** "Unit tests for the docs our agents obey."
- **Kill risk:** close to the killed codebase-knowledge-graph and A2 system-map theses; crowded.
- **Scores:** 7, 7, 6, 7, 7, 8, 8, 4, 4, 6, 4, 6 → **Avg 6.17**

## Thesis 3 — Agent Work Ledger (Jira/ITSM where agents are the assignees)
- **Existing category:** project management plus ITSM ticketing (Jira, ServiceNow ITSM, Linear, Asana), ~$25B+ combined (U).
- **Old assumption:** tickets are units of human attention; status is self-reported; throughput equals people.
- **Why AI breaks it:** agents generate and close work at 100x volume. Status must be proven (diff, test, deploy, log), not typed. The bottleneck becomes human review and dispatch across heterogeneous agents.
- **New category:** a work ledger. Each unit of work carries a spec, the agent assigned, cost, evidence of completion and reviewer sign-off, and the ledger dispatches to whichever agent is cheapest or most reliable.
- **Product:** a queue and router over Claude Code, Codex, Devin and Copilot with an evidence-gated "done" state and a per-agent scorecard.
- **Buyer:** VP Engineering.
- **Pain:** dozens of agent PRs a day; unclear which agent is good at what; review overload.
- **Evidence:** 4 (Linear "issue tracking is dead", agents as teammates); GitHub/Cursor autonomous merge (STATUS T3); Rovo; Jira agent assignment (U); ServiceNow AI Control Tower (STATUS).
- **Workaround:** Linear or Jira plus a GitHub label convention.
- **Competitors:** Linear (strong), Atlassian, GitHub Agent HQ / Copilot coding agent (U), Factory, Cursor background agents.
- **Why incumbents may lose:** Jira's seat model and human-workflow schema; but Linear is already agent-first, so the opening is narrow.
- **Wedge:** a cross-vendor agent scorecard. **Integration:** hours. **Pilot:** route 200 tasks; show cost per merged PR by agent.
- **Pricing:** % of agent spend routed or per task. **Expansion:** non-code work (ops, data).
- **Moat:** at 1,000 customers, cross-customer agent-performance data. Real but contested by GitHub.
- **CTO one-liner:** "Jira where the assignee is a model and 'done' needs proof."
- **Kill risk:** Linear plus GitHub ship this in quarters; overlaps the killed T3 and H theses.
- **Scores:** 8, 7, 6, 7, 8, 8, 8, 4, 4, 7, 5, 6 → **Avg 6.50**

## Thesis 4 — Capture-native CRM (system of record written by agents, not reps)
- **Existing category:** CRM (Salesforce, HubSpot, Dynamics), ~$80-100B (U).
- **Old assumption:** reps type the record; the CRM is a form-plus-report tool priced per seat.
- **Why AI breaks it:** agents both write (from email/calls) and read (SDR/AE agents act on it). Seat count falls while record volume and machine reads explode.
- **New category:** an event-sourced customer graph auto-built from communications, priced on records/actions, with an agent-first API.
- **Product / buyer:** CRO / RevOps head at a 50-500 person B2B company. **Pain:** dirty data that agents then amplify into bad outreach.
- **Evidence:** 7 (Day AI Sequoia $20M; Attio $116M raised); 1 (Salesforce Flex Credits, its stock drawdown "SaaSacre"); HubSpot agent price cuts (1); Clarify, Lightfield (U).
- **Competitors:** Attio, Day AI, Clarify, Lightfield, HubSpot Breeze, Salesforce Agentforce.
- **Why incumbents may lose:** a schema built around human data entry and seat revenue. But the space is well funded: competition, not opening.
- **Wedge / integration / pilot:** a shadow CRM synced from Gmail and calendar in hours; compare pipeline accuracy with Salesforce over 30 days.
- **Pricing:** usage. **Moat:** switching cost once it is the system of record. Takes years at enterprise.
- **CTO one-liner:** "A CRM nobody types into."
- **Kill risk:** already a funded race (Day AI, Attio); not a new insight.
- **Scores:** 9, 8, 6, 7, 6, 7, 7, 3, 4, 8, 6, 6 → **Avg 6.42**

## Thesis 5 — Metric Contracts (BI rebuilt for agent consumers)
- **Existing category:** BI (Tableau, Power BI, Looker), ~$47B (evidence 3).
- **Old assumption:** humans read dashboards and apply judgement to ambiguous metrics.
- **Why AI breaks it:** agents query metrics to make decisions (pricing, spend, alerts). Ambiguous definitions become automated wrong actions, so metrics need contracts, tests and change notifications for downstream agents.
- **New category:** a governed metric API with versioning, a blast-radius view of which agents consume each metric, and certification.
- **Buyer:** Head of Data. **Pain:** "the agent used the wrong revenue definition."
- **Evidence:** 3 (Omni $1.5B, OpenAI Frontier, Tableau MCP); Strategy/MicroStrategy blog on Google Next '26; AtScale "BI-embedded semantic layers fail AI"; dbt semantic layer (U).
- **Competitors:** Omni, dbt Labs, Cube, AtScale, Tableau, Snowflake/Databricks metric views, OpenAI Frontier.
- **Why incumbents may lose:** they won't. Omni has already won the funding; warehouses absorb it.
- **Wedge:** consumer-lineage/blast-radius for agent metric reads. **Integration:** days. **Pilot:** catalogue agent queries; flag definition drift.
- **CTO one-liner:** "Breaking-change alerts for metrics robots use."
- **Scores:** 8, 7, 6, 8, 7, 7, 7, 3, 3, 6, 4, 5 → **Avg 5.92**

## Thesis 6 — Digital Workforce Registry (HRIS/IAM for agents as workers)
- **Existing category:** HRIS plus IGA/IAM (Workday, Okta, SailPoint), ~$40B+ combined (U).
- **Old assumption:** every actor is an employee with a manager, a cost centre and a joiner/mover/leaver lifecycle; licences are bought per head.
- **Why AI breaks it:** agents outnumber employees, are spawned per task, and have owners, budgets and access but no HR record. Offboarding the human owner orphans agents.
- **New category:** a registry joining agent identity, human owner, budget, permissions and lifecycle events (owner leaves, so suspend and reassign).
- **Buyer:** CISO / CIO. **Pain:** orphaned agents with standing credentials.
- **Evidence:** 5 (NewCore $66M, Astrix, Defakto, Archestra, five deals in one week); 6 (Workday Agent System of Record); Okta for AI agents and Keycard $38M (search result); Microsoft Entra Agent ID (U).
- **Competitors:** Workday, Okta, Microsoft Entra, SailPoint, Astrix, Token Security, NewCore, Keycard.
- **Why incumbents may lose:** they won't; it is the most crowded square (STATUS T4, H, B+).
- **CTO one-liner:** "Offboarding for robots."
- **Scores:** 8, 7, 7, 7, 6, 7, 7, 2, 3, 6, 4, 5 → **Avg 5.75**

---

## Ranking and verdict
| Rank | Thesis | Avg |
|---|---|---|
| 1 | Inbound Agent Desk | 6.75 |
| 2 | Agent Work Ledger | 6.50 |
| 3 | Capture-native CRM | 6.42 |
| 4 | Context Compiler | 6.17 |
| 5 | Metric Contracts | 5.92 |
| 6 | Digital Workforce Registry | 5.75 |

None is near 8.5. Structural lesson for this track: categories where the **internal user** becomes an agent (CRM, BI, Jira, IAM, wiki) are re-platforming *inside* the incumbent or are already funded races within months. The only open shape is where the **external counterparty** becomes an agent (Thesis 1), because the incumbent's pricing (per AI resolution) and data model (conversation) both resist it. Next step for T1: measure real agent-originated contact share at 5 D2C/travel merchants before going deeper. It is pre-demand risk, the same failure mode as theses A and B+.
