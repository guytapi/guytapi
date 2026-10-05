# Round 2 — Physical AI Infrastructure Build-Out Bottlenecks (2025–2030)

Analyst stance: skeptical. Date: 2026-10-05. 35 web searches; WebFetch not used. Every URL below came from a search result. Figures labeled **[vendor claim]** come from vendors or content-marketing blogs and should be treated as directional. Figures labeled **[unverified]** are my own estimates or inferences.

---

## 0. Macro context (why this domain is worth looking at)

- 2026 capex for the top 5 US hyperscalers is about $660–720B, roughly double 2025's ~$380B. Amazon about $200B, Alphabet up to $185B, Meta $115–135B, Microsoft $120B+, Oracle about $50B. https://nasdaq.com/articles/720-billion-capex-trap-2-artificial-intelligence-ai-hyperscalers-spending-growth-while ; https://datacenterdynamics.com/en/news/moodys-hyperscaler-capex-forecasts-marked-up-by-85bn-to-close-in-on-1trn-by-2027/
- 30–50% of large data center capacity slated for 2026 will likely be delayed. One tracker covers 777 announced projects over 50 MW: about 16 GW is due in 2026, but only about 5 GW is under construction. In 2025, more than a quarter of expected capacity missed its date. https://www.networkworld.com/article/4201941/up-to-50-of-data-center-capacity-slated-for-2026-could-be-delayed.html ; https://www.axios.com/2026/02/24/ai-data-center-boom-projects-numbers ; https://eenews.net/articles/data-center-construction-delays-grow-report/
- Cost of delay: about $14.2M per month for a 60 MW facility (about $237K per MW-month), made up of $10.8M lost lease revenue, $2.2M labor and overhead, and $1.2M SLA penalties **[vendor claim — Kaizen consultancy]**. A 6-month slip cuts IRR from 17.1% to 8.8%. https://kaizen.com/us/insights-us/america-data-center-missing-dates/ ; ~$150M per GW-month of developer contracted revenue at risk: https://www.synmax.com/resource-hub/blog/datacenter-delays-are-a-3-billion-earnings-problem-and-most-of-it-hasnt-hit-yet-1
- About 23 GW was under construction globally at end-Sep 2025, roughly 75% of it in the US. https://about.bnef.com/insights/data-centers/ai-data-center-build-advances-at-full-speed-five-things-to-know/

**Key implication:** the value of one schedule-week is very large, roughly $50–60K per MW per week. The money is real. The hard question is who the buyer is and how many of them exist.

### Buyer-pool reality check (honest counts) [unverified estimates]
| Buyer type | Approx. count (US-centric) | Notes |
|---|---|---|
| Hyperscalers (self-build) | ~6–8 (AWS, MSFT, GOOG, META, ORCL, Apple, xAI, OpenAI/Stargate) | Tiny pool. They build tooling in-house and run long security reviews. |
| Neoclouds / AI-native developers | ~20–40 meaningful (CoreWeave, Crusoe, Nebius, Lambda, Fluidstack, Nscale, Together, SB Neo, etc.) | Fast buyers, but they concentrate quickly |
| Wholesale/colo developers | ~50–100 (Vantage, Aligned, QTS, Stack, Compass, EdgeCore, CyrusOne, DataBank, Prime, Tract…) | Best mid-size buyer pool |
| Large GCs doing mission-critical work | ~25–40 (DPR, Turner, Holder, Mortenson, Clayco, Whiting-Turner, Fortis, HITT, JE Dunn…) | Procore and Autodesk are already in place here |
| Electrical / mechanical subcontractors on DC work | ~300–600 with meaningful DC volume (Rosendin, Cupertino Electric, IES, MYR, Faith Technologies, Sachs, Southland…) | Large, under-served, and electrical is 45–70% of DC build cost |
| Commissioning firms (CxA) | ~200–500 | Fragmented services firms. Low ACV unless sold per project |
| Equipment OEMs / fabricators (transformers, switchgear, gensets, CDUs, skids) | ~100–300 relevant plants | Reshoring wave: more than $2B in announced NA transformer capacity |
| BESS / BTM generation IPPs and EPCs | ~300–1,000 | Much larger pool, less "AI hype" |

