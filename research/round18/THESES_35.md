# Round 18: 35 first-principles theses with immediate kill tests

Constraints applied: see FAILURE_TAXONOMY.md §4. Kill codes: F1 platform absorption, F2 visible-pain race, F3 pre-demand, F4 small TAM, F5 feature, F6 destination subsidy, CS cold-start, RG regulated.

| # | Structural question | Thesis (one line) | Kill test result |
|---|---|---|---|
| 1 | Software creation nearly free | **Build-replaces-buy:** find which SaaS tools a company's agents can now rebuild in-house, rebuild them, and run them; paid from the SaaS budget it cuts | **SURVIVE → evidence** |
| 2 | Software nearly free | AI-native MSP that operates/patches agent-built internal software | Services-heavy; fold into #1 as expansion |
| 3 | Software nearly free | Escrow/continuity for agent-built apps when the builder leaves | F5 |
| 4 | Software nearly free | Spec/requirements marketplace | F1 (Kiro, Tessl) |
| 5 | Intelligence abundant, what's scarce | Verified offline-business facts for agents calling SMBs | F1 (Google/Yelp), voice receptionists crowded |
| 6 | Attention scarce | Sender-bond / paid attention for B2B outreach | CS |
| 7 | Verified human scarce | Provenance certificate for human-made training data | F4 (~$50M, round 16) |
| 8 | Accountability scarce | Licensed professional sign-off as a service | RG |
| 9 | "Users are humans" breaks | **Agent-polluted product analytics:** de-agent funnels, A/B tests and attribution as agent traffic passes humans | **SURVIVE → evidence** |
| 10 | "Only humans make promises" breaks | **Commitment ledger for customer-facing AI agents:** every refund, discount, policy claim and date your agents promised, checked against real policy, with liability exposure | **SURVIVE → evidence** |
| 11 | "A photo is evidence" breaks | Proof-of-capture for warranty/refund/damage claims | F4 (6.5–6.6, found independently twice) — HOLD |
| 12 | "Tests measure humans" breaks | AI-proof hiring assessments | F2 crowded |
| 13 | "Work ≈ headcount" breaks | Workforce planning for human+agent orgs | F1 (Workday) |
| 14 | "Review is a control" breaks | Rubber-stamp detection | F1 (killed H) |
| 15 | Markets that exist because humans are expensive | **AI-deflation audit of services contracts:** outsourcers bill per FTE while their AI cuts the effort; recover the difference | **SURVIVE → evidence (merge with #1)** |
| 16 | Human labor markets | Upwork for agents | CS |
| 17 | Human labor markets | Expert-network replacement | F2 crowded |
| 18 | 10,000 autonomous workers | Agent performance/retirement management | F1 (killed B/E) |
| 19 | 10,000 autonomous workers | Internal token/compute allocation market | F5 |
| 20 | Systems built for human speed | **Agent-speed procurement:** approve new APIs/MCP servers/data vendors agents want in minutes (risk, legal terms, DPA, spend) | **SURVIVE → evidence** |
| 21 | Fraud models built for human velocity | False declines of legitimate agent purchases | F1 (Forter, Visa) |
| 22 | Agent-to-agent | Standard contract terms for agent transactions | Standards body, not a company |
| 23 | Agent-to-agent | Escrow/disputes for agent commerce | F3 |
| 24 | Unlimited generation | IP/brand infringement by AI content | F2 crowded |
| 25 | Unlimited generation | AI-generated package flood | F1 (Socket) |
| 26 | Bottleneck after execution | Real customer signal for 10x feature output | F2 crowded |
| 27 | Bottleneck after execution | Data-access approvals | F2 crowded |
| 28 | Bottleneck after execution | Test data for agents | F2 crowded |
| 29 | Frontier workaround | On-call ownership of agent-written code | F5 |
| 30 | Frontier workaround | Production-derived eval sets | F1/F2 evals |
| 31 | Compute as COGS | **ProsperOps for AI:** optimize AI commitments, priority/reserved tiers, batch routing and renewals for a share of savings | **SURVIVE → evidence** (untested survivor from round 1) |
| 32 | Humans as an input agents procure | Humans-as-API for agent verification/physical tasks | CS — watch |
| 33 | Agent externalities | Bill agents for costs they impose on third parties | F1 (Cloudflare, killed T4) |
| 34 | Pricing for agents | SaaS repricing ops for agent usage | F2 (Stigg, Schematic) |
| 35 | SaaS seat compression | Seat-loss intelligence for SaaS CFOs | F5 (killed reframe) |

## Survivors (6) and the theme they share
Three survivors (#1, #15, #31) share one under-explored theme: **AI deflation — money that should leave SaaS, services and compute budgets as agents do the work, but doesn't**. The buyer is the CFO, not the CTO; the incumbent (the vendor being paid) is structurally conflicted; savings are measurable in dollars. Possible one-sentence company: **"AI should make your vendors cheaper. We make sure it does."**

The other three (#9, #10, #20) are "victim-side" or "human-speed" problems surfaced by the taxonomy.

All six go to 60-day evidence and competitor checks.
