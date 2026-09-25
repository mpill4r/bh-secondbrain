---
last_updated: 2026-09-24
type: external
attendees: [Jindřich Tůma, Marek Pillár, Filip Černý, Jakub Turner, Tereza Foltýnová, Jana Egrmaierová, Petr Sláma]
recording_link:
---

# ViaPharma Reklamace Sync — Knowledge-Base Architecture Standoff & Testing Status

**Date**: 2026-09-24
**Attendees**: Jindřich Tůma, Marek Pillár, Filip Černý (STK-006), Jakub Turner (STK-007) — BigHub; Tereza Foltýnová (STK-013), Jana Egrmaierová (STK-044), Petr Sláma (STK-034) — ViaPharma CZE
**Type**: external
**Recording**: N/A
**Previous session**: [2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo](2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo.md) (closest prior recurring ViaPharma sync)
**Meeting prep**: N/A

## TL;DR

Testing status was quick (a new bug found, mobile-device logistics for shared testing settled, auth re-enable requested), but the meeting was dominated by an extended, sometimes tense disagreement over what "knowledge base" actually means and where it should physically live. Petr Sláma pushed back hard on Reklamace's AI-to-digitization reframe, arguing the original vision required a real branching email workflow — not a one-line Axapta parameter — and cited a written spec comment from 2026-05-20 (the "Zentiva" example) as evidence he'd flagged this months ago. Jindřich and Jakub Turner held the line that the actual logic needed turned out to be simple/deterministic, consistent with the digitization reframe already in motion (see [[ASM-122]]). Nothing was resolved; BigHub will bring a formal recommendation to the upcoming Dudaško/Žůrek decision meeting, which Sláma will now also attend.

## Key Discussion Points

### Scheduling context (opening)

Marek confirmed a Dudaško review happening later the same day, and will follow up informally with Tereza the next day to walk through potential new initiatives. Tereza had already scheduled a more formal session for the following Friday with Petr Spilka (STK-014) included as primary business owner.

### Reklamace testing — status and a new bug

Feedback is tracked on a shared sheet. Jana Egrmaierová was mid-testing the "příjem s výhradou" (receiving-with-reservation) flow and hit an "invalid request" error when submitting with attached photos — not yet reported to Petr Sláma. Filip had checked the sheet the previous morning when everything showed "pass" and hadn't prioritized it since; he'll investigate, suspecting it may relate to ongoing AKS infrastructure changes. Separately, the PUME-integration bug Filip had flagged as his own mistake (involving Jan Kopecký) is confirmed fixed and tested.

### Mobile testing device and auth

Tereza worked out device logistics with Petr Spilka: personal phones won't be allowed onto the warehouse network, so a shared internal phone will be provided for testers to pass around — Sláma is indifferent to which device, as long as something reaches the warehouse floor. Tereza will coordinate handoff (to Jana Egrmaierová, per the call).

Because the device will be shared, Sláma requested per-user login/auth be turned back on for testing (currently disabled to ease testing) so actions are attributable via the API. Filip confirmed login is already implemented but disabled; Jakub Turner clarified the auth work is in draft and not yet merged. Action: finish and enable it for testing.

### Reklamace Excel (supplier data) — mostly done, one known gap

Tereza considers the supplier Excel 100% delivered by Jana. Filip and Jana had already worked through edge cases directly — most cases are covered, but not all. The known gap: shipments physically split across two different addresses, a case the app doesn't currently handle. Since the app only reflects whatever address Axapta sends when generating the "rozvozový list" (dispatch list), this needs no app-side change *if* Axapta can supply the correct address per shipment. Filip noted Honza Sovka was separately exploring whether the underlying process could avoid this case entirely, or whether it should simply be excluded from testing scope for now. Not resolved.

### Knowledge-base architecture — the core disagreement

Sláma opened this by relaying that Dudaško, in a meeting with him earlier this week, confirmed Axapta should **not** hold significant logic for either the reklamace or freight ("doprava") case — that logic belongs in "the AI application," with the correct address sourced from "a knowledge base." His direct question: where does that knowledge base actually live — SharePoint, Confluence, or is "the Excel" itself now meant to be it?

Sláma then pushed back hard on the premise that a "knowledge base" is a one-line Axapta field. His read of the original project vision (an April kickoff document, "business cases for the AI"): a human should never touch the process — a warehouse worker photographs the issue, and **AI dispatches a sequence of emails to different parties depending on their responses** (send here, if they confirm, send there, then to shipping with the confirmed document). He argues that's a genuine branching workflow, not something Axapta can hold beyond a small (~4x5cm) text field — building real workflow support there would mean tens of mandays of custom development he doesn't have room for today.

