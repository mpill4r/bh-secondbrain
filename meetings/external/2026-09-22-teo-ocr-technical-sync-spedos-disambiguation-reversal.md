---
last_updated: 2026-09-23
type: external
attendees: [Alana Sihelská, Jura Brázdil, Radim Švarc, Michaela Albrechtová]
recording_link:
---

# TEO/OCR Technical Sync — SPEDOS Onboarding, Disambiguation Reversal & Storage Blocker

**Date**: 2026-09-22
**Attendees**: Alana Sihelská (BigHub), Jura Brázdil (BigHub — TEO/OCR developer, STK-026), Radim Švarc (Dr. Max — TEO/OCR contact, STK-041), Michaela "Míša" Albrechtová (Dr. Max — TEO/OCR contact, STK-042)
**Type**: external
**Recording**: N/A — processed from Alana Sihelská's condensed bullet-point notes, not a full transcript
**Previous session**: [2026-09-16-teo-ocr-technical-sync-pilot-results](2026-09-16-teo-ocr-technical-sync-pilot-results.md)
**Meeting prep**: N/A

## TL;DR

This is the recurring TEO/OCR technical sync (following up on the 2026-09-16 blind-pilot session). The "PEDOS" name from that earlier meeting is resolved — it's **SPEDOS**, a real vendor now being actively onboarded. Two significant reversals surfaced against very recent decisions: the ranked-candidate-list disambiguation approach decided in [[ASM-119]] appears to have been rejected in favor of simple manual-review flagging, and the Blob storage/deployment blocker is now described as still depending on Dr. Max infra/BDC, contradicting [[ASM-088]]'s "no BDC dependency" resolution — both need reconciliation with Jura before treating either as settled. Concrete forward progress: Míša sent real Thermetal autumn-2026 protocols for BigHub's first offline batch run, and Radim has already built a live, concrete intake pipeline on Dr. Max's side — a real mailbox (`automat.revize@drmax.cz`), a defined folder structure, a twice-weekly Power Automate push to BigHub's Blob storage, and a daily local script watching for BigHub's processed output, feeding a manual-review-then-SNOW-import flow. BigHub committed to a max-3-day processing turnaround.

**Note on source**: this note combines two sets of notes from the same meeting — Alana Sihelská's condensed bullet points (BigHub side) and Radim Švarc's own, more technical process notes (client side, image-captured, dated 2026-09-22 14:21). Neither is a full transcript, so there are no direct quotes or fine-grained speaker attribution beyond what each set of notes makes explicit.

## Key Discussion Points

### Address-matching gaps in the vendor directory (číselník)

Some branches referenced in protocols aren't found in the číselník (the branch/pharmacy directory BigHub was sent) — the concrete example raised was "Bezručova" in Mělník. This raises the open question of whether the fix is TEO updating the číselník on their side, or BigHub connecting to a live API with the pharmacy list instead of a static sheet. TEO will check the Bezručova entry specifically. Separately, address-extraction quality was reported as improved for the two existing pilot vendors (Racun, Thermetal) as well, not just new ones.

A related recurring gap: some protocols only list a city, not a full address, and where that city has multiple pharmacies (the example given: 5 in one city), the branch genuinely can't be reliably determined from the document alone. TEO's fix is process-side, not technical: they'll push vendors to fill in the complete address, and will return incomplete protocols to vendors for completion rather than have BigHub guess.

### SPEDOS confirmed as a real onboarding vendor

