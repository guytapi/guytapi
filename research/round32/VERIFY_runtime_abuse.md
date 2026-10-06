# VERIFY: F-A' "Runtime and content abuse at AI compute and hosting platforms"

Date: 2026-10-06. Method: 21 WebSearch queries, run adversarially (looking for reasons the idea fails). WebFetch was not used, so the figures come from search snippets of the cited pages.

**The thesis being tested:** abuse that happens *after* signup, which Stripe Radar does not see. It has three parts:
1. **Runtime:** cryptomining, proxying or DDoS inside sandboxes and agent runtimes (E2B, Modal, Replit, Browserbase, Daytona, Vercel Sandbox, Cloudflare containers).
2. **Content:** phishing or malware hosted on AI-generated sites (Lovable, v0, Bolt, Netlify, Replit deployments).
3. **Cost:** runaway agent token loops.

**Buyer:** platform, security and T&S leads.

## Bottom line
**The pain is real and growing, but it is an old hosting problem in new clothes, and every part already has a vendor or a bundled answer:**
- **Content:** Guardio is embedded in Lovable's generation chain. Netcraft gives hosts a free real-time abuse feed plus takedown. Abusix sells abuse-desk automation to hosts. Cloudflare and Vercel run in-house automation.
- **Runtime:** "freejacking" has been fought since 2021. Platforms solved it with card checks, trial credits and internal detectors, not with a vendor.
- **Cost:** gateways (Portkey, LiteLLM) and model providers (OpenAI hard limits, Jul 2026) cover it.

The three parts serve different buyers and do not combine into one product. The buyer pool is roughly 100–300 platforms. **Verdict: about 5.9, so the thesis is killed as a $10B lead.**

## 1. Evidence of pain

### Content abuse on generated and hosted sites (strongest evidence)
- **Lovable:**
  - Proofpoint finds tens of thousands of malicious lovable.app URLs since early 2025. One Feb 2025 campaign sent hundreds of thousands of messages to more than 5,000 organizations. Lovable added real-time detection at prompt time plus daily scanning, and promises action within 24 hours on abuse reports. [ciso2ciso.com/?p=183218; theoutpost.ai/news-story/...-19361; lovable.dev/faq/trust-and-safety/report]
  - Third-party scan, Apr 2026: 380k apps scanned, 5 brands phished on Lovable's domain. [vibe-eval.com/updates/lovable-security-report-apr-2026/]
- **Vercel:** INKY blocked more than 6,283 phishing emails abusing Vercel hosting across more than 2,030 organizations (Dec 2025–May 2026). Researchers frame v0 as collapsing attacker overhead. [kaseya.com/blog/phishing-campaigns-abusing-vercels-free-hosting-platform/; cipherssecurity.com/vercel-v0dev-phishing-ai-microsoft-cofense/]
- **Cloudflare:**
  - Fortra measured phishing on Workers up **104% YoY** and on Pages up **198% YoY**. [fortra.com/blog/cloudflares-pagesdev-and-workersdev-domains-increasingly-abused-phishing]
  - Cloudflare Drop (Jul 8 2026) allows anonymous deploys to workers.dev, with no account required for the first hour. [phishfort.com/cloudflare-drop-trusted-cdn-phishing-abuse/]
- **Replit and Netlify:** a steady flow of credential-phishing pages on replit.app and netlify.app subdomains in 2026. Replit's Fraud team "detects and shuts down phishing deployments". [tools.malwaretips.com/url-scan/...replit.app; phishdestroy.io/domain/...netlify.app; startup.jobs/staff-software-engineer-fraud-replit-3-8028470]
- **Hugging Face:** Spaces abused for malware hosting and C2:
  - the "Blitz" miner bot (2025)
  - an Android RAT with more than 6,000 commits and payloads changing every 15 minutes (Feb 2026)
  - NKAbuse via CVE-2026-39987 (Apr 2026)

  [gurucul.com/...blitz...; techrepublic.com/...hugging-face-android-rat...; bleepingcomputer.com/...marimo...nkabuse...]

