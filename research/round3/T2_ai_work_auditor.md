# T2 — "The Independent Auditor of AI Work": Kill Analysis

**Date:** 2026-10-05 | **Analyst stance:** skeptical, trying to kill it | **Searches used:** 32 of 35
**Verdict: KILL** as a standalone venture. The pain is real but small in dollars. The data is easy to get, which also makes the product easy to copy. Incumbents are already shipping it as a feature.

Convention: **[V]** = backed by a search result (source named). **[U]** = unverified, an estimate, or only from vendor or SEO marketing. Every figure from a source is from search-result snippets only. I could not open the pages (WebFetch not used), so these are not first-party checked.

---

## 1. Size and growth of outcome-priced AI spend (2026 → 2028)

| Vendor / category | 2026 data point | How much is truly outcome-metered? | Source |
|---|---|---|---|
| Intercom Fin (now "Fin", being bought by Salesforce for ~$3.6B; signed 2026-06-15, closing in Salesforce FQ3 FY27) | Fin ~$110M ARR (Apr 2026), "growing 350%/yr", ~8,000 businesses on Fin; $0.99/resolution | High (per-resolution is the native model). Avg Fin spend ≈ $110M / 8,000 ≈ **~$14K/customer** | [V] dealroom.co/charts/fin-intercom, sacra.com/research/intercom; acquisition: wlrk.com transaction page, shopifreaks, Salesforce 10-Q |
| Sierra | $200M ARR, $15.8B valuation (May 2026 Series E, $950M); "100+ enterprise customers", >40% of Fortune 50; ACV reportedly $1.2–1.8M | Outcome definitions are negotiated in each contract and bundled into multi-year agreements. Likely committed minimums, so the invoice is not purely metered [U] | [V] startupfortune/newmarketpitch/idlen.io; ACV figure [U] (fourweekmba-type secondary sources) |
| Decagon | Crossed $100M annualized revenue (reported Aug 2026); $4.5B valuation (Jan 2026, $250M Series D); 100+ enterprise brands | Per-conversation/per-resolution mix [U] | [V] Bloomberg (Jan 28 2026), valueaddvc.com |
| Zendesk AI agents | Outcome pricing ~$1–2/resolution; since May 2026, three tiers (Assisted escalation / Contained / **Verified** resolution). Only Verified is billed, after a 72-hour window **plus a secondary-LLM check** | High, but billed against prepaid "Resolution Allowance" | [V] futurumgroup.com, cmswire (Relate 2026), robylon.ai, support.zendesk.com announcement |
| Salesforce Agentforce | Agentforce ARR >$1.5B (+240% Y/Y) in Q2 FY27 (reported Aug 26, 2026), on an expanded definition that includes Slackbot and Headless 360 | Mostly **not outcome-priced**: Flex Credits ($0.10/action), $2/conversation, per-user licenses. A $2/resolution packaged service agent only reached GA in July 2026. Enterprise Flex commitments are ~$500K minimum | [V] investor.salesforce.com Q2 FY27 PR; pricing: redresscompliance, eesel [V/U] |
| AI SDR (pay-per-meeting) | Small vendors; show rates of 40–60% vs 70–85% for human SDRs | Outcome-priced, but contracts are small (mostly <$100K) [U] | [V] vantaige.io, prospeo.io |
| IT/BPO services outcome contracts | TCS: ~80% of contracts in its finance/HR/business-services segment are outcome-based (not 80% of all TCS revenue). Coforge: outcome contracts ~$150M (6–7% of $2.5B run rate). Outcome-based share of new outsourcing deals: 22% (2023) → 38% (2025); IDC: 30% of IT services contracts outcome-based by 2029 | Large dollars, but measured through negotiated SLAs/KPIs and the existing advisory ecosystem (ISG, Everest, Gartner, Big-4) | [V] Reuters via zawya/ibtimes; opsiocloud citing IDC [U on primary] |
| Macro | 23% of AI builders use some outcome-based pricing (another sample of 80 agent companies: 3.8%). Hybrid (base + variable) is the default for 41% of vendors. 41% of large-enterprise AI SaaS contracts include variable outcome-linked components | Pure outcome pricing is still a minority model, concentrated in support and sales | [V] withorb.com stats roundup, Futurum 1H26 survey |

