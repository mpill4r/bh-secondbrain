---
last_updated: 2026-09-29
type: internal
attendees: [Marek Pillár, Filip Černý]
recording_link:
---

# Reklamace — Email-Agent Demo Walkthrough & Data-Map Feedback with Filip Černý

**Date**: 2026-09-29
**Attendees**: Marek Pillár (AI Analyst / PM, BigHub), Filip Černý (Developer, Reklamace dev owner, BigHub)
**Type**: internal
**Recording**: N/A (transcript, ~27 min, Czech/Slovak)
**Previous session**: [2026-09-25 Reklamace supplier-data source options](2026-09-25-reklamace-supplier-data-source-options.md), where the ~1 MD email-agent demo was approved ([[ASM-173]]). Related: [2026-09-29 management-meeting debrief](2026-09-29-management-meeting-debrief-reklamace-thursday-plan.md), which fixed the 2026-10-01 agenda.
**Meeting prep**: N/A

## TL;DR

Filip walked Marek through the Reklamace email-agent demo. It is largely implemented (CLI only, not wired to Outlook) and built from 7 real supplier email threads Jana Egrmaierová sent him (6 usable). The first email is deterministic, triggered with the rozvozový list. A prompt-based LLM classifier (no fine-tuning) sorts supplier replies into a few known outcomes, "waiting" replies are parked, and anything unknown goes to a person. Both agreed this is a sound MVP ("Pareto") and that edge cases need more real threads from logistics. For 2026-10-01, Filip will present a simple slide deck / one-pager (user journey plus 2–3 real examples with the classification output) instead of a live demo or a draw.io diagram. The data-map Excel gets a final three-way review with Jindřich on 2026-09-30 afternoon.

**Continuity with 2026-09-25**: the demo decided there is now built (on schedule for Thursday, per the debrief). The "draft appears inside the thread" question is still open, since the demo isn't integrated with Outlook. Graph API access is still blocked on infra.

## Key Discussion Points

### Data-map Excel ("marek sheet") — Filip's review

Filip reviewed the data-source map and left comments. His view: mostly small things. Some rows repeat "one topic from several angles" and could be merged. One row reads more like a feature BigHub has to build from the inputs than a question of where data comes from. Overall "it surfaces the problems we're solving nicely" [translated from Czech].

Marek hasn't read the comments yet. He wants the Excel to be the approved basis for the final spec, so he'll work the comments in tonight or early tomorrow. The final walkthrough is **2026-09-30 afternoon (~15:00–16:00)** with Jindřich, so Filip can justify the content and prepare for Thursday. Marek will present the structure; Filip presents the demo. Marek will remove all the source references ("those are mine from Claude"). The meeting is online: Filip won't come to the office. Marek will be there after lunch with Alana, purely for the relationship.

### Email agent — how the demo works

- **Trigger**: AX sends the API request that generates the rozvozový list. The same trigger generates the **first email** to the supplier (the address is known).
- **First email is always the same.** In the threads Filip got, it's short, e.g. "Dobrý den, posílám notifikaci o reklamačním případu č. 123, dokumentace v příloze" ("sending notification of claim case no. 123, documentation attached"). The staff "write very briefly, everyone has the context — no need to generate epics" [translated from Czech].
- **Supplier-specific first-email variant** (e.g. "ship to warehouse A or B?", "send back or dispose?") is **out of scope for the demo**. It applies to a small share of suppliers ("well under 10 %, maybe under 5 %"), all of them known in advance from the supplier note. Later the LLM can parse the note and add the question to the first email. Marek: none of the 6 threads had it, so it isn't solved at this stage.
- **Urgency / reminder** (not built, out of demo scope, worth presenting): one thread shows the supplier not replying and staff sending "nezapomněli jste na nás?" ("did you forget about us?"). Tracking time without a reply and sending a reminder is simple.
- **Reply classifier (implemented)**: a prompt-based LLM classifier turns the supplier reply into a structured outcome:
  1. **Send to warehouse**: the supplier confirms and may give an address. Filip proposes comparing that address with the stored one (it matched in the one thread where it came up).
  2. **Own pickup (vlastní svoz)**: the goods go to a separate pile until the supplier's own transport collects them, often alongside a delivery.
  3. **Disposal**: a terminal state (2 of 7 threads). The worker just takes the goods to disposal.

  For each outcome, the worker knows exactly what to do next: print the rozvozový list and stick it on the goods, set aside for pickup, or dispose.
- **"Waiting" email** (covered, ~2 threads): the supplier replies at once with "we know, please wait for our statement". The classifier recognises it, waits, and classifies the next email in the thread.
- **Wrong recipient / forward** (covered, 1 thread): the supplier forwards it internally ("Jani, tohle je asi na tebe", "Jani, this one's probably yours"). The agent recognises it doesn't need to act and keeps waiting.
- **Hand-off to a person** (2 threads):
  - a supplier asking whether a replacement with a new expiry is acceptable if their courier takes the expired goods (needs a real business judgment);
  - a long, complex rejection ("no form").

  These go to the claims worker. In future, a tool with access to the right data could let the agent answer the first kind itself.

**Why a prompt, not training** (Marek asked about data volume): the outcomes are explicit in the emails ("please dispose", "send to warehouse 123", "our courier will collect"), so a prompt plus a few examples in context is enough. Fine-tuning is "completely out of scope and pointless". With ~30 labelled threads the prompt can be tuned to high accuracy. Filip expects close to 100 % on these categories.

