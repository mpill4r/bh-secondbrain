---
last_updated: 2026-09-16
classification: SoW / Proposal
source: internal
original_location: /Users/marekpillar/Downloads/OneDrive_1_9-16-2026/Dr_Max_TEO_navrh_AS (1).docx
---

# TEO/OCR — Solution Proposal (Variants & Estimates)

## Document Info

**Title**: Automatizace zpracování servisních listů a revizí — Návrh řešení pro technické oddělení Dr. Max [translated: Automating processing of service sheets and inspections — Solution proposal for Dr. Max's technical department]
**Author(s)**: BigHub (not individually attributed in the document)
**Date**: 2026-07 (July 2026)
**Classification**: SoW / Proposal
**Source**: Internal — BigHub draft, not yet shared with Dr. Max (per PM, 2026-09-16)
**Previous version**: N/A

## Executive Summary

BigHub's internal draft proposal laying out four solution variants for automating TEO/OCR (Dr. Max technical-department service-protocol processing), each with a man-day estimate and delivery target. Today's process is ~10,000 documents/year, ~3 pages average (up to 100-page bundles), with volume peaking each spring and autumn service season. The variants range from a lightweight API-only integration (12 MD) to a full internal validation web app (25-35 MD), with two optional add-ons (ServiceNow import automation, ServiceNow inspection-due readout) scoped as TBD effort. BigHub recommends starting with the 3-4 highest-volume document categories to front-load ROI and validate real-world accuracy before expanding scope.

## Key Points

**Today's process**: technical-department staff manually check and retype data from scanned PDFs into ServiceNow (SNOW). ~10,000 documents/year, ~3 pages/document on average, but single documents can bundle up to 100 pages. Volume peaks in spring and autumn inspection waves.

**Variant — API** (12 MD, delivery 4-6 weeks from approved spec): BigHub exposes an API on Dr. Max's existing AI platform; Dr. Max sends documents via API for processing through Microsoft AI Foundry models; structured JSON returned; downstream processing/SNOW import is Dr. Max's own responsibility; prompts tuned by BigHub per detected document category, no manual client-side prompt edits; includes validation passes over extracted results.
- *Pros*: simple, fast, no dependency on other systems; alternative sub-option lets Dr. Max edit prompts independently without involving BigHub.
- *Cons*: manual prompt rework needed if extraction quality is unsatisfactory; output is "just" JSON; limited handling of very large documents (needs internal prompt-engineering expertise + backtesting after every prompt change under the self-service alternative).

**Add-on — Nadstavba API / prompt editing** (+6 MD): exposes per-category prompt editing directly in Dr. Max's platform (extraction success not guaranteed under self-edited prompts).

**Variant — HYBRID** (18 MD, target: before autumn service season, assuming approved spec): builds a full OCR pipeline for agreed document types, triggered via API from Dr. Max's side. Categorizes documents, splits large bundles, extracts data, returns structured JSON. Segments that can't be read or fall below a confidence threshold are saved to shared storage for further handling. Prompts, categorization logic, and the OCR pipeline itself are code — not user-editable. Pipeline tuned to ≥94% reliability on the 3 most common variants per category, ≥75% on other variants. Reusable as the technical foundation for the APLIKACE variant later.

**Variant — APLIKACE (Application with validation)** (25-35 MD, target: before autumn service season, assuming approved spec): internal web app for technical-department staff that ingests documents from a shared mailbox, runs OCR/extraction, flags unclear values with a reason, lets staff validate/correct directly in-app, then prepares confirmed records for manual export (CSV or agreed format) to ServiceNow.
- *Pros*: built-in categorization/splitting pipeline for bulky documents; transparent (staff see document + result side by side); manual review of uncertain results before SNOW export means cleaner input data; prompt optimization driven by in-UI feedback; failed documents can be re-run.
- *Cons*: heavier implementation lift for both BigHub and Dr. Max; higher bar for collecting quality feedback from technical staff to drive prompt optimization correctly; mandatory manual review before SNOW export adds processing time.

**Add-on 1 — Automated SNOW import** (+TBD, dependent on Dr. Max's SNOW environment): documents/metadata write to ServiceNow automatically from the app — removes manual export/import.

**Add-on 2 — SNOW data readout** (+TBD, dependent on Dr. Max's SNOW environment): periodically reads equipment and inspection due-dates from ServiceNow; validates that a submitted inspection report covers all equipment a technician was scheduled to check; adds an upcoming-inspections-due overview to the app, replacing manual reminder tracking.

**BigHub's recommendation**: start implementation with the 3-4 most frequently processed document categories — these represent the largest share of volume and therefore the highest immediate manual-effort savings, while also letting BigHub validate real-world extraction accuracy and tune the solution before extending to lower-frequency categories. Recommends the first phase also favor the most common document variants/formats within each chosen category — high template/format diversity increases extraction complexity and can hurt model accuracy.

**Implementation notes**: large-document processing (20+ pages) has real limits — context-size pressure can degrade extraction quality or cause outright failure; mitigated by splitting documents into categorized chunks processed independently, and by automatically re-queuing on failure after a logged crash. All variants require some level of Dr. Max/BDC infrastructure-team involvement; historically, simple requests (e.g. a DNS record) take days, while requests needing external-network-access decisions take weeks.

## Extracted Requirements

- **DR-1**: Solution must categorize incoming documents automatically to route them to the correct extraction prompt/logic (all variants).
- **DR-2**: Solution must split large/bundled documents (up to 100 pages) into manageable segments for reliable extraction — source: Implementation notes.
- **DR-3**: HYBRID variant must reach ≥94% reliability on the 3 most common document variants per category, ≥75% on other variants — source: Variant HYBRID.
- **DR-4**: APLIKACE variant must flag uncertain extracted values with a stated reason and allow in-app staff correction before export — source: Variant APLIKACE.
- **DR-5**: Failed/low-confidence document segments must be preserved in shared storage for follow-up processing, not silently dropped — source: Variant HYBRID.

## Extracted Decisions & Assumptions

- **DA-1** (Open): Which of the 4 variants (+ optional add-ons) to formally propose to and pursue with Dr. Max is not yet decided — no client-facing commitment made in this document.
- **DA-2** (Proposed, BigHub-internal): Phased rollout should start with the 3-4 highest-volume document categories before expanding — stated as a recommendation, not yet confirmed with the client.
- **DA-3** (Implied): All build variants target production-readiness "before autumn service" — implies an autumn 2026 delivery pressure point, consistent with the previously-recorded November inspection-cycle target in `project-knowledge.md`, though phrased more loosely here ("before the autumn service wave" vs. a specific November date).

## Key Stakeholders & Contacts

No individuals named in this document — all references are to "BigHub" and "Dr. Max's technical department" collectively. Tomáš Burda (STK-025) and Radim Švarc (STK-041) are already tracked as this initiative's likely owner/domain expert respectively, per prior routing.

## Open Questions

- This document predates (July 2026) the 2026-09-15 Business Quantification call, where the ~40h/month (~5 MD) time estimate was independently reconfirmed — but no MD-effort variant here maps cleanly to "5 MD/month ongoing," since these are one-time build estimates, not run-rate. Worth clarifying with Radim/Burda whether recurring BigHub involvement (maintenance, prompt tuning) is expected beyond the build estimate.
- No per-MD or per-hour cost rate is given here (matches the still-open action item: Tomáš Burda to provide a rate).
- Document does not name a decision-maker or approval date — unclear whether any variant has since been informally favored internally.

## Routing Log

- **project-knowledge**: Merged into the "TEO / OCR" entry — new "BigHub's proposed solution variants" and "Provisioning" subsections (variant estimates, phased-rollout recommendation, implementation notes).
- **project-assumptions**: DA-1 → ASM-077 (Open — which variant to pursue not yet decided); DA-2 → ASM-078 (Open — phased rollout by document-category volume). DA-3 (autumn timing) merged into project-knowledge narrative text, no separate ASM.
- **project-daily**: Audit entries logged to 2026-09-16.
