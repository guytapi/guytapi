# VERIFY: F-D "Expert human review queues for AI output"

Date: 2026-10-06. Method: 22 WebSearch queries, run adversarially (looking for reasons the idea fails). WebFetch was not used, so figures come from search snippets of the cited pages. [E] marks an estimate.

Wedge under test: **confidence routing plus reviewer workflow plus QA, sold to AI products in specialist domains. Email claim: "Cut the share of AI output your experts must review from 40% to 10% at the same error rate."**

## Bottom line
**The headcount is real and in some places larger than SYNTHESIS said. But the thing the wedge sells, the auto-approve rate, is the vertical AI vendor's own core product metric. Horizontal attempts to sell it have stayed tiny or been shut down.**

1. **Workforce and headcount: confirmed.**
   - EvenUp has two expert pools: 100+ in-house nurses, paralegals and lawyers who QC the Piai model, plus a separate 150+ team producing expert-reviewed demands.
   - Spend on outsourced human review keeps rising. TaskUs AI Services grew 58.6% in FY2025, Mercor is at about $2B annualized gross revenue, and Snorkel is at a $375M run rate.
2. **The metric is already owned by the vendors.** In mature verticals, the "share that skips human review" is the headline number each vertical vendor sells:
   - CodaMetrix: 93%+ of visits go straight to billing; at UMass Memorial its automation rate rose 15 points to 86%.
   - Fathom: 93%+ straight-to-bill.
   - Hyperscience claims 98% automation, and intelligent document processing (IDP) as a category reaches 75–90% straight-through processing (STP).
   - A vendor will not outsource the model that decides what its own product can do unattended.
3. **Horizontal human-in-the-loop (HITL) tooling has a poor track record.**
   - Google **deprecated Document AI HITL** (shut down Jan 2025) and points customers to systems integrators instead.
   - AWS A2I (confidence-threshold routing to reviewers) has barely changed since 2020.
   - The startups doing exactly this wedge are tiny: Redouble AI (YC, a $500K pre-seed in 2024), HumanLayer ($500K seed), and Abundant (~$4.5M).
4. **The pieces are commoditized.**
   - Reviewer queues are free features in Langfuse and LangSmith annotation queues.
   - Cleanlab TLM sells a trust score with "route to human below threshold".
   - HumanSignal pivoted to production review interfaces (Jun 2026).
5. **The regulatory tailwind has slipped.** The Digital Omnibus moved the EU AI Act's Annex III high-risk obligations, including Article 14 human oversight, from Aug 2026 to **2 Dec 2027**.

**Verdict: drops from 7.0 to about 5.5.**

## 1. Breadth and size of HITL review headcount (2025–2026)

