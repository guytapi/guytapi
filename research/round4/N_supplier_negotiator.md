# Round 4: Thesis N, the Supplier-Side AI Negotiator ("revenue defense" against buyer bots)

**Thesis tested:** "Big buyers now negotiate with their suppliers using AI agents; we give suppliers their own AI negotiator." The product would detect AI-led negotiations, RFQs and tail-spend auctions run by Pactum, Fairmarkit, Keelvar, Arkestro, Zip, Coupa, Ariba Joule, Globality and Amazon. It would know the supplier's cost-to-serve, margin floors, contract history and each buyer's patterns, then negotiate back within guardrails or coach the rep. It would also build intelligence across all buyer-agent interactions. Pricing would be a subscription plus a share of margin protected.

**Date:** 2026-10-05. **Method:** 35 web searches. WebFetch was not used, so most facts come from search-result summaries. Labels used below:
- **[summary-only]**: taken from a search summary and not read on the primary page.
- **[unverified]**: could not be confirmed from a primary source.
- **[estimate]**: my own arithmetic.

**Stance:** red team. The aim was to kill the thesis.

---

## TL;DR

- **Buyer-side agents are real and accelerating, but they are aimed at the long tail.**
  - Pactum serves 50+ large enterprises, including Walmart, Otto Group, Honeywell, Novartis, Tetra Pak, Linde, AstraZeneca and Maersk.
  - Keelvar says **90% of events on its platform are agent-operated** (July 2026).
  - Fairmarkit, Lio, Zip, Coupa, SAP and Globality all ship sourcing or negotiation agents.
  - These agents are deliberately pointed at **tail spend and small contracts**. Walmart uses Pactum for tail suppliers and for equipment and goods-not-for-resale, not for the merchandise it sells.
- **The money at stake per supplier is small and the events are rare.**
  - The original Walmart pilot got **~1.5% price and payment terms to ~35 days**.
  - Phase 5's "+35 days" reading is probably wrong. At least one source says terms went **from 30 to 35 days**.
  - A typical supplier sees a handful of agent negotiations a year on contracts worth tens to hundreds of thousands of dollars. That is $5–50K of value at risk: a feature, not a $50K+ subscription.
- **Suppliers do not report pain.** In surveys, 75–83% of Walmart's tail suppliers *prefer* the bot. I found no visible supplier backlash (no Reddit or trade-press outrage).
- **The seller-side square is not empty.**
  - Keelvar's own white paper says **supplier-side bidding agents launched in Dec 2025 and joined ~1,420 events/month by July 2026**, mostly in freight, packaging and MRO. The two-sided market is forming *inside the buyer's platform*.
  - Pricing incumbents ship negotiation agents: Pricefx (125+ agents, floor/target/stretch prices), Zilliant (agentic AI plus an MCP server, Q1 2026), Vendavo (Deal Desk Agent) and PROS.
  - Freight quote agents already exist (Pallet/CoPallet, Transfix).
- **The proposed moat is legally toxic.**
  - A cross-supplier "negotiation data network" used by competing suppliers is close to the textbook definition of a **"common pricing algorithm"** under California AB 325, in force since 1 Jan 2026. That law is triggered by tech "used by two or more persons, that uses competitor data to recommend… a price or commercial term", whether the data is public or not.
  - It is also the DOJ's hub-and-spoke theory from the RealPage case.
  - Without the network, there is no moat.
- **VERDICT: KILL** as stated. Two narrow reframes are noted in the Verdict section. Neither is venture-grade today.

---

## 1. Buyer-side adoption, 2024–2026 (evidence)

