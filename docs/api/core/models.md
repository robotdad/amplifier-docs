---
title: Models API
description: Data model reference
---

# Models API

Core data models used throughout Amplifier. All models use Pydantic for validation.

**Source**: [amplifier_core/models.py](https://github.com/microsoft/amplifier-core/blob/main/amplifier_core/models.py)

## ToolCall

Represents an LLM's request to call a tool.

```python
class ToolCall(BaseModel):
    tool: str                        # Tool name to invoke
    arguments: dict[str, Any] = {}   # Tool arguments
    id: str | None = None            # Unique tool call ID
```

### Example

```python
ToolCall(
    id="call_123",
    tool="bash",
    arguments={"command": "ls -la"}
)
```

## ToolResult

Result returned by tool execution.

```python
class ToolResult(BaseModel):
    success: bool = True                    # Whether execution succeeded
    output: Any | None = None               # Tool output data
    error: dict[str, Any] | None = None     # Error details if failed
```

### Example

```python
# Successful result
ToolResult(output="File created successfully", success=True)

# Failed result
ToolResult(
    success=False,
    error={"message": "Permission denied", "code": "EPERM"}
)
```

## ProviderInfo

Metadata about a loaded provider.

```python
class ProviderInfo(BaseModel):
    id: str                              # Provider identifier (e.g., "anthropic")
    display_name: str                    # Human-readable provider name
    credential_env_vars: list[str] = []  # Environment variables for credentials
    capabilities: list[str] = []         # Capability list (e.g., "streaming", "batch")
    defaults: dict[str, Any] = {}        # Provider-level default config values
    config_fields: list[ConfigField] = [] # Configuration fields for setup
```

### Example

```python
ProviderInfo(
    id="anthropic",
    display_name="Anthropic",
    credential_env_vars=["ANTHROPIC_API_KEY"],
    capabilities=["streaming", "tools", "vision"],
    defaults={"timeout": 300.0}
)
```

## ModelInfo

Metadata about an AI model.

```python
class ModelInfo(BaseModel):
    id: str                          # Model identifier (e.g., "claude-sonnet-4-5")
    display_name: str                # Human-readable model name
    context_window: int              # Maximum context window in tokens
    max_output_tokens: int           # Maximum output tokens
    capabilities: list[str] = []    # Capability list (e.g., "tools", "vision", "thinking")
    defaults: dict[str, Any] = {}   # Model-specific default config values
```

### Example

```python
ModelInfo(
    id="claude-sonnet-4-5",
    display_name="Claude Sonnet 4.5",
    context_window=200000,
    max_output_tokens=8192,
    capabilities=["tools", "vision", "streaming"],
    defaults={"temperature": 1.0}
)
```

## ModuleInfo

Metadata about a loaded module.

```python
class ModuleInfo(BaseModel):
    id: str                          # Module identifier
    name: str                        # Module display name
    version: str                     # Module version
    type: str                        # Module type (provider, tool, hook, etc.)
    mount_point: str                 # Where module should be mounted
    description: str                 # Module description
    config_schema: dict | None = None # JSON schema for module configuration
```

## HookResult

Result from hook execution with enhanced capabilities.

```python
class HookResult(BaseModel):
    action: str = "continue"         # continue, deny, modify, inject_context, ask_user
    data: dict | None = None         # Modified event data (for action='modify')
    reason: str | None = None        # Explanation for deny/modification

    # Context injection
    context_injection: str | None = None      # Text to inject into agent context
    context_injection_role: str = "system"    # Role: system, user, assistant
    ephemeral: bool = False                   # Temporary injection (current call only)

    # Approval gates
    approval_prompt: str | None = None        # Question to ask user
    approval_options: list[str] | None = None # User choice options
    approval_timeout: float = 300.0           # Timeout in seconds
    approval_default: str = "deny"            # Default on timeout: allow, deny

    # Output control
    suppress_output: bool = False             # Hide hook's output from user
    user_message: str | None = None           # Message to display to user
    user_message_level: str = "info"          # Severity: info, warning, error
```

See [Hooks API](hooks.md) for detailed HookResult documentation.

## SessionStatus

Session status and metadata.

```python
class SessionStatus(BaseModel):
    session_id: str
    started_at: datetime
    ended_at: datetime | None = None
    status: str = "running"          # running, completed, failed, cancelled

    # Counters
    total_messages: int = 0
    tool_invocations: int = 0
    tool_successes: int = 0
    tool_failures: int = 0

    # Token usage
    total_input_tokens: int = 0
    total_output_tokens: int = 0

    # Cost tracking
    estimated_cost: float | None = None
```
