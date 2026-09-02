---
status: wip
last_updated: 2026-04-17
owner: Jan Koscelansky
phase: Phase 1
---

# Phase 1 — Type System + Scope/Feature Foundations

## Overview

Phase 1 establishes a type system across `product-scope` and `product-feature` — the foundation that Phase 2 (backlog-import rewrite) writes into. It modifies two existing skills and their templates; it adds no new skills and no new harness artifacts.

After Phase 1 ships, PMs can:
- Create scope entries with explicit types and Notes metadata under a canonical feature-table structure
- Create typed feature specs whose Q&A adapts to the feature's type
- Receive AI-proposed "Suggested Spec Order" recommendations on every scope review (always PM-confirmed before any write)

Phase 1 ships standalone value — it does not depend on Phase 2. Phase 2 depends on Phase 1.

Related specs: `IMPROVEMENT-SPEC-phase2-backlog-import.md`, `IMPROVEMENT-SPEC-phase3-codebase-audit.md`, `IMPROVEMENT-SPEC-phase4-integration.md`.

---

## Commands

| Command | When to use |
|---------|-------------|
| `/product-scope {phase-slug}` | Existing trigger. Phase 1 adds Type + Notes columns, product-area description paragraphs, and AI-proposed Suggested Spec Order on every review. |
| `/product-feature {feat-id or name}` | Existing trigger. Phase 1 adds `type` frontmatter and type-aware Q&A branching. |

No new commands. No new foundational artifacts; Phase 1 modifies the templates and skill logic of existing commands.

---

## User Roles

| Role | Interaction | Key Need |
|------|------------|----------|
| PM | Creates and edits scope entries and feature specs; confirms or adjusts AI-proposed Suggested Spec Order | Consistent type tagging across work; credible sequencing proposals to confirm rather than author from scratch |
| Other skills | `product-backlog-import` (Phase 2) reads the Type vocabulary, canonical feature-table structure, and Notes schema established here | Stable type vocabulary and Notes format so downstream writers produce consistent scope content |

---

## Document Structure

Phase 1 modifies two existing documents. No new documents introduced.

| # | Document | Primary data sources |
|---|----------|---------------------|
| 1 | `product/solution-space/product-scope-{phase-slug}.md` | PM input during `/product-scope`; Phase 1 adds Type + Notes columns to the canonical feature table, product-area description paragraphs, and a Suggested Spec Order section |
| 2 | `product/solution-space/features/FEAT-NNN-{slug}.md` | PM input during `/product-feature`; Phase 1 adds `type` frontmatter |

### Type vocabulary

Constrained values for Type (applied to scope tables and feature frontmatter):

| Type | Applies to |
|------|-----------|
| `feature` | New product capability |
| `bug` | Defect fix |
| `tech` | Technical debt, infrastructure, DX |
| `spike` | Time-boxed research |
| `other` | Escape hatch for items that don't fit the above |

Starting vocabulary is always these five. PMs may introduce project-specific types; custom types are accepted and preserved without validation prompting once introduced.

### Canonical feature-table structure

Phase 1 establishes a canonical feature-table structure in `product-scope/TEMPLATE.md`. The current template is skeletal (product-area tables emerge during `/product-scope` Aggressive Pre-Fill). Phase 1 adds a sample feature table under `## Product Areas / Epics` to establish the column order as the reference:

```markdown
## Product Areas / Epics

> Structure: each tier (Priority, Standard) contains product areas. Each area has
> a description paragraph above its feature table explaining what the area covers
> and why it matters. FEAT-NNN IDs are sequential across the scope.

### Priority

#### {Product Area Name}

> {1-paragraph description — the what and why of the area.}

| Feature ID | Name | Type | Description | Status | Design Status | Linear IDs | Notes |
|------------|------|------|-------------|--------|---------------|------------|-------|
| FEAT-NNN | {Feature name} | {feature\|bug\|tech\|spike\|other} | {Capability-level description} | {defined\|drafted\|speced\|in development\|released} | {not needed\|needed\|in progress\|done} | {source IDs if imported} | {aggregate points, context, blockers, relationships} |

### Standard

(same structure)
```

`product-scope/SKILL.md` A5 Aggressive Pre-Fill MUST emit feature tables in this column order.

### Suggested Spec Order section shape

Added to every `product-scope-{phase-slug}.md`:

