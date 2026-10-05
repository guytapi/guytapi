# What breaks next: shared infrastructure on GitHub's trajectory (round 9)

Date: 2026-10-05. Method: round7/METHOD.md, with a screen for being early. 40 web searches; WebFetch and Reddit blocked.
**Source caveat:** every URL below came back in search results. Figures are quoted from search-result summaries and I have **not** read them on the page. Items marked *(unverified)* come from a secondary source or need a check on the page before anyone relies on them.

## Bottom line

- **Nothing clears the bar (8.5, with no category below 7).**
- **The pattern from thesis G holds and it moves faster than we assumed.** In the most strained systems the incumbent has already shipped the agent-scale fix:
  - **Self-hosted Git:** GitLab announced its "next generation SCM for agentic scale" on 2026-06-10.
  - **Package registries:** Cloudsmith raised a $72M Series C on 2026-04-23, pitched explicitly on AI coding agents.
  - **CI:** WarpBuild, Tenki, Blacksmith and Depot all sell agent-load CI.
  - **Postgres:** Neon (Databricks) and AlloyDB "PostgreSQL for agents".
  - **Sandboxes:** Google's agent-sandbox project, GA on GKE 2026-05-20.
  - **SaaS egress gateways:** Boomi acquired Lunar.dev in July 2026.
- **Best near-miss: #1, the tenant-level quota and read plane for systems of record (Jira, Confluence, M365, Salesforce, Slack). Average 6.4.**
  - The strain is real, recent and still trade-press only: Atlassian's points enforcement started 2026-03-02, Slack moved to Tier 1 on 2026-03-03, and Rovo MCP is capped at 10k calls per hour.
  - Atlassian's own tracker carries open requests for tenant-level observability (AX-1883) and higher per-tenant limits (ROVO-968).
  - Nobody funded owns the buyer-side, multi-SaaS quota plane yet. But Glean, gateway vendors and the SaaS vendors themselves sit one feature away.

---

## Part 1: Scan of candidate systems

Early-signal strength (E): 1 = no strain visible, 5 = strain is measurable, accelerating and still not mainstream. "Agent-scale specialist?" asks whether a funded company already sells the agent-scale fix.

