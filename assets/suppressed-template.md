# Suppressed Issues Template

Use this as the template when creating `.planning/qa/suppressed.md` for the first time.

---

```markdown
# Deep QA — Suppressed Issues

Issues listed here are intentionally excluded from QA reports. Each suppression has an expiry date — after expiry, the issue will be reported again as a reminder to revisit.

To add a suppression: ask Claude to suppress a specific issue after a QA run, or add a row manually.
To remove a suppression: delete the row or set the expiry to a past date.

## Active Suppressions

| File | Line | Category | Description Pattern | Reason | Suppressed By | Date | Expiry |
|------|------|----------|-------------------|--------|---------------|------|--------|
| src/legacy/old.ts | 45 | security | hardcoded API key | Pre-existing — file scheduled for removal in Phase 4 | Trav | 2026-03-15 | 2026-06-15 |

## Matching Rules

- **File**: Exact match or glob pattern (e.g. `src/legacy/**`)
- **Line**: Exact line number, or `*` to match any line in the file
- **Category**: Must match exactly (build, security, design, code, deps, migration, a11y)
- **Description Pattern**: Substring match against the issue description (case-insensitive)
- **Expiry**: Date after which the suppression is ignored (YYYY-MM-DD). Default: 90 days from suppression date.

## Expired Suppressions

[Move rows here when they expire, for historical reference]

| File | Line | Category | Description Pattern | Reason | Suppressed By | Date | Expired |
|------|------|----------|-------------------|--------|---------------|------|---------|
```
