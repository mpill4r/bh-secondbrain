# project-lessons — Skill Logic

> Organizational knowledge capture — generalizable lessons learned that help other PMs, teams, or future projects. The key differentiator: this skill operates autonomously. Lessons are captured silently during meeting processing, document processing, and daily close — no PM confirmation required. PM can review, edit, or remove at any time.

---

## When This Skill Runs

This skill runs in four contexts:
- **PM invokes `/project-lessons`** → Interactive Mode (Section A)
- **Triggered by `project-meeting` after routing completes** → Autonomous Capture from Meeting (Section B)
- **Triggered by `project-document` after routing completes** → Autonomous Capture from Document (Section B2)
- **Triggered by `project-daily` close step** → Autonomous Capture from Daily (Section C)

---

## A. Interactive Mode

1. **Load context**: Read `project/management/project-lessons.md` (full file). Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose "Read for context when" conditions match the current task. If any file does not exist, skip silently.
2. **Present summary**: "You have X lessons captured. What would you like to do — review, add, search, or edit?"
3. Handle PM requests:

### Review / Query

PM can query by category, keyword, or date range:
- "Show me all harness lessons"
- "Anything about client communication?"
- "What did we capture this week?"

Read the file and synthesize a targeted answer.

### Manual Add

When PM provides a lesson directly:
1. **Check for duplicates**: Read existing entries. If a similar lesson already exists, surface it: "LL-008 covers something similar — update that one or create a new entry?" If updating, append new context to the existing entry.
2. **Generalization step**: If the PM provides a project-specific observation, propose a generalized version. The Lesson field must be understandable without project context. If the lesson can't be generalized beyond this specific client, capture it with a `client-specific` category — it's still valuable if the team works with this client again.
3. Assign the next sequential LL-ID (check highest existing ID, increment).
4. Structure the entry: ID, created date, category (assign based on context — categories are open-ended, not a fixed set), source: "PM".
5. Present the draft for PM confirmation. Write after confirmation.
6. Log audit entry to `project-daily`: `[MANUAL] project-lessons — LL-{NNN} added ({date})`.

### Edit / Remove

PM can edit or remove any lesson. Lessons are not sacred — if one is too specific, wrong, or redundant, PM deletes or adjusts it.

---

## B. Autonomous Capture from Meeting

Triggered silently after `project-meeting` completes its routing review and writes all confirmed routes.

1. Read the full meeting note that was just processed.
2. Review: key discussion points, decisions, sentiment, action items — identify any generalizable insights.
3. **Apply the selectivity filter**: "Would another PM on the team benefit from knowing this?" If the answer is no, write nothing. Most meetings will produce no lessons. Never create empty entries or "no lessons found" messages.
4. For each candidate lesson:
   - **Generalization step**: Take the specific project event and derive a broadly applicable insight. "CTO responds faster on Slack DMs" → "For urgent stakeholder approvals, try direct messaging before email — faster response in time-sensitive situations."
   - Assign the next sequential LL-ID.
   - Set category based on context (open-ended — not a fixed set).
   - Set source to the meeting slug.
   - Write the Lesson field for someone with no project context. Write the Context field with the project-specific details.
   - Add cross-references to related artifacts (assumptions, other meetings) when applicable.
5. **Check for duplicates**: Read existing entries before writing. If a similar lesson already exists, append new context to the existing entry rather than creating a duplicate.
6. Write silently to `project/management/project-lessons.md` — no PM confirmation required.
7. Log audit entry to `project-daily`: `[AUTO] project-lessons — LL-{NNN} captured from {meeting-slug} ({date})`.
8. If `project-lessons.md` does not exist, create it using the template first.

**Very active meetings**: If many candidates emerge, select the top 2-3 most impactful. Never flood the file.

---

## B2. Autonomous Capture from Document

Triggered silently after `project-document` completes its routing review and writes all confirmed routes.

1. Read the full document summary that was just processed.
2. Review: key points, extracted decisions, open questions — identify any generalizable insights. Particularly valuable sources: retrospective summaries, post-mortem reports, workshop outputs (FigJam boards), strategy reviews, and lessons-learned documents from the client.
3. Same process as meeting capture (B.3–B.8): selectivity filter, generalization, duplicate check, silent write, audit entry.

---

## C. Autonomous Capture from Daily Close

Triggered during the `project-daily` close step, after session summary and action item review.

1. Read today's daily: Key Events, Audit Log, and session summaries.
2. Identify generalizable insights from the day's work.
3. **Avoid duplicates from same-day captures**: Check existing entries — if a lesson was already captured from a meeting or document processed earlier today, do not duplicate it.
4. Same process as meeting capture (B.3–B.8): selectivity filter, generalization, duplicate check, silent write, audit entry.

---

## D. Generalization Quality

The generalization step is the core value of this skill. Requirements:

- **The Lesson field must stand alone**: Someone reading "Always do a PoC before estimating third-party API integrations" should know what to do without knowing which API or project.
- **The Context field preserves specifics**: What actually happened. This gives the lesson credibility and helps future readers judge applicability.
- **Capture lessons about the harness itself**: Suboptimal harness behavior, routing failures, skill gaps, or unexpectedly good results are all valuable lessons for harness improvement.
- **Categories are open-ended**: The harness assigns based on context. Common categories include: `client-specific`, `harness`, `discovery-methodology`, `project-management`, `technology`, `design`, `domain-specific`, `team`, `commercial`. New categories emerge naturally.

---

## E. PM Notification

When autonomous capture writes lessons, the PM is notified at the next session start via the daily briefing: "{N} new lessons captured yesterday — review with `/project-lessons`." This is informational, not a confirmation gate.

---

## Rules

- **Selective over prolific**: Better to miss a lesson than to flood the file with marginal entries. Quality over quantity.
- **Generalization is non-negotiable**: A lesson that's just a specific event restated is not useful cross-project. The skill must abstract from the specific to the general.
- **Plain language**: No jargon, no project-internal references in the Lesson field (those go in Context).
- **Autonomous capture needs no PM confirmation**: This is by design. PM reviews and adjusts at their discretion.
- **Never duplicate**: Always check existing entries before writing — in ALL write paths (autonomous and manual). Append new context to existing entries when the lesson is already captured.
- **Contradicting lessons are OK**: If a new lesson contradicts an earlier one, keep both. The Context fields explain the different circumstances. PM can reconcile during review.
- **Client-specific fallback**: If a lesson can't be generalized beyond this specific client, capture it with `client-specific` category rather than discarding it.
- **Volume cap on daily close**: Same as meetings — if many candidates emerge from daily close, select the top 2-3 most impactful. Never flood the file.
- **Audit everything**: Log to `project-daily` after every write. If `project-daily` does not exist, create it first.
- **File creation fallback**: If `project-lessons.md` does not exist when needed, create it using the template first.
- **IDs are sequential**: LL-001, LL-002, etc. Never reused.
