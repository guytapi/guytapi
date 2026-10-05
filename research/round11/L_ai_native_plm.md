# Thesis L: AI-native PLM (deep dive, red team)

**Date:** 2026-10-05 | **Origin:** round11/ai_native_challengers.md (scored 7.1 at scan level) | **Method:** round7/METHOD.md template + original bar | **Searches used:** 38 of 40 (WebFetch/Reddit blocked, so evidence comes from search snippets).

Legend: [S] = source found in search results this round. [U] = unverified or estimated. [I] = my inference from sources.

**Thesis under test:** "AI agents run engineering changes, BOMs and supplier/compliance data for hardware companies, replacing Windchill, Agile and Teamcenter." Wedge: a read-only ECO agent plus a fixed-price migration readiness scan, then becoming the system of record.

**Bottom line (up front): KILL as stated.** Every pillar of the scan-level 7.1 weakened under research:
1. The **"no funded AI-native challenger" claim was wrong.** The AI-layer-over-PLM slot was funded in the last 6 months: Flow Engineering raised $50M at $750M (Sequoia, Sep 30 2026), SPREAD AI raised $30M (Apr 2026) and CADDi raised $114M at $1.2B (Sep 2026).
2. **Every incumbent shipped or announced PLM agents in 2026**: Siemens, PTC, Dassault, Autodesk, Aras and Propel.
3. **The forced moves are leaky.** Windchill's change is a re-license, not a migration. Agile owners can stay on Rimini Street support for 15+ years, and every PLM vendor plus the SIs are already working the Agile list.
4. **The exit ceiling is weak.** Arena sold for $715M on about $50M ARR, and Duro was absorbed into Altium.

---

## 1. Problem
Hardware companies run engineering change (ECR/ECO/ECN), BOM control and supplier/compliance data through legacy PLM (Windchill, Teamcenter, Agile, ENOVIA) or spreadsheets.
- Change work is slow, manual and spread across CAD, PLM, ERP and email.
- Legacy PLM is expensive, heavily customized and disliked by engineers.
- Two vendor-driven deadlines (Windchill re-licensing, Agile end of Premier Support) supposedly force a re-buy in 2026-27.

## 2. Recent evidence (pain, Q1)

