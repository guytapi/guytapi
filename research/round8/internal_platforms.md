# Round 8: Internal agent platforms that companies built themselves (2025-2026)

Researcher pass, 2026-10-05. Method: look for engineering blogs, talks and write-ups ("how we built...", "why we built our own...") where companies describe internal systems for running agents at scale. Count the companies that built each system type independently, then check whether a vendor already sells it. 36 web searches. WebFetch is blocked (it failed on software-factories.port.io), so every fact below comes from search-result snippets. Dates come from those snippets. Anything marked *(unverified)* means I did not see a date or URL confirmed in a snippet. I did not make up any URLs. Several summaries come from secondary sources: ZenML LLMOps database, Port's "Inside the Software Factory" series, InfoQ and rywalker.com.

## Headline finding

**The pattern is very strong, but it does not point to a startup gap.** At least 14 companies built a background-agent platform in 2025-2026, and the platforms look much the same everywhere. Each one has:
- a sandboxed dev environment
- a forked or open-source agent harness
- a single MCP/tool gateway with scoped permissions
- a model gateway with cost tracking
- a registry of playbooks or skills
- triggers from Slack, GitHub and cron
- a verification and review layer

The reason companies gave for building it themselves is always the same: **deep integration with their own tools, devboxes and security boundaries, plus unattended execution.** That reason works against a product: the value is the integration work, not a reusable component. By September 2026 every layer of the stack has vendors:
- Ona, Cursor cloud agents, Codex, Claude, Copilot coding agent, Devin and Tembo sell the platform.
- Sourcegraph Agentic Batch Changes went GA on 2026-09-14.
- 14+ vendors sell MCP gateways.
- Cursor approval agents, Graphite and MergeShield cover auto-approval.
- DX, Jellyfish and Faros cover measurement.
- Open-Inspect gives away Ramp's design for free.

Builders far outnumber any single vendor ("no dominant vendor" holds), but every layer is crowded, and most of these systems were built before the vendors arrived. **No candidate clears the bar. Nothing here is strong enough to justify a deep dive.**

## Table: internal system types

Signal strength combines the number of independent builders, the vendor gap, and whether companies with 100-5,000 engineers will need it.

