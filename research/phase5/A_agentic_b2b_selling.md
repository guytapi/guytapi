# Phase 5 Deep Research: Thesis A, Agentic B2B Selling (seller side)

**Thesis tested:** "AI agents are becoming the buyers; we make every B2B supplier/distributor sellable to them." This is a seller-side layer that detects, qualifies and serves AI-agent buyers. It covers machine-readable customer-specific pricing, stock, lead times, quotes and RFQs, credit terms, order placement and approvals, plus routing real deals to humans and analytics on agent-originated demand.

**Date:** 2026-10-05. **Method:** 35 web searches. Most direct page fetches were blocked by the proxy (distributionstrategy.com, ucpchecker.com, salesforce.com), so many facts come from search-result summaries. These are marked **[summary-only]** where it matters. **[unverified]** means a claim I could not confirm from a primary source. **[estimate]** means my own arithmetic.

---

## TL;DR

- **Verdict: REFRAME.** The direction is right. But the thesis as written ("buyers are AI agents, make every supplier sellable to them") describes a channel that does not yet exist at measurable volume in B2B in 2026.
- The agent activity that **can** be observed comes through two routes, and neither one is "open-web agent buys from a supplier storefront":
  1. **Buyer-side procurement suites and agents reaching suppliers through email, portals and punchout.** Examples: Fairmarkit autonomous RFQs, Pactum negotiations, Didero supplier emails, SAP Ariba Joule intake.
  2. **AI-assistant referrals.** Humans research in ChatGPT and then click through to the supplier site.
- Incumbents have moved fast on the "sellable to agents" plumbing:
  - Salesforce Buyer Agent (B2B ordering with contract pricing).
  - MCP servers from commercetools, Adobe, BigCommerce, Microsoft Dynamics and Algolia.
  - TradeCentric UPOP (agentic punchout).
  - Webscale "Agentic Commerce OS" and Intershop.
  - Shopify B2B catalogs.
- The gap that is still open is narrower: **governed pricing and negotiation authority for suppliers facing buyer-side agents.** In other words, the seller's counterpart to Pactum, Fairmarkit and Didero.

---

## 1. Demand reality: is agent-originated B2B purchasing happening, measurably?

### Observed behaviour (hard data points)

