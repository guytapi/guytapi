# F5: Agent-speed procurement (thesis #20). Deep dive

Date: 2026-10-06. I ran 38 web searches. WebFetch and Reddit were blocked. **Every URL below came back in search results. I did not open any of the pages, so every claim is taken from a search snippet.** Items marked *(unverified)* need a check on the page before anyone relies on them. Funding figures and dates are as the snippets reported them.

**Thesis:** "Your agents want to use a new API, data source or tool every day; your procurement and security review takes 3 months. We approve vendors at agent speed." The product would combine:
- a pre-vetted vendor catalog that is monitored continuously;
- policy-based instant approval for low-risk vendors, with high-risk vendors routed to humans;
- review of legal terms and the data processing agreement (DPA);
- spend caps;
- enforcement at a gateway or through credentials.

The buyer would be the CISO, head of procurement or CTO.

## Verdict: **KILL** (average score 5.4; four categories below 7)

**Cause of death:** F1 (platform absorption) combined with F2 (visible-pain race). The pain is real and loud. Each piece of the product already has a funded owner or a platform feature, all shipped in the last 6 to 9 months:
- **Procurement intake plus vendor risk:** Zip.
- **Vendor risk review automated by AI agents:** Vanta, Whistic, Drata.
- **Re-checking risk as employees adopt new tools:** Nudge Security.
- **Allowlists for agent tools (MCP servers) plus enforcement:** JFrog, Runlayer, MintMCP, Claude Code managed MCP, Microsoft Agent 365.
- **Spend limits per provider for agent-provisioned services:** Stripe Projects, Ramp agent cards.

**What is left uncovered:** the policy that *links* these pieces. For example: "an agent may provision any vendor that has SOC 2, an approved DPA and EU data residency, under $500 a month." That is a workflow on top of Zip/Vanta plus a gateway. It is not a new system of record. And the premise that agents choose a brand-new vendor every day has **no public evidence**: agents in production mostly call catalogs that admins curated.

---

## 1. Evidence that approval is the bottleneck (strong, but it is about *human* adoption of AI tools)

