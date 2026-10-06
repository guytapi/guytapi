# Round 28 · H3 (incidents in code no human understands): skeptical VC partner view

Date: 2026-10-06. Role: a skeptical seed partner asking where the money is once most production systems are written and operated by agents. I ran 25 web searches; the turn-wide search budget ran out after that (limit shared by all agents), so a few points below are marked **[unverified]**. Every URL cited was returned by a search; none was fetched (WebFetch is blocked).

---

## 0. Verdict first

- **The obvious H3 products are taken or being absorbed.** These are AI SRE/RCA, change provenance ("which lines did the agent write"), pre-deploy change-risk gates, and agent-action evidence for compliance. The buyers are Datadog, PagerDuty, ServiceNow, Drata, OpenAI/Cursor, and a set of funded startups.
- **The one layer I would consider leading** is a **neutral reliability attestation network**. It is a third-party-verified record of operational control and SLA performance. The SaaS vendor publishes it, and its *customers, insurers and auditors* consume it. In practice it is SOC 2 plus a credit rating for "is this agent-run software under control?", with SLA-credit settlement as the 30-day wedge.
- **Honest score: 6.4 → outcome B (weak/conditional), not A.** It is not a Datadog feature, because the people who consume the output are people who will not trust the vendor's own observability tool. But Parametrix (outside-in monitoring of ~9,000 tech providers for AIG) and Drata/Vanta (trust centers, agent-evidence feeds) sit on both flanks.

---

## 1. Pushing H3 to 2028-2029

**Base state.** Most production changes are agent-authored. Remediation is increasingly agent-executed: ServiceNow's AI Specialist executes low-risk changes, and Datadog Bits SRE plus Bits Release validates and rolls out changes. Humans set policy and approve the top risk tier.

**First-order consequence: slower diagnosis and no owner.** Already served: Resolve AI ($1B+ valuation), Traversal (~$303M valuation, Amex Ventures strategic investment Mar 2026), incident.io AI SRE, PagerDuty AI Agent Suite, Datadog Bits AI SRE. This is the public decoy; don't fund it.

**Second-order consequences, which are where the money moves.**
1. **Change failure rate rises with throughput.** DORA 2025 found that AI adoption correlates with higher instability. Amazon's March 2026 six-hour retail outage was linked internally to "Gen-AI assisted changes" with "high blast radius", and Amazon now requires senior sign-off on AI-assisted changes. Amazon disputes that AI was the cause. More incidents means more SLA breaches.
2. **SLA credits become a real P&L line, while the credits themselves stay tiny next to customer losses.** Typical enterprise terms pay 10–25% of monthly fees per violation hour. Credits reportedly cover about 8% of customer losses. Both figures come from vendor blogs, so treat them as directional. The gap pushes customers toward contractual remedies and insurance.
3. **Insurers stop silently covering AI.** Verisk/ISO GenAI exclusions took effect Jan 1 2026, with 2,369 exclusion filings across 49 states by mid-2026. W.R. Berkley has an absolute AI exclusion across D&O, E&O and fiduciary lines. Some carriers apply AI sublimits of about 10% of cyber limits (CSA research note, Aug 30 2026). For a SaaS vendor, the hidden risk is that the tech E&O policy that pays customer claims after an outage may not pay if the outage "arose from AI".
4. **Insurers price downtime from the outside.** AIG and Parametrix launched parametric cloud-outage cover (Aug 2026), backed by monitoring of more than 750 data centers and more than 9,000 software providers. Mantas raised $1.77M (Jan 2026) for parametric cloud-downtime insurance. Insurers are already building a reliability score for each vendor. They build it outside-in, without the vendor's internal evidence.
5. **Auditors and boards want control evidence.** COSO published "Achieving Effective Internal Control Over Generative AI" on Feb 23 2026, which expects evidence of human review and logged model/config versions. Under SOC 2 change management, auditors treat an agent acting on a developer's credentials as the same principal as the developer, so it gives no segregation of duties. An agent-operated pipeline that cannot show a distinct human authorizer breaks the change-management control.

