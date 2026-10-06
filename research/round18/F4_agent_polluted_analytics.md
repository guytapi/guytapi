# F4 — Agent-polluted product analytics (Thesis #9)

**Thesis:** "Half your 'users' are now AI agents, and your product analytics can't tell. We separate humans from agents in every funnel, A/B test and attribution report."
**Date:** 2026-10-06 | **Searches:** 37 of 40 (WebFetch/Reddit blocked; evidence is from search snippets) | **Legend:** [S] source seen in results, [U] unverified/estimate, [I] inference.

## VERDICT: KILL (F1 platform absorption + F2 visible-pain race). Average 5.2; 7 of 11 categories score below 7.

**Why, in three points:**
1. **The pain is real but sits in marketing, not product.** "Half your users" is wrong for logged-in product analytics. HUMAN measured that 77% of agentic activity hits product/search pages. Only 6.4% hits account pages, 7% authentication and about 2.3% checkout [S]. The distortion falls on top-of-funnel web, CRO and paid attribution. That is the marketing-analytics buyer, which DataDome, HUMAN and Snowplow already sell to.
2. **The exact pitch has already shipped, mostly in the last 8 months.** Snowplow's landing page is titled "Half Your Traffic Isn't" and offers behavioral human-vs-agent detection, including handoffs inside one session (preview Feb 2026). Contentsquare added human-vs-AI visitor segmentation (Mar 17 2026). PostHog has bot/AI-agent classification and a Bots tab. HUMAN pushes Agentic Visibility into Adobe Experience Platform for marketers. Google Cloud Fraud Defense (reCAPTCHA) has an Agent overview dashboard. Fingerprint offers signed-agent detection plus AI Assistant Detection (Jun 2026). Vouched AgentShield sells "preserve the integrity of your analytics". Statsig and Optimizely filter bots by default. YC S26 has funded agent-experience analytics (Armature, Scope).
3. **Detecting the largest agents is becoming a protocol checkbox.** OpenAI, Anthropic and Perplexity sign requests with Web Bot Auth [S]. Any analytics vendor or CDN can verify a signature in a sprint. What is left is unsigned local agentic browsers, which need behavioral biometrics. That is Vara's real edge, but HUMAN, DataDome, Snowplow, Fingerprint and cside all already claim behavioral detection.

---

## 1. Evidence that agent traffic distorts metrics (2026)

| # | Signal | Source |
|---|---|---|
| 1 | Cloudflare Radar: automated traffic is 57.5% of HTML requests vs 42.5% human, the first crossover (Jun 2026) | [S] blog.cloudflare.com/signed-agents ; peakhour.io/blog/protecting-ab-testing-from-bots |
| 2 | HUMAN 2026 benchmark: agentic traffic +7,851% YoY. Browser agents (Comet 47%, Atlas 20.3%) are about 71% of agent activity. Only 8.8%/5% of agent activity hits account/auth pages (2025); Jul 2026 shares are 6.4% account, 7% auth (rising) | [S] humansecurity.com 2026 report; state-of-agentic-traffic July 2026 blog |
| 3 | Atlas, Comet and Claude for Chrome present a standard Chrome UA, so UA/IAB-list filtering misses them. This is how GA4, Amplitude, Statsig and Optimizely filter | [S] mediacat.uk; alhena.ai denominator-drift; amplitude.com/docs/data/block-bot-traffic; statsig.com/blog/guide-online-bot-filtering |
| 4 | Statsig: bots can be "0% to 50% of raw exposures depending on the company" | [S] statsig.com FAQ |
| 5 | Practitioner framing: "denominator drift" (the conversion-rate denominator fills with machines). Separately, "AI agents are breaking web analytics in a way nobody is solving" argues it is a category problem: the agent is real demand | [S] alhena.ai/blog/denominator-drift-ai-agents-conversion-rate ; leoanalysis.substack.com |
| 6 | Paid media: Atlas clicks on sponsored links are billed as human (Search Atlas CEO quote). 85.6% of marketers are worried about agentic invalid traffic | [S] searchatlas.com news; webtonic.io click-fraud stats |
| 7 | Product analytics as a distinct problem: "Agent as User: why your product analytics break when bots become your power users" (May 2026). Agents using MCP/APIs never fire activation milestones | [S] tianpan.co blog; userpilot (snippet) |
| 8 | Counter-signal: AI-referred traffic converts 42% better than organic (Mar 2026). Agents pre-filter by intent, so blindly excluding them deletes real demand | [S] webtonic.io / retail reports |

