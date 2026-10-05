# Thesis P: "The AI product-security team for every manufacturer selling connected products in Europe" (CRA)

*Red-team analysis, 2026-10-05. 36 web searches; WebFetch was not used. Every URL below came from search results. "(unverified)" marks an estimate, a single weak source, or a number from a data broker or vendor marketing. Builds on `V_vuln_response_deepdive.md`.*

---

## 0. Bottom line

**VERDICT: KILL the thesis as pitched ("OneTrust of product security"). One narrow niche survives, and it is still weak. Score: 5.0/10.**

- **The regulation is real and on schedule.** The Digital Omnibus did *not* postpone the CRA. Reporting has been live since 11 Sept 2026. Full obligations apply 11 Dec 2027. Only the harmonised-standards drafting slipped, by 2 months.
- **Readiness is terrible.** PwC finds only 3% of German industrial firms fully ready. Linux Foundation: 41% of manufacturers expect to be compliant by Dec 2027. ENISA: 35% of SMEs keep an SBOM.
- **The market was occupied before the deadline**, unlike GDPR in 2016-18:
  - Firmware SBOM/vuln platforms: ONEKEY, Finite State, Cybellum (LG), NetRise, Binarly, Eclypsium, Keysight, Black Duck.
  - A newly minted unicorn: **Exein, $270M at $1.7B in Sept 2026**.
  - The GRC layer: Drata shipped CRA support on 29 Sep 2026.
  - Cheap documentation tools at €25 to €149/month, plus 2025-26 seed clones: Cemply (Berlin, 2026, *exactly this product*), CRACI, Test of Things.
  - **Incumbents already ship AI agents.** ONEKEY launched its AI Agent on 1 Sep 2026. Finite State sells AgentOS / "Autonomous Product Security OS" with reachability and auto-resolve.
- **Willingness to pay is checkbox-grade.** The Commission's own estimate is about €47K of *total* compliance cost per manufacturer. About 90% of products are in the "default" category and can self-assess, so no auditor forces tool quality. The category leader in Europe, ONEKEY, had about $4M in revenue in 2023 (unverified).
- **The OneTrust analogy breaks.** GDPR touched every company and created a mandated buyer, the DPO. The CRA touches a narrower population, has no mandated role, and the hard part is engineering (fixing old firmware), not paperwork.
- **The only real gap is AI-generated fixes and backports for manufacturers' old firmware branches.** It is real, but it needs source and build access, it is services-heavy, and frontier models are commoditizing it (prior deep dive: PortGPT 89%, Aikido+Root). The first party to bolt it on is likely to be ONEKEY, Finite State or Exein, not a newco.

---

## 1. Scope: who is affected, how ready they are, what it costs

| Metric | Data | Source |
|---|---|---|
| Manufacturers/products in scope | The Commission impact assessment counts **615,272 manufacturers and products** in scope | https://venvera.com/learn/cyber-resilience-act-compliance-cost (citing the IA); arXiv industrial study https://arxiv.org/pdf/2505.14325 |
| Total compliance cost | **€29B** across those, about **€47K per manufacturer**. Average product development €140K with a 30.5% secure-dev uplift (€42.7K). Self-assessment €18.4K per product; third-party assessment €25K per product. | same |
| Another cost model | One-off about €78.3K, ongoing about €13.5K/yr, of which documentation+SBOM is about €8.4K (unverified calculator) | https://cyberresilienceact.eu/cost-calculator.html |
| Companies affected worldwide | "Over 600,000 companies worldwide," as repeated in press | https://arcticstartup.com/craci-raises-e1-4-million-pre-seed/ |
| Product classes | About **90% of products are "default"** and can use Module A self-assessment. Important Class I needs a notified body unless harmonised standards are applied. Class II and Critical need third-party assessment. | https://eucybersecurity.org/en/product-classification ; https://finitestate.io/blog/conformity-assessments-eu-cra-requirements |
| PwC Germany 2026 (100 industrial firms; 65% machine builders) | **3% fully prepared. Half have not started.** Firms with 500+ employees are far ahead (59% actively implementing); the Mittelstand lags and leans on external providers. | https://www.pwc.de/de/pressemitteilungen/2026/nur-3-prozent-der-deutschen-industrieunternehmen-sind-vollstaendig-auf-eu-cyber-resilience-act-vorbereitet.html |
| ONEKEY IoT/OT report 2026 (200 German industrial firms) | About half have formed CRA teams (28% up to 10 people, 22% larger). 19% have assigned nobody. **More than 60% rely on external help.** 61% have budget or plan to. | https://finchannel.com/onkey-iot-ot-cybersecurity-report-2026-half-of-all-companies-have-formed-cra-teams/134629/tech-2/2026/09/ |
| Linux Foundation / OpenSSF 2026 | 41% of manufacturers expect full compliance by Dec 2027; 39% don't know when they will be. 32% produce SBOMs for all products. 51% passively rely on upstream for fixes. 66% of all respondents are unfamiliar with the CRA (72% in US/Canada). | https://openssf.org/resources/publications/2026-cra-awareness-and-readiness-report/ ; https://www.linuxfoundation.org/blog/the-cra-readiness-reality-what-changed-and-what-didnt-between-2025-and-2026 |
| ENISA SME survey (Jun 2026, 194 orgs) | 35% keep an SBOM; 24% do threat modelling; incident response is the weakest area. Most-requested help: **documentation templates (73%), secure-development templates (71%), compliance assessment tools (68%).** That is a request for cheap templates, not for an AI PSIRT. | https://www.enisa.europa.eu/sites/default/files/2026-06/SME%20CRA%20survey%20report.pdf ; https://www.cyberresilienceact.eu/es/news/enisa-sme-cra-survey-high-awareness-low-readiness.html |
| Trade associations | VDMA has 3,600 member companies; ZVEI more than 1,600. Orgalim's member associations represent about 770K companies. | Wikipedia (VDMA, ZVEI, Orgalim) |