The 2026-09-16 sync flagged an uncertain vendor name — transcribed as "PEDOS" — as a possible 3rd autumn-2026 pilot vendor, with an open question on whether it was even a real name (see that meeting's Open Questions). This session confirms it: **SPEDOS** is real, and BigHub is giving it additional attention, committing to send an export by the end of this week. This resolves that open question and effectively updates [[ASM-089]] (whether to expand autumn scope to a 3rd vendor) from "under consideration" to "in progress."

### Extraction-method and disambiguation-UX decisions — one reverses ASM-119

Two scope decisions on how the pipeline should handle uncertain reads:
- **Reading values from a stamp/seal ("razítko") was rejected** as an extraction method.
- **Sending multiple possible candidate variants (cities and dates) to reviewers was rejected** — a simple flag for manual review in cases of uncertainty is considered sufficient instead.

The second point is a direct reversal of [[ASM-119]] (decided just 2026-09-21: "TEO/OCR disambiguation shifts to classify-against-known-branch-list + ranked candidate alternatives, not forced verbatim transcription"). It's not clear from Alana's notes whether this rejection is about the same mechanism ASM-119 describes, or a narrower point (e.g. how candidates are *presented* to reviewers vs. the underlying classification logic) — **flagged as a conflict for the PM/Jura to reconcile**, see Open Questions.

### Output format: Excel, not a web interface

The production output will be an **Excel file**, not a web interface with curated "columns of interest" for Michaela Albrechtová as previously discussed. Import into ServiceNow will happen either manually or automatically — the automatic path is not yet decided ("TBS" in Alana's notes, read as "to be specified/decided").

**PM concern (flagged 2026-09-23, not yet raised with Jura/Radim)**: Marek considers this Excel-centric design a real gap, not just a format preference — Radim's process notes (see below) confirm the entire human-review/correction step is 100% manual spreadsheet work with no AI assistance in that part of the loop, even though BigHub's own extraction is AI-driven upstream. Worth investigating whether a lighter AI-assisted review layer could replace or augment the raw-Excel handoff.

### Correction feedback loop — operationalizing ASM-120

Radim's team will send the "correct" excel/json back to BigHub, so BigHub can evaluate extraction accuracy and identify improvements over time — the exact format is to be agreed directly with Jura. This is the concrete implementation of [[ASM-120]] (decided 2026-09-21: reviewer corrections must flow back via API) — worth confirming whether "excel/json" sent back and forth satisfies that decision's intent, or whether a stricter API contract is still expected.

### Blob storage & deployment blocker — contradicts ASM-088

Alana's notes state blob storage and deployment "still stands on Dr. Max infra, resp. BDC" — i.e., still blocked pending Dr. Max-side infrastructure/BDC action. This directly contradicts [[ASM-088]] (decided 2026-09-16: Blob storage for the TEST environment would be self-provisioned by BigHub, with no BDC/infra-team dependency to create it). **Flagged as a conflict** — either the blocker has genuinely shifted since 2026-09-16 (e.g. a different piece of infra than what ASM-088 covered), or this is a note-taking imprecision. Needs a direct check with Jura before updating ASM-088's status either way.

Concretely, in parallel: Míša sent real Thermetal protocols from the autumn 2026 service season, and BigHub will run its first batch offline (including JSON output) against them — this doesn't depend on the blob storage/deployment blocker being resolved first.

### Data intake mechanics — Radim's concrete process design

Alana's notes captured this at a high level (mailbox + folder request, Power Automate syncing to blob storage, no BigHub preference on interval). Radim Švarc's own process notes from the same meeting (client-side, dated 2026-09-22 14:21) give the actual concrete design he's building on Dr. Max's side:

1. **Intake**: a new mailbox, `automat.revize@drmax.cz`, is live. Documents either arrive there or are manually saved to a folder (`914 Technicke/revize/automat/nové`). A Power Automate ("PA") online flow reads PDF/PNG attachments from the mailbox.
2. **Send to BigHub**: **twice a week**, Radim's Power Automate flow pushes the collected documents to BigHub's Blob storage. He explicitly flagged an open question back to BigHub: what's the batch-creation logic on BigHub's side?
3. **Watching for BigHub's output**: a **daily Power Automate Desktop Python script** on Radim's machine checks whether the number of processed batches has changed, tracked against a local CSV of already-processed batches. When a new batch appears, he builds a new Excel from it (named `{batchID}_processed_at.xlsx`) and (with a self-noted open question) may notify Míša that a new Excel is ready. Related PDFs get renamed with the batch ID prefix and moved into a `čeká` (waiting) folder.
4. **Manual review**: Míša manually checks and corrects rows in the Excel — same structure as what Jura sent as a template, with a clickable link per row that opens the source PDF at the exact page. Once she's done, the file moves to a `hotovo` (done) folder.
5. **SNOW-import prep**: a file move into `hotovo` triggers another Power Automate flow that trims the Excel down to the columns SNOW needs and creates an import-ready copy; the original PDFs then move to an archive folder.
6. **SNOW import itself**: manual, via the SNOW form, for now — Radim noted automatic import is a real possibility, not yet built.

This resolves the "TBS" ambiguity from Alana's notes more precisely than assumed: SNOW import is manual today by design choice, not an undecided blocker — automating it is a live option Radim is already flagging, not a stalled decision.

## Decisions Made

- SPEDOS confirmed as a real, actively-onboarded pilot vendor — BigHub to send an export by end of this week.
- Reading values from a stamp/seal is out of scope as an extraction method.
- Sending multiple disambiguation candidates to reviewers is rejected — a manual-review flag is sufficient (reverses the mechanism described in [[ASM-119]] — pending reconciliation).
- Production output is an Excel file, not a web interface with curated columns; SNOW import method (manual vs. automatic) still undecided.
- TEO will push vendors toward complete addresses and return incomplete protocols for completion rather than have BigHub guess the branch.
- BigHub commits to a max-3-day processing turnaround from submission.

## Action Items

- [ ] **Radim Švarc / Michaela Albrechtová**: Verify the "Bezručova" (Mělník) branch entry missing from the číselník — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] **Radim Švarc / Michaela Albrechtová**: Push vendors to fill in complete addresses on protocols; return incomplete ones for completion rather than have BigHub guess the branch — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] **Jura Brázdil**: Give SPEDOS additional pipeline attention and send an export by end of this week (2026-09-25) — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] **Jura Brázdil**: Run the first offline batch (incl. JSON output) against the real Thermetal autumn-2026 protocols Míša sent — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] **Jura Brázdil**: Answer Radim's open question on BigHub's batch-creation logic for documents arriving via his twice-weekly Blob storage push — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] **Marek Pillár**: Look into the Excel-only review-output issue — Radim's downstream review/correction workflow is entirely manual spreadsheet work with no AI assistance in that step; explore whether a better alternative exists — due 2026-09-24 — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] **Radim Švarc**: Send back "correct" excel/json corrections to BigHub in a format agreed with Jura, so accuracy can be tracked over time — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] **Marek Pillár / Jura Brázdil**: Reconcile the disambiguation-approach conflict with ASM-119 — confirm whether the ranked-candidate mechanism is being reversed or whether this was a narrower UI-presentation point — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] **Marek Pillár / Jura Brázdil**: Reconcile the Blob storage/deployment blocker conflict with ASM-088 — confirm current dependency status on Dr. Max infra/BDC — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal

