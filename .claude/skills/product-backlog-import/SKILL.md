# product-backlog-import — Skill Logic

> PM strategy advisor for external backlogs. Uses harness context to propose an opinionated scope structure — the PM's job is editorial (adjust, approve), not architectural. Runs in two modes: **import mode** produces a plan document at `documents/internal/backlog-import/YYYY-MM-DD-{project-slug}-backlog-import.md`; **route mode** reads it back, confirms, and writes directly to harness artifacts. Multiple route-mode sessions on the same plan are valid.

---

## When This Skill Runs

The skill runs when the PM invokes:

| Invocation | Mode |
|------------|------|
| `/product-backlog-import` | **Import mode** — new import. Orientation → harness context load → backlog access → classification → plan document |
| `/product-backlog-import {file-path}` | **Import mode** — same, but a file export is provided upfront; access method inferred as "file export" |
| `/product-backlog-import route` | **Route mode** — resume from an existing plan document; re-read harness context; confirm routing; write to harness on explicit PM confirmation |

If a prior plan exists and the PM runs `/product-backlog-import` (no `route`), the defensive check (Section C) decides whether to enter **update mode** (Section G).

---

## A. Pre-Orientation Filesystem Scan

Before asking anything, silently scan `documents/internal/backlog-import/` for prior plan documents (any file matching `*-backlog-import.md`). Capture: filenames, each plan's `status` and `source_tool` frontmatter, the most recent `last_updated`. This single scan feeds Section C (defensive check). Do not read any other harness files at this stage.

If the directory does not exist, note "no prior plan" and proceed.

---

## B. Orientation

Ask exactly three questions, in a single conversational message:

1. **What is the context for this import?** (initial brownfield onboarding / mid-project catch-up / new work stream)
2. **What tool is the backlog in?** (Linear / Jira / Notion / Trello / Asana / spreadsheet / other)
3. **Anything you want to specify upfront**, or defer specifics until I've explored the backlog?

Do NOT ask about filters, boards, views, or completed-items handling at this stage — those are decided after exploration (Section E) or classification (Section F).

**Access method is inferred from the tool answer**, not asked. Preference order: MCP integration (Linear, Jira/Atlassian, Notion) → file export → pasted content. State the inferred choice; don't ask. If the PM provided a file path as a command argument, access method is pre-set to "file export" and the tool is inferred from the PM's answer.

---

## C. Silent Defensive Check

Using Section A's filesystem scan result and the PM's Section B answers:

- **"initial brownfield onboarding" AND a prior plan exists** → surface the contradiction: "You mentioned initial onboarding but I found a prior import from {date} ({source_tool}, status `{status}`). Did you mean update mode, or a fresh re-import?"
- **"mid-project catch-up" AND no prior plan exists** → surface: "You mentioned catch-up but I don't see a prior import — is this the first harness import?"
- **Otherwise** → do not surface this check at all.

If the PM picks update mode, enter Section G. If the PM picks fresh import after contradiction, proceed to Section D.

---

## D. Harness Context Loading

After orientation (not before), read the following harness context files. Skip silently if any file does not exist.

- `product/problem-space/product-brief.md` — strategic context, phasing direction, personas, goals
- All `product/solution-space/product-scope-*.md` — existing scope, released FEATs, epic structure, highest existing FEAT-NNN ID
- All `product/solution-space/features/FEAT-*.md` — lightweight read (frontmatter + Section 1 Feature Summary only) to support "extends FEAT-NNN" detection and avoid duplicate FEAT IDs
- `product/problem-space/product-requirements.md` — open requirements that may map to backlog items
- `project/management/project-assumptions.md` — Decided items and blocked dependencies that shape classification
- `project/management/project-knowledge.md` — domain terms for interpreting source item titles
- `project/management/project-overview.md` — current phase, project RAG, delivery rhythm

**Tailor depth to the orientation answers**: "new work stream" reads existing scope shallower than "mid-project catch-up"; "initial brownfield onboarding" weights product-brief heavier. Track the highest existing FEAT-NNN across all scope files — new FEATs in the plan continue the sequence.

**Use the loaded context to inform**: FEAT grouping, type mapping recommendations, priority tier assignment, relationship detection with released features, velocity insight selection, Suggested Spec Order rationale, and routing target validation.

Do NOT re-read these files during later steps unless the plan is being adjusted across sessions (handled in Section I route mode).

---

## E. Backlog Access & Exploration

### E1. Access

Based on the inferred access method (Section B):

- **MCP**: Authenticate if needed. If auth fails, inform the PM once and fall through to export / paste: "Unable to authenticate with {tool}. Export as CSV and paste the path, or paste the items directly."
- **File export**: Accept CSV / JSON / XLSX. Auto-detect columns; ask only about ambiguous mappings.
- **Paste**: Accept pasted text in any format (tables, bullets, free-form). Parse, identify distinct items, confirm count with PM.