---

## 1. Problem inventory (19 problems)

### P1. Level 5 Integrated Systems Testing (IST) is the new critical path for liquid-cooled AI halls — **STRONG**
- **Problem:** Liquid cooling has roughly tripled IST duration, from 4–6 weeks for air-cooled halls to 10–14 weeks for liquid-cooled halls. L5 IST tests power, cooling and controls together: failover, black-building test, load banks. **[source is a practitioner Substack; treat as directional]**
- **Who:** Cx managers at developers and neoclouds, CxA firms, GC MEP leads. About 100–150 organizations run L5 on AI halls each year.
- **Evidence:** https://cxmatters.substack.com/p/racing-the-clock-the-challenges-of-commissioning-in-fast-track-data-center-delivery ; Uptime commentary on the liquid cooling Cx gap: https://datacentremagazine.com/news/from-commissioning-to-operations-best-practices-for-reliable-liquid-cooling ; Tetra Tech on liquid-cooled Cx challenges: https://www.tetratech.com/experts/john-herboth-discusses-challenges-in-commissioning-liquid-cooled-ai-data-centers/
- **$ pain:** At about $237K per MW-month, an extra 6–8 weeks of IST on a 100 MW hall costs about $35–45M in deferred revenue **[unverified arithmetic on vendor figure]**.
- **Existing:** CxAlloy (market leader; acquired OTTO, an automated functional-testing platform), Facility Grid (acquired PingCx in Aug 2026, an autonomous BAS commissioning tool, and has a DC-specific product), CxPlanner, Procore/Autodesk Build checklists. https://www.cxalloy.com/2026/05/26/ ; https://www.startupresearcher.com/news/facility-grid-acquires-autonomous-commissioning-platform-pingcx ; https://datacenterdynamics.com/en/product-news/facility-grid-launches-tailored-solution-for-data-centers
- **Why unsolved:** Incumbent Cx tools are checklist and issue trackers, systems of record. Nobody owns the work of turning live BMS/EPMS/CDU telemetry, load-bank data and FAT records into a pass/fail verdict and a blocker list. Incumbents are now moving there (OTTO, PingCx), which validates the space but narrows the window.

### P2. Liquid cooling flush/fill and CDU factory witness testing are being skipped — **MEDIUM** (sub-problem of P1)
- **Problem:** Uptime (Jan 2026) reports operators skipping CDU factory witness testing under schedule pressure. Cold plates have 25–50 μm microchannels, so debris or trapped air causes thermal throttling and shutdowns.
- **Evidence:** https://datacentremagazine.com/news/from-commissioning-to-operations-best-practices-for-reliable-liquid-cooling ; https://www.vertiv.com/en-emea/insights/articles/blog-posts/the-circulatory-system-of-the-ai-factory-why-flush-and-fill-is-no-longer-enough/
- **Who:** Neocloud ops and Cx teams, mechanical subs.
- **Existing:** Vertiv, Motivair/Schneider, CoolIT services. Point products only.
- **Why unsolved:** It is mostly a procedures and services problem. A software wedge exists here (digital flush records, particle-count logging, chain of custody), but alone it is too narrow.

