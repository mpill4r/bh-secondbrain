---
last_updated: 2026-10-15
type: external
attendees: [Jindřich Tůma, Marek Pillár, Tereza Foltová, Petr Sláma, Petr Spilka, Jana Egrmaierová, Jan Žižka]
recording_link:
---

# ViaPharma Reklamace Sync: Pickup Warehouse Settled, Zebra Chosen, Error Messages from Axapta & BrightPick Squeezes Sláma's Capacity

**Date**: 2026-10-15
**Attendees**:
- BigHub: Jindřich Tůma, Marek Pillár (PM)
- ViaPharma: Tereza Foltová (project lead, logistics), Petr Sláma (IT / Axapta), Petr Spilka (logistics, decision-maker), Jana Egrmaierová (claims, end user), Jan Žižka (transport, joins Thursdays when he can)
- Filip Černý absent (on leave until Tuesday 2026-10-20)

**Type**: external
**Recording**: N/A
**Previous session**: [2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity](2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity.md) (wrap-up in between: [2026-10-12](2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state.md))
**Meeting prep**: [2026-10-15-viapharma-logistics-status-meeting-prep](../prep/2026-10-15-viapharma-logistics-status-meeting-prep.md)

## TL;DR

- **Warehouse address solved.** It turned out to be two different facts. The warehouse where a claim originates is fixed per user (from login, or Axapta returns it via the API). Where the supplier picks the goods up is a property of the supplier, written as a sentence in the knowledge base; if the sentence is missing, the default is the originating warehouse.
- **Device: Zebra**, an older model for the start; mobile phones can't meet the security requirements. Spilka agreed, pending his email confirmation.
- **Error messages will come from Axapta.**
- **Sláma's capacity:** he goes onsite for BrightPick from 2026-11-16 (go-live around the turn of Nov/Dec) and has limited capacity until year-end. Spilka: BrightPick has priority and Reklamace has no fixed date. BigHub owes a roadmap next week showing durations and what each phase needs from ViaPharma; ViaPharma then decides the timing.

## Key Discussion Points

### Continuity with the 2026-10-08 sync and the 10-15 prep

- **Data map:** closed. Sláma's last open row was clarified today.
- **Testing:** done, and Filip has worked through most findings.
- **Device:** decided in principle (Zebra).
- **Still owed:** the Reklamace spec (Marek promises it today or tomorrow morning) and the roadmap (Jindřich apologised; it slips to next week).

### X-Manager for the knowledge base

- Jindřich: BigHub met the X-Manager owner this week, and it "looks like the most suitable candidate". BigHub sends the request to create the tables today, so Filip can work with them next week ([[ASM-243]]).

### Warehouse address vs. pickup location

- **Marek** raised the last open data-map point: how BigHub knows which warehouse the scanner (Zebra) is in. Filip had warned that the mapping isn't accurate.
- **Sláma**: two things got mixed up.
  1. **Where a person works and where the claim originates** is fixed: "each person works in one warehouse". It can come from the login, or Axapta can return it via the API when the SP label is scanned.
  2. **Where the supplier collects the goods** is the question in the Excel. Even if a claim originates in Pavlov, ViaPharma may move the goods to Brno by internal transport, and the supplier picks them up there. "That's a property of the supplier", so it belongs in the knowledge base, and it can change [translated from Czech].
- **Format:** a sentence in the KB, e.g. "Dodavatel vyzvedává ve skladu Brno" ("the supplier collects in the Brno warehouse"). If nothing is written, the pickup is at the workplace where the claim originated. Logistics corrects wrong entries.
- **Jana Egrmaierová**: "Brno — I wanted to add that, I have it there" [translated from Czech]. The expedition team knows each case (own transport vs. the internal shuttle to Brno), so the KB can be filled in continuously.
- **Sláma**: "If it isn't there, tough luck — someone set it up wrong" [translated from Czech]. Not a blocker.
- **Marek**: considers it closed and will agree the details with Filip when he's back.

### Testing, error messages, login

- **Testing:** Jindřich says testing is closed. Filip has handled most of the bug list; thanks to logistics.
- **Error messages:** also come from the Axapta side, and BigHub didn't know about all of them. Sláma and Filip align next week.
  - **Sláma**: both sides prefer the messages to come from Axapta. "The warehouse changes the texts often… so I'd rather pull them from Axapta, where we can change them quickly and internally" [translated from Czech].
  - **Marek**: also offered a one-hour session with Jana Egrmaierová to go through which message belongs where.
- **Login:** Filip didn't make it this week and does it next week. OAuth on the infrastructure side is ready, so "no catch there".

### Roadmap, estimates and Sláma's capacity (BrightPick)

