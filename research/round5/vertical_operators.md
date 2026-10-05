# Round 5 — "AI-native vertical operator" white-space scan

Date: 2026-10-05. Method: 40 web searches (WebSearch only; WebFetch not used). Pattern tested: "the EliseAI / Avoca / Toma of X" — an AI employee that takes over a labor-heavy front/back-office function in a fragmented mid-market vertical, then expands into the system of record.

**Legend.** `[V]` = verified in a search result during this session (source listed). `[E]` = analyst estimate / prior knowledge, NOT verified this session; treat as directional. URLs listed are only ones that appeared in search results.

---

## 1. Vertical scan (21 verticals)

Crowding score: 1 = open (no funded AI-native), 2 = seed-only, 3 = one Series A+ AI-native, 4 = several funded / incumbent bundling, 5 = crowded (killed list).

| # | Vertical | Labor pool & pain | # US buyers (mid-market) | Plausible ACV | AI readiness | Funded AI-native players found | Crowd | Verdict |
|---|---|---|---|---|---|---|---|---|
| 1 | **Heavy equipment / ag / truck dealers – service, parts, rental desk** | ~10K diesel-tech shortfall/yr costing dealers **~$7B/yr** in lost shop+parts revenue; ~$6M avg per dealer `[V]`; parts/service counters are phone+email+manual lookups | ~5–8K dealer companies, ~15K rooftops (AED + EDA + ATD + material handling) `[E]` | $50–250K per dealer group `[E]` | Medium: DMS (VitalEdge/IntelliDealer, e-Emphasys, CDK) + PDF manuals; email/phone heavy | Brilliant Harvest ($4M seed, Feb-2026; ~50% of CNH large dealer stores, Titan, RME) `[V]`; Chasi (YC W26, sales/rental/service agents) `[V]`; United Rentals built own agent (in-house) `[V]` | 2 | **TOP 1** |
| 2 | **Mid-market 3PL warehouses – client service, billing, claims** | Account managers/CSRs answer brand WISMO/inventory/ASN emails; billing & accessorial capture manual; carrier claims | ~70–73K "3PL businesses" total `[V]`; warehousing 3PLs $10M–$500M rev ~5–8K `[E]` | $50–120K `[E]` | Medium-high: WMS (Extensiv, Deposco, Logiwa) + email/portals | Prox (YC; live at ShipBob on carrier claims) `[V]`; Pallet ($27M B, $50M total; brokers/3PLs/forwarders, horizontal-logistics) `[V]`; Cartage ($3.3M seed) `[V]`; Conduit ($6M seed, dock/yard) `[V]`; Ciridae ($20M seed, services-led) `[V]` | 3 | **TOP 2** (watch Pallet) |
| 3 | **Contract security guard firms – scheduling, call-offs, payroll/billing, client reporting** | Guard turnover 89–200%+/yr `[V]`; schedulers/dispatchers/HR fight call-offs 24/7; 3–8% margins `[E]` | 112K "security services" businesses (IBISWorld) `[V]`; firms with 100+ guards ~4–6K `[E]` | $40–120K `[E]` | Medium: WFM (TrackTik/Trackforce, Belfry) + text/phone | Guard Owl ($3M seed, "agentic AI" for security ops) `[V]`; TrackTik incumbent ($45M historic raise) `[V]`; Belfry (guard software; funding unverified) | 2 | **TOP 3** (bundle w/ janitorial) |
| 4 | Commercial janitorial / facility services contractors | Same call-off/turnover dynamics; site inspections, supply orders, client tickets | ~5K firms with $5M+ rev `[E]` | $30–80K `[E]` | Low-med | Teambridge markets AI agents for janitorial & light industrial (funding not verified) `[V]`; robotics players (Brain Corp, Avidbots) not ops | 2 | Fold into #3 |
| 5 | Light-industrial staffing – shift fill, onboarding, timesheets, VMS, payroll | Coordinators/recruiters; timesheets re-keyed from client formats `[V]` | 20K+ staffing firms `[V]`; industrial top-59 = $28.7B `[V]` | $30–100K `[E]` | High (Bullhorn/Avionte APIs) | Alex ($20M incl. $17M A, interviews) `[V]`; Asendia (YC S26, AI recruiters) `[V]`; Teambridge Relay shift-fill agent `[V]`; Central ($8.6M, payroll/HR) `[V]`; ATS incumbents bundling | 4 | Crowded on recruiting; back-office (timesheet→payroll→invoice) is runner-up |
| 6 | Trucking carriers back office (dispatch, billing, safety, recruiting) | Dispatch/billing clerks; driver recruiting churn | ~5–8K carriers with 50–1,000 trucks `[E]` | $30–150K `[E]` | Medium | DataTruck ($12M A, Jan-2026, ~500 carriers, AI TMS) `[V]`; Cargofy ($11M A, Jun-2026) `[V]`; Numeo ($2.7M seed) `[V]`; Lunavo (YC) `[V]`; bubba.ai `[V]`; Kazakh driver-hiring AI `[V]` | 4 | Getting crowded |
| 7 | Freight forwarders | Quote/booking/doc clerks | ~5K US forwarders `[E]` | $50–200K | Medium | Nexcade ($6M seed, Jul-2026) `[V]`; 5U AI ($3.2M pre-seed) `[V]`; Raft ($30M B, 40% of top-25 forwarders) `[V]`; Pallet `[V]`; Cargofy | 4 | Crowded |
| 8 | Customs brokers | Entry writers; tariff chaos 2025-26 | ~2–3K brokerages `[E]` | $50–200K | Medium | Amari ($4.5M seed, 30+ firms) `[V]`; Alchemize (YC S26, AI-native brokerage) `[V]`; Nabu (€3M), Digicust (€2.3M), iCustoms ($2.2M) `[V]`; CBP Jan-2026 ruling on unlicensed AI pre-fill = regulatory risk `[V, per search summary; verify]` | 4 | Crowded + regulated |
| 9 | Commercial property mgmt / CRE operations (work orders, vendor dispatch, tenant requests) | Building engineers, PM coordinators | ~6–10K CRE PM firms `[E]` | $50–200K | Medium | Visitt ($22M B, Jan-2026, AI-native CRE ops) `[V]`; CentralComs (YC S26, residential) `[V]`; Fexa AI multi-agent FM `[V]` | 3 | Contested |
| 10 | Multi-site retail/restaurant facility management | FM coordinators, vendor chasing | ~5K multi-site operators `[E]` | $50–150K | Medium | Prefix ($7.5M seed, $2.5M ARR, 2K locations) `[V]`; ServiceChannel/Fexa incumbents | 3 | Contested |
| 11 | Waste haulers (independent) | CSRs, billing, routing | ~2–3K mid-size independents `[E]` | $30–100K | Low-med | Hauler Hero ($16M A, Feb-2026, OS + Hero Chat) `[V]` | 3 | Owned by SoR player |
| 12 | Fleet maintenance / repair coordination | Fleet managers, service writers | ~10K fleets 100+ vehicles `[E]` | $30–100K | High (telematics) | ServiceUp agentic repair platform (Jul-2026) `[V]`; Samsara Agent Studio `[V]` | 4 | Absorbed by Samsara risk |
| 13 | Manufacturers' aftermarket parts & service | Parts desks, service coordinators | ~3–5K OEMs `[E]` | $100–500K | Medium | ClearOps (€8.6M A; AGCO, Terex, Jungheinrich) `[V]`; Syncron, Aquant, Bruviti incumbents `[E]` | 4 | Enterprise-sales, crowded |
| 14 | Fire/life-safety inspection contractors | Inspection report writers, deficiency quoting, AHJ filing | ~8–12K contractors `[E]` | $20–60K | Low-med | Inspect Point (PE-backed, adding AI) `[V]`; Pyralisfire (2026, tiny) `[V]`; Probook/Netic adjacent | 2 | Interesting but ACV thin |
| 15 | Hotel groups – revenue mgmt, group sales RFPs | Revenue managers, group sales | ~3–5K mgmt cos/owners `[E]` | $20–100K | High | happyhotel (€6.5M A) `[V]`; hivr.ai (Amadeus-backed, in iVvy) `[V]`; many RMS incumbents | 4 | Crowded |
| 16 | Event venues / catering sales | Event sales managers | many small `[E]` | $5–20K | Medium | iVvy Instant Proposal / hivr `[V]`; Tripleseat etc. | 4 | Fails ACV |
| 17 | Self-storage operators | Call centers | concentrated (REITs) | $5–30K | High | StoreEase, XPS AleX, White Label, Patchwork voice agents `[V]` | 5 | Fails ACV + crowded |
| 18 | Travel management companies | Travel agents/servicing | ~2–3K TMCs `[E]` | $50–200K | High (GDS) | BizTrip ($2.5M pre-seed, Sabre-backed) `[V]`; Navan/Spotnana absorb | 3 | Platform-absorption risk |
| 19 | Ag retailers / co-ops | Agronomy sales, order desk | ~1.5–3K companies `[E]` | $50–150K | Low | Ever.Ag Everett agentic expansion (Jul-2026) `[V]`; Taranis/Syngenta `[V]` | 3 | Incumbent-led, seasonal |
| 20 | Propane / heating-oil distributors | CSRs, delivery dispatch, billing | ~4–6K retail distributors `[E]` | $20–60K | Low-med | Only generic AI receptionists (Dialzara) and Prosperous (wholesale fuel) `[V]` | 1 | Open but small; good wedge for a dealer-ops team later |
| 21 | Telecom/fiber & utility contractors (permits, closeout) | Permit coordinators, closeout packages | ~3–5K `[E]` | $50–200K | Low | PermitFlow ($54M B, general permits) `[V]`; Magnasoft services `[V]` | 3 | Gov-interface heavy |
| 22 | Architecture / engineering consultancies (proposals, PM) | Proposal coordinators; WSP says ~80% bid-headcount cut possible `[V]` | ~10–15K firms 20+ staff `[E]` | $20–80K | Medium | CivCore, Tyce, Cascade ($3.5M seed), Motif ($46M), FORMAS ($4M) `[V]`; Loopio/Responsive generic | 4 | Crowded |
| 23 | Elevator contractors / car rental & fleet leasing | — | Highly concentrated (big-4 elevator; Enterprise/Hertz/Avis) `[E]` | — | — | — | — | Fails buyer-count bar |

