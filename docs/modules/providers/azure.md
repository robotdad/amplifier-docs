---
title: Azure OpenAI Provider
description: Azure-hosted GPT models
---

# Azure OpenAI Provider

Integrates Azure OpenAI Service into Amplifier.

## Module ID

`provider-azure-openai`

## Installation

```yaml
providers:
  - module: provider-azure-openai
    source: git+https://github.com/microsoft/amplifier-module-provider-azure-openai@main
    config:
      endpoint: https://your-resource.openai.azure.com
      deployment: your-deployment-name
```

## Configuration

| Option | Type | Description |
|--------|------|-------------|
| `api_key` | string | Azure OpenAI API key |
| `endpoint` | string | Azure resource endpoint |
| `deployment` | string | Deployment name |
| `api_version` | string | API version |

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-provider-azure-openai)**
