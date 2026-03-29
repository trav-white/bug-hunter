# Stack Profiles — Detection & Agent Selection

Reference for auto-detecting the project's tech stack and selecting the appropriate QA agents.

---

## Detection Commands

Run these checks during Step 0.4 to build the stack profile:

```bash
# Package managers
ls package.json composer.json Gemfile requirements.txt Cargo.toml go.mod pyproject.toml 2>/dev/null

# Lock files (determines which package manager)
ls package-lock.json pnpm-lock.yaml yarn.lock bun.lockb composer.lock Gemfile.lock poetry.lock Pipfile.lock Cargo.lock go.sum 2>/dev/null

# Frameworks (JS ecosystem)
cat package.json 2>/dev/null | grep -E '"(next|react|vue|svelte|angular|express|fastify|nuxt|remix|astro|gatsby)"'

# TypeScript
ls tsconfig.json 2>/dev/null

# Test runners
cat package.json 2>/dev/null | grep -E '"(vitest|jest|mocha|playwright|cypress|testing-library)"'
[ -f "composer.json" ] && grep -E '"phpunit"' composer.json 2>/dev/null
[ -f "pyproject.toml" ] && grep -E 'pytest' pyproject.toml 2>/dev/null

# ORMs / Databases
cat package.json 2>/dev/null | grep -E '"(drizzle-orm|prisma|sequelize|typeorm|knex|mongoose)"'
[ -f "composer.json" ] && grep -E '"illuminate/database"' composer.json 2>/dev/null
ls prisma/schema.prisma drizzle.config.ts drizzle.config.js 2>/dev/null
ls database/migrations/ 2>/dev/null  # Laravel
ls alembic/ alembic.ini 2>/dev/null  # Python/Alembic

# CSS framework
cat package.json 2>/dev/null | grep -E '"(tailwindcss|styled-components|emotion|sass|less)"'
ls tailwind.config.* postcss.config.* 2>/dev/null

# Containerisation
ls Dockerfile docker-compose.yml docker-compose.yaml 2>/dev/null
```

---

## Stack Profiles

### Next.js + React + TypeScript

| Property | Value |
|----------|-------|
| Build command | `npm run build` |
| Type check | `npx tsc --noEmit` |
| Test runner | Vitest / Jest / Playwright |
| ORM | Drizzle / Prisma (check) |
| CSS | Tailwind / CSS Modules / styled-components (check) |

**Agent selection:**
- Wave 1: Build (1), Security (2), Design (3 if rules exist), Quality (4), Dependency (9), Migration (10 if ORM)
- Wave 2: API (5 if API routes changed), UI (6), Flow (7), A11y (8)
- Security focus: XSS, SSRF, auth middleware, API route exposure, server action validation
- Quality focus: React hooks, SSR hydration, loading/empty/error states

### Laravel + PHP

| Property | Value |
|----------|-------|
| Build command | `php artisan config:cache && php artisan route:cache` |
| Type check | PHPStan / Psalm (if configured) |
| Test runner | PHPUnit |
| ORM | Eloquent |
| CSS | Usually Tailwind or Bootstrap |

**Agent selection:**
- Wave 1: Build (1), Security (2), Quality (4), Dependency (9), Migration (10 if migrations changed)
- Wave 2: API (5 if routes/controllers changed), A11y (8 if blade views changed)
- Skip: Design (3) unless CLAUDE.md defines rules, UI (6) and Flow (7) unless Playwright configured
- Security focus: SQL injection, CSRF, mass assignment, file upload validation
- Quality focus: N+1 queries, service layer, validation rules, transaction boundaries

### Node.js API (Express / Fastify / plain)

| Property | Value |
|----------|-------|
| Build command | `npm run build` or `npx tsc --noEmit` |
| Test runner | Vitest / Jest / Mocha |
| ORM | Varies |

**Agent selection:**
- Wave 1: Build (1), Security (2), Quality (4), Dependency (9), Migration (10 if ORM)
- Wave 2: API (5)
- Skip: Design (3), UI (6), Flow (7), A11y (8) — no frontend
- Security focus: Auth, injection, rate limiting, input validation
- Quality focus: Async error handling, response consistency, connection cleanup

### Python (Django / Flask / FastAPI)

| Property | Value |
|----------|-------|
| Build command | `python -m py_compile` / `mypy` |
| Test runner | pytest / unittest |
| ORM | Django ORM / SQLAlchemy / Alembic |

**Agent selection:**
- Wave 1: Build (1), Security (2), Quality (4), Dependency (9), Migration (10 if ORM)
- Wave 2: API (5 if views/endpoints changed)
- Skip: Design (3) unless templates, UI (6), Flow (7)
- Security focus: SSTI, pickle deserialization, eval/exec, Django ORM injection
- Quality focus: Type hints, context managers, exception specificity

### Static HTML / JS / CSS

| Property | Value |
|----------|-------|
| Build command | Check for broken references, valid HTML |
| Test runner | Playwright if configured |

**Agent selection:**
- Wave 1: Security (2), Quality (4)
- Wave 2: UI (6) and Flow (7) if Playwright available
- Skip: Build (1) unless bundler configured, Design (3) unless rules exist, Dependency (9) unless package.json exists, Migration (10)
- Security focus: XSS, exposed credentials, script integrity
- Quality focus: Vanilla JS patterns, accessibility

### Rust / Go / Other Compiled

| Property | Value |
|----------|-------|
| Build command | `cargo check` / `go build ./...` |
| Test runner | `cargo test` / `go test ./...` |

**Agent selection:**
- Wave 1: Build (1), Security (2), Quality (4), Dependency (9)
- Wave 2: API (5 if HTTP handlers changed)
- Skip: Design (3), UI (6), Flow (7), A11y (8)

---

## Agent Applicability Matrix

Quick reference for which agents apply to which stack:

| Agent | Next.js | Laravel | Node API | Python | Static | Rust/Go |
|-------|---------|---------|----------|--------|--------|---------|
| 1 Build | Yes | Yes | Yes | Yes | Maybe | Yes |
| 2 Security | Yes | Yes | Yes | Yes | Yes | Yes |
| 3 Design | If rules | If rules | No | If rules | If rules | No |
| 4 Quality | Yes | Yes | Yes | Yes | Yes | Yes |
| 5 API | If API | If routes | Yes | If views | No | If HTTP |
| 6 UI | If PW | If PW | No | No | If PW | No |
| 7 Flow | If PW | If PW | No | No | If PW | No |
| 8 A11y | If UI | If blade | No | If tmpl | Yes | No |
| 9 Deps | Yes | Yes | Yes | Yes | If pkg | Yes |
| 10 Migration | If ORM | If migr | If ORM | If ORM | No | If ORM |

PW = Playwright available + dev server running
