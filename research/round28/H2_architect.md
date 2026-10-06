# H2 (architect view): what breaks in software delivery at 100x agent output, and the missing primitive

*Round 28. 2026-10-06. Role: technical infrastructure architect. 22 web searches (the shared per-turn search budget ran out after that, so three follow-up checks did not run: admission-control products, BuildBuddy/EngFlow agent load, and the full "When Agents Collide" write-up). WebFetch was blocked, so every fact comes from search-result snippets. [unverified] means I saw it in a single secondary snippet only. I did not invent any URLs.*

**Verdict: weak, conditional B (avg 6.6). Not A.** The missing primitive is **concurrency control for engineering intent**: a scheduler that sees every agent task before code exists, predicts what code it will touch, and decides whether to admit it, hold it behind another task (serialize), fold it into a duplicate, or drop it, based on contention and on verification capacity (CI, merge-queue slots, reviewer minutes). It also records what each shipped change cost. The architectural case is strong. The market case is weak: OSS fragments and single-vendor features already cover parts of it, and GitHub could absorb it. It survives only as the cross-vendor, org-wide version, and only if the replay test below shows large waste.

---

## 1. Push to 2028-2029: what actually breaks

Starting point (2026): agent-opened PRs on GitHub went from ~4M (Sep 2025) to 17M+ (Mar 2026). Uber reports ~70% of PRs agent-opened, Stripe ships 1,300+ agent PRs a week, and more than 80% of Anthropic's merged code is written by Claude (round 8; letsdatascience). Push that to 100x: 1,000-engineer orgs with 10k-50k agent tasks a day, from 3-5 vendors (Cursor, Claude Code, Codex, Copilot, internal Minions), all against the same monorepos.

