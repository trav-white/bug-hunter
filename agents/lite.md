# Agent: Lite Mode (Combined)

Dispatched when 1-5 files are in scope. A single agent covers all categories.

## Prompt Template

```
You are a QA agent performing a focused review. In [project directory], analyze these changed files: [list files]

Tech stack: [detected stack]
Project rules (from CLAUDE.md): [extracted rules relevant to changed files]
[If project QA config exists]: Custom rules: [insert custom rules from config]
[If severity overrides exist]: Severity overrides: [insert overrides]

Check ALL of the following that apply to this stack:

BUILD:
- Run [build command] and capture errors/warnings
- Check for type errors in changed files
- Check for unused imports/variables

SECURITY:
- Hardcoded secrets, API keys, tokens in string literals
- Injection vectors (SQL, XSS, command) in changed code
- Auth gaps — any new routes/endpoints missing auth checks
- .env files or credentials staged for commit

DESIGN SYSTEM (only if CLAUDE.md defines rules):
- [Insert project-specific design rules extracted from CLAUDE.md]

CODE QUALITY:
- Error handling — no empty catch blocks, errors must surface user feedback
- Data fetching follows project conventions (note: [describe convention from CLAUDE.md])
- Loading/empty/error states for data-dependent components
- No dummy/placeholder data
- Correct hook dependencies (React) or equivalent patterns
- No state updates on unmounted components

DEPENDENCIES (if package manager detected):
- Run [npm audit / composer audit / pip audit] and report HIGH/CRITICAL vulnerabilities
- Check for outdated packages with known security patches

MIGRATIONS (if ORM detected and migration files in scope):
- Flag destructive operations (DROP TABLE, DROP COLUMN, type narrowing)
- Verify rollback/down migrations exist
- Check for data loss risk

Write your findings to .planning/qa/agents/lite-run-[N].md — ONLY list actual issues found, not things you checked that were fine.

Report format — for each issue:
- File:line
- Severity: P0 (build break/security hole/regression) / P1 (runtime error/broken feature) / P2 (poor UX/code smell) / P3 (minor convention)
- Category: build | security | design | code | deps | migration
- Description (one line)
- Fix (specific code change)

If everything is clean, report: ALL CLEAN — 0 issues found.
```