### P3. Long-lead electrical equipment: delivery uncertainty and expediting — **STRONG pain / MEDIUM startup fit**
- **Problem:** US transformers average about 128 weeks, with large units at 3–5 years. GSU transformers exceed 160 weeks. HV breakers are at 125 weeks. Some suppliers have switchgear sold through 2028. Distribution-class gear runs 52–78 weeks.
- **Evidence:** https://thenextweb.com/news/us-power-companies-scramble-data-centre-equipment ; https://www.powermag.com/transformers-in-2026-shortage-scramble-or-self-inflicted-crisis ; https://www.kitco.com/news/off-the-wire/2026-07-09/us-power-companies-scramble-secure-equipment-surging-data-center ; https://www.datacenterdynamics.com/en/opinions/the-electrical-infrastructure-gap-what-ai-data-center-density-demands-from-every-project-team/
- **Who:** Procurement and supply chain leads at developers (Decima, for example, has dedicated "Long-Lead Equipment Procurement Manager" roles: https://job-boards.greenhouse.io/decimainternational/jobs/4691478006), GC procurement teams, and electrical subs.
- **$ pain:** One late MV switchgear lineup can idle an entire hall, at $1M+ per week for a 20–60 MW hall **[unverified]**.
- **Existing:** Elektrik (MV/HV components distribution platform; growth round from Lead Edge, undisclosed; cuts sourcing from about 20 days to 1; serves most of the top-50 NA EPCs) https://pulse2.com/elektrik-secures-growth-investment-from-lead-edge-capital-to-accelerate-electrical-infrastructure-procurement/ ; Kojo (about $94M raised; Wesco invested $10M; joint "Project POs" product for long-lead DC purchase orders) https://distributionstrategy.com/2025/09/kojo-secures-10-million-investment-from-wesco-expanding-construction-tech-platform/ ; Field Materials (more than $1.3B order volume, 3.5x YoY, data center driven) https://www.constructiondive.com/press-release/20260327-fueled-by-data-center-boom-field-materials-hits-13b-in-construction-purc ; Giga Energy (transformer supplier) https://www.gigaenergy.com/blog/lead-time-delays-for-data-centers
- **Why unsolved:** The root cause is physical capacity, and software does not create transformers. Software can deliver visibility into OEM production status (where in the queue, FAT dates, sub-component shortages), re-sequencing of construction around real ship dates, and secondary-market reallocation of slots. The Wesco/Kojo and Elektrik moves show distributors want to own this. Kill risk: OEMs refuse to share data.

### P4. FAT/SAT quality: defects discovered on site in long-lead gear — **MEDIUM**
- **Problem:** Delays often start in the factory, from incomplete verification, documentation gaps, or equipment shipped without full testing. New plants staffed by new workers raise defect risk **[inference]**.
- **Evidence:** SGS, Sep 2026: https://www.sgs.com/en-sg/news/2026/09/why-fat-and-sat-matter-more-than-ever-for-critical-data-equipment
- **Who:** Owners' QA/QC, Cx agents, OEM quality managers.
- **Existing:** Third-party inspectors (SGS, Intertek), generic inspection apps (MangoApps templates).
- **Why unsolved:** FAT data is PDFs and witness signatures that never connect to site Cx. A good wedge into P1 and P3, but weak as a standalone company.

### P5. Behind-the-meter gas turbines are sold out to about 2029–2031 — **STRONG pain / WEAK for a startup**
- **Evidence:** GE Vernova gas backlog plus slot reservations went from 100 GW to 116 GW in Q2 2026, with deliveries into 2031: https://www.utilitydive.com/news/ge-vernova-gas-turbine-backlog-climbs-to-116-gw/826039/ ; Siemens Energy backlog 69 GW: https://www.turbomachinerymag.com/view/siemens-energy-posts-record-backlog-joining-ge-vernova-and-baker-hughes-in-a-record-quarter-for-gas-turbines ; Of about 90 GW of BTM generation announced, only about 2 GW is operating and 60% is announcement only: https://cleanview.co/reports/behind-the-meter-data-centers/full-report
- **Why WEAK:** This is a hardware and capital problem, solved by recips, fuel cells (Bloom) and aeroderivatives. The software adjacent to it is thin: Cleanview-style intelligence tells you who is real, but that is a data business with a small market.

### P6. Electrician shortage — **STRONG pain / MEDIUM startup fit**
- **Evidence:** McKinsey: about 130K additional electricians needed by 2030 for AI infrastructure. Electrical work is 45–70% of DC construction cost. Oracle/OpenAI completion dates moved from 2027 to 2028 partly due to labor (Bloomberg, via Fortune). Texas housing is delayed 2 months as DCs poach electricians. https://fortune.com/2026/03/02/ai-data-centers-electrician-shortage-gen-z-training-careers/ ; https://www.planetizen.com/news/2026/05/137471-texas-data-centers-demand-electricians-delaying-housing-construction-2-months
- **Existing:** Buildforce (electrician staffing; $10M Series A, Jul 2026) https://pulse2.com/buildforce-10-million-series-a-raised-to-staff-electricians-nationally/ ; Tradesmen International and traditional staffing; hyperscaler-funded training (Meta, Google).
- **Why partially unsolved:** Staffing marketplaces are low-margin, and labor supply is fixed in the short run. The real software lever is productivity per electrician (P7).

### P7. Electrical/MEP production rates run far below plan — **STRONG**
- **Evidence:** Buildots benchmark across 25M sq ft of DC projects: electrical containment is progressing at 59.4% of the required pace, HVAC at 76.9%, domestic water at 44.9%. https://pulse2.com/buildots-raises-130-million/amp/ ; https://www.remio.ai/post/buildots-funding-round-adds-130-million-as-mega-projects-test-construction-ai
- **Who:** Electrical subcontractor PMs and superintendents (Rosendin, Cupertino Electric, IES, MYR, Faith Technologies, etc.) and GC operations.
- **$ pain:** A 10% productivity gain on a $300M electrical package is $30M **[unverified]**.
- **Existing:** Buildots ($297M total, $130M round, explicit DC focus), Doxel, OpenSpace for progress tracking at the GC/owner level. Trunk Tools ($70M) for documents. Field-level tools for subs (Fieldwire, Hilti-owned; Procore) are generic.
- **Why unsolved:** Progress-capture tools tell the GC the sub is behind but do not help the sub plan crews, prefab, material kitting and work packages. Subs are under-tooled. Faith Technologies and others are building prefab ("industrialized construction") in-house: https://faithtechinc.com/services-and-solutions/industrialized-construction-builds

### P8. Change orders, variations and delay claims — **MEDIUM**
- **Evidence:** Construction is the most common source of high-value DC disputes. Variation valuation and design responsibility are the main friction points. https://bclplaw.com/en-US/events-insights-news/dispute-resolution-in-data-centre-projects-proactive-strategies-for-a-high-stakes-environment.html ; https://stoneturn.com/insight/cost-accountability-in-data-center-construction-disputes/ ; https://www.fenwickelliott.com/knowledge-hub/annual-review/ar-2025/common-issues-in-data-centre-construction-and-how-to-avoid-them/
- **Who:** GC and sub project controls, owners' cost teams, claims consultants (StoneTurn, FTI, Ankura).
- **Existing:** Procore, Trunk Tools (Cortex links drawings, RFIs, changes and schedules), Document Crunch (contract AI; funding not verified in this round), forensic schedulers.
- **Why unsolved:** Claims work is consultant-heavy and episodic. Owners on cost-plus/GMP contracts with speed premiums often pay rather than fight, which lowers urgency until the cycle turns. The opportunity becomes STRONG if the build cycle slows and disputes spike (counter-cyclical hedge).

### P9. Commissioning talent shortage — **MEDIUM**
- **Evidence:** Claim of 340K unfilled DC positions by end-2026, with Cx agents taking about 3.5 months to hire **[vendor claim — Introl blog, low quality]** https://introl.com/blog/data-center-workforce-shortage-340000-unfilled-positions-2026 ; neoclouds hiring Cx engineers (Fluidstack, Crusoe job posts) https://jobs.dukecapitalpartners.duke.edu/companies/fluidstack/jobs/80459760-commissioning-project-engineer-data-centers
- **Implication:** This supports P1. Software that lets one Cx engineer cover 2–3x the scope fills the same gap from the other side.

### P10. Data center operations staffing — **MEDIUM**
- **Evidence:** Uptime 2026 survey: more than half of operators struggle to find qualified candidates, and turnover persists, often because staff are poached by other DC firms. https://intelligence.uptimeinstitute.com/resource/uptime-institute-global-data-center-survey-2026 ; https://www.businesswire.com/news/home/20260728112406/en/
- **Existing:** Phaidra (about $120M total; $50M+ Series B in Oct 2025 led by Collaborative, NVIDIA participating; "Prism" launched at GTC 2026) https://pulse2.com/phaidra-over-50-million-series-b-raised-for-building-ai-agents-for-ai-factories ; EkkoSense, Schneider/Vertiv DCIM.
- **Why medium:** Real, but well funded and close to OEM DCIM, which bundles it.

### P11. GPU cluster bring-up, burn-in and acceptance testing — **MEDIUM (crowded)**
- **Evidence:** 3–7 days of burn-in is the norm, and acceptance has 4 layers. Crusoe publishes its own burn-in process. NVIDIA ships a "Cluster Readiness Engine". https://www.crusoe.ai/resources/blog/how-crusoe-burn-in-tests-every-node-before-it-reaches-you ; https://docs.nvidia.com/cluster-readiness-engine/operations/faq ; SemiAnalysis ClusterMAX rates neocloud health checks as often poor: https://newsletter.semianalysis.com/p/clustermax-30-the-industry-standard
- **Why medium:** NVIDIA is giving it away and the top neoclouds build in-house (Nscale "Fleet Operations", Crusoe "Command Center"). There may be an independent-acceptance niche for financiers and lessees, but buyers are few.

### P12. GPU fleet reliability in production — **WEAK (for a new entrant)**
- **Evidence:** Meta's Llama 3 run had 419 interruptions in 54 days on 16K H100s, one about every 3 hours, with GPU and HBM3 causing about 47%. https://datacenterdynamics.com/en/news/meta-report-details-hundreds-of-gpu-and-hbm3-related-interruptions-to-llama-3-training-run
- **Existing:** Clockwork ($40M+; $20.6M round led by NEA; FleetIQ, TorchPass; vendor claim of about $6M per year saved per 2,048 H200s) https://techstartups.com/2025/09/10/stanford-spinout-clockwork-raises-20-6m-in-funding-launches-fleetiq-to-tackle-ais-gpu-bottleneck-and-inefficiency/ ; https://www.futuriom.com/articles/news/clockwork-io-guarantees-ai-training-uptime/2026/07 ; NVIDIA, hyperscaler in-house tooling, Nscale https://www.nscale.com/blog/the-gpu-fleet-that-fixes-itself
- **Why WEAK:** This is platform territory (NVIDIA plus the cloud itself), the same absorption pattern that killed round 1.

### P13. Site selection, power due diligence and entitlement — **WEAK (crowded)**
- **Existing:** Paces ($11M Series A, YC) https://www.esgtoday.com/?p=16827 ; Build.inc ($8.5M seed, Index; sells services, not software) https://thenextweb.com/news/build-8-5m-agentic-real-estate-ai-infrastructure ; Landgate; Cleanview. YC has an explicit RFS for automating DC development: https://www.datacenterdynamics.com/en/news/y-combinator-looks-for-startups-trying-to-remove-humans-from-data-center-development-and-operation
- **Why WEAK:** Heavily funded, data is commoditizing, buyers are lumpy, and many tools compete.

### P14. Developer-side interconnection and time-to-power management — **MEDIUM-WEAK**
- **Evidence:** Power availability is now the first gating question. https://www.bloomenergy.com/blog/data-center-site-selection-why-power-defines-where-you-can-build/
- **Why:** The bottleneck sits at the utility and ISO. Developer-side software (study tracking, queue analytics) helps at the margin. Paces is here.

### P15. Design and BIM automation for DC MEP — **WEAK (crowded)**
- **Existing:** ArchiLabs (YC F24, $3M) https://ycombinator.com/companies/archilabs ; Endra ($75M; $50M Series A led by a16z, MEP design) https://sovereignmagazine.com/article/endra-mep-engineering-us-uk-expansion ; Autodesk.
- **Why WEAK:** Well-capitalized competitors plus Autodesk distribution.

### P16. Commodity construction materials procurement — **WEAK (taken)**
- Field Materials, Kojo/Wesco and Elektrik already ride the DC wave (see P3). It is late to enter.

### P17. BESS commissioning delays and SAT underperformance — **MEDIUM-STRONG**
- **Evidence:** Typical BESS commissioning delays run 1–2 months, sometimes 8+. Only 83% of projects met nameplate at SAT. About 19% of projects lose returns to technical issues and downtime. https://www.energy-storage.news/commissioning-delays-and-technical-gaps-plague-battery-storage-handovers-industry-experts-warn/ ; https://www.ess-news.com/?p=6558 ; https://solarbuildermag.com/energy-storage/survey-of-bess-professionals-highlights-issues-in-rapidly-growing-industry/
- **Who:** IPPs, BESS EPCs, owner's engineers, plus hyperscalers and developers now co-locating BESS behind the meter. There are hundreds of buyers.
- **Existing:** ACCURE (battery analytics), Power Factors, TWAICE, Fluence/Tesla native tools.
- **Why unsolved:** Operating analytics exist, but construction-to-COD commissioning (punch, SAT evidence, OEM-EPC blame allocation) is still spreadsheets **[partly unverified]**. Notably, the same "commissioning evidence engine" from P1 applies here, which widens P1's buyer pool.

### P18. OEM factory ramp (reshoring): new transformer and switchgear plants staffed by new workers — **MEDIUM**
- **Evidence:** More than $2B in announced NA transformer capacity ramping through 2028: Hitachi Energy $457M South Boston VA (825 jobs) and $528M Mississippi (700+ jobs), Siemens Energy Charlotte ($150M, 600 hires; $421M total in NC). Manufacturers cite labor shortages as a cause. https://pulse2.com/hitachi-energy-to-invest-528-million-in-mississippi-transformer-factory-and-create-more-than-700-jobs/ ; https://tdworld.com/utility-business/article/21282724/transformer-shortage-siemens-energy-to-expand-manufacturing-in-charlotte-north-carolina ; https://www.kitco.com/news/off-the-wire/2026-07-09/us-power-companies-scramble-secure-equipment-surging-data-center
- **Who:** Plant managers and quality leads at about 100–300 plants (including tier-2 fabricators of skids, eHouses and busway).
- **Existing:** Generic MES and connected-worker tools (Tulip, Augmentir, Siemens Opcenter).
- **Why medium:** Real, but this is the generic "manufacturing ops / connected worker" category with incumbents, and large OEMs buy slowly.

### P19. Phantom pipeline: suppliers can't tell real projects from announcements — **MEDIUM**
- **Evidence:** Of about 16 GW due in 2026, only about 5 GW is under construction (networkworld link above). Of about 90 GW of BTM generation, 60% is announcement only (Cleanview link above).
- **Who:** OEMs, distributors and subs deciding where to allocate slots and crews.
- **Why medium:** This is a data and intelligence business (Cleanview, BNEF, DC Byte, Sightline). Good companion data, but its market is likely below $1B.

---

## 2. Top 3 startup theses

### Thesis A — "Readiness engine" for AI data halls: autonomous L1–L5 commissioning evidence and energization-blocker clearing
**One sentence:** "We turn every FAT report, Cx test, load-bank run, BMS/EPMS/CDU log and flush record on a data center (and BESS) build into a live, auditable 'ready-to-energize' verdict. That cuts weeks off IST, and every week is worth about $1M+ per hall."

- **Who buys:** VP Construction or Head of Cx at colo developers and neoclouds (economic buyer; delay costs hit their P&L). Users are CxA firms and GC MEP teams. Expansion goes to BESS and BTM plant owners.
- **Bottom-up math [unverified]:**
  - Wedge: about 120 developers and neoclouds × ~3 active AI halls per year × $150K per hall-project ≈ $54M per year in the US core.
  - Per-MW pricing alternative: US DC capacity reaching readiness is about 10–15 GW per year. At $5K per MW that is $50–75M per year US, or about $120M globally.
  - Plus BESS and BTM: about 300 IPP/EPC buyers × $75K ≈ $22M per year.
  - Plus operations continuity (the same evidence becomes the O&M baseline and digital twin seed): +$50–100M.
  - **Honest SAM is about $250–400M.** Reaching $1B+ requires becoming the system of record for the physical readiness of all critical infrastructure (DC, BESS, substations, fabs) or taking a share of Cx services revenue through AI-native Cx services, which is a big pool. Cx is typically about 1–3% of MEP cost **[unverified]** on roughly $100B+ per year of DC MEP spend, so about $1–3B per year in services.
- **Why now:** Liquid cooling has roughly tripled IST time (P1). Cx talent is short (P9). Operators are skipping FWT (P2). The delay cost per week has never been higher.
- **Why incumbents can't (yet):** CxAlloy and Facility Grid are checklist and forms systems of record built for human Cx agents. Their acquisitions (OTTO, PingCx) are BAS-only. Procore and Autodesk are document-centric and don't ingest OT telemetry. Vertiv and Schneider only see their own equipment.
- **90-day pilot:** One live liquid-cooled hall at a neocloud or colo developer. Ingest FAT PDFs, L3/L4 records and L5 IST telemetry (load banks, EPMS, CDU). Deliver automated pass/fail scripts, an auto-generated deficiency log and a daily "blockers to energize" list. Measure IST days versus the developer's prior hall.
- **Strongest kill risk:** **Absorption plus services drag.** CxAlloy or Facility Grid adds AI ingestion within 12–18 months, or the product only works with heavy forward-deployed engineers, which caps margins. Secondary risk: telemetry access is blocked by OEM and controls-vendor data silos. This is a **MEDIUM-STRONG** thesis.

### Thesis B — Production-status and expediting network for long-lead electrical and mechanical equipment
**One sentence:** "A 'FlightAware for transformers and switchgear': we connect OEM and fabricator production milestones, FAT dates and sub-component shortages to developers' construction schedules, so builders re-sequence before a late lineup idles a hall, and stranded slots get resold."

- **Who buys:** Developer and neocloud supply chain heads (Decima-style "long-lead procurement managers"), GC procurement, and electrical subs. The supply side (OEMs and tier-2 fabricators) joins for free, or pays for demand-signal data (P19).
- **Bottom-up math [unverified]:** About 150 developers, GCs and large subs × $150K ≈ $22M per year from visibility SaaS. The venture-scale version is transactional: take 1–3% on reallocated or secondary-market slots and expedite fees on a long-lead equipment market of about $40–60B per year for US DC plus grid **[unverified]**. Capturing 1% of flow means $400–600M of take. Elektrik and Field Materials prove flow-based models can scale ($1.3B volume).
- **Why now:** Lead times of 128–160+ weeks, switchgear sold out to 2028, and new plants ramping with new labor (P18) make delivery dates less reliable, not more.
- **Why incumbents can't:** Each OEM sees only its own queue and each buyer sees only its own POs. Procore and Kojo track POs, not factory WIP. Distributors (Wesco, Elektrik) are conflicted as sellers.
- **90-day pilot:** One developer with 10–30 open long-lead POs across 4–6 OEMs. Weekly milestone capture (manual plus OEM portal plus email parsing), risk scores, and a schedule-impact link to P6. Success means 2+ slippages flagged at least 4 weeks earlier than the developer's current process.
- **Strongest kill risk:** **OEMs won't share data** because a seller's market gives them no reason to. The product then collapses into an email-parsing expediting service. Also Wesco/Kojo "Project POs" and Elektrik are already heading this way. **MEDIUM**.

### Thesis C — Operating system for electrical subcontractors on mission-critical megaprojects
**One sentence:** "Electrical work is 45–70% of a data center's cost and runs at about 60% of planned pace. We give electrical subcontractors AI-planned work packages, prefab and kitting, crew allocation, and change and claim capture, so each scarce electrician installs more and every change gets paid."

- **Who buys:** COO or VP Operations at about 300–600 electrical subs with DC volume, starting with the top 50 (Rosendin, Cupertino Electric, IES, MYR, Faith, Sachs, etc.). Their DC backlogs run $100M–$2B+.
- **Bottom-up math [unverified]:** Top 50 subs × $400K ACV = $20M. Next 500 × $100K = $50M. Adding the mechanical subs (similar count) doubles that to about $140M. Payments and claims recovery (a % of recovered change orders) is the expansion lever. To reach $1B+, expand to all industrial, energy and fab electrical work (the BESS, solar, substation and semiconductor build-out is the same buyer). There are about 70K US electrical contractors, but only about 2–5K are large enough for a $50K ACV **[unverified]**.
- **Why now:** The electrician shortage is fixed in the short run (P6). Buildots data shows electrical containment at 59% of required pace (P7). Disputes are rising (P8). Subs have margin at risk on GMP contracts with speed premiums.
- **Why incumbents can't:** Procore and Buildots sell to GCs and owners, whose interests can conflict with the sub's on claims. Fieldwire is a generic task tool. Trunk Tools is GC-centric. ERP vendors for subs (Viewpoint/Trimble, Foundation) are accounting-first.
- **90-day pilot:** One electrical sub on one DC project. Ingest drawings, specs, schedule and daily logs. Generate weekly work packages plus a material kitting plan, and auto-detect scope changes from RFIs and drawing revisions into change-order requests. Measure installed feet per labor-hour versus baseline, and change-order dollars captured.
- **Strongest kill risk:** **Construction-tech sales cycles and adoption** (field crews resist new tools), plus Procore or Trunk Tools moving downstream to subs. Subs' IT budgets are thin, and $50K+ ACV is plausible only at the top few hundred. **MEDIUM**.

---

## 3. Bottom line (skeptical)

1. **The pain is real and quantified.** Delay costs about $50–60K per MW per week, and 30–50% of 2026 capacity is at risk. This domain passes "huge pain now" and "where the world is going" more clearly than round 1.
2. **The buyer pool is the problem.** The highest-value buyers (about 8 hyperscalers) are tiny in number and build in-house. A real mid-market of about 100–200 developers, neoclouds and GCs exists, but each sub-niche (Cx, procurement, GPU bring-up) produces a SAM in the low hundreds of millions. **$1B+ requires either (a) a transactional or services-capture model or (b) expanding from DC to the whole electrified build-out (BESS, substations, fabs, BTM generation).**
3. **Avoid:** GPU fleet reliability, GPU bring-up, site selection, design automation and commodity procurement. All are crowded or platform-absorbed (NVIDIA, Paces/Build, Endra/ArchiLabs, Field Materials/Kojo).
4. **Best bet:** Thesis A (readiness and commissioning engine), with BESS and BTM expansion built into the plan from day one, and a services-capture option (AI-native CxA) if pure SaaS stalls. Also watch for a cycle turn. If the build-out decelerates in 2027–28, claims and disputes (P8) become the stronger counter-cyclical play.

### Unverified / caveats
- The $14.2M per month per 60 MW figure is a Kaizen marketing estimate. The IST 10–14 week figure is from a practitioner Substack. The 340K unfilled positions figure is an Introl blog estimate. All buyer counts, ACVs and market sizes are my estimates.
- Document Crunch, ACCURE, TWAICE and Power Factors funding were not verified this round. The "Nomad (Cx)" company named in the brief could not be identified via search. Search returned only unrelated "Nomad" companies.