**Human in the loop**: everything is still a **draft**. There's no auto-send, and no Outlook integration yet (waiting on client infra). The goal is to shrink the hand-off share by identifying more typical situations. Marek: "if you take the very meaning of MVP, what you described is exactly it — they have nothing today, you cover a very large share, and there's a fallback" [translated from Slovak]. But BigHub needs the edge cases from logistics; without them it can't extend the flow. Filip: the structure is "infinitely extensible", but "we have to know the paths".

### How to present on 2026-10-01

Marek doubts a draw.io flow diagram works for the meeting. Options discussed:
- **Slides**: Marek could build them, or send Filip this transcript to generate a BigHub-branded deck with Claude, using screenshots of the real emails and their outputs.
- **Live demo**: Filip's idea was three folders (real supplier emails → inbox with a watcher → drafts), but drafting replies doesn't quite fit. Marek: it works if framed as "imagine this is sent; for testing it sits in drafts".
- **Where they landed**: a simple deck or one-pager. A high-level user journey (email arrives → AI splits it into outcomes → result for each), 2–3 concrete examples on the client's own data, and next steps: "which other frequent cases can we catch", framed as Pareto. Filip can honestly say "this easy case is done" without a live demo. Filip will think it over; they'll finalise the form tomorrow morning (async or a short call).

Filip's value argument: even a deterministic first email saves real time. Today every worker opens the case, retypes numbers and phrases it slightly differently each time.

### Business context

Marek shared the BQ framing: Petr Spilka defined the saving as 4 employees × 2 h/day (≈ 1 MD per day) → roughly 400k Kč a year, "not a very sexy project for Dr. Max". Filip thinks 2 h/day per person is "mega realistic" for the easy cases.

### Logistics

- Petr Neuman (Listing) meeting is tomorrow **2026-09-30 at 11:00** (Filip thought it was the afternoon).
- Filip will send Marek the example email threads.

## Decisions Made

- **Email-agent MVP shape**: a deterministic first email on the rozvozový-list trigger. A prompt-based LLM classifier (few-shot, no fine-tuning) sorts replies into: send to warehouse (with an address check), own pickup, disposal, waiting (park and re-classify), wrong recipient (wait), and hand-off to a person for anything unknown. Everything is a draft; no auto-send.
- **Out of demo scope**: the supplier-specific first-email question (warehouse A/B, dispose?) and urgency reminders. Both are presented as simple next steps.
- **Thursday format**: a simple deck or one-pager with real examples instead of a diagram or complex live demo (final form agreed 2026-09-30 morning).
- **Data-map Excel**: Marek works in Filip's comments, removes the source references, and holds a final three-way review with Jindřich on 2026-09-30 afternoon.

## Action Items

- [ ] **Marek Pillár**: Work Filip's comments into the data-map Excel ("marek sheet"): merge overlapping rows, reconsider the feature-like row, remove source references — due 2026-09-30 morning — from 2026-09-29-reklamace-email-agent-demo-review-filip
- [ ] **Marek Pillár**: Schedule the data-map / demo walkthrough with Jindřich Tůma and Filip Černý — due 2026-09-30 afternoon (~15:00–16:00) — from 2026-09-29-reklamace-email-agent-demo-review-filip
- [ ] **Marek Pillár**: Check whether logistics specified expectations for the first email / time saving (Marek recalled discussing it) — from 2026-09-29-reklamace-email-agent-demo-review-filip
- [ ] **Filip Černý**: Prepare the Thursday demo material (deck or one-pager: user journey, 2–3 real examples with classification, next steps); agree the form with Marek — due 2026-09-30 morning — from 2026-09-29-reklamace-email-agent-demo-review-filip
- [ ] **Filip Černý**: Send Marek the example supplier email threads — from 2026-09-29-reklamace-email-agent-demo-review-filip

## Open Questions

- Can logistics provide more real email threads (target ~30, including edge cases) to extend the classifier categories and cut the hand-off share?
- How does the agent decide business questions such as "is a replacement with a new expiry acceptable?" Is there a data source or rule it could check?
- Should urgency reminders and the supplier-specific first-email question go into Phase 1.1 scope or a later increment?
- Which data-map row does Filip consider a solution feature rather than a data source, and which rows overlap? (Answered in his Excel comments, not yet read.)

## Sentiment & Tone

Relaxed, collaborative and constructive. Filip was open that the demo took about one afternoon and actively asked for a second opinion. Marek was clearly positive ("za mňa úplne super", "totally great from my side") and framed the result as a textbook MVP. Both were pragmatic about scope, agreeing to defer edge cases and to present simply rather than impressively. No tension.

## Routing Log

Confirmed by PM on 2026-09-29 (confirm all).

- **project-assumptions**: ASM-204 (Decided), ASM-205 (Open), ASM-206 (Decided); update note on ASM-173
- **project-knowledge**: Reklamace entry, real supplier email-thread findings
- **project-stakeholders**: STK-006, STK-044
- **project-daily**: 2 action items (PM-owned); existing Marek/Filip/Jindřich sync item annotated with the agreed slot. Filip's items stay in this note only.
- **Spec**: `3. Reklamace v3.docx` Phase 1.1b gets the classifier outcomes (separate edit)
