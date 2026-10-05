# Thesis I: AI supply integrity ("we verify every call is the model you pay for")

Date: 2026-10-05. Method: round7/METHOD.md template, plus the original bar, simulated buyers, VC committee and red team (same format as round9/H). Starting point: round10/provider_forums.md cluster 1 (silent substitution) and cluster 2 (harness drift), thesis A there scored 5.8.
Budget: 40 web searches used (the maximum). WebFetch and Reddit were blocked, so page contents come from search snippets. Every URL below appeared in a search result. Claims I could not confirm are marked [unverified]. Numbers marked [estimate] are mine.

**One-line verdict: KILL (avg 4.6 on METHOD, 4.4 on the original bar).** Silent changes do happen and get confirmed. But the evidence splits three ways, and none of the three is a $1M+ enterprise buying a frontier API:
- **Consumer subscriptions.** The ChatGPT router, Claude Code plans and Perplexity. The remedy there is class actions, not procurement.
- **Open-weight resellers.** Here a neutral index already exists: the Artificial Analysis Endpoint Accuracy Index (launched Aug 4 2026). OpenRouter Auto Exacto and Moonshot's own Kimi Vendor Verifier cover the same ground.
- **Grey-market "shadow APIs".** The buyers are researchers and hobbyists, not enterprises.

On the enterprise path (pinned snapshots via the provider, Azure or Bedrock), confirmed incidents are rare. They are mostly *bugs* the provider finds and discloses within weeks, not covert swaps.

Detection is also weakest exactly where it matters:
- Closed frontier APIs expose few or no logprobs, which removes the cheapest statistical tests.
- Text classifiers cannot tell a model from its quantized version (about 50% accuracy, i.e. chance).
- A malicious provider can fine-tune a cheap model to defeat black-box fingerprints (GhostPrint).
- Embedded SaaS AI (M365 Copilot) routes between models *by design*, so there is no contractual "model behind the name" to attest.

Long term, attestation is going native through TEEs: Anthropic's confidential-inference research, Google Private AI Compute, Azure confidential inferencing, Tinfoil, Phala, and the Token-DiFR verification method.

The "neutral ratings agency of AI" seat is also already contested by funded players: Artificial Analysis, Vals AI (a16z, $40M, Aug 2026) and LMArena ($1.7B).

---

## Problem
Providers and resellers can change what serves a model name without a version bump. Examples are quantization, a smaller reasoning budget or context, routing to a cheaper sibling, and system-prompt or harness edits. Customers find out from their own users. No independent party certifies account-level supply.

## Recent evidence: how often do silent changes happen, and get confirmed?

**Confirmed by the provider (postmortems):**
| Event | What was confirmed | Who was affected | Source |
|---|---|---|---|
| Anthropic, Aug-Sep 2025 | Three infra bugs: context-window routing error (up to 16% of Sonnet 4 requests on Aug 31), TPU output corruption, approximate top-k XLA miscompilation. Fixed by Sep 16; Anthropic added continuous production quality monitoring | API and apps (the postmortem says it also hit third-party platforms [unverified detail]) | anthropic.com/engineering/a-postmortem-of-three-recent-issues; infoq.com/news/2025/10/anthropic-infrastructure-bugs; implicator.ai |
| OpenAI, Apr 25-28 2025 | GPT-4o sycophancy update rolled back; "Expanding on what we missed" (May 2) | ChatGPT (consumer) | openai.com/index/expanding-on-sycophancy; techcrunch.com 2025/04/29 |
| Anthropic, Mar-Apr 2026 | Claude Code default reasoning effort cut from high to medium (Mar 4 - Apr 7); thinking-clearing bug (Mar 26 - Apr 10); verbosity system prompt (Apr 16-20). Postmortem Apr 23; limits reset | Claude Code harness and subscriptions (reports suggest the API was not affected [unverified]) | infoq.com/news/2026/05/anthropic-claude-code-postmortem; tessl.io blog 28 Apr 2026; mcp.directory/blog/why-claude-felt-dumber-2026-postmortem |
| AWS Bedrock gpt-oss-120b, Aug 2025 | Artificial Analysis measured Bedrock at -6.3 pts GPQA, about -10% AIME25 and -4.9% IFBench versus leading providers for the *same open model* | Hyperscaler serving difference (open weights) | feeds.simonwillison.net/2025/Aug/15/inconsistent-performance; artificialanalysis.ai/models/gpt-oss-120b/providers |

