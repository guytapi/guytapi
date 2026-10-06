# Round 28 · H3 (Technical Infrastructure Architect): incidents in code no human understands

**Date:** 2026-10-06 | **Role:** technical infrastructure architect | **Searches:** 21 of 30. The session-wide search cap was hit after 21, so the Datadog and Harness positions below are **[U-prior]**: they come from pre-cutoff knowledge and were not re-verified this round.
Legend: [S] = source found this round. [U] = unverified or estimate. [I] = my inference.

**Verdict up front: B-weak (6.5 avg), not A.** The thesis is a **reversibility ledger**: a change-context primitive that tells humans and agents, during an incident, *which of the last N changes are live in the failing path, and which of them can be safely undone right now*. That includes changes that already wrote data. Each piece of this exists somewhere, but nobody sells the join. This is the only layer of H3 I could not find a direct owner for, and also the one most exposed to being absorbed as a Datadog/Harness/LaunchDarkly feature.

---

## 1. Pushing H3 to 2028-29 (method steps 1-3)

**Starting point.** Agent-authored changes are the majority, and change rate is 10-100x the 2024 level. Each production service has dozens of live changes in flight at once: code, flags, config, prompts/models, schema migrations, infra applies. They were made by different agents, from different intents, across repos, and deployed independently.

**First-order effects (already served, so not the answer):**
- "Which deploy caused this?" Served by AI SRE and change-intelligence tools: Rootly, NeuBird, Lightrun, Komodor, Causely, Resolve, Traversal. Killed as generic observability and AI SRE.
- "Who wrote this and why?" Served by intent→commit provenance: Entire Checkpoints, the Cursor Agent Trace spec (backed by Cognition, Cloudflare, Vercel, Google Jules, Amp), git-ai.
- "Ship every agent change behind a flag with auto-rollback." Served by LaunchDarkly CodeControl/Guarded Releases, the Unleash MCP `evaluate_change`/`wrap_change` tools, and FeatBit Skills.
- "How does this function behave in prod?" Served by Hud ($21M, Square Peg) and Lightrun.
- "Behavioral diff of a PR against real traffic." Served by Tusk Drift (YC), Speedscale, Keploy, Meticulous.
- "System map." Killed in round 12 (Apiiro, DeepWiki, etc.).

**Second-order effects (what breaks once all of the above exist):**
1. **The deploy is no longer the unit of attribution.** With 40-200 changes shipped per service per day, "the deploy at 14:02" holds 30 changes, half of them flag-gated with partial exposure. Correlating deploy timestamps with metrics gives a candidate list too long to act on.
2. **The flag is no longer the unit of rollback.** Every-change-is-a-flag (the LaunchDarkly and Unleash pattern) produces thousands of concurrent flags. Incidents come from *interactions* between changes (A+B breaks; A and B alone are fine). Flipping one flag off can be unsafe if a later change depends on it.
3. **Rollback stops being safe by default.** Rolling back code does not roll back data [S, pandastack, Red Gate]. A bad agent change that wrote rows in a new shape, emitted events to consumers, or ran a backfill cannot be undone with a flag flip. At agent speed, *forward-fix by another agent on top of corrupted state* becomes the default, and that compounds the damage.

**Third-order effects (the new category):**
- In an incident, the scarce resource is no longer diagnosis. AI SREs produce hypotheses in minutes (Elastic says 72 seconds [S]).
- The scarce resource is **a safe decision to undo**: "which of these 37 live changes do I revert, in what order, and what happens to the data they already wrote?"
- No human understands the code well enough to judge that, and an agent should not be trusted to guess it.
- So the system needs **machine-readable reversibility**: every change carries (a) where it is live at runtime, (b) what it has written or emitted, (c) what depends on it, and (d) a computed undo plan.

