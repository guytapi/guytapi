# Round 31 — Track 3: Internal tools at AI-native companies → which incumbent category is being outgrown

Researcher pass 2026-10-06. 12 web searches (WebFetch blocked; facts come from search snippets only). Builds on round8/internal_platforms.md (background-agent platform, MCP gateway, model gateway: already covered and killed). URLs below are ones that appeared in search results. Dates marked *(unverified)* were not confirmed in a snippet.

## Signal map: internal build → incumbent category it signals is being outgrown

| Internal build | Builder / source | Incumbent category being outgrown | Vendor state, Oct 2026 |
|---|---|---|---|
| Kepler in-house data agent (70k datasets, 80% of company uses it, answers in under 90s, used from Slack/Cursor) | OpenAI, Jan 2026: https://openai.com/index/inside-our-in-house-data-agent/ ; https://thenewstack.io/kepler-openais-internal-agent-platform-for-synthesizing-data/ ; OpenMetadata underneath: https://open-metadata.org/case-study/openai | BI + data catalog (Tableau/Looker/Alation/Collibra) | Snowflake Intelligence, Databricks Genie, Hex, ThoughtSpot, Collate: crowded |
| CLUE Triage (first-pass alert triage with Slack/docs/code/warehouse context, dispositions with confidence scores) | Anthropic: https://claude.com/blog/how-anthropic-uses-claude-cybersecurity | SIEM/SOAR + Tier-1 MSSP | Dropzone, Prophet, 7AI, Torq, CrowdStrike Charlotte, Google SecOps agents: crowded |
| Incident investigation agent wired to Honeycomb MCP | Stripe, O11yCon 2026: https://www.honeycomb.io/resources/conference-talks/building-an-ai-observability-agent-lessons-from-the-trenches-stripe-o11ycon-2026 | Observability UI + incident mgmt (Datadog/PagerDuty) | Resolve AI ($125M A at $1B, Feb 2026: https://techcrunch.com/2026/02/04/ai-sre-resolve-ai-confirms-125m-raise-unicorn-valuation/), Traversal ($48M, Kleiner/Sequoia), Cleric, Datadog Bits AI: crowded |
| Domain owners build their own agents; the platform team ships "the road, not the vehicles" (substrate + access) | WorkOS essay: https://workos.com/blog/person-with-the-problem-builds-the-tool *(date unverified)* | Internal-tools / low-code + long-tail SaaS seats | Retool, Replit, Lovable, Vercel v0, Airtable: crowded |
| 35% of enterprises replaced at least one SaaS tool with a custom build; 78% plan more; 60% shipped outside IT oversight | Retool 2026 report, 2026-02-17: https://www.businesswire.com/news/home/20260217548274/en/Retools-2026-Build-vs.-Buy-Report-Reveals-35-of-Enterprises-Have-Already-Replaced-SaaS-With-Custom-Software | Workflow automation, admin tools, then CRM/BI/PM/support | Same as above |
| Agents as assignable first-class users; Triage Intelligence turns Intercom/Zendesk/Gong into routed issues | Linear: https://eesel.ai/blog/linear-ai (Dec 2025 launch) | Jira / ServiceNow ticketing as the human work queue | Linear, Atlassian Rovo, ServiceNow AI agents |
| Shut down Salesforce/Workday, but actually replaced them with Deel + other SaaS + internal AI | Klarna: https://www.cxtoday.com/?p=65960 | CRM/HCM (mostly hype) | Counter-signal |
| Agent identity: "no HR process for agent deployment" | https://www.techzine.eu/blogs/security/143450/the-ai-agent-presents-a-new-identity-puzzle/ ; Okta for AI Agents EA: https://www.okta.com/blog/ai/okta-ai-agents-early-access-announcement/ | IGA/workforce IAM (Okta, SailPoint) | Okta, WorkOS, Astrix, Oasis, Aembit: crowded |

**Counter-evidence:** Datadog's CFO says customers mostly *buy* rather than build (https://www.marketbeat.com/instant-alerts/datadog-touts-re-acceleration-at-morgan-stanley-conference-as-ai-security-push-gains-steam-2026-03-09/). Klarna's "replaced Salesforce with AI" story was really a SaaS swap.

**Headline:** internal builds at frontier companies are almost always **agent layers on top of the incumbent's data**, not replacements of the system of record. Kepler sits on OpenMetadata and the warehouse. Stripe's agent queries Honeycomb. CLUE reads the SIEM. So the category being outgrown is the **human GUI/workflow layer** of each incumbent: dashboards, consoles, ticket queues. The storage and telemetry layers are not being outgrown. Each of those agent layers already has a $50M-$1B-funded startup plus the incumbent's own native agent. That fits STATUS lesson #1: public signal means funded within about 6 months.

