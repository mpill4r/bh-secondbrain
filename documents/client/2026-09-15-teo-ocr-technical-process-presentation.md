---
last_updated: 2026-09-15
source: client
classification: Presentation
---

# TEO/OCR — Technical Process Presentation (Dr. Max)

**Original file**: `PROJEKT_TECHNICKE 1.pptx` (5 slides, provided by Radim Švarc during the 2026-09-15 Business Quantification call)
**Ingested**: 2026-09-15
**Related meeting**: [2026-09-15-business-quantification-teo-ocr](../../meetings/external/2026-09-15-business-quantification-teo-ocr.md)

## Executive Summary

Dr. Max's technical department's own working presentation on the TEO/OCR problem — the same one Radim Švarc referenced live during today's Business Quantification call. It documents today's fully manual process (external service vendors email scanned PDF inspection reports with no OCR layer; a technician retypes data by hand into ServiceNow), confirms the previously-cited volume/time figures (~250 documents/week, ~40h/~5MD per month), and proposes a concrete automated-process architecture (dedicated intake email → PowerAutomate → AI extraction via API → reviewable Excel → SNOW import). Notably, Dr. Max's own team has already tested Claude directly on a 100-page sample document and is explicitly asking BigHub to confirm feasibility and a possible timeline.

## Key Points

**Current process** (Slide 2): External service vendors ("dodavatel") perform servicing at pharmacies and produce an inspection document per visit; documents are scanned and emailed as PDFs with no OCR layer to Dr. Max's technical department. A single document can contain up to ~100 individual inspections, covering multiple inspection types depending on equipment. A technician (Dr. Max staff) goes page by page, manually transcribing: cost-center/branch number (středisko), address, date, equipment type/count, order number (zakázka), service company, and technician-written defect notes — then manually re-enters all of it into ServiceNow. This confirms the volume/time figures already captured in today's call: ~250 documents/week, ~40 hours (~5 MD) per month of manual work.

**Proposed automated process** (Slide 4): Vendors keep sending documents as today, but to a dedicated intake email address (example given: `revize@drmax.cz`); some vendors instead save to a shared network drive. An automated service captures incoming emails and saves attachments, then sends them to an AI tool (via API) for extraction. Extracted data populates a shared Excel available to the technician, with uncertain/mismatched fields flagged (color or note) for review. The technician checks the Excel before it's imported into ServiceNow — either manually (a mechanism being prepared by a BDC-side contact, "pan Wágner") or automatically (via simulated user-click automation) — the choice between these two isn't decided in the document.

**Proposed tech stack** (Slide 5): Microsoft PowerAutomate for reading the email inbox and saving attachments; Python for sending documents to the AI tool and building/appending Excel rows (potentially reusable for the SNOW import step too); and an AI extraction layer described as either "BigHub's internal model" or Claude specifically — the presentation states Dr. Max's own team already tested **Claude directly on a 100-page document** (as an attachment to the original presentation, not included in what was shared here) and got it to read the full document, produce a complete xlsx of all rows, and flag unclear/incorrectly-read rows. The slide closes with a direct question to BigHub: **"bude možné BigHub využít? Možný termín?"** [translated from Czech: "Will it be possible to use BigHub [for this]? What's a possible timeline?"]

## Extracted Requirements

| ID | Requirement | Source |
|----|-------------|--------|
| DR-1 | Vendor documents should be redirected to a dedicated intake email address (e.g. `revize@drmax.cz`) as the primary ingestion mechanism | Slide 4 |
| DR-2 | An automated service must capture incoming emails and persist attachments (proposed tool: PowerAutomate) | Slide 4 |
| DR-3 | Saved documents must be sent to an AI extraction tool via API, extracting: cost-center number, address, date, equipment type/count, order (zakázka) number, service company, and technician-noted defects | Slide 2, 4 |
| DR-4 | Extracted data must be written into a shared Excel accessible to the technician, with uncertain/mismatched fields flagged (color or note) for review | Slide 4 |
| DR-5 | Technician reviews/corrects the Excel before ServiceNow import | Slide 4 |
| DR-6 | ServiceNow import mechanism — manual (BDC-prepared) or fully automated (click-simulation) — not yet decided | Slide 4 |

## Extracted Decisions & Assumptions

| ID | Item | Source |
|----|------|--------|
| DA-1 | Proposed tech stack: PowerAutomate (email/attachment capture) + Python (AI-tool orchestration, Excel row generation, possible SNOW import) + AI extraction layer (BigHub's model or Claude) | Slide 5 |
| DA-2 | Dr. Max's own team has already tested Claude directly against a 100-page sample document, successfully reading the full document, generating a complete row-level xlsx, and flagging uncertain/incorrect rows — informal client-side validation predating any formal BigHub pipeline | Slide 5 |
| DA-3 (open ask, not yet answered) | Dr. Max is directly asking BigHub to confirm feasibility of using BigHub for this extraction pipeline, and for a possible delivery timeline | Slide 5 |

## Key Stakeholders & Contacts

- **"pan Wágner" (BDC)** — new, low-confidence (surname only, no first name or further detail) — preparing the manual Excel-to-ServiceNow import mechanism as a fallback/interim path if automated import isn't pursued.
- Radim Švarc, Tomáš Burda — already in `project-stakeholders.md` (STK-041, STK-025); no new detail beyond what today's meeting captured.

## Open Questions

- Manual vs. automated ServiceNow import — not decided in the document; depends partly on whether Wágner's manual mechanism or a click-simulation automation is pursued.
- Direct, unanswered ask to BigHub: is this pipeline feasible on BigHub's side, and what's a realistic delivery timeline? This reads as a concrete action item for Marek/BigHub to respond to, not just background context.
- Whether the "AI tool" is expected to be BigHub's existing internal model or a direct Claude integration — the presentation uses both framings without fully reconciling them.

## Routing Log

- **project-stakeholders**: Added STK-047 ("Wágner," BDC, low-confidence — preparing the manual SNOW import mechanism). No new detail added for Radim Švarc/Tomáš Burda beyond what the related meeting already captured.
- **project-knowledge**: Merged into the "TEO / OCR" entry alongside the 2026-09-15 meeting content — see [DR-1 through DR-6 / DA-1 through DA-3] for the specific extracted architecture/decision points now reflected there.
- **project-daily**: 1 highest-prio action item added — respond to Dr. Max's direct feasibility/timeline ask (DA-3).
- **Related meeting**: [2026-09-15-business-quantification-teo-ocr](../../meetings/external/2026-09-15-business-quantification-teo-ocr.md) — routed as a combined review alongside this document.