**Analyst estimate [U]:** Spend on outcome-metered *AI agent work* (CX plus sales), where the invoice actually moves with a vendor-counted outcome, is **~$0.8–1.5B globally in 2026**. It could reach **~$3–6B by 2028** if Fin, Sierra, Decagon and Zendesk keep growing 2–3x a year and Agentforce's per-resolution SKU takes off. The much larger IT-services outcome pool (tens of billions) has a different buyer and existing referees, so it is not this startup's addressable market.

---

## 2. Evidence of distrust, disputes and "resolution gaming"

**Real signals [V]:**
- **Definitional gap.** Vendors claim 65–86% resolution (Fin 76%, Sierra 80%, Decagon 80%, Ada 75%). Production evidence clusters at 40–70%, and Fin's own case studies sit at 42–50% (dragapp.com). Intercom itself reports a 67% average while independent tests cluster at 38–53% (superframeworks). At $0.99, a claimed 76% that lands at 45% nearly doubles the effective cost per truly resolved conversation.
- **The "assumed resolution" problem.** Fin bills when a customer stops replying without asking for more help. Intercom's community has a thread titled "Fin's flawed resolution assumption" (community.intercom.com). Reddit r/SaaS (Nov 2025): "The 'resolution tax' is pissing people off" [V via secondary summary].
- **The "Cost-Per-Resolution Trap" post** (buildmvpfast.com): "the vendor writes the definition of the exact word you are paying for." Zendesk's old model counted 72 hours of silence plus an LLM "relevance" check as a resolution.
- **Consumer side.** Only 24% of 2,000 consumers (Ada/NewtonX, Mar 2026) said their last AI service interaction was fully resolved by AI (getmacha/richpanel citing it).
- **Gartner.** "Buyers struggle to understand the relationship between AI agent costs and outcomes delivered" (Gartner abstract). Gartner also runs a workshop on pricing AI agents to match buyer expectations for outcomes.
- **Practitioner advice** is to manually pull 50 random "resolved" tickets each month and read them (dragapp). So customers do audit by hand today, but casually.

**Why these signals are weaker than they look:**
- Most of the "gaming" content is **competitor marketing** (Lorikeet, Decagon, Drag, Macha, eesel, Maven), with each vendor attacking the others' definitions. I found **no public billing dispute, lawsuit, or named enterprise clawback** over AI resolutions.
- **Vendors are already fixing it themselves.** Zendesk's May 2026 move to "Verified resolution" (a secondary LLM confirms, and only verified resolutions are billed) is the vendor taking over the auditor's role. Sierra negotiates outcome criteria in each contract. That turns the conflict into a contract-definition question, not a data-verification question.
- The complaints come mostly from **SMB and mid-market Fin users** (average ~$14K/yr). Those are not $50K-ACV buyers.

---

## 3. Competitor / adjacent landscape

