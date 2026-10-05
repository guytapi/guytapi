# Round 2: New Budget Lines and New Jobs Created by AI (2025-2026)

Analyst stance: skeptical. Date: 2026-10-05. Searches used: 34 of 35. WebFetch was not used; all figures come from search-result snippets.

**Source quality key.** [P] = primary source (company press release, SEC filing, earnings release). [N] = established news outlet. [B] = vendor blog, aggregator, or SEO page: directionally useful, but the numbers are unverified. **UNVERIFIED** = I could not confirm the claim from a primary source. Every URL below appeared in a search result. None were invented, and none were opened directly.

---

## 0. Bottom line up front

1. **The biggest new budget line is "AI deployment labor", not AI software.** It covers forward-deployed engineers (FDEs), SI AI bookings, OpenAI's $4B Deployment Company, Palantir bootcamps and Cognizant's 1,000 "context engineers". Enterprises pay humans to turn models into working workflows. This spend is large and growing quickly, and it is mostly not software yet.
2. **IT services firms are being forced onto fixed-price and outcome pricing.** TCS has about 80% of its BPS contracts outcome-based, and Cognizant has crossed 50% of revenue on fixed-price or outcome contracts. Every hour of delivery labor they automate is now their own margin. That gives a tooling vendor a buyer with a real incentive.
3. **The obvious "capture how work is done for agents" category is already crowded and well funded.** Skan has about $120M, Scribe is valued at $1.3B, plus Mimica, Celonis and UiPath. **Generic eval tooling is consolidating into platforms**, with Humanloop, W&B, Langfuse and Galileo all acquired or shut down. Do not enter either category head-on.
4. **The expert-data boom is real but lab-driven.** Mercor is at about $2B gross run-rate, Handshake AI at $1.1B and Snorkel at $3.5B. An enterprise-internal version exists only as a claim so far. Its demand is real but thin.
5. **None of the theses below is clearly STRONG.** The best one (Thesis A) is a medium-to-strong bet, and it carries a serious "vendors build it in-house" risk.

---

## 1. Evidenced problems and new-budget signals

### 1. FDE demand far outstrips supply
- **Problem:** AI deployments fail unless engineers build inside each customer's environment. FDE labor is scarce, expensive and does not scale.
- **Who:** AI-native app vendors (Decagon, Sierra, Harvey and others), labs, Palantir-style platforms, and SIs.
- **Evidence:** FDE postings grew from 643 (Apr 2025) to 5,330 (Apr 2026), +729% YoY. Postings rose about 800% in Jan-Sep 2025 while the candidate pool grew about 50%. [B] https://www.paraform.com/blog/forward-deployed-engineer-demand-quadrupled. A separate analysis of 1,000 postings found +1,165% YoY. [B] https://getperspective.ai/blog/2026-fde-hiring-trends-what-1000-job-posts-reveal/markdown
- **$ pain:** Embedded FDE teams are estimated at $7.5M-$10M per year per large program (**UNVERIFIED**, from a search summary). A single FDE likely costs $250K-$400K loaded (**UNVERIFIED**, my estimate).
- **Competitors:** Rocketlane ($105M total, $60M Series C in Mar 2026, "Nitro" agentic delivery). Perspective AI (discovery). Point tools such as Braintrust, LangSmith, Modal and Langfuse.
- **Why unsolved:** Each FDE engagement is bespoke. Existing tools cover engineering steps, not the full arc from discovery to spec to eval to rollout.
- **Verdict:** **STRONG** signal (pain and budget). The software gap is MEDIUM.

### 2. Consultancy AI implementation revenue is a large, proven budget
- **Evidence:** Accenture Q1 FY26 advanced-AI bookings were about $2.2B (nearly 2x YoY) and revenue about $1.1B. Cumulative figures are $11.5B in bookings and $4.8B in revenue across about 11,000 projects. Accenture then stopped disclosing these metrics. [N] https://www.benzinga.com/markets/earnings/25/12/49477793/accenture-says-ai-demand-is-rising-but-scale-remains-limited ; [P] https://mms.businesswire.com/media/20251218755982/en/2673833/1/Accenture_Reports_First-Quarter_Fiscal_2026_Results.pdf?download=1
- **Who:** CIO, CAIO and business-unit heads paying SIs.
- **$ pain:** Roughly $4-5B per year at Accenture alone. Industry-wide spend is likely more than $20B (**UNVERIFIED** extrapolation).
- **Why unsolved:** It is labor-priced. Only about 1,300 of 9,000+ Accenture clients are engaged, so scale remains limited.
- **Verdict:** **STRONG** budget signal.

