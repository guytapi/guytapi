# Round 32: Group D, security / devtools / B2B SaaS that went AI-first

Companies: Wiz, Vanta, Semgrep, Snyk, Linear, PostHog, Sentry, Retool, Notion, Zapier, Airtable.
Method: 20 WebSearch queries, read from snippets only (no WebFetch). Covers roughly 2025-04 to 2026-10.
`[E]` = my estimate, not sourced. `[S#]` = numbered source at the end.
I did not search for startups solving these pains; vendor names appear only where the companies themselves named them.

---

## 1. Notion
1. **Changed:** AI was bundled into Business/Enterprise at $20/seat (the $8–10 add-on was removed, effective 2025-08-13). Notion Agent, AI Meeting Notes, Enterprise Search and Deep Research shipped. Custom Agents/Workers are metered at $10 per 1k credits [S2]. Notion AI serves 100M+ users [S1].
2. **Hiring:** "Model Behavior Engineer". It is a non-coding role that owns context engineering, eval datasets, and benchmarking OpenAI, Anthropic and Google models on quality, latency and cost for each launch [S3]. "AI Data Specialist (contract)" does annotation and labeling [S3]. "Software Engineer, AI Dev Velocity" [S1].
3. **Internal platforms:** an eval framework that keeps about 70 AI engineers aligned. New frontier models reach production in under a day. Custom LLM-as-judge scorers are written per feature [S1].
4. **Human ops:** the team says it spends "10% prompting, 90% evaluating, improving evals and inspecting usage" [S1]. Data specialists hand-build targeted datasets. Every model release triggers a re-benchmark.
5. **New architecture need:** multi-provider routing with per-feature model choice, a model-swap path measured in hours, and credit metering for agent runs.
6. **Scales linearly with:** AI features × model releases (each pair needs an eval pass). Agent runs drive inference cost, which is why the credit system exists.
7. **Complaints:** forced bundling raised prices (pricing-blog coverage [S2]). AI cost moved into seat price, so margin now depends on how efficient inference is.
8. **Built internally:** an eval org with a dedicated non-engineer job family (model behavior) and contract labelers.
9. **Tags:** eval-pipelines, regression-on-model-upgrade, model-selection-benchmarking, eval-dataset-curation, inference-cost-routing, ai-usage-metering
- **Economics (regression-on-model-upgrade):** PEOPLE: about 70 AI engineers spend about 90% of their time on eval/observability. That is a mix of product work and eval upkeep [E: 5–10 FTE-equivalent goes purely to eval upkeep]. INFRA: judge-model tokens per run [E: $10k–50k/mo]. FREQUENCY: each frontier model release, roughly 1–2/month across 3 providers. SCALING: features × models × providers. CURRENT: an external eval/observability SaaS (Braintrust) plus in-house scorers and human labelers [S1].

## 2. Vanta
1. **Changed:** an AI-first GRC push. AI questionnaire automation and a Trust Center Q&A bot let buyers ask questions that Vanta AI answers [S5]. Applied-AI agents work across compliance workflows.
2. **Hiring:** repeated "Software Engineer / Senior SWE, AI Product" postings, in Boston and Canada among others. They are required to "instrument evaluations, guardrails, and monitoring, and review customer usage" [S4].
3. **Internal platforms:** the AI Engineer talk "Why building eval platforms is hard" [S4]. It describes versioned, actively maintained eval datasets, LLM-as-judge pipelines *calibrated with GRC subject-matter experts*, repeatable experiment loops, and feedback from explicit and implicit user signals [S4]. Quote: "invest in the eval harness, because the model is going to be obsolete in a quarter."
4. **Human ops:** GRC SMEs label and calibrate judges by hand. Security teams still review and approve every AI-drafted questionnaire answer (human-in-the-loop by design [S5]). Vanta's survey names staffing (33%) and manual processes (32%) as the top blockers to proving security [S5].
5. **New architecture need:** answers must be grounded in an evidence corpus, with citations and an audit trail. AI answers are compliance claims, so a wrong one is a liability.
6. **Scales linearly with:** inbound security questionnaires × number of questions. AI-specific questions are now a growing section [E]. It also scales with frameworks × controls.
7. **Complaints:** questionnaire fatigue is industry-wide. No specific Vanta complaints were found.
8. **Built internally:** an SME-calibrated judge pipeline, i.e. domain experts acting as eval labelers.
9. **Tags:** eval-pipelines, eval-dataset-curation, judge-calibration-sme, ai-security-questionnaires, human-review-queue
- **Economics (ai-security-questionnaires):** PEOPLE: a typical vendor security team spends [E] 0.5–2 FTE on questionnaires at a mid-size SaaS, and AI-governance sections add [E] 20–30%. FREQUENCY: per enterprise deal, [E] 10–50 per month. SCALING: enterprise deals × AI features shipped. CURRENT: Vanta and peer tools draft answers, then a human approves them.

