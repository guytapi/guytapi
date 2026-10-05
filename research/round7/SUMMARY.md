# Round 7 summary (founder's pain-first method)

5 slices mined from practitioner sources (GitHub issues/PRs, HN, engineering blogs; Reddit and direct fetch blocked by the environment's network policy). ~33 candidate problems scored. One deep dive.

| Best problem per slice | Avg | Why it fails |
|---|---|---|
| Model retirements break production agents (deep-dived, M) | 5.5 (from 6.5) | rightmodeler, ZenML Kitaru, Datadog replay, LangWatch; free provider tools (AWS Transform, Foundry, Anthropic migrate); no WTP evidence |
| Agent-written test suites rot (Linear +2,000 tests/week; Anthropic tests 10x) | 6.3 | Not a budget line yet; Trunk/Datadog/Launchable one feature away |
| CI capacity/cost explosion (Anthropic CI jobs 25x) | ~6 | Depot, Blacksmith, WarpBuild, Tenki, Launchable |
| Secrets leaking into agent transcripts/traces | 5.9 | GitGuardian and Anthropic natural owners; 4+ OSS scrubbers |
| Prompt-cache regressions (10x cost spikes) | 5.6 | Gateways/observability show hit rate; provider may return miss reasons |
| MCP tool-surface drift / OAuth for parallel agents | 5.5 / 4.9 | Client bugs being fixed; Auth0, Nango, Composio, Arcade, MCPJam |

## Finding
The founder's hypothesis (look for pain solved with homegrown scripts) holds partly: homegrown tooling is everywhere. But in agent infra, loud public pain is matched within weeks by (a) open-source tools, (b) a platform fix, or (c) a feature in an existing vendor. The pains found are real but feature-sized.

## Next step (round 8)
Mine "we built this internally" engineering posts from AI-native companies: if 5+ companies independently built the same internal system in 2026, that is the strongest product signal.
