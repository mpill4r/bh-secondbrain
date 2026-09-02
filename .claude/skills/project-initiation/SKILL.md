# project-initiation — Skill Logic

> The entry point for every new project. The PM provides free-text context in a conversational exchange, and the skill autonomously creates all foundational artifacts — stakeholders, client intelligence, project overview, product brief, project encyclopedia, and skeleton files for assumptions, lessons, and requirements.

---

## When This Skill Runs

This skill runs once per project when the PM invokes `/project-initiation`. It collects PM input in two conversational beats, then autonomously creates all foundational artifacts across 5 phases.

---

## A. Beat 1 — Context Collection

### A1. Present the Prompt

Present a structured context collection prompt with 5 areas:

> **Let's set up your project. Share what you know across these areas — just free text for now. Don't upload any documents yet; we'll do that as the next step after setup.**
>
> 1. **Client & project** — client name and project name
> 2. **People involved** — who's on the internal team? Who are the key people on the client side? Names and roles if known.
> 3. **Project assignment** — what are the project goals? Any known milestones, timeline, or deliverables?
> 4. **Product state** — is this a brand new product (greenfield) or does a codebase already exist (brownfield)? If there's an existing codebase: what's the GitHub repository URL?
> 5. **Anything else** — any other context you want to share at the start.

Do not interrupt or redirect the PM during Beat 1. Accept their response as a single free-text message of any length.

### A2. Parse the Response

From the PM's response, extract:
- Client name
- Project name
- Stakeholder names — classify as internal or client/external where possible
- PM's own name (if identifiable)
- Project goals, milestones, timeline signals
- Problem signals, target user signals
- Product state: greenfield (new product) or brownfield (existing codebase). Default to greenfield if not mentioned.
- Codebase repository URL(s) — one or more GitHub URLs if brownfield
- Any other context (competitive landscape, existing solutions, domain terminology)

---

## B. Beat 2 — Gap Fill

### B1. Evaluate Gaps

