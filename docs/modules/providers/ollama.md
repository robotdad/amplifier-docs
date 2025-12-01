---
title: Ollama Provider
description: Local model integration
---

# Ollama Provider

Integrates locally-running Ollama models into Amplifier.

## Module ID

`provider-ollama`

## Installation

```yaml
providers:
  - module: provider-ollama
    source: git+https://github.com/microsoft/amplifier-module-provider-ollama@main
```

## Prerequisites

1. Install Ollama: `brew install ollama` (macOS)
2. Start server: `ollama serve`
3. Pull model: `ollama pull llama3.1`

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `base_url` | string | `http://localhost:11434` | Ollama server URL |
| `default_model` | string | `llama3.1` | Default model |

## Supported Models

Any model pulled with `ollama pull`:

- `llama3.1`
- `codellama`
- `mistral`
- And more...

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-provider-ollama)**