### 3. Model labs are verticalizing into deployment services
- **Evidence:** OpenAI launched the Deployment Company with more than $4B of initial investment (TPG, Bain Capital, Brookfield, among others). It acquired Tomoro, which brought about 150 FDEs. [P] https://openai.com/index/openai-launches-the-deployment-company ; [N] https://techcrunch.com/2026/02/23/openai-calls-in-the-consultants-for-its-enterprise-push
- **Read-through:** This validates the budget. It is also a threat: labs will own the top 500 accounts. A software layer that makes their FDEs, and everyone else's, faster could have the labs as customers rather than competitors. That is speculative.
- **Verdict:** **STRONG** signal and a competitive threat.

### 4. Palantir shows that deployment speed wins enterprise AI
- **Evidence:** Q2 2026 US commercial revenue was $764M, +149% YoY. US commercial TCV was a record $2.132B. Bootcamps cut sales cycles to days. [P] https://www.sec.gov/Archives/edgar/data/0001321655/000132165526000039/a2026q2ex991pressrelease.htm ; [N] https://lasvegassun.com/news/2026/aug/03/palantir-reports-q2-2026-us-comm-revenue-growth-of/
- **Read-through:** Buyers pay a premium for time-to-working-workflow. Non-Palantir vendors lack that bootcamp machinery.
- **Verdict:** **STRONG** signal for a "deployment velocity" thesis.

### 5. AI pilots fail to reach production
- **Evidence:** MIT NANDA (2025) found about 95% of genAI pilots produced no measurable return. [B] https://letsdatascience.com/news/mit-report-documents-genai-pilot-roi-gap-e0924d7d. Gartner predicts more than 40% of agentic projects will be scrapped by 2027 because of cost, unclear ROI and risk. [N] https://www.scmp.com/tech/tech-trends/article/3316025/over-40-agentic-ai-projects-forecast-be-scrapped-2027-due-lack-value. "Only 28% of AI projects deliver promised ROI", driven by scoping the wrong problem (**UNVERIFIED** Gartner figure, via a vendor blog). [B] https://getperspective.ai/blog/ai-deployment-tools-forward-deployed-engineering-teams-2026
- **Verdict:** **STRONG** pain. It is a generic, much-cited statistic, though, and every vendor pitches against it.

### 6. Agents don't know how work is actually done (process knowledge gap)
- **Evidence:** Skan AI raised a $63M Series C in Aug 2026 (about $120M total) for a "Context Graph of Work". [B] https://www.unite.ai/skan-ais-series-c-bets-enterprise-ai-needs-a-map-of-real-work/. Mimica raised a $26.2M Series B in Sep 2025 ("AI agents have no idea how you actually do your job"). [B] https://www.startuphub.ai/ai-news/funding-round/2025/mimica-raises-26m-to-stop-ai-agents-from-failing.md. Scribe raised a $75M Series C at a $1.3B valuation in Nov 2025 for Scribe Optimize ("what should we automate first?"). [P] https://scribe.com/library/scribe-raises-series-c ; [N] https://siliconangle.com/2025/11/10/scribe-raises-75m-process-documentation-platform/. Other players include KYP.ai (Gartner task-mining guide), Screenpipe and bizMRI (2026, AI interviews employees). [B] https://screenpi.pe/task-mining ; https://www.cbinsights.com/company/bizmri
- **Incumbents:** Celonis, UiPath. UiPath's AI product ARR is about $200M of $1.853B total ARR, growing only 11%. [N] https://www.fool.com/earnings/call-transcripts/2026/03/12/uipath-path-q4-2026-earnings-call-transcript/
- **Verdict:** Real pain, but **WEAK as a new entry** because it is crowded and well capitalized. The open whitespace is "process capture → executable agent artifact plus eval suite", which incumbents are also chasing.

### 7. "Context engineer" is a new services role
- **Evidence:** Cognizant plans to deploy about 1,000 context engineers to capture enterprise knowledge and build "context packs". [N] https://www.nasdaq.com/articles/cognizant-invests-agentic-ai-adding-1000-context-engineers-2026. Gartner predicts context engineering in 80% of AI tools by 2028 (**UNVERIFIED**, via a vendor page). [B] https://atlan.com/know/what-is-context-engineering/
- **Read-through:** SIs are staffing a manual job. Software that turns one context engineer into ten has an SI buyer.
- **Competitors:** Atlan, Glean, Shelf.io, data catalogs, and the context layers of the platforms themselves.
- **Verdict:** **MEDIUM**.

