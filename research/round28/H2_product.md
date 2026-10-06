# Round 28 — H2 (agent output nobody triages): first-principles product thesis

Author: first-principles product thinker. Date: 2026-10-06.
Method: research/round28/BRIEF.md. 22 web searches; the shared per-turn search limit ran out before my cap of 30. WebFetch was not used. Facts come from search-result snippets. **[UNVERIFIED]** marks claims I could not confirm in a snippet. I did not make up any URLs.

---

## 0. TL;DR

- **The surface pain is real but already owned.** Each layer of "triage the agent pile" now ships inside a platform:
  - **Task inbox and steering:** GitHub Agent HQ / mission control.
  - **Intent → agent session:** Linear Agent coding sessions (Jun 2026). Linear says it resolves about 30% of its own incoming bug reports this way.
  - **Spec → parallel agents:** Augment Intent.
  - **Stale-PR cleanup:** a Devin automation template.
  - **Intent and reasoning capture:** Entire Checkpoints ($60M seed).
  - **Cost per merged PR:** Jellyfish, Larridin, Vantage, Unblocked, Warp.
  - **Pre-write claim/lock coordination:** OSS patterns (agent-coord, grite, "claim plane" write-ups).
- **2028-29 extrapolation.** With 20-100 agents per engineer, most agent work is speculative and thrown away. The unit of work moves from "PR" to **intent → N attempts → 0-1 survivors**. Engineering spend moves from payroll to compute.
- **Second/third-order consequence nobody is solving end-to-end:** that shift is an **accounting problem**.
  - Today's finance systems treat engineering cost as headcount × time allocation.
  - When the main cost is token/compute spend, and most of it goes on discarded attempts, finance needs an attempt-level ledger. Three uses:
    - **(a) Capitalize the winners:** ASU 2025-06 internal-use software rules take effect for fiscal years after Dec 15, 2027.
    - **(b) Claim R&D credit on the experimentation:** under Section 41, discarded attempts are the best contemporaneous evidence of a "process of experimentation".
    - **(c) Measure cost per surviving outcome**, and eventually settle outcome-priced vendor contracts.
- **Thesis: "The cost ledger for speculative engineering."** It starts as audit-grade substantiation of AI compute for R&D credits and capitalization, and expands into the system of record for engineering work units and budgets.
- **Verdict: KILL as an A. Weak B.** Average **5.9**. It is the most original framing I found for H2, and it has a real CFO dollar, but Jellyfish already sells "AI Token Cost Management" and "Software Capitalization", and Neo.Tax/Boast already ingest GitHub/Jira for R&D credits. Either is one feature away from the wedge.

---

## 1. Pushing H2 to 2028-2029

| Today (Oct 2026) | 2028-29 extreme state |
|---|---|
| Agent PRs merge at 32.7% vs 84.4% for humans (LinearB 2026, cited in round 3) | Engineers launch work as **portfolios**: 3-10 attempts per intent across models/vendors, and expect 1 or 0 survivors. Discard rate above 80% is the design, not a failure |
| Nearly half of PRs at top AI adopters are opened by agents (Jellyfish) | Most PRs are agent-opened. The scarce resources are human judgment, integration slots and CI |
| Median token spend per user went from $5 to $81/month in 10 months; P99 $2,452 (Jellyfish H1 2026) | Compute becomes a large share of R&D cost at AI-native companies. Wage share of R&D falls |
| "Cost per merged PR" emerging as a KPI (Unblocked, Larridin, Warp blogs) | "Cost per surviving outcome" becomes a board metric. Finance asks why 80% of compute bought nothing |

### Second-order consequences
1. **Unit of work = intent, not PR.** A PR is one attempt. The thing being managed is the intent ("make checkout retry idempotent"), its attempts, their costs, and which one survived. Linear, GitHub and Entire are each grabbing part of this object.
2. **Duplicate/conflicting work becomes a concurrency-control problem** (claim before write). Platform-native, so already being absorbed.
3. **Planning becomes capital allocation.** The backlog turns into a priced portfolio, where you set a budget per intent and a kill rule. Today this lives inside agent vendors' best-of-N logic, plus academic routing work (CodeRescue, budget-aware best-of-N, AI21).
4. **Measurement becomes unit economics.** Already crowded (Jellyfish, Faros, DX/Atlassian, Larridin, Vantage).

