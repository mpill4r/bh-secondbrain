# product-client-spec — Skill Logic

> A client-facing development specification (Czech `.docx`, BigHub house style) for one initiative/stream — e.g. `1. Listing`, `2. Fakturace doprav`, `3. Reklamace`. Works like `/product-feature`: the skill gathers everything the harness and the source files already know about the initiative, asks the PM only about the gaps, and then builds the spec from the clean template. It encodes how the PM has built these specs before (Fakturace doprav rebuild 2026-09-16 + redline 2026-09-23, Listing client version 2026-09-17).

---

## When This Skill Runs

- PM invokes `/product-client-spec` (optionally with an initiative name, e.g. `/product-client-spec Reklamace`).
- PM says anything with the same intent — "start a new spec", "let's continue with the spec for X", "rebuild the X spec", "make a client version of the X spec".

---

## A. Intake (always first)

### A1. Identify the initiative

If the PM gave a name, match it against existing folders in the spec root (`~/Library/CloudStorage/OneDrive-BigHubs.r.o/1. Feature Specs/`) and against the initiative names in `project/management/project-knowledge.md`. If no name was given, ask for it.

Then detect the mode:
- **CREATE** — no `{N}. {Name}/` folder / no spec docx exists yet.
- **REBUILD** — a spec exists but the PM wants it rebuilt from the originals (e.g. "it's completely wrong").
- **UPDATE / REVIEW** — a spec exists; apply new information or the PM's review comments (redline flow, Section E).
- **CLIENT VERSION** — produce the external copy of a finished internal spec (Section F).

Confirm the detected mode in one line before continuing.

### A2. Pre-populate from the harness (silently)

Before asking anything, collect what the harness already knows about the initiative:
- `project/management/project-knowledge.md` — every entry for the initiative (business objective, phasing, data sources, naming conventions).
- `project/management/project-assumptions.md` — all ASM entries mentioning the initiative (decisions = facts for the spec; Open = open questions).
- `project/management/project-stakeholders.md` — business owner, domain expert, approvers, dev owner.
- `meetings/index.md` + the meeting notes for the initiative, **newest first**.
- `documents/index.md` + related documents.
- Recent dailies — action items and Key Events for the initiative.
- `project/management/project-lessons.md` — lessons tagged with spec work (e.g. LL-040, LL-054, LL-065, LL-066).
- `.claude/harness-artifacts-index.md` — any other artifacts whose "Read for context when" matches spec work.

### A3. Intake questions

Present a short summary of what was found (initiative, owners, number of meetings/ASMs/open questions found, candidate source files found on disk), then ask only what's missing — up to 4 questions per round, max 2 rounds, each with a recommendation. Standard intake set:

1. **Name / stream / number** — folder and file name, e.g. `3. Reklamace` → `1. Feature Specs/3. Reklamace/3. Reklamace.docx`. Recommend the next free number.
2. **Source files** — the original client spec (`.docx`, with its Word comments), briefs, roadmap Excel / tracker sheet, data maps, screenshots, codebase path (e.g. `cz-ai-logistics`). Offer the candidates found in A2 / on the Desktop / Downloads / OneDrive and let the PM confirm or add.
3. **Scope of this pass** — which phases, and what is explicitly out of scope for now.
4. **Audience and approvers** — internal draft vs. client-ready; who signs off (from stakeholders), and by when.
5. **Decisions still pending** — anything that must stay open in the spec until a meeting decides it (e.g. an options table waiting for a client decision). These go in as open questions, never as decided facts.

Record the intake answers in the session; they drive everything below.

---

## B. Source Audit (before writing anything)

### B1. Extract everything from the sources

- **Original spec docx**: full text in order, headings, tables, tracked changes (insertions/deletions), and **every Word comment** with author, date, anchor text and reply threading (`word/comments.xml`, `commentsExtended.xml`, `commentRangeStart/End` in `document.xml`).
- **Roadmap / tracker**: every row for the initiative, with its status and phase.
- **Meetings / harness**: the facts collected in A2.
- **Codebase** (if given): endpoints, data model, what is actually built vs. only planned.

### B2. Comment-resolution register

Build a register of **every** comment from the original spec — no sampling:

| # | Date | Author | Anchor | Comment (short) | Resolution | Where in new spec / reason |

Resolution is always one of: **accepted** (reflected in the spec), **deferred to phase N**, **rejected** (with reason), or **open** (goes to Otevřené otázky). A written client comment is never silently dropped — unresolved comments resurface later as "we told you in writing" (LL-066).

### B3. Conflict table — newest source wins

When sources disagree, the **newer source wins** (a September meeting beats a May spec comment; a decided ASM beats an older meeting note). List every conflict for the PM:

| Topic | Older source says | Newer source says | Used in spec |

If two sources are equally recent, or a newer note contradicts a well-documented recent decision, don't pick silently — ask the PM and record it as an open item needing reconciliation.

