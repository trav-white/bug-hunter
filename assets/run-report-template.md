# Run Report Template

Use this template when creating `.planning/qa/RUN-[N].md` during Step 4.

---

```markdown
# Deep QA — Run [N]

**Timestamp**: [YYYY-MM-DD HH:MM AEST]
**Branch**: [branch]
**Mode**: [Lite | Standard | Full | Smart re-test]
**Agents dispatched**: [list which agents ran]
**Duration**: [time taken]
**Suppressions filtered**: [count]

## Summary

| Severity | Count | Fixed | Remaining |
|----------|-------|-------|-----------|
| P0 Blockers | [count] | [count] | [count] |
| P1 Critical | [count] | [count] | [count] |
| P2 Medium | [count] | [count] | [count] |
| P3 Low (report only) | [count] | — | [count] |
| **Total** | **[count]** | **[count]** | **[count]** |

## Regressions
[If any issues reappeared from previous runs]

| # | File:Line | Category | Originally | Fixed In | Reappeared | Status |
|---|-----------|----------|-----------|----------|------------|--------|
| 1 | path:123 | security | P2 | Run 1 | Run 2 | ESCALATED TO P0 |

## Test Suite Results
[PASSED (X tests) | FAILED — list failures | Not detected]

## Issues

### P0 — Blockers
| # | File:Line | Category | Agent | Description | Fix | Status |
|---|-----------|----------|-------|-------------|-----|--------|
| 1 | path:123 | build | build | ... | ... | FIXED / ESCALATED |

### P1 — Critical
| # | File:Line | Category | Agent | Description | Fix | Status |
|---|-----------|----------|-------|-------------|-----|--------|
| 1 | path:123 | security | security | ... | ... | FIXED / ESCALATED |

### P2 — Medium
| # | File:Line | Category | Agent | Description | Fix | Status |
|---|-----------|----------|-------|-------------|-----|--------|
| 1 | path:123 | code | quality | ... | ... | FIXED / SKIPPED |

### P3 — Low (report only)
| # | File:Line | Category | Agent | Description | Suggested Fix |
|---|-----------|----------|-------|-------------|---------------|
| 1 | path:123 | code | quality | ... | ... |

## Test Stubs Generated
[If --generate-tests was enabled]

| # | Test File | Covers | Stub Type |
|---|-----------|--------|-----------|
| 1 | __tests__/path.test.ts | src/path.ts:functionName | Unit test |

## Fixes Applied
[Detailed list of changes made during auto-fix]

| # | File:Line | Change Description | Verified |
|---|-----------|-------------------|----------|
| 1 | path:123 | Parameterized SQL query | Build passed |

## Agent Output Files
- Build: .planning/qa/agents/build-run-[N].md
- Security: .planning/qa/agents/security-run-[N].md
- [list all agent files that were written]
```