**The missing primitive (OpenTelemetry analogy).**
- OTel arrived because *requests* crossed service boundaries and needed propagated context (trace ID).
- At agent scale, *changes* cross boundaries. One intent fans out into commits in N repos, a migration, a flag, a prompt version and a Terraform apply, all deployed at different times.
- The missing primitive is **change context propagation**: a `change_set` ID that rides on (1) build artifacts, (2) every request span (which change-units were active on this request path), and (3) **every persisted write and emitted event**. A ledger turns those into "blast radius in requests, blast radius in data, dependency order, undo plan".
- Today OTel defines `vcs.change.id` (a PR ID, as a repo attribute) and feature-flag evaluation events [S, opentelemetry.io], but has **no convention for stamping change identity on data writes, and no notion of reversibility**.

---

## 2. Thesis (finalist format)

### Name: **Undo Graph**, a reversibility ledger for agent-speed production

**One-line problem.**
- When production changes 100x a day and nobody wrote the code, incident responders (human or agent) cannot tell which live changes are in the failing path, or which can be safely undone given the data those changes already wrote.
- The result: hesitant rollbacks, compounding forward-fixes, and long data-repair tails.

**Why this problem exists now.**
- Instability rises with AI adoption, and it is measured:
  - DORA 2025: "AI adoption … is currently associated with increasing instability" [S].
  - Cortex 2026 benchmark: incidents per PR +23.5%, with longer resolution times [S].
  - Faros 2026: incidents per PR 3x, production incidents tripled (round 12) [S].
  - New Relic 2026 AI Code Report: 78% report more incidents and 82% hit a production failure tied to AI code in 6 months [S, via snippet].
  - One organization reported MTTR +23% [S, snippet].
- The every-change-behind-a-flag pattern became vendor doctrine in 2026 (LaunchDarkly: "Every AI-generated change that touches production should run behind a feature flag") [S]. This multiplies concurrent change-units, and that multiplication is the precondition for the problem.
- Intent provenance became standard on the left side (Agent Trace RFC, Entire Checkpoints, July 2026 preview) [S]. The right side (runtime and data) has no equivalent.
- Data-destroying agent incidents are now public and frequent: Replit/Lemkin, the Terraform wipe of a production DB, the 48K files deleted [S, incidentdatabase/OECD]. Buyers are primed to ask "can we undo it?".

**Exact buyer.**
- Head of Platform / Head of SRE / VP Infrastructure. They own the deploy pipeline, the flag system and incident tooling.
- Secondary budget: VP Eng, under "change failure rate / MTTR" OKRs.

**Exact ICP.**
- B2B SaaS and fintech/insurtech with 100-1,000 engineers.
- More than 40% agent-authored PRs, more than 20 prod deploys per day, Postgres/MySQL as primary OLTP, and OTel already deployed.
- An existing flag system (LaunchDarkly, Unleash, Statsig or in-house).
- At least one data-corruption incident in the last 12 months that took days of manual repair.
- Initial list: AI-forward Series C+ companies publicly reporting agent PR share (round 8 corpus), and Vercel/Neon customers deploying via agents (round 15) [I].

**Current workaround.**
- Incident channel archaeology: deploy timeline in Datadog [U-prior], git log, Slack "who merged this?", then a flag flip or revert by guess.
- Data repair: point-in-time restore plus diff, hand-written SQL, and audit tables where they exist (Bemi-style CDC context [S]), sometimes customer support cleanup for weeks.
- Meta-scale companies build pre-merge risk scoring (Meta DRS/RADAR: 1/50 production-incident rate on reviewed diffs [S]). That is *prevention*, not *undo*. Nobody outside hyperscalers has a reversibility model.

**Why incumbents cannot easily own it.**
- **Datadog** [U-prior] has deploy and change tracking and (via Eppo) flags. But it sees telemetry, not writes. It would have to sit in the database write path and own the cross-repo change graph, and its incentive is ingestion volume, not a decision primitive. **Biggest threat.**
- **LaunchDarkly / Unleash / Harness** own flags, and Harness also owns CD, verification and Database DevOps [U-prior]. Each sees only its own change-units: flags, or its own pipeline. Customers run mixed estates: flags in LD, deploys in Argo/GHA, migrations in Atlas/Flyway, prompts elsewhere. Reversibility needs the union.
- **Entire / Agent Trace** stop at the commit. They have no runtime or data presence.
- **AI SREs** (Resolve, Traversal, Rootly, NeuBird) consume context but have to *infer* it from telemetry after the fact. They would be *customers* of a deterministic ledger rather than builders of one. They want to stay read-only, not sit in the write path.
- **Backup/undo vendors** (Rubrik etc., round-1 thesis C) restore whole states. They have no change-level granularity and no knowledge of code intent.
- **Bemi** ($4M, YC) [S] is closest on the data side: CDC plus application context. It is an audit-trail tool, not a change/rollback decision system, but it is one product decision away. **Second-biggest threat.**

