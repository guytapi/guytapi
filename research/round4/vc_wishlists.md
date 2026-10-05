# Round 4: VC wishlist sweep (2025-2026)

Date: 2026-10-05. Method: collect publicly stated investor "requests", then crowding-check the best fits. Budget: 40 web searches. WebFetch was egress-blocked on every domain I tried (ycombinator.com, superframeworks, ibtimes, vccafe), so all content comes from search-result snippets and secondary write-ups of the primary posts.

**What the markers mean**
- **[V]**: the URL appeared in search results this session.
- **[unverified]**: from analyst memory. No URL was confirmed, and none is invented.
- **Crowding**: counts meaningfully funded startups (roughly a $3M+ round), with incumbents noted separately.
  - **Low**: 0-2 startups.
  - **Med**: 3-5 startups.
  - **High**: 6 or more, or a platform has already absorbed it.
- **Bar fit**: B2B, a path to $1B+, ACV of $50K+, a pilot within 90 days, a one-sentence VC pitch, no gov/defense/bank/insurance/regulated-healthcare buyer, not a cold-start marketplace, and not on our killed list.

## Primary source index

| Source | URL | Status |
|---|---|---|
| YC RFS (live page; holds Fall 2026) | https://www.ycombinator.com/rfs | [V], fetch blocked |
| YC Fall 2026, all 13 RFS (secondary) | https://modelence.com/yc-rfs-fall-2026 ; https://superframeworks.com/articles/yc-fall-2026-rfs-indie-hacker-plays ; https://explainx.ai/blog/yc-requests-for-startups-fall-2026 | [V] |
| YC Summer 2026, all 15 RFS (secondary) | https://thenextweb.com/news/yc-summer-2026-rfs-hard-tech-pivot ; https://www.vccafe.com/requests-for-startups-summer-2026-edition/ ; https://modelence.com/yc-rfs-summer-2026 | [V] |
| YC Spring 2026 RFS (secondary) | https://modelence.com/yc-rfs-spring-2026/ai-guidance-for-physical-work ; https://www.letsdatascience.com/news/yc-requests-ai-native-startups-across-industries-1c422935 | [V] |
| YC Spring/Summer 2025 RFS (secondary) | https://www.vccafe.com/extended-requests-for-startups-2025-list/ ; https://www.vccafe.com/requests-for-startups-2025-part-3/ | [V] |
| YC Fall 2025 RFS | none found; may not exist as a separate list | gap |
| a16z Big Ideas 2026 Part 1 / Part 2 | https://a16z.com/newsletter/big-ideas-2026-part-1/ ; https://a16z.com/newsletter/big-ideas-2026-part-2/ | [V] |
| a16z enterprise orchestration (podcast) | https://a16z.com/podcast/big-ideas-2026-the-enterprise-orchestration-layer/ | [V] |
| a16z speedrun "14 Big Ideas for 2026" | https://speedrun.substack.com/p/14-big-ideas-for-2026 | [V] |
| a16z American Dynamism ideas (secondary) | https://swipefile.com/4-big-bets-for-builders-in-2026 | [V] |
| Sequoia AI Ascent 2026 / services-as-software (secondary) | https://blog.innmind.com/sequoia-ai-ascent-2026-what-ai-founders-should-change-in-their-pitch-deck/ | [V] |
| Elad Gil: open markets and AI rollups | https://techcrunch.com/2025/11/03/elad-gil-on-which-ai-markets-have-winners-and-which-are-still-wide-open ; https://techcrunch.com/2025/06/01/early-ai-investor-elad-gil-finds-his-next-big-bet-ai-powered-rollups | [V] |
| Bessemer 2026 (healthcare AI breakout) | https://medcitynews.com/tag/healthcare-ai-2/ | [V] |
| Greylock $1.5B Fund 18 thesis | https://pulse2.com/greylock-raises-1-5-billion-for-greylock-18-to-back-ai-native-founders/amp/ | [V] |
| NFX, Lightspeed, General Catalyst, Accel, Index, Founders Fund, Conviction | no public 2026 "request list" found; only generic theses | gap |

