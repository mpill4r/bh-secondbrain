# product-codebase-audit — Skill Logic

> Analyzes an existing codebase from a product perspective, produces a structured product baseline, and — on PM confirmation — writes directly to harness artifacts. Two modes: **import mode** produces the baseline at `documents/internal/codebase-analysis/YYYY-MM-DD-{project-slug}-product-baseline.md` with `status: routing-preparation`; **route mode** re-reads harness context, reads the baseline in its current state, confirms routing with the PM, and flushes writes to harness artifacts, setting `status: routing-done`. Refresh mode re-runs the analysis against the current codebase and emits a new baseline with change tags.

---

## When This Skill Runs

| Invocation | Mode |
|------------|------|
| `/product-codebase-audit` | **Import mode** — access, orientation, harness context load, 3-pass analysis, baseline production. Repo URL resolved from `project-overview.codebase_repo` or prompted |
| `/product-codebase-audit {url-or-path}` | **Import mode** — same, with explicit URL or local path provided upfront |
| `/product-codebase-audit refresh` | **Refresh mode** — re-analyze against the most recent baseline; emit a new baseline with `[new]` / `[changed]` / `[status-changed]` / `[removed]` tags |
| `/product-codebase-audit route` | **Route mode** — re-read harness context; read existing baseline in current state (including PM edits); confirmation session; direct writes to harness |

---

## A. Pre-Orientation Filesystem Scan

Before asking anything, silently scan `documents/internal/codebase-analysis/` for prior baseline files (`*-product-baseline.md`). Capture filenames, each baseline's `status`, `codebase_repos` URLs, `codebase_snapshot_date`, most recent `last_updated`. Feeds the refresh-mode detection (Section D). Do not read harness files yet.

If the directory does not exist, note "no prior baseline" and proceed.

---

## B. Access

### B1. Resolve repo URL

Priority order:

1. **PM argument** (URL or local path) — use it.
2. **`project/management/project-overview.md`** — if it exists and `codebase_repo` frontmatter has a value other than `-tbd-`, offer it: "I see {repo URL} in project-overview. Analyze this repo?" PM confirms or overrides.
3. **Prompt directly**: "What's the GitHub repo URL for this project? You can provide multiple URLs if the product spans multiple repos, or a local file path."

### B2. Clone or access

For each GitHub URL:

1. `gh repo clone {url} {temp-dir}`. Default branch unless PM specified a branch or tag during orientation.
2. Verify by reading a top-level file (`README.md`, `package.json`, etc.).
3. On failure: "Unable to clone {url} — {error}. This may be a private repo. Verify you're authenticated with `gh auth status`." Suggest `! gh auth login` if relevant.
4. Invalid URL: "Repository {url} not found. Verify and try again." Stop.
5. Record HEAD SHA via `git rev-parse HEAD` for frontmatter.

For local paths:

1. Verify existence and non-emptiness. If missing/empty: "Path {path} not found or is empty." Stop.
2. Do not clone or copy — use the path directly.

### B3. Multi-repo

Accept multiple GitHub URLs. Orientation asks about additional repos conditionally if the PM gave only one and the product might span more.

### B4. Small-repo warning

If fewer than 10 source files: "This repo has very little content — {N} files. The baseline will be thin. Proceed?" PM confirms to continue or declines.

---

## C. Orientation

Ask three primary questions in a single conversational message:

1. **What is the current product state?** (active development / between phases / maintenance / other)
2. **What is the primary user-facing product this codebase serves?**
3. **Any areas to exclude from analysis** (deprecated, experimental, archived), or specific **focus areas** for deeper analysis?

**Conditional follow-ups**, asked only when relevant:

