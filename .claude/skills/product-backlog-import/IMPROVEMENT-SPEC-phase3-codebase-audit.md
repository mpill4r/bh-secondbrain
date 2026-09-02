---
status: wip
last_updated: 2026-04-17
owner: Jan Koscelansky
phase: Phase 3
---

# Phase 3 — Codebase-Audit Skill Rewrite

## Overview

Phase 3 rewrites `product-codebase-audit` to the same two-mode PM-strategy-advisor pattern Phase 2 established for `product-backlog-import`. The audit becomes a direct-routing skill instead of handing off to `/project-document`.

The skill analyzes the codebase (import mode), produces a structured product baseline, and in route mode writes directly to harness artifacts after PM confirmation. Refresh mode compares a new analysis against a prior baseline and produces a new baseline with change markers.

Key changes from the current skill:

- **New route mode** — reads baseline in its current state (including PM edits), re-reads harness context, presents routing confirmation, writes to harness on PM confirmation, sets status to `routing-done`
- **Status field on baseline** — `routing-preparation` → `routing-done`
- **Explicit context-loading FRs** — currently implicit in Section A3; Phase 3 formalizes timing (after orientation) and target set
- **Baseline frontmatter** — remove `routing: ready-for-routing` (dead after Phase 3); add `status`, `superseded_by`
- **Dead-code removal in `project-document`** — remove the "Codebase Analysis" classification branch and the broader `routing: ready-for-routing` detection mechanism, which is fully orphaned after both Phase 2 and Phase 3 (backlog-import and codebase-audit no longer route through `/project-document`)

The analytical core stays intact — 3-pass analysis (Skeleton → Domain Depth → Synthesis), 9-section baseline structure, PR-NNN / DA-NNN / FEAT-NNN ID schemes, confidence tags, fabrication guardrails, product-lens filtering, no-fabrication rule.

Phase 3 depends on Phase 1 (canonical feature-table structure and type vocabulary — codebase-audit writes typed FEATs to scope during route mode). Phase 3 is independent of Phase 2 but is best shipped alongside it for harness-wide consistency.

**Skill location:**
- Command: `.claude/commands/product-codebase-audit.md`
- Skill logic: `.claude/skills/product-codebase-audit/SKILL.md`
- Template: `.claude/skills/product-codebase-audit/TEMPLATE.md`

Related specs: `IMPROVEMENT-SPEC-phase1-type-system.md`, `IMPROVEMENT-SPEC-phase2-backlog-import.md`, `IMPROVEMENT-SPEC-phase4-integration.md`.

---

## Commands

| Command | When to use |
|---------|-------------|
| `/product-codebase-audit` | Start a new audit — access, orientation, harness context load, 3-pass analysis, baseline production. Resolves repo URL from argument or `project-overview.codebase_repo`. |
| `/product-codebase-audit {url-or-path}` | Same as above with explicit GitHub URL or local path provided upfront. |
| `/product-codebase-audit refresh` | Refresh mode — compare a new analysis against the most recent baseline; produce a new baseline with `[new]` / `[changed]` / `[status-changed]` / `[removed]` tags. |
| `/product-codebase-audit route` | Resume or initiate routing from an existing baseline. Re-reads harness context, reads baseline in current state (including PM edits), runs confirmation, writes to harness on PM confirmation. |

One command with mode disambiguation by argument.

---

## User Roles

| Role | Interaction | Key Need |
|------|------------|----------|
| PM | Runs audit, reviews baseline, confirms routing; validates code-derived inferences (personas, requirements, decisions) | Opinionated code-derived product baseline to edit rather than author from scratch; iterative review cycle |
| Other skills | `product-brief`, `product-scope`, `product-requirements`, `project-knowledge`, `project-assumptions`, `project-overview`, `documents/index.md`, `project-daily` receive routed writes | Consistent write format from a single upstream source |
| Internal engineering | Read-only — reviews flagged items (open decisions, gaps, low-confidence claims) when the PM chooses to hold routing for eng validation | Optional validation opportunity before routing |
| Source GH repo(s) | Read-only access via `gh repo clone` | Never modified — no write-back permitted |

---

## Document Structure

**Path**: `documents/internal/codebase-analysis/YYYY-MM-DD-{project-slug}-product-baseline.md`

