# G1: Agent resource sprawl across non-hyperscaler developer platforms. Deep dive

Date: 2026-10-06. I ran about 40 web searches. WebFetch and Reddit were blocked. **Every URL below came back in search results. I did not open any of the pages, so every claim is taken from a search snippet.** Items marked *(unverified)* need a check on the page. Prior-round figures come from `round15/P2_agent_pick_rate.md` and `round18/F5_agent_speed_procurement.md`.

**Thesis:** "Your coding agents now sign up for services, create databases, deploy apps and mint API keys across dozens of vendors on their own. Nobody knows what exists, who owns it, what it costs or what data is in it." The product would:
- discover every resource, account and key that agents created across vendors (Supabase, Neon, Vercel, Netlify, Railway, Render, Fly, Clerk, Resend, Upstash, Cloudflare, Stripe Projects providers, OpenAI/Anthropic keys and others);
- attribute each one to an agent session, a human and a repo;
- flag resources that are orphaned, costly or exposed;
- enforce policy (approved providers, auto-expiry, offboarding).

Buyer: CTO, VP Eng, Head of Platform or CISO at software companies with 50 to 2,000 engineers.

## Verdict: **KILL** (average score 4.8; eight of eleven scores below 7)

**Cause of death:** F1 (platform absorption) combined with F2 (visible-pain race). It also breaks taxonomy rules §4.1, §4.3 and §4.4.

**The behavior is real.** The why-now is one of the strongest we have:
- Vercel: agents trigger more than 50% of deploys.
- Supabase: AI tools start more than 60% of new databases.
- Neon: agents create more than 80% of databases.
- Stripe Projects plus Cloudflare: an agent can create a whole account, with billing, without a human.

Three findings kill it:

1. **The headline numbers mostly do not describe enterprise sprawl.** Much of Neon's 80% is platforms like Replit Agent creating databases under their own accounts. Neon says this outright: "if you're the company behind the agent, you'll quickly have a large database fleet full of inactive databases". Supabase's 60% is dominated by Claude Code, Lovable and other vibe-coder flows, and Supabase does not disclose how many of these become paid, persistent workloads. Large volume does not mean companies with 50 to 2,000 engineers have an ownership crisis. **I found no practitioner post at all** of the "Claude created 30 Supabase projects in our org" or "who owns this Neon DB" kind.
2. **The coverage gap closed during 2026.** In order of how much they matter:
   - **Wiz** now lists Vercel, Cloudflare, OpenAI Platform and Linode as environments, next to AWS, GCP and Azure.
   - **Nudge Security** discovers every SaaS or cloud account created with a work email, including Vercel and Supabase, plus OAuth grants and remote MCP connections.
   - **Vercel** made Enterprise Managed Users generally available on Aug 11 2026. It blocks personal accounts on company domains and puts lifecycle in the IdP.
   - **Neon** deletes preview branches automatically.
   - **Stripe Projects** has per-provider spend caps and scoped, delegated agent identities.
   - **NHI vendors** (Oasis $120M, Astrix, Token, Aembit, Keycard, which acquired Anchor.dev to govern coding agents) already discover API keys across SaaS and PaaS.
   - **GitGuardian** detects Supabase and AI-service secrets.
3. **The only new piece is linking a resource to the agent session that created it.** That is a feature of whoever logs the tool calls: Anthropic or Cursor (agent telemetry), Stripe (the orchestrator ledger), Keycard or Vercel Connect (the credential broker). It is not a standalone system of record.

---

## 1. Evidence of the behavior and the pain

