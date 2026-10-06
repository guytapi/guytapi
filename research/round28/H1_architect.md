# H1 (architect lens): where agent-service architecture breaks at 100x, and the missing primitive

**Role:** technical infrastructure architect. **Date:** 2026-10-06.
**Searches:** 21 of 30. The shared per-turn search budget ran out after 21, so the last competitor sweeps (reconciliation startups, tenant-policy-layer startups) **were not run**. This is the biggest evidence gap; see §6. WebFetch was blocked, so everything comes from search snippets.
**Tags:** [V] = backed by a search result (URL given). [B] = blog, vendor or secondary source. [U] = unverified, or my own inference.

---

## 0. Bottom line

- **Thesis: "Hammer for agent vendors".** A multi-tenant *behavior contract* layer for AI app companies.
  - Every human correction, exception resolution and customer policy is compiled into a **scoped, executable contract**: tenant-only, segment, or fleet-wide.
  - Contracts are enforced at runtime as pre-commit checks and as post-action verification against the system of record.
  - Every base change (model swap, prompt edit, tool change) is **replayed against every tenant's contracts** before it ships. That turns a 500-way fork into a single release.
- **Why this layer:** supervision cost grows linearly with customers for two architectural reasons:
  1. Per-customer forks cannot take base improvements.
  2. Corrections do not compound. A fix for customer A stays in A's prompt, or in a human's head.
- **Verdict:** **not A (avg 6.2). Classified as a weak B, roughly 10% odds.**
  - The pain is architecturally real, and the analogy holds (Salesforce Hammer).
  - But the top-tier buyers (Sierra, Decagon, Intercom) have already built the single-tenant version in-house.
  - Eval vendors (Braintrust, Coval, Cekura) and LaunchDarkly AgentControl are one feature away.
  - The moat depends on a data model, not on network effects.

---

## 1. Pushing H1 to 2028-2029: what breaks at 100x customers

Assume a vertical agent company in 2028 with 2,000 customers instead of 20, each with its own SOPs, thresholds, tone, integrations and escalation contacts.

| Subsystem | Works at 20 customers because... | Breaks at 2,000 because... | 2nd/3rd-order consequence |
|---|---|---|---|
| **Per-customer configuration** | An FDE hand-forks the prompt or AOP and remembers why | 2,000 forks with undocumented intent; owners rotate | **Base improvements stop shipping.** Every model migration becomes 2,000 migrations. The vendor gets pinned to old models, so inference cost and quality fall behind competitors |
| **Exception handling** | Slack channel per customer plus an ops person | Tens of thousands of exceptions a day, each needing the *tenant's* policy, contact and SLA | Ops headcount tracks customer count. Exceptions become the real COGS line under outcome pricing (escalations are free for Sierra customers) |
| **Learning from corrections** | The human fixes it, then patches the prompt | Patches pile up ("accretion by hotfix"). No one knows if a fix for tenant A should apply to B | Repeat exceptions. The same failure is fixed 300 times in 300 tenants. Corrections become a liability, not an asset |
| **Partial failure and compensation** | Engineer reads the trace and fixes it by hand | Multi-step actions across customer systems fail halfway: refund issued but ticket not closed, load booked but carrier not confirmed | "Unknown outcome" states pile up. The vendor can't prove what was done, so outcome billing is disputed |
| **Verification of completed work** | Spot-check | Can't spot-check 10M actions | Billing (per-resolution), SLAs and customer trust all hinge on an unverified "done" |
| **Release safety** | A/B test on one customer | A change that helps 1,900 tenants silently breaks 100 with special policies | Vendor slows releases to monthly. AI-native speed advantage gone |
| **Escalation routing** | Hard-coded per customer | Each tenant has different queues, hours, languages, authority limits; these change weekly | Misrouted escalations break SLAs. This is the classic "config drift" incident class |

