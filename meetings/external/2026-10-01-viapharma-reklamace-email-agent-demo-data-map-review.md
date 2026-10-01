---
last_updated: 2026-10-01
type: external
attendees: [Jindřich Tůma, Marek Pillár, Filip Černý, Petr Sláma, Tereza Foltýnová, Jana Egrmaierová, Kim Sullivan]
recording_link:
---

# ViaPharma Reklamace Sync — Email-Agent Demo & Supplier-Data Map Review

**Date**: 2026-10-01
**Attendees**: Jindřich Tůma (STK-003, BigHub PM), Marek Pillár (STK-001, BigHub — Reklamace spec owner), Filip Černý (STK-006, BigHub — Reklamace dev); Petr Sláma (STK-034, ViaPharma CZE), Tereza Foltýnová (STK-013, ViaPharma CZE), Jana Egrmaierová (STK-044, ViaPharma CZE), Kim Sullivan (ViaPharma CZE, present only at the start)
**Type**: external
**Recording**: N/A
**Previous session**: [2026-09-24-viapharma-reklamace-knowledge-base-standoff](2026-09-24-viapharma-reklamace-knowledge-base-standoff.md)
**Meeting prep**: N/A. Internal prep: [2026-09-30-reklamace-thursday-prep-data-map-demo-review](../internal/2026-09-30-reklamace-thursday-prep-data-map-demo-review.md)

## TL;DR

The 09-24 standoff has largely unlocked. Jindřich accepted Petr Sláma's May spec comment (automatic emails, the "Zentiva" sequence) as the way forward. Filip's email-agent proof of concept was well received, and Sláma asked for two additions: a CC to the shared claims mailboxes and the thread archived as a PDF on the claim in Axapta. On the data map, Sláma ruled Excel out ("last choice"), accepted minimal Axapta development, and asked that all supplier detail be entered in one place, a SharePoint List keyed by supplier account. That matches BigHub's recommendation. Formal feedback (column J) is due early next week, and the List still needs a Dr. Max owner. Phase 1 testing gets one more week. Sláma closed with "a big step forward since last week".

## Key Discussion Points

### Opening — the May spec comment

Petr Sláma opened by challenging last week's claim that the build was "per spec". He has comments in the spec from May saying the emails should go out automatically, including the Zentiva case (sending to several addresses in turn), and BigHub never replied to them: "I take it that since you didn't respond, it stands" [translated from Czech]. Jindřich Tůma confirmed the comment exists. It was reportedly handled on BigHub's side at the time (Honza Sovka was involved), but no feedback came back. He called it a shared miss: BigHub should have made sure the comment was worked in, and ViaPharma should have checked. Then he moved on: "let's go the way of your comment". Any budget impact would have been the same at the start as it is now. A separate meeting on the history is possible if Sláma wants one.

Marek Pillár positioned himself as the spec owner from now on. Sláma can bring comments or change requests to him directly, and development "can bend outside the spec" where it makes sense for the initiative. Marek is revising all specs, will address the open comments, and will soon deliver an updated spec as the current source of truth that includes the data sources from the Excel. Sláma: "super, thanks".

### Email-agent proof of concept (Filip Černý)

