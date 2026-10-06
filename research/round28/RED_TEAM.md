# Round 28: Red team

**Date:** 2026-10-06. **Role:** red team. The job was to kill theses on evidence while staying fair.
**Inputs read:** BRIEF.md, all nine H1-H3 theses, STATUS.md, round20/outcome_B_candidates.md, round18/FINALIST_FORMAT.md.
**Method:** 34 web searches. WebFetch was blocked, so every fact comes from search snippets. **[U]** marks a claim seen in only one secondary snippet. Every URL below appeared in a search result; none was invented.

## Verdict table

| # | Thesis | Author score | Red-team score | Verdict |
|---|---|---|---|---|
| 1 | H2 Intent Scheduler (cross-vendor, pre-code admission control) | 6.6 | **5.6** | **KILL** |
| 2 | H3 Undo Graph (reversibility ledger) | 6.5 | **5.6** | **KILL** (keep as a tripwire) |
| 3 | H3 Verified Uptime (neutral reliability attestation) | 6.4 | **5.3** | **KILL** |
| 4a | H1 Hammer for agent vendors (scoped contract graph) | 6.2 | **5.5** | **KILL** |
| 4b | H1 Statistical release control | 6.3 | **5.5** | **KILL** |
| 5 | Convergent theme: "independent attestation layer for AI-operated businesses" | n/a | **≤5.5 as one company** | **KILL** as a merge. It is weaker than the round-20 finalist. |

**Nothing survives as A or B.** Because no thesis survived, there is no finalist write-up. The round-20 counter-signature finalist (6.5) remains the best open item. One new fact makes it weaker: DocuSign's MCP server went GA on Sep 30 2026, and DocuSign pitches itself as "the essential agreement layer for any agent platform". Its competition score should drop from 6 to 5, which takes the average to about 6.4.

---

## 1. H2 "Intent Scheduler": KILL (6.6 → 5.6)

**The thesis's own claim:** no org-wide, cross-vendor commercial owner exists; the layer exists only as local OSS (Foremerge, Agent Mail, Weave and others), and that pattern usually comes just before a vendor category forms.

