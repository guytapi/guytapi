# DD: "Outcome Desk": ITSM rebuilt as an approved-outcome system of record
Round 31 deep dive. It merges T6 Thesis 2 ("service desk with no tickets", 6.5) with T5-3 ("attention router / approval exchange", 6.8). Date: 2026-10-06. I ran 10 WebSearches; WebFetch was blocked. Every URL below came from search results, and I did not read the full pages, so treat the details as secondary.

## Thesis under test
ITSM (ServiceNow, $10B+) is built around tickets that humans work. When agents do the work, the unit of work becomes an *approved outcome*: an intent, a policy check, an execution, evidence, and a human sign-off only when needed. So ITSM should be rebuilt as an outcome and approval system of record, priced per outcome rather than per fulfiller seat.

## Evidence gathered (searched in this round)
1. **Serval** raised a $75M Series B led by Sequoia at a $1B valuation, up from a $232M valuation in Aug 2025. Total raised is $127M. Its CEO says customers are "replacing incumbent systems of record". Customers automate 50%+ of tickets. It uses a Helper agent plus a Builder agent that writes TypeScript workflows. Sources: https://siliconangle.com/2025/12/12/serval-raises-75m-1b-valuation-automate-help-desk-request-processing/ , https://www.bloomberg.com/news/audio/2026-04-21/tech-disruptors-serval-ceo-on-replacing-legacy-itsm , https://sacra.com/c/serval
2. **Ravenna** ($15M, Khosla/Madrona) sells a full internal-support platform replacement. **Console** ($6.2M, Thrive) works as middleware on top of an existing ITSM. Sources: https://ravenna.ai/blog/ravenna-raises-15m-to-build-the-future-of-internal-support , https://techcrunch.com/2025/06/02/console-raises-6-2m-from-thrive-to-free-it-teams-from-mundane-tasks-with-ai
3. **ServiceNow** pricing is still per fulfiller seat: roughly $80-200 per fulfiller per month, plus $50-100+ per fulfiller for Now Assist. Agentic features sit only in Enterprise Plus. These are third-party estimates. Source: https://redresscompliance.com/servicenow-itsm-pricing-2026
4. At **ServiceNow Knowledge 2026**, AI Control Tower was extended to govern AI "regardless of where it runs". The release added "intelligent approvals". ServiceNow also opened flows, approvals, catalogs and audit trails to any external agent over MCP, a bid to become the common execution layer. It integrated with Microsoft Agent 365 and with Veza. Sources: https://www.efficientlyconnected.com/servicenow-knowledge-2026-agentic-ai-platform/ , https://nasdaq.com/press-release/servicenow-expands-ai-agent-governance-through-deeper-integration-microsoft-2026-05
5. **Microsoft Agent 365** went GA on May 1 2026 at $15 per user per month and is bundled in E7 at $99. It covers a registry, approval and publication workflows, lifecycle management, and sync with AWS and GCP. Source: https://www.epcgroup.net/blog/microsoft-agent-365-general-availability-may-2026-registry-sync-aws-google-cloud
6. **Atlassian** put Rovo Agents in Jira and JSM (Feb 2026). They resolve requests in the portal or Slack without a human step. Source: https://businesswire.com/news/home/20260224033792/en/Atlassian-Introduces-Agents-in-Jira-to-Drive-Human-AI-Collaboration-at-Enterprise-Scale
7. **Freshservice** includes the Freddy AI Agent in Enterprise with 1,200 sessions per license per year, and charges for overages. That is a seat-plus-usage hybrid. Source: https://www.eesel.ai/blog/freshservice-freddy-ai-pricing
8. **UiPath Action Center** (Apr 2026 release) lets agents escalate to humans through escalation apps. Agentic Orchestration (BPMN/DMN) covers third-party agents. Source: https://docs.uipath.com/action-center/automation-suite/2.2510/release-notes/2-2510-2
9. Earlier in this repo: ServiceNow bought Moveworks for $2.85B, and STATUS.md killed H, the cross-vendor human decision layer (HumanLayer pivoted; approvals went native).

---

## Role 1: Technical architect
**What has to exist:**
- An **intent object**: requester (human or agent identity), desired end state, scope, and expiry.
- A **policy engine**: who must approve, under which risk tier, or whether it is auto-granted. Use OPA/Cedar-style rules.
- An **executor**: idempotent connectors to Okta/Entra, Jamf/Intune, GitHub, AWS, Google Workspace and SaaS admin APIs.
- **Verification**: re-read the target system's state after execution. This is the key part. An "outcome" only counts if the state is observed to have changed.
- An **evidence ledger**: append-only and signed, holding the intent, the approvals, the actions and the observed end state.
- An **approval surface** in Slack/Teams, plus an MCP endpoint so external agents can submit intents.

