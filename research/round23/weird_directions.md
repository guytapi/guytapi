# Round 23: Weird directions (structural questions, outside the exhausted clusters)

Date: 2026-10-06. Method: 15 theses from 6 structural questions → 7 most promising checked with 20 web searches → kill using round18/FAILURE_TAXONOMY.md → full finalist format for the one that survived.
Excluded clusters (not proposed): AI governance/control, agent infra, fraud/verification, compliance mandates, migration, AI spend, agent commerce.
Source rule: every URL below appeared in a search result. Claims taken only from search snippets, not from reading the page, are marked *(snippet)*. Nothing here was fetched in full (WebFetch is blocked).

**Bottom line: none reach A. One weak B (a clearing network for stranded long-lead electrical gear), probably 10-15% likely to pass its test. It is also outside the founders' edge, so treat it as an option, not a recommendation.**

---

## 1. The 15 theses

### Q1. What becomes scarce when intelligence is abundant?
1. **Operational-trace licensing for non-tech firms.** Broker licenses to the decision traces that mid-market industrial companies hold (maintenance tickets, QC dispositions, approval chains) and sell them to AI labs and vertical-AI companies. *Insight:* public text runs out around 2026-2032, and process outcomes do not exist on the web. The owners are not set up to redact, price or sell this data.
2. **Tacit-knowledge escrow for retiring operators.** Record retiring plant operators and tradespeople and turn what they know into agent skills the employer owns and can license. *Insight:* this knowledge loses its value on the day the person retires unless it was captured, and capture is now cheap.
3. **Physical capture rights.** Exclusive contracts to put sensors in or record specific physical places (shelves, job sites, loading docks), sold to model builders. *Insight:* the right to observe a place, not the model, becomes the scarce asset.

### Q2. Markets that exist only because humans are slow: what happens to their *infrastructure*?
4. **Stranded BPO real estate.** Repurpose idle contact-center floors (Quezon City IT parks above 22% vacancy) into expert-data and RL-environment production sites or small inference sites. *Insight:* the buildings, power, fibre and PEZA tax status survive after the seats go.
5. **Exposure-basis drift in commercial insurance.** Workers' comp and GL premiums are rated on payroll. As agents replace payroll, carriers lose premium base that no longer matches the risk. Sell carriers and MGAs a new rating basis built from output and automation data. *Insight:* a whole insurance rating system assumes headcount is a proxy for activity.
6. **Telecom capacity unwind.** BPOs hold large SIP-trunk and DID portfolios that they are now winding down. A market to re-home and reputation-clean those numbers. *Insight:* phone numbers with a clean history become scarce as AI voice traffic grows.

### Q3. New assets
7. **Code-provenance diligence for M&A.** Value and de-risk agent-written codebases in acquisitions: license contamination, who could maintain it, whether it can be rebuilt. *Insight:* if code costs almost nothing to write, its value moves to whether it can be rebuilt and to its provenance.
8. **Inter-company licensing of skills and workflows.** A company sells its tuned internal agent workflows to peers as IP. *Insight:* operational know-how becomes a product with almost no marginal cost.
9. **Rebuildability escrow for AI-native vendors.** Software escrow plus regular checks that an agent can actually rebuild and run the escrowed code. *Insight:* escrow used to be theatre because nobody could run released code; agents make a release usable, while 3-person vendors make release more likely.

### Q4. New inter-company markets when agents do work
10. **Agent pooling through co-ops.** Credit unions, rural electric co-ops and ag co-ops build agents jointly through their existing shared-service companies (CUSOs and similar). *Insight:* co-op legal structures already exist for shared back-office work.
11. **Seasonal agent-capacity exchange between professional firms.** Tax and audit firms rent their tuned agents to peers in other jurisdictions or fiscal calendars. *Insight:* peak seasons differ by jurisdiction and fiscal year-end, so tuned capacity can move between firms.
12. **Vertical agent-performance telemetry as a data product.** Neutral benchmarks of how vendors' agents perform in production inside one vertical. *Insight:* buyers need a "Gartner from telemetry".

