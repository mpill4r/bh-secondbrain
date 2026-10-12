---
last_updated: 2026-10-12
type: internal
attendees: [Marek Pillár, Filip Černý]
recording_link:
---

# Sláma's Data-Map Feedback Walkthrough, Fakturace Doprav State Conflict & Listing Follow-ups with Filip Černý

**Date**: 2026-10-12 (Monday)
**Attendees**: Marek Pillár (STK-001, BigHub — Reklamace spec owner), Filip Černý (STK-006, BigHub — Reklamace / Fakturace doprav / Listing dev)
**Type**: internal
**Recording**: N/A (transcript, ~29 min, Czech/Slovak)
**Previous session**: [2026-09-30 Reklamace Thursday prep — data-map walkthrough](2026-09-30-reklamace-thursday-prep-data-map-demo-review.md) · related: [2026-10-08 ViaPharma Reklamace sync](../external/2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity.md)
**Meeting prep**: N/A

> **Transcript note**: "ak zapta" = Axapta; "Sláva" / "Slama" = Petr Sláma (STK-034); "paní Ing. Majová / Majerová" = Jana Egrmaierová (STK-044); "Honza" = Jan Sovka; "rozhlasovej list" = rozvozový list (delivery note).

## TL;DR

Petr Sláma's column-J feedback on the Reklamace data map has arrived, and he contested nothing: almost all supplier data lives in BigHub's knowledge base (a side table logistics maintain), with Axapta keeping only the supplier account as the key. Only two rows are unclear (row 17 "Způsob vyřízení" and the warehouse address on the delivery note). Marek will answer in a new column K and offer Sláma a call. Separately, Sláma's new Fakturace doprav proposal says BigHub holds each case until it is closed, which contradicts Jan Žižka's earlier "Axapta gets every scan immediately" ([[ASM-053]]). Filip wants Sláma and Žižka in one meeting (likely Thursday) to settle it. The X-Manager direction is "very likely" for Reklamace supplier data, but not decided.

**Continuity with 2026-09-30 / 10-08**: the data map, blocked since 10-01 ([[ASM-229]]), is finally reviewed, and the direction from 10-01 ([[ASM-228]]) holds with Sláma's sign-off. The knowledge-base decision is now close; the 10-16 target ([[ASM-184]]) looks reachable if Sláma responds to column K quickly. New friction moved to Fakturace doprav.

## Key Discussion Points

### 1. Sláma's data-map feedback: approved almost entirely

**Marek** had only skimmed it; it looked to him as if Sláma "approved everything". **Filip** had read it: all comments are "fine, valid", with two rows he didn't understand.

**Filip** on the overall direction: "it looks like he wants to move everything to us, and I think that's right… it'll live in a side table that they maintain themselves. A lot of that information doesn't belong in Axapta anyway." [translated from Czech] Asked by Marek whether any data must technically stay in Axapta, Filip said no: "it makes little sense for it to sit in a warehouse management system." [translated from Czech]

Row by row:

