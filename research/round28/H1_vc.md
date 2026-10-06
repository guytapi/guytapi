# Round 28 — H1 through a skeptical VC partner's eyes

**Role:** seed/Series A partner, 2026-10-06. **Hypothesis H1:** at AI app companies, human supervision, exception handling, QA, escalation and recovery costs grow in step with customer volume.
**Search budget note:** the shared web-search budget ran out after 15 searches, so a few competitor facts below come from memory. They are marked **[unverified]**. No URLs were invented.

---

## 1. Start from the money

| Fact | Source |
|---|---|
| AI-product gross margin averages 41% (2024), 45% (2025), 52–53% projected for 2026, and is on track for 59% in 2027. ICONIQ credits falling inference costs, routing and scale, not pricing power. | ICONIQ *State of AI 2026* (iconiq.com/growth/reports/state-of-ai-2026), via SaaStr summaries |
| Application-layer products reach about 60% gross margin in 2027, against 67% for infra/platform products. | Same |
| Inference is about 23% of revenue at scaling-stage AI B2B companies. 84% of them report 6+ points of margin erosion from AI infrastructure. | SaaStr/ICONIQ summaries |
| The forward-deployed engineer has become a permanent GTM motion. Half of companies plan to scale it, and most treat it as a revenue role. | ICONIQ 2026 via SaaStr |
| The labs are moving into services: Anthropic has an AI-native services firm backed by ~$1.5B, and OpenAI's Deployment Company raised $4B+ at ~$10B and is buying FDE benches. | SaaStr/ICONIQ summaries (search snippet) |
| Sierra charges per resolution, ~$1.50 (range $1.00–2.50), and escalations are free. Sierra pays for every failed conversation. Year-one cost is $200–350K+ including professional services. | buildmvpfast.com, fin.ai/learn/sierra-ai-pricing (third-party estimates) |
| Decagon charges per conversation by default, with per-resolution as an option. It does not disclose gross margin or escalation cost. | featurebase.app, fin.ai, sacra.com (third-party) |
| Harvey has ~$350M annualized revenue and is raising at ~$15.5B. Its gross margin is not public. | cryptobriefing.com, tech-insider.org (search snippets) |
| Crescendo, an AI-native BPO, is valued at $500M (GC-led Series C, Oct 2024). It runs 3,500+ human agents, claims ~90% autonomous resolution, and sells "outcome guarantees". | sacra.com, crescendo.ai, BNN Bloomberg |

**What the numbers say, and what they don't:**
1. Margins are improving, not collapsing. Anyone pitching "supervision headcount is destroying AI gross margins" is arguing against the best public benchmark. The honest version: inference is getting cheaper fast, so the human share of COGS is the part that is not falling. As inference approaches zero, the human residual (supervision, exceptions, QA, FDE) becomes most of the COGS that's left. No public dataset splits it out. That missing split is the real unknown in H1.
2. Outcome pricing moves exception risk onto the vendor. Under per-resolution pricing, every failed or escalated case is pure cost. Margin then depends on two numbers: the exception rate, and the cost to handle each exception.
3. The market is already paying for the human residual at scale. OpenAI's ~$10B services arm and Crescendo's 3,500 agents are the clearest proof that "AI plus humans, sold as an outcome" is a real P&L line.

## 2. Push it to 2028–29 (second- and third-order effects)

- **First order:** each AI app company runs an ops team (supervisors, QA, escalation, FDEs) whose size tracks customer count.
- **Second order:** inference costs fall about 10x, so that ops team becomes the largest variable COGS line. Public investors start valuing vertical-AI companies on "cost to serve per outcome" rather than gross margin. CFOs want supervision cost to be fixed per unit, not headcount.
- **Second order:** exceptions stop being mostly model failures and become mostly **world failures**: a counterparty system is down, a policy is ambiguous, a license or signature is required, or the customer's own data changed. Better models don't fix these. Someone has to absorb them.
- **Third order:** a market forms for absorbing the residual. On the demand side are thousands of AI app companies. On the supply side are BPOs, expert networks, licensed-clinician networks and lab services arms. Prices, quality and latency are opaque, so each AI company builds a private team and pays for peak staffing.
- **Third order:** the scarce input stops being labor and becomes **accountability**: licenses, signatures, guarantees. Whoever prices and absorbs that risk captures value.

## 3. Hunting competitors layer by layer (the obvious products exist)

