# Thesis G: Source control and code hosting built for agents

*Round 8 deep dive. 2026-10-05. Red-team analyst. 36 web searches. WebFetch was blocked for almost every domain, so the facts below come from search-result snippets. Anything marked [unverified] could not be checked against a primary source.*

**One-line verdict: KILL.** The pain is the most real and best documented of any thesis so far. But every wedge is already taken by a well-funded company that shipped in the last 12 months. Wedge (a) is held by Pierre ($23M, CRV) and Cloudflare. Wedge (b) is held by Entire ($60M seed, the former GitHub CEO). Wedge (c) is held by Cursor Origin (beta since Aug 17 2026). It is the clearest case yet of structural conclusion #2: the more visible the pain, the more crowded the space.

---

## Problem
The traffic on code hosting is now mostly machine traffic, not human. GitHub's architecture is a Rails monolith with Spokes/DGit storage and MySQL, sized for human request rates. It is now in an extended reliability crisis. Agents hit secondary rate limits, clone throttling, Actions failures and full outages, and each of these stalls whole agent fleets.

## Recent evidence (trigger, verified or extended)
1. **Load.** GitHub COO Kyle Daigle reported about 275M commits per week, on pace for about 14B in 2026. Agent-opened PRs went from about 4M (Sep 2025) to 17M+ (Mar 2026). (newclawtimes.com, techlogstack.com, quasa.io, dev.to/techlogstack; these are secondary sources.) The "~1B commits in all of 2025" comparison is [unverified].
2. **GitHub CTO Vlad Fedorov, "An update on GitHub availability".** The capacity plan grew from 10x (Oct 2025) to a 30x redesign (Feb 2026). Peaks reached 90M merged PRs and 1.4B commits. Stated fixes: isolate critical services, migrate hot paths from Ruby to Go, move to public cloud and multi-cloud, and optimize merge queue and monorepo handling. New stated priority: "Availability first, then capacity, then new features." (github.blog, read via snippets from daily.dev and techlogstack.)
3. **Incident counts.** 257 incidents from May 2025 to Apr 2026, 48 of them major; 37 in February 2026 alone. On May 15 2026, an Actions degradation failed 42% of runs at peak. On Aug 17, a 7h47m degradation came from load-balancer saturation: an Istio sidecar hit its concurrency limit and a misconfigured autoscale policy kept it from scaling. Microsoft routing GitHub traffic through AWS was reported Jun 16 2026. (techlogstack, techtimes.com/articles/318481, tech-insider.org/microsoft-aws-github-outages-2026.) The "9 incidents in May" figure appears at windowsnews.ai. The "88.4% availability in June" figure is [unverified]; the Register reports 90.21% over 90 days as of late April. The VS Code retry-storm detail is [unverified].
4. **Practitioner exodus.** Mitchell Hashimoto moved Ghostty off GitHub (announced Apr 28 2026, theregister.com/2026/04/29). His quote: "The issue isn't Git, it's the infrastructure we rely on around it: issues, PRs, Actions" (Register, May 15 2026). This matters for the thesis: the pain is in the forge, not in Git itself.
5. **Rate-limit workarounds in the wild.** Recent GitHub issues show teams building shared backoff and throttled `gh api` wrappers for agent sessions, for example cbusillo/codex-skills#1042 and the-hcma/repository-helpers#608. That is homegrown workaround code, but it is cheap to write and lives on the client side.
6. **Still not fixed.** On Sep 13 2026, about 28 services were degraded for 2 hours. GitHub now publishes availability numbers on its status page.

## Who has the pain
1. AI app builders that store millions of repos (Lovable, Bolt, Replit, v0, Base44 and similar).
2. Enterprises running fleets of background agents against GitHub.
3. Open-source maintainers. They don't pay.

## What they do today
- **App builders.** Lovable, Bolt, Amp, Poke, Anything and Parahelp are named customers of **Pierre code.storage**. Freestyle reports customers with "hundreds of thousands of repositories". So this has already been bought from a vendor, not built in-house.
- **Enterprises.** Backoff wrappers, GitHub Apps (which get per-installation rate limits), read mirrors, and now the Entire or Cursor Origin mirrors.
- **Open source.** Forgejo, Codeberg, Tangled.

## Why current products fail
GitHub does fail today. The startups built for this load do not obviously fail; they are 3 to 12 months old and growing. There is no evidenced gap left open.

## Why now
The timing is real. The load step-change started in December 2025, GitHub has been at roughly one nine of availability, and Microsoft's Azure migration is in progress. But the "why now" moment was Feb to Aug 2026, and the capital has already arrived.

