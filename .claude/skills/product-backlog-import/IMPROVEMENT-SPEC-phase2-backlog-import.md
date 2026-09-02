---
status: wip
last_updated: 2026-04-17
owner: Jan Koscelansky
phase: Phase 2
---

# Phase 2 — Backlog-Import Skill Rewrite

## Overview

Phase 2 rewrites `product-backlog-import` from a data reformatter (here's your backlog in a different table format) into a PM strategy advisor (here's how I'd structure this work for delivery — tell me where I'm wrong).

The skill uses harness context — product brief, existing scope and features, open requirements, assumptions, domain knowledge, project overview — to propose an opinionated scope structure. The PM's job becomes editorial (adjust, approve), not architectural (figure out the structure from scratch).

The skill maintains a per-import plan document at `documents/internal/backlog-import/YYYY-MM-DD-{project-slug}-backlog-import.md` — called "the backlog import plan" in prose. The plan has two lifecycle states: `routing-preparation` (PM still reviewing) and `routing-done` (PM confirmed, writes flushed to harness artifacts).

The skill runs in two modes. Import mode produces the plan; route mode reads it back, confirms routing with the PM, and writes directly to harness artifacts. Multiple route-mode sessions on the same plan are valid — the PM iterates before giving final go-ahead.

Phase 2 depends on Phase 1 (type system in product-scope and product-feature). It does not ship without Phase 1.

**Skill location:**
- Command: `.claude/commands/product-backlog-import.md`
- Skill logic: `.claude/skills/product-backlog-import/SKILL.md`
- Template: `.claude/skills/product-backlog-import/TEMPLATE.md`

Related specs: `IMPROVEMENT-SPEC-phase1-type-system.md`, `IMPROVEMENT-SPEC-phase3-codebase-audit.md`, `IMPROVEMENT-SPEC-phase4-integration.md`.

---

## Commands

| Command | When to use |
|---------|-------------|
| `/product-backlog-import` | Start a new import — orientation, harness context load, backlog access, classification, plan document creation. |
| `/product-backlog-import {file-path}` | Same as above but with a file export provided upfront; access method inferred as "file export." |
| `/product-backlog-import route` | Resume or initiate routing from an existing plan document. Reloads harness context, reads plan in its current state (including PM edits), runs confirmation, writes to harness on explicit PM confirmation. |

One command with mode disambiguation based on the argument. No separate create/update/route commands.

---

## User Roles

| Role | Interaction | Key Need |
|------|-------------|----------|
| PM | Runs import, reviews the proposed plan area by area, adjusts, confirms routing | An opinionated proposal to edit rather than architect; clear loop between import and routing; ability to iterate across sessions |
| Other skills | `product-scope`, `project-overview`, `project-lessons`, `project-assumptions`, `project-knowledge`, `documents/index.md`, `project-daily` receive routed writes | Consistent write format from a single upstream source |
| Source backlog tool (Linear, Jira, Notion, etc.) | Read-only access | Never modified — no write-back permitted |

---

## Document Structure

**Path**: `documents/internal/backlog-import/YYYY-MM-DD-{project-slug}-backlog-import.md`

**Created**: by PM via `/product-backlog-import` — a new plan per import session. Not created by `project-initiation`.

8 sections, all always present. Sections with no relevant content include a note explaining why. In prose and in skill messages, called "the backlog import plan" or "the plan."

| # | Section | Notes |
|---|---------|-------|
| 1 | Import Overview | Source, filter, item counts, import context (brownfield onboarding / catch-up / new work stream) |
| 2 | Velocity & Delivery Insights | 2-3 opinionated insights from completed items and backlog patterns; each tagged with a routing target |
| 3 | Proposed Scope Structure | Core section — product areas with description paragraphs, FEATs with type + grouped source items + aggregate points + proposed status + description + Notes content + grouping rationale |
| 4 | Stale & Deferred Recommendations | Items skill recommends skipping or deferring, with per-item rationale; PM may override |
| 5 | Suggested Spec Order | Sequencing recommendation with professional PM/engineering rationale per FEAT |
| 6 | Type & Priority Mapping | How source types and priorities were mapped to harness types — preserved for audit and future imports |
| 7 | Open Questions | Duplicates, conflicts, items needing PM clarification; carried forward until resolved |
| 8 | Routing Plan | Summary of where everything goes on PM confirmation (FEATs → phases, insights → artifacts, terms, blockers, lessons) |