**Finding:** YC and a16z are the only firms that publish idea-level wishlists. The other firms publish sector-level theses that are too broad to crowding-check.

## (a) Full wishlist table (49 ideas)

| # | Source | Idea | Bar fit | Crowding | Named competitors / notes |
|---|---|---|---|---|---|
| 1 | YC F26 (Gaddipati) | Self-Maintaining APIs: agents open PRs in customer repos when an API ships breaking changes | Y (borderline $1B) | **Low** | No direct funded startup found. Adjacent: Moderne ($30M B Feb-2025, $50M total; already does vendor-side upgrade recipes, e.g. Micronaut) [V techcrunch.com/2025/02/11/moderne-raises-30m-to-solve-technical-debt-across-complex-codebases/ ; devops.com/micronaut-taps-moderne-to-automate-java-framework-updates/]; Speakeasy ($15M A) and Stainless automate SDK version PRs [V]; vendor DIY agent "migration skills" (LaunchDarkly, Google Gemini) [V] |
| 2 | YC F26 (Goel) | AI-Native Compliance Infrastructure (financial) | N (bank/fin buyer) | High | Many RegTech players; excluded by bar |
| 3 | YC F26 (Tindle/Hu) | Data for the Real World: dense physical data for energy, ag, logistics, construction | Partial (capex-heavy) | Med | Noetive ($41M, Sep-2026), Archetype AI ($13M seed), NavVis ($85M D, Aug-2026) [V] |
| 4 | YC F26 (Warren) | New OS for the Physical World: coordinate agents, robots and wearable-equipped humans in field ops | Partial (overlaps killed robot-fleet ops) | Med | Overlaps killed thesis; [V modelence.com/yc-rfs-fall-2026/new-operating-systems-for-the-physical-world] |
| 5 | YC F26 (Epstein) | Multiplayer AI | N (platform absorption) | High | Slack, Notion, Microsoft, OpenAI team features |
| 6 | YC F26 (Koomen) | A Cloud for Small Software | N (low ACV) | Med | Vercel, Replit, Supabase |
| 7 | YC F26 (Kolysh) | Proving You're Human (B2B angle: hiring fraud) | N (absorbed) | High | Deel bought Clarity ($45-50M, Aug-2026); Zoom+BrightHire [V thenextweb.com/news/deel-acquires-clarity-deepfake-detection] |
| 8 | YC F26 (Chaubard) | Compute at Sea | N (capex) | Low | n/a |
| 9 | YC F26 | The Primer (education) | N | n/a | n/a |
| 10 | YC F26 (Driscoll) | Future of American Defense | N (defense) | n/a | n/a |
| 11 | YC F26 | AI consumer products for 1B people | N (consumer) | n/a | n/a |
| 12 | YC F26 | AI for the Aging Population | N (consumer/health) | n/a | n/a |
| 13 | YC F26 | Crypto | N | n/a | n/a |
| 14 | YC S26 (Dessaigne) | Hardware Supply Chain / "Supply Chain 2.0 for Semiconductors": tier-n visibility, packaging/OSAT, export compliance, faster hardware iteration | **Y** | **Low-Med** | Startups: Tradeverifyd (funding unknown), Cofactr ($17M A, sourcing), 1Buy.AI ($3.9M seed, India), Enmovil ($6M A, generic) [V]. Incumbents: Resilinc, Interos, Everstream, Strider [V/unverified] |
| 15 | YC S26 (Friedman) | SaaS Challengers: ERP | Y | High | Rillet, Campfire, Doss and others [unverified] |
| 16 | YC S26 | SaaS Challengers: industrial control systems / PLC | Y | High | Gigaton ($26M A, Jun-2026), PLCs.ai, PLC Copilot, Nexus Intelligence (seeds 2026) [V] |
| 17 | YC S26 | SaaS Challengers: chip design (EDA) | Y | High | ChipAgents, Cognichip, others [unverified] |
| 18 | YC S26 | SaaS Challengers: supply chain management | Y | High | Lyric, Auger, Didero [unverified] |
| 19 | YC S26 (Blomfield) | Company Brain | Y | High | Glean, Hyper, GBrain [V colrows.com/blogs/yc-company-brain-rfs/] |
| 20 | YC S26 (Hu) | AI Operating System for Companies | Y | High | Same set as Company Brain plus platforms |
| 21 | YC S26 (Epstein) | Software for Agents | Killed | High | On our killed list |
| 22 | YC S26 (Arora/Flora) | Selling to Huge Companies | Meta (a go-to-market thesis, not an idea) | n/a | n/a |
| 23 | YC S26 (Gupta) | Dynamic Software Interfaces (generative UI) | Partial | Med-High | Thesys, Vercel v0 [unverified] |
| 24 | YC S26 (Alstromer) | AI-Native Service Companies | Partial (services, not software) | High | n/a |
| 25 | YC S26 (Xu) | AI-Native Discovery Engines (closed-loop verification against the live web) | Unclear | Med | Perplexity, Exa [unverified] |
| 26 | YC S26 (Hu) | Inference chips for agent workflows | N (capex) | Med | Groq, Etched, others |
| 27 | YC S26 | Low-pesticide ag robots; counter-swarm defense; electronics in space; industrial space; AI personalized medicine | N | n/a | n/a |
| 28 | YC Sp26 | Cursor for Product Managers | Y | High | Many PM-AI tools [unverified] |
| 29 | YC Sp26 | AI Guidance for Physical Work (real-time multimodal coaching for frontline workers) | Y | Med | TechSee, GIDR.ai, Augmentir, Strivr, RealWear ecosystem [V partial] |
| 30 | YC Sp26 | Modern Metal Mills | N (capex) | Low | n/a |
| 31 | YC Sp26 | Large Spatial Models | N (lab-scale) | Med | World Labs and others |
| 32 | YC Sp26 | AI-native hedge funds / agencies; stablecoin financial services; AI for government | N | n/a | n/a |
| 33 | YC Sp25 | Compliance and audit automation | Partial (audit is regulated-adjacent) | High | Fieldguide and others [unverified] |
| 34 | YC Sp25 | Browser / computer-use automation | Y | High | Browserbase and others; platform-native agents |
| 35 | YC Sp25 | B2A: software whose customers are agents | Killed | High | n/a |
| 36 | YC Sp25 | AI personal staff / assistants | N (consumer) | High | n/a |
| 37 | YC Su25 | Full-stack AI companies; design founders; Voice AI | Partial / High | High | Voice AI is very crowded |
| 38 | a16z (J. Li) | Structuring and governing multimodal enterprise data for agents | Y | High | Reducto, Unstructured, Extend [unverified] |
| 39 | a16z (Aubakirova) | Infra for "agent-speed" bursty workloads that systems mistake for attacks | Near killed (agent auth/metering) | Med | Cloudflare, bot management |
| 40 | a16z (Cui) | AI-native data stack (vector + semantic context layer) | Y | High | Many |
| 41 | a16z (S. Wang) | Systems of record lose primacy: autonomous ITSM/CRM workflow engines | Y | High | ServiceNow, Salesforce, many startups |
| 42 | a16z (Immerman) | Multi-party agent collaboration in vertical industries | Y | Med (varies by vertical) | Vertical-specific |
| 43 | a16z (enterprise) | Multi-agent orchestration layer for the Fortune 500 | Killed-adjacent (governance) | High | n/a |
| 44 | a16z (AD) | AI-native manufacturing: design lines, schedules and safety before metal moves | **Y** | **Low (startups); High (incumbents)** | Factorymaker (€1.1M pre-seed); incumbents Dassault DELMIA, Siemens, NVIDIA Omniverse, Autodesk; full-stack factory builders Foundational ($25M seed), 1872 ($15M), Isembard ($50M) [V] |
| 45 | a16z (AD) | Electro-industrial stack; physical perception layer; autonomous labs | N / Partial (capex) | Med | n/a |
| 46 | a16z | Voice agents in high-stakes, regulated workflows | Partial | High | n/a |
| 47 | a16z speedrun | AI-native marketplaces that work for the buyer; "agent of my tastes" | N (marketplace/consumer) | n/a | n/a |
| 48 | Sequoia | Services-as-software; long-horizon agents | Partial (meta) | High | n/a |
| 49 | Elad Gil / General Catalyst | AI-enabled rollups | N (not a product) | High | n/a |