## Competition (the killer)
| Player | What it is | Funding / traction | Wedge it takes |
|---|---|---|---|
| **Pierre code.storage** (Jacob Thornton) | Headless, API-only, white-label Git for machines: ephemeral branches, GitHub sync, LFS, webhooks, grep | $23M led by CRV + O1A. Customers: Lovable, Bolt, Amp, Poke, Anything, Parahelp. Sustained peak above 15,000 repos/min for 3 hours; above 9M repos created in 30 days. Pricing: hot storage $0.75/GB/mo, cold $0.05/GB/mo | (a), fully |
| **Cloudflare Artifacts** | Git-compatible versioned storage for agents, aimed at tens of millions of repos; REST API plus Workers | Open beta (since about May 2026, InfoQ). Approaching 50k repos/day. Running a contest to "build the next Git platform on Cloudflare" | (a), with platform-absorption risk |
| **Freestyle** (YC; Floodgate, Two Sigma) | Multi-tenant Git plus forkable VMs, with GitHub sync | Launch HN Apr 2026. Customers with hundreds of thousands of repos. Amount raised [unverified] | (a) bundled with sandboxes |
| **Mesa** (YC S24) | Versioned POSIX filesystem plus headless Git server for parallel agents; has a code-storage pricing page | Funding [unverified] | (a) |
| **Entire** (Thomas Dohmke, former GitHub CEO) | Distributed Git network. One-step GitHub mirror so agents clone and pull from Entire; about 570k clones/hr and 586 pushes/s on one repo. Roadmap: Git-compatible database, semantic layer, agent UI | $60M seed at $300M valuation (Felicis, Madrona, M12). Preview launched Jul 8 2026 in US, EU and AU regions | (b), almost word for word; (c) on the roadmap |
| **Cursor Origin** (Anysphere) | Git forge: repos, PRs, two-way GitHub sync, agents built in. Reported 296k clones/hr [unverified] | Early beta Aug 17 2026, included in every paid Cursor plan. Owns Graphite (merge queue, stacked PRs; acquired Dec 2025). A reported SpaceX acquisition of Anysphere for about $60B [unverified, treat with caution] | (c), and enterprise (b) |
| **GitHub** | 30x redesign, Ruby to Go, multi-cloud via Azure plus AWS, merge-queue work, Agent HQ, stacked diffs coming 2026 | Incumbent with roughly 100M+ developers; Universe is Oct 28-29 2026 | All three, eventually |
| **GitButler** (GitHub co-founder) | Agent-aware Git client: parallel and stacked branches | $17M Series A, a16z (Apr 2026) | Client and workflow layer |
| **Tangled** | AT Protocol forge where agents can push | $4.5M seed (Mar 2026), with Dohmke as an angel | Open-source and EU niche |
| **GitLab** | Duo Agent Platform with usage-based credits | Public company | Enterprise incumbent |
| Others | Diversion, Graphite (inside Cursor), Forgejo/Codeberg, Daytona/E2B/Modal snapshots (the sandbox side) | n/a | Adjacent |

That is at least four funded companies plus Cloudflare built specifically for agent-scale Git, all launched between Oct 2025 and Aug 2026. Two are led by people central to GitHub's history (its former CEO; Thornton is ex-Twitter, and his team includes former GitHub engineers).

