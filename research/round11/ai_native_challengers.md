# Round 11: AI-native challengers to hated, expensive incumbents

Date: 2026-10-05. Analyst stance: skeptical. 39 web searches; WebFetch/Reddit were blocked, so all evidence comes from search-result snippets.
Tags: **[S]** = seen in a search-result snippet at the URL given (page not opened). **[U]** = estimate or from memory, not verified this round. No URL here was made up. Every link was returned by search.

## TL;DR

- **The lens works best when there is a forced migration event, not when customers are merely angry.** Customer anger is everywhere and seldom makes anyone switch. What creates a real buying window is an incumbent forcing a re-platform or re-license, because the customer then has to spend migration money anyway. In 2025-2027 we found four such events:
  - PTC ends legacy Windchill license renewals after **Sep 30 2026**.
  - Oracle Agile PLM Premier Support ends **Dec 31 2027**.
  - IBM Maximo 7.6 support ended **Sep 30 2025**.
  - Trimble Viewpoint Vista sunsets **end of 2026**.
  - Salesforce CPQ (end-of-sale, Mar 2025) is a weaker fifth.
- **Most categories on the candidate list are already funded:**
  - DMS: Tekion ($650M+), Numa ($48M)
  - Construction ERP: Adaptive (raised $57M, incl. $30M B in Sep 2026), Agave ($15M A from Accel, Jul 2026), Flow, MerlinAI
  - Carrier TMS: Datatruck ($12M A), Alvys, Truckbase, Vektor
  - CMMS: MaintainX, now owned by Autodesk ($3.6B, May 2026); Tractian ($720M valuation)
  - MES: Tulip ($1.3B, Jan 2026)
  - CPQ: DealHub ($100M, Jan 2026), Dealops
  - PSA: Certinia bought the AI-native Moonnox; Rocketlane
  - Hospitality PMS: Mews, Cloudbeds, Apaleo [U]
  - BI, data catalog, GRC: crowded [U]
- **Top pick: AI-native PLM for discrete manufacturers**, entered through the Windchill and Agile migration windows. It averages **7.1/10**, which is below the 8.5 bar.
- **Runner-up: AI-native EAM for manufacturers moving off Maximo or SAP PM.** It averages **6.3/10**.
- **Neither pick clears the bar.** PLM is the best "incumbent replacement" thesis of the 11 rounds so far, but it carries a structural kill risk: the CAD vendor owns the PDM link.

---

## 1. Category screen

