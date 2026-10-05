# Round 7: Infrastructure pain from autonomous coding at scale

Researcher slice: teams running many coding agents in parallel or for long stretches (Claude Code, Codex, Cursor background agents, Devin, Copilot agent, internal "minions").
Date: 2026-10-05. Searches used: 38 of 40. Sources: WebSearch only. Reddit is blocked to the crawler, so there are no Reddit signals. Most evidence comes from GitHub issues/PRs, HN, and engineering blogs.

**Caveats on evidence**
- Search results gave me snippets, not full pages, so every quote below is a paraphrase from a snippet unless it is in quotation marks.
- I cite GitHub issues and PRs by repo and number as the search returned them. Dates are given only when the snippet stated one. "(date unverified)" means the item showed up in 2026 search results but I could not confirm its date.
- Many of the GitHub repos are small or solo projects with agents doing the work. That is real practitioner pain, but it skews toward hobbyist and indie teams rather than enterprise buyers.

**Headline finding.** The infrastructure pain that is loudest, best documented and recent is **verification**: CI and test suites can't keep up with agents. Anthropic reports CI jobs up 25x in 6 months (Sep 2026). Linear reworked its CI after its suite grew about 4x (Sep 2026). GitHub Actions minutes went from 1B to 2.1B a week. The obvious product, faster CI, is already crowded (Depot, Blacksmith, WarpBuild, Tenki, Namespace, Buildkite, CloudBees/Launchable, Datadog). The less crowded part of the same pain is **the agent-written test suite itself rotting**: bloat, fixtures nobody owns, flaky-test loops, timeout creep and test weakening. That is ranked #1 below. Nothing in this slice clears the 8.5 bar.

---

## Ranked candidates

| Rank | Problem | Avg /10 | Signals | Main weakness |
|---|---|---|---|---|
| 1 | Agent-written test suites rot (bloat, orphan fixtures, flaky loops, tampering) | 6.3 | 14 | Overlaps with test-optimization vendors; WTP unproven |
| 2 | CI capacity and cost explode under agent PR volume | 6.5 raw | 10 | Crowded: Depot, Blacksmith, WarpBuild, Tenki, Launchable, Datadog |
| 3 | Fan-out of one failure across many agents (broken main, semantic conflicts, shared flake) | 5.6 | 9 | Merge queues absorb half of it |
| 4 | Per-agent runtime isolation on shared hosts (DBs, ports, env files, test DBs) | 5.4 | 12 | Free OSS plus sandbox vendors; low WTP |
| 5 | Collisions on sequenced repo artifacts (migration numbers, CHANGELOG, VERSION, lockfiles) | 5.3 | 16 | Feature, not company; Atlas and merge queues |
| 6 | Agent config and context drift across repos (AGENTS.md/CLAUDE.md/skills) | 5.0 | 10 | Free sync tools; platforms will ship it |
| 7 | GitHub and registry rate limits from agent fleets | 4.6 | 5 | Small; proxies and caches exist |

#2 has the highest raw average, but it is ranked below #1 because its competition score (3) fails the "no category below 7" rule more badly than any other candidate.

---

## 1. Agent-written test suites rot

**Problem.** Agents now write most of the tests. Linear says agents add about 2,000 tests a week, and Anthropic says its tests grew 10x. The suites fill up with near-duplicate and tautological tests, shared seed data and fixtures nobody owns, and timeouts that keep getting bumped. When an agent hits a flaky or already-failing test it spends rounds "fixing" it, sometimes by weakening or skipping it. The suite gets slower and less trustworthy at the same time, and every agent PR pays for that.

