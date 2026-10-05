# Phase 1 Problem Discovery: GTM, Support, Services, Workforce and New AI-Created Workflows

Date: 2026-10-05. Analyst notes: evidence below comes from web search results gathered in this session. Many 2026 figures come from vendor blogs or SEO content farms (flagged **[vendor/low-quality source]**). Treat those as directional, not audited. WebFetch was blocked by the egress proxy and the search budget ran out partway through, so a few claims I wanted to cross-check (HN/Reddit threads, Paid.ai and Stigg funding) are marked **unverified**. I did not invent any URLs. Every URL below came back in a search result.

Scoring: STRONG = clear, fast-growing pain + budget owner + no dominant player + an AI-driven "why now" (2027-2032). MEDIUM = real pain, but crowded or slow to adopt. WEAK = a feature, a small market, or already won.

---

## Landscape snapshot (who is already funded)

| Space | Funded players (latest known) |
|---|---|
| AI visibility / GEO | Profound ($180M Series D at $1.8B, Sep 2026; $96M Series C at $1B, Feb 2026), Scrunch ($26M), Peec AI ($29M), Evertune ($20M), Bluefish, AthenaHQ, Otterly, plus Semrush/Ahrefs modules |
| GTM data / outbound | Clay ($115M Series D at $7.1B, 2026; >$100M ARR Dec 2025), 11x, Artisan |
| AI support agents | Sierra ($950M at $15.8B, May 2026; ~$200M ARR), Decagon ($250M at $4.5B, Jan 2026), Wonderful ($150M), Intercom Fin |
| Support QA / agent evals | Solidroad ($25M A, Apr 2026), Coval ($28M A, Norwest), Hamming ($3.8M seed), Cekura (YC), Cresta (~$270M total, $100M ARR), Observe.AI ($213M total) |
| Usage billing | Metronome (acquired by Stripe, ~$1B, closed Jan 2026), Orb (acquired by Adyen, Jul 2026), Stripe Billing |
| RFP / security questionnaires | Loopio, Responsive (RFPIO), Conveyor ($12.5M A), Inventive AI ($4M seed), Arphie ($2.9M), Tribble, Vanta ($4.15B) |
| Hiring fraud | Clarity (acquired by Deel for ~$45-50M), Didit ($7.5M + YC W26), Proof, Persona/Ping (horizontal IDV) |
| AI adoption / spend measurement | Larridin, Worklytics, Zylo/SpendHound (SaaS mgmt), Finout/Vantage (FinOps) |
| Partner ops | Crossbeam (merged with Reveal; $117M total) |

---

## Problems

