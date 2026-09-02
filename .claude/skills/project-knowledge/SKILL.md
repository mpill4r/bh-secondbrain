# project-knowledge — Skill Logic

> The project encyclopedia. Captures domain terminology, client jargon, data model concepts, regulatory context, naming conventions, vendor context, seasonal patterns, project conventions, and historical context. Created during `project-initiation` as the last foundational artifact. Grows organically via routing and PM enrichment. No staleness check — this is an encyclopedia, consulted when needed.

---

## When This Skill Runs

This skill runs in three contexts:
- **PM invokes `/project-knowledge`** → Review/Enrichment Session (Section A)
- **Called from `project-initiation`** → Auto-Creation (Section B)
- **Receives routed content from other skills** → Inbound Routing (Section C)

---

## A. Review/Enrichment Session

### A1. Load Context

Read `project/management/project-knowledge.md` (full file). Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match the current task. If any file does not exist, skip silently.

### A2. Health Summary

Present on entry: total entry count, entries with `Status: Needs confirmation`, number of sections (fixed + dynamic), last update date. If no dynamic sections exist yet (first session after initiation), analyze available context and propose 0-3 dynamic sections based on the project domain. If no additional sections are warranted (generic domain), tell the PM: "No additional sections needed beyond the 9 fixed sections." Then ask what the PM wants to work on.

### A3. PM Interactions

The PM can:
- **Add new entries** to any section. Skill proposes the most appropriate section — PM can override. If a term genuinely spans sections, place in the primary section with a note referencing the other context.
- **Correct existing definitions** — update the Definition field, set `Last updated`.
- **Resolve `Needs confirmation` entries** — PM verifies, status changes to `Active`.
- **Propose new dynamic sections** — skill creates the section header. Dynamic sections use the same entry format as fixed sections.
- **Mark entries as `Superseded`** — old entry gets `Status: Superseded` with pointer to replacement. Not deleted.
- **Do a full review of a specific section** — skill walks through entries.

### A4. Duplicate Detection

Before adding any entry (in any write path — interactive or routed), check for duplicates:
- Same term or very similar concept already in the knowledge base.
- If match found: "This appears similar to '{existing term}' in {section}. Update the existing entry or create a new one?" PM decides.

### A5. Writing Changes

- Before writing, show a diff. Wait for PM confirmation. Never auto-write.
- End every session with: "Anything else to add?" as a final open input step.

### A6. After Writing

- Update frontmatter `last_updated` and `last_updated_by: manual — /project-knowledge`.
- Log audit entry to `project-daily`: `[MANUAL] project-knowledge updated via /project-knowledge — {sections updated, entries added/modified} ({date})`.
- If `project-daily` does not exist, create it first.

---

## B. Auto-Creation (called from project-initiation)

### B1. Prerequisites

`client-overview.md`, `project-overview.md`, `project-stakeholders.md`, and `product-brief.md` must exist before this skill runs — all are created earlier in the initiation flow. This skill is created LAST in the foundational sequence.

### B2. Read Context

Read all foundational artifacts:
- `client-overview.md` — Sections 1, 3, 4, 7, 12 for company profile, business model, market context, tech landscape, and inline domain terms.
- `project-overview.md` — Sections 1, 2, 6 for project description, goals, use cases.
- `project-stakeholders.md` — role context and communication patterns.
- `product-brief.md` — Sections 2, 3 for problem domain and user context.

No documents are available at initiation time. If any source does not exist, skip silently.

### B3. Pre-Populate Fixed Sections

Create `project/management/project-knowledge.md` using the template. Pre-populate entries from available context:

- **Section 1 (Domain Terminology)**: Extract domain-specific terms from all sources. Terms in `client-overview` Domain Language section pulled in directly. Any term whose meaning is not obvious from general knowledge gets an entry.
- **Section 2 (Client Jargon)**: Extract terms the client uses with non-standard meaning.
- **Section 3 (Data Model Concepts)**: Extract business entities and relationships from available context.
- **Section 4 (Regulatory & Compliance)**: Extract regulatory references. If nothing found, section present but empty.
- **Section 5 (Naming Conventions)**: Extract cases where different terms are used for the same concept. Cross-reference Sections 1-2.
- **Section 6 (Vendor & Partner Context)**: Extract third-party vendors, platforms, or partners mentioned. Each gets an entry with role and relationship.
- **Section 7 (Seasonal & Cyclical Patterns)**: Extract from planning or timeline references. Often empty at creation.
- **Section 8 (Project Conventions)**: Extract from working agreements or tool requirements. Project-internal conventions only — client-facing ways of working stay in `client-overview` Ways of Working.
- **Section 9 (Historical Context)**: Extract references to previous attempts, legacy systems, or past project history. Often sparse at creation.

