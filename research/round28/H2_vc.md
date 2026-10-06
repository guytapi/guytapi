# Round 28 · H2 (agent output nobody triages) · Skeptical VC partner pass

Date: 2026-10-06. Role: skeptical seed partner. Method: research/round28/BRIEF.md. 21 web searches; the shared search budget ran out after that, so a few checks are marked *(unverified)*. WebFetch is blocked, so every fact comes from search snippets. I did not invent any URLs.

---

## 0. Verdict first

**KILL as a standalone category. Not A. Not B.** The best version I can build, a cross-vendor **ledger of record for agent labor** that finance and auditors trust, scores **6.1**. I would not lead the seed today. I would lead only under the conditions in section 6.

Why, in one paragraph: the queue of agent output is real and measurable. But the money already moved in August–September 2026. CodeRabbit raised a **$143M Series C at a $1.5B valuation** and pitches itself as "the control layer for software change", and it shipped **Triage** (P0–P3 PR prioritization) in September 2026. GitHub **Agent HQ / Mission Control** is already cross-vendor (Claude, Codex, Cognition, Google, xAI). **Linear** and **Jira** let you assign work to Claude, Codex, Cursor, Copilot and Devin, and Atlassian shipped **Jira Planner** for intents and specs. **Cursor** owns Graphite and ships best-of-N with automatic judging. **DX, Jellyfish, Larridin and LinearB** already sell cost per PR. The "neutral layer because companies use multiple vendors" argument fails: the tracker and the forge are already neutral among agent vendors. The one thing they are *not* neutral about is themselves, and that thin argument is the only one left standing (section 3).

---

## 1. Pushing H2 to 2028-2029

| Order | Consequence | Who owns it already |
|---|---|---|
| 1st | Pile of stale, duplicate and conflicting agent PRs | CodeRabbit Triage, GitHub Agent HQ, Graphite/Cursor, merge queues. **Taken.** |
| 2nd | Most agent output is *meant* to be thrown away (best-of-N, speculative attempts). "Triage" becomes **selection**, and the merge rate stops meaning anything | Cursor best-of-N + auto-judge (Cursor 2.2 / 3), Emdash, TaskBounty. **Platform feature.** |
| 2nd | Coordination before the PR: two agents doing the same intent; 27.67% conflict rate (AgenticFlict); 40.2% of repos have agent PR pairs that overlap in time | Trackers dispatch the work (Linear, Jira, Agent HQ), so dedup at dispatch is a feature for them. Research prototypes use an append-only ledger. **Feature.** |
| 2nd | Planning shifts from tickets to intents and specs | Jira Planner, Linear, Traycer Epic Mode, Intent, Kiro/Tessl. **Crowded.** |
| 3rd | **Judgment is the scarce input**: every accept, reject or edit of agent output is a company's "taste", and whoever holds that data can automate the next layer of judgment | Every review bot learns per tool (CodeRabbit learnings, Greptile, Bugbot rules). A portable, company-owned judge comes close to banned "generic evals" and to the killed "in-loop verification judge" (5.5). |
| 3rd | **Agent labor becomes a material cost line that finance must account for** (Uber used up its 2026 AI budget by April and capped spend at $1,500 per engineer per tool per month; ~$144M implied). Auditors need a task-level "nexus of cost" before token spend can be capitalized under ASC 350-40 (Deloitte DART, EisnerAmper) | DX AI cost report (cost per PR), Jellyfish AI Impact (spend by initiative), Larridin (cost per outcome), CodeROI (R&D credit, §174, capitalization on AI spend). **Early but occupied.** |
| 3rd | Outcome pricing for agent work (Sourcegraph Batch Changes bills per merged changeset; TaskBounty pays on merge) needs a meter both sides trust | Vendor-metered today. Round 3's T2 (auditor of outcome-priced work) was killed at 4.7. |

**New category?** Only one consequence suggests a category rather than a feature: **auditable accounting for machine labor**, the payroll and timesheet equivalent for agents, which feeds capitalization, tax credits, chargeback, vendor settlement and budget allocation. Everything else is a forge or tracker feature.

---

## 2. Evidence the behavior is starting now

