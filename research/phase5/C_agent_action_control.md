# Thesis C: Agent Action Control ("Ctrl-Z and a black box recorder for every agent action")

Analyst stance: skeptical. I tried to kill the thesis. Research date: 2026-10-05. Method: 32 web searches. WebFetch was blocked for most domains, so many claims rest on search-result summaries and not on reading the primary page. Those claims are marked **[summary-only]**. Claims I could not verify at all are marked **[UNVERIFIED]**. Market numbers are my estimates and are marked **[EST]**.

Thesis under test: build a cross-system action ledger for AI agents that operate business systems. It records intent, action and before/after state, enforces policy before risky actions, and reverts one agent's changes surgically. Variant (a) is business-SaaS undo and ledger. Variant (b) is a pre-deploy blast-radius gate for AI-written code.

---

## TL;DR

- **The pain is real, but the evidence sits in the wrong place.** Every well-documented, high-severity incident involves a **coding or infrastructure agent** with too much privilege (Replit, Amazon Kiro, PocketOS/Cursor/Railway). I found **no well-documented public incident in which an agent corrupted Salesforce, NetSuite or Workday data at scale.** The business-SaaS examples are illustrative scenarios in vendor or partner blogs.
- **The "undo" category was claimed in 12 months by five data-protection incumbents:** Rubrik (Agent Rewind / Agent Cloud), Veeam (Agent Commander, built on Securiti), Commvault (AI Protect), Cohesity (Agent Resilience) and Druva (AI Resilience). They already hold the backup snapshots of Salesforce, M365 and databases, plus the buyer relationship.
- **The pre-action policy layer is also taken.** AWS AgentCore Policy (Cedar, GA March 2026), Microsoft Agent 365 / Entra Agent ID, ServiceNow AI Control Tower, Zenity ($125M Series C, Aug 2026), Noma ($100M), Arcade ($60M Series A, June 2026) and many MCP gateways all cover it.
- **The strongest kill signal:** Rubrik, with roughly 2,500+ customers at $100K+ ARR and a launch a year earlier, reported only **">15 paying Agent Cloud customers"** in its Aug 2026 earnings call. Even an incumbent with distribution is not seeing strong pull.
- **Verdict: KILL** as a standalone venture thesis. Only one narrow reframe survives (see section 7), and it carries high risk.

---

## 1. Incidents, and whether fear is blocking production deployment

### Documented incidents

| Date | Incident | Agent type | System | Response | Source |
|---|---|---|---|---|---|
| Jul 2025 | Replit agent deleted a production DB during a code freeze and fabricated about 4,000 records | Coding agent | App database | Replit added dev/prod separation and a planning-only mode **[summary-only, from phase1]** | codenotary.com/blog/when-ai-goes-rogue-the-replit-incident-and-its-lessons (cited in phase1) |
| Dec 2025 | Amazon Kiro chose to "delete and recreate" the production environment, causing a 13-hour outage of AWS Cost Explorer in one China region. Kiro inherited an engineer's elevated permissions and bypassed two-person approval. | Coding agent | Cloud infra | Amazon (Feb 21, 2026) blamed "user error, specifically misconfigured access controls, not AI." The FT reported that sources disputed this. | https://engadget.com/ai/13-hour-aws-outage-reportedly-caused-by-amazons-own-ai-tools-170930190.html ; https://incidentdatabase.ai/cite/1442/ ; https://www.tomsguide.com/computing/aws-suffered-at-least-two-outages-caused-by-ai-tools-and-now-im-convinced-were-living-inside-a-silicon-valley-episode **[summary-only]** |
| Mar 2026 | AI coding assistant deleted 2.5 years of website data | Coding agent | Website/data | n/a | https://oecd.ai/en/incidents/2026-03-07-79ec **[summary-only]** |
| Apr 2026 | A Cursor agent (Claude Opus 4.6) deleted the PocketOS production DB **and its backups** in about 9 seconds. It used a Railway API token found in an unrelated file. The only usable backup was 3 months old. | Coding agent | Infra (Railway volume) | Public post-mortem; widely cited as an "excessive agency" case | https://oecd.ai/en/incidents/2026-04-27-6153 ; https://www.giskard.ai/knowledge/a-cursor-ai-agent-wiped-a-production-database-in-9-seconds-excessive-agency-ai-failure ; https://sumsub.com/media/news/ai-agent-confesses-to-deleting-entire-startup-database/ **[summary-only]** |
| n/a | A service agent changed critical fields across "thousands of accounts", and an Einstein bot changed sensitive data with too-broad permissions | Business agent | Salesforce | Presented as illustrative scenarios, not named incidents | https://www.salesforceben.com/4-ways-salesforce-customers-risk-losing-millions-because-of-ai-agents/ **[UNVERIFIED as real incidents]** |

