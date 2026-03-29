---
description: "Initialize Bug Hunter for a project — detect stack, create config, set up QA directory structure with sensible defaults."
argument-hint: "[--minimal] [--strict]"
---

# Bug Hunter Setup

Interactive setup wizard that initializes Bug Hunter for the current project. Run this once per project to configure QA behaviour.

## Arguments

- `--minimal` — Create only the config file with auto-detected defaults, no questions asked
- `--strict` — Start with strict defaults (security=P0, a11y=P1, gate=true)

---

## Step 1: Verify Project

1. Confirm we're in a project directory (not `~/` or a non-project path)
2. Check for `CLAUDE.md` — if it exists, read it for project context
3. Check if `.planning/qa/` already exists:
   - If yes: ask user if they want to reconfigure or abort
   - If no: proceed with fresh setup

## Step 2: Detect Stack

Run the full stack detection from `references/stack-profiles.md`:

```bash
ls package.json composer.json Gemfile requirements.txt Cargo.toml go.mod pyproject.toml 2>/dev/null
cat package.json 2>/dev/null | grep -E '"(next|react|vue|svelte|angular|express|fastify|nuxt|remix|astro)"'
ls tsconfig.json 2>/dev/null
cat package.json 2>/dev/null | grep -E '"(vitest|jest|mocha|playwright|cypress)"'
cat package.json 2>/dev/null | grep -E '"(drizzle-orm|prisma|sequelize|typeorm|knex|mongoose)"'
ls database/migrations/ prisma/schema.prisma drizzle.config.* 2>/dev/null
cat package.json 2>/dev/null | grep -E '"(tailwindcss|styled-components|emotion)"'
ls Dockerfile docker-compose.yml 2>/dev/null
```

Present the detected stack to the user:

```
Detected Stack:
  Framework:    Next.js 14 + React
  Language:     TypeScript
  ORM:          Drizzle
  CSS:          Tailwind CSS
  Test runner:  Vitest + Playwright
  Package mgr:  pnpm
  Container:    Docker

Does this look right? (y/n)
```

If the user corrects anything, adjust the config accordingly.

## Step 3: Determine Agent Selection

Based on the detected stack, show which agents will be active:

```
Agent Selection for this stack:
  [x] 1. Build & Tests        (Wave 1 — always)
  [x] 2. Security & Auth      (Wave 1 — always)
  [ ] 3. Design System         (Wave 1 — no design rules in CLAUDE.md)
  [x] 4. Code Quality          (Wave 1 — always)
  [x] 5. API & Data            (Wave 2 — API routes detected)
  [x] 6. UI/UX Visual          (Wave 2 — Playwright detected)
  [x] 7. Flow & Integration    (Wave 2 — Playwright detected)
  [x] 8. A11y & Performance    (Wave 2 — UI components detected)
  [x] 9. Dependency Audit      (Wave 1 — pnpm detected)
  [x] 10. Migration Safety     (Wave 1 — Drizzle detected)

Want to adjust any of these? (y/n)
```

## Step 4: Configure Defaults

If `--minimal`, use auto-detected defaults. If `--strict`, use strict defaults. Otherwise, ask:

```
Default Settings:
  Scope:           all
  Auto-fix:        true (P0-P2 fixed automatically, P3 report only)
  Max runs:        5
  Format:          markdown
  Generate tests:  false
  Quality gate:    false

  Severity overrides: none
  [--strict would set: security=P0, a11y=P1, gate=true]

Want to customise any defaults? (y/n)
```

If yes, walk through each setting.

### Severity Overrides

```
Severity overrides let you reclassify minimum severity for categories.
For example, setting a11y=P1 means all accessibility issues are at least P1.

Current overrides: none

Add an override? (category -> severity, or 'done')
> a11y -> P1
> security -> P0
> done
```

### Excluded Paths

```
Excluded paths are skipped entirely by QA.
Use glob patterns (e.g. src/legacy/**)

Current exclusions: none

Add an exclusion? (glob pattern + reason, or 'done')
> src/legacy/** — Known tech debt, rewrite planned
> done
```

## Step 5: Custom Rules (Optional)

```
Custom rules add project-specific checks to built-in agents.
These are checked in addition to the standard checks.

Examples:
  build: "Verify npm run lint passes"
  security: "All API routes must check x-api-key header"
  code: "No direct DB queries — use repository pattern"

Add custom rules? (y/n)
```

If yes, walk through by category.

## Step 6: Custom Agents (Optional)

```
Custom agents handle domain-specific QA that the built-in agents don't cover.

Examples:
  "data-freshness" — verify cron sync jobs have staleness checks
  "email-templates" — verify all email templates render correctly

Add a custom agent? (y/n)
```

If yes, gather: name, wave (1 or 2), scope (glob), condition, and prompt.

## Step 7: Create Files

Create the QA directory structure and config:

```bash
mkdir -p .planning/qa/screenshots .planning/qa/agents
```

Write `.planning/qa/config.md` with all the configured values, using `assets/config-template.md` as the base structure but filled in with the user's choices.

Write `.planning/qa/suppressed.md` from `assets/suppressed-template.md` (empty, ready for use).

Write `.planning/qa/HISTORY.md` from `assets/history-template.md` (header only, ready for appending).

## Step 8: Summary

Print the final configuration:

```
Bug Hunter initialized for [project name]

  Config:     .planning/qa/config.md
  History:    .planning/qa/HISTORY.md
  Suppressed: .planning/qa/suppressed.md

  Stack:      Next.js 14 + React + TypeScript + Drizzle
  Agents:     8 of 10 active
  Defaults:   scope=all, fix=true, max-runs=5
  Overrides:  security=P0, a11y=P1
  Exclusions: 1 path excluded
  Custom:     0 custom agents, 2 custom rules
  Gate:       enabled

  Run /bug-hunter to start your first QA session.
  Run /bug-hunter --report to check session status.
  Run /bug-hunter:setup to reconfigure.
```

Offer to commit the QA config files:

```
Commit QA config to git? (y/n)
```

If yes, commit with message: `[PROJECT-CODE] Initialize Bug Hunter configuration`
