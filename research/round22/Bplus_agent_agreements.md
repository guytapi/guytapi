# B+: System of record for everything your agents agreed to. Red-team deep dive

**Date:** 2026-10-06. **Method:** 38 WebSearch queries (WebFetch and Reddit blocked). Every URL below appeared in a search result. **No page was opened**, so every claim comes from a search snippet. Tags: **[summary-only]** = seen only in a search summary; **[unverified]** = not confirmed from a primary source; **[estimate]** = my own arithmetic. Inputs: `round20/outcome_B_candidates.md` (the original B finalist, "Counter-signature for machine-to-machine deals"), `round19/G1_agent_resource_sprawl.md`, `round18/FAILURE_TAXONOMY.md`, `round18/FINALIST_FORMAT.md`.

**Thesis B+:** "Your AI agents now agree to things on your company's behalf: ToS, DPAs, API terms, usage commitments, procurement awards. They do it thousands of times a month. We are the system of record for everything your agents agreed to." The product would:
- capture each agreement event, from MCP and gateway hooks, email, browser-agent instrumentation and Stripe Projects webhooks;
- store the exact terms version and the authority chain;
- flag risky clauses;
- enforce "agents may only accept pre-approved terms; escalate the rest to legal".

Buyer: GC or legal ops, plus CISO or CTO.

---

## Verdict: **KILL** (average 4.6; nine of eleven scores below 7)

**Causes of death:**
- **F1 (platform absorption).** The rails that agents use to accept terms (Stripe Projects, WorkOS auth.md, Okta XAA/ID-JAG, Keycard) record the acceptance themselves.
- **F5 (feature, not company).** Capturing terms and snapshotting the version is a feature for gateways, Nudge or CLM vendors.
- **A 20-year non-category.** "Employees click 'I agree' on the company's behalf and no one keeps a record" has been true since roughly 2005. Law firms have warned about it for years (Miller Canfield; Foley, 2009). It never produced a buyer-side company. Making the clicker an agent does not change two facts: the terms are **non-negotiable**, and the **stakes per acceptance are low**.