## 3. Semgrep
1. **Changed:** Assistant autotriage handles about 60% of new SAST findings. Customers agree with it 96% of the time [S6]. Detection is now LLM plus RAG over code context.
2. **Hiring:** no specific posts were found in the snippets.
3. **Internal platforms:** a benchmark harness that compares Assistant verdicts with Semgrep's security research team, plus continuous re-alignment [S6]. A customer-facing metrics page tracks agreement rate [S6].
4. **Human ops:** security researchers label findings to make ground truth. Customers confirm or reject verdicts, which feeds the 96% number. The remaining 40% of findings still go to a human.
5. **New architecture need:** an LLM verdict on every finding, retrieval of code context per finding, and an agreement metric the customer can see as a trust signal.
6. **Scales linearly with:** findings, which grow with lines of code, and AI-generated code grows LOC faster [E]. Each finding costs one LLM call.
7. **Complaints:** the pain they address is that more than half of SAST findings are false positives [S6].
8. **Built internally:** an expert-labeled eval set plus a production agreement-tracking loop.
9. **Tags:** eval-pipelines, eval-dataset-curation, ai-triage-of-findings, generated-code-review, human-review-queue, ai-trust-metrics
- **Economics:** PEOPLE: AppSec triage per customer [E] 0.5–1 FTE before Assistant. Semgrep internally runs a research team for labels [E: 3–8 people]. INFRA: LLM call per finding [E] $0.01–0.10. FREQUENCY: continuous, per scan. SCALING: LOC × rules. CURRENT: built in-house.

## 4. Snyk
1. **Changed:** DeepCode AI is a hybrid of symbolic and generative AI. Agent Fix re-scans each generated fix with the symbolic engine before showing it [S7]. Snyk launched an "AI Trust Platform" and acquired Invariant Labs (2025-06) for agent guardrails, MCP server scanning, tool-poisoning detection and runtime agent observation [S8].
2. **Hiring:** none confirmed in the snippets.
3. **Internal platforms:** a pipeline in which ML proposes new rules and security analysts vet them before they enter the symbolic engine [S7]. Fix validation is closed-loop: generate, then re-scan [S7].
4. **Human ops:** security analysts vet ML-suggested rules by hand [S7]. Agent behavior is checked with policies (Invariant Guardrails).
5. **New architecture need:** every LLM-generated patch needs a deterministic check, and agents/MCP need runtime enforcement.
6. **Scales linearly with:** generated code and fix requests (one validation scan each), plus MCP servers and tools in customer environments.
7. **Complaints:** none found in this pass.
8. **Built internally:** a symbolic validator wrapped around generative output, and bought agent guardrails (Invariant).
9. **Tags:** generated-code-review, agent-guardrails-runtime, mcp-tool-security, human-rule-vetting, ai-fix-validation
- **Economics (generated-code-review):** PEOPLE: analyst rule vetting [E] 5–15 FTE. INFRA: one extra scan per fix (cheap). SCALING: AI code volume. CURRENT: built and acquired in-house.

## 5. Wiz
1. **Changed:** acquired by Google for $32B (announced 2025-03, closed 2026-03-11) [S9]. About 3,200 employees. Leader in AI-SPM: it discovers shadow AI pipelines, model deployments and training data across AWS, Azure and GCP [S9]. Wiz Research found the exposed DeepSeek ClickHouse database (API keys, chat logs) [S10].
2. **Hiring:** still hires through its own Greenhouse portal [S9]. AI-specific roles were not confirmed.
3. **Internal platforms:** no public writing found on an internal LLM gateway or eval stack.
4. **Human ops (customer side):** security teams have to inventory AI services, keys and data stores. The DeepSeek case shows AI infra failing on *basic* exposure [S10].
5. **New architecture need:** a graph of AI assets (models, endpoints, vector DBs, training data, keys) joined to the cloud graph.
6. **Scales linearly with:** AI services deployed per customer, and model/endpoint sprawl.
7. **Complaints:** none specific.
8. **Built internally:** AI-SPM graph extensions.
9. **Tags:** shadow-ai-inventory, ai-asset-posture, data-permissions-for-ai, ai-api-key-sprawl
- **Economics (shadow-ai-inventory):** PEOPLE: [E] 0.5–2 FTE of security-team time per enterprise to inventory AI. FREQUENCY: continuous. SCALING: teams shipping AI × clouds. CURRENT: CSPM/AI-SPM (Wiz) plus spreadsheets [E]. Cross-ref Larridin: 62% of enterprises lack a full inventory of AI apps [S15].