**Measured independently:**
- **Stanford Model Equality Testing (ICLR 2025).** 11 of 31 commercial endpoints for four Llama models served different distributions from Meta's reference weights. Source: arxiv.org/abs/2410.20247.
- **Artificial Analysis Endpoint Accuracy Index (Aug 4 2026).** GLM-5.2 scored 52% on one provider and 100% on others, with a 5.2x price spread. gpt-oss-120b tool calling scored 22% on some endpoints versus 37% on the reference. The causes were quantization, output-token caps and bugs. Sources: artificialanalysis.ai/articles/endpoint-accuracy-index; alphasignal.ai.
- **Moonshot Kimi Vendor Verifier.** Moonshot found a "stark contrast" between third-party and official API results, "widespread" across providers. Moonshot now ships the verifier itself. Source: kimi.com/en/blog/kimi-vendor-verifier.
- **"Real Money, Fake Models" (shadow APIs).** 45.83% of 24 grey-market endpoints failed fingerprint verification, with up to 47% performance divergence. 17 shadow APIs are used in 187 papers. Source: arxiv.org/pdf/2603.01919.
- **OpenRouter.** It has seen *no measurable tool-call impact from quantization alone*; tool-call parsers are the usual culprit. Source: openrouter.ai/blog/announcements/provider-variance-introducing-exacto.
- **2026 forum and issue evidence** (round10 file): Codex #30364 (reasoning-token clustering, 428 reactions), #32806 (context cut), Gemini CLI #28859 (flash alias served by 3.5-flash), OpenAI forum "silent downgrade to mini" (resolved_model_slug visible), Cursor billing the selected model while serving a fallback.

**Lawsuits (enterprise or consumer?):**
- *Pascual v. Anthropic* (N.D. Cal., filed Jul 24 2026): backend changes degraded Claude Code and drained limits from Mar 4 to May 6; no refunds. Sources: news.bloomberglaw.com; topclassactions.com Aug 5 2026; storage.courtlistener.com (gov.uscourts.cand.474951).
- *Kahn v. Anthropic* (Jun 15 2026): Max plan usage limits. Source: letsdatascience.com.
- *Perplexity Pro*: Deep Research cut back and queries "rerouted through less capable models without adequate disclosure". Source: dailyjournal.com/article/392243.
- An antitrust class action alleges labs agreed to slow model improvement. Source: openclassactions.com [unverified merit].
- **All of these are consumer cases.** I found no enterprise SLA-credit claim or B2B dispute over model quality or substitution. The lack of a public B2B dispute is itself evidence.

**Contracts:**
- Advisory content recommends model-pinning clauses with a named model ID and version plus a notice period. Some templates ask for "60 days prior written notice of any material change to a model version, prompt scaffolding, or system prompt". A GSA 2026 proposed clause requires 30/15 days of concurrent access to successor models [unverified primary]. Sources: tianpan.co/blog/2026-05-02-ai-procurement-clauses-lawyers-havent-learned-to-ask-for; tianpan.co/blog/2026-07-02-the-llm-contract-clauses-that-actually-matter; redresscompliance.com.
- OpenAI's own docs treat behavioural differences between snapshots as "backwards-compatible".
- **The clauses are about deprecation and notice, not attestation of each call.** Enforcement would rely on the buyer's own evals. No source shows a buyer paying a third party to enforce these clauses.

**Enterprise concern:**
- Generic "drift" statistics circulate, such as "91% of production LLMs drift within 90 days". They come from vendor blogs with weak methodology [unverified].
- Microsoft 365 Copilot routes per request between frontier and standard models. "CIOs mostly cannot audit it" (copilotconsulting.com). This is a real governance gap, but routing is the product, not a breach.