### Third-order consequence (the one picked)
5. **Accounting breaks.** Finance's model of R&D is "people × % time on project". Three rules now hit the new cost structure:
   - **R&D credit (§41):** QREs can include "amounts paid for the right to use computers in the conduct of qualified research", and practitioners now apply this to API/token spend (Aprio, Source Advisors, Strike Tax). Bloomberg Tax: "there is no IRS guidance on AI in this context". Taxpayers should keep records of how the tool was used, including the underlying queries. Usage tied to a project is easier to defend than a general subscription.
   - **Capitalization (ASC 350-40 as amended by ASU 2025-06):** the project-stage model is replaced by "management authorized + probable to complete". Effective for fiscal years ending after Dec 15, 2027 (snippet wording). Deloitte DART has a publication on accounting for AI costs in internal-use software development. Broadcom ValueOps describes "consumption-based timesheets: ingesting token files and treating token units like labor hours" and "tagging tokens with project/resource IDs for an audit trail". The example given: a company spending $50M/yr on development tokens gets a large adjusted-EBITDA effect from capitalizing it.
   - **The speculative twist nobody frames:** winners and losers get opposite treatment. Merged attempts on authorized projects may be **capitalizable**. Discarded attempts are **expensed**, but they are the strongest **§41 experimentation evidence**. Getting both right needs a per-attempt link: token → attempt → intent → business component → outcome. That record does not exist anywhere today: gateways see tokens, Git sees commits, Jira sees tickets, and agent vendors keep transcripts briefly.
   - **Evidence destruction:** agent session transcripts are short-lived or local by default **[UNVERIFIED, could not search]**. So the contemporaneous evidence for tax year 2026 claims is being lost now.
   - **Form 6765 Section G** (business-component QRE detail) is understood to become mandatory around tax year 2026 **[UNVERIFIED, search budget exhausted]**. If so, it forces per-component allocation of compute QREs.

**Does this create a new infrastructure category?** Possibly: **"cost accounting for machine labor in R&D"**. This is the engineering equivalent of what time-tracking + payroll + project accounting did for human R&D. If agents are the labor, someone has to keep the labor ledger. That is the most venture-shaped version of "work ledger / intent graph", because finance pays for ledgers and engineers do not.

---

## 2. Finalist-format thesis: **Speculative Engineering Ledger** (working name "Tally")

**One-line problem:** By 2028 most of a software company's R&D cost is agent compute, and most of it goes on attempts that are thrown away. Finance cannot tell which dollars built capitalizable assets, which qualify for R&D credits, and what each surviving outcome actually cost, because no system links tokens to attempts to intents to outcomes.

**Why now:**
- Token spend is growing 16x per user in ten months (Jellyfish).
- Agents open about half of PRs at top adopters.
- Agent merge rate is about 33%, so roughly two-thirds of attempt spend is discarded.
- ASU 2025-06 takes effect for FY2028 at most calendar-year companies; early adoption is allowed.
- No IRS guidance on AI QREs exists, and Big-4/boutique advisors are publishing "keep precise records" advice (Bloomberg Tax, Aprio, Leyton, Forvis Mazars, Deloitte, EisnerAmper, Crowe CPE events in 2026).
- Transcripts, the evidence, are being lost now [UNVERIFIED retention specifics].

**Exact buyer:** Corporate Controller / VP Finance (budget owner for the R&D credit study and capitalization policy), with the Head of Tax as co-signer. VP Engineering / DevEx lead is the technical sponsor who installs the collectors.

**Exact ICP:**
- US software companies with 150-2,000 engineers.
- At least $3M/yr of coding-agent spend (Claude Code/Codex/Cursor/Devin, API or enterprise plans, plus internal background-agent platforms).
- Already claim the §41 credit and capitalize internal-use or SaaS development.
- Pre-IPO or public, so the EBITDA and audit trail matter.
- Examples of the profile: the round-8 list of companies running internal agent platforms (Ramp, DoorDash, Monzo-like (UK R&D relief analogue), Coinbase-scale).