| Player | What it does | Vendor-neutral? | Does "independent verification of outcome-priced AI invoices"? | Threat |
|---|---|---|---|---|
| **Vaudit (TokenAudit, VendorAudit, AdAudit)** | Independent billing audit of AI tokens, cloud, ads, SaaS. Reviewed $34M of AI spend across 60 companies and found ~$1.7M (~5%) in overcharges, ~80% credited back. Customers incl. Panasonic, HP, Honda. ~$8.55M raised | Yes | **Closest match**: positions itself as "the independent verification layer for the vendor economy"; outcome-metric audit is a natural extension | High |
| **factrelay "Reconcile" (Apify Actor)** | Audits Zendesk AI billed Resolution Allowance rows against outcome evidence and buyer rules; flags disputes; **$0.49 per audit** | Yes | **Yes, literally**, for Zendesk | Shows how commoditized it is: a solo developer built it |
| Zendesk QA (ex-Klaus) | Scores 100% of interactions, including AI-agent evaluation; Aug 2026 adds deep evaluation of AI ratings | No (owned by the billing vendor) | No, but it already grades the same conversations | High (platform absorption) |
| evaluagent | QA with an "AI Agent Observability" module; integrates Zendesk, Salesforce, Genesys, Five9, Amazon Connect, Intercom; markets **vendor neutrality** | Yes | Not invoices, but grades bot conversations against the same standard as humans | High (a short step to invoice reconciliation) |
| Rippit (MaestroQA, rebranded Mar 2026) | Conversation analytics plus QA | Yes | No | Medium |
| Oversai | AutoQA for Sierra and Decagon conversations: hallucination detection, scoring | Yes | No (quality, not billing) | Medium-High |
| Level AI, Cresta, Observe.AI | QA and analytics plus their **own** AI agents; Cresta has automated AI-agent testing | No (they compete with the agent vendors) | No | Medium |
| SupportLogic | Support-experience analytics | Yes | Not found | Low-Med |
| Hamming, Cekura, Coval ($28M Series A) | Pre-production simulation and monitoring for voice/chat agents, sold to the **builder** | Builder-side | No | Low (different buyer), but could move toward production evaluation |
| Vendr (Ruth AI negotiator, $15B+ deal data), Tropic (14,000+ suppliers, AI pricing tracking) | SaaS price benchmarks and renewal negotiation | Yes | No outcome verification, but they own the "renewal leverage" expansion this thesis wants | High on the expansion path |
| ISG, Everest Group, HFS, Gartner | Outsourcing contract benchmarking, outcome-based contract advisory, PEAK Matrix | Yes | Covers the IT-services outcome contracts in practice (SLA and benchmark audits) | High in services; locked in |
| Larridin ($17M, a16z/GV), Worklytics | AI adoption/ROI measurement across the workforce | Yes | No | Low-Med |

**Finding:** Nobody of scale owns "outcome-invoice verification for AI agents" as a category. But the pieces exist: Vaudit (billing audit model), evaluagent/Oversai (neutral grading of bot conversations), Zendesk (self-verification), Vendr/Tropic (renewals). The only product doing exactly this is a $0.49 Apify actor. That points to a **feature, not a company**.

---

## 4. Would customers pay? Who, and with what leverage?

- **VP CX / Head of Support:** the natural user, but a **conflicted** buyer. They chose and championed the AI vendor, and an auditor that cuts the claimed resolution rate makes their own ROI story look worse. They want quality insight (QA tools already serve this), not invoice clawbacks.
- **CFO / Procurement:** the right economic buyer, but they engage **episodically** (at renewal or true-up), not continuously. That fits a contingency or one-off engagement (the Vaudit model), not $50K+ recurring SaaS.
- **Leverage and audit rights:** Sierra's outcome definitions are negotiated in each contract, so audit rights *can* be negotiated in [V on the negotiation; audit-rights clauses U]. I found no evidence that standard Fin/Zendesk click-through terms grant per-resolution audit or dispute rights [U]. Zendesk bills against a **prepaid Resolution Allowance**, and Agentforce against **committed Flex Credits** (~$500K minimum). Over-counting therefore burns allowance faster rather than creating an immediate refundable overcharge. Recovery comes as negotiation leverage at the next true-up, not as cash back.
- **Data access:** easy, since helpdesk APIs (Zendesk, Intercom, Salesforce) expose conversations, reopen events and CSAT. **But the vendor often *is* the helpdesk** (Zendesk, Salesforce, and soon Salesforce+Fin). They control the API terms and rate limits, and can ship the same evaluation natively (Zendesk already has).

---

## 5. Bottom-up market math

**Companies with more than $250K/yr of outcome-metered AI agent spend [U, analyst estimate]:**

