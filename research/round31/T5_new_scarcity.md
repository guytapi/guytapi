# Round 31 — Track 5: New Scarcity (2026-10-06)

Frame: once intelligence, code and execution are cheap, value moves to what stays scarce. For each scarce resource: the incumbent category that governs it (built for a human-speed world), and what would replace it.

| Scarce resource | Incumbent category (old-world design) | Replacement |
|---|---|---|
| Verification | Software testing/QA + code review (~$50B incl. services) | Evidence-based change acceptance (T5-1) |
| Authorization | IAM/IGA (~$20B; quarterly reviews, role-based) | Per-task mandates (T5-2) |
| Human attention | ITSM/approval workflow (ServiceNow, Jira; ~$15B) | Attention router / approval exchange (T5-3) |
| Context | Knowledge mgmt + data catalog (~$10B) | Context supply chain with freshness SLAs (T5-4) |
| Distribution | SEO/SEM/ad-tech/marketplaces (~$300B ad spend) | Agent-facing offer ledger (T5-5) |
| Compute (inference) | Cloud reserved instances / procurement (~$100B+) | SLA-bound inference capacity exchange (T5-6) |
| Coordination, physical access, accountability, reliable execution | Partly in prior rounds (round20 counter-signed records, H3 Verified Uptime, H2 hire-humans) | Not re-proposed here |

## Search evidence used (all URLs from WebSearch results; content not fetched directly, treat details as unverified)
- Sonar 2026 State of Code: AI = 42% of committed code; 96% don't fully trust it; 48% always check — https://www.sonarsource.com/company/press-releases/sonar-data-reveals-critical-verification-gap-in-ai-coding/
- GitLab 2026 AI Accountability Report (via search summary): 85% say the bottleneck moved to review/validation — https://devops.com/?p=188681 (unverified attribution)
- The Register, Jan 2026 — https://www.theregister.com/2026/01/09/devs_ai_code/
- Arcade $60M Series A (Jun 16 2026), agent authorization — https://aifunding.me/companies/arcade
- AIR $50M (Sep 2026), agent skill/tool vetting — https://aifunding.me/companies/air
- IETF draft agent decoupled authorization (Feb 2026) — https://www.ietf.org/archive/id/draft-chen-agent-decoupled-authorization-model-00.html
- NHI consolidation 2026: PANW/CyberArk closed Feb 11; Cisco/Astrix, CrowdStrike/SGNL, SailPoint/Entro, Cyera/Oasis, Okta/Permiso (~$200M); 109 machine identities per human — https://guptadeepak.com/identity-giants-bought-ai-agent-security/ , https://www.sdxcentral.com/news/palo-alto-networks-completes-25b-cyberark-deal-to-ignite-identity-in-ai-era/
- Context layer: Jedify $24M A (Norwest, Snowflake Ventures); Ekai $1.7M (Sep 2026); Gartner D&A 2026 "context layer became budget line" — https://www.businesswire.com/news/home/20260310566888/en , https://contextandchaos.substack.com/p/gartner-d-and-a-2026-where-the-context , https://atlan.com/know/why-ai-agents-need-an-enterprise-context-layer/
- Agent traffic: BrightEdge says agents ~15% of web traffic, most customers agents by end-2026; brands attributing ~10% revenue to agents — https://brightedge.com/news/press-releases/brightedge-data-ai-search-reaching-tipping-point-ai-agents-2026 , https://stellagent.ai/insights/ai-agents-driving-brand-revenue
- Sandboxes: Modal $355M at $4.65B, ~$300M ARR; Daytona $24M A — https://www.vcaonline.com/news/2026020508/daytona-raises-24m-series-a-to-give-every-agent-a-computer/ , https://rywalker.com/research/ai-agent-sandboxes
- Compute crunch: GPU lead times 36-52 weeks, spot gone, rental +~40%; agentic inference SLA-bound, price-inelastic — https://natesnewsletter.substack.com/p/executive-briefing-the-global-inference , https://tech-insider.org/nvidia-blackwell-gpu-rental-price-surge-ornn-index-2026/
- HITL: Stripe agent wallets release credentials after human approval (Sessions 2026); Gravitee HITL tasks — https://vp0.com/blogs/human-in-the-loop-approval-swipe-ui.md , https://www.gravitee.io/corpus/gen-1813/task-manager/human-in-the-loop-tasks.html

