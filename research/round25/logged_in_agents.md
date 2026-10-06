# Round 25: Problems for platforms when AI agents act inside users' logged-in sessions

Date: 2026-10-06. Role: skeptical analyst and red team.
Budget: 34 web searches + 1 GitHub MCP search (35 of 35). WebFetch was not used. Every URL below came from a search result. Claims marked [snippet] were read only in search-result snippets. Nothing marked [unverified] was confirmed by a second source.
Already ruled out (killed earlier): bot detection / agent-era trust (Z), agent-polluted analytics (F4), agent access and metering for SaaS (T4).

**Bottom line: all five candidates and four extras are KILL. Nothing qualifies as A or B. No full finalist write-up.** The closest near-miss, "in-session agent action attestation," scores **4.9** (scorecard in §4). Every candidate dies for one of three reasons:
1. **Liability has already been pushed onto the user.** The Ninth Circuit held that "the user, not Perplexity, accesses Amazon." Perplexity, Target and Gemini terms all make the user responsible for what the agent does. That leaves the platform with no new liability to budget for.
2. **The right control point is the agent vendor or the payment network, not the platform.** A single platform sees only its own pages. The agent sees every site and can act at read time. Visa and Mastercard own intent and authorization.
3. **Every remaining platform-side need splits into categories that are already crowded or already killed.** "Is this an agent?" is Z. "Let agents in with scoped access" is T4. "Did the user authorize it?" belongs to Visa/Mastercard/Prove/Proof. "Disputes" belong to chargeback vendors.

---

## 0. Context and what is actually true (verified)