Jindřich's response, laying out BigHub's read of three separate things that have been getting conflated:
1. **Supplier source-of-truth data** — previously split across Excel/notebooks (120 suppliers), now consolidated; makes sense to hold in Axapta as the single source, since Axapta needs it anyway.
2. **The "knowledge base" / procedure part** — per BigHub's assessment, this is genuinely small (2 lines of procedure per supplier in most cases), so the proposal is a simple added parameter/column in Axapta, not a robust process engine.
3. **Email draft generation** — already handled by the app for the large majority of reklamace types, per the already-approved Phase 1.1 spec.

Jindřich's conclusion: given these three things turned out to be simple and largely deterministic, this became a digitization project rather than something requiring an AI agent — consistent with [[ASM-122]]. Filip agreed, adding that from the start it didn't make business sense to frame deterministic decisions as "AI."

Jakub Turner pushed back at Sláma directly: AI **is** used where it makes sense (recognizing document content per spec, drafting emails) — but it can't invent workflows or procedures that exist nowhere in writing. He pointed to an explicit, already-approved spec line for Phase 1.1: **"vyjednávání s dodavatelem probíhá ručně"** (negotiation with the supplier happens manually).

Sláma disputed the framing that this gap was never raised — he says he flagged it in writing in his own spec comments on **2026-05-20**, using a specific supplier example ("Zentiva"), explicitly stating the process needed to be automatic. He wants this on record so it can't later be claimed BigHub was never told. He also referenced an April kickoff document defining the original business requirement, which he believes conflicts with the "manual for Phase 1.1" framing.

Considerable cross-talk followed about what "knowledge base" even refers to now. Turner's clarification: the knowledge base the app currently consumes is address + email per supplier, delivered via API from Axapta per the already-agreed Swagger contract — that's the whole of what's needed for the current draft-email flow. The broader procedural workflow knowledge (which suppliers need special handling, and what that handling is) was never captured anywhere structured — it lived informally across notebooks and Excel sheets, and remains unbuilt.

Jana Egrmaierová offered a concrete simplification: flag each of the ~280 suppliers in her Excel as either "standard procedure" (AI just uses the main contact, no special handling) or "specific procedure" (with the specific steps noted) — she estimates roughly 75 of 280 have their own transport arrangement and ~35 need some specific handling, though she flags this data isn't yet validated against the suppliers themselves. She thinks even this simple flag could help the AI decide when to follow the generic flow versus flag for manual handling.

Sláma raised a further technical gap: the current API only carries one generic contact per supplier, but in practice different steps of the same case need to email different addresses (e.g. reklamace department vs. transport/shipping) — a single universal contact isn't sufficient for the workflow he has in mind. Turner: that reflects what was actually built per the current spec; a richer per-role contact structure would be a new, separately-scoped change.

On where the knowledge base (both supplier data and procedural know-how) should physically live: Excel was rejected by both sides (uncontrolled edits, no versioning); Axapta was BigHub's proposed simple option but Sláma maintains it has no real room for anything beyond a short text field without a large custom build; Confluence/SharePoint was raised by Sláma (and previously by his manager) as having proper versioning and access control — Turner pushed back that from a data-integrity standpoint it's just as editable as Excel in practice, and reiterated his preference for keeping supplier data in one place users already go for it (i.e., wherever Axapta already holds it). Turner explicitly deferred the final call to Jindřich/Marek/BigHub, offering only a technical read on what AI can or can't work with once a location is chosen.

Sláma closed the thread saying he personally doesn't care which system is chosen — he'll build whatever's decided in Axapta if that's the outcome — but wants the alternatives and BigHub's reasoning on record, since he's under his own pressure (his manager, referenced here as "Tomáš Blažko," pushes him for visible savings — see Open Questions on a possible name overlap with "Kim," mentioned in a past meeting as his manager). He noted the real savings opportunity is in the email-workflow automation, not the reklamace-protocol creation step itself, which he considers the smaller win.

### Closing

Jindřich closed the topic: BigHub will formalize a recommendation, and will follow whatever alternative Dr. Max's side ultimately chooses, but wants BigHub's reasoning documented on the record. He'll bring this to the upcoming Dudaško/Žůrek decision meeting and asked that Petr Sláma be included in that meeting alongside everyone else with a stake in it. The call ran over time and didn't cover its full agenda.

## Decisions Made

