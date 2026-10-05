# Thesis F: Securing and Governing Apps That Employees Build With AI

**Date:** 2026-10-05. **Analyst stance:** I tried to kill this thesis and kept only what the evidence supports.
**Thesis under test:** "Every employee is now a developer; we find, secure and govern the thousands of apps and automations they build with AI." Variant: "the governed enterprise runtime for AI-built apps."

## Method and caveats

- I ran 32 web searches. WebFetch was blocked (itwire.com egress blocked), so most evidence is the search engine's summary of the page at the URL shown. **Treat every figure as "reported by that source", not checked by me.**
- Many sources have a stake in the story: vendor blogs (Superblocks, Retool, Pluto, Backslash), aggregator blogs (ai2.work, chatforest, rapidevelopers) and content farms. I mark weak sources **[weak source]**. Claims I could not tie to any source are marked **[unverified]**.
- No URLs were made up. Some are mirrors or `?p=` permalinks because that is how the search engine returned them.

---

## TL;DR verdict

**REFRAME. Kill the "governed runtime" variant. Keep a narrower security/discovery wedge only if it is cross-platform and outside-in.**

- **The behavior is real and huge.**
  - Lovable reports about $500M ARR and employees at about two-thirds of the Fortune 500.
  - Replit reports a $525M run rate and users at 85% of the Fortune 500.
  - Base44 is at about $100M ARR.
  - Red Access found 380K public assets on these platforms, with 2,000-5,000 holding sensitive corporate data.
- **Mid-2026 changed the picture.** The building platforms now ship the governance layer themselves:
  - Lovable: Security Center, Workspace Insights, a Wiz integration, SSO/SCIM, publishing controls and pentests.
  - Replit: can ban public apps, force private deployments and VPC hosting, and has its own Security Center.
  - Anthropic: private org links and admin controls for artifacts.
  - Microsoft and Google: Agent 365 and the Gemini Enterprise Agent Platform.
- **Both shapes of the idea are already crowded.**
  - Runtime: Retool, Superblocks, Vybe, Power Apps, and the platforms' own VPC deployments.
  - Security: Pluto, Red Access, Zenity, Nokod, Backslash, plus AppSec incumbents relabeling.
- **What is left for an independent:** inventory and exposure validation across all platforms. That means finding apps built on personal accounts outside the enterprise tenant, which is most usage today (Lovable enterprise revenue was only about 5% of ARR), checking from the outside whether they actually leak data, and moving them into the tenant the company already pays for.
- **The problem:** that is a real but feature-sized wedge. Pluto (seeded Feb 2026) and Red Access (owns the research narrative) are already there, and SSE vendors can add it.

---

## 1. How big is the behavior, and are buyers worried?

### Adoption and revenue

| Platform | Reported traction | Source |
|---|---|---|
| Lovable | $300M ARR end of Jan 2026, $500M annualized by Jun 2026. $400M raise at $13.3B valuation (Aug 2026). Employees at "almost two-thirds of Fortune 500". Named enterprise customers: Nvidia, Adidas, Hearst, Zendesk (also Klarna, HubSpot, Deutsche Telekom, Uber per weaker sources). **Enterprise revenue about $20M of about $400M ARR (about 5%) in Feb 2026.** | https://finder.techleap.nl/news/feed/lovable-hits-300m-arr-after-tripling-revenue-since-summer ; https://siliconangle.com/2026/08/12/vibe-coding-startup-lovable-doubles-valuation-13-3b-400m-raise/ ; https://chatforest.com/reviews/lovable-500m-arr-330m-series-b-vibe-coding-2026/ [weak source] ; https://sacra.com/c/lovable |
| Replit | $240M 2025 revenue. $525M annualized run rate in Apr 2026, targeting $1B. $9B valuation (Georgian-led $400M, Mar 2026). 50M+ users, users at 85% of Fortune 500, 500K+ business accounts. | https://sacra.com/research/replit ; https://ai2.work/blog/replit-hits-9b-as-vibe-coding-conquers-the-enterprise [weak source] ; https://www.superblocks.com/blog/replit-enterprise [competitor blog] |
| Base44 (Wix) | About $100M ARR. Pulls "nearly two-thirds as many new users as Wix itself". | https://www.gurufocus.com/news/9002962/wixcom-ltd-wix-q2-2026-earnings-call-highlights-aidriven-growth-accelerates-as-base44-margins-surge |
| Retool | $120M ARR (Oct 2025). 10K+ companies. AppGen and Agents launched in 2025. | https://sacra.com/research/retool |
| Claude artifacts | Private org-link sharing for Team/Enterprise (beta, Jun 2026). 20MB persistent storage, API calls from inside artifacts, Live Artifacts. | https://cryptobriefing.com/anthropic-claude-sharing-team-editing-features/ ; https://www.creativeainews.com/blog/claude-code-artifacts-live-shareable-pages-2026/ |
| Google / OpenAI | Gemini Enterprise Agent Platform (no-code for business users, built-in governance). Opal agent steps. OpenAI Workspace Agents launched the same week as Google Cloud Next '26. | https://www.theneuron.ai/explainer-articles/everything-google-announced-at-cloud-next-26-so-far/ ; https://venturebeat.com/ai/googles-opal-just-quietly-showed-enterprise-teams-the-new-blueprint-for |

