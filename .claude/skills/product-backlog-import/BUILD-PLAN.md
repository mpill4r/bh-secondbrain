# Build Plan — Product Harness Improvements (Phase 1–4)

> What to build, in what order, and how to verify. Specs are the source of truth for WHAT. This plan covers the sequence, dependencies, cross-skill modifications, and verification needed to ship Phase 1 (type system), Phase 2 (backlog-import rewrite), Phase 3 (codebase-audit rewrite), and Phase 4 (project-initiation brownfield flow + integration polish).
>
> Specs live in `.claude/skills/product-backlog-import/`:
> - `IMPROVEMENT-SPEC-phase1-type-system.md`
> - `IMPROVEMENT-SPEC-phase2-backlog-import.md`
> - `IMPROVEMENT-SPEC-phase3-codebase-audit.md`
> - `IMPROVEMENT-SPEC-phase4-integration.md`

---

## Scope

| # | Deliverable | Type | Spec |
|---|-------------|------|------|
| 1 | `product-scope` — canonical feature-table structure (Type + Notes columns), product-area descriptions, Suggested Spec Order section, PM-confirmed Spec Order proposals | Modify TEMPLATE.md + SKILL.md | Phase 1 |
| 2 | `product-feature` — `type` frontmatter, type-aware Q&A | Modify TEMPLATE.md + SKILL.md | Phase 1 |
| 3 | `product-backlog-import` — full rewrite to PM-strategy-advisor model with import/route modes and harness context loading | Rewrite SKILL.md + TEMPLATE.md | Phase 2 |
| 4 | `project-document` — remove dead "Backlog Import" classification branch | Modify SKILL.md | Phase 2 (Build 2 step 2.4) |
| 5 | `product-codebase-audit` — full rewrite to two-mode PM-strategy-advisor model aligned with Phase 2 pattern | Rewrite SKILL.md + TEMPLATE.md | Phase 3 |
| 6 | `project-document` — remove dead "Codebase Analysis" classification branch AND the `routing: ready-for-routing` detection mechanism (fully orphaned after Phase 3) | Modify SKILL.md | Phase 3 (Build 3 step 3.4) |
| 7 | `project-initiation` — brownfield follow-up list reorder, insert both rewritten skills with two-mode step descriptions | Modify SKILL.md (Part 2 only) | Phase 4 |
| 8 | `CLAUDE.md` / `README.md` — review for doc drift, update brownfield onboarding section if present | Review + minor updates | Phase 4 |

No changes to `.claude/harness-artifacts-index.md` are required across any phase — it's artifact-centric, and all routing targets for the rewritten skills are already registered.

---

## Build Order

Four builds, sequenced by dependency. Each build is independently committable and ships standalone value. Builds 2 and 3 can run in parallel after Build 1 lands — they are independent of each other. Build 4 depends on both.

### Build 1 — Phase 1 — Type system foundations

Must land first. Builds 2 and 3 write into the scope table structure and feature frontmatter established here.

| Step | File | Change |
|------|------|--------|
| 1.1 | `.claude/skills/product-scope/TEMPLATE.md` | Add a sample feature table under `## Product Areas / Epics` establishing the canonical column order `Feature ID \| Name \| Type \| Description \| Status \| Design Status \| Linear IDs \| Notes` (FR-PS-1). Add product-area description paragraph scaffolding above the sample table (FR-PS-2). Add new top-level `Suggested Spec Order` section (FR-PS-3). |
| 1.2 | `.claude/skills/product-scope/SKILL.md` | Update A5 Aggressive Pre-Fill to emit feature tables in the canonical column order (FR-PS-1). Prompt for Type per FEAT on create with `feature` default (FR-PS-4). On review, surface rows with empty Type and prompt PM; allow blank with "type unresolved" in Notes (FR-PS-5). On every create and review, analyze scope state and propose Suggested Spec Order (or changes) for PM review; never write or update the section without PM confirmation (FR-PS-6). Generation uses judgment across: technical dependencies, engineering sequencing, user/business value, delivery risk, external dependencies, spikes, prerequisite chains, spec readiness. Append to Notes rather than overwrite on routed updates (FR-PS-7). |
| 1.3 | `.claude/skills/product-feature/TEMPLATE.md` | Add `type: feature` to frontmatter (FR-PF-1, FR-PF-2). |
| 1.4 | `.claude/skills/product-feature/SKILL.md` | Prompt for type before Q&A (FR-PF-3). Branch Q&A per type: feature / bug / tech / spike / other (FR-PF-4). Prompt on mid-spec type change (FR-PF-5). |

