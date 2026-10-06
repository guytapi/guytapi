# Round 17: Analyst-category mining (2026-10-06)

**Method.** I mined 2026 analyst outputs for B2B categories at the "innovation trigger" stage, then checked vendor counts and funding for each. Sources: Gartner Hype Cycles 2026, Gartner Market Guides, Gartner Top Strategic Technology Trends, Forrester Waves and Landscapes 2026, and the CB Insights AI 100 2026.
- **Filter:** at most 3 meaningfully funded vendors, real buyer demand today, not on the STATUS.md killed list, and no excluded buyer types.
- **Search budget:** 33 WebSearch calls. WebFetch and Reddit were not used.
- **Source tags:**
  - [S]: the URL appeared in a search result.
  - [K]: a fact from my background knowledge that I did not re-verify this round.
  - [I]: my inference.
  - [U]: unverified, or my own estimate.

## Verdict up front

**Nothing clears the bar.** Analyst categories turn out to be lagging indicators. When Gartner or Forrester names a category, it already has its funded vendors, because Gartner needs sample vendors to name one. Of the 33 categories below:
- 25 fail on crowding or overlap with an earlier kill.
- 5 are pre-demand or not venture-scale.
- Only 2 pass the "≤3 meaningfully funded pure-play vendors" filter. Both are weak on demand or ROI:
  1. **Capture-time provenance for payment-triggering evidence (manufacturer warranty / service networks)**, from Gartner's "Digital provenance" trend: **6.5** on the original bar.
  2. **Data-contract enforcement for agent-written changes**, from Gartner's Innovation Trigger profile "Data contracts": **5.8** on the original bar.

