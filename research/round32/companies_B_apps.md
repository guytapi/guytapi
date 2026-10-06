# Round 32 — Companies B: AI applications / customer-facing agents

Scope: Sierra, Decagon, Intercom (Fin), Glean, Harvey, Hebbia, Perplexity (enterprise), ElevenLabs, Writer, Clay.
Method: 20 WebSearch queries (Oct 2026), snippets only (no page fetch). Evidence window mostly Apr 2025 – Sep 2026.
Convention: **[E]** = estimate/inference by researcher; everything else attributed to a cited source. Evidence strength: S = first-party (company blog/job post/exec on record), M = credible third party, W = aggregator/inference.

---

## 1. Sierra
1. **Changed:** Scaled to ~$10B valuation; agents for Sonos, WeightWatchers, SiriusXM serving millions of consumers/month; added voice; acquired OPERA TECH (Tokyo) Mar 2026 (sierra.ai/blog/agent-development-life-cycle; sierra.ai/jp/blog/engineering).
2. **Hiring:** ~20 variants of "Software Engineer, Agent" / "Agent Engineer, TLM" across SF, NY, London, Singapore, Tokyo, Paris, Madrid, Munich, Toronto, Sydney (zerogtalent.com blog on Sierra hiring; 4dayweek.io Agent Engineer TLM post). Role "owns the full Agent Development Life Cycle, from pilots and customer discovery through deployment, evaluation, and iteration." (S)
3. **Internal platforms:** Agent SDK (declarative skills + deterministic guardrails), supervisory LMs, "Agent Development Life Cycle" (ADLC): inspect real conversations → turn failures into tests → release → adapt to new channels (sierra.ai/blog/agent-development-life-cycle; AI Engineer talk ai.engineer/talks/...agent-development-life-cycle). τ-bench / τ²-bench simulated-user eval framework incl. full-duplex voice (sierra.ai/blog/benchmarking-ai-agents). "Ghostwriter" platform referenced (zerogtalent).
4. **Human ops:** FDEs "working side by side with each new customer to hand-build AI agents" (S). Conversation review → test authoring is manual loop.
5. **Architecture beyond SaaS:** per-customer agent codebases; simulated-user regression suites; supervisory models; voice + chat parity.
6. **Scales linearly with:** customers (FDE pods per logo), channels per customer, failure cases → tests, model upgrades × customers × test suites.
7. **Complaints:** τ-bench finding that simple function-calling/ReAct agents "perform poorly on even relatively simple tasks" — i.e., reliability requires bespoke harness (S).
8. **Built internally:** a full agent SDLC (SDK + simulation + test harness + supervisors) — a research-lab-grade eval stack.
9. **Tags:** forward-deployed-implementation, eval-pipelines, simulated-user-testing, regression-on-model-upgrade, customer-specific-config, conversation-review-to-test.
- *PEOPLE COST [E]:* ~1–3 agent engineers per enterprise logo at $250–400k loaded → $0.5–1M/logo/yr in delivery headcount. *SCALING LAW:* linear in logos × channels.

## 2. Decagon
1. **Changed:** ARR ~$44M end-2025 → ~$100M Jul 2026; 100+ new enterprise logos in 2025 (standout.work/joinrise snippet, M).
2. **Hiring:** 137 open roles, 55 "Engineer" titles: 29 core product/research vs **25 customer-facing deployment** (standout.work/blog/decagon-engineering-jobs-apply, M). Repeated: Agent Product Manager / Senior Agent PM / Manager of Agent PMs ("operationalize playbooks for building and scaling enterprise AI agents"), Engineering Manager Agent Product ($280–430k), Deployment Strategist, TPM for "end-to-end delivery of enterprise AI agent implementations" (jobs.accel.com, indexventures.com, choppingblock.ai — S).
3. **Internal platforms:** Agent Operating Procedures (AOPs) — natural language compiled to validated workflows (Apr 2025, decagon.ai/blog/why-we-built-aop); "The future of AI agents is test-driven" (Jul 2025, decagon.ai/blog/the-future-of-ai-agents-is-test-driven); unified chat/voice/email platform.
4. **Human ops:** AOPs explicitly built to remove "back-and-forth with external professional services to implement critical workflows" — confirms implementation bottleneck was services-heavy (S). Agent PMs per account.
5. **Architecture:** NL→workflow compiler with validation; actions (refunds, identity verification, subscription changes) against each customer's backend.
6. **Scales linearly with:** logos (deployment engineers ≈ 45% of eng hiring), SOPs per customer, backend actions/integrations per customer.
7. **Complaints:** (none surfaced in snippets; internal framing of services back-and-forth is the complaint).
8. **Built internally:** AOP compiler + test-driven agent harness.
9. **Tags:** forward-deployed-implementation, customer-specific-config, sop-to-agent-translation, eval-pipelines, integration-maintenance.
- *PEOPLE COST [E]:* 25 deployment-engineer openings × ~$300k loaded ≈ $7.5M/yr incremental, for ~100 net-new logos/yr → ~$75k delivery cost per new logo.