**Read-through:** Logistics (forwarding, customs, carriers) and staffing recruiting filled up fast in 2025-26. The remaining white space sits in **asset-heavy dealer fixed-ops** and **labor-heavy contract-services back office**, where only seed-stage teams exist. 3PL warehousing is the borderline case: open at the vertical level, but Pallet is a funded horizontal threat.

---

## 2. Top 3 theses

### Thesis 1: "The Toma/Avoca of equipment dealers": an AI fixed-ops employee for heavy-equipment, ag, and truck dealers

- **One-sentence pitch:** An AI service writer and parts counter rep that answers every customer, technician, and OEM inquiry, quotes parts from manuals plus DMS inventory, books shop time, and drafts warranty claims for equipment dealers that can't hire diesel techs or counter staff.
- **Buyer:** Dealer principal, VP Aftermarket/Product Support, or Service Manager at multi-store dealers (5–60 rooftops) for CAT/Deere/CNH/Kubota/Volvo/Komatsu/Peterbilt/Toyota-forklift. Secondary buyer: OEM dealer-network programs (Brilliant Harvest already shows this path via CNH `[V]`).
- **Buyers × ACV:** ~6,000 dealer companies `[E]` × ~$80K blended ACV (about $2–3K per rooftop per month for parts, service, and warranty agents) ≈ **$480M** core. Expanding into warranty recovery (share of recovered $), rental desk, and service-scheduling SoR takes ACV to $150–200K, or **$0.9–1.2B**. Adding EU/ANZ dealers, OEM network deals, and adjacent dealers (forklift, power-gen, marine/RV commercial) gives **>$1.5B**.
- **Penetration:** $10M ARR ≈ 120 dealer groups at $80K (~2%). $100M ARR ≈ 700 groups at $140K (~12%) or 2–3 OEM network-wide deals plus 400 direct.
- **Why now:** The $7B/yr technician-shortage loss and ~$6M per dealer `[V]`. Parts and service are 40–60% of dealer gross profit `[E]`. LLMs can now read 10K-page service manuals and parts diagrams. Voice and email agents are proven by Avoca and Toma. Dealers are consolidating (Titan, RDO, Rush, Papé) into groups with real software budgets.
- **Why not crowded:** Only seed-stage AI-natives so far: Brilliant Harvest ($4M, helpdesk/knowledge) and Chasi (YC W26, sales/rental) `[V]`. DMS vendors are slow, and auto-dealer AI (Toma etc.) doesn't cover equipment DMSs, OEM warranty portals, or machine serial/hour-meter logic.
- **90-day pilot:** One 8–15-store dealer. Days 1–30: parts-counter inbound agent (email/phone/web), with part ID from serial plus symptom, availability from DMS, and a quote. Days 31–60: service intake and scheduling, plus telematics fault-code (JDLink/VisionLink) triage into a work order. Days 61–90: warranty-claim drafting against OEM rules. KPIs: response time, parts quote→order conversion, counter headcount hours saved, warranty rejection rate and days-to-pay, billed tech hours.
- **Expansion to system of record:** Agent → own the service work-order and parts-quote workflow → warranty and fleet-PM management → replace or wrap the legacy DMS service and parts modules (VitalEdge/e-Emphasys) → customer-facing fleet portal for the dealer's customers.
- **Kill risks:** (1) OEMs (Deere, CAT) mandate their own dealer AI or block data access. (2) DMS vendors bundle "good enough" agents. (3) Brilliant Harvest raises a large A and locks in OEM channels. (4) Long dealer sales cycles and the farm-cycle downturn (ag 2025-26 softness `[E]`). Mitigation: start with construction/truck dealers, which are less OEM-locked and have heavier rental and service mix.

