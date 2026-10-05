# KYI: Know-Your-Importer for customs brokers (deep dive)

**Date:** 2026-10-05. **Origin:** round 13 audit (§2), scored 7.5 there. **Method:** round 7 template. Research used 40 web searches; WebFetch was blocked, so every fact below comes from search snippets.

**Tags:**
- [S] = a search result supports it (URL given; content seen in the snippet only).
- [U] = unverified.
- [I] = inference.
- [M] = from model memory, not re-checked this round.

**Thesis under test:** "A new executive order makes customs brokers liable for the importers they serve. We're the know-your-importer platform. We vet every importer and every shipment (ownership, sanctions, US assets/ability to pay, origin and valuation red flags) with bank-grade AML tech, and we keep the evidence CBP will ask for."

**Bottom line up front:** The trigger is real, dated and penalty-backed. But it is **narrower** than the thesis:
- It applies to **CTPAT-validated brokers** that file for **foreign** importers of record. It does not apply to every broker or every importer.
- The Nov 30 date is the deadline for **CBP to write the implementing rules** (180 days after the EO). It is not a confirmed date by which brokers must comply.

Competition is thicker than the audit found: GingerControl, Gaia Dynamics, Veroot, Tradeverifyd and Descartes. The broker revenue pool is small: about $5.5B of total US brokerage revenue.

**Fresh average: 6.8, down from 7.5.** It fails the 8.5 bar. The best version is not "compliance tool for brokers". It is **"Highway for customs"**: a shared importer-identity and risk network that brokers, sureties and later marketplaces all draw on. That version needs a 14-day test to prove brokers and sureties will share data.

---

## 1. Trigger verification (precise)

