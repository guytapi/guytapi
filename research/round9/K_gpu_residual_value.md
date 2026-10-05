# Thesis K: "Carfax + Kelley Blue Book for GPUs"
Round 9 | 2026-10-05 | Red-team deep dive | 35 searches (WebFetch blocked on most domains, so all claims come from search-result snippets; URLs are as returned by search, page content NOT independently verified)

**One sentence:** Per-GPU health telemetry plus market price data, turned into certified condition reports and residual-value curves for neoclouds, lessors, private credit, refurbishers and secondary marketplaces.

**VERDICT: KILL (avg 4.4/10).** The money is real and the pain is real, but the "Blue Book" half was built and funded in 2025-26 (Silicon Data, American Compute, Hashrate Index, Ornn, plus CME and ICE futures). The "Carfax" half (telemetry) belongs to NVIDIA, which made Fleet Intelligence free and is now underwriting residual value and utilization itself. That leaves no open wedge.

---

## 1. Size (evidence)
| Item | Evidence | Source (as returned by search) |
|---|---|---|
| GPU-backed debt | ">$20B of GPU-backed facilities announced" (Sep 2026). Grew from a "$2.3bn private-credit experiment" to investment-grade and syndicated within 30 months | wing.vc/content/how-the-gpu-became-collateral; peony.ink/blog/gpu-cluster-financing-data-room |
| CoreWeave | $8.5B GPU loan backed by the Meta deal (largest chip-backed deal), plus a $3.1B facility; total debt $35B at 30 Jun 2026 | news.bloomberglaw.com/capital-markets/coreweave-raises-8-5-billion-gpu-loan-backed-by-meta-deal; capacityglobal.com/news/coreweaves-debt-hits-35bn/ |
| Lambda | $926M TLB rated Baa2 by Moody's; $1B facility (May 2026); reported $500M "first-of-its-kind GPU-backed ABS" | storagenewsletter.com/?p=305474; pulse2.com/lambda-secures-926-million-gpu-term-loan-with-baa2-investment-grade-rating/ |
| xAI | SPV: $12.5B debt and $7.5B equity; Apollo ~$3.4B loan to a chip-leasing vehicle | fintool.com/news/apollo-xai-gpu-financing; techrepublic.com (xAI $20B) |
| Crusoe | ~$425M Upper90 facility | wing.vc (snippet) |
| Macro | Morgan Stanley: $1.5T data-center financing gap to 2028, ~$800B of it from private credit. Citadel Securities: $500B in chip financing debt by 2028 | Morgan Stanley "Bridging Data Center Gap" PDF; cryptobriefing.com/citadel-securities-500b-chip-financing-debt/ |
| NVIDIA financing push | 10 Aug 2026: six MOUs (Apollo, BlackRock, Blackstone, Brookfield, Goldman, KKR) aiming at >$500B. NVIDIA may provide **residual-value support up to 25%**, case by case (non-binding) | blog.cobaltintelligence.com/post/nvidia-offers-25-residual-support-in-ai-finance-push; futurumgroup.com |
| NVIDIA utilization backstop | 1 Jul 2026: NVIDIA rents back idle neocloud GPUs at a fixed rate (Sharon AI 40k GPUs; Firmus up to 170k) | capacityglobal.com/news/nvidia-now-agrees-to-rent-back-unused-gpu-capacity-...; datacenterdynamics.com |
| Installed base | Not cleanly found. CoreWeave alone has >250k GPUs; >100 neoclouds, 10-15 at scale in the US; ABI counts 696 neocloud facilities in 2026. Unverified estimate: several million Hopper/Blackwell GPUs, $300B+ | hashrateindex.com/blog/what-is-a-neocloud...; abiresearch.com |
| Depreciation fight | Burry: $176B understated depreciation 2026-28 (5-6yr book life vs 2-3yr economic life). CoreWeave/NVIDIA defend 4-6 years, citing A100s still rented through 2029 | finance.yahoo.com (Burry); nasdaq.com; blog.dshr.org/2026/02/mind-gaap-again.html |
| Rental prices | H100 went from ~$8/hr (2023-24 peak) to $2.85-3.50 (late 2025). Silicon Data index $2.36 (Jun 2025). Contract prices then *rose* about 40% ($1.70 Oct 2025 to $2.35 Mar 2026). B200 residual reported 58% *above* launch price | introl.com/blog/gpu-cloud-price-collapse...; intuitionlabs.ai; digg.com/tech/hvbx9vrx |
| Secondary market | Used H100 at 50-70% of new. Hashrate Index: refurbished H100 HGX node $246k (76% of new, asks only). American Compute GPU index down 8% YoY (Sep 2026). Compute Exchange launched a used-GPU marketplace (Jul 2026) | hashrateindex.com/blog/announcement-introducing-the-ai-hardware-price-index/; amcompute.com/rack-report; siliconangle.com/2026/07/17/compute-exchange-... |
| Failures | Llama 3 405B: 419 interruptions in 54 days on 16,384 H100s (one every ~3h). Faulty GPU 30.1%, HBM3 17.2%. Cited figure of ~9%/yr annualized GPU failure (training) | datacenterdynamics.com/en/news/meta-report-details-...; introl.com (9% figure unverified) |
| Refresh | GPU servers refreshed in 10-18 months at some hyperscalers. First large decommissioning wave expected 2026-2029 | dev.resource-recycling.com 2026/03/09; sktes.com |