| # | Internal system type | Builders (URL, date) | Problem solved | Why build, not buy | Vendor status (Oct 2026) | Signal |
|---|---|---|---|---|---|---|
| 1 | **Background coding-agent platform** (sandbox + harness + Slack/GitHub triggers → PRs) | **Stripe** Minions, 1,300+ PRs/wk, Goose fork: stripe.dev/authors/alistair-gray, InfoQ https://infoq.com/news/2026/03/stripe-autonomous-coding-agents/ (Feb-Mar 2026). **Ramp** Inspect, 30% → >50% of merged PRs: https://modal.com/blog/how-ramp-built-a-full-context-background-coding-agent-on-modal (2026-02-19), https://builders.ramp.com/post/why-we-built-our-background-agent *(date unverified)*. **Spotify** Honk: https://engineering.atspotify.com/2025/11/spotifys-background-coding-agent-part-1 (Nov 2025), part 4 (Apr 2026). **Uber** Minion, 1,800 changes/wk, 70% of PRs agent-opened: https://ai.engineer/talks/agentic-sdlc-at-uber-building-blocks-for-uber-s-software-factory (~Aug 2026). **Shopify** River, 1 in 8 merged PRs: https://software-factories.port.io/shopify *(date unverified)*. **DoorDash** Flux, 130k tasks/month: https://infoq.com/news/2026/08/doordash-flux-cloud-agent (2026-08-11). **Monzo** Agent Chip: https://monzo.com/blog/building-agent-chip (2026-08-13). **Coinbase** Mux/Forge, 600 users: zenml/odaily summaries (Apr 2026, *primary URL unverified*). **LiteLLM**: https://docs.litellm.ai/blog/lap-internal-agent-30-percent (2026-05-27). **LangWatch**: https://langwatch.ai/blog/background-agents-before-claude-tag. **Cloudflare** (internal stack, 93% R&D adoption, Apr 2026, *exact post URL unverified*; summary: https://www.zenml.io/llmops-database/building-an-enterprise-ai-engineering-stack-with-internal-agents-and-mcp-infrastructure). **Zalando** (pydantic-ai CLI + chat UI): https://engineering.zalando.com/posts/2026/08/agentic-engineering-at-zalando-a-snapshot.html (Aug 2026). **Harvey** "Spectre", **Genentech**, **Airbnb** (agent cloud workspaces; workspace cost "nearly doubled in Q1"): Background Agents Summit listings and job posts, *unverified primary* | Runs agents unattended, in parallel, with full company context; output is merged PRs | Unattended execution plus deep integration with internal tools, devboxes and security. Stripe passed on Claude Code and Cursor for this reason | **Crowded.** Ona (formerly Gitpod, runners in your VPC), Cursor cloud agents, OpenAI Codex cloud, Claude Code web/Tag, GitHub Copilot coding agent, Devin, Factory, Tembo (self-host; Agent Studio OSS), Open-Inspect (OSS clone of Ramp Inspect, ~1.9k stars Jun 2026), Port/Sourcegraph pitch "software factory" | Builders 14+; vendors 10+; platforms own it → **medium-low** |
| 2 | **Single MCP/tool gateway with scoped permissions and audit** | Stripe Toolshed (~400-500 tools, one endpoint); DoorDash Agent Gateway (scoped perms, audit logs); Uber MCP Gateway; Cloudflare (13 MCP servers, 182 tools behind Access); Zalando (LiteLLM proxy) | Agents need internal tools without N separate servers and credentials | Internal APIs and auth are company-specific | **Crowded.** 14+ named vendors (DigitalAPI comparison), Obot, Kong, Cloudflare MCP portals, Docker, TrueFoundry, Akto, Runlayer, MintMCP. Same ground as round 7's MCP OAuth finding | Low |
| 3 | **Model/LLM gateway with cost tracking** | Zalando (LiteLLM proxy, cost + caching); Uber model gateway; Cloudflare AI Gateway internal (241B tokens/mo) | Central key management, spend per team, caching | Mostly they *did* buy or use OSS (LiteLLM, own product) | **Crowded.** LiteLLM, Portkey, Cloudflare, Kong, OpenRouter. Thesis B already killed | Low |
| 4 | **Risk-based PR auto-approval / review routing for agent PRs** | Vercel, 58% merge without human review: https://vercel.com/blog/58-percent-of-prs-in-our-largest-monorepo-merge-without-human-review (2026-04-06). Zalando, 33% low-risk auto-approved, lead time -20-40% (Aug 2026). Augment Cosmos: https://augmentcode.com/blog/solving-code-review-with-cosmos *(date unverified)*. Rewind: https://rewind.com/blog/ai-approve-pull-requests-safely/ *(date unverified)*. Ona's own: https://ona.com/stories/auto-approving-low-risk-prs (lead time -74%). Uber uReview, 90% of 65k diffs/wk | Review is now the bottleneck at agent PR volume | Risk rules are org-specific; it was cheap to build on an LLM classifier | **Shipped by vendors.** Cursor approval agents (docs Jun 2026), Graphite, MergeShield, CodeAnt, GitHub. **Same as killed thesis T3** | Low (killed) |
| 5 | **Playbook / recurring-agent-job catalog** (YAML: task, tools, permissions, validation, safety; triggers via cron/Slack/GitHub) | DoorDash Flux, 300+ playbooks, 10k runs/wk (2026-08-11); Monzo one-shot jobs (alert investigation, team responder, code review); LangWatch, 7 scoped agents per Slack channel; Spotify Fleet Management prompts; Uber Shepherd/Autocover; LiteLLM backlog agent | Turns recurring engineering chores into governed, repeatable agent runs | Built as part of #1 | **Platform-owned.** GitHub Agentic Workflows, Ona Automations, Claude Code routines, Devin playbooks, Tembo Agent Studio (agent definitions in Git), Cursor automations *(unverified)* | Medium-low |
| 6 | **Fleet-wide migration campaigns** (one prompt → PRs across hundreds of repos, tracked to merge) | Spotify Honk/Fleet Management (1,500+ PRs); Uber Shepherd (250+ migrations, 9M LOC); Airbnb (Enzyme → RTL, 1.5 yrs → 6 wks); Google (39 migrations, 74% AI edits); Anthropic: https://claude.com/blog/ai-code-migration (2026-07-21) | Long-tail migrations that deterministic codemods could not finish | Existing fleet tooling was extended | **Vendors live.** Sourcegraph Agentic Batch Changes (beta Jun, GA 2026-09-14, outcome pricing), Moderne, Claude dynamic workflows | Low-medium |
| 7 | **Verification layer for unattended agents** (deterministic verifiers + LLM scope judge + CI cap) | Spotify Part 3: https://engineering.atspotify.com/2025/12/feedback-loops-background-coding-agents-part-3 (judge vetoes ~25% of sessions; half self-correct); Stripe (two-round CI cap, fast local lint); Ramp (agent proves its own work in a full env); Airbnb AirDev pre-CI validation; Shopify Dispatch (security findings must be "proven by exploit"); Uber Autocover | Unattended agents drift out of scope or "pass" without proof | Verifiers are per-repo, per-language | **Partly covered.** Review bots (CodeRabbit, Greptile, Cursor Bugbot), generic evals (excluded), Signadot (agent validation in K8s), test-impact vendors. No product owns "scope judge + verifier stack for background agents" | **Medium** (best gap, but feature-sized) |
| 8 | **Agent identity / registry** (every agent action traceable to a person) | Uber Agent Registry: https://www.uber.com/blog/solving-the-agent-identity-crisis/ *(date unverified)*; DoorDash gateway audit | Accountability and audit for agent actions | Ties to internal workload identity (K8s/SPIFFE) | **Crowded.** Okta, Astrix, Aembit, etc.; generic agent security is excluded | Low |
| 9 | **Skills / context marketplace** (governed registry of SKILL.md across agents) | AutoScout24: https://tech.autoscout24.com/blog/posts/designing-a-coding-agent-skills-marketplace/; Sanity: https://www.sanity.io/blog/skills-are-how-your-company-works; Uber skills marketplace; Zalando skill libraries; Cloudflare AGENTS.md for ~3,900 repos + "Engineering Codex" | Shares tribal knowledge with every agent | It's a Git repo plus a sync script | **Platform-owned + vendors.** Anthropic org skills, TrueFoundry registry, skills.sh, Factory Agent Readiness. Round 7 #6 scored it 5.0 | Low |
| 10 | **Context graph for agents** | Uber company-wide context graph; Shopify (public Slack channels as agent memory) | Agents fail on retrieval, not on reasoning | Org data is spread out | **Crowded.** Unblocked, Postman, Harness, Port, Sourcegraph, Augment, Glean | Low |
| 11 | **Multi-agent worktree orchestrator for one engineer** | Coinbase Mux (5,000+ PRs, 3.5x baseline) | Runs several agents in parallel without conflicts | Started as a side project | **Crowded.** Conductor, Vibe Kanban, Crystal, Superset, Cursor multi-agent | Low |
| 12 | **AI impact measurement** | Uber (published account of what measurement got wrong); Shopify (refuses to count AI LOC); Zalando (PR size and complexity impact) | Proving that agents improve outcomes | Wanted honest metrics | **Crowded.** DX, Jellyfish, Faros, Span, LinearB, Swarmia, Larridin; Greptile agent leaderboard | Low |
| 13 | **Provenance: which agent/session wrote this commit** | Uber registry (traceable to person); implied for regulated firms (Monzo, Coinbase) | Audit and debugging of agent-authored code | n/a | OSS (Semantica, lore, Agent Trace spec), git-native vendors; thin | Low-medium (pre-demand) |

