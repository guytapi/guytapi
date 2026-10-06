# F3: Commitment Ledger for Customer-Facing AI Agents (Thesis #10)

**Date:** 2026-10-06 | **Stance:** skeptical analyst and red team | **Searches used:** 38 of 40 (WebFetch was blocked on the one page I tried, so everything below comes from search snippets)
**Pitch tested:** "Your AI agents make thousands of promises to customers every week. We tell you which ones you're legally on the hook for."

## Verdict: KILL

**Average score 4.6. The bar is 8.5.**

Three separate causes of death, any one of which would be enough:

1. **F1, platform absorption, already happened.** Every major agent vendor shipped "QA every conversation against your policy" between 2024 and 2026:
   - Decagon Watchtower
   - Intercom/Fin Monitors (Mar 24, 2026)
   - Zendesk QA for AI agents (2024, still being extended)
   - Sierra supervisors that observe and intercept
   - Agentforce Command Center and Observability (GA)

   The supposed conflict ("vendors are graded on this") is not stopping them. They ship it because it removes an objection to buying.
2. **F2, visible-pain race, already crowded with cross-vendor neutral players.** These companies already sell exactly this check:
   - **Oversai.** Separate SKUs for Fin, Sierra, Zendesk and Gorgias. It "flags any answer that expands eligibility, creates an exception, omits a required condition, changes a timeline, or uses outdated policy language." That sentence is our product.
   - **Isara.** Zendesk marketplace app. Its blog headline is "Your AI agent just issued a refund it was never allowed to. Did you catch it?" It markets "an independent audit trail" and "audit reports for legal review."
   - **Swept.ai.** Pre-seed, AI agent supervision.
   - **Solidroad.** Hallucination QA.
   - Incumbent QA vendors: Rippit (formerly MaestroQA), Level AI, evaluagent, Playvox, NICE, Verint.
   - Pre-launch testing: Giskard (it has a red-team category literally named "Liability Engagement"), Cresta, Coval ($28M Series A, Jun 2026), Cekura, Hamming.
3. **F4, the dollars are small.** Each incident costs little:

   | Incident | Cost |
   |---|---|
   | Moffatt v. Air Canada | CA$812.02 |
   | Chevy dealer "$1 car" | Never honored |
   | Cursor | Cancellations and reputation, no legal cost |
   | UK shop, 80% fake code on an £8K order (Feb 2026) | Owner refused to honor it [U] |

   The real harm is to reputation and churn. That belongs to the Head of CX's QA budget, not to the GC or CFO. "Accruals for AI promises" does not hold up: a refund that was actually issued already sits in the ledger, and a promise that was never executed is rarely enforced. Courts have bound companies only in small-claims-sized cases.

Conventions: [V] = backed by a search result (source named). [U] = unverified or inferred.

---

## 1. Evidence: incidents, lawsuits, regulation (2024–2026)

