# H2 — "Humans for agents": verified-human dispatch API for enterprise agents

**Date:** 2026-10-06 · **Analyst stance:** skeptical / red team · **Searches used:** 38 of 40 (WebFetch blocked for ycombinator.com; facts below come from search snippets unless marked)
**Verdict: KILL** (avg 5.0, Competition position 2, Defensibility 3). The one leftover piece worth noting is in §8. It is not a B candidate.

---

## 0. Bottom line in five lines
1. **The behavior is real, but it is mostly consumers, crypto projects and developers.** In 2026 at least 10 "agents hire humans" platforms launched with an API or MCP endpoint. The clearest demand number points the wrong way: RentAHuman had **~160K humans signed up but only 81 agents posting jobs** (Feb 2026).
2. **This failed in public already. It was not "too early to see."** It went from YC batch to a $12M seed to clones within about 8 months (F2). Payman, the original "AI that pays humans" company, **moved to community-bank agent banking** (ICBA ThinkTECH, May 2026). We found no enterprise customer evidence for the "agent pays a human" flow.
3. **The supply owners are moving to own the agent interface (F1).** Upwork MCP server (Aug 10, 2026). Thumbtack in OpenAI Operator, Angi app in ChatGPT (Mar 2026), Airtasker booking in ChatGPT. DoorDash Tasks app on top of its courier base. Uber Digital Tasks. Field Nation is building agentic auto-dispatch into its 2026 roadmap.
4. **Vertical "send a vetted human to take verified photos" already has scaled incumbents with APIs.** ProxyPics has 450K collectors and is the first verified provider of the GSE Uniform Property Data Report (May 2026). WeGoLook (Crawford) has 45K "Lookers" and Duck Creek/CCC integrations. Merchant site-inspection firms sell to payments companies through an API. Agents are just a new caller for these APIs.
5. **"Verified human" is not a moat.** Veriff (used by Hire-a-Human), Persona, Incode and Didit all sell gig-worker liveness and anti-account-sharing. World AgentKit and Proof x401 own "proof of the human behind the agent." Vara's edge improves one feature of someone else's marketplace. It does not create the marketplace.

---

## 1. Evidence that agents need humans for steps