---

## Thesis 1 — Agent-native data analyst replaces BI dashboards
- **Existing category:** BI + data catalog. **Market:** about $30B BI plus about $1.5B catalog.
- **Old assumption:** humans build dashboards ahead of time, and analysts work the queue of ad-hoc questions.
- **Why AI breaks it:** agents answer ad-hoc questions in seconds. The scarce asset becomes curated semantics and table trust, not charts.
- **New category:** a "data answer engine" made of a semantic layer, usage-derived table trust, and an agent reachable from Slack, the IDE and other agents.
- **Product:** connect the warehouse and catalog, learn from query logs which tables are canonical, and answer in Slack with SQL plus lineage.
- **Buyer:** Head of Data. **Pain:** analyst backlog, and wrong-table answers.
- **Evidence:** OpenAI Kepler (Jan 2026; 80% adoption; days of searching cut to under 90s); OpenMetadata case study; Retool report lists BI among the tools being replaced; Snowflake/Databricks are shipping agents; Collate Summit '26.
- **Workaround:** analysts, Looker, and in-house text-to-SQL.
- **Competitors:** Snowflake Intelligence, Databricks Genie, Hex, ThoughtSpot Spotter, Julius, Collate. **Incumbents may lose because** dashboards stop being the unit of value. However, warehouse vendors own the data gravity.
- **Wedge:** answering questions across warehouses (Snowflake plus Postgres plus SaaS). **Integration:** days. **Pilot:** answer 200 real Slack questions and measure accuracy against analysts.
- **Pricing:** platform fee plus usage. **Expansion:** agent-to-agent data API. **Moat:** 10 customers: none; 100: semantic templates; 1,000: benchmark corpus.
- **$10B case:** becomes the default way people consume data. **One-liner:** "Kepler for companies without OpenAI's data team."
- **Scores:** Market 9, Transformation 8, Urgency 6, Why-now 7, Buyer reach 7, Pilot speed 7, Integration 7, Competitive opening 3, Differentiation 3, Expansion 7, Moat 3, VC 5 → **avg 6.0**. Warehouse vendors absorb it; same failure mode as killed thesis M.

## Thesis 2 — Agent SOC replaces SIEM console + Tier-1 MSSP
- **Category:** SIEM/SOAR/MDR, about $25B. **Old assumption:** humans triage every alert. **Breaks:** an LLM with company context gives each alert a disposition and a confidence score.
- **New category:** an autonomous triage layer that reads any SIEM and pulls context from Slack, docs, code and the warehouse (the Anthropic CLUE pattern).
- **Buyer:** CISO / SOC lead. **Pain:** alert volume, and analysts are expensive.
- **Evidence:** Anthropic CLUE Triage; AI-attacker why-now (round 13); Google/CrowdStrike/Microsoft agents; Dropzone/Prophet/7AI funding (from round-13 notes); MDR price pressure.
- **Competitors:** Dropzone, Prophet Security, 7AI, Torq, Exaforce, CrowdStrike, Google SecOps. **Wedge:** context sources outside security (Slack/code). **Integration:** days. **Pilot:** shadow-triage 30 days of alerts.
- **Pricing:** per alert or per endpoint. **Moat:** low (the model plus connectors are commodity).
- **One-liner:** "Tier-1 SOC as software."
- **Scores:** 8, 8, 8, 8, 6, 8, 7, 2, 3, 6, 3, 4 → **avg 5.9**. Crowded with 10+ funded vendors.

