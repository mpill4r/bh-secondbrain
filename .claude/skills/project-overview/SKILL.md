# project-overview — Skill Logic

> The living engagement summary. Captures everything important about a client engagement: what's being built, for whom, the team, the commercial structure, and the strategic rationale. Anyone on the team picking it up cold should understand the engagement without additional context. Created during `project-initiation`, continuously updated via silent routing. `/project-overview` is the manual review and update command.

---

## When This Skill Runs

This skill runs in three contexts:
- **PM invokes `/project-overview`** → Review & Update Session (Section A)
- **Called from `project-initiation`** → Auto-Creation (Section B)
- **Receives routed content from other skills** → Inbound Routing (Section C)

---

## A. Review & Update Session

### A1. Load Context

Read `project/management/project-overview.md` (full file) and `project/management/client-overview.md` (core dependency). Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match the current task. If any file does not exist, skip silently.

### A2. Review Summary

Identify all `-tbd-` fields, `> Needs confirmation` notes, and sections that may be stale relative to git history since `last_updated`. Present the review summary to the PM and ask whether they want to update anything. PM can provide specific changes or request a general scan.

### A3. General Scan

If PM requests a general scan, check git history for the last 7 days and propose relevant changes to sections with clear rationale for each. Show a diff for each proposed change.

### A4. Writing Changes

Before writing any changes, show a diff of all proposed updates. Wait for PM confirmation. Never auto-write in this mode.

End every session with: "Anything else to add?" as a final open input step.

### A5. After Writing

- Update frontmatter `last_updated` and `last_updated_by: manual — /project-overview`.
- Log audit entry to `project-daily`: `[MANUAL] project-overview updated via /project-overview — {sections updated} ({date})`.
- If `project-daily` does not exist, create it first.

---

## B. Auto-Creation (called from project-initiation)

### B1. Prerequisites

`client-overview.md` must exist before this skill runs — it is the primary data source. This is a hard prerequisite.

### B2. Read Context

Read `project/management/client-overview.md` (Sections 1, 3, 4, 6, 7 for company profile, business model, market context, strategic priorities, tech landscape) and the PM's free-text input from the initiation conversation (passed by `project-initiation`). No documents are available at initiation time — document ingestion happens after initiation via `/project-document`. Do NOT perform web research — all client intelligence comes from `client-overview`.

### B3. Pre-Fill All Sections

Create `project/management/project-overview.md` using the template. Pre-fill every section possible:

- **Section 1 (Project Description)**: From PM's initiation input (project name, client name, what's being built) and `client-overview` Sections 1 & 3.
- **Section 2 (Project Goals)**: From PM's goals context. Likely sparse at creation — enriched later via `product-brief` routing.
- **Section 3 (Client Profile)**: From `client-overview` Sections 1 & 3 (direct read — no re-research). Copy company name, industry, headquarters, company size, business model summary.
- **Section 4 (Client Categorization)**: Copied directly from `client-overview` **Client Categorisation** section — no re-inference. If that section in `client-overview` is `-tbd-`, this section is also `-tbd-`.
- **Section 5 (Project Categorization)**: From PM's initiation input. Use only the predefined taxonomy values. Mark unknown dimensions `-tbd-`.
- **Section 6 (Key Use-Cases & Problems)**: From PM's context about what problems are being solved. Enriched later via `product-brief` routing.
- **Section 7 (Solution Overview)**: From PM's context about what's being built and `client-overview` **Product & Tech Landscape** section.
- **Section 8 (Project Timeline)**: From PM's timeline context. Mostly `-tbd-` at creation — enriched later via `product-scope` routing.
- **Section 9 (Delivery Team)**: From PM's initiation input about team members. Populated as a thin index with ID, name, role, slug reference linking to `project-stakeholders.md`. Full profiles never live in this document.
- **Section 10 (Client Stakeholders)**: Populated as a thin index from stakeholder names provided during initiation. Slugs link to `project-stakeholders.md`. Full profiles never live in this document.
- **Section 11 (Commercials)**: `-tbd-` at creation (no documents available during initiation). Mark the section `> Internal — do not share with client.` Populated later via `/project-document` routing when SoW, contract, or proposal documents are ingested, or manually via `/project-overview`.