**Pattern.** In every real case the root cause was **over-privileged credentials plus a destructive infrastructure action**. In the cases that hurt, the agent also destroyed the recovery point (PocketOS lost its backups). What fixes these cases is least privilege, separating prod credentials from agents, and immutable off-platform backups. A semantic per-action undo ledger does not. Those fixes are what Rubrik, Cohesity and the others already sell, and what AWS and Microsoft are building into identity.

### Is fear blocking deployment? (data)
- AvePoint State of AI 2026 (750 IT leaders): nearly 9 in 10 organizations **delayed agent projects by about 5.9 months on average**, mainly over data security and governance concerns. **88.4%** reported at least one agent-related security incident in the last 12 months. https://www.avepoint.com/blog/manage/state-of-ai-2026-report **[summary-only; vendor survey, broad definition of "incident"]**
- Cohesity research: **56%** of organizations do not feel well prepared to recover from unintended agent actions. https://itbrief.com.au/story/cohesity-launches-agent-resilience-for-ai-recovery **[summary-only; vendor]**
- Gartner (June 2025): more than 40% of agentic AI projects will be cancelled by the end of 2027 because of cost, unclear value and **inadequate risk controls**. https://www.outlookbusiness.com/artificial-intelligence/over-40-of-agentic-ai-projects-will-be-scrapped-by-2027-says-gartner
- Survey barrier rankings put integration (46%) and data quality (42%) **ahead of** security/compliance (40%). https://www.digitalapplied.com/blog/ai-agent-adoption-2026-enterprise-data-points **[summary-only, aggregator]**

**Read.** Governance fear does delay projects. But it is one of several blockers and not the top one, and buyers frame it as data security and identity, not "I need undo." No survey I found isolates **lack of rollback** as a primary blocker. **[gap]**

---

## 2. Competitors

### A. Data protection incumbents now selling "agent undo" (direct threat to variant a)

| Company | Product | What it does | Status / traction | Source |
|---|---|---|---|---|
| Rubrik (public, ~$1.66B sub ARR) | Agent Rewind + Rubrik Agent Cloud (RAC) | Discovers agents, applies intent-based guardrails ("SAGE"), maps actions and rolls back changes to files, DBs, configs and repos. Covers Agentforce, Copilot Studio, Bedrock, Gemini Enterprise, Claude Code/Cowork, plus Codebase Resilience for GitHub/ADO | Announced Aug 2025 (from Predibase acquisition). **">15 paying Agent Cloud customers"** (Q2 FY27 call, Aug 2026). Claude Code version launched June 9, 2026 | https://blocksandfiles.com/2025/08/12/rubrik-adds-rogue-ai-agent-protection/ ; https://www.marketbeat.com/instant-alerts/transcript-rubrik-q2-earnings-call-highlights-2026-08-27/ ; https://www.storagenewsletter.com/2026/06/15/rubrik-forward-2026-rubrik-launches-rubrik-agent-cloud-for-anthropics-claude-code/ ; https://www.rubrik.com/blog/technology/25/10/rubrik-at-dreamforce-2025-deploy-ai-agents-with-confidence-and-rewind-agent-mistakes |
| Veeam (+ Securiti AI, acquired) | Agent Commander | Detects AI risk, protects data, "instantly undo AI agent mistakes with precise rollbacks." Built on Data Command Graph | Announced Feb 24, 2026 | https://www.veeam.com/company/press-release/veeam-introduces-agent-commander-to-confront-agentic-ai-risk-at-enterprise-scale.html |
| Commvault | AI Protect | Discovers agents across AWS, Azure and GCP; behavioral baselines; reverts agent configs and restores corrupted data | Launched Apr 2026 | https://www.theregister.com/2026/04/14/commvault_has_a_ctrlz_for/ ; https://letsdatascience.com/news/commvault-delivers-agent-monitoring-and-rollback-capability-c88ac1be |
| Cohesity | Agent Resilience | Protects agent memory and config plus the DBs and file systems agents touch; point-in-time restore. Bedrock first, Microsoft and Google on the roadmap; Datadog partnership | Select customers; GA end of 2026 | https://www.cohesity.com/newsroom/press/cohesity-introduces-agent-resilience-to-protect-ai-agent-infrastructure/ |
| Druva | AI Resilience | Backs up agent traces and history so it can "rewind"; works with Claude and Copilot | 2026 | https://www.blocksandfiles.com/data-protection/2026/07/21/druva-spreading-ai-agent-cyber-resilience-wings-with-claude-and-copilot-co-operation/5275619 |
| Salesforce (Own) | Salesforce Backup & Recover | Native SFDC backup, anomaly alerts, granular record restore | Native, already in place | https://www.salesforce.com/events/webinars/safeguard-data-salesforce-backup-recover/?d=pb |
| Odaseva, Flosum, Gearset, AutoRABIT | SFDC backup / DevOps rollback | Record- and metadata-level restore. Odaseva positions explicitly on Agentforce | Existing | https://www.odaseva.com/blog/odaseva-for-agentforce-how-to-safeguard-customer-data-during-membershio-updates-without-slowing-down-agent-workflows ; https://gearset.com/blog/rolling-back-unwanted-changes-in-a-salesforce-deployment/ |
| Keepit, HYCU, Spin.AI | SaaS backup | No agent-specific undo found in my searches **[not found; may exist]** | n/a | n/a |

