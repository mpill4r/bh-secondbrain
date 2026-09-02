---
status: wip
last_updated: 2026-04-17
owner: Jan Koscelansky
phase: Phase 4
---

# Phase 4 — project-initiation Brownfield Flow + Integration Polish

## Overview

Phase 4 wires Phase 2 (`product-backlog-import` rewrite) and Phase 3 (`product-codebase-audit` rewrite) into the rest of the harness. Two concrete changes:

1. Update `project-initiation`'s brownfield follow-up list — correctly ordered so context-generating skills run before context-consuming ones, with step descriptions that reflect the new two-mode behavior of both skills (produce a plan/baseline, then run `route`)
2. Review `CLAUDE.md` and `README.md` for doc drift caused by Phases 2 and 3 — both commands now have two-mode behavior that may need reflection in the Available Commands table and brownfield onboarding guidance

Phase 4 depends on both Phase 2 AND Phase 3. It ships last so the referenced commands are in their rewritten state.

No changes to `.claude/harness-artifacts-index.md` are needed — the index is artifact-centric and all routing targets for both rewritten skills are already registered.

Related specs: `IMPROVEMENT-SPEC-phase1-type-system.md`, `IMPROVEMENT-SPEC-phase2-backlog-import.md`, `IMPROVEMENT-SPEC-phase3-codebase-audit.md`.

---

## Commands

| Command | When to use |
|---------|-------------|
| `/project-initiation` | Existing trigger. Phase 4 updates only the Part 2 "What to Do Next" brownfield list presentation. No changes to any other behavior. |

No new commands. No new artifacts.

---

## User Roles

| Role | Interaction | Key Need |
|------|-------------|----------|
| PM | Runs `/project-initiation` on a brownfield project; reads the Part 2 follow-up list and discovers both rewritten skills | Correctly sequenced guidance — context-generating skills before context-consuming ones; accurate framing of two-mode behavior for both skills |

---

## Document Structure

Phase 4 modifies one file deeply (`project-initiation/SKILL.md`) and reviews two for potential minor updates (`CLAUDE.md`, `README.md`). No new documents.

| # | File | Primary data sources |
|---|------|---------------------|
| 1 | `.claude/skills/project-initiation/SKILL.md` | Spec authors; Phase 4 rewrites Part 2 brownfield list — reorders steps, inserts `/product-backlog-import`, updates step descriptions to reflect two-mode behavior |
| 2 | `CLAUDE.md` | Spec authors; Phase 4 verifies the Available Commands table — no changes expected unless a discrepancy surfaces |
| 3 | `README.md` | Spec authors; Phase 4 reviews the brownfield onboarding section and command reference — minor doc updates only if needed |

### Brownfield follow-up list — post-Phase-4 order

| Step | Command | Rationale + two-mode note |
|------|---------|---------------------------|
| 1 | `/project-document` | Upload SoW, PRD, proposals, contracts, strategy decks — critical documents first |
| 2 | `/project-meeting-upload` | Kickoff transcripts, discovery notes, past calls — feed as much early-context data as possible |
| 3 | `/product-codebase-audit` | Analyze the codebase and produce a product baseline; review, then run `/product-codebase-audit route` to write findings into harness artifacts |
| 4 | `/product-brief` | Coaching session to enrich problem definition, personas, goals — with full context (docs, meetings, codebase) already loaded |
| 5 | `/product-backlog-import` | Analyze planned work and produce a backlog import plan; review, then run `/product-backlog-import route` to write FEATs into scope with full harness context |
| 6 | `/product-scope {phase-slug}` | Polish scope after both route modes landed their initial structure |
| 7 | `/client-overview` | Fill client-intelligence gaps last — least dependency-creating step |

### Rationale for the reorder

The current brownfield list runs `/product-codebase-audit` first and `/client-overview` third. Phase 4 reorders because:

