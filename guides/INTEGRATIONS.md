# Integration Guide

## Claude Code Integration

### Installation

```bash
# Install Claude Code CLI
npm install -g @anthropic-ai/claude-code

# Authenticate
claude auth login
```

### Configuration

```toml
# .ralph-tui/config.toml
agent = "claude"

[agentOptions]
model = "sonnet"  # haiku | sonnet | opus
```

### Features

| Feature | Supported |
|---------|-----------|
| Streaming output | Yes |
| Subagent tracing | Yes |
| Rate limit detection | Yes |
| Fallback agents | Yes |

## OpenCode Integration

### Installation

```bash
# Install OpenCode CLI
npm install -g opencode

# Configure provider
opencode config
```

### Configuration

```toml
# .ralph-tui/config.toml
agent = "opencode"

[agentOptions]
model = "anthropic/claude-3-5-sonnet"
```

### Model Selection

OpenCode supports 75+ providers. Format: `provider/model`

| Provider | Example Models |
|----------|---------------|
| anthropic | claude-3-5-sonnet, claude-3-opus |
| openai | gpt-4o, gpt-4-turbo |
| google | gemini-pro, gemini-1.5-pro |
| xai | grok-1 |
| ollama | llama3, codellama |

## Beads Integration

### Installation

```bash
npm install -g @beads/cli bd
```

### Setup

```bash
# Initialize beads in your project
cd your-project
bd onboard

# Create an epic
bd create --type epic --title "My Feature"

# Add tasks to the epic
bd create --type task --epic <epic-id> --title "First task"
```

### Running Ralph

```bash
# Run with an epic
ralph-tui run --epic <epic-id>

# Or use beads-bv for intelligent task selection
ralph-tui run --tracker beads-bv --epic <epic-id>
```

## CI/CD Integration

### Status Check

```bash
# Check if session is complete (exits 0 if done)
ralph-tui status --json
```

### GitHub Actions Example

```yaml
name: Ralph Automation
on:
  push:
    branches: [main]

jobs:
  ralph:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: oven-sh/setup-bun@v1
        with:
          bun-version: latest
      - run: bun install -g ralph-tui
      - run: ralph-tui run --prd ./prd.json --headless --iterations 5
```

## MCP Integration

Ralph TUI can work with MCP (Model Context Protocol) servers configured in your agent.

### Claude Code MCP Setup

```bash
# Add MCP server to Claude Code config
claude mcp add <server-name>
```

The agent will have access to MCP tools during execution.
