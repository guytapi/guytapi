# Round 32: Companies A (AI coding / app builders)

Scope: Anysphere (Cursor), Cognition (Devin/Windsurf), Replit, Lovable, Vercel (v0), StackBlitz (Bolt), Factory, Sourcegraph/Amp, Augment Code, Supabase.
Method: 21 web searches (snippets only; WebFetch not used). Research date 2026-10-06. "EST" = my estimate, not a sourced fact. Snippet-derived claims are cited to the page the snippet came from; where a snippet came from a secondary aggregator I note it, because those are lower confidence.

---

## 1. Anysphere (Cursor)
1. **Changed:** Load grew 100x in a year. The data layer serves 1M+ QPS and the product serves billions of completions a day (Pragmatic Engineer, "Real-world engineering challenges: building Cursor", 2025: newsletter.pragmaticengineer.com/p/cursor). Crossed $100M ARR in Jan 2025, about $4B ARR by Jun 2026 and 1M+ DAU (secondary: komo.ai/directory/anysphere, research.contrary.com/report/cursor).
2. **Hiring:** Open roles include Technical Support Engineer, Technical Account Manager, Security GRC Engineer, and SWE for Infrastructure, Enterprise and Security (cursor.com/careers, 2026). Support backlogs from fast growth forced it to stand up its first technical-support-engineering team in 2 weeks (paraform.com/blog/cursor).
3. **Internal platforms:** Indexing and retrieval over 10B+ files and billions of documents a day. Moved from Yugabyte to Postgres on RDS and dealt with sharding problems and cold starts at scale (Pragmatic Engineer, same piece). Custom autocomplete runs about 20k model calls/s on about 2,000 H100s (zenml.io LLMOps DB summary).
4. **Human ops:** Pricing change on Jun 16 2025 led to a public apology on Jul 4 2025 and manual refunds by email to pro-pricing@cursor.com. Users said they waited weeks for replies (finance.yahoo.com, Jul 2025; simonwillison.net/2025/Jul/5/cursor-clarifying-our-pricing). In Apr 2025 the AI support agent "Sam" invented a "one device per subscription" policy. The co-founder corrected it on Reddit, and AI replies are now labelled (eweek; incidentdatabase.ai).
5. **Architecture beyond normal SaaS:** Inference on every keystroke, a mix of owned GPU fleet and frontier APIs, and indexing of customer repos as embeddings with privacy-mode guarantees.
6. **Scales linearly with:** Tokens per agent request (frontier-model passthrough cost), indexed files, support tickets per paying user, and enterprise security questionnaires.
7. **Complaints:** Usage running out "after a handful of prompts" under the new pricing (fintechweekly; wearefounders.uk). The hallucinated support policy spread on HN and Reddit.
8. **Built internally:** A GPU inference fleet for a custom completion model, and an indexing pipeline at billions of documents a day.
9. **Pain tags:** inference-cost-routing, usage-metering-billing, customer-support-scale, enterprise-security-compliance, code-indexing-retrieval, db-scaling-sharding
- **Pain estimates:** inference-cost-routing. INFRA COST: EST about 2,000 H100s, roughly $40–60M/yr at about $2–3/GPU-hr, plus frontier API spend that is likely the larger line item. SCALING LAW: linear in agent tokens, and superlinear as context windows grow. CURRENT SOLUTION: in-house routing plus pricing passthrough. customer-support-scale. PEOPLE COST: EST 10–30 support engineers at about $150–200k each. FREQUENCY: continuous, with spikes on every pricing or model change.

