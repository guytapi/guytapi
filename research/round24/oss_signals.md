# Round 24: OSS adoption signals (Jun–Oct 2026)

Date: 2026-10-06. Method: explosive open-source adoption, then new developer behavior, then check for an uncommercialized enterprise layer.
Budget: 32 web searches + 2 GitHub repo searches (34 of 35 allowed).
**Data note:** WebFetch and star-history/indiestartup were blocked. The `mcp__github__search_repositories` tool **did work**. Star counts marked **[GH]** come straight from GitHub search on 2026-10-06 and are verified. Everything else comes from search-result snippets and is marked [snippet]. No numbers are invented. Funding marked "unverified" means one search found nothing, not that no funding exists.

**Bottom line: the two best candidates are both classified KILL. No A, no B.** The method is valid, but it shows structural conclusion #1 at an even faster pace. When a repo goes viral, a funded company (or a hyperscaler feature) usually exists **before or within ~4 weeks of** the star spike. Every enterprise layer we found (registry, governance, hosting, security) already has a funded owner.

---

## 1. Macro picture (verified)

- Repos created after 2026-06-01 with >15K stars: 22 **[GH]**. Repos created Mar–Jun 2026 with >25K stars: 54 **[GH]**.
- Sep 2026: the top 100 repos gained 1.15M stars. Among the top 50 by category: AI Agent 16, AI Skills 12, AI Coding Assistant 12 [snippet, gittrend.io/monthly/2026-09].
- The biggest single story is deepseek-ai/deepseek-harness: 244,306 stars, created 2026-08-13 **[GH]**. It reached 200K in 15 days [snippet, star-history.com blog]. It is a coding-agent harness, so excluded.
- Runa ROSS Q2/Q3 2026 was not found by search (Q1 2026 exists: runacap.com/ross-index/q1-2026/). No a16z/Accel OSS report for H2 2026 turned up.
- npm signal: Claude Code 22.6M/wk, Codex 16.1M/wk, opencode 2.5M, Pi 2.2M [snippet, amplifying.ai/coding-agents/npm]. This confirms the substrate. Every behavior below rides on coding-agent CLIs.

**Meta-insight:** in 2026, almost every explosive repo is either an *agent* or an *add-on to a coding agent* (skill, plugin, MCP, CLI). The new developer behavior is "the coding agent is a general-purpose work engine." Non-agent OSS breakouts are rare (gods-eye-view OSINT globe, vorssaint macOS utils, Recordly, colibri, VoiceStudio).

## 2. Behavior clusters and projects