**Per-skill modification process:**

1. Read Phase 1 spec fully — every FR, AC, edge case, dependency
2. Read current SKILL.md and TEMPLATE.md for the skill being modified
3. Edit TEMPLATE.md — add sample feature table + product-area description scaffolding + Suggested Spec Order section; add `type` to feature frontmatter
4. Edit SKILL.md — translate each FR into imperative instructions; apply mitigations (edge cases → guard clauses, NFRs → Rules section)
5. Verify — 5-pass verification below

**Verification for Build 1 (5-pass):**

*Pass 1 — Structural:*
- [ ] `product-scope/TEMPLATE.md` has a sample feature table under `## Product Areas / Epics` with columns in the canonical order
- [ ] `product-scope/TEMPLATE.md` has a product-area description paragraph scaffold above the sample table
- [ ] `product-scope/TEMPLATE.md` has a top-level `Suggested Spec Order` section
- [ ] `product-feature/TEMPLATE.md` frontmatter includes `type: feature`
- [ ] Both modified SKILL.md files are imperative (no `FR-N` references visible to the runtime agent)

*Pass 2 — FR traceability:*
- [ ] FR-PS-1 through FR-PS-7 each traced to a specific instruction in `product-scope/SKILL.md`
- [ ] FR-PF-1 through FR-PF-5 each traced to a specific instruction in `product-feature/SKILL.md`
- [ ] NFR-1 (custom types preserved), NFR-2 (proposal perf), NFR-3 (no migration) translated into the Rules section
- [ ] FR-PS-6 judgment inputs (dependencies, sequencing, value, risk, external deps, spikes, prerequisite chains, spec readiness) explicitly listed in the skill's Spec-Order-generation instructions

*Pass 3 — AC coverage:*
- [ ] Every AC in Phase 1 Acceptance Criteria (12 items) is verifiable against the built files
- [ ] Every AC has a specific instruction in SKILL.md or a specific template change that implements it
- [ ] No AC is covered only by a general rule

*Pass 4 — Edge case coverage:*
- [ ] Zero-FEATs scope renders placeholder in Suggested Spec Order section
- [ ] PM decline-to-type path writes "type unresolved" into Notes
- [ ] Empty `type` frontmatter triggers prompt on open
- [ ] PM declines proposed Spec Order changes → skill respects, does not write
- [ ] Custom type introduction mid-session accepted and offered to subsequent FEATs
- [ ] Pre-Phase-1 scope file → structure rewrite to canonical column order on next review

*Pass 5 — Behavioral:*
- [ ] Loop check reconfirmed: Suggested Spec Order writes only after PM confirmation; no self-referential auto-rewrite loop
- [ ] No new cross-skill silent writes introduced
- [ ] Type-aware Q&A produces visibly different output for `type: bug` vs `type: feature`
- [ ] Out-of-scope items (retroactive migration, type registry, analytics) are not implemented

---

### Build 2 — Phase 2 — Backlog-import rewrite

Depends on Build 1. Independent of Build 3 — can run in parallel.

| Step | File | Change |
|------|------|--------|
| 2.1 | `.claude/skills/product-backlog-import/TEMPLATE.md` | Full rewrite: 8-section plan document structure per Phase 2 Document Structure. Frontmatter with `status`, `source_tool`, `source_filter`, `last_updated`, `last_updated_by`, `superseded_by`. |
| 2.2 | `.claude/skills/product-backlog-import/SKILL.md` | Full rewrite. Key sections: Pre-orientation filesystem scan, Orientation (3-question), Silent Defensive Check, Harness Context Loading (post-orientation import-mode read + route-mode re-read), Backlog Access + Exploration, Classification & Grouping, Velocity & Delivery Insights, Stale Item Handling, Metadata Preservation, Plan Document Production, Route Mode (including autonomous scope phase creation), Update Mode, Rules. |
| 2.3 | `.claude/commands/product-backlog-import.md` | Verify command wrapper; update description to cover the `route` sub-mode. |
| 2.4 | `.claude/skills/project-document/SKILL.md` | **Remove** the "Backlog Import" classification branch and any references in routing logic. Dead code after Phase 2 (Phase 2 FR-R-6 corollary). Ensure no dangling references elsewhere. |