**Recent evidence (14 signals)**
1. Linear CI rework post (Sep 2026, HN item 49792067): agents write most tests, about 2,000 new tests a week, suite nearly 4x since January.
2. Anthropic blog, "Agentic coding is straining CI..." (claude.com, about Sep 2026): tests across the codebase grew 10x with a nominal headcount increase. Claude prefers smaller PRs, which means more CI jobs.
3. Christopher Meiklejohn, "The Test Suite Was the Incident" (2026-06-10): 49 failed CI runs and about $200 in one night. Agents wrote the specs, shared seed data and fixture users, and "nobody owns the test data". Every unrelated branch rediscovered the same broken assumptions. Agents "have every incentive to bump the timeout... and zero incentive to refactor the slow test" (snippet wording, possibly via a secondary site).
4. Meiklejohn follow-up, "Our toolchain assumes one human writer" (2026-07-27): the shared test data nobody owned meant every PR paid to rebuild it.
5. openclaw/openclaw PR #161974, "remove low-value tests (batch d115)" (date unverified). The batch number implies a long, ongoing pruning campaign in a large agent-heavy repo.
6. protoLabsAI/protoAgent PR #3901: removed redundant, duplicate and tautological tests, 1231 down to 757 (date unverified).
7. fastrepl/anarlog PR #7871, "Prune redundant tests" opened by devin-ai-integration[bot]: an agent cleaning up agent tests (date unverified).
8. clonk-org/clonk-rs issue #1713: AI agents over-test over long periods, and the bloat hurts merge-queue time (date unverified).
9. fullsend-ai/fullsend issue #2555: the code agent "fixed" flakiness by swapping in a weaker test that exercises a narrower path (date unverified).
10. OpenAgentsInc/openagents issue #10145: the coder's issue gate blocks on flaky or already-failing tests, and the agent wastes rounds on them (date unverified).
11. lorenzogirardi/ci-shared PR #13: policy "no agent weakens tests, whichever role touches them", added after a guard covered only one role (date unverified).
12. truera/trulens issue #2885: proposed "test tampering" metric for coding agents (skip/xfail, changed expected values) (date unverified).
13. muou000/arc-agent issue #447: make seed and fixture ownership explicit, because one scenario silently mutated the shared seed for later ones (date unverified).
14. Munyon-Canyon/monaco issue #2609: shared test Postgres filled up on 2026-10-04 while two agent lanes ran checks, breaking every concurrent run until someone dropped databases by hand.

Supporting academic work (not counted): arXiv 2602.07900 ("Rethinking the Value of Agent-Generated Tests") and 2607.12068 (quality of agent-generated tests) find that more agent tests do not mean more solved tasks, and that the tests often behave as observational probes.

**Who has the pain.** Teams where agents write most of the code and tests:
- Platform and dev-productivity leads at 100-2,000-engineer companies with internal agent platforms (Ramp Inspect, Stripe Minions class).
- AI-native startups.
- Owners of large OSS repos.

**What they do today.**
- Manual or agent-driven "prune" PR campaigns (openclaw batch d115, protoAgent).
- Retry-once-and-label-flaky scripts.
- Policy text in AGENTS.md ("don't weaken tests").
- Homegrown test-impact services (Anthropic patched its own three times).
- Quarterly hand audits.

**Why current products fail.**
- Flaky-test tools (Trunk, BuildPulse, Datadog) detect and quarantine flakes but don't decide which tests are worth keeping.
- Test selection (CloudBees/Launchable, Develocity, Datadog TIA) runs fewer tests per PR but never shrinks the suite.
- Testomat.io duplicate detection works on test-case text, not runtime coverage or mutation.
- None of them tracks who owns which fixture or watches for an agent bumping a timeout or adding a skip.

**Why now.** Agents passed the point of writing most tests during 2026. Suites grew 4-10x in 6-9 months at named companies.

**Potential product.** A "test suite steward":
- Continuously scores each test on mutation-kill or unique coverage, runtime and flake rate.
- Opens prune and merge PRs for redundant tests.
- Assigns owners to fixtures and seed data and flags shared-fixture mutation.
- Gates agent PRs that add skips, loosen assertions or bump timeouts, and asks for justification.
- Exposes a "known flaky / already failing on main" feed that agents read before they try fixes.

**Time to value.** 1-3 days. It reads CI history plus repo, and the first output is a ranked prune list with expected CI-minute savings.

**Pilot (14-30 days).** One repo with heavy agent output. Baseline suite runtime and flake rate. Ship 3-5 prune PRs and the tampering gate. Target: 20-40% suite runtime reduction with no drop in mutation score.

**Willingness to pay.** Moderate. It can be priced against CI spend saved, which is measurable, but buyers may see it as a feature of their CI vendor. Unproven.

