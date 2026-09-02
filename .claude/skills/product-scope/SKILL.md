# product-scope — Skill Logic

> The phase-level roadmap and delivery tracker. One file per phase. Defines what to deliver, in which order, by when, and tracks how delivery is progressing. Primary alignment document between PM, engineering, and client. Load-bearing role: `project-daily` derives RAG status and current priority from this artifact's milestones, feature completion, and scope completion percentage.

---

## When This Skill Runs

This skill runs in four contexts:
- **PM invokes `/product-scope`** → Create or Update (Section A/B)
- **Receives routed content from meetings/documents** → Inbound Routing (Section C)
- **Prompt to create** fires when phasing exists but no scope file matches (Section D)

---

## A. Creation Mode

### A1. Load Context

Read `product/problem-space/product-brief.md` and `product/problem-space/product-requirements.md` (core dependencies). Read `project/management/project-assumptions.md` for Decided items relevant to scope decisions. Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match the current task. If any file does not exist, skip silently.

### A2. Mode Detection

If PM provides a phase slug and no file exists at `product/solution-space/product-scope-{slug}.md`, enter CREATE mode. If the file exists, enter UPDATE mode (Section B). If PM does not specify a slug, list existing scope files and ask PM which to work on or offer to create a new one.

### A3. PM Input

PM provides: phase slug, and optionally phase type (standard or PoC). If PM provides additional context about the phase (goals, epics, constraints), incorporate it.

### A4. Multi-Phase Check

When creating a new phase while other scope files already exist, read all existing scope files and ask the PM how the new phase relates to existing ones:

1. **Relationship**: "Phase 1 exists (active, 65% complete). Is Phase 2 independent, or should I pull in unfinished scope from Phase 1?"
2. **Scope transfer**: If PM wants to transfer scope, list Phase 1's Deferred Scope (Section 6), unfinished features from Section 3, and Future Ideas (Section 7). PM picks which items to bring into Phase 2. Transferred features retain their FEAT-NNN IDs. Future Ideas promoted to features get new FEAT-NNN IDs.
3. **Phase 1 status**: If scope is being transferred, ask: "Should Phase 1 remain active alongside Phase 2, or close it?" If PM closes Phase 1, unfinished features not transferred to Phase 2 move to Phase 1's Deferred Scope with rationale "Phase closed — not transferred to Phase 2."

Multiple phases can be `active` simultaneously — phases are independent. Each phase has its own Scope Status, milestones, and completion %.

### A5. Aggressive Pre-Fill

Pre-fill every section from available context:

- **Section 1 (Scope Status)**: Auto-calculated from Section 3 feature tables. At creation, shows the initial counts and completion %.
- **Section 2 (Phase Purpose & Goals)**: From `product-brief` Section 8 (the matching phase row — focus and key outcomes) and Sections 1-2 (north star and problem definition). For PoC phases, include hypotheses and validation approach as part of the purpose.
- **Section 3 (Product Areas / Epics)**: From `product-requirements` Open items — group by topic into proposed epics, propose Priority/Standard assignment based on requirements priorities. Each proposed epic gets an initial feature list derived from requirements. For every product area, write a 1-paragraph description (the what and why of the area) above the feature table. Emit every feature table in the canonical column order: `Feature ID | Name | Type | Description | Status | Design Status | Linear IDs | Notes`. For each FEAT, prompt the PM for Type with `feature` as the default proposal; valid values are `feature` · `bug` · `tech` · `spike` · `other`, or any project-specific type the PM has previously introduced in this project. If the PM declines to set a Type, leave it blank and append `type unresolved` to that row's Notes. Custom types introduced by the PM are accepted without revalidation for the rest of the session and offered as an option for subsequent FEATs. FEAT-NNN IDs assigned sequentially. Check existing scope files for the highest FEAT-NNN and continue from there. IDs are never reused.
- **Suggested Spec Order section**: After Section 3 is pre-filled, analyze the scope and **propose** an ordered list of FEATs for PM review. Use judgment across: technical dependencies (upstream FEATs spec before dependents), engineering sequencing (build-order prerequisites surface early), user/business value (high-impact FEATs earlier), delivery risk (riskiest or most-uncertain items earlier so unknowns surface in time), external dependencies (items blocked on external parties earlier for longer lead times), spikes (research earlier; its output informs downstream decisions), prerequisite chains (FEATs that unblock multiple others are higher priority), and spec readiness (where an external spec or design already exists, slot opportunistically). Frame the output as a product advisor guiding via engineering best practices and user-oriented value creation. Each entry: `**FEAT-NNN Feature Name** — rationale in 1-2 sentences (what it unblocks, delivery risk, spec readiness signals, strategic value)`. Never write or update this section without explicit PM confirmation. If scope has zero FEATs, render the placeholder line "No FEATs in scope yet — rerun `/product-scope` after adding features." instead of an empty section.
- **Section 4 (Development Estimate)**: `-tbd-` at creation. Include the reminder note: "PM: Estimates not yet provided. Get engineering input and update via `/product-scope`."
- **Section 5 (Release Plan)**: From `product-brief` Section 8 target release date. Scaffold a milestones table with "Scope finalized" as the first entry (status: Done).
- **Section 6 (Deferred Scope)**: Empty at creation.
- **Section 7 (Future Ideas)**: Empty at creation.

