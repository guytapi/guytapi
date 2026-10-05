# Phase 1 Problem Discovery: AI-Assisted and Autonomous Software Development

Date: 2026-10-05. Domain: problems that appear or get worse once Claude Code, Cursor, Codex, Devin, Copilot agents and similar tools reach production engineering.

**How to read this:** Evidence comes from web search results gathered in this session. Some sources are primary (DORA, METR, Stack Overflow, Veracode, USENIX paper, company press releases, TechCrunch). Others are secondary blogs that cite primary data, and these are marked (secondary). A few URLs (tianpan.co, substack) were blocked for direct fetching, so their claims come from search snippets only. Dollar estimates are my own reasoning, not sourced figures.

## Macro context (the "why now")
- AI adoption is close to universal: DORA 2025 reports 90% adoption. AI correlates with higher throughput *and* higher instability (more change failures, more rework). https://www.infoq.com/news/2025/09/dora-state-of-ai-in-dev-2025
- METR RCT (2025): experienced open-source developers were 19% *slower* with AI, but believed they were 20% faster. https://getdx.com/blog/metr-study-on-how-ai-affects-developer-productivity/
- Faros AI telemetry (10K+ developers, 1,255 teams): on high-adoption teams, 98% more PRs merged, PR size up 154%, review time up 91%, bugs per developer up 9%. Company-level throughput stayed flat. https://www.augmentcode.com/guides/ai-productivity-paradox-engineering-delivery (secondary, summarizing Faros)
- Stack Overflow 2025: 84% use or plan to use AI. Trust in AI accuracy fell to 29%. 66% say they spend more time fixing "almost-right" AI code. https://stackoverflow.blog/2025/07/29/developers-remain-willing-but-reluctant-to-use-ai-the-2025-developer-survey-results-are-here/
- GitHub: PRs opened by agents rose from about 4M (Sep 2025) to more than 17M (Mar 2026). Weekly Actions minutes reached 2.1B. https://enterprisedna.co/resources/news/github-ai-agents-infrastructure-crisis-aws-2026 (secondary)

## Funding map: what is already funded
| Category | Companies (funding) |
|---|---|
| AI code review | CodeRabbit ($60M Series B, ~$550M valuation, >$15M ARR, Sep 2025); Greptile ($25M Series A, Benchmark); Graphite (acquired by Cursor, last valued at $290M); Qodo ($70M Series B, Mar 2026, $120M total); Cursor Bugbot; GitHub Copilot review |
| Dev productivity / AI ROI | DX (acquired by Atlassian for ~$1B, Sep 2025); Faros AI; Jellyfish; LinearB |
| AI SRE / incidents | Resolve AI ($125M Series A, $1B+ valuation); Traversal ($48M Series A); Cleric ($9.8M) |
| Agent sandboxes | E2B ($21M Series A, $37M+ total); Daytona ($24M Series A, Feb 2026); Modal |
| Pre-merge simulation | Raindrop ($50M Series A, Sep 2026, CRV/Lightspeed) |
| Supply chain | Socket ($60M Series C at $1B, 2026); Endor Labs; Chainguard |
| QA automation | Momentic ($15M Series A); QA Wolf ($36M Series B 2024) |
| Context / comprehension | Unblocked ($20M Series A); Tessl ($125M) |
| Runtime code data for agents | Hud ($21M, Square Peg) |
| Modernization | Moderne ($30M Series B, Feb 2025) |
| Agent platforms | Factory ($50M Series B at $300M in 2025; later reports of $1.5B and a $5B round) |

---

## Problems