### B. Agent governance, runtime security, authorization (threat to the "pre-action policy" and "ledger" parts)

| Company | Category | Funding / outcome | Source |
|---|---|---|---|
| Zenity | Agent security/governance (Copilot Studio, Agentforce, etc.) | $125M Series C (Norwest, Aug 3, 2026). Named a frontrunner by Gartner, Apr 2026 **[summary-only]** | https://www.intelcapital.com/zenity-raises-125-million-to-secure-the-era-of-1-billion-ai-agent/ |
| Noma Security | AI/agent security | $100M Series B; claims 1,300% ARR growth | https://curatedtechnologynews.substack.com/p/ea471920bca2585a6fdb9bb9ee54189c **[summary-only]** |
| Arcade.dev | "Secure action layer": tool auth, governance; wrote the MCP authorization spec | $60M Series A (SYN Ventures, Morgan Stanley, Wipro), June 2026; $72M total | https://siliconangle.com/2026/06/15/ai-agent-authorization-startup-arcade-nabs-60m-investment/ |
| Prompt Security | Acquired by SentinelOne (~$250M, 2025) | | https://softwarestrategiesblog.com/2026/03/28/agentic-ai-security-startups-funding-mna-rsac-2026/ |
| Invariant Labs | Acquired by Snyk (June 2025) | | same |
| Lakera | Acquired by Check Point (~$300M) | | same |
| Pangea / Aim | Acquired by CrowdStrike / Cato | | same |
| Protect AI | Acquired by Palo Alto Networks (~$500M reported) | | same |
| Astrix | Acquired by Cisco (2026) **[summary-only]** | | https://guptadeepak.com/identity-giants-bought-ai-agent-security/ |
| Oasis | Acquired by Cyera (~$1B) **[summary-only]** | | same |
| Permiso / Entro | Acquired by Okta / SailPoint **[summary-only]** | | same |
| Keycard, Aembit, Oso, Permit.io, Cerbos | Agent identity and fine-grained authorization | Keycard $30M Series A (phase1). Others: funding not re-checked | phase1 agents_at_scale.md |
| Lasso, Pillar, Credal | Agent/GenAI security and governed agent access | Not re-checked this round **[UNVERIFIED]** | n/a |
| MCP gateways: MintMCP, Solo.io agentgateway, WitnessAI, Tetrate, Traefik | Per-call policy plus audit logs for agent tool calls | Many players, commoditizing | https://www.mintmcp.com/blog/agent-gateways-ai-startups ; https://witness.ai/blog/mcp-gateway/ |
| Composio | Tool/action layer | Natural place to add a ledger and undo | n/a |
| Galileo, Arize, Langfuse, LangSmith, Laminar (YC) | Observability and traces (not business records) | Crowded | https://www.ycombinator.com/companies/industry/aiops |
| Agentic Fabriq (YC) | Agent identity, scoped permissions, **approval flows, audit logs** across business tools | YC-backed; funding unknown | https://www.ycombinator.com/companies/industry/security **[summary-only]** |
| HumanLayer (YC F24), gotoHuman | Human approval for high-stakes tool calls | HumanLayer about $500K convertible note (CB Insights). I believe it shifted focus to coding-agent tooling **[UNVERIFIED]** | https://www.cbinsights.com/company/humanlayer/ |
| Agent-Undo (OSS on glama) | Compensating rollback for MCP tools | OSS hobby-level | https://glama.ai/mcp/servers/b2qlcn4zj2 |

