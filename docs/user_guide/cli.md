---
title: CLI Reference
description: Complete reference for Amplifier CLI commands
---

# CLI Reference

Complete reference for all Amplifier command-line commands.

## Global Options

```bash
amplifier [OPTIONS] COMMAND [ARGS]
```

| Option | Description |
|--------|-------------|
| `--version` | Show version and exit |
| `--help` | Show help and exit |
| `--install-completion` | Install shell completion |
| `--show-completion` | Show shell completion script |

## Core Commands

### `run`

Execute a single prompt.

```bash
amplifier run [OPTIONS] PROMPT
```

| Option | Description |
|--------|-------------|
| `--profile, -p` | Profile to use |
| `--provider` | LLM provider (anthropic, openai, etc.) |
| `--model, -m` | Specific model to use |
| `--max-tokens` | Maximum response tokens |
| `--output-format, -o` | Output format: `text`, `json`, `json-trace` |
| `--resume, -r` | Resume session by ID |
| `--no-tools` | Disable tool use |

**Examples:**

```bash
# Basic usage
amplifier run "Explain this code"

# With options
amplifier run --profile dev --model claude-opus-4-1 "Complex task"

# JSON output for scripting
amplifier run --output-format json "What is 2+2?"

# Resume a session
amplifier run --resume abc123 "Continue from where we left off"
```

### `continue`

Resume the most recent session.

```bash
amplifier continue [PROMPT]
```

**Examples:**

```bash
# Resume with a new message
amplifier continue "Now add error handling"

# Just resume interactively
amplifier continue
```

### Interactive Mode

Start without a command for interactive chat:

```bash
amplifier
```

#### Interactive Commands

| Command | Description |
|---------|-------------|
| `/help` | Show available commands |
| `/tools` | List available tools |
| `/agents` | List available agents |
| `/status` | Show session status |
| `/clear` | Clear conversation history |
| `/think` | Enable planning mode |
| `/quit`, `/exit` | Exit interactive mode |

#### Using Agents

```bash
amplifier> @explorer Analyze this codebase
amplifier> @bug-hunter Find issues in main.py
```

#### Using Mentions

Reference files or context:

```bash
amplifier> Review @src/main.py for issues
amplifier> @project:context/standards.md Apply these standards
```

## Session Commands

### `session list`

List recent sessions.

```bash
amplifier session list [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--limit, -n` | Number of sessions to show (default: 10) |
| `--all` | Show all sessions |

### `session show`

Show session details.

```bash
amplifier session show SESSION_ID
```

### `session resume`

Resume a specific session.

```bash
amplifier session resume SESSION_ID [PROMPT]
```

### `session delete`

Delete a session.

```bash
amplifier session delete SESSION_ID
```

### `session cleanup`

Clean up old sessions.

```bash
amplifier session cleanup [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--days, -d` | Delete sessions older than N days (default: 30) |

## Profile Commands

### `profile list`

List available profiles.

```bash
amplifier profile list
```

### `profile use`

Set the active profile.

```bash
amplifier profile use PROFILE_NAME
```

### `profile show`

Show profile configuration.

```bash
amplifier profile show [PROFILE_NAME]
```

### `profile current`

Show the current active profile.

```bash
amplifier profile current
```

### `profile default`

Show or set the default profile.

```bash
amplifier profile default [PROFILE_NAME]
```

### `profile reset`

Reset profile to default.

```bash
amplifier profile reset
```

## Provider Commands

### `provider list`

List available providers.

```bash
amplifier provider list
```

### `provider use`

Set the active provider.

```bash
amplifier provider use PROVIDER_NAME
```

### `provider current`

Show the current provider.

```bash
amplifier provider current
```

### `provider reset`

Reset to default provider.

```bash
amplifier provider reset
```

## Module Commands

### `module list`

List configured modules.

```bash
amplifier module list [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--type, -t` | Filter by type (provider, tool, hook, etc.) |

### `module add`

Add a module.

```bash
amplifier module add MODULE_NAME [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--source, -s` | Module source (git URL or path) |

### `module remove`

Remove a module.

```bash
amplifier module remove MODULE_NAME
```

### `module show`

Show module details.

```bash
amplifier module show MODULE_NAME
```

### `module check-updates`

Check for module updates.

```bash
amplifier module check-updates
```

### `module refresh`

Refresh module cache.

```bash
amplifier module refresh
```

## Collection Commands

### `collection list`

List installed collections.

```bash
amplifier collection list
```

### `collection add`

Add a collection.

```bash
amplifier collection add COLLECTION_NAME [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--source, -s` | Collection source (git URL) |

### `collection remove`

Remove a collection.

```bash
amplifier collection remove COLLECTION_NAME
```

### `collection show`

Show collection details.

```bash
amplifier collection show COLLECTION_NAME
```

### `collection refresh`

Refresh collection cache.

```bash
amplifier collection refresh
```

## Source Commands

### `source list`

List module source overrides.

```bash
amplifier source list
```

### `source add`

Add a source override (for local development).

```bash
amplifier source add MODULE_NAME SOURCE_PATH
```

### `source remove`

Remove a source override.

```bash
amplifier source remove MODULE_NAME
```

### `source show`

Show source override details.

```bash
amplifier source show MODULE_NAME
```

## Tool Commands

### `tool list`

List available tools from the active profile.

```bash
amplifier tool list
```

### `tool info`

Show tool details.

```bash
amplifier tool info TOOL_NAME
```

### `tool invoke`

Directly invoke a tool (for testing).

```bash
amplifier tool invoke TOOL_NAME [ARGS]
```

## Agent Commands

### `agents list`

List available agents.

```bash
amplifier agents list
```

### `agents show`

Show agent details.

```bash
amplifier agents show AGENT_NAME
```

## Other Commands

### `init`

Run first-time setup wizard.

```bash
amplifier init
```

### `update`

Update Amplifier and modules.

```bash
amplifier update [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--cli` | Update CLI only |
| `--modules` | Update modules only |
| `--collections` | Update collections only |

## Output Formats

The `--output-format` option supports:

### `text` (default)

Human-readable markdown output rendered in the terminal.

### `json`

Structured JSON for automation:

```json
{
  "status": "success",
  "response": "The answer is...",
  "session_id": "abc123",
  "model": "claude-sonnet-4-5",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### `json-trace`

Complete execution trace including tool calls:

```json
{
  "status": "success",
  "response": "...",
  "trace": [
    {"type": "tool_call", "tool": "bash", "input": {...}, "output": {...}},
    {"type": "llm_response", "content": "..."}
  ]
}
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_API_KEY` | Anthropic API key |
| `OPENAI_API_KEY` | OpenAI API key |
| `AZURE_OPENAI_API_KEY` | Azure OpenAI API key |
| `AZURE_OPENAI_ENDPOINT` | Azure OpenAI endpoint |
| `AMPLIFIER_PROFILE` | Default profile |
| `AMPLIFIER_PROVIDER` | Default provider |
| `AMPLIFIER_DEBUG` | Enable debug logging |

## Configuration Files

| File | Scope | Purpose |
|------|-------|---------|
| `~/.amplifier/settings.yaml` | User | Global user settings |
| `.amplifier/settings.yaml` | Project | Project settings (committed) |
| `.amplifier/settings.local.yaml` | Local | Machine-local settings (gitignored) |

## See Also

- [Profiles](profiles.md) - Profile configuration
- [Sessions](sessions.md) - Session management
- [Agents](agents.md) - Agent delegation