### Thesis 2: "The EliseAI of 3PLs": an AI account manager and billing analyst for mid-market warehouses

- **One-sentence pitch:** An AI employee that answers every brand-client email and portal ticket (inventory, orders, receiving, WISMO), captures every billable accessorial, reconciles invoices, and files carrier claims for mid-market 3PL warehouses.
- **Buyer:** COO/VP Ops or CFO at 3PLs with 2–30 warehouses and $10M–$500M revenue.
- **Buyers × ACV:** ~6,000 warehousing 3PLs `[E]` (of ~70K "3PL businesses" `[V]`) × $70K ≈ **$420M**. Adding revenue-share on recovered accessorials/claims and a client-portal/billing SoR takes ACV to $150K, or **~$900M**. EU/Canada push it to **$1B+**.
- **Penetration:** $10M ARR ≈ 140 3PLs (~2%). $100M ARR ≈ 800 3PLs at $125K (~13%).
- **Why now:** E-commerce SKU proliferation, tariff-driven inventory swings in 2025-26, and thin 3PL margins. Revenue leakage from unbilled accessorials is commonly cited at 3–8% `[E]`. Prox already shows a paid wedge in claims recovery at ShipBob `[V]`.
- **Why not crowded (honest):** The vertical-specific player is seed-stage (Prox, YC) `[V]`. The real threat is Pallet ($50M raised, General Catalyst) `[V]`, which sells horizontally across brokers, forwarders, and 3PLs and skews to freight. WMS vendors have not shipped account-manager agents at scale `[E]`. The thesis only works if it goes deep on warehouse billing logic and WMS integrations (Extensiv/3PL Central, Deposco, Logiwa, Infoplus) rather than generic logistics email.
- **90-day pilot:** One 3–6-warehouse 3PL. Weeks 1–4: client-inbox agent reading WMS, answering inventory/order/ASN questions, escalating exceptions. Weeks 5–8: billing audit of 6 months of activity vs. contracts to find unbilled accessorials (hard-dollar ROI). Weeks 9–12: carrier claims plus invoice-dispute agent. KPIs: tickets auto-resolved %, response time, $ recovered, AM headcount ratio (clients per AM).
- **Expansion to SoR:** Billing engine and rate-card management → client portal → contract/quote management for new brand onboarding → WMS-adjacent OS.
- **Kill risks:** (1) Pallet or Prox goes vertical-deep first. (2) WMS vendors bundle. (3) 3PL M&A consolidation shrinks the buyer count. (4) VCs may see it as "logistics, again" after the 22 killed theses. Score: medium crowding.