**What is missing:** I found no practitioner case of a *product* team (logged-in SaaS) shipping a wrong decision because agents polluted an A/B test. I also found no sourced share of logged-in sessions driven by agents [U]. The loud evidence comes from vendors (HUMAN, Snowplow, DataDome) and marketing/SEO writers.

## 2. Competitors

| Layer | Players and what shipped | Threat |
|---|---|---|
| Analytics/CDP vendors | **Snowplow** AI agent detection: behavioral, splits human and agent inside one session, runs on Snowflake, and its page is literally titled "Half Your Traffic Isn't" [S]. **Contentsquare** LLM/agent traffic analytics, human vs AI (Mar 2026) [S]. **PostHog** bot/AI agent classification plus Bots tab ("brand new") [S]. **Microsoft Clarity** bot detection plus AI Bot Activity report [S]. **GA4** AI Assistant channel (May 2026, referral-based) [S]. **Amplitude** IAB UA block filter only [S]. **Pendo** Agent Analytics (measures your own agents) [S] | Critical. The exact pitch exists, sold by the system of record |
| Experimentation | **Statsig** (OpenAI) bot filtering on by default; **Optimizely** IAB filtering; LaunchDarkly unclear [S] | High. One release from agent-aware filtering, and Statsig's owner signs its own agent traffic |
| Bot/agent trust | **HUMAN** Agentic Visibility for marketing teams, Adobe partner [S]. **DataDome** lists "marketing analytics assurance" as a use case, Forrester Leader [S]. **Fingerprint** Authorized AI Agent Detection (Feb 2026) plus AI Assistant Detection/Automation Intelligence API (Jun 2026) [S]. **Google Cloud Fraud Defense** Agent overview [S]. **Cloudflare** signed agents/Radar [S]. **cside** [S]. Castle (not searched) | Critical. Behavioral plus network moat already at scale |
| Agent analytics startups | **Vouched AgentShield** (analytics integrity; $17M A) [S]. **Known Agents** (ex-Dark Visitors, client+server agent analytics, free tier) [S]. **Profound/Scrunch** agent analytics via CDN (AEO) [S]. **SonicLinker** [S]. YC S26 **Armature** (AX product analytics), **Scope** [S, from snippet]. Lightsage (earlier round) | High, and crowded on the "agent funnel" angle |

## 3. Will analytics vendors absorb it?
**Yes, and they mostly have.** Three tiers:
- **Self-declared bots:** a UA list. Every vendor already has this.
- **Signed agents (Web Bot Auth: ChatGPT agent, Claude, Perplexity, Browserbase):** signature verification. A sprint for any vendor. Cloudflare, Fingerprint and Google already offer it.
- **Unsigned agentic browsers and stealth automation:** this genuinely needs client-side behavioral signals (mouse, scroll, keystroke cadence) and ideally a cross-site network.
  - It is structurally hard for *product-analytics* vendors. Amplitude and Mixpanel do not collect pointer-level telemetry at that granularity; session-replay vendors (Contentsquare, PostHog, Clarity) do.
  - It is *not* hard for bot-management vendors (HUMAN reports "one quadrillion interactions"; DataDome reports 17.7B agent requests per quarter) or for Snowplow (2M+ sites, 1T+ events/month) [S].
  - The cross-site fingerprint network already exists in the hands of companies 100-1,000x Vara's scale.

**Conflict check (§4.4 of the taxonomy):** analytics vendors have no reason *not* to act. Cleaner data is their value proposition, and "agent analytics" is upsell. Statsig belongs to OpenAI, which signs its own agent, so the hardest segment for OpenAI-owned Statsig is competitors' agents. That is not a reason they would refuse.