The thesis also breaks taxonomy rules §2.3 ("controls/visibility over AI is a category"), §4.1 (no visibility layer unless the platform is structurally barred), §4.4 (no reason incumbents won't act) and §4.5 ($100M without owning the niche).

**Comparison:** **the original B finalist (supplier-side counter-signature) is stronger.** B+ widens the scope in exactly the direction that removes the original's only structural edges:
- the multi-party conflict of interest;
- the dollar value per event;
- negotiated terms.

Most of what B+ adds (ToS and clickwrap for developer services, MCP terms, DPAs) is low-value, non-negotiable and already recorded by the rail. The only high-value subset is usage commitments and procurement awards, and that subset is the original B. **Recommendation:** do not run a separate B+ test. Fold one B+ element, a "terms snapshot plus authority chain at the moment of commitment", into the original B MVP. Treat everything else as a Nudge, Runlayer or Stripe feature.

---

## 1. Evidence that agents accept terms on behalf of companies

| Signal | Source | Read |
|---|---|---|
| **The Stripe Projects Developer Terms make the user bound.** The user acknowledges that their Agent "constitutes an 'electronic agent' as defined under ... UETA" and that agent-initiated transactions are legally binding. The user is "solely responsible for each transaction initiated by or through the Agent". Provisioning creates "a direct service relationship" with the Provider under the Provider's own ToS, privacy policy and AUP | https://stripe.com/legal/projects-developer-terms [summary-only] | **Real behavior: agents bind principals to third-party ToS.** But Stripe drafted the allocation and holds the record |
| **Stripe Projects enforces acceptance in the API.** It returns `TOS_ACCEPTANCE_REQUIRED` when developer or provider terms have not been accepted | https://stripe.com/legal/projects-developer-terms ; https://docs.stripe.com/projects/platform-integration [summary-only] | **Stripe already gates and logs terms acceptance.** The record is a by-product of the rail |
| **Cloudflare on Stripe Projects: "humans approve Terms of Service once".** That is the only required human step; after it, agents create accounts, buy domains and start paid subscriptions | https://blog.cloudflare.com/agents-stripe-projects ; https://ppc.land/cloudflare-lets-ai-agents-open-accounts-buy-domains-and-ship-code-no-human-required/ ; https://the-agent-report.com/2026/05/cloudflare-agent-account-domain-deploy/ [summary-only] | **On sanctioned rails, a human still accepts the ToS.** That weakens "agents agree thousands of times a month" |
| **WorkOS auth.md (May–Jun 2026; MIT license).** Agent sign-up protocol, adopted by Cloudflare, Firecrawl and Resend [unverified]. Two flows: (1) "Agent Verified": the agent's IdP (OpenAI, Anthropic, Cursor) attests the user through a signed ID-JAG; (2) "User Claimed": the user approves directly, which "produces an explicit record of user consent". The documented registration object has no "terms" field | https://workos.com/auth-md ; https://workos.com/changelog/agent-registration ; https://runtimewire.com/article/workos-launches-auth-md-agent-registration-protocol ; https://braindetox.kr/en/posts/auth_md_agent_signup_2026.html | **Agent sign-ups are being standardized, and the consent record is part of the protocol.** A missing `terms_version` field is a gap of one field |
| **Automated browser sign-ups breach most ToS.** "Every major SaaS platform" bans automated account creation. Agents like Claude Code or Devin that sign up through browser automation expose the operator to breach of contract, account termination and CFAA risk | https://anon.com/blog/agent-signups-tos-violations-legal-risk [summary-only; vendor content] | The unsanctioned path (browser agents clicking "I agree") is being pushed **toward sanctioned rails**, which record consent natively |
| **Legal commentary is settled enough to remove the "enforceability crisis" angle.** UETA §14: contracts can form by electronic-agent interaction "even if no individual was aware of or reviewed" them. Cripps (UK): AI is "an instrument through which the user acts" and "the user will be bound by the terms the AI accepts". Proskauer: "Who's really clicking 'Accept'?" (Part II, Apr 2025). Clifford Chance (Feb 2026): "liability gap ... may not be covered by existing contracts" | https://proskauer.com/blog/contract-law-in-the-age-of-agentic-ai-whos-really-clicking-accept ; https://www.cripps.co.uk/thinking/artificial-acceptance-how-ai-agrees-on-your-behalf/ ; https://stellagent.ai/insights/agentic-commerce-legal-liability ; https://blog.promise.legal/startup-central/copilot-committed-ad-ai-agent-liability-agency-law/ | **The law says the principal is bound.** That makes a record nice to have rather than decisive: the company is bound either way |
| **Apparent authority (pre-AI).** Anyone with apparent authority can bind the organization to a clickwrap. In one case the company escaped only because it had told the vendor in advance that only 3 executives could bind it. A 2009 case held a company bound by a clickwrap its *vendor* accepted | https://millercanfield.com/resources-alerts-607.html ; https://www.foley.com/?p=57844 ; https://www.lawjournalnewsletters.com/2010/06/30/when-employees-click-i-agree-for-their-employers | **This problem class is 15–20 years old.** No buyer-side category ever formed around it |
| **Reddit v. Anthropic (N.D. Cal., Mar 28, 2026).** The court found the companies "contractually bound" by Reddit's User Agreement through automated access, and remanded to state court | https://ppc.land/anthropic-loses-bid-to-keep-reddits-5-scraping-claims-in-federal-court/ ; https://www.courthousenews.com/reddit-prods-judge-to-move-anthropic-case-back-to-state-court/ | The strongest example of "automated systems bind a company to terms". It concerns crawlers at an AI lab, not enterprise agents. One case |
| **Amazon v. Perplexity (Comet).** PI in Mar 2026, based on ToS requiring agents to identify themselves. **Ninth Circuit lifted it in Aug 2026**: it is the *user* who accesses, with the agent's help | https://www.cooley.com/news/insight/2026/2026-03-17-court-finds-ai-agent-may-violate-state-federal-law-by-accessing-amazon-accounts-without-authorization ; https://aiweekly.co/alerts/ninth-circuit-lifts-amazon-block-on-perplexitys-comet-ai-agent | A dispute about agent **access**, not acceptance. The appellate trend is "the agent is the user's instrument", which again makes the principal bound |
| **AAA plus Integra Ledger Legal Context Protocol (Jun 24, 2026).** Records "the terms under which a transaction took place, which law governs it and what remedies are available", verifiable by counterparties and auditors. Contributors include Google, IBM, Circle and Wayfair | https://www.adr.org/news-and-insights/introducing-the-legal-context-protocol/ ; https://thepaypers.com/fraud-and-fincrime/news/aaa-and-integra-ledger-launch-agentic-commerce-legal-protocol ; https://cointelegraph.com/news/ai-is-getting-a-legal-layer-as-agentic-commerce-accelerates | The "terms version plus governing law" record is being **standardized as open protocol**, not sold as a product |
| **AP2 mandates and Mastercard Verifiable Intent.** Signed intent, cart and payment mandates give "who authorized what" for agent purchases. Both were donated to FIDO in Apr 2026 | https://risingwave.com/blog/agent-payments-protocol-ap2-explained/ ; https://eco.com/support/en/articles/15192002-ap2-protocol-explained-google-s-agentic-commerce-standard-2026 | **The authority chain for agent commerce is being standardized in protocols** |
| **MCP servers carry their own terms**, e.g. Hootsuite, BlueCat, Cisco ThousandEyes, ElevenLabs, InfoTrack, Curri. Typical clauses: no training on outputs, retention limits, the customer is responsible for agent loops and retries | https://www.hootsuite.com/legal/mcp-server-terms ; https://elevenlabs.io/mcp-terms ; https://bluecatnetworks.com/legal-documents/mcp-server-terms-and-conditions/ | **A new kind of agreement does exist.** In enterprises, MCP servers are connected through admin-approved gateways (Runlayer, MintMCP), so acceptance is an admin act, not an agent act |
| **Computer-use vendors recommend human confirmation for consequential actions.** Anthropic does; Microsoft Copilot Studio routes review requests to humans | https://learn.microsoft.com/et-ee/microsoft-copilot-studio/human-supervision-computer-use ; https://www.decryptiondigest.com/blog/governing-claude-computer-use-autonomous-desktop-agents [summary-only] | Default agent behavior is moving toward pausing before "I agree" |
| **Icertis survey (May 2026):** 47% of legal teams would detect an unauthorized AI action only after the fact; 23% have an agentic AI policy. **Litera (Jul 2026):** in-house legal is "winning on risk instinct, losing on governance infrastructure" | https://www.lawnext.com/2026/05/survey-legal-teams-lack-visibility-into-ai-agents-actions-icertis-research-finds.html ; https://www.lawnext.com/2026/07/in-house-legal-is-winning-on-risk-instinct-losing-on-governance-infrastructure-says-new-litera-report.html | Generic AI-governance anxiety. Nothing specific to agent-accepted terms |
| **Disputes or companies burned by agent-accepted terms** | Searches found **none**. Only consumer complaints about subscription auto-upgrades (Figma, Grok, Kling) that do not involve agents | **No evidence of pain.** Every scenario found is hypothetical |

**On the "thousands of times a month" claim [estimate]:** almost all agent activity happens *inside* accounts that already exist, under terms already accepted. New agreements arise only when a new provider, account, MCP server or paid tier is added. Even a heavy-agent company with 500 engineers probably creates tens of new vendor relationships a month, not thousands. Stripe Projects has about 49 providers in total. **Under this estimate the headline overstates the volume by about 100x.** The only high-frequency agreement events are procurement awards and M2M negotiations, which belong to the original B.

---

## 2. Competitors: every slice has an owner

| Slice of B+ | Who already does it | Overlap |
|---|---|---|
| **Capture the acceptance event plus who authorized it** | **Stripe Projects** (`TOS_ACCEPTANCE_REQUIRED`, scoped delegated credentials, per-provider caps); **WorkOS auth.md** (consent record in the User Claimed flow, ID-JAG attestation); **Okta XAA / ID-JAG** (GA Apr 2026 [unverified]; enterprise IdP decides which agent reaches which resource) and **Auth0 for AI Agents** (CIBA async approval); **Keycard** ("full chain of authority from the originating user to every downstream agent", step-up approval) | **Very high.** The authority chain is the core of what the identity vendors sell |
| **Gateway logs of agent tool calls, approvals and catalog** | **Runlayer** ($30M Series A, Jun 2026; catalog, approvals, an audit log per request); **MintMCP**; **Nirmata AIControls** (every delegated call written to an audit record attributed to the delegating human); MeshGuard ("delegation protocols with signed receipts", founded 2026) | **High.** "Agents may only use pre-approved providers" is the catalog feature these products already ship |
| **Terms version archive and clause intelligence across vendors** (the claimed "terms-version graph" moat) | **ConductAtlas**: 320+ platforms; provisions classified into 20 types (arbitration, liability, data sharing, etc.) with severity; SHA-256 hash per capture; diff views (e.g. Asana ToS); already covers Anthropic, LlamaIndex, Google Ads authority-to-bind clauses. **SaaS Tracker** (vendor terms, DPAs, sub-processors, with AI impact briefs and a review workflow). **TermDrift** (founded 2026). **PageCrawl, TOS Tracker, Changeflow, Visualping** | **Very high, and commoditizing.** The supposed moat is already a crowded niche of small tools |
| **Data-training clause flags per vendor** | **Nudge Security**: "condensed summaries of AI and SaaS vendors' data training policies" for 200K+ providers; tracks employee acknowledgements; finds every account created with a work email | **Very high**, and Nudge already sells to the CISO at the ICP |
| **Contract system of record / AI review** | **Ironclad** (>$200M ARR; Clickwrap via PactSafe; Renewal Agent Jun 2026); **DocuSign** (IAM, agents, Iris; MCP server opened to agents Sep 30, 2026); **Icertis Vera**; **Juro Operator**; **SpotDraft**; **Zip** (AI Contract Orchestration Apr 2026; 50 agents; risk classification); **Zylo** Contract Assist (Jan 2026) | High on the "procurement awards and commitments" slice. Ironclad Clickwrap and DocuSign Click hold acceptance evidence **on the seller side**, so they already have the counterparty's copy of what a customer's agent accepted |
| **Open-standard legal wrappers** | LCP (AAA/Integra), AP2 plus Verifiable Intent (FIDO), GLEIF vLEI | They set the format of the record. A neutral open standard lowers barriers to entry |
| **Agent-action evidence ledgers** | Ledger AI, AgentLedger (eIDAS QEL), LEDGIT (hackathon projects, 2026) | Signals the obvious idea is being built everywhere, and is trivially buildable |

**Is anyone doing exactly "a registry of agent-accepted agreements"?** I found no SKU with that name. The pieces exist across Stripe, WorkOS, Okta, Keycard, Runlayer, ConductAtlas and Nudge. Combining them is a join on (agent session, vendor, terms hash), which makes it **F5**.

---

## 3. Absorption: who owns it?

- **Stripe (Projects): the most likely owner of the developer-services slice.** It drafts the agent-binding clause, gates `TOS_ACCEPTANCE_REQUIRED`, knows the provider, cost and scoped identity, and has no conflict. An org-level "terms accepted by your agents" tab is a small feature that makes enterprises comfortable letting agents buy through Stripe.
- **Okta / Auth0 / Keycard / WorkOS: they own the authority chain** (who delegated to which agent). Adding a `terms_version` claim to an ID-JAG or auth.md registration is a spec change. Okta's motive is that "Agent governance" is its 2026 growth story.
- **Nudge (or Grip): owns "which vendor relationships exist and their training clauses"** for the CISO buyer. Adding "created by an agent" plus "terms version at sign-up" is a classifier on data Nudge already collects.
- **DocuSign: the natural owner for legal and GC buyers.** It holds the agreement repository, Iris clause extraction and an open MCP server, and its Deputy GC publicly framed "on whose authority did the agent act" (Aug 2026, per round 20). DocuSign Click already holds the seller-side acceptance records.
- **Ironclad: least likely to chase buy-side clickwrap, but could.** Clickwrap is a seller-side product. Ironclad's buy-side motion is Renewal Agent and CLM.

**Is any incumbent structurally barred (§4.4)?** No. The B+ events are **single-party**: the company's own agent accepts a vendor's standard terms. The conflict of interest that made the original B interesting (the buyer's platform holding the supplier's record) does not exist here.

---

## 4. Is the pain urgent?

**No. It is pre-demand, and probably low-value even once demand appears.**

1. **No company found that was harmed** by terms an agent accepted. Not one dispute, claim or practitioner post.
2. **The terms are non-negotiable.** For Vercel, Supabase, Cloudflare and MCP-server ToS, legal cannot redline anything. The only real decision is "use this vendor or not". That is a **vendor allowlist**, which security and IT already own (Nudge, Runlayer catalog, Stripe approved providers). It does not need a legal system of record.
3. **Stakes per acceptance are small.** Self-serve developer services usually cap liability at fees paid and default to free or low tiers. The large exposures (DPAs for regulated data, AI-training rights over customer data) already trigger enterprise procurement and security review before any agent touches the vendor.
4. **The law already resolves who is bound: the principal.** A record helps prove *what* was accepted. But vendors keep that proof themselves (Ironclad Clickwrap Snapshots, DocuSign Click), and in a dispute the vendor produces it.
5. **The 20-year precedent.** Employee clickwrap carried identical risk at higher volume and never became a funded buyer-side category. **The closest analog that *did* become a category is open-source license compliance (SCA: Snyk, Black Duck, FOSSA).** It became one because obligations attach on distribution and M&A diligence checks them. ToS for developer services have no comparable trigger.

**What could create urgency (watch list, not evidence):**
- M&A or SOC 2 / ISO 42001 auditors start asking for "an inventory of agreements entered by AI agents".
- Cyber or E&O insurers require it.
- A public incident where an agent-accepted MCP or API ToS assigned training rights over customer data.
- The EU AI Act logging obligations (Aug 2, 2026) get read to cover acceptance events.

None of these was found in this round.

---

## 5. Buyers, ACV, ARR math [estimate]

- **ICP pool:** software and AI-forward companies with heavy agent use and a GC or legal-ops function: about 5K–10K worldwide.
- **Budget:** legal-ops tooling budgets are small. Clickwrap and ToS-monitoring tools sell for about $5K–50K (ConductAtlas, SaaS Tracker and TermDrift are small tools).
- **Realistic ACV:** $15K–40K. Median about $25K.
- **$10M ARR:** about 400 customers at $25K. Possible only as a land inside an existing security or legal suite, while competing with Nudge renewals and free gateway logs.
- **$100M ARR:** about 4,000 customers, i.e. 40–80% of the niche. **Fails §4.5.**
- **Usage-based pricing** per agreement event: volume is tens per month per company, not thousands (§1), so the flow is too thin.
- **Moat claims, tested:**
  - **Terms-version graph across vendors:** already built and commoditizing (ConductAtlas: 320+ platforms with hashes and diffs; SaaS Tracker; TermDrift; generic page monitors).
  - **Authority registry:** owned by IdPs and agent-identity vendors (Okta XAA, Keycard, WorkOS, GLEIF vLEI).
  - **Counter-signature network:** only meaningful for *negotiated, two-party, high-value* commitments, which is the original B. With non-negotiable vendor ToS the vendor has no reason to counter-sign anything a neutral third party holds.

---

## Finalist format (for the record; outcome is KILL)

- **One-line problem:** AI agents bind companies to third-party terms (ToS, MCP and API terms, DPAs, usage commitments, procurement awards), and no one keeps a single record of what was accepted, which version, or on whose authority.
- **Why now:**
  - Stripe Projects (49 providers) makes agents UETA "electronic agents" whose actions bind the user.
  - Cloudflare lets agents create accounts after one human ToS approval.
  - WorkOS auth.md (May–Jun 2026) standardizes agent sign-ups.
  - MCP servers now ship their own terms.
  - LCP (Jun 2026) and AP2/Verifiable Intent (FIDO, Apr 2026) standardize the legal and authority wrapper.
- **Exact buyer:** GC or Head of Legal Ops (economic). CISO or CTO (co-signer, and in practice the real owner of vendor allowlisting).
- **Exact ICP:** software companies with 200–5,000 employees, more than 50% of engineers on Claude Code, Cursor or Codex, using Stripe Projects or 10+ agent-connected MCP or API vendors, with an in-house legal team of at least 3.
- **Current workaround:**
  - Vendor allowlists in the MCP gateway (Runlayer, MintMCP) or Stripe approved providers and caps.
  - Nudge for account discovery and training-policy summaries.
  - Enterprise procurement and security review for anything touching regulated data.
  - ToS monitors (ConductAtlas, SaaS Tracker, TermDrift).
  - The vendor's own acceptance records if a dispute arises.
  - In most companies, nothing, with no visible consequence.
- **Why incumbents cannot easily own it:** they can. Stripe, Okta, Keycard, WorkOS, Nudge and DocuSign each hold the event, the authority chain or the clause data. The events are single-party, so no structural conflict exists.
- **30-day MVP:**
  - An MCP and gateway plugin plus Stripe Projects webhook ingestion plus a mailbox parser for "Welcome / you accepted our Terms" emails.
  - On each new vendor relationship: fetch and hash the terms in effect, attach the agent session, human and repo, and score clauses (liability, training rights, auto-renew, governing law).
  - Policy: block non-allowlisted vendors and escalate flagged clauses to legal in Slack.
- **Pilot design:**
  - 3 companies, 14 days, read-only.
  - **Success:** at least 20 agent-initiated new agreements per 100 engineers per month; at least 1 flagged clause that legal says it would have rejected; and willingness to pay at least $20K.
- **Pricing hypothesis:** $20–40K per year platform fee, or per-engineer pricing. Usage pricing does not work because volume is low.
- **Expansion path:** registry, then policy enforcement, then renewal and commitment management, then procurement awards (converging into the original B), then counter-signature network. **Every expansion step leads into the original B or into Stripe, Okta or DocuSign territory.**
- **Moat:** weak (see §5). The terms graph is commoditized, the authority chain belongs to the IdPs, and the counter-signature network does not apply to non-negotiable ToS.
- **Why it could become $10B+:** only by becoming the evidence layer for *all* machine-made commitments, the DocuSign of agents. That outcome depends on negotiated, high-value commitments (the original B), not on clickwrap.
- **Direct competitors and adjacent threats:**
  - Rails and identity: Stripe Projects, WorkOS auth.md, Okta XAA / Auth0, Keycard.
  - Gateways and evidence ledgers: Runlayer, MintMCP, Nirmata AIControls, MeshGuard.
  - Discovery and clause intelligence: Nudge, ConductAtlas, SaaS Tracker, TermDrift.
  - CLM and procurement: DocuSign (IAM, Click, MCP), Ironclad (Clickwrap, Renewal Agent), Icertis, Juro, SpotDraft, Zip, Zylo.
  - Standards: LCP (AAA/Integra), AP2 / Verifiable Intent (FIDO).
- **One sentence to a GC:** "Last month your agents accepted 47 sets of vendor terms you've never read, 3 of them granting training rights over data your agents sent. Here is every one, with the version, the clause and the engineer who delegated it." *(Likely reply: "Those are non-negotiable click-throughs. Security already approves the vendor list. Why do I need this?")*
- **5 customer discovery questions:**
  1. How many new vendor, API or MCP relationships did agents create last month? Who approved them, and how do you know?
  2. Has any agent-accepted term (training rights, auto-renew, liability, jurisdiction) ever caused an issue, or been raised by an auditor, insurer or acquirer?
  3. Would legal do anything differently on a non-negotiable click-through except block the vendor? Who owns the vendor allowlist today?
  4. Do Nudge, your MCP gateway or Stripe Projects already show you this? What is missing?
  5. Is "agreements entered by AI agents" on your SOC 2, ISO 42001, M&A diligence or cyber-insurance questionnaire?
- **Hard kill criteria:**
  - (a) Fewer than 20 agent-initiated new agreements per 100 engineers per month. **Likely met**, per the §1 estimate.
  - (b) Legal says it would only allow or block the vendor, which makes this a security allowlist. **Likely met.**
  - (c) No auditor, insurer or acquirer asks for it.
  - (d) Stripe, Okta or WorkOS adds a terms-version field or acceptance log. **Partly met already** (Stripe gating, auth.md consent record).

### Scores

| Dimension | Score | Why |
|---|---|---|
| Pain | 3 | No incident, dispute or complaint found. The terms are non-negotiable and low stakes |
| Urgency | 3 | No audit, insurer or regulatory trigger yet. The principal is bound either way |
| ROI clarity | 3 | Value is speculative risk avoidance. The vendor already keeps the proof |
| Customer accessibility | 6 | GCs are reachable but have small tooling budgets. CISOs are flooded with offers |
| Pilot speed | 7 | Gateway and webhook ingestion is fast |
| Market size | 5 | About 5K–10K buyers at about $25K. Volume too thin for usage pricing |
| Expansion | 6 | Expansion leads into the original B or into incumbent territory |
| Venture potential | 4 | Reads as a Stripe, Okta, Nudge or DocuSign feature |
| Defensibility | 2 | Terms graph commoditized (ConductAtlas et al.). Authority chain owned by the IdPs |
| Why now | 8 | Stripe Projects' UETA clause, auth.md, MCP terms and LCP are all from 2026 |
| Competition position | 3 | Every slice is owned, and the rails record acceptance natively |
| **Average** | **4.5** | **KILL** (F1 + F5 + historical non-category). Fails §2.3, §4.1, §4.4 and §4.5 |

### Why not B
B requires the thesis to be unresolved and massive with a structural edge. B+ is **resolved by the rails**:
- Stripe gates and logs ToS acceptance.
- Cloudflare keeps the ToS step human.
- auth.md builds the consent record into the protocol.
- Okta, Keycard and WorkOS carry the authority chain.
- ConductAtlas-style tools already archive terms versions.

Its only structural edge, a neutral two-party record for negotiated high-value commitments, belongs to the original B, and broadening dilutes that edge rather than adding to it.

---

## Comparison with the original B finalist

| | Original B: supplier-side counter-signature for M2M deals | B+: all agent-accepted agreements |
|---|---|---|
| Value per event | High (procurement awards, $K–$M) | Low (mostly free or low-tier ToS) |
| Terms negotiable? | Yes (offers and counters) | Mostly no (clickwrap) |
| Parties | Two, and the record-keeper is conflicted (the buyer's platform) | One (own agent and the vendor's standard terms) |
| Structural reason incumbents won't own it | Partial (conflict, multi-platform) | None |
| Who records it today | Buyer platform only (Keelvar, Pactum) | Stripe, WorkOS, IdPs, gateways, the vendor itself |
| Network effect | Counter-signature is two-sided | None |
| Volume | 1,400+ M2M events/month on Keelvar alone, growing | Tens of new agreements per company per month [estimate] |
| Average score | 6.5 (B, conditional) | 4.5 (KILL) |

**The original B is stronger.** Keep its 14-day test unchanged. Add one question to it:

> "Besides awards, do your agents accept vendor terms or usage commitments? Would you want those in the same record?"

If at least 5 of 15 interviewees say yes, *and* cite a commitment of at least $10K (auto-renewing usage tiers, reserved capacity), add a "commitments beyond awards" module. Do not reopen B+ as a standalone company.

**Reopen B+ only if** one of these happens:
- A public incident in which an agent-accepted term (training rights, auto-renewing commitment, unlimited liability) costs a named company more than $1M.
- Or SOC 2 / ISO 42001 / Big-4 audit guidance requires an inventory of agent-entered agreements.
- Or Stripe, Okta and WorkOS all decline to expose acceptance records across rails by Q2 2027.

## Sources (all appeared in search results; none opened)
- Stripe Projects: https://stripe.com/legal/projects-developer-terms ; https://docs.stripe.com/projects/platform-integration ; https://stripe.com/blog/stripe-projects-adds-new-agents-providers-developer-controls ; https://glenbrook.com/payments_news/stripe-everything-announced-at-sessions-2026/
- Cloudflare: https://blog.cloudflare.com/agents-stripe-projects ; https://ppc.land/cloudflare-lets-ai-agents-open-accounts-buy-domains-and-ship-code-no-human-required/ ; https://the-agent-report.com/2026/05/cloudflare-agent-account-domain-deploy/
- auth.md: https://workos.com/auth-md ; https://workos.com/changelog/agent-registration ; https://runtimewire.com/article/workos-launches-auth-md-agent-registration-protocol ; https://braindetox.kr/en/posts/auth_md_agent_signup_2026.html
- Agent sign-up ToS risk: https://anon.com/blog/agent-signups-tos-violations-legal-risk
- Legal commentary: https://proskauer.com/blog/contract-law-in-the-age-of-agentic-ai-whos-really-clicking-accept ; https://www.cripps.co.uk/thinking/artificial-acceptance-how-ai-agrees-on-your-behalf/ ; https://stellagent.ai/insights/agentic-commerce-legal-liability ; https://blog.promise.legal/startup-central/copilot-committed-ad-ai-agent-liability-agency-law/ ; https://millercanfield.com/resources-alerts-607.html ; https://www.foley.com/?p=57844 ; https://www.lawjournalnewsletters.com/2010/06/30/when-employees-click-i-agree-for-their-employers ; https://www.ballardspahr.com/insights/blogs/2026/07/podcast-agentic-commerce-is-coming-will-the-legal-system-be-ready
- Cases: https://ppc.land/anthropic-loses-bid-to-keep-reddits-5-scraping-claims-in-federal-court/ ; https://www.courthousenews.com/reddit-prods-judge-to-move-anthropic-case-back-to-state-court/ ; https://www.cooley.com/news/insight/2026/2026-03-17-court-finds-ai-agent-may-violate-state-federal-law-by-accessing-amazon-accounts-without-authorization ; https://aiweekly.co/alerts/ninth-circuit-lifts-amazon-block-on-perplexitys-comet-ai-agent
- Standards: https://www.adr.org/news-and-insights/introducing-the-legal-context-protocol/ ; https://thepaypers.com/fraud-and-fincrime/news/aaa-and-integra-ledger-launch-agentic-commerce-legal-protocol ; https://cointelegraph.com/news/ai-is-getting-a-legal-layer-as-agentic-commerce-accelerates ; https://risingwave.com/blog/agent-payments-protocol-ap2-explained/ ; https://eco.com/support/en/articles/15192002-ap2-protocol-explained-google-s-agentic-commerce-standard-2026
- MCP terms: https://www.hootsuite.com/legal/mcp-server-terms ; https://elevenlabs.io/mcp-terms ; https://bluecatnetworks.com/legal-documents/mcp-server-terms-and-conditions/ ; https://www.thousandeyes.com/pdf/cisco-networking-mcp-server-terms.pdf
- Human confirmation: https://learn.microsoft.com/et-ee/microsoft-copilot-studio/human-supervision-computer-use ; https://www.decryptiondigest.com/blog/governing-claude-computer-use-autonomous-desktop-agents
- Surveys: https://www.lawnext.com/2026/05/survey-legal-teams-lack-visibility-into-ai-agents-actions-icertis-research-finds.html ; https://www.lawnext.com/2026/07/in-house-legal-is-winning-on-risk-instinct-losing-on-governance-infrastructure-says-new-litera-report.html
- Identity and gateways: https://nirmata.com/2026/08/18/okta-cross-app-access-xaa-id-jag/ ; https://auth0.com/blog/xaa-protocol-auth0-ai-agents/ ; https://keycard.ai/blog/announcing-keycard-for-coding-agents/ ; https://www.helpnetsecurity.com/2026/05/15/keycard-for-multi-agent-apps/ ; https://www.runlayer.com/mcp-gateway ; https://mintmcp.com/blog/mintmcp-vs-runlayer-vs-portkey ; https://linkedin.com/company/meshguard
- Terms intelligence: https://conductatlas.com/about/ ; https://conductatlas.com/methodology/ ; https://www.legaltechnologyhub.com/vendors/saas-tracker/ ; https://techindex.law.stanford.edu/companies/termdrift ; https://pagecrawl.io/blog/monitor-terms-of-service-changes-saas-vendors ; https://tostracker.app/compliance ; https://changeflow.com/learn/vendor-terms-of-service-monitoring
- Nudge: https://www.nudgesecurity.com/use-cases/ai-security-2 ; https://securitybrief.co.uk/story/nudge-security-adds-new-tools-to-govern-ai-in-saas
- CLM and procurement: https://ironcladapp.com/resources/product-features/clickwrap ; https://support.ironcladapp.com/hc/en-us/articles/40760031220887-2026-Release-Log ; https://legaldive.com/news/ironclad-Snapshots-contracts-CLM-legal-teams-defend-onlinecontracts-clickwrap-clickthrough/623280 ; https://www.docusign.com/products/docusign-click ; https://app.dealroom.co/news/feed/docusign-opens-ai-agreement-layer-to-every-agent-via-model-context-protocol ; https://www.icertis.com/products/platform/vera-agents/ ; https://juro.com/us ; https://secure.businesswire.com/news/home/20260416262512/en/Zip-Launches-AI-Contract-Orchestration-Giving-Legal-and-Procurement-Teams-Back-the-Millions-of-Hours-Lost-to-Manual-Contract-Review ; https://zylo.com/news/agentic-saas-management
- Hackathon and early ledgers: https://lablab.ai/ai-hackathons/techex-intelligent-enterprise-solutions-hackathon/ledgerai/ledger-ai ; https://hall.0g.ai/t/agentledger-making-ai-agents-insurable/253 ; https://ethglobal.com/showcase/ledgit-kxpph
- OSS license analog: https://www.blackduck.com/blog/open-source-license-compliance-dependencies.html