### B4. Code audit (initiatives with a codebase)

Check every "done / planned / confirmed" claim against the code, not just against the roadmap. Contradictions become open questions and an ASM candidate (LL-054).

Present B2–B4 to the PM as a compact summary (counts + the items needing a PM call) before generating.

---

## C. Adaptive Q&A (gaps only)

Same principles as `/product-feature` A5:
- Plan all questions first; ask only "must ask PM" items (scope, phase placement, client-facing decisions). Auto-decide wording/structure and state the assumption.
- Batch up to 4 per round, 2–3 rounds max, each with a recommendation + confidence (weak / medium / strong).
- Decision matrix when there are several viable approaches.
- Deferral detection: "later", "v2", "nice to have", "další fáze" → propose moving to Plná verze / Nice to Have / Další fáze.
- Map undefined phases explicitly (who owns defining them, by when) — don't leave empty phases unexplained (LL-065).

---

## D. Generate the Spec

### D1. Start from the clean template

- Copy `1. Feature Specs/spec-template.docx` into `1. Feature Specs/{N}. {Name}/{N}. {Name}.docx`. **Never edit the template itself.**
- Strip any leaked `word/comments.xml` / comment references from the copy (a template once carried 39 unrelated Listing comments).
- Remove the "O této šabloně" instruction section.

### D2. Fill the structure (Czech)

Template sections, in order: Management summary (MVP / Plná verze / Nice to Have tables) · Byznys hodnota · KPI (Goal → Question → Metric) · 1. MVP · 2. Plná verze · 3. Nice to Have / Backlog · Další fáze · Mimo rozsah · Závislosti · Technická příloha — API surface · Otevřené otázky (per phase + konsolidované).

Rules for the content:
- **Phase tables mirror the roadmap 1:1**, one row per roadmap item, with a **Zdroj** column. Never an abstracted "capability summary" — that dropped items before (LL-025). Items found elsewhere (code, meetings) with no roadmap row are added as flagged new rows citing their source.
- User stories as "Jako [role] chci [akce], abych [přínos]" per sub-function.
- Unknowns are `-tbd-`, never guessed. Effort always as "MD".
- Pending client decisions stay in Otevřené otázky, with who decides and by when.

### D3. Annotation colors (internal version)

- **Yellow** — business owner / client decision needed.
- **Orange** — Filip / dev team decision needed.
- **Gray** — internal-only note, stripped before the client version.
- `-tbd-` markers highlighted so they're easy to sweep.

### D4. Fidelity check (enumerated, not sampled)

Before presenting: walk the comment register, the roadmap rows and the conflict table item by item and confirm each one landed where the register says (LL-040). Report the counts ("33/33 comments resolved, 18/18 roadmap rows mirrored, 4 conflicts applied").

### D5. Present, then write

Show the PM a section-by-section summary plus the register/conflict tables. Write the docx only after confirmation.

---

## E. Review / Redline Mode

1. Diff the current spec against the original (or the previous version) and produce an annotated redline.
2. PM reviews in Word, leaving comments.
3. Extract all PM comments, apply each one, and report them one by one (applied / needs decision). Save as a new version (`new_{N}. {Name} v2.docx`), keeping the previous file.

---

## F. Client Version

Create a **separate copy** (`{N}. {Name} - klientská verze.docx`) — the internal original is never modified:
- Strip internal Word comments and gray internal notes.
- Turn remaining review threads into highlighted in-text notes (needs attention / our proposal).
- Sweep for every `-tbd-`, internal names and internal-only references.
- After stripping, diff against the internal version to confirm nothing real was deleted (a regex strip once removed a whole API section).

---

## G. After Writing

- Log to today's `project-daily`: `[MANUAL] {N}. {Name}.docx — {created/rebuilt/updated/client version} via /product-client-spec ({date})`, plus a 2–5 sentence Key Events summary.
- Update any matching action items in the daily (progress notes / mark done).
- **Routing check**: decisions, assumptions and contradictions surfaced during the session → propose `project-assumptions` / `project-knowledge` entries for PM confirmation.

---

## Rules

- **Intake before work**: never start writing before name, sources and mode are confirmed.
- **Newest source wins**; conflicts are listed, ambiguous ones asked.
- **Every source comment gets a resolution** — no sampling, no silent drops.
- **Originals are read-only**: never modify the original client spec, the template, or the internal version when making a client copy. Always write to a new file.
- **Close the file before writing**: check with `lsof` that Word/Excel doesn't have the target open; AutoSave silently reverts writes otherwise (LL-023/024). If it's open, ask the PM to close it.
- **Verify after writing**: re-open the saved file and check the content and fills actually rendered (LL on transparent fills).
- **Czech in the document**, BigHub house style; `-tbd-` for unknowns; "MD" for effort.
- **PM confirms before every write.**