Fields without reliable data: `-tbd-`. Uncertain fields: `> Needs confirmation — [reason]`. Never fabricate.

### A6. PM Review

Present the full pre-filled document to PM for review. PM can adjust any section — regroup epics, change Priority/Standard assignments, rename features, add or remove items — before confirming the initial write.

### A7. After Writing

- Set frontmatter: `phase_slug: {slug}`, `target_start: {date or -tbd-}`, `target_release: {date or -tbd-}`, `last_updated: {today}`, `last_updated_by: manual — /product-scope`.
- Log audit entry to `project-daily`: `[MANUAL] product-scope-{slug} created via /product-scope ({date})`.
- If `project-daily` does not exist, create it first.
- If requirements from `product-requirements` were mapped to features, update those requirements' status to `Processed` with `Addressed in: product-scope-{slug}.md`.
- Run outbound routing (Section E).
- Run routing check (Section F).

---

## B. Update Mode

### B1. Load Context

Same as A1. Additionally, read the target `product/solution-space/product-scope-{slug}.md` (full file).

### B2. Health Summary

Present on entry: Scope Status (completion % and feature count breakdown), milestone status summary, stale estimate warnings (if Development Estimate is `-tbd-` and phase is `active`), untyped-row count (rows in Section 3 with an empty Type column), last update date. Then respond to PM.

If the scope file pre-dates Phase 1 and its feature tables lack the Type column entirely, detect the missing column, rewrite the table structure in place to the canonical column order (`Feature ID | Name | Type | Description | Status | Design Status | Linear IDs | Notes`) preserving all existing values, and leave Type blank per row. Flag the rewrite to the PM alongside the untyped-row count.

### B2a. Untyped Rows Prompt

If any rows in Section 3 have an empty Type column, surface them as a batch: "{N} features are missing Type: [FEAT-NNN, FEAT-NNN, ...]. Fill now?" Propose a default of `feature` for each but let the PM override per row. Valid values: `feature` · `bug` · `tech` · `spike` · `other`, or any project-specific type previously introduced. If the PM declines to type a given row, leave it blank and append `type unresolved` to that row's Notes (if not already present). Custom types introduced mid-session are accepted without revalidation and offered as options for subsequent prompts in the same session.

### B2b. Suggested Spec Order Proposal

Analyze current scope state and propose either (a) an initial Suggested Spec Order if the section is empty, or (b) specific changes to the current order (reorderings, additions of newly-added FEATs, removals of deferred ones). Use judgment across: technical dependencies, engineering sequencing, user/business value, delivery risk, external dependencies, spikes, prerequisite chains, spec readiness. Frame as a product advisor — each proposed entry or change gets a 1-2 sentence rationale. Present the proposal to the PM and ask for confirmation, adjustments, or decline. Never write or update the Suggested Spec Order section without explicit PM confirmation. If the PM declines, the current order remains as-is. If scope has zero FEATs, the section renders the placeholder line "No FEATs in scope yet — rerun `/product-scope` after adding features." instead of an empty section.

