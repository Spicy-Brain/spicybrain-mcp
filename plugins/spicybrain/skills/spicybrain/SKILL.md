---
name: spicybrain
description: Manage the user's SpicyBrain projects, tasks, and reminders. Use when the user asks to plan work, capture or review tasks, create or complete reminders, organise work into projects, or inspect their SpicyBrain account.
---

# SpicyBrain

Use the SpicyBrain MCP tools to manage information for the authenticated account.

## Working principles

- Treat every tool response as scoped to the authenticated SpicyBrain user.
- Use list tools to resolve names to identifiers instead of guessing identifiers.
- Preserve the user's wording when creating project, task, and reminder names unless they ask for editing help.
- Ask a focused question when the intended project, parent task, date, timezone, recurrence, or notification channel is materially ambiguous.
- Summarise successful mutations concisely, including the created or completed item's name.
- Never claim that an unsupported edit, delete, or restore operation is available.

## Projects and tasks

- Call `list-projects` before `create-task` when the user identifies a project by name rather than id.
- Omit `project_id` only when the user genuinely wants an unfiled task.
- For a subtask, resolve the parent task first. The server inherits its project from the parent.
- Do not choose a board stage unless the user specifies one or the relevant stage is already known. The server supplies the project's default stage when omitted.
- Before completing a task, confirm the target when multiple tasks have similar names. Completing a parent also completes its subtasks.

## Reminders

- Interpret reminder dates in the user's stated timezone. Ask for a timezone when a relative or local time could otherwise resolve incorrectly.
- Use ISO 8601 date/time values when calling reminder tools.
- Distinguish the notification repeat interval from recurrence: `repeat_interval` controls re-notification while one reminder window is open; recurrence creates future occurrences.
- Only attach a reminder to another entity after resolving both its type and identifier.
- Completing a recurring reminder completes its current occurrence and may generate the next one; it does not stop the series.

## Read before write

When a request changes existing data, first list or search narrowly enough to identify the intended record. A direct creation request with all required details does not need an unnecessary preliminary list call.