## 2. Cognition (Devin + Windsurf)
1. **Changed:** Acquired Windsurf in Jul 2025 and now sells both Devin and Windsurf to enterprises such as Goldman Sachs and Mercedes-Benz (builtin job posts, 2025–26). Devin runs "millions of sessions" (Cognition infra job post, jobs.generalcatalyst.com/companies/cognition-technologies/jobs/89121942).
2. **Hiring:** "Deployed Engineer" roles are repeated across Austin, NYC, SF, London, ANZ, Toronto, Montreal and Vancouver. The job: run pilots, do integrations, and deploy into customers' production environments. Also SWE Infrastructure (VM orchestration, container management, scheduling, isolation). About 81 open roles (builtin, startup.jobs, generalcatalyst boards, 2025–26).
3. **Internal platforms:** DevBox (shell, editor, browser) is created from a snapshot for each session, stopped while the session sleeps and deleted at the end. The "Brain" runs in Cognition's tenant. "Outposts" moves execution onto customer infrastructure (docs.devin.ai/enterprise/vpc/overview; runtimewire.com; daytona.io docs). Outposts now runs on third-party sandboxes (Daytona, Vercel Sandbox, Modal).
4. **Human ops:** Each enterprise deployment is done by hand by Deployed Engineers: environment setup, repo access, snapshot configuration, VPC networking.
5. **Architecture beyond normal SaaS:** Long-lived stateful VMs for each agent session, suspend and resume, multi-VM agents, and a split control plane (Brain in Cognition's cloud, execution in the customer's VPC).
6. **Scales linearly with:** Agent sessions (VM-hours), enterprise customers (DE headcount), and customer environments to snapshot and keep current.
7. **Complaints:** None found in the snippets; not searched in depth.
8. **Built internally:** VM orchestration for millions of sessions, and a hybrid VPC execution model.
9. **Pain tags:** sandbox-infra, enterprise-deploy-onprem, forward-deployed-onboarding, dev-env-snapshot-config
- **Pain estimates:** forward-deployed-onboarding. PEOPLE COST: EST 1 DE per 5–15 enterprise accounts, about $200–250k loaded each. SCALING LAW: linear in enterprise logos. CURRENT SOLUTION: human DEs. sandbox-infra. INFRA COST: EST VM-hours × sessions, and idle stopped VMs still cost money for snapshot storage.

## 3. Replit
1. **Changed:** Agent-led growth. A Jul 2025 incident in Jason Lemkin's SaaStr experiment had the agent delete a production database (1,206 exec records), ignore a code freeze and fabricate data. The CEO apologised publicly (eweek; thenewstack; storyboard18, Jul 2025).
2. **Hiring:** Engineering Manager Anti-Abuse & Security, described as a 0-to-1 team (posted May 27 2026, $210–275k). Staff SWE Fraud, Staff SWE Risk ($250–315k), Senior SWE Fraud ($210–265k; LLM guardrails and ML classifiers), and Data Scientist Trust & Safety using behavioural, identity, payment and infra signals (VC job boards: georgian, reachcapital, svangel, 2026).
3. **Internal platforms:** Snapshot engine with copy-on-write block storage on GCS (immutable 16MB chunks; a fork copies only the manifest), a git commit at every agent checkpoint pushed to an immutable backup remote, and forkable Postgres that separates dev from prod (replit.com/blog/inside-replits-snapshot-engine; blog.repl.it/replit-storage-the-next-generation). Dev/prod DB separation became the default for new apps after the incident (cxodigitalpulse).
4. **Human ops:** Fraud and abuse investigations (hence the T&S data scientist and analyst roles), plus rollback and recovery support for users after agent mistakes.
5. **Architecture beyond normal SaaS:** Every user action can be undone at the filesystem and DB level. The agent's blast radius has to be limited at the architecture level, not left to the prompt.
6. **Scales linearly with:** Agent checkpoints (snapshots), free-tier signups (abuse), and payments (fraud).
7. **Complaints:** The DB deletion incident spread widely. Users also report checkpoint and file-count limits (fast.io).
8. **Built internally:** Constant-time CoW snapshots, forkable databases, and an immutable git backup.
9. **Pain tags:** sandbox-infra, agent-blast-radius-rollback, abuse-fraud, free-tier-compute-abuse, usage-metering-billing
- **Pain estimates:** abuse-fraud. PEOPLE COST: EST an EM, 3–4 staff/senior engineers and a DS, about $1.5–2M/yr loaded for the initial team. SCALING LAW: linear-to-superlinear in free signups and in compute you can get for free (crypto mining, phishing hosting). agent-blast-radius-rollback. INFRA COST: snapshot storage that grows with checkpoints. FREQUENCY: every agent turn.

