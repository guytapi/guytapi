# Thesis B: AI spend control ("FinOps for the AI workforce"): kill test

*Analyst: skeptical deep-research pass. Date: 2026-10-05. 33 web searches used. Tags: **[V]** means verified in a search snippet from a primary or reputable source. **[S]** means secondary or vendor source. **[U]** means unverified or my own estimate.*

**Thesis as stated:** A vendor-neutral control plane for AI spend across model APIs, coding agents and AI SaaS, with chargeback, budgets, routing and cost per business outcome.

**Bottom line up front:** The pain is real and large. The **category, however, was filled in 2026** by players with structural distribution advantages:

- Ramp shipped "AI Token Spend Management" in July 2026, and thousands of businesses have connected it.
- Vantage, CloudZero, Datadog, Finout, Zylo and Torii all ingest Anthropic, OpenAI and Cursor costs.
- ServiceNow AI Control Tower does cross-vendor agent cost and ROI.
- The model and coding vendors shipped native per-user caps:
  - Anthropic, July 2026: per-user caps plus cost per PR.
  - GitHub Copilot, June 2026: per-user budgets.
  - Cursor: Enterprise per-member limits.
- The traffic layer was bought up: Stripe bought OpenRouter (~$7.5B), Palo Alto bought Portkey, ClickHouse bought Langfuse and Mintlify bought Helicone.

As stated, the thesis is a feature of at least four incumbent categories. **Verdict: KILL as stated.** One narrow reframe is worth at most a 2-week validation (see section 5).

---

## 1. Pain magnitude

| Data point | Source | Tag |
|---|---|---|
| Ramp AI Index, April 2026: median company AI token spend **$2,246/mo**, mean **$140,842/mo**. 58% spend >$1K/mo, 31% >$10K/mo, 13% >$50K/mo, **9% >$100K/mo**, 2% >$500K/mo. | https://ramp.com/blog/ai-token-cost-for-businesses | [V] |
| Ramp: top 1% of adopters spend $7,400/employee/month and the top 10% spend $650. The median is $11.95. | same | [V] |
| Ramp: AI token spend across its customers up **20.7x since June 2025** (stated at its July 2026 launch). Effective price per 1M tokens fell to $0.68 by September 2026, down ~41% from the March peak. So volume, not price, drives spend. | https://siliconangle.com/2026/07/16/ramp-targets-ais-fastest-growing-cost-expanded-token-spend-tracking/ ; fourweekmba summary of the September Ramp AI Index | [V]/[S] |
| State of FinOps 2026: **98%** of FinOps teams now manage AI spend (63% in 2025, 31% in 2024). FinOps for AI is the #1 forward priority. | https://www.cloudkeeper.com/insights/blog/state-finops-2026-report-key-trends-insights-and-what-comes-next and others (secondary summaries of the FinOps Foundation report) | [S] |
| 73% of enterprises say AI costs exceeded projections. | via https://www.beri.net/article/ai-finops-2026-73-percent-blow-budget-cfo-fix | [S] |
| Harness 2026 State of AI in FinOps (n=700): **52% have no clear owner** for AI cost, **72% had an unexpected AI bill spike** in the past year, only 20% could explain a doubling within hours, an estimated **26% of AI spend is wasted**, and 56% forecast by guesswork. | https://www.harness.io/press-and-news/new-harness-report-reveals-enterprise-ai-spend-has-outgrown-the-systems-built-to-track-it | [V] (vendor survey) |
| a16z CIO survey: ~75% expected YoY LLM budget growth. The innovation-budget share fell to 7%, so spend has moved into core budget lines. | https://a16z.com/ai-enterprise-2025/ | [V] (2025 survey) |
| Menlo: enterprise GenAI spend went from $1.7B (2023) to **$37B (2025)**, with $19B of it in applications. | https://letsdatascience.com/news/enterprises-increase-ai-spending-to-37bn-6d854973 | [S] |
| **Uber** burned its full-year 2026 AI budget in ~4 months and capped spend at **$1,500/engineer/month** on Claude Code and Cursor. ~5,000 engineers, 95% adoption. **It built an internal dashboard** to track spend. | https://www.outlookbusiness.com/corporate/uber-caps-ai-tool-usage-after-exhausting-yearly-budget-in-just-4-months | [V] |
| **Microsoft** E+D division cancelled most internal Claude Code licenses by 30 June 2026 and moved to Copilot CLI. Per-user cost was $500-2,000/mo. | https://www.peoplematters.in/amp/news/ai-and-emerging-tech/microsoft-cancels-claude-code-licences-after-engineers-use-it-too-much-49918 | [S] |
| **Gartner (24 June 2026):** AI coding costs will exceed the average developer salary by 2028. It also notes that "AI coding vendors are yet to deliver mature, built-in cost optimization." | https://gartner.com/en/newsroom/press-releases/2026-06-24-gartner-predicts-ai-coding-costs-will-surpass-average-developer-salary-by-2028-as-token-consumption-surges | [V] |
| The Linux Foundation launched the Tokenomics Foundation on 9 June 2026 at FinOps X. | via https://www.beri.net/article/ai-finops-2026-73-percent-blow-budget-cfo-fix | [S] |

