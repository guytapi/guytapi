# Failure Taxonomy (16 rounds, ~45 deep dives, ~100 scan-level kills)

## 1. Clusters by real cause of death

| Cause of death | Share | Theses that died this way |
|---|---|---|
| **F1. Platform absorption** — the system that generates the data/behavior ships the control as a feature | ~30% | B AI spend (Ramp, Anthropic caps), C agent undo (Rubrik/Veeam), F citizen apps (Lovable/Replit), T1 agent sim (Google/Salesforce), T3 autonomous merge (GitHub/Cursor), H human decision layer (Claude Code auto mode), X SOX for agents (Optro/Workday), M model migration (AWS/Foundry/Anthropic migrate), T agent toll router (vendors meter themselves), test-suite steward |
| **F2. Visible-pain race** — pain was public (newsletters, HN, outage), specialists funded within weeks | ~25% | G source control (Pierre, Entire), V vuln response (HackerOne), AA AI attacker (Horizon3, $680M in 11 mo), P2 agent pick rate (Lightsage 4 weeks earlier), K GPU residual (Silicon Data), W verified code (Axiom, Harmonic), L AI PLM (Flow Engineering), R robot eval (Applied Intuition Dana) |
| **F3. Pre-demand future** — directionally right, no budget today | ~15% | A machine buyers, T agent tolls, N supplier negotiator, agent reputation, robot fleet ops, agent-to-agent contracts |
| **F4. Small or shrinking TAM** — real wedge, ceiling < $100M ARR | ~15% | R2 commissioning, S speed to power, KYI customs brokers, Q supplier data, Z caller verification, UL for training data, AU scam evidence |
| **F5. Feature, not company / sprint-buildable** — a platform team builds it in a sprint | ~10% | D FDE deployment OS, in-loop judge, Minions-in-a-box, prompt-cache regressions, MCP drift, AGENTS.md drift |
| **F6. Destination subsidy** — the vendor winning the workload gives it away | ~5% | VMware exit, CPQ rebuild, all forced migrations |

## 2. Assumptions that repeatedly produced false positives
1. **"Loud pain = opportunity."** Loud pain is a lagging signal; by the time we can find 5+ public complaints, funding has happened.
2. **"Neutral cross-vendor layer beats the platform."** Neutrality only wins when customers are forced to be multi-vendor *and* platforms are conflicted. Most buyers accept the platform's native control.
3. **"Controls/visibility over AI is a category."** It never was: it is always one release from the vendor that runs the AI.
4. **"Regulation creates a budget."** Only when liability lands on many mid-size firms *and* no generic compliance vendor reaches them first; mandates on giants are absorbed in-house.
5. **"Analog of a $10B cloud-era company."** The analog slot is usually filled by the incumbent extending itself (Applied Intuition, Okta, Stripe).
6. **"AI makes X 10x cheaper, so build the AI-native X."** Ignores that incumbents ship the same model capabilities; only works where the incumbent's business model is threatened by doing so.

## 3. Systematically under-explored areas
- **Economic second-order effects on non-AI companies** (what happens to the SaaS budget, the services budget, the hiring budget when agents work) — we looked at AI tooling, not at money moving.
- **The buyer is the CFO, not the CTO** — almost every thesis targeted engineering/security buyers who have the most vendors pitching them.
- **Problems created for the *victims* of agent behavior** (businesses receiving agent traffic, promises, purchases, content) rather than for agent operators.
- **Liability created by what agents say and promise**, not by what they execute.
- **Build-vs-buy inversion**: companies replacing purchased software with agent-built software.
- **Commitment and capacity markets** for AI compute (pricing tiers, reserved throughput), as opposed to spend visibility.
- **Humans as a scarce input that agents must procure** (verification, physical presence, judgment).

## 4. Search constraints for round 18 onward
1. **No control/visibility layer over AI** unless the platform is structurally prevented from shipping it (conflict of interest or multi-party data).
2. **Reject if 3+ public complaints already have a funded startup**; prefer weak signals and inferred second-order effects.
3. **Prefer buyers outside engineering** (CFO, COO, GC, procurement) or problems where the *counterparty* of agent behavior suffers.
4. **Require a reason the incumbent will not act** (cannibalization, conflict, or it is not their customer), not just "they haven't yet".
5. **Require a $100M ARR path without owning the whole niche** (≥5,000 buyers at ≥$25K, or usage-based on a growing flow).
6. **Ban migrations and one-time projects** unless they convert into a recurring system of record.
7. **Every survivor needs a 14-day test that produces money, data access or a signed pilot**, not opinions.
