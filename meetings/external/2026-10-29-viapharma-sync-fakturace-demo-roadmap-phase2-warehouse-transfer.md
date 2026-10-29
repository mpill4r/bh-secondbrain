---
last_updated: 2026-10-29
type: external
attendees: [Tereza Foltová, Jan Žižka, Jana Egrmaierová, Jan Kopecký, Jindřich Tůma, Marek Pillár]
recording_link:
---

# ViaPharma Sync — Fakturace Demo, Axapta Lookup Not Real Yet, Roadmap for Žůrek & Phase 2 Without Label Reading

**Date**: 2026-10-29 (Thursday, ~47 min)
**Attendees**: Tereza Foltová (ViaPharma, logistics), Jan Žižka (ViaPharma, transport; Fakturace part only), Jana Egrmaierová (ViaPharma, claims), Jan Kopecký (ViaPharma, Axapta/IT), Jindřich Tůma (BigHub), Marek Pillár (BigHub, PM). Absent: Petr Sláma (WMS), Petr Spilka, Filip Černý (holiday).
**Type**: external (client)
**Recording**: N/A
**Previous session**: [2026-10-22 ViaPharma Reklamace sync](2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel.md)
**Meeting prep**: [2026-10-29 prep](../prep/2026-10-29-viapharma-logistics-status-demo-roadmap-meeting-prep.md)

## TL;DR

Marek demoed the Fakturace doprav mock. It reads the route and the page count, tells night delivery from ZOPV, and counts stamps. Logistics will try it via a link from the recap. Kopecký warned that Axapta's route interface only returns a reply for any AR number and doesn't look anything up yet.

In Reklamace, login works (Egrmaierová tested it) and the roadmap was walked through ahead of Monday's Žůrek meeting. Egrmaierová corrected the Phase 2 spec. Goods are first transferred to a non-selling warehouse and the claim is made from there, so reading product labels in the warehouse isn't needed. Kopecký settled error messages: Axapta owns the codes and texts, and only a few key cases need listing.

Compared with 10-22: login and the X-Manager knowledge base are delivered, and Egrmaierová's process description arrived (not yet reflected in the roadmap). Sláma's Axapta work and the Fakturace mapping review are still stalled until he's back next week.

## Key Discussion Points

### Fakturace doprav — status and demo

- Foltová: nothing new on Fakturace. Sláma hasn't got to it, and the Canon contact is on holiday this week, so the scanner test hasn't moved. She calls Canon on Monday.
- Marek demoed the scan flow on Filip's test scans:
  - route read, "page x of 6", document type (night delivery vs. ZOPV), stamps counted
  - a summary of scanned and missing pages and the stamp count
  - the UI still overflows in places
- Limits he stated: testing only on the prepared routes; not every real document carries the AR number (Filip added it by hand).
- Stamps: the system recognises that a stamp is there, but the count needs a human check for now. Up to ~95 % accuracy is possible with sample stamps and some extra days.
  - Foltová asked whether it learns over time (90 → 99 %). Marek: yes, gradual improvement is possible.
  - Nothing goes live without the end user approving. A confidence score could let users skip checks on high-confidence cases, by agreement.
- Žižka wants to try it himself. Marek sends the link in the recap. He told them there is no login restriction and that the link "should work without VPN". **Filip's note says it is reachable from the VPN**, so this needs correcting in the recap.
- Double-sided scanning: the app doesn't care (one scan = one file; PNG, JPG and PDF are all fine). It is a scanner setting. Foltová: drivers shouldn't be able to touch settings; they just insert the paper.
- Egrmaierová: a temperature printout from the datalogger is attached to the rozvozový list. Žižka: the new ZOPV leaves space for it so it doesn't cover readable data; to be tested on the borrowed scanner.
- Egrmaierová: the example lacks the **expedition stamp**. The sentence "temperature during transport was / wasn't kept" should be ticked and checked by the AI, because the documents are shown at inspections.
  - Žižka: "honestly, nobody ticks it here". The next step of the project is AI verifying temperatures from the printouts.
  - Egrmaierová: "Sacha" should approve if the sentence is dropped.
  - Žižka and Egrmaierová agree it between themselves and give Foltová the outcome.
