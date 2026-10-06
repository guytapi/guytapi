# Round 31 — Track 4: Agent-first software (product primitive changes)

Date: 2026-10-06. Searches used: 10/20. URLs below came from search results; I did not open the pages (WebFetch is blocked), so the figures are as the search snippets reported them. Items marked [unverified] are my inference.

## Cross-track finding
In every category in this track, the incumbent or a funded startup already stated the primitive shift in public in 2026:
- Linear's CEO said "issue tracking is dead" (Mar 25 2026). He reported that 25% of new issues are created by agents and that 75% of enterprise workspaces have agents installed.
- Salesforce launched Headless 360 (Apr 15 2026), exposing its whole platform via API, MCP and CLI.
- Mintlify reported 257M agent requests against 131M human page loads (Aug 2026).
- Rillet raised $100M at a $1B valuation (Aug 2026) for agents inside the general ledger.
- AgentMail raised a $6M seed from General Catalyst (Mar 2026) and reports 500+ B2B customers.
- Nylas launched Agent Accounts, which give agents their own hosted email and calendar.
- Semantic layers have gone native in the warehouses: Snowflake Semantic Views, Databricks Metric Views, and the dbt MCP server called from Cortex.

The STATUS.md lesson holds here too: the shift is real, but the visible gaps are already funded or already shipped by incumbents. The remaining white space is narrower. It is the primitives incumbents cannot easily adopt because their seat-priced, GUI-centric data model resists them.

Sources:
- https://www.idlen.io/news/linear-agent-issue-tracking-dead-ai-agents-product-management
- https://www.devclass.com/development/2026/03/27/linear-moves-sideways-to-agentic-ai-as-ceo-declares-issue-tracking-dead/5211661
- https://www.techwyse.com/news/industry-news/salesforce-headless-360-tdx-2026-announcement
- https://redresscompliance.com/research-notes/salesforce-headless-360-january-2027
- https://www.mintlify.com/blog/the-state-of-knowledge-2026-highlights
- https://fintech.global/2026/08/21/ai-erp-challenger-rillet-raises-100m-at-1bn-value/
- https://thenextweb.com/news/agentmail-raises-6m-seed-ai-agent-email-inboxes
- https://www.nylas.com/?p=5046
- https://atlan.com/know/best-semantic-layer-tools/
- https://docs.getdbt.com/docs/dbt-ai/integrate-mcp-snowflake-cortex
- https://extruct.ai/data-room/ai-native-crm
- https://aifunding.me/companies/lightfield

---

## Thesis 4.1 — CRM becomes an agent-queryable customer state machine
- **Existing category:** CRM (~$80-100B; Salesforce ~$38B revenue).
- **Old assumption:** Reps type records into forms. The CRM is a database plus a UI, priced per seat.
- **Why AI breaks it:** Agents write most activity and read state via MCP. Records become an event log of commitments and states (lead → qualified → contracted) with transition rules. Salesforce credit forecasts ran 40-70% below actual once agents went live, per Redress Compliance.
- **New category:** A customer state machine. Every account is a typed state with guarded transitions and an event log, metered per transition rather than per seat.
- **Product:** An event-sourced customer graph plus a transition API plus a policy engine ("an agent may move to Proposal only if X"), with a human UI as a secondary view.
- **Buyer:** VP RevOps / CTO at an AI-native company.
- **Pain:** Salesforce agent costs are unpredictable. Agents corrupt fields. There is no audit of which agent changed what.
- **Evidence:**
  1. Lightfield $47M Series A (Sep 2026), "CRM for agent-driven companies"
  2. 23 AI-native CRMs with $515M+ raised (Extruct, Jun 2026)
  3. Salesforce Headless 360 (Apr 2026)
  4. Unpriced Salesforce meters for record operations and process invocations
  5. Fixture (YC W26)
  6. A $250M-funded agentic challenger (Jul 2026, name unverified)
- **Workaround:** Salesforce plus Agentforce credits; Attio/HubSpot APIs.
- **Competitors:**
  - Direct: Lightfield, Attio, Day.ai, Fixture
  - Adjacent: Salesforce, HubSpot