| Claimed trigger | Verified? | Exact finding | Source |
|---|---|---|---|
| **EO 14411, "Strengthening Customs Enforcement", Jun 3 2026** | **YES** | Directs DHS/CBP to revise rules for IORs, brokers, forwarders and custodians. DHS is to impose **maximum penalties on brokers that fail to conduct due diligence, repeatedly represent noncompliant clients, or fail to cooperate** with CBP requests for information. It eliminates mitigation for repeat offenders. It sets a **minimum 50% penalty floor** in mitigation unless exceptional national-security circumstances apply. Sec. 2(c): foreign IORs filing formal entries must be **CTPAT-validated or use a CTPAT-validated licensed broker**. | [S] whitehouse.gov/presidential-actions/2026/06/strengthening-customs-enforcement/ ; mofo.com/resources/insights/260617-new-executive-order-signals-broad-customs-enforcement-overhaul ; wilmerhale.com/en/insights/client-alerts/20260610-new-executive-order-on-strengthening-customs-enforcement-what-importers-need-to-know ; morganlewis.com/fr/pubs/2026/07/customs-crackdown-preparing-for-heightened-enforcement |
| **CTPAT Alert to brokers, Aug 12 2026** | **YES** (dated Aug 12 by ct-strategies and Mallory; the CBP PDF filename says 8_13_26) | Applies to CTPAT-validated customs brokers (CVCBs). They "will be expected" to vet **foreign** clients before conducting customs business, covering: legal identity, ownership structure, business affiliates, US assets, compliance and import history, **ability to pay** duties/taxes/fees, supply chain, and **classification, valuation and country of origin**. They must **keep records** of the vetting, POAs and communications. Penalties: financial penalties, more frequent audits, and **suspension or removal from CTPAT**. | [S] cbp.gov/sites/default/files/2026-08/ctpat_alert_-_brokers_8_13_26_pbrb_approved_5662-0826_508.pdf ; ct-strategies.com/?p=16146 ; strtrade.com/.../august/ctpat-validation-will-benefit-brokers-in-new-enforcement-environment-cbp-says ; aaei.org/ctpat-changes-ahead-for-customs-brokers/ |
| **Foreign-importer coverage deadline, Nov 30 2026** | **PARTLY. This is the key correction** | CBP has **180 days to publish implementing regulations**. Jun 3 + 180 days ≈ Nov 30. Vendors and forwarders (Veroot, Carra Globe) market it as "have a CTPAT broker before Nov 30". Law-firm phrasing is "additional DHS/CBP actions required by approximately Nov 30". The compliance date may come later, once a rule is published. The alert's own wording is "in the near future". | [S] securetradeadvisors.com/ctpat-customs-enforcement-executive-order/ ; mallorygroup.com/blog-posts/ctpat-alert-broker-responsibilities-under-eo-14411----what-it-costs-importers ; go.veroot.com/importer-of-record-compliance-guide ; carraglobe.com/customs-enforcement-executive-order-ior-2026/ |
| **CBP voiding IOR numbers since Sep 18 2026** | **YES** | Federal Register notice of Aug 19 2026 (FR 2026-16911) implements EO 14411. It reviews all CBP Form 5106 data. From Sep 18, inaccurate or incomplete IOR data means the number is **voided immediately**, which stops shipments. The physical address, email and phone must belong to the IOR. False statements fall under 18 USC 1001. | [S] govinfo.gov/content/pkg/FR-2026-08-19/html/2026-16911.htm ; akerman.com/en/perspectives/cbp-will-void-importer-of-record-ior-numbers-for-inaccurate-data-starting-septe.html |
| **19 CFR 111.39 / 2022 broker modernization rule** | **Mostly unverified** | The "customer verification" requirement is **TFTEA §116**, proposed as new **19 CFR 111.43, "Importer identity verification"**, in an NPRM of Aug 14 2019. It required 12 data elements at POA time and annual re-verification. One search summary said a final rule appeared in Aug 2026, but its citations pointed to the IOR-voiding notice, so **the final-rule status is [U] and probably conflated**. In the 2019 rulemaking, brokers called the cost estimate "grossly miscalculated". The 2021-22 modernization rule (national permits, CE credits, responsible supervision under 111.28) has no KYC content [M]. 111.39 covers broker duties to inform clients of noncompliance and errors [M]. | [S] govinfo.gov/content/pkg/FR-2019-08-14/html/2019-17179.htm ; freightwaves.com/news/customs-brokers-outline-burdens-of-importer-verification-rule |
| **FCA customs surge ($549.5M, May 2026)** | **YES** | DOJ, May 13 2026: Perfectus Aluminum and affiliates pay **$549.5M**. Aluminum extrusions were disguised as "pallets" to evade AD/CVD (conduct 2011-14). It is **more than 10x the prior customs-FCA record**, coordinated with the DOJ Trade Fraud Task Force. The case targets importers; no broker was charged [I]. | [S] morganlewis.com/pubs/2026/05/doj-announces-major-fca-settlement-relating-to-evaded-customs-duties ; clearygottlieb.com/.../549-5-million-fca-settlement-... ; btlaw.com/en/insights/alerts/2026/the-false-claims-acts-new-frontier |
| **40% transshipment penalty** | **YES, but from a different, older EO** | **EO 14326 (Jul 31 2025)** imposes a 40% additional duty on goods found transshipped to evade reciprocal tariffs. There is no mitigation, it stacks with other duties, and "transshipment" is undefined. Commerce/CBP are preparing a biannual list of high-risk countries and facilities. | [S] swlaw.com/publication/new-reciprocal-tariff-rates-announced-but-the-real-risk-is-hidden-transshipment-... ; sayari.com/resources/blog/transshipment-penalty/ ; e2open.com/blog/navigating-the-transshipment-crisis |

**Additional triggers found:**
- **Sep 2 2026 ANPRM, "Heightened Import Disclosures for Supply Chain Visibility"** (from EO 14411). CBP is weighing:
  - foreign export declarations and certificates of origin;
  - replacing the MID with full identification of supply-chain parties;
  - AI-driven traceability.
  - **Comments are due Dec 1 2026.** This is a second wave that would extend vetting from the importer to the supply chain. [S] federalregister.gov/documents/2026/09/02/2026-17926/heightened-import-disclosures-for-supply-chain-visibility ; bhfs.com/insight/cbp-posts-anprm-regarding-greater-visibility-into-importer-supply-chains/
- **Foreign IORs lose continuous bonds** and must post a single-transaction bond per shipment. Onboarding "stretches from days into weeks". [S] mallorygroup.com (above)
- **Bond insufficiency:** **27,479 cases worth about $3.6B in FY2025**, a record and almost double 2019. Some sureties raised individual bonds by 200%+ in early 2026. [S] torre.news/trump-tariffs-leave-importers-with-record-breaking-35-billion-...; suretyone.com
- **Shell IOR pattern (confirmed):**
  - Shell "importers of record" use up their bond, vanish without insolvency proceedings, and re-form under a new entity.
  - There is a **$112B gap** between China's reported US exports and CBP-recorded imports.
  - This is exactly the cross-broker "hopper" problem a consortium would catch.
  - [S] nbclosangeles.com/news/business/money-report/chinese-exporters-are-offering-sweet-deals-...; idnfinancials.com/news/61647; kelleydrye.com/viewpoints/articles/4-ways-to-help-cbp-curb-shell-co-import-schemes.md