**Created**: by PM via `/product-codebase-audit` — a new baseline per audit session. Not created by `project-initiation`.

9 sections always present (plus a conditional "Changes since last baseline" in refresh mode). All sections are present even when a section has no findings — a note explains why.

| # | Section | Notes |
|---|---------|-------|
| 1 | Product Summary | End-user-perspective summary from code |
| 2 | Inferred Personas | Persona table with confidence tags; Role × Capability matrix from permissions/role data |
| 3 | Architectural & Technical Boundaries (Product Implications) | Fact → implication format; product-relevant only |
| 4 | Domain Language | Terms classified as `project-specific` or `domain-standard`; all route to project-knowledge |
| 5 | Product Rules & Requirements (PR-NNN) | Each entry tagged `REQ` (→ product-requirements) or `Knowledge` (→ project-knowledge); source reference on every entry |
| 6 | Decisions & Assumptions (DA-NNN) | Cross-referenced against existing ASMs; source reference on every entry |
| 7 | Product Gaps & Anomalies | Gaps typed as `deferred` or `future-idea`; assigned to §8 epics |
| 8 | Derived Epics & Features | FEAT-NNN IDs (sequential, non-colliding with existing scope), typed per Phase 1 vocabulary, status derived from code signals |
| 9 | Open Questions | Owner + Impact tags; carried forward until resolved; do not auto-route |

In refresh mode, an additional section `Changes since last baseline` is inserted after the Scope Note and before §1.

**Frontmatter:**
```yaml
---
status: routing-preparation | routing-done
classification: Codebase Analysis
source: internal
codebase_repos:
  - url: {repo-url}
    sha: {HEAD-sha}
codebase_snapshot_date: YYYY-MM-DD
last_updated: YYYY-MM-DD
last_updated_by: auto — product-codebase-audit
superseded_by: {filename-if-replaced-by-later-baseline}
audience: harness AI first, PM second
---
```

Removed from prior template: `routing: ready-for-routing` — the mechanism it signalled in `/project-document` is removed in Build 3 and the field serves no purpose.

### Type vocabulary (inherits Phase 1)

Features in §8 use Phase 1 types: `feature` · `bug` · `tech` · `spike` · `other`. Code-derived FEATs are almost always `feature` or `tech`. The audit sets `feature` as the default; PM may reclassify during routing confirmation.

---

## Requirements

### Functional — Access

**FR-A-1** Resolve repo URL in this priority: PM argument → `project/management/project-overview.md` `codebase_repo` frontmatter (prompt PM to confirm or override) → prompt PM directly.

**FR-A-2** For GitHub URLs, clone via `gh repo clone {url} {temp-dir}` (default branch unless PM specified otherwise during orientation). Record HEAD SHA via `git rev-parse HEAD` for frontmatter.

**FR-A-3** For local paths, verify existence and non-emptiness; do not copy — use the path directly.

**FR-A-4** On clone failure, surface specific error and guide PM: "This may be a private repo. Verify you're authenticated with `gh auth status`." Suggest `! gh auth login` if needed. On invalid URL, inform PM and stop.

**FR-A-5** Accept multiple GitHub URLs for multi-repo products. Orientation asks if relevant.

**FR-A-6** On small repos (<10 source files), warn and confirm before proceeding: "This repo has very little content — {N} files. The baseline will be thin. Proceed?"

### Functional — Context Loading

**FR-CL-1** Before orientation, the skill MUST silently scan `documents/internal/codebase-analysis/` for prior baseline files. Informs refresh-mode detection (FR-RF-1).

**FR-CL-2** After orientation, the skill MUST read the following harness context files. Files that do not exist are skipped silently.

- `product/problem-space/product-brief.md` — existing product framing, personas, goals
- All `product/solution-space/product-scope-*.md` — existing FEAT-NNN IDs (for collision avoidance), epic structure, released features
- `product/problem-space/product-requirements.md` — existing REQ-NNN IDs (for cross-referencing PR entries)
- `project/management/project-assumptions.md` — existing ASM-NNN IDs (for cross-referencing DA entries)
- `project/management/project-knowledge.md` — known terminology (to avoid re-defining)
- `project/management/project-overview.md` — project and client context, `codebase_repo` field