**30-day MVP.**
1. **Change-set stamping.**
   - A CI step assigns `change_set_id` = hash(commit SHAs, flag variants, migration version, prompt version) per deploy unit and records its parent intent (Agent Trace / Entire trailer if present).
   - An OTel processor adds the active change-units to spans, using existing flag evaluation events plus the build SHA.
2. **Write stamping without schema changes.**
   - A Postgres extension or ORM hook emits `pg_logical_emit_message(change_set_id, txid)` into WAL alongside each transaction.
   - A CDC consumer (Debezium/wal2json) joins row changes with the change-set.
   - Result: "rows written/updated by change X". Overhead target <3% [I].
3. **Ledger + query API/MCP.** `live_changes(service, window)`, `blast_radius(change)` (requests, rows, events emitted), `dependents(change)`, `reversibility(change)` → {flag-flip safe | redeploy safe | needs data repair | irreversible external side effect}.
4. **Undo plan generator.**
   - Topological order of reverts.
   - For data: before-images from CDC give a candidate repair (inverse UPDATEs scoped to rows the change touched and nobody touched since). Conflicts are flagged for humans.
   - Plans are *proposed*, never auto-executed in v1.
5. **Slack/incident.io bot** answering "what can I safely undo?" with evidence.

**Pilot design (30 days, 2-3 design partners).**
- **Week 1:** install the CI step, OTel processor and CDC consumer on 1 Postgres cluster and 3-5 services. Validate stamping coverage of at least 95% of writes.
- **Weeks 2-4:** shadow mode on live incidents, plus **replay of the last 3 data-affecting incidents** reconstructed from WAL archives and deploy logs where retained.
- **Metrics:**
  - (a) time from alert to "candidate changes ranked", vs the incident record;
  - (b) number of incidents where the ledger's top-3 contained the culprit change;
  - (c) for data incidents, the percentage of affected rows correctly identified vs the team's manual repair;
  - (d) the number of rollbacks the ledger would have flagged as *unsafe* (data written or downstream dependents).
- **Pass:**
  - culprit in top-3 in at least 70% of incidents;
  - at least 90% row recall on a replayed data incident;
  - at least 1 "we would have made it worse" catch;
  - a paid conversion commitment from the platform lead.

**Pricing hypothesis.**
- Platform fee plus volume: $30K-$80K/yr mid-market (by stamped services and write volume), $150K-$400K enterprise [U].
- Anchors: LaunchDarkly enterprise and Harness CD contracts are in the same range [U]. One data-corruption incident costs 2-6 engineer-weeks plus customer credits [I].

**Expansion path.**
1. Undo for Postgres + one flag system →
2. All change-unit types (prompts/models, config, Terraform, Kafka schemas/events) →
3. **Pre-merge reversibility gates** ("this agent change is irreversible: requires a human or a staged write path"). Policy engines and coding agents call this. →
4. **Agent-executable undo**: AI SREs and remediation agents call the ledger as their safe-action API →
5. **Change-context standard** (an OTel semconv proposal for `change_set` on writes and events), with the ledger as reference implementation →
6. System of record for production change accountability: audit/SOX change management, insurance for agent-caused losses, vendor-dispute evidence.

**Moat.**
- **Position in the write path** (WAL/CDC plus SDK) is sticky once on.
- **Cross-vendor neutrality** across flag, CD, migration and prompt systems: Datadog and LaunchDarkly are each one side.
- **Labeled corpus of reversal outcomes** (which undo plans worked, interaction failures between change pairs). This becomes a learned "safe-to-undo" model that improves across customers.
- If the semconv lands, **standard ownership** à la Honeycomb/Lightstep in OTel's early days. That is brand, not a lock.
- **Honest:** at 10 customers the moat is just engineering, and a strong platform team could build a 60% version (CI hash plus span attribute plus Debezium join) in about a quarter.