**Frontmatter:**
```yaml
---
status: routing-preparation | routing-done
source_tool: {linear | jira | notion | spreadsheet | other}
source_filter: {team/board/view/project identifier}
last_updated: YYYY-MM-DD
last_updated_by: auto — product-backlog-import
superseded_by: {filename-if-replaced-by-later-import}
---
```

### Type vocabulary

Phase 2 writes the types established in Phase 1: `feature` · `bug` · `tech` · `spike` · `other`, plus any PM-introduced project-specific types. During classification, the skill maps source-tool type labels onto this vocabulary with PM confirmation (see FR-C-4).

---

## Requirements

### Functional — Context Loading

**FR-CL-1** Before orientation, the skill MUST silently scan `documents/internal/backlog-import/` for prior plan documents. This is the filesystem probe used by the defensive check (FR-D-1 through FR-D-4). No other context reading happens at this stage.

**FR-CL-2** After orientation, in import mode, the skill MUST read the following harness context files. Files that do not exist are skipped silently.

- `product/problem-space/product-brief.md` — strategic context, phasing direction, personas, goals
- All `product/solution-space/product-scope-*.md` — existing scope, released FEATs, epic structure, highest existing FEAT-NNN ID
- All `product/solution-space/features/FEAT-*.md` — lightweight read (frontmatter + Section 1 only) to support "extends FEAT-NNN" detection and avoid duplicate FEAT IDs
- `product/problem-space/product-requirements.md` — open requirements that may map to backlog items
- `project/management/project-assumptions.md` — Decided items and blocked dependencies that shape classification
- `project/management/project-knowledge.md` — domain terms for interpreting source item titles correctly
- `project/management/project-overview.md` — current phase, project RAG status, delivery rhythm

The skill MUST tailor the depth of each read based on the PM's orientation answers. E.g. "new work stream" reads existing scope shallower than "mid-project catch-up"; "initial brownfield onboarding" weights product-brief heavier.

**FR-CL-3** On route mode entry, the skill MUST re-read the same harness context files (FR-CL-2). Context may have changed between import and route sessions; the skill does not trust the import-time snapshot.

**FR-CL-4** The loaded harness context MUST inform: FEAT grouping, type mapping recommendations, priority tier assignment, relationship detection with released features, velocity insight selection, Suggested Spec Order rationale, and routing target validation.

### Functional — Orientation

**FR-O-1** Orientation MUST ask exactly three questions, in a single conversational message:
1. What is the context / reason for this import? (initial brownfield onboarding / mid-project catch-up / new work stream)
2. What tool is the backlog in? (Linear / Jira / Notion / Trello / Asana / spreadsheet / other)
3. Anything the PM wants to specify upfront, or defer specifics until the skill has explored the backlog?

**FR-O-2** The skill MUST infer access method from the tool answer. Preference order: MCP integration (Linear, Jira/Atlassian, Notion) → file export → pasted content. The skill states its choice; it does not ask.

**FR-O-3** MCP fallback chain MUST kick in silently on auth failure: skill informs PM once that MCP failed and offers export or paste as the next step.

**FR-O-4** Filter / board / view / project selection MUST NOT be asked before the skill has accessed the backlog.

**FR-O-5** Completed-items handling MUST NOT be asked upfront. It is decided during the classification step per the 4-tier approach (FR-C-5).

### Functional — Silent Defensive Check

**FR-D-1** The pre-orientation filesystem scan (FR-CL-1) populates the defensive check.

**FR-D-2** If the PM said "initial brownfield onboarding" AND a prior plan exists, the skill MUST surface the contradiction: "You mentioned initial onboarding but I found a prior import from {date}. Did you mean update mode, or fresh re-import?"

**FR-D-3** If the PM said "mid-project catch-up" AND no prior plan exists, the skill MUST surface: "You mentioned catch-up but I don't see a prior import — is this the first harness import?"

**FR-D-4** Absent a contradiction between PM-stated context and filesystem state, the skill MUST NOT surface this check to the PM.

### Functional — Exploration and Filter Selection

**FR-E-1** After backlog access, the skill MUST explore available structure (projects, boards, views, filters, statuses) before proposing any scope.

**FR-E-2** Filter questions MUST use real, concrete options discovered during exploration. Example: "Found 4 Linear teams: VAD-Phase1, VAD-Phase2, VAD-Internal, VAD-Ops. Which?"