| Signal | Data point | Type | Source |
|---|---|---|---|
| Buyer bots negotiating with suppliers at scale | Walmart uses Pactum with 2,000+ suppliers (US, Chile, South Africa). 68% supplier agreement rate, ~3% average savings, average **35-day payment-term extension**. ~75–80% of suppliers said they preferred the bot. | **Observed** (vendor- and press-reported) | brainstation.io/magazine/walmart-automates-supplier-negotiations-with-ai-platform-pactum ; chainstoreage.com/walmart-automates-supplier-negotiations **[summary-only]** |
| Autonomous RFQs sent to suppliers | Fairmarkit runs RFQs autonomously for tactical spend (<$50K): it invites suppliers, compares bids and awards POs. "Total Agentic Sourcing" extends this to strategic spend. Fairmarkit and Zip integrate intake to sourcing. | **Observed** product in production. No public volume figures. | fairmarkit.com/blog/fairmarkit-partners-with-zip-to-power-source-to-pay-with-autonomous-sourcing ; resources.rework.com/tools/ai-agents/best-ai-agents-for-procurement-2026 |
| Buyer-side agents emailing suppliers | Didero raised a $30M Series A (Chemistry, Headline, M12, Feb 2026). Its agents handle supplier communications, quotes and POs for 30+ manufacturers and distributors. | **Observed** (small base) | digitalcommerce360.com/2026/02/20/didero-30-million-funding-ai-procurement/ |
| Procurement suites shipping agents | SAP Joule Agents in Ariba Intake/Contracts are planned for GA in June 2026, with free runtime until 31 Dec 2026. Coupa Compose and Navi Agent Studio were announced at Inspire 2026. | **Shipping, early.** Intake-side, not yet transacting with supplier agents. | sapinsider.org/blogs/sap-delivers-joule-agents-across-ariba-and-fieldglass-in-june-2026/ ; erp.today/sap-joule-agents-ariba-fieldglass-procurement-automation-2026/ |
| AI referrals to B2B sites | ChatGPT-referred visits to B2B web properties grew from ~645K/month (Jun 2025) to **2.6M/month (Jun 2026)**, +303% (Demandbase data). | **Observed**, but this is *humans referred by an assistant*, not agents buying | cmswire.com/the-wire/chatgpt-referrals-to-b2b-websites-nearly-quadrupled-in-a-year-demandbase-data-shows/ |
| Shopify telemetry (mostly B2C) | AI-driven traffic up 7x and AI-attributed orders up 11x since Jan 2025. Agentic Storefronts live for US merchants since 24 Mar 2026. | Observed, B2C-dominated | search summaries of Shopify Editions coverage **[summary-only]** |
| Distributor adoption (seller side) | DSG "State of Agentic AI in Distribution 2026" surveyed 146 North American distributor executives in May 2026: **3 of 4 are not scaling agentic AI**. Elsewhere, 22% are deploying and 78% waiting. | Survey | distributionstrategy.com/report/state-of-agentic-ai-in-distribution-2026/ **[summary-only]** |
| Large distributors' public commentary | Grainger's 2026 calls describe AI applied to its own sales and product data (SellerInsights, KeepStock). I found **no disclosure of agent-originated customer orders** from Grainger, Fastenal or MSC. Fastenal reports 61.5% "digital footprint" sales, which means EDI, eProcurement and vending, not AI agents. | Absence of evidence | digitalcommerce360.com/2026/02/04/grainger-ai-sales-marketing-keepstock-tools/ ; MSC 8-Ks on sec.gov |

### Forecasts and hype (not observed)

- Gartner: AI agents will intermediate **$15T of B2B spend by 2028**, and 90% of B2B buying will be agent-intermediated by 2028. This is a forecast and is widely recycled by vendors.
- Forrester Predictions 2026: about 1 in 5 B2B sellers will face agent-led quote negotiations by the end of 2026 (forrester.com/blogs/predictions-2026-the-agentic-commerce-race-and-some-potential-regrets-in-digital-commerce). I found no follow-up measurement.
- "Nearly 40% of B2B buyers use agentic AI in purchasing; 24% of suppliers use agents" (elogic.co/blog/ai-agents-b2b-buying/). This is an agency blog with an unclear primary source. **[unverified]**
- Forecasts for agentic commerce overall range from $20.6B to $5T, a 240x spread (digitalapplied.com agentic-commerce-statistics-2026). Agent-completed end-to-end sales are **"not yet publicly broken out by any major retailer"**.

### Assessment

Real, measurable B2B agent activity in 2026 is **buyer-enterprise agents run by procurement suites** (Pactum, Fairmarkit, Didero, Ariba and Coupa agents). They reach suppliers through **email, supplier portals, punchout and EDI**, and suppliers almost always answer with humans. Open-web "ChatGPT agent buys MRO parts on a distributor's site with contract pricing" is **not measurable** in 2026. AI-assistant referrals are measurable and growing fast, but the person doing the buying is still a human.

---

## 2. Protocols and platforms: do any handle B2B specifics?