**Third-order consequence: who is allowed to sell software to a regulated enterprise.** Procurement stops asking "do you have SOC 2?" and starts asking for *continuous, verifiable proof that agent-operated production is under control*, plus a reliability record they can price. Procurement already runs AI-specific security reviews (the "80-question wall"), but today those questions cover AI *in* the product, not AI *running* the product. That gap is the whitespace, and it is also why demand is still early.

---

## 2. Where the money is (ranked)

| Money pool | Who pays | Size signal | Who owns it today |
|---|---|---|---|
| Faster incident resolution (MTTR) | VP Eng/SRE | Large, proven | Datadog, PagerDuty, incident.io, Resolve, Traversal, Cleric (**taken**) |
| Preventing bad agent changes | VP Eng/Platform | Large | Datadog Bits Release, ServiceNow autonomous change + risk scoring, Harness/LaunchDarkly guarded rollouts **[unverified 2026 specifics]** (**absorbing**) |
| Attributing code to agents | Eng/security | Small alone | Cursor Agent Trace spec (backed by Cognition, Cloudflare, Vercel, Google Jules), Git AI (team joined OpenAI), Exceeds (**commoditized**) |
| Compliance evidence for agent actions | CISO/GRC | Medium | Drata AI Agent Governance (Aug 4 2026, tamper-evident evidence feed), Kosli ($10M A, Deutsche Bank), Vanta agent (**absorbing**) |
| AI-agent certification and insurance | AI app vendors | Growing | AIUC ($55M total, $40M A Sep 15 2026, AIUC-1; customers include Cursor, Lovable, Harvey) |
| Downtime insurance pricing | Insurers / insureds | Growing | Parametrix + AIG, Mantas (outside-in only) |
| **Third-party-verified reliability and control record that customers and insurers can rely on, plus SLA settlement** | SaaS vendor (CFO/GC + VP Eng), paid because customers and insurers demand it | Unproven | **No clear owner found** (but see threats) |

The last row is the only one where I could not find an owner within 25 searches. It also has the least evidence of demand.

---

## 3. The thesis

### Thesis H3-VC: "Verified Uptime": a neutral reliability-and-control attestation network for agent-operated software

**One-line problem.** When agents write and operate production, a SaaS vendor's customers, insurers and auditors can no longer accept "trust our SRE team". The vendor has no independent, verifiable way to prove its operational control and SLA record, so it loses deals, pays credits it can't dispute, and carries uninsured AI-outage exposure.

**Why this exists now.**
- Agent-authored and agent-executed production changes became normal in 2026: Datadog Bits Release, ServiceNow autonomous changes, Amazon's sign-off policy.
- DORA 2025 links AI adoption to higher change failure.
- The insurance "silent AI" era ended in 2026 (ISO exclusions, Berkley absolute exclusion, AI sublimits). Parametric downtime products now score SaaS vendors from outside.
- COSO's Feb 2026 GenAI control guidance and SOC 2 segregation-of-duties expectations make "who authorized this agent change" an audit question.
- Twelve months ago none of these were true together.

**Exact buyer.** The CFO or General Counsel holds the budget for contract, insurance and SLA exposure. The champion is the VP Engineering or Head of SRE, who has to produce the evidence. The economic trigger is an enterprise deal or renewal that asks for reliability evidence, or a cyber/E&O renewal with AI exclusions.

**Exact ICP.**
- B2B SaaS / infrastructure API companies with $20M–$500M ARR, enterprise contracts with financially backed SLAs (99.9%+), and regulated customers (financial services under EU DORA, healthcare).
- More than 30% agent-authored changes, plus at least one AI SRE or auto-remediation agent with production write access.
- Examples: payments/fintech infrastructure, data infrastructure, communications APIs.

