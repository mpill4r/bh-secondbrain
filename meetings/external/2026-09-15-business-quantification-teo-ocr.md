---
last_updated: 2026-09-15
type: external
attendees: [Marek Pillár, Radim Švarc]
tldv_link:
---

# Business Quantification Call with Radim Švarc — TEO/OCR

**Date**: 2026-09-15
**Attendees**: Marek Pillár (BigHub, running the interview), Radim Švarc (Dr. Max — TEO technical department)
**Type**: external
**Recording**: N/A (pasted transcript, no timestamps beyond MM:SS speaker tags; transcript excerpt provided ends mid-discussion)
**Previous session**: N/A directly (first live business-quantification interview for TEO/OCR) — related context in [2026-09-03-maxbuddy-chatbot-ocr-project-handoff](../internal/2026-09-03-maxbuddy-chatbot-ocr-project-handoff.md) and [2026-09-07-ai-portfolio-roadmap-scope-review](../internal/2026-09-07-ai-portfolio-roadmap-scope-review.md)
**Meeting prep**: N/A

## TL;DR

Third Business Quantification interview run today, this time for TEO/OCR — Marek's opening assumption that Radim Švarc was the initiative's business owner got corrected mid-call: Radim is the working-level daily contact/domain expert, while Tomáš Burda (head of the technical department) is the actual business owner and needs to sign off. Radim gave a well-grounded Objective and business-value estimate (~250 handwritten service protocols/week, ~40 hours / ~5 MD per month of manual re-keying into ServiceNow) but pushed back on Marek's proposed time-saved KPI, preferring a document-count-based metric instead — that discussion was still in progress when the provided transcript excerpt ends.

## Key Discussion Points

### Business owner correction

Marek opened by asking Radim to confirm he was the business owner; Radim initially agreed ("Můžete si to tam napsat") but immediately qualified it — major directional decisions need sign-off from Tomáš Burda, head of the technical department. Marek reflected this back explicitly ("takže business owner tohoto byl pan Burda a vy budete ten můj daily contact?") and Radim confirmed. Marek asked Radim to loop in Burda today/tomorrow to confirm ownership and expectations, referencing the same pattern used with Tereza Foltýnová on the logistics side earlier today.

**This plausibly resolves an existing stakeholder record**: STK-025 (Tomáš Burda) is currently tracked only as owner of an initiative called "TD revisions" — sourced from the BigHub roadmap sheet with no further detail. "TD revisions" (Technical Department revisions) is a strong match for TEO/OCR itself (TEO = Dr. Max's technical department; the documents being processed are service/revision protocols). Flagged for PM confirmation rather than auto-merged.

### Objective (JTBD)

Radim shared a prepared presentation and walked through the origin story: a colleague in the technical department processes ~250 service protocols per week, each requiring her to read handwritten data (pen, pencil — whatever the technician used) and manually retype it twice — once off the paper, then again into ServiceNow. No OCR layer works today because the source notes are handwritten, ruling out classic OCR; this is what led Dr. Max to approach BigHub for an AI-based extraction approach instead. The core driver, in Radim's words, is that the work is simply extremely time-consuming.

### Business value (Fermi estimate)

- **~40 hours/month (~5 MD/month)** of manual data-entry time — Radim pulled this live from a note he'd previously sent to Lukáš Síč, based on a historical review of protocols stored on a network drive over roughly the past month/year, so he characterized it as a reasonably precise (not purely guessed) figure.
- **Seasonality**: volume is higher in autumn (door/climate-control service season) and lower over summer, but averages out to ~250/week annually.
- **Rate/cost**: Radim didn't have a per-MD cost figure available and deferred it to Tomáš Burda. Marek referenced the ~3 000 Kč/day figure used as an example in the logistics quantification (earlier today) as an illustrative placeholder, to be confirmed with Burda rather than treated as accurate for TEO.
- **FTE framing**: Radim noted a dedicated assistant currently spends most of her time specifically on this ServiceNow data-entry agenda, suggesting a potential ~0.5 FTE saving is plausible, though not firmly committed.

### Technical/integration status

BigHub is exposing an API service: Dr. Max will send batches of documents via API, BigHub's pipeline processes and extracts the data, and Dr. Max pulls the results back via API for review/correction and import into ServiceNow (the review/correction/import step stays on Dr. Max's side, owned by Radim). Radim received the API service specification the day before this call and is beginning to explore and test it.