### Thesis 3: "The Avoca of contract security and facility-services firms": an AI operations desk that keeps every post covered

- **One-sentence pitch:** An AI scheduler, dispatcher, and back-office clerk for contract security and janitorial companies. It fills call-offs in minutes, onboards and license-checks new hires, reconciles hours to payroll and client invoices, and writes client incident reports.
- **Buyer:** Owner/COO or VP Operations at security firms with 100–5,000 guards (and janitorial firms of similar size); also PE-backed roll-ups.
- **Buyers × ACV:** ~5,000 security firms with 100+ guards `[E]` (of 112K security-services businesses `[V]`) plus ~5,000 janitorial/FM contractors `[E]` ≈ 10,000 buyers × $50K ≈ **$500M**. Adding payroll/billing reconciliation and per-guard pricing ($8–15 per guard per month, an Owner.com-style per-seat model) with a full WFM SoR replacement gives **$1B+**.
- **Penetration:** $10M ARR ≈ 200 firms (~2%). $100M ARR ≈ 1,500 firms at $65K (~15%).
- **Why now:** Guard turnover of 89–200%+ `[V]` means constant hiring and call-offs. Wage inflation is squeezing 3–8% margins `[E]`, and every unfilled post is a contract penalty or lost billing. Voice and SMS agents can now run 3 a.m. call-off loops end to end.
- **Why not crowded:** Only Guard Owl ($3M seed) is AI-native `[V]`. TrackTik/Trackforce and Belfry are WFM systems of record, not AI employees. Teambridge markets agents to janitorial and light industrial `[V]` but is horizontal workforce software.
- **90-day pilot:** One 300–1,500-guard regional firm. Days 1–30: 24/7 call-off agent (SMS/voice) that finds qualified, licensed, non-overtime replacements from the WFM roster. Days 31–60: applicant screening, license verification, and onboarding paperwork. Days 61–90: timesheet→payroll→invoice reconciliation and automated daily client reports. KPIs: unfilled-post hours, overtime %, time-to-fill, scheduler headcount, billing leakage.
- **Expansion to SoR:** Own scheduling → replace WFM (TrackTik/Belfry) → payroll and billing → client portal plus incident management, extending to janitorial and parking/event staffing.
- **Kill risks:** (1) Thin-margin buyers resist $50K+ ACV, so price on unfilled-post savings. (2) Market concentration at the top (Allied Universal, Securitas, GardaWorld build in-house `[E]`). (3) Trackforce or Teambridge bundle agents. (4) Armed/licensing rules vary by state. Runner-up if this fails: light-industrial staffing back office (timesheet→VMS→payroll), which has the same mechanics but more crowding.

