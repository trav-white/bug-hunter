# Deep QA — Claude Code Skill

Iterative, multi-layer quality assurance skill for [Claude Code](https://claude.ai/claude-code). Auto-detects tech stack, scales agent count to diff size, and tests build, security, design, code quality, APIs, data flows, accessibility, dependencies, and database migrations. Runs until 0 issues remain or escalates.

## Features

- **10 specialized QA agents** covering build, security, design, code quality, API/data, UI/UX, flow testing, accessibility, dependency audit, and migration safety
- **Auto-scales** from lite (1 agent) to full swarm (10+ agents) based on diff size
- **Stack-adaptive** — auto-detects Next.js, Laravel, Python, Rust, Go, static sites, and more
- **Iterative convergence loop** — runs until clean, with smart re-testing on subsequent runs
- **Project-level config** — severity overrides, custom rules, excluded paths, custom agents
- **Issue suppression** — mark known issues as accepted with expiry dates
- **Multiple output formats** — Markdown, SARIF (CI/CD), JSON, GitHub annotations, terminal
- **Quality gate mode** — binary PASS/FAIL for CI integration
- **Historical tracking** — quality trends across sessions
- **Regression detection** — tracks fix-then-reappear issues across runs
- **Auto-commit** — fixes committed with structured messages
- **Test stub generation** — identifies untested code paths and generates stubs
- **Setup wizard** — `/deep-qa:setup` initializes config per project

## Installation

Copy the `deep-qa/` directory into your Claude Code commands folder:

```bash
# Global install (available in all projects)
cp -r deep-qa ~/.claude/commands/

# Project-specific install
cp -r deep-qa <your-project>/.claude/commands/
```

## Usage

```bash
# Run full QA on current branch changes
/deep-qa

# First-time setup for a project
/deep-qa:setup

# Specific scope
/deep-qa --scope=security
/deep-qa --scope=build,code

# QA an entire feature area (not just changed files)
/deep-qa --area=src/finance

# Only uncommitted changes
/deep-qa --diff-only

# Report only (no fixes)
/deep-qa --fix=false

# CI/quality gate mode
/deep-qa --gate --format=sarif

# Generate test stubs for untested code
/deep-qa --generate-tests

# Resume previous session
/deep-qa --continue

# Check session status
/deep-qa --report
```

## Directory Structure

```
deep-qa/
├── SKILL.md                      # Main orchestrator
├── agents/                       # Agent prompt templates
│   ├── lite.md                   # Combined agent (small diffs)
│   ├── build.md                  # Agent 1: Build & Tests
│   ├── security.md               # Agent 2: Security & Auth
│   ├── design.md                 # Agent 3: Design System
│   ├── quality.md                # Agent 4: Code Quality
│   ├── api.md                    # Agent 5: API & Data
│   ├── ui.md                     # Agent 6: UI/UX Visual
│   ├── flow.md                   # Agent 7: Flow & Integration
│   ├── a11y.md                   # Agent 8: A11y & Performance
│   ├── dependency.md             # Agent 9: Dependency Audit
│   └── migration.md              # Agent 10: Migration Safety
├── references/                   # Domain knowledge
│   ├── stack-profiles.md         # Tech stack detection matrix
│   ├── severity-guide.md         # P0-P3 classification guide
│   └── critical-rules.md        # Core operational rules
├── assets/                       # Templates
│   ├── session-template.md       # SESSION.md template
│   ├── run-report-template.md    # RUN-[N].md template
│   ├── summary-template.md       # SUMMARY.md template
│   ├── config-template.md        # Project QA config template
│   ├── history-template.md       # HISTORY.md template
│   └── suppressed-template.md    # Issue suppression template
└── workflows/
    └── setup.md                  # /deep-qa:setup wizard
```

## How It Works

1. **Setup** (Step 0) — Reads CLAUDE.md, loads project config, detects tech stack, determines scope and mode
2. **Pre-flight** (Step 1) — Checks Playwright, dev server, SSH availability
3. **Wave 1** (Step 2) — Dispatches code analysis agents in parallel (build, security, quality, deps, migration)
4. **Wave 2** (Step 3) — Dispatches runtime agents if prerequisites met (API, UI, flow, a11y)
5. **Collect** (Step 3) — Merges results, filters suppressions, detects regressions
6. **Report** (Step 4) — Writes run report in all requested formats
7. **Fix** (Step 5) — Auto-fixes P0-P2 issues, verifies fixes don't regress
8. **Loop** (Step 6) — Smart re-tests only agents that found issues or whose scope was touched
9. **Summary** (Step 7) — Final report, history update, auto-commit, quality gate check

## Project Configuration

Run `/deep-qa:setup` to create a project config, or manually create `.planning/qa/config.md`:

```markdown
## Severity Overrides
| Category | Minimum Severity | Reason |
|----------|-----------------|--------|
| security | P0 | All security findings are blockers |
| a11y | P1 | WCAG AA required |

## Excluded Paths
| Pattern | Reason |
|---------|--------|
| src/legacy/** | Scheduled for rewrite |

## Custom Rules
### security
- All API routes must check x-api-key header

## Custom Agents
### Agent: data-freshness
**Wave**: 1
**Scope**: src/cron/**
**Prompt**: |
  Check all cron sync jobs for staleness checks...
```

## Severity Levels

| Level | Definition | Auto-fix |
|-------|-----------|----------|
| P0 | Build break, security hole, data loss, regression | Yes |
| P1 | Broken feature, runtime error, auth issue | Yes |
| P2 | Poor UX, code smell, missing states | Yes |
| P3 | Convention, style, minor improvement | No (report only) |

## Requirements

- Claude Code CLI
- Git repository
- Stack-specific: Node.js/npm/pnpm, PHP/Composer, Python/pip, etc.
- Optional: Playwright (for UI/flow testing), dev server running

## License

MIT