- **Jindřich**:
  - The roadmap wasn't delivered (X-Manager took priority) and comes next week.
  - Filip's estimate for Phase 1 + 1.1a comes next week. The target is to finish Phase 1 + 1.1a within 14 days, i.e. by end of October.
  - The roadmap shows durations, not dates. For example, Phase 2 is roughly 4 weeks of BigHub development plus 2 weeks of ViaPharma testing.
  - Ideally, before the roadmap, a short per-phase analysis tells Sláma what BigHub needs from him ("A, B, C, D"), so he can estimate his part. That gives a timeline per phase (e.g. 3 weeks BigHub + 2 weeks Sláma + 2 weeks testing).
- **Sláma**:
  - In ~14 days he goes to Ostrava to implement and test **BrightPick**. He'll be "out until the end of the year", with limited capacity, though not zero.
  - Development must finish within the next 14 days. From **2026-11-16** the team is onsite for 14 days of intensive testing, the only window with the robots. Go-live is at the turn of Nov/Dec, then post-go-live support, with more BrightPick phases in January.
  - He asked whether the roadmap will show what ViaPharma must do. "Eddy" wanted the AI things done before then. Priority is Spilka's call.
- **Spilka**:
  - ViaPharma must adapt to BrightPick: external suppliers, budget and promised dates are involved. Full BrightPick operation is targeted around the end of February.
  - "I can't imagine slowing BrightPick down because of BigHub development"; for Reklamace "there's no date set in stone" [translated from Czech]. Dates will have to be "rubbery".
  - Meanwhile BigHub could work on things that don't depend on Sláma.
- **Jindřich**: "the ball is on our side". BigHub puts the work and time on the table; if ViaPharma then says "next year", that's valid.
- **Tereza**: accepts the slip and wants something in hand to plan with.
- **Marek**: the roadmap's purpose is to show what BigHub works on, when, and what it needs from ViaPharma. The Phases 3–5 discovery (Tereza and Jana are compiling the input) will weigh where Sláma's input is needed and look for parts that need little of it.

### Zebra vs. phones: Zebra

- **Tereza** met Dušan (IT) and Filip yesterday. Phones were the priority, but "we can't get around the security". The proposal is Zebras: Dušan found an older Zebra model he can distribute to the warehouses. His email went to Spilka yesterday afternoon (15:51).
- **Spilka**:
  - "If we can't, we'll go with the reader." He asked IT to pick the best model on price/performance.
  - The proposed reader is no longer hardware-supported and would run through a browser.
  - Longer term, hardware investment may be needed if the benefit materialises; "for the start it's enough".
  - He'll reply-all to confirm.
- **Tereza**: Zebras have big advantages (the scanner) even if they're less user-friendly than a phone. Filip gets a Zebra for testing.
- **Jindřich**: asks for email confirmation of the Zebra type.

### Fakturace doprav

- Jan Žižka will join the Thursday syncs when he can.
- **User description:** after the 10-14 meeting (Filip, Sláma), Tereza and Žižka add a user-level description to the spec. They meet tomorrow (10-16), and Tereza sends it by email so only Marek edits the spec ("so we don't blow the spec apart" [translated from Czech]).
- **Canon visit:** Tuesday 2026-10-20. Mr. Hnilička (Canon) comes to the warehouse, and Žižka shows him where devices could go. A 30-min call follows (Filip is needed) to move the kiosk idea forward.
- **Sláma's recap of 10-14** ([[ASM-053]]):
  - The platform sends documents to Axapta immediately, even incomplete, with a complete/incomplete status.
  - Axapta keeps no history: on each new scan the platform sends the merged document, and Axapta replaces the old file.
  - Žižka sees per route which documents are complete, incomplete or missing.
- **Open for Sláma:** how the billing record behaves when it was created from an incomplete document and the complete one arrives. Update it? Overwrite even if transport staff already edited values manually ([[ASM-280]])?
- **Marek**: building the mapping Excel over the next days, checks it with Filip on Tuesday; it becomes the base of the Fakturace spec.

### Reklamace spec

- **Marek**: the approved data map is routed into the spec, which lands today or tomorrow morning. It carries many business-owner questions, so ViaPharma should reserve time to answer them.

### 2027 initiatives (logistics)

- Tereza sent Excels and points to Spilka and Jan Maroušek yesterday. She wants to sit with them first, then hand the complete list to Marek; they can add "a thousand more points" and prioritise later. Pricing tools ("cenařky") came up as a possible item [transcription unclear].

### UAT approach

- **Marek**: plan testing time after every phase or set of tasks. Ideally test smaller pieces promptly as a "second set of eyes", like this week's quick turnaround on Filip's changes.
- **Jindřich**: there are usually two UAT types. Quick functional checks take little time. A final complete test at the end of each phase needs detail and time. BigHub always announces which is needed in advance.

