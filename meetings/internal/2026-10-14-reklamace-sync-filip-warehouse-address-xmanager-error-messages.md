---
last_updated: 2026-10-15
type: internal
attendees: [Marek Pillár, Filip Černý]
recording_link:
---

# Reklamace Sync with Filip: Warehouse Address Options, X-Manager KB Table, Error Messages & Test Mailbox

**Date**: 2026-10-14 (inferred; uploaded 2026-10-15)
**Attendees**: Marek Pillár (PM, BigHub), Filip Černý (developer, BigHub)
**Type**: internal
**Recording**: N/A
**Previous session**: [2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict](2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict.md)
**Meeting prep**: N/A

> Transcript note: the export attributes almost every line to "Marek Pillár". Slovak lines are attributed to Marek and Czech lines to Filip; attribution is best-effort. In this transcript "Excel / Excelka / Excelta" is a mis-transcription of **Axapta** wherever it refers to the system (e.g. "send to Excelka who made the change"). "Pan Slaváč" is read as Petr Sláma.

## TL;DR

Since the 10-12 sync the data map closed and Marek routed it into the spec. Filip disagrees that the warehouse address is solved: storing it in the KB doesn't say where the value comes from. Several sourcing options came up; none blocks anything before production. To unblock the knowledge base, Filip wants the supplier table imported into X-Manager now, almost 1:1 from Jana Egrmaierová's Excel, with basic validation. Remaining Reklamace loose ends: error messages (session with Jana, then Sláma), a who-changed-what audit trail after login, the communication PDF mechanism, and how users test against the test mailbox. Tuning of the email-agent sorting goes into per-phase UAT, with ~4 days per phase for feedback.

## Key Discussion Points

### Device: Zebra looks likely

- In the morning Tereza Foltová said the department has only one Zebra. It then turned out that many older Zebras are being decommissioned from pharmacies and could be reused in the warehouse.
- Filip: if it goes through, it's "really great", both technically and for users, because the hardware scanner is more reliable than the camera [translated from Czech].
- Not confirmed yet ([[ASM-265]]).

### Data map → spec, and the warehouse address

- Marek routed the final data map into the spec. The spec carries ~30 questions for logistics beyond the Excel. He will present and send it after the 10-15 meeting.
- Filip doesn't treat the warehouse address as solved: "where the warehouse addresses come from — we simply have to know that" [translated from Czech]. Sláma said the Excel contains it, but not always correctly (e.g. Pavlov vs. Brno), so validation is needed.
- **Options raised**:
  1. Map user identity to warehouse. Once login sends Axapta who submitted a claim, a small KB table keyed by employee email could give their warehouse. It works, but needs upkeep when people join or leave. Filip called it "a bit odd, but it would work".
  2. Device / network (IP address). Unknown whether the network setup allows it; to ask.
  3. One login account per warehouse (Marek).
  4. A warehouse dropdown in the app.
  5. A subdomain per warehouse (e.g. `brno.claims…`).
  6. Logistics simply supply correct data. Marek prefers this; Filip agrees it would be ideal.
- **Not blocking**: the only use is the delivery-note footer (which of the three warehouses it ships from). Having it before production is enough.
- **Agreed**: the spec lists it as a question for logistics, with the variants.

### X-Manager knowledge-base table

- Filip needs to know how many tables, which columns, and what to ask the X-Manager team (change logging / audit, flexibility for later changes), so BigHub doesn't find out late that the platform is wrong.
- **What's needed now**: an almost 1:1 copy of Jana Egrmaierová's supplier Excel (~10 columns × ~300 rows), imported into X-Manager. Roughly 90% stays as is; a column may be added, dropped or split.
  - Keep the supplier name, the purchase (nákupní) supplier account, address, main contact and the two contact columns. Contact cleanup is data cleaning for later.
  - Drop the "Zdroj" (source) column and the "Ekonomický dodavatel" column (the first and last columns).
  - Put the supplier account first, as the key column.
  - Basic validation: email fields allow one "@"; the supplier account is numeric, with no text or spaces.
