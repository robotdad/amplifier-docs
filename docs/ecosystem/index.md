---
title: Ecosystem
description: Amplifier modules and libraries
---

# Ecosystem

Amplifier's modular architecture provides a rich ecosystem of components you can mix and match.

---

## Runtime Modules

Modules are loaded dynamically at runtime based on your profile configuration. They extend the kernel with capabilities.

<div class="grid cards" markdown>

-   :material-cloud-outline: **[Providers](../modules/providers/index.md)**

    ---

    Connect to AI model providers like Anthropic, OpenAI, Azure, and Ollama.

-   :material-tools: **[Tools](../modules/tools/index.md)**

    ---

    Extend agent capabilities with filesystem, bash, web, search, and task delegation.

-   :material-play-circle-outline: **[Orchestrators](../modules/orchestrators/index.md)**

    ---

    Control execution loops: basic, streaming, or event-driven.

-   :material-memory: **[Contexts](../modules/contexts/index.md)**

    ---

    Manage conversation state with in-memory or persistent storage.

-   :material-hook: **[Hooks](../modules/hooks/index.md)**

    ---

    Observe, guide, and control agent behavior with logging, approval, and more.

</div>

---

## Libraries

Libraries are used by applications (like the CLI) to provide higher-level functionality. They are **not** used by runtime modules.

| Library | Description | Repository |
|---------|-------------|------------|
| **[amplifier-profiles](../libraries/profiles.md)** | Profile and agent loading with inheritance | [GitHub](https://github.com/microsoft/amplifier-profiles) |
| **[amplifier-collections](../libraries/collections.md)** | Collection discovery and management | [GitHub](https://github.com/microsoft/amplifier-collections) |
| **[amplifier-config](../libraries/config.md)** | Three-scope configuration management | [GitHub](https://github.com/microsoft/amplifier-config) |
| **[amplifier-module-resolution](../libraries/module_resolution.md)** | Module source resolution | [GitHub](https://github.com/microsoft/amplifier-module-resolution) |

!!! info "Architectural Boundary"
    Libraries are consumed by applications. Runtime modules only depend on `amplifier-core` and never use libraries directly.

---

## Quick Reference

**Total Official Components**: 30+

| Category | Count | Examples |
|----------|-------|----------|
| Providers | 6 | Anthropic, OpenAI, Azure, Ollama, vLLM, Mock |
| Tools | 6 | Filesystem, Bash, Web, Search, Task, Todo |
| Orchestrators | 3 | Basic, Streaming, Events |
| Contexts | 2 | Simple, Persistent |
| Hooks | 9 | Logging, Approval, Redaction, Backup, Streaming UI, Schedulers, etc. |
| Libraries | 4 | Profiles, Collections, Config, Module Resolution |
| Collections | 4 | Toolkit, Design Intelligence, Recipes, Issues |

---

## Using Modules

Modules are specified in profiles:

```yaml
# ~/.amplifier/profiles/my-profile.md
---
profile:
  name: my-profile
  extends: base

tools:
  - module: tool-web
    source: git+https://github.com/microsoft/amplifier-module-tool-web@main
---
```

Or managed via CLI:

```bash
# List installed modules
amplifier module list

# Show module details
amplifier module show tool-filesystem
```

See the [User Guide](../user_guide/profiles.md) for complete profile documentation.
