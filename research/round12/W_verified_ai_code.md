# Thesis W: Verified AI code ("AI writes code faster than humans can review it. We mathematically prove it's correct.")

**Date:** 2026-10-05 | **Round:** 12 (lens: hard technical problems where difficulty is the moat) | **Method:** round7/METHOD.md template + original bar + simulated buyers + VC committee + red team | **Searches used:** 35 of 40 (WebFetch/Reddit blocked, so evidence comes from search snippets).

Legend: [S] = source found in search results this round. [U] = unverified or estimated. [I] = my inference from sources.

**Thesis under test:** LLMs + proof assistants/SMT (Lean, Dafny, Verus, Kani, TLA+, Z3) infer specs from intent, tests and docs, then prove properties of code changes (or find counterexamples). Wedges: (a) proof-carrying migrations (prove migrated code behaves identically), (b) verified critical paths for non-bank fintech and infra companies, (c) a verification gate on agent PRs that touch critical code.

**Bottom line (up front): KILL.** Difficulty is a moat against small teams, but not against the people already in this market. The space has **over $600M of specialist capital** in it, plus every frontier lab and AWS:
- **Axiom Math:** $64M seed, then a $200M Series A at $1.6B (Mar 2026). Its pitch is literally "prove AI-generated code safe".
- **Harmonic:** $295M raised, valued at $1.45B, pre-revenue.
- **Theorem** (YC S25, Khosla, $6M): "stop AI-written bugs before they ship", including legacy code migration.
- Also Logical Intelligence (Yann LeCun on its research board), Pramaana Labs ($27M), Lanyon ($10.6M), Athanor and Axiomatic.
- **AWS** shipped SMT-backed requirements analysis and property-based "spec-to-code" checks in Kiro (May 2026). **Mistral** open-sourced a Lean code-proving agent (Leanstral, Mar 2026). **DeepMind** is hiring for "Verified Code Generation … for large real-world software projects".

Demand outside crypto and hyperscaler internals is still mostly a narrative. The best-known "AI code outage" (Amazon, Mar 2026) was disputed by Amazon, and the fix it reached for was **senior human sign-off, not proofs**. Harmonic is pre-revenue at $1.45B, and Axiom names no code-verification customers. This hits both standing killers at once: **crowded at the top, pre-demand at the bottom.** The work is also **services-heavy** (spec writing), which caps a seed-stage entrant's margins.

---

## 1. Problem
- AI agents now write a large share of production code. Human review does not scale with that volume, and tests only sample behavior.
- Classic formal verification gives guarantees but has cost about 10-100x the engineering effort. Theorem's founder cites "fifteen man-years" for one verified code generator [S](https://www.ycombinator.com/founders/jason-gross).
- The thesis: LLMs collapse the cost of writing specs and proofs, so proofs become a viable review substitute for critical code.

## 2. Recent evidence

### 2a. Technical state of the art (is it production-ready?)

