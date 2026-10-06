# Customer Discovery Machine

**Purpose:** find private pain created by AI agents, autonomous engineering and AI-native organizations, before it is visible as a startup category. Do not design a product until five CTOs independently describe the same pain in different words.

**How 27 rounds of public research shape this:** they are negative training data. Pain that is already loud in public (code review volume, CI cost, AI spend caps, secrets in transcripts, agent identity, MCP gateways, model migrations, eval tooling) already has vendors. The hypotheses below deliberately target **internal operational failures that companies do not publish**: margins, headcount reallocation, internal process breakdowns, and work nobody owns. Interviews must probe *below* the public versions; if an interviewee's answer is "we use vendor X and it works", that is a kill signal for that hypothesis.

---

## Part 1. Ten problem-discovery hypotheses

Each is a hidden operational failure, not a product. "Public decoy" names the adjacent pain that is already served, so interviews can tell the difference.

### H1. Human supervision scales linearly at AI app companies
**Failure:** AI-native B2B companies sell "autonomous" agents, but behind every customer sits a growing team of humans who configure, monitor, correct and escalate for that customer's agent. Supervision headcount grows with customers, not with product maturity, and quietly destroys gross margin.
**First to feel it:** CEO / CTO / VP Operations at a Series A–C AI app company (support agents, voice agents, legal/finance agents, vertical agents) with 20–300 customers.
**Public decoy:** FDE deployment tooling (killed: vendors build in-house), agent QA vendors (Hamming, Coval).

### H2. Agent output nobody triages
**Failure:** engineers launch background agent tasks freely; the result is a growing pile of half-finished PRs, duplicated work, conflicting changes and abandoned branches. Nobody owns the queue of agent output, so throughput gains disappear into triage and rework.
**First to feel it:** VP Engineering / engineering productivity lead at a 50–500 engineer software company where >30% of PRs are agent-authored.
**Public decoy:** AI code review and auto-merge (killed: GitHub/Cursor/Graphite).

### H3. Incidents in code no human understands
**Failure:** as agents author more production changes, incident response slows: on-call engineers can't find anyone who understands the failing code, postmortems can't assign ownership, and MTTR rises even though deploy frequency rose.
**First to feel it:** Head of SRE / VP Engineering / incident commander at a company with on-call rotations and >30% agent-authored code.
**Public decoy:** AI SRE agents (Resolve, Traversal) and comprehension-debt talk.

### H4. The spec writer became the bottleneck
**Failure:** coding is cheap, so senior engineers, tech leads and PMs now spend most of their time writing precise task specs and acceptance criteria for agents, and checking whether the output matches intent. The scarce resource moved from coding to specifying and judging, and nobody planned for it.
**First to feel it:** CTO / VP Engineering / Head of Product at AI-forward software companies.
**Public decoy:** spec-driven development tools (Kiro, Tessl).

### H5. Shared environments break under parallel agents
**Failure:** dozens of agents run tests in parallel against shared staging, seeded databases and third-party sandboxes (payment test modes, email sandboxes, partner APIs). Contention and quota exhaustion cause failures that look like code bugs, burning agent runs and engineer time.
**First to feel it:** Head of Platform / DevEx lead at a 100–1,000 engineer company.
**Public decoy:** sandboxes and devboxes (E2B, Daytona), CI speed (Depot, Blacksmith).

### H6. Customer-facing teams can't absorb the shipping rate
**Failure:** product changes ship faster than support, docs, customer success and solutions engineers can learn them. Ticket volume from "unannounced" behavior changes rises, docs drift, and enterprise customers complain about surprise changes.
**First to feel it:** VP Engineering together with Head of Support / Head of CS at B2B SaaS shipping daily with agents.
**Public decoy:** release-notes generators, docs AI (Mintlify).

### H7. Decisions live in agent sessions and disappear
**Failure:** design decisions are now made inside agent chat sessions and never recorded. Six months later nobody can answer "why does it work this way?", and new hires (or new agents) repeat old mistakes.
**First to feel it:** CTO / principal engineers at companies 2+ years into heavy agent use.
**Public decoy:** company knowledge tools (Glean, Unblocked), codebase wikis (DeepWiki).

