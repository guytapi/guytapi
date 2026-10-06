# Deep dive: "the platform where companies run their own AI-built apps replaces dozens of SaaS seats"

**Date:** 2026-10-06. **Inputs:** BRIEF.md, T3_internal_tools.md (thesis 4, scored 6.4), phase5/F_citizen_ai_apps.md (killed at 5.7 as a security play).
**Method:** 11 web searches; WebFetch blocked. Every figure below is what the cited page reports (via search summaries). I did not check them myself. Vendor-authored sources are marked [vendor].

## 0. The claim under test
"Enterprise SaaS ($300B+) assumes software is expensive to build, so companies buy generic per-seat apps. AI makes custom software nearly free. So the category gets rebuilt as the platform where companies run their own AI-built apps (data, identity, hosting, lifecycle). That new system of record replaces dozens of SaaS seats."

## 1. Evidence (all 2026)
| # | Signal | Source |
|---|---|---|
| 1 | Retool Build vs Buy report (Feb 2026): 35% of enterprises have replaced at least one SaaS tool with custom software; 78% expect to build more; 60% of builders work outside IT [vendor] | https://www.businesswire.com/news/home/20260217548274/en/Retools-2026-Build-vs.-Buy-Report-Reveals-35-of-Enterprises-Have-Already-Replaced-SaaS-With-Custom-Software |
| 2 | "SaaSpocalypse": about $285B of software market cap wiped out in one February day, after Claude Cowork launched; markets are pricing in per-seat erosion | https://ainsliebullion.com.au/News-Resources/Article/The-SaaSpocalypse-AI-Comes-for-Software-Stocks/ID/9101 ; https://bolt.new/blog/is-saas-dying |
| 3 | Counter-view: "The AI SaaSpocalypse is a mirage" | https://devinterrupted.substack.com/p/the-ai-saaspocalypse-is-a-mirage |
| 4 | Palantir replaced its own CRM with an app built on AIP "in a few months" | https://hudson-labs.com/research/ai-saas-replacement-2026 ; https://futurumgroup.com/insights/palantir-q1-fy-2026-revenue-beats-estimates-us-demand-drives-outlook-raise/ |
| 5 | Klarna "replaced Salesforce/Workday" with Deel plus other SaaS, not with custom builds | https://www.cxtoday.com/?p=65960 |
| 6 | Microsoft Power Apps "Vibe" (vibe.powerapps.com): agent-generated, code-backed apps that inherit the tenant's governance and ALM | https://thenewstack.io/power-apps-plans-feature-vibe-ifies-business-app-dev/ |
| 7 | Replit Enterprise: self-serve contracts up to $200K (May 2026); SSO/SCIM/RBAC/audit; 30+ connectors including Snowflake and Databricks; Sacra describes it as becoming an "internal app OS" | https://docs.replit.com/billing/plans/replit-enterprise ; https://sacra.com/research/replit-passes-500m-year/ |
| 8 | Supabase raised $500M at $10.5B (Jun 2026), about $170M ARR. Vercel valued at $9.3B | https://sacra.com/c/supabase/ ; https://news.bloombergtax.com/daily-tax-report-state/vercel-notches-9-3-billion-valuation-in-latest-ai-megaround |
| 9 | Vybe $14.75M seed (Dec 2025); Superblocks $62M total; Retool unicorn | https://www.caplight.com/company/vybe ; https://www.cbinsights.com/company/superblocks/financials |
| 10 | Maintenance reality: SaaStr says "getting v1 working is easy, everything after is where the wheels come off"; CIO.com: vibe-coding your own enterprise apps is "edgy business"; internal builds are typically abandoned within 6-18 months [weak source] | https://www.saastr.com/the-90-10-rule-for-ai-agents-updated-we-replaced-a-paid-saas-tool-in-a-day-with-a-vibe-coded-app-heres-what-we-learned/ ; https://www.cio.com/article/4148288/vibe-coding-your-own-enterprise-apps-is-edgy-business.html ; https://usetandem.ai/blog/when-vibe-coded-tools-stop-scaling |
| 11 | Notion Custom Agents (Feb 2026), with Salesforce and Box connectors by April 2026 | https://www.notion.com/releases/2026-04-14 |

## 2. Role 1: technical architect
**What the platform actually needs:**
1. Identity: SSO, app-level RBAC, and agent identities.
2. Data: a managed Postgres per app, plus governed read/write scopes into Snowflake and the remaining systems of record (SoRs).
3. Hosting: private-by-default, VPC, environments.
4. Lifecycle: an owner, versioning, deprecation, dependency patching, and AI-driven maintenance that regenerates or upgrades apps.
5. Catalog and deduplication.
6. Shared primitives: a common data model so apps compose with each other instead of becoming 400 silos.

