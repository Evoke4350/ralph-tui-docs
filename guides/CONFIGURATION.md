# Configuration Guide

## Configuration Layers

Ralph TUI loads configuration in order (later overrides earlier):

1. Global config: `~/.config/ralph-tui/config.toml`
2. Project config: `.ralph-tui/config.toml`
3. CLI flags (highest priority)

## Full Configuration Reference

```toml
# .ralph-tui/config.toml

# ===================================================================
# Core Settings
# ===================================================================

# Default tracker plugin: json, beads, beads-bv
tracker = "json"

# Default agent plugin: claude, opencode
agent = "claude"

# ===================================================================
# Execution Limits
# ===================================================================

# Maximum iterations (0 = unlimited)
maxIterations = 10

# Delay between iterations in milliseconds
iterationDelay = 0

# ===================================================================
# Prompt Template
# ===================================================================

# Path to custom Handlebars template (relative to project root)
# prompt_template = "./my-prompt.hbs"

# ===================================================================
# Output Directories
# ===================================================================

# Directory for iteration logs
outputDir = ".ralph-tui/iterations"

# Progress file for cross-iteration context
progressFile = ".ralph-tui/progress.md"

# ===================================================================
# Agent Options
# ===================================================================

[agentOptions]

# Model selection (agent-specific)
# Claude: sonnet, opus, haiku
# OpenCode: provider/model (e.g., openai/gpt-4o)
model = "sonnet"

# ===================================================================
# Error Handling
# ===================================================================

[errorHandling]

# Strategy when agent fails: retry, skip, abort
strategy = "skip"

# Maximum retry attempts
maxRetries = 3

# Delay between retries (milliseconds)
retryDelayMs = 5000

# Continue even if agent exits with non-zero code
continueOnNonZeroExit = false

# ===================================================================
# Subagent Tracing (Claude Code only)
# ===================================================================

# Detail level: off, minimal, moderate, full
subagentTracingDetail = "full"

# ===================================================================
# Rate Limit Handling
# ===================================================================

[rateLimitHandling]

# Enable automatic rate limit detection
enabled = true

# Fallback agents to try when rate limited
fallbackAgents = ["opencode"]

# ===================================================================
# Auto-Commit
# ===================================================================

# Automatically commit after each completed task
autoCommit = false
```

## Agent-Specific Configuration

### Claude Agent

```toml
[agentOptions]
model = "sonnet"  # haiku | sonnet | opus
```

### OpenCode Agent

```toml
[agentOptions]
model = "anthropic/claude-3-5-sonnet"  # provider/model format
# Examples:
# - openai/gpt-4o
# - google/gemini-pro
# - ollama/llama3
```

## Tracker-Specific Configuration

### JSON Tracker

No additional configuration required. Uses `prd.json` in project root.

### Beads Tracker

```bash
# Ensure bd CLI is installed
npm install -g @beads/cli

# Initialize beads in your project
bd onboard
```

### Beads-BV Tracker

```bash
# Ensure bd and bv CLIs are installed
npm install -g @beads/cli bv

# Initialize beads
bd onboard

# bv reads .beads/beads.jsonl automatically
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `RALPH_TUI_CONFIG` | Path to custom config file |
| `RALPH_TUI_HOME` | Override home directory for global config |
| `NO_COLOR` | Disable colored output |
| `CI` | Automatically enable headless mode |

## Validation

Configuration is validated on load using Zod schemas. Invalid configuration will produce an error message explaining what needs to be fixed.