### H8. Agent configuration became a platform team's full-time job
**Failure:** platform teams hand-maintain per-team agent setups across hundreds of repos: instructions files, skills, tool allowlists, credentials, model choices, guardrails. It is now a growing, unowned ops burden with drift and breakage.
**First to feel it:** Head of Platform / DevEx / AI enablement lead at 200–2,000 engineer companies.
**Public decoy:** skills registries (Tessl, JFrog), MCP gateways (Runlayer).

### H9. Production data requests for agent debugging
**Failure:** to reproduce bugs, agents (and engineers using agents) need realistic production data. Data-access requests and manual sanitization grow; security and data teams become a bottleneck, or worse, people bypass them.
**First to feel it:** Head of Data Platform / security engineering lead at B2B SaaS with customer data.
**Public decoy:** test data management (Tonic), DB branching (Neon).

### H10. The AppSec queue for sensitive code paths
**Failure:** AppSec teams manually review every agent change touching auth, billing, permissions and data access. The queue can't scale, so companies quietly ban agents from the most valuable repos, capping AI adoption exactly where it matters.
**First to feel it:** Head of AppSec / CISO / VP Engineering at AI-native B2B software companies (non-bank).
**Public decoy:** AI SAST/code security (Snyk, Semgrep, Corridor, Apiiro).

---

## Part 2. Interview questions per hypothesis (non-leading)

Rules: never name the hypothesis, never pitch, never ask "would you buy". Ask for the last specific instance, numbers, and who did the work.

**H1. Supervision at AI app companies**
1. Walk me through what happens between signing a new customer and their agent running unattended. Who is involved, and for how long?
2. How has the number of people supporting live customer deployments changed in the last 6 months compared with the number of customers?
3. What does your team manually review or correct in customers' agent behavior each week?
4. What internal tools have you built to watch, correct or escalate customer agents?
5. If gross margin is below where you want it, where does the gap come from?

**H2. Agent output triage**
1. What share of your PRs are started by agents today, and how has that changed since spring?
2. What happens to agent-created PRs that don't get merged? Who decides?
3. When two efforts collide (duplicate or conflicting changes), how do you find out?
4. What have you built internally to organize or limit background agent work?
5. Where did the time saved on coding actually go?

**H3. Incidents in agent-written code**
1. Tell me about the last significant incident. How did you find someone who understood the code involved?
2. Has time-to-mitigate changed since agents started writing more of your code? Do you measure it?
3. How do postmortems assign ownership when the change was agent-authored?
4. What did you change in on-call or review because of agent code?
5. What part of incident response still needs a specific human who knows the system?

**H4. Spec bottleneck**
1. How has the way your senior engineers spend a week changed in the last 6 months?
2. Who writes the task descriptions agents work from? How long does a good one take?
3. When agent output misses the intent, how do you catch it and who fixes it?
4. Which roles feel more overloaded than a year ago, and which less?
5. What have you tried to make intent clearer to agents (templates, tools, process)?

**H5. Environment contention**
1. What share of agent test runs fail for reasons unrelated to the code change? How do you know?
2. Which shared resources (staging, databases, third-party sandboxes) are hardest to share among parallel agents?
3. Have you hit quota or rate limits on test environments of external services because of agents?
4. What have you built to isolate or schedule agent environments?
5. How much engineer time goes into "it's the environment, not the code" investigations each week?

**H6. Customer-facing absorption**
1. How often does a customer find out about a product change before your support team does?
2. Has ticket volume tied to recent changes moved since you started shipping with agents?
3. How do docs, support and solutions engineers learn what changed each week?
4. What have enterprise customers said about the rate of change?
5. Who owns making sure customer-facing teams know what shipped?