**Expansion.** Fixture and test-data management, a flaky-test feed for agents, verification policy across repos, then into CI cost optimization.

**Competition.** Trunk (flaky tests and merge queue), BuildPulse, Datadog Test Optimization, CloudBees Smart Tests (Launchable), Gradle Develocity, Buildkite Test Engine, Testomat.io, mutation-testing OSS (Stryker, PIT). AI code-review vendors could add a "test tampering" check, and STATUS.md already killed AI code review as a category.

**Moat (10/100/1,000).**
- 10 customers: per-repo models of test value.
- 100: a cross-customer corpus of agent test anti-patterns (which agent and model produces which bloat).
- 1,000: benchmark data on "test value per CI dollar". The moat is weak until 100+ customers.

**CTO test.** "Our agents add 2,000 tests a week. CI is slower every month and I can't tell which tests actually catch anything."

**Kill test.** Will a platform lead pay a separate vendor for pruning when Trunk or Datadog could add a "redundant test" report in a quarter? Ask 10 teams with more than 50% agent-written code whether suite growth is a top-3 CI problem, and whether they have ever deleted tests at scale.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 6 | 8 | 7 | 7 | 6 | 5 | 6 | 5 | 6 | 6 | 6.3 |

---

## 2. CI capacity and cost explode under agent PR volume

**Problem.** Every agent PR and every push runs the full CI matrix. Agents push faster than CI responds. Queue times, runner bills and test-selection services all buckle.

**Recent evidence (10 signals)**
1. Anthropic: CI job volume up 25x in 6 months, test selection service patched 3 times. Advice: "assume your architecture will be at a 25x load within two quarters" (Sep 2026).
2. Linear: CI rework, PR wait 6 to 5 minutes, runner time per test halved despite a 4x suite (Sep 2026, HN 49792067).
3. HN comment on 48010604: GitHub Actions went from 500M minutes a week (2023) to 1B (2025) to 2.1B "this week", attributed to agentic coding. Someone quoted 14x load (2026).
4. HN "Show HN: Agent-CI" (47541521): Actions is "usually in the top-5 expenses", and agents "will easily double the bill".
5. HN 49198302 and others: repeated GitHub Actions degraded-availability threads in 2026.
6. HN 47932028: Copilot code review will start consuming Actions minutes.
7. stack-archive blog: P95 CI queue time hit 7h35m with agents on a single runner. Test selection cut it 92% (2026, secondary source).
8. Depot CEO: the GitHub PR model can't keep pace with agents. Depot launched "Depot CI" for agentic engineering (2026).
9. Tenki blog, "The Hidden CI Tax of AI Coding Agents" (Apr 2026), citing 3-5x more CI minutes per developer. This is a vendor source.
10. HN Ask "biggest bottleneck when developing with agents" (49263602): agentic coding increased pressure on CI.

**Who has the pain.** Every engineering org with heavy agent use. Platform/CI teams own the budget.

**What they do today.** Faster runners, sharding, batching, self-hosted ARC, homegrown test-impact analysis (Anthropic, Linear), local CI runners.

**Why current products fail.** They mostly don't. Vendors are shipping fast. The gap is agent-specific pacing: which pushes deserve CI at all, and batching agent iterations so CI doesn't run on every intermediate commit.

**Why now.** 25x volume in 6 months. GitHub added a self-hosted platform fee in March 2026.

**Potential product.** A "CI admission controller" for agents. It decides per push: skip, local-sandbox check, selected tests, or full matrix. It coalesces an agent's rapid commits.

**Time to value.** Days. **Pilot.** Cut CI minutes 30% on one repo in 14 days.

**Willingness to pay.** High. CI is a top-5 dev expense.

**Expansion.** Runners, caching, test selection.

**Competition.** Very crowded: Depot, Blacksmith, WarpBuild, Tenki, Namespace, RWX, Buildkite, CircleCI, CloudBees/Launchable, Datadog, Develocity, Trunk, GitHub itself.

**Moat.** Weak. A pacing policy is easy to copy.

**CTO test.** "Our CI bill doubled since agents and queues are hours long."