- **Marek**: think about scalability now so BigHub doesn't lock itself in. Nesting and history are future needs, not today's blocker ("a dead-simple 10×300 table" [translated from Czech]).
- **Later**: ask the X-Manager team for a form view for adding a supplier, instead of a raw table row.
- Frustration on how long this has taken: "three weeks… no, almost three months" [translated from Czech].
- Filip is back Tuesday morning (2026-10-20).

### Phase 1 build status

- **New build** with Jana Egrmaierová's requested changes (from the 10-12 wrap-up): visual tweaks, a labelled delete button, label/field order changed and enlarged for the device, and a confirmation modal. Users were confused about what the red colour meant.
- **Device preview**: Filip built a preview at the Zebra's screen resolution.
- **Login**: the UI is added but not functional yet; it works next week. Agreed with Jura Brázdil after Dudaško's green light that BigHub manages logins itself. Until now every user had to be requested through Dudaško.
- **"WoW" with Kubčík** (term and person unclear from the transcript): now live. Kubčík first asked BigHub to enforce it inbound, then said that isn't needed, so Filip reverted it. Kubčík is satisfied.

### Error messages

- Jana Egrmaierová isn't happy with the error messages. Filip calls it valid and "probably the most constructive feedback we got" [translated from Czech].
- **Two causes**:
  - Axapta doesn't always follow the API contract (detail not sent as agreed).
  - Some cases Jana wants identified never came up in discovery. For example, "SP label not found" also appears for more granular Axapta reasons such as "SP label empty".
  - Only a few messages were defined early, with Honza (e.g. product not found, SP label not found).
- **Plan**:
  1. Marek runs a screen-share call with Jana (aiming for Friday or Monday) to collect the cases.
  2. Filip agrees the technical side with Sláma.
- **Preferred direction** (discussed lightly with Sláma on Monday): Axapta sends ready, human-readable messages that the app only displays, rather than BigHub translating codes. This also lets ViaPharma change messages without BigHub ([[ASM-270]]).

### Audit trail of changes (who did what)

- Axapta should receive who made each change, not just what changed. This is tied to login and preliminarily agreed with Sláma.
- Filip proposes doing it after login is finished.

### Communication record (PDF)

- Still undefined how the PDF record reaches Axapta. Either Axapta asks an endpoint for the record, or on case close the platform also generates a snapshot of the communication along with the delivery note and the draft.
- Marek: both points (transfer method/timing, supplier attachments) are already in the spec as yellow questions for Sláma ([[ASM-254]]).

### Testing against the mailbox

- The test mailbox is set up: kvalitasklad on the test environment (not production), as a normal Outlook mailbox.
  - It was arranged by the stand-in for V. Tvarůžek, who was "very, very good", quick and helpful [translated from Czech].
  - Filip has access through his Dr. Max account; more Dr. Max accounts can be added.
- **Open**: how users test. Drafts can't go to real suppliers, and suppliers won't reply, so testers need a target address and mock supplier replies to try the agent's handling.
- Marek: for Phase 1, testing effectively ends at the draft. Filip: they still need to see the behaviour on the test mailbox, and mock replies are needed for the reply handling.

### Phase 1.1a / 1.1b scope and tuning

- **Filip's split**:
  - 1.1a is what the demo showed: drafts (done) plus sorting incoming replies into folders by classification (human, liquidation, send to warehouse, own transport), possibly colour-coded, with a done flag that works as a to-do list.
  - 1.1b is the follow-up sequence.
- Of Jana's ~7 sample threads, ~5 were resolved by one question and one supplier reply, with no longer sequence.
- Sorting can be delivered right away; it needs tuning on more examples so it isn't "a botch" [translated from Czech].
- **Marek**: tuning belongs to the per-phase testing he added to the roadmap. Budget ~4 days per phase for feedback.
- **Conflict**: the client spec defines 1.1a as the communication audit trail (PDF record in AX) and puts reply classification in 1.1b.

## Decisions Made

- The warehouse-address source goes into the spec as a question for logistics, with the variants; it isn't blocking (needed before production).
- The KB starts as an almost 1:1 X-Manager import of Jana Egrmaierová's Excel, without the "Zdroj" and "Ekonomický dodavatel" columns, supplier account first, with basic validation. An advanced version comes later.
- The who-changed-what audit trail is implemented after login.
- Email-agent tuning happens inside per-phase UAT, with ~4 days per phase for feedback.