- **Ninth Circuit, Aug 4 2026:** the court vacated the Mar 9 preliminary injunction against Comet on Amazon. It held that Amazon was unlikely to win under the CFAA or CDAFA because "it is users, not Perplexity, who access Amazon's systems." The case is back in N.D. Cal. ([Bloomberg Law](https://news.bloomberglaw.com/ip-law/perplexity-overturns-amazon-ban-on-ai-shopping-bot-on-appeal); [Ballard Spahr](https://www.ballardspahr.com/insights/alerts-and-articles/2026/08/ninth-circuit-opines-on-agentic-ai-in-e-commerce); [TNW](https://thenextweb.com/news/amazon-loses-perplexity-comet-ai-shopping-ruling)). Bloomberg Law's headline says the win "keeps hacking liability risk" alive ([bgov](https://news.bgov.com/ip-law/perplexitys-appeal-win-over-amazon-keeps-hacking-liability-risk)).
- **Amazon's Sep 2026 filing [snippet]:** Amazon says **Comet for iOS copies the user's Amazon session cookie to Perplexity's cloud**, where a virtual browser requests pages directly. That would contradict Perplexity's brief. **Comet ran at least 185,712 sessions on Amazon.com by Jun 15**, and Amazon's traffic team spent at least 1,280 hours on it ([aiweekly](https://aiweekly.co/alerts/amazon-alleges-perplexity-misled-ninth-circuit-on-comet-traffic)). **For skeptics: 185K sessions in about 11 months is a rounding error at Amazon's scale.** The volume of in-session agent actions on a top platform is still small.
- **Agent-side safeguards are now default:** Gemini auto-browse uses Google Password Manager to sign in, requires explicit approval before final actions such as orders, and went to all US Android users on Aug 18 2026 (auto-browse only for AI Pro/Ultra) [snippet] ([9to5google](https://9to5google.com/2026/01/28/chrome-gemini-auto-browse/); [pasqualepillitteri](https://pasqualepillitteri.it/en/news/3256/gemini-in-chrome-skills-how-they-work-countries-availability)). Atlas has a logged-in mode ([OpenAI help](https://help.openai.com/en/articles/12628199-chatgpt-atlas-agent-mode)).
- **OSS:** browser-use/browser-use has **117,241 stars [GH, 2026-10-06]**. I could not verify "millions of installs."
- **Volume claims are unreliable.** A blog says "34% of US online purchases in Q1 2026 involved AI agents" ([chattergo](https://www.chattergo.com/blog/agentic-commerce-reshaping-ecommerce-2026)) **[unverified, almost certainly conflates "AI-assisted research" with agent checkout]**. Round 18 estimated agents at roughly 6–7% of logged-in activity. Forter reports a 2,107% rise in "agentic activity" over 6 months across 400K businesses [snippet] ([e-commerce.news](https://e-commerce.news/story/forter-unveils-ai-copilot-to-tackle-surging-fraud-risk)). The growth rate is large; the base is small.

---

## 1. Candidate evaluations

### (a) Account-security breaks: platform content hijacks users' agents ("your site can command your users' agents")

**Evidence (strong, but all on the agent side):**
- *BioShocking* (LayerX, Jun 24 2026): indirect prompt injection compromised **six AI browsers and extensions (OpenAI, Anthropic, Perplexity)**. It made them copy SSH credentials from an authenticated GitHub repo and escalate to a full **1Password account takeover**. OpenAI fixed Atlas. Perplexity closed the report. LayerX says Anthropic's patch "did not hold" ([THN](https://thehackernews.com/2026/06/new-bioshocking-attack-tricks-ai.html); [CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-browser-prompt-injection-20260630-csa-s/)).
- *PleaseFix*, a 0-click attack on agentic browsers ([Zenity](https://zenity.io/research/pleasefix-vulnerabilities)). *PerplexedBrowser* ([HelpNet](https://helpnetsecurity.com/2026/03/04/agentic-browser-vulnerability-perplexedbrowser)). A 2025 Brave demo used a Reddit spoiler-tag comment to hijack Comet into pulling Gmail OTPs ([hackmag](https://hackmag.com/news/cometjacking); [BleepingComputer](https://bleepingcomputer.com/news/security/commetjacking-attack-tricks-comet-browser-into-stealing-emails)).
- In-platform agents leak too: Atlassian Rovo injection (PromptArmor; Varonis "RovoBlast," Aug 2026) and M365 Copilot SearchLeak CVE-2026-42824 (Jun 2026) ([CSA Rovo](https://labs.cloudsecurityalliance.org/research/csa-research-note-atlassian-rovo-prompt-injection-data-exfil/); [CSA SearchLeak](https://labs.cloudsecurityalliance.org/research/csa-research-note-m365-copilot-searchleak-ai-data-exfil-2026/)).

**Competitors and absorption:**
- Perplexity **BrowseSafe** (open-source HTML injection classifier) ([HF](https://huggingface.co/perplexity-ai/browsesafe)).
- Superagent sells "detect injections in user-generated content" for platforms ([superagent](https://safety.superagent.sh/use-cases/detect-block-prompt-injections-user-content)).
- Akamai Firewall for AI (inbound and outbound) and Cloudflare AI Security for Apps ([Akamai](https://akamai.com/products/firewall-for-ai)).
- Lakera (Check Point), HiddenLayer, and Prompt Security (SentinelOne) cover the enterprise and app side.
- **Akamai acquired LayerX** (completed Jul 2026) [snippet] ([Akamai PR](https://www.akamai.com/es/newsroom/press-release/akamai-technologies-announces-intent-to-acquire-layerx-advancing-its-workforce-security-strategy-with-ai-usage-control)).
- The UGC platforms with the most exposure (Gmail, GitHub, Reddit, Atlassian, M365) are giants that defend in-house.

**Buyer and money:** none found. The terms put responsibility on the user (§d). I found **no case or regulator** holding a platform liable because a visitor's agent was hijacked by content on its pages. The "Reasonable Platform Standard" claim comes from a law-firm marketing page ([daeryunlaw](https://www.daeryunlaw.com/us/practices/detail/global-platform-liability)) **[unverified, not a cited doctrine]**.

**Structural problem:** a platform scanning its own pages protects agents on one site. The agent vendor scanning at read time protects every site. The defense belongs to the agent vendor (F1). Platforms will not pay to fix a flaw in someone else's product when the law and the terms say they are not liable.

**Verdict: KILL** (F1 + no budget; F2 on the prompt-injection-defense tooling). Score ~4.3.

### (b) UX/conversion: platforms lose the user relationship (ads, upsell, retention)

**Evidence:** the ruling "potentially threatens Amazon's ad-driven retail model" because blanket bans may not survive ([paz.ai](https://www.paz.ai/blog/amazon-perplexity-court-block-ai-agents); Ballard Spahr). Publishers' page-view and impression metrics stop mattering ([AdPushup](https://www.adpushup.com/blog/agentic-browser/)). Retailers block their own agent customers: nearly half of test runs hit verification challenges ([Mediaweek](https://www.mediaweek.com.au/retailers-risk-losing-customers-as-ai-shopping-agents-arrive/)).

**Competitors and absorption:**
- **GEO/agent optimization is already funded.** Profound Series C at a **$1B** valuation, and Evertune, Bluefish and Profound raised $55M in Aug [snippet] ([Adweek](https://tunnel-sergio.adweek.com/commerce/6-hot-geo-startups-future-ai-shopping/)).
- **WebMCP** is in a Chrome 149–156 origin trial, a W3C CG draft with Microsoft involved. It is the free, browser-native "agent-mode surface" ([Chrome docs](https://developer.chrome.com/docs/ai/webmcp?authuser=0); [ppc.land](https://ppc.land/chrome-149-origin-trial-puts-webmcp-in-developers-hands-at-last/)).
- Cloudflare AI Crawl Control "agentic internet" tools ([CF changelog](https://developers.cloudflare.com/changelog/post/2026-04-17-tools-for-agentic-internet/index.md)).
- Forter Agentic Orchestration Suite ([Sacra](https://sacra.com/chat/h/c71a74fe-1c6a-4853-867d-5333ec853874/)).
- Anthropic retailer agent blueprints (Sep 2 2026) [snippet] ([stellagent](https://stellagent.ai/insights/ec-ai-news-digest-2026-09-04)).
- The platform's own countermove is first-party agents (Amazon Rufus / Buy for Me).

**Structural problem:** this is round-1 A (sellable to agents), round-15 P2 (being chosen by agents) and T4 metering under a new name. The real fix (charge agents, or become the agent) is a business-model decision the platform makes itself.

**Verdict: KILL** (F1 + F2 + overlaps prior kills). Score ~4.0.

### (c) Consent and authorization: step-up for agent actions inside sessions

**Evidence:** Commonwealth Bank's e-banking terms (from Jun 1 2026) say an automated agent must be expressly permitted and must "clearly identify itself and its function" [snippet] ([CommBank T&Cs](https://www.commbank.com.au/personal/netbank/terms-and-conditions.html)). Agents in real Chromium defeat WAF and user-agent checks ([cside](https://cside.com/blog/best-ai-agent-detection-tools-web-applications)). Amazon says Comet sent Chrome's user-agent string and updated within 24 hours to evade blocking ([ppc.land](https://ppc.land/amazon-sues-perplexity-over-covert-ai-agent-access-to-marketplace/)).

**Competitors (very crowded):**
- Networks: Visa Trusted Agent Protocol, now Intelligent Commerce; Mastercard Agent Pay and **Verifiable Intent (with Google, Mar 2026)** ([eco.com](https://eco.com/support/en/articles/15192001-what-is-mastercard-agent-pay-ai-agent-commerce-protocol); [Prove/BusinessWire](https://www.businesswire.com/news/home/20251023729694/en/Prove-Launches-Verified-Agent-Solution-to-Secure-the-%241.7-Trillion-Agentic-Commerce-Revolution)).
- Identity and authentication: Prove Verified Agent; **Proof** joined FIDO (May 2026) to bind IAL2 identity to agent actions ([BusinessWire](https://www.businesswire.com/news/home/20260501569763/en/Proof-Joins-FIDO-Alliance-to-Link-AI-Agent-Actions-to-Verified-Human-Identity)); ValidSoft cryptographic intent binding (Aug 2026) ([kdhnews](https://kdhnews.com/online_features/press_releases/validsoft-details-technical-approach-to-cryptographic-intent-binding-for-voicemfa-in-agentic-ai/article_0de0b882-f442-578d-bd33-57a2e312162c.html)).
- Bot and fraud vendors: HUMAN AgenticTrust with "granular permission management for agents" ([HUMAN](https://www.humansecurity.com/learn/resources/human-agentictrust)); BioCatch "agentic account takeover" ([BioCatch](https://www.biocatch.com/use-case/agentic-ai/agentic-account-takeover)); Transmit "Blinded by the Agent" ([Transmit](https://transmitsecurity.com/blog/blinded-by-the-agent-how-ai-agents-are-disrupting-fraud-detection)); Signifyd Account Integrity.
- Auth providers: Auth0 delegated authorization and Session Delegation ([Auth0](https://auth0.com/ai/docs/intro/delegated-authorization)); Stytch (Twilio) Connected Apps.
- Agent signing: **Web Bot Auth** is in production at OpenAI, Anthropic, Perplexity and Cloudflare. ChatGPT agent sends `Signature-Agent: https://chatgpt.com` ([guptadeepak](https://guptadeepak.com/guides/verify-an-ai-agent/)). The agent side also already enforces confirmation before final actions (Gemini).
- A "Visa acquires BioCatch" headline appeared in one snippet ([securityarsenal](https://securityarsenal.com/blog/visa-acquires-biocatch-the-critical-shift-to-behavioral-defense-against-ato-and-digital-fraud)) **[unverified]**.

**Structural problem:** "step up when an agent does X" first requires knowing an agent is present. That is detection, which is Z (killed). Once the agent is known, "prove the human authorized it" is owned by the networks, the agent vendors and IdV firms. Cloud agents sign their requests. Local, undisclosed agents (Comet) cannot be stepped up any differently from the human, because they are the human's browser.

**Verdict: KILL** (F1 + F2 + depends on Z). Score ~4.6.

### (d) Disputes and support: "my agent did it, not me"

**Evidence:** the dispute wave is widely predicted but mostly written by vendors: Chargebacks911 "I didn't buy that, my AI did," Chargeflow, startups.co.uk, stellagent ([Chargebacks911](https://chargebacks911.com/i-didnt-buy-that-my-ai-did-agentic-commerce-to-drive-new-wave-of-disputes/); [Chargeflow](https://www.chargeflow.io/blog/agentic-commerce-chargebacks-liability)). The Merchant Risk Council ran a 2026 session "who pays when things go wrong" ([MRC](https://merchantriskcouncil.org/learning/resource-center/events/London/2026-the-year-of-the-ai-agent-buying-spreewho-pays-when-things-go-wrong)). Target warns that users pay for its shopping agent's mistakes [snippet] ([ainauten](https://news.ainauten.com/markdown/target-warns-that-if-its-ai-shopping-agent-makes-an-expensive-mistake-youll-have-to-pay-for-it)). Reg E does not explicitly cover agent delegation ([Backbase](https://www.backbase.com/insights/agentic-payments-and-the-liability-gap-regulators-havent-closed)). **I found no real incident data** (dispute rates or dollar amounts attributed to agents). Support forum searches turned up only ordinary refund complaints.

**Competitors:** Chargeflow, Chargebacks911, Forter, Riskified, Signifyd, Justt, Verifi/Ethoca (network-owned), and OriginStamp-style verifiable records ([OriginStamp](https://originstamp.com/en/blog/reader/agentic-commerce-chargeback-verifiable-records)).

**Structural problems:**
1. Disputes go through the **existing reason codes** (Visa 10.4, 13.1, 13.3) ([chargeback.io](https://www.chargeback.io/pt/blog/agentic-payments-chargebacks)), so incumbents add an "agent evidence" field as a feature.
2. **Counterintuitively, local in-session agents leave the merchant better evidence**: the user's own device, IP and account history, which is what Visa CE 3.0 asks for. The evidence gap exists only for tokenized checkout or cloud-relay agents, and Verifiable Intent/TAP are being built for exactly that.
3. Non-payment disputes (account changes, cancellations) have no dollar pool.
4. ToS language (Perplexity: user responsible for "any actions taken by the Comet agent") pushes liability downstream ([aiweekly](https://aiweekly.co/the-artifice/court-rules-ai-shopping-agent-is-legally-its-user-companies-confirm-this-has)).

**Verdict: KILL** (F1 to chargeback incumbents and networks; F3 pre-demand on agent-specific volume). Score ~4.5.

### (e) Other problems found

| # | Problem | Evidence | Why it dies |
|---|---|---|---|
| e1 | **Authorized cookie relay vs stolen cookie.** Agents that copy session cookies to their own cloud (Comet iOS, per Amazon) look exactly like infostealer replay. Platforms adopting **DBSC** (Chrome 146 GA on Windows Apr 2026 [snippet], [Google](https://blog.google/security/protecting-cookies-with-device-bound-session-credentials/); [cside](https://cside.com/blog/dbsc-vs-device-fingerprinting)) will break those agents, which pushes them toward delegated tokens | Amazon filing (above) | The resolution is delegated OAuth or session delegation (Auth0, Stytch, Okta, WorkOS, Frontegg), which is **T4, killed**, plus Web Bot Auth, which is **Z, killed**. **The most novel weak signal in this round**, but it has no independent home |
| e2 | **Bank loss allocation when a hijacked agent pushes a payment** (UK APP reimbursement splits cost 50/50 between sending and receiving PSPs; US Reg E is silent) | [A&O Shearman](https://www.aoshearman.com/en/insights/ao-shearman-on-fintech-and-digital-assets/the-uks-authorised-push-payment-app-fraud-reimbursement-scheme); Backbase; CommBank terms | No public case of an agent-mediated APP claim. The buyers are few large PSPs that build in-house or buy BioCatch, Featurespace (Visa) or Feedzai. Failure modes F1/F4 and taxonomy assumption #4 (mandates on giants get absorbed) |
| e3 | **B2B SaaS tenant data exfiltrated through an employee's agent** (support tickets and shared docs used as injection carriers) | Rovo, SearchLeak, AITOPIA extensions (900K installs, 20K tenants) [snippet] | The enterprise side is owned by LayerX (Akamai), Island, Palo Alto Prisma Browser and Push. SaaS vendors patch their own agents. Gartner said "block AI browsers" ([The Register](https://www.theregister.com/2025/12/08/gartner_recommends_ai_browser_ban/?td=rt-3a)), and enterprises now allowlist |
| e4 | **Returns and errors from agent-placed orders** | Retail TouchPoints "liability storm" ([link](https://www.retailtouchpoints.com/features/executive-viewpoints/agentic-commerce-is-a-huge-opportunity-for-retailers-its-also-a-liability-storm)); Chain Store Age ([link](https://chainstoreage.com/how-agentic-commerce-will-test-loyalty-and-returns)) | Returns platforms (Loop, Narvar) add an agent flag. Merchants push the cost to users through terms (Target). No measured excess return rate yet (F3) |

---

## 2. Why the "victim-side" frame from round 24 does not hold here

The failure taxonomy pointed at "problems for the victims of agent behavior." For logged-in agents, the platform is often **not** a legal victim:
- The Ninth Circuit says the user is the actor.
- Agent vendors' terms make the user liable.
- Platforms respond by (i) shifting liability in their own terms (CommBank, Target), (ii) building first-party agents, or (iii) buying from existing bot, fraud, chargeback and identity vendors that have all published "agentic" products in the last 12 months.

The actual victim of a hijacked agent is the **user**, and the parties able to fix it are the **agent vendors** (OpenAI fixed BioShocking; Perplexity shipped BrowseSafe). That is F1 in its purest form.

## 3. Absorption map (who owns each platform-side need)

| Need | Owner(s) |
|---|---|
| Is this an agent, and which one? | Web Bot Auth (Cloudflare/OpenAI/Anthropic/Perplexity), HUMAN, DataDome, Kasada, cside, BioCatch (= Z, killed) |
| Let agents in with scoped rights | Auth0, Stytch, Okta, WorkOS, Frontegg, WebMCP (= T4, killed) |
| Did the human authorize it? | Visa TAP/VIC, Mastercard Agent Pay + Verifiable Intent, Prove, Proof, ValidSoft |
| Fraud and ATO through agents | Forter, Signifyd, Riskified, Transmit, BioCatch, Sardine |
| Disputes | Chargeflow, Chargebacks911, Justt, Verifi/Ethoca |
| Content that hijacks agents | Agent vendors (BrowseSafe, Atlas fixes), Superagent, Akamai/Cloudflare Firewall for AI, Lakera/Check Point |
| Losing the customer relationship | Profound ($1B), Bluefish, Evertune, WebMCP, first-party agents |

## 4. Closest near-miss scorecard (for the record, not a finalist)

**"In-session agent action attestation."** A neutral record, kept per sensitive action, of whether it was done by the human, a user-directed agent (which one, under what instruction), or a hijacked agent. It would be sold to regulated platforms (banks, brokerages, telecom port-out) for disputes and Reg E/APP claims. It reuses Vara's caller-verification and step-up components (round 12).

| Pain | Urgency | ROI | Access | Pilot speed | Market | Expansion | Venture | Defensibility | Why now | Competition |
|---|---|---|---|---|---|---|---|---|---|---|
| 5 | 4 | 4 | 5 | 5 | 6 | 6 | 5 | 3 | 8 | 3 |

**Avg 4.9. Classification: KILL.** The "hijacked vs directed" verdict needs the agent's own reasoning trace, which only the agent vendor has, so it is not observable from the platform side. Networks (Verifiable Intent) and BioCatch, Transmit and HUMAN already pitch the rest. Volume is tiny (185K Comet sessions on Amazon in 11 months).

**Optional 14-day test (not recommended):** ask 8 US/UK banks, brokerages or telcos for their count of disputes in the last 90 days where the customer said an AI agent acted. Pass = ≥3 have >50 such cases/quarter **and** have no vendor answer. Expected result: "we can't tell, and we haven't seen it." That would confirm F3.

## 5. Lessons for the war room

1. **Court rulings that make the user the legal actor move liability away from platforms.** A ruling like that kills platform-side budgets rather than creating them.
2. **The control point for any agent-reading risk is the agent vendor, not each website.** Any "protect the receiving site" thesis has to explain why a site would pay to fix another company's product.
3. **The only new technical conflict found is e1 (DBSC and device binding vs cloud-relay agents).** Watch it. If Amazon wins on the cookie-relay facts in N.D. Cal., or if major platforms adopt DBSC, cloud agents will be forced onto delegated tokens. That benefits T4 incumbents (Auth0, Stytch, Okta), not a new company.

## Sources (all from search results; [GH] = GitHub MCP, 2026-10-06)
Court and Amazon: news.bloomberglaw.com/ip-law/perplexity-overturns-amazon-ban-on-ai-shopping-bot-on-appeal ; news.bgov.com/ip-law/perplexitys-appeal-win-over-amazon-keeps-hacking-liability-risk ; ballardspahr.com/insights/alerts-and-articles/2026/08/ninth-circuit-opines-on-agentic-ai-in-e-commerce ; thenextweb.com/news/amazon-loses-perplexity-comet-ai-shopping-ruling ; aiweekly.co/alerts/amazon-alleges-perplexity-misled-ninth-circuit-on-comet-traffic ; aiweekly.co/the-artifice/court-rules-ai-shopping-agent-is-legally-its-user-companies-confirm-this-has ; ppc.land/amazon-sues-perplexity-over-covert-ai-agent-access-to-marketplace/ ; paz.ai/blog/amazon-perplexity-court-block-ai-agents
Security: thehackernews.com/2026/06/new-bioshocking-attack-tricks-ai.html ; labs.cloudsecurityalliance.org/research/csa-research-note-ai-browser-prompt-injection-20260630-csa-s/ ; zenity.io/research/pleasefix-vulnerabilities ; helpnetsecurity.com/2026/03/04/agentic-browser-vulnerability-perplexedbrowser ; hackmag.com/news/cometjacking ; labs.cloudsecurityalliance.org/research/csa-research-note-atlassian-rovo-prompt-injection-data-exfil/ ; labs.cloudsecurityalliance.org/research/csa-research-note-m365-copilot-searchleak-ai-data-exfil-2026/ ; huggingface.co/perplexity-ai/browsesafe ; safety.superagent.sh/use-cases/detect-block-prompt-injections-user-content ; akamai.com/products/firewall-for-ai ; theregister.com/2025/12/08/gartner_recommends_ai_browser_ban/ ; blog.google/security/protecting-cookies-with-device-bound-session-credentials/ ; cside.com/blog/dbsc-vs-device-fingerprinting ; cside.com/blog/best-ai-agent-detection-tools-web-applications
Identity/authorization: guptadeepak.com/guides/verify-an-ai-agent/ ; help.openai.com/en/articles/12628199-chatgpt-atlas-agent-mode ; humansecurity.com/learn/resources/human-agentictrust ; biocatch.com/use-case/agentic-ai/agentic-account-takeover ; transmitsecurity.com/blog/blinded-by-the-agent-how-ai-agents-are-disrupting-fraud-detection ; businesswire.com/news/home/20260501569763/en/ (Proof/FIDO) ; businesswire.com/news/home/20251023729694/en/ (Prove Verified Agent) ; eco.com/support/en/articles/15192001-what-is-mastercard-agent-pay-ai-agent-commerce-protocol ; auth0.com/ai/docs/intro/delegated-authorization ; commbank.com.au/personal/netbank/terms-and-conditions.html ; developer.chrome.com/docs/ai/webmcp
Disputes/commerce: chargebacks911.com/i-didnt-buy-that-my-ai-did-agentic-commerce-to-drive-new-wave-of-disputes/ ; chargeflow.io/blog/agentic-commerce-chargebacks-liability ; chargeback.io/pt/blog/agentic-payments-chargebacks ; originstamp.com/en/blog/reader/agentic-commerce-chargeback-verifiable-records ; merchantriskcouncil.org/...who-pays-when-things-go-wrong ; backbase.com/insights/agentic-payments-and-the-liability-gap-regulators-havent-closed ; aoshearman.com/en/insights/.../the-uks-authorised-push-payment-app-fraud-reimbursement-scheme ; e-commerce.news/story/forter-unveils-ai-copilot-to-tackle-surging-fraud-risk ; sacra.com/chat/h/c71a74fe-1c6a-4853-867d-5333ec853874/ ; tunnel-sergio.adweek.com/commerce/6-hot-geo-startups-future-ai-shopping/ ; retailtouchpoints.com/features/executive-viewpoints/agentic-commerce-is-a-huge-opportunity-for-retailers-its-also-a-liability-storm ; github.com/browser-use/browser-use [GH]