## 3. Intercom (Fin)
1. **Changed:** Fin resolution rate ~30% → ~70%; priced $0.99 per resolution (eesel.ai, gleap.io pricing guides 2025–26; Chain of Thought podcast w/ Fergal Reid).
2. **Hiring:** AI group led by Chief AI Officer Fergal Reid; fin.ai/research publishes ML work (no specific job counts surfaced).
3. **Internal platforms:** custom reranker on ModernBERT-large beating Cohere Rerank v3.5, **80% lower reranking cost** (fin.ai/research/how-we-built-a-world-class-reranker-for-fin, S); fine-tuned retrieval model; "every component in the Fin AI Engine is a custom model fine-tuned on hundreds of millions of real support interactions" (S). Replaced GPT for a summarization task costing **$250K/month** with fine-tuned Qwen 14B, saving "almost all of it" (chainofthought.transistor.fm episode, S — exec on record).
4. **Human ops:** gains came from "surrounding systems (custom re-rankers, retrieval models, query canonicalization), not the core frontier LLM" — ongoing ML team work per component.
5. **Architecture:** per-resolution pricing means inference COGS directly hits gross margin per outcome → must own model routing / self-hosting.
6. **Scales linearly with:** conversations (inference spend), resolutions (revenue), number of pipeline stages × models to re-validate on each upgrade.
7. **Complaints:** customers complain per-resolution pricing is unpredictable (qualimero.com "Why per-resolution fails", 2025, W).
8. **Built internally:** in-house fine-tuned reranker, retriever, summarizer, self-hosted GPU inference — an applied-ML org most SaaS can't afford.
9. **Tags:** inference-cost-routing, self-hosted-model-distillation, eval-pipelines, regression-on-model-upgrade, outcome-pricing-margin.
- *INFRA COST:* $250K/mo for one task (S) → $3M/yr; reranker vendor cost cut 80% (S). *SCALING LAW:* linear in conversation volume; savings require dedicated ML team [E: 10–30 ML engineers].

## 4. Glean
1. **Changed:** pitch shifted from enterprise search to "AI workforce platform"/agents (2025–26) (benchlm.ai, openaitoolshub, W).
2. **Hiring:** not surfaced in snippets.
3. **Internal platforms:** 275+ connectors (native, push/Indexing API, partner-built); permissions-aware index intersecting results with per-source permission snapshots at query time; event-driven indexing (~60s) but full crawls 6h–28 days by connector; "missed deletion events wait for the next full crawl" (benchlm.ai / docs.glean.com/connectors/key-terms, M). Single-tenant / Cloud-Prem deployments.
4. **Human ops:** connector configuration per customer; Indexing API for custom/self-hosted systems implies customer/partner-built pushes (tray.ai connector listing).
5. **Architecture:** must mirror ACLs of 100s of SaaS systems, keep fresh, and enforce at retrieval and agent-action time; per-customer isolated deployment.
6. **Scales linearly with:** connectors × customers (each upstream API change), documents indexed, permission changes, single-tenant deployments to operate.
7. **Complaints:** freshness gaps/stale deletions (benchlm.ai, M); competitors (Unblocked, "Is Glean good enough") argue code/eng knowledge coverage gaps (W).
8. **Built internally:** a 275-connector permission-synced crawler fleet + per-tenant cloud ops.
9. **Tags:** knowledge-ingestion-permissions, integration-maintenance, index-freshness, single-tenant-ops.
- *INFRA/PEOPLE [E]:* connector maintenance likely 1 engineer per ~10–20 connectors → 15–30 engineers just on connector upkeep; scales with SaaS API churn.