## 6. Linear
1. **Changed:** Triage Intelligence and Product Intelligence (duplicate detection, related issues, suggested properties). The Agent API (2025) makes Claude Code, Devin, Cursor and Copilot workspace "teammates" [S11][S12].
2. **Hiring:** not found.
3. **Internal platforms:** an eng blog post, "How we built triage intelligence" [S12]. Embeddings started on OpenAI with pgvector on GCP, then moved to turbopuffer with Cohere embeddings because they needed hybrid search. GPT-5 and Gemini 2.5 Pro handle the complex issues [S12]. Talk: "Building the platform for agent coordination" [S12].
4. **Human ops:** humans accept or reject AI suggestions. The design treats provenance and trust as first-class [S12].
5. **New architecture need:** per-issue model routing (small vs. large model), re-indexing of embeddings when the provider changes, and identity/permissions for third-party agents acting as users.
6. **Scales linearly with:** issues created (one embedding plus an LLM call each), plus agent actions from third-party agents.
7. **Complaints:** third-party commentary says agents lack customer signal and cross-agent memory [S11].
8. **Built internally:** a hybrid-search retrieval stack, a provider-switch migration, and an agent identity model.
9. **Tags:** embedding-migration, inference-cost-routing, agent-identity-permissions, multi-agent-coordination, ai-provenance-ux
- **Economics (embedding-migration):** PEOPLE: [E] 1–3 eng-months per migration. INFRA: re-embed the full corpus. FREQUENCY: [E] about yearly. SCALING: corpus size. CURRENT: done by hand in-house.

## 7. PostHog
1. **Changed:** shipped PostHog AI (Max), its in-app agent, and sells LLM observability/analytics as a product [S13].
2. **Hiring:** not confirmed.
3. **Internal platforms:** the blog post "8 learnings from 1 year of agents" [S13]. A weekly **"Traces Hour"** has humans review production LLM traces, and evals are derived from what they find [S13]. Building realistic environments for multi-step tool evals is "a greater challenge than building the agent itself" [S13].
4. **Human ops:** a recurring meeting to read traces by hand, and ad-hoc evaluation of agent work [S13]. Token costs became a practical constraint when agents ran against live analytics data [S13].
5. **New architecture need:** sandbox or replay environments that support every tool the agent can call, for evals.
6. **Scales linearly with:** agent sessions (tokens) and tools (the size of the eval environment).
7. **Complaints:** agents produce "plausible but incorrect fixes" without rigorous evals [S13].
8. **Built internally:** an LLM analytics product built first for its own use (they dogfood it).
9. **Tags:** agent-observability, eval-pipelines, eval-environment-simulation, manual-trace-review, inference-cost-routing
- **Economics (manual-trace-review):** PEOPLE: a weekly hour × [E] 5–15 engineers, so about 0.2–0.4 FTE ongoing. FREQUENCY: weekly. SCALING: grows with agent surface area, not with traffic, because they sample. CURRENT: a human ritual plus their own trace tool.

## 8. Sentry
1. **Changed:** Seer reached GA. It is a root-cause and autofix agent, extended 2026-01-27 to local dev (via MCP) and to PR code review [S14]. Pricing went from $1 per fix run plus $0.003 per issue scan to a flat $40 per active contributor per month [S14].
2. **Hiring:** not confirmed.
3. **Internal platforms:** context assembly that walks trace-connected telemetry deterministically ("it's all about context" post) [S14]. A Seer budget management page exists in the docs [S14].
4. **Human ops:** customers manage their Seer budgets and quotas [S14]. Developers review the AI-generated fixes and PR comments.
5. **New architecture need:** an agent with access to the customer's repos plus telemetry, cost metering per run, and a switch from usage pricing to seat pricing (which implies cost-predictability complaints).
6. **Scales linearly with:** issues (scans), fix runs, and PRs (review).
7. **Complaints:** $40/contributor adds $400/mo for 10 engineers, and bills already spike after noisy deploys [S14].
8. **Built internally:** a telemetry-grounded agent and a pricing/metering redesign.
9. **Tags:** generated-code-review, ai-usage-metering, inference-cost-routing, ai-pricing-redesign, agent-observability
- **Economics (ai-usage-metering):** PEOPLE: the pricing redesign took [E] 2–5 people across eng, finance and product. INFRA: [E] fix runs cost $0.2–1.0 in tokens. FREQUENCY: pricing changes every 6–12 months. SCALING: runs per contributor. CURRENT: in-house metering, which they replaced with seats.