Filip presented the flow:
- The assistant opens a claim thread and saves a first draft to the supplier.
- The worker approves and sends it. Approval can be dropped if not wanted.
- The agent waits for the reply and classifies it into one of three groups: a final outcome (disposal, send to the supplier's warehouse, or own/carrier pickup), waiting (e.g. "please bear with us, a pickup label is coming"), or cannot decide → hand to a person.
- The first email is deterministic for now, because all 7 real threads he read open with the same request.

Four examples:
- **Disposal**: a credit note is attached and the reply says "dispose of it". The case is filed to disposal.
- **Send back**: "send it to our warehouse at this address".
- **Waiting, then pickup**: the HIP thread. "Please wait" was recognised as non-final, then the label arrived in the same thread with pickup set for 16. 9.
- **Forwarded, then unknown**: the case was forwarded inside the supplier, and a colleague offered to swap the expired stock with their driver bringing the replacement. Flagged for a person.

Filip: "it's very important that the agent always has a way out."

Next ideas, with user feedback first:
- Real Outlook integration, still waiting on the mailbox.
- Different first emails per supplier (e.g. "warehouse A or B?").
- Automatic reminders when a supplier doesn't reply within 2 days.

**Feedback**:
- **Jana Egrmaierová** asked for ViaPharma in CC, ideally the shared addresses (reklamace@praha-viafarma.cz, the Ostrava claims mailbox, or quality). Filip: no problem if the rule is fixed (e.g. always supplier + ViaPharma). Sláma: agree the exact rule first, then add it.
- **Jana Egrmaierová** asked whether the email goes to the main contact from the knowledge base. Filip: yes for now. Where a supplier has several possible recipients and the choice depends on the worker's knowledge, phase 1 could generate two identical drafts with different recipients for the worker to pick. Rule-based automation comes later, once the rules are known.
- **Petr Sláma** asked for the email communication to be attached to the claim in Axapta via the API, the way photos and documents are. Otherwise the history lives only in individual mailboxes. It must be PDF, not MSG, because the terminals have no Outlook. Finance also uses this to check how a credit note was resolved ("Hanka"). Filip: this is in the original spec too, "let's add it".
- **Petr Sláma**: "I like it at first sight… a big step forward" [translated from Czech]. He asked for the deck in the shared Teams channel folder. Jana wants time to think it over.

### Problem types beyond "damaged goods" (Tereza Foltýnová)

Tereza flagged that "damaged goods" may be misleading. Axapta has ~19 "typy problémů" (problem types: non-delivery, expiry, etc.), yet all current testing uses damaged goods only, and she can't see in the spec where receiving claims get split by type. Phase 3 is named "nedodané zboží" (undelivered goods), which is a separate topic. She asked whether the app could get a dropdown. "Don't take it as a blocker."

Sláma restated the agreed phasing:
1. Damaged on receipt first.
2. Then damaged in the warehouse.
3. Then the other types, where a code list (číselník) can be added to the app and the selected type sent to Axapta via the interface.

Jana agreed to finish receiving damage first (warehouse damage is rarer). She had assumed separate apps for receiving and warehouse claims because their process differs (no master label or SP label in the warehouse). Sláma and Filip pointed out the app already has tabs for receiving, warehouse, and receiving-with-reservation, and the UX can still change.

Jindřich: where and when types enter the process, and whether they affect the email flow, needs defining by Marek with Tereza and Sláma. The spec gets "at least a sentence" as an open point, to be scheduled within delivery 1 / 1.1.

Marek's principle: UX-level feedback from testing doesn't belong in the contract-level spec. Handle it operationally by email or in a working session, and confirm only the logical points in the spec. Rewriting the spec for every point is impractical for both sides.

Tereza and Jana will email Marek the problem-type list, possibly pulled from Axapta. Jana mentioned the types are being narrowed (20 vs. 10 doesn't matter now).

### Testing extension and infra blockers

Tereza asked for one more week of testing (phase 1) given everything going on around it. Jindřich: "you just need more time, totally fine", and he will update the harmonogram (timeline).

Jindřich on blockers: the Graph API and the mailbox/mail group are blocked. Max infra is tied up resolving AKS problems, "the biggest escalation there is at Max", so BigHub waits, but it's known.

Shared test phone (Tereza): Dušan confirmed he'll send it, no ETA. Tereza's kiosk request (Fakturace doprav) is also stuck at infra but not urgent while that stream is paused.

### Supplier-data map — the core topic (Marek Pillár)

Marek walked through the Excel:
- **Columns A–D**: original data source → epic → item.
- **Column E**: what the item is, and whether it was agreed or specified.
- **Columns F–I**: where the data can live: Excel, Axapta (green = agreed or recommended), Confluence/SharePoint, SharePoint List.

BigHub's recommendation (as [[ASM-214]]):
- Only the critical minimum goes into Axapta.
- Everything else goes into a SharePoint List, "a fancy table", cloud-based, with reporting possible.
- Excel is not pushed: archaic, open to anyone, not scalable, partly unsafe.
- Some minimal Axapta development will be needed regardless.
- No decision is needed today. The pros/cons summary sits below the table.

Two conditions for the List:
- It must have a **Dr. Max owner**. BigHub can fill and admin it for a while, but it must live on Dr. Max's side.
- Reading it needs Graph API access, another infra request. Filip will handle it with infra, maybe together with the mailbox access.

Marek admitted some items were collected historically and may drift.

**Petr Sláma's position**:
- **Excel**: "last choice" (no change history, no permissions).
- **SharePoint/Confluence**: preferred, for permissions and history.
- **Axapta**: "I have no problem doing some minimal development in Axapta." He initially suggested addresses could go into Axapta with validation, but then argued against splitting. Axapta is not user-friendly for addresses and contacts (separate fields, valid-from timestamps). He does not want half the data in Axapta and half in SharePoint: "then it drifts apart and nobody maintains it."
- **His ideal**: the supplier number (the unique ID already sent on every API) keys a SharePoint record holding the address, contacts, and so on. People maintain everything in SharePoint only, quality staff edit, warehouse staff read.

Filip: "the ideal approach, let's agree on it". The approved API contract "isn't set in stone": address, main contact, and pickup type can all live in the new table. The second group of "yes" items, such as the claim number, stays in Axapta as source of truth. Linking is by one ID (supplier account): one row per supplier.

Jindřich: Axapta-side definition is clear direction for BigHub. Whatever non-Axapta platform is chosen needs an owner who manages access and data quality. "It will be in the minutes." Sláma agreed. Dr. Max must ask infra to create it and name someone responsible, because the data must be maintained "or the emails will be completely wrong". Axapta has an owner today and the new store doesn't, so this must be defined.

### Axapta's future (Marek → Petr Sláma)

Marek asked whether the move away from Axapta blocks anything. Sláma: Axapta today is ERP + WMS together. The **WMS part** will be replaced by a new WMS. The **ERP part** stays for the foreseeable future, at least partly: finance, sales, purchasing, and claims. The supplier code list and claim documents in Axapta will "surely" remain.

### Sláma's review sequencing and Fakturace doprav

Sláma has been "completely out" for 14 days launching the new A-frame and is on leave tomorrow (2026-10-02). He'll review the data-map Excel early next week with notes in a new column J. After that he'll review Filip's Fakturace doprav proposal, which he has been promising for 14 days. Filip and Jindřich agreed. The Excel is the priority because "that was the block we were stuck on".

### Bug reporting channel (Jana Egrmaierová)

Jana asked whether to route app feedback via Tereza or directly to Filip. Her current bug:
- In "příjem s výhradou" (receiving with reservation), after a wrong response on a master-label scan she can't leave the flow to scan another label.
- Scanning a new label keeps the first label's photos.

Filip: a bug on BigHub's side.

Jindřich: keep everything in one place both sides see, which is the shared Excel for now. Jana logs there and pings Filip. Jindřich will push for X-Manager as the ticketing tool, since later phases will need it.

### User login for testing (Filip Černý)

Per-user login for testing ([[ASM-182]]) is being solved together with other projects through the platform ([[ASM-217]]). Filip works on it with a colleague on Monday 2026-10-05, likely ready next week.

## Decisions Made

- **Sláma's May spec comment (automatic emails, Zentiva multi-recipient sequence) is accepted as the direction.** Jindřich: "let's go the way of your comment". Any budget impact is acknowledged, with a separate meeting on the history only if wanted. This resolves the [[ASM-181]] standoff in Sláma's favour on direction.
- **Email-agent design (PoC) carries forward**: the worker approves the first draft, the agent classifies replies (final / waiting / hand to a person), and there is always a human way out.
- **Email-agent additions agreed**:
  1. ViaPharma CC, likely the shared claims mailboxes; the exact rule is to be agreed.
  2. The email thread is attached to the claim in Axapta via API as PDF, not MSG.
  3. Where a supplier has multiple possible recipients, phase 1 generates alternative drafts per recipient for the worker to choose.
- **Problem-type phasing confirmed**: damaged on receipt → damaged in the warehouse → other Axapta problem types (a code list in the app, sent to Axapta via the interface). The spec gets an open point and the timing is set within delivery 1 / 1.1.
- **UX-level testing feedback is handled operationally** (email or a working session), not by rewriting the contract-level spec ([[ASM-186]]).
- **Phase 1 testing is extended by one week** at ViaPharma's request. Jindřich updates the harmonogram.
- **Supplier-data store, direction converging (formal feedback early next week)**: Excel is out. Axapta keeps the supplier register (supplier account) plus the case fields only it holds. Everything else, including address and main contact, goes into one SharePoint List keyed by supplier account. Quality staff edit, warehouse staff read. Data is entered in one place, not split across stores. Minimal Axapta development is acceptable to Sláma.
- **The non-Axapta store needs a named Dr. Max owner.** Dr. Max requests it from infra.
- **The bug-reporting channel is the shared Excel for now** (Jana pings Filip). X-Manager is to follow for later phases.

## Action Items

- [ ] **Marek Pillár**: Send logistics the recap of today's decisions for confirmation, and the Reklamace spec with agreed changes / open questions highlighted — due 2026-10-02 — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Marek Pillár**: Put into the new Reklamace spec: the email-agent flow and additions (CC, PDF archive to Axapta, alternative drafts), the SharePoint List direction, the problem-types open point, and answers to Sláma's open May comments — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Petr Sláma**: Review the data-map Excel and add notes in column J — due early week of 2026-10-05 — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Petr Sláma**: Then review Filip's Fakturace doprav proposal — after the data-map review — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Dr. Max (Petr Sláma / Tereza Foltýnová)**: Name a business owner for the supplier-data SharePoint List and request it from infra — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Tereza Foltýnová / Jana Egrmaierová**: Email Marek the list of Axapta problem types (typy problémů) — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Filip Černý**: Send the email-agent deck and upload it to the shared Teams channel folder — due 2026-10-01 — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Filip Černý**: Raise the Graph API read-access request for the SharePoint List with infra, ideally bundled with the mailbox access — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Filip Černý**: Fix the "příjem s výhradou" master-label bug (can't exit after a wrong response; old photos persist on a new label) — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Filip Černý**: Finish per-user login for testing via the platform with a colleague — starts 2026-10-05, target week of 2026-10-05 — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Jana Egrmaierová**: Log testing bugs in the shared Excel and ping Filip — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Jindřich Tůma**: Update the harmonogram with the one-week phase 1 testing extension — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] **Jindřich Tůma**: Push X-Manager as the ticketing tool for testing feedback in the next phases — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review

