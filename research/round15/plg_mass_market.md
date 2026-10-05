# Round 15: product-led, self-serve B2B utilities built on new AI behaviors

Date: 2026-10-05 · Searches used: 31 of 35 · Lens: tools priced at $2K-$30K/yr, sold bottom-up to tens or hundreds of thousands of teams, used daily, with a viral loop, built on behavior AI created in 2025-2026.

## Verdict up front
**Nothing clears the bar.** The two best ideas average **7.0** and **7.1** on the original 11 categories, and both score below 7 in at least one category: Competition (5 and 3) and Defensibility (6 and 4).
The PLG lens repeats lesson #1 in STATUS.md, only faster. When an AI-created behavior shows up as a self-serve utility gap, one of three things happens within one or two quarters:
- a YC company ships it (AgentMail, AgentPhone, Skillsync, Vybe);
- the platform builds it in (Lovable commenting, Jam MCP, Microsoft Teams bot detection, Greenhouse Real Talent, Retell branded caller ID, Calendly/Cal.com agent APIs);
- the GEO/observability vendors add it as a module (Otterly Agent Analytics).

PLG utilities have a structural problem here: whatever can be adopted bottom-up in minutes, a platform can also ship in a sprint. That is why Defensibility is the category that usually fails.

## Candidate table (21 scanned)