## 4. Market math
- **Buyers:** Amplitude reports roughly 4,000+ paying customers; Mixpanel, PostHog and Heap/Contentsquare together reach tens of thousands. Companies with a real experimentation program number about 5,000-15,000 [U].
- **ACV:** as a data-quality add-on, about $10-50K. Snowplow/HUMAN enterprise deals run higher [U]. Buyers expect it bundled.
- **$10M ARR** ≈ 300 customers × $33K. Possible as a niche in e-commerce/marketplaces.
- **$100M ARR** ≈ 3,000 × $33K, against bundled features from their own analytics vendor plus HUMAN/DataDome. Not credible.
- **$10B:** no path as an analytics company. The only $10B story is "agent trust layer", which belongs to HUMAN, Cloudflare and Persona (see round 12, Z).

## 5. Finalist format (filled for the record)
- **One-line problem:** agent sessions inflate denominators and contaminate experiments and attribution, and UA-based filters miss agentic browsers.
- **Why now:** browser agents (Comet, Atlas, Claude for Chrome) went mainstream in 2025-26 and present as Chrome. Automation passed 50% of HTML traffic in 2026.
- **Exact buyer:** Head of Growth/CRO or Director of Analytics. In practice it is the marketing-analytics owner, not the CPO.
- **Exact ICP:** e-commerce, travel and marketplaces with more than $50M GMV running 20+ experiments a quarter on high-traffic PDP/search pages.
- **Current workaround:** IAB UA lists (GA4, Amplitude, Statsig, Optimizely), PostHog HogQL bot classification, bot-management dashboards (HUMAN/DataDome), manual "spike with flat conversions" detective work.
- **Why incumbents cannot easily own it:** *they can.* Signed agents are a protocol, behavioral signals already sit with Snowplow, HUMAN, DataDome and Fingerprint, and analytics vendors are motivated to ship it.
- **30-day MVP:** JS SDK (Vara behavioral collector) that tags each session/event `human | signed_agent:<operator> | suspected_agent | handoff`. It pushes the tag as a user/event property into Amplitude, Mixpanel, PostHog, GA4, Statsig and Optimizely, plus a "re-read your last 10 experiments without agents" report.
- **Pilot design:** 14-day shadow tag on 2-3 e-commerce sites; re-run the last quarter's A/B tests excluding agent sessions. Success = at least 1 experiment whose winner flips or whose lift changes by more than 30%.
- **Pricing hypothesis:** $1-3 CPM tagged sessions, or a $20-60K/yr platform fee [U].
- **Expansion path:** agent-funnel analytics (what agents do and where they fail), agent-specific experiences, ad invalid-traffic refunds, then agent trust/blocking.
- **Moat:** weak. A behavioral model plus a cross-customer agent-fingerprint library, but incumbents' networks are orders of magnitude larger.
- **Why $10B+:** it would not be. See §4.
- **Direct competitors / adjacent threats:** Snowplow, Contentsquare, PostHog, HUMAN, DataDome, Fingerprint, Vouched AgentShield, Known Agents, cside, Google Fraud Defense, Cloudflare; Statsig/Optimizely/GA4 one release away.
- **One sentence to a CPO:** "UA filters miss every Comet, Atlas and Claude-for-Chrome session, so we tag each session human or agent at the SDK level and re-score your experiments; last quarter X% of your test exposures were agents." Likely reply: "Snowplow/HUMAN/PostHog already show me that."
- **5 discovery questions:**
  1. Have you ever reversed or doubted an experiment result because of bot or agent traffic? Which one, and what did it cost?
  2. What share of your logged-in (not marketing-page) sessions do you believe are agents, and how do you know?
  3. Who owns data quality for experiments, and has that person bought a tool for it?
  4. Have you looked at agent features from your analytics, experimentation or bot vendor? Why are they insufficient?
  5. Would you pay separately for this, or do you expect it inside Amplitude, Statsig or HUMAN?
- **Hard kill criteria:** already met. A system of record (Snowplow/Contentsquare/PostHog) ships behavioral human-vs-agent segmentation, *and* the largest agents sign via Web Bot Auth, *and* there is no evidence of logged-in product distortion above about 7%.

## 6. Scores (bar: avg ≥8.5, none <7)

