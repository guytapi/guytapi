# Round 32 — Companies E: vertical AI, agentic, AI-first operators

Scope: Ramp, Mercor, Surge AI, EvenUp, Shopify, Duolingo, Canva, Figma, Instacart, Uber, DoorDash.
Method: 20 WebSearch queries (snippets only; WebFetch not used). Dates: last 12–18 months where possible (today 2026-10-06).
Several companies here have more than 1,000 employees. They are included because their engineering blogs describe the internal AI platforms that smaller companies will need. Estimates are marked **[est]**. Sources are listed per company.

---

## 1. Ramp (fintech, AI-first operator)
1. **Changed:** Built the internal background coding agent "Inspect". Its v2 shipped Nov 2025. By May 2026 it authored about 75% of merged PRs, and it passed 1M sessions by Jul 2026. Ramp also built an internal AI suite: Glass (productivity), Ramp Research (Snowflake), Ramp CLI, and Dojo (a shared skills marketplace).
2. **Hiring:** "Software Engineer, Agent Developer Platform". "AI Operations Specialist | Agentic Workflows", whose goal is to deploy "dozens of AI-driven automations or copilots across non-engineering teams within 6–12 months" and measure them "via dashboards, QA checks". "AI Operations Manager, Agentic CX". "Agentic Operator, Growth Marketing". "AI Product Engineer".
3. **Internal platforms:** Inspect runs on Modal sandboxes. Each session gets a full, disposable VM with Postgres, Redis, Temporal, RabbitMQ, a VS Code server and VNC/Chromium for visual checks. A job refreshes repo filesystem snapshots about every 30 min. Inspect is wired into Sentry, Datadog, LaunchDarkly, Braintrust (evals), GitHub, Slack and Buildkite, and can query a read-only, sanitized replica of the production DB.
4. **Human ops still required:** Humans review and merge a large volume of agent-written PRs. A new role, the AI-ops enabler, builds internal agents for non-engineering teams, then QAs and monitors them. Someone has to curate the shared skills library (Dojo).
5. **Architecture beyond normal SaaS:** Per-session ephemeral copies of the full production stack. Agents get the same credentials an engineer has, against sanitized production data. Snapshot pre-warming.
6. **Scales linearly with:** agent sessions (sandbox compute), agent PRs (review load), internal workflows deployed (QA/monitoring load).
7. **Complaints:** none found in snippets. The risk is implicit: agents hold engineer-equivalent tool access.
8. **Built internally that others couldn't afford:** the full-context background-agent platform with sandbox snapshots, and an internal agent/skills marketplace.
9. **Tags:** `internal-agent-platform`, `agent-sandbox-environments`, `generated-code-review`, `agent-permissions-governance`, `internal-ai-enablement-ops`, `eval-pipelines`
   - *Pain (generated-code-review):* PEOPLE COST about 0.5–1 FTE of senior review time per 20 engineers once agents write more than 50% of PRs **[est]**. FREQUENCY: every PR. SCALING LAW: linear in agent PR volume, and agent PR volume grows faster than headcount. CURRENT SOLUTION: human reviewers plus CI.
   - *Pain (agent-sandbox-environments):* INFRA COST $10k–100k+/mo of sandbox compute at 1M sessions **[est]**. SCALING: linear in sessions. CURRENT SOLUTION: built in-house on Modal.

