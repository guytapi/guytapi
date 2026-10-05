# Thesis S: "We get your new facility powered 12-24 months faster"

**Analyst stance:** red team, trying to kill the thesis. **Date:** 2026-10-05. **Searches used:** 34 of 40 (WebFetch not used).
**Sourcing:** every URL below came back in search results. Figures come from search snippets. **[UNVERIFIED]** marks a figure I could not cross-check, or one that may be garbled in the snippet. **[EST]** marks my own estimate.
**Builds on:** `round4/electricity_shock.md` (Thesis A, speed to power, scored 7.1 there).

---

## 0. TL;DR

- **The pain is real.** PG&E industrial projects wait up to 18 months, and some Bay Area sites face 5-8 years. A new PG&E substation can take up to about 3,242 days. Fleet depots routinely wait 18-36 months. In the Netherlands, 14,044 offtake requests (9 GW) sit on distribution-operator waiting lists, plus 212 requests (38 GW) at TenneT, and parts of the country won't be fixed until 2033-2035.
- **The thesis dies on volume and value capture.**
  - PG&E's flagship Flex Connect program has **5 enrolled customers, 7 projects ever energized, and about 85 sites in the pipeline after roughly 2 years**. That is 11 MW managed, with another 38 MW in the pipeline.
  - ComEd's program targets about **50 MW a year**.
  - At 2-5 MW per site, that means the whole US flexible-connection market is **on the order of 100-300 sites a year in 2026-27** [EST]. That isn't enough for a venture-scale software company on its own.
- **The utility builds or buys the brain.**
  - The operating envelope (the hourly limit the site must stay under) is computed by the utility's own grid-management software (DERMS): PG&E's own system, Camus FlexConnect, or Itron working with The Mobility House.
  - The customer side only needs a controller that obeys the limit, and charger and battery vendors already ship one (Kempower, Heliox, PowerFlex, which now owns The Mobility House North America).
  - Xcel's Capacity*Connect is **200 MW of utility-owned batteries**, so the utility is literally doing it itself.
- **The demand driver weakened.** California repealed the Advanced Clean Fleets rule for high-priority and drayage fleets (effective 2026-09-10), and EPA is rolling back the federal truck greenhouse-gas standards. Electric-truck depots, the largest pool of flexible-connection customers, are slowing.
- **The Netherlands has the volume but is crowded and cheap.** Tibo Energy (€6M; a simulator plus a real-time energy management system for congestion) is essentially this product already, alongside Eddy Grid (€7.5M), Spectral, Sympower, Zympler, Currentt and ACC. Many waitlisted firms are SMEs, so contracts are small. The grid operators set the contract terms, and the subsidy runs through batteries (Flex-E covers up to 40%).
- **The closest venture-backed player already exists:** Critical Loop ($26M Series A, $49M total). It is cited in the CPUC decision and won Terawatt 4+ MW of flexible capacity "in a few months".
- **VERDICT: KILL as a standalone venture thesis.** Keep two pieces: (a) the flexible-connection application engine as a feature or wedge inside a broader operating system for new sites, and (b) the Netherlands data point as evidence that congestion pain can scale. Neither justifies a company today.

---

## 1. How long are the waits for loads that aren't data centers, and what does delay cost?