| # | Utility (new AI behavior it rides) | Viral loop | Who owns it already (evidence) | Avg (orig. bar, rough) | Kill reason |
|---|---|---|---|---|---|
| 1 | Email inboxes for agents (agents email for users) | Each agent email reaches a new recipient | AgentMail: $6M seed led by General Catalyst (Mar 2026), 500+ B2B customers, hundreds of thousands of agent users | 4.5 | Breakout already exists |
| 2 | Phone numbers / SMS / iMessage for agents | Same as above | AgentPhone (YC P26, 100+ companies, Replit/LangChain), AgentCall | 4.5 | YC company in the 2026 batch |
| 3 | Shared coding-agent sessions ("GitHub for agent sessions") | Session links shared in PRs and Slack | Skillsync (YC W26), Entire (Dohmke), claude-replay, Simon Willison's open-source transcripts tool | 5.0 | Crowded; open-source substitutes |
| 4 | Team registry for agent skills, CLAUDE.md and AGENTS.md | Skills shared across a team | Tessl ($125M raised; 3,000+ skills), TrueFoundry Skills Registry, native plugin marketplaces | 4.8 | Funded leader plus native features |
| 5 | Analytics for AI-agent traffic to websites (agents are 57.5% of HTML traffic) | Benchmarks | Otterly Agent Analytics (Aug 13 2026), Siteline (#1 Product Hunt, Feb 2026), Salespeak free tool, Cloudflare Radar | 5.2 | GEO vendors added it as a module |
| 6 | Stakeholder feedback on AI-built prototypes | Reviewers join through comment links | Lovable in-app commenting (native) | 4.5 | Platform feature |
| 7 | Detecting deepfake job candidates | Weak | Deel bought Clarity ($45-50M); Pindrop Pulse; Reality Defender; InCruiter | 5.0 | Absorbed by HR platforms |
| 8 | **Share button for internal tools built with Claude Code or Lovable** | **Every shared link brings in a coworker, who then builds their own** | Luo, Vybe (YC), Lovable on Microsoft tenants, Replit, Retool, Vercel, and the AI labs' own sharing of published pages | **7.1** | Competition 3; platform risk (see deep dive B) |
| 9 | Product analytics for MCP servers (every SaaS ships an MCP server) | Weak | AgentCat (formerly MCPcat), mcpeye (open source), Datadog/Sentry | 5.0 | Small; feature-sized |
| 10 | Bug capture that coding agents can read | Bug links | Jam MCP (Chrome extension feeding Claude Code/Cursor) | 4.0 | Owned |
| 11 | Brand context MCP (on-brand AI content) | Weak | Frontify MCP, brandkit-mcp (open source), @brandsystem/mcp | 4.5 | Frontify, plus open source |
| 12 | Governance for meeting notetaker bots | Weak | Microsoft Teams bot detection on by default (2026); Zoom waiting rooms | 3.8 | Platform absorbed it |
| 13 | Filtering AI auto-apply applicants (242 applications per opening) | Weak | Greenhouse Real Talent with CLEAR; other ATS natives | 4.5 | ATS absorbed it |
| 14 | QA agent for vibe-coded apps | Report links | TestSprite ($6.7M; 35K developers), Momentic, QA Wolf | 5.0 | Funded; crowded |
| 15 | Branded caller ID for outbound AI voice agents | None | Retell ships it natively; Hiya/Numeracle/First Orion | 4.3 | Native to voice platforms |
| 16 | Self-serve tooling for ChatGPT ads (Ads Manager since May 5 2026) | Weak | OpenAI Ads Manager plus partners (Adobe, Criteo, Pacvue, StackAdapt) and holding companies | 5.0 | Adtech incumbents moved on day one |
| 17 | Citation and claim verification for client deliverables ("vibe citing") | "Verified" badge on deliverables | GPTZero Hallucination Check, CitateGenie (Word add-in), TrueCite, CiteSentinel, Manupatra, Superhuman (Grammarly) fact-check | 6.5 | Fragmented, but Superhuman/Copilot are a feature away; low venture ceiling |
| 18 | **Agent pick rate for dev tools ("Search Console for coding agents")** | **Public leaderboards and badges; competitors see each other** | Amplifying (vendor intelligence), Armature ($500K seed; services from $5K/mo), Netlify AXIS (open source), Ora | **7.0** | Competition 5, Defensibility 6 (see deep dive A) |
| 19 | AX (agent-experience) score for APIs and docs | Badges | Netlify AXIS (free, MIT), Ora (10,851 sites scanned), Mintlify | 5.5 | Merged into #18 |
| 20 | Security scanner for vibe-coded apps (39% of Supabase-backed AI apps leak data) | Free scan, then share | Vibesecur (free), VibeAppScanner, Symbiotic, Aikido, Lovable native scan | 5.0 | Free tools plus native scans |
| 21 | "Calendly for agents" (agents book meetings) | Booking links | Calendly and Cal.com scheduling APIs; Chatbase/Dialpad/ElevenLabs integrations | 3.5 | Incumbents own it |

---

## Deep dive A: Agent Pick Rate, a "Search Console for coding agents"

**VC sentence:** Coding agents now choose the stack (Claude Code picks Stripe 91% of the time and Vercel 100% of the time for JS projects), so every dev-tool company needs to measure and raise how often agents pick it and integrate it successfully, the way it once did for SEO.

**Problem.** Coding agents install packages, write imports and commit code, so the tool an agent picks is the tool that ships. Dev-tool vendors cannot see this decision: no analytics captures it, and it differs by agent and by repository language.

**Recent evidence (5+ independent signals)**
1. Amplifying study (Feb 2026): Claude Code across 2,430 repositories builds custom/DIY code in 12 of 20 categories. When it does pick, it picks decisively: GitHub Actions 94%, Stripe 91%, shadcn/ui 90%. https://amplifying.ai/research/claude-code-picks
2. Armature study (Sep 3 2026), 16,893 sessions:
   - the three agents agree in only 42% of cases;
   - PayPal was mentioned 139 times and chosen 0 times;
   - the winner flips by language (Resend on TypeScript, SendGrid on Python, Postmark on Go).
   https://ai-tldr.dev/releases/armature-coding-agent-tool-choice/ · https://www.stackone.com/blog/coding-agents-tool-choice-disagree/
3. Armature sells growth services from $5K/month and raised a $500K seed (Mar 2026), so willingness to pay exists, though today it is bought as a service. https://yage.ai/share/agent-tool-selection-layer-en-20260928.html
4. Carbon Ads blog "get your dev tool picked by AI agents"; Derivatex agency offers GEO for dev tools; a 2026 guide on how to get picked by coding agents. https://www.carbonads.net/blog/get-your-dev-tool-picked-by-ai-agents · https://derivatex.agency/industries/devtools/ · https://andrew.ooo/answers/how-to-get-your-tool-picked-by-ai-coding-agents-2026-guide/
5. Supabase State of Startups 2026: 61% of startups have more than half their code written by AI (reported via the andrew.ooo guide; primary source not opened).
6. Netlify AXIS (open source, scores 22 agents) and Ora (10,851 sites scanned) show vendors want an AX score. https://www.netlify.com/blog/how-we-measure-netlify-agent-experience · https://www.everydev.ai/tools/ora-ai
7. 97% of MCP tool descriptions have quality issues (Queen's University study, cited in AXIS coverage).

**Who has the pain.** Growth, DevRel and docs leads at dev-tool, API, infra and SaaS companies with SDKs, especially challengers losing to defaults (PayPal against Stripe; SendGrid and Postmark against Resend).

**What they do today.** They run agents manually in throwaway repositories, hire Armature or GEO agencies, or check Netlify AXIS once.

**Why current products fail**
- GEO tools (Profound, Peec, Otterly) measure chat answers, not agent installs.
- Amplifying and Armature sell research and services, not a continuous self-serve product.
- AXIS measures integration success but not selection.

**Why now.** Agent-written code went mainstream in 2026; the first public pick-rate studies came out in Feb and Sep 2026; MCP, skills and plugin marketplaces are new placement levers.

**Product.** Enter an npm/PyPI package or docs URL and get, within an hour:
- **pick rate:** how often each agent (Claude Code, Codex, Cursor, Antigravity, Copilot) picks you, across languages and prompt variants;
- **integration success:** does it build, does the test pass, how many turns did it take;
- **competitor share** in your category.

It then generates fixes (llms.txt, agent skills, MCP tool descriptions, docs patches) and re-runs in CI whenever docs or SDKs change. A free public leaderboard per category is the viral loop.

**Time to value:** under 1 hour from a public package name, with no integration needed.
**Pilot (14 days):** baseline report for 10 challenger vendors, apply 3 fixes, re-measure.
**Willingness to pay:** $500-$5K/month. Anchors: Armature at $5K/month; GEO tools at $300-$3K/month.
**Expansion path:** measurement → fixes → skills/MCP distribution → "agent-era ads" and placement in marketplaces → selling the panel data to investors and the labs.

**Competition**
- Direct: Amplifying (vendor product), Armature (services), Netlify AXIS (free), Ora.
- Adjacent: Profound/Peec/Otterly could add coding-agent prompts within a quarter; Mintlify/GitBook own docs and agent analytics; Context7 (Upstash) owns docs delivery to agents.

**Moat**
- At 10 customers: none.
- At 100: a benchmark panel across agent versions, with history.
- At 1,000: becomes the industry's "Nielsen" for agent picks, with causal data on which fixes move pick rate.

The weakness: sandboxed agent runs are cheap to copy, and the labs could publish this data themselves.

**CTO test sentence:** "Run 500 Claude Code/Codex/Cursor sessions a week against prompts in our category and tell me why we lose to Resend" — a DevRel lead would say yes; a CTO would say "nice to have".

**Kill test question:** Will 10 of 30 challenger dev-tool vendors pay $1K+/month after seeing a free baseline report, or do they treat it as a one-off study?

**Customers × ACV**
- Dev-tool/API/SaaS companies with public SDKs or MCP servers: an estimated 15K-40K worldwide (**unverified estimate**).
- At $12K average ACV and 25% penetration of 20K: **~$60M ARR**.
- Adding non-dev "agent pick" (shopping and B2B agents choosing vendors) merges with GEO: 100K+ brands at $6K = $600M+ TAM, but that is crowded.

The lower-ACV condition is only partly met: there are tens of thousands of customers, but distribution is efficient only through the public leaderboard.

**Scores, METHOD template (1-10):** Pain 6 · Urgency 7 · Market timing 9 · Speed to pilot 9 · Ease of integration 10 · Ease of reaching customers 9 · Willingness to pay 6 · Competition 5 · Moat 5 · Market size 6 · VC attractiveness 7 → **avg 7.2**

**Scores, original bar:**

| Category | Score |
|---|---|
| Pain | 6 |
| Urgency | 7 |
| ROI clarity | 6 |
| Customer accessibility | 9 |
| Pilot speed | 9 |
| Market size | 6 |
| Expansion | 7 |
| Venture potential | 7 |
| Defensibility | 6 |
| Why now | 9 |
| Competition position | 5 |
| **Average** | **7.0** |

**Fails the bar:** five categories score below 7 (Pain, ROI clarity, Market size, Defensibility, Competition position), and the average is below 8.5.

---

## Deep dive B: "Share button" for internal tools built with AI

**VC sentence:** Every employee now builds internal tools with Claude Code or Lovable, and this is the Vercel for those tools: one command gives the tool hosting, company sign-in, permissions and data connectors, and every shared link brings in a new builder.

**Problem.** Internal tools built with Claude Code die on a laptop, because sharing one means setting up hosting, auth, a database, OAuth per integration, cron and IT approval.

**Evidence**
1. Luo positions itself as "the Share button for the tools you build" (hosting, sign-in, permissions, Gmail/Slack/Airtable/Notion connectors, all as one MCP server). https://luo.app/cli
2. Vybe (YC) offers "Lovable for internal apps" with SSO and integrations built in. https://www.ycombinator.com/launches/NZO-vybe-lovable-for-internal-apps
3. Lovable publishes apps into a company's Microsoft tenant and reuses workspace identity. https://lovable.dev/hi/blog/microsoft-partnership · https://docs.lovable.dev/features/lovable-workspace-identity-reuse
4. Lovable has 500K+ developers (secondary source).
5. Security incidents (170+ fully exposed Lovable apps; 39% of Supabase-backed AI apps leak data) push IT toward a governed host. https://vibeappscanner.com/blog/vibe-coded-app-security-report-2026

**Who has the pain.** Ops, finance, RevOps and engineering builders at 50-5,000-person companies; IT signs off.
**What they do today.** Screenshots, Vercel with a shared password, Retool rewrites, or Lovable's Business tier.
**Why current products fail.** Builder platforms host only what was built on them. Claude Code and Cursor output has no governed home with company sign-in and connectors.
**Why now.** In 2026 many non-engineers started building internal tools with coding agents.

**Product.** A CLI/MCP command, `share`, that deploys with:
- SSO (Google/Microsoft);
- per-user scoped OAuth connectors;
- a database, cron and audit logs;
- an IT admin console.

**Time to value:** about 5 minutes.
**Pilot:** 14 days at 5 companies; success means 20+ shared tools and 3 IT approvals.
**Willingness to pay:** $20-40 per builder per month plus a $5K-$30K/yr IT tier.
**Expansion:** more builders, then viewers, then connectors, then governance and app inventory.

**Competition (fatal):** Luo, Vybe, Lovable/Replit/Bolt hosting, Retool, Superblocks, Vercel/Netlify/Cloudflare, and the AI labs, which already publish shareable pages with identity and storage. The thesis also overlaps killed thesis F (Lovable/Replit governance).

**Moat:** the connector graph and IT approval within an organization are moderately sticky. Any lab or host that adds SSO plus connectors wipes it out.

**CTO test sentence:** "Our people have 200 Claude-built tools and IT won't let any of them touch Salesforce data." Real, but the CTO's answer is "we'll use whatever Anthropic/Microsoft/Lovable ships."

**Kill test question:** In 30 days, does a lab or Lovable ship governed hosting of arbitrary agent-built code with corporate connectors? Signs say yes.

**Customers × ACV**
- 200K+ companies with 50+ employees worldwide (**unverified estimate**).
- 5% at $8K average = **$80M ARR**.
- At venture scale, 30K companies × $15K = $450M ARR.

The lower-ACV condition is met on paper: the viral loop is native and the market has hundreds of thousands of companies.

**Scores, METHOD template:** Pain 7 · Urgency 6 · Market timing 9 · Speed to pilot 10 · Ease of integration 9 · Ease of reaching customers 9 · Willingness to pay 6 · Competition 3 · Moat 4 · Market size 8 · VC attractiveness 7 → **avg 7.1**

**Scores, original bar:**

| Category | Score |
|---|---|
| Pain | 7 |
| Urgency | 6 |
| ROI clarity | 6 |
| Customer accessibility | 9 |
| Pilot speed | 10 |
| Market size | 8 |
| Expansion | 8 |
| Venture potential | 8 |
| Defensibility | 4 |
| Why now | 9 |
| Competition position | 3 |
| **Average** | **7.1** |

**Fails the bar:** Competition position 3, Defensibility 4, Urgency 6 and ROI clarity 6 are all below 7, and the average is below 8.5.

---

## Lesson for STATUS.md
For this lens, **PLG utilities built on AI behaviors are the fastest-closing gaps we have seen.** YC batches (W26, P26) and platform features fill them within one or two quarters, because anything adoptable in minutes can be built in a sprint. The only partial exception is **measurement data the platforms have a conflict in publishing**, such as agent pick rate. Its moat is a benchmark panel, which is thin.
If this lens is pursued, run deep dive A's kill test: 30 challenger vendors get a free baseline report, and success means 10 pay $1K+/month.

## Sources (all from search results; not opened unless noted)
- AgentMail seed: https://thenextweb.com/news/agentmail-raises-6m-seed-ai-agent-email-inboxes · https://www.agentmail.to/blog/agentmail-seed-launch
- AgentPhone: https://www.ycombinator.com/companies/agentphone
- Claude Code transcripts: https://simonwillison.net/2026/Jan/25/claude-code-transcripts · https://hn.svelte.dev/item/47276604
- Skillsync YC W26 / Tessl: https://yespress.io/skillsync-yc-w26.md · https://www.ai.engineer/orgs/tessl
- Agent analytics: https://www.cmswire.com/the-wire/otterlyai-launches-agent-analytics-making-ai-agent-traffic-visible/ · https://hunted.space/product/siteline
- Lovable commenting: https://www.createwith.com/tool/lovable/updates/lovable-introduces-in-app-commenting-for-team-collaboration
- Deel/Clarity: https://thenextweb.com/news/deel-acquires-clarity-deepfake-detection
- Luo / Vybe / Lovable on Microsoft: https://luo.app/cli · https://www.ycombinator.com/launches/NZO-vybe-lovable-for-internal-apps · https://lovable.dev/hi/blog/microsoft-partnership
- AgentCat: https://mcpcat.io/blog/gibson-ai/
- Jam MCP: https://jam.dev/docs/jam-mcp
- Frontify MCP: https://www.frontify.com/en/kitchen/frontify-mcp-brand-work-at-the-speed-of-conversation
- Teams bot blocking: https://www.yaps.ai/blog/teams-blocking-ai-notetaker-bots
- Greenhouse Real Talent: https://www.greenhouse.com/blog/introducing-greenhouse-real-talent
- TestSprite: https://pulse2.com/testsprite-6-7-million-seed-funding-closed-to-power-testing-for-ai-native-development
- Retell spam labeling: https://www.retellai.com/blog/spam-detection-blocking-calls
- ChatGPT Ads Manager: https://www.axios.com/2026/05/05/openai-self-serve-ad-platform · https://openai.com/blog/new-ways-to-buy-chatgpt-ads
- Vibe citing: https://gptzero.me/news/investigations-kpmg/ · https://www.einpresswire.com/article/929129446/evidite-announces-citategenie
- Agent pick rate: https://amplifying.ai/research/claude-code-picks · https://amplifying.ai/for-vendors · https://ai-tldr.dev/releases/armature-coding-agent-tool-choice/ · https://yage.ai/share/agent-tool-selection-layer-en-20260928.html · https://www.carbonads.net/blog/get-your-dev-tool-picked-by-ai-agents
- AXIS / Ora: https://www.netlify.com/blog/how-we-measure-netlify-agent-experience · https://www.everydev.ai/tools/ora-ai
- Vibe-app security: https://vibeappscanner.com/blog/vibe-coded-app-security-report-2026 · https://www.symbioticsec.ai/blog/we-scanned-1-072-vibe-coded-apps-98-had-security-flaws