### B4. Entry Status Assignment

- Entries from highly reliable sources (e.g., glossary section in a SoW that explicitly defines terms): `Status: Active`.
- Entries inferred from usage context: `Status: Needs confirmation`.
- Use judgment: a term clearly defined in a document is Active; a term inferred from context is Needs confirmation.

### B5. Dynamic Sections

Do NOT propose dynamic sections during initiation — insufficient context at this stage. Dynamic sections are proposed during the first `/project-knowledge` session (Section A2).

### B6. Complete

- Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — project-initiation`.
- All 9 fixed sections present as headers. Sections without entries are present as headers with no content — no placeholder text.
- Complete silently — no summary, no prompts, no interruptions.

---

## C. Inbound Routing (from meetings and documents)

### Routing sources

- **`project-document`**: Domain terminology from glossaries and SoW, data model entities from technical docs, regulatory constraints from legal documents, vendor references, naming inconsistencies between documents.
- **`project-meeting`**: New terms used by client stakeholders, data model concepts discussed, regulatory constraints mentioned, historical context shared ("we tried this before..."), seasonal patterns referenced, client jargon identified.

### Writing routed entries

- Routed entries are written with `Status: Active` — PM already confirmed them during the source skill's routing review.
- Each entry includes the source reference (meeting slug or document slug).
- Place entries in the appropriate section.

### Conflict handling

When a routed entry contradicts an existing definition, the conflict is flagged during the source skill's routing review (not here): "New definition of '{term}' from {source} differs from existing: existing says '{X}', new source says '{Y}'. Which is correct?" PM resolves:
- Update to new definition
- Keep existing
- Mark as `Needs confirmation` with both versions noted

When a definition evolves (not contradicts — more detail, broader scope), update the existing entry in place. Set `Last updated` and update `Source` to include the new source alongside the original.

### Duplicate detection in routing

Before writing any routed entry, check for existing entries with the same term or similar concept. If match found, handle as an update to the existing entry (with PM confirmation via the source skill's routing review).

### After each routed write

- Update frontmatter `last_updated` and `last_updated_by: auto — {source skill} routing`.
- Log audit entry to `project-daily`: `[AUTO] project-knowledge — {section} updated from {source-slug} ({date})`.
- If `project-knowledge.md` does not exist, create it from template first (all 9 fixed sections, empty), then write. Log: `[AUTO] project-knowledge — file created and {section} updated from {source-slug} ({date})`.
- If `project-daily` does not exist, create it first.

---

## Rules

- **9 fixed sections always present**: All section headers exist, even if empty. No placeholder text in empty sections.
- **Consistent entry format**: Every entry in every section (fixed and dynamic) uses the same format: H3 term name, field table (Definition, Source, Added, Last updated, Status), optional context.
- **No sequential IDs**: Terms are referenced by name, not by ID.
- **Duplicate detection in all write paths**: Check before adding in interactive mode, routing, and creation. Same term or similar concept → merge or ask PM.
- **`-tbd-` over fabrication**: Never fabricate definitions.
- **Plain language**: Definitions are written so a new team member understands without prior domain expertise. No circular definitions.
- **Superseded entries preserved**: Old entries get `Status: Superseded` with pointer to replacement. Never deleted.
- **No staleness check**: This artifact is not monitored by `project-daily` close step. It is an encyclopedia — consulted when needed.
- **Audit everything**: Every write (manual and routed) logs to `project-daily`. If `project-daily` does not exist, create it first.
- **Machine-readable format**: Consistent structure so other skills can parse entries reliably.
- **Same term used differently by different stakeholders**: Note the variation in the optional context line. Status: `Needs confirmation` until aligned definition established.
- **Naming convention conflicts (Section 5)**: Client and team use same word for different things — capture both meanings with clear attribution.
- **Knowledge-heavy project (100+ entries)**: No entry limit. During review sessions, group entries by status (Needs confirmation first, then recently added, then Active) to focus PM attention.