| Player | What it does to suppliers | Scale / traction | Funding | Source |
|---|---|---|---|---|
| **Pactum** | Autonomous chat negotiations on price, payment terms and contract terms with long-tail suppliers | 50+ large enterprises. 25+ Global 2000 customers added in 2024, including Honeywell, Novartis and Tetra Pak. Also Walmart, Veritiv, Suez, Linde, Otto Group (Crate & Barrel, Hermes, Evri) and AstraZeneca (Coupa Inspire 2026). Dollar value handled up 489% in 2024; ARR 2.5x. "Up to 10,000 negotiations simultaneously." One summary says "$529M in supplier contracts" **[summary-only, context unclear]**. | $54M Series C (Insight, Jun 2025); >$100M total | siliconangle.com/2025/06/09/pactum-raises-54m-procurement-automation-platform/ ; procurementmag.com/news/pactum-secures-series-c-funding-to-drive-agentic-ai-adoption ; samsearch.co (Pactum $529M) |
| **Walmart × Pactum** | Tail suppliers, **"only for smaller contracts and only with suppliers that provide equipment it uses, rather than goods it sells"** | 2,000 suppliers at once. 68% close rate, ~3% average savings. Pilot: 64% deal rate in ~11 days, **~1.5% savings, terms "to 35 days" / "from 30 to 35 days"**. 75% of suppliers prefer the bot; 83% find it easy to use. | — | pymnts.com/news/artificial-intelligence/2023/walmart-finds-75-percent-vendors-prefer-negotiating-with-chatbot/ ; retaildive.com/news/the-startup-thats-automating-supplier-negotiations-for-walmart/591972 ; talkinglogistics.com/2023/05/01/negotiating-with-a-chatbot-a-walmart-procurement-case-study/ |
| **Keelvar** | Sourcing bots that invite suppliers, run bids and recommend awards. Autonomous Negotiation Agents (protocol-based, not chat). Kai orchestrator (Nov 2025). | **90% of events agent-operated (Jul 2026)**, up from 71% in 2025. Monthly event volume up 16x since 2023. Median event takes ~2 hours. **Supplier-side bidding agents in ~1,420 events/month** since a Dec 2025 launch. **[summary-only; vendor white paper]** | $43M total (Series B $24M) | keelvar.com/documents/the-two-sided-agentic-market-in-enterprise-procurement ; keelvar.com/knowledge-hub/autonomous-negotiation-agents-the-end-of-the-chatbot-era-in-sourcing |
| **Fairmarkit** | Autonomous tail-spend RFQs by email: match suppliers, collect bids, award. Total Agentic Sourcing (Apr 2026) runs from a "$500 purchase to a $500M contract". | Was "on track for 200,000+ sourcing events/yr" (2022). Claims ~10% average savings. | ~$78M total (Series C $35.6M) | businesswire.com/news/home/20260429737522/en/ ; citybiz.co/article/315325/fairmarkit-secures-35-6-million-series-c/ |
| **Lio (askLio)** | "Virtual buyers" that research vendors and negotiate terms | Dozens of Global 2000 customers (Munich Re, Brose, Novozymes). "Billions" of dollars in spend managed. | $30M Series A led by a16z (Mar 2026) | prnewswire.com (20260305EN02303) ; vcaonline.com/news/2026030502/ |
| **Zip** | Price Negotiation Agent (Oct 2025) gives benchmarks and tactics to buyers. Superagents in 2026. | $6B+ in customer savings claimed | Large (not re-checked) | businesswire.com/news/home/20251021882875/en/ |
| **Arkestro** | Predictive procurement: game-theory "anchoring" of supplier quotes | Fortune 500 manufacturers and energy companies; claims 18.8% savings | $36M (May 2025; Altira, Aramco Ventures) | aramcoventures.com/news/arkestro-secures-36m-... |
| **Globality** | Glo 2.0 runs events from intake to award autonomously (Sep 2026) | Customers include BT, Tesco, UPS, HP, Fidelity | $356M total | e-commerce.news/story/globality-launches-autonomous-sourcing-platform-glo-2-0 |
| **Coupa** | 20 Navi agents in production, 65 planned by Jan 2027. Agents for sourcing event creation and bid comparison. | — | Incumbent (Thoma Bravo) | incisiv.com/blog/coupa-goes-all-in-on-agentic-key-takeaways-from-inspire-2026 |
| **SAP Ariba Joule** | Bid Analysis Agent (Q1–Q2 2026). Sourcing event agent. Intake agent GA Jun 2026. These are **analysis and intake, not autonomous counter-negotiation.** | — | Incumbent | sapinsider.org ; resources.rework.com/tools/ai-agents/best-ai-agents-for-procurement-2026 |
| **Amazon (1P vendor)** | "Automated vendor negotiations, margin guardrails", cost-support asks, price-follower stance. Fewer human vendor managers. | Amazon Vendor Negotiation Study: 200+ vendor leaders say talks are tougher **[summary-only]** | — | metricscart.com/insights/podcast/digital-shelf-insider-ep37/ ; kamcity.com |
| **Also** | Lytica Neo (electronics buyers), Vendr "Ruth" (SaaS buyers), project44 freight procurement agent, Duvo.ai / Gain / Relex for retail merchants | — | — | munich-startup.de ; ajot.com ; modernretail.co (22 Jun 2026) |