### 8. Agent Skills means enterprises need skills/SOP libraries
- **Evidence:** Anthropic made Agent Skills an open standard (Dec 2025), adopted by Microsoft (VS Code, GitHub), Cursor and others. Org-wide skill management and audit trails shipped in Feb 2026. [N] https://venturebeat.com/ai/anthropic-launches-enterprise-agent-skills-and-opens-the-standard ; [N] https://siliconangle.com/2025/12/18/anthropic-makes-agent-skills-open-standard/.
- **Read-through:** SOPs are becoming a machine-executable artifact. Someone has to author, test and maintain thousands of them per enterprise. The registry itself is being absorbed by Anthropic and Microsoft, but authoring and validation from real work is not.
- **Verdict:** **MEDIUM**. This is a useful wedge format, not a company on its own.

### 9. SME review of agent output, with eval tooling consolidating
- **Evidence:** Databricks ships a managed-evals UI for SMEs. [P] https://docs.databricks.com/aws/generative-ai/agent-evaluation/managed-evals-sme. Humanloop, W&B, Langfuse and Galileo were all acquired or shut down between May 2025 and Apr 2026 (**UNVERIFIED** compilation). [B] https://atlan.com/know/ai-agent/ai-agent-evals/best-ai-agent-evaluation-platforms/
- **Verdict:** **WEAK** for horizontal eval. Platforms absorb it, which repeats the Round 1 pattern.

### 10. The expert-data market is huge but lab-driven
- **Evidence:** Mercor reached more than $2B gross annualized revenue in Jun 2026, with $614M gross in H1 2026. It is valued at $10B and in talks at $20B. [N/B] https://dealroom.co/news/137121-mercor-doubles-to-2b-gross-revenue-run-rate-as-ai-labs-buy-expert-data/. Handshake AI reached $1.1B gross annualized in Apr 2026 (+349%). [B] https://sacra.com/research/handshake-indeed-for-data-labelers/. Snorkel raised a $350M Series E at $3.5B in Sep 2026 and sells Expert Data-as-a-Service to enterprises. [B] https://www.implicator.ai/snorkel-ai-350m-series-e/ ; [P] https://snorkel.ai/press/snorkel-evaluate-and-snorkel-expert-data-as-a-service-empower-enterprises-to-evaluate-and-tune-specialized-ai-at-scale/
- **Enterprise-internal angle:** Mercor cites growth from "Fortune 500 customers looking to build their own models or fine-tune" (**UNVERIFIED** split). Invisible is pivoting from lab data to "enterprise AI operations": workflows, reviews and human signoff. [B] https://sacra.com/research/invisible
- **Verdict:** **MEDIUM**. The budget exists at labs. Enterprise-internal demand is plausible but unproven, and Snorkel and Invisible are already moving there.

### 11. RL environments for enterprise workflows
- **Evidence:** Bespoke Labs raised $40M total (Series A from Wing, Jul 2026). AfterQuery raised a $30M Series A (Apr 2026). Fleet is reported at about $60M run-rate within four months on a $15M seed (**UNVERIFIED**, from rl-list.com). [B] https://ai2.work/blog/bespoke-labs-bets-40m-that-agents-need-sandboxes-first ; https://www.rl-list.com/vendors/fleet-ai. Centific sells RL Environments-as-a-Service to labs and Fortune 500s. [P] https://www.centific.com/solution/rl-environments-as-a-service
- **Verdict:** **MEDIUM**. Buyers today are labs, where spend is concentrated and lumpy. Enterprise buyers are early.

### 12. Agent operations roles are a new job family
- **Evidence:** Decagon posts "Agent Success Manager" ($160K-$220K) and "Agent Strategy Manager" roles. [B] https://jobs.accel.com/companies/decagon-2/jobs/87247117-agent-success-manager. There have been 1,575 US AI-operations postings since Jan 2026, with titles such as AI Agent Manager and Agent Supervisor (**UNVERIFIED** recruiter data). [B] https://axialsearch.com/insights/ai-operations-jobs. "Agentic AI postings +280%, about 90K open" is low confidence. [B] same source.
- **Read-through:** This person tunes agents weekly from failed conversations, using spreadsheets and vendor consoles.
- **Verdict:** **MEDIUM**. The role is real, but vendors (Decagon, Sierra) build these consoles themselves.

