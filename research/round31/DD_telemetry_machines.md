# Deep dive: Telemetry for machine readers (Round 31, Thesis 1, scored 6.7 before this review)

Date: 2026-10-06. I ran 12 web searches. Every URL below comes from those search results. Inputs: BRIEF.md, T6_replacements.md (Thesis 1), STATUS.md (generic observability was killed earlier and AI SRE was judged crowded).

**Verdict up front: KILL as a standalone category bet. The revised average is 5.0.** The broken assumption is real. But every serious incumbent has already shipped the fix (an agent query surface plus cheap columnar or customer-account storage), and funded challengers own each remaining angle. One narrow residual idea is kept at the end, but it does not stand on its own as a company.

---

## Evidence gathered (last ~90-240 days)

1. **Datadog Q2 2026:** MCP tool calls grew more than 22x since Q4 2025. More than 750 AI customers. Net revenue retention (NRR) is in the low 120s. Datadog is *monetizing* agent readers, not losing them. https://www.marketbeat.com/instant-alerts/datadog-q2-earnings-call-highlights-2026-08-06/
2. **Datadog MCP Server** went GA in Q1 2026 (Q1 revenue $1,006M, up 32% YoY). https://investors.datadoghq.com/news-releases/news-release-details/datadog-announces-first-quarter-2026-financial-results
3. **Grafana Labs:** more than $600M ARR and 10k customers. Grafana Assistant is used by 18k orgs. Assistant Investigations and Adaptive Telemetry are separate products (Aug 2026). https://grafana.com/press/2026/08/26/grafana-labs-crosses-10000-customer-milestone-as-ai-adoption-accelerates-growth-across-the-platform/
4. **ClickHouse:** Managed ClickStack (HyperDX) ships AI notebooks. ClickHouse also bought Langfuse in 2026 and markets itself as "the agentic AI database". https://clickhouse.com/docs/cloud/manage/clickstack ; https://sacra.com/chat/h/a5c45d66-bcae-4d53-9760-ba4909886d7b/
5. **Snowflake closed the Observe acquisition** on Feb 2, 2026. It sells AI agents on telemetry stored in Snowflake. https://www.snowflake.com/en/blog/observe-acquisition-ai-powered-observability/
6. **Palo Alto is buying Chronosphere for $3.35B.** Chronosphere had more than $160M ARR, and the plan pairs it with AgentiX for autonomous remediation. https://securityboulevard.com/2025/11/palo-alto-networks-to-acquire-ai-era-observability-platform-chronosphere-for-3-35-billion/
7. **Coralogix raised a $200M Series F at $1.6B** (Jun 2026). It runs in-stream analytics with no indexing, has more than 5k customers and grows more than 60%. https://www.tamradar.com/funding-rounds/coralogix-series-f-200m
8. **Tsuga raised a $35M Series A** (Jun 2026, General Catalyst, DST, Databricks Ventures). It is "AI-native" observability deployed in the customer's own cloud, with no egress, and aimed at cost. https://www.tsuga.com/resources/blog/we-raised-35-million-here-is-why-and-what-it-means-
9. **OpenObserve raised a $10M Series A.** It has an AI SRE, MCP support and S3-native storage. https://pulse2.com/openobserve-raises-10-million-series-a-to-accelerate-ai-native-observability/
10. **Honeycomb** has a hosted MCP that exposes its whole query engine (BubbleUp, SLOs) to Claude Code, Cursor and custom SRE agents, plus Canvas for multi-agent investigations. https://www.honeycomb.io/blog/hosted-mcp-now-available ; https://devops.com/honeycomb-adds-ability-to-orchestrate-multiple-ai-agents-to-observability-platform/
11. **Cribl** has more than $300M ARR, an MCP server, and agentic Cribl Search (Mar 2026). https://toolradar.com/tools/cribl-mcp ; https://www.startuphub.ai/startups/cribl.md
12. **Resolve AI is at $1.5B** (Apr 2026). Coinbase, DoorDash, MongoDB and Salesforce run it in production. https://www.beri.net/article/resolve-ai-190m-ai-sre-production-incidents-2026
13. **Traversal** has $48M from Kleiner and Sequoia plus an Amex Ventures strategic investment (Mar 2026), and targets large enterprises. https://www.businesswire.com/news/home/20260304551167/en

Dash0 did not come up in my searches. I treat it as another OTel-native, AI-first entrant, but that is not verified.

---

## Role 1: Technical architect

**What really changes when agents read telemetry**