**FR-E-3** Before deep analysis, the skill MUST state scope and confirm: "I'll pull {specific filter} from {tool} — approximately {N} items across {M} statuses. Proceed to full analysis?"

### Functional — Classification and Grouping

**FR-C-1** The skill MUST produce a full proposed scope structure, not a list of items for the PM to organize.

**FR-C-2** Every item in the Proposed Scope Structure MUST have a FEAT ID — no items fall through the cracks.

**FR-C-3** Small or thematically-related items MUST be grouped into umbrella FEATs. The skill MUST explain each grouping; the PM MUST be able to split, merge, or move items during the confirmation session. The plan document MUST be updated live as the PM adjusts.

**FR-C-4** Every FEAT in the Proposed Scope Structure MUST have a type (per Phase 1 vocabulary). Source-tool type labels MUST be mapped to harness types with PM confirmation, and the mapping MUST be recorded in Section 6 of the plan.

**FR-C-5** Completed items MUST be handled via a 4-tier approach:
1. Summary stats always captured in Velocity & Delivery Insights
2. Significant capabilities not already represented in scope — imported as `released` FEATs with PM confirmation
3. Items related to active FEATs — noted as context, not imported separately
4. Everything else — skipped by default; PM may override

The skill MUST present this as a concrete recommendation: "Of {N} completed items, I'd import {X} as released FEATs, note {Y} as context on active features, and skip {Z} — agree?"

**FR-C-6** Product areas in the proposed structure MUST include description paragraphs per Phase 1 FR-PS-2.

**FR-C-7** Priority / Standard tier assignment MUST use backlog priority signals, dependency analysis, and in-progress signals.

**FR-C-8** Items that enhance released features MUST receive their own FEAT IDs, with "extends FEAT-NNN" recorded in the Notes column.

### Functional — Velocity & Delivery Insights

**FR-V-1** The skill MUST generate 2-3 opinionated insights per import — not an exhaustive dump. Insight types include: delivery velocity, type distribution (new features vs. maintenance work), priority accuracy, blocker / dependency patterns, team capacity signals.

**FR-V-2** Each insight MUST be framed as an observation for PM consideration, not a conclusion — e.g. "This pattern suggests X — does that match your experience, or was something else going on?"

**FR-V-3** Each insight MUST be tagged with a routing target:

| Insight type | Routes to |
|---|---|
| Velocity / capacity baseline (including new-vs-maintenance distribution) | project-overview |
| Process lessons | project-lessons |
| Blocked dependencies | project-assumptions |
| Team working patterns | project-knowledge |

**FR-V-4** Insight selection MUST be context-aware: brownfield onboarding produces different insights than mid-project catch-up.

### Functional — Stale Item Handling

**FR-S-1** Staleness MUST be assessed relative to the project's own cadence (calibrated via the orientation question about backlog maintenance, or observed activity). Hardcoded time thresholds are forbidden.

**FR-S-2** Stale / deferred recommendations MUST include per-item rationale. PM may override any recommendation without explanation.

**FR-S-3** The skill MUST detect duplicates, blocked-on-external-dependency items, underspecified-and-deprioritized items, and items superseded by newer work — and graduate its recommendation accordingly (skip, defer, or keep).

### Functional — Metadata Preservation (Notes column)

**FR-M-1** Backlog metadata MUST be condensed into the single Notes column on the scope feature table (per Phase 1 FR-PS-1). Contents include: aggregate story points, who has context, key dates/signals, relationship to existing FEATs, import-specific context, blockers.

**FR-M-2** Individual source-item descriptions MUST NOT be written into scope — they remain in the plan document only, useful when PM later runs `/product-feature` to spec the FEAT.

**FR-M-3** Source statuses, creation dates, and labels MUST be consumed during classification and then discarded — not persisted to scope.

**FR-M-4** Estimation units (story points, hours, t-shirt sizes) MUST be preserved as-is. No unit conversion.

### Functional — Plan Document (Import Mode Output)

**FR-P-1** The plan document MUST be written to `documents/internal/backlog-import/YYYY-MM-DD-{project-slug}-backlog-import.md`. The directory MUST be created if it does not exist.

**FR-P-2** The plan MUST include all 8 sections from Document Structure. Sections with no content MUST include a note explaining why.

**FR-P-3** Frontmatter MUST include `status: routing-preparation` on initial creation.

**FR-P-4** The plan MUST be written in English regardless of source tool language. Non-English titles and descriptions MUST be translated; originals preserved in parentheses only if the PM requested it during orientation.

