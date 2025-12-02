---
title: Orchestrators
description: Execution loop strategies
---

# Orchestrators

Orchestrators control how agents execute: the loop structure, tool handling, and response generation.

## Available Orchestrators

| Orchestrator | Description | Repository |
|--------------|-------------|------------|
| **[Basic](loop_basic.md)** | Simple request/response loop | [GitHub](https://github.com/microsoft/amplifier-module-loop-basic) |
| **[Streaming](loop_streaming.md)** | Real-time token streaming | [GitHub](https://github.com/microsoft/amplifier-module-loop-streaming) |
| **[Events](loop_events.md)** | Event-driven architecture | [GitHub](https://github.com/microsoft/amplifier-module-loop-events) |

<!-- MODULE_LIST_LOOP -->

## Configuration

```yaml
session:
  orchestrator: loop-streaming  # or loop-basic, loop-events

orchestrator:
  config:
    max_iterations: 10
    parallel_tools: false
```

## Contract

See [Orchestrator Contract](../../developer/contracts/orchestrator.md) for implementation details.
