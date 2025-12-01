---
title: Task Tool
description: Sub-agent delegation
---

# Task Tool

Delegates tasks to specialized sub-agents.

## Module ID

`tool-task`

## How It Works

1. Agent decides to delegate a task
2. Task tool spawns a sub-session with agent configuration
3. Sub-agent executes with its own tools and context
4. Results return to parent session

## Repository

**→ [GitHub](https://github.com/microsoft/amplifier-module-tool-task)**