**Hard parts:**
1. Connector breadth (a long tail of SaaS admin APIs).
2. Rollback and compensation for partial failure.
3. Verifying a state change in systems with eventual consistency.
4. Identity of agent requesters, which depends on Entra/Okta agent IDs.

**Honest read:** this is buildable in 6-9 months by a strong team. But it is *exactly* what Serval already builds: a Builder agent generates the workflow code and a Helper agent executes it. It is also what ServiceNow exposed over MCP (flows, approvals and audit for external agents). The architecture has nothing new except "verify the end state and store it as the record". That is a feature, and incumbents can add it in a quarter.

## Role 2: Skeptical CIO/CTO (2,000-employee company)
- "I don't buy a 'system of record for outcomes'. I buy fewer tickets and a smaller headcount. Serval, Ravenna, Rovo and Freddy all promise 50%+ deflection now."
- "Approvals aren't my bottleneck. Provisioning sprawl is. My approvals already live in Slack, in Okta Access Requests, and in Teams through Agent 365."
- "Replacing ServiceNow means re-platforming the CMDB, change, audit and SOX evidence. That's 12-18 months. I'd only do it for a vendor with real scale, which today means Serval."
- "Per-outcome pricing makes my bill unpredictable. Finance prefers seats or capped usage, which is what Freshservice does."
- "Agent-originated requests (coding agents asking for access) are real but small for us today. They go through our IdP's JIT access, not the service desk."
- **Would buy:** cheaper, AI-first ITSM with proven deflection. **Would not buy:** a new abstraction layer.

## Role 3: Top-tier VC partner
- **Category:** real and huge. Sequoia's Serval bet is the market validating the thesis. That cuts both ways, because the obvious winner is already funded at $1B, with Ravenna, Console, Atomicwork and Aisera behind it.
- **Differentiation test:** "What do you do that Serval can't ship in 90 days?" The approval/outcome ledger fails this test. The merged T5-3 half was already killed as H.
- **Pricing-model wedge:** per-outcome pricing is the only structural angle, because ServiceNow's fulfiller-seat revenue resists it. But challengers can price this way freely, so it is no advantage against them. Freshworks is already moving to hybrid pricing.
- **Would fund?** Not as stated. The firm would only look at a sharply different wedge with an unfair distribution channel (see the sharpened thesis). Pass for a seed/A as an "outcome desk".

## Role 4: Competitor analyst
| Player | Position vs thesis | Threat |
|---|---|---|
| ServiceNow (+Moveworks) | AI Control Tower governs any agent. Flows, approvals and audit exposed over MCP. Intelligent approvals. Seat model is a weakness, but it will tolerate cannibalizing seats to defend the Fortune 2000 | Very high in the enterprise |
| Serval ($1B, Sequoia) | Already the AI-native "agents do the work" ITSM. Code-generated workflows. Replacing systems of record at mid-market and growth companies | Fatal for a new entrant on the same wedge |
| Atlassian JSM + Rovo | Agents resolve in the portal and Slack. Bundled with Jira for engineering-led mid-market | High |
| Freshworks Freddy | Enterprise bundle plus session usage. Price-led mid-market | Medium |
| Ravenna / Console | Slack-native full desk / overlay. Well funded at seed-A | Medium; crowds the opening |
| UiPath Action Center | Human escalation for any agent, plus BPMN orchestration. Owns the "approval exchange" story in ops | High for the T5-3 half |
| Microsoft Agent 365 | Registry plus approvals at $15/user, in E7. Owns the Teams approval surface | High for the T5-3 half |

**Structural gaps that remain:**
- (a) No one owns **requests that originate from agents**, verified across IdP, cloud and SaaS, with signed evidence for auditors.
- (b) No one offers a **neutral outcome ledger** across ServiceNow, Serval and agent vendors.
- Gap (b) is the H thesis, which is already dead. Gap (a) is narrow and sits next to Okta/Entra agent identity (T5-2 / Thesis 6).

