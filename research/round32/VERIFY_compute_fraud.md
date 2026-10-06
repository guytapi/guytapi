# VERIFY: F-A "Stripe Radar for AI compute"

Date: 2026-10-06. Method: about 20 WebSearch queries, run adversarially (looking for reasons the idea fails). WebFetch was not used, so the figures come from search snippets of the cited pages.

## Bottom line
**The pain is real and bigger than SYNTHESIS assumed. The opening is mostly gone.** At Sessions 2026 (May 2026), Stripe launched almost exactly the proposed wedge:
- multi-account abuse scoring at signup
- free-trial abuse prediction
- pay-as-you-go (usage) abuse protection
- protection that works off Stripe and on any processor
- a network-wide abuser graph built from device fingerprints, IPs and email domains

Stripe's own marketing calls it "Defend against customer abuse, from sign-up to usage", and it is aimed squarely at AI companies. A funded specialist, Verisoul, already counts Augment Code (on our target list) and Clay as customers. Stytch has a Replit customer story titled "Stopping fraudsters at signup". **Verdict: drops to about 7.1.**

## 1. Competition

| Player | What / when | Positioning vs F-A |
|---|---|---|
| **Stripe Radar** (Sessions 2026, May) | The "biggest expansion ever" of Radar. It adds multi-account abuse, free-trial abuse and pay-as-you-go abuse protection, works regardless of payment processor, and draws on the Stripe network (fingerprints, IPs, emails). These features sit in the Radar Pro plan, with a pricing update planned for Jan 2027. It blocked 3.3M risky trial attempts in one month across 8 AI businesses, and 550k abusive trials across 4 AI companies in 2 months, about **$4.4M of compute saved**. [stripe.com/blog/expanding-stripe-radar-to-protect-more-of-your-business; stripe.com/radar/customer-abuse; stripe.com/blog/everything-we-announced-at-sessions-2026; support.stripe.com "Updates to Radar pricing (January 2027)"; fortune.com/2026/09/28/ai-unit-economics-token-theft-stripe/] | **This is the thesis, including the cross-company graph and the "compute dollars saved" framing.** Stripe already processes payments for most of these companies, so distribution is built in. |
| **Verisoul** (Austin) | $8.8M Series A led by High Alpha (with Lookout, Bain Future Back, Bitkraft, Third Prime). 100+ customers, more than 6x YoY ARR growth. Customers include **Augment Code**, Clay and Morning Consult. At Clay, 47% of signups were fake or duplicate; blocking them saved $175k of credits in one month and added $150k ARR. [highalpha.com/news/verisoul-raises-8-8m-series-a...; pulse2.com/verisoul-8-8-million-funding; verisoul.ai/customer-stories/clay; verisoul.ai/industries/saas-ai-tech] | A direct AI-native competitor already selling to the target list. |
| **Stytch** (owned by Twilio) | Device Fingerprinting with "prevent free trial abuse" guides. Customer stories: **Replit** ("Stopping fraudsters at signup") and **Kilo Code** ("Stopping AI and LLM abuse"). Stytch says fraud prevention has become a bigger need for its AI customers. [stytch.com/docs/fraud/guides/prevent-free-trial-abuse; stytch.com/customer-stories/replit; stytch.com/customer-stories/kilocode] | Replit, our top evidence company, already buys a vendor. |
| **Clerk** | Bot and multi-account protection included in every plan, marketed for AI apps. [clerk.com/ai-authentication] | Free and bundled, which squeezes the low end. |
| **Vercel BotID** | Deep Analysis on signup and inference routes. In 2025, Nous Research had its free inference drained by thousands of fake accounts despite Cloudflare Turnstile, then switched to BotID. [vercel.com/blog/how-nous-research-used-botid-to-block-automated-abuse-at-scale] | Bundled into the main hosting platform for AI apps. |
| Cloudflare Turnstile / Bot Mgmt, Fingerprint, Castle, Sift, SEON, Arkose, Persona, Socure ($5.2B valuation, Aug 2026) | General-purpose vendors. I found no AI-credit-specific launch from these in my searches, but none is needed given the above. | They own the commodity layer. |
| Smaller players: ShieldLabs (shieldlabs.ai, content on "trial farming"); PandaStack blog on cryptomining in free sandboxes (Aug 2026); SheerID (used by Cursor) | Early or content-led. | They show the niche is crowded with entrants too. |

## 2. Size of the pain (confirmed, mostly from Stripe)
- **1 in 6 signups at AI companies is linked to multi-account abuse.** Patrick Collison called it a "wave of token theft wreaking havoc on the AI economy" (Fortune, 2026-05-07). Attempted multi-account abuse rose 40% in 6 months, and by more than 600% in some sub-sectors. Free-trial abuse grew 6.2x YoY (Nov 2025–Feb 2026). [fortune.com/2026/05/07/stripe/; stripe.com/blog/what-stripe-data-shows-about-fraud-at-ai-startups; oecd.ai/en/incidents/2026-05-07-8776]
- Self-serve AI products with API access see **10x more attempted abuse** than enterprise AI. In Q3 2025, AI startups' attempted transaction-fraud rate was 4.3x the startup average; by Q1 2026 it was 2.6x. [Stripe blog]
- Dollars: about $4.4M of compute saved across 4 AI companies in 2 months, roughly **$0.5M per company per month**. Clay saved $175k per month. This supports SYNTHESIS's "$1M–$20M+/yr at a scaled AI app".
- Anthropic disabled about **1.45M accounts** from Jul to Dec 2025, mostly automated abuse and ToS detections (Transparency Hub, Jan 2026). In 2026 it also cracked down on subscription-OAuth reuse (the OpenClaw bans). [pcworld.com/article/3068842; tinycorestudios.uk/blog/news/2026-04-11-anthropic-banned-openclaw]
- Canva cracked down on "seat cycling", a scheme that farms AI credits from free accounts (2026). [ia.acs.org.au/article/2026/canva-cracks-down-on-ai-credit-fraud.html; startupdaily.net]
- Phishing hosting: Proofpoint sees **tens of thousands of lovable.app URLs flagged as threats every month** since Feb 2025. One campaign hit more than 5,000 organizations. Guardio coined "VibeScamming". Lovable shipped prompt-time detection and daily scanning in Jul 2025. [proofpoint.com/us/blog/threat-insight/cybercriminals-abuse-ai-website-creation-app-phishing; gendigital.com/blog/insights/research/vibe-scams]
- Not found: a public share of *free-tier GPU spend* lost to abuse. The 5–20% claim is still an estimate, but "1 in 6 signups" makes it plausible.

