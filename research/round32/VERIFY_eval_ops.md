# VERIFY: F-B "Eval and ground-truth operations"

Date: 2026-10-06. Method: 22 WebSearch queries, run adversarially (looking for reasons the idea fails). WebFetch was not used, so figures come from search snippets of the cited pages. [E] marks an estimate.

Wedge under test: **managed, expert-calibrated LLM judges per domain, sold with an agreement SLA (≥0.85 vs. the customer's experts), cutting expert-labeling hours per model upgrade by 70%.**

## Bottom line
**The pain is real but much smaller than SYNTHESIS sized it, and the market has already crowded and consolidated around it.**

- **The tooling layer** has one $1B+ independent (LangChain), one at $800M (Braintrust), one $70M Series C (Arize) and one $50M Series B (Patronus). The other big players have been acquired by platforms: Galileo by Cisco, Langfuse by ClickHouse, W&B by CoreWeave, Humanloop by Anthropic and Promptfoo by OpenAI.
- **The expert human-data layer** has moved into enterprise evals: Scale Enterprise Evaluations, Mercor Enterprise, Snorkel Expert Data-as-a-Service (Snorkel is at a $375M run rate and a $3.5B valuation), Surge, micro1 Cortex, and Vals AI for domain-expert graders.
- **Judge calibration as a product feature** already exists: LangSmith Align Evals.
- **"17 of 19 built in-house" is misread.** The source files show the pattern is hybrid: Notion and Zapier buy Braintrust and build only the domain scorers. What stays in-house is the *customer's own definition of quality*, and practitioner consensus says that should not be outsourced.

**Verdict: drops from 7.8 to about 5.9.** The opening is narrow and service-heavy.

## 1. Competitor landscape (2025–2026)

| Player | Status / funding | Overlap with the wedge |
|---|---|---|
| **Braintrust** | $80M Series B at an $800M valuation, Feb 2026 (ICONIQ, a16z, Greylock). About $36M ARR in 2025. Customers include OpenAI, Notion, Stripe, Vercel, Replit, Ramp, Airtable and Zapier. [forbes.com.au/news/innovation/notion-and-stripe-trust-this-year-old-startup...; finder.techleap.nl/news/feed/braintrust-raises-80m...; ecosistemastartup.com/7-herramientas-de-observabilidad-ia-2026...] | It is the backbone that our "in-house" evidence companies actually run on. Its Loop feature generates scorers. |
| **LangChain / LangSmith** | $125M at a $1.25B valuation, Oct 2025 (IVP, Sequoia, Benchmark, CapitalG; Datadog and Databricks also invested). $12–16M ARR in mid-2025. [siliconangle.com/2025/10/20/...; fortune.com/2025/10/20/...] | **Align Evals** calibrates LLM judges against human graders, with an alignment score, a list of disagreements and a saved baseline. [blog.langchain.com/introducing-align-evals; venturebeat.com/ai/langchains-align-evals...] This is the calibration half of the wedge, shipped as a feature. |
| **Arize** | $70M Series C, Feb 2025 (Adams Street, M12, Datadog). [arize.com/blog/arize-ai-raises-70m-series-c...] | Evals and observability, plus the open-source Phoenix. |
| **Patronus AI** | $50M Series B, Jun 2026, ~$443M valuation. It has pivoted toward "digital world models" for agent testing. Judge models include Lynx and Judge-Image. [raising.fi/news/patronus-ai-series-b-june-2026; caplight.com/company/patronus-ai] | The closest earlier attempt at "judges as a product". It moved upmarket into simulation, which suggests judge-as-a-product alone was not enough. |
| **Galileo** | **Acquired by Cisco** (closed 2026-05-22) for Splunk Observability. [mlex.com/mlex/articles/2313963] | Consolidation into observability suites. |
| **Humanloop** | **Acqui-hired by Anthropic**, Aug 2025. The platform shut down 2025-09-08, and the team went into the Console's Evaluations features. [finder.techleap.nl/.../anthropic-acquires-humanloop...; tech.co] | Labs absorb eval tooling. |
| **Promptfoo** | **Acquired by OpenAI**, Mar 2026, and folded into the Frontier enterprise agent platform. It was used by 25% of the Fortune 500. [news.bloomberglaw.com/...promptfoo...; futurumgroup.com] | Same pattern. |
| **OpenAI Evals** (AgentKit, Oct 2025) | **Winding down**: announced 2026-06-03, read-only from 2026-10-31, gone 2026-11-30. [mcp.directory/blog/openai-agentkit-deprecation-2026; spotdev.co.uk] | A small migration window; teams must move their eval datasets out by end of October. |
| **Langfuse** | **Acquired by ClickHouse**, Jan 2026. 2,000+ paying customers and 63 of the Fortune 500. [clickhouse.com/blog/clickhouse-acquires-langfuse...] | Open-source evals and traces, now free or cheap. |
| **Datadog LLM Obs; W&B Weave** (CoreWeave acquired W&B, Mar 2025) | Both have experiments and quality evals. [braintrust.dev/articles/datadog-llm-observability-alternatives-2026; respan.ai] | Bundled into existing infrastructure contracts. |
| **Confident AI** (DeepEval) | $2.2M seed (YC). Now on AWS Marketplace. [finder.techleap.nl/.../confident-ai-raises-2-2m...] | Low end, open source. |
| **Scale AI: Enterprise Evaluations** | A dedicated team that builds "gold-standard human-rated datasets and expert rubrics that anchor AI evaluation systems" plus LLM-as-judge autoraters, *with enterprise customers*. [jobs.accel.com/companies/scale-ai/jobs/...enterprise-evaluations; greenhouse scaleai 4629589005] | **This is the wedge** (expert rubrics plus a calibrated autorater) offered as a managed service. |
| **Mercor** | Mercor Enterprise captures "how their best people actually work" for Fortune 500 agents. Its APEX benchmarks are built with experts in law, medicine and finance, and it pays experts more than $4M a day. [jobs.generalcatalyst.com/companies/mercor/...] | Has the expert supply and an enterprise motion. |
| **Snorkel AI** | $350M Series E at $3.5B, Sep 2026. **$375M run rate.** Products are Snorkel Evaluate and Expert Data-as-a-Service (SME-built evaluation datasets). [implicator.ai/snorkel-ai-350m-series-e; snorkel.ai press] | A direct, well-funded "expert ground truth plus eval workflow" offer for enterprises. |
| **Surge AI** | Rubrics, evaluation protocols, live chat rating and transcript scoring. It markets itself as a neutral evaluator. [sacra.com/research/surge-ai] | Mostly sells to labs today, with enterprise optionality. |
| **Vals AI** | $40M Series A at $400M, Aug 2026 (a16z). Private domain benchmarks for legal, tax, finance and clinical work, with "automated grading systems that evaluate the final work product to an expert standard". [wsgr.com/...vals-ai...; sacra.com/c/vals-ai] | Domain-expert-calibrated graders, the closest match to "expert-calibrated judge per domain". Today it is positioned on model benchmarking, and the pivot to grading a customer's own app is short. |
| **micro1 (Cortex)**, HUD, FutureAGI, Scorecard, Okareo and others | micro1 sells an "enterprise agent-evaluation layer". [rl-list.com; presenc.ai/research/ai-agent-evaluation-startups-2026] | A long tail of entrants. |

**No one sells an explicit *agreement SLA* for a calibrated judge.** That is the only literally unclaimed element I found. Scale, Snorkel and Vals each sell the ingredients (expert rubrics, gold data and an autorater) as a managed service.

## 2. Why companies still build in-house (explicit reasons)
- **Quality is product-specific taste, not a domain standard.** Hamel Husain (who has trained 2,000+ people at 500+ companies) says off-the-shelf metrics such as hallucination and toxicity are "not worth paying attention to directly". He recommends a single principal domain expert, a "benevolent dictator", whose judgment becomes the gold standard. [lennysnewsletter.com/p/building-eval-systems-that-improve] LangChain's calibration guide: "Labels must come from a domain expert, not outsourced annotators." [langchain.com/articles/llm-as-a-judge] **This directly undercuts "managed experts".** The expert who matters is the customer's own (Shopify's merchant-success lead, Notion's model-behavior engineer, Vanta's GRC SMEs, Harvey's lawyers).
- **What they buy and what they build.** Notion and Zapier buy Braintrust as the backbone and build per-feature scorers in-house (companies_D, S1/S18). Vanta's talk "Why building eval platforms is hard" describes judges *calibrated with its own GRC SMEs*. Shopify calibrates its judge against its own 3+ expert labelers. The in-house part is the domain rubric and the labels, which are the company's own IP and moat.
- **Control of cost and vendors.** Judge calls add a second dependency on the judge-model vendor's pricing, and teams want to own who the eval tool is accountable to. [futureagi.substack.com/p/when-is-building-your-llm-evals-actually; layerlens.ai/blog/stop-building-your-own-llm-evaluation-framework] A counterpoint from vendors: an in-house build takes 3–6 months and more than $500k. That argues for buying tooling, not for buying experts.
- **Integration with traces and product data.** Evals derive from production traces (PostHog's Traces Hour, Zapier's failure-to-eval tool, Canva's production sampling), and that data stays inside.

## 3. What remains unserved
| Sub-problem | Served? |
|---|---|
| Eval tooling, tracing, datasets, CI | **Fully served**, and now commoditizing (Langfuse open source, Datadog bundling). |
| Judge calibration *workflow* | **Served as a feature** (LangSmith Align Evals, Ragas align, Hamel's validate-evaluator skill). |
| Expert ground truth in generic domains (law, medicine, finance, code) | **Served and well funded**: Scale Enterprise Evals, Snorkel EDaaS, Mercor, Surge, Vals. |
| Ground truth in *the customer's* definition of quality | **Not outsourceable by design.** This is why builds stay in-house. It is the gap, but a vendor can't fill it. |
| **Re-certification on model upgrade** (re-validate prompts and judges when the app model *or the judge model* changes, with minimal new expert labels) | **Partly unserved.** Tools re-run evals, but nobody sells "certify this upgrade with a statistical guarantee in 48 hours using ≤50 new expert labels". Enterprise posts describe re-validation taking weeks and needing compliance sign-off. [airia.com/blog/the-change-management-problem...; ud.hk/.../model-deprecation-enterprise-risk-2026-07-31] Model deprecations (e.g., OpenAI Evals sunset) force migrations. |
| A contractual agreement SLA | **Unclaimed**, but no buyer was found asking for one. |

## 4. Buyer count and spend
- **Buyers.**
  - About 1,000–3,000 AI-product companies and AI-native vendors with ≥10 AI engineers [E].
  - About 300–800 of them operate in expert domains (legal, health, finance, security, education) where expert labels are costly [E].
  - Adding enterprises building internal agents takes the pool into the tens of thousands, but those buyers are being served by Scale, Snorkel, OpenAI Frontier and Cisco/Datadog.
- **Market spend.**
  - Analyst figure: LLM observability was about $2.7B in 2026 (from $2.0B in 2025), forecast at $9.3B by 2030. Low reliability. [ecosistemastartup.com; marktechpost.com/2026/08/09/...]
  - The leaders' ARR is small: Braintrust about $36M (2025) and LangChain $12–16M (mid-2025). Actual tooling spend is therefore well under $1B.
- **The wedge's slice.**
  - SYNTHESIS's "30–60% of AI engineering time, $5–10M a year" is mostly product iteration, not outsourceable labeling.
  - The source files themselves estimate the pure eval-upkeep and expert-labeling slice at 0.5–2 FTE at Shopify and 5–10 FTE-equivalent at Notion. That is about **$0.1–1.5M a year per company** [E].
  - A 70% cut gives an ACV of about $50–250k [E]. Across 300–800 domain-heavy buyers, the wedge ceiling is about **$25–150M ARR**. That is a services-margin business, not a $10B one.

## Re-score (10 criteria)

| Criterion | SYNTHESIS | Re-score | Justification |
|---|---|---|---|
| Pain today | 8 | **8** | Confirmed: Notion's 90% figure, Vanta, Shopify, Canva teams, and weeks of re-validation per migration. |
| Dollars attached | 9 | **6** | The outsourceable slice (expert labeling and re-validation) is $0.1–1.5M per company, not $5–10M. |
| Headcount attached | 9 | **6** | 0.5–10 FTE of upkeep. The rest is core product work that stays in-house. |
| Growth rate of pain | 8 | **7** | Model cadence drives it, but tooling (auto-scorers, Align Evals) is absorbing part of it. |
| Ease of finding buyers | 8 | **7** | Visible via eval talks and job posts, but already courted by Braintrust, LangSmith, Scale and Snorkel. |
| 30-day pilotability | 6 | **6** | Measurable (agreement and hours saved), but it needs customer expert labels first. |
| Existing internal builds | 10 | **6** | Hybrid: companies buy the backbone and build only the taste layer, which resists outsourcing. |
| Competitive opening | 5 | **3** | Tooling has consolidated (Cisco, ClickHouse, CoreWeave, OpenAI, Anthropic). Expert-eval services come from Scale, Snorkel ($375M run rate), Mercor and Vals. Calibration ships as a LangSmith feature. |
| Expansion potential | 8 | **6** | The "quality system of record" is already claimed by Braintrust, LangSmith, Arize and Datadog. |
| $10B potential | 7 | **4** | The wedge ceiling looks like $25–150M ARR at services margins. Platforms and labs absorb the category. |
| **Average** | **7.8** | **5.9** | |

## Sharpest surviving wedge
**"Upgrade certification": a 48-hour, statistically bounded re-certification of an existing AI feature when the app model or the judge model changes.**
- **Buyers:** regulated-domain AI vendors (legal, health, finance, security) whose customers or compliance teams need a signed sign-off.
- **Mechanism:** sit on top of the customer's existing Braintrust or LangSmith data, with no new platform.
  - Use active sampling and disagreement mining to request only the ~30–50 expert labels that matter, from the customer's own experts.
  - Re-fit the judge, then issue a certificate with confidence intervals and a list of regressions.
- **Why it might survive:** it is narrow, recurring (every 1–3 months), tied to an event (model release or deprecation date), and the incumbents' self-serve tooling doesn't sell it as an outcome.
- **Why it is still weak:**
  - Braintrust or LangSmith could ship it as a feature within a quarter.
  - The expert-label step is still the customer's bottleneck.
  - Revenue is per-event and services-flavored.
- **Estimated score:** ~6.3, unverified.

## Verdict
**It drops from 7.8 to about 5.9.** F-B found a real, widely felt pain, but SYNTHESIS read it wrongly in three ways:
1. **"Built in-house" means "built the taste layer on top of a vendor".** Taste is exactly what can't be bought.
2. **The tooling and expert-data markets already hold more than $5B of combined valuation**, and incumbents have been acquired into platforms (Cisco, ClickHouse, CoreWeave, OpenAI, Anthropic). The expert-eval service the wedge describes is already sold by Scale, Snorkel, Mercor and Vals.
3. **The outsourceable dollars are about 10–20% of the "30–60% of AI engineering time" headline.**

Round 32 still has no finalist at or near 8.5 after verification. F-B ranks below the residual F-A estimate (~7, in-session runtime abuse).