**Gartner Top Strategic Technology Trends 2027 is not out yet.** Gartner session pages show it being unveiled at Symposium, which starts Oct 20, 2026 ([S] https://www.gartner.com/en/conferences/na/symposium-us/sessions/detail/4761465-Signature-Series-Top-Strategic-Technology-Trends-for-2027). **Recommendation:** re-run this filter in about 3 weeks against that list. Do not expect a different outcome, for the structural reason above.

**New lesson (round 17):** an analyst "Innovation Trigger" label does not mean a category is uncrowded. Gartner profiles need sample vendors, so by publication 5-10 funded companies usually exist. In this round the Innovation Trigger profiles split into three groups:
- Agent-control layers that are already crowded: guardian agents, agentic AI security/governance, IVIP/ISPM, agentic coding security.
- Research-stage items that are pre-demand: swarm intelligence, neurosymbolic agents, AI-to-AI negotiation.
- Dull data plumbing where platforms own the native version: data contracts, data agents.

---

## 1. Category table (33 named categories)

Vendor and funding notes come from search results [S] unless tagged otherwise. "Pass?" means: at most 3 meaningfully funded vendors, demand today, and not killed.

| # | Category (as named by analyst) | Source | URL | Vendors / funding seen | Pass? |
|---|---|---|---|---|---|
| 1 | Guardian agents | Gartner, inaugural Market Guide for Guardian Agents (Feb 25, 2026) | https://thehackernews.com/2026/03/5-learnings-from-first-ever-gartner.html [S] | Astrix, Cato Networks, Polygraf AI, Orchid named as representative vendors [S]; Zenity, Credal, Runlayer [K] | No: crowded; overlaps H/F kills |
| 2 | Agentic AI governance | Gartner Hype Cycle for Agentic AI 2026 (inaugural, 30+ profiles) | https://www.gartner.com/en/articles/hype-cycle-for-agentic-ai [S] | Zenity (named in 2 categories) [S]; ServiceNow AI Control Tower, Credal [K] | No: killed (H, X) |
| 3 | Agentic AI security | Same | https://www.businesswire.com/news/home/20260415309905/en/Zenity-Named-in-Two-Categories-in-the-2026-Gartner-Hype-Cycle-for-Agentic-AI [S] | Straiker $85M total, NeuralTrust $20M, CodeIntegrity $5.25M [S]; Noma, Zenity [K] | No: crowded |
| 4 | FinOps for agentic AI | Same | https://www.gartner.com/en/articles/hype-cycle-for-agentic-ai [S] | Vantage, Ramp, native caps [K] | No: killed (B) |
| 5 | AI-to-AI negotiation | Agentic AI HC 2026, Innovation Trigger | https://tray.ai/blog/gartner-agentic-ai-hype-cycle-2026/ [S] | Pactum, Fairmarkit [K] | No: killed (N); 5-10 yrs to mainstream |
| 6 | Swarm intelligence | Same | https://tray.ai/blog/gartner-agentic-ai-hype-cycle-2026/ [S] | Research stage [I] | No: pre-demand |
| 7 | Neurosymbolic AI agents | Same | https://tray.ai/blog/gartner-agentic-ai-hype-cycle-2026/ [S] | Research stage; Harmonic/Axiom adjacent [K] | No: pre-demand; W kill |
| 8 | AI agent management platforms (rated Transformational) | Gartner HC for Platform Engineering 2026 | https://www.truefoundry.com/blog/decoding-the-gartner-hype-cycle-for-platform-engineering-2026 [S] | Hyperscalers, UiPath, ServiceNow, Salesforce [K] | No: crowded |
| 9 | GenAI model routers / AI gateways | Same | https://truefoundry.com/gartner-2026-hype-cycle-for-platform-engineering [S] | TrueFoundry [S]; OpenRouter, Portkey, Kong, Cloudflare [K] | No: crowded |
| 10 | Multi-agent systems for procurement (Innovation Trigger, 2-5 yrs) | Gartner HC for Procurement & Sourcing Solutions 2026 | https://digitalterminal.in/tech-companies/procol-earns-gartner-hype-cycle-2026-recognition-for-agentic-ai-in-procurement [S] | Procol, Levelpath [S]; Zip, Globality, Fairmarkit, Pactum [K] | No: crowded |
| 11 | Context graphs (new 2026 profile in 6 HCs, <1% penetration) | Gartner 2026 HCs via Atlan analysis | https://atlan.com/context-and-chaos/issue/gartner-hype-cycles-2026-nobody-owns-context/ [S] | Jedify $24M A, Interloom €14.2M seed, Tribal $10M seed (Team8), Trace $3M (YC) [S]; Glean, Atlan [K] | No: >3 funded; VC-hyped ("trillion-dollar") |
| 12 | Data contracts (Innovation Trigger) | Same; Gartner HC for D&A Governance 2026 | https://www.gartner.com/en/documents/7957473 [S] | Gable $27M total (Series A Mar 2025) [S]; dbt model contracts, Soda, Acceldata, Monte Carlo features [K/S] | **Partial: 1 pure-play** → candidate #2 |
| 13 | Data agents (Innovation Trigger) | Atlan analysis of 2026 HCs | https://contextandchaos.substack.com/p/gartner-hype-cycles-2026-nobody-owns [S] | Snowflake, Databricks, Hex native [K] | No: platform-native |
| 14 | MCP / context engineering (at Peak) | Same | https://atlan.com/context-and-chaos/issue/gartner-hype-cycles-2026-nobody-owns-context/ [S] | Dozens [K] | No |
| 15 | AI SOC agents (moved Trigger → Peak; 1-5% penetration) | Gartner HC for Security Operations 2026 | https://www.dropzone.ai/blog/gartner-hype-cycle-security-operations-2026 [S] | Dropzone, Simbian [S]; Prophet, 7AI, Torq [K] | No: crowded |
| 16 | Identity Visibility & Intelligence Platforms (IVIP), Innovation Trigger | Gartner HC for Digital Identity 2026 | https://silverfort.com/blog/3-takeaways-from-the-2026-gartner-hype-cycle-for-digital-identity/ [S] | Axonius, AuthMind [S]; Radiant Logic [S]; Veza, Orchid [K] | No: crowded |
| 17 | Identity Security Posture Management (ISPM), Innovation Trigger | Same | https://silverfort.com/blog/3-takeaways-from-the-2026-gartner-hype-cycle-for-digital-identity/ [S] | Silverfort, Oasis, Astrix, Veza [K] | No: crowded |
| 18 | AI agent identity / credentialing | Gartner Digital Identity HC 2026; CB Insights AI 100 2026 cohort | https://www.cbinsights.com/research/report/artificial-intelligence-top-startups-2026/ [S] | Astrix [S]; Aembit, Okta, Frontegg, WorkOS [K] | No: killed (T4) |
| 19 | Agentic coding security (High benefit, Emerging) | Gartner HC for Secure Software Engineering 2026 | https://www.arnica.io/blog/arnica-gartner-hype-cycle-secure-software-engineering [S] | HiddenLayer $100M B (Sep 2026), Neo Security $100M (a16z/BVP), Straiker, DryRun $8.7M seed [S]; Endor, Arnica [S] | No: crowded |
| 20 | Bot and agent trust management (renamed from bot mgmt) | Forrester Wave Q2 2026 | https://datadome.co/agent-trust-management/the-forrester-wave-bot-and-agent-trust-management-software-key-findings/ [S] | DataDome, HUMAN, Kasada, Arkose, CHEQ, Netacea, hCaptcha, Google [S] | No: 8 vendors; Z kill |
| 21 | Agentic development platforms | Forrester Landscape Q3 2026 (launch) | https://www.forrester.com/blogs/launching-the-agentic-development-platforms-vendor-landscape-q3-2026/ [S] | Cursor, GitHub, Cognition, etc. [K] | No: excluded (coding agents) |
| 22 | Proactive security platforms (ASM+UVM merge) | Forrester Wave Q3 2026 (first under this name) | https://www.forrester.com/blogs/announcing-the-forrester-wave-proactive-security-platforms-q3-2026/ [S] | Tenable, Rapid7, Horizon3, XBOW [K] | No: killed (AA) |
| 23 | Marketplace platforms for physical goods / digital services | Forrester, two Landscapes 2026 | https://www.forrester.com/blogs/marketplace-platforms-arent-one-market-anymore-announcing-forresters-two-landscapes-for-2026/ [S] | Mirakl, VTEX, Arcadier [K] | No: crowded |
| 24 | Risk consulting services | Forrester inaugural Landscape Q3 2026 | https://www.forrester.com/blogs/announcing-the-inaugural-risk-consulting-services-landscape-q3-2026/ [S] | Big 4, Protiviti [K] | No: services, not venture |
| 25 | Physical AI (new standalone category, 11 cos) | CB Insights AI 100 2026 | https://www.cbinsights.com/research/report/artificial-intelligence-top-startups-2026/ [S] | 11 AI-100 companies [S] | No: crowded; R/R1 kills |
| 26 | Digital provenance | Gartner Top 10 Strategic Tech Trends 2026 | https://truescreen.io/articles/digital-provenance-gartner-top-10-trends-2026/ [S] | Capture side: Truepic $36M total (insurance/lending focus) [S], TrueScreen $2.7M [S]. Detection side crowded: Reality Defender, OPSWAT, Shift, Claimlane, Delos, SymphonyAI [S/K] | **Partial: capture side ≤3 funded** → candidate #1 |
| 27 | Preemptive cybersecurity | Gartner Top Trends 2026 | https://nationalcioreview.com/articles-insights/live-from-gartner-2026-tech-trends-are-here/ [S] | Morphisec, Palo Alto, CrowdStrike [K] | No: crowded |
| 28 | Geopatriation | Gartner Top Trends 2026 [K] | https://nationalcioreview.com/articles-insights/live-from-gartner-2026-tech-trends-are-here/ [S] (list not re-verified) | Sovereign clouds give migration away [I] | No: round-15 sovereignty kill; destination subsidy |
| 29 | Confidential computing | Gartner Top Trends 2026 [K] | same [S] | Fortanix, Anjuna, Opaque, Edgeless; going native in clouds [K] | No: crowded; I-kill (TEE native) |
| 30 | Domain-specific language models | Gartner Top Trends 2026 [K] | same [S] | Hundreds [K] | No |
| 31 | AI-native software engineering | Gartner HC for AI & Cloud Platform Services 2026 | https://www.gartner.com/en/documents/7997669 [S] | Crowded [K] | No: excluded |
| 32 | Data center infrastructure (AI-enabled, modular) | Gartner HC for Data Center Infrastructure Technologies 2026 (Jun 9) | https://www.gartner.com/en/documents/7973637 [S] | Profiles not visible in search [U] | No: R2/S/E1 kills |
| 33 | Top Strategic Technology Trends 2027 | Gartner (unveiled at Symposium from Oct 20, 2026) | https://www.gartner.com/en/conferences/na/symposium-us/sessions/detail/4761465-Signature-Series-Top-Strategic-Technology-Trends-for-2027 [S] | Not released | Re-check after Oct 20 |

Also seen but not profiled in detail:
- Gartner Hype Cycle for Emerging Technologies 2026 (Jul 23; 30 technologies; four themes: autonomous business, hypermachinity, augmented humanity, techno-societal fragility): https://www.gartner.com/en/documents/8163629 [S]
- Gartner Hype Cycle for AI 2026 (Aug 28; AI-ready data at the Peak): https://www.gartner.com/en/documents/8319853 [S]

The individual Innovation Trigger profile lists in these reports are paywalled and did not show up in search results.

---

## 2. Candidate #1: Capture-time provenance for payment-triggering evidence

**One sentence for a VC:** "Every warranty claim, field-service job and B2B refund is paid on a photo that GenAI can now fake in seconds. We put a cryptographic chain of custody on that photo at capture and flag reused or synthetic evidence across a manufacturer's whole dealer and service network."

Fields follow the round-7 METHOD template.

- **Problem.** Manufacturers and service networks pay on photo evidence: a warranty claim photo, a technician's proof of repair, a dealer's damage photo. Generative AI made that evidence free to forge, and after-the-fact detection is an arms race.
- **Recent evidence:**
  - Warranty fraud is 3-10% of claims, about $45B/yr for US brands (Claimlane: https://www.claimlane.com/resources/blog/warranty-fraud-explained [S]).
  - Warranty claims cost manufacturers 2.5-4.8% of revenue, with 3-15% fraudulent (Delos: https://delos.so/blog/ai-powered-warranty-management [S]).
  - AI-generated fake receipts went from 0% to 70.8% of flagged fraud documents in 14 months (cited in the same result set [S]; original source unverified [U]).
  - AI-image refund fraud on Vinted, Amazon and Fnac (OECD.AI incident, Mar 2026: https://oecd.ai/en/incidents/2026-03-02-16b3 [S]).
  - Debevoise on AI-generated images in claims "and other frauds" (Jan 2026: https://www.debevoise.com/insights/publications/2026/01/use-of-ai-generated-images-for-fake-insurance [S]).
  - Gartner names digital provenance a 2026 top trend (https://truescreen.io/articles/digital-provenance-gartner-top-10-trends-2026/ [S]).
- **Who has the pain.** Warranty and after-sales VPs at durable-goods, auto/powersports, HVAC and appliance OEMs. Facility-management firms paying subcontractors on photo proof (round-16 T4). Insurers are out of scope (excluded buyer).
- **What they do today.** Manual adjuster review and parts-return requirements. Dealer audits. Newer AI detection add-ons inside warranty software: Tavant, SymphonyAI warranty agent, Delos, ServiceCPQ, Claimlane [S].
- **Why current products fail.** Detection-after-upload is probabilistic, and accuracy degrades with each new model [I]. Truepic's capture-side product is aimed at insurance and lending (its customers include Equifax, TransUnion and Palomar) [S]. Nobody holds a cross-OEM view of reused images or serial-fraud technicians [I].
- **Why now.** Image-gen quality reached forensic-proof level in 2025-26. C2PA content credentials are shipping in phone cameras [K]. Gartner's provenance trend gives CIOs cover to fund it.
- **Potential product.** A capture SDK for the dealer and technician apps: signed photo plus device, GPS and time attestation. A verification API at claim intake. A cross-network hash graph of reused images and devices (Vara's AML network analytics and device biometrics fit here).
- **Time to value.** About 2 weeks for back-testing historical claims with hash and duplicate analysis. Capture-SDK rollout across a dealer network takes months.
- **Pilot (14-30 days).** Back-test 12 months of one OEM's claim photos and quantify duplicate or synthetic rates and dollars.
- **Willingness to pay.** At 1% recovery of a $50M warranty spend, the program saves $500K/yr, so an ACV of $100-250K is defensible [U].
- **Expansion.** Warranty → field service → B2B returns → FM subcontractors → logistics proof-of-delivery.
- **Competition.** Warranty-software incumbents (Tavant, PTC/Syncron, SAP) bolt on AI detection. Truepic could re-point at OEMs. Fraud vendors (Shift, OPSWAT) cover claims [S/K].
- **Moat:**
  - At 10 customers: the back-test data asset.
  - At 100: a cross-OEM technician/device fraud graph, the shared-data network pattern that survives where buyers are concentrated (round-16 lesson). Dealers serve many OEMs.
  - At 1,000: a standard capture SDK embedded in dealer management systems.
- **CTO test sentence.** "Would you require signed capture in your dealer app if it cut warranty fraud payouts by 1%?"
- **Kill test question.** Does a top-20 OEM's back-test show ≥2% of claim dollars on duplicate or synthetic evidence? If not, the problem is fraud-team noise.

**METHOD scores (1-10):**

| Pain | Urgency | Market timing | Speed to pilot | Ease of integration | Ease of reaching customers | WTP | Competition | Moat | Market size | VC attractiveness | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 6 | 8 | 7 | 5 | 5 | 7 | 6 | 7 | 6 | 6 | **6.4** |

**Original bar scores:**

| Pain | Urgency | ROI clarity | Customer accessibility | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 6 | 7 | 5 | 7 | 6 | 7 | 6 | 7 | 8 | 6 | **6.5** |

**Fails:** urgency, accessibility, market size, venture potential and competition position are all below 7.

**Buyers × ACV [U]:**
- About 1,500 OEMs worldwide with warranty spend >$20M × $150K = **~$225M**.
- Plus about 2,000 FM/service networks × $50K = $100M.
- **SAM ≈ $325M.** This is venture-possible only with the cross-network graph and expansion into logistics and returns.

---

## 3. Candidate #2: Data-contract enforcement for agent-written changes

**One sentence for a VC:** "Coding agents now ship schema changes faster than data teams can review them. We block the PR that builds fine but silently breaks a downstream dashboard, model or agent."

Fields follow the round-7 METHOD template.

- **Problem.** Agents and humans change upstream schemas. Contracts exist only as documentation. The dangerous change compiles and quietly breaks consumers.
- **Recent evidence:**
  - arXiv 2602.02335, "Correct-by-design lakehouse... for humans and agents" (https://arxiv.org/pdf/2602.02335 [S]).
  - dev.to on schema boundaries for AI agents (https://dev.to/gyu07/designing-schema-boundaries-for-ai-agents-1cjo [S]).
  - Acceldata on contracts that exist only as documentation (https://www.acceldata.io/blog/real-time-schema-change-tracking-tools-that-actually-enforce-data-contracts [S]).
  - Data Engineering Digest, Feb 2026 [S].
  - Gartner places data contracts at the Innovation Trigger (Atlan [S]).
- **Who has the pain.** Data platform leads at companies with 20+ data engineers.
- **What they do today.** dbt model contracts, CI schema checks, Great Expectations/Soda tests, Slack "heads up" messages.
- **Why current products fail.** Checks are per-tool. No cross-repo lineage judges the producer's PR against all consumers [S/I].
- **Why now.** Agent-authored PR volume (Vercel >50% of deploys by agents, from round 15).
- **Product.** A GitHub app plus lineage graph that comments on and blocks producer PRs that break registered consumers.
- **Time to value.** 1 day in CI.
- **Pilot.** Replay 90 days of merged PRs and count the incidents it would have caught.
- **WTP.** $30-80K [U].
- **Expansion.** Agent tool contracts (MCP schemas) and API contracts.
- **Competition.** Gable ($27M, Databricks Ventures) [S]. dbt Labs, Monte Carlo, Acceldata and Soda are one feature away [K/S]. A platform team can build 70% of it in a sprint (round-8 lesson).
- **Moat.** Weak; lineage is commoditizing.
- **CTO test sentence.** "Would you pay $50K to auto-block producer PRs that break downstream consumers?"
- **Kill test question.** Do 3 of 5 data leads name an agent-caused schema incident in the last quarter with a cost of more than $20K?

**METHOD scores:**

| Pain | Urgency | Market timing | Speed to pilot | Ease of integration | Ease of reaching customers | WTP | Competition | Moat | Market size | VC attractiveness | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 5 | 7 | 8 | 8 | 7 | 5 | 5 | 4 | 6 | 5 | **6.0** |

**Original bar scores:**

| Pain | Urgency | ROI clarity | Customer accessibility | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 5 | 5 | 7 | 8 | 6 | 6 | 5 | 4 | 7 | 5 | **5.8** |


**Fails:** pain, urgency, ROI, market size, venture potential, defensibility and competition position.

**Buyers × ACV [U]:** about 8,000 companies with 20+ data engineers × $50K = **~$400M SAM**, sharply capped by native dbt/Snowflake/Databricks features.

---

## 4. Recommendation

- **Stop using analyst reports as an idea source.** They confirm the round-1 to round-16 pattern: by the time a category is named, it is funded.
- **The only useful output** is candidate #1, a provenance/fraud-graph play that fits Vara's stack and extends round-16 T4. It remains a 14-day back-test idea, not a winner: get 12 months of claim photos from one OEM or FM firm and pass only if ≥2% of claim dollars sit on duplicate or synthetic evidence.
- **Re-check Gartner's 2027 trends** after Oct 20, 2026.