## 3. Breadth (more companies)
- Hiring T&S or anti-abuse in 2026:
  - Gamma: T&S SWE covering phishing, abuse and fraud, Jul 2026, $180–310k [jobs.accel.com]
  - OpenRouter: T&S SWE covering abuse and fraud, Sep 2026 [jobs.menlovc.com]
  - OpenAI, Anthropic Safeguards and Google Workspace AI T&S are also hiring.
- Tightened or controlled free tiers:
  - Cursor (fingerprinting plus SheerID)
  - Canva (seat cycling)
  - Nous Research (free inference abused)
  - Anthropic (OpenClaw)
  - Amp (ad-funded free tier dropped)
  - Augment (repricing)
- Searches did not surface 2026 T&S postings for Perplexity, Hugging Face, Railway or Render.
- Overall breadth is good: the problem is universal across self-serve AI. That cuts both ways, because it is also why Stripe built it.

## 4. Kill risks
- **Generic and platform vendors cover it.** Stripe now covers signup, trial and usage abuse with a network graph and no processor lock-in. Verisoul, Stytch, Clerk and BotID cover the rest. The SYNTHESIS line "Stripe Radar for the card only (it doesn't see compute usage)" is **false as of May 2026**.
- **The "still building internally" signal is weaker than read.** Replit uses Stytch and Augment uses Verisoul. The 2026 hires look like teams that operate and integrate vendors plus a policy layer (T&S, phishing, CSAM), not a gap that no vendor fills.
- **Network effects favor the incumbent.** The cross-company abuser graph is Stripe's core asset. A startup's graph starts at zero.
- **Buyer count:**
  - About 300–800 AI companies give away meaningful compute (coding agents, app builders, sandboxes, inference APIs, gen-media, chat apps).
  - Only about 50–150 lose more than $1M a year.
  - Plenty for a $50–100M ARR business, but $10B needs the broader identity and fraud market, where Stripe, Socure and Sift already are.
- **Residual opening.** The part no one clearly owns is *in-session runtime abuse* (cryptomining in sandboxes, agent-loop token burn, proxying or reselling) plus *generated-content abuse* (phishing apps, malware hosting). Stripe sees signups and payments, not sandbox syscalls or generated HTML. This is narrower, closer to infra and content security, and a different buyer (platform and security, not growth or CFO).

## Re-score (10 criteria)

| Criterion | SYNTHESIS | Re-score | Justification |
|---|---|---|---|
| Pain today | 8 | **9** | 1 in 6 signups, the Collison quote, Canva and Nous incidents, 1.45M Anthropic bans. |
| Dollars attached | 8 | **8** | About $0.5M per month per company (Stripe sample) and $175k per month at Clay. Real, but no public free-tier-share number. |
| Headcount attached | 7 | **7** | Teams of 3–8 at the larger players. Many buy vendors instead. |
| Growth rate of pain | 9 | **9** | Up 40% to more than 600% in 6 months, 6.2x YoY. |
| Ease of finding buyers | 9 | **8** | Easy to find, but they are already being pitched by Stripe, their incumbent vendor. |
| 30-day pilotability | 9 | **7** | Technically easy, but it competes with Stripe's one-toggle Radar Pro and Verisoul's live shadow mode. |
| Existing internal builds | 9 | **6** | Replit uses Stytch and Augment uses Verisoul. The internal work is integration and policy. |
| Competitive opening | 7 | **3** | Stripe shipped the exact wedge, including the network and compute-dollars ROI. A funded AI-native specialist already sells to the target list. |
| Expansion potential | 8 | **7** | Agent traffic and agent payments are also on Stripe's roadmap (agentic commerce). |
| $10B potential | 7 | **4** | Stripe owns the moat (the network graph). A standalone ceiling looks like Verisoul or Castle scale. |
| **Average** | **8.1** | **6.8** | |

## Verdict
**It drops: from 8.1 to about 6.8.** It does not reach 8.5, and it does not stay around 8.

The thesis was right about the pain, so right that Stripe productized it four months before this round. The surviving sub-thesis is **"runtime and content abuse for compute and hosting platforms"**: cryptomining and proxy abuse in sandboxes, phishing and malware on generated sites, agent-loop burn, sold to platform and security leads at Vercel, Lovable, Replit, E2B, Browserbase, Modal, Daytona and others. It needs its own verification. Expect a pre-verification score around 7, with competition from Cloudflare, Proofpoint and Netcraft-style takedown vendors and with the platforms' own scanners.