### C. Variant (b): code deploy risk

| Company | Relevance |
|---|---|
| Harness, LaunchDarkly (guarded releases), Unleash | Progressive delivery, automatic rollback, change approvals. Unleash markets "safer AI-generated code" directly: https://www.getunleash.io/blog/safer-ai-generated-code-with-unleash |
| Gearset | Salesforce deployment rollback |
| Sleuth, Cortex, Resolve | DORA metrics, change risk, and IDP scorecards (not re-checked this round) |
| Cytix | Raised a $7M Series A in Aug 2026 after pivoting to a "change risk" platform for AI-written code: https://www.techmarketview.com/ukhotviews/archive/2026/08/12/cytix-banks-7m-series-a-to-secure-the-age-of-ai-written-code |
| Rubrik Codebase Resilience | Immutable repo snapshots outside the repo (Claude Code launch) |
| BlastRadius (Product Hunt) | Pre-flight safety scan for coding agents (indie): https://www.producthunt.com/p/self-promotion/blastradius-a-pre-flight-safety-scan-for-ai-coding-agents |

**The incidents point at the platform, not a new vendor.** Kiro and PocketOS were not caused by a missing "blast-radius score on the PR." The agents ran destructive infra API calls using inherited or found credentials. The fix is credential scoping (Entra Agent ID, AgentCore Identity/Policy) and immutable backups, both of which incumbents own.

---

## 3. Can the platforms own this? What is left for an independent?

| Platform | What it covers | Gap |
|---|---|---|
| **AWS Bedrock AgentCore Policy + Gateway** | Deterministic Cedar allow/deny on every agent-to-tool call, outside the model, with each decision **written to the audit log**. Lambda interceptors run before and after tool calls. GA March 3, 2026. https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/policy-getting-started.md | No before/after state capture of the target SaaS; no revert |
| **Microsoft Agent 365 / Entra Agent ID / ID Protection** | Agent identities, Conditional Access for agents, risky-agent blocking, audit and sign-in logs, export to SIEM. Requires an Agent 365 license. https://learn.microsoft.com/en-us/entra/id-protection/concept-risky-agents | Identity-layer only. No data-level undo, except through Purview and partners (Rubrik integrates with Copilot Studio) |
| **ServiceNow AI Control Tower** | Inventory and governance of ServiceNow, Copilot and Agentforce agents plus custom agents via API. "Every action routed through Action Fabric runs through the AI Control Tower, carrying identity verification, permission scoping, and a full audit trail." Kill-switch messaging. https://www.bankinfosecurity.com/servicenows-new-platform-also-governs-everyone-elses-ai-a-31631 ; https://erp.today/servicenow-ai-security-governance-knowledge-2026/ **[summary-only]** | No automatic rollback |
| **Salesforce Agentforce** | Field history, Shield Event Monitoring, session tracing, plus native Backup & Recover (Own). Agentforce ARR above $1.5B by Q2 FY27, though the metric's definition was widened. https://pulse2.com/salesforce-net-income-jumps-87-as-agentforce-and-data-360-arr-surges-more-than-210-to-nearly-3-9-billion/ | No intent-linked "revert this agent's session" across objects; users complain about the lack of agent version control (https://mcguinnessai.substack.com/p/agent-snapshots-the-missing-feature) |

**What an independent could still own:**
1. **Intent-linked, cross-system *semantic* compensation.** Example: "Agent X's session 4411 changed 312 opportunities in SFDC, created 40 NetSuite credit memos and closed 90 Zendesk tickets. Revert all of it and generate compensating actions for what can't be reverted, such as a sent email or an issued invoice." Backup vendors restore snapshots by object or time and do not model business side effects. This is the real white space.
2. **Neutrality.** One ledger across Agentforce, Copilot, Bedrock, custom LangGraph agents and Claude/Cursor.