### Q5. Physical constraints that become binding
13. **Clearing network for stranded long-lead electrical gear and factory slots.** About 45% of planned 2026 US data-center capacity is delayed or cancelled. Developers reserved transformer, switchgear and generator production slots years ahead. Build an exchange that moves those slots and finished units to buyers who can energize now (other developers, utilities, co-ops, industrial, BESS/solar). *Insight:* the AI build-out made **factory slots a financial asset**, and the cancellations made them liquid. No neutral venue exists.
14. **Managed on-prem inference appliance fleet ops** for law firms and hospitals, including the power and cooling retrofit. *Insight:* building-level power, not GPUs, limits inference in offices.
15. **Heat-offtake contracts for on-prem inference.** Sell waste heat from inference closets to building HVAC or district heat. *Insight:* on-prem inference turns office buildings into small heat sources.

### Q6. Software economics when building is nearly free
(Covered by #7 and #9.) Also considered: **enterprise-funded OSS triage service.** Maintainers are drowning in AI-written pull requests, so enterprises would pay a steward to triage the dependencies they rely on.

---

## 2. Reality checks (7 theses, 20 searches)

| # | Thesis | What we found | Verdict |
|---|---|---|---|
| 1 | Operational-trace licensing | One market map (Jun 2026) *(snippet)* counts 15 active data-brokerage companies with >$178M raised. Aptura AI already targets "enterprises license proprietary data to AI companies". Human Native AI, Opendatabay and Appen "enterprise data" also active. ([extruct.ai](https://www.extruct.ai/data-room/ai-training-data-marketplaces/), [premieralts](https://www.premieralts.com/companies/aptura-ai), [appen](https://www.appen.com/enterprise-data)) | **KILL** F2 (visible-pain race) |
| 4 | Stranded BPO real estate | The pain is real: QC IT parks >22% vacancy, Cebu heading to 18-20%, lease decisions stretching to 12-18 months *(snippet)* ([kitalent](https://kitalent.com/articles/article-quezon-city-bpo-hollow-growth), [sunstar](https://www.sunstar.com.ph/cebu/cebu-office-vacancy-may-hit-20-on-ai-new-supply)). But it is a local real-estate repositioning play with landlord buyers and no software moat. | **KILL** F4 / not venture |
| 5 | Exposure-basis drift | Found no evidence of the problem. WC risk tracks humans (fewer workers means fewer injuries), so the "mismatch" is mostly imaginary. Where agents create losses without payroll, that is AI liability insurance (funded MGAs). Premium-audit AI (Nomad Data, V7) is already sold to carriers. ([nomad-data](https://www.nomad-data.com/doc-chat/solving-classification-errors-ai-powered-detection-of-underreported-exposures-for-workers-compensation-and-general-liability-a-guide-for-underwriting-analysts), [v7labs](https://www.v7labs.com/agents/ai-agent-for-premium-auditors)) | **KILL**: the core insight is wrong |
| 7 | Code-provenance M&A diligence | Black Duck already sells M&A code audits and says reliable AI-origin detection does not exist and may never exist *(snippet)*. ([blackduck](https://www.blackduck.com/blog/software-quality-audits-ma-due-diligence.html)) | **KILL** F1 plus unsolvable detection |
| 8 | Skills/workflow licensing | Agensi, AgentExchange (Salesforce, 200+ partners), Agentmarketplace.ai and many others. Labs run native skill directories. ([mdskills](https://www.mdskills.ai/learn/ai-skills-marketplace-2026)) | **KILL** F1/F2 |
| 9 | Rebuildability escrow | Codekeeper already sells "AI Escrow" covering weights, prompts, agent logic and workflow orchestration ([codekeeper](https://codekeeper.co/ai-escrow?hsLang=en)). The escrow market is small. | **KILL** F4 + incumbent extended |
| 10 | Co-op agent pooling | CUltivate (Vertice AI/Vizo/Filene), DASO AI (Digital Align + SkyOne FCU), Precision CUSO (Teachers FCU + Corridor), Delfi CUSO. ([cuinsight](https://www.cuinsight.com/press-release/cultivate-unveils-first-foundational-ai-platform-purpose-built-for-credit-unions/), [cubroadcast](https://www.cubroadcast.com/news/teachers-federal-credit-union-and-corridor-platforms-announce-intent-to-launch-precision-cuso-to-expand-ai-driven-credit-decisioning-for-credit-unions-nationwide)) | **KILL** F2 |
| 14 | On-prem inference appliance ops | Qualcomm AI On-Prem Appliance, Dell/HPE/Vertiv 360AI reference designs. Turiyam and others raising. ([qualcomm](https://www.qualcomm.com/news/releases/2025/01/qualcomm-launches-on-prem-ai-appliance-solution-and-inference-su), [letsdatascience](https://letsdatascience.com/news/turiyam-builds-cheaper-ai-inference-infrastructure-for-enter-824f28b0)) | **KILL** F1 |
| 16 | OSS triage stewardship | GitHub is weighing a pull-request kill switch and building maintainer controls. Tidelift (now Sonar) and Open Source Pledge cover the funding side. ([opensourceforu](https://www.opensourceforu.com/2026/02/github-weighs-pull-request-kill-switch-as-ai-slop-floods-open-source/), [softwareseni](https://www.softwareseni.com/what-github-and-the-oss-ecosystem-are-building-to-protect-maintainers-from-ai-slop)) | **KILL** F1 |
| 13 | **Stranded long-lead gear exchange** | See below | **Survives → weak B** |

Not checked (lowest prior): #2 (Augmentir-style connected-worker vendors likely), #3 (pre-demand), #6 (Hiya/TNS/First Orion own number reputation), #11 (pre-demand), #12 (Vals AI, Artificial Analysis), #15 (small).

### Evidence for #13
- **Cancellations are real and large:** about half / ~45% of planned 2026 US data-center capacity is delayed or cancelled, partly because of transformer, switchgear and battery shortages (Apr 2026) ([Yahoo Finance](https://finance.yahoo.com/sectors/technology/articles/half-planned-us-data-center-150928890.html), [The Standard HK](https://www.thestandard.com.hk/innovation/article/328687/US-AI-expansion-hit-by-power-shortages-half-planned-data-centers-delayed-or-canceled)). Bernstein expects cancellations to keep rising through 2027 ([Tribune India](https://www.tribuneindia.com/news/business/data-center-pipeline-faces-construction-delays-cancellations-to-mount-through-2027-bernstein/)).
- **Slots are now an asset class:** slot reservations made by letter of intent are spreading. Tier-1 transformer OEMs are said to be booked to 2030 ([Asia Economy, Apr 2026](https://view.asiae.co.kr/en/article/2026041409530886171)) *(snippet)*. Developers reserve factory slots "years before a specific project is finalized" ([datacentres.com, Aug 2026](https://www.datacentres.com/news/36-month-lead-times-turn-transformer-shortage-into-data-centre-site-selection-ki-slot3-2026-08-07)) *(snippet; the site looks templated, so weak source)*. Ayr Energy ($25M, EIP) sells modular transformers precisely because customers must order before projects are finalized ([munich-startup](https://insights.munich-startup.de/news/feed/ayr-energy-raises-25m-to-build-century-old-transformers-for-ai-data-centres)).
- **Secondary prices are high:** used units reportedly trade at 78-82% of new replacement cost *(snippet, same weak source; unverified)*. Remanufactured distribution units ship in 1-4 weeks against 60-80 weeks for new ([POWER](https://www.powermag.com/partner-content/beating-the-transformer-bottleneck-remanufacturing-build-to-stock-and-smart-procurement/)).
- **Incumbents are dealers, not exchanges:** Maddox (buys surplus at up to 5x scrap, remanufactures), CORE Transformers (Emerald Lake PE, 2025), IPS asset recovery, Electrical Trader, Hashwatt, Elektrik ($1M seed 2021, new MV gear e-commerce) ([maddox](https://www.maddox.com/services/sell-surplus), [peprofessional](https://peprofessional.com/2025/09/emerald-lake-launches-north-american-transformer-platform-with-core-buy/), [renewableenergyworld](https://www.renewableenergyworld.com/energy-business/energy-finance/high-voltage-equipment-e-commerce-start-up-raises-1-million-seed-funding/)). Grid-software startups (GridCARE, Gridware, GridStrong) work on capacity and ops, not equipment liquidity. **No funded neutral slot/stranded-gear exchange found in 4 targeted searches. That is weak evidence of absence.**
- **Legacy pooling precedent:** EEI STEP and Shared Inventory Management LLC pool large power transformers for disaster spares ([DOE RFI PDF](https://www.energy.gov/sites/prod/files/2015/09/f26/PEICo_Submission_RFI_Transformer%20Reserve.pdf)). This shows utilities will pool assets, but only for disaster spares, not for trading.
- **Counter-signal (important):** distribution-transformer availability has improved. Scarcity is now concentrated in large power transformers and GSUs (128-144 weeks) ([POWER](https://www.powermag.com/transformers-in-2026-shortage-scramble-or-self-inflicted-crisis)) *(snippet)*. China transformer imports rose from <1,500 (2022) to >8,000 units (2025) *(snippet)*. Giga Energy is adding ~3,000 MV units/yr in Houston ([transformer-technology](https://transformer-technology.com/giga-energy-opens-new-houston-factory-to-expand-u-s-transformer-production/)). **The spread this business lives on is cyclical.**

---

## 3. Finalist: Clearing network for stranded long-lead electrical gear and factory slots

- **One-line problem:** About $X B (unquantified) of transformers, switchgear and generator slots reserved by delayed or cancelled AI data-center projects is sitting idle, while other buyers wait 2-5 years for the same gear. No neutral venue exists to match, verify and transfer it.
- **Why now:** (1) Slot reservations by LOI only became normal in 2024-26. (2) The cancellation wave (~45% of 2026 capacity) began in 2026 and is expected to grow through 2027. (3) Prices for used gear are near new-unit prices, so a transfer is worth doing.
- **Exact buyer:** Sell side: the VP of Procurement / Head of Supply Chain at data-center developers and EPCs holding reserved slots or finished units (deposit at risk, carrying cost). Buy side: the procurement director at utilities, G&T co-ops, munis, BESS/solar developers and industrial plant engineering.
- **Exact ICP:** Sell: US developers with ≥200 MW pipelines and at least one paused site (roughly 150-300 firms, unverified). Buy: ~900 co-ops + ~2,000 munis + IOUs + ~1,000 active BESS/solar developers (counts from memory, unverified).
- **Current workaround:** Calling dealers (Maddox, CORE, IPS), who buy below value and resell. Informal developer-to-developer calls. Asking the OEM to move the slot (the OEM usually keeps the deposit and reprices the slot to its waitlist).
- **Why incumbents cannot easily own it:** OEMs gain from re-pricing cancelled slots themselves, so they are conflicted against a transparent market. Dealers make money on the spread and hold inventory, and would lose it if pricing became transparent. Utilities' pooling bodies (STEP, Grid Assurance) are disaster-spare co-ops, not markets.
- **30-day MVP:** A confidential listing registry. Normalized specs (kVA/MVA, voltages, BIL, impedance, cooling, standards), condition and test records, slot-delivery date, and whether the slot can be assigned. Buyers search against their specs. Transactions are brokered by hand under NDA, with an escrowed deposit and a third-party factory-acceptance or test witness.
- **Pilot design:** Two sell-side developers list ≥5 items each. Run spec-matching against the open RFQs of five utilities or BESS developers. Target one closed transfer within 60 days.
- **Pricing hypothesis:** 3-6% success fee per transfer, paid by the seller (on a $2-8M large unit that is $60-480K). Later: an annual data subscription for price and lead-time indices (an "Emerald/Silicon Data for grid gear") and slot-backed financing.
- **Expansion path:** Brokerage → price and lead-time index → financing/insurance of slot deposits → futures-like slot contracts → global (EU/India OEM slots) → other long-lead items (turbines, HV breakers, chillers).
- **Moat:** Transaction data no one else has (true clearing prices, slot calendars) and two-sided liquidity. It is weak until volume exists, and pricing data can be copied by dealers who see the same flow.
- **Why it could become $10B+:** Only if the index and financing layer becomes the benchmark for a $65B/yr power-equipment market (E&E News projection) ([eenews](https://www.eenews.net/articles/data-centers-to-triple-us-power-equipment-market-to-65b/)), the same way Silicon Data did for GPU compute. Brokerage alone is a $50-200M revenue business at peak and then shrinks as the shortage ends.
- **Direct competitors / adjacent threats:** Maddox, CORE (PE-backed), IPS, Electrical Trader, Hashwatt; OEM waitlist programs; GridCARE-type capacity platforms; Caplight-style secondary venues moving into real assets; hyperscalers running internal slot pools.
- **One sentence to send a developer's VP Procurement / CFO:** "If any of your reserved transformer or switchgear slots belong to a paused site, we will match them with a buyer who can energize this year and recover your deposit plus a premium, without the OEM re-pricing the slot or a dealer taking the spread."
- **5 discovery questions:**
  1. How many reserved slots or finished units are tied to sites you have paused, and what is the deposit exposure?
  2. Do your OEM LOIs let you assign the slot to a third party? What happened last time you asked?
  3. What did you do with the last surplus unit, and at what percentage of replacement cost?
  4. (Buy side) What would you pay above list to move a 2028 delivery to Q1 2027, and who approves that?
  5. What test or witness evidence would you need before buying a unit you have not seen?
- **Hard kill criteria:** <2 of 8 developers hold transferable surplus; OEM LOIs are uniformly non-assignable *and* OEMs refuse consent; buyers will not pay ≥10% over the dealer price for the time saved; distribution and MV lead times fall below 30 weeks by mid-2027 (the spread disappears).

**Scores:** Pain 7, Urgency 7, ROI clarity 8, Customer accessibility 5, Pilot speed 5, Market size 6, Expansion 6, Venture potential 6, Defensibility 4, Why now 8, Competition position 6 → **avg 6.2. Not A.**

**Classification: B (weak).** The supply of stranded slots is new (2026), its size is unknown, and it does not show up in public sources. That is the B profile. Main risks: the shortage is cyclical (F4 over time), slots may not be assignable, and the founders have no edge here (their assets are security/AML/caller verification). Prior that the test passes: ~10-15%.

### 14-day test
- **Days 1-3:** Build a target list from public news on paused or cancelled data-center projects: 25 developers/EPCs. Build a buy-side list of 15 co-ops, munis and BESS developers with open transformer RFPs (public procurement portals).
- **Days 3-10:** 20 calls (aim for 8 sell side, 7 buy side). Ask the 5 questions above. Ask each seller for a redacted inventory sheet and the assignment clause of one LOI.
- **Days 10-14:** Run spec matching between the sheets and the buyer RFQs. Send matched pairs indicative terms.
- **Pass (all three):** (a) ≥3 sellers share inventory totalling ≥$20M at replacement value; (b) ≥2 of those slots or units are legally transferable or the OEM has said it would consent; (c) ≥1 buyer signs a non-binding LOI at ≥10% over dealer pricing, *or* ≥1 seller signs an exclusive listing agreement with a success fee.
- **Fail:** fewer than 2 sellers share inventory, or no LOI is assignable and no seller holds finished units.

---

## 4. Lessons from this round
1. "Weird" asset theses (data licensing, skills, escrow, co-op agents) were all crowded already. Platforms and fast followers fill new-asset markets as fast as tooling markets.
2. The one survivor came from a **physical market made illiquid by the AI build-out itself** (factory slots, stranded gear), where the incumbents are dealers and OEMs who profit from opacity. That pattern is worth mining further: chillers, turbines, HV breakers, interconnection positions.
3. Survivors in physical markets are cyclical. Any B in this family must pass a "does the spread outlive 2028?" test.