### B3. Conversational Interaction

Interaction is conversational — PM types requests in plain language. Infer intent:

- **Add epic**: Propose the epic header with description, ask PM for Priority or Standard tier.
- **Add feature**: Propose the feature entry in the appropriate epic's table (canonical column order). Assign next FEAT-NNN ID (check all scope files for highest, increment). Prompt for Type with `feature` as default; accept any custom project-specific type the PM has introduced in this project. If the PM declines, leave blank and append `type unresolved` to Notes. Ask PM to confirm.
- **Change priority tier**: Move epic or feature between Priority and Standard.
- **Update feature status**: PM indicates a feature has progressed (e.g., "FEAT-003 is now in development"). Update the status. If moving to `speced`, check whether a feature spec file exists at `product/solution-space/features/FEAT-003-*.md` and warn if not found: "No feature spec found for FEAT-003. Mark as speced anyway?"
- **Update design status**: Update the Design column for a feature (`not needed` / `not started` / `in progress` / `done`).
- **Update estimates**: PM provides per-epic or overall estimates for Section 4.
- **Defer scope**: Move epic or feature from Section 3 to Section 6 (Deferred Scope) with rationale. If an entire epic is deferred, all its features move too. FEAT-NNN IDs are preserved. If deferred items had linked requirements, ask: "FEAT-NNN was linked to REQ-NNN. Mark that requirement as Deferred too?"
- **Promote deferred items**: Move items from Section 6 back to Section 3. Restore with preserved FEAT-NNN IDs and ask PM which priority tier.
- **Add future idea**: Add to Section 7 as a simple list entry with date context.
- **Update milestones**: Add, update status, or modify milestones in Section 5. Status values: `Done` / `Upcoming` / `At Risk` / `Missed`.
- **Phase status change**: PM can promote `draft` to `active` or `active` to `completed`. Never auto-promote. For completion, check milestone status and warn if any milestones are `At Risk` or `Missed`: "{N} milestones are at risk. Still mark as completed?" PM can confirm with a note.

### B4. Premature Phase Close

When PM marks `active → completed` while features are still in progress, warn: "{N} features are not yet released. Transfer remaining scope to another phase, move to Deferred Scope, or close as-is?" PM chooses per feature or in bulk.

### B5. Writing Changes

Before writing any changes, show a diff and ask PM to confirm. Section 1 (Scope Status) recalculation is included in the diff. End every session with "Anything else to add or update?"

### B6. After Writing

- Update frontmatter `last_updated` and `last_updated_by: manual — /product-scope`.
- Log audit entry to `project-daily`: `[MANUAL] product-scope-{slug} updated via /product-scope — {what changed} ({date})`.
- If `project-daily` does not exist, create it first.
- If requirements were newly mapped to features, update those requirements' status to `Processed` with `Addressed in: product-scope-{slug}.md`.
- Run outbound routing (Section E).
- Run routing check (Section F).

---

## C. Inbound Routing (from meetings and documents)

`project-meeting`, `project-document`, and `product-feature` route scope-relevant content to `product-scope` via PM-confirmed routing review (for meetings/documents) or silent status sync (for feature specs). The routing review is owned by the originating skill — this skill receives the writes, it does not initiate them.

### Routable content

- Epic-level scope decisions → Section 3 (from meetings/documents)
- Feature identification → Section 3 (assign FEAT-NNN IDs for new features; always include Type — propose `feature` as default if unknown; emit row in canonical column order; populate Notes from source content)
- Estimation data → Development Estimate section (from meetings/documents)
- Timeline signals → Release Plan section (from meetings/documents)
- Dependency information → Release Plan Dependencies (from meetings/documents)
- Deferral decisions → Deferred Scope section (from meetings/documents)
- Feature status updates → Section 3 feature table (from `product-feature`: when a feature spec is created, FEAT-NNN status updates to `drafted` and Description column is populated from Feature Summary; when marked `speced`, status updates to `speced`; status changes to `in development` or `released` update accordingly)
- Notes-column updates for existing FEATs (aggregate points, blockers, relationships, context) → **append** to the existing Notes cell with a newline separator, never overwrite. Prefix each appended entry with a short source tag like `[{source-slug} {date}]` so the audit trail is visible in the cell.

