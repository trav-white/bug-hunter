# Severity Guide — P0 through P3

Reference for consistent severity classification across all agents. When in doubt, consult this guide.

---

## P0 — Blocker

**Definition**: The application cannot build, crashes, has a security hole exploitable without authentication, or loses/corrupts data.

**Response**: Must be fixed before any other work. Auto-fix immediately. If fix is uncertain, escalate to user as P0.

**Examples**:
- Build fails (`npm run build` exits non-zero)
- Type error that prevents compilation
- Hardcoded API key / secret / password in source code
- SQL injection via unsanitised user input
- XSS via `dangerouslySetInnerHTML` with user-controlled content
- Auth bypass — route/endpoint accessible without authentication that should be protected
- DROP TABLE / DROP COLUMN in migration without explicit safety acknowledgement
- Credentials staged for git commit (.env, .json with tokens)
- Regression — an issue that was fixed in a previous run has reappeared
- Unhandled exception that crashes the server/app

**NOT P0** (common misclassifications):
- Missing loading state (P1-P2)
- Unused import (P3)
- Missing alt text (P2)
- Outdated dependency without known exploit (P3)

---

## P1 — Critical

**Definition**: A feature is broken, a runtime error occurs under normal usage, or a security issue requires authentication to exploit.

**Response**: Must be fixed in this QA session. Auto-fix.

**Examples**:
- Runtime error on a common user path (null reference, undefined property)
- API endpoint returns wrong data shape (component crashes or shows wrong info)
- Form submission doesn't work or loses data
- Navigation leads to 404 / blank page
- Auth token stored insecurely (localStorage for sensitive tokens)
- Missing CSRF protection on state-changing endpoints
- N+1 query on a page that loads lists (performance degradation at scale)
- Data loss risk in migration (column rename, type narrowing)
- Missing rollback/down migration
- CRITICAL/HIGH CVE in a dependency with a fix available
- Missing error handling on user-facing operations (submit, save, delete)
- Empty catch block that silently swallows errors

**NOT P1**:
- Slight visual misalignment (P2)
- Missing memoisation on non-critical component (P2-P3)
- Deprecated function that still works (P2-P3)

---

## P2 — Medium

**Definition**: Poor user experience, code smell, performance concern, or accessibility gap. The feature works but is degraded.

**Response**: Fix if time permits in this session. Auto-fix unless ambiguous.

**Examples**:
- Missing loading state (spinner, skeleton) during data fetch
- Missing empty state ("No results found" message)
- Content overflow / horizontal scroll at a breakpoint
- Colour contrast below WCAG AA threshold
- Missing keyboard focus indicator
- Unused variable / dead code introduced in this diff
- Console.log / debug statement left in production code
- Missing input validation (non-security — e.g. email format)
- Index missing on foreign key column
- MODERATE CVE in a dependency
- Build warning introduced in changed files
- Missing alt text on informative images
- Prop drilling > 3 levels deep
- Large component that should be split

**NOT P2**:
- Code style preference with no UX impact (P3)
- Perfectly functional code that could be slightly more elegant (P3)

---

## P3 — Low

**Definition**: Minor convention violation, style issue, or improvement opportunity. No user impact.

**Response**: **Never auto-fix.** Report only. User decides.

**Examples**:
- Import ordering doesn't match project convention
- Variable naming doesn't match project style
- Missing JSDoc / docstring on a public function
- TODO comment without ticket reference
- Slightly verbose code that could be simplified
- LOW CVE in a dependency
- Deprecated function used (still works, no security risk)
- Minor heading order skip (h2 to h4)
- Missing aria-label on a button that has visible text
- Type assertion that could be narrowed
- Magic number that could be a named constant

---

## Severity Override Rules

Projects can override default severity via `.planning/qa/config.md`. Common overrides:

| Override | Effect |
|----------|--------|
| `a11y -> P1` | All accessibility issues treated as P1 (accessibility-critical projects) |
| `security -> P0` | All security issues treated as P0 (high-security projects) |
| `design -> P1` | All design violations treated as P1 (design-system-strict projects) |
| `deps -> P2` | All dependency issues capped at P2 (when upgrades are deferred) |

When an override is active, it sets the **minimum** severity for that category. An issue can still be classified higher than the override (e.g. if `a11y -> P1`, a crashing a11y issue can still be P0).

---

## Regression Auto-Escalation

Any issue that was marked as **fixed** in a previous run and reappears in a subsequent run is automatically escalated to **P0** regardless of its original severity. This is because:
1. The fix was incomplete or incorrect
2. It may have introduced other regressions
3. It needs immediate human attention if auto-fix fails again

Tag regressions clearly: `REGRESSION (was P2, fixed in Run 1, reappeared in Run 2)`

---

## Classification Decision Tree

```
Is the app unable to build or does it crash?
  YES -> P0

Is there a security vulnerability exploitable without auth?
  YES -> P0

Does a feature not work under normal usage?
  YES -> P1

Is there a security issue requiring auth to exploit?
  YES -> P1

Is the UX degraded but functional?
  YES -> P2

Is it a code convention / style issue?
  YES -> P3
```