- **Agent PRs fail in bulk.** LinearB 2026 benchmarks (8.1M PRs, ~4,800 teams): AI PRs merge at less than half the human rate. The 32.7% vs 84.5% figure appears in secondary snippets; the exact number was *unverified* against LinearB. AIDev (9,428 agent PRs): merge probability is 84.3% for Claude Code and 43% for Devin. In failed agent PRs, 67.9% of rejections have no explicit reviewer feedback (arXiv 2601.15195).
- **Duplication and conflict.** AgenticFlict: 142K+ agent PRs, 27.67% conflict rate. "Prior resolution of the same issue by another PR" is a top cause of non-merge (arXiv 2602.00164).
- **Unit economics are now a CFO question.** Cost per merged PR is a named metric (Unblocked, Larridin, developertoolkit.ai, Insight "cost to a merged feature" 2026-07-06). The same feature cost $7–$70 depending on model and harness.
- **Budget shock.** Uber's CTO said the 2026 AI budget was gone by April; Microsoft cut internal Claude Code licenses (kucoin/feedbagel snippets; secondary sources).
- **Multiple vendors per company.** 59% of developers use 3+ AI coding tools; Cursor + Claude Code is the most common pair (secondary survey snippets).
- **Finance rules exist.** Deloitte DART has guidance on AI costs in internal-use software; capitalizing tokens requires task-level attribution.

---

## 3. Who captures value when output is abundant and judgment is scarce?

My answer as a partner: **whoever owns the dispatch point and the merge point.** That is GitHub (forge + Agent HQ + Copilot metrics API), Cursor (IDE + Graphite + best-of-N), Linear/Atlassian (intent + dispatch; Atlassian also owns DX *(acquisition ~$1B, Sep 2025, from memory, unverified this round)*), and CodeRabbit (the change-control layer, $1.5B). Owning the queue means owning the place where humans decide. No new entrant gets there by building the queue UI.

**Where incentives *force* a neutral layer:**
1. **Several agent vendors? Not enough.** Agent HQ, Linear and Jira are already multi-agent, and they want to be the neutral dispatcher.
2. **Finance needs cost per shipped outcome? Partly.** Each platform reports its own agent's success: GitHub's Copilot metrics API counts *Copilot* coding-agent PRs merged. A CFO comparing Copilot, Claude, Codex and Cursor on cost per shipped change, and an auditor signing off on capitalized token spend, both need a party with no product in the race. Analogy: ad verification (DoubleVerify, IAS) exists because platforms grade their own homework. This is the only real structural argument.
3. **Planning moves from tickets to intents? No.** The intent lives in the tracker; Jira Planner and Linear absorb it.

So the only version worth writing up is #2.

---

## 4. Best thesis: **Agent Labor Ledger**, the auditor-grade system of record for machine engineering labor

**One-line problem.** Companies now spend 8-9 figures a year on coding agents from 3+ vendors. Finance cannot say what each dollar shipped, cannot capitalize the spend without a task-level cost trail, and has to rely on numbers reported by the vendors being measured.

**Why now.**
- Spend is suddenly large: Uber blew its budget, $500–$2,000 per engineer per month, per-tool caps.
- Agents from several vendors run in the same repos.
- ASC 350-40 lets companies capitalize agent token cost *only* with a "nexus of cost" tying spend to specific capitalizable tasks. That is a direct EBITDA lever, and most companies cannot prove the link today.
- Outcome-priced agent contracts (per merged changeset) are starting.
- Merge rates of 33–84% across vendors mean the cost per attempt understates the true cost by up to 3x.

**Exact buyer.** VP Finance / Corporate Controller (capitalization, audit), with the CFO signing. Co-buyer: VP Engineering / Head of Developer Productivity, who wants vendor allocation.

**Exact ICP.** US companies with 200–3,000 engineers, preparing for or after IPO (they capitalize software and face audit scrutiny), running ≥2 coding-agent vendors, with ≥$3M a year in agent and token spend. Examples of the profile: late-stage fintech and SaaS that already publish background-agent work.

**Current workaround.**
- Spreadsheets that allocate the vendor invoice pro rata to headcount, or no capitalization of AI spend at all.
- DX / Jellyfish cost-per-PR dashboards, which are estimates built for engineering and not evidence auditors accept.
- Per-vendor admin consoles and Uber-style hard caps.
- Jellyfish or Pensero-style capitalization reports based on ticket time, built for human labor.