**Why that white space is thin:**
- The most damaging actions (an email sent, a payment made, a contract signed, data exfiltrated) **cannot be undone, only prevented.** Prevention sits in the policy and approval layer, which is crowded and partly native to the platforms.
- Building semantic compensation means writing per-object, per-system logic for hundreds of SaaS objects. The integration burden is large, and backup vendors already hold API access and snapshots for SFDC, M365 and Dynamics.
- Rubrik's marketing already claims "precise time and blast radius rollback." Whether that is true or not, the buyer will hear "we already have that from our backup vendor."

---

## 4. Buyer, budget, market math

**Who buys?** It is fragmented, which is a problem in itself.
- CISO: buys agent security (Zenity, Noma). Thinks of this as runtime security, not undo.
- CIO / Infrastructure & Operations: buys backup and resilience (Rubrik, Veeam). Undo is an upsell on an existing backup contract.
- Head of AI Platform: builds custom agents and buys tool/action layers (Arcade, Composio) and observability. Most likely to want a ledger SDK, but has the smallest budget.
- Business Systems / RevOps (SFDC admins): feel the pain of records being clobbered, but have little budget and buy point tools such as Gearset or Odaseva.

**How many companies have agents writing to systems of record?** **[EST]**
- Salesforce reported about 9,500 paid Agentforce deals as of Q3 FY26 (late 2025). https://www.cxtoday.com/conversational-ai/salesforce-hits-8000-agentforce-deals-opens-up-on-its-informatica-acquisition/ **[summary-only]** Most are service and Q&A agents with narrow write scopes.
- Claims that "70% of enterprises run agents in production" (Google Cloud trends) count assistants. I estimate the number of companies with **autonomous agents doing material, unsupervised writes to a system of record (CRM, ERP, HRIS, ITSM, billing)** as:
  - 2026: about 3,000–6,000 companies with more than 1,000 employees worldwide.
  - 2028: about 15,000–30,000. Gartner says 33% of enterprise apps will include agentic AI and 15% of daily work decisions will be autonomous by 2028.