**Forecasts:**
- Gartner: by 2027, half of companies will use AI for supplier contract negotiations.
- Gartner: by 2028, $15T of B2B spend will be agent-intermediated (digitalcommerce360.com/2025/11/28/...).
- Gartner: 40%+ of agentic AI projects will fail by 2027.
- MIT CTL analysed 280K human vs. AI negotiations in freight procurement: AI was 59% more cost-effective (ctl.mit.edu/news/how-ai-reshaping-supplier-negotiations).

**How many agent negotiations reach a typical mid-size supplier per year?**
- No data exists. This is my **[estimate]**.
- A $50–300M supplier selling to ~10–30 enterprise accounts might see:
  - **1–5 Pactum-style term or price renegotiations a year**. These are annual or contract-renewal driven.
  - **Tens to a few hundred autonomous RFQs a year**, if it sells tactical or MRO categories into Fairmarkit or Keelvar customers. These are mostly <$50K each.
- Strategic, high-value contracts are still negotiated by humans. The vendors say so themselves: "keep human involvement on strategic spend".

**Supplier reaction:**
- Measured sentiment is *positive*: 75–80% prefer the bot, citing their own pace, consistency and no pressure.
- I found **no** Reddit threads or trade-press backlash about Walmart or Pactum bots. The searches came back empty.
- Concern shows up only in advisory blogs (Asian factories disengaging when they find out it was a bot).
- **Pain is not felt as pain.** Suppliers see a 1.5–3% concession on a tail contract as the cost of keeping the business.

---

## 2. Seller-side competitors (searched hard)

| Name | What | Funding | Threat to N |
|---|---|---|---|
| **Keelvar supplier-side bidding agents** | Supplier agents bidding inside Keelvar events since Dec 2025, ~1,420 events/month. Who builds them, and whether they are Keelvar-provided or third-party, is **[unverified]**. | Part of Keelvar | **High.** The buyer's platform designs the mechanism and can host or certify the supplier agent. |
| **Pricefx Agents** | 125+ agents covering floor/target/stretch prices, margin-leak detection and negotiation guidance (with ServiceNow). 26 agent deals in under 6 months. | Private, PE/VC-backed | **High** for "coach the rep" and the deal desk |
| **Zilliant** | Agentic AI plus an MCP server (Q1 2026). Automates customer-specific pricing and negotiated agreements, which can be "up to 80% of revenue" in distribution. | PE-backed | **High.** Already holds the floors and cost-to-serve data. |
| **Vendavo** | AI Deal Desk Agent | PE-backed | High |
| **PROS** | AI agents for quoting and sales | Acquired (Thoma Bravo, 2025) **[unverified]** | Medium–High |
| **Nibble** | AI negotiation agent; "Sales Contracts and Procurement", e-commerce haggling; 1.5M+ negotiations | ~$3.3M seed (2022) | Medium. Can point its agent at the sell side. |
| **Dealops** | AI deal pricing and quoting for revenue teams (SaaS-focused) | $7M (Pear, General Catalyst) | Low–Medium |
| **Titan AI** | B2B "deal copilot" for pricing and negotiation strategy | $215K seed | Low |
| **Genesy** | Autonomous B2B sales agents, "outreach and negotiations" | $5M seed | Low–Medium |
| **Pallet/CoPallet, Transfix, Greenscreens-type tools** | Freight brokers' agents that answer shipper RFPs and spot quotes: "32% more spot quotes won" | Various | High in freight, where M2M is most advanced |
| **Crisp (CPG), Stackline, MerchantSpring, Consulterce** | CPG/Amazon vendor negotiation analytics and advisory | Various | Medium for the retail-vendor wedge |
| **Proton.ai, Endeavor, Mercura, Korso, Lark** (from Phase 5) | Inbound quote and RFQ automation for distributors and manufacturers | $2–10M seeds | Medium. "Answer the RFQ" overlaps. |
| **RFP-response tools (Loopio, Responsive, Inventive)** | Seller-side RFP answering | Large | Low. Not searched this round. **[unverified relevance]** |
| **Pactum** | Pure buy side. Sells only to procurement. | ~$108M | Would block or ignore N rather than serve it |