- Marek: temperature labels and checkboxes are a separate scope, to be estimated, and can be added if they fit the timeline.
- Marek has sent the Fakturace Excel (the agreed mapping incl. communication) for confirmation. Žižka goes through it tomorrow.
- Foltová: Sláma is available next week and will finish the Axapta work.
- **Kopecký**: the Axapta interface for Fakturace "just returns something". Any call with an ID starting with AR passes; it doesn't really search. "We have nothing set up, it will have to be built." [translated from Czech]
  - Axapta could also confirm the document type (night delivery / ZOPV), giving a double check.
  - In theory Axapta could find the AR from a document number, "but we probably shouldn't". Marek agreed.

### Reklamace — login and access

- Entra login works; without access the app refuses entry. Egrmaierová tested it: "it works".
- Access today: Egrmaierová, Foltová, Marek, Jindřich, Filip. Add **Spilka**; Žůrek isn't needed. Anyone missing access writes to Marek.

### Reklamace — roadmap

- Marek showed the roadmap (built with Jindřich and Filip). It goes to Žůrek on Monday 11-02 and will be updated after every sync. It replaces the to-do e-mails.
  - Cell notes explain each row.
  - BigHub delivers Phase 1 within 5–7 working days once unblocked (Axapta done, API approved). Ideally development is done by Tue 10 Nov; testing dates will shift.
  - Deadlines are only what was said in meetings; shifts are expected.
- Foltová: it makes sense, since Žůrek will want to see a roadmap. Several items are already done but sit in e-mails Marek hasn't processed yet (the holiday week).
- Knowledge base: imported into X-Manager and reachable via API; set up with Machata early this week.
- **Kopecký**: work on the API contract is in progress. **Boomi** is a middle layer, so even when Axapta is done Boomi may not be. He wants it noted in the roadmap: a potential delay of about a week.
- E-mail testing: Foltová defines the preliminary 3 accounts.
- Sláma's estimate cells are highlighted for him to fill without pressure.

### Knowledge base (X-Manager) ownership and access

- Foltová asked who owns it. Jindřich: Machata owns the platform, but the access process may change. BigHub will specify it and hand over documentation and how-tos. Some users get write rights.
- Foltová sends **4–5 names**: one person per warehouse plus herself and Egrmaierová. Marek: access likely only once Filip finishes the integration.

### Phase 2 spec correction (Egrmaierová)

- Today, goods on a selling location are first moved by an **operational transfer** to a non-selling warehouse. The claim protocol is then created from there.
- Creating it straight from selling locations would break: there are running sales and reservations. The claim protocol isn't a transaction until it's accepted (negative purchase order), so quantities could no longer match.
- So the spec skipped the transfer step. Claims are made from the non-selling warehouse, and **label reading isn't needed**. There's one label per warehouse (5RV, 9RV; Prague / Ostrava), which she sends today.
- Marek: valid. The spec came from Honza Sovka's documentation and he missed this; he will revise it and welcomed quick 1:1 clarifications.

### Done items and the user description

- Egrmaierová's user manual / process description was shared by Foltová right after Monday's meeting (link in the Reklamace folder). "Jana has everything done."
- Marek: the roadmap doesn't reflect the e-mails yet; he updates it by tomorrow at the latest so Monday shows reality.

### Error messages

- Foltová: Sláma says error messages are for logistics to define, not him.
- Egrmaierová assumed the API returns what it can.
- **Kopecký**: Axapta holds and manages the error codes and the user texts itself, and the app just displays them. The text can be tuned with end users and hotfixed later, so a list is "almost pointless" unless something obvious comes to mind.
  - Every listed message commits them to returning and testing it, so **max ~3**.
  - Marek: matches the earlier agreement; Pareto approach, tests fill the rest.
- Egrmaierová writes a short list anyway. Today every failure returns a generic "položka nenalezena" (404). She wants "label doesn't exist" distinguished, because "položka" means the product to warehouse staff.
- Foltová adds comments on problem types to the spec.

### 2027 initiatives (logistics)

- Marek: Foltová's list is the best-prepared so far. He'll respond and add value-calculation guidance to fill async, by Monday at the latest.
- Foltová: not needed for Žůrek on Monday. Maroušek only edited wording; once copied into BigHub's table it is closed.

## Decisions Made

