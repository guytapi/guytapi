# Thesis V deep dive: AI security-response team for software vendors ("PSIRT Autopilot")

*Red-team analysis, 2026-10-05. 39 web searches. Sources are cited inline. Anything marked (unverified) is an estimate or a single weak source. I did not invent any URLs.*

---

## 0. Bottom line

**VERDICT: REFRAME. The broad end-to-end version should be killed.**

- **The pain is real and severe.** The volume shock is the best-documented "why now" of any thesis we have tested.
- **Each piece of the end-to-end loop is already funded or absorbed:**
  - Intake, triage and fix plans: HackerOne and Bugcrowd.
  - Finding and patching: frontier labs (Mythos/Glasswing, Codex Security, Gemini 4 Argon, CodeMender).
  - Third-party OSS backports: Aikido+Root, Seal.
  - Mainline autofix: GitHub, Pixee, depthfirst, Corridor.
  - CRA, SBOM and VEX: Finite State, Cybellum, Sonatype.
- **The biggest buyers are building it themselves.** Microsoft, Cisco, Apple and Google run in-house pipelines on frontier models. Elastic built its own triage agent at about $2 per report.
- **What remains uncovered** is the vendor's *own-code* last mile, for vendors with many supported versions: multi-branch backport of the vendor's own fixes, regression testing per release train, advisory/CSAF/VEX, CRA 24h/72h/14d reporting, and customer notification. This matters most for on-prem, appliance, embedded and device makers.
- **That niche has problems.** It is narrower, more services-heavy, and exposed to frontier models commoditizing backporting. Advance it only if 10 interviews confirm budget of at least $100K per vendor for this specific slice.

---

## 1. Volume: the demand driver is confirmed and extreme

| Signal | Data | Source |
|---|---|---|
| CVE total | 2025 ended at a record 48,185 CVEs. FIRST mid-year forecast is about 66,000 for 2026. H1 2026 ran about 50% ahead of H1 2025. | Trend Micro "vulnpocalypse" https://www.trendmicro.com/en_us/research/26/g/making-sense-of-the-vulnpocalypse.html ; https://forkast.news/ai-is-finding-software-flaws-faster-than-the-exploit-infrastructure-can-track-or-fix-them/ |
| NVD | 45,207 entries Jan to Jul 2026. NVD fully analyzed only about 28% of 2025 CVEs. In April 2026 it moved pre-March-2026 CVEs to "Not Scheduled". | https://letsdatascience.com/news/nvd-logs-more-than-45000-vulnerabilities-through-july-27-0b8e28c2 ; Trend Micro (above) |
| AI share | FIRST names three drivers: AI-assisted discovery, GHSA volume up 449% YoY, and VulnCheck CNA-of-last-resort activity up 3,119%. There is no clean "AI-found %" figure. | Trend Micro / forkast (above) |
| Microsoft | Sept 2026 Patch Tuesday fixed 974 CVEs (966 to 997 depending on how you count), the all-time record. July/Aug fixed 570/398. | https://infosecurity-magazine.com/news/microsoft-patch-tuesday-record ; https://www.tenable.com/blog/microsofts-september-2026-patch-tuesday-addresses-964-cves-cve-2026-81963-cve-2026-85880 ; CSA note in context file |
| Linux kernel | Nearly 2,000 CVEs per release, against about 500 across the whole 6.x era. The security list went from 2 to 3 reports a week a couple of years ago to 5 to 10 a day in 2026. 432 CVEs landed in one weekend. GKH: "a very long 18 months at the least." He also says the problem is the *number* of AI reports, not their quality. | https://phoronix.com/news/Linux-Kernel-CVEs-Nearly-2000 ; https://www.noze.it/en/insights/432-linux-kernel-cves-two-days/ |
| Cisco | In July 2026 Cisco moved to a "risk-based disclosure" model. It now ships twice-monthly "hardening releases" for the many bugs its own frontier-AI work finds, and groups same-CWE bugs under umbrella CVEs. | https://sec.cloudapps.cisco.com/security/center/resources/risk-based-disclosure |
| Glasswing (Anthropic Mythos) | About 200 partners have found more than 10,000 high/critical flaws since April. Anthropic disclosed 530; 75 are patched, and 827 confirmed bugs await disclosure. **Average patch time is about 2 weeks.** In other words, fixing is the bottleneck, not finding. | https://www.implicator.ai/anthropic-adds-150-new-project-glasswing-partners-in-more-than-15-countries/ ; https://letsdatascience.com/news/anthropic-expands-project-glasswing-to-global-partners-98e03019 |
| Bounty slop | curl ended its bug bounty at the end of Jan 2026. Internet Bug Bounty paused payouts. HackerOne reports a 100%+ surge in AI-assisted submissions. | https://www.theregister.com/2026/01/21/curl_ends_bug_bounty/ ; https://www.csoonline.com/article/4154216/internet-bug-bounty-program-hits-pause-on-payouts-2.html ; https://www.hackerone.com/press-release/hackerone-launches-h1-remediation-accelerate-path-validated-exposure-verified-fix |
| Fix gap | HackerOne: the resolution rate for critical vulns fell from more than 83% to under 40% in a year, and the unresolved critical backlog grew 29x. | HackerOne H1 Remediation PR (above) |
| Not found | No public "overwhelmed" quotes were found from Apple, Oracle, Fortinet or Ivanti PSIRTs (not searched exhaustively). |  |