- **"Detective Border."** A White House report proposes AI transshipment detection: routing, ownership links, production capacity, anomaly detection. It names 40+ high-risk countries and puts exposure at $40-303B/yr. **CBP is building the government-side version.** [S] novadata.io/resources/news/cbp-ai-detective-border-transshipment-august-2026 ; exiger.com/perspectives/white-house-transshipment-report-...

**Broker reactions:**
- **NCBFAA** (Secretary Laurie Arnold, via AAEI) calls the change a "substantial expansion of current importer onboarding procedures" that "may require customs brokers to implement more formal client qualification and risk assessment processes". It also introduces IOR "good standing", meaning loss of the right to appoint a broker. Its tone is cooperative ("practical and achievable"). [S] aaei.org/?p=29010
- **Mallory Group:** "brokers are pushing that straight back onto importers". This means the first broker response is **document collection from the client, not buying software** [S/I].
- **STR / CBP** are pitching brokers to get CTPAT-validated: CBP frames validation as a competitive benefit. [S]
- **Supply Chain Dive and JOC:** no EO-14411-specific broker-reaction pieces surfaced in search [U].

---

## 2. Market

| Metric | Figure | Source/quality |
|---|---|---|
| Licensed individual brokers | ~14,454-14,500 | [S] cbp.gov/node/77830 + 2026 secondary source |
| Licensed brokerage firms | ~6,200 (2026 secondary source). NCBFAA has 1,500+ member firms handling ~97% of entries | [S/U]. Active filers are probably ~1,500-2,500 [I] |
| **CTPAT-validated brokers (the regulated subset)** | **Unknown.** CTPAT has ~11,400 partners across all 12 types | [S] reformhq.com/blog/ctpat. Broker share is probably a few hundred to ~1,000 [U] |
| Foreign/nonresident IORs | Unknown. Only nonresident Canadian importers can join CTPAT directly | [S] ct-strategies.com. Likely tens of thousands active [U] |
| Entry summaries | ~2.7-3.1M/month, so **~35M/yr** (FY2025) | [S] strtrade.com monthly CBP stats |
| US customs brokerage revenue | **~$5.5B (2026), 2.9% CAGR.** Forwarders/3PLs hold 65% | [S] mordorintelligence.com/industry-reports/united-states-customs-brokerage-market |
| FMC-licensed OTIs (NVOCCs/forwarders) | Not found. ~5,000-6,000 [M/U] | [U] |
| Customs bond sureties | Concentrated, roughly a dozen active underwriters [M/U] | [U] |

**Budget and willingness to pay:**
- Thin margins.
- Brokers fought the 2019 KYC rule's cost.
- Brokerage fees are compressing.
- Licensed staff now cost 20-30% more than in 2022 [S: Mordor].
- The positive case is **revenue defense**: a CVCB that can vet can keep and win foreign IORs that other brokers drop.

**ACV models:**
- (a) Subscription: $12-60K/yr for mid-size, $100-300K for top-50.
- (b) Per importer vetted: $150-500 onboarding plus $10-30/month monitoring, passed through to the foreign IOR, who already pays more under the EO.
- (c) Per entry monitored: $0.10-0.50.
- (d) Surety underwriting data: per-decision API.
- All prices are [I].

---

## 3. Competitors (searched)

