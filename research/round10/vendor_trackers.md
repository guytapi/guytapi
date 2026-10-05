# Vendor feature-request trackers and admin forums (round 10)

Date: 2026-10-05. Method: round7/METHOD.md, applied to vendor trackers (Atlassian JAC and Community, Salesforce IdeaExchange, ServiceNow Community, Microsoft Learn Q&A and Tech Community, Google Workspace Admin Help, HubSpot Ideas, Zendesk, Shopify Community, GitHub Community Discussions, Okta, Snowflake, AWS re:Post). 38 web searches. WebFetch and Reddit were blocked.

**Source caveat:** every URL below came back in search results. Vote and comment counts are quoted from search-result summaries. I did **not** read them on the page. Items marked *(unverified)* need a check on the page before anyone relies on them. I could not get vote counts for most JAC and IdeaExchange items: the search snippets do not include them.

## Bottom line

- **Nothing clears the bar (8.5, with no category below 7).** The best result averages **5.4**.
- **The tracker method mostly confirms round 9's lesson, one layer down.** Admin requests that conflict with a vendor's business model get one of two answers:
  - The vendor ships a minimal native control within 3 to 9 months. Examples: Rovo agent audit events, Rovo MCP domain allowlist, GitHub per-user AI-credit budgets, GitHub `actor_is_agent` audit field, Copilot Studio App Insights export (Jul 2026), Agent 365 registry convergence, Shopify AI-channel data controls (May 25, 2026).
  - Or a funded horizontal vendor already sells the cross-vendor version. Examples: Zylo Consumption Cost Management (Apr 14, 2026), Valence AI-SPM, CloudEagle, ServiceNow AI Control Tower and AI Gateway, Forter Agentic Orchestration Suite, Riskified.
- **The most-voted unmet needs are "let me turn the AI off" requests, not "give me more AI" requests:**
  - GitHub #159749 (block Copilot-generated issues/PRs): **1,239 upvotes, 125 comments**
  - Atlassian AI-930 (enable/disable AI per user): **446 votes**
  - Shopify "can't opt out of Agentic Storefronts" threads
  - Salesforce "turn off Ask Agentforce pop-up"
  - Atlassian ROVO-741 (hide the Ask Rovo button)
  
  Opt-out has low willingness to pay and SSPM vendors already cover it.
- **The only genuinely new, dated trigger found: Atlassian starts extra-usage billing for Rovo credits, and charges $1 per AI-agent resolution, on 2026-12-03.** Admins still have no per-user cap and no per-user usage view. Pick #1 is built on this, but it falls inside killed thesis B (AI FinOps). The new evidence narrows B to "credit pools embedded in SaaS". It does not rescue it.

---

## Part 1: Recurring unmet needs

