# Round 4: The AI-Data-Center Electricity Shock for Every Other Business

**Analyst stance:** skeptical. **Date:** 2026-10-05. **Search budget used:** 34 of 35 web searches (WebFetch not used).
**Sourcing:** every URL below came back in search results. Numbers come from search-result snippets. **[UNVERIFIED]** marks figures I could not cross-check, or that look like the search engine mixed up two events. **[EST]** marks my own estimates.

---

## 0. TL;DR

- **The pain is real and documented.** PJM capacity has cleared at the cap three auctions running: $329.17 (26/27), $333.44 (27/28) and $325 (28/29). Without the cap the last two would have cleared at $529.80 and $555. PJM plans to keep a collar of about $175-$325 through 2029/30, so the shock is now **structural through at least mid-2030**. The MISO 2025/26 summer price was $666.50/MW-day, 22x the year before.
- **What it does to bills:** commercial prices rose year over year to July 2026 in DC (+20.8%), Ohio (+20.3%), Virginia (+20.0%), Maryland (+18.8%) and Pennsylvania (+15.8%). The national figure was +5.9%. Named manufacturers are hurting: Belden Brick's monthly capacity charge went from $1,600 to $12,000, and Plaskolite's annual capacity charges went from $0.2M to $1.2M.
- **But the obvious company already exists, many times over.** "We cut your capacity tag / 5CP / 4CP / demand charge" is a 15-year-old product category. It's sold by Enel X (formerly EnerNOC), CPower, Voltus, GridBeyond, Vistra, Constellation, NRG and dozens of brokers, and peak alerts are often free with a supply contract. Software alone doesn't create flexibility. You still need load that can be curtailed, or a battery.
- **The less crowded angle is "speed to power" for loads that aren't data centers:** fleet depots, warehouses and factory expansions. Emerald AI ($1.05B valuation) is doing this for data centers. For C&I sites it's being done mostly by hardware-heavy players (Critical Loop, Scale Microgrids, Electrada). A software-first orchestrator there is plausible, but every deal is gated by the local utility.
- **VERDICT: REFRAME.** Kill the generic "AI cuts your bill 20%" pitch. Keep exploring (a) a speed-to-power OS for new C&I loads, which needs validation, and (b) an autonomous capacity-tag autopilot as a vertical wedge in cold storage, which would expand into (a).

---

## 1. How big is the cost shock?

### 1.1 Capacity prices

| Market | 2024/25 | 2025/26 | 2026/27 | 2027/28 | 2028/29 | Notes |
|---|---|---|---|---|---|---|
| PJM RTO ($/MW-day) | 28.92 | 269.92 | 329.17 (cap) | 333.44 (cap; uncapped 529.80) | 325 (cap; uncapped ~555) | 27/28 was the first time the whole RTO fell short of its reliability requirement (by 6,623 MW). 28/29 was short by 6.8 GW. 28/29 total cost was **$16.4B**, about $6.3B of it tied to data centers |
| MISO ($/MW-day) | ~30 summer / ~21 annualized | **666.50 summer**, ~217 annualized | not retrieved | | | New sloping demand curve; surplus fell from 6.5 GW to 2.6 GW |
| ERCOT | no capacity market | 4CP transmission charge, ~$47.53/kW-yr (Oncor, 4/2025); $65k-$110k/MW-yr depending on location | **PUCT proposal (July 2026) replaces 4CP with 12CP using 30-min intervals**; rules due by 12/31/2026 under SB6 | | | Classic 4CP avoidance becomes less valuable and harder to game |