**Read:** volume growth is 1.5 to 4x depending on the source. This is a genuine regime change. The binding constraint has moved from discovery to *fix + backport + disclose*.

## 2. Time-to-exploit and the cost of slow response

- **VulnCheck 1H 2026:**
  - 23.4% of KEVs were exploited on or before the day the CVE was published (28.9% in 2025).
  - Median time from CVE publication to KEV fell from 120 days to 80.
  - **But only about 1.4% of CVEs become KEVs.** This undercuts the "every bug is an emergency" narrative. https://www.vulncheck.com/blog/state-of-exploitation-1h-2026
- **Other estimates** (from the context file): CSA puts mean CVE-to-exploit at about 10h; M-Trends 2026 puts time-to-exploit at -7 days.
- **Vendor damage, Ivanti** is the canonical case:
  - Q2 revenue fell 11% YoY to $189M and adjusted EBITDA fell 21%.
  - S&P downgraded it to CCC, and its $1.8B loan trades at about 36 cents.
  - CISA ordered federal agencies to disconnect Ivanti products. Critics tie the decline to slow response.
  - Sources: https://www.privateequitywire.co.uk/clearlake-backed-ivanti-reports-21-drop-in-ebitda/ ; https://www.darkreading.com/remote-workforce/ivanti-ceo-commits-to-security-overhaul-day-after-vendor-discloses-4-more-vulns
  - Causality is mixed: part of the revenue drop is the license-to-subscription transition.
- **Other cases** (MOVEit/Progress lawsuits, Citrix, Fortinet) are well known but were not re-verified in this pass.

**Read:** there is a strong fear narrative for the board ("don't become Ivanti"). The ROI for any single bug is hard to prove.

## 3. EU Cyber Resilience Act

- **From 11 Sept 2026,** manufacturers must report *actively exploited vulnerabilities* and *severe incidents* through ENISA's Single Reporting Platform, to ENISA and the coordinating CSIRT at the same time:
  - early warning within 24h;
  - notification within 72h;
  - final report within 14 days after a fix or mitigation is available (1 month for incidents).
  - Sources: https://www.jonesday.com/en/insights/2026/07/eu-cyber-resilience-act-24hour-reporting-duties-start-september-11-2026 ; https://www.traverssmith.com/knowledge/knowledge-container/the-eu-cyber-resilience-acts-vulnerability-and-incident-reporting-requirements-are-now-live/
- **From 11 Dec 2027,** full obligations apply: vulnerability handling for the whole support period, free security updates, SBOM, and coordinated disclosure policy. Source: Finite State/Sonatype guidance (search snippet).
- **How many companies are affected:** every manufacturer, importer or distributor of "products with digital elements" sold in the EU. That is likely tens of thousands (unverified; I found no official count). The reporting duty applies only to *exploited* vulns, about 1.4% of CVEs, so CRA alone creates a low-frequency, high-stakes workflow, not a volume workflow.
- **The real driver is the Dec 2027 obligation.** Security updates across the whole support period means backports to every supported version. That is the strongest structural argument for the reframed wedge.