### B4. Field Handling

- Fields without reliable data: `-tbd-`.
- Low confidence: `> Needs confirmation — [what was found and why it's uncertain]`.
- Never fabricate data.
- Categorization fields (Sections 4 and 5) use only the predefined taxonomy values — non-standard values are never used.

### B5. Complete

- Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — project-initiation`.
- Complete silently — no summary, no prompts, no interruptions to the initiation flow.
- If `project-daily` exists, log audit entry: `[AUTO] project-overview — created from project-initiation ({date})`.

---

## C. Inbound Routing (silent)

All auto-routing to `project-overview.md` happens silently without PM confirmation. If the file does not exist, skip the routing silently. Every write is logged as an audit entry in the current `project-daily` log.

### Routing sources and targets

- **`project-meeting`**: Status or phase changes → **Section 1 (Project Description)**. Team composition changes → **Section 9 (Delivery Team)**.
- **`project-stakeholders`**: Auto-syncs **Section 9 (Delivery Team)** with all active internal team members — ID, name, role, slug reference. Auto-syncs **Section 10 (Client Stakeholders)** with key client stakeholders only — high influence, most active counterparts, people responsible for the project. ID, name, role, slug reference. This sync is mechanical — no PM confirmation needed.
- **`product-brief`**: Goals and problem framing → **Section 2 (Project Goals)** and **Section 6 (Key Use-Cases & Problems)**.
- **`product-scope`**: Phase table → **Section 8 (Project Timeline)**. Current phase and services → **Section 5 (Project Categorization)**.
- **`project-document`**: Receives writes from `project-document` via PM-confirmed routing review (the routing review is owned by `project-document`, not this skill): commercial terms → **Section 11 (Commercials)**; timeline data → **Section 8 (Project Timeline)**; team/resource info → **Section 9 (Delivery Team)**; strategic rationale → **Section 1 (Project Description)**. If data is ambiguous, fields are marked `> Needs confirmation — [what was found and why it's uncertain]`.

### After each routed write

- Update frontmatter `last_updated` and `last_updated_by: auto — {source skill} routing`.
- Log audit entry to `project-daily`: `[AUTO] project-overview — {section name} updated from {source} ({date})`.
- If `project-daily` does not exist, create it first.
- Preserve all existing content exactly. Only targeted sections and fields are modified.

---

## Rules

- **11 sections always present**: All sections exist in the document, even if mostly `-tbd-`.
- **`-tbd-` over fabrication**: Unknown fields are always `-tbd-`, never guessed.
- **No independent web research**: All client intelligence comes from `client-overview`. This skill never performs web research.
- **Predefined taxonomy only**: Categorization fields (Sections 4 and 5) use only the predefined values listed in the Document Structure section of the spec. Non-standard values break portfolio analytics.
- **Thin indexes for people**: Delivery Team and Client Stakeholders sections contain IDs and slug references only — full profiles live in `project-stakeholders.md`. Never copy profile data into this document.
- **Commercials are internal**: Section 11 is always marked `> Internal — do not share with client.`
- **Professional and specific writing**: No generic filler. "The team is building a real-time fraud detection pipeline for the client's transaction monitoring system" not "an innovative AI solution."
- **Human-readable standalone**: Anyone on the team picking up this document cold should understand the engagement without additional context.
- **PM confirms all manual writes**: Never auto-write during `/project-overview` sessions. Always show diff and wait.
- **Silent routing never blocks**: All auto-routing is silent. If the target file does not exist, skip silently. Never prompt PM during routing writes.
- **Preserve existing content**: When writing, preserve all existing content exactly. Only targeted sections and fields are modified.
- **Machine-readable format**: Clear section headers, consistent field labels, structured data blocks. Other skills reference this document programmatically.
- **Audit everything**: Every write (manual and routed) logs to `project-daily`. If `project-daily` does not exist, create it first.
- **Staleness check is external**: Owned by `project-daily` close step (>5 `-tbd-` or >30 days since `last_updated`). This skill does not check its own staleness.
- **`client-overview` is upstream**: If `client-overview` has `-tbd-` fields, this document mirrors those gaps. PM should run `/client-overview` first to enrich client data before enriching this document.