The skill MUST tailor analysis depth based on PM orientation answers (product state, focus areas, exclusions).

**FR-CL-3** On route mode entry, the skill MUST re-read the same harness context files (FR-CL-2). Context may have changed between baseline production and route sessions; the skill does not trust the import-time snapshot.

**FR-CL-4** The loaded harness context MUST inform: FEAT-NNN ID collision avoidance, "vs. existing harness" columns on §5 and §6 entries, synthesis framing (product state signals), routing target validation.

### Functional — Orientation

**FR-O-1** Orientation MUST ask three primary questions in a single conversational message:
1. What is the current product state? (active development / between phases / maintenance / other)
2. What is the primary user-facing product this codebase serves?
3. Any areas to exclude from analysis (deprecated, experimental, archived) or specific focus areas for deeper analysis?

**FR-O-2** Conditional follow-ups, asked only when relevant:
- Branch or tag representing production release (if not the default branch)
- Additional repos (if multi-repo is possible and PM provided only one URL)

**FR-O-3** Orientation context MUST shape subsequent analysis:
- Product state informs framing (active → forward-looking suggestions; maintenance → stability-focused observations)
- Exclusions → those code areas are skipped during Pass 1 and Pass 2
- Focus areas → deeper analysis in Pass 2
- Additional repos → cloned per FR-A-1 and FR-A-2

### Functional — Refresh-Mode Detection

**FR-RF-1** The pre-orientation filesystem scan (FR-CL-1) populates refresh-mode detection.

**FR-RF-2** If PM provides `refresh` argument AND a prior baseline exists → enter refresh mode.

**FR-RF-3** If PM provides `refresh` argument AND no prior baseline exists → "No prior baseline found — running as first-time analysis." Proceed as first-time.

**FR-RF-4** If a prior baseline exists AND PM did not provide `refresh` → "Found existing baseline from {date} ({snapshot_sha}). Run as refresh (compare against prior and highlight changes) or full re-analysis (produce a new baseline from scratch)?" PM decides.

**FR-RF-5** If the prior baseline's `codebase_repos` URLs differ from the current repo URLs → surface: "Prior baseline analyzed {old URL}, current repo is {new URL}. Treat as fresh analysis (different repo) or refresh (same project, new location)?" Default to fresh if PM unsure.

### Functional — Analysis (3-Pass)

**FR-AN-1** Pass 1 (Skeleton) reads files across all repos in order, adapting to detected tech stack: package/dependency files → documentation → deployment configs → entry points → type/schema definitions → route/handler definitions → GitHub activity (`gh release list`, `gh pr list --state merged --limit 20`, `gh pr list --state open`; skipped for local paths).

**FR-AN-2** Pass 2 (Domain Depth) for each major domain area identified in Pass 1 extracts: capabilities, business rules/invariants, design decisions, domain terminology, gaps/anomalies, feature boundaries, permission/role matrix. Every extracted claim MUST have a source reference (`file.ts:42-58` or minimum `file.ts`).

**FR-AN-3** Pass 3 (Synthesis) follows this ordering — sections have dependencies:

*Phase 3a — Derive features first (§8):*
- Structure capabilities into epics (domain names, not code module names)
- Target 20-50 features for a mature product
- Assign FEAT-NNN IDs, avoiding collision with existing scope IDs (per FR-CL-2)
- Rich multi-sentence descriptions (what + rules + dependency refs)
- Determine status from code signals (released / in development / defined)
- Assign type per Phase 1 vocabulary (default `feature`; `tech` when the feature is infrastructural)

*Phase 3b — Cross-reference dependent sections (§5, §7):*
- §5 (PR-NNN) — assign IDs, classify `REQ` / `Knowledge` routing hints, populate `Addressed in` column with FEAT-NNN(s), populate `vs. existing harness` column using relationship vocabulary (`confirms REQ-NNN` / `refines REQ-NNN` / `new — not captured` / `contradicts REQ-NNN`)
- §7 (Gaps) — classify `deferred` / `future-idea`, assign to §8 epics, list anomalies and failure modes separately