**How to read the table:** the builder counts are real: 14+ for #1, 6+ for #5/#6/#7, 5 for #2/#4. But for every type with 5+ builders, a vendor or platform shipped a product in 2026, usually after the internal build had been written up. That fits STATUS.md conclusion #1: gaps that public sources can see get filled within about 6 months. Writing up an internal platform is itself the signal vendors copy. Open-Inspect, Ona's white paper on Stripe and Ramp, and Port's "software factories" series are all vendors or open-source projects turning these posts into products.

---

## Candidate 1: "Minions-in-a-box": a self-hosted background-agent control plane for companies with 100-2,000 engineers

**Problem.** Stripe, Ramp, DoorDash, Uber and Shopify each spent 4-15 engineers building the same stack: sandbox, harness, tool gateway, playbooks, triggers, verification. Companies one size down (100-2,000 engineers) see the results (30-75% of PRs agent-authored) but can't fund a 4-person platform team. Vendor cloud agents (Cursor, Codex, Copilot) don't reach internal tools, private networks or company devboxes.

**Recent evidence (5+ independent signals).**
1. Stripe Minions, 1,300+ PRs/wk, built because no off-the-shelf tool ran unattended (InfoQ, Mar 2026).
2. Ramp Inspect: 4 engineers + a part-time PM, 3 of 4 merged PRs (Modal blog 2026-02-19; Port profile).
3. DoorDash Flux: 130k tasks/month, Firecracker sandboxes with p95 setup under 5 s, YAML playbooks, Agent Gateway (2026-08-11).
4. Monzo Agent Chip, built "to maintain flexibility and full control" (2026-08-13).
5. LiteLLM, a small company, built one that covers 30% of its backlog (2026-05-27).
6. Coinbase Mux, Uber Minion, Shopify River, Cloudflare, Zalando, LangWatch.
7. Airbnb: agent cloud-workspace cost nearly doubled in Q1 (job/DPE material, unverified primary).