**Conclusion:** I found no funded startup pitched exactly as "counter-Pactum for suppliers". But the *capability* is being covered from three directions:
1. **Buyer platforms hosting supplier agents** (Keelvar's two-sided market).
2. **Pricing incumbents** (Pricefx, Zilliant, Vendavo, PROS) that already own floors, cost-to-serve and deal desks, and are shipping agents and MCP servers.
3. **Vertical quote agents** in freight and distribution.

The gap is a wedge into a field incumbents are already moving toward, not open whitespace.

---

## 3. Value and market math

**Value at stake per supplier [estimate]:**
- **Walmart-type tail supplier:**
  - Contracts are small (tail; Fairmarkit tail RFQs are mostly <$50K).
  - Assume $1M of revenue renegotiated per year at 1.5–3%, which is **$15–30K** in concessions.
  - Add a 5-day terms extension on $1M at an 8% cost of capital, roughly **$1K**.
  - An agent that defends 25–40% of that recovers **$4–12K/yr**.
  - That cannot carry a $25K+ subscription, and these suppliers are SMBs that are hard to reach.
- **Mid-size industrial or CPG supplier, $100M revenue, ~20% of revenue touched by buyer agents each year:**
  - $20M × 1.5–3% gives **$300–600K** in concessions at stake.
  - Defending 20–30% gives **$60–180K/yr**.
  - Supports an ACV of **$20–50K** plus gain-share. Plausible, but the 20%-touched assumption is unproven.
- **Large supplier ($1B+):**
  - Its strategic contracts with Walmart, Amazon and Honeywell are negotiated by humans and key-account teams.
  - Buyer agents touch only its tail SKUs and sites. Its pricing team already licenses Pricefx, Zilliant or Vendavo.
  - The incremental willingness to pay is a feature inside the existing pricing tool.
- **Exception: Amazon 1P vendors.**
  - Automated cost-support asks and margin-guardrail pressure land on large brands.
  - This is real pain, but it sits in one buyer, in retail ecommerce, and is crowded with analytics firms and consultants.

**Who buys:**
- VP Sales / Key Account Director, who owns the relationship and fears looking adversarial.
- VP Pricing / Revenue Management, who owns floors and already has a pricing vendor.
- CFO, for terms and DSO.
- The champion is fragmented, and the budget sits with the pricing incumbent.

**Account count:**
- I found no public list of suppliers selling >$10M to Pactum, Fairmarkit or Keelvar customers.
- **[estimate]:** Pactum (~50 customers) and the other agentic buyers (~a few hundred enterprises) each have thousands of tail suppliers, but few have >$10M exposure that a bot negotiates.
- Suppliers with >$10M of *agent-negotiated* revenue: probably **low thousands at most in US+EU**. Suppliers with any agent exposure: tens of thousands, mostly SMB.

**ARR math [estimate]:**

| Target | Path | Plausibility |
|---|---|---|
| $10M | 400 suppliers × $25K, or 200 × $50K | Possible by 2029 if agent exposure keeps growing. Requires selling to fragmented mid-market sales orgs. |
| $50M | 1,000 × $50K, or 2,000 × $25K | Requires agent-negotiated revenue to become a large share of mid-size supplier revenue. Pricing incumbents likely bundle before then. |
| $100M | 1,000 × $100K (needs a full revenue-defense platform) | Requires the deal desk and pricing expansion, which means displacing Pricefx, Zilliant and Vendavo. Unlikely. |

---

## 4. Will buyers block supplier agents? Legal and relationship risks

- **Buyers control the mechanism.**
  - Pactum, Keelvar and Fairmarkit design the protocol: chat UI, bid sheets, email RFQs.
  - Keelvar is *already* defining how supplier agents participate, and lists "structural guardrails" and mechanism design as priorities. The buyer platform can whitelist, rate-limit, certify or ban third-party supplier agents.
  - Pactum's value proposition (savings for the buyer) is directly reduced by an effective counter-agent. Expect terms-of-use restrictions or detection.
- **Relationship risk.**
  - Key-account managers at Walmart, Amazon and Honeywell suppliers will not want to be seen "botting back" against a top-5 customer.
  - Survey data says suppliers *like* the current bots. That removes the emotional trigger.
- **Antitrust (the decisive issue for the "network moat"):**
  - **California AB 325 (in force 1 Jan 2026)** amends the Cartwright Act. It targets "common pricing algorithms": any tech "used by two or more persons, that uses competitor data to recommend, align, stabilize, set, or otherwise influence a price or commercial term". It does not matter whether the data is public. It also covers *coercing* adoption of recommended terms. (alston.com/en/insights/publications/2025/11/california-ab-325-antitrust-standards ; sheppard.com/insights/blogs/california-passes-broad-limits-on-common-pricing-algorithms)
  - **DOJ RealPage consent decree (Nov 2025):** training data must be ≥12 months old, and no data narrower than state level. The DOJ treats an algorithm acting as middleman like a human conspirator (hub-and-spoke). (bakermckenzie.com/en/insight/publications/alerts/2025/12/united-states-doj-settles-realpage-case ; wsgr.com)
  - **DOJ/FTC public inquiry on competitor-collaboration guidelines (23 Feb 2026).**
  - **What follows for N:** one vendor negotiating for competing suppliers into the same buyer, using cross-supplier outcome data ("Walmart accepted +2% from others in this category") is close to a hub-and-spoke fact pattern. It would also face sell-side collusion scrutiny, where buyers are the plaintiffs. The product has to silo each supplier's data, which **kills the cross-buyer network moat**. Pooling only *buyer-behaviour* data (how the Pactum bot concedes) is lower risk but still "competitor data influencing a commercial term" under a broad reading of AB 325. Outside counsel is required before any pooling.

---

## 5. 90-day pilot, moat and venture math

**Pilot design (best case):**
- **Target:** 3 suppliers with $100M–1B revenue in packaging, MRO or freight. These are the categories with the most M2M activity per Keelvar. Each must have ≥3 enterprise customers running Keelvar, Fairmarkit, Pactum or Coupa sourcing.
- **Ingest:** price floors, cost-to-serve, terms limits and 24 months of bid history.
- **Run:** shadow mode. Detect and classify inbound agent events (email or portal), draft counteroffers or bids, rep approves.
- **KPIs:** event count (a kill if fewer than 10 events in 90 days), win rate vs. baseline, average price and terms conceded, rep hours saved.
- **Pilot risk:** event frequency. Pactum-style renegotiations are annual, so 90 days may show **0–2** strategic events. Only RFQ-heavy categories produce enough events to prove value.

**Moat:**
- Planned: a cross-buyer negotiation data network. **Legally constrained** (see Section 4).
- Remaining moats: integrations into supplier ERP and pricing systems (which the incumbents already own), and per-supplier policy models (weak).
- Defensibility is low.

---

## 6. Kill signals (ranked)

1. **Buyer agents target tail spend, not material revenue.** Walmart applies Pactum to small contracts with non-merchandise suppliers. Fairmarkit focuses on tail RFQs under $50K. Value at stake per supplier is small.
2. **Concessions are modest.** The pilot got ~1.5% and terms to ~35 days. Phase 5's "+35 days" is likely a misreading.
3. **No felt pain.** 75–83% of suppliers prefer the bot, and I found no backlash online.
4. **The buyer platform owns the two-sided market.** Keelvar launched supplier-side bidding agents (Dec 2025, ~1,420 events/month) and controls the mechanism design.
5. **Pricing incumbents ship negotiation agents.** Pricefx (125+ agents, floor/target/stretch), Zilliant (agentic AI plus MCP), Vendavo (Deal Desk Agent) and PROS already sit on the floors and cost-to-serve data the product needs.
6. **The antitrust law makes the network moat toxic.** CA AB 325, the RealPage decree and the DOJ hub-and-spoke posture all apply.
7. **Low event frequency means slow pilots and weak proof.**
8. **Relationship risk.** Key-account teams will not bot back against top customers.

**Survive signals (what keeps a sliver alive):**
- Agent-operated event volume is exploding (Keelvar at 90%, 16x volume growth).
- M2M bidding is emerging in high-frequency categories: freight, packaging, MRO.
- Amazon's automated vendor asks hit large brands.
- Gartner expects half of companies to use AI negotiation by 2027.

---

## Sharpened thesis (if pursued at all)

> "In high-frequency, formula-priced categories (freight, packaging, MRO consumables), buyer platforms now run 90% of sourcing events by agent, and response time and price precision decide wins. We are the supplier's bid agent: we answer every agent-run RFQ in minutes, within margin floors, across Keelvar, Fairmarkit, Coupa and email, and price each bid on that supplier's own win/loss history. Every supplier's data stays separate."

This is a **bid-response and pricing-execution tool, not a negotiator**. It competes with freight quoting agents, Pricefx and Zilliant, and with Keelvar's native supplier agents.

---

## Cold message and simulated reaction

**Message (to the VP Sales of a $400M packaging converter):**
> "Your top customers now run most sourcing events through AI agents. Keelvar reports 90% of its events are agent-operated, and Pactum negotiates terms for Walmart, Honeywell and Novartis. We deploy a bid agent that answers those events in minutes, never below your margin floor, and shows you what each customer's bot concedes. A 90-day shadow pilot costs nothing. Want to see how many agent events hit you last quarter?"

**Simulated reaction:**
> "Interesting, but I don't know which of our customers use bots. Most RFQs still come through Ariba or by email, and my inside-sales team answers them. Our pricing guardrails live in Pricefx and we're already piloting their agents. I'd take a look at the 'how many agent events' report. I wouldn't let a third-party bot bid on our behalf into P&G or Amcor without legal review."

That is a curious no to the agent, and a weak yes to the analytics.

---

## 5 simulated buyers

| Buyer | Response | Why |
|---|---|---|
| $1.2B industrial distributor, VP Pricing (Zilliant customer) | **NO** | "Zilliant's agents and MCP cover floors. I'll wait for the module." |
| $250M packaging converter, CFO | **MAYBE** | Keen on bid speed and margin floors for RFQs. Wants proof of event volume first. |
| $80M Walmart GNFR equipment supplier, owner | **NO** | "The bot asked for 2% and five days. I said yes to keep the account. I'm not paying $20K a year to fight it." |
| $600M CPG brand, VP Amazon (1P) | **MAYBE** | Real pain from automated cost-support asks. Wants an Amazon-specific tool and already uses consultants and analytics. |
| $150M regional freight broker, COO | **YES (for quoting)** | Answers shipper RFPs and spot bids. But CoPallet and Transfix-style tools already compete. |

Tally: 1 YES (in a crowded vertical), 2 MAYBE, 2 NO.

---

## Scores (1–10)

| Dimension | Score | Rationale |
|---|---|---|
| Pain | 3 | Suppliers prefer the bots. Concessions are small and on tail contracts. |
| Urgency | 3 | No felt crisis. Strategic contracts are still human-negotiated. |
| ROI clarity | 5 | Measurable in bps and days, but small absolute dollars per supplier. |
| Customer accessibility | 4 | Fragmented champions (sales, pricing, CFO). Suppliers don't know which buyers use agents. |
| Pilot speed | 4 | Integration is easy, but event frequency is low. Pactum renegotiations are annual. |
| Market size | 4 | Low-thousands of suppliers with material agent exposure. A $10–50M ARR ceiling for now [estimate]. |
| Expansion | 5 | A deal desk and revenue-defense expansion runs into Pricefx, Zilliant, Vendavo and PROS. |
| Venture potential | 4 | Depends on agent-negotiated share reaching core revenue. That is a 2028+ bet. |
| Defensibility | 2 | The network moat is constrained by antitrust. Buyer platforms control the mechanism. Incumbents own the pricing data. |
| Why now | 7 | Agentic sourcing volume is exploding (Keelvar 90%, Pactum 489%, Lio $30M, Fairmarkit TAS). |
| Competition position | 3 | Squeezed between buyer platforms hosting supplier agents and pricing incumbents shipping agents. |

**Average ≈ 4.0**

## VERDICT: **KILL** (as stated)

- **Why it dies:**
  - The buyer agents are pointed at suppliers' least valuable revenue.
  - Suppliers report liking them.
  - The counterpart agent is already appearing inside buyer platforms (Keelvar) and pricing suites (Pricefx, Zilliant, Vendavo).
  - The only real moat, cross-supplier negotiation data, sits on top of the law California put in force in January 2026.
- **Narrow reframes worth one cheap test each (not as a venture thesis yet):**
  1. **Supplier bid agent for high-frequency M2M categories** (freight, packaging, MRO), with data kept separate per supplier. Test: get the exact M2M volume from Keelvar's white paper and find out who builds those supplier agents.
  2. **Amazon 1P "automated-ask defense"** for $100M+ brands. Test: 5 interviews with the brands in the Consulterce study.
- **Re-open the thesis if** Pactum or Walmart extend autonomous negotiation to *goods-for-resale and strategic* suppliers, or if a buyer platform publishes an open supplier-agent protocol that third parties can plug into.

---

## Sources (as found; mostly search summaries)

- siliconangle.com/2025/06/09/pactum-raises-54m-procurement-automation-platform/ ; procurementmag.com/news/pactum-secures-series-c-funding-to-drive-agentic-ai-adoption ; procurementmag.com/news/pactum-transforms-procurement-with-its-agentic-ai-platform ; samsearch.co/government-contracting-news/pactum-utilizes-ai-agents-to-revolutionize-supplier-negotiations-for-major-corporations-120405
- pymnts.com/news/artificial-intelligence/2023/walmart-finds-75-percent-vendors-prefer-negotiating-with-chatbot/ ; retaildive.com/news/the-startup-thats-automating-supplier-negotiations-for-walmart/591972 ; talkinglogistics.com/2023/05/01/negotiating-with-a-chatbot-a-walmart-procurement-case-study/ ; modernretail.co/technology/ai-is-now-doing-parts-of-merchants-jobs-managing-products-and-vendors/
- keelvar.com/documents/the-two-sided-agentic-market-in-enterprise-procurement ; keelvar.com/knowledge-hub/autonomous-negotiation-agents-the-end-of-the-chatbot-era-in-sourcing ; businesswire.com/news/home/20251112367315/en/ (Keelvar Kai)
- businesswire.com/news/home/20260429737522/en/ (Fairmarkit TAS) ; citybiz.co/article/315325/fairmarkit-secures-35-6-million-series-c/
- prnewswire.com (Lio $30M, 2026-03-05) ; businesswire.com/news/home/20251021882875/en/ (Zip) ; aramcoventures.com (Arkestro $36M) ; e-commerce.news/story/globality-launches-autonomous-sourcing-platform-glo-2-0 ; incisiv.com/blog/coupa-goes-all-in-on-agentic-key-takeaways-from-inspire-2026
- digitalcommerce360.com/2025/11/28/gartner-ai-agents-15-trillion-in-b2b-purchases-by-2028/ ; ctl.mit.edu/news/how-ai-reshaping-supplier-negotiations
- metricscart.com/insights/podcast/digital-shelf-insider-ep37/ ; kamcity.com (Amazon vendor negotiation)
- pricefx.com/content/news/pricefx-2026-record-momentum-ai-adoption ; pricefx.com/content/news/pricefx-integrates-servicenow ; businesswire.com/news/home/20251009250891/en (Zilliant agentic + MCP) ; vendavo.com (Deal Desk Agent)
- vcaonline.com/news/2025081206/dealops-raises-7-million-to-power-pricing-in-the-ai-era/ ; trysignalbase.com/news/funding/titan-ai-secures-215k-seed ; vcbacked.co/company/nibble-technology ; cortinovis.de (Genesy $5M) ; pallet.com/use-cases/quoting
- alston.com/en/insights/publications/2025/11/california-ab-325-antitrust-standards ; sheppard.com/insights/blogs/california-passes-broad-limits-on-common-pricing-algorithms ; bakermckenzie.com/en/insight/publications/alerts/2025/12/united-states-doj-settles-realpage-case ; jdsupra.com (AI Antitrust Issues Checklist, June 2026)