- **Documents and meetings run first** — they contain the highest-value non-code context (vision, commitments, constraints). Loading them early makes every subsequent skill smarter.
- **Codebase audit comes after documents and meetings** — the audit can cross-reference documented intent against code reality, producing a richer baseline than a cold audit.
- **Product brief comes after codebase audit** — the coaching session benefits from both documented intent and code-derived reality.
- **Backlog import comes after product brief** — the opinionated advisor needs strategic context (brief), delivery context (scope), and code context (audit) to classify and group well.
- **Product scope polish comes after backlog import** — if backlog-import routed initial structure, scope polish works with existing data rather than a blank file.
- **Client overview comes last** — it's the least-dependency-creating step and doesn't feed downstream skills in this flow.

### Two-mode framing

Both `/product-codebase-audit` (Phase 3) and `/product-backlog-import` (Phase 2) now use a two-mode pattern:

1. Default mode produces a baseline/plan document with `status: routing-preparation`
2. `route` sub-mode writes confirmed routing to harness artifacts and sets `status: routing-done`

The brownfield follow-up list MUST reflect this. Step descriptions call out both phases so the PM knows to run `route` separately after reviewing the produced document.

---

## Requirements

### Functional — project-initiation brownfield flow

**FR-PI-1** The brownfield follow-up list in `project-initiation`'s Part 2 MUST present steps in this order: `/project-document` → `/project-meeting-upload` → `/product-codebase-audit` → `/product-brief` → `/product-backlog-import` → `/product-scope {phase-slug}` → `/client-overview`.

**FR-PI-2** Step 3 (`/product-codebase-audit`) description MUST note the two-mode behavior: "produces baseline; run `/product-codebase-audit route` after review to write findings into harness artifacts."

**FR-PI-3** Step 5 (`/product-backlog-import`) description MUST include the caveat about running with full context AND the two-mode behavior: "Run this after the above steps so the skill can reason about groupings, velocity, and priority with full context. Running it cold produces weaker proposals. Produces a backlog import plan; run `/product-backlog-import route` after review to write FEATs into scope."

**FR-PI-4** The greenfield follow-up list MUST NOT include `/product-backlog-import` (greenfield projects have no existing backlog). The greenfield list MAY or MAY NOT include `/product-codebase-audit` depending on whether the greenfield project has starting code — Phase 4 makes no change to greenfield content.

**FR-PI-5** Phase 4 MUST NOT change any other behavior in `project-initiation` — the create-all-artifacts flow, input collection (Beats 1 and 2), frontmatter handling, Phase 0-4 internal logic, and audit trail remain unchanged.

### Functional — CLAUDE.md review

**FR-CR-1** Phase 4 MUST verify the Available Commands table in `CLAUDE.md` accurately reflects both rewritten skills. Expected state after Phases 2 and 3: both commands listed under "Product Management" with descriptions matching the rewritten skills. If a discrepancy exists, update to match; otherwise no change.

### Functional — README.md review

**FR-RM-1** Phase 4 MUST review the `README.md` brownfield onboarding section (if one exists) and verify it:
- Lists both `/product-codebase-audit` and `/product-backlog-import`
- Reflects the two-mode flow (baseline/plan → `route`)
- Reflects the new brownfield follow-up order

**FR-RM-2** If the `README.md` brownfield section does not exist or is materially out of sync, Phase 4 MAY add a minimal brownfield onboarding section. Scope limited to: the 7-step follow-up order, a note about two-mode behavior, and a pointer to `/project-initiation` as the entry point.

### Non-Functional

**NFR-1** Phase 4 MUST NOT modify behavior outside `project-initiation/SKILL.md` Part 2, `CLAUDE.md` Available Commands table, and `README.md` brownfield onboarding section. No template changes, no new commands, no new skills, no changes to `.claude/harness-artifacts-index.md`.

**NFR-2** The follow-up list presentation MUST remain conversational — not a rigid checklist the PM must complete in order. Steps are recommendations and can be skipped.

---

## User Flows

1. **Brownfield initiation after Phase 4** — PM runs `/project-initiation` for a brownfield project. Foundational artifacts created by existing Phase 0-4 logic (unchanged). Part 2 completion summary presents the seven-step follow-up list per FR-PI-1. Steps 3 and 5 include two-mode notes per FR-PI-2 and FR-PI-3.