## 4. Competitors

| Name | What | Funding / status | Overlap |
|---|---|---|---|
| **HackerOne** (Hai, H1 Remediation, Jul 29 2026) | Intake, AI validation, root cause traced to lines of code, developer-ready fix plan in the customer's codebase, pushed into Jira/AI coding agents via MCP, verified fix, exposure-duration metric | Last valued at $829M (2022). Revenue unverified. | **HIGH.** It already owns intake → triage → fix plan → retest for its customer base. https://www.hackerone.com/blog/fixing-the-fix-gap-introducing-h1-remediation |
| **Bugcrowd** (AI Triage Assistant, AI Connect MCP) | Conversational triage, remediation guidance, Nuclei retest templates, auto rescans, 98% accuracy on critical prediction | $102M raised in 2024 | **HIGH** on intake/triage. https://www.bugcrowd.com/blog/turn-vulnerability-data-into-remediation-velocity-introducing-bugcrowd-ai-triage-assistant/ |
| Intigriti, YesWeHack, Synack | Bounty/pentest platforms that will copy these features | Various | Med |
| **Anthropic Mythos / Project Glasswing** | Find + patch with about 200 partners (MSFT, Apple, Cisco, Google, AWS, Broadcom, Linux Foundation…), $100M in credits | Platform | **HIGH** for large vendors, who get the capability directly |
| **OpenAI Codex Security** (ex-Aardvark) | Find, verify, one-click patch. Research preview since Mar 2026 | Platform | High (mainline fix) |
| **Google Gemini 4 Argon** (Sept 30 2026) / CodeMender / Big Sleep | Autonomously find, validate, patch. Fairwind early-access program | Platform | High |
| **GitHub** Copilot Autofix, PVR, GHSA | Private vulnerability reporting, advisory/CVE issuance (CNA), autofix in PRs (free for OSS) | Platform | **HIGH** for the GitHub-hosted, mainline-only case |
| **Aikido** + **Root** (acquired Jun 30 2026, $70M) | Agentic backports of OSS fixes into the versions already in use (15 to 40 min) → "Aikido Libraries" | Aikido $1B valuation (Jan 2026, $60M) | Med. Third-party OSS deps, not the vendor's own code. https://siliconangle.com/2026/06/30/aikido-acquires-root-patch-open-source-without-forced-upgrades/ |
| Seal Security | Backported OSS patches plus an autonomous remediation agent (Mar 2026) | $20M total ($13M A) | Med (OSS deps) |
| Chainguard | Hardened images/libraries | $612M raised, $3.5B valuation, $40M ARR → $100M target (FY26) | Low-Med |
| Echo | CVE-free base images | $50M | Low |
| HeroDevs, TuxCare, ActiveState, Minimus | EOL/LTS patched OSS, VEX feeds | Not verified | Low-Med |
| **depthfirst** | Autonomous detect, triage, remediate | $40M A (Accel, Jan 2026) | Med-High (could move to the vendor side) |
| Corridor | AI-native software security | $25M A at $200M valuation (Mar 2026; Anthropic/OpenAI/Cursor invested) | Med |
| Pixee | Autofix/triage | $15M seed (2025) | Med |
| ZeroPath (YC) | Find + fix | $5M | Med |
| Corgea | Autofix | $2.5M seed (2024) | Low-Med |
| Mobb, Snyk Agent Fix, Semgrep Assistant, Endor Labs, Amplify, DryRun | Autofix/triage | Not verified this pass | Med |
| **Konvu** | AI agents that triage vulns with evidence; publishes on auto-reproducing bounty reports | $5M (2024); won the Infosecurity Europe 2026 startup award | Med (reproduction/triage). https://konvu.com/blog/bug-bounty-reproduction-challenge |
| Triage Security (triagesecurity.ai) | Sandbox reproduction of VDP reports, evidence packs | Unknown | **Med-High** (same wedge) |
| Backline | AI agents that auto-remediate | $9M seed (2025) | Med |
| XBOW | AI pentester, #1 on HackerOne | $120M C + $35M extension, about $1B valuation (May 2026) | Low today (finding side) |
| Theori, Trail of Bits Buttercup, RunSybil | AI discovery | Not verified | Low |
| Finite State | Device/firmware SBOM, CRA vulnerability handling | $49.5M total | Med (advisory/CRA layer) |
| Cybellum | Product security, automated VEX | $12M A+ (old) | Med |
| Sonatype, VicOne, CRA Evidence, NetRise, Manifest, Anchore, RunSafe, Interlynk, ReversingLabs | SBOM/VEX/CRA compliance | Various | Med on advisory/VEX |
| **DIY: Elastic** | Built its own AI bounty-triage agent at about $2 per report, 85% agreement with humans across 3,300 reports | Internal | **Kill signal** for the triage wedge. https://www.elastic.co/security-labs/blog/ai-vulnerability-triage-bug-bounty-hackerone |
| Academic: PortGPT | LLM backporting, 89% success on about 2,000 patches | Research | Signals that backporting becomes a commodity. https://www.helpnetsecurity.com/2025/11/05/portgpt-ai-backport-security-patches-automatically/ |