- **Why incumbents may lose:** Seat revenue cannibalization. Their schemas are 20 years of customization that agents cannot reason over.
- **Wedge:** AI startups with fewer than 200 employees, where most outbound activity is agentic.
- **Integration:** Days. Email/calendar sync plus import.
- **30-day pilot:** Run the agent SDR's writes through the state machine and measure invalid transitions blocked.
- **Pricing:** Per state transition plus a platform fee.
- **Expansion:** CPQ, contracts, billing triggers.
- **Moat:** At 10 customers, none. At 100, transition-template library. At 1,000, cross-company benchmarks [weak].
- **$10B case:** Displaces CRM for the agent-native cohort as it ages.
- **CTO one-liner:** "Our CRM is an API with rules. Agents call it, humans glance at it."
- **Scores:**

| Mkt | Transf | Urg | Why-now | Buyer | Pilot | Integ | Opening | Diff | Expand | Moat | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 10 | 7 | 5 | 7 | 6 | 6 | 6 | 4 | 5 | 8 | 5 | 7 | **6.3** |

  Killer: crowded (23+ funded), and Salesforce/HubSpot ship headless.

## Thesis 4.2 — Ticketing replaced by work contracts
- **Existing category:** Issue/work management (Jira, Linear, Asana, ServiceNow ITSM; ~$15-25B).
- **Old assumption:** A ticket is a note for a human. Done means a human says so.
- **Why AI breaks it:** 25% of new Linear issues are created by agents, and agent work volume grew 5x in 3 months. An agent needs a machine-checkable spec: inputs, acceptance tests, budget, deadline, permissions. It also needs verifiable completion.
- **New category:** A work-contract ledger. Each unit of work is a contract carrying an executable acceptance criterion, a cost cap and an escrowed result. It is dispatched to any agent (Claude Code, Devin, Copilot) or to a human.
- **Product:** A contract spec (YAML) plus a dispatcher plus a verifier that runs tests or evals before closing, plus per-agent cost and quality scorecards.
- **Buyer:** VP Engineering / Head of Platform.
- **Pain:** Agent PRs pile up unverified, there is no comparison of cost per completed task across agents, and spec ambiguity drives rework.
- **Evidence:**
  1. Linear "issue tracking is dead" (Mar 2026)
  2. Linear Insights filters work by agent session
  3. Jira assigns to Rovo Dev / Copilot
  4. Linear Coding Agent on its roadmap
  5. The "issue tracker as agent dispatch surface" pattern (agentpatterns.ai)
- **Workaround:** Linear/Jira plus GitHub Actions plus manual review.
- **Competitors:**
  - Direct: Linear, Atlassian Rovo
  - Adjacent: Factory, Devin, GitHub Agent HQ
- **Why incumbents may lose:** Linear is moving fast here, so loss is weak. A neutral multi-agent verifier is the only gap. Note T3 (autonomous merge) was killed when GitHub/Cursor shipped it.
- **Wedge:** Teams running 3+ coding agents that want cross-agent bake-offs.
- **Integration:** Hours. GitHub app plus Linear sync.
- **30-day pilot:** Route 200 tasks and report cost and acceptance rate per agent.
- **Pricing:** Per verified contract.
- **Expansion:** Non-code work (ops, data, support).
- **Moat:** At 10 customers, none. At 100, agent performance dataset. At 1,000, a routing benchmark.
- **$10B case:** Becomes the procurement layer for all agent labor.
- **CTO one-liner:** "We don't file tickets, we post contracts. Whoever passes the tests cheapest gets paid."
- **Scores:**

| Mkt | Transf | Urg | Why-now | Buyer | Pilot | Integ | Opening | Diff | Expand | Moat | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 8 | 6 | 8 | 7 | 8 | 8 | 3 | 4 | 8 | 4 | 7 | **6.6** |

  Killer: Linear and GitHub own the surface.

