# product-brief — Skill Logic

> The highest-level strategic product document. Captures what problem is being solved, for whom, what we're building, how the market looks, and how the product phases out. Created during `project-initiation` with aggressive pre-fill. Enriched via coaching-style `/product-brief` sessions and silent routing from meetings and documents.

---

## When This Skill Runs

This skill runs in three contexts:
- **PM invokes `/product-brief`** → Conversational Enrichment (Section A)
- **Called from `project-initiation`** → Auto-Creation (Section B)
- **Receives routed content from other skills** → Inbound Routing (Section C)

---

## A. Conversational Enrichment

### A1. Load Context

Read `product/problem-space/product-brief.md` (full file) and `project/management/client-overview.md` (core dependency). Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match the current task — this includes `project-stakeholders.md` (person resolution), `project-knowledge.md` (terminology), and `product-requirements.md` (scope boundary context). If any file does not exist, skip silently.

### A2. Health Summary

Present on entry: total section count, sections with `-tbd-` fields, sections with `> Needs confirmation` notes, last update date. Then ask what the PM wants to work on.

### A3. Coaching Model

The interaction is conversational — no explicit modes. The skill helps the PM discover answers, not just record them. Three patterns to draw from as appropriate:

- **Probing questions**: When PM doesn't have an answer, ask questions that help them find it. "Who in the client's organization loses the most time in the current process? What happens if they do nothing for another year?"
- **Activity suggestions**: When a question genuinely can't be answered without more information, suggest the activity that would produce the answer. PM can either start it immediately within the session or capture it as an action item in `project-daily` for later. "This needs user research with actual end-users — want me to help draft an interview plan now, or should I add it as an action item?"
- **Draft proposals**: Synthesize what's known from the pre-read context and propose content for PM to react to. It's easier to edit a draft than write from scratch.

### A4. Section-Specific Guidance

**Section 1 (Product North Star)**: Proactively propose a 1-2 sentence statement when Sections 2-5 have enough content. Write the proposal with `> PM review needed` note and keep the field `-tbd-` until PM explicitly confirms. The north star should be directional, memorable, and repeatable.

**Section 4 (Business Goals & Success Metrics)**: Prompt for concrete measurable outcomes. If PM provides vague goals, help make them specific: "What would success look like in numbers? Revenue target, user count, time saved?"

**Section 5 (Solution Definition)**: Structure discussion across four perspectives (product, business, market, technology). May suggest a Before→After comparison if it helps. Format is flexible — free text, bullets, or table, whatever PM prefers. If PM starts describing detailed features, redirect: "That's feature-level detail — it belongs in product-scope. Let's capture the high-level solution concept here."

**Section 6 (Market Positioning)**: Read `client-overview` Market & Competitive Position for competitive context. If insufficient, ask PM: "I don't have enough competitive data. I can research the top 3-5 competitors now, or we can take this as a separate activity — which do you prefer?" If PM says now, conduct web research within the session. If PM defers, offer to capture as action item in `project-daily`.

**Section 8 (High-Level Phasing)**: Propose phase structure from phasing signals in documents and requirement priorities. Always lightweight — detailed scope belongs in `product-scope`.

### A5. Writing Changes

- PM can enrich multiple sections in one session. Track what has been discussed and confirmed.
- Before writing, show a diff of proposed updates. PM can choose: a single grouped diff at the end, or a diff after each section. Default to grouped unless PM prefers per-section. Never auto-write.
- End every session with: "Anything else to add or refine?" as a final open input step.

### A6. Routing Check

At the end of the session (before the final write), scan for decisions and assumptions that emerged from the coaching Q&A — strategic pivots, persona decisions, scope boundary commitments, market positioning choices. Present any unrouted items: "These decisions emerged during our session — route to project-assumptions? [list]." PM confirms, skips, or adjusts. Confirmed items are written to `project-assumptions.md` as Decided entries with source `product-brief session ({date})`. If `project-assumptions.md` does not exist, skip silently.

### A7. After Writing

- Update frontmatter `last_updated` and `last_updated_by: manual — /product-brief`.
- Log audit entry to `project-daily`: `[MANUAL] product-brief updated via /product-brief — {sections updated} ({date})`.
- Run outbound routing (Section D).

---

## B. Auto-Creation (called from project-initiation)

### B1. Prerequisites

`client-overview.md` and `project-overview.md` must exist before this skill runs — both are created earlier in the initiation flow.

### B2. Read Context

Read `project/management/client-overview.md` (Sections 3, 4, 6, 7 for business model, market position, strategic priorities, tech landscape) and `project/management/project-overview.md` (Sections 1, 2, 6 for project description, goals, use cases). Also read the PM's free-text input from the initiation conversation (passed by `project-initiation`). If any source does not exist, skip silently. No documents are available — document ingestion happens after initiation.

### B3. Aggressive Pre-Fill

Create `product/problem-space/product-brief.md` using the template. Pre-fill **every section possible**:

