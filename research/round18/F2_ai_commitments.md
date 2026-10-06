# F2: "ProsperOps for AI" (autonomous AI commitment and capacity buying) — finalist deep dive

*Analyst: skeptical research plus red team. Date: 2026-10-06. Thesis #31 in THESES_35, the untested reframe (wedge c) from phase5/B_ai_spend_control.md. 37 web searches; WebFetch is blocked, so all evidence comes from search snippets.*

**Tags:**
- **[V]**: the snippet comes from the primary source or a reputable outlet.
- **[S]**: the snippet comes from a secondary or vendor blog. Treat these as directional.
- **[U]**: unverified, or my own estimate.

Every URL below appeared in a search result. None were constructed.

---

## 0. Bottom line up front

**Verdict: KILL.** This is not a lack-of-pain kill. Three facts about how AI is bought in 2026 break the ProsperOps mechanism.

1. **Large-enterprise AI spend already burns down cloud commits.**
   - Claude bought through AWS Marketplace or Claude Platform on AWS counts 100% toward the AWS EDP.
   - OpenAI models on Bedrock (GA 1 June 2026) can be bought "without leaving their AWS account or their existing $-commitment".
   - The commitment that matters for these buyers is the EDP, MACC or GCP commit. That is exactly what Flexera+ProsperOps, nOps, Archera, Usage.ai and others already manage.
   - AI is becoming a consumption line inside a commitment someone already optimizes.
2. **AI-specific commit instruments are lumpy, illiquid and contract-level.** The instruments are:
   - Azure PTU reservations (1 month or 1 year, locked to model and region)
   - Bedrock Provisioned Throughput and the new Reserved tier
   - Vertex GSUs
   - OpenAI Scale Tier and Guaranteed Capacity (1-3 year terms)
   - Anthropic committed-spend contracts

   No secondary market exists for these. ProsperOps' edge was hourly rebalancing over a liquid instrument set (convertible RIs and Savings Plan laddering). AI commitments are 1-5 negotiated contracts per company per year. That is procurement advisory, and Ramp, Vertice/Tropic, Redress and the cloud resellers already sell it.
3. **The dominant 2026 failure mode is under-commitment, not idle commitments.**
   - Token spend on Ramp grew 20x YoY.
   - Anthropic ends discounts the moment contracted tokens run out.
   - Firms burn their annual AI budget in months.
   - Under-commitment is a "commit more" problem, and the vendor's AE is happy to solve it for free. The conflict-of-interest moat ("no vendor will help you buy less of itself") barely applies when the right move is to buy *more, committed*.

The pieces that are genuinely "buy less" have each been absorbed or are being absorbed:
- **Idle PTUs:** PointFive DeepWaste, nOps, Finout, Microsoft Cost Management.
- **Batch, flex and priority routing:** request-level `service_tier` on Bedrock and OpenAI, plus gateways now owned by Palo Alto and Stripe.
- **Caching:** automatic on Anthropic and Gemini.
- **Self-hosted reserved GPU:** Cast AI (5% utilization data), SF Compute resale ($40M), Ornn ($33M).

Cause of death: **F1 (platform and incumbent absorption) plus F5 (each lever is a feature)**. The structural reason is that AI commitment savings are not liquid enough to support a share-of-savings autopilot.

---

## 1. How large and complex AI commitments are in 2026, and evidence of waste

### 1a. Size

