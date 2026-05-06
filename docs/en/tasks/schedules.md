# Scheduled Tasks

Scheduled tasks run automatically at a configured time. Use them for daily check-ins, periodic information lookup, reminders, and other fixed-time or repeated workflows.

## Create a scheduled task

Entry: `Tasks -> Automation -> Schedules -> New`.

The create/edit page is organized into these sections:

1. **Basic info**: name, task description, and user playbook.
2. **Execution target**: date, time, repeat mode, and the app to open first.
3. **Execution preference**: route mode and screen recording.
4. **Save schedule**: save or submit the schedule.

## Field guide

Field names below follow the actual frontend labels.

| Frontend field | Meaning | Required | Example |
| --- | --- | --- | --- |
| Name (optional) | A readable name for the scheduled task. It can be empty. | No | Daily check-in |
| Task description (required) | What AutoLXB should do. Include target app, target page, and final action when possible. | Yes | Open the app and complete check-in. |
| User playbook (optional) | Extra execution guidance for the model, such as page order or button names. | No | Enter the home page, tap Check in, then confirm. |
| Run time | Preview of the currently selected run time. It is controlled by Pick Date and Pick Time. | Yes | 2026-05-06 11:00 |
| Pick Date | Opens the date picker. | Yes | 2026-05-06 |
| Pick Time | Opens the time picker, using 24-hour time. | Yes | 11:00 |
| Repeat | Selects Once, Daily, or Weekly. | Yes | Daily |
| Selected days | Appears only for Weekly repeat. Select at least one weekday. | Required for Weekly | Mon / Wed / Fri |
| Package (select from local snapshot) | Select the app that the task should open first. Pick one when possible to reduce app-resolution uncertainty. | No | Example App (`com.example.app`) |
| Task route mode | Shown as Off / On. When On, the task tries its saved route first. | Yes | On |
| Open task route editor | Appears only after the task has been saved once. Opens this exact task's route editor. | No | - |
| Export Portable Task | Appears only after the task has been saved once. Exports the task config and route. | No | - |
| Record task screen | Saves task recording to `Movies/lxb` for debugging. | Yes | On |

!!! note "Route editor and export are not shown while creating"
    The route editor and portable export buttons appear only after the task configuration has been saved once. Submit the task first, then reopen it to edit routes or export it.

## Task description vs user playbook

**Task description (required)** should describe the final goal:

```text
Open the coffee app and order a coconut latte.
```

**User playbook (optional)** should describe execution details:

```text
After entering the coffee app, tap Menu, search coconut latte, choose large hot drink, and continue. Close upsell popups if they appear.
```

## Tips

- Test the same description as a quick task before creating a schedule.
- For payment, ordering, or important messages, test with low-risk content first.
- If the path is stable, save a route and turn on **Task route mode**.
- Changing time or repeat mode does not invalidate the saved route.

## Imported schedules

Imported scheduled tasks are disabled by default. After import, review task description, package, run time, repeat mode, and route settings before enabling the task.