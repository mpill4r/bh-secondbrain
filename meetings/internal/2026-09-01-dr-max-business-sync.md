---
last_updated: 2026-09-01
type: internal
attendees: [Marek Pillár, Jindřich Tůma, Ján "Honza" Kabát]
tldv_link:
---

# Dr. Max — Regular Business Sync

**Date**: 2026-09-01
**Attendees**: Marek Pillár (Product Manager), Jindřich Tůma (Project Manager / AI Manager), Ján "Honza" Kabát (Head of Sales — present but not represented in the transcribed dialogue)
**Type**: internal (business sync — BigHub-only)
**Recording**: N/A
**Previous session**: N/A (first recurring instance captured)
**Meeting prep**: N/A

## TL;DR

Recurring BigHub-internal sync on the Dr. Max account: Jindřich reported his onboarding progress (MVP-framing approach, first stabilized project, colour/branding alignment with Dr. Max's Martová/Mertová), MaxBuddy was confirmed delivered and moved into ongoing product-development mode, and both agreed the account badly needs a real backlog/PM tool (no JIRA available) plus a clean, consistently-structured spec format across all projects. Marek pitched two new angles — consolidating all AI initiatives into one story to unlock Microsoft "Partner-led"/"Field-led" funding, and using a split Excel (business view + dynamic roadmap) to win Dudaško over — both landed well with Jindřich, who wants to finalize the roadmap split by Wednesday.

## Key Discussion Points

### Jindřich's onboarding & MVP framing approach

Jindřich said access to most projects came quickly; he still needs deeper technical access (e.g. TEO). His working principle: most projects can, in the end, be delivered — the job is to frame them as an MVP, hold a firm narrow through-line to deployment, and park anything extra as a follow-on "expansion package" rather than let scope creep block the first release. Example: the chatbot got briefly derailed when a tender for graphics/logo work appeared — the team politely acknowledged it and kept it out of the MVP.

He also coordinated with **paní Martová/Mertová** (name spelled two ways in the transcript — same person, spelling unconfirmed) on Slovak Dr. Max branding: pick one visual direction, let it be voted on, then apply variants once a winner is chosen. She agreed.

> "Achilova pata" of these projects, per Jindřich, is that they start from a rough spec, and reality (other systems, other integrations) always reshapes it during build — the goal is a solid-enough MVP without letting rediscovery stretch delivery 3-4 months out, while still handling the business side properly. Deviations from spec are fine if justified and explained back to the stakeholder — the customer's trust holds as long as they feel informed.

### Voicebot infra blocker (Atlantis)

A Thursday meeting with **Atlantis** (infra/access vendor) confirmed no blocker in principle — they just need the list of required access/`prostupy` for Max infra. Promised Thursday, chased again Friday and today — still outstanding. Jindřich sees no reason (technical contact at Dr. Max or at Atlantis) to expect this to actually stall, but flagged it as a live risk if access keeps slipping.

### MaxBuddy status — delivered, now in product-development mode

Jindřich and **Alana** (business owner) aligned Friday: MaxBuddy is treated as delivered, with the first batch of post-launch improvements already released and accepted. Going forward, Jindřich (acting in a role referred to only as "TMK" — acronym not explained in the transcript) will always accept these change batches himself, since this is now product development, not implementation.

Marek flagged the underlying governance problem: there's no formally closed/accepted project boundary, so it's unclear what counts as "in the original scope" vs. new work, which complicates how it's funded (currently via "TNK," a mechanism that partly conflicts with how a regional contact — referred to only as "Ono" — expects it to work). Jindřich agreed this same gap exists across other projects (incl. "Max Barim") and said he's already raised with BigHub's **Jakub Válek** that the account needs a real backlog/prioritization tool so that whatever Dudaško (or anyone) prioritizes has somewhere to land, get estimated, and be tracked.

### No PM tool on the account

Dr. Max has no JIRA — only DevOps and Teams, neither well suited to this. Jindřich would like JIRA (or equivalent); BigHub's own **Easy Project** also isn't a good fit. Work is currently scattered across Teams channels per topic, with no single owning thread. Marek separately noted their own internal process is to funnel everything through one channel, then thread-by-thread underneath — a possible model to borrow. Not solved yet.

### Roadmap Excel restructuring

Jindřich reviewed the roadmap Excel Honza Sovka produced and now understands its structure. He wants to propose to Dudaško that it be split into two documents:
1. **Business view** — of ~30 AI initiatives, 7 are actually launched, showing current state and deadlines.
2. **Actual roadmap** — more dynamic; Jindřich isn't convinced Excel is the right medium long-term and is considering a platform instead.

This split will be the first thing he and Marek work on together, targeted for **Wednesday this week** — the first artifact Dudaško will actually see, since no presentation meeting with Dr. Max has happened yet (everything so far has been trial/exploratory). A second phase of changes Jindřich already has in mind will be held back until Dudaško is comfortable with phase one.

Marek's read: Dudaško personally cares about follow-through and reportedly complained that **Luky, Lomano, and especially Alana** didn't keep the existing Excel maintained, even though it mattered to him. Marek's suggestion: splitting the sheet into the specific value dimensions Dudaško actually tracks (a handful of tabs) would likely delight him.

### Microsoft funding angle (Marek's proposal)

Marek raised that Microsoft's new Penta-wide contract gives brands funding based on how well they demonstrate workload/velocity readiness — decision-maker is **pan Lala** in Operations at **Pentagru** (the parent group). Dr. Max's brands (across ~6 countries + 2 DZ, sibling brands include Fortuna and Uber) operate autonomously and compete individually for this budget, so nobody is currently making one consolidated case.

Marek's idea: define what they want to do over the next 12 months, plus not-yet-started initiatives, and show the **ACR (Azure Consumption Revenue) uplift** — a story no single brand in the group has assembled. He noted Microsoft is already "scouting" this opportunity. He also referenced Dudaško reportedly saying he has "60 news cases on a napkin" with no consolidated view — compiling one master list would be both a concrete win to celebrate with Dudaško and the raw material for the Microsoft pitch, potentially funding an extra FTE (or more) per year even on a modest ask.

Jindřich separately explained Microsoft's two funding tracks: **Partner-led** (BigHub, as a Microsoft partner, unlocks project funding by meeting expected-spend conditions) and **Field-led** (Microsoft's own reps decide funding directly) — they're currently pursuing **Field Lab** funding tied to this. There's also **Partner Lab** money that could raise margin. Marek noted this funding could either be passed to the client as more delivered value or kept to improve BigHub's own profitability — both useful, and not mutually exclusive.