**Per-skill rewrite process:**

1. Read Phase 2 spec fully
2. Read current product-backlog-import SKILL.md + TEMPLATE.md for structural reference only — this is a rewrite, not an edit
3. Draft TEMPLATE.md from spec's Document Structure section
4. Draft SKILL.md translating every FR into imperative instructions. Apply mitigations:
   - Context loading (FR-CL-1 to FR-CL-4) — explicit file-read steps, tailored by orientation answers; skip silently on missing files
   - Edge cases → guard clauses (empty backlog, MCP auth failure, PM closes mid-classification, manual edits between sessions, prior plan from different tool, missing target phase, etc.)
   - NFRs → Rules section (no write-back, no raw-data mode, English output, units preserved, audit-everything, machine-readable output)
   - Every write path has: audit entry to project-daily, directory creation fallback for `documents/internal/backlog-import/`, frontmatter update, `documents/index.md` update
   - Explicit prohibitions: no write-back to source tool, no "raw data" mode, no auto-removal from scope, no `/project-document` handoff
5. Edit `project-document/SKILL.md` to remove the "Backlog Import" classification branch (step 2.4). Build 2 scope does NOT include removing the broader `routing: ready-for-routing` mechanism — that is Build 3's responsibility (see step 3.4). Note: Builds 2 and 3 both modify `project-document/SKILL.md`; in parallel execution the edits are in different sections and merge cleanly, but coordinate at merge time.
6. Verify — 5-pass verification below

**Verification for Build 2 (5-pass):**

*Pass 1 — Structural:*
- [ ] Command wrapper at `.claude/commands/product-backlog-import.md` reflects both modes (default and `route`)
- [ ] SKILL.md imperative — no spec jargon, no `FR-N` references to the runtime agent
- [ ] TEMPLATE.md has exactly 8 sections matching Phase 2 Document Structure
- [ ] Frontmatter fields match Phase 2 spec (status, source_tool, source_filter, last_updated, last_updated_by, superseded_by)
- [ ] `project-document/SKILL.md` no longer references "Backlog Import" classification (step 2.4)
- [ ] Build 2 does NOT remove the `routing: ready-for-routing` mechanism — that is Build 3's scope. At Build 2 commit time, the mechanism may still be present (if Build 3 hasn't landed yet) or already removed (if Build 3 landed first). Either is acceptable.

*Pass 2 — FR traceability:*
Trace every Phase 2 FR to a specific instruction in SKILL.md:
- [ ] FR-CL-1 to FR-CL-4 (Context Loading)
- [ ] FR-O-1 to FR-O-5 (Orientation)
- [ ] FR-D-1 to FR-D-4 (Silent Defensive Check)
- [ ] FR-E-1 to FR-E-3 (Exploration + Filter Selection)
- [ ] FR-C-1 to FR-C-8 (Classification & Grouping)
- [ ] FR-V-1 to FR-V-4 (Velocity Insights)
- [ ] FR-S-1 to FR-S-3 (Stale Item Handling)
- [ ] FR-M-1 to FR-M-4 (Metadata Preservation)
- [ ] FR-P-1 to FR-P-5 (Plan Document)
- [ ] FR-R-1 to FR-R-9 (Route Mode, including FR-R-9 autonomous scope phase creation)
- [ ] FR-U-1 to FR-U-6 (Update Mode, including FR-U-6 prior mapping source from prior plan §6)
- [ ] NFR-1 to NFR-5 translated into Rules section

*Pass 3 — AC coverage:*
- [ ] Every AC in Phase 2 Acceptance Criteria (21 items) verifiable against the built files
- [ ] Every AC has a specific instruction — not only covered by general rule

*Pass 4 — Write path audit:*

Enumerate Phase 2 write paths:
- Plan document creation at `documents/internal/backlog-import/…`
- Plan status update (`routing-preparation` → `routing-done`)
- Prior plan frontmatter update (`superseded_by`)
- `product-scope-{phase-slug}.md` — new FEATs, updated FEATs (Notes append per Phase 1 FR-PS-7)
- `product-scope-{phase-slug}.md` Suggested Spec Order section population
- `product-scope-{phase-slug}.md` autonomous creation when missing (FR-R-9)
- `project-overview.md` — velocity baseline
- `project-lessons.md` — process lessons
- `project-assumptions.md` — blocked dependencies
- `project-knowledge.md` — new domain terms
- `documents/index.md` — plan entry
- `project-daily` — audit entries