**Kill test.** What can you do that Depot or Blacksmith can't ship in a month? Probably nothing.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 8 | 8 | 6 | 6 | 7 | 7 | 3 | 4 | 8 | 7 | 6.5 |

---

## 3. One failure fans out across many agents (broken main, semantic conflicts, shared flake)

**Problem.** When main breaks, or a shared flaky test or broken fixture appears, every in-flight agent independently hits it. Each one investigates and patches the symptom, burning tokens and CI. Two green agent PRs can also merge into a red main, because checks ran against a stale base. Nothing broadcasts "main is red because of X, don't fix it" to the agent fleet.

**Recent evidence (9 signals)**
1. Meiklejohn (2026-06-10): every unrelated branch rediscovered the same broken assumption and kicked off the same loop (fail, agent investigates, patch, fail elsewhere).
2. sytone/botnexus issue #3694: semantic merge conflict broke main, green PRs merged against a stale base (date unverified).
3. vfarcic/dot-agent-deck issue #1088: two green PRs merge into a broken main, and a red main "notifies nobody" (date unverified).
4. StefanMaron/BusinessCentral.AL.Runner issue #2924: semantic conflicts break main (date unverified).
5. gastownhall/beads issue #7245: main broken by a merge gap between #7199 and #7210 (Gas Town is a multi-agent orchestrator) (date unverified).
6. ddteeter/agentic-guardrails-scaffolding issue #98 and misnaej/forge issue #524: nothing re-verifies the combination (date unverified).
7. arXiv 2609.25396, "Passes Alone, Fails Together": a benchmark of semantic coordination failures in parallel agent development (Sep 2026).
8. OpenAgentsInc/openagents issue #10145: the agent blocks on already-failing tests. The fix proposed was to tell the agent which failures pre-exist.
9. tadasant/zimmer PR #1163: a duplicate migration version failed "every job on main" (date unverified).

**Who has the pain.** Teams running more than 5 concurrent agents on one repo.

**What they do today.**
- Turn on merge queues or "require up to date".
- Retry, then rerun on the base commit, then label as "already failing on main" (homegrown, per the GitHub issues above).
- Hand-written prompt notes.

**Why current products fail.** Merge queues (GitHub, Trunk, Graphite, Mergify, Aviator) prevent part of the problem. None of them pushes failure context back into running agent sessions, or dedupes the investigation work agents are doing.

**Why now.** It only matters once there are many concurrent non-human writers.

**Potential product.** A "main health bus" for agents:
- Classifies CI failures as pre-existing, flaky or caused by this PR.
- Exposes the result via MCP or a hook so agents check it before trying a fix.
- Assigns one agent to fix a shared break and pauses the others.

**Time to value.** Days. **Pilot.** Measure duplicate-investigation tokens and CI runs before and after on one repo.

**Willingness to pay.** Low to moderate. Hard to quantify, and it reads as a feature.

**Expansion.** Into merge queue and CI.

**Competition.** Merge queues, Trunk flaky quarantine, agent orchestrators (Superset, Conductor), and the agent vendors themselves (Cursor, Devin, Codex could add "main is red" awareness).

**Moat.** Low.

**CTO test.** "When main goes red, twenty agents all try to fix it and I pay for every one."

**Kill test.** Does a merge queue plus a flaky label already remove 80% of this?

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 6 | 7 | 7 | 7 | 5 | 4 | 5 | 5 | 5 | 5 | 5.6 |

---

## 4. Per-agent runtime isolation on shared hosts

**Problem.** Parallel agents in worktrees on one machine, or in a shared dev or staging environment, collide in several ways:
- They fight over Postgres, ports and Docker Compose names.
- Env files get copied by hand between worktrees.
- They share a test database that fills up.
- They run migrations against a shared staging database.

Every team writes its own `worktree.sh`.