- Error messages: Axapta owns codes and user texts; the app only displays them. Logistics lists only a few key cases (max ~3), e.g. "label doesn't exist" vs. generic "item not found".
- Phase 2: claims are created from the non-selling warehouse after an operational transfer; warehouse label reading isn't needed (one label per warehouse). Spec to be revised.
- Spilka gets Reklamace access; Žůrek doesn't.
- The roadmap is the shared status tool, updated after each sync and shown to Žůrek on Monday 11-02.
- Temperature printouts, expedition stamp and transport checkbox checks are a separate scope, estimated later.
- Knowledge-base access for logistics comes after Filip finishes the integration; Foltová names 4–5 people.

## Action Items

- [ ] **Marek Pillár**: Send the recap with the Fakturace demo link (correct the VPN statement per Filip) and the request for 4–5 knowledge-base names — due 2026-10-29 — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Marek Pillár**: Process the logistics e-mails and update the roadmap for Monday: mark Egrmaierová's description done, add the Boomi risk (~1 week), label samples, error-message approach, Phase 2 AX row — due 2026-10-30 — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Marek Pillár**: Revise the Phase 2 spec: operational transfer to the non-selling warehouse, claim from there, no label reading — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Marek Pillár**: Respond to Foltová's 2027 initiatives list with value-calculation guidance (async) — due 2026-11-02 — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Marek Pillár / Filip Černý**: Give Petr Spilka access to the Reklamace app — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Jan Žižka**: Review the Fakturace mapping Excel — due 2026-10-30 — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Jan Žižka / Jana Egrmaierová**: Agree on the expedition stamp and the transport-temperature checkbox (incl. Sacha's sign-off); give Foltová the outcome — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Tereza Foltová**: Call Canon on Monday about the scanner test — due 2026-11-02 — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Tereza Foltová**: Send 4–5 names for knowledge-base access (one per warehouse + Foltová + Egrmaierová) — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Tereza Foltová**: Add comments on problem types to the Reklamace spec — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Jana Egrmaierová**: Share one label sample per warehouse (5RV, 9RV) in the Reklamace folder — due 2026-10-29 — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Jana Egrmaierová**: Send Kopecký a short list of key error cases (max ~3) — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Jan Kopecký / Petr Sláma**: Build the real AR route lookup in Axapta for Fakturace — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Petr Sláma**: Finish the Axapta work (Reklamace + Fakturace) on return — due week of 2026-11-02 — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer
- [ ] **Jindřich Tůma**: Specify the knowledge-base access process and hand over docs / how-tos — from 2026-10-29-viapharma-sync-fakturace-demo-roadmap-phase2-warehouse-transfer

## Open Questions

- Does the Fakturace demo link need VPN for logistics (Filip: yes)?
- When will Axapta's real route lookup and Boomi be ready?
- Is the transport-temperature sentence kept (then it must be ticked) or dropped (Sacha to approve)?
- Who is "Sacha" (QA / quality?) — not yet in the stakeholder map.
- How far does the Phase 2 correction shrink the AX work (label lookup by EAN, batch, expiry)?

## Sentiment & Tone

Constructive and noticeably warmer than recent syncs. Foltová welcomed the roadmap as exactly what Žůrek will ask for, and teased that "Jana has everything done" while gently pointing out that Marek is behind on their e-mails. Marek owned it openly (holiday week). Egrmaierová was precise and helpful: her Phase 2 correction came as domain expertise, not criticism, and Marek took it gracefully.

Kopecký was the realist: twice he made sure nobody overestimates Axapta (the Fakturace interface is a stub, Boomi adds about a week). He also simplified error messages in BigHub's favour. Žižka was engaged and wants to try the demo himself.

Watch:
- Marek's backlog of unprocessed client e-mails is visible to the client.
- Sláma remains the bottleneck for both streams.

## Routing Log

Confirmed by PM (2026-10-29, "confirm all"):

- **project-assumptions**: added ASM-361–ASM-364; updated ASM-325 (→ Decided), ASM-358, ASM-318.
- **product-requirements**: added REQ-017.
- **project-knowledge**: Reklamace (warehouse claims flow); Fakturace doprav document flow.
- **project-stakeholders**: Egrmaierová, Kopecký, Foltová, Žižka, Spilka.
- **project-daily**: 15 action items added; 6 closed; 7 annotated.
- **project-lessons**: LL-112.
