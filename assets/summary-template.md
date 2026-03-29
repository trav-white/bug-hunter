# Summary Template

Use this template when creating `.planning/qa/SUMMARY.md` during Step 7.

---

```markdown
# Bug Hunter -- Expedition Report

**Safari**: [start time] -- [end time]
**Branch**: [branch]
**Habitat**: [detected stack]
**Mode**: [Lite | Standard | Full]
**Verdict**: PASSED | PASSED WITH NOTES | ESCALATED
**Runs**: [N]
**Total specimens found**: [count]
**Total specimens wrangled**: [count]
**Still at large**: [count] (with details if any)
**Protected species active**: [count]

## Quality Gate
[If --gate was used]
**Status**: PASSED | FAILED
**P0 remaining**: [count]
**P1 remaining**: [count]

## Convergence

| Run | Mode | Agents | P0 | P1 | P2 | P3 | Total | Wrangled |
|-----|------|--------|----|----|----|----|-------|----------|
| 1 | Full | 1-4,9 | X | X | X | X | X | X |
| 2 | Smart | 1,4 | X | X | X | X | X | X |
| ... | | | | | | | | |

## Test Suite
[Status after final run]
- **Result**: PASSED (X tests) | FAILED (X/Y) | Not detected
- **Failures**: [list if any]

## Regressions -- Bugs That Played Dead
[Specimens that were wrangled then escaped -- these indicate fragile fixes]
- [file:line -- description -- originally caught in Run N, escaped in Run M]

## Specimens Wrangled
[Grouped by category -- what we caught and how]

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

## Still At Large (if any)
[Specimens that got away -- couldn't auto-wrangle, needs a human]

| # | File:Line | Threat | Category | Description | Why it got away |
|---|-----------|--------|----------|-------------|-----------------|
| 1 | path:123 | P1 | security | ... | Ambiguous fix -- needs human judgement |

## Protected Species
[Specimens filtered by suppression rules]
- [X] specimens protected (see .planning/qa/suppressed.md for details)

## Test Stubs Generated
[If --generate-tests was used]
- [X] test stubs generated in [directory]
- Run `[test command]` to see TODOs

## Field Notes
[Observations from the expedition -- architectural concerns, patterns noticed, tech debt spotted. Not bugs, just things worth knowing]
- [observation]
- [observation]
```