## 5. Harvey
1. **Changed:** ~$11B valuation, $760M raised in funding blitz; "12x token surge" (zerogtalent.com Harvey posts 2026, W); multi-model (Anthropic via Bedrock, Google via Vertex) added 2025 (harvey.ai/blog/expanding-harveys-model-offerings, S).
2. **Hiring:** ~180 legal engineers (former practicing lawyers) — one in every deployment (SaaStr, 2026, M); "Senior Full Stack Software Engineer, Forward Deployed" (builtin.com, S); Head of AMER Legal Engineering roles in NY/Chicago/Dallas/SF at $400–450k (zerogtalent); Vault PM with "permissioning models that mirror law-firm ethics walls" (S via job snippet). Bloomberg Law: hiring "all sorts of lawyers".
3. **Internal platforms:** BigLaw Bench proprietary eval with rubrics for answer quality + source reliability; every model tested through it; human preference + LLM-judge multi-layer evals with lawyers in loop (harvey.ai/blog/tag/technical; zenml LLMOps database; artificiallawyer.com 2025-08-08 "GPT-5 tops BigLaw Bench").
4. **Human ops:** FDE/legal-engineer pods (PM + 1–2 lawyers + SWEs) embed 6–9 months inside a firm; rebuild firm-specific knowledge bases, house style, precedent vault, confidentiality walls (getperspective.ai FDE playbook 2026, W/M).
5. **Architecture:** ZDR with model providers, data-residency choice, ethical walls per matter, multi-provider routing with same guarantees.
6. **Scales linearly with:** firms/deployments (legal engineer per deployment), matters (permission walls), models added × eval rubric runs (expert-graded).
7. **Complaints:** cost of lawyer-graded evals; (snippets did not surface customer complaints).
8. **Built internally:** domain benchmark graded by lawyers + ~180-person legal engineering deployment force.
9. **Tags:** forward-deployed-implementation, eval-pipelines, expert-human-eval, knowledge-ingestion-permissions, ethical-walls-matter-permissions, data-residency-zdr, regression-on-model-upgrade.
- *PEOPLE COST [E]:* 180 legal engineers × ~$300k loaded ≈ **$54M/yr** in deployment headcount (count from SaaStr; comp estimate). *SCALING LAW:* linear in deployments.

## 6. Hebbia
1. **Changed:** processes **>250B tokens/month** (hebbia.com/blog/how-hebbia-approaches-token-efficiency-for-financial-ai, S); Matrix positioned for millions-to-billions of documents.
2. **Hiring:** not surfaced.
3. **Internal platforms:** token-efficiency system: (a) fewer tokens per problem, (b) cheaper cost per token (model routing), (c) avoid recomputation via caching; selective component attention instead of fixed retrieval limits (S).
4. **Human ops:** not surfaced; finance customers imply heavy onboarding of deal-room docs [E].
5. **Architecture:** fan-out of LLM calls across every cell of a doc×question matrix — compute explodes multiplicatively.
6. **Scales with:** documents × questions × re-runs (multiplicative, not linear).
7. **Complaints:** pricing opacity (eesel.ai Hebbia pricing, W).
8. **Built internally:** token budget optimizer + caching layer + model router.
9. **Tags:** inference-cost-routing, llm-caching, doc-fanout-compute.
- *INFRA COST [E]:* 250B tok/mo at blended $1–3/M tokens ≈ $250k–750k/month; a 30% efficiency gain is worth $1–3M/yr.