## Decisions Made

- **Pickup location:** a supplier property in the KB, as a sentence. If missing, the default is the originating warehouse; logistics fills in and corrects entries. The originating warehouse comes from the user (login) or the Axapta API.
- **Error messages:** come from Axapta; the platform displays them.
- **Device:** Zebra (older model for the start), pending Spilka's email confirmation; hardware investment possible later.
- **Roadmap:** durations per phase (BigHub dev, Sláma's part, ViaPharma testing), not fixed dates. ViaPharma decides timing given BrightPick priority.
- **Fakturace user description:** sent by email; Marek is the only spec editor.
- **UAT:** after each phase or set of tasks: quick functional checks plus a final full test. BigHub announces the type in advance.

## Action Items

- [ ] **Jindřich Tůma**: Send the X-Manager table request today — due 2026-10-15 — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] **Jindřich Tůma / Marek Pillár**: Deliver the Reklamace roadmap next week, with durations per phase, what BigHub needs from ViaPharma / Sláma, and UAT windows — due week of 2026-10-19 — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] **Filip Černý**: Estimate for Phase 1 + 1.1a (target: done by end of October); login next week — due week of 2026-10-19 — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] **Filip Černý / Petr Sláma**: Align on error messages coming from Axapta — due week of 2026-10-19 — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] **Marek Pillár**: Send the Reklamace spec (data map routed, business-owner questions) — due 2026-10-16 morning — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] **Marek Pillár**: Build the Fakturace doprav mapping Excel; review with Filip on Tuesday 2026-10-20 — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] `waiting` **Petr Spilka**: Confirm the Zebra choice by reply-all on Dušan's email — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] `waiting` **Tereza Foltová**: Give Filip a Zebra for testing — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] `waiting` **Tereza Foltová / Jan Žižka**: Email Marek the Fakturace doprav user description after their meeting — due 2026-10-16 — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] `waiting` **Tereza Foltová**: Canon visit (Hnilička + Žižka on site) and 30-min call with Filip — due 2026-10-20 — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity
- [ ] `waiting` **Tereza Foltová**: Hand Marek the complete logistics 2027 initiatives list after sitting with Spilka and Maroušek — from 2026-10-15-viapharma-reklamace-sync-pickup-warehouse-zebra-brightpick-capacity

## Open Questions

- Fakturace: when the billing record exists for an incomplete document and the complete one arrives, update it? Overwrite manual edits by transport staff? ([[ASM-280]])
- Who is "Eddy" (wanted the AI work done before BrightPick)?
- Which Zebra model exactly, and how many units per warehouse?
- What exactly does BigHub need from Sláma per phase, and how much time is that? (input to the roadmap)

## Sentiment & Tone

The meeting was cooperative and efficient (30 minutes), with a clear realism shift.

- **Data map:** the last row closed without friction. Sláma corrected the misunderstanding helpfully, and Jana backed him with operational detail.
- **Capacity:** the main tension. Sláma was apologetic but firm that BrightPick takes him out until year-end. Spilka was candid that Reklamace ranks below BrightPick and has "no date set in stone". There's a relationship signal here: ViaPharma frames Reklamace as an improvement project between "two players", while BrightPick carries external commitments.
- **BigHub:** Jindřich handled it well by putting the "ball on our side" (show the work, let them decide timing). That avoids pressure and keeps BigHub credible, but it means Reklamace timing is now effectively in ViaPharma's hands.
- **Tereza:** accepting and plan-oriented.
- **Zebra:** Spilka visibly didn't want to own the decision but agreed pragmatically.
- **Roadmap:** Jindřich's second apology for the late roadmap is a small credibility cost, so next week's delivery matters.

## Routing Log

Confirmed by PM 2026-10-15 ("confirm all").

- **project-assumptions**: ASM-286 (Phase 1 + 1.1a by end of October, new); ASM-263, ASM-265, ASM-270 → Decided; updates on ASM-243, ASM-257, ASM-248, ASM-283 (2 weeks of client testing incl. ~4 days of BigHub feedback work), ASM-280, ASM-281.
- **project-stakeholders**: Petr Spilka, Petr Sláma, Jan Žižka updated; STK-071 Hnilička (Canon) and STK-072 "Eddy" added (low confidence).
- **project-knowledge**: "Zebra terminals" updated; "BrightPick" added.
- **project-daily**: 11 action items; warehouse-address and device items closed; 3 annotated.
- **Follow-on**: spec v2 and the roadmap blockers updated (warehouse address, device, error messages resolved; Sláma / BrightPick capacity added).
