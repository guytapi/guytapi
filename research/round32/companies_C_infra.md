# Round 32 — Companies C: AI infrastructure

Scope: Modal, Baseten, Together AI, Fireworks AI, OpenRouter, LangChain, Pinecone, Browserbase, E2B, Temporal, Neon.
Method: 20 web searches (snippets only; WebFetch not used). Date: 2026-10-06. `[E]` = estimate/inference, not sourced. `[S#]` = source list at bottom.

Pain-cost legend per pain: PEOPLE / INFRA / FREQ / SCALING / CURRENT.

---

## 1. Modal (serverless GPU compute)
1. **Changed:** $300M+ ARR, ~5x growth in a year; $355M Series C at $4.65B [S13]. >20,000 concurrent GPUs, 4M cloud instances launched; GPU sources across AWS/GCP/Azure/OCI, expanded 5→13 infra providers [S1][S2]. Clusters GA (gang scheduling, RDMA) [S1].
2. **Hiring:** Compute Strategy & Operations Lead ($200–300K) — own GPU/CPU procurement across hyperscalers/neoclouds/DC operators, negotiate reserved/spot contracts, MSAs, DPAs [S17]. Support Engineer (repeated postings, 4 cities, $120–220K, "engineering role closest to customers") [S13].
3. **Internal platforms:** GPU reliability system (Dec 2025): instance-type qualification, CI-validated machine images, boot checks, passive+active GPU healthchecks [S1]; idle-GPU buffers, lazy-loading container FS, CPU+GPU memory snapshotting [S1].
4. **Human ops:** contract negotiation per provider (13 providers ⇒ 13 sets of MSAs/DPAs/order forms) [S17]; customer debugging of CUDA/driver/low-level issues by engineers [S13].
5. **Non-SaaS architecture:** real-time arbitrage of GPU price/availability across 13 clouds; detect silently-bad GPUs (Xid errors, degraded NVLink) before customer workloads land.
6. **Scales linearly with:** # providers × GPU SKUs × regions (qualification matrix); # GPUs (bad-node rate); # customers with exotic stacks (support tickets).
7. **Complaints:** cold starts / peak-to-average demand ratio drives idle buffer cost [S1].
8. **Built internally:** multi-cloud GPU scheduler + fleet health system — not affordable for a normal company.
9. **Tags:** `gpu-capacity-procurement`, `multi-cloud-gpu-ops`, `gpu-fleet-health`, `cold-start-idle-buffer`, `technical-support-engineering`
- *gpu-fleet-health* — PEOPLE: 3–6 infra eng FTE [E]; INFRA: 1–3% of fleet out at any time ⇒ at 20K GPUs ≈ 200–600 GPUs ≈ $4–13M/yr idle/lost [E, at ~$2.5/GPU-hr]; FREQ: continuous; SCALING: linear in GPUs × providers; CURRENT: built in-house.
- *gpu-capacity-procurement* — PEOPLE: dedicated lead + finance/legal support, $200–300K+ base [S17]; INFRA: overcommit/underutilization of reserved contracts is the largest cost line [E]; FREQ: weekly/monthly; SCALING: linear in providers; CURRENT: humans + spreadsheets [E].

## 2. Baseten (inference platform)
1. **Changed:** Series F; Multi-Cloud Capacity Management (MCM) now "thousands of GPUs across 20+ clouds and regions"; Cloud / Self-hosted / Hybrid modes on one stack [S3][S4].
2. **Hiring:** Global Capacity Lead and Global Capacity Manager (repeat) — secure "multi-million dollar GPU clusters", run H100/B200 pods, "air traffic control", maintenance, reserve dedicated capacity for largest enterprise customers [S4][S17].
3. **Internal platforms:** MCM — unified control plane across clouds, single pane of glass [S3].
4. **Human ops:** per-enterprise capacity reservations negotiated by humans; lifecycle tracking of GPU pods [S17].
5. **Non-SaaS architecture:** same inference stack must run in Baseten cloud, customer VPC, and hybrid burst; SOC2/HIPAA/GDPR data residency per region [S3].
6. **Scales linearly with:** # enterprise customers demanding dedicated capacity or self-host; # clouds/regions.
7. **Complaints:** (none surfaced in snippets).
8. **Built internally:** MCM (multi-cloud GPU control plane) + BYOC/self-hosted packaging.
9. **Tags:** `gpu-capacity-procurement`, `multi-cloud-gpu-ops`, `enterprise-deploy-byoc`, `data-residency-compliance`
- *enterprise-deploy-byoc* — PEOPLE: 2–5 eng per major self-host variant + FDE per large account [E]; INFRA: low; FREQ: per enterprise deal; SCALING: linear in enterprise logos × cloud targets; CURRENT: in-house.

