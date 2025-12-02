---
title: Local Development
description: Setting up a local development environment
---

# Local Development

This guide covers setting up a development environment for working on Amplifier itself or developing modules locally.

## Prerequisites

- **Python 3.11+**
- **uv** - Fast Python package manager
- **Git** - Version control

### Install uv

```bash
# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## Development Setup

### Clone the Repository

```bash
# Clone amplifier (next branch)
git clone -b next https://github.com/microsoft/amplifier.git
cd amplifier
```

### Install Dependencies

```bash
# Install all packages in development mode
make install
```

This installs:

- `amplifier-core`
- `amplifier-app-cli`
- All supporting libraries
- All modules

### Verify Installation

```bash
# Check amplifier works
amplifier --version

# Run a test
amplifier run "Hello, world!"
```

## Repository Structure

```
amplifier/
├── amplifier_app_cli/            # CLI application
├── data/                         # Profiles and default data
├── tests/                        # Test suite
└── pyproject.toml                # Package configuration
```

Related repositories:

- [amplifier-core](https://github.com/microsoft/amplifier-core) - Kernel
- [amplifier-profiles](https://github.com/microsoft/amplifier-profiles) - Profiles library
- [amplifier-collections](https://github.com/microsoft/amplifier-collections) - Collections library
- [amplifier-module-*](https://github.com/microsoft?q=amplifier-module) - Module packages

## Working on a Module

### 1. Navigate to Module

```bash
cd amplifier-module-tool-filesystem
```

### 2. Make Changes

Edit the code in `amplifier_module_tool_filesystem/`.

### 3. Test Changes Immediately

Changes to Python files are reflected immediately (editable install).

```bash
# From amplifier root
amplifier run --profile dev "List files in current directory"
```

### 4. Run Module Tests

```bash
cd amplifier-module-tool-filesystem
uv run pytest
```

## Working on Core

### 1. Navigate to Core

```bash
cd amplifier-core
```

### 2. Make Changes

Edit the code in `amplifier_core/`.

### 3. Run Tests

```bash
uv run pytest
```

### 4. Test Integration

```bash
# From amplifier root
amplifier run "Test prompt"
```

## Source Overrides

For testing changes to modules without modifying the profile:

### Via Settings

Create `.amplifier/settings.local.yaml`:

```yaml
module_sources:
  provider-anthropic: file:///path/to/your/provider-anthropic
  tool-filesystem: file:///path/to/your/tool-filesystem
```

### Via Environment

```bash
export AMPLIFIER_MODULE_SOURCE_TOOL_FILESYSTEM="file://$(pwd)/amplifier-module-tool-filesystem"
```

### Via CLI

```bash
amplifier source add tool-filesystem file://$(pwd)/amplifier-module-tool-filesystem
```

## Debugging

### Enable Debug Logging

```bash
export AMPLIFIER_DEBUG=1
amplifier run "Test"
```

### View Session Logs

```bash
# Find recent session
ls -lt ~/.amplifier/projects/*/sessions/*/events.jsonl | head -1

# View events
cat ~/.amplifier/projects/*/sessions/<session-id>/events.jsonl | jq
```

### Debug Specific Events

```bash
# LLM requests
grep '"event":"llm:request"' events.jsonl | jq

# Tool executions
grep '"event":"tool:post"' events.jsonl | jq
```

## Testing

### Run All Tests

```bash
# From amplifier root
make test
```

### Run Specific Module Tests

```bash
cd amplifier-module-tool-bash
uv run pytest -v
```

### Run with Coverage

```bash
uv run pytest --cov=amplifier_core --cov-report=html
```

## Common Workflows

### Adding a New Module

1. Create module directory
2. Create `pyproject.toml` with entry point
3. Implement `mount` function
4. Add tests
5. Add to `.amplifier/settings.local.yaml` for testing

### Modifying a Contract

1. Update contract documentation in `amplifier-core/docs/contracts/`
2. Update protocol in `amplifier-core/amplifier_core/interfaces.py`
3. Update existing modules to match
4. Run all tests

### Testing Profile Changes

1. Edit profile in `amplifier-app-cli/data/profiles/`
2. Test with:
   ```bash
   amplifier profile show dev --resolved
   amplifier run --profile dev "Test"
   ```

## Git Workflow

### Submodule Awareness

Each `amplifier-*` directory is a separate git repo. Be mindful when making changes:

```bash
# Check which repo you're in
git remote -v

# Check submodule status
git submodule status
```

### Making Changes

```bash
# Make changes in a submodule
cd amplifier-module-tool-bash
git checkout -b my-feature
# ... make changes ...
git add .
git commit -m "My changes"

# Update parent repo's submodule pointer
cd ..
git add amplifier-module-tool-bash
git commit -m "Update tool-bash submodule"
```

## Verification Tests

Before submitting changes:

```bash
# Quick verification
cd dev_verification
SKIP_GITHUB_TEST=1 ./run_all_tests.sh

# Full verification
./run_all_tests.sh
```

## Troubleshooting

### "Module not found"

```bash
# Check module is installed
amplifier module list

# Check source override
amplifier source list

# Reinstall
cd amplifier
make install
```

### "Import error"

Ensure editable installs are up to date:

```bash
cd amplifier
uv pip install -e amplifier-core
uv pip install -e amplifier-app-cli
```

### "Submodule issues"

Reset submodules:

```bash
git submodule update --init --recursive --force
```

## References

- **→ [Local Development Guide](https://github.com/microsoft/amplifier/blob/next/docs/LOCAL_DEVELOPMENT.md)** - Detailed guide