**Read:**
- The pain is broad but shallow per company.
- The €47K-per-manufacturer total figure caps what software can capture across the long tail.
- The real buyers are the roughly top 10 to 20% of manufacturers by size who run their own firmware stacks.

---

## 2. Will enforcement be real? (critical)

| Question | Finding | Source |
|---|---|---|
| Did the Digital Omnibus postpone the CRA? | **No.** The Omnibus (Reg. (EU) 2026/1744, in force 27 Jul 2026) delayed **AI Act** high-risk duties to Dec 2027. CRA dates are unchanged. | https://www.praxikon.com/en/posts/digital-omnibus-high-risk-postponement-december-2027 ; https://www.cyberresilienceact.eu/state-of-play.html |
| What did the Omnibus do to the CRA? | It added a *single entry point* for incident reporting ("report once, share many"). A CRA severe-incident report can also satisfy NIS2. This **lowers** the reporting burden, which weakens the "ENISA 24h/72h" product wedge. | https://thelens.slaughterandmay.com/post/102lxgd/eu-proposes-single-entry-point-for-cyber-incident-reporting-but-is-it-really-re ; https://www.taylorwessing.com/de/global-data-hub/2026/the-digital-omnibus-proposal/gdh---the-digital-omnibus-and-incident-reporting |
| Reporting live? | Yes. ENISA SRP went live on 11 Sep 2026. Docs came out on 10 Sep, a day before, and the CSIRT list on 4 Sep. | https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/09/CSA_research_note_enisa-cra-reporting-platform_20260918-csa-styled.pdf |
| Harmonised standards | About 41 standards under mandate M/606. A July 2026 draft amendment pushed deadlines **2 months**, to 31 Oct / 31 Dec 2026. ETSI is balloting 17 vertical ENs (EN 304 xxx) until mid-Nov 2026. Citation in the OJ historically takes months, which squeezes 2027. | https://www.cyberresilienceact.eu/news/cra-standardisation-deadlines-pushed-back-two-months.html |
| Industry lobbying for delay | Euralarm calls for "stop-the-clock": essential requirements to apply one year after horizontal standards are available. VDW (machine tools) published a position paper asking for a CRA implementation-schedule extension (Aug 2025). **No Commission proposal to delay the CRA was found as of Oct 2026.** | https://www.euralarm.org/resource/euralarm-calls-for-stop-the-clock-mechanism-on-cyber-resilience-act-timeline.html ; https://vdw.de/wp-content/uploads/2025/09/vdw_pospap_cra_extension_implementation_schedule_202508.pdf |
| Notified bodies | Notification provisions applied from 11 Jun 2026. DEKRA says it will be a CRA notified body; TÜV NORD is applying to BSI. TÜV SÜD/Rheinland designation is unconfirmed. Capacity is irrelevant for the roughly 90% that self-assess. | https://www.dekra.com/en/cyberresilienceact/ ; https://cvdportal.com/standards/notified-bodies |
| Market surveillance | In Germany, BSI is the market surveillance authority from 2027. Bitkom and industry flag BSI capacity and governance concerns. | https://www.bitkom.org/sites/main/files/2026-03/bitkom-stellungnahme-cra-umsetzung-cyberresilienz.pdf ; https://www.advisori.de/services/regulatory-compliance-management/cra-cyber-resilience-act/cra-bsi-en |

