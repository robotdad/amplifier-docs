---
title: Logging Hook
description: JSONL event logging for observability
---

# Logging Hook

Provides visibility into agent execution through lifecycle event logging.

## Module ID

`hooks-logging`

## Installation

```yaml
hooks:
  - module: hooks-logging
    source: git+https://github.com/microsoft/amplifier-module-hooks-logging@main
    config:
      level: INFO
      output: console
```

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `level` | string | `INFO` | Log level: DEBUG, INFO, WARNING, ERROR |
| `output` | string | `console` | Output target: console, file, or both |
| `file` | string | - | Log file path (required if output includes "file") |
| `auto_discover` | bool | `true` | Auto-discover module events |
| `additional_events` | list | `[]` | Extra events to log |

## Log Levels

### INFO (Recommended)

- Session lifecycle
- Tool invocations (name only)
- Sub-agent activity
- Errors and warnings

### DEBUG

Shows all details including:

- Tool arguments and results
- Full message content
- LLM request/response details (requires `debug: true` on provider)

### WARNING / ERROR

Shows only warnings or critical failures.

## Features

- **Zero code changes** - Pure configuration
- **Auto-discovery** - Modules declare observable events
- **Standard Python logging** - No external dependencies
- **Flexible output** - Console, file, or both

## Example Output

```
2025-10-06 12:00:00 [INFO] === Session Started ===
2025-10-06 12:00:01 [INFO] Tool invoked: grep
2025-10-06 12:00:02 [INFO] Tool completed: grep ✓
2025-10-06 12:00:05 [INFO] Sub-agent spawning: architect
2025-10-06 12:00:10 [INFO] Sub-agent completed: architect
2025-10-06 12:00:11 [INFO] === Session Ended ===
```

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-hooks-logging)**