**Who has the pain.** VP Eng or Head of Developer Productivity at software companies with 200-2,000 engineers, a platform team, and a security team that blocks SaaS agents from touching production-adjacent systems.

**What they do today.** Pilot Cursor or Codex cloud agents on a few repos, or fork Open-Inspect or Goose, or ask the platform team for a "Minions" project.

**Why current products fail.** SaaS agents run outside the VPC and don't have internal MCP tools, real dev environments or org playbooks. Ona comes closest (runners in your VPC, automations), followed by Tembo (self-host). Open-Inspect is free but needs DIY ops.

**Why now.** Stripe, Ramp and DoorDash published their designs in Feb-Aug 2026. The 2026 Background Agents Summit (May 6-7) and the "software factory" framing are now standard VP Eng talking points.

**Potential product.** A control plane deployed in your VPC that includes:
- warm sandboxes from your devbox image
- a harness-agnostic runner (Claude, Codex or Goose)
- YAML playbooks with permissions and verifiers
- a Slack/GitHub/cron trigger router
- per-playbook success, cost and merge-rate dashboards

**Time to value.** 2-4 weeks: the first playbook (dependency bumps or flaky-test fixes) produces merged PRs.

**Pilot (14-30 days).** One repo and 3 playbooks. Target: 50+ merged agent PRs, and verifier pass rate and reviewer time per PR measured.

