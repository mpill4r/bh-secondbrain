---
last_updated: 2026-10-02
type: internal
attendees: [Marek Pillár, Jan Sovka]
recording_link:
---

# 1:1 with Jan Sovka — Account Update, Monday Reklamace Meeting & Okamžité Avízo

**Date**: 2026-10-02 (Friday)
**Attendees**: Marek Pillár (STK-001), Jan Sovka (STK-002, account owner, Marek's line manager)
**Type**: internal
**Recording**: N/A (transcript, ~35 min, Czech/Slovak; personal topics excluded per PM)
**Previous session**: N/A. The weekly 1:1 isn't processed as a series; the last processed meeting with Jan was [2026-09-08](2026-09-08-ai-platform-strategy-history-with-jan-sovka.md)
**Meeting prep**: N/A

## TL;DR

Jan was away for two weeks. He read the account running fine without him as a sign it's in good hands, and he will cut his involvement in logistics to near zero. He won't join Monday's 10:00 Reklamace "next steps" meeting (Žůrek, Dudaško, Spilka, Tereza, Marek). Marek and Jindřich can use it to mark a clean break from the earlier Honza/Alana phase. Jan gave a read on the Monday attendees, sent the March 2026 email with logistics' original initiative list, and explained **okamžité avízo**: some suppliers want notice of a příjem s výhradou within ~24 h, before the item-level claim exists. Both agreed it does not block testing.

## Key Discussion Points

### Account status (Marek)

Marek: "a very, very successful week" [translated from Slovak]:
- **Logistics**: the 10-01 meeting was the first good one in a long time, after the previous week's "shitstorm". Relations with Tereza, Sláma and Egrmaierová have recovered.
- **Dudaško**: praised the initiatives table and is keen on the platform work.
- **Order prediction**: Šimoník praised BigHub at a large management meeting (Jindřich was there).
- **Listing**: Marek met Neuman in person on Wednesday. Magento won't allow import/export for at least ~6 months and is to be retired in ~9 months, so the MVP was reshaped ([[ASM-207]]). They meet again in person on Monday.
- **Logistics initiatives**: new topics such as cenařky (pricing clerks) are being opened. See [2026-10-02 green-field meeting](../external/2026-10-02-logistics-initiatives-green-field-cenarky-analysis.md).

**Capacity**: Marek flagged the load. He isn't sure how long he can stay full-time on this one account, and he also covers TEO/OCR with Alana. It's sustainable for now, but not light. He has spent 2–3 days on the Reklamace spec with Filip.

Jan: this confirms his theory that having Marek and Jindřich dedicated full-time to the client pays off. He noted the handover from the earlier team was hard because documentation was in mixed states.

### Working with Jindřich (Marek)

Last Friday Marek and Jindřich talked through their different working styles. One point was that BigHub is remote-first, so mandatory meetings called at an hour's notice, and objecting when someone can't make them, don't fit. Marek saw a shift in Jindřich's communication afterwards.

The role split as Marek sees it:
- **Jindřich**: manages the people and politics on the Dr. Max side.
- **Marek**: delivery, and in meetings stating openly that BigHub has limited capacity and prioritises across ~50 initiatives, so "something you like" isn't automatically built.

The data-map Excel was co-created rather than directed, and it landed well with Sláma. Jan offered to step in if expectations are ever off and asked for constructive feedback at any time. Marek said nothing is needed.

### Jan stepping back; Monday 10:00 Reklamace meeting

- Jan will reduce his logistics involvement "ad absurdum" (to agree with Jindřich). He wasn't at the last two weeks of logistics calls anyway.
- **Monday 2026-10-05, 10:00, in person**: "reklamační proces — další kroky", organised by Tereza Foltýnová, with Rudolf Žůrek, Tomáš Dudaško, Petr Spilka and Marek. Jan won't attend. He is onboarding new BigHub colleague Lukáš on Monday, and he leaves relationships to Ján Kabát. He also thinks his absence helps: Marek and Jindřich can say "that was the introductory phase with Honza and Alana; now we're here full-time" without speaking about the predecessor in front of him.
- **Marek's read of the meeting's purpose (unconfirmed)**: Tereza fears Reklamace will end, because it has little financial upside. The initiatives Excel puts Reklamace at ~700k vs. tens of millions for MaxBuddy/Listing. That's why Dudaško, Žůrek and Spilka are attending. Spilka said this morning that Reklamace's ~8 h/day saving is small next to cenařky's "hundreds of hours".

### Stakeholder read for Monday (Jan)

- **Rudolf Žůrek**: the most senior person there, responsible for logistics, and the one "calling the shots". Very direct with everyone ("this is rubbish" is possible), but fair, down to earth and open to arguments. Don't take bluntness personally.
- **Petr Spilka**: head of ViaPharma logistics, Žůrek's direct report. Good one-to-one. In front of Žůrek and Dudaško he may posture as the decisive one, but has less real power than he projects.
- **Marek's own read**: Dudaško is 50/50, with some very good meetings and a few poor ones. Marek doesn't know Žůrek. Tereza is stressed and Marek keeps calming her. Egrmaierová is very pleasant. Marek and Jindřich will prepare for Monday.

### Original logistics initiative list (March 2026)

Jan asked whether Marek ever got logistics' original email (March 2026) listing possible logistics use cases, plus Jan's management summary per project. Marek hadn't. Jan forwarded it during the call as context for Monday. Marek: items like "výstupní kontrola" (outbound check) match the initiatives Excel ("probably just copied over").

Marek reported this morning's tracker reset: the old rows don't mean much even to logistics, so they rebuild from scratch and co-create with BigHub. The next sync with Tereza is Wednesday.

### Reklamace spec process (Marek)

The process:
1. Sláma reviews the data-map Excel.
2. Logistics names a business owner for the supplier data and decides what goes into Axapta. BigHub pitched the necessary minimum in AX and offered Confluence / SharePoint for the rest.
3. Marek folds the result into the spec.
4. The spec goes to Sláma for final approval.

Marek keeps stressing that the spec is the contract and changes are fine if confirmed in writing, which is why he now sends many confirmation emails. Jindřich today floated running it through "their [Dr. Max] manager" tool instead. The transcript is unclear: likely X-Manager, unconfirmed. Marek is indifferent.

### Okamžité avízo: origin and phase (Jan)

Jan's explanation:
- **Příjem s výhradou** (receiving with reservation) is a warehouse term: when a truck arrives and a pallet is visibly damaged, the receiver photographs it and notes it in the driver's protocol before unpacking.
- The item-level claim for the actual damaged goods may come only ~2 days later.
- Some suppliers require notice of such a receipt within ~24 h of hand-over. That was meant to be captured per supplier in the knowledge base, but the Excel wasn't fully analysed then.
- The idea: an **optional per-supplier switch**. A nightly job (e.g. at midnight) collects everything photographed as příjem s výhradou that day and sends an **automatic email** to those suppliers: "received with reservation today; expect a detailed analysis within 1–3 working days".
- Purpose: notify the supplier as early as possible, within their contractual terms.
- Jan called the "bolitelné" part a shot in the dark at the time, since the supplier analysis wasn't finished.

**Phase**: Marek's view, with Filip's recommendation: likely few suppliers want it, so build it if logistics wants it, but it must not block the upcoming testing. Jan agreed ("I don't think it blocks… super, full stop" [translated from Czech]).

### Cadence

The weekly 1:1 stays on Wednesday. Jan will start a BigHub team meeting once Lukáš is onboarded.

## Decisions Made

- Jan Sovka won't attend Monday's 10:00 Reklamace meeting. Marek and Jindřich represent BigHub and can frame it as the start of the full-time phase.
- Jan reduces his involvement in logistics to near zero (to align with Jindřich).
- Okamžité avízo: intended as an optional per-supplier flag that sends an **automatic** nightly notice after příjem s výhradou. It does **not block** Phase 1 testing. Exact phase to be confirmed with logistics.

## Action Items

- [ ] **Marek Pillár**: Read Jan's forwarded March 2026 logistics email (original use-case list + Jan's summary) before Monday's meeting — due 2026-10-05 — from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo
- [ ] **Marek Pillár / Jindřich Tůma**: Prepare for the Monday 10:00 in-person Reklamace "next steps" meeting (Žůrek, Dudaško, Spilka, Tereza): expected value/continuation question, stakeholder read above — due 2026-10-05 — from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo
- [ ] **Marek Pillár**: Update the okamžité-avízo section of the Reklamace spec with Jan's context (purpose, ~24 h supplier requirement, nightly automatic email, optional per supplier; doesn't block testing) and ask logistics which suppliers need it and in which phase — from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo
- [ ] **Jan Sovka**: Agree his reduced logistics role with Jindřich — from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo

