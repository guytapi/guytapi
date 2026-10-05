# Round 2: AI Labor Replacement in Skilled B2B Work Pools

*Analyst stance: skeptical. Research date: 2026-10-05. Searches used: 35 (WebSearch only; WebFetch not used).*

**Conventions**
- **[V]** means a search result snippet states the claim directly. The URL is listed.
- **[U]** means unverified: my estimate, or a vendor's own claim I could not check independently.
- Market-size figures come from market-research vendors (Mordor, IMARC, Data Bridge and others). Treat them as rough indications only. Vendor numbers often disagree with each other by 2x or more.
- Every URL below appeared in a search result. None were made up. I did not open the pages, so I have only seen each claim as a snippet.

---

## 0. Headline finding (read this first)

**Most of the obvious "AI replaces a labor pool" categories already had well-funded entrants by mid-2026.** ERP implementation (6+ funded entrants in 2026), MEP design (Endra, $75M from a16z), QA testing (Momentic, QA Wolf and others), market research (Listen Labs at a $500M valuation), IT L1/L2 (Serval at $1B) and industrial sales engineering (Atira, Accel seed, Sept 2026) are all taken or crowding fast.

What is left falls into two groups:
- **(a) Narrow vertical wedges** inside big pools, where the work depends on unstructured specs and drawings and the leaders are horizontal.
- **(b) Unglamorous pools that VCs have not yet noticed.** Examples: distributor product data, fabrication and shop-drawing detailing, make-ready/OSP engineering.

The failure mode from Round 1 was "platform absorbs you." It applies directly to group (b). PIM vendors, Trimble/Autodesk and Amazon are already shipping AI features.

---

## 1. Candidate table (summary)