| Region / utility | Load type | Wait (evidence) | Source |
|---|---|---|---|
| PG&E (N. California) | Industrial / warehouse / R&D | Up to 18 months typical; some sites face **5-8 years**; delays cause "multimillion-dollar losses" | [Bisnow San Jose](https://www.bisnow.com/news/san-jose/industrial/industrial-developers-say-pge-delays-are-hurting-their-bottom-line-119044) |
| PG&E published timelines | Commercial service line vs. new substation | Average **182 days** for a service line; up to **3,242 days** (~9 years) for a new substation | [TestFit](https://www.testfit.io/blog/how-fleet-electrification-rewrote-industrial-feasibility) |
| S./Central California (SCE etc.) | Warehouses | One project stalled **14 months** | [Bisnow LA](https://www.bisnow.com/news/los-angeles/industrial/electricity-availability-to-warehouse-projects-in-southern-central-california-presenting-hurdles-for-developers-117942) |
| US/EU fleet depots | Electric trucks and vans | **18-36 months** is "far from unusual"; some report up to 10-year waits; large fleet plans take 3-5 years | [trans.info](https://trans.info/en/electric-trucking-2026-460158), [ACEEE](https://www.aceee.org/fleet-electrification) |
| US manufacturing | New plants / expansions | "Multiple years" to energize large new load; manufacturers compete with data centers | [Manufacturing Dive (sponsored)](https://www.manufacturingdive.com/spons/building-manufacturing-capacity-when-the-grid-cant-keep-up/814394), [Bloom blog (vendor)](https://www.bloomenergy.com/blog/why-power-now-leads-the-manufacturing-growth-plan/) |
| Netherlands | All business offtake | 14,044 DSO requests (9 GW) plus 212 TenneT requests (38 GW); ACM backlog of 22,600 connections (14,000 offtake). The Hague area waits until **2033**; expansions done ~**2035**. Some municipalities put **all** new connections on a waitlist from 2026-07-01 | [Enlit](https://www.enlit.world/library/netherlands-to-appoint-flexibility-coordinator-as-grid-bottlenecks-recur), [Zoetermeer](https://en.zoetermeer.nl/wachtlijst-vanaf-1-juli-2026-voor-alle-aanvragen-stroomaansluitingen), [Stedin](https://www.stedingroep.nl/eng/press-and-media/persberichten/growing-pressure-on-the-electricity-grid-is-now-affecting-households-too) |
| Netherlands (Stedin) | Large consumers | 1,100 large consumers waitlisted. Companies that want **5+ EV chargers** can no longer be connected | [Stedin](https://www.stedingroep.nl/eng/press-and-media/persberichten/growing-pressure-on-the-electricity-grid-is-now-affecting-households-too) |
| Germany | Retail / commercial | Connections take up to **18 months** (HDE) | [Clean Energy Wire / DIHK](https://www.dihk.de/en/newsroom/-connection-processes-must-become-faster-digital-and-less-bureaucratic--172586) |
| UK | Demand connections | Queue reform underway: flexible, non-firm and phased connections (Ofgem "Connect" update, June 2026) | [HSF Kramer](https://www.hsfkramer.com/insights/2026-07/uk-grid-connections-reform), [Gowling](https://gowlingwlg.com/insights-resources/articles/2026/ofgem-demand-connection-queue-reform) |

**Cost of delay per site [EST]:**
- **Warehouse:** about 250k sq ft at the US average rent of $8.87/sq ft ([CRE Daily](https://www.credaily.com/briefs/warehouse-real-estate-trends-signal-market-rebalance-in-2026/)) is ~$2.2M/yr, or ~$185k per month of delay.
  - **But big-box vacancy is 10.2%** (up from ~3% in 2022). Many speculative warehouses have no tenant waiting, so a month of delay often costs little more than carrying cost.
  - An ambient warehouse draws only ~0.4 MW and usually isn't power-constrained. The constraint bites when the tenant electrifies (EV yard, cold storage).
- **Fleet depot:** stranded electric trucks at ~$250-400k each. A 50-truck depot idle for 12 months strands ~$15M of capex plus diesel costs. But with the mandates repealed, fleets now simply **delay buying trucks**. Delay costs them little, which kills the urgency.
- **Factory line:** foregone gross margin can be $1M+ per month. This is the strongest value case, but the volume is low, every project is bespoke, and many plants have 24/7 loads that can't flex.
- **Netherlands:** ABN AMRO estimates Dutch grid delays cost "up to €376M a year" (carbon cost of renewables in the queue, not business losses) ([ABN AMRO](https://abnamro.com/research/en/our-research/esg-economist-dutch-grid-delays-cost-up-to-eur-376-million-every-year)). A figure of "€40B/yr congestion cost" appears in one article ([EnergyGlobal](https://www.energyglobal.com/special-reports/15072026/global-grid-congestion-lessons-to-be-learned-from-the-netherlands/)) **[UNVERIFIED; likely garbled]**. Two in three organizations call the full grid an obstacle ([Solar Magazine](https://solarmagazine.nl/nieuws-zonne-energie/i44166/2-op-3-organisaties-ervaart-vol-stroomnet-als-belemmering)).

---

## 2. Flexible-connection tariffs and pilots (2026)

| Jurisdiction | Mechanism | Status / scale | Implication |
|---|---|---|---|
| **PG&E** | Flex Connect: the DERMS sends day-ahead hourly limits | 5 enrolled, 7 energized, 2 already moved to firm service, ~85 in pipeline, 10 large-load applications in 2026. Full capacity in **90% of hours**; loads affected <1% of the time; ~**1.5 years** earlier energization. 11 MW managed, 38 MW pipeline | Proven but **tiny**. The utility runs the brain ([mgrid](https://mgrid.org/2026/09/02/pge-counts-5-flex-connect-customers-and-85-in-the-pipeline-with-full-capacity-in-90-percent-of-hours/), [Utility Dive](https://www.utilitydive.com/news/pge-sees-rising-interest-in-customer-driven-flexible-interconnection-pil/829447/), [Microgrid Knowledge](https://www.microgridknowledge.com/distributed-energy/article/55298646/flexible-interconnection-programs-from-utilities-on-the-rise-saving-time-and-money-for-microgrid-and-der-developers)) |
| **PG&E + SCE** | CPUC D.26-02-025 Standard Offer Flexible Service Connection (a tariff) | Implementation advice letters filed 2026-04-13; report on cost-efficiency due 2029-01-15 | Standardized tariff, so **less bespoke engineering for anyone to sell** ([CPUC filing](https://docs.cpuc.ca.gov/PublishedDocs/Efile/G000/M596/K142/596142999.PDF), [CalRegulatory](https://www.calregulatory.com/february-5-2026-cpuc-voting-meeting-results-commission-clears-path-for-immediate-energization-under-new-flexible-service-connection-rules/), [ZEG blog](https://www.zeroemissiongrid.com/zeg-blog/cpuc-decision-2025/)) |
| **ComEd** | Flexible interconnection, now a full program rather than a pilot | ~50 MW in 2026, then ~50 MW/yr, ~240 MW cumulative by 2027 **[figure partly truncated in snippet]** | Second real US market, but still small ([Microgrid Knowledge](https://www.microgridknowledge.com/distributed-energy/article/55298646/flexible-interconnection-programs-from-utilities-on-the-rise-saving-time-and-money-for-microgrid-and-der-developers)) |
| **Xcel (MN)** | Capacity*Connect: **200 MW of utility-owned distribution batteries** (approved 2026-04-02) | Utility solves the constraint itself | **Kill signal: utility builds it** ([Fresh Energy](https://fresh-energy.org/xcel-energys-new-capacityconnect-program-is-a-positive-step-toward-building-the-grid-of-the-future)) |
| **National Grid (MA)** | Local Power Controller pilot (behind-the-meter, net-zero thermal impact) | Pilot | Small |
| Duke, Dominion, ConEd | No dedicated C&I flexible-load tariff found | Camus is demonstrating FlexConnect to Duke, Edison and PG&E | Not yet a market ([Camus Q&A](https://www.renewableenergyworld.com/power-grid/smart-grids/flexible-interconnection-promises-speed-to-power-for-utilities-data-center-developers-qa-with-camus-energy/)) |
| ERCOT / Texas | Large-load rules (SB6) aimed at 75 MW+ loads; controllable load resources | Data-center scale, not mid-size C&I | Not relevant to the core segment |
| **Netherlands** | Capacity restriction contracts (2022); non-firm transport agreements (ACM, 2024-01-31); **TenneT time-dependent transport rights** (live 2025-10-01; 85% guaranteed, ≤15% curtailed with day-ahead notice; 9 GW identified); **group transport agreements for energy hubs** (first in N. Brabant, 2026-07-09); **Liander FlexPlus Battery**; RVO Flex-E subsidy (up to 40%); each operator holds ≥1 regional flexibility tender in 2026 | **Most mature flexible-connection toolbox in the world** | Real volume, but the tools are standardized contracts run by grid operators ([TenneT](https://www.tennet.eu/nl-en/time-dependent-transport-rights-tdtr), [Fieldfisher](https://www.fieldfisher.com/en/insights/introduction-of-alternative-transport-rights-in-the-netherlands), [Brainport](https://brainporteindhoven.com/en/nieuws/north-brabants-first-group-transmission-agreement-marks-a-new-step-in-tackling-grid-congestion), [Solar Magazine (FlexPlus)](https://solarmagazine.nl/nieuws-zonne-energie/i44673/bedrijven-kunnen-wachtlijst-omzeilen-door-batterij-te-delen-met-stroomnet), [Stibbe](https://www.stibbe.com/publications-and-insights/parliamentary-letter-on-grid-congestion-eight-measures-for-better)) |
| **Germany** | Flexible connection agreements (§8a EEG / EnWG) now the norm for 2026; §14a covers small controllable devices | Mainly generation and storage; for C&I offtake still early | Second EU market ([Bird & Bird](https://www.twobirds.com/en/insights/2025/germany/flexibler-flaschenhals-chancen-und-risiken-der-neuen-regelungen-zu-flexiblen-netzanschlussvereinbaru), [pv magazine](https://www.pv-magazine.com/2026/02/26/germanys-battery-sector-calls-for-faster-grid-connections-amid-backlog/)) |
| **UK** | Ofgem/DESNZ demand-connection reform (Curate / Plan / Connect) with flexible, non-firm and phased connections; UKPN has offered timed connections for bus garages; £170M depot-charging fund (2026-30) | In progress | Possible later market ([gov.uk](https://www.gov.uk/government/publications/connecting-electric-vehicle-chargepoints-to-the-electricity-network/connecting-electric-vehicle-chargepoints-to-the-electricity-network)) |

**Is the Netherlands a better beachhead?**
- **Volume: yes.** About 14,000 businesses wait for offtake, against hundreds in the US.
- **Venture fit: no**, for four reasons:
  1. The Netherlands already has 6+ funded congestion-energy-management startups, and Tibo explicitly pairs a simulator with real-time control, which is the same product.
  2. Many waitlisted firms are SMEs. Their realistic ACV is €5-30k, and batteries capture most of the spend.
  3. The grid operators control the contract types (non-firm, time-dependent, group agreements) and set the terms. Your "engineering package" mostly fills in a standardized form.
  4. Utrecht, Amsterdam or Eindhoven teams with local relationships beat a US entrant on distribution.

---

## 3. Competitors

| Company | What it does | Funding / status (as reported) | Overlap with Thesis S |
|---|---|---|---|
| **Emerald AI** | Compute flexibility so data centers connect faster (Conductor) | $150M Series A at $1.05B; ~$220M total | Data centers only. It validates the category, not the C&I segment ([DCVC](https://www.dcvc.com/news-insights/dcvc-co-leads-emerald-ais-150-million-series-a-round-to-transform-data-centers-into-intelligent-grid-responsive-assets), [MIT Tech Review](https://www.technologyreview.com/2026/06/16/1138591/data-center-online-quickly-electric-grid-flex/)) |
| **Critical Loop** | Modular batteries plus software; flexible service agreements; bridging power | $26M Series A, $49M total equity and debt. Cited in the CPUC flexible-connection rulemaking. Terawatt got 4+ MW across 2 sites "in a few months" | **Direct, and ahead of us** ([pulse2](https://pulse2.com/critical-loop-26-million-series-a-to-accelerate-grid-interconnection-and-industrial-power-deployment/), [beinsure](https://beinsure.com/news/critical-loop-raises-26mn-to-cut-grid-connection/)) |
| **Camus Energy** | Utility-side FlexConnect (hourly operating envelopes); claims connections 3-5 years sooner | $26M Series A total (2024); Google for Startups accelerator 2026; demos with Duke, Edison and PG&E | Owns the utility side. Customers don't need a separate envelope engine ([Camus Q&A](https://www.renewableenergyworld.com/power-grid/smart-grids/flexible-interconnection-promises-speed-to-power-for-utilities-data-center-developers-qa-with-camus-energy/)) |
| **Itron + The Mobility House** | FIX (Fast & Flexible Interconnect) for EV fleets | Itron is public | Direct for depots ([Itron](https://investors.itron.com/node/23606)) |
| **PowerFlex** (EDF) + The Mobility House NA | Fleet charging and energy management; 100 MW of fleet charging under management | Acquisition announced 2026-08-06; Manulife $100M (2022) | Owns the depot controller ([BusinessWire](https://secure.businesswire.com/news/home/20260806539006/en/PowerFlex-and-The-Mobility-House-North-America-Combine-to-Create-North-Americas-Leading-Fleet-Charging-and-Energy-Management-Platform)) |
| Kempower, Heliox (Siemens) | Charger OEMs with built-in dynamic load management | Public / corporate | The site limit is a feature of the hardware ([Kempower](https://kempower.com/?p=2166)) |
| Voltus | VPP / "bring your own capacity" (Google, 100 MW in PJM; Octopus and Sunrun partnerships) | ~$600M valuation **[UNVERIFIED]** | Data-center capacity, not C&I sites ([Latitude](https://www.latitudemedia.com/news/google-is-voltus-first-bring-your-own-capacity-customer/)) |
| Terawatt, Zeem ($50M ArcLight), Voltera, Electrada | Powered depots / charging-as-a-service | Infrastructure-funded | They absorb the interconnection problem for fleets ([FleetOwner](https://www.fleetowner.com/emissions-efficiency/article/21245967/ev-fleet-as-a-service-provider-secures-50m-for-expansion)) |
| Scale Microgrids (EQT), Enchanted Rock, Bloom | Onsite and bridging power | Big infrastructure capital; Bloom revenue $2.02B (FY25) | Bridging is capital-heavy. Customers buy power, not software |
| **Tibo Energy** (NL) | Energy system simulator plus real-time EMS for congestion | €6M seed (KOMPAS, Hitachi Ventures, SET, Speedinvest); expanding to DE and BE | **Same product, in the best geography** ([tech.eu](https://tech.eu/2025/06/30/tibo-energy-raises-eur6m-to-scale-ai-energy-management-platform/)) |
| Eddy Grid (NL) | Battery and asset optimizer; 500 MW under management | €7.5M (May 2026) | Adjacent ([ioplus](https://ioplus.nl/en/posts/energy-asset-optimizer-eddy-grid-lands-75-million-)) |
| Spectral (BRIGHTER), Sympower, ACC (energy-hub software), Zympler (€1.5M), Currentt (€1.7M), simpl.energy, Withthegrid | NL congestion and energy-hub tools | Seed stage | Crowded seed field ([startuphub](https://www.startuphub.ai/news/zympler-secures-e1-5m-seed-funding-for-grid-congestion-solutions), [siliconcanals](https://siliconcanals.com/currentt-secures-e1-7m/), [withthegrid/ACC](https://withthegrid.com/teleport/partners/acc/)) |
| Paces | Siting / grid-capacity data | $11M Series A | Adjacent: the pre-site layer ([BuiltWorlds](https://builtworlds.com/news/cleantech-platform-startup-paces-raises-11m-to-scale-energy-project-development/)) |
| Build.inc, Pearl Street, GridBeyond, Nuvve, Fermata, ev.energy, Synop, WeaveGrid, Jedlix, Dexter, Scholt, Equans, GridPoint | Various | Not re-verified this round | Low to medium |

---

## 4. Buyers, volume, ACV and sales cycle

- **Buyers:**
  - Fleet electrification leads at parcel, beverage, school-bus and transit fleets.
  - CPO and depot developers (Terawatt, Zeem, Voltera): **the best buyer, but they increasingly build this in-house or partner with Critical Loop**.
  - Industrial developers' development and construction VPs.
  - Plant engineering for expansions.
- **US project count [EST]:**
  - PG&E: 85 in the pipeline after 2 years.
  - ComEd: ~50 MW/yr, i.e. ~10-25 sites.
  - SCE Standard Offer: maybe 30-80 a year.
  - Total: **~100-300 US flexible-connection projects a year** through 2027.
  - Even if "constrained sites that could use flex" were 10x that, the utility must offer a program, and most don't.
- **EU count [EST]:** NL has ~14,000 waitlisted offtake requests. Perhaps 2-4k are firms above 1 MW with flexible assets. DE and UK are emerging.
- **ACV per site [EST]:**
  - US: study plus application, $30-80k one-off, and $20-60k/yr for the controller. Customers will compare this to the free load management bundled with the chargers.
  - NL: €10-40k/yr.
- **Sales cycle:** 6-18 months, tied to the project schedule. The utility review takes months.
- **90-day pilot?**
  - A feasibility study plus a filed application in 90 days is feasible.
  - Getting energized and proving the time saved is not; that runs on the utility's clock.
  - In NL, a 90-day energy-management deployment behind an existing connection is feasible, which is what Tibo sells.

---

## 5. Moat

- **Utility relationships:** real, but each one is bespoke, which means services work. Standardization (the CPUC Standard Offer, ACM contract types) erodes the moat for everyone.
- **Load-flex performance data:** the utility holds the grid-side data. Charger OEMs and CPOs hold the load-side data.
- **Engineering automation:** you could automate the load modeling and the application, but that is a feature, cheap to copy, and the volume is low.
- **Network across utilities:** only valuable if 20+ utilities run programs, and there are ~4 in the US today.
- **Verdict:** weak (3/10).

---

## 6. Market math [EST]

| ARR target | US-only route | US + NL/EU route | Plausibility |
|---|---|---|---|
| **$10M** | ~150 sites at $65k blended. That is roughly **50-100% of all US flex-connection projects** for 1-2 years | ~80 US sites + ~300 NL/DE sites at €20k | Hard, but possible by 2029 if CA and IL scale and 2-3 more states adopt |
| **$50M** | Needs ~750 US sites/yr with recurring revenue; requires ~15+ utilities with tariffs | 1,500+ EU sites, against Tibo and others | Unlikely before 2030 |
| **$100M** | Requires flexible connection as the **default** US path for all C&I, plus expansion into whole-site energy management, demand response and tag management | Pan-EU | Only if it becomes a general site energy operating system, which is a different, more crowded company |

**Expansion paths:** after energization, the site's flexibility moves into demand response and capacity-tag revenue (Thesis B), plus battery dispatch. That is the crowded aggregator and energy-management space covered in the prior report.

---

## 7. Kill signals: status

| Kill signal | Status |
|---|---|
| Utility-by-utility bespoke work turns into services | **CONFIRMED**: few programs, each different. Standardization helps the utility, not the vendor |
| Low project volume | **CONFIRMED**: PG&E has 5 enrolled and 7 energized in ~2 years; ComEd ~50 MW/yr |
| Hardware- or financing-heavy | **CONFIRMED** for bridging: Critical Loop, Scale and Bloom win with capital. Software alone doesn't create flexibility |
| Utilities building it themselves | **CONFIRMED**: PG&E DERMS, Xcel's 200 MW of utility batteries, Camus/Itron sold to utilities |
| Demand driver shrinking | **NEW**: ACF repeal (2026-09-10) and the EPA rollback slow electric-truck depots, the main customer pool |
| Incumbent controllers | PowerFlex + The Mobility House, Kempower and Heliox include site-limit management |

---

## 8. Sharpened thesis (best surviving version)

> "**Flex-connection engine for CPOs and depot/industrial developers**: given a site and a utility, auto-generate the load model, the flexible-connection application (PG&E/SCE Standard Offer, ComEd, NL non-firm/time-dependent/group agreements), and a certified controller that obeys the utility's envelope across any brand of charger, battery or HVAC."

- **Sold to:** CPOs and developers with 20+ sites a year (repeat pipelines; PG&E notes "repeat customer interest").
- **Problem:** that is maybe 20-50 buyers in the US. It works better as a feature for Critical Loop, PowerFlex or Camus, or as an acqui-hire, than as a $1B company.

---

## 9. Cold message and simulated reaction

**To:** VP Infrastructure, a depot developer / CPO (Terawatt / Zeem / Voltera type)
> Subject: Energize your stuck CA/IL depots ~18 months sooner
> PG&E reports flex-connected sites get full capacity 90% of hours and energize ~1.5 years early, but only 7 projects have done it. We automate the flexible-connection package (load model + SCE/PG&E Standard Offer filing) and run a brand-agnostic controller that holds your site under the utility's envelope. 30-min call to run 3 of your stuck sites through it?

**Simulated reaction:** "We already did this with PG&E and Critical Loop. Our chargers' energy-management system handles the limit. The hard part is the utility engineer's calendar, not the paperwork. If you can get SCE to respond faster, call me. Otherwise, no." **Outcome: polite NO, or 'send a one-pager'.**

---

## 10. Five simulated buyers

| Buyer | Situation | Response | Why |
|---|---|---|---|
| Fleet electrification lead, beverage distributor (CA) | 3 depots on PG&E | **NO** | ACF repeal, so they slowed truck orders. PepsiCo-style projects are already done with PG&E directly |
| VP Development, industrial REIT (Bay Area) | Speculative warehouses waiting on PG&E | **MAYBE** | Pain is real (5-8-year cases), but a speculative warehouse has no flexible load to offer. Would pay for a study, not SaaS |
| Plant engineering director, manufacturer expanding a line (IL, ComEd) | 6 MW expansion; 2028 energization quoted | **MAYBE** | Would consider the ComEd flex program if part of the load can shift. Process load is mostly firm. Wants it from the EPC or utility, not a startup |
| CPO / depot developer (Terawatt-type) | Pipeline of 20 sites | **NO / partner** | Has done it in-house or with Critical Loop; controller comes from the charger vendor |
| Dutch logistics firm, 2 MW on the Stedin waitlist | Wants e-trucks and a cooling expansion | **YES (small ticket)** | Would buy a battery plus energy management plus a non-firm or group-agreement filing. Budget ~€15-30k/yr software. Already pitched by Tibo, Joulz and battery vendors |

Tally: 1 YES (small), 2 MAYBE, 2 NO.

---

## 11. Scores (1-10)

| Criterion | Score | Note |
|---|---|---|
| Pain | 7 | Real and multi-year in CA and NL; diluted by speculative-warehouse vacancy and the fleet slowdown |
| Urgency | 5 | Mandate repeal lets fleets wait; factories are urgent but rare |
| ROI clarity | 7 | "Months earlier" is easy to value when there's a tenant or production waiting |
| Customer accessibility | 4 | Project-driven, scattered buyers; CPOs build in-house |
| Pilot speed | 3 | Energization runs on the utility's clock |
| Market size | 3 | ~100-300 US flex-connect projects a year; NL has volume at low ACV |
| Expansion | 5 | Into demand response / tag management / energy management, which is crowded |
| Venture potential | 3 | Feature-sized unless utilities adopt flexible connection universally |
| Defensibility | 3 | Standardized tariffs, utility-owned envelopes, OEM controllers |
| Why now | 7 | CPUC Standard Offer, ComEd program, NL time-dependent/group agreements; offset by the ACF repeal |
| Competition position | 3 | Critical Loop, Camus, Itron/TMH, PowerFlex, Tibo |
| **Average** | **4.5** | Down from 7.1 in the prior scan |

---

## 12. VERDICT: **KILL** (as a standalone company)

- **Why:** the evidence confirms the pain but kills the business.
  - Flexible-connection volume is tiny: PG&E has 5 enrolled and 7 energized in about two years.
  - Utilities own the envelope software or simply build batteries.
  - Charger and battery vendors own the controller.
  - Critical Loop already holds the venture-backed slot.
  - Mandate repeal removed the main demand driver.
  - The Netherlands has the volume but a crowded field of local energy-management startups and small contracts.
- **Salvage:**
  1. Track SCE/PG&E Standard Offer uptake (biannual reports) and any PJM-utility flexible-load tariffs. Revisit if US flex-connect volume exceeds ~1,000 sites a year.
  2. If the team is EU-based, the best adjacent bet is a **congestion operating system for Dutch and German industrial parks / energy hubs (group transport agreements)**, but only with a clear edge over Tibo.
  3. Otherwise, fold the "flex-connection package" into another thesis as a feature.