| Category | Score | Why |
|---|---|---|
| Pain | 5 | Real for CRO/marketing, unproven for logged-in product |
| Urgency | 5 | "Spikes with flat conversions" is an annoyance, not a fire |
| ROI clarity | 4 | Hard to put a dollar value on "cleaner data"; ad-fraud refunds are clearer but crowded (CHEQ, ClickCease, Lunio) |
| Customer accessibility | 6 | Growth/analytics leads are reachable, and an SDK install is easy |
| Pilot speed | 8 | Shadow tag plus experiment re-read in 14 days |
| Market size | 6 | Large in theory, bundled in practice |
| Expansion | 6 | Agent funnels and agent experience, which YC S26 is also attacking |
| Venture potential | 4 | Feature, not company |
| Defensibility | 3 | Protocol plus incumbent networks |
| Why now | 8 | Genuinely new behavior in 2025-26 |
| Competition position | 2 | Snowplow uses the identical pitch; 10+ others |
| **Average** | **5.2** | |

## 7. Red team (strongest case for keeping it alive)
- Product-analytics leaders (Amplitude, Mixpanel) have *not* shipped behavioral agent detection; Amplitude still uses the IAB UA list [S]. A Vara SDK that writes a property into those tools could ride their ecosystems.
- Mixed human/agent sessions (a human hands off to Comet mid-checkout) break session-level filtering, and that needs biometrics. Vara has them.
- **Rebuttal:** Snowplow already markets in-session handoff detection [S], and Amplitude can partner with HUMAN/Fingerprint (HUMAN already partners with Adobe). It also fails taxonomy §4.1 (a visibility layer the platform is not prevented from shipping) and §4.2 (3+ public complaints, with funded startups present).

**Salvage note (not a finalist):** Vara's behavioral SDK is better positioned as a *signal supplier* (OEM into an analytics/experimentation vendor or a bot vendor) than as a standalone analytics company. Test: 3 BD conversations (PostHog, Statsig, Amplitude partnerships) asking whether they would license an "unsigned agentic-browser" classifier.

### Sources (from search results; none fetched)
blog.cloudflare.com/signed-agents ; humansecurity.com (2026 benchmark PDF; state-of-agentic-traffic April/June/July 2026; agentic-visibility blog; newsroom marketing release; chatgpt-atlas-vs-perplexity-comet) ; peakhour.io/blog/protecting-ab-testing-from-bots ; alhena.ai/blog/denominator-drift-ai-agents-conversion-rate/ ; leoanalysis.substack.com/p/ai-agents-are-breaking-web-analytics ; tianpan.co/blog/2026-05-06-agent-as-user-product-analytics-bot-consumers ; mediacat.uk (Atlas breaks analytics) ; searchatlas.com/news/what-chatgpt-atlas-means-for-marketers-and-businesses/ ; posthog.com/docs/web-analytics/bot-detection ; amplitude.com/docs/data/block-bot-traffic ; statsig.com/blog/guide-online-bot-filtering ; statsig.com/faq/prevent-statsig-experiment-bots ; docs.developers.optimizely.com/full-stack/docs/manage-bot-filtering ; snowplow.io/ai-agent-detection-preview ; snowplow.io/blog/how-to-detect-bots-and-ai-agent-traffic ; contentsquare.com/press/new-ai-agent-and-analytics-capabilities/ ; clarity.microsoft.com/blog/ai-bot-activity-in-clarity/ ; delante.co/ga4-adds-a-ai-assistant-channel-what-it-changes/ ; docs.cloud.google.com/recaptcha/docs/monitor-agents ; businesswire.com (Fingerprint 2026-02-03 and 2026-06-01 releases) ; fingerprint.com/blog/product-roundup-ai-detection-smart-signals/ ; techintelpro.com (DataDome agentic traffic report) ; vouched.id/learn/blog/vouched-agentshield-ai ; cside.com/en/solutions/ai-agent-detection ; darkvisitors.com/docs/analytics ; tryprofound.com/blog/scrunch-ai-review ; scrunch.com/faqs ; soniclinker.com/blog ; neuronfeed.com/startups/scope ; webtonic.io/blog/click-fraud-statistics ; guptadeepak.com/guides/verify-an-ai-agent/. Armature (YC S26) appeared only in a search summary: treat as [U].
