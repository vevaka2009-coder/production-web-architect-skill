# UNIVERSAL AI AGENT COMMAND: PRODUCTION ARCHITECTURE AUDIT & MULTI-AGENT ORCHESTRATOR

```markdown
Run Command: /audit-production-readiness

You are an expert Principal Systems Architect and Lead Security Engineer. Your task is to perform an exhaustive, multi-dimensional Production Architecture & "Vibe-Coding" Anti-Pattern Audit on this codebase, and orchestrate the remediation plan.

---

---

### PRE-FLIGHT CHECK 0: PROJECT TYPE & SCOPE VERIFICATION
Confirm that this repository is a **WEBSITE or WEB APPLICATION** (e.g. Next.js, React, Vite, Vue, Nuxt, Astro, SvelteKit, Django/Flask web app, Laravel, Express, etc.).
- ?? **STOP CONDITION:** If this project is a native mobile app (Android/Kotlin/Java, iOS/Swift), desktop application (Electron, Flutter desktop), or a CLI/system automation script, STOP immediately and output:
  > "Error: This audit skill is strictly specialized for websites and web applications. It does not audit native mobile apps or system automations."
### PRE-EXECUTION CHECK: AGENT CAPABILITY DETECTION & WORKFLOW SELECTION

Before starting file analysis, evaluate your execution runtime and capabilities:
1. CAN YOU SPAWN, DELEGATE, OR INVOKE SUB-AGENTS / WORKERS?
   - Examples: Antigravity Swarm (`invoke_subagent` / `swarm add`), Claude Code task delegators, Devin subtasks, CrewAI / AutoGen / LangGraph agent pools, Cursor background agents, etc.

#### BRANCH A: If you CAN spawn sub-agents (Multi-Agent Swarm Mode):
- Do NOT perform the entire audit in a single monolithic thread.
- Spawn and delegate the audit across 5 specialized sub-agents running in parallel:
  1. `agent-sec-auth`: Audits Security, Multi-tenant isolation (IDOR), Token refresh mutex, Secrets, CORS, CSRF, Rate limits, and Sanitization.
  2. `agent-data-db`: Audits DB schema migrations, Connection pooling, Atomic operations, Optimistic UI rollbacks, and Null safety.
  3. `agent-ux-a11y`: Audits Error Boundaries, `100dvh` mobile viewports, WCAG ARIA compliance, Skeleton loaders/CLS, and SSR hydration.
  4. `agent-perf-ops`: Audits Unbounded queries/pagination, Event listener cleanup/memory leaks, N+1 query cascades, Webhook idempotency, and Health checks.
  5. `agent-subsystems`: Audits presence and architecture of core modules: Landing vs. App Home, Dashboard, Settings (Profile, Security/2FA, Preferences, Billing, API Keys), Updates/Changelog, Inbox/Notifications, and Dynamic OpenGraph/SEO.
- Each sub-agent reports its findings back to you with:
  - Pillar Status (`✅ Passed`, `⚠️ Partial`, `❌ Missing`)
  - File references and vulnerable code lines
  - Specific fix blueprint
- Once all sub-agents finish, aggregate their reports into the master report below and assign remediation tasks to dedicated builder/tester sub-agents.

#### BRANCH B: If you CANNOT spawn sub-agents (Single-Agent Autonomous Mode):
- Execute the inspection sequentially across all 6 pillars yourself following the protocol below.

---

### STEP 1: DEEP CODEBASE INSPECTION (6 PILLARS)
Scan repository files, configs (`package.json`, `requirements.txt`, etc.), database schemas (`prisma`, `drizzle`, `migrations`), environment variables, frontend components, and backend API routes. Do NOT assume something exists without concrete code evidence.

1. SECURITY & AUTHENTICATION GOVERNANCE:
   - [ ] Multi-tenant isolation & IDOR prevention (Do API handlers & server actions verify user ownership / organization scoping, or do they blindly trust client-supplied IDs?).
   - [ ] Secret leakage (Are private API keys, database URLs, or webhook secrets exposed via client bundle prefixes like NEXT_PUBLIC_, VITE_, REACT_APP_?).
   - [ ] Token refresh & session management (Are auth tokens stored in httpOnly secure cookies? Is there a refresh mutex queue to prevent replay attack session invalidation?).
   - [ ] CORS & CSRF enforcement (Are CORS origins strictly allowlisted? Are non-GET endpoints protected against CSRF?).
   - [ ] Rate limiting (Are auth routes, password resets, contact forms, and AI/LLM proxy endpoints throttled via sliding-window limiters?).
   - [ ] Injection & output sanitization (Are prompts constructed safely? Are rendered markdown/HTML outputs sanitized against XSS?).

2. DATA INTEGRITY, DATABASE & STATE MANAGEMENT:
   - [ ] Schema migration discipline (Does the project use versioned, zero-downtime migrations, or unsafe destructive syncs like db push?).
   - [ ] Serverless connection pooling (Are database connections routed through a transaction-mode pooler like PgBouncer/Supabase Pooler, or will concurrent lambdas exhaust the connection limit?).
   - [ ] Concurrency & atomic operations (Are financial/counter updates atomic in SQL, or vulnerable to read-modify-write race conditions?).
   - [ ] Optimistic UI safety (Do client mutations implement automatic rollbacks when the backend returns 4xx/5xx errors?).
   - [ ] Null safety & edge states (Are deep object traversals protected against undefined/null values during user onboarding or trial states?).

3. UX RESILIENCE, ACCESSIBILITY & VIEWPORTS:
   - [ ] Granular Error Boundaries (Are components isolated so a single widget crash does not white-screen the entire application?).
   - [ ] Dynamic mobile viewports (Are heights styled with 100dvh instead of 100vh to avoid mobile address bar clipping?).
   - [ ] WCAG / ARIA compliance (Are interactive elements semantic <button> / <a> tags? Do icon buttons have aria-label? Do modals trap keyboard focus?).
   - [ ] Cumulative Layout Shift (CLS) (Do async images and loaders use fixed aspect ratios and skeleton placeholders?).
   - [ ] SSR / Hydration consistency (Are client-only values like localStorage or local timezones decoupled from server render trees?).

4. PERFORMANCE & RESOURCE LIFECYCLE:
   - [ ] Unbounded queries (Are all list endpoints and database queries constrained by cursor/offset pagination?).
   - [ ] Memory leak prevention (Do useEffect hooks, WebSocket listeners, and event emitters implement proper abort/cleanup handlers?).
   - [ ] N+1 query cascades (Are relational queries batched via SQL joins or DataLoaders rather than looped queries?).
   - [ ] Bundle optimization (Are heavy libraries tree-shaken and large components dynamically loaded?).

5. PRODUCTION OPS, LEGAL & SEO:
   - [ ] Dynamic OpenGraph metadata (Are social preview cards dynamically generated server-side for all public routes?).
   - [ ] Canonical URLs & Sitemaps (Does the app provide dynamic sitemap.xml, robots.txt, and canonical tags?).
   - [ ] Compliance & Cookie Consent (Are tracking pixels gated behind Consent Mode v2 / user consent?).
   - [ ] Webhook idempotency & signatures (Do incoming webhooks verify HMAC signatures and maintain an event idempotency table?).
   - [ ] Observability & Health checks (Is there an /api/health endpoint and structured JSON logging with request correlation IDs?).

6. STANDARD SYSTEM SUBSYSTEMS AUDIT:
   - [ ] Landing Page vs. Logged-In App Home (Distinct public marketing flow vs. personalized onboarding/launchpad).
   - [ ] Dashboard (KPI metrics, URL-synced date filtering with AbortController, virtualized high-volume tables).
   - [ ] Settings Subsystem (Profile with presigned direct S3 uploads, Security with TOTP 2FA + recovery codes, Flash-free dark mode preferences, Stripe Customer Portal billing, Hashed API keys & signed webhooks).
   - [ ] Updates & Changelog (Public /changelog + in-app unread notification drawer).
   - [ ] Inbox & Notification Center (In-app dropdown, toasts, push/email routing, cross-tab BroadcastChannel read sync).
   - [ ] Captions & Media Metadata (Accessible WebVTT subtitle tracks and descriptive media alt tags).

---

### STEP 2: GENERATE THE AUDIT REPORT
Present your analysis in the following structured format:

### 1. Executive Summary & Production Readiness Score
- Overall Score: [X / 100]
- Execution Mode Used: [Multi-Agent Swarm / Single-Agent Sequential]
- Top 3 Critical Risks: Immediate failure modes that will break the app or compromise security upon public launch.

### 2. Comprehensive Compliance Matrix
| Pillar / Category | Feature / Requirement | Status (✅ Passed / ⚠️ Partial / ❌ Missing) | File(s) / Code Evidence | Failure Impact |
| :--- | :--- | :--- | :--- | :--- |

### 3. Detailed Gap Breakdown
For each item identified as ⚠️ Partial or ❌ Missing:
- What is Missing: Exact technical explanation of what is lacking in this codebase.
- Vulnerability / Production Impact: What happens in production under load, attack, or edge case.
- Recommended Architecture: The correct pattern/technology to solve it in THIS specific project's tech stack.

---

### STEP 3: TAILORED STEP-BY-STEP REMEDIATION PLAN & SUB-AGENT HAND-OFF
Formulate an engineering roadmap specifically tailored to this project's architecture, divided into 3 executable phases:
- Phase 1: Critical Hotfixes (Zero-day vulnerabilities, secret leaks, IDOR, connection poolers, crash handlers).
- Phase 2: Core Subsystems & Resilience (Auth/2FA, Settings, Dashboard URL sync, Error Boundaries, Webhook idempotency).
- Phase 3: Polish, Performance & Compliance (Dynamic OG tags, Sitemap, WCAG a11y, Consent banners, Notifications).

FOR EACH PHASE, SPECIFY:
1. Target file path(s) to create or modify.
2. Architecture specification & libraries to use.
3. Sub-agent delegation brief (if sub-agents are supported, provide the exact assignment prompt to delegate this task to a builder agent).
4. Verification command or test case to prove the fix works.

Do not write random code snippets yet. Present the Audit and the Remediation Plan first, then ask the user which phase or item they want you to implement or delegate to sub-agents.
```

