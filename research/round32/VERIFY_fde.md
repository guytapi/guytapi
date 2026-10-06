# VERIFY: F-C "Forward-deployed implementation" (SOP to agent)

Date: 2026-10-06. Method: 21 WebSearch queries, run adversarially (looking for reasons the idea fails). WebFetch was not used, so all figures come from search snippets of the cited pages. [E] marks an estimate.

Wedge under test: **a product that turns a customer's SOP documents, call logs and tickets into a tested agent spec and eval suite, cutting each deployment from about 6 weeks to about 1. The first buyers are AI-agent vendors (VP Deployment). Enterprises building agents in-house come later.**

## Bottom line
**The pain is confirmed and is even bigger than SYNTHESIS assumed. The product, though, already exists, and the vendors sell it themselves.**

- **Hiring is exploding.** FDE postings on Indeed went from 643 to 5,330 between April 2025 and April 2026, up about 729%. Lightcast measured more than 1,000% growth.
- **The vendors in our own evidence list have already shipped this exact wedge:**
  - **Sierra Ghostwriter** takes "SOPs, transcripts from support calls, … audio recordings" and outputs "a production-ready agent", then runs its own loop of analyze, improve, test and ship.
  - **Decagon AOP Copilot** (Sep 2025) converts "rough notes or existing SOPs into production-ready AOPs".
  - **Intercom Fin Procedures** lets you paste an SOP and get a structured procedure back.
  - **Cresta Conductor** builds agents from real conversation data and claims deployment is "2x faster".
  - **Harvey Workflow Builder** has produced 18,000+ customer-built workflows.
  - **Salesforce Agentforce Builder** auto-generates topics from knowledge articles.
- **Vendors will not buy this from outside.** For them it is the product, not a tool. a16z frames the FDE as "trading margin for moat", so automating it in-house is what drives their margins up.
- **For the later enterprise buyer, the category is already funded and has a channel.** June raised $20M pre-seed from Benioff, Dell and Levie (Aug 2026), pitched explicitly as "an alternative to forward-deployed engineers". Interloom raised $16.5M to turn tickets, emails and transcripts into a context graph for agents. Skan raised a $63M Series C for "Blueprints". Celonis AgentC and Mimica cover process mining to agent. The channel is SIs plus the labs: OpenAI Frontier Alliances with McKinsey, BCG, Accenture and Capgemini, alongside OpenAI's own FDEs. Accenture alone books about $2.2B a quarter in advanced AI.

**Verdict: drops from 7.2 to 5.9. Kill it as framed.** A narrower buyer-side variant survives at about 6.2, unverified, and it overlaps with F-B.

## 1. Scale of FDE hiring (confirms the pain)

| Signal | Figure | Source |
|---|---|---|
| Indeed FDE postings | 643 (Apr 2025) → 5,330 (Apr 2026), +729% YoY | paraform.com/insights/forward-deployed-engineer-demand-quadrupled; latestly.com; dev.ua |
| Jan–Sep 2025 growth | +800% | paraform.com; inc42.com/features/why-forward-deployed-engineers-are-becoming-ais-hottest-jobs |
| Bloomberry analysis of 1,000 FDE jobs | +1,165% YoY | paraform.com |
| Lightcast, Jan–Aug 2026 vs. 2025 | >1,000% | paraform.com |
| Paraform platform, Q1'25 → Q1'26 | +350%; candidate pool grew only about 50% | paraform.com |
| Base pay | Anthropic $280–320k, OpenAI $185–300k plus equity (Sep 2026 postings). Median mid-level total comp $385k, staff $610k | vallettasoftware.com/blog/post/forward-deployed-engineer-salary; getperspective.ai 2026 FDE compensation report (1,200 FDEs) |
| Who builds FDE units | Meta, Anthropic, OpenAI, Box; 20+ YC startups | inc42.com; vccafe.com/the-9-billion-bet-on-forward-deployed-engineers |
| Margins | AI cos project 52% gross margin in 2026 (45% in 2025, 41% in 2024). One vendor now gives a dedicated FDE only to customers with ≥5,000 employees | saastr.com/iconiqs-latest-state-of-ai-report...; saastr.com/who-gets-an-fde-and-who-doesnt... |
| Skeptic view | Gartner: about 70% of vendor-led AI engineering "excursions" abandoned by 2028 | channeldive.com/news/can-forward-deployed-engineers-fdes-fix-ai-gartner/831816 |

How to read this: the pain axis is if anything *under*-scored. But the ≥5,000-employee FDE cutoff and the rising margins show that vendors are already solving it themselves, through tiering plus self-serve tooling.

## 2. Existing products and startups (this is what kills the idea)