**Previous session (09-24) follow-through**:
- Knowledge-base recommendation: **done**, presented today.
- Shared test phone: **in progress**. Dušan will send it, no ETA.
- Per-user login: **in progress** (platform login, next week).
- "Invalid request" photo bug, two-address shipments ([[ASM-183]]), Jana's supplier-flag validation, and Sláma's invite to the Dudaško/Žůrek meeting: **not discussed**.

## Open Questions

- Who on Dr. Max's side owns the supplier-data SharePoint List ([[ASM-215]])?
- Is the address really leaving Axapta? Sláma first offered addresses in Axapta with validation, then argued for everything in SharePoint. His column-J feedback should settle it, together with which approved API-contract fields (address, main contact) are dropped.
- What is the exact CC rule for supplier emails (always the shared claims mailbox? per warehouse?), and is approval of the first draft required or optional?
- How does the PDF thread archive reach Axapta: which API, and when (per message or at closure)?
- Where do Axapta problem types enter the process, and do they change the email flow?
- Does the one-week phase 1 testing extension affect the 2026-10-15–16 full UAT start ([[ASM-056]])?
- Does accepting Sláma's May comment change budget or MD? It was acknowledged in principle, but under [[ASM-186]] any change needs an MD cost and written approval.
- Who is Kim Sullivan (ViaPharma CZE)? Is this the "Kim" referenced earlier as Sláma's manager?

