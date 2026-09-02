# product-feature — Skill Logic

> Individual feature specifications. Each file defines a single product feature in enough detail for a designer and engineer to build it. The skill runs adaptive Q&A — asking only about gaps the harness can't fill, batching questions efficiently, and auto-deciding implementation details. Feature specs are tightly coupled to `product-scope`: creating a spec updates FEAT status to `drafted`; passing the quality gate updates to `speced`.

---

## When This Skill Runs

This skill runs in three contexts:
- **PM invokes `/product-feature`** → Create or Update (Section A/B)
- **Receives routed content from meetings/documents** → Inbound Routing (Section C)

---

## A. Creation Mode

### A1. Load Context

Read `product/solution-space/product-scope-*.md` (find FEAT entry) and `product/problem-space/product-brief.md` (core dependencies). Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match the current task — this includes `product/problem-space/product-requirements.md` and `project/management/project-knowledge.md`. If any file does not exist, skip silently.

### A2. Mode Detection

- If PM provides **FEAT-NNN** and a file exists at `product/solution-space/features/FEAT-NNN-*.md` → **UPDATE** mode (Section B).
- If PM provides **FEAT-NNN** and no file exists → **CREATE** mode. Verify FEAT-NNN exists in a product-scope file; if not found, inform PM and ask whether to create a new FEAT entry in product-scope.
- If PM provides a **feature name** without FEAT-NNN → search product-scope for a matching feature name. If found, use its FEAT-NNN. If not found, offer to create a new FEAT entry in product-scope first, then proceed to CREATE mode.

### A3. No Product-Scope Edge Case

If no product-scope file exists, warn: "No product-scope file found. Create a scope document first via `/product-scope`, or proceed without scope linkage?" If PM proceeds, the feature spec is created but no FEAT-NNN sync occurs. The file is named `FEAT-000-{slug}.md` as a placeholder until linked.

### A4. Pre-Populate from Context

In CREATE mode with a valid FEAT-NNN, read the feature's name and description from product-scope to pre-populate context for the Q&A. Also gather any requirements mapped to this feature from `product-requirements`. Also read the Type column for this FEAT.

### A4a. Type Resolution (before Q&A)

Resolve the feature's `type` before Q&A begins:

- If the scope row has a Type value, adopt it and confirm briefly with the PM: "Spec'ing FEAT-NNN as `{type}` — confirm or change?"
- If the scope row's Type is blank or the row has `type unresolved` in Notes, prompt the PM: "What type is this? feature · bug · tech · spike · other (or a custom type you've used in this project)." Default proposal: `feature`. Accept any custom project-specific type the PM has previously introduced in this project; once introduced it is preserved without revalidation.
- If no scope row exists (no-scope edge case), prompt for type before Q&A using the same wording.

Write the resolved type to the feature file's `type` frontmatter field before Q&A output is generated. If the PM later changes the type mid-session, apply Section A5a (mid-spec type change).

### A5. Adaptive Q&A

1. **Assess context**: If the FEAT has a description in product-scope, requirements mapped to it, and relevant context in product-brief → fewer questions needed (1-2 rounds). If just a name with no description → full Q&A (2-3 rounds).
2. **Plan all questions before asking**: Categorize each as "must ask PM" (user-facing behavior, scope decisions, UX approach) vs "auto-decide" (implementation details, technical approach). Only present "must ask" items. State auto-decided assumptions in the output so PM can correct.
3. **Batch questions**: Up to 4 per round, target 2-3 rounds maximum. For each question, provide a recommendation with confidence level (weak / medium / strong) and brief rationale. Auto-decide strong recommendations on implementation details without asking.
4. **Decision matrix**: When multiple viable approaches exist for a significant feature decision (scope, UX approach, integration strategy), present a comparison table with criteria (user value, integration complexity, risk to existing flows, consistency, implementation effort), recommendation, confidence, and rationale.
5. **Deferral detection**: During Q&A, watch for signals: "out of scope", "v2", "later", "nice to have", "separate feature", "future enhancement". When detected, offer: "Want to save this to product-scope's Deferred Scope or Future Ideas?" If PM accepts, capture immediately (item, reason, notes), then continue Q&A where it left off.
6. **Branch Q&A by type**: The Q&A focus and section emphasis depends on the resolved `type` (from A4a):
   - **`feature`** — user stories, acceptance criteria, edge cases, design, happy and sad paths. Full 8-section spec as standard.
   - **`bug`** — reproduction steps, root-cause hypothesis, affected areas/users, fix criteria, regression risk. AC section describes the corrected behavior and regression-guard criteria rather than a new flow. Edge Cases section focuses on boundary conditions that could still fail after the fix.
   - **`tech`** — technical rationale (why now), migration plan, rollback strategy, success criteria (observable outcomes), risk. User Stories may be written as engineering-team stories or marked `N/A` with a one-line note. AC describes completion signals (e.g., "zero requests hitting legacy endpoint over N days"). Edge Cases emphasize rollout/rollback failure modes.
   - **`spike`** — research questions, time-box, expected outputs/deliverables, decision criteria, follow-up actions. AC describes what makes the spike "done" (research artifacts produced, decision documented) rather than shipped functionality. Out of Scope explicitly lists implementation work the spike will not do.
   - **`other`** — adaptive. Open the session by asking the PM what shape of spec is most useful, then proceed with a tailored question set.
   
   Custom project-specific types (preserved per the type vocabulary) default to the `feature` shape unless the PM indicates otherwise at the start of Q&A.

