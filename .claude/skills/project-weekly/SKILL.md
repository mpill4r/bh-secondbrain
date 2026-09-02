# project-weekly — Skill Logic

> The weekly status summary is the primary visibility tool for internal management. It synthesizes the week's daily logs into a management-grade readout: what happened, what's at risk, what's next. A separate client-safe variant filters sensitivity for external stakeholders.

---

## When This Skill Runs

This skill runs in one of three contexts:

- **PM runs `/project-weekly`** → run **Internal Weekly Mode** (Section A)
- **PM runs `/project-weekly-client`** → run **Client Weekly Mode** (Section B)
- **Auto-trigger fires (RemoteTrigger, Friday 4pm)** → run **Auto-Generation Mode** (Section C)

---

## A. Internal Weekly Mode

### A1. Determine Week

Calculate the current ISO week number (`YYYY-WNN`). The target file is `project/weekly/project-weekly-YYYY-WNN.md`.

### A2. Check for Existing Weekly

If the target file already exists:
- Read it and present it to the PM for review and update.
- The PM can adjust specific sections, request regeneration with guidance, or confirm as-is.
- After PM confirms, update `status: confirmed` in frontmatter, update `last_updated` to today, update `last_updated_by: manual — /project-weekly`.
- Log audit entry to today's `project-daily` (see Section D). If today's daily does not exist, create it first using the project-daily template.
- Stop here — do not regenerate.

If the target file does not exist, proceed to A3.

### A3. Load Context

Read the following sources:

1. **All dailies for the current week** — read every `project-daily-YYYY-MM-DD.md` file from Monday through today (or through Friday if running on Friday). These are the sole data source. If no dailies exist for the current week, inform the PM: "No dailies exist for this week — cannot generate a meaningful weekly. Create dailies first." Stop here.
2. **`product-scope`** — read all `product/solution-space/product-scope-*.md` files for timeline, milestones, and phase context. If none exist, skip silently.
3. Read `.claude/harness-artifacts-index.md`. If it exists, load any additional artifacts whose "Read for context when" conditions match weekly status generation. If the index does not exist, skip silently.

### A4. Extract from Dailies

From the loaded dailies, extract:
- Project status (RAG) entries and any changes throughout the week
- Key Events (session summaries, significant events)
- Audit Log entries (decisions, artifact changes)
- Action items — opened, resolved (checked), and still open (unchecked)
- Current priority (from most recent daily)

### A5. Generate the Weekly

Generate the internal weekly using the TEMPLATE.md structure. Apply these synthesis rules:

