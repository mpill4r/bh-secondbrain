---
last_updated: 2026-10-22
type: external
attendees: [Tereza Foltová, Jan Žižka, Jindřich Tůma, Filip Černý, Marek Pillár]
recording_link:
---

# ViaPharma Reklamace Sync — Sláma Out Next Week, 4 November at Risk, E-mail-Agent Test Setup & Fakturace Mapping Excel

**Date**: 2026-10-22
**Attendees**:
- BigHub: Jindřich Tůma, Filip Černý, Marek Pillár (PM)
- ViaPharma: Tereza Foltová (project lead, logistics), Jan Žižka (transport; left after the Doprava part, ~10:40)
- Absent: Petr Sláma (excused, in "total press"), Petr Spilka (no notice)

**Type**: external
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: [2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity](2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity.md)
**Meeting prep**: N/A

> **Transcript note**: "Fílo" / "Máro" = Filip Černý / Marek Pillár; "Egermajerová" = Jana Egrmaierová; "pan Sám / Slám" = Petr Sláma; "Petr z Pilka" = Petr Spilka; "Marouška" = Jan Maroušek; "pan Žurek … Ruda" = Rudolf Žůrek (read as one person); "WMSA mezinárodní" = international WMS meetings; "kvalitasklad@vafarma.cz" read as the shared claims mailbox kvalitasklad@viafarma.cz.

## TL;DR

Sláma is out of reach next week (international WMS meetings on top of BrightPick), so ViaPharma's Reklamace inputs won't come next week and the **4 November target ([[ASM-323]]) is effectively off**. BigHub needs 5–7 working days once inputs arrive. Jindřich asked Foltová to agree a realistic delivery date with Sláma, from which BigHub re-plans development and the testing window. The **e-mail-agent test setup** is agreed: no new mailbox; the e-mails of ~3 known suppliers in the knowledge base are temporarily switched to ViaPharma staff addresses, who reply to simulate the supplier. On Fakturace, Filip deploys the **mock without Axapta next week**; Marek showed the **Fakturace mapping Excel** and sends it today; ViaPharma's user description is held until Sláma reviews it, so Fakturace inputs also slip past next week. Logistics' **2027 initiatives** are stuck (Maroušek and Spilka unreachable); Foltová keeps them and asked Jindřich not to raise it with Žůrek yet.

## Continuity (vs. 2026-10-15)

