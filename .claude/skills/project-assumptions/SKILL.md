# project-assumptions — Skill Logic

> The single tracking artifact for all ideas, directions, assumptions, and decisions. Captures everything the team believes, proposes, or commits to — from early-stage ideas to firm commitments. Tracks the lifecycle from Open through Decided or Retired. The key value-add: proactive impact analysis across trade-off dimensions for every assumption.

---

## When This Skill Runs

This skill runs when the PM invokes `/project-assumptions`, when other skills route assumptions, or when `project-initiation` creates the skeleton file.

The skill is conversational — PM types requests in plain language. No explicit modes.

---

## A. Starting a Session

1. **Load context**: Read `project/management/project-assumptions.md` (full file), `project/management/project-stakeholders.md` (for person resolution), and `product/problem-space/product-requirements.md` (for cross-reference awareness — know which REQ-IDs exist). Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match the current task. If any file does not exist, skip silently.
2. **Present summary**: "You have X open, Y decided, Z retired. What would you like to do?"
3. Wait for PM input and respond conversationally.

---

## B. Adding Assumptions

When the PM provides a new assumption:

1. **Assign ID**: Check the highest existing ASM-ID in the file. Assign the next sequential ID. IDs are never reused.
2. **Resolve person**: Use `project-stakeholders.md` to resolve person references. When PM says "Peter suggested this", look up Peter's full name and stakeholder ID.
3. **Draft the entry**:
   - ID: next sequential
   - Created: today's date
   - Source: meeting slug, document slug, or "PM session"
   - By: stakeholder name (STK-ID) or "Team" for group decisions
   - Status: `Open ({today})` by default, or `Decided ({today})` if PM explicitly says this is already committed
   - Description: plain language, 1-3 sentences
   - Rationale: why this was proposed
4. **Proactively analyze impact**: Think broadly across dimensions — timeline, budget, scope, quality, team, client relationship, technical debt, risk. Select the relevant dimensions for this assumption. Draft a structured impact assessment with:
   - Specific trade-offs (positive and negative)
   - Second-order consequences the PM might not have considered
   - References to actual project context (current phase, team size, deadlines)
   - Impact must be genuinely useful, not boilerplate. "Timeline: Neutral" for everything is a failure.
5. **Check for duplicates**: Before presenting, check existing entries for similar assumptions. If a match exists, surface it: "ASM-008 covers something similar — is this the same or a distinct assumption?" PM decides.
6. **Check for conflicts**: If the new assumption conflicts with an existing decided assumption, flag it: "This conflicts with ASM-005 (web-only). If accepted, ASM-005 may need to be retired." PM decides.
7. **Check for requirement overlap**: If the assumption overlaps with an existing requirement in `product-requirements.md`, surface the match: "REQ-014 already covers EU data residency. Is this assumption different, or should it reference the existing requirement?" PM decides.
8. **Present the full draft** (including impact) to PM for review. PM can adjust any field.
9. **Write after confirmation**: Update the file — add the entry to the Entries section (newest first) and update the Index table.
10. **Multiple assumptions in one interaction**: Each gets its own impact analysis. Present all drafts for a single grouped confirmation. If multiple people claim the same assumption, use "Team" as the By field and note the contributors in the rationale.

---

## C. Updating Status

### Open → Decided

When PM says "we're going with ASM-012" or a meeting/document confirms it:

1. Update status to `Decided ({today})`.
2. PM can optionally add or update the rationale.
3. Re-evaluate impact if the decision changes the trade-off picture.
4. Show the updated entry for confirmation before writing.
5. Update the Index table.

### Open/Decided → Retired

When PM says "retire ASM-008" or "ASM-008 is no longer relevant":

1. Update status to `Retired ({today})`.
2. PM provides or confirms the retirement reason — append to the Rationale field.
3. Show the updated entry for confirmation before writing.
4. Update the Index table.

### Hard Decisions (direct to Decided)

Assumptions that are already committed when first captured can be created directly as `Decided` — they skip the Open stage. Use step B with `Decided` status.

### Cross-references

When a decided assumption generates a downstream artifact:
- Spawns a requirement → add `→ REQ-NNN` at the end of the Impact section
- Superseded by another assumption → add `→ superseded by ASM-NNN`
- Related to another assumption → add `→ see ASM-NNN`

---

## D. Reviewing and Querying

PM can ask for any filtered view or analysis:
- "Show all open assumptions"
- "What's decided about architecture?"
- "Any retired items from last week?"
- "What open assumptions have high impact?"
- "Are there open items older than 14 days?"

Read the document and synthesize a targeted answer.

---

## E. Routing from Other Skills

When `project-meeting` or `project-document` routes assumptions:

1. Assumptions appear as a grouped block in the routing review — PM can confirm the block, skip it, or expand to review individually.
2. For each routed assumption:
   - Assign `Open` status by default
   - Set the meeting or document slug as source
   - Draft an impact analysis — include in the routing review so PM sees it before confirmation
3. Check for conflicts: if a new assumption conflicts with an existing decided assumption, flag it: "ASM-019 conflicts with ASM-005 (web-only). If ASM-019 is accepted, ASM-005 should be retired."
4. Check for duplicates: if a similar assumption already exists, surface the match rather than creating a duplicate.
5. After PM confirms routing, write all entries and update the Index table.
6. Log audit entry to today's `project-daily`: `[AUTO] project-assumptions — {N} assumptions added from {source-slug} ({date})`.
7. If `project-assumptions.md` does not exist, create it using the template first.

---

## F. File Maintenance

- **Index table**: Update on every write — must always reflect current state of all entries.
- **Frontmatter**: Update `last_updated` on every write. Set `last_updated_by` to the appropriate source (e.g., `auto — project-meeting routing`, `manual — /project-assumptions`).
- **Preserve existing entries**: Only the targeted entry is modified. All other entries remain exactly as they are.
- **Assumptions are never deleted**: Only Retired. If PM asks to delete, explain and offer to retire instead.

---

## Rules

- **PM confirms everything**: Every entry and every status change requires PM confirmation before writing. The skill never auto-promotes Open to Decided.
- **Impact is the value-add**: The proactive impact analysis is what makes this skill useful. Surface non-obvious trade-offs, second-order consequences, and risks. Be specific to the assumption and reference actual project context.
- **Person resolution**: Always pre-read `project-stakeholders.md` to resolve person references. Use full name and STK-ID.
- **`-tbd-` over fabrication**: Unknown fields are always `-tbd-`, never guessed.
- **Audit everything**: Log to `project-daily` after every write. If `project-daily` does not exist, create it first.
- **Plain language**: Entries must be understandable by a stakeholder or new team member without project context.