| Player | What it does | Threat to KYI |
|---|---|---|
| **GingerControl** (Austin, $2.1M seed May 2026, Backed VC) | AI trade compliance for importers and **brokers**: multi-client catalogs, per-client policy alerts, per-client audit trail (19 CFR 163.4). Publishes "EO 14411: what it demands from importers" and a "Trade compliance software for customs brokers 2026" buyer guide [S: gingercontrol.com/blog/...] | **High.** Already broker-native, already writing EO 14411 content; one feature away from a "client vetting" tab |
| **Gaia Dynamics** ($7M seed plus an $8.6M SEC filing; AI Fund) | Classification, a Tariff Audits engine over **ACE entry data** (Mar 2026), ~800 accounts including brokerages [S: pulse2.com; runtimewire.com] | **Medium-high.** Already ingests broker entry data; adding entry-pattern risk is adjacent |
| **Veroot** | The #1 CTPAT certification and software vendor, AFA Vendor of the Year 7x. Already runs EO 14411 campaigns ("180-day CTPAT roadmap", "IOR compliance guide") aimed at the same CVCB buyers [S: veroot.com; go.veroot.com] | **High on distribution.** Owns the CTPAT relationship; could bolt on a vetting questionnaire. Also a plausible **partner or acquirer** |
| **Tradeverifyd** | Trade intelligence: 200+ sources, ownership to tier 3, AI agents. Has an EO 14411 blog [S: artofprocurement.com/provider-directory/tradeverifyd] | Medium. A data and ownership layer; brokers are not its core buyer [U] |
| **Descartes** (Visual Compliance: ~2,000 customers, 67,500 subscribers; MyCarrierPortal "Know-Your-Carrier" bought 2024) | Denied-party screening that brokers already use; a KYC-for-logistics precedent [S: dcvelocity.com; sapinsider.org] | **High platform risk.** Its playbook is to buy the winner. A "Know-Your-Importer" product is a natural extension. None found yet |
| **WiseTech CargoWise** (BorderWise; dominant broker OS) | Filing plus a compliance library. No importer-screening module found [S: fullyloaded.com.au; cargowise.com] | High platform risk, but slow to ship [U] |
| Sayari / Kharon / Exiger / Altana / Oritain | Ownership and transshipment data. Exiger has a CBP contract; Altana has CBP Product Passports. They publish content on transshipment and EO 14411 [S] | Medium. Data suppliers more than broker workflow. Conflict on the CBP side for some |
| Alchemize (YC S26), Amari AI ($4.5M, First Round; 30+ customers, $15B of goods), iCustoms ($2.2M), DocUnlock ($3M) | AI-native brokerages and broker automation [S: ycombinator.com/companies/alchemize; techcrunch.com 2026/02/19] | Low-medium. They could build vetting in-house. AI brokerages are also **ideal design partners** |
| **Highway** (FTV growth equity Aug 2025; 1,050 freight brokers, 70 of the top 100) | Carrier identity and fraud for **freight** brokers [S: freightwaves.com/news/carrier-identity-platform] | **The best comp and a threat.** Highway shows a logistics-intermediary identity network can reach growth stage. It could extend from carrier identity to importer identity |
| Generic KYB/AML (Middesk, Baselayer, Persona, ComplyAdvantage, Sardine, Unit21, LexisNexis Bridger, Dow Jones) | Identity, sanctions and AML. None trade-specific [M] | Low as competitors. They are **components**, which hurts Vara's "bank-grade" differentiation |
| AML Watcher, Pelican (TBML for forwarders) | [S: round 13 audit] | Low-medium |

**Is anyone purpose-built for broker importer vetting after EO 14411?**
- **Not found as a named product.** Confidence is moderate: snippet-level only, WebFetch was blocked.
- But at least 4 broker- or CTPAT-native vendors (GingerControl, Gaia, Veroot, Descartes) are each one feature away, and two already market against EO 14411.
- **The market-structure gap is real but the window is short** (1-2 quarters).

---

## 4. Expansion path to venture scale

**(a) Beyond brokers**
- **Customs sureties.** The $3.6B insufficiency problem plus per-shipment bonds for foreign IORs makes sureties the best-funded second buyer.
- **AI-native brokerages and digital forwarders** (Flexport-class).
- **Marketplaces** with DDP foreign sellers: INFORM Act seller verification [M].
- **Freight brokers:** Highway owns this.
- **Customs-bond-backed lenders and trade finance:** Vara AML/SAR fits here, but these are banks, which the founders want to avoid.

**(b) Beyond the US**
- The **new EU Union Customs Code entered into force Sep 20 2026**.
- The **EU Customs Data Hub** goes live for e-commerce on **Jul 1 2028** (all goods by 2034).
- **Platforms become the "deemed importer"**, liable for duties and compliance, from 2028.
- This creates a genuine second mandate: platform KYB of foreign sellers for customs. [S] cassidylevy.com/news/the-eus-largest-customs-overhaul-...; fieldfisher.com
- UK: [U].

**(c) From vetting to a trade financial-crime platform**
- Transshipment and undervaluation detection over the broker's entry data.
- Cross-broker shell-IOR detection.
- Evidence for prior disclosures.
- This competes with the government-side "Detective Border", Exiger and Altana [I].

**Is "AML for non-bank intermediaries made liable by regulators" a $1B+ category?**
- **Mixed.** In the **FinCEN** world the trend is **retreating**:
  - the residential real-estate rule was **vacated by a Texas court on Mar 19 2026**;
  - the investment-adviser AML rule was **postponed to Jan 1 2028** and its scope is being revisited [S: mofo.com/pdf/resources/insights/260108-fincen-hits-pause-...; jdsupra].
