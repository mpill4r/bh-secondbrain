---
last_updated: 2026-10-14
type: external
attendees: [Jan Žižka, Petr Sláma, Tereza Foltová, Filip Černý, Marek Pillár]
recording_link:
---

# Fakturace Doprav — Where Document State Lives: Žižka's "Send Everything Immediately" Wins, Latest Document Overwrites

**Date**: 2026-10-14 (Wednesday), 8:30
**Attendees**: Jan Žižka (STK-015, ViaPharma CZE — business owner, Fakturace doprav), Petr Sláma (STK-034, ViaPharma CZE — Axapta), Tereza Foltová (STK-013, ViaPharma CZE), Filip Černý (STK-006, BigHub), Marek Pillár (STK-001, BigHub; in the office with Tereza, sharing one microphone)
**Type**: external
**Recording**: N/A (transcript, ~31 min, Czech/Slovak)
**Previous session**: [2026-10-12 Phase 1 testing wrap-up](2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state.md), where this meeting was set · origin: [2026-09-10 Fakturace doprav demo](2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo.md)
**Meeting prep**: [2026-10-14 prep](../prep/2026-10-14-fakturace-doprav-stav-dokumentov-slama-zizka-meeting-prep.md)

> **Transcript note**: speaker labels are badly scrambled. Marek and Tereza shared one microphone: Czech lines under "Marek EXT Pillár" (e.g. 00:07–03:50, 25:17, 26:28, 28:19, 29:16) are **Tereza Foltová**; Slovak lines under "Filip EXT Černý" (01:43, 02:25, 03:25, 06:26, 26:06, 29:43) are **Marek Pillár**. "ŽIŽKA Jan" at 05:38 is **Petr Sláma**; at 07:12–08:47 and 26:14 it is **Filip Černý**. Žižka joined at 06:16 ("omlouvám se za zpoždění"). "Švédske" = Swagger; "pani Sterka / Fota" = Tereza Foltová; "Honza Sofka" = Jan Sovka; "TFS" (02:05) likely the guest wifi; "ARK" = AR number.

## TL;DR

Jan Žižka confirmed his model: **every scan goes to Axapta immediately**, because logistics invoices ~150 routes a day continuously, checks km on every rozvozový list, and must chase drivers for missing pages before month-end. Petr Sláma accepted it ("I won't dispute it further") once the mechanics were clear: BigHub **merges new pages into the document and resends the full, latest version**; Axapta **replaces the old file**, with a complete / incomplete status per document and **no version history**. Still open is what goes into the billing row when only a non-ZPPV page has been scanned: Žižka wants the row created from the AR number on the first paper, and Sláma wants that written into the spec. **Žižka (with Tereza) writes the business requirements into the spec in user language**; Marek offered a mapping Excel like the Reklamace one; then Filip lightly updates the Swagger. Filip also offered a **standalone scanning demo next week** (not connected to Axapta).

**Continuity with 2026-10-12**: the dispute ([[ASM-053]] vs. [[ASM-269]]) is settled in Žižka's favour, with Sláma's main worry (versioning in Axapta) solved by overwrite. The device question (Zebra vs. phone) moved: Tereza is chasing Dušan for a call today at 11:00.

## Key Discussion Points

### 0. Before Žižka joined: device (Reklamace)

**Tereza**: trying to get Dušan (IT) for a call on the device today at 11:00 (Filip available), otherwise next week. Filip is off Thursday–Monday and back on Tuesday 2026-10-20.
- The **warehouse wants phones**: more available, and staff already have work phones. Downside: Tereza can only get phones onto the guest network.
- Rejecting the **Zebra** is the warehouse's decision for now, not final. Zebras are picking devices; one shared Zebra for claims would end up "lying somewhere" while the person runs to do claims without it. Tereza could probably find a spare Zebra per warehouse. She personally likes the Zebra (reader, everything).
- **Marek**: the people doing claims are different from the Zebra (picking) users.