| Protocol / platform | B2B specifics (contract price, customer catalog, RFQ/negotiation, credit terms, approvals) | Evidence |
|---|---|---|
| **UCP (Google + Shopify; Tech Council expanded Apr 2026 to add Amazon, Meta, Microsoft, Salesforce, Stripe)** | **No.** B2B "has not been formally scoped by the Technical Council". The spec reportedly has *zero mentions* of contract pricing, POs, net terms, punchout, quote-to-order or MOQ. Payment is card-at-checkout. | ucpchecker.com/verticals/b2b **[summary-only]** ; mcfadyen.com/articles/b2b-agentic-commerce-what-works-now **[summary-only]** |
| **ACP (OpenAI/Stripe)** | Built for consumer checkout inside ChatGPT. No B2B primitives found. | reveation.io/blog/agentic-commerce-b2b-ucp-vs-acp |
| **AP2 / Visa / Mastercard** | Visa **Intelligent Commerce Connect** explicitly extends to *B2B procurement and bill pay*. It is one integration across TAP, ACP, MPP and UCP. Mastercard Agent Pay is pushing into B2B sourcing with IBM watsonx Orchestrate. Both are payment and identity rails, not pricing or terms. | stellagent.ai/insights/visa-intelligent-commerce-connect-b2b **[summary-only]** |
| **MCP / A2A** | Generic transport only. A2A has 150+ supporting orgs and now sits in the Agentic AI Foundation. | multiple |
| **Salesforce Agentforce Commerce** (GA June/July 2026) | **Partial yes.** *Buyer Agent* handles B2B reorders over WhatsApp and SMS, with SKU confirmation and **contract pricing**. It also offers headless B2B, B2B Search, and catalog channels to ChatGPT (ACP) and Google (UCP). It serves **human buyers via messaging**, not external buyer agents, and has no RFQ negotiation authority. | shopifreaks.com coverage; futurecio.tech; elogic.co **[summary-only]** |
| **Shopify** | B2B company profiles, up to 3 custom catalogs, and net-30/60 terms are now available on Basic plans. Agentic Storefronts syndicate products to ChatGPT, Gemini, Copilot and Meta. I could not confirm whether B2B-specific pricing passes through to agents. **[unverified]** | search summaries |
| **commercetools** | Commerce MCP (May 2025) exposes catalog, cart, pricing and orders. commercetools has company-specific pricing natively. | commercetools.com/press-releases/commercetools-launches-commerce-mcp |
| **Adobe Commerce** | Commits to UCP and ACP (Feb 2026). Its Commerce MCP Server exposes catalog, pricing, inventory and checkout. Adobe Commerce has native B2B quotes and approvals, but I found no evidence these are exposed to agents. | stellagent.ai/insights/adobe-commerce-summit-agentic-upgrades **[summary-only]** |
| **BigCommerce** | MCP server in beta. The "B2B storefront for MCP" is listed as **coming soon**. | bigcommerce.com/blog/b2b-agentic-commerce/ |
| **Microsoft Dynamics 365 Commerce** | MCP server (NRF 2026 / Jun 2026) covering discovery, inventory, pricing, discounts and checkout. | microsoft.com/en-us/dynamics-365/blog/... (Jun 29 2026) |
| **SAP Commerce** | "Most capability is roadmap through 2026". Merchants must deploy the MCP server themselves. | search summary |
| **Optimizely** | Opal agent orchestration. B2B AI features exist, but there is no explicit external-agent B2B API. | optimizely.com blog |
| **TradeCentric UPOP** (May 2026, design-partner stage) | **Closest B2B-native one.** "Universal PunchOut Platform", a governed integration layer for "buyers, suppliers, and AI agents" with "relationship-specific rule enforcement" and "approval-aware purchasing logic". TradeCentric already sits between suppliers and Ariba/Coupa. | tradecentric.com/news/tradecentric-introduces-upop/ |

**Conclusion:** No open protocol handles RFQ/negotiation, credit terms or approvals. That gap is real. But the commerce platforms that hold the contract-price engines (Salesforce, commercetools, Adobe, SAP, Dynamics) are each adding MCP endpoints. The punchout incumbent (TradeCentric) is explicitly building the "agentic punchout" layer. The **data-exposure** part of the thesis (machine-readable customer-specific price, stock and lead time) will be **commoditized by platforms**. The **policy and negotiation** part (what may I quote this agent, at what discount, with what terms, and when does a human step in) is less covered.

---

## 3. Competitors

