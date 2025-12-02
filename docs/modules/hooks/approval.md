---
title: Approval Hook
description: User approval gates for dangerous operations
---

# Approval Hook

Intercepts tool execution requests and coordinates user approval before dangerous operations.

## Module ID

`hooks-approval`

## Installation

```yaml
hooks:
  - module: hooks-approval
    source: git+https://github.com/microsoft/amplifier-module-hooks-approval@main
    config:
      patterns:
        - rm -rf
        - sudo
        - dd if=
      auto_approve: false
```

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `patterns` | list | `[]` | Command patterns requiring approval |
| `auto_approve` | bool | `false` | Skip approval prompts |

## Features

- **Hook-based interception** via `tool:pre` events
- **Pluggable approval providers** (CLI, GUI, headless)
- **Rule-based auto-approval** configuration
- **Audit trail logging** (JSONL format)
- **Risk-level based** approval requirements
- **Optional timeout** support

## Usage

```yaml
hooks:
  - module: hooks-approval
    config:
      patterns:
        - rm -rf
        - sudo
        - dd if=
      auto_approve: false
```

## Philosophy

- **Mechanism, not policy**: Core provides hooks, this module orchestrates
- **Tools declare needs** via metadata
- **Providers handle UI**
- **Audit trail** for accountability

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-hooks-approval)**
