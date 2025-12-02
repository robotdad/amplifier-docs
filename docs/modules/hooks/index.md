---
title: Hooks
description: Observability and control
---

# Hooks

Hooks observe and control operations. They can log events, block operations, inject context, and request user approval.

## Available Hooks

| Hook | Description | Repository |
|------|-------------|------------|
| **[Logging](logging.md)** | JSONL event logging | [GitHub](https://github.com/microsoft/amplifier-module-hooks-logging) |
| **[Approval](approval.md)** | User approval gates | [GitHub](https://github.com/microsoft/amplifier-module-hooks-approval) |
| **[Redaction](redaction.md)** | Sensitive data redaction | [GitHub](https://github.com/microsoft/amplifier-module-hooks-redaction) |
| **Streaming UI** | Real-time output display | [GitHub](https://github.com/microsoft/amplifier-module-hooks-streaming-ui) |
| **Backup** | File backup before writes | [GitHub](https://github.com/microsoft/amplifier-module-hooks-backup) |
| **Status Context** | Status tracking injection | [GitHub](https://github.com/microsoft/amplifier-module-hooks-status-context) |
| **Todo Reminder** | Todo list context injection | [GitHub](https://github.com/microsoft/amplifier-module-hooks-todo-reminder) |
| **Scheduler Heuristic** | Smart tool scheduling | [GitHub](https://github.com/microsoft/amplifier-module-hooks-scheduler-heuristic) |
| **Scheduler Cost-Aware** | Cost-optimized scheduling | [GitHub](https://github.com/microsoft/amplifier-module-hooks-scheduler-cost-aware) |

<!-- MODULE_LIST_HOOKS -->

## Configuration

```yaml
hooks:
  - module: hooks-logging
    config:
      level: info
      output: ~/.amplifier/logs/

  - module: hooks-approval
    config:
      require_approval_for:
        - tool-bash
        - tool-filesystem:write
```

## Hook Actions

| Action | Effect |
|--------|--------|
| `continue` | Proceed normally |
| `deny` | Block operation |
| `modify` | Transform data |
| `inject_context` | Add to conversation |
| `ask_user` | Request approval |

## Contract

See [Hook Contract](../../developer/contracts/hook.md) for implementation details.
