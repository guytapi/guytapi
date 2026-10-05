# P2: Agent Pick Rate, a "Search Console for getting chosen by coding agents"

Date: 2026-10-05 · Origin: round15 idea #18 / deep dive A (avg 7.0) · Searches: 40 of 40. WebFetch was blocked for every domain tried (amplifying.ai, stackone.com, yage.ai), so **all facts come from search-result summaries** unless marked otherwise. "[unverified]" marks a claim I could not confirm from a primary page. "[estimate]" marks my own arithmetic. "[memory]" marks a fact from background knowledge that I did not search.

**Thesis tested:** "AI coding agents now choose your customers' tech stack. We're the Search Console for getting chosen by agents." The product would run thousands of agent sessions to measure pick rate, integration success and the reasons agents choose a competitor. It would then generate fixes and run as a CI check on every docs or SDK release. The expansion path is: all APIs and SaaS → an agent-facing DX platform → the "Nielsen of agent-driven adoption".

---

## VERDICT up front: **KILL as a standalone venture** (original-bar average **6.3**, down from 7.0)

The phenomenon is real and is the strongest "why now" we have seen in 15 rounds. Agents now trigger more than 50% of Vercel deployments, 60-70% of new Supabase databases, 80%+ of Neon databases, and 62-66% of traffic to Mintlify-hosted docs.

The business does not survive red-teaming, for three reasons:

1. **The exact product was funded four weeks ago.** Lightsage raised a $4M seed led by Nexus on Sep 8, 2026. It runs "Agent-Led Growth" simulations across Claude Code, Codex, Cursor, Copilot and OpenCode, diagnoses failures (discoverability, docs, auth, endpoint, SDK, MCP), tracks real agent traffic, and names customers (Firecrawl, Reducto, Daytona, Rime, Tinyfish). Amplifying already sells vendor-intelligence reports covering 4 agents, 10K+ queries and 20 categories. Armature (YC P26) ships Analytics (launched Jul 28) and Evals for MCPs and CLIs (launched Aug 4).
2. **The measurement layer is being given away.** Netlify AXIS is free under MIT and supports 22 agents. Vercel and Ora launched is-agentic.com as a free scorer. Supabase built its own open-source Supabase Evals (Jul 31) to benchmark Claude Code, Codex and OpenCode on its platform. Mintlify ships agent-traffic analytics natively. The leaders build this in-house.
3. **The labs are monetizing placement.** OpenAI launched Sponsored Agents (Sep 16, 2026) on a ChatGPT ads business that reached a $1B run rate in about seven months. Anthropic bought Stainless ($300M, May 2026) and curates the official plugin marketplace (68 partner plugins). If tool selection becomes an ad surface, measurement belongs to the ad seller, just as Google gives Search Console away free.

---

## 1. Is agent-driven tool selection real and material in 2026? **Yes: strongly observed, not forecast**

