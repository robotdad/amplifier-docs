---
title: Amplifier - Modular AI Agent Framework
description: A modular AI agent framework with Linux kernel-inspired architecture
---

# Amplifier

<div class="hero">
<p style="font-size: 1.4rem; opacity: 0.9;">
A modular AI agent framework with Linux kernel-inspired architecture
</p>
</div>

**Amplifier** brings AI capabilities to your command line through a clean, modular architecture. Build AI-powered development workflows with swappable providers, tools, and orchestration strategies.

<div class="grid">

<div class="card">
<h3>🔌 Modular by Design</h3>
<p>Swap providers (Anthropic, OpenAI, Azure, Ollama), tools, and orchestration strategies without changing your code.</p>
</div>

<div class="card">
<h3>🐧 Kernel Philosophy</h3>
<p>Tiny, stable core (~2,600 lines) that rarely changes. All features live at the edges as replaceable modules.</p>
</div>

<div class="card">
<h3>🤖 Agent Delegation</h3>
<p>Spawn specialized sub-agents for focused tasks. Each agent has its own tools, context, and capabilities.</p>
</div>

<div class="card">
<h3>📦 Profile System</h3>
<p>Pre-configured capability sets from minimal to full-featured. Create your own profiles for repeatable workflows.</p>
</div>

</div>

## Quick Start

=== "Install"

    ```bash
    # Install with uv (recommended)
    uv tool install git+https://github.com/microsoft/amplifier@next

    # Or with pipx
    pipx install git+https://github.com/microsoft/amplifier@next
    ```

=== "Configure"

    ```bash
    # First-time setup wizard
    amplifier init

    # Or set provider directly
    export ANTHROPIC_API_KEY="your-key"
    amplifier provider use anthropic
    ```

=== "Run"

    ```bash
    # Single command
    amplifier run "Explain this codebase"

    # Interactive chat
    amplifier

    # Resume previous session
    amplifier continue
    ```

[Get Started →](getting_started/installation.md){ .md-button .md-button--primary }
[View on GitHub →](https://github.com/microsoft/amplifier){ .md-button }

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│  amplifier-core (KERNEL) - ~2,600 lines                     │
│  • Ultra-thin, stable, boring                               │
│  • Mechanisms ONLY (loading, coordinating, events)          │
│  • NEVER decides policy                                     │
└─────────────────────────────────────────────────────────────┘
                             ▲
                             │ stable contracts
                             ▼
┌─────────────────────────────────────────────────────────────┐
│  MODULES (Userspace - Swappable)                            │
│  • Providers: LLM backends (Anthropic, OpenAI, Azure, etc.) │
│  • Tools: Capabilities (filesystem, bash, web, search)      │
│  • Orchestrators: Execution loops (basic, streaming, events)│
│  • Contexts: Memory management (simple, persistent)         │
│  • Hooks: Observability (logging, approval, redaction)      │
└─────────────────────────────────────────────────────────────┘
```

The center stays still so the edges can move fast.

[Learn More →](architecture/overview.md)

## Ecosystem

Amplifier provides a rich ecosystem of swappable modules and libraries.

| Type | Examples | Purpose |
|------|----------|---------|
| **Providers** | Anthropic, OpenAI, Azure, Ollama | LLM backend integrations |
| **Tools** | Filesystem, Bash, Web, Search | Agent capabilities |
| **Orchestrators** | Basic, Streaming, Events | Execution loop strategies |
| **Contexts** | Simple, Persistent | Conversation memory |
| **Hooks** | Logging, Approval, Redaction | Observability & control |
| **Libraries** | Profiles, Collections, Config | App-layer functionality |

[Browse Ecosystem →](ecosystem/index.md){ .md-button } [Community Showcase →](showcase/index.md){ .md-button }

## Who Is This For?

<div class="grid">

<div class="card">
<h3>👩‍💻 Developers</h3>
<p>Build AI-powered development workflows. Code review, refactoring, debugging, and documentation assistance.</p>
</div>

<div class="card">
<h3>🔧 Module Authors</h3>
<p>Create custom providers, tools, or hooks. Stable contracts make modules independently developable.</p>
</div>

<div class="card">
<h3>🏢 Teams</h3>
<p>Share profiles and collections across your organization. Consistent AI workflows for everyone.</p>
</div>

</div>

## Next Steps

- **[Installation](getting_started/installation.md)** - Get Amplifier running
- **[Quickstart](getting_started/quickstart.md)** - Your first AI session
- **[CLI Reference](user_guide/cli.md)** - All available commands
- **[Architecture](architecture/overview.md)** - How it all fits together
- **[Module Development](developer/module_development.md)** - Build your own modules

## Community

- [GitHub Repository](https://github.com/microsoft/amplifier)
- [Issue Tracker](https://github.com/microsoft/amplifier/issues)
- [Contributing Guide](community/contributing.md)

---

<div style="text-align: center; opacity: 0.7; margin-top: 2rem;">
<p>Amplifier is a Microsoft open source project.</p>
</div>