| Name | What | Funding (as found) | Seller-side B2B? |
|---|---|---|---|
| **TradeCentric (UPOP)** | Punchout/cXML middleware between suppliers and procurement systems. Building governed "agentic punchout". | Private, established. Funding not checked. | **Y** (closest structural threat) |
| **Salesforce Agentforce Commerce (Buyer Agent)** | B2B ordering agent with contract pricing over messaging, plus ChatGPT/Google catalog channels. | Incumbent | **Y** (for human buyers) |
| **Webscale (Agentic Commerce OS)** | B2B commerce infrastructure repositioned to agentic commerce for dealers and distributors. | Strategic round led by BGV (2025), amount undisclosed. | **Y** |
| **Intershop** | B2B commerce platform with copilots and agents (Spring 2026). | Public (DE) | Y |
| commercetools / Adobe / BigCommerce / MS Dynamics / Algolia | MCP servers exposing catalog, price and stock to agents. | Incumbents | Partial (plumbing) |
| **Proton.ai** | Distributor CRM. Agentic Order & Quote Entry GA in Jul 2026: drafts quotes, follows up, sources substitutes. | VC-backed (amount not checked) | Y (human-originated inbound) |
| **Endeavor** | Agents for order entry, quoting and AP at manufacturers (ClarkDietrich, Bridgestone Americas). | $7M seed (Craft) | Y (quote automation) |
| **Mercura** | Quote automation for industrial wholesale. | €1.8M seed (Jan 2026; TQ, SignalFire, YC) | Y (quote automation) |
| **Korso** (YC S26), **Lark** (YC F26), **Whitespace** (YC S26) | Inbound RFQ to quote, and distributor ops agents. | YC | Y (ops automation) |
| **Anglera** (YC) | AI product-data enrichment and AEO for MRO/industrial distributors. | YC; amount not checked | Y (data layer) |
| **ChatSKU** | Makes B2B catalogs "searchable, quote-ready and agent-ready". | Unknown | Y (small) **[unverified scale]** |
| **Threekit** | Configuration and AI web agent for manufacturers selling through dealers. | $65M total | Y (CPQ/config) |
| **ReFiBuy** | "Agentic Commerce Optimization" of catalogs for AI shopping agents. | $13.6M seed (NewRoad) | N (brands and retailers, B2C) |
| **Profound** | GEO/AEO monitoring, Agent Analytics (crawler traffic). | $180M Series D at $1.8B | N (marketing, horizontal) |
| **Scrunch (AXP)** | Serves machine-readable pages to AI crawlers. | Acquired by Sitecore ~$225M (Jun 2026) | N |
| **Firmly (Firmly Connect)** | No-code merchant connection to AI shopping agents. | Not checked | N (B2C) |
| **Rye**, **Crossmint**, **Nekuda** ($5M seed), **Skyfire** ($9.5M), **Basis Theory** ($33M B), **Sapiom** ($15.75M seed), **Payman** | Checkout execution, agent wallets and payment rails. | as listed | N |
| **Pactum** | Buyer-side negotiation agent (Walmart, Maersk). | $108M total (Series C) | N (buyer side, which is the demand creator) |
| **Fairmarkit**, **Zip**, **Coupa**, **SAP Ariba Joule**, **Didero** ($30M A) | Buyer-side autonomous sourcing, intake and supplier communications. | Fairmarkit ~$78M total **[unverified]** | N (buyer side) |
| PROS / Zilliant / Vendavo | Price optimization. PROS AI Agents (2025) are internal sales-assist. No external buyer-agent interface found. | Incumbents | Partial (pricing engine owners; natural acquirers or competitors) |
| Salsify / Syndigo / Akeneo / inriver | PIM/PXM pushing "agent-ready product data". inriver publishes "B2B agentic commerce can't run on retail protocols". | Incumbents | Partial (data only) |