For each write path:
- [ ] Audit entry logged to project-daily (format: `[AUTO] product-backlog-import — {what changed} ({date})`)
- [ ] project-daily fallback (create today's daily if it doesn't exist)
- [ ] Frontmatter updated with `last_updated` + `last_updated_by`
- [ ] Directory creation fallback where applicable
- [ ] Target file fallback where applicable

*Pass 5 — Edge case + behavioral:*
- [ ] Empty backlog after filter → skill notifies, no plan written
- [ ] Backlog >300 items → narrow suggested, NFR-1 warning on insist
- [ ] MCP auth fails mid-import → fallback to export/paste
- [ ] PM closes mid-classification → partial plan persisted
- [ ] PM edits plan between sessions → route mode reads edits (FR-R-1)
- [ ] Non-English source translated; originals preserved only if requested
- [ ] Prior plan from different tool → mismatch surfaced, default fresh import
- [ ] Prior plan `routing-done` → new import allowed, old `superseded_by`
- [ ] PM re-routes after `routing-done` → manual revert supported (FR-R-8)
- [ ] Mixed estimation units preserved, flagged in §7
- [ ] Custom project type accepted per Phase 1 NFR-1
- [ ] Duplicate source IDs flagged, not auto-deduplicated
- [ ] Target phase missing → propose slug, create on confirmation (FR-R-9)
- [ ] Harness context file missing → skipped silently (FR-CL-2)
- Behavioral prohibitions:
- [ ] No write-back to source (NFR-3)
- [ ] No "raw data only" mode (NFR-2)
- [ ] No auto-removal from scope on update (FR-U-4)
- [ ] Route mode never hands off to `/project-document` (FR-R-6)
- [ ] `project-document` "Backlog Import" branch fully removed (step 2.4)
- [ ] Loop check reconfirmed: no routing targets write back to product-backlog-import

---

### Build 3 — Phase 3 — Codebase-audit rewrite

Depends on Build 1. Independent of Build 2 — can run in parallel.

| Step | File | Change |
|------|------|--------|
| 3.1 | `.claude/skills/product-codebase-audit/TEMPLATE.md` | Frontmatter changes: remove `routing: ready-for-routing`, add `status`, add `superseded_by`. 9 sections preserved. Conditional "Changes since last baseline" section added only in refresh mode. |
| 3.2 | `.claude/skills/product-codebase-audit/SKILL.md` | Full rewrite. Key sections: Pre-orientation filesystem scan (refresh detection), Access (URL / local path / overview fallback), Orientation (3 primary + conditional follow-ups), Harness Context Loading (post-orientation 6-file set + route-mode re-read), 3-Pass Analysis (Skeleton → Domain Depth → Synthesis), Content Rules, Baseline Production, Engineering Review Suggestion, Route Mode (including autonomous scope creation), Refresh Mode, Handoff & Cleanup, Rules. |
| 3.3 | `.claude/commands/product-codebase-audit.md` | Verify command wrapper; update description to cover `refresh` and `route` sub-modes. |
| 3.4 | `.claude/skills/project-document/SKILL.md` | **Remove** the "Codebase Analysis" classification branch AND the broader `routing: ready-for-routing` detection mechanism (fully orphaned after Phase 2 removed "Backlog Import" in Build 2 and Phase 3 removes "Codebase Analysis" here). Phase 3 FR-R-6 corollary. Verify no dangling references anywhere in project-document. |

**Per-skill rewrite process:**