## Open Questions

- What does Monday's meeting actually aim at: continue/stop Reklamace, re-scoping, or the wider logistics portfolio? Marek's theory isn't confirmed.
- Which "manager" tool did Jindřich mean for the supplier data (X-Manager?), and does it compete with the SharePoint List direction ([[ASM-228]])?
- Okamžité avízo: which suppliers require it, with what deadline (~24 h?), and is the automatic send an accepted exception to the "no automatic emails" rule in the spec?
- How long can Marek stay full-time on this account given the parallel TEO/OCR load?

## Sentiment & Tone

Warm, relaxed and supportive. Jan was openly pleased the account ran well without him. He offered help without pushing, and he deliberately stepped back to give Marek and Jindřich room to own the client. Marek was confident and upbeat after a strong week, while candid about capacity and the Jindřich working-style reset. No tension.

## Routing Log

Routed 2026-10-02 (PM: confirm).
- **project-assumptions**: Added ASM-240 (okamžité avízo), ASM-241 (Jan steps back), ASM-242 (Monday meeting purpose, Open), ASM-243 (Jindřich's "manager" tool idea, Open).
- **project-stakeholders**: Updated STK-024 (influence → High), STK-014, STK-002, STK-003, STK-010. Added STK-060 Lukáš (new BigHub colleague, low confidence). Also moved STK-059 Kim Sullivan from Internal to External (misplaced on 2026-10-01).
- **project-knowledge**: Reklamace entry: okamžité avízo explained. Logistics initiatives: the March 2026 original email.
- **client-overview**: Ways of Working: logistics decision-making (Žůrek vs. Spilka).
- **project-daily**: 3 PM-owned action items.
- **project-lessons**: LL-80.
- **meeting-index**: Entry added.
- Conflict 1 (automatic send vs. the "no automatic emails" rule): left open for logistics, in the spec. Conflict 2 (Magento retirement): already in knowledge (move to global PIM ~9 months out); no change.