```markdown
## Suggested Spec Order

> AI-proposed sequencing based on dependency analysis, priority signals, spec
> readiness, delivery risk, and user/business value. Review and adjust with
> `/product-scope` — the skill never writes or updates this section without PM
> confirmation.

1. **FEAT-NNN Feature Name** — rationale in 1-2 sentences: what it unblocks,
   delivery risk, spec readiness signals, strategic value
2. ...
```

One entry per FEAT in scope. If scope has zero FEATs, the section renders with a placeholder line ("No FEATs in scope yet — rerun `/product-scope` after adding features.") instead of an empty section.

---

## Requirements

### Functional — product-scope

**FR-PS-1** Every scope document MUST use the canonical feature-table column order: `Feature ID | Name | Type | Description | Status | Design Status | Linear IDs | Notes`. The canonical structure lives in `product-scope/TEMPLATE.md` as a sample; `product-scope/SKILL.md` A5 Pre-Fill emits tables in this column order.

**FR-PS-2** Each product area in a scope document MUST have a description paragraph above its feature table, capturing the what and why of the area.

**FR-PS-3** Every scope document MUST include a `Suggested Spec Order` section.

**FR-PS-4** On scope create, the skill MUST prompt for Type per FEAT with `feature` as the default proposal.

**FR-PS-5** On scope review, the skill MUST surface feature rows with an empty Type column and prompt the PM to fill them. Unresolved rows are allowed but flagged in Notes ("type unresolved").

**FR-PS-6** On every scope create and review, the skill MUST analyze scope state and **propose** a Suggested Spec Order (or changes to the current order) for PM review. The skill MUST NOT write or update the Suggested Spec Order section without explicit PM confirmation.

Proposal inputs — the skill uses judgment across these considerations, not a rigid formula:

- **Technical dependencies** — upstream FEATs spec before dependents
- **Engineering sequencing** — build-order prerequisites surface early
- **User / business value** — high-impact FEATs earlier
- **Delivery risk** — riskiest or most-uncertain items earlier so unknowns surface while there's time to adjust
- **External dependencies** — items blocked on external parties earlier (longer lead times)
- **Spikes** — research and discovery items earlier; their output informs downstream decisions
- **Prerequisite chains** — FEATs that unblock multiple others are higher priority
- **Spec readiness** — where an external spec or design already exists, spec effort is lower and items can slot in opportunistically

The skill frames its output as a product advisor guiding via engineering best practices and user-oriented value creation. The suggested order implicitly also suggests a development sequence, not only a specing sequence.

**FR-PS-7** When routing info arrives from other skills (Phase 2+), updates to existing scope entries MUST append to the Notes column rather than overwrite.

### Functional — product-feature

**FR-PF-1** The product-feature frontmatter MUST include a `type` field.

**FR-PF-2** Valid values for `type`: `feature` · `bug` · `tech` · `spike` · `other`, or any project-specific value the PM has introduced.

**FR-PF-3** On feature create, the skill MUST prompt for type before Q&A begins.

**FR-PF-4** The skill's Q&A MUST branch on type:
- `feature` — user stories, ACs, edge cases, design, happy and sad paths
- `bug` — reproduction steps, root cause hypothesis, affected areas, fix criteria, regression risk
- `tech` — technical rationale, migration plan, rollback strategy, success criteria, risk
- `spike` — research questions, time-box, expected outputs, decision criteria, follow-up actions
- `other` — adaptive based on PM direction

**FR-PF-5** If the PM changes a feature's type mid-spec, the skill MUST prompt: "Switching from {old} to {new} — re-run the relevant Q&A sections, or keep current content?"

### Non-Functional

**NFR-1** Custom project-specific types introduced by the PM MUST be preserved and accepted in both skills without revalidation once introduced.

**NFR-2** Suggested Spec Order proposal generation MUST complete within a single skill turn for scopes of up to 50 FEATs.

**NFR-3** No backwards-compatibility logic for untyped entries or untyped feature specs. Projects spawned from the template begin with typed FEATs from day one; migration of pre-existing untyped artifacts in already-initialized project repositories is out of scope and handled by ad-hoc PM action if needed.

---

## User Flows

1. **New scope creation** — PM runs `/product-scope {new-phase}`. Skill walks product areas with a description paragraph per area, creates feature tables in the canonical column order, prompts for Type per FEAT with `feature` as default, and proposes the initial Suggested Spec Order for PM confirmation. (FR-PS-1, FR-PS-2, FR-PS-3, FR-PS-4, FR-PS-6)