**Crowding check, verified:** 7 of the B2B-fit ideas are High or already absorbed by a platform: Company Brain, ICS/PLC, CAM-adjacent (CloudNC raised $20M in Sep-2026, [V]), hiring-fraud detection, ERP, multimodal data and voice. Only 3 fit ideas came out Low: #1, #14 and #44.

## (b) Top 5 under-served ideas

### 1. Supply-chain intelligence for AI hardware (YC S26 "Hardware Supply Chain")
- **Pitch:** "Tier-n visibility and allocation intelligence for the AI hardware supply chain (HBM, CoWoS/advanced packaging, substrates, OSAT), so chip and server companies see a shortage 2 quarters before it hits."
- **Buyer:**
  - VP Supply Chain or Strategic Sourcing at fabless chip companies, AI server OEMs/ODMs, EMS providers and neoclouds.
  - Commercial buyers, not government.
- **Buyers x ACV:**
  - Core: about 600 companies (fabless/IDM, AI hardware OEM/ODM, neoclouds) x $250K = **$150M**.
  - Expansion: about 5,000 electronics OEMs x $100K = **$500M**.
  - The $1B path needs a procurement/transaction layer on top (allocation hedging, broker-of-last-resort).
- **Why now:**
  - AI capex supercycle.
  - Shortages in HBM and advanced packaging.
  - Export controls on AI chips are tightening.
  - Tariffs.
  - Only 17.7% of companies report high confidence in their Tier 2-3 visibility (Tradeverifyd survey [V]).
