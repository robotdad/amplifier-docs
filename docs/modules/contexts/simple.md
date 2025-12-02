---
title: Simple Context
description: Basic in-memory conversation context
---

# Simple Context

Basic message list context manager for conversation state. This is the default context manager.

## Module ID

`context-simple`

## Installation

```yaml
contexts:
  - module: context-simple
    source: git+https://github.com/microsoft/amplifier-module-context-simple@main
    config:
      max_messages: 100
```

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `max_messages` | int | `100` | Optional message limit |

## Behavior

- **In-memory message list**
- **No persistence** across sessions
- **Automatic compaction** when approaching token limit
- **Preserves tool pairs** as atomic units during compaction

## Compaction Strategy

Compacts automatically when token usage reaches threshold (default: 92% of max_tokens):

- **Keeps**: All system messages + last 10 conversation messages
- **Deduplicates**: Non-tool messages (based on role and first 100 chars)
- **Preserves tool pairs**: Tool_use and tool_result messages stay together

## Usage

```toml
[session]
context = "context-simple"
```

Perfect for:

- Development and testing
- Short conversations
- Stateless applications

Not suitable for:

- Cross-session persistence
- Custom compaction strategies

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-context-simple)**
