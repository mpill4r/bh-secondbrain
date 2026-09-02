# project-daily — Skill Logic

> The daily context log is the primary continuity mechanism between sessions. It tracks project status, current priority, action items, session summaries, and an audit trail. The daily is primarily populated autonomously — data flows in from other skills. The `/project-daily` command is for explicit interactions: reviewing the day, closing, or querying across days.

---

## When This Skill Runs

This skill runs when the PM invokes `/project-daily`. It does NOT handle daily creation — that is managed by the CLAUDE.md session startup checklist using the TEMPLATE.md from this skill.

Before dispatching to a mode, run the **Pending Routing Check** below. Then parse the PM's arguments:
- No arguments or general review request → run **Review Mode** (Section A)
- `close` or intent to close the day ("close the day", "wrap up", "end of day") → run **Close Mode** (Section B)
- A question spanning multiple days ("what happened this week?", "show me all open action items", "what decisions were made since Monday?") → run **Query Mode** (Section C)

### Pending Routing Check

Runs first, regardless of mode. Purpose: the PM has been surprised before by jumping straight to `/project-daily` after a meeting/document upload and finding the discussed action items and updates missing — because routing was presented but never confirmed. This check surfaces that state loudly instead of letting it pass silently.

1. Check `meetings/index.md` and `documents/index.md` for entries dated today.
2. For each, open the source file and check its `Routing Log` (meetings) or equivalent routing section (documents). If it still reads as the unfilled placeholder (i.e. routing was never confirmed), it's pending.
3. If any pending items are found, lead with this before anything else in the response — do not bury it under the status/priority/action-item summary:
   > "⚠️ You have unconfirmed routing from today: {list of meeting/document titles}. Nothing from {them} has been written to the daily or other artifacts yet. Want to confirm now?"
4. If the PM confirms, run the routing review/write for those sources before continuing with whatever mode was requested.
5. If nothing is pending, proceed silently — no need to mention the check happened.

---

## A. Review Mode

1. Read today's daily at `project/daily/project-daily-YYYY-MM-DD.md`. If it does not exist, create it using the template (see Section D: Creation).
2. Present a summary to the PM:
   - Project status (RAG) with rationale
   - Current priority
   - Open action items — count and list the top items
   - Key events so far today
3. Ask the PM if anything needs adjusting. If the PM adjusts status or priority, update the daily immediately.

---

## B. Close Mode

Run the following steps in order. Write results directly — no PM confirmation needed (this is housekeeping).

### B1. Session Summary

Check today's Key Events section. If no session summary has been written yet today, write one based on the current conversation context — what was worked on, what decisions were made, any notable context. Keep it to 2-5 sentences.

### B2. Action Item Review

Scan all action items in today's daily. For each unchecked item, check if it was resolved today — look at session context, today's Key Events, and today's Audit Log for evidence. Mark resolved items as checked (`- [x]`). Unchecked items will be carried forward by tomorrow's daily creation.

### B3. Staleness Check

1. Read `.claude/harness-artifacts-index.md`. If the file does not exist, skip staleness checks entirely.
2. For each artifact in the index that has a **Staleness** field defined:
   - Read the artifact file (if it exists)
   - Evaluate the staleness condition specified in the index (e.g., count of `-tbd-` fields, days since `last_updated`, open items without status change)
   - If the condition is met, append an action item to today's Action Items: `- [ ] \`staleness\` Review {artifact name} — {reason}`
3. Artifacts without a **Staleness** field in the index are skipped silently.

### B4. Project Status Update

Re-derive project status (RAG) using the derivation rules in Section E. Compare to this morning's assessment. If it changed, update the frontmatter `project_status` field and append a Key Event noting the shift with rationale.

### B5. Priority Check

Re-derive current priority using the derivation rules in Section F. If it shifted during the day, append a Key Event noting the change with rationale (what was the priority before, what triggered the change).

### B6. Lessons Capture

Silently trigger the `project-lessons` skill — it reviews today's Key Events, Audit Log, and session summaries for generalizable insights and writes any lessons autonomously. If the `project-lessons` skill files do not exist yet, skip silently.

### B7. Mark Closed

Set frontmatter `status: closed` and update `last_updated` to today's date.

---

## C. Query Mode

1. Determine the date range from the PM's question (e.g., "this week" = Monday through today, "since Monday" = that Monday through today, "last 3 days" = 3 days back through today).
2. Read all daily files in `project/daily/` that fall within the range.
3. Synthesize an answer based on what the PM asked:
   - "What happened?" → summarize Key Events across the range
   - "Show open action items" → collect all unchecked items from the most recent daily (since carry-forward consolidates them)
   - "What decisions were made?" → scan Key Events and Audit Log entries for decision signals
   - General question → read the relevant sections and provide a targeted answer
4. Present the synthesized answer. Follow up if the PM asks more.

---

## D. Creation (used by CLAUDE.md session startup)

> This section is referenced by the CLAUDE.md session startup checklist, not by the `/project-daily` command directly. It is included here so all daily logic lives in one place.

1. Determine today's date and day of week.
2. Check if `project/daily/` directory exists. If not, create it.
3. Read the most recent daily file in `project/daily/` (sort by filename descending to find it).
4. **Carry forward action items**: From the previous daily, collect all unchecked action items (`- [ ]` entries). For each:
   - Change the label to `carry-forward`
   - Preserve the original source reference
   - Add to today's Action Items section
   - If no previous daily exists, the Action Items section starts empty.