**Size conclusion:** the underlying asset pool is huge ($100Bs) and so are the debt flows. That is the only thing that holds up.

## 2. Pain
- "Nobody knows what a used GPU cluster is worth": HN front page (item 48917135). "A $10M fleet of H100 servers could be worth $3M or $7M in three years"; "no standard appraisers or futures markets"; "lenders charge an enormous premium for a risk they cannot measure". (hn.nuxt.dev/item/48917135; snippet only)
- "GPU compute has neither forward curves nor residual value markets… no insurance or swap market" (youmind / fourweekmba). **This was already out of date by Oct 2026.**
- Lessors: "GPU residual risk is unquantifiable with standard models" (introl/epoka). FMV leases leave the residual with the lessor.
- Who loses: neoclouds refinancing at wide spreads; lessors and private credit with residual exposure; used-GPU buyers (certified units sell at a 15-25 point premium over unknown provenance, introl snippet); ITADs.
- **But:** "The chips are the collateral on paper; the contracted revenue is the collateral that actually gets underwritten" (peony.ink). Lenders underwrite the *offtake contract* (Meta, Microsoft, IG customers), and residual is a secondary input. Spreads already tightened to A3/SOFR+225 without a GPU Carfax. That shrinks how much condition data is worth.
- Physical wear is a weak driver of value: "GPUs have no moving parts… nothing naturally degrades with normal use"; value moves in "step-change resets triggered by architectural releases". **Per-GPU health explains little of residual value. Generational obsolescence and power cost explain most of it.** This undercuts the "Carfax" half of the thesis.

## 3. Competition (search hard)
| Player | What they do | Funding / traction |
|---|---|---|
| **Silicon Data** | 9 indices (H100/H200/A100/B200/MI300X rental, token spend), **forward curves (Apr 2026)**, **GPU Residual Value Curve (DCF off the forward curve)**, **SiliconMark per-cluster performance benchmark** (finds 34% variance within the same SKU). CME NYMEX H100/B200 futures settle on its index from **5 Oct 2026 (today)** | $4.7M seed (Mar 2025) + **$30.5M Series A (11 Aug 2026)** led by Valor Atreides; CME, DRW, Jump, VanEck, Samsung Next. >1,000 users; Bloomberg-terminal coverage |
| **American Compute (amcompute.com)** | **GPU appraisals and diligence for private credit and equipment finance (FMV + orderly liquidation value), whole rack**; monthly **Rack Report** of realized resale prices (600k+ closed-transaction data points from brokers, resellers, ITADs); $2B+ of equipment reviewed; **residual value insurance** with A-rated reinsurers, up to $500M per deal; "GPU Residual Value Report 2026" | Funding not found |
| **Ornn** | Compute price index (on Bloomberg) + futures. ICE GPU futures on its index pending approval | $5.7M seed + **$33M led by a16z (Jun 2026)** |
| **Forward Compute** | Residual-value insurer for compute | unverified |
| **Hashrate Index (Luxor)** | AI Hardware Price Index (HGX nodes, new vs refurbished; asks only) | Luxor-funded |
| **Compute Exchange** | Used/refurbished GPU marketplace (Jul 2026) | unverified |
| **Vast.ai** | Certified refurbished GPU servers with burn-in, VRAM, benchmark and thermal certification reports | established |
| MillionMiner, BuySellRam, Alta, refurbishers | Run their own diagnostics (memory error history, NVLink/NVSwitch health, load test) before shipping | many |
| **NVIDIA Fleet Intelligence** | **Free managed service** for Hopper/Blackwell/Rubin: an agent streams utilization, power, thermals, ECC, NVLink and reliability data to NGC, plus cryptographic firmware attestation. Open-source agent | NVIDIA. Learned from DGX Cloud's hundreds of thousands of GPUs |
| NVIDIA DCGM, Mission Control, RMA data | Health checks and fleet failure data NVIDIA alone holds at scale | |
| **NVIDIA as financier** | 25% residual-value support; utilization backstop; reportedly sounding out insurers | Aug/Jul 2026 |
| Clockwork.io | FleetIQ/TorchPass GPU fault migration (Nebius, Nscale) | >$40M (NEA) |
| SemiAnalysis ClusterMAX | Neocloud ratings. Critics flag conflicts if certifier outputs drive covenants | |
| ITADs (Iron Mountain, Sims Lifecycle, SK TES, Reconext) | Remarketing and testing of decommissioned AI servers. They feed American Compute's data | large |
| Rating agencies | Moody's rated Lambda's GPU TLB Baa2, so methodology exists (contract-led). Data-center ABS criteria from Moody's (Feb 2025), Fitch (Sep 2025), S&P (2024) | |
| Hilco / Gordon Brothers / Tiger | No GPU-specific appraisal evidence found (gap or invisible). Natural acquirers or partners for American Compute-type players | |

