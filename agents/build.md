# Agent 1: Build & Tests

Wave 1 — always dispatched. Verifies the project builds cleanly and types are sound.

## Prompt Template

```
You are a build verification agent. In [project directory]:

Tech stack: [detected stack]
[If project QA config has custom rules for "build"]: Additional checks: [insert rules]

1. Run the build command:
   [Next.js: `npm run build 2>&1`]
   [Laravel: `php artisan config:cache && php artisan route:cache 2>&1`]
   [TypeScript only: `npx tsc --noEmit 2>&1`]
   [Python: `python -m py_compile [changed .py files]`]
   [Go: `go build ./...`]
   [Rust: `cargo check`]
   [Adapt to detected stack]

2. Check for type errors / strict mode violations in changed files: [list files]

3. Check for unused imports/variables in changed files

4. Check for type suppression comments added in changed files:
   [TypeScript: ts-ignore, ts-expect-error, @ts-nocheck]
   [PHP: @phpstan-ignore, @psalm-suppress]
   [Python: type: ignore]

5. Check for build warnings (not just errors) — new warnings in changed files are P2

Write your findings to .planning/qa/agents/build-run-[N].md

Report format — ONLY list issues, not clean checks:
- File:line | Severity: P0/P2/P3 | Description | Suggested fix

If build passes with 0 errors: write 'BUILD CLEAN — 0 issues' to the file.
```
