---
last_updated: 2026-09-16
classification: Technical
source: internal
original_location: /Users/marekpillar/Downloads/OneDrive_1_9-16-2026/production_spec_cs.pdf
---

# TEO/OCR — Production Operational Spec (v1.1)

## Document Info

**Title**: Vytěžování servisních protokolů — jak bude řešení fungovat v provozu [translated: Extracting service protocols — how the solution will work in production]
**Author(s)**: BigHub (not individually attributed)
**Date**: 2026-08-07, v1.1
**Classification**: Technical
**Source**: Internal — BigHub draft, not yet shared with Dr. Max (per PM, 2026-09-16)
**Previous version**: N/A (references a separate, not-yet-ingested "OCR API v1.1" contract document for the formal API spec)

## Executive Summary

This is BigHub's detailed operational spec for the TEO/OCR pipeline's internally agreed architecture: blob storage intake → batch AI processing → API read-out. It documents, step by step, how a document moves through the system (upload → classification → dual-model reading → cross-check → assembly into protocols → API access), how uncertain results are flagged, and how multi-protocol documents get split and reassembled using deterministic rules rather than AI judgment. Measured against 370 real pages / 281 protocols across all 7 categories, the pipeline hits 90-100% field accuracy with a critical "silent error" rate (wrong value with no review flag) below 1.4-9% depending on field — the single most important number in the whole spec, since it's what could reach ServiceNow uncorrected. Mailbox intake and ServiceNow write-back are explicitly out of scope for this phase; today's output is API read-out of structured protocol records.

## Key Points

**Scope (this phase)**: processing of service/inspection protocols in all common forms (scans, photos, PDF, Word) across 7 tuned categories, plus a fallback mode for unrecognized forms; the 5 core extracted fields; an API to read results including crops/previews; ongoing accuracy measurement. **Explicitly not in scope this phase**: mailbox integration and ServiceNow integration — both can be added later without rearchitecting. Platform infrastructure details live in a separate document.

**Document journey (7 steps)**:
1. **Intake** — Dr. Max uploads files to a `dropbox/` folder in blob storage; the system polls the folder; duplicate uploads (by content hash) are processed only once.
2. **Prep** — each page is converted to an image (Word files are read as text directly).
3. **Classification** — a smaller AI model identifies document category from the first page (~95% accuracy); unrecognized types fall into a general mode with stricter human review.
4. **Reading** — every page is read independently by two AI models (GPT-5 and GPT-5-mini), each with category-tuned instructions, running in cost-efficient batch mode (typically done within hours, guaranteed within 24 hours).
5. **Cross-check** — for checkbox-style forms (PBZ, door checklists), Azure AI Document Intelligence independently detects checked fields.
6. **Assembly** — pages are assembled into complete protocol records with a final verdict, governed entirely by deterministic rules (§4 of the source doc) — no AI judgment involved at this step.
7. **Result** — protocol records become available via API, including links to source crops and a rendered preview.

