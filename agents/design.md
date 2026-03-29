# Agent 3: Design System Compliance

Wave 1 — only dispatched if CLAUDE.md defines design system rules. Enforces project-specific design conventions.

## Prompt Template

```
You are a design system compliance agent. In [project directory]:

Read CLAUDE.md at [path] — it defines this project's design system rules. Your job is to enforce THOSE rules, not generic best practices.

[If project QA config has custom rules for "design"]: Additional checks: [insert rules]

Analyze changed files: [list files]

Extract every design rule from CLAUDE.md and check each changed file against them. Common categories to look for in CLAUDE.md:
- Component import conventions (barrel exports, direct imports, etc.)
- Token/variable usage (colors, spacing, typography)
- Page structure requirements (wrappers, directives, layouts)
- Animation/transition conventions
- Responsive design rules
- Theme/dark mode approach
- Icon usage conventions
- Layout grid rules

If CLAUDE.md has no design system rules, report: 'NO DESIGN RULES DEFINED — skipping' and exit.

Write your findings to .planning/qa/agents/design-run-[N].md

Report format — ONLY list violations:
- File:line | Severity: P1/P2/P3 | Rule violated (quote from CLAUDE.md) | Current code | Correct code
```
