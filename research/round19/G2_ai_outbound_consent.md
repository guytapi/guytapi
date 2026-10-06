# G2: TCPA/consent compliance for AI outbound voice and SMS ("make AI outbound legally safe")

**Date:** 2026-10-06 | **Analyst stance:** skeptical red team | **Searches used:** 33 of 40 | **Verdict: KILL (avg 5.0/10)**

The thesis: "Millions of AI voice agents now place outbound calls and texts. Every one is a TCPA lawsuit waiting to happen. We sell the consent ledger, the real-time pre-dial gate and the litigation evidence ledger."

**Bottom line.** The litigation risk is real and growing. But the product is an extension of a 20-year-old, mostly bootstrapped compliance category, and in 2026 that category already moved to serve AI agents. DNC.com, PossibleNOW, Gryphon, ActiveProspect/Jornaya, Twilio, Microsoft, Saperly, Verfi and Blacklist Alliance (through Bland) all ship agent-facing compliance today. Several do it as MCP servers. The legal pressure is also *softening* in 2026, not tightening. The category leader in consent certificates certifies about 2.5B leads a year on an estimated ~$28M of revenue, which means the profit pool is small. Failure modes: **F2 (visible-pain race) + F4 (small TAM) + F1 (platform absorption).**

---

## 1. Evidence