| Signal | Source | Note |
|---|---|---|
| IT security review is the biggest delay between choosing a vendor and completing the purchase (39%). 50% of enterprise buyers name it as their top post-selection delay. 40% say evaluation is the longest stage. | [G2 2026 Buyer Behavior Report](https://sell.g2.com/2026-buyer-behavior-report?hsLang=fr); [Sovereign Magazine summary](https://www.sovereignmagazine.com/article/g2-ai-software-evaluation-report-2026) | Vendor survey *(figures unverified on page)* |
| "Is your security review process where AI initiatives go to die?": a 4-month vendor assessment stalls an AI pilot, and security teams describe a backlog. | [Netskope blog, May 7 2026](https://www.netskope.com/blog/is-your-security-review-process-where-ai-initiatives-go-to-die) | An incumbent is already marketing against this pain, which is the F2 signal |
| 30% of professionals say "approval processes are too slow or unclear" is a reason they use AI tools without approval. 54% use personal AI tools because company adoption is too slow. | [SalesAPE](https://www.salesape.ai/articles/the-real-reason-your-team-is-already-using-ai-without-asking) | Small vendor survey *(unverified)* |
| Unapproved AI use on corporate devices rose from 15% to 45% of the workforce (attributed to the Verizon 2026 DBIR). 66% of office workers used AI they thought was not permitted (PagerDuty 2026). | Repeated in search summary from [Deel](https://www.deel.com/deel-works/shadow-ai-workplace) / [softwareseni](https://www.softwareseni.com/shadow-ai-and-the-governance-gap-enterprises-are-not-measuring/) | Second-hand *(unverified)* |
| Large enterprises add an average of 21 applications a month. Spend on AI-native apps is up 108% overall and up 393% at companies with more than 10,000 employees. Much of it is bought on credit cards. | [Zylo 2026 SaaS Management Index](https://zylo.com/reports/2026-smi/) | The best "rate of adoption" data point |
| 63% of TPRM programs have 1 or 2 full-time staff, and more than half manage 300+ vendors. | [Ncontracts 2026 TPRM survey](https://secure.businesswire.com/news/home/20260312118257/en/Ncontracts-Releases-2026-State-of-Third-Party-Risk-Management-Survey-Report) | Financial institutions skew |
| 78% say limited staff or tools restrict how many third parties they can assess. | [Drata State of TPRM 2026](https://drata.com/resources/reports/state-of-tprm-2026) | Vendor survey |
| 1,465 respondents report prolonged assessment cycles. | [ProcessUnity / Ponemon-Sullivan, Mar 2026](https://ponemonsullivanreport.com/2026/03/state-of-third-party-risk-assessments/) | |
| The CSA AI Controls Matrix (243 controls) adds 1 to 2 weeks to AI vendor reviews. | [Reco CISO hub](https://www.reco.ai/ciso-hub/how-to-evaluate-ai-security-vendors) *(unverified)* | |
| Public MCP registry: about 9,652 server records (May 24 2026). Directories list more than 20,000. Local MCP servers were downloaded about 67M times in April 2026. | [Nordic APIs](https://nordicapis.com/10-interesting-mcp-statistics/); [Archestra](https://archestra.ai/blog/state-of-mcp-2026) | The supply is large. **No source gives the number of MCP servers per enterprise.** |
| About 2/3 of 36,500 public MCP servers are not safe for enterprise use. 41% of about 7,000 require no authentication (BlueRock). | [PointGuard AI](https://www.pointguardai.com/blog/we-tested-36-500-public-mcp-servers-two-thirds-arent-safe-for-enterprise-use) | Makes the case for vetting, and shows vetting is already a product |
| Agents provision and pay for services on their own: Stripe Projects lists 49 providers, and transaction volume reportedly grew from 70K (March) to 560K (June). | [Stripe blog](https://stripe.com/blog/stripe-projects-adds-new-agents-providers-developer-controls); [Cobo summary](https://www.cobo.com/agentic-wallet/news/stripe-projects-enables-ai-agents-to-autonomously-register-and-pay-for-s) *(volume figure unverified)* | The only real evidence of "agent-chosen vendors". It is small, and mostly developer infrastructure. |

**Read:** the backlog is real and quantified. But the evidence describes *employees* adopting AI SaaS tools, which existing tools cover: Zylo, Nudge, Zip and Vanta. "Agents choosing new vendors daily" in enterprises is not shown. It exists in developer and startup settings (Stripe Projects, coding agents) where nobody runs procurement anyway.

## 2. Competitors (is anyone doing "instant policy approval plus enforcement"?)

| Layer | Player | What they shipped (date) | Overlap with thesis |
|---|---|---|---|
| Procurement intake plus TPRM | **Zip** ($2.2B valuation, Series D, Oct 2024) | AI Risk Orchestration (Apr 2025), expanded into full TPRM at Zip Forward 2026. Claims 85% faster cycle times and up to 90% less manual review. Intake Superagent; Preferred Vendor Agent that surfaces approved suppliers at intake; Zip MCP; 50 agents. Customers include Anthropic, OpenAI and Stripe. ([Zip AI summit recap](https://zip.com/blog/zip-ai-summit-2026-recap); [Procurement Mag](https://procurementmag.com/news/everything-from-opening-keynote-zip-forward); [Zip $52B risk release](https://www.businesswire.com/news/home/20250401038182/en/Zip-Expands-into-$52-Billion-Risk-Management-Market-as-98-of-Companies-Face-Third-Party-Breach-Exposure)) | **High.** Policy-routed intake with fast risk review. Zip MCP means agents can file the request themselves. |
| Intake | **Omnea** ($50M Series B, Sep 2025; >$75M total; revenue up 5x) | AI intake, automated risk detection, MCP server (June 2026). ([Pulse2](https://pulse2.com/omnea-50-million-raised-for-ai-based-procurement-intake-and-orchestration-platform)) | High |
| AI-native procurement plus risk | **Coverbase** ($20M; Series A led by Canapi) | Autonomous Intake Workflow, Risk Assessment Copilot, Contract Guardian; AI governance controls added Jul 20 2026 ([Pulse2](https://pulse2.com/coverbase-20-million/); [fintech.global](https://fintech.global/2025/11/20/coverbase-unveils-ai-procurement-platform-after-20m-raise/)) | **Very high.** Closest startup match on the "vendor approval at speed" pitch. |
| TPRM | **Vanta** | AI agent runs vendor reviews end to end. Acquired Riskey (Jul 2025) for continuous monitoring. ([Vanta](https://www.vanta.com/resources/vanta-acquires-riskey); [HelpNet](https://www.helpnetsecurity.com/2025/09/09/vanta-ai-risk-management-workflows/)) | High |
| TPRM | **Whistic** | Vendor Monitoring (Mar 24 2026, breach scans every 30 minutes). Automation Orchestrator / AutoAssess with 4 agents (Aug 18 2026). *(dates from snippet, unverified)* | High |
| TPRM plus trust network | **Drata + SafeBase** ($250M acquisition) | TPRM agent reads vendor trust centers to complete assessments ([Drata help](https://help.drata.com/en/articles/15453390-safebase-trust-center-integration-in-drata-tprm)) | High. This is the "pre-vetted catalog" network effect, and it is already owned. |
| Others | OneTrust, ProcessUnity, Mitratech/Prevalent, SecurityScorecard, BitSight, Panorays, UpGuard | Ratings plus questionnaires | Medium |
| SaaS / shadow AI | **Nudge Security** | Adaptive Risk Management (Sep 30 2026): re-assesses risk continuously as employees adopt tools and OAuth grants. Agents act on authorised steps. Thousands of vendor security profiles. ([press](https://www.nudgesecurity.com/press/nudge-security-unveils-adaptive-risk-management)) | **Very high** for tools humans adopt |
| SaaS management | Zylo, Torii, Productiv, CloudEagle | Discovery, spend, renewals | Medium |
| Security review automation | **Clearly AI** ($8.4M seed, Feb 2026; RSAC 2026 Sandbox finalist); Conveyor (vendor side) | Automates internal security and privacy reviews ([Zeltser](https://zeltser.com/media/rsac-2026-sandbox/clearly-ai)) | Medium |
| AI legal governance | **Luminos.ai** ($17.25M) | Product is built around a "Time To Approval" metric ([Luminos](https://www.luminos.ai/resource-center/the-ai-goldilocks-window)) | Medium; same pitch, different object (AI systems, not vendors) |
| MCP registry / gateway | **Runlayer** ($11M seed, Khosla/Felicis) | Private MCP registry (18K+ servers), pre-approved directory, permissions mapped to Okta/Entra ([seedtable](https://seedtable.com/companies/runlayer/funding-rounds/seed-2025-11)) | **High** on the enforcement side |
| MCP registry / gateway | **JFrog** MCP Registry (Mar 19 2026) | Zero-trust: blocked by default. Curation shows vulnerabilities, licenses and approval status. Enforced in Claude Code and Cursor ([JFrog](https://jfrog.com/ai-catalog/mcp-registry/); [BusinessWire](https://www.businesswire.com/news/home/20260318132919/en/)) | **High.** An incumbent with an existing package-curation business. |
| MCP registry / gateway | MintMCP (Okta integration Jul 29 2026), Arcade ($60M Series A, Jun 2026), Composio, Docker MCP catalog, Smithery, Gravitee, ServiceNow AI Gateway, Harmonic (remote MCP gateway), Prompt Security/SentinelOne | Allowlist, identity and audit | High |
| Agent spend | **Stripe Projects** (per-provider and global monthly spend limits); **Ramp** agent cards (merchant, vendor and category restrictions, Apr 2026) | ([Stripe docs](https://docs.stripe.com/cli/projects/billing); [Ramp](https://ramp.com/blog/virtual-cards-for-ai-agents)) | High on the spend-cap and enforcement side |
| Contract / DPA | Ironclad, LegalFly, Vallor, DataGrail DPA skill, CassidyAI | AI review of DPAs in seconds ([LegalFly](https://www.legalfly.com/post/how-to-review-data-processing-agreements-with-ai)) | A commodity capability |

**Is anyone doing exactly "instant policy-based approval plus enforcement for vendors an agent chose"?** Not as one SKU that I found. But the result is **assembled from 2 or 3 tools the buyer already owns**:
1. **Zip, Coverbase or Omnea** for policy routing and auto-approval of low-risk requests.
2. **Vanta, Whistic or Drata** for automated risk scoring.
3. **Runlayer, JFrog or Agent 365** for allowlist enforcement, or **Stripe Projects / Ramp** for spend enforcement.

Zip's stated 2030 vision, "agentic procurement orchestration", is this thesis ([01net](https://www.01net.it/zip-named-a-leader-for-the-second-time-in-idc-marketscape-for-worldwide-ai-enabled-spend-orchestration-2026-vendor-assessment/)). Hackathon projects implement the exact "low-risk fast path / human review / reject" flow (GateKeeper, VendorPulse on lablab.ai), which is a sign the idea is sprint-buildable (F5).

## 3. Platform absorption risk: **very high**

- **Microsoft Agent 365:**
  - Approval policies for MCP servers and connected agents live in the M365 admin center.
  - Microsoft pre-certifies the servers in its catalog.
  - Its own guidance says third-party servers "require additional vendor risk assessment", which is exactly where a TPRM integration plugs in.
  - Source: [Zero Trust workshop AI_170/171](https://microsoft.github.io/zerotrustassessment/ja/docs/workshop-guidance/AI/AI_170).
- **Okta:**
  - Agent SSO went GA on Aug 24 2026, free in core SSO across 20,000+ customers.
  - Cross App Access has more than 25 integrations.
  - Okta controls which apps an agent may connect to ([IT Brief](https://itbrief.com.au/story/okta-expands-ai-agent-access-controls-with-25-links)).
- **Anthropic and Cursor:**
  - Claude Code supports `allowManagedMcpServersOnly` and a server-managed allowlist pushed from the admin console ([docs](https://code.claude.com/docs/en/managed-mcp)).
  - Cursor team dashboards lock the MCP allowlist.
- **ServiceNow:**
  - AI Control Tower registers MCP servers with vendor and risk class and routes approvals.
  - ServiceNow also sells TPRM and procurement, so it can close the loop natively ([eesel](https://www.eesel.ai/blog/servicenow-ai-control-tower-risk-compliance); [diginomica](https://diginomica.com/servicenow-knowledge-2026-ai-control-tower-expands-autonomous-workforce-reaches-every-function-and)).
- **Zip:** already combines intake, TPRM and the approved-vendor list, and exposes an MCP server. Adding "agent-filed request with an instant decision" is a feature release for Zip.
- **Stripe and Ramp:** own the payment rail where an agent's purchase actually happens. Vendor allowlists are already a card control.

**Is the incumbent structurally prevented from acting?** No. None of these players has a conflict of interest; faster approval *increases* usage on every one of their platforms. This fails taxonomy constraint §4.4.

## 4. Market sizing

- **Buyer count:**
  - US/EU companies with formal TPRM and procurement and active agent programs: roughly 15,000 to 25,000 with 500 or more employees *(assumption)*.
  - Those whose agents actually provision *new external vendors* on their own: likely under 1,000 today *(assumption; no data)*.
- **Contract size (ACV):**
  - TPRM and intake tools: about $30K to $250K *(market norm, unverified)*.
  - A standalone "agent approval policy layer" competing for the same budget: about $25K to $75K.
- **TPRM market size:** estimates range from $8B to $16.8B for 2026, depending on scope ([orbiqhq summary](https://www.orbiqhq.com/vendor-risk-management/third-party-risk-management-software)). The money exists, but it already flows to the incumbents above.
- **$10M ARR:** about 200 customers at $50K. Plausible only as a Zip or Vanta add-on, and likely to be acquired or copied first.
- **$100M ARR:** about 2,000 customers at $50K. That would require displacing Zip, Vanta or Drata as the procurement/TPRM system of record, and those companies already ship agents. There is no plausible path without owning the whole niche, so this fails §4.5.

---

## Finalist format

- **One-line problem:** Agents and employees adopt new AI tools, APIs and MCP servers faster than security, legal and procurement can review them, so adoption stalls or turns into shadow AI.
- **Why now:**
  - Enterprises add about 21 apps a month (Zylo).
  - More than 20K public MCP servers exist.
  - Stripe Projects lets agents provision and pay for services on their own.
  - Security review is the top post-selection delay (G2 2026).
- **Exact buyer:** CISO (security review), with the head of procurement as co-signer. Secondary: the CTO who owns the agent platform.
- **Exact ICP:** Tech-forward companies with 1,000 to 10,000 employees, already running Zip or Omnea plus Vanta, Drata or Whistic, with Claude Code or Cursor rolled out to more than 200 engineers and 50+ MCP-server requests a quarter.
- **Current workaround:**
  - Zip/Omnea intake with risk-tiered routing.
  - Vanta/Whistic AI-agent assessments.
  - A Nudge "experiment until it is business-critical" policy.
  - Managed MCP allowlists (Claude Code, Cursor, JFrog, Runlayer).
  - Stripe Projects per-provider spend limits, or Ramp agent cards.
- **Why incumbents cannot easily own it:** **They can, and they are doing it.** Zip, ServiceNow, Microsoft and JFrog each own one side, and none has a conflict of interest. Only a thin claim survives: no single vendor yet joins TPRM status to gateway enforcement in real time.
- **30-day MVP:**
  - A policy engine: risk tier from Vanta/Whistic/SafeBase data, plus DPA clause check, plus spend threshold.
  - Its decisions write to the Claude Code managed-MCP allowlist, Runlayer/JFrog, and Stripe Projects provider limits.
  - Slack approval for anything above the low-risk tier.
- **Pilot design:**
  - 3 customers, 30 days.
  - Measure median time from request to approval for MCP-server and API requests: baseline compared with the pilot.
  - Success: under 1 hour for 70% of requests, with zero policy violations.
- **Pricing hypothesis:** $30K to $60K a year platform fee, or $2K to $5K per approved vendor-connection a year. Neither reaches $100M ARR.
- **Expansion path:**
  - Renewal and continuous re-assessment.
  - Agent spend governance.
  - Becoming the approved-vendor system of record. That collides directly with Zip and Coupa.
- **Moat:**
  - A shared catalog of pre-vetted vendors (a network effect).
  - **Already held by** the Whistic network, Drata/SafeBase (8,500+ trust centers), Nudge's vendor security profiles, Runlayer's 18K servers, and the JFrog curation database.
- **Why it could be $10B+:** It would need to become the control point for all agent-to-vendor commerce, the "Okta for agents buying things" (Gartner forecasts 90% of B2B buying intermediated by agents by 2028, [DC360](https://www.digitalcommerce360.com/2025/11/28/gartner-ai-agents-15-trillion-in-b2b-purchases-by-2028/)). That slot is being contested by Stripe, Ramp, Zip and Okta, each from a stronger starting position.
- **Direct competitors and adjacent threats:** Zip, Coverbase, Omnea, Levelpath, Vanta, Whistic, Drata/SafeBase, Nudge Security, Runlayer, JFrog, MintMCP, ServiceNow AI Control Tower and AI Gateway, Microsoft Agent 365, Okta Agent SSO, Stripe Projects, Ramp.
- **One sentence to a CTO:** "Any agent or engineer can start using a new API or MCP server within an hour, but only if it meets your security, DPA and spend policy, and the gateway blocks everything else." *(Likely reply: "Zip plus Runlayer does that.")*
- **5 customer discovery questions:**
  1. How many new external APIs or MCP servers did agents or engineers request last quarter, and how many were initiated by an agent rather than a person?
  2. What is the median time from request to approval for a low-risk developer tool today, and what does a day of delay cost?
  3. Does your Zip/Omnea risk-tiered auto-approval already handle this? If not, what specifically breaks?
  4. Who enforces the decision at runtime (MCP allowlist, card controls, network), and is the link to the TPRM record manual?
  5. Would you pay a separate vendor for this, or wait for Zip, Vanta or Microsoft to add it?
- **Hard kill criteria (already met):**
  - The incumbent with the purchase workflow (Zip) ships risk orchestration and an agent intake/MCP interface: **met**.
  - At least 3 funded startups sell parts of the bundle: **met** (Coverbase, Runlayer, Nudge, MintMCP, Arcade).
  - Enforcement is native in the agent clients: **met** (Claude Code managed MCP, Cursor, Agent 365).
  - No public evidence of daily agent-initiated adoption of new vendors inside enterprises: **met**.

### Scores

| Category | Score | Rationale |
|---|---|---|
| Pain | 7 | The backlog is quantified (G2, Netskope, Ncontracts) |
| Urgency | 7 | Shadow AI is rising; CFO pressure on AI ROI |
| ROI clarity | 6 | Cycle-time savings are claimed by incumbents (Zip: 85% faster) |
| Customer accessibility | 6 | The CISO is the most-pitched buyer (taxonomy §3) |
| Pilot speed | 6 | Needs integrations into TPRM, intake and gateway |
| Market size | 6 | The TPRM budget is large but already allocated |
| Expansion | 5 | Every expansion path collides with Zip, Coupa or ServiceNow |
| Venture potential | 4 | Reads as a Zip, Vanta or Runlayer feature |
| Defensibility | 3 | The vetting-catalog network effect is already owned by others |
| Why now | 7 | Real: MCP, Stripe Projects, agent cards |
| Competition position | 2 | Incumbents and funded startups on every side |
| **Average** | **5.4** | **KILL**: F1 + F2. Fails §4.1, §4.2, §4.4 and §4.5. |

### Why not B

B requires the thesis to be genuinely new and too early for public evidence. Here the opposite holds: the pain is public, incumbents market against it by name, and the pieces ship monthly.

One sub-question really is untested: *whether agents in enterprises choose new paid vendors on their own at meaningful volume*. If that happens, the right product is not an approval layer. It is the payment and identity rail, which Stripe, Ramp and Okta already hold.

**Signal worth watching (not a thesis):** Stripe Projects transaction volume, and whether Stripe adds org-level "approved provider" policies that read TPRM data. If Stripe partners with Vanta or Zip for that, this space is closed.