| Row / item | Sláma's position | BigHub view (Filip) |
|---|---|---|
| Supplier account | Confirmed as Axapta's primary key | As expected |
| Return address | Knowledge base | Agreed |
| Pickup type | Already agreed | — |
| Delivery-note (rozvozový list) template | Template must be sent to them; something to add to the API | Borderline data item; Filip believes it's already in the API (tested). Sláma likely means implementation on ViaPharma's side, which doesn't concern BigHub |
| Main contact / other contacts / contact by step | Knowledge base | Agreed; don't split contacts between Axapta and the KB. "Contact by step" needs defining and relates to the broader agentic system. Current structure not ideal; BigHub fixes it |
| Okamžité avízo | Wants it in the KB, doesn't know what it means | Specific case for a few suppliers, deprioritised with Jan Sovka ([[ASM-240]]). Filip has started it on a branch; a few unclear or contradictory details. Easy to finish once agreed with logistics |
| Row 13 (May comment, where to store) | — | Resolved: storage location now agreed. Marek counts it as done |
| Notes | Proposes notes live with BigHub and **Axapta acts as the frontend**: the platform sends per-supplier notes for each case, Axapta displays them | Filip likes it: an alternative to his Outlook side-panel idea, minimal implementation on both sides |
| Standard / specific procedure flag | Sláma seems to misread it | Today = the blue-coloured suppliers (some unnecessarily). No separate flag needed: if a supplier has an instruction, follow it, otherwise standard |
| Photo instructions | Knowledge base | Easy to add to the app (~half an hour), but the information doesn't exist. Filip guesses ~5 of ~300 suppliers |
| Follow-up email threads / procedures | — | Only a basic picture: ~7 real conversations; the demo covered 6 of 7. More real examples needed |
| Row 17 "Způsob vyřízení" (resolution method) | Extend the app to show it; send it from Axapta to the AI platform | Filip doesn't know what it is (an Axapta code list that came up only recently). Thinks the direction should be reversed: the platform proposes the resolution (e.g. credit note). Sláma may have written it backwards. Flag for clarification |
| Claim number, document number, issue date | — | Clear |
| Warehouse address on the delivery note | Big open question: which warehouse (e.g. Brno vs. Pavlov) the claim is processed in | Neither Axapta nor BigHub has it; someone must find out who does. Simplest: the warehouse sends the address. Options: IP-based detection (Marek: "overkill"), a subdomain per warehouse (e.g. pavlov.reklamace…). Needs a decision |
| Manual fields on the delivery note | Written by hand with a marker | Fine. No OCR needed; the document leaves BigHub's scope |

**Filip**'s caveat: the knowledge base won't map one Excel row to one column. Some rows collapse into one column, others grow into separate tables. BigHub designs it, owns it during development (changing it freely, since nobody else consumes it yet), then hands it over and trains someone to maintain it. **Marek**: the Excel was only a way to present the features, so its shape doesn't matter.

### 2. Email agent: first-phase scope

**Filip**: first phase is folder sorting (already built; just needs deploying), then drafting. Where a clear decision exists (typically yes / no), draft both emails; the person picks one and sends it. Jana Egrmaierová is fine with this. Still to discuss: which cases and warehouses are in play.

### 3. How to close the data map

**Marek**: he'll add a **column K** with notes from this meeting. Where BigHub agrees, no note; where there's a question or answer, he writes it there. Sláma can respond on the 2–3 open rows, and then the data map counts as done. Sláma had offered a call; **Filip** is happy to talk to him directly ("so there are no changes later"). Marek will DM Sláma that a call is welcome and ask him to propose a time. Filip: the call could cover Reklamace too, if Sláma prefers talking to writing.

### 4. X-Manager

**Marek** (not a decision yet): BigHub will "very probably" go with X-Manager, following last week's talk with its product owner. The product owner was easy-going and pleased BigHub wants to build in it, and BigHub should be able to bend it to its needs ([[ASM-243]]).

### 5. Sláma's email: Fakturace doprav proposal and the state conflict

Sláma's email contained a proposal for how Fakturace doprav should work (also posted in Teams). He approved the simplified Swagger (v0.9.11) and doesn't want it simpler. It also had a document Marek didn't recognise; Filip reads it as a spec.

**Filip**: Sláma's concept (BigHub holds the whole case until it is closed, then hands it to Axapta) is what Filip originally understood too. But at the meeting where Filip asked for the transcript, Jan Žižka said Axapta must get information immediately: "when something is scanned, it goes to Axapta." [translated from Czech] That means open cases live in Axapta, which contradicts Sláma's proposal ([[ASM-053]]).

**Filip**: don't make a point of the contradiction; just get Sláma and Žižka together and ask "so how will it be?". "Each of them clearly sees it differently, and they need to agree on what they want." [translated from Czech] Sláma proposes discussing it on Thursday; Marek isn't sure Žižka can join sooner.

**Marek** will reply to the email: the Excel is filled in with questions; he is updating the spec as agreed; and yes to the meeting, to settle it without escalating.

### 6. Listing: Neuman's email