## Thesis 4.3 — Docs become executable knowledge (skills plus verified procedures)
- **Existing category:** Knowledge management, developer docs and wikis (Confluence, Notion, Mintlify, ReadMe, Glean; ~$10-20B).
- **Old assumption:** Humans read prose.
- **Why AI breaks it:** Agents are now the majority readers (Mintlify: 2:1 agent to human traffic). They need runnable procedures (skills, MCP tools, test-verified snippets), and stale docs make agents fail at scale.
- **New category:** Executable knowledge base. Each procedure is a versioned skill with tests run continuously against the live product, so a doc fails CI when the product changes.
- **Product:** A repo of skills/procedures plus a nightly agent harness that executes each one against staging, plus auto-PRs when it breaks.
- **Buyer:** Head of DevRel / Platform Engineering.
- **Pain:** Agents hallucinate outdated API usage, which creates support load and lost activation.
- **Evidence:**
  1. Mintlify agent traffic report (Aug 2026)
  2. Mintlify per-site MCP and skill.md
  3. Salesforce Ventures "AI native knowledge infrastructure" thesis
  4. Tessl (skills) noted killed in STATUS
  5. llms.txt adoption
- **Workaround:** Mintlify plus manual QA.
- **Competitors:** Mintlify (strongest), ReadMe, GitBook, Tessl, Context7.
- **Why incumbents may lose:** They don't, mostly. Mintlify is already there. A continuous-execution verifier is the only differentiator, and it is copyable.
- **Wedge:** API companies whose activation depends on coding agents.
- **Integration:** Days.
- **30-day pilot:** Execute 100 doc procedures and report the failure rate.
- **Pricing:** Per verified procedure.
- **Expansion:** Internal runbooks and SOPs.
- **Moat:** Low.
- **$10B case:** Weak.
- **CTO one-liner:** "Our docs are tests that agents run."
- **Scores:**

| Mkt | Transf | Urg | Why-now | Buyer | Pilot | Integ | Opening | Diff | Expand | Moat | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 8 | 6 | 8 | 7 | 8 | 8 | 3 | 4 | 6 | 3 | 5 | **6.0** |

## Thesis 4.4 — Dashboards replaced by queryable metric contracts
- **Existing category:** BI/analytics (Tableau, Looker, Power BI; ~$30B).
- **Old assumption:** Humans look at charts. Metric definitions live in dashboards.
- **Why AI breaks it:** Agents query metrics via MCP thousands of times per day and act on them, so a wrong definition becomes a wrong action.
- **New category:** Metric contracts. Each metric carries a signed definition, freshness SLA, owner, allowed consumers and action thresholds. Agents subscribe to it rather than view it.
- **Product:** A semantic layer plus contract enforcement plus agent query audit.
- **Buyer:** Head of Data.
- **Pain:** Ungoverned agent SQL gives conflicting numbers.
- **Evidence:**
  1. dbt MCP from Cortex
  2. Snowflake Semantic Views
  3. Databricks Metric Views
  4. Cube's "semantic layer for agents 2026"
  5. Atlan semantic-layer roundups
- **Workaround:** dbt SL / Cube.
- **Competitors:** dbt, Cube, AtScale, Snowflake, Databricks, Looker.
- **Why incumbents may lose:** They don't. The warehouses absorb it natively.
- **Wedge:** None clear.
- **Integration:** Days.
- **30-day pilot:** Audit agent queries.
- **Pricing:** Per query.
- **Expansion:** Data products.
- **Moat:** Low.
- **$10B case:** Only if one is a warehouse.
- **CTO one-liner:** "Agents don't read dashboards, they call metrics."
- **Scores:**

| Mkt | Transf | Urg | Why-now | Buyer | Pilot | Integ | Opening | Diff | Expand | Moat | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 7 | 5 | 7 | 7 | 7 | 7 | 2 | 3 | 6 | 3 | 4 | **5.5** |

  Killer: an incumbent can add it trivially.

## Thesis 4.5 — Email/calendar as an agent communication and commitment layer
- **Existing category:** Email/calendar APIs and communications platforms (Nylas, SendGrid, Twilio, Google/Microsoft; ~$20B+).
- **Old assumption:** A mailbox belongs to a human. A meeting is a human time slot.
- **Why AI breaks it:** Agents need their own inboxes, identities and negotiation of slots and commitments with other agents. A message becomes a structured offer or accept rather than prose.
- **New category:** An agent-native messaging plus commitments protocol over email. It parses requests into typed commitments (meet, deliver, pay), tracks them, and provides counter-signed confirmations. This overlaps with the Round-20 counter-signature item.
- **Product:** Inbox API plus commitment extraction plus a shared ledger.
- **Buyer:** CTO of an agent product.
- **Pain:** Agent emails land in spam, there is no identity, and commitments get lost.
- **Evidence:**
  1. AgentMail $6M (GC), 500+ B2B customers
  2. Nylas Agent Accounts (2026)
  3. Nylas report: 94% would switch vendors for agentic capability
  4. Lightfield/CRMs syncing agent mail
  5. Round-20 counter-signature evidence
