---
title: Tools
description: Agent capabilities
---

# Tools

Tools provide capabilities that agents can invoke to interact with the environment.

## Available Tools

| Tool | Description | Repository |
|------|-------------|------------|
| **[Filesystem](filesystem.md)** | Read/write files | [GitHub](https://github.com/microsoft/amplifier-module-tool-filesystem) |
| **[Bash](bash.md)** | Execute shell commands | [GitHub](https://github.com/microsoft/amplifier-module-tool-bash) |
| **[Web](web.md)** | Fetch web content | [GitHub](https://github.com/microsoft/amplifier-module-tool-web) |
| **[Search](search.md)** | Search codebases | [GitHub](https://github.com/microsoft/amplifier-module-tool-search) |
| **[Task](task.md)** | Delegate to sub-agents | [GitHub](https://github.com/microsoft/amplifier-module-tool-task) |
| **[Todo](todo.md)** | AI self-accountability for complex tasks | [GitHub](https://github.com/microsoft/amplifier-module-tool-todo) |

<!-- MODULE_LIST_TOOL -->

## Configuration

```yaml
tools:
  - module: tool-filesystem
    config:
      allowed_paths: ["/home/user/projects"]
      read_only: false

  - module: tool-bash
    config:
      timeout: 30
      blocked_commands: ["rm -rf /"]
```

## Contract

See [Tool Contract](../../developer/contracts/tool.md) for implementation details.