- **Kill risk:**
  - Resilinc, Interos and Everstream could bolt on AI.
  - Suppliers may refuse to share data.
  - Cofactr could move up-market.
  - Tradeverifyd's funding is unknown; check it before the war room.

### 2. Self-Maintaining APIs, paid for by the provider (YC F26)
- **Pitch:** "API vendors pay us to auto-migrate their customers off deprecated versions: our agents open tested PRs in integrator repos, so a breaking change no longer means 18 months of version sprawl."
- **Buyer:**
  - Head of Developer Experience or API Platform at API-first companies (payments, comms, devtools, SaaS platforms).
  - Second wedge: Fortune 2000 platform teams changing internal service contracts.
- **Buyers x ACV:**
  - About 3,000 public-API companies with 1,000+ integrators x $80K = **$240M**.
  - Plus about 2,000 enterprises x $200K for internal API contracts = **$400M**.
  - A $1B outcome is plausible only if this becomes the "API change-management system of record". **Weakest $1B case of the five.**
- **Why now:**
  - Coding agents can now produce mergeable PRs.
  - API surface is exploding because of agent integrations.
  - Vendors are already hand-writing agent "migration skills", which shows the demand is real.
- **Kill risk:**
  - **High.**
  - Moderne ($50M raised) already sells vendor-side upgrade recipes.
  - Stainless and Speakeasy own SDK generation and could add this.
  - GitHub Copilot or Claude Code could make it a free feature.
  - Integrators may resist giving repo access.
  - Also sits close to our killed "autonomous code merge" thesis.