| Signal | Source | Read |
|---|---|---|
| Agent-initiated weekly Vercel deploys rose from under 3% to more than 50% between Jan and Jul 2026 | https://startupfortune.com/guillermo-rauch-says-ai-agents-now-trigger-more-than-half-of-all-vercel-deployments/ (via P2) | Real. It counts deploys, not orphaned resources |
| More than 60% of new Supabase DBs are started by AI tools, Claude Code the largest source; DB launches up 600% YoY. Supabase "did not disclose how many of the AI-started databases become paid, persistent workloads" | https://www.implicator.ai/supabase-doubles-to-10-5-billion-as-agents-deploy-most-of-its-databases/ ; https://letsdatascience.com/blog/supabase-10-5-billion-ai-agents-build-most-databases | Much of it is ephemeral or hobby use. Supabase raised $500M at $10.5B (Jun 2026) and $150M led by GIC and CapitalG (late Sep 2026) *(unverified)* |
| More than 80% of Neon DBs are created by agents. Replit Agent creates "thousands of Postgres databases per day" on Neon | https://neon.com/use-cases/ai-agents ; https://www.databricks.com/blog/databricks-neon | **Platform-owned fleets** (Replit and other codegen platforms), not employer sprawl |
| Stripe Projects: agents provision and pay for services from the CLI or API. About 50 providers (32 live at one update, with 13 and then 16 added later). Integrated with Hermes, Factory Droids and Warp. Volume reportedly grew from 70K (Mar) to 560K (Jun) transactions *(unverified, per F5)* | https://stripe.com/blog/stripe-projects-adds-new-agents-providers-developer-controls ; https://www.createwith.com/tool/stripe/updates/stripe-projects-adds-13-providers-across-ai-data-and-growth | Small but growing. Stripe holds the ledger of what was provisioned |
| Cloudflare is the first major provider on the Stripe Projects protocol. "If the user has no existing Cloudflare account, Cloudflare provisions one automatically"; $100 a month per provider by default. Any platform with signed-in users can act as orchestrator | https://blog.cloudflare.com/agents-stripe-projects ; https://www.infoq.com/news/2026/05/cloudflare-stripe-agent-commerce ; https://ppc.land/cloudflare-lets-ai-agents-open-accounts-buy-domains-and-ship-code-no-human-required/ | **The most interesting raw signal:** accounts created under an individual's identity, outside any company org. Enterprise adoption is unknown |
| Stripe Projects writes credentials to a local `.env` and `.projects/vault/`, with a warning not to commit them | https://docs.stripe.com/cli/projects/billing ; https://support.stripe.com/questions/stripe-projects | A secrets-sprawl vector, already covered by GitGuardian-style scanning |
| UpGuard: 16,326 Supabase DBs with publicly readable tables, over half with PII signals | https://cybernews.com/news/16000-supabase-databases-exposed/ | Loud, public pain, but mostly indie and vibe-coded apps |
| Moltbook: Supabase key in client JS exposed about 30K emails and about 1.5M API keys | https://securitybrief.co.uk/story/moltbook-vibe-coded-flaw-exposed-ai-chats-keys | Same pattern: indie or startup, not a 500-engineer company |
| GitGuardian 2026: 29M secrets on public GitHub (+34%). AI-service leaks +81% (1.28M). Supabase secrets +992%. 32% of internal repos hold a hardcoded secret | https://thehackernews.com/2026/03/the-state-of-secrets-sprawl-2026-9.html ; https://www.gitguardian.com/state-of-secrets-sprawl-report-2026 | Strong evidence of leaked keys, already owned by GitGuardian |
| Vercel breach (Apr 2026): Context.ai OAuth compromise, then access to non-sensitive customer env vars. The infostealer also took Supabase, Datadog and Authkit logins | https://trendmicro.com/en_us/research/26/d/vercel-breach-oauth-supply-chain.html ; https://www.halborn.com/blog/post/explained-the-vercel-hack-april-2026 | Pushed buyers toward "rotate everything stored on Vercel". Wiz, Nudge and GitGuardian marketed against it |
| An agent ran up about $6.5K on AWS in a day (DN42 incident) | https://braindetox.kr/en/posts/ai_agent_6531_aws_bill_2026.html *(unverified secondary source)* | Bill shock exists, but on AWS, where FinOps and CSPM already look |
| Vercel previews are kept 6 months by default. Neon now deletes branches automatically when the last preview is gone. A "Vercel Preview Cleanup" skill exists | https://neon.com/docs/guides/vercel-branch-cleanup ; https://mcpmarket.com/tools/skills/vercel-preview-cleanup | Sprawl gets fixed **by the vendor** or by a free skill |
| Essays on "orphaned agents" and "agent-created infra has no ownership trail" | https://guptadeepak.com/ciso/orphaned-agents/ ; https://tianpan.co/blog/2026-06-01-the-recurring-task-your-agent-scheduled-with-nobody-to-inherit ; https://www.cio.com/article/4162664/shadow-ai-morphs-into-shadow-operations.html | Thought leadership exists. NHI vendors already claim the "orphaned agent" framing |
| Practitioner complaints ("Claude created N Supabase projects", "who owns this Neon DB") | Searches returned **nothing** (Reddit blocked) | **No public evidence of the specific enterprise pain** |