## Action Items

- [ ] **Marek Pillár**: Send logistics the final client spec (~30 questions + data-map outcomes) after the 2026-10-15 meeting — due 2026-10-15 — from 2026-10-14-reklamace-sync-filip-warehouse-address-xmanager-error-messages
- [ ] **Marek Pillár**: Add the warehouse-address question with its variants to the spec questions for logistics (logistics supplies it correctly / employee→warehouse table / IP / per-warehouse login / dropdown / subdomain) — from 2026-10-14-reklamace-sync-filip-warehouse-address-xmanager-error-messages
- [ ] **Marek Pillár**: Send the X-Manager team the KB table definition: Jana Egrmaierová's Excel ~1:1 without "Zdroj" and "Ekonomický dodavatel", supplier (purchase) account first, basic validation (email one "@", numeric account), noting an advanced version will follow; plus a short list of platform checks (change logging / audit, flexibility) — before Filip is back 2026-10-20 — from 2026-10-14-reklamace-sync-filip-warehouse-address-xmanager-error-messages
- [ ] **Marek Pillár**: Run a screen-share call with Jana Egrmaierová to collect the error-message cases she needs (aim Fri 2026-10-16 or Mon 2026-10-19), then hand them to Filip — from 2026-10-14-reklamace-sync-filip-warehouse-address-xmanager-error-messages
- [ ] **Filip Černý**: After the error-case list, agree the error-message mechanism with Petr Sláma (Axapta sends readable messages vs. codes translated by BigHub) — from 2026-10-14-reklamace-sync-filip-warehouse-address-xmanager-error-messages
- [ ] **Filip Černý**: Make login functional next week (BigHub manages logins itself, agreed with Jura Brázdil) — due week of 2026-10-19 — from 2026-10-14-reklamace-sync-filip-warehouse-address-xmanager-error-messages
- [ ] **Filip Černý**: After login, agree with Petr Sláma how the user identity (who changed what) is sent to Axapta — from 2026-10-14-reklamace-sync-filip-warehouse-address-xmanager-error-messages
- [ ] **Marek Pillár / Filip Černý**: Raise with logistics how users will test against the test mailbox (target for sent drafts, mock supplier replies, which Dr. Max accounts get access) — from 2026-10-14-reklamace-sync-filip-warehouse-address-xmanager-error-messages

## Open Questions

- Who supplies the processing/pickup warehouse, and through which mechanism? Six variants, with data quality in the Excel a concern.
- Is the decommissioned-pharmacy Zebra route confirmed by IT / logistics?
- How does the communication PDF record reach Axapta: an on-demand endpoint, or generated on case close?
- How do users test the mailbox flow without real suppliers (mock sender and replies)?
- Phase scope: is reply sorting into folders part of 1.1a (Filip) or 1.1b (client spec)?
- What is "WoW", and who is Kubčík?

## Sentiment & Tone

The call was practical and aligned, with some mutual pushback that clarified things. Filip corrected Marek's "both open points answered" on the warehouse address, and Marek accepted it. Filip was candid about the error messages as fair, constructive criticism that BigHub partly owes. Both showed shared frustration at how long the knowledge-base storage has taken ("almost three months"), and both clearly want the simplest unblocking step now. The tone toward the client side was warm: the infra stand-in and Kubčík were praised.

## Routing Log

Confirmed by PM 2026-10-15 ("confirm all").

- **project-assumptions**: ASM-283 (per-phase UAT, Decided), ASM-284 (1.1a vs. 1.1b reply sorting, Open), ASM-285 (who-changed-what audit trail after login, Decided); ASM-263 reopened (warehouse-address source); updates on ASM-265, ASM-270, ASM-243, ASM-254.
- **project-knowledge**: "Zebra terminals" updated; "Test mailbox kvalitasklad (Reklamace)" added.
- **project-stakeholders**: STK-044 Jana Egrmaierová updated; STK-070 infra stand-in for V. Tvarůžek added (low confidence).
- **project-daily**: 7 action items added; "send the final spec" merged into the existing spec item; build-check and Zebra items annotated.
- **Not routed**: "WoW" / Kubčík, which is unclear from the transcript.