*Phase 3c — Independent sections (any order):*
- §1 Product Summary (end-user-perspective)
- §2 Inferred Personas (confidence tags; pain points and success criteria always `-tbd-`)
- §3 Architectural Boundaries (fact → implication; product-relevant only)
- §4 Domain Language (specificity classification)
- §6 DA-NNN Decisions & Assumptions (cross-referenced against existing ASMs)
- §9 Open Questions (Owner + Impact)

**FR-AN-4** For codebases >10 packages or >50 top-level source directories, Pass 2 MUST use Explore subagents for parallelization across 5-8 domain areas. Otherwise sequential.

**FR-AN-5** On context-limit exhaustion during Pass 2, the skill MUST complete what's possible and note partial coverage in §1 and on the PM handoff message.

**FR-AN-6** No deep git history analysis — recent releases and merged PRs only. Do not analyze commit history depth, blame data, contributor patterns, or branch evolution.

**FR-AN-7** Non-English codebases — analyze in original language, output in English, mark translated quotes with `[translated from {language}]`.

### Functional — Content Rules (Baseline Production)

**FR-CR-1** No fabrication of user experience, business motivation, or stakeholder intent. Code reveals *what* and *how* — never *who*, *why*, or *what frustrates*.

**FR-CR-2** Product lens only. If a sentence is only useful to an engineer implementing the feature, exclude it. If it helps a PM make a product decision, scope a feature, or prepare for a client conversation, include it.

**FR-CR-3** No file paths in narrative sections. File paths appear only in the Source column of PR/DA tables and in the Scope Note.

**FR-CR-4** No engineering-only content — no architecture diagrams, dependency graphs, code quality metrics, test coverage, implementation recipes.

**FR-CR-5** Confidence tags on every persona inference. Pain Points and Success Looks Like are always `-tbd-`.

**FR-CR-6** Source reference on every PR/DA entry — absence of a code reference means absence from the baseline.

**FR-CR-7** Fact→implication format for §3 — facts without product implications are excluded.

**FR-CR-8** Illustrative details flagged as "illustrative — not confirmed with stakeholders."

**FR-CR-9** Feature granularity — target 20-50 features for a mature product. Epic names from domain areas, not code modules.

**FR-CR-10** Rich feature descriptions — §8 descriptions multi-sentence: what + key rules + inline FEAT-NNN dependency refs. Single-phrase descriptions not acceptable.

**FR-CR-11** PR-NNN routing hints — every entry tagged `REQ` or `Knowledge`.

**FR-CR-12** Domain language specificity — every §4 entry tagged `project-specific` or `domain-standard`; both route to project-knowledge.

**FR-CR-13** Gap classification — every §7 gap tagged `deferred` or `future-idea`.

### Functional — Baseline Production

**FR-P-1** Write baseline to `documents/internal/codebase-analysis/YYYY-MM-DD-{project-slug}-product-baseline.md`. Create directory if it does not exist. Multi-repo analysis produces one unified document (not one per repo).

**FR-P-2** All 9 sections always present. Sections with no findings include a note explaining why (e.g., "No regulatory content identified").

**FR-P-3** Frontmatter MUST include `status: routing-preparation` on initial creation.

**FR-P-4** Set frontmatter fields: `classification: Codebase Analysis`, `source: internal`, `codebase_repos` (url + sha per analyzed repo), `codebase_snapshot_date: today`, `last_updated: today`, `last_updated_by: auto — product-codebase-audit`, `audience: harness AI first, PM second`.

**FR-P-5** If the session ends before PM confirms routing, the skill MUST surface clear resume guidance: "The baseline is saved at `{path}` with status `routing-preparation`. When you're ready to continue, run `/product-codebase-audit route`."

### Functional — Engineering Review Suggestion

**FR-ER-1** After writing baseline, count items that would benefit from engineer validation: §6 DA entries with open/uncertain status, §7 gaps, any PR/DA entries with thin code-signal.

**FR-ER-2** If any such items exist, surface to PM: "There are {N} items in the baseline that an internal engineer could validate in a short review — {X} open decisions, {Y} product gaps, {Z} low-confidence claims. Want to hold routing until an engineer reviews, or proceed and circle back later?"

**FR-ER-3** PM decides — this is advisory, not a gate. Do NOT block the skill on engineering review.

