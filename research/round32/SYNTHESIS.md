# Round 32 synthesis: 53 companies → 15 hidden pain clusters → 5 finalists

Sources: companies_A_coding.md (10), companies_B_apps.md (10), companies_C_infra.md (11), companies_D_saas_sec.md (11), companies_E_vertical.md (11). About 100 searches; snippets only, no page fetches. [E] marks an estimate. Company evidence and citations are in the source files.

## 15 hidden pain clusters (ranked by number of companies)

| # | Cluster | Companies showing it | Built internally | Counts as "new human work"? |
|---|---|---|---|---|
| 1 | **Eval and ground-truth operations**: evals, judge calibration, expert labels, trace review turned into tests, regression on model upgrades | Notion, Vanta, Semgrep, PostHog, Zapier, Retool, Sierra, Decagon, Intercom, Harvey, ElevenLabs, Canva, Shopify, DoorDash, Duolingo, Figma, Uber, Instacart, Linear (19) | 17 | Yes |
| 2 | **AI usage metering, pricing redesign, billing disputes** | Cursor, Augment, Bolt, Replit, Amp, Notion, Sentry, Retool, Airtable, Pinecone, OpenRouter, Neon, Temporal, Clay (14) | ~9 | Partly |
| 3 | **Inference cost reduction**: routing, distillation, self-hosting, batch | Intercom, Hebbia, Writer, Clay, Cursor, Linear, Airtable, Notion, Instacart, Canva, Uber, OpenRouter (12) | 10 | No |
| 4 | **Abuse and fraud on AI compute**: free-tier and credit abuse, payment fraud, phishing hosted on generated sites, use-case vetting | Replit, Lovable, Vercel, Supabase, Augment, Amp, Browserbase, Neon, E2B (9) | 7 | Yes (new T&S teams) |
| 5 | **Expert human review queues for AI output** | EvenUp, Duolingo, Instacart, DoorDash, Shopify, Figma, Vanta, Semgrep, Snyk, Linear, Harvey (11) | 7 | Yes |
| 6 | **Forward-deployed implementation**: turning each customer's SOPs into a configured agent | Harvey, Decagon, Sierra, ElevenLabs, Writer, Cognition, Factory, Fireworks, Baseten (9) | 3 with tooling; the rest is people | Yes (largest headcount) |
| 7 | **Sandboxes and execution environments** | Cognition, Replit, Vercel, Bolt, Cursor, E2B, Browserbase, Modal, Ramp, Figma (10) | 9 | No |
| 8 | **Internal LLM gateway and cost attribution** | Uber, Instacart, DoorDash, Shopify, Retool, Notion, Linear (7) | 5 | No |
| 9 | **BYOC / self-hosted enterprise deployment** | Baseten, Fireworks, LangChain, Pinecone, E2B, Cognition, Glean, Harvey (8) | 6 | Partly (support load) |
| 10 | **Review of generated code** | Uber, Ramp, Semgrep, Snyk, Sentry, Lovable (6) | 5 | Yes |
| 11 | **Internal agent platform rebuilt and consolidated** | Ramp, DoorDash, Figma, Uber, Zapier, Retool (6) | 6 | No |
| 12 | **Runtime guardrails and agent permissions** | DoorDash, Shopify, Uber, Snyk, Wiz, Linear (6) | 4 | Partly |
| 13 | **GPU capacity procurement and fleet health** | Modal, Baseten, Together, Fireworks, Cursor (5) | 3 | Yes (weekend fault watchers) |
| 14 | **Enterprise trust paperwork for AI**: questionnaires, residency, ZDR | Perplexity, Harvey, Glean, Vanta, Cursor, Factory (6) | 3 | Yes |
| 15 | **Fleets of agent-created resources**: DBs, sandboxes, sprawl | Supabase (1M+ DBs a week, 60% by AI tools), Neon (80%+ by agents), Replit, E2B, Browserbase (5) | 3 | Partly |

