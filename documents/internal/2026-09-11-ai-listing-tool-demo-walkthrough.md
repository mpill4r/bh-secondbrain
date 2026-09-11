---
last_updated: 2026-09-11
last_updated_by: auto — project-document ingestion
classification: Design
source: internal
---

# Document Summary — AI Listing Tool Demo Walkthrough

## Document Info

| Field | Value |
|-------|-------|
| Title | Dr. Max AI Listing Tool — Demo Walkthrough |
| Presented by | Filip Černý (BigHub — dev owner, Reklamace / logistics / Listing streams; STK-006) |
| Classification | Design (structured UI/product walkthrough) |
| Source | Internal (BigHub-only, not client-facing) |
| Original location | Provided by PM in conversation (structured notes derived from a recorded demo); original recording not stored in the harness |
| Related harness artifact | `product/solution-space/listing-specifikace.md` — this content was already used to enrich that document before being formally routed here |

## Executive Summary

This document captures a structured walkthrough of the Dr. Max AI Listing Tool, presented by Filip Černý. It is an internal e-commerce PIM (Product Information Management) and AI catalog-enrichment platform for pharmacy/health e-commerce content managers, covering catalog health scoring, AI-generated product content, and per-category rule configuration ("Listovací minima"). The walkthrough traces five screens — category selection, product catalog table, AI-assisted product detail editing, category rule/prompt configuration, and return to overview — and confirms that several roadmap items already marked "Done" are demonstrably working. It also surfaces capabilities not previously documented anywhere in the harness: a per-product health/completeness score, version history with rollback, a granular per-field AI prompt configuration system, a 28-attribute product taxonomy, and a regulatory compliance blacklist for non-compliant medical claims. The demo confirms the tool's current live scale: 72 products in the single pilot category ("Proteiny / Doplňky stravy").

## Key Points

- **Category selection screen**: search + recent-category shortcuts; user enters a category to work within.
- **Product catalog table**: per-product SKÓRE (health/completeness score, 0–100-style progress bar), STAV (per-product workflow status: observed values *Import*, *Rozpracováno*), and PROBLÉMY (validation issue badges by severity). Pagination confirmed 72 products in the demoed category.
- **Product detail / AI generation**: dual-pane diff editor (current listing vs. AI proposal), validation score breakdown, source selection for generation (original listing text vs. custom text), one-click "Generovat" to produce structured description sections (intro, key features, composition, dosage, warnings) plus AI-enriched structured parameters, and version history with rollback (e.g. to v2.04).
- **Category rules ("Listovací minima")**: per-category configuration covering (1) 6 description fields, each with a natural-language AI prompt, min/max character counts, and a mandatory flag; (2) 2 meta-description fields with fixed character ranges (140–180 and 60–90 chars); (3) a 28-attribute product parameter taxonomy, each independently toggled between AI auto-generation and manual-only; (4) a blacklist of non-compliant medical-claim phrases (e.g. "léčí", "hojí", "terapeutický", "léčivý", "uzdravuje", "zmírňuje příznaky").
- **Design system**: Dr. Max green brand palette for primary actions/valid states, semantic red/amber/green for error/warning/success, split/diff-screen pattern for AI review, high information density suited to back-office bulk SKU processing, and an AI-integration pattern built around explicit user-triggered generation plus visual diffing rather than silent automation.

## Extracted Requirements

**DR-1** · Confirmed capability · per-field AI prompt configuration
Each of the 6 listing description fields (Úvodní text, Hlavní vlastnosti, Složení, Dávkování, Upozornění, O značce) has an independently configurable natural-language AI prompt, a min/max character count, and a mandatory flag, set per category.

**DR-2** · Confirmed capability · meta-description constraints
Meta descriptions enforce fixed character ranges: Krátký popis 140–180 characters, Teaser popis 60–90 characters.

**DR-3** · Confirmed capability · per-attribute generation control
Each of the 28 product parameter attributes can be independently toggled between AI auto-generation and manual-only entry.

**DR-4** · Confirmed capability · compliance guardrail
Generated content is checked against a per-category blacklist of non-compliant medical/curative claim phrases before use.

**DR-5** · Confirmed capability · catalog health scoring
Every product carries a numeric health/completeness score plus a categorized breakdown of validation issues (error / warning / info), visible both in the catalog table and the product detail view.

**DR-6** · Confirmed capability · version history
Product listing edits are versioned, with a rollback selector exposed in the product detail header.

## Extracted Decisions & Assumptions

None — this is a descriptive product walkthrough rather than a decision-making session. It corroborates existing assumptions ([[ASM-011]], [[ASM-031]]) about Listing's current single-category scope but does not introduce new decisions.

## Key Stakeholders & Contacts

- **Filip Černý** (STK-006) — already tracked in `project-stakeholders`. No new stakeholders identified. No role/sentiment change warranted purely from this demo.

## Open Questions

- Only two product-level workflow statuses were observed (*Import*, *Rozpracováno*) — is there a further lifecycle state (e.g. approved/published), and what triggers each transition?
- The "Odvodit minima" (derive minima) button on the category rules screen was visible but not exercised in the walkthrough — unclear what it automates.
- Is the 28-attribute parameter taxonomy fixed platform-wide, or configurable per category? The walkthrough only showed one category's configuration.
- Is the non-compliant medical-claims blacklist itself signed off by Dr. Max, or a BigHub-authored draft pending client review? Relevant given the account's broader pattern of BigHub building ahead of client-side sign-off.

## Routing Log

- **project-knowledge**: Added "AI Listing Tool (Dr. Max)" (Client Jargon) and "Listing — non-compliant medical claim blacklist" (Regulatory & Compliance, status: Needs confirmation).
- No routing to `product-requirements` / `product-brief` / `product-scope` — those artifacts track the Second Brain meta-tool in this harness, not Dr. Max's products.
- No stakeholder changes — Filip Černý already fully tracked (STK-006).