## Sentiment & Tone

Markedly better than 2026-09-24. Sláma opened with a pointed, record-setting remark about the unanswered May comments, but Jindřich defused it fast by owning the miss and accepting the comment as direction, without arguing the history. Marek reinforced this by offering himself as the open channel for change requests. Sláma's tone then turned openly positive: he liked the demo "at first sight", repeatedly called it a big step, agreed with the single-store principle, and closed with "I feel a huge step forward since last week".

Tereza was constructive and careful to frame the problem-type question as "not a blocker". Jana was engaged and practical (CC addresses, the bug-channel question). Two things to watch: Sláma's sensitivity to the spec-as-record point (he will expect his comments answered in writing), and the List owner, which nobody volunteered for. Jindřich's "a block we were stuck on… this straightens it out" framing landed well. The table-first approach worked.

## Routing Log

Routed 2026-10-01.
- **project-assumptions**: Added ASM-223 (May comment accepted), ASM-224 (email-agent additions), ASM-225 (problem-type phasing), ASM-226 (operational UX feedback + bug channel), ASM-227 (phase 1 testing +1 week), ASM-228 (supplier-data single-store direction, Open), ASM-229 (Sláma's review order). ASM-181 → Decided. Update notes on ASM-139, ASM-204, ASM-214, ASM-215, ASM-176, ASM-169, ASM-182, ASM-217, ASM-056, ASM-142.
- **project-knowledge**: Reklamace entry: 10-01 outcome. Axapta entry: ERP vs. WMS split (corrects the "retire Axapta" framing).
- **project-stakeholders**: Updated STK-034 (Neutral → Neutral leaning Champion), STK-013, STK-044 (sentiment set to Neutral, engaged), STK-003, STK-006. Added STK-059 Kim Sullivan (low confidence).
- **client-overview**: Ways of Working: unanswered spec comments are read as accepted.
- **project-daily**: 2 PM-owned action items added; options-Excel walkthrough done; 10-02 recap/spec item partial. Non-PM action items stay in this note only.
- **project-lessons**: LL-76, LL-77.
- **meeting-index**: Entry added.
