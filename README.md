# Bug Hunter -- Deep QA for Claude Code

**v1.2.0** | Built by Trav White, [Neighbourhood CO](https://www.nbh.co)

> *"Crikey, look at the size of that codebase! Don't worry mate, we've got 10 specially trained agents ready to wrangle every last bug out of hiding."*

Bug Hunter is an iterative, multi-layer quality assurance skill for [Claude Code](https://claude.ai/claude-code). It tracks down every bug, broken flow, missing state, and visual issue lurking in your code -- then wrangles them -- then verifies they stay caught -- looping until the habitat is clean or the gnarly ones get escalated to a human.

Auto-detects your tech stack. Scales its agent swarm to match the size of your changes. Narrates the whole safari with ASCII dashboards, threat meters, and a trophy case of everything you've caught.

## The Hunt

```
╔══════════════════════════════════════════════════════════════╗
║                     ___                                      ║
║                    /   \                                     ║
║                    _____                                     ║
║                ___/     \___                                 ║
║               /             \                                ║
║              .---------------.                               ║
║              |   []     []   |                               ║
║              |      .__      |                               ║
║              '---------------'                               ║
║                |||  |||  |||                                  ║
║                                                              ║
║          D  E  E  P        Q  A                              ║
║          B  U  G     H  U  N  T  E  R                       ║
╚══════════════════════════════════════════════════════════════╝
```

Every session is a safari. The Bug Hunter -- a pixel-art creature in a safari hat -- narrates the journey with Steve Irwin-style commentary, dashboards, progress trackers, and a full Stats Dashboard at the end. 10 moods, randomised quote pools, and more Unicode box-drawing than you can poke a stick at.

See [`references/bug-hunter.md`](references/bug-hunter.md) for the full visual system specification.

## Features

No bug too small, no code path too wild.

- **10 specialist agents** -- each one trained for a different species of bug: build failures, security holes, design drift, code smells, API mishaps, UI jank, broken flows, accessibility gaps, dodgy dependencies, and migration landmines
- **Auto-scaling swarm** -- 1-5 files? Sends a single scout. 20+ files? Deploys the full hunting party
- **Stack-adaptive** -- sniffs out Next.js, Laravel, Python, Rust, Go, static sites, and more. Knows which agents to send for which habitat
- **Convergence loop** -- hunts, wrangles, re-tests, repeat. Doesn't let up until the habitat is clean or something needs a human
- **Bug Hunter visual system** -- ASCII dashboards, Safari Trail breadcrumbs, Threat Level Meter, Bug Trophy Case, Wrangling Progress tracker, and a mascot with 10 moods. Your terminal has never looked this good
- **Regression detection** -- catches bugs that play dead. If a fix unravels, it gets auto-escalated to P0. *"Thought you could slip past me, did ya?"*
- **Multiple output formats** -- Markdown, SARIF (for CI), JSON, GitHub annotations, terminal. Whatever your pipeline speaks
- **Quality gate** -- binary PASS/FAIL. No bugs? Green light. Bugs? Red light. Simple as
- **Safari log** -- tracks quality trends across sessions. Are things getting better or worse? The log knows
- **Protected species** -- some bugs are features. Mark them as intentional with an expiry date so they don't clog up your reports
- **Test stub generation** -- spots untested code paths and generates skeleton tests. No excuses, mate
- **Project config** -- severity overrides, custom rules, excluded paths, even your own custom agents. Every habitat is different
- **Setup wizard** -- `/deep-qa:setup` gets your project base camp sorted in minutes

## Installation

Drop it in and you're ready to hunt:

```bash
# Global install -- available across all projects
cp -r deep-qa ~/.claude/commands/

# Project-specific install -- just this repo
cp -r deep-qa <your-project>/.claude/commands/
```

## Usage

```bash
# Full safari -- hunt everything on the current branch
/deep-qa

# First-time base camp setup
/deep-qa:setup

# Target specific species
/deep-qa --scope=security
/deep-qa --scope=build,code

# Hunt an entire territory (not just changed files)
/deep-qa --area=src/finance

# Only uncommitted changes -- quick recon
/deep-qa --diff-only

# Reconnaissance only -- report but don't wrangle
/deep-qa --fix=false

# CI quality gate mode
/deep-qa --gate --format=sarif

# Generate test stubs for untested code
/deep-qa --generate-tests

# Resume a previous expedition
/deep-qa --continue

# Check safari status
/deep-qa --report
```

## How the Safari Works

1. **Base Camp** (Step 0) -- Reads the lay of the land. Loads CLAUDE.md, detects tech stack, scopes the hunting ground. Displays the Bug Hunter splash screen. *"Right, let's see what we're dealing with here..."*
2. **Gear Check** (Step 1) -- Checks Playwright, dev server, SSH. Can't catch runtime bugs without a running app
3. **Deploy the Hunting Party** (Step 2) -- Launches code analysis agents in parallel. Build, security, quality, deps, migration. Shows the Mission Control board with live deployment status
4. **Collect Specimens** (Step 3) -- Runtime agents go next (API, UI, flow, a11y). Results pour in. Shows Threat Level Meter and Bug Trophy Case
5. **Log the Hunt** (Step 4) -- Documents every specimen found. Markdown, SARIF, JSON, GitHub annotations -- your call
6. **Wrangle Specimens** (Step 5) -- Auto-fixes P0-P2 issues with per-bug progress tracking. Verifies each fix doesn't introduce new problems. *"Easy does it... don't want to spook the others"*
7. **Check the Traps** (Step 6) -- Smart re-testing. Only re-deploys agents that found issues or whose territory was touched by fixes
8. **Expedition Debrief** (Step 7) -- Final report card with Stats Dashboard, capture rate, and streak tracking. Victory dance if clean, escalation report if not. *"What a beauty! Not a single P0 left in the wild!"*

## The Agent Squad

| # | Agent | Speciality | When deployed |
|---|-------|-----------|---------------|
| 1 | Build & Tests | Build failures, test regressions | Always -- the gatekeeper |
| 2 | Security & Auth | Injection, auth bypass, leaked secrets | Always -- you don't mess around with security |
| 3 | Design System | Component drift, token violations | When CLAUDE.md defines design rules |
| 4 | Code Quality | Smells, dead code, type issues | Always -- keeps things tidy |
| 5 | API & Data | Endpoint bugs, data integrity | When API routes are in scope |
| 6 | UI/UX Visual | Visual regressions, layout bugs | When Playwright is available |
| 7 | Flow & Integration | Broken user journeys, nav issues | When Playwright is available |
| 8 | A11y & Performance | WCAG violations, perf issues | When UI components are in scope |
| 9 | Dependency Audit | CVEs, outdated packages | When a package manager is detected |
| 10 | Migration Safety | Schema conflicts, data loss risks | When ORM + migrations are in scope |

## Threat Classification

Not all specimens are created equal.

| Level | What it means | Auto-wrangle? |
|-------|--------------|--------------|
| P0 | The habitat is on fire. Build breaks, security holes, data loss, regressions | Yes -- drop everything |
| P1 | That's gonna leave a mark. Runtime errors, auth failures, broken features | Yes |
| P2 | Bit rough around the edges. Code smells, missing states, poor UX | Yes |
| P3 | She'll be right. Convention drift, style nits, the stuff you fix on a slow Friday | No -- report only |

## Directory Structure

```
deep-qa/
├── SKILL.md                      # The safari playbook
├── agents/                       # Agent field manuals
│   ├── lite.md                   # Solo scout (small diffs)
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
├── references/                   # Field guides
│   ├── bug-hunter.md             # Visual system spec (the good stuff)
│   ├── stack-profiles.md         # Tech stack detection matrix
│   ├── severity-guide.md         # Threat classification guide
│   └── critical-rules.md        # Rules of the hunt
├── assets/                       # Report templates
│   ├── session-template.md       # Mission briefing template
│   ├── run-report-template.md    # Hunt log template
│   ├── summary-template.md       # Expedition report template
│   ├── config-template.md        # Project config template
│   ├── history-template.md       # Safari log template
│   └── suppressed-template.md    # Protected species template
└── workflows/
    └── setup.md                  # Base camp setup wizard
```

## Project Configuration

Every habitat is different. Run `/deep-qa:setup` for the guided wizard, or hand-craft `.planning/qa/config.md`:

```markdown
## Severity Overrides
| Category | Minimum Severity | Reason |
|----------|-----------------|--------|
| security | P0 | All security findings are blockers |
| a11y | P1 | WCAG AA required |

## Excluded Paths
| Pattern | Reason |
|---------|--------|
| src/legacy/** | Scheduled for controlled burn |

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

## Requirements

- Claude Code CLI
- A git repository (the Bug Hunter needs tracks to follow)
- Stack-specific tooling: Node.js/npm/pnpm, PHP/Composer, Python/pip, etc.
- Optional: Playwright (for the full runtime hunt), dev server running

## License

MIT
