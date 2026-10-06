# War Room Status (2026-10-05)

**Result so far: no idea has cleared the bar. ~55 theses deep-dived across 19 rounds plus an evidence audit and a failure taxonomy; ~130 problems rejected at scan level. Highest after deep dive: 6.9.**
The search continues; this file is the scoreboard.

## Scoreboard (all deep-dived theses)

| # | Thesis (one sentence) | Round | Avg /10 | Cause of death |
|---|---|---|---|---|
| A | Make B2B suppliers sellable to AI buyer agents | 1 | 5.4 | No agent orders yet; Salesforce/commercetools/TradeCentric absorb plumbing |
| B | FinOps for AI spend | 1 | 5.6 | Ramp, Anthropic/Cursor/Copilot native caps, Vantage, ServiceNow |
| C | Ctrl-Z for agent actions | 1 | 4.6 | 5 backup vendors shipped it; Rubrik ~15 paying customers |
| F | Secure employee-built AI apps | 1 | 5.7 | Lovable/Replit ship governance; Pluto, Red Access, Zenity |
| R1 | QA for robot brains | 2 | n/a | ~300-600 buyers; fleets too small in 2026 |
| R2 | Data-center commissioning readiness | 2 | n/a | ~8 hyperscalers + 100-200 developers |
| R3 | Deployment OS for FDEs | 2→4 | 4.6 | Sierra/Decagon in-house; Auctor, Rocketlane, June funded |
| R4 | AI applications engineer for custom equipment | 2 | n/a | Atira (Accel), Korso, Uptool |
| T1 | Flight simulator for agents | 3 | 5.1 | Arga Labs (GC), Google/Salesforce native sims |
| T2 | Auditor of outcome-priced AI work | 3 | 4.7 | Small spend; Zendesk self-verifies; Vaudit |
| T3 | Autonomous merge for AI code | 3 | ~5.6 | GitHub/Cursor/Greptile shipped it Sep 2026 |
| T4 | Stripe for agents using SaaS | 3 | 4.5 | Cloudflare, Frontegg, Okta, Stripe/Metronome |
| E1 | Capacity-charge autopilot | 4 | 6.5 | 15-year-old DR category |
| S | Speed to power | 4 | 4.5 | PG&E Flex Connect 5 customers; Critical Loop; Tibo |
| V | AI vuln-response for vendors | 4 | 5.7 | HackerOne H1 Remediation; frontier labs; Aikido/Root |
| P | CRA product-security team | 4 | 4.8 | Exein $1.7B; ONEKEY/Finite State agents; low WTP |
| N | Supplier AI negotiator | 4 | 4.0 | Tail spend only; suppliers like bots; AB 325 risk |
| X | SOX controls for AI agents | 5 | 4.0 | Optro/Pathlock own it; SEC shrinking 404(b) |
| T | Agent toll router | 6 | 3.9 | Tolls not live; flat-fee ELAs; SAP bans copies |
| + | ~6 more killed at scan level (env. compliance, dealer service ops, 3PL ops, AI hardware supply chain, brand agent OS, AI continuity) | 5-6 | n/a | Crowding / small / fails "exciting" filter |

**Highest average reached: 7.1 (speed to power, before deep dive). Bar: 8.5 with no category below 7.**

## Structural conclusions
1. **AI-tooling gaps visible in public sources get funded within ~6 months** (Oct 2026), and platforms ship the obvious control layer. Every "control/visibility over AI" idea died this way.
2. **Pain and competition are inversely correlated in desk research**: the more evidence of pain we find online, the more startups have already found it too.
3. **"Future" ideas that are uncrowded are pre-demand** (agentic commerce, agent tolls, robot fleets, agent reputation).
4. Ideas that pass the competition filter tend to be in dull verticals (env. compliance, dealer service), which fails the founder's "interesting / easy for VCs" filter.

## Implication
Public-source research alone is unlikely to produce an idea that scores ≥8 on both "pain" and "competition position". The likely route to a winner is **proprietary insight**: founder access to a specific buyer group, or data from real customer conversations that public sources don't show. The research continues, but the founders should run the 14-day tests on the two or three best near-misses in parallel.

## Rounds 7-8 (founder's pain-first method)
| Thesis | Avg | Cause of death |
|---|---|---|
| Q. Supplier product-data network | 4.6 | Assent ($1.3B) already sells supplier-side "answer once" + AI Request Manager; ~$55K/yr pain |
| M. Model migration autopilot | 5.5 | rightmodeler, ZenML Kitaru, Datadog replay, LangWatch; free provider tools |
| Test-suite steward (agent-written test rot) | 6.3 | Not a budget line; Trunk/Datadog/Launchable one feature away |
| Minions-in-a-box (background coding-agent platform) | 5.7 | 14+ companies built it in-house, but Ona/Cursor/Codex/Devin/Tembo/Open-Inspect sell it |
| In-loop verification judge | 5.5 | Real gap, feature-sized |

