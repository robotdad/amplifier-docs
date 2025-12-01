---
title: Anthropic Provider
description: Claude model integration
---

# Anthropic Provider

Integrates Anthropic's Claude models into Amplifier.

## Module ID

`provider-anthropic`

## Installation

```yaml
providers:
  - module: provider-anthropic
    source: git+https://github.com/microsoft/amplifier-module-provider-anthropic@main
    config:
      default_model: claude-sonnet-4-5
```

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `api_key` | string | `$ANTHROPIC_API_KEY` | API authentication key |
| `default_model` | string | `claude-sonnet-4-5` | Default model |
| `max_tokens` | int | 4096 | Maximum response tokens |
| `temperature` | float | 1.0 | Sampling temperature |

## Supported Models

| Model | Description |
|-------|-------------|
| `claude-opus-4-1` | Most capable |
| `claude-sonnet-4-5` | Balanced (recommended) |
| `claude-haiku-3-5` | Fastest |

## Usage

```bash
# Set API key
export ANTHROPIC_API_KEY="sk-ant-..."

# Use provider
amplifier provider use anthropic
amplifier run "Hello!"
```

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-provider-anthropic)**
