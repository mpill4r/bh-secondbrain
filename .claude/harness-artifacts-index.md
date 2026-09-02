---
last_updated: 2026-04-07
owner: Jan Koscelansky
---

# Harness Artifacts Index

Central registry of all harness artifacts. Skills that route information or read context reference this index instead of maintaining hardcoded artifact lists.

**Convention**: Any new artifact must be registered here. Any artifact change (path, purpose, routing condition) must be updated here. This is the single source of truth for what artifacts exist and when to use them.

---

## Project Management

### `project-overview`
- **Path**: `project/management/project-overview.md`
- **Purpose**: Living engagement summary — what's being built, for whom, by whom, commercial structure, strategic rationale
- **Owner skill**: `project-overview`
- **Route to when**: Project status changes, phase transitions, key milestone updates, team structure changes
- **Read for context when**: Status meetings, steering committees, milestone reviews, any meeting needing project-level context
- **Staleness**: >5 `-tbd-` fields or >30 days since `last_updated`

### `client-overview`
- **Path**: `project/management/client-overview.md`
- **Purpose**: Client intelligence document — company profile, market context, business model, ways of working, relationship health, commercial context
- **Owner skill**: `client-overview`
- **Route to when**: Client strategy updates, market context, ways-of-working signals, relationship updates, commercial context, sentiment shifts
- **Read for context when**: Any client or external meeting, proposal preparation, communications drafting
- **Staleness**: >5 `-tbd-` fields or >30 days since `last_updated`

### `project-stakeholders`
- **Path**: `project/management/project-stakeholders.md`
- **Purpose**: Living map of all stakeholders — roles, influence, sentiment, communication preferences, expectations, org hierarchy
- **Owner skill**: `project-stakeholders`
- **Route to when**: New stakeholders discovered, role changes, sentiment updates, engagement signals, communication preference changes
- **Read for context when**: Any meeting — attendee profiles and sentiment; stakeholder-sensitive communications
- **Staleness**: >5 `-tbd-` fields or >30 days since `last_updated`

### `project-assumptions`
- **Path**: `project/management/project-assumptions.md`
- **Purpose**: Tracks all ideas, directions, assumptions, and decisions — from early suggestions to firm commitments. Each entry: ASM-NNN ID, status (Open/Decided/Retired), description, rationale, and AI-driven impact analysis across trade-off dimensions.
- **Owner skill**: `project-assumptions`
- **Route to when**: Ideas, suggestions, directions, assumptions, or decisions surfaced in meetings, documents, or conversations. Anything the team believes, proposes, or commits to.
- **Read for context when**: Any meeting — current assumptions and decisions inform discussion; scope work; feature specification; priority derivation in `project-daily`
- **Staleness**: Open items >14 days without status change

### ~~`project-log`~~ — Deferred
- Dropped from Phase 1. Milestone events and audit trail go to `project-daily` Key Events. Can be generated retroactively from dailies if needed.

### `project-lessons`
- **Path**: `project/management/project-lessons.md`
- **Purpose**: Organizational knowledge capture — generalizable lessons learned that help other PMs, teams, or future projects. Captured autonomously (no PM confirmation) after meeting processing and during daily close. Each entry: LL-NNN ID, category (open-ended), generalized lesson, project-specific context, cross-references.
- **Owner skill**: `project-lessons`
- **Route to when**: Autonomously triggered — after `project-meeting` routing review completes, after `project-document` routing review completes, and during `project-daily` close step. Also: explicit lessons or retrospective insights mentioned by PM. Documents are particularly valuable sources when they contain retrospective summaries, post-mortems, or workshop outputs.
- **Read for context when**: Retrospectives, project close, similar situations arising, starting a new phase or project

---

### `project-knowledge`
- **Path**: `project/management/project-knowledge.md`
- **Purpose**: Project encyclopedia — domain terminology, client jargon, data model concepts, regulatory constraints, naming conventions, vendor context, seasonal patterns, project conventions, historical context
- **Owner skill**: `project-knowledge`
- **Route to when**: New domain terminology, client-specific terms, data model concepts, regulatory context, vendor references, naming inconsistencies, seasonal patterns, team conventions, or historical project intelligence discovered
- **Read for context when**: Any interaction involving domain terminology, client context, technical systems, data models, project conventions, or unfamiliar terms. Skills check this condition via index-driven loading and decide dynamically whether to read the file.

---

## Product Management

### `product-requirements`
- **Path**: `product/problem-space/product-requirements.md`
- **Purpose**: Single structured source of truth for all requirements — Business, Data, Design, Tech, Other. Each entry: REQ-NNN ID, type, MoSCoW priority, status (Open/Processed/Deferred), source person and artifact, description.
- **Owner skill**: `product-requirements`
- **Route to when**: Raw requirements, constraints, success criteria, acceptance criteria at the capture level — anything that reads as "the system must/should/shall" or defines a measurable outcome. This is the entry point for all requirements; they may later feed into product-scope (as features) or product-feature (as ACs). Requirements appear as grouped block in routing review.
- **Read for context when**: Discovery meetings, scoping sessions, review meetings, feature specification, product scope definition

### ~~`domain-knowledge`~~ → Renamed to `project-knowledge`, moved to Project Management section above