**Behavioral signal:** Retool's 2026 Build vs. Buy survey (n=817 Retool customers and builders, so a biased sample):

- 60% of builders shipped tools outside IT oversight in the past year.
- 35% have replaced at least one SaaS tool with a custom build.
- 78% expect to build more of their own tools.

Source: https://www.businesswire.com/news/home/20260217548274/en/Retools-2026-Build-vs.-Buy-Report-Reveals-35-of-Enterprises-Have-Already-Replaced-SaaS-With-Custom-Software

**Category legitimacy:** Gartner published a *Market Guide for Enterprise Vibe Coding Platforms* on 2026-04-28. It says "governance, security, and exit strategy outweigh generation speed" as selection criteria. Source: https://www.gartner.com/reviews/market/enterprise-vibe-coding-platforms

### Incidents

| Incident | What happened | Source |
|---|---|---|
| Red Access "Shadow Builders" (May 2026) | 380K+ public assets across Lovable, Base44, Replit and Netlify. 2,000+ (another write-up says about 5,000) held sensitive corporate data, often with admin access by default. WIRED and Axios confirmed live examples: a Brazilian bank's financials, a shipping company's vessel schedules, a UK clinical trial's data. Also phishing sites built on Lovable. | https://thehackernews.com/2026/05/what-2000-exposed-vibe-coded-apps.html ; https://axios.com/2026/05/07/loveable-replit-vibe-coding-privacy |
| CVE-2025-48757 (Lovable RLS) | CVSS 9.3. 170 of 1,645 showcase apps (about 10%, 303 endpoints) had Supabase tables readable or writable with the public anon key. | https://cvemon.intruder.io/cves/CVE-2025-48757 ; https://www.superblocks.com/blog/lovable-rls-breach |
| Base44 auth bypass (Jul 2025, found by Wiz) | A non-secret app_id let anyone register a verified account on private apps, bypassing SSO. Patched within 24 hours. No evidence of exploitation. | https://thehackernews.com/search/label/Wix |
| Missing controls at scale | 0 of 5,600 vibe-coded apps had CSRF protection, security headers or properly scoped policies. | https://labs.cloudsecurityalliance.org/research/ciso-daily-briefing-20260529/ |
| Unit 42 (Palo Alto) | Real breaches of sales apps with missing authentication, an auth bypass, prompt-injection RCE, and an agent deleting a production database. Palo Alto published the SHIELD framework in response. | https://infosecurity-magazine.com/news/palo-alto-networks-vibe-coding |
| n8n (automations) | CVE-2026-21858, an unauthenticated RCE rated CVSS 10. About 105K vulnerable instances (Jan 2026), 24.7K still unpatched in Feb. CVE-2025-68613 is on the CISA KEV list. Compromise exposes every stored credential. | https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/03/CSA_research_note_n8n_rce_ai_pipeline_attack_surface_20260312-csa-styled.pdf ; https://gbhackers.com/over-100000-internet-exposed-n8n-instances/amp/ |
| Tea app | Consumer app, not an enterprise citizen-built case. Not re-verified this session, and not used as evidence. | — |

