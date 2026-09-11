---
last_updated: 2026-09-09
type: internal
attendees: [Marek Pillár, Jindřich Tůma]
tldv_link:
---

# Logistics & CC Roadmap Presentation Prep

**Date**: 2026-09-09
**Attendees**: Marek Pillár (PM), Jindřich Tůma (PM/coordination lead)
**Type**: internal
**Recording**: N/A (transcript provided as text, no tldv link)
**Previous session**: N/A — new thread (related to the still-open "present the finished roadmap to the client" action item from 2026-09-02/2026-09-03)
**Meeting prep**: N/A

## TL;DR

Marek walked Jindřich through his plan for tomorrow's roadmap presentations to the Logistika and CC teams — showing each audience only its relevant slice of the roadmap board, with comments and MVP estimates already in place. Jindřich approved the overall approach but flagged a real gap: the board has no timeline, and man-day figures mean nothing to business stakeholders like Tereza Foltová without a calendar view — Marek agreed to build one before tomorrow. Jindřich also asked Marek to start capturing business value as concrete numbers (not vague qualitative claims) as he begins 1:1s with domain experts across the portfolio starting next week.

## Key Discussion Points

### Tomorrow's roadmap presentations (Marek Pillár, Jindřich Tůma)

Marek plans to show the roadmap board filtered per audience rather than build separate decks: Logistika (reklamace, fakturace doprav) in the morning, CC (Max Chatbot, Maxie, Lexie) later in the day. Each item already carries a comment and, where possible, an MVP estimate — Marek noted that "if everything goes smoothly for reklamace, Filip could finish it in one day," with several items already in progress (shown yellow) and remaining blockers documented with reasons pulled from earlier dev meetings `[translated from Slovak]`. He expects developers to also be present tomorrow so they can speak to blocked items directly rather than relying on him or Filip alone.

Jindřich confirmed the plan is clear and sufficient ("za mňa to ukazuje všetko, čo potrebujeme my, všetko, čo potrebujú oni" — "for me it shows everything we need, everything they need" `[translated from Slovak/Czech]`) and expects the Logistika session to move quickly since Tereza Foltová was the primary requester and reklamace largely covers what she asked for. For CC, he wants less time spent on the roadmap walkthrough itself — the session is only ~1 hour and its main purpose is reviewing testing feedback with Kateřina Karlecová toward a production decision. He suggested reserving only the last ~15 minutes for the roadmap, mainly so Karlecová can see and scroll through it.

Marek's export approach: he pushed the roadmap into Figma so he can capture live comments from both meetings in real time, then export a static PNG/PDF afterward to email back to attendees along with whatever gets agreed on the calls.

### Closing the current MVP phase (Marek Pillár)

Marek framed both sessions around a broader goal: closing the current MVP phase before opening the next one requires testing with the client, collecting feedback through an established channel, and triaging what's a change request (in/out of original scope) versus a genuinely new feature. Only after that should a Discovery session with a domain expert on the client side kick off the next phase — Marek wants to ask Logistika tomorrow who that domain expert is for reklamace, aiming to start Discovery next week.

### Chatbot, Maxie, Lexie framing for CC (Marek Pillár)

Marek plans to explain to CC that Maxie's man-day figures look large mainly because the project hasn't really started yet — capacity has gone to the chatbot first — but the estimate should come down substantially since Honza Zelený can reuse most of what Jura Brázdil already built for the chatbot (shared "brain"/logic, not incidental overlap). Lexie still has no estimates at all, pending Viliam Gago's return from vacation.

Marek also wants to reframe the overall narrative from last time's sentiment ("finally we're seeing something from you" `[translated from Slovak]`) toward showing concrete delivered progress and shifting the conversation to value and KPIs per initiative going forward.

### Business value quantification (Jindřich Tůma)

Jindřich's one substantive ask: whenever Marek meets domain experts going forward, he needs to come back with a **business quantification in concrete numbers**, not just a qualitative reason for why a project matters — enough that a non-technical, "economically competent" person could look at it and understand the value, and enough that BigHub can measure against it once delivered. He suggested starting with CC, since those projects deliver within two weeks. Example given: "we save 3 minutes per case" translated into an actual cost figure via average wage rate `[translated from Czech]`.

Marek proposed handling this two ways: hard numbers where data exists, and a hypothetical framing ("if we roll MaxBuddy out everywhere, we expect X") where it doesn't yet — but agreed the end state should be numeric either way. His personal goal is to fill in the roadmap Excel's "Strategy" tab (Value + KPI per initiative) and meet 1:1 with each domain expert to gather this and confirm names/expectations/timelines — avoiding the current problem of information being scattered across streams with no single place to find it. Petr Neuman for Listing is the one contact he already has confirmed.

### Domain-expert meeting cadence (Jindřich Tůma)

Jindřich wants to join only the very first MaxBuddy-related domain-expert meeting, to introduce a separate topic he needs to kick off personally — after that, Marek can run subsequent meetings solo. For CC, Marek can schedule freely without Jindřich. Jindřich asked to always be told in advance whenever Marek books one of these meetings, so he can feed in anything relevant beforehand.

### Missing timeline view (Jindřich Tůma)