**Does anyone own the vendor's vulnerability response end to end?** Not yet, but HackerOne is about 60% of the way there, and its customer base is exactly these vendors. No YC "AI PSIRT" company was found (YC directory search was inconclusive).

**Uncovered gaps:**
1. Multi-branch backport of the vendor's *own* code with per-release-train CI.
2. Advisory/CSAF/VEX generation linked to the actual patched builds.
3. The CRA SRP reporting clock.
4. Downstream customer notification.
5. Cross-source dedupe across bounty, scanner, AI-lab disclosures (Glasswing, Big Sleep), CNA feeds and customer reports. HackerOne sees only HackerOne.

## 5. Buyer and market math

- **Buyer:** Head of PSIRT / VP Product Security, with VP Eng (release engineering) as co-signer.
  - At mid-size vendors, the PSIRT is often 1 to 3 people (unverified).
  - At the top 50 (Microsoft, Cisco…), PSIRTs number in the hundreds, those vendors have Glasswing access, and they build in-house.
- **Counts:**
  - 502 CNAs participating, about 340 active in H1 2026 (search snippet). Many are vendors.
  - About 6,000 vendors with PSIRT-like duties (context file; unverified).
  - CRA-scope manufacturers: tens of thousands (unverified).
  - **Realistic ICP:** commercial on-prem/appliance/embedded/device software vendors with 3 or more supported versions and an EU market. Estimate 1,500 to 3,000 (unverified).
- **ACV:**
  - Mid-market: $60K to $150K (platform plus per-product/version).
  - Large: $300K to $1M.
  - The cost replaced is 1 to 3 product-security engineers plus release-engineering time: $250K to $750K fully loaded.

| ARR goal | Mix needed | Share of a ~2,500 ICP |
|---|---|---|
| $10M | 100 × $100K | 4% |
| $50M | 300 × $130K + 25 × $400K | 13% |
| $100M | 500 × $140K + 60 × $500K | 22% plus big logos (the hardest part, since big logos build in-house) |

**Read:** $10M is plausible. $100M needs either a very high share of a narrow ICP, or expansion into enterprise-side consumption of the advisories/VEX (a crowded space) or into OSS-dependent enterprises (where Aikido/Root, Seal and Chainguard already are).