**Willingness to pay.** Real but contested. Budgets exist (Airbnb's spend doubled). Buyers compare against Cursor or Codex seats they already pay for, and against an open-source fork that costs zero.

**Expansion.** More playbooks, more repos, non-engineering users (PMs and designers already use Ramp's and Coinbase's tools), incident and alert playbooks.

**Competition.** Ona (best-funded and closest fit; it published the Stripe/Ramp white paper), Cursor cloud agents, Codex, Claude Code web/Tag/routines, GitHub Copilot coding agent plus Agentic Workflows, Devin, Factory, Tembo, Open-Inspect, Sourcegraph, Port. **Crowded, and the platforms are moving in.**

**Moat.**
- 10 customers: playbook library.
- 100 customers: cross-customer data on which playbooks merge.
- 1,000 customers: a verified playbook marketplace.

All three are weak against model labs that own the harness.

**CTO test sentence.** "Get Stripe's Minions inside your VPC in two weeks, without a 4-person platform team."

**Kill test question.** Would a 500-engineer company pick this over Ona's VPC runners or Cursor cloud agents with self-hosted runners at equal price? If the main reason is "integration with our tools", does that integration still have to be custom-built per customer, making it a services business?

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 7 | 8 | 6 | 4 | 6 | 6 | 2 | 3 | 8 | 6 | **5.7** |

---

## Candidate 2: Verification and scope gate for unattended agents (verifier stack + scope judge + CI budget)

**Problem.** Once agents run unattended, the expensive failures are PRs that pass CI but are out of scope, and CI loops that burn compute. Spotify's LLM judge vetoes about 25% of sessions. Stripe hard-caps CI at two rounds. Ramp, Airbnb and Shopify each built a "prove it" layer: a full-env check, pre-CI validation, or proof-by-exploit.

**Recent evidence.**
1. Spotify Honk Part 3: deterministic verifiers with regex-trimmed errors, plus an LLM judge that vetoes a quarter of sessions; half of those self-correct (Dec 2025).
2. Stripe two-round CI cap (Port/InfoQ 2026).
3. Ramp: the agent verifies its own work with Sentry, Datadog and browser (Feb 2026).
4. Airbnb AirDev validation before CI (job postings 2026).
5. Shopify Dispatch: 300+ security findings, each "proven by exploit".
6. Uber Autocover mutation testing; Augment Cosmos agent review team.

**Who has the pain.** Platform teams that already run background agents (#1 builders) and teams adopting vendor cloud agents.

**What they do today.** Per-repo scripts, an LLM-judge prompt, CI retry caps.

**Why current products fail.**
- Review bots comment after the PR is open. They don't sit inside the agent loop.
- Generic eval tools score models, not individual PRs.
- Test-impact tools handle test selection but don't judge scope.

**Why now.** Agent PR volume (Stripe 1,300/wk, Uber 1,800/wk) makes each false merge or wasted CI loop costly.

**Potential product.** A verifier SDK plus a hosted judge that runs inside any harness. It returns compact, agent-readable failures, enforces scope against the original prompt, applies per-playbook CI budgets, and logs veto and self-correct rates.

**Time to value.** Days, as a hook in an existing harness.

**Pilot.** Shadow mode for 14 days on an existing agent fleet. Measure the veto rate, and how many vetoed changes would have been reverted or rejected by a human.

**Willingness to pay.** Low to medium. It feels like a feature, and buyers expect it bundled into their agent platform.

**Expansion.** Policy packs (security, migrations), a cross-harness standard.

**Competition.**
- Cursor Bugbot and agent self-review, Claude Code adversarial review (Anthropic migration post: "three adversarial review rounds"), Greptile, CodeRabbit.
- Signadot for agent validation.
- Ona and Devin build verification into their platforms.

**Moat.** Weak. Veto-calibration data would be the only asset.

**CTO test sentence.** "Stop a quarter of your agent PRs before CI or a human ever sees them."

**Kill test question.** Do teams that run cloud agents from Cursor, Codex or Claude get this natively by mid-2027? Very likely yes.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 6 | 7 | 8 | 7 | 5 | 4 | 5 | 3 | 5 | 5 | **5.5** |

---

## Candidate 3: Playbook registry and ops for recurring agent work (cross-vendor)

**Problem.** DoorDash runs 300+ playbooks with 10k runs a week. Monzo, LangWatch, Spotify, Uber and LiteLLM each run a catalog of scoped, triggered agent jobs. Mid-size companies use 3-4 agent vendors (Coinbase Mux coordinates Cursor, Copilot, OpenCode and Claude Code). Nothing tracks which recurring agent jobs exist, who owns them, what permissions each has, their merge or success rate, or their cost, across vendors.

**Recent evidence.**
1. DoorDash Flux playbooks (YAML: task, tools, permissions, validation, safety) (2026-08-11).
2. Monzo's 5 one-shot job types (2026-08-13).
3. LangWatch's 7 Slack-scoped agents.
4. Spotify Fleet Management prompts.
5. Uber Shepherd, Autocover and uReview.
6. Coinbase Mux's multi-vendor coordination (Apr 2026).
7. Tembo Agent Studio: "agent definitions live in Git" (OSS May 2026, 3 stars, so demand is thin).

**Who has the pain.** Developer-productivity leads at companies with more than 3 agent tools and more than 20 recurring agent jobs.

**What they do today.** YAML in repos, cron and GitHub Actions, spreadsheets of bots.

**Why current products fail.** Each vendor's automations (GitHub Agentic Workflows, Ona Automations, Claude routines, Devin playbooks) only cover its own agent.

**Why now.** Recurring agent jobs went from 0 to hundreds per company in 2026.

**Potential product.** A Git-native playbook registry with a cross-vendor runner adapter, a permission manifest per playbook, and a scorecard per playbook (merge rate, revert rate, cost, reviewer minutes).

**Time to value.** 1-2 weeks.

**Pilot.** Inventory and score a company's existing agent jobs in 14 days.

**Willingness to pay.** Low. Buyers say "that's an internal YAML repo". Only companies with more than 100 playbooks feel it, and those build their own.

**Competition.** GitHub Agentic Workflows, Sourcegraph Agentic Batch Changes, Ona, Claude routines, Tembo, Port (an agent-catalog angle is likely).

**Moat.** A shared playbook library, but it has no network effect, because playbooks are company-specific.

**CTO test sentence.** "Know every recurring agent job you run, who owns it, what it can touch, and whether it's worth its cost."

**Kill test question.** At 100-5,000 engineers, does anyone run enough recurring agent jobs, across enough vendors, to pay for a registry within 12 months?

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 5 | 4 | 6 | 8 | 7 | 5 | 3 | 5 | 3 | 5 | 5 | **5.1** |

---

## Verdict

- **The method worked as a signal detector.** Background-agent platforms are the most independently rebuilt internal system of 2026: 14+ named builders, with similar architecture and similar metrics (30-75% of PRs). That is stronger convergence than anything found in rounds 1-7.
- **It failed as a gap detector.** Builders posted Nov 2025 to Aug 2026. Vendors and open-source projects (Ona, Open-Inspect, Tembo, Sourcegraph Agentic Batch Changes, Cursor approval agents, GitHub Agentic Workflows) shipped in parallel. Every layer with 5+ builders has 3+ vendors. The stated reason for building, deep custom integration, means the next 1,000 companies will either buy a platform vendor and integrate it themselves, or hire services.
- **Nothing is genuinely strong.** Best average 5.7, no category at or above the 8.5 bar, competition at or below 5 everywhere. The only gap without a clear vendor is #7 (verification/scope judge), and it is feature-sized.
- **One useful byproduct:** the agent platform team at companies like Stripe, DoorDash and Uber is now a real buyer persona with budget. Any future thesis should be tested by asking whether that team would build it in a sprint. All 13 types above fail that test.