| Category | Incumbent pool | Anger / switching evidence | Forcing event | AI-native challengers (funding) | Verdict |
|---|---|---|---|---|---|
| **PLM** (Teamcenter, Windchill, ENOVIA, Agile) | Overall PLM market (CIMdata's broad definition, which includes CAD/CAE) was **$88.3B in 2025**. Siemens, PTC, Dassault, Autodesk, SAP and Aras hold about 83% [S](https://www.cimdata.com/en/news/item/30183-cimdata-publishes-executive-plm-market-report). The cPDm/PLM-system slice is about $15-25B [U]. | **Windchill:** buyers expect "less functionality for higher cost" under the ePLM re-licensing [S](https://www.goengineer.com/blog/windchill-migration-2026-your-options-risks-and-next-steps). A long-running eng-tips complaint describes PTC repackaging licenses "at a new higher price" and says it is cheaper to dump data out of Windchill than to license users [S](https://www.eng-tips.com/goto/post?id=9063971). **Agile:** most users declined Oracle Fusion PLM because moving means rebuilding [S](https://officeless.mekari.com/blog/oracle-agile-plm-end-of-life-alternatives). **Usability:** engineers fall back to Excel [S](https://openbom.com/blog/the-secret-of-why-engineers-are-using-excel-instead-of-plm-was-finally-revealed). **Teamcenter:** reviews mention modules sold outside the default license [S](https://www.peerspot.com/landing/product-report-siemens-plm-teamcenter). | **Yes, two hard deadlines.** Windchill legacy renewals end after 9/30/2026 [S](https://enterprise.trimech.com/windchill-migration-deadline-paths-forward-before-legacy-licenses-expire/). Agile Premier Support ends 12/31/2027 and 9.3.6 is the final release [S](https://www.traceone.com/oracle-agile-plm-when-does-support-end-and-what-are-the-options-trace-one). | Duro ($7.5M seed) was **acquired by Altium in Dec 2025** [S](https://www.automation.com/en-us/products/june-2025/duro-design-first-ai-native-plm-engineering). Bild has about $4.5M [S](https://www.cbinsights.com/company/bild-2). Propel raised $48M total, last round Series C in 2021, and runs on Salesforce [S](https://pulse2.com/propel-raises-18-million-funding/). OpenBOM [U funding]. Arena is owned by PTC. Leo AI ($9.7M seed) is a copilot layered on PLM [S](https://finder.techleap.nl/news/feed/leo-ai-raises-9-7m-for-ai-copilot). Adjacent: CoLab ($72M C, design review) [S](https://betakit.com/colab-cashes-in-on-ai-demand-with-72-million-usd-funding-round/) and **CADDi ($114M at $1.2B, Sep 2026, entering the US)** [S](https://siliconangle.com/2026/09/16/caddi-raises-114m-at-1-2b-valuation-to-bring-manufacturing-ai-to-north-america/). Aras is repositioning as "AI-native PLM" [S](https://www.businesswire.com/news/home/20260203577069/en/Aras-Expands-Engineering-and-Product-Leadership-to-Advance-AI-Native-PLM-Strategy). | **TOP 1.** No funded AI-native system-of-record challenger. |
| **EAM/CMMS** (IBM Maximo, SAP PM, HxGN/Infor EAM) | EAM is about $5-6B [U]. SAP PM sits inside ECC, whose mainstream maintenance ends in 2027 [U]. | Maximo customers on 7.6 must either pay 20-30% extended-support premiums or move to MAS. When converting old licenses to AppPoints, IBM "under-converts" entitlements [S](https://redresscompliance.com/ibm-maximo-application-suite-licensing.html). | **Yes.** Maximo 7.6.1 support ended 9/30/2025 [S](https://becolve.com/en/blog/support-for-ibm-maximo-7-6-1-ends-on-september-30-how-does-it-affect-you/). SAP ECC 2027 deadline [U]. | **Autodesk buying MaintainX for $3.6B** (>$135M ARR in 2026, >50% growth) [S](https://aecmag.com/news/autodesk-buys-maintainx-for-3-6bn/). Tractian $120M C at $720M [S](https://salestools.io/en/report/tractian-raises-120m-series-c). Verdantis is rebranding as "AI-native EAM" [S](https://techintelpro.com/news/ai/enterprise-ai/verdantis-rebrands-as-ai-super-agent-for-mro-eyes-ai-native-eam). Also Fiix (Rockwell), Limble, UpKeep [U]. | **Runner-up.** The category is proven but crowded below the enterprise tier. |
| **Construction ERP** (Viewpoint Vista, CMiC, Sage 300 CRE) | About $3-5B [U] | Vista migration is mandatory "whether your firm feels ready or not" [S](https://www.acumatica.com/blog/viewpoint-vista-construction-weighing-options/). | **Yes.** Vista sunsets at the end of 2026 [S](https://www.acumatica.com/blog/viewpoint-vista-construction-weighing-options/). | Adaptive: $30M B on 9/17/2026, $57M total, 750+ customers [S](https://www.thesaasnews.com/news/adaptive-raises-30m-series-b/). Agave: $15M A from Accel, Jul 2026 [S](https://seedtable.com/companies/agave/funding-rounds/series-a-2026-07). Flow ERP, MerlinAI, Access Coins Evo, Acumatica. | Kill: crowded, and a16z, Accel and Emergence already back players |
| **Auto DMS** (CDK, Reynolds) | CDK about $2B+ [U] | June 2024 ransomware outage; $100M antitrust settlement; Tekion's antitrust suit claims CDK blocks switching [S](https://en.wikipedia.org/wiki/CDK_Global) | Partial (outage) | Tekion ($650M+ raised, AI-native at NADA 2026), Numa ($32M B, $48M total, 600 dealers) [S](https://www.autoremarketing.com/ar/retail/numa-to-use-32m-funding-boost-to-power-the-ai-native-dealership) | Kill: Tekion owns the "AI-native DMS" pitch |
| **Carrier TMS** (McLeod, TMW/Trimble) | About $1-2B [U] | Vendor-written migration stories, e.g. "saved $100K migrating off McLeod" [S](https://www.datatruck.io/success-stories/how-apl-cargo-saved-100k-with-datatruck-migrating-off-mcleod) | No | Datatruck $12M A [S](https://pulse2.com/datatruck-12-million-series-a/amp/), Alvys, Truckbase, Vektor | Kill: crowded, and ACV at 30-500-truck fleets is under $50K |
| **WMS** (Manhattan, Blue Yonder, Körber) | About $4-5B [U] | Blue Yonder ransomware (Nov 2024: Starbucks, Morrisons, Sainsbury's; 3,000+ clients) [S](https://www.techmonitor.ai/technology/cybersecurity/blue-yonder-ransomware-attack-disrupts-supply-chains-across-uk-and-us). No evidence of mass switching found. | No | No enterprise AI-native WMS found. Point tools: Takt ($9M A), Gather AI, Logiwa, ShipHero [S](https://www.gather.ai/news/gather-ai-raises-17m-to-accelerate-growth-and-bring-warehouses-into-the-modern-era-with-ai-powered-inventory-monitoring) | Uncrowded, but **fails pilot speed**: physical go-lives take 6-12 months and peak-season freezes are a hard constraint. Shelve. |
| **MES** (Rockwell, Siemens Opcenter) | About $15B per vendor reports [U] | Generic complaints only | No | Tulip $120M D at $1.3B, Jan 2026 [S](https://www.builtinboston.com/articles/tulip-raises-120m-series-d-1b-valuation-20260116); Smart Craft (Japan); Apprentice (pharma) | Kill: Tulip owns it |
| **EHS** (Enablon, Cority, Intelex) | About $2B [U] | Weak | Regulatory only | Serenity $5.5M A [S](https://pulse2.com/serenity-ai-based-ehs-software-solutions-company-raises-5-5-million-series-a/amp/); Benchmark Gensuite's "Genny" agents | Kill: cost-center buyer; a close cousin of round-4's env-compliance thesis |
| **Field service** (ServiceMax/PTC, SF Field Service) | About $5B [U] | Not checked in depth | No | Zinier ($120M total), FieldPulse $50M C [S](https://techcrunch.com/?p=1933192); SMB home-services AI is crowded | Kill: crowded |
| **CPQ** (Salesforce CPQ) | About $2-3B [U] | End-of-sale confirmed Mar 2025; EOL expected 2029-30 [S](https://automationchampion.com/2026/07/06/salesforce-cpq-end-of-life-choose-between-revenue-cloud-and-cpq-alternative/) | Soft | DealHub $100M (Jan 2026) [S](https://www.riverwoodcapital.com/rwcm_news/dealhub-io-amplifies-massive-growth-with-100m-new-funding/), Dealops ($7M), Salesforce RCA | Kill: crowded, and the user flagged it |
| **PSA** (Kantata, Certinia) | About $1-2B [U] | Weak | No | Certinia bought AI-native Moonnox [S](https://diginomica.com/certinia-acquires-moonnox-speed-progress-ai-native-psa); Rocketlane | Kill: small, and the incumbent is absorbing AI-native players |
| **PIM** (Salsify, Akeneo) | About $1-3B [U] | Not verified this round | No (agentic-commerce feeds are a soft driver) | Emfas (€600K angel) [S](https://finder.techleap.nl/news/feed/emfas-raises-600k-for-ai-pim-system), Pimberly (debt) | Uncrowded, but adjacent to killed theses A and Q, and the pool is small. Not pursued. |
| **Property mgmt** (Yardi, RealPage) | About $3-4B [U] | Pricing and lock-in complaints; RealPage/Yardi antitrust suits [S](https://www.law360.com/articles/2393498) | No | AppFolio is AI-forward; EliseAI owns the AI layer [U] | Kill: AppFolio/EliseAI, plus antitrust overhang |
| **Hospitality PMS** (Oracle Opera) | About $1-2B [U] | Not checked | No | Mews, Cloudbeds, Apaleo, Stayntouch [U] | Kill: crowded [U] |
| **BI, data catalog, GRC, LMS** | Large | Known | No | Many (Atlan, Vanta/Drata, many AI BI tools) [U] | Kill: crowded [U] |

---

## 2. TOP PICK: AI-native PLM ("the AI-native replacement for Windchill and Agile")

**One sentence:** An AI-native PLM where agents do the BOM, change-order and compliance work engineers hate, and where moving off Windchill, Agile or Teamcenter takes weeks because an agent does the migration.

**Buyer:** VP Engineering or Director of PLM/Engineering Systems, with the CIO co-signing. Target: discrete manufacturers with $100M-$5B in revenue in industrial machinery, electronics/hi-tech, automotive tier-2/3, robotics, energy equipment and consumer hardware. **Avoid** medical devices (FDA-regulated, a large share of Agile's base) and aerospace and defense (ITAR).

**Buyers × ACV:**
- Agile has about 1,250-1,500 installed companies [S](https://idatalabs.com/tech/products/oracle-agile-plm). This is the beachhead and the forced-exit list.
- Windchill and Teamcenter each have thousands of mid-to-large customers [U].
- About 15-25K discrete manufacturers worldwide are in the $100M-$5B band [U].
- ACV is $100-500K once replacement is complete. A wedge deal is $50-150K.
- 5,000 × $200K = **$1B ARR**. The ceiling is set by a PLM-system pool of $15-25B [U].

**Why now:**
1. **Hard deadlines.** PTC ends legacy Windchill renewals after 9/30/2026 and pushes customers to role-based ePLM and Windchill+ [S](https://enterprise.trimech.com/windchill-migration-deadline-paths-forward-before-legacy-licenses-expire/). Agile Premier Support ends 12/31/2027, and most Agile users rejected Fusion [S](https://officeless.mekari.com/blog/oracle-agile-plm-end-of-life-alternatives). Thousands of companies must budget a PLM project in 2026-27 either way.
2. **AI removes the migration cost.** Today a PLM migration costs $300K-$1M upfront [S](https://www.digitalengineering247.com/article/integrating-legacy-data-perennial-plm-pain-point/plm) and takes 1-2 years. LLM agents can map data models, clean BOMs, reconcile part numbers and validate the result, which shrinks the switching cost that has protected incumbents.
3. **AI improves the product.** Most PLM work is unstructured: ECO impact analysis, where-used, supplier and compliance documents, and drawings. That is LLM territory. CADDi's $1.2B round shows investors will pay for "manufacturing data plus AI" [S](https://fortune.com/2026/09/15/caddi-manufacturing-startup-valuation-funding-round-series-d-exclusive/).
4. **The market leaves an opening.** CIMdata says SME PLM spend grows 18.6% a year versus 8.3% for large manufacturers [S](https://www.cimdata.com/en/news/item/28569-cimdata-publishes-plm-market-and-solution-provider-market-report). The challenger that existed, Duro, was acquired by Altium [S](https://www.automation.com/en-us/products/june-2025/duro-design-first-ai-native-plm-engineering).

**Why incumbents can't respond:** Revenue from licensing and services (VARs, SIs, migration factories) depends on complexity. Siemens even sells a "Teamcenter migration factory" [S](https://www.siemens.com/en-us/products/intelizign-engineering-services-teamcenter-migration-factory/). An AI-native data model would break customizations built up over 20 years. PTC's own move to ePLM is a re-licensing exercise, not a re-architecture. Skeptic's caveat: Aras and Siemens will ship credible agents on top (PTC's Document Vault agent already exists [S](https://www.digitalengineering247.com/article/ptc-brings-ai-powered-plm-to-hannover-messe-2025/plm)). The wedge has to beat "good-enough AI inside the incumbent."

**30-90 day pilot (runs alongside the incumbent):** a read-only connector to Windchill, Agile or Teamcenter plus ERP, covering two jobs.
- **(a) ECO agent:** drafts change orders, runs where-used and impact analysis, flags BOM errors before release, and prepares the CCB packet.
- **(b) Migration readiness scan:** a cleaned, mapped, de-duplicated copy of the full product record, with a fixed-price cutover quote.

Success metrics: ECO cycle time, BOM error rate, and engineer hours saved. This produces evidence in about 60 days without touching the system of record.

**Expansion:** shadow copy, then read/write for new products (greenfield programs first), then full cutover at the license renewal or support-end date, then adjacent modules: quality (non-regulated), supplier collaboration, compliance (RoHS/REACH/CRA), and service BOM.

**Moat:**
- Being the system of record for product data is about as sticky as enterprise software gets.
- A proprietary dataset of cross-PLM migrations makes each later migration cheaper.
- Over time, an agent graph across ECO, supplier and quality work.

**Kill risks:**
1. **The CAD-PDM link.** Creo is wired to Windchill, NX to Teamcenter, CATIA to ENOVIA. Without deep CAD integration, engineers stay in the vendor's PDM and a challenger becomes "PLM for BOMs only." This is how Arena and Propel got capped.
2. **Sales cycles.** Enterprise cycles run 6-18 months, and a VAR channel guards the accounts.
3. **Absorption.** CADDi ($1.2B) or Autodesk/Altium could move into AI PLM.
4. **Risk aversion.** Buyers often take the cheap path: Agile third-party support, or grudging ePLM renewals.
5. **Fragmentation.** Every customer runs a heavily customized schema.

**Scores (1-10):**

| Pain | Urgency | ROI clarity | Access | Pilot speed | Market | Expansion | Venture | Defensibility | Why now | Competition | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 8 | 6 | 5 | 6 | 8 | 8 | 8 | 7 | 8 | 7 | **7.1** |

---

## 3. RUNNER-UP: AI-native EAM for manufacturers ("the AI-native replacement for Maximo and SAP PM")

**One sentence:** An AI-native EAM where agents plan work orders, spare parts and PM schedules from sensor data, manuals and technician notes, and migrate customers off Maximo or SAP PM in weeks.

**Buyer:** VP Operations/Reliability at multi-plant manufacturers (food and beverage, chemicals, metals, paper, packaging). Avoid utilities, government and transit, even though they make up a large part of Maximo's base.

**Buyers × ACV:** Maximo has thousands of customers, 46% of them large enterprises and 51% in the US [S](https://idatalabs.com/tech/products/ibm-maximo), plus SAP PM users facing ECC 2027 [U]. About 8-12K multi-plant manufacturers [U] × $150K = about $1.2-1.8B.

**Why now:** Maximo 7.6 support has ended. The MAS migration forces a re-buy, and AppPoint under-conversion raises the price [S](https://redresscompliance.com/ibm-maximo-application-suite-licensing.html). Autodesk paid $3.6B for MaintainX, which proves exit value [S](https://aecmag.com/news/autodesk-buys-maintainx-for-3-6bn/).

**Pilot:** a spare-parts and PM-optimization agent on top of Maximo at one plant for 60 days. Metrics: MRO inventory reduction and unplanned downtime.

**Kill risks:**
- Competitors are already there: MaintainX, now with Autodesk's distribution; Tractian; Verdantis (which is doing exactly this pitch); Fiix; IBM's own MAS AI.
- "AI-native EAM" is no longer a novel pitch to VCs.
- Phase-1 research found buyers want ROI proof that takes longer than a quick pilot.

**Scores:**

| Pain | Urgency | ROI clarity | Access | Pilot speed | Market | Expansion | Venture | Defensibility | Why now | Competition | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 7 | 7 | 6 | 6 | 7 | 7 | 6 | 6 | 7 | 4 | **6.3** |

---

## 4. Lessons for STATUS.md

- **"Hated incumbent" alone predicts nothing. "Forced migration" predicts buying.** When an incumbent sunsets or re-licenses a product, its customers already have a migration budget and are open to alternatives. Track sunset calendars: Windchill 9/2026, Vista 12/2026, Agile 12/2027, SAP ECC 2027, Salesforce CPQ EOL around 2029.
- **Most categories on the hit list were funded in 2025-26.** Examples: Adaptive's B (Sep 2026), Agave's A (Jul 2026), Tulip's unicorn round (Jan 2026), DealHub's $100M (Jan 2026), MaintainX's exit (May 2026). This fits structural conclusion #1.
- **PLM is the exception: big pool, hard deadline, and the only native challenger (Duro) was acquired.** It still scores 7.1, mainly because of CAD lock-in and slow enterprise sales.
- **Cheapest next test:** interview 10 Agile PLM owners at non-medtech hi-tech and industrial firms. Ask whether they have budgeted the 2027 exit, what they are choosing, and whether an agent-led, fixed-price migration plus an ECO agent would change the decision. If 3 of 10 would pilot, PLM passes "Urgency" and "Access" at 8 or higher.