### Runtime abuse (cryptomining and proxying)
- **Documented, but mostly older:**
  - Netlify's threat-intel team published a cryptominer campaign against SaaS free tiers (Sep–Nov 2024). [netlify.com/blog/netlify-threat-intelligence-brief-anatomy-of-an-abusive-cryptominer-campaign]
  - Sysdig found mining across 30+ GitHub, 2,000 Heroku and 900 Buddy accounts. GitHub said it spent "thousands of hours" on mitigations. GitLab required card verification in 2021. [sysdig.com/blog/massive-cryptomining-operation-github-actions/; about.gitlab.com/blog/prevent-crypto-mining-abuse]
  - Darktrace reports Selenium Grid misused for mining and proxyjacking. [darktrace.com/blog/...selenium-grid...]
- **Free tiers removed:**
  - Fly.io cut its free tier to a 2-hour trial, explicitly citing abuse including crypto miners.
  - Railway replaced its free tier with a $5 credit.
  - [saaspricepulse.com/blog/flyio-pricing-history; community.fly.io/t/free-tier-is-dead/20651]
- **Not found:** any public 2026 incident of mining or proxying at E2B, Modal, Daytona or Browserbase. Their usage-billed, card-on-file models appear to cap exposure. The evidence for "AI sandbox" runtime abuse is thin.

### Runaway agent loops
- One widely circulated case: four LangChain agents looped for 11 days and ran up a $47k bill. [dev.to/waxell/the-47000-agent-loop...]
- Otherwise the evidence is anecdotal blog content. The cost lands on the *customer* paying for the API, not on the platform's T&S team, so it is a different buyer.

### Hiring (abuse operations in 2026)
| Company | Role and date | Source |
|---|---|---|
| Vercel | Senior SWE, T&S, Jul 2026, ~$196k, "protect millions of developers and projects from abuse at internet scale" | job-boards.greenhouse.io/vercel/jobs/5788954004 |
| Replit | Staff SWE, Fraud | startup.jobs/staff-software-engineer-fraud-replit-3-8028470 |
| Gamma | T&S SWE covering phishing, abuse and fraud, Jul 2026 | (earlier verification) |
| GitHub | T&S engineer covering spam, malware and abuse tooling | getmatched.axented.com/.../39003324 |
| Cloudflare | T&S threat investigations | themuse.com/jobs/cloudflare/... |

Searches did **not** surface 2026 abuse or T&S postings at Netlify, Render, Railway, Fly.io, E2B, Modal or Daytona. The smaller platforms handle abuse with security generalists plus pricing gates.

## 2. Existing solutions (the opening is narrow)

| Layer | Players | Notes |
|---|---|---|
| Content scanning at creation | **Guardio embedded in Lovable** (scans every site created) [guard.io/blog/lovable-integrates-guardio...; tech.yahoo.com/...lovable-adds-safe-browsing-engine] | **This is the AI-builder wedge, already sold to the top target.** |
| Host-side threat feed and takedown | **Netcraft**: free real-time API for hosting providers since Mar 2025; 1.9h median takedown; Preemptive Domain Disruption (2026) [netcraft.com/cybercrime; forums.freebsd.org/...netcraft-launches...] | Free to hosts, funded by brand-side customers. Hard to undercut. |
| Brand-side takedown | Bolster, Doppel, Proofpoint, PhishFort, Fortra [bolster.ai/blog/netcraft-alternatives] | They create the inbound report volume that hosts must process. |
| Abuse-desk automation | **Abusix Guardian Ops** (hosting providers and ISPs): "300%+ more cases without headcount", up to 99% auto-resolved [abusix.com/blog/why-abusixs-guardian-ops...] | An incumbent in exactly this category. |
| T&S operations platforms | Cinder ($41M Series B, May 2026), SafetyKit (Character.ai, Substack, others), Musubi ($5M seed) [trysignalbase.com/news/funding/cinder-secures-410m; ycombinator.com/companies/industry/Trust & Safety; pulse2.com/musubi...] | Well funded, and could add hosting and phishing classifiers. |
| Platform-native | Cloudflare (78% of phishing reports auto-resolved, median under 1h), Vercel BotID and T&S org, Google Web Risk / Safe Browsing, VirusTotal, urlscan | The biggest hosts build and also sell these. |
| Runtime detection | Falco (open source, CNCF graduated) and Sysdig, cryptnono (2i2c), Darktrace [businesswire.com/...falco-feeds...; infrastructure.2i2c.org/.../cryptnono] | Commodity detectors. Card checks and trial credits do most of the work. |
| Agent spend caps | Portkey (hard budgets), LiteLLM, floe-guard, OpenAI hard project limits (Jul 22 2026) [waxell.ai/blog/ai-agent-token-budget-enforcement; lava.so/blog/best-ai-spend-management] | Being absorbed into gateways and model providers. |
| Signup and usage | Stripe Radar (May 2026), Verisoul, Stytch | See VERIFY_compute_fraud.md. |