## Thesis 3 — AI SRE replaces observability dashboards + on-call
- **Category:** observability plus incident management, about $50B. **Old assumption:** humans read dashboards at 3am. **Breaks:** an agent queries telemetry through MCP and writes the root-cause analysis; the dashboard becomes an API.
- **New category:** "investigation engine" priced per incident resolved. Telemetry storage becomes cheap and commodity.
- **Buyer:** VP Infra / SRE lead. **Evidence:** Stripe O11yCon 2026 agent; Resolve $125M at $1B (Feb 2026) and a later report of $1.5B valuation (https://www.beri.net/article/resolve-ai-190m-ai-sre-production-incidents-2026, *details unverified*); Traversal $48M; Cleric seed (Dec 2025); Datadog Bits AI; New Relic 2026 forecast (24.6% run agents unmonitored).
- **Wedge/integration:** read-only MCP into existing telemetry; days. **Pilot:** replay the last 20 incidents.
- **Moat:** incident-graph data, but Resolve already has it. **One-liner:** "Your on-call's first responder is software."
- **Scores:** 9, 8, 7, 8, 6, 7, 7, 2, 3, 7, 4, 4 → **avg 6.0**. Category formed and unicorn-led.

## Thesis 4 — Governed substrate for employee-built software ("the road, not the vehicles")
- **Category:** low-code/internal tools plus long-tail SaaS seats. That long tail is the $100B+ of SaaS sold per seat.
- **Old assumption:** software output is scarce, so companies buy SaaS per employee. **Breaks:** employees vibe-code replacements in days. 35% have already replaced a SaaS tool, and 60% shipped outside IT.
- **New category:** an internal app platform that provides identity, data access scopes, hosting, audit and lifecycle for agent-built apps and agents. Platform teams own "the road."
- **Buyer:** VP Platform / CIO. **Pain:** shadow apps holding production data credentials; duplicate builds.
- **Evidence:** Retool report (Feb 2026); WorkOS "person with the problem builds the tool"; Stripe Toolshed / DoorDash gateway (round 8); Anthropic lawyers and marketers building tools; Klarna consolidation.
- **Competitors:** Retool, Replit/Lovable enterprise governance (killed thesis F), Vercel, Superblocks, Microsoft Power Platform. **Incumbents may lose:** per-seat SaaS revenue erodes. But the platforms already ship governance.
- **Wedge:** inventory and govern the shadow apps that already exist. **Integration:** hours (SSO plus repo scan). **Pilot:** find 50 shadow apps and their credentials.
- **Moat:** low to medium. **One-liner:** "Okta plus Heroku for the apps your employees' agents write."
- **Scores:** 9, 9, 6, 8, 6, 7, 7, 3, 4, 8, 4, 6 → **avg 6.4**. This is thesis F (killed at 5.7) rebuilt as a platform-team buy rather than a security buy. Only a modest change.

## Thesis 5 — Agent-assignable work queue replaces Jira/ServiceNow ticketing
- **Category:** ITSM plus work management, about $25B. **Old assumption:** tickets are worked by humans, priced per agent seat. **Breaks:** coding and ops agents pick up tickets, and support conversations become issues automatically.
- **New category:** a queue where agents are first-class assignees with SLAs, verification, and cost per resolution.
- **Buyer:** VP Eng / IT. **Evidence:** Linear for Agents plus Triage Intelligence (Dec 2025); background agents at 14+ companies (round 8) take tickets from Slack/GitHub; ServiceNow internal pilots (https://www.aol.com/news/servicenow-uses-internal-ai-pilots-145033408.html); internal AI helpdesks resolve about 40% (unthread/rework snippets); Zendesk Sell sunset in 2027.
- **Competitors:** Linear, Atlassian Rovo, ServiceNow, Siit, Unthread. **Moat:** low. Incumbents add an "assign to agent" button.
- **Scores:** 8, 7, 5, 7, 6, 7, 7, 2, 2, 6, 3, 3 → **avg 5.25**. Incumbents can add it trivially.

## Thesis 6 — Non-human workforce IGA (agent identity lifecycle)
- **Category:** IGA/workforce IAM, about $20B. **Old assumption:** every identity comes from HR. **Breaks:** agents get deployed without HR, IT or provisioning.
- **New category:** joiner/mover/leaver for agents, with owner, scope, expiry and access review.
- **Evidence:** Techzine identity puzzle; Okta for AI Agents EA; WorkOS vs Okta agent identity; Okta guardrails podcast (DX); internal gateways at DoorDash/Stripe (round 8).
- **Competitors:** Okta, SailPoint, Astrix, Oasis, Aembit, WorkOS, Microsoft Entra Agent ID. Thesis T4 and round-7 MCP OAuth were already killed.
- **Scores:** 8, 8, 7, 8, 6, 6, 6, 2, 3, 7, 4, 4 → **avg 5.75**.

## Verdict
No thesis clears the bar (best is 6.4, thesis 4). The structural finding is useful negative data. AI-native companies do not replace the incumbent's system of record. They put an agent over it, which turns the incumbent's GUI and per-seat layer into an API. Every such agent layer was already funded by October 2026. Pursue one only if the founders' proprietary access changes the competitive-opening score. The one non-obvious angle is thesis 4's "platform team owns the road" buyer: a budget forming in 2026 that is distinct from security.