### 2a. Agent vendors' own SOP-to-agent tooling (it removes the vendor buyer)
| Product | What it does | Source |
|---|---|---|
| **Sierra Ghostwriter** (Agent Studio) | "Upload SOPs, transcripts from support calls, photos of whiteboard sketches, process documentation, and audio recordings … identifies the key behaviors and edge cases … production-ready agent." It also feeds on "golden recordings" and runs an automatic analyze, improve, test and ship cycle | sierra.ai/product/ghostwriter; sierra.ai/product/agent-studio |
| **Decagon AOPs + AOP Copilot** (Sep 2025) | Natural-language SOPs compiled into executable logic. Copilot turns "rough notes or existing SOPs into production-ready AOPs". Its "test-driven agents" cover the eval half | decagon.ai/blog/aop-the-future-of-cx; getmacha.com/blog/decagon-ai-complete-guide |
| **Intercom Fin Procedures** | Paste an SOP and Fin structures it into steps, tools and guidance | intercom.com/help/.../13449439-building-fin-procedures; fin.ai/learn/ai-agent-procedures-aops-journeys |
| **Cresta Conductor** | "Agent for AI agent development", grounded in real conversations and knowledge bases. Claims deployment is 2x faster | cresta.com/press/cresta-launches-conductor...; martechseries.com |
| **Parloa AMP** | Large-scale simulated conversations before go-live | parloa.com/.../simulationstests; seedtable.com/products/parloa-ai-agent-management-platform-amp |
| **ElevenLabs Agents Testing** | Tests auto-generated from past conversations (from companies_B_apps.md) | elevenlabs.io/blog/tests-for-elevenlabs-agents |
| **Harvey Workflow Builder / Agent Builder** | Self-serve, with 18,000+ customer-built workflows. "Turning implementation from a model building project into a workflow rollout motion" | harvey.ai/blog/introducing-workflow-builder; sacra.com |
| **Salesforce Agentforce Builder** | Auto-drafts topics from knowledge articles and metadata, plus a testing center | salesforce.com/agentforce/agent-builder; hatenabase.jp |
| **Microsoft Copilot Studio** | Low-code agents and agent flows. Manufacturing scenarios turn expert walkthroughs into SOPs | adoption.microsoft.com/scenario-library/manufacturing/visual-work-instruction-agent |

**Four of the nine companies in our evidence list (Sierra, Decagon, ElevenLabs, Harvey) have each productized exactly the step the wedge targets.** Their FDE hiring keeps going because what FDEs mostly do is *integration, politics, change management and data access*, not writing specs. So the wedge's "6 weeks → 1 week" claim targets the part of the job that is already being automated, not the part that drives FDE headcount. [E]

### 2b. Independent startups going after "replace the FDE / implementation" for enterprises
| Company | Funding | Overlap | Source |
|---|---|---|---|
| **June** | $20M pre-seed, Aug 2026 (TIME Ventures/Benioff, Dell, Diane Greene, Levie, Kurtz). Founded by the Bonobo team (exited to Salesforce) | Auto-scans Salesforce, Workday and ServiceNow, generates agent workflows and implementation plans; "pitched as an alternative to forward-deployed engineers" | aiweekly.co/alerts/june-exits-stealth...; calcalistech.com; salesforceben.com |
| **Interloom** | $16.5M, Mar 2026 (DN Capital, Air Street) | Ingests support emails, tickets and transcripts into a "context graph" of how work actually gets resolved. Customers: Commerzbank, VW, Zurich | fortune.com/2026/03/23/interloom-ai-agents-raises-16-million...; finder.techleap.nl |
| **Skan AI** | $63M Series C | Observes desktop work, produces "Blueprint for AI deployment planning", plus Agents | tamradar.com/funding-rounds/skan-ai-series-c-63m; kyp.ai comparison |
| **Mimica** | VC-backed | Mapper produces implementation blueprints from desktop capture (RPA, GenAI, agents) | kyp.ai; dupple.com/learn/best-ai-process-mining-tools |
| **Celonis AgentC** | Large incumbent | Process intelligence fed into agent platforms | silicon.co.uk/press-release/celonis-agentc... |
| **Coval** ($28M Series A), **Cekura** ($2.4M seed) | | Simulation and testing of conversational agents, with enterprise and AI-native customers | coval.ai/blog/coval-vs-cekura; cekura.ai |
| SOP authoring tools (Scribe, Guidde, Cassidy) | | Turn captured work into SOPs, one step upstream of the wedge | scribe.com/tools/sop-generator; guidde.com |

## 3. Would vendors buy outside tooling? (Mostly no)
- **This is core IP and the margin lever.** a16z's "Trading Margin for Moat" says the FDE work *is* the moat. So the tooling that compresses it (Ghostwriter, AOP Copilot) gets built in-house and sold as a product to the vendor's own customers. Sierra markets Ghostwriter publicly as a feature (vccafe.com; sierra.ai).
- **Where vendors *do* buy outside tools, it is commodity infrastructure next to the core:** voice testing (Coval and Cekura customers include AI-native companies; Cekura names Lindy and HighLevel) and eval tooling (Braintrust; see VERIFY_eval_ops.md). The spec layer, which is the agent's own DSL (AOPs, Sierra's SDK, Fin Procedures), cannot be outsourced. A third-party spec would have to compile to every vendor's proprietary format.
- **The buyer pool is small and consolidating.** Sierra and Decagon are each valued at $4.5B+, and they are the agent vendors with real deployment headcount. That is a few dozen, not a few hundred [E], and the leaders are exactly the ones who already built this.