| # | Labor pool | Pool size evidence | $/customer/yr (est.) | Key competitors (funding) | Verdict |
|---|---|---|---|---|---|
| 1 | Manual QA / software testing (outsourced) | ~$48–52B testing services 2025 [V] | $200K–$2M QA vendor spend at mid/large software orgs [U] | Momentic ($19.2M), QA Wolf ($36M Series B), QA.tech (€3M), BotGauge ($2M), TesterArmy (~$1.2M), Quash, Tricentis agentic platform | MEDIUM-WEAK (crowded) |
| 2 | Packaged-app (SAP/ERP) regression testing | Part of #1 and #3 | $300K–$3M per SAP program [U] | Tricentis (SAP ECT partnership, agentic platform, bought Tabnine Jul 2026) | WEAK (incumbent lock) |
| 3 | ERP implementation / SI labor | $29.5B ERP impl. services 2025 (Mordor) [V]; S/4 SI market >$108B by 2032 [V]; "$50B+/yr on consultants" (Trope claim) [U] | $1M–$20M per project | Auctor ($20M, Sequoia), Tessera Labs ($60M Series A, a16z), June AI ($20M pre-seed), Trope (YC S26), Nova Intelligence ($31.5M A), DualEntry ($90M A) | MEDIUM: biggest pool, but now the most crowded |
| 4 | Data migration services | Feature of #3 | $200K–$2M per migration [U] | DualEntry "NextDay Migration," Nova, Hypercubic, Kodesage (€2.3M) | WEAK as standalone (feature, not company) |
| 5 | MEP design drafting (AEC) | Data center construction $50.7B SAAR Apr 2026, +79% in 2 yrs [V]; backlogs to 2029 [V] | $100K–$1M per MEP firm [U] | Endra ($75M; $50M A from a16z, Jun 2026), Eagle (Lightspeed, AI roll-up of engineering firms) | MEDIUM (real pain, leader funded) |
| 6 | Drawing QA/QC and code-compliance checking | BLS drafters median $65,380 (2024) [V] | $50K–$300K per firm [U] | Structured AI (YC), Kestrel Labs ($2.2M), CodeComply.ai ($2M), PlanChecker.ai, AutoReview, Permitify ($500K) | WEAK-MEDIUM (half the buyers are municipalities, i.e. gov) |
| 7 | Steel/MEP fabrication detailing and shop drawings | Detailing largely offshored (India/Philippines) [U]; Tekla shipping AI fabrication drawings [V] | $250K–$3M per large fabricator/subcontractor [U] | Trimble Tekla 2026 AI Cloud Fabrication Drawings, ALLPLAN Steel Genie, Ferra ($3.3M, estimating), SketchDeck.ai | MEDIUM (open wedge, incumbent risk) |
| 8 | Construction takeoff/estimating | n/a | $20K–$100K [U] | Attentive.ai/Beam ($48M total; $30.5M B Insight), Togal.AI, many more | WEAK (crowded, low ACV) |
| 9 | Industrial sales/applications engineering (RFQ to configured bid) for engineered-to-order products | ">$128B annual labor spend" (Atira's claim) [U, vendor] | $150K–$500K [U] | Atira ($17.5M, Accel, Sept 2026), Korso (YC S26), Uptool ($6M, Khosla/Eclipse/Bessemer/KP), Mercura ($2.1M, YC), Hexa ($500K) | STRONG pain, MEDIUM-STRONG opportunity (race on now) |
| 10 | Software RFP / security questionnaires | n/a | ~$20K/yr (Loopio list price) [V] | Loopio, Responsive, Inventive (YC), Arphie, AutoRFP | WEAK (ACV too low, crowded) |
| 11 | SaaS presales / sales engineers | n/a | $50K–$200K [U] | Vivun (Ava agent), DocketAI ($15M) | WEAK |
| 12 | Product data onboarding/enrichment (distributors and manufacturers) | 2–5 hrs and 10–15 interactions per SKU launch; ~15,000 data issues per distributor per year [V, vendor blog] | $100K–$500K at 100K+ SKU distributors [U] | Akeneo (bought Unifai), Inriver, Feedonomics/BigCommerce, Pivotree, Mirakl, Lasso, Catalog ($3M pre-seed), Hypotenuse, Anglera (funding not found) | MEDIUM-STRONG (absorption risk) |
| 13 | Technical documentation / service manuals (manufacturing) | BLS: 56,400 US technical writers, median $91,670 (2024) [V]; offshore tech-pubs vendors (HCL etc.) | $200K–$2M for OEMs with large fleets [U] | Circuit ($30M seed), INSTRKTIV DocRock, Code and Pixels, HCLTech | MEDIUM-WEAK (US pool small; aerospace/defense part excluded) |
| 14 | Localization / translation | $72.6B 2025, <1% CAGR to 2030 [V] | varies | DeepL, Smartling, Lilt, LSP majors (not re-verified this round) | WEAK (deflating, commoditized) |
| 15 | Market research (qual interviews) | n/a this round | $100K–$1M at enterprises [U] | Listen Labs ($69M B at $500M), Outset ($17M A), Aaru, Simile, Keplar | WEAK (crowded) |
| 16 | IT MSP L1/L2 | n/a | n/a | Serval ($127M total, $1B valuation) | WEAK (taken) |
| 17 | Network operations center (NOC) | CIOs expect ~25% of network engineers to retire by ~2028 (Opengear 2023, via Fierce) [V] | $200K–$2M [U] | Aviz Networks (AI NOC), Supertrace AI, Kentik, EPAM/Sutherland/iOPEX (BPO-led) | MEDIUM-WEAK (telco buyers slow; vendor platforms absorb) |
| 18 | Fiber OSP design and make-ready engineering (private fiber) | Maine Fiber Co: make-ready is "our single largest operating expense" [V]; manual fiber design 45–60 days vs ~25 automated (Wipro) [V] | $300K–$3M per mid-size fiber builder [U] | IQGeo, VCTI Broadband IQ, CHR Solutions, Deepomatic; **no VC-funded AI-native startup found** [search gap, U] | MEDIUM (whitespace, but ~40% of builds are co-ops/munis [V] plus BEAD gov money) |
| 19 | Utility asset inspection review | Utility engineers took 6–8 months; AI takes hours/days (Buzz claim) [V, vendor] | $500K+ per utility [U] | Buzz Solutions ($20M A, S3), Zeitview ($60M) | WEAK-MEDIUM (regulated utilities, slow procurement, taken) |
| 20 | Marketplace management for brands | Fewer than 8,000 sellers drive half of Amazon US 3P sales [V] | $30K–$150K [U] | Lumian ($3M), Kily ($3.2M); **Amazon opened Seller Central to Claude/agents, Sept 23 2026** [V] | WEAK (platform absorption, the Round 1 failure mode) |
| 21 | PLC / industrial controls engineering | Controls system integrator labor [U] | $100K–$1M [U] | Gigaton ($26M A, Plural), Nexus Intelligence ($4.8M), PLCs.ai ($4M), PLC Copilot (seed) | MEDIUM (safety-critical; replacement hard; "assist" for now) |
| 22 | Manufacturing quality engineering (CAPA/8D) | n/a | $50K–$200K [U] | iFactory, ComplianceQuest, Omnex, Siemens + Instrumental | WEAK (assist not replace; QMS incumbents; med-device regulated) |
| 23 | Civil site design (land development) | n/a | $100K–$500K per civil firm [U] | Allsite.ai, Inertia LandAI, Bentley copilots | MEDIUM-WEAK |
| 24 | Patent drafting | Excluded (legal-heavy regulated) | n/a | Not researched | EXCLUDED |

---

## 2. Candidate detail (evidence and why still unsolved)

### 1. Manual QA / software testing
- **Labor pool:** Testing services market of ~$48B (Mordor) to ~$52B (outsourced, per Technavio-type sources) in 2025 [V]. India-heavy offshore manual testing [U].
- **Who pays:** VP Engineering at software companies, and enterprise IT.
- **Evidence:** https://dreamix.eu/insights/outsourced-software-testing-guide-2025/ ; https://technavio.com/report/outsourced-software-testing-market-industry-analysis
- **Competitors:**
  - Momentic: $19.2M total, $15M Series A Nov 2025. https://pulse2.com/momentic-15-million-series-a/
  - QA Wolf: $36M Series B. https://neuronfeed.com/compare/momentic-vs-qa-wolf
  - QA.tech: €3M. https://arcticstartup.com/qa-tech-raises-e3-million-seed
  - BotGauge: $2M. https://entrackr.com/snippets/ai-software-testing-startup-botgauge-ai-raises-2-mn-led-by-surface-ventures-11092144
  - Quash: pre-seed. https://entrackr.com/snippets/agentic-ai-startup-quash-raises-pre-seed-round-led-by-arali-ventures-8608038
  - TesterArmy, and ManaMind (games QA, $2M, Apr 2026).
  - "$844M tracked funding in AI testing category" [V, neuronfeed].
- **Why not solved:** Web E2E is now a funded category. The enterprise long tail (thick clients, SAP GUI, mainframe green screens) is still manual, but Tricentis owns it.
- **Verdict:** MEDIUM-WEAK.

### 2. SAP / packaged-app regression testing
- **Evidence:**
  - Tricentis launched its agentic QE platform in Mar 2026. It reports up to 60% automation of regression grids and covers ~200 ERPs.
  - It launched SAP ECT AI test generation in May 2026 and acquired Tabnine in Jul 2026.
  - Sources: https://www.tricentis.com/news/tricentis-releases-agentic-ai-testing-sap-business-transformation ; https://sapinsider.org/blogs/tricentis-tabnine-acquisition-agentic-sap-testing/
- **Verdict:** WEAK. Tricentis is resold by SAP, which is the definition of "absorbed by platform."

### 3. ERP implementation / SI labor (largest pool)
- **Labor pool:**
  - $29.52B ERP implementation services in 2025, rising to $31.05B in 2026 (Mordor) [V]. https://www.mordorintelligence.com/industry-reports/erp-implementation-services-market
  - S/4HANA SI services market >$108.5B by 2032 [V]. https://sapinsider.org/blogs/sap-s-4hana-systems-integrator-services-market-to-pass-100-billion-by-2032/
  - ECC deadline: one source says 2027 and ~12,000 customers. Fortune says the deadline was pushed to 2030 [V, conflicting]. https://www.fortune.com/2026/05/05/exclusive-nova-intelligence-ai-sap-chemistry-emma-qian/
- **Competitors (all 2026):**
  - Auctor: $20M Series A, Sequoia, sells to SIs. https://www.sovereignmagazine.com/article/auctor-20m-sequoia-system-integrators
  - Tessera Labs: $60M Series A, a16z, ECC to S/4. https://www.tamradar.com/funding-rounds/tessera-labs-series-a-60m
  - June AI: $20M pre-seed. https://www.trysignalbase.com/news/funding/june-ai-raises-200m-pre-seed-for-ai-native-system-integration
  - Trope (YC S26): https://www.ycombinator.com/companies/trope
  - Nova Intelligence: $31.5M.
  - DualEntry: $90M Series A, ERP plus migration. https://sundayguardianlive.com/feature/ai-startup-dualentry-raises-90-million-to-deepen-erp-market-push-2-154204/
- **Why not solved:** Implementations are political and multi-stakeholder, and liability sits with the SI. Most entrants sell tools *to* SIs rather than replacing them.
- **Verdict:** MEDIUM. The sub-segment that is still open is mid-market NetSuite/Dynamics/Acumatica *delivered as a fixed-fee AI-native SI*. Entry is late, though.

### 4. Data migration
- Already a wedge for DualEntry, Nova, Hypercubic and Kodesage. https://app.dealroom.co/news/feed/kodesage-secures-2-3m-for-ai-platform
- **Verdict:** WEAK standalone.

### 5. MEP design (AEC)
- **Pain:**
  - US private data center construction ran at a $50.7B SAAR in Apr 2026, up 79% in 2 years [V].
  - "Engineering firms cannot hire their way out of the current backlog" [V].
  - Sources: https://hackernoon.com/endra-expands-to-the-us-with-$50m-firepower-as-data-center-boom-outruns-engineering-workforce ; https://learnformula.com/latest-intelligence/the-data-center-distortion-decoding-the-enr-2026-top-500-and-the-31percent-surge-redefining-us-design
- **Competitors:**
  - Endra: $75M total, $50M Series A from a16z Jun 2026, Power Studio launched Sept 16 2026. https://pulse2.com/endra-raises-50-million-series-a-to-build-ai-based-infrastructure-platform-for-mep-engineering-firms/
  - Eagle: Lightspeed, buys and AI-transforms civil/structural/MEP firms. https://apis.io/providers/eagle/
- **Verdict:** MEDIUM. Huge pain, but the category leader is well funded.

### 6. Drawing QA/QC and code compliance
- Structured AI (YC): https://www.ycombinator.com/companies/structured-ai/jobs/YMmsemK-founding-operations-lead
- Kestrel Labs, $2.2M: https://ascendants.in/business-stories/kestrel-labs-raises-2-2m-ai-building-code-permitting-software/
- CodeComply.ai, $2M: https://www.trysignalbase.com/news/funding/codecomply.ai-secures-2-million-in-seed-funding-to-revolutionize-permitting-processes-with-ai
- CivicPlus brought AI plan review to municipalities: https://www.civicplus.com/news/nn/civicplus-brings-ai-building-plan-review-codecomply-ai/
- **Verdict:** WEAK-MEDIUM. Municipal buyers are excluded (gov). The firm-side QA/QC tool is likely ~$30–80K ACV and is a feature of #5.

### 7. Fabrication detailing and shop drawings (steel, MEP, rebar)
- **Evidence:**
  - Trimble Tekla 2026 "AI Cloud Fabrication Drawings" trains on a fabricator's historical drawings [V]. https://www.nomic.ai/glossary/ai-cloud-fabrication-drawings
  - ALLPLAN Steel Genie: AI steel takeoff, Apr 2026 [V].
  - Ferra: $3.3M, steel estimating. https://www.vcbacked.co/company/ferra
  - SketchDeck.ai: Boreal/BDC, Apr 2026. https://edmonton.taproot.news/briefs/2026/04/28/steel-estimation-startup-looks-to-expand-after-investment
  - Industry debate: https://www.advenser.com/2026/05/29/is-ai-taking-over-the-steel-detailing-industry/
- **Labor pool:** Detailing is heavily outsourced to Indian and Philippine detailing shops [U, widely known, not quantified here].
- **Why not solved:** Funded startups are on *estimating*, not *detailing/coordination*. Detailing output must be fabrication-exact, and errors cost real steel.
- **Verdict:** MEDIUM. Incumbent (Trimble) risk is high.

### 8. Construction takeoff
- Attentive.ai/Beam, $30.5M Series B: https://www.businesswire.com/news/home/20251112659082/en/Attentive.ai-Secures-$30.5-Million-Series-B-to-Accelerate-AI-Innovation-in-Construction
- Togal: https://www.togal.ai/news/togal-ai-raises-5-million
- **Verdict:** WEAK.

### 9. Industrial sales/applications engineering (engineered-to-order)
- **Pain:** An RFQ response "can take weeks or several months" and needs sales engineers, specialists, legal and commercial teams [V].
- **Labor pool:** Atira claims more than $128B/yr in global industrial sales-engineering labor [U, vendor].
- **Competitors:**
  - Atira: $17.5M, Accel-led seed, Sept 2026; customers landed without a sales team. https://tech.eu/2026/09/03/atira-raises-175m-to-bring-ai-orchestration-to-industrial-sales/ ; https://pulse2.com/atira-raises-17-5-million/
  - Korso (YC S26): https://ycombinator.com/companies/korso
  - Uptool: $6M seed, job-shop quoting. https://app.dealroom.co/companies/uptool
  - Mercura: $2.1M seed, YC/TQ/SignalFire, wholesale and construction quotes. https://seedtable.com/companies/mercura/funding-rounds/seed-2025-12
  - Hexa: $500K.
- **Incumbents:** CPQ vendors (Tacton, Configit, Salesforce CPQ; not verified this round) need hand-built rule models. They do not read 300-page spec packs.
- **Why not solved:** Product knowledge is tribal, rules are scattered across PDFs/ERP/CAD, and mistakes become warranty liability.
- **Verdict:** STRONG pain, MEDIUM-STRONG opportunity. The race started in 2026 and Atira is ahead in Europe. A US vertical wedge (data center electrical/thermal equipment) is still plausible.

### 12. Product data onboarding for distributors and manufacturers
- **Evidence:**
  - 2–5 hrs per SKU launch; ~15,000 inaccurate product-data issues per distributor per year [V, vendor-cited stat]. https://www.anglera.com/blog/mro-industrial-state
  - Supplier portals fail. https://distributionstrategy.com/2026/03/the-supplier-portal-trap-why-distributors-should-stop-waiting-and-start-enriching/
  - BigCommerce/Feedonomics launched AI enrichment in Sept 2026 [V]. https://distributionstrategy.com/2026/09/commerce-expands-ai-product-data-tools-as-it-sharpens-b2b-strategy/
  - Inriver Summer 2026 "system of work" release [V]. https://aimagazine.com/globenewswire/3319610
  - Akeneo acquired Unifai [V].
  - Catalog: $3M pre-seed. https://simplify.jobs/c/Catalog
- **Why now:** AI shopping agents and LLM procurement cannot parse messy B2B catalogs [V, vendor framing]. That makes data quality a revenue problem, not a hygiene problem.
- **Why not solved:** The work is a long tail of supplier formats, and incumbents sell software seats rather than finished outcomes.
- **Verdict:** MEDIUM-STRONG pain. **Absorption risk is high:** PIMs and commerce platforms are shipping exactly this, which is the Round 1 failure mode.

### 13. Technical documentation (manufacturing)
- BLS technical writers: 56,400 employed, median $91,670 [V]. https://www.bls.gov/ooh/Media-and-Communication/Technical-writers.htm
- Circuit: $30M seed. https://www.tamradar.com/funding-rounds/circuit-seed-30m
- HCLTech AI tech-pubs: https://www.hcltech.com/blogs/ai-automation-aerospace-technical-publications
- **Verdict:** MEDIUM-WEAK. The US pool is small, and big tech-pubs spend is in aerospace/defense, which is excluded.

### 14. Localization
- $72.6B in 2025, growing <1%/yr [V]. https://voxbooster.com/blog/localization-industry-statistics-2026 ; https://www.nimdzi.com/nimdzi-100-2025
- **Verdict:** WEAK. The market is deflating: AI is shrinking the spend pool rather than moving it to a new vendor.

### 15. Market research
- Listen Labs: $69M Series B at a $500M valuation, revenue 8 figures. https://pulse2.com/listen-labs-69-million-series-b/amp/
- Outset: $17M. https://getcoai.com/news/outset-raises-17m-to-automate-market-research-with-ai-interviews/
- **Verdict:** WEAK (taken).

### 16. IT MSP L1/L2
- Serval: $1B valuation. https://finance.yahoo.com/news/ai-startup-serval-valued-1-110259800.html
- **Verdict:** WEAK.

### 17. NOC
- Network-engineer retirement claim: https://www.fierce-network.com/cloud/supertrace-ai-builds-ai-noc-networks-face-looming-talent-crunch
- Aviz AI NOC: https://vimeo.com/1182199751
- **Verdict:** MEDIUM-WEAK. Carriers buy slowly, and Cisco/Juniper/Kentik platforms will absorb this.

### 18. Fiber OSP / make-ready engineering
- **Evidence:**
  - Make-ready is "our single largest operating expense" (Maine Fiber Co) [V]. https://www.fierce-network.com/telecom/maine-fiber-company-utility-pole-attachment-make-ready-our-single-largest-operating-expense
  - Design takes 45–60 days manually vs ~25 days with AI [V]. https://www.wipro.com/communications/articles/ai-transforms-fiber-network-deployment-connecting-everyone-to-tomorrow/
  - VCTI says design is 40x faster. https://www.fiberopticsonline.com/doc/vcti-accelerates-long-haul-fiber-route-design-by-x-with-broadband-iq-0001
  - Co-ops, munis and independent ISPs drive ~40% of builds [V]. https://www.communitynetworks.org/content/national-fiber-buildout-goes-local-co-ops-munis-and-independent-isps-drive-40-percent-fiber
- **Competitors:** IQGeo, VCTI, CHR Solutions, Deepomatic. Most of the work goes to engineering contractors (OSP design firms that pay offshore drafters) [U].
- **Gap:** No VC-funded AI-native make-ready/OSP design startup appeared in my searches [U, a search miss is not proof].
- **Verdict:** MEDIUM. Real whitespace, but the build cycle is tied to BEAD/government money and there are few large private buyers.

### 19. Utility asset inspection
- Buzz Solutions: $20M Series A. https://dealroom.co/news/143006-buzz-solutions-raises-20m-series-a-to-scale-grid-inspection-ai/
- Zeitview: $60M. https://finder.techleap.nl/news/feed/zeitview-raises-60m-for-ai-powered-infrastructure-inspection-platform
- **Verdict:** WEAK-MEDIUM.

### 20. Marketplace management
- Lumian: $3M. https://pulse2.com/lumian-3-million-raised-to-build-ai-native-amazon-agency-with-specialized-agents-for-brand-operations/
- Amazon opened Seller Central to Claude [V]. https://enterprisedna.co/resources/news/amazon-seller-central-claude-plugin-agentic-workflows-2026/
- **Verdict:** WEAK. Amazon itself is absorbing the agent layer.

### 21. PLC / controls engineering
- Gigaton: $26M Series A. https://news.latent.space/story/clu_vbvsv5
- PLCs.ai ($4M): https://www.caplight.com/company/plcs
- Nexus ($4.8M): https://www.caplight.com/company/getnexus
- **Verdict:** MEDIUM. The pool is large and aging, but the work is safety-critical, so "replace" is 3+ years out.

### 22. Manufacturing CAPA/8D
- Evidence is mostly vendor marketing: https://ifactoryapp.com/article/ai-vision-to-capa-automated-workflow
- **Verdict:** WEAK.

### 23. Civil site design
- Allsite.ai: https://www.esri.com/about/newsroom/arcnews/ai-and-arcgis-help-automate-design-for-large-scale-developments
- AEC Magazine on civil design agents: https://aecmag.com/news/ai-agent-for-civil-design-expands-reach/
- **Verdict:** MEDIUM-WEAK.

### Macro pool evidence
- India engineering services outsourcing: $62.8B in 2025 (IMARC) [V]. https://www.imarcgroup.com/india-engineering-services-outsourcing-market
- India ER&D services: $133.7B (Mordor) [V]. https://www.mordorintelligence.com/industry-reports/india-engineering-research-and-development-services-market
- This is the offshore pool that the AEC, detailing, documentation and controls theses all draw from.

---

## 3. Three best theses

### Thesis A (best): AI applications-engineering team for data center and electrification equipment makers
> **"We are the AI applications-engineering team that turns a 300-page spec pack into a compliant, configured, priced bid in 48 hours. We replace the 20–40-person sales-engineering department at engineered-to-order electrical and thermal equipment makers."**

- **Buyer:** VP Sales / COO at engineered-to-order manufacturers with $200M–$5B revenue. Products: switchgear, UPS/power distribution, chillers/CRAHs, gensets, pumps/valves, transformers.
- **Buyers × ACV:**
  - ~2,000–4,000 such manufacturers in NA+EU [U, estimate].
  - ACV of $150K–$400K, priced against SE headcount: 20 SEs × ~$130K loaded ≈ $2.6M/yr [U].
  - Serviceable revenue ≈ $0.3–1.6B. Expansion into order engineering and submittals adds more.
- **Why now:**
  - Data center construction is up 79% in 2 years [V], which floods equipment makers with RFQs.
  - Spec packs are unstructured PDFs, which LLMs can now read.
  - Speed-to-quote drives win rate.
- **Why incumbents can't:** CPQ vendors need clean rule models that these firms don't have. ERP vendors don't read specs. SIs bill hours.
- **90-day pilot:**
  - Weeks 1–4: replay 50 historical RFQs and score against the bids actually submitted (spec compliance, BOM accuracy, exceptions flagged).
  - Weeks 5–12: shadow live RFQs. KPI is SE-hours per bid and quote turnaround.
  - Paid pilot at $25–50K.
- **Strongest kill risk:** Atira (Accel, $17.5M, Sept 2026) and Korso/Uptool get there first.
  - Second risk: each customer's product logic is bespoke, so deployments become a services business with weak gross margins.
  - Must validate: will a VP Sales trust AI output on a bid that carries liquidated damages?

### Thesis B: AI detailing department for fabricators and MEP/steel subcontractors
> **"We are the AI detailing department that turns approved design models into fabrication-ready shop drawings and coordination packages. We replace the offshore detailing shops that steel fabricators and mechanical/electrical subcontractors pay by the ton or by the sheet."**

- **Buyer:** VP of VDC / Operations at the top ~1,500 US steel fabricators and large mechanical/electrical subcontractors [U, estimate].
- **Buyers × ACV:**
  - ACV of $200K–$1M, displacing detailing spend at outsourced rates [U].
  - 1,500 × $300K ≈ $450M US, roughly 2x with EU/AU.
- **Why now:**
  - The data center backlog runs to 2029 [V].
  - The trades labor shortage needs 456K new workers in 2027 (ABC) [V].
  - Funded AEC AI money has gone to the *design* side (Endra) and *estimating* side (Beam, Ferra), not to fabrication detailing.
- **Why incumbents can't:** Trimble/Autodesk sell seats to detailers. Delivering finished drawings with error liability would cannibalize their seat model and their partner channel.
- **90-day pilot:** Take a completed project. Regenerate its shop drawings from the IFC model and diff them against the issued drawings. Then detail one live package in parallel with the existing vendor. KPIs: RFIs, revision count, sheets per day.
- **Strongest kill risk:** Trimble Tekla's "AI Cloud Fabrication Drawings" (2026) [V] becomes good enough inside the tool fabricators already use. This is the platform-absorption failure mode again.

### Thesis C: AI product-data team for industrial distributors
> **"We are the AI product-data team that onboards, normalizes and enriches every supplier SKU so it can be found by buyers and AI agents. We replace the offshore data-entry and content teams at industrial distributors."**

- **Buyer:** VP eCommerce/Digital at MRO, electrical and plumbing distributors with $300M+ revenue, and at their manufacturers.
- **Buyers × ACV:** ~1,000–2,000 distributors [U] × $100K–$300K ACV, priced per SKU-onboarded ≈ $0.2–0.6B. Manufacturers add an upside of similar size [U].
- **Why now:**
  - B2B buying is moving to AI agents.
  - Each SKU takes 2–5 hours to launch [V, vendor stat].
  - Commerce platforms are launching enrichment now (Sept 2026) [V], which shows demand.
- **Why incumbents can't (partially):** PIMs store data but don't chase suppliers or own accuracy. This works only if sold as an outcome (guaranteed time-to-live and accuracy SLA) rather than a tool.
- **90-day pilot:** Take a 20K-SKU backlog of unlaunched supplier items. KPIs: time-to-live, attribute completeness, search conversion lift.
- **Strongest kill risk:** Akeneo (with Unifai), Inriver, Feedonomics and Mirakl bundle "good-enough" AI enrichment into existing contracts. ACV gets squeezed toward $50K.

**Wildcard, not top 3:** AI make-ready/OSP engineering for private fiber builders (#18). There is evident whitespace and acute pain. It is excluded from the top 3 because the build cycle depends on BEAD/government funding and ~40% of buyers are co-ops and munis.

---

## 4. Skeptic's bottom line
- **Avoid:** ERP SI, QA testing, MEP design, market research, IT L1/L2, marketplace management, localization. All are funded or absorbed.
- **The only thesis that clears all three bars** (huge pain now, a tailwind from the data center/electrification capex wave, and a one-sentence pitch) is **A**. It is a race against Atira. The defensible version is a US vertical wedge, starting with data-center electrical/thermal equipment, with deep spec-compliance accuracy as the moat.
- **B and C are real** but carry the same platform-absorption risk that killed Round 1.
- **Next step:** Before committing, run 10 customer calls with VP Sales at engineered-to-order equipment makers (Thesis A). Validate SE headcount, RFQ volume and liability tolerance.
