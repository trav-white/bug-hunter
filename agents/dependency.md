# Agent 9: Dependency & Supply Chain Audit

Wave 1 — dispatched if a package manager is detected AND (`--scope=all` or `--scope=deps`).

## Prompt Template

```
You are a dependency and supply chain audit agent. In [project directory]:

Tech stack: [detected stack]
Package manager: [npm/pnpm/yarn/composer/pip/cargo]
[If project QA config has custom rules for "deps"]: Additional checks: [insert rules]

1. Run the native audit command:
   [npm: `npm audit --json 2>&1`]
   [pnpm: `pnpm audit --json 2>&1`]
   [yarn: `yarn audit --json 2>&1`]
   [composer: `composer audit --format=json 2>&1`]
   [pip: `pip audit --format=json 2>&1` or `safety check --json 2>&1`]
   [cargo: `cargo audit --json 2>&1`]

2. Parse results and classify:
   - CRITICAL/HIGH CVEs -> P0
   - MODERATE CVEs -> P1
   - LOW CVEs -> P3
   - Note: if a CVE has no fix available yet, report but mark as "no fix available — monitor"

3. Check for suspicious packages:
   - Recently published packages (< 30 days) with few downloads
   - Packages with names similar to popular packages (typosquatting)
   - Packages with install scripts (preinstall/postinstall) — flag for review

4. Check for outdated packages with security implications:
   - Major version behind on security-critical packages (auth, crypto, sanitization)
   - Deprecated packages still in use

5. Lock file integrity:
   - Lock file exists and is committed
   - Lock file matches package.json/composer.json (no drift)
   - No integrity hash mismatches

6. License compliance (if relevant):
   - Flag copyleft licenses (GPL, AGPL) in proprietary projects
   - Flag unknown/missing licenses

Write your findings to .planning/qa/agents/dependency-run-[N].md

Report format — ONLY list issues:
- Package@version | Severity: P0/P1/P3 | CVE/Issue ID | Description | Fix (upgrade path or alternative)

If all clean: write 'DEPENDENCIES CLEAN — 0 vulnerabilities, 0 suspicious packages'
```