---

## T5-1 Evidence-based change acceptance (verification)
- **Existing category:** Software testing/QA + code review + change management (CAB). **Market:** ~$45-55B testing incl. services; tools ~$8B.
- **Old assumption:** humans write code slowly; a human reviewer reading the diff is the proof of correctness.
- **Why AI breaks it:** 42% of code AI-written, heading to 65%; review is the stated #1 bottleneck; 52% of devs don't always check. Reading diffs doesn't scale with generation.
- **New category:** acceptance by evidence — each change must ship with machine-checkable proof (behavioral diffs from replayed prod traffic, property tests, blast-radius estimate) and gets auto-accepted, sampled, or escalated by risk tier.
- **Product:** PR gate that replays a sanitized slice of prod traffic against old vs new build, returns "behavior changed here", and assigns a risk tier.
- **Buyer:** VP Eng / Head of Platform. **Pain:** review queues, reviewer burnout, incidents from rubber-stamped AI PRs.
- **Workaround:** AI reviewers (CodeRabbit, Greptile, Copilot review), more tests written by AI (which share the model's blind spots).
- **Competitors:** direct: Qodo, Meticulous, Speedscale, Diffblue; adjacent: GitHub/Cursor native merge (killed T3), Sonar, Harness.
- **Why incumbents may lose:** reviewers judge text; replay needs capturing prod traffic and deterministic env, which code hosts don't own. Weak — observability vendors (Datadog) could add it.
- **Wedge:** API-heavy backend teams with >50% AI PRs. **Integration:** days (traffic capture sidecar + CI step). **30-day pilot:** measure % PRs auto-accepted with zero rollback vs baseline. **Pricing:** per verified change ($1-5) or per service. **Expansion:** deploy gate → change-management/CAB replacement → audit evidence. **Moat:** 10: none; 100: risk models from outcome data; 1,000: cross-customer regression-pattern corpus. **$10B case:** replaces human review + CAB as the permission to ship for all AI-written software.
- **CTO one-liner:** "Stop reading AI diffs; we show you what behavior actually changed."
- **Scores:** Market 8, Transformation 8, Urgency 7, Why-now 8, Reach buyer 7, Speed to pilot 6, Integration 5, Competitive opening 4, Differentiation 5, Expansion 7, Moat 5, VC 7 → **Avg 6.4**
- **Kill risk:** crowded (Meticulous, Qodo) and close to killed T3/W; prod-traffic capture is a security-review blocker.

## T5-2 Per-task mandates (authorization)
- **Existing category:** IAM/IGA/PAM (~$20B+). **Old assumption:** identities are humans with stable roles; access reviewed quarterly.
- **Why AI breaks it:** 109 machine identities per human; agents need access for one task for minutes; roles are the wrong unit.
- **New category:** mandate-based authorization — a signed, scoped, expiring grant tied to an intent ("refund ≤$200 for ticket 123"), issued just-in-time and logged.
- **Product:** mandate issuer + policy decision point that MCP gateways and SaaS APIs query.
- **Buyer:** CISO / Head of IAM. **Pain:** standing over-privileged agent tokens.
- **Competitors:** Arcade ($60M), Permit.io, AuthZed, Okta (Permiso, Auth0 for AI), PANW/CyberArk, CrowdStrike/SGNL, Cisco/Astrix, SailPoint.
- **Why incumbents may lose:** they won't — six acquisitions in 2026 show incumbents absorbing it. Only angle: cross-company mandates (agent of firm A acting in firm B's system), which no single IdP owns.
- **Wedge:** SaaS vendors exposing MCP servers that need to accept outside agents. **Integration:** days. **Pilot:** one SaaS issues mandate-scoped tokens to 3 customer agents. **Pricing:** per active mandate/month. **Moat:** network of issuers/verifiers at 1,000. **$10B case:** the OAuth of delegated agent work.
- **CTO one-liner:** "Every agent call carries a receipt for what it was allowed to do, and why."
- **Scores:** Market 9, Transformation 8, Urgency 7, Why-now 8, Reach 6, Speed 6, Integration 6, Opening 3, Differentiation 4, Expansion 8, Moat 6, VC 6 → **Avg 6.4**
- **Kill risk:** strongest consolidation of any category in the scan; overlaps killed T4.

