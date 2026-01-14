# API Reference

## CLI Commands

### ralph-tui run

Start Ralph execution.

```bash
ralph-tui run [options]
```

**Options**:

| Option | Type | Description |
|--------|------|-------------|
| --prd | string | PRD file path |
| --epic | string | Epic ID for beads tracker |
| --agent | string | Agent plugin name |
| --model | string | Model override |
| --tracker | string | Tracker plugin name |
| --iterations | number | Maximum iterations (0 = unlimited) |
| --headless | boolean | Run without TUI |

### ralph-tui resume

Resume an interrupted session.

```bash
ralph-tui resume [options]
```

**Options**:

| Option | Type | Description |
|--------|------|-------------|
| --cwd | string | Working directory |
| --headless | boolean | Run without TUI |
| --force | boolean | Override stale lock |

### ralph-tui status

Check session status (headless mode).

```bash
ralph-tui status [options]
```

**Options**:

| Option | Type | Description |
|--------|------|-------------|
| --json | boolean | Output in JSON format |
| --cwd | string | Working directory |

**Returns**:
- Exit code 0: Session active
- Exit code 1: No session
- Exit code 2: Session complete

### ralph-tui logs

View iteration logs.

```bash
ralph-tui logs [options]
```

**Options**:

| Option | Type | Description |
|--------|------|-------------|
| --iteration | number | View specific iteration |
| --task | string | View logs for specific task |
| --clean | boolean | Clean up old logs |
| --keep | number | Number of logs to keep |
| --verbose | boolean | Show full output |

## Configuration API

### Config File Structure

```toml
# .ralph-tui/config.toml

# Core settings
tracker = "json"
agent = "claude"

# Execution limits
maxIterations = 10
iterationDelay = 0

# Prompt template
prompt_template = "./my-prompt.hbs"

# Output
outputDir = ".ralph-tui/iterations"
progressFile = ".ralph-tui/progress.md"

# Agent options
[agentOptions]
model = "sonnet"

# Error handling
[errorHandling]
strategy = "skip"  # retry | skip | abort
maxRetries = 3
retryDelayMs = 5000
continueOnNonZeroExit = false

# Subagent tracing
subagentTracingDetail = "full"  # off | minimal | moderate | full

# Rate limit handling
[rateLimitHandling]
enabled = true
fallbackAgents = ["opencode"]
```

## Template Variables

### Available Variables

| Variable | Description |
|----------|-------------|
| {{taskId}} | Task identifier |
| {{taskTitle}} | Task title |
| {{taskDescription}} | Task description |
| {{taskAcceptanceCriteria}} | Acceptance criteria |
| {{taskDependencies}} | Task dependencies |
| {{recentProgress}} | Last 5 iterations of progress |
| {{iteration}} | Current iteration number |

### Example Template

```handlebars
Task: {{taskId}} - {{taskTitle}}

Description:
{{taskDescription}}

Acceptance Criteria:
{{taskAcceptanceCriteria}}

Recent Progress:
{{recentProgress}}

Work on this task until complete. Output <promise>COMPLETE</promise> when done.
```