### Are CISOs and CIOs worried?

- CSA (Jun 2026): NIST AI RMF, OWASP LLM Top 10, MAESTRO and AICM give **no dedicated guidance** for citizen developers. That is a governance gap. Source: https://labs.cloudsecurityalliance.org/research/csa-research-note-vibe-coding-ai-governance-gap-20260602-csa/
- IANS (May 2026) blog, "Easy-to-Build, Easy-to-Expose": a sign the topic is on CISO advisory agendas. Source: https://www.iansresearch.com/resources/all-blogs/post/security-blog/2026/05/15/easy-to-build--easy-to-expose--how-vibe-coding-is-creating-new-data-risks
- **I found no rigorous CISO survey where citizen-built AI apps rank as a top-3 priority.** The best numbers are weak: 53% call vibe coding unsuitable for security and scale (source unclear) and Retool's 60% shipped-outside-IT figure. **Kill-test result:** worry is high in the press and in research, but there is no proof it is a budget line yet **[unverified]**.

---

## 2. Competitors

| Company | Shape | Funding / traction | Threat to thesis |
|---|---|---|---|
| **Pluto Security** (Tel Aviv, founded Aug 2025) | "AI workspace security": find, monitor and secure the AI builder tools and apps employees use. Its pitch is almost word for word Thesis F. | Seed Feb 2026 (TLV Partners, Mercer Ventures, Modern Technical Fund). Amount not found. https://startupim.com/company/pluto-security ; https://pluto.security/blog/vibe-coding-security/ | **Very high.** The most direct competitor, about 9 months ahead. |
| **Red Access** | Agentless, session-based SSE. Authored the Shadow Builders research. | $17M Series A (Norwest, S Ventures), $23M total. https://www.securityweek.com/red-access-raises-17-million-for-agentless-security-platform/ | **High.** Owns the narrative and the discovery data. |
| **Zenity** | Security and governance for AI agents and low-code (Copilot Studio, Power Platform, and more). | Round of about $125M (Aug 2026; SoftBank, Hitachi, LG), about $185M total. https://cryptobriefing.com/zenity-125m-ai-agent-security-funding/ | **High** for automations and agents. Could extend to vibe-coding platforms. |
| **Nokod Security** | AppSec for low-code/no-code and RPA apps. | $8M seed (2023). https://darkreading.com/application-security/nokod-raises-8m-seed-round-from-seasoned-cybersecurity-investors-to-enhance-low-code-no-code-app-security | Medium. Older category. |
| **Backslash** | Vibe-coding security for developer environments (IDEs, agents, MCP). | $19M Series A plus $8M seed. https://www.backslash.security/press-releases/backslash-security-raises-19m-series-a-to-secure-vibe-coding-boom-in-the-enterprise-bolsters-board-with-cybersecurity-industry-leader | Medium. Developer-side, not citizen-side. |
| **Cytix** | Security and operational risk of AI-assisted coding. | $7M Series A (Aug 2026). https://aifunding.me/companies/cytix | Low-medium. |
| **AppSec incumbents** (Snyk, Checkmarx, Cycode, Endor, Aikido, Harness) | Relabeling as "vibe coding security". Cycode pitches shadow AI discovery. | Large and established. | Medium. Developer-centric, but have the budget. |
| **Wiz (Google)** | Native integration in Lovable that scans code as it is generated. Found the Base44 bug. | Part of Google. https://www.createwith.com/tool/lovable/updates/lovable-joins-google-cloud-marketplace-with-gemini-integration-and-wiz-security | **High.** Embedded in the platforms themselves. |
| **Superblocks** | Governed enterprise vibe-coding runtime (Clark agent, 2.0 in Apr 2026, AWS VPC co-marketing). | About $60M total ($23M A, May 2025). https://www.superblocks.com/blog/announcing-superblocks-2-0-a-new-era-for-governed-enterprise-vibe-coding | **Very high** for the runtime variant. |
| **Retool** | Internal-app platform with AppGen and Agents. Inherits enterprise security and data governance. | $120M ARR, 10K+ companies. https://sacra.com/research/retool | **Very high** for the runtime variant. |
| **Vybe** (YC S25) | "Secure internal apps by AI": auth, roles, connectors and a non-AI security layer. | $10M seed (First Round). https://www.vybe.build/blog/vybe-raises-10m-seed-funding | High for the runtime variant. |
| **Fabrix.ai** | "Governed VibeOps": oversight and spend controls. | Unknown. https://devx.com/daily-news/fabrix-ai-promotes-controls-for-enterprise-vibe-coding | Low. |
| **Lovable Enterprise** | SSO/SCIM, roles, restricted projects, publishing controls, Security Center, Workspace Insights (every project, publish status, risk signals), scheduled deep scans, audit logs, Wiz integration, $100 AI pentests. | $13.3B valuation. https://docs.lovable.dev/introduction/lovable-for-enterprise ; https://www.createwith.com/tool/lovable/updates/lovable-launches-workspace-insights-for-enterprise-governance-and-security | **Very high** inside its own walls. |
| **Replit Enterprise** | SSO/SCIM, RBAC, audit-log streaming, "ban public apps, require private deployments, mandate security scans", Security Center, single-tenant VPC. | $9B valuation. https://docs.replit.com/billing/plans/replit-enterprise | **Very high** inside its own walls. |
| **Microsoft** | Agent inventory in the M365 admin center, Power Platform connector DLP policies, Agent 365 as a control layer "across Microsoft and beyond". | Bundled. https://www.microsoft.com/power-platform/blog/it-pro/security-and-governance-for-agents/ | **Very high** at Microsoft-standard customers. |
| **Google** | Gemini Enterprise Agent Platform with governance and role-based controls. | Bundled. | High. |
| **SaaS security / SSE** (Netskope, Zscaler, Palo Alto, Reco, Valence, Grip, Nudge, Obsidian) | No specific vibe-coding app discovery found in my searches. Red Access argues that CASB cannot tell vibe-coded apps apart from normal platform traffic. | Big. | Medium. **Gap today**, but these vendors can follow. |