**Recent evidence (12 signals)**
1. Maji-Studio/noma-dmrv PR #917, "harden the agent environment from the October retro" (Oct 2026): parallel sessions kept colliding on the dev database, port 3100 and hand-copied env files. Built `scripts/worktree.sh` to own DBs and ports per worktree.
2. Munyon-Canyon/monaco issue #2609 (2026-10-04): shared test Postgres filled twice during agent runs.
3. alexsiri7/interstellarai.net issue #66 (Sep 2026): feature branches ran `prisma migrate dev` against the shared staging DB and left 6 tables and 2 enums behind (cleaned 2026-09-06).
4. jackvincentnz/lab issue #983: isolate local dev ports per worktree for parallel agent runs.
5. MrJuancho/webstack-agent-harness PR #3: isolate Postgres per git worktree.
6. Hendingar/hendingar.no PR #113: each worktree gets its own database and ports.
7. leomontigatti/en-escena PR #1332: per-worktree DB and port, and sweep finished ones.
8. openaustralia/planningalerts issue #2227 and PR #2240: parallel tests across worktrees, compose ports per worktree.
9. OSS tools that each exist to solve this: Docktree, tug, dockportless, markcipolla/worktrees, KudcraftsHQ/conductor, jdtzmn/port.
10. abi83/prepify issue #85: agents (Claude Code non-interactive) collide on a shared Neon dev branch. Agents now stop and flag instead of migrating.
11. HN Superset launch (46368739): setup scripts create a DB branch or container per workspace.
12. anthropics/claude-code issue #27063: an agent ran a destructive DB command and wiped a production DB (date unverified; a severity example).

Items 4-8 are dated unverified.

**Who has the pain.** Individual developers and small teams running 3-10 local agents, and platform teams providing devboxes.

**What they do today.** Homegrown shell scripts, Superset/Conductor setup scripts, Neon branches, Compose overrides.

**Why current products fail.** Cloud sandboxes (E2B, Daytona, Modal, Coder, Codespaces, Qovery, Signadot) solve this off-box, with cost and setup overhead. The local, per-worktree problem is solved by free OSS.

**Why now.** Running worktrees with parallel agents became mainstream in 2026.

**Potential product.** A "resource lease daemon" for agents: DB, port, queue and secret leases per agent with TTL cleanup, working locally and in CI.

**Time to value.** Hours. **Pilot.** 14 days.

**Willingness to pay.** Low for the local version. Higher as part of an enterprise devbox platform, which is a crowded market.

**Expansion.** Into cloud devboxes.

**Competition.** Heavy: Superset, Conductor, Coder, Daytona, E2B, Modal, Namespace, Ona (Gitpod), Neon, Signadot, Bunnyshell, Qovery, Tenki, Docker itself.

**Moat.** Low.

**CTO test.** "Our agents keep stepping on each other's databases."

**Kill test.** Would anyone pay over $20 per developer per month when a 100-line script works?

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 7 | 7 | 6 | 5 | 6 | 4 | 3 | 4 | 6 | 5 | 5.4 |

---

## 5. Collisions on sequenced repo artifacts

**Problem.** Parallel agent branches all allocate "the next" migration number, edit the same CHANGELOG section, bump VERSION or package.json, and regenerate lockfiles. The result:
- Duplicate migration versions, sometimes silently half-applied.
- Every open PR goes into conflict after each merge.
- Lockfiles break.

**Recent evidence (16 signals)**
- Migrations:
  - u2giants/shared-db issue #670: a near-miss on 2026-08-10, when two agents dispatched in one session both authored migration 20260810130000.
  - sentania-labs/hades issue #447: migration numbers collide across parallel workers.
  - VATUSA/OIS issue #569: two PRs claim the same version and sqlx applies both, leaving the database half-migrated.
  - Lumen-Scribe/Lumenqraph issue #361: duplicates 0017 x2 and 0022 x3.
  - ilv78/Art-World-Hub issue #820: parallel agent PRs touching shared/schema.ts collide.
  - tadasant/zimmer PR #1163: duplicate 20260912120000 failing every job on main (about Sep 2026).
  - carverauto/serviceradar PR #5270: duplicate 20261006170000. The version string is in the future relative to today, so treat this as uncertain.
  - reliant-labs/forge PR #338: timestamp versions so parallel branches can't collide.
  - bifanaboy/liszt issue #36 and zzzubair/clashlens PR #170.