2. **Scope review on existing file** — PM runs `/product-scope {existing-phase}`. Skill surfaces feature rows missing Type and offers to fill them. Skill analyzes scope state and proposes Suggested Spec Order changes (or confirms current order); PM confirms before anything is written. (FR-PS-5, FR-PS-6)

3. **New feature spec** — PM runs `/product-feature FEAT-NNN`. Skill reads scope for existing type; if present, uses it; if missing, prompts before Q&A. Q&A branches per FR-PF-4. (FR-PF-1, FR-PF-3, FR-PF-4)

4. **Mid-spec type change** — Partway through a feature spec, PM says "this is actually a spike, not a feature." Skill prompts per FR-PF-5, then either re-runs spike-flavored Q&A or preserves current content as directed. (FR-PF-5)

---

## Acceptance Criteria

- [ ] Scope template includes a sample feature table under `## Product Areas / Epics` establishing the canonical column order (FR-PS-1)
- [ ] `product-scope/SKILL.md` A5 Aggressive Pre-Fill emits feature tables in the canonical column order (FR-PS-1)
- [ ] Scope template has product-area description paragraphs above feature tables (FR-PS-2)
- [ ] Scope template includes a Suggested Spec Order section (FR-PS-3)
- [ ] Feature template has `type` in frontmatter (FR-PF-1)
- [ ] `/product-scope` on create prompts for Type per FEAT with `feature` default (FR-PS-4)
- [ ] `/product-scope` on an existing file surfaces untyped rows and prompts the PM (FR-PS-5)
- [ ] `/product-scope` proposes Suggested Spec Order (or changes) for PM review on every create and review; never writes or updates the section without PM confirmation (FR-PS-6)
- [ ] `/product-feature` prompts for type before Q&A (FR-PF-3)
- [ ] `/product-feature` with `type: bug` runs bug-flavored Q&A, not feature Q&A (FR-PF-4)
- [ ] Mid-spec type change prompts per FR-PF-5
- [ ] PM can introduce a custom project-specific type and both skills accept it (NFR-1)

---

## Edge Cases

- **Scope has zero FEATs** — Suggested Spec Order section renders with a placeholder line ("No FEATs in scope yet — rerun `/product-scope` after adding features.") instead of an empty section.
- **PM declines to type a feature during scope review** — skill accepts a blank Type column but writes `type unresolved` into Notes for that row.
- **Feature file has empty `type` frontmatter** — skill prompts the PM on open; does not silently default.
- **PM declines proposed Suggested Spec Order changes** — skill respects and does not write. Current order remains as-is.
- **PM introduces a custom type mid-session** — accepted per NFR-1; offered as an option for subsequent FEATs in the same session.
- **Scope file pre-dates Phase 1 (no Type column present)** — on next review, skill detects missing column, rewrites the table structure to the canonical order per FR-PS-1, and prompts the PM to fill Type per row.

---

## Dependencies

- `product-scope` — primary subject of Phase 1 changes
- `product-feature` — primary subject of Phase 1 changes
- `product-backlog-import` — downstream consumer in Phase 2; reads Type vocabulary, canonical feature-table structure, and Notes schema established here
- `product-codebase-audit` — downstream consumer in Phase 3; also reads Type vocabulary and canonical feature-table structure to write typed FEATs during its route mode
- `project-initiation` — unchanged in Phase 1; Phase 4 updates the brownfield follow-up list to include backlog-import and codebase-audit
- `.claude/harness-artifacts-index.md` — unchanged across all phases (Phases 1-4 require no index modifications; the index is artifact-centric and all routing targets are already registered)

**Loop check**: No routing loops detected. Phase 1 introduces no new cross-skill silent writes. `product-scope` and `product-feature` remain PM-driven via explicit commands. Suggested Spec Order writes only happen after PM confirmation (FR-PS-6), so no self-referential auto-rewrite loop is possible.

---

## Out of Scope

- Retroactive migration of existing FEATs or scope entries to the new type system in already-initialized project repositories (out of scope for the template itself; handled by ad-hoc PM action in downstream projects if needed)
- Backlog-import integration with the type system — handled in Phase 2
- `project-initiation` updates to include `/product-backlog-import` and `/product-codebase-audit` in the brownfield follow-up list — handled in Phase 4
- Predefined registry of project-specific type vocabulary — PMs introduce types ad hoc; no curated list
- Type-based reporting, filtering, or analytics across scope — future enhancement