### After each routed write

- Recalculate Section 1 (Scope Status) from Section 3 feature tables.
- Update frontmatter `last_updated` and `last_updated_by: auto — {source skill} routing`.
- Log audit entry to `project-daily`: `[AUTO] product-scope-{slug} — {section} updated from {source-slug} ({date})`.
- If `project-daily` does not exist, create it first.
- If `product-scope-{slug}.md` does not exist when a routing write is attempted, create the file from template with all sections present (Section 3 empty, Section 1 showing 0%, Suggested Spec Order rendered with the zero-FEATs placeholder), then write the routed content. Log: `[AUTO] product-scope-{slug} — file created and {section} updated from {source-slug} ({date})`.
- If routed content includes new features mapped to requirements from `product-requirements`, update those requirements' status to `Processed` with `Addressed in: product-scope-{slug}.md`. If `product-requirements.md` does not exist, skip silently.
- Preserve all existing content exactly. Only targeted sections and fields are modified.
- Run outbound routing (Section E).

---

## D. Prompt to Create

When `product-brief` **High-Level Phasing** section is populated with phase data but no corresponding `product-scope-{slug}.md` file exists, suggest creating it. This check happens during `product-brief` enrichment sessions and at session start (via `project-daily` context). The prompt is: "Phase 1 is defined in product-brief but has no scope document yet. Want to create it now via `/product-scope {slug}`?"

---

## E. Outbound Routing (after every write)

After every write (creation, update, or inbound routing), silently route relevant content outbound. If a target file does not exist, skip the routing silently.

1. **`product-brief` High-Level Phasing section**: Update the corresponding phase row (focus, target release, key outcomes) ONLY if these fields actually changed compared to the current High-Level Phasing content. This is the bidirectional sync — gated on actual content changes, not on any write event. If nothing changed in the phasing data, do NOT write to `product-brief`.
2. **`client-overview` Active Initiatives & Project History section**: Add or update the phase entry with: phase name, timeline, status, one-line focus. If `client-overview.md` does not exist, skip silently.
3. **`project-daily` Key Events**: Log milestone key events when: (a) scope document created, (b) phase status changed (draft→active, active→completed), (c) significant scope change (epic added/removed from Priority, feature count changed significantly).
4. **`project-daily` Audit Log**: Standard audit entry for every write.

Each outbound write is logged as a separate audit entry to `project-daily`.

---

## F. Routing Check (end of session)

At the end of every `/product-scope` session (before the final write), scan for decisions and assumptions that emerged — priority trade-offs, deferral rationale, estimation assumptions, timeline commitments, dependency assumptions. Present any unrouted items: "These decisions/assumptions emerged during our session — route to project-assumptions? [list]." PM confirms, skips, or adjusts. Confirmed items are written to `project-assumptions.md` with source `product-scope session ({date})`. If `project-assumptions.md` does not exist, skip silently.

---

## G. Scope Status Derivation

Section 1 is auto-derived on every write. Recalculate from Section 3 feature tables.

**Feature counts**: Count features by status across all epics in Section 3. Features in Section 6 (Deferred Scope) are excluded.

**Completion % formula** (weighted average):

| Status | Weight |
|--------|--------|
| defined | 5% |
| drafted | 15% |
| speced | 45% |
| in development | 75% |
| released | 100% |

`Scope Completion = sum(weight per feature) / total features`

If no features are defined → 0%.

PM never edits Section 1 directly. If PM attempts to, explain that it is auto-calculated from feature status in Section 3.

---

## Rules