**The common root cause (architect's read):** today's agent stacks have no first-class object for *"what this tenant requires, and why."* Tenant requirements are smeared across:

- prompt text
- AOPs
- tool code
- eval datasets
- humans' heads

Salesforce faced the same problem in 2005-2010 and solved it with two primitives:

1. **Metadata-driven multi-tenancy.** Customizations live as metadata on a shared runtime, not as forks.
2. **Hammer.** Before every release, Salesforce runs more than 210 million customer-written Apex tests twice, on the current version and on the release candidate. Any difference blocks the release [V][1].

Agent vendors have neither. Their "customer tests" don't exist, because the customer's requirements were never written down in executable form.

---

## 2. Evidence that the behavior is starting now

| Signal | What it shows | Source |
|---|---|---|
| CTO with **47 per-customer system prompts**. A provider cutover deadline turned into 47 migrations. "91% of revenue lived inside the 47 variants," with no formal eval slices and owners who had rotated out. Called "a forked product line problem dressed up as a config knob" | The fork-drift break, described by practitioners (May 2026) | [B] tianpan.co/blog/2026-05-14-per-customer-prompt-forks-47-variant-migration (may be a composite example) |
| Decagon **Agent Versioning** (Nov 5, 2025): isolated workspaces, traffic splits, rollback per version | Top vendors had to build release management for agent behavior in-house | [V] decagon.ai/blog/decagon-agent-versioning |
| Intercom **Evals and Releases** (test changes before launch, validate on live traffic) and **Fin Suggestions** (learn edits from conversation patterns) | Same: built in-house, single-product | [V] createwith.com/tool/intercom/updates/intercom-evals-and-releases-adds-safer-testing-for-fin-updates ; createwith.com/tool/intercom/updates/intercom-launches-fin-suggestions-to-automate-ai-agent-performance-tuning |
| Sierra builds **custom supervisors per customer** in regulated settings; Agent SDK tunes determinism per action | Per-tenant policy enforcement is hand-built by agent engineers | [V] sierra.ai/blog/meet-the-ai-agent-engineer |
| Harvey: "the harness becomes the product." Needs durability, retry semantics, durable task records; "every engineering organization... ends up building similar infrastructure" | Even top vertical vendors rebuild the runtime substrate | [V] harvey.ai/blog/building-spectre-internal-collaborative-cloud-agent-platform |
| HappyRobot: 150+ customers, 8 of top 10 US freight brokers, 20K calls/day; "escalating when human judgment is needed, with full context traveling with every handoff" | Exception handoff is a core product surface at a vertical leader | [V] forkast.news (HappyRobot $1.2B); happyrobot.ai/solutions/operations; freightcaviar.com podcast |
| UiPath **Maestro Case** (Jun 16, 2026): agentic case management for "exception-heavy" processes | The enterprise-internal version of exception handling is being productized by incumbents | [V] businesswire.com/news/home/20260616259667/en/ |
| "Companies with active agentic deployments hiring **3-5 people per production agent system**"; 73% of 4,000 agentic job postings have no prior title | Supervision headcount is real but the figure comes from a secondary source | [B] algeriatech.news (secondary, UNVERIFIED) |
| ICONIQ: AI-company gross margin 52% in 2026, up from 41% in 2024 | Margins are improving. This argues **against** extreme urgency | [B] saastr.com ICONIQ summary |
| Intercom counts an outcome when "the customer doesn't ask for more help," or even on a handoff | "Done" is not verified against the system of record. This is a weak point once buyers audit | [B] lorikeetcx.ai; thesaascfo.com |
| Research: TRACE "compiling user corrections into runtime enforcement" (arXiv 2606.13174); Agent Gym (arXiv 2608.15591); regression-set curation for agent-extensibility platforms with **per-tenant provisioned fixtures** (arXiv 2608.01004) | The academic direction is converging on "corrections become enforceable constraints" | [V] arxiv.org |

---

## 3. Competitors and moving one layer deeper

| Layer | Who owns it | Implication |
|---|---|---|
| Durable execution, retries, compensation (sagas) | Temporal ($12.55B), Restate, Inngest, DBOS, LangGraph (round 7) | Don't build. Sit on top |
| Single-product versioning, A/B tests, rollback | Decagon, Intercom, Sierra in-house; LaunchDarkly AgentControl (AI Configs, guarded rollouts, per-segment targeting) [V] launchdarkly.com/docs/home/agentcontrol | The obvious product exists. Move deeper |
| Evals, simulation, QA monitoring | Braintrust, Coval, Cekura (75+ customers), Hamming; plus Oversai and Isara for policy QA (round 18) | Generic evals are banned; these vendors are one feature from "per-tenant datasets" |
| Learning from corrections | Lleverage.ai ("learn from every correction... pricing rules, exceptions, customer quirks"), DBNT OSS, Fin Suggestions | Single-tenant "memory of fixes" exists. **Cross-tenant scoping does not** [U] |
| Enterprise case management | UiPath Maestro Case, Pega, ServiceNow | Enterprise-internal; not built for an ISV serving 2,000 tenants |
| Multi-tenant agent hosting | AWS Bedrock AgentCore multi-tenant patterns (silo/pool/bridge) [V] | Isolation, not behavior contracts. Could extend |

**The deeper layer nobody visibly owns [U]: the *scope-resolution and fleet-replay* problem.** Two questions in particular:

- "Does this correction apply to tenant A only, to tenants with policy X, or to everyone?"
- "Which tenants does this base change break, and why?"

That is what Salesforce Hammer and metadata multi-tenancy solve. No agent-infra vendor found in 21 searches markets it. **Caveat:** the competitor sweep was cut short.

---

## 4. Finalist format

**One-line problem.** AI app companies can't ship one improvement to all customers. Every customer's agent is a hand-maintained fork, and every human correction stays trapped in one tenant. So supervision headcount and release risk grow linearly with customers.

**Why now.**
1. Vertical agent companies crossed 100-150+ customers in 2025-26 (HappyRobot 150+, Sierra 40% of the Fortune 50).
2. Frontier model deprecation cadence forces fleet-wide migrations several times a year.
3. Outcome pricing makes every exception and unverified "done" a direct COGS and billing line.
4. Top vendors proved the need by building single-tenant versioning in 2025-26: Decagon (Nov 2025), Intercom Releases.
5. The next ~2,000 vertical agent companies can't afford Decagon-sized platform teams.

**Exact buyer.** CTO, or Head of Platform/Applied AI, at the AI app company. Budget comes from the COGS/ops line, co-signed by the VP of Deployments/Operations.

**Exact ICP.**
- Series A-C vertical agent company: voice, support, logistics, healthcare RCM, property management, insurance ops, legal ops.
- 50-1,000 customers, at least 20 distinct per-customer configurations.
- Takes actions in customer systems of record.
- Has at least 5 deployment or AI-ops staff.
- Facing a model migration in the next 2 quarters.
- **Not** Sierra, Decagon or Intercom, which have built it.

**Current workaround.**
- Forked prompts or AOPs per customer, plus a shared eval set (rarely per tenant).
- Slack channel per customer for exceptions.
- FDEs as the "memory" of why each tenant is different.
- Hotfix sentences appended to prompts.
- Model migrations done tenant by tenant with manual spot checks.

**Why incumbents can't easily own it.**
- *Agent vendors* (Sierra, Decagon) build it only for themselves. They won't sell infrastructure to the long tail of vertical competitors.
- *Eval vendors* are organized around datasets and experiments, not around a tenant-scoped policy graph with runtime enforcement and inheritance. Adding scope resolution means changing their data model, though it is possible.
- *LaunchDarkly* targets segments but has no idea what a correction means.
- *Temporal* is below the semantic layer.
- **Honest view:** this is the weakest section. A Braintrust "tenant" dimension plus LaunchDarkly segments gets 50-60% of the way there.

**30-day MVP.**
1. *Ingest:* the design partner's per-tenant prompts/configs, the last 90 days of escalations and human corrections, and traces.
2. *Contract compiler:* an LLM plus a human-confirm step turns each correction into a typed contract. The contract has:
   - scope (tenant / segment / global)
   - trigger condition
   - required behavior (a deterministic check where possible, an LLM-judge otherwise)
   - provenance (who corrected, when, the source ticket)
3. *Fork decomposer:* diffs N tenant prompts against the base and expresses each as base plus overlays (contracts), surfacing contradictory and dead overrides.
4. *Fleet replay ("Hammer"):* for a candidate change (new model or edited base), replay each tenant's contract cases on old and new. Output a per-tenant pass/fail/flip report and a staged rollout plan.
5. *Metric:* repeat-exception rate, and supervised minutes per tenant per week.

**Pilot design (2 design partners, 30 days, data-driven).**
- Run the decomposer and compiler on the partner's real history.
- Pass criteria:
  1. At least 60% of tenant prompt text expressible as overlays.
  2. At least 25% of escalations in the last 30 days are repeats of a correction already made somewhere in the fleet. This is the core "corrections don't compound" proof.
  3. Fleet replay of one pending model migration catches at least 3 tenant-specific regressions the partner's existing evals missed.
  4. The partner commits to gating its next migration on the replay.

**Pricing hypothesis.**
- Platform fee of $30-60K/yr, plus $15-40 per active tenant per month.
- Or a share of measured ops savings.
- A 500-tenant customer pays about $120-300K/yr [U].

**Expansion path.**
1. Fleet replay (release gate).
2. Runtime contract enforcement: pre-commit checks on high-risk actions, plus post-action verification against the system of record. This becomes the source of truth for "verified outcome" billing.
3. Exception object and routing: tenant-scoped escalation policies, SLA clocks, resolution capture that feeds back into contracts.
4. Customer-facing "behavior contract" portal. The vendor's customers can see and approve their agent's rules. This becomes the procurement and audit artifact.
5. Cross-vendor standard for agent behavior SLAs.

**Moat.**
- A *workflow and data-model* moat: once a vendor's tenant requirements live as contracts with provenance, switching costs are high (Salesforce metadata).
- An anonymized cross-vendor contract taxonomy is possible ("refund-threshold contracts fail on model X"), but vendors resist pooling (round 4 lesson). Treat it as weak.
- No network effect is guaranteed.

**Why $10B+ (the B argument).**
- If agentic services become the dominant way B2B software is delivered (thousands of vendors, each with thousands of tenants), every one of them needs (a) a definition of what each tenant's agent must do and (b) proof it did it.
- That is the agent-era equivalent of the metadata and test layer that let Salesforce, Workday and ServiceNow scale multi-tenancy, which those companies built internally at enormous cost.
- A neutral layer that also becomes the system of record for *verified outcomes* sits in the billing path of outcome-priced software, like Stripe sits in the payment path.
- **Plausible-but-unproven chain [U].**

**Direct competitors and adjacent threats.**
- Decagon Agent Versioning, Intercom Evals/Releases/Suggestions, Sierra Insights and supervisors (all in-house).
- LaunchDarkly AgentControl.
- Braintrust, Coval, Cekura, Hamming.
- Lleverage.ai (correction learning, single tenant).
- UiPath Maestro Case.
- Temporal and Restate (substrate).
- AWS AgentCore.
- Frontier-lab platforms (OpenAI Frontier, Anthropic managed agents) adding tenant-scoped configs.
- Unswept: possible seed-stage "agent policy layer" startups.

**One sentence to the CTO.** "Your next model migration is really one migration per customer: give us your prompts and 90 days of escalations, and we'll show you which customer requirements live only in forks, which escalations repeat a fix you already made elsewhere, and exactly which tenants the new model breaks, before you ship."

**Hard kill criteria.**
1. In 2 design partners, fewer than 15% of escalations are fleet-repeats. That would mean corrections are genuinely tenant-unique, so there is nothing to compound.
2. The partners' existing evals already catch at least 80% of the regressions found by fleet replay.
3. Braintrust, LaunchDarkly or Coval ships tenant-scoped datasets with inheritance and replay before the pilot ends.
4. ICP vendors report under 10 distinct tenant configurations (they productized configuration as settings), so there is no fork problem.
5. No partner gates a real migration on the replay within 30 days.

### Scores (honest)

| Category | Score | Why |
|---|---|---|
| Pain | 7 | Architecturally certain at scale; the 47-fork story is vivid, but margins are rising (ICONIQ 52%) |
| Urgency | 6 | Triggered by model migrations and new customer cohorts. Otherwise chronic, not acute |
| ROI clarity | 6 | Ops minutes and avoided regressions are measurable, but attribution is fuzzy |
| Customer accessibility | 7 | CTOs of Series A-C vertical agent companies are reachable (YC, a16z portfolios) |
| Pilot speed | 7 | Offline replay on logs, no production integration needed for the first value |
| Market size | 6 | About 1,000-3,000 vertical agent vendors by 2028 × $150K ≈ $150-450M SAM [U]. $10B needs the verified-outcome expansion |
| Expansion | 7 | Release gate → runtime enforcement → exceptions → verified-outcome billing is a coherent path |
| Venture potential | 7 | The Salesforce/Stripe analogy sells. The risk is that it reads as an "evals feature" |
| Defensibility | 5 | Data-model lock-in only; cross-vendor network is weak |
| Why now | 7 | Model deprecation cadence plus customer counts crossing 100+ plus outcome pricing |
| Competition position | 4 | Leaders built it in-house; eval and flag vendors are one feature away; sweep incomplete |
| **Average** | **6.2** | Fails A (needs ≥8.5, none below 7) |

**Classification: weak B (about 10% odds), not A.**
- What would make it a real B: the pilot finds at least 25% fleet-repeat escalations and replay catches regressions that evals miss.
- That would show the missing object is the *scoped contract graph*, which eval vendors would have to rebuild their data model to offer.
- If the remaining competitor sweep finds a funded "tenant policy layer for agent vendors," **KILL**.

---

## 5. Architecture sketch

```
                 AI APP VENDOR (e.g., 2,000 tenants)
 ┌──────────────────────────────────────────────────────────────────┐
 │  Base agent (prompts, tools, model)   Tenant configs (today: forks)│
 └───────────────┬──────────────────────────────────┬───────────────┘
                 │                                  │ decompose
                 ▼                                  ▼
 ┌──────────────────────────── CONTRACT PLANE ──────────────────────┐
 │  Contract Graph (versioned, scoped)                              │
 │   global ─► segment (e.g. "healthcare", "EU") ─► tenant ─► site  │
 │   contract = {scope, trigger, required behavior, check type      │
 │               (deterministic | SoR query | LLM judge),           │
 │               provenance: correction id, approver, date}         │
 │  Scope resolver: effective policy(tenant, action) + conflicts    │
 └──────┬────────────────────┬─────────────────────────┬────────────┘
        │ release time       │ run time                │ after action
        ▼                    ▼                         ▼
 ┌──────────────┐   ┌─────────────────────┐   ┌─────────────────────────┐
 │ FLEET REPLAY │   │ PRE-COMMIT GUARD    │   │ OUTCOME VERIFIER        │
 │ ("Hammer")   │   │ high-risk tool call │   │ query system of record: │
 │ old vs new × │   │ → check effective   │   │ did refund post? ticket │
 │ every tenant │   │ contracts → allow / │   │ closed? → verified /    │
 │ → per-tenant │   │ block / escalate    │   │ unknown / failed →      │
 │ flips, staged│   └─────────┬───────────┘   │ compensation hook       │
 │ rollout plan │             │               └───────────┬─────────────┘
 └──────────────┘             ▼                           ▼
                    ┌───────────────────────────────────────────────┐
                    │ EXCEPTION OBJECT  (like Stripe's PaymentIntent)│
                    │ states: requires_human → assigned → resolved / │
                    │ compensated; tenant routing policy, SLA clock, │
                    │ evidence bundle                                │
                    └───────────────────┬───────────────────────────┘
                                        │ resolution
                                        ▼
                    ┌───────────────────────────────────────────────┐
                    │ CORRECTION COMPILER                           │
                    │ resolution → proposed contract + suggested    │
                    │ scope ("applies to 37 tenants with policy X") │
                    │ → human confirm → contract graph (loop closes)│
                    │ metric: repeat-exception rate ↓, humans/tenant↓│
                    └───────────────────────────────────────────────┘
 Substrate (don't build): Temporal/Restate for durability; vendor's own
 agent runtime; LaunchDarkly-style traffic splitting optional.
```

**Missing-primitive analogy.**
- Payments needed a *PaymentIntent* (a state machine for a unit of money movement, with disputes and refunds).
- Agent services need two things:
  - a *WorkIntent/Exception* object: a state machine for a unit of delegated work, with verification and compensation;
  - a *Contract Graph*: tenant-scoped requirements that compound across the fleet.
- Without the second, the first just produces more exceptions for humans.

---

## 6. Evidence gaps and red flags

- **The competitor sweep is incomplete.** The search budget ran out before these could be searched:
  - "reconciliation/verification of agent actions" startups;
  - "tenant policy layer for agent vendors" startups.
- The 47-fork story comes from a single practitioner blog and may be a composite.
- "3-5 people per agent system" comes from a secondary source.
- ICONIQ margin improvement suggests vendors are already absorbing supervision cost (H1's premise may be weaker than claimed).
- The round 4 lesson applies: vendors build deployment knowledge tools in-house and won't pool data.
- Round 7 (exactly-once/unknown-outcome) and round 18 (commitment QA) killed adjacent pieces. This thesis survives only as the scoped-contract + fleet-replay combination.

## Sources (all from search results; none invented)
1. Salesforce Hammer: slideshare.net/slideshow/production-readiness-testing-at-salesforce-using-spark-mllib/63068733 ; developer.salesforce.com/podcast/2020/02/episode-17-spring-20-apex-with-chris-peterson
2. tianpan.co/blog/2026-05-14-per-customer-prompt-forks-47-variant-migration
3. decagon.ai/blog/decagon-agent-versioning ; decagon.ai/blog/the-future-of-ai-agents-is-test-driven
4. createwith.com/tool/intercom/updates/intercom-evals-and-releases-adds-safer-testing-for-fin-updates ; createwith.com/tool/intercom/updates/intercom-launches-fin-suggestions-to-automate-ai-agent-performance-tuning
5. sierra.ai/blog/meet-the-ai-agent-engineer ; sacra.com/c/sierra/
6. harvey.ai/blog/building-spectre-internal-collaborative-cloud-agent-platform
7. happyrobot.ai/solutions/operations ; forkast.news/happyrobot-wants-1-2-billion-to-run-your-freight-by-voice/ ; freightcaviar.com/podcast/how-happyrobot-runs-20k-freight-calls-a-day-WOCijKDvQP4
8. businesswire.com/news/home/20260616259667/en/ (UiPath Maestro Case)
9. launchdarkly.com/docs/home/agentcontrol
10. lleverage.ai/product/ai-agents ; pypi.org/project/dbnt/
11. arxiv.org/pdf/2606.13174 ; arxiv.org/pdf/2608.15591 ; arxiv.org/pdf/2608.01004
12. ycombinator.com/companies/cekura-ai
13. saastr.com/iconiqs-latest-state-of-ai-report-the-10-most-important-data-points-for-saas-founders
14. lorikeetcx.ai/articles/best-outcome-priced-ai-support-regulated-2026 ; thesaascfo.com/how-to-build-outcome-based-pricing
15. algeriatech.news/?p=28730 (secondary, UNVERIFIED)