## 3. Together AI (AI cloud: inference + GPU clusters)
1. **Changed:** sells both serverless inference and dedicated GPU clusters; many new model endpoints (status pages per model: GLM-5.x, DeepSeek V4) [S19].
2. **Hiring:** Senior DevOps Eng — orchestration over large fleets of distributed GPU hardware, "reliability, availability, serviceability, and profitability" [S5]; Technical Support Engineer, GPU Clusters (US weekends) — monitor cluster health, proactively tell customers about thermal throttling, BMC failures, missing GPUs, NVLink/InfiniBand degradation [S5]; GPU Cluster Resource Scheduling & Optimization Engineer [S5].
3. **Internal platforms:** not surfaced; inferred custom scheduling + health telemetry [E].
4. **Human ops:** **weekend human shifts to watch GPU hardware health and email customers** — strongest "should not exist" signal in this set [S5].
5. **Non-SaaS architecture:** hardware-level fault detection (BMC, IB fabric) surfaced into customer comms; per-model endpoint SLOs.
6. **Scales linearly with:** # GPU nodes sold as clusters (hardware faults); # model endpoints (each its own status component) [S19].
7. **Complaints:** MTTR ~66 min when incidents acknowledged [S19].
8. **Built internally:** cluster scheduler/health tooling [E].
9. **Tags:** `gpu-fleet-health`, `multi-cloud-gpu-ops`, `gpu-capacity-procurement`, `technical-support-engineering`, `model-endpoint-sprawl`
- *gpu-fleet-health (customer comms)* — PEOPLE: 24/7 coverage ≈ 5–8 support FTE ≈ $1–1.5M/yr [E]; INFRA: SLA credits [E]; FREQ: daily hardware events at multi-thousand-GPU scale [E]; SCALING: linear in nodes; CURRENT: humans watching dashboards + manual customer notices [S5].

## 4. Fireworks AI (inference)
1. **Changed:** ~$305M ARR end-2025 → $800M ARR May 2026; >10,000 customers by Oct 2025; $4B Series C [S6][S18]; reported 140B+ tokens/day (other source claims 43T/day — inconsistent) [S6].
2. **Hiring:** 45 open roles; 4 Forward Deployed / AI Field Engineer roles (AI Natives, Enterprise, Microsoft Foundry) [S18]; Data Platform Engineer [S18].
3. **Internal platforms:** optimized serving stack, fine-tune + serve; runs on Crusoe and others [S6].
4. **Human ops:** FDEs per segment and per cloud marketplace (Foundry) — channel-specific deployment work [S18].
5. **Non-SaaS architecture:** per-customer fine-tuned model hosting (LoRA multiplexing) [E]; 99.99% uptime claim [S6].
6. **Scales linearly with:** # enterprise customers (FDE time); # cloud marketplaces; # fine-tuned variants [E].
7. **Complaints:** none surfaced.
8. **Built internally:** custom inference engine, multi-provider GPU sourcing.
9. **Tags:** `gpu-capacity-procurement`, `enterprise-deploy-byoc`, `forward-deployed-eng`, `cloud-marketplace-integration`, `usage-metering-billing`
- *forward-deployed-eng* — PEOPLE: ~$180K median FDE [S18] × N accounts; FREQ: per deal; SCALING: linear in enterprise logos; CURRENT: humans.

