# todo — Skill Logic

> A fast, priority-ranked view of open action items, followed by an interactive triage pass that keeps the top of the list honest — still valid? still needs doing?

---

## When This Skill Runs

Runs when the PM invokes `/todo`.

---

## Step 1: Load Open Items

Read the most recent daily at `project/daily/project-daily-YYYY-MM-DD.md` (sort by filename descending). Carry-forward already consolidates all unresolved items from prior days into the latest daily's Action Items section — this is the single source of truth, no need to read older dailies.

Parse every unchecked item (`- [ ]`). Keep each item's full text (label tags, owner, task, due date, source) intact — never compress or drop content while parsing.

If no daily exists, tell the PM there's nothing to review and stop.

## Step 1.5: Filter to the PM's Own Items

This is the PM's personal to-do list, not a team tracker — filter down to items that are actually the PM's before ranking:

- **Keep** an item if its owner field (the bolded name(s) before the colon) contains the PM's name from `CLAUDE.md` (e.g. "Marek Pillár"), alone or jointly with others (e.g. "Marek Pillár / Jindřich Tůma"), or the literal owner `PM`.
- **Keep** an item with no bolded owner at all (e.g. system-generated `staleness` checks) — these are implicitly the PM's.
- **Drop** everything else — items owned solely by colleagues, clients, or "Unassigned" — from this skill's view entirely. They still exist in the daily (other skills/PM tracking still rely on them) and, if archived per the PM's action-items-archive cleanup, in `project/management/action-items-archive.md` — this skill just doesn't surface them.

Do this filtering before ranking and before counting "how many more remain" in Step 7.

## Step 2: Rank by Priority

Derive a priority tier from each item's label tags:

1. `highest-prio`
2. `mid-prio`
3. *(no priority label present — "normal")*
4. `low-prio`

Sort all open items into this order. Within a tier, preserve the existing list order (already roughly chronological from carry-forward). Ignore non-priority labels (`carry-forward`, `staleness`, `blocker`, `follow-up`, etc.) for ranking — they're metadata, not priority.

## Step 3: Show the Full List

Present the complete priority-sorted list to the PM — topmost priority first, lowest last. Use a compact format: owner, task, tier. This is a read-only overview; nothing is written yet.

## Step 4: Interactive Triage (Top 10)

Immediately after showing the list, walk through the **top 10 items** (by the same priority order) in an interactive Q&A using `AskUserQuestion`.

Each item gets exactly one question with exactly 3 options, always offered in this order:
1. **"Skip"** — leave the item exactly as-is, no change. Default choice when nothing about the item needs correcting.
2. **"Done"** — the task was actually carried out.
3. **"No longer valid — remove"** — stale, superseded, or irrelevant; distinct from "Done" (this was never actually completed, it just doesn't need doing).

Use the item's owner + task text (truncated if needed) as the question header/context so the PM can tell items apart at a glance. Batch up to 4 items' questions per `AskUserQuestion` call.

## Step 5: Apply Answers

Process all 10 items' answers together once every question has been asked (don't write mid-batch):

- **"Skip"** → no change. The item is left exactly as it was.
- **"Done"** → mark the item `- [x]` in the daily immediately, appending `— marked done via /todo review ({date})` to its text. It does not carry forward.
- **"No longer valid"** → mark the item `- [x]` in the daily immediately, appending `— marked no-longer-valid via /todo review ({date})` to its text. It does not carry forward.

Write all changes to the daily file (the most recent one loaded in Step 1) directly — this is a PM-invoked, manual review action, not autonomous routing, so no separate confirmation step is needed before writing. If that daily's `status` is already `closed`, still write directly to it (editing a closed daily for an explicit PM correction is normal — see the project-daily skill's own Review Mode precedent for direct PM-driven edits).

## Step 6: Audit Entry

Append one line to the daily's Audit Log:

```
[MANUAL] project-daily — /todo review: {D} marked done, {K} marked no-longer-valid, {S} skipped ({date})
```

## Step 7: Summary

Report back concisely: how many were marked done, marked no-longer-valid, or skipped, and remind the PM how many more items remain below the top 10 if they want to keep going (they can just re-run `/todo`).

---

## Rules

- **Never touch items outside the top 10** during the Q&A — the full list in Step 3 is read-only context, not something to bulk-edit.
- **Owner filter is a display filter, not a data change** — items excluded in Step 1.5 are never edited, checked off, or removed from the daily by this skill.
- **Preserve item text exactly** apart from the specific tag/checkbox being changed — don't rewrite or summarize an item's task description.
- **Don't invent priority tiers** — only use `highest-prio` / `mid-prio` / `low-prio` / untagged("normal"), matching the labels already in use across dailies.
- **This is a manual action** — audit entries use `[MANUAL] ... /todo` per the harness convention for PM-triggered skill sessions, not `[AUTO]`.
