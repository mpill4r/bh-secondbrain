# product-requirements — Skill Logic

> The single structured source of truth for everything the product must do and why. Collects all requirements from meetings, documents, and PM input. Tracks each from Open (captured) through Processed (solution defined) or Deferred (out of scope). The skill is conversational — PM interacts in plain language.

---

## When This Skill Runs

This skill runs when the PM invokes `/product-requirements`, when other skills route requirements, or when `project-initiation` creates the skeleton file.

The skill is conversational — no explicit modes. Infer intent from PM's input.

---

## A. Starting a Session

1. **Load context**: Read `product/problem-space/product-requirements.md` (full file), `project/management/project-stakeholders.md` (for person resolution), and `project/management/project-knowledge.md` (for classification accuracy — domain terms, naming conventions, data model context). Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match the current task. If any file does not exist, skip silently.
2. Respond to the PM's request conversationally. Handle: add, review, mark processed, defer, change type, toggle high-priority, edit description, gap summary.

---

## B. Adding Requirements

When the PM provides a new requirement:

1. **Resolve person**: Use `project-stakeholders.md` to look up the person who raised it. Use their full name and role in the Source field.
2. **Assign ID**: Check the highest existing REQ-ID in the file. Assign the next sequential ID. IDs are never reused — if a requirement was removed, its ID is retired.
3. **Classify type**: Propose the best-fit type (Product / Business / Data / Design / Tech / Other). Ask one clarifying question if genuinely ambiguous — never write without agreement on type. For cross-cutting requirements, pick the closest type and note the overlap in the description.
4. **Assess priority**: If the requirement sounds critical, propose the `high-priority` tag. Most entries should NOT have it — it's for the genuinely critical few.
5. **Draft the entry** in the entry format:
   ```
   **REQ-NNN** · {Type} · Open [· high-priority] · {YYYY-MM-DD}
   **Source**: {Person} via {artifact-slug}

   {Requirement description — one paragraph, plain language}
   ```
   - Source artifact: meeting slug, document slug, or current `project-daily` slug if PM is adding from memory
   - Source person: stakeholder name or "PM" for direct additions
   - Rewrite jargon-heavy input into clear, plain language. Show the rewrite to PM.
6. **Present the draft** for PM confirmation. PM can adjust type, priority, description, or source.
7. **Check for duplicates**: Before drafting, check existing entries for near-identical requirements. If a match is found, surface it: "REQ-005 covers something similar — is this the same or a distinct requirement?" PM decides.
8. **Multiple requirements in one interaction**: Group all drafts and present for a single confirmation — not one by one.
9. **Write after confirmation**: Place the entry in the correct type section. Update `last_updated` frontmatter.

---

## C. Updating Requirements

### Mark as Processed

Two paths:
- **Auto-sync from `product-scope` or `product-feature`**: When those skills address a requirement, they update the status to `Processed` and add the `Addressed in` link automatically. Audit entry logged to `project-daily`.
- **Manual via this skill**: PM provides the REQ-ID and the scope or feature file where it's addressed. Show the updated entry with `Addressed in` link for PM confirmation before writing.

### Defer

PM specifies REQ-ID and optionally a reason. Update status to `Deferred`. If a reason is provided, append to the description in parentheses: `(Deferred: {reason})`. Show the updated entry for PM confirmation before writing. Deferred requirements are never deleted — they remain in their type section.

### Change Type or Toggle high-priority

Move the entry to the correct section if type changes. Update the metadata line. REQ-ID does not change. Show updated placement for PM confirmation.

### Edit Description

PM can refine any entry's description. Show the proposed change for confirmation.

---

## D. Reviewing and Querying

PM can ask for any filtered view:
- "Show all Open business requirements"
- "What high-priority items are still Open?"
- "Do we have any data requirements about GDPR?"
- "What's missing?" → surface entries with missing source fields, types with no requirements, Open items older than 14 days

Read the document and synthesize a targeted answer.

---

## E. Routing from Other Skills

When `project-meeting` or `project-document` routes requirements:

1. Requirements appear as a **grouped block** in the routing review — grouped under "Product Requirements", not listed item-by-item alongside other artifact types.
2. PM can confirm the entire block, skip it, or expand to review and adjust individual entries.
3. For each routed requirement:
   - Assign `Open` status
   - Set the meeting or document slug as source artifact
   - Set the named person (already resolved by the originating skill) as source person
   - Place in the correct type section
4. **Check for duplicates**: If a near-identical requirement already exists, surface the match: "REQ-005 covers something similar — is this the same or a distinct requirement?" PM decides.
5. After PM confirms, write all entries to the file.
6. Log audit entry to `project-daily`: `[AUTO] product-requirements — {N} requirements added from {source-slug} ({date})`.
7. If `product-requirements.md` does not exist, create the full skeleton file first (using the template), then write entries. Note in audit: `[AUTO] product-requirements — file created and {N} requirements added from {source-slug} ({date})`.

---

## F. File Maintenance

- **Frontmatter**: Update `last_updated` on every write. `status` is always `wip` — requirements are never declared stable during active project work. Set `last_updated_by` to the appropriate source.
- **Preserve existing entries**: When writing, preserve all existing entries exactly. Only the targeted entry is modified. Requirements may be moved between type sections on reclassification, but no content is silently altered.
- **All changes shown to PM**: Every modification is shown to PM before writing. No silent alterations.

---

## Rules

- **Never infer requirements**: If PM discusses a problem but doesn't explicitly identify it as a requirement, do not add it. May ask: "Should I add this as a requirement?"
- **Never delete requirements**: Requirements are never deleted — only Deferred. If PM asks to delete, explain and offer to defer instead.
- **Every requirement has a source**: Person and artifact. Direct PM additions use "PM" as person and current `project-daily` slug as artifact.
- **Plain language**: Rewrite jargon-heavy input into clear language intelligible to non-engineers. Show the rewrite before saving.
- **Person resolution**: Always pre-read `project-stakeholders.md` to resolve person references.
- **`-tbd-` over fabrication**: Unknown fields are always `-tbd-`, never guessed.
- **Audit everything**: Log to `project-daily` after every write. If `project-daily` does not exist, create it first.
- **File creation fallback**: If `product-requirements.md` does not exist, create the skeleton first.
- **IDs are sequential**: REQ-001, REQ-002, etc. Never reused, never backfilled.