### 1. The two models

**Filip** framed them:
1. **Stateless platform** (agreed with Žižka at the 2026-09-10 demo, with Jan Sovka present): Axapta is the only source of truth for every document and page; even a single scanned page goes to Axapta immediately ([[ASM-053]]).
2. **Sláma's counter-proposal**: the platform holds incomplete documents and sends them only when complete, or forced at month-end ([[ASM-269]]). This was also the original spec reading.

**Sláma**: he needs to know why Žižka agreed on the first model and what Axapta should do with "one page of 20".

### 2. Žižka's requirement

**Žižka**: doesn't care about Axapta vs. app technicalities. "The moment a driver scans any paper, the row must appear in Axapta, because we do it continuously. We have ~150 routes a day; we can't wait until the 30th to start invoicing." [translated from Czech] Today they scan the rozvozový list barcode themselves and a row appears in the billing table. The row shows that work on the route has started, so they can chase the driver for whatever is missing. Otherwise they'd face thousands of rows at month-end. Each rozvozový list is checked (km comparison controls), so processing must be continuous: "otherwise it makes no sense, and we can throw it away and do it the old way."

### 3. How partial documents behave

**Sláma** pressed on the edge case: one page of a 5-page rozvozový list today, another tomorrow. What does Axapta show? "That will be a mess, mainly for you."

**Žižka**: only the status should change (all documents returned or not); when everything is back, the route closes. Sending documents is a "side product" for record-keeping; he doesn't mind how many pages are stored.

**Filip**: BigHub's design already assumes that day 1 sends the single page, and day 2 sends the **complete merged document** (old + new pages) as one file, so only the newest document is valid.

**Sláma**: fine. He'll attach whatever arrives to the route. "If that's how Honza wants it, I won't dispute it further." [translated from Czech]

**Overwrite vs. history**: Sláma asked Žižka a user-level question: when a newer, more complete file arrives, delete the old attachment or keep history? **Žižka**: "No, I don't need it… keep just the freshest, most complete document." "In the end we should get the same thing we handed the drivers." **Sláma**: so he discards previous files and uploads the newer one.

**Fraud check** (Filip): overwriting could in theory let someone alter km on a ZPPV. **Žižka**: physical documents stay with ViaPharma, are sorted and archived for audits, and km mismatches are flagged by their controls. Filip sees no problem then.

### 4. Billing row and statuses: not in the approved spec

**Sláma**: the approved spec has the billing row filled with km and other data read from the **ZPPV**. If the first scan is, say, a night-delivery confirmation, what goes into the billing row?
- **Žižka**: create the row from the **AR number** on the first scanned paper, then fill the rest when the ZPPV arrives.
- **Sláma**: that isn't in the spec he was given. Without ZPPV data he'd create the row only when the ZPPV is complete. If Žižka wants an empty row after the first page, he must write it in the spec in his own words, plus **status per document** (complete / incomplete) and **status per route** (all documents returned). The current spec assumed documents arrive complete, so document status isn't described.
- **Sláma**: a recurring problem. Requirements get changed in meetings he's not in, and "the devil is in the details". He wants one business description, not fixes later.

### 5. Next steps

- **Tereza** will sit down with Žižka and write it into the spec at user level (what they need to see), not technically.
- **Marek** offered to prepare a mapping Excel like the Reklamace data map, so everything is in one place; Tereza and Sláma liked it.
- **Filip**: once the business description exists, he'll propose a light Swagger update and settle details (file naming etc.) directly with Sláma.
- **Marek**: specs will keep changing as edge cases appear, but having it written down lets everyone move.

### 6. Standalone scanning demo

**Filip** offered a demo not connected to Axapta: upload scans and see how pages merge and sort into routes; nothing is sent or stored. Both sides' infra is ready, so it could start **next week**. **Žižka**: "Gladly." **Tereza**: it fits next week's **Canon** scanner meeting; she'll arrange it for next week and check whether Canon can come on site.

