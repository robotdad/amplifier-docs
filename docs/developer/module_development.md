---
title: Module Development
description: Creating custom Amplifier modules
---

# Module Development

This guide covers creating custom modules for Amplifier: providers, tools, hooks, orchestrators, and context managers.

## Module Structure

Every module follows the same structure:

```
amplifier-module-{type}-{name}/
├── amplifier_module_{type}_{name}/
│   └── __init__.py         # Module code
├── tests/
│   └── test_module.py      # Tests
├── pyproject.toml          # Package configuration
├── README.md               # Documentation
└── LICENSE
```

## The Mount Function

Every module exposes a `mount` function:

```python
from typing import Any, Callable

async def mount(
    coordinator: "ModuleCoordinator",
    config: dict[str, Any] | None = None
) -> Callable | None:
    """
    Mount the module.

    Args:
        coordinator: Infrastructure context from kernel
        config: Configuration from Mount Plan

    Returns:
        Optional cleanup function (async callable)
    """
    config = config or {}

    # Create your module instance
    module = MyModule(config)

    # Mount to appropriate mount point
    await coordinator.mount("tools", module, name="my-tool")

    # Optional: return cleanup function
    async def cleanup():
        await module.close()

    return cleanup
```

## Creating a Tool

Tools provide capabilities to agents.

### Tool Contract

```python
class Tool:
    name: str               # Unique identifier
    description: str        # Human-readable description
    input_schema: dict      # JSON Schema for parameters

    async def execute(self, input: dict) -> ToolResult:
        """Execute the tool with given input."""
        ...
```

### Example: Calculator Tool

```python
# amplifier_module_tool_calculator/__init__.py

from typing import Any

async def mount(coordinator, config=None):
    tool = CalculatorTool(config or {})
    await coordinator.mount("tools", tool, name="calculator")
    return None

class CalculatorTool:
    name = "calculator"
    description = "Perform mathematical calculations"
    input_schema = {
        "type": "object",
        "properties": {
            "expression": {
                "type": "string",
                "description": "Mathematical expression to evaluate"
            }
        },
        "required": ["expression"]
    }

    def __init__(self, config: dict):
        self.config = config

    async def execute(self, input: dict[str, Any]) -> dict:
        expression = input.get("expression", "")
        try:
            # Safe evaluation (in production, use proper parser)
            result = eval(expression, {"__builtins__": {}}, {})
            return {
                "success": True,
                "output": str(result)
            }
        except Exception as e:
            return {
                "success": False,
                "error": str(e)
            }
```

### pyproject.toml

```toml
[project]
name = "amplifier-module-tool-calculator"
version = "1.0.0"
description = "Calculator tool for Amplifier"
requires-python = ">=3.11"
dependencies = []

[project.entry-points."amplifier.modules"]
tool-calculator = "amplifier_module_tool_calculator:mount"

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[tool.hatch.build.targets.wheel]
packages = ["amplifier_module_tool_calculator"]
```

## Creating a Provider

Providers integrate LLM backends.

### Provider Contract

```python
class Provider:
    name: str

    def get_info(self) -> ProviderInfo: ...
    async def list_models(self) -> list[ModelInfo]: ...
    async def complete(self, request: ChatRequest, **kwargs) -> ChatResponse: ...
    def parse_tool_calls(self, response: ChatResponse) -> list[ToolCall]: ...
```

### Example: Mock Provider

```python
async def mount(coordinator, config=None):
    provider = MockProvider(config or {})
    await coordinator.mount("providers", provider, name="mock")
    return None

class MockProvider:
    name = "mock"

    def __init__(self, config):
        self.response = config.get("response", "Mock response")

    def get_info(self):
        return {"name": "mock", "version": "1.0.0"}

    async def list_models(self):
        return [{"id": "mock-model", "name": "Mock Model"}]

    async def complete(self, request, **kwargs):
        return {
            "content": [{"type": "text", "text": self.response}],
            "usage": {"input_tokens": 10, "output_tokens": 5}
        }

    def parse_tool_calls(self, response):
        return []
```

## Creating a Hook

Hooks observe and control operations.

### Hook Contract

```python
async def handler(event: str, data: dict) -> HookResult:
    """Handle an event."""
    return HookResult(action="continue")
```

### HookResult Actions

| Action | Effect |
|--------|--------|
| `continue` | Proceed normally |
| `deny` | Block the operation |
| `modify` | Modify event data |
| `inject_context` | Add to conversation |
| `ask_user` | Request approval |

### Example: Timing Hook