**Assessment.** The pain is real, recurring and confirmed. But where money is lost:
- **Consumer**: the remedy is lawsuits and refunds.
- **Open-weight resellers**: the remedy is free indices and routing.
- **Grey market**: the buyers won't pay.
- **Enterprise frontier API**: incidents are mostly provider bugs, disclosed within weeks, and costs are absorbed as quality noise rather than claimed.

## Who has the pain
- Engineers on coding-agent subscriptions: loud, but low willingness to pay.
- Builders on open-weight resellers: served by Exacto and AA EAI.
- Researchers on shadow APIs.
- Enterprise AI platform teams: real, but intermittent and low-severity on pinned snapshots. They already run their own eval suites (Braintrust, LangSmith, Arize).

## What they do today
- Pin snapshots.
- Run their own regression evals in CI and on production samples.
- Read public watchdogs: Marginlab, AIStupidLevel, IsItNerfed, AA.
- Use OpenRouter `:exacto` or provider allowlists.
- Use provider-native verifiers (Kimi KVV).
- Wait for the postmortem.

## Why current products fail (the honest gap)
- Public watchdogs test default paths, not *your* account, region or tier.
- Eval tools can't separate "my prompt broke" from "they changed upstream" unless you add fixed canaries. That is a one-sprint add, and stillsane already does it for free.
- No one produces signed, contract-grade evidence. But no buyer was found who asks for it.

## Why now (claimed versus evidenced)
- **AI spend and GPU pressure**: true.
- **Confirmed silent changes**: true, but on consumer and harness surfaces.
- **EU AI Act GPAI**: the obligations cover provider documentation and training-data transparency, not per-call serving attestation. No search evidence ties GPAI to customer-side verification [unverified; treated as weak].
- **Model-version clauses**: emerging, notice-based.
- **Counter-trend**: TEE-based attestation and provider changelogs are making the problem native.

