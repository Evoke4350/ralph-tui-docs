# Ralph TUI Documentation

AI Agent Loop Orchestrator - A terminal UI for orchestrating AI coding agents to work through task lists autonomously.

[![npm version](https://img.shields.io/npm/v/ralph-tui.svg)](https://www.npmjs.com/package/ralph-tui)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Built with Bun](https://img.shields.io/badge/Built%20with-Bun-f9f1e1.svg)](https://bun.sh)

## Overview

Ralph TUI connects your AI coding assistant (Claude Code, OpenCode) to your task tracker (prd.json, Beads) and runs them in an autonomous loop, completing tasks one-by-one with intelligent selection, error handling, and full visibility into what's happening.

### Key Features

- **Autonomous Loop**: Selects tasks, builds prompts, runs agents, and detects completion automatically
- **Multi-Agent Support**: Claude Code, OpenCode with fallback agent configuration for rate limit handling
- **Multi-Tracker Support**: JSON (prd.json), Beads, and Beads-BV with graph-aware task selection
- **Session Persistence**: Pause anytime, resume later, survive crashes
- **Subagent Tracing**: Visualize nested agent execution (when using Claude Code with structured output)
- **Rate Limit Handling**: Automatic retry with exponential backoff and agent fallback
- **Interactive TUI**: Real-time progress monitoring with keyboard controls

## Quick Start

### 5-Minute Quickstart (JSON Mode)

```bash
# 1. Install
bun install -g ralph-tui

# 2. Setup (creates config, installs skills)
cd your-project
ralph-tui setup

# 3. Create a PRD for your feature
ralph-tui create-prd --chat

# 4. Run Ralph!
ralph-tui run --prd ./prd.json
```

### Alternative: With Beads Tracker

```bash
# Run with an epic
ralph-tui run --epic my-project-epic
```

## Documentation

- **[Architecture Documentation](architecture/ARCHITECTURE.md)** - Complete system architecture
- **[Component Reference](architecture/COMPONENTS.md)** - All components and their interactions
- **[API Reference](api/API_REFERENCE.md)** - Complete API documentation
- **[Quick Start Guide](guides/QUICKSTART.md)** - Getting started guide
- **[Configuration Guide](guides/CONFIGURATION.md)** - Configuration reference
- **[Integrations Guide](guides/INTEGRATIONS.md)** - Integration guides for Claude Code, OpenCode, etc.
- **[Troubleshooting Guide](guides/TROUBLESHOOTING.md)** - Common issues and solutions
- **[International Resources](community-international/INTERNATIONAL_RESOURCES.md)** - Korean, Chinese, Japanese, Vietnamese resources
- **[Disclaimer](DISCLAIMER.md)** - Project disclaimer

## How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   ┌──────────────┐     ┌──────────────┐     ┌──────────────┐   │
│   │  1. SELECT   │────▶│  2. BUILD    │────▶│  3. EXECUTE  │   │
│   │    TASK      │     │    PROMPT    │     │    AGENT     │   │
│   └──────────────┘     └──────────────┘     └──────────────┘   │
│          ▲                                         │            │
│          │                                         ▼            │
│   ┌──────────────┐                         ┌──────────────┐    │
│   │  5. NEXT     │◀────────────────────────│  4. DETECT   │    │
│   │    TASK      │                         │  COMPLETION  │    │
│   └──────────────┘                         └──────────────┘    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### The Execution Loop

1. **Select Task**: Choose highest-priority task with no unresolved dependencies
2. **Build Prompt**: Render Handlebars template with task context and recent progress
3. **Execute Agent**: Run AI agent with the prompt
4. **Detect Completion**: Parse output for `<promise>COMPLETE</promise>` token
5. **Update Tracker**: Mark task complete and proceed to next task

### Key Concepts

| Concept | Description |
|---------|-------------|
| **Task Tracker** | Where your tasks live (prd.json user stories, Beads issues) |
| **Agent Plugin** | The AI CLI that does the work (Claude Code, OpenCode) |
| **Prompt Template** | Handlebars template that turns task data into agent prompts |
| **Completion Token** | `<promise>COMPLETE</promise>` signals task completion |
| **Session Persistence** | State saved to `.ralph-tui-session.json` for crash recovery |

## Installation

### Prerequisites

- **Bun** >= 1.0.0 (required - Ralph TUI uses OpenTUI which requires Bun)
- One of these AI coding agents:
  - [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (`claude` CLI)
  - [OpenCode](https://github.com/opencode-ai/opencode) (`opencode` CLI)

### Install

```bash
# Install globally with Bun
bun install -g ralph-tui

# Or run directly without installing
bunx ralph-tui
```

## CLI Commands

| Command | Description |
|---------|-------------|
| `ralph-tui` | Launch the interactive TUI |
| `ralph-tui run [options]` | Start Ralph execution |
| `ralph-tui resume [options]` | Resume an interrupted session |
| `ralph-tui status [options]` | Check session status (headless, for CI/scripts) |
| `ralph-tui logs [options]` | View/manage iteration output logs |
| `ralph-tui setup` | Run interactive project setup (alias: `init`) |
| `ralph-tui create-prd [options]` | Create a new PRD interactively (alias: `prime`) |
| `ralph-tui convert [options]` | Convert PRD markdown to JSON format |
| `ralph-tui config show` | Display merged configuration |
| `ralph-tui template show` | Display current prompt template |
| `ralph-tui plugins agents` | List available agent plugins |
| `ralph-tui plugins trackers` | List available tracker plugins |
| `ralph-tui help` | Show help message |

## TUI Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `s` | Start execution |
| `p` | Pause/Resume execution |
| `d` | Toggle progress dashboard |
| `i` | Toggle iteration history view |
| `v` | Toggle tasks/iterations view |
| `h` | Toggle showing closed tasks |
| `l` | Load/switch epic |
| `u` | Toggle subagent tracing panel |
| `t` | Cycle subagent tracing detail level |
| `T` (Shift+T) | Toggle subagent tree panel |
| `,` | Open settings |
| `r` | Refresh task list |
| `j` / `k` or `↑` / `↓` | Move selection up/down |
| `Enter` | Drill into task/iteration details |
| `Escape` | Back (from detail views) / Quit (from task list) |
| `q` | Quit |
| `?` | Show help overlay |
| `Ctrl+C` | Interrupt current agent (with confirmation) |
| `Ctrl+C` x2 | Force quit immediately |

## Configuration

Ralph TUI uses TOML configuration files with layered overrides:

1. **Global config**: `~/.config/ralph-tui/config.toml`
2. **Project config**: `.ralph-tui/config.toml` (in project root)
3. **CLI flags**: Override everything

### Example Configuration

```toml
# .ralph-tui/config.toml

# Default tracker and agent
tracker = "json"
agent = "claude"

# Execution limits
maxIterations = 10

# Agent-specific options
[agentOptions]
model = "sonnet"

# Error handling
[errorHandling]
strategy = "skip"        # retry | skip | abort
maxRetries = 3
retryDelayMs = 5000
continueOnNonZeroExit = false

# Subagent tracing detail level
# off | minimal | moderate | full
subagentTracingDetail = "full"
```

## Agent & Tracker Plugins

### Built-in Agents

| Plugin | CLI Command | Description |
|--------|-------------|-------------|
| `claude` | `claude --print` | Claude Code CLI with streaming output |
| `opencode` | `opencode run` | OpenCode CLI |

### Built-in Trackers

| Plugin | Description | Features |
|--------|-------------|----------|
| `json` | prd.json file-based tracker | Simple JSON format, no external tools |
| `beads` | Beads issue tracker via `bd` CLI | Hierarchy, dependencies, labels |
| `beads-bv` | Beads + `bv` graph analysis | Intelligent selection via PageRank, critical path |

### Plugin Comparison

| Feature | json | beads | beads-bv |
|---------|------|-------|----------|
| External CLI | None | `bd` | `bd` + `bv` |
| Dependencies | Yes | Yes | Yes |
| Priority ordering | Yes | Yes | Yes |
| Hierarchy (epics) | No | Yes | Yes |
| Graph analysis | No | No | Yes |
| Sync with git | No | Yes | Yes |
| Setup complexity | Lowest | Medium | Highest |

## License

MIT License - see [LICENSE](https://github.com/subsy/ralph-tui/blob/main/LICENSE) for details.

## Repository

GitHub: https://github.com/subsy/ralph-tui
