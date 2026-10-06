# Round 31 — Track 2: Exploding usage (infra seeing 10x+ AI-driven load)

Date: 2026-10-06. 13 web searches (WebFetch blocked; numbers come from search-result snippets and are not verified against primary sources unless the outlet is primary, e.g. github.blog). Only URLs returned by search are cited.

## What breaks first: ranked by evidence

| Layer | AI multiplier observed | Breaks first? | Incumbent architecture problem |
|---|---|---|---|
| CI / code hosting | Actions 1B → 2.1B min/week (early 2026); AI PRs 4M → 17M/mo (Sep 25 → Mar 26); GitHub CTO says design for 30x; availability ~88% in Jun 2026 | **Yes, already broken** | Per-repo YAML queues, shared multi-tenant runners, no idea which changes need to be verified |
| Databases | 97% of Databricks branches and >80% of Neon DBs created by agents | Being rebuilt (Neon/Lakebase, Xata, Supabase) | Provisioning, per-instance pricing, staging copies |
| Package registries | Malicious packages up 4.5x in H1 2026; 800-1,000 "slopsquat" packages in Aug; agents run `npm install` unattended | Yes (security) | Publish-first, review-never; trust is name-based |
| SaaS / public APIs | Stripe: ~70% of API commands from agents; Alpaca 30% in one quarter | Starting | Rate limits keyed on API key/IP, built for deterministic apps |
| Observability | Telemetry heading to 5-10x; services built 3-5x faster | Bills, not systems | Per-host/per-GB pricing; index everything |
| IaC / cloud control plane | Agents author + apply Terraform; "bottleneck moved from authoring to verification" | Governance gap | Plan/apply built around a human reading the plan |
| Identity / NHI | 45-144:1 NHI:human; 29M leaked secrets (+34%) | Already consolidated | Cisco-Astrix, SailPoint-Entro, Okta-Permiso, Cyera-Oasis: **covered, not proposed** |
| Warehouse | Agent questions fan out to 5-15 calls; Snowflake split out AI credits | Cost overruns | Incumbents charge for it; FinOps already killed (thesis B) |

Not proposed: NHI/secrets (4 acquisitions in 2026), source control (G killed), warehouse FinOps (B killed), agent sandboxes (E2B/Daytona/Minions killed).

---