---

## 3. Sources (from search results this session; not individually fetched)

- Equipment tech shortage $7B / $6M per dealer: https://www.constructionequipmentguide.com/aed-foundation-releases-2026-technician-shortage-research-report/72229 ; https://www.equipmentworld.com/diesel-tech-shortage-part-1-call-it-the-perfect-storm-one-thats-been-gathering-for-decades/
- Brilliant Harvest $4M seed: https://betakit.com/agtech-startup-brilliant-harvest-secures-4-million-usd-in-seed-funding/ ; https://agfundernews.com/brilliant-harvest-raises-4m-to-solve-ag-equipments-service-bottleneck-with-ai/
- Chasi (YC W26): https://www.roundfunded.com/en/yc-startup/chasi
- United Rentals Equipment Agent: https://s21.q4cdn.com/336331232/files/doc_news/United-Rentals-Introduces-AI-Powered-Equipment-Agent-2026.pdf
- Prox (YC): https://www.ycombinator.com/companies/prox
- Pallet $27M B: https://www.dcvelocity.com/technology/artificial-intelligence/tech-startup-pallet-raises-27-million-for-workflow-ai
- Cartage $3.3M: https://www.freightwaves.com/news/cartage-secures-3-3m-to-support-shippers-and-carriers-with-automation
- Ciridae $20M seed: https://pulse2.com/ciridae-raises-20-million-seed-round-led-by-accel-to-bring-ai-transformation-to-real-economy-businesses/
- 3PL counts: https://redstagfulfillment.com/how-many-3pls-are-there/ ; https://www.ibisworld.com/united-states/number-of-businesses/third-party-logistics/5504/
- Security services 112K businesses / turnover: https://www.ibisworld.com/united-states/industry/security-services/1487/ ; https://belfrysoftware.com/blog/security-guard-turnover ; https://www.asisonline.org/security-management-magazine/latest-news/today-in-security/2025/october/guard-force-turnover/
- TrackTik $45M: https://itbusiness.ca/?p=108334
- Teambridge agents: https://www.teambridge.com/product/agents/relay
- Alex $20M: https://www.staffingindustry.com/news/global-daily-news/ai-agent-provider-alex-raises-20m
- Asendia (YC S26): https://www.ycombinator.com/companies/asendia-ai
- Staffing industry size: https://www.staffingindustry.com/news/global-daily-news/largest-industrial-staffing-firms-made-315-million-more-in-2025
- DataTruck $12M A: https://seedtable.com/companies/datatruck/funding-rounds/series-a-2026-01
- Cargofy $11M A: https://itbrief.news/story/cargofy-raises-usd-11-million-for-ai-freight-agents
- Nexcade $6M: https://theloadstar.com/ls_press_release/nexcade-raises-6m-to-build-ai-agents-for-freight-forwarders/
- Amari: https://techcrunch.com/2026/02/19/this-former-big-tech-engineers-are-using-ai-to-navigate-trumps-trade-chaos/ ; https://pear.vc/amari-ai-seed/
- Alchemize (YC S26): https://ycombinator.com/companies/alchemize
- Raft $30M B (2023): https://cargonewswire.com/raft-raises-30m-in-series-b-funding-to-transform-global-supply-chain-execution-with-ai/
- Visitt $22M B: https://www.calcalistech.com/ctechnews/article/bychnr4uwg (per search summary)
- Prefix $7.5M: https://siliconangle.com/2026/04/14/prefix-raises-7-5m-scale-ai-driven-facility-management-platform
- Hauler Hero $16M A: https://techcrunch.com/2026/02/10/hauler-hero-collects-16m-for-its-ai-waste-management-software/
- ServiceUp: https://collisionweek.com/2026/07/21/serviceup-launches-agentic-ai-platform-automate-fleet-vehicle-repair/
- ClearOps €8.6M A: https://www.munich-startup.de/en/news/clearops-raises-e8-6-million
- happyhotel €6.5M A: https://www.phocuswire.com/german-rms-happyhotel-series-a-round
- iVvy/hivr: https://meetings.skift.com/2026/01/23/ivvy-ai-venue-proposals/
- BizTrip: https://www.phocuswire.com/biztrip-ai-1-5-million-dollars-pre-seed-funding
- Ever.Ag: https://www.global-agriculture.com/global-agriculture/ever-ag-advances-everett-its-ag-decision-engine-to-agribusiness/
- Cascade: https://tech.eu/2026/07/21/ai-engineering-project-predictor-startup-cascade-wins-35m-seed-investment/
- Guard Owl $3M: https://www.unite.ai/ai-security-monitoring-job-recruitment-companies-raise-funds/ (per search summary)

**Unverified / to check next:** dealer company counts (AED/EDA/ATD membership), Teambridge and Belfry funding, Probook $34M A (seen only in a newsletter summary), the CBP Jan-2026 AI pre-fill ruling, and propane distributor count.