## 5. OpenRouter (LLM router / marketplace)
1. **Changed:** 5T → 25T tokens/week in ~6 months, later >90T/week; $113M Series B; $1.3B valuation; Stripe talks reported [S7][S8]. Team ~19–50 [S8].
2. **Hiring:** small; platform/product/applied AI engineers [S8].
3. **Internal platforms:** provider router — health-aware (30s outage window), inverse-square-price weighting, automatic fallback [S9].
4. **Human ops:** credit disputes; edge cases where 429/partial outputs still consume credits [S9].
5. **Non-SaaS architecture:** normalize 300+ models × dozens of providers; detect providers returning HTTP 200 with `content: null` or missing usage object [S9]; reconcile billing against each upstream's usage report.
6. **Scales linearly with:** # providers × # models (normalization + quirks); tokens (billing reconciliation); prepaid credit purchases (fraud/chargebacks) [E].
7. **Complaints:** 3 outages of 35–50 min Aug 2025–Feb 2026, no credit regime; billing edge cases [S9].
8. **Built internally:** real-time provider health/routing + cross-provider metering — the core product.
9. **Tags:** `inference-cost-routing`, `provider-quirk-normalization`, `usage-metering-billing`, `billing-reconciliation`, `abuse-fraud` [E — prepaid credits + stolen cards typical; not sourced]
- *billing-reconciliation* — PEOPLE: 1–3 FTE [E]; INFRA: revenue leakage 0.5–2% on pass-through tokens [E]; FREQ: per request; SCALING: linear in providers × tokens; CURRENT: in-house.

## 6. LangChain (LangSmith + LangSmith Deployment)
1. **Changed:** LangGraph Platform GA, renamed LangSmith Deployment (Oct 2025); ~400 companies deployed agents in beta period [S10].
2. **Hiring:** not surfaced in snippets.
3. **Internal platforms:** ClickHouse as primary trace/feedback store; "SmithDB"; self-host scaling docs + cluster sizing calculator; LangSmith-managed ClickHouse for self-hosters [S11].
4. **Human ops:** sizing self-hosted clusters per customer (a dedicated calculator exists ⇒ recurring support load) [S11].
5. **Non-SaaS architecture:** ingest every LLM/tool span (trace volume ≫ request volume); long-running stateful agent runtime; cloud / hybrid (SaaS control + self-host data) / full self-host [S10].
6. **Scales linearly with:** agent steps/tool calls (trace rows); # self-hosted enterprise installs.
7. **Complaints:** ClickHouse ops burden pushed onto self-hosters (hence managed-ClickHouse beta) [S11].
8. **Built internally:** high-volume trace store + hybrid deployment plane.
9. **Tags:** `agent-observability`, `trace-storage-cost`, `enterprise-deploy-byoc`, `agent-runtime-state`
- *trace-storage-cost* — PEOPLE: 2–4 data infra FTE [E]; INFRA: storage ∝ spans; agent with 20–50 spans/run ⇒ 20–50x rows vs request logs [E]; FREQ: continuous; SCALING: super-linear with agent depth; CURRENT: in-house ClickHouse.

## 7. Pinecone (vector DB)
1. **Changed:** Dedicated Read Nodes GA (late 2025, "up to 97% lower costs" for large workloads); BYOC preview on AWS; 2025-10 API [S12].
2. **Hiring:** not surfaced.
3. **Internal platforms:** serverless rewrite (reads/writes/storage split, blob as source of truth); billing rebuilt on 4 meters (RU, WU, GB-month, egress) [S12].
4. **Human ops:** customer migrations between pods/serverless/DRN; cost-surprise support [E].
5. **Non-SaaS architecture:** multi-tenant ANN with cold/warm tiers; BYOC in customer AWS with vendor ops.
6. **Scales linearly with:** # namespaces/tenants (agent-memory pattern) [E]; # BYOC accounts.
7. **Complaints:** unpredictable serverless bills at scale (implied by DRN positioning) [S12].
8. **Built internally:** usage metering for 4 dimensions; BYOC control plane.
9. **Tags:** `usage-metering-billing`, `cost-predictability`, `enterprise-deploy-byoc`, `multi-tenant-isolation`