| # | New behavior | Projects (verified stars [GH] unless noted) | Who's behind it | Commercialized already? | What enterprises would pay for | One-sentence thesis | Verdict |
|---|---|---|---|---|---|---|---|
| 1 | **Pre-indexing codebases into deterministic graphs for agents** (instead of grep/RAG) | Graphify-Labs/graphify 124,184 (created Apr 3); Egonex-AI/Understand-Anything 85,394; colbymchenry/codegraph 66,332 [snippet; solo author, 391 of ~430 commits]; TencentDB-Agent-Memory 27,729 | Graphify: YC S26 ($500K) with an "Enterprise" tier (merge-gate, graph-aware review, Jira) [snippet, dealroom]; codegraph is solo | **Yes.** Graphify Labs (YC), Potpie ($2.2M), Augment Context Engine, Blitzy ($200M, KG-based), Sourcegraph, DeepWiki. Enterprise DNA, Jul 2026: "now a crowded, fast-moving category" | Org-wide graph across 1,000s of repos, RBAC, freshness | "Shared, always-fresh system graph for every agent in the org" | KILL. Same as round-12 A2 plus a YC company |
| 2 | **Token/code-volume minimization as a dev habit** | DietrichGebert/ponytail 156,370 (created Jun 12; "54% less code"); JuliusBrussee/caveman 110,087 ("cuts 65% of tokens"); codegraph ("62% fewer tokens") | Solo creators | Indirectly: AI spend tooling (killed thesis B) and native caps | Spend reduction | "Agent efficiency layer" | KILL (thesis B, F1) |
| 3 | **Skills as the unit of shared knowledge** ("distill an employee") | mattpocock/skills ~242K [snippet]; garrytan/gstack 135,448; nuwa-skill 33,655 ("distill how anyone thinks"); book-to-skill 33,924; emilkowalski/skills 43,787; cloudflare/security-audit-skill 24,999 | Individuals plus big vendors | **Yes, heavily.** Tessl ($125M), JFrog Skills Registry, AWS Agent Registry (GA Aug 2026), Anthropic org skill management, Vercel skills.sh, iFlytek SkillHub (OSS), Snyk+Tessl. Security: 13–26% of skills are vulnerable, ~5% malicious; scanners bypassed >90% (CSA SkillCloak, Jul 2026) | Private registry, signing, scanning | "npm + Snyk for skills" | KILL (F1+F2) |
| 4 | **Coding agent as a content studio** (diagrams, video, design, 3D) | tt-a1i/archify 78,401 (+~45K in Sep; top gainer); cathrynlavery/diagram-design 43,597; nexu-io/open-design 99,637; heygen-com/hyperframes 57,558; calesthio/OpenMontage 64,454; browser-use/video-use 28,171; hypit-ai/hypit 19,617; img2threejs 17,569; VoltAgent/awesome-design-md 119,749; google-labs-code/design.md 28,256 | Mostly solo; HeyGen, Browser Use, Google are funded | Partly: HeyGen, Claude Design, Canva/Figma agents, Google DESIGN.md spec | Brand-safe asset generation and review | "Brand compliance gate for agent-made assets" | KILL (brand agent OS killed at scan; Canva/Figma/labs absorb) |
| 5 | **Making non-API software agent-operable through CLIs** | HKUDS/CLI-Anything 51,619 (academic, HKU) plus CLI-Hub; jackwener/OpenCLI 29,868 (uses the *logged-in browser*); iOfficeAI/OfficeCLI 31,611; googleworkspace/cli 31,262 | Academic or solo; Google official | **Yes.** Speakeasy and Stainless CLI generation (Anthropic bought Stainless May 2026); Minicor (YC, legacy desktop → API); Zatanna; Simular; **Amazon WorkSpaces for AI agents GA**; UiPath | Governed agent access to legacy and no-API apps | "Agent-native interface for every legacy app" | **Top-2 pick → KILL** (see §3B) |
| 6 | **Replacing LLM calls with single-pass "System-1" decision models** | NandhaKishorM/laya 31,087 (created **Sep 18**, so 31K in ~18 days) | "Convai Innovations" [snippet]; funding unverified (the CB Insights "Convai" is a different, virtual-characters company) | **Yes, by the category leader.** TypeSafe AI's Jev: $40M seed (DCVC, Sep 16, 2026), reportedly in talks at >$10B (unconfirmed), "~13% of one gateway's paid teams" [snippet]. 5–9 OSS alternatives already listed (pinggy, datacamp, scriptbyai) | Fine-tuning on own labels, VPC hosting, calibration monitoring | "Open-weight Jev: calibrated decision models trained on your labels, in your VPC" | **Top-2 pick → KILL** (see §3A) |
| 7 | **Frontier MoE models on hardware you already own** (experts streamed from SSD) | JustVugg/colibri 39,882 (created Jul 1; pure C; GLM-5.2 744B on 25GB RAM) | Solo, unfunded as far as found | No direct company. llama.cpp/Ollama/ktransformers are adjacent | Air-gapped batch inference without GPUs | "GPU-less frontier inference appliance" | KILL. 0.1–0.5 tok/s cold [snippet]; round-23 on-prem box kill; llama.cpp/Ollama absorb the trick |
| 8 | **Fully local voice cloning/dubbing** | debpalash/VoiceStudio 54,036 (#1 gainer Sep, +37,780); k2-fsa/OmniVoice (trending #5 Sep 11) | Solo plus academic | ElevenLabs and many others; consumer/prosumer | n/a | n/a | KILL (consumer; ElevenLabs) |
| 9 | **Mass stripping of AI watermarks** | guillaumemeyer/watermarks-remover 23,428 (created Aug 11; C2PA/SynthID) | Solo | Victim side: Truepic, Google, Adobe | Detection that survives stripping | "Watermark-independent provenance" | KILL (round-21 proof-of-capture kill; noted as a weak victim signal) |
| 10 | **Agent memory hubs** | MemPalace/mempalace 59,426; garrytan/gbrain 30,585; TencentDB-Agent-Memory | Mixed | Mem0, Letta, Zep, Tencent, all funded | — | — | KILL (generic agent infra, excluded) |

Excluded per brief (coding agents, harnesses, frameworks, wrappers): deepseek-harness, grok-build, claw-code, orca (YC), herdr, paperclip, openworker (Andrew Ng), yc-software/qm, opencodex/freellmapi/OmniRoute (LLM proxies), browser-use/jev-ultrafast, obscura.

---

## 3. Top 2 assessed in full finalist format

### 3A. Open self-hosted "System-1" decision models (laya cluster)

- **One-line problem:** software makes millions of small judgments (route, classify, approve, flag), and running each through an autoregressive LLM is slow, costly and returns unparseable text.
- **Why now:** TypeSafe Jev launched Sep 15–16, 2026 and laya went open-weight Sep 18. Both are non-autoregressive encoders that return typed, calibrated answers in ~33 ms. Jev claims 84–150x cheaper than Opus 5.5 [snippet, aimlapi]. This behavior barely existed 3 weeks ago.
- **Exact buyer:** Head of ML platform / AI platform lead. The CFO is a secondary sponsor through the inference bill.
- **Exact ICP:** companies running >50M LLM classification/routing/moderation calls a month: support platforms, marketplaces, trust & safety, fintech fraud ops, gateways.
- **Current workaround:** small LLMs (Haiku/Flash), fine-tuned BERT classifiers, OpenPipe-style distillation (acquired by CoreWeave), Predibase (Rubrik), Fastino.
- **Why incumbents cannot easily own it:** they can. TypeSafe ($40M) leads. Bedrock/Vertex/HF can host laya-class weights in a day. LLM labs can ship a "decision mode". OSS weights are already free.
- **30-day MVP:** a "labels → calibrated laya checkpoint" pipeline. Ingest a customer's LLM call logs, distill into a decision model, deploy into their VPC, and add drift and calibration monitoring.
- **Pilot design:** replay 1M historical routing/moderation calls. Pass = within 2 pts accuracy of the current LLM at ≥20x lower cost and <50 ms.
- **Pricing hypothesis:** $50–150K/yr platform plus per-checkpoint training.
- **Expansion path:** a decision-model registry, agent-loop guardrails ("is this shell command dangerous?"), the LLM-judge replacement market.
- **Moat:** weak. The labelled data belongs to the customer. Model quality comes down to who has more research money (TypeSafe), and calibration techniques (RLCD) are published.
- **Why $10B+:** if System-1 calls outnumber LLM calls 100:1 in agent stacks, the decision layer is very large. That outcome is TypeSafe's, though, not a newcomer's.
- **Direct competitors and adjacent threats:** TypeSafe Jev, laya's own authors, Fastino, Interfaze, OpenPipe/CoreWeave, Predibase/Rubrik, HF Inference Endpoints, Bedrock custom models, Arize (already benchmarking Jev).
- **Sentence to a CTO:** "We turn your 50M monthly LLM classification calls into a 33 ms in-VPC decision model at 1/50th the cost, with calibrated confidence you can threshold."
- **5 discovery questions:** (1) How many LLM calls/month return a label, score or yes/no? (2) What does that line cost today? (3) Have you tried Jev or fine-tuned BERT, and what stopped you? (4) Must the data stay in your VPC? (5) Who owns the routing/classification models?
- **Hard kill criteria:** TypeSafe ships open weights or VPC deployment; Bedrock or Vertex hosts laya-class models as a managed SKU; <3 of 10 ICP companies have >10M decision calls/month.
- **Scores:** Pain 6, Urgency 5, ROI clarity 8, Accessibility 6, Pilot speed 8, Market size 8, Expansion 7, Venture potential 7, Defensibility 3, Why now 9, Competition position 2. **Avg 6.3.**
- **Classification: KILL.** F2 visible-pain race (the leader raised $40M *two days before* the OSS breakout) plus F1 (clouds host open weights).
- **ACV / ARR path:** $80K ACV. $10M needs 125 customers, which is plausible. $100M needs 1,250 against TypeSafe and hyperscalers, which is implausible without a model-quality edge.
- **14-day test (if the founders still want a test):** get 5 ICP companies to share 100K anonymized classification calls. Pass = 3 show ≥20x cost reduction at ≤2-pt accuracy loss *and* say Jev is unacceptable (data residency). Expect it to fail on "why not Jev/Bedrock".

### 3B. Agent-native interfaces for software with no API (CLI-Anything / OpenCLI / OfficeCLI)

- **One-line problem:** agents can drive anything with an API or CLI, but most enterprise work still runs in GUIs, desktop ERP, Citrix apps and logged-in web portals.
- **Why now:** CLI-Anything (HKU academic lab) reached 51.6K stars with a CLI-Hub install registry. OpenCLI (29.9K) turns any site into a CLI using the *user's logged-in browser*. Developers increasingly prefer CLIs over MCP for agents.
- **Exact buyer:** VP Automation / CoE lead (the ex-RPA budget). The CIO is the economic buyer.
- **Exact ICP:** insurers, banks, healthcare providers and logistics firms with 10+ legacy line-of-business apps and an existing UiPath/Blue Prism estate.
- **Current workaround:** RPA bots, computer-use agents, WorkSpaces/Citrix plus vision agents, Minicor-style API wrappers.
- **Why incumbents cannot easily own it:** they already do. Amazon WorkSpaces for AI agents (GA), UiPath agentic automation, Speakeasy/Stainless (Anthropic) for API-backed CLIs, Minicor (YC) and Zatanna for no-API desktop apps, Simular for desktop agents.
- **30-day MVP:** auto-generate a deterministic, permissioned CLI for one legacy desktop app (e.g. SAP GUI transaction set), with an audit log and per-command approval scopes.
- **Pilot design:** take one RPA process that breaks ≥monthly, rebuild it as agent + generated CLI, and measure breakage and handle time over 2 weeks.
- **Pricing hypothesis:** $40–100K per app per year.
- **Expansion path:** a CLI registry across the estate, then governed agent access.
- **Moat:** a per-app connector library (UiPath already has one).
- **Why $10B+:** RPA replacement is a $10B+ budget, but UiPath, AWS and Microsoft own the buyer relationship.
- **Direct competitors and adjacent threats:** UiPath, Automation Anywhere, AWS WorkSpaces AI, Microsoft Copilot Studio computer use, Minicor, Zatanna, Simular, Composio/Arcade, Speakeasy, Stainless/Anthropic.
- **Sentence to a CTO:** "Every legacy app your RPA bots break on becomes a stable, permissioned command line your agents can call."
- **5 discovery questions:** (1) How many RPA bots break per month, and what does that cost? (2) Which apps have no API? (3) Have you tried WorkSpaces AI or UiPath agents? (4) Who approves agent access to the ERP? (5) What would you pay per app to never script against the GUI again?
- **Hard kill criteria:** the ICP says "UiPath/AWS covers it"; generated CLIs break as often as RPA selectors.
- **Scores:** Pain 7, Urgency 6, ROI clarity 7, Accessibility 5, Pilot speed 6, Market size 8, Expansion 6, Venture potential 6, Defensibility 3, Why now 6, Competition position 2. **Avg 5.6.**
- **Classification: KILL.** F1 (AWS WorkSpaces AI, UiPath) plus F2 (Minicor YC, Zatanna), and the "connector library" moat fails "build in a sprint."
- **ACV / ARR path:** $60K/app ACV. $10M = ~170 app-deployments. $100M requires displacing UiPath.
- **14-day test:** not recommended.

---

## 4. Lessons for the war room

1. **OSS stars are now a lagging signal too.** In both top picks, a funded leader existed *before* the OSS breakout (TypeSafe 2 days before laya; Speakeasy/Stainless/Minicor before CLI-Anything). Viral OSS increasingly comes *in reaction to* a funded launch: it is the "open alternative."
2. **The creator-unfunded condition holds only for add-ons to coding agents** (skills, graphs, diagram generators), and each of those is a feature of an agent platform (F5) or absorbed by registries (Tessl/JFrog/AWS).
3. **The one non-crowded weak signal:** watermark/provenance stripping at scale (23K stars in 8 weeks) and logged-in-browser agents (OpenCLI) both create *victim-side* problems (platforms relying on SynthID/C2PA; websites whose users let agents drive their sessions). That fits the failure taxonomy's under-explored "victims of agent behavior" area. Worth one scan in round 25, though proof-of-capture (round 21) and agent-traffic trust (round 12 Z) already cover parts of it.

## Sources (all from search results; [GH] = GitHub search via MCP, 2026-10-06)
- Repos: github.com/NandhaKishorM/laya, github.com/tt-a1i/archify, github.com/HKUDS/CLI-Anything, github.com/jackwener/OpenCLI, github.com/iOfficeAI/OfficeCLI, github.com/JustVugg/colibri, github.com/Graphify-Labs/graphify, github.com/colbymchenry/codegraph, github.com/DietrichGebert/ponytail, github.com/JuliusBrussee/caveman, github.com/debpalash/VoiceStudio, github.com/guillaumemeyer/watermarks-remover, github.com/deepseek-ai/deepseek-harness
- https://gittrend.io/monthly/2026-09 ; https://www.star-history.com/blog/output/ (Sep 2026 monthly) ; https://www.analyticsvidhya.com/blog/2026/09/top-github-repositories-august-2026/ ; https://runacap.com/ross-index/q1-2026/
- https://dealroom.co/news/151032-typesafe-exits-stealth-with-40m-seed-to-build-ai-for-software-not-people/ ; https://aimlapi.com/blog/what-is-jev ; https://runtimewire.com/article/typesafe-investors-discuss-a-higher-valuation-after-jev-reaches-nearly-13-of-one ; https://pinggy.io/blog/best_open_source_jev_alternatives_self_hosted_decision_models/ ; https://andrew.ooo/posts/laya-review-open-weight-jev-alternative-system-1-decision-model/
- https://app.dealroom.co/companies/graphify_labs_yc_s26 ; https://enterprisedna.co/resources/ai-pulse/ai-pulse-2026-07-23-codebase-knowledge-graph-for-ai-agents-is-now-a-crowded-fast ; https://www.sovereignmagazine.com/article/potpie-ai-raises-2-2-million-to-give-ai-agents-codebase-context
- https://labs.cloudsecurityalliance.org/research/csa-research-note-skillcloak-agent-skill-evasion-20260706-cs/ ; https://jfrog.com/ai-catalog/skills-registry/ ; https://aws.amazon.com/about-aws/whats-new/2026/08/aws-agent-registry-generally-available
- https://www.speakeasy.com/product/cli-generation ; https://www.anthropic.com/news/anthropic-acquires-stainless ; https://ycombinator.com/companies/minicor ; https://www.citi.com/ventures/perspectives/opinion/computer-use-agents-startups.html
- https://pasqualepillitteri.it/en/news/7923/colibri-glm-5-2-744b-25gb-ram-en ; https://amplifying.ai/coding-agents/npm