**H7. Lost decisions**
1. When someone asks "why does this work this way?", how do they find the answer today?
2. Where are design decisions recorded now that much design happens with agents?
3. Tell me about a recent case where a past decision was unknown and it cost you.
4. What do new engineers (or new agents) get wrong most often in their first month?
5. Have you tried to capture agent session reasoning? What happened?

**H8. Agent configuration ops**
1. How many repos/teams have their own agent setup (instructions, skills, tools, credentials)?
2. Who maintains those setups, and how much of their week does it take?
3. What broke last time a model, tool or policy changed across teams?
4. What internal tooling have you built to manage agent configuration?
5. What would happen if the person maintaining this left?

**H9. Production data for agent debugging**
1. How do engineers and agents get realistic data to reproduce a production bug?
2. How many data-access requests or sanitization tasks per week? Who handles them?
3. Has this changed since agents started debugging?
4. What shortcuts do you suspect people take?
5. What have you built to make safe data available?

**H10. AppSec queue**
1. Which code areas are agents not allowed to change, formally or informally? Why?
2. How many changes per week does AppSec review manually, and how has that changed?
3. Tell me about the last agent change in a sensitive area that worried you.
4. What did you build or change in your process because of agent-authored code?
5. If review capacity doubled tomorrow, where would you let agents work that you don't today?

---

## Part 3. Strong and kill signals (apply to every hypothesis)

**Strong signal (count per interview; validation needs ≥3 of these from ≥5 independent companies, described in different words):**
- "We built this internally" / names an internal tool, script or bot.
- "We assigned N people / N engineers to this" or "we hired for this".
- A number: hours per week, $ per month, % of runs, MTTR change, margin points.
- "We can't put more agents into [area] until we solve this."
- "This got worse in the last 6 months" with a specific trigger.
- Unprompted: the interviewee raises the problem before you reach that question.
- Asks for a follow-up or offers data/screenshares.