| Source of spend | 2026 | 2028 (aggressive) | Basis |
|---|---|---|---|
| Sierra customers | 100–250 | 400–700 | 100+ enterprise customers, ACV $1.2–1.8M, 8–12 new deals/month [U] |
| Decagon customers | 80–200 | 300–600 | 100+ enterprises, $100M ARR |
| Fin customers above $250K | 50–150 | 200–500 | 8,000 customers averaging ~$14K; the Fin API Platform SKU starts at $250K |
| Zendesk AI agents above $250K | 50–200 | 200–600 | Enterprise base, $1–2/resolution [U] |
| Agentforce per-resolution / others (Ada, Parloa, Kustomer, Gorgias, Lorikeet, Maven, AI SDR) | 50–150 | 300–800 | Most Agentforce spend is credits, not outcomes |
| **Total (de-duplicated ~25% for multi-vendor)** | **~300–700** | **~1,100–2,400** | |

**ACV options:**
- *Flat SaaS at $50K:* that is 5–20% of a $250K–$1M outcome bill. Buyers will compare it with Vaudit's ~5% overcharge finding, so a $50K fee only pays off at roughly $1M+ of spend. Realistic ACV is ~$25–60K. Only ~200–500 accounts in 2026 have enough spend to justify it.
- *Percentage of recovered dollars (25–35% contingency):* $1M spend × 5–15% disputable × 30% = **$15–45K per account per year**, and it shrinks as vendors tighten definitions (Zendesk already has).
- *Percentage of spend under management (1.5–3%):* $1M → $15–30K.

**Path to $100M ARR:** you need ~2,000 accounts at $50K, or ~1,000 at $100K. The entire 2028 eligible base is ~1,100–2,400 *before* competition and penetration. At an optimistic 20% share by 2028: ~300–500 accounts × $50K = **$15–25M ARR**. Getting to $1B needs (a) the IT-services outcome pool, where buyers already have ISG, Everest and Big-4 assurance, or (b) the benchmark data network, which needs scale you cannot reach first. **The CX-only TAM is ~$60–150M in 2028. That fails the $1B bar.**

---

## 6. Kill signals (ranked)

1. **Too little spend per customer, concentrated in a few hundred accounts.** Fin, the poster child, averages ~$14K/yr. Enterprise outcome spend is held by ~300–700 companies.
2. **Vendors self-verify and contracts absorb the dispute.** Zendesk's LLM-verified billing (May 2026) and Sierra's negotiated outcome criteria remove the definitional ambiguity that is the auditor's reason to exist. This is a repeat of the Round-1 failure: platforms absorb control layers.
3. **Commoditized technically.** It is helpdesk API plus an LLM judge plus invoice CSV matching. A $0.49 Apify actor already does it for Zendesk, and evaluagent, Oversai and Zendesk QA grade the same conversations today.
4. **Platform consolidation.** Salesforce + Fin, Zendesk + Klaus. The billing vendor owns both the system of record and the QA tool.
5. **Buyer misalignment.** The VP CX is conflicted and the CFO only engages at renewal, which means episodic, contingency-style revenue (Vaudit model, ~5% findings) rather than durable $50K+ SaaS.
6. **Prepaid allowances and committed credits** mean over-counting is negotiation leverage, not refundable cash. That weakens the ROI story.
7. **Unit prices are falling** ($0.99 → enterprise discounts below $1). The fee pool shrinks even as volume grows.
8. **No hard dispute evidence.** I found no lawsuits, publicized clawbacks, or named enterprises auditing AI vendors. The noise is SMB complaints plus competitor marketing.

**What would revive it:** a public dispute or clawback at a Fortune-500 Sierra/Decagon customer; analysts (Gartner, Forrester) recommending third-party outcome verification in AI agent contracts; or vendors agreeing to accept third-party measurement as the billing source of truth, the way ad-verification (IAS/DoubleVerify) became the currency in adtech.

---

## 7. Sharpened thesis (best version) and why it still fails

**One-sentence version:** "We are the DoubleVerify for AI agents: the neutral measurement standard both buyers and AI vendors agree to bill against."

