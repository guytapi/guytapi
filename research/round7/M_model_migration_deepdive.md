# Thesis M deep dive: Model migration and "model arbitrage" for production agents

Date: 2026-10-05. Analyst stance: red team. My job was to kill this unless the evidence kept it alive.
Builds on: `agent_runtime_reliability.md` #1 (6.5/10) and `ai_infra_ops.md` #2 (5.5/10).
Budget: 38 web searches. WebFetch and Reddit were blocked, so every claim comes from search-result snippets. URLs below are ones the search engine returned. Anything marked **[unverified]** means I saw a snippet but did not read the page.

**Thesis (as given):** "Your AI provider retires the model your agents run on every few months, and newer models are cheaper but behave differently. We move your agents to the right model safely. We replay your real production runs on candidate models, show exactly which agent decisions and tool calls change, auto-fix prompts and tool schemas, and certify the switch. We do it before the deadline, or whenever a cheaper model can do the job."

**Bottom line up front:** The pain is real, recurring and dated. The product, however, has already been built at least five times: as an open-source CLI (rightmodeler), as a replay runtime (ZenML Kitaru, Retrace), as a feature inside every observability and eval tool (Datadog one-click trace replay, LangWatch, LangSmith, Braintrust Loop), as a prompt auto-fixer (Not Diamond Prompt Adaptation, Vertex, Foundry and OpenAI prompt optimizers), and as free hyperscaler tooling (AWS Transform model-to-model, Microsoft Foundry's six-phase migration process, Google Cloud's agent-based upgrade workflow, Anthropic's `/claude-api migrate`). The cost-arbitrage expansion is being chased by three YC S26 companies (Understudy, Experiential, Belvedir) plus Stripe-owned OpenRouter (bought for more than $7B). **Verdict: KILL as a standalone company.** The REFRAME options are weak (see the end).

---

## 1. Retirement cadence, notice periods, breakage, migration effort

### Cadence and notice (2025-2026)
| Provider | Evidence | Notice |
|---|---|---|
| OpenAI | 18 models shut down on Jul 23, 2026 ([ecorpit](https://ecorpit.com/openai-model-shutdowns-23-july-2026-migration-map/) [unverified]). An Oct 23, 2026 batch covers gpt-3.5-turbo, gpt-4, gpt-4-turbo, gpt-4.1-nano, gpt-4o-2024-05-13 and o-series snapshots ([OpenAI deprecations](https://developers.openai.com/api/docs/deprecations/index.html), [community notice](https://community.openai.com/t/deprecation-notice-upcoming-model-shutdowns-in-2026/1379553)). chatgpt-4o-latest ended Feb 16, 2026 ([VentureBeat](https://venturebeat.com/ai/openai-is-ending-api-access-to-fan-favorite-gpt-4o-model-in-february-2026)). Evals and the dataset-backed prompt optimizer go read-only Oct 31 and shut down Nov 30, 2026 ([prompt optimizer guide](https://developers.openai.com/api/docs/guides/prompt-optimizer)). | Typically 3-6 months. No grace period and no automatic fallback. |
| Anthropic | Sonnet 4.5 deprecated 2026-09-30 and retires Nov 30, 2026, a 61-day window (some sources say a Nov 24 start with throttling from Oct 30) ([Anthropic deprecations](https://platform.claude.com/docs/en/resources/model-deprecations), [Retell notice](https://docs.retellai.com/deprecation-notice/2026/09-29_claude_sonnet_4_5)). The date was reportedly pushed back several times (May 18, then Jun 22, then Nov) ([aiproductivity](https://aiproductivity.ai/news/anthropic-claude-sonnet-45-deprecation-date-extended-may-18/), [vantagepoint](https://vantagepoint.io/blog/ai/claude-sonnet-4-5-retirement-june-22) [unverified]). One deprecation in April 2026 had a 62-day window, Apr 14 to Jun 15 ([agentpatterns](https://agentpatterns.ai/workflows/model-deprecation-lifecycle/) [unverified]). Opus 4.1 retired Aug 5, 2026 (prior file). | About 60 days. |
| Google | Gemini 2.5 Flash and Pro shut down Oct 16, 2026, roughly 4.5 months after the 2.0 migrations ([gcpstudyhub](https://gcpstudyhub.com/blog/google-is-retiring-gemini-2-5-on-agent-platform-what-you-need-to-know-and-do-before-october-2026)). Some users got early 404s on Jul 9, which Google rolled back ([forum 174267](https://discuss.ai.google.dev/t/gemini-2-5-flash-and-gemini-2-5-flash-lite-returning-404-no-longer-available-today-july-9-contradicts-oct-16-2026-shutdown-date/174267), [174217](https://discuss.ai.google.dev/t/gemini-2-5-flash-deprecated-without-warning-earlier-than-shutdown-date/174217)). Google's own count is six major model evolutions since 2023 ([Google Cloud blog](https://cloud.google.com/blog/products/compute/lessons-in-accelerating-foundation-model-upgrades)). | 3-6 months, and sometimes less in practice. |
| Azure / Foundry | gpt-4o 2024-11-20 and gpt-4o-mini 2024-07-18 retired Oct 1, 2026. Standard deployments auto-upgrade; PTU and NoAutoUpgrade deployments get HTTP 410 after the date, with no extensions ([privatedevops](https://privatedevops.com/news/azure-openai-gpt-4o-retirement-october-2026), [MS model retirements](https://learn.microsoft.com:443/en-us/azure/ai-services/openai/concepts/model-retirements)). GA models usually carry a retirement date about 18 months out ([baeke.info](https://news.baeke.info/articles/microsoft-foundry-details-six-phase-process-for-migrating-llm-models)). | Longest windows of the group, but auto-upgrade can move production silently. |
| Bedrock | Has a lifecycle page. AWS Transform excludes models within 90 days of end of life from its recommendations ([AWS what's new](https://aws.amazon.com/about-aws/whats-new/2026/06/aws-transform-model-to-model-assessments/)). | Not researched further. |
| Downstream platforms | GitHub Copilot retired Gemini 3.5/3.6 Flash, Kimi K2.7 and Opus 4.7 on Oct 2 ([aicybr](https://aicybr.com/blog/github-copilot-model-deprecation-october-2026) [unverified]). Kore.ai, Retell, LivePerson and UiPath all pushed "action required" notices to customers. | These pass the pain on to enterprise buyers. |

**Synthesis.** A team using two providers in production now faces roughly 2-4 forced migrations per production integration per year. "Versioned models had a shelf life of roughly six months in 2026" ([softwareseni](https://www.softwareseni.com/deprecation-pressure-the-six-month-shelf-life-of-enterprise-ai) [unverified]). Of all the claims in the thesis, the cadence claim holds up best.

### Breakage examples
- **Sonnet 5.5:** forced `tool_choice` returns 400. The fix is `auto` plus `strict`, after which "the model may now answer without calling the tool". Sampling parameters, prefill, thinking budgets and disabling thinking all return 400. Adaptive thinking is now on by default ([Anthropic migration guide](https://platform.claude.com/docs/en/models/sonnet-5-5/migration-guide)). This is exactly the "tool-call decisions change" failure mode the thesis targets.
- **gpt-realtime-2.1:** command execution fell to about 25% from 98-100% (OpenAI community, prior file).
- Tursio: 95.1% and 97.3% pass rates on newer GPT models, which works out to about 500 silent failures a day at 10k queries ([tianpan](https://tianpan.co/blog/2026-05-17-model-end-of-life-took-your-prompt), secondhand).
- LangWatch's own example: a model 38% cheaper "stopped asking for the order number before issuing a refund" in a handful of 200 scenarios ([LangWatch docs](https://langwatch.ai/docs/improve-your-agent/reduce-cost-and-latency)). The example is real, and a vendor already uses it in its marketing.

### Effort per migration
- AWS: "one production model migration can take two days to two weeks" (via [PromptLayer glossary](https://www.promptlayer.com/glossary/model-migration) / [ibl.ai](https://ibl.ai/blog/frontier-model-churn-migration-cost-portability.md) [unverified]).
- Practitioner blogs: "two to six weeks of engineering time", and "spend the next two weeks firefighting regressions" ([tianpan migration playbook](https://tianpan.co/blog/2026-04-10-model-migration-playbook-swap-foundation-models-without-breaking-production)).
- Google says its agent workflow cut upgrades "from weeks to days", in hours for some projects ([webpronews](https://www.webpronews.com/google-cuts-foundation-model-upgrades-from-weeks-to-days-lessons-learned/), [Google blog](https://cloud.google.com/blog/products/compute/lessons-in-accelerating-foundation-model-upgrades)).
- **Number of prompts or agents per company:** I found no hard number. LangChain's survey says 57% of 1,340 respondents have agents in production, 89% have observability and only 52% have evals ([LangChain State of Agent Engineering](https://langchain.com/state-of-agent-engineering)). That 89-vs-52 gap is the best evidence for "traces exist, golden sets don't". It also means the trace holders (observability vendors) sit in the strongest position.

**Red-team read:** at 0.4-6 engineer-weeks per migration and about $4-5k per engineer-week fully loaded, a migration costs a team roughly $2k-30k in labor. With 2-4 migrations a year, the labor saved per integration is about $10-100k a year. A company with 5-20 integrations has a meaningful but not huge pool, and most of that work becomes partly automated by free provider tooling and coding agents (`/claude-api migrate` handles the API-shape part).

## 2. Cost-savings side (model arbitrage)
- 2026 list prices per 1M input/output tokens: GPT-5.5 $5/$30; Claude Sonnet 4.6 $3/$15; Gemini 3.5 Flash $1.50/$9; DeepSeek V4 $0.435/$0.87, which is 5-70x cheaper ([CometAPI](https://www.cometapi.com/2026-llm-api-pricing-comparison-gpt-5-5-claude-gemini/) [unverified figures]). Gaps of 3-30x exist between frontier and "good enough" tiers.
- "Stuck because re-validating is expensive": this exists only as **analyst and blog framing**, not as first-person practitioner quotes. Examples: "abstraction layer handles roughly 20% of the actual switching cost" ([tianpan vendor lock-in](https://tianpan.co/blog/2026-04-17-llm-vendor-lock-in-hidden-switching-costs)) and "the eval re-anchoring tax" ([tianpan](https://tianpan.co/blog/2026-05-14-model-migration-eval-reanchoring-hidden-cost)). I found **no** HN or GitHub post saying "we would save $X but can't validate". This gap is a kill signal for the arbitrage expansion.
- **Arbitrage is crowded, and with a better-funded approach.** Understudy Labs (YC S26) captures traces and distills a cheaper owned model via prompt tuning, SFT and RL, claiming up to 50x cheaper ([YC](https://www.ycombinator.com/companies/understudy-labs)). Experiential Labs (YC S26, AutoGPT founders) is an open-source gateway that turns production traffic into a custom router or model, "50%+ cheaper" ([YC](https://www.ycombinator.com/companies/experiential-labs), HN launch Aug 27). Belvedir (YC S26) is a "custom model factory" ([extruct](https://www.extruct.ai/data-room/ycombinator-companies-s26/) [unverified]). Not Diamond and Martian sell routers. Stripe is acquiring OpenRouter for more than $7B ([Bloomberg Gov](https://news.bgov.com/mergers-and-acquisitions/stripe-nears-deal-to-buy-ai-firm-openrouter-for-over-7-billion)). Microsoft Foundry ships a model router.

## 3. Competition: what each player does compared with "replay + diff tool calls + auto-fix + certify"

| Player | Replay prod traces | Diff tool-call decisions | Auto-fix prompts/schemas | Certify / cutover | Notes |
|---|---|---|---|---|---|
| **rightmodeler** (OSS CLI) | Yes: auto-detects 10 trace formats (LangSmith, OpenAI SDK, Langfuse, Braintrust) into a per-step schema | Per-step agreement, abstentions | No | **Ships approved swaps as PRs "with evidence attached"** | Close to a feature-for-feature clone of the wedge ([futuretools](https://futuretools.io/tools/rightmodeler-8ac89a3f) [unverified]) |
| **ZenML Kitaru** | Yes: re-executes whole sessions, with tool calls "answered from the recording" by name and arguments | Yes (downstream decision path) | No | No | Explicitly markets "switch from one model to another" ([ZenML blog](https://www.zenml.io/blog/introducing-the-new-kitaru), [docs](https://docs.zenml.io/kitaru/guides/replay-and-overrides.md)) |
| **Retrace**, OrcaReplay, runopsy-replay, agent-replay | Record, replay, fork with model swap and stubbed tools | Side-by-side divergence | No | No | Product Hunt / OSS ([PH](https://www.producthunt.com/posts/retrace-2)) |
| **Datadog LLM Obs Experiments** | "With a single click, import a problematic trace and replay it with alternative prompts, providers" | Partial | No | No | Already the incumbent APM in large accounts ([Datadog](https://datadoghq.com/blog/llm-experiments)) |
| **LangWatch** | "Turns your real conversations into simulated scenarios and runs them against the candidate model" | Per-scenario | Optimization Studio (DSPy) | No | Markets the cheaper-model use case directly |
| **LangSmith** ($1.25B) | Datasets from traces; trajectory evals | Trajectory evals | Prompt canvas | No | |
| **Braintrust** ($800M, Feb 2026) | Logs to datasets; proxy model swap "with zero code changes" | Scorers | **Loop agent** improves prompts, datasets and scorers together | No | ([Braintrust Loop](https://braintrust-mk7vysyg7.preview.braintrust.dev/docs/guides/loop)) |
| Langfuse (acquired by ClickHouse, Jan 2026; 2,000+ paying customers) | Datasets from traces | Evals | Prompt management | No | |
| Arize/Phoenix, Galileo (AutoTune), W&B Weave, Opik, Confident AI, Patronus, FutureAGI | Compare models on datasets | Varies | Some prompt optimization | No | Generic evals (excluded category) |
| Humanloop | Gone (acqui-hired by Anthropic in Aug 2025; platform off Sep 8, 2025) | | | | |
| promptfoo | Acquired by OpenAI in Mar 2026, folded into Frontier | Red-team plus agent evals | | | |
| **Not Diamond Prompt Adaptation** | No | No | **Yes: agentic rewrite of prompts for a target model**, "migrate between model providers" | No | Private beta per its docs ([docs](https://docs.notdiamond.ai/docs/what-is-prompt-adaptation)) |
| DSPy / GEPA, PromptWizard | No | No | Yes (OSS) | No | |
| **AWS Transform model-to-model** (Jun 2026) | No (scans code) | No | Code changes plus prompt optimization (Bedrock Advanced Prompt Optimization) | Migration plan | Free; moves you *to Bedrock* only |
| **Microsoft Foundry** | Simulator plus continuous eval | 30+ evaluators | Prompt Optimizer, agent optimization | Auto-upgrade controls | A full six-phase "Discover→Retire" process (Sep 2026) |
| **Google Cloud** | Agent-based migration workflow (internal and Applied ML; tied to Gemini Enterprise Agent Platform + Antigravity) | Yes | Yes | n/a | "Weeks to days" |
| **Anthropic** `/claude-api migrate` | No | No | Parameter and code fixes, not behavior | No | Free |
| OpenAI prompt optimizer | No | No | Yes (dataset-backed) | No | **Being shut down Nov 30, 2026**; OpenAI is folding testing into Frontier and promptfoo |
| Voice: Hamming, Coval ($28M A), Cekura, Bluejay | Call replay and simulation | Yes | No | No | They own voice regression testing |
| Routers: OpenRouter/Stripe, Martian, Not Diamond, Experiential, Foundry router | Cost routing | n/a | Not Diamond | n/a | Own the arbitrage layer |

**Net:** no single vendor bundles all four boxes with a "certificate". But each box is either commoditized open source or a sprint-sized feature for a vendor that already holds the customer's traces. "Certify" is a PDF, not a moat.

## 4. Would providers or eval vendors build it?
- **Providers:** they already have. AWS, Microsoft and Google each built migration tooling in 2026, and Anthropic ships a migration skill. They have every incentive to automate *same-provider* upgrades, and AWS even automates *cross-provider-to-AWS* moves for free. A neutral cross-provider tool is the only gap they leave open. That gap is exactly where OpenRouter/Stripe, routers and eval vendors sit.
- **Eval vendors:** a "migration mode" is about 1 quarter of work for Braintrust (Loop plus proxy swap plus logs) or Datadog (one-click replay already exists). LangWatch already markets the cheaper-model flow with stubbed scenarios. Expect each to ship a "deprecation-aware migration report" timed to the next big retirement wave.

## 5. Buyer, market size, ACV, pilot, WTP
- **Buyer:** Head of AI Platform or CTO at AI-native and mid-market SaaS companies with 5+ production LLM integrations. Budget is episodic and spikes around deadlines.
- **Companies with production agents:** about 57% of LangChain's survey respondents (a biased sample). A reasonable estimate is 3,000-8,000 companies worldwide with platform teams and LLM spend above $250k a year [estimate].
- **ACV options:** per-migration certificate at $15-40k. Subscription for deprecation readiness plus regression CI at $30-80k a year. A share of savings (20-30% of year-1 savings) only works where swaps actually happen, and those buyers are the ones Understudy, Experiential and routers already target.
- **Benchmark:** LangSmith, the category leader's eval and observability product, had about $12-16M ARR in 2025 ([Sacra](https://sacra.com/c/langchain) [unverified]). Braintrust is valued at $800M. A migration-only *slice* of that category is smaller than the category itself.
- **Pilot (14-30 days):** take a Sonnet 4.5 (Nov 30) or gpt-4o snapshot customer. Import 2-5k traces, replay with stubbed tools on Sonnet 5.5 or gpt-5.x, report per-workflow tool-call deltas, run auto prompt and schema edits, then do a canary cutover. Success means a cutover before the deadline with incidents at or below baseline, and engineer time under 3 days.
- **WTP:** low to medium. Evidence of *paying* for migration is absent. The free alternatives (provider tools, OSS rightmodeler, Kitaru, an existing eval vendor seat, Claude Code doing the edit) set the anchor near zero. Tian Pan's "trace replay you cannot trust" argument (caches, memory and side effects aren't in the trace) also weakens the "certify" promise, because a certificate that misses regressions is a liability.

## Market math
- **$10M ARR:** about 250 customers at $40k. Feasible if the product beats the free tools. With 3-8k qualified buyers, that is 3-8% penetration.
- **$50M ARR:** about 800 customers at $60k. This requires becoming a full eval and regression-CI platform, meaning head-on competition with Braintrust, LangSmith, Datadog and Langfuse/ClickHouse.
- **$100M ARR:** about 1,300 customers at $75k, or a savings-share model on more than $1B of managed LLM spend. That is the router or OpenRouter business, which Stripe bought for over $7B. No evidence a newcomer gets there from a migration wedge.

## 5 simulated buyers
1. **Head of AI Platform, Series C vertical-AI company (30 agents on Sonnet 4.5, Nov 30 deadline):** MAYBE. "We already have Braintrust logs. If Loop plus a proxy swap gets us 80% of the way, I'm not adding a vendor 8 weeks before the deadline."
2. **CTO, voice-agent startup (gpt-realtime retiring Jan 20, 2027):** NO for this product. "Replay shows me it's broken. Hamming already shows that. I need the tool calls to actually fire on 2.1, which is an architecture fix."
3. **Enterprise AI CoE lead on Azure (auto-upgrade):** NO. "Foundry has the migration process, simulator and evaluators, and procurement already approved Microsoft."
4. **Eng manager, AI-native SaaS with $3M/yr LLM spend:** MAYBE, but on the arbitrage side, comparing against Understudy and Experiential, which promise a 50% cut via owned models rather than a one-time swap.
5. **Platform lead, 200-person fintech with 8 LLM features and no evals:** YES for one $20k engagement. Its own words would be: "Do it for us before Oct 23." That is a services buyer with no renewal.
Score: 1 YES (services-shaped), 2 MAYBE, 2 NO.

## VC committee view
- **Bull case:** a recurring forcing function (2-4 migrations a year, dated deadlines) is rare in dev tools, and a cross-customer "model X breaks pattern Y" dataset could become a compatibility matrix.
- **Bear case (which wins):** (a) this is the excluded generic-evals category with a calendar attached; (b) trace holders (Datadog, LangSmith, Braintrust, Langfuse) own the input data and ship this as a feature; (c) hyperscalers give migration away free to win workloads; (d) the arbitrage expansion is already crowded with YC S26 distillation startups and a $7B Stripe-owned router; (e) the product is episodic and services-shaped.
- **Could it be $10B?** Only if it becomes the neutral control plane for model choice, and that seat is taken by OpenRouter/Stripe plus the observability majors. **Committee verdict: pass.** The likely outcome is a $20-80M tuck-in by an eval vendor at best.

---

## METHOD template

**Problem.** Providers retire model snapshots every 2-6 months, often with about 60 days' notice. Successor models change agent behavior: tool-call propensity, rejected parameters, thinking defaults, formats. Teams have no behavior-parity test built from their own traffic, and cheaper models go unused because re-validation is costly.

**Recent evidence (5+ independent signals).** (1) Sonnet 5.5 rejects forced tool_choice, sampling parameters and prefill (Anthropic guide); (2) Sonnet 4.5 retires Nov 30 after 61 days' notice; (3) Gemini 2.5 retires Oct 16, with premature 404s in July; (4) Azure PTU and NoAutoUpgrade deployments get 410 errors on Oct 1 with no extensions; (5) OpenAI's Oct 23 batch plus Evals and prompt optimizer shutting down Nov 30; (6) gpt-realtime-2.1 tool regression from 98% to 25%; (7) Google, Microsoft and AWS each publishing migration tooling or processes in Jun-Sep 2026; (8) downstream platform notices (Retell, Kore.ai, UiPath, Copilot). Pain is established. **Paying demand is not.**

**Who has the pain.** AI platform teams at AI-native and mid-market SaaS companies with multiple production LLM integrations. Voice-agent companies are hit hardest.

**What they do today.** grep for model IDs, `/claude-api migrate`, spot checks, existing eval vendor datasets, provider migration guides and optimizers, shadow traffic through gateways, and forum pleas.

**Why current products fail.** Eval tools need golden sets, and only 52% of teams have evals. Provider tools fix API shape, not behavior, and only within their own cloud. Replay tools debug single runs rather than certify a migration. *Counterpoint:* rightmodeler, Kitaru, LangWatch and Datadog each close a large part of that gap.

**Why now.** The heavy deprecation wave of Oct-Dec 2026, forced parameter changes in Sonnet 5.5, OpenAI Evals shutting down (orphaned eval suites), and Gemini's double migration in 4.5 months.

**Potential product.** Trace import into a replay harness with stubbed tools, then per-workflow tool-decision diffs, prompt and schema auto-repair, a parity certificate, and a canary plan, with continuous deprecation readiness afterward.

**Time to value.** 1-2 weeks with traces; 3-4 weeks without.

**Pilot (14-30 days).** One Sonnet 4.5 or gpt-4o customer, 2-5k traces, cutover before the deadline, incidents at or below baseline, under 3 engineer-days.

**Willingness to pay.** Low to medium, and episodic: $15-40k per migration. Free substitutes set the anchor. No evidence of anyone paying for this specific job.

**Expansion.** Cost arbitrage, cross-provider portability, regression CI for every prompt or agent change, a behavior system of record. All of these are contested.

**Competition.** Very high (see the table): rightmodeler, Kitaru, Retrace, Datadog, LangWatch, LangSmith, Braintrust Loop, Langfuse/ClickHouse, Not Diamond, AWS Transform, Microsoft Foundry, Google Cloud, Anthropic, Hamming/Coval/Cekura, Understudy, Experiential, Belvedir, OpenRouter/Stripe.

**Moat (10/100/1,000 customers).** At 10: none, since the replay harness is open-source-grade. At 100: a library of model-pair breakage patterns, though providers publish breaking changes themselves and the patterns go stale with each generation (6-month half-life). At 1,000: a cross-customer compatibility matrix, but Datadog, LangSmith and Braintrust each already see far more traces, and OpenRouter sees more model-switch traffic. Moat stays weak at every scale.

**CTO test sentence.** "Before Sonnet 4.5 dies on Nov 30, we replay your last 5,000 agent runs on Sonnet 5.5, show every tool decision that flips, fix the prompts, and hand you a signed cutover plan." Likely response: "Braintrust / Datadog / Claude Code can do most of that. What's the 20% they can't?"

**Kill test question.** "For your last forced migration: how many engineer-days did it take, did you use your eval or observability vendor or provider tools, and would you have paid $20k to a new vendor to make it 2 days?" Kill if fewer than 3 in 10 say yes, or if most say their existing vendor covered it.

### Scores (1-10)
| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC |
|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 8 | 8 | 7 | 6 | 6 | 4 | 2 | 3 | 5 | 4 |
**Average: 5.5** (down from 6.5 in the first pass, after the competitor search found rightmodeler, Kitaru, Datadog replay, LangWatch, AWS Transform, Foundry, Google's workflow and three YC S26 arbitrage startups).

## Kill signals (observed)
1. A near-identical OSS tool exists: rightmodeler (trace replay on candidate models, then a PR with evidence).
2. Trace holders already ship replay with model swaps (Datadog one-click, Kitaru, LangWatch).
3. All three hyperscalers plus Anthropic ship migration tooling for free (Jun-Sep 2026).
4. The arbitrage expansion is occupied: three YC S26 companies plus a $7B Stripe/OpenRouter.
5. No practitioner evidence of *paying* for migration, and no first-person "stuck on expensive model" posts. The case rests on blog and analyst framing.
6. Episodic, services-shaped budget; a benchmark category ARR of about $12-16M (LangSmith 2025).
7. Methodological attack on "certify" (trace replay misses caches, memory and side effects).

## VERDICT: KILL
The pain is real and calendar-driven, but the product is the excluded "generic evals" category with a deadline attached. Every component is already shipped by a free provider tool, open-source software, or a vendor that already holds the traces. The only surviving REFRAMEs are weak:
- (a) **Voice-agent deterministic tool layer** (prior file #2, 5.9): it fixes behavior instead of measuring it, but the buyer pool is a few hundred companies.
- (b) **Migration-as-a-service agency** riding the Oct-Dec 2026 wave for cash, not venture scale.

Neither clears the 8.5 bar.