### KPI — unresolved, discussion in progress when the transcript ends

Marek proposed an example KPI to anchor the conversation (explicitly framed as just a starting suggestion, not a decision): saving ~80 hours within 3 months of deployment (≈ half an FTE). Radim pushed back constructively — he wasn't convinced a time/FTE-saved framing would capture the initiative's real impact on paper vs. in practice, and proposed instead focusing on a **document-count metric**: the number/share of imported documents that were read correctly and needed no manual correction before import into ServiceNow — freeing time for other work rather than measuring the time saving directly. He was still thinking through how to define this precisely when the provided transcript excerpt cuts off.

## Decisions Made

- Business ownership reassigned in discussion: Tomáš Burda is the business owner for TEO/OCR (pending his own confirmation); Radim Švarc is the domain expert / daily working contact.
- The example "~80 hours / half-FTE in 3 months" KPI proposed by Marek was **not adopted** — Radim pushed back and the conversation moved toward a document-count-based metric instead, without landing on a final definition in this excerpt.

## Action Items

- [ ] **Radim Švarc**: Loop in Tomáš Burda today/tomorrow to confirm business ownership and expectations for TEO/OCR — from 2026-09-15-business-quantification-teo-ocr
- [ ] **Marek Pillár**: Send the draft quantification Excel to Radim Švarc for review/completion once filled — from 2026-09-15-business-quantification-teo-ocr
- [ ] **Radim Švarc**: Send Marek the presentation with the ~40 hours/month (~5 MD) time estimate, once updated — from 2026-09-15-business-quantification-teo-ocr
- [ ] **Tomáš Burda** (via Radim Švarc): Provide a per-MD/per-hour cost rate for the technical department, to replace the illustrative logistics-derived placeholder — from 2026-09-15-business-quantification-teo-ocr
- [ ] **Radim Švarc / Marek Pillár**: Finalize the KPI definition — resolve between a time/FTE-saved framing and Radim's proposed document-count/correction-rate framing — from 2026-09-15-business-quantification-teo-ocr
- [ ] **Marek Pillár / Radim Švarc**: Continue/complete this Business Quantification interview — the provided transcript excerpt ends before Business Value/KPI fields were finalized — from 2026-09-15-business-quantification-teo-ocr

## Open Questions

- Is Tomáš Burda's "TD revisions" roadmap entry (STK-025) the same initiative as TEO/OCR? Strongly suggested by today's call and the name itself, not yet explicitly confirmed.
- What per-MD/hourly cost rate should be used for the technical department's business-value calculation?
- Final KPI definition — time/FTE saved vs. a document-count/correction-rate metric — was not resolved in this excerpt.
- The transcript provided ends mid-sentence; it's unclear whether the live call continued beyond this point and, if so, what was discussed/decided afterward.

## Sentiment & Tone

Collaborative and thoughtful, similar in register to today's earlier logistics quantification calls. Radim came prepared (had a presentation ready, pulled a real historical estimate rather than guessing) and, notably, pushed back on Marek's proposed KPI rather than accepting it passively — a good sign of genuine engagement with getting the metric right rather than just filling in a form. No friction; the only rough patch was early audio/mic issues at the start of the call, quickly resolved.

## Routing Log

- **project-stakeholders**: Enriched STK-041 (Radim Švarc — domain expert confirmation, business-value data, KPI pushback) and STK-025 (Tomáš Burda — flagged as likely business owner, matched to his existing "TD revisions" entry). Added STK-047 ("Wágner," BDC, low-confidence) from the related technical presentation.
- **project-knowledge**: Enriched the "TEO / OCR" entry with ownership structure, business-value/volume figures, the proposed automated architecture and tech stack, and the open KPI framing question.
- **project-daily**: 7 action items added to 2026-09-15's daily, including a highest-prio item for Dr. Max's direct feasibility/timeline ask.
- **Related document**: `documents/client/2026-09-15-teo-ocr-technical-process-presentation.md` (Radim Švarc's supporting presentation, ingested and routed alongside this meeting).