**Read:** agents provisioning resources is a large, real and new behavior. But the pain splits into slices that already have owners:
- **Data exposure:** the Supabase RLS and leaked-key incidents.
- **Secrets:** GitGuardian.
- **Accounts outside SSO:** Nudge, Grip, Vercel EMU.
- **Cost:** Vantage, Stripe caps, Neon scale-to-zero.

The thesis's distinct claim ("nobody knows what exists or who owns it, across vendors, inside 50 to 2,000 engineer companies") has no public evidence. That cuts two ways: it may be early (a B argument), or most agent-created resources may live in hobby, startup and platform-owned accounts that an employer never has to govern.

## 2. Competitors

| Layer | Player | Coverage of the thesis | Overlap |
|---|---|---|---|
| CNAPP | **Wiz** (Google) | Environments list includes **Vercel**, **Cloudflare**, **OpenAI Platform**, Linode, OCI, Snowflake, Databricks, GitHub/GitLab and Copilot Studio agents. The Vercel connector ingests projects, domains, teams, members and firewall config into the Security Graph and flags public projects that could leak sensitive data. https://www.wiz.io/environments ; https://wiz.io/blog/introducing-wiz-vercel-integration | **High.** Supabase and Neon were not found in Wiz's list (the gap is a quarter of connector work, not a moat) |
| CNAPP | Orca, Palo Alto | Nothing found for Vercel or Supabase *(unverified absence)* | Low today. They follow Wiz |
| SaaS discovery / SSPM | **Nudge Security** | Discovers "every managed and unmanaged cloud and SaaS account ever created" through Google Workspace and email. Shows who signed up, when, and which scopes. Security profiles exist for Vercel and Supabase. Detects remote MCP connections. Launched an OAuth Grant Risk Analyst agent (Jul 2026). Reports 88 OAuth grants per employee. https://www.nudgesecurity.com/post/were-taking-on-sprawling-oauth-and-browser-extension-risk-with-two-new-ai-agents ; https://nudgesecurity.com/faqs | **Very high** on "which accounts exist and who owns them". Weak on resources *inside* accounts and on attribution to an agent session |
| SaaS discovery | **Grip Security** | Email, browser and IdP signals cover the "full long tail of shadow applications". https://www.upguard.com/competitors/grip-security | High |
| SaaS discovery | Reco | "Vibe coding security governance": discovery of Lovable, Base44 and v0 apps and coding tools. https://www.reco.ai/use-cases/vibe-coding-security-governance | Medium-high |
| SaaS discovery | AppOmni Agent Inventory (May 2026) | Agents inside SaaS platforms | Medium |
| SaaS management | Zylo, Productiv | Spend and licence discovery. Nothing found specific to developer infrastructure *(unverified)* | Medium (finance view of the same vendors) |
| NHI / agent identity | **Oasis** ($120M, Mar 2026), **Astrix**, Token Security ($20M A), Aembit, Clutch, Entro | Discover API keys, OAuth tokens and service accounts across IaaS, SaaS and PaaS. Assign owners with ML. Rotate. Oasis claims ownership assignment explicitly. https://raising.fi/news/oasis-security-series-a-march-2026 ; https://zeltser.com/media/rsac-2026-sandbox/token-security | **Very high** on the "mint API keys, nobody owns them" half |
| Agent credential broker | **Keycard** ($38M; acquired Anchor.dev in Feb 2026 "to govern coding agents"). Its MCP gateway for Supabase logs each call with user identity and resource, and fronts 29 tools including project creation | https://www.securityweek.com/keycard-emerges-from-stealth-mode-with-38-million-in-funding/amp/ ; https://docs.keycard.ai/admin/catalog/mcp-servers/supabase | **Very high** on enforcement and agent-session attribution |
| Secrets | **GitGuardian**, Doppler, Infisical | Supabase and AI-service secret detectors. Vaults | High on leaked keys |
| FinOps | **Vantage** | Native Vercel (FOCUS billing API), Cursor, MongoDB, Datadog and 30+ others, plus "custom providers" for anything else. Neon, Supabase and Clerk are not native. https://www.vantage.sh/integrations/vercel ; https://vantage.sh/integrations/custom-providers | High on cost |
| Orchestrator | **Stripe Projects** | Global and per-provider monthly spend caps. Delegated agent identities with scoped credentials and spending guardrails per Project. Credentials held in Stripe Secret Store. https://docs.stripe.com/cli/projects/billing | **Owns the ledger** of agent-provisioned services on its rail |
| Vendor org admin | **Vercel** EMU (GA Aug 11 2026), Passport, Connect (short-lived scoped tokens with audit trails). **Neon** auto branch cleanup. **Supabase** org SSO, RBAC and audit. **Lovable** spending its $400M on governance and permissions | https://vercel.com/changelog/enterprise-managed-users ; https://www.createwith.com/tool/vercel/updates/vercel-launches-enterprise-agent-platform-with-built-in-security-controls ; https://siliconangle.com/2026/08/12/vibe-coding-startup-lovable-doubles-valuation-13-3b-400m-raise/ | High. Each vendor fixes sprawl inside its own platform |