**Why it could become a $10B+ company (outcome-B argument).**
- If agent-authored change becomes 90%+ of production change, the binding constraint on how much autonomy companies grant agents in prod is **"can we undo it?"**, not "can we diagnose it?".
- The layer that answers that deterministically becomes the safety substrate that every remediation agent, coding agent and approval policy depends on, the way OTel/tracing became mandatory for microservices. Three things follow:
  1. It is a **tax on every production change**, priced by change volume, which is growing 10-100x.
  2. It is the **only source of truth for agent-caused-loss attribution**: insurers, auditors and vendor disputes.
  3. It gives the right to own **automated remediation execution**, which is the money AI SRE vendors chase but cannot do safely without it.
- Comparable outcomes: Datadog's APM and tracing franchise, and LaunchDarkly (about $3B at peak [U]) for one change-unit type only.
- This is plausible only if the standard and cross-vendor neutrality are won before Datadog bundles it.

**Direct competitors and adjacent threats.**

| Player | Overlap | Gap left |
|---|---|---|
| LaunchDarkly CodeControl / Guarded Releases [S] | Per-change flags, metric-guarded auto-rollback | Single change-unit type; no data-write blast radius; no cross-change dependency or undo ordering |
| Unleash MCP, FeatBit Skills [S] | Agents auto-wrap risky changes in flags | Same as above; adds flag sprawl |
| Datadog Change Tracking + Eppo/flags [U-prior] | Change timeline on service pages, flag data | Telemetry-side only; no write stamping; no reversibility semantics. **Most likely absorber** |
| Harness CD + CV + Feature Flags (Split) + DB DevOps [U-prior] | Pipeline-scoped verification and rollback, DB change tagging (Harness DB DevOps "tag" for targeted rollbacks [S]) | Only for changes deployed through Harness; schema-level, not row-level |
| Entire Checkpoints, Agent Trace, git-ai [S] | Intent → commit provenance | No runtime/data; natural **upstream input** |
| Hud ($21M) [S], Lightrun [S] | Function-level runtime behavior for agents | Behavior, not change identity or reversibility |
| Rootly, NeuBird, Komodor, Causely, Resolve, Traversal, Elastic [S] | "Which change caused this?" by inference | Probabilistic correlation; read-only; would consume the ledger |
| Bemi ($4M, YC) [S], DBOS provenance/time travel [S] | Row-level change capture with app context / time travel | No change-set or undo-plan layer; Bemi is the fastest possible entrant |
| Tusk Drift, Speedscale, Keploy [S] | Pre-merge behavioral diffs | Prevention, not undo |
| Meta DRS/RADAR [S] | Pre-merge risk | Internal-only; prevention |
| Rubrik / backup "agent undo" (round 1) | Whole-state restore | No change granularity |

**One sentence to send a CTO.**
"When your agents ship 100 changes a day and something breaks, we tell your on-call (or your SRE agent) in one query which live changes are in the failing path, exactly which rows each one wrote, and which can be undone safely right now, with the repair script."

**Hard kill criteria.**
1. In replay of a design partner's last 10 incidents, fewer than 3 involved a change whose rollback safety was unclear or data-affecting. That would mean deploy-level revert is good enough.
2. Write-stamping overhead above 5% p99 latency on OLTP, or stamping coverage below 90% after 2 weeks (ORMs, raw SQL, async workers).
3. Datadog, Harness or LaunchDarkly ships row-level data blast radius or a cross-change undo ordering by Q2 2027. Bemi shipping "deploy/commit context + revert by change" kills the data wedge immediately.
4. Platform leads at 3 of the first 5 ICP companies say "Debezium plus a CI hash; we'll build it in a sprint" *and* do so.
5. A paid pilot cannot be closed at $30K or more within 60 days. Undo as insurance may be a "nice after the incident" purchase, not a budget line.

---

