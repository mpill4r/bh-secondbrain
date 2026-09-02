---
status: routing-preparation
source_tool: {linear | jira | notion | trello | asana | spreadsheet | other}
source_filter: {team/board/view/project identifier}
last_updated: {YYYY-MM-DD}
last_updated_by: auto — product-backlog-import
superseded_by:
---

# Backlog Import Plan — {Project}

> Called "the backlog import plan" or "the plan" in prose and skill messages.

## 1. Import Overview

**Source tool**: -tbd-
**Source filter**: -tbd-
**Import context**: {initial brownfield onboarding | mid-project catch-up | new work stream}
**Import date**: -tbd-

**Total items in source after filter**: -tbd-
**Items included in this plan**: -tbd-

| Status (source) | Count |
|-----------------|-------|
| -tbd- | -tbd- |

-tbd- (1-paragraph summary of what this backlog represents and why this import matters for the project right now)

## 2. Velocity & Delivery Insights

> 2-3 opinionated insights only. Each framed as an observation for PM consideration, not a conclusion. Each tagged with a routing target so route mode knows where to write it.

- **{Insight 1 title}** — *Routes to: {project-overview | project-lessons | project-assumptions | project-knowledge}*
  {1-3 sentences. Observation, suggested interpretation, and a prompt: "Does that match your experience, or was something else going on?"}

- **{Insight 2 title}** — *Routes to: {target}*
  {...}

- **{Insight 3 title}** — *Routes to: {target}*
  {...}

## 3. Proposed Scope Structure

> The core of the plan. Product areas with description paragraphs; FEATs grouped from source items with type, aggregate points, proposed status, description, Notes content, and grouping rationale. Every source item in scope has a FEAT ID — nothing falls through the cracks.

### Priority

#### {Product Area Name}

> {1-paragraph description — the what and why of this area.}

| Feature ID | Name | Type | Description | Status | Design Status | Linear IDs | Notes |
|------------|------|------|-------------|--------|---------------|------------|-------|
| FEAT-NNN | {Feature name} | {feature\|bug\|tech\|spike\|other} | {Capability-level description} | {defined\|drafted\|speced\|in development\|released} | {not needed\|needed\|in progress\|done} | {source IDs, comma-separated} | {aggregate points; who has context; key dates/signals; "extends FEAT-NNN" if applicable; blockers; grouping rationale} |

### Standard

(same structure)

## 4. Stale & Deferred Recommendations

> Items the skill recommends skipping or deferring, with per-item rationale. PM may override without explanation.

| Source ID | Title | Recommendation | Rationale |
|-----------|-------|----------------|-----------|
| -tbd- | -tbd- | {skip\|defer} | -tbd- |

## 5. Suggested Spec Order

> Sequencing recommendation with PM/engineering rationale per FEAT. Route mode writes this list into the Suggested Spec Order section of the target `product-scope-{phase-slug}.md` on PM confirmation.

1. **FEAT-NNN Feature Name** — rationale in 1-2 sentences (what it unblocks, delivery risk, spec readiness signals, strategic value)
2. ...

## 6. Type & Priority Mapping

> How source-tool type labels and priority signals were mapped onto the harness vocabulary (Phase 1). Preserved for audit and to inform future imports via update mode (FR-U-6).

### Type Mapping

| Source label | Harness type |
|--------------|-------------|
| -tbd- | {feature\|bug\|tech\|spike\|other or custom} |

### Priority Mapping

| Source priority | Harness tier |
|-----------------|-------------|
| -tbd- | {Priority\|Standard} |

### Product Area Mapping

| Source grouping (epic / project / label) | Harness product area |
|-----------------------------------------|---------------------|
| -tbd- | -tbd- |

## 7. Open Questions

> Duplicates, conflicts, items needing PM clarification, mixed estimation units, and other questions that should be resolved before or during route mode. Carried forward until resolved.

- -tbd-

## 8. Routing Plan

> Summary of where everything goes on PM confirmation. Route mode reads this as its write checklist.

- **`product-scope-{phase-slug}.md`** — new FEATs: {count}; updated FEATs: {count}; Notes appends: {count}
- **`product-scope-{phase-slug}.md` Suggested Spec Order** — populated from §5
- **`project-overview.md`** — velocity / capacity baseline from §2
- **`project-lessons.md`** — process lessons from §2 (if any)
- **`project-assumptions.md`** — blocked dependencies from §2 / §7 (if any)
- **`project-knowledge.md`** — new domain terms discovered during classification
- **`documents/index.md`** — entry for this plan
- **`project-daily`** — audit entry per write

> If the target `product-scope-{phase-slug}.md` does not exist at route time, the skill will propose phase metadata from source context for PM confirmation and autonomously create the scope file (FR-R-9).