### Functional — Route Mode

**FR-R-1** `/product-codebase-audit route` MUST read the baseline document in its current state, including any PM edits.

**FR-R-2** Route mode MUST begin with a routing confirmation session. No writes happen without explicit PM confirmation.

**FR-R-3** Multiple route-mode sessions on the same baseline are valid. The skill MUST support iterative PM adjustments across sessions.

**FR-R-4** On confirmed routing, the skill MUST write directly to:

- `product/problem-space/product-brief.md` — §1 Product Summary informs strategic framing; §2 Personas route to brief's persona section (surface for PM confirmation before overwriting existing personas); §3 product implications inform solution definition
- `product/solution-space/product-scope-{phase-slug}.md` — §8 FEATs (typed per Phase 1; mostly `released`) written to canonical feature table; §7 `deferred` gaps → Deferred Scope; §7 `future-idea` → Future Ideas
- `product/solution-space/product-scope-{phase-slug}.md` Suggested Spec Order section — proposes order for any new FEATs added via this route; respects Phase 1 FR-PS-6 (PM confirmation required)
- `product/problem-space/product-requirements.md` — §5 entries tagged `REQ` (new REQ-NNN IDs or cross-references to existing)
- `project/management/project-knowledge.md` — §4 domain language entries; §5 entries tagged `Knowledge`
- `project/management/project-assumptions.md` — §6 DA entries (new ASM-NNN IDs or cross-references)
- `project/management/project-overview.md` — `codebase_repo` field (confirm or update); `product_state` signals from §1
- `documents/index.md` — baseline entry
- `project-daily` — audit entries for every write

**FR-R-5** After successful writes, baseline frontmatter MUST be set to `status: routing-done`.

**FR-R-6** Route mode MUST NOT hand off to `/project-document`. As a corollary, the "Codebase Analysis" classification branch AND the broader `routing: ready-for-routing` detection logic in `project-document/SKILL.md` MUST be removed in Build 3 — after Phase 2 removed the "Backlog Import" branch and Phase 3 removes the "Codebase Analysis" branch, the `routing: ready-for-routing` mechanism has no remaining consumers.

**FR-R-7** §9 Open Questions MUST NOT auto-route to a harness artifact — they are PM-facing queries carried forward until resolved. The skill surfaces them during routing confirmation for PM to address (typically noted in project-daily or routed manually).

**FR-R-8** Existing artifact updates MUST NOT auto-overwrite. Specifically:
- `product-brief` persona and summary updates are surfaced to PM for section-by-section confirmation before writing
- `product-scope` FEAT table additions use the canonical column order; updates to existing FEATs append to Notes per Phase 1 FR-PS-7
- `product-requirements` REQ entries are added, not deduplicated silently — cross-reference relationships (`confirms` / `refines`) from the baseline are preserved as notes

**FR-R-9** PM MAY manually set baseline status back to `routing-preparation` and re-run route mode to route additional items after `routing-done`.

**FR-R-10** If the target `product-scope-{phase-slug}.md` does not exist at route time, the skill MUST propose phase metadata derived from source context:

