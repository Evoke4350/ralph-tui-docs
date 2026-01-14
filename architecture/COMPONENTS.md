# Component Reference

## Agent Plugins

### Claude Agent

| Property | Value |
|----------|-------|
| Name | claude |
| CLI Command | claude --print |
| Models | sonnet, opus, haiku |

### OpenCode Agent

| Property | Value |
|----------|-------|
| Name | opencode |
| CLI Command | opencode run |
| Models | 75+ provider/model combinations |

## Tracker Plugins

### JSON Tracker

Simple file-based tracker using prd.json format.

**Configuration**: None required

**File Format**:
```json
{
  "tasks": [
    {
      "id": "US-001",
      "title": "User story title",
      "status": "open",
      "priority": 1,
      "dependsOn": []
    }
  ]
}
```

### Beads Tracker

Git-backed issue tracker using the Beads CLI.

**Configuration**: Requires bd CLI

**Features**:
- Hierarchy (epics)
- Dependencies
- Labels
- Git synchronization

### Beads-BV Tracker

Beads with graph analysis via bv CLI.

**Configuration**: Requires bd and bv CLIs

**Features**:
- All Beads features
- PageRank-based task selection
- Critical path analysis
- Bottleneck detection
