# Changelog

## v1.2.0 (2026-03-29)

### The personality update -- Bug Hunter finds its voice

### Added
- **Voice & Tone section** in SKILL.md -- instructs Claude to narrate QA sessions with Steve Irwin energy, safari metaphors, and Australian flair throughout all terminal output
- Steve Irwin-style severity flavour text (P0: "the habitat is on fire", P3: "she'll be right")

### Changed
- **Rebranded to Bug Hunter** -- skill title, commit message prefixes (`[BugHunter]`), and all user-facing language updated
- **README.md** -- complete rewrite with puns, safari metaphors, and personality. Same info, more fun
- **SKILL.md step headers** themed: Base Camp, Gear Check, Deploy the Hunting Party, Collect Specimens, Log the Hunt, Wrangle Specimens, Check the Traps, Expedition Debrief, Protected Species, Rules of the Hunt
- **All 5 templates** rewritten with personality:
  - Session: "Safari Mission Briefing" with Hunting Party, Gear Check, Safari Log
  - Run report: "Hunt Log" with Haul Summary, threat-level section headers, Wrangling Log
  - Summary: "Expedition Report" with "Specimens Wrangled", "Still At Large", "Field Notes"
  - History: "Safari Log" with habitat/verdict/escapes columns
  - Suppressed: "Protected Species" -- because some bugs are features, mate

### Fixed
- Splash screen character now wears safari hat (was missing in v1.1.0)
- Victory display legs symmetric (`\|| || ||/`)
- Victory/Escalate results line uses compact placeholders with proper right-padding

---

## v1.1.0 (2026-03-29)

### Added
- **Bug Hunter visual system** -- full terminal UI with interactive ASCII mascot
  - 10 character states with pixel-art poses (HUNTING, FOUND_P0, FOUND_P1, FOUND_MINOR, FOUND_CLEAN, WRANGLING, LOOPING, REGRESSION, VICTORY, ESCALATE)
  - Safari Trail progress breadcrumb for every stage
  - Mission Control agent dispatch board with live status
  - Threat Level Meter with 5-level severity gauge
  - Bug Trophy Case with severity breakdown and density bars
  - Wrangling Progress tracker with per-bug status
  - Stats Dashboard with career stats, capture rate, and streak tracking
  - Steve Irwin-style quote pools (randomized, no repeats per session)
  - 8 composite display specs (Splash, Hunt, Found, Wrangle, Verify, Loop, Victory, Escalate)
  - Credit line on splash and final displays
- Version field added to SKILL.md frontmatter
- CHANGELOG.md

### Changed
- SKILL.md updated with Bug Hunter Visual System section and 6 integration trigger points (Steps 0.11, 2, 3, 5, 6, 7)
- README.md updated with Bug Hunter section, visual preview, and updated How It Works

## v1.0.0 (2026-03-27)

Initial release.

- 10 specialized QA agents (build, security, design, code quality, API/data, UI/UX, flow, a11y, dependency, migration)
- Auto-scales from lite (1 agent) to full swarm based on diff size
- Stack-adaptive detection (Next.js, Laravel, Python, Rust, Go, static sites)
- Iterative convergence loop with smart re-testing
- Project-level config with severity overrides, custom rules, excluded paths
- Issue suppression with expiry dates
- Multiple output formats (Markdown, SARIF, JSON, GitHub annotations, terminal)
- Quality gate mode for CI integration
- Historical tracking and regression detection
- Auto-commit fixes with structured messages
- Test stub generation
- Setup wizard (`/deep-qa:setup`)