### E2. Exploration

Before any classification, explore the available structure — projects, boards, views, filters, statuses. List what's available with real, concrete names.

### E3. Filter Selection

Ask filter questions using real discovered options (never abstract categories). Example: "Found 4 Linear teams: VAD-Phase1, VAD-Phase2, VAD-Internal, VAD-Ops. Which?"

### E4. Scope Confirmation

Before deep analysis, state the scope and confirm: "I'll pull {specific filter} from {tool} — approximately {N} items across {M} statuses. Proceed to full analysis?" If N > 300, recommend narrowing the filter; if the PM insists on all, warn about NFR-1 (single-session completion risk) and proceed.

---

## F. Classification & Grouping

Produce a full proposed scope structure — not a list for the PM to organize. The output of this step populates plan §3.

- **Every source item has a FEAT ID**. Nothing falls through the cracks.
- **Group small or thematically-related items** into umbrella FEATs. Explain each grouping in the row's Notes. The PM may split / merge / move during confirmation; update the plan live as the PM adjusts.
- **Assign types** per Phase 1 vocabulary: `feature` · `bug` · `tech` · `spike` · `other`, or any PM-introduced custom type. Record the source-tool type-label → harness-type mapping in plan §6 with PM confirmation.
- **Product areas need description paragraphs** above their feature table (Phase 1 FR-PS-2). Derive descriptions from theme analysis of grouped items plus existing product-brief / scope context.
- **Emit feature tables in the canonical Phase 1 column order**: `Feature ID | Name | Type | Description | Status | Design Status | Linear IDs | Notes`.
- **Priority / Standard tier**: use backlog priority signals, dependency analysis, and in-progress signals. Record the mapping in plan §6.
- **Items that enhance released features** get their own FEAT IDs with "extends FEAT-NNN" recorded in Notes.

### Completed items — 4-tier approach

Handle completed items via this recommendation, surfaced as a concrete proposal:

"Of {N} completed items, I'd import {X} as released FEATs, note {Y} as context on active features, and skip {Z} — agree?"

1. **Summary stats** → always captured in plan §2 Velocity & Delivery Insights
2. **Significant capabilities not already represented in scope** → imported as `released` FEATs with PM confirmation
3. **Items related to active FEATs** → noted as context in the active FEAT's Notes, not imported separately
4. **Everything else** → skipped by default; PM may override

---

## G. Velocity & Delivery Insights

Generate **2-3 opinionated insights per import** (not an exhaustive dump) for plan §2. Insight types include: delivery velocity, type distribution (new features vs. maintenance), priority accuracy, blocker / dependency patterns, team capacity signals.

- **Frame each as an observation**, not a conclusion: "This pattern suggests X — does that match your experience, or was something else going on?"
- **Tag each with a routing target**:

| Insight type | Routes to |
|---|---|
| Velocity / capacity baseline (including new-vs-maintenance distribution) | `project-overview` |
| Process lessons | `project-lessons` |
| Blocked dependencies | `project-assumptions` |
| Team working patterns | `project-knowledge` |

- **Context-aware selection**: brownfield onboarding produces different insights than mid-project catch-up. Use the orientation context (Section B) and loaded harness context (Section D) to shape which observations matter.

---

## H. Stale Item Handling

Populate plan §4 with items recommended for skip or defer, with per-item rationale.

- **Assess staleness against the project's own cadence**, not a hardcoded threshold. Calibrate via the orientation answer about backlog maintenance or by observing activity patterns (last updated dates relative to typical cycle length).
- **Detect and graduate**: duplicates, blocked-on-external-dependency items, underspecified-and-deprioritized items, items superseded by newer work. Recommend skip / defer / keep accordingly.
- **PM may override any recommendation without explanation.**

---

## I. Metadata Preservation (Notes column)

When writing rows into plan §3 (and later into scope during route mode), condense backlog metadata into the single Notes cell:

- Aggregate story points (sum across grouped source items, preserved in original unit — no conversion)
- Who has context (assignees, last commenters)
- Key dates / signals (cycle targets, last activity, blocker start dates)
- Relationship to existing FEATs ("extends FEAT-NNN" / "related to FEAT-NNN")
- Import-specific context (e.g. "grouped 4 source items under umbrella theme")
- Blockers

**Do NOT write individual source-item descriptions into scope.** They live in the plan document only, referenced via the Linear IDs / source IDs column. They stay useful later when the PM runs `/product-feature` to spec the FEAT.

**Do NOT persist source statuses, creation dates, or labels into scope.** Those are consumed during classification and discarded.