**Is it a funded priority?** Yes, for FinOps teams and CFO offices: it is the #1 FinOps priority, and AI spend now sits in core budget lines. **The counter-signal:** the funded response at Uber, Microsoft and Meta was an internal dashboard, a blunt per-head cap or a vendor consolidation. None of them bought a third-party tool. Big tech builds this capability itself.

**Spend per company (my estimates, anchored on Ramp and others) [U]:**
- Mid-market (200-2,000 employees): $0.1-1.5M/yr across tokens, coding agents and AI SaaS.
- Large enterprise: $3-30M+/yr.
- Engineering orgs with 1,000 engineers on agents: $6-24M/yr at $500-2,000 per engineer per month.

## 2. Competitors

| Name | What it does on AI spend | Funding / status | Overlap |
|---|---|---|---|
| **Ramp** (AI Token Spend Management, July 2026) | Connects Anthropic, OpenAI, Cursor and Gemini. Splits spend by team, person, project and key. Sets limits by team, project and key, raises anomaly alerts and suggests model-downgrade savings. "Thousands" of businesses connected. | $44B valuation (Series F, June 2026). 70K+ customers. >$1B annualized revenue. | **Very high.** Owns the CFO relationship and card data. |
| **Vantage** | Supports Anthropic API and Claude Enterprise (Claude Code, Cowork, Chat), OpenAI, and others. | $21M Series A (2023). Later rounds unknown [U]. | Very high |
| **CloudZero** | Integrations for Anthropic, OpenAI and Cursor (Admin API, per-user). Most customers ingest AI spend. | $56M Series C (May 2025). ~$42M ARR (March 2026, Sacra estimate). | Very high |
| **Datadog CCM + LLM Obs** | Cursor and Anthropic Usage & Cost integrations, broken down by user and product, including Claude Code. | Public | High |
| **Finout** | AI-token FinOps, agent allocation framework, autonomous remediation agents (June 2026). | $85M total ($40M Series C, January 2025). | High |
| **Harness CCM** | FinOps for AI; published the survey above. | Large private | Medium-high |
| **Zylo** | Consumption Cost Management (April 2026): OpenAI, Anthropic, Databricks, Snowflake, Vertex. | Late stage | High (procurement / IT buyer) |
| **Torii** | AI Management Platform: dedicated Cursor, Codex and Claude Code spend modules. Gartner MQ Leader in SaaS management. | Growth stage | High |
| **ServiceNow AI Control Tower** | Governs agents across 25+ platforms. Tracks tokens across OpenAI, Anthropic and Google, and ties spend to outcomes in ROI dashboards. | Public | High (enterprise agent-fleet ROI) |
| **Anthropic native** (July 2026) | Org and per-user spend limits, 75%/90% alerts, Spend Limits Admin API, Claude Code value tab with **cost per commit / per PR**, breakdown by SCIM group, and a feed to Datadog and CloudZero. | n/a | High for single-vendor shops |
| **GitHub Copilot native** (June 2026) | Usage-based AI Credits. Per-user, team and department budgets and alerts. | n/a | High |
| **Cursor native** | Member, group and team spend limits and dynamic limits (Enterprise). Admin API. | n/a | Medium-high |
| **OpenRouter → Stripe** | Router across 400+ models, ~5% take. ~$140M annualized revenue (July 2026). Stripe deal ~$7.5B (August 2026). | Acquired | Medium (routing, billing) |
| **Portkey → Palo Alto** | AI gateway: budgets, routing, governance. Closed 29 May 2026; now part of Prisma AIRS. | Acquired | Medium-high (traffic control point) |
| **LiteLLM** | OSS gateway with per-team and per-key budgets. Enterprise tier ~$30K/yr. | YC W23. Seed ~$1.6M; a $16M seed is reported but [U]. | Medium-high (free OSS ceiling) |
| **TrueFoundry** | AI gateway (in Gartner's Market Guide). | $21M total ($19M Series A, February 2025). | Medium |
| **Langfuse → ClickHouse; Helicone → Mintlify** | LLM observability with cost tracking. | Acquired (2026) | Medium |
| **Kong, Cloudflare AI Gateway, Bifrost (Maxim)** | Gateway cost tracking and rate limits. | Public / funded | Medium |
| **Revenium** | AI cost and ROI: Tool Registry (tokens + APIs + human review) and AI Outcomes (ROI per workflow). | $13.5M seed (November 2025). | **Very high (closest to "cost per outcome")** |
| **Pay-i** | GenAI cost and value intelligence. Founders are ex-Microsoft. | $4.9M seed (May 2025). | Very high |
| **Paid.ai** | Sell-side: billing and margin tracking for agent makers. | $33M ($21.6M seed led by Lightspeed). | Low-medium (sell-side) |
| **Larridin** | AI adoption, proficiency and impact for humans and agents. | $17M (a16z-led). | Medium (ROI angle) |
| **Jellyfish / DX (Atlassian) / Faros** | AI coding tool spend and impact, vendor-agnostic (Jellyfish). | Large / acquired | Medium-high on coding ROI |
| **FinOpsly, PointFive, nOps, Amnic, Ternary, Kubecost/IBM, Apptio/IBM** | Cloud FinOps adding AI. | FinOpsly $4.45M seed. PointFive $60M Series B. | Medium |
| **Credal, Spendflo, Vertice, Tropic** | AI governance and procurement. Vertice/Tropic negotiate AI contracts with benchmarks. | Funded | Medium |
| **YC 2026 batch** | At least one company tracks spend across 14 providers (OpenAI, Anthropic, Bedrock, Azure, Cursor, OpenRouter and others). Another claims 30% savings via routing and compression. Names not confirmed. | Seed | High [U] |

There are already SEO listicles such as Torii's "8 Spend Management Tools for Claude Code in 2026". That is a classic sign that a category is commoditizing.

## 3. Why incumbents own this, and whether an independent position is defensible

- **The data is trivially accessible.** Every vendor now exposes a read-only Admin/Usage API (Anthropic, OpenAI, Cursor, Copilot). Ingestion is a weekend integration, so there is no data moat. Ramp, Vantage, CloudZero, Datadog, Zylo and Torii all shipped connectors within months.
- **Distribution decides the race.** Ramp owns the CFO and the card that pays the bill. Cloud FinOps vendors own the FinOps lead and FOCUS pipelines. ServiceNow owns the CIO's governance workflow. Gateways own enforcement in the traffic path, and the strategics (Palo Alto, Stripe) bought them. An independent startup has none of these.
- **Native caps remove the urgent pain.** Uber's problem was "set a per-head cap", and Anthropic, Copilot and Cursor now do that natively. Cross-vendor aggregation is the only remaining gap, and the aggregators above already fill it.
- **Where neutrality could still matter [U]:**
  - **Enforcement across vendors in real time**, such as routing Claude Code subtasks to cheaper models or killing runaway loops. This requires sitting in the agent or traffic path, which is gateway territory and contested by LiteLLM OSS (free) and Palo Alto/Portkey.
  - **Joining cost with outcomes from systems of record** (CRM, ticketing, Git). This is where Revenium, Pay-i, ServiceNow, Jellyfish and Anthropic's own cost per PR are heading.
- **Conclusion:** Neutrality is necessary but not sufficient. The defensible layer, if there is one, is not visibility. It is **taking action on money**: commitments, capacity and contracts (see section 5).

## 4. Buyers, number of target companies and ACV

**Buyers:**
- FinOps lead / Head of Cloud Economics: most likely, and already served by the FinOps vendors.
- CFO / FP&A: served by Ramp.
- VP Eng / Head of Platform: for coding agents, served by native consoles and Jellyfish.
- CIO / Head of AI: for agent fleets, served by ServiceNow, Larridin and Revenium.

No buyer is unserved. 52% say no one owns AI cost (Harness), which cuts both ways: the pain is real, but the buying process is confused.

**Companies with more than $1M/yr AI spend (tokens + coding agents + AI SaaS) [U, estimate]:**
- **Anchor:** 9% of Ramp's tracked companies spend >$100K/mo, i.e. >$1.2M/yr, on tokens alone. Ramp has 70K+ customers skewed toward SMB and mid-market. If ~50% of them are AI spenders in the index, that is ~3K or more companies above $1.2M/yr on Ramp alone.
- **Global extrapolation:** Ramp is a small slice of the ~20K US firms and ~70K global firms with 1,000+ employees.

| Year | Companies >$1M/yr AI spend (global) | Assumption |
|---|---|---|
| 2026 | **8-15K** | Ramp anchor ×3-5 for non-Ramp and global firms |
| 2027 | **15-25K** | ~75% budget growth (a16z), more firms crossing the threshold |
| 2029 | **35-60K** | Gartner trajectory on coding cost; agent fleets |

**ACV [U]:** Cloud FinOps tools typically charge ~1-3% of spend under management (prior knowledge, not re-verified). LiteLLM Enterprise is ~$30K/yr, and Jellyfish is ~$360 per engineer per year.

- Realistic ACV: **$20-50K mid-market, $100-250K enterprise**, roughly 0.5-2% of AI spend.
- Price pressure is severe because Ramp bundles this into its card platform and native vendor consoles are free.

**Bottom-up market [U]:**
- 2026: 12K firms × $50K blended = **~$0.6B**.
- 2029: 50K × $90K = **~$4.5B** theoretical.

At least four incumbent categories plus the vendors contest it. A new independent entrant could plausibly reach 2-5%, which gives a $90-225M ARR ceiling by 2029-30. That is good enough for a strategic exit, but it is not a breakout venture outcome.

## 5. Sharper wedges, and whether any survive

| Wedge | Evidence | Status |
|---|---|---|
| **(a) Coding-agent spend governance** | Pain is acute (Uber, Microsoft, Gartner). But since June-July 2026, Anthropic (caps + cost per PR), Copilot (budgets), Cursor (limits), Ramp, Torii (dedicated Claude Code, Cursor and Codex modules), Datadog, CloudZero, Vantage and Jellyfish all cover it. | **Dead as visibility and caps.** A sliver may survive as *active optimization*: context-bloat and loop detection, and per-task model routing for agents. Gartner says vendors lack it. But that is gateway or agent-runtime territory, and vendors are incentivized to add only "good enough" controls. Low defensibility. |
| **(b) Cost per outcome for agent fleets** (tokens + tool APIs + human review vs. tickets resolved and deals closed) | Revenium (Tool Registry, AI Outcomes), Pay-i, ServiceNow AI Control Tower (cross-vendor ROI), Larridin, and Anthropic cost per PR. Large agent fleets are still rare in 2026. | **Early and contested.** The thesis is attractive but the market is not ready: few companies run 50+ production agents. ServiceNow and Workday are natural owners. Watch, don't build. |
| **(c) AI commitment, capacity and contract optimization** ("ProsperOps for AI"): autonomously manage prepaid commits and discount tiers, provisioned throughput (Azure PTUs, Bedrock PT), batch vs. on-demand, cross-vendor arbitrage at renewal, and audit of outcome-priced invoices (per-resolution). Priced as a % of realized savings. | Anthropic discount tiers unlock at roughly $100K / $500K / $1M / $5M of commit ([S], redresscompliance). AI prices are falling 40-70% ([S]), so commitments go stale fast. Vertice and Tropic do generic SaaS negotiation (Tropic saved customers $33M in H1 2026). ProsperOps and similar show that "autonomous commitment management, paid on savings" works in cloud (prior knowledge [U]). Not found: any dedicated AI-commitment autopilot. | **The only plausible survivor [U].** It is action on money rather than a dashboard. Pay-on-savings sidesteps the free native consoles. It needs neutrality, because no vendor will help you buy less of itself. Risks: Ramp/Vertice extend into it; commit and PTU markets may be too small or too vendor-specific in 2026; it needs evidence that buyers overcommit or undercommit materially. **Unvalidated.** |

## 6. Kill signals (found)

1. **Ramp launched the exact product (July 2026)** with "thousands" of businesses connected, CFO distribution and a $44B war chest. This is the strongest single kill signal.
2. **Vendors shipped native cost controls in June-July 2026** (Anthropic, Copilot, Cursor), including Anthropic's cost per PR, the "cost per outcome" pitch for coding.
3. **Every FinOps and SaaS-management incumbent added AI connectors**: Vantage (incl. Claude Code), CloudZero, Datadog, Finout, Zylo, Torii, Harness.
4. **Gateway consolidation by strategics:** Palo Alto/Portkey, Stripe/OpenRouter (~$7.5B), ClickHouse/Langfuse, Mintlify/Helicone. The enforcement chokepoint is now owned by security and payments platforms.
5. **ServiceNow AI Control Tower** claims cross-vendor (25+ platforms) agent cost tracking plus ROI, aimed at the enterprise CIO.
6. **Big tech responded by building internally or consolidating**, not buying: Uber built an internal dashboard and cap; Microsoft consolidated onto Copilot.
7. **Funded direct startups already exist:** Revenium $13.5M, Pay-i $4.9M, Larridin $17M, plus YC-batch clones.
8. **Token price deflation** ($1.15 → $0.68 per 1M tokens, March to September 2026) partly self-solves the cost pain over time. Volume still dominates, though.

Signals that keep *some* life:
- Gartner says vendors' built-in *optimization* is immature.
- 26% of spend is wasted (Harness).
- 52% have no cost owner.
- Spend is growing ~20x YoY on Ramp.

---

## Sharpened thesis (if anything is pursued)

> **"Autonomous AI commitment & capacity manager":** a neutral agent that decides how to buy AI (commit tiers, PTUs and provisioned throughput, batch vs. on-demand, vendor mix at renewal) and audits outcome-priced AI invoices. It is paid as a % of realized savings.

Validation gate before investing more:
- **Pass:** 8 of 15 interviews with FinOps or procurement leads at companies spending more than $2M/yr confirm material over- or under-commitment, or idle PTUs, worth more than 10% of spend, and say Ramp/Vertice/Vantage do not handle it today.
- **Otherwise:** kill.

## Scores (1-10)

| Criterion | Score | Note |
|---|---|---|
| Pain | **8** | 72% hit a bill spike, 26% waste, Uber and Microsoft blowups |
| Urgency | **7** | Budgets blown mid-year, but native caps relieve the acute part |
| ROI clarity | **7** | Savings are easy to quantify |
| Customer accessibility | **5** | Buyer ownership unclear (52%); FinOps buyers already have vendors |
| Pilot speed | **7** | Read-only admin APIs make pilots fast, which equally helps every competitor |
| Market size | **6** | ~$0.6B (2026) to ~$4.5B (2029) theoretical, heavily contested |
| Expansion | **6** | From tokens to SaaS credits to agents to outcomes, but incumbents expand the same way |
| Venture potential | **4** | Likely capped at a strategic tuck-in |
| Defensibility | **2** | No data moat; commodity connectors; bundling by Ramp, FinOps vendors and the model vendors |
| Why now | **8** | Copilot usage billing (June 2026), Gartner, FOCUS/Tokenomics standards |
| Competition position | **2** | Late: the category filled in 2026 |

## VERDICT: **KILL** (as stated). Optional narrow REFRAME (wedge c) only through a 2-week interview gate.

**Reasoning:** The thesis is right about the problem and wrong about the opportunity.

- In June-July 2026, the three natural owners each shipped the core product: the payer (Ramp), the vendor (Anthropic, GitHub, Cursor native controls) and the FinOps/SaaS-management incumbents (Vantage, CloudZero, Datadog, Zylo, Torii, Finout). ServiceNow took the enterprise "agent ROI" framing.
- Strategics acquired the traffic-path chokepoint (Palo Alto/Portkey, Stripe/OpenRouter).
- Visibility, budgets, chargeback and caps are now features with zero switching cost.
- "Cost per outcome" is already marketed by Revenium, Pay-i, ServiceNow and Anthropic (cost per PR), and agent-fleet scale is not yet there.

The only position that is both neutral and not a dashboard is *acting on how AI is bought*: commitments, capacity and contract renewal, paid on savings. That idea is unvalidated and should be treated as a hypothesis, not a thesis.

### Unverified items to check if reframing
- A dedicated AI-commitment or PTU optimization vendor may already exist. Not found in this pass, so do one targeted search plus customer interviews.
- LiteLLM's reported $16M seed.
- Vantage's post-2023 funding.
- Names of the YC 2026 AI-spend companies.
- Ramp's absolute count of companies above $1M AI spend. The 9% figure covers tracked companies, not all 70K customers.
