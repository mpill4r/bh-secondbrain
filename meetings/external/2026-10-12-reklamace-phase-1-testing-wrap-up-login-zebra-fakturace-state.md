---
last_updated: 2026-10-12
type: external
attendees: [Tereza Foltová, Petr Sláma, Jana Egrmaierová, Filip Černý, Marek Pillár]
recording_link:
---

# Reklamace Phase 1 Testing Wrap-up — UX Feedback, Login, Zebra vs. Phones & the Fakturace Doprav State Question

**Date**: 2026-10-12 (Monday)
**Attendees**: Tereza Foltová (STK-013, ViaPharma CZE), Petr Sláma (STK-034, ViaPharma CZE — Axapta), Jana Egrmaierová (STK-044, ViaPharma CZE — quality / Reklamace tester), Filip Černý (STK-006, BigHub — Reklamace / Fakturace dev), Marek Pillár (STK-001, BigHub — joined ~32 min in, connection problems). Jindřich Tůma (STK-003) did not attend.
**Type**: external
**Recording**: N/A (transcript, ~58 min, Czech/Slovak)
**Previous session**: [2026-10-08 ViaPharma Reklamace sync](2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity.md), which set this wrap-up for Monday · related: [2026-10-12 internal data-map review with Filip](../internal/2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict.md)
**Meeting prep**: N/A

> **Transcript note**: "Speaker 10000" at 00:01 is unattributed. "pan Holek / Hůlek" = a ViaPharma colleague Filip phoned about the Zebra terminals (spelling unconfirmed). "Dušan" = ViaPharma IT contact (surname unknown). "Andrejka" = a ViaPharma colleague who suggested the QR code. "pan Kupčík" = Boomi contact. "Slegr" at 54:20 = Swagger. "20. 6." at 42:25 is almost certainly a transcription error: Tereza said Jana has 14 days, i.e. around 2026-10-26.

## TL;DR

Jana Egrmaierová has finished Phase 1 testing and walked through her feedback: all small UX fixes, which Filip takes on (tiles instead of tabs, clearer error messages, one "done" button, SP number on the scan screen, a scan-success indicator, a trash icon with confirmation for deleting photos, lowercase SP labels accepted). Login goes through Microsoft accounts: everyone on receiving has a Windows login (confirmed live), and the point is the audit trail (who created / photographed what), not security; whether the API carries that identity is to be checked. The device question (Zebra vs. phone) stays open: technically everyone prefers the Zebra (internal network, hardware barcode reader), but the warehouse calls it a no-go, so Tereza sets up a call with IT (Dušan) and Spilka. On Fakturace doprav, Sláma laid out his model: **send only complete documents to Axapta**, immediately, with incomplete ones held by BigHub until forced; it is to be settled with Jan Žižka on **Wednesday 2026-10-14 at 8:30**.

**Continuity with 2026-10-08**: the Phase 1 wrap-up happened as planned (Monday), but was much longer than 15 minutes. The shared mailbox now exists (Tvarůžek finished it on Friday night), so email-agent integration can start. Per-user login ([[ASM-217]]) is still stuck on BigHub's side. Next-phase input from logistics is in progress (Jana, ~14 days).

## Key Discussion Points

### 1. Login to the app

**Jana**: what happened to the login, and how will it work? Like Anywhere, where warehouse staff scan a login card?

**Filip**: still in progress, stuck between BigHub and infrastructure because Vladislav Tvarůžek is on vacation; BigHub wants one login for this app and the main platform ([[ASM-217]]). He had never heard of a card and assumed Microsoft (Entra) login.

**Sláma**: he doubts warehouse staff have Microsoft accounts, but they all have AD accounts (needed for Axapta). For logistics it isn't a security matter: "it matters to us only so we know who did it… that Franta photographed this one." [translated from Czech] Anywhere is plain name + password; same or different doesn't matter, "no need to make it complicated". The users are mainly the **receiving foremen (předáci na příjmu)**, not the quality staff upstairs.

**Tereza** checked live: Lukáš Gebovský confirmed everyone on receiving has a Windows login, so Microsoft login should work.