| # | Unmet need | Votes / replies (where found) | Vendors where it appears | Evidence (URL, date) | Why vendor won't (fully) fix | Current workaround | Competitors (honest) | One-sentence product | Verdict |
|---|---|---|---|---|---|---|---|---|---|
| 1 | **Per-user / per-agent attribution and hard caps for SaaS-embedded AI credit pools** | ROVO-532 (system-level upper limit) *(votes unknown)*; HubSpot "credits usage per workflow" and "Breeze credit history" ideas *(votes unknown)*; GitHub #190671 (Mar 26 2026, team of ~18 asking for per-source breakdown; GitHub replied "use audit logs") | Atlassian (Rovo credits pooled org-wide, no per-user dashboard, overage billing from **2026-12-03**), HubSpot (single credit pool, no per-workflow view), GitHub (AI credits; per-user budgets now native), Salesforce (Flex Credits), Snowflake (AI credits), Zendesk (resolutions), Notion (credits) | [Rovo usage allowance thread](https://community.atlassian.com/forums/discussion/3282436/rovo-usage-allowance); [How Rovo credits work](https://support.atlassian.com/rovo/docs/rovo-usage-limits/); [AI agent resolutions billing](https://support.atlassian.com/customer-service-management/docs/manage-usage-for-ai-agent-resolutions/); [AI agents billing impact discussion](https://community.atlassian.com/forums/discussion/3283331/latest-changes-to-ai-agents-billing-impact); [Monitor Rovo credits in Teamwork Collection](https://community.atlassian.com/forums/Jira-questions/How-to-monitor-Atlassian-Rovo-credits-usage-in-Teamwork/qaq-p/3095517); [HubSpot credits per workflow](https://community.hubspot.com/t/hubspot-credits-usage-per-workflow/150132); [Breeze credit history](https://community.hubspot.com/t5/HubSpot-Ideas/Breeze-credit-history/idi-p/1151757); [Limits on Breeze enrichment](https://community.hubspot.com/t5/HubSpot-Ideas/Ability-to-add-limits-to-Breeze-Intelligence-enrichment-via/idi-p/1109291); [GitHub #190671](https://github.com/orgs/community/discussions/190671); [Utilization metrics for Rovo agent](https://community.atlassian.com/forums/Jira-questions/Utilization-metrics-for-Rovo-Agent/qaq-p/3087678) | Pooled credits plus overage is the new revenue line. Granular caps reduce overage. Vendors ship coarse controls only (GitHub shipped user-level budgets; Atlassian has not). | Spreadsheets; disabling Rovo entirely ("cannot enable Rovo until there is a guarantee", per the ROVO-532 thread *(unverified quote)*); manual tagging of agents | **Zylo** Consumption Cost Management (Apr 14 2026; currently OpenAI, Anthropic, Databricks, Snowflake, Vertex; more coming), Vertice / Tropic (SaaS spend), Vantage, Ramp; native GitHub budgets | Reads each SaaS's usage and audit APIs, attributes AI-credit burn to user, team, agent and automation, and enforces caps by toggling AI access via admin APIs before overage. | **Pick #1** (killed-thesis B overlap) |
| 2 | **Merchant-side integrity for orders placed by AI agents** (fees, add-ons, compatibility, age or legal rules, opt-out) | Several Shopify Community threads; reply counts not visible | Shopify (Agentic Storefronts default-on across ChatGPT, Copilot, Gemini, AI Mode), WooCommerce (10.8 dashboard setting, May 26 2026), BigCommerce (ACP via Stripe), Etsy | [Agentic checkout bypassing required fee apps](https://community.shopify.com/t/agentic-ai-checkout-bypassing-required-fee-apps-platform-level-issue-with-no-merchant-solution/629454); [Worried agents bypass checkout parts](https://community.shopify.com/t/is-anyone-else-worried-that-ai-shopping-agents-could-completely-bypass-parts-of-the-checkout-experience-merchants-depend-on/630479); [Why can't we opt out](https://community.shopify.com/t/why-cant-we-opt-out-of-agentic-storefronts/631140); [Not allowed to opt out](https://community.shopify.com/t/not-allowed-to-opt-out-of-generative-ai-agentic-storefronts/600746); [Absent from ChatGPT Shopping since Jul 25](https://community.shopify.dev/t/merchant-present-and-ranking-in-global-catalog-search-lookup-verified-but-absent-from-chatgpt-shopping-since-jul-25-how-can-the-openai-syndication-state-be-checked/37218); [AI-agent-initiated orders API](https://community.shopify.dev/t/ai-agent-initiated-orders-api/29140); [Has anyone seen AI-referred orders](https://community.shopify.com/t/has-anyone-actually-seen-ai-referred-orders-chatgpt-shopping-in-their-shopify-analytics-yet/681884) | Shopify wants default-on AI distribution (business model). The app ecosystem's cart-stage hooks are skipped by design in API checkouts. | Turn off "Direct Checkout"; hide surcharges inside shipping rates; metafields for compatibility | **Forter** Agentic Orchestration Suite + Agentic Activity dashboard; **Riskified** Decision Studio agent rules (Mar 3 2026); Signifyd; Shopify itself (routes checkout back through storefront since Mar 2026; AI-channel controls May 25 2026); UCP/ACP plugins | A policy layer that makes every agent-channel order honour the merchant's fees, bundles, compliance and compatibility rules, and quarantines non-compliant ones before fulfilment. | **Pick #2** |
| 3 | **Per-user / per-group AI feature enablement and opt-out** | **AI-930: 446 votes**; ROVO-23 (with dupes ROVO-820, ROVO-942); ROVO-107; ROVO-741; ROVO-606 (Slack admins restricting the Rovo bot); SF "turn off Ask Agentforce pop-up" | Atlassian, Salesforce, Shopify, GitHub, M365 (agent sprawl: "we could end up with 20,000 agents") | [AI-930](https://jira.atlassian.com/browse/ai-930); [ROVO-23](https://jira.atlassian.com/browse/ROVO-23); [ROVO-107](https://jira.atlassian.com/browse/ROVO-107); [ROVO-741](https://jira.atlassian.com/browse/ROVO-741); [ROVO-606](https://jira.atlassian.com/browse/ROVO-606); [SF idea](https://ideas.salesforce.com/s/idea/a0BHp000019Opj8MAC/option-to-turn-off-ask-agentforce-popup-in-trailhead); [M365 Copilot blog thread on sprawl](https://techcommunity.microsoft.com/blog/microsoft-copilot-blog/microsoft-365-copilot-wave-2-ai-innovations-in-sharepoint-and-onedrive/4245159/replies/4274094) | Default-on AI drives adoption metrics and credit consumption. Group-gating is held back as an upsell (ROVO-942 asks for it on Standard and Premium). | Disable AI per product entirely; Guard Premium | Valence AI-SPM, CloudEagle, AppOmni, Obsidian, Reco; Google and Microsoft have OU/group controls natively | Cross-SaaS AI-feature policy engine | Kill: covered by SSPM; opt-out has low WTP |
| 4 | **Block or triage AI-generated inbound contributions** (issues, PRs, reports) | **GitHub #159749: 1,239 upvotes, 125 comments** (May 2025, still referenced 2026) | GitHub; also curl, Ghostty and others | [#159749](https://github.com/orgs/community/discussions/159749); [Ghostty LOC gating](https://github.com/ghostty-org/ghostty/discussions/10550); [anti-slop action](https://github.com/marketplace/actions/anti-slop); [SlopGuard](https://github.com/Blue-B/slopguard); [GitHub blog on AI-first contributors](https://github.blog/open-source/maintainers/your-contributors-are-ai-first-now-is-your-project/) | GitHub sells Copilot issue and PR creation. It shipped repo-level PR restrictions (collaborators only / disable) rather than AI detection. | OSS actions, LOC gating, collaborator-only PRs | Many free OSS tools; GitHub native controls | Contribution-provenance triage app | Kill: payers are OSS maintainers (no budget); enterprise version overlaps thesis V |
| 5 | **Tenant-level observability of who consumes API / MCP capacity, and per-site scoping of AI connections** | AX-1883, ROVO-968, ROVO-891 (per-site MCP allowlist, sandbox vs production), ROVO-753 | Atlassian, Microsoft (Copilot Studio log questions), AWS (hidden InvokeAgent limits) | [ROVO-891](https://jira.atlassian.com/browse/ROVO-891); [ROVO-753](https://jira.atlassian.com/browse/ROVO-753); [MS Q&A detailed agent logs](https://learn.microsoft.com/en-ca/answers/questions/5911005/how-to-obtain-detailed-logs-of-agents-created-in-c); [re:Post InvokeAgent throttling](https://repost.aws/questions/QUGXuP2lgBSju-hVhWCadsig/bedrock-agent-invokeagent-api-throttling-despite-service-quota-increase) | Partly fixed (org-level allowlist; Copilot Studio App Insights export Jul 2026) | Backoff; support tickets | ServiceNow AI Gateway (platform-agnostic MCP governance), Runlayer, Credal, Boomi/Lunar | n/a | Kill: already round 9 #1 (6.4) / thesis H |
| 6 | **Agent lifecycle hygiene** (inventory, unused-agent deletion, agent creation permissions) | SF "No-code deletion of unused Agentforce"; ROVO-154 (count inactive agents); HubSpot "Enhanced Breeze Studio permission management" | Salesforce, Atlassian, HubSpot, Microsoft | [SF idea](https://ideas.salesforce.com/s/idea/a0BHp000016Kl9dMAC/nocode-deletion-of-unused-agentforce); [ROVO-154](https://jira.atlassian.com/browse/ROVO-154); [HubSpot idea](https://community.hubspot.com/t/enhanced-breeze-studio-permission-management/139611); [Rovo agent governance + create permissions](https://community.atlassian.com/forums/Atlassian-AI-Rovo-articles/IT-S-HERE-Rovo-Agent-Governance-Create-Permi/ba-p/3095332) | Vendors are shipping it (Rovo create permissions, Agent 365 registry, M365 Agent Builder admin approval) | Manual cleanup | Agent 365, Zenity, ServiceNow AI Control Tower, Valence | n/a | Kill: native + crowded |
| 7 | **Distinguishing AI vs human edits in system-of-record history** | Community Q&A: Rovo chat actions are logged as the human user; Atlassian guidance asks users to tag Rovo content with a robot emoji | Atlassian, Salesforce (Setup Audit Trail only), GitHub (solved: `actor_is_agent`, Copilot authored, human co-author) | [Does Jira store Rovo as a user in history?](https://community.atlassian.com/forums/Rovo-questions/Does-JIRA-store-ROVO-as-a-User-in-the-History/qaq-p/3204438); [GitHub agentic audit events](https://docs.github.com/en/copilot/reference/agentic-audit-log-events) | Being fixed incrementally; GitHub already shipped it | Emoji tags | Vendors themselves | n/a | Kill: feature, vendors converging (X/SOX overlap) |

Searched with nothing new found: ServiceNow (AI Control Tower already governs third-party agents and MCP: [community Q](https://www.servicenow.com/community/now-assist-for-creator-forum/how-does-ai-control-tower-handle-governance-for-third-party-ai/m-p/3535450), [June 2026 release](https://www.servicenow.com/community/ai-control-tower-articles/ai-control-tower-what-s-new-in-the-june-2026-release/ta-p/3561445)), Okta (XAA / Agent SSO; only implementation questions), Notion (agent audit trail is native), Snowflake (no indexed per-user AI-credit cap request), AWS re:Post (quota questions, 2025-era), Google Workspace (Workspace Intelligence admin data-source controls shipped Apr 2026; third-party MCP connectors Sep 2026). Not searched (budget): SAP, Workday, Databricks community, Zendesk community threads beyond docs.

**Pattern across vendors:** the same three admin needs appear at every vendor: turn AI off per group, see who or what burned the credits, and scope agent connections. Each vendor answers them in its own admin console, and the cross-vendor layer already has a funded owner for each:
- **Turn AI off:** SSPM vendors (Valence, CloudEagle and others).
- **See who burned the credits:** Zylo.
- **Scope agent connections:** ServiceNow AI Gateway and Runlayer.

---

## Part 2: Full METHOD write-ups

### Pick #1: AI-credit governor for SaaS credit pools ("cap and attribute Rovo, HubSpot, Flex and Copilot credits per user and agent")

**Problem.** In 2026, systems of record moved their AI features from bundled seats to **pooled, metered credits with overage**:
- Atlassian: Rovo credits; overage billing and $1 per AI-agent resolution from 2026-12-03.
- HubSpot: credits.
- Salesforce: Flex Credits.
- GitHub: AI credits.
- Snowflake: AI credits.
- Zendesk: automated resolutions.
- Notion: credits.

Credits are allotted per seat but pooled tenant-wide. A single team, automation or runaway agent can drain the pool. Admins can see a tenant total, but often not who or what consumed it. Most vendors offer no enforceable cap. So cautious admins keep AI switched off ("cannot enable Rovo until there is a guarantee").

**Recent evidence:**
1. Atlassian: extra-usage billing for Rovo credits and $1 per AI-agent resolution begin 2026-12-03 ([Rovo credits](https://support.atlassian.com/rovo/docs/rovo-usage-limits/); [AI agent resolutions](https://support.atlassian.com/customer-service-management/docs/manage-usage-for-ai-agent-resolutions/)).
2. Rovo allowances are pooled org-wide; there is no per-user dashboard; ROVO-532 requests system-level upper limits ([community](https://community.atlassian.com/forums/discussion/3282436/rovo-usage-allowance)). Search summary, *(unverified on page)*.
3. Admins asking how to see credit use ([Teamwork Collection](https://community.atlassian.com/forums/Jira-questions/How-to-monitor-Atlassian-Rovo-credits-usage-in-Teamwork/qaq-p/3095517); [Rovo chat credits](https://community.atlassian.com/forums/Jira-questions/How-to-find-out-how-many-credits-we-have-used-on-Rovo-chat/qaq-p/3125840); [AI agents billing impact](https://community.atlassian.com/forums/discussion/3283331/latest-changes-to-ai-agents-billing-impact)).
4. HubSpot ideas: per-workflow credit usage, credit history, enrichment limits ([1](https://community.hubspot.com/t/hubspot-credits-usage-per-workflow/150132), [2](https://community.hubspot.com/t5/HubSpot-Ideas/Breeze-credit-history/idi-p/1151757), [3](https://community.hubspot.com/t5/HubSpot-Ideas/Ability-to-add-limits-to-Breeze-Intelligence-enrichment-via/idi-p/1109291)).
5. GitHub #190671 (Mar 2026): no native per-source breakdown of Copilot requests; GitHub says to build it from audit logs ([discussion](https://github.com/orgs/community/discussions/190671)).
6. Salesforce Flex Credits: "monthly expenditures can be highly unpredictable" ([Trailhead](https://trailhead.salesforce.com/content/learn/modules/agentforce-for-employees-quick-look/get-started-with-agentforce-for-employees)).
7. Zylo's index: 78% of IT leaders hit unexpected AI or consumption charges ([CIO Influence](https://cioinfluence.com/machine-learning/zylo-launches-industry-first-solution-unifying-saas-and-consumption-spend-bringing-visibility-to-exploding-ai-and-usage-based-costs/)). Vendor-sourced.

**Who has the pain.** IT/SaaS admins and finance at companies with 500 to 10,000 seats on Atlassian Premium or Enterprise plus HubSpot or Salesforce.

**What they do today.** Leave AI off. Watch the tenant-total dashboard monthly. Open support tickets. Use GitHub's native per-user budgets where they exist.

**Why current products fail.**
- Zylo's consumption module reads AI API and data-platform bills (OpenAI, Anthropic, Snowflake), not SaaS-embedded credit pools at user or agent level. That is a gap *for now*; Zylo says more integrations are coming.
- Vendor consoles are per-vendor and coarse.
- Nobody **enforces** caps across vendors.

**Why now.** Overage billing switches on 2026-12-03 for Atlassian. Other vendors moved to credits during 2025-26.

**Potential product.** Connectors to each vendor's admin and usage APIs:
- Attribute burn to user, team, agent and automation.
- Forecast overage.
- Enforce caps by flipping per-group AI access through admin APIs where available (Google OUs, M365 licences, GitHub budgets, Atlassian groups once ROVO-23 ships).

**Time to value.** Days for read-only attribution, if the vendor exposes per-user usage. **The key risk: Atlassian does not expose per-user Rovo usage today**, so attribution might only be possible by inference from audit logs (Guard Premium).

**Pilot (14-30 days).** Atlassian plus HubSpot tenant. Success: per-user and per-agent attribution covering 80% or more of credit burn, plus a forecast of December overage.

**Willingness to pay.** Low to medium. It is capped by the size of the overage avoided. Most mid-market overage bills are likely four to five figures a year *(assumption)*.

**Expansion.** Every SaaS with credits; chargeback; procurement negotiation data (true-up benchmarks).

**Competition.** Zylo (the closest), Vertice, Tropic, Vantage, Ramp, CloudEagle; native caps (GitHub shipped; Atlassian will likely ship ROVO-532-style caps under customer pressure, as GitHub did).

**Moat.** 10 customers: connector coverage. 100: cross-tenant credit-cost benchmarks. 1,000: negotiation data, which is what Vertice and Tropic already sell.

**CTO / CIO test sentence.** "We turned Rovo and Breeze on for everyone because we can see and cap every team's credit burn."

**Kill test question.** Can per-user Rovo and HubSpot credit consumption actually be read by API today? Will 5 of 10 Atlassian admins say December overage is a top-3 concern rather than "we'll just set a budget"?

| Category | Score | Rationale |
|---|---|---|
| Pain severity | 5 | Bill shock is real but bounded; leaving AI off is a cheap workaround |
| Urgency | 7 | Hard date: 2026-12-03 |
| Market timing | 7 | Early for SaaS credit pools; late for AI FinOps in general |
| Speed to pilot | 6 | Depends on vendor usage APIs that may not exist |
| Ease of integration | 5 | Per-user usage data often missing; caps need admin APIs vendors haven't shipped |
| Ease of reaching customers | 6 | Atlassian/HubSpot admins are reachable through marketplaces |
| Willingness to pay | 4 | Capped by the overage avoided |
| Competition | 4 | Zylo already markets "consumption cost management"; native caps arriving |
| Moat potential | 4 | Connectors only |
| Market size | 6 | Every credit-metered SaaS tenant, but it is a slice of SaaS management |
| VC attractiveness | 5 | Reads as a Zylo feature; thesis B already killed |
| **Average** | **5.4** | Below bar; effectively a narrowed re-run of thesis B |

### Pick #2: Agent-channel order integrity for merchants ("make AI-agent orders obey your store's rules")

**Problem.** Since March 2026, Shopify Agentic Storefronts expose merchants by default to ChatGPT, Copilot, Gemini and AI Mode. WooCommerce (10.8), BigCommerce and others followed. Agent checkouts hit backend APIs with a prebuilt cart and skip the cart-stage app layer merchants rely on: mandatory fees, surcharges, shipping protection, warranties, bundles, gift and personalisation fields, age and legal checks. Merchants report direct losses per order and say it is "a platform-level issue apps cannot fix". They also cannot see why they fall out of AI catalogs, and many cannot opt out.

**Recent evidence:**
1. "Agentic/AI checkout bypassing required fee apps: platform-level issue with no merchant solution" ([Shopify Community](https://community.shopify.com/t/agentic-ai-checkout-bypassing-required-fee-apps-platform-level-issue-with-no-merchant-solution/629454)).
2. "Is anyone else worried that AI shopping agents could completely bypass parts of the checkout experience merchants depend on?" ([thread](https://community.shopify.com/t/is-anyone-else-worried-that-ai-shopping-agents-could-completely-bypass-parts-of-the-checkout-experience-merchants-depend-on/630479)).
3. Opt-out complaints ([1](https://community.shopify.com/t/why-cant-we-opt-out-of-agentic-storefronts/631140), [2](https://community.shopify.com/t/not-allowed-to-opt-out-of-generative-ai-agentic-storefronts/600746)).
4. Catalog syndication is a black box: a merchant has been absent from ChatGPT Shopping since Jul 25 and cannot check OpenAI syndication state ([dev forum](https://community.shopify.dev/t/merchant-present-and-ranking-in-global-catalog-search-lookup-verified-but-absent-from-chatgpt-shopping-since-jul-25-how-can-the-openai-syndication-state-be-checked/37218)).
5. ChatGPT checkout returns "blocked" with no error object ([OpenAI dev forum](https://community.openai.com/t/bug-in-chatgpt-com-checkout-stripe-session-reaches-requires-approval-then-post-backend-api-payments-checkout-approve-returns-result-blocked-with-no-error-object/1392195)). Legal cannabis merchants refused ([thread](https://community.openai.com/t/refusals-for-legal-cannabis-buisness/1396112)).
6. Many merchants still see no AI orders at all ([thread](https://community.shopify.com/t/has-anyone-actually-seen-ai-referred-orders-chatgpt-shopping-in-their-shopify-analytics-yet/681884)). This is a demand-side warning.

**Who has the pain.** Shopify, Woo and BigCommerce merchants with mandatory fees, regulated goods, configurable or compatibility-sensitive products, or add-on-heavy economics. Also the app developers whose apps get bypassed.

**What they do today.** Turn off Direct Checkout (which loses the conversion benefit). Put fees in shipping rates. Rewrite product data into metafields. Wait for Shopify.

**Why current products fail.** Forter and Riskified handle **fraud and abuse** on agent orders, not merchant business-rule compliance. Cart-stage apps never see agent carts. Shopify's own fix (Checkout Functions, UCP) is the natural owner.

**Why now.** Default-on agent channels launched in Mar 2026; Shopify terms changed May 25 2026; WooCommerce 10.8 shipped May 26 2026.

**Potential product.** A Shopify/Woo app running at the order or Functions layer:
- Detect agent-channel orders.
- Re-price or hold orders that violate fee, compliance or compatibility rules.
- Push structured constraints into the agent feed (metafields, UCP) so agents stop producing bad orders.
- Report agent-channel economics.

**Time to value.** Days (app install).

**Pilot.** 10 merchants with mandatory fees. Success: zero fee leakage on agent orders without turning off Direct Checkout.

**Willingness to pay.** SMB app pricing, roughly $20 to $300 a month. Low per merchant; only interesting at volume.

**Expansion.** Agent-channel analytics; catalog syndication diagnostics; multi-platform.

**Competition.** Shopify itself (it owns the checkout and can close the gap in one release; it already routes agent checkout back through the storefront). Forter (Agentic Orchestration Suite + Agentic Activity dashboard), Riskified (agent rules), Signifyd, UCP/ACP plugin vendors, AI-visibility tools.

**Moat.** Weak. At 10, 100 and 1,000 customers it stays an app on a platform that can absorb it at any time.

**CTO test sentence.** "Every order from ChatGPT or Gemini now carries our fees and passes our compliance rules, and we kept one-click agent checkout on."

**Kill test question.** Does Shopify's next Checkout/UCP release let fee and validation Functions run on agent checkouts? If yes, the product is dead on arrival.

| Category | Score | Rationale |
|---|---|---|
| Pain severity | 5 | Real per-order loss for a subset; many merchants see no AI orders yet |
| Urgency | 5 | Growing with agent-channel volume |
| Market timing | 6 | Default-on is recent; demand still thin |
| Speed to pilot | 8 | App install |
| Ease of integration | 7 | Standard Shopify app surfaces |
| Ease of reaching customers | 7 | App store, Shopify Community |
| Willingness to pay | 3 | SMB app pricing |
| Competition | 3 | Platform owner plus Forter/Riskified adjacent |
| Moat potential | 2 | Platform-dependent feature |
| Market size | 5 | Large merchant count, small ACV |
| VC attractiveness | 4 | "Shopify app" plus overlap with killed thesis A |
| **Average** | **5.0** | Below bar |

---

## Lessons for the method

1. **Trackers are early, but vendors read them too.** Several requests from 2025 to early 2026 were partly fixed by Q3 2026: the Rovo audit and MCP allowlist, GitHub per-user budgets and `actor_is_agent`, Copilot Studio telemetry export. A highly voted, open request is usually a feature on the vendor's roadmap, not a startup gap.
2. **The highest-vote AI requests are opt-out requests.** That signals user backlash, not budget.
3. **The cross-vendor version of each admin need already has a funded owner:** Zylo (credits), Valence and CloudEagle (AI features), ServiceNow AI Gateway and Runlayer (connections), Forter (agent orders).
4. **A useful by-product: a dated trigger.** On 2026-12-03 Atlassian Rovo overage and AI-resolution billing start. Watch the Atlassian Community in December for bill-shock threads before re-opening thesis B.
