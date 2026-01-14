# Architecture Documentation

## System Overview

Ralph TUI is built as a modular CLI application using Bun, OpenTUI for the terminal interface, and React for component composition.

## Core Components

### CLI Layer (src/cli.tsx, src/commands/)

The CLI layer handles:
- Command parsing and routing
- Configuration loading and validation
- Template management
- User interaction prompts

### Execution Engine (src/engine/)

The heart of Ralph TUI that orchestrates the autonomous loop:

| Component | Responsibility |
|-----------|---------------|
| index.ts | Main loop orchestration, task selection, iteration management |
| rate-limit-detector.ts | Detects API rate limits from agent output |
| types.ts | Engine type definitions and interfaces |

### Plugin System (src/plugins/)

Modular plugins for extensibility:

| Type | Path | Purpose |
|------|------|---------|
| Agents | src/plugins/agents/ | AI CLI integrations (Claude, OpenCode) |
| Trackers | src/plugins/trackers/ | Task management (JSON, Beads, Beads-BV) |

### Presentation Layer (src/tui/)

Terminal UI built with OpenTUI and React:
- Task list panel
- Iteration output panel
- Progress dashboard
- Settings modal

## Technologies

| Component | Technology |
|-----------|------------|
| Runtime | Bun |
| CLI Framework | Commander-style (custom) |
| TUI Framework | OpenTUI |
| UI Components | React |
| Templating | Handlebars |
| Config Format | TOML |
| Validation | Zod |
