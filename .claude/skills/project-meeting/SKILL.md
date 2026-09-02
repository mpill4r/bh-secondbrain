# project-meeting — Skill Logic

> The meeting intelligence skill. Upload mode processes raw meeting input into structured notes and routes findings to harness artifacts. Prep mode generates meeting prep documents from harness context. Both modes maintain `meetings/index.md` as the central meeting directory.

---

## When This Skill Runs

This skill runs in two modes served by two commands:
- **`/project-meeting-upload`** → Upload Mode (Section A)
- **`/project-meeting-prep`** → Prep Mode (Section B)

---

## A. Upload Mode

### A1. Accept Input

Accept any of the following as input:
- Pasted transcript text
- Uploaded file path (`.txt` / `.rtf` / `.md` / `.docx`)
- PM's bullet-point notes
- Stream-of-consciousness brain dump
- FigJam board URL (via Figma MCP)

For `.rtf` files, strip RTF formatting codes before processing — extract plain text only.

If FigJam URL is provided, use Figma MCP to read the board. Treat sticky notes, diagrams, and text identically to a transcript. If Figma MCP is not active, inform the PM and ask them to paste the board content manually.

### A2. Language Handling

All meeting notes and routed harness artifacts are always written in English regardless of the transcript language. Process the transcript in its original language and produce all outputs in English. Direct quotes from non-English transcripts are translated and marked `[translated from {language}]`.

### A3. tldv Processing

The primary transcript source is tldv. When processing tldv output:
1. Format is `Speaker Name [MM:SS]: utterance` — use full names for all attribution, never shorthand.
2. Timestamps are precise — use as-is for sequencing.
3. Exports may contain double-spaced words — normalize whitespace before processing.
4. Repeated filler words (e.g. "yeah, yeah, yeah...") are a transcription artifact of verbal agreement — treat as acknowledgment, not quotable content.

If a tldv recording link is provided, store in frontmatter as `tldv_link` and display in the Meeting Header. The transcript must always be provided as text or file — the link is a reference only.

### A4. Read Bootstrap Context

Before processing, silently read:
- `meetings/index.md` — for recurring meeting detection and previous instances
- `project/management/project-stakeholders.md` — for person recognition and role attribution
- Last 3 entries in `project/daily/` — for recent context
- Any `product/solution-space/product-scope-*.md` files — for feature/epic awareness
- `product/problem-space/product-brief.md` — for strategic framing (problem definition, goals, personas)

This is a fixed bootstrap set — not driven by the index. If any of these files do not exist, skip silently and proceed without that context.

### A5. Determine Meeting Metadata

Determine from the input: meeting title, date, type (internal / client / external / milestone), attendees with roles. If anything is unclear or ambiguous, ask whatever follow-up questions are needed — there is no limit on clarifying questions. Always prefer asking over assuming incorrect information.

The meeting slug is derived automatically from title and date: `YYYY-MM-DD-{meeting-title-slug}.md`. If the title is unclear, ask. The slug must be descriptive — `2026-03-29-rivelo-proposal-call.md` not `2026-03-29-meeting.md`.

### A6. Recurring Meeting Intelligence

After determining metadata, check `meetings/index.md` for previous instances of the same meeting. Use judgment — title similarity, attendee overlap, or both may signal a recurring meeting. Do not over-match; when in doubt, treat as a new thread.

If a previous instance is found:
- Add a `Previous session` link in the meeting header.
- Read the previous meeting note and actively use its content: check whether action items from the previous session were resolved in this meeting, note which open questions were answered, assess overall progress (are things moving forward or stalling?).
- Include this assessment in the TL;DR and in relevant sections — do not just reference the previous session, reflect on continuity.

If a meeting prep file exists in `meetings/prep/` for the same meeting (matched by date and slug pattern), link it in the meeting header as `Meeting prep`.

### A7. Write Meeting Note

Produce a structured meeting note following the template. Write to `meetings/{type}/YYYY-MM-DD-{slug}.md`.

The sections are the default structure. Use judgment on what applies — very short meetings (standups, quick syncs) can compress or omit less relevant sections; complex workshops or discovery sessions can add additional sections if the content warrants it. Structure serves the content, not the other way around.