## Self red-team
- **"The ticket is dead" is overstated.** Serval and Rovo still keep tickets as the record and just automate them. The unit doesn't need to change for the value to be captured, so the "new category" is marketing.
- **Incumbents adding it trivially** is a kill criterion and is close to true. ServiceNow shipped governance plus approvals plus MCP. Microsoft and UiPath shipped HITL routing.
- **Switching advantage** is real (cost, speed), but it goes to the leader, Serval, not to a new entrant.
- **Urgency** is real for deflection. It is weak for "outcome records".
- **Wedge** needs enterprise adoption (re-platforming the system of record), which is another kill criterion.
- **Steelman:** auditors (SOX/SOC 2) may come to require evidence of what agents changed and who approved it. A verified-outcome ledger could become a compliance product. The counter: GRC tools (Vanta/Drata) and ServiceNow IRM sit closer to the auditor.

## Final sharpened thesis (brief format)
**Shape:** ITSM ($15B+) works as a ticket queue that fulfiller seats work through, because it assumed humans file and fix requests. Agents now do both, so the record should be a *verified outcome* (intent, policy, execution, observed end state, approvals by exception) rather than a ticket.
- **Existing category:** ITSM/ESM. **Market:** ServiceNow around $13B revenue (inferred); ITSM+ESM $20B+.
- **Old assumption:** humans request, humans fulfil, billing per fulfiller.
- **Why AI breaks it:** 50%+ of L1 is auto-resolved (Serval). Requesters are increasingly agents. Seats shrink.
- **New category:** an outcome desk, which is a policy-bound executor plus a verified-outcome ledger.
- **Product:** "Requests from people and agents get executed under policy. Each one ends with proof the state actually changed. Humans approve only the exceptions."
- **Buyer:** VP IT / CIO at 300-3,000-employee companies. **Pain:** ServiceNow cost, L1 headcount, audit evidence for agent actions.
- **Evidence:** signals 1-8 above.
- **Workaround:** Serval, Rovo, Freddy, Okta Workflows, Slack bots.
- **Competitors:** Serval, Ravenna, Console, Atomicwork, Aisera (direct); ServiceNow+Moveworks, JSM Rovo, Freshservice, UiPath Action Center, Agent 365 (adjacent and incumbent).
- **Why incumbents may lose:** seat revenue. This holds only against ServiceNow, not against Serval.
- **Narrowest viable wedge (if pursued at all):** *agent-originated access and infra requests* (coding agents, ops agents) with signed evidence for SOC 2. Sell to platform and security engineering, not IT.
- **Integration:** days. **Pilot:** 30 days. Measure the % of agent requests auto-executed with verified end state, and audit-evidence completeness.
- **Pricing:** per verified outcome plus a platform fee. **Expansion:** human requests leading to full ITSM, then change management.
- **Moat:** 10: none; 100: policy/runbook library; 1,000: audit-evidence standard (speculative).
- **$10B case:** displace ServiceNow below the Fortune 500. Serval is already the favourite to do this.
- **CTO one-liner:** "Every request from a person or an agent gets done under policy, and the record proves it."

### Revised scores
| Mkt | Transf | Urg | Why-now | Reach | Pilot | Integ | Opening | Diff | Expand | Moat | VC | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 9 | 7 | 6 | 7 | 5 | 6 | 6 | 2 | 3 | 7 | 4 | 4 | **5.5** |

Compared with the inputs: Opening drops from 4 to 2 (Serval at $1B, Ravenna and Console funded, ServiceNow MCP plus Control Tower, Agent 365 and UiPath HITL). Diff drops from 5 to 3 (the outcome ledger is a feature). VC drops from 6-7 to 4. The T5-3 approval half adds nothing because it is a re-run of the killed H.

## Verdict
**KILL** (5.5, below 6.5 and 6.8). The merge combines one thesis that the market already validated *and funded a winner for* (Serval, Sequoia, $1B) with one thesis this repo already killed (H, the approval layer). The kill criteria apply: incumbents and the leader can add "outcome records" trivially, and a system-of-record wedge needs enterprise re-platforming. STATUS.md lesson #2 applies directly: AI-native money goes to layers that avoid migration, and Serval has already taken the migration bet.

**Only residual worth noting:** agent-originated access and infra requests with verified-outcome evidence. It is better re-filed under T5-2 (per-task mandates / agent identity) than as an ITSM replacement.

**STATUS.md line:** `Outcome desk (ITSM as approved-outcome SoR, merged T6-2+T5-3) | 5.5 | Serval $1B Sequoia already replacing ITSM SoR; Ravenna/Console funded; ServiceNow Control Tower+MCP approvals, Agent 365, UiPath Action Center own approvals; approval half = killed H`