**Read: the law is real; enforcement will be soft early on.**
- Hard deadlines exist: Dec 2027 for full obligations, and reporting already live.
- Practical enforcement will be **spot checks and documentation audits by under-resourced authorities from 2028**.
- A second "stop-the-clock" push in 2027 is plausible: standards will be late, and the Omnibus precedent exists for the AI Act. This is a **live tail risk** (my estimate: 25 to 35%) that it gets partially deferred.
- Either way, early buyers optimize for *defensible paperwork at lowest cost*, not for engineering excellence.

---

## 3. Competitors (searched hard)

| Company | What it does for CRA | Funding / traction | Threat |
|---|---|---|---|
| **Exein** (IT) | Embedded runtime security, SBOM/vuln, CRA. Building a foundation model on telemetry from 2B devices; M&A program for 2026 | **$270M at $1.7B (Sep 2026, Headline; EIB, KfW, T.Capital)**, on top of €170M in 2025 | **Very high.** Capital to buy any wedge. https://www.orrick.com/en/News/2026/09/Exein-Becomes-Italian-Unicorn-at-17-Billion-Valuation-After-New-Financing-Round-Led-by-Headline ; https://tech.eu/2025/12/18/exein-raises-an-additional-eur100m-to-expand-its-embedded-cybersecurity-platform/ |
| **ONEKEY** (Düsseldorf) | Binary firmware SBOM, vuln management, VEX/SSVC, "CRA Fast Start," compliance; **AI Agent launched 1 Sep 2026**; "VulnOps" narrative | PwC Germany + eCapital. Revenue about $1.1M (2021) → $4.1M (2023) (unverified, prospeo) | **High** in DACH. Same buyer, same pitch, PwC channel. https://www.onekey.com/resource/the-ai-vulnerability-storm-is-here-embedded-manufacturers-need-vulnops ; https://www.remio.ai/post/onekey-launches-evidence-first-ai-agent-for-firmware-security |
| **Finite State** (US) | "Autonomous Product Security OS," AgentOS, reachability and auto-resolve, CRA self-assessment packages, EMEA expansion | About $49.5M total ($20M growth round, Mar 2024); acquired MergeBase | **High.** https://finitestate.io/ ; https://finitestate.io/hubfs/Collateral/Reachability%20%26%20Auto-Resolve%20Datasheet.pdf |
| **Cybellum** (LG) | Product security platform for auto/medical/industrial: SBOM, VEX, compliance, incident response | Acquired by LG (about $240M) | High in auto/industrial. https://www.securityweek.com/lg-acquire-vehicle-cybersecurity-firm-cybellum/amp/ |
| NetRise | Binary/firmware SBOM, CRA page | $24.8M total ($10M A, Apr 2025) | Med. https://www.netrise.io/solutions/eu-cra-compliance |
| Binarly | Binary SBOM/CBOM, patented reachability | About $14M | Med. https://www.binarly.io/ |
| Eclypsium | Firmware/hardware supply chain, SBOM | More than $100M total (+$25M, Mar 2026) | Med (enterprise-side). https://eclypsium.com/blog/eu-cra-cyber-resilience-act-firmware-hardware-security/ |
| Keysight SBOM Manager | Binary/firmware SBOM aimed at the CRA; test-equipment channel into device makers | Public company | Med-High (channel). https://www.helpnetsecurity.com/?p=362369 |
| Black Duck (BDBA) | Binary SCA, CRA marketing | Large incumbent | Med. https://www.nasdaq.com/press-release/black-duck-leads-software-security-push-european-cyber-resilience-act-compliance-2025 |
| **Drata** | CRA framework: controls, evidence, product-security readiness (29 Sep 2026) | Large GRC | **Med-High** on the "OneTrust" layer. https://drata.com/blog/introducing-eu-cyber-resilience-act-support |
| Vanta / OneTrust | No CRA module found (Vanta has NIS2/DORA) | — | Low today; fast follower |
| **Cemply** (Berlin, founded 2026) | **Exactly the thesis:** SBOM, vuln monitoring, ENISA reporting, CE technical file | Funding unknown | Proof the idea is obvious. https://www.startuphub.ai/startups/cemply |
| CRACI (Helsinki) | CI/CD SBOM, vuln, CRA docs | €1.4M pre-seed (Lifeline) | Low-Med. https://arcticstartup.com/craci-raises-e1-4-million-pre-seed/ |
| Test of Things (Helsinki) | IoT compliance automation (62443, RED/EN 18031, CRA) | €1.2M pre-seed (Mar 2026) | Low-Med. https://www.tamradar.com/funding-rounds/test-of-things-pre-seed-1-2m |
| CRA-Ready, CRA Evidence, others | Self-serve CRA documentation at **€25 to €149/month** or $49/month | — | **Price anchor** for the documentation layer. https://www.capterra.com/p/10045966/CRA-Ready/ |
| Sbomify, Interlynk, Anchore | SBOM/VEX management with CRA/FDA checks | Small | Low-Med. https://sbomify.com/compliance/eu-cra/ ; https://www.interlynk.io/solutions/cyber-resilience-act |
| TIC firms: DEKRA (bought Onward Security), Bureau Veritas Cybersecurity (Secura), TÜV NORD/SÜD/Rheinland/TÜViT, SGS | Gap assessment, testing, notified body, consulting | Large | Channel *or* competitor for services. https://www.dekra.com/en/cyberresilienceact/ ; https://www.tuvit.de/en/topics/regulations/cyber-resilience-act/ |
| Consultancies: PwC, advisori, pi3g, itemis, engineering firms | CRA programs; the PwC-ONEKEY link | — | They own the Mittelstand relationship. https://www.pwc.de/de/cyber-security/product-cyber-security/pwc-product-security-survey-2026.html |
| Embedded LTS maintainers: Canonical, Wind River, Timesys/Lynx, CIP SLTS, Linutronix, Pengutronix (not searched this pass) | Long-term patched Linux/BSPs | — | High for the "backport" survivor angle (unverified) |
| In-house (Siemens ProductCERT, 100+ experts; Bosch; Schneider) | Big OEMs build their own | — | Removes the top of the market. https://cert-portal.siemens.com/ |

