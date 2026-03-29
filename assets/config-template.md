# Project QA Config Template

Copy this to `.planning/qa/config.md` in your project and customise. Bug Hunter reads this file during session setup and applies overrides to all agents.

---

```markdown
# Bug Hunter — Project Configuration

## Defaults

Override default flags for this project. These apply when the flag isn't explicitly passed.

| Setting | Value |
|---------|-------|
| scope | all |
| fix | true |
| format | markdown |
| max-runs | 5 |
| mode | auto |
| generate-tests | false |
| gate | false |

## Severity Overrides

Reclassify minimum severity for specific categories in this project.
Format: `category -> minimum severity`

| Category | Minimum Severity | Reason |
|----------|-----------------|--------|
| a11y | P1 | Accessibility-critical project — WCAG AA required |
| security | P0 | All security findings are blockers |

## Excluded Paths

Directories and files that QA should skip entirely. Glob patterns supported.

| Pattern | Reason |
|---------|--------|
| src/legacy/** | Known tech debt — scheduled for rewrite |
| **/*.test.ts | Test files — not production code |
| scripts/** | Build/deploy scripts — out of QA scope |

## Custom Rules

Additional checks for built-in agents to include. Keyed by agent category.

### build
- Verify `npm run lint` passes in addition to build
- Check that no `console.error` calls were added

### security
- All API routes must check `x-api-key` header
- No external HTTP calls from server-side code (data comes from DB only)

### code
- All database queries must go through the repository pattern
- Components must use the project's `<Card>` wrapper, not raw divs

### design
- All colours must use CSS variables from `globals.css`
- Spacing must use the 4px grid (multiples of 0.25rem)

## Custom Agents

Define additional domain-specific QA agents. These run alongside the built-in agents.

### Agent: data-freshness
**Wave**: 1
**Scope**: src/cron/**, src/lib/sync/**
**Condition**: Always (when scope files are in diff)
**Prompt**: |
  You are a data freshness verification agent. In [project directory]:

  Check all cron sync jobs in the changed files:
  1. Every sync job must have a staleness check (max age before alert)
  2. Every sync job must have error handling that notifies (not just logs)
  3. Sync intervals must match the data source's rate limits
  4. No sync job should fetch more than 90 days of historical data

  Write findings to .planning/qa/agents/data-freshness-run-[N].md

### Agent: [name]
**Wave**: [1 or 2]
**Scope**: [glob pattern]
**Condition**: [Always | If specific condition]
**Prompt**: |
  [Full agent prompt]
```