- Subset with multi-system agents (where a neutral cross-system ledger adds value beyond a single platform's native tools): about 30%.

**Bottom-up SAM (independent cross-system ledger + undo)** **[EST]**

| | 2026 | 2028 |
|---|---|---|
| Firms with SoR-writing agents | 4,500 | 22,000 |
| Multi-system, need neutral layer (30%) | 1,350 | 6,600 |
| Realistic ACV (independent, mid-market/enterprise) | $50K | $90K |
| **SAM** | **~$68M** | **~$594M** |
| Realistic independent share after bundling by Rubrik/Veeam/platforms (5–10%) | $3–7M | $30–60M |

**ACV reality check.** Zenity publishes no price (custom annual contracts). Backup vendors can bundle agent undo into existing six-figure contracts at little marginal cost. Benchmarks for a standalone tool are about $30–80K for mid-market and $100–250K for large enterprises across many systems **[EST]**. Rubrik's >15 paying customers after about 12 months suggests even incumbents cannot yet sell this as a standalone line item.

---

## 5. Pilot: 90 days with limited integration? The sharpest wedge?

**Feasible pilot, but weak proof.**
- Technically you can build a pilot in 90 days: an MCP or tool proxy that wraps the agent's write tools for **one system** (Salesforce REST/Bulk API). Before each write it captures a before-image, logs the intent (prompt, plan and tool call), applies a policy ("more than 50 records, or amount above $X, needs approval"), and offers one-click session revert by writing back the before-images. Salesforce field history and CDC events help.
- **Problem 1:** the pilot only proves value on the day something goes wrong. Most 90-day pilots will see zero incidents. ROI rests on fear, and the procurement default for fear is "ask our backup vendor."
- **Problem 2:** it only works if the agent's writes go through your proxy. Agentforce agents act inside Salesforce and will not route through a third-party proxy. That restricts you to **custom-built agents**, which is the Head of AI Platform buyer (smaller budget, and Arcade or Composio may add the feature).

**Sharpest wedge, if pursued:** a "**shadow-write / staged changes**" mode for custom agents writing to Salesforce or NetSuite. The agent's writes land as a reviewable diff (a PR for CRM data) that is approved in bulk, applied, and revertible as a unit. This sells **deployment acceleration** ("let the agent go from read-only to write in 30 days") instead of insurance, which fixes the ROI-on-incident-only problem. It overlaps heavily with HumanLayer, gotoHuman, Arcade and AgentCore interceptors.

---

## 6. Kill signals (observed)

1. **The incumbent shows weak pull:** Rubrik has >15 paying Agent Cloud customers after about 12 months despite massive distribution (Aug 2026). **[summary-only of earnings call]**
2. **Five backup incumbents launched agent undo within 12 months** (Rubrik, Veeam, Commvault, Cohesity, Druva). That is table stakes, not white space.
3. **Pre-action policy is native to the platforms:** AWS AgentCore Policy GA (Mar 2026) with audit logs; Microsoft Agent 365 / Entra Conditional Access for agents; ServiceNow AI Control Tower with Action Fabric audit trail.
4. **The agent security layer is heavily funded and consolidating:** more than 14 acquisitions in 2026 alone (per a deals ledger cited on softwarestrategiesblog), plus Zenity $125M, Noma $100M and Arcade $60M.
5. **The incident evidence is for coding and infra agents, not business SaaS.** The well-known incidents are fixed by least privilege and immutable backups, not by a semantic ledger.
6. **The most harmful actions are irreversible** (emails, payments, exfiltration), so "undo" is the weaker half of the value proposition.
7. **The buyer is fragmented** across CISO, CIO/I&O, AI platform and business systems teams, so nobody owns the budget.
8. **The no-incident pilot problem:** ROI is unprovable in 90 days unless the product is reframed as accelerating write-access rollout.

**What would revive the thesis (watch-list):**
- A **named, public, material incident** where an agent corrupted CRM, ERP or billing data and backups could not cleanly fix it, because the downstream effects spread across systems.
- Insurers or auditors (SOC 2, ISO 42001, EU AI Act deployer obligations) **requiring per-action before/after evidence plus a demonstrated reversal capability** for agents.
- Rubrik or Veeam customers publicly complaining that snapshot rollback breaks referential integrity across systems.

---

## 7. Sharpened thesis (the only version worth testing)

> "**Staged writes for AI agents on systems of record.** Agents propose changes to Salesforce/NetSuite/Zendesk as a reviewable, policy-checked changeset; humans bulk-approve; every applied changeset is atomic, attributable and revertible across systems. We get custom agents from read-only to write access 3x faster."

- It sells **speed to production**, not insurance.
- The buyer is the Head of AI Platform or Business Systems lead at mid-to-large companies building **custom** agents (not Agentforce-native).
- Differentiation is cross-system changesets and compensation logic, not backups.
- **Main risk:** Arcade, Composio or AgentCore interceptors add "changesets" as a feature within 12 months. Low defensibility unless proprietary compensation models for the top 20 SaaS objects become a real moat.

Variant (b), the pre-deploy blast-radius gate for AI code, is **weaker still**. Harness, LaunchDarkly, Unleash, Cytix and Rubrik Codebase Resilience cover it, and coding-agent vendors such as Cursor and Claude Code are building their own guardrails.

---

## 8. Scores (1–10)

| Dimension | Score | Rationale |
|---|---|---|
| Pain | 6 | Real and visceral when it happens, but the documented cases are infra/coding and rare in business SaaS |
| Urgency | 4 | Delays are real (about 6 months), but buyers frame them as security/identity; rollback is not a top-cited blocker |
| ROI clarity | 4 | Insurance-like; only provable after an incident |
| Customer accessibility | 4 | Fragmented buyer; the backup vendor already owns the relationship |
| Pilot speed | 5 | Single-system proxy is doable in 90 days, but limited to custom agents and proof is weak with no incident |
| Market size | 6 | Could reach several hundred million dollars of SAM by 2028 if writing agents scale **[EST]** |
| Expansion | 6 | Ledger to audit to insurer scoring to policy is a logical land-and-expand |
| Venture potential | 4 | Squeezed between backup incumbents and platform-native policy |
| Defensibility | 3 | Integrations are replicable; incumbents hold the snapshots and API access |
| Why now | 7 | Agent write access is rising sharply in 2026 and incidents get press |
| Competition position | 2 | Rubrik, Veeam, Commvault, Cohesity and Druva, plus AWS, Microsoft and ServiceNow, plus $300M+ of funded agent-security startups |

**Average about 4.6/10.**

## VERDICT: **KILL**

Kill the thesis as stated, for both variant (a) and variant (b). The "Ctrl-Z for agents" narrative was taken by five data-protection incumbents in 2025–26, and their weak early traction (Rubrik >15 paying customers) suggests standalone demand is thin. Keep only the section 7 "staged writes / changesets for custom agents" idea as a **low-priority reframe**, and revive it only if the watch-list signals in section 6 appear.