| Layer | Designed for | What happens at 100x | Order of consequence |
|---|---|---|---|
| **Git branch model** | Few long-lived human branches. Optimistic concurrency: work in isolation, reconcile at merge | Optimistic concurrency control (OCC) collapses under high contention. In databases, abort and retry rates grow superlinearly once concurrent transactions overlap in hot rows. Hot modules (auth, billing, shared types, API schemas) become hot rows. AgenticFlict already measures **27.67% textual conflicts** across 107k simulated agent PRs, averaging 11.36 conflict regions per conflicting PR, at today's concurrency | 1st: rebase storms. 2nd: every rebase re-runs CI. 3rd: in hot zones CI cost grows roughly with N², not N |
| **Merge semantics** | Line-level three-way merge | Clean textual merges hide semantic breakage: one agent renames or replaces an interface while another still extends or calls it. The STALE benchmark ("Passes Alone, Fails Together", EXPRESS '26, Oct 2026) formalizes this. Foremerge's canonical example: one agent replaces PaymentService while another extends it, Git merges cleanly, and the second agent's work is stranded | 2nd: green-CI-then-broken main. 3rd: incidents per PR +242.7% (Faros 2026) are partly integration failures, not authoring failures |
| **CI capacity** | Roughly 1 run per human push | 3-5x more CI minutes per developer than a year ago. One team's CI bill rose 130% in six weeks while per-PR dashboards looked normal [secondary: tianpan.co]. GitHub Actions hit 2.1B minutes in one week of 2026. Copilot review is now billed at Actions-minute rates (Jun 1 2026) | 2nd: CI becomes the binding budget line. 3rd: platform teams ration CI, which silently rations agents |
| **Merge queue** | Serial or lightly batched human PRs | Anthropic's merge queue became a delivery bottleneck after the jump in output (Krieger, via letsdatascience). Vendors respond with dynamic batching (Mergify, Jun 2026), path-partitioned parallel queues (Aviator) and optimistic merging (Trunk). Larger batches mean costlier bisection when a batch fails | 2nd: queue latency becomes the new lead time |
| **Work-item dependency** | Human tracker (Jira/Linear) with coarse issue links | Agents create sub-tasks faster than humans link them. Dependencies get discovered at merge time, not at planning time. Beads (17.9k stars) exists because agent sessions lose task state | 2nd: agents work on top of things that are about to change |
| **Conflict detection before code exists** | Nothing; humans coordinated in standups | Nobody knows two intents collide until both have burned tokens, CI and review minutes | **The core gap.** The only place to prevent waste instead of cleaning it up |
| **Reuse of partial work** | Abandoned branches rot | Agent PRs merge at **32.7% vs 84.4%** for humans (LinearB, 8.1M PRs), so about two-thirds of agent output is thrown away and the effective cost per shipped change is about 3x the cost per attempt. Abandoned branches often hold correct sub-pieces (a migration, a test, a refactor) that are never found again | 3rd: orgs pay repeatedly for the same partial solutions |
| **Provenance to intent and cost** | `git blame` → human | Entire Checkpoints and Cursor Agent Trace record which session wrote which lines. Nobody links **intent → all attempts → tokens + CI + reviewer minutes → shipped/abandoned** | 3rd: no cost per shipped intent, so no way to manage agent ROI |

**Macro symptom (key evidence):** Faros 2026 (22k devs, 4k+ teams) reports **+66% epics completed per developer**, median review time +441.5% and churn +861%. A secondary snippet (36kr) attributes a **-11.7% drop in weekly deployments** to the same report [unverified against Faros primary]. Output is rising while delivery stalls. That is the signature of a congested shared resource, not a slow author.

## 2. Second and third-order consequences (beyond "triage the pile")

1. **The waste is created at admission, not at merge.** Every downstream tool (review bots, auto-merge, merge queues, stale-PR closers) handles work that should never have started, or should have started after another task. Cleaning the PR pile is the surface pain (the "Public decoy" in DISCOVERY_MACHINE.md). The structural fix is to schedule work before generation.
2. **Verification capacity becomes the scarce resource that rations the whole org.** Token cost falls, while CI, merge slots and human attention do not. Whoever controls who gets to use verification capacity controls engineering throughput. This mirrors cluster scheduling (Borg/Kubernetes): once compute is shared and scarce, a scheduler becomes mandatory infrastructure.
3. **Optimistic → hybrid concurrency is a forced architectural transition.** Deterministic databases (Calvin-style) declare each transaction's read and write sets up front so the system can schedule without aborts. Agent tasks can do the same: a task's predicted footprint is its declared read/write set. Version control never needed this because humans were slow and few.
4. **Agent ROI becomes a board-level question without a ledger.** CFOs see token, CI and seat bills. VPs Eng see merged PRs. Nobody can say "this feature cost $X across 7 attempts by 3 vendors". The cost ledger falls out of the scheduler, because the scheduler sees every attempt.

## 3. Is this a new infrastructure category?

**Yes, architecturally.** Version control serialized *edits*. CI serialized *verification*. The missing layer serializes **intents**: a transaction manager for engineering work that sits between planning tools (Linear/Jira/Slack prompts) and execution (agents → Git → CI → merge queue). Call it an **Intent Scheduler** (admission control + intent-level locking + salvage + cost lineage).

**Commercially it is uncertain**, because the pieces are being built from both sides (section 6).

---

## 4. Finalist: Intent Scheduler, concurrency control for agent engineering work

### One-line problem
At agent scale, engineering orgs waste most of their token, CI and review capacity on work that collides, duplicates or gets abandoned, because nothing coordinates agent tasks before code exists.

### Why this problem exists now
- Agent PR volume grew more than 4x in 6 months (4M → 17M+/month on GitHub). Multi-vendor fleets are now normal (GitHub Agent HQ lets you @Copilot, @Claude or @Codex on the same issue; Coinbase Mux coordinates four vendors).
- Measured costs: 27.67% textual conflict rate (AgenticFlict), 32.7% agent merge rate (LinearB), CI minutes up 3-5x per developer, merge queues as a bottleneck (Anthropic).
- The behavior is starting **now** as OSS workarounds, all from Jun-Sep 2026: Foremerge (intent lifecycle INTENT→CLAIMED→…→COMMITTED with deterministic conflict rules), MCP Agent Mail (advisory file leases), Weave (entity claims over MCP), Clash (cross-worktree conflict warnings), conflict-check (launched Sep 2026), Beads/Flowcontrol/Werkgraph (agent task graphs), backlog-groomer agents that auto-close duplicate and stale PRs. Many independent builders, all local and single-machine, none org-wide. Per round 8, this is the pattern that comes just before a vendor category forms.

### Exact buyer
Head of Developer Productivity / Platform Engineering, with budget from the VP Engineering. The CFO co-signs when the pitch is "cost per shipped change". The same agent platform team round 8 identified as having real budget.

### Exact ICP
Software companies with 300-3,000 engineers, 1-3 large monorepos, more than 40% agent-authored PRs, two or more agent vendors plus an internal background-agent platform, GitHub or GitLab, Bazel/Nx/Turborepo-style build graphs, and CI spend above $1M/yr. Examples of the profile (not prospects contacted): Ramp, DoorDash, Coinbase, Monzo, Zalando, Datadog-scale orgs.

### Current workaround
- Merge queues with bigger batches (Mergify, Aviator, Trunk, Graphite).
- CI retry caps (Stripe's two-round cap).
- Stale-PR auto-closers and duplicate-groomer agents.
- Advisory OSS leases (Agent Mail, Weave).
- Single-vendor coordinators inside one product (Augment Intent's coordinator and living spec, Factory Missions, Cursor multi-agent).
- Linear duplicate detection at issue level.
- Humans in Slack saying "don't touch billing this week".

### Why incumbents cannot easily own it
- **Coding-agent vendors** (Cursor, Factory, Augment, Devin) only see their own agents. Coordination across vendors runs against their interest in winning the fleet.
- **GitHub** sees PRs and CI, but only after code exists. Pre-code intent lives in Cursor, Claude and Codex sessions and in Linear. GitHub is still the biggest threat, because Agent HQ is cross-vendor and it owns Actions plus the merge queue.
- **Linear/Jira** see intent but not code footprint, build graph or CI economics.
- **Merge-queue vendors** (Aviator, Trunk, Graphite-in-Cursor) act at the end of the pipe. Moving upstream to admission is a different product and a different buyer conversation.
- **Honest caveat:** none of these walls is high. A platform team could build a footprint-overlap check in a sprint. What it cannot build in a sprint is calibrated contention and salvage prediction trained on many orgs' outcomes.

### Architecture sketch

```
 Planning / triggers                         Execution
 Linear, Jira, Slack, cron,          ┌──────────────────────────────┐
 PM prompts, agent-spawned subtasks  │ Agent harnesses (Cursor,      │
            │                         │ Claude Code, Codex, Copilot,  │
            ▼                         │ internal Minions)             │
 ┌───────────────────────────────┐   │  pre-task hook / MCP tool:    │
 │ 1. INTENT LEDGER              │◀──┤  request_admission(intent)    │
 │ intent, owner, parent, value, │   │  heartbeat(live_diff)         │
 │ budget, state machine         │──▶│  lease granted / wait / merge │
 │ (proposed→admitted→leased→    │   └──────────────┬───────────────┘
 │  validated→merged|salvaged)   │                  │ commits / PRs
 └──────────────┬────────────────┘                  ▼
                │                         Git forge (GitHub/GitLab/Origin/Entire)
 ┌──────────────▼────────────────┐                  │
 │ 2. FOOTPRINT PREDICTOR        │                  ▼
 │ intent text + code graph      │        CI / build system / merge queue
 │ (symbols, call graph, build   │                  │  webhooks: minutes, failures,
 │ targets, CODEOWNERS, schema   │◀─────────────────┘  queue position, reverts
 │ contracts) → predicted read/  │
 │ write set at entity level;    │
 │ refined from live diffs       │
 └──────────────┬────────────────┘
 ┌──────────────▼────────────────┐   ┌───────────────────────────────┐
 │ 3. CONTENTION + CAPACITY      │   │ 4. SALVAGE INDEX              │
 │ ENGINE                        │   │ abandoned/failed attempts     │
 │ pairwise overlap of write/read│   │ split into entity-level       │
 │ sets; contract-change vs      │◀─▶│ patches + tests; offered to   │
 │ caller rules; CI-minute, queue│   │ new intents with overlapping  │
 │ slot, reviewer-minute budget  │   │ footprint                     │
 │ → ADMIT / SERIALIZE (lease) / │   └───────────────────────────────┘
 │ FOLD (dedupe) / SPLIT / DROP  │
 └──────────────┬────────────────┘
 ┌──────────────▼────────────────┐
 │ 5. LINEAGE + COST LEDGER      │  intent → attempts → tokens + CI + review min
 │ (ingests Agent Trace / Entire │  → shipped | reverted | abandoned
 │ Checkpoints where present)    │  → cost per shipped intent, per team/vendor
 └───────────────────────────────┘
```

Design choices:
- **Leases are entity-level and time-bounded**, not file locks. Pessimistic control applies only in hot zones; everything else stays optimistic.
- **Contract rules are deterministic** (Foremerge-style: destructive vs additive edits on the same symbol, interface change vs live callers in other intents). The LLM only proposes the predicted footprint and never makes the blocking decision, so outcomes are explainable.
- **Shadow mode first**: it predicts and logs without blocking, so the ROI can be proven from the customer's own history before it touches anyone's workflow.

### 30-day MVP
1. GitHub App plus a CI webhook ingester, and an MCP server / pre-task hook for Claude Code, Codex and Cursor (all support hooks or MCP).
2. Footprint predictor for one language family (TypeScript or Python) using tree-sitter entity graphs plus build-graph targets.
3. **Replay engine**: ingest 90 days of PRs, branches, CI runs and agent session metadata. Reconstruct which concurrent tasks overlapped, what CI ran on rebases and re-runs, and which abandoned branches contained entities later rewritten.
4. Output: a "waste report" ($ of CI, tokens and reviewer minutes spent on collided, duplicated or abandoned work, plus salvageable patches), then live shadow-mode advisories posted to the agent and in Slack.

### Pilot design (replay-first; no interviews needed)
- **Days 1-7:** connect read-only to one ICP org's GitHub org, CI provider and one agent platform's logs. Run the 90-day replay.
- **Days 8-21:** shadow mode on live agent tasks: predict footprint at task start, flag collisions, duplicates and salvage candidates, and score predictions against what actually happened at merge.
- **Days 22-30:** turn on enforcement for one hot zone (e.g., billing or shared types): leases plus fold-duplicates.
- **Success metrics:**
  - Replay attributes ≥20% of agent-related CI minutes to rebases or re-runs from collisions plus abandoned work.
  - Shadow precision ≥70% on predicted collisions.
  - In the enforced zone, CI minutes per merged change fall ≥25% and merge-queue failures fall ≥30%.

### Pricing hypothesis
- Platform fee $40k-$150k/yr by engineer band, plus usage at roughly $0.02-0.05 per admitted intent.
- Alternative for CFO-led buys: 20% of measured CI and token savings for year one, converting to a fixed fee.
- At 1,000 engineers × 20 intents/engineer/day, usage alone is about $100k-250k/yr. That has to stay below the CI savings: a 1,000-engineer org at $3-6M CI/yr saving 25% is $0.75-1.5M.

### Expansion path
Waste report → shadow advisories → hot-zone leases → org-wide admission control with priority (the "Borg for engineering work") → salvage marketplace inside the org → cost-per-shipped-intent ledger as the system of record for agent ROI (CFO/FinOps) → planning interface (intents decomposed and scheduled automatically, which is the long-run replacement for sprint planning) → policy (which vendor or model gets which intent, given historical success per footprint).

### Moat
- **10 customers:** integrations across 3-5 agent vendors plus CI providers. Weak.
- **100 customers:** calibration data. Which footprints actually collide, which intents salvage well, contention-versus-waste curves by repo shape. This data exists only for whoever sees pre-code intent and post-merge outcome across vendors.
- **1,000 customers:** becomes the system of record for intent → cost lineage. Planning tools and agent vendors write to it, much as CI became the place every tool reports status. Switching then means losing the cost history and the scheduler's learned priors.
- **Honest view:** a data moat in coordination is unproven. Git, CI and merge queues were all commoditized or bundled.

### Why it could become a $10B+ company
If agent fleets make verification capacity the scarce resource in software production, the scheduler of that capacity becomes the control point, as cluster schedulers did for compute and CI did for quality. It sits on every unit of engineering work across all vendors, so its natural expansion runs into planning (Jira/Linear's $10B+ category), FinOps for agent work, and delivery (merge, release). Comparable outcomes: GitHub ($7.5B in 2018), Atlassian, HashiCorp (neutral infrastructure across clouds, analogous to neutral across agent vendors). **This requires** (a) a multi-vendor agent world that persists, and (b) GitHub not shipping a good-enough pre-code admission layer inside Agent HQ. I put (b) at ≥50% likely by 2028.

### Direct competitors and adjacent threats
| Player | Overlap | Threat |
|---|---|---|
| GitHub Agent HQ + Actions + merge queue | Cross-vendor assignment, audit, CI, queue. Missing pre-code footprint and cost lineage | **High** (absorption) |
| Linear (coding sessions, duplicate detection, triage automations) | Owns intent intake and dedupe at issue level | High |
| Augment Intent (coordinator, living spec, verifier) | Pre-code planning and coordination, single workspace | Medium-high |
| Factory Missions | Multi-agent scheduling with milestones, within Factory | Medium |
| Cursor (Origin + Graphite merge queue + multi-agent) | Forge + queue + agents under one vendor | High for Cursor-only shops |
| Entire (Checkpoints, semantic layer roadmap) | Provenance; "semantic inference layer" could extend to coordination | Medium-high |
| Aviator / Trunk / Mergify | Path-partitioned parallel queues, dynamic batching | Medium (could move upstream) |
| OSS: Foremerge, MCP Agent Mail, Weave, Clash, conflict-check, Beads, Flowcontrol, Werkgraph | Exactly the primitive, locally | Medium (commoditizes the protocol, validates the behavior) |
| Faros / DX / Jellyfish | Measurement, could add a "waste" report | Low-medium |
| Bazel ecosystem (BuildBuddy, EngFlow) | Own build graphs and affected-target data | Low-medium [not checked: search budget ran out] |

### One sentence to send a CTO
"Give us read access to 90 days of your repos, CI and agent logs, and we'll show you how many dollars of CI, tokens and review time went to agent work that collided, duplicated or got abandoned. Then we'll prevent it by scheduling agent tasks before they write code."

### Hard kill criteria
- The replay at 2 ICP orgs attributes <10% of agent-related CI and token spend to collision, duplication and abandonment (the waste is too small to fund a scheduler).
- Shadow-mode collision precision stays below 60% after 3 weeks (footprints can't be predicted before code exists, so the layer degrades into post-hoc conflict detection, which is a feature).
- GitHub announces pre-code task leasing or footprint-based admission in Agent HQ at Universe (Oct 28-29 2026), or Linear ships code-footprint dedupe.
- Platform teams at both pilot orgs say "we'll build the overlap check ourselves" after seeing the waste report (fails round 8's sprint test).
- Fewer than 50% of ICP orgs run two or more agent vendors (no neutrality premium).

### Scores (honest)
| Criterion | Score | Why |
|---|---|---|
| Pain | 7 | Measured waste (27.67% conflicts, 32.7% merge rate, CI 3-5x) but spread across budget lines; nobody's single top pain |
| Urgency | 6 | Felt at Anthropic/Uber/Stripe scale today; most ICP orgs are 6-18 months from it |
| ROI clarity | 6 | CI and token savings are measurable via replay; reviewer-time and salvage value are softer |
| Customer accessibility | 7 | Platform/DevEx teams are reachable and buy infrastructure; read-only GitHub App onboarding |
| Pilot speed | 8 | Replay on historical data gives a result in days without changing workflow |
| Market size | 7 | Every AI-native eng org eventually; near-term ICP ~2-5k orgs × $100-300k |
| Expansion | 8 | Admission → scheduling → planning → agent FinOps → policy |
| Venture potential | 7 | "Borg/transaction manager for engineering work" is a clean VC story, but sits next to killed T3/G |
| Defensibility | 5 | Calibration data is plausible but unproven; OSS protocols exist; GitHub/Linear can bundle |
| Why now | 8 | Behavior visibly starting Jun-Sep 2026 (8+ OSS tools, the STALE benchmark, CI bill shock) |
| Competition position | 4 | No org-wide cross-vendor commercial owner found, but strong adjacent owners on every side |
| **Average** | **6.6** | Three categories below 7; fails A |

*(Sum 73/11 = 6.6.)*

### Classification: **weak B (conditional), not A**
- **Why B rather than KILL:** the specific layer (org-wide, cross-vendor, pre-code admission control with cost lineage) has no commercial owner I could find. The behavior is emerging right now as many independent local OSS workarounds, which is the round 8 precursor pattern. And the architectural argument (optimistic concurrency collapses at high contention, so verification capacity needs a scheduler) holds regardless of which vendor wins.
- **Why not A:** competition position (4) and defensibility (5). GitHub Agent HQ and Linear are each one roadmap item away, and the replay may show the waste is real but too small (<10%) to fund a separate layer.
- **Estimated odds the replay test passes:** ~20-25%.
- **Precise test (replaces interviews):** 90-day replay at 2 ICP orgs plus 3-week shadow mode. Pass = ≥20% of agent-related CI minutes attributable to collision, duplication or abandonment, AND ≥70% collision precision, AND at least one org commits ≥$50k to move to hot-zone enforcement.

### Rejected adjacent framings (for the record)
- **"Stale/duplicate agent PR triage queue"**: surface pain, feature-sized. Groomer agents already exist and Linear dedupes issues. KILL.
- **"Semantic merge driver"**: Weave and Mergiraf are free OSS, and semantic merging also lands inside forges. KILL.
- **"Provenance of agent code"**: Entire Checkpoints ($60M) and Cursor Agent Trace spec. KILL (killed G territory).
- **"CI cost control for agents"**: Trunk, Depot and Blacksmith plus GitHub repricing; generic FinOps was killed (thesis B). KILL as standalone; it survives only as the cost ledger inside the scheduler.
- **"Single-workspace multi-agent coordinator"**: Augment Intent, Factory Missions, Superset, Conductor. Killed as generic orchestration.

---

## Sources (from search snippets; not opened)
- AgenticFlict dataset: https://arxiv.org/pdf/2604.03551 ; https://huggingface.co/papers/2604.03551 ; https://news.creeta.com/en/multi-agent-worktree-merge-train-2026/
- STALE / "Passes Alone, Fails Together" (EXPRESS '26): https://arxiv.org/pdf/2609.25396
- "When Agents Collide" (33,596 PRs): https://codex.danielvaughan.com/2026/07/28/agent-pr-merge-conflicts-concurrent-coding-agents-codex-cli-worktree-isolation-coordination-defence/ (content not retrieved)
- Multi-agent coordination problem: https://codex.danielvaughan.com/2026/06/06/multi-agent-coordination-problem-concurrent-agents-semantic-conflicts-codex-cli/
- Foremerge: https://users.rust-lang.org/t/foremerge-a-git-like-coordination-protocol-for-parallel-coding-agents-one-binary-sqlite-deterministic-conflict-rules/142084 ; https://www.everydev.ai/tools/foremerge
- conflict-check: https://www.indiehackers.com/product/conflict-check
- MCP Agent Mail: https://github.com/Dicklesworthstone/mcp_agent_mail
- Weave (Ataraxy Labs): https://www.sourcepulse.org/projects/25659037 ; https://hn.nuxt.dev/item/47241976
- Beads: https://www.morphllm.com/beads-agent-memory ; https://steve-yegge.medium.com/introducing-beads-a-coding-agent-memory-system-637d7d92514a
- Flowcontrol: https://flowcontrol.readthedocs.io/ ; Plane work graph: https://plane.so/blog/the-work-graph-for-ai-agents-the-missing-layer-in-agentic-work
- Duplicate/stale PR groomer agents: https://git.cleverthis.com/cleveragents/cleveragents-core/pulls/1325 ; HF agent contributions: https://huggingface-open-source-agent-contributions.hf.space/
- Entire Checkpoints: https://futurumgroup.com/insights/selling-agent-provenance-to-the-cio-entire-changes-who-signs/ ; https://ostechnix.com/entire-cli-git-observability-ai-agents/
- Agent Trace: https://www.infoq.com/news/2026/02/agent-trace-cursor ; https://agent-trace.dev/
- GitHub Agent HQ: https://siliconangle.com/2025/10/28/github-tackles-vibe-coding-chaos-control-center-ai-coding-agents/ ; https://venturebeat.com/ai/githubs-agent-hq-aims-to-solve-enterprises-biggest-ai-coding-problem-too
- Linear agents/coding sessions: https://linear.app/enablement/guides/coding-sessions ; https://blog.buildbetter.ai/linear-ai-agents-2026-guide-5-alternatives-for-engineering-teams/
- Augment Intent: https://www.augmentcode.com/blog/intent-a-workspace-for-agent-orchestration
- Factory Missions: https://www.plushcap.com/content/factory/blog/factory-introducing-missions
- CI bill: https://tianpan.co/blog/2026-06-02-the-coding-agent-ci-bill-that-doubled-without-a-postmortem (secondary) ; https://tenki.cloud/blog/hidden-ci-tax-ai-coding-agents
- Merge queues: https://trunk.io/blog/merge-fast-or-merge-cheap-fine-tuning-merge-queues-to-handle-an-increase-in-prs-f ; https://mergify.com/blog/dynamic-merge-queue-batch-size ; https://aviator.co/merge-queue ; https://graphite.dev/blog/the-first-stack-aware-merge-queue
- Anthropic output/merge-queue bottleneck: https://letsdatascience.com/blog/claude-writes-80-percent-of-anthropics-code-brake-pedal ; https://eu.36kr.com/en/p/3943294418009475 (Faros -11.7% deployments figure, unverified)
- Faros 2026: https://faros.ai/research/ai-acceleration-whiplash ; https://vibegraveyard.ai/story/faros-ai-acceleration-whiplash-study/
- LinearB 32.7% merge rate: via https://codex.danielvaughan.com/2026/07/09/agentic-pull-requests-merge-reject-conflict-data-codex-cli-auto-review-agents-md-pr-workflow/ and round3/T3
- Superset/Superplane seed: https://neuronfeed.com/category/ai-agents?page=12 (aggregator)
- Prior corpus: research/round8/G_agent_source_control.md, research/round8/internal_platforms.md, research/round3/T3_autonomous_merge.md