| Candidate layer | Who already owns it | Verdict |
|---|---|---|
| Human escalation API/marketplace for agents | **Humwork** (YC S26, $500K, MCP plugin across Claude Code, Cursor, Codex, ChatGPT, Lovable; expert in <30s); **Human API** ($65M, Feb 2026); **RentAHuman** (YC S26); round 21 already killed this | Taken |
| AI-plus-human managed service (AI-native BPO) | **Crescendo** ($500M, outcome guarantees); **Invisible Technologies** [unverified current valuation]; TaskUs/Teleperformance/Concentrix pivoting [unverified] | Taken, services margins |
| Agent outcome insurance / warranty | **AIUC** ($40M Series A led by Ribbit, Sep 2026, $55M total; AIUC-1 certifies Cursor, ElevenLabs, Harvey, UiPath, Fin, Lovable; up to $50M cover); **Armilla** ($25M Jan 2026; "AI Performance Warranty" pays out when AI underperforms) | Taken, and well funded |
| Licensed human sign-off network | **Wheel** markets itself as "the clinical action layer for AI" (50-state clinician network); **OpenLoop**. In law, ABA Rule 5.4 fee-sharing limits the play | Taken in health, blocked in law |
| Exception QA / monitoring | Decagon Watchtower, Fin Monitors, Hamming, Coval (round 18 kill) | Taken / platform feature |
| FDE deployment tooling | Sierra/Decagon build in-house; Auctor, Rocketlane (round 4 kill) | Killed |
| Margin and cost-per-outcome tracking | Paid.ai [unverified], Metronome/Orb billing | Feature |
| Labs vertically integrating services | OpenAI Deployment Co (~$10B), Anthropic services firm (~$1.5B) | The biggest threat to everything above |