**Is anyone doing exactly "cross-vendor inventory of agent-created resources, attributed to agent session, human and repo"?** I found no single SKU that does. But the parts already exist:
- **Nudge or Grip:** accounts and owners.
- **Wiz:** resources and exposure on Vercel, Cloudflare and OpenAI.
- **Oasis or Astrix:** keys and owners.
- **GitGuardian:** env files and repos.
- **Vantage:** cost.
- **Keycard or Stripe:** agent-session lineage at provisioning time.

What is left is linking the agent session to the resource. That is F5 (sprint-buildable) for any of the players above.

## 3. Absorption risk: **very high**

- **Wiz:**
  - It already put Vercel, Cloudflare and OpenAI into the Security Graph.
  - Adding Supabase, Neon, Railway, Render and Fly is roadmap work. It has the CISO budget at exactly this ICP.
  - Google ownership adds the incentive to cover "everything that isn't AWS".
- **Stripe:**
  - As orchestrator it knows every account, provider, cost and credential an agent created through Projects.
  - An org-level "Projects admin" view (approved providers, owners, offboarding) is a natural upsell.
  - Stripe has no conflict here: governance makes enterprises comfortable letting agents spend through Stripe.
- **Vercel, Supabase, Neon:**
  - Each has a direct revenue reason to make its own enterprise org governance excellent: EMU, SSO and audit are Enterprise-plan upsells.
  - They have no incentive to help a neutral layer, but they do not block one either (APIs exist).
- **Agent vendors (Anthropic, Cursor):**
  - Managed settings and tool-call logs already record which MCP calls created which resources.
  - "Resources created by this session" is a dashboard feature for them.
- **Nudge:**
  - Already markets "every cloud account ever created".
  - Adding "created via Stripe Projects or an agent" is a classifier on top of signals it already collects.

**No incumbent is structurally barred** (taxonomy §4.4). The neutrality argument (§2.2) is weak: buyers already accept Wiz plus Nudge.