- **Section 1 (North Star)**: `-tbd-` — requires PM synthesis via enrichment.
- **Section 2 (Problem Definition)**: Pre-fill from PM's initiation input (problem context, target users), `client-overview` Business Model and Strategic Priorities. "Why Current Approaches Fail" table pre-filled if PM described existing solutions.
- **Section 3 (Target User Personas)**: Pre-fill from PM's input about target users. Structured fields populated where data exists; remaining `-tbd-`.
- **Section 4 (Business Goals & Success Metrics)**: Pre-fill from PM's goals and milestones context, `client-overview` Strategic Priorities. Metrics `-tbd-` unless explicitly stated.
- **Section 5 (Solution Definition)**: Pre-fill from PM's context about what's being built, `client-overview` Product & Tech Landscape. Four perspectives populated where data exists.
- **Section 6 (Market Positioning)**: Pre-fill from `client-overview` Market & Competitive Position. Likely mostly `-tbd-` without documents or web research.
- **Section 7 (Scope Boundaries)**: Pre-fill from PM's context about deliverables and scope boundaries.
- **Section 8 (High-Level Phasing)**: Pre-fill from PM's timeline and milestone context.

### B4. Field Handling

- Fields without reliable data: `-tbd-`.
- Low confidence: `> Needs confirmation — [what was found and why it's uncertain]`.
- Conflicting sources: `> Needs confirmation — [source A says X, source B says Y]`.
- Never fabricate.

### B5. Complete

- Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — project-initiation`.
- Complete silently — no summary, no prompts, no interruptions to the initiation flow. Do NOT ask additional questions — work only with what the PM already provided and what's in the prerequisite artifacts.
- Do NOT perform web research at creation. Web research is available during `/product-brief` enrichment sessions.
- Pre-fill quality depends on upstream data quality. If `client-overview` has many `-tbd-` fields, this document will mirror those gaps. Do not attempt to compensate for missing upstream data.
- Run outbound routing (Section D).

---

## C. Inbound Routing (from meetings and documents)

`project-meeting` and `project-document` route brief-relevant content via PM-confirmed routing review. The routing review is owned by the originating skill — this skill receives the writes.

### Routable content

- Problem framing changes or refinements → Section 2
- New user persona information → Section 3
- Business goal signals → Section 4
- Solution definition insights → Section 5
- Competitive/market intelligence → Section 6
- Scope direction signals → Section 7
- Phasing indications → Section 8

### Persona handling

- If routed content refines an existing persona, update the existing persona subsection — do not create a duplicate. Check existing persona names and roles before creating a new entry.
- If routed content suggests a new persona, create a new subsection with available fields and `-tbd-` for the rest.
- If uncertain whether it's a new persona or an update, mark with `> Needs confirmation — [possible duplicate of {existing persona name}]`.

### After each routed write

- Update frontmatter `last_updated` and `last_updated_by: auto — {source skill} routing`.
- Log audit entry to `project-daily`: `[AUTO] product-brief — {section name} updated from {source-slug} ({date})`.
- Run outbound routing (Section D).
- If `product-brief.md` does not exist when a routing write is attempted, create it from template first, then write. Log: `[AUTO] product-brief — file created and {section} updated from {source-slug} ({date})`.
- If `project-daily` does not exist, create it first.

---

## D. Outbound Routing (after every write)

After every write to `product-brief.md` (manual or routed), silently route relevant content outbound:

1. **Engagement goals and problem framing** → `client-overview.md` Engagement Context section. If `client-overview.md` does not exist, skip silently.
2. **Goals and problem framing** → `project-overview.md` Project Goals and Key Use-Cases & Problems sections. If `project-overview.md` does not exist, skip silently.

Outbound routing writes only the relevant subset of data — not the entire brief. Goals route as goal statements. Problem framing routes as problem summaries.

Each outbound write is logged as a separate audit entry to `project-daily`.

---

## E. Phasing Sync with product-scope

Section 8 (High-Level Phasing) has a bidirectional sync with `product-scope`:
- When `product-scope` changes phases, focus, target release, or key outcomes, Section 8 is updated automatically.
- Section 8 serves as strategic input when `product-scope` is created.

The sync only fires when phasing content actually changed — preventing re-trigger loops.

---

## Rules

- **8 sections always present**: All sections exist, even if `-tbd-`.
- **Coaching, not form-filling**: The enrichment experience is a strategic coaching session. Probe, propose, suggest activities — don't just ask "what should I put here?"
- **Client-ready language**: No internal jargon. Professional but accessible.
- **Section 8 is always lightweight**: If PM provides detailed scope, redirect to `product-scope`.
- **Structured personas**: Section 3 personas always use the structured field format (Role/Title, Context, Primary Goal, Pain Points, Success Looks Like). No narrative-only personas.
- **No persona deletion**: Personas are marked `Status: Retired` with rationale, not deleted.
- **North Star requires explicit PM confirmation**: Proposals are marked `> PM review needed` and field stays `-tbd-` until PM confirms.
- **`-tbd-` over fabrication**: Never fabricate data. Low-confidence fields use `> Needs confirmation`.
- **PM confirms all manual writes**: Always show diff, always wait for confirmation. Never auto-write during enrichment.
- **`status` is PM-controlled**: Frontmatter `status` stays `wip` until PM explicitly marks `stable`. Never auto-promote.
- **Preserve existing content**: When writing, preserve all existing content exactly. Only targeted sections and fields are modified.
- **Machine-readable format**: Clear section headers, consistent structured fields, predictable formatting. Other skills reference this document programmatically.
- **Audit everything**: Every write (manual and routed) logs to `project-daily`. If `project-daily` does not exist, create it first.
- **All sections already populated**: `/product-brief` still presents health summary and allows PM to refine. Proactively check for internal consistency across sections and flag contradictions.