**Competitor count:** at least 6 funded startups are directly on the security/discovery framing, at least 4 are on the runtime framing, and every building platform ships native governance. This is not a category without a leader. It is an early, crowded one.

---

## 3. Can the platforms or CASB/SSPM vendors own this? What is left for an independent?

**What the platforms already own (evidence above):** governance inside their own tenant. That covers identity, publishing controls, scanning, private deployment and an admin inventory. Lovable's Workspace Insights is literally "every project, publish status, risk signals". Microsoft and Google bundle agent inventory. Anthropic gates artifacts to org-private links. **Any per-platform "find and fix" feature will be commoditized.**

**What is structurally left (the only real gaps):**

1. **Apps built outside the enterprise tenant.** Lovable's enterprise revenue was about 5% of ARR. Most corporate building happens on personal or Pro accounts that the company's admin console never sees. A platform has no incentive to report a company's "shadow" usage to that company, and it cannot match accounts to the company reliably. This is the real gap, but it may shrink as companies push employees into enterprise tenants.
2. **One cross-platform inventory.** Lovable, Replit, Base44, Bolt, v0/Vercel, Netlify, Claude artifacts, Custom GPTs, n8n, Zapier, Make and Copilot Studio each show only their own slice. Microsoft's "Agent 365 across the ecosystem" is a stated ambition, not proven.
3. **Outside-in exposure validation.** Checking whether the app is actually public, whether its Supabase tables can be read with the anon key, and whether secrets sit in the client bundle. Red Access shows CASBs miss this. SSE vendors could add it.
4. **Data-flow view.** Which corporate data sources (Salesforce, Snowflake, Drive) are wired into which citizen apps, through which personal OAuth tokens.

