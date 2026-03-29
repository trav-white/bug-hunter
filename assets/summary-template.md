# Summary Template

Use this template when creating `.planning/qa/SUMMARY.md` during Step 7.

---

```markdown
# Deep QA Summary

**Session**: [start time] — [end time]
**Branch**: [branch]
**Stack**: [detected stack]
**Mode**: [Lite | Standard | Full]
**Result**: PASSED | PASSED WITH NOTES | ESCALATED
**Iterations**: [N]
**Total issues found**: [count]
**Total issues fixed**: [count]
**Remaining**: [count] (with details if any)
**Suppressions active**: [count]

## Quality Gate
[If --gate was used]
**Status**: PASSED | FAILED
**P0 remaining**: [count]
**P1 remaining**: [count]

## Convergence

| Run | Mode | Agents | P0 | P1 | P2 | P3 | Total | Fixed |
|-----|------|--------|----|----|----|----|-------|-------|
| 1 | Full | 1-4,9 | X | X | X | X | X | X |
| 2 | Smart | 1,4 | X | X | X | X | X | X |
| ... | | | | | | | | |

## Test Suite
[Status after final run]
- **Result**: PASSED (X tests) | FAILED (X/Y) | Not detected
- **Failures**: [list if any]

## Regressions Detected
[Issues that were fixed then reappeared — these indicate fragile fixes]
- [file:line — description — originally fixed in Run N, reappeared in Run M]

## Issues Resolved
[Grouped by category — brief description of each fix]

### Build
- [description]

### Security
- [description]

### Code Quality
- [description]

### Dependencies
- [description]

### Migrations
- [description]

## Remaining Issues (if any)
[Issues that couldn't be auto-fixed with explanation]

| # | File:Line | Severity | Category | Description | Why not fixed |
|---|-----------|----------|----------|-------------|---------------|
| 1 | path:123 | P1 | security | ... | Ambiguous fix — needs human decision |

## Suppressed Issues
[Count of issues filtered by suppression rules]
- [X] issues suppressed (see .planning/qa/suppressed.md for details)

## Test Stubs Generated
[If --generate-tests was used]
- [X] test stubs generated in [directory]
- Run `[test command]` to see TODOs

## Recommendations
[Architectural concerns, tech debt, or patterns noticed during QA — not issues, but observations]
- [observation]
- [observation]
```