### Consistent spec structure going forward

Jindřich wants every project spec to follow the same shape from now on: a **business-language intro** (readable by both business and technical people), followed by a **BAU justification** section — why this project, framed in time/cost terms (e.g. "saves 3 minutes per request × request volume"), and a matching **success-measurement** section at the end (e.g. validating that 95 of 100 cases actually used the chatbot). The product owner should own and push these numbers to the business.

He's already agreed this structure with **paní Martová/Mertová**, who owns three projects (Max, Maxie, Lexie). Honza Sovka's original specs are solid on content but were built under time pressure without a consistent shape — Jindřich wants Marek to own making sure every spec has a coherent "head and tail."

### Adoption / newsletter

Marek is connecting Jindřich with **Soňa** to own a newsletter highlighting wins (she's somewhat reluctant — not her core job — but will be supplemented). Marek will draft the first post himself, then look at automating a monthly cadence. Jindřich hasn't started the wider adoption campaign yet but has already spoken with **Kateřina Leš**, who's tried something similar in another country — a coffee/comparison session is planned. Marek separately mentioned **Paťanda** favorably as someone doing good work worth learning from.

## Decisions Made

- MaxBuddy is treated as delivered; all further work is product development, and Jindřich will personally accept future change batches.
- Roadmap Excel will be split into a business-facing view (initiative status/deadlines) and a separate, more dynamic roadmap — target Wednesday this week, before any Dudaško-facing presentation.
- All Dr. Max project specs must follow a consistent structure: business intro → BAU/cost-time justification → (at close) success measurement against that justification.
- Colour/branding for Slovak Dr. Max: get a single direction approved first, then generate variants — agreed with paní Martová/Mertová.

## Action Items

- [ ] **Jindřich**: Finalize the AI initiatives list and split the roadmap Excel (business view + roadmap) — due 2026-09-03 (Wednesday) — from dr-max-business-sync
- [ ] **Jindřich**: Sync with Dudaško this week on what has/hasn't played out, and share the go-forward vision — due -tbd- — from dr-max-business-sync
- [ ] **Marek**: Verify with Alana whether MaxBuddy is formally accepted by Tomáš Dudaško — due -tbd- — from dr-max-business-sync
- [ ] **Marek**: Close out the "8K" item with the Operations contact — due this week — from dr-max-business-sync
- [ ] **Jindřich**: Chase Atlantis for the outstanding infra access list blocking the voicebot — due -tbd- — from dr-max-business-sync
- [ ] **Jindřich**: Review TVXLu and send the file to Marek — due -tbd- — from dr-max-business-sync
- [ ] **Jindřich**: Roll out the consistent spec structure (business intro + BAU + success measurement), starting with Martová/Mertová's Max/Maxie/Lexie projects — due -tbd- — from dr-max-business-sync
- [ ] **Marek**: Draft the first adoption newsletter post, then evaluate automating a monthly cadence — due -tbd- — from dr-max-business-sync
- [ ] **Jindřich**: Meet Kateřina Leš to compare adoption/newsletter approaches across countries — due -tbd- — from dr-max-business-sync

## Open Questions

- What does "TMK" (the role/mechanism under which Jindřich now always accepts MaxBuddy changes) actually stand for?
- Who is "Ono" (the regional contact whose funding expectations partly conflict with the TNK mechanism)?
- Will Dr. Max provide any PM tool (JIRA or otherwise), or will BigHub need to bring/build one?
- Is Excel the right long-term medium for the roadmap, or should it move to a platform?

## Sentiment & Tone

Warm, informal, high-trust working relationship between Marek and Jindřich — lots of shorthand, banter, and mutual validation ("to je pecka," "to je super myšlenka"). Substantively, the tone is constructive but candid about real operational gaps: no backlog tool, inconsistent specs, unclear project-acceptance boundaries. Jindřich is confident and proactive but stretched thin (limited technical depth so far, chasing vendors for access); Marek is energized and already pattern-matching new opportunities (Microsoft funding) within his first day.

## Routing Log

{Written after PM confirms routing review}

> Migration note: ported from the predecessor repo (`bh-secondBrain`) on 2026-09-02, where this note existed but was never routed to harness artifacts (Routing Log was still an empty placeholder there too). That unrouted state is preserved here — no routing was performed during migration. Header/type field updated to conform to the fixed `internal | client | external | milestone` type enum (original free-form type: "business sync"); reclassified as `internal` since all three attendees are BigHub staff, matching the note's own TL;DR ("Recurring BigHub-internal sync").