### 3. AI-native factory and line planning (a16z AD "design before metal moves")
- **Pitch:** "Generative design for new production lines: from a product spec, produce a validated layout, takt/throughput simulation, robot cells and staffing plan in days instead of 6 months of consultants."
- **Buyer:**
  - VP Manufacturing Engineering or Advanced Manufacturing at OEMs building or retooling plants (batteries, data-center hardware, auto, industrial).
  - Also EPC and integrator firms.
- **Buyers x ACV:**
  - About 3,000 US/EU manufacturers with active line or plant projects x $150K/year = **$450M**.
  - Per-project fees of $250K-1M on greenfield plants add upside.
  - The $1B path is to become the planning system that hands off to MES and commissioning.
- **Why now:**
  - The reshoring wave.
  - Dassault and NVIDIA "industry world models" (Feb-2026) show the tech is ready, but incumbent tools still need expert operators.
  - BMW Debrecen proved full virtual design works [V].
  - A brownfield line-rebalancing pilot fits in 90 days.
- **Kill risk:**
  - Siemens, Dassault and Autodesk bundle AI into their tools.
  - Revenue is project-based and lumpy.
  - Adjacent to our killed "AI infra commissioning" thesis; position upstream at design, not commissioning.
  - Full-stack builders (Foundational, 1872, Isembard) may keep this capability in-house.

### 4. Export-control and deemed-export compliance for AI and chip companies (carved out of YC S26 hardware supply chain)
- **Pitch:** "Continuous ECCN classification, end-user screening and deemed-export tracking for chip, AI-hardware and model companies, so trade compliance keeps up with monthly rule changes."
- **Buyer:**
  - Head of Trade Compliance or GC at semiconductor, AI-infra and frontier-model companies.
  - These are commercial buyers; the regulator is not the buyer.
- **Buyers x ACV:** about 1,500 companies x $120K = **$180M** core; the market expands as controls widen to models and compute.
- **Why now:** US/UK AI-chip controls tightened in 2026 and compliance now requires "proving who accessed what, when" [V tradeverifyd.com].
- **Kill risk:**
  - Crowding is **unverified**: the 2025-26 tariff wave funded many trade-compliance startups.
  - Incumbents: Descartes, Thomson Reuters ONESOURCE.
  - Arguably regulated-adjacent.
  - Needs one more crowding search before the war room.

### 5. AI guidance for physical work in industrial maintenance (YC Sp26)
- **Pitch:** "A real-time multimodal copilot that lets a 2-year technician fix equipment like a 20-year veteran, via phone or glasses, trained on the plant's own manuals and work orders."
- **Buyer:** VP Maintenance or Reliability at manufacturers, utilities-adjacent industrials, mining and data-center operators.
- **Buyers x ACV:** about 10,000 mid-to-large industrial sites x $60K = **$600M**.
- **Why now:**
  - Skilled-trade retirement wave.
  - Real-time vision and voice models have become cheap.
  - Reported improvements: +25% first-time-fix and -32% procedural errors with AR workflows [V oxmaint, vendor claim].
- **Kill risk:**
  - Crowding is **Medium** and the bar requires 2 or fewer funded startups: TechSee, Augmentir, GIDR.ai, Strivr, plus Tractian and MaintainX adding copilots.
  - Included only as a benchmark; likely a kill.

## Bottom line

VC wishlists in 2026 have moved to hard tech and capex-heavy ideas. Most software-shaped requests are already crowded because founders also read these lists. The three ideas that cleared both the bar and the crowding check (#1 AI-hardware supply chain, #3 factory planning and the narrower #2 self-maintaining APIs) all sell to **physical or hardware industries, or to API vendors**, not into general "AI agent tooling". Ranked by fit to the bar: **#1 > #3 > #2**. #4 needs one more crowding check; #5 is probably a kill.