## 4. Buyers, ACV and ARR math (estimates, not sourced)

- **Buyer pool:** software companies with 50 to 2,000 engineers. I estimate about 15K to 25K worldwide *(estimate)*.
- **Reachable share:** those with real use of non-hyperscaler platforms plus agent rollout (Claude Code or Cursor at scale) is perhaps 5K to 10K.
- **ACV:** platform-security comparables (Nudge, NHI) price per employee or per identity. A standalone sprawl product would land at $20K to $60K. Median about $30K.
- **$10M ARR:** about 330 customers at $30K. Plausible as a product, but you would be selling against Nudge and Wiz renewals.
- **$100M ARR:** about 3,300 customers at $30K. That means roughly a third to half of the reachable pool, displacing Wiz, Nudge and NHI line items. It fails rule §4.5: it needs the whole niche plus wins against funded incumbents.
- **Usage-based alternative:** a fee per discovered resource grows with agent activity. But resources are mostly ephemeral and free-tier, so value per resource is tiny, and Neon's own economics are built on cheap idle DBs.

---

## Finalist format

- **One-line problem:** Coding agents create accounts, databases, deployments and keys across dozens of non-hyperscaler vendors. No one can list them, name an owner, see the cost or know what data sits in them.
- **Why now:**
  - Agent-triggered Vercel deploys went from under 3% to over 50% in 2026.
  - Agents create 60%+ of new Supabase DBs and 80%+ of Neon DBs.
  - Stripe Projects and Cloudflare let agents open accounts and pay without a human (2026).
  - The Vercel breach in Apr 2026 made "what secrets live on PaaS X" a board question.
- **Exact buyer:** CISO (exposure), with Head of Platform as co-signer. The CFO only for cost, which is small.
- **Exact ICP:** software companies with 200 to 2,000 engineers, more than 50% of them on Claude Code or Cursor, with at least 5 non-hyperscaler developer platforms in use, Google Workspace or Okta as IdP, and no Wiz or Nudge yet.
- **Current workaround:**
  - Nudge or Grip for account discovery.
  - Wiz connectors for Vercel, Cloudflare and OpenAI.
  - GitGuardian for keys in repos.
  - Vendor SSO/EMU and an enterprise-plan consolidation ("everyone moves to the company Vercel team").
  - Stripe Projects spend caps.
  - Quarterly manual cleanup.
- **Why incumbents cannot easily own it:** they can. Wiz, Nudge and Stripe each hold more than half of the needed data. The only thin claim is cross-vendor lineage from agent session to resource, which none sells today.
- **30-day MVP:**
  - Connect the Google Workspace mailbox (sign-up and invoice emails), GitHub (env files, `.projects/` folders, vendor SDK imports), Claude Code and Cursor telemetry, and the Supabase, Neon and Vercel org APIs.
  - Output one inventory table: resource, vendor, creator, agent session, repo, last activity, monthly cost, public exposure and PII flag.
  - Add Slack nudges to owners and auto-expiry for idle resources.
- **Pilot design:**
  - 3 companies, 14 days, read-only.
  - **Success:** more than 30% of the discovered vendor accounts or resources are unknown to the platform team, **and** at least one exposed or PII-bearing resource that Wiz or Nudge did not flag, **and** willingness to pay $25K or more.