**Who is closest?** For the full thesis: **TradeCentric UPOP + Salesforce Buyer Agent + platform MCP servers**. Combined, they cover data exposure, governed transaction rails and contract-priced ordering. For the "detect, qualify and route agent RFQs" piece: **Proton.ai and Endeavor/Mercura**, which already own inbound quote automation and can add an "agent-originated" flag. I found **no funded startup positioned as "the seller's negotiation agent against Pactum/Fairmarkit-style buyer agents"**. That is the empty square.

---

## 4. Buyer, target count and ACV

**Economic buyer:**
- Primary: **VP/SVP Digital or eCommerce, or Chief Digital Officer** at $500M+ distributors. They own the web store, punchout, EDI and PIM budget.
- For the negotiation and pricing wedge: **VP Pricing / VP Sales Ops or CRO** (margin authority).
- CIO/IT approves the ERP and pricing-engine integration.
- At $100–500M distributors there is often no CDO. The buyer becomes the COO or VP Sales, the sales cycle is slower, and budgets are smaller.

**Target counts (bottom-up):**
- US wholesale: >330K distributor establishments (Census) and ~25K wholesaler-distributors served by NAW.
- **Count of $100M+ US distributors: no public figure found.** My estimate is **~3,000–5,000** **[estimate, unverified]**, by triangulating MDM top-distributor lists and the long-tailed revenue distribution.
- EU: similar, **~3,000–4,000** **[estimate]**.
- Share offering ecommerce: DSG reports ~37% at $50–100M and ~51% at $1B+ (DSG 2022/23 State of eCommerce, older data). Using ~45% gives **~3,000 US+EU distributors with transactional B2B ecommerce at $100M+ revenue**.
- Add $100M+ manufacturers selling direct B2B with contract pricing (components, chemicals, packaging): perhaps **~4,000–6,000 US+EU** **[estimate]**.
- **Total addressable accounts ≈ 7,000–9,000.** The near-term buyable core is the **top ~1,000 distributors** that have digital teams, punchout and PIM.

**ACV:**
- Comparables:
  - PIM and B2B commerce add-ons run $50–250K/yr.
  - Pricing software (PROS/Zilliant) is $150K–1M+ at large distributors **[unverified]**.
  - Quote-automation startups are likely $30–100K **[unverified]**.
- Realistic for this product: **$40–80K** at entry (one agent channel plus analytics), rising to **$100–250K** with negotiation authority, ERP pricing integration and multiple channels.

**Market math [estimate]:**
- Core: 1,000 top distributors × $80K = **$80M** near-term SAM.
- Full: 8,000 accounts × $75K = **$600M** subscription TAM in US+EU.
- Transaction upside: if agent-originated orders reach ~5–10% of US B2B ecommerce (several $T) by 2030–32, a 0.1–0.2% take on agent-originated GMV adds **$0.3–1B+**. This is speculative and depends on protocol position.
- Venture-scale only if the transaction or network layer materializes. A pure SaaS "agent-readiness" tool tops out in the low hundreds of millions of dollars.

---

## 5. Wedge test: what can be piloted in 90 days with value today?

