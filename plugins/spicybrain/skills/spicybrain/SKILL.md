---
name: spicybrain
description: Manage the user's SpicyBrain reminders, tasks, subtasks, projects, board stages and Today list with the SpicyBrain MCP tools. Use when the user mentions SpicyBrain or asks to add, find, move, reschedule or finish reminders, tasks or projects, or what to focus on today.
---

# SpicyBrain

SpicyBrain is an ADHD-friendly app for life and home admin. Every tool acts only on the signed-in user's account.

## Tone

- Keep replies short. Confirm what changed in one line, then offer one next step at most.
- For "what's next?", surface one to three items, not the whole list.
- Keep the user's own wording for names.

## Find before you act

- Never guess ids. Resolve names with `list-projects`, `list-tasks` (`search`, `project_id`, `status`) and `list-reminders` (`search`).
- If several records match, ask which one. If none match, say so; don't create a duplicate unless asked.
- Read before you write: check the current record (`list-tasks`, `show-reminder`) before changing or removing it.
- A clear create request needs no extra lookup, apart from resolving a named project or parent task.
- `list-tasks` and `list-reminders` return up to `limit` items (default 50, max 100). If `next_offset` is not null, call again with `offset` set to it. Stop once you have what you need.

## Projects, tasks and stages

- `list-projects` returns each project's board `stages` (`id`, `name`, `sort_order`) and outstanding task counts.
- A task has two separate positions:
  - List/tree: parent, project and order. Change with `reorder-task`. Subtasks sit under a parent task.
  - Board: the stage (column) it is in. Change with `move-task-to-stage`; omit or null `stage_id` for the unstaged "Tasks" column.
- `update-task` is partial. Omitted fields keep their values. Null `description` clears it, null `project_id` unfiles the task, null `parent_id` makes it top-level.
- `focus-task` and `unfocus-task` manage the Today list. `list-tasks` with `status: today` shows it.
- `reopen-task` undoes a completion. `delete-task` is a soft delete that `restore-task` can undo.
- Stages: `create-stage`, `update-stage`, `reorder-stage`, `delete-stage`.

## Reminders

- Call `list-reminder-options` when unsure about channels, recurrence types, calendar day strategies, the account timezone or what a reminder can attach to.
- Dates are ISO 8601. Use the user's timezone. If it is unclear and matters, use the account timezone and say so.
- Recurring reminders keep the same local clock time, even across daylight saving changes.
- `repeat_interval` is minutes between re-notifications while a reminder is open (minimum 5). It is not how often the reminder recurs.
- Monthly and yearly recurrence need `calendar_day_strategy`: `fixed_day_of_month` or `end_of_month`.
- `recur_finish` is an exclusive YYYY-MM-DD stop date in the series timezone. To keep an occurrence on 31 March, pass 1 April.
- `update-reminder` needs `reminder_id` and `update_scope`. Omitted fields keep their values.
  - `occurrence`: changes only this occurrence.
  - `series`: changes this and future occurrences. Required for recurrence pattern changes.
- `move-reminder-to-tomorrow` keeps the same clock time, one day later.

### Ending a reminder

- Done for now: `complete-reminder`. A recurring reminder carries on; tell the user when the next one is due.
- Never again: `stop-reminder-series` completes it and ends the whole series.
- Should not exist: `delete-reminder`. There is no restore tool.
- "Done" on a recurring reminder means `complete-reminder`, not stopping the series.

## Confirm before destructive tools

Name the item and get a clear yes before calling:

- `complete-task`: also completes its subtasks and permanently stops recurrence on attached reminders. Reopening does not restart them.
- `stop-reminder-series`
- `delete-reminder`, `delete-task`, `delete-project`, `delete-stage`

One yes covers one action, unless the user listed exactly what to remove.

## Errors

Tool errors are plain messages, such as "No task with id 42 was found." Re-check with a list tool, then explain in one line. Don't repeat the same failing call.
