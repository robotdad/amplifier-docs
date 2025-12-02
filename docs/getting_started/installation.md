---
title: Installation
description: Install Amplifier on your system
---

# Installation

Amplifier can be installed as a standalone CLI tool or as a Python package for development.

## Quick Install (Recommended)

### Using uv

[uv](https://docs.astral.sh/uv/) is the recommended way to install Amplifier:

```bash
uv tool install git+https://github.com/microsoft/amplifier@next
```

### Using pipx

Alternatively, use [pipx](https://pipx.pypa.io/):

```bash
pipx install git+https://github.com/microsoft/amplifier@next
```

### Verify Installation

```bash
amplifier --version
```

## First-Time Setup

Run the setup wizard to configure your provider and preferences:

```bash
amplifier init
```

This will:

1. Prompt you to select an LLM provider (Anthropic, OpenAI, Azure, Ollama)
2. Configure your API key securely
3. Set up shell completion (optional)

## Manual Configuration

If you prefer manual setup:

### 1. Set Your API Key

=== "Anthropic"

    ```bash
    export ANTHROPIC_API_KEY="your-api-key"
    ```

=== "OpenAI"

    ```bash
    export OPENAI_API_KEY="your-api-key"
    ```

=== "Azure OpenAI"

    ```bash
    export AZURE_OPENAI_API_KEY="your-api-key"
    export AZURE_OPENAI_ENDPOINT="https://your-resource.openai.azure.com"
    ```

=== "Ollama"

    ```bash
    # Ollama runs locally, no API key needed
    # Just ensure Ollama is running: ollama serve
    ```

### 2. Select Your Provider

```bash
amplifier provider use anthropic  # or openai, azure, ollama
```

### 3. Verify Setup

```bash
amplifier run "Hello! Are you working?"
```

## Shell Completion

Enable tab completion for your shell:

```bash
amplifier --install-completion
```

Supports bash, zsh, fish, and PowerShell.

## Updating

Update to the latest version:

```bash
amplifier update
```

Or reinstall:

```bash
uv tool install --force git+https://github.com/microsoft/amplifier@next
```

## Development Installation

For contributors or those who want to modify Amplifier:

```bash
# Clone the repository (next branch)
git clone -b next https://github.com/microsoft/amplifier.git
cd amplifier

# Install in development mode
uv pip install -e .
```

See [Local Development](../developer/local_development.md) for more details.

## Troubleshooting

### "Command not found: amplifier"

Ensure your tool bin directory is in PATH:

```bash
# For uv
export PATH="$HOME/.local/bin:$PATH"

# For pipx
export PATH="$HOME/.local/bin:$PATH"
```

Add this to your shell profile (`.bashrc`, `.zshrc`, etc.).

### "No API key found"

Make sure your API key environment variable is set:

```bash
echo $ANTHROPIC_API_KEY  # Should show your key
```

Or run `amplifier init` to configure it.

### "Module not found" errors

Try reinstalling with a clean state:

```bash
uv tool uninstall amplifier
uv tool install git+https://github.com/microsoft/amplifier@next
```

## Next Steps

- [Quickstart →](quickstart.md) - Run your first AI session
- [Provider Setup →](providers.md) - Configure your LLM provider