| Signal | Data | Source (search summary) |
|---|---|---|
| Vercel | Agent-initiated weekly deployments rose from under 3% to more than 50% between Jan and Jul 2026. Agent-deployed projects are 20x more likely to call AI inference. Earlier: "10% of Vercel signups arrive via ChatGPT" | https://startupfortune.com/guillermo-rauch-says-ai-agents-now-trigger-more-than-half-of-all-vercel-deployments/ · https://ecommercenews.co.nz/story/vercel-unveils-agent-tools-as-deployments-turn-ai-led |
| Supabase | More than 60% of new databases are started by AI tools, with Claude Code the largest single source. Database launches grew 600% YoY. One summary says 70% by Oct 2026 [unverified]. $500M Series F at $10.5B | https://www.implicator.ai/supabase-doubles-to-10-5-billion-as-agents-deploy-most-of-its-databases/ · https://letsdatascience.com/blog/supabase-10-5-billion-ai-agents-build-most-databases |
| Neon | More than 80% of databases are created by agents (30% at launch). Databricks acquired Neon for about $1B (May 2025) | https://www.databricks.com/blog/databricks-neon |
| Mintlify docs | Agents made 61.87% of docs visits in Aug 2026 (212M agent visits vs 131M human), up from 15.2% in Jan 2026 | https://mintlify.com/blog/state-of-docs-traffic |
| Resend | ChatGPT is its top customer-acquisition channel (YC podcast, Feb 2026) [secondary] | search summary only |
| Lovable | 100K+ new projects per day (Dec 2025). Supabase and Stripe are built in as defaults | https://automationatlas.io/tools/lovable/ |
| Convex | $57M Series B (Aug 2026) to be "the backend for agent-written software" | https://www.unite.ai/convex-raises-57m-series-b-to-build-the-backend-for-agent-written-software/ |
| Picks are concentrated | Claude Code: GitHub Actions 94%, Stripe 91%, shadcn 90%, and it builds DIY in 12 of 20 categories. Redux → Zustand in 0 of 88 cases. Vitest 101 picks vs Jest 7. Claude picks Bun 63% vs Codex 13%. Codex leans Cloudflare, Claude leans Vercel | https://amplifying.ai/research/claude-code-picks · https://s.amplifying.ai/research/codex-vs-claude-code-picks/report |
| Agents disagree | Armature, Sep 3 2026: 16,893 sessions across 75 repos, 10 languages and 1,163 prompt variants. Agents agree in only 42% of cases. PayPal was mentioned 139 times and picked 0 times | https://pinggy.io/blog/what_ai_coding_agents_pick_for_your_stack/ · https://mer.vin/news/what-17000-coding-agent-runs-reveal-about-tool-choices/ |
| AX movement | Netlify coined "Agent Experience". AXIS (MIT) scores 4 dimensions across 22 agents. Netlify scored itself 84/100 | https://www.createwith.com/tool/netlify/updates/netlify-launches-axis-open-source-framework-to-measure-agent-experience-with-api |

**Important nuance (red team).** Agent selection follows three different mechanisms, and only the first can be fixed with docs:
- **(a) Model-learned priors** in Claude Code, Codex and Cursor. These can partly be moved with docs, llms.txt, skills and MCP, but mostly change through training data, on a 6-12 month lag.
- **(b) Hard-wired platform defaults.** Lovable/Bolt/Replit ship Supabase + Stripe built in, and Anthropic ships an official plugin marketplace with Vercel, Supabase, Firebase and others. These are **BD deals**, not optimization.
- **(c) Paid placement.** OpenAI Sponsored Agents is the first step.

A "Search Console" only moves (a), and (a) is the slowest lever.

## 2. Willingness to pay: **real but modest, and mostly from challengers**

- Armature sells growth services from $5K/month (round15 source). Lightsage and Amplifying have no public pricing.
- Lightsage's named customers are seed and Series A/B dev-infra startups (Firecrawl, Reducto, Daytona, Rime, Tinyfish). These are small budgets.
- Dev-tool companies already pay GEO vendors: Profound's customers include Cursor, MongoDB, Figma and Ramp. Budget exists under **Growth or the CMO**, and is bought as "AI visibility". Category leaders build in-house (Supabase Evals, Netlify AXIS).
- DevRel budgets are fragile:
  - more than half of medium and large companies cut DevRel budgets;
  - 40% of DevRel leads have no set budget;
  - 62% of dev-marketing teams *increased* budgets for 2026 (Draft.dev).
  - Source: https://draft.dev/2026-developer-marketing-survey and SlashData summaries.
- **Whose budget:** the Head of Growth or VP Marketing at a challenger. DevRel champions it but rarely owns the money. A CTO says "nice to have" unless integration success is broken.
- **Where the money really goes:** winners (Stripe, Vercel, Supabase) don't need the product, and losers' real fix is BD with Lovable or Anthropic, or ads. Paid demand is concentrated in the middle tier.

## 3. Competitors (searched hard)

