# Sisyphus Junior Tasks

This document contains tasks suitable for Sisyphus Junior agents to work on. Each task is self-contained with clear acceptance criteria.

## Quick Start for Agents

To work on these tasks:
1. Select a task from the list below
2. Read the full specification in [ENHANCEMENTS.md](ENHANCEMENTS.md)
3. Implement following the acceptance criteria
4. Run tests: `bun run typecheck && bun run lint`
5. Create PR with your changes

## Available Tasks

### Category: Quick Wins (1-2 hours each)

#### TASK-001: Add Task Filtering by Status

Implement `/` key to filter tasks by status in the TUI.

**Acceptance Criteria**:
- [ ] Pressing `/` opens a filter input prompt
- [ ] Can type status: "open", "in_progress", "done"
- [ ] Task list updates to show only matching tasks
- [ ] Pressing Escape clears the filter
- [ ] Filter indicator shows in header when active

**Files to modify**: `src/tui/components/TaskList.tsx`

---

#### TASK-002: Add Theme Toggle Key

Implement `Ctrl+T` to toggle between light and dark themes.

**Acceptance Criteria**:
- [ ] Pressing `Ctrl+T` toggles theme
- [ ] Theme persists across sessions
- [ ] System theme detected on first run
- [ ] No visual glitches during toggle

**Files to modify**: `src/tui/`, `src/config/`

---

#### TASK-003: Add Completion Pattern Configuration

Allow custom completion detection patterns via config.

**Acceptance Criteria**:
- [ ] Add `completionPatterns` array to config schema
- [ ] Each pattern is a regex string
- [ ] All patterns checked during execution
- [ ] First match wins
- [ ] Log which pattern matched

**Files to modify**: `src/engine/index.ts`, `src/config/`

---

### Category: Feature Additions (3-6 hours each)

#### TASK-004: GitHub Issues Tracker

Create a new tracker plugin for GitHub Issues.

**Acceptance Criteria**:
- [ ] New plugin in `src/plugins/trackers/github/`
- [ ] Reads issues from specified repo
- [ ] Updates issue status via GitHub API
- [ ] Supports `--github-repo owner/name` flag
- [ ] Handles authentication via GH_TOKEN or gh CLI
- [ ] Documentation updated

**Files to create**: `src/plugins/trackers/github/index.ts`

---

#### TASK-005: Debug Mode Implementation

Add comprehensive debug mode for troubleshooting.

**Acceptance Criteria**:
- [ ] `--debug` flag enables debug output
- [ ] Logs engine state changes
- [ ] Logs prompt content (truncated if large)
- [ ] Logs tracker operations
- [ ] Logs agent execution details
- [ ] Output timestamped and color-coded

**Files to modify**: `src/engine/`, various

---

#### TASK-006: Task Notes/Comments System

Allow adding notes to tasks in the JSON tracker.

**Acceptance Criteria**:
- [ ] Add optional `notes` field to task schema
- [ ] Notes display in task detail view
- [ ] Can add notes via TUI (press `n`)
- [ ] Notes persist to prd.json
- [ ] Notes included in agent prompt as `{{taskNotes}}`

**Files to modify**: `src/plugins/trackers/json/`, `src/tui/`

---

### Category: Quality Improvements (2-4 hours each)

#### TASK-007: Better Error Messages

Improve error messaging throughout the application.

**Acceptance Criteria**:
- [ ] Each error includes actionable next steps
- [ ] Error messages are consistent in tone
- [ ] Common errors have specific messages
- [ ] Error codes documented
- [ ] Warnings distinguishable from errors

**Files to modify**: Various, focus on `src/engine/`, `src/plugins/`

---

#### TASK-008: Input Validation Improvements

Add validation for all user inputs.

**Acceptance Criteria**:
- [ ] Config validation on load
- [ ] PRD validation before run
- [ ] Task ID format validation
- [ ] File path validation
- [ ] Clear error messages for invalid inputs

**Files to modify**: `src/config/`, `src/prd/`, `src/plugins/`

---

#### TASK-009: Documentation Examples

Add practical examples throughout documentation.

**Acceptance Criteria**:
- [ ] Each config option has example
- [ ] Each command has usage example
- [ ] Integration guide has complete walkthrough
- [ ] Troubleshooting guide has real scenarios
- [ ] API reference has code samples

**Files to modify**: `docs/`, `README.md`

---

### Category: Performance (3-5 hours each)

#### TASK-010: Output Panel Optimization

Optimize the output panel for large outputs.

**Acceptance Criteria**:
- [ ] Implement virtual scrolling
- [ ] Only render visible lines
- [ ] Maintain scroll position during updates
- [ ] Add `maxOutputLines` config option (default 1000)
- [ ] Old lines trimmed when limit exceeded
- [ ] Performance measured: <100ms for 10k lines

**Files to modify**: `src/tui/components/OutputPanel.tsx`

---

#### TASK-011: Lazy Tracker Loading

Defer tracker plugin loading until needed.

**Acceptance Criteria**:
- [ ] Trackers loaded on first use
- [ ] Startup time reduced by >30%
- [ ] Loading indicator in TUI
- [ ] Error handling for load failures
- [ ] Tracker registry caches loaded plugins

**Files to modify**: `src/plugins/trackers/`

---

#### TASK-012: Prompt Caching

Cache rendered prompts when task hasn't changed.

**Acceptance Criteria**:
- [ ] Calculate hash of task + template + variables
- [ ] Cache rendered prompts by hash
- [ ] Reuse cached prompt when hash matches
- [ ] Cache invalidated on task change
- [ ] Log cache hits/misses
- [ ] Config option to disable caching

**Files to modify**: `src/engine/`, `src/templates/`

---

## Task Selection Guidelines

### For New Agents

Start with Quick Wins (TASK-001 through TASK-003).

### For Experienced Agents

Feature Additions (TASK-004 through TASK-006) or Quality Improvements (TASK-007 through TASK-009).

### For Advanced Agents

Performance tasks (TASK-010 through TASK-012) require deeper understanding of the codebase.

## Claiming Tasks

To claim a task:
1. Create an issue with the task number (e.g., "TASK-001: Add Task Filtering")
2. Assign yourself to the issue
3. Reference the issue in your PR

## Task Completion Checklist

Before submitting:
- [ ] All acceptance criteria met
- [ ] `bun run typecheck` passes
- [ ] `bun run lint` passes
- [ ] Tests added (if applicable)
- [ ] Documentation updated
- [ ] PR description references task number