- **Workaround:** Gmail Workspace accounts per agent.
- **Competitors:** AgentMail, Nylas, Resend, Google/Microsoft.
- **Why incumbents may lose:** Google and Microsoft per-seat licensing penalizes agent mailboxes [unverified], and their deliverability rules target bots.
- **Wedge:** Agent startups (devs) at $X per inbox.
- **Integration:** Hours.
- **30-day pilot:** 100 agent inboxes.
- **Pricing:** Per inbox plus per commitment.
- **Expansion:** Calendar, voice, identity.
- **Moat:** At 100+ customers, sender reputation network.
- **$10B case:** The Twilio of agents.
- **CTO one-liner:** "Every agent gets an address, a calendar and a ledger of what it promised."
- **Scores:**

| Mkt | Transf | Urg | Why-now | Buyer | Pilot | Integ | Opening | Diff | Expand | Moat | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 7 | 6 | 8 | 8 | 9 | 9 | 4 | 5 | 7 | 5 | 6 | **6.75** |

  Killer: AgentMail and Nylas are already here, and the commitment ledger is the only new part.

## Thesis 4.6 — ERP transaction layer: agent-postable ledger with guarded journal contracts
- **Existing category:** ERP/accounting (~$50-100B).
- **Old assumption:** Accountants key entries and close monthly.
- **Why AI breaks it:** Agents post continuously, so the ledger needs per-agent permissions, policy-checked postings and continuous close.
- **New category:** An agent-native GL.
- **Product:** A real-time ledger with policy-guarded postings and human sign-off queues.
- **Buyer:** CFO / Controller.
- **Pain:** Close takes 10+ days, and agents can't safely write to NetSuite.
- **Evidence:**
  1. Rillet $100M at $1B, 600+ customers, new ARR doubled in 3 months
  2. EY alliance
  3. Partner of more than half of the top-20 CPA firms
  4. Campfire and Light (other AI ERPs, from memory, unverified)
  5. NetSuite/SAP agent announcements [unverified]
- **Workaround:** NetSuite plus close tools.
- **Competitors:** Rillet, Campfire, Digits, NetSuite.
- **Why incumbents may lose:** NetSuite's batch-era data model.
- **Wedge:** Already taken by Rillet.
- **Integration:** Weeks to months (migration).
- **30-day pilot:** Hard.
- **Pricing:** Platform fee.
- **Expansion:** AP/AR/procurement.
- **Moat:** High once adopted (switching costs).
- **$10B case:** Real, but owned by Rillet.
- **CTO one-liner:** "Agents post, the ledger enforces policy, humans sign exceptions."
- **Scores:**

| Mkt | Transf | Urg | Why-now | Buyer | Pilot | Integ | Opening | Diff | Expand | Moat | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 9 | 7 | 6 | 7 | 5 | 3 | 3 | 3 | 5 | 8 | 8 | 6 | **5.8** |

  Killer: Rillet has a lead, migration is slow, and the market sits near regulated finance.

---

## Ranking
1. 4.5 Agent comms + commitments: 6.75
2. 4.2 Work contracts: 6.6
3. 4.1 CRM state machine: 6.3
4. 4.3 Executable docs: 6.0
5. 4.6 Agent-native GL: 5.8
6. 4.4 Metric contracts: 5.5

None reaches 8.5. The recurring pattern is that the primitive shift is real, but incumbents (Linear, Salesforce, Mintlify, Snowflake) declared it themselves in 2026, and funded startups (Lightfield, Rillet, AgentMail) occupy the startup slots.

The most promising thread is the shared "commitment" primitive across 4.1, 4.2 and 4.5: typed, counter-signed promises between agents and parties. That converges with the Round-20 counter-signature item (~6.4) and is the one layer no incumbent owns.