### 13. QA of AI agents in customer service
- **Evidence:** Human QA covered only 1-2% of interactions. AI QA now covers 100%, and vendors QA human and AI agents together. [N] https://www.cmswire.com/the-wire/three-successkpi-ai-releases-automate-quality-review-work-for-human-and-ai-agents/ ; [B] https://blog.getdarwin.ai/en/ai-contact-center-quality-assurance-2026
- **Competitors:** MaestroQA, Observe.ai, Level AI, Cresta, SuccessKPI, plus CCaaS incumbents.
- **Verdict:** **WEAK**. It is crowded and platform-absorbed.

### 14. Knowledge-base quality caps AI resolution rates
- **Evidence:** Intercom Fin resolves about 51-66% on average. Unresolved cases are "often a content failure rather than a model failure." [B] https://www.usefini.com/guides/leading-ai-customer-support-knowledge-managers-enterprise
- **Competitors:** Intercom, Ada and Forethought each ship content-gap tooling, alongside Shelf.io and Guru.
- **Verdict:** **WEAK-MEDIUM**. The pain is clear, but the agent vendors own the fix.

### 15. "Workslop" and the AI verification tax
- **Evidence:** Workday (Jan 2026) found about 37-40% of AI time savings lost to rework, and only 14% of employees getting consistently positive net outcomes. [N] https://www.hcamag.com/au/specialisation/hr-technology/ai-productivity-gains-offset-by-rework-costs-study-finds/565096 ; [N] https://www.accountingtoday.com/news/time-saved-by-ai-partially-cancelled-out-by-time-spent-checking-ai. The estimated cost is $186 per employee per month, or about $8.9M per year for a 10K-person firm (**UNVERIFIED** methodology).
- **Verdict:** **MEDIUM** pain with **no clear buyer**. It is diffuse and horizontal, and Microsoft, Google and OpenAI will absorb it.

### 16. Agentforce implementation overruns
- **Evidence:** Year-1 cost runs 3-5x the quote ($150K-$600K versus a $50K budget) (**UNVERIFIED** vendor guide). [B] https://www.11x.ai/guides/agentforce-pricing. Agentforce ARR exceeds $1.2-1.5B. Meanwhile 0% of surveyed partners named Agentforce a bookings driver. [B] https://salesforcedictionary.com/news/salesforce-news-august-27-2026-agentforce-partner-revenue-gap
- **Read-through:** The implementation tax is real, but SIs aren't capturing it, likely because deals are small and fixed-fee. That margin squeeze could make them buy delivery tooling.
- **Verdict:** **MEDIUM**.

### 17. IT services are moving to outcome and fixed pricing
- **Evidence:** TCS has about 80% of BPS contracts outcome-based, double the share since late 2023. Cognizant's fixed-price and outcome contracts exceeded 50% of revenue in 2026. Infosys is walking away from uneconomic deals. [N] https://www.thestar.com.my/tech/tech-news/2026/08/21/ai-reshapes-india039s-it-services-sector-contracts-as-clients-demand-more-for-less
- **Read-through:** SIs now keep the margin from automating their own delivery, including discovery, documentation, testing and agent configuration. That is a buyer with a hard-dollar incentive and ACVs in the millions.
- **Verdict:** **STRONG** budget signal.

### 18. AI-native services roll-ups are buying delivery firms
- **Evidence:** General Catalyst earmarked $1.5B for AI roll-ups across accounting, legal, IT services and call centers, including Titan ($74M), Crescendo, Eudia and Accrual. [N] https://www.privateequitywire.co.uk/general-catalyst-backs-ai-driven-it-services-platform-titan-with-74m-investment/ ; [P] https://www.generalcatalyst.com/stories/the-future-of-services
- **Read-through:** Dozens of PE- and VC-backed roll-ups need a repeatable way to convert acquired firms' workflows into agents. Each has a strong incentive and money.
- **Verdict:** **MEDIUM**. There are few buyers, but each is high value. They tend to build in-house.

### 19. PSA vendors are pivoting to agentic delivery (direct validator and competitor)
- **Evidence:** Rocketlane raised a $60M Series C (Insight, Mar 2026), more than doubled revenue, has 750+ customers including Glean, Notion and Intercom, and cut delivery effort by up to 50%. Atlassian Ventures invested in Jul 2026. [N] https://siliconangle.com/2026/03/25/rocketlane-bags-60m-investors-accelerate-professional-services-automation-ai-agents/ ; [P] https://www.insightpartners.com/ideas/rocketlane-raises-60-million-series-c-to-redefine-professional-services-for-the-ai-era/
- **Verdict:** It validates Thesis A's budget and is its main competitor.