## T5-3 Attention router / approval exchange (human attention)
- **Existing category:** ITSM & approval workflows (ServiceNow, Jira Service Mgmt, email/Slack approvals) (~$15B).
- **Old assumption:** humans create requests; approval queues are low-volume and each tool can have its own inbox.
- **Why AI breaks it:** each agent product ships its own HITL prompts (Stripe wallet approvals, coding agents, support agents). Approvals grow with agent count; human attention stays flat. The scarce input is a qualified human's 30 seconds.
- **New category:** one cross-vendor queue that routes each agent's approval to the right human with full context, deduplicates, batches, sets SLOs, and learns which approvals can be auto-granted (and turns them into policy).
- **Product:** API `request_approval(action, evidence, risk)` + Slack/mobile swipe UI + auto-approve policy learned from history.
- **Buyer:** COO / VP Ops, or Head of AI Platform. **Pain:** agents stalled waiting; approval fatigue that becomes rubber-stamping.
- **Workaround:** each vendor's own inbox, Slack DMs. **Competitors:** ServiceNow AI Control Tower, Gravitee, Courier, HumanLayer, Microsoft Copilot Studio approvals.
- **Why incumbents may lose:** ServiceNow is ticket-centric (minutes-hours SLA); agent vendors won't route to a rival's queue. A neutral layer benefits from cross-vendor data. Moderate: Slack/Microsoft could own the surface.
- **Wedge:** companies running 3+ agent products with HITL. **Integration:** hours (SDK). **Pilot:** median approval latency and % auto-granted after 30 days. **Pricing:** per approval decision or per approver seat. **Expansion:** approval history → accountability record → policy authoring. **Moat:** 100: learned auto-approve policies; 1,000: vendor integrations as standard. **$10B case:** the system of record for human judgment in an agent company.
- **CTO one-liner:** "One inbox for every agent that needs a human, and fewer of them every week."
- **Scores:** Market 7, Transformation 8, Urgency 6, Why-now 8, Reach 7, Speed 8, Integration 8, Opening 6, Differentiation 5, Expansion 7, Moat 5, VC 7 → **Avg 6.8**
- **Kill risk:** feature-sized if Slack/Teams standardize an approval card; ties to round20 counter-signed-record work.

## T5-4 Context supply chain (context)
- **Existing category:** knowledge management + data catalog/semantic layer (Confluence, Glean, Collibra, Atlan) (~$10B).
- **Old assumption:** humans search, read and judge freshness themselves.
- **Why AI breaks it:** agents act on what they retrieve with no judgment; 57% saw confident-wrong failures; Gartner treats the context layer as a budget line.
- **New category:** context with ownership, freshness SLAs and lineage; stale facts expire, owners get pinged, agents get "trust score" per fact.
- **Product:** fact registry pulled from systems of record with owner, validity window and conflicts flagged.
- **Buyer:** CDO / Head of AI Platform. **Competitors:** Atlan, Jedify ($24M), Glean, Snowflake/Databricks semantic layers, Quantexa, Collibra.
- **Why incumbents may lose:** catalogs index tables, not facts in docs/tickets; weak — Glean and Atlan are moving fast.
- **Wedge:** support/sales agents giving wrong policy answers. **Integration:** weeks. **Pilot:** wrong-answer rate on 200 eval questions. **Pricing:** per agent/connected source. **Moat:** low until owner workflows are embedded. **$10B case:** the source of truth agents trust.
- **CTO one-liner:** "Every fact your agents use has an owner and an expiry date."
- **Scores:** Market 7, Transformation 7, Urgency 7, Why-now 8, Reach 6, Speed 5, Integration 4, Opening 3, Differentiation 4, Expansion 7, Moat 5, VC 6 → **Avg 5.8**

