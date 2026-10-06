# F1 — "AI should make your vendors cheaper. We make sure it does."
Merged thesis #1 (build-replaces-buy) + #15 (AI-deflation audit of services contracts). Round 18 deep dive, 2026-10-06. 39 web searches; WebFetch was blocked on most sources (hfsresearch, informationweek, brightfield, gartner), so most facts come from search-result snippets and are marked where unverified.

## Verdict: **KILL** (avg 6.0; Competition position 3, Pilot speed 4, Defensibility 4)
**Cause of death: F2 visible-pain race plus a variant of F1 (absorption by existing advisors).** The behavior is real and speeding up. The services half is one of the best-documented money flows we have looked at. But it is fully public: Reuters, Gartner, IDC, HFS, ISG, UpperEdge and Brightfield have all written about it, and incumbent advisors already sell it on contingency. The SaaS half is owned by Vertice+Vendr, Tropic and Zylo on renewals, and by Retool, Superblocks and Lovable on rebuilds. What is left is a consulting business (lumpy, one deal per contract cycle), not a venture-scale system of record. One narrow residual idea (customer-owned delivery telemetry used to verify productivity-sharing clauses) is noted at the end. It is not a finalist.

---

## 1. Is the behavior real and accelerating?

### (b) Services / BPO deflation: YES, strongly, and in the last 60 days
| Evidence | Date | Source (as found; content mostly via search snippets) |
|---|---|---|
| Global clients demand discounts of up to 30% (some up to 40%) on existing IT contracts. About 20-30% of current contracts reopened for renegotiation. 40-50% of new 2025 outsourcing deals include AI pass-through clauses. Persistent CEO: clients want the same work for 25-30% less | Aug 20-21, 2026 (Reuters, syndicated) | https://www.thestar.com.my/tech/tech-news/2026/08/21/ai-reshapes-india039s-it-services-sector-contracts-as-clients-demand-more-for-less ; https://whbl.com/2026/08/20/ai-reshapes-indias-it-services-sector-contracts-as-clients-demand-more-for-less/ |
| TCS: about 80% of contracts in its finance/HR/business-services segment are now outcome-based, double the share since late 2023. TCS CEO put pricing savings passed to clients in a "10-15% range". Cognizant–Daimler Truck deal splits AI savings. Cognizant AI-infused rate cards ("digital labour") | Aug 2026 | same Reuters piece; https://www.peoplematters.in/news/ai-and-emerging-tech/cognizant-starts-charging-for-ai-alongside-human-work-in-new-pricing-model-49484 |
| HFS: corporates now reopen IT services contracts **within 24 months** instead of waiting for renewal. Contracts with ACV over $50M face the most pressure. "Shadow AI gains" (the provider uses AI and does not pass it on). ISG/HFS's Phil Fersht: shift from FTEs/rate cards to productivity commitments and gain-share | 2026 (exact date unverified, fetch blocked) | https://www.hfsresearch.com/news/ai-drives-it-contract-renegotiations-within-24-months-as-pricing-models-shift/ |
| Gartner (via ARN/Reseller NZ): **60% of large IT services contracts will include AI clawback clauses by 2027** | 2026 (date unverified) | https://www.arnnet.com.au/?p=4102083 (snippet) |
| Accenture Q4 FY26: revenue $18.7B (+6%). Snippets report that prices were "lower in many areas" because clients expect to share in AI savings | late Sep 2026 | https://newsroom.accenture.com/content/4q-full-fy26-earnings/accenture-reports-fourth-quarter-and-full-year-fiscal-2026-results.pdf ; https://www.resultsense.com/news/2026-10-02-accenture-forecast-it-services-rally/ (pricing quote not verified against transcript) |
| Kotak: 3-3.5% annual revenue deflation for Indian IT through FY2028-29. HCLTech: about 25-30% more effort needed for the same revenue. Infosys tracks "AI-led deflation" internally but does not disclose it | 2026 | https://www.tribuneindia.com/news/business/it-services-growth-to-stay-range-bound-at-3-per-cent-as-ai-deflation-pressures-margins-mid-tiers-better-placed-says-kotak/ ; https://www.wrightresearch.in/blog/what-happens-to-indian-it-when-ai-reprices-its-core-business/ |
| Google cut its HCLTech engineering contract by about $50M a year (of about $200M) as part of AI/automation consolidation | 2026 (exact date unverified) | https://www.peoplematters.in/news/business/google-cuts-hcltech-contract-by-dollar50-million-as-ai-reshapes-it-outsourcing-51220 |
| Concentrix Q3 (Sep 29, 2026): faster-than-expected client AI automation is compressing revenue. Two hyperscaler clients are dropping support for some customer sets. Earlier in 2026, clients renegotiated pricing and cut volumes to fund their own AI | Sep 29, 2026 | https://www.marketbeat.com/instant-alerts/transcript-concentrix-q3-earnings-call-highlights-2026-09-29/ ; https://www.briefing.com/story-stocks/archive/2026/6/30/concentrix-tumbles-as-client-cost-pressures-drive-guidance-reset-(cnxc) |
| Consultants "head for a showdown with their own clients" as AI upends pricing | Aug 31, 2026 | https://www.irishtimes.com/business/2026/08/31/consultants-head-for-a-showdown-with-their-own-clients/ (not read) |
| ISG Q2 2026: managed services ACV $10.9B, only +2.7% YoY. AI sentiment is negative for labor-based managed services | Jul 2026 | https://www.marketbeat.com/instant-alerts/information-services-group-sees-ai-cloud-demand-fuel-record-tech-spending-2026-07-10/ |