**Preserve estimation units exactly as-is.** Mixed units (e.g. story points + hours across groups) are preserved and flagged in §7 Open Questions.

---

## J. Plan Document Production

Write the plan to `documents/internal/backlog-import/YYYY-MM-DD-{project-slug}-backlog-import.md`. Use the TEMPLATE.md structure — all 8 sections always present; sections with no content include a note explaining why.

- **Create the directory** `documents/internal/backlog-import/` if it does not exist.
- **Date** = today's date.
- **Project slug** = derived from `project-overview.md` project name if available, else from orientation context.
- **Frontmatter** on initial write: `status: routing-preparation`, `source_tool: {tool}`, `source_filter: {filter description}`, `last_updated: {today}`, `last_updated_by: auto — product-backlog-import`.
- **All content in English.** Non-English titles / descriptions are translated; originals preserved in parentheses only if the PM requested it during orientation.
- **Update `documents/index.md`**: add an entry with ingestion date, title `{Project} Backlog Import Plan from {Tool}`, source `internal`, summary file link, first 2 sentences of §1 as excerpt. Create `documents/index.md` with appropriate headers if missing.
- **Log audit entry** to today's `project-daily`: `[AUTO] product-backlog-import — backlog import plan written from {tool} — {N} items across {M} product areas ({date})`. Create today's daily from `project-daily/TEMPLATE.md` if it does not exist.

### J1. Session-end Guidance

If the session ends before the PM starts routing, surface clear resume guidance:

> "The plan is saved at `{path}` with status `routing-preparation`. When you're ready to route into the harness, run `/product-backlog-import route`."

### J2. Mid-classification session close

If the PM closes the session partway through classification, persist a partial plan with `status: routing-preparation` and a note in §1 describing what's incomplete. On next `/product-backlog-import`, the defensive check detects it and offers to resume or redo.

---

## K. Route Mode

Triggered by `/product-backlog-import route`. Reads an existing plan and writes the harness artifacts on PM confirmation.

### K1. Re-read harness context

Re-read the harness context files listed in Section D. Context may have changed between the import and route sessions (the PM may have edited scope, added assumptions, etc.). Do not trust the import-time snapshot.

### K2. Read the plan in its current state

Load the most recent plan from `documents/internal/backlog-import/` — the one with `status: routing-preparation`. Read it in full, including any PM manual edits made between sessions.

If no plan has `status: routing-preparation` but a `routing-done` plan exists, offer to re-route: "The last plan is already `routing-done`. To route additional items, set its status back to `routing-preparation` (or I can do that for you), then re-run me. Want me to flip the status?"

### K3. Routing confirmation session

Walk the PM through the plan's §8 Routing Plan area by area. For each planned write, present: target artifact, what will be written, which plan section it comes from. PM confirms, adjusts inline, or skips per item. No writes happen before explicit confirmation.

### K4. Missing target phase — autonomous scope creation

If `product-scope-{phase-slug}.md` referenced in §8 does not exist, propose phase metadata derived from source context:

- **Phase slug** — e.g., Linear team name → slug
- **Phase focus** — 1-line description from dominant themes in the backlog
- **Target release** — where inferable (e.g., Linear cycle end date), otherwise `-tbd-`
- **Key outcomes** — 2-3 bullets from dominant capability themes

Surface the full proposal during routing confirmation. On PM confirmation, invoke `product-scope`'s full create-mode flow (Section A of `product-scope/SKILL.md`) — including canonical feature-table structure, description-paragraph scaffolding, Suggested Spec Order section population, AND Section E outbound routing (which syncs the new phase to `product-brief` Section 8 High-Level Phasing under the bidirectional-sync-gated rule). Log an audit entry for the creation.

### K5. Writes

On confirmed routing, write directly to the target artifacts. No handoff to `/project-document` — the skill has full context.

Write paths:

- **`product-scope-{phase-slug}.md`** — new FEATs (typed, canonical columns, product-area descriptions), updated FEATs. Notes column writes append (never overwrite, per Phase 1 FR-PS-7) with a source tag like `[product-backlog-import {date}]`.
- **`product-scope-{phase-slug}.md` Suggested Spec Order section** — populate from plan §5. PM has already confirmed via the routing confirmation session, which satisfies Phase 1 FR-PS-6's PM-confirmed-write rule.
- **`project-overview.md`** — velocity / capacity baseline from plan §2 (velocity / capacity-tagged insights).
- **`project-lessons.md`** — process lessons from plan §2 (process-lessons-tagged insights). Continue the existing LL-NNN ID sequence.
- **`project-assumptions.md`** — blocked dependencies from plan §2 (blocked-dependency-tagged insights) and any assumption-shaped items from §7. Continue the existing ASM ID sequence.
- **`project-knowledge.md`** — new domain terms discovered during classification. Continue the existing entry format.
- **`documents/index.md`** — plan document entry (if not already written during import mode; otherwise skip).
- **`project-daily`** — audit entry per write, format `[AUTO] product-backlog-import — {what changed} ({date})`. Create today's daily from `project-daily/TEMPLATE.md` if missing.