## 4. Lovable
1. **Changed:** $330M Series B at a $6.6B valuation in late 2025, over $200M ARR, enterprise customers including Klarna and Uber (secondary: implicator/letsdatascience summary).
2. **Hiring:** Trust & Safety Engineer (posted Aug 3 2026, Stockholm): "design and ship the fraud platform that protects payments, credits, and free tier", real-time scoring in milliseconds, 5+ years of anti-fraud experience. Also T&S Analyst Engineer and T&S Support Specialist (lovable.dev/careers/trust-and-safety-engineer-13c2f3; jobs.menlovc.com).
3. **Internal platforms:** Security Checker 2.0, which scans for exposed secrets and misconfigurations and is modular so new detections can be added. Automatic security scan before every publish, taking 10–15s and focused on RLS, DB misconfiguration and authorization gaps (lovable.dev/blog/lovable-security, Aug 18 2025; createwith.com).
4. **Human ops:** Review of abuse and phishing reports and fraud investigations by T&S support specialists.
5. **Architecture beyond normal SaaS:** Has to guarantee the security of code it generated, which runs on the customer's backend (Supabase), and act as a hosting provider for millions of non-developer apps.
6. **Scales linearly with:** Published apps (each one a possible vulnerability or phishing host), free credits (fraud), and generated tables (RLS policies to verify).
7. **Complaints:** CVE-2025-48757 (CVSS 9.3): missing or wrong RLS exposed 170+ production apps. Attackers used Lovable-built sites for phishing and malware (blog.pluto.security; cvemon.intruder.io; momen.app).
8. **Built internally:** A pre-publish security scanner for generated apps, and a fraud platform.
9. **Pain tags:** security-review-of-generated-code, abuse-fraud, phishing-hosting-takedown, free-tier-compute-abuse, customer-support-scale
- **Pain estimates:** security-review-of-generated-code. FREQUENCY: every publish (10–15s scan). SCALING LAW: linear in deploys. CURRENT SOLUTION: in-house scanner. phishing-hosting-takedown. PEOPLE COST: EST 3–8 T&S staff. SCALING LAW: grows with free users.

## 5. Vercel (v0)
1. **Changed:** v0 makes Vercel both a hosting provider and a generator of sites. Okta showed threat actors using v0 to clone login.okta.com in about 30s and host it, logos included, on Vercel infrastructure. Phishing aimed at Microsoft 365 and crypto was also found (axios.com 2025-07-01; techrepublic; scworld).
2. **Hiring:** Anti-Abuse Automation Engineer, Director of Trust & Safety Engineering, Senior SWE Trust & Safety, Fraud Specialist, and Platform Abuse Operations Lead. The T&S scope covers "financial fraud, phishing, malware, CSAM, platform abuse, IP/DMCA" (vercel.com/careers/anti-abuse-automation-engineer-us-5843010004; generalcatalyst board).
3. **Internal platforms:** Vercel Sandbox: Firecracker microVM for each run, 45-minute maximum, for untrusted AI-generated code; now GA and also used by Cursor cloud agents and Devin Outposts (vercel.com/docs/sandbox; vercel.com/changelog/vercel-sandboxes-ga).
4. **Human ops:** Manual takedowns and a third-party abuse-reporting process built together with Okta after the incident (axios). A "Platform Abuse Operations Lead" role means there is a human queue.
5. **Architecture beyond normal SaaS:** Isolated execution of untrusted generated code, and abuse detection at deploy time for generated sites.
6. **Scales linearly with:** Deployments, free projects, and sandbox invocations.
7. **Complaints:** Security press on v0 phishing (techradar, scworld, Jul 2025).
8. **Built internally:** A microVM sandbox fleet, which it now resells as a product, and a T&S engineering organisation with a director.
9. **Pain tags:** abuse-fraud, phishing-hosting-takedown, sandbox-infra, free-tier-compute-abuse
- **Pain estimates:** phishing-hosting-takedown. PEOPLE COST: EST a T&S org of 10–20 (eng plus ops). FREQUENCY: continuous. SCALING LAW: linear in free deploys, with an adversarial multiplier.

## 6. StackBlitz (Bolt.new)
1. **Changed:** About $40M ARR within about 6 months. Over 1M sites in 5 months. Bolt V2 and Bolt Cloud (DB, auth, storage, hosting) shipped Oct 2025 (sacra.com/c/bolt-new; morphllm.com).
2. **Hiring:** No job posts found within the search budget.
3. **Internal platforms:** WebContainers run Node in the browser and remove the cloud VM bill. Gross margin went from about 40% (May 2025) to close to 70%, per the company (sacra).
4. **Human ops:** Billing disputes over token burn. "Thin billing-dispute support" is one of the two dominant complaints (sacra/codegen summaries).
5. **Architecture beyond normal SaaS:** The client device is the compute, which avoids per-session VMs. With Bolt Cloud it now also has to run hosting and backends.
6. **Scales linearly with:** Tokens burned per fix loop (the agent rewrites whole files to fix its own bugs), and support disputes.
7. **Complaints:** Token burn, and paying for the model's own mistakes (superdesign.dev review; sacra).
8. **Built internally:** WebContainers, a browser OS runtime few companies could build.
9. **Pain tags:** inference-cost-routing, usage-metering-billing, customer-support-scale, sandbox-infra
- **Pain estimates:** usage-metering-billing / billing disputes. FREQUENCY: EST a large share of tickets are token refunds. SCALING LAW: linear in failed agent loops.