**Read:** this is a large, real money flow. Large customers are already capturing AI deflation of 10-30%. **The problem is who captures it:** procurement teams plus incumbent advisors at renewal and mid-term reopeners, with vendors pre-emptively offering 10-15% and outcome pricing. The "unclaimed gap" a startup would recover shrinks every quarter as vendors re-price on their own to protect accounts.

### (a) Build-replaces-buy: REAL but overstated; evidence is mostly vendor-funded
- Retool 2026 Build vs Buy report (n=817): 35% have replaced at least one SaaS tool with custom software; 78% plan to build more; workflow automation (35%) and internal admin (33%) lead. **Vendor survey with an obvious bias.** https://www.businesswire.com/news/home/20260217548274/en/Retools-2026-Build-vs.-Buy-Report-Reveals-35-of-Enterprises-Have-Already-Replaced-SaaS-With-Custom-Software
- "McKinsey 2026: 32% abandoned at least one software purchase because coding agents can replicate it." Found only on a secondary site, **unverified**: https://winzheng.com/en/article/mckinsey-ai-coding-agents-build-vs-buy-32-percent-2026
- Gartner (via CFOtech/IT Brief): $234B of enterprise application spend at risk from agentic AI. About 20% of enterprise app SaaS spend is exposed by 2030. Seat-based share of contracts fell from 21% to 15% in 12 months (snippet). https://cfotech.news/story/gartner-warns-agentic-ai-threatens-234bn-saas-spend
- **Klarna is a weak anchor:** CX Today reports that Klarna replaced Salesforce/Workday mostly with *other SaaS* (Deel etc.) plus a Neo4j graph layer, not purely with in-house AI. https://www.cxtoday.com/?p=65960
- Zylo SMI 2026 (Jan 29): AI-native app spend +108% overall and +393% at companies over 10K employees. Sep 23, 2026 update: AI-native spend +334% YoY. **SaaS budgets are being re-allocated to AI, not deflated.** https://zylo.com/news/2026-saas-management-index ; https://zylo.com/news/ai-native-software-spend-surges
- SaaS stocks: Monday.com about -44%, HubSpot about -51% peak-to-trough in 2026 on "build-it-yourself" fear (Saxo, Aug 7, 2026). Atlassian counter-signal: Rovo customers expand ARR at 2x. https://www.home.saxo/content/articles/equities/saas-disruption-07082026
- Weak signals: individual devs cancelling SaaS after a 2-hour Claude Code rebuild (HackerNoon, €360/yr Cal.com). This happens at tail-spend scale, not enterprise core systems.

**Read:** long-tail SaaS replacement is real, but the dollar value per customer is small (admin tools, forms, simple CRM). The large lines (Salesforce, Workday, ServiceNow, SAP) are not being rebuilt; vendors are re-pricing to agent/outcome models instead. "Rebuild and run it for you" is an AI-native MSP (services margins) up against Retool, Superblocks ("in a single prompt, replace million-dollar SaaS" with AWS) and Lovable/Replit enterprise.

