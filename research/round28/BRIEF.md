# Round 28 brief (shared by all agents)

Founder instruction: take the hidden-failure hypotheses in research/discovery/DISCOVERY_MACHINE.md (H1-H10) and ask: "What product would need to exist if this hidden failure becomes 10x worse over the next 2-3 years?" Output must be STARTUP THESES, not discovery plans. Do not recommend interviews.

Method for each hypothesis:
1. Push to the extreme future state (companies run hundreds/thousands of agents, 2028-2029).
2. Identify second- and third-order consequences; do NOT solve the obvious surface pain.
3. Ask whether a consequence creates a completely new infrastructure category.
4. Search for evidence the underlying behavior is starting NOW (internal workarounds, job posts, eng blogs, architecture writeups, pricing changes).
5. Search aggressively for competitors; if the obvious product exists, move one layer deeper.
6. Prefer a required infrastructure layer over a productivity feature.
7. Prefer a simple 30-day wedge that expands into something every AI-native company needs.
8. Banned (already killed): generic coding agents, generic agent orchestration, generic observability, generic evals, generic AI security, generic context management, generic company OS, generic self-driving R&D, generic agent identity — plus everything in research/STATUS.md.

Infer from internal-workaround signals, architectural necessity, economic incentives and where current systems break at 100x scale. Do not stop because public evidence is incomplete.

Bar: A = avg ≥8.5 with no category <7 across Pain, Urgency, ROI clarity, Customer accessibility, Pilot speed, Market size, Expansion, Venture potential, Defensibility, Why now, Competition position. B = so early that absence of competitors is itself plausible, with a precise explanation of why it could become a $10B+ infrastructure company.

Deliver each thesis in the finalist format of research/round18/FINALIST_FORMAT.md (one-line problem, why now, exact buyer, exact ICP, current workaround, why incumbents cannot own it, 30-day MVP, pilot design, pricing hypothesis, expansion path, moat, why $10B+, competitors & adjacent threats, one-sentence CTO pitch, hard kill criteria, 11 scores) — omit the "customer discovery questions" item.

H1: AI app companies whose human supervision, exception handling, QA, escalation and recovery costs grow linearly with customer volume. Candidate deeper layers to explore (not limited to): autonomous exception resolution, machine-verifiable work, human escalation markets, agent quality guarantees, autonomous service delivery, agent operations infrastructure, something not yet named.
H2: Agent output nobody triages: background agents create a growing pile of half-finished PRs, duplicate/conflicting work and abandoned branches; nobody owns the queue of agent output.
H3: Incidents in code no human understands: as agents author more production changes, incident response slows; no human owner; MTTR rises.