- Phase slug (from project context, PM's orientation answer about the primary product, or release-tag signals from `gh release list`)
- Phase focus (one-line description from dominant code-derived capabilities in §8 of the baseline)
- Target release (almost always `-tbd-` for codebase-audit — code does not reveal forward timelines; inferable only from scheduled-release signals if present)
- Key outcomes (2-3 bullets from dominant capability themes in §8)

The skill MUST surface the full proposal during routing confirmation, and autonomously create the scope file on PM confirmation. Creation MUST invoke `product-scope`'s full create-mode flow — including Phase 1 canonical feature-table structure, the Suggested Spec Order section, AND Section E outbound routing (which automatically syncs the new phase to `product-brief` Section 8 High-Level Phasing under the existing bidirectional-sync-gated rule). Creation is logged as an audit entry in `project-daily`.

### Functional — Refresh Mode

**FR-RF-6** In refresh mode, the skill runs the same analysis as first-time mode (Sections Access, Orientation, Context Loading, Analysis).

**FR-RF-7** During Pass 3 synthesis, the skill MUST compare findings against the prior baseline:
- Feature-level: new, changed (description/rules/dependencies), removed, status changes
- PR/DA-level: new, changed, unchanged, gaps addressed

**FR-RF-8** The new baseline MUST include a `Changes since last baseline` section inserted after the Scope Note and before §1, summarizing additions, changes, removals, and status changes, referencing the prior baseline filename and date.

**FR-RF-9** Changed items MUST be tagged in the baseline body: `[new]`, `[changed]`, `[status-changed]`, `[removed]` on PR/DA entries and features.

**FR-RF-10** The prior baseline's frontmatter MUST be updated with `superseded_by: {new-filename}`.

### Functional — Handoff and Cleanup

**FR-H-1** Add baseline entry to `documents/index.md` on initial creation (not on route-mode writes — routing adds its own audit entry but doesn't re-register the baseline).

**FR-H-2** Update `project-overview.md`'s `codebase_repo` field only if it's `-tbd-` or empty. If it has a different value, ask PM before overwriting.

**FR-H-3** Log audit entries to today's `project-daily` for every write path. Create today's daily if it does not exist.

**FR-H-4** After baseline is written (initial or refreshed), present a routing summary to PM: item counts by section, route-mode guidance ("Run `/product-codebase-audit route` to write findings into harness artifacts"), and the engineering-review suggestion per FR-ER-2 if applicable.

**FR-H-5** Clean up temporary clone directories after all output is written. Local paths are not deleted. If cleanup fails, inform PM.

### Non-Functional

**NFR-1** Baseline generation MUST complete within a single session for small-to-medium codebases (<10 packages, <50 top-level source dirs). Larger codebases use Explore subagents per FR-AN-4; context-limit partial coverage is acceptable per FR-AN-5.

**NFR-2** Write-back to the source repo is forbidden. The skill is strictly read-only against the source.

**NFR-3** Every write to a harness artifact MUST produce a corresponding audit entry in `project-daily` (format: `[AUTO] product-codebase-audit — {what changed} ({date})`).

**NFR-4** All baseline content in English regardless of source codebase language.

**NFR-5** Baseline is machine-readable first, PM-readable second — consistent table formats, ID conventions, section headers to enable reliable downstream routing.

**NFR-6** Temp directories cleaned up after the skill completes.

**NFR-7** Staleness signal — `codebase_snapshot_date` in frontmatter enables downstream skills to warn if the baseline is older than 3 months.

---

## User Flows

1. **First-time audit** — PM runs `/product-codebase-audit {url}`. Pre-orientation scan (FR-CL-1) confirms no prior baseline. Access and clone (FR-A-1 to FR-A-6). Three-question orientation (FR-O-1). Skill loads harness context tailored to answers (FR-CL-2). 3-pass analysis (FR-AN-1 to FR-AN-5). Baseline produced per FR-P-1 to FR-P-4 with `status: routing-preparation`. Engineering review suggestion surfaced if applicable (FR-ER-1 to FR-ER-3). Session ends or continues into route.

2. **Route mode after PM review** — PM runs `/product-codebase-audit route`. Skill re-reads harness context per FR-CL-3. Reads baseline in current state (FR-R-1), including PM edits. Presents routing confirmation section-by-section (§1 → product-brief, §8 → product-scope, etc.). PM adjusts, confirms. Skill writes per FR-R-4, sets status to `routing-done` (FR-R-5), logs audit entries per NFR-3.

3. **Refresh mode** — PM runs `/product-codebase-audit refresh`. Pre-scan finds prior baseline (FR-CL-1). URL consistency check (FR-RF-5). Access and clone current state. Orientation (FR-O-1 — product state may have changed). Analysis. Synthesis with comparison (FR-RF-7). New baseline with change markers (FR-RF-8, FR-RF-9). Prior baseline `superseded_by` updated (FR-RF-10). Status `routing-preparation`.

4. **Missing target scope phase at route** — PM confirms routing to a phase whose scope file doesn't exist. Skill proposes phase slug (FR-R-10), PM confirms, skill autonomously creates scope file using Phase 1 canonical structure, then writes FEATs.

5. **Engineering review hold** — After baseline production, skill surfaces {N} items for potential engineering review (FR-ER-1). PM chooses to hold — session ends, baseline stays at `routing-preparation`. After engineering review, PM resumes with `/product-codebase-audit route`.

---

## Acceptance Criteria

- [ ] Pre-orientation scan for prior baselines runs for refresh-mode detection (FR-CL-1)
- [ ] Three-question orientation covers product state, primary product, exclusions/focus (FR-O-1)
- [ ] Post-orientation 6-file harness context load, tailored to answers, skipped silently on missing files (FR-CL-2)
- [ ] Route mode re-reads harness context on entry (FR-CL-3)
- [ ] Repo access supports URL, local path, and fallback from `project-overview.codebase_repo` (FR-A-1)
- [ ] Clone failure surfaces specific error and auth guidance (FR-A-4)
- [ ] Multi-repo products supported (FR-A-5)
- [ ] Pass 1 reads skeleton files in the specified order adapted to tech stack (FR-AN-1)
- [ ] Pass 2 extracts capabilities, rules, decisions, terms, gaps, boundaries, permissions per domain with source references (FR-AN-2)
- [ ] Pass 3 follows synthesis ordering: §8 first, then §5/§7, then independent sections (FR-AN-3)
- [ ] Large codebases (>10 packages or >50 top-level dirs) trigger Explore subagent parallelization (FR-AN-4)
- [ ] Every PR/DA entry has a source reference; entries without are excluded (FR-CR-6)
- [ ] §8 features are typed per Phase 1 vocabulary (default `feature`; `tech` when infrastructural)
- [ ] FEAT-NNN IDs avoid collision with existing scope IDs read from FR-CL-2
- [ ] Baseline has `status: routing-preparation` on initial creation (FR-P-3)
- [ ] Baseline template removes `routing: ready-for-routing` from frontmatter
- [ ] All 9 sections always present; sections with no findings include an explanation note (FR-P-2)
- [ ] Engineering review suggestion surfaces when applicable items exist; PM decides; never blocks (FR-ER-1 to FR-ER-3)
- [ ] `/product-codebase-audit route` reads baseline in current state including PM edits (FR-R-1)
- [ ] Route mode writes directly to harness without handing off to `/project-document` (FR-R-4, FR-R-6)
- [ ] `project-document/SKILL.md` "Codebase Analysis" classification AND `routing: ready-for-routing` detection mechanism are removed in Build 3 (FR-R-6 corollary)
- [ ] Route mode sets baseline status to `routing-done` after writes (FR-R-5)
- [ ] Existing artifacts are not auto-overwritten; section-by-section PM confirmation for product-brief; Notes append for product-scope (FR-R-8)
- [ ] Missing target scope phase triggers autonomous scope file creation with PM-confirmed slug (FR-R-10)
- [ ] Refresh mode produces `Changes since last baseline` section and `[new]`/`[changed]`/`[status-changed]`/`[removed]` tags (FR-RF-7 to FR-RF-9)
- [ ] Prior baseline `superseded_by` updated on refresh (FR-RF-10)
- [ ] No fabrication of user experience, business motivation, or stakeholder intent (FR-CR-1, NFR-2 against source)
- [ ] Temp directories cleaned up (NFR-6, FR-H-5)
- [ ] Every harness write produces a matching audit entry in project-daily (NFR-3)

---

## Edge Cases

- **Private repo, no auth** — specific error surfaced, `! gh auth login` suggested per FR-A-4
- **Local path doesn't exist / empty** — error surfaced, skill stops per FR-A-3
- **Very small repo (<10 source files)** — warn, confirm before proceeding (FR-A-6)
- **Multi-repo product with different URLs** — clone each, produce single unified baseline (FR-A-5, FR-P-1)
- **Non-English codebase** — analyze in original language, output English, mark translated quotes (FR-AN-7, NFR-4)
- **Large codebase (>10 packages or >50 top-level dirs)** — Explore subagent parallelization (FR-AN-4)
- **Context limits hit during Pass 2** — complete what's possible, note partial coverage (FR-AN-5)
- **Refresh with different repo URL** — ask PM, default to fresh (FR-RF-5)
- **PM closes session mid-analysis** — no partial baseline written; skill resumes from scratch on next run (different from backlog-import because analysis is linear and not interactive-reviewable during Pass 2)
- **PM edits baseline between sessions** — route mode reads edits as authoritative (FR-R-1)
- **Prior baseline exists with `status: routing-done`** — import mode still creates a new baseline; old one marked `superseded_by` per FR-RF-10
- **PM wants to re-route after `routing-done`** — PM manually sets status back, re-runs route (FR-R-9)
- **Target scope phase doesn't exist at route** — skill proposes slug, PM confirms, skill creates (FR-R-10)
- **Product-brief already has personas** — surface for PM confirmation before overwriting; do not auto-merge (FR-R-8)
- **Harness has no foundational artifacts (no project-overview, no product-brief)** — proceed with what's available; note in PM handoff that `/project-initiation` may need to run before routing lands meaningfully
- **Harness context file missing** (e.g. no `product-brief.md`) — skipped silently per FR-CL-2
- **Existing ASM/REQ cross-references return no match** — entry tagged `new — not captured`; no fabrication of matches
- **Clone directory cleanup fails** — inform PM, suggest manual removal per FR-H-5

---

## Dependencies

- **Phase 1 required** — codebase-audit writes typed FEATs in the canonical feature-table column order established in Phase 1 (FR-R-4)
- `product-scope` — receives FEAT writes; receives Suggested Spec Order proposals; may be autonomously created per FR-R-10
- `product-brief` — receives strategic-level direct writes (§1 Summary, §2 Personas, §3 implications). Also indirectly written via `product-scope` Section E outbound routing when FR-R-10 autonomously creates a new phase (the phasing sync updates `product-brief` Section 8). Direct writes target Sections 1-7 (strategic slices); phasing sync targets Section 8 — the two do not conflict.
- `product-requirements` — receives REQ entries from §5
- `project-knowledge` — receives §4 domain language and §5 Knowledge entries
- `project-assumptions` — receives DA entries from §6
- `project-overview` — receives `codebase_repo` confirmation, product-state signals
- `documents/index.md` — receives baseline entry
- `project-daily` — receives audit entries for every write
- `project-document` — dead-code removal in Build 3 ("Codebase Analysis" classification branch + `routing: ready-for-routing` detection mechanism)
- GitHub / `gh` CLI — for repo cloning and release/PR queries
- `project-initiation` — PM pointed to `/product-codebase-audit` from brownfield follow-up list; updated in Phase 4
- `product-backlog-import` — sibling two-mode skill (Phase 2); codebase-audit adopts the same pattern for consistency

**Loop check**: No routing loops detected. `product-codebase-audit` writes outbound only to product-brief, product-scope, product-requirements, project-knowledge, project-assumptions, project-overview, documents/index, and project-daily. None write back to product-codebase-audit. Audit entries to project-daily are safe under the known-safe pattern. `product-scope` may write a Suggested Spec Order section from its own reviews (Phase 1 FR-PS-6) — but per Phase 1 that write is PM-confirmed, so there is no auto-triggered loop between codebase-audit and product-scope.

---

## Out of Scope

- Write-back to the source repo (forbidden per NFR-2; never supported)
- Full git history analysis (commit depth, blame, branch evolution) — out per FR-AN-6
- Engineering-only content (architecture diagrams, quality metrics) — out per FR-CR-4
- Fabrication of personas or stakeholder motivations beyond code signals — out per FR-CR-1
- Single-repo assumption — multi-repo supported per FR-A-5
- `/project-initiation` brownfield flow updates — handled in Phase 4
- Changes to `.claude/harness-artifacts-index.md` — not needed (artifact-centric index; codebase-audit's routing targets are already registered there)
- Migration of pre-Phase-3 baselines in already-initialized project repositories — out of scope for the template itself; handled by ad-hoc PM action in downstream projects if needed
- Automatic engineering-review gating — FR-ER-2 is advisory, not blocking
- Auto-routing of §9 Open Questions — they are PM-facing, not artifact-facing (FR-R-7)
- Design-aware classification using Figma context — future enhancement
- Reading `project-stakeholders.md` or existing `FEAT-NNN-*.md` spec files at context-load time — excluded by design: stakeholder sentiment doesn't directly shape codebase analysis, and scope-file IDs are sufficient for FEAT-NNN collision avoidance without deep feature reads