- Shared internal testing phone confirmed as the mobile-access solution (not personal devices) — logistics to Tereza/Spilka.
- Per-user login/auth for the reklamace app will be re-enabled for testing (was off to ease earlier testing).
- The two-different-addresses rozvozový-list edge case needs no app change if Axapta supplies the correct address per shipment — otherwise unresolved, tied to Honza Sovka's separate process-level exploration.
- No decision yet on the knowledge base's physical location (Axapta vs. Confluence/SharePoint vs. other) — BigHub will bring a formal recommendation to the Dudaško/Žůrek decision meeting; Petr Sláma will be included in that meeting.

## Action Items

- [ ] **Filip Černý**: Investigate the "invalid request" error Jana hit submitting a photo-attached "příjem s výhradou" request — possibly AKS-related — from 2026-09-24-viapharma-reklamace-knowledge-base-standoff
- [ ] **Tereza Foltýnová**: Coordinate handoff of the shared testing phone to Jana Egrmaierová — from 2026-09-24-viapharma-reklamace-knowledge-base-standoff
- [ ] **Filip Černý / Jakub Turner**: Finish and merge the reklamace app's auth/login work, then enable it for testing — from 2026-09-24-viapharma-reklamace-knowledge-base-standoff
- [ ] **Filip Černý**: Resolve (with Honza Sovka) how the two-different-addresses rozvozový-list case will be handled — app-side, process-side, or excluded from testing scope — from 2026-09-24-viapharma-reklamace-knowledge-base-standoff
- [ ] **Jindřich Tůma / Marek Pillár**: Formalize BigHub's knowledge-base architecture recommendation ahead of the Dudaško/Žůrek decision meeting — from 2026-09-24-viapharma-reklamace-knowledge-base-standoff
- [ ] **Jindřich Tůma / Tereza Foltýnová**: Ensure Petr Sláma is invited to the Dudaško/Žůrek Reklamace decision meeting — from 2026-09-24-viapharma-reklamace-knowledge-base-standoff
- [ ] **Jana Egrmaierová**: Validate the standard/specific-procedure supplier flags against actual suppliers (currently based on her own experience, not confirmed) — from 2026-09-24-viapharma-reklamace-knowledge-base-standoff

## Open Questions

- Where will the knowledge base (supplier data + procedural know-how) physically live — Axapta, Confluence/SharePoint, or something else? Genuinely undecided, with real constraints raised on every option.
- Is "Tomáš Blažko" (Sláma's manager, applying pressure for visible savings, per this call) the same person previously referenced as "Kim" (Sláma's manager in an earlier meeting), or a different person? Not reconciled.
- Does Sláma's 2026-05-20 written spec comment (the "Zentiva" example) actually contradict the Phase 1.1 "manual negotiation" line, or was it addressing a later phase? Not directly resolved in this call — worth checking the actual spec comment thread.
- Whether a richer per-role supplier contact structure (multiple addresses per supplier, not one generic contact) is actually needed, and if so, how it gets scoped as a change.

## Sentiment & Tone

Tenser than the team's typical status calls — Sláma was visibly frustrated, repeating "we've discussed this five times" and pointedly noting he felt he was being told things weren't raised when he believes he raised them in writing months ago. He was careful to frame this as wanting shared understanding and a paper trail, not blame, and explicitly said the final decision is fine either way from his side. Jakub Turner matched some of that frustration ("já moc nerozumím, co tady teď řešíme"), while Jindřich and Filip stayed measured and worked to separate the three conflated issues (supplier data, procedure, email generation) rather than argue the framing further. Jindřich closed constructively, taking the disagreement as something to resolve at the right level (the Dudaško/Žůrek meeting) rather than in this call.

## Routing Log

Routed 2026-09-25 (late; committed 2026-09-24 without routing).
- **project-assumptions**: Added ASM-181 (Sláma's original-vision claim, open), ASM-182 (shared test phone + per-user login), ASM-183 (two-address shipments, open). Update notes on ASM-122, ASM-139, ASM-171.
- **project-knowledge**: Reklamace entry: knowledge-base standoff, Jana's procedure flags.
- **project-stakeholders**: Updated STK-006, STK-007, STK-013, STK-014, STK-034 (sentiment Neutral leaning Champion → Neutral), STK-044.
- **client-overview**: Ways of Working: written client comments treated as the record.
- **project-daily**: 5 action items added. "Formalize BigHub's knowledge-base recommendation" not added: covered by the 2026-09-25 options table (ASM-169).
- **project-lessons**: LL-066.
- **meeting-index**: Entry added.
