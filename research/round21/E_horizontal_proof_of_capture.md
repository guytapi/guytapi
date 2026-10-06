# THESIS E — Horizontal capture-time evidence layer ("make photos and documents trustworthy again")

**Date:** 2026-10-06 · **Stance:** skeptical analyst / red team · **Searches used:** 39 of 40 (WebFetch blocked; all facts come from search-result snippets and need checking at the source before going in a deck)
**Prior appearances:** round 4 #2 "know your evidence" · round 17 earnings-calls C2 (6.6) · round 17 analyst-categories #1 (6.5) · round 21 H2 leftover (verified-human evidence bundle)
**Verdict: KILL as a standalone venture thesis** (average 5.8; Defensibility 3, Competition position 3). Making it horizontal does not rescue it. It turns a TAM problem (F4) into a competition problem (F2) and a partial absorption problem (F1). The company this thesis describes already exists. **Truepic Vision** is sold across insurance, lending, warranty (OtterBox), product recalls (Recall Results / CPSC), auto (Ford) and P2P commerce. It added a cross-company **Risk Network** in Sept 2025 and is embedded in Qualcomm silicon. Meanwhile Apple (Sept 2026) and Google (Pixel 10) now provide the capture trust root for free. One narrow residue is listed in §10.

Labels: [S] = from a search snippet with a URL · [I] = our inference · [U] = unverified or self-reported

---

## 0. Bottom line in six lines
1. **The pain is real, measured and loud.** Ravelin (2026): **67% of merchants** report receiving AI-generated fake refund evidence, and 65% of consumers say AI made false refund claims easier [S]. Forter: AI-generated damage claims are the **fastest-growing form of return abuse** [S]. MRC 2026: policy abuse is the **#1 cited fraud risk** (41% of merchants) [S]. Public incidents span every target vertical: DoorDash's AI delivery photo (Jan 2026), Lyft's Gemini cleaning-fee photos (May 2026), Airbnb's $9K AI damage claim, Vinted/Amazon/Fnac refunds, Boll & Branch and Bogg.
2. **"Detection loses, capture wins" is now the consensus, not an insight.** Switch Labs (Aug 2026) found detectors below chance on 2024-26 generators and ~10%+ false positives [S]. Every vendor, including Truepic, Vaarhaft, Captur, Switch Labs and Succinct, now sells exactly this message.
3. **The horizontal, cross-company version already exists.** Truepic Vision has 100+ enterprises across 6+ verticals, a shared Risk Network across organizations, and live capture at 100K+ OtterBox warranty claims in under 4 months [S]. Vaarhaft offers cross-submission duplicate hashing plus SafeCam web capture for e-commerce returns [S]. Captur raised a $6M seed (Mar 2026) for on-device verification of POD, inspection and e-com photos and handles "tens of millions" of images a month [S].
4. **The platforms are giving away the hardest part.** Apple Reference Image (iPhone 18 Pro, Sept 9 2026) signs at the sensor, ships **APIs for third-party apps in iOS 27**, and Apple will support SynthID [S]. Pixel 10 signs every photo with C2PA at Assurance Level 2 [S]. Google's SynthID Content Detection API is on Google Cloud in partner preview [S]. Truepic's library is in Snapdragon [S]. Capture integrity becomes a free OS primitive on new devices over 2027-2030.
5. **The cross-company graph is not a clean moat.** Forter, Signifyd and Riskified already own the cross-merchant *person/device* graph, which is the stronger fraud signal. Truepic owns the cross-company *capture/device* graph. A perceptual-hash reuse network is easy to copy.
6. **Venture math:** a $100M ARR path is plausible only with blended per-verification pricing across 3+ verticals. That requires 3+ different workflow integrations (Loop/Shopify, Tavant/Syncron, Onfleet/carrier TMS, Airbnb-style marketplace trust stacks), which is exactly where Truepic, Captur and the workflow owners already sit. A $10B outcome needs Socure-like scale ($364M ARR, $5.2B valuation, Aug 2026 [S]) in a category where the market leader (Truepic) has raised only ~$36M in 9+ years [S].

---

## 1. Size of evidence-based payouts and the AI share