**Hidden competitors found (Jul-Oct 2026).** The category formed during the round. These are commercial or team-wide, not local:
- **Shepherd by Korso (YC P26).** A shared hub that agents connect to over MCP (Claude Code, Codex, Cursor). It gives out *leases on parts of the codebase* and shows a *live presence feed* across teammates' machines. It is open source and self-hostable, launched on Product Hunt. This is the thesis's "hot-zone leases" MVP, already shipped and backed by YC. ([producthunt.com/products/shepherd-9](https://www.producthunt.com/products/shepherd-9); [github.com/Korso-AI/Shepherd](https://github.com/Korso-AI/Shepherd))
- **Tether (tetherlab), an F4 Fund portfolio company.** Describes itself as "the coordination layer for teams running AI coding agents in parallel… duplicate PRs and conflicting changes… keeps every agent aware of what the others are building." Funding size unknown **[U]**. ([f4.fund/startups/tetherlab](https://f4.fund/startups/tetherlab))
- **Coordinaut** (task ownership, scoped file locks and handoffs across Codex, Claude Code and Cursor) and **Tirith** (claims, contracts and change notices over MCP; last updated Sep 18 2026). ([enterprisedna.co/directories/mcp/eabz-tirith](https://enterprisedna.co/directories/mcp/eabz-tirith))
- **Augment Cosmos** "coordinates and governs fleets of agents across a team's entire software development lifecycle". This is new since the thesis listed only Augment Intent. ([augmentcode.com/tools/factory-ai-vs-augment-cosmos](https://www.augmentcode.com/tools/factory-ai-vs-augment-cosmos))
- **The research layer is already formalized.** The "Claim Plane: Enforceable Change Intents and Dynamic Scope" paper (arXiv 2607.21909, Jul 2026) defines exactly the admission-control primitive, so the IP is public. ([arxiv.org/pdf/2607.21909](https://arxiv.org/pdf/2607.21909))
- **The cost ledger is taken.** Faros **Token Intelligence** sorts token spend into "productive, inefficient, or wasteful" and links it to PR merge rate, change failure and incidents. ([faros.ai/blog/token-intelligence-for-ai-engineering](https://www.faros.ai/blog/token-intelligence-for-ai-engineering))
- **The platform absorbs the symptom.** In September 2026 GitHub shipped Copilot "agent merge", which handles review feedback, failed checks, merge conflicts and workflow reruns, plus automatic session cleanup. ([github.blog changelog 2026-10-01](https://github.blog/changelog/2026-10-01-github-copilot-in-vs-code-september-2026-releases))

**Economic incentive attack.**
- **Abandoned work is not the same as waste.** The "32.7% merge rate means two-thirds is waste" step counts deliberate best-of-N attempts (Agent HQ assigns Copilot, Claude and Codex to the *same issue* on purpose) as waste. Buyers pay for those attempts by choice. So the measurable waste is only collisions plus genuine duplicates, which is a much smaller number than the thesis's ≥20% pass bar assumes.
- **Conflicts are getting cheaper to fix after the fact.** The OCC-collapse argument needs the cost of a conflict to be high: rebase, then re-run CI. GitHub agent merge and cheap tokens make resolving conflicts after the fact automatic. Prevention is worth paying for only if after-the-fact costs stay high, and the platforms are pushing those costs down every month.

**Does it break at 100x?**
- The architecture argument is still correct: hot modules really do behave like hot rows.
- But a lease service is a sprint-sized build (round-8 test), and Shepherd ships one as free OSS.
- The thesis's moat is "calibration data across many orgs". Shepherd and Tether will collect the same data first.

**Cheapest disproof.** It already happened: a YC company launched the MVP as OSS before our first pilot, and an F4-backed startup sells the same positioning.

**Revised scores:** Pain 6, Urgency 5, ROI clarity 5, Customer accessibility 7, Pilot speed 8, Market size 6, Expansion 7, Venture potential 5, Defensibility 3, Why now 8, Competition position 2. **Average 5.6.** Two of the thesis's own kill criteria are already close to firing: "platform teams will build it" and a funded entrant with the same pitch.

---

## 2. H3 "Undo Graph": KILL (6.5 → 5.6), kept as a tripwire

**The thesis's own claim:** nobody sells the join of change identity → runtime → data writes → undo plan.

**What absorbs each half:**
- **"Which live changes are in the failing path" is Datadog's.**
  - Datadog **Bits Release** "automatically follows every change from PR to production", writes a validation plan for each PR, and runs it continuously on telemetry. ([datadoghq.com/blog/bits-release](https://datadoghq.com/blog/bits-release/))
  - Datadog Feature Flags change tracking "automatically identif[ies] which services are affected by a flag change, and roll[s] back problematic flags directly from inside Datadog". ([docs.datadoghq.com/change_tracking/feature_flags](https://docs.datadoghq.com/change_tracking/feature_flags/))
  - The thesis listed Datadog only as [U-prior]. That status is now confirmed, and Datadog covers more than the thesis assumed.
- **Undo by deployment ID already exists at the schema level.** Liquibase's targeted rollbacks ("rollback-one-update… revert all changes… related to a specific deployment ID") and Harness DB DevOps tags. ([docs.liquibase.com targeted rollbacks](https://docs.liquibase.com/oss/user-guide-4-33/what-are-targeted-rollbacks))
- **Whole-state undo is native to the database platforms.**
  - Neon snapshots are pitched explicitly as "checkpoints for agents": a restorable database version per meaningful change, plus 100 snapshots per project. ([neon.com/blog/checkpoints-for-agents-with-neon-snapshots](https://neon.com/blog/checkpoints-for-agents-with-neon-snapshots))
  - Dolt markets a version-controlled database "when agents break things". ([aidatabase.dolthub.com](https://aidatabase.dolthub.com/))
  - Rubrik's "rewind" covers files, databases, configurations and repos. ([itbrew.com, Mar 2026](https://www.itbrew.com/stories/2026/03/06/how-reversible-is-an-agentic-mistake))
  - This is the thesis C graveyard (4.6).
- **What remains unowned:** row-scoped inverse writes for one change set, computed from CDC before-images, and only for rows nobody has touched since. That is a single feature.

**Economic incentive attack.**
- **No base rate.** The thesis admits no public source gives the share of incidents that were rollback-unsafe or needed data repair. My search for postmortems turned up the usual episodic cases (LootLocker migration data loss, Apr 2026; PostHog's multi-day person-property backfill, Jan 2026), not a rising series.
- **Bought after the pain, not before.** The purchase looks like insurance and happens after an incident, and the thesis itself scores urgency 6. Round 1 thesis C died on exactly that dynamic.
- **Install friction.** It sits in the database write path (a WAL-message extension) and needs DBA and security approval. The incumbents that already own the data plane (Neon, Datadog, Harness) do not face that friction.

**Does it break at 100x?** Yes for flag-interaction attribution. That is a real second-order effect. But at 100x the responder is an AI SRE (Resolve, Traversal, Datadog Bits). They will either consume a write-stamp standard for free, or Datadog will add `change_set` to its own tracer. Whoever owns the tracer owns the standard, and an independent OTel processor does not.

**Cheapest disproof (data, not interviews).**
- Take 90 days of incident records from two ICP companies.
- Count incidents where deploy-level or flag-level revert was *unsafe* because of data the change wrote.
- **Kill** if there are fewer than 2 per quarter per company. **Prior:** that is likely, given the lack of any public series.

**Tripwire to reopen:** an OTel semconv proposal for change identity on writes; or a public AI-SRE vendor post saying rollback safety blocks auto-remediation; or Bemi/Neon shipping "revert by commit".

**Revised scores:** Pain 6, Urgency 5, ROI clarity 5, Customer accessibility 6, Pilot speed 5, Market size 6, Expansion 7, Venture potential 6, Defensibility 5, Why now 7, Competition position 4. **Average 5.6.**

---

## 3. H3 "Verified Uptime": KILL (6.4 → 5.3)

**The wedge (SLA-credit reconciliation) is crowded and small, on the customer side:**
- **Complaya** (automates SLA enforcement; "recover 3%+ of SaaS, cloud and AI spend").
- **Pingoru** ("independent, time-stamped uptime evidence" across 6,000+ status pages).
- **SLA Credit Watch.**
- The figure quoted in that market is that the average enterprise leaves **$20-50K/yr** in credits unclaimed. That is too small to fund a CFO/GC sale. ([Complaya release](https://markets.financialcontent.com/wral/article/abnewswire-2025-7-22-complaya-is-automating-sla-enforcement-helping-to-recover-lost-saas-cloud-and-ai-credits); [pingoru.io/sla-monitoring](https://pingoru.io/sla-monitoring))
- The thesis's ≥$250K discrepancy pass bar therefore looks unlikely to clear.

**The network side is owned on every flank:**
- **Parametrix** tracks 7,000+ SaaS/PaaS/IaaS services and 750+ data centres and runs AIG's parametric cover (Aug 2026). It raised a $27M Series B in Dec 2025 ($45M total), with 3x top-line growth. ([parametrixinsurance.com Series B](https://www.parametrixinsurance.com/in-the-news/parametrix-raises-27m-in-series-b-round))
- **Vanta** (raised $150M at a $4.15B valuation) has moved from point-in-time checks to "continuous, zero-touch verification", plus Trust Centers whose evidence its own vendor-risk agent pulls in. ([pulse2.com Vanta Series D](https://pulse2.com/vanta-150-million-series-d-funding-raised-at-4-15-billion-valuatoin-for-ai-based-trust-management-platform); [Vanta launch, Mar 2026](https://vanta2023tf.q4web.com/news/news-details/2026/Vantas-New-Agents-and-Enterprise-Controls-Eliminate-Audit-Chaos/default.aspx))
- **Kosli** launched "governance infrastructure for AI assisted software delivery" on May 15 2026: policy-as-code and cryptographic evidence chains. It partnered with Adaptavist in June 2026 and co-chairs FINOS SDLC controls with Deutsche Bank and Morgan Stanley. That is the change-control half of this thesis, sold to the same regulated ICP. ([prnewswire Kosli launch](https://tools.prnewswire.com/en-us/live/20813/release/20260515EN60727))
- **Drata** supports the AIUC-1 framework and sells agent governance. ([drata.com AIUC-1](https://drata.com/updates/new-framework-support-aiuc-1))
- **Ratings side:** Kovrr sells an AI vendor risk score, and SecurityScorecard has TITAN AI. ([kovrr.com/ai-score-contact](https://www.kovrr.com/ai-score-contact))

**Buyer urgency test (failed).**
- I searched for an outage claim denied under an AI exclusion and found **none documented**. There is only commentary on exclusions (Shumaker client alert, tianpan) and the "coverage vacuum discovered at claim time" framing.
- EU DORA does push evidence requests onto SaaS vendors, but those requests go to TPRM and trust-centre tools today and are not specific to agents. ([blog.usecure.io DORA](https://blog.usecure.io/dora-what-the-eus-cyber-resilience-law-means-for-saas-vendors-and-their-financial-sector-customers))

**Incentive problem left unresolved.** The author already noted it. A neutral record that "this outage came from an agent change" helps carriers *deny* claims under AI exclusions, so the vendor's GC is not incentivized to create it. The party that pays is the party the record exposes.

**Revised scores:** Pain 5, Urgency 4, ROI clarity 5, Customer accessibility 5, Pilot speed 6, Market size 6, Expansion 7, Venture potential 6, Defensibility 5, Why now 6, Competition position 3. **Average 5.3.**

---

## 4a. H1 "Hammer for agent vendors": KILL (6.2 → 5.5)

- **Market size kills it before competition does.** The author's own serviceable market is $150-450M, and $10B needs a separate "verified outcome billing" leap that T2 already killed (4.7).
- **The top buyers built it in-house:** Decagon Agent Versioning, Intercom Evals/Releases, Sierra.
- **Eval tools cover most of the long tail.** Braintrust already does CI regression with "one click [turns] a production trace into a test case". A tenant tag on a dataset is metadata, not a new data model. ContextQA runs "1,200+ model-upgrade regressions weekly". LaunchDarkly AgentControl has per-segment targeting. ([braintrust.dev](https://www.braintrust.dev/learn/ai-testing/v0); [contextqa.com/integrations/amazon-bedrock](https://contextqa.com/integrations/amazon-bedrock/))
- **Unproven core:** the "fleet-repeat escalations ≥25%" claim has no data behind it.
- **Pilot speed is generous.** Pilots need access to each tenant's escalation history, which is customer data under DPAs.

**Revised scores:** Pain 6, Urgency 5, ROI clarity 6, Customer accessibility 7, Pilot speed 7, Market size 5, Expansion 6, Venture potential 5, Defensibility 4, Why now 6, Competition position 3. **Average 5.5.**

## 4b. H1 "Statistical release control": KILL (6.3 → 5.5)

- **Cleanlab → Handshake (Jan 2026) is now corroborated by a second snippet [U, secondary]**: trust scores plus human-in-the-loop remediation. ([rfp.wiki/vendors/cleanlab](https://www.rfp.wiki/vendors/cleanlab))
- **The statistics are public playbook material.** The "100/10/1" tiered sampling playbook (100% heuristics, 10% LLM judge, 1% human) and review-queue research (arXiv 2605.27202) mean it fails the sprint test. ([channel.tel tiered sampling](https://www.channel.tel/blog/tiered-eval-sampling-production-agents); [arxiv.org/pdf/2605.27202](https://arxiv.org/pdf/2605.27202))
- **The certificate side is owned.** Armilla sells "independent verification to support compliance and procurement" plus an AI Performance Warranty that pays when AI underperforms ($25M, Jan 2026). AIUC-1 requires quarterly third-party testing. ([armilla.ai/vendor](https://armilla.ai/vendor))
- **No urgency driver.** Margins are rising (ICONIQ), so review cost does not force a purchase.

**Revised scores:** Pain 6, Urgency 5, ROI clarity 7, Customer accessibility 6, Pilot speed 7, Market size 6, Expansion 6, Venture potential 5, Defensibility 3, Why now 6, Competition position 3. **Average 5.5.**

---

## 5. Convergent theme: "a neutral, verifiable record of what AI did, that third parties rely on"

**Question:** is this one company with a stronger case than any single thesis, such as "the independent attestation layer for AI-operated businesses"? **Answer: no. The merge is weaker than its parts.**

**Why the convergence happened.** Round 21's lesson applies: when an idea surfaces independently many times, the pain is real *and* a horizontal incumbent already exists. Here the stack is filled from top to bottom:

| Layer of "attestation for AI-run businesses" | Owner, as of Oct 2026 |
|---|---|
| Standard + independent audit + quarterly re-test + insurance | **AIUC** ($40M A on Sep 15 2026, $55M total; AIUC-1; Schellman as auditor; customers include Cursor, Harvey, Fin, UiPath, Lovable, KPMG) ([siliconangle](https://siliconangle.com/2026/09/15/ai-agent-certification-startup-aiuc-raises-40m-to-begin-auditing-frontier-models/)) |
| Continuous evidence *between* audits | **AgentStatus**, positioned explicitly as the AIUC-1 complement: daily outside-in tests from 800+ devices ([agentstatus.dev/aiuc](https://agentstatus.dev/aiuc)); Drata's AIUC-1 framework support |
| Performance verification + warranty | **Armilla** ($25M) |
| Trust centre / continuous control verification | **Vanta** ($4.15B), **Drata** |
| Software change-control evidence | **Kosli** (May 2026 AI-delivery launch, FINOS) |
| Licensed assurance opinion | **PwC "Assurance for AI"**, Deloitte, EY and KPMG frameworks ([techmarketview](https://www.techmarketview.com/ukhotviews/archive/2025/07/23/pwc-ups-the-ante-on-ai-assurance)) |
| Outside-in reliability score for insurers | **Parametrix** (AIG) |
| Tamper-evident agent "black box" log | Commoditized OSS: Aileron, AIR Blackbox, Forensa ([pypi.org/project/aileron](https://pypi.org/project/aileron/); [pkg.go.dev airblackbox](https://pkg.go.dev/github.com/airblackbox/gateway)) |
| Agent-to-agent agreement record | **DocuSign** MCP GA on Sep 30 2026 ("essential agreement layer for any agent platform") ([optionfinance.fr](https://www.optionfinance.fr/info-financiere-en-continu/d/2026-09-04-docusign-ouvre-son-serveur-mcp-aux-agents-dia.html)); Keelvar and Pactum native audit trails |
| Outcome verification for billing | Vendor self-verification: Zendesk "Verified Resolutions" (May 2026), Salesforce Help Agent (Jul 2026). T2 already killed. |

**Structural reasons the merge fails:**
1. **In attestation, the value is the signer, not the record.** A hash-chained log is free OSS. The scarce asset is a party whose signature counterparties accept: a licensed CPA, a standard-setter, or an insurer with capital. AIUC deliberately combined standard + auditor + insurer. A software startup without licensure or capital is a supplier *to* those signers, which is plumbing priced like AgentStatus, not a $10B company.
2. **Four different buyers.**
   - Undo / black box: the SRE.
   - Certified error rate: the COO.
   - Counter-signed deals: the supplier's CFO.
   - Verified uptime: the SaaS CFO/GC.

   Merging them multiplies pilot paths and buys only a bigger TAM story. Rounds 9 and 18 showed that ideas without one budget owner die.
3. **Third parties are not yet demanding it.** Across five rounds there is no documented case of a customer, insurer or auditor *rejecting* a vendor's own logs and requiring an independent record for agent operations. The only live demand loci (AIUC-1 insurance, DORA vendor evidence) already route to incumbents.
4. **The incentive conflict cuts against it.** The party that pays (the vendor) is the party an independent record exposes: claim denials under AI exclusions, SLA credits. Neutral records get built when a *consumer* with power mandates them, as carriers mandated EDR or regulators mandated flight recorders. No such mandate exists for agent operations.

**Merge score (best version, "attestation plumbing for certifiers and insurers"):** Pain 5, Urgency 4, ROI clarity 4, Customer accessibility 5, Pilot speed 5, Market size 7, Expansion 8, Venture potential 6, Defensibility 5, Why now 7, Competition position 3. **Average 5.4. KILL.**

**Tripwire to reopen any neutral-record thesis.** One of these must happen:
- a carrier, Lloyd's bulletin or regulator (ESAs/FCA) requires an *independent* record of agent production actions;
- a public dispute turns on whose agent logs are believed;
- AIUC or Armilla announces they will accept third-party continuous telemetry as underwriting input from a vendor *other than* their own partners.

---

## Implication for the founders

- This round produced no A and no new B.
- The kill pattern from STATUS.md held again, and faster than before:
  - Two of the three "uncovered" layers had funded or YC entrants launched in the last 90 days (Shepherd/Korso and Tether for H2; AgentStatus-plus-AIUC for continuous attestation).
  - The third (Undo Graph) has no direct competitor but is feature-sized, and there is no public evidence of how often the problem occurs.
- **Recommendation:** the cheapest, highest-information action is still the round-20 counter-signature 14-day test. Adjust its kill criteria to include "DocuSign agent MCP is used for supplier agent commitments".