**5 extracted fields per protocol**: protocol type/category; inspection date (verbatim as written + normalized format; never confused with next-inspection-due date); pharmacy address (actual site of inspection, including from a customer stamp; in-building location like "2nd floor" or "warehouse" excluded); branch/cost-center number (including from stamps; landlord building codes excluded); inspection/document title (verbatim printed title); service company (vendor who performed the inspection — Dr. Max or the building's landlord are never recorded here); verdict/compliance status (only when explicitly stated on the page — see verdict logic below); defects/findings (verbatim transcription, used both to justify the verdict and for review); uncertain-fields list (self-flagged low-confidence fields).

**Verdict logic**: only an explicit verdict counts — a circled option ("device IS/IS NOT operational"), a checked compliant/non-compliant box, a verdict sentence, or (for PBZ) a color status (green = compliant, yellow = compliant with reservations, red = non-compliant). An explicit "device functional: NO" checkbox always overrides a milder color status. A positive verdict plus recorded defects on the same page becomes "compliant with reservations," with the defects surfaced in the justification. A routine service sheet with no stated verdict (typically air conditioning) honestly gets "no verdict stated" — the system never converts "work was performed" into "passed."

**Multi-protocol assembly rules** (deterministic, not AI-judged): a new page starts a new protocol only when *both* models independently agree it's a new protocol start; on disagreement, the page attaches to the in-progress protocol and gets flagged for a human to verify the boundary — this rule resolved all 39 disputed boundaries correctly in testing (signature backs, repeated-header report pages, two-page service sheets). A safeguard also catches forms that reprint a full header on every table page (fire extinguishers, hydrants) — if such a page lacks its own date/branch number, it's attached to the previous protocol with a flag. A protocol's final verdict is always the worst explicit verdict across its pages (non-compliant beats reservations beats compliant); a model disagreement on verdict takes the worse reading and flags for review; "no verdict but defects recorded" also goes to review. Header fields (date, address, company…) take the first populated value across pages; a second model reading a different value sends that field to review. Optional (per Dr. Max preference): for landlord-issued blanket documents, the system can merge per-device sheets into one record per inspection visit (e.g. 33 fire-door sheets → 1 row with the worst verdict).

**Storage**: blob storage holds the `dropbox/` intake folder plus page images, crops, and protocol previews — crops/previews are never served via direct storage link, only through the keyed API. The database holds document/page records, both models' complete raw outputs (for audit), assembled protocol records, and reviewer-correction history (used to keep improving the system). Everything is fully replayable from the original `dropbox/` files — this is also the basis for verification/validation (V&V) and resolving any future disputes.

**API** (full contract in a separate "OCR API v1.1" document, not yet ingested): `GET /ocr/protocols?since=…` lists newly completed protocols; `GET /ocr/protocols/{id}` returns the 5 fields plus verdict/justification/citation, review flags, and full per-page underlying data; `GET /ocr/protocols/{id}/render.pdf` renders the protocol's pages as one PDF (always addressed at protocol level, never the raw source file, since one file can contain up to 50 protocols); every flagged field carries a link to a crop of the original so a reviewer can verify by sight without hunting through the source file; a `review_required` flag marks records needing human attention — which specific triggers set that flag is a tunable setting (measured impact shown in §7 of the source), and changing the setting never requires reprocessing already-read documents.

**Measured accuracy** (on 281 protocols from real documents against manually verified reference data) — the "silent error" column (wrong value with no review flag) is called out as the single most important number:

| Field | Correct | Flagged for review | Silent error |
|---|---|---|---|
| Inspection date | 90.9% | 16 | 3 (1.4%) |
| Pharmacy address | 86.8% | 7 | 15 (9%) |
| Branch/cost-center | 91.6% | — | 17 |
| Protocol title | 100%* | 0 | 0 |
| Service company | 100%* | 0 | 0 |
| Verdict | 100%* | 0 | 0 |

(*The three 100% fields had their reference data built from agreement between both model readings, so the figure should be read cautiously — ~45 protocols were independently re-verified by manual scan reading + cross-checked checkbox detection, and no verdict errors were found. Production accuracy is continuously tracked from reviewer corrections.) Before any prompt or model change ships, the system automatically re-measures against the reference set — a change that would reduce accuracy is blocked from going live.

**Error handling**: a delayed or partially returned batch auto-resends unprocessed pages next cycle (nothing lost); an unreadable/corrupt file ends up in a "failed" state with a reason (never silently disappears); if one of the two model readings fails for a page, the page still processes on the surviving reading, but all its fields get flagged for review (no silent single-source results); a failed checkbox cross-check doesn't halt anything, it's just noted as unconfirmed; unrecognized document types get the general fallback mode with stricter review, using the same safeguards (flags, citations) as tuned categories.

**Cost**: ~0.35 Kč/page in batch mode, ~0.60 Kč/page in fast mode (for urgent cases); roughly 9,000 Kč/year in inference at an assumed 30,000 pages/year.

## Extracted Requirements

- **DR-1**: Duplicate file uploads (same content) must be detected and processed only once.
- **DR-2**: A protocol boundary is only established when both independent model readings agree; disagreement attaches the page to the in-progress protocol and flags the boundary for human review.
- **DR-3**: A protocol's assembled verdict must always be the worst explicit verdict found across its constituent pages.
- **DR-4**: Crops and previews must never be served via a direct, unauthenticated storage link — API access only, with a key.
- **DR-5**: Any accuracy-affecting model/prompt change must be automatically re-measured against the reference set before going live; regressions are blocked.
- **DR-6**: Mailbox intake and ServiceNow write-back are out of scope for this phase but must be addable later without re-architecting.

## Extracted Decisions & Assumptions

- **DA-1** (Decided, internal, v1.1): Architecture is blob storage → batch processing → API — described explicitly as "the agreed solution," dated 2026-08-07.
- **DA-2** (Decided): Dual independent AI readings (GPT-5 + GPT-5-mini) with rule-based (non-AI) assembly logic for multi-page/multi-protocol documents.
- **DA-3** (Assumption): Cost/accuracy figures assume 30,000 pages/year — see the reconciliation note also raised in the accuracy-validation document (`2026-09-16-teo-ocr-accuracy-validation-cost-analysis.md`).
- **DA-4** (Open): The specific triggers that set `review_required` are described as tunable, to be "worked out together" with Dr. Max — not yet finalized.

## Key Stakeholders & Contacts

No individuals named. References Dr. Max's technical team as the document uploader/reviewer collectively.

## Open Questions

- The referenced "OCR API v1.1" contract document (full technical API spec) has not been provided/ingested — worth requesting if a deeper technical review is ever needed.
- This document's existence and detail level (an "agreed," versioned spec dated 2026-08-07) sits awkwardly against `project-knowledge.md`'s current framing of TEO/OCR as "still a local feasibility prototype ... not deployed anywhere" as of the 2026-09-07 portfolio review — flagged for PM resolution in the routing review below (PM has already confirmed these documents reflect current reality — see below).
- Unclear whether this internal spec has ever been discussed with Radim Švarc or Tomáš Burda, given the Sept 15 Business Quantification call still treated KPI definition and even basic feasibility as fully open.

## Routing Log

- **project-knowledge**: Merged into the "TEO / OCR" entry — new "Agreed production architecture (v1.1)" subsection (pipeline steps, verdict/assembly logic, API design, silent-error accuracy framing), plus "Status correction" note superseding the 2026-09-07 "local prototype" framing.
- **project-assumptions**: DA-1 and DA-2 → ASM-076 (Decided — agreed architecture, dual-model + deterministic assembly). DA-3 (page-volume reconciliation, same as the accuracy-validation doc) and DA-4 (review_required tunability, open) merged into project-knowledge narrative text, no separate ASM.
- **project-daily**: Audit entries logged to 2026-09-16.
