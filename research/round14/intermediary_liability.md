# Round 14: New liability on non-bank intermediaries (scan + top-2 deep dive)

**Date:** 2026-10-05. **Method:** round7/METHOD.md template plus the original 11-category bar. **Searches:** 40 of 40 (WebFetch and Reddit blocked, so every fact comes from search snippets only).

**Tags:**
- [S] = a search snippet supports it (source named).
- [U] = unverified.
- [M] = model memory, not re-checked.
- [I] = inference.

**The question.** STATUS.md found that new liability placed on *intermediaries* was the one area (EO 14411, customs brokers) where a 4-month-old mandate still had no purpose-built vendor. Does the same pattern hold elsewhere? We scanned 2025-26 mandates that put new verification, monitoring or reporting duties on non-bank intermediaries and platforms.

**Bottom line up front:**
- **The pattern holds only partly.** Where the liable intermediaries are a few giants (VLOPs, app stores, the AU under-16 ban, TAKE IT DOWN), they build the capability themselves or trust-and-safety vendors already sell it.
- **Where the liable entities are many and mid-sized and the mandate is new** (AUSTRAC Tranche 2, EU AMLR, FTPF, DROP), generic AML or GRC vendors re-badged their products within months.
- **Two pockets remain where no purpose-built vendor was found and Vara's stack fits closely:**
  1. **Scam liability moving onto telcos and platforms** (Australia SPF, in force 31 Mar 2027; EU PSR platform liability).
  2. **KYC plus traffic monitoring for originating voice providers** (FCC; the KYC rule is still *proposed*).
- **Neither clears the 8.5 bar.** Best: SPF telco "scam-liability ledger" at **6.6**. Voice-provider KYC: **6.2**.

---

## 1. Mandate scan (verification status, liability, vendors, gap)