## Decisions Made

1. **Every scan goes to Axapta immediately** (Žižka's model, [[ASM-053]] holds); Sláma's hold-until-complete model ([[ASM-269]]) is dropped.
2. **BigHub merges pages and resends the full latest document; Axapta replaces the old file.** No version history needed (Žižka).
3. **Each document carries a complete / incomplete status**; the route shows whether all documents are back.
4. **The business requirements get written into the spec in user language** by Žižka with Tereza (billing row from the first paper's AR number, document and route status), then Filip updates the Swagger with Sláma.
5. **A standalone scanning demo** (no Axapta) is offered for next week, alongside the Canon meeting.

## Action Items

- [ ] **Tereza Foltová / Jan Žižka**: Write the business requirements into the Fakturace doprav spec in user language (billing row from the first scanned paper's AR number, then completed from the ZPPV; status per document and per route; latest document replaces the old one) — from 2026-10-14-fakturace-doprav-document-state-zizka-slama
- [ ] **Marek Pillár**: Prepare a mapping Excel for Fakturace doprav (like the Reklamace data map) to capture Žižka's requirements in one place — from 2026-10-14-fakturace-doprav-document-state-zizka-slama
- [ ] **Filip Černý**: Once the requirements are written, propose a light Swagger update; agree details (file naming, status fields) directly with Sláma — from 2026-10-14-fakturace-doprav-document-state-zizka-slama
- [ ] **Filip Černý**: Set up the standalone scanning demo (no Axapta) for next week — from 2026-10-14-fakturace-doprav-document-state-zizka-slama
- [ ] **Tereza Foltová**: Arrange the Canon scanner meeting next week (on site if possible), tied to the demo — from 2026-10-14-fakturace-doprav-document-state-zizka-slama
- [ ] **Tereza Foltová**: Get Dušan (IT) for the device call (today 11:00, else next week) — from 2026-10-14-fakturace-doprav-document-state-zizka-slama

## Open Questions

- What goes into the billing row when the first scan isn't the ZPPV? (Žižka: create from AR, fill later. To be specified.)
- How are document and route status shown in Axapta, and who builds that (Sláma's capacity, [[ASM-257]])?
- File naming / identity so Axapta knows which attachment to replace (Filip + Sláma).
- Does the Swagger's version field ([[ASM-132]]) stay, or is it replaced by plain overwrite?

## Sentiment & Tone

**Tense in the middle, constructive by the end.**

- **Petr Sláma**: frustrated that requirements change in meetings he isn't in ("the devil is in the details"); pushed Žižka hard on edge cases and refused to treat them as "technical". He conceded gracefully once the overwrite approach was clear, and keeps insisting on a written business spec.
- **Jan Žižka**: business-focused, impatient with technicalities ("these are technical things"), clear on why continuous processing matters. A little defensive when pressed, but he answered the key user question (overwrite, no history) decisively.
- **Tereza Foltová**: organiser and broker; took ownership of writing it down with Žižka.
- **Filip Černý**: calm technical translator. His merge-and-resend design dissolved most of Sláma's objection.
- **Marek Pillár**: kicked off and offered the mapping-Excel format.

**Watch-out**: Sláma's recurring complaint, that decisions are made without him, should be addressed by putting everything in the written spec he can see.

## Routing Log

Confirmed by PM on 2026-10-14 (confirm all).

- **project-assumptions**: ASM-053 → Decided; ASM-269 → Retired; ASM-132, ASM-265 updated; added ASM-280, ASM-281
- **project-stakeholders**: STK-015, STK-034, STK-013
- **project-knowledge**: Fakturace doprav document flow
- **client-overview**: Ways of Working (decisions made without Sláma)
- **project-daily**: meeting item done; mapping-Excel item added; 3 waiting items for Tereza. Filip's items stay in this note.
- **project-lessons**: LL-92