The adtech analogy only worked because (a) spend was enormous and fragmented across thousands of publishers, (b) fraud was large and provable (bots, non-viewable impressions), and (c) advertisers collectively demanded a third-party currency. In AI CX: (a) spend sits with ~5 vendors and a few hundred enterprises, (b) the "fraud" is a definitional gap the vendors are already closing, and (c) there is no buyer coalition. Even the strongest version is a **feature of Vendr/Tropic (renewals), evaluagent/Zendesk QA (grading), or Vaudit (billing audit)**.

---

## 8. Scores (1–10)

| Dimension | Score | Rationale |
|---|---|---|
| Pain | 5 | The definitional gap is real (76% claimed vs 42–50%), but the dollars hurt mainly SMBs |
| Urgency | 4 | Felt at renewal and true-up, not continuously; no dispute wave |
| ROI clarity | 6 | Easy to express as "$X overbilled", but recovery runs through allowances and negotiation |
| Customer accessibility | 6 | Helpdesk APIs are open; the buyer is conflicted (VP CX) or episodic (CFO) |
| Pilot speed | 8 | Read-only API plus an invoice gives a report in 2–4 weeks |
| Market size | 3 | ~300–700 qualifying accounts in 2026, ~1–2.4K in 2028; CX TAM ~$60–150M |
| Expansion | 5 | Benchmarks and renewal negotiation are plausible, but Vendr/Tropic and ISG/Everest hold those positions |
| Venture potential | 3 | A credible $20–30M ARR outcome; $1B is a stretch |
| Defensibility | 2 | LLM-judge plus API; already replicated by a $0.49 actor and QA incumbents |
| Why now | 7 | Outcome pricing spreading (Zendesk, Agentforce $2/resolution, Sierra, Decagon) |
| Competition position | 3 | Squeezed between platform self-verification, neutral QA tools, and billing-audit firms |
| **Average** | **4.7** | |

---

## 9. VERDICT: **KILL**

The thesis does not clear the bar on market size, defensibility or venture potential. The market is a few hundred accounts with modest auditable dollars. The product is easy to copy, the platforms are already absorbing it (Zendesk's "Verified resolution", Salesforce buying Fin), and adjacent players can add the feature (Vaudit, evaluagent, Vendr/Tropic). Revisit only if a public enterprise dispute or clawback appears, or if vendors start accepting third-party measurement as the billing currency.

### Key sources (from search results; not opened directly)
- dealroom.co/charts/fin-intercom; sacra.com/research/intercom
- wlrk.com/transaction/salesforce-in-its-3-6-billion-acquisition-of-fin-formerly-intercom
- investor.salesforce.com (Q2 FY27 results press release, Aug 2026)
- bloomberg.com/news/articles/2026-01-28/ai-customer-support-startup-decagon-valued-at-4-5-billion; valueaddvc.com/pulse/decagon-100m-arr-ai-customer-agents-2026
- futurumgroup.com (Zendesk outcome pricing); support.zendesk.com/hc/en-us/articles/10677925692698-Announcing-changes-to-AI-agent-reporting; robylon.ai/blog/zendesk-automated-resolution-explained
- buildmvpfast.com/blog/cost-per-resolution-trap-ai-agents-game-resolution-kpi-2026; dragapp.com/blog/ai-support-agent-resolution-rates/; community.intercom.com (Fin's flawed resolution assumption)
- apify.com/factrelay/reconcile; vaudit.com/post/ai-billing-reconciliation-how-vaudits-tokenaudit-found-1-7m-in-billing-errors; lasvegassun.com (TokenAudit launch, Jun 30 2026)
- evaluagent.com comparison pages; oversai.com/platforms/sierra/auto-qa; coval.ai/blog/hamming-vs-cekura
- withorb.com/blog/outcome-based-pricing-statistics; Futurum 1H26 pricing survey press release
- zawya.com (Reuters: AI reshapes India's IT services contracts)
- gartner.com/en/documents/8053833 (abstract)