## 9. Retool
1. **Changed:** Retool Agents (build, test, deploy, evaluate, monitor), billed per agent-hour with separate rates for Retool-managed and self-managed LLMs ($5/hr for self-managed) [S16]. Self-hosted customers get it in a stable release [S16].
2. **Hiring:** not confirmed.
3. **Internal platforms:** a provider-abstraction layer. It uses Retool-managed OpenAI/Anthropic keys, *or* any custom provider that follows the OpenAI, Anthropic, Google or Cohere schema [S16]. Docs show customers putting an external AI gateway in front as the custom provider [S16]. In effect it is a built-in LLM gateway inside the product, plus agent evals and monitoring.
4. **Human ops:** enterprise customers have to wire their own gateway and governance, and self-hosted customers have to bring models.
5. **New architecture need:** support for BYO-model, BYO-key and BYO-gateway across both self-hosted and cloud, plus per-hour agent metering.
6. **Scales linearly with:** agent hours, the number of customer model providers, and self-hosted versions.
7. **Complaints:** none found.
8. **Built internally:** a multi-provider gateway, agent evals and monitoring, all duplicated *inside a product*.
9. **Tags:** internal-llm-gateway, byo-model-enterprise, internal-agent-platform, ai-usage-metering, eval-pipelines
- **Economics (internal-llm-gateway):** PEOPLE: [E] 2–4 engineers maintain provider adapters as provider APIs change. FREQUENCY: about monthly API changes [E]. SCALING: providers × features (tools, streaming, caching). CURRENT: built in-house, and customers often stack their own gateway on top.

## 10. Zapier
1. **Changed:** Agents, Chatbots and AI by Zapier. A non-technical-user agent builder [S17].
2. **Hiring:** "Staff Engineer, Applied AI" posted in several regions. An **AI Capabilities team** exists to *unify the runtimes, tooling, data models, and orchestration layers* behind Agents, Chatbots and AI by Zapier [S17]. That is explicit evidence that separate AI stacks were consolidated.
3. **Internal platforms:** a shared AI execution platform. A hierarchical eval framework runs unit tests, then trajectory evals, then A/B tests. Custom tooling turns any failure into an eval [S17]. An internal ecosystem of lightweight agents automates thousands of ops/admin tasks [S17]. They used RL fine-tuning with an outside lab (Prime Intellect case study) [S18].
4. **Human ops:** humans cluster user frustration, read the last interactions of customers who churned in the past 7 days, and compare Gemini Pro with Claude on regressions [S18].
5. **New architecture need:** full-run traces across model calls, DB calls, tools and REST, where any step can cascade a failure [S18]. Grading must handle intermediate tool calls and grader bias.
6. **Scales linearly with:** agent runs × integrations (8k+ apps means a huge tool surface), and churned customers reviewed.
7. **Complaints:** "Building a platform for non-technical people to build agents is even harder" [S18].
8. **Built internally:** a unified AI runtime (after duplication), a failure-to-eval tool, and an internal agent fleet.
9. **Tags:** internal-agent-platform, platform-consolidation-ai, eval-pipelines, agent-observability, regression-on-model-upgrade, tool-surface-testing
- **Economics (internal-agent-platform / consolidation):** PEOPLE: a team to unify the runtimes [E] 6–12 engineers. FREQUENCY: one-off re-platforming plus ongoing upkeep. SCALING: AI products × runtimes. CURRENT: built in-house, with Braintrust for evals [S18].