**Can an independent hold these?** Gaps 1-3 are what Pluto and Red Access already sell. Gap 4 overlaps with SSPM/OAuth tools (Reco, Valence, Obsidian, Grip) and Zenity. **Structurally, an independent has a 12-24 month window before SSE and SaaS-security platforms add "vibe-coded app" detection and the building platforms push enterprise-tenant consolidation. After that, the likely outcome is acquisition (the Zenity, Prompt or Aim pattern), not a $1B standalone company.**

---

## 4. Buyer, number of companies, ACV and budget

- **Buyer (security framing):** CISO, with AppSec or SaaS-security lead as champion. Budget line: AppSec, SSPM or shadow-IT/shadow-AI. Fastest entry: right after a Red Access-style press event or an internal exposure.
- **Buyer (runtime framing):** CIO or Head of IT/Business Systems, plus platform engineering. Budget line: low-code (Power Apps, Retool, ServiceNow App Engine). Slower and competitive, and it means displacing incumbents.
- **Number of companies:** companies with 1,000+ employees worldwide, roughly 40-60K **[unverified estimate]**. Companies with heavy citizen building and a security team able to buy, 2027: roughly 10-20K **[estimate]**.
- **Realistic ACV:**
  - Discovery and exposure tool: $30-100K. Mid-market $20-40K; Fortune 1000 $100-250K.
  - Runtime: $50-300K. Retool and Superblocks enterprise deals are reportedly in this range **[unverified]**.

### Bottom-up market math

| Framing | Buyers (2028) | ACV | Serviceable market |
|---|---|---|---|
| Security / discovery | 15K companies × 40% likely to buy a dedicated tool = 6K | $60K | **About $360M** |
| Security, stretch (automations + agents + apps, all platforms) | 20K × 50% = 10K | $100K | About $1B |
| Governed runtime (per builder) | 15K companies × 150 builders × $40/builder/month | about $72K/company | About $1.1B, but contested by Retool, Power Apps, Superblocks and the platforms' own enterprise tiers, whose revenue is about $1B+ ARR combined |

**Reading the numbers:** the security framing's serviceable market is about $300M-1B. That supports a $100M ARR company only with dominant share, which is unlikely given Pluto, Red Access and Zenity, plus platform bundling. The runtime TAM is bigger, but the incumbents have 10-100x more distribution.

---

## 5. Which framing is stronger, and the sharpest 90-day pilot

**Governed runtime: weaker. Recommend kill.**

- To be "Heroku for citizen apps", you have to win the builder's love against Lovable ($13B) and Replit ($9B). Both already offer private deployments, VPC, SSO and admin consoles.
- On the IT side, you have to beat Retool ($120M ARR), Superblocks (AWS-backed GTM), Vybe and Power Apps.
- A neutral runtime that "any vibe tool deploys into" needs the tools to cooperate. They have every incentive to keep hosting, which is their monetization and lock-in.

**Security / discovery: stronger, but only in this sharpened form.** A cross-platform, outside-in plus identity-in inventory of every AI-built app and automation tied to the company, including personal-account builds. Each exposure is validated by exploit, not just flagged. Each app gets a one-click path to "adopt into our Lovable, Replit or Retool enterprise tenant, or kill". Position it as the platforms' ally that converts shadow builds into their enterprise seats, not as their competitor. That partner angle also creates a possible channel and an acquirer.

### Sharpest 90-day pilot (2-3 design partners: 2,000-20,000 employees, Google or M365, at least one known vibe-coding incident or press scare)

- **Weeks 1-2 (no agent, read-only):**
  - Outside-in scan of `*.lovable.app`, `*.replit.app`, Base44, Bolt/Netlify and Vercel subdomains for company names, domains, logos and API references.
  - IdP and OAuth grant logs (Google/Entra) for Lovable, Replit and Supabase consents.
  - Corporate-email signups.
  - Expense data (Ramp/Brex/Amex) for builder subscriptions.
  - n8n/Zapier/Make and Copilot Studio inventory via APIs.