- **All sections always present**: Scope Status, Phase Purpose & Goals, Product Areas / Epics, Suggested Spec Order, Development Estimate, Release Plan, Deferred Scope, and Future Ideas — all exist, even if empty at creation.
- **`-tbd-` over fabrication**: Unknown fields are always `-tbd-`, never guessed.
- **FEAT-NNN IDs are project-wide sequential**: Check all existing scope files for the highest FEAT-NNN and continue from there. IDs are never reused, even after deferral or restoration.
- **Canonical feature-table column order**: Every feature table (on create, update, routed write, or migration of pre-Phase-1 files) uses the column order `Feature ID | Name | Type | Description | Status | Design Status | Linear IDs | Notes`. No other orderings accepted.
- **Product-area descriptions always present**: Each product area in Section 3 has a 1-paragraph description above its feature table. Never skip.
- **Type vocabulary**: Valid Type values are `feature` · `bug` · `tech` · `spike` · `other`, or any project-specific type the PM has previously introduced in this project. Custom types are accepted and preserved without revalidation once introduced in a session, and offered as options for subsequent FEATs in that session.
- **Type prompts on create and review**: On create, prompt for Type per FEAT with `feature` as default. On review, surface rows with an empty Type column and prompt the PM. If the PM declines to type a row, leave it blank and append `type unresolved` to Notes.
- **Suggested Spec Order is PM-confirmed only**: On every create and review, analyze scope and propose an order (or changes). Never write or update the Suggested Spec Order section without explicit PM confirmation. If the PM declines, the current order remains as-is.
- **Spec Order proposal must complete within one skill turn** for scopes up to 50 FEATs.
- **No backwards-compatibility logic for untyped legacy entries**: Projects spawned from the template begin typed from day one. Migration of pre-existing untyped artifacts in already-initialized projects is ad-hoc PM action, not automatic; however, pre-Phase-1 scope files with feature tables missing the Type column are restructured to the canonical column order in place on next review, with Type left blank per row for the PM to fill.
- **Notes updates append, never overwrite**: Routed writes (from Phase 2+ backlog-import, codebase-audit, meetings, documents) that target the Notes column append a new line with a source tag like `[{source-slug} {date}]`. Existing Notes content is preserved exactly.
- **Feature status lifecycle is strict**: `defined` → `drafted` → `speced` → `in development` → `released`. No skipping steps.
- **Design status is metadata**: Tracked separately (`not needed` / `not started` / `in progress` / `done`). Does not factor into scope completion %. Provides visibility into design readiness alongside delivery status.
- **Two-tier prioritization**: Priority (deliver first) and Standard (deliver after). Both are committed scope — everything is expected to be delivered. Priority determines delivery order.
- **Section 1 is always auto-derived**: PM never edits it directly. Recalculated on every write from Section 3 feature tables.
- **Deferred items are excluded from Scope Status**: Features moved to Section 6 do not count toward completion %.
- **Epics are deferred, never deleted**: If PM wants to delete an epic, move it to Section 6 (Deferred Scope). Maintains audit trail.
- **Phase status never auto-promotes**: `draft → active` and `active → completed` require explicit PM confirmation.
- **Feature-level detail redirects to product-feature**: If PM starts providing acceptance criteria, user stories, or detailed specifications for a feature, redirect: "That level of detail belongs in a product-feature spec. Want me to create one via `/product-feature`?"
- **Estimation follows PM granularity**: Range estimates for epics are always valid. Never force granularity the PM does not have.
- **Internal estimation data**: Section 4 is marked `> Internal — do not share with client.`
- **Bidirectional sync with product-brief is gated**: Write to product-brief High-Level Phasing only when phase focus, target release, or key outcomes actually changed — preventing re-trigger loops.
- **Preserve existing content**: When writing, preserve all existing content exactly. Only targeted sections and fields are modified.
- **Machine-readable format**: Frontmatter, milestone tables, feature status values, and Scope Status section must be consistently formatted so that `project-daily` and `project-weekly` can parse them reliably.
- **PM confirms all manual writes**: Always show diff and wait for confirmation during `/product-scope` sessions. Never auto-write.
- **Audit everything**: Every write (manual and routed) logs to `project-daily`. If `project-daily` does not exist, create it first.
- **No product-brief edge case**: If `product-brief` does not exist at creation, proceed with whatever context is available. Sections that rely on it are sparsely populated. Note: "`product-brief` does not exist yet — consider running `/product-brief` first for richer context."
- **No open requirements edge case**: If no open requirements exist, Section 3 is created with empty Priority and Standard tiers. PM adds epics and features manually.
