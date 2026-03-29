# Session Template

Use this template when creating `.planning/qa/SESSION.md` during Step 0.10.

---

```markdown
# Safari Mission Briefing

**Expedition started**: [timestamp -- YYYY-MM-DD HH:MM AEST]
**Branch**: [branch name]
**Git base**: [BASE commit short hash]
**Stack**: [detected stack profile -- e.g. "Next.js 14 + React + TypeScript + Drizzle ORM"]
**Mode**: [Lite | Standard | Full]
**Scope**: [all | specific layers]
**Territory**: [count] files ([list or "see below"])
**Blast radius**: [count]
**Routes to test**: [list]
**Existing tests**: [PASSED (X tests) | FAILED (X/Y) | Not detected]
**Project config**: [Loaded from .planning/qa/config.md | Not found -- using defaults]
**Protected species**: [X active suppressions loaded | None]
**Current run**: 1
**Status**: HUNTING

## Gear Check
- Playwright: [available | NOT AVAILABLE -- Wave 2 UI agents will be skipped]
- Dev server: [running on :3000 | running on :8000 | NOT RUNNING]
- SSH (remote): [available | not needed | NOT AVAILABLE]

## Hunting Ground
[List of all files in scope, grouped by category:]

### Direct targets
- path/to/file.ts
- path/to/file.ts

### Blast radius (imports/exports)
- path/to/file.ts
- path/to/file.ts

### Excluded (from config)
- path/to/excluded.ts (reason: [from config])

## Hunting Party
| # | Agent | Wave | Status |
|---|-------|------|--------|
| 1 | Build & Tests | 1 | STANDING BY |
| 2 | Security & Auth | 1 | STANDING BY |
| ... | ... | ... | ... |

## Safari Log
[Updated after each run -- see Step 6]

### Run 1
- **Started**: [timestamp]
- **Agents deployed**: [list]
- **Specimens**: P0: X, P1: X, P2: X, P3: X
- **Wrangled**: [count]
- **Still at large**: [count]
- **Duration**: [time]

### Run 2 (if needed)
- **Started**: [timestamp]
- **Mode**: Smart re-test
- **Agents redeployed**: [list -- subset of Run 1]
- **Specimens**: P0: X, P1: X, P2: X, P3: X
- **Wrangled**: [count]
- **Still at large**: [count]
- **Duration**: [time]

## Regression Map
[Tracked across runs -- see Step 6]

| Specimen Key | First Seen | Wrangled In | Escaped In | Status |
|-------------|-----------|------------|------------|--------|
| file:line:category | Run 1 | Run 1 | -- | CAUGHT |
```
