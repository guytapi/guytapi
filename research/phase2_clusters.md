# Phase 2: Problem Clusters

Source: 147 problems across 6 Phase 1 files (research/phase1/*.md).
Added filter from the founder: the idea must be **interesting, aligned with where the world is going, and understandable to a VC in one sentence**. Recovery-audit businesses like "SPA Claim Desk" fail this filter.

## Clusters, ranked by cross-domain convergence

| # | Cluster | Domains it appeared in independently | One-sentence pitch | Initial status |
|---|---|---|---|---|
| A | **Selling to machine buyers (agentic B2B commerce, seller side)** | agents_at_scale #1, gtm #3, supply_chain #1, gtm #5, finance #5 (5 hits, 4 domains) | "AI agents are becoming the buyers; we make every B2B supplier sellable to them." | DEEP RESEARCH |
| B | **AI spend control / AI P&L** (tokens, coding agents, cost per outcome) | ai_dev #2, agents #4, it #3, finance #2, gtm #4 (5 hits, 5 domains) | "FinOps for the AI workforce: what every agent costs and what it earns." | DEEP RESEARCH (crowding risk: Revenium, Paid, Vantage, CloudZero, Ramp, Palo Alto/Portkey) |
| C | **Controlling what agents do** (undo, action ledger, authorization, deploy-risk gate) | agents #2, it #2, ai_dev #1, ai_dev #3 | "Ctrl-Z and a black box recorder for every action an AI agent takes in your company." | DEEP RESEARCH (crowding risk: identity/governance vendors, Rubrik Agent Rewind) |
| F | **Securing apps that employees build themselves with AI** (Lovable/Replit/Base44/Claude artifacts) | it #1 (+ shadow AI adjacency) | "Every employee is now a developer; we find and secure the thousands of apps they ship." | DEEP RESEARCH |
| E | **Auditing outcome-priced AI vendors** | gtm #1 | "We verify the AI agents you pay per outcome actually delivered it." | HOLD: narrow today (CX only); revisit as an expansion of B |
| D | **Contract-to-cash enforcement** (supplier invoice vs contract, unbilled terms, tariff refunds) | finance #1,#3,#4; supply #2,#4 | "We make sure what contracts promise is what gets paid." | DEPRIORITIZED: strong pain but fails the "where the world is going / exciting" filter (SPA-like) |
| G | Hiring fraud / candidate-to-employee identity | gtm #2 | "Stop fake and deepfake employees." | KILL-LEANING: Persona, CLEAR, Deel/Clarity, Socure bundling |
| H | Agent license / entitlement management | agents #3 | "Flexera for agents." | Fold into B |

## Clusters killed for crowding (from Phase 1)
AI code review, AI SRE, agent identity/NHI, Copilot oversharing, shadow-AI DLP, AI helpdesk, GEO/AI visibility, AI support agents, usage billing, email-to-ERP order entry, quoting, freight audit, deductions, EDI, SOC2 automation, SaaS license management, dev productivity analytics.

## Why A is the lead hypothesis going in
- It is the only theme that came up **independently** from the agents, GTM, supply chain and finance researchers.
- It is easy to understand (an investor gets it in one sentence) and directional (2027–2032 commerce shifts from humans to agents).
- The buyer is revenue-side (the money comes in through it), not a cost center.
- Main risks to test: (1) Is agent-originated B2B demand actually arriving now, or is it 2029? (2) Shopify/commercetools/Salesforce Commerce/SAP/UCP/ACP protocols. (3) Is the B2B part (contract pricing, credit terms, RFQs, approvals) really unsolved?
