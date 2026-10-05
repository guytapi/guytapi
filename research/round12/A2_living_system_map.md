# Thesis A2: Living, evidence-backed system map ("AI agents rewrite your systems every day and nobody knows the real architecture anymore. We generate a living, evidence-backed map of your entire system — every service, endpoint, data flow, field and credential — straight from code and infrastructure, and flag what changed, what's exposed and what broke.")

**Date:** 2026-10-05 | **Round:** 12 | **Method:** round7/METHOD.md template, plus original bar, simulated buyers, VC committee and red team | **Searches used:** 37 of 40 (WebFetch and Reddit were blocked, so evidence comes from search snippets only).

Legend: [S] = source found in search results this round. [U] = unverified or estimated. [I] = my inference.

**Founder edge:** "Vara Architecture" already works. It builds an evidence-backed graph from a codebase plus Terraform. The graph covers systems, Cloud Run containers, every HTTP endpoint (module/handler/method/path, gateway-exposed flag), data stores, third parties, end-to-end flows, field-level mappings, machine credentials and validation issues. Every node carries a pointer to a file and line (e.g. `cloud_run.tf:100`). Import (incl. OpenAPI), export, query and validation are exposed via API/MCP.

**Bottom line (up front): REFRAME. The broad "living system map" thesis dies. One narrow wedge is worth a 14-day test.**

- **The pain is real and among the best documented we have seen.** Faros 2026 (22,000 devs): 5x median review time, 3x incidents per PR, production incidents tripled. "Comprehension debt" became a named category in 2026. Geoffrey Litt's "Understanding is the new bottleneck" (AI Engineer, Jul 2026).
- **But every one of the four use cases already has a funded owner, and most have a free one:**
  1. **Agent context:** Augment Context Engine MCP (GA Feb 2026), Unblocked ($20M A), Sourcegraph, Greptile, Qodo ($70M B, Mar 2026), Swimm 2.0, Bito AI Architect, GitNexus, Graphify. Free options: DeepWiki MCP and Windsurf Codemaps.
  2. **System-level security review of PRs:** Apiiro (Deep Code Analysis plus "Material Change" detection; Guardian Agent Jan 2026; AI Threat Modeling Mar 2026 "detects drift between design and code"; ARR +104% in 2025). Endor Labs ($93M B; PR agents "for changes to architectures that affect security posture"). Prime ($20M A), Clover ($36M), Seezo ($7M, Accel). Plus Wiz Code, Cycode+Bearer, Ox, Snyk Evo and Checkmarx.
  3. **Always-current docs:** Google Code Wiki (free, regenerates on commit), DeepWiki (free), Driver ($8M, GV), Eraser (Eraserbot updates diagrams on every PR), Brainboard and Pluralith (Terraform diagrams).
  4. **Incident response / runtime truth:** Datadog IDP and service maps, Port Context Lake, Cortex.
- **What remains uncovered is narrow:**
  - a **deterministic, file:line-cited** graph that joins **application code with IaC** down to **field-level PII flows and machine credentials**;
  - **diffed per PR** and **priced for mid-market regulated companies** that cannot justify Apiiro.
- That gap is real but feature-sized. Apiiro and Endor are one roadmap item away, and their buyers already own the budget line.

---

## 1. Problem
- Coding agents now write 30-75% of PRs at leading companies (round 8). No human holds a mental model of the system, and diagrams and docs go stale within weeks.
- **Agents** make cross-service mistakes: they edit one service and guess at downstream schemas.
- **Security and architecture review** cannot keep pace with PR volume. The risky changes are system-level, not line-level: a new public endpoint, a new PII flow, a new third party, a new credential use.
- **Audits and customer questionnaires** ask for current data-flow diagrams that nobody keeps up to date.

## 2. Recent evidence (pain NOW)