## 3. Architecture sketch

```
 INTENT                CHANGE                     DEPLOY                 RUNTIME                     STATE
 ───────               ──────                     ──────                 ───────                     ─────
 ticket / agent  ──►  commits in N repos   ──►  CI: change_set_id  ──►  OTel spans carry      ──►  Postgres WAL:
 session              (Agent Trace /             = H(SHAs, flags,        change.units[] (build       pg_logical_emit_message
 (Entire trailer)      Entire trailer)            migration, prompt)     SHA + flag evals +          (change_set_id, txid)
                       migrations, flags,        signed manifest         prompt/model version)       Kafka headers:
                       prompts, TF applies                                                           change_set_id
        │                    │                         │                        │                          │
        └────────────────────┴───────────┬─────────────┴────────────────────────┴──────────────────────────┘
                                         ▼
                        ┌───────────────────────────────────────────┐
                        │            UNDO GRAPH LEDGER              │
                        │  nodes: intents, change-units, deploys,   │
                        │         services, tables/topics           │
                        │  edges: produced-by, live-on, depends-on, │
                        │         wrote(rows, before-images),       │
                        │         emitted(events→consumers)         │
                        │  derived: reversibility class per change  │
                        │  {flag-safe | redeploy-safe |             │
                        │   needs-repair | irreversible-external}   │
                        └───────────────┬───────────────────────────┘
                                        │  query API + MCP
        ┌───────────────────────────────┼─────────────────────────────────┐
        ▼                               ▼                                 ▼
  Incident bot / AI SRE          Undo planner                        Pre-merge gate
  live_changes(svc, t)           topo-ordered reverts +              "irreversible change:
  blast_radius(change)           scoped inverse writes               needs human / staged
  rank by exposure diff          (rows untouched since) ;            write path"
  (exposed vs unexposed          conflicts → human                   (coding agents, policy
   cohorts on same path)                                              engines call this)
```