| # | Mandate | Obligation | Who is liable (how many) | Dates | Penalty | Existing vendors | Gap | One-sentence startup | Vara fit |
|---|---|---|---|---|---|---|---|---|---|
| 1 | **Australia Scams Prevention Framework (SPF)**. Act passed 13 Feb 2025 [S]. Draft Common, Telco, Banking and Digital Platforms Codes and SPF Rules released 28 May 2026; consultation closed 25 Jun [S: Ashurst, Corrs, HSF, Baker McKenzie]. One snippet says the SPF Rules commenced 1 Sep 2026 [S, single source; U]. | Codes turn 5 of 6 principles (governance, prevent, detect, disrupt, respond) into civil-penalty duties [S]. "Actionable scam intelligence" must be reported to the ACCC, with reasonable steps to investigate within 28 days [S]. Platforms must verify advertiser identity against government records and block unlicensed financial-services ads [S]. Messaging codes cover 7 named services (WhatsApp, Telegram, WeChat, iMessage, FaceTime, Google Messages, Meet) [S; possibly conflated with Singapore OCHA codes, so U]. Proposed **A$3,000 auto-reimbursement** threshold [S]. **AFCA** becomes the single EDR scheme for bank, telco and platform scam complaints and can **apportion liability across bank, telco and platform** [S: HWL Ebsworth, Mallesons, Ashurst]. The apportionment guidelines are not yet released [S]. | Banks; telcos (carriage service providers); digital platforms (social media, paid search ads, direct messaging) [S]. Telco count [U]: 3 large, about 20-40 mid-tier and MVNO, a long tail of hundreds of small CSPs [I]. A new public CSP register is coming [S: Mallesons]. | Full effect **31 Mar 2027** [S] | **Up to A$50M per contravention** or 30% of turnover [S], plus multi-regulator enforcement and a **private right of action** [S] | Bank side is crowded: NICE Actimize, Outseer, BioCatch, Feedzai [S/M]. Telco network side: Apate.ai (A$1.6M seed; TPG uses it to block ~10K scam calls a day) [S], Mobileum, TNS, Hiya [M]. Netcraft publishes an SPF readiness checklist (takedown and brand protection) [S]. AFCX Intel Loop is the existing cross-sector intel channel (banks, telcos, social media, NASC) [S]. | **No vendor found selling SPF compliance to telcos or mid-tier platforms**: ASI reporting, a per-complaint "reasonable steps" evidence file for AFCA apportionment, and code-mapped controls. Telcos already run C661 call blocking [S]. What is new is **liability and evidence** [I]. | "The scam-liability ledger for telcos: detect, report ASI to the ACCC, and defend every AFCA complaint with a timestamped evidence file." | **Very high**: regulatory filing, evidence ledger, voice deepfake/scam-call detection, transaction-rules engine. Telco buyer, not a bank. |
| 2 | **EU Payment Services Regulation (PSR/PSD3)**. Political deal 27 Nov 2025 [S: EP press release, William Fry, Sumsub]. | **Online platforms become liable to PSPs** that reimbursed fraud victims if the platform was notified of fraudulent content and did not remove it [S]. Impersonation-fraud refunds by PSPs [S]. Cooperation with electronic communications providers [M]. | Online platforms (scope tied to DSA) [I]; PSPs | Application date [U] (likely around 2028 [I]) | Civil liability to PSPs [S] | DSA notice-and-action vendors (Tremau, Checkstep) [M] | **No vendor found** turning a bank's fraud claim into proof of platform notice and failed removal, or the reverse defense for platforms [I] | "Claims clearinghouse between banks and platforms for PSR fraud-content liability." | High (evidence ledger), but the bank side is the claimant. Expansion route for #1 |
| 3 | **FCC robocall: KYC / KYUP / RMD / STIR-SHAKEN** | Third-party authentication: providers must sign calls with their own certificate. **In force 18 Sep 2025** [S: Mintz]. RMD-integrity order effective **5 Feb 2026** [S]. **KYC FNPRM, 30 Apr 2026 (proposed):** collect and verify name, address, government ID and alternate phone before service; extra diligence for high-volume customers; **$2,500 per-call base forfeiture**; a possible **safe harbor for AI/automated KYC** [S: DWT, Telecompetitor, DLA]. KYUP and STIR/SHAKEN FNPRM 20 May 2026 [S]. RMD expansion FNPRM 23 Jul 2026 [S]. | Originating voice service providers, gateways and intermediates. **2,411 RMD filers** cited in a 2024 show-cause order [S; may be a subset]. About 1,200 removed in Aug 2025 [S], 14 more removed 2 Sep 2026 [S]. | KYC rule **not final** [S]. Third-party authentication in force | Removal from RMD means downstream carriers must block all traffic (corporate death) [S/M]. $2,500 per call proposed | TransNexus (NexOSS), Neustar/TransUnion robocall mitigation [S]. Didit already markets FCC voice KYC [S]. Numeracle, ZipDX, Twilio Trust Hub, The Campaign Registry for 10DLC [M] | Partial: network analytics exists. **"AML-style" customer vetting plus per-customer traffic monitoring plus a traceback/RMD evidence file for small UCaaS/CPaaS resellers** is thin [I] | "Know-your-caller-customer: KYB, sanctions and Covered-List screening plus traffic-pattern monitoring and a traceback evidence file for VoIP originators." | **High**: KYB and sanctions screening, rules engine over call records, voice AI-clone detection on outbound traffic, evidence ledger |
| 4 | **TAKE IT DOWN Act (US)** | Notice-and-removal process; remove NCII within **48h**; prevent re-upload [S] | Every covered platform hosting user-generated content (thousands) [I] | FTC enforcement since **19 May 2026**; FTC warning letters; TakeItDown.ftc.gov complaint portal [S] | FTC Act unfair or deceptive practice penalties [M] | Hive, Checkstep, ActiveFence (now "Alice") with a TIDA product page [S]. StopNCII hashing [M] | Small: crowded trust-and-safety category | "48h NCII removal SLA-as-a-service for mid-size UGC apps." | Low (image hashing, not fraud) |
| 5 | **US app-store age verification** (Utah Mar 2025; Texas SB2420) | App stores verify age and get parental consent; developers consume age signals [S] | Apple, Google, plus developers using the signals | Texas: district court enjoined it Dec 2025; **the Fifth Circuit stayed the injunction, so the law took effect around Jun 2026** [S: MoFo]. Apple and Google comply via Declared Age Range and age-verification tools [S] | State AG enforcement and private actions [M] | Apple and Google native; Yoti, k-ID, Persona [M] | Platforms absorb it | none | Low |
| 6 | **Australia under-16 social media ban** (SMMA, in force 10 Dec 2025) | Reasonable steps to stop under-16 accounts [S] | About 10 named platforms [M] | Live; 4.7M accounts removed; eSafety investigating FB, IG, Snap, TikTok, YouTube [S] | A$49.5M [S] | Yoti, k-ID, platform in-house [M] | Giants build it | none | Low-medium (behavioral biometrics for age inference, but the buyers are giants) |
| 7 | **UK Online Safety Act** (illegal harms Mar 2025; child safety/age assurance Jul 2025) [M] | Risk assessment, age assurance; Category 1 fraudulent-advertising duty later [M] | About 100K services [M] | Live [M] | 10% of global turnover [M] | Crowded: Yoti, Persona, Tremau, Checkstep, Unitary [M] | Crowded | none | Low |
| 8 | **EU DSA**: Art 30 KYBC trader traceability; VLOP systemic risk | Collect and verify 6 trader data points; self-declaration is not enough [S] | All EU marketplaces (Art 30); about 25 VLOPs | Live; **Temu fined €200M on 28 May 2026** (systemic-risk assessment of illegal products; action plan due 28 Aug 2026) [S: EC IP/26/1178, Lewis Silkin]; Shein investigated incl. Art 30 [S] | 6% of turnover [S/M] | KYB vendors: Sumsub, Onfido, Persona, Trulioo, Middesk; seller-verification at Amazon in-house [M] | Generic KYB covers it | none (a feature) | Medium (KYB), crowded |
| 9 | **INFORM Consumers Act (US)** | Verify high-volume sellers (200+ sales and $5K in 12 months) [S] | Marketplaces | In force Jun 2023; **first FTC case: Temu, $2M, Sep 2025** [S] | Civil penalties [S] | Same KYB vendors [M] | Weak enforcement; crowded | none | Low |
| 10 | **EU customs reform** (deal 26 Mar 2026) | Platforms are the **deemed importer**; real-time sales data to the EU Customs Data Hub; €2 handling fee from 1 Nov 2026 [S] | Marketplaces selling into the EU | Fee Nov 2026; deemed importer around 2028 [S/M] | Customs debt | Customs software (Descartes, e-commerce DDP providers) [M] | Covered in round 13 KYI ("Highway for importers", 2028 act) | see KYI | Medium |
| 11 | **FMCSA broker financial responsibility** | $75K bond or trust; suspension if not replenished within 7 business days; surety notice within 2 days [S] | About 30K+ brokers [M] | **16 Jan 2026** [S]. Motus registration with identity and business verification rolled out 19 May 2026; Idemia does identity checks [S] | Authority suspension [S] | Highway, Carrier Assure, RMIS, Truckstop, NMFTA SCAC Verified [S/M] | Freight fraud is crowded (STATUS already notes Highway) | none | Medium; crowded |
| 12 | **FinCEN non-bank rules** | Investment adviser AML rule **delayed to 1 Jan 2028** [S: MoFo, GT]. Residential real estate rule **vacated 19 Mar 2026** [S] | ~ | Retreating | ~ | ~ | US non-bank AML is shrinking | none | ~ |
| 13 | **AUSTRAC Tranche 2** | AML/CTF programs, CDD, SMRs and records for lawyers, accountants, real estate, conveyancers, TCSPs, precious-metal dealers [S] | **About 80,000+ businesses** [S] | Live **1 Jul 2026**; enrolment by 29 Jul 2026 [S] | AML/CTF Act civil penalties [M] | Crowded already: VinciWorks, NameScan, Moody's, Zyphe, Ble, First AML, InfoTrack, Arctic Intelligence [S/M] | Vendors landed before go-live | none (late) | High tech fit, but the buyers are small professional firms. Crowded |
| 14 | **EU AMLR** | New obliged entities: high-value goods traders (>€10K), crowdfunding; football clubs and agents in 2029 [S] | Tens of thousands [I] | **10 Jul 2027**; football 10 Jul 2029 [S] | AMLR sanctions [M] | AML Watcher, Ble and generic KYC vendors are already marketing to it [S] | Same pattern as Tranche 2; football clubs are a small niche | "AML for football transfers (2029)": niche | High fit, but small or early |
| 15 | **UK ECCTA failure to prevent fraud** | Large orgs (250+ staff / £36M turnover / £18M assets) need "reasonable procedures" [S] | Thousands of UK large organisations [I] | In force **1 Sep 2025** [S]. **No prosecutions or confirmed investigations as of Mar 2026**; SFO "very, very keen" [S] | Unlimited fine [M] | Mitratech (GRC) marketing it [S]; Big-4 and law firms; VinciWorks training [M] | The buy is a policy plus training plus a GRC module. No fraud-detection mandate | "Continuous FTPF control-evidence monitor": weak until a first prosecution | Medium (evidence ledger), but no forcing event yet |
| 16 | **California Delete Act / DROP** | Data brokers process DROP deletion lists every 45 days [S] | **600+ registered data brokers** [S] | **1 Aug 2026** [S] | $200/day per unprocessed request [S] | TrustArc, UnsubCentral guides; privacy vendors [S] | Small, privacy not fraud | none | Low |
| 17 | **EU AI Act deployers** | High-risk obligations deferred to **2 Dec 2027** (stand-alone) and **2 Aug 2028** (embedded); Art 50 transparency held at 2 Aug 2026 [S: Sidley, Pinsent Masons] | All deployers | Omnibus approved by EP 16 Jun and Council 29 Jun 2026 [S] | AI Act fines | Crowded AI-governance category (Credo, Holistic AI, OneTrust) [M] | Crowded and delayed | none | Low |
| 18 | **US state AI laws** | Colorado AI Act **repealed and replaced** by SB 26-189 (signed 14 May 2026); notice and disclosure on automated decisions; effective **1 Jan 2027** [S] | Deployers | 2027 | AG enforcement | GRC vendors | Weaker duties | none | Low |
| 19 | **UK APP fraud reimbursement** (PSR) | PSPs reimburse; £173M paid Oct 2024-Sep 2025 [S]. A **cross-sector liability review** (telcos, platforms) is under discussion for Q2 2026 [S: bratby.law, single source; U] | PSPs now; telcos and platforms possibly | Telco/platform liability **not enacted** [S/I] | ~ | Bank-side vendors | Pre-mandate | Expansion target for #1 | High once enacted |
| 20 | **India Telecom Cyber Security Amendment Rules 2025** (G.S.R. 771(E), 22 Oct 2025) | Creates **TIUEs** (non-telecom entities using mobile numbers to identify customers: fintech, OTT, logistics) and a government **Mobile Number Validation platform**; government can order TIUEs to suspend identifiers [S] | Potentially thousands of Indian apps [I] | Notified Oct 2025; MNV platform operational status [U] | Telecom Act penalties [M] | Government-run MNV platform [S]; Indian KYC stacks [M] | The government platform *is* the product | none | Low (government utility) |
| 21 | **FCC SIM-swap / port-out rules** (Nov 2023 order; compliance mid-2025 [M]) | Secure authentication before SIM change or port-out; notify customers [M] | Wireless carriers and MVNOs | In force [M] | FCC forfeitures | Prove, Telesign, Pindrop, carriers in-house [M] | Covered in round 12 (caller-verification wedge) | see round 12 | High (voice) |

