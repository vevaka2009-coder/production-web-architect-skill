---
name: production-web-architect
description: Production-grade web architecture, security audit, and AI "vibe-coding" anti-pattern defense skill. Detects IDOR vulnerabilities, missing database migrations, serverless connection pool starvation, optimistic UI rollbacks, mobile viewports (100dvh), accessibility, rate limiting, and blueprints standard subsystems (Landing Page, Dashboard, Settings, Updates/Changelog, Inbox/Notifications, Meta/SEO).
metadata:
  author: vevaka2009-coder
  version: 1.0.0
  tags:
    - web-architecture
    - security-audit
    - vibe-coding-remedy
    - multi-agent-orchestration
    - full-stack-standards
---

# Production Web Architect & Vibe-Coding Guard

This skill empowers AI agents to audit, architect, and harden web applications against the systematic blindspots introduced by AI code generation and rapid "vibe-coding".

## When to Activate This Skill
Activate this skill whenever:
- Auditing an existing codebase for production readiness, scalability, and security.
- The user asks to inspect or review a website built with AI, Cursor, v0, Bolt, Lovable, or Devin.
- Building or refactoring standard web modules: Authentication, Dashboard, Settings, Updates/Changelog, Notifications/Inbox, or SEO/Meta engines.
- Checking for security vulnerabilities (IDOR, leaked client secrets, token refresh race conditions, rate limit bypasses).
- Preparing a web application for commercial launch, security compliance, or multi-tenant scaling.

## Core Capabilities

### 1. 6-Pillar Production Readiness Audit
The skill provides a rigorous inspection protocol across:
1. **Security & Identity Governance:** Multi-tenant scoping (IDOR elimination), client bundle secret audits, HttpOnly cookie auth, token refresh mutex queues, CORS/CSRF headers, sliding-window rate limiters, and prompt/output sanitization.
2. **Data Integrity & State:** Versioned zero-downtime migrations (Expand/Contract pattern), serverless connection poolers (PgBouncer/Supabase Pooler), atomic counter updates, optimistic UI error rollbacks, and null-safe object traversal.
3. **UX Resilience & Viewports:** Granular React Error Boundaries, mobile dynamic viewports (`100dvh`), semantic HTML with WCAG ARIA attributes, fixed-aspect-ratio skeleton loaders (CLS < 0.1), and flash-free theme scripts.
4. **Performance & Resources:** Mandatory cursor/limit pagination, cleanup functions on async event/socket listeners, eager-loading relations to eliminate N+1 queries, and code-split bundles.
5. **SEO, Legal & Operations:** Dynamic OpenGraph image generation (`1200x630`), canonical tags, dynamic `sitemap.xml`, Consent Mode v2, webhook HMAC verification with idempotency tables, and structured health check endpoints (`/api/health`).
6. **Standard Subsystem Blueprinting:** High-fidelity architectural specifications for Landing vs. Logged-in Home, Dashboard, Settings (Profile, Security/2FA, Preferences, Billing, API Keys), Updates/Changelog, Inbox/Notifications, and Dynamic Captions/SEO.

### 2. Multi-Agent Swarm Orchestration Mode
When operating in an agent runtime capable of spawning sub-agents (Antigravity Swarms, Claude Code, Devin subtasks, CrewAI, AutoGen):
- Dispatches parallel audit workers:
  * `agent-sec-auth` (Security & Auth)
  * `agent-data-db` (Database, Migrations & State)
  * `agent-ux-a11y` (UX, Viewports & Accessibility)
  * `agent-perf-ops` (Performance, Webhooks & Ops)
  * `agent-subsystems` (Core Web Views & Engines)
- Aggregates findings into an executive scorecard and issues task-specific implementation briefs for builder sub-agents.

### 3. Single-Agent Autonomous Mode
When running as a standalone agent or in standard chat environments:
- Sequentially scans the project directory and files.
- Generates a structured Compliance Matrix (`✅ Passed`, `⚠️ Partial`, `❌ Missing`).
- Outputs a 3-phase remediation engineering roadmap tailored to the project's exact framework (Next.js, Vite, Django, Laravel, Supabase, Express, etc.).

## Quick Command
To run an immediate audit on the current workspace, execute the command from `commands/audit-production-readiness.md`:
```markdown
/audit-production-readiness
```

## References & Blueprints
- `references/website_architecture_and_ai_pitfalls.md`: The complete 1,800+ line master reference manual detailing the top 25 AI omissions with code examples and remedies.
- `references/database_schema_ddl.sql`: Complete PostgreSQL schema with Row-Level Security (RLS) policies.
- `commands/audit-production-readiness.md`: The universal prompt to copy-paste into any external AI agent.
