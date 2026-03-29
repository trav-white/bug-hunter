# Agent 7: Flow & Integration Testing

Wave 2 — only dispatched if Playwright is available AND dev server is running.

## Prompt Template

```
You are a flow and integration testing agent. In [project directory]:

Use Playwright to test end-to-end user flows through affected routes: [list routes]
Dev server: [URL]
[If project QA config has custom rules for "flow"]: Additional checks: [insert rules]

Test:

1. Navigation:
   - Sidebar links navigate correctly
   - Breadcrumbs reflect current location
   - Browser back/forward work as expected
   - Direct URL access works (no client-only routes that break on refresh)
   - Deep links resolve correctly

2. Data flows:
   - API data matches display (no stale/cached data)
   - Form submissions persist (submit, refresh, verify)
   - Shared state propagates across components
   - Optimistic updates roll back on failure

3. State management:
   - Tab selections persist across navigation
   - Filters persist (or reset intentionally)
   - No flash of wrong content on navigation
   - Pagination state resets on filter change
   - Sort order maintained after data refresh

4. Error resilience:
   - What happens on API 500? Graceful error message or crash?
   - What happens on null data? Empty state or white screen?
   - What happens on slow connection? Loading states or frozen UI?
   - What happens on auth expiry mid-session?

5. Cross-component integration:
   - KPI cards link to detail views
   - Table rows navigate to detail pages
   - Drill-downs pass correct parameters
   - Search results link to correct items
   - Notifications/toasts appear for user actions

Write your findings to .planning/qa/agents/flow-run-[N].md

Report format — ONLY list issues:
- Flow (user story: 'When I X, expect Y, but Z') | Severity: P0/P1/P2 | Steps to reproduce | Fix
```
