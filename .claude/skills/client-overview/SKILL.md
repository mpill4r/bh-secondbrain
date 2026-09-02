# client-overview — Skill Logic

> A 12-section intelligence document about the client. Gives internal management and sales a portfolio-level view. Serves as a machine-readable context preamble for other skills. Created during `project-initiation`, continuously enriched via routing and PM Q&A sessions.

---

## When This Skill Runs

This skill runs in three contexts:
- **PM invokes `/client-overview`** → Q&A Review Session (Section A)
- **Called from `project-initiation`** → Auto-Creation (Section B)
- **Receives routed content from other skills** → Inbound Routing (Section C)

---

## A. Q&A Review Session

1. **Load context**: Read `project/management/client-overview.md` (full file) and `project/management/project-stakeholders.md` (core dependency). Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match the current task. If any file does not exist, skip silently.
2. **Identify gaps**: Find all `-tbd-` fields and `> Needs confirmation` notes across all 12 sections.
3. **Offer web research if not yet done**: If Sections 1-5 have no `[Source: ...]` citations (web research hasn't been performed), proactively offer: "I notice no web research has been done for this client yet. Want me to research {client name} now to fill in gaps before we start the review?" If PM accepts, perform web research, show diff, confirm, then proceed to Q&A on remaining gaps. If PM declines, continue with Q&A.
4. **Dynamic Q&A**: Group questions by topic based on actual gaps — no fixed groupings. Sessions with few gaps should be short; sessions after initiation may be longer. For each group, show the current state and ask PM to confirm, correct, or provide missing information. PM can also volunteer information for any section not currently flagged.
5. **Before writing**: Show a diff of all proposed changes. Wait for PM confirmation. Never auto-write.
6. **Final prompt**: Ask "Anything else to add?" as a final open input step.
7. **After writing**: Update frontmatter `last_updated` and `last_updated_by: manual — /client-overview`. Log audit entry to `project-daily`: `[MANUAL] client-overview updated via /client-overview — {sections updated} ({date})`.

---

## B. Auto-Creation (called from project-initiation)

1. Read the client name and any stakeholder info passed from `project-initiation`.
2. Create `project/management/client-overview.md` using the template from `.claude/skills/client-overview/TEMPLATE.md`.
3. **Populate from PM-provided context only**: No documents are available at initiation time (document ingestion happens after). No web research. Fill in whatever the PM provided during the initiation conversation. Mark everything else `-tbd-`.
4. **Section 2 (Client Categorisation)**: Cannot be inferred without documents or web research at this point. Mark `-tbd-`.
5. **Section 5 (Financial Context)**: Mark commercial data as `> Internal — do not share with client.`
6. **Section 8 (Stakeholder Map)**: Populate as a thin index from stakeholder names provided during initiation — client/external stakeholders only, no internal team. ID, name, role, slug reference linking to `project-stakeholders.md`.
7. **Section 11 (Engagement Context)**: Mark commercial history table as `> Internal — do not share with client.`
8. **Section 12 (Domain Language)**: Create pointer to `project-knowledge.md` (created later in the same initiation flow — the pointer is valid because the file will exist by the time initiation completes).
9. **Fields without reliable data**: Mark `-tbd-`. Fields where confidence is low: mark `> Needs confirmation — [what was found and why it's uncertain]`. Never fabricate.
10. Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — project-initiation`.
11. Complete silently — no summary, no prompts, no interruptions to the initiation flow.

---

## C. Inbound Routing (from other skills)

Routing to `client-overview.md` arrives via the source skill's PM-confirmed routing review. The PM sees client-overview items grouped in the routing review and confirms them alongside all other routes. No separate client-overview-specific confirmation is needed.

### Routing sources and targets

- **`project-meeting`**: Strategic priorities or key client decisions → Section 6 (Strategic Priorities). Ways of working patterns → Section 9 (Ways of Working). Relationship signals → Section 11 (Engagement Context). Stakeholder sentiment is routed to `project-stakeholders.md`, NOT Section 8.
- **`project-document`**: SoW/PRD → Sections 3, 6, 7 (Business Model, Strategic Priorities, Product & Tech Landscape). Company/strategy docs → Sections 1, 4, 5, 6 (Company Profile, Market & Competitive Position, Financial Context, Strategic Priorities). Commercial docs → Section 11 (Engagement Context).
- **`project-stakeholders`**: Auto-syncs Section 8 (Stakeholder Map) thin index on every stakeholder change. Client/external stakeholders only — no internal team. Writes ID, name, role, slug only. This sync is mechanical — no PM confirmation needed.
- **`project-overview`**: Updates Section 10 (Active Initiatives & Project History) on project status or phase changes.
- **`product-brief`**: Routes engagement goals and problem framing to Section 11 (Engagement Context).
- **`product-scope`**: Updates Section 10 (Active Initiatives & Project History) on phase creation/completion.

### After each routed write

- Update frontmatter `last_updated` and `last_updated_by: auto — {source skill} routing`.
- Log audit entry to `project-daily`: `[AUTO] client-overview — {section name} updated from {source} ({date})`.
- If `client-overview.md` does not exist when a routing write is attempted, skip silently.
- If `project-daily` does not exist, create it first.

---

## D. Client Categorisation

Section 2 uses exactly one of four predefined values — no variations or free text:

- **Start-up** — early-stage, pre-PMF, founder-led, seed/pre-seed or bootstrapped, building 0→1
- **Scale-up** — post-PMF, VC-backed growth stage Series A–C, scaling features on existing product
- **SME** — established traditional business on non-VC path, digitising operations or building tools
- **Large Enterprise** — large corporate with formal governance, procurement, legacy estate, complex stakeholder map

Inferred from ingested documents if possible (funding stage, headcount, growth signals, ownership structure). If insufficient signal, marked `-tbd-` until web research or PM sets it manually.

---

## E. Web Research

Web research is **never performed during initiation** — it is deferred to the first `/client-overview` session.

When web research is performed (during Q&A session):
- All research-populated fields include an inline source reference: `[Source: {URL or description}]` so PM can verify accuracy.
- Conflicting research results are marked: `> Needs confirmation — [source A says X, source B says Y]`. Resolved in the Q&A session.

---

## Rules

- **12 sections always present**: All sections exist in the document, even if mostly `-tbd-`.
- **`-tbd-` over fabrication**: Unknown fields are always `-tbd-`, never guessed. Low-confidence fields use `> Needs confirmation`.
- **Stakeholder Map is a thin index**: Section 8 contains IDs and slug references only — full profiles live in `project-stakeholders.md`. Client/external stakeholders only, no internal team.
- **Sentiment routes to stakeholders, not here**: Stakeholder sentiment from meetings is routed to `project-stakeholders.md`, not the Stakeholder Map section.
- **Commercial data is internal**: Section 5 and the Section 11 commercial table are marked `> Internal — do not share with client.`
- **Client Categorisation uses predefined values only**: Exactly one of Start-up / Scale-up / SME / Large Enterprise.
- **Machine-readable format**: Clear section headers, consistent field labels, structured data blocks. Other skills reference this document programmatically.
- **Audit everything**: Every modification logs an audit entry to `project-daily`. If `project-daily` does not exist, create it first.
- **File already exists at initiation**: Handled by `project-initiation` which asks PM: overwrite, skip, or review and merge.
- **Staleness check is external**: Owned by `project-daily` close step (>5 `-tbd-` or >30 days since `last_updated`). This skill does not check its own staleness.