### 20. Chief AI Officer and AI adoption measurement
- **Evidence:** IBM reports 76% of firms have a CAIO, up from 26% a year earlier. [N] https://www.peoplematters.in/amp/news/ai-and-emerging-tech/76percent-of-firms-now-have-a-chief-ai-officer-up-from-26percent-in-a-year-ibm-49550. Larridin reports enterprise token spend up 13x in six months. [B] https://larridin.com/blog/enterprise-tools-measure-ai-roi. Worklytics sells AI adoption measurement. [B] https://www.worklytics.co/blog/introducing-worklytics-for-ai-adoption-measure-benchmark-and-accelerate-ai-impact-across-your-organization
- **Verdict:** **WEAK**. This is Round 1 territory (governance and spend), and Workday's ASOR and the model vendors absorb it. [N] https://www.constellationr.com/insights/news/workday-aims-be-system-record-ai-agents-digital-labor

### 21. GTM Engineer
- **Evidence:** Postings are up about 205% YoY. Only about 1,200 people hold the title, and 91% of companies employ one. [B] https://www.onfire.ai/blog/gtm-engineering-data ; https://www.herohunt.ai/blog/how-to-hire-gtm-engineer-2026/
- **Verdict:** **WEAK**. The population is tiny and Clay owns it.

### 22. Voice-agent testing
- **Evidence:** Coval raised a $28M Series A (Norwest). Competitors include Hamming, Roark and Cekura. [N] https://thenextweb.com/news/coval-28m-series-a-voice-ai-testing
- **Verdict:** **WEAK**. It is crowded.

---

## 2. Pattern

New money is flowing to **people who make agents work in a specific customer's environment**: FDEs, context engineers, agent success managers, SI AI practices and roll-ups. Their daily work is discovery interviews, shadowing users, writing SOPs and prompts, hand-building test cases, configuring integrations, watching failed runs and iterating. Three forces make this labor a cost center that someone now has a hard-dollar reason to automate: vendors' gross margins, SI fixed-price contracts, and roll-up EBITDA targets.

The tooling these people use is fragmented. It ranges from Scribe and Skan for capture, to Braintrust and LangSmith for evals, to Rocketlane for projects, to Google Docs for everything in between. No product owns the **deployment artifact chain**: observed work → spec/skill → eval suite → rollout acceptance.

---

## 3. Top 3 startup theses

### Thesis A (best): "Deployment OS for agent implementers"
**One sentence:** We cut the forward-deployed-engineering hours to put an AI agent into production by 5x. We turn customer discovery, observed work and historical tickets into a versioned agent spec, Agent Skills, and an acceptance eval suite that the customer signs off on.

- **Buyer:** VP of Deployment, VP of Professional Services or Head of FDE at AI-native app vendors. Second wave: AI-practice leaders at SIs on fixed-price contracts and at roll-ups.
- **Buyers × ACV:**
  - About 1,500 AI app vendors with deployment teams × $120K = $180M (**UNVERIFIED** count).
  - Top 100 SIs and boutiques × $1M = $100M.
  - About 50 roll-ups and labs' deployment arms × $500K = $25M.
  - About 3,000 enterprise AI centers of excellence × $150K = $450M.
  - Total near-term SAM is about $750M. A $1B+ outcome requires winning enterprise CoEs and pricing per deployment.
- **Why now:**
  - FDE postings are up about 8x and supply about 1.5x.
  - OpenAI ($4B Deployment Co) and Palantir (+149% US commercial) prove deployment velocity is the wedge.
  - SI pricing has flipped to fixed and outcome terms (TCS about 80%, Cognizant over 50%).
  - Agent Skills gives a standard output format.
- **Why incumbents can't:**
  - Scribe and Skan stop at maps and documents, not executable, tested agent artifacts.
  - Rocketlane is project management, not agent semantics or evals.
  - Model labs want lock-in, so their tools won't be cross-platform for SIs that serve many stacks.
  - Eval vendors start after the spec exists.