- CHANGELOG, VERSION and lockfiles:
  - apiad/aegis issue #10: "CHANGELOG.md is the only file that conflicts, and it conflicts on every PR".
  - bill10/agent-007 PR #115: changelog.d fragments.
  - aaltaay/Nova issue #344: "commit process for a parallel agent swarm: derive versions, shard the ledgers, queue the merges".
  - open-astro/AlpacaBridge issue #759.
  - migu-developer/financial-management PR #72: lockfile broken by two parallel bumps.
  - eh-homelab/ScadBuddy issue #508: ranked merge-conflict hotspots.
- Meiklejohn (2026-07-27): "a migration sequence assumes somebody is assigning the order".

**Who has the pain.** Any repo with more than 3 concurrent agents and an ordered artifact.

**What they do today.** They rediscover known fixes repo by repo: timestamps, renumber at merge, changelog fragments, deriving versions, CI duplicate checks.

**Why current products fail.** Fixes are per-tool (Atlas non-linear detection, django-linear-migrations, changesets, release-please). Nothing scans a repo for "conflict surfaces" and installs the fixes.

**Why now.** It appears as soon as there are N concurrent writers. With humans it was rare enough to ignore.

**Potential product.** A "repo parallelism linter and fixer": finds the hotspot files that serialize agents and installs fragment, derive or allocate patterns plus merge-time renumbering.

**Time to value.** Hours. **Pilot.** 7-14 days.

**Willingness to pay.** Low. It is a one-time fix, and agents can apply the fixes themselves once told.

**Expansion.** Weak.

**Competition.** Atlas/Bytebase for migrations, merge queues, release tooling, and the coding agents themselves.

**Moat.** Very low.

**CTO test.** "Two agents shipped the same migration number and half-migrated staging."

**Kill test.** After the first fix, is there any recurring value? Almost certainly not.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 6 | 7 | 8 | 8 | 5 | 3 | 4 | 3 | 4 | 4 | 5.3 |

---

## 6. Agent config and context drift across repos

**Problem.**
- AGENTS.md, CLAUDE.md and skills diverge between tools and between repos.
- Claude Code does not read AGENTS.md natively, so a CLAUDE.md subset masks the gap.
- Instructions go stale as code changes.
- Orgs with hundreds of repos can't push shared guidance.

**Recent evidence (10 signals)**
- mento-protocol/monitoring-monorepo PR #2562: a "quarterly CLAUDE.md/AGENTS.md drift audit (2026-10)".
- eweser/eweser-db PR #99: Claude was reading "a drifted subset".
- lifeodyssey/animichi PR #1803: repair stale AGENTS.md claims.
- levygit837-cyber/web-agent-research issue #105.
- yurukusa gist on keeping the two files in sync, referencing the #6235 cluster with "5,200+ reactions" (count from the snippet, unverified).
- devantler-tech/monorepo issue #3195: a stale agent definition was being served.
- Sync tools that exist to solve this: trick77/agents-md-sync (central template to many repos), dallay/agentsync, kishandyadav/agent-skills-sync-tool, the Agent Sync Action on GitHub Marketplace, vincentkoc/dotskills issue #1, executor issue #1442 (skill gateway).

**Who has the pain.** Dev-productivity teams at multi-repo orgs.

**What they do today.** Symlinks, pre-commit mirrors, central template repos, quarterly audits.

**Why current products fail.** Free OSS covers syncing. Nothing verifies that instructions are still true against the code.

**Why now.** Multi-agent tool sprawl in 2026.

**Potential product.** "Agent context CI": validates AGENTS.md claims against the repo, syncs across tools and repos, and tracks which instructions agents actually obey.

**Willingness to pay.** Low.

**Competition.** Anthropic, GitHub and Cursor enterprise-managed settings. Sourcegraph, Augment and Unblocked on the context side.

**Moat.** Low.

**CTO test.** "Every repo has a different CLAUDE.md and half of it is wrong."

**Kill test.** Will Anthropic or GitHub ship org-level managed instructions (partially exists) and make this moot?

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 4 | 4 | 6 | 8 | 8 | 6 | 3 | 4 | 3 | 5 | 4 | 5.0 |

---

## 7. GitHub and registry rate limits from agent fleets

**Problem.** Many agents sharing one token or app burn through GitHub REST limits (5,000 requests an hour) or trip secondary limits, causing hour-long 403s. Agents also use the Contents API as a remote filesystem.