- **Query economics flip.** Humans query rarely and in predictable ways. That is why vendors index at write time and show dashboards. An AI SRE runs 50-500 queries per investigation, across arbitrary high-cardinality dimensions. The cost moves from ingest and index to scan and compute. Columnar storage on object storage (ClickHouse, Iceberg on S3) plus compute priced per query fits this better than an inverted index billed per GB.
- **The best context is change data, not telemetry.** Agents get the best answers by joining telemetry with deploys, PRs, feature flags, config diffs and ownership. That "change/causality graph" is where answer quality comes from. It is also exactly what Resolve and Traversal build *on top of* any store.
- **Retention policy driven by the reader.** If the agent is the reader, you can measure which signals investigations actually use. Keep those hot, move the rest to cold storage, and drop what is never used. This is a closed loop that humans could never run. Grafana Adaptive Telemetry and Cribl already do a heuristic version of it.
- **Regenerate instead of retain.** Agents can rerun or replay a request with debug logging turned on, instead of storing everything. This only works for deterministic or replayable services, so it is research-grade.
- **Interface.** MCP or SQL with a semantic schema (OTel semantic conventions) plus a planner that bounds cost per question. Every vendor in the evidence list already has an MCP server.

**Architect's conclusion:** the right architecture is clear, and it is becoming a commodity: OTel, then object storage, then a columnar engine, then MCP, then a change graph. Nothing in it needs a new company to own a primitive.

## Role 2: Skeptical CTO

- "My Datadog bill hurts, but my AI SRE pilot (Resolve, or Bits) already reads Datadog through MCP. Why would I re-platform my storage to make an agent slightly better?"
- "If I want cheap, I already have ClickStack, Grafana or Coralogix quotes. And Snowflake now owns Observe, and we have a Snowflake commit."
- "Dual-writing is easy. Moving alerts, dashboards, SLOs, on-call and compliance retention is a 6-12 month migration. Agent-native does not remove that."
- "Per-investigation pricing scares me. Agents loop. I would rather have a fixed $/TB."
- **Would they run a pilot?** Yes, as a cost play, which is a fight against 6+ funded cost-down vendors. No, as an "agent answers are better" play, because that is benchmarked against Resolve or Traversal sitting on the existing store.

## Role 3: Top-tier VC partner

- The market is huge and re-platforming is real: Chronosphere sold for $3.35B, Observe was acquired, Coralogix is at $1.6B. That is exactly the problem: the **2025-26 vintage is already funded and largely exited.** Tsuga (GC/DST, Jun 2026) is the in-customer-cloud plus AI-native bet. OpenObserve is the OSS bet. Coralogix is the no-index bet. Resolve and Traversal are the reader-agent bets.
- Datadog's 22x growth in MCP calls and NRR in the low 120s weaken the innovator's-dilemma story. Agent reads *increase* Datadog usage, and Datadog can price per Bits investigation on top of per-GB without cutting its own revenue.
- A new entry would need a non-obvious edge, for example owning the change graph as a standard. That is an AI SRE feature, and AI SRE is already crowded per STATUS.
- **Decision: pass**, unless the team brings a proprietary data asset or a distribution channel such as a cloud marketplace default.

## Role 4: Competitor analyst

| Player | Storage cost story | Agent-reader story | Threat to thesis |
|---|---|---|---|
| Datadog | Weak (per-GB), but Flex Logs exists | MCP GA, Bits AI SRE, 22x MCP calls | High: owns the data and the workflow |
| Splunk/Cisco | Weak | AI assistant, Cisco bundling | Medium: enterprise lock-in |
| Grafana | Strong (Loki/Mimir, Adaptive Telemetry) | Assistant plus Investigations, 18k orgs | Very high |
| Chronosphere/PANW | Strong (control plane, drop/shape) | AgentiX remediation | High in security-led enterprises |
| ClickHouse/ClickStack | Strongest per $ | AI notebooks, Langfuse, "agentic DB" | Very high: this *is* the proposed architecture |
| Observe/Snowflake | Strong (S3/Snowflake) | O11y agents, "10x faster" | High: rides Snowflake commits |
| Honeycomb | Medium | Full-engine MCP, Canvas | Medium (mid-market) |
| Dash0 (unverified) | OTel-native | AI-first | Low-medium |
| Coralogix | Strong (no index) | AI-native, $200M raise | High |
| Cribl | Pipeline routing to cheap lakes | MCP, agentic Search | High: kills the "cheap raw storage" wedge |
| Tsuga | In-customer-cloud | AI on in-perimeter data | Direct clone of the proposed thesis |
| Resolve / Traversal | Store-agnostic | The reader agent itself | Takes the "better answers" value |

**Gap analysis:** "cheap store" is taken by ClickHouse, Coralogix, Grafana, OpenObserve and Tsuga. "Agent reader" is taken by Resolve, Traversal, Bits and Grafana Assistant. "Agent API on telemetry" is everyone's MCP. The only thing with no clear owner is **pricing per question answered, with a guaranteed cost cap**. That is a pricing tactic, not a structural moat.

---

## Self red-team