Clusters 1, 4, 5 and 6 match the requested shape: "we deployed AI, but now we need humans to …". Clusters 3, 7, 8 and 11 are infrastructure that every company rebuilds, but well-funded vendors exist and buyers are engineers (F1/F2 from the round-18 taxonomy).

## The 5 finalists (strongest money evidence)

### F-A. Fraud and abuse on AI compute (cluster 4)
- **PROBLEM:** every AI product that gives away compute (free tiers, trial credits, sandboxes, hosting) is farmed by abusers, and each loss is a direct GPU or token bill.
- **EVIDENCE:**
  - Replit started an Anti-Abuse & Security team in May 2026 (EM $210–275k; Staff Fraud/Risk $250–315k).
  - Lovable is hiring to build "the fraud platform that protects payments, credits, and free tier" (Aug 2026).
  - Vercel has a full T&S engineering org with a director and an abuse-ops lead, and v0 was used to clone an Okta login page (Axios, Jul 2025).
  - On Augment, one $250-plan user consumed ~$15k a month (Augment blog, Oct 2025).
  - Supabase auto-pauses and throttles projects; Browserbase runs manual KYC on large use cases; Neon caps agent plans.
- **WHY NOW:** in classic SaaS a free user cost cents. In AI products a free user can burn dollars an hour in GPU and tokens, and generated apps make phishing sites free to build.
- **SCALING LAW:** grows with signups × compute per session; agentic sessions run longer and cost more each quarter.
- **ECONOMIC COST [E]:** 4–10 FTE trust-and-safety and fraud engineers per company ($1.5–3.5M), plus abuse-burned compute at 5–20% of free-tier inference, i.e. $1M–$20M+ a year at a scaled AI app.
- **CURRENT SOLUTION:** a new in-house team, scripts, manual review, Stripe Radar for the card only (it doesn't see compute usage).
- **BUYER:** Head of Trust & Safety, Head of Growth, or the CFO (GPU bill).
- **WEDGE:** an API scoring each signup and session for abuse risk, using compute-usage patterns, device and payment signals and a shared cross-company abuser graph, with throttle/verify/block actions.
- **30-DAY PILOT:** replay 90 days of signups and usage, then run in shadow mode. Prove the dollars of compute consumed by accounts we flag, and the false-positive rate.
- **EXPANSION:** a trust layer for all AI consumption, covering agent traffic, agent payments, account farms and generated-content hosting abuse. Cross-customer network effect: an abuser seen at Lovable is blocked at Replit.
- **COMPETITION:** Stripe Radar (payments only), Sift, Castle, Fingerprint, Arkose, Cloudflare bot management, Persona (KYC). None prices the risk in GPU dollars. Not yet verified for AI-specific startups (deliberately, per method); verification is the next step.
- **WHY THERE IS AN OPENING:** at least 3 companies are staffing new in-house fraud platforms *in 2026* despite all those vendors. That is the "still building internally" signal.
- **EMAIL CLAIM:**
  > "Abusers burn 5–20% of your free-tier GPU spend. We find it in 30 days from your own logs and cut it by 70%, without hiring a fraud team."

### F-B. Eval and ground-truth operations (cluster 1)
- **PROBLEM:** every AI product team spends most of its AI engineering time producing ground truth (labels, rubrics, calibrated judges) and re-running it on every model change.
- **EVIDENCE:**
  - Notion: "10% prompting, 90% evaluating" across ~70 AI engineers, plus a new "Model Behavior Engineer" job family and contract labelers.
  - Canva: a dedicated Evaluation Platform team.
  - Shopify: judge vs. human agreement 0.61 against a 0.69 expert ceiling, with 3+ expert labelers.
  - Vanta: a talk titled "Why building eval platforms is hard".
  - Harvey: BigLaw Bench graded by lawyers.
  - PostHog: a weekly manual "Traces Hour".
  - Uber, DoorDash, Duolingo, Instacart, Figma, Sierra, Decagon, ElevenLabs and Intercom all built their own.
- **WHY NOW:** a model upgrade every 1–3 months forces re-validation, and agent behavior can't be unit-tested.
- **SCALING LAW:** grows with AI features × model releases × customer-specific configurations.
- **ECONOMIC COST [E]:** 30–60% of AI engineering time; at a 50-AI-engineer company that is $5–10M a year, plus expert labelers.
- **CURRENT SOLUTION:** in-house platforms, sometimes on top of Braintrust or LangSmith, plus contractors.
- **BUYER:** Head of AI / VP Engineering.
- **WEDGE:** a managed, expert-calibrated judge for one domain, delivered as an SLA ("agreement with your experts ≥ 0.85").
- **30-DAY PILOT:** replace X hours a week of expert labeling with a judge at a measured agreement level.
- **EXPANSION:** the quality system of record for AI products.
- **COMPETITION:** Braintrust, LangSmith, Arize, Galileo, Patronus on tooling; Scale, Surge and Mercor on human data.
- **WHY THERE IS AN OPENING:** 17 of 19 companies still built their own despite those vendors. But the opening is "domain ground truth", which is service-heavy.
- **EMAIL CLAIM:**
  > "Your AI engineers spend over half their time on evals. We cut the expert-labeling hours behind each model upgrade by 70% and get you to production in days."

### F-C. Forward-deployed implementation (cluster 6)
- **PROBLEM:** AI-agent vendors need roughly one engineer per enterprise deployment to turn customer SOPs, systems and policies into a working agent.
- **EVIDENCE:**
  - Harvey has ~180 legal engineers, ≈$54M a year [E].
  - At Decagon, 25 of 55 engineering openings are deployment roles.
  - Sierra has ~20 "Agent Engineer" job variants across 10 cities.
  - ElevenLabs reposted its FDE role in 8+ regions; Cognition and Factory post repeated deployment-engineer roles.
  - Fireworks and Baseten also hire forward-deployed engineers.
- **SCALING LAW:** linear with enterprise customers, which is what keeps these companies' gross margins services-like.
- **ECONOMIC COST [E]:** 20–40% of headcount at agent-app companies.
- **CURRENT SOLUTION:** people, plus proprietary SDKs (Sierra ADLC, Decagon AOPs).
- **BUYER:** COO / VP Deployment at AI-app vendors (a few hundred companies), later enterprises building agents in-house.
- **WEDGE:** turn SOP documents, call logs and tickets into a tested agent spec and eval suite.
- **COMPETITION:** each vendor's own SDK; agent-builder platforms.
- **WHY IT IS WEAK:** this is the vendors' core IP, and the buyer pool today is small (F4/F5 risk).
- **EMAIL CLAIM:**
  > "Each deployment takes 6 weeks of a $300k engineer. We cut it to 1 week, so one deployment engineer covers 4× the customers."

### F-D. Expert human review queues (cluster 5)
- **PROBLEM:** AI output in specialist domains still needs a credentialed human to approve the low-confidence share, and that queue grows with volume.
- **EVIDENCE:** EvenUp has 100+ legal and medical reviewers; Duolingo's learning designers review all generated content; Instacart sends low-confidence outputs to humans; DoorDash escalates guardrail failures; Vanta has GRC experts; Snyk has analysts; Semgrep has a research team.
- **COST [E]:** 10–100+ reviewers per company.
- **WEDGE:** confidence routing plus reviewer workflow and quality control.
- **COMPETITION:** Scale, Surge, Mercor, Labelbox, Snorkel, and BPO firms.
- **EMAIL CLAIM:**
  > "Cut the share of AI output your experts must review from 40% to 10% at the same error rate."

### F-E. Inference cost reduction via distillation (cluster 3)
- **EVIDENCE:** Intercom moved a $250K/month GPT summarization workload to a fine-tuned Qwen 14B (Chain of Thought podcast, Fergal Reid); its reranker cut reranking cost 80%; Hebbia, Writer, Cursor, Linear, Instacart (Maple batch saves ~50%) and Canva show the same.
- **COMPETITION:** OpenPipe (acquired by CoreWeave), Predibase (acquired by Rubrik), and fine-tuning from Fireworks/Together. Category exits so far are acquisitions, not $10B outcomes, and labs keep cutting prices (F1).
- **EMAIL CLAIM:**
  > "We move your top 3 LLM workloads to a distilled model and cut that inference bill by 70% in 30 days."

## Final ranking (1–10)

| Criterion | F-A Compute fraud | F-B Eval/ground truth | F-C Deployment | F-D Review queues | F-E Distillation |
|---|---|---|---|---|---|
| Pain today | 8 | 8 | 9 | 8 | 7 |
| Dollars attached | 8 | 9 | 9 | 8 | 8 |
| Headcount attached | 7 | 9 | 10 | 9 | 4 |
| Growth rate of pain | 9 | 8 | 8 | 8 | 7 |
| Ease of finding buyers | 9 | 8 | 6 | 6 | 7 |
| 30-day pilotability | 9 | 6 | 5 | 6 | 8 |
| Existing internal builds | 9 | 10 | 7 | 7 | 6 |
| Competitive opening | 7 | 5 | 7 | 5 | 4 |
| Expansion potential | 8 | 8 | 6 | 7 | 6 |
| $10B potential | 7 | 7 | 5 | 6 | 5 |
| **Average** | **8.1** | **7.8** | **7.2** | **7.0** | **6.2** |

## Verdict
- **Leader: F-A, "Stripe Radar for AI compute"**, at 8.1 before verification. That is the highest score in 32 rounds and the first lead that came from repeated company behavior rather than desk ideation. It is easy to explain ("abusers are burning your GPU bill"), is directional (every AI product gives away compute, and agents make the problem grow), and has clear buyers who are hiring for this right now.
- **Not yet 8.5.** Two checks are open:
  1. Are there already AI-compute-specific fraud startups, or a Stripe/Cloudflare launch, that close the opening?
  2. Is abuse-burned compute really ≥5% of free-tier spend at more than a handful of companies?
- F-B is the strongest "still building internally" signal (17 of 19), but vendors are well funded and the gap is service-heavy.

## Post-verification update (VERIFY_compute_fraud.md)
F-A drops from **8.1 to 6.8**. The pain is confirmed and larger than assumed: 1 in 6 AI signups are tied to multi-account abuse, and Anthropic disabled 1.45M accounts in H2 2025. But the opening is closed:
- Stripe Radar Sessions (May 2026) covers trial and usage abuse on any processor, with a network graph; it saved ~$4.4M of compute across 4 AI companies in 2 months.
- Verisoul (Series A) already serves Augment and Clay.
- Stytch, Clerk and Vercel BotID already serve Replit and others.

Lesson: the method found the right pain, about 12 months late, because Stripe watches the same signals across its network.

What survives: abuse *after* signup that Stripe doesn't see (cryptomining or proxy abuse in sandboxes, phishing hosted on generated sites, runaway agent token loops). Estimated ~7, unverified.

**Round 32 result: no 8.5.** The best verified finalist is now F-B (eval/ground truth, 7.8 before verification, with a known weak opening).

## Final verification results
| Finalist | Pre-check | Verified | Killer |
|---|---|---|---|
| F-A compute fraud | 8.1 | 6.8 | Stripe Radar Sessions (May 2026), Verisoul, Stytch, Clerk |
| F-A' runtime abuse after signup | ~7 | 5.9 | Guardio (built into Lovable), Netcraft, Abusix, Cinder; 100–300 buyers |
| F-B eval / ground truth | 7.8 | 5.9 | Braintrust, LangSmith, Snorkel, Scale; hybrid builds on vendors; $0.1–1.5M addressable per company |
| F-C forward-deployed implementation | 7.2 | 5.9 | Sierra Ghostwriter, Decagon AOP Copilot, Harvey Workflow Builder; June ($20M), Interloom; vendors keep it as core IP |
| F-D expert review queues | 7.0 | not verified | Scale/Surge/Mercor/Snorkel |

**Round 32 result: no outcome A.** The company-level method found real repeated pains. But each one that is visible enough to show up across 5+ companies through public evidence (job posts, blogs) is also visible to vendors, who already serve it.