- **Weeks 3-6:** validate exposures: anon-key Supabase reads, secrets in client bundles, unauthenticated admin routes, public apps holding PII. Assign owners through the identity graph.
- **Weeks 7-12:** remediation workflow (adopt into enterprise tenant, lock down, or retire) and a policy pack (no public publish, SSO required, approved connectors).
- **Success metrics:**
  - At least 30 AI-built apps or automations found per 1,000 employees, more than 70% unknown to IT.
  - At least 3 validated critical exposures per partner.
  - At least 50% of high-risk apps remediated.
  - Conversion to a paid annual contract of $50K or more.
- **Fail metric:** fewer than 10 apps per 1,000 employees, or the CISO says "Lovable Workspace Insights plus our SSE covers this".

---

## 6. Kill signals

**Already observed (heavy):**

- Lovable and Replit shipped Security Center, Workspace Insights, ban-public-apps, private deployment and a Wiz integration in 2026. Per-platform governance is commoditized.
- Pluto Security (seed Feb 2026) has the same pitch and is about 9 months ahead. Red Access owns the research narrative and is funded ($23M). Zenity raised about $125M in Aug 2026 for agent and low-code governance.
- In the runtime space, Superblocks, Retool, Vybe and Power Apps are all funded and live, and Gartner already has a market guide.
- There is no hard survey evidence that this is a dedicated budget line rather than "add to SSE or AppSec".

**Watch (would confirm a kill):**

- Netskope, Zscaler or Palo Alto ship vibe-coded app instance detection. Watch Palo Alto especially, since it has published SHIELD.
- Wiz/Google ships cross-platform "AI-built app" discovery.
- Lovable or Replit enterprise share rises well above 5% of ARR, shrinking shadow builds.
- Pilots find fewer than 10 apps per 1,000 employees.

**Signals that would revive the thesis:**

- A regulator or auditor names citizen-built AI apps explicitly. CSA says no framework covers them today.
- A large breach with a named enterprise victim.
- Apps per company grow 10x by 2028, making cross-platform inventory structurally necessary.

---

## Sharpened thesis

> "Your employees have already built hundreds of AI apps and automations on a dozen platforms, most of them on personal accounts IT never sees. We find every one tied to your company in a week, prove which ones leak data, and move the keepers into the enterprise tenants you already pay for."

Sell to the CISO. Partner with the platforms. Treat a security platform acquisition as the likely exit.

---

## Scores (1-10)

| Dimension | Score | Rationale |
|---|---|---|
| Pain | 7 | Real exposures confirmed (Red Access, CVE-2025-48757, Unit 42, n8n KEV), but losses are mostly latent. |
| Urgency | 6 | Spikes after press events. No mandate or framework forces action. |
| ROI clarity | 5 | Risk avoidance plus maybe license consolidation. Hard to put a number on. |
| Customer accessibility | 7 | CISOs take "we found your exposed apps" meetings easily. Outside-in scan is a great door-opener. |
| Pilot speed | 9 | Outside-in plus OAuth/expense discovery gives value in week 1 with no agent. |
| Market size | 5 | About $300M-1B serviceable for security. Runtime is bigger but not winnable. |
| Expansion | 6 | Apps to automations to agents to data-flow governance, but each step hits Zenity, SSPM or the platforms. |
| Venture potential | 4 | Most likely a $100-400M acquisition, not a $1B+ independent. |
| Defensibility | 3 | Scanners and connectors are easy to copy. Platforms and SSE vendors hold the advantaged data. |
| Why now | 8 | 2025-26 adoption explosion, Gartner category, CSA governance gap. |
| Competition position | 3 | Pluto, Red Access, Zenity and the platforms' native features. A newcomer starts behind. |

**Average: about 5.7.**

## VERDICT: REFRAME, leaning KILL for a new entrant

- **Kill** the "governed enterprise runtime" variant. Platforms and Retool/Superblocks/Vybe/Microsoft own it.
- **Reframe** security to a cross-platform, outside-in, personal-account-inclusive discovery and validation layer that converts shadow builds into enterprise tenants. Advance only if a 3-week, no-agent discovery sprint with 3 design partners clears more than 30 apps per 1,000 employees with validated critical exposures, and buyers say native platform plus SSE controls do not cover it.
- If the team has no distinctive data or distribution edge over Pluto and Red Access, **kill**.
