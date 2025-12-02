---
title: Events API
description: Canonical event constants
---

# Events API

Amplifier uses a canonical event system for observability and hook integration.

**Source**: [amplifier_core/events.py](https://github.com/microsoft/amplifier-core/blob/main/amplifier_core/events.py)

## Event Taxonomy

Events follow a `namespace:action` naming convention.

### Session Events

| Event | Description |
|-------|-------------|
| `session:start` | Session initialized |
| `session:end` | Session cleanup complete |
| `session:fork` | Child session created |
| `session:resume` | Session resumed |

### Prompt Events

| Event | Description |
|-------|-------------|
| `prompt:submit` | User prompt submitted |
| `prompt:complete` | Prompt processing complete |

### Planning Events

| Event | Description |
|-------|-------------|
| `plan:start` | Planning phase started |
| `plan:end` | Planning phase completed |

### Provider Events

| Event | Description |
|-------|-------------|
| `provider:request` | LLM request initiated |
| `provider:response` | LLM response received |
| `provider:error` | LLM request failed |
| `llm:request` | LLM request (alias) |
| `llm:response` | LLM response (alias) |

### Content Block Events

| Event | Description |
|-------|-------------|
| `content_block:start` | Content block streaming started |
| `content_block:delta` | Content block chunk received |
| `content_block:end` | Content block streaming complete |
| `thinking:delta` | Thinking content chunk |
| `thinking:final` | Thinking content complete |

### Tool Events

| Event | Description |
|-------|-------------|
| `tool:pre` | Before tool execution |
| `tool:post` | After tool execution |
| `tool:error` | Tool execution failed |

### Context Events

| Event | Description |
|-------|-------------|
| `context:pre_compact` | Before context compaction |
| `context:post_compact` | After context compaction |
| `context:include` | Content included in context |

### Orchestrator Events

| Event | Description |
|-------|-------------|
| `orchestrator:complete` | Orchestration loop finished |

### User Events

| Event | Description |
|-------|-------------|
| `user:notification` | User notification |

### Artifact Events

| Event | Description |
|-------|-------------|
| `artifact:write` | Artifact written |
| `artifact:read` | Artifact read |

### Policy/Approval Events

| Event | Description |
|-------|-------------|
| `policy:violation` | Policy violation detected |
| `approval:required` | User approval needed |
| `approval:granted` | User approved action |
| `approval:denied` | User denied action |

## Usage

Events are emitted via the coordinator's hook registry:

```python
# In a module
await coordinator.hooks.emit("tool:pre", {
    "name": "bash",
    "input": {"command": "ls -la"}
})

# Execute the tool...

await coordinator.hooks.emit("tool:post", {
    "name": "bash",
    "result": {"output": "..."}
})
```

## Observability

The `hooks-logging` module subscribes to all events and writes them to JSONL:

```json
{
  "ts": "2024-01-15T10:30:00Z",
  "event": "tool:pre",
  "data": {"name": "bash", "input": {"command": "ls"}}
}
```

See [Event System](../../architecture/events.md) for architecture details.
