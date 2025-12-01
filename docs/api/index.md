---
title: API Reference
description: Auto-generated API documentation
---

# API Reference

Auto-generated API documentation from source code docstrings.

## Core API

The `amplifier-core` package provides the kernel APIs:

- **[Session](core/session.md)** - Main entry point for creating AI sessions
- **[Coordinator](core/coordinator.md)** - Infrastructure context for modules
- **[Hooks](core/hooks.md)** - Event system and hook registry
- **[Models](core/models.md)** - Data models (HookResult, ToolResult, etc.)
- **[Events](core/events.md)** - Canonical event constants

## CLI API

The `amplifier-app-cli` package provides CLI components:

- **[Commands](cli/index.md)** - CLI command implementations

## Usage

### Creating a Session

```python
from amplifier_core import AmplifierSession

mount_plan = {
    "session": {
        "orchestrator": "loop-basic",
        "context": "context-simple"
    },
    "providers": [
        {"module": "provider-anthropic"}
    ]
}

async with AmplifierSession(mount_plan) as session:
    await session.initialize()
    response = await session.execute("Hello!")
```

### Using the Coordinator

```python
# In a module's mount function
async def mount(coordinator, config=None):
    # Access infrastructure
    session_id = coordinator.session_id

    # Mount modules
    await coordinator.mount("tools", my_tool, name="my-tool")

    # Emit events
    await coordinator.hooks.emit("my-module:ready", {})

    # Register capabilities
    coordinator.register_capability("my-capability", implementation)
```

## Note on Auto-Generation

These API docs are generated from Python docstrings using [mkdocstrings](https://mkdocstrings.github.io/).

For the most accurate and up-to-date information, refer to the source code:

- **→ [amplifier-core source](https://github.com/microsoft/amplifier-core/tree/main/amplifier_core)**
- **→ [amplifier-app-cli source](https://github.com/microsoft/amplifier-app-cli/tree/main/amplifier_app_cli)**