| # | Signal | Strength | Source |
|---|---|---|---|
| 1 | ECOs "consume 30-50% of engineering capacity"; Aberdeen survey: 85% call their change systems "broken" | Old (IHS whitepaper, Aberdeen ~2000s). Directionally real but stale | [S](https://cdn.ihs.com/www/pdf/Change-Management.pdf) |
| 2 | Teradyne cut change cycle time from 90 to 14 days (84%) and saved $2M/yr with PLM | Vendor case study (Siemens). Shows the pain is solvable by existing PLM | [S](https://blogs.sw.siemens.com/electronics-semiconductors/?p=149) |
| 3 | 67% of PLM programs exceed budget/timeline, with a 32% average overrun and about 4.5 months of delay | SI marketing (HCLTech) | [S](https://www.hcltech.com/en-us/trends-and-insights/plm-programs-roi-challenges-and-optimization) |
| 4 | Academic study (U. Twente): the claimed <50% PLM success rate in SMEs is "not evidenced" | Cuts against the pain narrative | [S](https://research.utwente.nl/en/publications/plm-implementation-success-rate-in-sme-an-empirical-study-of-impl-2/) |
| 5 | Windchill ePLM: buyers expect "less functionality for higher cost… to set up the eventual move to Windchill+" | VAR blog (GoEngineer, which sells alternatives) | [S](https://www.goengineer.com/blog/windchill-migration-2026-your-options-risks-and-next-steps) |
| 6 | Legacy Windchill packages cannot be renewed after 9/30/2026; renewals after 7/1/2026 must move to ePLM | Confirmed (TriMech) | [S](https://enterprise.trimech.com/windchill-migration-deadline-paths-forward-before-legacy-licenses-expire/) |
| 7 | Agile 9.3.6 is the final release and Premier Support ends 12/31/2027; "most Agile users declined Fusion Cloud PLM" | Confirmed (Trace One, Mekari) | [S](https://www.traceone.com/oracle-agile-plm-when-does-support-end-and-what-are-the-options-trace-one), [S](https://officeless.mekari.com/blog/oracle-agile-plm-end-of-life-alternatives) |
| 8 | Hardware startups "get surprisingly far on Google Sheets until the first ECO derails" them | Listicle (Indie Hackers) | [S](https://www.indiehackers.com/post/the-7-best-bom-management-software-options-for-lean-hardware-teams-in-2026-9c3000b93f) |

**Assessment:** The pain is real but chronic, not acute.
- The newest quantitative evidence is vendor or SI marketing. No 2026 practitioner wave was found (Reddit blocked; HN search returned nothing specific).
- The Windchill "forced move" is a **re-license inside PTC**. The path of least resistance is to pay PTC more.
- **Agile customers have a cheap escape hatch:** Rimini Street supports Agile "including all customized code — for 15+ more years" at up to 90% lower support cost [S](https://riministreet.com/support-for-oracle/agile-plm). Spinnaker offers the same [S](https://redresscompliance.com/oracle-agile-plm-third-party-support-decision).

## 3. Who has the pain
- VP Engineering, Director of PLM/Engineering Systems, Head of Hardware Ops, and the CIO (co-signs at mid-market and enterprise).
- Startups: Head of Hardware or the first ops hire.
- Scale: about **4,177 US manufacturing firms with 500+ employees** (Census, 2022) [S](https://manufacturingleadgeneration.com/small-manufacturing-business-statistics/), and roughly 235K smaller firms, most with no PLM.
- Agile installed base: about 1,250-1,500 companies [S, from round 11](https://idatalabs.com/tech/products/oracle-agile-plm), heavily medtech and hi-tech.

## 4. What they do today
- **Enterprise:** Teamcenter, Windchill or ENOVIA, plus SI-run migration factories (Siemens/Intelizign Teamcenter Migration Factory [S](https://www.siemens.com/en-us/products/intelizign-engineering-services-teamcenter-migration-factory/); PROSTEP OpenPDM [S](https://www.prostep.com/en/digital-thread-platform/openpdm-migrate); TTPSC Agile→Windchill [S](https://ttpsc.com/en/services/oracle-agile-to-windchill-migration/)).
- **Mid-market:** Arena, Propel, Aras or Fusion Manage.
- **Startups:** Sheets, OpenBOM, Bild, or Duro (formerly).
- **Agile owners:** the four paths are sustaining support, third-party support, Fusion, or an alternative PLM.

## 5. Why current products fail (and why that no longer opens a door)
- Legacy PLM is complex and customization-heavy, CAD-coupled, and priced by module or role.
- **But the AI gap is being closed from four directions at once** (section 10):
  1. Incumbent agents (Siemens, PTC, Dassault, Autodesk, Aras).
  2. Cloud-native mid-market vendors with agents (Propel One on Agentforce, Arena AI Assistant).
  3. Overlay AI layers that need no migration (Flow, SPREAD, CADDi, Leo).
  4. CAD/EDA owners absorbing startup PLM (Altium/Duro).

## 6. Why now (tested)

| Claimed driver | Verdict |
|---|---|
| Windchill legacy renewals end 9/30/2026 | **Weak.** It is a re-license within PTC. Customers update data structures and pay. VARs pitch ENOVIA/Aras/Propel as alternatives, but nothing shows switching at scale. Also, the window has already closed (today is 10/5/2026), so deals were decided in Q2-Q3. |
| Agile Premier Support ends 12/31/2027 | **Real but contested.** About 1,250-1,500 companies have 15 months left. But Propel ("Life Beyond Agile" campaign; record FY bookings +42%, with Agile replacements "at an accelerated pace") [S](https://www.businesswire.com/news/home/20260303913603/en/Propel-Software-Marks-Best-Year-in-Company-History-Fueled-by-DesignHub-Propel-One-Solutions), PTC [S](https://www.ptc.com/en/blogs/plm/transitioning-from-oracle-agile-plm), Autodesk [S](https://www.autodesk.com/blogs/design-and-manufacturing/key-considerations-for-transitioning-from-oracle-agile-product-lifecycle-management-to-autodesk-fusion-manage/), Aras, Siemens and Rimini are all hunting that list. Medtech-heavy (FDA-validated), which is the hardest segment for a startup. |
| Hardware renaissance | **Real demand, weak buyer.** Robotics raised $18.8B YTD 2026, beating any full year [S](https://news.crunchbase.com/robotics/startup-venture-funding-surges-2026-data/). YC W26: 1 in 8 companies is physical [S](https://pinggy.io/blog/what_yc_is_funding_in_2026/). But startups pay $3-30K/yr, and the high-velocity ones (Anduril, Rivian, Stoke, Joby) are buying **Flow Engineering**. |
| AI can draft ECOs and migrate cheaply | **True, which is why everyone shipped it in 2026** (section 10). Not unique. |

## 7. Potential product
Read-only connectors to Windchill/Teamcenter/Agile plus ERP, covering:
1. An ECO agent: impact analysis, where-used, CCB packet, BOM error flags.
2. A migration readiness scan: a cleaned, de-duplicated, mapped product record with a fixed-price quote.
3. Later: a system of record with supplier and compliance agents.

## 8. Time to value
- Overlay: 4-8 weeks to connect to one incumbent instance (incumbent APIs and customizations are the bottleneck) [I].
- System-of-record replacement: 6-18 months, plus validation for regulated customers [U].

## 9. Pilot (30-90 days)
- **Feasible as an overlay.** This is exactly how Flow lands: "plugging into tools engineers already use… instead of forcing a full PLM rip and replace" [S](https://sacra.com/research/flow-engineering).
- **Infeasible as a PLM replacement.** You cannot cut over a system of record in 90 days.
- The read-only pilot competes head-on with the incumbent's own bundled agent (Teamcenter AI BOM agent, Windchill AI Assistant). Those are already inside the access-control model and need no security review.

## 10. Competition (Q3, searched hard)

**Incumbents shipped agents in 2026 (Q4: "can't respond" is false)**
- **Siemens Teamcenter AI BOM agent:** "BOM-aware agentic experience… analyze impact, and execute changes within governed workflows"; Intelligence Center X [S](https://blogs.sw.siemens.com/teamcenter/ai-bom-agent-plm-engineering-change/). This is the thesis's ECO wedge, shipped by the incumbent.
- **PTC:**
  - Windchill AI Assistant GA'd Apr 28 2026, with agents for "parts and change management" on the roadmap [S](https://www.ptc.com/en/news/2026/ptc-launches-windchill-ai-assistant).
  - Windchill AI parts rationalization (part de-duplication) [S](https://www.digitalengineering247.com/article/ptc-launches-windchill-ai-parts-rationalization-capabilities/plm).
  - Arena AI Assistant for ECOs and CAPAs [S](https://www.ptc.com/it/news/2025/ptc-launches-arena-ai-assistant).
  - Onshape AI Advisor and a FeatureScript MCP server [S](https://www.digitalengineering247.com/article/onshape-ai-advisor-now-embedded-directly-in-the-design-environment).
- **Dassault:** AURA/LEO/MARIE "Virtual Companions" on the "AI-native agentic 3DEXPERIENCE" (Feb, Jul and Sep 2026 releases) [S](https://www.3ds.com/assets/invest/2026-02/dassault-systemes-unveils-new-way-of-working-for-industry-with-ai-powered-virtual-companions-pr-final-11-feb-2026_0.pdf), [S](https://www.intelligentcio.com/eu/2026/07/23/dassault-systemes-expands-ai-native-3dexperience-platform-with-agentic-virtual-companions-for-industrial-engineering/).
- **Autodesk:** Fusion Manage "agentic PLM experience" previewed at AU 2026 (Sep) [S](https://monoist.itmedia.co.jp/mn/articles/2610/01/news015.html). Autodesk also owns MaintainX and Upchain.
- **Aras:** Innovator Edge "engineering AI platform" (MCP, GraphRAG, connects to other PLMs) launching FY2026; ACE 2026 theme was "agentification of PLM"; 80% of new customers choose SaaS [S](https://monoist.itmedia.co.jp/mn/articles/2602/26/news042.html), [S](https://www.cimdata.com/component/docman/doc_download/4173-the-agentification-of-plm-aras-ace-2026-strategy-and-insights-commentary).

**Cloud-native PLMs with agents**
- **Propel:**
  - Propel One agentic AI (Salesforce Agentforce) works across items, BOM, change, quality and training.
  - Claims to be the first PLM with production MCP.
  - DesignHub provides multi-CAD.
  - Record FY ended Jan 2026: +42% bookings.
  - About 130 employees; revenue estimates range from $25M to $80M [U] [S](https://www.businesswire.com/news/home/20260303913603/en/Propel-Software-Marks-Best-Year-in-Company-History-Fueled-by-DesignHub-Propel-One-Solutions), [S](https://www.qualitydigest.com/inside/improvement-tools-news/propel-software-launches-production-model-context-protocol-plm-072126).
  - **Propel is already the "AI-native Agile replacement" pitch.**
- **OpenBOM** has an AI Agent [S](https://www.openbom.com/blog/openbom-for-startups-how-hardware-startups-can-use-plm-to-streamline-their-businesses).
- **Bild:** cloud PDM/PLM with an AI diff/search suite; about 24 employees; Mucker-backed; G2 awards in 2026 [S](https://mucker.com/company/bild/).

**Duro after the Altium deal**
- Duro was acquired by Altium (CB Insights shows Oct 1 2025; announced Dec 2025).
- Its features are now gated by Altium Develop / Altium Agile / Altium Designer editions, and its docs sit under an Altium "legacy" path [S](https://www.altium.com/vi/documentation/altium-365/legacy-valispace/duro-plm?version=4).
- [I] Duro has become an EDA-bundled feature (Renesas → Altium → Duro), not an independent PLM. The one AI-native PLM challenger was absorbed at seed scale. That reads as a weak exit, not proof of a gap.

**AI overlay layers (the thesis's actual wedge) are funded**
- **Flow Engineering:** $50M Series B at **$750M** (Valor, Atreides, Sequoia; Sep 30 2026).
  - Agents "run impact analysis, flag conflicts" across CAD, Git, simulation and docs.
  - Customers: Rivian, RV Tech, GM, Anduril, Stoke, Joby, Astranis, Intuitive Machines, Pacific Fusion.
  - Sacra frames it as a **"lighter PLM front door"** [S](https://techcrunch.com/2026/09/30/valor-atreides-and-sequoia-back-ai-startup-flow-engineering-at-750m-valuation/), [S](https://sacra.com/research/flow-engineering).
  - **This is the "hardware renaissance AI-native change/impact" company, and it is funded and winning the exact ICP.**
- **SPREAD AI:** $30M Series B (Apr 2026; DTCP, IQT, Salesforce).
  - Engineering Intelligence "Product Twin" across PLM/CAD/ERP **"without requiring data migration"**.
  - Customers: BMW, Mercedes, Rheinmetall, MBDA [S](https://vestbee.com/insights/articles/spread-ai-lands-30-m).
  - It occupies the enterprise overlay.
- **CADDi:** $114M at $1.2B (Sep 2026), drawing and manufacturing data AI, launching in the US; more than half of Japan's top 100 manufacturers are customers [S](https://siliconangle.com/2026/09/16/caddi-raises-114m-at-1-2b-valuation-to-bring-manufacturing-ai-to-north-america/).
- **Leo AI:** $9.7M, 50K+ engineers, a copilot over Teamcenter/3DX [S](https://pulse2.com/leo-ai-9-7-million-raised-for-transforming-mechanical-engineering/amp/).
- **CoLab:** $72M (design review), from round 11.
- **Hestus** (YC S24, CAD change propagation) [S](https://theaiinsider.tech/2025/01/31/hestus-receives-1-5m-to-automate-cad-workflows-with-ai-powered-design-assistance/).

**Not found:** "Partful", "Mecha", "Stell", "Vessel", "Revo" and "Kinetic" did not surface as AI-PLM startups [U]. No YC 2025-26 company was found that is explicitly a system-of-record PLM. A DemystifyingPLM episode claims "30+ startups proving PLM disruption is real" [S](https://www.deezer.com/us/show/1002959811), so the space is crowded at the seed level even if the names did not surface.

**Does any AI-native PLM system of record have traction?** No independent one at scale.
- Propel (cloud plus agents) is the closest and is growing.
- Every AI-native company with real traction (Flow, SPREAD, CADDi, Leo) deliberately **avoids being the system of record**.
- [I] The market is telling us that the system-of-record replacement is the wrong product and the overlay is the right one. The overlay is taken.

## 11. Moat at 10 / 100 / 1,000 customers (Q6)
- **10 customers:** none. Connector work is the only asset, and the incumbents own their APIs.
- **100 customers:** some migration mappings and part-classification data. Siemens/Intelizign, PROSTEP and TTPSC already have years of migration tooling.
- **1,000 customers:** a cross-company part/supplier graph is plausible. But SiliconExpert, Octopart/Altium, Assent ($1.3B; see killed thesis Q) and CADDi (a cross-customer drawing corpus) already own component and supplier networks. Customers also resist sharing product data across companies.
- **System-of-record stickiness is real only after cutover.** Reaching cutover is the unsolved problem, and the CAD-PDM lock (Creo↔Windchill, NX↔Teamcenter, CATIA↔ENOVIA) caps a non-CAD PLM at "BOM-only PLM". That ceiling capped Arena (~$50M ARR at exit) and Propel.

## 12. Market math (Q2, Q6)
- **Pool:** CIMdata total PLM was $88.3B in 2025 (+9.9%), but that includes CAD/CAE tools [S](https://www.cimdata.com/en/news/item/30183-cimdata-publishes-executive-plm-market-report). The cPDm slice was not found publicly [U]. The round-11 guess of $15-25B is unverified.
- **ACV anchors:**
  - Arena: about 1,200 customers and about $50M ARR at the 2020 exit, which works out to **~$40K ACV** [S](https://kyodonewsprwire.jp/index.php/release/202012228992).
  - Arena list price: about $3K/user/yr [S](https://www.softwareadvice.com/manufacturing/arena-plm-profile/alternatives/).
  - Enterprise Teamcenter/Windchill: $200K-$5M [U].
- **What each ARR level requires:**
  - **$10M ARR:** 250 × $40K mid-market, or 50 × $200K Agile replacements. Plausible in 4-5 years, in head-to-head competition with Propel, Arena, Aras and Fusion Manage.
  - **$50M ARR:** 1,250 mid-market accounts, which is Arena's entire 2020 base, or 250 enterprise replacements against Siemens/PTC with CAD lock. Hard.
  - **$100M ARR:** 500 × $200K enterprise system-of-record wins. No PLM founded after 2000 except Aras (~$100M+ [U]) has done it independently.
- **Exit comps:**
  - Arena $715M (~14x ARR, 2020 peak multiples).
  - Onshape $470M at near-zero revenue (CAD, not PLM) [S](https://www.sec.gov/Archives/edgar/data/857005/000156459021057806/ptc-10k_20210930.htm).
  - Duro: small undisclosed [U].
  - The "$10B GitHub for hardware" narrative is now attached to Flow ($750M) and CADDi ($1.2B), not to a PLM system of record.

## 13. Expansion
- The story runs: supplier collaboration → NPI → compliance (RoHS/REACH/PFAS) → quality → manufacturing, an "OS for hardware companies."
- Every step is occupied:
  - Compliance: Assent.
  - Quality: Propel and Arena QMS, ETQ.
  - Supplier/drawing data: CADDi.
  - Requirements/V&V: Flow.
  - MES: Tulip ($1.3B).
  - CAD-to-ERP: Siemens/SAP.

## 14. Buyer and sales cycle (Q5)
- Buyer: Director of PLM/Engineering Systems, VP Engineering, and the CIO.
- Sales cycles: 6-18 months for system of record [U]. VARs guard accounts (GoEngineer, TriMech and others resell Dassault/PTC).
- Regulated customers (medtech/A&D, a big share of Agile's base) need validated systems, so startups lose on risk.
- The read-only overlay pilot is feasible in 30-90 days, but it lands as a "nice copilot" against free or bundled incumbent agents.
- Migration difficulty:
  - Customized schemas, CAD vaults and 20 years of change history.
  - AI lowers mapping cost, but validation, cutover and the CAD-PDM link remain human- and vendor-bound [I].
  - Incumbent migration factories exist and now also use automation.

## 15. CTO test sentence
"We'll put an agent next to your Windchill that drafts ECOs and impact analysis, then migrate you off it at a fixed price."
**Likely CTO reply:** "PTC/Siemens just gave us an AI assistant in our license, we just re-signed ePLM for 3 years, and my Creo vault isn't moving. If I want agents across tools I'm looking at Flow or SPREAD."

## 16. Kill test question
"Name 3 of 10 Agile or Windchill owners (non-medtech) who have **not** already chosen a path (Propel, PTC, Siemens, Rimini) and would pilot a startup system of record." Desk evidence says the deciders have already been worked by 5+ vendors, and the Windchill window closed 9/30/2026.

## 17. Five simulated buyers

| Buyer | Response | Why |
|---|---|---|
| Director of PLM, $800M industrial machinery, Windchill + Creo | **NO** | Already migrated to ePLM in Q3 2026. CAD vault lock. Will trial the Windchill AI Assistant first. |
| VP Eng, $300M hi-tech electronics on Agile 9.3.6 | **MAYBE** | Must decide by 2027. Short list is Propel (has agents and Agile migration programs), Arena and Rimini as a bridge. A startup gets an "interesting, but who supports you in 5 years?" |
| Medtech QA/RA + PLM lead on Agile | **NO** | Validated system, FDA audit trail. Will take Rimini plus Propel/Arena, never a seed-stage system of record. |
| Head of Hardware, Series B robotics startup (80 engineers, Onshape + Sheets/OpenBOM) | **MAYBE** | Would try an AI ECO/BOM tool at $10-30K/yr. But Onshape release management, Bild, OpenBOM and Flow compete, and the ACV is small. |
| CIO, $3B auto tier-1 on Teamcenter | **NO** | Teamcenter AI BOM agent plus a Siemens migration factory. SPREAD-type overlay if anything. Will not replace the system of record. |

**Tally: 0 YES / 2 MAYBE / 3 NO.**

## 18. VC committee view
- **Bull:** a forced-replacement window plus agents. System of record is the most valuable enterprise position. Propel's +42% bookings shows replacement demand exists. Flow at $750M shows investors pay for AI hardware engineering.
- **Bear (prevails):**
  - The AI hardware engineering slot was just priced, at Flow ($750M), SPREAD and CADDi ($1.2B), by Sequoia, IQT and Salesforce Ventures. A new entrant pitching "AI PLM" gets compared to them and looks late.
  - PLM system-of-record outcomes historically cap at about $50M ARR / ~$700M exit unless you own CAD.
  - All incumbents bundle agents.
  - Sales cycles are long, VARs gatekeep, and the medtech-heavy Agile base is the hardest segment.
  - **Not a $10B story** unless it becomes Flow.
- **Committee: pass.** Would only revisit with proprietary access (e.g., a founder who ran PLM at a top-20 robotics/EV company with 5 LOIs).

## 19. Red team (strongest case for survival, then rebuttal)
1. *"Incumbent copilots are chat over documents; real agents need a new data model."* Partly true for PTC (its April assistant is Q&A). But Siemens' BOM agent already "executes changes within governed workflows", and Aras/Propel expose MCP. The gap is months, not years.
2. *"Agile's 1,250-1,500 companies are a forced, budgeted list."* Yes, but Propel has run a dedicated "Life Beyond Agile" campaign since 2024-25, and Rimini lets them defer for 15 years. Medtech skew favors validated vendors.
3. *"Startups and the hardware renaissance want a new system of record."* The high-velocity ones chose Flow (overlay) plus Onshape/Arena/Bild/OpenBOM. Startup ACV is $10-40K. That is a SMB PLM business (Arena-scale), not venture-scale fast.
4. *"Migration-as-a-wedge is novel."* SI migration factories (Intelizign, PROSTEP, TTPSC) exist, and AI-assisted mapping is a feature they can add. Fixed-price migration is a services business, low-multiple.

## 20. Kill signals (Q7), observed
- [x] Incumbents ship the wedge feature (Teamcenter AI BOM agent; Arena AI Assistant ECOs; Windchill parts rationalization).
- [x] Funded AI-native players in the overlay slot within 6 months (Flow $50M/$750M, SPREAD $30M, CADDi $114M).
- [x] The only AI-native PLM system-of-record startup (Duro) was absorbed at small scale.
- [x] A forced move with a cheap defer option (Rimini/Spinnaker for Agile; ePLM re-license for Windchill).
- [x] Agile window crowded by Propel/PTC/Autodesk/Aras/Siemens campaigns.
- [ ] Not found: any 2026 practitioner wave of "we're leaving Windchill/Teamcenter for a startup."

---

## 21. Scores

**METHOD template (11):**

| Pain severity | Urgency | Market timing | Speed to pilot | Ease of integration | Ease of reaching customers | Willingness to pay | Competition | Moat potential | Market size | VC attractiveness | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 5 | 4 | 5 | 3 | 3 | 6 | 2 | 5 | 7 | 4 | **4.5** |

**Original bar (11):**

| Pain | Urgency | ROI clarity | Customer accessibility | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 5 | 5 | 3 | 5 | 7 | 6 | 4 | 5 | 5 | 2 | **4.8** |

The score fell from the scan-level 7.1 to 4.8. The biggest drops were Competition (7→2: Flow/SPREAD/CADDi plus incumbent agents), Venture (8→4: the overlay slot is priced, and the system-of-record exit ceiling is about $700M), and Why now (8→5: the Windchill window closed into a re-license, and Agile has a defer option).

## 22. VERDICT: **KILL** (as an AI-native PLM system of record)

**Reframe considered and rejected:** "Agent-led Agile exit for non-medtech hi-tech" is a services/SI wedge competing with Propel's own migration programs. "AI change-impact overlay for robotics/EV" is Flow Engineering. Neither clears the bar.

**Residual lesson (add to STATUS):**
- A legacy-replacement window in 2026 does not open a door for a new system of record when the incumbent re-licenses rather than sunsets, a third-party support defer exists, and AI-native money goes to **overlays that avoid migration** (Flow, SPREAD, CADDi).
- Those overlays get funded first, and fast.