## Technical feasibility
| Method | Accuracy / cost | Works on closed frontier APIs? | Works on embedded SaaS? |
|---|---|---|---|
| Model Equality Testing (MMD two-sample, Stanford) | Good with about 10 samples × many prompts; detects quantization and fine-tunes on open models | Partly (text only; needs a reference distribution, which you only get from the same API historically) | No |
| LLMmap (USENIX Sec '25) | 95%+ over 42 model versions in 8 queries | Identifies the *family or version*, not quantization or budget | Partly (identification through an app UI) |
| Idiosyncrasies (ICML '25) | 97.1% five-way, across vendors | Separates vendors, not variants | Partly |
| Logprob tracking (ICLR 2026, arxiv 2512.03816) | Detects one fine-tuning step; about 1,000x cheaper | **Only where logprobs are exposed.** Anthropic doesn't expose them; OpenAI reasoning models restrict them [partly unverified] | No |
| McNemar degradation test (Amazon Science, ICLR 2026) | Controlled false positives on task accuracy | Yes (task-level), but this is just an eval | Weak |
| Text classifier for full vs quantized (arxiv 2504.04715, NeurIPS 2025) | **About 50%, i.e. chance** | No | No |
| Token-DiFR / Activation-DiFR (MATS, ICML 2026) | AUC >0.999 for 4-bit quantization in 300 tokens | **Needs seed sync and a reference implementation, so the provider must cooperate** | No |
| Fingerprint spoofing (GhostPrint, arxiv 2606.16100) | A weak model fine-tuned to pass fingerprints at low cost | Shows black-box attestation is defeatable by an adversary | n/a |
| TEE attestation (Anthropic/Pattern Labs, Google PAC, Azure confidential inferencing, Tinfoil, Phala) | Cryptographic model hash plus code measurement; modest overhead | Only if the provider deploys it, and then it is native, not third-party | Only if the SaaS deploys it |

**Verdict on feasibility:**
- Behavioural drift detection (black-box task canaries plus CUSUM) is easy and commoditised: AIStupidLevel, stillsane, llm-fingerprint-detector, apimaster.ai, IRIS, AgentProv and many arXiv methods, all free.
- Proof of substitution or quantization on closed frontier APIs is weak without provider cooperation. arxiv 2504.04715 concludes software-only methods are "fundamentally unreliable" and recommends TEEs.
- Reasoning-budget and context probes do work: counting reasoning tokens, needle-at-N context tests. Users already find these unaided (Codex #30364, #32806).
- Embedded SaaS: the contract doesn't name a model, routing is intended, and any change in the vendor's harness confounds the measurement. **You can't attest what was never promised.**

## Competition (searched hard)
- **Neutral index or monitoring:**
  - Artificial Analysis: AI Grant, Friedman/Gross seed; 500+ models, 100+ providers, 1,000+ endpoints; *Endpoint Accuracy Index* since Aug 2026; enterprise subscription plus private benchmarking; calls itself "the independent ratings agency of AI".
  - Vals AI: $40M Series A, a16z, Aug 13 2026, about $400M valuation [valuation via pulse2, unverified]; revenue 8x.
  - LMArena: $150M Series A, $1.7B valuation, Jan 2026; customers include OpenAI, Google, xAI and Microsoft.
  - Marginlab: daily SWE-Bench-Pro tracker for Claude Code; independent.
  - AIStupidLevel: OSS, 21 models, CUSUM.
  - IsItNerfed: 2025, Florida; vibe plus metrics checks.
  - Epoch: not searched.
- **Reseller-side:**
  - OpenRouter Exacto and Auto Exacto: on by default; signals from real traffic.
  - Kimi Vendor Verifier: the model lab polices its own resellers.
  - apimaster.ai and beatapi.io "check which model your API runs".
  - ToseaAI llm-fingerprint-detector (OSS).
- **Eval and observability, one feature away:**
  - Braintrust, LangSmith, Arize, Galileo (Cisco), Patronus, Openlayer (in Gartner's 2026 Market Guide for AI Evaluation and Observability).
  - Datadog LLM Observability.
  - I found no specific "upstream changed" alert feature [gap is real, but feature-sized].
- **AI-BOM and provenance:**
  - Cisco Model Provenance Kit: weight-level fingerprint DB, 150 base models.
  - Manifest Cyber ("AI BOMs still largely aspirational").
  - Foley guidance on AI-BOM contracting (Jul 2026).
- **Verifiable inference:**
  - Tinfoil (YC X25): NVIDIA CC enclaves, verifiable.
  - Phala: GPU TEE, 3B+ tokens/day.
  - Atoma, Rena Labs ($3.3M pre-seed), NEAR AI Cloud, io.net confidential inference.
  - zkML (EZKL, Modulus, Inference Labs): not searched; impractical at frontier scale [judgment].

## Will providers ship attestation themselves?
**Partly, and it is already happening on the privacy side:**
- Anthropic published confidential inference via trusted VMs with Pattern Labs. It explicitly calls this early research.
- Google shipped Private AI Compute (Nov 2025): TPU plus Titanium Intelligence Enclaves, remote attestation, NCC Group review.
- Azure has confidential inferencing (Whisper preview; HPKE plus attested KMS).
- Moonshot ships a vendor verifier for its own model.
- OpenRouter scores providers itself.

**Frontier labs have little incentive to attest against their own compute rationing.** That is the bull case for a third party. But the evidence shows the remedy flows through lawsuits, postmortems and refunds, not paid attestation. Once TEEs ship for privacy, a model-hash measurement comes almost for free, and that kills third-party "proof" for open and enterprise deployments.

## Potential product
Shadow canary probes from the customer's own keys and accounts across providers, resellers and regions. Context and reasoning-budget probes. Fingerprint plus task-canary change-point detection. A signed evidence log, contract-clause mapping, a vendor-risk report and a cross-customer change feed.

## Time to value
One day (API keys).

## Pilot (14-30 days)
Shadow probes on 3 provider accounts, 2 resellers and 1 embedded SaaS. **The problem:** on pinned enterprise snapshots, the base rate of a *material* undisclosed change within 30 days is low [estimate: <30% chance in any given month on direct/Azure/Bedrock frontier endpoints, judging by about 2-4 confirmed API-level incidents a year across labs]. A pilot whose success criterion is "detect at least one material change" will often show nothing. The likely pilot output is "your vendors were fine", which is a weak renewal story. On open-weight resellers the pilot *will* find variance, but AA EAI and Exacto already show it for free.

## Willingness to pay
- No enterprise SLA-credit or B2B dispute found.
- Contract clauses are notice-based.
- Procurement and vendor-risk teams buy questionnaires and attestations (SOC 2, ISO 42001), not continuous black-box tests.
- Willingness to pay is demonstrated for *independent benchmarking* (Vals, AA, LMArena), and those players already own it.
- Plausible ACV $15-50K [estimate]. Budget owner unclear: the AI platform team builds it, and procurement has no tool budget for it.

## Expansion
Routing optimisation; insurer and auditor feed; plaintiff-side forensic evidence (consumer class actions, a niche); reseller certification (but Moonshot and OpenRouter do it themselves).

## Moat
- **10 customers:** none. Probes are reproducible from papers and OSS.
- **100 customers:** a cross-customer change feed. But a public watchdog already sees the same global changes. Account-specific changes, such as A/B cohorts or regional routing, are the only unique signal, and they are rare.
- **1,000 customers:** a historical index. AA, Vals and LMArena are already building this, with 10-100x the capital.

## CTO test sentence
"We'll tell you, with signed evidence, the day your vendor changes the model behind your contract." Likely CTO reply: "Our eval suite and pinned snapshots already catch what matters, and Anthropic or OpenAI publish a postmortem within weeks."

## Kill test question
Can you find 5 enterprises that have *claimed or wanted to claim* a credit or contract remedy for an undisclosed model change in the last 12 months? Desk research found zero B2B cases and several consumer class actions.

## Scores (METHOD, 1-10)
| Pain | Urgency | Timing | Speed to pilot | Integration | Reach | WTP | Competition | Moat | Market size | VC attractiveness | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 4 | 6 | 6 | 8 | 4 | 3 | 3 | 3 | 4 | 4 | **4.6** |

Notes on the scores:
- Speed to pilot was cut to 6 because the pilot's success depends on an event that may not occur.
- Competition is 3: the neutral index is owned by AA, Vals and LMArena, and detection is free OSS.

## Scores: original bar (8.5 avg needed, none below 7)
| Pain | Urgency | ROI clarity | Customer accessibility | Pilot speed | Market size | Expansion | Venture potential | Defensibility | Why now | Competition position |
|---|---|---|---|---|---|---|---|---|---|---|
| 6 | 4 | 3 | 4 | 6 | 4 | 5 | 4 | 3 | 6 | 3 |

**Average: 4.4.** All eleven categories are below 7.

## Buyer, number of buyers, ACV
- **Buyer:** Head of AI Platform (builds it with evals), CTO (relies on the vendor), and procurement/vendor risk (no tooling budget; buys attestations, not tests).
- **Number of buyers:** companies spending $1M+/yr on model APIs, perhaps 2,000-5,000 globally in 2026 [estimate]. Of those, ones with multi-vendor or reseller exposure that would buy a separate attestation line are perhaps 10-20% [estimate].
- **ACV:** $15-50K [estimate].

## Market math
- **$10M ARR:** about 300 customers at $33K. Plausible only by bundling with evals or a gateway, which puts it in the generic-evals category (killed).
- **$50M ARR:** about 1,000 at $50K. Requires procurement adoption as a compliance standard. No evidence of that pull.
- **$100M ARR:** requires becoming the "Moody's/UL of AI supply". AA ("independent ratings agency of AI"), Vals ($400M valuation) and LMArena ($1.7B) are already competing for that seat with labs as customers.
- **$10B?** Ratings agencies win through regulatory designation (NRSRO) or issuer-pays models. Neither exists for AI serving. TEEs make the "proof" a hardware feature, not a ratings product.

## 5 simulated buyers
1. **Head of AI Platform, fintech ($4M/yr OpenAI via Azure, pinned snapshots): NO.** "We pin snapshots and run Braintrust evals nightly on our real tasks. That's our canary. In 18 months the only drift we hit was our own prompt changes."
2. **CTO, legal-AI startup ($2M/yr, Anthropic direct plus Bedrock failover): MAYBE.** "The Aug 2025 bug hurt us for two weeks. A cross-provider early-warning feed is worth $10-20K. Not a contract-evidence product, though. Anthropic refunded nothing and we didn't ask."
3. **VP Procurement, Fortune 500 (Copilot, Agentforce, Azure OpenAI commit): NO.** "Our contracts say 'service', not 'model X'. Microsoft routes by design. I want ISO 42001 and SOC 2 reports, not a startup's probe statistics that Microsoft will dispute."
4. **Coding-agent platform (Cursor-like reseller, buys from 4 labs and 6 open-weight hosts): MAYBE/YES at low ACV.** "We already use AA's Endpoint Accuracy data and our own evals for hosts. An account-level feed is nice. $20-30K, and we'd rather build it."
5. **Vendor-risk lead, EU bank (AI Act readiness): MAYBE.** "An 'AI SBOM / provenance' report fits our third-party risk programme, but we'd get it from our GRC vendor (OneTrust/ServiceNow) or the provider's documentation, not continuous probes."

**Tally: 0 YES, 3 MAYBE, 2 NO.**

## VC committee view
- **Bull:** a structural conflict of interest (providers grade themselves), confirmed incidents at every lab, spend heading to the hundreds of billions, a "Moody's for AI supply" narrative, consumer class actions showing harm, and academic work showing 11/31 and 45.8% failure rates.
- **Bear (wins):**
  1. The seat is taken. Artificial Analysis launched the Endpoint Accuracy Index (Aug 2026), Vals raised $40M from a16z, LMArena is at $1.7B, and labs pay them.
  2. Detection is commoditised (OSS plus a dozen arXiv methods) and defeatable by adversaries (GhostPrint). The only cryptographic version needs TEEs the providers control.
  3. The money-losing incidents are consumer or open-weight, and enterprise buyers on pinned snapshots shrug.
  4. The product collapses into "evals with an upstream lens", which is killed in STATUS.md.

**Pass.**

## Red team (the best case for keeping it alive)
- **Plaintiff and forensic niche.** Consumer class actions (Pascual and Kahn v. Anthropic, Perplexity) need *timestamped longitudinal evidence* of degradation. A historical, account-level probe archive is expert-witness material. It is small, but it has real WTP per case ($50-250K engagements) [estimate]. This is a services business, not a venture one.
- **Open-weight supply certification for labs.** Moonshot built KVV because resellers damage its brand. Other open-weight labs (Zhipu/GLM, DeepSeek, Qwen, Mistral, OpenAI gpt-oss) might pay a neutral certifier rather than build one. But AA already does this publicly, and labs prefer to control it.
- **Account-specific A/B and regional routing** (Gemini CLI alias substitution, the OpenAI "silent downgrade to mini" threads) is the one signal public watchdogs can't see. If providers increasingly segment by tier or capacity in 2027, an account-level panel gains value.
- **TEE integrator.** As providers expose attestation reports (Google PAC, Azure CC, future Anthropic confidential inference), someone must verify them continuously across vendors and map them to vendor-risk controls. That is a real but thin "attestation verifier" layer, likely absorbed by GRC or gateways.

None of these reaches 8.5. The forensic niche is the most honest residual.

## Kill signals (observed)
1. A neutral public index exists and is funded: AA Endpoint Accuracy Index (Aug 4 2026), Vals ($40M, a16z), LMArena ($1.7B).
2. Resellers and labs police themselves: OpenRouter Auto Exacto on by default; Moonshot KVV.
3. No B2B dispute or SLA credit found. The remedies are consumer class actions and provider postmortems.
4. Software-only proof is weak on closed APIs (chance-level quantization detection, no logprobs, spoofable fingerprints). Strong proof requires provider cooperation (DiFR, TEEs).
5. Embedded SaaS routes by design, so there is no promise to attest.
6. Detection code is free and abundant (stillsane, llm-fingerprint-detector, AIStupidLevel, arXiv IRIS/AgentProv/MET).
7. The pilot depends on a rare event, and a likely "nothing found" result undermines renewal.
8. It fails the round 8 test: a platform team can add fixed upstream canaries to its existing eval tool in a sprint.

## VERDICT
**KILL.** The pain is real, but it is spread across buyers who won't pay (consumers, researchers) or are already served (open-weight via AA, Exacto and KVV). Where the money sits (enterprise frontier APIs), incidents are infrequent provider bugs disclosed within weeks, and buyers rely on evals and pinned snapshots. The "Moody's for AI" seat is contested by three funded players. Hardware attestation will make "proof" a provider feature. The best residual, forensic evidence for consumer class actions, is a services niche.
**Avg 4.6 (METHOD) / 4.4 (original bar).** Down from 5.8 for thesis A in provider_forums.md, after the competition and evidence of who actually pays.

## Sources (all appeared in search results)
- anthropic.com/engineering/a-postmortem-of-three-recent-issues ; infoq.com/news/2025/10/anthropic-infrastructure-bugs ; implicator.ai/anthropics-postmortem-three-bugs-pushed-claude-degradation-to-16-at-peak
- openai.com/index/expanding-on-sycophancy ; techcrunch.com/2025/04/29/openai-explains-why-chatgpt-became-too-sycophantic
- infoq.com/news/2026/05/anthropic-claude-code-postmortem ; tessl.io/blog/anthropic-postmortem-shows-how-small-changes-compounded-into-claude-code-failure ; mcp.directory/blog/why-claude-felt-dumber-2026-postmortem
- arxiv.org/abs/2410.20247 (Model Equality Testing) ; arxiv.org/pdf/2504.04715 (Auditing Model Substitution) ; arxiv.org/html/2407.15847v3 (LLMmap) ; arxiv.org/pdf/2502.12150 (Idiosyncrasies) ; arxiv.org/html/2512.03816v1 (Logprob tracking) ; arxiv.org/html/2602.10144 (McNemar, Amazon) ; arxiv.org/html/2511.20621v1 (DiFR) ; arxiv.org/pdf/2606.16100 (GhostPrint spoofing) ; arxiv.org/pdf/2603.01919 (shadow APIs) ; arxiv.org/pdf/2607.20860 (IRIS) ; arxiv.org/pdf/2609.00052 (AgentProv)
- openrouter.ai/blog/announcements/provider-variance-introducing-exacto ; openrouter.ai/blog/announcements/auto-exacto
- kimi.com/en/blog/kimi-vendor-verifier
- artificialanalysis.ai/articles/endpoint-accuracy-index ; artificialanalysis.ai/methodology/endpoint-accuracy-index ; artificialanalysis.ai/models/gpt-oss-120b/providers ; feeds.simonwillison.net/2025/Aug/15/inconsistent-performance ; artificialanalysis.ai/pricing ; latent.space/p/artificialanalysis
- marginlab.ai/trackers/claude-code ; aistupidlevel.info/faq ; everydev.ai/developers/isitnerfed ; github.com/msanket9/stillsane ; github.com/ToseaAI/llm-fingerprint-detector ; apimaster.ai/ai-api-model-tester
- news.bloomberglaw.com/ip-law/anthropic-hit-with-consumer-deception-suit-over-reduced-service ; topclassactions.com (Aug 5 2026) ; letsdatascience.com/news/anthropic-faces-claude-max-usage-limits-lawsuit-213d8c21 ; dailyjournal.com/article/392243-perplexity-sued-over-alleged-cuts-to-premium-ai-subscription-benefits ; openclassactions.com (antitrust)
- tianpan.co/blog/2026-05-02-ai-procurement-clauses-lawyers-havent-learned-to-ask-for ; tianpan.co/blog/2026-07-02-the-llm-contract-clauses-that-actually-matter ; redresscompliance.com/cio-playbook-negotiating-openai-contracts-for-generative-ai/
- anthropic.com/research/confidential-inference-trusted-vms ; thehackernews.com/2025/11/google-launches-private-ai-compute.html ; ycombinator.com/companies/tinfoil ; docs.phala.network/llm-in-gpu-tee/inference-api ; theblock.co/post/333676 (Rena Labs)
- copilotconsulting.com/insights/copilot-model-routing-frontier-vs-standard-answers-enterprise ; esecurityplanet.com (Cisco Model Provenance Kit) ; darkreading.com/cyber-risk/is-2026-year-ai-bills-of-materials-get-real
- pulse2.com (Vals AI $40M at $400M) ; mexicobusiness.news (LMArena $1.7B)