### A5a. Mid-Spec Type Change

If at any point during Q&A or spec review the PM indicates the feature is a different type than previously resolved (e.g., "this is actually a spike, not a feature"), prompt: "Switching from `{old}` to `{new}` — re-run the relevant Q&A sections, or keep current content?"

- **Re-run**: update `type` frontmatter, re-apply type-branch guidance from A5 step 6, replace the type-sensitive sections (typically User Stories, ACs, Edge Cases, Out of Scope, Dependencies) with regenerated content, and preserve PM-authored material where the PM asks to keep it.
- **Keep current content**: update only the `type` frontmatter. Note a single line at the top of the Feature Summary: "Type reclassified from `{old}` to `{new}` — spec content retained as originally shaped."

Also sync the scope table's Type column for this FEAT to the new value on the next outbound route.

### A6. Generate Spec

After Q&A is complete, generate the full spec following the template structure. All 8 sections + Open Questions section must be present. Emojis in section headers are intentional.

- **Section 1 (📋 Feature Summary)**: 1 paragraph — what is being built, why, user problem solved, business value delivered.
- **Section 2 (👤 User Stories)**: `As a [role], I want to [action], So that [value]` — one per distinct role or use case.
- **Section 3 (✅ Acceptance Criteria)**: Given/When/Then per user story. Explicitly define: what the UI shows, what triggers transitions, what is blocked/disabled and under what conditions. Implementation-ready. For every mandatory input field, include relevant validations (min/max length, format rules, required characters).
- **Section 4 (🔥 Edge Cases & Failure Scenarios)**: Empty states, invalid inputs, concurrent actions, permissions, network failures, boundary values, unexpected sequences. Every edge case must map to a corresponding acceptance criterion in Section 3.
- **Section 5 (🚫 Out of Scope)**: What's NOT included — prevents scope creep. Do NOT include a "Future Enhancements" section — deferred items go to product-scope.
- **Section 6 (⚙️ Technical Constraints & Assumptions)**: Known constraints, assumptions, items needing engineering confirmation.
- **Section 7 (🔗 Dependencies)**: Other features (FEAT-NNN refs), external services, prerequisites.
- **Section 8 (🎨 Design)**: Use Figma MCP when available — PM provides a Figma link, skill reads via `get_design_context` and `get_screenshot`, lists all frames with direct Figma links. If Figma MCP is not active or not configured, PM provides screenshots or pastes the link manually. Never block on Figma availability.
- **Open Questions (❓)**: Questions for engineering, design, client, or other teams. Must be empty before `speced`.

Present the complete document to PM for review. PM can adjust any section before confirming the write.

### A7. After Writing

- Set frontmatter: `feat_id: FEAT-NNN`, `phase: {phase-slug}`, `slug: {feature-slug}`, `type: {resolved-type}`, `last_updated: {today}`.
- Log audit entry to `project-daily`: `[MANUAL] FEAT-NNN-{slug} — created via /product-feature ({date})`.
- If `project-daily` does not exist, create it first.
- Run outbound routing (Section D).
- Run routing check (Section E).

---

## B. Update Mode

### B1. Load Context

Same as A1. Additionally, read the target `product/solution-space/features/FEAT-NNN-{slug}.md` (full file).

### B2. Status Summary

