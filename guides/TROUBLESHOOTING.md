# Troubleshooting Guide

## Common Issues

### "No tasks available"

**Symptoms**: Ralph starts but immediately reports no tasks to work on.

**Solutions**:

1. Check your prd.json has tasks:
   ```bash
   cat prd.json | jq '.tasks[] | select(.status == "open")'
   ```

2. Verify tasks aren't blocked:
   ```bash
   cat prd.json | jq '.tasks[] | select(.dependsOn | length > 0)'
   ```

3. For Beads, check epic has open tasks:
   ```bash
   bd list --epic <your-epic-id>
   ```

### "Agent not found"

**Symptoms**: Error that agent CLI cannot be found.

**Solutions**:

1. Verify agent is installed:
   ```bash
   which claude  # or: which opencode
   ```

2. Check agent is in PATH:
   ```bash
   echo $PATH | tr ':' '\n' | grep -i claude
   ```

3. Reinstall agent if needed:
   ```bash
   npm install -g @anthropic-ai/claude-code
   # or
   npm install -g opencode
   ```

### "Session lock exists"

**Symptoms**: Error about existing session lock.

**Solutions**:

1. Check if another Ralph instance is running:
   ```bash
   ps aux | grep ralph-tui
   ```

2. If no other instance, force resume:
   ```bash
   ralph-tui resume --force
   ```

3. Manually remove lock (last resort):
   ```bash
   rm .ralph-tui-session-lock.json
   ```

### "Task stuck in_progress"

**Symptoms**: Task marked as in_progress but Ralph crashed.

**Solutions**:

1. Resume will auto-reset stale tasks:
   ```bash
   ralph-tui resume
   ```

2. For Beads, manually reset:
   ```bash
   bd update <task-id> --status open
   ```

3. For JSON tracker, edit prd.json:
   ```bash
   # Change status from "in_progress" to "open"
   ```

### Rate Limit Issues

**Symptoms**: Agent reports rate limits, Ralph stops or retries excessively.

**Solutions**:

1. Enable fallback agents:
   ```toml
   [rateLimitHandling]
   enabled = true
   fallbackAgents = ["opencode"]
   ```

2. Adjust retry settings:
   ```toml
   [errorHandling]
   strategy = "retry"
   maxRetries = 5
   retryDelayMs = 10000  # 10 seconds
   ```

3. Use a cheaper model for subtasks:
   ```toml
   [agentOptions]
   model = "haiku"  # Faster, cheaper
   ```

### High Token Costs

**Symptoms**: Unexpected API costs.

**Solutions**:

1. Set iteration limits:
   ```bash
   ralph-tui run --iterations 5 --prd ./prd.json
   ```

2. Use cheaper models where possible:
   ```toml
   [agentOptions]
   model = "haiku"  # or opencode with free models
   ```

3. Enable prompt caching (if supported by agent):
   ```toml
   # Configure in agent settings
   ```

### Agent Output Not Streaming

**Symptoms**: No real-time output in TUI.

**Solutions**:

1. Check agent supports streaming:
   ```bash
   # Claude Code requires --print flag
   claude --print "test"
   ```

2. Verify subagent tracing isn't filtering:
   ```toml
   subagentTracingDetail = "full"
   ```

3. Check for buffer issues with pipe:
   ```bash
   # Some shells buffer; try with unbuffer
   unbuffer ralph-tui run --prd ./prd.json
   ```

## Debug Mode

Enable verbose output:

```bash
# Set environment variable
RALPH_TUI_DEBUG=1 ralph-tui run --prd ./prd.json

# Or check iteration logs
ralph-tui logs --iteration 1 --verbose
```

## Getting Help

- GitHub Issues: https://github.com/subsy/ralph-tui/issues
- Documentation: https://github.com/subsy/ralph-tui