**Current workaround.**
- Customers get a status page, which the vendor controls and which is often under-reported, plus a SOC 2 Type II report that is up to 12 months stale.
- SLA credits are computed by hand from the vendor's own metrics after the customer files a claim.
- Insurers rely on annual questionnaires and outside-in scans such as Parametrix.
- Vendors answer "how do you control AI-generated changes?" with a policy PDF.
- Inside the vendor, Datadog/incident.io hold the truth, but nobody outside the company can verify it.

**Why incumbents cannot easily own it.**
- **Conflict of interest.** Datadog/PagerDuty/incident.io are the vendor's own tools, and increasingly they *operate* the changes (Bits SRE, Bits Release). A tool that operated the change cannot credibly certify the change was under control. That is the auditor-independence logic, and it is the main argument against "it's a Datadog feature".
- **Cross-vendor comparability.** Insurers and procurement need the same score across thousands of vendors whatever their observability stack. Datadog sees only its own customers.
- **Inside-out vs outside-in.** Parametrix sees only external availability. It cannot see change authorization, agent vs human authorship, or near-misses.
- **Drata/Vanta** own trust centers and now agent-evidence feeds, but they attest *security* controls from GRC integrations. They lack SLO-grade telemetry and contract-level SLA computation. This is the weakest moat argument, because they are one acquisition away.

**30-day MVP.**
1. Read-only connectors: deploy/change sources (GitHub, Argo/Spinnaker, feature flags, Terraform), agent attribution (Agent Trace / Git AI notes), incident tool (PagerDuty/incident.io), SLO source (Datadog/Prometheus).
2. A tamper-evident ledger per incident: changes in the blast radius, author type (agent/human/mixed), the human authorizer distinct from the proposer, which guardrail fired, and time to mitigate.
3. A contract parser: upload enterprise MSAs, extract SLA terms, and compute *per-customer* SLA impact and credits owed, both paid and disputed.
4. A customer-facing "verified reliability" page: SLO attainment, change-control coverage (% of agent changes with distinct human authorization or policy-tier approval), and incident dossiers, signed by the neutral party.

**Pilot design.** 2–3 design partners. Back-fill 12 months of incidents and changes.

Pass if:
- (a) The SLA computation finds ≥$250K of credits that were miscounted, owed but unpaid (a risk), or overpaid.
- (b) At least one enterprise customer or prospect accepts the verified page in place of a custom reliability questionnaire.
- (c) The vendor's broker or carrier agrees to look at it at renewal.

Fail if no partner's CFO/GC engages within 14 days.

**Pricing hypothesis.**
- Platform fee: $40K–$150K/yr, scaled by ARR or contract count.
- Network side, later: free for consuming customers; insurers pay per-vendor data access, or there is a revenue share on parametric/E&O products underwritten on the data, which is the capital-light MGA route.

**Expansion path.**
1. SLA ledger and incident dossiers.
2. Continuous "verified control" attestation (partner CPA firms sign SOC 2 / ISAE-style reports using the ledger).
3. A reliability score consumed by procurement and TPRM platforms.
4. Underwriting data for downtime/E&O carriers, with SLA-credit-backed insurance.
5. Settlement rail: automatic, contract-true SLA credits between vendor and customer.

**Moat.**
- Two-sided network: each vendor's attestation is consumed by many customers, and each customer pushes many vendors to join. That is the SOC 2 / trust-center flywheel.
- A proprietary dataset linking change provenance and authorization to incidents, losses and claims, which is exactly what insurers lack.
- Neutrality as a brand asset: incumbents that operate production cannot credibly claim it.

**Why it could become $10B+.** It is not a monitoring tool. It is the **trust layer that decides which agent-run software enterprises can buy and insurers can cover.** Revenue pools:
- Attestation, the SOC 2 economy. Vanta is reportedly valued at ~$4B **[unverified, from memory]**.
- Ratings, the Bitsight/SecurityScorecard model, applied to operations instead of security.
- Insurance distribution and settlement on the downtime/E&O market, which AIG and Parametrix are only now productizing.

If agent-run software produces more incidents while insurers exclude AI by default, the party with verified inside-out control data becomes the underwriting standard. That is the $10B path. It depends heavily on insurers and procurement actually adopting a neutral standard (AIUC-1 shows this can happen for AI agents).

