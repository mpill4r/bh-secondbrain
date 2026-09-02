---
status: routing-preparation
last_updated: {YYYY-MM-DD}
last_updated_by: auto — product-codebase-audit
classification: Codebase Analysis  # metadata-only (for documents/index.md classification column) — no routing consumer since Phase 3 removed the detection branch in project-document
source: internal
codebase_repos:
  - url: {repo-url}
    sha: {HEAD-sha}
codebase_snapshot_date: {YYYY-MM-DD}
superseded_by:
audience: harness AI first, PM second
---

# {Project} Product Baseline

## Purpose

This document captures the product-oriented baseline of the {project} codebase — what the product does, who it serves, what domain concepts exist, and what requirements, decisions, and gaps can be inferred from the code. It is designed for routing into harness artifacts via `/project-document`.

## Disclaimer

This baseline is inferred from code analysis and PM orientation context. Personas and user-facing interpretations are hypotheses to confirm with stakeholders — not ground truth. Confidence levels are marked on every inference.

## Scope Note

The codebase reveals *what* the system does and *how* — not *who* uses it, *why* they use it, or *what frustrates them*. User voice, UX quality, product roadmap intent, and compliance interpretations are captured as open questions (§9), not fabricated.

---

## 1. Product Summary

-tbd-

## 2. Inferred Personas

| Persona | Evidence in Code | Likely Role | Confidence |
|---------|-----------------|-------------|------------|
| -tbd- | -tbd- | -tbd- | -tbd- |

> All personas are inferred from code — pending stakeholder validation.

**Pain Points**: -tbd- (code cannot reveal subjective user experience)
**Success Looks Like**: -tbd- (code cannot reveal subjective user experience)

**Personas not visible in code but likely to exist:**
- -tbd-

### Role × Capability Matrix

| Role | {Epic 1} | {Epic 2} | {Epic 3} | ... |
|------|----------|----------|----------|-----|
| -tbd- | -tbd- | -tbd- | -tbd- | -tbd- |

> Access levels: Full · Manage · View · None · Sign-Off. Inferred from permission definitions, route guards, UI conditionals.

## 3. Architectural & Technical Boundaries (Product Implications)

> Format: **fact** → **why a PM should know**. Technical facts appear ONLY when they have a direct product implication.

1. -tbd-

## 4. Domain Language

| Term / Concept | Description | Specificity |
|---------------|-------------|-------------|
| -tbd- | -tbd- | -tbd- |

> Specificity: `project-specific` (coined by this project/team) · `domain-standard` (recognized in the industry). All entries route to project-knowledge.

## 5. Product Rules & Requirements (PR-NNN)

### {Rule Category}

| ID | Rule / Requirement | Routing | Addressed in | vs. Existing Harness | Source |
|----|-------------------|---------|-------------|---------------------|--------|
| PR-001 | -tbd- | -tbd- | -tbd- | -tbd- | -tbd- |

> Routing: `REQ` → product-requirements · `Knowledge` → project-knowledge. Addressed in: FEAT-NNN references (REQ entries only).

## 6. Decisions & Assumptions (DA-NNN)

| ID | Decision / Assumption | Rationale (Observable in Code) | vs. Existing Harness | Source |
|----|----------------------|-------------------------------|---------------------|--------|
| DA-001 | -tbd- | -tbd- | -tbd- | -tbd- |

## 7. Product Gaps & Anomalies

### Deferred Scope Candidates

| Item | Epic | Evidence | Type |
|------|------|----------|------|
| -tbd- | -tbd- | -tbd- | -tbd- |

> Type: `deferred` (partial code exists) · `future-idea` (no code signal). Routes to product-scope Deferred Scope / Future Ideas.

### General Anomalies

- -tbd-

### Failure Modes

- -tbd-

## 8. Derived Epics & Features

| Epic | Feature ID | Name | Type | Description | Status | Design Status | Linear IDs | Notes |
|------|-----------|------|------|-------------|--------|---------------|------------|-------|
| -tbd- | FEAT-NNN | -tbd- | {feature\|bug\|tech\|spike\|other} | -tbd- | -tbd- | -tbd- | | -tbd- |

> Columns match the canonical Phase 1 scope column order (Linear IDs left blank for code-derived FEATs unless imported from backlog).
> Description: multi-sentence — what it does + key rules/complexity + inline FEAT-NNN dependency refs.
> Type: default `feature`; `tech` when the FEAT is infrastructural; other Phase 1 vocabulary values accepted.
> Status: `released` · `in development` · `defined`. Design Status: `unknown`.

## 9. Open Questions

| # | Question | Owner | Impact |
|---|----------|-------|--------|
| 1 | -tbd- | -tbd- | -tbd- |

> Owner: Client · Engineering · Legal · PM. Impact: High · Medium · Low.
