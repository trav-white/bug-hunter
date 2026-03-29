# QA History Template

Use this as the header when creating `.planning/qa/HISTORY.md` for the first time.
Append one row per QA session. Never modify previous entries.

---

```markdown
# Deep QA History

Quality tracking across QA sessions. One row per session, append-only.

| Date | Branch | Stack | Mode | Runs | P0 | P1 | P2 | P3 | Found | Fixed | Remaining | Result | Regressions | Duration |
|------|--------|-------|------|------|----|----|----|----|----- |-------|-----------|--------|-------------|----------|
```

## Column Definitions

| Column | Description |
|--------|-------------|
| Date | Session date (YYYY-MM-DD) |
| Branch | Git branch name |
| Stack | Detected tech stack (abbreviated) |
| Mode | Lite / Standard / Full |
| Runs | Number of iterations |
| P0-P3 | Total issues found at each severity |
| Found | Total issues found across all runs |
| Fixed | Total issues auto-fixed |
| Remaining | Issues remaining after all runs |
| Result | PASSED / PASSED WITH NOTES / ESCALATED |
| Regressions | Count of fix-then-reappear issues |
| Duration | Total session time |

## Trend Analysis

When reviewing history, look for:
- **Rising issue counts** — code quality may be declining, consider stricter rules or earlier QA
- **Recurring categories** — if security issues appear every session, consider adding linting rules
- **Regression frequency** — frequent regressions suggest fragile code areas that need refactoring
- **Convergence speed** — if runs-to-converge is increasing, the codebase may be getting harder to QA
- **Mode escalation** — if Lite mode keeps finding issues, consider defaulting to Standard
