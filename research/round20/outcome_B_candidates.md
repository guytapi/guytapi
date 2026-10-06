# Round 20: Re-evaluating "pre-demand" kills under Outcome B

**Date:** 2026-10-06. **Method:** 35 web searches (WebSearch only; WebFetch and Reddit blocked). Most facts come from search-result summaries, not primary pages. Labels: **[summary-only]** = read only in a search summary; **[unverified]** = not confirmed from a primary source; **[estimate]** = my own arithmetic. Every URL below appeared in a search result. None are invented.

**Outcome B bar (founder):**
1. Genuinely unresolved: no direct vendor.
2. Massive if true ($10B+ plausible), with a structural reason incumbents won't own it.
3. Some early behavioral evidence exists.
4. A precise 14-day test exists that yields money, data access or signed pilots, with thresholds.

---

## TL;DR

- **Four of the five original candidates fail B on criterion 1 or 2.** In each case a vendor or standard showed up between Apr and Sep 2026:
  - **(a) Agent credit bureau.** Experian launched an Agent Registry with a dynamic per-agent trust score (Apr 30, 2026). Visa, Mastercard and Ant began a KYA framework with "continuous transaction monitoring" and "shared certification" (Sep 10, 2026). There are also crypto-native scorers: AgentScore, Credifold, ERC-8004, SwarmScore, ATEP.
  - **(c) Supplier bid agents.** Suppliers already build their own agents (Keelvar: 1,420+ machine-to-machine events/month). Freight is crowded (Transfix RFP automation May 2026, Vooma, Greenscreens, Pallet). The antitrust problem (AB 325) is unchanged.
  - **(d) Machine-customer front door.** Still no published agent-originated B2B order share. Platforms keep absorbing the plumbing.
  - **(e) Transferable AI capacity.** Model-API commitments are still non-transferable. OpenAI Guaranteed Capacity (May 19, 2026) is "use-it-or-lose-it". The raw-GPU resale market is crowded: SF Compute, Compute Exchange, Fluence auctions (Aug 2026), Ornn.
- **(b) Binding agreements between agents** is the only candidate with live behavior, a fresh standard and no product vendor:
  - **Live behavior:** Keelvar's 1,420 M2M negotiations/month; Pactum's 87-second autonomous signings; Anthropic Project Deal (186 deals).
  - **Fresh standard:** AAA + Integra Ledger **Legal Context Protocol**, June 2026, backed by Google, IBM, UiPath and Wayfair.
  - **No product vendor yet.** But DocuSign's Deputy GC published the exact thesis on Aug 27, 2026, and Keelvar describes a shared hash-chained negotiation ledger. The window is open but closing.
- **Best B candidate (conditional):** narrow (b) to the side that has a structural reason to need a neutral record, the **supplier**. Name: "Counter-signature for machine-to-machine deals." It is a supplier-owned authority, terms and outcome record for every commitment its agents, or a buyer's agent, make across Keelvar, Pactum, Fairmarkit, Coupa and Ariba. Agent reputation (a) is the expansion path.
- **Confidence: low.** I estimate a 15–20% chance it passes the 14-day test. If it fails, classify it KILL and stop reopening the agent-commerce family.

---

## Candidate scorecard (B criteria)

| # | Candidate | C1 Unresolved | C2 Massive + structural | C3 Early behavior | C4 14-day test | B verdict |
|---|---|---|---|---|---|---|
| a | Agent reputation / credit bureau | **FAIL** | **FAIL** | PASS (weak) | PASS | **FAIL** |
| b | Binding agreements between agents | PASS (narrowly) | PASS (conditional) | PASS | PASS | **Conditional PASS** |
| c | Supplier bid agents (freight/packaging/MRO) | **FAIL** | **FAIL** | PASS (strongest) | PASS | **FAIL** |
| d | Machine-customer front door (B2B) | **FAIL** | FAIL | **FAIL** | PASS | **FAIL** |
| e | Transferable AI capacity market | **FAIL** | FAIL | FAIL | n/a | **FAIL** |
| f (own) | B2B agent authority verification ("is this agent allowed to commit Acme for $X?") | PASS (partly) | FAIL alone | PASS (weak) | PASS | Fold into b |
| g (own) | Bid integrity: prompt injection in supplier documents aimed at buyer sourcing agents | FAIL | FAIL | weak | PASS | **FAIL** |
| h (own) | Instant trade credit for agent-originated buyers | FAIL | FAIL | weak | PASS | **FAIL** |

