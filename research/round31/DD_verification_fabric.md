# Deep dive: T2-1 Verification fabric (CI rebuilt for agent-volume change streams)
Date: 2026-10-06. Starting score 6.9. 14 web searches. Sources are cited inline. Market-size figures not sourced here are estimates.

## New evidence collected this round
- **Blacksmith**: $45M Series B at $550M (Peak XV, Aug 12 2026). Grew from ~800 to 6,000+ customers in 11 months. Most of the money goes to compute (it plans 10x cores). It also launched "codesmith", a cloud coding agent, so it is moving up the stack toward the agent loop ([pulse2](https://pulse2.com/blacksmith-raises-45-million-series-b-at-550-million-valuation/), [unite.ai](https://unite.ai/blacksmith-raises-funding-for-ai-code-validation-layer/)).
- **Depot CI**: a new CI engine launched Mar 24 2026, pitched as "CI was designed for humans; agents need it rebuilt". It includes local patch execution. This is the exact thesis framing ([depot.dev](https://depot.dev/blog/ci-for-agentic-engineering), [tenki](https://www.tenki.cloud/blog/depot-ci-vs-tenki-agentic-runners)).
- **CloudBees Smart Tests** (formerly Launchable): GA Apr 2 2026, positioned as "control for the surge of AI-generated code flooding CI pipelines". It does predictive and semantic test selection and claims a 35-70% runtime cut ([cloudbees](https://www.cloudbees.com/newsroom/cloudbees-smart-tests-brings-control-to-ai-generated-code)).
- **Nx Cloud**: Self-Healing CI is in production. Nx says developers save more time from it "than caching + DTE combined". Its 2026 roadmap is "infrastructure for autonomous agents" ([nx.dev](https://nx.dev/blog/nx-2026-roadmap), [nx self-healing](https://nx.dev/ci/features/self-healing-ci)).
- **Trunk**: merge queue plus flaky-test detection plus an "AI DevOps agent". Its roadmap includes an agent that fixes flakes when they are detected and a merge queue that is aware of impacted targets ([trunk roadmap](https://trunk.io/roadmap), [docs](https://docs.trunk.io/ai-devops-agent/overview)).
- **Buildkite**: MCP server, Preflight (experimental), Test Engine with flaky quarantine routed to agents, "govern 100,000+ concurrent CI agents" ([buildkite](https://buildkite.com/platform/agentic-workflows/)).
- **Namespace**: Series A in Mar 2026 (reported as $15M or $23M, NEA) ([signalbase](https://www.trysignalbase.com/news/funding/namespace-secures-23m-series-a)).
- **Graphite/Cursor**: acquisition announced Dec 2025. It brings a stack-aware merge queue with speculative execution and batch bisection, to be integrated with Cursor background agents ([graphite](https://graphite.com/blog/graphite-joins-cursor)).
- **GitHub**: hosted runner prices cut by up to 39% from Jan 2026. The $0.002/min self-hosted fee was withdrawn within 48 hours. GitHub promises 12 months of investment in the self-hosted experience. It added a setting that lets Copilot agent workflows run without human approval (Mar 2026). From Jun 1 2026, Copilot code review consumes Actions minutes ([github resources](https://resources.github.com/actions/2026-pricing-changes-for-github-actions/), [changelog](https://github.blog/changelog/2026-03-13-optionally-skip-approval-for-copilot-coding-agent-actions-workflows/), [changelog](https://github.blog/changelog/2026-04-27-github-copilot-code-review-will-start-consuming-github-actions-minutes-on-june-1-2026/)).
- **Pain signal**: "The coding agent CI bill that doubled without a postmortem" (Jun 2026). The same source reports Actions bills up to +280% for Copilot-adopting teams (a secondary claim) ([tianpan](https://tianpan.co/blog/2026-06-02-the-coding-agent-ci-bill-that-doubled-without-a-postmortem)). Also "The merge queue is the new bottleneck" (Jul 2026) ([tianpan](https://tianpan.co/blog/2026-07-02-the-merge-queue-is-the-new-bottleneck)).
- **Harness**: its 2026 news is AI Evals and an "Agent DLC" (Jul 2026). Its existing Test Intelligence (test selection) is now a commodity feature inside the Harness suite ([devopsdigest](https://www.devopsdigest.com/node/14575)).
- **EngFlow/BuildBuddy**: no fresh funding found. EngFlow's last round was an $18M Series A about 3 years ago. BuildBuddy markets remote execution to coding agents ([cbinsights](https://www.cbinsights.com/compare/buildbuddy-vs-engflow)).

---

## 1. Technical architect
**What has to be true.** The fabric only wins if it does something that faster runners cannot: **avoid work**. It has three levers:
1. **Change-to-test mapping.** It needs a reliable map from each change to the tests that change affects. There are three ways to get one:
   - (a) A build graph (Bazel, Nx, Pants, Turborepo). This is precise but only exists in about 10-20% of repos.
   - (b) Per-test coverage maps. These are precise but expensive to keep fresh, and they break on dynamic languages, config changes, and reflection.
   - (c) ML or LLM prediction (the Launchable approach). This works everywhere but gives probabilistic recall, around 90-95% of failures caught at 30-50% of the tests.
   For agent PRs, (c) is acceptable if a full run still happens at merge-queue time. That two-tier design (fast probabilistic tier, then a full gate at merge) is the real architecture.
2. **Deduplication of agent branches.** Agents running N parallel attempts at one task produce near-identical diffs. You can hash the affected-target set together with the content hashes of inputs, then reuse results across branches. This is exactly what Bazel/REAPI action caching already does at the action level. Outside Bazel you have to build a content-addressed test-result cache keyed on (test id, transitive input hash). That is hard for arbitrary repos because the inputs are undeclared. Hermeticity is the hidden cost.
3. **Moving verification into the agent loop.** Today an agent writes code, pushes, waits about 10 minutes, and reads the logs. The better loop is that the agent calls `verify(patch)` mid-task over MCP or an API, gets the affected tests run on a warm snapshot in under 60 seconds, and only opens a PR once the patch is green. Depot (local patch execution), Buildkite (Preflight), and Nx (agent fixes) are all converging here.

**Hard parts:** warm per-repo snapshots (memory/disk-snapshot VMs such as Firecracker, which Namespace and Blacksmith already run); undeclared dependencies; flaky tests that poison dedupe; and secrets and egress for agent-triggered runs.

**Architect's verdict:** it is buildable in about 6-9 months by a strong team. The defensible core is the test-impact and result-reuse brain, not compute. But every serious component already exists somewhere: CloudBees (selection), Nx (graph and self-heal), Bazel/EngFlow (content-addressed reuse), Depot/Namespace (snapshots), Trunk/Graphite (queue). The novelty is integration, not invention.

## 2. Skeptical CTO buyer (Series C, 300 engineers, ~35% agent PRs)
- "My CI bill went from $40K to $110K a month. That hurts, but it is under 5% of the agent token bill and engineer cost. My first move is to switch runs-on to Blacksmith (half price, one-line change) and turn on `paths:` filters. That gets me 50%+ savings in a day."
- "Test selection: we tried Launchable in 2023. The team distrusted skipped tests after one escaped regression and turned it off. Why would agent PRs change that? Actually, agent PRs make it worse: I trust their code less, so I want **more** testing, not less."
- "Dedupe across agent attempts is nice, but my agents run in Cursor or Codex cloud sandboxes. Their tests run *there*, not in my CI. The vendor of the agent sandbox owns the inner loop."
- "Integration in hours? Only the runner part. Selection plus a hermetic cache means weeks of work from my platform team, which is the team I'm short on."
- "What I'd pay for: a guarantee that main stays green while 300 agent PRs a day merge, plus a CI bill flat against volume. Sell me a **cost-per-merged-change SLA**, not a scheduler."

**Buyer verdict:** real pain, but the CTO's first dollar goes to cheaper runners, and the second goes to whatever the merge queue and agent vendor bundle. A CTO would maybe take a free shadow pilot and would be reluctant to sign a standalone contract.

## 3. Top-tier VC partner
- **Market:** CI/CD tooling is about $3-5B plus a large compute pass-through (estimate). It is growing with agent volume, and that growth is real (2.1B Actions minutes a week, 17M agent PRs a month). Blacksmith grew 7.5x in customers in 11 months, which proves demand.
- **But the money already moved** (lesson G). In 2026: Blacksmith $45M at $550M, Namespace Series A, the Depot CI launch, Cursor buying Graphite, CloudBees Smart Tests GA. A seed company in October 2026 would be the 6th or 7th entrant into a category that newsletters already named ("CI for agentic engineering").
- **Business model tension:** runner companies earn on minutes, so a vendor that reduces minutes cannibalizes its own revenue. That is the only structural opening: an **incentive-aligned** seller priced per verified change. But GitHub just cut prices 39%, and runner vendors will happily bundle selection as a retention feature, because margin on compute makes the feature free for them.
- **Exit and outcome:** a plausible path is a $50-150M acquisition by GitHub, Cursor, or Datadog. A $10B outcome needs to own the "verification oracle" every agent calls, but the agent vendors (Cursor, OpenAI Codex, GitHub Copilot, Anthropic) each want to own that in-house, and they control the sandbox.
- **Partner verdict:** pass at seed unless the founders bring a proprietary wedge, such as ex-Bazel/Google TAP engineers with a hermetic-cache breakthrough for non-Bazel repos.

## 4. Competitor analyst
| Player | What they have now | Distance to "verification fabric" |
|---|---|---|
| Blacksmith | Bare-metal runners, 6K customers, $550M, codesmith agent, caching | Selection/dedupe is 1-2 quarters away; it has the distribution and data |
| Depot | Depot CI engine (Mar 2026), agent framing, local patch execution, cache | Closest match to the thesis narrative already |
| Namespace | Snapshot-based ephemeral compute, Series A 2026 | Has warm snapshots; lacks the brain |
| BuildBuddy / EngFlow | REAPI remote execution and content-addressed reuse | Has the *true* dedupe, but only for Bazel shops; underfunded |
| CloudBees Smart Tests (Launchable) | Predictive and GenAI test selection, GA Apr 2026, explicitly targets AI code | Owns the selection brain; weak on compute and DX |
| Trunk | Merge queue, flaky detection, AI DevOps agent | Owns the merge gate plus flake data |
| Harness | Test Intelligence (selection) inside its suite; AI Evals | Feature in an enterprise bundle |
| GitHub Actions | Default; prices cut; agent approval skip; self-hosted investment; capacity-constrained | Could add affected-test hints via Copilot; slow, but it owns the default |
| Nx Cloud | Project graph, DTE, remote cache, self-healing CI, agent roadmap | Already sells "affected + cache + agent fix" to JS/TS monorepos |
| Graphite / Cursor | Stack-aware merge queue, speculative batching, linked to background agents | Can close the loop agent → verify → merge inside Cursor |
| Buildkite | MCP server, Preflight, Test Engine, agent-scale orchestration | Enterprise-grade substitute |

**Analyst conclusion:** every layer of the thesis (compute, selection, dedupe, queue, self-heal, agent API) has at least one funded owner, and three players (Depot, Nx, Blacksmith) are each about one quarter from the full bundle. No white space was found in "CI for agents" as such.

## 5. Self red-team
- *Am I over-killing because of lesson G?* Possibly. Markets this size support 3-5 winners, and Blacksmith's growth suggests the pie is expanding fast. But an entrant must still win on something structural, and "smarter scheduling" is not structural.
- *The incentive-misalignment argument* (minute sellers will not cut minutes) is the strongest argument for a new entrant. Counter: Blacksmith and Depot compete on price already and will use selection to win logos. CloudBees sells selection without selling compute, and it has not exploded.
- *The real unclaimed piece may not be CI at all.* It may be the **pre-PR verification API called by any agent vendor**, neutral across Cursor, Codex, Copilot, and Claude Code, running the customer's real test environment. But the T3 kill (autonomous merge was shipped natively) and the "in-loop verification judge" kill (5.5, feature-sized) both point the same way: agent vendors absorb the loop.
- *Evidence quality:* the +280% bill figure and the 17M agent PRs are from secondary blogs. GitHub's own figures are stronger.

---

## Final sharpened thesis
**"CI/CD (a ~$3-5B tooling market plus compute, estimated) works as *run the whole pipeline per push, billed per minute*, because changes arrived at human speed and humans would wait. AI makes that false: agent changes are 10-30x more numerous, mostly speculative, and near-duplicate. So verification should be rebuilt as a neutral, per-verified-change service: agents call `verify(patch)` mid-task; it runs only the affected tests on a warm snapshot, reuses results across sibling attempts through a content-addressed cache, and returns a signed verdict that the merge queue trusts. The price is per verified change, so the vendor's incentive is to *avoid* compute."**

- **Product (CTO-simple):** "Your agents check their own patches against your real tests in 60 seconds, before a PR exists. You pay per verified change, and your CI bill stops tracking agent volume."
- **Buyer:** Head of Developer Productivity / Platform. **Wedge:** Bazel/Nx/Pants monorepos with ≥30% agent PRs (a graph already exists, so dedupe is exact).
- **14-day test (only if pursued):** 5 platform leads at companies with ≥30% agent PRs. Pass condition: 3 say they would pay per-change pricing **in addition to** their runner vendor, and 1 agrees to a shadow run showing ≥50% compute avoided with zero escaped failures at the merge gate.

**Revised scores:** Market 7, Transformation 8, Urgency 7, Why-now 9, Buyer reach 6, Pilot speed 7, Integration 5 (selection and hermetic caching take weeks), Competitive opening 2, Structural diff 4, Expansion 6, Moat 4, VC 4 → **avg 5.75** (down from 6.9).

**Verdict: KILL.** The problem is real and well documented, but it has been funded on every layer in 2026: Blacksmith, Depot CI, Namespace, CloudBees Smart Tests, Nx self-healing, Trunk, Graphite/Cursor, and Buildkite. An incumbent can add the brain cheaply because it is a feature on top of compute margin. The only residual angle, a neutral per-change verification oracle, duplicates the killed "in-loop verification judge" and T3. Add to STATUS: "agent-volume CI: funded on every layer within 6 months of GitHub's public strain (lesson G again)."
