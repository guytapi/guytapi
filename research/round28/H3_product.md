# Round 28 — H3 (incidents in code no human understands): first-principles product thesis

**Date:** 2026-10-06 | **Role:** first-principles product thinker | **Searches:** 16 run, then the shared per-turn web-search limit was hit, so every claim below comes from those 16 searches plus earlier rounds. WebFetch and Reddit were blocked, so evidence comes from search snippets only.
Legend: [S] = seen in a search result this round. [R] = from an earlier round in this repo. [U] = unverified (from memory, not re-checked this round). [I] = my inference.

**Bottom line:** the best thesis I could build is the **Production Black Box**: a neutral, tamper-evident record of every change made to production, and of the full production state at any moment, which agents both change and operate. It is a real future category, but it **does not reach A (6.1 average) and is too crowded at the edges to be B. Verdict: KILL.** The only open part is **neutrality**: a record that the agents being judged do not keep themselves. That part depends on insurers and contracts requiring it, and the brief rules out insurers as primary buyers. It is noted below as a tripwire to watch, not as a candidate.

---

## 1. Pushing H3 to 2028-2029

Assume most production code is written by agents, AI SRE agents (Resolve, Traversal Workers, AWS/Azure SRE agents) take remediation actions without asking, and vendors' agents push changes into your stack every day. The "person who knows the system" no longer exists. Below are the second- and third-order consequences, each with the obvious product and why it is already owned.

| # | Consequence (2028) | Obvious product | Who already owns it |
|---|---|---|---|
| 1 | Nobody can explain the failing code at 2 a.m. "Comprehension debt" brings in a new metric, MTTE (mean time to explain) [S tianpan.co] | AI SRE agent that explains and fixes | Resolve ($1B+ valuation; $125M reported Feb 2026) [S], Traversal ($48M A, Kleiner/Sequoia) [S], Cleric [S], Datadog Bits [U] — **killed as crowded** |
| 2 | **Production memory:** why the system is built the way it is, how it has failed before, and what fixed it | Knowledge graph of production | Traversal "Production World Model" + "Knowledge Bank" (explicitly pitched as the lock-in) [S]; Resolve's "always-up-to-date knowledge graph … code and configuration changes" [S] |
| 3 | **Change provenance:** which lines came from which agent, under whose authority | Attribution records | Cursor **Agent Trace** open spec, backed by Cognition, Cloudflare, Vercel, Jules, Amp (on the Thoughtworks Radar) [S]; Sourcegraph "agent provenance" [S]; TierZero audit trail [S] |
| 4 | **Change-control evidence for regulators:** DORA's final major-incident report requires a root cause. 3,383 major incidents were reported in 2025 and 29% started at third parties [S ESAs Jun 2026] | Change ledger and evidence store | **Kosli** ($10M Series A led by Deutsche Bank; now pitched as "governance infrastructure for AI-assisted software delivery … ship at agentic speed") [S]; ServiceNow change management [U] |
| 5 | **Recovery without understanding:** the only safe fix is to return to a known-good state, but agent changes span code, configuration, flags, schemas and infrastructure | Point-in-time rollback of the cloud | ControlMonkey "time machine" daily snapshots (Mar 2026: now also covers Datadog/Grafana configuration) [S]; Firefly asset history and revert [S]; Argo/LaunchDarkly per layer [U]; Rubrik/backup vendors for data [R thesis C] |
| 6 | **Many agents acting on one system:** remediation agents fight over stale state | Arbitration and locking for agent actions | Quali Torque ("arbitrates conflicting intentions before race conditions occur") [S]; SuperPlane (€2.28M pre-seed, open-source control plane for agents and engineers on production) [S]; agent control planes (Obot, Lyzr) [S] — also close to banned generic orchestration and identity |
| 7 | **Accountability disputes:** the AWS Kiro agent "deleted and recreated" an environment, causing a 13-hour outage; AWS called it "user error … not AI" [S FT via Engadget/Decoder/OECD AI incident log] | Neutral incident attribution | **No product found** [I] |
| 8 | **Insurance and representations:** carriers add AI sublimits of about 10% of limits (Beazley, QBE). Questionnaires ask for a kill switch, a named accountable executive and data provenance. A policyholder's claim that "all production code is peer-reviewed" quietly becomes false once agents skip review, which gives the insurer grounds to deny [S tianpan/cloudapper/buildmvpfast, secondary sources] | Continuous proof that control claims hold | Vanta/Drata (GRC) [U] + Kosli [S] — and insurers are not primary buyers (per the brief) |
| 9 | **Customer SLA disputes:** vendors write "customer solely responsible for outputs" into contracts; agentic contracts shift toward BPO-style terms [S Mayer Brown, Morgan Lewis] | Proof of fault for SLAs | Too little money: service credits are small percentages of monthly fees [S redresscompliance] |