**Why each criterion failed:**
- **(a)**
  - C1: Experian's Agent Registry with dynamic trust score (Apr 2026). Visa, Mastercard and Ant's KYA framework includes continuous monitoring and certification (Sep 2026). AgentScore, Credifold, Alien ($7.1M) and ERC-8004 also exist.
  - C2: the card networks and bureaus own the consumer flow. In B2B no one would buy it before deals exist.
- **(c)**
  - C1: suppliers build their own bid agents. Freight RFP tools already exist (Transfix, Vooma, Greenscreens, Pallet).
  - C2: the buyer platform hosts the mechanism, and AB 325 blocks the shared-data moat.
- **(d)**
  - C1: Salesforce, commercetools, TradeCentric UPOP and MCP servers cover it.
  - C3: still no agent-order share disclosed. Deloitte says fewer than a quarter of suppliers use agentic AI.
- **(e)**
  - C1: SF Compute, Compute Exchange, Fluence and Ornn cover GPUs.
  - Model-API commitments cannot be transferred, so there is no market to build.
- **(f)**
  - C1: GLEIF vLEI role credentials and the IETF AGTP-LEI draft are starting to cover it.
  - C2: an identity feature on its own. It is useful as part of (b).
- **(g)**
  - C1: F5 sells AI guardrails for sourcing. It is a feature of AI-security vendors and of Keelvar/Coupa themselves.
- **(h)**
  - C1: B2B BNPL already covers it (Apruve, TreviPay and others).

---

## (a) Reputation / track-record network for agents ("credit bureau for agents")

**Competitors found (2026):**
- **Experian Agent Trust** (announced Apr 30, 2026).
  - Includes Human-to-Agent Binding, a real-time Agent Trust Token, and an **Agent Registry that keeps a dynamic trust score for each registered agent, based on behavioral signals**.
  - Ecosystem partners: Visa, Cloudflare, Skyfire.
  - Sources: https://www.experianplc.com/newsroom/press-releases/2026/experian-announces-agent-trust-to-power-trusted-ai-driven-commer ; https://www.businesswire.com/news/home/20260430719198/en/
- **Ant International + Visa + Mastercard KYA interoperability framework** (Sep 10, 2026).
  - Covers operator traceability, **shared certification requirements** and **continuous transaction monitoring** using identity and transaction signals.
  - Ant says it will add "capabilities, behavior, execution performance and risk data".
  - Runs through Singapore's BuildFin.ai.
  - Sources: https://www.pymnts.com/cybersecurity/2026/visa-mastercard-team-with-ant-know-your-agent-framework/ ; https://technode.com/2026/09/10/ant-international-visa-and-mastercard-develop-know-your-agent-framework-for-ai-payments/
