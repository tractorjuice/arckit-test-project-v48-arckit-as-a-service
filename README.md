# ArcKit as a Service

ArcKit as a Service for UK Government — a managed, multi-tenant offering of the ArcKit enterprise architecture governance toolkit, designed for UK public sector adoption (GDS Service Standard, TCoP, NCSC CAF, G-Cloud).

## Overview

This repository uses **ArcKit v4.12.3** for enterprise architecture governance and documentation.

## Getting Started

### Prerequisites

- [Claude Code](https://claude.ai/code) installed
- GitHub Codespaces (recommended) or local development environment

### Setup

1. Open this repo in a GitHub Codespace (or clone locally)
2. Claude Code will auto-install via `.devcontainer/devcontainer.json`
3. The ArcKit plugin is auto-enabled via `.claude/settings.json`
4. Restart Claude Code once to resolve the marketplace plugin

### First Commands

```bash
# Check ArcKit is working
/arckit.init

# Define architecture principles (if not already done)
/arckit.principles

# Start with stakeholder analysis
/arckit.stakeholders ArcKit as a Service

# Generate requirements
/arckit.requirements ArcKit as a Service
```

## Project Structure

```text
projects/
├── 000-global/                     # Cross-project artifacts (principles, standards)
└── 001-arckit-as-a-service/        # Project-specific artifacts (created by commands)
```

## Available Commands

This project uses the ArcKit plugin which provides 70+ slash commands for architecture governance. See the [full command reference](https://tractorjuice.github.io/arc-kit/).

## Links

- [ArcKit Documentation](https://tractorjuice.github.io/arc-kit/)
- [ArcKit Repository](https://github.com/tractorjuice/arc-kit)
- [ArcKit Plugin Marketplace](https://github.com/tractorjuice/arc-kit)