**Direct competitors and adjacent threats.**
- **Parametrix** (monitors 9,000+ tech providers for AIG parametric cover). This is the most dangerous threat: it already owns the insurer relationship and could add inside-out data via vendor opt-in.
- **Drata AI Agent Governance** (tamper-evident agent evidence feed, Aug 2026), plus the Vanta agent and trust centers. They could add SLO and incident attestation.
- **AIUC** (AIUC-1 standard, insurance, $55M raised). It could extend from "AI agent product" certification to "agent-operated infrastructure" certification.
- **Kosli** (change governance and audit trails for regulated delivery, Deutsche Bank-backed). It is the closest on change evidence.
- **Datadog** (Bits Release / Bits SRE). It could publish "verified SLO" reports for customers.
- incident.io / Atlassian Statuspage (customer-facing status). ServiceNow (change risk + AI Control Tower).
- Outside-in monitors (Catchpoint, ThousandEyes, StatusGator/IsDown) **[2026 moves unverified]**.
- Bitsight / SecurityScorecard adding resilience ratings **[unverified]**.

**One sentence to the CFO.** "Your agents now ship and fix most of production, and your insurer just excluded AI-caused losses; we give your customers, auditors and carrier one independently verified record of your uptime and change control, and we reconcile every SLA credit to the contract."

**Hard kill criteria.**
1. Two of three design partners' CFO/GC won't engage. That would mean the pain sits with engineering only, which is the generic-observability failure mode.
2. No enterprise buyer or prospect will accept a third-party page in place of their own questionnaire within the pilot.
3. Brokers/carriers say they will not credit inside-out data at renewal, or Parametrix announces vendor opt-in data.
4. Drata/Vanta/Datadog ships customer-facing verified SLO/change-control attestation before we have 10 vendors live.
5. The SLA back-test finds less than $100K of discrepancy per partner, so there is no ROI hook.

**Scores (1–10, honest).**

| Criterion | Score | Why |
|---|---|---|
| Pain | 6 | Real (credits, exclusions, audit gaps), but felt in pieces across the CFO, GC and SRE; no proof yet that anyone is losing deals over it |
| Urgency | 5 | The insurance exclusion wave is real, but outage-related tech E&O claim denials are not yet documented; procurement asks about AI *in* products, not AI *running* products |
| ROI clarity | 6 | SLA-credit reconciliation is concrete; deal velocity and premiums are speculative |
| Customer accessibility | 6 | CFO/GC plus VP Eng is a two-buyer sale; reachable through brokers and auditors |
| Pilot speed | 7 | Read-only connectors plus a 12-month back-fill is doable in weeks |
| Market size | 7 | Attestation, ratings and insurance pools are large if the network forms |
| Expansion | 8 | Ledger → attestation → rating → underwriting → settlement |
| Venture potential | 7 | Rare two-sided, standard-setting shape; heavy dependence on insurer adoption |
| Defensibility | 6 | Network plus neutrality, but early on it is a ledger that Drata/Datadog could copy |
| Why now | 7 | 2026 exclusions, COSO guidance, Amazon's sign-off policy, DORA instability, parametric cover |
| Competition position | 5 | Flanked by Parametrix (insurer side), Drata/Vanta (attestation side), Datadog (data side), AIUC (standard side) |
| **Average** | **6.4** | Fails the A bar (≥8.5, none <7) |

**Classification: B (weak/conditional), roughly 10–15% odds that the precise test passes.** It qualifies as B because the third-order demand (customers and insurers demanding inside-out proof of control over agent-operated production) is plausibly 12–24 months early. The absence of a dedicated vendor is consistent with that, not proof the space is closed. It is not A, because neither urgency nor competition position reaches 7.