Before writing to any target, read its TEMPLATE.md (at `.claude/skills/{owner-skill}/TEMPLATE.md`) for correct entry format; continue its ID sequence; place entries in the correct section.

### K6. Status update

On successful writes, update the plan's frontmatter: `status: routing-done`, `last_updated: {today}`, `last_updated_by: auto — product-backlog-import`.

### K7. Iterative route sessions

Multiple route-mode sessions on the same plan are valid. The PM may run route mode, confirm a subset, close, and resume later. Support this without destroying prior state — on re-entry, identify which §8 entries already have `[routed {date}]` marks in the plan (add these marks as you write) and focus the confirmation session on the remaining entries.

### K8. Manual re-route after routing-done

If the PM wants to route additional items after `status: routing-done`, they may set the status back to `routing-preparation` and re-run route mode. Support this flow.

---

## L. Update Mode

Entered from Section C when a prior plan was detected and the PM confirmed update.

### L1. Light orientation

Skip questions answered by the prior import. Ask only: "Anything new to specify upfront, or re-run with last import's type and priority mappings?" Read prior type/priority/area mappings from the prior plan's §6 Type & Priority Mapping.

### L2. Load harness context

Same as Section D.

### L3. Compare against the existing scope document

Compare the newly-pulled backlog state against the existing `product-scope-{phase-slug}.md` (NOT against the prior plan). Flag:

- `[new]` — items in the new backlog that are not in scope
- `[changed]` — existing scope FEATs whose source items have changed status, priority, or description
- `[removed]` — items in the prior plan but no longer in the backlog; surface for PM review. **Auto-removal from scope is forbidden.**

### L4. Produce the new plan

Write a new plan document at `documents/internal/backlog-import/YYYY-MM-DD-{project-slug}-backlog-import.md`. Include a "Changes since last plan" subsection in §1. Routing suggestions in §8 focus on new/changed items; unchanged items do not need re-routing.

### L5. Supersede the prior plan

Update the prior plan's frontmatter: `superseded_by: {new-filename}`. This is a targeted edit; do not modify other content in the prior plan.

### L6. Hand off to route mode

Same as Section J1 — surface resume guidance with the new plan's path.

---

## M. Rules

- **No write-back to source** — forbidden. The skill is read-only against the source backlog tool. No status updates, no comments, no changes written back.
- **No "raw data only" mode** — the skill is opinionated-advisor-first by design. If the PM wants raw data, they use the source tool.
- **No auto-removal from scope** — update mode flags removed items for PM review only.
- **Route mode never hands off to `/project-document`** — it routes directly because it has full context from the import and confirmation sessions.
- **One source per import** — no multi-project or multi-source merges within a single import session.
- **All 8 sections always present** — sections with no content include a note explaining why.
- **English output** — all plan content in English. Non-English titles / descriptions translated; originals preserved in parentheses only if PM asked during orientation.
- **Preserve estimation units** — no conversion between story points, hours, t-shirt sizes. Mixed units flagged in §7.
- **Every harness write produces an audit entry** in today's `project-daily` with format `[AUTO] product-backlog-import — {what changed} ({date})`. Create today's daily from TEMPLATE if missing.
- **Machine-readable structure** — all sections (tables, mappings, item structure) stay in consistent format so route mode, update mode, and future imports parse reliably.
- **Directory creation fallback** — create `documents/internal/backlog-import/` before writing if it does not exist.
- **Target file creation fallback** — create `documents/index.md` and today's `project-daily` from their templates if they do not exist before writing.
- **Custom types are accepted** — if the PM introduces a custom project-specific type during Type & Priority Mapping, preserve it without revalidation (Phase 1 NFR-1).
- **Duplicate source IDs are flagged, not deduplicated** — surface in §7 Open Questions.
- **Plan generation is single-session for ≤ 300 items** (NFR-1). For larger, narrow the filter during E3.
- **Staleness is project-relative** — no hardcoded time thresholds.
- **Missing harness context files are skipped silently** (FR-CL-2). Proceed with whatever is available.
- **Filter / completed-items questions happen after exploration** (Section E / Section F) — never upfront.
- **Notes column writes always append** — never overwrite. Source tag prefix: `[product-backlog-import {date}]`.
- **Plan status lifecycle**: `routing-preparation` (default on create) → `routing-done` (after confirmed writes). PM may manually flip back to re-route.
