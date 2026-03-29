---
name: error-journal
description: Automatically logs errors when Claude Code executes bash commands. Builds a searchable knowledge base of mistakes and lessons learned. Trigger keywords: error, log, mistake, bug, remember, lesson, error journal.
---

# Error Journal

## Overview

This skill helps Claude Code automatically log errors encountered during bash command execution, building a searchable knowledge base of mistakes and lessons learned to prevents repeated errors.

## When to Use

1. **Auto-trigger**: When a bash command fails (returns non-zero exit code)
2. **Manual trigger**: When user says "log this error", "remember this", "note this mistake"
3. **Post-resolution**: After fixing a problem, log the solution and lessons learned

## Error Log Location

```
~/.claude/skills/error-journal/references/error-log.md
```

## Record Format

```markdown
## [#1] Brief Title

| Field | Content |
|-------|---------|
| **Date** | YYYY-MM-DD HH:MM |
| **Command** | `the command executed` |
| **Error** | Error message summary |
| **Context** | What task was you doing |
| **Root Cause** | Why it happened |
| **Solution** | How it was fixed |
| **Lesson** | How to avoid in the future |

---
```

## Workflow

```
┌─────────────────┐
│ Bash Error      │
└────────┬────────┘
         │
         ▼
   ┌─────────┐     ┌─────────────────┐
   │ Failed?  ├────►│ Log to error-journal │
   └─────────┘     └─────────────────┘
         │                    │
         ▼                    ▼
    Continue              Search history on future
```

## Usage Examples

### Example 1: Auto Log on Deployment Error
```
[Claude runs command]
ssh root@server "docker-compose up -d"

[Error]
Error: port 80 already in use

[Claude auto-logs]
## #1 Docker Port Conflict

| Field | Content |
|-------|---------|
| **Date** | 2024-01-15 14:30 |
| **Command** | `docker-compose up -d` |
| **Error** | port 80 already in use |
| **Context** | Deploying to production server |
| **Root Cause** | Another service using port 80 |
| **Solution** | Stop conflicting service or change port |
| **Lesson** | Check port usage before deployment: `lsof -i :80` |
---
```

### Example 2: Manual Log on npm Error
```
User: Remember this - npm install needs --legacy-peer-deps

[Claude logs]
## #2 npm Peer Dependency Conflict

| Field | Content |
|-------|---------|
| **Date** | 2024-01-15 15:00 |
| **Command** | `npm install` |
| **Error** | peer dependency conflict |
| **Context** | Installing project dependencies |
| **Root Cause** | npm 7+ strict peer dep checking |
| **Solution** | Use `npm install --legacy-peer-deps` |
| **Lesson** | When encountering peer dep conflicts, try --legacy-peer-deps first |

---
```

### Example 3: Query History
```
User: Have we seen port conflicts before?

[Claude searches log]
Found #1 Docker Port Conflict, shows details...
```

## Best Practices

1. **Log immediately**: Record errors right they memory is fresh
2. **Keep complete**: After fixing, go back and fill in "Solution" and "Lesson"
3. **Be concise**: Summarize error messages, no full stack traces needed
4. **Search-friendly**: Use searchable keywords in titles and lessons

## Anti-Patterns (Avoid)
- Logging too much detail, making the log bloated
- Recording without supplementing, missing solutions
- Logging trivial errors that don't matter