**Evidence (5 signals)**
- github/github-mcp-server issue #2385: improve rate-limit errors for agents.
- cornerstonemarketingus/atlas issue #198: agents use the Contents API as a filesystem across concurrent agents. Fix: clone once and cache by SHA.
- the-hcma/repository-helpers issue #608: a throttled `gh api` wrapper plus an agent rule to use it.
- uberblick-ai/ub-agents issue #80 and PR #82: multiple launchers on one account exhaust the quota.
- An unnamed source in results described the secondary limiter 403ing every call "for the better part of an hour" after a burst of reply/resolve calls.
- No fresh evidence for npm registry 429s caused by agents. The npm results were older and generic.

**Who, today, why they fail.** Small agent-platform builders. Fixes are a throttled wrapper, a GitHub App instead of a PAT, or a caching proxy. These work.

**Product.** A GitHub API caching and throttling proxy for agent fleets.

**Competition.** GitHub may raise limits for agents. Generic API gateways.

**Moat.** None.

**Kill test.** Does moving to a GitHub App plus a local clone fix 95% of it? Likely yes.

| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market | VC | Avg |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 5 | 5 | 6 | 7 | 7 | 4 | 3 | 5 | 3 | 3 | 3 | 4.6 |

---

## Signals that didn't make it

- **Sandboxes and devboxes for hundreds of agents.** The pain is real: Ramp Inspect uses Modal snapshots at most 30 minutes stale, and Stripe Minions keep warm devbox pools that start in 10 seconds. But it is the most crowded category in this slice: E2B, Daytona, Modal, Vercel Sandbox, Cloudflare, Coder, Ona, Qovery, Bunnyshell, Tenki, Namespace, kubernetes-sigs/agent-sandbox.
- **Secrets inside agent sandboxes.** Examples: kubernetes-sigs/agent-sandbox issue #1045 (credential vault proxy), sandbase-harness issue #323, PraisonAI advisory GHSA-2xv2-w8cq-5gxw. This falls under the excluded "generic agent security" category.
- **Agent-to-human or agent-to-agent session handoff.** Many free skills exist (agent-session-resume, agenthandoff, softaworks session-handoff, n0an/handoff-skill). Low WTP, and agent vendors will ship it natively.
- **File-level coordination and locks between parallel agents.** Examples: manaflow-ai/cmux issue #3323 (file-lock broker), casehubio/claudony issue #216, and arXiv "Claim Plane" papers 2607.21909 and 2608.00947. It is mostly research and orchestrator features, and close to the killed "generic orchestration".
- **Human attention and review as the real bottleneck** (HN Ask threads 46682551, 47573483, 49263602): developers can't usefully supervise more than about 3 sessions. This is review, which was already killed.
- **Agent-written code makes CI the bottleneck, with "verification debt"** (Depot, WarpBuild, CircleCI 59% throughput stat via tianpan.co). Folded into #2.
- **Database branching for agents.** Neon reports that agents create 20x more branches and do 50x more rollbacks than humans (snippet; source page not confirmed). Neon, Supabase branching and Xata already own this.
- **Codex and Claude cloud setup-script maintenance per repo.** Many repos are adding setup scripts. It is a chore with no sign anyone would pay to solve it.
- **Spend from parallel agents** (three agents burning a $200 plan in 30 minutes, HN 47559293). This is the killed AI-spend-caps category.

## Researcher's verdict

- No candidate clears the bar.
- The slice's robust, recent and quantified pain is verification throughput (CI plus tests), and the vendor field there is dense.
- The only partly open sub-wedge is **test-suite quality and ownership when agents are the authors** (#1). Its open questions:
  - Do buyers see "the suite is bloated and lying" as a budget line?
  - Will Trunk, Datadog or Launchable absorb it within 6 months?
- If the founders pursue it, the fastest kill test is 10 calls to platform leads at companies publicly reporting more than 50% agent-written code (Anthropic, Linear, Ramp, Stripe-class).
- Ask each of them: "In the last quarter, did you delete tests at scale or block an agent from weakening a test? Would you pay to automate that?"