**FR-P-5** If the session ends before PM confirms the proposed structure, the skill MUST surface clear resume guidance: "The plan is saved at `{path}` with status `routing-preparation`. When you're ready to continue, run `/product-backlog-import route`."

### Functional — Route Mode

**FR-R-1** `/product-backlog-import route` MUST read the plan document in its current state, including any PM edits made between sessions.

**FR-R-2** Route mode MUST begin with a routing confirmation session. No writes happen without explicit PM confirmation.

**FR-R-3** Multiple route-mode sessions on the same plan are valid. The skill MUST support iterative PM adjustments across sessions without destroying prior state.

**FR-R-4** On confirmed routing, the skill MUST write directly to:
- `product-scope-{phase-slug}.md` — new or updated FEATs, product areas, types, Notes (append per Phase 1 FR-PS-7)
- `product-scope-{phase-slug}.md` Suggested Spec Order section — populated from plan §5
- `project-overview.md` — velocity / capacity baseline
- `project-lessons.md` — process lessons
- `project-assumptions.md` — blocked dependencies, unresolved decisions
- `project-knowledge.md` — new domain terms
- `documents/index.md` — plan document entry
- `project-daily` — audit entries for every write

**FR-R-5** After successful writes, the plan's frontmatter MUST be set to `status: routing-done`.

**FR-R-6** Route mode MUST NOT hand off to `/project-document`. It routes directly because it has full context from the import and confirmation sessions. As a corollary, the "Backlog Import" classification branch in `project-document/SKILL.md` (used by the pre-Phase-2 handoff flow) MUST be removed in Build 2 — it is dead code after Phase 2.

**FR-R-7** Existing scope entry updates MUST append to the Notes column rather than overwrite (per Phase 1 FR-PS-7).

**FR-R-8** The PM MAY manually set the plan status back to `routing-preparation` and re-run route mode to route additional items; the skill MUST support this flow.

**FR-R-9** If the target `product-scope-{phase-slug}.md` does not exist at route time, the skill MUST propose phase metadata derived from source context:

- Phase slug (e.g. Linear team name → slug)
- Phase focus (one-line description from dominant themes in the backlog)
- Target release (where inferable from source signals — e.g. Linear cycle end date; otherwise `-tbd-`)
- Key outcomes (2-3 bullets from dominant capability themes)

The skill MUST surface the full proposal during routing confirmation, and autonomously create the scope file on PM confirmation. Creation MUST invoke `product-scope`'s full create-mode flow — including Phase 1 canonical feature-table structure, the Suggested Spec Order section, AND Section E outbound routing (which automatically syncs the new phase to `product-brief` Section 8 High-Level Phasing under the existing bidirectional-sync-gated rule). Creation is logged as an audit entry in `project-daily`.

### Functional — Update Mode

**FR-U-1** When a prior plan is detected and the PM confirms update, the skill MUST compare the new backlog against the existing scope document (not the prior plan).

**FR-U-2** New items MUST be classified and proposed as new FEATs or additions to existing FEATs.

**FR-U-3** Changed items (status, priority, description) MUST be flagged on existing FEATs for PM review.

**FR-U-4** Removed items (in prior import but no longer in backlog) MUST be flagged for PM review. Auto-removal from scope is forbidden.

**FR-U-5** The prior plan's frontmatter MUST be updated with `superseded_by: {new-filename}`.

**FR-U-6** Update mode orientation MUST skip questions already answered by the prior import. It MUST ask only: "Anything new to specify upfront, or re-run with last import's type and priority mappings?" Prior mappings are read from the prior plan document's Type & Priority Mapping section (§6).

### Non-Functional

**NFR-1** Plan document generation MUST complete within a single session for backlogs up to 300 items. Larger backlogs require a filter-driven scope narrow during exploration.

**NFR-2** No "raw data only" mode. The skill is opinionated-advisor-first by design. If the PM wants raw data, they use the source tool.

**NFR-3** Write-back to the source backlog tool is forbidden. The skill is read-only against the source.

**NFR-4** Every write to a harness artifact MUST produce a corresponding audit entry in `project-daily` (format: `[AUTO] product-backlog-import — {what changed} ({date})`).

**NFR-5** All sections of the plan MUST be machine-readable — consistent table formats, item structure, mapping tables — so downstream consumers (route mode, future imports) parse reliably.

---

## User Flows