| Evidence | Figure | Source |
|---|---|---|
| EvenUp | 100+ experts QC the model, plus a separate 150+ legal professionals for expert-reviewed demands. 72% of demand content starts from an AI draft. Business Insider (Dec 2024) reported missed injuries and fabricated conditions. | [evenuplaw.com blog](https://evenuplaw.com/blog/leveraging-ai-human-review-in-demand-letters-the-evenup-difference); [aiwiki.ai/wiki/evenup](https://aiwiki.ai/wiki/evenup); [sacra.com/c/evenup](https://sacra.com/c/evenup/); [businessinsider.nl](https://businessinsider.nl/evenups-valuation-soared-past-1-billion-on-the-potential-of-its-ai-the-startup-has-relied-on-humans-to-do-much-of-the-work-former-employees-say/) |
| Harvey | Its stated position is that "lawyer review is non-negotiable". The reviewers are the *customer's* lawyers, so the queue sits at the law firm and is not Harvey's cost. | [aiagentrank.io Harvey review 2026](https://aiagentrank.io/blog/harvey-ai-review-2026); [rfp.wiki/vendors/harvey](https://www.rfp.wiki/vendors/harvey) |
| TaskUs (BPO) | FY2025 revenue $1.184B. AI Services +58.6% and Trust & Safety +23.9%. AI Services has grown more than 30% for 6 straight quarters through Q1 2026. | [businesswire FY2025](https://www.businesswire.com/news/home/20260224268151/en); [businesswire Q1 2026](https://secure.businesswire.com/news/home/20260506183641/en/TaskUs-Announces-Fiscal-First-Quarter-2026-Results) |
| Medical coding | Autonomous coding: 92% on tuned specialties, 78% on generalist mixes, 65% on complex ones. Health systems see 65–80% direct-to-bill outpatient and 30–45% inpatient. **The review share is falling inside vendor products.** | [stealthagents.com](https://stealthagents.com/research/ai-medical-coding-automation-statistics-2026); [rfp.wiki/vendors/codametrix](https://www.rfp.wiki/vendors/codametrix); [rfp.wiki/vendors/fathom-health](https://www.rfp.wiki/vendors/fathom-health) |
| Market sizing | A "$14.8B human AI oversight services market by 2028" figure circulates. It comes from low-quality content-marketing sources, so treat it as unreliable. | [stealthagents.com HITL stats](https://stealthagents.com/research/human-in-the-loop-ai-operations-statistics-2026) |

**Read:** the headcount exists, but it is concentrated in a few vertical AI vendors (EvenUp-style "AI plus experts as a service") and in BPOs. At the other cluster-5 companies the reviewers are either the customer's own professionals (Harvey, Vanta auditors, Snyk/Semgrep users triaging findings) or small internal teams (DoorDash: 1–3 FTE of QA, per the source file).

## 2. Competitor landscape

| Player | Status | Overlap with the wedge |
|---|---|---|
| **Redouble AI** (YC) | $500K pre-seed, Sep 2024. Says it addresses an "$11B market" and claims clients "save 80% of staff costs". | **This is the exact wedge**: it learns from domain reviewer feedback, recommends whether each output goes to a human, monitors reviewers and flags suspicious reviews. Two years on, no larger round is visible. [ycombinator.com/companies/redouble-ai](https://ycombinator.com/companies/redouble-ai); [YC launch](https://www.ycombinator.com/launches/Lhb-redouble-ai-quality-control-for-ai-in-regulated-industries); [vcbacked.co](https://www.vcbacked.co/company/redouble-ai) |
| **Abundant** (YC) | ~$4.5M seed. On-demand experts behind a "Human Intelligence API" for agents in healthcare, legal and finance. | Workflow plus workforce, and it generates labels as a by-product. [YC launch](https://ycombinator.com/launches/MHz-abundant-on-demand-human-workforce-for-ai-agents); [promptloop](https://promptloop.com/directory/what-does-abundant-ai-do) |
| **HumanLayer** | $500K seed, Nov 2024. Approval workflows for agent tool calls over Slack and email. | Approval routing for agents. [caplight](https://www.caplight.com/company/humanlayer); [humanlayer.dev](https://humanlayer.dev) |
| **Cleanlab TLM** | Commercial product. | A trust score on any LLM output, with "route to human below threshold" as the documented pattern. This is the confidence half of the wedge. [cleanlab.ai/blog/trustworthy-language-model](https://cleanlab.ai/blog/trustworthy-language-model) |
| **Not Diamond** | Model router. | Documents "human-in-the-loop routing". [docs.notdiamond.ai](https://docs.notdiamond.ai/docs/human-in-the-loop-routing) |
| **AWS A2I** | General availability since 2020. | Confidence-threshold or random-sample routing to your own staff, Mechanical Turk or vendors. It is the free default for AWS shops. [aws.amazon.com/augmented-ai/features](https://www.aws.amazon.com/augmented-ai/features/) |
| **Google Document AI HITL** | **Deprecated and shut down Jan 2025.** Google sends customers to SIs (Devoteam, Searce, Quantiphi). | A hyperscaler judged generic HITL tooling not worth keeping. [docs.cloud.google.com/document-ai/docs/deprecation](https://docs.cloud.google.com/document-ai/docs/deprecation?authuser=0); [discuss.google.dev](https://discuss.google.dev/t/hitl-alternative-human-in-the-loop/181104) |
| **Langfuse / LangSmith annotation queues** | Free or bundled. | Expert review queues, corrections and escalation to more reviewers. Braintrust's review is score-only. [langfuse.com annotation queues](https://langfuse.com/docs/evaluation/evaluation-methods/annotation-queues); [langchain.com LangSmith vs Braintrust](https://www.langchain.com/resources/langsmith-vs-braintrust) |
| **HumanSignal (Label Studio)** | Evaluation engine for in-production review, plus "Interfaces" (Jun 2026): reviewer UIs generated by an agent. | The reviewer-workflow half of the wedge. [labelstud.io/blog/new-evaluation-engine](https://labelstud.io/blog/new-evaluation-engine); [humansignal.com press](https://humansignal.com/press/interfaces-in-label-studio-enterprise) |
| **IDP vendors** (Hyperscience, Rossum, Instabase, Extend) | Mature category. | Field-level confidence thresholds, STP rate as the KPI, and reviewer corrections fed back into training. **The 40%→10% claim is their standard pitch.** [hyperscience.ai](https://www.hyperscience.ai/?p=10487); [extend.ai confidence scoring](https://www.extend.ai/resources/best-confidence-scoring-systems-document-processing) |
| **Vertical autonomous vendors** (CodaMetrix, Fathom) | 93%+ straight-to-bill. | Confidence routing is the product itself. |
| **Scale / Surge / Mercor / Snorkel / Invisible / Labelbox (Alignerr)** | Scale expects >$1B revenue in 2026 after the Meta deal and a 14% layoff. Mercor is at ~$2B annualized gross revenue and in talks at a $20B valuation. Snorkel raised a $350M Series E at $3.5B with a $375M run rate. Invisible is valued at $2B+. | Mostly training and eval data for labs. They supply expert workforces and could add production review, but most do not sell routing software to vertical apps. [kucoin/Scale](https://www.kucoin.com/news/flash/scale-ai-revenue-expected-to-exceed-1-billion-in-2026-as-enterprise-ai-applications-grow); [sacra.com/c/mercor](https://sacra.com/c/mercor/); [implicator.ai Snorkel](https://www.implicator.ai/snorkel-ai-350m-series-e/); [bgov Invisible](https://news.bgov.com/crypto/scale-ai-rival-invisible-technologies-valued-at-over-2-billion) |
| **TaskUs / BPOs** | AI Services +58.6%. Plans to invest $25M+ in "AI-led outcome-based solutions" in 2026. | They sell review labor and are moving toward outcome pricing, which means they will build their own routing to protect margin. [businesswire](https://www.businesswire.com/news/home/20260224268151/en) |
| **Research** | Conformal abstention, learning-to-defer and selective conformal uncertainty (SConU, ACL 2025). | The methods are public and no startup owns them. [arXiv 2502.06884](https://www.arxiv.org/abs/2502.06884); [SConU](https://preview.aclanthology.org/setup/2025.acl-long.934) |

## 3. Do companies still build their own review tooling?
**Yes, for structural reasons that work against a vendor:**
- **The routing threshold is the product.** EvenUp, CodaMetrix and Instacart's PARSE (which routes low-confidence output to humans) all tie confidence to domain-specific error costs and rubrics. That is the same "taste layer" problem that sank F-B.
- **The review UI is domain-specific.** Medical chronologies with links back to the source, demand-letter drafting standards and catalog attributes don't share a UI. HumanSignal's answer (agent-generated custom interfaces) makes a custom build cheap rather than making a vendor necessary.
- **Reviewer data is training data.** Every correction feeds the vendor's model moat (EvenUp's Piai, Abundant's pitch), so vendors want to own the pipeline.
- **Evidence of generic-tool failure:** Google killed Document AI HITL, A2I stagnated, and Redouble has not grown past its pre-seed in two years. Buyers chose internal builds or SIs.

## 4. Buyer count and dollars

| Item | Estimate |
|---|---|
| AI-native vertical companies with a staffed credentialed review team of ≥10 (legal, medical, insurance, tax, compliance, coding) | **~100–300 [E]** |
| Enterprises running review queues on internal AI (claims, KYC, catalog) | Thousands, but they are served by IDP, BPOs and SIs today. |
| Reviewer cost per vertical buyer | $1–15M/yr (EvenUp at 250+ experts is about $20–35M/yr [E]). |
| Software spend they would give a third party | **$50–300K/yr [E]**. Vendors price against reviewer savings, but the buyer's own ML team owns the same goal. |
| Addressable software dollars (AI-native segment) | ~$15–90M/yr [E]. The bigger pool is BPO-style services at low margins. |

Bessemer reports vertical AI growing ~400% YoY at ~65% gross margins ([agentmarketcap.ai](https://agentmarketcap.ai/blog/2026/04/15/bessemer-vertical-ai-2026-thesis-400-percent-growth)). Human review is a main reason margins sit at 65% rather than 80%, so vendors are attacking that themselves.

## Re-score (10 criteria)

| Criterion | SYNTHESIS | Verified | Why |
|---|---|---|---|
| Pain today | 8 | **7** | Real and costly (EvenUp, BPO growth), but it sits in a narrower set of companies than cluster 5 suggested. Harvey, Vanta, Snyk and Semgrep push review onto customers. |
| Dollars attached | 8 | **6** | Reviewer cost is large, but the share a third-party tool can capture is $50–300K per buyer. |
| Headcount attached | 9 | **7** | Hundreds at a few vendors and large BPO pools. The typical product company has 1–10. |
| Growth rate of pain | 8 | **6** | Volume grows, but the review *share* is falling fast inside vendor products (coding +15 pts at UMass, IDP at 75–90% STP). The pain partly solves itself. |
| Ease of finding buyers | 6 | **6** | Visible through reviewer job posts, but each buyer's ML team sees this as its own job. |
| 30-day pilotability | 6 | **6** | Measurable offline on historical reviewer decisions, but it needs data access and a domain rubric. |
| Existing internal builds | 7 | **5** | Built in-house because the routing threshold is core IP. That signals "not outsourceable", not "unserved". |
| Competitive opening | 5 | **4** | Redouble, Abundant, HumanLayer, Cleanlab, A2I, Langfuse/LangSmith queues, HumanSignal, IDP vendors, BPOs. Google's exit shows how weak horizontal demand is. |
| Expansion potential | 7 | **5** | Could expand into a reviewer marketplace, but that collides with Mercor ($2B) and Snorkel. |
| $10B potential | 6 | **3** | No horizontal HITL company has broken out in 6 years (A2I is from 2020). Value sits with the vertical vendors and the labor marketplaces. |
| **Average** | **7.0** | **5.5** | |

## Sharpest surviving wedge
**"Auto-approve certification": a statistically guaranteed review-sampling policy, plus continuous reviewer QA, for regulated AI vendors that must defend *why* they don't review everything.**
- **Buyer:** vertical AI vendors in legal, medical, coding and insurance (EvenUp-, CodaMetrix- or Supio-style) whose customers, malpractice insurers or auditors ask "what's your error rate on unreviewed output?" A second buyer is BPOs moving to outcome pricing.
- **Mechanism:** sit on the vendor's existing review logs. Fit a conformal risk-control threshold that guarantees error ≤ X% at 95% confidence, and choose a spot-check rate for the auto-approved slice. Monitor drift and inter-reviewer agreement, and flag reviewers who rubber-stamp or diverge. The output is an audit-ready report each period.
- **Why it might survive:**
  - It doesn't try to own the vendor's confidence model, only the *proof* and the *reviewer audit*.
  - Neutral third-party attestation is something a vendor can't credibly do for itself.
  - It is recurring, tied to model changes, and the EU AI Act Article 14 deadline (Dec 2027) and its automation-bias clause point at it.
- **Why it is still weak:**
  - Redouble already pitches "flag suspicious reviews".
  - Audit firms and AI-assurance startups could claim attestation.
  - The buyer pool is ~100–300.
  - It looks like a $20–80M ARR niche [E].
- **Estimated score:** ~6.0, unverified.

## Verdict
**It drops from 7.0 to about 5.5.** F-D found a real and visible workforce, but SYNTHESIS read it wrongly in three ways:
1. **"Review queues grow with volume" is half true.** Volume grows, but vendors are pushing the review share down themselves, because it is their gross-margin lever and their product KPI. The 40%→10% claim is the standard IDP and autonomous-coding pitch, already delivered by the vertical vendors.
2. **"Built internally" means the threshold is core IP**, not that the market is unserved. Horizontal HITL has repeatedly failed to become a large business: Google shut its offering down, A2I stalled, and Redouble and HumanLayer are still at pre-seed scale.
3. **The money sits with labor, not software.** Mercor, Snorkel, Surge, Invisible and TaskUs capture expert-review spend, so a routing tool takes only a thin slice.

Round 32 still has no finalist at 8.5 after verification:

| Finalist | Verified score |
|---|---|
| F-A | 6.8 |
| F-A' | 5.9 |
| F-B | 5.9 |
| F-C | 5.9 |
| F-D | 5.5 |