| # | Signal | What it says | Source |
|---|---|---|---|
| 1 | **Vericoding benchmark** (MIT/Tegmark group, Sep 2025; POPL/Dafny 2026): 12,504 specs. Off-the-shelf LLMs succeed on **82% in Dafny, 44% in Verus/Rust, 27% in Lean**. Pure Dafny verification rose from 68% to 96% in a year | Fast progress, but on small, **given** specs. The spec is supplied, not inferred | [S](https://arxiv.org/abs/2509.22908v1) |
| 2 | **ATLAS** (Dec 2025): synthesized 2.7K verified Dafny programs; a fine-tuned 7B model gains +23pp on DafnyBench | Training data for verified code is being mass-produced, so it is not a moat | [S](https://arxiv.org/html/2512.10173v1) |
| 3 | **Heimdall** (May 2026): LLM translation of eBPF C to Rust, with Z3/symbolic-execution equivalence proofs for **96 of 102 programs (94%)** | Proof-carrying migration works on **small, pure, bounded** programs. eBPF is a best case | [S](https://arxiv.org/pdf/2605.25411) |
| 4 | VERT and LAC2R: C-to-Rust translation with bounded equivalence checking (Kani) or fuzzing-based equivalence | Mostly "bounded" or "tested", not full proofs | [S](https://themoonlight.io/de/review/vert-verified-equivalent-rust-transpilation-with-large-language-models-as-few-shot-learners) |
| 5 | **AlphaProof Nexus** (DeepMind, May 2026): Gemini 3.1 Pro + Lean solved 9 Erdős problems and 44 OEIS conjectures at a few hundred dollars each | Math proving is solved-ish at the frontier. Labs own the prover | [S](https://winbuzzer.com/2026/05/26/google-deepmind-says-alphaproof-nexus-is-still-not-agi-xcxwbn/) |
| 6 | DeepMind research role "Verified Code Generation": Lean proofs, formal specs and verified static analysis "for large real-world software projects" | A frontier lab is explicitly targeting this thesis | [S](https://www.analyticsinsight.net/artificial-intelligence/googles-new-formal-verification-framework-targets-safer-ai-development) |
| 7 | **Mistral Leanstral** (Mar 16, 2026): Apache-2.0, 119B MoE Lean 4 agent that writes code and proves it meets its spec | The prover layer is becoming open-source and commoditized | [S](https://mistral.ai/news/leanstral) |
| 8 | **AWS at scale:** a Dafny-built authorization engine (1B calls/s) deployed in 2024 after 4 years of work. AWS still ran **10^15 production-sample differential tests** before deploying. Cedar is verified in Lean with "verification-guided development" | Production-grade verification exists, but it is hyperscaler-internal, took years, and was still backed by massive testing | [S](https://www.amazon.science/publications/formally-verified-cloud-scale-authorization), [S](https://lean-lang.org/use-cases/cedar/) |
| 9 | **Spec bottleneck** remains unsolved. Verus-SpecBench: "no guarantee that the formal spec itself matches the user's intent". The 2026 survey names the "translation bottleneck, verifier tax, scalability gap" | The core claim "infer specs from intent" is the unsolved part | [S](https://arxiv.org/pdf/2608.14590), [S](https://benchmarklist.com/benchmarks/verus_specbench/) |
| 10 | Kleppmann, "AI will make formal verification go mainstream" (Dec 2025), 467 HN points | The developer community has bought the narrative. The same story is pulling in money for every entrant | [S](https://martin.kleppmann.com/2025/12/08/ai-formal-verification.html) |

**Verdict on readiness [I]:** It is production-ready for **small, pure, spec-given** code (crypto primitives, parsers, eBPF, authorization engines). It is **not ready for ordinary enterprise code**: ORMs, network I/O, distributed state, framework magic and implicit specs. On realistic Verus/Lean tasks the success rate is 27-44%, even before the spec has to be inferred. The thesis can work for codebases that look like AWS's authorization engine or Jane Street's, but not for a typical fintech's Django or Node monolith.

### 2b. Demand

| # | Signal | Strength | Source |
|---|---|---|---|
| 1 | Amazon, Mar 2026: a 6-hour ecommerce outage. Reports tied incidents to AI coding tools, and a Kiro-caused 13-hour AWS outage was reported for Dec 2025 | Strong headline. But **Amazon disputed it**: "none involved AI-written code". The guardrail was **senior sign-off**, not formal methods | [S](https://oecd.ai/en/incidents/2026-03-10-01aa), [S](https://www.techradar.com/pro/amazon-is-making-even-senior-engineers-get-code-signed-off-following-multiple-recent-outages) |
| 2 | AWS response: Kiro Requirements Analysis (SMT on specs; 60% of first-draft requirements needed refinement) plus property-based testing for "spec-to-code alignment" | The demand is real enough that **the platform absorbed it inside the IDE** | [S](https://thenewstack.io/kiro-requirements-analysis-automated-reasoning/), [S](https://www.geekwire.com/2026/aws-targets-ai-slop-with-new-spec-check-in-kiro-coding-tool-amid-scrutiny-of-agent-reliability/) |
| 3 | Antithesis: $105M Series A led by **Jane Street (a customer)**, pitched as "AI accelerates code volume; traditional testing cannot keep pace" | Willingness to pay for **better testing** is proven. Buyers chose deterministic simulation over proofs | [S](https://pulse2.com/antithesis-105-million-series-a/) |
| 4 | Certora: blue-chip DeFi clients (Aave, Uniswap, Lido…), "$100B TVL", and the team grew 4x to 40 experts (25 PhDs) in 2025 | WTP for proofs exists where **one bug = $ millions, irreversibly** (crypto, which is excluded). The model is expert services | [S](https://www.certora.com/blog/momentum-for-2026), [S](https://en.cryptonomist.ch/2026/01/20/certora-security-defi-risk-2025/) |
| 5 | Logical Intelligence: "early commercial traction is in the crypto space" | Even the code-proof specialists find buyers mainly in crypto | [S](https://pebblebed.com/portfolio/logical-intelligence) |
| 6 | Harmonic: pre-revenue at $1.45B (Feb 2026). Axiom: no named code customers. AXLE is a free Lean verification API | The best-funded players have not shown enterprise code-verification revenue | [S](https://sacra.com/c/harmonic), [S](https://axiommath.ai/research/releasing-axle) |
| 7 | Theorem: users "found zero-days in GPU accelerated code and cryptography implementations, and sped up code migration in legacy systems" | Real but narrow, high-assurance buyers (GPU kernels, crypto) | [S](https://www.ycombinator.com/launches/NZA-theorem-ai-coding-that-is-trustworthy-by-default) |

**Assessment:** Demand for "fewer AI-code bugs" is real. Demand for **proofs** outside crypto and hyperscalers is not visible. Buyers pick (1) human sign-off, (2) better testing (Antithesis, property-based testing in Kiro) and (3) the platform's own spec checks. No practitioner thread was found where a non-crypto, non-hyperscaler company said "we need proofs and would pay" [U]. The HN thread is enthusiasm from engineers, not purchase intent from buyers.

## 3. Who has the pain
- **Real buyers today:** crypto/DeFi (excluded); hyperscalers (build in-house: AWS ARG, Microsoft Verus, Google); HFT/quant (Jane Street uses Antithesis and OCaml tooling); GPU kernels and crypto libraries (Theorem's niche); chips/RTL (Athanor, Axiomatic).
- **Hoped-for buyers:** VP Eng or Head of Platform at non-bank fintech (payments processors, BNPL, payroll), plus infra/IaC owners. Rough count: about 500-1,500 companies with a critical module worth >$100K/yr to protect [U].

## 4. What they do today
- Code review (now with AI reviewers), unit, integration and property-based tests, and fuzzing.
- Shadow/differential testing for migrations; for AWS this was **even alongside Dafny proofs**.
- Antithesis-style simulation, staged rollouts and feature flags.
- Senior sign-off on AI changes (Amazon).
- Formal methods only where an in-house team exists: AWS ARG (decade old), Cedar, s2n.

## 5. Why current products fail
- Tests sample behavior, while proofs cover it fully. But proofs need specs. Nobody writes specs, and LLM-inferred specs can be silently wrong (Verus-SpecBench).
- Proof tooling (Lean, Verus) does not cover real enterprise stacks: Python, TypeScript, Java with frameworks, DBs and network side effects. Dafny and Verus cover a subset of Rust, or require writing code in Dafny.
- **Net [I]:** this gap is precisely what $600M+ of specialists and several labs are trying to close. A new seed company has no structural edge.

## 6. Why now
- Vericoding success rates jumped in 12 months (Dafny 68% to 96% on pure verification).
- Open provers (Leanstral, Kimina, DeepSeek-Prover class), cheap Lean APIs (AXLE, free) and AI-code volume.
- **But "why now" is also why everyone else is here**: the market saw it in 2025, and money arrived from Sep 2024 (Harmonic A) through Mar 2026 (Axiom A), then Jun-Aug 2026 (Pramaana, Athanor, Lanyon).

## 7. Potential product
- **(a) Proof-carrying migration:** run old and new code side by side, LLM-guided equivalence proofs (symbolic execution + SMT + Kani), counterexample reports and an equivalence certificate. This is the strongest wedge, because **the old code is the spec**, so no spec inference is needed.
- **(b) Verified critical paths:** infer invariants for payments or ledger modules (double-entry balance, idempotency, no negative balances) and re-prove them on every PR.
- **(c) Agent-PR verification gate:** a CI check that blocks agent PRs touching annotated critical modules unless the properties re-verify.

## 8. Time to value
- (a) Weeks per migration unit, if the code is pure and bounded. Months if it is I/O-heavy (most enterprise code). [I]
- (b) Spec elicitation alone is 2-6 weeks of expert time per module [U]. This is the services trap.
- (c) Only valuable after (b) exists.

## 9. Pilot (30-90 days)
- **Pilot A (migration):** pick one in-flight migration, such as a Java 8 to 21 service, a Python 2-era ledger module to Go, or a COBOL/C routine to Rust. Prove equivalence for the top 20 functions, with bounded proofs plus differential fuzz on the rest.
  - Value metric: % of functions certified equivalent, divergences found (real bugs), and reduction in shadow-testing weeks.
- **Pilot B (critical paths):** take the top 10 payment and ledger functions, write 5-10 invariants with the customer, prove them, and gate PRs.
  - Value metrics: counterexamples found, invariant violations blocked, and review hours saved on agent PRs.
- **Honest expectation [I]:** most value in either pilot would come from **counterexamples found by bounded checking and fuzzing**, not from full proofs. That makes it a better-testing product, which is Antithesis's, Benchify's and Kiro's ground.

## 10. Willingness to pay
- Crypto audits: $50K-$500K per engagement [U, industry norm; Certora pricing not found].
- Non-crypto: no price points found. Comparables: Antithesis (enterprise, Jane Street-class), Diffblue and Qodo (seat-priced testing tools).
- Estimated ACV for (b): $60K-$250K at mid-market fintech, if it is sold. Pilot conversion depends on finding a real bug in the pilot. [U]
- Migration (a) runs into the **"destination subsidy" problem from round 11**: clouds, SIs and the migration-tool vendors (and AI coding agents themselves) bundle verification for free to win the migration.

## 11. Expansion
More modules, then more invariants, then the PR gate on all agent code, then compliance evidence (SOC 2 / PCI "change correctness" attestations [I]).

## 12. Competition (search-hard results)

| Player | Funding / status | Overlap with W | Source |
|---|---|---|---|
| **Axiom Math** | $64M seed + **$200M A at $1.6B** (Menlo, Mar 2026); 20 people; AXLE Lean API (free); Putnam 12/12 | Direct: "prove AI-generated code safe" | [S](https://siliconangle.com/2026/03/12/verifiable-ai-startup-axiom-raises-200m-prove-ai-generated-code-safe/), [S](https://menlovc.com/perspective/ai-will-write-all-the-code-mathematics-will-prove-it-works/) |
| **Harmonic** (Aristotle) | **$295M** total, $1.45B, pre-revenue; Aristotle API; hiring formal-verification engineers for "software and hardware" | Direct over time; currently math-first; used in pipelines that lift Rust into Lean | [S](https://dashboard.channelchek.com/?p=98780), [S](https://www.indexventures.com/startup-jobs/harmonic/formal-verification-engineer/) |
| **Theorem** (YC S25) | $6M seed (Khosla) | Most direct: AI-written bug prevention, legacy code migration, GPU and crypto code | [S](https://venturebeat.com/security/theorem-wants-to-stop-ai-written-bugs-before-they-ship-and-just-raised-usd6m) |
| **Logical Intelligence** | Funded (Pebblebed; amount not found); Aleph verification agent + Noa audit agent; LeCun as research board chair | Direct; crypto-first traction | [S](https://pebblebed.com/portfolio/logical-intelligence), [S](https://www.businesswire.com/news/home/20260120751310/en/Logical-Intelligence-Introduces-First-Energy-Based-Reasoning-AI-Model-Signals-Early-Steps-Toward-AGI-Adds-Yann-LeCun-and-Patrick-Hillmann-to-Leadership) |
| Pramaana Labs | $27M seed (Khosla, Accel, Nexus), Jun 2026 | Adjacent: domain rules converted to verified logic | [S](https://inc42.com/buzz/pramaana-labs-raises-27-mn-to-build-ai-verification-layer/) |
| Lanyon AI | $10.6M (Dimension), Aug 2026 | Formally verified scientific code | [S](https://runtimewire.com/article/lanyon-ai-10-6m-formally-verified-scientific-computing) |
| Athanor AI / Axiomatic AI | Seed Jul 2026 / $18M seed Mar 2026 | Verified RTL/engineering claims | [S](https://pitchbook.com/profiles/company/1442724-94), [S](https://letsdatascience.com/news/axiomatic-ai-raises-18m-seed-round-daa4339c) |
| Imandra (CodeLogician) | ~$9M total; neuro-symbolic code reasoning agent (Mar 2025); finance roots | Direct for fintech critical paths | [S](https://www.cbinsights.com/company/imandra) |
| Benchify (YC) | $500K pre-seed; formal-methods-based code repair and review | Adjacent (gate) | [S](https://www.extruct.ai/hub/benchify-com-funding/) |
| Galois | Services/R&D; 2026 AI-for-FM stack for legacy code, spec generation and Rust transpilation; CN/VERSE | Wedge (a) | [S](https://www.galois.com/ai-fm) |
| Antithesis | $105M A (Jane Street) | The substitute: deterministic simulation instead of proofs | [S](https://pulse2.com/antithesis-105-million-series-a/) |
| **AWS Kiro** | GA; SMT requirements analysis + PBT spec-to-code (May 2026); ARG decade of in-house FM | Platform absorption of wedge (c) | [S](https://siliconangle.com/2026/05/12/aws-kiro-accelerates-software-development-proving-code-correctness-gets-work/) |
| **Mistral Leanstral** | Open source (Apache 2.0) | Commoditizes the prover | [S](https://mistral.ai/news/leanstral) |
| **Google DeepMind** | AlphaProof Nexus; Verified Code Generation team | Lab absorption | [S](https://www.analyticsinsight.net/artificial-intelligence/googles-new-formal-verification-framework-targets-safer-ai-development) |
| Certora / Runtime Verification | Crypto FV leaders | Excluded niche; proves the services model | [S](https://www.certora.com/blog/momentum-for-2026) |
| Atlas Computing (nonprofit), Morph Labs (Szegedy, autoformalization) | R&D | Spec-generation tools | [S](https://metagov.org/projects/atlas-computing), [S](https://twimlai.com/go/745) |
| Microsoft (Verus), Diffblue, Qodo, Kestrel | Not re-searched this round (search budget) | Verus is MSR open source; Diffblue/Qodo cover tests | [U] |

**Count:** at least 8 funded specialists with more than $600M combined, plus AWS, Google, Mistral and open-source provers. That is crowded at the top, on a market with no visible enterprise revenue yet.

## 13. Moat (10 / 100 / 1,000 customers)
- **10:** Expert know-how and per-customer spec libraries, which is services. Axiom and Harmonic have 10-50x more prover R&D.
- **100:** Per-framework spec and proof libraries (Stripe SDK contracts, Postgres semantics, Django ORM models) and a verified-component catalog. This is plausible, but the specs are customer-specific and the frameworks are public. Labs and Axiom can synthesize them, as ATLAS shows (2.7K verified programs auto-generated).
- **1,000:** A cross-customer corpus of (code, spec, proof) is a real data moat, **but** the leader with $264M in funding (Axiom) or a lab will reach 1,000 first if the market materializes.
- **"Difficulty is the moat" fails [I]:** the difficulty is real, but the people best equipped to beat it (IMO-gold prover teams, DeepMind, AWS ARG) are already competing. For a new team, difficulty is a barrier to entry, not protection.

## 14. Market math
- **$10M ARR:** about 60 customers at $165K. Plausible, if the work is mostly services (Certora-like).
- **$50M ARR:** about 250 customers at $200K. This needs non-crypto, non-hyperscaler adoption that has not appeared, and roughly 25-50% services gross margin drag [I].
- **$100M ARR:** about 400 customers at $250K, or a migration-bundle model. It collides with Axiom, Harmonic, AWS and the labs.
- **Could it be $10B?** Only as "the verification layer for all AI code", which is exactly Axiom's and Harmonic's $1.5B pitch. A $10B outcome goes to whoever owns the prover model. That is a lab-scale bet, not a seed wedge. A wedge-sized company tops out at a Certora/Galois-scale services-plus-software business, typically $50-150M ARR [U].

## 15. CTO test sentence
"Before any agent PR touching payments merges, we prove the ledger invariants still hold, or we hand you the failing input."
- Likely CTO reply [I]: "Can you do that on our TypeScript/Python stack without my team writing specs? If not, Antithesis, property tests and Kiro get me 80% of the way."

## 16. Kill test question
"Can we find 10 non-crypto, non-hyperscaler companies that will pay $100K+ for proofs (not tests) on AI-written code within 90 days, ahead of Axiom, Theorem and Kiro?"
- Desk evidence says no: zero named non-crypto customers among the best-funded players, and Amazon chose human sign-off.

## 17. Scores (1-10)

| Criterion | Score | Why |
|---|---|---|
| Pain severity | 6 | AI-code quality is a real worry. Proofs are a "nice to have" vs. tests outside high-assurance code |
| Urgency | 4 | Buyers reach for sign-off and testing first. No proof mandates outside crypto |
| Market timing | 4 | Technically about 1-2 years early for general code. Commercially, the specialists got there first |
| Speed to pilot | 4 | Spec elicitation takes weeks of experts. Migration equivalence is faster only for pure code |
| Ease of integration | 3 | Mainstream languages and frameworks are poorly supported by Lean, Verus and Dafny |
| Ease of reaching customers | 4 | Buyer is unclear (VP Eng vs. security vs. platform). The narrative is crowded with $1B+ players |
| Willingness to pay | 4 | Proven only in crypto and hyperscalers. Harmonic is pre-revenue |
| Competition | 2 | Axiom $264M, Harmonic $295M, Theorem, Logical Intelligence + 4 more, plus AWS, DeepMind and Mistral |
| Moat potential | 5 | The proof/spec corpus is real, but the leaders accumulate it first, and auto-synthesis (ATLAS) erodes it |
| Market size | 6 | Large if verification becomes default for AI code. Mostly captured by prover-model owners |
| VC attractiveness | 4 | VCs love the category, but have already picked winners. A 2026 seed "me-too vs Axiom" is a hard sell |
| **Average** | **4.2** | |

## 18. Original bar scores (bar: 8.5 avg, no category < 7)

| Bar criterion | Score |
|---|---|
| Pain (acute, budgeted) | 5 |
| Competition position | 2 |
| Exciting / easy for VCs | 6 (exciting yes, easy no: the category is taken) |
| Founder-fit for a non-PhD-prover team | 3 [I] |
| Speed to revenue | 3 |
| **Avg** | **3.8: fails, multiple categories < 7** |

## 19. Five simulated buyers

| Buyer | Answer | Reasoning [I] |
|---|---|---|
| VP Eng, Series D payments processor (~400 engs, TypeScript/Go) | **MAYBE then NO** | "Interesting for the ledger, but you need my staff engineers for 6 weeks to write invariants. I'll take Antithesis or property tests + Kiro specs. Come back when it's zero-spec." |
| Head of Platform, public SaaS migrating Java 8 to 21 and splitting a monolith | **NO** | "The migration vendor / Amazon Q / our agents do it, and we shadow-test. A proof certificate doesn't change my risk sign-off. Only canaries do." |
| CISO, crypto exchange (out of scope but real) | **YES** | Already buys Certora/RV-style proofs; would pay $200K+. Excluded niche and already served |
| Director of Infra, cloud-scale company with an IaC estate | **MAYBE** | "Prove no security group ever opens 0.0.0.0/0 on port 22." AWS Zelkova/Config and Kiro already do policy-level proofs natively, so likely absorbed |
| CTO, HFT/quant firm | **MAYBE** | Values correctness hugely, but already uses Antithesis or in-house OCaml/FM teams. Would trial Theorem or Axiom before an unknown seed company |

**Tally: 1 YES (excluded niche), 3 MAYBE, 1 NO.** No in-scope YES.

## 20. VC committee view (simulated)
- **Bull partner:** "Verification is the bottleneck of AI coding; this is a $10B+ layer. Kleppmann-level mindshare; tech curves are steep (Dafny 68% to 96%)."
- **Bear partner:** "We'd be the 9th funded entrant. Axiom has $264M and IMO/Putnam talent. Harmonic has $295M. Theorem got there in 2025 with Khosla. AWS put SMT spec checks in Kiro. Mistral open-sourced the prover. DeepMind has a verified-code team. Where's the revenue? Harmonic is pre-revenue at $1.45B. Outside crypto, nobody has shown that a buyer pays for proofs over tests."
- **Decision:** Pass, unless the team is world-class prover researchers (in which case they compete with Axiom for the platform, not a wedge) **or** they have exclusive access to a migration channel. Even then, the "destination subsidy" risk applies.

## 21. Red team (the strongest case for keeping it alive, then why it still dies)
- **Best survival path:** wedge (a), equivalence-proved migrations, sold to **migration factories and SIs** (not end buyers) as a "certified equivalent" upsell.
  - Why it could work: the old code is the spec, so the hardest problem goes away. Heimdall shows 94% on eBPF.
- **Why it still dies:**
  1. Enterprise migration code is I/O- and framework-heavy, so proofs degrade to bounded checks plus fuzzing, which is just testing.
  2. Theorem already markets "sped up code migration in legacy systems", and Galois's 2026 stack targets legacy code and Rust transpilation.
  3. The round 11 lesson holds: migration destinations (clouds, AI coding agents) subsidize the tooling.
  4. AWS itself still required 10^15 differential samples next to Dafny proofs. Buyers trust shadow traffic, not certificates.
- **Second-best path:** a verification gate for agent PRs on a narrow, high-value, spec-native domain such as authorization policies (Cedar/OPA/IAM) or financial ledgers with clear invariants. But IAM and policy proofs are AWS-native (Zelkova, Cedar analysis), and ledgers are the Imandra/Pramaana direction. This is feature-sized and crowded, the same death as T3 and the in-loop verification judge.

## 22. Kill signals checklist

| Signal | Status |
|---|---|
| Too early technically for mainstream code | **Yes**: 27-44% on Lean/Verus benchmark tasks, and the spec problem is unsolved |
| Frontier labs / platforms build it | **Yes**: DeepMind verified-code team, Mistral Leanstral, AWS Kiro, Harmonic/Axiom at lab-scale funding |
| Tests good enough for buyers | **Mostly yes**: Amazon chose sign-off; Jane Street funded Antithesis (simulation) |
| Services-heavy spec writing | **Yes**: Certora's 40 experts/25 PhDs model; Theorem claims "weeks or even days" per verification |
| Crowding | **Yes**: >$600M across 8+ specialists in 18 months |

## VERDICT: KILL (avg 4.2; original bar 3.8)
The lens "difficulty is the moat" breaks here, because the difficulty attracted the best-funded technical teams of 2025-26 before us. Proofs are being commoditized from above (labs, open-weight provers, free Lean APIs) and absorbed sideways (AWS Kiro). Meanwhile buyer demand outside crypto and hyperscalers remains unproven. Revisit only if (1) a named non-crypto company publicly pays for proof-gated AI code, **and** (2) the leaders stay math-first through mid-2027. A narrow residual worth noting for founders with proof-engineering talent: **equivalence certification sold through migration SIs.** Treat it as a services business, not a venture thesis.