**Filip**: the app gets explicit log-in / log-out, so on a shared device it's always clear who is logged in and under whom cases are created. Granting access is a small infra request (add users in the Azure portal).

**Who photographed it, in the API**: Sláma expects the creator's identity to come through the API so Axapta can record it. Filip fears it isn't there yet. Both will check; it gets added if missing.

### 2. Jana's UX feedback

| Item | Feedback | Outcome |
|---|---|---|
| Layout on mobile | Tabs are hard to read on a phone; prefers big tiles | Filip: tiles, bigger text, colours. Sláma likes it |
| Error messages | "Produkt nenalezen" shows for everything; the user should learn what's wrong (label doesn't exist, empty, already scanned) | They are BigHub's translations of Axapta API errors. Sláma: maybe Axapta should return sensible messages and the app just shows them. Filip investigates the example and posts the source + a proposal on Teams |
| End screen | "Ukončit" and "Další položka" do the same; one SP label = one item, so "next item" confuses | Simplify to one action; Jana proposes the wording (e.g. "Dokončit" / "Skenovat další štítek") |
| QR code on the rozvozový list | A colleague's idea (seen at other suppliers) | Sláma: not until follow-up processes define what it holds and who reads it ("it would look cool, but nobody would use it"). Filip's idea: an optional template field, printed only if sent. Parked |
| SP scan result screen | Add the SP number just scanned; order: SP label, supplier, item name, batch, expiry, quantity at the bottom | Filip: no problem |
| Camera scanning | Aiming at the SP label is the slowest step; success shows only as a frozen frame | Add a clear success indicator (green frame / tick). A Zebra hardware reader would make this moot |
| Red X on photos | Jana read it as an error and thought it caused a failed submit | It deletes the photo. Marek: don't make a destructive action green. Agreed: trash icon instead of X, plus a "Really delete this photo?" confirmation; red is fine |
| Photo size / count | Same size on every device? Max 10? | Max 10 on any device; photos above a size cap are compressed on BigHub's side |
| Lowercase SP labels | Manual entry with lowercase "sp" is rejected | Axapta isn't case-sensitive (Sláma), so accept lowercase. Filip |

Jana's failed submit today was the app being down: Filip is mid-way through the Boomi authorization change (with pan Kupčík).

### 3. Device: Zebra vs. phones

**Filip** had discussed with a ViaPharma colleague (pan Holek / Hůlek) using the Zebra's hardware barcode reader, which reads faster than the camera, with a physical button and a beep.

**Tereza**: "still very open". She has Jindřich's write-up of Filip's three options and will forward it to IT, calling them first to raise its priority. **The warehouse says the Zebra is a no-go**: it's a picking device and passing it around would be awkward. Personally she likes it, because it's on the internal network. The guest wifi is password-protected but not internal; you need VPN to reach Axapta.

**Filip**: BigHub's app and backend run only inside the internal network, so devices need internal access or another opening. Technically the Zebra is "the clear solution": already configured, managed by ViaPharma IT, with the reader. If the choice is semi-political, he can't see into it. Otherwise: a separate wifi for phones that reaches only the BigHub app, or phones via VPN. He'd like to talk to ViaPharma IT about what they've done before.

**Sláma**: the Zebra "meets everything we want". **Tereza**: "the camera will never be as user-friendly as a physical reader with a button that beeps." [translated from Czech]

**Outcome**: decided separately. Tereza calls Dušan (IT) to set up a call ASAP, with Petr Spilka (who had a problem with the reader). **Jana** asked whether the Zebra talks to Axapta the same way as a PC: yes, network-wise it behaves like a PC on VPN.

### 4. Next steps after testing

**Tereza**: Jana spent more time testing than needed. Next time, prepare better what is ready and what to test; the phone mix-up wasted effort.

**Filip**'s next steps: (1) the UX changes above; (2) the Boomi authorization change behind the scenes; (3) integrating the shared mailbox, now created ("Tvarůžek finished it heroically on Friday night"), so email drafts can start; (4) the Axapta → BigHub data, being settled with Sláma via the data map.