## Why GitHub can't fix it (and why that doesn't help us)
- **Structural limits are real.** A Rails monolith and MySQL, Spokes replication sized for humans, an Azure migration in progress (12.5% of traffic on Azure, target 50% by Jul 2026), and a business incentive tilted toward Copilot features. The CTO's statement that "availability comes first" is itself an admission.
- **But it doesn't matter to a newcomer.** GitHub's weakness creates the opening, and Entire and Cursor already went through it. Their advantages over a new startup are distribution (Cursor's paid base), brand and capital ($60M), and enterprise trust (Dohmke). GitHub also only needs to become "good enough" (back to 99.9%) to stop most enterprises from moving. Its 30x program plus AWS capacity makes recovery within 6 to 12 months plausible.

## Potential product
(a) A Stripe-style API for code storage for app builders. (b) An agent-side mirror and cache in front of GitHub. (c) A full forge for AI-native teams. All three already exist, see the table.

## Time to value
Hours for (a) and (b). That is fast, but it also means switching costs are low between agent-native vendors.

## Pilot (14 to 30 days)
- (a) Migrate one app builder's new repos to our API.
- (b) Mirror one enterprise agent fleet's top 50 repos and measure clone p95 and rate-limit errors.

Both are technically feasible. The problem is that the buyer's comparison set is Pierre, Cloudflare and Entire, which are free or cheap and already in production.

## Willingness to pay
- **(a)** Usage-based storage. At $0.75/GB hot, most generated repos are a few MB, so 10M repos is about 10-50 TB, roughly $90K-450K per year per large builder, compressing toward Cloudflare's commodity price. A few builders are at $1M+.
- **(b)** Enterprise mirror at roughly $50K-300K per year. GitHub Enterprise, Cursor and Entire will all bundle it.

## Expansion
CI, merge queue, agent code search and indexing, review, deploy: the "GitHub of the agent era". This is the right story, and it is exactly the stated roadmap of Entire and Cursor Origin.

## Moat
- **10 customers.** None. Git is an open protocol and repos sync both ways.
- **100 customers.** Ops excellence and scale economics. Cloudflare and Pierre are ahead.
- **1,000 customers.** A forge network effect: PRs, review, identity. This accrues to whoever owns humans plus agents, which favors GitHub and Cursor.

## CTO test sentence
"Your agents never wait on GitHub again: they clone, branch and push against us at 100x the rate limits, and we sync to GitHub for your humans."
**Likely CTO reply:** "Entire does that, Cursor just gave me Origin with my existing licence, and GitHub says it's fixing it. Why you?"

## Kill test question
Is there a segment of agent-scale code-hosting buyers that Pierre, Cloudflare, Freestyle, Entire, Cursor Origin and GitHub's 30x program all fail to serve? **No evidence that there is.** Kill signals 3 (Pierre already owns wedge a) and 1 (GitHub is mid-fix, and Entire/Cursor own b and c) are both confirmed.

---

## Scores: METHOD template (1-10)
| Criterion | Score | Note |
|---|---|---|
| Pain severity | 8 | Most documented pain of all 29 theses |
| Urgency | 7 | Acute Feb-Aug 2026; GitHub is mid-fix |
| Market timing | 4 | Right moment, but about 9 months late |
| Speed to pilot | 7 | Mirror or API pilot in days |
| Ease of integration | 8 | Speaks Git |
| Ease of reaching customers | 4 | App builders are already signed with Pierre; enterprises are being courted by Cursor and Dohmke |
| Willingness to pay | 5 | Storage is commoditizing (Cloudflare) |
| Competition | 1 | Four or more funded specialists, Cloudflare, Cursor and GitHub |
| Moat potential | 3 | Open protocol, two-way sync, zero switching cost |
| Market size | 7 | GitHub was acquired for $7.5B; GitLab is public |
| VC attractiveness | 3 | VCs have already picked their horses (CRV, Felicis, a16z) |
| **Average** | **5.2** | |

## Scores: original bar
| Criterion | Score |
|---|---|
| Pain | 8 |
| Urgency | 7 |
| ROI clarity | 6 |
| Customer accessibility | 4 |
| Pilot speed | 7 |
| Market size | 7 |
| Expansion | 7 |
| Venture potential | 4 |
| Defensibility | 3 |
| Why now | 6 |
| Competition position | 1 |
| **Average** | **5.5**; four categories are below 7, against a bar of 8.5 with nothing below 7 |

## Market math
- **$10M ARR.** About 15 app builders at roughly $300K each, plus about 50 enterprises at roughly $100K. That means taking customers from Pierre and Cloudflare: plausible only on price, and Cloudflare will win on price.
- **$50M ARR.** About 250 enterprise agent fleets at $200K. This competes directly with Cursor (bundled with existing licences), Entire and GitHub Enterprise.
- **$100M ARR.** Requires becoming a forge, not a storage layer. That is the "GitHub of the agent era" race, and Cursor (owning Graphite), Entire and GitHub are already 6 to 12 months and $60M+ ahead.
- **TAM** is large (GitHub was on a reported $2B+ run-rate [unverified]). The share available to a 2026-Q4 entrant is very small.

## Five simulated buyers
1. **Infra lead at a top-10 app builder (already on Pierre): NO.** "We moved to code.storage last year; it does 15k repos/min. Re-platforming has no upside."
2. **Platform lead at a startup app builder (around 100k repos): MAYBE leaning NO.** "Cloudflare Artifacts is pennies and we're already on Workers. Freestyle gives us VMs and Git together."
3. **VP Engineering at a Fortune 500 with 2,000 agent sessions a day on GitHub Enterprise: NO.** "We're not moving code hosting. Microsoft gave us SLA credits and an AWS-backed capacity plan. If we need a mirror, Entire is run by the guy who ran GitHub."
4. **CTO of a 200-person AI-native startup on Cursor: NO.** "Origin came with our Cursor plan."
5. **Head of developer productivity at a fintech with a big monorepo and rate-limit pain: MAYBE.** "A cache that kills our 403s is worth $100K. But my team built a GitHub App plus a read-through cache in two weeks." This fails the sprint test from round 8.

Result: 0 YES, 2 MAYBE, 3 NO.

## VC committee view
- **Could it be $10B?** The category could. The agent-era forge plausibly reaches $10B+, given GitHub's $7.5B price in 2018 and today's AI-scaled load.
- **Would we lead the seed today?** No. A partner would ask why we would back a fifth entrant against Dohmke ($60M at $300M), Pierre (CRV, with Lovable and Bolt as customers) and Cursor, which has distribution plus Graphite. The only fundable version is a non-consensus technical bet, for example a non-Git, jj-style or CRDT-native VCS with agent conflict resolution and a named founder pedigree. That is a different thesis with deep tech risk.

## Red team
- **Strongest bull case.** The market is huge and GitHub is visibly failing. Incumbent displacements happen during reliability crises; Slack beat HipChat on reliability, for example. Multiple winners are possible: storage (Pierre, Cloudflare), mirror (Entire), forge (Cursor).
- **Rebuttal.** All three of those winner slots are already filled by funded or distribution-advantaged players. Our only claimed advantage would be "built for agents", which is exactly what every one of them markets. Infra-layer storage gets absorbed by Cloudflare, AWS (S3 Express or similar is a likely follow) and GitHub. The enterprise mirror is a sprint project or a Cursor/Entire bundle. A full forge requires network effects we cannot bootstrap ahead of Cursor.
- **Unverified risks in our evidence.** Some trigger stats come from low-quality aggregator sites (techlogstack, quasa, newclawtimes). The SpaceX/Anysphere deal is [unverified]. None of this changes the verdict, because the competitor launches are corroborated by multiple outlets (TechCrunch, GeekWire, SD Times, InfoQ, DevOps.com).

## VERDICT: KILL
- **Cause of death:** crowding plus platform absorption. Pierre and Cloudflare own wedge (a), Entire owns (b), Cursor Origin (with Graphite) owns (c), and GitHub is running a 30x rebuild.
- **Reframe considered and rejected:** "agent merge-conflict and coordination layer among parallel agents". Thesis T3 died on this already (GitHub, Cursor and Greptile shipped it Sep 2026), and Entire's "semantic reasoning layer" is aimed squarely at it.
- **Lesson for STATUS.md:** a public infrastructure-failure crisis at an incumbent attracts specialist capital within weeks. By the time it reaches the Pragmatic Engineer, it is already funded.

## Sources (from search results; most could not be opened)
- blog.pragmaticengineer.com/the-pulse-ai-load-breaks-github/ ; blog.pragmaticengineer.com/the-pulse-is-github-still-best-for-ai-native-development/
- code.storage ; code.storage/pricing ; code.storage/changelog/introducing-code-storage ; x.com/fat/status/2089760972387000387
- techcrunch.com/2026/02/10/former-github-ceo-raises-record-60m-dev-tool-seed-round-at-300m-valuation/ ; geekwire.com/2026/former-github-ceo-launches-new-developer-platform-with-huge-60m-seed-round/ ; entire.io/news/entire-launches-distributed-git-network-for-the-agent-era ; sdtimes.com/softwaredev/startup-entire-launches-distributed-git-network-for-the-agent-era/
- devops.com/cursor-launches-origin-code-hosting-platform-as-github-rival/ ; testingcatalog.com/cursor-begins-origin-code-hosting-rollout-for-paid-plans/ ; siliconangle.com/2025/12/19/cursor-acquires-ai-code-review-startup-graphite/
- infoq.com/news/2026/05/cloudflare-artifacts-ai-agents/ ; blog.cloudflare.com/next-git-platform-on-cloudflare/
- docs.freestyle.sh ; hn.svelte.dev/item/47663147 ; mesa.dev/features/git-server
- siliconangle.com/2026/03/02/tangled-announces-4-5m-round-build-github-alternative-built-blueskys-protocol/ ; pulse2.com (GitButler $17M Series A)
- techtimes.com/articles/318481/20260616/... ; tech-insider.org/microsoft-aws-github-outages-2026/ ; windowsnews.ai (9 May outages) ; theregister.com/2026/04/29/mitchell_hashimoto_ghostty_quitting_github/ ; theregister.com/devops/2026/05/15/git-is-unprepared-for-the-ai-coding-tsunami/5241480
- github.com/cbusillo/codex-skills/issues/1042 ; github.com/the-hcma/repository-helpers/issues/608
- about.gitlab.com/blog/introducing-gitlab-credits
- Not checked: codely.com and the gigazine 20260821 article.