Present the current spec status, current `type`, and Open Questions count. If `type` frontmatter is empty or missing, prompt the PM immediately to resolve it (same wording as A4a) before accepting other changes — do not silently default. PM can: edit any section, add edge cases, update acceptance criteria, update status, resolve open questions, add design references, change type (applies A5a).

### B3. Quality Gate (drafted → speced)

When PM requests status change from `drafted` to `speced`, auto-trigger a quality check before applying the change. Check for:

- Vague or unmeasurable language ("fast", "user-friendly", "simple", "intuitive")
- Subjective terms without targets ("better", "improved")
- Missing rationale for decisions
- Implicit assumptions not stated in Section 6
- Conflicting requirements between acceptance criteria
- Missing user flows (feature mentioned without step-by-step interaction)
- Only happy path described (no edge cases for a given flow)
- Unbounded scope ("all", "any", "every" without limits)
- Missing non-functional requirements where relevant (accessibility, security, data handling)

Present quality issues grouped by severity:
- **Critical** (must resolve before speced) — PM resolves or overrides with written rationale. Overrides are logged: `[MANUAL] FEAT-NNN — quality gate overridden: {rationale}`.
- **Warning** (can acknowledge and proceed) — noted but don't block.

Open Questions section (❓) must be empty before `speced`. If items remain, block: "These open questions need resolution before marking as speced: [list]. Resolve them now?" PM must resolve or remove each item.

### B4. Status Changes

- **drafted → speced**: Quality gate passes → update frontmatter and product-scope FEAT-NNN status to `speced`.
- **speced → in development**: PM-triggered. Update frontmatter and product-scope.
- **in development → released**: PM-triggered. Update frontmatter and product-scope.

### B5. Writing Changes

Before writing any changes, show a diff and ask PM to confirm. End every session with: "Anything else to add or update?"

### B6. After Writing

- Update frontmatter `last_updated` and `status`.
- Log audit entry to `project-daily`: `[MANUAL] FEAT-NNN-{slug} — {what changed} via /product-feature ({date})`.
- If `project-daily` does not exist, create it first.
- Run outbound routing (Section D).
- Run routing check (Section E).

---

## C. Inbound Routing (from meetings and documents)

`project-meeting` and `project-document` route feature-level content to existing feature specs via PM-confirmed routing review. The routing review is owned by the originating skill — this skill receives the writes, it does not initiate them.

### Routable content and target sections

- Acceptance criteria → Section 3 (✅ Acceptance Criteria)
- Edge cases → Section 4 (🔥 Edge Cases & Failure Scenarios)
- UX flow details → Section 3
- Design decisions → Section 8 (🎨 Design)
- Technical constraints → Section 6 (⚙️ Technical Constraints & Assumptions)
- Dependency information → Section 7 (🔗 Dependencies)
- Scope clarifications → Section 5 (🚫 Out of Scope)

New content is clearly marked with source attribution: `<!-- Routed from {source-slug} ({date}) -->`.

### Fallback when spec file does not exist

If a FEAT-NNN feature spec file does not exist when routing is attempted, route the content to `product-scope` instead — append as a note on the FEAT-NNN entry in the feature table (e.g., "Detail captured from {source-slug} — create spec via `/product-feature FEAT-NNN`"). This prevents information loss while keeping feature spec creation under PM control.

### After each routed write

- Update frontmatter `last_updated` and `last_updated_by: auto — {source skill} routing`.
- Log audit entry to `project-daily`: `[AUTO] FEAT-NNN-{slug} — {section name} updated from {source-slug} ({date})`.
- If `project-daily` does not exist, create it first.
- Preserve all existing content exactly. Only targeted sections and fields are modified.

---

## D. Outbound Routing (after every write)

After every write (creation, update, status change, or inbound routing), silently route relevant content outbound. If a target file does not exist, skip silently.

1. **`product-scope` FEAT-NNN status and type sync**: If the product-scope file does not exist, skip silently.
   - On creation: set status to `drafted`, add or update Description column from the Feature Summary, and write the resolved `type` into the FEAT's Type column (overwriting any prior value). If the FEAT was `defined`, this is the first status change.
   - On `speced` (quality gate passed): set status to `speced`.
   - On `in development` or `released`: set status accordingly.
   - On type change (per A5a): update the FEAT's Type column in the scope table to match the new frontmatter value.
2. **`product-requirements` status update**: If the feature spec addresses requirements from `product-requirements` (referenced in Q&A context or explicitly mapped by PM), update those requirements' status to `Processed` with `Addressed in: product/solution-space/features/FEAT-NNN-{slug}.md`. If `product-requirements.md` does not exist, skip silently.
3. **`project-daily` audit entry**: Standard audit entry for every write.