**Competition conclusion:** every piece of the thesis exists with a funded owner: price index (Silicon Data, Ornn), residual curve (Silicon Data), appraisal + realized-price data (American Compute), RVI (American Compute, Forward Compute), per-cluster performance certification (SiliconMark), refurb certification (Vast.ai, refurbishers), fleet telemetry (NVIDIA, free), residual guarantee (NVIDIA). The thesis is 12-18 months late.

## 4. Can NVIDIA or appraisers own this? Data access
- **Telemetry access is the fatal problem.** A neocloud has no reason to send per-GPU fault history to a third party that will then *mark down* its collateral. Lenders can't compel continuous telemetry beyond what covenants already require (utilization and revenue "oracles"). The only party with cross-fleet telemetry at scale and an opt-in agent already installed is NVIDIA (Fleet Intelligence, free), and NVIDIA is now the residual guarantor. NVIDIA has every incentive to own the "certified Hopper/Blackwell" condition standard, tied to warranty and attestation (a "CPO for GPUs").
- Price-side data comes from brokers and ITADs, and American Compute has already aggregated 600k closed trades. A newcomer starts at zero.
- So yes: NVIDIA (condition) plus Silicon Data / American Compute (value) can and do own it.

## 5. Buyer, count, pricing, pilot
- Buyers: ~100-200 neoclouds (10-15 at scale), maybe 50-150 GPU lenders and lessors (private credit, equipment finance, ABS desks; banks excluded), ~20-50 serious ITADs and refurbishers, a handful of marketplaces. **Realistically ~300-500 accounts.** Debt is concentrated: the top 10 borrowers hold most of the $20B+.
- Pricing benchmarks: appraisal per deal $25k-$150k (unverified; typical equipment-appraisal norms); data subscriptions $20-100k/yr; RVI premium in bps of notional (that money goes to insurers and brokers).
- 30-day pilot: run a condition and value report on a 1-2k GPU fleet for one lender's refinancing. Feasible, but American Compute already sells exactly this.

## 6. Moat and market math
- Claimed moat: a cross-fleet failure and price dataset. In reality NVIDIA holds the failure data, American Compute and Silicon Data hold the price data, and CME/ICE index licensing gives the index winner (Silicon Data) a Bloomberg/ICE-style lock-in.
- $10M ARR = ~100 lenders/neoclouds at $100k: plausible only as an *incumbent*. $50M = 500 accounts at $100k, which is the entire buyer pool. $100M requires a transaction toll (bps on debt and resale volume) or index licensing, and the index seat is taken.
- VC view: "Moody's/Bloomberg for compute" could be a $10B outcome. **But the category leader was crowned in Aug-Oct 2026** (Silicon Data: CME futures live today, Valor/CME/DRW/Jump cap table; Ornn: a16z/ICE). A 2026 entrant pitching the same story is a "why not Silicon Data?" pass.

