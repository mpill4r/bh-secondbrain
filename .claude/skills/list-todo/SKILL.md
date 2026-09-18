# list-todo — Skill Logic

> A read-only, visually formatted view of every open action item **owned by the PM**, grouped by priority. No writes, no publishing — shown directly in the conversation only.

---

## When This Skill Runs

Runs when the PM invokes `/list-todo`, or says anything with the same intent in natural language — e.g. "show me priorities", "show me to do list", "list me priorities", "what's on my plate", "show me my todos". Recognize the intent, not just the exact phrase.

---

## Step 1: Load Open Items

Read the most recent daily at `project/daily/project-daily-YYYY-MM-DD.md` (sort by filename descending). Carry-forward already consolidates all unresolved items from prior days into the latest daily's Action Items section.

Parse every unchecked item (`- [ ]`). Extract owner (the bolded name) and task text; keep the due date and source reference available but don't need to display all of it — this is a scan view, not the full record.

If no daily exists, tell the PM there's nothing to show and stop.

## Step 1.5: Filter to the PM's Own Items

This is the PM's personal to-do list, not a team tracker — filter down to items that are actually the PM's before ranking:

- **Keep** an item if its owner field (the bolded name(s) before the colon) contains the PM's name from `CLAUDE.md` (e.g. "Marek Pillár"), alone or jointly with others (e.g. "Marek Pillár / Jindřich Tůma"), or the literal owner `PM`.
- **Keep** an item with no bolded owner at all (e.g. system-generated `staleness` checks) — these are implicitly the PM's.
- **Drop** everything else — items owned solely by colleagues, clients, or "Unassigned". They still exist in the daily for PM tracking/audit purposes; this skill just doesn't surface them.

The total count shown in Step 3 is the filtered count (the PM's own open items), not the daily's total open-item count.

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
- A one-line total count at the top (e.g. "**31 open items**") before the sections — this is the PM's own filtered count, per Step 1.5.

## Rules

- **Read-only, always** — this skill never checks off items, never reprioritizes, never edits the daily. For that, use `/todo`.
- **Never publish** — no Artifact, no file write, no external post. Output goes only into the chat response.
- **Full list, not a subset — but only of the PM's own items** — unlike `/todo`'s top-10 triage cap, `list-todo` always shows everything open that belongs to the PM. It is not a subset of the PM's own items, but it is a subset of the daily's full item list by design (see Step 1.5) — never present it as "every open item in the project."
- **Natural-language triggering** — this skill should fire on clear intent ("show me my priorities/todos/to-do list") without requiring the exact `/list-todo` command.