- **Mastercard Verifiable Intent** (Mar 2026). Links identity, instruction and outcome into one tamper-resistant record [summary-only].
- **Startups and standards:**
  - AgentScore: on-chain grades, `/v1/reputation` API (https://agentcommunity.org/m/agentscore).
  - Credifold: "Experian for agents", pre-team (https://www.indiehackers.com/post/looking-for-technical-co-founder-building-ai-agent-attestation-network-credifold-b4bdc0267b).
  - Alien: $7.1M pre-seed, Agent IDs anchored to humans (https://www.vouched.id/learn/alien-raises-7.1m-to-build-identity-infrastructure-for-humans-and-ai-agents).
  - ReputAgent.
  - SwarmScore, an IETF draft (https://datatracker.ietf.org/doc/html/draft-stone-swarmscore-v1).
  - ATEP passport, an IETF draft (https://www.ietf.org/archive/id/draft-stone-atep-02.xml).
  - ERC-8004 reputation registry.
  - cheqd + Vouched: reputation packaged as verifiable credentials.

**Early evidence:** The consumer-payments version has real buyers (issuers, merchants). The **cross-company B2B outcome history** version has no behavior to score yet. B2B M2M deals are a few thousand per month on one platform.

**Verdict: FAIL B.**
- The consumer slot belongs to Experian and the card networks. That is the textbook failure "F1 + analog slot filled by incumbent".
- The B2B slot has no data to score until (b)'s records exist.
- The founder's Vara consortium edge is real, but this would mean competing with Experian on its home turf.
- **Keep it as the expansion layer of (b):** outcome history is a by-product of holding the commitment records.

**14-day test, if run anyway:** ask 3 agentic-commerce platforms (procurement or marketplace) for 90 days of agent-counterparty dispute and default data, and for a $10K paid scoring pilot. Kill if fewer than 2 share data.

---

## (b) Binding agreements between agents ("who signs when agents make deals?")

**Early behavioral evidence (strongest in this round):**
- **Keelvar** (Jul 2026 white paper, CEO Alan Holland):
  - 90% of events are agent-operated.
  - **1,400–1,420+ machine-to-machine negotiations/month**, a category that did not exist before Dec 2025.
  - Median cycle under 2 hours.
  - It describes the emerging pattern as "structured offers and counters between authorized agents, recorded on a ledger both sides can verify, with hash-chained entries" [summary-only].
  - Sources: https://www.keelvar.com/documents/the-two-sided-agentic-market-in-enterprise-procurement ; https://info.keelvar.com/hubfs/Brochures%20Datasheets%20Case%20Studies%20eBooks/Whitepapers%2c%20eBooks%20and%20Reports/The%20Two-sided%20Agentic%20Market%20in%20Enterprise%20Procurement.pdf
- **Pactum:**
  - Negotiation plus signing in 87 seconds.
  - Up to 10,000 parallel negotiations; 50+ enterprises; spend handled up 489%.
  - "The other party is still 100% human" [summary-only].
  - Source: https://pactum.com/blog/can-ai-negotiate
- **Anthropic Project Deal** (published Apr 24, 2026):
  - 69 employees, 186 deals, about $4K.
  - Stronger models got better deals and "the losers don't even notice". This is an argument that weaker parties need an independent record.
  - Sources: https://the-decoder.com/anthropic-says-stronger-ai-models-cut-better-deals-and-the-losers-dont-even-notice/ ; https://www.techwyse.com/news/ai-search/anthropic-project-deal-ai-agent-marketplace-experiment
- **Legal Context Protocol (LCP)** (Jun 2026):
  - From the AAA and Integra Ledger, Apache 2.0.
  - Founding contributors: Google, IBM, Circle, UiPath, Wayfair, Crossmint, Trinsic and others.
  - Covers which terms applied, which law governs and what recourse exists.
  - The AAA says "most agent-to-agent transactions currently lack verifiable terms".
  - Sources: https://www.adr.org/news-and-insights/introducing-the-legal-context-protocol/ ; https://www.trinsic.id/blog/aaa-and-industry-leaders-launch-legal-protocol-for-agentic-commerce ; https://www.mlex.com/pulse/legal-tech/articles/2493375/aaa-rolls-out-protocol-for-ai-agent-transactions
- **Internet Court** (Jul 10, 2026):
  - GenLayer-led, 27 crypto backers.
  - AI-validator dispute resolution at about $1 per case.
  - Source: https://cryptobriefing.com/genlayer-okx-metamask-back-internet-court-a-new-ai-agent-dispute-standard/
- **Icertis survey** (May 2026):
  - 47% of in-house legal teams would not detect an unauthorized or incorrect AI action until after it happened.
  - Only 23% have a documented agentic AI policy.
  - Source: https://www.lawnext.com/2026/05/survey-legal-teams-lack-visibility-into-ai-agents-actions-icertis-research-finds.html
- **GLEIF vLEI role credentials for agents**, and the IETF AGTP-LEI draft (Jun 2026). Sources: https://www.gleif.org/en/newsroom/blog/why-ai-agents-need-verifiable-organizational-identity ; https://datatracker.ietf.org/doc/html/draft-hood-agtp-lei-00

**Competitors and threats:**
- **DocuSign.**
  - Its Deputy GC, Ken Priore, wrote "Accountability by Design in Agentic Contract Management" (Artificial Lawyer, Aug 27, 2026): "is there a record of what it did and on whose authority it acted?" The essay positions eSignature-style sealing for agent actions.
  - DocuSign IAM plus MCP plus contract agents shipped May 2026.
  - **This is the biggest threat.**
  - Sources: https://artificiallawyer.com/2026/08/27/accountability-by-design-in-agentic-contract-management ; https://www.docusign.com/company/news-center/docusign-announces-agentic-contract-workflows-for-inhouse-legal-teams
- **Keelvar, Pactum and the other buyer platforms.** They can build a native negotiation ledger; Keelvar already describes one.
- **eSign.AI VeriAgent.AI** (WAIC Jul 2026): JIT agent credentials, agent signing, tamper-proof logs. Mostly a China/APAC play [summary-only]. Source: https://www.aap.com.au/aapreleases/cision20260723ae10847/
- **Integra Ledger:** commercial steward of LCP; product scope unknown [unverified].
- **Google AP2 mandates:** consumer and payments focused, contributed to FIDO in Apr 2026.
- **Mastercard Verifiable Intent.**
- **Icertis and Ironclad:** CLM incumbents.

**Structural reason incumbents might not own it:**
1. **The record-keeper is a party to the deal.**
   - Pactum, Keelvar and Fairmarkit are paid by the buyer, and their ledger is the buyer's ledger.
   - A supplier facing 5 buyer platforms cannot use 5 buyer-controlled records as its own system of record for what its agents committed.
   - Equally, a buyer's auditor needs evidence that the *counterparty's* agent had authority.
2. **Multi-party by construction.** Authority proofs come from each company's own delegation chain (officer → role → agent). No single platform holds both sides.
3. **DocuSign's business is per-envelope signatures by humans.** Agent M2M deals are thousands of micro-commitments per month inside a sourcing protocol, which does not fit envelope pricing. This argument is weak: DocuSign could reprice.

**C2 sizing [estimate]:**
- Gartner's "$15T B2B agent-intermediated by 2028" is vendor-recycled.
- Even 1% of US+EU B2B transactions at 2–5 bps per committed dollar is about $1–4B/yr in fees.
- The $10B outcome requires that agent-made commitments become a legal-evidence category, like the eSignature category DocuSign built (about $3B revenue). Plausible but unproven.

**Verdict: conditional PASS.** Pursue the supplier-side wedge below.

---

## (c) Supplier-side bid agents for formula-priced categories

**Evidence:**
- Keelvar reports supplier agents in 1,420+ events/month, concentrated in "high request frequency, ad-hoc demand and formulaic pricing" categories (freight, packaging, MRO).
- Search summaries say **suppliers build their own agents** [summary-only]. That is the internal-workaround signal B asks for.

**Competitors:**
- **Freight:**
  - Transfix RFP automation for brokers, May 2026 (https://www.businesswire.com/news/home/20260519635199/en/Transfix-Launches-RFP-Automation-Software-for-Freight-Brokers-Turning-Thousand-Lane-Bids-into-a-Strategic-Pricing-Plan).
  - Vooma: $16.6M, quote agents, Greenscreens partnership (https://yespress.io/vooma).
  - Pallet quoting (https://www.pallet.com/use-cases/quoting).
  - Shippers' counterpart: project44's procurement agent (https://www.ajot.com/news/project44-launches-ai-freight-procurement-agent).
- **Packaging/MRO:** pricing incumbents (Pricefx, Zilliant, Vendavo) from round 4. No dedicated startup found.

**Verdict: FAIL B.**
- It is resolved in freight, the biggest M2M category.
- In packaging/MRO the value per supplier is small and the events are tail-spend.
- Keelvar controls the mechanism.
- AB 325 bars the cross-supplier data moat.
- This is the round-4 kill reconfirmed. **Its useful residue:** the suppliers running those 1,420 events/month are the best discovery pool for (b).

---

## (d) Machine-customer front door (B2B), 2026 update

**Data found (Jul–Oct 2026):**
- No distributor discloses an agent-originated order share.
- Amazon Business is at $60B annualized, with agentic discovery, but no agent-order share is broken out (https://www.marketscale.com/industries/software-and-technology/amazon-business-hits-60-billion-in-annualized-gross-sales-as-agentic-ai-reshapes-b2b-procurement).
- Deloitte: fewer than a quarter of B2B suppliers use agentic AI (https://www.deloitte.com/us/en/what-we-do/capabilities/applied-artificial-intelligence/articles/b2b-agentic-commerce.html).
- UCP still has no B2B primitives (POs, net terms, RFQ) (https://ucpchecker.com/verticals/b2b).
- Digital Commerce 360: "agentic commerce faces reality check in B2B" (Mar 2026) (https://www.digitalcommerce360.com/2026/03/10/agentic-commerce-faces-reality-check-in-b2b-ecommerce/).

**Verdict: FAIL B** on C1 and C3. Same incumbents as Phase 5 (Salesforce Buyer Agent, TradeCentric UPOP, platform MCP servers), and still no behavior to point to.

---

## (e) Transferable AI capacity market

**Findings:**
- **OpenAI Guaranteed Capacity** (May 19, 2026): 1–3 year commitments from under 100M to over 1B TPM, drawable across OpenAI products, described as "use-it-or-lose-it". No transfer or resale terms were found.
  - Sources: https://www.datacenterdynamics.com/en/news/openai-launches-guaranteed-capacity-offering-giving-customers-ability-to-secure-long-term-access-to-compute/ ; https://www.beri.net/article/openai-30m-capacity-trap-3-year-lockin-pays
- Anthropic moved Claude Enterprise to prepaid token commitments (Apr 2026) [summary-only].
- Google Provisioned Throughput is model-locked.
- **No provider allows transfer.**
- Raw GPU resale is crowded:
  - SF Compute: reserve, then resell unused hours.
  - Compute Exchange: used-GPU marketplace, Jul 2026 (https://blockspace.media/insight/compute-exchange-launches-used-gpu-marketplace/).
  - Fluence GPU Cluster Auctions, Aug 2026.
  - Ornn futures.

**Verdict: FAIL B.** The instrument needed for a market does not exist. Re-open only if a frontier lab publishes assignment terms for commitments.

---

## Own additions

- **f. B2B agent authority verification.**
  - Example: a supplier gets a PO or a term change from "Acme's procurement agent" and needs to know whether that agent may bind Acme for this amount.
  - Real fraud surface: agent impersonation of procurement, rogue agents acting "within technically authorized parameters" (https://www.sunrate.com/blog/thoughtleadership/invoice-manipulation-vendor-impersonation-rogue-agent-spend-the-new-b2b-fraud-surface/).
  - Standards forming: GLEIF vLEI role credentials.
  - Not a company on its own, but it is the **authority half of (b)** and fits Vara's fraud background. Folded in.
- **g. Bid integrity (prompt injection in supplier bids aimed at buyer agents).**
  - F5 already markets AI guardrails for sourcing that "detect and prevent prompt injections designed to manipulate supplier recommendations" (https://www.f5.com/company/blog/ai-security-for-sourcing-procurement).
  - The sourcing platform owns the fix. FAIL (F1/F5).
- **h. Instant trade credit for agent-originated buyers.** It is B2B BNPL with a new label (Apruve, TreviPay). FAIL.

---

# FINALIST (Outcome B, conditional): "Counter-signature for machine-to-machine deals"

### One-line problem
When a supplier's bid agent and a buyer's sourcing agent close a deal in 2 hours with no human signing, neither company has an independent, auditor-grade record of **who had authority, what terms bound them, and what was delivered**. The only record sits on the buyer's platform.

### Why this problem exists now
- Machine-to-machine negotiation did not exist before **Dec 2025**. By **Jul 2026** it ran 1,420+ events/month on Keelvar alone, with 90% of Keelvar events agent-operated and median cycles under 2 hours.
- Pactum closes and signs in 87 seconds.
- The legal layer was only specified in **Jun 2026** (LCP). The AAA states that most agent-to-agent transactions lack verifiable terms.
- Agent authority credentials are still IETF and GLEIF drafts (Jun 2026).
- In-house legal cannot see agent actions in time: 47% would detect only after the fact (Icertis, May 2026).
- DocuSign's Deputy GC publicly named the gap on Aug 27, 2026. That confirms the gap, and it also starts the clock.

### Exact buyer
- **Economic buyer:** CFO or Corporate Controller at the supplier. They own revenue recognition, commitments and audit evidence for agent-made sales commitments.
- **Co-signer:** General Counsel / Head of Commercial Contracts.
- **Second side, later:** CPO plus Internal Audit at enterprise buyers running Keelvar, Pactum or Fairmarkit. They need proof that the counterparty's agent had authority before awards are treated as binding.

### Exact ICP
- Suppliers with $200M–$5B revenue in freight brokerage/carriage, corrugated and flexible packaging, and MRO/industrial distribution.
- They sell into 3+ enterprise customers that run agentic sourcing (Keelvar, Pactum, Fairmarkit, Coupa, Ariba Joule).
- They already run, or are piloting, an automated bid or quote agent. These are the companies behind Keelvar's 1,420 M2M events/month.
- **[estimate]** a few hundred such suppliers today; 3,000–8,000 if M2M spreads beyond the formula-priced categories.

### Current workaround
- Each buyer platform's own event log and award notice.
- Email confirmations.
- The supplier's bid agent's internal logs, which vary by vendor and are not tamper-evident.
- Manual reconciliation of awards to ERP orders.
- Delegation of authority sits in a PDF policy that the agent never references.
- Disputes (wrong lane, wrong price, unit-of-measure errors) are settled by phone and credit memo.

### Why incumbents cannot easily own it
1. **Conflict:** the buyer platform is paid by the buyer. A record kept by one party's vendor is weak evidence for the other party.
2. **Multi-party:** each side's authority chain comes from its own officers, so no single platform holds both.
3. **Multi-platform:** a supplier faces Keelvar, Pactum, Fairmarkit, Coupa and Ariba at once and needs one ledger across all of them.
4. **DocuSign's model fits human envelopes, not thousands of micro-commitments per month inside a sourcing protocol.** This is the weakest leg. DocuSign is the most likely to close the gap, by building it or buying it.

### 30-day MVP
- An SDK and a mail/portal sidecar that wraps every outbound commitment from the supplier's bid agent, or inbound award, into an **LCP-compatible signed commitment record**. Each record contains:
  1. The agent identity and authority credential (officer → role → agent → limits; vLEI-compatible where available).
  2. A terms hash plus the governing terms.
  3. Counterparty identity and award evidence.
  4. A hash-chained, timestamped seal.
- An authority-policy engine that blocks or escalates any commitment outside the delegated limits.
- A reconciliation view: commitments vs. ERP orders vs. deliveries and invoices, with an exceptions list.
- A one-click evidence pack for an auditor or a dispute.

### Pilot design (60 days)
- **Partners:** 2 suppliers (one freight broker, one packaging or MRO) with active agent bidding, plus 1 enterprise buyer that runs agentic sourcing.
- **Back-test:** 90 days of historical agent events to find commitments outside authority, unrecorded terms, and award/ERP/invoice mismatches.
- **Live run:** wrap all new commitments for 30 days.
- **Success:**
  - At least 1% of agent commitments by value show an authority or terms exception.
  - At least one dispute or credit memo is resolved from the record.
  - The external auditor or GC accepts the evidence pack as a control.
  - The buyer agrees to counter-sign records.

### Pricing hypothesis
- Platform fee of $30–60K/yr per supplier entity.
- Plus $0.50–$2 per sealed commitment, or 1–3 bps of committed value above a threshold.
- Buyers counter-sign free at first. Charge buyers' audit and procurement teams later ($50–150K/yr).

### Expansion path
1. Supplier commitment ledger (freight, packaging, MRO).
2. Buyer-side counter-signature, which creates network effects: each record is two-party.
3. Authority registry: a company's agents and their limits, verifiable by any counterparty.
4. **Outcome history across counterparties.** This is the B2B agent reputation layer from (a), built from data the company already holds.
5. Dispute resolution and recourse (LCP / AAA-aligned) and insurance underwriting data.

### Moat
- A two-sided record network: every sealed deal adds both parties, and counter-signature pulls in the other side.
- An authority registry that counterparties query.
- Longitudinal outcome data (delivered vs. committed) that no single platform holds.
- Integration into each buyer platform's protocol.
- **Antitrust note:** records hold commitment facts and authority, not price recommendations, which keeps them outside AB 325's "common pricing algorithm" definition. Outside counsel must confirm.

### Why it could become a $10B+ company
- If even a small share of the projected agent-intermediated B2B flow ($15T forecast, vendor-recycled) needs an evidence-grade commitment record, this becomes **the DocuSign plus Experian of machine commerce**: signature, authority and track record in one network.
- Per-commitment fees grow with M2M volume, not with seats.
- Reputation and dispute data compound.

### Direct competitors and adjacent threats
- **DocuSign** (agentic IAM; the Deputy GC essay on agent accountability).
- **Keelvar** and other buyer platforms (native hash-chained negotiation ledger).
- **Pactum.**
- **Integra Ledger / LCP** (protocol steward, could productize).
- **eSign.AI VeriAgent** (APAC).
- **Experian Agent Trust** and **Visa/Mastercard/Ant KYA** (they could extend from consumer to B2B).
- **GLEIF vLEI ecosystem vendors.**
- **Icertis / Ironclad** (CLM).
- **Internet Court** (crypto dispute resolution).

### The one sentence to send a CFO
"Your bid agents and your customers' sourcing agents are now closing deals with no human signature. We give you an auditor-grade record of who had authority, what terms bound you, and what was delivered, across Keelvar, Pactum, Fairmarkit and Coupa, so an agent-made commitment never becomes an unprovable dispute or an audit finding."

### 5 customer discovery questions
1. How many commitments did your bid or quote agents make last quarter, through which buyer platforms, and for what total value? Can you export them today?
2. When an agent-made award was disputed (price, lane, quantity, terms), what record did you rely on, whose system was it in, and what did the dispute cost?
3. Does your delegation-of-authority policy cover agents? Has your auditor or GC asked how agent commitments are authorized and evidenced?
4. Would you accept your largest customer's platform log as the only record of what your company agreed to? If not, what do you do today?
5. If your customer's sourcing platform asked you to prove your agent's authority to bind you, how would you do it?

### Hard kill criteria
- Fewer than 5 of 15 target suppliers can name agent-made commitments in the last 90 days. That means M2M is still too rare outside Keelvar.
- Back-test on 2 suppliers finds fewer than 0.5% of commitments (by value) with authority, terms or reconciliation exceptions, and no disputes. That means no pain.
- Zero GCs, controllers or auditors say platform logs are insufficient.
- Keelvar or Pactum confirms a native two-party counter-signed ledger that suppliers can export and that auditors accept.
- DocuSign announces agent-commitment sealing for sourcing protocols before the pilots sign.
- Outside counsel finds that the shared record creates AB 325 or hub-and-spoke exposure that can't be designed around.

### Scores (1–10). Outcome B: these reflect present evidence, not the potential the test is meant to reveal
| Dimension | Score | Note |
|---|---|---|
| Pain | 4 | No disputes found in public. Pain is inferred from structure. |
| Urgency | 4 | First audit questions are likely in FY2026 year-end, but not confirmed. |
| ROI clarity | 5 | Dispute and credit-memo savings plus audit control. Unproven. |
| Customer accessibility | 6 | Suppliers in Keelvar M2M categories are identifiable. CFO/GC are reachable. |
| Pilot speed | 7 | Back-test on exported event logs within days. |
| Market size | 7 | Tied to M2M volume. $10B only if machine commerce scales. |
| Expansion | 9 | Ledger → authority registry → reputation → disputes and insurance. |
| Venture potential | 8 | A "DocuSign + Experian for machine commerce" story VCs will take. |
| Defensibility | 6 | Two-sided network if it wins. DocuSign and the platforms can contest it. |
| Why now | 9 | M2M born Dec 2025; LCP Jun 2026; vLEI drafts Jun 2026. |
| Competition position | 6 | No product vendor yet, but DocuSign is circling and Keelvar has a native ledger. |
| **Average** | **6.5** | Does not meet A. Qualifies only as B, contingent on the test. |

---

## The 14-day test (precise)

**Goal:** find out whether agent-made B2B commitments already create record or authority pain worth paying for.

| Day | Action | Output |
|---|---|---|
| 1–2 | Build a target list of 40 suppliers in freight brokerage, packaging and MRO that sell to known Keelvar, Pactum or Fairmarkit customers. Ask Keelvar and Pactum for one call each, framed as "independent counter-signature for your M2M events", to learn whether they would welcome or block it. | List; 2 platform calls booked |
| 2–7 | 15 CFO/GC/pricing-lead calls (founder network plus Vara trust/fraud contacts in logistics and industrials). Ask the 5 questions above and request a **data export of 90 days of agent-made commitments under NDA**. | Interview notes; data-access requests |
| 3–8 | 5 calls with audit partners or internal-audit heads: "Are agent-made sales or procurement commitments in scope for FY2026 year-end? What evidence will you accept?" | Auditor stance |
| 6–12 | Back-test whatever exports arrive: authority exceptions, terms mismatches, award/ERP/invoice breaks, disputes. | Exception rate, $ at stake |
| 10–14 | Present findings. Ask for a **paid 60-day pilot ($15–25K)** or an LOI, plus one buyer willing to counter-sign. | Signed pilots or LOIs |

**Pass thresholds (all of them):**
- At least 5 of 15 suppliers confirm agent-made commitments in the last 90 days, and at least 3 confirm a dispute or reconciliation break tied to one.
- At least 2 suppliers hand over event or commitment data.
- The back-test finds at least 1% of committed value with exceptions, or at least $50K of disputed or credit-memo value.
- At least 2 paid pilots or LOIs at $15K or more, plus 1 buyer willing to counter-sign.
- At least 1 of 5 auditors says agent commitments are in scope and platform logs alone are insufficient.

**"Massive" signal (go hard):**
- A buyer platform (Keelvar or Pactum) says it would *require* independent counter-signature for supplier agents, or would integrate it.
- Or suppliers report agent-commitment volume growing more than 3x quarter on quarter.

**Fail (KILL, and close the agent-commerce family):** fewer than 2 data handovers, or zero paid pilots or LOIs, or the platforms confirm they already provide two-party records that auditors accept.

---

## Sources (all appeared in search results this round)
- Keelvar: https://www.keelvar.com/documents/the-two-sided-agentic-market-in-enterprise-procurement ; https://info.keelvar.com/hubfs/Brochures%20Datasheets%20Case%20Studies%20eBooks/Whitepapers%2c%20eBooks%20and%20Reports/The%20Two-sided%20Agentic%20Market%20in%20Enterprise%20Procurement.pdf ; https://www.keelvar.com/knowledge-hub/autonomous-negotiation-agents-the-end-of-the-chatbot-era-in-sourcing
- Pactum: https://pactum.com/blog/can-ai-negotiate ; https://procurementmag.com/news/pactum-transforms-procurement-with-its-agentic-ai-platform
- Project Deal: https://the-decoder.com/anthropic-says-stronger-ai-models-cut-better-deals-and-the-losers-dont-even-notice/ ; https://www.techwyse.com/news/ai-search/anthropic-project-deal-ai-agent-marketplace-experiment
- LCP: https://www.adr.org/news-and-insights/introducing-the-legal-context-protocol/ ; https://www.trinsic.id/blog/aaa-and-industry-leaders-launch-legal-protocol-for-agentic-commerce ; https://thepaypers.com/fraud-and-fincrime/news/aaa-and-integra-ledger-launch-agentic-commerce-legal-protocol ; https://cointelegraph.com/news/ai-is-getting-a-legal-layer-as-agentic-commerce-accelerates
- Internet Court: https://cryptobriefing.com/genlayer-okx-metamask-back-internet-court-a-new-ai-agent-dispute-standard/ ; https://en.cryptonomist.ch/2026/07/10/ai-agent-dispute-resolution/
- DocuSign: https://artificiallawyer.com/2026/08/27/accountability-by-design-in-agentic-contract-management ; https://www.docusign.com/company/news-center/docusign-announces-agentic-contract-workflows-for-inhouse-legal-teams
- eSign.AI: https://www.aap.com.au/aapreleases/cision20260723ae10847/
- Icertis: https://www.lawnext.com/2026/05/survey-legal-teams-lack-visibility-into-ai-agents-actions-icertis-research-finds.html
- GLEIF / AGTP-LEI: https://www.gleif.org/en/newsroom/blog/why-ai-agents-need-verifiable-organizational-identity ; https://datatracker.ietf.org/doc/html/draft-hood-agtp-lei-00 ; https://www.gleif.org/organizational-identity/research-publications/2026-08-13_agentic_ai_in_payments_v1.0-1.pdf
- Experian: https://www.experianplc.com/newsroom/press-releases/2026/experian-announces-agent-trust-to-power-trusted-ai-driven-commer ; https://www.businesswire.com/news/home/20260430719198/en/
- Visa/Mastercard/Ant KYA: https://www.pymnts.com/cybersecurity/2026/visa-mastercard-team-with-ant-know-your-agent-framework/ ; https://technode.com/2026/09/10/ant-international-visa-and-mastercard-develop-know-your-agent-framework-for-ai-payments/
- Reputation startups and standards: https://agentcommunity.org/m/agentscore ; https://www.indiehackers.com/post/looking-for-technical-co-founder-building-ai-agent-attestation-network-credifold-b4bdc0267b ; https://www.vouched.id/learn/alien-raises-7.1m-to-build-identity-infrastructure-for-humans-and-ai-agents ; https://datatracker.ietf.org/doc/html/draft-stone-swarmscore-v1 ; https://www.ietf.org/archive/id/draft-stone-atep-02.xml ; https://cheqd.io/blog/2026/06/
- Freight: https://www.businesswire.com/news/home/20260519635199/en/Transfix-Launches-RFP-Automation-Software-for-Freight-Brokers-Turning-Thousand-Lane-Bids-into-a-Strategic-Pricing-Plan ; https://yespress.io/vooma ; https://www.pallet.com/use-cases/quoting ; https://www.ajot.com/news/project44-launches-ai-freight-procurement-agent
- B2B front door: https://www.marketscale.com/industries/software-and-technology/amazon-business-hits-60-billion-in-annualized-gross-sales-as-agentic-ai-reshapes-b2b-procurement ; https://www.deloitte.com/us/en/what-we-do/capabilities/applied-artificial-intelligence/articles/b2b-agentic-commerce.html ; https://ucpchecker.com/verticals/b2b ; https://www.digitalcommerce360.com/2026/03/10/agentic-commerce-faces-reality-check-in-b2b-ecommerce/
- Capacity: https://www.datacenterdynamics.com/en/news/openai-launches-guaranteed-capacity-offering-giving-customers-ability-to-secure-long-term-access-to-compute/ ; https://www.beri.net/article/openai-30m-capacity-trap-3-year-lockin-pays ; https://www.finout.io/blog/cloud-vendors-finally-agreed-on-commitments.-ai-vendors-didnt ; https://blockspace.media/insight/compute-exchange-launches-used-gpu-marketplace/
- Fraud and injection: https://www.sunrate.com/blog/thoughtleadership/invoice-manipulation-vendor-impersonation-rogue-agent-spend-the-new-b2b-fraud-surface/ ; https://www.f5.com/company/blog/ai-security-for-sourcing-procurement