| Data point | Source | Tag |
|---|---|---|
| Anthropic customers spending >$1M/yr went from ~500 (February 2026) to >1,000 (April 2026). About 12 were at that level in early 2024. | https://letsdatascience.com/news/anthropic-hits-50-billion-annual-revenue-f1e10978 ; https://www.gradually.ai/en/anthropic-ipo/ | [S] |
| Ramp: "Enterprise AI contracts are approaching an average of $1M in 2026", and 80% of companies miss AI spend forecasts by ≥25%. Monthly token spend is up 20x (June 2025 to June 2026). | https://ramp.com/blog/ai-token-spend-launch | [V] (vendor) |
| Gartner: AI models and platforms spend of **$64B in 2026** (+63%). Foundation GenAI models alone grow from $11.4B to **$23.4B** (+104%). | https://itbrief.co.uk/story/gartner-forecasts-ai-spending-to-hit-usd-64bn-in-2026 | [V] |
| Anthropic moved enterprise billing from bundled seats to **per-token billing plus a mandatory monthly spending commitment** based on Anthropic's estimate of usage. This applies at renewal and started in November 2025. | https://www.theregister.com/2026/04/16/anthropic_ejects_bundled_tokens_enterprise/ ; https://itbrief.co.uk/story/anthropic-shifts-enterprise-billing-to-token-based-pricing | [V] |
| Anthropic committed-spend discount tiers sit at roughly $100K / $500K / $1M / $5M per year. The bands are ~5-15% / 15-25% / 20-30% off pay-as-you-go. | https://redresscompliance.com/anthropic-claude-enterprise-contract-negotiation-guide.html | [S] (advisory firm) |
| The Information (via TNW): Anthropic's enterprise discounts are **~15% off list**. The discount **ends immediately when contracted tokens run out**, after which customers renegotiate or pay list. OpenAI gives the rest of the month plus one more month. | https://thenextweb.com/news/anthropic-openai-enterprise-discounts-tokens-the-information | [V] |
| OpenAI **Guaranteed Capacity** (19 May 2026): 1-3 year terms, discounts scale with annual spend, up to 1B tokens per minute, **drawable across model families and supported clouds**. | https://www.eweek.com/artificial-intelligence/news-openai-guaranteed-capacity-enterprise-ai-compute/ | [V] |
| OpenAI tiers: Standard, Flex (~50% off), Scale Tier (TPM bought upfront, 30-day minimum, one snapshot) and Priority (renamed "Fast mode" on 30 July 2026, 2x rate). | https://openai.com/api-scale-tier ; https://www.promptlayer.com/glossary/openai-service-tier | [V]/[S] |
| Bedrock now has **four service tiers on one API call** (Reserved, Priority at 1.75x, Standard, Flex at 0.5x), selected with a `service_tier` parameter. Reserved is metered in TPM with minimums of 100K input and 10K output. Classic Provisioned Throughput offers no-commit, 1-month or 6-month terms. | https://flexprice.io/pricing-index/aws-bedrock ; https://docs.aws.eu/bedrock/latest/userguide/prov-throughput.html | [S]/[V] |
| Azure PTUs: hourly, monthly or yearly reservations, locked to model, deployment and region. Up to ~64% (monthly) or 70% (yearly) off hourly. A ~$2,400/month minimum is cited. | https://techcommunity.microsoft.com/blog/finopsblog/unlock-cost-savings-with-azure-ai-foundry-provisioned-throughput-reservations/4414647 ; https://www.finout.io/blog/cloud-vendors-finally-agreed-on-commitments.-ai-vendors-didnt | [V]/[S] |
| Vertex Provisioned Throughput: GSUs with terms of 1 week, 1 month, 3 months or 1 year. Throughput per GSU varies by model. A 50% promo on Gemini Flash PT runs August to December 2026. | https://docs.cloud.google.com/vertex-ai/generative-ai/docs/use-provisioned-throughput ; https://www.nops.io/blog/gcp-provisioned-throughput/ | [V]/[S] |

