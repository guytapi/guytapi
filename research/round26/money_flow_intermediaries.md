# Round 26: Follow the money (new intermediaries in AI-driven B2B money flows)

Date: 2026-10-06. Lens: B2B money flows growing ≥3x from 2024 to 2027 because of AI. For each flow: which intermediary function (clearing, settlement, escrow, reconciliation, pricing, underwriting, verification, matching, compliance) is new or still done by hand, and is anyone funded doing it? Excluded (killed in STATUS.md): GPU residual value, compute exchanges, AI spend control, data-licensing brokers, expert-data verification, stranded electrical gear.

Method: 33 web searches (WebFetch blocked for most domains, so figures come from search snippets unless noted). URLs below are the ones the searches returned. Figures marked **[snippet]** were not read in the full source. Estimates marked **[est.]** are my own arithmetic.

**Bottom line: no A. One weak B, which is the only intermediary gap I found that has a large, verified, new money flow and no funded software or startup intermediary: utility collateral for large loads (data-center "credit support").** The capital side of that gap is already being filled by banks, sureties and specialist funds. What is left is the analytics and lifecycle layer, which may be too small for a venture-scale company. Everything else maps to a crowded, platform-owned or already-killed category.

---

## 1. Flow × intermediary table

| # | Flow | Size / growth (source) | Intermediary function examined | Current workaround | Competitors / incumbents | Verdict |
|---|---|---|---|---|---|---|
| 1 | Hyperscaler AI capex | ~$600-785B in 2026, approaching ~$1T in 2027 (Moody's via [DCD](https://datacenterdynamics.com/en/news/moodys-hyperscaler-capex-forecasts-marked-up-by-85bn-to-close-in-on-1trn-by-2027/), [DCK](https://www.datacenterknowledge.com/hyperscalers/hyperscaler-capex-snowballs-toward-700b-as-firms-stage-ai-capacity-builds)) [snippet] | Construction-draw verification for lenders | Independent engineers, lender site visits | Built, Rabbet, Procore (from memory, **not re-verified this round**) | KILL: construction fintech is already established; hyperscalers self-fund |
| 2 | Data-center construction spend | $81.5B YTD through June 2026, >3x full-year 2024 ([ConstructConnect](https://news.constructconnect.com/august-2026-data-center-report-construction-starts-total-22.3-billion-second-highest-on-record)); ~75 projects (~$130B) delayed in Q1 [snippet] | Subcontractor prequalification, payment and lien risk | GC prequal teams, surety bonds | Highwire, Billd, Procore Pay (**unverified this round**); surety brokers ([Grit](https://gritinsurance.com/blog/data-center-construction-boom-contractor-bonding)) | KILL: crowded construction-payments category, not specific to AI |
| 3 | **Utility collateral for large loads (credit support)** | From ~0 to tens of $B in 2 years: Switch $2.6B syndicated performance LC, "first of its kind" ([Switch](https://switch.com/switch-secures-landmark-2-6-billion-syndicated-letter-of-credit-facility-setting-a-new-standard-for-data-center-power-infrastructure/)); QTS seeking ~$2B ([Bloomberg Law](https://news.bloomberglaw.com/artificial-intelligence/blackstones-qts-asks-banks-for-2-billion-to-guarantee-ai-power)); Oracle >$7B collateral, LC fees "could easily exceed $100M/yr" ([DCK](https://www.datacenterknowledge.com/regulations/oracle-lawsuit-tests-wisconsin-ai-data-center-credit-rules), [GTR](https://www.gtreview.com/news/americas/oracle-battles-us-state-authorities-over-data-centre-lc-rules/)); 36+ utilities with large-load tariffs ([Varnum](https://www.varnumlaw.com/insights/mpsc-approves-consumers-energy-tariff-for-large-data-centers/)) | Collateral **sizing/benchmarking, sourcing (LC vs surety vs cash vs guarantee), step-down/release tracking**, and cross-utility credit assessment | Developer treasury spreadsheets; bank syndicates; surety brokers; E3-style consultants; utility credit teams; outside counsel | Banks (Natixis-led syndicate); Marsh / WTW / Aon bank-fronted surety ([Marsh](https://www.marsh.com/en/services/surety/insights/the-role-of-surety-development-operations-of-data-center.html), [WTW](https://www.wtwco.com/en-us/insights/2025/06/surety-bonds-for-data-center-development)); Great Bay Renewables interconnection LCs ([NACE](https://www.nacleanenergy.com/alternative-energies/sol-systems-secures-80-million-from-great-bay-renewables-to-power-its-development-pipeline)); $95M Dynamix Texas queue-collateral fund ([AIN](https://angelinvestorsnetwork.com/alternative-investments/dynamix-texas-data-center-power-fund)) [snippet]; E3 "Credit Efficiency Index" whitepaper ([E3](https://www.ethree.com/data-center-credit-collateral-whitepaper/)); Crux (adjacent, debt + tax credits) | **SURVIVOR → weak B** (Section 2) |
| 4 | Speculative / duplicate large-load requests ("phantom load") | 195 GW of large load with signed construction or supply agreements; 331 GW disclosed ([WoodMac](https://www.woodmac.com/press-releases/us-data-centre-developers-shift-focus-to-existing-pipelines-as-new-capacity-additions-slow-in-q1-2026/)); 60% of surveyed utilities have received ≥500 MW requests while none serves >500 MW ([E3](https://www.ethree.com/data-center-credit-collateral-whitepaper/)) [snippet] | Cross-utility registry and dedupe of requests; verifying request readiness | Self-disclosure (Texas SB6), consultant load forecasts | ERCOT/PJM can do it in-house; GridCARE $64M ([SiliconANGLE](https://siliconangle.com/2026/05/15/gridcare-raises-64m-speed-ai-data-center-projects/)) and Verse $54M are adjacent | KILL (finalist 2, Section 3): ISOs absorb it (F1); utilities are a slow buyer (F4) |
| 5 | GPU-backed debt | >$400B in AI-related debt raised in 2026; CoreWeave $8.5B GPU loan; Lambda $926M TLB ([Bloomberg Law](https://news.bloomberglaw.com/capital-markets/coreweave-raises-8-5-billion-gpu-loan-backed-by-meta-deal), [pulse2](https://pulse2.com/lambda-secures-926-million-gpu-term-loan-with-baa2-investment-grade-rating/)) [snippet] | Borrowing-base and collateral monitoring; delivered-output vs offtake reconciliation | Agent banks, data rooms, independent engineers | Hydra Host lender dashboard ([Hydra](https://hydrahost.com/post/lender-dashboard-gpu-asset-visibility/)), Silicon Data, American Compute ([amcompute](https://www.amcompute.com/gpu-loans)) | KILL: next to the killed GPU-residual category, and already served |
| 6 | Neocloud tenant credit in data-center leases | Hyperscaler guarantees and credit wrappers are now standard ([Bisnow](https://www.bisnow.com/news/national/data-center-capital-markets/neoclouds-rewriting-rules-data-center-financing-135570)) | Tenant credit rating / credit enhancement | Rating agencies, hyperscaler guarantees ("guarantee-for-equity") | Moody's/S&P/Fitch/KBRA; hyperscalers | KILL: ~20-40 tenants (F4); the guarantor is the hyperscaler |
| 7 | Enterprise genAI spend (apps + APIs) | $11.5B (2024) → $37B (2025), 3.2x (Menlo via [letsdatascience](https://letsdatascience.com/news/enterprises-increase-ai-spending-to-37bn-6d854973)) [snippet] | Usage reconciliation, benchmarking, chargeback | FinOps, procurement | Ramp, Vantage, native caps | KILL: AI spend control was already killed (B) |
| 8 | Usage-based AI agent billing between companies (marketplaces) | AWS agent marketplace (launch-date reporting conflicts: [TechCrunch 2025](https://techcrunch.com/2025/07/10/aws-is-launching-an-ai-agent-marketplace-next-week-with-anthropic-as-a-partner) vs 2026 secondary sources) | Settlement and revenue-share clearing | The marketplace settles it | AWS/Azure/Salesforce marketplaces, Stripe/Metronome | KILL: the platform clears it (F1) |
| 9 | Expert-data labor | Mercor >$2B gross run rate (Jun 2026); 30K+ experts ([Dealroom](https://dealroom.co/news/137121-mercor-doubles-to-2b-gross-revenue-run-rate-as-ai-labs-buy-expert-data/)) [snippet] | Global contractor payouts, classification, tax compliance | Done in-house by the platforms + EOR vendors | Deel, Remote; the platforms themselves | KILL: platforms own payroll; next to the killed expert-data verification category |
| 10 | AI services / FDE | Accenture advanced-AI bookings $2.2B/quarter, consensus ~$9.3B for FY26 ([FourWeekMBA](https://fourweekmba.com/ai-accenture-genai-bookings-2-billion-quarter-2026/)) [snippet] | Outcome verification, rate benchmarking | Sourcing advisors (ISG, UpperEdge) | Already killed (T2, round-18 deflation capture) | KILL |
| 11 | Robotics hardware / RaaS | Bank asset finance appearing (FENKA €3M, Jul 2026) ([Seedtable](https://seedtable.com/companies/fenka-robotics/funding-rounds/debt-2026-07)); RobotCare humanoid underwriting framework ([automate.org](https://www.automate.org/companies/robotcare-llc)) | Residual-value underwriting, fleet lease servicing | Equipment lessors, OEM captives | Leasing cos, OEM captives | KILL: pre-demand (F3); residual underwriting resembles the killed GPU thesis |
| 12 | Data-center electricity / on-site gas | 130 projects plan on-site generation (~186 GW); utility supply to data centers 82.9 GW in 2026 → 183 GW in 2030 ([Enverus](https://www.enverus.com/newsroom/off-the-grid-on-the-gas/), [S&P](https://www.spglobal.com/energy/en/news-research/latest-news/natural-gas/052726-pipeline-operators-strike-deals-as-data-centers-turn-to-colocated-generation)) [snippet] | PPA / fuel-supply settlement, tolling, flexibility | IPPs, midstream, utilities, energy desks | LevelTen, Enverus, Emerald AI, Verse, GridCARE | KILL: crowded, and energy trading/settlement is mature |
| 13 | Data-center sales-tax exemptions (repeals) | VA ~$1.6B/yr, GA ~$2.5B, OH $1.6B; OH repealed, IL/AZ paused ([TechRadar](https://techradar.com/pro/torrent-of-states-repeal-data-center-tax-exemptions-but-it-could-increase-costs-by-upwards-of-7-percent)) [snippet] | Eligibility, grandfathering and server-refresh exemption compliance | Big 4 SALT practices, Vertex/Avalara | Big 4, tax engines | KILL: F4 (a few hundred buyers); one-time grandfathering work |

**Pattern.** The fastest-growing AI flows (capex, debt, power) already have deep, well-paid incumbent intermediaries (banks, sureties, brokers, rating agencies, Big 4, ISOs). Software-layer flows (genAI spend, agent marketplaces) are cleared by the platforms. The one function that is **new** is utility credit support: it barely existed in 2024 and is now a multi-$B LC/surety market. Even there, capital providers arrived within about 12 months.

---

## 2. Finalist 1: Large-load collateral desk (weak B)

**One-line problem.** Data-center developers must post billions in utility collateral (LCs, surety, cash) under 36+ different large-load tariffs. Nobody prices, optimizes or tracks the release of that collateral systematically, so developers over-post and overpay. Oracle alone faced >$7B and >$100M/yr in LC fees.

**Why now.** Large-load tariffs went live in 2025-26: Dominion at $1.5M/MW (developers asked for $450K/MW), with automatic enrollment from Jan 1 2027 ([DCD](https://www.datacenterdynamics.com/en/news/dominion-proposes-new-rate-class-for-data-centers-in-virginia/)). Wisconsin PSC set an A-/A3 threshold in Apr 2026. Oracle sued, then dropped the suit in Aug 2026 after S&P cut it to BBB- ([WPR](https://www.wpr.org/news/oracle-drops-wisconsin-suit-financial-requirements-data-centers)). The PA model tariff (May 2026) and Texas SB6 add milestone-based step-downs and refunds ([K&L Gates](https://www.klgates.com/thought-leadership/Pennsylvania-Public-Utility-Commission-Adopts-Model-Interconnection-Tariff-for-Large-Load-Customers-5-29-2026)). The first syndicated performance LC (Switch, $2.6B) closed in Apr 2026. Rough outstanding exposure **[est.]**: 195 GW signed × ~$0.3-1.5M/MW × ~30-60% not covered by rating exemptions ≈ $20-150B. At 50-150 bps, that implies a $0.1-2B/yr fee pool, most of which goes to banks.

**Exact buyer.** CFO / treasurer / head of capital markets at a data-center developer or neocloud. Secondary: credit/treasury at mid-size utilities, co-ops and munis that receive large-load requests but have no credit desk.

**Exact ICP.** Sub-A-rated, US-focused developers and neoclouds with ≥3 sites in ≥2 utility territories and ≥300 MW contracted: PE-backed developers (QTS, Vantage, Aligned, Stack, EdgeCore, CyrusOne), bitcoin miners converting to AI (IREN, Core Scientific, Cipher, TeraWulf, Hut 8), and neoclouds. Roughly 80-200 firms **[est.]**.

**Current workaround.** Treasury spreadsheets; relationship banks syndicate LCs (Natixis); brokers place bank-fronted surety (Marsh/WTW/Aon/Horton); consultants (E3) argue tariff policy for the Data Center Coalition; law firms negotiate step-downs one ESA at a time; nobody systematically tracks milestone-based releases.

**Why incumbents cannot easily own it.** Banks earn the LC fee and gain from over-collateralization. Brokers are paid on placement and do not monitor milestones afterwards. Utilities are the counterparty, so they will not optimize the developer's position. E3 works on policy for the trade group, not on per-site operations. *Weakness:* Marsh or Aon could add a dashboard, and large developers' treasury teams could keep this in Excel.

**30-day MVP.** (1) A tariff database: collateral formulas, accepted forms, rating thresholds and step-down/release triggers for the top 40 large-load tariffs plus PJM/MISO/ERCOT interconnection deposits, parsed from PUC filings. (2) A per-portfolio calculator: required collateral by site and month across the ramp, the cheapest mix of instruments, and release dates for which a claim can be filed. (3) A benchmark: "your $/MW vs the tariff median."

**Pilot design.** Load one developer's 3-6 ESAs plus its LC/surety schedule. Deliver within 3 weeks: (a) collateral that could be released or reduced now under existing terms; (b) savings from switching instrument mix (surety-backed LC vs cash LC); (c) a step-down calendar. Success: ≥$1M/yr in identified fee savings or ≥$50M in releasable collateral.

**Pricing hypothesis.** $75-250K/yr platform fee per developer, plus 5-15 bps on collateral restructured through a bank/surety panel (tech-enabled broker). Utility side: per-application credit review billed to the applicant, like a study deposit.

**Expansion path.** Data-center collateral → all large loads (fabs, battery plants, hydrogen, reshored manufacturing) → generator interconnection deposits (storage/solar developers; Key Capture's $300M LC) → becoming the standard counterparty-credit layer between large loads and utilities (a "credit desk as a service" for co-ops/munis) → an MGA-style risk product for stranded-load risk, using proprietary ramp/default data.

**Moat.** A normalized tariff and collateral database; a proprietary dataset of actual ramp vs contracted load and drawdown events (needed to price stranded-load risk); acceptance as a pre-vetted collateral form by utilities, a two-sided network that would be slow to build.

**Why it could become a $10B+ company (stretch).** Only if it becomes the underwriter of record for "will this large load show up and keep paying" across $100B+ of utility exposure (a Moody's/MGA hybrid for the grid-load asset class). Software alone tops out well below that.

**Direct competitors and adjacent threats.** Marsh / WTW / Aon / Lockton surety; relationship banks (Natixis, MUFG, Standard Chartered); Great Bay Renewables; the Dynamix fund; Crux (could add LC/surety to its debt marketplace); E3/Brattle consulting; ETRM credit modules (Triple Point, Allegro, **unverified fit**). Policy risk: regulators loosen requirements (developers lobbying for $450K/MW) or tighten them into cash-only.

**One sentence to send a CFO.** "Send us your utility service agreements and LC schedule. In two weeks we'll show you how much collateral you can release or re-instrument under terms you already signed, and we only get paid on what we free up."

**5 customer discovery questions.**
1. How much utility and interconnection collateral do you have outstanding today, in what forms, and at what all-in cost (bps + cash drag)?
2. Who tracks step-down and release milestones, and when did you last file a release claim? Did any collateral sit posted longer than the tariff required?
3. Did you choose LC vs surety vs cash on cost, or because that is what the utility or your bank defaulted to?
4. Would you pay a fee on released or re-instrumented collateral? What fee feels fair: bps, % of savings, flat?
5. Which utility credit desks are hardest to deal with, and would you share ESA terms (anonymized) to get a benchmark back?

**Hard kill criteria.**
- Fewer than 3 of 10 target CFOs/treasurers confirm ≥$100M outstanding collateral with no systematic release tracking.
- The pilot portfolio shows <$500K/yr of savings or <$25M of releasable collateral.
- Their broker (Marsh/Aon) already does milestone tracking and instrument optimization for free as part of placement.
- Developers refuse to share ESAs or LC schedules even under NDA.
- The ICP count turns out to be <100 firms with no credible path into other large loads or generator interconnection.

**Scores (1-10).**
| Pain | Urgency | ROI clarity | Accessibility | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 7 | 8 | 4 | 5 | 5 | 6 | 5 | 4 | 9 | 5 | **5.9** |

**Classification: B (weak), not A.** The money flow is verified and new, and no software or startup intermediary was found for sizing, optimizing and releasing collateral. But the pain is already public (Bloomberg, GTR, DCK, Aug 2026). Capital providers (banks, sureties, Great Bay, Dynamix) are moving in. The buyer pool is small and outside the founders' edge (security/AML/caller verification). Estimated chance the test passes: ~10-15%.

**14-day test.**
- Days 1-4: build a database of collateral formulas and release triggers for ~15 tariffs (Dominion, AEP Ohio, We Energies, PA model, Oncor/SB6, Georgia Power, Consumers, Entergy, Duke) from public PUC filings.
- Days 3-10: cold-reach 25 treasurers/CFOs at miner-to-AI converters and PE-backed developers (public 10-Ks disclose LC and restricted-cash balances, which serve as a pre-qualifier), plus 5 utility/co-op credit managers.
- Days 8-14: run 2 free portfolio reviews on real ESAs and LC schedules.
- **Pass:** 2 developers share real documents; at least one review finds ≥$1M/yr savings or ≥$25M releasable collateral; and 1 signed paid pilot or success-fee letter (≥$50K or ≥10 bps).
- **Fail:** documents not shared, savings under threshold, or "our broker does this."

---

## 3. Finalist 2: Cross-utility large-load request registry (KILL)

- **One-line problem.** The same data-center campus files requests with several utilities and ISOs, inflating load forecasts (60% of surveyed utilities hold ≥500 MW requests they have never served), and no single utility can see the duplicates.
- **Why it seemed promising.** A multi-party data problem (a structural reason one platform cannot see it); fits the lesson that shared networks win where a regulator can mandate participation; 195 GW signed / 331 GW disclosed.
- **Why it dies.** (1) In ERCOT, SB6 already forces self-disclosure of similar requests, and ERCOT/PJM run centralized large-load processes that can dedupe in-house (F1). (2) The buyers are utilities and regulators: slow procurement, few hundred buyers, low WTP (F4). (3) Collateral rules (Finalist 1) are the market's chosen fix for speculation, since $/MW deposits deter duplicate requests more effectively than a registry. (4) GridCARE ($64M) and Verse ($54M) own developer-side power-acceleration relationships and could add it.
- **Scores:** Pain 6, Urgency 6, ROI 4, Access 3, Pilot 3, Size 4, Expansion 5, Venture 4, Defensibility 6, Why now 8, Competition 5 → **avg 4.9. KILL.**

---

## 4. Lessons for the scoreboard
1. **In AI capex, debt and power, the intermediary slots are filled by capital, not software.** When a new financial obligation appears (utility collateral, GPU loans), banks, sureties and specialist funds supply the balance sheet within ~12 months. The remaining software gap is the analytics/lifecycle layer, which is real but sized like a tool (F4).
2. **Software-layer AI flows are cleared by the platforms** (marketplaces, model vendors, labor platforms). This repeats F1.
3. **The most durable new intermediary function is underwriting a new risk class**: "will a contracted large load actually ramp and keep paying." Whoever builds the ramp-vs-contract dataset could later price it. That is a 2028+ MGA/rating play, not a 2026 startup wedge, and it sits outside the founders' current edge.
