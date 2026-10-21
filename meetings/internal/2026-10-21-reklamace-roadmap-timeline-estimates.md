---
last_updated: 2026-10-21
type: internal
attendees: [Jindřich Tůma, Filip Černý, Marek Pillár]
recording_link:
---

# Reklamace Roadmap & Timeline — Per-Phase Estimates, UAT Windows, 4 November Delivery Target

**Date**: 2026-10-21 (afternoon, after the weekly sync)
**Attendees**: Jindřich Tůma (BigHub, account lead; left at ~37:00), Filip Černý (BigHub developer), Marek Pillár (BigHub, PM)
**Type**: internal
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: [2026-10-21 BigHub weekly sync](2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout.md) (same day; this was the "roadmap/timeline" meeting announced there)
**Meeting prep**: N/A

> **Attribution note**: speaker labels are shuffled. Statements are attributed by content: Slovak lines → **Marek Pillár**; Czech lines about the code, branches, login and estimates → **Filip Černý**; Czech lines about the client, UAT defaults, steerco and dates → **Jindřich Tůma**. The line labelled "Marek Pillár" at 37:17 ("I have to run to another slot") is Jindřich leaving. "Exakta / Akzapta / Excelta" = Axapta; "Jägermajerová / Egromajerová" = Jana Egrmaierová; "Slama" = Petr Sláma.

## TL;DR

The team walked Marek's roadmap diagram phase by phase and agreed the client format: **per phase, BigHub development + client (Axapta/Sláma) development + UAT**, with every blocker tagged with its owner so Sláma gets a to-do list to estimate. It goes to the client as an **Excel** (they're used to it), not the diagram. First estimates: **Phase 1 ~6 MD (pessimistic 8)**, **1.1a 1–3 MD**, **Phase 2 3–4 MD**, **Avízo 1–2 MD**; **1.1b, 3, 4, 5 and 3.1 can't be estimated** before discovery. Delivery target for the next batch moves from "end of October" to **4 November** (Filip's leave next Thu/Fri), dependent on client inputs; the client is asked to reserve **4–6 November** for testing.

## Key Discussion Points

### 1. Format for the client

- **Jindřich**: BigHub can't promise much while things are still being specified. The roadmap should show two things: what's needed from the client, and **per phase: BigHub development, client development (question mark, for them to fill in) and UAT**. UAT gets a standard **2 weeks by default**; if it takes 3–4, that's on them and visible.
- One **UAT at the end of each phase** (Filip: the Axapta integrations are the riskiest part to test). Filip would prefer shorter, more frequent testing, but logistics always asks for 2 weeks and last time tested for almost a month.
- **Marek** floated continuous testing (estimate × 1.2, "half an hour a week" instead of a 3-day block); not taken up — Jindřich prefers static, time-boxed UAT per phase, responsibility left with the client, and slightly pessimistic estimates to protect BigHub. Phase 2 gets refined after Phase 1/1.1.
- **Blockers with an owner tag** ("Sláma", "Egrmaierová"…), so Sláma sees exactly which items he must estimate and the timeline becomes dynamic (BigHub weeks + client weeks + testing weeks).
- **Excel, not the diagram**: Marek converts it, since logistics would be confused by the diagram. Marek also sees it replacing the 20-page spec for steering purposes (Jindřich agrees: the "what's needed to continue" part is what matters).

### 2. Phase 1 (kap. 1.2–1.5) — next batch