## Open Questions

- Does the rejection of "multiple candidate variants" fully reverse ASM-119's ranked-candidate-alternatives decision, or is it a narrower point about reviewer-facing presentation? Not resolved in these notes.
- Is the Blob storage/deployment blocker genuinely back on Dr. Max/BDC's side, contradicting ASM-088, or is this a different infra dependency (or a note-taking imprecision)?
- Whether číselník gaps (like Bezručova) should be fixed via a manual TEO update or a live API connection to Dr. Max's pharmacy list — not decided.
- What batch-creation logic BigHub uses on its side when Radim's twice-weekly Power Automate flow delivers documents to Blob storage — Radim asked this directly and it wasn't answered in the notes available.
- Whether Radim's uncertainty markers in his own notes ("notifikace na Míšu, že je nový excel?") — i.e. whether Míša gets notified automatically when a new Excel is ready — have been resolved, or are still open on his side.
- Whether the fully-manual, Excel-based review/correction step (no AI assistance) is worth revisiting — PM's own concern, not yet raised with Jura or Radim.
- Whether "excel/json" as the correction-feedback format satisfies the API-based feedback loop originally envisioned in ASM-120, or whether a stricter contract is still expected.

## Sentiment & Tone

Not assessable in detail from condensed bullet notes rather than a transcript — no tone or attribution signals beyond the topics and decisions themselves. Content-wise, this reads as a normal working-level technical sync consistent with the collegial, detail-oriented pattern from the 2026-09-16 session, with two open reversals against recent decisions that will need direct reconciliation rather than reading as friction.

## Routing Log

Routed on PM confirmation ("route everything you can"), 2026-09-23:

- **project-assumptions**: ASM-127 (SPEDOS confirmed, resolves ASM-089), ASM-128 (disambiguation-reversal conflict vs. ASM-119), ASM-129 (Blob storage/BDC conflict vs. ASM-088), ASM-130 (PM flags manual Excel-only review as a gap); updated ASM-089 (resolved) and ASM-120 (correction-feedback format concretized)
- **project-stakeholders**: STK-004 (Alana), STK-026 (Jura), STK-041 (Radim), STK-042 (Míša)
- **project-knowledge**: "TEO / OCR" entry updated with 2026-09-22 delivery progress and the two flagged conflicts
- **project-daily (2026-09-23)**: 9 action items added; Key Events and Audit Log entries written
- **project-lessons**: LL-053 captured (reconciling apparent decision-reversals rather than silently overwriting)
- **meetings/index.md**: entry added