**Read:** this is the most crowded field of any thesis in this round. **The claimed AI differentiation was publicly shipped by the two closest incumbents in Sept 2026.**

---

## 4. Buyer

- **Who buys:**
  - At €100M+ manufacturers: Head of Product Security or Product CERT, often newly created for the CRA, reporting to the CTO or Head of R&D.
  - At €20M to €100M machine builders: Head of R&D/Engineering, or the Quality/Regulatory (CE-marking) manager who already owns the Machinery Directive and RED technical files.
  - The **CE/quality owner is a checkbox buyer** who compares against TÜV/consultant quotes and €149/month tools.
- **How many targets** (unverified estimate):
  - About 3,600 VDMA plus 1,600 ZVEI members, much of the German core.
  - EU-wide, manufacturers with at least €20M revenue that ship their own firmware or software: roughly **6,000 to 12,000**.
  - Plus non-EU exporters (US/Taiwan/China/Japan/Korea): another 5,000 or more, but 72% of US/Canada respondents haven't heard of the CRA.
  - Realistic ICP for an AI product-security platform (own firmware, multiple product lines, ongoing releases): **about 4,000 to 8,000**.
- **ACV** (unverified):
  - Mid-market: €25K to €80K.
  - Large (multi-product): €100K to €300K.
  - Anchors on the low side: the Commission's €47K *total* per manufacturer, €8.4K/yr documentation+SBOM in the cost calculator, and ONEKEY's small revenue base.
- **Sales cycle:**
  - Mittelstand: 6 to 12 months. Committees, German language, on-prem demands. Uploading firmware to a startup's cloud is a trust hurdle, and ONEKEY offers on-prem.
  - PwC: smaller firms rely on external providers.
  - ONEKEY: more than 60% use outside help.
- **Channel:**
  - TIC bodies and consultancies own the relationship.
  - A startup would have to be the tool *inside* a TÜV/DEKRA/PwC engagement, but PwC already owns part of ONEKEY.

---

## 5. Does AI really change it?