- **90-day pilot:** replay the last 12 months of inbound reports and fixes. Metrics:
  - dedupe/slop precision and recall against human decisions (Elastic's bar is 85%);
  - auto-reproduction rate;
  - % of fixes auto-backported to all supported branches with green CI;
  - draft advisory/CSAF/VEX accepted with light edits;
  - median report-to-shipped-patch time.

  This is fast and data-rich, *if* the vendor grants source and CI access. That is the gating issue: product code is the crown jewel.

## 6. Moat

- **Claimed:** a cross-vendor dataset of reports, exploits and fixes; dedupe across vendors (the same bug in a shared OSS component reported to many vendors); researcher reputation; system of record for product security.
- **Reality check:**
  - **Researcher reputation and the cross-vendor report graph already belong to HackerOne and Bugcrowd.**
  - The fix data is the vendor's private code, which is non-pooling by contract.
  - Backport skill is model capability (PortGPT 89% in 2025, better now), so it commoditizes.
  - The best defensible asset is the **system of record for "which of our versions are affected, fixed, notified, reported to ENISA"**: workflow lock-in plus regulatory audit trail. That is moderate defensibility, the same kind of moat Jira-for-PSIRT tools have, and not a data network effect.

## 7. Expansion path to $100M+

1. Wedge: backport + advisory/CRA autopilot for multi-version on-prem/device vendors.
2. Add intake/dedupe across all sources, sitting on top of HackerOne/Bugcrowd rather than competing with them.
3. Customer-side distribution: machine-readable VEX/CSAF feeds to the vendor's enterprise customers. Two-sided, giving a possible network effect where enterprises pull vendors in.
4. Extend-support-as-a-service: patching EOL versions for vendors' customers (HeroDevs-like economics).
5. Medical/automotive/OT verticals (FDA 524B, UN R155) at higher ACV.

Each step meets an incumbent: HackerOne at step 2, Finite State/Cybellum/Sonatype at step 3, HeroDevs/TuxCare at step 4, Cybellum/VicOne at step 5.

## 8. Kill signals

| Signal | Status |
|---|---|
| Platform bundling | **Firing.** HackerOne H1 Remediation (Jul 2026), Bugcrowd AI Triage, GitHub Autofix free for OSS, Codex Security, Gemini 4 Argon (Sept 30 2026), Mythos via Glasswing |
| Big vendors build in-house | **Firing.** Cisco hardening releases from in-house frontier-AI work; Elastic's DIY triage at $2 per report; Glasswing partners get models directly |
| Backport commoditized / acquired | **Firing for OSS deps** (Aikido bought Root for $70M; Seal). Open for the vendor's own code |
| Vendors refuse AI-written patches | Partial. Every player (Seal, CodeMender, Elastic) keeps a human in the loop, so this is a speed limit, not a blocker |
| Few buyers with big budgets | **Likely.** The top 50 build in-house. The mid-market has small PSIRTs, so ACV pressure pushes toward $50 to 80K |
| Services-heavy | **Likely.** Each vendor's build/CI/release trains are bespoke, so onboarding looks like professional services |
| Only ~1.4% of CVEs get exploited | Weakens the "hours" urgency for most bugs. The real urgency is the CRA clock plus the long tail of volume |

## 9. Sharpened thesis (the reframe)

> **"Release engineering for security fixes."** For on-prem, appliance and embedded software vendors that support many versions at once: when a fix lands on main (from HackerOne, Glasswing, an internal AI scan, anywhere), we backport it to every supported branch, run each release train's CI, assemble the patched builds, generate the CSAF advisory and VEX for exactly the affected versions, file the CRA 24h/72h/14d reports, and notify affected customers. That turns a two-week patch into a same-day patch. **We sit downstream of HackerOne, not against it.**

Why this version might survive:
- It is downstream of where HackerOne stops (the fix plan).
- GitHub Autofix only does mainline.
- Root and Seal patch third-party OSS, not vendor code.
- Glasswing's two-week average patch time shows the bottleneck.

Why it might still die:
- Frontier-model coding agents plus a vendor's own release engineers may make this a script, not a company.
- HackerOne could add "backport + advisory" within a year.

## 10. CTO cold message and simulated reaction

> Subject: Your 2-week patch time vs. the CRA 24-hour clock
>
> Hi [Name]. Kernel CVEs went from about 500 per era to about 2,000 per release, and Microsoft shipped 974 fixes in September. The bottleneck isn't finding bugs, it's shipping the fix to every version you support. We take a merged fix on main, backport it to all your supported branches, run each branch's CI, and produce the CSAF/VEX advisory and CRA report automatically, with your engineers approving every patch. Pilot: we replay your last 12 months of security fixes and show which backports we'd have shipped green and how many days we'd have saved. 30 minutes?

**Simulated reaction** (CTO, $300M on-prem infrastructure software vendor, 4 supported major versions):
> "Backports are genuinely our worst toil. Our release team spent most of Q3 on security trains. But I'm not giving an outside startup write access to our source and build farm. And HackerOne just pitched me 'fix plans', and Claude Code is already in our repo. Show me it works on our branches *on-prem / in our VPC*, and price it under one headcount. Replay pilot, maybe."

→ **MAYBE**. Pain is acknowledged. The deployment model (in-VPC) and the "why not our own agent" question are the gates.

## 11. Five simulated buyers

| # | Profile | Reaction | Why |
|---|---|---|---|
| 1 | Head of PSIRT, Fortune-100 networking vendor (Glasswing partner) | **NO** | Has Mythos access and a 100+ person PSIRT, and is building internal hardening-release pipelines like Cisco's. Won't let a vendor touch source. |
| 2 | VP Product Security, $400M on-prem storage/backup ISV, 5 supported versions, sells into the EU | **YES (pilot)** | Backport toil plus the CRA support-period obligation from Dec 2027. 3-person PSIRT. Would pay about $150K if it runs in-VPC. |
| 3 | CISO, $80M B2B SaaS (single version, continuous deploy) | **NO** | No backports. HackerOne plus Copilot Autofix cover it. Triage noise is solved by H1/Bugcrowd AI. |
| 4 | Product security lead, industrial IoT/OT device maker (firmware, 10-year support) | **MAYBE→YES** | Huge version matrix, CRA reporting, IEC 62443. But the code is C/RTOS, so CI/hardware-in-loop testing is hard and the work is services-heavy. Would buy the advisory/CRA part first. |
| 5 | Director of Security Response, mid-size open-core company (OSS project plus enterprise LTS) | **MAYBE** | Flooded by AI reports on the OSS side (curl-like). Would want the dedupe plus LTS backports. Budget around $60K. Might DIY with Claude Code. |

Result: 1 YES, 2 MAYBE, 2 NO. The positive signal is concentrated in **multi-version on-prem/device vendors**, not SaaS and not mega-vendors.

## 12. Scores (1 to 10)

| Dimension | Score | Note |
|---|---|---|
| Pain | 8 | Volume shock is extremely well documented; Glasswing's 2-week patch average |
| Urgency | 7 | CRA live since Sept 11 2026; but only about 1.4% of CVEs are exploited |
| ROI clarity | 6 | Headcount and days-to-patch are measurable; avoided breach cost is fuzzy |
| Customer accessibility | 5 | PSIRT heads are reachable, but source/CI access is a big ask |
| Pilot speed | 6 | Replaying history is fast once access is granted; integration per build system is slow |
| Market size | 5 | Narrow ICP of about 1,500 to 3,000; $100M needs about 20% share |
| Expansion | 6 | VEX feeds to customers, EOL support, regulated verticals |
| Venture potential | 5 | Plausible $30 to 50M ARR outcome or acquisition by HackerOne/Aikido/Snyk |
| Defensibility | 3 | Model capability commoditizes; the report graph belongs to H1/Bugcrowd |
| Why now | 9 | Best in the portfolio |
| Competition position | 3 | HackerOne H1 Remediation, frontier labs, Aikido+Root, depthfirst all adjacent and well funded |
| **Average** | **~5.7** | |

## 13. VERDICT: REFRAME (kill the broad end-to-end version)

- **Kill:** "own the whole loop from intake to fix."
  - HackerOne and Bugcrowd own intake and triage, and added fix plans in July 2026.
  - Frontier labs give large vendors find-and-patch directly.
  - Aikido bought Root for OSS backports.
  - The SaaS majority doesn't need backports.
- **Possible survivor:** security-fix release engineering + CRA/advisory autopilot for multi-version on-prem/embedded vendors, deployed in-VPC and positioned downstream of HackerOne.
- **Gate before investing more:** 10 interviews with this ICP. Advance only if:
  - 5 or more confirm backport/advisory toil above 1 FTE;
  - they confirm willingness to pay at least $100K;
  - they confirm willingness to grant in-VPC source/CI access.
- **Also test:** whether HackerOne's roadmap includes multi-branch backports. If it does, kill.