**Why incumbents cannot easily own it.**
- GitHub, Cursor, Atlassian and Anthropic/OpenAI are each *a vendor being measured*, so their numbers lack independence for audit and vendor comparison.
- Each sees only its own surface: GitHub doesn't see Linear-dispatched Codex cloud runs' token invoices; Cursor doesn't see Copilot.

**Honest rebuttal:** DX (inside Atlassian), Jellyfish, LinearB and Larridin are not agent vendors, already ingest multiple tools, and already show cost per PR. The independence argument works against GitHub, not against them. Their weakness is narrower: they are engineering-productivity tools built on estimates, not ledgers that auditors rely on.

**30-day MVP.**
- Connectors: GitHub (PRs, commits, agent co-author trailers), Linear/Jira (intent IDs), and billing/usage exports from Anthropic, OpenAI, Cursor and Copilot.
- Join each agent session to its task, then its PR, then its outcome (merged, abandoned, reverted within 30 days).
- Outputs: (a) cost per shipped change by vendor, model and team; (b) a capitalization schedule (tokens and seat cost tagged to capitalizable projects in the application-development stage) with a drill-down evidence trail per dollar; (c) a "waste" report on spend for abandoned, duplicate and superseded work.

**Pilot design.**
- Two design partners; replay the last 90 days of spend.
- Pass: ≥$500K of agent spend newly supportable for capitalization, accepted in principle by the partner's external auditor, AND ≥20% of spend identified as non-shipping waste, AND the controller agrees to use it for the quarter close.
- Duration: 30 days to replay, one quarter-close to validate.

**Pricing hypothesis.**
- 0.5–1.5% of agent spend under management, with a $40K annual floor.
- Alternatively, a share of the first-year EBITDA uplift from capitalization, capped. At $10M of agent spend that is $50–150K ARR.

**Expansion path.**
1. Capitalization and cost per outcome.
2. Vendor allocation: routing budget to the vendor and model with the lowest cost per shipped change.
3. Settlement for outcome-priced contracts (a neutral meter for pay-per-merge).
4. Admission control: budget plus judgment-capacity limits before agents start work.
5. All machine labor beyond code (support, ops and finance agents): "payroll for agents".

**Moat.**
- A cross-vendor benchmark of cost per shipped change by task class: a data network effect, if it reaches hundreds of companies.
- Auditor acceptance: once Big 4 workpapers reference the ledger, switching is costly.

Both moats are slow, and neither exists at seed.

**Why it could be $10B+.**
- Rough sizing: if agent labor reaches 20–40% of a ~$1T+ global software R&D spend, it becomes the second-largest R&D cost line after people.
- Payroll/HCM is a $10B+-company category because labor is the largest cost and needs a trusted system of record (ADP, Workday). An auditor-trusted record for machine labor across every vendor, the "Workday for agent labor", is the only H2 framing that is not a GitHub feature.

**Discount for skepticism:** the same logic was tried for cloud cost (FinOps). That produced good companies (Vantage, CloudHealth sold to VMware for ~$500M, ProsperOps bought by Flexera), but no $10B independent company, because the clouds absorbed the basics.