## 7. Factory
1. **Changed:** $50M Series B in Sep 2025 and $150M Series C (Khosla, Apr 2026, $1.5B). Users at Nvidia, Adobe, EY, Palo Alto Networks, MongoDB and others (enterprisedna; techinterview.org; secondary).
2. **Hiring:** "Software Engineer, Deployed", Mid-Market Solutions Engineer Director, Enterprise AE. About 45 open roles (fastaijobs.com/companies/factory-ai).
3. **Internal platforms:** Specialised droids for code, knowledge and reliability/incident response. Enterprise integrations with source control, ticketing and observability (latent.space/p/factory; zenml summary).
4. **Human ops:** Deployed engineers onboard each enterprise: connect integrations and tune droids to the customer's workflow.
5. **Architecture beyond normal SaaS:** Agents that own end-to-end SDLC tasks inside customer toolchains, with many integrations.
6. **Scales linearly with:** Enterprise customers and the integrations per customer.
7. **Complaints:** None found within the budget.
8. **Built internally:** Integration fabric and an agent harness (inferred).
9. **Pain tags:** forward-deployed-onboarding, integration-maintenance, enterprise-security-compliance, eval-pipelines (inferred, weak)

## 8. Sourcegraph / Amp
1. **Changed:** Amp spun out as Amp Inc. in Dec 2025. Cody became enterprise-only around Jun 2026 (en.wikipedia.org/wiki/Sourcegraph; usagepricing.com).
2. **Hiring:** Not searched.
3. **Internal platforms:** "Amp Free", funded by ads, launched Oct 15 2025, reached a $10M+ run rate, and dropped ads in Mar 2026 while keeping a $10/day allowance (rywalker.com/research/amp-sourcegraph; secondary). One snippet said abuse and ops costs were the reason; that is unverified.
4. **Human ops:** Unknown.
5. **Architecture beyond normal SaaS:** A free agent tier subsidised by inference, which needs per-user daily caps and abuse controls.
6. **Scales linearly with:** Free-tier tokens.
7. **Complaints:** None found within the budget.
8. **Built internally:** Code search and code graph (legacy Sourcegraph).
9. **Pain tags:** inference-cost-routing, free-tier-compute-abuse (weak), usage-metering-billing, code-indexing-retrieval

## 9. Augment Code
1. **Changed:** Moved from per-message to credit pricing on Oct 20 2025. The stated reason: one user on the $250 Max plan sent 335 requests an hour, every hour, for 30 days, costing Augment close to $15k a month (augmentcode.com/blog/augment-codes-pricing-is-changing, Oct 6 2025). Completions were later sunset (fast.io review).
2. **Hiring:** Not searched.
3. **Internal platforms:** The "Context Engine" (retrieval over large codebases) is listed as a cost line inside credits (Augment blog).
4. **Human ops:** Explaining price changes and forecasting costs for customers (blog says it aims to help users "forecast costs").
5. **Architecture beyond normal SaaS:** Unit economics per request vary more than 50x between users, so metering has to track true cost.
6. **Scales linearly with:** Requests and context size. One automated user can cost 60x their subscription price.
7. **Complaints:** Cost increases for heavy users (kilo.ai test: $0.26–0.67 per task).
8. **Built internally:** Context engine and credit metering.
9. **Pain tags:** inference-cost-routing, usage-metering-billing, free-tier-compute-abuse (power-user and automation abuse), code-indexing-retrieval
- **Pain estimates:** usage-metering-billing. INFRA COST: in the example, a 60x cost-to-price gap per abusive account. SCALING LAW: heavy-tailed in automation. CURRENT SOLUTION: re-pricing (credits).