**Not checked (search budget):** Japan Mobile Software Competition Act app-store duties (Dec 2025 [M]); Canada (no new non-bank verification mandate identified [U]); Singapore OCHA codes (excluded from the jurisdiction list).

**Scan conclusions:**
1. **Mandates on a handful of giants** (rows 4-8, 17) are absorbed by the giants or by trust-and-safety and KYB incumbents.
2. **Mandates on many small professionals** (rows 13-16) were met by generic AML or GRC vendors *before* go-live. Tranche 2 had vendors marketing a year early.
3. **US non-bank AML is retreating** (row 12). Colorado retreated too (row 18).
4. **The only rows where liability is new, an identifiable mid-sized intermediary carries it, and no purpose-built vendor was found are the scam/fraud-liability shift onto telcos and platforms (rows 1, 2, 19) and voice originators (row 3).** Both sit in Vara's voice and fraud core.

---

## 2. Top pick #1: "Scam-liability ledger" for telcos (Australia SPF first, then EU PSR and the UK)

### METHOD template

**Problem.**
- From 31 Mar 2027, every Australian telco is legally on the hook for scams that touch its network. It must prevent, detect, disrupt and respond. It must report "actionable scam intelligence" to the ACCC and investigate within 28 days.
- It faces up to A$50M per contravention and a private right of action.
- When a victim complains, **AFCA can split the loss between the bank, the telco and the platform in one case**. The telco will need a per-complaint record proving it took "reasonable steps".
- Telcos today block calls under C661 and SMS rules. They do **not** have a liability or evidence system [I].

