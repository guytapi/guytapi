# 14-Day Test Plan: Caller Verification for AI Voice Front-Doors

**Status:** best founder-specific wedge found (thesis Z reframe, avg 5.6). **Not a winner.** This test exists to find out quickly whether real-world evidence moves it above the bar, or kills it.

## The hypothesis in one sentence
"AI agents now answer support lines, and fraudsters now call them with cloned voices and AI callers. Before your AI agent does anything risky (port a number, swap a SIM, move loyalty points), it calls our `verify_caller` tool, and we tell it in two seconds whether to proceed, challenge or block."

## Why this wedge (and not the broad thesis)
- Uses all four components Vara has already built: voice deepfake analysis, challenge-response with per-tenant session tokens, web behavioral capture (via an SMS link sent mid-call), and the rules engine.
- Avoids the crowded web/bot channel (DataDome, HUMAN, Kasada) and checkout (Forter, Riskified).
- Attacks Pindrop's weak spot: enterprise-only sales, no self-serve developer motion inside voice-AI platforms.

## Who to contact (15 conversations)
| Segment | Target role | # calls | Where to find them |
|---|---|---|---|
| Telecom / MVNO | Head of Fraud, Head of Care Operations | 6 | LinkedIn: "fraud" + carrier/MVNO names; CTIA and GSMA fraud groups |
| Travel loyalty (airlines, hotel groups) | Loyalty fraud lead, Director of Contact Center | 4 | LinkedIn; loyalty fraud conference speaker lists |
| Voice-AI platforms (Vapi, Retell, Bland, Synthflow, PolyAI, Parloa) | CTO, Head of Partnerships | 5 | Direct outreach; their partner programs |

## Cold message (3 sentences)
> Your support line is now answered by an AI agent, and 1 in 106 calls reaching it isn't a live human. Before that agent ports a number or moves loyalty points, it can call one API that checks the voice, challenges the caller if needed, and returns proceed / challenge / block in about two seconds. Can we back-test it on 30 days of your recordings and show you what slipped through?

## What to ask (no "would you use this?")
1. "In the last 90 days, how many confirmed fraud cases started with a phone call? What did they cost?" (Ask for the number, not an opinion.)
2. "How many of those involved a synthetic voice, an AI caller, or a scripted bot?"
3. "What do you use today to verify callers before a high-risk action? What does it cost per call?"
4. "Have you evaluated Pindrop? What stopped you, or what do you pay?"
5. "Can we run a back-test on 30 days of call recordings plus your confirmed-fraud labels, under NDA?"
6. For voice-AI platforms: "Do your customers ask for caller verification? Would you list a `verify_caller` tool in your marketplace or partner program?"

## Pass criteria (all must hold)
- **3 or more** organizations agree to a back-test on 30 days of recordings, or to a shadow pilot.
- **1 or more** says Pindrop is too expensive, too slow to integrate, or not available to them.
- **1 or more** voice-AI platform agrees to a partner integration or co-marketing.
- In back-tests: synthetic/bot signals explain **at least 10%** of confirmed phone-originated fraud.

## Kill criteria (any one)
- Fewer than 2 organizations will share recordings.
- Back-test shows synthetic/bot signals explain under 10% of confirmed fraud.
- Pindrop (or a peer) launches a self-serve API or a Vapi/Retell-style integration with step-up during the test.
- Voice-AI platforms say they will build caller verification natively.

## What would move it toward the bar
- Evidence that losses per carrier from port-out/SIM-swap via AI callers exceed $1M/yr (raises Pain and ROI to 9).
- Two voice-AI platforms willing to distribute it (raises Customer accessibility and Pilot speed to 9).
- A consortium effect: the same cloned voice or AI-caller fingerprint seen across 2+ customers in back-tests (raises Defensibility and Venture potential).

## Day-by-day
| Days | Action |
|---|---|
| 1-2 | Build target list of 60 names; send cold messages; package a demo `verify_caller` endpoint using existing voice-intelligence + challenge APIs |
| 3-7 | Run first 8-10 calls; request recordings and fraud labels under NDA |
| 8-11 | Run back-tests on any data received; finish remaining calls |
| 12-13 | Score against pass/kill criteria; re-score the 11 bar categories with real evidence |
| 14 | Decide: advance to paid pilot, reframe, or kill |
