---
last_updated: 2026-09-16
classification: Technical
source: internal
original_location: "/Users/marekpillar/Downloads/OneDrive_1_9-16-2026/navrh_ocr_cs 2.pdf"
---

# TEO/OCR — Accuracy Validation & Cost Analysis

## Document Info

**Title**: Automatizovaná extrakce servisních protokolů — návrh řešení [translated: Automated extraction of service protocols — solution proposal]
**Author(s)**: BigHub (not individually attributed)
**Date**: 2026-08 (August 2026)
**Classification**: Technical
**Source**: Internal — BigHub draft, not yet shared with Dr. Max (per PM, 2026-09-16)
**Previous version**: N/A

## Executive Summary

BigHub's internal validation report for the TEO/OCR extraction pipeline, measured on 366 real pages across all 7 document categories — this is materially past prototype stage. The solution reads each page with two independent models (GPT-5 + GPT-5-mini, natively in Microsoft Azure AI Foundry) whose results are merged; checkbox-style forms get an added deterministic pass via Azure AI Document Intelligence. Overall measured accuracy is 91% on handwritten free-text content and 94% on structural form content, with 0 fabricated values found across 500+ pages tested and 14% of pages flagged for human review. Running cost is negligible (~17,000 Kč/year unbatched, ~8,500 Kč/year with batch processing at 30,000 pages/year) since it reuses BigHub's existing shared AI platform — no new paid Azure resources required. Full automation (mailbox intake, SNOW write-back) needs three external provisioning requests that historically take days (infra) to weeks (cross-team).

## Key Points

**Architecture**: dual reading via GPT-5 (primary) + GPT-5-mini (independent check) natively in Microsoft Azure AI Foundry — results are merged; prompts tuned per document-form category. Checkbox-style forms get an additional deterministic pass via Azure AI Document Intelligence to detect checked fields. Any field where the two readings disagree, or where the system itself is uncertain, is flagged for human review and backed by a crop/excerpt of the original source. The system is designed to never invent content — 0 fabricated values found across 500+ pages tested. Runs fully inside Azure — no data leaves the client's tenant.

**Accuracy by category** (measured on 292 reference pages across all 7 tuned categories):

| Category | Pages | Handwriting accuracy | Structural accuracy |
|---|---|---|---|
| Automatic doors | 83 | 92% | 91% |
| PBZ (fire safety) | 69 | — | 100% |
| Electrical/EZS/lightning rods | 62 | 100% | 93% |
| Air conditioning/HVAC | 28 | 90% | — |
| Elevators | 22 | 87% | — |
| Gas/pressure vessels/flue paths | 20 | — | — |
| Fire extinguishers/hydrants | 8 | — | 93% |
| **Total (7 categories)** | **292** | **91%** | **94%** |

("—" = fewer than 8 findings in that category/line, too small a sample for a meaningful percentage; still counted in the total row.)

**Header-field accuracy**: pharmacy branch/cost-center 92% (read from header and customer stamp); address 76% (biggest gap is an ambiguous definition — pharmacy address vs. equipment's in-building location — accuracy improvable once the definition is clarified with the client); inspection/protocol type 93%; equipment type 93%; equipment count — accuracy not yet measured (schema extension in progress, read deterministically via Azure AI Document Intelligence); date 92% (mismatched readings flagged for review; residual unflagged error rate ~1-2% after review).

**Review load**: 14% of pages are flagged for human review; every flagged field carries a crop of the original for fast verification.

**Cost**: ~0.55 Kč per page for dual-model inference; ~17,000 Kč/year (~$735) at an assumed 30,000 pages/year; ~8,500 Kč/year with batch processing (-50%). No new paid Azure resources needed — GPT-5 and GPT-5-mini are already deployed on the shared AI platform; storage, database, and monitoring already exist.

**Provisioning needed for full automation** (can be requested in parallel): (1) shared mailbox + Microsoft Graph API app access from Dr. Max's IT/M365 team — historically weeks for this type of cross-team request; (2) AKS firewall egress rule from the infra team — standard request, days to weeks; (3) ServiceNow import-set API access from the SNOW team — only needed for the write-back phase; until then, output is a review spreadsheet (Excel with crops) + notification. Recommends submitting these requests immediately once the next phase is approved.

## Extracted Requirements

- **DR-1**: System must flag any field where dual-model readings disagree, or where confidence is low, for human review with a source crop attached.
- **DR-2**: System must never fabricate content for unreadable/absent fields — validated at 0 fabrications across 500+ tested pages.
- **DR-3**: Checkbox-style forms require deterministic checkbox detection (Azure AI Document Intelligence) in addition to LLM reading.
- **DR-4**: Full automation requires 3 external provisioning grants (mailbox/Graph API access, AKS firewall egress, SNOW import-set API access) before mailbox intake and SNOW write-back can go live.

## Extracted Decisions & Assumptions

- **DA-1** (Decided, internal): Dual-model reading architecture (GPT-5 + GPT-5-mini via Azure AI Foundry, merged, with Document Intelligence for checkboxes) is the validated technical approach — not merely proposed, but measured against real data.
- **DA-2** (Assumption): Cost projections assume 30,000 pages/year — this is notably higher than the ~250 docs/week (~13,000/year, ~3 pages avg per the proposal doc = ~39,000 pages/year) figure elsewhere; roughly consistent order of magnitude, not a hard conflict, but worth reconciling which page-volume figure is authoritative.
- **DA-3** (Open): Whether/when to request the 3 external provisioning items is not decided — recommended "immediately after next-phase approval," which hasn't happened yet.

## Key Stakeholders & Contacts

No individuals named — document refers to "Dr. Max/BDC infrastructure team," "IT/M365 team," and "SNOW team" collectively, without naming contacts (Vladislav Tvarůžek, STK-016, is the existing tracked BDC infra contact and may be relevant here, though not explicitly named in this document).

## Open Questions

- Address-field accuracy (76%) is explicitly attributed to an ambiguous definition (pharmacy address vs. equipment's physical location within a building) rather than a model-quality gap — this is an open definitional question for Dr. Max, not a technical one.
- Equipment-count field accuracy not yet measured — schema work in progress.
- Page-volume figure here (30,000/year) vs. the proposal document's implied ~39,000/year — not flagged as a hard contradiction, but worth a single authoritative figure going forward.

## Routing Log

- **project-knowledge**: Merged into the "TEO / OCR" entry — new "Validated architecture & accuracy" and "Cost" subsections.
- **project-assumptions**: DA-1 → ASM-076 (Decided — dual-model architecture validated). DA-2 (page-volume reconciliation) and DA-3 (provisioning-timing, open) merged into project-knowledge narrative text, no separate ASM.
- **project-daily**: Audit entries logged to 2026-09-16.