| Flow | Size signal | AI-evidence signal | Source |
|---|---|---|---|
| US e-commerce/retail returns | NRF: $849.9B returns in 2025, ~9% fraudulent ≈ **$76B** [S]. Stripe cites $103B fraudulent of $685B (2024) [S] | Forter: AI damage claims are the fastest-growing return abuse. Pindrop: ~3 in 10 retail fraud attempts AI-generated. Ravelin: 1 in 3 refund abusers use or consider AI; 67% of merchants received AI fake evidence | [Retail Gazette Jun 2026](https://www.retailgazette.co.uk/blog/2026/06/retailers-face-surge-in-ai-generated-fake-damage-claims-and-refund-scams/), [Practical Ecommerce](https://practicalecommerce.com/ai-makes-refund-evidence-easier-to-fake), [BRC/Ravelin](https://brc.org.uk/news-and-events/news/associate-insight/2026/the-state-of-refund-abuse-repeat-offenders-eroding-loyalty-and-ais-impact/), [Stripe](https://stripe.com/gb/resources/more/refund-abuse) |
| **Photo-gated** refunds (the subset this thesis actually serves) | Not published. Most returns are gated by the physical item coming back (Happy Returns, carrier scan), not by a photo. Photo-gated means "damaged on arrival / keep it / partial refund / marketplace dispute." Our estimate: **5-15% of refund dollars** ≈ $4-11B US [I] | Inpainting real photos defeats whole-image detectors [S] | [Switch Labs](https://www.switchlabs.dev/post/ai-faked-damage-photos-playbook) |
| Manufacturer warranty | 3-10% of claims fraudulent ≈ $45B/yr for US brands [S, vendor figure] | Truepic/OtterBox, auto warranty (29 reused-image claims, $350K, round 17); NAM asked CPSC to require image verification against AI photos (recall fraud) | [Claimlane](https://www.claimlane.com/resources/blog/warranty-fraud-explained), [Foley Jul 2026](https://www.foley.com/insights/publications/2026/07/when-recalls-go-rogue-the-impact-of-ai-fueled-recall-fraud/), [NAM](https://nam.org/nam-to-cpsc-take-action-on-recall-fraud/) |
| Delivery POD / item-not-received | No reliable 2026 $ figure found. Captur customer GoBolt: −30% disputed delivery claims in week 1 [S] | DoorDash driver banned for AI POD photo (Jan 2026) | [Captur seed](https://pulse2.com/captur-6-million-raised-for-on-device-ai-image-verification-platform), [CXO Digital Pulse](https://www.cxodigitalpulse.com/?p=42336) |
| Gig/field completion | No $ figure | Lyft driver used Gemini for fake cleaning-fee photos (May 2026) | [AI Weekly](https://aiweekly.co/alerts/lyft-bans-driver-who-used-gemini-to-fake-damage-photos) |
| Property/rental damage | No $ figure | Airbnb $9,041 AI damage claim; Airbnb admitted it could not verify the photos | [Indian Defence Review](https://indiandefencereview.com/airbnb-ai-damage-claim-9000-dollar-fraud-case/), [AIID](https://incidentdatabase.ai/cite/1161/) |
| P2P marketplaces | No $ figure | Vinted/Amazon/Fnac AI damage refunds (OECD incident, Mar 2026) | [OECD.AI](https://oecd.ai/en/incidents/2026-03-02-16b3) |
| Documents (non-bank) | Inscribe: ~1 in 16 documents fraudulent; AI-generated up 5x (Apr-Dec 2025), but **<5% of fraudulent docs are AI-generated**, and they are mostly bank statements, invoices and payslips (lender-heavy) | | [Inscribe 2026](https://www.inscribe.ai/blog/1-in-16-documents-flagged-as-fraudulent-inside-our-2026-report) |

**Red-team read:** headline totals ($76B, $45B) overstate the addressable amount by about 10x. The thesis only addresses **photo-gated payouts**, and the *AI-evidence* share of those is still small in dollars (Inscribe: <5% of document fraud; no retail source gives a dollar share). The **growth rate** is the striking number, not the base. The "detectors below chance" finding is solid (Switch Labs citing a 16-method, 291-generator, 2.6M-image study) [S]. Note that Switch Labs sells a competing product.

---

## 2. Competitors: is anyone horizontal across non-insurance verticals with a cross-company network?

**Yes. Truepic, and it is the closest possible match.**

| Player | What it does in 2026 | Horizontal? | Cross-company network? | Threat |
|---|---|---|---|---|
| **Truepic Vision** | Live capture, 50+ image/data checks, cryptographic seal, workflow delivery. Customers include Equifax, Ford, Palomar, OtterBox, Recall Results; verticals listed as insurance, banking, automotive, P2P commerce, project management, international development [S]. Pricing $15-50 per *inspection* [S] | **Yes** (6+ verticals) | **Yes**: Risk Network (Sept 25 2025), which shares anonymized device/behavior flags across organizations [S] | **Fatal.** Funding only ~$36M (Series B 2021) [S], so it is beatable on distribution, but it has the product, the references and the network. Note: a snippet dates a TechCrunch growth article to "June 2026" and puts the Truepic library in "Snapdragon 8 Gen 5" [U]. Earlier coverage put it in Snapdragon 8 Gen 3 (2023). |
| **Vaarhaft** (Hamburg, ~7 staff) | Image/document fraud API, duplicate fingerprinting against prior submissions, **SafeCam** web-browser capture link for high-risk e-com returns, insurance and Airbnb-damage content [S] | Insurance + e-com + rental | Per-customer (cross-customer unclear) | Medium. Small, but it already sells the exact e-com workflow |
| **Captur** (NYC, $6M seed Mar 2026, Rally) | On-device photo verification in ~30ms on 6,000+ device types; POD, inspections, parking, e-com; tens of millions of images/month [S] | Delivery + mobility + e-com | Not stated | High in POD/gig. Owns the SDK slot in delivery apps |
| **Switch Labs VerifyAI** | Photo policy verification API at **$0.008/verification**; returns, POD; publishes "migrating from Captur" guide [S] | Yes (cheap, self-serve) | No | Price anchor. Shows the low end is near-free |
| **Succinct ZCAM** (Paradigm) | Cryptographic camera app + SDK (Apr 2026); markets insurance, delivery, marketplaces, KYC [S] | Yes (as SDK) | No | Medium. Crypto-native and free-ish |
| Attestiv ($8.4M) | Photo tamper scoring, Duck Creek / PCMS (insurance) [S] | Insurance | No | Low outside insurance |
| Forter / Signifyd / Riskified / Ravelin | Own the cross-merchant identity/behavior graph; Forter publishes the AI-damage-claims data [S]. **No image/capture product found** [S] | Retail | **Yes (person graph)** | High. One acquisition (Vaarhaft/Captur-sized) away; they own the buyer |
| Loop Returns | **AI Image Recognition** on shopper return photos (damage, tags, packaging, correct product) [S] | Returns only | Within Loop's merchant base (potentially) | High. Owns the photo upload step for Shopify brands |
| UPS Happy Returns | **Return Vision** AI matching of returned items to catalog + behavioral risk scoring; 10,000 drop-off locations (Apr 2026) [S] | Returns | Across hundreds of retailers | Medium. Mostly in-person inspection, not photos |
| Claimlane, Tavant, SymphonyAI, Delos | AI warranty agents with photo-manipulation checks and serial-fraud patterns [S] | Warranty | Within platform | Medium. Workflow owners bundle it |
| Inscribe / Resistant AI / Ocrolus | Document fraud. Resistant: $25M Series B Oct 2025, breakeven, 10x ARR since Series A [S] | Lending/banking-heavy | Yes (document network) | Medium for the "vendor docs" slice |
| Reality Defender / Hive | Detection APIs: ~$0.05/image (RD PAYG) and ~$0.003/image (Hive) [S, third-party listing] | Horizontal detection | No | Detection is commoditized |
| Google SynthID Content Detection API | Cloud API in partner preview; detects Google and "other popular models"; insurance fraud named as a use case [S] | Horizontal | n/a | Commoditizes server-side detection |
| ProxyPics / WeGoLook / DeGould / Ravin / Click-Ins / Tractable | Vertical capture/inspection networks (property, insurance, vehicles) | Vertical | Vertical | Own their verticals |

**Answer:** a horizontal, non-insurance, cross-company evidence network **is not white space**. Truepic is that product. Its weakness is price ($15-50 per inspection fits high-value claims, not $40 refunds) and a sales-led motion. That leaves a gap for a *low-cost, high-volume* tier, but the low end is already covered by Captur, Switch Labs ($0.008), Vaarhaft and Loop's built-in features.

---

## 3. Absorption: are Apple and Google making capture native and free?

| Platform | Status Oct 2026 | Implication |
|---|---|---|
| **Apple** | **Apple Reference Image** announced Sept 9 2026 with iPhone 18 Pro/Pro Max and iOS 27. Opt-in; sensor-signed second copy via Private Cloud Compute; 48MP main camera stills only; proprietary (not C2PA); **APIs for third-party apps** in iOS/iPadOS/macOS 27. Apple will also support SynthID [S] ([TechCrunch](https://techcrunch.com/2026/09/09/apple-has-a-new-way-prove-your-iphone-photos-arent-ai-slop/), [MacRumors](https://www.macrumors.com/2026/09/09/apple-reference-image/), [c2paviewer](https://c2paviewer.com/articles/apple-reference-image-vs-c2pa)) | Within ~3-4 years, a large share of US iPhone photos submitted as evidence can be checked for free against an Apple-rooted signature. Today it covers Pro models only and is opt-in, so the near-term installed base is small [I] |
| **Google** | Pixel 10 (Aug 2025): C2PA on **every** Pixel Camera JPEG, C2PA **Assurance Level 2** (Tensor G5 + Titan M2); Google Photos signs edits; developer blueprint + c2pa-android library using Keystore/StrongBox [S] ([Google blog](https://blog.google/security/pixel-android-trusted-images-c2pa-content-credentials/)) | Android follows on high-end silicon. Pixel's US share is small |
| Samsung | S25: C2PA only on AI-*edited* images, not normal captures [S]. No S26 capture-signing evidence found | Gap in Android mid-tier, which is where much fraud happens [I] |
| Qualcomm | Truepic library in Snapdragon [S/U on generation] | The silicon vendor's partner is the incumbent |

**Read:** absorption is **partial but decisive for the moat**. OEMs give away the trust root (device attestation and signed pixels). They will not build claim workflows, risk decisioning or a cross-merchant graph. So value moves to (a) orchestration and decisioning and (b) networks. That is where Truepic (Risk Network), Forter (person graph) and workflow owners (Loop, Tavant) already sit. The "hardened capture SDK" that was the founder's technical edge becomes a commodity on new phones and stays hard only on cheap Android and web, which is what Captur and Vaarhaft SafeCam already address.

---

## 4. Buyers, pricing and ARR math

**Buyer counts (US-first, rough) [I]:**

| Vertical | Buyers with meaningful photo-gated payouts | Realistic ACV | Integration point |
|---|---|---|---|
| E-com brands/retailers (>$50M online) | ~3,000-5,000 | $20-60K | Loop, Narvar, Shopify, Gorgias, Zendesk |
| Marketplaces (P2P, rental, gig, delivery) | ~300-600 | $100K-$1M | In-house trust & safety (prefer to build) |
| OEM warranty / recall programs | ~1,500 globally (>$20M warranty spend) | $100-300K | Tavant, Syncron/PTC, SAP, Claimlane, recall administrators |
| 3PL / carriers / last-mile | ~500-1,000 | $50-250K | TMS / driver apps (Onfleet, Bringg), already Captur territory |
| Proptech / equipment rental / auto marketplaces | ~1,000 | $25-150K | PMS, rental platforms, vehicle inspection vendors |
| Non-bank KYB / vendor onboarding docs | ~2,000 | $25-100K | Persona, Middesk, procurement suites, Inscribe/Resistant |

**Per-verification pricing:** the market spans **$0.003 (Hive detection) → $0.008 (Switch Labs) → $0.05 (Reality Defender) → $15-50 per inspection (Truepic)** [S]. A capture + network verdict for a refund realistically supports **$0.25-1.00** (round 17 estimate). Above ~$1, a $40 refund doesn't pay for it.

**ARR math at a blended $0.50 per verification [I]:**
- **$10M ARR** = 20M verifications/yr ≈ 60-80 mid-market brands + 5 OEMs + 2 marketplaces. **Feasible**: Captur already handles tens of millions of images a month at lower price points.
- **$50M ARR** = 100M/yr. Needs 2 large marketplaces or carriers *plus* hundreds of brands, i.e. two different integrations and sales motions.
- **$100M ARR** = 200M/yr. Needs presence in ≥3 verticals, each with its own workflow owner who can bundle a feature (Loop, Tavant, carrier apps). This is the F2/F1 trap: every vertical's system of record sees the flow first.

**Which vertical has the most urgency and the fastest pilot?** **Mid-market DTC brands on Shopify + Loop/Gorgias (damaged-on-arrival / keep-it refunds).** Reasons: the most public pain (Boll & Branch, Bogg, Ravelin 67%), decision-makers are reachable (Head of CX/LP), and a capture link can replace the upload step in days. But this is also the vertical where Loop (native AI image recognition), Vaarhaft (SafeCam) and Forter (the network) are already present, and the ACV is lowest. **OEM warranty** has better ACV and less crowding, but Truepic already has OtterBox and the recall channel, and dealer-network rollouts take months.

---

## 5. Moat analysis

| Claimed moat | Reality |
|---|---|
| Cross-company evidence graph (same photo at 5 merchants) | Real network effect in principle, but (1) perceptual-hash reuse is a commodity, (2) Truepic Risk Network already shares device/behavior flags across organizations, (3) Forter's cross-merchant *person/device* graph catches the same ring through identity, with better coverage, (4) image-reuse rates fall as fraudsters switch to fresh AI inpaints per claim, so the graph catches yesterday's fraud [I] |
| Device integrity / sensor / C2PA | Being commoditized by Apple Reference Image, Pixel AL2 and Snapdragon + Truepic |
| Behavioral biometrics during capture (Vara edge) | **The one real differentiator.** It answers "is a human live-capturing this, and is it the same person or device as prior fraud," which works even on cheap Android/web where OS attestation is weak. But it is a feature inside a capture flow, not a category. Truepic already uses "device and behavior" signals in its Risk Network [S] |
| Workflow lock-in | Owned by Loop, Tavant, carrier apps and marketplaces, not by the evidence vendor |

**Defensibility: 3/10.**

---

## 6. VC view

- **Could it be $10B?** Comps: Socure $5.2B on $364M ARR (Aug 2026) [S]; Persona $2B on ~$100M ARR (Apr 2025) [S]; Forter ~$3B (round 17 prompt, not re-verified) [U]. These are identity/transaction fraud platforms that sit on *every* transaction. Evidence verification happens only on the claim and dispute minority of transactions. The direct category leader, Truepic, has raised ~$36M in 9 years with no new round found since 2021 [S]. That is the strongest market-size warning: the category has been "obviously important" since 2018 and still has not produced a scaled company.
- **Exit shape:** most likely an acquisition by Forter/Signifyd/Riskified, Loop/Narvar, a warranty platform, or an IDV player (Persona/Socure/Veriff extending into "verified evidence"). That is a $100M-$1B outcome, not $10B [I].
- **Interesting / directional?** Directionally right ("evidence needs provenance") and the one-sentence pitch is clear. But "directionally right with a clear sentence and loud pain" is our own taxonomy's false-positive pattern #1 (loud pain = lagging signal) plus #2 (neutral cross-vendor layer beats the platform).

---

## 7. Finalist format

| Field | Content |
|---|---|
| One-line problem | Businesses pay refunds, warranty claims, delivery disputes and job completions based on photos and documents that GenAI can now forge in seconds, and after-the-fact detectors no longer work. |
| Why now | Photorealistic inpainting (2025-26); detectors below chance (Switch Labs, Aug 2026); Ravelin 67% of merchants hit; Forter calls it the fastest-growing return abuse; CPSC RFI on AI recall fraud (2026); OEM capture signing (Pixel 10, iPhone 18 Pro) makes provenance checkable. |
| Exact buyer | VP CX Ops / Loss Prevention (e-com); VP Warranty & After-sales (OEM); Head of Trust & Safety (marketplace); Director of Claims (3PL/carrier). |
| Exact ICP | US DTC brand, $100M-$1B online revenue, on Shopify + Loop/Gorgias, offering keep-it or damaged-on-arrival refunds above $50 AOV; or OEM with >$20M annual warranty spend paying on photo evidence. |
| Current workaround | Manual photo review; "send it back" requirements; Forter/Signifyd abuser scoring; Loop AI Image Recognition; Truepic Vision (high-value); Vaarhaft SafeCam; Captur (POD); policy tightening. |
| Why incumbents cannot easily own it | **They largely can.** Truepic already sells it horizontally with a network. Forter/Loop can buy or build a capture step. Apple/Google provide the trust root free. The only structural opening is price: Truepic's $15-50/inspection does not fit sub-$100 refunds. |
| 30-day MVP | Web capture link (no app) with live-capture check, Vara behavioral/liveness signals, C2PA / Apple Reference Image / Pixel verification when present, SynthID + detector ensemble as a secondary signal, perceptual-hash reuse graph across tenants, and a Loop/Gorgias/Shopify Flow app returning approve / step-up / deny. |
| Pilot design | 3 brands × 30 days. Week 1: back-test 12 months of claim photos for cross-brand reuse and synthetic flags. Weeks 2-4: route claims above $X through the capture link at 50% traffic; measure refund $ avoided, claim drop-off, CSAT. |
| Pricing hypothesis | $0.35-0.75 per verified capture; $1-3 for warranty/high-value; minimum $2K/month. |
| Expansion path | DTC returns → marketplaces → OEM warranty → POD/3PL → field service → (later) insurance via partners. Each step means a new workflow owner and a new competitor. |
| Moat | Cross-tenant reuse + device/behavior graph; behavioral-biometric liveness on web/low-end Android. Weak (3/10). |
| Why it could be $10B+ | Only if "verified evidence" becomes a universal step in every payout flow (a Socure for evidence). Not supported by evidence: the category leader is small after 9 years, and OEMs commoditize the core. |
| Direct competitors / adjacent threats | Truepic (Vision + Risk Network), Vaarhaft, Captur, Switch Labs, Succinct ZCAM, Attestiv, Claimlane/Tavant/SymphonyAI; Forter/Signifyd/Riskified/Ravelin; Loop, Happy Returns; Inscribe/Resistant AI; Reality Defender/Hive; Google SynthID API; Apple Reference Image; Pixel C2PA. |
| One sentence to a CFO | "Swap your 'upload a photo' step for our 20-second capture link and stop paying refunds and warranty claims on reused or AI-faked evidence, priced per check at under 1% of the claim." |
| 5 discovery questions | (1) What $ of refunds/claims last year were approved *only* on a customer photo, with no item returned? (2) How many AI-faked or reused photos did you catch in the last 90 days, and how did you catch them? (3) Have you evaluated Truepic, Vaarhaft, Captur or Loop's image AI, and why didn't you buy or roll it out? (4) What claim drop-off would you accept from adding a live-capture step for claims above $X? (5) Would you share hashed claim images and device signals into a cross-merchant network, and would legal approve it? |
| Hard kill criteria | (a) <3 of 10 ICP brands quantify photo-only refund fraud ≥$250K/yr; (b) back-test shows <1% of photo-gated claim $ on reused or synthetic evidence; (c) ≥3 of 10 already use or have trialed Truepic/Vaarhaft/Loop image AI and are satisfied; (d) <2 of 10 will pay ≥$0.30/verification; (e) Forter/Signifyd/Loop ships capture within 6 months. **(c) and (e) are partly met on public evidence:** Loop has native image AI; Truepic is in warranty/recall. |

---

## 8. Scores (bar: average ≥8.5, none <7)

| Category | Score | Why |
|---|---|---|
| Pain | 7 | Real and measured (67% of merchants), but per-incident $ are small for most |
| Urgency | 6 | Growing fast from a small dollar base; not yet a CFO line item (round 17: absent from earnings calls) |
| ROI clarity | 6 | Fraud avoided vs. claim friction; reuse is easy to measure, synthetic is hard |
| Customer accessibility | 7 | CX/LP heads reachable; Shopify app distribution |
| Pilot speed | 7 | Capture link swap is fast; back-test needs data access |
| Market size | 6 | Photo-gated payouts are ~10x smaller than headline fraud numbers |
| Expansion | 6 | Each vertical needs a new workflow integration and has a new incumbent |
| Venture potential | 5 | Leader small after 9 years; likely an M&A outcome |
| Defensibility | 3 | OEM trust root free; hash graph copyable; Truepic network exists |
| Why now | 8 | Strongest category: generators + detector failure + Apple/Google signing |
| Competition position | 3 | Truepic is this thesis already; Captur/Vaarhaft/Loop cover the low end |
| **Average** | **5.8** | Fails the bar in 9 of 11 categories |

**Classification: KILL.** Causes: **F2** (visible-pain race: Captur seed Mar 2026, ZCAM Apr 2026, Switch Labs, Vaarhaft, Loop features, Truepic expansion into warranty/recall) + **F1** (Apple Reference Image, Pixel C2PA, SynthID API, Qualcomm) + **F4** on the defensible slice. **Not B**: the space is neither unresolved nor too early for public evidence. Evidence is abundant, and it shows a funded, horizontal incumbent with a network.

---

## 9. The 14-day test (if the founders still want to rule it in or out cheaply)
The goal is to falsify the two claims that would revive the thesis: (i) cross-merchant reuse is large, and (ii) Truepic's price leaves a high-volume gap that buyers will pay to fill.
1. **Days 1-3:** Contact 15 Shopify/Loop brands ($100M+ online, AOV >$50) through Loop/Gorgias partner channels and Vara's network. Ask questions 1 and 3 from §7.
2. **Days 3-10:** Get **12 months of photo-gated claim images + order metadata from ≥3 brands** (NDA, hashed export). Run perceptual-hash reuse across brands, stock/marketplace-listing image matches, SynthID/C2PA checks and an ensemble detector. Report reuse and synthetic flags as % of claim dollars.
3. **Days 8-14:** Offer a paid 60-day pilot at $0.50/verification with a $2K/month minimum.
- **Pass (reopen as B):** ≥2 signed paid pilots **and** cross-brand reuse/synthetic ≥2% of photo-gated claim $ **and** ≥2 brands say they rejected Truepic/Vaarhaft on price or friction (not "never heard of it").
- **Fail (stay KILLed):** any one of these: <2 pilots; cross-brand reuse <1% of claim $; prospects say Loop's built-in image AI or Forter is "good enough."

---

## 10. Residue worth keeping (not a thesis)
- **Vara as a supplier, not a category creator:** sell *behavioral-biometric liveness for capture flows* (web/low-end Android, where OS attestation is missing) as an OEM signal to Truepic, Captur, Vaarhaft, Loop or Forter. That is a partnership or acquisition path that uses the founder edge without fighting the network incumbents.
- **Watch item:** if Forter/Signifyd have still not shipped any evidence-capture product by mid-2027 and Truepic stays priced per inspection, the "per-check, Shopify-native capture + cross-merchant reuse" slot may still be open. Re-test then.

---

## Sources (all from search snippets; WebFetch was blocked)
- Retail Gazette, Jun 2026: https://www.retailgazette.co.uk/blog/2026/06/retailers-face-surge-in-ai-generated-fake-damage-claims-and-refund-scams/
- Modern Retail, Mar 2 2026: https://www.modernretail.co/technology/from-boll-branch-to-bogg-brands-are-battling-a-surge-of-ai-driven-return-fraud/
- Practical Ecommerce: https://practicalecommerce.com/ai-makes-refund-evidence-easier-to-fake
- Ravelin/BRC 2026: https://brc.org.uk/news-and-events/news/associate-insight/2026/the-state-of-refund-abuse-repeat-offenders-eroding-loyalty-and-ais-impact/ ; https://retailtechinnovationhub.com/home/2026/9/21/ravelin-research-flags-the-rise-of-the-refundjacker-as-dishonesty-becomes-normalised-among-shoppers
- Switch Labs: https://www.switchlabs.dev/post/ai-image-detectors-damage-claims ; https://www.switchlabs.dev/post/ai-faked-damage-photos-playbook ; VerifyAI: https://www.switchlabs.dev/verify-ai ; https://verify.switchlabs.dev/docs/guides/migrating-from-captur
- Stripe refund abuse: https://stripe.com/gb/resources/more/refund-abuse
- Claimlane: https://www.claimlane.com/resources/blog/warranty-fraud-explained ; https://www.claimlane.com/resources/blog/ai-warranty-fraud-detection-ecommerce
- Foley, Jul 2026: https://www.foley.com/insights/publications/2026/07/when-recalls-go-rogue-the-impact-of-ai-fueled-recall-fraud/ ; NAM: https://nam.org/nam-to-cpsc-take-action-on-recall-fraud/
- Truepic: OtterBox https://www.truepic.com/blog/truepic-otterbox-partner ; https://coverager.com/otterbox-adopts-truepic-for-warranty-claims/ ; Risk Network https://www.globenewswire.com/news-release/2025/09/25/3156416/0/en/Truepic-Introduces-Groundbreaking-Risk-Network-for-Mitigating-and-Preventing-Fraud-Across-the-Financial-Sector.html ; Recall Results https://truepic.com/blog/truepic-and-recall-results-partner-to-innovate-product-recall-with-image-authentication-technology ; pricing https://truepic.com/pricing/vision ; Series B https://www.truepic.com/blog/truepic-raises-26-million-series-b-financing-led-by-m12-microsofts-venture-fund-to-scale-worlds-most-secure-camera-technology ; newsroom https://www.truepic.com/company/newsroom
- Captur: https://pulse2.com/captur-6-million-raised-for-on-device-ai-image-verification-platform ; https://raising.fi/news/captur-seed-march-2026
- Vaarhaft: https://www.vaarhaft.com/blog/ecommerce-return-fraud-trends ; https://www.vaarhaft.com/blog/fake-airbnb-damage-photo-fraud ; https://pitchbook.com/profiles/company/606978-28
- Attestiv: https://www.cbinsights.com/company/attestiv ; https://www.duckcreek.com/blog/attestiv-photo-authenticity-and-fraud-protection-now-available-to-duck-creek-partner-ecosystem
- Succinct ZCAM: https://blog.succinct.xyz/introducing-zcam/ ; https://biometricupdate.com/202604/zcam-app-brings-cryptographic-proof-to-photos-for-kyc-fraud-use-cases
- Loop AI Image Recognition: https://help.loopreturns.com/en/articles/9565825 ; Happy Returns: https://www.retaildive.com/news/ups-happy-returns-vision-software-pilot-everlane/809083/ ; https://www.businesswire.com/news/home/20260421965642/en/UPS-and-Happy-Returns-Cement-Position-as-Largest-Box-Free-Label-Free-Return-Network-with-Expansion-to-10000-U.S.-Locations
- Inscribe: https://www.inscribe.ai/blog/1-in-16-documents-flagged-as-fraudulent-inside-our-2026-report ; https://www.inscribe.ai/blog/reports-ai-document-fraud-mid-year-2026
- Resistant AI: https://coverager.com/resistant-ai-raises-25-million/
- Apple Reference Image: https://techcrunch.com/2026/09/09/apple-has-a-new-way-prove-your-iphone-photos-arent-ai-slop/ ; https://www.macrumors.com/2026/09/09/apple-reference-image/ ; https://c2paviewer.com/articles/apple-reference-image-vs-c2pa
- Google Pixel C2PA: https://blog.google/security/pixel-android-trusted-images-c2pa-content-credentials/ ; c2pa-android: https://opensource.contentauthenticity.org/docs/c2pa-android
- Samsung S25 C2PA: https://www.phonearena.com/news/ai-edited-photos-about-to-expose-themselves-as-samsung-expands-this-galaxy-s25-feature-to-millions-older-phones_id173556
- SynthID API: https://infoq.com/news/2026/05/google-synthid-content-detection
- Incidents: DoorDash https://www.cxodigitalpulse.com/?p=42336 ; Lyft https://aiweekly.co/alerts/lyft-bans-driver-who-used-gemini-to-fake-damage-photos ; Airbnb https://incidentdatabase.ai/cite/1161/ ; Vinted https://oecd.ai/en/incidents/2026-03-02-16b3
- Detection pricing (third-party listing, unverified): https://toolradar.com/tools/reality-defender
- Socure: https://ffnews.com/news/socure-hits-52b-valuation-with-strategic-investment-and-fravity-acquisition ; Persona: https://siliconvalleyinvestclub.com/companies/withpersona/

## Caveats
- Photo-gated share of refunds (5-15%) and buyer counts are our inferences, not sourced.
- The Truepic "June 2026 TechCrunch / 300% growth / Snapdragon 8 Gen 5" snippet may be mis-dated recycled coverage [U].
- Forter's ~$3B valuation was not re-verified. No Forter/Signifyd image-capture launch was found, but absence in search results is weak evidence.
- Vendor-sourced fraud rates (Claimlane $45B, Switch Labs) have commercial bias.