- **Pricing hypothesis:** $20 to $40 per engineer per year (about $20K to $60K ACV), or a platform fee.
- **Expansion path:** inventory, then policy (approved providers, expiry), then agent-provisioning gateway (be the orchestrator), then FinOps for the long tail of vendors.
- **Moat:** weak. Connector breadth can be copied. Agent-session lineage needs telemetry owned by Anthropic, Cursor and Stripe. There is no network effect.
- **Why it could be $10B+:** only by becoming the orchestrator itself: the enterprise control plane through which every agent provisions every third-party service. That is Stripe Projects' declared role, and Stripe starts with the rail, the identity and the providers.
- **Direct competitors and adjacent threats:** Nudge Security, Grip, Reco, AppOmni, Wiz, Oasis, Astrix, Token, Aembit, Clutch, Keycard, GitGuardian, Vantage, Stripe Projects, Vercel (EMU, Connect, Passport), Supabase and Neon native controls, Anthropic and Cursor managed settings.
- **One sentence to a CTO:** "Your agents created 312 databases, deployments and API keys across 23 vendors last quarter. Here is who owns each one, what it costs, and the 9 that hold customer data in public." *(Likely reply: "Nudge shows our accounts and Wiz covers Vercel. Why a third tool?")*
- **5 customer discovery questions:**
  1. How many vendor accounts or projects (Supabase, Neon, Vercel, Railway, Cloudflare and so on) exist outside your company org today? How did you count them?
  2. In the last 90 days, did an agent create a resource that later caused an incident, a bill, or a cleanup task? What did it cost?
  3. Do you run Nudge, Grip or Wiz? What do they miss on these platforms, specifically?
  4. Have you pushed engineers onto enterprise or EMU orgs for Vercel and Supabase? Did that solve it?
  5. Is anyone using Stripe Projects or Cloudflare agent sign-up at work? Would you block it or govern it?
- **Hard kill criteria:**
  - (a) At 3 of 5 target companies, Nudge plus Wiz already find more than 80% of what a pilot finds. **Likely met**, given the coverage above.
  - (b) Unknown or unowned resources are fewer than 10 per 100 engineers.
  - (c) No exposed or PII resource found that existing tools missed.
  - (d) Stripe ships an org admin for Projects, or Wiz adds Supabase and Neon. **Expected within 2 to 3 quarters.**

### Scores

| Dimension | Score | Why |
|---|---|---|
| Pain | 5 | Real for indie and vibe-coder apps (16K exposed Supabase DBs). Not shown inside 50 to 2,000 engineer companies |
| Urgency | 4 | Rotate secrets after the Vercel breach, yes. But no regulation, and incidents land on small companies |
| ROI clarity | 4 | Long-tail costs are small (scale-to-zero, free tiers). The value is risk avoidance |
| Customer accessibility | 6 | CISOs are reachable but are pitched by Nudge, Wiz and NHI vendors constantly |
| Pilot speed | 7 | Read-only connectors give a 14-day pilot |
| Market size | 5 | About 5K to 10K reachable buyers at about $30K. $100M needs a third or more of the niche |
| Expansion | 5 | Gateway and orchestrator expansion runs straight into Stripe and Keycard |
| Venture potential | 4 | Reads as a Nudge, Wiz or Stripe feature |
| Defensibility | 3 | Connectors can be copied. The lineage data is owned by agent vendors and Stripe |
| Why now | 8 | Genuinely new behavior (50% / 60% / 80% agent shares, agent account creation) |
| Competition position | 2 | Funded incumbents cover every slice |
| **Average** | **4.8** | **KILL**: F1 + F2. Fails §4.1, §4.3, §4.4 and §4.5 |

### Why not B

B requires the thesis to be unresolved and too early for public evidence. The behavior is public. Discovery (Nudge, Grip), posture (Wiz now on Vercel, Cloudflare and OpenAI), keys (Oasis, Astrix, GitGuardian), cost (Vantage) and agent provisioning controls (Stripe, Keycard, Vercel Connect) all shipped in 2025 and 2026. The missing proof that companies with 50 to 2,000 engineers suffer is more likely a sign that the worst sprawl sits in hobby and platform-owned accounts than a sign the market is early.

**Signal worth watching (not a thesis):** the **"agent creates a new vendor account under a personal identity"** path: Stripe Projects plus Cloudflare auto-account creation, outside Vercel EMU-style domain capture. If Stripe Projects shows real use inside companies (for example, more than 10% of engineers at a 500-engineer company) and Stripe does **not** ship an org admin within two quarters, re-open the question as "orchestrator for the enterprise". A cheap check: ask 5 Nudge customers whether Nudge already surfaces Stripe Projects-created Cloudflare and Neon accounts. If it does, the space is closed.