| Candidate wedge | Value today (low agent volume)? | Differentiated? | Verdict |
|---|---|---|---|
| (a) Make catalog, price and stock agent-readable (llms.txt, structured specs, MCP endpoint) and capture AI-assistant-referred demand | Some. ChatGPT referrals to B2B are up ~4x, but volumes are small per distributor. | **No.** Platforms (commercetools, Adobe, BigCommerce, Dynamics, Salesforce) ship MCP. Anglera, PIMs, Profound, Scrunch/Sitecore and ReFiBuy cover data and visibility. | Weak. A feature, not a company. |
| (b) Auto-answer buyer agents' RFQ emails | Yes, but the value is really "answer all RFQs faster", and agent-originated ones are a small slice. | **No.** Mercura, Endeavor, Proton.ai, Korso, Lark and others are crowded. Phase 1 already killed quoting. | Weak alone |
| (c) **Seller-side negotiation and pricing-authority agent for buyer-agent events.** Respond to Pactum, Fairmarkit and Didero-style negotiations, autonomous RFQs and Ariba/Coupa sourcing events. Policy-as-code discount and term authority (floor price, term limits, rebate trade-offs), counteroffers, human escalation, and win/loss and margin analytics by originating agent. | **Yes, measurably.** Walmart's Pactum program alone pushed 2,000+ suppliers to an average **35-day term extension and ~3% price concession**. Every supplier to an enterprise running Fairmarkit autonomous sourcing gets machine-run RFQs today. ROI = concession avoided + bids won + rep hours saved. | **Mostly yes.** No funded seller-side counterpart found. Quote tools optimize extraction, not negotiation strategy against an optimizing counterparty. | **Best wedge** |
| (d) Agent-traffic detection and analytics only ("which of my inbound is machine-originated?") | Low ROI alone | Profound Agent Analytics covers crawlers. Bot-management vendors cover the web. | Bundle into (c) |

**90-day pilot for (c):**
- Target: a $300M–2B supplier (CPG or industrial) that sells to 2–5 enterprise accounts known to run Pactum, Fairmarkit, Coupa or Ariba sourcing agents.
- Ingest: contract terms, price floors, cost-to-serve and historical bid outcomes.
- Run in shadow mode: draft responses and counteroffers for live sourcing events and negotiation chats, with human approval.
- Measure: response time, win rate on tactical RFQs, and margin and terms conceded versus the prior year's baseline.
- Pilot speed is fine. Integrations are email, portal and price-file based.

**Caveats on (c):**
- Event frequency per supplier is low. Strategic negotiations are annual, and tactical RFQs are frequent but small.
- Large-retailer suppliers may resist being seen as "botting back" against Walmart.
- Pricing vendors (PROS, Zilliant, Vendavo) are the natural owners if this becomes obvious.

---

## 6. Kill signals (strongest evidence against the thesis as written)

1. **No measurable open-agent B2B ordering in 2026.** No major distributor discloses agent-originated orders. Even in B2C, agent-completed sales are "not publicly broken out by any major retailer". DSG: 3 of 4 distributors are not scaling agentic AI. Demand for a supplier "agent front door" is anticipatory.
2. **Humans still sit in the loop.** Gartner (May 2026): **69% of B2B buyers turn to sales reps to validate AI-generated insights** (businesswire.com/news/home/20260520585188/en/...). Consumer data shows 14% would let an agent buy unsupervised.
3. **Buyer agents go through existing rails, not new ones.** Ariba Joule, Coupa, Fairmarkit and Didero talk to suppliers via **portals, punchout, cXML/EDI and email**. Those rails are owned by TradeCentric (now building UPOP for agents), SAP Business Network and Coupa supplier networks. A new seller-side protocol layer would have to win against the procurement networks themselves.
4. **Platforms are commoditizing the "machine-readable" layer.** MCP servers from commercetools, Adobe, BigCommerce, Microsoft and Algolia. Salesforce Buyer Agent with contract pricing. Shopify B2B catalogs on Basic. Visa Intelligent Commerce Connect covering B2B procurement.
5. **Standards risk.** UCP's Tech Council now includes Amazon, Microsoft, Salesforce and Stripe. If it scopes a B2B extension (POs, net terms, contract price), the "B2B layer" becomes a free spec implemented by platforms.
6. **Inbound quote automation is crowded** (Mercura, Endeavor, Proton.ai, Korso, Lark, Whitespace). "Answer agent RFQs" collapses into "answer RFQs".
7. **GEO/agent-visibility consolidation.** Profound is at $1.8B and Sitecore bought Scrunch. The "be visible to AI" budget is already captured by marketing tools.
8. **Most forecast numbers are vendor-recycled.** The $15T, 90% and 40%-of-buyers figures appear in agency blogs without primary methodology. Forrester's "1 in 5 sellers face agent negotiations in 2026" has no published follow-up measurement.

