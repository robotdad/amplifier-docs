---
title: Persistent Context
description: Cross-session memory with file loading
---

# Persistent Context

Extends SimpleContextManager with persistent file loading for cross-session memory.

## Module ID

`context-persistent`

## Installation

```yaml
contexts:
  - module: context-persistent
    source: git+https://github.com/microsoft/amplifier-module-context-persistent@main
    config:
      memory_files:
        - ./AGENTS.md
        - ./PROJECT.md
        - ~/.amplifier/AGENTS.md
      max_tokens: 200000
      compact_threshold: 0.92
```

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `memory_files` | list | `[]` | Context files to load at session start |
| `max_tokens` | int | `200000` | Maximum token limit |
| `compact_threshold` | float | `0.92` | Compaction threshold (0-1) |

## Features

- **Inherits from SimpleContextManager**: All base functionality
- **File loading at session start**: Automatically loads configured files
- **Graceful error handling**: Skips missing files with warnings
- **Clear context labeling**: Each loaded file is labeled
- **Home directory expansion**: Supports `~/` paths

## How It Works

1. **Session Start**: Loads all configured files
2. **File Processing**: Each file added as system message
3. **Context Labeling**: Files labeled (e.g., `[Context from AGENTS.md]`)
4. **Error Handling**: Missing files skipped with warnings
5. **Normal Operation**: Behaves like SimpleContextManager

## Usage

```toml
[session]
context = "context-persistent"

[context]
memory_files = [
    "./TEAM_STYLE_GUIDE.md",
    "./PROJECT_ARCHITECTURE.md"
]
```

Perfect for:

- Team context files
- Project-specific knowledge
- Personal AI preferences

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-context-persistent)**
