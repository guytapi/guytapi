# Phase 1 Problem Discovery: IT Ops, Enterprise Security, Identity, Data, SaaS, Cloud

Date: 2026-10-05. Domain: IT operations / security / identity / enterprise data / SaaS management / cloud and AI infrastructure.

## Method and caveats (read first)

- Evidence came from about 40 web searches (Oct 2026). Direct page fetches were blocked by the network proxy (TechCrunch, CoreView, HN Algolia), so most evidence is the search engine's summary of the page at the URL shown. **Treat every figure as "reported by that source", not checked by me.** Many stats come from vendor blogs (CloudNuro, OneUptime, Akave, Teramind), which have a reason to make the problem look big. I flag these.
- The session ran out of search budget before I could check a few funding figures. Facts from before my training cutoff that I did not re-check are marked **(prior knowledge, not re-verified)**.
- Some URLs show up as mirror or `?p=` permalinks because that is how the search engine returned them. No URLs were made up.
- How I score a "venture wedge": (a) is the pain budgeted today, (b) can a pilot run in under 30 days, (c) ACV of $25K-150K+, (d) does it get bigger with the 2027-2032 AI and agent trend, (e) does a big platform (Microsoft, Palo Alto, CrowdStrike, ServiceNow, Okta, Datadog) already own it or have it on the roadmap. Big platforms are buying fast in 2025-26: Palo Alto bought CyberArk, Protect AI, Portkey and Chronosphere; ServiceNow bought Veza, Moveworks and Armis; SentinelOne bought Prompt Security. So "category-defining" means getting ahead of the M&A wave or picking a wedge the platforms structurally will not build.

---

## 1. MCP server sprawl: no inventory, no identity, no audit of what AI clients connect to

