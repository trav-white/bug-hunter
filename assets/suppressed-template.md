# Suppressed Issues Template

Use this as the template when creating `.planning/qa/suppressed.md` for the first time.

---

```markdown
# Bug Hunter -- Protected Species

Specimens listed here are intentionally excluded from hunt reports. Some bugs are features, mate. Each protection has an expiry date -- after expiry, the specimen will be reported again as a reminder to revisit.

To protect a specimen: ask Claude to suppress a specific issue after a hunt, or add a row manually.
To revoke protection: delete the row or set the expiry to a past date.

## Active Protections

| File | Line | Category | Description Pattern | Reason | Protected By | Date | Expiry |
|------|------|----------|-------------------|--------|--------------|------|--------|
| src/legacy/old.ts | 45 | security | hardcoded API key | Pre-existing -- file scheduled for removal in Phase 4 | Trav | 2026-03-15 | 2026-06-15 |

## Matching Rules

- **File**: Exact match or glob pattern (e.g. `src/legacy/**`)
- **Line**: Exact line number, or `*` to match any line in the file
- **Category**: Must match exactly (build, security, design, code, deps, migration, a11y)
- **Description Pattern**: Substring match against the specimen description (case-insensitive)
- **Expiry**: Date after which the protection lapses (YYYY-MM-DD). Default: 90 days from protection date.

## Expired Protections

[Move rows here when they expire, for historical reference]

| File | Line | Category | Description Pattern | Reason | Protected By | Date | Expired |
|------|------|----------|-------------------|--------|--------------|------|---------|
```
