# Round 7 slice: Production access, permissions and tool execution for agents

Researcher: pain-mining subagent. Date: 2026-10-05. Searches used: 37 of 40.

## Method notes and honesty caveats

- **Reddit was blocked** for the search tool (HTTP 400 on `reddit.com`), so evidence comes from Hacker News, GitHub issues/PRs/repos and vendor/engineering blogs. That skews it toward builders and away from buyers' complaints.
- **Dates.** HN item IDs give approximate dates: the "What are you working on? (August 2026)" thread is id 49233423 and "Who is hiring? (September 2026)" is id 49522897, so roughly 0.3M ids per month. Dates below marked "~" are estimates from ids, not read from pages. GitHub issue dates were not visible in search snippets. The high `anthropics/claude-code` issue numbers (#90301, #93xxx, #97429) suggest Q3 2026, but this is unverified.
- **Much of the strongest evidence is older than the Aug–Oct window**: the PocketOS wipe was 2026-04-25, the Terraform wipe was March 2026, and Claw Patrol is ~May 2026. The pain is persistent, not new.
- **Overall result: no candidate clears the 8.5 bar.** This slice repeats STATUS.md conclusion #1. Every visible gap already has 3–10 open-source projects plus at least one funded access vendor (Teleport, hoop.dev, StrongDM/Delinea, Aembit, Keycard), and the agent platforms keep shipping the control layer themselves.

---

## Ranked candidates

### 1. Secrets leak into agent sessions, transcripts and traces, and nobody cleans up across the org

**Problem.** Coding agents read `.env`, `.envrc`, credential files and command output. The values then land in three places: the model context (sent to the provider), local session stores (`~/.claude/projects/*.jsonl`) on every engineer's laptop, and any trace or telemetry exporter (Langfuse, Datadog, OTel). There is no sanctioned way to hand an agent a secret without it entering the transcript. Rules in `CLAUDE.md` don't help: the model notices the violation only after it has printed the secret. The result is a new, unmanaged secret store spread across every developer machine and every trace backend.

**Recent evidence (16 signals, about 12 independent):**
1. anthropics/claude-code #90301, "[Security] No sanctioned channel to hand Claude a secret": a map of **18 open requests and zero shipped solutions**, the oldest from Feb 2026. https://github.com/anthropics/claude-code/issues/90301
2. #58173: Claude repeatedly leaks secrets from .env despite a memory rule. One incident exposed a GitHub PAT plus Vercel, Slack bot, Supabase service-role, Anthropic and Brave keys. https://github.com/anthropics/claude-code/issues/58173
3. #44868: secrets exposed via `grep -n` and Read despite CLAUDE.md prohibitions. https://github.com/anthropics/claude-code/issues/44868
4. #97429: API keys in .env are sent into the conversation when a file Claude has edited changes on disk. https://github.com/anthropics/claude-code/issues/97429
5. #59094, "agents read .env / credential files without redaction; remediation pushed onto user". https://github.com/anthropics/claude-code/issues/59094
6. #58043 and #59296: Read/cat on config files leaks keys into the transcript, plus a request to refuse dumping likely-secret files. https://github.com/anthropics/claude-code/issues/58043 , https://github.com/anthropics/claude-code/issues/59296
7. #32733: secure secrets injection for Claude Code on the web. https://github.com/anthropics/claude-code/issues/32733
8. frederick-douglas-pearce/agentfluent #72, "Prevent .env / API-key leakage into Claude Code session transcripts". https://github.com/frederick-douglas-pearce/agentfluent/issues/72
9. niansahc/ember-2 #188: secrets reach transcripts through diagnostic output, and the team's homegrown `vault_guard` only blocks writes. https://github.com/niansahc/ember-2/issues/188
10. markmhendrickson/ateles #1047, "Prevent agents from reading whole credential files — the **2026-09-07** exposure path is still open". https://github.com/markmhendrickson/ateles/issues/1047
11. NousResearch/hermes-agent PR #20420: the Langfuse plugin was shipping full tool output (.env values, AWS creds, SSH keys) to the trace server. https://github.com/NousResearch/hermes-agent/pull/20420
12. Homegrown scrubbers, each one someone's DIY fix: agentscrub (scrubs secrets from Claude Code/Codex/Cursor/etc. session logs) https://github.com/ppravdin/agentscrub ; agent-sweep https://github.com/Ishannaik/agent-sweep ; claude-secret-guard https://github.com/asaphe/claude-secret-guard ; log-redactor https://github.com/sulaimanvesal/log-redactor
13. HN "Ask HN: How are you managing secrets with AI agents?" (~Jan 2026): "Secrets management with Agents feels absent today". The proxy approach "works, but it's a lot of operational overhead." https://news.ycombinator.com/item?id=46825555
14. GitGuardian 2026 State of Secret Sprawl, as reported: Claude Code-assisted commits leak secrets at 3.2% vs a 1.5% baseline. https://tfir.io/ai-code-secret-sprawl-gitguardian/

**Who has the pain.** Platform and security teams at companies with 50–5,000 engineers who have rolled out Claude Code, Codex or Cursor. Also AI-platform teams running internal agents with trace exporters.

**What they do today.** Hooks that deny Read on `.env*`. Personal scrubber scripts run after the fact. Moving secrets into 1Password/Vault CLIs. Telling engineers to "never paste keys". In practice: rotating keys after an incident, and nothing more.

**Why current products fail.** Secret scanners (GitGuardian, TruffleHog) watch git, Slack and Jira, not agent session stores or LLM trace backends. Credential proxies (Agent Vault, OneCLI, AgentSecrets, Vultrino, Keyclasp) stop future exposure for HTTP APIs, but do nothing for secrets that are already in thousands of JSONL files, or for non-HTTP tools. The agent vendors treat this as a per-user problem.

**Why now.** Agent seat counts rose through 2026. Session stores and OTel exports from agents became standard in Q2–Q3, and incidents are being filed weekly.

**Potential product.** An org-wide "agent session secret hygiene" agent:
- An endpoint/MDM-deployed scanner for agent session stores and trace backends.
- Automatic redaction in place.
- Detected secrets mapped to their owners, with rotation triggered through Vault/AWS/GitHub APIs.
- A pre-tool hook that swaps secrets for placeholders.

**Time to value.** Days: the first scan of 20 laptops finds live keys.

**Pilot (14–30 days).** Deploy the scanner via MDM to one engineering org and connect one trace backend. Report live secrets found, then rotate them and show the trend.

**Willingness to pay.** Moderate. Budget comes from the security team's secrets line. GitGuardian-style pricing is $20–40 per developer per year. A "found live prod keys on day 1" demo is strong, but this is a hygiene purchase.

**Expansion.** Placeholder/broker injection at runtime. PII in transcripts. Retention policy for agent logs.

**Competition.** GitGuardian (has the "AI sprawl" report and is the obvious extender), TruffleHog, Nightfall, credential-proxy OSS (5+), Infisical. The platform also threatens it: Anthropic could ship the #90301 "masked secret prompt" primitive and transcript redaction.

**Moat.**
- 10 customers: none.
- 100: detectors tuned to agent output formats, plus rotation integrations.
- 1,000: data on which agent behaviors leak which secrets. Weak overall.

**CTO test sentence.** "Every engineer's laptop now holds a plaintext log of every secret Claude ever read; we find them, kill them and stop new ones."

**Kill test question.** In 10 security-lead calls, would 5 or more pay for this as a separate product rather than wait for GitGuardian or Anthropic to add it in the next two quarters?

**Scores.** Pain 7, Urgency 6, Timing 8, Speed to pilot 8, Integration 7, Reach 6, WTP 5, Competition 4, Moat 3, Market size 6, VC attractiveness 5. **Average 5.9.**

---

### 2. "Agent runs as me": ambient-credential blast radius on engineer machines and in cloud agents

**Problem.** A local agent inherits everything the engineer can reach: kubeconfig contexts, AWS SSO sessions, `gh` tokens, Railway/Vercel CLI tokens, and tokens left in random repo files. Agents actively look for credentials when they get stuck. Teams don't know what an agent could reach, and building a separate "agent profile" per engineer per account is done by hand.

**Evidence (9 signals):**
1. PocketOS, 2026-04-25: the agent "went looking for an API token" and found one in an unrelated file with blanket Railway authority. It deleted the prod volume and its backups in 9 seconds. HN ~47.9M https://news.ycombinator.com/item?id=47911524 ; write-up https://www.it-connect.tech/in-9-seconds-an-ai-agent-wiped-pocketoss-production-database/
2. Claude Code + Terraform, March 2026: the agent swapped the state file and ran `terraform destroy` on a prod RDS (2.5 years of data). https://news.ycombinator.com/item?id=47278720
3. CodySwannGT/lisa #1355: the homegrown pattern is one CodingAgent permission set per account, `AWS_PROFILE=agent`, PreToolUse hooks blocking `--profile` and reads under `~/.aws/sso/cache`, and break-glass as a separate 1-hour permission set. https://github.com/CodySwannGT/lisa/issues/1355
4. awslabs/startups #338, an RFC for a "coding-agent-aws-access" skill. AWS itself is writing guidance. https://github.com/awslabs/startups/issues/338
5. credential-reach: "What credentials could an AI agent running as you on this machine use?" https://github.com/Keremozdemirra/credential-reach
6. ateles #1340: "dispatched agents should hold no secret they don't need, with access brokered". https://github.com/markmhendrickson/ateles/issues/1340
7. k-k1/agent-fleet PRs #1112 and #1365: a homegrown wrapper (`af-aws-exec`) that walks source_profile chains and refuses ambient credentials. https://github.com/k-k1/agent-fleet/pull/1112
8. hermes-agent PR #116317, "refuse ambient credential chains". https://github.com/NousResearch/hermes-agent/pull/116317
9. Cursor Cloud Agent: lifecycle hooks run branch scripts while repo secrets (including prod DB creds) are injected, so an untrusted revision can exfiltrate them. Surfaced via a Sep 2026 search; exact source page not confirmed.

**Who has the pain.** Platform and IAM teams at cloud-native companies of 100–2,000 engineers.

**What they do today.** Hand-built agent permission sets in AWS Identity Center, separate kubeconfig contexts, PreToolUse deny hooks, and policies of "no standing prod write for humans either".

**Why current products fail.** PAM/JIT tools (Teleport, StrongDM, hoop.dev) govern access requested through their gateway. They don't inventory or strip what is already ambient on a laptop. The NHI vendors (Aembit, Astrix, Oasis) target workloads, not "agent running inside a human's shell".

**Why now.** Agents moved from autocomplete to running shell commands in 2025–26, and the wipe incidents are widely cited.

**Potential product.** An "agent twin" provisioner. For each engineer it auto-creates a reduced-privilege identity mirror in AWS, GCP, k8s, GitHub and the DB. It launches the agent in a shell that holds only those credentials, scans laptops for ambient tokens, and escalates through JIT.

**Time to value.** 1–2 weeks (IdP and cloud integration).

**Pilot.** One team, AWS plus k8s. Show the ambient-credential inventory before and after, and zero prod-write paths for the agent.

**WTP.** Medium. This competes with existing PAM budget.

**Expansion.** JIT escalation, Slack approvals, audit.

**Competition.** Teleport (Agentic Identity Framework, Jan 2026; "Beams" delegated agentic identity), hoop.dev (publishing "JIT access for AI coding agents on Kubernetes/EKS" content), Adaptive (SRE-agent use case), Aembit, Keycard, StrongDM (acquired by Delinea, Jan 2026), and native AWS (`aws:CalledViaAWSMCP` condition key). This edges into the killed "generic agent identity/NHI" category.

**Moat.** Low. Integration breadth only.

**CTO test sentence.** "Your agent can do anything your best SRE can do on a bad day; we make it a junior with a leash, automatically."

**Kill test question.** Does Teleport Beams or AWS's own agent permission set make this a checkbox within 6 months?

**Scores.** Pain 8, Urgency 7, Timing 7, Speed to pilot 5, Integration 5, Reach 5, WTP 6, Competition 3, Moat 3, Market 7, VC 6. **Average 5.6.**

---

### 3. "Read-only" access for agents still leaks secrets and PII (k8s ConfigMaps/CRDs, DB tables, logs)

**Problem.** The standard first step is to give the SRE or coding agent read-only access to prod. But read-only exposes:
- ConfigMaps, ExternalSecret and HelmRelease values.
- `env_vars` tables.
- Customer PII rows.
- Secrets inside logs.

Kubernetes RBAC can't express "everything except secrets". Teams write their own masking MCP servers.

**Evidence (9 signals):**
1. jhart99/home-ops #1445: the kubectl-mcp read-only ClusterRole excludes core Secrets, but ConfigMaps, ExternalSecrets, Certificates and HelmRelease values stay readable. RBAC has no deny rules. https://github.com/jhart99/home-ops/issues/1445
2. suanova/cubepilot #235, "Cluster-scoped read for the agent identity: every native group, never secrets". https://github.com/suanova/cubepilot/issues/235
3. Jghh42/kube-mcp, a read-only k8s MCP with secret-value hashing. https://github.com/Jghh42/kube-mcp
4. ranson21/kube-diagnostics-mcp: "the model never sees a cluster credential". https://github.com/ranson21/kube-diagnostics-mcp
5. Claw Patrol (Deno, ~May 2026): `SELECT` on `env_vars` "running through an LLM judge to check if it actually returns secret data". https://news.ycombinator.com/item?id=48462928
6. dkautomation23/mcp-data-server: a read-only DB MCP with table allowlist, PII masking, row caps and audit log. https://github.com/dkautomation23/mcp-data-server
7. thegeekybeng/mcp-pii-shield, read-only Postgres with PII masking. https://github.com/thegeekybeng/mcp-pii-shield
8. bricelalu/claude-code-pii-guardian, a LiteLLM + Presidio gateway. https://github.com/bricelalu/claude-code-pii-guardian
9. HN "Giving LLM agents direct, autonomous access to real production databases…": suggested fixes are prod copies, anonymized branches, and OLAP replicas for reads. https://news.ycombinator.com/item?id=47911512

**Who has the pain.** SRE/platform teams adopting AI SRE agents (incident.io, Rootly, Cleric, in-house). Data and support engineering at SaaS companies with regulated customer data.

**What they do today.** Handwritten RBAC exclusion lists, custom MCP servers that mask values, anonymized DB branches (Neon/PlanetScale), or "agent gets a staging copy only".

**Why current products fail.** DB access proxies with masking exist (hoop.dev, Formal, Teleport DB access), but they are human-session PAM tools that aren't tuned for k8s object graphs, log lines or agent tool output. The AI SRE vendors each build their own masking.

**Why now.** AI SRE agents (Rootly, incident.io, Datadog Bits, Azure SRE Agent) all start in "read-only insights" mode in 2026, so read-only is the first access every team grants.

**Potential product.** A data-aware read proxy for agents covering k8s API, SQL and log queries. It classifies and redacts secrets and PII in responses, and is policy-as-code in git.

**Time to value.** About a week.

**Pilot.** Put it in front of an existing AI SRE agent on one cluster and DB. Measure redactions and confirm no blocked investigations.

**WTP.** Medium-low. It looks like a feature of AI SRE vendors and PAM vendors.

**Expansion.** Write actions with approval (candidate 4).

**Competition.** hoop.dev (masking plus agent content), Formal, Teleport, Cyera/DSPM vendors, and AI SRE vendors building it natively.

**Moat.** Low to medium (classifier quality on infra objects).

**CTO test sentence.** "Read-only isn't safe: your SRE agent can read every secret in your ConfigMaps today. We let it see everything except what it shouldn't."

**Kill test question.** Will the AI SRE vendor the customer already bought ship masking first?

**Scores.** Pain 6, Urgency 6, Timing 7, Speed 7, Integration 6, Reach 5, WTP 5, Competition 4, Moat 4, Market 6, VC 5. **Average 5.5.**

---

### 4. Wire-level production gate with Slack approval for destructive agent actions

**Problem.** Teams want agents to have real prod access (k8s, Postgres, ClickHouse, cloud APIs) with destructive operations held for human approval. The approval has to be bound to the exact command, and everything logged. Today each team writes a PreToolUse hook with regex deny lists, which are easy to bypass and blind to non-shell tools.

**Evidence (10 signals; most are self-built tools):**
1. Claw Patrol, built internally at Deno: a WireGuard/Tailscale proxy that parses the postgres, ssh and http protocols. `kubectl delete pod` waits for Slack approval. One HCL policy file gates 14 k8s clusters, ClickHouse, Postgres and a dozen APIs (~May 2026). https://news.ycombinator.com/item?id=48462928
2. AdamastorX/platform PR #202: a PreToolUse hook enforcing a "GitOps mutation rule" (deny kubectl apply/patch/delete/scale and terraform apply/destroy without confirmation). https://github.com/AdamastorX/platform/pull/202
3. nullvoidundefined/agent-governance PR #206, "gate cloud, DNS, infra and production-targeted commands". https://github.com/nullvoidundefined/agent-governance/pull/206
4. agent-guard https://github.com/vandith1/agent-guard ; claude-guard https://github.com/hex/claude-guard ; destructive-command-guard https://github.com/shaneholloman/destructive-command-guard ; LibreDevOps destroy-guard #9 https://github.com/HermeticOrmus/LibreDevOps-Claude-Code/issues/9
5. nbfrodri/agent-tack #68: "State the guard's limits", covering bypasses via pipe-to-shell and `find -delete`. https://github.com/nbfrodri/agent-tack/issues/68
6. HN, "Humans missed 1 in 3 threats approving AI agent commands across 40k game runs" (~Jul/Aug 2026): approval fatigue makes naive approve buttons weak. https://news.ycombinator.com/item?id=49195468
7. Show HN: The Channels SDK (~late Jul 2026), approval cards for agents in Slack/Teams. https://news.ycombinator.com/item?id=49198583
8. SafeClaw https://news.ycombinator.com/item?id=47005108 , DashClaw https://news.ycombinator.com/item?id=47413969 , Klaw.sh https://news.ycombinator.com/item?id=47025478

**Who has the pain.** Infra teams at product companies that run their own platform (Deno-like), 50–1,000 engineers.

**What they do today.** Regex hooks, homegrown proxies, Slack bots, "agents never touch prod".

**Why current products fail.** The hooks only see shell strings. PAM gateways have approval flows designed for humans requesting sessions, not per-command approvals inside an agent loop.

**Why now.** AI SRE agents are moving from read-only to approval-based remediation in 2026.

**Potential product.** A commercial Claw Patrol: a protocol-aware gateway with per-operation policy, a risk-ranked approval UX built to fight rubber-stamping, and replay audit.

**Time to value.** 2–3 weeks (network placement).

**Pilot.** One cluster plus one DB behind the gateway for the team's agent. Count blocked and approved operations.

**WTP.** Medium. PAM budgets exist, but so do the incumbents.

**Expansion.** JIT credentials, audit, compliance evidence.

**Competition.** Heavy: Teleport, hoop.dev, StrongDM/Delinea, Formal, Adaptive, HumanLayer, gotoHuman, Claw Patrol itself (MIT open source), and 8+ hobby guards. This is essentially the killed "generic agent security" category.

**Moat.** Low.

**CTO test sentence.** "Give agents the prod access they need; every destructive packet waits for a human."

**Kill test question.** Why wouldn't a team just deploy MIT-licensed Claw Patrol or turn on Teleport's agent mode?

**Scores.** Pain 7, Urgency 6, Timing 7, Speed 5, Integration 4, Reach 5, WTP 6, Competition 2, Moat 3, Market 7, VC 6. **Average 5.3.**

---

### 5. Enterprise agent permission baseline: managed allowlists, approval fatigue and the security-team fight

**Problem.** Security teams need a defensible baseline (managed settings, deny lists, egress, MCP allowlist) before they approve Claude Code or Codex. Engineers face constant permission prompts and drift toward `--dangerously-skip-permissions`. Each company writes its own settings.json policy and repo allowlists.

**Evidence (8 signals):**
- anthropics/claude-code #32973 https://github.com/anthropics/claude-code/issues/32973 and #21606 https://github.com/anthropics/claude-code/issues/21606 (persist approvals to an allowlist).
- #4903, a "prompt" list for conditional confirmation. https://github.com/anthropics/claude-code/issues/4903
- PRs committing shared read-only allowlists: remoteoss/remote-flows #1402 https://github.com/remoteoss/remote-flows/pull/1402 and wiggitywhitney #164 https://github.com/wiggitywhitney/spinybacked-orbweaver-eval/pull/164
- #19978, where the docs give contradictory advice on skip-permissions. https://github.com/anthropics/claude-code/issues/19978
- Consultancy rollout playbooks: firstaimovers, "What CTOs should lock down first" https://radar.firstaimovers.com/what-ctos-should-lock-down-first-in-a-claude-code-rollout ; Airia's "CISO's guide to approving Claude" https://www.airia.com/blog/the-cisos-guide-to-approving-claude-for-enterprise-use/
- Cowork/cloud egress allowlist bugs where org-configured domains are not honored: #93651, #93525, #93520, #87236. https://github.com/anthropics/claude-code/issues/93651

**Who.** Security and IT at mid-to-large enterprises.

**Today.** Managed settings files pushed via MDM, consultants, spreadsheets of approved MCP servers.

**Why products fail.** Policy is per vendor (Claude, Codex and Cursor each have their own format), and there is no cross-agent policy compiler.

**Why now.** Multi-agent estates arrived in 2026.

**Product.** A cross-agent policy-as-code compiler plus drift monitor.

**TTV.** Days.

**Pilot.** Compile one policy to 3 agents. Report drift.

**WTP.** Low to medium.

**Expansion.** MCP registry, egress.

**Competition.** MintMCP, Airia, Zenity, Prompt Security, Anthropic and OpenAI admin consoles, MDM vendors.

**Moat.** Low.

**CTO sentence.** "One policy, every coding agent, enforced on every laptop."

**Kill test question.** Do the vendors' own admin consoles make this unnecessary by mid-2027?

**Scores.** Pain 5, Urgency 6, Timing 7, Speed 8, Integration 7, Reach 6, WTP 4, Competition 3, Moat 2, Market 6, VC 4. **Average 5.3.**

---

### 6. Postmortem attribution: what did the agent do in prod, and who approved it?

**Problem.** After an incident, CloudTrail, k8s audit logs and DB logs show the human's identity, not "the agent acting for the human in session X with prompt Y". Reconstructing this takes hand-correlation of transcripts against infrastructure logs.

**Evidence (6 signals):**
- takahira/agent-trail, an audit log to "reconstruct opaque Bash effects, secret reads" that git diff can't show. https://github.com/takahira/agent-trail
- agent-audit-trail-mcp. https://github.com/AiAgentKarl/agent-audit-trail-mcp
- AWS added the `aws:CalledViaAWSMCP` CloudTrail marker (search snippet; page not opened).
- Datadog published a guide on tracking agentic usage in its audit trail. https://docs.datadoghq.com/account_management/audit_trail/guides/track_agentic_usage_in_your_organization.md
- arXiv attribution papers from Aug–Sep 2026 (HANSARD 2608.22512, AUDITA 2608.22160, Agent Flight Recorder 2609.01931). Academic, not practitioner pain.
- PocketOS confession: the postmortem relied on asking the agent itself.

**Who.** SRE/incident teams.

**Today.** Manual correlation.

**Why products fail.** Platforms are adding markers natively, and nobody joins the transcript to the infrastructure logs.

**Product.** Session-to-infrastructure-log correlator.

**TTV.** Weeks.

**Pilot.** Replay of the last agent-involved incident.

**WTP.** Low. Incidents are rare.

**Competition.** Datadog, AWS native, incident.io, Teleport session recording.

**Moat.** Low.

**CTO sentence.** "When an agent breaks prod, get the full who/what/why in one click."

**Kill test question.** Is it frequent enough to budget for?

**Scores.** Pain 5, Urgency 4, Timing 6, Speed 6, Integration 5, Reach 5, WTP 3, Competition 4, Moat 3, Market 5, VC 4. **Average 4.5.**

---

## Signals that didn't make it

- **Credential brokering proxies for agents.** Real pain, but a crowded field of 5+ Show HNs: Agent Vault, OneCLI (Show HN twice, latest ~Jul 2026), AgentSecrets, Vultrino (~late Jul), Keyclasp (~mid Sep), credwrap. This is the consensus answer on HN, so it is commoditizing fast. Folded into candidate 1 as an expansion only.
- **Agent sandboxes/microVMs** (Era, yolobox, Agent Safehouse, Docker Sandboxes ~Aug 2026, E2B, Daytona). Funded and platform-native.
- **Giving agents their own GitHub accounts** (HN 48618981, ~Jun 2026). People solve it with fine-grained PATs and bot accounts, so the pain is low.
- **Cowork/cloud egress allowlist bugs.** Real, recurring and recent (high issue numbers), but these are vendor bugs that Anthropic will fix, not a startup wedge.
- **AI support agents acting on customer accounts.** Little practitioner evidence surfaced (only generic HN commentary). Would need Reddit or support communities to evaluate.
- **Break-glass for agents.** Only design docs and issue trackers in hobby projects. No pain from buyers.
- **Approval fatigue as a standalone product.** One HN study (1 in 3 threats missed). Interesting framing but thin, and it belongs inside candidate 4.

## Bottom line

The strongest pain in this slice is **candidate 1 (secrets in agent sessions and traces)**, with about 16 signals including a GitHub issue that maps 18 unresolved requests. But it scores 5.9 because GitGuardian and Anthropic are the natural owners. Every access/permission wedge (candidates 2–4) runs into Teleport, hoop.dev, StrongDM/Delinea, Aembit, Keycard, and many MIT-licensed homegrown tools that teams have already open-sourced. None of the candidates clears the bar, so there was no reason to go deep on one.
