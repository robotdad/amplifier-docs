---
title: Redaction Hook
description: Sensitive data masking for logs
---

# Redaction Hook

Masks secrets and PII before logging.

## Module ID

`hooks-redaction`

## Installation

```yaml
hooks:
  - module: hooks-redaction
    source: git+https://github.com/microsoft/amplifier-module-hooks-redaction@main
```

## Behavior

Scans messages for sensitive patterns and replaces them with `[REDACTED]`:

- Email addresses
- Phone numbers
- Credit card numbers
- Custom regex patterns

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `patterns` | list | (built-in) | Additional regex patterns to redact |
| `replacement` | string | `[REDACTED]` | Replacement text |

## Usage

```yaml
hooks:
  - module: hooks-redaction
    config:
      patterns:
        - "sk-[a-zA-Z0-9]{48}"  # API keys
        - "ghp_[a-zA-Z0-9]{36}"  # GitHub tokens
```

!!! important "Priority"
    Register redaction hook with **higher priority** than logging to ensure sensitive data is masked before it reaches logs.

```yaml
hooks:
  - module: hooks-redaction
    priority: 100  # High priority - runs first

  - module: hooks-logging
    priority: 50   # Lower priority - runs after redaction
```

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-hooks-redaction)**
