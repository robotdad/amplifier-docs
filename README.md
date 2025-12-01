# Amplifier Documentation

Documentation site for Amplifier, built with MkDocs and Material theme.

## Quick Start

```bash
cd amplifier-docs

# Install dependencies (no project build needed)
uv sync --no-install-project

# Serve locally (auto-reload)
uv run mkdocs serve

# Build static site
uv run mkdocs build
```

The docs site will be available at http://127.0.0.1:8000

## Development

The documentation uses:
- **MkDocs** with **Material** theme
- **mkdocstrings** for API documentation from docstrings
- **mkdocs-awesome-nav** for navigation structure
- Custom hooks for module catalog generation

## Structure

```
amplifier-docs/
├── docs/                    # Documentation source
│   ├── index.md            # Landing page
│   ├── getting_started/    # Installation, quickstart
│   ├── user_guide/         # CLI, profiles, agents
│   ├── architecture/       # Kernel, modules, events
│   ├── modules/            # Module catalog
│   ├── libraries/          # Supporting libraries
│   ├── developer/          # Module development
│   ├── api/                # API reference
│   └── community/          # Contributing, roadmap
├── mkdocs.yaml             # MkDocs configuration
└── pyproject.toml          # Dependencies
```

## Deployment

Configure Read the Docs with `.readthedocs.yaml` or deploy to any static hosting.