### 1a. Litigation volume (real, but not specific to AI)
- WebRecon/TCPAWorld: **April 2026 had 330 TCPA cases, 255 of them class actions**, a monthly record and up about 40% year over year. Through May 2026: **1,072 class actions vs 850** in the same period of 2025 (+26%). [tcpaworld.com/2026/06/04/april-tcpa-filings-off-the-chart-...](https://tcpaworld.com/2026/06/04/april-tcpa-filings-off-the-chart-330-tcpa-cases-255-tcpa-class-actions-filed-in-april-2026-up-40-from-2025/), [tcpaworld.com/2026/07/06/heat-wave-...](https://tcpaworld.com/2026/07/06/heat-wave-tcpa-class-action-filings-continue-to-cook-the-nation-at-a-record-pace-as-summer-heats-up/)
- **Most of these cases are not about AI.** They involve ordinary texting, quiet hours, DNC and wrong numbers. Only a handful of AI-voice cases were found:
  - *Sutton v. DV Injury Law / HAH LLP / Heilbrun Law* (Texas, July 2026). Mass-tort law firms used an AI-voice platform. The plaintiff said "no" repeatedly and the AI kept pitching. The claims are TCPA plus Texas law. [Sheppard/Mondaq](https://www.mondaq.com/unitedstates/consumer-law/1821332/ai-robocalls-tcpa-and-texas-converge-in-class-action), [Law360](https://www.law360.com/articles/2500293)
  - *Mortgage One Funding* (E.D. Mich., Feb 24, 2026). Synthetic-voice refinance calls. [Inman](https://www.inman.com/2026/02/27/class-action-accuses-lender-of-unsolicited-ai-generated-cold-calls/)
  - *Lowrey v. OpenAI & Twilio* (W.D. Va., 6:2025-cv-00116, filed Dec 29, 2025). This tests whether a *platform* is liable for a customer's AI robocalls and robotexts (Fresh Start Group). No ruling on a motion to dismiss was found. [TCPAWorld](https://tcpaworld.com/2025/12/31/openai-liable-for-robocalls-texts-new-tcpa-complaint-claims-openai-and-twilio-are-liable-for-user-initiated-robotexts-violating-the-tcpa-and-this-could-change-everything/)
  - A collector faced a wrong-number "artificial or prerecorded voice" class action (Feb 2026). [accountsrecovery.net](https://www.accountsrecovery.net/2026/02/20/collector-facing-tcpa-class-action-over-wrong-number-calls-using-artificial-or-prerecorded-voice/). AiAdvantage settled a prerecorded wrong-number case for $3M covering 32,188 numbers (Aug 2026). [TCPAWorld](https://tcpaworld.com/2026/08/05/tcpa-advantage-aiadvatage-to-settle-tcpa-class-action-for-3000000-00/)
  - A practitioner blog claims that AI-related class actions in 2025-26 settled in the $5-20M range ([vida.io blog](https://vida.io/blog/tcpa-2026-what-changed)). **Unverified.**

### 1b. Regulation is pulling in both directions, and on balance it is getting *weaker* for this thesis
- **Raises risk:** FCC Feb 2024 declaratory ruling (AI voice = "artificial voice"). California law in force since Jan 1, 2025 requires an artificial-voice disclosure, with "artificial voice" defined to include AI. Texas SB 140 (Sept 1, 2025) extended state telemarketing law to texts. Utah SB 226 requires gen-AI disclosure. 25 state AI laws passed in 2026 through April. [JustCall summary](https://justcall.io/blog/ai-voice-agent-disclosure-laws.html), [entagl](https://www.entagl.com/blog/us-ai-chatbot-disclosure-laws-2026)
- **Lowers risk:**
  - *Bradford v. Sovereign Pest Control* (5th Cir., Feb 25, 2026) held that the TCPA requires only "prior express consent", which can be **oral**, not *written*, even for telemarketing artificial-voice calls. This weakens the "written-consent ledger" core of the pitch, at least in TX/LA/MS. [Nixon Peabody](https://www.nixonpeabody.com/insights/alerts/2026/02/27/fifth-circuit-holds-the-tcpa-does-not-require-prior-express-written-consent), [TCPAWorld](https://tcpaworld.com/2026/02/25/written-consent-new-fifth-circuit-decision-says-congress-never-required-it-in-the-first-place/)
  - *McLaughlin v. McKesson* (S. Ct. 2025) plus *Loper Bright*: district courts no longer have to follow FCC orders. That opens challenges to the AI-voice ruling itself, especially for cloned real voices. [Troutman](https://www.troutman.com/insights/why-does-the-tcpa-equal-chaos-the-us-supreme-court-opens-fcc-orders-to-new-challenges.html)
  - The FCC's "revoke-all" consent rule has been delayed again, to **Jan 31, 2027**, pending possible changes. [Burr](https://www.burr.com/telephone-consumer-protection-act/the-fcc-delays-effective-date-of-tcpa-revoke-all-rule-until-january-31-2027)
  - The one-to-one consent rule was vacated by the 11th Circuit in Jan 2025. That was not re-verified this round and comes from prior knowledge.
  - The FCC's Aug 2024 AI-call disclosure NPRM is still not final. The Carr FCC is signaling a lighter touch. [Perkins Coie](https://perkinscoie.com/insights/update/fcc-proposes-new-rules-ai-generated-content-calls-and-texts), [Thoughtly](https://thoughtly.com/blog/tcpa-ai-outbound-calling-compliance-checklist)
- No 2026 state-AG enforcement against a *legitimate business* using AI outbound was found. Enforcement targets scammers and political deepfakes.

### 1c. Outbound AI volume (real, but most of the "millions of agents" is inbound or consented follow-up)
- Retell: $40M+ ARR, about 40M calls a month (early 2026). Vapi: 1B+ calls processed, $500M valuation, and its marquee win (Amazon Ring) is *inbound*. Bland: 3.5M calls a week. [Retell blog](https://www.retellai.com/blog/best-voice-ai-providers) (vendor source)
- Inbound took 52% of AI voice-agent revenue in 2025 ([Grand View](https://grandviewresearch.com/industry-analysis/ai-voice-agents-market-report)). A vendor statistic says 28-34% of mid-market and enterprise B2B sales teams use an AI voice agent for outbound ([CloudTalk](https://www.cloudtalk.io/blog/sales-ai-voice-agent-statistic/), unverified).
- **Key structural point: the platforms ban AI cold calling themselves.** Bland's policy says AI outbound may only call consented contacts or existing customers, and purchased lists are prohibited ([bland.ai/blogs/cold-calling](https://www.bland.ai/blogs/cold-calling)). So the legitimate AI-outbound flow is mostly *consented speed-to-lead follow-up*. The risk is concentrated in rogue lead-gen operators, who won't buy compliance anyway.

### 1d. Practitioner worry
It is loud. Every platform has a TCPA playbook post: Retell's "2026 TCPA Compliance Playbook for Voice AI Outbound", ElevenLabs' TCPA docs page, Thoughtly, Kixie, Aloware. DNC.com's 2025 summit had a session on "AI Systems & TCPA Gaps". Per taxonomy assumption #1, loud pain is a lagging signal, and here the incumbents have already responded to it.

---

## 2. Competitors. Is anyone purpose-built for AI-agent outbound compliance? **Yes, several, and the incumbents too.**

| Player | What they ship for AI agents (2026) | Threat |
|---|---|---|
| **DNC.com / Contact Center Compliance** | "Compliance MCP Server for Agentic Outbound AI": real-time legal decisions per outbound action, covering litigators, reassigned numbers, expired consent, internal DNC and EBR. API plus 20+ dialer/CRM integrations, Litigator Scrub. [dnc.com/agentic-ai](https://www.dnc.com/agentic-ai) | Very high. This is the thesis's gate, shipped. |
| **PossibleNOW** | DNCSolution for Salesforce Headless360, exposed as MCP/A2A services for Agentforce and Copilot. Covers federal/state DNC, litigators, wireless ID, state calling-hour and frequency limits, EBR. [destinationcrm](https://www.destinationcrm.com/Articles/CRM-News/CRM-Across-the-Wire/PossibleNOW-Launches-DNCSolution%c2%a0for-Salesforces-Headless360-175279.aspx), [possiblenow.com](https://www.possiblenow.com/resources/possiblenow-brings-dnc-compliance-into-the-agentic-era-with-dncsolution-for-salesforces-headless360/) | Very high (enterprise) |
| **Gryphon AI** | Gryphon ONE for Salesforce (Jan 2026). Certifies every voice, SMS and email touch before it goes out, blocks in real time, and markets "Agentic Governance". [gryphon.ai](https://gryphon.ai/category/news/) | High |
| **ActiveProspect** (TrustedForm) **+ Jornaya/LeadiD + Infutor** | Acquired Verisk Marketing Solutions in Jan 2026, uniting the two main consent-certificate standards. 2.5B+ leads certified a year. Presented "Scaling Lead Gen with AI Voice" at LeadsCon 2026. Pricing $0.06-0.15 per retained certificate. [Verisk PR](https://s29.q4cdn.com/767340216/files/doc_news/Verisk-Announces-Sale-of-its-Marketing-Solutions-Business-to-ActiveProspect-2026.pdf), [pricing](https://support.activeprospect.com/hc/en-us/articles/44399426362004-ActiveProspect-Pricing) | Very high. Owns the consent proof that litigation defense depends on. |
| **Twilio** | Compliance Toolkit, now GA for messaging: quiet hours, monthly Reassigned Numbers Database checks, consent and opt-out management, with "additional channels" planned. Also a named defendant in *Lowrey*, so it has a strong incentive to extend this to voice. [Twilio](https://www.twilio.com/en-us/blog/products/compliance-toolkit-generally-available) | High (absorption) |
| **Microsoft Dynamics 365 Customer Insights** | MCP server that checks consent before outbound messaging. [MS Learn](https://learn.microsoft.com/en-us/dynamics365/customer-insights/journeys/mcp-server-consent) | Medium |
| **Saperly** | "Phone carrier for AI agents" with numbers, voice, SMS and **compliance (TCPA, A2P, STIR/SHAKEN) in one API**. $2-4M seed, SF. [startuphub](https://www.startuphub.ai/startups/saperly) | Direct, AI-native |
| **Verfi** | TCPA consent-verification MCP server and agent plugin: verify consent, return machine-readable proof, 3-year retention. [claudemarket listing](https://claudemarket.ai/mcp/Verfi-io/verfi-mcp-server) | Direct, AI-native |
| **Atlog (YC)** | Voice-AI platform with built-in TCPA/FDCPA/state rules. [voiceaispace](https://www.voiceaispace.com/tool/atlog) | Direct, vertical |
| **Bland + Blacklist Alliance** | Built-in DNC and litigator screening. [bland.ai](https://www.bland.ai/blogs/how-bland-ai-ensures-tcpa-dnc-compliance) | Platform-native |
| Numeracle, Hiya, First Orion | Branded calling and caller-ID reputation. Adjacent. | Low-medium |
| TCPA defense firms (Troutman Amin, etc.) | Litigation and audits. Partners or channel, not a product threat. | Low |

The space between "consent proof" (ActiveProspect) and "pre-dial gate" (DNC.com, PossibleNOW, Gryphon) is the thesis's whole product, and it is filled from both sides. The AI-native newcomers (Saperly, Verfi, Atlog) cover the long tail of developers.

## 3. Absorption risk: **High**
- Voice platforms (Bland, Retell, Vapi, ElevenLabs) treat compliance as table stakes and bundle it through partners like Blacklist Alliance. *Lowrey* gives every carrier and model vendor a liability reason to build consent enforcement in.
- Twilio's toolkit already covers 3 of the 5 gate checks for SMS.
- ActiveProspect can add a "consent token is valid for AI voice" flag to TrustedForm in a quarter, because the AI-disclosure consent language is just another policy check in TrustedForm Verify.
- There is no structural conflict that would stop any of them (constraint #4 fails).

## 4. Market size: **F4**
- **Profit-pool check:** the category leader, ActiveProspect, is estimated at ~$28M revenue ([prospeo, unverified](https://prospeo.io/c/activeprospect)) on 2.5B certificates. DNC scrubbing costs fractions of a cent per number. Gryphon, PossibleNOW and DNC.com are mid-size private firms (revenue unverified, probably $10-60M each). **The whole outbound-compliance software category is plausibly $200-500M a year (estimate).**
- **Per-call economics:** an AI call costs about $0.05-0.15 a minute. A compliance gate can charge roughly $0.002-0.02 per attempt. Even at 5B AI outbound attempts a year in the US (generous), that is $10-100M of gross gate revenue for the *whole market*. Reaching $100M ARR means capturing most of the market *and* pricing above incumbents.
- **Buyer count:** the realistic buyers are lead gen, home services, auto, real estate, solar, education, B2B SDR teams and logistics. Maybe 20-50K US firms run any outbound automation, and a few thousand run AI outbound at meaningful scale. ACV for a mid-market buyer is roughly $6-30K (comparable to Gryphon/PossibleNOW seats and scrubbing). Constraint #5 (≥5,000 buyers at ≥$25K) is unlikely.
- **Without regulated industries:** the biggest TCPA spenders are insurance (ActiveProspect has a "GM of Insurance"), mortgage/lending, collections, healthcare and banking. Remove them and you are left with home services, solar, education, auto and real estate lead gen. These are fragmented, low-ACV and churn-prone, and many are exactly the rogue operators who skip compliance. **The market does not work without the regulated buyers.**
- **Who the founder would need:** a CFO/GC at a lead-gen company pays to avoid lawsuits, but already buys TrustedForm plus a DNC scrub. The incremental willingness to pay for an "AI layer" is thin.

## 5. Vara founder edge: **weak fit**
Deepfake detection and challenge-response protect the *recipient* from fraudulent voices. This thesis protects the *caller* from consent suits, which is a different buyer and a different data asset. The evidence-ledger and regulatory-filing skills carry over, but ActiveProspect, Jornaya and Verfi already sell court-tested consent evidence with years of case law behind them (TrustedForm certificates are cited routinely in TCPA defense).

---

## Finalist format (completed for the record; verdict KILL)

- **One-line problem:** Businesses using AI voice and SMS agents for outbound face $500-1,500 per call in TCPA exposure and cannot prove, call by call, that consent covered an AI voice.
- **Why now:** FCC 2024 AI-voice ruling; record TCPA filings in 2026 (+26% YoY); AI outbound adoption; state AI-disclosure laws; *Lowrey* platform-liability theory.
- **Exact buyer:** GC or VP Compliance (or the founder/COO at smaller firms) at companies running AI outbound. Secondary: voice-AI platforms as OEM partners.
- **Exact ICP:** US lead-gen buyers and sellers, home services, solar, education and auto dealers running more than 50K AI call attempts a month, plus voice-AI agencies reselling Retell or Vapi.
- **Current workaround:** TrustedForm/Jornaya certificates + DNC.com/PossibleNOW/Blacklist Alliance scrub + platform calling-hour settings + an AI disclosure line in the script + TCPA counsel. Increasingly bundled via MCP (DNC.com, PossibleNOW) or the platform (Bland, Saperly).
- **Why incumbents cannot easily own it:** *They already do.* No conflict of interest blocks them. This is the failing criterion.
- **30-day MVP:** A pre-dial API and MCP tool that takes a TrustedForm/Jornaya token, checks the consent language for AI-voice and seller coverage, runs DNC and reassigned-number checks, applies state time and frequency rules and two-party recording states, injects the AI-disclosure script, and writes a hash-chained evidence record of the call (consent, disclosure transcript, opt-out handling).
- **Pilot design:** 2-3 Retell/Vapi agencies, shadow-mode gate on 30 days of call logs, measuring the share of attempts that would be blocked and why.
- **Pricing hypothesis:** $0.005-0.02 per gated attempt plus $500-2,000 a month platform fee. OEM revenue share with voice platforms.
- **Expansion path:** litigation-defense evidence packs, then inbound recording consent, then multi-channel (WhatsApp, email), then international (UK PECR, Canada CRTC).
- **Moat:** weak. Possible data moat from opt-out/litigator signals seen across AI calls, but DNC.com and Blacklist Alliance already own litigator data, and ActiveProspect owns consent provenance.
- **Why it could be $10B+:** only if AI outbound becomes the dominant way businesses reach consumers *and* liability moves to platforms, making the gate mandatory infrastructure. Neither is evidenced, and the courts are moving the other way (*Bradford*, *McLaughlin*).
- **Direct competitors and adjacent threats:** DNC.com MCP, PossibleNOW Headless360, Gryphon ONE, ActiveProspect+Jornaya, Twilio Compliance Toolkit, Microsoft D365 consent MCP, Saperly, Verfi, Atlog, Blacklist Alliance, platform-native features.
- **One sentence to a CFO/GC:** "Every AI call your agents place carries $500-1,500 of uncapped TCPA exposure. We block the uncovered ones before dialing and hand your counsel a court-ready evidence file for every call."
- **5 discovery questions:**
  1. How many AI outbound attempts did you place last month, and what share went to purchased versus first-party leads?
  2. What did you spend on TCPA claims, demand letters and settlements in the last 12 months?
  3. Does your current consent language name AI or artificial voice and the specific seller? Who checks it?
  4. What do TrustedForm/Jornaya, your DNC scrub and your platform *not* cover today, specifically for AI calls?
  5. Would you pay per attempt for a gate that blocks calls, given that it lowers connect volume?
- **Hard kill criteria:** already met.
  1. ≥3 funded or incumbent products ship an agent-native gate. Met: DNC.com, PossibleNOW, Gryphon, Saperly, Verfi.
  2. The category leader's revenue is under $100M despite near-universal adoption. Met (estimate).
  3. Platforms bundle compliance at no extra charge. Met: Bland/Blacklist Alliance, Twilio toolkit.

### Scores (bar: avg ≥8.5, none <7)

| Dimension | Score | Rationale |
|---|---|---|
| Pain | 7 | Record class-action volume, uncapped statutory damages |
| Urgency | 6 | Courts loosening (*Bradford*, *McLaughlin*), revoke-all delayed to 2027, AI NPRM stalled |
| ROI clarity | 6 | Clear on paper; buyers already have certificates plus scrubbing |
| Customer accessibility | 6 | Lead-gen buyers are reachable but fragmented; the best buyers are regulated |
| Pilot speed | 7 | Shadow-mode gate on call logs is fast |
| Market size | 3 | Category profit pool is about $200-500M; per-attempt pricing is fractions of a cent |
| Expansion | 5 | Channels and geographies, all contested |
| Venture potential | 4 | No $100M ARR path without regulated buyers |
| Defensibility | 3 | Incumbents own litigator data and consent provenance |
| Why now | 6 | Real behavior shift, but regulation is softening |
| Competition position | 2 | Incumbents shipped agent-native MCP gates in 2026; AI-native seeds exist |
| **Average** | **5.0** | **KILL** |

**Classification: KILL.** Causes: F2 (visible pain answered by incumbents within months), F4 (small profit pool), F1 (Twilio and platforms absorb it). It is not B: the behavior is public and the incumbents have responded, so nothing here is "too early for public evidence".

**Salvageable adjacent angle (not scored; for a future round):** the *recipient* side fits Vara better. That means businesses and carriers receiving AI-agent calls who need to verify that an inbound AI caller is authorized (agent caller-ID attestation, deepfake plus challenge-response at the IVR). Earlier rounds killed this as "Z caller verification" (F4), so revisit it only with new data.

### Unverified items
ActiveProspect ~$28M revenue (third-party database). $5-20M AI-case settlement range (vendor blog). 28-34% outbound adoption statistic (vendor). Category size $200-500M (analyst estimate). Saperly raise ($2M vs $4M, conflicting sources). 11th Circuit vacatur of one-to-one consent (prior knowledge, not re-checked this round).