**Hard parts:**
- **The shared data model (item 6) is the only part that makes this a "system of record."** It is also exactly what Salesforce, ServiceNow, Palantir Foundry (the Ontology) and Microsoft Dataverse already are. Without it you are Heroku with SSO.
- **Replacing SaaS means replacing more than the UI.** You also have to replace embedded domain logic, integrations, compliance artifacts (SOC reports, audit trails) and vendor-maintained updates. "Nearly free to build" is not "nearly free to own." The total cost of ownership (TCO) is mostly run and change costs, not the build.
- **Feasible today:** items 1-4, which are commodity (Supabase + Vercel + Okta + Backstage). Agent-driven maintenance (item 4) is genuinely new and is the one technically differentiated bet: "every app has an agent on-call that keeps it patched and working."

**Verdict:** buildable, but the defensible part is either already owned (the data model) or not yet proven (autonomous maintenance).

## 3. Role 2: skeptical CTO/CIO
- **"Which SaaS will I actually turn off?"** The long tail: $5-50K tools such as sponsor portals, approval flows, trackers and dashboards. Not Salesforce, Workday, NetSuite or Zendesk. Those carry compliance, ecosystem and data gravity. Klarna, the poster child, swapped vendors rather than building.
  - So the "replaces dozens of SaaS seats" dollars are a small slice of my spend. The long tail is perhaps 10-20% of the SaaS budget [estimate].
- **"I already own a platform for this."** Power Platform comes with my Microsoft E5, and now it vibe-codes inside my existing governance. My data team has Snowflake/Databricks apps. My engineers use Vercel/Supabase. Why add a vendor?
- **"Ownership is my real problem, not hosting."** Who is on call when the builder leaves? Show me lifecycle and maintenance, not another runtime.
- **"Shadow apps exist on personal Lovable/Replit accounts."** That is a discovery and governance problem. Thesis F already found that space crowded.
- **What would make me buy:** a measured, contractual saving ("we retired $X of SaaS"), plus a guarantee that apps keep working with no builder involved.

## 4. Role 3: top-tier VC partner
- **The narrative is first-tier.** Public markets are already repricing per-seat SaaS, and this is the "picks and shovels of the SaaSpocalypse" story.
- **Investable winners in the layer already exist and are priced:**
  - Replit ($9B), Lovable ($13.3B), Supabase ($10.5B), Vercel ($9.3B), Retool (unicorn).
  - Each of them is converging on "governed internal app platform." Replit Enterprise is that thesis, live, self-serve, at $500M+ run rate.
- **Seed-stage question: "Why are you not a feature of Replit + Supabase + Okta?"** I need a non-obvious angle:
  - (a) an outcome-priced business model: share of the SaaS savings retired;
  - (b) autonomous maintenance as the product;
  - (c) a domain-specific SoR for one function.
- **Would I write a seed check on the generic platform?** No. On (a)+(b) together, maybe, if the founders have an enterprise platform-engineering distribution edge. Expect a crowded Series A.

## 5. Role 4: competitor analyst
| Player | Position on "run your own AI-built apps" | Threat |
|---|---|---|
| Microsoft Power Platform | Vibe apps that inherit tenant governance; Dataverse is the SoR; bundled into E5 | Very high (distribution + price of zero) |
| Replit Enterprise | Governed internal app factory: SSO/SCIM/RBAC, warehouse connectors, self-serve up to $200K | Very high (it is the thesis) |
| Lovable | Security Center, SSO, Wiz integration; enterprise only about 5% of ARR but has huge bottom-up reach | High |
| Retool | 10K+ companies, AppGen, agents; publishes the very stat behind the thesis | High |
| Superblocks / Vybe | Purpose-built "enterprise vibe coding for internal apps", funded | Medium-high (direct) |
| Vercel / Supabase | The default hosting and data substrate under these apps; either can add a governance/catalog layer | Medium (substrate owners) |
| Airtable / Notion | Agents and apps over their own data model; already the SoR for the long tail | Medium |
| Salesforce / ServiceNow | Agentforce / App Engine: "build custom on our SoR"; they defend by becoming the platform | Medium (incumbent counter-move) |
| Palantir Foundry/AIP | Ontology + AIP = literally "the SoR you build custom apps on"; claims CRM replacement | High at the top end |

**Opening:** the generic platform has almost none. The gaps the evidence points to are:
- (1) cross-platform lifecycle and maintenance of apps built anywhere;
- (2) proof of retirement — measuring and guaranteeing the SaaS dollars actually removed.

