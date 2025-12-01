---
title: OpenAI Provider
description: GPT model integration
---

# OpenAI Provider

Integrates OpenAI's GPT models into Amplifier.

## Module ID

`provider-openai`

## Installation

```yaml
providers:
  - module: provider-openai
    source: git+https://github.com/microsoft/amplifier-module-provider-openai@main
```

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `api_key` | string | `$OPENAI_API_KEY` | API key |
| `default_model` | string | `gpt-4o` | Default model |

## Supported Models

| Model | Description |
|-------|-------------|
| `gpt-4o` | Latest multimodal |
| `gpt-4-turbo` | Fast, capable |
| `gpt-4` | Original GPT-4 |

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-provider-openai)**
