# Thesis T: "Agent Toll Router" (cut what SaaS vendors charge your AI agents per action, and stay within your contracts): kill test

Analyst stance: red team, trying to kill it. Date: 2026-10-05. Inputs: round6/fresh_tech_events.md (origin, TOP 1), round3/T4_agent_access_saas.md (vendor-side view, KILLED), phase5/B_ai_spend_control.md (AI spend control, KILLED).

Budget: about 42 web searches (slightly over the 40 cap). WebFetch was not used. Every fact below comes from search-result snippets. Every URL appeared in a search result; none was constructed. **[U]** means unverified, a single secondary source, or my own estimate. **[V]** means a primary source, or several consistent secondary sources.

---

## 0. Verdict up front

**KILL as a standalone company in 2026. Park it with tripwires (section 8).**

The thesis is built on a timing illusion, which has three parts.

1. **What is billed at scale is mostly first-party agents, and those cannot be routed around.** Agentforce ($1.5B ARR), Copilot Credits, Zendesk/HubSpot per-resolution fees and Now Assist all run *inside* the vendor. A router cannot point a vendor's own agent at your warehouse.
2. **The fees a router *could* avoid, on third-party agent reads, are mostly not billed yet.** Salesforce's "Headless Platform Interactions" multiplier is "TBA" and metering has not started. Atlassian Rovo MCP is free, and enforcement of overage billing begins Dec 3 2026. HubSpot MCP is free. ServiceNow's MCP server is "included" in Now Assist SKUs, with assists negotiated at $0.02–0.10. Microsoft does not charge licensed M365 Copilot users credits for internal agents.
3. **Where the toll is real, the bypass is either easy to build yourself or forbidden.**
   - Easy to build yourself: Salesforce core data is customer data. Bulk export, Fivetran/Informatica (which Salesforce now owns) and Data 360 Zero Copy (free to connect) already replicate it, and Stacksync (YC W24) markets "source systems see no agent traffic at all."
   - Forbidden: SAP API Policy v4.2026 bans large-scale extraction *and* agent orchestration outside SAP pathways, and it is tied to the master contract and enforced through audits. Slack bans persistent copies and LLM use of its data.

   The router's value lives only in the thin, shrinking band between those two cases.

Two further problems. Vendors are answering cost anxiety with flat-fee agentic ELAs (Salesforce AELA), which take away the per-action bill a router would optimize. And the "contract intelligence / renewal evidence" layer is already sold by Redress Compliance (VendorBenchmark, Enterprise AI Credits Playbook), Tropic (AI-credit negotiation guide), Zylo CCM and Flexera/Snow (SAP Digital Access).

---

## 1. Are per-action agent fees actually billed at scale in 2026?