- **Resolved**: warehouse address. Filip had flagged it as open yesterday, but Sláma and Egrmaierová settled it at the 10-15 sync, with minimal changes on both sides ([[ASM-263]]).
- **Resolved**: e-mail testing approach (open since 10-15 and on yesterday's list for today, [[ASM-321]] context).
- **Progressing**: login. Filip expects logins working today or tomorrow; user management is shared with the whole AI platform.
- **Progressing**: Canon scanner test ([[ASM-316]]). Foltová drives it with Hnilička, aiming for next week.
- **Slipping**: Sláma's capacity. 10-15 named BrightPick from 16. 11.; now the week of 26. 10. is also lost to international WMS meetings. The roadmap's AX deadline of 30. 10. is no longer realistic.
- **Still open**: Zebra for Filip, the Fakturace user description (promised for 10-16), logistics' 2027 list, X-Manager data source (Machata back 26. 10.).
- **Not covered today**: Swagger approval, error-message texts (on ViaPharma), testing window 4–6 November.

## Key Discussion Points

### 1. Doprava / Fakturace doprav

- **Mock deployment (Filip)**: a deployment without Axapta, so logistics can click through the app and judge document recognition and route matching. Everything on the Dr. Max / ViaPharma infra side is ready; the delay is only Filip's time, since Reklamace kept taking priority. Target: next week ([[ASM-318]]).
- **Mapping Excel (Marek)**: same form as the Reklamace data map. The left column holds the original data source, then what it should do, categories and the individual Swagger items / data sets. Columns F–I record where the data lives: paper document (F), Axapta (G), BigHub app (H), shared storage (I). It follows Žižka's solution from the 10-14 discussion with Sláma ([[ASM-280]]). Marek tidies it to the latest version, adds column J "komentáře logistiky" for comments and approvals, with decisions and open questions below (e.g. who approves, whether a row can be added before the app ships). He sends it after the meeting for review.
- **User description (Foltová)**: Žižka has written the user view of Fakturace, as was done for Reklamace, to merge with the reworked spec. Foltová holds it until **Sláma reviews it**, so BigHub doesn't receive a version Sláma later disputes on Axapta grounds. Sláma is in "total press" and next week has international WMS meetings, so **neither the Excel review nor the user description will come next week**. Foltová called it a blocker on their side.
- Marek offered help as an independent consultant (mapping, product questions). Foltová: it's on their side for now; BigHub merges it into the spec afterwards.

### 2. Scanner test (Canon)

- Three tasks came out of the scanner meeting ([[ASM-316]]). Foltová arranges the test with Hnilička (Canon) and calls him herself.
- **Žižka**: the priority is the **mechanical durability** with drivers' handling, before checking what it reads. The machine may be rejected on durability alone. As soon as possible.
- **Filip** agrees: reading quality and connectivity aren't a worry for business-grade scanners. He looked at the Canon software Hnilička mentioned and finds it very promising.
- Foltová: arranging it for next week would be a success.

### 3. Reklamace — delivery timing

- **Jindřich**: if Sláma delivered next week, BigHub could be done by **Tuesday 3 November**, then a short, simple test on ViaPharma's side.
- **Foltová**: for Sláma, next week is "pase". Spilka is also missing; she needs him for Marek's Excel and the business decisions to write into the spec. She doesn't think that part blocks BigHub.
- **Jindřich**: it is a blocker. BigHub is **5–7 working days** from finishing and needs ViaPharma's inputs plus an agreed e-mail testing setup. Ideally within 7 days, but at least an agreed date.
- **Foltová**: "we're in trouble, honestly" `[translated from Czech]`, no people. Egrmaierová has finished the **user-view description of Reklamace** (final, read by a second person). There's a meeting on it Monday (26. 10.), but neither Petr is available.
- **Agreed way forward**: Foltová sits down with Sláma and commits to a date (e.g. "in two or three weeks"). BigHub then plans its remaining development (~5 days) and proposes when ViaPharma should block the testing in calendars.
- **Foltová asked for a short list of "hot" blockers** instead of the full spec, so she can push people. Marek has it, will check with Filip what's already resolved, and sends it in a presentable form together with the Excel.

### 4. X-Manager data source

- Machata is on holiday all week. The tables still got in via Customer Care, but BigHub needs access to the data source. **Jindřich talks to Machata on Monday (26. 10.)**; speed depends on his priorities after the holiday ([[ASM-297]]).
- Remaining on ViaPharma: the **error messages** ([[ASM-325]]).

### 5. E-mail-agent testing (Filip)

- The next phase includes: when a case closes in Axapta, BigHub generates the **rozvozový list**, attaches it to an e-mail and saves it as a **draft in the shared mailbox kvalitasklad@viafarma.cz**. A worker approves and sends it. The supplier's reply is then linked and the agent's decision (sorting) shown, as in the demo three to four weeks ago.
- Problem: test drafts must not go to real suppliers, and a supplier reply must be simulated.
- **Agreed setup**: pick ~3 known suppliers (e.g. Zentiva) and temporarily change their e-mail in the knowledge base to a ViaPharma person (Foltová, Egrmaierová or similar), keeping all other supplier data. That person replies from their mailbox; BigHub links the e-mails and the agent's evaluation shows in the shared mailbox.
- Jindřich first suggested a new mailbox (e.g. testreklamace@…); **Foltová prefers their own existing e-mails**, even private ones, because creating a mailbox costs time. That's also how she tests today.

### 6. Login (Filip)

- Logins should work today or tomorrow. User management is **shared with the whole AI platform**, which simplifies the later handover ([[ASM-290]]).

### 7. 2027 initiatives — logistics

- **Foltová**: she can't get Maroušek or Spilka; they have ~3 repeated e-mails about sitting down on it and probably haven't looked. She'll try once more to book a hard slot: "if they don't write anything, they won't have anything" `[translated from Czech]`. She may ask BigHub to write to them so it comes from someone else.
- **Marek**: tell them BigHub needs realistically **2–3 hours of their time by year-end**, and nothing will be built before next year; it's only mapping. Let him know whether she books it or he should write.
- **Jindřich** sees Žůrek before the end of the week on another topic, and this will come up. **Foltová asked not to raise it with Žůrek yet**, fearing it lands as an escalation. Agreed: Jindřich tells Žůrek that **Foltová is handling it**. She has her regular Monday meeting with Žůrek and will try to get Maroušek and Spilka before then.

### 8. Next Thursday (29. 10.)

- Foltová fears many people will be away next Thursday and asked to consider the meeting. Not decided in the call.

## Decisions Made

- **E-mail-agent test setup**: no new mailbox. ~3 known suppliers get a ViaPharma person's e-mail in the knowledge base temporarily; that person replies to simulate the supplier.
- **Reklamace delivery date**: ViaPharma commits to a date for its inputs (Foltová + Sláma). BigHub re-plans development (~5–7 working days) and the testing window from that date. The 4 November target no longer holds as stated.
- **Fakturace user description** is held until Sláma reviews it; not expected next week.
- **Fakturace mock** (no Axapta) goes live next week (Filip).
- **Scanner test** checks mechanical durability with drivers first, reading quality second.
- **Logistics 2027 initiatives** stay with Foltová; Jindřich tells Žůrek she's handling it, no escalation.

## Action Items

- [ ] **Marek Pillár**: Send the Fakturace doprav mapping Excel (latest version, column J "komentáře logistiky", decisions + open questions) to Foltová / Žižka / Sláma — due 2026-10-22 — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Marek Pillár**: Send Foltová a short list of the hottest Reklamace blockers on ViaPharma's side (checked with Filip for what's already resolved), together with the Excel — due 2026-10-22 — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Tereza Foltová / Petr Sláma**: Agree a date by which ViaPharma delivers its Reklamace inputs, so BigHub can re-plan development and the testing window — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Tereza Foltová / Jana Egrmaierová**: Name ~3 test suppliers and the ViaPharma e-mail addresses that replace theirs in the knowledge base for e-mail-agent testing — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Tereza Foltová**: Arrange the Canon scanner test with Hnilička (mechanical durability with drivers first), ideally next week — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Tereza Foltová**: Send the Fakturace user description (Žižka) after Sláma's review — not before the week of 2026-11-02 — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Tereza Foltová**: Send the final Reklamace user-view description (Egrmaierová) after Monday's (2026-10-26) meeting — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Tereza Foltová**: Book a hard slot with Maroušek and Spilka for the logistics 2027 initiatives (2–3 h by year-end), or tell Marek to write to them — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Filip Černý**: Deploy the Fakturace mock (no Axapta) for logistics — due week of 2026-10-26 — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Filip Černý**: Make Reklamace logins work (user management shared with the platform) — due 2026-10-23 — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Jindřich Tůma**: Talk to Machata on Monday about access to the X-Manager data source — due 2026-10-26 — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Jindřich Tůma**: Tell Žůrek that Foltová is handling the logistics 2027 initiatives (no escalation) — due 2026-10-23 — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel
- [ ] **Jindřich Tůma / Tereza Foltová**: Decide whether next Thursday's sync (2026-10-29) takes place — due 2026-10-28 — from 2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel

## Open Questions

- When can ViaPharma realistically deliver the Reklamace inputs (Swagger approval, error-message texts, AX changes, test e-mails) given Sláma's WMS week and BrightPick from 16. 11.?
- Does Sláma's AX work for Phase 1 + 1.1a still fit before BrightPick (16. 11.)? If not, what happens to Phase 2 and later?
- Is the 4–6 November testing window still worth holding, or should it move with the new date?
- Will the 29. 10. sync happen?
- Which ~3 suppliers and whose e-mails for the test?

## Sentiment & Tone

Cooperative but strained. Foltová was candid and apologetic ("we're in trouble") about ViaPharma's capacity: both Petrs unavailable, Sláma squeezed by WMS and BrightPick, Maroušek and Spilka ignoring the initiatives. Jindřich pushed firmly but politely that the client's inputs are now the blocker and asked for a committed date rather than a promise. Foltová is protective of her people and of her relationship with Žůrek: she explicitly asked BigHub not to escalate the initiatives, and BigHub agreed to cover for her. Žižka was pragmatic and focused on scanner durability. Filip was upbeat (login closing, Fakturace mock ready on infra, warehouse address settled).

**Signals**
- Foltová wants short, actionable asks (a "hot blockers" list) over long specs.
- Delivery risk has moved fully to ViaPharma's side; BigHub's timeline now depends on one person (Sláma).
- The initiatives topic is sensitive inside ViaPharma; handle via Foltová.

## Routing Log

Confirmed by PM 2026-10-22 ("confirm all"):
- **project-assumptions**: ASM-323 → At risk; added ASM-330 (date reset: ViaPharma commits a date for inputs), ASM-331 (Decided: e-mail-agent test setup); updated ASM-316, ASM-318, ASM-280, ASM-263, ASM-290.
- **project-stakeholders**: STK-013 Foltová, STK-034 Sláma, STK-014 Spilka, STK-021 Maroušek, STK-015 Žižka, STK-024 Žůrek.
- **project-knowledge**: Reklamace next-phase e-mail flow + test setup.
- **project-daily** (2026-10-22): 10 items added (incl. revise the roadmap Excel), 2 closed (X-Manager table request, Thursday sync), 6 annotated.