## 8. Browserbase (headless browsers for agents)
1. **Changed:** 50M sessions in 2025; 1,000+ companies, 20K devs; $40M Series B @ $300M; ~55 employees; "Agents" one-call API [S14][S20].
2. **Hiring:** growth + engineering roles [S20]; a dedicated **Stealth Team** maintaining a custom Chrome build [S14].
3. **Internal platforms:** custom Chromium fork (Advanced Stealth) [S14].
4. **Human ops:** **manual KYC-like vetting of large-scale use cases under internal compliance guidelines** [S20].
5. **Non-SaaS architecture:** fingerprint/IP/TLS identity management; residential proxy rotation; session isolation; anti-bot arms race [S14].
6. **Scales linearly with:** sessions (proxy cost); # new large customers (vetting); anti-bot vendor updates (stealth maintenance).
7. **Complaints:** stealth breaks at scale — identity correlation, fingerprint reuse, poor observability into session failures [S14].
8. **Built internally:** maintained Chrome fork — not affordable normally.
9. **Tags:** `abuse-fraud`, `customer-use-case-vetting`, `sandbox-infra`, `anti-bot-arms-race`, `agent-observability`
- *customer-use-case-vetting* — PEOPLE: 1–2 FTE + founder time [E]; INFRA: legal risk; FREQ: per large account; SCALING: linear in customers; CURRENT: humans + internal guidelines [S20].

## 9. E2B (code-execution sandboxes)
1. **Changed:** 1B+ sandboxes started; "94% Fortune 100" adoption; 3.5M SDK downloads/mo (Jun 2026) [S15].
2. **Hiring:** not surfaced.
3. **Internal platforms:** Firecracker microVM orchestration, <200ms boot; BYOC production on AWS+GCP, on-prem, self-hosted [S15].
4. **Human ops:** per-enterprise BYOC rollouts [E].
5. **Non-SaaS architecture:** run untrusted AI-generated code with hardware isolation at massive churn; snapshot/resume.
6. **Scales linearly with:** agent executions (sandbox starts); enterprise BYOC targets.
7. **Complaints:** none surfaced.
8. **Built internally:** microVM fleet + snapshotting.
9. **Tags:** `sandbox-infra`, `enterprise-deploy-byoc`, `abuse-fraud` [E — free compute is magnet for mining; not confirmed by search]

## 10. Temporal (durable execution, agent workloads)
1. **Changed:** 380% YoY revenue, 350% WAU, 20M installs/mo, 9.1T lifetime Cloud actions (1.86T from AI-native cos); $300M D @ $5B (Feb 2026) → reported $550M E @ $12.55B; OpenAI runs agentic workflows on it [S16].
2. **Hiring:** "hiring blitz", Seattle [S16].
3. **Internal platforms:** Cloud autoscaling >300K actions/s; absorbed unannounced 150K actions/s spikes [S16].
4. **Human ops:** capacity planning for bursty AI customers [E].
5. **Non-SaaS architecture:** agent workloads = long-lived, bursty, retry-heavy; state history per workflow.
6. **Scales linearly with:** agent steps/tool calls (actions) — metered per action.
7. **Complaints:** none surfaced.
8. **Built internally:** multi-tenant durable-execution cloud with autoscaling.
9. **Tags:** `agent-runtime-state`, `bursty-agent-capacity`, `usage-metering-billing`

## 11. Neon (serverless Postgres, now Databricks/Lakebase)
1. **Changed:** acquired by Databricks (~$1B); >80% of databases created by AI agents; $25M ARR May 2025 [S21][S22].
2. **Hiring:** n/a (inside Databricks).
3. **Internal platforms:** <500ms provisioning, branching, scale-to-zero (~5 min idle suspend); Agent Plan with two-org structure (free vs paid), 30K projects/org default [S22].
4. **Human ops:** quota raises for agent platforms; free-tier policing [E].
5. **Non-SaaS architecture:** "1,000 signups ⇒ 10,000 databases" for platforms provisioning per user [S22]; customers are machines.
6. **Scales linearly with:** agent-created projects (storage, control-plane objects), not human customers.
7. **Complaints:** idle storage of abandoned agent DBs [S22].
8. **Built internally:** scale-to-zero + Agent Plan quota system.
9. **Tags:** `agent-created-resource-sprawl`, `abuse-fraud`, `usage-metering-billing`, `multi-tenant-isolation`
- *agent-created-resource-sprawl* — PEOPLE: 1–2 FTE quota/abuse [E]; INFRA: storage for long-tail dead DBs [E]; FREQ: continuous; SCALING: ∝ agent executions (10x human signups) [S22]; CURRENT: in-house (scale-to-zero, org caps).