Jindřich's main pushback on the roadmap board itself: at a high level it's great, but a phase estimate like "MVP in one man-day" is meaningless to someone like Tereza Foltová without a real calendar attached — a mandate could mean a week or much longer in wall-clock time. He asked Marek to prepare a simple table before tomorrow: item names on the left, a monthly time axis on the right, with filled-in cells marking when testing happens, when bugs get fixed, and when rollout lands — nothing elaborate, just visually clear enough that Tereza can see "testing starts here, we have 3 days for it." He expects reklamace to be quick to plot since UAT is essentially the client testing the reklamace workflow itself, followed by the email-draft and data-connection work.

Marek's plan to build this: use today's 3pm internal meeting (where the wider dev team will be present) to ask each developer directly for realistic testing/rollout timing rather than estimate it himself — he was explicit that he doesn't feel confident making that call solo.

## Decisions Made

- Tomorrow's roadmap walkthroughs will be split by audience from the same underlying roadmap board rather than built as separate decks: Logistika in the morning (reklamace, fakturace doprav), CC later (~1 hour, focused mainly on reviewing chatbot/Lexie testing feedback, with only the last ~15 minutes on the roadmap, primarily for Kateřina Karlecová's visibility).
- Closing the current MVP phase and opening the next requires, in order: client testing, feedback collection via an established channel, and change-request/new-feature triage against the original spec — only then does a Discovery session with a client-side domain expert start the next phase.
- Business value for each initiative must be captured in concrete, measurable numbers (not vague qualitative claims), starting with CC initiatives since they deliver within two weeks — Marek will track this in a new Value/KPI ("Strategy") tab on the roadmap Excel.
- Domain-expert engagement model: Jindřich joins Marek only for the first MaxBuddy 1:1 (to introduce a separate topic); all other domain-expert meetings run solo by Marek, who keeps Jindřich informed whenever one gets scheduled.
- A calendar/timeline-style view (item name + filled time-axis cells for testing/bugfix/rollout) is needed alongside the existing MD-estimate roadmap board, since raw man-day figures aren't meaningful on their own to non-technical business stakeholders.

## Action Items

- [ ] **Marek Pillár**: Present the roadmap board to the full dev team at today's 3pm internal meeting and ask each developer directly for realistic testing/rollout timing input — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Marek Pillár**: Build a simple calendar-style timeline table (item name + filled time-axis cells for testing/bugfix/rollout) for the Logistika and CC items, using input from today's 3pm meeting, ready before tomorrow's client sessions — due 2026-09-09 (before 2026-09-10) — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Marek Pillár**: Lead tomorrow's Logistika roadmap walkthrough (reklamace + fakturace doprav) — due 2026-09-10 — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Marek Pillár**: Lead tomorrow's CC session — prioritize reviewing chatbot/Lexie testing feedback with Kateřina Karlecová, reserve only the last ~15 minutes for the roadmap — due 2026-09-10 — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Marek Pillár**: Capture live comments from both meetings in the Figma export of the roadmap, then export as PNG/PDF and email back to attendees with what gets agreed — due 2026-09-10 — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Marek Pillár**: Ask the Logistika team tomorrow who the domain expert is for reklamace, to start a Discovery session next week — due 2026-09-10 — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Marek Pillár**: Fill in the roadmap Excel's "Strategy" tab with Value + KPI columns per initiative — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Marek Pillár**: Schedule and hold 1:1s with each project's domain expert next week (starting with CC contacts and Petr Neuman for Listing) to confirm identities/expectations/timelines and gather concrete business-quantification numbers — due week of 2026-09-14 — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Marek Pillár**: Notify Jindřich Tůma in advance whenever a new domain-expert meeting is scheduled — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Jindřich Tůma**: Create two separate recurring calendar invites for himself — one for Logistika, one for CC — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] **Jindřich Tůma**: Join Marek for the first MaxBuddy domain-expert meeting to introduce a topic he needs to kick off personally — due week of 2026-09-14 — from 2026-09-09-logistics-cc-roadmap-presentation-prep

## Open Questions

- Whether Reklamace's "~1 day to finish MVP if everything goes smoothly" estimate (Marek's own read, not yet confirmed by Filip Černý directly) should be reflected in the roadmap board/Excel.

## Sentiment & Tone

Collaborative, low-friction internal planning call. Jindřich was consistently affirming of Marek's approach ("za mňa je to přehledný... paráda... super"), with his only real pushback being constructive — the missing timeline view — which Marek accepted without resistance. Marek was candid about his own uncertainty on estimating dev timing solo and proactive about closing the gap (asking devs directly rather than guessing). Overall an aligning, forward-planning tone rather than a status-review one.

## Routing Log

Confirmed 2026-09-09 (all items). Written:
- **project-assumptions**: ASM-046 (MVP-phase exit criteria), ASM-047 (business-value quantification), ASM-048 (domain-expert engagement model), ASM-049 (roadmap presentation split), ASM-050 (timeline-view requirement)
- **project-stakeholders**: enriched STK-003 (Jindřich Tůma), STK-013 (Tereza Foltová), STK-037 (Kateřina Karlecová)
- **project-daily** (2026-09-09): 11 action items added