- Branch or tag representing the current production release (if the default isn't production)
- Additional repos (if multi-repo is possible and only one URL was provided)

**Let the orientation context shape subsequent analysis:**

- Product state → framing (active = forward-looking; maintenance = stability-focused)
- Exclusions → skipped during Pass 1 and Pass 2
- Focus areas → deeper in Pass 2
- Additional repos → cloned per Section B

---

## D. Refresh-Mode Detection

Using Section A's scan result and PM invocation:

- **`refresh` argument AND prior baseline exists** → enter refresh mode (Section J).
- **`refresh` argument AND no prior baseline** → "No prior baseline found — running as first-time analysis." Proceed as first-time.
- **Prior baseline exists AND PM did not pass `refresh`** → "Found existing baseline from {date} ({snapshot_sha}). Run as refresh (compare against prior and highlight changes) or full re-analysis (new baseline from scratch)?" PM decides.
- **Prior baseline's `codebase_repos` URLs differ from current** → "Prior baseline analyzed {old URL}, current repo is {new URL}. Treat as fresh analysis (different repo) or refresh (same project, new location)?" Default to fresh if PM is unsure.

---

## E. Harness Context Loading

After orientation (not before), read the following. Skip silently if any file is missing.

- `product/problem-space/product-brief.md` — existing product framing, personas, goals
- All `product/solution-space/product-scope-*.md` — existing FEAT-NNN IDs (for collision avoidance), epic structure, released features
- `product/problem-space/product-requirements.md` — existing REQ-NNN IDs (for cross-referencing PR entries)
- `project/management/project-assumptions.md` — existing ASM-NNN IDs (for cross-referencing DA entries)
- `project/management/project-knowledge.md` — known terminology (to avoid re-defining)
- `project/management/project-overview.md` — project and client context, `codebase_repo` field

**Tailor analysis depth** to orientation answers — product state, exclusions, and focus areas shape what Pass 1 and Pass 2 prioritize.

**Use loaded context to inform**: FEAT-NNN ID collision avoidance, "vs. existing harness" columns on §5 and §6, synthesis framing, routing target validation.

Do NOT re-read these files during analysis; they are re-read on route-mode entry (Section I).

---

## F. 3-Pass Analysis

### F1. Pass 1 — Skeleton

Read across all analyzed repos, adapting to the detected tech stack. Order:

1. **Package / dependency files**: `package.json`, `pnpm-workspace.yaml`, `turbo.json`, `nx.json`, `Cargo.toml`, `go.mod`, `pyproject.toml`, `Gemfile`, `build.gradle` — tech stack, workspace structure, dependencies.
2. **Documentation**: `README.md`, `CLAUDE.md`, `docs/`, `documentation/` — existing project docs.
3. **Deployment configs**: `wrangler.jsonc`, `Dockerfile`, `docker-compose.yml`, `serverless.yml`, `terraform/`, `k8s/`, `.github/workflows/` — deployment topology.
4. **Entry points**: `src/index.ts`, `src/main.ts`, `app/`, `pages/`, `routes/` — app entry and routing.
5. **Type / schema definitions**: `types/`, `models/`, `schemas/`, `prisma/`, `drizzle/`, `entities/` — domain entities.
6. **Route / handler definitions**: `routes/`, `controllers/`, `handlers/`, `api/`, `resolvers/` — capability surface.
7. **GitHub activity** (skip for local paths): `gh release list`; `gh pr list --state merged --limit 20`; `gh pr list --state open`.

Goal: tech stack identified, architecture shape understood, domain areas enumerated, capabilities surface mapped, recent activity understood. **No deep git history** — commit depth, blame, branch evolution are out.

### F2. Pass 2 — Domain Depth

For each major domain area from Pass 1, extract:

- **Capabilities** — what users can do
- **Business rules and invariants** — what constraints govern behavior
- **Design decisions** — why things are built the way they are
- **Domain terminology** — jargon and concepts
- **Gaps and anomalies** — half-built features, schema-defined-but-not-implemented, dead code
- **Feature boundaries** — module/package boundaries, route groups, entity clusters, UI page groups forming coherent features
- **Permission / role matrix** — role definitions, permission mappings, route guards, UI conditionals

Every extracted claim MUST have a source reference (`file.ts:42-58`, or minimum `file.ts`).

**Parallelization**: If the codebase has >10 packages or >50 top-level source dirs, use Explore subagents across 5-8 domain areas in parallel. Otherwise sequential.

**Context-limit handling**: If limits hit during Pass 2, complete what's possible and note partial coverage in §1 and the PM handoff message.

**Non-English codebases**: Analyze in original language; output English; mark translated quotes `[translated from {language}]`.

### F3. Pass 3 — Synthesis

Combine findings into the 9-section baseline. **Synthesis ordering matters — sections have dependencies:**

**Phase 3a — Derive features first (§8).** Establishes FEAT-NNN IDs needed by dependent sections.

1. Structure capabilities into epics using domain area names (not code module names). Target 20-50 features for a mature product.
2. Assign FEAT-NNN IDs sequentially, avoiding collision with existing scope IDs (from Section E).
3. Write rich multi-sentence descriptions: what it does + key rules/complexity + inline FEAT-NNN dependency refs. Single-phrase descriptions are not acceptable.
4. Determine status from code signals: full implementation with tests/UI → `released`; partial (service, no UI) → `in development`; schema/types only → `defined`.
5. Set Design Status to `unknown` for all FEATs (code cannot reveal design status).
6. **Assign type per Phase 1 vocabulary**: default `feature`; `tech` when the FEAT is infrastructural; other vocabulary values (`bug`, `spike`, `other`) accepted when signals warrant.
7. Leave Linear IDs blank and use Notes for code-derived context (module references, related FEAT links).

**Phase 3b — Cross-reference dependent sections (§5, §7).**

**§5 — Product Rules & Requirements (PR-NNN)**:

1. Assign sequential PR-NNN IDs.
2. Classify each entry: `REQ` (routes to `product-requirements` — "system must/should/shall" statements or measurable outcomes) or `Knowledge` (routes to `project-knowledge` — how a domain concept works).
3. For `REQ` entries, populate `Addressed in` with the FEAT-NNN(s) from §8 that implement it. Unmapped REQ may indicate a missing feature in §8.
4. Populate `vs. existing harness` using the relationship vocabulary: `confirms REQ-NNN`, `confirms ASM-NNN`, `refines REQ-NNN`, `refines ASM-NNN`, `new — not captured`, `contradicts REQ-NNN`. If no harness artifacts exist yet, mark all as `new`.
5. Group by domain area or rule category.

**§7 — Product Gaps & Anomalies**:

1. Classify each gap: `deferred` (partial code exists — TODOs, empty impls, schema-defined-but-not-built) or `future-idea` (no code signal; inferred from domain patterns or missing capability).
2. Assign each gap to the most relevant epic from §8.
3. List general anomalies and failure modes separately.

**Phase 3c — Independent sections (any order).**

- **§1 Product Summary** — end-user perspective.
- **§2 Inferred Personas** — persona table with confidence tags; Role × Capability Matrix from permission/role data. Pain Points and Success Looks Like are always `-tbd-`.
- **§3 Architectural & Technical Boundaries** — fact → implication format; product-relevant only.
- **§4 Domain Language** — each entry classified `project-specific` or `domain-standard`; both route to `project-knowledge` (specificity is metadata, not a routing filter).
- **§6 Decisions & Assumptions (DA-NNN)** — sequential IDs, cross-referenced against existing ASMs using the same relationship vocabulary as §5.
- **§9 Open Questions** — combine questions and missing info. Assign Owner (Client / Engineering / Legal / PM) and Impact (High / Medium / Low).

If multiple repos were analyzed, note the source repo for findings where the distinction matters.

---

## G. Content Rules

Apply these rules to all baseline content. Violations should not reach the baseline.

1. **No fabrication.** Code reveals *what* and *how* — never *who*, *why*, or *what frustrates*. Do not fabricate user experience, business motivation, or stakeholder intent.
2. **Product lens only.** A sentence useful only to an engineer is excluded. A sentence that helps a PM make a product decision, scope a feature, or prepare a client conversation is included.
3. **No file paths in narrative sections.** File paths appear only in Source columns of PR/DA tables and in the Scope Note.
4. **No engineering-only content.** No architecture diagrams, dependency graphs, code quality metrics, test coverage, implementation recipes.
5. **Confidence tags on every persona inference.** Pain Points and Success Looks Like are always `-tbd-`.
6. **Source reference on every PR/DA entry.** Absence of a code reference means absence from the baseline.
7. **Fact → implication format for §3.** Facts without product implications are excluded.
8. **Illustrative details flagged** as "illustrative — not confirmed with stakeholders."
9. **Feature granularity** — target 20-50 features for a mature product. Epic names come from domain areas, not code modules.
10. **Rich §8 feature descriptions** — multi-sentence (what + rules + inline FEAT-NNN dependency refs). Single-phrase descriptions not acceptable.
11. **PR-NNN routing hints** — every entry tagged `REQ` or `Knowledge`.
12. **§4 specificity classification** — every entry tagged `project-specific` or `domain-standard`; both route to project-knowledge.
13. **§7 gap classification** — every gap tagged `deferred` or `future-idea`.

---

## H. Baseline Production

### H1. Write the baseline

Write to `documents/internal/codebase-analysis/YYYY-MM-DD-{project-slug}-product-baseline.md`.

- Date = today's analysis date.
- Project slug from `project-overview.md` project name if available; else from orientation context.
- **Create the directory** `documents/internal/codebase-analysis/` if missing.
- **Multi-repo** → single unified document (not one per repo).

Use TEMPLATE.md. All 9 sections always present; sections with no findings include a note explaining why (e.g., "No regulatory content identified in the codebase").

### H2. Frontmatter

Set on initial creation:

- `status: routing-preparation`
- `classification: Codebase Analysis`
- `source: internal`
- `codebase_repos` — list of analyzed repos with URL and HEAD SHA per repo
- `codebase_snapshot_date: {today}`
- `last_updated: {today}`
- `last_updated_by: auto — product-codebase-audit`
- `audience: harness AI first, PM second`
- `superseded_by:` (empty on initial create; populated only by refresh mode on a previously-written baseline)

### H3. Documents index

Add an entry to `documents/index.md`: ingestion date (today), title `{Project} Product Baseline`, source `internal`, classification `Codebase Analysis`, summary file link, first 2 sentences of §1 as excerpt, original location (GH repo URL(s)). Create `documents/index.md` with appropriate headers if it does not exist.

### H4. Project overview sync

If `project-overview.md` exists:

- Read its `codebase_repo` frontmatter.
- If the field is `-tbd-` or empty, set it to the analyzed repo URL(s).
- If it has a different value, ask PM: "project-overview currently lists {old URL} as the codebase repo. Update to {new URL}?"
- If project-overview does not exist, skip silently.

### H5. Audit entry

Log to today's `project-daily`:

`[AUTO] product-codebase-audit — product baseline written for {repo URL(s)} ({date})`

Create today's daily from `project-daily/TEMPLATE.md` if it does not exist.

### H6. Engineering review suggestion

After baseline production, count items that could benefit from engineering validation: §6 DA entries with open/uncertain status, §7 gaps, any PR/DA entries where the code signal was thin.

If any exist, surface to PM:

> "There are {N} items in the baseline that an internal engineer could validate in a short review — {X} open decisions, {Y} product gaps, {Z} low-confidence claims. Want to hold routing until an engineer reviews, or proceed and circle back later?"

PM decides — **advisory, not a gate**. Never block the skill on engineering review.

### H7. Handoff message

Present a routing summary: item counts by section, route-mode guidance ("Run `/product-codebase-audit route` to write findings into harness artifacts"), and the engineering-review suggestion (H6) if applicable.

If the harness has no foundational artifacts (no `project-overview`, no `product-brief`), note: "It looks like `/project-initiation` hasn't been run yet. Consider running it before routing — it creates the target artifacts that routing writes to."

### H8. Session-end guidance

If the session ends before PM starts routing, surface clear resume guidance:

> "The baseline is saved at `{path}` with status `routing-preparation`. When you're ready to continue, run `/product-codebase-audit route`."

### H9. Temp cleanup

After all output is written, delete temporary clone directories.

- Local paths are not deleted.
- If cleanup fails: "Unable to clean up temp directory at {path}. Please remove manually."

---

## I. Route Mode

Triggered by `/product-codebase-audit route`. Reads an existing baseline and writes harness artifacts on PM confirmation.

### I1. Re-read harness context

Re-read the files listed in Section E. Context may have changed between baseline production and the route session — do not trust the import-time snapshot.

### I2. Read the baseline in its current state

Load the most recent baseline with `status: routing-preparation` from `documents/internal/codebase-analysis/`. Read in full, including any PM manual edits made between sessions.

If no baseline has `status: routing-preparation` but a `routing-done` baseline exists, offer to re-route: "The latest baseline is already `routing-done`. To route additional findings, set its status back to `routing-preparation` (or I can do that for you), then re-run me. Want me to flip the status?"

### I3. Routing confirmation session

Walk the PM through proposed writes section by section. For each, show: target artifact, what will be written, which baseline section it comes from. PM confirms, adjusts inline, or skips per item. No writes before explicit confirmation.

### I4. Missing target scope phase — autonomous creation

If `product-scope-{phase-slug}.md` referenced in the routing plan does not exist, propose phase metadata derived from source context:

- **Phase slug** — from project context, PM's orientation answer about the primary product, or release-tag signals from `gh release list`
- **Phase focus** — 1-line description from dominant code-derived capabilities in §8
- **Target release** — almost always `-tbd-` for codebase-audit (code does not reveal forward timelines; inferable only from scheduled-release signals if present)
- **Key outcomes** — 2-3 bullets from dominant capability themes in §8

Surface the full proposal during routing confirmation. On PM confirmation, invoke `product-scope`'s full create-mode flow (Section A of `product-scope/SKILL.md`) — including canonical feature-table structure, product-area description paragraphs, Suggested Spec Order population, AND Section E outbound routing (which syncs the new phase to `product-brief` Section 8 High-Level Phasing under the bidirectional-sync-gated rule). Log an audit entry.

### I5. Writes

On confirmed routing, write directly. **No handoff to `/project-document`** — the skill has full context.

Write paths:

- **`product/problem-space/product-brief.md`** — §1 Product Summary informs strategic framing; §2 Personas route to the brief's persona section (**surface for PM section-by-section confirmation before overwriting existing personas**); §3 product implications inform solution definition. Do not auto-overwrite; PM approves each update.
- **`product/solution-space/product-scope-{phase-slug}.md`** — §8 FEATs (typed per Phase 1; mostly `released` for brownfield) written to the canonical feature table. §7 `deferred` gaps → Deferred Scope section. §7 `future-idea` → Future Ideas section. **Notes writes append (never overwrite)** per Phase 1 FR-PS-7 with source tag `[product-codebase-audit {date}]`.
- **`product/solution-space/product-scope-{phase-slug}.md` Suggested Spec Order** — propose order for any new FEATs added via this route; PM confirms (Phase 1 FR-PS-6). The routing confirmation session satisfies the PM-confirmed-write rule.
- **`product/problem-space/product-requirements.md`** — §5 entries tagged `REQ`. Add as new REQ entries or cross-reference existing (based on baseline's `vs. existing harness` column); preserve `confirms`/`refines` relationships as notes. Continue the existing REQ-NNN ID sequence.
- **`project/management/project-knowledge.md`** — §4 domain language entries; §5 entries tagged `Knowledge`. Continue the existing entry format.
- **`project/management/project-assumptions.md`** — §6 DA entries. Add new ASM-NNN or cross-reference existing. Continue the existing ASM ID sequence.
- **`project/management/project-overview.md`** — `codebase_repo` field (confirm or update per H4); `product_state` signals from §1.
- **`documents/index.md`** — baseline entry (already written in H3 during import mode; on route this is only updated if metadata changed).
- **`project-daily`** — audit entry per write with format `[AUTO] product-codebase-audit — {what changed} ({date})`. Create today's daily from TEMPLATE if missing.

Before writing to any target, read its TEMPLATE.md (at `.claude/skills/{owner-skill}/TEMPLATE.md`) for the entry format; continue the existing ID sequence; place entries in the correct section.

### I6. Open Questions handling

**§9 Open Questions do NOT auto-route.** They are PM-facing queries carried forward until resolved. Surface them during the routing confirmation session for PM to address (typically noted in project-daily or routed manually).

### I7. Status update

On successful writes, update baseline frontmatter: `status: routing-done`, `last_updated: {today}`, `last_updated_by: auto — product-codebase-audit`.

### I8. Iterative route sessions

Multiple route-mode sessions on the same baseline are valid. The PM may confirm a subset, close, and resume. Support this without destroying prior state — mark routed items in the baseline as `[routed {date}]` so the next session's confirmation focuses on the remaining entries.

### I9. Manual re-route after routing-done

If the PM wants to route additional items after `status: routing-done`, they may set the status back to `routing-preparation` and re-run route mode. Support this flow.

---

## J. Refresh Mode

Triggered when a prior baseline exists and the PM confirmed refresh (Section D).

### J1. Read the prior baseline

Read fully — all 9 sections, frontmatter, PR/DA entries, features. Compare `codebase_repos` URLs with current. If URLs differ, confirm per Section D (default to fresh on uncertainty).

### J2. Run analysis

Run the same analysis as first-time (Sections B through F). Orientation still runs — product state may have changed since the prior audit.

### J3. Compare during synthesis

During Pass 3 (Section F3), compare findings against the prior baseline.

**Feature-level**: new / changed (description / rules / dependencies) / removed / status changes.

**PR/DA-level**: new / changed / unchanged / gaps addressed.

### J4. Emit the new baseline with change markers

Produce a new baseline with a **`Changes since last baseline`** section inserted after the Scope Note and before §1:

- Summarize feature additions, changes, removals, status changes
- Summarize PR/DA additions and changes
- Reference the prior baseline filename and date

**Tag items in the baseline body:**

- `[new]` — PR/DA entries and features added since prior
- `[changed]` — PR/DA entries or features whose content changed
- `[status-changed]` — features whose status changed
- `[removed]` — items in prior baseline but no longer in code

### J5. Supersede the prior baseline

Update the prior baseline's frontmatter: `superseded_by: {new-baseline-filename}`. This is a targeted edit — do not modify other content in the prior baseline.

### J6. Hand off

Follow Section H (write baseline, update index, log audit, handoff message). In the handoff message, note: "This is a refresh — routing review should focus on new and changed items (marked `[new]`, `[changed]`, and `[status-changed]`)."

---

## K. Rules

- **No write-back to the source repo** — forbidden. Strictly read-only against the source.
- **No fabrication** — code reveals *what* and *how*, never *who*, *why*, or *what frustrates*. Persona pain points, success criteria, and stakeholder motivations are always `-tbd-`. When inferring beyond direct code evidence (personas), mark the inference with a confidence tag.
- **Product lens only** — exclude engineering-only content. Test: would this sentence help a PM make a product decision? If not, exclude.
- **Source reference on every PR/DA** — no reference means absence from the baseline.
- **No file paths in narrative** — only in Source columns of PR/DA tables and in the Scope Note.
- **`-tbd-` over guessing** — unknown fields are `-tbd-`, never guessed.
- **All 9 sections always present** — sections with no findings include an explanation note.
- **Baseline frontmatter lifecycle** — `status: routing-preparation` (default on create) → `status: routing-done` (after confirmed writes). PM may manually flip back to re-route.
- **Frontmatter never carries `routing: ready-for-routing`** — the mechanism it triggered in `/project-document` is removed; the field has no meaning.
- **`classification: Codebase Analysis` is metadata-only** — written for the `documents/index.md` classification column and general document identification. It has no routing consumer after Phase 3 removed the matching branch in `/project-document`. Do not treat it as a routing instruction.
- **Route mode never hands off to `/project-document`** — the skill has full context and writes directly.
- **Single unified baseline** — multi-repo analysis produces one document. Source repo noted where the distinction matters.
- **FEAT-NNN IDs avoid collision with existing scope** — check all scope files (via Section E) for the highest ID and continue from there.
- **Features are typed per Phase 1 vocabulary** — default `feature`; `tech` when infrastructural. Custom types accepted per Phase 1 NFR-1 if the PM has previously introduced them.
- **Canonical feature-table columns** — §8 uses the Phase 1 canonical column order.
- **Notes column writes always append, never overwrite** — source tag prefix `[product-codebase-audit {date}]`.
- **product-brief personas are never auto-overwritten** — PM section-by-section confirmation required.
- **Open Questions (§9) do NOT auto-route** — PM-facing only; addressed during confirmation.
- **Every harness write produces an audit entry** in today's `project-daily` (format `[AUTO] product-codebase-audit — {what changed} ({date})`). Create daily from TEMPLATE if missing.
- **Preserve existing content** — targeted section/field writes only; never rewrite surrounding content.
- **English output** — all baseline content in English regardless of codebase language. Translated quotes marked `[translated from {language}]`.
- **Machine-readable first** — consistent section headers, table formats, and ID conventions enable reliable downstream routing.
- **No deep git history analysis** — recent releases and merged PRs only. No commit depth, blame, branch evolution.
- **Large codebase handling** — >10 packages or >50 top-level source dirs triggers Explore subagent parallelization in Pass 2.
- **Context-limit partial coverage is acceptable** — complete what's possible, note in §1 and in the handoff.
- **Staleness signal** — `codebase_snapshot_date` in frontmatter lets downstream skills warn if the baseline is older than 3 months.
- **Temp directories cleaned up** — cloned repos deleted after all output is written. Local paths are not deleted.
- **Engineering review is advisory, not a gate** — never block the skill on engineering validation.
- **Harness context file missing → skip silently** — proceed with what's available (FR-CL-2).