| Vendor | Unit / rate | First-party (vendor's agent) billed? | **Third-party agent calls billed?** (only these are routable) | Source | Tag |
|---|---|---|---|---|---|
| **Salesforce** | Flex Credits: Agentforce action = 20 credits ≈ $0.10; voice 30; $500/100K credits. Employee agent add-on ≈ $125/user/month | **Yes, at scale.** Agentforce ARR $1.5B (+240%). Agentforce + Data 360 ≈ $3.9B. 3.2B Agentic Work Units in Q2 (+97% QoQ). 50% of Agentforce bookings are refills. MCP calls grew 6x in Q2 | **No, not yet.** "Headless Platform Interactions" (each successful MCP/API call by a registered agent) is listed on the rate card with multiplier **"TBA"**. "Agentic usage is not currently being metered." 30 days' notice before billing. Redress flags January 2027 renewals as the moment to price it in writing | https://www.salesforceben.com/salesforce-will-charge-flex-credits-for-agentic-mcp-and-api-calls/ ; https://www.salesforce.com/en-us/wp-content/uploads/sites/4/assets/pdf/agentforce/Flex-Credits-Rate-Card-08.31.2026.pdf ; https://redresscompliance.com/research-notes/salesforce-headless-360-january-2027 ; https://futurumgroup.com/insights/salesforce-q2-fy-2027-can-agentforce-drive-revenue-reacceleration/ ; https://www.techmarketview.com/ukhotviews/archive/2026/08/27/salesforce-q2-keeps-agentforce-growth-story-moving | [V] |
| **Salesforce AELA** | Unlimited Agentforce / Data 360 / MuleSoft for a fixed fee over 2–3 years | Flat fee | Flat fee | https://www.beri.net/article/salesforce-aela-flat-fee-agentic-pricing-2026 ; Gartner warns AELAs convert to defined-quantity contracts at renewal: https://letsdatascience.com/news/gartner-warns-salesforce-customers-about-aela-renewals-2d34c6a7 | [S] |
| **ServiceNow** | Assists. $0.20 overage list price; negotiated top-ups $0.02–0.10. Bundled into Foundation/Advanced/Prime with finite pools (since Apr 9 2026) | Yes | **Partly.** Action Fabric (May 5 2026; Anthropic is design partner): headless actions by external agents draw on the same assist pool. The MCP server is "included in Now Assist and AI Native SKUs" | https://www.pymnts.com/artificial-intelligence-2/2026/servicenow-sap-and-workday-make-ai-agents-pay-to-play/ ; https://redresscompliance.com/servicenow-assist-top-up-unit-price-benchmark ; https://www.eesel.ai/blog/claude-for-servicenow ; https://www.reworked.co/digital-workplace/servicenow-launches-action-fabric-major-overhaul-of-ai-control-tower/ | [V]/[S] |
| **SAP** | AI Units (BTP/Joule/BDC) plus Digital Access (document-based) | Yes | **Not a toll. It is a ban plus a mandated pathway.** API Policy v4.2026 (enforced Jun 9) prohibits APIs for "(semi-)autonomous or generative AI systems that plan, select, or execute sequences of API calls" and "systematic and/or large-scale data extraction or replication" outside SAP pathways. Gartner calls this "Indirect Access 2.0" | https://www.beri.net/article/sap-api-policy-ai-governance-2026 ; https://redresscompliance.com/sap-restricted-third-party-api-access-guide.html ; https://www.forrester.com/blogs/sap-is-attempting-to-become-the-gatekeeper-of-enterprise-ai-cios-should-push-back/ | [V] |
| **Workday** | Flex Credits, 1–750 credits per agent action. No public rate card; negotiated, with annual commitment | Yes | Via **Agent Gateway** (third-party agents, REST/SOAP/Graph/WQL/RaaS). Agent System of Record "is the only place burn is visible." Rates are negotiated | https://redresscompliance.com/workday-flex-credits-licensing-pillar-2026 ; https://investor.workday.com/news-and-events/press-releases/news-details/2026/Workday-Launches-New-Tools-for-Developers-to-Build-Connect-and-Verify-AI-Agents-For-HR-Finance-and-IT/default.aspx | [S] |
| **Microsoft** | Copilot Credits: $0.01 PAYG, $200 per 25K-credit pack. Agent action = 5 credits | Yes. Production use runs above estimates | n/a. Internal agent use by licensed M365 Copilot users consumes **no** credits | https://www.cloudzero.com/blog/copilot-studio-pricing/ ; https://www.licensingschool.co.uk/wp-content/uploads/2026/07/Microsoft-Copilot-Studio-Licensing-Guide-July-2026.pdf | [V] |
| **HubSpot** | $10/1K credits. Customer Agent 50 credits ($0.50) per resolved conversation (since Apr 14 2026) | Yes | **No.** The MCP server is free for external agents, limited only by API units | https://saastr.com/almost-every-pre-ai-vendor-we-use-is-raising-prices-for-agent-access-they-may-be-building-an-agentic-death-spiral ; https://resolve247.ai/blog/hubspot-ai-agent-pricing | [V] |
| **Atlassian** | Rovo credits, $0.01 overage. Chat/agent 10 credits; deep research 100 | Billing enforcement starts **Dec 3 2026** | **Mostly no.** The Rovo MCP server is free with no add-on; rate limits run 1K–10K calls/hour. Only "enriched" Teamwork Graph calls consume 1–10 credits | https://techrepublic.com/article/news-atlassian-rovo-automation-pricing ; https://support.atlassian.com/organization-administration/docs/usage-limits-in-atlassian-intelligence/ ; https://www.empyra.com/blog/atlassian-rovo-pricing-guide-rovo-credits | [V] |
| **Zendesk** | ≈$1.50–2.00 per automated resolution (unpublished) plus $50/agent/month add-on. "Verified Resolutions" only since May 2026 | Yes | No per-call toll found | https://eesel.ai/blog/zendesk-ai-pricing/ | [S] |
| **Snowflake** | AI Credits $2.00–2.20 (since Apr 1 2026) for Cortex Agents/Intelligence, plus warehouse compute | Yes | n/a. **Snowflake is where a router's rerouted reads would land, so the cost moves there rather than disappearing** | https://coefficient.io/snowflake/snowflake-intelligence-cost | [S] |

**Bill shock exists, but it comes from first-party agent multipliers.**
- Redress: "the agentic multiplier of five to ten times" drives the bill, and vendor first-year estimates ran **40–70% below** actual burn. https://redresscompliance.com/enterprise-ai-credits-playbook-landing [S, advisory with a commercial interest]
- FinOps Foundation (via secondary sources): only about 20% of organizations forecast AI spend within ±10%. https://www.sovereignmagazine.com/article/agentic-ai-pay-per-action-pricing-bill-shock [S]
- Tropic: 20–37% "AI tax" at renewals. https://www.tropicapp.io/blog/ai-credit-pricing-negotiation-guide [S]

**Typical spend [U, my estimates]:**
- A Global-2000 Salesforce + ServiceNow + M365 shop in 2026 likely spends **$0.5–5M/yr on first-party agent credits** (not routable).
- The same shop likely spends **$0–300K/yr on third-party-agent tolls** that are actually billed (routable). Most of that is ServiceNow assists drawn from pools that are already prepaid.
- By 2028, if Salesforce sets a meaningful HPI multiplier and others copy it, routable tolls could reach $0.5–3M at heavy agent users.

**Finding 1: the thesis's addressable pool is ~10x smaller today than the headline numbers suggest.** Headlines such as "Agentforce $1.5B" and "Gartner $234B" measure fees and exposure that a read-router cannot touch.

---

## 2. Contracts: can agent reads be served from replicated data?

| Vendor | Can you replicate and let agents read the copy? | Do they monetize the sanctioned copy path? | Implication |
|---|---|---|---|
| **Salesforce core (CRM)** | **Yes, it is your data.** Bulk API exports, Fivetran/Informatica (Salesforce-owned) replicate it. Zero Copy with Snowflake/Databricks/BigQuery/Redshift: "no cost associated with connecting a source via Zero Copy." Costs apply only when Data 360 features process the data. https://www.salesforceben.com/salesforce-data-cloud-zero-copy-when-and-when-not-to-use-it/ ; https://www.default.com/post/salesforce-data-cloud-integrations | Data 360 credits (Starter SKU about $60K/yr) when used inside Salesforce | **The bypass is legal and easy, which is why customers can do it themselves.** SaaStr says the "immediate reaction" is to sync to your own DB and write back on change. No router is needed |
| **Salesforce: Agent Integration Protocols** | Agents must be registered with distinct identity. "Must not misrepresent or mask the identity of the API client." https://developer.salesforce.com/salesforce-agent-integration-protocols | Registered agents' calls become HPIs | Any router that pools or proxies agent calls to hide which agent is calling breaches the protocol. **Dedup/caching across agents is legally grey** [U] |
| **Slack (Salesforce)** | **No.** API terms ban bulk export, "persistent copies, archives, indexes or long-term data stores," and LLM use. Glean was cut to query-by-query. https://www.hunton.com/insights/legal/salesforce-locks-down-slack-data-time-to-review-your-slack-api-terms | Slack AI / Agentforce in Slack | The read-from-copy path is **forbidden** |
| **SAP** | **No, outside SAP pathways.** It bans "systematic and/or large-scale data extraction or replication" and agent orchestration. ODP-via-RFC has been banned since 2024 (ODP OData is allowed; Fivetran uses OData and an ABAP add-on). The policy is "linked to master contract terms" and referenced in audits; SAP grants "no leniency" on indirect-access violations. https://www.fivetran.com/blog/a-technical-deep-dive-into-how-fivetran-centralizes-sap-data ; https://redresscompliance.com/sap-restricted-third-party-api-access-guide.html ; https://redresscompliance.com/sap-audit-trends/ | **Yes.** BDC + SAP Databricks via zero-copy Delta Sharing is the sanctioned path, billed in AI Units/BDC capacity. https://docs.databricks.com/aws/en/delta-sharing/sap-bdc | Bypass = buy SAP's bypass. **A router adds legal risk without saving money** |
| **ServiceNow** | Workflow Data Fabric offers zero-copy connectors *into* ServiceNow (Snowflake, Databricks, BigQuery, Redshift). Replication out goes through standard export/APIs. I found no explicit agent-read ban [U] | Action Fabric assists for external agent actions | Reads from a copy are plausible. The real cost is writes and actions, which still go through assists |
| **Workday** | The Agent Gateway is the "controlled interface" for third-party agents. Data Cloud / AWS integration announced Jun 2. Explicit replication terms not found [U] | Flex Credits plus Data Cloud | Middle ground. Watch for restrictions |
| **Atlassian / HubSpot / Zendesk** | Standard APIs plus free MCP | Their own agents only | **No toll to route around** |

**Finding 2: the market splits into three groups.**
- **(a) Vendors with an easy, legal bypass** (Salesforce core, HubSpot, Atlassian, Zendesk). Customers already do it with Fivetran, Stacksync, CData or Zero Copy, so a router has no unique role.
- **(b) Vendors where the bypass is forbidden** (SAP, Slack). A router means audit exposure, and SAP sells the sanctioned path.
- **(c) Vendors with unclear terms** (ServiceNow, Workday). Here the toll is mostly on actions and writes, which must hit the metered API regardless.

Rerouting also does not remove cost. Reads move onto Snowflake/Databricks compute and AI credits, plus Fivetran/replication fees. Net savings are much smaller than gross savings.

---

## 3. Competitor table

| Player | What they do relevant to T | Status / funding | Overlap with T |
|---|---|---|---|
| **Salesforce Digital Wallet** | Near-real-time Flex Credit consumption, threshold alerts, trends | Native, free | Metering for Salesforce |
| **Workday Agent System of Record / Agent Gateway** | Registers first- and third-party agents at skill level; "only place burn is visible" | Native | Metering for Workday |
| **ServiceNow AI Control Tower** | Cross-vendor agent cost/ROI (but CIO.com calls it a "hazy view of spend") | Native | Metering for ServiceNow and partly cross-vendor |
| **MuleSoft Agent Fabric** (Salesforce) | Registry, Broker (routing), AI Gateway that "manages costs, usage" across agents, MCP and LLMs. Broker GA Jun 2026; six-figure contracts | Salesforce-owned | Routing plus cost governance, but the toll collector owns it |
| **Redress Compliance** | Enterprise AI Credits Playbook (7 vendors normalized), VendorBenchmark (520 vendors, 500K+ deals), SAP API policy and Salesforce Headless 360 renewal advisory | Independent advisory | **Owns "contract intelligence plus renewal evidence"** |
| **Tropic** | AI-credit negotiation guide, SKU benchmarks from 100K+ transactions; bookings +79% YoY, $33M saved H1 2026 | Late-stage | Renewal evidence |
| **Vertice, Vendr, Spendflo, Cledara** | Procurement/benchmarks | Funded | Renewal evidence |
| **Zylo CCM** (Apr 14 2026) | Consumption cost management with contract context (OpenAI, Anthropic, Snowflake, Databricks, Vertex) | Late-stage | Metering plus contract context; can add Salesforce/ServiceNow credits |
| **Torii, Productiv** | SaaS management, AI modules | Funded | Inventory |
| **Flexera/Snow, USU** | SAP Optimizer, **Digital Access Estimator** (indirect-use tracing), ServiceNow SAM | Large | **SAP indirect/agent licensing exposure, already sold** |
| **Ramp, Vantage, CloudZero, Finout** | AI token spend. Finout blog: "your agents are about to be charged per data query at every SaaS vendor" | Large | Finout can extend to SaaS agent credits |
| **Stacksync** (YC W24, ~$0.5M) | Two-way sync of Salesforce/HubSpot/NetSuite/SAP to Postgres for agents; "source systems see no agent traffic at all" | Tiny | **This is T's read-path compiler, already marketed** |
| **CData Connect AI** | Managed MCP over 300+ systems, live or replicated; SAP BW to Agentforce | Mid-size | Read path plus connectivity |
| **Fivetran, Airbyte, Estuary, Informatica** (Salesforce-owned) | Replication | Large | Supplies the copy |
| **Composio** ($29M), **Arcade** ($72M), **Merge Agent Handler**, Nango, **One** (YC, $4M) | Agent tool-calling, auth, governance | Funded | Gateway position for agent→SaaS calls |
| **Kong, Apigee, Gravitee, PANW/Portkey, TrueFoundry, Bifrost** | MCP proxy, semantic caching, rate limiting | Large | Caching, dedup, rate limits (T items 3 and part of 1) |
| **Snowflake / Databricks** | Zero-copy partners of Salesforce/SAP/ServiceNow; meter agents with their own AI Credits | Large | They gain from rerouting, so they partner but will not cut tolls for you |
| Dedicated "agent toll router" startup | **None found** in ~42 searches | — | White space, but see section 1: the white space exists because the toll is not live yet |

---

## 4. Can vendors, MuleSoft or Workato own this? Would they retaliate?

- **Vendors meter themselves natively** (Digital Wallet, Agent SoR, AI Control Tower) and offer flat ELAs. Their counter to "cut the toll" is "buy AELA," which turns variable cost into a fixed commitment and leaves nothing to optimize until renewal.
- **Retaliation is already written into contracts.** Salesforce requires registered agent identity and forbids masking it. SAP ties its API policy to the master contract and to audits with "no leniency," and Gartner says indirect-use true-ups can reach "24 times" initial estimates. Slack bans copies outright. A product whose pitch is "route around the vendor" becomes evidence in an audit. Large customers' legal teams will not deploy it on SAP. On Salesforce they do not need it.
- **Customer appetite:** customers push back through user groups (DSAG on SAP) and analysts (Forrester: "CIOs should push back"; Gartner: "negotiate agent access terms now"). The chosen weapon is **negotiation**, not circumvention, which points spend toward advisors such as Redress, Tropic, Gartner and UpperEdge rather than a router.
- **MuleSoft** (Salesforce) already ships Agent Broker plus AI Gateway cost control. **Workato** sells an Enterprise MCP. **Kong/PANW** cache and rate-limit. Composio/Arcade/Merge sit in the agent→SaaS call path and could add a "cost-aware routing" feature in a quarter.

---

## 5. Buyer, count, ACV, 90-day pilot

- **Buyer:** Head of Enterprise Applications/Architecture (who owns the agent plumbing) plus IT procurement/SAM (who own renewals). The CIO sponsors. FinOps is a weak buyer, because SaaS credits sit in the IT apps budget, not cloud.
- **Enterprises with *material routable* third-party-agent tolls [U]:**
  - 2026: about **100–300 worldwide** (heavy ServiceNow external-agent users drawing down assist pools, Workday Agent Gateway early adopters). Salesforce HPI billing is not live.
  - 2028: about **1,500–3,000**, *if* Salesforce publishes an HPI multiplier above roughly $0.01/call and ServiceNow/Workday hold their tolls.
- **ACV:** $75–200K subscription, or 15–25% of verified net savings [U].
- **90-day pilot as proposed** ("meter Salesforce Flex Credits, show 30%+ savings"): **cannot be run today.** There is no HPI bill to cut, and first-party Agentforce credits cannot be rerouted. The realistic version is ServiceNow: baseline assist drawdown from external agents (Claude Cowork via Action Fabric), serve read-only lookups from a replicated table, and measure the assist reduction. The catch is that pools are prepaid and bundled, so the savings appear only at renewal, 12–36 months out. **That is a modelled-savings pilot, which buyers treat as a consulting deliverable.**

---

## 6. Market math

| Target | Requires | Plausibility |
|---|---|---|
| **$10M ARR** | about 70 customers × $140K | Feasible by 2028 *if* tolls go live. In 2026–27 it looks like an advisory/tool hybrid competing with Redress and Tropic |
| **$50M ARR** | about 300 × $165K | Needs Salesforce HPI plus ServiceNow plus Workday tolls to be real and material, *and* the bypass still allowed. Two independent conditions that vendors control |
| **$100M ARR** | about 550 × $180K, or a take-rate on about $500M+ of avoided tolls | Requires vendors to keep high per-call tolls while also tolerating systematic rerouting. **That combination contradicts itself:** the more a router saves, the faster vendors move to flat ELAs, bans (SAP/Slack-style) or identity rules |

Top-down: Gartner's $234B "exposed" figure is *seat revenue at risk for vendors*, not toll spend. A realistic 2028 pool of routable third-party-agent tolls might be **$1–3B globally [U]**. Of that, perhaps 30–40% is avoidable net of warehouse costs, and a 20% take on the avoided amount gives a **$60–240M revenue ceiling for the whole category**. That is not a $10B outcome.

**Moat:** cross-customer contract/pricing benchmarks are already held by Redress (500K deals), Tropic (100K transactions) and Vertice/Vendr. Per-vendor optimization playbooks are consultant IP that copies quickly. A data network effect would start at zero against incumbents. **Defensibility is weak.**

---

## 7. Kill signals

1. **The routable toll is not billed yet.** Salesforce HPI multiplier is TBA with no metering. Atlassian MCP is free and enforcement starts Dec 3. HubSpot MCP is free. **TRIGGERED** (timing).
2. **The fee pool at scale is first-party and cannot be routed.** Agentforce $1.5B, Copilot, Zendesk/HubSpot resolutions. **TRIGGERED.**
3. **Where tolls are real, the bypass is forbidden** (SAP v4.2026, Slack) and SAP sells the sanctioned bypass (BDC/Databricks). **TRIGGERED.**
4. **Where the bypass is allowed, it is a commodity** (Zero Copy free, Fivetran, Informatica, Stacksync, CData). **TRIGGERED.**
5. **Vendors offer flat ELAs** (Salesforce AELA), removing per-action variance. **TRIGGERED.**
6. **Identity rules forbid masking or pooling agent calls** (Salesforce Agent Integration Protocols). **PARTIAL.**
7. **Renewal evidence and contract intelligence are already sold** (Redress, Tropic, Zylo, Flexera/Snow). **TRIGGERED.**
8. **Native metering exists** (Digital Wallet, Workday Agent SoR, AI Control Tower), and MuleSoft Agent Fabric routes plus controls cost. **TRIGGERED.**
9. **Net savings are lower than gross**, because reads move to Snowflake/Databricks AI credits and compute. **Structural.**
10. **It sits next to two previously killed theses** (T4 vendor-side; B AI spend control). **Pattern match.**

---

## 8. Sharpened thesis (best surviving version) and tripwires

**Best reframe:** *"Agent-Access Renewal Desk: before you sign a 2026–27 Salesforce, ServiceNow, Workday or SAP renewal, we instrument your actual agent→SaaS call graph for 60 days. That covers which agents call what, read/write mix, and the projected HPI, assist and Flex Credit exposure under each draft term. You get the clause redlines and caps that keep it bounded, plus a compliant read architecture (Zero Copy/BDC) where it is cheaper."*

This is still weak. It is a time-boxed, renewal-driven, consulting-shaped product. Redress and Tropic already sell the redlines, and the telemetry piece is a feature for Composio/Merge/Kong or MuleSoft.

**Tripwires to revisit (check monthly):**
- (a) Salesforce publishes an HPI multiplier **≥ $0.01/call** and starts metering.
- (b) ServiceNow moves the MCP server out of bundles into separate per-action billing.
- (c) Customer reports of **$1M+ third-party-agent toll bills** appear.
- (d) Vendors do **not** extend Slack/SAP-style copy bans to core CRM/ITSM data.

If (a), (c) and (d) all hold, this reopens as a real category in 2027.

---

## 9. CIO cold message and simulated reaction

**Message (to the CIO of a $10B industrial on Salesforce, ServiceNow and S/4HANA):**
> Subject: Your agents' SaaS toll before the January renewal
> Salesforce will start charging Flex Credits for every MCP/API call your Claude and Copilot agents make ("Headless Platform Interactions"), and ServiceNow already draws assists for Action Fabric calls. We map every agent→SaaS call, serve read-only lookups from your Snowflake copy where your contract allows, and give you clause language to cap the rest before you sign. 20 minutes to see your projected exposure?

**Simulated reaction:**
> "Salesforce hasn't priced HPI yet. My account team is offering an AELA that makes it moot for three years. Our Salesforce data is already in Snowflake via Fivetran and our agents read from there; we did that last year for latency, not cost. SAP? Legal will not let anything touch SAP outside BTP after the June policy, and we're mid digital-access true-up. The ServiceNow assists come out of a prepaid pool. Send me something in Q3 next year if the bill is real. Meanwhile Redress is already doing our Salesforce renewal."

---

## 10. Five simulated buyers

| Buyer | Context | Answer | Why |
|---|---|---|---|
| Head of Enterprise Apps, Fortune 100 bank (Salesforce, ServiceNow, Workday) | Heavy in-house agents, Snowflake lakehouse | **NO** | Already reads from the lakehouse. HPI is unpriced. Wants identity and audit, not routing. Its MuleSoft contract covers the gateway |
| CIO, $8B manufacturer on S/4HANA | Wants Claude over SAP | **NO** | The only compliant path is BDC/Joule. A third-party router raises audit risk |
| VP IT Ops, $3B SaaS company running Claude Cowork on ServiceNow via Action Fabric | Assist pool burning faster than planned | **MAYBE** | Wants burn forecasting and renewal ammo. Would pay $40–60K, not $150K, and asks "can't ServiceNow's AI Control Tower do this?" |
| Director of SAM/Procurement, global pharma | Salesforce renewal Feb 2027 | **MAYBE** (one-off) | Wants an exposure model and clause pack for one renewal. Will buy from Redress or Gartner if they get there first. No recurring need |
| Head of AI Platform, digital-native retailer (HubSpot, Zendesk, Atlassian) | Many third-party agents | **NO** | HubSpot/Atlassian MCP is free. Zendesk fees are first-party resolutions. Nothing to route |

Result: 0 YES, 2 MAYBE (low ACV / one-off), 3 NO.

---

## 11. VC committee view: could it be $10B?

- **Bull:** "Gartner's $234B is the size of the vendors' fear, and every system of record will toll agents. The neutral router across 30 vendors becomes the agent-era procurement system of record, the way Zylo/Coupa are for seats and spend."
- **Bear (prevails):** The router only has value in a window where vendors (i) bill third-party agent calls per action, (ii) allow replication, and (iii) don't offer flat ELAs. Vendors control all three and are already closing the window: SAP and Slack banned copies, Salesforce is selling AELA and mandating identity, ServiceNow bundles. Spend is real but first-party. The contract-intelligence layer belongs to advisors with large deal databases, and the plumbing belongs to MuleSoft, Kong, Composio and Fivetran. The category ceiling is a ~$100–250M revenue pool. **Not $10B. Pass; revisit if Salesforce HPI billing goes live with a material multiplier.**

---

## 12. Scores (1–10)

| Dimension | Score | Rationale |
|---|---|---|
| Pain | 5 | Credit bill shock is real (40–70% under-estimates), but it comes from first-party agents the router can't touch |
| Urgency | 4 | Routable tolls are mostly unpriced or unbilled. The renewal-terms urgency is real but one-off |
| ROI clarity | 4 | Gross savings are offset by warehouse/AI-credit and replication costs. Prepaid pools hide savings until renewal |
| Customer accessibility | 4 | Enterprise apps leaders are reachable, but SAP shops won't touch it and Salesforce shops are on AELA or already replicate |
| Pilot speed | 3 | No live HPI bill to cut. ServiceNow savings appear only at renewal, so the pilot is a model |
| Market size | 4 | About $60–240M category revenue ceiling by 2028 [U] |
| Expansion | 5 | Agent-era procurement/contract intelligence is plausible, but incumbents own it |
| Venture potential | 3 | Window controlled by counterparties; no $1B path |
| Defensibility | 2 | Benchmarks held by Redress/Tropic; playbooks copy easily; legal exposure |
| Why now | 6 | Tolls announced in 2026, renewals in 2026–27. But announced is not billed |
| Competition position | 3 | No direct "toll router" exists, but every component ships elsewhere (native meters, MuleSoft, Kong, Stacksync/CData, Redress/Tropic, Flexera) |
| **Total** | **43/110** | |

## VERDICT: **KILL** (park with the tripwires in section 8; the narrow "Agent-Access Renewal Desk" reframe is not recommended for advance)

This is the third time the same structure has failed: a control layer between agents and SaaS gets squeezed. The vendor is the counterparty that sets the rules (bans, identity, ELAs), the plumbing is commodity, and the intelligence layer belongs to incumbents with deal databases. The origin memo's own top kill risk, "vendors rewrite terms to forbid agents from using replicated data," has **already happened** at SAP and Slack. At Salesforce it is unnecessary, because the toll itself is not yet priced.

---

## Sources (snippet-level; all from search results)
- Salesforce HPI / Flex Credits: https://www.salesforceben.com/salesforce-will-charge-flex-credits-for-agentic-mcp-and-api-calls/ ; https://www.salesforce.com/en-us/wp-content/uploads/sites/4/assets/pdf/agentforce/Flex-Credits-Rate-Card-08.31.2026.pdf ; https://vantagepoint.io/blog/sf/salesforce-flex-credits-agentic-api-calls
- Salesforce Headless 360 / Jan 2027: https://redresscompliance.com/research-notes/salesforce-headless-360-january-2027
- Salesforce Q2 FY27: https://futurumgroup.com/insights/salesforce-q2-fy-2027-can-agentforce-drive-revenue-reacceleration/ ; https://www.techmarketview.com/ukhotviews/archive/2026/08/27/salesforce-q2-keeps-agentforce-growth-story-moving
- Salesforce AELA: https://www.beri.net/article/salesforce-aela-flat-fee-agentic-pricing-2026 ; https://letsdatascience.com/news/gartner-warns-salesforce-customers-about-aela-renewals-2d34c6a7
- Salesforce Agent Integration Protocols: https://developer.salesforce.com/salesforce-agent-integration-protocols
- Zero Copy: https://www.salesforceben.com/salesforce-data-cloud-zero-copy-when-and-when-not-to-use-it/ ; https://www.default.com/post/salesforce-data-cloud-integrations
- Slack API terms: https://www.hunton.com/insights/legal/salesforce-locks-down-slack-data-time-to-review-your-slack-api-terms
- SaaStr death spiral: https://saastr.com/almost-every-pre-ai-vendor-we-use-is-raising-prices-for-agent-access-they-may-be-building-an-agentic-death-spiral
- ServiceNow: https://www.pymnts.com/artificial-intelligence-2/2026/servicenow-sap-and-workday-make-ai-agents-pay-to-play/ ; https://redresscompliance.com/servicenow-assist-top-up-unit-price-benchmark ; https://www.eesel.ai/blog/claude-for-servicenow ; https://www.reworked.co/digital-workplace/servicenow-launches-action-fabric-major-overhaul-of-ai-control-tower/ ; https://www.cio.com/article/4169954/servicenows-ai-control-tower-offers-hazy-view-of-spend.html ; WDF zero copy: https://www.cxtoday.com/customer-analytics-intelligence/servicenow-workflow-data-fabric-what-is-it-how-does-it-work/
- SAP: https://www.forrester.com/blogs/sap-is-attempting-to-become-the-gatekeeper-of-enterprise-ai-cios-should-push-back/ ; https://www.beri.net/article/sap-api-policy-ai-governance-2026 ; https://redresscompliance.com/sap-restricted-third-party-api-access-guide.html ; https://redresscompliance.com/sap-audit-trends/ ; https://www.fivetran.com/blog/saps-latest-api-policy-raises-the-stakes-for-your-ai-strategy ; https://www.fivetran.com/blog/a-technical-deep-dive-into-how-fivetran-centralizes-sap-data ; https://docs.databricks.com/aws/en/delta-sharing/sap-bdc
- Gartner: https://www.gartner.com/en/newsroom/press-releases/2026-07-01-gartner-says-us-dollars-234-billion-in-enterprise-application-software-spend-is-at-risk-from-agentic-artificial-intelligence ; Indirect Access 2.0: https://www.gartner.com/en/documents/7625829 ; https://www.cio.com/article/4192242/agentic-ai-puts-234b-in-enterprise-saas-spending-at-risk-gartner-says.html
- Workday: https://redresscompliance.com/workday-flex-credits-licensing-pillar-2026 ; https://investor.workday.com/news-and-events/press-releases/news-details/2026/Workday-Launches-New-Tools-for-Developers-to-Build-Connect-and-Verify-AI-Agents-For-HR-Finance-and-IT/default.aspx
- Microsoft: https://www.cloudzero.com/blog/copilot-studio-pricing/ ; https://www.licensingschool.co.uk/wp-content/uploads/2026/07/Microsoft-Copilot-Studio-Licensing-Guide-July-2026.pdf
- Atlassian: https://techrepublic.com/article/news-atlassian-rovo-automation-pricing ; https://support.atlassian.com/organization-administration/docs/usage-limits-in-atlassian-intelligence/ ; https://www.empyra.com/blog/atlassian-rovo-pricing-guide-rovo-credits
- HubSpot: https://resolve247.ai/blog/hubspot-ai-agent-pricing ; Zendesk: https://eesel.ai/blog/zendesk-ai-pricing/ ; Snowflake: https://coefficient.io/snowflake/snowflake-intelligence-cost
- Tollgate framing: https://ai2.work/blog/the-agent-tollgate-enterprise-software-charges-by-the-action ; https://www.finout.io/blog/your-agents-are-about-to-be-charged-per-data-query-at-every-saas-vendor
- Bill shock: https://www.sovereignmagazine.com/article/agentic-ai-pay-per-action-pricing-bill-shock ; https://redresscompliance.com/enterprise-ai-credits-playbook-landing
- Competitors: Zylo https://zylo.com/news/ai-consumption-cost-management-launch ; Tropic https://www.tropicapp.io/blog/ai-credit-pricing-negotiation-guide , https://www.tropicapp.io/newsroom/tropic-grows-bookings-79-yoy-saves-customers-33m-in-h1-2026-and-deepens-its-reach-inside-claude-and-chatgpt ; Redress VendorBenchmark https://redresscompliance.com/vendorbenchmark-platform-overview ; Flexera/Snow https://www.flexera.com/about-us/press-center/new-snow-digital-access-estimator-sapr-delivers-licensing-transparency-sap-digital ; MuleSoft Agent Fabric https://www.cxtoday.com/contact-center/salesforce-launches-mulesoft-agent-fabric-to-tackle-agent-sprawl/ , https://www.beri.net/article/salesforce-agent-fabric-multi-vendor-control-plane-150k-agents-2026 ; Stacksync https://www.stacksync.com/blog/ai-agent-data-layer-mcp-vs-synced-database , https://www.stacksync.com/about ; CData https://www.cdata.com/ai/use-cases/enterprise-mcp-connectivity/ ; Composio/Arcade/Merge https://www.merge.dev/blog/composio-pricing , https://www.hpcwire.com/bigdatawire/this-just-in/arcade-secures-60m-to-scale-authorization-and-governance-for-ai-agents/ ; Kong https://dailyaiworld.com/mcp-directory/kong-ai-gateway-mcp-proxy-translating-enterprise-rest-apis ; Salesforce Agentforce Credit Tracker (Chrome) https://chromewebstore.google.com/detail/gmnogolobdlpopipkglbomphhfigfjpe ; One (YC) https://www.withone.ai/yc
