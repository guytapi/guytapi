# Round 2 — Physical AI & Robots at Scale: Second-Order Problems

Analyst stance: skeptical. Date: 2026-10-05. 35 web searches, no page fetches (search snippets only).
Legend: **[V]** = shown in a cited search result; **[U]** = unverified / my estimate / from memory; **[VM]** = cited but source is vendor marketing or low-quality, so treat with caution.

---

## 0. Bottom line first (timing check)

- **The "500 robots from 6 vendors" customer is rare in 2026.** Mobile robots are at roughly 53,000 sites [V], and shipments are growing 20–30%/yr toward a 4.2M-unit installed base by 2030 [V]. But Interact Analysis *cut* its forecast by 12% on tariff uncertainty [V]. Most sites run 1–2 vendors [U]. The real multi-vendor sites today are Amazon-scale (1M+ robots across 300+ facilities, all in-house [V]) and top 3PLs/retailers.
- **Humanoids don't matter commercially yet.** One audit says the only verified Western production humanoid deployments in 2026 are 2 Figure robots at BMW Spartanburg and Agility Digit at GXO [V]. About 13.3K humanoids were produced globally in 2025, mostly by Chinese makers [V]. Selling third-party "humanoid fleet ops" before 2028 is too early.
- **The money and urgency sit with the companies building robots, not the end users.** Physical Intelligence is reportedly raising at about $11B [V], Skild AI raised $1.4B at more than $14B [V], and Q1 2026 was a record for robotics funding [V]. Hundreds of funded robot companies now need deployment, evaluation, teleop and data tooling. End-user buyers (warehouse operators) will matter more from 2027–2028 onward.
- **The same pattern that killed Round 1 is here too.** Orchestration and ops layers get absorbed by robot OEM platforms (LocusONE, MujinOS), WES/WMS suites (Manhattan, Körber) and NVIDIA's free blueprints. Good theses need either a **neutral** position that OEMs structurally can't hold, or a **new workflow** created by learned (VLA) policies.

---

## 1. Problem inventory (18 problems)