**Marek**: unblock the data-map Excel with Sláma (BigHub's comments coming), complete it, and in parallel work through Phases 3–5 with Tereza, so development flows on once the feedback and the Axapta / knowledge-base questions are resolved.

**Tereza**: the next-phase write-up is with Jana now, as a priority, ~14 days.

**Test emails** (Jana): will drafts land in kvalitasklad@ and scare colleagues not testing? **Filip**: no, it runs in a separate test environment.

### 5. Fakturace doprav: where open-case state lives

**Tereza** wanted Jan Žižka (STK-015) at Thursday's status (he isn't normally invited). **Sláma** doesn't understand how logistics would work with incomplete documents or versions in Axapta and needs Žižka to explain.

**Sláma**'s account: BigHub met Žižka without him and agreed "Axapta holds all states"; the draft based on that was then rejected by Tomáš Hraško as too much Axapta development. His model:
- BigHub sends a **document** to Axapta as soon as it is **complete** (all pages scanned), even if the route isn't complete.
- **Incomplete documents stay with BigHub** until forced: e.g. a month-end "send me all incomplete ones for October", or selectively per document.
- Axapta keeps a per-route list of expected documents and shows status per route (all / none / half) and per document, with a link to view it.
- He wants **no document versioning in Axapta**. If Žižka insists on continuous sending, Axapta would simply overwrite the document each time.

**Filip**: he first understood it Sláma's way; BigHub moved after Žižka said even a single scanned page must reach Axapta ([[ASM-053]]). He had read "complete" at **route** level, not document level, so Sláma's model is new to him. Technically fine. Today's Swagger sends the latest version authoritatively, with no comparison needed in Axapta. Holding incomplete documents means BigHub needs its own database ("a light extension, nothing unmanageable"). His remaining concern: BigHub would hold information Axapta doesn't have during the month.

**Scheduling**: Filip is on vacation Thursday–Friday (10-15–16); Sláma is in Ostrava with trainings. Agreed: **Wednesday 2026-10-14, 8:30** with Žižka; Tereza invites him (not yet confirmed). Filip: the decision is really Sláma's and Žižka's; BigHub adapts.

### 6. Data map, spec and recap emails

**Marek**: BigHub's comments on the data-map Excel come shortly ("we agree with ~95%"); then the spec version for the first phases, updated with the Excel, goes out **during tomorrow (2026-10-13)**.

**Marek** asked whether recap emails like last Thursday's are welcome or feel "authoritative". **Tereza**: "super", not an unpleasant to-do list; others agreed. Marek: if nobody objects to the features listed, no need to reply.

## Decisions Made

1. **Login via Microsoft accounts** (everyone on receiving has a Windows login), with explicit log-in / log-out for shared devices. Purpose is the audit trail in Axapta, not security.
2. **Creator identity goes to Axapta via the API**; added if missing.
3. **UX changes accepted** (Filip): tiles, clearer error messages, one end action, SP number + new field order on the scan screen, scan-success indicator, trash icon + delete confirmation (red is fine), lowercase SP labels accepted.
4. **No QR code on the rozvozový list for now**: only once a follow-up process defines its content and use.
5. **Photos**: max 10 per claim on any device; oversized photos compressed by BigHub.
6. **Device choice (Zebra vs. phone) decided separately** with ViaPharma IT and Spilka. Zebra is technically preferred by BigHub, Sláma and Tereza; the warehouse objects.
7. **Fakturace doprav state** settled with Žižka on **Wednesday 2026-10-14, 8:30**.
8. **Recap emails stay**: no reply needed unless someone objects.

## Action Items

