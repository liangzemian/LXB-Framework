# Task Export and Import

Task export and import are used to move a **task configuration plus its task route** between devices. It is not just a list of tap coordinates. The exported file keeps task information, route steps, and necessary execution preferences.

## When to export

Export is useful when:

- You have tuned a scheduled task on one device and want to use it on another.
- You want to back up a notification-triggered task.
- You want to share a task with someone else, and let them adapt it locally after import.

Export is not suitable when:

- The task has not been proven to work.
- The task strongly depends on local account state, time, location, or temporary UI state.
- The task performs high-risk actions such as payment, ordering, or sending messages without being tested on the target device.

## Export

The frontend button is **Export Portable Task**. It appears inside an already saved task's configuration page:

- Scheduled task: open a saved scheduled task configuration page, then tap **Export Portable Task**.
- Notification-triggered task: open a saved notification trigger configuration page, then tap **Export Portable Task**.

The export button is not shown while creating a new task. Submit or save the task first.

The exported file is saved to:

```text
Downloads/LXB/Tasks/lxb-task-portable-<timestamp>.json
```

The file includes:

- Task name and description.
- Package / package-match information needed by the task.
- User playbook / action playbook.
- Route settings.
- Saved task route.
- Route behavior such as **finish after replay**.

## What is not exported

To avoid carrying private local runtime state to another device, export does not include:

- The original task's local identity.
- Historical run records.
- Historical run times.
- The concrete schedule time.
- Local active-time settings for notification rules.

After import, review time, enabled state, and other local settings on the new device.

## Import

The import entry is next to the **Automation** header on the Tasks page. The frontend button is **Import**. Select an exported JSON file and AutoLXB will identify whether it is a scheduled task or notification-triggered task.

After import:

- A new local task is created.
- The new task is disabled by default, so it will not run immediately.
- The route is bound to the new task.
- For scheduled tasks, review run time, repeat mode, and package.
- For notification-triggered tasks, review package match, title/body matching, LLM condition, and trigger interval.

## Cross-device route adaptation

Some route steps can be reused directly, such as buttons with clear text or descriptions. Other steps may have been coordinate-backed on the source device. These steps need local adaptation on the new device.

On the first run after import, AutoLXB tries to use semantic descriptions and the current screen to find the target UI element again, then saves the adapted result locally.

!!! warning "Always test after import"
    Different devices may have different screen sizes, font scales, app versions, and login states. After importing a task, run a low-risk manual test before enabling scheduled or notification-triggered execution.