## 7. Kill signals (hit)
1. Funded incumbents on both price and appraisal (Silicon Data $35M, Ornn $39M, American Compute live with RVI).
2. NVIDIA owns telemetry (free Fleet Intelligence) and is the residual guarantor (25% RV support, utilization backstop). It will define "certified condition".
3. Underwriting is driven by contracts, not condition. Residual value is set by generational obsolescence, not wear, so the "Carfax" data has low marginal value.
4. Small, concentrated buyer pool (~300-500), financial/regulated adjacency (insurance placement needs licensed brokers, covenants need independence).
5. Data access: owners won't volunteer negative telemetry.

---

## METHOD template fields
- **Problem:** Lenders, lessors and buyers can't price the residual value or condition of GPU collateral.
- **Recent evidence (5+):** HN "Nobody knows what a used GPU cluster is worth"; Burry depreciation fight; NVIDIA 25% RV support (Aug 10); NVIDIA utilization backstop (Jul 1); CME compute futures (Oct 5); Silicon Data Series A (Aug 11); Ornn a16z (Jun); Compute Exchange used market (Jul); lessor quotes on "unquantifiable" residual.
- **Who has the pain:** private credit, equipment lessors, neocloud CFOs refinancing, used-GPU buyers.
- **What they do today:** American Compute appraisals + Rack Report; Silicon Data indices and residual curves; offtake-contract underwriting; NVIDIA guarantees; RVI; refurbisher burn-in reports.
- **Why current products fail:** mostly they don't. The remaining gap is per-unit condition, which matters little for value and is NVIDIA-gated.
- **Why now:** asset class is maturing, a decommission wave is coming, futures are listing. The same "why now" already pulled in incumbents.
- **Potential product:** telemetry-backed condition certificate + residual curve + transaction toll.
- **Time to value:** 2-6 weeks per appraisal (agent install + data).
- **Pilot:** one lender refinancing, a 1-2k GPU fleet report.
- **WTP:** real but per-deal and lumpy; $25-150k/appraisal (unverified).
- **Expansion:** index, futures, RVI, marketplace. All occupied.
- **Competition:** see table. Severe.
- **Moat (10/100/1,000):** 10 customers: none; 100: some price data but behind American Compute; 1,000: there aren't 1,000 buyers.
- **CTO test sentence:** "We certify the health and residual value of every GPU you finance." Lender reply: "We use American Compute for appraisals, Silicon Data for curves, and NVIDIA is guaranteeing 25%."
- **Kill test question:** Will a top-20 GPU lender switch from American Compute/Silicon Data, or pay extra for per-GPU telemetry they can't force the borrower to share? Evidence suggests no.

## Scores (1-10)
| Criterion | Score | Why |
|---|---|---|
| Pain severity | 6 | Real residual uncertainty, but contracts carry the underwriting |
| Urgency | 5 | Refinancing wall and decommission wave are 2027-29; tools exist |
| Market timing | 3 | 12-18 months late; leaders crowned Aug-Oct 2026 |
| Speed to pilot | 6 | Report-style pilot is easy |
| Ease of integration | 3 | Needs borrower telemetry; NVIDIA agent is the default |
| Ease of reaching customers | 5 | Concentrated, relationship-driven credit world |
| Willingness to pay | 5 | Per-deal fees; insurance economics go to carriers |
| Competition | 2 | Silicon Data, American Compute, Ornn, NVIDIA, Forward Compute, Vast.ai |
| Moat potential | 4 | Index/network moat already claimed by others |
| Market size | 5 | Huge asset pool, ~300-500 buyers |
| VC attractiveness | 4 | "Why not Silicon Data / a16z-backed Ornn?" |
| **Average** | **4.4** | |

