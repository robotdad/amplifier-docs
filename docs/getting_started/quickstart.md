---
title: Quickstart
description: Your first AI session with Amplifier
---

# Quickstart

Get your first AI session running in under 5 minutes.

## Prerequisites

- Amplifier installed ([Installation Guide](installation.md))
- API key configured ([Provider Setup](providers.md))

## Your First Command

Run a simple query:

```bash
amplifier run "What is the capital of France?"
```

You should see the AI response streamed to your terminal.

## Interactive Mode

Start an interactive chat session:

```bash
amplifier
```

This opens a REPL where you can have a back-and-forth conversation:

```
amplifier> What programming languages do you know?
[AI responds...]

amplifier> Can you write a Python function to sort a list?
[AI responds with code...]

amplifier> /help
[Shows available commands...]

amplifier> /quit
```

### Interactive Commands

| Command | Description |
|---------|-------------|
| `/help` | Show available commands |
| `/tools` | List available tools |
| `/agents` | List available agents |
| `/status` | Show session information |
| `/clear` | Clear conversation history |
| `/quit` or `/exit` | Exit interactive mode |

## Working with Code

Amplifier excels at code-related tasks. Try it in a project directory:

```bash
cd your-project

# Explain the codebase
amplifier run "Explain the structure of this project"

# Find bugs
amplifier run "Review main.py for potential issues"

# Generate code
amplifier run "Write a unit test for the User class"
```

## Using Tools

With the `dev` profile, Amplifier has access to powerful tools:

```bash
# Use the dev profile (includes filesystem, bash, search tools)
amplifier run --profile dev "List all Python files in this directory"
```

The AI can now:

- Read and write files
- Execute shell commands
- Search the codebase
- Browse the web

## Session Management

### Resume a Session

Continue your most recent conversation:

```bash
amplifier continue "Now add error handling to that function"
```

### List Sessions

View your recent sessions:

```bash
amplifier session list
```

### Resume a Specific Session

```bash
amplifier session resume abc123
```

## Using Profiles

Profiles are pre-configured capability sets:

```bash
# List available profiles
amplifier profile list

# Use a specific profile
amplifier run --profile dev "Analyze this codebase"

# Set default profile
amplifier profile use dev
```

| Profile | Description |
|---------|-------------|
| `foundation` | Minimal - just LLM access |
| `base` | Basic tools (filesystem, bash) |
| `dev` | Full development (tools + agents + search) |
| `test` | Testing focused |
| `full` | All features enabled |

## Using Agents

Agents are specialized assistants for specific tasks:

```bash
# List available agents
amplifier agents list

# Use an agent (in interactive mode)
amplifier
amplifier> @explorer What is the architecture of this project?
amplifier> @bug-hunter Find issues in auth.py
```

| Agent | Purpose |
|-------|---------|
| `explorer` | Breadth-first codebase exploration |
| `bug-hunter` | Systematic debugging |
| `zen-architect` | System design with simplicity focus |
| `researcher` | Research and synthesis |

## Output Formats

For automation, use JSON output:

```bash
# JSON output
amplifier run --output-format json "What is 2+2?"

# Pipe to other tools
amplifier run --output-format json "Analyze this" | jq '.response'
```

## Next Steps

You've completed the quickstart! Continue learning:

- [CLI Reference](../user_guide/cli.md) - All available commands
- [Profiles](../user_guide/profiles.md) - Configure capability sets
- [Agents](../user_guide/agents.md) - Specialized sub-agents
- [Sessions](../user_guide/sessions.md) - Session management
- [Architecture](../architecture/overview.md) - How it all works