1. Read Phase 3 spec fully
2. Read current product-codebase-audit SKILL.md + TEMPLATE.md — preserve the analytical core (3-pass, 9-section structure, content rules), rewrite the input/output plumbing
3. Draft TEMPLATE.md adjustments to frontmatter (remove `routing: ready-for-routing`, add `status`, `superseded_by`)
4. Draft SKILL.md translating every FR into imperative instructions. Apply mitigations:
   - Context loading (FR-CL-1 to FR-CL-4) — pre-orientation scan for refresh detection; post-orientation 6-file read; route re-read
   - Analytical core preserved — 3-pass (Skeleton → Domain Depth → Synthesis), 9-section structure, PR/DA/FEAT ID schemes, confidence tags, fabrication guardrails
   - Content rules (FR-CR-1 to FR-CR-13) — keep existing 14 rules from the prior skill, translated into imperative
   - Route mode (FR-R-1 to FR-R-10) — direct writes to harness; autonomous scope creation for missing phase; PM confirmation for product-brief overwrites
   - Refresh mode (FR-RF-1 to FR-RF-10) — compare + tags + superseded_by
   - NFRs (NFR-1 to NFR-7) — Rules section
5. Edit `project-document/SKILL.md` to remove "Codebase Analysis" classification branch AND the `routing: ready-for-routing` detection mechanism (step 3.4) — both are now fully dead
6. Verify — 5-pass verification below

**Verification for Build 3 (5-pass):**

*Pass 1 — Structural:*
- [ ] Command wrapper at `.claude/commands/product-codebase-audit.md` reflects all modes (default, `refresh`, `route`, and URL/path argument)
- [ ] SKILL.md imperative — no spec jargon, no `FR-N` references to the runtime agent
- [ ] TEMPLATE.md frontmatter has `status` field, does NOT have `routing: ready-for-routing`, has `superseded_by` field
- [ ] TEMPLATE.md has 9 sections preserved
- [ ] `project-document/SKILL.md` no longer references "Codebase Analysis" classification
- [ ] `project-document/SKILL.md` no longer references `routing: ready-for-routing` detection — the mechanism is fully removed

*Pass 2 — FR traceability:*
Trace every Phase 3 FR to a specific instruction in SKILL.md:
- [ ] FR-A-1 to FR-A-6 (Access)
- [ ] FR-CL-1 to FR-CL-4 (Context Loading)
- [ ] FR-O-1 to FR-O-3 (Orientation)
- [ ] FR-RF-1 to FR-RF-5 (Refresh-Mode Detection)
- [ ] FR-AN-1 to FR-AN-7 (Analysis)
- [ ] FR-CR-1 to FR-CR-13 (Content Rules — kept from prior skill)
- [ ] FR-P-1 to FR-P-5 (Baseline Production)
- [ ] FR-ER-1 to FR-ER-3 (Engineering Review Suggestion)
- [ ] FR-R-1 to FR-R-10 (Route Mode, including FR-R-10 autonomous scope creation)
- [ ] FR-RF-6 to FR-RF-10 (Refresh Mode)
- [ ] FR-H-1 to FR-H-5 (Handoff and Cleanup)
- [ ] NFR-1 to NFR-7 translated into Rules section

*Pass 3 — AC coverage:*
- [ ] Every AC in Phase 3 Acceptance Criteria (29 items) verifiable against the built files
- [ ] Every AC has a specific instruction — not only covered by general rule

*Pass 4 — Write path audit:*

Enumerate Phase 3 write paths:
- Baseline document creation at `documents/internal/codebase-analysis/…`
- Baseline status update (`routing-preparation` → `routing-done`)
- Prior baseline frontmatter update (`superseded_by`) in refresh mode
- `product-brief.md` — §1, §2, §3 with PM section-by-section confirmation
- `product-scope-{phase-slug}.md` — §8 FEATs (typed, canonical columns), §7 gaps to Deferred Scope / Future Ideas
- `product-scope-{phase-slug}.md` Suggested Spec Order proposals (Phase 1 FR-PS-6 compliant — PM confirms)
- `product-scope-{phase-slug}.md` autonomous creation when missing (FR-R-10)
- `product-requirements.md` — §5 REQ entries
- `project-knowledge.md` — §4 terms, §5 Knowledge entries
- `project-assumptions.md` — §6 DA entries
- `project-overview.md` — `codebase_repo`, product_state signals
- `documents/index.md` — baseline entry
- `project-daily` — audit entries

For each write path:
- [ ] Audit entry logged to project-daily (format: `[AUTO] product-codebase-audit — {what changed} ({date})`)
- [ ] project-daily fallback (create today's daily if it doesn't exist)
- [ ] Frontmatter updated with `last_updated` + `last_updated_by`
- [ ] Directory creation fallback where applicable
- [ ] Target file fallback where applicable