| Player | What it does | Funding / traction | Threat |
|---|---|---|---|
| **Lightsage** | Agent-Led Growth platform: simulated tasks across APIs, SDKs, CLIs, MCP and Skills; failure root cause; real agent-traffic tracking; covers answer engines **and** coding agents (Claude Code, Codex, Cursor, Copilot, OpenCode) | $4M seed, Nexus, Sep 8 2026; angels include Postman's CEO and Salesforce's ex-CTO; 5 named customers | **Identical product; fatal** — https://thenextweb.com/news/lightsage-4m-nexus-agent-led-growth-coding-agents-eu-psd2-strong-customer-authentication |
| **Amplifying** | Public pick-rate research, a Coding Agents Index (daily GitHub signatures and npm), per-tech pages (e.g. /tech/supabase), and paid vendor-intelligence dashboards | Unknown funding; owns the public narrative (Feb 2026 study widely cited) | High; owns the "benchmark index" moat we would want — https://amplifying.ai/for-vendors |
| **Armature** | YC P26; Analytics for agent sessions on Claude Connectors, ChatGPT Apps and MCP; Evals across harnesses; the 16.9K-session study | $500K, 3 people | Medium-high — https://ycombinator.com/companies/armature |
| **Netlify AXIS** | Open-source AX scoring across 22 agents | Free (MIT) | Commoditizes integration-success measurement |
| **Ora + Vercel (is-agentic.com)** | Free agent-readiness scanner, 100+ checks, real agents, MCP/REST API | Vercel partnership | Commoditizes the free-scan funnel — https://ora.ai/blog/is-agentic-with-vercel |
| **Supabase Evals** | Vendor's own OSS benchmark of Claude Code, Codex and OpenCode | In-house | Proof that leaders self-build — https://runtimewire.com/article/supabase-launches-evals-ai-coding-agent-benchmark |
| **Profound** | GEO leader; its blog treats "Claude and Claude Code" as distinct answer engines, so it already thinks about coding agents [product coverage unverified] | $180M Series D at $1.8B (Sep 2026), 1,000+ brands, revenue 3x in 6 months | One module away — https://tryprofound.com/blog/claude-and-claude-code-are-distinct-answer-engines |
| **Scrunch (Sitecore)** | AXP serves agents an optimized site version | Acquired by Sitecore, Jun 2026 | Adjacent |
| **Mintlify** | Native agent-traffic analytics, llms.txt, hosted MCP | Docs incumbent | Owns the docs-fix surface |
| **Context7 (Upstash)** | Most popular MCP; feeds library docs to agents | 60.6K stars | Owns docs delivery to agents |
| **Stainless → Anthropic** | SDK + MCP generation | Acquired for $300M, May 2026; hosted generator wound down | A lab owns the SDK-ergonomics lever |
| Speakeasy, Fern (Postman) | SDK/MCP generators; also scored by agent-readiness indexes | Speakeasy $29M; Fern bought by Postman, Jan 2026 | Own the "fix the SDK" step |
| Free indexes | startuphub Agent Readiness Index, API Evangelist Kin Score, xpay agent-ready index | Free | Commoditize the score |
| Agencies | Evil Martians AX services, Derivatex, Carbon Ads guides | Services | Absorb the services budget |
| **The labs** | OpenAI Sponsored Agents (Sep 16 2026; ads at $1B run rate); Anthropic official plugin marketplace (33 first-party + 68 partner) | — | **Structural**: whoever sells placement owns measurement |

**Conflict-of-interest angle.** The original pitch was that "labs won't publish pick data, so a neutral measurer wins." That holds for *neutral* data. It does not stop labs from monetizing placement and giving attribution away, as Google did with Search Console. A neutral index is worth something (Nielsen, Similarweb), but Amplifying already holds that position, and its research is the reference everyone cites.

## 4. Market math