2. **Greenfield initiation (mostly unchanged)** — PM runs `/project-initiation` for a greenfield project. Follow-up list remains as today; `/product-backlog-import` does not appear per FR-PI-4. Existing greenfield content not modified by Phase 4.

3. **PM reads README.md or CLAUDE.md after Phase 4** — documentation reflects both rewritten skills and the two-mode flow; PM has a consistent picture across `/project-initiation` guidance, README, and CLAUDE.

---

## Acceptance Criteria

- [ ] `/project-initiation` brownfield completion summary presents the seven-step follow-up list in the order defined by FR-PI-1
- [ ] Step 3 description includes the two-mode note per FR-PI-2
- [ ] Step 5 description includes the cold-run caveat AND the two-mode note per FR-PI-3
- [ ] Greenfield completion summary does not include `/product-backlog-import` (FR-PI-4)
- [ ] No other behavior change in `project-initiation` outside Part 2 (FR-PI-5, NFR-1)
- [ ] `CLAUDE.md` Available Commands table reviewed; updates applied only if discrepancy surfaced (FR-CR-1)
- [ ] `README.md` brownfield onboarding section reviewed; reflects the 7-step order, two-mode behavior, and pointer to `/project-initiation` (FR-RM-1, FR-RM-2)

---

## Edge Cases

- **Existing brownfield project initiated before Phase 4 shipped** — no retroactive notification. PM discovers the new command(s) and two-mode flow via the rewritten README, or by running `/project-initiation` on a subsequent project. Accepted drift.
- **PM runs `/product-backlog-import` cold (step 5) without upstream context** — Phase 4 framing is advisory, not blocking. Phase 2 skill handles cold runs gracefully but produces weaker proposals; the step-5 caveat warned the PM upfront.
- **PM runs `/product-codebase-audit` cold (step 3) without prior documents or meetings** — permitted; Phase 3 skill handles absent harness context gracefully (files skipped silently per Phase 3 FR-CL-2).
- **PM runs steps out of order** (e.g. scope before backlog-import) — permitted. Step order is a recommendation per NFR-2, not a hard gate.
- **PM skips steps** (e.g. no past meetings to upload) — permitted; downstream skills handle missing context gracefully.
- **`README.md` has a brownfield onboarding section that references outdated command behavior** — update to match current. If significantly out of date, prefer replacing the relevant subsection rather than line-editing.
- **`CLAUDE.md` is silent about either command** — add an Available Commands row pointing to the skill's SKILL.md description.

---

## Dependencies

- **Phase 2 required** — `/product-backlog-import` must be in its rewritten two-mode form
- **Phase 3 required** — `/product-codebase-audit` must be in its rewritten two-mode form
- `project-initiation` — modified (Part 2 brownfield list; step 3 and step 5 descriptions updated for two-mode)
- `product-backlog-import` — referenced in step 5
- `product-codebase-audit` — referenced in step 3
- `CLAUDE.md` — reviewed for doc drift
- `README.md` — reviewed for doc drift

**Loop check**: No routing loops detected. Phase 4 introduces no cross-skill writes. `project-initiation` remains a one-time-per-project PM-triggered command. `CLAUDE.md` and `README.md` are human-and-agent-readable documentation, not runtime artifacts.

---

## Out of Scope

- Retroactive notification or migration for projects initiated before Phase 4 shipped (accepted drift)
- Command-order enforcement in `/project-initiation` — the list is a recommendation, not a workflow gate per NFR-2
- Hard blocking of `/product-backlog-import` or `/product-codebase-audit` when upstream context-building artifacts are empty — both skills handle cold runs gracefully per Phases 2 and 3
- Changes to `.claude/harness-artifacts-index.md` — not needed (the index is artifact-centric and all routing targets are already registered)
- Template changes, new commands, or new skills (NFR-1)
- Greenfield follow-up list restructuring (scope limited to confirming `/product-backlog-import` is absent)
- Full `README.md` rewrite — Phase 4 is surgical, only updates brownfield onboarding and command reference if they exist
- Syncing `skill-catalog.md` in the external cpo-harness-development repo (lives outside this harness)
- Automated drift detection between spec files and documentation — future enhancement