## T2-1. Verification fabric: CI rebuilt for agent-volume change streams
- **Existing category:** CI/CD (GitHub Actions, CircleCI, GitLab CI, Buildkite, Jenkins). Market size: ~$3-5B in CI/CD tooling plus compute (estimate, unverified).
- **Old assumption:** changes arrive at human speed (a few PRs per engineer per day), so you can run the whole pipeline on every push.
- **Why AI breaks it:** 17M AI PRs/month; Actions minutes doubled in about a year; agents push dozens of speculative branches. Running the full suite on every change costs too much and queues too long, and most agent PRs are thrown away.
- **New category:** a verification fabric. It runs as a change-aware scheduler: it picks which tests a change actually touches, dedupes and batches near-identical agent branches, keeps warm caches per repo graph, and returns a signed "verified" result the agent can use within seconds.
- **Product (CTO-simple):** "Point your runners at us. Agent PRs get verified in 90 seconds for a tenth of the compute. Humans get the same result, just faster."
- **Buyer:** VP Eng / Head of Developer Productivity / Platform lead.
- **Pain:** CI queues, GitHub outages, CI bills growing faster than headcount.
- **Evidence (≥5):** (1) Actions at 2.1B min/week, early 2026 ([36kr](https://eu.36kr.com/en/p/3838634999417353)); (2) AI PRs 4M → 17M/mo ([ai2.work](https://ai2.work/blog/github-agentic-pull-requests-surge-28-fold-in-ten-months)); (3) GitHub availability report May 2026 ([github.blog](https://github.blog/2026-06-11-github-availability-report-may-2026/)); (4) Microsoft adds AWS capacity for GitHub ([aiweekly](https://aiweekly.co/alerts/microsoft-taps-aws-to-keep-github-running-amid-ai-surge)); (5) Blacksmith $45M B at $550M, CI jobs +5-10% week over week, Aug 12 2026 ([SiliconANGLE](https://siliconangle.com/2026/08/12/blacksmith-raises-45m-aid-ai-code-validation-agentic-development-grows/)); (6) Tenki pitching "agentic runners" against Depot ([tenki](https://www.tenki.cloud/blog/depot-ci-vs-tenki-agentic-runners)).
- **Workaround:** faster runners (Blacksmith/Depot/Namespace), Bazel remote cache, Launchable/Trunk test selection, throttling agents.
- **Competitors:** direct: Blacksmith, Depot, Namespace, Tenki, Buildkite. Adjacent: GitHub (native), Trunk, Launchable (CloudBees), Nx Cloud, EngFlow.
- **Why incumbents may lose:** GitHub Actions is a multi-tenant queue that must serve 100M+ users and is fighting for capacity. Selecting and deduping tests needs a per-customer dependency graph, which GitHub has not built. The weakness: faster-runner startups are adding this quickly.
- **Wedge:** cut verification time for agent PRs at teams with ≥30% agent-authored PRs.
- **Integration:** hours (change runs-on label), days for test selection.
- **30-day pilot:** shadow-run on one monorepo; report the % of compute saved and p50 time-to-green.
- **Pricing:** per verified change, or per compute minute with a savings share.
- **Expansion:** merge queue, flaky quarantine, signed provenance, preview environments.
- **Moat at 10/100/1,000:** caches / cross-repo flake & test-impact models / default verification oracle that agent vendors call.
- **$10B case:** CI becomes the gate every machine-written change must pass, priced on change volume, which grows 10-30x.
- **CTO one-liner:** "CI was built for humans pushing 3 times a day; we built it for agents pushing 300."
- **Scores:** Market 7, Transformation 8, Urgency 8, Why-now 9, Buyer reach 7, Pilot speed 8, Integration 8, Competitive opening 4, Structural diff 5, Expansion 7, Moat 5, VC 7 → **avg 6.9**
- **Kill risk:** Blacksmith ($550M) plus T3 (autonomous merge) and the test-suite steward were already killed. The opening exists only if the product is the dedupe/selection brain, not runners.

## T2-2. Disposable production twins (staging rebuilt)
- **Existing category:** staging/preview environments plus test data management (Delphix, Tonic, Shipyard, Release, Qovery, internal staging). Market size: TDM ~$1.5-2B plus staging infra spend (unverified).
- **Old assumption:** one long-lived shared staging environment is enough because humans ship a few changes a day.
- **Why AI breaks it:** dozens of agent PRs per day each need a running, data-realistic full stack for verification. Shared staging becomes the bottleneck and the place agents break each other's work.
- **New category:** per-change production twins: a copy-on-write DB clone with masked data, the services, and mocked third parties. Spin-up in under 60 s, a TTL, and a cost cap.
- **Product:** "Every agent change gets its own masked copy of prod in under a minute, then it disappears."
- **Buyer:** Head of Platform / VP Eng; the CISO co-signs on masking.
- **Pain:** staging contention, unrealistic test data, PII in dev.
- **Evidence:** (1) 97% of Databricks branches agent-created ([SaaStr](https://www.saastr.com/databricks-only-19-of-organizations-have-deployed-ai-agents-but-theyre-already-creating-97-of-databases/)); (2) Lakebase GA Feb 2026 ([Nucleus](https://nucleusresearch.com/research/single/databricks-lakebase-makes-postgres-ready-for-agents/)); (3) StackGen acquires Shipyard ([webull](https://www.webull.com/news/15661549759824896)); (4) Render: preview envs as agent sandboxes ([render](https://render.com/articles/preview-environments-as-agent-sandboxes)); (5) Xata instant clones ([joinnextdev](https://www.joinnextdev.com/a/xata/xata-bets-on-instant-clones-for-the-ai-agent-era)); (6) lakeFS agentic data sandbox ([lakefs](https://lakefs.io/blog/agentic-data-sandbox/)); (7) Qovery comparing 9 platforms ([qovery](https://www.qovery.com/blog/coding-agent-ephemeral-dev-environments-9-platforms-compared)).
- **Workaround:** in-house k8s namespaces plus nightly DB snapshot scripts (e.g. Nirvana blog).
- **Competitors:** direct: Shipyard/StackGen, Qovery, Northflank, Signadot, Release, Railway/Render. Adjacent: Neon/Lakebase, Xata, Tonic, Delphix (Perforce).
- **Why incumbents may lose:** Delphix and Tonic are batch tools built for a refresh every few weeks. Database vendors only clone their own DB, and the hard part is the full stack plus masking plus third-party mocks.
- **Wedge:** Postgres plus k8s shops with heavy agent PR volume and PII.
- **Integration:** days.
- **Pilot:** one service, all agent PRs, 30 days; measure defects caught before merge.
- **Pricing:** per environment-hour plus a platform fee.
- **Expansion:** agent eval data, incident replay, compliance evidence.
- **Moat:** masking policies plus a service-dependency map per customer; weak network effects.
- **$10B case:** staging becomes a per-change consumption product like CI.
- **CTO one-liner:** "Staging was a place; now it's a function call."
- **Scores:** Market 6, Transformation 8, Urgency 7, Why-now 8, Buyer reach 7, Pilot 6, Integration 5, Opening 5, Structural 6, Expansion 7, Moat 5, VC 6 → **avg 6.3**

## T2-3. Agent-aware API front door for SaaS and API companies
- **Existing category:** API management/gateways (Apigee, Kong, MuleSoft, AWS API GW). Market size: ~$5-8B (unverified).
- **Old assumption:** API calls come from deterministic apps written by a known developer, so key-based rate limits and quotas are enough.
- **Why AI breaks it:** agents produce bursty, exploratory, retrying, fan-out traffic. One "customer" may be 1,000 agent instances. Stripe says ~70% of API commands come from agents.
- **New category:** an agent traffic controller. It identifies the agent, delegating user, and task; applies intent-level quotas, cost-aware throttling, and duplicate/retry suppression; and prices per outcome, not per call.
- **Product:** "Know which agent, for whom, and why — and stop one runaway loop from taking down your API."
- **Buyer:** VP Platform / Head of API at API-first companies.
- **Evidence:** (1) Stripe ~70% agent commands, Alpaca 30% ([TechSpot](https://www.techspot.com/news/112657-bots-have-officially-overtaken-humans-internet-cloudflare.html?rand=98523), secondary); (2) bots 57.5% of HTTP, Jun 2026 (same); (3) Cloudflare predicts agent traffic will reach 1,000x human ([ecosistemastartup](https://ecosistemastartup.com/cloudflare-alerta-el-trafico-de-agentes-sera-1-000x-el-humano/)); (4) GitHub load crisis partly from agent API use ([waxell](https://waxell.ai/blog/github-ai-agent-crisis-infrastructure-enforcement-2026)); (5) MCP tool payloads >10K tokens ([fast.io](https://www.fast.io/resources/ai-agent-terraform-infrastructure.md)). Fewer than 5 primary signals: **weak**.
- **Competitors:** Cloudflare (Web Bot Auth, AI gateway), Kong AI Gateway, Zuplo, Stytch/WorkOS/Okta agent identity, Stripe/Metronome usage billing.
- **Why incumbents may lose:** gateways are stateless per request, and agent control needs session/task state. Weakness: Cloudflare can ship this with identity; T4 (Stripe for agents) and T (toll router) were already killed.
- **Integration:** days (sits in front of the gateway). **Pilot:** shadow mode, classify traffic, show the share of runaway loops. **Pricing:** per million agent requests.
- **Moat:** a cross-customer agent fingerprint network (real at 100+ customers).
- **$10B case:** agent calls become most API traffic and need their own control layer.
- **CTO one-liner:** "Your rate limiter thinks it's talking to an app. It's talking to a swarm."
- **Scores:** Market 7, Transformation 7, Urgency 6, Why-now 7, Buyer reach 6, Pilot 7, Integration 7, Opening 4, Structural 5, Expansion 7, Moat 6, VC 6 → **avg 6.25**

## T2-4. Change control plane for agent-driven infrastructure
- **Existing category:** IaC orchestration/TACOS (HCP Terraform, Spacelift, env0, Scalr), plus cloud change management. Market size: ~$2-3B (unverified).
- **Old assumption:** a human writes HCL, reads the plan, and clicks apply; changes are rare and reviewed.
- **Why AI breaks it:** agents author and apply changes through MCP. Change volume rises 10x and nobody reads plans, so blast-radius verification has to be automatic.
- **New category:** a policy-and-simulation gate. It predicts the blast radius of each change against live cloud state, sets budgets for each agent, auto-approves low-risk changes, and stages rollouts with automatic revert.
- **Buyer:** Head of Platform / Cloud Infra.
- **Evidence:** (1) HashiCorp "HCP Terraform is the control plane for AI-driven infrastructure" ([hashicorp](https://hashicorp.com/blog/hcp-terraform-is-the-control-plane-for-ai-driven-infrastructure)); (2) StackGuardian agentic IaC, Aug 6 2026 ([stackguardian](https://www.stackguardian.io/post/agentic-iac)); (3) Firefly State of IaC 2026 ([firefly](https://www.firefly.ai/state-of-iac-2026)); (4) Scalr guide for coding agents ([scalr](https://scalr.com/learning-center/infrastructure-as-code-with-ai-coding-agents)); (5) ControlMonkey on AI assistants changing governance ([nhimg](https://nhimg.org/articles/ai-assistants-for-terraform-now-change-how-cloud-infrastructure-is-governed/)).
- **Competitors:** HashiCorp/IBM, Spacelift, env0, Firefly, StackGuardian, ControlMonkey, Pulumi Neo. **Crowded; incumbents are already marketing it.**
- **Integration:** days. **Pilot:** gate agent PRs on one account. **Pricing:** per managed resource.
- **Scores:** Market 6, Transformation 7, Urgency 6, Why-now 7, Buyer 7, Pilot 7, Integration 6, Opening 3, Structural 4, Expansion 6, Moat 4, VC 5 → **avg 5.7**

## T2-5. Dependency admission control (artifact registry for agent installs)
- **Existing category:** artifact repositories plus SCA (JFrog ~$500M ARR, Sonatype, Snyk). Market size: ~$4-6B combined (unverified).
- **Old assumption:** a human picks a dependency, and the registry trusts names.
- **Why AI breaks it:** agents install unseen packages unattended, and attackers mass-publish AI-plausible names (1,000 in a single August wave).
- **New category:** an admission controller between agents and every registry. It enforces cooldowns, builds from source, checks reputation, and supplies a "known-good" substitute when an agent hallucinates a name.
- **Evidence:** (1) CSA: 4.5x malicious packages in H1 ([CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-package-registry-systemic-risk-20260623/)); (2) slopsquat RAT campaign, Aug 2026 ([CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-npm-ai-slopsquatting-rat-infostealer-20260/)); (3) Chainguard Repository launch ([letsdatascience](https://letsdatascience.com/news/chainguard-launches-repository-to-secure-dependencies-b7f40754)); (4) Chainguard plus Cursor ([letsdatascience](https://letsdatascience.com/news/chainguard-and-cursor-secure-ai-agent-supply-chains-825999c0)); (5) Socket raises $60M; Replit deploys Socket Firewall ([govinfosecurity](https://www.govinfosecurity.com/socket-raises-60m-for-wider-software-supply-chain-defense-a-31785)).
- **Competitors:** Chainguard, Socket, JFrog Curation, Sonatype Firewall, Endor Labs, Aikido. **Funded and shipping.**
- **Scores:** Market 7, Transformation 7, Urgency 8, Why-now 8, Buyer 7, Pilot 8, Integration 8, Opening 2, Structural 3, Expansion 6, Moat 4, VC 5 → **avg 6.1** (likely kill: Chainguard/Socket own it).

## T2-6. Telemetry built for 10x-volume, machine-read observability
- **Existing category:** observability/logging (Datadog, Splunk, Elastic, New Relic). Market size: ~$50B+.
- **Old assumption:** humans read dashboards, and telemetry grows with headcount and hosts, so index everything and price per GB/host.
- **Why AI breaks it:** agents create services 3-5x faster, telemetry heads to 5-10x, and the main reader becomes an SRE agent that wants raw, queryable, cheap data, not dashboards.
- **New category:** an object-storage-native telemetry lake priced on query, with an agent query API as the primary interface.
- **Evidence:** (1) OneUptime: "AI coding agents will 10x your Datadog bill" ([oneuptime](https://oneuptime.com/blog/post/2026-02-12-ai-coding-agents-will-10x-your-datadog-bill/view)); (2) Dynatrace State of Log Management 2026 ([dynatrace](https://www.dynatrace.com/news/press-release/the-state-of-log-management-2026/)); (3) Datadog rebrands LLM Obs as Agent Observability ([truefoundry](https://www.truefoundry.com/blog/datadog-llm-observability-pricing)); (4) Augment: 5-10x volume trajectory ([augmentcode](https://augmentcode.com/tools/best-observability-platforms)); (5) OneUptime bill shock, Mar 2026 ([oneuptime](https://oneuptime.com/blog/post/2026-03-17-datadog-bill-shock-real-cost-observability-2026/markdown)). Mostly vendor marketing: **weak**.
- **Competitors:** ClickHouse/ClickStack, Grafana, Cribl, Observe (Snowflake), Chronosphere (Palo Alto), Honeycomb, plus AI-SRE startups (Resolve, Traversal, Cleric). **Very crowded.**
- **Scores:** Market 9, Transformation 7, Urgency 6, Why-now 6, Buyer 6, Pilot 6, Integration 5, Opening 3, Structural 4, Expansion 7, Moat 4, VC 5 → **avg 5.7**

---

## Summary
| Thesis | Avg | Verdict |
|---|---|---|
| T2-1 Verification fabric (agent-volume CI) | 6.9 | Best evidence of breakage (GitHub 30x). Blacksmith $550M is the threat. Worth a 14-day test only as a test-selection/dedupe brain |
| T2-2 Disposable production twins | 6.3 | Real; fragmented field (Shipyard acquired, DB vendors only partial) |
| T2-3 Agent-aware API front door | 6.25 | Strong data point (Stripe 70%), but close to killed T4/T and Cloudflare |
| T2-5 Dependency admission control | 6.1 | Urgent but owned by Chainguard/Socket |
| T2-4 Agent IaC change control | 5.7 | Incumbents already marketing it |
| T2-6 Telemetry lake for 10x volume | 5.7 | Huge market, very crowded |

Pattern (consistent with STATUS lesson G): where usage visibly broke first (code hosting, CI, DB branching, registries), specialist money arrived within months. None reaches 8.5. The layers still uncrowded (API front door, per-change twins) have the weakest public evidence.