### P1. Multi-vendor mobile-robot fleet interoperability and orchestration
- **Who:** Automation/engineering leads at DCs and factories running 2+ AMR/AGV brands. Sites with mobile robots: about 53K [V]. Sites with multiple vendors: maybe 10–20% [U].
- **Evidence:** VDA 5050 v3.0 has been released, and MiR shipped a VDA 5050 adapter for "heritage" mixed fleets ([MiR](https://mobile-industrial-robots.com/blog/mir-supports-interoperability-with-vda5050), [AWO](https://www.automatedwarehouseonline.com/?p=8572)). ABI says AMR vendor response to the MassRobotics standard is "lukewarm" and that it covers only basic information sharing, not task allocation ([ABI](https://abiresearch.com/market-research/insight/7779407-massrobotics-push-for-interoperability-pre)). Managers watch "multiple separate dashboards running in parallel" ([Nasdaq PR](https://www.nasdaq.com/press-release/coordinated-robot-fleets-are-fast-becoming-next-frontier-autonomous-operations-2026)).
- **$ pain:** Traffic deadlocks and idle robots. A failed AMR reduces throughput on adjacent robots by 12–18% [VM, [Oxmaint](https://oxmaint.com/industries/manufacturing-plant/warehouse-automation-case-study-amr-fleet-uptime-predictive-maintenance)].
- **Existing players:** SVT Robotics ($25M Series A led by Tiger Global, Prologis Ventures; [Robot Report](https://www.therobotreport.com/svt-robotics-raises-25m-in-series-a-funding/)), InOrbit ($10M Series A, Sept 2025; [Robot Report](https://www.therobotreport.com/globant-invests-inorbit-series-a-funding-advance-robot-orchestration/)), Meili Robots (about $293K; [vcbacked](https://www.vcbacked.co/company/meili-robots)), Botsync SyncOS ([A3](https://www.automate.org/robotics/news/botsync-secures-sginnovate-funding-to-scale-amr-platform/boa)), Formant ($21M Series A in 2023; [Robot Report](https://www.therobotreport.com/formant-brings-in-21m-to-expand-enterprise-focus/)), and WES vendors ([SC247](https://www.supplychain247.com/article/warehouse_execution_systems_wes_stretches_to_encompass_labor)).
- **Why unsolved:** OEMs won't cede control of traffic. The standards are slowly turning this into a commodity. The company that wins likely becomes the WES, not a startup.
- **Verdict: WEAK–MEDIUM.** The pain is real, but the space is crowded with sub-scale players and a standard is commoditizing it. This is the Round-1 absorption trap again.

### P2. Exception handling and remote teleoperation labor
- **Who:** Robot OEMs and RaaS providers (several hundred [U]), plus end users who staff "robot babysitters."
- **Evidence:** YC's InLoop Robotics (2026) ships imperfect policies, detects failures in real time and hands off to remote humans, turning each intervention into training data ([yespress](https://yespress.io/inloop-robotics-yc-p26.md)). Avatar Robotics raised a $6.5M seed in Aug 2026 for teleoperated warehouse robots ([Dealroom](https://dealroom.co/news/143314-avatar-robotics-raises-6-5m-seed-round-for-teleoperated-warehouse-robots/)). Third Wave's "Shared Autonomy" has remote humans oversee forklifts ([Homebrew](https://www.homebrew.co/blog-posts/third-wave-automation-raises-usd40-million-series-b-to-modernize-the-forklift)). Most humanoids run at about 1:1 operator ratios, and "until robots per operator climbs well above 1:1, human-in-the-loop robotics is a labor arbitrage business" ([ai2.work](https://ai2.work/blog/avatar-robotics-bets-6-5m-on-humanoids-that-fire-their-operators), [Verbine RFS](https://verbine.substack.com/p/request-for-startups-teleoperation)).
- **$ pain:** At 1:1, a $25–40/hr operator per robot erases the ROI [U]. Moving to 1:10 is the gap between a services business and a software business.
- **Existing players:** Formant (acquired Formation, a teleop company; [Robot Report](https://www.therobotreport.com/formant-buys-formation-teleoperation-robotics-fleet-management/)), Freedom Robotics ($6.6M seed in 2019, current status unclear [U]), Avea (YC S26), InLoop (YC), and in-house stacks at every OEM.
- **Why unsolved:** Every OEM builds its own teleop. Latency and safety need deep access to the robot stack. The ops layer (operator routing, SLAs, multi-robot attention allocation) is mostly ad hoc.
- **Verdict: MEDIUM–STRONG.** The pain exists today and gets worse as learned policies ship before they're reliable. The risk is OEM in-sourcing.

### P3. Real-world data for robot foundation models
- **Who:** About 30–100 serious model builders: PI, Skild, NVIDIA GR00T, Figure, Tesla, and OEMs fine-tuning models [U].
- **Evidence:** Human Archive raised $8.2M and has 1,000+ camera headsets on workers in India ([Pulse2](https://pulse2.com/human-archive-8-2-million-raised-to-build-training-data-infrastructure-for-physical-ai/)). Mecka AI raised $60M ([AI Business](https://aibusiness.com/robotics/vendor-training-robots-human-data-raises-60-million)), Ropedia $30M ([IT Brief](https://itbrief.news/story/ropedia-raises-usd-30-million-to-expand-physical-ai-data)) and Axis Robotics $12M ([Seedtable](https://seedtable.com/companies/axis-robotics/funding-rounds/axis-robotics-seed-2026-07)). Encord raised a $60M Series C and reports 10x growth in physical-AI revenue, with data on its platform growing from 1 PB to 5 PB ([SiliconANGLE](https://siliconangle.com/2026/02/26/physical-ai-data-infrastructure-startup-encord-lands-60m-accelerate-intelligent-robot-drone-development/)).
- **$ pain:** Labs with $1B+ in funding spend a large share on data [U].
- **Why unsolved:** It isn't unsolved. It is being flooded with capital. Collection is labor and ops heavy (Scale-style margins), and the buyers are concentrated.
- **Verdict: MEDIUM (crowded).** It doesn't suit pure software founders unless they take a narrow angle such as deployment-fleet data (see P4).

### P4. Turning deployed-fleet data into training data (intervention → dataset loop)
- **Who:** Robot OEMs deploying learned policies, and end users whose sites generate valuable edge-case data.
- **Evidence:** InLoop explicitly sells "every intervention becomes training data" (link above). Foxglove raised a $40M Series B (Bessemer) for multimodal data/observability, with customers including NVIDIA, Amazon and Dexterity ([BusinessWire](https://www.businesswire.com/news/home/20251112126106/en/Foxglove-Raises-%2440-Million-Series-B-to-Power-the-Future-of-Physical-AI)).
- **Why unsolved:** The tooling stops at logging and visualization (Foxglove, Rerun [U]). Data rights between OEMs and end users are unclear [U].
- **Verdict: MEDIUM.** It is a strong feature but will likely be absorbed by Foxglove or Encord.

### P5. Evaluating and validating learned (VLA) robot policies before and after rollout
- **Who:** Any robot company shipping learned policies. About 300–600 funded companies [U], rising as OEMs adopt third-party models from PI and Skild.
- **Evidence:** Real-world VLA evaluation "has relied on binary success rates with very small sample sizes (N ≤ 25 rollouts), often without confidence intervals" ([PhAIL arXiv](https://arxiv.org/pdf/2605.29710)). On SO-101, "execution instability emerged as the dominant failure source" ([arXiv](https://arxiv.org/pdf/2606.08881)). YC S26 includes Robocurve (real-world evaluation) and Instance (automated policy evals) ([timewell](https://timewell.jp/en/columns/yc-summer-2026-batch-analysis)).
- **$ pain:** One bad model update across a fleet means site-wide throughput loss and customer churn. An analogy is the early days of autonomous-vehicle safety validation [U].
- **Why unsolved:** The category is brand new. Simulation fidelity for contact-rich tasks is poor, and there is no "CI/CD for robot behavior" standard.
- **Verdict: STRONG on "riding where the world is going."** Timing risk: the buyer pool is still small, and YC already has 2+ entrants.

### P6. Integration and system-integrator bottleneck (deployment engineering)
- **Who:** SIs (thousands of mostly small firms [U]), robot OEMs that depend on them, and in-house automation teams at manufacturers.
- **Evidence:** A 2025 survey of 120 SME manufacturers found that 73% underestimated integration costs by more than 40%, and that the robot is only 25–40% of project cost ([grabarobot](https://grabarobot.com/blog/robot-integration-cost-guide-2026/) [VM]). ABI reports Universal Robots struggling to find SIs to support growth ([ABI](https://hs.abiresearch.com/market-research/insight/7785091-universal-robots-struggles-to-find-system)). Interact Analysis lists cost and integration difficulty as the main adoption barriers ([AWO](https://www.automatedwarehouseonline.com/interact-analysis-asks-what-customers-want-from-mobile-robots-in-global-survey/)). SVT pitches "days or weeks instead of months or years" ([Robotics247](https://www.robotics247.com/article/svt_robotics_raises_25m_in_series_a_funding_for_software_to_ease_robot_deployments)).
- **$ pain:** For each $30–50K robot, buyers pay roughly $75–150K+ in surrounding project cost (implied by the 25–40% figure).
- **Existing players:** Intrinsic Flowstate (folded into Google in March 2026; Foxconn JV; [SiliconANGLE](https://siliconangle.com/2025/11/20/alphabets-intrinsic-foxconn-plan-accelerate-factory-automation-smarter-robots)), Mujin ($233M Series D, building a certified-integrator network; [BusinessWire](https://www.businesswire.com/news/home/20251202560677/en/Mujin-Raises-US%24-233-Million-to-Accelerate-Global-Growth-and-Drive-the-Future-of-Intelligent-Automation)), Vention and Standard Bots [U], and SVT.
- **Why unsolved:** Every cell is bespoke (grippers, PLCs, safety, the customer's WMS/MES). SIs are services firms with thin software budgets.
- **Verdict: STRONG pain, but buyer and ACV are hard.** LLM agents that write PLC and robot code, specs and risk assessments make this newly tractable.

### P7. Safety risk assessment and certification for each new deployment or layout change
- **Who:** SIs and end-user EHS/engineering teams. Required on every AMR deployment under ANSI/A3 R15.08-2 (risk assessment per ISO 12100 / B11.0) ([AWO](https://www.automatedwarehouseonline.com/2023/10/26/new-amr-safety-standard-available-with-release-of-ansi-a3-r15-08-2/)). ISO 10218-1/2:2025 makes functional-safety requirements explicit ([Control Design](https://www.controldesign.com/industry-news/news/55268769/iso-10218-update-makes-functional-safety-requirements-more-explicit)).
- **$ pain:** Weeks of consultant time per site and per change [U]. Re-assessment is needed whenever the layout, fleet or software changes, and changes become more frequent as learned policies update.
- **Existing players:** Consultants and TÜV-type firms. Little software [U].
- **Verdict: MEDIUM.** It is a niche on its own and a good wedge into P6. It is near "regulated," but workplace safety compliance is not a banking/healthcare-style regulator problem.

### P8. Robot uptime and multi-vendor maintenance
- **Evidence:** One estimate puts the cost of one goods-to-person AGV being down at $2,400/day, and $200–500/hr per robot at a 30-AMR site [VM, [Oxmaint](https://oxmaint.com/industries/manufacturing-plant/warehouse-automation-case-study-amr-fleet-uptime-predictive-maintenance)]. Over 118K robotics technician jobs are open [VM, [robotomated](https://robotomated.com/learn/market/robotics-jobs-market-2026)], against about 15K BLS-counted robot technicians in 2024 [VM, same source].
- **Existing players:** OEM service contracts (RaaS bundles maintenance; e.g., Brightpick charges $1,900–2,200/robot/month all-in ([Brightpick](https://brightpick.ai/resources/how-brightpicks-raas-works/))), CMMS vendors and Oxmaint.
- **Why unsolved:** OEMs bundle maintenance under RaaS. Third parties lack access to diagnostic data.
- **Verdict: WEAK–MEDIUM.** RaaS pushes the problem back onto OEMs.

### P9. Automation ROI underperformance and lack of vendor accountability
- **Who:** COO, VP Automation and CFO at 3PLs, retailers, CPG and automotive companies.
- **Evidence:** "Up to 50% of warehouse automation projects fail to achieve their originally defined goals," and 20–40% deliver significantly lower ROI than the business case ([xpert.digital](https://xpert.digital/en/fail-faster-through-automation/) [VM]). Also [Conveyco](https://www.conveyco.com/news/when-warehouse-automation-fails-how-to-avoid/) [VM].
- **$ pain:** Projects worth tens of millions underdeliver. Usage-based RaaS (Magazino charges 6¢/pick, [AWO](https://www.automatedwarehouseonline.com/?p=5820)) creates invoices that someone needs to verify.
- **Existing players:** OEM dashboards (each OEM grades itself), WES analytics and consultants.
- **Why unsolved:** No neutral layer normalizes KPIs across vendors, and OEMs have a conflict of interest.
- **Verdict: MEDIUM–STRONG** (see Thesis C). The key question is data access.

### P10. Pre-deployment simulation and site digital twins for planning and sales
- **Evidence:** NVIDIA's Mega Omniverse blueprint, with KION and Accenture as first adopters ([NVIDIA](https://blogs.nvidia.com/blog/mega-omniverse-blueprint)). MetAI/Kenmec ([AWO](https://www.automatedwarehouseonline.com/metai-and-kenmec-use-nvidia-omniverse-to-create-logistics-simulation-environment/)). Mujin is building a real-time digital twin (Series D release). Antioch raised an $8.5M seed ([TAMradar](https://www.tamradar.com/funding-rounds/antioch-seed-8-5m-robotics-sim)), and Parallax Worlds raised $4.9M ([A3](https://www.automate.org/news/parallax-worlds-raises-4-9m-to-stress-test-robots-before-they-hit-the-factory-floor/boa)).
- **Why unsolved:** Building a twin is still expensive. NVIDIA gives away the platform, and integrators (Accenture) capture the services revenue.
- **Verdict: MEDIUM–WEAK.** NVIDIA and the OEMs crowd this space.

### P11. Fleet software delivery (OTA updates and versioning) for robot companies
- **Evidence:** YC S26's Agency Tool Company ships delta OTA updates to robot fleets ([timewell](https://timewell.jp/en/columns/yc-summer-2026-batch-analysis)).
- **Verdict: WEAK–MEDIUM.** It's a devtool with a small buyer pool and competes with Foxglove, Formant and AWS IoT.

### P12. Robot cybersecurity (OT security for robots and humanoids)
- **Evidence:** Unitree Go1 backdoor CVE-2025-2894 ([Axios](https://www.axios.com/2025/04/01/threat-spotlight-backdoor-in-chinese-robots-future-of-cybersecurity)). A wormable BLE root exploit affects Go2, B2, G1 and H1 ([IEEE Spectrum](https://spectrum.ieee.org/unitree-robot-exploit)). Chinese makers shipped most humanoids in 2025 [V].
- **Existing players:** OT security incumbents (Claroty, Nozomi, Dragos) [U] could extend into robots. Alias Robotics [U].
- **Verdict: MEDIUM, and early.** The CISO buyer is real, but robot-specific spend is small until fleets grow. The OT incumbents will add robot coverage as a feature.

### P13. RaaS / usage-based billing and metering
- **Evidence:** Magazino charges 6¢/pick and Brightpick $1,900–2,200/robot/month (links above).
- **Verdict: WEAK.** Billing tools (Zuora, Stripe) cover most of it. The only defensible part is metering verification, which folds into P9.

### P14. Humanoid fleet operations
- **Evidence:** Only about 2 Figure units at BMW and Digit at GXO count as verified production deployments ([nextwavesinsight](https://nextwavesinsight.com/humanoid-robotics-deployment-2026/)). Digit has moved 100K+ totes ([ai2.work](https://ai2.work/blog/digit-crosses-100-000-totes-humanoids-exit-the-demo-phase)).
- **Verdict: WEAK (too early).** Fleets are in single or double digits per site, and OEMs fully control the stack.

### P15. Autonomous forklift and dock operations in mixed human-robot traffic
- **Evidence:** Docks bring trailer and pallet variability, mixed workflows and peak congestion ([robotics.press](https://www.robotics.press/news/fox-robotics-symbotic-acquisition-profile/)). Symbotic acquired Fox Robotics (March 2026, per the same source). Third Wave raised a $40M Series B.
- **Verdict: WEAK for software startups.** OEMs own it, and consolidation is underway.

### P16. Autonomous yard trucks and yard orchestration
- **Evidence:** Outrider and YMX signed a 5-year channel partnership in Oct 2026 ([Supply Chain Dive](https://www.supplychaindive.com/press-release/20260930-ymx-logistics-and-outrider-establish-strategic-partnership-to-accelerate-au-1/)).
- **Verdict: WEAK (too early, and YMS incumbents exist).**

### P17. Drone-in-a-box inspection data pipelines
- **Evidence:** DIB systems are a mature category ([DroneU](https://www.thedroneu.com/blog/drone-in-the-box-systems/)). Skydio Dock leans federal and defense.
- **Verdict: WEAK.** The category is mature and skews toward regulated buyers (utilities, government) that we exclude.

### P18. Human–robot labor orchestration (task split between people and robots)
- **Evidence:** WES is "stretching to encompass labor" ([SC247](https://www.supplychain247.com/article/warehouse_execution_systems_wes_stretches_to_encompass_labor)). The WES market is about $4B by 2030 [V/U].
- **Verdict: WEAK.** WES and labor-management incumbents (Manhattan, Körber) own it.

---

## 2. Three best startup theses

### Thesis A — "Production QA for robot brains"
**One sentence:** *Continuous evaluation, regression testing and live monitoring for learned robot policies, so a robot company knows before rollout that a new model checkpoint won't drop pick success at customer site X, and can prove reliability to its customers.*

- **Who buys:** Head of Autonomy/ML or VP Deployment at robot companies shipping learned policies (Dexterity, Ambi, Agility, Figure, Locus Array, Third Wave and others). Later, OEMs that license PI or Skild models they didn't train, and enterprise end users who need acceptance testing.
- **Market math:** Today about 300–600 funded robot companies × $100–250K ACV = **$30–150M** [U]. At scale, pricing is per deployed robot. If 10% of a 4.2M-unit 2030 installed base [V] runs learned policies (420K robots) at $50–100/robot/month, that is **$250–500M ARR**. Adding enterprise acceptance testing gets to a plausible $1B+ path, but only if learned policies win in production.
- **Why now:** Foundation models (PI at ~$11B, Skild at $14B+) are moving from labs to fleets in 2026–2027. Today's evaluation is N≤25 with no confidence intervals (PhAIL). OEMs adopting third-party models need independent validation.
- **Why incumbents/OEMs can't:** Model labs grading their own homework is a conflict, much like the case for an independent tester. Foxglove is a logging and visualization tool, not a statistical evaluation and gating tool (yet). OEMs build one-off internal scripts.
- **90-day pilot:** Attach to one robot company's logs (MCAP/ROS bags) and intervention data. Build a held-out "site regression suite" from real failures. Replay or shadow-evaluate the next 2 model releases and predict the field success-rate delta with confidence intervals. Success means the prediction is within ±2 points of the measured field result.
- **Strongest kill risk:** Foxglove ($40M Series B, Bessemer) or Encord adds evaluation, or each foundation-model lab bundles it free. YC already has Robocurve and Instance. Also, contact-rich tasks may stay non-simulatable, which would reduce the product to a dashboard.

### Thesis B — "The AI systems integrator"
**One sentence:** *An agent that turns a robot cell or AMR deployment requirement into a validated layout, robot/PLC code, a safety risk assessment (R15.08 / ISO 10218:2025) and a commissioning plan, cutting deployment engineering time by half or more.*

- **Who buys:** (1) Robot OEMs blocked by SI capacity (UR struggles to find SIs per ABI) to arm their channel. (2) The top ~500 SIs [U]. (3) In-house automation engineering teams at ~1,000–2,000 large manufacturers and 3PLs [U].
- **Market math:** Seats/platform: 2,500 orgs × $60–150K = **$150–375M**. A per-deployment take rate is the bigger prize. Integration is 60–75% of project cost [VM]. If ~500K industrial robots are installed per year [U, from memory of IFR figures] plus AMR projects, at roughly $50–100K of engineering per project, that is a $25B+ services pool. Taking 3–5% through software gives **$1B+**.
- **Why now:** LLM agents can now write PLC and robot code and compliance documents. ISO 10218 was updated in 2025. SI scarcity and labor shortages are acute, and integration is buyers' #1 stated barrier.
- **Why incumbents can't:** Each OEM tool (Flowstate, MujinOS, UR) covers one brand. SIs lack software DNA. Siemens and Rockwell cover PLCs, not multi-vendor cells [U].
- **90-day pilot:** Partner with one mid-size SI on 3 live projects. The agent produces the risk assessment, I/O mapping and robot program skeleton. Measure engineering hours against the SI's historical baseline.
- **Strongest kill risk:** The long tail of heterogeneity makes it services-heavy (the "AI-native integrator" margin trap). Google (Intrinsic plus Gemini) or Siemens could ship a "good enough" copilot. SIs have weak willingness to pay, so ACV may land at $20–40K, below the $50K bar.

### Thesis C — "Neutral performance and accountability layer for multi-vendor automation"
**One sentence:** *Vendor-neutral software that ingests telemetry from every robot and automation system in a company's network, normalizes KPIs, verifies RaaS/SLA invoices, and tracks each project against its business case, like an independent auditor plus Datadog for warehouse automation.*

- **Who buys:** VP Automation/Engineering and the CFO at 3PLs (GXO, DHL), retailers, CPG and automotive. Champions are people who have just watched a project miss its goals (up to 50% do [VM]).
- **Market math:** About 2,000 enterprises with multi-vendor automation [U] × $100–250K = **$200–500M**. Per-site expansion at $20–40K × the 53K sites [V] growing 20–30%/yr gives **$1B+ by 2030** if the product becomes the system of record.
- **Why now:** RaaS and per-pick pricing are spreading. VDA 5050 v3 and MassRobotics give standard telemetry hooks. Mixed fleets are growing, and boards are asking where the automation ROI went.
- **Why OEMs/WES can't:** OEMs won't grade themselves or verify their own invoices. WES vendors are tied to one execution stack and are themselves vendors being judged.
- **90-day pilot:** One 3PL with 3–5 sites and 2+ robot vendors. Connect via VDA 5050/MassRobotics feeds, WMS logs and invoices. Deliver a normalized OEE/uptime view, an invoice reconciliation and a variance-to-business-case report. Success means finding $250K+ in SLA credits or recoverable throughput.
- **Strongest kill risk:** Data access, since OEMs can throttle APIs. It may also be perceived as a "nice dashboard," with Manhattan or Körber adding analytics. Honestly, the 500-robots-from-6-vendors customer is still rare in 2026, so this may be 12–24 months early for anyone outside the top 200 operators.

---

## 3. Honest ranking

1. **Thesis A**: best fit with "where the world is going" and with the founders' AI skills. It sells to a cash-rich buyer pool now. Its weakness is early competition (YC S26) and absorption by Foxglove or Encord.
2. **Thesis B**: biggest proven pain and clearest $, but the riskiest on ACV and services drag.
3. **Thesis C**: neutral wedge with a clear VC sentence, but timing and data access are the risks.

None of these is a clean "huge pain NOW with $50K+ ACV from many buyers" winner. Physical AI is still a 2027–2029 market at the end-user layer. The most venture-scale and least absorbable play is selling to robot builders (Thesis A, or a teleop/intervention ops variant of P2) while their fleets scale.