- **Problem:** Employees and developers connect Claude, ChatGPT, Cursor and Copilot to internal systems through local and remote MCP servers. Security has no inventory of which MCP servers exist, what credentials they hold, or what tool calls they make.
- **Who:** CISO / AppSec / platform engineering at tech-forward companies with 500+ employees. About 15-25K companies worldwide now, growing as MCP becomes the default connector.
- **Evidence:**
  - Runlayer raised an $11M seed (Khosla's Keith Rabois, Felicis). It signed "dozens of customers, including eight unicorns or public companies like Gusto, dbt Labs, Instacart, and Opendoor" within 4 months — https://techcrunch.com/2025/11/17/mcp-ai-agent-security-startup-runlayer-launches-with-8-unicorns-11m-from-khoslas-keith-rabois-and-felicis
  - July 2026: a widespread campaign scanning for exposed MCP endpoints and AI-assistant credential files — https://aviatrix.ai/threat-research-center/mcp-server-ai-assistant-credential-scanning-july-2026
  - Malicious MCP packages on PyPI/npm stealing env vars and API keys (MAL-2026-4608) — https://osv.dev/vulnerability/MAL-2026-4608
  - Exposed MCP servers spreading into cloud environments — https://www.trendmicro.com/vinfo/ru/security/news/vulnerabilities-and-exploits/update-on-exposed-mcp-servers-the-threat-widens-to-the-cloud
  - "the question is 'can I run this with audit logs, identity integration, and a CISO who'll sign off'" — https://obot.ai/blog/mcp-is-just-getting-started
- **Economic pain:** $50-200K/yr. Blocked AI rollouts are the main cost (eng productivity gains held up by security review), plus breach exposure. One shadow-AI breach adds about $670K on average (IBM-derived figure cited by CSA) — https://labs.cloudsecurityalliance.org/research/ciso-daily-briefing-20260529/
- **Competitors:** Runlayer ($11M), MintMCP, Obot (open source), Archestra, Lasso, Zenity, Palo Alto (Portkey gateway, closed May 2026 — https://nand-research.com/palo-alto-networks-portkey-acquisition-anchors-its-agentic-security-stack/), Cloudflare and Kong MCP gateways, Anthropic/OpenAI enterprise admin controls.
- **Why now / why unsolved:** MCP only became the de facto standard in 2025. Remote MCP plus OAuth is still changing. Gateways exist, but local stdio servers on developer laptops are hard to see.
- **Verdict: MEDIUM-STRONG.** Real, urgent and budgeted, but crowded fast and squeezed by gateway incumbents (Palo Alto/Portkey, Cloudflare). To win, you need endpoint-level discovery plus a policy engine, not just another proxy.

## 2. AI agents have no individual identity: shared API keys, no attribution, no delegation model

- **Problem:** Production AI agents run on shared service accounts and API keys. Nobody can say which agent (or which human through which agent) did what, or limit an agent to "act on behalf of user X, only for task Y".
- **Who:** CISO, IAM lead and platform engineering at companies deploying internal agents. About 20-40K enterprises by 2028.
- **Evidence:**
  - "Two in three organizations cannot tell, after the fact, whether a given action in their production systems was taken by a human or an AI agent" (survey of 900+ security leaders). "Agents share API keys with no individual identity, actions are not attributable" — https://akave.com/blog/ai-observability-is-not-ai-governance-the-agent-audit-gap-78-of-organizations-cant-close (vendor blog)
  - Cyera's thesis: about 68% of orgs will be unable to tell human activity from agent activity — https://securitybrief.news/story/cyera-raises-usd-600-million-at-usd-12-billion-valuation
- **Funding flood (2026):**
  - NewCore $66M (Jun 2026) — https://thenextweb.com/news/newcore-66-million-ai-agent-identity-security
  - Oak $60M seed (Jul 2026) — https://dealroom.co/news/139124-oak-exits-stealth-with-60m-seed-to-build-identity-layer-for-ai-agents/
  - Defakto $30.75M — https://www.govinfosecurity.com/defakto-raises-3075m-to-lead-non-human-identity-space-a-29767
  - Hush Security $30M — https://cryptobriefing.com/hush-security-30m-ai-agent-governance/
  - Plus Astrix, Oasis, Aembit, Clutch, Token Security, Natoma (prior knowledge: Astrix about $85M total, Oasis about $75M, Aembit about $45M; not re-verified)
  - Okta, CyberArk (now Palo Alto) and Microsoft Entra Agent ID are all shipping agent identity.
- **Economic pain:** $100-500K/yr for large enterprises (audit failure, blocked agent deployments, incident forensics).
- **Why now:** Agents move from pilots to production in 2026-27. The OAuth on-behalf-of and token-exchange standards for agents are still forming.
- **Verdict: WEAK as a new entrant (the problem is STRONG).** At least 10 funded startups and every IdP is moving in. A newcomer needs a very narrow wedge (see #3).

## 3. Agent action authorization and audit: "prove this agent action was authorized"

- **Problem:** Even where agents have identity, nothing enforces fine-grained, context-aware authorization on individual tool calls (refund under $500, read only this customer's records), and nothing produces audit evidence a SOC2 or ISO 42001 auditor accepts.
- **Who:** Engineering/platform teams building customer-facing or ops agents at SaaS companies and enterprises. About 10-30K.
- **Evidence:**
  - "observability tells you what happened, but auditing proves it was authorized. 78% of teams can't pass an AI governance audit"; "88% of enterprises had experienced AI agent security incidents... only 21% had any runtime visibility" — https://akave.com/blog/ai-observability-is-not-ai-governance-the-agent-audit-gap-78-of-organizations-cant-close (vendor blog, stats unverified)
  - An agent "approved 340 applications over a weekend using parameters nobody signed off on" — https://www.tierzero.ai/blog/ai-agent-audit-trail/ (anecdote, vendor)
- **Economic pain:** $50-250K/yr (one bad autonomous action like refunds, deletions or customer emails can cost far more).
- **Competitors:** Oso, Permit.io, Cerbos, AuthZed (authz for apps); Arcade.dev, Composio (agent tool auth); Zenity, Noma; LangSmith/Arize (observability but not authz). Prior knowledge, funding not re-verified.
- **Why unsolved:** Observability vendors log, IdPs authenticate, but no one owns policy at the moment a tool call happens plus evidence an auditor will accept.
- **Verdict: MEDIUM-STRONG.** It is a developer-led infra wedge that could become "Okta for agent actions". The risk is it gets bundled into agent frameworks.

## 4. Copilot / Glean / enterprise-AI oversharing: permissions debt exposed by AI search

- **Problem:** AI assistants inherit messy SharePoint/Drive/Box permissions and surface salary data, board minutes and M&A docs to anyone who asks, so enterprises stall rollouts until permissions are cleaned up.
- **Who:** CIO/CISO/M365 admins at companies with 1,000+ seats on M365 or Google Workspace. About 50K+.
- **Evidence:**
  - CoreView: 66% of enterprises delayed or cancelled Copilot over SharePoint exposure fears; 73% of C-level — https://itbrief.news/story/two-thirds-of-firms-delay-copilot-over-sharepoint-risks
  - Gartner survey of 132 IT leaders: 40% delayed rollout 3+ months over oversharing; Concentric: about 802K overshared files per org — summarized at https://securitybrief.news/story/two-thirds-of-firms-delay-copilot-over-sharepoint-risks
  - Earlier report — https://infosecurity-magazine.com/news/microsoft-copilot-delayed-over
- **Economic pain:** $200K-$2M/yr. Delayed Copilot value at $30/seat × thousands of seats, plus consultant cleanup projects (often $100K+).
- **Competitors:** Microsoft Purview/SAM (bundled), Varonis, Cyera ($12B valuation, $2.3B raised — https://www.intellinews.com/israeli-data-security-firm-cyera-raises-600mn-at-12bn-valuation-448033/), Concentric, Knostic, Opsin, Bonfy, Credal.
- **Why now:** AI turns latent permission debt into active exposure.
- **Verdict: WEAK-MEDIUM.** Very real pain, but Microsoft bundles it and Cyera/Varonis own the budget. The only gap is automated remediation (actually fixing permissions with owner sign-off, not just alerting). That is a feature fight.

## 5. Shadow AI: employees pasting company data into unsanctioned AI tools

- **Problem:** Most employees use AI tools IT does not know about and paste customer, financial and HR data into them. Security cannot see or govern this without blocking productivity.
- **Who:** CISO at every company with 500+ employees. About 100K+.
- **Evidence:**
  - Wakefield/PagerDuty 2026 survey (1,250 office workers at $500M+ revenue companies): 66% used AI they believed was not permitted; 34% entered customer data — https://www.pagerduty.com/fr/blog/ai/shadow-ai-workplace-survey-2026/
  - Bosses overconfident about shadow AI use — https://www.theregister.com/ai-ml/2026/05/27/bosses-blinded-by-confidence-about-shadow-ai-use-by-workers/5247275
  - Teramind report — https://www.teramind.co/wp-content/uploads/2026/06/The-Shadow-AI-Behavior-Report.pdf
- **Economic pain:** $30-150K/yr in tooling. Breach-cost argument of about $670K.
- **Competitors:** Harmonic ($26M+ — https://www.securityweek.com/harmonic-raises-17-5m-to-defend-against-ai-data-harvesting/amp/), Prompt Security (acquired by SentinelOne Aug 2025), Aim (acquired by Cato, prior knowledge), Lasso, LayerX, Island/Talon-style enterprise browsers, Netskope/Zscaler/Palo Alto SSE.
- **Verdict: WEAK.** Consolidated into SSE and browser vendors in 2025. Category already decided.

## 6. AI browsers / computer-use agents acting inside authenticated sessions

- **Problem:** Agentic browsers (Atlas, Comet, Chrome-Gemini) and computer-use agents click, copy and submit forms with the user's live SaaS sessions. Prompt injection on any web page can turn them into exfiltration tools, so Gartner says block them, and employees install them anyway.
- **Who:** CISO/endpoint teams at all knowledge-work enterprises. About 50K+.
- **Evidence:**
  - Gartner: "block all AI browsers for the foreseeable future" — https://www.csoonline.com/article/4102571/keep-ai-browsers-out-of-your-enterprise-warns-gartner-2.html
  - 27.7% of orgs already have at least one Atlas user; CometJacking attacks — https://layerxsecurity.com/?p=6012 (vendor)
- **Economic pain:** $50-200K/yr. Blocking forfeits productivity; allowing risks credential and data theft.
- **Competitors:** LayerX, Island ($5B+ val, prior knowledge), Talon (Palo Alto), Menlo, Seraphic, SquareX, and browser vendors' own enterprise modes.
- **Why now:** Agentic browsing goes mainstream 2026-2028. Blocking cannot hold.
- **Verdict: MEDIUM.** A "safe agentic browsing" policy layer is a real future need, but enterprise-browser incumbents are well placed. Pursue only with a sharp technical edge in prompt-injection containment.

## 7. AI token spend attribution / chargeback (AI FinOps)

- **Problem:** Enterprise AI spend runs across API keys, seat licenses, coding agents and embedded SaaS AI, and companies cannot attribute tokens to team, product, feature or customer. So they cannot budget, charge back or measure ROI.
- **Who:** FinOps lead / CFO office / platform engineering at companies with $1M+ annual AI spend. About 10-20K now, growing very fast.
- **Evidence:**
  - IDC 2026: 75% of AI-driven enterprises cite lack of token attribution as top chargeback challenge; Ramp: avg enterprise token spend up 13x since Jan 2025; 73% overspent vs expectations — https://www.finout.io/blog/finops-for-ai-tokens-why-the-rules-changed-and-what-to-do-about-it (vendor blog citing IDC/Ramp)
  - FinOps Foundation FOCUS 1.4 adds AI billing — https://finance.yahoo.com/sectors/technology/articles/finops-takes-daunting-task-managing-115250953.html
- **Economic pain:** At 10-30% savings on $2-20M AI spend, that is $200K-$6M/yr. The value is easy to quantify.
- **Competitors:**
  - Cloud FinOps: Vantage, CloudZero, Finout, Ternary
  - Gateways: Portkey (acquired by Palo Alto), LiteLLM, OpenRouter, Helicone
  - Observability: Datadog LLM Obs
  - Usage-based billing: Paid, Metronome, Orb
- **Why unsolved:** Spend is fragmented. Coding-agent spend (Cursor, Claude Code) and seat licenses sit outside cloud bills, and token cost per outcome (per ticket, per PR) is not measured.
- **Verdict: MEDIUM-STRONG.** Fast budget growth and easy ROI. The risk is that it becomes a feature of cloud FinOps and gateways. The wedge is "AI unit economics": cost per business outcome across all AI vendors, sold to the CFO.

## 8. Engineering AI spend governance (coding agents) specifically

- **Problem:** Coding-agent spend (Claude Code, Cursor, Codex, Devin, Copilot) is exploding per engineer ($500-5,000+/month for heavy users) with no per-developer ROI view or guardrails, and CTOs are asked to justify it.
- **Who:** CTO/VP Eng at software companies with 100+ engineers. About 30K.
- **Evidence:**
  - FinOps for AI coding — https://getunblocked.com/blog/finops-for-ai-coding/ (vendor)
  - Token spend up 13x (Ramp, via Finout above)
  - AI-assisted commits leak secrets at 2x baseline — https://www.scworld.com/news/ai-coding-assistants-twice-as-likely-to-leak-secrets-as-overall-leaks-rise-34
- **Economic pain:** For a 300-engineer org at $1-3K/month each, spend is $3.6-10M/yr. 15-30% optimization is $0.5-3M.
- **Competitors:** Engineering intelligence (Jellyfish, LinearB, DX — acquired by Atlassian, prior knowledge, Faros); vendor admin consoles.
- **Verdict: MEDIUM.** Growing budget, but the measurement of "productivity" is contested and the vendors' own dashboards may be good enough.

## 9. Unused AI seats (Copilot / ChatGPT Enterprise / Gemini) and SaaS license waste

- **Problem:** Enterprises bought AI seats in bulk. Usage is low, and SaaS management tools do not measure AI-seat activity well.
- **Who:** IT procurement / SaaS ops at 1,000+ employee companies. About 30K.
- **Evidence:**
  - Zylo 2026 SaaS Management Index: 43% of licenses unused
  - Claims of 85% unused ChatGPT Enterprise seats (CloudNuro vendor blog, unverified) — https://www.cloudnuro.ai/blog/microsoft-copilot-licensing-largest-ungoverned-ai-spend
- **Economic pain:** $180-540K/yr per 5,000 Copilot seats (vendor estimate).
- **Competitors:** Zylo, Torii, Productiv, CloudEagle, Zluri, Vendr, Tropic. Crowded.
- **Verdict: WEAK.** A solved category with low pricing power. AI seats are just another SKU.

## 10. Secrets sprawl worsened by AI coding agents and MCP configs

- **Problem:** AI coding assistants and MCP config files are causing a record surge of hardcoded and leaked secrets. Old leaked secrets stay valid for years because rotation is manual and owners are unknown.
- **Who:** AppSec/DevSecOps at software companies. About 50K.
- **Evidence:** GitGuardian 2026: 29M secrets on public GitHub in 2025, AI-service leaks +81%, AI co-authored commits leak at 2x baseline, and "64% of secrets confirmed as valid in 2022 were still exploitable in January 2026" — https://www.gitguardian.com/state-of-secrets-sprawl-report-2026 and https://dev.to/gitguardian/the-state-of-secrets-sprawl-2026-ai-service-leaks-surge-81-and-29m-secrets-hit-public-github-2bgj
- **Economic pain:** $30-150K/yr in tools plus remediation labor.
- **Competitors:** GitGuardian, Truffle, GitHub Advanced Security, Doppler, Infisical, HashiCorp Vault, Akeyless, plus the NHI players.
- **Why unsolved:** Detection is solved. **Automated rotation and owner attribution** is not.
- **Verdict: WEAK-MEDIUM.** A "zero-standing-secrets auto-rotation" wedge exists but overlaps heavily with NHI vendors and Aembit-style secretless access.

## 11. SaaS-to-SaaS OAuth integrations as a supply-chain attack surface

- **Problem:** Hundreds of third-party apps hold long-lived, over-scoped OAuth tokens into Salesforce, Google and M365. One compromised vendor (Salesloft Drift) opened 700+ tenants and bypassed MFA.
- **Who:** CISO/SaaS security at 500+ employee companies. About 50K.
- **Evidence:** Salesloft/Drift breach, Aug 2025: 700+ orgs, including Cloudflare, Zscaler and Palo Alto. Attackers searched Salesforce Cases for AWS/Snowflake keys — https://www.varonis.com/blog/salesloft-drift-breach-and-saas-risk?hsLang=en and https://www.cm-alliance.com/cybersecurity-blog/salesloft-drift-attack-one-compromised-integration-shakes-700-cos
- **Economic pain:** $50-200K/yr in tools. Breach cost in the millions.
- **Competitors:** Astrix, Obsidian, AppOmni, Valence, Grip, Nudge, Reco, Wing (acquired by CrowdStrike, prior knowledge), Adaptive Shield (acquired by CrowdStrike).
- **Verdict: WEAK.** A legitimate problem but saturated SSPM/ITDR category. AI-tool OAuth grants are a feature extension for these players.

## 12. Vibe-coded internal apps: citizen-built production apps outside IT

- **Problem:** Employees publish internal apps built on Lovable, Replit, Base44, Bolt and similar tools that touch corporate data, often public, unauthenticated and unknown to security. Meanwhile IT wants to *enable* this building safely.
- **Who:** CISO + CIO at 500+ employee companies. About 50K now, potentially every company by 2030.
- **Evidence:**
  - Red Access "Shadow Builders": 380K+ public assets on vibe-coding platforms, 2,000+ with sensitive corporate data unauthenticated; 0 of 5,600 apps had CSRF protection/proper policies — https://labs.cloudsecurityalliance.org/research/ciso-daily-briefing-20260529/
  - CSA research note — https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/06/CSA_research_note_vibe_coding_ai_governance_gap_20260602-csa-styled.pdf
- **Economic pain:** $50-150K/yr. Exposure risk, plus replacing low-code license spend (Retool/PowerApps budgets).
- **Competitors:** Red Access (discovery), Retool and Superblocks (governed internal apps), Lovable/Replit enterprise tiers, AppSec scanners (Aikido, Snyk), Zenity (low-code security).
- **Why now:** Building moved from developers to everyone in 2025-26. Security frameworks have no guidance (CSA).
- **Verdict: STRONG.** A new, fast-growing attack surface with no clear category leader. Two possible shapes: (a) "discover and secure all citizen-built AI apps" (security), or (b) a governed internal-app runtime with SSO, data connectors, audit and DLP that any vibe-coding tool deploys into (platform, bigger). Easy one-line pitch: "Employees now ship apps; we make that safe."

## 13. Stale and contradictory enterprise knowledge poisoning RAG and agents

- **Problem:** Enterprise AI assistants and agents retrieve outdated, duplicate and contradictory docs and answer confidently and wrongly. No one owns ongoing knowledge freshness and accuracy.
- **Who:** Head of KM / support ops / IT owners of Glean, Copilot or internal RAG at 1,000+ employee companies. About 30K.
- **Evidence:**
  - More than 3 in 4 surveyed leaders saw AI surface an outdated doc and produce a wrong answer (n=143, Slite, vendor) — https://slite.com/learn/dangers-of-stale-documentation
  - Insufficient/outdated context raises hallucination from 10.2% to 66.1% (Google Research, as cited) — https://tianpan.co/blog/2026-05-07-stale-docs-confident-wrong-answers-rag-knowledge-base
  - "Why Enterprise RAG fails: the data layer problem" — https://shelf.io/blog/why-enterprise-rag-fails-the-data-layer-problem/
- **Economic pain:** $50-300K/yr. Wrong answers to customers, support escalations, and AI program ROI failure.
- **Competitors:** Shelf (about $60M+, prior knowledge), Guru, Glean (verification features), Atlan/Unstructured on the data side.
- **Why now:** Before AI, people hesitated over stale docs. Agents act on them at scale.
- **Verdict: MEDIUM-STRONG.** Agent reliability depends on it, and it points straight at 2030 ("context quality is the bottleneck"). The risk is that buyers see it as a KM tool (historically low ACV). It needs to be framed as "AI context reliability", with automatic contradiction detection and owner-driven resolution.

## 14. Enterprise "context layer" for agents: business definitions and tribal knowledge not machine-readable

- **Problem:** Agents fail on enterprise tasks because the meaning of data (which revenue table is correct, what "active customer" means, how the refund process really works) lives in people's heads and Slack, not in any machine-readable form.
- **Who:** Data platform / AI platform leaders at 1,000+ employee companies. About 20K.
- **Evidence:** The domain-expert bottleneck in RAG curation — https://tianpan.co/blog/2026-05-07-domain-expert-bottleneck-rag-knowledge-curation. Gartner: poor data quality costs $12.9M/yr per org (as cited) — https://hyscaler.com/insights/best-data-observability-tools-2026/
- **Economic pain:** $100-500K/yr (failed AI projects, analyst time).
- **Competitors:** Atlan, Alation, Collibra (catalogs), dbt semantic layer, Cube, Snowflake/Databricks native semantic/AI features.
- **Verdict: MEDIUM.** Big and strategic, but incumbents (catalogs, warehouses) claim it, and success is hard to show in a short pilot.

## 15. SAP ECC → S/4HANA migration crunch (2027 mainstream maintenance end)

- **Problem:** About 35K SAP ECC customers face end of mainstream maintenance in Dec 2027, extendable to 2030 at a premium. Nearly half will not finish, mainly because of millions of lines of undocumented custom ABAP and lost process knowledge.
- **Who:** CIO/SAP CoE at large manufacturers, retailers and distributors, plus SIs. About 15-17K unmigrated.
- **Evidence:**
  - Gartner: about half of 35K will still be on ECC at the deadline — https://www.theregister.com/2026/02/27/dsag_ecc_sap/
  - Nearly 60% of migrations delayed and over budget — https://www.theregister.com/2026/02/05/sap_migrations_research/
  - Gartner calls the deadline "unrealistic" — https://itdaily.com/news/software/sap-deadline-legacy-unrealistic
- **Economic pain:** Migrations cost $5-100M+. Cutting 20-50% of custom-code and fit-gap labor is worth $1M+ per customer, so ACV of $150K-1M is plausible.
- **Competitors:**
  - Nova Intelligence, $40M (Accel, Conviction, Chemistry, SAP.iO) — https://www.fortune.com/2026/05/05/exclusive-nova-intelligence-ai-sap-chemistry-emma-qian/
  - Qorelo, $3.5M seed — https://vestbee.com/insights/articles/qorelo-raises-3-5-m
  - smartShift, Panaya, SAP's own Joule/BTP tools, Accenture/Deloitte AI tooling
- **Why now:** Deadline plus LLMs that can read ABAP.
- **Verdict: MEDIUM.** Huge budget and fast urgency, but it is a time-boxed wave (2026-2031), which is not "where the world is going". Large SIs capture much of the value, and Nova has a strong lead. Best as a services-heavy business unless it extends into ongoing ERP change management.

## 16. Mainframe / legacy system knowledge loss

- **Problem:** Engineers maintaining COBOL/mainframe and legacy ERP are retiring, and with them goes undocumented system knowledge that critical operations depend on.
- **Who:** CIO at large enterprises running mainframes (many are banks/insurers/government, which are **excluded**). Non-regulated: retail, airlines, logistics, manufacturing. About 3-5K.
- **Evidence:** Hypercubic (YC) $5.3M seed: "fewer than 100,000 [mainframe engineers] left worldwide", average age 55+ — https://pulse2.com/hypercubic-raises-5-3-million-seed-to-turn-mainframe-modernization-into-a-software-driven-process/ and https://www.ycombinator.com/companies/hypercubic
- **Economic pain:** Large ($1M+), but buyers are concentrated in excluded sectors.
- **Competitors:** IBM watsonx Code Assistant for Z, AWS Transform, Mechanical Orchard, Hypercubic, Anthropic/Claude-based SIs.
- **Verdict: WEAK** for this search, because core buyers are banks, insurers and government.

## 17. Observability bill shock (Datadog et al.)

- **Problem:** Observability bills grow 30-50% per year, faster than infrastructure, driven by log/metric/span volume and custom-metric cardinality. Teams cannot tell which telemetry is worth paying for.
- **Who:** VP Infra/SRE/FinOps at companies spending $250K+/yr on observability. About 15-25K.
- **Evidence:**
  - Bills growing 30-50% YoY; Reddit posts of $130K/month surprise bills — https://oneuptime.com/blog/post/2026-03-17-datadog-bill-shock-real-cost-observability-2026/markdown (vendor with an agenda)
  - "Is a $1 million Datadog bill worth it?" — https://signoz.io/blog/justifying-a-million-dollar-observability-bill
- **Economic pain:** 20-50% of a $0.5-10M bill, so $100K-$5M/yr. Clear ROI.
- **Competitors:**
  - Cribl ($3.5B val, prior knowledge)
  - Chronosphere (acquired by Palo Alto, prior knowledge)
  - Grafana, ClickHouse/HyperDX, SigNoz, OneUptime, Dash0 ($1B val — https://dash0.com/podcast/33-inside-the-ai-sre-boom-anish-agarwal)
  - Sawmills, Observe (acquired by Snowflake, prior knowledge)
- **Verdict: WEAK-MEDIUM.** Proven pain, but pipeline and alternative-backend markets are crowded. AI-driven "which telemetry is never queried and should be dropped" is a feature for Cribl and others.

## 18. SIEM ingest cost forcing security teams to drop logs

- **Problem:** SIEM pricing by ingest ($800K-1.5M/yr at 1 TB/day for Splunk) forces security teams to drop data sources, which creates detection blind spots, while AI-agent telemetry adds new volume.
- **Who:** SOC managers/CISO at mid-large enterprises. About 20K.
- **Evidence:** Splunk pricing ranges; Realm Security claims 50-70% volume cut — https://securityboulevard.com/2026/04/siem-pricing-2026-leading-siem-providers-compared-how-to-reduce-the-price-of-siem-ownership and https://splunkbase.splunk.com/app/8058
- **Competitors:** Cribl, Realm, Abstract Security, Axoflow, Databahn, Monad, Tenzir, plus security data lakes (Snowflake, Databricks, Anvilogic, Panther), and SIEMs built on Google/Microsoft/CrowdStrike data lakes.
- **Verdict: WEAK.** Over-funded segment with about 10 near-identical "security data pipeline" startups.

## 19. AI SRE: incident root cause in complex production systems

- **Problem:** On-call engineers spend hours correlating telemetry to find root cause. AI agents can now do the investigation.
- **Who:** SRE/platform at software companies with 50+ engineers. About 30K.
- **Evidence:**
  - Resolve AI $125M at unicorn valuation (Feb 2026) — https://techcrunch.com/2026/02/04/ai-sre-resolve-ai-confirms-125m-raise-unicorn-valuation/
  - Traversal $48M (Sequoia, Kleiner) — https://www.builtinnyc.com/articles/traversal-raises-48m-to-launch-ai-sre-20250620
  - Plus Cleric, Dash0, NeuBird, incident.io, Datadog Bits AI
- **Economic pain:** $100-500K/yr (MTTR, engineer time, downtime).
- **Verdict: WEAK** for new entrants. The category was set in 2025-26.

## 20. IT helpdesk / ITSM automation

- **Problem:** Routine IT tickets (access requests, onboarding, device issues) still need humans, and ServiceNow is expensive and slow.
- **Who:** IT Ops at 200+ employee companies. About 100K.
- **Evidence:** Serval $75M Series B at $1B (Sequoia, Jan 2026). Sequoia: "The last time we heard customer feedback this strong was 16 years ago when we partnered with ServiceNow" — https://finance.yahoo.com/news/ai-startup-serval-valued-1-110259800.html. ServiceNow bought Moveworks for $2.85B (search summary).
- **Verdict: WEAK.** Taken (Serval, Moveworks/ServiceNow, Atomicwork, Ravenna, Console).

## 21. Access governance / entitlement cleanup / offboarding (humans + agents)

- **Problem:** Access reviews are rubber-stamped spreadsheets, offboarding misses SaaS accounts and tokens, and AI agents now add identities that also need reviews.
- **Who:** IT/IAM/GRC at 300+ employee companies. About 60K.
- **Evidence:** ConductorOne ($100M+ raised, Series B $79M) — https://pulse2.com/conductorone-12-million-series-a-expansion/. Lumos ($85M+) is pushing "six-agent identity workforce" — https://yespress.io/lumos. ServiceNow bought Veza (about $1B, search summary).
- **Verdict: WEAK.** Crowded (SailPoint, Saviynt, ConductorOne, Lumos, Opal, Veza/ServiceNow, Okta IGA).

## 22. Compliance evidence / SOC2 and security questionnaires

- **Problem:** B2B vendors spend weeks collecting compliance evidence and answering 300-question security questionnaires per enterprise deal.
- **Who:** Security/GRC/sales engineering at B2B SaaS. About 50K.
- **Evidence:**
  - Vanta $300M ARR (Apr 2026), $4.15B valuation — https://sacra.com/research/vanta-at-300m-year/
  - Delve scandal (Mar 2026, alleged audit mills) undermines trust in "AI SOC2"
  - Conveyor ($32M+) and Vendict ($21.5M) — https://pulse2.com/conveyor-12-5-million-funding/ and https://www.vcbacked.co/company/vendict
- **Opportunity inside it:** The Delve scandal shows **trust in compliance artifacts is breaking**. As AI makes it free to generate questionnaire answers and evidence, buyers will need *verifiable, continuously attested* security posture instead of PDFs. A "trust exchange" with machine-verifiable controls is a 2030 idea, but has network-effect cold-start problems.
- **Verdict: WEAK** (automation is taken); **MEDIUM** for the verifiable-trust angle, which is speculative.

## 23. GPU / inference capacity waste

- **Problem:** Enterprise-owned and reserved GPU fleets sit mostly idle (5% average utilization by Cast AI telemetry; 22% for inference) because scheduling, sharing and right-sizing tools are immature.
- **Who:** ML platform/infra at companies with $1M+ GPU spend. About 3-8K now.
- **Evidence:** Cast AI 2026 report (23K clusters): 5% average GPU utilization; 86% of GPU owners at ≤50% — https://www.hpcwire.com/aiwire/2026/04/21/companies-are-racing-to-buy-gpus-many-sit-idle
- **Economic pain:** 30-60% of a $2-50M GPU bill, so $1M+.
- **Competitors:** Cast AI (unicorn, prior knowledge), Run:ai (acquired by NVIDIA), Rafay, ScaleOps, Modal/Baseten (serverless inference), CoreWeave, NVIDIA Dynamo.
- **Verdict: MEDIUM-WEAK.** A large but concentrated buyer set. NVIDIA and clouds absorb it. Most enterprises will rent inference by the token rather than own GPUs, so the problem moves to #7.

## 24. Data pipeline breakage feeding AI (data quality for agents)

- **Problem:** Silent upstream schema/volume/freshness breaks corrupt the dashboards and now the agents that act on warehouse data, with about 61 data incidents/month per team (Monte Carlo survey, as cited).
- **Who:** Data engineering at companies on Snowflake/Databricks. About 30K.
- **Evidence:** https://hyscaler.com/insights/best-data-observability-tools-2026/; r/dataengineering is full of these threads (not individually cited).
- **Competitors:** Monte Carlo (prior knowledge, $1.6B val 2022), Bigeye, Anomalo, Soda, Elementary, Metaplane (acquired by Datadog, prior knowledge), and native Snowflake/Databricks features.
- **Verdict: WEAK.** Mature category. The "agents act on bad data" angle reframes it but does not reopen it.

## 25. Snowflake / Databricks spend overruns

- **Problem:** Data warehouse spend overruns of 40-60% from over-provisioned warehouses and inefficient queries (vendor claim).
- **Evidence:** https://www.revefi.com/blog/snowflake-cost-optimization; Yuki, Chaos Genius, PerfectScale/DoiT — https://www.doit.com/demo/perfectscale-for-data-lakes
- **Verdict: WEAK.** Many small players, and the warehouse vendors fix it natively.

## 26. AI system inventory for EU AI Act / ISO 42001 (non-regulated deployers)

- **Problem:** Companies must keep an inventory of AI systems and risk classifications (EU AI Act deployer duties; high-risk obligations likely pushed to Dec 2027 by the Digital Omnibus). 83% have no inventory.
- **Who:** GRC/legal/CISO at EU-exposed companies. About 30K.
- **Evidence:** Vision Compliance (Apr 2026): 78% have taken no meaningful steps; 83% have no AI inventory — https://enterprisedna.co/resources/news/eu-ai-act-78-percent-enterprises-unprepared-2026/ and https://www.gosign.de/en/magazine/eu-ai-act-2026-enterprises/
- **Competitors:** Credo AI ($41M — https://siliconangle.com/2024/07/30/credo-ai-raises-21m-help-enterprises-deploy-ai-safely-responsibly-compliant-way/), Holistic AI, OneTrust, ServiceNow AI Control Tower, Vanta/Drata ISO 42001 modules, Airia.
- **Verdict: WEAK-MEDIUM.** Driven by regulation, so buyers do the minimum, deadlines slip, and GRC suites bundle it. Useful as a door-opener for #1/#3 (automated discovery feeding the inventory), not as a standalone wedge.

---

## Cross-cutting observations

1. **Agentic identity/security is the hottest and most crowded area.** NHI/agent identity got at least $250M in 2026 seed and A rounds alone (NewCore, Oak, Defakto, Hush), plus platform M&A. Problem-strength is not the issue; differentiation is.
2. **M&A is fast.** Palo Alto (CyberArk, Protect AI, Portkey, Chronosphere), ServiceNow (Veza, Moveworks, Armis), SentinelOne (Prompt), CrowdStrike (SGNL, Pangea, Onum — prior knowledge, not re-verified), Snowflake (Observe), Datadog (Metaplane). Startups in this domain often exit at $300M-$1B before reaching category size. For a $1B+ independent outcome, go where platforms are *structurally* weak: new runtimes (citizen-built apps), cross-vendor neutrality (AI spend across all vendors), or developer-led infra (agent authz).
3. **The best 2027-2032 bets are things that only exist because of agents:** apps built by non-engineers, agent actions needing authorization and audit, context reliability, and cost per AI outcome. Bolting AI onto old categories (helpdesk, SIEM, SSPM, IGA) is mostly taken.

---

## Top 5 most promising

1. **Governed runtime and security for vibe-coded / citizen-built internal apps (#12): STRONG.** A brand-new attack surface (380K+ public vibe-coded assets, thousands leaking corporate data), no category leader, no framework guidance, and it grows with the "everyone is a builder" trend. Pitch: "Employees now ship software; we're the safe place it runs." Pilot: discover existing apps in week 1. ACV $50-200K. Risk: Retool/Superblocks or the vibe-coding platforms' enterprise tiers.
2. **Agent action authorization and audit-grade evidence (#3): MEDIUM-STRONG.** Policy at the moment of each tool call plus proof an auditor accepts, sitting between agent identity (crowded) and observability (crowded). Pitch: "Okta + audit log for what AI agents *do*." Risk: framework bundling, and IdPs extending downward.
3. **AI unit economics / cross-vendor AI spend attribution (#7, #8): MEDIUM-STRONG.** Token spend up 13x, 75% cannot attribute it, and coding-agent spend is ungoverned. ROI is concrete for a CFO buyer. Pitch: "Cost per AI outcome across every model, agent and seat." Risk: Vantage/CloudZero/Datadog add it, and the gateway layer (now Palo Alto) captures traffic.
4. **AI context reliability: stale/contradictory knowledge detection and resolution for RAG and agents (#13, with #14): MEDIUM-STRONG.** Agent accuracy is limited by corpus quality. More than 3 in 4 leaders have seen confident wrong answers from stale docs. Pitch: "Continuous QA for what your AI knows." Risk: seen as a low-ACV KM tool, and Glean/Microsoft add freshness signals.
5. **MCP / AI-connector control plane with endpoint discovery (#1): MEDIUM-STRONG.** Pull is proven (Runlayer signed 8 unicorns/public companies in 4 months), and there are active attacks (MCP scanning campaign, malicious MCP packages). The window is short, and the gateway play is already contested by Palo Alto/Portkey and Cloudflare. A new entrant would need differentiated discovery of local or unsanctioned MCP use plus policy.

Honorable mention: **SAP ECC migration AI (#15).** Huge budgets and a real deadline, but it is a time-boxed wave and Nova Intelligence ($40M, Accel/Conviction/SAP.iO) already leads.

Explicitly not recommended (taken or consolidated): shadow-AI DLP, AI SRE, AI helpdesk, IGA/access reviews, SSPM/OAuth app security, security data pipelines, observability cost, SOC2/questionnaire automation, SaaS license management, data observability.
