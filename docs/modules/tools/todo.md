---
title: Todo Tool
description: AI self-accountability for complex tasks
---

# Todo Tool

AI self-accountability tool for managing todo lists during complex multi-step tasks.

## Module ID

`tool-todo`

## Installation

```yaml
tools:
  - module: tool-todo
    source: git+https://github.com/microsoft/amplifier-module-tool-todo@main
    config: {}
```

## Purpose

Provides cognitive scaffolding for AI agents to maintain focus through long, complex turns where context fills up and plans might get buried.

**This is NOT for showing task progress to users** - it's for AI self-management to prevent wandering or forgetting steps.

## The Problem It Solves

**Typical failure pattern:**

1. AI gets complex task, creates plan [Step 1-5]
2. Completes steps 1-2, context fills with results (30k+ tokens)
3. At step 3: AI forgets original plan buried in context
4. Risk: AI wanders, declares done prematurely, abandons remaining steps

**Solution:**

- AI creates todo list using this tool
- Hook injects reminders before each turn
- AI sees: "✓1 done, ✓2 done, ☐3 pending..."
- AI stays on track, completes all commitments

## Tool Interface

### Actions

**create**: Replace entire list with new todos

```json
{
  "action": "create",
  "todos": [
    {"content": "Research auth requirements", "activeForm": "Researching auth requirements", "status": "pending"},
    {"content": "Design auth flow", "activeForm": "Designing auth flow", "status": "pending"}
  ]
}
```

**update**: Replace entire list (AI manages transitions)

```json
{
  "action": "update",
  "todos": [...]
}
```

**list**: Return current todos

```json
{
  "action": "list"
}
```

## Todo Item Schema

```typescript
{
  content: string;    // Imperative: "Run tests"
  activeForm: string; // Present continuous: "Running tests"
  status: "pending" | "in_progress" | "completed";
}
```

## Works With

Pairs with `hooks-todo-reminder` for automatic context injection:

```yaml
tools:
  - module: tool-todo

hooks:
  - module: hooks-todo-reminder
```

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-tool-todo)**