| # | Signal | What it shows | Source |
|---|---|---|---|
| 1 | Faros AI Engineering Report 2026 (22,000 devs, 4,000 teams): PR size +51%, bugs/PR +28%, **median review time 5x**, incidents/PR 3x, code churn 10x, production incidents tripled | Review is the bottleneck, and quality degrades at system level | [S](https://faros.ai/research), [S](https://www.augmentcode.com/guides/ai-productivity-paradox-engineering-delivery) |
| 2 | Faros 2025 (10,000 devs): +98% PRs merged, review time +91%, PR size +154% | Trend confirmed a year earlier | [S](https://getunblocked.com/blog/ai-productivity-paradox/index.md) |
| 3 | "Comprehension debt" (Addy Osmani and many others, 2026). Stack Overflow 2026: 76% of AI-tool users ship code they don't fully understand. Anthropic study: AI-assisted engineers scored 17% lower on comprehension (50% vs 67%) | The problem has a name and data behind it | [S](https://addyosmani.com/blog/comprehension-debt/), [S](https://tianpan.co/blog/2026/06/21/comprehension-debt-the-system-no-human-understands) |
| 4 | Geoffrey Litt (Notion), AI Engineer Jul 2026: "Understanding is the new bottleneck"; built "Explain Diff" | Thought leaders now frame understanding, not writing, as the constraint | [S](https://www.ai.engineer/speakers/geoffrey-litt) |
| 5 | Architecture drift posts: "an agent producing 10 PRs per day across 5 services can introduce drift that would take a team a week". DIY tools on dev.to and GitHub | Practitioners build their own fixes, which is the classic early signal (but also shows it is sprint-buildable) | [S](https://techdebt.guru/ai-architecture-drift/), [S](https://dev.to/deepcodersinc/agentic-coding-architectural-drift-heres-what-i-built-to-fix-it-4h2j), [S](https://github.com/Double00kevin/ai-architecture-map) |
| 6 | arXiv 2604.04990 "How AI Coding Agents Shape Software Architecture" | Academic attention | [S](https://arxiv.org/pdf/2604.04990) |
| 7 | Checkmarx (Apr 2026): 81% knowingly shipped vulnerable code. Survey: 93% use AI code, only 12% apply the same controls. 69% say AI code introduced vulnerabilities | AppSec cannot keep up | [S](https://nhimg.org/articles/manual-appsec-triage-is-becoming-a-governance-liability/), [S](https://www.tullahomanews.com/?p=105948) |
| 8 | Context-engineering posts: agents "write correct code against the wrong picture of the system"; "cross-repo blindness" | Demand for an architecture-level model as agent context | [S](https://bito.ai/blog/ai-coding-agents-collapse-in-real-production-systems/), [S](https://devsu.com/resources-center/context-engineering-ai-coding-agents) |
| 9 | Augment: adding Context Engine improved agent performance 70%+ across Claude Code/Cursor/Codex (vendor claim) | Context measurably helps, and the incumbent already captures that value | [S](https://augmentcode.com/blog/context-engine-mcp-now-live) |
| 10 | Security questionnaires routinely ask "Do you have data flow diagrams for customer data?" | Steady compliance pull for current DFDs | [S](https://wolfia.com/security-questionnaire-questions/do-you-have-data-flow-diagrams-for-customer-data) |

**Cost of stale architecture docs:** no sourced dollar figure was found [U]. Driver claims source-code documentation takes "two hours vs three months" (vendor claim) [S](https://pulse2.com/driver-8-million-seed-funding-raised-for-simplifying-technical-documentation/). The pain is expressed as review time, incidents and security exposure, not as a "docs" budget.

## 3. Who has the pain
- VP Eng / CTO at companies with 50-2,000 engineers and heavy agent adoption (review load, incidents, onboarding).
- CISO / Head of AppSec (agent PR volume, design review coverage of 10-15%).
- Platform / agent-infrastructure teams (agent context quality).
- GRC / compliance in regulated mid-market (fintech, healthtech, insurtech): DFDs, PCI scoping, DPIA, SOC 2.

## 4. What they do today
- **Agent context:** CLAUDE.md/AGENTS.md files, Augment/Sourcegraph/Greptile indexing, DeepWiki MCP, or nothing. Agents run agentic search (grep) at runtime.
- **Security review:** Apiiro/Endor/Wiz Code/Cycode at enterprise level. Manual design reviews (10-15% coverage per Prime). Semgrep/CodeQL rules for "new route" checks.
- **Docs:** Confluence diagrams, Eraser/Lucid, Brainboard for Terraform, Code Wiki/DeepWiki for public repos.
- **Incidents:** Datadog/Dynatrace runtime service maps, Port/Backstage catalogs.

## 5. Why current products fail
- Doc/wiki tools (DeepWiki, Code Wiki, Driver, Codemaps) produce **LLM prose and diagrams**. They are not a queryable, deterministic graph, they are per-repo, and they ignore IaC exposure and credentials [I].
- Context engines (Augment, Sourcegraph, Greptile) model **symbols and files, not systems**: they know nothing of gateway exposure, Cloud Run topology or field-level PII flow [I].
- IaC diagrammers (Brainboard, Pluralith) see infrastructure but not handlers, fields or flows.
- Runtime maps (Datadog) see only traffic that already ran in production. They cannot gate a PR.
- ASPM (Apiiro, Endor) **does** model architecture from code and flags material changes. It is enterprise-priced and security-only, and does not serve as an agent-consumable system model for engineering [I; Apiiro pricing U]. **This is the one real gap, and it is the weakest one: it is a pricing/segment gap, not a capability gap.**

## 6. Why now
- Agent PR share (30-75%), review time 5x, incidents 3x.
- MCP makes "architecture as a tool call" distributable.
- Evidence pointers matter more now because LLM-generated docs hallucinate, and agents need verified context (Swimm 2.0's "AI summarizes, never invents" positioning shows incumbents see this too) [S](https://swimm.io/blog/swimm-2-0-the-understanding-platform-for-ai-modernization).

## 7. Potential product
- **Vara Architecture as an "architecture diff" engine:**
  - On every PR, rebuild the graph and emit a system-level diff: new or changed endpoints and their exposure, new data-store or third-party edges, new PII field flows, credential use, and broken flows.
  - Each diff item carries file:line evidence.
  - Policy gates, e.g. "a public endpoint touching PII requires AppSec review".
- **Same graph, three more outputs:**
  - an MCP tool for agents (`get_flow`, `who_calls`, `blast_radius`);
  - auto-exported DFDs and asset inventories for SOC 2 / PCI / DPIA;
  - incident blast-radius lookup.

## 8. Time to value
- Connect repos plus Terraform and get the first map in hours. This is credible because the tool already works.
- The first useful PR diff arrives within a day.
- **Risk [I]:** accuracy on polyglot and multi-cloud estates beyond the founders' GCP/Cloud Run stack. Expect weeks of parser work per new framework or cloud (AWS API Gateway/Lambda, K8s ingress, Kong).

## 9. Pilot (14-30 days)
- **Days 1-3:** connect 5-20 repos plus Terraform and produce the baseline map. Have the customer's staff engineer grade accuracy on 50 random nodes (target ≥90%).
- **Days 4-25:** run a GitHub check on the next 50-200 agent PRs that posts the system-level diff. Measure:
  - how many diffs surfaced something reviewers would otherwise have missed (new public endpoint, PII-to-third-party, credential);
  - AppSec review minutes per PR;
  - and, if the MCP is enabled, cross-service agent errors in an A/B on 20 tasks.
- **Day 30:** export the DFD and inventory for their SOC 2/PCI auditor.
- **Success:** ≥3 "we would have shipped that" catches and an AppSec lead willing to pay.

## 10. Willingness to pay
- Comparable spend: ASPM tools sell to enterprises at roughly $50K-$500K+ [U]. Design-review agents (Prime/Clover/Seezo) reportedly sell at $30K-$150K [U]. Doc tools are cheap or free (DeepWiki, Code Wiki) and Eraser sells per seat [U].
- **Realistic ACV for this wedge: $20K-$60K mid-market and $80K-$200K enterprise [U].**
- Weak spots:
  - "Docs" alone has near-zero WTP because the free tools exist.
  - Agent context is bundled into the coding-agent spend (Augment, Cursor).
- Budget exists only on the security/compliance side.

## 11. Expansion
- System-level PR gate → compliance evidence (continuous DFDs, PCI scoping, DPIA, AI-BOM) → "system of record for how software actually works", feeding agents, IR, M&A diligence and catalogs.
- Expansion is plausible on paper, but each step collides with an incumbent: Apiiro/Wiz (security), Vanta/Drata (compliance evidence, Vanta at $300M ARR [S](https://sacra.com/research/vanta-at-300m-year/)), and Port/Datadog (catalog).

## 12. Competition (search-hard results)

| Player | What it does vs A2 | Funding / traction | Source |
|---|---|---|---|
| **Apiiro** | Deep Code Analysis builds a software graph of code, APIs, data flows, OSS, cloud and runtime. Material Change detection blocks PRs. Guardian Agent (Jan 2026). AI Threat Modeling (Mar 2026) "detects drift between design and code". **Closest competitor on use case 2** | $135M raised; valuation est. $500M-1B [U]; ARR +104% in 2025; Fortune 500 | [S](https://www.helpnetsecurity.com/2026/03/23/apiiro-ai-threat-modeling/), [S](https://apiiro.com/news_item/apiiro-achieves-104-arr-growth-in-2025-as-fortune-500-adopt-agentic-appsec-to-reduce-massive-risk-across-the-software-development-lifecycle), [S](https://stockanalysis.com/private/apiiro/) |
| **Endor Labs** | AI agents review PRs "for changes to architectures that affect security posture" | $93M B (Apr 2025), $188M total | [S](https://qnow.quantisnow.com/insight/endor-labs-raises-93m-series-b-to-secure-the-ai-5997607) |
| Prime Security | "Agentic Security Architect": automated design reviews. PayPal, Qualtrics, Bumble | $20M A (Dec 2025, Scale) | [S](https://www.businesswire.com/news/home/20251209948665/en/Prime-Security-Raises-$20M-From-Scale-Venture-Partners-to-Transform-Product-Security-With-the-First-Agentic-Security-Architect) |
| Clover Security | AI design reviews; ServiceNow invested Mar 2026 | $36M | [S](https://www.bankinfosecurity.com/clover-raises-36m-to-automate-product-security-reviews-a-30238) |
| Seezo / DevArmor | Security design review automation | $7M A Accel / bootstrapped ~$770K revenue | [S](https://www.trysignalbase.com/news/funding/seezo-raises-7m-seed-round), [S](https://getlatka.com/companies/devarmor.com) |
| Cycode (+Bearer) | ASPM, API discovery, 120+ sensitive data types in code flows; material code change alerting | Acquired Bearer Mar 2024 | [S](https://cycode.com/blog/cycode-acquires-bearer/), [S](https://cycode.com/blog/ai-driven-material-code-change-alerting/) |
| Wiz Code (Google) | Code-to-cloud security graph, runtime to code owner | Inside Google Cloud 2026 | [S](https://www.wiz.io/) |
| Ox / Snyk Evo / Checkmarx One | Agentic AppSec, AI-BOM; Snyk Evo 60% of new deal volume | Ox $94M; Snyk/Checkmarx large | [S](https://www.ox.security/press/as-ai-accelerates-code-generation-ox-security-raises-60m-to-focus-developers-on-the-5-of-risks-that-truly-matter/), [S](https://cyprusshippingnews.com/2026/09/22/as-ai-risk-scales-and-vulnerabilities-compound-evo-by-snyk-reaches-60-of-new-deal-volume/) |
| Akto (Levo, Salt, Traceable similar) | API inventory from source code via AI agents, any language | Funded API security | [S](https://docs.akto.io/api-inventory/concepts/api-inventory-from-source-code) |
| Relyance AI | Code + infra + vendor data-flow mapping for privacy | $62M total (M12) | [S](https://www.relyance.ai/press-releases/relyance-ai-emerges-from-stealth-with-30m-in-funding-to-give-privacy-pros-real-time-insights-into-their-codebase) |
| Augment Context Engine | Cross-repo context MCP for any agent; GA Feb 2026 | Augment $1.4B val | [S](https://www.augmentcode.com/changelog/context-engine-mcp-in-ga) |
| Unblocked | Org context engine/MCP; customers with 100K+ repos | $20M A | [S](https://getunblocked.com/blog/best-engineering-knowledge-platforms-ai-coding-agents-2026/) |
| Sourcegraph | Code graph, Deep Search cross-repo (split from Amp Dec 2025) | 800K devs | [S](https://ai.engineer/orgs/sourcegraph-amp) |
| Greptile / Qodo / CodeRabbit | Graph-indexed PR review, cross-repo breaking-change detection | Qodo $70M B Mar 2026 | [S](https://thenewstack.io/qodo-cross-repo-code-review/), [S](https://en.globes.co.il/en/article-1001538970) |
| Bito AI Architect | "Deep system context layer" MCP for design/coding/review agents | n/a [U] | [S](https://bito.ai/ai-tools/best-mcp-servers/) |
| Swimm 2.0 | Deterministic "understanding platform" with MCP, legacy focus | Dawn Capital-backed | [S](https://swimm.io/platform) |
| GitNexus / Graphify (YC) | Deterministic org-wide code knowledge graph over MCP | Early | [S](https://producthunt.com/products/gitnexus-akon-labs), [S](https://graphify.com/yc) |
| Cognition DeepWiki + Codemaps | Free wikis with Mermaid architecture diagrams and an MCP; Codemaps shows data flow and dependencies with click-to-line | Free / Devin Pro for private repos | [S](https://codersera.com/blog/deepwiki-complete-developer-guide-2026/), [S](https://cognition.ai/blog/codemaps) |
| Google Code Wiki | Free, regenerates architecture/sequence diagrams on each commit (public repos; private via Gemini CLI planned [U]) | Google | [S](https://www.infoq.com/news/2025/11/google-code-wiki) |
| Driver | Codebase → architecture maps and docs | $8M seed (GV, YC W24) | [S](https://pulse2.com/driver-8-million-seed-funding-raised-for-simplifying-technical-documentation/) |
| Eraser | Diagrams from codebase; Eraserbot updates on every PR; MCP | VC-backed [U] | [S](https://docs.eraser.io/what-is-eraser) |
| Brainboard / Pluralith / Inframap | Terraform → diagrams in CI | Small | [S](https://www.brainboard.co/blog/ai-terraform-diagrammer) |
| Port / Cortex / Datadog IDP | Catalog plus "Context Lake" MCP; Datadog AI-generated Systems | Large | [S](https://docs.port.io/context-lake/overview/), [S](https://www.datadoghq.com/about/latest-news/press-releases/datadog-launches-internal-developer-portal-to-give-engineering-teams-autonomy-and-help-them-ship-production-ready-code-quickly/) |
| Multiplayer.app | Pivoted from auto-documented architecture to full-stack session recording | $3M (2023) | [S](https://www.getapp.com/collaboration-software/a/multiplayer/) |
| CodeSee | Dead (codebase maps) [U, not re-verified] | — | — |

**What exactly is uncovered:**
- The combination: (a) cross-repo **plus IaC** join (handler → container → gateway exposure); (b) **field-level** PII mapping; (c) **machine credentials**; (d) **file:line evidence on every node**; (e) **deterministic PR diff**; (f) **agent-consumable API/MCP**; (g) **mid-market price**.
- No single vendor was found shipping all seven. Apiiro covers roughly a, b, d-ish, e and partly f, at enterprise prices [I].

## 13. Moat (10 / 100 / 1,000 customers)
- **10:** none. Parsers plus prompts, and a strong platform engineer can replicate the 70% version.
- **100:** framework/IaC parser coverage plus a curated policy library ("dangerous architecture changes") plus labeled diffs. This is a modest data moat, and Apiiro holds a larger version (patented DCA).
- **1,000:** a graph embedded in PR gates, audit evidence and agent context creates switching costs as a system of record. That is the same position Apiiro/Wiz are taking with larger distribution.
- **Net:** moat is weak to moderate. Defensibility comes from workflow embedding, not technology.

## 14. Market math
- Mid-market regulated software companies (50-1,000 engineers, fintech/health/insurtech/B2B SaaS selling to enterprise): about 5,000-10,000 globally [U].
  - **$10M ARR** = about 250 customers at $40K. Plausible in 4-5 years if the wedge works.
  - **$50M ARR** = about 800 at $40K plus 100 enterprise at $150K. Requires beating Apiiro/Endor/Wiz downmarket.
  - **$100M ARR** = requires becoming the "system of record for how software works" across engineering, security and compliance, i.e. displacing ASPM and catalog spend.
- **$10B outcome?** Only as a Wiz-like category creator. The category (ASPM + code-to-cloud graph) already has Wiz (Google, $32B) and Apiiro, so the $10B slot is taken [I].

## 15. CTO test sentence
"On every agent PR, we show you, with file-and-line proof, which public endpoints, PII fields, third parties and credentials changed across your services and Terraform. We also hand that same verified map to your agents and your auditors."

## 16. Kill test question
"Show the CISO of a 300-engineer fintech that has Wiz or Snyk a 30-day diff report on their agent PRs. Do they pay $40K on top of what they have, or say 'Apiiro/Endor/our ASPM already does material-change detection'?"

## 17. Scores (METHOD, 1-10)

| Criterion | Score | Why |
|---|---|---|
| Pain severity | 7 | 5x review time, 3x incidents; system-level comprehension loss is real |
| Urgency | 6 | Security leaders feel it now; "docs" urgency is low |
| Market timing | 7 | Peak relevance, but funding already arrived (2025-26) |
| Speed to pilot | 8 | Tool exists; repos + TF → map in hours |
| Ease of integration | 7 | GitHub App + read-only TF; accuracy beyond GCP unproven |
| Ease of reaching customers | 5 | AppSec buyers are saturated with ASPM pitches |
| Willingness to pay | 5 | Only the security/compliance framing pays; docs/context are free or bundled |
| Competition | 3 | Apiiro, Endor, Prime, Clover, Wiz Code, Augment, Unblocked, free DeepWiki/Code Wiki |
| Moat potential | 4 | Workflow embedding only; Apiiro patents DCA |
| Market size | 6 | Large adjacent spend (ASPM, compliance), contested |
| VC attractiveness | 5 | Good story, crowded "AI code security" category; VCs will ask "why not Apiiro?" |
| **Average** | **5.7** | |

## 18. Original bar scores (bar: 8.5 avg, no category below 7)

| Category | Score |
|---|---|
| Pain | 7 |
| Urgency | 6 |
| ROI clarity | 4 (catches are anecdotal; "review minutes saved" is soft) |
| Customer accessibility | 5 |
| Pilot speed | 8 |
| Market size | 6 |
| Expansion | 7 |
| Venture potential | 5 |
| Defensibility | 4 |
| Why now | 8 |
| Competition position | 3 |
| **Average** | **5.7. Fails the bar (five categories below 7)** |

## 19. Five simulated buyers
1. **CISO, 400-eng Series D fintech (has Wiz + Snyk):** MAYBE. "PII-to-third-party diff with line evidence is exactly what my PCI QSA asks for. But Snyk Evo and Wiz Code are adding this; I'll pilot if it's cheap and doesn't add another dashboard."
2. **Head of AppSec, F500 bank (Apiiro customer):** NO. "Apiiro material change plus threat modeling covers this. I'm consolidating vendors."
3. **VP Eng, 150-eng B2B SaaS heavy on Claude Code:** NO for docs, MAYBE for context. "DeepWiki and Augment are good enough; my agents grep the code anyway. I won't pay for a map."
4. **Platform lead, 800-eng marketplace:** NO. "We built a service graph from Backstage + Terraform state + OpenAPI in a quarter. Field-level flow is nice, not budget-worthy."
5. **Head of GRC, 200-eng healthtech pre-SOC2 Type II / HITRUST:** YES (small). "Auto-generated, evidence-cited DFDs and asset inventory save me weeks per audit and per questionnaire. $15-25K, not $60K."

**Tally:** 1 YES (small), 2 MAYBE, 2 NO.

## 20. VC committee view (simulated)
- **Bull:**
  - Strongest pain narrative of the year (comprehension debt, Faros data).
  - The founders have a working, differentiated deterministic graph.
  - MCP distribution.
  - Apiiro's 104% ARR growth proves budget.
- **Bear:**
  - Apiiro has a 5-year head start and a patent.
  - Wiz (Google) owns code-to-cloud, and Endor/Prime/Clover took the agentic design-review seed and Series A slots in 2025-26.
  - Free DeepWiki/Code Wiki anchor docs at $0, and Augment/Unblocked own agent context.
- **Committee outcome:** "Interesting team asset, not a fundable standalone category. Come back with 10 paying mid-market security buyers or a clear compliance-evidence wedge with Vanta-like velocity." **Pass at this stage.**

## 21. Red team
- **"A platform team builds it in a sprint."** Partly true. A 70% map (tree-sitter routes + Terraform graph + LLM summary) takes 2-6 weeks with Claude Code. Field-level flows, evidence integrity and cross-framework accuracy take months, but most buyers will not value that last 30% until an incident happens.
- **"Agents don't need a map."** Agentic search (grep at runtime) is winning in Claude Code/Codex. A precomputed graph helps mainly cross-repo and with IaC, and Augment/Sourcegraph already sell that.
- **Platform absorption:**
  - GitHub (Copilot code review plus code scanning) could add "architecture change" summaries.
  - Cognition already has DeepWiki plus Codemaps plus Devin Review.
  - Google has Code Wiki plus Wiz.
  - Anthropic ships Claude Code security review.
  - The free tier of this category is being given away.
- **Accuracy liability:** a security gate that misses a public PII endpoint is worse than none. Evidence pointers help, but coverage claims are hard on polyglot estates.
- **The founders' graph is tuned to their own GCP/Cloud Run/fintech stack.** Generalizing to AWS/K8s/Kong/Lambda plus 10 frameworks is a long tail.
- **"Docs for audits" has low WTP** and Vanta/Drata can add DFD generation from cloud integrations [I].
- **Pain-competition inverse law (STATUS.md conclusion 2) holds again:** the best-evidenced pain had the most funded entrants.

## 22. Would a platform team build it? Would platforms give it away? What is defensible?
- **Build in-house:** yes for the map (2-6 weeks). Probably not for a maintained, multi-framework, evidence-checked diff with a policy library. That is the only buyable part.
- **Give away:**
  - DeepWiki, Code Wiki and Codemaps are already free.
  - GitHub/Cursor/Anthropic will keep bundling "understand this repo".
  - None of them currently ships IaC exposure, field-level PII flow or credential-diff gates [I], but Wiz (Google) and Apiiro do adjacent versions.
- **Defensible:**
  - parser coverage plus a curated "dangerous system change" policy corpus plus audit-evidence workflow lock-in;
  - possibly a regulated-vertical specialization (fintech: transaction-screening/regulatory-filing flows, PCI scoping) where the founders have domain knowledge.

## 23. Recommended wedge for THESE founders
**Rank:**
1. **System-level security/compliance diff of agent PRs for regulated mid-market (fintech/healthtech, 50-500 engineers).** Sharpest.
2. Compliance evidence (continuous DFD/asset inventory).
3. Agent context. Weakest: free substitutes and bundling by Augment/Cursor/Cognition.

**Wedge spec: "Architecture change control for regulated software"**
- GitHub check plus weekly digest. Each agent PR gets a diff:
  - new or changed gateway-exposed endpoints;
  - new PII field flows (especially to third parties or logs);
  - new machine-credential use;
  - new data stores;
  - broken end-to-end flows (e.g. "transaction screening" no longer reaches the sanctions provider).
- Every item cites file:line.
- The same graph exports a PCI/SOC 2/DPIA-ready DFD and inventory on demand.

**Why this wedge:**
- It reuses every component the founders have.
- It sells to a budget holder (CISO/compliance), not to "docs".
- "Flows broke" is a fintech-native story (screening/filing) that generic ASPM does not tell.
- It is priced below Apiiro ($20-50K).

**14-day test:**
- 8 calls with CISOs/Heads of Security at Series B-D fintechs on GCP (founders' stack strength).
- Run the tool on 2 design partners' repos and replay their last 100 merged PRs.
- **Pass:** ≥3 diff items per partner that the security lead calls "we didn't know", plus 2 verbal commits at ≥$25K.
- **Kill:** "our ASPM does this", or catches limited to things CodeQL/Semgrep already flag.

**Expected ceiling:** $10-30M ARR unless it expands into a compliance system of record.

## 24. Kill signals
- Design partners already have Apiiro/Endor/Cycode material-change detection and see no delta.
- Replay of 100 historical agent PRs yields <1 material system-level finding per 50 PRs.
- Accuracy <90% on a non-GCP estate after 2 weeks of parser work.
- Snyk Evo, Wiz Code or GitHub ship "architecture change summary / new public endpoint + PII flow" PR checks in Q4 2026.
- Buyers will only pay for it as a compliance document (<$15K ACV).
- Vanta/Drata announce code-derived DFDs.

---

## VERDICT: REFRAME (avg 5.7; original bar 5.7; fails bar)
- **Strong pain, crowded on every use case.** The broad "living system map" is killed by crowding plus platform absorption (free DeepWiki/Code Wiki/Codemaps; Augment/Unblocked for context; Apiiro/Endor/Wiz for security).
- **Best wedge:** evidence-cited system-level security and compliance diffs of agent PRs for regulated mid-market fintech/healthtech. Run it as a 14-day test only.
- Even if it works, treat Vara Architecture as a **feature/asset**, possibly folded into Vara's security offering, rather than a venture-scale standalone, unless design partners prove a compliance-evidence pull.

### Sources (all from search results this round; none invented)
- Faros research: https://faros.ai/research ; Augment summary: https://www.augmentcode.com/guides/ai-productivity-paradox-engineering-delivery ; Unblocked summary: https://getunblocked.com/blog/ai-productivity-paradox/index.md
- Comprehension debt: https://addyosmani.com/blog/comprehension-debt/ ; https://tianpan.co/blog/2026/06/21/comprehension-debt-the-system-no-human-understands
- Litt: https://www.ai.engineer/speakers/geoffrey-litt
- Drift: https://techdebt.guru/ai-architecture-drift/ ; https://dev.to/deepcodersinc/agentic-coding-architectural-drift-heres-what-i-built-to-fix-it-4h2j ; https://github.com/Double00kevin/ai-architecture-map ; https://arxiv.org/pdf/2604.04990
- AppSec: https://nhimg.org/articles/manual-appsec-triage-is-becoming-a-governance-liability/ ; https://www.tullahomanews.com/?p=105948
- Context: https://bito.ai/blog/ai-coding-agents-collapse-in-real-production-systems/ ; https://devsu.com/resources-center/context-engineering-ai-coding-agents ; https://augmentcode.com/blog/context-engine-mcp-now-live ; https://www.augmentcode.com/changelog/context-engine-mcp-in-ga
- Competitors: links in §12.