### `product-brief`
- **Path**: `product/problem-space/product-brief.md`
- **Purpose**: Highest-level strategic product document — north star, problem definition (incl. why current approaches fail), target personas, business goals, solution definition (flexible format, optional Before→After), market positioning, scope boundaries, high-level phasing (synced with product-scope). Created at project initiation with aggressive auto-fill from PM-provided context (no documents available at initiation — ingested after); enriched via coaching-style `/product-brief` sessions and document routing.
- **Owner skill**: `product-brief`
- **Route to when**: Strategic-level product signals — problem framing shifts ("this is really about X, not Y"), new or refined user personas, business goal changes, solution direction signals, competitive or market intelligence, scope boundary decisions, phasing direction. This is the strategic level — if content is about *what to build and why*, it likely belongs here. If it's about *how to deliver it*, it belongs in product-scope.
- **Read for context when**: Alignment meetings, kick-offs, scope decisions, feature specification, any meeting needing product-level strategic context
- **Staleness**: >5 `-tbd-` fields or >14 days since `last_updated`

### `product-scope`
- **Path**: `product/solution-space/product-scope-{phase-slug}.md`
- **Purpose**: Phase-level roadmap and delivery tracker — epics, features (FEAT-NNN), delivery status, design status, completion %. 5-step lifecycle (defined → drafted → speced → in development → released). Two-tier prioritization (Priority/Standard). One file per phase.
- **Owner skill**: `product-scope`
- **Route to when**: Delivery-planning-level product signals — new epics or features identified, scope changes (features added/removed/moved between epics), feature status updates, priority shifts, deferrals ("push X to Phase 2"), estimation data, milestone updates, timeline changes, release date signals. This is the delivery level — if content is about *what to deliver, when, and in what order*, it belongs here. Also receives feature-level detail as fallback when a FEAT-NNN spec file doesn't exist yet.
- **Read for context when**: Scoping sessions, estimation meetings, phase review meetings, sprint planning, daily status derivation (RAG + priority), weekly status generation (milestones + timeline)
- **Staleness**: >5 `-tbd-` fields or >14 days since `last_updated` (active phases only)

### ~~`product-journey`~~ — Deferred
- Dropped from Phase 1. User journey mapping handled ad-hoc via `project-meeting` and `project-document`.

### `product-slidedeck`
- **Path**: `product/solution-space/slidedeck-{slug}.md`
- **Purpose**: Slide deck content brief — structured markdown specifying every slide's content, layout mode, and component composition. Input for Claude Design rendering against the house slide master. One file per deck.
- **Owner skill**: `product-slidedeck`
- **Route to when**: Not a primary routing target. May receive updates when product-brief, product-scope, or client-overview changes affect an existing deck's content.
- **Read for context when**: Deck revision requests, presentation preparation, proposal drafting
- **Staleness**: Deck-specific — stale if the underlying product/project context has changed significantly since `last_updated`

### `product-feature`
- **Path**: `product/solution-space/features/FEAT-NNN-{slug}.md`
- **Purpose**: Individual feature specification — enough detail for a designer and engineer to build it. 8 sections: Feature Summary, User Stories, Acceptance Criteria (Given/When/Then), Edge Cases, Out of Scope, Technical Constraints, Dependencies, Design (Figma). Status synced bidirectionally with product-scope FEAT-NNN entries.
- **Owner skill**: `product-feature`
- **Route to when**: Implementation-detail-level content for a specific identified feature (FEAT-NNN) — acceptance criteria, edge cases, UX flow details, design decisions, technical constraints, dependency information, scope clarifications. The originating skill must identify which FEAT-NNN the content relates to (from product-scope context). If the FEAT-NNN spec file doesn't exist yet, route to product-scope instead (as a note on the feature entry).
- **Read for context when**: Implementation discussions, design reviews, QA planning for a specific feature

---

## Operational

### `project-daily`
- **Path**: `project/daily/project-daily-YYYY-MM-DD.md`
- **Purpose**: Autonomous daily context log — project status (RAG), current priority, action items, session summaries, audit trail. Primary continuity mechanism between sessions.
- **Owner skill**: `project-daily`
- **Route to when**: Audit entries from any skill that modifies a harness artifact (`[AUTO]`/`[MANUAL]` format); action items with owner/deadline from `project-meeting`, `project-document`, and other routing skills
- **Read for context when**: Session start (CLAUDE.md startup — briefing); any meeting (recent blockers, open action items); status checks; weekly summary generation

### `project-weekly`
- **Path**: `project/weekly/project-weekly-YYYY-WNN.md` (+ `-client.md` variant)
- **Purpose**: Management-grade weekly status summary — transparent internal version for internal management, sensitivity-filtered client version for external stakeholders. Generated from daily logs.
- **Owner skill**: `project-weekly`
- **Route to when**: Not a routing target — generated from daily logs. Auto-generated Fridays at 4pm via RemoteTrigger, or manually via `/project-weekly`.
- **Read for context when**: Weekly status meetings, management briefings, client status updates

### `meeting-index`
- **Path**: `meetings/index.md`
- **Purpose**: Central directory of all processed meetings — date, type, attendees, TL;DR, file link, counts
- **Owner skill**: `project-meeting`
- **Route to when**: Every processed meeting (upload and prep) gets an entry
- **Read for context when**: Any meeting — check for previous instances, recurring meeting detection

### `document-index`
- **Path**: `documents/index.md`
- **Purpose**: Central directory of all ingested documents — date, title, source, classification, summary link, executive summary excerpt
- **Owner skill**: `project-document`
- **Route to when**: Every ingested document gets an entry; updated versions link to previous
- **Read for context when**: Document ingestion — duplicate/version detection, previous document context