**Recent evidence (signals).**
1. Treasury draft Telco, Platform, Banking and Common Codes plus Rules, 28 May 2026 (Ashurst, Corrs, HSF, Baker McKenzie, G+T) [S].
2. A$50M penalties and a private right of action [S].
3. AFCA scam rules and cross-sector apportionment; AFCA-TIO agreement; A$126M scam cap proposal (financemagnates headline) [S].
4. Comms Alliance warns SPF adds A$228M of compliance cost in year 1 and A$88M a year after, "when many telcos are already struggling", and asks for a code safe harbour [S].
5. The A$3,000 auto-reimbursement threshold creates direct loss exposure [S].
6. Apate.ai/TPG shows telcos will buy scam tech from a startup [S].
7. NICE Actimize's 2026 SPF status paper is bank-focused, leaving telcos as the uncovered segment [S/I].

**Who has the pain.**
- Primary: Australian mid-tier telcos and MVNOs (heads of fraud, regulatory and compliance).
- Secondary: SMS aggregators and wholesale voice providers; Tier-1 telcos for the evidence and ASI layer only.
- Tertiary: digital platforms below the giants if designation widens [I].

**What they do today.**
- C661 call-blocking and SMS sender-ID tooling.
- AFCX Intel Loop participation (the larger players).
- Spreadsheets for complaints.
- Law-firm gap analyses; Netcraft-style checklists [S/I].

