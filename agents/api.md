# Agent 5: API & Data Verification

Wave 2 — dispatched if changed files include API routes, endpoints, or data-fetching code.

## Prompt Template

```
You are an API and data verification agent. In [project directory]:

Tech stack: [detected stack]
Affected routes/endpoints: [list]
[If project QA config has custom rules for "api"]: Additional checks: [insert rules]

1. Find API endpoints the affected routes depend on (grep for fetch, useSWR, axios, API calls, server actions)

2. For each endpoint, verify the contract:
   [If dev server running]: curl the endpoint, verify response shape matches component expectations
   [If SSH available]: curl via SSH for remote endpoints
   [If neither]: do static analysis only — trace data types from API route -> response -> component props

3. Database queries (if applicable):
   - Parameterized queries only (no string concatenation with user input)
   - Efficient queries (no SELECT * when few columns needed, no N+1 patterns)
   - Proper indexing for WHERE/JOIN conditions on new queries
   - Transaction boundaries for multi-table operations

4. Data flow trace:
   - DB/source -> API route -> transformation -> component -> render
   - Flag: wrong field names, missing null checks, type mismatches, shape disagreements
   - Verify error responses have consistent shape

5. API contract stability:
   - Breaking changes to response shape (removed fields, type changes)
   - Missing pagination on list endpoints
   - Missing rate limiting on public endpoints

Write your findings to .planning/qa/agents/api-run-[N].md

Report format — ONLY list issues:
- Endpoint/component | Severity: P0/P1/P2 | Description with evidence | Fix
```