*Pass 5 — Edge case + behavioral:*
- [ ] Private repo, no auth → specific error, auth guidance (FR-A-4)
- [ ] Local path not exists / empty → skill stops (FR-A-3)
- [ ] Very small repo (<10 files) → warn, confirm (FR-A-6)
- [ ] Multi-repo accepted, unified baseline (FR-A-5, FR-P-1)
- [ ] Non-English → translated, marked with source language (FR-AN-7, NFR-4)
- [ ] Large codebase → Explore subagents (FR-AN-4)
- [ ] Context limits → partial coverage noted (FR-AN-5)
- [ ] Refresh with different repo URL → ask PM, default fresh (FR-RF-5)
- [ ] PM edits baseline between sessions → route reads edits (FR-R-1)
- [ ] Prior baseline `routing-done` → new import allowed, old `superseded_by`
- [ ] PM re-route after `routing-done` → manual revert (FR-R-9)
- [ ] Target phase missing → propose slug, create on confirmation (FR-R-10)
- [ ] product-brief personas exist → surface for PM confirmation before overwriting (FR-R-8)
- [ ] Harness has no foundational artifacts → proceed with what's available
- [ ] Harness context file missing → skipped silently (FR-CL-2)
- [ ] Temp cleanup fails → inform PM (FR-H-5)
- Behavioral prohibitions:
- [ ] No write-back to source repo (NFR-2)
- [ ] No fabrication of user experience, motivation, intent (FR-CR-1)
- [ ] No engineering-only content (FR-CR-4)
- [ ] No file paths in narrative (FR-CR-3)
- [ ] No auto-overwrite of existing product-brief content (FR-R-8)
- [ ] Route mode never hands off to `/project-document` (FR-R-6)
- [ ] `project-document` "Codebase Analysis" branch AND `routing: ready-for-routing` mechanism fully removed (step 3.4)
- [ ] No deep git history analysis (FR-AN-6)
- [ ] Loop check reconfirmed: no routing targets write back to product-codebase-audit

---

### Build 4 — Phase 4 — project-initiation brownfield flow + integration polish

Depends on both Build 2 and Build 3. Small and mechanical.

| Step | File | Change |
|------|------|--------|
| 4.1 | `.claude/skills/project-initiation/SKILL.md` | In Part 2 "What to Do Next" brownfield list: reorder steps and insert `/product-backlog-import` per Phase 4 FR-PI-1. Step 3 description notes two-mode behavior of `/product-codebase-audit` (FR-PI-2). Step 5 description includes cold-run caveat AND two-mode note of `/product-backlog-import` (FR-PI-3). Greenfield list unchanged (FR-PI-4). No other changes to `project-initiation` (FR-PI-5). |
| 4.2 | `CLAUDE.md` | Review Available Commands table for accuracy after Phases 2 and 3. Apply updates only if a discrepancy surfaces (FR-CR-1). |
| 4.3 | `README.md` | Review brownfield onboarding section for accuracy. Update to reflect 7-step order, two-mode behavior of both skills, `/project-initiation` entry point (FR-RM-1). If section doesn't exist and is needed, add a minimal one (FR-RM-2). |

**Verification for Build 4:**

*Pass 1 — Structural:*
- [ ] `project-initiation/SKILL.md` Part 2 brownfield list has exactly 7 steps in the FR-PI-1 order
- [ ] Step 3 includes the two-mode note per FR-PI-2
- [ ] Step 5 includes the cold-run caveat AND the two-mode note per FR-PI-3
- [ ] Greenfield list unchanged — no `/product-backlog-import` (FR-PI-4)
- [ ] `CLAUDE.md` Available Commands table reviewed; any updates applied
- [ ] `README.md` brownfield onboarding section reviewed; any updates applied

*Pass 2 — FR traceability:*
- [ ] FR-PI-1 through FR-PI-5 each traced to specific text in `project-initiation/SKILL.md`
- [ ] FR-CR-1 (CLAUDE.md review) noted in review artifacts
- [ ] FR-RM-1 / FR-RM-2 (README.md review) noted in review artifacts
- [ ] NFR-1 verified: no changes outside listed files
- [ ] NFR-2 verified: follow-up list remains conversational recommendation

*Pass 3 — AC coverage:*
- [ ] Every AC in Phase 4 Acceptance Criteria (7 items) verifiable against the built files

