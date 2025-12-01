---
title: Module Contracts
description: Reference documentation for module interfaces
---

# Module Contracts

Contracts define the interfaces that modules must implement. They are the stable "studs" that allow modules to be developed and swapped independently.

## Contract Philosophy

- **Stable**: Contracts rarely change
- **Backward compatible**: Changes are additive
- **Protocol-based**: Duck typing via structural subtyping
- **Documented**: Clear expectations and examples

## Available Contracts

| Contract | Purpose | Link |
|----------|---------|------|
| **Provider** | LLM backend integration | [Provider Contract](provider.md) |
| **Tool** | Agent capabilities | [Tool Contract](tool.md) |
| **Hook** | Observability and control | [Hook Contract](hook.md) |
| **Orchestrator** | Execution loop strategy | [Orchestrator Contract](orchestrator.md) |
| **Context** | Memory management | [Context Contract](context.md) |

## Contract Structure

Each contract document covers:

1. **Purpose**: What this module type does
2. **Protocol**: The interface definition
3. **Mount Function**: How to register with the kernel
4. **Configuration**: Available options
5. **Events**: Events emitted/handled
6. **Examples**: Reference implementations

## Authoritative Sources

The authoritative contract documentation lives in `amplifier-core`:

- **→ [Provider Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/PROVIDER_CONTRACT.md)**
- **→ [Tool Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/TOOL_CONTRACT.md)**
- **→ [Hook Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/HOOK_CONTRACT.md)**
- **→ [Orchestrator Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/ORCHESTRATOR_CONTRACT.md)**
- **→ [Context Contract](https://github.com/microsoft/amplifier-core/blob/main/docs/contracts/CONTEXT_CONTRACT.md)**
