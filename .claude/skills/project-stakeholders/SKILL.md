# project-stakeholders — Skill Logic

> The living map of everyone involved in the project. External stakeholders are tracked with roles, influence, sentiment, and relationship context. Internal stakeholders are tracked with roles only — no sentiment analysis. The document is created during `project-initiation` and enriched continuously via routing and PM interaction.

---

## When This Skill Runs

This skill runs when the PM invokes `/project-stakeholders`, when other skills route stakeholder updates, or when `project-initiation` seeds the initial entries.

Parse the PM's intent:
- No arguments or general request → run **Review Mode** (Section A)
- Specific update request → apply it directly (Section B)
- Called from `project-initiation` → run **Seeding Mode** (Section C)
- Called from another skill's routing → run **Routing Mode** (Section D)

---

## A. Review Mode

1. **Load context**: Read `project/management/project-stakeholders.md` (full file). Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match (e.g., recent meeting notes for attendee context). If any file does not exist, skip silently.
2. **Analyze the map**: Identify:
   - Count of `-tbd-` fields across all entries
   - External stakeholders missing sentiment context
   - Incomplete org chart sections
   - Active external stakeholders with `Last interaction` older than 14 days (stale)
3. **Present review summary**: Show the PM: total stakeholder count (internal vs external), `-tbd-` count, stale entries, and key gaps.
4. **Ask what the PM wants to do**: PM can:
   - Provide specific updates → apply them (show diff, confirm before writing)
   - Request a guided walkthrough of gaps → go through stakeholders with the most `-tbd-` fields first, asking targeted questions: "STK-003 (David, Legal Counsel) — I have no influence level, sentiment, or communication preference. Any context on David?" PM can answer, skip, or defer each.
   - Add new stakeholders → create entries with whatever is provided, `-tbd-` for the rest
5. **Before writing any changes**: Show a diff of what will change. Wait for PM confirmation. Never auto-write in review mode.
6. **End the session**: Ask "Anyone else to add or update?" as a final open input step.
7. **After writing**: Log audit entry to today's `project-daily`: `[MANUAL] project-stakeholders updated via /project-stakeholders — {what changed} ({date})`. Run cross-artifact sync (Section E).

---

## B. Conversational Updates (without command)

When the PM provides stakeholder updates in natural conversation (not via `/project-stakeholders`):

1. Read `project/management/project-stakeholders.md`.
2. Apply the requested changes directly — no routing review needed (PM is explicitly telling you what to write).
3. Write the updated file. Log audit entry to `project-daily`: `[MANUAL] project-stakeholders — {what changed} ({date})`.
4. Run cross-artifact sync (Section E).
5. If today's `project-daily` does not exist, create it first using the daily template.

---

## C. Seeding Mode (called from project-initiation)

When `project-initiation` passes stakeholder names and roles:

1. Create `project/management/project-stakeholders.md` using the template from `.claude/skills/project-stakeholders/TEMPLATE.md`.
2. For each person provided:
   - Assign the next sequential `STK-{NNN}` ID
   - Set name and role (if provided)
   - Place in the correct section: Internal Team if internal, External Stakeholders if external. If unclear, default to external.
   - All other fields set to `-tbd-`
   - Status: `Active`
3. Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — project-initiation`.
4. Complete silently — no summary, no prompts, no interruptions to the initiation flow.
5. Run cross-artifact sync (Section E) — sync thin indexes to `client-overview` and `project-overview` if those files exist.

---

## D. Routing Mode (called from other skills)

When `project-meeting`, `project-document`, or other skills route stakeholder updates:

1. The originating skill presents the routing candidates to the PM as part of its routing review. Candidates may include:
   - New stakeholders discovered (with proposed role and organization)
   - Role changes
   - Sentiment signals for external stakeholders (must include context — never a bare label)
   - Communication preferences observed
   - Expectations stated
   - Engagement signals
   - Location information
   - Aliases or nicknames discovered
2. PM confirms, skips, or adjusts each candidate before writing.
3. For confirmed updates:
   - **New stakeholder**: Create entry with available fields, `-tbd-` for the rest. Assign next sequential STK-ID.
   - **Existing stakeholder update**: Update the specific fields. For sentiment, always update the label AND context together.
   - **Alias match**: When a name or nickname matches an existing stakeholder's aliases, update the existing entry — do not create a duplicate. Add new aliases to the `Aliases` field.
4. `Last interaction` is automatically updated whenever a stakeholder appears as an attendee in a processed meeting — this is mechanical and does not require PM confirmation.
5. After writing: Log audit entry to `project-daily`: `[AUTO] project-stakeholders — {what changed} from {source} ({date})`.
6. Run cross-artifact sync (Section E).

---

## E. Cross-Artifact Sync

After every modification to `project-stakeholders.md`, silently sync thin indexes:

1. **`project-overview.md` Delivery Team section**: All active internal team members — ID, name, role, slug reference. If `project-overview.md` does not exist, skip silently.
2. **`project-overview.md` Client Stakeholders section**: Key client stakeholders only (high influence, most active counterparts, people responsible for the project) — ID, name, role, slug reference. If `project-overview.md` does not exist, skip silently.
3. **`client-overview.md` Stakeholder Map section**: All client/external stakeholders (active and key inactive) — no internal team. ID, name, role, slug reference. If `client-overview.md` does not exist, skip silently.

These syncs are silent — no PM confirmation, no separate audit entries (the primary audit entry already covers the change).

---

## F. Inactive Stakeholders

When a stakeholder leaves the project (team member on leave, client contact changes roles, vendor relationship ends):

1. Set their `Status` to `Inactive`.
2. Set `Left` date and reason (if known).
3. Move the entry to the `Inactive` subsection within their group (Internal Team or External Stakeholders).
4. Never delete a stakeholder entry — historical context is preserved.

---

## G. Org Chart

The org chart section tracks client-side reporting lines and decision-making structure. Build it progressively from:
- Meeting transcripts (reporting references, escalation patterns, who defers to whom)
- Ingested documents (org charts, SoWs listing reporting lines)
- Direct PM input

When a new reporting relationship is detected during routing, include it in the routing review for PM confirmation before updating the org chart. Keep it as a text-based hierarchy.

---

## H. Stakeholder ID Assignment

- IDs use a shared sequence across internal and external stakeholders: `STK-001`, `STK-002`, etc.
- Assign by checking the highest existing ID and incrementing.
- IDs are never reused — if a stakeholder is marked inactive, their ID remains assigned.

---

## I. Duplicate Detection

Before creating a new stakeholder entry (in any write path — routing, seeding, review mode, or conversational adds):
- Check existing entries for name matches, alias matches, or role+organization matches.
- If a likely match is found, propose an update to the existing entry rather than creating a duplicate.
- If uncertain, ask the PM: "This may be the same person as STK-003 (David, Legal). Same person or new entry?"

---

## Rules

- **Sentiment always has context**: Never write a bare sentiment label. Every sentiment update must include the `Sentiment context` field explaining why.
- **No sentiment for internal stakeholders**: Internal team members have no influence, sentiment, or communication preference fields.
- **`-tbd-` over fabrication**: Unknown fields are always `-tbd-`, never guessed. No web research on stakeholders.
- **PM confirms all routing writes**: Nothing is written from routing without explicit PM approval. Exception: `Last interaction` date updates are mechanical and need no confirmation.
- **Audit everything**: Every modification to `project-stakeholders.md` gets an audit entry in `project-daily`.
- **File creation fallback**: If `project-stakeholders.md` or `project-daily` do not exist when needed, create them with appropriate structure first.
- **Stakeholder in both orgs**: If a person belongs to both the internal team and the client/external side (e.g., a consultant), ask the PM which section they belong in. Do not guess.
- **Bulk additions**: When adding 10+ stakeholders at once (e.g., from a kick-off attendee list), create all entries in one write and present the batch for PM confirmation.