- **Trade-enforcement** mandates are **advancing** (EO 14411, the ANPRM, the EU deemed importer).
- The EU AMLR (applies Jul 2027) expands obliged entities [M].
- So the category exists as a **pattern**: Highway (freight brokers), Descartes MCP (carriers), Persona/Middesk (marketplaces). But each sub-vertical is a mid-size company. Reaching $1B+ requires **owning identity across several intermediary types** [I].

---

## 5. Buyer, sales cycle, pilot

**Buyer:**
- Owner, or compliance manager or licensed broker of record, at a CTPAT-validated broker with a foreign-IOR book (Canadian/Mexican nonresidents, Chinese DDP e-commerce sellers).
- The economic buyer at small firms is the owner. At top-50 firms it is the VP of compliance.

**Sales cycle:**
- SMB brokers: 2-6 weeks.
- Top-50 brokers and forwarders: 3-9 months, with IT and CargoWise integration questions [I].

**Pilot (14-30 days):**
1. Ingest the client list, POA files and 12 months of ACE ES-003/entry reports.
2. Score every foreign IOR against the alert's 8 fields:
   - identity, ownership and affiliates (KYB plus sanctions);
   - US assets and bond sufficiency (ability to pay);
   - Form 5106 accuracy (void risk);
   - origin and valuation plausibility (unit-value outliers vs lane peers, transshipment lanes, HS shifts).
3. Output a ranked list, field gaps and a CBP-ready dossier per IOR.

**Success criteria:**
- at least 5 IORs the broker agrees to drop or remediate;
- counsel accepts the dossier;
- at least 1 IOR flagged with a Form 5106 defect before CBP voids it.

**Willingness-to-pay evidence:**
- **None direct.** No price points for broker vetting surfaced.
- Indirect positive: CBP and NCBFAA both say formal risk-assessment processes are needed. Foreign IORs face weeks of onboarding delay, so a "fast verified onboarding" product has a payer: the IOR.
- Indirect negative: the 2019 cost pushback, a thin-margin industry, and "push it back on the importer".

---

## 6. Moat and market math

**Moat by customer count:**
- **10 customers:** labeled outcomes (which flagged IORs later drew CF-28/29s, voids or penalties). Modest.
- **100 customers:** a **cross-broker importer identity graph**. Shell IORs that "use up the bond, vanish, re-form" [S] and hop brokers become visible: shared directors, addresses, phones, emails, the same foreign shipper, the same bank. This is the Sardine/Alloy/Highway consortium pattern, and the only real moat. Risk: brokers are competitors and may refuse to share client data. Highway shows freight brokers *did* share carrier data, but carriers are not their clients [I].
- **1,000 customers** (brokers plus sureties plus platforms): a de-facto "importer good-standing" score consumed by sureties for underwriting and by platforms for EU deemed-importer KYB. **Risk: CBP itself owns "good standing"** (an EO concept) and is building Detective Border.

**Market math [I]:**
| Scenario | Composition | ARR |
|---|---|---|
| Brokers only, realistic | 300-600 CVCBs × $20-30K plus 30 top brokers/forwarders × $150K | **~$10-22M** (the $10M ARR path; needs ~40% of CVCBs) |
| Plus IOR pass-through and sureties | +30-60K foreign IORs × $300-600/yr; +5-8 sureties × $0.5-2M | **~$25-55M** (the $50M path) |
| Plus EU deemed-importer platforms (2028+), forwarders/NVOCCs, AI brokerages, trade-finance AML | +marketplaces × $0.5-3M; EU brokers/representatives | **$100M+** only after 2028 and outside brokers |

**Sanity check:** $5.5B of brokerage revenue × 1-2% tech/compliance spend ≈ $55-110M for the broker segment *in total* [I]. That is a ceiling, not a venture outcome.

**VC view:**
- $10B? Not from brokers.
- Plausible outcome: $300M-1.5B if it becomes the importer-identity network across brokers, sureties and EU platforms (Highway-like).
- Comps:
  - Persona ~$2B (2025) [M]
  - Alloy $1.55B (2021) [M]
  - Sardine ~$70M Series C (2025) [M]
  - Middesk Series B (2021) [M]
  - ComplyAdvantage [M]
  - Altana ~$1B (2025) [M]
  - Highway growth equity (undisclosed) [S]
- Most likely exit: acquisition by Descartes, WiseTech or e2open (Descartes paid $250M for Visual Compliance) [S: dcvelocity.com].