5. **Derive project status**: Follow Section E to derive the RAG status.
6. **Derive current priority**: Follow Section F to derive the priority.
7. Create today's daily at `project/daily/project-daily-YYYY-MM-DD.md` using the template from `.claude/skills/project-daily/TEMPLATE.md`. Fill in:
   - Frontmatter: `status: open`, `last_updated: {today}`, `last_updated_by: auto — session startup`, `project_status: {derived}`
   - Header: today's date and day of week
   - Project Status: derived RAG with rationale
   - Current Priority: derived priority statement
   - Action Items: carried-forward items (or empty)
   - Key Events: empty
   - Audit Log: empty
8. **Friday nudge**: If today is Friday, add an action item: `- [ ] \`task\` **PM**: Generate & review project-weekly today — /project-weekly`

### Closing a previous unclosed daily

If the most recent daily has `status: open` (it was never closed), run the Close Mode (Section B) on that daily before creating today's daily. Use whatever is already recorded in that daily's Key Events and Audit Log for the session summary — it will be less rich than an in-session close, but functional.

---

## E. Project Status Derivation (RAG)

Derive the status primarily from **milestone/deadline adherence** and **stakeholder sentiment**:

**Green**: Project is on track with `product-scope` milestones and deadlines (across all active phases). Aggregated stakeholder sentiment is stable or positive. No significant delivery risks.

**Amber**: One or more of:
- Milestone or deadline at risk of slipping
- Stakeholder sentiment trending toward Skeptic
- Significant event detected (e.g., budget overrun signals, key team member departure, major scope change under discussion)

**Red**: One or more of:
- Milestone or deadline missed or will certainly be missed
- Stakeholder sentiment at Blocker
- Critical delivery disruption (e.g., project strongly over budget, team disruption, key dependency failure)

**What to read for derivation**:
- `product-scope` files in `product/solution-space/product-scope-*.md` — milestones, feature status, scope completion %. If no scope files exist yet, this input is unavailable — skip it.
- `project/management/project-stakeholders.md` — aggregated sentiment. If file does not exist, skip.
- Recent dailies' Key Events and Audit Log — significant events from meetings, documents, other skills
- Recent dailies — trend (improving or degrading?)

**What does NOT impact status**: Action item counts, staleness check results, and blocker counts are operational hygiene — they do not directly drive the RAG indicator.

**First day of project (no prior data)**: Default to Green with rationale "Project initiated."

Always present the derived status to the PM for confirmation. If PM overrides, record the override rationale in the Project Status section.

---

## F. Current Priority Derivation

Derive a single statement describing the most important focus right now. Sources:

1. `product-scope` files (`product/solution-space/product-scope-*.md`) — current phase, nearest milestone/deadline, feature completion %. This is the primary source when it exists. If no scope files exist yet, skip.
2. `project/management/project-assumptions.md` — recent decided assumptions that shift focus. If file does not exist, skip.
3. Recent meeting notes in `meetings/` — explicitly stated priorities from client or team.
4. Previous daily's priority — maintain continuity unless something changed.

When the priority changes from the previous daily, note the shift in Key Events with rationale: what triggered the change and what the priority was before.

**First day of project**: Default to "Complete project setup — upload documents, enrich client overview."

Always present the derived priority to the PM for confirmation. If PM overrides, record the override.

---

## G. Receiving Data from Other Skills

> These formats are used by other skills when they write to the daily. They are documented here as the canonical reference.

### Audit Entries

Other skills append audit entries to today's Audit Log section:

- Routing-triggered changes: `[AUTO] {artifact-name} — {what changed} from {source} ({YYYY-MM-DD})`
- PM-initiated changes: `[MANUAL] {artifact-name} updated via /{command} — {what changed} ({YYYY-MM-DD})`

Each entry is one line. If today's daily does not exist when a skill needs to write an audit entry, create it first using Section D (fallback creation).

### Action Items

Other skills append action items to today's Action Items section after PM confirms routing:

```
- [ ] `{label}` **{Owner}**: {Task} — due {deadline if mentioned} — from {source}
```

- Labels are dynamic, assigned by the routing skill based on the nature and source of the item. Common labels: `meeting`, `task`, `focus`, `open-question`, `blocker`, `follow-up`, `review`. New labels can emerge naturally.
- If no owner is specified, default to PM.
- The `— due {deadline}` part is included only when a deadline is mentioned.
- The `— from {source}` part references the meeting or document that surfaced the item.

### Session Summaries

Written to Key Events at commit time (triggered by CLAUDE.md instruction, not by this skill). Format: a brief narrative (2-5 sentences) capturing what was worked on, what decisions were made, any notable context. This is not a git log — it captures the *why* and *so what*.

---

## Rules

- **Append-only during the day**: Existing entries in Key Events and Audit Log are never modified or deleted. Only new entries are added. Exception: action items can be marked as checked (`- [x]`).
- **Conciseness**: Session summaries are 2-5 sentences. Audit entries are one line each. If a day has unusually high activity, keep entries brief.
- **Action item accuracy**: Action items are the most critical section. Never leave stale items unchecked, never lose carry-forwards, never duplicate items.
- **Resolved items stay put**: When an action item is resolved, mark it checked in the daily where it was resolved. It does not carry forward. The check mark stays in that daily permanently.
- **Multiple sessions in one day**: Each session appends to the same daily. Carry-forward only happens at daily creation, not between sessions.
- **`-tbd-` over fabrication**: Unknown fields are always `-tbd-`, never guessed.
- **Directory creation**: If `project/daily/` does not exist, create it automatically.