- **90-day pilot:** Pick one AI vendor (for example a Decagon-tier CX or legal-AI company) and run 3 live customer deployments side-by-side against the status quo. Measure FDE hours per go-live, days to production and eval pass-rate at launch. Success means a 40% or greater hours reduction.
- **Strongest kill risk:** Each well-funded AI vendor treats deployment as its moat and builds this in-house. Decagon and Sierra already have Agent Success teams and internal consoles, which leaves only the long tail and SIs. A second risk is that Rocketlane (Nitro) or Scribe extends into it within 12 months.
- **Verdict:** **MEDIUM-STRONG**. This is the only thesis directly riding the biggest new budget line.

### Thesis B: "Internal expert-data factory"
**One sentence:** Mercor for your own employees. We turn enterprise subject-matter experts' spare hours into golden eval sets, rubrics and RL tasks for each workflow, and score whether each agent is ready to go live.

- **Buyer:** CAIO or the head of the AI CoE, co-signed by the function owner (finance ops, legal ops, support).
- **Buyers × ACV:** About 4,000 enterprises over $1B revenue with agent programs × $150K = $600M. Expansion is per workflow.
- **Why now:**
  - Expert data is a $3B+ gross market at labs (Mercor about $2B, Handshake $1.1B).
  - Enterprises are fine-tuning and running RL on their own agents, with Snorkel selling them exactly this.
  - About 40% of AI time savings are lost to rework, which means output quality is unmeasured.
- **Why incumbents can't:** Mercor and Surge sell external contractors, while enterprise data is confidential and domain-specific. Databricks' SME UI is a feature, not an incentive and workflow system.
- **90-day pilot:** One function (for example AP exceptions or contract review), with 20 SMEs at 2 hours per week. Deliver a 500-case golden set plus a readiness score for the incumbent agent. Success means the buyer gates go-live on our score.
- **Strongest kill risk:** Snorkel ($3.5B, Expert DaaS), Invisible's enterprise pivot, Scale, and Databricks/Snowflake bundling. SMEs also won't make the time. The idea is absorbable, which is the Round 1 failure pattern.
- **Verdict:** **MEDIUM**.

### Thesis C: "SI delivery-margin engine"
**One sentence:** We give IT services firms and AI roll-ups on fixed-price contracts software that automates their own delivery work (discovery, documentation, test generation, agent configuration), so the AI-productivity savings become their margin rather than their client's discount.

- **Buyer:** COO or head of delivery at the top 100 SIs and BPOs, and operating partners at roll-ups.
- **Buyers × ACV:** About 200 SIs, BPOs and roll-ups × $750K (seat plus per-project pricing) = $150M base. Upside comes from per-engagement pricing on a delivery labor pool worth hundreds of billions of dollars.
- **Why now:** Outcome and fixed pricing crossed 50-80% at Cognizant and TCS in 2026. Infosys is walking from uneconomic deals. Cognizant is hand-staffing 1,000 context engineers.
- **Why incumbents can't:** SIs' internal platforms (myWizard, Cognizant Flowsource and similar) are bespoke and slow. Rocketlane targets SaaS onboarding teams, not large SI delivery.
- **90-day pilot:** One delivery tower at a mid-tier SI (for example a Salesforce/Agentforce practice, where Year-1 overruns run 3-5x). Measure delivery hours per agent go-live.
- **Strongest kill risk:** SIs are notoriously slow, procurement-heavy buyers that prefer to build or acquire. Big SIs also mean concentrated revenue. Thesis C may be better as Thesis A's second motion than as its own company.
- **Verdict:** **MEDIUM**.

---

## 4. Explicitly rejected

These were rejected because platforms absorb them or the market is crowded:
- Horizontal eval/observability (consolidating).
- CX AI QA.
- KB-gap tools.
- AI adoption and spend measurement (Round 1 repeat).
- Agent HR registry (Workday ASOR).
- GTM engineering tools (Clay).
- Voice-agent testing.
- Standalone process/task mining (Skan, Scribe, Mimica, Celonis).

## 5. Gaps and what to verify next

- **FDE headcount:** Count FDE and Agent Success headcount at the top 50 AI app vendors via LinkedIn. That gives Thesis A's real SAM.
- **Customer interviews:** Interview 10 deployment and FDE leads. Do they buy tools, or insist on building them? This is the key kill test.
- **Spend estimates:** Check Fleet's run-rate and the "$7.5-10M per FDE team" estimate. Both are **UNVERIFIED**.
- **Rocketlane Nitro:** Check whether Nitro already ships agent spec and eval generation.