## Sources (all from search snippets; not opened)
- Stripe Projects: https://stripe.com/blog/stripe-projects-adds-new-agents-providers-developer-controls ; https://docs.stripe.com/cli/projects/billing ; https://docs.stripe.com/cli/projects/spend ; https://support.stripe.com/questions/stripe-projects ; https://www.createwith.com/tool/stripe/updates/stripe-projects-adds-13-providers-across-ai-data-and-growth ; https://www.createwith.com/tool/stripe/updates/stripe-projects-expands-provider-catalog-with-wix-laravel-heygen-and-more
- Cloudflare: https://blog.cloudflare.com/agents-stripe-projects ; https://www.infoq.com/news/2026/05/cloudflare-stripe-agent-commerce ; https://ppc.land/cloudflare-lets-ai-agents-open-accounts-buy-domains-and-ship-code-no-human-required/ ; https://www.computerworld.com/article/4165880/are-we-ready-to-give-ai-agents-the-keys-to-the-cloud-cloudflare-thinks-so-2.html
- Supabase and Neon: https://www.implicator.ai/supabase-doubles-to-10-5-billion-as-agents-deploy-most-of-its-databases/ ; https://letsdatascience.com/blog/supabase-10-5-billion-ai-agents-build-most-databases ; https://neon.com/use-cases/ai-agents ; https://neon.com/docs/guides/vercel-branch-cleanup ; https://runtimewire.com/article/supabase-raises-150m-acquires-turso
- Exposure and secrets: https://cybernews.com/news/16000-supabase-databases-exposed/ ; https://securitybrief.co.uk/story/moltbook-vibe-coded-flaw-exposed-ai-chats-keys ; https://thehackernews.com/2026/03/the-state-of-secrets-sprawl-2026-9.html ; https://www.gitguardian.com/state-of-secrets-sprawl-report-2026
- Vercel breach and controls: https://trendmicro.com/en_us/research/26/d/vercel-breach-oauth-supply-chain.html ; https://www.halborn.com/blog/post/explained-the-vercel-hack-april-2026 ; https://vercel.com/changelog/enterprise-managed-users ; https://vercel.com/docs/security/enterprise-managed-users ; https://www.createwith.com/tool/vercel/updates/vercel-launches-enterprise-agent-platform-with-built-in-security-controls
- Wiz: https://www.wiz.io/environments ; https://wiz.io/blog/introducing-wiz-vercel-integration
- Nudge, Grip, Reco, AppOmni: https://www.nudgesecurity.com/post/were-taking-on-sprawling-oauth-and-browser-extension-risk-with-two-new-ai-agents ; https://nudgesecurity.com/faqs ; https://nudgesecurity.com/security-profile/vercel-com ; https://www.upguard.com/competitors/grip-security ; https://www.reco.ai/use-cases/vibe-coding-security-governance ; https://blogs.apievangelist.com/blogs/appomni-2026-05-21-agent-inventory-for-saas-ai-agents/
- NHI and agent identity: https://raising.fi/news/oasis-security-series-a-march-2026 ; https://zeltser.com/media/rsac-2026-sandbox/token-security ; https://www.securityweek.com/keycard-emerges-from-stealth-mode-with-38-million-in-funding/amp/ ; https://docs.keycard.ai/admin/catalog/mcp-servers/supabase
- FinOps: https://www.vantage.sh/integrations/vercel ; https://vantage.sh/integrations/custom-providers
- Bill shock and orphaned agents: https://braindetox.kr/en/posts/ai_agent_6531_aws_bill_2026.html ; https://guptadeepak.com/ciso/orphaned-agents/ ; https://www.cio.com/article/4162664/shadow-ai-morphs-into-shadow-operations.html
- Lovable: https://siliconangle.com/2026/08/12/vibe-coding-startup-lovable-doubles-valuation-13-3b-400m-raise/
