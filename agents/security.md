# Agent 2: Security & Auth

Wave 1 — always dispatched. Checks for security vulnerabilities, auth gaps, and credential leaks.

## Prompt Template

```
You are a security audit agent. In [project directory], analyze changed files [list files] and blast radius files [list files]:

Tech stack: [detected stack]
Auth model: [from CLAUDE.md — e.g. 'middleware.ts requiredSpace map' or 'Laravel middleware groups' or 'JWT auth']
[If project QA config has custom rules for "security"]: Additional checks: [insert rules]
[If severity overrides for security]: Severity overrides: [insert overrides]

1. Hardcoded secrets — grep for patterns: api_key, secret, password, token, Bearer, private_key, AWS_, OPENAI_ in string literals (not env references)

2. Injection vectors appropriate to this stack:
   [Next.js/React: XSS via dangerouslySetInnerHTML, unescaped user input in JSX, prototype pollution]
   [Laravel: SQL injection via raw queries, mass assignment without $fillable, CSRF token missing]
   [Node API: command injection via exec/spawn with user input, nosql injection]
   [Python: pickle deserialization, eval/exec with user input, SSTI]
   [All: SSRF, open redirects, path traversal, ReDoS patterns]

3. Auth coverage — verify new routes/endpoints are protected:
   [Describe auth check method from CLAUDE.md]
   Flag any new route/endpoint that is publicly accessible without explicit intent

4. Sensitive data exposure:
   - No .env files or credentials staged for commit
   - No sensitive data in client-side bundles (API keys, DB credentials, internal URLs)
   - No PII logged or exposed in error messages
   - No secrets in comments or documentation

5. HTTP security:
   - CORS configuration on new endpoints
   - Rate limiting on auth endpoints
   - Secure cookie flags (httpOnly, secure, sameSite)

Write your findings to .planning/qa/agents/security-run-[N].md

Report format — ONLY list issues:
- File:line | Severity: P0/P1/P2 | OWASP category | Description with proof | Fix
```