---

## 7. Interesting or dull? Framing

- **Dull framing:** "CTPAT broker vetting checklist plus dossier." This is a feature, priced like Veroot.
- **Exciting framing:** "**The identity layer for who is allowed to import.**"
  - Tariffs made the IOR slot a $100B+ fraud target (a $112B China export gap).
  - Shell importers burn bonds and re-form.
  - Regulators on both sides of the Atlantic just made intermediaries (US brokers now, EU platforms in 2028) liable for knowing who they import for.
  - "Highway did it for carriers; we do it for importers."
- **One-sentence VC clarity:** "Tariff evasion runs through disposable shell importers. Washington just made brokers liable for spotting them. We are the shared importer-identity network brokers, sureties and marketplaces check before a container moves."
- **Verdict on interest:** directionally interesting and VC-legible, but in a narrow, mandate-dependent first market.

---

## METHOD template (all fields)

**Problem.**
- CTPAT-validated brokers must soon vet every **foreign** IOR on 8 fields and keep proof.
- Failure means maximum penalties, no mitigation for repeat offenders, a 50% penalty floor, more audits, and CTPAT removal, which in turn means losing the right to file for foreign IORs.
- Separately, any IOR (domestic too) with bad Form 5106 data is voided on sight from Sep 18.
- Underneath sits the shell-IOR fraud wave and bond insufficiency.

**Recent evidence (7 independent signals).**
1. EO 14411 text and 4+ law-firm alerts (MoFo, WilmerHale, Morgan Lewis, Quarles) [S].
2. CBP CTPAT broker alert PDF (Aug 12-13) [S].
3. Aug 19 FR notice and IOR voiding from Sep 18 (Akerman, Cassidy Levy, GHY) [S].
4. NCBFAA statement calling for "formal client qualification and risk assessment processes" [S].
5. Sep 2 ANPRM on supply-chain disclosures, comments due Dec 1 [S].
6. Bond insufficiency of $3.6B (FY2025) and per-shipment bonds for foreign IORs [S].
7. The Perfectus $549.5M FCA settlement and the shell-IOR fraud coverage (CNBC-syndicated) [S].

**Who has the pain.**
- Primary: CVCBs with foreign-IOR books (count [U]).
- Secondary: all brokers (Form 5106 accuracy), sureties, foreign IORs stuck in weeks-long onboarding, AI-native brokerages.

**What they do today.**
- POA packets, Google, D&B and Secretary-of-State lookups.
- Descartes Visual Compliance for denied-party screening.
- Spreadsheets and emails to clients ("push it back on the importer").
- Trade counsel and CTPAT consultants (Veroot).

**Why current products fail.**
- DPS tools answer "is this party sanctioned?"
- KYB tools answer "does this company exist?"
- Neither answers "can this foreign IOR pay a 40% transshipment assessment?", "is this declared origin and value plausible for this lane?", "is this IOR a re-formed shell another broker dropped?", or "show me the dossier".
- Broker operating systems file entries; they do not risk-score clients [U].

**Why now.**
- EO Jun 3, alert Aug 12, FR notice Aug 19, voiding Sep 18, ANPRM Sep 2.
- Implementing rules are due around Nov 30; ANPRM comments are due Dec 1.
- EU UCC in force Sep 20; Data Hub 2028.

**Potential product (Vara assets mapped).**
1. **Onboarding:** importer KYB plus sanctions (Vara AML screening), plus liveness and document checks on the POA signer (biometrics SDK), plus voice challenge for phone-originated changes (deepfake detection).
2. **Monitoring:** rules engine over ACE entries for unit-value outliers, lane and transshipment patterns, HS drift, new-shipper bursts, and bond-utilization velocity (Vara rules engine).
3. **Evidence:** a timestamped dossier per IOR and per alert (Vara evidence ledger and regulatory workspace, retargeted from SAR to "CBP due-diligence file" and prior-disclosure packs).
4. **Import of existing vendor data:** Descartes DPS exports, CargoWise client lists (Vara import/mapping).
5. **Network:** a cross-broker shell-IOR graph.

**Time to value.** 1-2 weeks on CSV/ACE reports.

**Pilot (14-30 days).** See §5.

**Willingness to pay.** Unproven. Estimate $12-60K per mid-size broker plus IOR pass-through. The negative signals are strong (§5).

**Expansion.** See §4: sureties, then AI brokerages and forwarders, then EU deemed-importer platforms (2028), then trade-finance AML.

