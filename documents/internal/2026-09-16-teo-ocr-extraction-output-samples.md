---
last_updated: 2026-09-16
classification: Presentation
source: internal
original_location: /Users/marekpillar/Downloads/OneDrive_1_9-16-2026/ukazka_extrakce.pdf
---

# TEO/OCR — Extraction Output Samples

## Document Info

**Title**: Vytěžení servisních protokolů — ukázka výstupu [translated: Service protocol extraction — output sample]
**Author(s)**: BigHub (not individually attributed)
**Date**: 2026-08 (August 2026, per cover page)
**Classification**: Presentation
**Source**: Internal — BigHub draft, not yet shared with Dr. Max (per PM, 2026-09-16)
**Previous version**: N/A

## Executive Summary

A 13-page side-by-side demo deck showing 12 real example extractions across all 7 tuned document categories (automatic doors, PBZ/fire safety, gas/pressure vessels, electrical/EZS/lightning-rods/hydrants, air conditioning, elevators, fire extinguishers/hydrants) — original document on the left, system output on the right. Each example shows the extracted verdict with a direct quote and page citation, the reasoning behind it, the 5 extracted header fields, and which fields (if any) were flagged for human review. This is the most concrete illustration available of what a reviewer actually sees day-to-day, and it makes visible how often even "flagged" examples still return highly usable structured data.

## Key Points

12 example protocols shown, spanning all 7 categories:

| Category | Verdict shown | Fields flagged for review |
|---|---|---|
| Automatic doors (155.pdf) | NEVYHOVUJE (non-compliant) | způsobilost (verdict) |
| Automatic doors (Termetal) | VYHOVUJE S VÝHRADAMI (compliant w/ reservations) | způsobilost |
| Automatic doors (Prostějov) | VYHOVUJE S VÝHRADAMI | datum (date) |
| PBZ (Frýdek Místek) | NEVYHOVUJE | název kontroly, servisní firma |
| Gas (Kontropa) | VYHOVUJE S VÝHRADAMI | způsobilost |
| Gas (boiler service) | VYHOVUJE | adresa (address) |
| Electrical/EZS (boiler check) | BEZ ZÁVĚRU NA DOKUMENTU (no verdict stated) | způsobilost |
| Electrical/EZS (fire+safety review) | VYHOVUJE S VÝHRADAMI | adresa, způsobilost |
| Air conditioning | BEZ ZÁVĚRU NA DOKUMENTU | způsobilost |
| Elevators (Hustopeče, 2018) | NEVYHOVUJE | segmentace (segmentation), způsobilost |
| Elevators (Hustopeče, 2024) | BEZ ZÁVĚRU NA DOKUMENTU | segmentace, způsobilost |
| Fire extinguishers/hydrants (Zlín) | BEZ ZÁVĚRU NA DOKUMENTU | segmentace, servisní firma, způsobilost |

Every example includes: the verdict as a direct, page-cited quote from the source document; a plain-language reason (defects/findings that justify it); the 5 extracted header fields (inspection date, pharmacy address, inspection title, service company, branch/cost-center); and an explicit flag list for any field the system itself was not confident about. Multi-page protocols show which page was used as the representative view (e.g. "6 stran; zobrazena strana 1 a 5").

Notably, several examples show "BEZ ZÁVĚRU NA DOKUMENTU" (no verdict stated on the document) rather than a fabricated pass/fail — a direct real-world illustration of the "never invents content" behavior also described in the accuracy-validation document (`2026-09-16-teo-ocr-accuracy-validation-cost-analysis.md`). "Segmentace" (segmentation/boundary) flags appear specifically on multi-page elevator and fire-extinguisher documents, matching the production spec's description of page-assembly edge cases (`2026-09-16-teo-ocr-production-spec-v1-1.md`).

## Extracted Requirements

None beyond what's already captured in the production spec and accuracy-validation documents — this is a demonstration artifact, not a new requirements source.

## Extracted Decisions & Assumptions

None — purely illustrative.

## Key Stakeholders & Contacts

No individuals named. Service-vendor company names appear per example (ASSA ABLOY Entrance Systems, TERMETAL Moravia, TRIDO, TriLine, EMI-TEST, JETOP, BOZP-PO, INKOMO CZ, TÜV SÜD Czech, ThyssenKrupp Výtahy, Hastech Servis) — these are third-party inspection vendors referenced inside extracted data, not project stakeholders, and are not being added to `project-stakeholders.md`.

## Open Questions

None — content is self-contained and consistent with the other three TEO/OCR documents ingested today.

## Routing Log

- **documents-index**: Entry added. No further routing — purely illustrative of accuracy/behavior already captured from the other 3 documents in this batch; referenced from `project-knowledge.md`'s "Validated architecture & accuracy" subsection as supporting evidence.