## T5-5 Agent-facing offer ledger (distribution)
- **Existing category:** SEO/SEM, ad-tech, marketplaces (~$300B ad spend). **Old assumption:** humans discover products by browsing pages and clicking ads.
- **Why AI breaks it:** agents ~15% of traffic, invisible to GA; ~10% revenue via agents for some brands; ads have no slot in an agent answer.
- **New category:** machine-readable, signed offers (price, terms, availability, warranties) that agents can query and cite, with attribution back to the seller.
- **Product:** offer feed + agent-traffic analytics + conversion attribution.
- **Buyer:** CMO / VP Ecommerce. **Competitors:** Profound, BrightEdge, Scrunch, Yotpo, Shopify/OpenAI/Google agentic checkout protocols, Stripe.
- **Why incumbents may lose:** agent platforms set protocols themselves; startups become feed tooling. Overlaps killed thesis A.
- **Wedge:** mid-market DTC brands. **Integration:** hours. **Pilot:** agent-attributed revenue lift. **Pricing:** % of attributed GMV. **Moat:** low. **$10B case:** the ad network of agent commerce, only if platforms allow third parties.
- **CTO one-liner:** "Know what agents say about you and give them signed facts to quote."
- **Scores:** Market 9, Transformation 9, Urgency 7, Why-now 8, Reach 7, Speed 8, Integration 8, Opening 3, Differentiation 3, Expansion 6, Moat 3, VC 5 → **Avg 6.3**
- **Kill risk:** GEO tooling crowded; platforms own the rails.

## T5-6 SLA-bound inference capacity exchange (compute)
- **Existing category:** cloud reserved capacity / procurement (~$100B+). **Old assumption:** compute is elastic and on-demand; workloads tolerate delay.
- **Why AI breaks it:** agent inference is SLA-bound and price-inelastic; GPU lead times 36-52 weeks; spot gone; hyperscalers are competitors for their own capacity.
- **New category:** buyers reserve guaranteed tokens/sec with failover across providers and neoclouds, settle like a capacity market.
- **Product:** routing layer with guaranteed throughput contracts and automatic failover.
- **Buyer:** Head of AI Infra / CFO. **Competitors:** OpenRouter, Together, Fireworks, Silicon Data/CME futures, Ornn index, Modal, cloud marketplaces.
- **Why incumbents may lose:** neutral broker across providers; but lab-direct deals and capital needs dominate. Echoes killed B and K.
- **Wedge:** AI-native apps hit by rate limits. **Integration:** hours. **Pilot:** uptime under rate-limit events. **Pricing:** spread on capacity. **Moat:** liquidity at 1,000. **$10B case:** the capacity market for intelligence.
- **CTO one-liner:** "Guaranteed tokens per second, whoever's GPUs they come from."
- **Scores:** Market 9, Transformation 7, Urgency 8, Why-now 8, Reach 6, Speed 7, Integration 8, Opening 4, Differentiation 4, Expansion 6, Moat 5, VC 6 → **Avg 6.5**
- **Kill risk:** capital-intensive; OpenRouter plus futures markets already exist.

---

## Verdict
None reaches 8.5. Ranking: T5-3 Attention router 6.8 > T5-6 Inference capacity 6.5 > T5-1 Evidence-based acceptance 6.4 = T5-2 Mandates 6.4 > T5-5 Offer ledger 6.3 > T5-4 Context supply chain 5.8.
Pattern: every scarce resource with a visible gap is already funded or being bought up (NHI: six acquisitions in 2026). The least-occupied one is **human attention**: incumbents treat approvals as tickets, and agent vendors each keep their own inbox. Best combined with the round20 counter-signed-records candidate, since approval decisions are the records. 14-day test: find 5 companies running 3+ HITL agent products and count pending approvals per day and median wait.