---

## Summary table

| Pain tag | Companies | Built internally | Evidence strength |
|---|---|---|---|
| gpu-capacity-procurement | Modal, Baseten, Together, Fireworks | Modal (13-provider arbitrage), Baseten (MCM) | **Strong** — dedicated senior job posts at Modal & Baseten [S17], Together scheduling role [S5] |
| multi-cloud-gpu-ops | Modal, Baseten, Together, Fireworks | Modal, Baseten | **Strong** — eng blog [S1], product [S3] |
| gpu-fleet-health | Modal, Together | Modal (GPU reliability system) | **Strong** — blog [S1]; Together weekend support role for HW faults [S5] |
| enterprise-deploy-byoc | Baseten, Fireworks, LangChain, Pinecone, E2B | Baseten, LangChain, Pinecone, E2B | **Strong** — 5 companies ship self-host/hybrid/BYOC [S3][S10][S12][S15] |
| usage-metering-billing | OpenRouter, Pinecone, Temporal, Neon, Fireworks | Pinecone (4-meter rebuild), OpenRouter, Temporal | Medium — product docs; pain inferred |
| billing-reconciliation | OpenRouter | OpenRouter | Medium — user complaints on credit edge cases [S9] |
| abuse-fraud | Browserbase, Neon, OpenRouter[E], E2B[E] | Browserbase (manual vetting), Neon (agent-plan caps) | Weak–medium — only Browserbase KYC sourced [S20] |
| customer-use-case-vetting | Browserbase | Browserbase (manual) | Medium [S20] |
| technical-support-engineering | Modal, Together | — (people) | **Strong** — repeated job posts [S5][S13] |
| forward-deployed-eng | Fireworks, Baseten | — (people) | Medium [S18][S17] |
| agent-observability | LangChain, Browserbase | LangChain (ClickHouse/SmithDB) | Medium [S11][S14] |
| trace-storage-cost | LangChain | LangChain | Medium [S11] |
| agent-runtime-state | Temporal, LangChain | both | Medium [S16][S10] |
| bursty-agent-capacity / cold-start-idle-buffer | Temporal, Modal | both | Medium [S16][S1] |
| inference-cost-routing | OpenRouter | OpenRouter | Strong (core product) [S9] |
| provider-quirk-normalization | OpenRouter | OpenRouter | Medium [S9] |
| sandbox-infra | E2B, Browserbase, Modal | all three | Strong (products) [S15][S14] |
| anti-bot-arms-race | Browserbase | Browserbase (Stealth Team, Chrome fork) | Medium [S14] |
| agent-created-resource-sprawl | Neon (also implied E2B, Browserbase) | Neon | Medium [S21][S22] |
| multi-tenant-isolation | Pinecone, Neon | both | Weak (inferred) |
| cost-predictability | Pinecone | Pinecone (DRN) | Medium [S12] |
| data-residency-compliance | Baseten | Baseten | Weak [S3] |
| model-endpoint-sprawl | Together | — | Weak [S19] |
| cloud-marketplace-integration | Fireworks | — | Weak [S18] |

