# Quick Start Guide

Get started with Ralph TUI in 5 minutes.

## Prerequisites

- **Bun** >= 1.0.0 (required)
- One of the following AI coding agents:
  - [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (`claude` CLI)
  - [OpenCode](https://github.com/opencode-ai/opencode) (`opencode` CLI)

## Installation

```bash
bun install -g ralph-tui
```

## Step 1: Initialize Your Project

```bash
cd your-project
ralph-tui setup
```

The interactive wizard will:
1. Detect installed agents (Claude Code, OpenCode)
2. Create `.ralph-tui/config.toml`
3. Install bundled skills for PRD creation
4. Optionally detect existing trackers

## Step 2: Create a PRD

```bash
ralph-tui create-prd --chat
```

The AI will ask about:
- Feature goals and requirements
- Target users
- Scope (inclusions/exclusions)
- Quality gates (commands that must pass)

## Step 3: Run Ralph

```bash
ralph-tui run --prd ./prd.json
```

## Understanding the TUI

```
┌─────────────────────────────────────────────────────────────────┐
│ Ralph TUI - Iteration 3 - Task: US-002          [s] [p] [q] [?] │
├────────────────────────────────┬────────────────────────────────┤
│  TASKS                          │  OUTPUT                        │
│                                 │                                │
│  ✓ US-001 Setup project         │  Running typecheck...          │
│  → US-002 Implement auth        │  All tests passing             │
│    Blocked by: US-001           │  <promise>COMPLETE</promise>   │
│                                 │                                │
│  ○ US-003 Create UI             │                                │
│  ○ US-004 Add tests             │                                │
│                                 │                                │
├────────────────────────────────┴────────────────────────────────┤
│ [s]start [p]ause [d]ashboard [i]terations [r]efresh [q]uit      │
└─────────────────────────────────────────────────────────────────┘
```

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `s` | Start execution |
| `p` | Pause/Resume |
| `d` | Toggle progress dashboard |
| `i` | Toggle iteration history |
| `q` | Quit |
| `?` | Show help |

## Next Steps

- Read the [Configuration Guide](CONFIGURATION.md) for advanced options
- See [Integrations](INTEGRATIONS.md) for Claude Code and OpenCode setup
- Check [Troubleshooting](TROUBLESHOOTING.md) for common issues