## 6. Self red-team
- **The "$300B" market size is a category error.** The money that actually moves is the long tail of SaaS plus internal-tools spend. That is still $10B+, but the money flows to whoever already hosts the builders (Microsoft, Replit, Lovable).
- **"Nearly free software" undermines a per-app platform's pricing too.** Hosting is a commodity. A new SoR has to win on the data model, and the data model is owned by incumbents.
- **The 35% stat is a Retool survey.** "Replaced at least one tool" is a low bar, and the evidence of retired spend at scale is anecdotal (SaaStr's $10K portal).
- **The steelman for the thesis:** maintenance is the unsolved part (6-18 month abandonment). A platform whose agents own app upkeep turns build-once into run-forever. That is the real assumption break: "software needs human maintainers." Nobody clearly owns it yet. But Replit/Lovable agents are the natural owners, because they already hold the code.
- **Prior kill check:** this is thesis F / thesis 4 again unless the business model changes. Outcome pricing plus maintenance-as-product is a moderate change, not a fundamental one.

## 7. Sharpened thesis (brief format)
- **Existing category:** long-tail per-seat SaaS plus internal tools/low-code. Market: low-code about $30B+; long-tail SaaS spend $30-60B [estimate].
- **Old assumption:** software is costly to build and to *maintain*, so companies rent vendor-maintained apps per seat.
- **Why AI breaks it:** building is now hours. Maintaining is the remaining blocker, and agents can increasingly do it.
- **New category:** "Managed custom software": an agent-maintained fleet of company-specific apps, with an owner, SLA and deprecation for each app, priced against the SaaS it retires.
- **Product (CTO-simple):** connect SSO, the repos and the SaaS spend data. We list which tools are retire-able, generate replacements on your existing stack (Supabase/Vercel/Power Platform), and keep them patched and working with an on-call agent.
- **Buyer:** CIO / VP Platform, co-signed by procurement/FinOps.
- **Pain:** SaaS sprawl cost, plus orphaned vibe-coded apps.
- **Workaround:** Retool/Power Apps, plus heroic individual builders.
- **Competitors:**
  - Direct: Replit Enterprise, Superblocks, Vybe, Retool.
  - Adjacent: Power Platform, Lovable, Palantir, SaaS-management tools (Zylo, Vendr).
- **Why incumbents may lose:** builders monetize seats and builds, not retired spend. SaaS vendors cannot sell their own replacement. Microsoft governs only its own stack.
- **Wedge:** retire 5 long-tail tools in 30 days and keep them alive for 6 months.
- **Integration:** days.
- **Pilot:** a spend scan, 3 replacements, and a measured saving.
- **Pricing:** 30-50% of the retired SaaS spend, annually.
- **Expansion:** more tools retired, then mid-tier apps.
- **Moat:**
  - At 10 customers: services know-how.
  - At 100: a library of replacement templates per SaaS category.
  - At 1,000: maintenance telemetry and a reliability record. Still medium.
- **$10B case:** 3% of the long-tail SaaS budget flows through outcome pricing. Plausible only if maintenance agents prove reliable.
- **CTO one-liner:** "We turn your $40K tools into apps you own, and we keep them working."

### Revised scores
Order: Market size, Market transformation, Urgency, Why-now, Ease of reaching buyer, Speed to pilot, Ease of integration, Competitive opening, Structural differentiation, Expansion potential, Moat, VC attractiveness.

| Version | Scores | Average |
|---|---|---|
| Original framing (generic platform/SoR) | 7, 8, 5, 8, 5, 5, 5, 2, 3, 7, 4, 5 | **5.3** |
| Sharpened (managed custom software, outcome-priced) | 7, 8, 6, 8, 6, 7, 6, 4, 5, 7, 4, 6 | **6.2** |

The original framing scores lower than T3's 6.4. Market size is cut from 9 to 7, because the $300B of tier-1 SoR spend is not actually in play. Competitive opening is cut to 2, because Replit Enterprise and Power Apps Vibe already ship this.

## 8. Verdict
**Kill the "new system of record / platform" framing.** It repeats thesis 4 and thesis F (killed). Microsoft, Replit, Lovable, Retool and Palantir own it, and the $300B headline counts SoR spend that is not moving.

**Park, rather than pursue, the narrower reframe** (agent-maintained, outcome-priced replacement of long-tail SaaS) at about 6.2. It touches a real unclaimed assumption: "software needs human maintainers." But it looks like a tech-enabled service, its moat is weak, and builders can add maintenance agents. Revisit only if:
- there is evidence that agent-maintained apps survive at least 12 months without the builder; or
- the founders have a procurement/FinOps distribution edge.