## Sources
- [S1] Modal GPU reliability / capacity: https://letsdatascience.com/news/modal-deploys-multi-cloud-gpu-reliability-system-b2c319ed ; https://www.plushcap.com/companies/modal/blog/summaries/2026/5 ; https://runtimewire.com/article/modal-clusters-general-availability-serverless-rdma
- [S2] Modal Sacra: https://sacra.com/research/modal-labs
- [S3] Baseten MCM: https://www.baseten.co/blog/how-baseten-multi-cloud-capacity-management-mcm-powers-cloud-self-hosted-and-hybr/ ; https://www.baseten.co/products/multi-cloud-capacity-management/
- [S4] Baseten Global Capacity Lead: https://inferencejobs.com/companies/baseten/jobs/global-capacity-lead
- [S5] Together AI jobs: https://builtin.com/job/senior-devops-engineer/6467468 ; https://jobgether.com/offer/6a72a043e9f5b78658694cfd-technical-support-engineer-gpu-clusters---us-weekends ; https://talent.emcap.com/companies/together-ai-2/jobs/45135916-gpu-cluster-resource-scheduling-and-optimization-engineer
- [S6] Fireworks: https://sacra.com/research/fireworks-ai/ ; https://research.contrary.com/company/fireworks-ai
- [S7] OpenRouter growth: https://www.01net.it/openrouter-raises-113-million-capitalg-led-series-b-as-weekly-volume-explodes-to-25t-tokens/ ; https://techcrunch.com/2026/05/26/openrouter-more-than-doubles-valuation-to-1-3b-in-a-year
- [S8] OpenRouter team: https://zerogtalent.com/blog/company-culture-at-openrouter ; https://eu.36kr.com/en/p/3944714512956806
- [S9] OpenRouter routing/pitfalls: https://openrouter.ai/blog/insights/reliability-failover/ ; https://pinggy.io/blog/openrouter_production_provider_routing_pitfalls/
- [S10] LangGraph Platform: https://blog.langchain.com/langgraph-platform-ga ; https://docs.langchain.com/langgraph-platform/plans
- [S11] LangSmith ClickHouse/self-host: https://clickhouse.com/blog/langchain-why-we-choose-clickhouse-to-power-langchain ; https://docs.langchain.com/langsmith/self-host-scale ; https://enterprise-hub.langchain.com/tools/sizing-calculator ; https://docs.smith.langchain.com/self_hosting/langsmith_managed_clickhouse
- [S12] Pinecone: https://blocksandfiles.com/2025/12/01/pinecone-dedicated-read-nodes/ ; https://usagepricing.com/blueprint/pinecone ; https://theaiengineer.substack.com/p/what-does-pinecone-actually-do
- [S13] Modal support engineer: https://jobs.luxcapital.com/companies/modal-labs-2/jobs/59248694-support-engineer ; https://www.inferencejobs.com/companies/modal/jobs/support-engineer
- [S14] Browserbase stealth: https://www.browserbase.com/changelog/advanced-stealth ; https://www.browserless.io/blog/browserless-playwright-stealth-guide ; https://dev.to/cport1/how-to-detect-browser-as-a-service-scrapers-in-2025-mmk
- [S15] E2B: https://e2b.dev/enterprise.md ; https://rywalker.com/research/e2b
- [S16] Temporal: https://temporal.io/news/temporal-raises-300M-to-make-agentic-ai-real-for-companies ; https://siliconangle.com/2026/02/17/ai-agent-reliability-startup-temporal-raises-300m-funding/ ; https://pulse2.com/temporal-raises-550-million-series-e-at-12-55-billion-valuation/ ; https://zerogtalent.com/blog/temporal-s-300m-series-d-at-5b-is-fueling-a-hidden-hiring-blitz-in-agentic-ai-infrastructure-and-seattle-is-quietly-becoming-the-orchestration-capital
- [S17] Capacity job posts: https://careers.redpoint.com/companies/modal-labs-2/jobs/74795147-compute-strategy-operations-lead ; https://jobs.stripes.co/companies/baseten/jobs/70585671-global-capacity-manager
- [S18] Fireworks jobs: https://www.fastaijobs.com/companies/fireworks-ai/forward-deployed-engineer ; https://www.indexventures.com/startup-jobs/fireworks-ai/member-of-technical-staff-data-platform-engineer/
- [S19] Together status: https://apistatuscheck.com/blog/together-ai-status-guide ; https://incidenthub.cloud/status/togetherai/inference-chat-deepseek-v4-pro-0813
- [S20] Browserbase Series B / vetting: https://aimmediahouse.com/ai-startups/browserbase-raises-40-million-series-b-as-demand-for-ai-web-automation-accelerates ; https://pulse2.com/browserbase-director-launch-and-40-million-series-b-raised-for-automating-web-browsing/amp/
- [S21] Neon 80% agents: https://current.tinyfish.ai/issue/13/market-pulse/article/8307/when-80-of-your-customers-stop-being-human ; https://au.finance.yahoo.com/news/databricks-buy-open-source-database-120751104.html
- [S22] Neon agent plan / scale to zero: https://neon.com/docs/introduction/agent-plan.md ; https://neon.com/blog/building-patterns-unlocked-by-scale-to-zero