### 1. B2B vendors cannot see or control how AI assistants describe and rank them during buyer research
- **Who has it:** CMOs and demand-gen and product marketing leads at B2B software and services companies. Roughly 30-50K B2B SaaS companies worldwide plus about 100K+ B2B services firms. Budget sits mostly with companies above $20M ARR (around 8-10K).
- **Evidence:** Responsive's Oct 2025 survey of 350+ buyers found that "nearly two-thirds" use GenAI as much as or more than search when researching vendors, rising to 80% in tech/software (https://www.responsive.io/news/buyer-intelligence-2025). Digital Commerce 360 reports the same shift (https://www.digitalcommerce360.com/2025/10/15/generative-ai-traditional-search-b2b-vendor-discovery/).
- **Economic pain:** Organic and inbound pipeline for a $50M ARR company is often worth $10M+ a year. Losing even 10% of AI-intermediated shortlists is a $1M+ pipeline impact. Willingness to pay today is $30-150K/yr.
- **Existing solutions:** Profound ($1.8B valuation), Scrunch, Peec, Evertune, AthenaHQ, Bluefish, Semrush and Ahrefs (https://scrunch.com/faqs/what-are-the-most-well-funded-ai-visibility-startups-for-aeo-geo-monitoring/).
- **Why unsolved / why now:** Monitoring is solved and crowded. Causal levers (which content or third-party sources move the model) and B2B-specific depth (comparison queries, pricing accuracy, security-claim accuracy) remain thin.
- **Verdict: WEAK as a new entrant.** Profound is already the category leader at $1.8B and about 10 others are funded. Only a sharp B2B sub-wedge (see #2) is still open.

### 2. AI assistants and buyer agents state wrong facts about a vendor's pricing, integrations, compliance or capabilities, and the vendor has no feed to correct them
- **Who has it:** PMM and RevOps teams at mid-market and enterprise B2B software companies (about 10K companies).
- **Evidence:** Responsive data (above). Agent-led procurement coverage: "Product data, pricing rules, availability, technical documentation, certifications, and commercial policies must be structured clearly enough for agents to interpret" (https://elogic.co/blog/ai-agents-b2b-buying/). Scrunch is pivoting its Series A toward an "Agent Experience Platform" that serves structured content to crawlers (same Scrunch URL as #1).
- **Economic pain:** A false "no SOC 2" or "no SSO" statement silently disqualifies the vendor from shortlists, and the cost is invisible. Plausibly $0.5-3M/yr in lost pipeline for a $50M+ ARR vendor. **[estimate]**
- **Existing solutions:** Scrunch AXP, Profound "agent analytics", llms.txt conventions, trust centers (Vanta, SafeBase) and G2 data feeds.
- **Why unsolved / why now:** There is no canonical, signed "vendor facts" layer that AI agents trust. The trust center for agents (security, pricing, integrations, references served machine-readably with attestations) does not yet exist as a category.
- **Verdict: MEDIUM.** It's real and new, but GEO incumbents and trust-center vendors (Vanta/SafeBase) are adjacent and will try to claim it.

### 3. Sellers must answer AI buyer agents that request quotes, RFIs and negotiate, but CPQ and deal-desk systems are built for humans
- **Who has it:** Deal desk, RevOps and sales leaders at B2B vendors with transactional and mid-market motions, plus B2B distributors and manufacturers. Around 20K software vendors plus 100K+ industrial suppliers.
- **Evidence:** "Forrester expects about one in five B2B sellers to face agent-led quote negotiations by the end of 2026" and "Gartner projects AI agents will intermediate $15 trillion in B2B purchases by 2028" (https://elogic.co/blog/ai-agents-b2b-buying/, https://www.marketscale.com/industries/software-and-technology/80-of-b2b-tech-buyers-now-use-ai-agents-forcing-procurement-and-sales-teams-to-rebuild-how-enterprise-deals-get-done). Activant research on agentic procurement (https://activantcapital.com/research/agentic-procurement).
- **Economic pain:** Deal-desk headcount is $150-200K per FTE. Slow quote turnaround loses agent-run competitive bids. For mid-size vendors, the cost of discount leakage and slow quotes is $1-5M/yr.
- **Existing solutions:** Salesforce Revenue Cloud/Agentforce, DealHub, Conga and PROS, but none is agent-facing. On the buy side: Zip, Levelpath, Fairmarkit. No search result surfaced a funded "seller-side agent negotiation" startup.
- **Why unsolved / why now:** Agent-to-agent commerce protocols (MCP, A2A, agentic payments) only became credible in 2025-26. Sellers need guardrailed pricing authority (discount policy as code), agent authentication and audit trails.
- **Verdict: STRONG (timing risk).** It's a one-sentence pitch ("the deal desk for selling to AI agents") with a clear budget owner (CRO/CFO), but volume in 2026 is still early and Forrester's estimate may be optimistic.

### 4. Cold outbound is collapsing because AI SDR volume has saturated inboxes and filters, and teams lack a channel that still works
- **Who has it:** CROs and SDR leaders at about 50K+ B2B companies running outbound.
- **Evidence:** Cold email reply rates fell to roughly 1-3%, and AI SDR platforms sent "an estimated 4-7x more cold email volume into B2B inboxes in 2024-2025 than in 2022". Artisan and 11x reportedly moved to hybrid models (https://laxis.com/blog/state-of-ai-sdr-2026) **[vendor/low-quality source]**. Also LeadGenius: "The idea of an AI SDR is showing some real weakness" (https://www.leadgenius.com/resources/the-idea-of-an-ai-sdr-is-showing-some-real-weakness).
- **Economic pain:** An SDR team of 10 costs about $1M/yr. Falling yield means pipeline cost doubles.
- **Existing solutions:** Clay ($7.1B), Apollo, Outreach, Salesloft, 11x, Artisan, and warm-intro and partner tools (Crossbeam).
- **Why unsolved / why now:** The fix is warm, consented, trust-network channels. Warm intros reportedly convert at 30-50% versus about 3% for cold (laxis, same URL). That's a network-effect business, which is hard to bootstrap.
- **Verdict: MEDIUM.** The pain is huge, but "the new outbound channel" is vague and Clay plus Crossbeam sit nearby. A wedge is buyer-side permissioned intent ("buyers opt in to be contacted by agents").

### 5. Executives at target accounts are drowning in AI-generated sales outreach (email, LinkedIn, voice) and have no buyer-side filter
- **Who has it:** VPs and C-level buyers at mid-market and enterprise companies, plus IT/security teams fielding complaints. Potentially every company with more than 500 employees (around 60K in the US).
- **Evidence:** The same volume data as #4. Gmail and Microsoft retuned filters against AI-pattern outreach (laxis, above).
- **Economic pain:** Exec time is hard to monetize. Willingness to pay is weak: more consumer-ish than an enterprise budget line.
- **Existing solutions:** Native Gmail/Outlook filtering, email security (Abnormal, Proofpoint) and SaneBox.
- **Why unsolved / why now:** The buyer doesn't pay and the email security vendors can extend into it.
- **Verdict: WEAK.** No clear budget owner, and incumbents can absorb it.

### 6. Inbound forms and demo requests are polluted by bots and AI agents, so SDRs waste time and attribution breaks
- **Who has it:** Marketing ops and RevOps at B2B companies with inbound motions (about 50K+).
- **Evidence:** "roughly 22% of analyzed traffic was invalid," with B2B services and technology among the highest invalid rates. "Invalid traffic doesn't just skew analytics – it becomes fake leads in the CRM" (https://www.clickcease.com/blog/?p=11088) **[vendor source]**. ActiveProspect bot mitigation coverage (https://activeprospect.com/blog/bot-mitigation-news/).
- **Economic pain:** For a company spending $2M/yr on paid demand, 20% invalid traffic is $400K of waste plus SDR time.
- **Existing solutions:** ClickCease/CHEQ, ActiveProspect, Cloudflare bot management, HUMAN and Clearbit-style enrichment.
- **Why unsolved / why now:** The new twist is legitimate buyer agents filling forms on a human's behalf. The job is no longer blocking bots but distinguishing good agents from bad ones and routing them (ties to #3).
- **Verdict: MEDIUM.** The "Know Your Agent for inbound" angle is interesting, but bot-detection incumbents are well funded.

### 7. Companies paying AI support vendors per resolution cannot independently verify that a "resolution" was real
- **Who has it:** VPs of CX and support ops plus procurement/finance at mid-market and enterprise companies using Fin, Sierra, Decagon or Zendesk AI. Several thousand today, likely 20K+ by 2028.
- **Evidence:** Intercom Fin charges $0.99 per resolution and Sierra about $1.50 per resolved interaction (https://valueaddvc.com/blog/how-does-sierra-ai-make-money-outcome-based-pricing-enterprise-agents-and-the-business-model-breakdown). "The vendor's margin depends on AI accuracy in production — if a conversation resolves without escalating to a human, the vendor invoices." On attribution: "Without clear documentation, outcome-based pricing contracts routinely collapse into billing disputes within the first quarter of deployment" (https://www.revrag.ai/resources/blog/outcome-based-pricing-ai-contracts-bfsi) **[vendor source]**. Fin's own published resolution figures range from 51% to 76% depending on the source (https://www.anthropic.com/customers/intercom, https://vantaige.io/ai-tool/intercom-fin), which shows how definition-sensitive the metric is.
- **Economic pain:** An enterprise with 2M AI-handled conversations a year at about $1-1.50 each spends $2-3M/yr. If 10-20% of "resolutions" are customers giving up (who then call back or churn), that is $200-600K in overbilling plus hidden churn cost.
- **Existing solutions:** Vendor dashboards (the vendor grades its own homework). QA tools (Solidroad, Klaus/Zendesk QA, MaestroQA) score quality but don't reconcile invoices.
- **Why unsolved / why now:** Outcome pricing is new (2024-26). Gartner forecasts outcome-based pricing elements in 40% of enterprise SaaS by 2026 (cited at https://www.getmonetizely.com/articles/building-an-outcome-based-pricing-model-for-agentic-ai-reimagining-value-in-the-age-of-autonomous-systems) **[secondary citation]**. The market needs a neutral "auditor of AI outcomes".
- **Verdict: STRONG.** "The independent auditor for outcome-based AI contracts" is a clean VC sentence. It starts in support and extends to every agent priced on outcomes. The risk is vendors refusing data access, which requires a customer-side helpdesk integration.

### 8. Support leaders running AI agents cannot systematically find where the AI resolved wrongly, invented policy or failed to escalate
- **Who has it:** CX ops and QA managers at around 10-30K companies deploying AI support agents.
- **Evidence:** The Air Canada tribunal held the airline liable for its chatbot's invented bereavement policy, and "policy hallucinations stopped being a quality issue and became a liability issue" (https://www.respan.ai/resources/support-ai-policy-hallucination). Gartner found 64% of customers prefer companies not use AI in service, citing fear of inaccurate info (cited in the same article). Robylon notes that vendor contracts cap damages at 12 months of fees (https://www.robylon.ai/blog/ai-customer-service-liability).
- **Economic pain:** QA teams cost $300K-1M/yr at mid-to-large companies. Liability and refund exposure comes on top.
- **Existing solutions:** Solidroad ($25M A), Coval ($28M A), Hamming, Cekura, Cresta, Observe.AI, Zendesk QA (Klaus), and the platform vendors' own evals.
- **Why unsolved / why now:** Pre-deploy simulation (Coval) and human-agent QA (Solidroad) are funded. Production monitoring across multiple vendors and agents, tied to policy and liability, is less covered.
- **Verdict: MEDIUM.** It's crowded fast. It's better framed as part of #7 (audit plus QA plus billing reconciliation) than standalone.

### 9. AI product companies cannot see per-customer gross margin as variable inference costs swing, so pricing and packaging decisions are guesses
- **Who has it:** CFOs, pricing leads and founders at AI-native and AI-feature SaaS companies. About 20-40K companies shipping AI features, of which about 5K have meaningful inference spend.
- **Evidence:** "AI-first companies spend 40% to 50% of revenue on model hosting and inference," against 15-20% COGS in traditional SaaS (https://www.getmonetizely.com/articles/the-economics-of-ai-first-b2b-saas-in-2026-margins-pricing-models-and-profitability) **[vendor source]**. AI-native SaaS gross margins run "20-40 points" below classic SaaS (https://enterprisedna.co/resources/ai-pulse/ai-pulse-2026-07-31-ai-native-saas-gross-margins-are-still-running-20-40-points). CloudZero publishes guidance on AI gross margin (https://www.cloudzero.com/blog/ai-gross-margin).
- **Economic pain:** For a $30M ARR AI company, a 5-point margin improvement is worth $1.5M/yr.
- **Existing solutions:** Metronome (now Stripe), Orb (now Adyen), Stripe Billing, CloudZero, Vantage, Paid.ai (agent billing; funding **unverified**), Stigg and Schematic (entitlements).
- **Why unsolved / why now:** Billing rails consolidated into payments companies (Stripe, Adyen). That leaves room for a neutral "margin and pricing intelligence" layer joining cost-per-event with revenue-per-event, though Stripe will push into it.
- **Verdict: MEDIUM.** Real and urgent, but both billing leaders were just acquired by payments giants who will bundle it. FinOps vendors also converge here.

### 10. SaaS vendors are losing revenue to seat compression as customers use AI to do the same work with fewer seats
- **Who has it:** CEOs, CFOs and pricing leads at seat-priced SaaS companies (about 15K+ companies above $10M ARR).
- **Evidence:** "58% of companies report lower NRR because AI productivity enables customers to achieve the same output with fewer people." NRR fell from 110.5% in 2023 to 107.1% in 2025 (https://sbigrowth.com/insights/the-great-unbundling). Worked example: "A 30% seat decline with a 10% price increase still nets out to -23% revenue" (https://mgiresearch.com/research/is-the-saas-business-model-dead/).
- **Economic pain:** A 3-point NRR drop on $100M ARR is $3M/yr, and it compounds.
- **Existing solutions:** Pricing consultancies (Simon-Kucher), Monetizely, Stigg, Schematic, Metronome/Orb and Gainsight for churn signals.
- **Why unsolved / why now:** Re-pricing from seats to usage or outcomes is a multi-year organisational change. Tooling for pricing experimentation, migration modelling and customer-by-customer conversion is thin.
- **Verdict: MEDIUM.** A massive "where the world is going" story, but the work is mostly consulting. A software wedge (pricing migration simulator plus contract conversion) is possible, but ACVs may be lumpy.

### 11. Billing and customer success teams face disputes over usage and outcome invoices that customers did not expect or cannot reconcile
- **Who has it:** Billing ops, finance and CS at usage-priced B2B companies (about 10K+).
- **Evidence:** The "routinely collapse into billing disputes" quote above (revrag). Attribution "is the hard part: a human reply that settles the issue first usually ends the billable event" (https://giga.ai/news/outcome-based-vs-resolution-based-vs-conversation-based-ai-prici).
- **Economic pain:** Bill shock drives churn. Dispute handling takes about 1-2 FTE ($150-300K) plus write-offs at 1-3% of usage revenue.
- **Existing solutions:** Billing platforms (Stripe/Metronome, Orb, Chargebee, Maxio) and spend alerts.
- **Why unsolved / why now:** This is the vendor-side mirror of #7. The opportunity is a shared, verifiable usage and outcome ledger both parties trust.
- **Verdict: MEDIUM.** Better as part of the #7 platform (two-sided outcome ledger) than as its own company.

### 12. CFOs cannot measure ROI on enterprise AI spend (seats, agents, API) and are cutting projects blind
- **Who has it:** CFOs, CIOs and AI program leads at about 20K enterprises with more than 1,000 employees.
- **Evidence:** "Only 14% of CFOs report seeing clear, measurable impact from their AI investments" (Forrester, cited at https://tianpan.co/forum/t/cfos-are-killing-ai-projects-in-2026-only-14-see-measurable-roi-heres-whats-changing) **[secondary]**. VC-backed CFOs expect AI spending to double in 2026 (https://www.cfobrew.com/stories/2026/04/14/vc-backed-cfos-expect-ai-spending-to-double-this-year). SVB's State of the VC-Backed CFO report (https://svb.com/trends-insights/reports/state-of-the-vc-backed-cfo/). Three-quarters of HR leaders report "only moderate or minimal returns" from AI (https://itbrief.co.uk/story/gartner-maps-nine-ai-driven-work-trends-chros-face-by-2026).
- **Economic pain:** An enterprise of 5K employees spends $3-10M/yr on AI seats and agents. Cutting 20% waste or redirecting it to winners is worth $0.6-2M.
- **Existing solutions:** Larridin, Worklytics, Zylo, SpendHound, Productiv, Microsoft Copilot Analytics and vendor dashboards (https://larridin.com/blog/ai-tool-sprawl-enterprise, https://www.worklytics.co/ai-cost-tracking).
- **Why unsolved / why now:** Usage is measurable but impact is not. Linking AI usage to business outcomes (tickets closed, deals won, cycle time) needs joins across systems of record. Vendor-reported metrics are conflicted.
- **Verdict: STRONG (crowding risk).** "The P&L for AI" is a board-level question for 2027-2030. Larridin and Worklytics exist but are small. The winner likely starts from outcome data (see #7), not from seat counts.

### 13. Finance cannot allocate exploding LLM and agent API bills to teams, products or customers
- **Who has it:** FinOps, finance and platform engineering at about 5-10K companies with more than $1M/yr AI API spend.
- **Evidence:** "total enterprise AI spending grew 483% from 2024 to 2026" and "finance receives a single line item it cannot allocate." Example: a 2,000-engineer company spending $1.66M a month across Anthropic, OpenAI, Copilot and Azure (https://futureagi.com/blog/enterprise-llm-gateway-cost-tracking-coding-agents-2026/) **[vendor source]**. Harness also reports that AI spend "has outgrown the systems built to track it" (https://www.harness.io/press-and-news/new-harness-report-reveals-enterprise-ai-spend-has-outgrown-the-systems-built-to-track-it).
- **Economic pain:** At $20M/yr AI spend, 15% optimization is $3M.
- **Existing solutions:** Finout, Vantage, CloudZero, Harness, LLM gateways (Portkey, LiteLLM, Kong, Cloudflare) and Datadog.
- **Why unsolved / why now:** It's real but being absorbed by FinOps and gateway vendors.
- **Verdict: WEAK.** A feature of FinOps and gateways. It's also more of a dev-infra domain than GTM.

### 14. Recruiters cannot tell real candidates from AI-generated, proxy-interviewed or deepfaked ones in remote hiring
- **Who has it:** TA leaders, CISOs and HR at companies hiring remote technical and knowledge workers (about 50K+ companies). Acute at tech, IT services and MSPs.
- **Evidence:** Gartner predicts 1 in 4 candidates will be fake by 2028 (https://wjcw.com/news/report-by-28-1-in-4-job-applicants-will-be-ai, https://www.nbcnews.com/tech/security/fake-job-seekers-are-flooding-us-companies-are-hiring-remote-positions-rcna200199). Experian's 2026 forecast lists deepfake candidates among its top 5 fraud threats (https://thenextweb.com/news/deel-acquires-clarity-deepfake-detection). DOJ has run actions against North Korean IT worker schemes, with roughly 100K DPRK IT workers estimated (https://www.hklaw.com/en/insights/publications/2026/08/hidden-in-plain-sight-labor-employment-and-cybersecurity-risks, https://www.jenner.com/en/news-insights/client-alerts/are-you-employing-a-north-korean-it-worker-what-companies-need-to-know-to-prepare-for-and-respond-to-this-threat).
- **Economic pain:** A single bad hire costs $50-250K (salary, recruiting, remediation). A security breach via an imposter can cost millions. ACV of $25-100K is plausible for companies hiring 200+ people a year.
- **Existing solutions:** Clarity (acquired by Deel for ~$45-50M), Didit, Proof, Persona, Ping, Socure, CLEAR, and ATS add-ons (Greenhouse identity verification).
- **Why unsolved / why now:** Identity is checked once at application, then handed to IT. "The handoff itself being the weak point" (thenextweb above). Continuous identity from candidate to employee to device is unowned, and the buyer is split between HR and security.
- **Verdict: STRONG.** It's clear ("identity assurance from first interview to first laptop"), backed by security budget and a Gartner stat, with fast pilots. The risks are IDV incumbents (Persona, CLEAR) and HR platforms (Deel) bundling it.

### 15. Recruiting teams are overwhelmed by AI-mass-applied applications and can't find signal
- **Who has it:** TA teams at about 100K+ companies.
- **Evidence:** Applications per job rose from 116 to 244 and applications per recruiter from 146 to 746 between 2022 and 2025. LinkedIn processes 11,000 applications per minute (https://blog.theinterviewguys.com/the-quality-paradox/, https://getcoai.com/news/ai-job-applications-flood-linkedin-with-11000-per-minute/) **[low-quality sources; LinkedIn stat widely reported]**.
- **Economic pain:** Recruiter time is $100K+ per FTE, and slow hiring costs more.
- **Existing solutions:** Paradox (acquired by Workday), Eightfold, HireVue, Ashby, Greenhouse AI, Metaview, and many AI recruiter startups (Mercor, Juicebox, Alex).
- **Why unsolved / why now:** It's being heavily addressed. Detecting authentic, unassisted ability (skills proof) is the open piece and overlaps #14 and #16.
- **Verdict: WEAK.** Very crowded with ATS bundling.

### 16. Live interviews are compromised by invisible AI copilots (Cluely-style), making interview signal unreliable
- **Who has it:** Engineering and hiring managers at tech companies (about 30K).
- **Evidence:** Cluely raised $5.3M for a tool that operates "invisible to interviewers, even during screen sharing" and reportedly had $3M ARR (https://techcrunch.com/2025/04/21/columbia-student-suspended-over-interview-cheating-tool-raises-5-3m-to-cheat-on-everything). One source claims "38.5% of candidates are cheating the interview" (https://blog.theinterviewguys.com/?p=17305) **[low-quality source]**.
- **Economic pain:** A mis-hire costs $50-250K.
- **Existing solutions:** CodeSignal, HackerRank proctoring, Karat, return to onsite interviews.
- **Why unsolved / why now:** It's an arms race. It can be bundled with #14.
- **Verdict: WEAK standalone, MEDIUM inside #14.**

### 17. RFP and security questionnaire volume keeps rising, AI buyers make it easier to send them, and accuracy and liability matter
- **Who has it:** Proposal teams, sales engineers and security/GRC at B2B vendors (about 30K+).
- **Evidence:** Responsive's survey says deciding factors remain "trust, industry expertise, and the quality of the RFP response" (https://www.responsive.io/news/buyer-intelligence-2025). The vendor field is wide (https://www.complyjet.com/blog/best-security-questionnaire-automation).
- **Economic pain:** Sales engineer and GRC time runs $200-500K/yr per mid-size vendor.
- **Existing solutions:** Loopio, Responsive, Conveyor ($12.5M), Inventive AI, Arphie, Tribble, Vanta, Drata and SafeBase (acquired by Drata).
- **Why unsolved / why now:** It's largely solved by LLMs. Prices are compressing.
- **Verdict: WEAK.** A commoditising feature. The forward-looking version is #2 (machine-readable vendor facts that remove questionnaires entirely).

### 18. Law and accounting firms whose AI cuts hours cannot price, scope or margin-manage fixed and value-based fees
- **Who has it:** Managing partners, pricing directors and CFOs at about 1,500 law firms with 50+ lawyers in the US (AmLaw 200 and mid-size) and the top 500 accounting firms. Globally about 10K firms.
- **Evidence:** "90% of all legal dollars still flow through standard hourly rate arrangements," and AI creates a "productivity paradox" (https://www.legal.io/articles/5771590/AI-Adoption-Pushes-Law-Firms-Toward-Alternative-Fees-But-Change-Will-Be-Incremental). Top accounting firms are "developing future pricing models" as AI "stand[s] to slash billable hours" (https://news.bloomberglaw.com/financial-accounting/ai-efficiency-gains-push-accounting-firms-to-reimagine-pricing). Coverage that the billable hour is not dead but eroding (https://valawyersweekly.com/2026/08/10/the-billable-hour-is-not-dead-but-ai-is-chipping-away-at-its-prevalence/).
- **Economic pain:** For a $500M-revenue firm, mispricing fixed fees by 5% is $25M. Pricing teams are small and spreadsheet-driven.
- **Existing solutions:** Legal pricing tools (Clocktimizer/Litera, BigHand, Thomson Reuters Elite, Intapp), plus PE-backed accounting rollups building in-house.
- **Why unsolved / why now:** Pricing needs historical matter data plus a model of AI-adjusted effort. Firms adopt slowly ("change will be incremental"). Legal is borderline-regulated.
- **Verdict: MEDIUM.** Large dollars per customer, but a slow-adopting market with entrenched vendors (Intapp, TR Elite). PE-owned accounting firms are the faster entry.

### 19. Professional services and IT services firms can't measure timesheet-based utilization when AI agents do part of the work
- **Who has it:** COOs and finance at consultancies, agencies and MSPs (about 100K+ firms, of which about 10K have more than 100 staff).
- **Evidence:** It follows logically from #18, and from MSP and AI-agency shifts to per-outcome pricing. Direct evidence is thin in this session. **[mostly inference]**
- **Economic pain:** A utilization metric that is wrong by 5 points on $50M revenue is a large staffing error.
- **Existing solutions:** PSA tools (Kantata, Certinia, ConnectWise, Autotask, Harvest).
- **Why unsolved / why now:** PSA vendors will add AI-work tracking.
- **Verdict: WEAK.** Incumbent PSA feature.

### 20. HR and finance lack a way to plan headcount alongside AI agents ("digital workers"): what to automate, what to rehire, what capacity exists
- **Who has it:** CHROs, CFOs and FP&A at about 20K enterprises.
- **Evidence:** Gartner warns of "a risk of cutting roles before AI delivers measurable returns and then needing to rehire." Only 1% of H1 2025 layoffs resulted from AI productivity, and 60% of large enterprises will use AI-augmented workforce planning by end of 2026 (https://itbrief.co.uk/story/gartner-maps-nine-ai-driven-work-trends-chros-face-by-2026). Klarna rebuilt human support capacity after its AI-only push (https://www.respan.ai/resources/support-ai-policy-hallucination).
- **Economic pain:** A wrong 10% headcount cut, followed by rehiring, costs millions at enterprise scale.
- **Existing solutions:** Workday, Visier, Orgvue, ChartHop, Anaplan, Pigment, Lattice ("AI employees" experiment).
- **Why unsolved / why now:** The input data (what AI agents actually complete) isn't standardised. It depends on #7 and #12 outcome data.
- **Verdict: MEDIUM.** A big narrative, but sold into slow HR planning cycles. It's best as a module of an "AI P&L" platform.

### 21. Sales comp and commission disputes are rising as plans get more complex (usage-based revenue, AI-assisted deals, partner splits)
- **Who has it:** Sales ops and comp admins at about 30K B2B companies.
- **Evidence:** "More than 60 percent of sales reps have experienced commission errors in the previous 12 months" (Salesforce State of Sales, cited at https://blog.salescookie.com/2026/05/15/sales-commission-disputes-anatomy-cut-in-half/). Root causes include splits and mid-period plan changes (same source, plus https://www.qobra.co/blog/sales-commission-disputes-how-to-eliminate-them).
- **Economic pain:** Comp admin FTEs plus rep attrition: $200K-1M/yr.
- **Existing solutions:** CaptivateIQ, Spiff (Salesforce), Xactly, QuotaPath, Everstage, Qobra, Varicent.
- **Why unsolved / why now:** It's solved by a crowded field. The new angle is comp for usage and consumption revenue, which incumbents are adding.
- **Verdict: WEAK.** Crowded and mature.

### 22. Salesforce CPQ customers are being forced to re-implement (no automated migration), which opens the deal desk and quote stack to replacement
- **Who has it:** RevOps and deal desk teams at thousands of Salesforce CPQ customers (estimated low thousands of mid-market and enterprise accounts).
- **Evidence:** CPQ entered end-of-sale in March 2025, with EOL expected 2029-2030. "There is no automated migration tool... product rules, bundles, and pricing logic are rebuilt," and reimplementation runs "$100 thousand to $500 thousand" (https://crm.folio3.com/blog/the-end-of-sale-eos-salesforce-cpq/, https://www.everstage.com/cpq/salesforce-cpq-end-of-life).
- **Economic pain:** $100-500K reimplementation plus about $200 per user per month licence.
- **Existing solutions:** Salesforce Revenue Cloud Advanced, DealHub, Conga, Zuora CPQ, PROS, Nue, and SI partners.
- **Why unsolved / why now:** It's a forced-migration window (2025-2030). An AI-native CPQ or deal desk that also handles usage pricing (#9) and agent buyers (#3) could ride it.
- **Verdict: MEDIUM.** A great timing catalyst, but CPQ is a feature-heavy, services-heavy category. Combine it with #3 for venture scale.

### 23. Partner and channel teams can't attribute or orchestrate co-sell when buyers discover via AI and marketplaces
- **Who has it:** Partner and alliance leaders at about 10K B2B software vendors.
- **Evidence:** Crossbeam (25K+ companies, $117M funding) is repositioning as an "AI-era context layer" with MCP (https://komo.ai/directory/crossbeam, https://tech.eu/2024/06/25/crossbeam-acquires-reveal-in-all-stock-transaction/).
- **Economic pain:** Partner-sourced pipeline is often 20-30% of total. Attribution disputes affect partner payouts.
- **Existing solutions:** Crossbeam, Impartner, PartnerStack, Kiflo, and cloud marketplaces (AWS, Tackle, Clazar).
- **Why unsolved / why now:** Crossbeam dominates the data network.
- **Verdict: WEAK.** A network-effect incumbent.

### 24. Customer success teams can't predict churn when AI changes product usage patterns (fewer seats, agent-driven usage)
- **Who has it:** CS leaders at about 15K SaaS companies.
- **Evidence:** NRR compression data from #10 (https://sbigrowth.com/insights/the-great-unbundling).
- **Economic pain:** Each 1 point of gross retention on $100M ARR is $1M.
- **Existing solutions:** Gainsight, ChurnZero, Vitally, Totango and many AI-CS startups.
- **Why unsolved / why now:** Health scores built on seat logins break when agents, not humans, are the users. It's a real but incremental shift.
- **Verdict: WEAK-MEDIUM.** Incumbents will retrain their models.

### 25. Enterprises deploying many AI agents (support, SDR, back office) have no single record of what each agent did, what it cost and what it produced
- **Who has it:** COOs, CFOs and heads of AI ops at about 10-20K mid-to-large companies by 2028.
- **Evidence:** Synthesises #7, #12 and #13. Larridin markets "usage, proficiency, and impact across humans and agents" (https://larridin.com/blog/cio-ai-monitoring). Agent spend chargeback "requires granular attribution that follows the full request tree" (https://www.finout.io/blog/finops-for-ai-agents-a-four-step-allocation-framework).
- **Economic pain:** Combined AI agent spend of $2-20M/yr per large enterprise. Governance gaps carry liability (Air Canada).
- **Existing solutions:** Agent observability (LangSmith, Arize, Datadog), FinOps (Finout), AI measurement (Larridin), and platform-vendor dashboards (Salesforce Agentforce, ServiceNow AI Control Tower).
- **Why unsolved / why now:** Each vendor reports on its own agents. A cross-vendor, business-facing (not engineering-facing) system of record for digital labor (work done, quality, cost, outcome, invoice) doesn't exist.
- **Verdict: STRONG (needs a sharp wedge).** It's "the system of record for the digital workforce", a 2027-2032 category. Platform vendors (ServiceNow, Workday) will attack it, so enter via an urgent wedge (#7 outcome audit) rather than a horizontal dashboard.

---

## Top 5 most promising

1. **Independent outcome audit for AI-agent contracts (#7, with #11 and #8 folded in).** Customers pay Sierra, Decagon and Fin per resolution with no neutral verification, and outcome pricing is spreading across SaaS. Wedge: connect to the helpdesk, re-grade every "resolution" (repeat contacts, sentiment, policy accuracy) and reconcile against the invoice. Expand into an outcome ledger for all agents. The buyer is CX plus procurement, ACV is $50-150K, and a pilot runs in weeks on historical data. Key risk: vendors restrict data or improve their own transparency.
2. **Continuous identity assurance from candidate to employee (#14 + #16).** Gartner's 1-in-4 fake candidates by 2028, the DPRK enforcement actions and Deel's acquisition of Clarity all validate demand. The open gap is the HR-to-IT handoff and continuous verification. Security budget, fast pilots. Key risk: Persona, CLEAR, Okta and Deel bundling it.
3. **Seller-side infrastructure for AI buyer agents (#3 + #2, riding the #22 CPQ migration).** This is a deal desk and vendor-facts endpoint that lets agents get accurate specs, quotes and negotiated prices within policy. Very clear 2027-2032 direction (Gartner's $15T agent-intermediated B2B by 2028). Key risk: timing, since 2026 volume is still small.
4. **The AI P&L / digital-workforce system of record (#25 + #12 + #20).** CFOs can't prove AI ROI: only 14% see measurable impact per Forrester, while spend doubles. It's a board-level question, and Larridin and Worklytics are small. Best entered from outcome data (#1 on this list) rather than seat counts.
5. **Machine-readable, verifiable vendor facts for AI agents (#2).** This is the trust center for agents: it fixes AI misstatements about pricing, compliance and integrations and replaces questionnaires (#17). Key risk: Profound, Scrunch and Vanta/SafeBase are adjacent and well funded.

Explicitly deprioritised: general GEO monitoring (Profound has won), RFP automation, commissions, AI SDRs, recruiting volume tools, partner ops, and LLM FinOps. All are crowded or solved.

### Evidence gaps to close in Phase 2
- Primary practitioner voice (Reddit/HN threads, G2 reviews). Both search and fetch were blocked late in the session, so customer interviews are needed for #7 (do CX leaders distrust vendor resolution counts?) and #3 (are agent-originated RFQs actually arriving?).
- Funding checks for Paid.ai, Stigg, Schematic, Larridin, and any "AI outcome audit" startups (none surfaced, which needs confirming).