- **Swagger changes**: the approval item is first on **Filip** — he promised one file with all changes written in, some already agreed orally (easy, quick yes expected), plus the open points (warehouse address, error messages). He'll do it this afternoon / tomorrow.
- **Warehouse address**: Marek recalls Sláma closed it at the 10-15 sync (users log in under their accounts → warehouse per user); Marek will find it in the transcript. (Harness: [[ASM-263]] Decided.)
- **Error messages**: BigHub handles every case in Honza's original spec and the approved contract, but none of the 3–4 cases Egrmaierová sent were defined before. **Filip** will propose to Sláma (who suggested it himself) that **Axapta owns the messages**: on failure Axapta returns an error code **plus the exact user-facing text**, and BigHub just displays it.
- **Estimate**: BigHub dev **~6 MD** (Friday + next week); Marek noted **8 MD pessimistic**. Filip may take **next Thu–Fri off** (maybe only Fri). Filip, privately: Mon–Tue next week is possible but very optimistic — don't promise.
- **Target**: **Jindřich**: tell the client BigHub aims to deliver by **4 November** (3 Nov mentioned first), dependent on their inputs, then hand over for final testing.
- **UAT**: **1 week** (realistically ~2 hours: new UI they've seen, login for 2 users, X-Manager-based drafts). Ask them to **reserve 4–6 November**; if they want a full end-to-end retest or 3–4 weeks, that's their choice — BigHub moves on to other work.
- Still open: **how they test the e-mail agent** (Thursday), and **Zebra** confirmation.

### 3. Phase 1.1a — audit trail + reply sorting

- **Filip**: unblocked except the testing decision and more e-mail threads. Both features (communication record, sorting) are **done on branches**; what's left is integration: **1–3 MD** (optimistic 1).
- He'd like ~**30 real threads** to test before handover, so he can hand it over confidently. Marek adds a to-do for Egrmaierová (visible to Žůrek too).
- **UAT**: **2 weeks** as a time range (1 person ~30–60 min a day); higher chance of finding issues than in Phase 1 (subjective judgement of sorting, audit-trail exports).

### 4. Phase 1.1b — follow-up e-mail sequence

- Not BigHub's PoC (that was sorting). **Unspecified**: of the 7 threads received, 5 were plain question–answer with no follow-up. Example of the hard cases: the supplier offers a different batch for expired goods — the worker decides from knowledge nobody has written down.
- **No estimate**: "could be 2 days if one pattern covers half the e-mails, or very hard if every case is like that". Marked **"based on discovery / further analysis"**; testing likewise.
- Needs real threads incl. unusual cases; Filip and Marek will draw a decision diagram together once examples exist.
- It runs **in parallel with Phase 2**, not before it; Marek keeps it in place in the doc (already flagged "not discovered").

### 5. Phase 2 — warehouse claims

- **Filip**: classic software work; the shared part with receiving claims was built reusable and is partly done; the UI is almost identical. **2 days** after inputs → entered as **3–4 MD**.
- Unknowns: **Axapta capacity/readiness** (product lookup by label data) and **no samples** — label photos and what Axapta wants in the package (examples are enough, no JSON needed).
- **UAT**: 2 weeks (different back-office process, new users).

### 6. Okamžité avízo (optional)

- Spec is framework-level only; open: **which suppliers, at what time (e.g. 23:00), which exact case, text template**. Today workers do it from memory.
- **Filip**: the spec places it under receiving claims, but it most likely belongs to **příjem s výhradou** (notify the supplier that goods were received with reservation and a claim may follow). He'd need a **~4-hour session** with whoever designed it with Honza — the owner on the client side is unknown.
- **Estimate**: **1–2 MD** if specified (1 MD with an exact A4 spec); treat cautiously like Phase 2.

### 7. Phases 3, 4, 5 and 3.1

- Nothing in the spec beyond a few paragraphs → **discovery, no estimate**.
- Ideas (Filip): an Outlook add-in or simple frontend showing supplier info / a summary of the e-mail thread; **Axapta infolog** via API (Axapta displays formatted info to the user — simple for BigHub).

### 8. Other

- **Fakturace mapping Excel**: Filip hasn't reviewed it; it's lower priority than this. He finishes **login** first, then the Excel.
- Jindřich: the roadmap doesn't have to be shown at Thursday's meeting — by the end of the week is fine.

## Decisions Made

- **Roadmap format**: per phase BigHub dev + client dev (blank for Sláma) + UAT; blockers tagged with owner; delivered to the client as **Excel**.
- **UAT**: one per phase, at the end; default time box (Phase 1: 1 week; 1.1a, 2: 2 weeks); duration is the client's responsibility.
- **Next-batch delivery target: 4 November 2026**, dependent on client inputs; ask the client to reserve **4–6 November** for testing. Supersedes the "end of October" internal target ([[ASM-317]]).
- **Estimates recorded** (BigHub dev): Phase 1 ~6 MD (pess. 8), 1.1a 1–3 MD, Phase 2 3–4 MD, Avízo 1–2 MD; 1.1b, 3, 4, 5, 3.1 after discovery.

## Action Items

- [ ] **Marek Pillár**: Convert the Reklamace roadmap to Excel (per phase: BigHub dev / client dev blank for Sláma / UAT; blockers tagged with owner; estimates above) and send it to Jindřich and Filip — due 2026-10-23 — from 2026-10-21-reklamace-roadmap-timeline-estimates
- [ ] **Filip Černý**: Send logistics one file with all Swagger changes (agreed ones + open points) for approval — due 2026-10-22 — from 2026-10-21-reklamace-roadmap-timeline-estimates
- [ ] **Marek Pillár**: Find Sláma's statements on the warehouse address and error messages in the 10-15 transcript and send them to Filip — due 2026-10-22 — from 2026-10-21-reklamace-roadmap-timeline-estimates
- [ ] **Filip Černý**: Propose to Sláma that Axapta owns error messages (error code + exact user-facing text) — from 2026-10-21-reklamace-roadmap-timeline-estimates
- [ ] **Jindřich Tůma / Filip Černý**: Thursday ViaPharma sync — 4 November target, testing window 4–6 November, e-mail-agent testing approach — due 2026-10-22 — from 2026-10-21-reklamace-roadmap-timeline-estimates
- [ ] **Marek Pillár**: To-do list for Jana Egrmaierová (more real e-mail threads, ~30, incl. unusual cases; error-message cases), visible to Žůrek — from 2026-10-21-reklamace-roadmap-timeline-estimates
- [ ] **Marek Pillár**: Find out who on the client side owns the Avízo feature; set up a ~4 h session with Filip — from 2026-10-21-reklamace-roadmap-timeline-estimates
- [ ] **Filip Černý**: Finish Reklamace login, then review the Fakturace mapping Excel — from 2026-10-21-reklamace-roadmap-timeline-estimates

## Open Questions

- Will logistics accept 1 week of UAT for the next batch and reserve 4–6 November?
- Did Sláma already map the error messages (Filip's recollection)?
- Who owns Avízo on the client side, and is it about příjem s výhradou?
- Phase 1.1b: which follow-up cases are frequent enough to automate?

## Sentiment & Tone

Constructive and pragmatic. Jindřich set a protective line (time-boxed UAT, pessimistic estimates, "we can't fight them on testing"); Filip was confident about everything specified (1.1a, Phase 2, Avízo) and firm about not estimating the unspecified e-mail sequence. Shared mild frustration with the client's slow feedback and long testing.

## Routing Log

Confirmed by PM 2026-10-21 ("confirm all"):
- **project-assumptions**: ASM-317 superseded; added ASM-323 (Decided: 4 Nov target, 4–6 Nov testing), ASM-324 (Decided: Excel roadmap format), ASM-325 (Axapta owns error messages), ASM-326 (1.1b after discovery).
- **project-knowledge**: Reklamace estimates, Avízo, later-phase ideas.
- **project-daily** (2026-10-21): 5 items added; Swagger, Thursday and Fakturace-review items updated.
- **Roadmap HTML** (`1. Feature Specs/3. Reklamace/Final/reklamace-roadmap-diagram.html`): MD row filled, target pills set to 4. 11. 2026.