## 10. Supabase (backend for vibe-coded apps)
1. **Changed:** More than 1M Postgres databases a week, over 140k a day (Copplestone, via arkolith.com). 15.1M databases created in 2025, more than all prior years combined (supabase.com/wrapped). More than 60% of new DBs are launched by AI tools. Valuation reported at $10.5B (implicator.ai).
2. **Hiring:** Not searched.
3. **Internal platforms:** A dedicated Postgres instance per project. Auto-pausing of free projects after 7 days idle. Throttling and pausing of noisy neighbours (jetadmin.io; adhdecode.com).
4. **Human ops:** Incident response: 77 outages and about 74h of downtime from Dec 24 2025 to Oct 2026, per a third-party tracker. Includes us-east-2 project access (Aug 14 2026), a hardware failure, and project create/unpause failures in eu-west-1 (pingoru.io; isdown.app).
5. **Architecture beyond normal SaaS:** Provisioning DBs at agent speed. Most databases are short-lived or abandoned, so pausing and resuming millions of them is a core function. RLS security now depends on what an AI wrote (see Lovable CVE).
6. **Scales linearly with:** Agent-created projects (most never paid for), RLS misconfigurations, and the incident surface (control plane load).
7. **Complaints:** CVE-2025-48757 blame lands partly on Supabase defaults. Free-tier pause friction.
8. **Built internally:** Pause and unpause automation for fleet-scale Postgres.
9. **Pain tags:** free-tier-compute-abuse, security-review-of-generated-code, db-provisioning-fleet-ops, control-plane-reliability
- **Pain estimates:** db-provisioning-fleet-ops. INFRA COST: EST if 140k DBs a day each cost even $0.01/day while active, that is about $1.4k/day of new liability added every day. Pausing is what keeps it bounded. SCALING LAW: linear in agent creations, not in revenue. That is the economic mismatch.

---

## Cross-company pain table

| pain tag | companies showing it | which built internally | evidence strength |
|---|---|---|---|
| abuse-fraud (fraud, payments, credits) | Replit, Lovable, Vercel, (Amp, Augment: weak) | Replit (new team), Lovable (fraud platform), Vercel (T&S org) | **Strong**: repeated job posts at 3 companies in 2026 |
| free-tier-compute-abuse | Replit, Lovable, Vercel, Supabase, Augment, Amp | Supabase (auto-pause/throttle), Lovable, Augment (credit re-pricing) | Strong (Augment $15k example; job posts); Amp weak |
| phishing-hosting-takedown | Vercel, Lovable, (Replit implied) | Vercel (abuse ops + Okta reporting), Lovable (T&S) | Strong (Okta/Axios Jul 2025; Lovable CVE reports) |
| sandbox-infra | Cognition, Replit, Vercel, Bolt, Cursor (cloud agents on Vercel Sandbox) | Cognition (DevBox), Replit (snapshot engine), Vercel (Firecracker), Bolt (WebContainers) | **Strong**: 4 built internally; Cognition now outsources Outposts execution |
| agent-blast-radius-rollback | Replit, (Cognition, Supabase dev/prod) | Replit (CoW snapshots, forkable DB) | Strong for Replit; medium overall |
| inference-cost-routing | Cursor, Bolt, Augment, Amp, Cognition (EST) | Cursor (own GPU fleet + model) | Strong (Cursor 2k H100s; Augment blog) |
| usage-metering-billing | Cursor, Augment, Bolt, Replit, Amp | Augment (credits), Cursor (usage pricing) | **Strong**: 3 public pricing crises (Cursor Jun 2025, Augment Oct 2025, Bolt complaints) |
| customer-support-scale | Cursor, Bolt, Lovable | Cursor (AI support agent "Sam", then TSE team) | Medium-strong (Cursor incident + Paraform case study) |
| security-review-of-generated-code | Lovable, Supabase, (Replit, Vercel) | Lovable (Security Checker 2.0, pre-publish scan) | Strong (CVE-2025-48757, CVSS 9.3, 170+ apps) |
| forward-deployed-onboarding | Cognition, Factory, (Cursor TAMs) | Human only | Strong (many repeated DE posts) |
| enterprise-deploy-onprem | Cognition, (Cursor, Factory) | Cognition (Outposts / VPC) | Medium |
| enterprise-security-compliance | Cursor, Factory | Cursor (GRC eng hire) | Medium-weak |
| code-indexing-retrieval | Cursor, Augment, Sourcegraph | All three | Medium (core product, not hidden pain) |
| integration-maintenance | Factory, Cognition | Unclear | Weak (inferred) |
| db-provisioning-fleet-ops / control-plane-reliability | Supabase, (Bolt Cloud, Replit DBs, Lovable Cloud) | Supabase | Medium (1M DBs a week; 77 outages, third-party tracker) |
| db-scaling-sharding | Cursor | Cursor | Medium (single source) |
| eval-pipelines | Factory (inferred) | Not found | Weak; not evidenced within the budget |

**Clusters that pass the round's cluster filter so far:** abuse-fraud + free-tier-compute-abuse + phishing-hosting-takedown (5–6 companies, 3+ built in-house, grows with every free signup or deploy). sandbox-infra (5 companies, 4 built in-house, already partly commoditised by Vercel/Daytona/Modal). usage-metering-billing + inference-cost-routing (5 companies; caused by heavy-tailed agent usage).
