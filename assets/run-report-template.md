# Run Report Template

Use this template when creating `.planning/qa/RUN-[N].md` during Step 4.

---

```markdown
# Bug Hunter -- Hunt Log [N]

**Timestamp**: [YYYY-MM-DD HH:MM AEST]
**Branch**: [branch]
**Mode**: [Lite | Standard | Full | Smart re-test]
**Agents deployed**: [list which agents ran]
**Duration**: [time taken]
**Protected species filtered**: [count]

## Haul Summary

| Threat Level | Found | Wrangled | At Large |
|-------------|-------|----------|----------|
| P0 -- Habitat On Fire | [count] | [count] | [count] |
| P1 -- Gonna Leave a Mark | [count] | [count] | [count] |
| P2 -- Rough Around the Edges | [count] | [count] | [count] |
| P3 -- She'll Be Right (report only) | [count] | -- | [count] |
| **Total** | **[count]** | **[count]** | **[count]** |

## Regressions -- Bugs That Played Dead
[If any specimens escaped from previous runs]

| # | File:Line | Category | Original Threat | Caught In | Escaped In | Status |
|---|-----------|----------|----------------|----------|------------|--------|
| 1 | path:123 | security | P2 | Run 1 | Run 2 | ESCALATED TO P0 |

## Test Suite Results
[PASSED (X tests) | FAILED -- list failures | Not detected]

## Specimens

### P0 -- Habitat On Fire
| # | File:Line | Category | Agent | Description | Fix | Status |
|---|-----------|----------|-------|-------------|-----|--------|
| 1 | path:123 | build | build | ... | ... | CAUGHT / ESCALATED |

### P1 -- Gonna Leave a Mark
| # | File:Line | Category | Agent | Description | Fix | Status |
|---|-----------|----------|-------|-------------|-----|--------|
| 1 | path:123 | security | security | ... | ... | CAUGHT / ESCALATED |

### P2 -- Rough Around the Edges
| # | File:Line | Category | Agent | Description | Fix | Status |
|---|-----------|----------|-------|-------------|-----|--------|
| 1 | path:123 | code | quality | ... | ... | CAUGHT / SKIPPED |

### P3 -- She'll Be Right (report only)
| # | File:Line | Category | Agent | Description | Suggested Fix |
|---|-----------|----------|-------|-------------|---------------|
| 1 | path:123 | code | quality | ... | ... |

## Test Stubs Generated
[If --generate-tests was enabled]

| # | Test File | Covers | Stub Type |
|---|-----------|--------|-----------|
| 1 | __tests__/path.test.ts | src/path.ts:functionName | Unit test |

## Wrangling Log
[Detailed list of fixes applied during this run]

| # | File:Line | What Changed | Verified |
|---|-----------|-------------|----------|
| 1 | path:123 | Parameterized SQL query | Build passed |

## Agent Reports
- Build: .planning/qa/agents/build-run-[N].md
- Security: .planning/qa/agents/security-run-[N].md
- [list all agent files that were written]
```