**Current workaround:**
- R&D credit study by a boutique or Big-4 firm, or Neo.Tax/Boast, using payroll + Jira/GitHub. AI spend is either excluded (money left on the table) or allocated by a top-down % (audit risk).
- Capitalization by Jellyfish/spreadsheet time allocation that treats AI spend as a subscription opex line.
- Engineering cost per outcome from Jellyfish/Larridin dashboards, not reconciled to the GL.

**Why incumbents cannot easily own it (honest):**
- *Agent vendors* (Anthropic, OpenAI, Cursor, GitHub) see only their own sessions. A tax/audit record needs to be cross-vendor and neutral, and vendors avoid taking positions on customers' tax treatment.
- *Jellyfish/DX/Faros* attribute at the PR/ticket level using inferred signals ("without tagging"). That is fine for dashboards but weak as audit-grade evidence at the attempt level, and they have no transcript evidence store.
- *Neo.Tax/Boast/Big-4* are study-once-a-year businesses without real-time collectors in the agent runtime.
- *Entire* captures transcripts but is a developer platform. Finance is not its buyer.
- **Weakness:** none of these structural reasons is strong. Jellyfish already lists "AI Token Cost Management" and "Software Capitalization" as products. Neo.Tax (distributed via Thomson Reuters) only needs to add a gateway/billing-export connector.

**30-day MVP:**
1. Collectors: an LLM-gateway/billing-export ingester (Anthropic/OpenAI/Cursor admin APIs, LiteLLM/Portkey logs), a GitHub app (branches, PRs, merge/revert/survival at 30 days), a Linear/Jira connector, and opt-in transcript archiving through agent hooks (Claude Code/Codex hooks, Entire Checkpoints import).
2. Attempt graph: cluster sessions into attempts and attempts into intents (ticket ID, branch, semantic similarity), with outcome labels: merged-survived / merged-reverted / discarded.
3. Two finance outputs:
   - **(a) §41 compute-QRE workpaper**: per business component, the attempts, the uncertainty statement extracted from the prompt or spec, and the alternatives tried (discarded attempts) with cost.
   - **(b) ASU 2025-06 capitalization schedule** for compute on authorized projects, plus an expense schedule for speculative attempts.
4. An engineering view: cost per surviving outcome by team, vendor and task type.

**Pilot design (60 days, 3 companies):**
- Back-fill the last 6-9 months of billing exports + Git history.
- Pass if:
  - At least $250K of incremental defensible compute QREs per company (about $16-25K+ credit value at a ~6.5-10% effective rate), **or**
  - At least $1M of compute reclassified as capitalizable.
- The tax advisor or auditor must accept the workpaper format without rework.
- The engineering lead must use the cost-per-surviving-outcome report to change one budget or vendor decision.

**Pricing hypothesis:**
- Platform fee of $30-120K/yr, scaled by agent spend under management (about 1-2% of AI dev spend).
- Optional success fee on incremental credit (10-15%, below the 20-30% boutique norm).
- Later, a per-seat or per-agent charge for budget and policy controls.

**Expansion path:**
1. Finance substantiation (credit + capitalization).
2. **Budgets per intent and kill rules**: speculative execution policy (max attempts, model mix, auto-discard thresholds), enforced through the gateway. Planning becomes capital allocation.
3. **Chargeback/showback** of agent compute to products and P&Ls.
4. **Outcome-priced vendor settlement**: the neutral meter of "merged and survived N days" when coding vendors move to per-outcome pricing.
5. The system of record for machine labor across all R&D agents (not just coding), and later non-R&D agent work for opex allocation.

**Moat:**
- Audit-acceptance precedent: once an auditor/IRS exam accepts the ledger, switching is risky.
- Historical evidence archive: the transcripts are irreplaceable after vendor retention expires.
- Cross-company benchmarks for cost per surviving outcome by task type, which feed the budget-policy layer.
- **Weak spots:** precedent takes years to build, and benchmarks are something Jellyfish already has (20M+ PRs).