| # | System | Growth / strain evidence (date, URL) | Owner today | Agent-scale specialist? | E | One-sentence startup idea | Verdict |
|---|---|---|---|---|---|---|---|
| 1 | **SaaS systems-of-record APIs** (Jira, Confluence, Slack, M365 Graph, Salesforce) | Atlassian points-based quotas enforced 2026-03-02. Tier-1 apps share a 65,000 pts/hr **global pool**; per-tenant pools are 100k-150k base + 10-30 per user. [Atlassian rate limiting](https://developer.atlassian.com/cloud/jira/platform/rate-limiting), [community thread](https://community.developer.atlassian.com/t/2026-point-based-rate-limits/97828?page=3), ["Rate limit abuse (new attack vector)"](https://community.developer.atlassian.com/t/rate-limit-abuse-new-attack-vector/99654), [AX-1883 tenant admin observability request](https://jira.atlassian.com/browse/AX-1883), [ROVO-968 higher per-tenant Rovo limits](https://jira.atlassian.com/browse/ROVO-968). Rovo MCP cap of 1,000/hr + 20 per user, max 10,000/hr; one user was blocked 30 minutes with no backoff signal ([community](https://community.atlassian.com/forums/Rovo-questions/Clarification-on-Atlassian-Rovo-MCP-Server-Rate-Limits-10-000/qaa-p/3264375)). Slack cut conversations.history to Tier 1 (1 request/min, 15 objects) for unlisted apps, applied to existing installs 2026-03-03 ([Slack changelog](https://docs.slack.dev/changelog/2025/05/29/rate-limit-changes-for-non-marketplace-apps)). Graph and SharePoint throttling described as a "tenant reliability boundary" in the Copilot era ([dev.to](https://dev.to/aakash_rahsi/rahsi-sharepoint-online-throttling-internals-limits-and-survival-patterns-copilot-era-edition-p9n), [MS Graph limits](https://learn.microsoft.com/graph/throttling-limits)). Salesforce 24h rolling API limit ([SF cheatsheet](https://developer.salesforce.com/docs/platform/salesforce-app-limits-cheatsheet/guide/salesforce-app-limits-platform-api.html)). | Atlassian, Microsoft, Salesforce, Slack (they set the limits) | Partial. Lunar.dev was acquired by Boomi in Jul 2026 ([Boomi](https://boomi.com/?p=61007)). Gravitee, Kong and Zuplo sell gateways; Truto and Composio sell unified APIs (vendor-side). Glean indexes SaaS. One OSS hobby mirror, gadak ([pkg.go.dev](https://pkg.go.dev/github.com/midagedev/gadak@v0.15.1)). No funded **buyer-side, multi-SaaS tenant quota plane**. | **4** | A tenant-level read replica and quota scheduler that mirrors your Jira, Confluence, M365 and Salesforce data. It serves agent reads locally and spends the tenant's write and API budget by priority. | **Pick #1** |
| 2 | **Public package registries** (npm, PyPI, crates.io, Maven Central) | Sonatype "significantly tightened" Maven Central limits in May 2026; 1% of IPs carry 83% of bandwidth ([Sonatype blog](https://www.sonatype.com/blog/beyond-ips-addressing-organizational-overconsumption-in-maven-central), [429 FAQ](https://central.sonatype.org/faq/429-error/)). CircleCI and Harness incidents ([CircleCI status](https://status.circleci.com/incidents/qhxl36d29vfl), [Harness status](https://status.harness.io/incidents/mq6ptvcp9wbm)); Trivy breakage ([GH issue](https://github.com/aquasecurity/trivy/issues/10691)). PyPI AWS spend +69% YoY "as agents and CI runs surge", ending an 8-year flat streak ([PyPI blog 2026-08-14](https://blog.pypi.org/posts/2026-08-14-how-aws-powers-pypi-and-the-psf/)). crates.io reportedly used nearly all of its 18-19 PB 2026 bandwidth estimate in H1 *(unverified; from [Datadog OSS page](https://opensource.datadoghq.com/projects/rust-foundation/))*. Joint registry statement cites "agentic AI driving a further explosion of machine-driven, often wasteful automated usage" ([LWN](https://lwn.net/Articles/1039127)). CSA note on AI package registry systemic risk, 2026-06-23 ([CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-package-registry-systemic-risk-20260623/)). | PSF, Rust Foundation, Sonatype, GitHub/npm (registries); JFrog, Sonatype Nexus, Cloudsmith (enterprise mirrors) | **Yes.** Cloudsmith $72M Series C, 2026-04-23, framed on AI coding agents ([tech.eu](https://tech.eu/2026/04/23/cloudsmith-raises-72m-series-c-to-secure-the-ai-era-software-supply-chain/)). Nx read-through cache for agents ([nx.dev](https://nx.dev/docs/features/ci-features/npm-read-through-cache)). Rivet agentOS registry ([rivet](https://rivet.dev/changelog/2026-07-06-introducing-the-agentos-package-registry)). | **5** strain, but funded | A pre-resolved, content-addressed dependency plane for sandbox fleets: lazy-mounted environments in place of `pip install` / `npm install` on every agent boot. | **Pick #2** (strongest strain, weakest whitespace) |
| 3 | **Data warehouses and BI** (Snowflake, BigQuery) under agent SQL | Snowflake AI Credits as a separate currency from 2026-04-01; agent retries billed per message ([coefficient](https://coefficient.io/snowflake/snowflake-intelligence-cost)). "Agents should run somewhere else" ([definite](https://www.definite.app/blog/ai-agents-snowflake-cost)). Uber reportedly exhausted its 2026 AI budget in 4 months *(unverified, secondary)*. Revefi on agent-driven Snowflake bills ([revefi](https://www.revefi.com/blog/wait-my-snowflake-bill-did-what-the-hidden-cost-of-agentic-ai-in-snowflake)). Research: OLAP semantic cache with 82% hit rate ([arXiv 2602.19811](https://www.alphaxiv.org/abs/2602.19811)). | Snowflake, Google, Databricks | Partial. Revefi, Select.dev ([changelog](https://select.dev/changelog/ai-copilot)), Definite, MotherDuck, plus semantic layers (Cube, dbt, Coginiti). No funded "agent query plane". | 3 | An agent-workload SQL plane: semantic result cache, dedup, and routing of agent queries to a cheap replica engine (DuckDB / Iceberg) away from the warehouse. | **Pick #3** (weak) |
| 4 | CI runners | GitHub agent PRs went from ~4M (Sep 2025) to 17M+ (Mar 2026); Actions at 2.1B min/week *(secondary: [tianpan](https://tianpan.co/blog/2026-06-02-the-coding-agent-ci-bill-that-doubled-without-a-postmortem))*. 3-5x CI minutes per developer ([WarpBuild](https://warpbuild.com/blog/ai-assisted-development-ci-infrastructure)). | GitHub Actions, CircleCI, Buildkite | Yes: WarpBuild, Tenki ([tenki](https://www.tenki.cloud/blog/agent-pr-volume-ci-scale)), Blacksmith, Depot, Namespace | 2 (public) | n/a | Kill: crowded |
| 5 | Self-hosted Git (GHES, GitLab, Bitbucket DC) | "Git was designed for human-speed operations"; GitLab claims 1000x less network than clones ([GitLab PR 2026-06-10](https://about.gitlab.com/press/releases/2026-06-10-gitlab-announces-new-capabilities-to-give-enterprises-speed-control-at-agentic-scale/)) | GitHub, GitLab, Atlassian | Incumbent shipped it, plus Pierre, Entire, Cloudflare Artifacts (thesis G) | 1 | n/a | Kill (G variant) |
| 6 | Operational Postgres under agents | Connection-pool exhaustion is the top incident ([c-sharpcorner](https://www.c-sharpcorner.com/article/can-postgresql-keep-up-when-thousands-of-ai-agents-query-it-at-once)); 80% of Neon DBs are created by agents ([Databricks](https://www.databricks.com/blog/databricks-neon)) | AWS, Google, Databricks/Neon | Yes: AlloyDB "PostgreSQL for agents" ([Google](https://cloud.google.com/blog/products/databases/announcing-postgresql-for-agents-in-alloydb)), CockroachDB, Supabase, Xata | 2 | n/a | Kill |
| 7 | Kubernetes / sandbox control plane | agent-sandbox warm pool: 300 sandboxes/s per cluster; GA on GKE 2026-05-20 ([agent-sandbox docs](https://agent-sandbox.sigs.k8s.io/docs/use-cases/examples/hpa-swp-scaling/)). Events can flood etcd (CVE-2026-10533, [SentinelOne](https://www.sentinelone.com/vulnerability-database/cve-2026-10533/)) | Google/CNCF, E2B, Modal, Daytona | Yes | 2 | n/a | Kill |
| 8 | Docker Hub / container pulls | Limits unchanged since Mar 2025 (100-200 pulls / 6h unauthenticated or personal) ([Docker docs](https://docs.docker.com/docker-hub/usage/pulls/)) | Docker; ECR/GHCR | Depot, registries above | 2 | n/a | Folded into #2 |
| 9 | Hugging Face Hub | Per-5-minute resolver buckets; 429s even on Pro ([HF docs](https://huggingface.co/docs/hub/en/rate-limits)); JFrog-HF changes in June 2026 ([HF blog](https://huggingface.co/blog/jeffboudier/jfrog-artifactory-june-2026)) | Hugging Face, JFrog | JFrog, Cloudsmith ML registry | 2 | n/a | Folded into #2 |
| 10 | Identity providers / token issuance | Machine identities ~109x humans; Okta caps each OAuth app at 50% of a bucket ([SSOJet](https://ssojet.com/blog/enterprise-authentication-trends), [Okta](https://developer.okta.com/docs/reference/rl2-token-oauth/)). No strain incidents found. | Okta, Entra | Yes: Okta for AI Agents, Entra Agent ID, NHI vendors (Astrix, Aembit, etc.) | 1 | n/a | Kill |
| 11 | Secrets managers | AWS Secrets Manager GetSecretValue 10,000 TPS per region ([AWS](https://docs.aws.amazon.com/secretsmanager/latest/userguide/reference_limits.html)). No strain found. | AWS, HashiCorp/IBM | n/a | 1 | n/a | Kill: no signal |
| 12 | DNS / certificates for previews | Route 53: 100 changes/s sustained, 1,500 burst ([AWS](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/throttling-api-requests.html)). LE rate limits doc updated Aug 2026 ([LE](https://letsencrypt.org/docs/rate-limits/)). No strain reports. | AWS, Cloudflare, ISRG | Vercel/Cloudflare absorb | 1 | n/a | Kill: no signal |
| 13 | Cloud control planes / IaC | Runaway agent loop: 127k API calls, ~$47k in 8h *(unverified anecdote, [Zuplo](https://zuplo.com/blog/never-ship-mcp-server-without-rate-limit))*. Terraform locking unchanged ([Scalr](https://scalr.com/learning-center/infrastructure-as-code-with-ai-coding-agents)) | AWS / HashiCorp | Scalr, Spacelift, Env0, Firefly | 2 | n/a | Kill: no measurable strain |
| 14 | Observability ingest | Not searched (excluded category, crowded) | Datadog etc. | many | n/a | n/a | Excluded |
| 15 | OSS maintainers / issue trackers, web bot traffic | Already mainstream (curl, Cloudflare reports) | GitHub, Cloudflare | Cloudflare, TollBit | 1 | n/a | Kill: public |

**What the scan shows:** the systems with strain we can measure (registries, CI, Git, Postgres) are exactly where funded specialists or incumbent fixes already exist. The systems with no specialist (secrets, DNS, certificates, identity) show no strain. SaaS tenant quotas are the only system where both the strain and the whitespace are partial.

---

## Part 2: Full METHOD write-ups

### Pick #1: Tenant quota and read plane for systems of record ("agent read replica for Jira, Confluence, M365, Salesforce")

**Problem.** Every employee's coding agent, Rovo or Copilot agent, Glean connector and internal automation now draws from **one per-tenant API budget** that each SaaS vendor set for human-driven apps. Atlassian's 2026 points system meters each call by work done. The Rovo MCP endpoint caps a whole enterprise at 10,000 calls per hour. Slack cut history reads to 1 request per minute for unlisted apps. Graph/SharePoint throttling is a tenant boundary that Copilot, Power Automate and agents compete for. When the budget runs out, **everything** in the tenant throttles, including critical human workflows and Marketplace apps. Today nobody can see which agent burned it.

**Recent evidence (signals):**
1. Atlassian points-based enforcement started 2026-03-02. Shared 65k pts/hr global pool for Tier 1; per-tenant pools scale with users ([docs](https://developer.atlassian.com/cloud/jira/platform/rate-limiting); [community thread, page 3](https://community.developer.atlassian.com/t/2026-point-based-rate-limits/97828?page=3)).
2. Open Atlassian request AX-1883, "Tenant Admin Observability for API Consumption and Rate Limiting". Admins can't see who consumes the budget ([jira.atlassian.com](https://jira.atlassian.com/browse/AX-1883)).
3. ROVO-968: Rovo agent invocations in Automation hit a fixed per-tenant limit and fail at random under bursts ([jira.atlassian.com](https://jira.atlassian.com/browse/ROVO-968)).
4. Developer thread "Rate limit abuse (new attack vector)": one app or script can starve a tenant ([community](https://community.developer.atlassian.com/t/rate-limit-abuse-new-attack-vector/99654)). Also "one bad script can spoil it for everyone" ([community article](https://community.atlassian.com/forums/Jira-Cloud-Admins-articles/Burst-API-Rate-Limits-one-bad-script-can-spoil-it-for-everyone/bc-p/3220404)).
5. Rovo MCP cap: 1,000/hr + 20 per user, max 10k/hr. A user was locked out for 30 minutes with no backoff signal ([community](https://community.atlassian.com/forums/Rovo-questions/Clarification-on-Atlassian-Rovo-MCP-Server-Rate-Limits-10-000/qaa-p/3264375)).
6. Slack's Tier 1 history limit applied to existing unlisted installs from 2026-03-03 ([Slack changelog](https://docs.slack.dev/changelog/2025/05/29/rate-limit-changes-for-non-marketplace-apps)).
7. SharePoint/Graph throttling in the "Copilot era" described as a shared tenant envelope ([dev.to](https://dev.to/aakash_rahsi/rahsi-sharepoint-online-throttling-internals-limits-and-survival-patterns-copilot-era-edition-p9n)).
8. Practitioners have started building their own local mirrors to dodge limits, e.g. gadak, which syncs Jira and Confluence to SQLite and exposes it through MCP ([pkg.go.dev](https://pkg.go.dev/github.com/midagedev/gadak@v0.15.1)).
- *Gap in the evidence:* no Reddit or HN data (blocked), and no hard numbers on agent share of tenant API traffic. The 5-20x per year growth rate is **inferred** (agent PR volume ~4x in 6 months, from a secondary source), not measured for SaaS APIs.

**Who has the pain.** Platform, enterprise-apps and IT engineering teams at companies with 2,000+ seats on Atlassian Cloud, M365 or Salesforce that rolled out coding agents with MCP. Also SaaS vendors' Marketplace app builders, who get collateral throttling.

**What they do today.** Exponential backoff in each agent. Banning or limiting MCP servers. Opening tickets with Atlassian or Microsoft to raise limits. Homegrown nightly exports to a warehouse. Hobby mirrors.

**Why current products fail.**
- Gateways (Gravitee, Kong, Zuplo, Lunar/Boomi) rate-limit **your** API, or proxy egress per call. They don't hold a synced replica, so they can't remove the reads.
- Unified APIs (Truto, Composio, Merge) serve SaaS vendors building integrations, not the buyer's tenant.
- Glean indexes content for search, but agents need structured, fresh, writable objects such as issue fields and transitions.
- Atlassian and Microsoft have no incentive to cut metered API traffic, and Atlassian charges for higher tiers.

**Why now.** Atlassian points enforcement (Mar 2026), Slack Tier 1 for existing installs (Mar 2026), Rovo MCP GA (Feb 2026) and Copilot/agent rollouts all landed in the same 6 months. Agent PR volume per company is up several times over.

**Potential product.** A deployable "agent read replica" per tenant:
- Change-data-capture sync from Jira, Confluence, Slack, Graph and Salesforce, using webhooks plus incremental reconciliation, done once per tenant.
- One MCP and SQL endpoint for all agents, with permission-aware row filtering that mirrors the source ACLs. This is the hard part.
- A write-through queue that spends the tenant's points budget by priority: humans and production first, background agents last.
- Per-agent attribution dashboards, which is what AX-1883 asks for.

**Time to value.** 1-2 weeks for Jira and Confluence read offload (CDC plus MCP endpoint), with visible point savings in week 1.

**Pilot (14-30 days).** Route the company's Jira MCP traffic through the replica. Success: at least 70% of agent reads served locally, zero tenant-wide 429 events, and a per-agent consumption report.

**Willingness to pay.** Anchor on the Atlassian or Microsoft upgrade the customer would otherwise buy, plus engineer hours lost to throttling. Plausible $30k-150k/yr per enterprise *(assumption, not validated)*.

**Expansion.** More systems of record (ServiceNow, Zendesk, HubSpot, Workday). Become the governed "agent data plane" for SaaS, with write approval and audit.

**Competition.**
- Glean, which could add structured replicas.
- Boomi plus Lunar, Gravitee, Kong (egress gateways).
- Atlassian or Microsoft raising limits or shipping caching. Atlassian could also respond with ToS: mirroring may conflict with API terms, which is a **material risk**.
- CData / Fivetran-style sync vendors that already replicate SaaS to SQL.
- Hobby mirrors (gadak).

**Moat.**
- 10 customers: connector quality and permission-mirroring correctness.
- 100 customers: a cross-tenant library of point-cost models per endpoint and sync-efficiency tricks.
- 1,000 customers: becomes the system agents talk to instead of the SaaS, a strategic chokepoint. That invites a vendor response.

**CTO test sentence.** "Every agent in the company reads Jira and SharePoint from one replica we control, and we never get tenant-throttled again."

**Kill test question.** Do 5 of 10 platform leads at 2,000+ seat Atlassian or M365 shops report a tenant-wide throttling incident caused by agents in the last 90 days? And will their legal teams accept a synced replica under Atlassian and Microsoft API terms?

**Scores:**

| Category | Score | Rationale |
|---|---|---|
| Pain severity | 6 | Real, but workarounds (backoff, banning MCP) are tolerable today |
| Urgency | 6 | Enforcement is fresh; incidents are sporadic |
| Market timing | 8 | Early: limits from Mar 2026, admin observability still a feature request |
| Speed to pilot | 7 | Read-only Jira replica in 2 weeks |
| Ease of integration | 6 | OAuth app plus MCP redirect; permission mirroring is hard |
| Ease of reaching customers | 6 | Atlassian admins and platform teams are reachable; enterprise security review |
| Willingness to pay | 5 | Unproven; competes with "just buy a higher tier" |
| Competition | 6 | No funded buyer-side specialist, but Glean, Boomi/Lunar and sync vendors are adjacent |
| Moat potential | 6 | Connectors plus a permissions-correct replica is hard; vendor ToS risk |
| Market size | 7 | Every large SaaS tenant; extends to all systems of record |
| VC attractiveness | 7 | "Agent data plane" story; risk of being seen as a feature |
| **Average** | **6.4** | Below bar |

### Pick #2: Dependency plane for agent sandbox fleets ("never `pip install` from the internet again")

**Problem.** Every agent sandbox and CI job boots cold and re-downloads its dependency tree from public registries that donors fund. Registries are responding with throttling (Maven Central, May 2026) and paid tiers. Enterprises see 429s, broken builds and slow sandbox starts, and their agents pull unvetted packages during a record malware wave.

**Recent evidence:**
- Maven Central tightened limits in May 2026, aimed at the top few percent of consumers ([Sonatype 429 FAQ](https://central.sonatype.org/faq/429-error/); [Sonatype blog](https://www.sonatype.com/blog/beyond-ips-addressing-organizational-overconsumption-in-maven-central)).
- CircleCI ([status](https://status.circleci.com/incidents/qhxl36d29vfl)), Harness ([status](https://status.harness.io/incidents/mq6ptvcp9wbm)) and Bitrise ([blog](https://bitrise.io/blog/post/open-source-registries-are-changing-how-bitrise-keeps-your-builds-running)) disruptions; Trivy breakage ([GH issue](https://github.com/aquasecurity/trivy/issues/10691)).
- PyPI AWS spend +69% YoY due to "automated agents installing packages" and CI ([PyPI blog](https://blog.pypi.org/posts/2026-08-14-how-aws-powers-pypi-and-the-psf/)).
- crates.io H1 2026 traffic near its full-year estimate *(unverified)*.
- Registries' joint statement names agentic AI ([LWN](https://lwn.net/Articles/1039127)). Sustaining Package Registries WG formed.
- Malware: 497 malicious npm/PyPI packages in H1 2026, 4.5x the prior year; Mini Shai-Hulud hit 160+ packages ([CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-package-registry-systemic-risk-20260623/)).

**Who has the pain.** Platform teams running internal agent fleets (background coding agents, eval farms); sandbox providers; CI vendors.

**What they do today.** Artifactory, Nexus or Cloudsmith remote repos; Nx read-through cache; baked container images; uv and pnpm caches.

**Why current products fail.** Artifact managers serve repos by request. They don't hand a sandbox a **pre-resolved, lazily mounted environment snapshot**, so cold sandboxes still resolve, download and extract. They are priced for human-scale seats and CI.

**Why now.** Registry throttling plus sandbox volumes in the millions per day plus the malware wave.

**Potential product.** A content-addressed dependency store (Nix-store-like) with lockfile-to-snapshot resolution, block-level lazy loading into microVMs, policy gating, and registry-cost accounting.

**Time to value.** Days for an install-latency demo; weeks for a fleet rollout.

**Pilot.** Swap the install step in one sandbox fleet. Measure boot time, egress bytes and 429s.

**Willingness to pay.** Moderate. Artifact-management budgets already exist (JFrog, Cloudsmith), but the delta over them is mainly latency.

**Expansion.** Model weights (HF Hub), container layers, toolchains.

**Competition.** **Cloudsmith ($72M Series C, Apr 2026, AI-agent framing)**, JFrog, Sonatype, Chainguard Libraries, Socket, Nx, Depot, Rivet agentOS registry, and the sandbox vendors' own caches (E2B, Modal, Daytona).

**Moat.** Weak at 10 customers. At 100, cross-customer dedup gives better hit rates. At 1,000, it becomes a cache network and runs into Cloudflare/Fastly economics.

**CTO test sentence.** "Our 50k daily agent sandboxes boot with dependencies in 200 ms and never touch PyPI."

**Kill test question.** Would a platform team switch from or add to an existing Artifactory or Cloudsmith remote repo just for faster sandbox boot?

| Category | Score |
|---|---|
| Pain severity | 6 |
| Urgency | 6 |
| Market timing | 5 (already public; specialist funded) |
| Speed to pilot | 7 |
| Ease of integration | 7 |
| Ease of reaching customers | 6 |
| Willingness to pay | 5 |
| Competition | 3 |
| Moat potential | 4 |
| Market size | 6 |
| VC attractiveness | 5 |
| **Average** | **5.5** |

### Pick #3: Agent query plane for warehouses (semantic result cache plus offload)

**Problem.** Agents issue large numbers of small, repetitive, bursty queries. Each one spins up a warehouse sized and priced for analysts. Snowflake now bills AI in separate credits, and spend is unpredictable.

**Evidence:**
- Snowflake AI Credits from 2026-04-01 ([coefficient](https://coefficient.io/snowflake/snowflake-intelligence-cost)).
- "Analyst dashboards and agents are different workloads" ([definite](https://www.definite.app/blog/ai-agents-snowflake-cost)).
- Revefi on agentic Snowflake bills ([revefi](https://www.revefi.com/blog/wait-my-snowflake-bill-did-what-the-hidden-cost-of-agentic-ai-in-snowflake)).
- Research shows 67-82% cache hit rates on production NL/SQL ([arXiv 2602.19811](https://www.alphaxiv.org/abs/2602.19811); [arXiv 2601.11687](https://arxiv.org/pdf/2601.11687v1)).
- Uber budget anecdote *(unverified)*.

**Who.** Data platform teams that run text-to-SQL or analytics agents.

**Today.** Resource monitors, smaller warehouses, semantic layers.

**Why products fail.** Cost tools observe spend but don't intercept and cache queries. Semantic layers improve correctness, not cost.

**Product.** A wire-compatible SQL proxy: semantic dedup and caching, then routing to a DuckDB/Iceberg replica, then the warehouse as fallback.

**Pilot.** Point one agent at the proxy for 14 days and measure the credit delta.

**Competition.** Revefi, Select.dev, Definite, MotherDuck, Snowflake and Databricks native features (adaptive warehouses, result cache), Cube.

**Moat.** Low to moderate.

**CTO test sentence.** "Our agents' warehouse bill dropped 60% with zero query changes."

**Kill test question.** Is agent SQL more than 15% of warehouse credits at 5 of 10 data teams?

| Category | Score |
|---|---|
| Pain severity | 5 |
| Urgency | 5 |
| Market timing | 6 |
| Speed to pilot | 8 |
| Ease of integration | 7 |
| Ease of reaching customers | 6 |
| Willingness to pay | 6 |
| Competition | 4 |
| Moat potential | 4 |
| Market size | 6 |
| VC attractiveness | 5 |
| **Average** | **5.6** |

---

## Recommendation

1. **Run the kill test on Pick #1 by calling 10 Atlassian/M365 admins and platform leads.** It is the only candidate where strain is new (Mar 2026), the vendor's own tracker shows the missing tenant controls (AX-1883, ROVO-968), and no funded buyer-side specialist exists.
   - Ask first about API ToS for mirroring.
   - Then ask whether agents have caused tenant-wide throttling in the last 90 days.
2. **Update the lesson from G.** For hard infrastructure, incumbents and late-stage players now announce "agentic scale" fixes in the same quarter the strain appears: GitLab in Jun 2026, Cloudsmith in Apr 2026, Sonatype limits in May 2026. Being early through public-source research now means reading vendor developer forums and feature trackers (Atlassian community, jira.atlassian.com) before the strain reaches status pages or the news.
3. **Systems with no strain signal yet** (secrets, DNS, certificates, IdP token issuance) are pre-demand. Re-scan them in Q1 2027.