**Pattern:** every layer an actor would build (explain, remember, attribute, roll back, arbitrate) has a funded owner as of Oct 2026. The one layer no actor can credibly own is the **neutral record that actors are judged against** (consequence 7). In the Kiro case, the party that built the agent was also the party that declared the cause. In aviation, the flight recorder is not built by the pilot or the airline's PR team.

---

## 2. Thesis: Production Black Box

### One-line problem
Once agents both write and operate production, nobody (human or agent) can say with authority **what the whole production state was at a given moment, what changed it, under whose authority and with what stated intent**. Without that, incidents can't be pinned on a cause, recovery can't target a coherent known-good state, and accountability to customers, regulators and agent vendors can't be defended.

### Why this exists now
- Agents now change production outside git: the AWS Kiro outage (Dec 2025, reported Feb 2026) was an agent acting with human-level permissions without approval [S]. At least two AWS outages have been linked to AI tools [S Tom's Guide/Sherwood].
- AI SRE agents now take remediation actions without being asked (Traversal Workers, 2026) [S]. Production is mutated by actors whose own logs are the only record.
- A secondary-source claim says 68% of organizations cannot tell agent actions from human actions after the fact [S TierZero blog, unverified primary].
- Line-level attribution (Agent Trace) exists for code but stops at the merge. Configuration, flags, cloud API calls, schema migrations and prompt/model swaps have no shared record [I].
- Insurers are writing autonomy questions and AI sublimits into 2026 riders [S]. DORA requires root-cause final reports [S].

### Exact buyer
VP Infrastructure / Head of SRE, co-signed by the CISO or Head of Operational Resilience in regulated firms. Budget: change-management/GRC tooling or observability.

### Exact ICP
EU/UK-regulated fintechs, payment firms and insurtechs with 200-2,000 engineers and more than 40% agent-authored PRs. At least one AI SRE or ops agent has write access to production. They file DORA major-incident reports or the UK operational-resilience equivalent.

### Current workaround
They piece together a timeline from GitHub, Argo, LaunchDarkly, Terraform state, CloudTrail and the agent's own session logs, by hand, during the postmortem. Kosli or ServiceNow covers deploy evidence only. AI SRE tools build a private graph the customer cannot audit independently.

### Why incumbents can't easily own it
- **AI SRE vendors and agent vendors are the parties being judged.** A record they keep has the Kiro problem: the actor writes the verdict. This is the only structural argument.
- Observability vendors (Datadog) store telemetry, not authority and intent. They also sell agents themselves, which creates the same conflict.
- **Honest counterpoint:** Kosli is already neutral, already sells in this ICP (Deutsche Bank is an investor) and already pitches itself for agentic delivery. ControlMonkey/Firefly already snapshot cloud state. A neutral ledger is something Kosli could ship as a feature, not something it can't own.

### 30-day MVP
- A read-only collector across GitHub (+Agent Trace), Argo/Flux, LaunchDarkly, Terraform state/CloudTrail, and the audit logs of one AI SRE agent.
- It builds a **content-addressed production state version** every N minutes and a hash-chained mutation log: actor, delegating human or policy, stated intent if available, diff.
- Output 1: during an incident, "diff production between the last healthy time and now", ranked candidate causes.
- Output 2: a one-click chain-of-custody PDF for the DORA final report.

### Pilot design
- Replay the last 10 major incidents at 2 ICP firms.
- Pass: the candidate set contains the true cause in at least 8 of 10; reconstruction time falls by at least 50%; at least 1 incident had an agent-originated mutation missing from their own timeline.
- Commercial pass: a $40K+ paid pilot.

### Pricing hypothesis
$30-80K per year platform fee plus a fee per production environment. An "attested record" tier ($150K+) for firms that use it for regulators, insurers or customer RCAs.

### Expansion path
- Incident diff → coherent restore (orchestrating per-layer rollback to one state version).
- → Pre-change admission ("this mutation is not reversible to the current state version") → continuous control-assertion proof for SOC 2, DORA and insurers.
- → An inter-company black box (vendor-change feeds into customers' recorders).
- → A standard record format that contracts and riders cite.

### Moat
- Hash-chained history can't be backfilled: a recorder installed later lacks the earlier years [I].
- Neutrality, if it becomes a contract or rider requirement.
- Weak overall: collectors are easy to copy, and Agent Trace plus OpenTelemetry-style standards make the format a commodity.

### Why it could be $10B+
If 2028 contracts, insurers and regulators require an **independent** production recorder for any system where agents hold write access (the way aviation requires a flight data recorder), every company running agents in production pays for it, as a separate line item from observability. That is a large conditional. Today no regulator or insurer requires independence. Insurer questionnaires ask for a kill switch and a named executive, not a third-party recorder [S].

### Direct competitors and adjacent threats
- Kosli (closest; neutral, regulated ICP, agentic positioning) [S].
- ControlMonkey and Firefly (cloud state history and revert) [S].
- Quali Torque and SuperPlane (governed gateway that sees every agent mutation, so it gets the log for free) [S].
- Resolve/Traversal knowledge graphs [S]; Datadog change tracking and Feature Flags (Feb 2026) [S].
- Agent Trace (attribution standard) [S]; Sourcegraph provenance [S]; TierZero [S].
- ServiceNow change management, Komodor, Harness [U]; Vanta/Drata for control assertions [U].

### One sentence to send a CTO
"When the next outage comes from an agent's change, can you prove in an hour, to your regulator and to the agent vendor, the exact production state before and after and who authorized each change? We give you a neutral, tamper-evident black box for production that the agents you're judging don't keep themselves."

### Hard kill criteria
- In 2 replays, at least 3 of 10 incidents are not reconstructed better than the firm's existing Kosli/Datadog/AI SRE timeline.
- No buyer will pay for **neutrality** over the AI SRE vendor's own graph.
- Kosli or an AI SRE vendor ships state-version diffs within the pilot window.
- No insurer, regulator or enterprise customer has asked for an independent change record by mid-2027.

### Scores (honest)

| Category | Score | Reason |
|---|---|---|
| Pain | 6 | Real (MTTE, Kiro), but felt during postmortems rather than as a budgeted line |
| Urgency | 5 | Agent write access to production is still mostly gated in 2026; pain peaks in 2028 |
| ROI clarity | 5 | MTTR savings are shared credit with AI SRE tools; regulatory value is soft |
| Customer accessibility | 6 | SRE/resilience heads are reachable; regulated firms buy slowly |
| Pilot speed | 7 | Read-only collectors plus incident replay are possible in 30 days |
| Market size | 7 | Every company with agents in production, if it becomes a requirement |
| Expansion | 8 | Restore, admission control, control assertions, inter-company recorder |
| Venture potential | 7 | Only if independence becomes required |
| Defensibility | 5 | History lock-in only; collectors and format are commoditizing |
| Why now | 7 | Kiro, Traversal Workers, AI riders, DORA reports in 2026 |
| Competition position | 4 | Kosli + ControlMonkey/Firefly + Quali + AI SRE graphs surround it |
| **Average** | **6.1** | Fails the A bar (8.5, none below 7) |

**Classification: KILL.** It is not B, because the uncrowded core (neutrality) depends on an external requirement (insurers, regulators, contracts) that has not appeared, and its most likely sponsor (insurers) is excluded as a primary buyer. Every component that is useful without that requirement has a funded owner.

---

## 3. Other directions checked and killed

| Thesis | Why killed |
|---|---|
| Arbitration and locking for production changes made by many agents | Quali Torque already markets "arbitrates conflicting intentions"; SuperPlane is funded; close to banned generic orchestration and identity [S] |
| Production memory / system world model | It is Traversal's and Resolve's main moat [S] |
| Behavioral contract registry (humans approve changes in behavior, not code; contracts learned from traffic) | Most interesting intellectually. Speedscale, Tusk, Keploy, Meticulous, Antithesis and Postman (Akita) cover traffic-derived behavior [U, search budget ran out before checking]. Probably a feature of testing vendors |
| Sign-off tool so a named accountable human can legitimately approve agent changes | Collapses into AI code review (CodeRabbit, Greptile, Graphite) and the round-12 Apiiro kill [R] |
| Neutral outage-forensics service for SLA, insurer and agent-vendor disputes | No buyer: SLA credits are tiny [S], insurers are excluded, disputes are rare and settled privately |
| Radar for upstream vendor changes (vendor agents ship daily and break you) | Killed in round 11 ("what breaks next") [R] |

## 4. Tripwire worth watching (not a thesis)
If any of the following happens, reopen the Production Black Box as a B candidate with neutrality as the core:
- a cyber/E&O carrier or Lloyd's market bulletin requires an **independent** record of agent production changes;
- a DORA/ESAs or FCA statement names agent-originated changes in root-cause expectations;
- a public outage dispute between an agent vendor and an operator turns on whose logs are believed.

Sources (search results this round): techcrunch.com/2026/02/04/ai-sre-resolve-ai-confirms-125m-raise-unicorn-valuation/ ; traversal.com/comparison/traversal-vs-resolve-ai ; resolve.ai/our-agentic-ai ; engadget.com/ai/13-hour-aws-outage-reportedly-caused-by-amazons-own-ai-tools-170930190.html ; computing.co.uk/news/2026/ai/aws-blames-user-error-not-ai ; oecd.ai/en/incidents/2026-02-20-dd2a ; agent-trace.dev ; thoughtworks.com/radar/platforms/agent-trace ; kosli.com/blog/tags/agentic/ ; startuplab.no/insights/in-the-news-kosli-raises-100-mnok-in-series-a ; securitybrief.news/story/controlmonkey-adds-observability-recovery-for-cloud-tools ; firefly.ai/controlmonkey-vs-firefly ; quali.com/blog/multiple-ai-agents-one-infrastructure-zero-coordination/ ; therecursive.com/serbian-superplane-pre-seed-dev-tool.md ; esma.europa.eu/sites/default/files/2026-06/JC_2026_16_ESAs_2025_report_on_major_ICT-related_incidents.pdf ; tianpan.co/blog/2026/06/21/comprehension-debt-the-system-no-human-understands ; tianpan.co/blog/2026-04-27-ai-cyber-insurance-agent-action-coverage-gap ; buildmvpfast.com/blog/cyber-insurance-ai-requirements-2026 ; tierzero.ai/blog/ai-agent-audit-trail/ ; sourcegraph.com/blog/compliance-first-ai-proving-agent-provenance ; itbrief.news/story/datadog-links-feature-flags-with-real-time-telemetry ; mayerbrown.com/es/insights/publications/2026/02/contracting-for-agentic-ai-solutions-shifting-the-model-from-saas-to-services ; redresscompliance.com/ai-sla-uptime-enterprise-agreement-negotiation.html
