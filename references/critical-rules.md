# Critical Rules

These rules govern all Deep QA behaviour. Agents and the orchestrator must follow them without exception.

---

## Execution Rules

1. **Parallel agent calls** — Wave 1 agents are independent; launch all simultaneously in a SINGLE message with multiple Agent tool calls. Same for Wave 2. This cuts QA time in half.

2. **Agents write to files** — All agent output goes to `.planning/qa/agents/[name]-run-[N].md`. Do NOT carry full agent reports in the main conversation context. Read the files, extract the issue list, work from the summary.

3. **Smart re-testing** — Run 2+ only re-dispatches agents that found P0/P1/P2 issues OR whose scope was touched by fixes. Agent 1 (Build) always re-runs as a regression gate. This typically cuts subsequent runs from 10 agents down to 2-3.

4. **Max iterations** — Respect `--max-runs` (default 5). If convergence isn't reached, escalate to user. Don't loop forever.

5. **Run existing tests first** — If the project has a test suite, run it before dispatching agents. Fail fast on known test failures.

6. **Pre-flight before Wave 2** — Check Playwright, dev server, SSH before dispatching runtime agents. Skip agents whose prerequisites aren't met rather than wasting agent slots.

---

## Quality Rules

7. **Evidence, not opinions** — Every issue must include file:line, error output, curl response, or screenshot. "This looks wrong" is not valid. If you can't point to the exact line and explain the exact problem, it's not an issue.

8. **Severity accuracy** — Don't inflate P3s to P1s. A slightly off margin is not critical. A crash is. Consult `references/severity-guide.md` when uncertain. Over-reporting erodes trust in the tool.

9. **Stack-adaptive prompts** — Agent prompts must reference the detected tech stack. Don't check React patterns in a Laravel project or PHP patterns in a Next.js project. Irrelevant checks waste agent time and produce false positives.

10. **Never auto-fix P3s** — Report them, let the user decide. Auto-fix P0-P2 only. P3 fixes are opinionated and may conflict with the developer's intent.

---

## Project Respect Rules

11. **Read CLAUDE.md first** — Project-specific rules override generic best practices. If the project says "no Tailwind", don't flag inline styles. If the project says "all data from DB via cron", don't flag the absence of real-time API calls.

12. **Honour project config** — If `.planning/qa/config.md` exists, its severity overrides, custom rules, excluded paths, and custom agents all take precedence over defaults.

13. **Filter suppressions** — Always check `.planning/qa/suppressed.md` before reporting issues. Suppressed issues are intentionally accepted and should not appear in reports.

14. **Respect project boundaries** — Only test and fix files in the current project scope. Don't modify protected files listed in CLAUDE.md. Don't touch files outside the project directory.

---

## Tracking Rules

15. **Track regressions** — If an issue was fixed in Run N and reappears in Run N+1, auto-escalate to P0 and tag as REGRESSION. This catches bad fixes immediately.

16. **History is append-only** — Always update `.planning/qa/HISTORY.md` at session end. Never modify previous entries. This provides quality trending across sessions.

17. **Commit fixes, not just reports** — QA fixes should be committed to the branch (never main). QA report files in `.planning/qa/` get their own commit. Never leave the user with uncommitted fix code.

---

## Output Rules

18. **Context efficiency** — Do NOT paste full agent outputs into the main conversation. Read the agent output files, extract the issue summary, and present a concise report to the user.

19. **Format compliance** — When `--format` is specified, produce valid output in that format. SARIF must validate against the SARIF 2.1.0 schema. JSON must be valid JSON. GitHub annotations must use the `::error`/`::warning`/`::notice` syntax.

20. **Quality gate is binary** — When `--gate` is set, the result is PASS or FAIL. No ambiguity. P0 or P1 remaining = FAIL. Everything else = PASS.
