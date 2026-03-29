# History Template

Use this as the header when creating `.planning/qa/HISTORY.md` for the first time.
Append one row per safari. Never modify previous entries.

---

```markdown
# Bug Hunter -- Safari Log

Quality tracking across expeditions. One row per safari, append-only.

| Date | Branch | Habitat | Mode | Runs | P0 | P1 | P2 | P3 | Found | Wrangled | At Large | Verdict | Escapes | Duration |
|------|--------|---------|------|------|----|----|----|----|----- |----------|----------|---------|---------|----------|
```

## Column Definitions

| Column | Description |
|--------|-------------|
| Date | Safari date (YYYY-MM-DD) |
| Branch | Git branch name |
| Habitat | Detected tech stack (abbreviated) |
| Mode | Lite / Standard / Full |
| Runs | Number of iterations |
| P0-P3 | Total specimens found at each threat level |
| Found | Total specimens found across all runs |
| Wrangled | Total specimens auto-fixed |
| At Large | Specimens remaining after all runs |
| Verdict | PASSED / PASSED WITH NOTES / ESCALATED |
| Escapes | Count of wrangled-then-escaped specimens (regressions) |
| Duration | Total safari time |

## Trend Analysis

When reviewing the safari log, look for:
- **Rising specimen counts** -- the habitat may be getting wilder. Consider stricter rules or earlier hunts
- **Recurring categories** -- if security specimens appear every safari, add linting rules to catch them earlier
- **Escape frequency** -- frequent escapes suggest fragile code areas that need refactoring
- **Convergence speed** -- if runs-to-converge is increasing, the habitat may be getting harder to clear
- **Mode escalation** -- if Lite mode keeps finding specimens, consider defaulting to Standard