## 3. Do companies still build internally?
Yes, but that has been true since at least 2021 without a dedicated vendor category emerging:
- GitHub, GitLab, Netlify (its own threat-intel team), Vercel, Replit and Cloudflare all run in-house teams.
- The persistent internal pattern reads less as an unmet need and more as a problem that is core to each platform and solved cheaply by policy (card checks, trial credits, free-tier removal) plus a few engineers.
- The one place a new vendor got traction quickly, Guardio at Lovable, was an *existing* safe-browsing company extending sideways.

## 4. Buyer count and dollar size
- **Buyers:** about 100–300 platforms with meaningful anonymous or free compute or hosting. That includes AI builders (Lovable, Bolt, v0, Replit, Base44, Gamma), sandboxes (E2B, Modal, Daytona, Browserbase and roughly 20 more), PaaS (Netlify, Render, Railway, Fly.io) and model hubs (Hugging Face). The largest (Cloudflare, Vercel, GitHub) build their own.
- **Dollars at stake per platform:** phishing costs mainly reputation and deliverability (the risk of the root domain being blocklisted), not direct dollars. Runtime abuse is capped by billing gates. I found no public figure for sandbox compute lost to miners.
- **Market size:** a plausible ACV of $50–250k gives a serviceable market of roughly **$15–75M** [E]. That is Abusix or Netcraft-hosting-feed scale, not $10B. Expansion into general T&S runs into Cinder and SafetyKit.

## Score (same 10 criteria as SYNTHESIS.md)

| Criterion | F-A original | F-A after VERIFY_compute_fraud | **F-A' runtime/content** | Justification |
|---|---|---|---|---|
| Pain today | 8 | 9 | **7** | Phishing on AI builders is well documented (Lovable, Vercel, Cloudflare up 104–198%). Runtime mining in AI sandboxes is not documented in 2026. |
| Dollars attached | 8 | 8 | **5** | Mostly reputational. Compute losses are capped by card and credit gates. No public dollar figure. |
| Headcount attached | 7 | 7 | **6** | Vercel, Replit, Gamma and GitHub have T&S teams; smaller platforms have none. |
| Growth rate of pain | 9 | 9 | **8** | Phishing on these platforms grows 2–3x YoY and anonymous deploys (Cloudflare Drop) are spreading. |
| Ease of finding buyers | 9 | 8 | **6** | They are identifiable, but the pool is small and the top ones build their own. |
| 30-day pilotability | 9 | 7 | **7** | Easy to replay content scanning against past deploys. Runtime detection needs deep host integration. |
| Existing internal builds | 9 | 6 | **8** | Builds are widespread, but they have persisted since 2021 without a vendor emerging, so the signal is ambiguous. |
| Competitive opening | 7 | 3 | **4** | Guardio is inside Lovable, Netcraft's host feed is free, Abusix covers abuse desks, Cinder and SafetyKit are well funded, and gateways cover spend caps. |
| Expansion potential | 8 | 7 | **5** | Three unrelated problems with three different buyers: T&S, infra security and FinOps. |
| $10B potential | 7 | 4 | **3** | A ~$15–75M market [E] with a commodity-feeling ceiling. |
| **Average** | **8.1** | **6.8** | **5.9** | |

## Verdict
**Killed at 5.9.** It does not hold the ~7 pre-verification estimate.
- **The content-abuse arm** is the only real pain, and Guardio (at Lovable), Netcraft (a free feed for hosts) and the platforms' own teams already cover it.
- **The runtime-abuse arm** is a solved-by-pricing problem dating from 2021, with no 2026 AI-sandbox incidents found.
- **The agent-loop arm** belongs to a different buyer and is being absorbed by gateways and model providers.

Lesson for the method: once Stripe took the cross-company signal at signup, what was left of F-A split into three niche, crowded markets. Round 32 still has no 8.5. F-B (eval and ground-truth operations, 7.8, unverified) remains the best remaining finalist.