**Complexity is real.** Finout (27 May 2026) put it this way: cloud commitments converged on flexible spend-based models, but "the AI commitment market is still in 2015". The five AI commitment products on the market look nothing like each other, so cloud-commitment know-how "doesn't transfer to AI" ([S], https://www.finout.io/blog/cloud-vendors-finally-agreed-on-commitments.-ai-vendors-didnt). This is the strongest pro-thesis signal found. It is also written by an incumbent that is positioning to own the space.

### 1b. Evidence of waste

| Waste type | Evidence | Tag |
|---|---|---|
| Idle PTU / PT | Practitioner guidance says PTU breaks even at ~50-70% utilization; below that the commitment is wasted. PointFive lists "underutilized PTU quota" and "underutilized Bedrock PT on low-volume workloads" as standard detections. | [S] https://redresscompliance.com/reserved-capacity-vs-pay-as-you-go-for-azure-openai-enterprise-implications-and-negotiation-strategy ; https://hub.pointfive.co/inefficiencies/underutilized-ptu-quota-for-azure-openai-deployments-da831 ; https://hub.pointfive.co/inefficiencies/underutilized-bedrock-provisioned-throughput-on-low-volume-workloads |
| Unused committed tokens | If an enterprise consumes 70% of its OpenAI allocation, the other 30% evaporates. Carry-forward is negotiable. | [S] https://redresscompliance.com/openai-trueup-trueforward-overages-negotiation.html |
| **Overage at list price** (under-commitment) | Anthropic drops the discount at the cap. Budgets were exhausted within months, which prompted Anthropic spend caps. 80% miss forecasts by ≥25% (Ramp). | [V] |
| Batch / flex not used | No adoption statistic found. Batch adoption rate is **unknown [U]**. Vendor blogs say "most teams have more batch-suitable traffic than they think". | [U] |
| Caching misconfigured | Example: a 7% cache hit rate at ProjectDiscovery. Claims that "95% of enterprise AI teams not using caching" come from low-quality SEO sources. | [S]/[U] https://www.digitalocean.com/community/tutorials/prompt-caching-in-practice-hit-rate |
| Self-hosted reserved GPU | Cast AI 2026 measured ~5% GPU utilization in Kubernetes clusters. ClearML found nearly half of enterprises waste millions on idle GPUs, with hoarding driven by scarcity. | [V] https://itbrief.co.uk/story/cast-ai-report-finds-5-gpu-use-in-kubernetes-clusters ; https://sia.hackernoon.com/nearly-half-of-enterprises-waste-millions-on-underutilized-gpu-capacity |

**Red-team reading of the waste evidence:**
- The largest waste pool, self-hosted GPUs at ~5% utilization, is a scheduling and workload problem. Cast AI, Run:ai/NVIDIA and others already sell into it. It is not a commitment-buying problem.
- The commitment-specific pool (idle PTUs and expiring tokens) is real but **shrinking structurally**, for three reasons:
  - Vendors are converging on spend-based, cross-model, cross-cloud commitments. OpenAI Guaranteed Capacity is drawable across model families and clouds.
  - Demand is growing ~20x YoY.
  - Capacity is scarce: Altman says the world will be capacity-constrained for some time.

  In a scarce, fast-growing market, buyers under-buy. They do not over-buy.

---

## 2. ProsperOps as the analog: what it is, and whether the analog slot is already filled

| Company | Facts | Extends to AI commitments? | Tag |
|---|---|---|---|
| **ProsperOps → Flexera (Thoma Bravo)** | Raised $72M (last round February 2023). Manages ~$6B of annual cloud usage. ARR up >6x in 3 years, revenue growing >90%, EBITDA up 9x. **Acquired by Flexera on 6 January 2026**; price undisclosed. In June 2026 it shipped "Unified Autonomous Rate and Workload Optimization" as a "single brain". Flexera launched an **AI Cost Management platform on 10 June 2026** spanning agents, models, data and compute, explicitly naming Bedrock, with a Fortune 500 early-access program. | **Moving there.** No snippet confirmed autonomous PTU/PT purchasing yet [U]. The engine, the buyer and the distribution are all in place. | [V] https://hig.com/news/h-i-g-growth-partners-completes-sale-of-prosperops/ ; https://flexera.com/about-us/press-center/flexera-expands-its-finops-solution-with-agentic-and-ai-enabled-cost-optimization ; https://www.flexera.com/about-us/press-center/flexera-launches-ai-cost-management-platform-to-address-growing-ai-cost-crisis |
| **nOps** | Manages $4B+ of cloud spend. Autonomous hourly commitment rebalancing across AWS, Azure and GCP. Pricing is share-of-savings ("ShareSave"). Has a GenAI / Bedrock cost product page. | Partial (Bedrock visibility and savings). | [S] https://www.nops.io/genai/ ; https://www.nops.io/sharesave |
| **PointFive** | $60M Series B (Accel), $96M total, ARR 6x. **DeepWaste AI** module covers OpenAI, Anthropic, AWS, Azure and GCP. Detects underutilized PTUs ("up to 99% savings on underutilized PTUs") and runs **"What-If PTU vs PPM economics ... before commitment"**. Its AI detections went from 0 to 17 in one quarter (~$8M addressable). | **Yes, the advisory half of the thesis.** | [S] https://pulse2.com/pointfive-raises-60-million-series-b-to-help-enterprises-control-ai-and-cloud-costs/ ; https://www.pointfive.co/deepwaste |
| **Finout** | Commitment management for cloud. Published the "AI commitment market is still in 2015" analysis and a provisioned-capacity primer. | Positioning [S]. | https://www.finout.io/blog/provisioned-capacity-for-ai-a-beginners-guide-to-dedicated-vs.-on-demand-ai-capacity |
| **Archera** | Insured commitments (walk away after 30 days or 1 year). GCP Guaranteed CUDs added in August 2026. | No AI evidence. Natural extension to "insured PTUs" [U]. | [S] https://www.usage.ai/blogs/finops/tools/archera-alternatives/ |
| **Usage.ai, CloudKeeper Commit, Zesty, Xosphere** | Outcome-priced commitment management (CloudKeeper guarantees 30-45%). | No AI evidence. | [S] https://www.cloudkeeper.com/cloudkeeper-commit-azure |
| **Spot (NetApp)** | The prompt states it went to Flexera. **Not verified in this pass [U].** | — | — |
| **CloudZero** | Does not manage RIs or Savings Plans; it partners for that. | No | [S] https://docs.cloudzero.com/docs/aws-recommendations |
| **Vantage** | Autopilot for AWS Savings Plans. | No AI-commit evidence found [U] | [S] |

**Market size for cloud commitment management [U]:**
- Cloud IaaS/PaaS is ~$400B+. Commitment-eligible compute is perhaps 40-50% of that.
- Tool fees run at ~20-30% of savings. Savings run at ~25-40% of covered spend.
- Theoretical fee pool: low single-digit billions.
- Realized revenue is much smaller. ProsperOps with $6B under management probably had ~$50-100M ARR [U].

Read-through: ProsperOps is the best company in the category, and it reached a PE-to-strategic exit rather than a $10B outcome. **The analog itself argues against a $10B ceiling**, and the analog slot for AI is being claimed by the analog company itself, now owned by Flexera. This is failure-taxonomy assumption #5 in its purest form.

---

## 3. Competitors and adjacent threats, by lever

| Lever | Who already does it | Assessment |
|---|---|---|
| Commit-tier sizing and renewal (Anthropic, OpenAI, Google direct) | **Ramp** tracks "spend commitments against utilization", surfaces pricing benchmarks and recommends extend, renegotiate or cancel (Q2 2026). Also: Vertice, Tropic, NPI, Redress Compliance and other advisors. Vendor AEs push upsizing. | Covered. The CFO channel belongs to Ramp. https://ramp.com/blog/ai-token-spend-launch ; https://ramp.com/new-on-ramp-q2-2026 |
| Azure PTU / Bedrock PT / Vertex GSU right-sizing | PointFive DeepWaste, nOps, Finout, Flexera, Microsoft Cost Management reservation utilization, DoiT and other resellers. | Covered (detection plus what-if). |
| EDP/MACC burn-down via marketplace AI purchases | Cloud resellers and MSPs (DoiT, CloudKeeper), ProsperOps/Flexera and AWS itself. | Covered. This is the incumbents' home turf. |
| Batch / flex / priority routing | Native `service_tier` (Bedrock, OpenAI). Gateways: LiteLLM (OSS), Portkey→Palo Alto, OpenRouter→Stripe, Kong, Cloudflare, TrueFoundry. Routers: Martian, Not Diamond. | Feature. It requires knowing each request's latency tolerance, which is an application decision. |
| Prompt caching configuration | Automatic caching on Anthropic and Gemini. Observability tools (Langfuse/ClickHouse, Helicone/Mintlify) show hit rates. PointFive and Finout detections. | F5 feature. Phase 5 already killed "prompt-cache regressions". |
| Reserved GPU for self-hosted inference | Cast AI, NVIDIA Run:ai, SF Compute (resale; $40M A at $300M), Ornn ($33M, compute futures with ICE index). | Covered, plus the compute-market players. https://docs.sfcompute.com/preview/guides/reselling-introduction ; https://siliconangle.com/2026/06/24/ornn-raises-33m-help-companies-buy-sell-ai-compute-commodity-like-oil |
| Unused committed capacity resale | Possible only for raw GPU (SF Compute, Ornn). PTUs, Scale Tier and Anthropic commits are non-transferable [U, no evidence of transferability]. | No market to build on. |
| Cost per outcome / AI spend visibility | Revenium ($13.5M), Pay-i ($4.9M), Ramp, Vantage, CloudZero, Datadog. | Killed in phase 5. |

**Was a dedicated "AI commitment optimization" startup found?** None, despite three targeted searches. The likeliest reason is that the job is being absorbed as a module by PointFive, Flexera/ProsperOps, nOps and Ramp, rather than that it is undiscovered.

---

## 4. Conflict of interest: does it protect a startup?

**The claim:** "No vendor will help you buy less of itself."

**Where it holds:**
- Anthropic and OpenAI will not tell you to shift 40% of traffic to Gemini Flash at renewal.
- They will not volunteer that your PTU sits at 35% utilization.

**Where it fails:**
1. **The hyperscalers are neutral across models and want the EDP burned.**
   - AWS happily routes your commit to Claude, OpenAI or Nova.
   - Microsoft Cost Management already reports reservation utilization.
   - AWS, Azure and GCP each benefit when a customer shifts *between model vendors* inside their commit.
2. **Third parties with no conflict already exist and own the buyer:**
   - Ramp (CFO and card)
   - Flexera/ProsperOps (FinOps)
   - PointFive and nOps (FinOps)
   - Vertice and Tropic (procurement)

   The conflict argument protects "a neutral party", not "a new startup".
3. **In 2026 the cheapest move is often to commit *more*:**
   - Discounts vanish at the cap.
   - Demand is growing ~20x.
   - Capacity is scarce.

   On this axis the vendor's interest is aligned with the buyer's, which kills the "they won't help you" story for the largest savings lever.
4. **Model deflation is the vendor's own strategy.** Price per 1M tokens fell ~41% from March to September 2026 (Ramp index, per phase 5). Vendors are cutting price to win volume, so the "they won't tell you to buy less" gap is narrower than it was with AWS RIs.

---

## 5. Buyer, company counts and savings-share math

**Buyer:** Head of FinOps / Cloud Economics. Secondary buyers are procurement and the CFO, with the Head of AI Platform as co-signer. Most of these buyers already have Flexera, nOps, PointFive, Vantage or Ramp.

**Companies with >$1M/yr in AI model/API commitments [U]:**
- **Anchors:**
  - Anthropic has >1,000 customers above $1M/yr (April 2026) [S].
  - OpenAI's count is undisclosed. Assume a similar 1,000-2,000.
  - Google and Azure OpenAI add more.
  - There is heavy overlap across vendors.
- **2026: ~2,000-4,000 unique companies.**
- **2028: ~8,000-15,000.** Assumes the Anthropic cohort keeps doubling, slowing to 2x per year.

Only a subset of these have AI-specific commitments that are *not* simply EDP or MACC burn-down. I estimate 40-60% [U].

**Savings-share math [U]:**

| Item | Estimate |
|---|---|
| AI spend in a typical managed account | $5M/yr |
| Incremental savings an optimizer adds over a competent procurement team plus native tooling | 5-10% of spend (better tier sizing, PTU right-sizing, flex/batch shift). Not 25-40%: AI discounts are only ~15-30%, and much of that a buyer gets by signing the vendor's standard tier. |
| Fee at 25% of savings | 1.25-2.5% of spend, i.e. **$60-125K ACV** |
| **$10M ARR** | ~$400-800M of AI spend under management, ~80-160 customers. **Achievable** for a services-heavy team. |
| **$100M ARR** | ~$4-8B under management, i.e. **~15-35% of Gartner's 2026 foundation-model spend ($23B)**, or ~8-15% of a ~$50B+ 2028 pool [U]. That requires category dominance against Flexera, PointFive, nOps and Ramp. **This fails the round-18 constraint "$100M ARR without owning the whole niche".** |

The ceiling is a ProsperOps-sized outcome (sub-$1B exit), not $10B.

---

## 6. Finalist format

- **One-line problem:** Companies committing $1M+ a year to AI vendors pick commit tiers, PTUs and service tiers blind. They pay for idle capacity or fall off their discount into list-price overage.
- **Why now:** Several shifts landed at once:
  - Anthropic moved to per-token billing plus mandatory monthly commitments at renewal (since November 2025) and drops discounts at the cap.
  - OpenAI Guaranteed Capacity (May 2026) introduced 1-3 year terms.
  - Bedrock added four service tiers.
  - Vertex added short-term GSUs.
  - Finout calls the AI commitment market "still in 2015".
- **Exact buyer:** Head of FinOps / Cloud Economics, with procurement as co-signer.
- **Exact ICP:** US enterprises spending $2-20M/yr on AI APIs across at least two vendors, including at least one direct (non-marketplace) commit or PTU reservation.
- **Current workaround:**
  - Spreadsheets plus vendor AEs.
  - Redress, NPI and other negotiation advisors.
  - Ramp commitment tracking.
  - PointFive and nOps detections.
  - Routing purchases through EDP/MACC so the existing commitment tool covers them.
- **Why incumbents cannot easily own it:** **They can, and they are.** Flexera/ProsperOps (same engine and buyer, AI cost platform shipped in June 2026), PointFive (PTU what-if), Ramp (commit vs. utilization) and hyperscaler-native reservation tooling all cover parts of it. Two things block a newcomer:
  - The instruments are non-transferable and contract-level, so there is no liquidity trick a startup could own.
  - Request-tier routing lives in code and gateways.
- **30-day MVP:**
  - Read-only connectors to Azure Cost Management (PTU utilization), the Bedrock CUR and the Anthropic/OpenAI Admin usage APIs.
  - A commit-sizing simulator.
  - A flex/batch-eligible traffic estimator built from request logs.
  - A renewal memo.
- **Pilot design:** Take 3 enterprises with ≥$3M AI spend. Do a free 2-week savings assessment, then a share of *realized* savings for 6 months.
- **Pricing hypothesis:** 20-30% of realized savings, with a floor of $50K per year.
- **Expansion path:** AI SaaS seats and credits, GPU reservations, then outcome-priced invoices. Every step overlaps Ramp or Flexera.
- **Moat:** Weak. Possible sources are a benchmark dataset of negotiated AI rates (a Vertice-style data moat) and cross-customer demand forecasting. Neither is defensible against Ramp's 70K-customer dataset.
- **Why it could be $10B+:** Only if AI compute becomes a liquid, tradable commodity *and* enterprises hold large multi-vendor portfolios of transferable commitments. Then a "treasury desk for AI compute" could exist. Ornn (futures, ICE index) and SF Compute (resale) are building that for raw GPUs, not for model-API commits. Today: no.
- **Direct competitors and adjacent threats:** Flexera/ProsperOps, PointFive, nOps, Finout, Ramp, Vertice/Tropic, Archera, Usage.ai, CloudKeeper, DoiT, Microsoft/AWS/Google native tooling, LiteLLM, Portkey (Palo Alto), OpenRouter (Stripe), Martian, Not Diamond, Cast AI, SF Compute, Ornn.
- **Sentence to send a CFO:** "You're committing $5M to Anthropic and OpenAI next year on a vendor's own usage estimate. We size the commit, the PTUs and the batch share so you neither pay for idle capacity nor fall off your discount, and we're paid only from what we save."
- **5 discovery questions:**
  1. What share of your AI spend runs through an EDP/MACC/GCP commit versus direct vendor contracts?
  2. In the last 12 months, did you pay list-price overage after exhausting a commit, or leave committed tokens or PTUs unused? How many dollars?
  3. Who sized your last AI commit, and with what data?
  4. Do Ramp, PointFive, Flexera or your reseller already flag PTU utilization or commit burn? What do they miss?
  5. Would you let a third party change `service_tier` and PTU counts, or only recommend?
- **Hard kill criteria. Kill if any of these holds:**
  - ≥60% of ICP AI spend flows through hyperscaler commits.
  - Fewer than 5 of 15 report ≥$250K/yr of commitment-specific waste (idle plus overage).
  - Flexera/ProsperOps or PointFive ships autonomous PTU/PT purchasing.
  - Buyers will not grant write access to tiers or reservations.

  **Status:** the first is likely true already for the largest buyers. Flexera's AI platform makes the third imminent.

### Scores (1-10)

| Criterion | Score | Note |
|---|---|---|
| Pain | 6 | Real but bimodal. Overage pain is the larger half, and vendors address it by upselling. |
| Urgency | 6 | Spikes at renewal (annual); not continuous. |
| ROI clarity | 8 | Savings are dollar-measurable. |
| Customer accessibility | 5 | The FinOps buyer is saturated with vendors. |
| Pilot speed | 7 | Read-only APIs make a fast pilot possible. |
| Market size | 5 | ~$0.3-1B fee pool by 2028 [U]. |
| Expansion | 5 | Every adjacency is contested. |
| Venture potential | 4 | The analog exited sub-$1B to a PE platform. |
| Defensibility | 2 | No liquidity, no proprietary data, incumbents already own the engine. |
| Why now | 7 | Real pricing-model churn in 2026. |
| Competition position | 2 | Flexera+ProsperOps, PointFive, nOps and Ramp all moved in H1 2026. |
| **Average** | **5.2** | Bar is ≥8.5 with no score below 7. **Fails.** |

## VERDICT: **KILL**

**Kill reasons, ranked:**
1. The analog company (ProsperOps, now Flexera) and its peers (PointFive, nOps, Finout) have already extended into AI cost and PTU optimization. Ramp covers commit-vs-utilization and renewal advice for the CFO.
2. A large share of enterprise AI spend retires against EDP/MACC commits that existing tools already optimize.
3. AI-specific commitments are illiquid, contract-level and annual, so there is no hourly autopilot to build.
4. In a capacity-scarce market growing ~20x, the main lever is to commit *more*, which neutralizes the vendor-conflict moat.
5. Batch routing and caching are request-level features owned by vendors and gateways.
6. Even the analog's best outcome is sub-$10B.

**Residual worth watching (not a B):**
- **The trigger:** if model-API capacity ever becomes *transferable* (resale of PTU, Guaranteed Capacity or Scale Tier), a liquidity layer becomes possible. That could take the form of an "AI compute treasury" or a secondary market for model-API commits.
- **What to monitor:** OpenAI Guaranteed Capacity terms and any assignment/resale clauses, and whether Ornn or SF Compute extend from GPUs to model-API capacity.
- **Current evidence:** none [U].

### Unverified items
- That Spot/NetApp went to Flexera (not checked).
- ProsperOps ARR and deal price (undisclosed).
- Batch/flex adoption rates (no data found).
- Whether Flexera/ProsperOps already automates PTU/PT *purchasing*, rather than only visibility.
- The OpenAI count of customers above $1M.
- Whether any AI commit instrument is transferable.
- The share of enterprise AI spend that runs through EDP/MACC (the 100% EDP-eligibility of Claude is [S]; the share actually routed that way is unknown).