## 7. Perplexity (Enterprise)
1. **Changed:** Enterprise Pro: SOC 2 Type II, GDPR, PCI DSS; Security Hub admin console; Connectors (Google Drive, OneDrive, SharePoint); org-wide Internal Knowledge Search (perplexity.ai hub blog "How Perplexity Enterprise Pro keeps your data secure", S).
2. **Hiring:** not surfaced.
3. **Internal platforms:** Security Hub (permissioning for uploads/downloads, sharing, which users may connect data sources).
4. **Human ops:** enterprise security reviews — third parties (strac.io "Is Perplexity safe") show buyers' security-questionnaire scrutiny (W).
5. **Architecture:** consumer product retrofitted with admin governance, connector permissions, data-retention controls.
6. **Scales with:** enterprise accounts (security reviews), connectors, admin policy surface.
7. **Complaints:** data-leak/shadow-AI concerns from security vendors (W).
8. **Built internally:** compliance program + governance console.
9. **Tags:** enterprise-security-questionnaires, knowledge-ingestion-permissions, admin-governance-controls.

## 8. ElevenLabs
1. **Changed:** ElevenAgents (voice + chat agents) "with the integrations, testing, monitoring, and reliability necessary to deploy… at scale."
2. **Hiring:** "Forward Deployed Engineer – Software Engineer" reposted region-by-region through 2026: US/DE/PL/UK (Jan 14), LATAM (Jul 20), Canada, Sweden, Netherlands (Aug 11), Poland (Aug 18) (choppingblock.ai, remowork.life listings, S).
3. **Internal platforms:** Agents Testing — structured simulations for tool calls, human transfers, workflows, guardrails; CI/CD integration; tests auto-generated from past conversations (elevenlabs.io/blog/tests-for-elevenlabs-agents, S).
4. **Human ops:** FDEs per region; customers write/curate test scenarios.
5. **Architecture:** real-time voice latency + tool calling + handoff to humans; regression testing for non-deterministic dialog.
6. **Scales with:** deployments per region (FDE per geo), conversations, test scenarios × prompt changes.
7. **Complaints:** third-party voice testing vendors (cekura.ai, 2026-04) publish guides for testing ElevenLabs agents → native coverage seen as insufficient (W).
8. **Built internally:** voice-agent simulation/test harness.
9. **Tags:** forward-deployed-implementation, simulated-user-testing, eval-pipelines, conversation-review-to-test, agent-observability.

## 9. Writer
1. **Changed:** AI HQ (Apr 2025) — hub to build, activate, supervise agents; Palmyra X5 (1M ctx, $0.60/$6 per M tokens) (businesswire 2025-04-28, S); Action Agent and agentic upgrades Nov 2025 (siliconangle 2025-11-18).
2. **Hiring:** not surfaced in snippets.
3. **Internal platforms:** own full-stack foundation models (Palmyra family), Agent Builder shared by IT + business, "dynamic model delegation", built-in RAG.
4. **Human ops:** "unites IT and business teams" — agent supervision/approvals central to pitch [E: manual governance remains].
5. **Architecture:** owns model training + serving to control cost/latency; agent supervision layer.
6. **Scales with:** agents per enterprise (supervision), model training cycles.
7. **Complaints:** not surfaced.
8. **Built internally:** proprietary LLM training stack — extreme version of "own the model to own margin".
9. **Tags:** inference-cost-routing, self-hosted-model-distillation, agent-governance-supervision, customer-specific-config.

## 10. Clay
1. **Changed:** $100M Series C Aug 2025 at $3.1B (CapitalG); later $1.25B-referenced raise headlines (cmswire); 130+ data providers; Claygent used daily by 30% of customers, **500K+ research tasks/day** (coldoutbound.com, M).
2. **Hiring:** invented the "GTM Engineer" title — customer-side role required to operate it (amplemarket, M).
3. **Internal platforms:** waterfall enrichment across 130+ providers; credit metering; BYO API keys.
4. **Human ops:** customers' GTM engineers maintain 400+ tables (largest user ran 37M rows/week); community threads on slow Claygent batches (800 rows/30 min; 40k rows) and batching (community.clay.com, S-community).
5. **Architecture:** shared multi-tenant LLM rate limits — engineering joke "50% for Eric and 50% for the masses" (coldoutbound.com, M); requires 450K TPM for Claygent.
6. **Scales with:** rows × enrichment steps × providers; LLM tokens per research task; provider API quotas.
7. **Complaints:** non-linear credit costs, fragile Salesforce/HubSpot integrations (zoominfo pipeline review; syncgtm 2026, W/M); slow Claygent at volume (S-community).
8. **Built internally:** provider-aggregation + credit metering + rate-limit pooling across tenants.
9. **Tags:** inference-cost-routing, llm-rate-limit-pooling, integration-maintenance, usage-metering-credits, customer-side-ops-headcount.