- **Project Status**: Use the most recent daily's RAG status. If the status changed during the week, add a trend note: "Status moved from {previous} to {current} on {day} — {reason}."
- **Week Summary**: Write a 3-5 sentence narrative synthesis — the arc of the week. What was the state on Monday, what shifted, where are we now. This is NOT a concatenation of daily summaries.
- **Key Decisions**: Extract decisions from dailies' audit logs and key events. Reference assumption IDs from `project-assumptions` where available. If decisions were made but not yet formally logged as assumptions, flag this: "Not yet logged in project-assumptions."
- **Milestones & Progress**: What was achieved, what moved forward. Reference `product-scope` timeline and milestones where available.
- **Risks & Issues**: Be specific and transparent. Never use vague labels like "timeline risk." Always include context and impact: "Phase 1 scope finalization is 2 days behind because client stakeholder review took longer than expected — mitigation: parallel-tracking the design work."
- **Action Items**: All unchecked items from the most recent daily (Friday's if it exists, otherwise latest). Group by owner. Highlight blockers and overdue items (past deadline).
- **Next Week**: Upcoming deadlines from `product-scope`, open action items, key meetings or milestones ahead.
- **Team Notes**: Capacity changes, availability, team dynamics from the week's dailies. If nothing notable, write "No changes."

### A6. Present for Review

Present the generated weekly to the PM in conversation. The PM can:
- **Confirm** → proceed to A7
- **Adjust specific sections** → apply the PM's changes, then present again for confirmation
- **Request regeneration with guidance** → regenerate with the PM's direction, then present again

### A7. Save and Log

1. If the directory `project/weekly/` does not exist, create it.
2. Save the weekly to `project/weekly/project-weekly-YYYY-WNN.md`.
3. Set frontmatter: `status: confirmed`, `last_updated: {today}`, `last_updated_by: manual — /project-weekly`, `week: YYYY-WNN`, `project_status: {RAG}`.
4. Log audit entry to today's `project-daily` (see Section D). If today's daily does not exist, create it first using the project-daily template.
5. Update `last_updated` and `last_updated_by` on the saved weekly file frontmatter.

---

## B. Client Weekly Mode

### B1. Check Internal Weekly Exists

Calculate the current ISO week number (`YYYY-WNN`). Read `project/weekly/project-weekly-YYYY-WNN.md`.

If it does not exist, inform the PM: "No internal weekly exists for this week. Run `/project-weekly` first to generate the internal version." Stop here.

### B2. Generate Client Version

Read the internal weekly. Generate the client-safe version by applying these sensitivity filters:

- **Week Summary**: Reframe to focus on what was delivered and achieved — progress-oriented, highlighting wins and momentum. Remove internal process commentary.
- **Milestones & Progress**: This is the headline section. Emphasize completions, forward movement, demos or deliverables ready for review.
- **Decisions**: Include only client-facing decisions. Omit internal-only decisions (tooling, process, team allocation, internal budget).
- **Risks & Issues**: Reframe constructively — "We identified X and are addressing it with Y." Omit internal team dynamics, budget concerns, and internal process issues.
- **Action Items for Client**: Replace the internal Action Items section. Include only items requiring client action — pending approvals, feedback needed, decisions the client needs to make. Clear owners and deadlines.
- **Team Notes**: Omit entirely unless there is a client-relevant capacity note (e.g., "key team member on leave next week — coverage arranged").
- **Language**: Professional, confident, progress-oriented. The project is moving and the team is delivering.

Use this structure for the client weekly:

```
---
status: draft
last_updated: {YYYY-MM-DD}
last_updated_by: manual — /project-weekly-client
week: {YYYY-WNN}
---

# Weekly Status — {YYYY-WNN} ({Mon DD} – {Fri DD Mon YYYY})

## Week Summary

{Progress-oriented summary}

## Milestones & Progress

{Headline section — completions, forward movement, deliverables}

## Decisions

{Client-facing decisions only}

## Risks & Issues

{Constructive framing — problem + mitigation}

## Action Items for Client

{Items requiring client action — approvals, feedback, decisions. Clear owners and deadlines.}
```

### B3. Present for Review

Present the client version to the PM. The PM can adjust tone, remove mentions, add context, or confirm.

### B4. Save and Log

1. Save to `project/weekly/project-weekly-YYYY-WNN-client.md`.
2. Set frontmatter: `status: confirmed`, `last_updated: {today}`, `last_updated_by: manual — /project-weekly-client`, `week: YYYY-WNN`.
3. Log audit entry to today's `project-daily` (see Section D). If today's daily does not exist, create it first using the project-daily template.
4. Inform the PM: "Client weekly saved. It's not auto-posted anywhere — share it however you prefer (email, Slack, client portal)."

---

## C. Auto-Generation Mode

This mode runs when a RemoteTrigger fires (Friday at 4pm) or when Claude detects it should auto-generate.

### C1. Check for Existing Weekly

Calculate the current ISO week number (`YYYY-WNN`). Check for `project/weekly/project-weekly-YYYY-WNN.md`.

- If the file exists with `status: confirmed` → **skip entirely**. The PM already reviewed and confirmed. No duplicate.
- If the file exists with `status: draft` → **skip entirely**. The PM started but hasn't confirmed — do not override PM's in-progress review.
- If no file exists → proceed to C2.

### C2. Generate

Follow the same steps as A3 (Load Context), A4 (Extract from Dailies), and A5 (Generate the Weekly).

### C3. Save

1. If the directory `project/weekly/` does not exist, create it.
2. Save the weekly to `project/weekly/project-weekly-YYYY-WNN.md`.
3. Set frontmatter: `status: confirmed`, `generated: auto`, `last_updated: {today}`, `last_updated_by: auto — project-weekly`, `week: YYYY-WNN`, `project_status: {RAG}`.
4. Log audit entry to today's `project-daily` (see Section D). If today's daily does not exist, create it first using the project-daily template.

Auto-generated weeklies are considered confirmed since the PM had the opportunity to generate manually earlier in the day.

---

## D. Audit Entry Format

Every write to a weekly file is logged as an audit entry to today's `project-daily` Audit Log section:

- Manual generation: `[MANUAL] project-weekly — generated and confirmed internal weekly {YYYY-WNN} ({date})`
- Manual update/review: `[MANUAL] project-weekly — updated internal weekly {YYYY-WNN} ({date})`
- Auto-generation: `[AUTO] project-weekly — auto-generated internal weekly {YYYY-WNN} ({date})`
- Client version: `[MANUAL] project-weekly-client — generated client weekly {YYYY-WNN} ({date})`

---

## E. Friday Nudge

This section is implemented by `project-daily`, not by this skill. When `project-daily` creates or updates a daily on a Friday, it adds the following action item:

`- [ ] \`task\` **PM**: Generate & review project-weekly today — /project-weekly`

This is documented here for completeness — the instruction lives in the project-daily SKILL.md.

---

## Rules

1. **No duplicate weeklies** — only one internal weekly per week number. All paths (manual, auto) work with the existing file if one exists.
2. **Client version is always PM-triggered and PM-confirmed** — never auto-generated, never auto-posted. The PM decides how to share it.
3. **Dailies are the sole data source** — the weekly synthesizes dailies. It does not read meetings, documents, or other artifacts directly (except `product-scope` for timeline context and artifacts loaded via index conditions).
4. **Narrative synthesis, not concatenation** — the Week Summary captures the arc of the week, not a day-by-day list.
5. **Risks must be specific and transparent** — no vague labels. Always include context, impact, and mitigation where available. The internal version must be honest — sugarcoating defeats the purpose.
6. **Client version must be professional and constructive** — problems are acknowledged with mitigation plans, not hidden. Language is confident and progress-oriented.
7. **Readable in under 2 minutes** — lead with status, then details. Management doesn't have time for lengthy reports.
8. **Reads like a thoughtful PM wrote it** — narrative flow, not bullet-point dumps. Natural language, not auto-generated feel.
9. **Preserve existing content** — when updating an existing weekly (A2 path), only modify the sections the PM requests. Do not regenerate untouched sections.
10. **Mid-week generation is valid** — if the PM runs `/project-weekly` before Friday, generate from available dailies (Mon through today). The weekly can be updated later if re-run.
11. **Short week handling** — if only 1-2 days of dailies exist (holidays, project start mid-week), generate a proportionally shorter weekly. Do not fabricate content for missing days.
12. **RemoteTrigger not required** — the Friday nudge and manual generation work without a RemoteTrigger being set up. The auto-trigger is an enhancement.