### Original bar scores (bar: 8.5 avg, none below 7)
Pain 6 / Competition 2 / Exciting-for-VCs 6 (the story is great, the timing isn't) / Market size 6 / Founder-reachability 5. **Fails on competition and timing.**

## 5 simulated buyers
1. **Private credit fund, GPU desk (~$2B GPU loans): NO.** "We underwrite the Microsoft offtake. American Compute gives us OLV, and NVIDIA's 25% RV support is the new floor."
2. **Mid-size neocloud CFO (8k H100s, refinancing 2027): NO.** "Why would I hand a third party fault logs that lower my collateral value? We already run NVIDIA Fleet Intelligence for free."
3. **Equipment lessor (FMV leases on HGX): MAYBE.** "Per-unit return-condition grading at lease end is useful, but that's a feature on our ITAD contract."
4. **ITAD/refurbisher: MAYBE.** "A neutral certificate could add 15-25 points to price. But NVIDIA-attested certification would beat a startup's stamp, and we already sell our data to American Compute."
5. **Secondary marketplace (Compute Exchange-type): MAYBE/YES for an API at low ACV ($20-50k).** Too small to build a company on.

## VC committee view
- **Bull:** compute as an asset class is real: $20B+ debt heading to $500B, futures live, someone becomes the Moody's of compute.
- **Bear (wins):** that someone is already chosen. Silicon Data (CME index provider, Valor/DRW/Jump) and Ornn (a16z, ICE) hold the benchmark seats. American Compute holds appraisal + RVI. NVIDIA holds telemetry and is backstopping residuals directly. A newcomer's only differentiator (per-GPU telemetry) depends on data access it can't get, and measures the variable (wear) that matters least. **Pass.**

## Red team (best case for keeping it alive)
- Condition *does* matter at the margin for HBM failures and liquid-cooled GB200 leak/thermal history. NVL72 racks are more fragile and harder to resell, so rack-level health could become important in 2028-29.
- NVIDIA's guarantee creates a need for *independent* condition verification (lenders may not trust the guarantor to grade itself), and covenant-independence concerns about certifiers are already voiced.
- Hilco/Gordon Brothers don't seem to be active, so a Hilco-for-GPUs is open on the liquidation side.
- **Rebuttal:** all three are niches that American Compute or Silicon Data (SiliconMark already measures per-cluster delivered performance) can extend into within a quarter. None reaches 8.5.

## VERDICT
**KILL.** Thesis K is #31 on the scoreboard. Same pattern as G and T3: a well-publicized gap (HN, Burry, Wing) was funded within months. Silicon Data's Series A was 11 Aug 2026 and CME futures go live today. If revisited, the only angle worth a look is **GB200/GB300 NVL72 rack-level condition and liquidation for the 2028-29 Blackwell decommission wave**, and only with founder access to ITADs or liquidators. Even that is likely a feature for American Compute.

### Sources (as returned by WebSearch; content not fetched)
- silicondata.com/products/gpu-residual-value ; silicondata.com/products/silicon-mark ; axios.com/pro/enterprise-software-deals/2026/08/11/silicon-data-compute-pricing-nvidia ; cryptobriefing.com/cme-group-compute-futures-launch/
- amcompute.com/solutions/appraisals-diligence ; amcompute.com/rack-report ; amcompute.com/gpu-residual-value-insurance
- siliconangle.com/2026/06/24/ornn-raises-33m/
- developer.nvidia.com/blog/introducing-nvidia-fleet-intelligence-for-real-time-gpu-fleet-visibility-and-optimization/
- blog.cobaltintelligence.com/post/nvidia-offers-25-residual-support-in-ai-finance-push
- capacityglobal.com/news/nvidia-now-agrees-to-rent-back-unused-gpu-capacity-from-neocloud-operators-if-customer-demand-falls-short/
- wing.vc/content/how-the-gpu-became-collateral ; peony.ink/blog/gpu-cluster-financing-data-room ; hn.nuxt.dev/item/48917135
- news.bloomberglaw.com/capital-markets/coreweave-raises-8-5-billion-gpu-loan-backed-by-meta-deal ; capacityglobal.com/news/coreweaves-debt-hits-35bn/
- pulse2.com/lambda-secures-926-million-gpu-term-loan-with-baa2-investment-grade-rating/
- datacenterdynamics.com/en/news/meta-report-details-hundreds-of-gpu-and-hbm3-related-interruptions-to-llama-3-training-run
- hashrateindex.com/blog/announcement-introducing-the-ai-hardware-price-index/ ; siliconangle.com/2026/07/17/compute-exchange-opens-secondary-market-used-nvidia-h100-a100-gpus/
- futuriom.com/articles/news/clockwork-io-guarantees-ai-training-uptime/2026/07
- introl.com/blog/gpu-cloud-price-collapse-h100-market-december-2025 ; dev.resource-recycling.com/e-scrap/2026/03/09/ai-servers-reshape-itad-sector-recyclers-brace-for-new-wave/
- Forward Compute and the 9% annual failure figure: unverified.
