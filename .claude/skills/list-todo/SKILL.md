# list-todo — Skill Logic

> A read-only, visually formatted view of every open action item, grouped by priority. No writes, no publishing — shown directly in the conversation only.

---

## When This Skill Runs

Runs when the PM invokes `/list-todo`, or says anything with the same intent in natural language — e.g. "show me priorities", "show me to do list", "list me priorities", "what's on my plate", "show me my todos". Recognize the intent, not just the exact phrase.

---

## Step 1: Load Open Items

Read the most recent daily at `project/daily/project-daily-YYYY-MM-DD.md` (sort by filename descending). Carry-forward already consolidates all unresolved items from prior days into the latest daily's Action Items section.

Parse every unchecked item (`- [ ]`). Extract owner (the bolded name) and task text; keep the due date and source reference available but don't need to display all of it — this is a scan view, not the full record.

If no daily exists, tell the PM there's nothing to show and stop.

## Step 2: Rank by Priority

Same tiers as the `todo` skill:

1. `highest-prio`
2. `mid-prio`
3. *(no priority label present — "normal")*
4. `low-prio`

Sort into this order; preserve existing order within a tier.

## Step 3: Render Privately in Chat

Present the full list **directly in the conversation reply** — never as a published Artifact, never written to a file, never posted anywhere else. This is what "privately, visible only to me" means for this skill: it lives in this response and nowhere else.

Format for visual clarity:

- One emoji-headed section per tier that has items — skip empty tiers entirely:
  - 🔴 **Highest Priority**
  - 🟠 **Mid Priority**
  - ⚪ **Normal**
  - 🔵 **Low Priority**
- Each item as a dash bullet: `- **{Owner}** — {task, trimmed to one line}`
- Keep task text to roughly one line (~100 chars); this is a scan view, not the verbose record — full detail is always in the daily itself if needed.
- A one-line total count at the top (e.g. "**178 open items**") before the sections.

## Rules

- **Read-only, always** — this skill never checks off items, never reprioritizes, never edits the daily. For that, use `/todo`.
- **Never publish** — no Artifact, no file write, no external post. Output goes only into the chat response.
- **Full list, not a subset** — unlike `/todo`'s top-10 triage cap, `list-todo` always shows everything open.
- **Natural-language triggering** — this skill should fire on clear intent ("show me my priorities/todos/to-do list") without requiring the exact `/list-todo` command.