**Why current products fail.**
- Network vendors (Mobileum, TNS, Hiya, Apate) *block*. They do not produce a code-mapped, per-complaint evidence trail for AFCA, or automate ASI reports.
- Bank fraud hubs (Actimize, Feedzai, BioCatch) are priced and built for banks.
- GRC tools hold policies, not events.

**Why now.**
- Draft codes May 2026; Rules reportedly commenced 1 Sep 2026 [U].
- Full effect 31 Mar 2027, about 6 months away.
- AFCA apportionment guidelines are due. The EU PSR platform-liability deal closed Nov 2025. The UK cross-sector review is live.

**Potential product (Vara assets mapped).**
1. **ASI engine:** ingest CDRs, SMS logs and customer complaints, then rule-based and model scoring (Vara rules engine). **Voice-clone and robocall detection** on reported calls (Vara deepfake detection).
2. **Regulatory filing:** auto-generate ACCC ASI reports and 28-day investigation records (Vara regulatory filing). Code-control mapping for annual self-certification.
3. **Evidence ledger per complaint:** for each AFCA case, show what the telco knew, when, and what it did. Export it as the telco's apportionment defense (Vara evidence ledger).
4. **Step-up for high-risk account actions:** SIM swap, port-out, new eSIM (Vara biometrics SDK plus voice verification; the round-12 wedge).
5. **Cross-sector exchange connector:** push and pull to AFCX/NASC, and to bank partners.

**Time to value.** 2-4 weeks on CDR and complaint exports (no inline network integration for v1).

**Pilot (14-30 days).**
- Back-test 6 months of one MVNO's scam complaints.
- Produce (a) the ASI reports that *would have been due*, (b) evidence files for 20 past complaints scored against draft-code duties, (c) a list of complaints where the telco would carry an apportioned share.

**Willingness to pay.** Unproven. Anchor: A$88M a year in sector compliance spend across all sectors [S]. Telco share [U]. Estimate A$50-250K a year for mid-tier, A$15-40K for small CSPs and aggregators [I].