Sources: [InfoQ Ramp coding agent platform](https://infoq.com/news/2026/01/ramp-coding-agent-platform/), [Modal: How Ramp built Inspect](https://modal.com/blog/how-ramp-built-a-full-context-background-coding-agent-on-modal), [Port software factories: Ramp](https://software-factories.port.io/ramp), [dbt Summit: Ramp internal AI stack](https://www.getdbt.com/dbt-summit/sessions/ramps-internal-ai-stack-agents-sandboxes-and-an-ai-first-bi-tool), [Ramp AI Ops Specialist job](https://jobs.generalcatalyst.com/companies/ramp-2/jobs/57190561-ai-operations-specialist-agentic-workflows), [Agent Developer Platform job](https://jobs.generalcatalyst.com/companies/ramp-2/jobs/67702164-software-engineer-agent-developer-platform), [AI Ops Manager Agentic CX](https://www.builtinnyc.com/job/ai-operations-manager-agentic-cx/9344653)

---

## 2. Mercor (expert-labor marketplace for AI labs)
1. **Changed:** Run-rate gross revenue went from about $75M (Feb 2025) to about $840M (Oct 2025) to about $2B (Jun 2026). Mercor works with OpenAI, Anthropic and 6 of the "Mag 7".
2. **Hiring:** a network of 30k+ experts paid about $95/hr on average to test and score models, write rubrics and build RL environments. The internal FTE base is small relative to the contractor base **[est]**.
3. **Internal platforms:** an AI interviewer and vetting platform, plus project and rubric tooling. No detailed engineering blog was found.
4. **Human ops still required:** Every model evaluation is produced by humans. Ops staff set up and wind down projects, onboard and offboard thousands of contractors at once ("Project L" grew past 11k contractors, followed by mass offboarding in May 2026), set pay rates, and run quality review of the expert work.
5. **Architecture beyond normal SaaS:** expert matching and vetting at scale, rubric versioning, QA of graders ("who grades the graders"), and per-lab data isolation.
6. **Scales linearly with:** lab post-training budgets and the number of eval/rubric tasks. Contractor hours are the unit of revenue.
7. **Complaints:** Nov 2025: a project was cancelled and workers were re-offered work at lower hourly rates (Forbes, BI). Reddit calls "Project L" a scam. Contractors churn heavily.
8. **Built internally:** AI-run interviewing and vetting at a volume of tens of thousands of experts.
9. **Tags:** `data-labeling-ops`, `expert-rubric-authoring`, `human-review-queues`, `annotator-quality-control`, `eval-pipelines`
   - *Pain:* PEOPLE COST is the product itself. The labs' spend implies about $2B/yr of expert hours bought by about 10 labs **[est from run rate]**. FREQUENCY: continuous. SCALING LAW: linear in eval/RL task volume, which grows with each model generation. CURRENT SOLUTION: managed expert marketplaces (Mercor, Surge, Scale).

Sources: [Contrary Research: Mercor](https://research.contrary.com/report/mercor), [Sacra: Mercor](https://sacra.com/c/mercor/), [Big Think: rise of Mercor](https://bigthink.com/business/inside-the-meteoric-rise-of-mercor/), [Runtimewire: $2B run rate](https://runtimewire.com/article/as-amazon-lets-mechanical-turk-fade-mercor-hits-a-2-billion-gross-run-rate), [AOL/BI: contractor pay cut](https://www.aol.com/articles/worlds-youngest-self-made-billionaires-204308445.html), [Project L offboarding](https://breakingeven.online/blog/mercor-project-l-mass-offboarding-may-2026)

---

## 3. Surge AI (RLHF / data annotation)
1. **Changed:** $1.2B revenue in 2024, driven by about 12 frontier labs. First external raise in Jul 2025, seeking up to $1B at a valuation above $15B. Profitable and bootstrapped since 2021.
2. **Hiring:** about 130 FTEs managing about 50k expert contractors, paid 30–40¢ per working minute.
3. **Internal platforms:** an annotation platform with API access plus managed services for RLHF and RL environments. Quality control is the core of the platform **[est; no eng blog found]**.
4. **Human ops still required:** the whole product is human judgment (preference ranking, red-teaming, RL environment building). Internally, QA of annotators and routing of tasks.
5. **Architecture beyond normal SaaS:** worker quality scoring, gold-task injection, spam and AI-cheat detection among annotators **[est]**.
6. **Scales linearly with:** frontier-lab post-training spend, and the number of tasks per model release.
7. **Complaints:** none specific in snippets. Industry-wide issues are annotator pay opacity and concentration on about 12 customers.
8. **Built internally:** a quality-control layer that lets 130 FTEs manage 50k contractors (about 385 contractors per FTE).
9. **Tags:** `data-labeling-ops`, `annotator-quality-control`, `human-review-queues`, `eval-pipelines`
   - *Pain:* SCALING LAW: linear in lab spend. CURRENT SOLUTION: outsourced to Surge, Mercor or Scale. Large enterprises increasingly need the same thing internally for their own evals (see Canva's human-labelling tooling, Shopify's expert labels, Instacart's human evaluation UI).

Sources: [Wikipedia: Surge AI](https://en.wikipedia.org/wiki/Surge_AI), [Sacra: Surge AI](https://sacra.com/c/surge-ai)

---

## 4. EvenUp (vertical AI, personal-injury law)
1. **Changed:** Valuation passed $1B (Oct 2024, $135M Series D) and then $2B (Oct 2025). Output is "thousands of demands and medical chronologies every week".
2. **Hiring:** repeated "Legal Ops Associate" and "Legal Ops Reviewer" postings (US, Canada, Singapore, remote). The in-house team has 100+ lawyers, paralegals and medical professionals.
3. **Internal platforms:** the Piai model, trained on hundreds of thousands of PI cases. EvenUp itself describes a combined AI-plus-human review pipeline.
4. **Human ops still required:** Associates draft from the AI output. Reviewers check every demand against drafting standards. 72% of demand content starts from an AI draft, up from 63% in Jun 2023. Employees spend 20% less time writing. Eight former employees told BI that humans did much of the work. They reported missed injuries, hallucinated conditions and wrongly recorded doctor visits, and said managers once told staff not to use the AI.
5. **Architecture beyond normal SaaS:** a two-layer human QA queue (drafter, then reviewer) on every generated document. Medical-record extraction with traceability back to the source.
6. **Scales linearly with:** cases processed. Reviewer headcount grows with demand volume. EvenUp markets "AI-only demands without human review" as "borderline malpractice".
7. **Complaints:** the BI exposé (AI overpromised; humans did the work), and OpenTools coverage of it.
8. **Built internally:** a domain-trained model plus a staffed expert review layer of 100+ professionals.
9. **Tags:** `human-review-queues`, `hallucination-verification`, `source-grounding-traceability`, `expert-rubric-authoring`
   - *Pain:* PEOPLE COST is 100+ experts. At an assumed loaded cost of about $80–150k each, that is roughly $8–15M/yr **[est]**. FREQUENCY: every document, thousands per week. SCALING LAW: linear in cases, with only a slow fall in human minutes per document (20% drop per year). CURRENT SOLUTION: in-house reviewer queues following drafting standards.

Sources: [EvenUp: AI & human review](https://evenuplaw.com/blog/leveraging-ai-human-review-in-demand-letters-the-evenup-difference), [BI via businessinsider.nl](https://businessinsider.nl/evenups-valuation-soared-past-1-billion-on-the-potential-of-its-ai-the-startup-has-relied-on-humans-to-do-much-of-the-work-former-employees-say/), [EvenUp vs Supio](https://www.evenuplaw.com/demo/evenup-vs-supio), [Legal Ops Associate job](https://builtinottawa.com/job/legal-ops-associate-canada-remote/4454405), [BGov: $2B valuation](https://news.bgov.com/esg/ai-legal-tech-evenup-raises-150-million-at-2-billion-valuation), [OpenTools](https://opentools.ai/news/evenups-ai-overpromise-legal-tech-startup-faces-scrutiny)

---

## 5. Shopify (AI-first mandate)
1. **Changed:** Lütke's April 2025 memo made AI use mandatory. Teams must show AI can't do a job before getting new headcount, and AI use is part of performance reviews. Sidekick grew into an agentic merchant assistant.
2. **Hiring:** constrained by the memo. No specific AI-platform job posts were found in the snippets.
3. **Internal platforms:** an internal LLM proxy, "chat.shopify.io", maintained "for years". It "makes all models in the world accessible via openai standard protocol and does the metering and failover" and "does filtering centrally". For Sidekick, Shopify built an evaluation framework: ground truth labeled by at least 3 product experts, agreement measured with Cohen's Kappa, Kendall Tau and Pearson, an LLM judge calibrated to humans (agreement rose from 0.02 to 0.61 against an expert-to-expert ceiling of 0.69), and a merchant simulator. Training uses GRPO (ICML 2025 talk).
4. **Human ops still required:** experts label ground-truth conversations to calibrate judges. Recalibration is presumably needed per model or prompt change **[est]**.
5. **Architecture beyond normal SaaS:** central metering, failover and filtering of every model call; judge-versus-human agreement statistics; synthetic user simulation.
6. **Scales linearly with:** agent tool count (Shopify reported tool sprawl as Sidekick grew), and eval sets per skill.
7. **Complaints:** the memo drew backlash about mandatory AI and hiring freezes.
8. **Built internally:** the LLM gateway, a calibrated LLM-judge pipeline, and a simulated-merchant eval harness.
9. **Tags:** `internal-llm-gateway`, `eval-pipelines`, `llm-judge-calibration`, `human-review-queues`, `agent-simulation-testing`, `internal-ai-enablement-ops`
   - *Pain (llm-judge-calibration):* PEOPLE COST is 3+ experts labeling each criterion set, recurring for each new skill or model **[est 0.5–2 FTE ongoing]**. FREQUENCY: every model upgrade and new tool. CURRENT SOLUTION: built in-house.

Sources: [Shopify Eng: Building production-ready agentic systems](https://shopify.engineering/building-production-ready-agentic-systems), [ICML 2025 talk](https://icml.cc/Expo/Conferences/2025/talkpanel/46781), [PPC Land: mandatory AI memo + proxy](https://ppc.land/shopifys-mandatory-ai-usage-establishes-new-workplace-norm/), [Pragmatic Engineer: Farhan Thawar](https://newsletter.pragmaticengineer.com/p/how-ai-is-changing-software-engineering), [First Round: Shopify](https://www.firstround.com/ai/shopify)

---

## 6. Duolingo (AI-first)
1. **Changed:** April 2025 "AI-first" memo: stop using contractors for work AI can do, such as content and translation, and hire only if work can't be automated. Launched about 148 AI-generated courses. DuoRadio went from 300 to 15,000+ episodes in under 6 months.
2. **Hiring:** contractors cut. Learning Designers were kept as reviewers.
3. **Internal platforms:** an LLM lesson-generation tool (prompts combining fixed rules and variable parameters), an LLM-as-evaluator layer with criteria designed by experts (about 20 evaluations per trace), and an LLM+TTS audio pipeline.
4. **Human ops still required:** Learning Designers review all generated content before it ships, catching grammar, unnatural phrasing and pedagogy issues. Experts keep refining the eval criteria.
5. **Architecture beyond normal SaaS:** multi-layer eval cascades per generated item; generation at a scale of tens of thousands of items across 25+ languages.
6. **Scales linearly with:** generated content items multiplied by languages. The human review gate is the bottleneck.
7. **Complaints:** users and veterans say AI content is lower quality and inaccurate ("joined the dark side"), and there was backlash about contractor layoffs.
8. **Built internally:** a multi-layer LLM evaluation pipeline for content, and generation tooling for subject experts.
9. **Tags:** `human-review-queues`, `eval-pipelines`, `generated-content-qa`, `llm-judge-calibration`, `contractor-to-reviewer-shift`
   - *Pain:* PEOPLE COST: the reviewer pool replaces the contractor pool, but review stays mandatory **[est tens of FTE]**. SCALING LAW: linear in items × languages unless eval layers auto-pass most items. CURRENT SOLUTION: in-house LLM eval layers plus designer review.

Sources: [Computing: Duolingo AI-first](https://www.computing.co.uk/news/2025/ai/duolingo-goes-ai-first-as-it-phases-out-human-contractors), [Fortune](https://www.fortune.com/article/duolingo-ceo-says-getting-rid-of-contract-employees-replacing-them-with-ai), [The74: user backlash](https://www.the74million.org/article/as-duolingo-turns-to-ai-some-users-say-language-app-has-joined-the-dark-side/), [ZenML: Duolingo lesson generation](https://www.zenml.io/llmops-database/ai-powered-lesson-generation-system-for-language-learning), [ZenML: multi-layered eval pipeline](https://www.zenml.io/llmops-database/multi-layered-llm-evaluation-pipeline-for-production-content-generation), [ZenML: DuoRadio](https://zenml.io/llmops-database/scaling-audio-content-generation-with-llms-and-tts-for-language-learning), [AI Engineer talk: better evals](https://ai.engineer/talks/spvXj9tnWAQ-engineering-better-evals-scalable-llm-evaluation)

---

## 7. Canva
1. **Changed:** Magic Studio features (Magic Switch, Magic Write) and an expanding AI suite. The AI Platform Group became a formal organization.
2. **Hiring:** "Engineering Manager (ML) – Evaluation Platform", and "Research Engineer – Evaluations" (multiple postings, Senior and IC).
3. **Internal platforms:** an Evaluation Platform team owning "test-like evals integrated into developer workflows, the Arena comparative evaluation service, monitoring evals sampled from production traffic, and human labelling tooling". A Magic Switch eval framework with rule-based and LLM evaluators (information preservation, intent, tone, format). An Anyscale/Ray AI platform: 12x faster model evaluation, 50% lower cloud cost. Synthetic data for privacy-preserving search eval.
4. **Human ops still required:** human labelling to anchor evals; reviewing Arena side-by-side comparisons.
5. **Architecture beyond normal SaaS:** evals as CI, sampling production traffic for evals, privacy-safe synthetic eval data.
6. **Scales linearly with:** number of AI features × model versions (each needs eval suites).
7. **Complaints:** none found.
8. **Built internally:** a whole eval platform team (EM plus research engineers) — it shows eval infrastructure has become a staffed internal product.
9. **Tags:** `eval-pipelines`, `human-labeling-tooling`, `production-traffic-eval-sampling`, `regression-on-model-upgrade`, `inference-cost-routing`
   - *Pain:* PEOPLE COST: one dedicated team of about 5–10 FTE **[est]**. FREQUENCY: every PR touching AI, plus continuous monitoring. CURRENT SOLUTION: built in-house.

Sources: [Canva EM Evaluation Platform job](https://jobs.blackbird.vc/companies/canva/jobs/91142198-engineering-manager-ml-evaluation-platform), [Research Engineer Evaluations](https://jobs.generalcatalyst.com/companies/canva/jobs/55332830-research-engineer-evaluations), [ZenML: Canva eval framework](https://www.zenml.io/llmops-database/systematic-llm-evaluation-framework-for-content-generation), [Anyscale case study](https://anyscale.com/resources/case-study/how-canva-built-a-modern-ai-platform-using-anyscale), [ZenML: synthetic search eval](https://www.zenml.io/llmops-database/synthetic-data-generation-for-privacy-preserving-search-evaluation)

---

## 8. Figma
1. **Changed:** Config 2025 launched Figma Make (prompt to app), Sites, Buzz and Draw. A Figma Design Agent followed.
2. **Hiring:** repeated "Software Engineer – AI Platforms" postings. Responsibilities: "evaluation frameworks for design generation quality used across every Figma AI feature", "sandboxes, harnesses, and tools leveraged by the agents that power Figma Make and the Figma Design Agent", and context and search tools for agents.
3. **Internal platforms:** shared eval frameworks, agent sandboxes and harnesses, and context retrieval for agents.
4. **Human ops still required:** human-centered evaluation. Head of Product AI (Kossnick) says capabilities are "only validated through actual testing" with people (First Round).
5. **Architecture beyond normal SaaS:** sandboxed execution of generated apps; subjective quality evals for visual and design output.
6. **Scales linearly with:** generated apps and sites (sandbox compute), and AI features (eval suites).
7. **Complaints:** none specific in snippets.
8. **Built internally:** a shared agent harness and sandbox platform, and design-quality evals.
9. **Tags:** `eval-pipelines`, `agent-sandbox-environments`, `internal-agent-platform`, `agent-context-retrieval`, `human-review-queues`

Sources: [First Round: Figma AI eval process](https://review.firstround.com/figma-ai-eval-process/), [Figma SWE AI Platforms job](https://www.indexventures.com/startup-jobs/figma/software-engineer-ai-platforms/), [Working Nomads posting](https://www.workingnomads.com/jobs/software-engineer-ai-platforms-figma-1898900)

---

## 9. Instacart
1. **Changed:** LLMs used across catalog cleanup, attribute enrichment, perishables routing and search relevance, with millions of LLM calls per job.
2. **Hiring:** "Senior SWE II (ML/AI Platform)", "EM, Catalog Enrichment".
3. **Internal platforms:** an **AI Gateway** (a central abstraction over multiple LLM providers), a **Cost Tracker** (spend per job and per team), **Maple** (a batch LLM service handling batching, encoding, file management, retries and cost tracking, saving up to 50% versus real-time calls), and **PARSE** (self-serve multimodal attribute extraction with a human evaluation interface for gold labels, plus routing of low-confidence outputs to human review). PARSE cut attribute development time from weeks to days. Human judges rate 85% of extractions correct (Qwen3 study).
4. **Human ops still required:** auditors label gold values; low-confidence extractions go to human review queues.
5. **Architecture beyond normal SaaS:** batch inference orchestration at millions of prompts, per-team LLM cost attribution, confidence-gated human fallback.
6. **Scales linearly with:** catalog SKUs × attributes × retailers. The human review queue scales with the low-confidence share.
7. **Complaints:** none found.
8. **Built internally:** gateway, batch platform, cost tracker and extraction platform. The same stack shows up at Uber and DoorDash.
9. **Tags:** `internal-llm-gateway`, `inference-cost-routing`, `llm-cost-attribution`, `batch-llm-processing`, `human-review-queues`, `confidence-based-escalation`, `eval-pipelines`
   - *Pain (batch-llm-processing / cost):* INFRA COST: 50% savings on batch jobs implies a large LLM line item **[est $M/yr]**. FREQUENCY: daily catalog jobs. CURRENT SOLUTION: built in-house (Maple).

Sources: [Instacart Tech: Maple](https://tech.instacart.com/simplifying-large-scale-llm-processing-across-instacart-with-maple-63df4508d5be), [Instacart Tech: PARSE](https://tech.instacart.com/multi-modal-catalog-attribute-extraction-platform-at-instacart-b9228754a527), [arXiv: parallel decoding attribute extraction](https://arxiv.org/pdf/2609.09716), [Instacart ML/AI Platform job](https://scoutify.com/companies/instacart/jobs/1214781/)

---

## 10. Uber (Michelangelo / GenAI platform)
1. **Changed:** 60+ LLM use cases, which led to teams integrating models in disparate ways and duplicating effort. Agentic developer tools launched: uReview (Aug 2025), AutoCover, and Genie.
2. **Hiring:** none captured in snippets. Michelangelo is a large standing platform organization.
3. **Internal platforms:**
   - **GenAI Gateway:** one interface to OpenAI, Vertex and Uber-hosted models, with authn/z, metrics and alerting, audit logs for cost attribution, security audit, quality eval, and PII redaction. It includes a standardized review process run by Engineering Security.
   - **Prompt Engineering Toolkit:** templates, version control, batch offline generation, hallucination checks, a standard eval framework, and a safety policy.
   - **LLM training/fine-tuning stack.**
   - **uReview:** AI code review with a Commenter and a Fixer. Its motivation: "reviewers are overloaded with the increasing volume of code from AI-assisted code development"; its main challenge is false positives.
   - **AutoCover:** test generation, credited with 21k dev hours saved.
   - **Genie:** an on-call copilot for about 45k Slack questions/month, saving 13k eng hours. Agentic RAG reduced incorrect advice by 60%.
4. **Human ops still required:** a security review per LLM use case before onboarding; human reviewers triaging AI review comments; owners maintaining on-call channel knowledge.
5. **Architecture beyond normal SaaS:** central routing, auditing and redaction of every LLM call; prompt registry; AI-reviewing-AI-code loops.
6. **Scales linearly with:** LLM use cases (each onboarding), generated code volume (review load), on-call questions.
7. **Complaints:** internal: AI code review false positives and noise erode trust.
8. **Built internally:** gateway, prompt toolkit, code-review agent and test-generation agent — the full "internal AI platform" reference stack.
9. **Tags:** `internal-llm-gateway`, `llm-cost-attribution`, `ai-use-case-security-review`, `prompt-management-versioning`, `eval-pipelines`, `generated-code-review`, `ai-review-false-positives`, `internal-support-copilot`
   - *Pain (generated-code-review):* PEOPLE COST: reviewer hours are the bottleneck. AutoCover's 21k hours saved gives a sense of the magnitude. SCALING LAW: linear-to-superlinear in AI-written code volume. CURRENT SOLUTION: built in-house (uReview).
   - *Pain (ai-use-case-security-review):* FREQUENCY: each of 60+ use cases. PEOPLE COST: security engineers' time per review **[est 1–3 days each]**. CURRENT SOLUTION: a manual standardized review.

Sources: [Uber: GenAI Gateway](https://www.uber.com/blog/genai-gateway), [Uber: Prompt Engineering Toolkit](https://uber.com/blog/introducing-the-prompt-engineering-toolkit), [Uber: LLM training](https://www.uber.com/blog/open-source-and-in-house-how-uber-optimizes-llm-training), [Uber: uReview](https://www.uber.com/blog/ureview/), [Uber: Genie](https://uber.com/en-IN/blog/genie-ubers-gen-ai-on-call-copilot/), [ZenML: AutoCover/dev tools](https://www.zenml.io/llmops-database/ai-powered-developer-tools-for-code-quality-and-test-generation), [Biweekly Eng ep. 33](https://biweekly-engineering.beehiiv.com/p/generative-ai-gateway-uber-biweekly-engineering-episode-33)

---

## 11. DoorDash
1. **Changed:** The Ask DoorDash agent platform (Part 4 blog, Jul 2026) passed 2M+ conversations. It launched Restaurant and Grocery support in 2 months, and adding a third domain agent (Reservations) took 1 week, about 10x faster than the first ones. A Dasher support RAG bot is in production. "AI juries" judge millions of menus. A cloud agent platform handles engineering tasks.
2. **Hiring:** "Senior SWE, ML Infrastructure – Generative AI", and a QCon 2026 talk, "Building GenAI Platform at DoorDash".
3. **Internal platforms:** an **LLM Gateway** (routing, observability, fallback, rate limiting across providers with different quota models, cost attribution). Agent platform: Gateway, then Orchestrator, then domain agents, with shared session state, memory, artifacts, tracing, **evaluation infrastructure** and **rollout controls**. Dasher support has an **LLM Guardrail** (real-time validation; hallucinations down 90%, severe compliance issues down 99%), an **LLM Judge**, and a quality improvement pipeline. LLM-as-judge is used for search evaluation.
4. **Human ops still required:** "manually reviewed thousands of chat transcripts" to define quality categories. Guardrail failures "default to human agents", so a human escalation queue remains. Domain teams own their eval criteria.
5. **Architecture beyond normal SaaS:** real-time guardrail in the response path, multi-provider quota management, staged agent rollout, an LLM jury for catalog data.
6. **Scales linearly with:** conversations (guardrail and judge calls), domain agents (eval suites), menus and SKUs (judge calls).
7. **Complaints:** none specific. The platform blog states its motivation: domain teams were rebuilding the underlying systems.
8. **Built internally:** a multi-domain agent platform with shared evals and rollout, an LLM gateway, and a guardrail plus judge stack.
9. **Tags:** `internal-llm-gateway`, `internal-agent-platform`, `llm-guardrails-runtime`, `eval-pipelines`, `human-review-queues`, `confidence-based-escalation`, `agent-observability`, `agent-rollout-controls`, `llm-cost-attribution`
   - *Pain (human escalation + transcript review):* PEOPLE COST: reviewing thousands of transcripts per iteration **[est 1–3 FTE ongoing QA]**. FREQUENCY: continuous. SCALING: linear in conversations × failure rate. CURRENT SOLUTION: in-house judge and guardrail plus human support agents.

Sources: [ZenML: Dasher RAG with guardrails](https://www.zenml.io/llmops-database/rag-based-dasher-support-automation-with-llm-guardrails-and-quality-monitoring), [ZenML: multi-domain agent platform](https://www.zenml.io/llmops-database/building-a-multi-domain-agent-platform-with-shared-infrastructure-and-specialized-agents), [QCon: Building GenAI Platform at DoorDash](https://boston.qcon.ai/presentation/boston2026/building-genai-platform-doordash), [WebProNews: AI juries for menus](https://www.webpronews.com/doordash-turns-ai-juries-loose-on-millions-of-menus-to-tame-chaotic-food-data/), [ZenML: search eval with LLM judge](https://www.zenml.io/llmops-database/llm-powered-search-evaluation-system-for-automated-result-quality-assessment), [ZenML: cloud agent platform](https://www.zenml.io/llmops-database/cloud-based-agent-platform-for-automated-engineering-tasks), [DoorDash GenAI infra job](https://startup.jobs/senior-software-engineer-machine-learning-infrastructure-generative-ai-doordash-usa-8671012)

---

## Cross-company patterns: "we deployed AI, but now humans must..."
- **...review the code agents write.** Ramp: about 75% of PRs are agent-written. Uber's uReview exists because "reviewers are overloaded" by AI-assisted code.
- **...review every generated document or content item.** EvenUp: 100+ experts and two review layers. Duolingo: Learning Designers review everything. Instacart: low-confidence outputs go to humans. DoorDash: guardrail failures go to human agents.
- **...label ground truth to calibrate the LLM judge.** Shopify: 3+ experts, kappa statistics. Canva: human labelling tooling. Instacart: gold-label UI. DoorDash: thousands of transcripts.
- **...security-review each new LLM use case.** Uber's Engineering Security standardized review. Shopify's central filtering.
- **...enable and QA the internal agents non-engineers build.** Ramp's AI Ops Specialist role; Shopify's memo making AI use a performance criterion.
- **Independently rebuilt platforms:** an LLM gateway (Uber, Instacart, DoorDash, Shopify), eval platforms (Canva, Shopify, DoorDash, Duolingo, Figma, Uber, Instacart), agent platforms and sandboxes (Ramp, DoorDash, Figma).

## Summary table

| Pain tag | Companies | Built internally | Evidence strength |
|---|---|---|---|
| eval-pipelines | Canva, Shopify, DoorDash, Duolingo, Figma, Uber, Instacart, Ramp (Braintrust), Mercor/Surge (sell the human side) | Canva, Shopify, DoorDash, Duolingo, Figma, Uber, Instacart | **Strong** (eng blogs plus dedicated team job posts) |
| human-review-queues | EvenUp, Duolingo, Instacart, DoorDash, Shopify, Figma, Mercor, Surge | EvenUp, Duolingo, Instacart, DoorDash | **Strong** (BI exposé, company blogs, job posts) |
| internal-llm-gateway | Uber, Instacart, DoorDash, Shopify | All 4 | **Strong** (eng blogs plus CEO statement) |
| llm-cost-attribution | Uber, Instacart, DoorDash, Shopify (metering) | All 4 | Strong |
| internal-agent-platform | Ramp, DoorDash, Figma, Uber (dev agents) | All 4 | Strong |
| generated-code-review | Ramp, Uber | Uber (uReview); Ramp (human review) | Medium-strong (2 companies, explicit motivation) |
| agent-sandbox-environments | Ramp, Figma | Both | Medium |
| llm-judge-calibration | Shopify, Duolingo, DoorDash, Canva | All 4 | Strong (Shopify gives quantitative detail) |
| human-labeling-tooling | Canva, Instacart, Shopify | All 3 | Medium |
| data-labeling-ops / annotator-quality-control | Mercor, Surge (vendors); Canva, Shopify, Instacart (internal demand) | Mercor, Surge (as product) | Strong (revenue figures) |
| expert-rubric-authoring | Mercor, EvenUp, Shopify, Duolingo | EvenUp, Shopify, Duolingo | Medium |
| confidence-based-escalation | Instacart, DoorDash, EvenUp | All 3 | Medium |
| llm-guardrails-runtime | DoorDash, Shopify (central filter), Uber (PII redaction) | All 3 | Medium-strong |
| inference-cost-routing / batch-llm-processing | Instacart, Canva, Uber | All 3 | Medium |
| internal-ai-enablement-ops | Ramp, Shopify | Ramp (dedicated roles) | Medium (job posts) |
| prompt-management-versioning | Uber, Instacart (PARSE), Duolingo | All 3 | Medium |
| ai-use-case-security-review / agent-permissions-governance | Uber, Shopify, Ramp | Uber, Shopify | Medium |
| agent-observability / agent-rollout-controls | DoorDash, Uber, Ramp | DoorDash, Uber | Medium |
| regression-on-model-upgrade | Canva, Shopify (implied by recalibration) | Canva | Weak-medium (inferred) |
| hallucination-verification / source-grounding-traceability | EvenUp, DoorDash, Uber (Genie) | All 3 | Medium |
| agent-simulation-testing | Shopify | Shopify | Weak (1 company) |
| contractor-to-reviewer-shift | Duolingo, EvenUp | Both | Medium |