Section-specific requirements:
- **TL;DR**: 2-3 sentences max. Answer: what happened, what was decided, what shifted.
- **Key Discussion Points**: Attribute viewpoints to named individuals. Include direct quotes where impactful. Quotes from non-English transcripts are translated and marked `[translated from {language}]`.
- **Sentiment & Tone**: Appears in every meeting note. For internal and external meetings, capture a brief sentiment read (e.g. "productive and aligned", "tense on timeline"). For client and milestone meetings, provide a deeper relational analysis: overall tone, tension or resistance, relationship signals, anything not said explicitly but evident from the dynamic.
- **Action Items**: Structured as: `- [ ] **{Owner}**: {Task} — due {deadline if mentioned} — from {meeting slug}`.

Raw transcripts are never stored in the `meetings/` folder. The structured meeting note is the only output.

### A8. Routing Review

After writing the meeting note, extract all routing candidates and present them to the PM as a structured review list grouped by artifact before writing anything to harness artifacts.

Read `.claude/harness-artifacts-index.md` and assess every registered artifact. Any artifact where relevant content was found — per the routing conditions defined in the index — is included in the routing review. Routing targets are determined by the index — not hardcoded.

While preparing routing candidates, read each target artifact and flag contradictions between the meeting content and the artifact's current state (e.g. "This meeting states delivery pushed to Q3, but `project-overview` currently shows Q2 — which is correct?"). PM resolves conflicts during the review.

**Product artifact routing classification**: Use the bootstrap context (product-brief, product-scope) to classify routing candidates to the correct product artifact level:
- **Problem framing, personas, goals, competitive insights, solution direction** → `product-brief` (strategic level)
- **Epic decisions, feature identification, priority shifts, timeline changes, estimation, deferrals** → `product-scope` (delivery planning level)
- **Acceptance criteria, edge cases, UX flows, design decisions for a specific feature** → `product-feature` (implementation detail level — must reference a FEAT-NNN)
- **Raw requirements, constraints, success criteria** → `product-requirements` (capture level)

When content could route to multiple product artifacts, route to each appropriate target — the PM confirms per artifact.

**Action items** are included in the routing review as structured task entries. They are written to today's `project-daily` only after PM confirms. If today's `project-daily` does not exist, create it first.

The PM can reply "confirm all", skip individual items, or adjust content before anything is written. PM can adjust individual routing candidates inline in conversation — they type the corrected content and the skill applies it before writing. Only after PM confirms are artifacts updated.

If a routing target artifact does not exist, create it by reading the target skill's TEMPLATE.md (at `.claude/skills/{owner-skill}/TEMPLATE.md`) and using it as the scaffold — this ensures correct frontmatter, section structure, and entry format from the start.

### A9. After Routing Confirmation

1. Write approved items to harness artifacts. Before writing to any target artifact:
   - **Read the target's TEMPLATE.md** (at `.claude/skills/{owner-skill}/TEMPLATE.md`) to learn the prescribed entry format and section structure.
   - **Conform routed content to that format exactly** — use the template's field names, layout, and conventions. Do not invent table structures, add fields, or use conventions (like MoSCoW priority) that the template doesn't define.
   - **Continue the artifact's ID sequence** — scan the existing artifact for the last used ID (e.g., REQ-047, ASM-012, LL-005) and increment for each new entry.
   - **Place entries in the correct section** — sectioned artifacts (e.g., product-requirements has Product / Business / Data / Design / Tech / Other sections) require entries under the matching section heading, not appended at the end.
   - **Update index tables** — if the template defines an index table (e.g., project-assumptions has an Index table at the top), add a row for each new entry.
2. Write the Routing Log section in the meeting note.
3. Silently log audit entries to today's `project-daily` — one entry per target artifact using the canonical format: `[AUTO] {target-artifact} — {what changed} from {meeting-slug} ({date})`. Audit entries are automatic bookkeeping after confirmation — they are not part of the routing review. If `project-daily` does not exist, create it first.
4. Silently trigger `project-lessons` — the skill reviews the full meeting note for generalizable insights and writes any lessons autonomously. Before writing, read `.claude/skills/project-lessons/TEMPLATE.md` for the LL-NNN entry format and continue the existing ID sequence. This is not part of the routing review and requires no PM confirmation.

### A10. Follow-Up Draft

After PM confirms routing, offer to draft a follow-up message for any meeting type. Format: short, professional message covering what was discussed, decisions made, action items with owners, and next steps. No internal jargon — suitable for sending to any attendee.

The follow-up draft is shown in conversation for PM review. PM copies and sends manually. It is not saved as a file.

