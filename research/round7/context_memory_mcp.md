# Round 7 slice: Context infrastructure, agent memory, MCP and tool execution

Researcher run: 2026-10-05. 37 web searches. Reddit is blocked to the search tool, so evidence comes from GitHub issues, HN threads, vendor and engineering blogs, and arXiv. WebFetch is blocked, so **exact posting dates could not be checked for most items**. Where I give a date, it comes from the search snippet. HN item IDs above roughly 49.4M (for example "Ask HN: Who is using MCP in production?", item 49548600) and very high GitHub issue numbers (for example claude-code #85236, openclaw #139477, codex #48507) suggest Aug–Oct 2026, but I did not confirm this. All URLs below appeared in search results. No quotes were invented. Where text is paraphrased from a snippet, I say so.

## Bottom line (read first)

**No problem in this slice is strong enough to go deep on.** The slice follows the pattern already noted in STATUS.md: the pains with the most evidence are either (a) bugs that the platform vendors (Anthropic, OpenAI, GitHub, Google) are fixing in their own clients, or (b) categories that already have funded vendors (Tessl $125M, Unblocked, Glean, Guru, Mem0/Zep/Letta/Supermemory, Composio/Arcade/Nango/Auth0 Token Vault, Manufact (YC), MCPJam, Scalekit/Stytch/WorkOS, Runlayer and others). The best near-miss is #1, MCP credential lifecycle for unattended or concurrent agents. It has by far the most independent signals (~20), but it fails the competition test and the "is this a company or a client patch" test.

---

## Ranked candidates

### 1. Credentials break when agents run unattended or in parallel (MCP OAuth refresh and rotation failures)

- **Problem:** OAuth-backed MCP connectors work at install time and then die, often after about 1 hour, when agents run in the background, in several sessions at once, or across processes. The causes are: refresh tokens never issued (missing `offline_access`), refresh tokens wiped on write-back, refresh sent to the wrong token endpoint, and concurrent refreshes against providers with single-use rotating refresh tokens (Stripe, Supabase, GitLab, Atlassian) that revoke the whole token family. The visible symptom is "re-login every hour" or a connector that is silently disabled.
- **Recent evidence (~20 independent signals, all GitHub issues or PRs):**
  - openai/codex #48507: concurrent processes race refresh-token rotation and the next startup hits `invalid_grant` (https://github.com/openai/codex/issues/48507)
  - anthropics/claude-code #85236: per-process refresh lock lets concurrent sessions race, rotation-strict servers revoke the token family (https://github.com/anthropics/claude-code/issues/85236)
  - github/copilot-cli #3456: concurrent refresh requests kill the OAuth chain (https://github.com/github/copilot-cli/issues/3456), plus #4842 and #2779
  - anomalyco/opencode #49439; vercel/ai #20674; can1357/oh-my-pi #5081; PrefectHQ/fastmcp #4901 (OAuthProxy rotates with no grace period); kentcdodds/kody PR #2233; gleanwork/agent-plugins PR #4 (Glean fixing cross-process rotation in its own plugin)
  - NousResearch/hermes-agent #62333 ("MCP servers die ~1h after login"); OpenHands software-agent-sdk PR #5306 (refresh hits the wrong endpoint, refreshed state not persisted in hosted deployments)
  - anthropics/claude-ai-mcp #253 (managed connector tokens expire about every 24h, `offline_access` missing) and #247 (Claude Enterprise custom connector not refreshing); claude-code #25245, #29257 (Slack MCP 1h expiry, no refresh token), #44652 (step-up auth)
  - openai/codex #14144, #24906 (Google-backed servers never get a refresh token), #38198 (connector permanently disabled after a failed refresh); google-gemini/gemini-cli #29577; LibreChat #16011; craft-agents-oss #710; HQBase #137 (ChatGPT does not request a refresh token); redhat template-agent #322 (SSO refresh races during long-running agent runs)
- **Who has the pain:** (a) developers running several coding-agent sessions; (b) platform teams running background or scheduled agents against SaaS; (c) SaaS vendors whose MCP servers get blamed ("your connector keeps logging me out").
- **What they do today:** Re-authenticate by hand. Each client project patches its own refresh lock or single-writer daemon. Server authors add grace windows. Some fall back to API keys or PATs.
- **Why current products fail:** Most of the bugs are in the clients (Claude Code, Codex, Copilot CLI, Gemini CLI), which an outside party cannot fix. Token vaults (Auth0 Token Vault with Privileged Worker, Nango, Composio, Arcade) fix this for agents built on top of them, not for off-the-shelf clients.
- **Why now:** MCP OAuth (DCR → CIMD) is new, background and parallel agents became normal in 2026, and rotating refresh tokens are spreading.
- **Potential product:** A local or hosted "credential broker" that sits between every MCP client and remote servers as one refresh writer (one daemon per machine or org, a proxy for remote MCP), plus a conformance test suite for MCP servers.
- **Time to value:** Days for a local broker.
- **Pilot (14–30 days):** One platform team running 50+ background agents against 3 rotating-token providers. Measure forced re-auths per week before and after.
- **Willingness to pay:** Low to medium. It looks like a bug fix, and clients will ship fixes (Glean, kody and OpenHands are already fixing theirs).
- **Expansion:** Org-wide credential inventory, revocation, audit. This runs straight into the agent-identity and NHI market.
- **Competition:** Auth0 Token Vault (Privileged Worker, EA), Nango, Composio, Arcade (background agents), Scalekit, Stytch, WorkOS, Descope, Keycard, MCPJam OAuth debugger, Cloudflare workers-oauth-provider, MCP gateways (Runlayer, Obot, Zuplo, TrueFoundry). Very crowded.
- **Moat (10/100/1,000):** 10: none. 100: provider quirk database (which IdPs rotate, which drop refresh_token). 1,000: still thin; the platforms absorb it.
- **CTO test sentence:** "Our background agents stop working every hour because Slack/Atlassian tokens expire and parallel sessions revoke each other. We want one thing that keeps every agent's connectors logged in."
- **Kill test question:** Six months from now, after Claude Code, Codex and Copilot ship cross-process refresh locks, is there any pain left that justifies a separate vendor? (Probably not.)
- **Scores:** Pain 6, Urgency 6, Timing 7, Speed to pilot 8, Integration 7, Reach 6, WTP 3, Competition 2, Moat 2, Market size 4, VC attractiveness 3. **Avg 4.9**

### 2. MCP tool-surface drift: "my server updated, my agent broke"

- **Problem:** Remote MCP servers change tool names, required parameters or descriptions without a version bump. Clients cache stale `tools/list` results. Agents do not crash; they degrade quietly by apologizing, retrying or hallucinating.
- **Recent evidence (~9):** mherod/swiz #998 (stdio servers keep advertising old schemas); Nitjsefnie/Overflow #654 and #782 (MCP surface changes never move the version; no breaking-change detection); lucashutyler #389 (clients cannot tell when tools change); adrirubio/claude-deck #447 (schema drift after tool additions); WordPress/mcp-adapter #313 (supporting breaking MCP revisions); macanderson/oxagen #4477 (pin and diff the tools agents see); pydelhi/talks #429 (a talk titled "My Server Updated, My Agent Broke"); hackernoon "why schema drift is the silent killer of MCP deployments"; tianpan.co "the tool schema migration that broke your agent retries for two weeks" (2026-06-03) and "Deprecating an API when your biggest client is a prompt" (2026-07-02); dev.to "catch MCP tool catalog drift"; arkforge "MCP Tool Description Drift".
- **Who:** Teams consuming third-party remote MCP servers in production agents; internal platform teams that publish MCP servers to many internal agents.
- **Today:** Pin `tools/list` as JSON in the repo and diff it in CI, write hand-rolled snapshot tests, wait for `notifications/tools/list_changed`.
- **Why products fail:** Gateways offer pinning, but it is a checkbox, not a workflow. There is no "changelog for agents" between producer and consumer.
- **Why now:** Vendors report a growing share of usage arriving through MCP (HN "Who is using MCP in production?": one commenter says many vendors see 15%+ of usage from MCP). Producers are iterating fast.
- **Potential product:** Contract registry for tool surfaces: snapshot, semantic diff, impact replay against recorded agent traces, deprecation channel to consumers.
- **Time to value:** 1 week. **Pilot:** One company with more than 10 internal MCP servers and more than 5 agent teams; count silent breakages caught.
- **WTP:** Medium-low (feels like CI tooling). **Expansion:** Into gateway or registry, which is contested.
- **Competition:** MCPJam (record/replay, CI), MCPSpec, test-mcp, mcpbr, Manufact, mintmcp (config drift), arkforge, Speakeasy/Gram, Stainless, Runlayer/Obot/TrueFoundry registries with version pinning, Boomi MCP management.
- **Moat:** 10: none. 100: trace corpus for impact analysis. 1,000: network of producer↔consumer contracts (weak).
- **CTO test sentence:** "Last month Atlassian changed an MCP tool and our triage agent quietly stopped filing tickets for 9 days."
- **Kill test question:** Will the MCP spec or the major gateways ship a version/changelog primitive before a startup gets traction?
- **Scores:** Pain 6, Urgency 5, Timing 7, Speed 8, Integration 7, Reach 5, WTP 4, Competition 4, Moat 4, Market 5, VC 5. **Avg 5.5**

### 3. Org-wide agent instruction and context drift (AGENTS.md, CLAUDE.md, skills across hundreds of repos)

- **Problem:** Instruction files and skills go stale and diverge across repos and tools, and agents treat them as authoritative. Companies now maintain two doc sets (human docs and agent docs).
- **Evidence (~8):** arXiv 2606.09090 "Context Rot in AI-Assisted Software Development" (stale code references in 23% of 356 repos); githubnext/gh-aw-cao issues #13191, #11290, #13637 (GitHub Next runs an automated "agents-md-curator" against drift, which is a platform signal); modelcontextprotocol/inspector #2427 (AGENTS.md and CLAUDE.md with no drift check); lifelike-and-believable #34 (lint the paths named in AGENTS.md); gist on AGENTS.md vs CLAUDE.md for the "#6235 cluster (5,200+ reactions)"; HN 44957776 (paraphrased: managing many agents.md files with duplication is painful); HN 48441589 / 47034087 / 47295454 (debate over whether AGENTS.md helps at all).
- **Who:** Platform or DevEx teams at companies with 200+ engineers using several coding agents.
- **Today:** Symlinks, `@AGENTS.md` imports, pre-commit sync hooks, cron diff-watchers, occasional "context engineer" hires (BT, Hex "Engineering Director, Agent Context").
- **Why products fail:** Most tools generate context; few verify it continuously against code.
- **Why now:** Agent instruction files became execution-critical in 2026.
- **Product:** Continuous "context CI": verify claims in instruction files and skills against code and config, propagate org rules, report drift.
- **Time to value:** Days. **Pilot:** 50 repos; count stale references fixed and agent PR rework.
- **WTP:** Low-medium. **Expansion:** Into skills registry and context engine, both contested.
- **Competition:** Tessl ($125M; skills registry, versioning, activation tracking), Unblocked (context engine), GitHub Next/Copilot itself, Factory, Augment, Sourcegraph, DeepWiki/Devin, DataHub (context management for data), vercel-labs/skills, OSS skills marketplaces.
- **Moat:** Weak; the platforms own the file formats.
- **CTO test sentence:** "Half our CLAUDE.md files reference build commands we deleted, and agents keep running them."
- **Kill test question:** Won't GitHub/Anthropic/Cursor ship "AGENTS.md lint and auto-refresh" natively? (GitHub Next is already prototyping it.)
- **Scores:** Pain 5, Urgency 5, Timing 7, Speed 8, Integration 8, Reach 6, WTP 3, Competition 3, Moat 3, Market 5, VC 5. **Avg 5.3**

### 4. Per-tenant memory isolation and verifiable deletion for teams building agent products

- **Problem:** Memory layers in agent frameworks pool every user's memories into one store. `user_id` scoping is often a no-op, background compaction crosses users, and deletes leave orphaned embeddings, which breaks GDPR erasure and customer offboarding.
- **Evidence (~8):** crewAI PR #5967 (per-tenant memory isolation; recall mixed users); PraisonAI #4818 (`user_id` scoping unenforced, cross-tenant leak); openclaw #66003 (shared vault across agents = cross-tenant leak); NousResearch/hermes-agent #34352 ("Solving the Multi-Tenant Hermes Problem"); Extra-Chill/data-machine #3487 (daily compaction summarizes other users' chats into the wrong memory); LibreChat #14988 (deleting KB files orphans vectors); mcp-guard #99; arXiv "Ghost Vectors" 2606.18497 (soft-deleted HNSW embeddings reconstructible); OSS governance layers (00sodj/amnesia, MNEME).
- **Who:** B2B AI product teams storing customer memory; their security and privacy reviewers.
- **Today:** Hand-thread `tenant_id` through every layer, one collection per tenant, manual delete scripts.
- **Why products fail:** Memory vendors focus on recall quality. One snippet notes Mem0/Zep are weak on conflict detection. Deletion proofs across vector, graph and history stores are rare.
- **Why now:** Persistent memory is shipping in B2B agents, and enterprise security questionnaires now ask about it.
- **Product:** Memory governance proxy: enforced scoping, cross-store delete with receipts, retention TTLs, audit.
- **Pilot:** One B2B agent company that has a pending enterprise security review.
- **WTP:** Medium if tied to closing deals. **Expansion:** Becomes a memory platform (crowded).
- **Competition:** Mem0, Zep, Letta, Supermemory, LangGraph/LangMem, vector DB native multi-tenancy (Pinecone namespaces, Turbopuffer, Weaviate), data-privacy vendors (Skyflow, Private AI). The scoping can be built in-house in days.
- **Moat:** Weak.
- **CTO test sentence:** "Our security review found customer A's memories retrievable from customer B's agent, and we can't prove deletions."
- **Kill test question:** Is this more than a feature that Mem0/Zep/vector DBs add in one quarter?
- **Scores:** Pain 6, Urgency 5, Timing 6, Speed 7, Integration 6, Reach 5, WTP 5, Competition 4, Moat 3, Market 5, VC 4. **Avg 5.1**

### 5. Cross-client MCP compatibility for SaaS vendors shipping public MCP servers

- **Problem:** One MCP server behaves differently across Claude, ChatGPT, Cursor, VS Code, Codex and Gemini CLI. Clients rename tools (dots become underscores, causing collisions), truncate names, use different OAuth registration methods (DCR, static, bearer), and ChatGPT refuses metadata without PKCE S256.
- **Evidence (~6):** VrajVed/mcp-use-compat (OSS: "Find what breaks your MCP server in Claude, ChatGPT, Cursor..."); ardianhermawan17 PR #61 (verify compatibility across clients); recoupable/mono #207 (OAuth across agent surfaces); HQBase #137; atlassian-mcp-server #171 (429s far below expected limits); HN "Who is using MCP in production?" (vendors serving several chat clients).
- **Who:** SaaS vendors' MCP/API teams. **Today:** Manual testing in each client.
- **Competition:** Manufact (YC S25; per-client analytics), MCPJam, mcp-use, Speakeasy Gram, Stainless, Cloudflare, TrackMCP, AgentCat. Crowded, and the problem shrinks as clients converge on the spec.
- **CTO test sentence:** "Our MCP server works in Claude but ChatGPT users can't connect and Cursor drops two tools."
- **Kill test question:** Does it survive client convergence on the 2026 spec?
- **Scores:** Pain 5, Urgency 5, Timing 6, Speed 8, Integration 8, Reach 7, WTP 4, Competition 3, Moat 3, Market 4, VC 4. **Avg 5.2**

### 6. Company knowledge freshness for agents (stale or conflicting docs outrank the truth)

- **Problem:** Retrieval ranks by similarity, so a polished old page beats a messy new correction (wording from Unblocked's blog). Agents answer from deprecated Confluence pages or columns.
- **Evidence (~6):** HN Ktx thread 48309986 (ARR example: agent unaware a column was deprecated); HN 47867392 (shared agents need shared context); arXiv 2606.26511 (temporal validity; old and new facts retrieved as equally relevant); arXiv 2605.06527 STALE benchmark; arXiv 2609.03588 KC-Bench; HN "Ask HN: Is every company's internal wiki just broken by default?" (older).
- **Competition:** Guru (verification workflows, now "AI source of truth"), Unblocked, Glean, FreshPage for Confluence/Rovo, Notion, Ktx (OSS), semantic layers (Cube, dbt, ThoughtSpot, PostHog), DataHub. Very crowded.
- **CTO test sentence:** "Our support agent quoted a refund policy we retired in March."
- **Kill test question:** What does this do that Guru verification plus Glean does not?
- **Scores:** Pain 7, Urgency 6, Timing 6, Speed 6, Integration 5, Reach 5, WTP 5, Competition 2, Moat 4, Market 7, VC 4. **Avg 5.2**

### 7. Tool-definition bloat and tool selection at scale (killed at scan)

- **Evidence:** HN 45954572, 47193064 (MCP server cutting Claude Code context use by 98%), 47157398 / 47305149 (mcp2cli), 47392011 ("CLI. Always CLI. Never MCP."); snippets cite ~55K tokens of definitions for a 5-server setup, accuracy dropping past 30–50 tools, 97% of MCP servers with description quality issues.
- **Why killed:** Platforms have fixed it. Anthropic Tool Search (`defer_loading`, ~85% reduction), OpenAI deferred hosted MCP, and code-mode/CLI patterns. The remaining GitHub issues (claude-code #30920, #86284; openai-agents-js #1978) are client bugs, not a market.
- **Scores:** Pain 5, Urgency 4, Timing 3, Speed 8, Integration 8, Reach 6, WTP 2, Competition 2, Moat 2, Market 4, VC 3. **Avg 4.3**

---

## Signals that didn't make it

- **Memory poisoning** (OWASP ASI06; eTAMP Apr 2026, MemMorph May 24 2026, GhostWriter and MemGhost Jul 2026; CSA research note 2026-07-23): real and rising, but this is generic agent security (excluded), and Akto, PointGuard, ShieldCortex and the gateways are already covering it.
- **Multi-agent handoff and shared-state collisions** (HN 46587478, 47358618, 47761625; arXiv 2608.29028): falls under orchestration frameworks (excluded).
- **MCP rate limits and agents DDoSing backends** (atlassian-mcp-server #171, awslabs/mcp #2949, zai GLM-5 #151, trinity #3244 retry repeating side effects): this is gateway territory (WSO2, Zuplo, Runlayer).
- **Silent tool failures when SaaS APIs are deprecated** (aiweekly alert; tianpan.co posts; Gravitee corpus): real, but folds into #2 and into API management vendors.
- **Memory-layer cost** (an HN snippet estimates $1–3K/month per 100K memories from LLM-on-every-op): this is a pricing complaint about Mem0/Zep, not a new category.
- **"Context engineer" as a role** (BT and Hex postings; DataHub report claims 95% of data teams will invest): shows budget exists, but DataHub, Unblocked and Tessl are already positioned there.
- **Internal MCP registries and gateways** (Uber and Sierra built their own; Obot, Zuplo, TrueFoundry blogs): the category is contested per STATUS.md.
- **Team memory for coding agents ("same mistake every session")**: mostly arXiv evidence (2608.00122, 2606.13174, 2606.12329) plus Show HN projects. Thin practitioner signal, and Claude/Cursor memory features cover it.

## Method caveats

- Reddit was not reachable. Most HN and GitHub dates could not be confirmed. The evidence leans on GitHub issues, which overweights developer-tool bugs and underweights enterprise operations pain.
- Several "evidence" items are arXiv papers or vendor blogs, which are weaker than practitioner posts. I counted them separately in my head when scoring, and none of the scores above rests on them alone.