**New lesson (round 8):** agent platform teams at large companies now have real budgets. Any infra idea must pass "could that team build it in a sprint?". All 13 internal system types found fail it.
| R. Applied Intuition for robots (policy eval) | 5.5 | Applied Intuition Dana (Jul 2026), NVIDIA Isaac Lab-Arena free, One Robot (YC/Accel), Robocurve, Instance |
| G. Source control built for agents | 5.5 | Best-documented pain of all (GitHub 30x redesign, 257 incidents/yr). Pierre $23M (Lovable, Bolt), Cloudflare Artifacts, Entire (ex-GitHub CEO, $60M seed) mirror, Cursor Origin forge |

**Lesson (G):** when an incumbent's infrastructure failure becomes public, specialist money arrives within weeks; by the time it reaches newsletters, the space is funded.

## Round 9
| Thesis | Avg | Cause of death |
|---|---|---|
| H. Human decision layer (cross-vendor approvals/control tower) | 4.5 (orig bar 4.9) | HumanLayer deprecated its approvals SDK and pivoted; auto-approval native (Claude Code auto mode default Aug 14, Ramp Policy Agent, GitHub managed permissions Sep 9, Copilot Studio); cross-vendor routing in UiPath Action Center, ServiceNow AI Control Tower, Credal, Runlayer |

## Round 10
| Thesis | Avg | Cause of death |
|---|---|---|
| I. AI supply integrity / model-substitution attestation | 4.6 (orig bar 4.4) | Artificial Analysis Endpoint Accuracy Index (Aug 2026), Vals ($40M a16z), LMArena ($1.7B) own the neutral index; OpenRouter Auto Exacto and Kimi Vendor Verifier police resellers; confirmed harm is consumer (Anthropic/Perplexity class actions) or open-weight, with no B2B SLA disputes found; black-box proof is weak on closed APIs (no logprobs, quantization detection at chance, GhostPrint spoofing); TEE attestation is going native |

## Rounds 9-11
| Thesis | Avg | Cause of death |
|---|---|---|
| K. Carfax for GPUs | 4.4 | Silicon Data ($30.5M, CME futures), American Compute appraisals, NVIDIA Fleet Intelligence + residual guarantees |
| H. Human decision layer for agents | 4.9 | Built into Claude Code/Ramp/GitHub/Copilot; UiPath Action Center; HumanLayer pivoted away |
| What breaks next (tenant API replica) | 6.4 | Same as T; incumbents fix strain within the quarter |
| I. Model integrity attestation | 4.4 | Consumer-side harm only; Artificial Analysis, Vals AI; TEEs make it native |
| VMware estate exit | 6.2 | "Destination subsidy": Red Hat/AWS/Nutanix give migration free |
| L. AI-native PLM | 4.8 (from 7.1) | Flow Engineering ($50M, Sequoia, $750M), SPREAD AI, CADDi; all incumbents shipped agents |

**Lessons:** (1) "destination subsidy" kills migration plays; (2) AI-native money goes first to layers that avoid migration, not to new systems of record.