- **Customer count** [estimate]:
  - vendors with a public SDK, API or MCP and more than $1M ARR: about **4K-8K** worldwide (Tyler Jewell's devtools landscape alone lists 1,000+ notable vendors);
  - plus 20K+ smaller API and SaaS products that would use a free tier.
- **ACV:**
  - challenger mid-market: $12K-30K;
  - enterprise (PayPal-class, Twilio, Okta/Auth0, MongoDB): $60K-200K;
  - blended ~$25K [estimate].

| ARR target | Customers needed at $25K | Penetration of 6K core | Plausible? |
|---|---|---|---|
| $10M | 400 | ~7% | Yes, if you win the category, but Lightsage and Amplifying start ahead |
| $50M | 2,000 | ~33% | Only with enterprise ACVs, or with expansion beyond dev tools |
| $100M | 4,000 (or 1,000 at $100K) | 65%+ | Requires non-dev SaaS selected by agents, which **is GEO**: Profound, Peec, Scrunch/Sitecore, AthenaHQ, Otterly |

- **SAM for dev tools alone:** ~$150-250M [estimate].
- **Expansion to "every SaaS chosen by agents":** this is the Profound market, already led at $1.8B with 1,000+ brands. Entering from dev tools means attacking the leader from the narrow end.

## 5. Moat at 10, 100 and 1,000 customers

- **10 customers:** none. Sandboxed agent runs are reproducible by any team with API credits; AXIS is OSS; Supabase built its own in weeks.
- **100 customers:** a longitudinal panel across agent versions, plus a history of before-and-after effects of fixes. Amplifying already has a public index tracked since Feb 2025, and Lightsage gets the same data from its customer base.
- **1,000 customers:** causal "which fix moves pick rate" data and an industry benchmark (the Nielsen position). The labs see real installs across millions of sessions; we only see simulations. A model update (e.g. Opus or GPT version bumps) resets much of the learned playbook, so history decays fast.
- **Integration-success telemetry from CI:** sticky, but Armature Evals, AXIS and SDK vendors (Speakeasy, Stainless/Anthropic) sit on that workflow.

**Net: a thin moat that a lab can overturn.**

## 6. Pilot (14-30 days), CTO/CMO test, kill test

- **Pilot:** take 15 challenger vendors that are losing by language or category (e.g. Postmark/SendGrid vs Resend, PayPal vs Stripe, Jest vs Vitest, Auth0 vs Clerk or DIY).
  - Free baseline: 500 sessions per vendor across Claude Code, Codex and Cursor.
  - Apply 3 fixes (llms.txt or skill, MCP tool descriptions, quickstart and error-message patches) and re-measure.
  - Success means pick rate up ≥10 points **without a model update** at 5 or more vendors, and 5 of them sign at $2K+/month.
- **CMO test sentence:** "Claude Code picks your competitor 9 times out of 10 in Python and we know exactly which doc page loses you the deal." The CMO responds, but then asks: "Can't Profound or Lightsage do that, and isn't the fix just paying for placement?"
- **CTO test sentence:** "Agents integrate your SDK on the first try only 41% of the time; here is the CI check." This is real, but the CTO answers: "We'll run AXIS or Supabase-style evals ourselves."
- **Kill test:** after free baselines, do at least 5 of 15 challengers pay $2K+/month **instead of choosing Lightsage, Amplifying or a self-built AXIS harness**, and do docs fixes measurably move picks (as opposed to integration success) within 30 days? Desk evidence suggests picks are dominated by training priors and BD defaults, so the second condition will likely fail.

## 7. VC committee view

- **For:** "Agents are the new distribution channel" is one sentence, directional and exciting, and the data (Vercel 50%, Supabase 60-70%, Neon 80%) is the best why-now in the whole war room. It passes the founder's "interesting" filter.
- **Against:**
  1. Nexus already funded the exact pitch (Lightsage) on Sep 8; we are four weeks late, with no proprietary data.
  2. Google Search Console is **free**. The SEO industry's value went to Semrush (~$2B; Adobe agreed to acquire it for ~$1.9B in Nov 2025 [memory, unverified]) and Similarweb (<$1B market cap [memory]), not to the measurement primitive. The labs are the Google here, and OpenAI is already selling Sponsored Agents.
  3. A "$10B Nielsen" would need neutral panel data that labs, vendors and investors all buy. Amplifying holds the public-reference position, and the labs hold real telemetry.
  4. The large expansion market (all SaaS) is Profound's, at $1.8B with 3x revenue growth.
- **Committee outcome:** pass. This is a good company for someone; for a new team without a dataset or lab relationships it is late. Venture ceiling: likely $30-100M ARR for the category winner, who will probably be Lightsage, Amplifying or Profound. A $10B outcome needs the labs to stay neutral *and* not sell placement, and the evidence already contradicts that.

## 8. Kill signals (strongest first)

1. Lightsage ($4M Nexus, Sep 2026) ships this exact product with paying dev-infra customers.
2. Free measurement: Netlify AXIS (MIT), is-agentic.com (Vercel + Ora), Supabase Evals (OSS), Mintlify native agent analytics.
3. Labs monetize placement: OpenAI Sponsored Agents (Sep 16) and ads at a $1B run rate; Anthropic curates partner plugins and bought Stainless.
4. Defaults on vibe platforms are BD deals (Lovable ships Supabase + Stripe), so docs fixes cannot move them.
5. Picks track model training priors and reset with each model version, which weakens both the "fix" ROI and the longitudinal moat.
6. Leaders self-build; challengers have fragile DevRel budgets (more than half of mid and large companies cut them).
7. Amplifying owns the public-index narrative; Armature (YC) owns the most-cited 16.9K-session study.

---

## Scores: METHOD template (1-10)

| Field | Score | Note |
|---|---|---|
| Pain severity | 6 | Real for challengers losing share; leaders don't feel it |
| Urgency | 6 | Share is shifting now, but the fix (training priors, BD, ads) is not docs |
| Market timing | 9 | Agents trigger more than 50% of Vercel deploys and 60%+ of Supabase DBs |
| Speed to pilot | 9 | Public package names; no integration needed |
| Ease of integration | 10 | Outside-in |
| Ease of reaching customers | 8 | DevRel and Growth are reachable; leaderboard virality |
| Willingness to pay | 5 | $2-5K/month services anchor; leaders self-build; DevRel cuts |
| Competition | 3 | Lightsage, Amplifying, Armature, AXIS, Ora/Vercel, Profound, labs |
| Moat potential | 4 | Simulations copyable; labs hold real telemetry; model updates reset data |
| Market size | 6 | ~$150-250M dev-tool SAM; beyond that it is GEO |
| VC attractiveness | 6 | Great story, but the exact pitch was funded last month |
| **Average** | **6.5** | |

**Template fields (summary):**
- **Problem:** vendors can't see or influence why agents pick competitors.
- **Evidence:** see §1 (10+ independent signals).
- **Who:** Growth, DevRel and docs leads at challenger dev tools.
- **Today:** manual agent runs, AXIS, agencies, Amplifying reports, Lightsage.
- **Why products fail:** they no longer clearly do; Lightsage covers selection plus integration.
- **Why now:** agent-driven deploys went from under 3% to 50% in 2026.
- **Product, time to value, pilot:** see §6. Time to value is under 1 hour.
- **WTP:** $2-5K/month.
- **Expansion:** all SaaS → collides with Profound.
- **Competition:** §3.
- **Moat:** §5.
- **CTO/CMO test and kill test:** §6.

## Scores: original bar

| Category | Score |
|---|---|
| Pain | 6 |
| Urgency | 6 |
| ROI clarity | 5 (picks are driven by training priors, BD and ads, so attributing gains to fixes is weak) |
| Customer accessibility | 8 |
| Pilot speed | 9 |
| Market size | 6 |
| Expansion | 7 |
| Venture potential | 6 |
| Defensibility | 4 |
| Why now | 9 |
| Competition position | 3 |
| **Average** | **6.3** (round15 rough score was 7.0; the Lightsage discovery and free tooling lowered it) |

Eight categories are below 7. This fails the bar (8.5, with none below 7).

## 5 simulated buyers

| Buyer | Response | Why |
|---|---|---|
| Head of Growth, challenger transactional-email API (loses to Resend on TypeScript) | **MAYBE→YES** | Would pay $2-3K/month for 6 months to test fixes, but also gets a Lightsage demo and churns if picks don't move |
| DevRel lead, Series A dev-infra startup (Firecrawl-like) | **MAYBE** | Exactly Lightsage's customer profile; buys whichever is cheaper; budget under $20K/yr |
| VP Developer Marketing, PayPal-class enterprise | **MAYBE** | Commissions a one-off study (Amplifying or an agency), then pursues BD with Anthropic, OpenAI and Lovable and buys Sponsored placement; continuous SaaS is a hard sell |
| CTO, category leader (Supabase/Vercel-like) | **NO** | Already built its own evals (Supabase Evals, Netlify AXIS); wins by default |
| CMO, non-dev SaaS (HubSpot-like) | **NO** | Already pays Profound; asks Profound to add agent-selection tracking |

## Red team (the best case against my kill, and my reply)

- **"Lightsage is a 2-person seed; the category is open."** True: no one has scale, and Amplifying is research-led. But a third entrant with no dataset, no lab relationships and no customers starts behind three teams plus free OSS. Pain and competition are inversely correlated again (STATUS lesson #2).
- **"Integration success is the real wedge; selection is noise."** That points toward AX CI testing, which Armature Evals, AXIS, Speakeasy and Stainless/Anthropic already cover. It is feature-sized.
- **"Labs won't sell placement inside coding agents; developers would revolt."** Possible, but OpenAI already sells Sponsored Agents in ChatGPT, and plugin marketplaces are curated distribution. Even without ads, labs can ship a free "Claude Code vendor console".

## Lesson for STATUS.md
The strongest why-now in 15 rounds (agent-triggered deploys went from under 3% to over 50% in 2026) still lost to the round-1 rule: **when a phenomenon shows up in public studies (Feb and Sep 2026), a seed round follows within weeks** (Lightsage, Sep 8). Worse, the platform at the center (the labs) monetizes placement and gives measurement away free.

## Sources (search-result summaries; none opened, since WebFetch was blocked)
- Armature study: https://pinggy.io/blog/what_ai_coding_agents_pick_for_your_stack/ · https://mer.vin/news/what-17000-coding-agent-runs-reveal-about-tool-choices/ · https://zeli.app/story/49557206 · https://www.stackone.com/blog/coding-agents-tool-choice-disagree/
- Armature company: https://ycombinator.com/companies/armature · https://yctierlist.com/s26/armature/
- Amplifying: https://amplifying.ai/research/claude-code-picks · https://amplifying.ai/for-vendors · https://amplifying.ai/research/claude-code-hardcoded-vendors · https://s.amplifying.ai/research/codex-vs-claude-code-picks/report · https://amplifying.ai/coding-agents/npm
- Lightsage: https://thenextweb.com/news/lightsage-4m-nexus-agent-led-growth-coding-agents-eu-psd2-strong-customer-authentication · https://runtimewire.com/article/lightsage-raises-4m-ai-agent-growth-stack · https://hackernoon.com/lightsage-raises-$4m-led-by-nexus-to-build-the-growth-stack-for-ai-agents
- Supabase: https://www.implicator.ai/supabase-doubles-to-10-5-billion-as-agents-deploy-most-of-its-databases/ · https://runtimewire.com/article/supabase-launches-evals-ai-coding-agent-benchmark · https://sacra.com/research/supabase-170m-year-growing-221-yoy/
- Neon: https://www.databricks.com/blog/databricks-neon
- Vercel: https://startupfortune.com/guillermo-rauch-says-ai-agents-now-trigger-more-than-half-of-all-vercel-deployments/ · https://ecommercenews.co.nz/story/vercel-unveils-agent-tools-as-deployments-turn-ai-led
- Mintlify: https://mintlify.com/blog/state-of-docs-traffic
- Netlify AXIS: https://www.createwith.com/tool/netlify/updates/netlify-launches-axis-open-source-framework-to-measure-agent-experience-with-api · https://www.netlify.com/blog/how-we-measure-netlify-agent-experience.md
- Ora/Vercel: https://ora.ai/blog/is-agentic-with-vercel · https://www.ora.ai/methodology
- Profound: https://aiweekly.co/alerts/profound-hits-18b-on-180m-series-d-from-sequoia-kleiner · https://tryprofound.com/blog/claude-and-claude-code-are-distinct-answer-engines
- Scrunch AXP / Sitecore: https://scrunch.com/platform/agent-experience
- OpenAI Sponsored Agents: https://adlibrary.com/posts/chatgpt-sponsored-agents · https://ppc.land/openai-lets-advertisers-run-chatgpt-ads-from-hubspot-and-shopify/
- Stainless/Anthropic: https://uctoday.com/anthropic-acquires-stainless-the-sdk-and-mcp-startup-behind-every-official-claude-api-library · https://scalar.com/resources/stainless-wind-down
- Claude plugin marketplace: https://code.claude.com/docs/en/discover-plugins
- Context7: https://developertoolkit.ai/en/ecosystem/mcp/context7/
- Convex: https://www.unite.ai/convex-raises-57m-series-b-to-build-the-backend-for-agent-written-software/
- Lovable: https://automationatlas.io/tools/lovable/
- DevRel budgets: https://draft.dev/2026-developer-marketing-survey · https://www.slashdata.co/post/what-are-the-main-challenges-for-developer-programs