**Kill signal (any two in ≥3 interviews kills the hypothesis):**
- "We use [vendor] and it handles it" (and they're satisfied).
- "It's annoying but small" / no number, no owner, no internal tool.
- Pain exists only in theory ("I could imagine...").
- Only the interviewee's team cares; no budget owner above them.
- The pain is solved by a process tweak they already made.

---

## Part 4. Ranking

Scores 1–5 (5 = best). Hidden = likelihood the pain is invisible in public research.

| # | Hypothesis | Hidden | Urgency | Budget | Reach | Pilot speed | Category size | Total |
|---|---|---|---|---|---|---|---|---|
| H1 | Supervision scales linearly at AI app companies | 5 | 5 | 5 | 4 | 4 | 5 | **28** |
| H2 | Agent output nobody triages | 4 | 4 | 3 | 5 | 5 | 4 | **25** |
| H3 | Incidents in code no human understands | 4 | 5 | 4 | 4 | 3 | 4 | **24** |
| H10 | AppSec queue for sensitive paths | 3 | 5 | 4 | 4 | 3 | 4 | 23 |
| H8 | Agent config became a platform job | 4 | 3 | 3 | 5 | 4 | 3 | 22 |
| H6 | Customer-facing teams can't absorb shipping | 4 | 3 | 3 | 4 | 4 | 3 | 21 |
| H4 | Spec writer is the bottleneck | 4 | 4 | 2 | 5 | 2 | 4 | 21 |
| H5 | Shared environments under parallel agents | 3 | 3 | 3 | 5 | 4 | 3 | 21 |
| H9 | Production data for agent debugging | 3 | 3 | 3 | 4 | 3 | 3 | 19 |
| H7 | Decisions disappear in agent sessions | 4 | 2 | 2 | 4 | 2 | 4 | 18 |

**Why H1 ranks first:** margins are never published, so public research cannot see it; the buyer is the CEO/CTO with P&L pain; round 2 found the largest new AI budget line is people deploying and babysitting agents (FDE postings up 8x), and round 4 found vendors build deployment tools in-house — but nobody looked at the *ongoing* supervision cost after go-live.

---

## Part 5. Outreach list specifications

### H1. Supervision at AI app companies
- **Role:** CEO, CTO, VP Operations, Head of Customer Engineering / Deployments.
- **Company type:** AI-native B2B app companies selling agents that act for customers (support, voice, sales, legal ops, finance ops, IT ops, vertical agents).
- **Size:** Series A–C, 30–400 employees, 20–300 paying customers.
- **Technical profile:** production agents running for many customers; titles like "AI operations", "deployment strategist", "forward deployed engineer", "agent ops" in their team.
- **Trigger signals:** job posts for FDE/AI ops/deployment roles in the last 90 days; recent round with "enterprise expansion"; outcome-based pricing; customer logos growing faster than headcount in product/eng.
- **Where:** YC directories (2023–2026 batches), a16z/Sequoia/Conviction portfolios, LinkedIn job searches for "forward deployed engineer" + "AI agent".

### H2. Agent output triage
- **Role:** VP Engineering, Director of Engineering Productivity / DevEx, staff engineer owning developer tooling.
- **Company type:** B2B software companies and AI-native startups with heavy coding-agent use.
- **Size:** 50–500 engineers.
- **Technical profile:** Claude Code / Codex / Cursor background agents in daily use; internal "background agent" platform or Slack-triggered agents; GitHub-based workflow.
- **Trigger signals:** engineering blog posts about agent adoption; job posts for "AI developer productivity"; public statements like "X% of our PRs are written by agents".

### H3. Incidents in agent-written code
- **Role:** Head of SRE / Reliability, VP Engineering, incident commanders, staff SREs.
- **Company type:** B2B SaaS with customer-facing SLAs.
- **Size:** 100–1,000 engineers, on-call rotations.
- **Technical profile:** PagerDuty/incident.io/FireHydrant in use; >30% agent-authored changes.
- **Trigger signals:** public status page incidents in the last 90 days; SRE hiring; blog posts on AI-assisted development at scale.

---

## Part 6. Ten-interview sprints for the top 3

Common mechanics for each sprint:
- **Who:** 10 interviews from the outreach spec, max 2 from the same company, at least 6 companies.
- **Duration:** 30 minutes, recorded with consent; notes in the shared tracker (Part 7).
- **Order:** open with "what changed in the last 6 months" before any hypothesis-specific question; ask the specific questions only if the interviewee hasn't already raised them.
- **Never:** describe a product, name the hypothesis, or ask about willingness to pay before the last 3 minutes.

### Sprint 1: H1 Supervision at AI app companies

**Outreach message (CEO/CTO):**
> Subject: The humans behind autonomous agents
>
> I'm researching how AI app companies run customer deployments after go-live: who watches, corrects and escalates for each customer's agent, and how that scales. I'm not selling anything. 30 minutes comparing notes? I'll share anonymized findings from other agent companies.

**Questions (in order):**
1. What changed most in how you operate customer deployments in the last 6 months?
2. Walk me through the last customer you onboarded, from signature to the agent running unattended. Who was involved and for how long?
3. After go-live, what do people on your team still do for that customer each week?
4. How has the number of people in deployment/ops roles changed relative to customers this year?
5. What have you built internally to monitor, correct or escalate customer agents?
6. Where do humans still have to be in the loop, and why can't the agent do it yet?
7. What are you afraid to automate in customer deployments?
8. If you could hand one part of running deployments to someone else, which part?
9. (Last 3 minutes) What does this cost you today, roughly, in people or margin?

**Validation:** ≥5 of 10 companies report supervision headcount growing with customers AND ≥3 have built internal tooling for it AND ≥3 give a number (FTEs per customer, margin points, hours per customer per week) — in different words.
**Kill:** most say supervision drops sharply after 30–60 days per customer; or they use a vendor platform (their agent framework) that already handles it; or headcount growth is attributed to sales, not supervision.
**Prototype only after validation:** an "agent operations console" spanning customers: anomaly detection on customer-agent behavior, correction queue with learned fixes, and a cost-per-customer-supervised metric — first built on one design partner's logs.

### Sprint 2: H2 Agent output triage

**Outreach message (VP Eng / productivity lead):**
> Subject: Where did the saved coding time go?
>
> I'm talking to engineering leaders about what happened after coding agents took over a large share of PRs: what got faster, what got harder, and what nobody owns yet. Research only. 30 minutes? I'll share what other teams told me.

**Questions:**
1. What changed in how your team works in the last 6 months?
2. Roughly what share of PRs are agent-started now? How did that change?
3. What happens to agent PRs that don't get merged? Who decides, and how fast?
4. Tell me about the last time two efforts collided or duplicated each other.
5. What internal tools, bots or rules have you created to organize agent work?
6. Where did the time saved on writing code actually go?
7. What work is growing faster than your headcount?
8. What do you review manually every day that you didn't a year ago?
9. (Last 3 minutes) How many people-hours a week go into handling agent output that never ships?

**Validation:** ≥5 companies describe an unowned growing pile of agent output (stale PRs, rework, duplication) AND ≥3 built internal bots/scripts or assigned people AND ≥3 give a number.
**Kill:** most say merge rates are high and existing review/merge tools handle it; or the pile is small and self-cleaning.
**Prototype only after validation:** an agent work ledger: every agent task linked to its intent, outcome and cost; duplicate and conflict detection; automatic triage of stale work. Built first against GitHub + one agent platform at a design partner.

### Sprint 3: H3 Incidents in agent-written code

**Outreach message (SRE / VP Eng):**
> Subject: On-call when agents wrote the code
>
> I'm researching how incident response changes when agents author a large share of production changes: finding the right person, postmortems, ownership. Research only, no pitch. 30 minutes? Happy to share anonymized patterns from other teams.

**Questions:**
1. What changed in incident response in the last 6 months?
2. Tell me about your last significant incident. How did you find someone who understood the code involved?
3. Do you track time-to-mitigate? Has it moved since agent-authored changes increased?
4. How do postmortems handle ownership for agent-authored changes?
5. What have you changed or built in on-call, review or deploys because of agent code?
6. Where does incident response still require a specific human who knows the system?
7. What are you afraid to let agents change in production?
8. What unexpectedly became a bottleneck in reliability work this year?
9. (Last 3 minutes) What did your last bad incident cost in time, credits or customer trust?

**Validation:** ≥5 companies describe slower diagnosis or ownership gaps tied to agent-authored code AND ≥3 changed process or built tooling AND ≥2 show MTTR or incident-cost numbers.
**Kill:** MTTR flat or improving; AI SRE tools (Resolve, Traversal, incident.io AI) cited as solving it; or no attribution to agent code.
**Prototype only after validation:** change-provenance for incidents: for any failing service, which recent changes were agent-authored, with the original intent, session reasoning and the humans who approved, surfaced in the incident channel.

---

## Part 7. Operating the machine

**Weekly cadence:**
- Mon: build 40 contacts per active sprint; send 25 messages.
- Tue–Thu: run 8–12 interviews.
- Fri: synthesis.

**Tracker columns:** company, role, size, % agent-authored work, hypothesis, date, unprompted mentions, strong signals (list), kill signals (list), numbers quoted, internal tools named, quote in their own words, follow-up offered (Y/N).

**Synthesis rule ("five CTOs, different words"):** a hypothesis advances only when ≥5 companies describe the same underlying failure in their own words, with ≥3 naming internal tooling or assigned people. Cluster quotes by underlying failure, not by our hypothesis label; often the real pain is adjacent to the hypothesis. If a new, unplanned pain appears in ≥3 interviews, add it as H11 and test it in the next sprint.

**Advancing:** only a validated hypothesis returns to competitive research (using the existing corpus in research/) and product design. Then run the round-20-style 14-day paid-pilot test.

**Reuse:** the round-20 outcome-B finalist (counter-signed records for agent-to-agent deals) has its own discovery kit in round20/DISCOVERY_KIT.md and can run in parallel with a supplier-side audience.