- The **PJM collar is extended** to 28/29 and 29/30 (ceiling about $325, floor about $175). All 13 governors, the White House NEDC and DOE back it, along with a reliability backstop procurement for data-center supply. So capacity costs stay far above the 2024/25 level until at least mid-2030. That's good for the thesis: the "why now" lasts. It also means the price is politically capped, so it won't spike further.
- Sources: [renewableenergyworld](https://www.renewableenergyworld.com/power-grid/pjm-capacity-auction-hits-price-cap-again-as-region-falls-short-of-reliability-target), [PJM 27/28 release](https://www.pjm.com/-/media/DotCom/about-pjm/newsroom/2025-releases/20251217-pjm-auction-procures-134479-mw-of-generation-resources.pdf), [PJM 28/29 release](https://www.pjm.com/-/media/DotCom/about-pjm/newsroom/2026-releases/20260714-pjm-capacity-auction-procures-138318-mw-of-generation-resources.pdf), [OPIS 28/29](https://www.opis.com/resources/energy-market-news-from-opis/pjms-2028-2029-capacity-auction-clears-at-price-cap-for-third-time/), [PJM collar board decision](https://www.pjm.com/-/media/DotCom/about-pjm/who-we-are/public-disclosures/2026/20260212-board-decision-on-price-collar-for-2028-2029-and-2029-2030-capacity-auctions.pdf), [PJM Inside Lines](https://insidelines.pjm.com/pjm-files-price-collar-expedited-interconnection-as-part-of-large-load-plan/), [Enel MISO 2025](https://www.enelnorthamerica.com/insights/blogs/miso-2025-capacity-auction-results), [Voltus MISO PRA](https://www.voltus.co/blog/miso-2025-pra), [K&L Gates on the PUCT draft](https://www.klgates.com/Request-for-Comments-on-Texas-PUCT-Draft-Report-Regarding-Transmission-Cost-Recovery-in-the-ERCOT-Region-3-30-2026), [PUCT Project 58000 (ERCOT)](https://www.ercot.com/files/docs/2026/07/23/PUCT-Project-58000-pfp_adopted-9-July-2026.pdf), [Vistra 4CP](https://commercial.vistracorp.com/resources/4-coincident-peak/), [Convergent ERCOT](https://resources.convergentep.com/industrial-facilities-plan-for-ercot-price-hikes-with-battery-storage).

### 1.2 Retail C&I prices (EIA-derived, 12 months to July 2026, YoY)
- US commercial average **13.85 c/kWh, +5.9%**. Prices rose in 46 of 51 jurisdictions.
- DC +20.8%, OH +20.3%, VA +20.0%, MD +18.8%, PA +15.8%, ME +12.9%, WA +11.4%, IL +10.3%, NY +10.2%, NJ +10.1%. PJM states lead the list.
- Industrial prices were reported up 31% in PA and 26% in OH by late 2025.
- Sources: [startbusinessbystate (EIA analysis)](https://startbusinessbystate.com/data-center-electricity-prices-by-state/), [newsbytes](https://www.newsbytesapp.com/news/business/manufacturers-face-higher-electricity-bills-as-ai-data-centers-expand/tldr).

### 1.3 How the charges are allocated (the levers software can pull)
- **PJM capacity uses PLC / "capacity tag".** Each customer is charged on its average load during PJM's **5 coincident peak hours (5CP)** of the prior June-September, times a loss factor. The tag sets the capacity charge for the whole next delivery year. Capacity is about **15-30% of a C&I bill** (roughly 25% is the common figure). Transmission uses a separate 1CP Network Service Peak Load (NSPL) in most PJM zones. ([GRESB primer](https://www.gresb.com/peak-load-management-primer/), [NIH 5CP technical bulletin, May 2026](https://orf.od.nih.gov/TechnicalResources/Documents/Technical%20Bulletins/26TB/PJM%20Five%20Coincident%20Peaks%20%285CP%29%20and%20Capacity%20Charges%20-%20A%20Data%20Science%20Approach%20-%20May%202026%20TB_508.pdf), [Calmac](https://www.calmac.com/the-13-billion-a-year-mystery-an-in-depth-understanding-of-pjm’s-demand-charges))
- **ERCOT transmission uses 4CP**: the 4 summer 15-minute peaks, which 95% of the time fall on weekdays 4-5pm. This is moving to **12CP with 30-minute intervals**, so more events and less concentrated value per event.
- **MISO and NYISO** capacity is passed through by retailers and utilities, based on the customer's peak contribution.
- **Utility demand charges ($/kW of monthly non-coincident peak)** apply everywhere. They make up 30-50% of a cold-storage bill ([Envigilance](https://envigilance.com/blog/cold-storage-demand-charges/)).
- **Key skeptic note:** in deregulated PJM, many C&I customers on fixed-price supply contracts only see the capacity hit at renewal, or as a "capacity pass-through" line item. So the pain shows up in waves as contracts roll over. That works as a sales trigger, but it's lumpy.

### 1.4 What it costs typical facilities ([EST]; PJM, capacity line only)
At $329/MW-day, 1 MW of PLC costs about **$120k/yr**, against about $10.6k at $28.92. That's an increase of roughly $110k per MW of tag ([mgrid](https://mgrid.org/2024/07/26/pjm-capacity-price-surge-forces-industrial-demand-charge-management/) also quotes about $120k per 1 MW of PLC).

| Archetype | Assumed PLC | Capacity cost 24/25 | Capacity cost 26/27+ | Increase | Value of a 20% PLC cut |
|---|---|---|---|---|---|
| Mid-size manufacturer | 5 MW | ~$53k | ~$600k | +$550k | ~$120k/yr |
| Cold-storage DC | 1.5 MW | ~$16k | ~$180k | +$164k | ~$36k/yr (plus demand-charge savings, often larger) |
| Ambient warehouse | 0.4 MW | ~$4k | ~$48k | +$44k | ~$10k/yr (too small for $50K ACV) |
| University or hospital campus | 20 MW | ~$210k | ~$2.4M | +$2.2M | ~$480k/yr |
| Retail chain (300 stores x 0.2 MW) | 60 MW | ~$630k | ~$7.2M | +$6.6M | ~$1.4M/yr, but spread across 300 sites with little flexible load each |

Real cases: Belden Brick ($1.6k to $12k/month capacity, about +$125k/yr, a 90% jump in total electricity cost; it raised its prices). Plaskolite ($0.2M to $1.2M/yr; it's weighing a direct natural-gas feed). Americold (energy headwind of about $2M in Q1-2026; it's deploying refrigeration AI). Pittsburgh hospitals and universities ([IDEA blog](https://www.districtenergy.org/blogs/district-energy/2026/08/05/why-pittsburghs-hospitals-and-universities-arent-w)). Sources: [thestar/Bloomberg syndication](https://www.thestar.com.my/tech/tech-news/2026/07/07/big-tech-data-centers-are-driving-up-power-bills-at-america039s-rust-belt-factories), [Spokesman](https://www.spokesman.com/stories/2026/jul/07/big-tech-data-centers-are-driving-up-power-bills-a/), [Americold Q1 2026](https://finviz.com/news/351792/americold-announces-first-quarter-2026-results).

### 1.5 Capacity ("speed to power")
- The median US interconnection (generation) built in 2025 took **61 months**, up from 36 in 2015. Distribution-transformer lead times are reported at more than 2 years.
- Warehouse developers in Southern and Central California report finished buildings that can't operate, with one delay of 14 months. ([Bisnow](https://www.bisnow.com/news/los-angeles/industrial/electricity-availability-to-warehouse-projects-in-southern-central-california-presenting-hurdles-for-developers-117942), [North Bay Business Journal](https://www.northbaybusinessjournal.com/article/article/bills-aim-to-fix-californias-long-delays-in-connecting-construction-projec/))
- EV depots: utility upgrades take **12-24 months** and cost hundreds of thousands of dollars ([Flipturn](https://www.getflipturn.com/blog/how-autonomous-fleets-can-continue-to-grow-despite-capacity-constraints)).
- **Proof that flexible connection works for C&I:** under PG&E **Flex Connect**, the DERMS sends day-ahead hourly limits. PepsiCo's Fresno depot went from 3 MW (nights only) to as much as 4.5 MW, **18 months early** ([Fleet Equipment](https://www.fleetequipmentmag.com/pge-ev-charging-infrastructure/), [Latitude Media](https://www.latitudemedia.com/news/can-pge-make-flexible-grid-connection-the-california-standard/)). Most of the pipeline is EV fleets and batteries.

---

## 2. What software can actually do

| Lever | Typical savings | Software-only? | Maturity / crowding |
|---|---|---|---|
| 5CP / 4CP / 1CP peak prediction and alerts | Only valuable if load is cut | Yes, but the value needs curtailable load | **Commoditized.** Retailers, brokers and DR firms give alerts away. Even NIH built its own model |
| Autonomous peak response (BMS, refrigeration, process PLC control) | 10-30% of capacity, transmission and demand charges | Needs control integration (OT) | Moderate. Point solutions exist in cold storage and HVAC (e.g. Americold's refrigeration AI) |
| Demand response / capacity-market enrollment | $ per kW-yr payments | Aggregator license plus telemetry | **Crowded** (Enel X, CPower, Voltus, Leap, GridBeyond, Enersponse) |
| Tariff optimization / bill audit | 2-10% one-off; 18-20% of bills reportedly have errors | Yes | Crowded and low-multiple (Arcadia, EnergyCAP, TrueMeter, Billee, Delos, contingency-fee auditors) |
| Procurement and hedging | Timing and structure | Yes | Broker-dominated; AI entrants in the EU (trawa €24M, avoltra €2.3M) |
| BTM battery sizing and dispatch | Battery cuts peak by 45-65% of its rated size; about $100/kW-yr tag value in PJM | Needs hardware plus financing | Growing (Stem, Novele, Budderfly/Redaptive EaaS). Storage is "becoming the primary deal" in 2026 ([Solar Builder](https://solarbuildermag.com/projects/ci-installers-battery-storage-playbook-for-2026/)) |
| Flexible interconnection / speed to power | Months of earlier revenue | Needs utility cooperation plus a controllable load or battery | **Early.** Emerald AI (data centers), Critical Loop and Scale (hardware). Few software-first C&I players |
| EV fleet charging management | Demand-charge and capacity-limit management | Yes | Crowded (many charge-management platforms) |
| Onsite generation (gas, fuel cells) | Bypasses the grid | No (capex, EPC) | Infrastructure-fund territory (Scale Microgrids, Bloom) |

---

## 3. Competitors

| Company | What | Funding / status (as reported) | Threat to us |
|---|---|---|---|
| Enel X North America (ex-EnerNOC) | C&I DR, 5CP/4CP, procurement | Enel bought EnerNOC for ~$250M (2017); top-3 NA C&I aggregator | High in PLC/DR |
| CPower | C&I DR/VPP, PLC management | H.I.G. Capital majority, Constellation minority | High |
| Voltus | DER/VPP platform; "bring-your-own-capacity" for hyperscalers | $150M Series C at ~$600M (Oct 2024) **[UNVERIFIED; results conflict]**; Google named as a BYOC customer (June 2026) **[UNVERIFIED]** | High; moving toward speed to power |
| Leap | API-first BTM flexibility marketplace | ~$20.2M total; partnered with Enel NA (Dec 2025) | Medium |
| GridBeyond | AI flexibility / 4CP automation | ~$111M total; Series D $13.7M (Mar 2026); 2024 revenue ~$47.9M | Medium-high in ERCOT 4CP |
| Enersponse | DR provider | Not found | Low-medium |
| Gridmatic | AI power marketer / retail | ~$100M total (last round Nov 2023) **[UNVERIFIED]** | Medium (procurement) |
| Arcadia | Utility data APIs, tariff and bill data (~125 utilities) | Reported $200M Series E at $1.5B (Feb 2026). **[UNVERIFIED; may be confused with its 2021 round]** | Medium; more likely a data supplier or partner |
| Budderfly | Energy-as-a-service for SMB/chains | $100M debt (Nuveen, Jun 2025) | Medium in retail chains |
| Redaptive | Energy-as-a-service (capex-free retrofits) | $650M credit facility (May 2025) | Medium |
| Edo | Grid-interactive buildings | Not retrieved | Low-medium |
| Verdigris | AI electrical monitoring | ~$10M round (older); no 2025-26 round found | Low |
| Grid Status | Grid data / analytics | Not retrieved | Low (data tool) |
| Camus Energy | Utility grid orchestration (DERMS) | $25M+ Series A | Low; utility buyer. Could be the utility-side counterpart in flex interconnection |
| Emerald AI | Data-center compute flexibility to get power faster | $25M strategic (Mar 2026); **$150M Series A at $1.05B**; $220M total | Validates the speed-to-power thesis; data centers only, for now |
| Texture | Data/ops platform for DER operators | $12.5-13M Series A (May 2026); ~$22M total | Low (infrastructure layer) |
| Branch Energy | Reported "Arc" containerized battery ("grid in a box") | $33M Series B (Sep 2026) **[UNVERIFIED; may be a different Branch Energy than the Houston retail electricity provider]** | Medium in speed to power |
| Critical Loop | Mobile MW batteries + controller for fast connection | $26M Series A; $49M total (2026) | **High** in C&I speed to power (EV depots, airports) |
| Scale Microgrids | Build-own-operate C&I microgrids | >$1B project finance; acquired by EQT | Medium; infrastructure-heavy |
| Electrada | Charging-as-a-service for fleets | Duke Energy depot JV; funding not retrieved | Medium (fleets) |
| Fermata Energy | V2G bidirectional charging | Not retrieved | Low |
| Station A | AI clean-energy procurement for CRE portfolios | Series A (June 2025) | Low-medium |
| Novele | AI plus in-building battery for commercial buildings | $17M Series A (Sep 2026); 2,000 buildings in pipeline | Medium in CRE |
| Base Power | Residential batteries (TX) | Large raises (not re-verified) | Not a direct competitor |
| Brokers / retailers (NRG, Constellation, Engie, Vistra) | Supply plus free 4CP/5CP alerts | Incumbents | High; they bundle the alert for free |
| Bill audit (EnergyCAP, TrueMeter, Billee, Delos, contingency auditors) | Audit / UBM | Billee $9.15M seed | Low-multiple category |
| YC energy (Elyos, Dartboard, Rewbi, Astro) | Load shifting (Elyos, UK), battery and market analytics | Seed | Elyos is closest (load shifting for commercial buildings) |
| EU AI procurement (trawa €24M, avoltra €2.3M) | AI procurement for industry | Seed / Series A | Low in the US |

---

## 4. What's missing, and two theses

**The obvious one-sentence company ("We cut your electricity bill 20% with AI, no capex") exists in name many times over.** EaaS players, DR aggregators and brokers all say a version of it. What doesn't exist at scale:
1. **A fully autonomous capacity-tag and peak "autopilot"** that actually controls OT (refrigeration, compressed air, HVAC, process lines, fleet charging, batteries). It would guarantee savings under a SaaS contract with no aggregator license or market enrollment required. Most incumbents are aggregators (they earn from market payments) or alerters (they hand the work to plant staff).
2. **Software-first speed to power for loads that aren't data centers.** Emerald AI is doing this for data centers. For warehouses, fleet depots and factory expansions, today's answers are hardware rental (Critical Loop, temporary gensets) or build-own-operate (Scale).

### Thesis A: "Get your new site powered 12-24 months sooner" (Speed-to-Power OS for C&I)
*One sentence:* **"We get your new warehouse, fleet depot or factory line energized 12-24 months faster by turning it into a flexible load the utility can say yes to."**
- **Product:** AI load modeling of the planned facility, then a flexible-connection application package (hourly limits, guaranteed curtailment), then a real-time controller for chargers, refrigeration, batteries and temporary gensets that keeps the site under the utility's dynamic limit. Hardware is partner-supplied (BESS, rental gens).
- **Buyers:** industrial developers (Prologis-type REITs), 3PLs, fleet operators (delivery, school bus, drayage), manufacturers expanding lines, cold-chain builders.
- **Value:** a 250k sq ft warehouse at about $12/sq ft/yr is about $3M/yr in rent. Delivering 12 months early is worth about $3M. A fleet depot that can't charge strands trucks worth millions. **ACV:** $150-400k per project (setup plus controller SaaS); about $50-100k/yr ongoing per site.
- **Market math [EST]:** say ~3,000-6,000 constrained US C&I projects a year (large new warehouses, depots, expansions that hit capacity limits), at $200k blended in year one plus $60k/yr recurring. That's about **$0.6-1.2B/yr** of new-project spend plus a growing recurring base. A $1B+ outcome is plausible if it becomes the default path for developers.
- **Risks:** utility-gated (a flexible tariff like PG&E Flex Connect has to exist, and most PJM EDCs don't offer one yet). Project-based, lumpy revenue. Critical Loop and Voltus BYOC are moving here. A 90-day pilot is hard because energization happens on the utility's clock. A pilot can still deliver a "flex-connection feasibility plus utility filing" within 90 days.

### Thesis B: "Capacity-Tag Autopilot", starting with cold storage and industrial refrigeration
*One sentence:* **"Our AI autonomously runs your refrigeration and batteries to cut your capacity and demand charges 20-30%, guaranteed, live in 90 days."**
- **Why cold storage first:** it has thermal mass (it can pre-cool and coast), demand charges are 30-50% of the bill, and the operators feel the pain publicly (Americold's ~$2M Q1-2026 headwind; Lineage claims up to 30% savings from rate-aware cooling). Expand from there to food processing, plastics and other heavy process manufacturing, and campuses.
- **Market math [EST]:** about 3,000-4,000 US cold-storage and refrigerated food-processing sites with more than 1 MW of load. At ~$60-100k ACV that's $0.2-0.4B. Adding PJM/MISO/NYISO/ERCOT manufacturing and campuses above 2 MW (roughly 20-30k sites at ~$60k) brings the total to **$1.4-2.2B TAM**. Cross-check: PJM capacity alone is $16.4B/yr. If C&I carries about 40% ($6.5B) and an autopilot cuts 20% ($1.3B) at a 25% take, that's about **$330M from PJM capacity alone**, before demand charges, MISO or ERCOT.
- **Risks:** CrossnoKaye and other refrigeration-optimization vendors (not searched; **[UNVERIFIED]** competitive map), incumbent aggregators adding auto-control, OT integration costs (PLCs, Frick and other controls), and savings-share revenue that public markets value like services.

---

## 5. Kill signals

1. **Crowded, commoditized PLC/DR.** 15+ years of incumbents, alerts given away free, and a consolidation history (Enel/EnerNOC, Centrica/Restore, Engie/Kiwi, the CPower merger). Investors value DR aggregators at low multiples (the Voltus ~$600M valuation is tied to market revenue).
2. **Savings ceilings and fragility.** Capacity savings depend on regulator-set rules. ERCOT's 4CP-to-12CP change (30-minute intervals) blunts a well-known savings play, and PJM could change 5CP allocation or move to more hours. The price **collar caps the upside** of the pain through 2029/30.
3. **Software doesn't create flexibility.** Without curtailable load or a battery, prediction is worth almost nothing. Plants with 24/7 processes resist curtailment, and batteries bring capex, financing and EPC work.
4. **Utility-specific integration.** Tariffs, PLC methods (each EDC is different) and flexible-connection programs vary by utility. Speed to power only works where the utility cooperates.
5. **Lagged, lumpy pain.** Fixed-price supply contracts hide the shock until renewal.
6. **Savings-share economics.** Contingency/gain-share companies look like services (bill audit, EaaS). Getting to a $50K+ ACV floor rules out warehouses and small retail.
7. **Political risk.** Data-center large-load tariffs, backstop procurement, or state action could shift costs off C&I and reduce the urgency.

---

## 6. Scores (1-10)

| Criterion | Thesis A: Speed-to-Power OS | Thesis B: Capacity-Tag Autopilot (cold storage wedge) |
|---|---|---|
| Pain | 9 | 8 |
| Urgency | 8 | 8 (resets at each contract renewal and each summer 5CP window) |
| ROI clarity | 8 | 8 |
| Customer accessibility | 6 (developers and fleets are reachable but deal-driven) | 7 |
| Pilot speed (90 days) | 4 (utility clock) | 7 (pre-cool pilot in one summer; but PLC savings only show up after the June-Sep window) |
| Market size | 7 | 6 |
| Expansion | 8 (to ongoing site OS, tag management, DR revenue) | 7 (to campuses, manufacturing, batteries) |
| Venture potential | 7 | 5 |
| Defensibility | 6 (utility relationships, interconnection data) | 4 (OT integrations; incumbents can copy) |
| Why now | 9 | 9 |
| Competition position | 6 | 3 |
| **Average** | **7.1** | **6.5** |

---

## 7. VERDICT: **REFRAME**

- **KILL** the horizontal pitch ("AI cuts any business's electricity bill / capacity tag 20%"). It's a crowded, commoditized aggregator and broker category with low multiples, and the price collar caps the shock.
- **ADVANCE to validation:** Thesis A (speed to power for new C&I loads), with Thesis B as the operating layer that keeps the customer after energization. Narrowed one-liner: **"Emerald AI for everyone else: we get new warehouses, fleet depots and factory lines powered years sooner by making them flexible loads."**
- **Next diligence before committing:**
  1. Count the US utilities with live flexible-connection or non-firm service tariffs, and the queue sizes for C&I distribution upgrades (PJM EDCs, ComEd, Duke, Georgia Power, Oncor).
  2. Interview 10 industrial developers and fleet operators about lost months and willingness to pay.
  3. Map Critical Loop, Voltus BYOC and Emerald AI roadmaps toward C&I.
  4. Check CrossnoKaye and other refrigeration-AI competitors before pursuing Thesis B.
  5. Confirm the **[UNVERIFIED]** funding figures (Arcadia, Voltus, Branch, Gridmatic).