**Competition.** See §3. Nobody has the named product, but GingerControl, Gaia, Veroot and Descartes are each a feature away, and Highway is a pattern-adjacent threat.

**Moat (10/100/1,000).** See §6. The consortium is the moat, but only if competitors share data.

**CTO/CEO test sentence (broker owner).** "If CBP audits my foreign-IOR book tomorrow, I can hand them a dossier per client, and I already know which eight clients are re-formed shells another broker dropped."

**Kill test question.** "Before Nov 30, will you pay ≥$20K/yr for software, rather than send your clients a document checklist, and will you let us match your clients against other brokers' dropped clients?"

### METHOD scores (1-10)
| Category | Score | Note |
|---|---|---|
| Pain severity | 7 | Real penalties, but scoped to CVCBs × foreign IORs. Brokers can push work onto clients |
| Urgency | 8 | Dated events, but Nov 30 is a rulemaking deadline and could slip |
| Market timing | 9 | 2026 trigger cluster plus EU 2028 |
| Speed to pilot | 8 | CSV/ACE ingest |
| Ease of integration | 8 | No integration for v1; CargoWise later |
| Ease of reaching customers | 6 | NCBFAA/CTPAT channels exist; founders have no logistics network; Veroot owns the CTPAT relationship |
| Willingness to pay | 5 | No direct evidence; historic pushback |
| Competition | 6 | No named product, but 4 vendors a feature away; Highway pattern |
| Moat potential | 6 | Consortium plausible but unproven; CBP owns "good standing" |
| Market size | 5 | Brokerage revenue $5.5B, so the broker software pool is under ~$110M |
| VC attractiveness | 6 | Legible as "Highway for importers", but exits look like Descartes roll-ups |
| **Average** | **6.7** | |

### Original bar scores (11)
| Category | Audit | **Now** | Why changed |
|---|---|---|---|
| Pain | 8 | **7** | Scope narrowed to CVCBs × foreign IORs; "push back to importer" |
| Urgency | 9 | **8** | Nov 30 is the date for CBP's rules, not confirmed broker compliance |
| ROI clarity | 7 | **6** | No price or WTP evidence; ROI is probabilistic |
| Customer accessibility | 7 | **7** | Unchanged |
| Pilot speed | 8 | **8** | Unchanged |
| Market size | 7 | **5** | $5.5B brokerage pool; CVCB count unknown |
| Expansion | 8 | **7** | EU 2028 deemed importer verified (+); FinCEN non-bank mandates retreating (−) |
| Venture potential | 7 | **6** | Highway is a decent but not $10B comp |
| Defensibility | 6 | **6** | Unchanged; shell-IOR hopping verified (+), CBP "good standing" and Detective Border (−) |
| Why now | 9 | **9** | Verified, plus ANPRM and EU UCC |
| Competition position | 7 | **6** | GingerControl, Gaia, Veroot, Tradeverifyd surfaced |
| **Average** | 7.5 | **6.8** | Fails 8.5. Four categories below 7 |

---

## Simulated buyers (5)
1. **Owner, 25-person CTPAT broker in Laredo (Mexican nonresident IORs, ~120 clients). MAYBE→YES.** "I lose those clients if I lose CTPAT. $1-2K a month is fine if it produces the file CBP wants, and I can bill the IOR a vetting fee." Concern: "Will CBP accept your dossier?"
2. **VP Compliance, top-20 broker/forwarder (CargoWise shop). MAYBE.** "We'll build a checklist in CargoWise workflows and use Descartes for DPS. The entry-pattern monitoring is interesting if it plugs into CargoWise. Pilot yes, budget next fiscal year." Also: "I will never share client lists with competitors."
3. **Compliance manager, LA broker with Chinese DDP e-commerce IORs. YES.** "Half these IORs are shells. I need to know which ones before CBP voids them and leaves me holding the penalty. The shell-hopper match is the thing I'd pay for."
4. **Small non-CTPAT broker (8 people). NO.** "This only applies to CTPAT brokers with foreign clients. I'll stop taking foreign IORs." This is the scope-narrowing effect.
5. **Underwriting head, customs surety. MAYBE→YES (best buyer).** "Bond insufficiency is killing us and foreign IORs now need per-shipment bonds. An importer risk score from entry behavior plus a shell-entity graph is worth real money, but I need coverage across many brokers first."

**Tally:** 2 YES, 2 MAYBE, 1 NO. The strongest pull is from **shell-IOR detection** and **sureties**, not the checklist.

---

