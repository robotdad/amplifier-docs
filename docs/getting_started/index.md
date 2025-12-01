---
title: Getting Started
description: Get up and running with Amplifier in minutes
---

# Getting Started

Welcome to Amplifier! This section will help you get up and running quickly.

## What You'll Learn

1. **[Installation](installation.md)** - Install Amplifier and its dependencies
2. **[Quickstart](quickstart.md)** - Run your first AI session in 5 minutes
3. **[Provider Setup](providers.md)** - Configure your LLM provider (Anthropic, OpenAI, etc.)

## Prerequisites

- **Python 3.11+** - Amplifier requires Python 3.11 or later
- **uv** (recommended) or **pipx** - For isolated tool installation
- **API Key** - From your chosen LLM provider

## Quick Overview

```bash
# Install
uv tool install git+https://github.com/microsoft/amplifier@next

# Configure provider
export ANTHROPIC_API_KEY="your-key"
amplifier provider use anthropic

# Run
amplifier run "Hello, what can you help me with?"
```

That's it! You're ready to use Amplifier.

## Next Steps

After completing the getting started guide, explore:

- **[User Guide](../user_guide/index.md)** - Detailed usage documentation
- **[Profiles](../user_guide/profiles.md)** - Pre-configured capability sets
- **[Agents](../user_guide/agents.md)** - Specialized sub-agents for focused tasks