---

## Sharpened thesis (best wedge)

> **"Buyer-side AI agents (Pactum, Fairmarkit, Coupa/Ariba agents, Didero) already negotiate and run RFQs against suppliers, and suppliers answer with humans and lose margin. We give suppliers their own governed negotiation agent: policy-as-code pricing and terms authority that responds to machine buyers in seconds, protects margin, escalates real deals to reps, and reports agent-originated demand."**

**Expansion path:**
1. Win tactical RFQs and buyer-bot negotiations (today).
2. Become the supplier's single "agent counterpart policy engine" across email, portals, punchout/UPOP, and MCP/UCP endpoints as B2B primitives arrive (2027–28).
3. Use network position across many suppliers for benchmark data, agent reputation and identity, and possibly take a transaction fee (2029+).

**Fallback if suppliers won't buy (c):** fold A into a pricing-intelligence product for distributors. Phase 1 already flagged that "the defensible angle is pricing intelligence and margin, not extraction."

---

## Scores (1–10)

| Dimension | Score | Rationale |
|---|---|---|
| Pain | 5 | Real for suppliers facing Pactum and Fairmarkit (terms and price concessions). For the generic "be sellable to agents" story, pain is mostly anticipatory. |
| Urgency | 3 | Distributors are mostly waiting (DSG: 3/4 not scaling). No measurable agent order flow. |
| ROI clarity | 4 | Clear for the negotiation wedge (bps of margin, days of terms). Vague for the agent-readiness and analytics wedge. |
| Customer accessibility | 5 | Digital and pricing leaders at the top ~1,000 distributors are reachable. Mid-market lacks owners. Sales cycles run 6–9 months with ERP and pricing integration. |
| Pilot speed | 6 | A shadow-mode negotiation and RFQ pilot via email, portal and price files can be done in 90 days. Full transactional agent access needs ERP work. |
| Market size | 6 | ~$80M near-term SAM and ~$600M subscription TAM [estimate]. Larger only if a transaction layer emerges. |
| Expansion | 8 | Natural path from negotiation to policy engine, protocol endpoints and network/transaction fees. |
| Venture potential | 7 | A big "where the world is going" story, but contingent on agent volume arriving by 2028–30. |
| Defensibility | 4 | Data exposure gets commoditized by platforms. The moat would come from policy, outcome data and network position, none of which exists yet. |
| Why now | 7 | Buyer-side agents are in production (Pactum at Walmart, Fairmarkit autonomous sourcing, Ariba Joule GA June 2026). Protocols lack B2B primitives. |
| Competition position | 4 | The thesis as written loses to platforms plus TradeCentric plus quote tools. The reframed negotiation wedge is open but within reach of PROS, Zilliant and Proton.ai. |

**Average ≈ 5.4**

## VERDICT: **REFRAME**

**Why not ADVANCE:** The core premise, "AI agents are becoming the buyers" at suppliers' storefronts, is **not observable in 2026 B2B data**. The generic "make suppliers agent-readable" layer is being absorbed by commerce platforms (Salesforce, commercetools, Adobe, BigCommerce, Microsoft), punchout incumbents (TradeCentric UPOP) and PIM/GEO vendors. Building it now means selling insurance against a future channel, and the target buyers are explicitly "waiting".

**Why not KILL:**
- One part of the machine-buyer world **is** real and measurable today: buyer-enterprise agents negotiating with and sourcing from suppliers (Walmart/Pactum with 2,000+ suppliers; Fairmarkit autonomous RFQs; Ariba/Coupa agents).
- Suppliers have **no counterpart**, and no funded seller-side startup was found.
- No protocol covers RFQ, negotiation, terms or approvals, so a seller-side policy and negotiation engine can ride whatever rails win.