- [ ] **Filip Černý**: Implement Jana's UX changes (tiles, end-screen action, SP number + field order, scan-success indicator, trash icon + delete confirmation, lowercase SP labels) — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Filip Černý**: Investigate the error messages ("Produkt nenalezen"); post their source and a proposal on Teams (incl. Axapta returning readable messages) — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Filip Černý / Petr Sláma**: Check whether the API carries the creator's identity; add it if missing — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Filip Černý**: Finish the per-user Microsoft login (after Tvarůžek's return) and the Boomi authorization change; start the shared-mailbox integration — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Jana Egrmaierová**: Propose the wording for the end-screen action — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Tereza Foltová**: Forward the device-options write-up to IT and set up a call with Dušan (IT), Petr Spilka and BigHub on Zebra vs. phones — ASAP — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Tereza Foltová**: Invite Jan Žižka to the Fakturace doprav state meeting — 2026-10-14 8:30 — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Jana Egrmaierová**: Write up Reklamace Phases 3–5 — due ~2026-10-26 — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Marek Pillár**: Send the data-map column K comments to Sláma — due 2026-10-12 — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Marek Pillár**: Send the updated first-phases spec (with the data-map outcomes) — due 2026-10-13 — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state
- [ ] **Marek Pillár**: Send the recap email of this meeting — due 2026-10-12 — from 2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state

## Open Questions

- **Device**: Zebra (technically preferred, warehouse objects) or phones (new restricted wifi or VPN)? Depends on ViaPharma IT.
- Does the current API carry the creator's identity?
- Should Axapta return readable error messages instead of BigHub translating codes?
- **Fakturace doprav**: complete-document sending with forced release (Sláma) vs. every scan immediately (Žižka, [[ASM-053]])? If Sláma's model wins, BigHub needs its own document store.
- Who is Tomáš Hraško, and was his rejection of the Axapta-heavy draft ever communicated to BigHub?
- Does the Reklamace full UAT timing change given the open device and login questions?

## Sentiment & Tone

**Constructive and warm, with good working chemistry; minor friction on preparation.**

- **Jana Egrmaierová**: engaged and thorough, a bit apologetic ("I'm just asking"). Briefly defensive when Marek pushed back on green for the delete button, then relaxed once it was clear the X deletes the photo. Her detailed testing is a big asset; Tereza's note that she over-invested is a signal to scope tests better.
- **Petr Sláma**: pragmatic and engaged, focused on what Axapta needs (audit trail, no versioning). Frank about not being at the Žižka meeting; his Fakturace model is clear and well reasoned. He positions BigHub and himself as fellow "implementers" against an Axapta-heavy design, which Filip politely declined to take sides on.
- **Tereza Foltová**: supportive and action-oriented (checked logins live, chased Žižka during the call). Mild frustration that testing preparation was muddled ("the phone confusion"). She openly favours the Zebra but faces warehouse resistance.
- **Filip Černý**: open and receptive, quick to own fixes ("this is a 3-minute change"). Careful not to take sides between Sláma and Žižka.
- **Marek Pillár**: joined late; framed next steps and checked the recap-email format, which landed well.

**Watch-outs**:
- The device decision blocks real-world rollout; warehouse resistance to the Zebra is operational, not technical, so it needs Spilka.
- Test-preparation communication: next test wave needs a clear "what's ready, what to test" brief.
- Fakturace doprav: Wednesday's meeting must end with one model agreed by both Sláma and Žižka, or the Swagger churns again.

## Routing Log

Confirmed by PM on 2026-10-12 (confirm all). Also covers Jindřich Tůma's e-mail to Tereza with Filip's three device options (folded into ASM-265).

- **project-assumptions**: added ASM-265 to ASM-270; updates on ASM-053 (meeting moved to Wed 10-14 8:30), ASM-217, ASM-182, ASM-227, ASM-258
- **project-stakeholders**: STK-044, STK-034, STK-013; new STK-064 Tomáš Hraško, STK-065 Lukáš Gebovský, STK-066 Dušan (IT), STK-067 pan Holek / Hůlek
- **project-knowledge**: Zebra terminals, Anywhere, ViaPharma networks, Předáci na příjmu
- **client-overview**: Ways of Working (recap e-mails welcomed)
- **project-daily**: 3 items added (recap e-mail, Fakturace 10-14 meeting, Tereza's device call); column K, Fakturace reply, spec-send and Phases 2–5 items annotated. Other people's items stay in this note.
- **project-lessons**: LL-90