**14-day test (data, not interviews).**
1. Back-test 12 months of incidents and changes plus enterprise MSAs at two SaaS companies. Pass: ≥$250K of SLA discrepancy in total, and ≥40% of Sev1/2 incidents have an agent-authored or agent-executed change in the blast radius with no distinct human authorizer recorded.
2. Send a sample verified-reliability dossier to two cyber/tech-E&O brokers. Pass: one asks for it in a live renewal.
3. Put the page in one live enterprise security review. Pass: the reviewer accepts it in place of reliability questions.

All three must pass.

---

## 4. Partner memo: what would make me lead, what stops me

**What would make me lead the seed.**
- A founder with **insurance or audit DNA plus SRE credibility**, for example ex-Parametrix/Coalition/At-Bay underwriting paired with an ex-Stripe/Datadog reliability lead. The company wins on who trusts the record, not on code.
- One named carrier or MGA willing to use the data as an underwriting input (a letter of intent for a pilot), plus one Big-4/CPA firm willing to sign attestations on it. Those two endorsements make it a standard, not a tool.
- Evidence that a real tech E&O or cyber claim was denied or disputed because an outage "arose from AI". That single event would move urgency from 5 to 8.
- A back-test showing contract-true SLA discrepancies large enough (≥0.5% of ARR) that the CFO pays for the wedge even if the network never forms.

**What stops me.**
- **Parametrix is the natural owner.** It already scores 9,000+ tech providers for AIG. If it adds vendor opt-in internal data ("share your telemetry, get a better premium"), this thesis becomes a feature of its distribution.
- **Drata shipped a tamper-evident agent-evidence feed in Aug 2026**, and Vanta/Drata own the trust-center habit. A "verified SLO" widget is a quarter of work for them.
- **The answer to "why not a Datadog feature?" holds only if consumers insist on independence.** If enterprise buyers accept a Datadog-signed SLO report, as they accept AWS's own SLA dashboards, neutrality is worthless.
- **Two-buyer sale with no named victim.** Engineering feels MTTR pain and finance feels credit and insurance pain, but nobody owns "verifiable operational control" yet. Past rounds show that ideas without one budget owner die (round 9, H decision layer).
- **The insurance angle may cut the other way.** A precise ledger of "this outage came from an agent change" could *help* carriers deny claims under AI exclusions. GCs may refuse to create that record. This is a real adoption risk I could not resolve from desk research.
- Pattern from 27 rounds: "control/visibility over AI" layers get absorbed within about 6 months once visible. This one survives only because its consumers are external.

---

## 5. Directions considered and killed in this pass

| Direction | Why killed |
|---|---|
| AI SRE / agentic RCA for agent-written code | Resolve ($1B+), Traversal (~$303M, Amex), incident.io AI SRE, PagerDuty AI Agent Suite, Datadog Bits AI SRE, Cleric |
| Change provenance for incidents (the DISCOVERY_MACHINE prototype) | Cursor Agent Trace spec with broad backing; Git AI team joined OpenAI; Exceeds Ink; Datadog Bits Release validates change intent; feature-sized |
| Pre-deploy blast-radius gate for agent changes | Datadog Bits Release (staging checks, rollout monitoring), ServiceNow Now Assist change-risk scoring plus autonomous low-risk execution (Knowledge 2026); round-3 note already flagged it |
| Agent-change compliance evidence (SOC 2 / COSO) | Drata AI Agent Governance (Aug 2026), Kosli, Vanta agent |
| Insurance for AI-caused outages (carrier/MGA) | AIUC ($55M), AIG + Parametrix, Mantas; capital-heavy and outside founder edge |
| "Comprehension restoration" (explain agent-written code to on-call) | Generic context management, banned; Unblocked/DeepWiki-class tools |

---