## 11. Airtable
1. **Changed:** an "AI-native refounding". Omni is a conversational app builder that assembles production-tested components instead of writing raw code. Field Agents do enrichment and routing. HyperDB supports 100M rows and connects to Snowflake, Databricks and Salesforce [S19]. Estimated $478M ARR (2024). Gross margin is about 90%, and Airtable says it will *trade margin* for AI growth [S19].
2. **Hiring:** not confirmed.
3. **Internal platforms:** a component library as the guardrail for generated apps, so generation is constrained rather than freeform [S19].
4. **Human ops:** [E] reviewing apps built by AI and fixing broken generated automations. Field Agents run per record, so cost has to be governed.
5. **New architecture need:** agents that run per row (each field cell is an LLM call) over 100M-row bases, which requires cost caps.
6. **Scales linearly with:** rows × agent fields × refreshes. This is the purest example of per-execution inference cost.
7. **Complaints:** the margin compression is explicit [S19].
8. **Built internally:** a constrained generation framework.
9. **Tags:** inference-cost-routing, ai-margin-pressure, generated-app-guardrails, ai-usage-metering
- **Economics (inference-cost-routing):** INFRA: [E] at 1M rows × $0.002 per call that is about $2k per refresh per field. PEOPLE: [E] 1–3 engineers on cost optimization and model routing. SCALING: rows × fields × frequency. CURRENT: in-house.

---

## Cross-cutting evidence
- Harness 2026 survey: 52% report no clear owner of AI costs, 72% had an unexpected AI bill spike in the past year, only 20% could explain a cost doubling within hours, and an estimated 26% of AI spend is wasted [S15].
- Larridin 2026: 58% cite fragmented AI ownership, and 62% lack an AI app inventory [S15].
- Shared vendor: Notion and Zapier both publicly use the same external eval/observability vendor (Braintrust) *plus* in-house scorers and tools [S1][S18]. That points to a hybrid pattern: buy the backbone, build the domain scoring.

## Pain tag summary