## Round 12
| Thesis | Avg | Cause of death |
|---|---|---|
| W. Formally verified AI code | 3.8 | Axiom ($1.6B), Harmonic ($1.45B), Theorem, AWS Kiro; spec inference unsolved |
| Z. Cross-channel agent-era trust (built on Vara's existing components) | 5.6 REFRAME | Pindrop BotStopper (Sep 2026) + AI voice consortium; DataDome/HUMAN/Kasada; buyers buy per channel |

**Best wedge for these founders (not a winner, 14-day test only):** caller-verification + step-up API for AI voice front-doors (telecom/MVNO port-out & SIM swap, travel loyalty), sold direct and as a `verify_caller` tool inside Vapi/Retell. Uses all four existing Vara components. Expected ceiling $10-30M ARR unless it expands.
| A2. Living evidence-backed system map (built on Vara Architecture) | 5.7 REFRAME | Apiiro (material-change PR detection, AI threat modeling), Endor, Wiz Code; free DeepWiki/Code Wiki; platform team builds 70% in weeks |

**Founder-edge wedges to test with real customers (neither is a winner):**
1. Caller verification for AI voice front-doors (telecom/travel) — see round12/14_DAY_TEST_PLAN.md.
2. System-level security & compliance diff of agent PRs for regulated mid-market fintech/healthtech (50-500 engineers): replay 100 past PRs at 2 design partners; pass = 3+ unknown findings each and 2 verbal $25K+ commitments.

## Round 13
| Thesis | Avg | Cause of death |
|---|---|---|
| Forming categories via top-tier seeds (best: AI attacker emulation 6.5, plant shift engineer 6.2) | ≤6.5 | Once a top-tier round is public, the category has a leader |
| AA. AI-attacker readiness | 5.5 | Strongest why-now of all; Horizon3 ($2B+, ~7K customers), XBOW, Pentera, Adaptive, Doppel; ~$680M raised in 11 months |

**Note:** the AA helpdesk-impersonation test is folded into the round-12 caller-verification wedge as its sales motion (attack → deploy verify_caller → re-test).
| Fraud layer for AI companies (free-tier/GPU abuse) — scan only | n/a | Real pain (7.4% of AI-company signups multi-account abuse; 6.2x growth), but Stripe Radar abuse prevention, Castle, WorkOS Radar, ShieldLabs already sell it |

## Evidence audit + KYI
- Audit: 46 kills reviewed; 31 STRONG, 4 MIXED, 9 WEAK. Partial false negative: proof-of-origin + Vara AML stack, reframed to customs brokers (7.5 at audit).
- KYI (know-your-importer for customs brokers, EO 14411): deep dive 6.8. Trigger verified but narrower (CTPAT brokers, foreign importers only) and Nov 30 is a rulemaking deadline, not compliance. Market small (US brokerage revenue ~$5.5B). GingerControl, Gaia, Veroot, Descartes a feature away.
- Surviving version: "Highway for importers" — shared importer-identity network across brokers → sureties → EU platforms (EU deemed-importer liability 2028). 14-day test: LOIs from 2 brokers + 1 surety at $20K+, 3 brokers agree to shared matching, back-test finds 5+ high-risk importers.

**Lesson:** look for new regulatory liability placed on intermediaries; this was the one area where a 4-month-old mandate still had no purpose-built vendor.

## Round 14 (intermediary liability mandates)
21 mandates scanned. Best: telco scam-liability evidence system under Australia's Scams Prevention Framework (6.6; AU market ~A$7.6M; venture-scale only as cross-sector claims clearinghouse), US voice-provider vetting under FCC proposed rules (6.2; rule not final). Liability on few giants gets absorbed in-house; liability on many small firms draws generic compliance vendors before go-live.

## Round 15
| Thesis | Avg | Cause of death |
|---|---|---|
| PLG mass-market scan (best: share button for AI-built tools 7.1, agent pick rate 7.0) | ≤7.1 | Bottom-up utilities get built by platforms/YC in a sprint |
| Europe/Israel gaps (best: sovereignty exposure graph 7.0) | ≤7.0 | EU compliance startups fill gaps in 6-12 months; EU base = distribution, not moat |
| P2. Search Console for being chosen by coding agents | 6.3 | Strongest why-now (Vercel >50% deploys by agents, Neon >80% DBs by agents) but Lightsage ($4M, Nexus, Sep 8), Amplifying, Armature, free Netlify AXIS; labs sell placement (OpenAI Sponsored Agents) |

## Round 16 (first-principles synthesis)
20 theses generated, 8 checked, 7 killed. Best: "UL for human training data" (behavioral-biometric proof of expert authorship + cross-vendor ban network for AI data vendors like Mercor/Surge/Scale) at 6.9 — fails market size (~$50M today), ROI clarity, access. Lesson: shared-data networks survive only where vendors are fragmented and a few concentrated buyers can mandate participation.

## Round 17 (analyst categories, earnings calls)
Best: capture-time provenance for warranty/claims evidence (6.5-6.7, found independently for the third time), data-contract enforcement (5.8). Lesson: analyst-named categories are already funded; earnings calls are a weak source of AI pain.

## Round 18 (founder's new method: failure taxonomy + 35 first-principles theses)
See round18/FAILURE_TAXONOMY.md and THESES_35.md. 6 survivors, all killed:
| Thesis | Avg | Cause of death |
|---|---|---|
| AI deflation capture (SaaS rebuild + services contracts) | 6.0 | Sourcing advisors (ISG, UpperEdge, IDC) sell it on contingency; one-time revenue |
| ProsperOps for AI commitments | 5.2 | AI spend counts against cloud commits; AI commitments non-transferable; Flexera bought ProsperOps |
| Agent-speed procurement | 5.4 | Zip, Vanta, Runlayer, Microsoft Agent 365 cover each piece |
| Agent-polluted product analytics | 5.2 | Snowplow, GA4, PostHog, Contentsquare; agents ~6-7% of logged-in activity |
| Commitment ledger for customer-facing agents | 4.6 | Decagon Watchtower, Fin Monitors, Oversai, Isara; small dollars |

## Round 19 (weak signals from round 18 kills)
| Thesis | Avg | Cause of death |
|---|---|---|
| Agent-provisioned resource sprawl | 4.8 | Big numbers are platform-owned DBs; Wiz, Nudge, Vercel EMU, Stripe Projects caps |
| AI outbound TCPA consent | 5.0 | DNC.com MCP server, PossibleNOW, Gryphon, ActiveProspect; legal pressure easing |
| AI notetaker transcript liability | 5.3 | Teams/Meet/Zoom block bots by default; Purview; Theta Lake, Nudge |

**Lesson:** even victim-side and CFO-side problems are covered when they are publicly visible. Next: deliberately target outcome B (too early for public evidence, precise 14-day test).

## Round 20 — first finalist under outcome B (conditional)
**Counter-signature for machine-to-machine deals** (round20/outcome_B_candidates.md): an independent, auditor-grade record of who had authority, what terms bound both sides, and what was delivered, for supplier commitments made by agents across Keelvar, Pactum, Fairmarkit, Coupa and Ariba.
- Qualifies as **outcome B** (genuinely early, no product sold yet, precise 14-day test), **not A** (6.5 on current evidence; estimated 15-20% chance the test passes).
- Verified independently: AAA Legal Context Protocol (Jun 2026, Google/IBM/Circle/Integra Ledger); Keelvar reports ~71% of sourcing events run by AI agents. Supplier-side agent events (~1,420/month) come from Keelvar's white paper (search snippet).
- Biggest threats: DocuSign (Deputy GC published the thesis Aug 27, 2026), buyer platforms' native ledgers, Integra Ledger productizing LCP.
- Other B candidates failed: agent credit bureau (Experian Agent Registry, Visa/Mastercard/Ant KYA), supplier bid agents, B2B machine-customer front door, transferable AI capacity.

## Round 21
| Thesis | Avg | Cause of death |
|---|---|---|
| H2. API for agents to hire verified humans | 5.0 | RentAHuman (160K humans, 81 agents), 10+ horizontal players; Upwork/DoorDash/Uber open supply to agents directly |
| E. Horizontal proof-of-capture (4th independent appearance) | 5.8 | Truepic already horizontal with a cross-company Risk Network; Captur, Vaarhaft, Switch Labs at the cheap end; Apple Reference Image and Pixel C2PA make capture signing native |

**Lesson:** an idea surfacing repeatedly from independent directions means the pain is real, not that the space is open; here it meant a funded horizontal incumbent already existed.

## Round 22
| Thesis | Avg | Cause of death |
|---|---|---|
| B+. System of record for everything agents agreed to | 4.5 | Stripe Projects logs ToS acceptance; WorkOS auth.md consent records; ConductAtlas/Nudge track terms; Okta/Keycard authority; pre-demand, ~tens of new agreements/company/month. Original B finalist remains stronger (6.5). |

## Round 23 (weird directions)
15 theses, 10 checked, 9 killed (ops-data licensing brokers, call-center real estate, payroll-rated insurance, AI-code provenance for M&A, inter-company agent workflow marketplaces, AI escrow, CU agent pooling, on-prem inference boxes, OSS triage). Weak B survivor (6.2, ~10-15% test-pass odds, outside founder edge): clearing network for stranded transformer/switchgear inventory and factory slots from delayed data-center projects.

## Round 24 (exploding OSS without a company)
22 repos created after Jun 1 2026 have >15K stars; nearly all are coding-agent add-ons ("coding agent as general work engine"). Ten clusters mapped, all killed: codebase knowledge graphs (Graphify YC S26), token minimization, skills (Tessl), agent-made design/video, CLIs for API-less apps (Amazon WorkSpaces for agents, UiPath), local inference/voice, watermark stripping, agent memory, open decision models (TypeSafe Jev $40M seed). Lesson: OSS star spikes now lag too — viral repos are often the open alternative to an already-funded launch.

## Round 25 (problems for platforms when agents act inside logged-in sessions)
All killed (best 4.9). Liability moved to the user (Ninth Circuit, Aug 4 2026; agent ToS); fixes belong to agent vendors (Atlas patches, BrowseSafe); remaining needs map to crowded/killed categories (Visa/Mastercard Verifiable Intent, Prove, HUMAN, BioCatch, Chargeflow/Forter). Comet ran only ~185K sessions on Amazon.com by Jun 15.
