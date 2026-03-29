# QA Session Template

Use this template when creating `.planning/qa/SESSION.md` during Step 0.10.

---

```markdown
# QA Session

**Started**: [timestamp — YYYY-MM-DD HH:MM AEST]
**Branch**: [branch name]
**Git base**: [BASE commit short hash]
**Stack**: [detected stack profile — e.g. "Next.js 14 + React + TypeScript + Drizzle ORM"]
**Mode**: [Lite | Standard | Full]
**Scope**: [all | specific layers]
**Changed files**: [count] ([list or "see below"])
**Blast radius**: [count]
**Routes to test**: [list]
**Existing tests**: [PASSED (X tests) | FAILED (X/Y) | Not detected]
**Project config**: [Loaded from .planning/qa/config.md | Not found — using defaults]
**Suppressions**: [X active suppressions loaded | None]
**Current run**: 1
**Status**: IN PROGRESS

## Pre-flight
- Playwright: [available | NOT AVAILABLE — Wave 2 UI agents will be skipped]
- Dev server: [running on :3000 | running on :8000 | NOT RUNNING]
- SSH (remote): [available | not needed | NOT AVAILABLE]

## Scoped Files
[List of all files in scope, grouped by category:]

### Changed (direct)
- path/to/file.ts
- path/to/file.ts

### Blast Radius (imports/exports)
- path/to/file.ts
- path/to/file.ts

### Excluded (from config)
- path/to/excluded.ts (reason: [from config])

## Agents Selected
| # | Agent | Wave | Status |
|---|-------|------|--------|
| 1 | Build & Tests | 1 | PENDING |
| 2 | Security & Auth | 1 | PENDING |
| ... | ... | ... | ... |

## Run Log
[Updated after each run — see Step 6]

### Run 1
- **Started**: [timestamp]
- **Agents dispatched**: [list]
- **Results**: P0: X, P1: X, P2: X, P3: X
- **Fixed**: [count]
- **Remaining**: [count]
- **Duration**: [time]

### Run 2 (if needed)
- **Started**: [timestamp]
- **Mode**: Smart re-test
- **Agents dispatched**: [list — subset of Run 1]
- **Results**: P0: X, P1: X, P2: X, P3: X
- **Fixed**: [count]
- **Remaining**: [count]
- **Duration**: [time]

## Regression Map
[Tracked across runs — see Step 6]

| Issue Key | First Seen | Fixed In | Reappeared In | Status |
|-----------|-----------|----------|---------------|--------|
| file:line:category | Run 1 | Run 1 | — | FIXED |
```