*Pass 4 — Edge case scan:*
- [ ] Pre-Phase-4 brownfield projects → no retroactive notification (accepted drift)
- [ ] PM runs backlog-import cold → advisory, not blocking
- [ ] PM runs codebase-audit cold → advisory, not blocking
- [ ] PM runs steps out of order → permitted (NFR-2)
- [ ] Outdated README section → updated surgically

*Pass 5 — Behavioral:*
- [ ] No new cross-skill writes introduced
- [ ] Loop check reconfirmed: `project-initiation` remains PM-triggered one-time
- [ ] Out-of-scope items (no index changes, no template changes, no skill-catalog sync) confirmed not implemented

---

## Post-Build

### AC Verification Sweep

After all 4 builds are committed, run a spec-first AC verification sweep — walk every AC in every phase spec and trace to the built files.

**Phase 1** — walk every AC (12 items) from `IMPROVEMENT-SPEC-phase1-type-system.md`:
- [ ] Each AC has a specific instruction in `product-scope/SKILL.md` or `product-feature/SKILL.md` that implements it
- [ ] Each AC has a corresponding template element that enables it (sample feature table with canonical columns, type frontmatter, Suggested Spec Order section, product-area description scaffolding)
- [ ] No AC is covered only by a general rule

**Phase 2** — walk every AC (21 items) from `IMPROVEMENT-SPEC-phase2-backlog-import.md`:
- [ ] Each AC has a specific instruction in `product-backlog-import/SKILL.md` (or in `project-document/SKILL.md` for the FR-R-6 corollary AC)
- [ ] Each AC has corresponding template structure where applicable
- [ ] No AC is covered only by a general rule

**Phase 3** — walk every AC (~27 items) from `IMPROVEMENT-SPEC-phase3-codebase-audit.md`:
- [ ] Each AC has a specific instruction in `product-codebase-audit/SKILL.md` (or in `project-document/SKILL.md` for the FR-R-6 corollary ACs)
- [ ] Each AC has corresponding template structure where applicable (9 sections, new frontmatter fields, removed `routing: ready-for-routing`)
- [ ] No AC is covered only by a general rule

**Phase 4** — walk every AC (7 items) from `IMPROVEMENT-SPEC-phase4-integration.md`:
- [ ] Each AC has specific content in `project-initiation/SKILL.md` Part 2 (or CLAUDE/README if updates were applied)
- [ ] No AC is covered only by a general rule

**Cross-phase integration checks:**
- [ ] Phase 2 route mode writes to the Suggested Spec Order section introduced in Phase 1 — section name matches verbatim
- [ ] Phase 3 route mode writes to the Suggested Spec Order section introduced in Phase 1 — section name matches verbatim
- [ ] Phase 2 and Phase 3 Type and Notes writes align with Phase 1 canonical column order and naming
- [ ] Phase 2 and Phase 3 autonomous scope creation (FR-R-9 / FR-R-10) use Phase 1 canonical feature-table structure
- [ ] Phase 2 FR-R-9 and Phase 3 FR-R-10 autonomous scope creation invokes `product-scope`'s full create-mode flow including Section E outbound routing — verify `product-brief` Section 8 (High-Level Phasing) is updated with the new phase row after autonomous creation
- [ ] Phase 2 FR-R-9 and Phase 3 FR-R-10 proposals include phase focus, target release (or `-tbd-`), and key outcomes — not just the slug
- [ ] Phase 4 project-initiation step 3 references the Phase 3 command name and two-mode flow accurately
- [ ] Phase 4 project-initiation step 5 references the Phase 2 command name and two-mode flow accurately
- [ ] `project-document/SKILL.md` has no remaining "Backlog Import" or "Codebase Analysis" classification branches
- [ ] `project-document/SKILL.md` has no remaining `routing: ready-for-routing` detection logic

### Integration Testing

After AC sweep passes, test end-to-end flows against real data:

1. **Phase 1 — scope and feature typing**:
   - Run `/product-scope {new-phase}` on a fresh phase — verify canonical feature table columns, product-area descriptions, Suggested Spec Order section proposed for PM confirmation
   - Run `/product-scope {existing-phase}` — verify untyped rows surfaced, Spec Order changes proposed for PM review (never auto-written), PM decline respected
   - Run `/product-feature FEAT-NNN` for each of: feature, bug, tech, spike, other — verify Q&A branches visibly differ
   - Mid-spec type change — verify re-run-or-keep prompt
   - Custom project type — introduce, verify persistence and offering to subsequent FEATs