**One layer deeper, the only unowned shape I can find:** the **clearing layer between demand and supply.** Nobody quotes a firm price for an exception before it is handled, routes it to the cheapest competent resolver across *all* supply (a stronger model, the customer's own staff, a BPO pool, an expert network, a licensed network), guarantees the SLA, and sends a structured fix back to the vendor's agent. Every player above is **one supply source** (Humwork, Crescendo, Wheel) or **one risk wrapper** (AIUC, Armilla). Nobody has priced the exception itself.

---

## 4. Thesis: Exception Clearing — firm-quoted, guaranteed resolution of agent exceptions

*Working name: "Residual". Analogies: OpenRouter for the human residual, plus Signifyd's fixed-fee guarantee model.*

**One-line problem.** Vertical AI companies on outcome or per-task pricing pay for every exception their agents can't finish with a private, peak-staffed human ops team. That cost scales with customers, can't be predicted per contract, and is now the largest variable COGS line left once inference gets cheap.

**Why now.**
- Outcome pricing is spreading (Sierra per resolution, Decagon per-resolution option, HubSpot switching to per resolution per SaaStr), so vendors carry exception risk.
- Inference share of COGS is falling (ICONIQ: margins from 41% to a projected 59%), which leaves the human residual as the cost that doesn't fall.
- Supply now exists and can be called by API (Humwork, Human API, Wheel, BPOs exposing APIs), but it is fragmented and priced opaquely.
- The labs' services push (OpenAI DeployCo, Anthropic) is pushing independent app companies to show "software-like" cost to serve or lose the services story to the labs.

**Exact buyer.** CFO, or COO/VP Operations, at a Series A–C vertical AI company. The budget line is "AI ops / customer operations COGS". The CTO is a co-signer because of the integration.

**Exact ICP.** Vertical-agent companies with 20–300 enterprise customers, priced per task or outcome, in domains where exceptions are mostly **world failures** rather than judgment calls: insurance claims and FNOL intake, freight and logistics exceptions, AP/AR and collections, property-management ops, non-clinical healthcare admin, and voice-agent front doors. They have 10–80 ops headcount growing with customer count, and no Sierra-scale internal tooling team. Rough count: ~1,500–3,000 such companies worldwide by 2027 (estimate, unverified).

**Current workaround.** In-house ops pods per customer cohort (supervisors in Slack or a Zendesk-style queue), FDEs doubling as escalation staff, an offshore BPO contract at fixed seat count, or simply eating SLA credits.

**Why incumbents can't easily own it.**
- Agent platforms (Sierra, Decagon, Intercom) build escalation for *their own* agents and won't clear competitors' exceptions.
- Supply players (Humwork, Crescendo, Wheel, BPOs) are conflicted: each routes to itself, so none can be a neutral price-setter.
- Insurers (AIUC, Armilla) price tail liability annually. They don't operate resolution per event.
- Labs' services arms serve large enterprises directly and compete with app companies rather than supplying them.

**Honest rebuttal:** these are "haven't yet / conflicted" arguments. They are not structural bans, and round 18's taxonomy says that usually isn't enough.

**30-day MVP.**
- One API: `quote(exception)` returns a price and an SLA, then `resolve(exception)` delivers the resolution plus a structured `fix_candidate` (proposed policy, KB or tool change).
- Routing behind it, across three resolver tiers: (1) retry with a stronger model plus a verifier, (2) a contracted pool of 15–30 domain specialists, (3) handback to the customer's own staff in a one-click form.
- One vertical (freight exceptions or insurance FNOL).
- A dashboard showing cost per exception, exception mix and money saved versus in-house cost.

**Pilot design.**
- Two or three design partners route **one exception class** (for example "carrier won't confirm POD" or "missing claim documentation") for 30 days at a fixed per-exception price set at ~70% of their measured in-house cost.
- Success means: ≥80% resolved within SLA, ≥25% unit-cost reduction, and ≥1 accepted `fix_candidate` per week that lowers the vendor's exception rate.
- The partner shares 90 days of exception logs up front so the quote can be priced actuarially.

**Pricing hypothesis.** A firm per-exception fee ($3–40 depending on class), with an SLA credit funded from the spread between quote and actual resolution cost. Optional add-on: a monthly "cost-to-serve cap" (vendor pays a fixed amount per covered outcome, we absorb variance), which is the Signifyd-style guarantee. Target 35–45% contribution margin early, rising as tier-1 (model) resolution share grows.

**Expansion path.**
1. One exception class, then all exception classes for a vendor, then multiple verticals.
2. Firm quotes become **cost-to-serve underwriting**: we price a vendor's outcome contract *before* they sign it, using cross-vendor exception data.
3. Pooled specialist supply becomes a credentialed, licensed resolver network, the accountability layer: signatures, licensed sign-off, liability.
4. Resolution data becomes auto-generated fixes that shrink the exception rate, and we share in the savings.

**Moat.**
- (a) An actuarial dataset of exception cost, latency and quality by class across vendors. Nobody single-vendor has it, and it is what makes firm quotes possible.
- (b) Two-sided liquidity: vendors bring exceptions, resolvers bring capacity. Pooling lets a shared pool staff at the average rather than every vendor staffing at its own peak.
- (c) Being the system of record for cost to serve that a vendor's CFO and lenders rely on.

**Weakness:** (a) only compounds if vendors let their exceptions leave the building.

**Why it could be $10B+.** All of this is an unverified estimate. If AI app revenue reaches ~$150–300B by 2029 and the human residual is 10–20% of it, that is **$15–60B of spend a year**. A further ~$300B of BPO spend is moving to "AI plus human residual". A clearing layer taking 15–25% of routed spend on $10–20B of flow is $2–5B of revenue, which supports a $10B+ valuation, *if* it becomes the default price-setter the way Visa or OpenRouter became defaults. Without the clearing position it is a BPO worth 1–2x revenue.

**Direct competitors and adjacent threats.**
- **Direct-ish:** Humwork, Human API, RentAHuman (supply-side escalation APIs that can add quoting).
- **Hybrid service:** Crescendo, Invisible [unverified], TaskUs/Concentrix AI units [unverified].
- **Risk:** AIUC (Ribbit-backed; adding per-event guarantees is natural for it), Armilla (AI Performance Warranty).
- **Platforms:** Sierra/Decagon/Intercom native escalation; OpenAI and Anthropic services arms.
- **Vertical clearinghouses:** Wheel and OpenLoop in health; payer-call AI firms such as Infinitus [unverified].

**One sentence to the CFO.** "Send us your agent's exceptions and we'll quote a fixed price per exception before we touch it, resolve it within SLA for less than your ops team costs, and send back the fix so the same exception stops recurring."

**Hard kill criteria.**
- In 30 days, design partners won't send exceptions outside their walls (data, customer-contract or learning-loop objections) for at least one exception class: KILL.
- The human residual is under 10% of COGS at 3 of 5 sampled ICP companies (it hides inside FDE/CS lines, or is small): KILL.
- Under 30% of exception volume belongs to classes that recur *across* vendors, so pooling can't work: KILL.
- We can't get within ±20% of actual resolution cost after 90 days of logs, so firm quotes lose money: KILL.
- AIUC, Humwork or Crescendo ships firm per-exception quoting before we have 5 paying vendors: KILL.

## 5. Scores (honest)

| Category | Score | Why |
|---|---|---|
| Pain | 6 | Real, but ICONIQ shows margins *improving*. The human residual is inferred, not measured publicly. |
| Urgency | 5 | CFOs feel it at the next raise, not this quarter. Outcome pricing is still a minority. |
| ROI clarity | 7 | Per-exception cost against in-house cost is easy to measure. |
| Customer accessibility | 6 | Founders of vertical-AI companies are reachable, but they are protective of their exception data. |
| Pilot speed | 6 | Thirty days is possible for one exception class, but supply contracting and system access slow it. |
| Market size | 7 | Large flow if the residual stays 10%+. Uncertain. |
| Expansion | 7 | Clean path from clearing to underwriting to licensed network. |
| Venture potential | 6 | $10B only via the clearing-default position. The default outcome is a BPO multiple. |
| Defensibility | 4 | Cross-vendor data only compounds if vendors export exceptions. Supply is replicable. |
| Why now | 7 | Outcome pricing, falling inference costs and API-callable human supply all converged in 2026. |
| Competition position | 4 | Humwork, Human API ($65M), Crescendo, AIUC ($55M), Armilla ($25M), Wheel, and labs' services arms each own a piece. |
| **Average** | **5.9** | Five categories below 7. |

## 6. Classification: **KILL as A. Weak B at best (~10% odds).**

The B argument: H1's real unknown, the share of COGS that is human residual at Series A–C vertical-AI companies and how much of it recurs across vendors, is *structurally* private. No company publishes it. If it were 25%+ of COGS and 40%+ cross-vendor, the clearing layer would be unowned infrastructure with a real path to $10B. The 14-day test is a **data test, not interviews**: get 90-day exception logs and COGS splits from 3 vertical-AI companies under NDA, price one exception class, and see whether any will prepay a fixed per-exception rate. Pass means 2 prepaid pilots of $15K+ and measured residual ≥20% of COGS.

## 7. Which version I would lead, and why

I would **not** lead the escalation marketplace (Humwork exists and it's a commodity), the insurance wrapper (AIUC/Ribbit and Armilla have it), or an AI-native BPO (services multiple, Crescendo, the labs). The only version I would lead is **firm-quoted cost-to-serve underwriting**: the company that can tell a vertical-AI CFO, *before signing a customer*, "this contract will cost $X per outcome to serve, and we'll take the variance". That is the pricing layer for outcome-based AI. It turns exception data into the asset, the way FICO turned repayment data into one. That's why it could be a $10B company rather than a feature: platforms see only their own exceptions, while the price-setter sees everyone's.

**What would make me lead the round:**
1. Five ICP companies show the human residual is ≥20% of COGS *and* rising as a share while inference falls.
2. A design partner routes a full exception class out of the building in under 30 days, and renews.
3. Quotes land within ±15% of actual cost after 90 days, and at least one vendor uses our quote to price a new customer contract. That is the moment it becomes infrastructure.
4. A founding team with combined BPO-ops and actuarial/insurance experience, plus 2–3 vertical-AI founders as committed design partners.

**What stops me:**
1. **Exceptions are the learning loop.** The best AI app companies treat their exceptions as their moat and training data. The companies that would outsource them are the weaker ones, which means adverse selection on the demand side.
2. **Pooling may be an illusion.** Exceptions require customer-system access and tenant-specific policy, so cross-vendor reuse may be under 30%.
3. **The trend runs against the pain.** Public margins are rising. If inference and better agents shrink exception rates faster than customers grow, the residual flattens before we scale.
4. **Well-funded neighbours sit one feature away.** AIUC can add per-event pricing, Humwork can add quotes, Crescendo already sells outcome guarantees, and the labs' services arms can absorb the whole category for their own customers.
5. **The services-multiple trap.** Unless tier-1 (model) resolution passes ~60% of volume within 18 months, this is a BPO with good software, valued at 1–2x revenue.

**Partner verdict:** pass today. I'd write a small check only if the 14-day data test shows the residual is ≥20% of COGS and two prepaid pilots. I wouldn't lead without the quote-accuracy proof.

---
### Sources (from search results; third-party estimates noted above)
- ICONIQ *2026 State of AI*: iconiq.com/growth/reports/state-of-ai-2026; saastr.com summaries ("the builders economy 10 metrics…", "iconiqs latest state of ai report…", "the execution era of ai…")
- Sierra pricing: buildmvpfast.com/blog/sierra-per-resolution-economics-vertical-ai-agents-2026; fin.ai/learn/sierra-ai-pricing; saastr.com/hubspot-switching-ai-pricing-from-per-use-to-per-resolution
- Decagon pricing: featurebase.app/blog/decagon-pricing; fin.ai/learn/decagon-ai-pricing; sacra.com/c/decagon
- Harvey: cryptobriefing.com/harvey-500m-funding-16b-valuation-lightspeed; tech-insider.org/harvey-ai-200m-arr-manifold-odds-2026
- Crescendo: sacra.com/c/crescendo; crescendo.ai news; bnnbloomberg.ca (Oct 2024)
- Humwork: ycombinator.com/companies/humwork; Human API: dealroom.co/companies/human-api; RentAHuman: ycombinator.com/companies/rentahuman
- AIUC: runtimewire.com/article/aiuc-raises-40m-ai-agent-certification-insurance; dealroom.co news 150943
- Armilla: armilla.ai (Armilla Guaranteed); techcrunch.com/2024/02/15/armilla-wants-to-give-companies-a-warranty-for-ai
- Wheel: wheel.com/companies/ai-health; OpenLoop: openloophealth.com
- [unverified, from memory, not searched]: Invisible Technologies valuation, Paid.ai, TaskUs/Concentrix AI units, Infinitus