**Why it could become a $10B+ company:**
- If agents become the main labor in R&D, global R&D cost accounting moves from payroll systems to compute ledgers.
- US business R&D is about $700B+/yr, and the §41 credit is tens of billions/yr [order-of-magnitude, UNVERIFIED].
- The company that becomes "Workday/ADP for machine labor": records machine work, assigns it to assets and credits, and settles outcome contracts. That sits in the money path of every AI-native company.
- **Honest view:** the near-term wedge market (credit-study fees + capitalization software for agent spend) is probably $0.3-1B. The $10B path depends on step 4-5 expansion and on agent compute actually becoming a large share of R&D (plausible by 2029 at AI-native companies, but not proven).

**Direct competitors and adjacent threats:**
- **Jellyfish:** AI Token Cost Management, Software Capitalization, DevFinOps, AI Impact. The closest threat, and it already has finance buyers.
- **Neo.Tax:** AI-agent R&D credit studies from Jira/GitHub/payroll; Thomson Reuters partnership; GV-backed.
- **Boast.ai:** GitHub/Jira ingestion.
- **Big-4 / Aprio / Leyton / Source Advisors:** service-led.
- **Broadcom ValueOps/Clarity:** consumption-based timesheets for tokens.
- **Entire:** intent/transcript capture with commits; could add a finance export.
- **Vantage, Larridin, Faros, DX (Atlassian):** cost and impact analytics.
- **LLM gateways** (LiteLLM, Portkey, Maxim): token tagging by project.
- **GitHub/Linear:** own the intent object.
- **Agent vendors:** usage APIs with cost by project.

**One sentence to send a CFO:** "About two-thirds of your coding-agent spend goes on attempts that are thrown away. We turn that spend into documented R&D-credit evidence and the merged third into a capitalizable asset under ASU 2025-06, and you see the real cost of every shipped change. Give us 60 days and your billing exports and we'll show you the dollar number."

**Hard kill criteria:**
1. In the pilot, the tax advisor or auditor rejects attempt-level compute QREs, or says top-down % allocation is already accepted with no exam risk (makes the product unnecessary).
2. Incremental credit + capitalization value is under $100K/company/yr at $3M of agent spend.
3. Jellyfish or Neo.Tax ships attempt-level compute allocation with transcript evidence before we have 5 paying customers.
4. Agent vendors' native usage exports with project tags plus a Jellyfish connector meet auditors' needs (likely by 2027).
5. Finance won't buy before ASU 2025-06 adoption (late 2027), which leaves a 12-month dead zone.

### Scores (honest)

| Category | Score | Rationale |
|---|---|---|
| Pain | 6 | Real dollars, but felt as "money left on table", not as an emergency. Engineering's triage pain is not what this solves |
| Urgency | 5 | ASU 2025-06 is FY2028. No IRS guidance means no forcing event. Section G timing unverified |
| ROI clarity | 8 | Credit dollars and EBITDA reclassification are directly measurable |
| Customer accessibility | 6 | Controllers are reachable, but credit studies are sold through advisors with entrenched relationships |
| Pilot speed | 7 | Back-fill from billing exports + Git history works in weeks. Transcript evidence is limited for past periods |
| Market size | 5 | Near-term wedge is under $1B. $10B depends on unproven expansion |
| Expansion | 7 | Budgets/policy → chargeback → outcome settlement is a coherent path |
| Venture potential | 6 | A "Workday for machine labor" story is fundable. The wedge looks like tax-tech, which VCs discount |
| Defensibility | 5 | Audit precedent and evidence archive are slow to build. Jellyfish has benchmarks and finance buyers |
| Why now | 7 | Token growth, half of PRs from agents, ASU 2025-06, and no IRS guidance all line up |
| Competition position | 3 | Jellyfish lists both features. Neo.Tax/Boast one connector away |
| **Average** | **5.9** | Fails A (needs ≥8.5, none <7) |

**Classification: KILL as A. Weak B (estimated 10-15% chance a test passes).** The B case: "machine labor cost accounting" is too early for public evidence, because finance has not yet seen compute become a large share of R&D. If agent compute at AI-native companies reaches 20-40% of R&D cost by 2028, a ledger becomes required infrastructure, and incumbents that attribute by inference ("without tagging") may not be audit-grade.

Precise 14-day test (artifact-based, no interviews):
- Take billing exports + Git history from 2 design partners.
- Produce the §41 compute workpaper.
- Have their existing tax advisor score it.
- Pass = at least $250K incremental defensible QREs per company, plus the advisor states they would rely on it.