| pain tag | companies | which built internally | evidence strength |
|---|---|---|---|
| eval-pipelines | Notion, Vanta, Semgrep, PostHog, Zapier, Retool | Notion, Vanta, Semgrep, PostHog, Zapier, Retool (all hybrid in-house) | **Strong** (talks, eng blogs, job posts) |
| eval-dataset-curation (incl. SME/expert labeling) | Notion, Vanta, Semgrep, Snyk | Notion (contract labelers), Vanta (GRC SMEs), Semgrep (research team), Snyk (analysts) | Strong |
| regression-on-model-upgrade / model-selection-benchmarking | Notion, Zapier, Linear | Notion, Zapier | Strong (Notion <1 day model rollout, Zapier Gemini vs. Claude) |
| agent-observability / manual-trace-review | PostHog, Zapier, Sentry, Snyk(Invariant) | PostHog, Zapier | Strong |
| inference-cost-routing / ai-margin-pressure | Notion, Airtable, Linear, PostHog, Sentry | Linear (model tiering), Airtable, Notion | Medium-strong (pricing changes, margin statement) |
| ai-usage-metering / ai-pricing-redesign | Notion, Sentry, Retool, Airtable | Notion (credits), Sentry, Retool (agent-hours) | Strong (public pricing pages) |
| generated-code-review / ai-fix-validation | Semgrep, Snyk, Sentry | Semgrep, Snyk, Sentry | Strong (products plus methodology) |
| internal-agent-platform / platform-consolidation-ai | Zapier, Retool, Linear | Zapier (AI Capabilities team), Retool | Medium (Zapier job post is explicit) |
| internal-llm-gateway / byo-model-enterprise | Retool, Notion, Linear | Retool | Medium (inferred from multi-provider docs) |
| human-review-queue (AI output approval) | Vanta, Semgrep, Snyk, Linear | Vanta, Semgrep | Medium |
| ai-security-questionnaires | Vanta (customers' pain) | Vanta | Medium (one company, product evidence) |
| shadow-ai-inventory / ai-asset-posture | Wiz (plus Larridin survey) | Wiz | Medium |
| agent-guardrails-runtime / mcp-tool-security | Snyk, Wiz, Linear (agent identity) | Snyk (acquired Invariant) | Medium |
| eval-environment-simulation / tool-surface-testing | PostHog, Zapier | PostHog, Zapier | Medium (explicit quotes) |
| embedding-migration | Linear | Linear | Weak (single company) |
| agent-identity-permissions / data-permissions-for-ai | Linear, Wiz | Linear | Weak-medium |

---

## Sources
- [S1] Notion: braintrust.dev/blog/notion; braintrust.dev/customers/notion; latent.space/p/notion; ai.engineer/talks/how-to-build-world-class-ai-products-sarah-sachs-notion-and-carlos-esteban-braintrust; zenml.io/llmops-database/scaling-ai-product-development-with-rigorous-evaluation-and-observability; builtinnyc.com/job/software-engineer-ai-dev-velocity/9343304
- [S2] Notion pricing: userjot.com/blog/notion-pricing-2025-plans-ai-costs-explained; usagepricing.com/blueprint/notion-ai
- [S3] Notion jobs: builtinla.com/job/model-behavior-engineer/8552058; job-boards.greenhouse.io/notion/jobs/6565449003; builtin.com/job/ai-data-specialist-contract/3991903
- [S4] Vanta: ai.engineer/talks/why-building-eval-platforms-is-hard; builtinboston.com/job/senior-software-engineer-ai-product/7776264; builtinsf.com/job/software-engineer-ai-product-canada/9652499
- [S5] Vanta Trust Center: vanta.com/resources/vanta-trust-center-enhanced-questionnaire-automation-ai; businesswire.com/news/home/20240501482792/en
- [S6] Semgrep: semgrep.dev/blog/2025/semgrep-is-confidently-handling-60-of-all-triage-for-users-without-reducing-coverage; semgrep.dev/blog/2025/building-an-appsec-ai-that-security-researchers-agree-with-96-of-the-time/; semgrep.dev/docs/semgrep-assistant/metrics
- [S7] Snyk: snyk.io/blog/snyk-safe-adoption-of-ai/; snyk.io/platform/deepcode-ai/
- [S8] Snyk/Invariant: snyk.io/news/snyk-acquires-invariant-labs-to-accelerate-agentic-ai-security-innovation/; tech.eu/2025/06/24/snyk-acquires-ai-security-pioneer-invariant-labs-for-a-new-era-in-ai-safeguards/
- [S9] Wiz: aimagazine.com/news/how-wiz-became-a-32bn-cloud-security-powerhouse; gigazine.net/gsc_news/en/20260312-google-wiz; techinterview.org/companies/wiz-interview-guide/
- [S10] Wiz/DeepSeek: techtarget.com/cybersecurity/news/366618594/Wiz-reveals-DeepSeek-database-exposed-API-keys-chat-history
- [S11] Linear agents: blog.buildbetter.ai/linear-ai-agents-2026-guide-5-alternatives-for-engineering-teams/
- [S12] Linear: linear.app/blog/how-we-built-triage-intelligence; linear.app/now/how-we-built-product-intelligence; ai.engineer/talks/building-the-platform-for-agent-coordination
- [S13] PostHog: posthog.com/blog/8-learnings-from-1-year-of-agents-posthog-ai; createwith.com/tool/posthog/updates/posthog-tests-ai-agents-that-generate-product-improvements-from-analytics-data
- [S14] Sentry: blog.sentry.io/seer-sentrys-ai-debugger-is-generally-available/; sentry.io/about/press-releases/sentry-expands-seer-ai-debugging-agent; blog.sentry.io/want-ai-to-be-better-at-debugging-its-all-about-context; docs.sentry.io/pricing/quotas/manage-seer-budget; rollbar.com/blog/sentry-alternatives/
- [S15] Surveys: harness.io/press-and-news/new-harness-report-reveals-enterprise-ai-spend-has-outgrown-the-systems-built-to-track-it; larridin.com/press-releases/maximizing-ai-adoption-has-become-enterprises-largest-challenge-impacting-profits-in-72-according-to-a-new-larridin-study
- [S16] Retool: docs.retool.com/3.300/agents/concepts/faq; docs.retool.com/data-sources/reference/ai-models; portkey.ai/docs/aigw/integrations/libraries/retool.md
- [S17] Zapier: zenml.io/llmops-database/building-production-ai-agents-platform-for-non-technical-users; zenml.io/llmops-database/internal-ai-orchestration-and-automation-across-multiple-departments; builtinbristol.uk/job/staff-engineer-applied-ai/7888312
- [S18] Zapier evals: ai.engineer/talks/turning-fails-into-features-zapier-s-hard-won-eval-lessons; braintrust.dev/customers/zapier; primeintellect.ai/case-study/zapier
- [S19] Airtable: airtable.com/newsroom/introducing-the-ai-native-airtable; sacra.com/research/airtable; maginative.com/article/airtable-bets-big-on-ai-agents-with-omni-reboots-as-an-ai-native-app-platform/