1. **First-time brownfield import** — PM runs `/product-backlog-import`. Silent pre-orientation filesystem scan (FR-CL-1) confirms no prior plan. Three-question orientation (FR-O-1). Skill loads harness context tailored to answers per FR-CL-2. Skill infers MCP for Linear (FR-O-2), connects, explores: shows 4 teams. PM picks a team. Skill confirms scope per FR-E-3, runs deep analysis, produces plan per FR-P-1 and FR-P-2 with status `routing-preparation`. Session ends or continues into route.

2. **Route mode after PM review** — PM runs `/product-backlog-import route`. Skill re-reads harness context per FR-CL-3 (context may have changed since import). Skill reads plan in current state (FR-R-1), including PM's manual edits. Presents routing confirmation. PM adjusts a few FEATs, confirms. Skill writes per FR-R-4, sets status to `routing-done` (FR-R-5), logs audit entries per NFR-4.

3. **Update mode against existing scope** — PM runs `/product-backlog-import` on a project with a prior plan. Defensive check detects prior (FR-D-1). PM confirms update. Light orientation per FR-U-6 with prior mappings loaded from prior plan §6. Skill loads harness context, compares new backlog against the existing scope document per FR-U-1 — flags new/changed/removed items.

4. **Contradictory orientation** — PM says "initial brownfield onboarding" but a prior plan exists. Skill surfaces the mismatch per FR-D-2. PM clarifies; skill proceeds accordingly.

5. **Route mode with no existing scope phase** — PM confirms routing to a phase whose scope file doesn't exist. Skill proposes a phase slug derived from source context, PM confirms the name, skill autonomously creates the scope file (FR-R-9) and writes FEATs into it. Audit entry logged.

---

## Acceptance Criteria

- [ ] Pre-orientation filesystem scan runs for defensive check only; no other context reads (FR-CL-1)
- [ ] Import mode reads the 7-file harness context set after orientation, skipping silently on missing files (FR-CL-2)
- [ ] Route mode re-reads the same harness context on entry (FR-CL-3)
- [ ] Context depth is tailored to PM's orientation answers (FR-CL-2)
- [ ] Orientation asks exactly 3 questions; skill infers access method and does not ask (FR-O-1, FR-O-2)
- [ ] MCP auth failure falls through to export / paste without PM intervention beyond notification (FR-O-3)
- [ ] Filter / board / view / completed-items questions happen after backlog access, never upfront (FR-O-4, FR-O-5)
- [ ] Silent defensive check surfaces only on contradiction with PM-stated context (FR-D-1 through FR-D-4)
- [ ] Every item in the Proposed Scope Structure has a FEAT ID and a type (FR-C-2, FR-C-4)
- [ ] Small items are grouped into umbrella FEATs with explicit rationale (FR-C-3)
- [ ] Completed items follow the 4-tier approach and are presented as a concrete PM recommendation (FR-C-5)
- [ ] Velocity & Delivery Insights section contains 2-3 insights, each tagged with a routing target (FR-V-1, FR-V-3)
- [ ] Plan document has `status: routing-preparation` on creation (FR-P-3)
- [ ] `/product-backlog-import route` reads the plan in its current state including PM edits (FR-R-1)
- [ ] Route mode writes directly to harness artifacts without handing off to `/project-document` (FR-R-4, FR-R-6)
- [ ] `project-document` "Backlog Import" classification branch is removed as part of Build 2 (FR-R-6 corollary)
- [ ] Plan status is set to `routing-done` after confirmed writes (FR-R-5)
- [ ] Existing scope entry updates append to Notes rather than overwrite (FR-R-7)
- [ ] Missing target phase triggers autonomous scope file creation with PM-confirmed slug (FR-R-9)
- [ ] Update mode compares against the existing scope document, not the prior plan; prior mappings loaded from prior plan §6 (FR-U-1, FR-U-6)
- [ ] Every harness write produces a matching audit entry in project-daily (NFR-4)

---

## Edge Cases