**Filip** asked if anything is expected from him: Petr Neuman (STK-023) sent an incomplete catalogue, which seems pointless since a new one is coming soon. **Marek** agreed it likely doesn't help; what's still owed is the **cost breakdown** and the **legal write-up**. **Filip** admitted he hasn't done the legal part ("I keep forgetting, because I'm always on logistics") and will do it this afternoon as a priority. **Marek**: answer Neuman's email with the cost breakdown (what it would cost on BigHub's side) as one or two one-pagers, plus the legal part. Marek will look at Neuman's comments in the catalogue (basic, nothing drastic).

## Decisions Made

1. **Data map closes via column K**: Marek adds BigHub's notes and questions in column K; Sláma responds on the 2–3 open rows; then the data map counts as done. A call with Sláma is offered, at his choice.
2. **Supplier data lives in BigHub's knowledge base**, not Axapta; Axapta keeps only the supplier account as the key. Sláma's feedback confirms the 10-01 direction ([[ASM-228]]). No data was identified as technically required in Axapta.
3. **No separate "standard / specific procedure" flag**: a supplier with an instruction gets it followed; otherwise the standard procedure applies.
4. **Row 13 (Sláma's May comment on storage) counts as resolved.**
5. **Don't escalate the Fakturace doprav state contradiction**: get Sláma and Žižka in one meeting (likely Thursday 2026-10-15) to agree.

## Action Items

- [ ] **Marek Pillár**: Add column K to the data-map Excel with this meeting's notes and questions (row 17 "Způsob vyřízení" direction, warehouse-address source, delivery-note template / API, okamžité avízo meaning) and tell Sláma when done — due 2026-10-12 — from 2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict
- [ ] **Marek Pillár**: DM Petr Sláma that a call on the data map (and Reklamace) is welcome; ask him to propose a time — from 2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict
- [ ] **Marek Pillár**: Reply to Sláma's Fakturace doprav email: Excel filled in with questions, spec being updated, yes to a meeting with Sláma + Jan Žižka (likely Thursday) on where open-case state lives — from 2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict
- [ ] **Marek Pillár**: Send Filip Černý the transcript of the meeting where Jan Žižka said Axapta must receive scans immediately — from 2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict
- [ ] **Filip Černý**: Do the Listing legal write-up today, as a priority — due 2026-10-12 — from 2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict
- [ ] **Filip Černý**: Prepare the Listing cost breakdown (own solution vs. third-party) as one or two one-pagers, as the reply to Petr Neuman's email — from 2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict
- [ ] **Marek Pillár**: Review Neuman's comments in the catalogue — from 2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict

## Open Questions

- **Row 17 "Způsob vyřízení"**: what is it, and which direction does it flow? Axapta → platform (as Sláma wrote) or platform → Axapta as a proposed resolution (Filip's reading)?
- **Warehouse address on the delivery note**: who knows which warehouse a claim is processed in? Warehouse sends it, IP detection, or a subdomain per warehouse?
- **Photo instructions**: does this information exist for any supplier?
- **Follow-up email threads**: can logistics provide more real conversations beyond the ~7 Filip has?
- **Fakturace doprav**: does BigHub hold the case until it is closed (Sláma), or does Axapta get every scan immediately (Žižka, [[ASM-053]])?
- **X-Manager vs. SharePoint List** for supplier data: when is it decided, and who tells logistics?

## Sentiment & Tone

Relaxed and well aligned. Marek was under the weather and let Filip lead the row-by-row review; Filip came prepared, with a clear technical view and a pragmatic, non-confrontational stance towards ViaPharma ("let's not rub it in that they contradict each other"). Both read Sláma's feedback as a positive turn: he signed off the direction BigHub wanted. Filip was a bit sheepish about forgetting the Listing legal work and committed to it the same afternoon.

## Routing Log

Confirmed by PM on 2026-10-12 (confirm all).

- **project-assumptions**: added ASM-260 to ASM-264; ASM-228 → Decided; ASM-053 → Open (disputed); updates on ASM-229, ASM-243, ASM-240, ASM-224, ASM-184
- **project-stakeholders**: STK-034, STK-006
- **project-knowledge**: "Způsob vyřízení"; data-map Excel columns J / K
- **project-daily**: 5 PM-owned items added; data-map, Listing legal and cost-breakdown items annotated; Sláma column-J chases closed. Filip's items stay in this note.
- **project-lessons**: LL-89