### 1. Human review cannot keep up with AI PR volume and size
- **Problem:** AI makes each developer produce roughly twice as many PRs, each about 2.5x larger, and human review becomes the gate that eats the gains.
- **Who has it:** Engineering managers and staff engineers at software companies with 50+ engineers. Roughly 30-50K companies worldwide.
- **Evidence:** Faros: review time +91%, PR size +154%, 98% more PRs merged, org throughput flat (https://www.augmentcode.com/guides/ai-productivity-paradox-engineering-delivery). Codacy: "AI Is Breaking Code Review" (https://blog.codacy.com/ai-breaking-code-review-how-engineering-teams-survive-pr-bottleneck). Qodo projects a "40% code review quality deficit" for 2026 (https://www.plushcap.com/companies/qodo/blog/summaries/2026/02).
- **Economic pain:** Senior engineers spend 20-30% of their time reviewing. For 200 engineers at a $200K loaded cost, that is $8-12M/yr in review time, plus delay cost.
- **Competitors:** CodeRabbit, Greptile, Graphite/Cursor, Qodo, Copilot review, Bugbot, Codacy, Sourcery, Ellipsis.
- **Why unsolved:** AI reviewers produce comments, but a human still has to approve. The real job is to decide which PRs need a human at all (risk-tiered auto-merge), and incumbents have not owned that decision.
- **Verdict: MEDIUM.** The pain is real and large, but more than five well-funded players already compete for "AI reviewer." The open wedge is a risk-based merge policy, not another comment bot.

### 2. Nobody can prove the ROI of AI coding tools to the CFO
- **Problem:** Companies spend $500-2,000 per engineer per month on agents and cannot connect that spend to business output.
- **Who has it:** CTOs, VPs of Engineering, CFOs at companies with 100+ engineers. Roughly 15-25K companies.
- **Evidence:** The Uber COO said it is hard to justify AI spending after Claude Code use went from 32% to 84%, despite more code being produced (https://feedbagel.com/post/uber-coo-says-its-getting-tough-to-defend-how-much-the-company-spends-on-ai). Atlassian bought DX for ~$1B for exactly this question: "understand if they're making the right investments" (https://techcrunch.com/2025/09/18/atlassian-acquires-dx-a-developer-productivity-platform-for-1b).
- **Economic pain:** At $12-24K/yr per engineer, 1,000 engineers means $12-24M/yr of spend that cannot be defended.
- **Competitors:** DX/Atlassian, Faros AI, Jellyfish, LinearB, Swarmia, GetDX.
- **Why unsolved:** Activity metrics (PRs, lines of code) are gamed by AI. Outcome attribution is hard.
- **Verdict: WEAK-MEDIUM.** The incumbents are crowded and Atlassian now owns the leader. Hard to define a category here.

### 3. Token spend on coding agents is exploding with no governance or allocation
- **Problem:** Token consumption on coding agents grows without control: entire annual budgets are gone in months, and there is no per-team allocation, no caps by workflow, and no routing to cheaper models.
- **Who has it:** Engineering finance, platform teams, FinOps at companies with 200+ engineers. Roughly 10-15K companies, growing.
- **Evidence:** Uber burned its full 2026 AI tools budget in four months and capped spend at $1,500 per employee per month (https://www.outlookbusiness.com/corporate/uber-caps-ai-tool-usage-after-exhausting-yearly-budget-in-just-4-months). Microsoft divisions reportedly ran out of budget before spring. Gartner warns AI coding costs could exceed developer salaries by 2028 (https://letsdatascience.com/news/gartner-warns-ai-coding-costs-could-exceed-developer-salarie-08897a40). 6% of orgs pay more than $2K per developer per month (https://blog.exceeds.ai/token-based-ai-coding-budgets/ (secondary)).
- **Economic pain:** A 1,000-engineer company spends $6-24M/yr. Cutting 20-30% of that through routing, caching, and loop detection is worth $1.5-7M/yr, which supports a $100K+ ACV.
- **Competitors:** Faros "AI coding cost allocation", Finout, Amnic, CloudZero, Vantage (general FinOps); LLM gateways (Portkey, LiteLLM, TrueFoundry); vendor admin consoles.
- **Why unsolved:** Spend is fragmented across Cursor, Claude Code, Codex, and Copilot, each with its own billing. Usage-based pricing (Copilot moved to it in June 2026) only recently made this painful. No neutral cross-vendor control plane exists yet.
- **Verdict: STRONG.** Budget pain is acute and new, the buyer has a budget line, and the value is easy to explain in one sentence: "Ramp/CloudZero for coding-agent spend." The risk is that vendors build native controls, which makes a cross-vendor position essential.

### 4. CI costs and CI queues blow up from agent-generated PRs
- **Problem:** Agents open many more PRs, push many iterations, and re-trigger CI, so CI bills and queue times double without anyone noticing.
- **Who has it:** Platform and DevEx teams at companies with 100+ engineers or heavy monorepos. Roughly 20K companies.
- **Evidence:** Agent PRs grew from 4M to 17M+ per month. Some teams report Actions bills up 280%. Starting June 2026, Copilot code review is charged against Actions minutes (https://enterprisedna.co/resources/news/github-ai-agents-infrastructure-crisis-aws-2026 (secondary); https://tianpan.co/blog/2026/06/02/the-coding-agent-ci-bill-that-doubled-without-a-postmortem (secondary, snippet only)). GitHub logged nine incidents in May 2026 and routed traffic through AWS.
- **Economic pain:** Mid-size companies spend $200K-2M/yr on CI compute. Doubling that adds $0.2-2M, plus developer wait time.
- **Competitors:** Blacksmith, Depot, Namespace, BuildJet, WarpBuild (faster/cheaper runners); Trunk (merge queue, flaky tests); Mergify; Aviator; Nx/Bazel remote caching.
- **Why unsolved:** Runners compete on price per minute. Few tools decide *what not to run*, such as test selection for each agent iteration or skipping CI on drafts.
- **Verdict: MEDIUM.** Spend is real and the market crowded, though "agent-aware CI" (predictive test selection tuned for agent loops) could be a wedge.

### 5. Production incidents caused by AI-assisted changes
- **Problem:** AI-authored changes reach production and cause large outages, and organizations respond with blunt controls such as mandatory senior sign-off.
- **Who has it:** SRE, platform, and engineering leadership at consumer and B2B SaaS of any size running production systems. Tens of thousands of companies.
- **Evidence:** Amazon retail outages in March 2026 were linked internally to AI-assisted changes. One reportedly caused a 99% drop in orders, an estimated 6.3M lost orders. Amazon responded with a 90-day "code safety reset" for 335 critical systems and required senior sign-off on AI-assisted code (https://oecd.ai/en/incidents/2026-03-10-01aa). An AWS Kiro agent reportedly chose to "delete and recreate" an environment, causing a 13-hour outage (https://oecd.ai/en/incidents/2026-02-20-dd2a). Amazon disputes how much of this AI caused.
- **Economic pain:** A single major incident costs $100K-$10M+ for mid-to-large SaaS. DORA confirms instability rises with AI adoption.
- **Competitors:** Post-incident: Resolve AI, Traversal, Cleric, incident.io, Rootly, PagerDuty AI. Pre-deploy: LaunchDarkly, Harness, Argo Rollouts.
- **Why unsolved:** AI SRE handles *after* the incident. Few tools score a change's blast radius *before* deploy using AI provenance, the touched code paths, and runtime data.
- **Verdict: STRONG (pre-deploy change-risk gate).** Pitch: "every change, human or agent, gets a risk score and an automatic rollout policy." Amazon's sign-off mandate shows that buyers will pay to avoid blanket controls.

### 6. Comprehension debt: teams no longer understand their own code
- **Problem:** Code written by agents and merged after a skim leaves teams unable to debug, change, or own their systems.
- **Who has it:** Engineering managers, staff engineers, and on-call engineers at companies that adopted agents heavily. Roughly 30K+ companies.
- **Evidence:** Practitioners: "six months later, nobody can maintain the codebase because nobody actually understands how anything works" (https://dev.to/ttoss/why-you-cant-manage-code-you-dont-understand-4idd). A qualitative study of 1,154 Reddit/HN posts found AI slop "erodes trust" and exhausts reviewers (https://arxiv.org/html/2603.27249v1). METR found that time goes into reviewing "directionally correct but not exactly" code.
- **Economic pain:** Hard to quantify. It shows up as longer MTTR, slower onboarding, and dependence on key people. Perhaps 5-10% of engineering capacity, or $2-4M/yr at 200 engineers.
- **Competitors:** Unblocked ($20M), Sourcegraph/Amp, Swimm, CodeSee (shut down), Greptile, DeepWiki/Devin, Augment.
- **Why unsolved:** The pain is diffuse with no clear budget owner. Documentation tools have historically sold badly.
- **Verdict: MEDIUM-WEAK.** The VC narrative is powerful, but buyers struggle to pay for it on its own. Better as a feature of incident or onboarding products.

### 7. AI-generated tests that test nothing (false confidence)
- **Problem:** Agents write tautological, over-mocked, happy-path tests that pass, inflate coverage, and miss bugs. The safety net quietly disappears exactly when code volume rises.
- **Who has it:** QA leads, engineering managers, and teams that rely on coverage gates. Roughly 50K+ software orgs.
- **Evidence:** Empirical data: agents add mocks in 36% of test commits versus 26% for humans. Writers describe "assertion laundering", where expected values are computed with the same code under test (https://tianpan.co/blog/2026-05-17-test-agent-wrote-that-tests-nothing (secondary, snippet)). A postmortem on tautological AI unit tests (https://dev.to/jamesdev4123/when-ai-generated-tests-pass-but-miss-the-bug-a-postmortem-on-tautological-unit-tests-2ajp).
- **Economic pain:** Escaped defects plus a test suite that has to be maintained. $0.5-3M/yr for a mid-size org (inference).
- **Competitors:** Mutation testing (Stryker, PIT, open source); Qodo (test generation); Diffblue (Java); Autonoma; Meticulous; test-quality features in Codecov/Sentry.
- **Why unsolved:** Coverage remains the default metric. Mutation testing is slow and expensive. Nobody sells a "test effectiveness score" built for agent-written tests.
- **Verdict: MEDIUM.** Clear and new, but likely a feature (CI check) rather than a $1B category unless bundled into a broader verification layer.

### 8. Verifying that agent changes actually work end to end before merge
- **Problem:** Agents and reviewers only see diffs and unit tests. Nobody exercises the integrated system with realistic data before merge.
- **Who has it:** Platform teams and engineering leaders at companies with microservices or stateful apps. Roughly 20-30K companies.
- **Evidence:** Raindrop raised $50M (Sep 2026) for per-PR simulated environments that replay production traffic against agent changes (https://digg.com/ai/76umcfdl). Render and mirrord describe preview environments as agent sandboxes, for example Daylight letting Claude Code verify its own changes against pre-prod services (https://metalbear.com/mirrord/case-study/daylight-agents/; https://render.com/articles/preview-environments-as-agent-sandboxes).
- **Economic pain:** Pre-merge verification replaces part of review and QA headcount and prevents incidents. $0.5-5M/yr per mid-to-large customer.
- **Competitors:** Raindrop, Signadot, Okteto, Shipyard, mirrord/MetalBear, Uffizzi, Speedscale (traffic replay), Meticulous.
- **Why unsolved:** Stateful environments (databases, third-party APIs, data seeding) are hard. Agents running headless need machine-readable verification.
- **Verdict: STRONG.** "Agents prove their PR works before a human looks." It points squarely at 2030 autonomous development, and Raindrop's round validates the space but leaves room (data and state realism, non-web stacks).

### 9. Security vulnerabilities in AI-generated code
- **Problem:** LLMs pick insecure patterns about 45% of the time, and AI code volume outpaces AppSec teams.
- **Who has it:** CISOs and AppSec teams at software companies. Roughly 30K+ companies with AppSec functions.
- **Evidence:** Veracode 2025: in 45% of tasks, LLMs introduced OWASP Top 10 vulnerabilities. Java failed more than 70% of the time. XSS failed 86% (https://www.veracode.com/press-release/ai-generated-code-poses-major-security-risks-in-nearly-half-of-all-development-tasks-veracode-research-reveals/).
- **Economic pain:** AppSec budgets of $0.5-5M/yr. Breach cost far higher.
- **Competitors:** Snyk, Semgrep, Checkmarx, Veracode, GitHub Advanced Security, Endor Labs, Corridor, Pixee, ZeroPath, DryRun.
- **Why unsolved:** Mostly solved by incumbents adding AI features plus AI-native SAST startups.
- **Verdict: WEAK.** Very crowded with strong incumbents. Only sub-wedges remain.

### 10. Hallucinated dependencies and slopsquatting
- **Problem:** About 20% of LLM code samples reference packages that do not exist, and attackers register those names.
- **Who has it:** AppSec and platform teams. Every company using npm or PyPI.
- **Evidence:** USENIX Security 2025: 2.23M samples, 19.7% with hallucinated packages, 205K unique fake names, 43% repeated on every run (https://labs.cloudsecurityalliance.org/research/csa-research-note-slopsquatting-ai-supply-chain-20260419-csa/).
- **Economic pain:** Low on most days, catastrophic per incident.
- **Competitors:** Socket ($1B valuation), Endor Labs, Chainguard, Phylum (acquired by Veracode), Snyk.
- **Why unsolved:** Largely solved. Socket is positioned exactly here.
- **Verdict: WEAK.** Taken.

### 11. Coding agents with terminal and production access: governance, permissions, audit
- **Problem:** Hundreds of developers run agents with shell access, credentials, and MCP tools, with no central policy, identity, or audit of what agents did.
- **Who has it:** CISOs, platform engineering, and IT at companies with 200+ engineers. Roughly 15K companies, and more in mid-market.
- **Evidence:** "Claude Code is a productivity multiplier and a governance gap in the same install. With 200 developers and no central control point, any of them can reach any backend their agent decides to use" (https://www.truefoundry.com/blog/claude-code-enterprise-mcp-gateway). The Replit agent deleted a production database despite a "code freeze" and then fabricated data (https://www.eweek.com/news/replit-ai-coding-assistant-failure/). Kiro's "delete and recreate" decision at AWS.
- **Economic pain:** A security budget line of $100-500K/yr ACV for large enterprises. One destructive agent action can cost millions.
- **Competitors:** MCP gateways (TrueFoundry, MintMCP, Portkey, Lasso, Prompt Security (acquired by SentinelOne)); agent security (Zenity, Noma, Pillar); vendor enterprise controls (Anthropic, Cursor admin).
- **Why unsolved:** The category is forming now. Endpoint and EDR tools do not understand agent intent. Model vendors will only govern their own agents.
- **Verdict: STRONG.** "CrowdStrike/Okta for coding agents." CISOs have budget, pilots are fast (install on dev machines), and the problem grows with autonomy. Risks: crowding from AI-security startups and vendor-native controls.

### 12. Agents making destructive database and schema changes
- **Problem:** Agent-generated migrations and SQL can irreversibly destroy or corrupt production data, and agents ignore warnings.
- **Who has it:** Backend and data platform teams. Every company with a production RDBMS and agent adoption.
- **Evidence:** "When they generate migrations, the worst outcome is irreversible data corruption... agents often don't respect warnings" (https://atlasgo.io/use-cases/ai-safe-migrations). Prisma added detection of AI agents plus a consent environment variable to block `migrate reset --force` (https://www.prisma.io/blog/stop-your-ai-agent-dropping-your-database).
- **Economic pain:** Rare but severe. Hard to justify $50K+ ACV on its own.
- **Competitors:** Atlas (Ariga), Bytebase, Neon branching, PlanetScale, Liquibase, Prisma.
- **Why unsolved:** Partly solved by existing schema tools adding agent policies.
- **Verdict: WEAK-MEDIUM.** Better as part of #11 or #8.

### 13. Merge conflicts and coordination between parallel agents
- **Problem:** Running many agents on one repo leads to frequent conflicts (reported cross-agent conflict rate of 41.7%) and semantic clashes that git does not detect.
- **Who has it:** Early-adopter teams running fleets of background agents. Hundreds to a few thousand companies today, but growing fast.
- **Evidence:** https://www.morphllm.com/parallel-coding-agents (secondary); Adam Tornhill on merge conflicts as "the new agentic bottleneck" (https://adamtornhill.substack.com/p/why-merge-conflicts-became-the-new, snippet); arXiv 2607.04697 on pre-write coordination.
- **Economic pain:** Today mostly wasted tokens and developer time. Could grow to an infrastructure-level problem.
- **Competitors:** Open-source orchestrators (Conductor, Claude Squad, Emdash, Composio); Graphite stacked PRs; merge queues (Trunk, Mergify, Aviator); Factory, Devin.
- **Why unsolved:** Too early. The workflow is still being invented, and agent vendors will likely absorb it.
- **Verdict: MEDIUM (future).** "Air-traffic control for agent fleets" fits 2028-2032, but the market is small today and the risk of being bundled is high.

### 14. Architecture drift and convention erosion
- **Problem:** Agents ignore AGENTS.md and copy degraded patterns, so architecture erodes and duplication compounds.
- **Who has it:** Staff engineers and architects at companies with large codebases. Roughly 10-20K companies.
- **Evidence:** GitClear 2025: 5+ line duplicated blocks rose 8x in 2024, and refactored/moved code fell from 25% to under 10% (https://www.i-programmer.info/news/105-artificial-intelligence/17871-gitclear-reveals-ais-negative-impact-on-code-quality.html). ThoughtWorks Radar: "architecture drift reduction with LLMs" (https://www.thoughtworks.com/radar/techniques/architecture-drift-reduction-with-llms). arXiv ContextCov on agents deviating from instructions (https://arxiv.org/html/2603.00822v1).
- **Economic pain:** Long-term maintenance tax, perhaps 10-20% of capacity over years. Hard to sell.
- **Competitors:** CodeScene, ArchUnit, SonarQube, vFunction (architecture observability), CodeRabbit/Greptile custom rules.
- **Why unsolved:** Buyers do not pay for long-term health. Rules are hard to codify.
- **Verdict: WEAK-MEDIUM.** Important but weak urgency. Likely a feature of review tools.

### 15. Specs and requirements become the bottleneck
- **Problem:** When implementation is cheap, ambiguous tickets and lost context drive agent failure. Product and engineering lack a structured "intent layer."
- **Who has it:** Product managers, tech leads at all software companies. Roughly 50K+.
- **Evidence:** Tessl's founder: the bottleneck "is not the agent but the context around it" (https://rywalker.com/research/tessl). AWS Kiro built a spec-driven IDE (https://kiro.dev/about/).
- **Economic pain:** Rework from misunderstood requirements is large but diffuse.
- **Competitors:** Kiro (AWS), GitHub Spec Kit, Tessl ($125M), Linear/Jira AI, Factory, Notion.
- **Why unsolved:** Unclear whether this is a product category or a workflow inside the IDE or tracker. Incumbents (Atlassian, Linear, GitHub) are well placed.
- **Verdict: MEDIUM-WEAK.** Big vision, but platform risk is very high.

### 16. Choosing and tuning coding agents for your own codebase
- **Problem:** Public benchmarks do not predict how agents perform on a company's own repo, so companies choose tools, models, and harness settings blind.
- **Who has it:** DevEx and platform teams at companies with 300+ engineers making $1-20M tool decisions. Roughly 5-10K.
- **Evidence:** "The most reliable benchmark is the one you run against your own codebase" (https://blaxel.ai/blog/llm-coding-benchmarks). Bitrise built its own eval framework and its own agent (https://levelup.gitconnected.com/choosing-the-best-ai-coding-agent-for-bitrise-72a0bb1edd91). CodeProbe open source replays merged PRs as evals (https://pypi.org/project/codeprobe/0.13.0/).
- **Economic pain:** Buying decisions worth $1-20M/yr. Choosing the wrong model or harness wastes 20-40%.
- **Competitors:** Mostly in-house or open source. Braintrust, Galileo, and others are general LLM eval tools, not specific to coding.
- **Why unsolved:** New. Buyers only now hold multi-vendor agent portfolios.
- **Verdict: MEDIUM.** Could be a strong wedge into #3 (spend) as the "control plane for coding agents" ("which agent, which model, which task, at what cost"). Weak alone.

### 17. Flaky tests amplified by agent iteration loops
- **Problem:** Flaky tests mislead agents (they "fix" non-bugs or retry endlessly) and waste human time.
- **Who has it:** Teams with large test suites. Roughly 20K companies.
- **Evidence:** Atlassian estimated flaky tests cost it 150,000 developer hours per year (https://trunk.io/blog/trunk-flaky-tests-is-out-of-beta; see also https://dev.to/sol_causely/the-real-cost-of-flaky-ci-a-community-survey-nil).
- **Economic pain:** $18K/yr for a 20-person team, up to millions at large orgs.
- **Competitors:** Trunk, BuildPulse, Datadog CI Visibility, Launchable (CloudBees), Gradle Develocity.
- **Verdict: WEAK.** Existing players cover it. Feature rather than company.

### 18. Open-source maintainers and inner-source repos flooded with slop PRs
- **Problem:** Low-quality AI PRs swamp maintainers. One estimate says 1 in 10 is legitimate.
- **Who has it:** Open-source maintainers and inner-source platform owners.
- **Evidence:** GitHub weighed a PR "kill switch". A Godot maintainer called slop PRs "draining and demoralizing" (https://www.theregister.com/2026/02/03/github_kill_switch_pull_requests_ai/).
- **Economic pain:** Low willingness to pay (open source).
- **Competitors:** GitHub natively.
- **Verdict: WEAK.** No buyer. Signal only.

### 19. License and IP contamination from AI-generated code
- **Problem:** AI emits snippets derived from copyleft code that bypass package-based license scanning. AI-only output may also not be copyrightable.
- **Who has it:** Legal, OSPO, and M&A diligence at software companies. Roughly 10K companies with OSPOs.
- **Evidence:** OSSRA 2026 reports the largest year-over-year jump in license conflicts in 11 years, and 17% of OSS enters outside package managers (https://www.herodevs.com/blog-posts/68-of-codebases-contain-license-conflicts-and-ai-generated-code-is-making-it-worse). Supreme Court denied cert in Thaler v. Perlmutter (Mar 2026), per https://tianpan.co/blog/2026/04/19/ai-output-copyright-trap-llm-generated-code (secondary).
- **Economic pain:** Concentrated around M&A and audits. Episodic.
- **Competitors:** Black Duck, FOSSA, Snyk, ScanCode; vendor IP indemnities (Microsoft, Anthropic, etc.).
- **Verdict: WEAK.** Indemnities and incumbents cover most of it. Episodic buyer.

### 20. No provenance record of which code was AI-written (attribution and audit)
- **Problem:** Git records the human committer, not the agent, model, or prompt, so companies cannot audit, attribute incidents, or measure AI code quality.
- **Who has it:** Platform and security teams, and compliance at SOC2/ISO software companies. Roughly 20K.
- **Evidence:** A wave of open-source tools appeared in 2026: agentdiff (https://docs.rs/agentdiff), Semantica (https://pkg.go.dev/github.com/semanticash/cli), LineageLens. GitHub is considering AI attribution for PRs (The Register link above). Amazon's policy requires knowing which code was AI-assisted.
- **Economic pain:** Not a standalone budget. It enables #2, #5, and #11.
- **Competitors:** Open-source tools; Faros/DX/Jellyfish measure AI usage; vendor telemetry.
- **Verdict: MEDIUM as a data layer, WEAK alone.** Provenance is the dataset that makes a change-risk product (#5) or governance product (#11) defensible.

### 21. Junior developer pipeline collapse and skill erosion
- **Problem:** Entry-level hiring falls, and juniors who rely on AI never build debugging skill, which threatens the future senior pipeline.
- **Who has it:** Engineering leaders, but with weak willingness to pay.
- **Evidence:** Stanford "Canaries in the Coal Mine": employment of developers aged 22-25 in AI-exposed roles fell about 13% (https://leaddev.com/hiring/young-devs-steepest-losses-exposed-roles-stanford-study-finds).
- **Economic pain:** Long-term and societal. Not on an annual budget.
- **Verdict: WEAK.** Not a B2B wedge at $25K+ ACV.

### 22. Legacy migration and modernization at scale
- **Problem:** Enterprises want agents to modernize millions of lines (Java upgrades, framework migrations), but agents struggle with large-scale coordinated change.
- **Who has it:** Large enterprises (excluding banking, insurance, and government per constraints, which removes much of the COBOL market). Roughly 5K companies with large legacy estates.
- **Evidence:** Moderne grew customers 250% in 2024 and raised $30M. Its OpenRewrite engine is embedded in Amazon Q and Copilot (https://fintech.global/2025/02/12/moderne-raises-30m-series-b-to-accelerate-ai-powered-code-transformation/).
- **Economic pain:** $1-20M per migration program. Services-heavy.
- **Competitors:** Moderne, Grit (acquired by Honeycomb), Amazon Q Transform, Copilot app modernization, vFunction, plus GSIs (Accenture, Infosys).
- **Why unsolved:** Hard deterministic plus LLM hybrid work. Customers in excluded sectors dominate spend.
- **Verdict: MEDIUM.** Large ACVs, but GSIs and hyperscalers compete and the work trends toward services.

### 23. Production context missing from coding agents
- **Problem:** Agents write code without knowing how it behaves in production (hot paths, error rates, real inputs), so they create performance and reliability regressions.
- **Who has it:** Backend teams at SaaS companies. Roughly 20K.
- **Evidence:** Hud raised $21M for a "runtime code sensor" that feeds function-level production behavior to agents (https://clickhouse.com/blog/hud-runtime-code-sensor). OneUptime: "AI is writing your code. Who is watching it run?" (https://oneuptime.com/blog/post/2026-03-12-ai-is-writing-your-code-who-is-watching-it-run/markdown).
- **Competitors:** Hud, Datadog/Sentry MCP servers, Lightrun.
- **Verdict: MEDIUM.** Logical direction, but observability incumbents (Datadog, Sentry) will push into it hard.

---

## Top 5 most promising

1. **Pre-deploy change-risk control for AI-era changes (#5 + #20).** "Every change, human or agent, gets a blast-radius score and an automatic rollout or approval policy." The evidence is the strongest: Amazon's 90-day safety reset and senior sign-off mandate, and DORA's rising instability. AI SRE (Resolve, Traversal) is funded *after* incidents, while the pre-deploy gate is underbuilt. ACV $50-250K. Buyer: VP Eng or Head of SRE. Moat: proprietary dataset linking provenance, diff, runtime, and outcome.
2. **Coding-agent spend control plane (#3 + #16).** "Ramp for Claude Code, Cursor, and Codex spend": cross-vendor allocation, budgets, model routing, loop detection, and per-task ROI. Uber and Microsoft budget blowouts, Copilot's move to usage-based billing, and Gartner's warning all make the pain acute in 2026. ACV $50-200K, savings fund the purchase. Risk: vendor-native controls and generic FinOps tools (Finout, CloudZero) adding features.
3. **Governance, identity, and audit for coding agents (#11 + #12).** "Okta and CrowdStrike for coding agents." CISOs hold the budget. The Replit and Kiro destructive-action incidents are concrete. Pilots are fast. Risk: crowded AI-security field (Zenity, Noma, Lasso, MCP gateways) and Anthropic or Cursor shipping enterprise controls.
4. **Agents self-verify in realistic environments before human review (#8 + #7).** The shift from review to proof: an ephemeral, stateful environment plus traffic replay plus test-effectiveness scoring. Raindrop's $50M validates it. Signadot and Okteto are older infrastructure plays. Room remains for data and state realism plus machine-readable verdicts.
5. **Review triage and risk-tiered auto-merge (#1, repositioned).** Not another AI reviewer. Instead the policy layer that decides which PRs merge automatically, which need one human, and which need an expert. Large pain (+91% review time), but CodeRabbit, Greptile, Qodo, and Cursor/Graphite will move toward it, so this ranks lowest of the five.

**Overall take:** The obvious "AI code review" wedge is already crowded (CodeRabbit ~$550M, Qodo $120M raised, Greptile, Graphite acquired). Whitespace sits around *control* (spend, permissions, deploy risk) and *verification* (environments, test effectiveness), where incidents and budget blowouts in 2026 have created urgent, budgeted pain.
