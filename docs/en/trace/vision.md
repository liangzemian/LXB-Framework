# Visual Execution Trace

Visual execution trace helps determine whether the model received a screenshot, what action it returned, whether the output was parsed, and whether the action executed.

## `vision_screenshot_ready`

A screenshot was captured successfully for this visual execution turn.

```json
{
  "task_id": "task-20260506-001",
  "size": 384221,
  "attached": true,
  "ts": "2026-05-06T09:00:10.100+0800",
  "event": "vision_screenshot_ready"
}
```

| Field | Meaning |
| --- | --- |
| `size` | Screenshot size in bytes. Greater than 0 usually means the screenshot is valid. |
| `attached` | Whether the screenshot was attached to the model request. |

If you see `vision_screenshot_failed` or `vision_screenshot_error`, screenshot capture failed and the model may not be able to observe the page.

## `llm_prompt_vision_act`

A prompt is about to be sent to the model for visual execution.

```json
{
  "task_id": "task-20260506-001",
  "state": "VISION_ACT",
  "attempt": 1,
  "prompt": "You are controlling an Android phone...",
  "ts": "2026-05-06T09:00:10.200+0800",
  "event": "llm_prompt_vision_act"
}
```

| Field | Meaning |
| --- | --- |
| `state` | Current phase, usually `VISION_ACT`. |
| `attempt` | Attempt number. The model may be retried after parse or request failures. |
| `prompt` | Prompt sent to the model. Long but useful for difficult issues. |

## `llm_response_vision_act`

The model returned a raw response.

```json
{
  "task_id": "task-20260506-001",
  "state": "VISION_ACT",
  "attempt": 1,
  "response": "<Observing>Home page...</Observing><command>TAP 540 1860</command>",
  "ts": "2026-05-06T09:00:12.300+0800",
  "event": "llm_response_vision_act"
}
```

| Field | Meaning |
| --- | --- |
| `response` | Raw model output. It shows what the model understood and planned to do. |
| `attempt` | Which attempt this response belongs to. |

## `llm_structured_vision_act`

The model output was parsed into structured fields. This is easier to read than the raw response.

```json
{
  "task_id": "task-20260506-001",
  "state": "VISION_ACT",
  "data": {
    "Observing": "The app home page is visible",
    "Ovserve_result": "A check-in entry is visible near the bottom",
    "Thinking": "Need to enter the check-in page",
    "action": "Tap the check-in entry",
    "expected": "The check-in page opens",
    "command": "TAP 540 1860"
  },
  "command": "TAP 540 1860",
  "ts": "2026-05-06T09:00:12.360+0800",
  "event": "llm_structured_vision_act"
}
```

| Field | Meaning |
| --- | --- |
| `data.Observing` | What the model observed on the screen. |
| `data.Thinking` | Why the model wants to act this way. |
| `data.action` | Human-readable action description. |
| `data.expected` | What the model expects after the action. |
| `command` | Actual command passed to the executor. |

## `vision_retry`

A retryable problem happened, such as model request failure, action execution failure, or invalid output format.

```json
{
  "task_id": "task-20260506-001",
  "state": "VISION_ACT",
  "phase": "parse",
  "attempt": 1,
  "max_attempts": 3,
  "error": "missing <command> tag",
  "retrying": true,
  "ts": "2026-05-06T09:00:12.500+0800",
  "event": "vision_retry"
}
```

| Field | Meaning |
| --- | --- |
| `phase` | Where the problem happened, such as `planner_call`, `parse`, `command_args`, or `action_exec`. |
| `attempt` | Current attempt number. |
| `max_attempts` | Maximum attempts. |
| `error` / `reason` | Failure reason. Field name may vary by phase. |
| `retrying` | Whether AutoLXB will retry. |

## `vision_instruction_invalid`

The model output could not be parsed after retries, so visual execution failed.

```json
{
  "task_id": "task-20260506-001",
  "state": "VISION_ACT",
  "error": "missing <command> tag",
  "ts": "2026-05-06T09:00:15.100+0800",
  "event": "vision_instruction_invalid"
}
```

If this appears often, the selected model may not follow the required visual execution format, or the prompt/output format is not compatible with that model.