After parsing Beat 1, evaluate what's missing. Typical critical gaps:
- PM's own name (if not mentioned or not identifiable from context)
- Problem being solved and target users (if Beat 1 focused on logistics/timeline without describing the product problem)
- Internal vs client classification of people (if ambiguous from Beat 1)
- GitHub repository URL (if PM indicated brownfield but didn't provide a repo URL)

### B2. Ask or Skip

- If critical gaps exist, ask a **single follow-up message** covering all gaps. Do not ask multiple rounds of questions — one message, all gaps.
- If Beat 1 provided enough context to fill all critical fields, skip Beat 2 entirely and move directly to creation.

### B3. Announce and Proceed

After Beat 2 (or after Beat 1 if Beat 2 was skipped), announce: "Setting up your project — creating all foundational artifacts." Then proceed autonomously. No further PM interaction until the completion summary — except for existing file conflicts (see Section H).

---

## C. Phase 0 — Infrastructure and Skeletons

### C1. Create Folders

Create all project folders. Skip existing folders silently.

```
project/management/
project/daily/
project/weekly/
product/problem-space/
product/solution-space/
product/solution-space/features/
meetings/
meetings/internal/
meetings/client/
meetings/external/
meetings/milestone/
meetings/prep/
documents/
documents/internal/
documents/client/
documents/external/
```

### C2. Personalize CLAUDE.md

Read `CLAUDE.md`. Replace the `{project-name}`, `{client-name}`, and `{pm-name}` placeholders in the "What This Harness Is" section with actual values from Beat 1/2. If any value is still unknown, leave the placeholder as-is.

Log audit entry: `[AUTO] project-initiation — personalized CLAUDE.md ({date})`

### C3. Create Today's Daily

Check for existing file conflict (Section H). Create today's `project-daily` using the project-daily TEMPLATE.md at `project/daily/project-daily-YYYY-MM-DD.md`.

Set:
- `project_status`: `:green_circle: Green — project initiated`
- Current Priority: "Complete project setup — upload documents, enrich client overview."
- `last_updated_by: auto — project-initiation`

If today's daily already exists, append audit entries to the existing daily instead of creating a new one.

Log audit entry: `[AUTO] project-initiation — created project-daily ({date})`

### C4. Create Skeleton Files

For each of the following, check for existing file conflict (Section H), then create using the respective template with empty entries:

1. **`project/management/project-assumptions.md`** — use project-assumptions TEMPLATE.md. Structure present, no entries.
2. **`project/management/project-lessons.md`** — use project-lessons TEMPLATE.md. Structure present, no entries.
3. **`product/problem-space/product-requirements.md`** — use product-requirements TEMPLATE.md. Structure present, no entries.

Set frontmatter on each: `last_updated: {today}`, `last_updated_by: auto — project-initiation`, `owner: {PM name}`.

Log audit entry for each: `[AUTO] project-initiation — created {artifact-name} ({date})`

### C5. Create Index Files

Check for existing file conflict (Section H) for each.

**`meetings/index.md`**:
```markdown
# Meeting Index

| Date | Type | Title | Attendees | TL;DR | File |
|------|------|-------|-----------|-------|------|
```

**`documents/index.md`**:
```markdown
# Document Index

| Date | Title | Source | Classification | Summary | File |
|------|-------|--------|---------------|---------|------|
```

Log audit entry for each: `[AUTO] project-initiation — created meetings/index ({date})` and `[AUTO] project-initiation — created documents/index ({date})`

### C6. Replace README.md

Check for existing file conflict (Section H). Replace `README.md` with a project-specific version containing:

- **Project identity**: project name, client name, PM name
- **Available commands**: full commands table (same as CLAUDE.md)
- **Typical workflow**: the 8-step workflow guide:
  1. Start a session — Claude reads the latest daily and briefs you
  2. Upload documents — `/project-document` to ingest SoWs, PRDs, decks
  3. Upload meetings — `/project-meeting-upload` to process transcripts and notes
  4. Enrich artifacts — `/client-overview`, `/product-brief`, `/project-knowledge`
  5. Define scope — `/product-scope {phase-slug}` when ready to plan delivery
  6. Specify features — `/product-feature FEAT-NNN` for implementation-ready specs
  7. Review status — `/project-daily` for today, `/project-weekly` for the week
  8. Close the day — `/project-daily close` to wrap up and capture lessons
- **Repository structure**: simplified folder map
- **Team**: names and roles from PM input (from `project-stakeholders.md` entries created in this initiation)

Log audit entry: `[AUTO] project-initiation — replaced README.md ({date})`

### C7. Create Stakeholders

Check for existing file conflict (Section H). Create `project/management/project-stakeholders.md` using the project-stakeholders TEMPLATE.md.

For each person mentioned by the PM:
- Assign sequential ID: `STK-001`, `STK-002`, ...
- Fill: name, role (if provided), classification (Internal Team or External Stakeholders section)
- All other fields: `-tbd-`
- Status: `Active`

No web research. No PM interaction.

If the PM's name is still unclear after Beat 2, mark the PM's stakeholder entry with `> Needs confirmation — verify PM identity`.

Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — project-initiation`, `owner: {PM name}`.

Log audit entry: `[AUTO] project-initiation — created project-stakeholders ({date})`

---

## D. Phase 1 — Client Overview

Check for existing file conflict (Section H). Create `project/management/client-overview.md` using the client-overview TEMPLATE.md.

Populate sections from PM-provided context only:
- Sections 1-7: fill from Beat 1/2 context (client name, business context, project goals). Fields without data are `-tbd-`.
- Section 8 (Stakeholder Map): thin index referencing `project-stakeholders.md` — list client/external stakeholders only (ID, name, role).
- Sections 9-12: fill from PM context where available, `-tbd-` otherwise.

Do NOT offer or perform web research. Web research is deferred to the first `/client-overview` session.

Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — project-initiation`, `owner: {PM name}`.

Creation completes silently. Log audit entry: `[AUTO] project-initiation — created client-overview ({date})`

---

## E. Phase 2 — Project Overview

Check for existing file conflict (Section H). Create `project/management/project-overview.md` using the project-overview TEMPLATE.md.

Read `project/management/client-overview.md` as primary data source (it was just created in Phase 1).

Populate:
- Project name, client name, PM name
- Team structure from `project-stakeholders.md`
- Goals and timeline from PM context
- Client profile sections from `client-overview.md`
- `product_state` frontmatter: set to `greenfield` or `brownfield` based on Beat 1/2 input. Default to `-tbd-` if not mentioned.
- `codebase_repo` frontmatter: set to the GH repo URL(s) if brownfield and URL was provided. Otherwise leave as `-tbd-`.
- Fields without data: `-tbd-`

Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — project-initiation`, `owner: {PM name}`.

Creation completes silently. Log audit entry: `[AUTO] project-initiation — created project-overview ({date})`

---

## F. Phase 3 — Product Brief

Check for existing file conflict (Section H). Create `product/problem-space/product-brief.md` by following the product-brief skill's **Auto-Creation** mode (Section B in the product-brief SKILL.md).

That mode reads `client-overview.md` and `project-overview.md`, aggressively pre-fills every section from available PM context, and handles field uncertainty with `-tbd-` and `> Needs confirmation` notes.

Key rules during initiation:
- **Section 1 (North Star)**: always `-tbd-` — requires PM synthesis.
- **Sections 2-3**: if PM's input didn't describe problem or target users, mark `-tbd-` with `> Needs confirmation — PM did not provide problem definition or target user details during initiation. Enrich via /product-brief.` Do NOT ask additional questions.
- Do NOT perform web research.
- Complete silently — no summary, no prompts.
- Fire outbound routing per product-brief SKILL.md Section D (goals/problem → `project-overview`, engagement goals → `client-overview`). If target files do not exist, skip silently.

Log audit entry: `[AUTO] project-initiation — created product-brief ({date})`
Log separate audit entries for each outbound routing write.

---

## G. Phase 4 — Project Knowledge

Check for existing file conflict (Section H). Create `project/management/project-knowledge.md` using the project-knowledge TEMPLATE.md.

Read all previously created foundational artifacts:
- `project/management/client-overview.md`
- `project/management/project-overview.md`
- `project/management/project-stakeholders.md`
- `product/problem-space/product-brief.md`

Pre-populate the 9 fixed sections with any domain terminology, client jargon, or project-specific terms found in PM context and these artifacts.

Do NOT propose dynamic sections during initiation. There is typically insufficient context. Dynamic sections are deferred to the first `/project-knowledge` session.

Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — project-initiation`, `owner: {PM name}`.

Creation completes silently. Log audit entry: `[AUTO] project-initiation — created project-knowledge ({date})`

---

## H. Existing File Handling

Before creating each artifact, check whether the target file already exists. If it does:

Ask the PM: "{artifact-name}.md already exists. Overwrite, skip, or review and merge?"

- **Overwrite**: replace with the newly created version.
- **Skip**: preserve the existing file as-is. Move to the next artifact. Log: `[AUTO] project-initiation — skipped {artifact-name} (already exists) ({date})`
- **Merge**: read the existing file, show the PM a comparison of existing vs new content, and let the PM decide what to keep. Write the merged version.

This is the only PM interaction between Beat 2 and the completion summary.

Folder creation (Phase 0 C1) is always idempotent — existing folders are never overwritten or removed. No PM prompt needed for folders.

If today's project-daily already exists, append audit entries to it rather than creating a new one. No PM prompt needed.

---

## I. Completion Summary

After all artifacts are created, present the completion summary.

### Part 1 — What Was Created

List each artifact with its population status:

| Artifact | Status |
|----------|--------|
| `project-daily` | Created — initial status set |
| `project-stakeholders` | Created — {N} entries from PM input |
| `project-assumptions` | Skeleton ready |
| `project-lessons` | Skeleton ready |
| `product-requirements` | Skeleton ready |
| `meetings/index` | Created — empty |
| `documents/index` | Created — empty |
| `README.md` | Replaced with project-specific version |
| `CLAUDE.md` | Personalized — placeholders replaced |
| `client-overview` | Created — {N} of 12 sections populated, {M} gaps |
| `project-overview` | Created — {N} of 11 sections populated, {M} gaps |
| `product-brief` | Created — {N} of 8 sections populated, {M} gaps |
| `project-knowledge` | Created — {N} entries across {M} sections |

For skipped artifacts (existing file conflicts), show: "Skipped — already existed."

### Part 2 — What to Do Next

Present prioritized follow-up actions. The list depends on whether the project is greenfield or brownfield.

**If brownfield:**

1. **Upload project documents** — `/project-document` — SoW, PRD, proposals, contracts, strategy decks. Loading critical documents first makes every downstream skill smarter.
2. **Upload past meetings** — `/project-meeting-upload` — kickoff transcripts, discovery notes, past calls. Feed as much early-context data as possible before the codebase audit.
3. **Analyze the codebase** — `/product-codebase-audit` — two-mode skill: the default run produces a product baseline at `documents/internal/codebase-analysis/…` with `status: routing-preparation`; review, adjust, then run `/product-codebase-audit route` to write findings into harness artifacts (product-brief, product-scope, product-requirements, project-knowledge, project-assumptions, project-overview) and flip the baseline to `status: routing-done`.
4. **Enrich the product brief** — `/product-brief` — coaching session to deepen problem definition, personas, and goals, now with full context (docs, meetings, codebase) already loaded.
5. **Import the backlog** — `/product-backlog-import` — two-mode skill. Run this after the above steps so the skill can reason about groupings, velocity, and priority with full context — running it cold produces weaker proposals. The default run produces a backlog import plan at `documents/internal/backlog-import/…` with `status: routing-preparation`; review, adjust, then run `/product-backlog-import route` to write FEATs into scope and flush velocity insights, lessons, assumptions, and terms into their target artifacts.
6. **Define or polish delivery scope** — `/product-scope {phase-slug}` — once the audit and backlog-import route passes have landed initial scope structure, polish rather than author from scratch.
7. **Enrich client profile** — `/client-overview` — fill gaps in client intelligence last; least dependency-creating step and includes optional web research.

**If greenfield (or product state not specified):**

1. **Upload project documents** — `/project-document` — SoW, PRD, proposals, contracts, strategy decks. Each document automatically enriches the artifacts just created.
2. **Enrich client profile** — `/client-overview` — fill gaps in client intelligence, includes optional web research.
3. **Upload past meetings** — `/project-meeting-upload` — kickoff transcripts, discovery notes, earlier call recordings.
4. **Enrich the product brief** — `/product-brief` — coaching session to deepen problem definition, personas, and goals.
5. **Define delivery scope** — `/product-scope {phase-slug}` — when ready to define what gets built, in what order.

### Part 3 — Session Summary to Daily

Append a session summary to today's `project-daily` Key Events:

"Project initiated for {client name} / {project name}. Created {N} artifacts ({M} with content, {K} skeletons). PM follow-up actions: upload documents, enrich client overview."

The completion summary is the final output of `/project-initiation`. After presenting it, the skill is done.

---

## J. Audit Entry Format

Every artifact created during initiation is logged to today's `project-daily` Audit Log:

`[AUTO] project-initiation — created {artifact-name} ({date})`

For skipped artifacts:
`[AUTO] project-initiation — skipped {artifact-name} (already exists) ({date})`

For outbound routing writes triggered by product-brief creation:
`[AUTO] product-brief — {target section} updated from project-initiation ({date})`

---

## Rules

1. **Two beats maximum** — Beat 1 collects context, Beat 2 fills gaps. No third round. If data is still missing after Beat 2, create artifacts with `-tbd-`.
2. **Beat 1 is conversational, not a form** — welcoming, natural language. The PM should feel invited to share context freely.
3. **Beat 2 is a single message** — one follow-up covering all gaps. Never multiple rounds.
4. **No documents during initiation** — the Beat 1 prompt explicitly states "don't upload any documents yet." If the PM uploads a document despite the instruction, accept it gracefully, use it as additional context, and note in the completion summary that it wasn't formally processed via `/project-document`.
5. **No web research during initiation** — do not offer or perform web research. It is deferred to the first `/client-overview` session and listed as a follow-up action.
6. **No dynamic section proposals for project-knowledge** — deferred to the first `/project-knowledge` session.
7. **`-tbd-` over fabrication** — fields without reliable data are always `-tbd-`. Never infer beyond what the PM explicitly stated.
8. **Autonomous between beats and summary** — no PM interaction during Phases 0-4, except for existing file conflicts (Section H).
9. **All frontmatter uses standard fields** — `last_updated`, `last_updated_by: auto — project-initiation`, `owner: {PM name}`. Only `project-daily` and `project-weekly` use `status` in frontmatter (lifecycle artifacts with open/closed or draft/confirmed states).
10. **Phase order matters** — Phase 0 → 1 → 2 → 3 → 4. Later phases read artifacts created in earlier phases. Do not reorder.
11. **Partial creation failure** — if an artifact creation fails (e.g., write error), log the failure, continue with the next artifact, and report the failure in the completion summary. Re-running `/project-initiation` is safe due to existing file handling (Section H).
12. **Completion summary must be scannable** — the PM should immediately see what exists and what to do next.
13. **Product-brief fires outbound routing on creation** — per product-brief spec, goals/problem route to `project-overview` and engagement goals route to `client-overview`. This happens silently during Phase 3.
