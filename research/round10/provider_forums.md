# Round 10: Provider forums and issue trackers (Jun to Oct 2026)

Date: 2026-10-05. Method: the founder's pain-first template (round7/METHOD.md), applied only to the AI providers' own channels. GitHub issue counts and reactions were pulled live through the GitHub issue-search API, sorted by reactions, for issues created on or after 2026-06-01. Forum threads came from web search restricted to each forum's domain. Direct page fetch and Reddit were blocked, so forum thread *contents* come from search snippets. Every URL below appeared in a tool result; none was constructed by hand. 21 web searches and 9 GitHub searches were used.

Excluded as already killed: model-retirement migration, prompt-cache visibility, spend caps, secrets in transcripts, MCP OAuth, generic evals and observability.

## Where the volume is (top-reacted issues since 2026-06-01)

- **anthropics/claude-code** (35,050 issues since June). The top items are model behaviour and harness changes, not just bugs. #77136 is the rhetorical-tics regression across 4.7/4.8/5.0/Fable (575 reactions, 138 comments). #65961 is verbose comments that ignore instructions (250). #80988 is a hidden `heron_brook` prompt that overrides user delegation policy (91). #87647 reports that "Over 6k issues labeled has-repro auto-closed" (85).
- **openai/codex** (19,147 issues). The top items are the quota cost per token jumping 10-20x (#28879, 560 reactions), reasoning-token clustering at 516/1034/1552 degrading complex tasks (#30364, 428), context cut from 353K to 258K against an advertised 1.05M (#32806, 68), and encrypted MultiAgentV2 messages removing the readable audit trail (#28058, 145).
- **Low-volume channels**: vercel/ai, openai-agents-python, anthropic-sdk-python, and the modelcontextprotocol spec repo each have issues with fewer than 15 reactions. Builders' cross-provider pain shows up there as many small schema and compatibility bugs, not as upvoted threads.
- **google-gemini/gemini-cli**: the issues are about model availability and silent substitution (#28859: any `--model gemini-*-flash` is silently served by 3.5-flash, "including versions that do not exist").

## Clusters

| # | Cluster | Independent reporters / threads (Jun-Oct 2026 unless noted) | Why providers won't fix it | Workaround today | Competitors | One-sentence product |
|---|---|---|---|---|---|---|
| 1 | **Silent model substitution and degradation** (same name, worse or cheaper model, smaller context or reasoning budget) | 20+ threads across all 4 providers and resellers; 1,000+ reactions in total (see the A table below) | Conflict of interest: quietly cutting compute is how they protect margin under capacity limits, and they will not certify against themselves | Personal canary prompts, public watchdogs, rolling back versions, anecdote threads | AIStupidLevel (OSS), IsItNerfed, Marginlab tracker, stillsane (OSS canary), OpenRouter Auto Exacto (open-weight only), Latitude, every eval vendor | Independent, account-specific "are you getting the model you pay for" attestation, producing evidence fit for contracts |
| 2 | **Vendor harness drift** (server-side flags, A/B experiments and self-updates change coding-agent behaviour under enterprise config) | CC #80988 (91), #62061 (50), #90450 (48), #87971 (97), #87575 (42), #75607 (16), #95690 (14); Codex #28058 (145), #41622 (99), #39903 (83), #31814 (206) | Continuous experimentation is their release method, and they won't expose cross-vendor change control | Pin the CLI (fails: #75607 reports self-update despite `autoUpdates:false`), cchistory diffs, `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` | cchistory, claude-code-changelog (bot), Piebald claude-code-system-prompts, phistory (multi-CLI), Anthropic server-managed settings, Codex requirements.toml feature pins, TrueFoundry/Fiddler gateways | Change-control gate that diffs every harness, prompt and flag change and canaries it on your repos before it reaches the fleet |
| 3 | **Capacity lies** (429 at very low quota, new accounts at 0 TPM, stuck batch/background jobs) | Gemini forum: 10 threads, including "429 at 0.03% of quota", "since Aug 4 2026 half of gemini-3.6-flash calls 429". AWS re:Post: 10 threads on "quotas stuck at 0 / Too many tokens per day" on new accounts. OpenAI: Batch stuck threads, Responses background "stuck in queued, Sept 2026". CC #69415 (92), #69358 (61) | They are capacity-constrained, and honest quota reporting exposes it | Multi-provider failover, retries, keeping several accounts | OpenRouter, Portkey, LiteLLM, Vercel/Cloudflare AI Gateway, Martian, Not Diamond (very crowded) | (Gateway feature; not a company) |
| 4 | **Cross-provider structured output and tool-schema incompatibility** | vercel/ai #16662, #16121, #18199, #20729, #16298, #16021, #16926; anthropic-sdk #1925, #1926, #1759, #1764; gemini-cli #28579, #28604; MCP #2806 (oneOf not consumable); LangChain forum "response_format works for OpenAI not Gemini" | Each provider optimises its own dialect, and a common contract is against lock-in | Hand-patched converters in every SDK; hardcoded per-model lists (#18199) | BAML, Instructor, Vercel AI SDK, provider-schema-linter (OSS), LiteLLM | Schema compiler and conformance CI across providers (OSS-sized) |
| 5 | **Subscription quota metering opacity** | Codex #28879 (560), #34035 (268), #31606 (71); gemini-cli #28761 (38, "limit reached at 1-8%"); CC #78610 (49), plus a long tail since Jan (596 matches) | The quota formula is a pricing lever | ccusage-style trackers | ccusage and others; adjacent to the killed FinOps/spend-cap area | (consumer; low willingness to pay) |
| 6 | **Opaque provider-held agent state** (encrypted reasoning/messages, non-exportable conversation state) | Codex #28058 (145); OpenAI forum: Responses API state "black box / non-portable", conversation_locked threads; Gemini thought_signature errors (#28579) | Lock-in is the point | Keep your own transcript copy with `store=false` | Letta, Zep, LangGraph checkpointers, observability vendors | (thin; the audit half overlaps generic observability) |
| 7 | **Non-English tool-call corruption** | CC #83033 (153, "100% Hangul corruption"), refs #80009 and #78996; anthropic-sdk #1926 | They *will* fix it (a model bug) | Avoid escape-writing; post-process | n/a | (not a company) |
| 8 | **Provider bug trackers auto-close real bugs** | CC #87647 (85: ">6k has-repro issues auto-closed since March 2026") | Triage bots cut cost | Re-file; Discord | StatusGator, IsDown (status pages only) | Cross-provider "known regressions" registry (thin) |

**Ranking for depth.** Clusters 1 and 2 have the most independent reporters, the clearest conflict of interest at the providers, and are not killed areas. Cluster 3 is real but owned by gateways. Clusters 4-8 are feature-sized, consumer, or will be fixed by the provider.

---

## A. Model-substitution attestation ("are you getting the model you're paying for?")

**Problem.** Providers and resellers change what sits behind a model name: quantisation, reasoning budget, context window, routing to a cheaper sibling, safety system prompts, harness prompts. They do this with no version change and no notice. Builders find out from users, days later. Each provider grades itself, so no one checks independently.

**Recent evidence (independent signals):**
| Source | Date | Signal |
|---|---|---|
| github.com/openai/codex/issues/30364 | 2026-06-27 | Reasoning tokens cluster at 516/1034/1552, which may be degrading complex tasks: 428 reactions, 188 comments |
| github.com/openai/codex/issues/32806 | 2026-07-13 | GPT-5.6 Sol context cut "again" from 353K to 258K despite an advertised 1.05M: 68 reactions |
| github.com/openai/codex/issues/28879 | 2026-06-18 | Quota cost per token up about 10-20x overnight: 560 reactions |
| github.com/anthropics/claude-code/issues/83510 | 2026-08-03 | "Measurable quality regression in Claude generation 5 ... under-disclosed model fallback (Fable 5 → Opus 4.8): reproducible measurements" (24 reactions) |
| github.com/anthropics/claude-code/issues/77136 | 2026-07-13 | Rhetorical tics and incoherent prose across 4.7/4.8/5.0/Fable: 575 reactions |
| github.com/google-gemini/gemini-cli/issues/28859 | 2026-08-17 | Any `--model gemini-*-flash` silently served by 3.5-flash, even versions that don't exist |
| community.openai.com/t/i-need-to-report-a-model-routing-issue-silent-downgrade/1391776 | 2026 (date not verified) | A gpt-5-6-thinking request is routed to gpt-5-5-mini; `resolved_model_slug` shows it |
| community.openai.com/t/chatgpt-is-silently-downgrading-to-mini-models/1390114 | 2026 (date not verified) | Same pattern, a different reporter |
| community.openai.com/t/codex-work-gpt-6-astra-has-a-serious-model-downgrading-issue/1397173 | 2026 (latest ID range; date not verified) | Codex GPT-6-ASTRA downgrade thread, 18+ replies |
| community.openai.com/t/how-do-you-catch-silent-quality-regressions-after-a-model-update-before-users-notice/1388754 | 2026 (date not verified) | A builder's feature degraded silently for 10 days and was found by accident |
| discuss.ai.google.dev/t/...-gemini-3-6-flash-model-code-modification-failures/176502 | 2026 (date not verified) | 3.6 Flash "dumbing down" on code edits |
| forum.cursor.com/t/safeguard-fallback-to-opus-4-8-is-billed-as-the-model-you-selected-not-as-opus-4-8/172823 | 2026 (date not verified) | A reseller bills the selected model while serving the fallback |
| forum.cursor.com/t/composer-2-5-degradation-or-redirect/164147 | after 2026-06-20 | Suspected redirect to a cheaper model |
| forum.cursor.com/t/available-context-for-many-models-being-truncated/139480 | earlier in 2026 | Advertised 200K, but about 36K is lost |

**Who has the pain.** Teams running LLM features in production with more than about $500K a year of model spend: fintech, legal, support automation, and coding-agent platform teams. Resellers also face it (Cursor-style tools, OpenRouter customers).

**What they do today.** Ad-hoc canary prompts and personal eval suites, and checking public watchdogs (AIStupidLevel, IsItNerfed, Marginlab). They post forum threads and wait for a postmortem. Anthropic's 2026 postmortems (a reasoning-effort downgrade on Mar 4, a cache bug on Mar 26, a verbosity prompt on Apr 16, per mcp.directory's summary) were all found by users first.

**Why current products fail.** Public watchdogs test the provider's default path, not *your* tier, region, plan, reseller, or harness. Eval and observability vendors measure your app, not whether the upstream changed, so they cannot separate "my prompt broke" from "they swapped the model". None produce evidence a procurement team can put into a contract clause. Contract-advice posts (tianpan.co, Jul 2026) tell buyers to negotiate "right to validate updates" and pinned snapshots, but no one supplies the validation.

**Why now.** 2026 brought a public run of confirmed silent changes at all three labs, plus capacity rationing (cluster 3) that makes silent cost-cutting more likely. Enterprise LLM contracts are now big enough for quality clauses (OpenAI-on-AWS, Bedrock commits).

**Potential product.** Continuous probes from the customer's own keys and accounts: behavioural fingerprints, context-length and reasoning-budget probes, and private task canaries. Statistical change-point detection (CUSUM) runs per model × surface × region. The output is a signed evidence log and a "drift incident" report that maps to contract clauses and SLA claims.

**Time to value.** One day (API keys only; no SDK).
**Pilot (14-30 days).** Run on 3 provider accounts and 2 resellers. Success means catching at least one undisclosed change the customer didn't know about, with a timestamped evidence pack.
**Willingness to pay.** Weak to moderate. Platform teams already pay eval vendors. A separate "attestation" line item is unproven. The plausible buyer is procurement/vendor-risk at large AI-spend enterprises, at roughly $20-60K a year.
**Expansion.** Multi-provider benchmarking for routing decisions; reseller verification (Cursor/OpenRouter tier); insurer and auditor data feed.
**Competition.** AIStupidLevel (OSS, 21 models, CUSUM), IsItNerfed, Marginlab, stillsane (OSS canary), OpenRouter Auto Exacto (scores providers every ~5 minutes on tool-call telemetry, but open-weight pools only), Latitude/FutureAGI/Klu drift features, plus Braintrust/Arize/LangSmith one feature away. A provider could kill the wedge overnight by exposing `resolved_model` and a change log (Azure Foundry model router already returns ordered attempts and fallback metadata).
**Moat.**
- 10 customers: none (probes can be copied).
- 100 customers: a cross-customer panel; seeing the same change across many accounts sooner and with more certainty than anyone else.
- 1,000 customers: becomes the reference data source for AI contracts and insurers. This is credible only at that scale.

**CTO test sentence.** "We tell you, with signed evidence, the day OpenAI, Anthropic, Google, or your reseller changes the model behind your contract, before your users do."
**Kill test question.** Will 5 enterprise procurement or vendor-risk owners (not engineers) commit $20K+ to independent attestation, given that watchdogs are free and an eval vendor could add upstream drift?

**Scores (1-10):**
| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market size | VC attractiveness | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 7 | 5 | 7 | 9 | 9 | 5 | 4 | 4 | 4 | 5 | 5 | **5.8** |

**Verdict.** This is the loudest cross-provider pain in the providers' own channels, and the conflict of interest is real. But engineers' pain is high while their willingness to pay is low, free watchdogs exist, and the paying version shrinks into "generic evals with an upstream lens" (killed). It fails the bar at 5.8.

---

## B. Harness change-control for coding-agent fleets

**Problem.** Claude Code, Codex, and Gemini/Antigravity CLIs change behaviour from week to week. This happens through server-side feature flags, A/B experiments, new hidden system-prompt sections, and forced self-updates. The changes silently override enterprise configuration (CLAUDE.md, delegation policy, thinking visibility, audit-readable transcripts). A 2,000-engineer rollout gets new agent behaviour without anyone approving it.

**Recent evidence:**
| Source | Date | Signal |
|---|---|---|
| github.com/anthropics/claude-code/issues/80988 | 2026-07-24 | A hidden `heron_brook` section injects "Do not call the AgentTool unless the user requested it" for Opus 5 only, "silently overriding user-configured delegation policy, with no opt-out" (91 reactions) |
| github.com/anthropics/claude-code/issues/62061 | 2026-05-24 | Server-side system-prompt injection via `tengu_heron_brook` feature flag (50) |
| github.com/anthropics/claude-code/issues/75607 | 2026-07-08 | A server-side experiment (`x-cc-atis`) removed thinking summaries, and the CLI self-updated despite `autoUpdates:false` (16) |
| github.com/anthropics/claude-code/issues/90450 | 2026-08-28 | Auto Mode's Bash-first instruction silently disables nested CLAUDE.md and path rules (48) |
| github.com/anthropics/claude-code/issues/87971 | 2026-08-19 | Auto mode makes Claude abuse bash for reads and writes (97) |
| github.com/anthropics/claude-code/issues/87575 | 2026-08-18 | The Auto mode prompt makes /rewind fail silently (42) |
| github.com/anthropics/claude-code/issues/95690 | 2026-09-20 | AGENTS.md support "a local feature locked behind a remote switch" (14) |
| github.com/openai/codex/issues/28058 | 2026-06-13 | Encrypted MultiAgentV2 messages remove the readable task audit trail (145) |
| github.com/openai/codex/issues/31814 | 2026-07-09 | GPT-5.6 Sol can't specify subagent models (206) |
| github.com/openai/codex/issues/41622, /39903 | Aug 2026 | Users ask for opt-outs from new default behaviours (99, 83) |
| github.com/google-gemini/gemini-cli/issues/27858 | 2026-06-12 | "Antigravity CLI is a massive downgrade ... bring back auto-edit and model routing" (20) |

**Who has the pain.** Developer-productivity and platform teams that roll coding agents out to 500+ engineers, especially in regulated industries that need change management on dev tooling.
**What they do today.** Pin versions (the pin leaks per #75607), read @ClaudeCodeLog and cchistory diffs by hand, set `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS`, use Codex `requirements.toml` feature pins, and file GitHub issues.
**Why current products fail.** The diff trackers are public and per-release. They don't see per-account server-side flags, and they don't test the effect on your repos. Gateways (TrueFoundry, Fiddler control plane, Portkey) log traffic but don't treat the harness prompt as a versioned artefact to gate.
**Why now.** Auto mode became the default (Aug 2026), there are fleets of background agents, and vendors ship weekly.
**Potential product.** A local proxy (via `*_BASE_URL`) captures the effective system prompt, tools, and flags for each request. It diffs them against the approved baseline and runs a 30-task canary on internal repos for any new version or flag. It promotes or blocks the change per group and keeps an auditor-ready change log.
**Time to value.** Two days. **Pilot.** One platform team, two vendors, 30 days. Success means at least one behaviour change caught and held before fleet rollout.
**WTP.** Low to moderate. It looks like a sprint-sized internal tool (round 8 lesson: "could the platform team build it in a sprint?" Yes: proxy + diff + canary).
**Expansion.** Policy-as-code across vendors, plus the evaluation dashboard for model and harness changes.
**Competition.** Free: cchistory, claude-code-changelog, Piebald claude-code-system-prompts (266 versions), phistory (multi-CLI). Native: Anthropic server-managed settings, Codex requirements.toml feature pins and governance dashboards, GitHub/Cursor team controls. Gateways: TrueFoundry, Fiddler control plane for coding agents, Portkey, Runlayer/Credal (round 9).
**Moat.** 10 customers: none. 100: a cross-fleet panel of flag and experiment exposure. 1,000: a de-facto change registry. A weak moat, and vendors can close it by publishing flag manifests.
**CTO test sentence.** "No change to how our coding agents behave reaches 2,000 engineers until it has passed our canary repos and someone has approved it."
**Kill test question.** Would a platform team pay rather than spend a sprint on proxy + diff + canary, and will Anthropic or OpenAI ship an "enterprise channel / frozen experiments" option first?

**Scores (1-10):**
| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market size | VC attractiveness | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 5 | 7 | 8 | 7 | 6 | 3 | 4 | 3 | 4 | 4 | **5.2** |

**Verdict.** The pain is real and dated, and vendors are structurally unwilling to freeze experiments. But it can be built in a sprint, free trackers cover the visibility half, and a vendor "stable channel" ends it. It fails at 5.2.

---

## Findings

1. **What the providers' channels mostly show.** Their own trackers are dominated by pain *about the providers themselves*: silent model, quota, and harness changes (clusters 1, 2, 5). The structural reason providers won't fix these is a conflict of interest, not technical difficulty. That is a better "won't fix" reason than earlier rounds found, but the buyer who suffers (the engineer) is not the buyer who pays.
2. **Cross-provider builder pain (clusters 3, 4, 6) is spread thin.** It shows up as dozens of low-reaction SDK bugs, which are absorbed by gateways (OpenRouter, Portkey, LiteLLM) and SDKs (Vercel AI SDK, BAML). This confirms the round 7 lesson: feature-sized, and fixed within weeks.
3. **Possible merger of A and B.** Combined as a "supply-chain integrity for AI" product (attestation for models + harness + reseller), the A/B wedge could serve vendor-risk and procurement buyers rather than engineers. That is the only version with a separate budget line. It needs proprietary validation: 5 calls to procurement or vendor-risk leads at enterprises spending $1M+ a year on models. Public sources cannot answer it.

No thesis clears the 8.5 bar. Best: A at 5.8.
