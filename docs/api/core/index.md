---
title: Core API
description: amplifier-core API reference
---

# Core API

The `amplifier-core` package provides the kernel APIs.

## Modules

- **[Session](session.md)** - `AmplifierSession` class
- **[Coordinator](coordinator.md)** - `ModuleCoordinator` class
- **[Hooks](hooks.md)** - `HookRegistry` and `HookResult`
- **[Models](models.md)** - Data models
- **[Events](events.md)** - Event constants

## Quick Import

```python
from amplifier_core import (
    AmplifierSession,
    ModuleCoordinator,
    HookResult,
    ToolResult,
)

from amplifier_core.events import (
    SESSION_START,
    SESSION_END,
    TOOL_PRE,
    TOOL_POST,
)
```