2. **Phase 2 — backlog-import end-to-end**:
   - Run `/product-backlog-import` against a real backlog (Linear MCP preferred). Verify: pre-orientation scan, 3-question orientation, harness context loaded after orientation (tailored), silent defensive check, exploration before filter asks, classification produces universal FEAT IDs with types, 2-3 velocity insights tagged with routing targets, plan document with `status: routing-preparation` and all 8 sections
   - Close session mid-plan; reopen with `/product-backlog-import route`. Verify harness context re-read, plan in current state
   - Route mode — verify direct writes to all 7 targets, status → `routing-done`
   - Route mode with missing target phase — verify autonomous scope creation with PM-confirmed slug
   - Update mode — verify comparison against scope document (not prior plan), new/changed/removed flags, prior mappings from prior plan §6, prior `superseded_by` set
   - Non-MCP path — verify CSV export fallback works
   - Dead-code check — `/project-document` has no "Backlog Import" classification

3. **Phase 3 — codebase-audit end-to-end**:
   - Run `/product-codebase-audit {url}` against a real GH repo. Verify: pre-orientation scan, access, 3-question orientation, harness context loaded (6-file set), 3-pass analysis, baseline with `status: routing-preparation` and all 9 sections, engineering review suggestion surfaced if applicable
   - Close session; reopen with `/product-codebase-audit route`. Verify harness context re-read, baseline in current state
   - Route mode — verify direct writes to all 8 targets (including product-brief section-by-section confirmation), status → `routing-done`
   - Route mode with missing target phase — verify autonomous scope creation with PM-confirmed slug
   - Refresh mode — run again against the same repo, verify Changes section, `[new]`/`[changed]`/`[status-changed]`/`[removed]` tags, prior baseline `superseded_by`
   - Multi-repo — verify single unified baseline from multiple URLs
   - Non-MCP clone failure — verify auth guidance surfaces
   - Dead-code check — `/project-document` has no "Codebase Analysis" classification and no `routing: ready-for-routing` detection logic

4. **Phase 4 — project-initiation brownfield flow**:
   - Run `/project-initiation` for a brownfield project. Verify 7-step follow-up list in FR-PI-1 order
   - Verify step 3 includes two-mode note for `/product-codebase-audit`
   - Verify step 5 includes cold-run caveat AND two-mode note for `/product-backlog-import`
   - Run `/project-initiation` for a greenfield project. Verify `/product-backlog-import` does not appear
   - Check `CLAUDE.md` Available Commands table matches built state
   - Check `README.md` brownfield onboarding section (if present) matches current behavior

### Cleanup

After testing passes and integration commits land:

- Keep `IMPROVEMENT-SPEC-phase{1,2,3,4}-*.md` as historical reference — they document the why and the cost to keep is minimal
- **OR** delete the phase specs if a clean skill directory is preferred — contents are frozen in git history
- Decide on `IMPROVEMENT-SPEC.md` (the original brainstorm doc, superseded by the phase specs): delete, keep as history, or reduce to a short index pointing to the phase specs
- Delete this `BUILD-PLAN.md` after all four builds, AC sweep, and integration testing are complete — the plan is transient

---

## Build Tracker

| # | Build | Status | Notes |
|---|-------|--------|-------|
| 1 | Phase 1 — Type system foundations | not started | Prereq for Builds 2 and 3 |
| 2 | Phase 2 — Backlog-import rewrite | not started | Depends on Build 1; includes project-document "Backlog Import" classification removal (step 2.4); can run parallel to Build 3 |
| 3 | Phase 3 — Codebase-audit rewrite | not started | Depends on Build 1; includes project-document "Codebase Analysis" classification + `routing: ready-for-routing` mechanism removal (step 3.4); can run parallel to Build 2 |
| 4 | Phase 4 — project-initiation brownfield flow + integration polish | not started | Depends on Builds 2 AND 3; minimal-scope changes |
| — | AC Verification Sweep | not started | Runs after all 4 builds |
| — | Integration Testing | not started | Runs after AC sweep |
| — | Cleanup | not started | Decide fate of spec files + this plan |