## 4. Enterprises as the later buyer: SIs vs. product
- **The services market is huge, and it is where the money goes.** Accenture's advanced-AI bookings were about $2.2B in Q1 FY26, with $11.5B cumulative across 11,000+ projects (fourweekmba.com; marketchameleon.com; spglobal.com). Deloitte has committed $3B through FY2030, runs an agentic practice with Google Cloud and has 1,000+ prebuilt agents (insidepublicaccounting.com; munich-startup.de). Gartner puts agentic AI spending at $201.9B in 2026 (+141%) and AI services at $588.6B (softwarestrategiesblog.com/2026/02/16/gartner-forecasts-agentic-ai...).
- **The labs route enterprise deployment through SIs plus their own FDEs.** OpenAI Frontier launched 2026-02-05, with Frontier Alliances (McKinsey, BCG, Accenture, Capgemini) investing in dedicated practices. Uber, Intuit and State Farm are early adopters (fortune.com/2026/02/23/openai-partners-with-mckinsey...; openai.com/index/introducing-openai-frontier).
- **What this means:** enterprises do pay a lot for implementation, but they pay *people* bundled with a platform. A product that automates implementation either sells *to* SIs as a delivery accelerator (SIs build their own, like Deloitte Zora and Accenture's internal tools, or take them from platform partners), or competes with June, Interloom and Skan, which already have money and enterprise logos. The way in for a new entrant is narrow.

## 5. Re-scored criteria

| Criterion | SYNTHESIS | Verified | Why |
|---|---|---|---|
| Pain today | 9 | 8 | Confirmed (+729% postings). But vendors now tier FDEs (≥5k-employee customers only) and self-serve the rest |
| Dollars attached | 9 | 8 | $385k median total comp × thousands of roles is real money. But most of it goes to integration and change management, not spec writing |
| Headcount attached | 10 | 9 | Confirmed at industry scale |
| Growth rate of pain | 8 | 8 | Lightcast >1,000% in 2026 |
| Ease of finding buyers | 6 | 4 | Vendor buyers build it themselves. Enterprise buyers buy through SIs or labs |
| 30-day pilotability | 5 | 5 | A pilot needs live systems access and a real deployment to compare against |
| Existing internal builds (signal) | 7 | 5 | Internal builds have become *shipped products* (Ghostwriter, AOP Copilot, Fin Procedures, Conductor). That still proves the pain, but it is the opposite of an opening |
| Competitive opening | 7 | 3 | Every vendor's own tool, plus June ($20M), Interloom ($16.5M), Skan ($63M), Celonis, Mimica, SIs and OpenAI Frontier |
| Expansion potential | 6 | 5 | Leads into agent ops and evals, which are crowded (see VERIFY_eval_ops.md) |
| $10B potential | 5 | 4 | Squeezed between platform-native builders and SIs |
| **Average** | **7.2** | **5.9** | |

## 6. Sharpest surviving wedge (unverified, about 6.2)
**A vendor-neutral "agent acceptance spec" for enterprise buyers.** It takes the enterprise's own SOPs, call logs and tickets and produces a portable behavioral spec plus a simulation and eval suite that the *buyer* owns. Uses:
1. Run 4–6-week Sierra vs. Decagon vs. Fin bake-offs on the same test set, with "resolution" defined in the contract. Buyer guides already tell enterprises to do this by hand (voiceflow.com/blog/decagon-vs-sierra; retellai.com/blog/sierra-vs-decagon).
2. Gate vendor releases and model upgrades as an acceptance test.
3. Make switching vendors cheap.

- **Why it survives:** no vendor will build a tool that makes it easy to switch away from them. The buyer, not the vendor, holds the incentive. And it uses the same SOP-to-spec engine.
- **Buyer:** Head of CX or the AI procurement owner at enterprises with 2+ agent vendors or an active RFP. It could also be sold to SIs running vendor selection.
- **Risks:** it overlaps F-B (eval/ground truth, verified at 5.9) and Coval/Cekura simulation. Deal sizes are bounded at $50–250k a year [E]. Vendors may resist trace access.
- **Email claim:** "Before you sign Sierra or Decagon, own the test. We turn your SOPs and 10k past tickets into a vendor-neutral test suite in 1 week, so the bake-off, the contract's resolution definition and every future model upgrade are scored by you, not the vendor's dashboard."

## Verdict
**F-C: 7.2 → 5.9. Kill it as framed.** The FDE boom is real (Indeed +729%, Lightcast >1,000%, $385k median total comp). But the "SOP/call logs → tested agent" product already ships inside Sierra (Ghostwriter), Decagon (AOP Copilot), Intercom (Fin Procedures), Cresta (Conductor) and Harvey (Workflow Builder). Those vendors treat it as their margin lever and will not buy it from outside. The enterprise version is funded (June $20M, Interloom $16.5M, Skan $63M) and channeled through SIs plus OpenAI Frontier. It is the same pattern as F-A and F-B: a pain visible across 5+ companies is visible to the companies themselves, and they productize it first. The only angle left is buyer-side and vendor-neutral acceptance testing (about 6.2, unverified), which folds into the F-B eval space.
