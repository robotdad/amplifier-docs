---
title: Provider Contract
description: LLM backend integration contract
---

# Provider Contract

Providers integrate LLM backends into Amplifier.

## Purpose

Providers translate between Amplifier's unified message format and vendor-specific LLM APIs.

## Protocol

```python
from typing import Protocol, runtime_checkable

@runtime_checkable
class Provider(Protocol):
    @property
    def name(self) -> str:
        """Unique provider identifier."""
        ...

    def get_info(self) -> ProviderInfo:
        """Return provider metadata."""
        ...

    async def list_models(self) -> list[ModelInfo]:
        """List available models."""
        ...

    async def complete(
        self,
        request: ChatRequest,
        **kwargs
    ) -> ChatResponse:
        """Complete a chat request."""
        ...

    def parse_tool_calls(
        self,
        response: ChatResponse
    ) -> list[ToolCall]:
        """Extract tool calls from response."""
        ...
```

## Mount Function

```python
async def mount(coordinator, config=None):
    config = config or {}
    provider = MyProvider(config)
    await coordinator.mount("providers", provider, name=provider.name)
    return cleanup_function  # or None
```

## Configuration

Common configuration options:

| Option | Type | Description |
|--------|------|-------------|
| `api_key` | string | API authentication key |
| `default_model` | string | Default model to use |
| `max_tokens` | int | Maximum response tokens |
| `temperature` | float | Sampling temperature |
| `timeout` | float | Request timeout in seconds |

## Events

Providers should emit these events:

| Event | When | Data |
|-------|------|------|
| `llm:request` | Before API call | model, message_count |
| `llm:response` | After API response | usage, duration |
| `llm:request:debug` | Debug logging | Request summary |
| `llm:response:debug` | Debug logging | Response summary |

## Example Implementation

```python
class MyProvider:
    name = "my-provider"

    def __init__(self, config):
        self.api_key = config.get("api_key")
        self.default_model = config.get("default_model", "my-model")

    def get_info(self):
        return {"name": self.name, "version": "1.0.0"}

    async def list_models(self):
        return [{"id": self.default_model, "name": "My Model"}]

    async def complete(self, request, **kwargs):
        # Convert to vendor format
        # Call vendor API
        # Convert response back
        return ChatResponse(...)

    def parse_tool_calls(self, response):
        # Extract tool calls from response
        return []
```

## Authoritative Reference

**→ [Provider Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/PROVIDER_CONTRACT.md)** - Complete specification