---

## Cross-cutting notes
- **Deployment headcount is the dominant hidden cost.** Sierra (~20 agent-eng req variants), Decagon (25/55 eng openings customer-facing), Harvey (~180 legal engineers), ElevenLabs (FDE reposted in ≥8 geos). Decagon's AOP launch explicitly targets professional-services back-and-forth.
- **Every agent company built its own eval/simulation harness**: Sierra (τ-bench, ADLC), Decagon (test-driven agents), Harvey (BigLaw Bench), ElevenLabs (Agents Testing), Intercom (component evals for custom models). Common loop: production conversation → failure → test case → CI gate → model/prompt change.
- **Inference COGS forces in-house ML** where pricing is per outcome/usage: Intercom ($250K/mo → near-zero on one task; reranker −80%), Hebbia (250B tok/mo optimizer), Writer (own models), Clay (pooled rate limits).
- **Permission mirroring** is a separate cluster: Glean, Harvey (ethical walls), Perplexity (connector governance).

## Pain-tag summary table

| pain tag | companies showing it | which built internally | evidence strength |
|---|---|---|---|
| forward-deployed-implementation | Sierra, Decagon, Harvey, ElevenLabs, (Writer [E]) | Sierra (ADLC/SDK), Decagon (AOPs to cut services), Harvey (legal-eng pods) | S (job posts, exec/SaaStr counts) |
| eval-pipelines | Sierra, Decagon, Intercom, Harvey, ElevenLabs | all five | S |
| simulated-user-testing | Sierra, ElevenLabs, Decagon | Sierra (τ-bench), ElevenLabs (Agents Testing), Decagon | S |
| conversation-review-to-test | Sierra, ElevenLabs, Decagon | Sierra, ElevenLabs | S |
| regression-on-model-upgrade | Sierra, Intercom, Harvey, (Decagon) | Harvey (BigLaw Bench per model), Sierra, Intercom | S/M |
| inference-cost-routing | Intercom, Hebbia, Writer, Clay, (Harvey multi-model) | Intercom, Hebbia, Writer | S |
| self-hosted-model-distillation | Intercom, Writer | Intercom (Qwen 14B, ModernBERT), Writer (Palmyra) | S |
| customer-specific-config | Sierra, Decagon, Harvey, Writer | Decagon (AOP), Sierra (SDK) | S/M |
| sop-to-agent-translation | Decagon, Sierra, Harvey | Decagon | S |
| knowledge-ingestion-permissions | Glean, Harvey, Perplexity | Glean, Harvey (Vault walls), Perplexity (Security Hub) | S/M |
| integration-maintenance | Glean, Decagon, Clay | Glean (275 connectors), Clay (130 providers) | M |
| index-freshness | Glean | Glean | M |
| enterprise-security-questionnaires | Perplexity, Harvey, Glean | Perplexity (SOC2/Hub) | M/W |
| data-residency-zdr | Harvey, Glean (single-tenant) | Harvey | S/M |
| expert-human-eval | Harvey, (Sierra conversation review) | Harvey | S |
| agent-observability | ElevenLabs, Sierra (supervisory LMs) | both | M |
| agent-governance-supervision | Writer, Sierra, Perplexity | Writer (AI HQ), Sierra | M |
| llm-rate-limit-pooling | Clay, Hebbia [E] | Clay | M |
| llm-caching / doc-fanout-compute | Hebbia | Hebbia | S |
| outcome-pricing-margin | Intercom, Sierra (outcome pricing [E]) | Intercom | M |
| usage-metering-credits | Clay | Clay | M |
| customer-side-ops-headcount | Clay (GTM engineers), Glean [E] | — | M |

Strongest clusters meeting the ≥5 companies / ≥2 built-internally filter within this set: **eval-pipelines (5/5 built)**, **forward-deployed-implementation (4–5, 3 built)**, **inference-cost-routing (4–5, 3 built)**. Near-miss: knowledge-ingestion-permissions (3 here; likely merges with infra-company files).