| Capability | Status quo | Does AI create a new winner? |
|---|---|---|
| SBOM from firmware/binaries | Mature (ONEKEY, Finite State, NetRise, Binarly, Keysight, BDBA) | No. Deterministic unpacking plus signatures; incumbents have years of corpus. |
| Reachability/triage on binaries | Incumbents ship it: Binarly (patented), Finite State (reachability and auto-resolve). LLM-assisted taint research is improving fast (LuaTaint, LATTE, LIVA). | Incremental. Incumbents add LLMs on top of their own extraction (ONEKEY's "evidence-first" AI Agent). |
| VEX/advisory/ENISA report drafting | LLM-trivial; Drata and cheap tools cover it; the single entry point simplifies it | No. Commodity. |
| Technical file / conformity docs | Templates, consultants, €25 to €149/month tools | No. Commodity. |
| **Auto-generated fixes/backports for old firmware branches (vendor kernels/BSPs, RTOS, own code)** | Mostly manual, or bought from LTS vendors. Yocto reviewers are already flooded with AI patches. Academic backporting: FixMorph 75%, PortGPT 89%. | **Yes, the only real delta.** But it needs source, toolchain and build/CI access per product line, plus hardware-in-the-loop regression for safety-relevant machines. It looks like services. |

https://www.helpnetsecurity.com/?p=310701 ; https://arxiv.org/html/2310.08275v1 ; https://www.techveda.live/2026/06/28/kernel-embedded-digest-steady-embedded-gains-strained-review/ ; https://www.comp.nus.edu.sg/%7Eabhik/pdf/ISSTA21.pdf

---

## 6. Market math

Assumptions (unverified): ICP of about 6,000 (EU plus exporters); blended ACV €60K mid-market and €250K large.

| ARR | Mix | ICP share | Comment |
|---|---|---|---|
| $10M | about 170 × €55K | ~3% | Plausible by 2029, if you can out-sell ONEKEY and Finite State in DACH |
| $50M | 550 × €60K + 60 × €250K | ~10% | Requires category leadership against a $1.7B Exein, LG-Cybellum and Keysight |
| $100M | 1,000 × €65K + 130 × €250K | ~19% | Implausible on CRA alone. Needs global expansion **and** the backport/maintenance service line. |

**Expansion: weak.**
- UK PSTI, Japan JC-STAR STAR-1, and (cross-recognized) US Cyber Trust Mark: the latter is voluntary, lost UL as administrator, and moved to ioXt in Apr 2026. These are light baseline labels, not CRA-depth. https://broadbandbreakfast.com/fcc-picks-ioxt-alliance-to-head-cyber-trust-mark-program/ ; https://www.meti.go.jp/english/press/2025/1106_002.html
- FDA 524B (medical) is excluded by the brief, and Medcrypt/Cybellum already own it.
- NIS2 supply-chain clauses create customer pull for SBOMs, but that pull runs through the same incumbents.

**"Global product-security system of record"** is the stated strategy of Finite State ("Product Security OS"), Cybellum and Exein. A newco enters fourth or fifth.

---

## 7. Kill signals

| Signal | Status |
|---|---|
| Omnibus delay | **Not firing** for the CRA. A **Watch** risk remains: a stop-the-clock push in 2027 when standards are late. |
| Incumbent saturation | **Firing.** At least 10 funded binary/SBOM players; Exein unicorn; ONEKEY and Finite State AI agents (Sept 2026); Drata CRA (Sept 2026); Cemply/CRACI/Test of Things clones |
| Low willingness to pay / checkbox | **Firing.** 90% self-assessment. €47K total-cost estimate. €25 to €149/month tools. SMEs ask for *templates*. ONEKEY revenue about $4M (unverified). |
| Services-heavy | **Firing.** More than 60% want external help; the backport wedge needs per-customer build integration. |
| Europe-only | **Partially firing.** US awareness is low; other regimes are lighter labels. |
| Burden reduction | **Firing (mild).** The Omnibus single entry point simplifies reporting. |

---

## 8. Sharpened thesis (best surviving version)

**"CRA support-period maintenance on autopilot: AI-generated, CI-verified security backports for manufacturers' frozen firmware branches (vendor BSP kernels, Yocto layers, own code), shipped as signed update candidates with VEX."**

- **Buyer:** Head of R&D at €50M to €1B device and machine makers with 5 to 50 firmware lines and a 5- to 10-year support obligation.
- **Pricing:** priced per maintained branch (€15K to €40K per branch per year), sold *through* or *alongside* ONEKEY/Finite State/TÜV, not against them.
- **Proof point:** "% of applicable CVEs closed per branch with green build and HIL smoke test, within 14 days" (the CRA final-report clock).
- **Still weak:**
  - It competes with Canonical, Wind River and Timesys-style LTS offerings.
  - It needs deep access.
  - Exein or ONEKEY could add it once models improve.
- **Best exits:** acquisition by Exein, ONEKEY or a TIC firm, not a standalone $1B company.

---

## 9. CTO cold message plus simulated reaction

> **Subject:** CRA: 5 years of security updates for every firmware line you shipped
>
> Hi Dr. Weber, from 11 Dec 2027 every machine you sell needs security updates for its support period, and since September you have 24h to report exploited vulns. We connect to your Yocto/BSP repos, map which CVEs actually reach code in each firmware branch, and deliver AI-generated, build-tested backports plus the VEX/ENISA paperwork, so your 3 embedded engineers don't spend 2027 backporting. 30-min call to run it on one old controller branch?

**Simulated reaction (CTO, €300M Swabian machine builder):** "We started with ONEKEY via PwC last year for SBOM and monitoring, and our quality team has the technical file with TÜV. Backports are interesting, but I'm not giving source code to a startup. Our HMI runs on a supplier's BSP, so the supplier must patch it. Send me something we can run on-prem and I'll pass it to the head of embedded. Maybe Q2." → **soft MAYBE, 9-plus-month cycle.**

---

## 10. Five simulated buyers

| Buyer | Response | Why |
|---|---|---|
| Head of Product Security, €2B industrial automation OEM | **NO** | Has ProductCERT and a Finite State/Cybellum contract; builds AI triage in-house on frontier models |
| CTO, €300M machine builder (DACH) | **MAYBE** | Backport pain is real; trust/on-prem and incumbent (ONEKEY/PwC) block it; slow |
| Quality/CE manager, €40M sensor maker | **NO** | Wants templates and a TÜV stamp; will buy a €149/month tool or the consultant package |
| VP Eng, €150M router/gateway maker (Class I, multi-branch Linux) | **YES (pilot)** | Many old kernel branches, actively exploited vulns, notified-body exposure; would pay €100K+ for verified backports |
| Head of R&D, Taiwanese ODM exporting to the EU | **MAYBE** | Customers (EU brands) push CRA down; price-sensitive; wants per-device pricing |

**Tally: 1 YES, 2 MAYBE, 2 NO.**

---

## 11. Scores (1 to 10)

| Dimension | Score | Note |
|---|---|---|
| Pain | 6 | Real, but mostly paperwork pain; the engineering pain is concentrated in multi-branch vendors |
| Urgency | 7 | Hard dates; reporting live; soft enforcement until 2028; stop-the-clock risk |
| ROI clarity | 4 | Fine avoidance and market access are abstract; checkbox buyers anchor on €47K total |
| Customer accessibility | 4 | Mittelstand is slow, consultant/TIC-mediated, wary of source access |
| Pilot speed | 5 | Firmware SBOM pilot is fast (commodity); backport pilot needs build access |
| Market size | 6 | Large count, low ACV; realistic $50M ceiling on CRA alone |
| Expansion | 4 | Other regimes are light labels; "system of record" already claimed by others |
| Venture potential | 4 | Path to $100M unclear; exit by acquisition more likely |
| Defensibility | 3 | Binary corpus belongs to incumbents; AI layer is shipped by all; docs are commodity |
| Why now | 8 | Best "why now" of the round: CRA dates plus the AI vuln flood |
| Competition position | 2 | Newco would be 5th to 10th entrant, behind a $1.7B unicorn and AI-agent-shipping incumbents |
| **Average** | **4.8** | |

---

## 12. Verdict

**KILL.** "OneTrust of product security / AI PSIRT for CRA" is already being built by:
- funded incumbents (Exein $1.7B, Finite State, LG-Cybellum, ONEKEY with PwC);
- GRC platforms (Drata);
- 2026 seed clones (Cemply, CRACI).

The core AI claims (triage, VEX, ENISA reporting, documentation) shipped in Sept 2026 or are commodity at €25 to €149/month. The only uncovered slice is AI backports for frozen firmware branches. Pursue it only as a narrow, partner-led, possibly acquisition-targeted business, and only if 10 interviews with multi-branch Class I/II device makers confirm at least €100K/yr budget *and* willingness to grant build access.

---

### Unverified or open items

- No official count of "€20M+ manufacturers in scope" was found. The ICP figures are my estimates.
- ONEKEY revenue comes from a data broker (prospeo).
- Pricing of ONEKEY, Finite State and Cybellum was not found.
- The status of RunSafe, Sternum, Medcrypt, JFrog/Vdoo and Shift Left was not verified this pass.
- No VDMA/ZVEI/Bitkom 2026 readiness numbers were found beyond PwC and ONEKEY's German surveys. Bitkom's March 2026 statement on the German CRA implementation law exists but was not read.