## VC committee view
- **Partner A (fintech/identity), for:** "Classic regulation-pushes-KYC-onto-intermediaries wedge. Sardine and Alloy took this path for fintechs, Highway for freight brokers. The team has AML, SAR and biometrics already built, so it ships in weeks. The shell-IOR network is the moat. EU deemed-importer in 2028 is the second act."
- **Partner B (supply chain), against:** "The customs broker software market is small and owned by WiseTech and Descartes, who buy winners for $100-300M. The mandate is an executive order. One administration change or a slipped CBP rule and urgency evaporates. CBP is building Detective Border itself. Brokers don't share data."
- **Partner C (seed generalist):** "Fund only if the 14-day test shows (a) brokers or sureties pay or sign LOIs before the CBP rule lands, and (b) at least 3 brokers agree to shared matching. Otherwise it's a nice $10-20M ARR business for a strategic."
- **Committee outcome:** **Pass at Series A; possible seed** if the network proof exists. It is not a $10B story on current evidence.

---

## Red team
1. **Scope inflation.** The thesis says "vet every importer and every shipment". The mandate covers CVCBs × **foreign** IORs. Domestic IORs carry only Form 5106 accuracy (voiding) and general broker care duties.
2. **The deadline is soft.** Nov 30 is CBP's rulemaking deadline. Rules slip routinely, so urgency could move into 2027.
3. **Path of least resistance.** Brokers respond with a document checklist pushed to clients ("pushing that straight back onto importers") and drop risky foreign IORs. Neither needs software.
4. **Incumbent feature risk.** Veroot (CTPAT owner), GingerControl and Gaia (broker-native, EO-aware), and Descartes (DPS plus a "Know-Your-Carrier" precedent) can each ship a vetting tab in a quarter.
5. **CBP becomes the network.** EO "good standing", Form 5106 voiding and Detective Border make the government the importer-risk registry, which could commoditize the consortium.
6. **Data-sharing taboo.** Brokers compete for the same clients, so a cross-broker match needs a privacy-preserving design (hashing, Sardine-style). That is unproven in this industry.
7. **Political mandate risk.** EO-based, tariff-linked policy can reverse with courts or administrations. FinCEN rules were just vacated or delayed; trade policy could be next.
8. **Vara edge is partly generic.** Sanctions screening, KYB and liveness are commodity APIs. The real customs edge (origin and valuation plausibility, transshipment) requires trade data Vara does not have (Panjiva, ImportGenius, Sayari licensing).
9. **Founders have no logistics network.** Veroot, AFA and NCBFAA relationships matter.
10. **Banks are the natural expansion (TBML)**, and the founders don't want them.

## Kill signals
- In 10 calls with CVCB owners, fewer than 3 say they would pay ≥$15K before the rule lands, or most say "checklist plus drop clients".
- Veroot, GingerControl, Gaia or Descartes announces an EO 14411 client-vetting module before Dec 2026.
- The CBP implementing rule is delayed past Q1 2027, or it lets brokers rely on IOR self-certification.
- Brokers refuse cross-broker matching even in hashed or privacy-preserving form, and sureties won't pay without it.
- CBP publishes a shared "good standing" or IOR-risk list that brokers can query for free.
- The CVCB count turns out to be under ~300.

---

## VERDICT
**DOWNGRADED NEAR-MISS: 6.8, from the audit's 7.5. It fails the 8.5 bar.**

The trigger is verified and real. But it is:
- narrower than pitched (CTPAT brokers × foreign IORs);
- softer on timing (Nov 30 is CBP's rulemaking deadline);
- on a small revenue pool ($5.5B brokerage);
- contested by four feature-away vendors.

**What survives is not the broker-compliance tool. It is the "Highway for importers" network:**
- shell-IOR detection across brokers;
- sold to brokers first, then to **customs sureties** (the best-funded buyer, facing $3.6B in insufficiencies);
- then to EU deemed-importer platforms (2028).

**Recommendation:** run a **cheap 14-day test only if it targets the network thesis**:
- 6 CVCBs (Laredo/LA/Miami, foreign-IOR heavy);
- 2 AI-native brokerages (Alchemize, Amari) as design partners;
- 3 customs sureties;
- 1 call with Veroot about partnering.

**Pass criteria:**
- at least 2 brokers plus 1 surety sign LOIs at ≥$20K;
- at least 3 brokers agree to hashed cross-broker matching;
- a back-test of one broker's 12-month entries finds at least 5 IORs the broker agrees are shells or high-risk.

**Otherwise kill it.** Do not build the dossier tool alone; it is a feature Veroot or Descartes will ship.
