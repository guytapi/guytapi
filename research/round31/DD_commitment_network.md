# DD: The Commitment Network (merger of T4 4.5 + T1 Inbound Agent Desk + R20 counter-signature B)
Date: 2026-10-06. 11 searches used (limit 20). (U) = unverified.

## 0. Merged thesis as given
Business communication (email/collab ~$X0B incl. M365/Workspace share, plus contact-center software ~$15-20B and $300B+ in labour) assumes humans exchange prose and humans make commitments. When agents talk to agents across companies, the unit of communication becomes a **typed, counter-signed commitment** (offer → accept → fulfil → dispute). Rebuild business communication as the commitment network between companies' agents.

## 1. New evidence (searched this round)
1. **A2A v1.0 → 1.2 under the Linux Foundation, with signed Agent Cards and 150+ orgs** (Microsoft, AWS, Salesforce, SAP, ServiceNow) in production. Transport and identity for cross-company agents are now commoditized and open. Sources: [you.com A2A explainer, Aug 11 2026](https://you.com/resources/a2a-protocol-explained-what-agent-to-agent-communication-solves), [aiagentrank](https://aiagentrank.io/blog/what-is-a2a-protocol-2026).
2. **IETF draft PACT (Propose, Agree, Complete, Trust):** -00 published Jul 2026, -01 Sep 2026. It defines a signed Verifiable Task Contract, co-signed liability, escrowed settlement and co-signed Work Attestations, which is almost exactly the "typed counter-signed commitment" primitive. Sources: [draft-01](https://www.ietf.org/archive/id/draft-laxsharma-pact-01.html), [datatracker](https://datatracker.ietf.org/doc/draft-laxsharma-pact/).
3. **AAA + Integra Legal Context Protocol (Jun 24 2026),** with Google, IBM, Wayfair, UiPath and Circle as founding contributors. It covers terms, consent and recourse for agent transactions, needs "no intermediaries", and runs on any web server. Sources: [The Paypers](https://thepaypers.com/fraud-and-fincrime/news/aaa-and-integra-ledger-launch-agentic-commerce-legal-protocol), [Trinsic](https://www.trinsic.id/blog/aaa-and-industry-leaders-launch-legal-protocol-for-agentic-commerce).
4. **DocuSign opened its MCP server to agents (Sep 4 2026)** and ships Agent Studio plus obligation tracking. This is agent-to-system, not agent-to-agent, but DocuSign is reaching for the system of record for agreements. Sources: [optionfinance](https://www.optionfinance.fr/info-financiere-en-continu/d/2026-09-04-docusign-ouvre-son-serveur-mcp-aux-agents-dia.html), [DocuSign news](https://www.docusign.com/company/news-center/docusign-unveils-ai-assistant-and-agents-to-power-the-next-era-of-agreement-work).
5. **AgentMail raised a $6M seed (GC, Mar 2026). Nylas Agent Accounts shipped in Q1 2026** (100 sends per day, 7-day retention), so agent inboxes are now a funded race. Sources: [TNW](https://thenextweb.com/news/agentmail-raises-6m-seed-ai-agent-email-inboxes), [Nylas CLI guide](https://cli.nylas.com/guides/agentmail-vs-nylas-vs-cloudflare-email).
6. **Outlook Copilot Agent mode (Apr 27 2026)** handles triage, follow-ups and rescheduling. Workspace agents reach 750M users. Microsoft and Google own the human end of every email-shaped commitment. Sources: [letsdatascience](https://letsdatascience.com/news/microsoft-adds-agent-mode-to-copilot-in-outlook-cf24ae28), [towardsai](https://pub.towardsai.net/google-just-turned-gmail-docs-and-sheets-into-ai-agents-78e662b2c4d2).
7. **Demand check, contact center:** Gartner predicted in 2023 that 20% of inbound service volume would come from machine customers by 2026. Search found **no 2026 measurement** that confirms it. Sierra reports $150M+ ARR selling to human-shaped endpoints. Sources: [Gartner PR](https://www.gartner.com/en/newsroom/press-releases/2023-03-01-gartner-says-20-percent-of-inbound-customer-service-contact-volume-will-come-from-machine-customers-by-2026), [myaskai](https://myaskai.com/blog/zendesk-ai-sierra-ai-comparison-2026).
8. **Demand check, email:** AI SDR mail is huge, but reply rates fell to 4-5% and Gmail and Microsoft filter against it. No data found on agent-to-agent email threads. Salesforce's B2B Buyer Agent works over SMS and WhatsApp against **its own** catalog, not another company's agent. Sources: [Instantly](https://instantly.ai/blog/future-ai-bdr-b2b-sales/), [salesforcedictionary](https://salesforcedictionary.com/news/salesforce-news-june-24-2026-agentforce-commerce-ga).
9. **Carried forward from round 20 (internal):** Keelvar runs 1,420+ agent events per month, Pactum closes in 87 seconds, and DocuSign's Deputy GC named the gap on Aug 27.

## 2. Role 1: Technical architect
**System:** a "Commitment Gateway" per company plus a shared notarization and lookup network.
- **Ingest adapters:** A2A tasks, MCP tool calls, email (AgentMail/Nylas/Graph/Gmail), procurement platforms (Keelvar, Pactum, Coupa), and support channels.
- **Commitment schema:** a typed object `{parties, authority proof (agent card + delegation credential + limit), type: meet|deliver|pay|refund|SLA, terms hash (LCP pointer), deadline, verification method, status}`. It should be a strict superset of PACT VTC and LCP, not a rival standard.
- **Counter-signature:** each side's gateway signs with a company key (JWS/COSE). It falls back to a one-click human or email countersign link when the counterparty has no gateway. That fallback is what bootstraps the network.
- **Lifecycle engine:** obligations, reminders, fulfilment evidence (webhooks from ERP/OMS), breach detection and dispute export (AAA-ready bundle).
- **Policy firewall:** inbound commitments are checked against company limits before the agent may accept them, so prompt-injected or over-limit acceptances are blocked.
- **Hard parts:** (a) extracting commitments from prose email reliably, which an LLM does at roughly 90% and needs human-in-loop for the rest; (b) authority credentials, which are still drafts (GLEIF vLEI, IETF); (c) fulfilment evidence, which needs ERP integration and means days to weeks, not hours.
- **Buildability:** an MVP in 8-10 weeks for a single vertical (supplier procurement agents), using open standards.

## 3. Role 2: Skeptical CTO
- "A2A plus a signed JSON blob plus our CLM is already 80% of this. Why another vendor in the middle of every deal?"
- "My counterparties' agents run on Agentforce, Coupa or Pactum. Whatever those platforms log is the record, and I'll ask them for an export."
- "Email commitments? My people make them in Outlook, and Copilot will track them. I won't route mail through a startup."
- "How many cross-company agent-to-agent commitments do we make? Honestly, close to zero outside one sourcing pilot."
- "Fine if it's a free SDK I can call. I'm not paying $50K for a ledger nobody else uses."
- **Verdict:** interesting in 2028. Today it's a feature request to Coupa and DocuSign.

## 4. Role 3: Top-tier VC partner
- **Love:** a network-effect primitive (each record has two parties) that could become the "Visa/DocuSign of agent commerce". A huge TAM story spanning email, CLM, contact center and procurement.
- **Hate:**
  - The merger *widens* the story but splits the wedge into three buyers: a CTO of an agent product, a VP CX and a supplier CFO.
  - The open standards (PACT, LCP, A2A signed cards) commoditize the primitive. The value has to come from network and workflow, and those need volume that doesn't exist yet.
  - The same pre-demand failure as A and B+ (STATUS: B+ "system of record for everything agents agreed to" killed at 4.5).
- **Would invest if:** a founder shows 3 suppliers whose agents already close >100 deals a month each and who pay for the sealed record. Otherwise pass, and track LCP adoption.
- **Comps:** DocuSign at ~$15B+ EV shows the record-of-agreement layer can be huge, but it took 15 years and a law (ESIGN).

## 5. Role 4: Competitor analyst
| Player | Position vs the commitment network | Threat |
|---|---|---|
| Microsoft (Outlook/Copilot, A2A in Foundry/Copilot Studio) | Owns the human mailbox, calendar and Entra agent identity. Could add "commitments" to Copilot as a feature. Weak cross-tenant neutrality. | High on email, medium on cross-company |
| Google (Workspace agents, A2A originator, LCP contributor) | Controls the protocol stack and backs LCP, which means it wants the record *open*, not owned. | High: commoditizes the primitive |
| DocuSign (MCP, Iris, Agent Studio) | The natural incumbent for "counter-signed". It has the brand, the legal acceptance and the CLM obligation tracking. Its gap is that it is human-envelope-centric with per-envelope pricing. | **Highest**: one product cycle away |
| AgentMail / Nylas | Inbox infrastructure for agents. Could add structured "commitment" extraction. Developer-focused, low ACV. | Medium on the email wedge |
| AAA LCP / Integra | An open standard plus arbitration rails. A partner, not a product. Integra may sell notarization. | Medium (Integra) |
| Google A2A / PACT draft | Free protocol layers. They define the object, so the startup can't own the format. | Commoditizer |
| Salesforce Agentforce | Buyer and B2B ordering agents log commitments inside Salesforce. It wants to be the system of record for both sides inside its own walled garden. | High in CRM-centric B2B |
| Sierra / Decagon | Vendor-side conversational agents, priced per resolution. They could expose typed actions (refund, RMA) with receipts in a quarter. | Medium-high on the support wedge |
| Zendesk | Same as Sierra, plus an installed base. An "actions API for bots" is trivial for them. | Medium-high |
| Coupa/Ariba/Keelvar/Pactum (not on the list but decisive) | Own the actual cross-company agent deals today, and therefore the records. | **Highest in the only vertical with demand** |

**Structural opening that remains:** *neutrality across platforms.* A supplier selling through Keelvar, Coupa, Ariba and email has no single record of its own commitments, and no platform wants to be a neutral record for a rival platform's deals. This is the round-20 insight, and the merger adds nothing to it.

## 6. Self red-team: is there demand today?
- **Email-agent commitments:** no. Agent-to-agent email is mostly an SDR agent hitting a filter or an auto-reply. Commitments are still made by humans in Outlook and Gmail, where Microsoft and Google will add tracking.
- **Contact center:** no measured agent-originated volume. Gartner's 20%-by-2026 forecast has no confirming 2026 data. Vendors' pricing resists the shift, but there are no buyers yet (T1's own caveat).
- **Procurement / sourcing agents:** **yes, narrowly.** Thousands of agent-closed events per month exist (Keelvar, Pactum). This is the only place a counter-signed record has a real user today.
- **Legal / standards:** the attention is real (LCP, PACT, DocuSign GC), but standards are coming before revenue. Founders of standards rarely capture value unless they also run the network.
- **Conclusion:** the merger does not create demand. It **adds TAM narrative on top of the same single demand pocket**, which is supplier-side commitments in agent-run sourcing. "Business communication" as a framing invites Microsoft and Google into the competition and dilutes the wedge.

## 7. Final sharpened thesis (brief format)
**Shape:** "B2B commitments (sales orders, quotes, SLAs, which are today scattered across email, CLM and procurement portals, a $X0B workflow) assume a human said yes and the paper trail lives in one party's system. Agent-run sourcing makes both false: deals close in minutes between two companies' agents on a third party's platform. Therefore the commitment record must be rebuilt as a neutral, counter-signed network owned by the parties, not the platform."
- **Existing category:** CLM / e-signature (~$5-8B, U) + B2B order and commitment management + agent comms. Narrative TAM touches email and contact center, but they are excluded from the wedge.
- **Old assumption:** humans make and sign commitments, and the record lives in the buyer's or the platform's system.
- **Why AI breaks it:** agent-closed deals (Keelvar 90% agent-operated, Pactum 87 seconds), no human signature, and authority that is unverifiable.
- **New category:** a commitment network, which is a PACT/LCP-compatible gateway plus a two-party sealed record plus an authority registry.
- **Product:** "Every commitment our agents make, or accept, is typed, limit-checked, counter-signed and tracked to fulfilment, wherever it was made."
- **Buyer:** supplier CFO/Controller (economic) and GC (co-signer). Later, buyer-side procurement and audit.
- **Pain:** no auditor-grade record of agent-made commitments, unverifiable authority, and disputes argued on the buyer's platform logs.
- **Evidence:** §1 items 2, 3, 4 and 9, plus A2A signed cards (item 1).
- **Workaround:** platform exports, manual CLM entry, and email confirmations.
- **Competitors:** DocuSign, Coupa/Ariba/Keelvar/Pactum, Salesforce, Integra. Open standards: PACT, LCP, A2A.
- **Why incumbents may lose:** platforms can't be neutral across rivals. DocuSign's envelope and per-human pricing doesn't fit $0.50 machine commitments at 87-second speed.
- **Wedge:** freight, packaging and MRO suppliers selling into agent-run sourcing events.
- **Integration:** days (platform exports plus ERP order feed). Hours for the SDK countersign.
- **30-day pilot:** 3 suppliers, all agent-closed events sealed, 1 buyer counter-signing, 1 reconciliation that found a discrepancy.
- **Pricing:** $30-60K per year per entity plus $0.50-2 per sealed commitment. The counterparty countersigns free.
- **Expansion:** buyer side → authority registry → cross-counterparty outcome reputation → support/refund commitments (the T1 desk) → email-sourced commitments.
- **Moat:** at 10 customers, schemas and connectors. At 100, a two-sided record graph where counterparties are already enrolled. At 1,000, the default verifier any agent checks before accepting.
- **$10B case:** if agent-made B2B commitments become a majority, the neutral record becomes DocuSign plus Dun & Bradstreet for machines.
- **CTO one-liner:** "A receipt both companies signed for every promise our agents make."

## 8. Revised scores
| Criterion | 4.5 (T4) | T1 Desk | R20 B | **Merged (broad)** | **Sharpened (supplier wedge)** |
|---|---|---|---|---|---|
| Market size | 8 | 8 | 7 | 9 | 8 |
| Transformation | 7 | 8 | 8 | 8 | 8 |
| Urgency | 5 | 5 | 6 | 4 | 6 |
| Why-now | 7 | 6 | 8 | 7 | 8 |
| Buyer reach | 7 | 7 | 5 | 4 | 5 |
| Pilot speed | 8 | 7 | 6 | 5 | 6 |
| Integration | 8 | 7 | 6 | 5 | 6 |
| Competitive opening | 5 | 6 | 6 | 4 | 6 |
| Differentiation | 5 | 6 | 7 | 5 | 6 |
| Expansion | 8 | 8 | 8 | 9 | 8 |
| Moat | 6 | 6 | 7 | 6 | 7 |
| VC attractiveness | 7 | 7 | 6 | 6 | 6 |
| **Avg** | 6.75 | 6.75 | ~6.4-6.6 | **6.0** | **6.67** |

The broad merger scores *lower* than its parts. Urgency, buyer and opening collapse because Microsoft, Google, DocuSign and Salesforce all compete and the buyer is unclear. Open standards (PACT, LCP, A2A) cut differentiation versus round 20.

## 9. Verdict
**KILL the merged "rebuild business communication" thesis** as framed: there is no demand in email or contact center, the incumbents with the best distribution are already there, and the primitive is being standardized openly. **Keep one conditional survivor:** the sharpened supplier-side commitment network at 6.67, which is the round-20 B finalist re-validated. It still has the 15-20% test-pass odds and must pass the same 14-day test: at least 3 suppliers with more than 100 agent-closed commitments a month who will pay for a neutral sealed record. If it fails, close the agent-commitment family (A, B, B+, 4.5, T1) for good. Nothing reaches 8.5.