**Key design choices (architect's view):**
- **Context propagation, not inference.**
  - Attribution comes from *exposure*: spans and writes tagged with active change-units.
  - That allows a per-change cohort comparison (requests with change X live vs not, on the same route), which handles interleaved changes and partial flag rollouts.
  - Deploy-timestamp correlation, which is what AI SREs do, cannot handle those cases [I].
- **WAL logical messages avoid schema changes.** Stamping is per transaction, not per row column, and the join happens in the CDC consumer. Async workers inherit `change_set_id` from job metadata, like trace-context propagation into queues.
- **Interaction handling.** The ledger records co-exposure, so a failure seen only when A and B are both live is detectable by cohort intersection. This is impossible with per-flag guardrails alone.
- **Undo is a plan, not an action, in v1.** Execution comes later and behind policy. This avoids the accuracy-liability trap that killed thesis C.
- **Standard-first distribution.** Ship as an open OTel processor plus Postgres extension (open source), and sell the ledger, planner and gate.

---

## 4. Evidence table (step 4: is the behavior starting now?)

| Signal | What it shows | Source |
|---|---|---|
| DORA 2025: AI adoption "associated with increasing instability", more change failures, longer resolution | Instability tied to AI change volume | [S](https://www.splunk.com/en_us/blog/learn/state-of-devops), [S](https://redmonk.com/rstephens/2025/12/18/dora2025/) |
| Cortex 2026 Benchmark: PRs/author +20%, incidents/PR +23.5% | More change → more incidents per change | [S](https://go.cortex.io/rs/563-WJM-722/images/2026-Benchmark-Report.pdf?version=0), [S](https://tianpan.co/forum/t/cortex-2026-benchmark-prs-per-author-up-20-but-incidents-per-pr-up-23-5-were-shipping-faster-into-more-fires/619) |
| New Relic 2026 AI Code Report: 78% more incidents, 82% hit a prod failure tied to AI code in 6 months, 86% more senior firefighting (snippet) | Senior engineers are the bottleneck in incidents | [S](https://newrelic.com/sites/default/files/2026-06/New-Relic-2026-AI-Code-Report-06-09-2026.pdf), [S](https://itbrief.co.uk/story/ai-code-praised-in-review-but-faults-rise-in-production) |
| Faros 2026 "Acceleration Whiplash" | Incidents tripled (round 12) | [S](https://pages.faros.ai/hubfs/AI_Engineering_Report_2026_The_Acceleration_Whiplash_Faros.pdf) |
| LaunchDarkly: "Every AI-generated change that touches production should run behind a feature flag"; guarded rollback example (13/243 exposed users saw errors) | The flag-per-change doctrine is spreading, which multiplies change-units | [S](https://launchdarkly.com/docs/guides/cheatsheets/ai-code), [S](https://launchdarkly.com/blog/our-ai-software-factory-saved-me-from-an-incident/) |
| Unleash MCP `evaluate_change` / `wrap_change` in Claude Code, Codex, Antigravity; FeatBit Skills | Agents auto-create flags, so flag sprawl is coming | [S](https://www.getunleash.io/blog/claude-code-unleash-agentic-ai-release-governance), [S](https://featbit.co/ai-control-layer) |
| Cursor Agent Trace RFC (Cognition, Cloudflare, Vercel, Jules, Amp, OpenCode); Thoughtworks Radar | Left-side provenance is standardizing | [S](https://agent-trace.dev/), [S](https://www.infoq.com/news/2026/02/agent-trace-cursor) |
| Entire Checkpoints: session → commit trailer, AI line attribution | Same, commercial | [S](https://docs.entire.io/web/checkpoints), [S](https://futurumgroup.com/?p=92609) |
| OTel semconv: `vcs.change.id`, feature-flag evaluation events; no write-side change identity | The standard has a hole where the primitive belongs | [S](https://opentelemetry.io/docs/specs/semconv/feature-flags/feature-flags-spans), [S](https://opentelemetry.io/docs/specs/semconv/registry/attributes/vcs/index.md) |
| "Rolling back code does not roll back data"; DB rollback pitfalls | Rollback safety is the unsolved part | [S](https://pandastack.io/blog/rollback-failed-deployment), [S](https://www.red-gate.com/simple-talk/sql/database-administration/rollback-and-recovery-troubleshooting-challenges-and-strategies) |
| Change-intelligence / AI-SRE: NeuBird, Rootly, Elastic (72s), Lightrun RCA | Diagnosis is commoditizing, so the bottleneck moves to the undo decision | [S](https://neubird.ai/resources/change-intelligence-correlating-changes-to-incidents), [S](https://rootly.com/blog/telemetry-deploy-correlation-ai-sre), [S](https://www.elastic.co/observability-labs/blog/ai-root-cause-analysis-agent-builder) |
| Meta DRS / RADAR: production incident rate 1/50 on RADAR-reviewed diffs | Hyperscalers invest heavily in change-risk infrastructure (an internal-workaround signal) | [S](https://engineering.fb.com/2025/08/06/developer-tools/diff-risk-score-drs-ai-risk-aware-software-development-meta/) |
| Agent-caused data destruction incidents (Replit, Terraform DB wipe, 48K files) | Buyers primed for "can we undo?" | [S](https://incidentdatabase.ai/entities/ai-code-generation-systems/), [S](https://oecd.ai/en/incidents/2026-03-07-79ec) |
| Bemi ($4M YC): CDC + app context; DBOS provenance time travel | Data-side building blocks exist, and so do fast entrants | [S](https://neon.com/docs/guides/bemi), [S](https://www.infoworld.com/article/3714441/dbos-cloud-overturns-database-on-os-conventions-for-speed.html) |
| Hud ($21M Square Peg) runtime code sensor for agents | Runtime-for-agents is funded; adjacent | [S](https://www.hud.io/introducing-hud), [S](https://www.calcalistech.com/ctechnews/article/rygzfgomwe) |
| Tusk Drift, Speedscale, Keploy behavioral replay | Pre-merge behavioral diff is crowded | [S](https://keploy.io/compare/tusk), [S](https://docs.speedscale.com/) |

**Missing evidence (honest):**
- No public source quantifies *rollback-unsafe* or *data-repair* incidents as a share of agent-caused incidents.
- No job posts were found for "rollback safety" roles. Not searched; the budget ran out.
- No public internal-tool writeups were found of companies stamping writes with deploy IDs, beyond generic audit-trail practice.
- The thesis rests on architectural necessity [I] more than on observed spend.

---

## 5. Scores (bar: avg ≥8.5, none <7)

| Category | Score | Why |
|---|---|---|
| Pain | 7 | Incidents and MTTR are rising and measured; the data-repair tail is severe but episodic |
| Urgency | 6 | Felt acutely after a data incident; most teams today still revert by deploy and survive |
| ROI clarity | 6 | Per-incident savings are real but lumpy; insurance-like purchase |
| Customer accessibility | 6 | Platform/SRE leads are reachable but heavily pitched by AI SRE vendors |
| Pilot speed | 6 | CI + OTel are fast; DB write-path install needs security/DBA approval (weeks) |
| Market size | 7 | Every company with agent-scale change; priced on change volume |
| Expansion | 8 | Undo → gates → agent-executable remediation → standard → audit/insurance |
| Venture potential | 7 | Clear "OTel for changes" story; VCs will ask "why not Datadog?" |
| Defensibility | 6 | Write-path position + cross-vendor neutrality + reversal corpus; 60% buildable in a quarter |
| Why now | 8 | Flag-per-change doctrine plus agent-scale deploys plus left-side provenance standardized in 2026 |
| Competition position | 5 | No direct owner of the join, but Datadog, Harness, LaunchDarkly and Bemi are each one feature away |
| **Average** | **6.5** | Fails A (six categories <7) |

## 6. Classification: **B-weak (conditional), about 10-15% odds**

- **Why not KILL.**
  - Every obvious H3 layer is owned: provenance, flags, AI SRE, runtime sensors, behavioral replay, maps.
  - The *join* is not owned: change identity propagated into runtime **and data writes**, plus reversibility semantics. OTel has a visible hole exactly there.
  - Plausibly, competitors are absent because the problem appears only once flag-per-change and agent-scale deploys coexist, which is a 2026 behavior.
- **Why not A.**
  - The evidence of spend is inferential.
  - Datadog, Harness, LaunchDarkly and Bemi each sit adjacent.
  - Install friction in the DB write path is real.
- **Precise 14-day test (data, not interviews).**
  - At 2 ICP companies, obtain incident records for the last 90 days, plus deploy, flag and migration logs and WAL/CDC archives where retained.
  - Classify each incident: (a) was the culprit a change-unit not identifiable from the deploy timeline alone (interleaved or flag-partial)? (b) was rollback unsafe or data-affecting?
  - **Pass:**
    - at least 30% of incidents fall into (a) or (b);
    - at least 1 data incident needed more than 3 engineer-days of repair;
    - the replayed ledger prototype hits top-3 culprit at 70% or more;
    - the platform lead signs a $30K+ paid pilot.
  - **Kill:** most incidents are revertible by deploy, and data incidents are under 1 per quarter.
- **Note for the founders.** The Vara Architecture graph (round 12) could serve as the *static* half of the ledger: services, stores, flows and file:line evidence. But the moat here is runtime and write-path stamping, not the map.

## 7. Other H3 layers considered and rejected (one line each)
- **Intent→commit provenance:** Entire, Agent Trace, git-ai. Owned and standardizing.
- **Flag-per-agent-change with auto-rollback:** LaunchDarkly CodeControl, Unleash, FeatBit.
- **Runtime understanding for agents:** Hud ($21M), Lightrun.
- **Causal incident attribution by inference:** Rootly, NeuBird, Causely, Komodor, Resolve, Traversal (killed as AI SRE).
- **Behavioral contract diff on PRs:** Tusk Drift, Speedscale, Keploy, Meticulous. Schema contracts: Pact/Buf/Specmatic [U-prior].
- **Executable system knowledge for incidents:** killed as system maps in round 12 (Apiiro, DeepWiki, Port, Datadog IDP).
- **Pre-merge change-risk scoring:** Meta DRS shows the value, but it is prevention and a feature of review vendors (round 3 T3 killed).