### A11. Meetings Index

Every processed meeting is added to `meetings/index.md` with: date, type, attendees, TL;DR, file link, decisions count, action items count. Counts reflect confirmed and routed items only — not all extracted candidates. If `meetings/index.md` does not exist, create it with appropriate headers before adding the first entry.

---

## B. Prep Mode

### B1. Q&A Session

Before reading any harness context, run a Q&A session with the PM to understand:
- Meeting goal(s)
- Key topics to discuss
- Specific areas where the PM wants the harness to help (e.g. "I need context on their tech stack", "remind me what decisions are still open with them", "help me handle their concern about timeline")

This input drives what harness content is pulled. The Q&A should be conversational and grouped — not a rigid form.

### B2. Harness Reading

Based on the PM's stated goals and questions, read `.claude/harness-artifacts-index.md` and select relevant artifacts using the "Read for context when" conditions defined in the index. Do NOT blindly read all artifacts — read what is relevant to this specific meeting's purpose.

Always check `meetings/index.md` and previous meeting notes for any meeting with prior history.

### B3. Write Prep Document

Produce a meeting prep document at `meetings/prep/YYYY-MM-DD-{slug}-meeting-prep.md` following the template.

Section-specific requirements:
- **Meeting Overview**: Explicitly state the meeting goal(s) as provided by the PM in the Q&A — not inferred, but verbatim or lightly structured from what PM said.
- **Open Items to Resolve**: If this is a recurring meeting, include a progress assessment from previous sessions — what was committed to, what was resolved, what is still outstanding.
- **Talking Points & Watch-outs**: Must be grounded in actual harness data — stakeholder sentiment from `project-stakeholders.md`, recent assumptions/decisions from `project-assumptions.md`, relevant scope context. No generic advice.

### B4. Prep Index Entry

Add the prep document to `meetings/index.md` with type `prep`. If `meetings/index.md` does not exist, create it with appropriate headers before adding the first entry.

### B5. Prep Date Check

If the meeting date has already passed, detect and warn: "This meeting date has already passed. Do you want to run upload mode instead?"

---

## Rules

- **Raw transcripts never stored**: The structured meeting note is the only output in `meetings/`. If PM wants to archive the original, use `/project-document`.
- **Any input quality accepted**: Clean transcripts, messy notes, incomplete brain dumps — never refuse to process. Work with what's available and mark gaps explicitly.
- **Human-readable notes**: Meeting notes should make sense to someone who was not in the meeting.
- **PM confirms all routing**: Nothing is written to harness artifacts until PM explicitly confirms. The review step is lightweight — PM can confirm all at once — but nothing is committed without approval.
- **Routing targets from index**: Read `.claude/harness-artifacts-index.md` to determine routing targets — never hardcode artifact lists.
- **Audit entries are automatic**: After PM confirms routing, audit entries are silently logged to `project-daily`. No additional confirmation needed.
- **Meeting type ambiguous**: Ask once — never assume the type.
- **tldv link is reference only**: If PM provides only a tldv link without transcript, ask them to provide the transcript as text or file.
- **First recurring session**: No previous instance found — no progress assessment, no open items carry-forward. Treated as a new thread.
- **`harness-artifacts-index.md` missing**: This is a configuration error. Notify PM that the index is missing and routing cannot proceed. The meeting note is still written, but routing is blocked until the index is restored.
- **English output**: All outputs (meeting note, routing candidates, routed content) are always in English regardless of transcript language.
- **Descriptive slugs**: `2026-03-29-rivelo-proposal-call.md` not `2026-03-29-meeting.md`.
- **Sentiment in every note**: Brief for internal/external meetings; deeper relational analysis for client/milestone meetings.
- **Prep reads selectively**: Prep mode reads only artifacts relevant to the meeting purpose — not all artifacts.
- **Preserve existing content**: When writing routed content to harness artifacts, preserve all existing content exactly. Only add or update targeted entries.
- **Respect target artifact entry format**: Before writing to any artifact, read its owning skill's TEMPLATE.md (at `.claude/skills/{owner-skill}/TEMPLATE.md`) for the prescribed entry format. Use that format exactly — do not invent table structures, add fields, or use conventions the template doesn't define. The TEMPLATE.md is the authoritative format source.
- **Conflicts flagged during routing**: Contradictions between meeting content and existing harness state are flagged in the routing review with specific details. PM resolves before writing.