## Sources (all from search results; none fetched)
- Amazon outages and senior sign-off: https://www.techradar.com/pro/amazon-is-making-even-senior-engineers-get-code-signed-off-following-multiple-recent-outages ; https://oecd.ai/en/incidents/2026-03-10-01aa
- DORA 2025 instability: https://redmonk.com/rstephens/2025/12/18/dora2025/ ; https://www.splunk.com/en_us/blog/learn/state-of-devops
- Datadog Bits AI SRE / Bits Release (DASH 2026): https://devops.com/datadog-leverages-ai-to-extend-observability-reach-deeper-into-devops-workflows/ ; https://itbrief.co.uk/story/datadog-unveils-new-bits-ai-agents-to-streamline-cloud-workflows
- PagerDuty AI Agent Suite: https://www.businesswire.com/news/home/20251008279706/en/PagerDuty-Launches-Industrys-First-End-to-End-AI-Agent-Suite-Slashing-Incident-Response-Times-and-Empowering-Teams-to-Innovate
- incident.io $62M B: https://techcrunch.com/2025/04/10/incident-io-raises-62m-at-a-400m-valuation-to-help-it-teams-move-fast-when-things-break
- Traversal / Amex Ventures: https://pulse2.com/traversal-ai-site-reliability-engineering-platform-receives-strategic-investment-from-amex-ventures/amp/ ; valuation figure from https://stockanalysis.com/private/traversal/ (snippet)
- Resolve AI unicorn: https://techcrunch.com/2025/12/19/ex-splunk-execs-startup-resolve-ai-hits-1-billion-valuation-with-series-a
- AIUC $40M A / AIUC-1: https://siliconangle.com/2026/09/15/ai-agent-certification-startup-aiuc-raises-40m-to-begin-auditing-frontier-models/
- Agent Trace: https://www.infoq.com/news/2026/02/agent-trace-cursor ; https://agent-trace.dev/
- Git AI → OpenAI: https://aicatchup.com/news/openai-welcomes-git-ai-agent-attribution ; https://usegitai.com/blog/introducing-git-ai
- Enterprise AI questionnaires: https://tianpan.co/blog/2026-04-27-80-question-wall-enterprise-ai-security-questionnaire
- SOC 2 segregation of duties with agents: https://zof.ai/blog/separation-of-duties-for-ai-agents-who-proposes-who-authorizes-who-is-accountable ; https://scalr.com/learning-center/can-ai-agents-change-infrastructure-and-stay-compliant
- SLA credit economics (vendor blogs, directional): https://www.softwareseni.com/calculating-the-true-cost-of-cloud-outages-and-downtime ; https://www.cloudnuro.ai/blog/saas-sla
- AIG + Parametrix parametric cloud outage cover: https://www.reinsurancene.ws/aig-parametrix-launch-cyber-parametric-solution-for-cloud-service-outage-losses/ ; https://www.insurtechinsights.com/aig-parametrix-launch-parametric-cover-for-cloud-outage-losses/
- Mantas: https://fintech.global/2026/01/27/mantas-raises-1-77m-to-bring-parametric-insurance-to-cloud-downtime/
- Kosli: https://www.startuplab.no/insights/in-the-news-kosli-raises-100-mnok-in-series-a
- ServiceNow autonomous change (Knowledge 2026): https://www.bluemantis.com/blog/beyond-chatbots-how-servicenow-now-assist-is-revolutionizing-it-change-management/ (snippet; specifics partly from search summary)
- ISO GenAI exclusions / exclusion wave: https://www.insurancebusinessmag.com/us/news/cyber/isos-generative-ai-exclusion-is-already-on-thousands-of-cgl-policies-589971.aspx ; https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-insurance-exclusion-wave-20260830-csa-s/ ; https://fenwick.com/insights/publications/end-silent-ai-emerging-ai-exclusions-coverage-fragmentation-and-practical-implications
- COSO GenAI guidance: https://dart.deloitte.com/USDART/home/publications/deloitte/heads-up/2026/coso-internal-controls-generative-ai
- Drata AI Agent Governance: https://drata.com/about/news/drata-extends-trust-management-platform-to-continuously-monitor-and-govern-ai-agents
- Cyber insurance questionnaires and AI code (blog-level evidence): https://www.cloudapper.ai/enterprise-ai/why-your-cyber-insurance-policy-may-not-cover-a-breach-caused-by-ai-generated-code/