## 2. Competitors
| Layer | Players | Status |
|---|---|---|
| Services sourcing advisors (direct for (b)) | **ISG** (publicly touting AI-driven sourcing deals: $130M/20% savings for a US hospital network; $15M/yr for a media co), **UpperEdge** (running a content series: "Q1 2026 MSP earnings signal… why enterprises risk overpaying in the AI era"), **IDC Sourcing Advisory** (Jul 31, 2026: "The 90-Day IT Contract Audit… before your MSP arrives", plus "AI is making MSPs more efficient, here's how to share in the gains"), Everest Group, HFS, Gartner, Hackett, Info-Tech, KPMG/Deloitte/EY sourcing advisory, Implement Consulting ("contracting for AI impact"), law firms (Morgan Lewis, Dickinson Wright quoted by InformationWeek) | Already selling it, some on **25% of savings contingency** (snippet, redresscompliance) |
| Services/SOW spend analytics | **Brightfield** (content series "The Robot Surplus: Why AI productivity gains may not be showing up in your contracts", "The AI Dividend: four ways procurement is re-defining services", masterclass "AI Unplugged: the new economics of SOW"), SAP Fieldglass, Coupa services procurement, Beeline, Genpact SOW AI | Owns SOW data at large enterprises |
| AI contract intelligence | **Infinity Loop** ($5M seed, Glasswing/TIAA, Aug 2025; claims ≥12% savings, $19.5M in 5 months for one client) | Funded, same pitch |
| SaaS renewal / negotiation | **Vertice acquired Vendr** (Jun 2026; $75B spend, 32K vendors; AI negotiator "Ana", Vendr's "Ruth"), Tropic (5 AI procurement agents), Zylo ($100B+ processed), Spendflo, Cledara | Category consolidated; AI negotiators shipped |
| Build/replace | Retool, Superblocks 3.0 (AWS), Lovable, Replit, Bolt, plus IT services firms themselves | Platforms pitch "replace SaaS" directly |
| Procurement AI | Zip ($2.2B), Pactum ($54M C, autonomous negotiation), Fairmarkit, Arkestro, Levelpath, Didero | Adjacent; could add a "services AI-deflation" module |
| The vendors themselves | TCS/Cognizant/Accenture offer outcome pricing and gain-share **pre-emptively** | Reduces the recoverable gap (destination-subsidy dynamic, F6-like) |

No startup was found whose sole wedge is "AI-deflation audit of IT/BPO services contracts". But the function is already performed by advisors who have the relationships, benchmarks and contingency pricing. Per taxonomy rule §4.2, the pain has 3+ public write-ups and paid providers.

## 3. Conflict of interest: does it protect us?
- **The vendor being paid is conflicted.** True: Infosys won't disclose its deflation rate, and "shadow AI gains" exist. But the vendor is not the competitor. The competitor is the **advisor**, and advisors are not conflicted on the buy side. (Partial exception: ISG/Everest/Gartner also sell research and ratings to providers. That is a soft conflict buyers already tolerate.)
- **Can advisors do it?** Yes, and they already are. The only thing they lack is *continuous, data-driven measurement* of vendor effort. They work from benchmarks and rate cards, not from telemetry.
- **SaaS side:** Vertice/Vendr already sit in the renewal. Rebuild platforms (Retool/Superblocks) are not conflicted; they *want* the SaaS replaced.

## 4. Buyer counts and $10M / $100M ARR math
- Buyers: companies with ≥$20M/yr in IT/BPO outsourcing. Roughly 3,000-5,000 globally (estimate, not sourced). HFS says pressure concentrates on contracts with ACV over $50M, i.e. Global 2000 (~2,000 firms).
- Savings-share economics: a $50M/yr contract with 8% recovered deflation = $4M/yr. At 20-25% of year-1 savings, that is a fee of about $0.8-1.0M **once per contract cycle**. Recurring subscription for monitoring: maybe $100-250K/yr.
- **$10M ARR:** about 15 contingency wins a year plus 20 monitoring subscriptions. Feasible as a boutique.
- **$100M ARR:** about 150 large-contract wins a year, *every year*, against ISG/UpperEdge/Big-4, with 6-12-month enterprise sales and reopen cycles. The whole public sourcing-advisory leader (ISG) is a roughly $250M-revenue company (approximate, unverified), which suggests this is a services-multiple ceiling, not a $10B outcome.
- Fails taxonomy rule §4.6: the money arrives as one-time renegotiation events. The deflation also shrinks over time as vendors re-price on their own (Kotak: 3-3.5%/yr). Once contracts are outcome-priced, the arbitrage disappears.

## 5. Weak signals
- Counted as weak/early: "we cut SaaS by building internally" exists only anecdotally (HackerNoon) and in vendor surveys. No mid-market CFO-side posts found quantifying it. Reddit is blocked; nothing found on HN.
- "Asked our outsourcer for AI savings": not weak at all. It is in Reuters, Gartner and IDC (the signal has already crossed into the mainstream).
- Real gap noticed: the **customer owns the systems vendors work in** (ServiceNow tickets, Jira, GitHub/GitLab, contact-center platforms). Throughput per billed FTE, AI-assisted commit share and ticket deflection could be measured continuously from customer-owned data, without vendor cooperation. Advisors don't do this today; they use rate-card benchmarks. This is the only non-obvious piece (see residual).

---

## Finalist format

- **One-line problem:** Outsourcers and SaaS vendors are capturing AI productivity gains as margin while customers keep paying per FTE/seat.
- **Why now:** 2025-26 agentic delivery cut provider effort 20-50% (provider claims). Clients are reopening 20-30% of contracts. Gartner forecasts 60% of large contracts with AI clawbacks by 2027.
- **Exact buyer:** CPO / Head of IT Sourcing & Vendor Management (with CFO sponsorship).
- **Exact ICP:** Enterprises spending ≥$20M/yr on T&M/FTE-priced IT, application maintenance, service desk or CX BPO contracts, with a renewal or reopener within 12 months.
- **Current workaround:** Hire ISG/UpperEdge/IDC/Everest/Big-4 sourcing advisory (fixed fee or ~25% contingency). Accept the vendor's pre-emptive 10-15% / outcome-pricing offer. Vertice/Vendr/Tropic for SaaS renewals. Retool/Superblocks/Lovable for rebuilds.
- **Why incumbents cannot easily own it:** They mostly can. The provider is conflicted, but advisors are not, and advisors already sell it. The only thing they lack is telemetry-based continuous measurement, which is feature-sized.
- **30-day MVP:** Connectors to ServiceNow/Jira/GitHub/contact-center platforms that compute "effort per unit of output" trends for each vendor team against billed FTEs and invoices, producing a "deflation owed" estimate plus negotiation brief.
- **Pilot design:** 2 enterprises with an upcoming reopener. Back-test 24 months of tickets/commits against invoices. Success = a quantified gap of ≥8% that the customer uses in negotiation, with a contingency fee on signed savings.
- **Pricing hypothesis:** 20% of first-year verified savings + $100-250K/yr continuous clause verification.
- **Expansion path:** SaaS renewals → services → all labor-priced vendors (agencies, legal, audit). Become the measurement layer for AI clawback/gain-share clauses.
- **Moat:** Cross-customer benchmark of AI-era effort per output by vendor and tower. Weak: advisors already hold larger benchmark datasets, and vendors can obscure work across systems.
- **Why it could be $10B+:** Only if it becomes the system of record that clawback and outcome contracts settle against (a "Nielsen for AI-era labor output"). No evidence buyers or vendors would standardize on a third party for that, and T2 (auditor of outcome-priced AI work) was killed at 4.7.
- **Direct competitors / adjacent threats:** ISG, UpperEdge, IDC Sourcing, Everest, Hackett, Big-4 sourcing, Brightfield, Infinity Loop, Vertice+Vendr, Tropic, Zylo, Zip, Pactum, Coupa/SAP Fieldglass, Retool/Superblocks/Lovable, and the providers' own outcome-pricing offers.
- **One sentence to a CFO:** "We measure from your own ServiceNow, Jira and GitHub how much less work your outsourcers do since they adopted AI, and get that difference back on your invoice. We are paid only from what we recover."
- **5 discovery questions:**
  1. In the last 12 months, did you reopen any services contract over AI productivity? Who ran it (internal team or advisor), and what % did you get?
  2. How did you quantify the gap? Did the vendor accept your number?
  3. Do your vendors work inside your own ticketing/repo systems, and does procurement have access to that data?
  4. Would you pay contingency for a second pass on a contract an advisor already renegotiated?
  5. Do your new contracts have AI clawback/gain-share clauses, and how will you verify them every quarter?
- **Hard kill criteria:** (a) In 10 interviews, ≥6 already used an advisor or accepted a vendor's pre-emptive offer and see no remaining gap. (b) Vendor work is not visible in customer systems for ≥50% of spend. (c) No buyer will grant ticket/repo data access within 14 days. (d) Recovered gap is under 5% after the vendor's voluntary concessions.

## Scores (1-10)
| Pain | Urgency | ROI clarity | Customer accessibility | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 8 | 7 | 5 | 4 | 7 | 6 | 5 | 4 | 9 | 3 | **6.0** |

Bar: avg ≥8.5 with none below 7. Five categories fall below 7. **KILL.**

### Residual (not a finalist; for the founders only if one has enterprise sourcing access)
"Clause verification from customer-owned delivery telemetry": with Gartner forecasting AI clawback clauses in 60% of large contracts by 2027, those clauses need a quarterly measurement that neither vendor nor advisor produces today. 14-day test: get 2 enterprises with existing gain-share/AI clauses to export 12 months of ServiceNow/Jira data for one vendor. Pass = a measurable effort-per-output decline of ≥15% not reflected in invoices, plus one signed contingency pilot. Expected ceiling without the system-of-record outcome: about $20-50M ARR (F4).