**Direct competitors and adjacent threats.**
- DX (Atlassian *(unverified)*): AI cost management report with cost per PR.
- Jellyfish AI Impact: spend by tool, team and initiative; capitalization reports.
- Larridin: cost per outcome, agent effectiveness score.
- LinearB benchmarks; Faros; Pensero (capitalization).
- CodeROI: R&D credit, §174 and capitalization on AI spend.
- GitHub Copilot usage metrics API (per-repo agent PR merges).
- AI FinOps (Vantage, Pay-i, Revenium; round 1's B killed at 5.6).
- CodeRabbit ($1.5B, "control layer for software change").
- Anthropic/OpenAI enterprise admin analytics.

**One sentence to send a CFO.** "You spent $X on coding agents last year across four vendors; we'll show which dollars actually shipped, and give your auditor the task-level evidence to capitalize the ones that did."

**Hard kill criteria.**
- The external auditor at both design partners declines to rely on the ledger, or says pro-rata allocation is enough.
- Less than $300K of newly capitalizable spend per partner.
- DX or Jellyfish ships auditor-grade capitalization evidence for agent spend before we have 5 paying customers.
- Agent vendors move to flat enterprise licenses, so spend stops being variable and attributable.
- Controllers tell us AI spend is immaterial to their P&L.

### Scores (honest)

| Category | Score | Why |
|---|---|---|
| Pain | 6 | Real for the CFO after Uber-type overruns, but it is a reporting and EBITDA problem, not an outage |
| Urgency | 6 | Budget overruns create urgency to cap spend, which per-tool caps and vendor admin already solve; capitalization is upside, not a fire |
| ROI clarity | 7 | Capitalized dollars are concrete and auditable |
| Customer accessibility | 6 | Controllers are reachable, but buying this is new behavior; engineering buys DX/Jellyfish instead |
| Pilot speed | 7 | Replaying 90 days is fast; auditor acceptance waits for a quarter close |
| Market size | 6 | Today, % of agent spend at a few thousand companies is a few hundred $M of TAM; the $10B case depends on "all machine labor" |
| Expansion | 7 | Clear ladder toward settlement, allocation and non-code agents |
| Venture potential | 6 | A FinOps-shaped outcome is more likely than a Workday-shaped one |
| Defensibility | 4 | Integrations can be copied; benchmark and auditor moats are slow |
| Why now | 8 | Spend shock + ASC 350-40 guidance + multiple vendors + outcome pricing, all in 2026 |
| Competition position | 4 | DX (Atlassian), Jellyfish, Larridin, CodeROI each about one feature away |
| **Average** | **6.1** | Three categories below 7; fails the A bar |

**Classification: KILL.** It fails A (6.1, with categories below 7). It fails B because competitors exist, so the absence of competitors cannot be the premise. CodeROI and Jellyfish already sell the capitalization wedge.

---

## 5. Other versions considered and killed (≤1 line each)

| Version | Why it dies |
|---|---|
| Queue / PR triage for agent output | CodeRabbit Triage (Sep 2026) + $143M Series C; GitHub Agent HQ |
| Cross-vendor intent ledger / agent dispatch | Linear (Devin, Cursor, Codex, Copilot, Warp), Jira Agents GA May 2026 + Jira Planner, Agent HQ Mission Control |
| Pre-PR dedup / conflict leasing between agents | A feature of the dispatcher; also research prototypes (append-only coordination logs) |
| Best-of-N selection / arbitration | Cursor best-of-N + auto-judge, Emdash, TaskBounty |
| Portable company "taste" judge from accept/reject history | Review bots learn per tool; borders on banned generic evals and the killed in-loop judge (5.5) |
| Neutral meter for outcome-priced coding contracts | Too few such contracts (Sourcegraph only); T2 killed at 4.7 |

---

## 6. What would make me lead / what stops me

**What would make me lead:**
1. Evidence that a Big 4 auditor or a public-company controller **refuses** to rely on DX, Jellyfish or vendor consoles for capitalizing agent spend and wants an independent ledger. That gives a regulatory-grade wedge incumbents can't fake.
2. A founder from controllership or audit (ex-Big 4 tech accounting + ex-platform engineer), not a devtools founder. The buyer is finance.
3. Two design partners each showing ≥$1M a year of agent spend that becomes capitalizable, i.e. an EBITDA uplift the CFO can quote on an earnings call.
4. Evidence that outcome-priced agent contracts are spreading beyond Sourcegraph (≥3 major vendors bill per merge or per resolved task). Then a neutral settlement meter becomes necessary, like ad verification.

**What stops me:**
1. CodeRabbit, GitHub, Cursor and Atlassian already compete for the "control layer for change". The valuable chokepoints (dispatch and merge) are owned.
2. Atlassian owns both the intent (Jira) and the measurement (DX *(unverified)*), so it can bundle cost per outcome for free.
3. This is FinOps again: the cloud-cost precedent produced exits of ~$0.5–1B, not $10B, because platforms commoditized visibility.
4. Agent vendors may move to flat enterprise licenses (Uber-style caps push this way), which removes variable spend to attribute.
5. The STATUS.md pattern holds: this gap is visible in public sources, so it gets funded within 6 months, and it already has been, by DX, Jellyfish, Larridin and CodeROI.

**Why $10B rather than a GitHub feature?** Only if the company becomes the independent system of record for *all* machine labor cost and outcome (code first, then support, ops and finance agents), relied on by auditors and used to settle outcome-priced contracts. Anything narrower (queue, triage, dedup, intent, cost per PR dashboard) is a GitHub, Linear, Cursor or CodeRabbit feature, and most of it has already shipped.

---

## Sources (from search snippets)
- GitHub Agent HQ: https://sdtimes.com/ai/github-unveils-agent-hq-the-next-evolution-of-its-platform-that-focuses-on-agent-based-development/ ; https://www.i-programmer.info/news/105-artificial-intelligence/18651-github-adds-claude-and-codex-to-agent-hq.html ; https://venturebeat.com/ai/githubs-agent-hq-aims-to-solve-enterprises-biggest-ai-coding-problem-too
- Linear agents / coding sessions: https://linear.app/docs/agents-in-linear ; https://linear.app/changelog/2026-06-11-coding-sessions ; https://sacra.com/chat/h/fce0f56a-9255-4d05-aaba-2221c1ee4c6b/
- Jira agents / Planner: https://jirareleases.atlassian.com/announcements/put-ai-teammates-to-work-right-inside-jira ; https://www.atlassian.com/blog/jira/introducing-jira-planner
- CodeRabbit: https://siliconangle.com/2026/08/12/coderabbit-bags-143m-help-companies-get-grip-explosion-ai-generated-code/ ; https://coderabbit.ai/blog/coderabbit-triage ; https://infoworld.com/article/4208611/coderabbit-targets-ai-generated-code-overload-with-agentic-change-management.html
- Cursor/Graphite: https://siliconangle.com/2025/12/19/cursor-acquires-ai-code-review-startup-graphite/ ; best-of-N: https://forum.cursor.com/t/cursor-2-2-multi-agent-judging/145826 ; https://docs.emdash.sh/best-of-n
- Agent PR failure research: https://arxiv.org/html/2601.15195v1 ; https://arxiv.org/abs/2602.00164v1 ; https://codex.danielvaughan.com/2026/08/04/what-220000-pull-requests-reveal-agentic-pr-task-routing-codex-cli-test-coverage-gaps/ ; https://codex.danielvaughan.com/2026/07/28/agent-pr-merge-conflicts-concurrent-coding-agents-codex-cli-worktree-isolation-coordination-defence/ ; https://linearb.io/dev-interrupted/podcast/linearb-2026-benchmarks-ai-pr-merge-rate
- Cost per merged PR: https://getunblocked.com/blog/cost-per-merged-pr/index.md ; https://larridin.com/measurement-guide/agent-effectiveness/cost-per-outcome/ ; https://blog.insight-services-apac.dev/2026/07/06/cost-to-a-merged-feature ; https://developertoolkit.ai/en/strategy/economics/
- Measurement vendors: https://getdx.com/blog/meet-the-new-ai-cost-management-report/ ; https://jellyfish.co/platform/jellyfish-ai-impact/investment-management/ ; https://github.blog/changelog/2026-07-17-repository-level-github-copilot-usage-metrics-generally-available/
- Spend shock: https://www.kucoin.com/news/flash/microsoft-and-uber-report-ai-cost-overruns-as-claude-code-spending-surpasses-budgets ; https://feedbagel.com/post/ubers-1500month-ai-limit-is-a-useful-signal-for-ai-tool-pricing
- Capitalization: https://dart.deloitte.com/USDART/home/publications/deloitte/industry/technology/accounting-ai-costs-associated-internal-use-software-development ; https://www.eisneramper.com/insights/technical-accounting-advisory/accounting-for-ai-data-consumption-cost-0726/ ; CodeROI: https://www.webull.com/news/15508547898909696
- Outcome pricing: https://agentpatterns.ai/patterns/agent-design/outcome-pricing-as-scope-signal/ ; TaskBounty: https://peerpush.com/p/taskbounty
- Multi-tool use: https://edge.amplifying.ai/research/state-of-coding-agents ; https://andrew.ooo/answers/ai-coding-agent-market-share-cursor-claude-code-copilot-july-2026/
- Actual AI seed: https://finder.techleap.nl/news/feed/actual-ai-raises-3-2m-for-ai-agents