Each outbound write is logged as a separate audit entry to `project-daily`.

---

## E. Routing Check (end of session)

At the end of every `/product-feature` session (before the final write), scan for decisions and assumptions that emerged — scope decisions, technical assumptions, integration dependencies, UX approach commitments. Present any unrouted items: "These decisions/assumptions emerged during our session — route to project-assumptions? [list]." PM confirms, skips, or adjusts. Confirmed items are written to `project-assumptions.md` with source `product-feature FEAT-NNN session ({date})`. If `project-assumptions.md` does not exist, skip silently.

---

## Rules

- **All 8 sections + Open Questions always present**: Every feature spec has all sections, even if some are initially `-tbd-`.
- **Type is required frontmatter**: Every feature spec carries `type` in frontmatter. Valid values: `feature` · `bug` · `tech` · `spike` · `other`, or any project-specific type the PM has previously introduced in this project. Custom types are accepted and preserved without revalidation once introduced.
- **Resolve type before Q&A**: In CREATE mode, resolve `type` in A4a before the Q&A begins — read from the scope row, confirm with the PM, or prompt with `feature` as default. Never run Q&A against an unresolved type.
- **Empty type frontmatter triggers prompt on open**: In UPDATE mode, if the feature file's `type` frontmatter is empty or missing, prompt the PM immediately. Do not silently default.
- **Q&A branches by type**: Q&A emphasis differs for `feature`, `bug`, `tech`, `spike`, and `other` per Section A5 step 6. A feature spec with `type: bug` runs bug-flavored Q&A, not feature Q&A.
- **Mid-spec type change prompts per A5a**: Never silently rewrite sections on a type change; always ask re-run or keep.
- **Type changes sync to scope**: When the feature's `type` changes, the next outbound route updates the FEAT's Type column in the scope feature table.
- **Emojis in section headers**: Intentional and consistent across all feature specs. Aids visual scanning.
- **`-tbd-` over fabrication**: Unknown fields are always `-tbd-`, never guessed.
- **Product document, not technical spec**: No source code, no file paths (except Figma links and external URLs provided by PM), no package names. No performance thresholds — those are engineering decisions.
- **UI copy defers to Figma**: Describe behavior and purpose of each element, append "(copy per Figma)" for exact wording. Figma is the single source of truth for all UI text.
- **Acceptance criteria are implementation-ready**: Explicitly define what happens at every step of a flow, what state the UI is in, what triggers transitions, what is blocked/disabled and under what conditions.
- **Every edge case maps to an AC**: Each edge case in Section 4 must have a corresponding acceptance criterion in Section 3.
- **No "Future Enhancements" section**: Deferred items are captured to product-scope Deferred Scope or Future Ideas during Q&A, not stored in the feature spec.
- **Input validations included**: For every mandatory input field, include relevant validations (min/max length, format rules, required characters).
- **Open Questions must be empty before speced**: The quality gate blocks if questions remain.
- **Quality gate auto-triggers**: On `drafted → speced` request, the quality check runs automatically. PM cannot skip it.
- **Feature status syncs bidirectionally with product-scope**: Status changes in the feature spec update product-scope, and vice versa (on next session read).
- **FEAT-NNN IDs persist**: If a feature is reassigned, the old product-scope entry is updated. New features always get the next sequential ID.
- **FEAT-NNN reassignment**: If PM wants to change the FEAT-NNN assignment, update the frontmatter `feat_id`, rename the file, update the old FEAT entry in product-scope (status reverts or is cleared), and update the new FEAT entry.
- **Feature spans multiple epics**: The feature spec is a single file. If it logically spans epics, FEAT-NNN is assigned to the primary epic. The spec's Dependencies section (🔗) references the other epic.
- **Partial specs are valid**: PM can create a spec without completing Q&A — status stays `drafted`. PM returns via UPDATE mode.
- **Preserve existing content**: When writing, preserve all existing content exactly. Only targeted sections and fields are modified.
- **PM confirms all manual writes**: Always show diff and wait for confirmation. Never auto-write during `/product-feature` sessions.
- **Audit everything**: Every write (manual and routed) logs to `project-daily`. If `project-daily` does not exist, create it first.
- **Design degrades gracefully**: If Figma MCP is not available, Section 8 is populated manually. Never block on Figma availability.