| Signal | What it shows | Source (verification) |
|---|---|---|
| RentAHuman (YC, Liteplo/Tani, launched early Feb 2026): API + MCP, stablecoin pay, errands, queues, photos | Behavior exists; **thin demand side**: 81 agents vs 160K humans (Feb); later claims 700K humans / 11K bounties (Apr); researchers found only ~83 visible profiles; has a "RENT" token | [Storyboard18](https://storyboard18.com/brand-makers/robot-bosses-want-you-ai-agents-are-hiring-humans-now-88979.htm), [Analytics Vidhya](https://www.analyticsvidhya.com/blog/2026/02/ai-hiring-humans/), [GadgetReview](https://www.gadgetreview.com/rent-a-human-the-weird-2026-marketplace-where-ai-agents-are-hiring-humans), [Forbes](https://www.forbes.com/sites/ronschmelzer/2026/02/05/when-ai-agents-start-hiring-humans-rentahumanai-turns-the-tables/), [Medium/XT token](https://medium.com/@XT.exchange/rentahuman-rent-explained-how-the-token-fits-the-ai-agent-narrative-a14522c40c63). "$12M seed" ([startuphub](https://www.startuphub.ai/startups/rentahuman.md)) and "500K users, $20K MRR in 2 weeks" (YC listing snippet, [YC](https://www.ycombinator.com/companies/rentahuman)): **unverified, self-reported** |
| Upwork CEO: clients' agents post job ads to hire humans but "aren't very good at it"; human+agent pairs raise completion by 70%+ | Digital human-for-agent demand exists, and the incumbent marketplace captures it | [Semafor, Mar 12 2026](https://www.semafor.com/article/03/12/2026/upworks-ceo-on-the-ai-agents-that-try-to-hire-human-workers), [CDO Magazine](https://www.cdomagazine.tech/aiml/ai-agents-are-posting-job-ads-on-upwork-and-theyre-not-very-good-at-it) |
| Upwork MCP server, Aug 10 2026: agents turn a request into a job post, shortlist and draft an offer | **Platform absorption** of the digital half | [Upwork press release](https://www.upwork.com/press/releases/upwork-talent-is-now-everywhere-ai-works) (date from snippet) |
| Human API (Eclipse Labs): API launched Jan 2026, mobile app Apr 2026, focus on audio data | Crypto-adjacent; mostly training data, not enterprise ops | [TechStartups](https://techstartups.com/2026/04/01/human-api-launches-mobile-app-to-let-ai-agents-hire-humans-for-paid-tasks/), [Investing.com](https://ca.investing.com/news/company-news/exclusive-human-api-exits-stealth-aims-to-bridge-ai-agents-and-human-labor-4451736). "$65M" ([HackerNoon](https://hackernoon.com/the-app-that-lets-ai-agents-hire-you-human-api-goes-mobile-with-a-$65mn-long-on-human-data)) **is probably Eclipse's own raise, attributed to Human API — unverified** |
| Quest (Singapore): agents dispatch "Heroes" via MCP; ~750K users in 8 markets (Jul 2026) | An Asian gig network already added agent dispatch | [Wikipedia](https://en.wikipedia.org/wiki/Quest_(Singapore_company)) (unverified secondary) |
| DoorDash Tasks (2M US couriers; shelf scans, entrance photos, menu photos), Uber Digital Tasks, Instacart | The largest verified-human field networks are productizing "tasks" themselves | [NBC](https://www.nbcnews.com/tech/tech-news/doordash-now-letting-drivers-train-ai-rcna264387), [Entrepreneur](https://www.entrepreneur.com/business-news/doordash-offers-gig-workers-tasks), [PYMNTS](https://www.pymnts.com/artificial-intelligence-2/2026/the-gig-economy-is-now-the-training-layer-for-ai/) |
| Amazon moved MTurk, SageMaker Ground Truth and **Augmented AI (A2I, AWS's HITL-review service)** to maintenance; closed to new customers Jul 2026 | **Counter-signal:** AWS is leaving generic "human-in-the-loop as a service" | [The Decoder](https://the-decoder.com/amazon-sunsets-mechanical-turk-the-original-artificial-artificial-intelligence/), [mezha.net](https://mezha.net/eng/bukvy/734219b0_amazon_closes_mturk/) |
| Noema essay (Umang Bhatt, Cambridge): agents need humans as sensors, verifiers and bearers of liability | The thesis is public, and has been since Mar 2026 | [Noema](https://www.noemamag.com/ai-agents-are-recruiting-humans-to-observe-the-offline-world/) |
| Enterprise agent signal (procurement / vendor onboarding) | Agents cut onboarding from days to hours. The remaining human step is **internal approval**, not a hired human. We found no enterprise post saying "our agent needed to procure an external verified human" | [MarketScale](https://www.marketscale.com/industries/software-and-technology/southeast-asian-enterprises-cut-vendor-onboarding-from-5-days-to-4-hours-with-agentic-ai) |

**Read-through:** demand from enterprise agent builders for *external* verified humans is **not visible**. The visible demand comes from hobbyist/crypto agents, AI training-data collection, and digital freelancing. The digital freelancing piece is already absorbed by Upwork.

## 2. Competitor map

**A. Horizontal "agents hire humans" (crowded, F2):** RentAHuman (YC, ~$12M), Human API (Eclipse), Quest (SG, MCP), Humwork (YC Spring 2026; agent→expert chat in under 30s, 3,000 verified experts, $500K seed — [neuronfeed](https://neuronfeed.com/startups/humwork), [yctierlist](https://yctierlist.com/s26/humwork/)), SanctifAI (verification/escalation/consultation, on-chain attestations — [Hatchworks](https://hatchworks.com/?p=34958)), NeedaHuman.ai (GPS + freshness codes — [site](https://needahuman.ai/)), HumanForHire ("Human Execution API", claim SLA, webhook proof bundles — [site](https://www.humanforhire.net/)), HumanTask API (property/address/store verification modules — [site](https://humantaskapi.com/)), Hire-a-Human (Veriff-verified — [site](https://hire-a-human.ai/)), Human Dispatch MCP ([G2](https://ai.g2.com/marketplace/tools/human-dispatch-mcp)). Many of these already pitch **evidence bundles plus verified humans**, which is our exact product.

**B. Supply owners adding agent interfaces (F1):** Upwork MCP; Thumbtack (Operator), Angi and Airtasker in ChatGPT ([Thumbtack](https://press.thumbtack.com/announcements/thumbtack-launches-as-home-services-collaborator-for-openais-new-operator), [Angi](https://www.barchart.com/story/news/560053/angi-launches-the-angi-app-in-chatgpt), [IT Brief](https://itbrief.com.au/story/airtasker-launches-chatgpt-booking-for-local-services)); DoorDash Tasks, Uber Digital Tasks; Field Nation (2026 strategy: agentic auto-dispatch, rate negotiation, event-driven "if X, dispatch Y" — [Field Nation](https://fieldnation.com/resources/field-nation-2026-product-strategy)); WorkMarket inside ADP's agent marketplace push ([ADP](https://mediacenter.adp.com/2026-03-02-ADP-Marketplace-Launches-AI-Agents-to-Help-Make-Work-Easier,-Smarter)).

**C. Vertical verified-capture incumbents (already API-first):** ProxyPics (450K collectors, Freddie Mac UPD integration, first verified UPDR provider — [ProxyPics](https://www.proxypics.com/proxy-pics-becomes-first-verified-provider-of-uniform-property-data-report-updr-bringing-standardized-property-data-reporting-to-the-mortgage-industry)); WeGoLook/Crawford (45K Lookers, Duck Creek, CCC — [WeGoLook](https://wegolook.com/), [CCC](https://www.cccis.com/partners/wegolook)); Metro Site Inspections (merchant KYB site visits, order by API — [Metro](https://www.metrositeinspections.com/merchant-site-inspection/)); Shufti Pro on-site enhanced KYB ([docs](https://developers.shuftipro.com/docs/business_identification_risk/know_your_business/enhanced_kyb/onsite)); Truepic / TrueScreen for proof-of-capture.

**D. "Proof of human" and accountable identity:** World AgentKit (Mar 2026) and upgraded World ID (Apr 2026); Proof x401 (v0.1.0 Jun 25 2026, IAL2-bound agent mandates, FIDO) plus Proof's licensed-notary network, which already covers the "legally required human" case ([Digital Transactions](https://www.digitaltransactions.net/tech-firms-begin-to-tackle-the-ai-fraud-question/)); Veriff, Incode and Didit for gig-worker liveness and anti-account-rental.

**E. Human-in-the-loop for enterprise agents (internal mode):** UiPath Action Center, ServiceNow AI Control Tower, Salesforce Agentforce Field Service (internal technician dispatch), OpenAI Presence (escalation to humans), Agno AgentOS HITL, gotoHuman. HumanLayer **left** HITL for CodeLayer (coding IDE). This is the round-9 "H" kill again.

**F. Expert/judgment labor:** Invisible, Scale, Mercor, Surge, Toloka, CloudFactory. They sell to labs and enterprises, and pivot toward "auditability and accountability" use cases ([Sacra](https://sacra.com/research/invisible-vs-mercor)).

## 3. Cold-start reality
- **Single-sided via the customer's own workforce:** possible. But this is enterprise HITL routing, which UiPath, ServiceNow and Salesforce Field Service already own (killed as H in round 9, F1).
- **Single-sided by reselling existing networks through their APIs (ProxyPics, WeGoLook, Field Nation, Upwork MCP, DoorDash Tasks if opened):** possible on day 1. But that makes us a thin aggregator with no supply lock-in, and suppliers each ship their own MCP. Margin is squeezed from both sides: suppliers keep 20–40% take, so we can add maybe 5–10% on GMV.
- **Own supply:** the full two-sided cold start, against RentAHuman, Quest and DoorDash, which already have hundreds of thousands to millions of workers.
- Verdict: cold start is solvable only in forms that are commodity or already owned. **#32 "CS — watch" turns into a confirmed kill.**

## 4. Platform absorption risk
- OpenAI already routes agents to human marketplaces through partners (Thumbtack/Operator, Angi/Airtasker apps, Upwork in ChatGPT). Anthropic has no native marketplace, but MCP makes every supplier one install away, which is the opposite of a gap.
- Suppliers (Upwork, DoorDash, Uber, Field Nation, ProxyPics) have every incentive to own agent demand themselves. They are not conflicted.
- **Risk: high (F1), together with F2 crowding.**

## 5. Market math
- **Unit economics:** physical verification task $25–150 (ProxyPics/WeGoLook-type pricing, unverified). A 25% take on $50 = $12.50 per task.
- **$10M ARR** needs ~$40M GMV, about 800K tasks/yr, about 2,200/day. That is roughly 10–20% of what a ProxyPics-scale network likely does today (inference).
- **$100M ARR** needs ~$400M GMV, about 8M tasks/yr. That is DoorDash Tasks or Crawford scale. The adjacent markets are not small (US building inspectors ~$6.8B, [IBISWorld](https://www.ibisworld.com/united-states/industry/building-inspectors/1405/)), but they are vertical, licensed and served by incumbents.
- **Enterprise buyers who need a *new* agent-callable path:** few. Lenders/servicers, insurers (excluded), and payments KYB already buy on-site capture through existing APIs. Property managers and field-service firms dispatch their own vendors through FSM software (ServiceTitan, Property Meld, Salesforce FS).
- **SaaS ACV alternative (verified-human evidence layer):** $25–75K per marketplace × perhaps 200–500 relevant marketplaces/networks = **$5–35M ceiling (F4)**.

## 6. Finalist format (filled for completeness)

| Field | Answer |
|---|---|
| One-line problem | Enterprise agents stall at steps that need an accountable, identity-verified human (site check, signature, human-only call, judgment). |
| Why now | Agent deployments in ops/procurement/field service (2026); MTurk/A2I sunset; EU AI Act human-oversight obligations from Aug 2 2026; gig account-rental fraud (TransUnion 2026: 31% of Millennial/Gen Z gig workers rented or shared accounts, via [Didit](https://updates.didit.me/blog/gig-economy-identity-verification/), secondary). |
| Exact buyer | Head of Ops / agent platform owner at a lender-servicer, property manager, payments/KYB team, or field-service operator. |
| Exact ICP | US mid-market operators running production agents with ≥1,000 physical-verification events/month. |
| Current workaround | Agent escalates to an internal queue (UiPath/ServiceNow), or the workflow calls ProxyPics/WeGoLook/site-inspection APIs, or a human dispatcher uses Field Nation/WorkMarket. |
| Why incumbents can't easily own it | **They can, and are.** Upwork MCP, Field Nation auto-dispatch, DoorDash Tasks, OpenAI-partner marketplaces. Failed check. |
| 30-day MVP | MCP tool `request_verified_human(task, location, SLA, evidence_schema)` routing to ProxyPics/Field Nation/Upwork APIs, with Vara liveness re-check at task start and signed capture bundle. |
| Pilot design | One servicer or KYB team: 200 tasks; compare TAT, fraud/redo rate, cost against their current vendor. |
| Pricing hypothesis | $5–15 per task orchestration fee, or 10% of GMV; enterprise mode $30–60K/yr. |
| Expansion path | Evidence data → risk scoring of sites/workers → accountable sign-off network (licensed professionals). In practice, every step collides with Proof, ProxyPics or Upwork. |
| Moat | Weak: supply is rented, evidence formats are being standardized (UPDR, C2PA), and verified identity is a commodity (Veriff/Persona/World). |
| Why $10B+ | Only if agents become the main buyer of human labor *and* buyers need a neutral cross-network layer. Both are speculative, and supply owners are not conflicted. |
| Competitors / threats | See §2 (A–F). |
| CTO sentence | "When your agent needs a human to see, sign or call, one tool call gets a re-verified person on site with a signed evidence bundle, in hours." |
| 5 discovery questions | (1) How many agent runs/month end in a physical or human-only step, and what happens next? (2) Who do you call today (vendor, staff) and what does it cost per event? (3) Have you had a fraudulent or reused-photo field report in the last 12 months, and what did it cost? (4) Would you let an agent dispatch and pay an external worker without human approval, and up to what amount? (5) If ProxyPics/Field Nation/Upwork offered this via MCP, why would you use a third party? |
| Hard kill criteria | <3 of 10 target operators report ≥500 agent-originated human-step events/month; or ≥2 of 3 incumbent networks already expose agent APIs that buyers accept; or no buyer pays ≥$10/task over the vendor price. **Already met on public evidence (criterion 2).** |

## 7. Scores

| Pain | Urgency | ROI clarity | Customer access | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 5 | 4 | 5 | 5 | 7 | 6 | 6 | 5 | 3 | 7 | 2 | **5.0** |

Fails the bar (avg ≥8.5, none <7) on 10 of 11 categories. Causes of death: **F2 (visible race, 10+ startups including 2 YC companies, launched within months) + F1 (Upwork/DoorDash/Field Nation/OpenAI partners) + F4 for the only defensible slice.** Not B: the space is not unresolved or too early for evidence. Evidence exists, and it shows crowding plus weak enterprise demand (81-agent demand side; Payman's exit to banking; AWS sunsetting A2I).

## 8. Residual worth logging (not a finalist)
**"Same-person-as-verified" continuous presence assurance plus signed capture for task networks** (ProxyPics, WeGoLook, DoorDash Tasks, Quest, RentAHuman, Field Nation): re-verify the worker with liveness and behavioral biometrics at task start and capture, then emit a signed evidence bundle that the calling agent or underwriter can trust. This uses Vara's stack directly and is the 4th independent appearance of "proof-of-capture" (rounds 16/17/18 at 6.5–6.7). Ceiling is likely $10–30M ARR (F4), with Veriff/Incode/Didit/Truepic one feature away. If the founders want a cheap check, they can **email 5 task networks (ProxyPics, WeGoLook, Field Nation, Quest, RentAHuman) asking whether redo/fraud from account rental or reused photos costs them ≥$250K/yr. Fewer than 2 yes answers = drop.** Fold it into the round-12 caller-verification / proof-of-capture wedge list. Do not open a new thesis.

## 9. Unverified / caveats
- RentAHuman funding ($12M), MRR ($20K) and user counts are self-reported or from secondary aggregators; the YC page could not be fetched.
- Human API "$65M" is likely Eclipse's parent raise, not a Human API round.
- Quest's 750K users come from Wikipedia (secondary).
- Upwork MCP date (Aug 10 2026) comes from a search snippet of the press release.
- ProxyPics/WeGoLook per-task pricing is inferred, not sourced.
- No enterprise-scale buyer interviews; the enterprise demand finding is "absence of public evidence," which by our own taxonomy is weak. The incumbent-API evidence (Upwork, Field Nation, ProxyPics, DoorDash), however, is direct.