- *Steelman for:* telemetry volume really may grow 5-10x, and the per-GB contracts were signed before agents. A forced renewal crisis in 2027 could reopen accounts. Counter: that crisis benefits whoever already holds a cheap store, which is ClickHouse, Grafana or Coralogix, not a seed-stage company.
- *Did I under-weight Datadog's weakness?* Datadog grew 32% with NRR in the low 120s. There is no sign it is being displaced. AI-native customers, the most likely early adopters, are paying Datadog more than $10M/yr (8 of them).
- *Is the reader-driven retention loop a moat?* It needs the reader agent and the store in the same product. Grafana and Datadog have both. A newcomer has neither.
- *Did the earlier analysis repeat a killed thesis?* Mostly yes. Without the agent-reader story, this is the killed "generic observability" thesis, and the agent-reader part belongs to the crowded AI SRE space.

---

## Final sharpened thesis (brief format)

**Shape:** Observability (~$50B) works like an indexed, per-GB, dashboard-first SaaS because it assumed humans read telemetry rarely, in predictable patterns, and that volume grows at headcount speed. AI makes this false: agent-written services multiply volume, and AI SREs become the main reader, running hundreds of ad hoc queries per incident. So the category must be rebuilt as **telemetry stored in the customer's own object storage, kept or dropped based on which signals the reader agent actually uses, and billed per answered investigation with a hard cost cap.**

- **Existing category:** observability and log analytics (Datadog, Splunk, Elastic, New Relic, Sumo).
- **Market size:** about $50B TAM. Datadog runs at about $4B+ (Q1 revenue was $1,006M). Grafana has $600M ARR. Cribl has $300M+ ARR.
- **Old assumption:** humans read dashboards, and indexing at write time is worth it.
- **Why AI breaks it:** agent readers scan, not look up. Volume tracks code generation, not headcount.
- **New category:** an agent-first telemetry lake with reader-driven retention.
- **Product:** "Point OTel at your own S3. Our agent tells you which 70% of telemetry nobody ever uses, and answers incidents for $X each, capped."
- **Buyer:** VP Infrastructure / Head of Platform, with the CFO as co-signer.
- **Pain:** a Datadog renewal that grows faster than revenue.
- **Evidence:** items 1-13 above.
- **Workaround:** Cribl routing, Flex Logs, sampling, ClickStack or Grafana migrations.
- **Competitors:** see the table. Direct: Tsuga, ClickStack, Coralogix, OpenObserve, Grafana. Adjacent: Resolve, Traversal, Bits.
- **Why incumbents may lose:** per-GB revenue sits at the core of Datadog and Splunk. *Weakened:* Datadog can add per-investigation fees on top, and the cheap-store vendors have no dilemma at all.
- **Wedge:** a retention audit. Replay 90 days of investigations and show which data was never read.
- **Integration:** hours for dual-write, months for full migration.
- **30-day pilot:** mirror the noisiest cluster, replay 10 incidents, and compare cost and answer quality.
- **Pricing:** $/TB in the customer's bucket (near zero) plus $/investigation with a monthly cap.
- **Expansion:** SIEM logs, an AI SRE, and remediation.
- **Moat:** 10 customers: none. 100: an investigation-usage corpus that tunes retention. 1,000: the default store for third-party agents (contested by ClickHouse and Snowflake).
- **$10B case:** a 2027 renewal crisis forces re-platforming and this becomes the agent-era default. The probability is low given who already holds the cheap stores.
- **CTO one-liner:** "Only pay to keep the telemetry your agents actually read."

### Revised scores

| Mkt | Transf | Urg | Why-now | Reach | Pilot | Integ | Opening | Diff | Expand | Moat | VC | **Avg** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 9 | 6 | 5 | 6 | 6 | 7 | 6 | 2 | 3 | 7 | 3 | 3 | **5.3** |

Changes from the 6.7 baseline:
- Transformation 7 to 6: incumbents absorbed the agent-reader shift.
- Urgency 7 to 5: renewals are painful but Datadog NRR holds in the low 120s.
- Opening 4 to 2: Tsuga, ClickStack, Coralogix, Observe and Chronosphere are each already funded or acquired.
- Differentiation 4 to 3.
- Moat 5 to 3.
- VC 6 to 3: the vintage has already been funded and exited.

## Verdict

**KILL** (5.3, well below 8.5). Add it to STATUS as "Telemetry for machine readers: agent-native/per-GB-breaking observability. Datadog MCP GA with 22x MCP calls and NRR low-120s; Grafana Assistant (18k orgs, $600M ARR); ClickStack plus Langfuse; Snowflake-Observe; PANW-Chronosphere $3.35B; Coralogix $1.6B; Tsuga $35M in-customer-cloud AI-native. The only unowned piece is per-investigation pricing, which is a tactic, not a moat."

**Residual idea to keep (not a thesis on its own):** reader-driven retention, meaning keep only the telemetry agents actually use. This is a feature that an AI SRE (Resolve, Traversal) or a pipeline (Cribl) will ship. It should not be pursued as a company.