| Event | Date | What it shows | Source |
|---|---|---|---|
| Moffatt v. Air Canada, 2024 BCCRT 149 | Feb 2024 | Chatbot statement = company statement (negligent misrepresentation). Damages **CA$812.02**. Small-claims tribunal, so no binding US precedent | [V] cbc.ca, mccarthy.ca, incidentdatabase.ai/cite/639 |
| Cursor "Sam" support bot invents a one-device policy | Apr 2025 | Cancellations, a public apology, no legal action | [V] theregister.com 2025/04/18, fortune.com |
| Gap / Sierra agent jailbroken (sex toys, Nazi Germany) | Late Nov 2025 | Guardrails "inadvertently misconfigured." Sierra fixed it itself, so the vendor owns remediation | [V] emarketer.com, vibegraveyard.ai |
| UK small business chatbot talked into 25%→80% fake discount codes; an order worth over £8K demands it be honored | Feb 2026 | Unauthorized concession by manipulation. Outcome unclear [U] | [V] vibegraveyard.ai (secondary) |
| **OLG Hamm, 4 UKl 3/25** (Verbraucherzentrale NRW v. Aesthetify) | **May 12, 2026** | Chatbot output is attributed to the operator **regardless of fault**. Curated training data is not a defense. Appeal to the BGH allowed. Case type: an injunction over misleading advertising (invented physician titles), not damages | [V] dlapiper.com (Jun 15, 2026), cms.law, innobu.com |
| Munich Regional Court bars Google from false AI Overviews | 2026 | Liability for AI statements is spreading in Germany | [V] innobu.com (secondary) |
| FTC Operation AI Comply; DoNotPay ($193K); Air AI (~$19M) | 2024–2025 | Targets **claims about AI products**, not statements made by agents to customers | [V] ftc.gov, orrick.com |
| State AGs: letter from 42 AGs (Dec 2025); KY and PA v. Character.AI (2026); Colorado Chatbot Safety Act (May 2026) | 2025–2026 | Focus is **child safety and companions**. No AG action found over a commerce agent's promises | [V] regulations.ai, troutman.com |
| Taylor v. ConverseNow (Domino's voice AI), CIPA class action allowed to proceed | 2025 | The class-action risk is **wiretap/privacy**, not promises | [V] wsgr.com |
| EU Product Liability Directive (transposition due Dec 9, 2026) | 2026 | Covers personal injury, property and data loss. **Pure economic loss from promises is excluded**, so it is not a driver | [V] gibsondunn.com, ELI |
| Verisk ISO GenAI exclusions CG 40 47/40 48/35 08 (Jan 2026); >80% of carrier filings approved | 2026 | Insurance is retreating. Armilla/Lloyd's standalone AI liability now goes up to $25M (Jan 2026) | [V] insurancebusinessmag.com, insurancejournal.com (Jul/Aug 2026), armilla.ai |

**Last 60 days (Aug–Oct 2026):** I found **no new case** involving promises made by an agent. Recent news is about insurance exclusions (Insurance Journal, Jul/Aug 2026) and infrastructure M&A: Dynatrace bought Arize for $915M (announced Aug 13, 2026) and Cisco closed its Galileo deal in May 2026. In 2.5 years the list of incidents has grown slowly, and each one is cheap.

**Survey data:**
- Gartner: 91% of 321 service leaders feel pressure to deploy AI (Feb 2026) [V].
- Gartner consumer survey: 42% worry about incorrect AI information [V].
- Qualtrics 2026: AI customer service fails at about 4x the rate of other AI uses [V].
- "58% considered switching after a wrong AI answer, 22% switched" (2025) [U, secondary].

**I found no survey where GCs or CFOs name agent promises as a budgeted risk.**

**Leakage and fraud data:**
- Pindrop: 3 in 10 retail fraud attempts are AI-generated; some chains get more than 1,000 bot calls a day [V via fisherphillips/secondary].
- Ravelin 2026: 1 in 4 shoppers admit to refund abuse, and 98% of them succeeded [V].

That is a **fraud** problem, already served by Ravelin, Pindrop and Riskified. It is not about liability for agent promises.

**I found no quantified data on unauthorized discounts or refunds issued by AI agents.**

## 2. Competitors: is anyone extracting commitments or liability from agent transcripts?

**Yes, functionally, from several directions.**

| Layer | Players | Overlap with the thesis |
|---|---|---|
| Agent vendors' own QA and supervision | Decagon **Watchtower** (custom plain-language flags, "regulated complaints", compliance); **Fin Monitors** (Mar 2026, always-on QA across AI and human conversations); **Zendesk QA for AI agents** (100% AutoQA); **Sierra supervisors** (audit every action and response for policy; can switch from observe to intercept); **Agentforce Command Center** (guardrail and policy checks, human review queues) | About 70%. They lack only a "liability $" label |
| Cross-vendor AI agent QA | **Oversai** (separate Fin/Sierra/Zendesk/Gorgias pages; eligibility-expansion, exception and timeline-change detection); **Isara** (independent audit trail, unauthorized actions, audit reports for legal); Solidroad; Swept.ai ($1.4M pre-seed) | **About 90%. This is the product** |
| Contact center QA and analytics | Zendesk QA (Klaus), Rippit (formerly MaestroQA, rebranded Mar 2026), Level AI, evaluagent, Playvox, Observe.AI, NICE CXone Interaction Analytics ("reputational, financial and regulatory risks"), Verint | 60%. They already own the QA budget and the transcripts |
| Pre-deployment testing | Cresta (automated AI agent testing; Synthetic Customers, May–Jun 2026), Coval ($28M A), Cekura ($2.4M), Hamming ($3.8M), Giskard ("Legal & Financial Risk" scan category) | Prevention rather than detection |
| Guardrails and observability | Galileo (Cisco), Arize (Dynatrace), Guardrails AI, NeMo | Infrastructure, now owned by acquirers |
| Regulated FS | Gradient Labs ($26M, agents with built-in Consumer Duty guardrails); NICE/Verint UDAAP monitoring; Spring Labs ($5M) | Owns the one vertical where per-statement liability is real |
| Sales and CS promise tracking | falkster.com "Customer Commitment agent" (Gong/Salesforce/Slack vs. roadmap) | Shows the "commitment ledger" framing is a weekend build |

**The only gap left** is the label ("legal exposure in $") and the buyer (GC/CFO). That gap exists because those buyers do not pay for this. It is not a gap nobody has noticed.

## 3. Would the agent vendors absorb it?

They already have. The conflict-of-interest argument (vendors grading their own homework) fails in practice:
- Buyers accept vendor-native QA. Fin Monitors was built because customers asked for "always-on QA across every conversation."
- Vendors fix incidents themselves (Sierra/Gap).
- Where neutrality is demanded, neutral QA tools (Oversai, Isara, Zendesk QA) already sit on the helpdesk API.

Only enterprises running several agent vendors, or regulated ones, would want an independent auditor. That group is small, and NICE and Verint already serve the regulated part.

## 4. Market math

**Deployers:**
- Zendesk: ~20,000 AI customers [V]
- Agentforce: >6,000 paying customers [V]
- Fin: ~8,000 businesses [V, T2]
- Sierra: 100+ enterprises; Decagon: 100+ enterprises [V]

Gross deployers are around 30–40K. Firms with enough agent volume and legal sensitivity to buy a separate liability product: **~2,000–4,000** [U].

**What they would pay [U]:**
- Head of CX for AI QA: $15–60K. Comparable to Zendesk QA, Level AI, Oversai seats, but squeezed by bundling.
- GC or CFO: nothing found. No line item exists.

**ARR paths [U]:**
- **$10M ARR:** ~300 customers at $35K. Plausible as a QA niche, but you would be the fifth entrant against Oversai and Isara, plus free vendor-native tools.
- **$100M ARR:** needs ~3,000 customers at $35K, i.e. most of the reachable market, against bundled free features. Not credible. It fails filter 5 in the taxonomy.

---

## Finalist format

- **One-line problem:** Customer-facing AI agents make statements (refunds, discounts, dates, policies) that courts treat as the company's own, and nobody counts the exposure.
- **Why now:**
  - Agent volume grew 2–3x a year (Agentforce >6K payers; Fin, Sierra and Decagon each over $100M ARR).
  - OLG Hamm (May 2026) established no-fault attribution of chatbot output to the operator in Germany.
  - Verisk GenAI exclusions (Jan 2026) remove insurance cover.
- **Exact buyer (claimed):** GC or legal ops; CFO/Controller. **Actual buyer found:** Head of CX/Support Ops, out of the QA budget.
- **Exact ICP:** B2C enterprise (airline, telco, retail, fintech, SaaS) with 50K+ AI-handled conversations a month across two or more agent vendors.
- **Current workaround:** vendor-native QA (Watchtower, Monitors, Zendesk QA, Sierra supervisors); cross-vendor AI QA (Oversai, Isara); hard caps on refund tools; sampling 50 conversations a month by hand; honoring the occasional small claim.
- **Why incumbents cannot easily own it:** **They can and did.** The thesis fails here.
- **30-day MVP:**
  1. Read-only helpdesk connectors (Zendesk/Intercom/Salesforce).
  2. LLM extraction of commitments into a schema (type, amount, date, condition).
  3. Diff each commitment against policy docs and order/refund system data.
  4. A $-exposure dashboard.

  It is buildable in 30 days, which is itself evidence for F5.
- **Pilot design:** Backfill 90 days of transcripts for one enterprise. Report:
  - number of off-policy commitments
  - $ value of unauthorized concessions actually executed
  - number of promises never fulfilled

  Success = more than $250K a year in quantified, recoverable leakage, and a budget owner outside CX.
- **Pricing hypothesis:** $30–120K/yr platform fee by conversation volume, or a share of leakage recovered.
- **Expansion path:**
  - From promises to sales and CS human promises (Gong data)
  - Then to agent-to-agent B2B commitments
  - Then to underwriting data for AI liability insurers (Armilla)

  The insurer angle is the only non-obvious one, and it is small.
- **Moat:** Weak.
  - The commitment taxonomy and policy diffs are per-customer configuration.
  - The data belongs to the helpdesk and agent vendors.
  - No network effect, unless benchmarks across customers or insurer pricing become the asset.
- **Why it could become $10B+:** Only if agent promises become a material accounting or regulatory category (e.g., the BGH upholds Hamm, EU consumer authorities run sweeps, and US class actions over systematic agent misstatements succeed) **and** auditors or insurers require independent attestation. No evidence of this today.
- **Direct competitors:** Oversai, Isara, Solidroad, Swept.ai, Zendesk QA, Rippit (MaestroQA), Level AI, evaluagent, Observe.AI.
- **Adjacent threats:** Decagon Watchtower, Fin Monitors, Sierra supervisors, Agentforce Command Center, NICE, Verint, Cresta, Coval, Giskard, Cisco/Galileo, Dynatrace/Arize, Gradient Labs.
- **One sentence to a CFO:** "Your AI agents gave away $X in off-policy refunds and promised Y things your systems never delivered last quarter. Here is the list with transcripts." (Only works if X is large, which no evidence supports.)
- **5 discovery questions:**
  1. In the last 12 months, what is the largest dollar amount you paid or honored because an AI agent said something off-policy?
  2. Who signed off on the agent's refund and credit authority limits, and who reviews breaches today?
  3. Does legal or finance receive any report on agent conversations today? Would they pay from their own budget for one?
  4. How many agent vendors are live, and do you trust each vendor's own QA scores?
  5. Has an insurer, auditor or regulator asked you to prove what your agents told customers?
- **Hard kill criteria (already triggered):**
  - (a) Two or more funded cross-vendor tools sell policy-adherence QA for AI agents: **triggered** (Oversai, Isara, Swept, Solidroad).
  - (b) The major agent vendors ship native QA against policy: **triggered** (Decagon, Fin, Zendesk, Sierra, Salesforce).
  - (c) No GC or CFO budget, with largest-incident dollars under $100K in 10 discovery calls: likely, given that the public record is CA$812 to £8K.

## Scores (1–10)

| Criterion | Score | Reason |
|---|---|---|
| Pain | 5 | Reputational, but small dollars per incident |
| Urgency | 4 | No 60-day catalyst. Hamm is under appeal |
| ROI clarity | 4 | Leakage is unquantified. Executed refunds are already visible in billing |
| Customer accessibility | 6 | CX leaders are reachable. GC and CFO are not engaged |
| Pilot speed | 8 | Read-only helpdesk API, backfill in days |
| Market size | 5 | ~2–4K real buyers, squeezed QA budget |
| Expansion | 5 | Insurer data is the only novel path |
| Venture potential | 3 | $100M ARR not credible against bundling |
| Defensibility | 2 | LLM extraction plus policy diff. Vendors own the data |
| Why now | 7 | Volume and German case law are real |
| Competition position | 2 | Fifth or later entrant, with platforms already shipping |
| **Average** | **4.6** | Fails the bar (≥8.5, none <7) |

## Residual worth logging (not a finalist)

Two adjacent ideas deserve a scan-level check only:

- **AI liability insurers' underwriting and claims data.** Armilla and Lloyd's need evidence of agent performance drift to price cover, and Verisk exclusions are pushing risk toward standalone AI policies. The buyer is the insurer, not the deployer.
- **German and EU consumer-law exposure after Hamm, if the BGH upholds it.** Consumer associations (Verbraucherzentralen) can bring injunctions at scale, which would turn chatbot claims into competition-law risk.

Revisit only if the BGH affirms Hamm, or if a US class action over systematic agent misstatements (not wiretapping) survives a motion to dismiss.

## Sources (all from search results; [U] where secondary)
- dlapiper.com/en/insights/publications/2026/06/german-court-addresses-liability
- cms.law (Verbraucherzentrale NRW v. Aesthetify GmbH, 12 May 2026 tracker entry)
- innobu.com/en/articles/ai-liability-chatbot-companies-2026.html
- cbc.ca/news/canada/british-columbia/air-canada-chatbot-lawsuit-1.7116416
- mccarthy.ca/en/insights/blogs/techlex/moffatt-v-air-canada-misrepresentation-ai-chatbot
- theregister.com/2025/04/18/cursor_ai_support_bot_lies/
- emarketer.com/content/gap-chatbot-jailbreak-brand-safety-risk
- vibegraveyard.ai/story/uk-chatbot-80-percent-discount-refund/ [U, secondary]
- oversai.com/products/ai-agent-qa ; oversai.com/sierra/ai-agent-qa ; oversai.com/fin/ai-agent-qa
- isara.ai/blog/your-ai-agent-just-issued-a-refund-it-was-never-allowed-to-did-you-catch-it/
- finder.techleap.nl/news/feed/swept-ai-raises-1-4m-for-supervision
- decagon.ai/blog/decagon-watchtower
- cxfoundation.com/news/fin-intercom-monitors
- support.zendesk.com/hc/en-us/articles/7423754224410-Announcing-quality-assurance-QA-for-AI-agents
- sierra.ai/jp/blog/enterprise-grade-agents
- salesforce.com/agentforce/command-center
- cresta.com/press/cresta-launches-automated-ai-agent-testing-so-businesses-can-deploy-ai-agents-with-confidence
- futureagi.com/blog/best-hamming-alternatives-2026/ (Coval $28M A) [U, secondary]
- cekura.ai/blogs/fundraise
- docs.giskard.ai/hub/ui/scan/vulnerability-categories/legal-and-financial-risk
- armilla.ai/resources/armilla-ai-raises-lloyds-backed-coverage-to-25m-as-traditional-insurers-retreat-from-ai-risk
- insurancebusinessmag.com/us/news/cyber/isos-generative-ai-exclusion-is-already-on-thousands-of-cgl-policies-589971.aspx
- insurancejournal.com/magazines/mag-features/2026/08/17/881424.htm
- wsgr.com/en/insights/us-federal-court-allows-cipa-class-action-against-ai-customer-service-provider-to-proceed.html
- ravelin.com/blog/ai-powered-refund-abuse-dispute-fraud
- fisherphillips.com/en/insights/insights/the-top-7-ai-generated-retail-scams-you-need-to-worry-about-in-2026
- gcom.pdo.aws.gartner.com/en/newsroom/press-releases/2026-02-18-gartner-survey-finds-ninety-one-percent-of-customer-service-leaders-under-pressure-to-implement-ai-in-2026
- usefini.com/blog/qualtrics-ai-customer-service-failing [U, secondary]
- nasdaq.com/articles/salesforces-agentforce-bookings-surge-will-adoption-drive-revenues (>6K paying Agentforce customers) [U on exact figure]
- neofeed.com.br (Zendesk ~20K AI customers) [U, secondary]
- solidroad.com/resources/best-maestro-qa-alternatives (Rippit rebrand) [U, secondary]
- blogs.cisco.com/news/cisco-announces-the-intent-to-acquire-galileo ; kucoin.com (Dynatrace–Arize $915M) [U, secondary]
- fintech.global/2026/06/02/gradient-labs-raises-26m-to-build-ai-agents-for-banks
- falkster.com/blog/agent-customer-commitments