```python
import time

async def mount(coordinator, config=None):
    handler = TimingHook(config or {})

    coordinator.hooks.register("tool:pre", handler.on_tool_pre)
    coordinator.hooks.register("tool:post", handler.on_tool_post)

    return None

class TimingHook:
    def __init__(self, config):
        self.timings = {}

    async def on_tool_pre(self, event, data):
        tool_name = data.get("tool_name")
        self.timings[tool_name] = time.time()
        return {"action": "continue"}

    async def on_tool_post(self, event, data):
        tool_name = data.get("tool_name")
        if tool_name in self.timings:
            duration = time.time() - self.timings[tool_name]
            print(f"Tool {tool_name} took {duration:.2f}s")
        return {"action": "continue"}
```

## Creating an Orchestrator

Orchestrators control execution flow.

### Orchestrator Contract

```python
class Orchestrator:
    async def execute(
        self,
        prompt: str,
        context: ContextManager,
        providers: dict[str, Provider],
        tools: dict[str, Tool],
        hooks: HookRegistry,
    ) -> str:
        """Execute the orchestration loop."""
        ...
```

### Example: Simple Orchestrator

```python
async def mount(coordinator, config=None):
    orchestrator = SimpleOrchestrator(config or {})
    await coordinator.mount("orchestrator", orchestrator)
    return None

class SimpleOrchestrator:
    def __init__(self, config):
        self.max_iterations = config.get("max_iterations", 10)

    async def execute(self, prompt, context, providers, tools, hooks):
        # Add user message
        await context.add_message({"role": "user", "content": prompt})

        # Get first provider
        provider = list(providers.values())[0]

        for _ in range(self.max_iterations):
            # Get messages
            messages = await context.get_messages()

            # Call provider
            await hooks.emit("provider:request", {"messages": messages})
            response = await provider.complete({"messages": messages})
            await hooks.emit("provider:response", {"response": response})

            # Add response to context
            await context.add_message({
                "role": "assistant",
                "content": response["content"]
            })

            # Check for tool calls
            tool_calls = provider.parse_tool_calls(response)
            if not tool_calls:
                # No tools, return response
                return response["content"][0]["text"]

            # Execute tools
            for call in tool_calls:
                tool = tools.get(call["name"])
                if tool:
                    await hooks.emit("tool:pre", {"tool_name": call["name"]})
                    result = await tool.execute(call["input"])
                    await hooks.emit("tool:post", {"result": result})
                    await context.add_message({
                        "role": "tool",
                        "content": result
                    })

        return "Max iterations reached"
```

## Testing Modules

### Unit Testing

```python
import pytest
from amplifier_module_tool_calculator import CalculatorTool

@pytest.fixture
def tool():
    return CalculatorTool({})

@pytest.mark.asyncio
async def test_addition(tool):
    result = await tool.execute({"expression": "2 + 2"})
    assert result["success"] is True
    assert result["output"] == "4"

@pytest.mark.asyncio
async def test_invalid_expression(tool):
    result = await tool.execute({"expression": "invalid"})
    assert result["success"] is False
    assert "error" in result
```

### Integration Testing

```python
from amplifier_core.testing import MockCoordinator

@pytest.mark.asyncio
async def test_mount():
    coordinator = MockCoordinator()

    from amplifier_module_tool_calculator import mount
    cleanup = await mount(coordinator, {})

    assert "calculator" in coordinator.tools
    assert coordinator.tools["calculator"].name == "calculator"
```

## Publishing Modules

### To GitHub

```bash
# Create repository
gh repo create amplifier-module-tool-myname --public

# Push code
git init
git add .
git commit -m "Initial commit"
git push -u origin main
```

### Using Your Module

```yaml
# In profile or mount plan
tools:
  - module: tool-myname
    source: git+https://github.com/yourname/amplifier-module-tool-myname@main
```

## Best Practices

1. **Single responsibility**: One module, one purpose
2. **Minimal dependencies**: Keep modules lightweight
3. **Clear documentation**: Include README with examples
4. **Comprehensive tests**: Unit and integration tests
5. **Semantic versioning**: Use git tags for versions
6. **Error handling**: Return errors, don't throw

## References

- **→ [Provider Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/PROVIDER_CONTRACT.md)**
- **→ [Tool Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/TOOL_CONTRACT.md)**
- **→ [Hook Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/HOOK_CONTRACT.md)**
- **→ [Orchestrator Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/ORCHESTRATOR_CONTRACT.md)**
- **→ [Context Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/CONTEXT_CONTRACT.md)**