- **Source backlog empty or returns zero items after filter** — skill notifies PM and exits; no plan is written.
- **Source backlog over 300 items** — skill suggests filter-narrow during exploration; if PM insists on all, warns about NFR-1 and proceeds.
- **MCP auth fails after partial progress** — skill persists any partial state, informs PM, offers export fallback for the remaining work.
- **PM closes session mid-classification** — skill persists a partial plan with `status: routing-preparation` and a note in §1 describing what's incomplete.
- **PM edits the plan document manually between sessions** — route mode reads PM edits as authoritative (FR-R-1).
- **Non-English source** — titles and descriptions translated to English per FR-P-4; originals preserved in parentheses only if PM asked during orientation.
- **Prior plan from a different tool** — defensive check surfaces the mismatch; default treatment is fresh import.
- **Prior plan exists with `status: routing-done`** — import mode still creates a new plan (new calendar import); the old one is marked `superseded_by` per FR-U-5.
- **PM wants to re-route items after `routing-done`** — PM manually sets status back to `routing-preparation` and re-runs route mode (FR-R-8).
- **Source item has no description** — imported with title only; skill marks the FEAT description as "No description in source — enrich during `/product-feature` specing."
- **Mixed estimation units in source** — preserved as-is per FR-M-4; inconsistency flagged in §7 Open Questions.
- **PM introduces a custom project type during Type & Priority Mapping** — accepted per Phase 1 NFR-1; used in the plan and in written scope.
- **Duplicate source IDs in export file** — flagged in §7 Open Questions; not auto-deduplicated.
- **Target scope phase doesn't exist at route time** — skill proposes a slug from source context, PM confirms, skill creates the scope file autonomously per FR-R-9.
- **Harness context file missing** (e.g. no `product-brief.md` on a brand-new project) — skipped silently per FR-CL-2; the skill proceeds with whatever context is available.

---

## Dependencies

- **Phase 1 required** — type system and canonical feature-table structure in `product-scope` and `product-feature` (IMPROVEMENT-SPEC-phase1-type-system.md). Phase 2 cannot ship without Phase 1.
- `product-scope` — receives FEAT writes during route mode (FR-R-4); may be autonomously created per FR-R-9
- `product-feature` — downstream; PM runs it to spec FEATs the plan produced (no direct write from backlog-import)
- `product-brief` — read for strategic context (FR-CL-2); also indirectly written via `product-scope` Section E outbound routing when FR-R-9 autonomously creates a new phase (the phasing sync updates `product-brief` Section 8). No direct write from backlog-import itself.
- `product-requirements` — read for requirements context
- `project-overview` — receives velocity / capacity baseline writes; also read for current phase / RAG context
- `project-lessons` — receives process lessons
- `project-assumptions` — receives blocked dependencies; also read for Decided items influencing classification
- `project-knowledge` — receives new domain terms; also read for domain vocabulary
- `documents/index.md` — receives plan document entry
- `project-daily` — receives audit entries for every write
- `project-document` — "Backlog Import" classification branch is removed in Build 2 (dead after Phase 2)
- MCP integrations — Linear, Jira/Atlassian, Notion (preferred access paths per FR-O-2)
- `project-initiation` — PM is pointed to `/product-backlog-import` from the brownfield follow-up list; list is updated in Phase 4

**Loop check**: No routing loops detected. `product-backlog-import` writes outbound only to `product-scope`, `project-overview`, `project-lessons`, `project-assumptions`, `project-knowledge`, `documents/index.md`, and `project-daily`. None of these write back to `product-backlog-import`. Audit entries to `project-daily` are safe under the known-safe pattern — `project-daily` routing rules trigger on PM-initiated events (close step, explicit command), not on appended audit entries. `product-scope` may also write a Suggested Spec Order section from its own reviews (Phase 1 FR-PS-6) — but per Phase 1, that write is PM-confirmed, so there is no auto-triggered loop between backlog-import and product-scope.

---

## Out of Scope

- Write-back to the source backlog tool (forbidden per NFR-3; never supported)
- "Raw data only" mode that skips opinionated analysis (forbidden per NFR-2; never supported)
- Automatic removal of scope entries when source items are deleted (update mode flags for PM review only per FR-U-4)
- Multi-project or multi-source merges within a single import session (one source per import)
- Curated registry of project-specific types (PMs introduce ad hoc per Phase 1)
- Conversion of estimation units between systems (forbidden per FR-M-4)
- `/project-initiation` brownfield flow updates — handled in Phase 4
- Changes to `.claude/harness-artifacts-index.md` — not needed (the index is artifact-centric and backlog-import's routing targets are already registered)
- Design-aware classification using Figma context (future enhancement)
- Reading `product-codebase-audit` baseline or `project-stakeholders.md` at context-load time — excluded by design: codebase content is already reflected in existing scope, and stakeholder sentiment doesn't directly shape backlog grouping