---

## 3. Other H2 deeper layers considered and killed

| Candidate | Why killed |
|---|---|
| Intent registry / "work ledger" for engineers (semantic dedup of intents across teams) | The intent object is owned by Linear (Agent + coding sessions), GitHub Agent HQ, Augment Intent and Entire. Engineers won't pay for a separate ledger |
| Pre-write concurrency control ("claim plane": agents lease files/symbols/APIs before writing) | Real at monorepo scale (research shows duplicate-work rates of 78% with no coordination, 64% with locks only, 0% with locks + shared state), but it is a coordination primitive that GitHub, Cursor, Linear or the merge-queue vendors add as a feature. OSS already exists. Also falls under "generic orchestration" |
| Speculative execution allocator (budget per intent, best-of-N, early kill across vendors) | Agent vendors do this internally, and a cross-vendor allocator is orchestration. Academic routing methods are public. It survives only as expansion step 2 of the ledger, where finance budgets give it authority |
| Agent output inbox / triage queue | Surface pain. GitHub mission control, Linear, Cursor agents view, Devin stale-PR cleanup. Also round-9 human decision layer kill |
| Cost per merged outcome dashboard | Jellyfish, Larridin, Vantage, Unblocked, Faros, DX |
| "Negative-results registry" (what agents tried and failed, so others don't repeat it) | Context management (banned) + Entire Checkpoints |

---

## Sources (from search snippets)
- Claude Code issue on dismissing abandoned agent sessions: https://claudeissues.com/issue/66202-feature-let-me-mark-an-agent-session-as-completed-dismiss-it-from-the-agents-vie
- GitHub mission control: https://github.blog/ai-and-ml/github-copilot/how-to-orchestrate-agents-using-mission-control/ ; Agent HQ: https://visualstudiomagazine.com/articles/2025/10/28/github-introduces-agent-hq-to-orchestrate-any-agent-any-way-you-work.aspx
- Linear coding sessions: https://linear.app/changelog/2026-06-11-coding-sessions
- Augment Intent: https://www.augmentcode.com/product/intent
- Entire $60M seed: https://techcrunch.com/2026/02/10/former-github-ceo-raises-record-60m-dev-tool-seed-round-at-300m-valuation/
- Cost per merged PR: https://getunblocked.com/blog/cost-per-merged-pr ; https://larridin.com/measurement-guide/agent-effectiveness/cost-per-outcome/ ; https://www.vantage.sh/blog/agentic-coding-efficiency ; https://www.warp.dev/articles/reduce-ai-coding-agent-costs
- Claim-plane coordination: https://codex.danielvaughan.com/2026/07/28/claim-plane-pre-write-admission-control-parallel-coding-agents-codex-cli-changeintent-scope-promotion/ ; https://codex.danielvaughan.com/2026/06/20/before-the-pull-request-multi-agent-coordination-codex-cli-grite-duplicate-work-prevention/
- Devin stale PR cleanup: https://docs.devin.ai/automation-templates/stale-pr-cleanup
- Jellyfish token benchmarks and products: https://jellyfish.co/state-of-ai-software-engineering/
- R&D credit and AI spend: https://news.bloombergtax.com/daily-tax-report/claiming-r-d-tax-breaks-for-ai-costs-requires-precise-records ; https://www.aprio.com/insights-events/ai-spend-and-the-rd-credit-what-qualifies-and-when-ins-article-rd/ ; https://sourceadvisors.com/blogs/rd/ai-token-and-cloud-computing-costs-as-qualified-rd-expenses/
- Capitalization: https://dart.deloitte.com/USDART/home/publications/deloitte/industry/technology/accounting-ai-costs-associated-internal-use-software-development ; https://valueops.broadcom.com/blog/accounting-best-practices-for-ai-use-in-software-development ; https://www.eisneramper.com/insights/technical-accounting-advisory/ai-development-cost-under-us-gaap-0726/
- Neo.Tax: https://tax.thomsonreuters.com/en/corporation-solutions/c/neotax
- Budget-aware routing research: https://arxiv.org/pdf/2608.22191 ; https://tldr.takara.ai/p/2607.19338
