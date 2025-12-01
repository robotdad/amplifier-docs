---
title: Contexts
description: Memory management
---

# Contexts

Context managers handle conversation memory, token limits, and optional persistence.

## Available Contexts

| Context | Description | Repository |
|---------|-------------|------------|
| **[Simple](simple.md)** | In-memory context | [GitHub](https://github.com/microsoft/amplifier-module-context-simple) |
| **[Persistent](persistent.md)** | File-backed persistence | [GitHub](https://github.com/microsoft/amplifier-module-context-persistent) |

<!-- MODULE_LIST_CONTEXT -->

## Configuration

```yaml
session:
  context: context-persistent  # or context-simple

context:
  config:
    max_tokens: 100000
    compaction_strategy: truncate
```

## Contract

See [Context Contract](../developer/contracts/context.md) for implementation details.
