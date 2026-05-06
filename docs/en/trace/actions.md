# Action Execution Trace

Action execution trace confirms whether AutoLXB actually tapped, swiped, input text, waited, or pressed Back. A model saying "I will tap" does not guarantee the action succeeded; check execution trace.

## `exec_tap_start` / `exec_tap_done`

Tap started and finished.

```json
{
  "task_id": "task-20260506-001",
  "x": 540,
  "y": 1860,
  "ts": "2026-05-06T09:00:12.700+0800",
  "event": "exec_tap_start"
}
```

```json
{
  "task_id": "task-20260506-001",
  "x": 540,
  "y": 1860,
  "ts": "2026-05-06T09:00:12.760+0800",
  "event": "exec_tap_done"
}
```

| Field | Meaning |
| --- | --- |
| `x` / `y` | Actual tap coordinates. |

If the model output contains a tap but there is no `exec_tap_start`, the action may not have reached the executor.

## `exec_swipe_start` / `exec_swipe_done`

Swipe started and finished.

```json
{
  "task_id": "task-20260506-001",
  "x1": 540,
  "y1": 1800,
  "x2": 540,
  "y2": 600,
  "duration": 600,
  "ts": "2026-05-06T09:00:14.000+0800",
  "event": "exec_swipe_start"
}
```

| Field | Meaning |
| --- | --- |
| `x1` / `y1` | Swipe start point. |
| `x2` / `y2` | Swipe end point. |
| `duration` | Swipe duration in milliseconds. |

## `exec_input_start`

Text input is starting.

```json
{
  "task_id": "task-20260506-001",
  "text": "hello",
  "ts": "2026-05-06T09:00:16.000+0800",
  "event": "exec_input_start"
}
```

| Field | Meaning |
| --- | --- |
| `text` | Text to input. Mask private content before sharing trace publicly. |

## `exec_input_try`

AutoLXB tried one input method.

```json
{
  "task_id": "task-20260506-001",
  "try": 1,
  "method": 0,
  "status": 1,
  "actual_method": 0,
  "ts": "2026-05-06T09:00:16.200+0800",
  "event": "exec_input_try"
}
```

| Field | Meaning |
| --- | --- |
| `try` | Attempt number. |
| `method` | Planned input method. Internal numeric value; keep it when reporting issues. |
| `actual_method` | Actual input method used. |
| `status` | Input status. Usually `1` means success. |

## `exec_input_result`

Final input result.

```json
{
  "task_id": "task-20260506-001",
  "text": "hello",
  "method_auto": true,
  "chosen_method": 0,
  "actual_method": 0,
  "status": 1,
  "ts": "2026-05-06T09:00:16.260+0800",
  "event": "exec_input_result"
}
```

If `status` is not `1`, input usually failed. For Chinese input failures, first check whether ADB Keyboard is installed and enabled.

## `exec_wait_start` / `exec_wait_done`

The task intentionally waited.

```json
{
  "task_id": "task-20260506-001",
  "ms": 1000,
  "ts": "2026-05-06T09:00:17.000+0800",
  "event": "exec_wait_start"
}
```

| Field | Meaning |
| --- | --- |
| `ms` | Wait duration in milliseconds. |

## `exec_back_start` / `exec_back_done`

The system Back key was pressed.

```json
{
  "task_id": "task-20260506-001",
  "ts": "2026-05-06T09:00:18.000+0800",
  "event": "exec_back_start"
}
```

If a task repeatedly presses Back or returns to the wrong page, combine this with visual execution trace to see why the model chose Back.