**Expansion.**
- AU platforms below the giants (if designation extends) [U].
- EU PSR platform liability (platforms vs PSP claims) [S, date U].
- UK if cross-sector liability is enacted [U].
- US FCC voice KYC (pick #2) as the North American wedge.
- Long term: the neutral **cross-sector scam-liability clearinghouse** (bank ↔ telco ↔ platform claims).

**Competition.** No purpose-built SPF telco evidence product found [I, 3 searches]. Feature-adjacent players:
- Apate.ai: telco relationships; could add reporting.
- Mobileum/Subex/TNS: telco fraud management incumbents [M].
- Netcraft: SPF content marketing [S].
- AFCX: could build a compliance layer on top of Intel Loop [I].
- Big-4: code-mapping consulting.

**Moat (10/100/1,000).**
- 10: code-mapped evidence templates and AFCA outcome data.
- 100: cross-telco scam-number and voice-clone fingerprints; becomes a de facto evidence standard AFCA recognises.
- 1,000 (global): claims clearinghouse network between banks, telcos and platforms.

**CTO/CEO test sentence (MVNO head of fraud).** "When AFCA joins us to a bank's scam complaint, I can show in one click what we knew, when we knew it, and that we met every Telco Code duty, and I filed the ACCC report automatically."

**Kill test question.** "Will you pay ≥A$50K a year before 31 Mar 2027 for ASI reporting plus per-complaint evidence, or will you handle it with your existing fraud vendor and a spreadsheet?"

### METHOD scores (1-10)
| Category | Score | Note |
|---|---|---|
| Pain severity | 7 | A$50M penalties, private actions and AFCA apportionment are real. Telcos see SPF as cost, not loss, until complaints arrive |
| Urgency | 8 | Hard date 31 Mar 2027 [S] |
| Market timing | 9 | Codes drafted; final guidelines pending; a 6-month window |
| Speed to pilot | 8 | Back-test on exports |
| Ease of integration | 7 | CDR/complaint exports for v1; inline later |
| Ease of reaching customers | 5 | Australia-only; founders have no AU telco network; small buyer pool |
| Willingness to pay | 6 | Comms Alliance cost complaints show budget pressure, but the spend is mandated |
| Competition | 7 | No purpose-built vendor found; Apate, Mobileum and AFCX are a feature away |
| Moat potential | 6 | Evidence standard plus cross-telco data; AFCX could own the network |
| Market size | 4 | AU telco SAM around A$10M (math below); global only via EU PSR/UK |
| VC attractiveness | 6 | "Scam liability clearinghouse" is a strong story; AU-only start is weak |
| **Average** | **6.6** | |

### Original bar scores (11)
| Category | Score | Note |
|---|---|---|
| Pain | 7 | as above |
| Urgency | 8 | hard date |
| ROI clarity | 6 | Penalty and apportionment avoidance is probabilistic; auto-reimbursement under A$3K is concrete |
| Customer accessibility | 5 | AU, small pool, no network |
| Pilot speed | 8 | exports |
| Market size | 4 | ~A$10M AU; expansion unproven |
| Expansion | 7 | EU PSR, UK, US voice; clearinghouse |
| Venture potential | 6 | Depends on the clearinghouse |
| Defensibility | 6 | Data plus evidence standard |
| Why now | 9 | SPF Mar 2027 plus EU PSR |
| Competition position | 7 | Gap verified in 3 searches only |
| **Average** | **6.6** | Fails 8.5; 5 categories below 7 |

### Buyers × ACV
- AU telcos [U counts]:
  - 4 large (Telstra, Optus, TPG, Vocus) × A$300K = A$1.2M. Likely build in-house or use incumbents, so assume 50% → **A$0.6M**.
  - ~30 mid-tier and MVNO × A$100K = **A$3.0M**.
  - ~200 small CSPs, SMS aggregators and wholesale voice × A$20K = **A$4.0M**.
  - **AU telco SAM ≈ A$7.6M (~US$5M).** Platforms not counted: the designated ones are giants.
- EU PSR: ~25 VLOPs plus ~500 marketplaces and social platforms × €50-200K if a claims-defense product fits → **€25-100M [I, speculative]**.
- UK telcos and platforms, if enacted: ~£10-20M [I].
- **Ceiling without the clearinghouse is about $30-120M ARR.** A venture outcome requires the cross-sector clearinghouse.

### 14-day test
- **Day 1-3:** Get the final or near-final Telco Code text. Map every duty to evidence fields. Ask a contact to request the AFCA apportionment guideline status.
- **Day 2-10:** Run 12 calls with 8 mid-tier telcos/MVNOs (heads of fraud and regulatory), 2 SMS aggregators and 2 platforms below the giants. Ask: (a) who owns SPF; (b) budget line and vendor; (c) how they will answer an AFCA joinder.
- **Day 5-14:** Back-test 1 telco's 6 months of scam complaints.
- **Also:** 1 call with Apate.ai (partner or competitor) and 1 with AFCX (exchange connector).
- **Pass:**
  - ≥3 telcos confirm no vendor is selected for ASI and evidence;
  - ≥2 LOIs at ≥A$50K;
  - the back-test shows ≥30% of complaints lack the evidence a draft-code duty would need.

### Kill signals
- Telcos say "our fraud vendor (Mobileum/TNS/Apate) or Comms Alliance tooling will cover it" (≥50% of calls).
- AFCX or the NASC launches a free ASI reporting and evidence portal.
- The final Telco Code gives a safe harbour for C661 compliance (Comms Alliance asked for one [S]).
- The commencement date slips beyond 2027, or the AU telco count with real budgets is under 15.
- EU PSR platform liability is narrowed in final text or applies after 2029.

---

## 3. Top pick #2: Know-your-customer plus traffic monitoring for US voice originators ("AML for voice")

### METHOD template

**Problem.**
- Every US originating voice provider must "know its customer". The FCC removes non-compliant providers from the Robocall Mitigation Database, which means downstream carriers must refuse their traffic. More than 1,200 providers were removed in Aug 2025 and 14 more on 2 Sep 2026 [S].
- The **Apr 30 2026 FNPRM** would make KYC prescriptive: ID, address and alternate phone before service; extra diligence for high-volume customers; a **$2,500 per-call base forfeiture**; and possibly a **safe harbor for AI/automated KYC** [S].
- Third-party authentication (sign with your own certificate) has applied since 18 Sep 2025 [S]. A provider is now accountable for traffic it signs on behalf of resellers.
- This is a bank-style KYC plus transaction-monitoring problem landing on small VoIP, UCaaS and CPaaS companies.

**Recent evidence.**
1. KYC FNPRM, 30 Apr 2026 (DWT, Telecompetitor, consumerfinancialserviceslawmonitor, FCC-26-27) [S].
2. KYUP/STIR-SHAKEN FNPRM, 20 May 2026 (Wiley) [S].
3. RMD-expansion FNPRM, 23 Jul 2026 [S].
4. RMD order effective 5 Feb 2026 [S].
5. RMD removals: 1,200 (2025), 14 (Sep 2026), and a 35-company cure order (Mar 2026) [S].
6. Didit content marketing for "FCC KYC voice providers 2026" shows vendors smell it [S].

**Who has the pain.** About 2,400+ RMD filers [S, 2024 subset; total U]:
- small VoIP/UCaaS originators;
- wholesale carriers onboarding resellers;
- CPaaS platforms (Twilio, Telnyx, Plivo, Bandwidth, Sinch, Vonage), whose customers include AI voice-agent companies placing outbound calls.

**What they do today.**
- Manual onboarding forms and credit-card checks.
- TransNexus/Neustar analytics (larger players).
- Spreadsheets for traceback responses (ITG) [M/I].

**Why current products fail.**
- Robocall analytics scores *calls*. Generic KYC (Didit, Persona) verifies *people*.
- Nobody joins customer-level KYB, sanctions and Covered-List checks to per-customer traffic behaviour (short-duration bursts, spoofed ANIs, AI-voice outbound) to the traceback/RMD evidence file [I].
- **AI voice agents placing outbound calls** add a new class of high-volume customer [I].

**Why now.** The FNPRM is pending (final rule expected 2027 [U]). Removals continue. A safe harbor for automated KYC is proposed, so a vendor could become the safe-harbor default.

**Potential product (Vara assets).**
1. KYB, sanctions and Covered-List screening at onboarding (Vara screening).
2. A rules engine over CDRs per customer (transaction-monitoring analog).
3. Voice-clone/TTS detection on sampled outbound audio (Vara deepfake detection).
4. Evidence ledger and auto-drafted traceback responses and RMD plan text (Vara regulatory filing).
5. Architecture mapping to document the provider's call flow for the RMD plan (Vara Architecture).

**Time to value.** 1-2 weeks on CDR exports.

**Pilot.**
- Back-test 90 days of CDRs and customer lists at 2 wholesale or UCaaS providers.
- Flag customers matching traceback history.
- Draft the KYC file the FNPRM would require.

**Willingness to pay.** Unproven. Small providers are cost-sensitive. Estimate $12-36K a year small, $100-300K for CPaaS [I].

**Expansion.**
- 10DLC/SMS brand vetting.
- AI-voice-agent outbound certification ("verified agent caller", which links to round 12).
- Canada (CRTC) and UK (Ofcom CLI rules) [M].
- Australia SPF telcos (pick #1).

**Competition.**
- TransNexus and Neustar/TransUnion: call analytics and STIR/SHAKEN [S].
- Didit: KYC marketing [S].
- Numeracle, ZipDX, The Campaign Registry for SMS [M].
- CPaaS in-house trust teams (Twilio Trust Hub [M]).
- **A gap exists, but it is crowded on both flanks.**

**Moat.** A cross-provider bad-customer graph: robocallers hop between providers, like shell IORs in KYI. It is the strongest moat element, but needs providers to share data.

**CTO/CEO test sentence (wholesale carrier CEO).** "Every reseller I sign is vetted, monitored and documented, so a traceback or FCC letter takes 10 minutes, not a removal from the RMD."

**Kill test question.** "Will you pay ≥$15K a year *before* the FCC finalises KYC, and will you share hashed bad-customer data with other providers?"

### METHOD scores
| Category | Score | Note |
|---|---|---|
| Pain severity | 7 | RMD removal is existential; $2,500 per call is proposed |
| Urgency | 5 | KYC rule not final |
| Market timing | 7 | Pre-final window; safe-harbor opportunity |
| Speed to pilot | 8 | CDR exports |
| Ease of integration | 7 | Exports, then API at onboarding |
| Ease of reaching customers | 6 | US; INCOMPAS/SIPNOC channels [M]; many small buyers |
| Willingness to pay | 5 | Thin margins at small providers |
| Competition | 5 | TransNexus, Neustar, Didit, CPaaS in-house |
| Moat potential | 6 | Bad-customer graph |
| Market size | 5 | ~$30M US SAM |
| VC attractiveness | 6 | "AML for voice / AI-agent callers" is legible |
| **Average** | **6.1** | |

### Original bar scores
| Category | Score | Note |
|---|---|---|
| Pain | 7 | |
| Urgency | 5 | proposed rule |
| ROI clarity | 6 | Avoided removal is binary but rare |
| Customer accessibility | 6 | |
| Pilot speed | 8 | |
| Market size | 5 | |
| Expansion | 7 | SMS, AI agents, SPF |
| Venture potential | 6 | |
| Defensibility | 6 | |
| Why now | 7 | FNPRM 2026 |
| Competition position | 5 | |
| **Average** | **6.2** | Fails |

### Buyers × ACV
- ~10 CPaaS/large carriers × $200K = $2M.
- ~300 mid wholesale and UCaaS × $40K = $12M.
- ~2,000 small originators × $8K = $16M.
- **US SAM ≈ $30M.** Plus SMS/10DLC and AI-agent outbound certification, which is maybe 2-3x [I].

### 14-day test
- 10 calls: 4 wholesale carriers, 4 UCaaS, 2 CPaaS trust teams.
- 1 call with a telecom regulatory lawyer on FNPRM timing and the safe harbor.
- Back-test 1 provider's 90-day CDRs.
- **Pass:**
  - ≥3 say they would buy before the final rule;
  - ≥2 LOIs ≥$15K;
  - the back-test flags ≥5 customers the provider agrees are high-risk;
  - ≥3 agree to hashed sharing.

### Kill signals
- The FNPRM stalls past mid-2027, or the safe harbor names STIR/SHAKEN analytics only.
- TransNexus or Neustar ships customer-KYC modules.
- Twilio/Telnyx expose free KYC to resellers.
- Most small providers say "a form plus a credit card is enough".

---

## 4. Verdict
- **No idea clears 8.5.** The intermediary-liability lens produced two Vara-native near-misses (6.6 and 6.2), both below KYI (6.8).
- **The lens is useful as a filter, not a generator.** A new intermediary mandate stays vendor-free only when (a) liability is genuinely new, (b) the liable class is mid-sized and numerous, and (c) the duty is about *evidence and liability allocation* rather than a detection feature incumbents already sell.
- **The SPF evidence ledger meets all three, but the market is Australia-sized.** Its venture case depends on the **cross-sector scam-liability clearinghouse** (bank ↔ telco ↔ platform). AU AFCA apportionment (2027), EU PSR platform liability (~2028 [U]) and a possible UK cross-sector shift all point to it.
- **Recommendation:**
  - Fold pick #1 into the existing round-12 voice wedge as the **telco motion**: caller verification for SIM swap and port-out, plus the SPF evidence ledger, sold to AU mid-tier telcos.
  - Run the 14-day SPF test only if the founders can reach 8+ AU telco fraud heads in two weeks.
  - Park pick #2 until the FCC KYC rule is final.

## Sources (search snippets only; not fetched)
ashurst.com (SPF draft rules; operationalising SPF); corrs.com.au; hsfkramer.com (Stage 1 SPF); bakermckenzie.com (2026/06 draft code); gtlaw.com.au; hwlebsworth.com.au (SPF codes; AFCA rules); mallesons.com (AFCA scam rules; CSP register); commsalliance.com.au (SPF cost submission); insurancebusinessmag.com.au (AFCA-TIO); financemagnates.com (AFCA cap); netcraft.com (SPF checklist); resources.niceactimize.com (2026 SPF status); finder.techleap.nl and aea.gov.au (Apate.ai); ausbanking.org.au and govtechreview.com.au (AFCX Intel Loop); europarl.europa.eu (PSR deal 20251121IPR31540); williamfry.com; wiley.law (TAKE IT DOWN; KYUP FNPRM; RMD FNPRM); ftc.gov (TAKE IT DOWN enforcement); activefence.com / alice.io; aiweekly.co; mofo.com (Texas app store; FinCEN IA delay); macrumors.com; mondaq.com (FTPF no cases); irwinmitchell.com; mitratech.com; dwt.com, telecompetitor.com, dlapiper.com (FCC KYC FNPRM); didit.me; mintz.com (third-party auth 18 Sep 2025); tcpaworld.com, accountsrecovery.net (RMD removals); transnexus.com; europa.eu IP/26/1178, lewissilkin.com (Temu €200M); xictron.com (Art 30); mcdermottlaw.com (INFORM/Temu $2M); aa.com.tr, cyprus.representation.ec.europa.eu (EU customs deal); fmcsa.dot.gov, fleetowner.com (broker rule); freightwaves.com; sidley.com, pinsentmasons.com (AI Act omnibus); privacy.ca.gov, trustarc.com (DROP); vinciworks.com, namescan.io (Tranche 2); esafety.gov.au, mediaweek.com.au (SMMA); bratby.law, regulationtomorrow.com (UK APP); jdsupra.com, ropesgray.com (Colorado SB 189); joinble.io, amlwatcher.com (AMLR); conventuslaw.com, mondaq.com (India TCS Amendment Rules).