**Next tests (Phase 6):**
1. Interview 10 suppliers to Walmart, other Pactum clients and Fairmarkit users. How many buyer-bot events do they see per year? What did they concede? Would they pay for a counter-agent?
2. Ask 3 enterprise procurement teams whether they would accept or block supplier-side agents.
3. Check TradeCentric UPOP scope, and whether PROS or Zilliant plan external-agent negotiation.
4. Get a reliable count of $100M+ distributors (MDM/NAW data).

---

## Sources (as found; many via search summaries)

- distributionstrategy.com/report/state-of-agentic-ai-in-distribution-2026/ ; distributionstrategy.com/2026/02/how-agentic-commerce-is-starting-to-reach-wholesale-distribution/
- elogic.co/blog/ai-agents-b2b-buying/ ; elogic.co/blog/agentic-commerce/
- sapinsider.org/blogs/sap-delivers-joule-agents-across-ariba-and-fieldglass-in-june-2026/ ; erp.today/sap-joule-agents-ariba-fieldglass-procurement-automation-2026/
- distributionstrategy.com/2026/04/amazon-business-deploys-ai-across-procurement/ ; marketscale.com (Amazon Business $60B annualized)
- blueboltsolutions.com/ucp-and-b2b-ecommerce/ ; ucpchecker.com/verticals/b2b ; mcfadyen.com/articles/b2b-agentic-commerce-what-works-now
- reveation.io/blog/agentic-commerce-b2b-ucp-vs-acp ; shopifreaks.com (Salesforce Agentforce Commerce B2B) ; futurecio.tech (Salesforce Jul 2026)
- commercetools.com/press-releases/commercetools-launches-commerce-mcp ; algolia.com/about/news/algolia-launches-production-grade-mcp-for-agentic-commerce ; bigcommerce.com/blog/b2b-agentic-commerce/ ; microsoft.com Dynamics 365 Commerce MCP blog (2026-06-29) ; stellagent.ai/insights/adobe-commerce-summit-agentic-upgrades
- stellagent.ai/insights/visa-intelligent-commerce-connect-b2b
- tradecentric.com/news/tradecentric-introduces-upop/ ; tradecentric.com/agentic-commerce/
- webscale.com/press/webscale-announces-jay-smith-as-ceo-and-secures-strategic-funding-to-lead-agentic-commerce-ai-powered-infrastructure/
- fairmarkit.com/blog/fairmarkit-partners-with-zip-to-power-source-to-pay-with-autonomous-sourcing
- brainstation.io/magazine/walmart-automates-supplier-negotiations-with-ai-platform-pactum ; chainstoreage.com/walmart-automates-supplier-negotiations ; tracxn.com (Pactum $108M)
- digitalcommerce360.com/2026/02/20/didero-30-million-funding-ai-procurement/
- proton.ai/blog/proton-ends-rekeying-era-with-agentic-order-quote-entry-automation
- munich-startup.de/en/132383/mercura-secures-e1-8-million/ ; yespress.io/endeavor.md
- accessnewswire.com (ReFiBuy $13.6M seed) ; rye.com/blog/agentic-commerce-startups ; stellagent.ai/insights/agentic-commerce-infra-startups
- sacra.com/c/profound ; search summaries re: Sitecore acquiring Scrunch
- anglera.com/blog/structure-product-data-for-ai-agents ; chatsku.com/ai-ready-b2b-catalog-autonomous-buying/
- cmswire.com/the-wire/chatgpt-referrals-to-b2b-websites-nearly-quadrupled-in-a-year-demandbase-data-shows/
- forrester.com/blogs/predictions-2026-the-agentic-commerce-race-and-some-potential-regrets-in-digital-commerce
- businesswire.com/news/home/20260520585188/en/Gartner-Survey-Finds-69-of-B2B-Buyers-Turn-to-Sales-Reps-to-Validate-AI-Generated-Insights
- digitalapplied.com/blog/agentic-commerce-statistics-2026-data
- ycombinator.com/companies/industry/supply-chain (Korso, Lark, Whitespace)
