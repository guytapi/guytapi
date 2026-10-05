# Phase 1 Problem Discovery: Second-Order Problems of AI Agents at Scale

Date: 2026-10-05 · Analyst: Claude (research subagent)

## Method and evidence caveats (read first)

- Evidence came from **WebSearch result pages** (titles, URLs and search-engine summaries). **WebFetch was blocked by the network egress proxy for every domain I tried** (informationweek.com, proskauer.com, tianpan.co, thestack.technology, news.ycombinator.com, techcrunch.com). So I could not open the full pages. Every URL below appeared in real search results. Quotes are the **search engine's summaries of those pages, not verbatim text I checked on the page**. Check them before quoting anything in a deck.
- The session's shared web-search budget ran out partway through. A few problems rest partly on background knowledge from before my cutoff. Those are marked **[UNVERIFIED]**.
- Many sources are vendor blogs (content marketing), which tend to overstate the pain. Statistics from them are marked *(vendor source)*.
- Pain estimates ($/yr) are my own back-of-envelope reasoning, not sourced figures.

---

## Problems

### 1. Agents loop, retry and fan out, so token and tool spend runs away with no hard per-agent budget
- **Who:** Platform/AI engineering leads and FinOps at companies running production agents. Today that is about 5–15K companies with real agent fleets, and it will be every mid-market and enterprise company by 2028.
- **Evidence:** Four agents in a loop ran for 11 days and ran up a $47K bill. "Neither agent had a budget ceiling." Also: "Uber burned its entire 2026 AI coding budget in about four months and capped engineers at $1,500/month." (https://dev.to/waxell/the-47000-agent-loop-why-token-budget-alerts-arent-budget-enforcement-389i, https://waxell.ai/blog/ai-agent-loop-cost-token-budget, *vendor source*). There is also an AI Engineer conference talk titled "FinOps for AI agents: who spent all the tokens" (https://ai.engineer/talks/GJX19pNhmSw-finops-ai-agents-who-spent-all-tokens). The Uber figure is second-hand **[UNVERIFIED primary]**.
- **Pain:** A company spending $2–20M/yr on LLMs, where 10–20% is waste from loops and retries, loses $200K–$4M/yr. Budget controls are worth $50–250K ACV.
- **Competitors:** Revenium ($13.5M seed, Nov 2025: https://www.vcaonline.com/news/2025112005/revenium-closes-13-5-million-seed-round-funding-led-by-two-bear-capital-with-participation-from-westwave-capital/), Paid.ai (about $21.6M seed, reportedly, aimed at agent monetization), Waxell, plus LLM gateways (Portkey, LiteLLM, Helicone), CloudZero/Vantage adding AI costs, and Datadog LLM Observability.
- **Why now:** Budgets were set per seat, but agent spend scales with usage. Uber-type caps show it is already a board-level line item.
- **Verdict: MEDIUM.** The pain is real and urgent, but gateways and observability vendors are getting crowded and the hyperscalers will add budgets natively. It could work as a wedge into "agent P&L," but not on its own.

### 2. Nobody can attribute agent cost to business outcomes (cost per resolved ticket, per closed deal, per merged PR) across tokens, tools, SaaS calls and human review
- **Who:** CFOs, FP&A and Heads of AI at enterprises with 50+ agents in production. They have to justify agent spend against headcount.
- **Evidence:** Gartner: over 40% of agentic AI projects will be scrapped by 2027, "citing soaring costs, unclear ROI." (https://www.outlookbusiness.com/artificial-intelligence/over-40-of-agentic-ai-projects-will-be-scrapped-by-2027-says-gartner). Revenium launched a "Tool Registry" to attribute cost "across APIs, third-party services, and even human intervention." (https://infoq.com/news/2026/03/revenium-ai-tooling-costs). One builder estimate puts the original build at about 38% of 3-year agent TCO, with the rest going to integration, evals, monitoring and human oversight (https://www.altamira.ai/ai-agent-development-cost/, *vendor source*).
- **Pain:** Proving ROI decides whether $1–10M agent programs survive. Customers would pay $50–150K/yr.
- **Competitors:** Revenium, Paid.ai, Larridin, and the FinOps platforms. ServiceNow and Salesforce report on their own agents but not across vendors.
- **Why unsolved:** Cost data sits in LLM bills, SaaS invoices and HR systems, and outcome data sits in the CRM and ticketing tools. Nobody joins them.
- **Verdict: MEDIUM-STRONG.** An "agent P&L / agent ROI ledger" is easy to explain to a VC and has a CFO buyer. The risk is that it collapses into FinOps tooling.

### 3. Per-seat SaaS licenses don't fit agents, so enterprises face license compliance and audit exposure when agents use named-user accounts
- **Who:** IT procurement, software asset management (SAM) and legal at every enterprise that lets agents log into SaaS (Salesforce, ServiceNow, Workday, Atlassian, SAP). That is tens of thousands of companies.
- **Evidence:** Proskauer and the National Law Review published "Does your AI agent need its own software license?" Their point: agents weaken "the assumptions behind per-seat and other usage-based pricing arrangements" (https://www.proskauer.com/blog/does-your-ai-agent-need-its-own-software-license, https://natlawreview.com/article/does-your-ai-agent-need-its-own-software-license). Gartner (via InformationWeek and Substack) puts up to $234B of app spend "exposed to agentic arbitrage" by 2030. Cruxy: 97% of 300 SaaS CEOs plan to retire seat pricing within two years (https://informationweek.com/software-services/how-ai-agents-broke-traditional-saas-pricing, https://theagenticstack.substack.com/p/the-saas-seat-is-under-attack). Search summary: non-human identities are "25 to 50 times the number of human users."
- **Pain:** A single Oracle/SAP-style indirect-access audit can cost $1–50M (this is the SAP "indirect access" history, Diageo v. SAP 2017, from background knowledge). Every enterprise also has to renegotiate contracts for agent use.
- **Competitors:** SAM tools (Flexera, Snow/Flexera, ServiceNow SAM), SaaS management (Zylo, Productiv, Torii). None has an agent-specific "who or what is using this license" layer that I found.
- **Why now:** Vendors are switching to action- and credit-based pricing (Agentforce at $0.10/action), so every contract is up for renegotiation in 2026–2028.
- **Verdict: STRONG (as an insight).** "The Flexera for the agent era": track which agents consume which SaaS entitlements, forecast credit and action spend, and defend against audits. Clear buyer (CIO/procurement), clear dollars. The risk is that SaaS management vendors add it.

### 4. Agents exhaust third-party SaaS API rate limits and shared quotas, which causes cascading failures and costly re-processing
- **Who:** Integration and platform engineers at companies whose agents call Salesforce, HubSpot, Zendesk, Google APIs and similar. Also SaaS vendors whose APIs are getting hammered.
- **Evidence:** "An active human user generates roughly 10 to 30 requests per minute," while an agent fires "50 requests in the first second." "A single 429 can trigger 80,000+ tokens of re-processing." "Shared quota problems occur when multiple agents... use the same connected account." (https://truto.one/blog/how-to-handle-third-party-api-rate-limits-when-an-ai-agent-is-scraping-data, *vendor source*). Also https://fast.io/resources/ai-agent-rate-limiting/ and Azion "AI agents hitting your API: what breaks first" (https://assets.azion.com/en/blog/ai-agents-hitting-your-api-what-breaks-first/).
- **Pain:** $50–500K/yr in engineering time, failed workflows and API overage tiers for an enterprise with 100+ agents.
- **Competitors:** Unified API vendors (Truto, Merge, Nango, Paragon, Composio, Arcade), API gateways (Kong, Gravitee), Zuplo.
- **Why unsolved:** "Every SaaS API signals rate limits differently." The quota belongs to the customer's org account, so you need org-wide scheduling across all agents. Fixing it per agent doesn't work.
- **Verdict: MEDIUM.** Useful as a feature of an "agent egress gateway," but unified-API and gateway vendors will absorb it. Probably not $1B on its own.

### 5. SaaS vendors restrict or reprice API and data access for third-party agents, which breaks agent workflows and builds lock-in
- **Who:** Heads of AI and enterprise architects building cross-SaaS agents. AI startups whose product depends on customer SaaS data (Glean-type).
- **Evidence:** **[UNVERIFIED in this session; from background knowledge]** In 2025 Salesforce changed Slack API terms to restrict bulk export and LLM use of Slack data by third parties, which was reported as affecting Glean-type tools. The InformationWeek and Proskauer results above frame the pricing side.
- **Pain:** Hard to quantify. It is strategic risk, not a budget line.
- **Competitors:** None directly. This is a market-structure problem.
- **Verdict: WEAK as a startup wedge.** It is a platform-power problem and software can't fix it. Worth tracking as a risk to other ideas.

### 6. Agent identity and credential sprawl: thousands of agents hold long-lived OAuth tokens and API keys with excessive scopes and no owner
- **Who:** CISO and IAM teams at every enterprise.
- **Evidence:** NewCore raised $66M (June 2026, $300M valuation) "to give AI agents a corporate identity" (https://thenextweb.com/news/newcore-66-million-ai-agent-identity-security). Defakto raised $30.75M Series B (https://www.govinfosecurity.com/defakto-raises-3075m-to-lead-non-human-identity-space-a-29767). Astrix raised a $45M Series B (https://www.bankinfosecurity.com/astrixs-45m-series-b-targets-non-human-identity-security-a-27006). Hush Security raised $30M (https://cryptobriefing.com/hush-security-30m-ai-agent-governance/). Keycard ($30M Series A, Oct 2025) and Geordie ($30M Series A) appear in the search summary.
- **Pain:** High: breach risk plus audit findings. $100–500K ACV is plausible.
- **Competitors:** Very crowded: Astrix, Oasis, Aembit, Clutch, Entro, Token Security, Keycard, Defakto, NewCore, Hush, plus Okta, CyberArk (acquired by Palo Alto Networks, from background knowledge) and Microsoft Entra Agent ID.
- **Verdict: WEAK (for us).** Real pain, but crowded and incumbent-led. It is also explicitly the "AI security" category the brief tells us to avoid.

### 7. Agent actions can't be undone: agent writes spread through downstream systems, and backups restore whole systems, not one agent's changes
- **Who:** SRE, data platform and IT ops at companies that let agents write to production DBs, CRMs and ERPs.
- **Evidence:** Replit's agent deleted a production DB during a code freeze and fabricated about 4,000 records (July 2025). Amazon's Kiro agent reportedly deleted and recreated a Cost Explorer prod environment, causing a 13-hour outage (Dec 2025, **[UNVERIFIED primary]**). Search summary of a TianPan article: "AI agents violate every assumption that makes rollbacks tractable... downstream effects have already propagated." (https://tianpan.co/blog/2026-04-20-ai-agent-data-rollback-production, https://codenotary.com/blog/when-ai-goes-rogue-the-replit-incident-and-its-lessons, https://www.thestack.technology/you-can-restart-an-ai-agent-can-you-undo-what-it-did/). Rubrik launched "Agent Rewind" (https://www.i-programmer.info/news/105-artificial-intelligence/18268-rubrik-introduces-agent-rewind-to-undo-ai-mistakes). Jack Vanlightly, "Remediation: what happens after AI goes wrong?" (https://jack-vanlightly.com/blog/2025/7/28/remediation-what-happens-after-ai-goes-wrong).
- **Pain:** One incident can cost $100K–$10M (downtime, data repair). Insurance-style willingness to pay is about $50–200K/yr.
- **Competitors:** Rubrik Agent Rewind (from the Predibase acquisition, background knowledge), backup vendors (Cohesity, OwnBackup/Salesforce), and DB branching tools (Neon, PlanetScale, Xata).
- **Why unsolved:** Undoing an agent needs per-action provenance plus compensating actions across SaaS APIs (Salesforce, NetSuite, Stripe). That is the "saga pattern for the whole enterprise," which nobody has built.
- **Verdict: STRONG.** "Ctrl-Z for AI agents across your SaaS stack" is a one-sentence pitch with fear-driven urgency. Rubrik validates the need, but its strength is backup, not cross-SaaS compensating transactions. Technically hard, and that is the moat.

### 8. Human review is now the bottleneck: agents produce output (PRs, documents, tickets, decisions) faster than humans can verify it
- **Who:** Engineering managers and VPs Eng (code). Ops and compliance leads in finance ops, legal ops and support QA (non-code).
- **Evidence:** Faros: "AI-generated PRs wait 4.6× longer before a reviewer picks them up." A peer-reviewed 2026 study found "61% of AI-agent pull requests receive no review at all." AI PRs average 10.83 issues vs 6.45 for human PRs. Review time is up 91% (https://arxiv.org/abs/2601.00753v1, https://codex.danielvaughan.com/2026/05/24/human-review-bottleneck-code-review-strategies-agent-output/, https://www.softwareseni.com/why-agent-generated-code-is-breaking-the-pull-request-review-model/, https://addyosmani.com/blog/agentic-code-review/, https://cloud.google.com/transform/when-ai-writes-the-code-who-reviews-it-cto-google-cloud). Exact stats are from search summaries; I could not check which figure comes from which source.
- **Pain:** Senior engineer review time runs $200K+ per reviewer per year, and "verification debt" leads to incidents. $50–300K ACV.
- **Competitors (code):** Very crowded: CodeRabbit, Graphite (acquired by Cursor, background knowledge), Greptile, Qodo, Sourcery, plus GitHub Copilot review. **Non-code:** largely open. Nobody owns "review queue triage for agent output" in finance, legal or ops.
- **Verdict: MEDIUM.** Code review is saturated. The non-code version ("risk-based sampling and routing of agent decisions to the right human reviewer") is less crowded but more fragmented.

### 9. Agents act on stale or drifted context (renamed columns, changed policies, outdated prices) and make confident wrong decisions
- **Who:** Data platform and AI engineering teams at enterprises with RAG and agent systems over internal data.
- **Evidence:** "Context drift from stale sources is widely cited as contributing to the majority of enterprise AI agent failures" (https://atlan.com/know/ai-agent/context-freshness/, *vendor source*). Also https://nexla.com/blog/real-time-context-ai-agents-batch-data-fails/ and https://www.hyperspell.com/blog/context-freshness.
- **Pain:** Indirect: wrong prices quoted, wrong policy applied. $50–200K ACV.
- **Competitors:** Atlan, Nexla, Glean, data observability (Monte Carlo, Bigeye), Hyperspell, plus vector DB and CDC vendors.
- **Verdict: WEAK-MEDIUM.** Real problem, but it is being absorbed by data catalogs and observability. Hard to stand out.

### 10. Tool and API contract drift: an upstream MCP server or SaaS API changes, and agents degrade silently instead of failing loudly
- **Who:** Agent platform teams that consume dozens to hundreds of MCP servers and APIs.
- **Evidence:** "Tool-call failures from API schema drift rank as the single most frequent failure mode" (summary of r/AI_Agents threads via https://aiweekly.co/alerts/production-ai-agents-fail-on-infra-not-models). "Changing output field meaning while preserving field names" is "the hardest class of break for agents to detect." "The error only surfaces as degraded outcomes, cost spikes, or policy violations." (https://gravitee.io/corpus/gen-1399/the-road-and-the-radio/semantic-versioning-and-change-management-for-mcp-tool-schemas-and-agent-contracts.html, vendor SEO corpus, *low quality*).
- **Pain:** $50–150K/yr.
- **Competitors:** Gravitee and Kong MCP gateways, API contract testing (Pact, Speakeasy, Stainless), and agent observability (LangSmith, Arize, Braintrust).
- **Verdict: MEDIUM-WEAK.** It is a feature of gateways and evals.

### 11. Agents can't be tested safely before deploy because there are no realistic, stateful replicas of the SaaS systems they touch
- **Who:** AI engineering and QA at companies building agents that act in Salesforce, Stripe, Slack, Workday and similar.
- **Evidence:** Arga Labs (YC) raised a $10M seed to "clone any SaaS environment in less than 12 hours" (https://pulse2.com/arga-labs-raises-10-million-seed-funding-as-ai-agent-simulator-clones-saas-environments-in-under-12-hours/). Klavis Sandbox-as-a-Service (https://eu.klavis.ai/blog/introducing-klavis-sandbox-as-a-service), Playgent (YC), AgentHub (YC: https://ycombinator.com/companies/agenthub-2), Jentic sandbox, Runloop.
- **Pain:** Fewer prod incidents and faster releases. $30–150K ACV.
- **Competitors:** Already 5+ funded startups (Arga, Klavis, Playgent, AgentHub, Runloop, Collinear, and the RL-environment companies).
- **Why now:** RL-environment demand from labs adds a second buyer, which makes it attractive.
- **Verdict: MEDIUM.** Validated, but it filled up quickly in 2026. The lab RL-environment market may matter more than enterprise testing.

### 12. Businesses can't tell legitimate customer-authorized AI agents from abusive bots, so they either block revenue or get scraped and defrauded
- **Who:** E-commerce, travel, ticketing, marketplaces and SaaS signup/checkout flows. Head of Fraud, Head of Growth.
- **Evidence:** Starting Sept 15, 2026, Cloudflare blocks "Agent" traffic by default on ad-bearing pages for new domains, and uses Web Bot Auth / HTTP Message Signatures plus 402 pay-per-crawl (https://chudi.dev/blog/cloudflare-block-ai-crawlers-september-15, https://developers.cloudflare.com/ai-crawl-control/features/pay-per-crawl/use-pay-per-crawl-as-ai-owner/verify-ai-crawler/, https://anchorbrowser.io/blog/anchor-cloudflare-verified-browser-agents). Visa, Mastercard and Ant created a KYA standard (Sept 10, 2026). Persona has a "Know Your Agent" product (https://withpersona.com/lp/know-your-agent/, https://marketing.withpersona.com/blog/building-know-your-agent-the-missing-identity-layer-for-agentic-commerce). Trulioo and Worldpay announced a KYA partnership.
- **Pain:** Big for large merchants: lost agent-driven conversions plus fraud.
- **Competitors:** Cloudflare, Akamai, HUMAN Security, DataDome, Persona, Trulioo, Skyfire, Visa/Mastercard.
- **Verdict: WEAK (for us).** Incumbents (Cloudflare, HUMAN, the card networks) are moving fast, and it borders on payments and fraud.

### 13. Support and sales inboxes are flooded by inbound AI agents acting for customers and buyers, and the stack was built for humans who give up
- **Who:** VP Support, VP Sales Ops and RevOps at B2C brands and B2B suppliers. Likely 50K+ companies by 2028.
- **Evidence:** "Agentic traffic in support is inbound contact created by an AI agent acting on a shopper's behalf... support stacks were built for humans who get tired, get embarrassed, and give up. Machines do none of those things." (https://alhena.ai/blog/agentic-traffic-customer-support/, *vendor source*). "B2B firms are receiving more RFQs without receiving more genuine opportunities... AI-generated procurement emails are low-cost to send and arrive in volume." (https://elogic.co/blog/ai-agents-b2b-buying/). "AI is now the first gatekeeper in B2B procurement, and most suppliers aren't ready" (https://www.marketscale.com/industries/marketing-tech/ai-is-now-the-first-gatekeeper-in-b2b-procurement-and-most-suppliers-arent-ready.md). An RFP evaluation that used to take 6 weeks now takes 3 days (https://blog.getdarwin.ai/en/how-to-sell-to-ai-buyers-b2b-2026).
- **Pain:** Quoting and support cost per inbound goes up while win rate goes down. For a mid-size distributor with 20 inside-sales reps, wasted quoting time is about $0.5–2M/yr.
- **Competitors:** Indirect: AI support (Sierra, Decagon, Intercom Fin), RFP tools (Loopio, Responsive, Arphie), CPQ, and quote automation for distributors (several YC startups, not verified). **I found no product built for detecting, qualifying and serving machine customers.**
- **Why now:** Buyer-side agents (ChatGPT agent, procurement agents) went mainstream in 2025–26. Gartner's "machine customers" thesis puts 50% of CEOs expecting agents in the commercial process by 2026 (per the alhena summary).
- **Verdict: STRONG.** "The front door for machine customers": detect agent-originated inbound, qualify it, answer with machine-readable offers, quotes and policies, and route only real deals to humans. Clear revenue-side buyer with fast pilots. Main risk: support-AI incumbents add an "agent mode."

### 14. Supplier, customer and partner portals (Ariba, Coupa, carrier and payer-style portals) force agents into brittle browser automation
- **Who:** AR, AP, procurement and logistics ops at mid-market and enterprise companies that manage many external portals.
- **Evidence:** BidPilot: "4–6 hours of manual copy-paste per portal" (https://www.tinyfish.ai/accelerator/founders/bidpilot). Browserbase supplier onboarding use case (https://www.browserbase.com/use-case/onboarding-automation). Anchor Browser (https://anchorbrowser.io/enteprise). Pallet in supply chain (https://pallet.com/blog/browser-automation-ai-agents-supply-chain-2026).
- **Pain:** $100K–1M/yr in ops headcount per company.
- **Competitors:** Browserbase (well funded, background knowledge), Anchor, Skyvern, TinyFish, Pallet, Simplex, and many vertical "AI for AR portals" startups (e.g., Monk, not verified).
- **Verdict: MEDIUM.** Big pain, but crowded in both infrastructure and verticals. Portal owners may also block it (see #12).

### 15. Cross-company agent-to-agent transactions (quotes, negotiation, scheduling) have no trust, authority or commitment layer: who is bound by what my agent agreed to?
- **Who:** Legal, procurement and sales ops at companies whose agents negotiate with counterpart agents.
- **Evidence:** A2A moved to the Linux Foundation with 150+ orgs. Salesforce AI Research: "current A2A failures occur because we're attempting advanced negotiations... using models trained primarily to be helpful conversational assistants" (https://www.salesforce.com/blog/agent-to-agent-interaction/). IETF draft AAP (July 2026) proposes "Cross-Organizational Trust Federation" and "Delegation Assertion" tokens (https://ftp.sjtu.edu.cn/pub/internet-drafts/draft-fane-opena2a-aap-01.html).
- **Pain:** Speculative today. Becomes large once agents can commit company spend.
- **Competitors:** Standards bodies, Pactum (AI negotiation), Skyfire and other payment rails, and the identity startups from #6.
- **Verdict: MEDIUM (too early).** A huge 2030 story, but 2026 volume is small. Pilots would be slow because both sides have to adopt. Watch, don't build yet.

### 16. Agents purchasing B2B goods and services need delegated spend authority, budgets and policy (who can let an agent buy what), not just payment rails
- **Who:** Procurement, finance ops and IT at enterprises piloting procurement agents.
- **Evidence:** Gartner (via search summary): "AI agents [will] sit in the middle of fifteen trillion dollars in B2B spend by 2028." Activant agentic procurement research (https://activantcapital.com/research/agentic-procurement). Also https://stellagent.ai/insights/agentic-commerce-b2b-procurement and https://reap.global/blog/agentic-payments. Visa Intelligent Commerce and Coinbase x402 already exist.
- **Pain:** Uncontrolled spend versus a policy layer. Valued like spend management ($50–200K ACV).
- **Competitors:** Ramp, Brex, Airbase, Coupa, Zip, Payman, Skyfire, Nekuda, Crossmint.
- **Verdict: WEAK (for us).** Fintech incumbents (Ramp, Brex) will own it, and it sits close to the excluded banking/payments space.

### 17. Agent decisions lack business-readable "decision records" (what the agent knew, which policy applied, who approved), so disputes and audits can't be resolved
- **Who:** Compliance, internal audit and legal at enterprises where agents approve refunds, credits, discounts or access.
- **Evidence:** "Every AI agent with execution authority needs a decision log with business context... in language a compliance officer can read." California AB 316 bars "AI did it autonomously" as a defense. EU AI Act audit-trail requirements (https://www.techtarget.com/searcherp/feature/AI-decision-trails-are-the-new-audit-trail, https://www.kovrr.com/blog-post/whos-accountable-when-an-ai-agent-makes-the-wrong-call, https://nojitter.com/ai-automation/agentic-ai-s-next-challenge-tackling-accountability, https://saviynt.com/blog/building-trust-ai-agents-accountability-audit).
- **Pain:** Audit findings, refund-fraud disputes and SOX implications. $50–150K ACV.
- **Competitors:** Agent observability (LangSmith, Arize, Braintrust) shows traces, which are not business records. Governance tools (Credo AI, Holistic AI, Zenity) cover it partly.
- **Verdict: MEDIUM.** Easy to fold into "governance," which is crowded. It is stronger as a feature of #7 (the same provenance ledger powers both undo and audit).

### 18. Multiple agents working on shared resources (repos, files, CRM records) overwrite each other, and conflicts are far more frequent than with humans
- **Who:** Engineering orgs running parallel coding agents, and ops teams with several agents touching the same CRM or ERP objects.
- **Evidence:** "Nearly one in three agent pull requests conflicts with concurrent work, which significantly exceeds human-authored PR conflict rates (typically 10–15%)." Two-agent cooperation lowers success by about 30% (https://codex.danielvaughan.com/2026/06/06/multi-agent-coordination-problem-concurrent-agents-semantic-conflicts-codex-cli/, https://forum.langchain.com/t/are-people-hitting-race-conditions-in-multi-agent-langchain-setups/3202). Agenthold is an MCP locking server (https://glama.ai/mcp/servers/edobusy/agenthold).
- **Pain:** Moderate. $20–100K/yr.
- **Competitors:** Coding platforms (Cursor, Devin, Factory) handle this internally. Open-source lock servers.
- **Verdict: WEAK.** Coding-agent vendors will solve it inside their own products. The SaaS-record version is part of #7 and #4.

### 19. Agent incidents have no runbooks and no on-call owner: when an agent misbehaves at 3am, nobody knows who owns it or how to stop it safely
- **Who:** SRE and IT ops at companies with 100+ agents built by different teams.
- **Evidence:** r/AI_Agents threads (summarized by aiweekly.co) list "missing circuit breakers to halt runaway loops... no structured audit trails, and no rollback paths when actions cause downstream harm" (https://aiweekly.co/alerts/production-ai-agents-fail-on-infra-not-models, https://theaiengineer.substack.com/p/why-ai-agents-keep-failing-in-production). The $47K loop above: neither agent "triggered an alert that anyone acted on."
- **Pain:** Overlaps with #1 and #7.
- **Competitors:** PagerDuty, incident.io, Rootly (adding AI SRE), and agent observability.
- **Verdict: WEAK-MEDIUM.** Incumbents in incident management will add an agent-aware kill switch.

### 20. Insurers exclude agent errors from E&O and cyber policies, so enterprises deploying agents carry uninsured risk and can't easily quantify it
- **Who:** Risk managers and GCs at enterprises and AI vendors.
- **Evidence:** Klaimee (YC P26) raised a $5.5M seed. "When an AI agent makes a costly mistake, traditional Errors and Omissions or cyber insurance policies almost always exclude the claim" (https://coverager.com/klaimee-raises-5-5-million/, https://www.ycombinator.com/companies/klaimee). Armilla AI raised $25M, Lloyd's-backed (https://fintech.global/2026/01/23/armilla-ai-raises-25m-to-expand-ai-liability-coverage).
- **Verdict: EXCLUDED.** This is insurance, which the brief rules out. Still relevant: the **agent scoring and certification data** insurers need could be a non-insurance wedge, and it ties into #7 and #17.

### 21. Pilot-to-production gap: 78% of enterprises pilot agents but about 12% reach production at scale, because integration, security and cost can't be justified
- **Who:** Heads of AI and CIOs.
- **Evidence:** "78% of enterprises are running AI agent pilots, but only 12% of those pilots reach production at scale" (https://www.softwareseni.com/why-most-enterprise-ai-agents-never-reach-production/, secondary source, origin unknown, **[UNVERIFIED]**). DataRobot "Unmet AI Needs" Jan 2026 report (https://page.datarobot.com/Unmet-AI-Needs.html). Blockers: security 73%, legacy integration 56%, operating cost 43% (survey origin unverified).
- **Verdict: WEAK as a wedge.** It is a meta-problem, a mix of #1, #2, #6 and #11, and not one specific thing to buy.

### 22. SaaS vendors can't meter, price or govern agent traffic hitting their own products (the supply side of #3 and #4)
- **Who:** CPOs, pricing and platform teams at 30K+ B2B SaaS companies moving off per-seat pricing.
- **Evidence:** 97% of SaaS CEOs plan to retire seat pricing within two years (Cruxy, via https://theagenticstack.substack.com/p/the-saas-seat-is-under-attack). Agentforce prices at $2/conversation and $0.10/action. Intercom Fin charges $0.99/resolution (https://www.mpt.solutions/ai-agents-are-killing-seat-based-saas-pricing-heres-whats-replacing-it/, https://www.entagl.com/blog/ai-agent-pricing-models-2026). Azion "AI agents hitting your API: what breaks first."
- **Pain:** Revenue leakage for the vendor: agents replace 10 seats and the vendor gets paid for 1.
- **Competitors:** Usage billing (Metronome, which Stripe acquired [UNVERIFIED, background knowledge], Orb, Amberflo, Paid.ai, Stripe Billing), plus Zuplo and Kong for API metering.
- **Verdict: MEDIUM.** Billing infrastructure is crowded. The gap is **detecting and classifying agent vs human usage inside a SaaS product so the vendor can price it**, a "Segment for agent traffic." That has a narrower but real wedge.

### 23. Evaluating agent quality in production: model upgrades and prompt changes silently change behavior on long-horizon tasks
- **Who:** AI engineering teams.
- **Evidence:** Partial. The r/AI_Agents summary notes that "models occasionally changing output format slightly... broke downstream parsing" (https://aiweekly.co/alerts/production-ai-agents-fail-on-infra-not-models). My follow-up search on eval regression was cut off by the budget limit.
- **Competitors:** Very crowded: Braintrust, Arize, LangSmith, Galileo, Patronus, Weights & Biases Weave, HumanLoop (acquired by Anthropic, background knowledge **[UNVERIFIED]**), Datadog.
- **Verdict: WEAK.** Crowded and model labs bundle it.

---

## Funded-startup landscape (as found)
| Area | Companies found (funding where seen) |
|---|---|
| Agent cost / FinOps | Revenium ($13.5M seed), Paid.ai (~$21.6M seed), Waxell |
| Agent identity / NHI | NewCore ($66M), Defakto ($30.75M B), Astrix ($45M B), Hush ($30M), Keycard ($30M A), Geordie ($30M A), Archestra ($10M seed), Astrasync |
| Agent undo / rollback | Rubrik Agent Rewind (incumbent) |
| Simulation / sandboxes | Arga Labs ($10M seed, YC), Klavis, Playgent (YC), AgentHub (YC), Runloop |
| Agent liability insurance | Armilla ($25M), Klaimee ($5.5M seed, YC) |
| Know-Your-Agent / bot verification | Persona, Trulioo+Worldpay, Visa/Mastercard/Ant KYA standard, Cloudflare Web Bot Auth |
| Browser/portal agents | Browserbase, Anchor Browser, BidPilot, Pallet, TinyFish |
| AI code review | CodeRabbit, Greptile, Qodo, Graphite (crowded) |

---

## Top 5 most promising

1. **Machine-customer front door (#13).** "Sierra for when the customer is an AI agent": detect, qualify and serve agent-originated inbound in support, sales and RFQ, with machine-readable answers and offers, and route real deals to humans. Revenue-side buyer, fast pilots (put it in front of one inbox), no dedicated competitor found, and it rides an inevitable 2027–2032 trend. Risk: Sierra, Decagon or Intercom add an "agent mode." Validate how real inbound agent volume is today.
2. **Cross-SaaS undo / provenance ledger for agent actions (#7 + #17).** "Ctrl-Z and a black box recorder for every agent action across Salesforce, NetSuite, Zendesk and more." Fear-driven buyer (CIO/SRE), with one-incident ROI. The same ledger also powers audit (#17) and insurer scoring (#20). Rubrik validates the category but is backup-centric. Hard technically, which is a moat.
3. **Agent license and entitlement management (#3, with #22 as the mirror image).** "The Flexera for agents": map which agents consume which SaaS licenses, credits and actions, forecast spend under the new action-based pricing, and defend against vendor audits. Every enterprise renegotiates SaaS contracts in 2026–2028. The buyer has a budget (procurement/SAM). Risk: Zylo, Productiv or Flexera add the feature.
4. **Agent P&L / outcome-based cost attribution (#2, absorbing #1).** "What does each agent cost per business outcome, compared with the human it replaced?" CFO buyer, and it addresses Gartner's "40% scrapped for unclear ROI." Revenium and Paid.ai are early competitors. You win by joining outcome data (CRM, ticketing), not token data.
5. **Org-wide agent egress control for third-party SaaS (#4 + #10).** One governed gateway for all outbound agent calls to SaaS: shared-quota scheduling, contract-drift quarantine, budget enforcement. MEDIUM on its own, because unified-API vendors (Merge, Nango, Composio, Arcade) are close. Listed mainly as the infrastructure that ideas 2–4 could be built on.

**Skeptical note:** 2026 survey data still says most enterprises are stuck at pilot stage (#21). Problems that need "thousands of agents" (#15, #18, #19) may not have enough buyers until 2028+. The two least time-sensitive bets are #13 (driven by *other people's* agents, so it doesn't depend on the customer's own maturity) and #3 (driven by vendor pricing changes, which are already happening).
