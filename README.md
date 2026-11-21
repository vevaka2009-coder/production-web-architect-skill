# Production Web Architect & Vibe-Coding Guard 🛡️

An autonomous AI agent skill and multi-agent audit framework designed to evaluate, harden, and blueprint production-ready web applications against standard AI "vibe-coding" anti-patterns.

---

## 🎯 What It Does

When developers build websites using rapid conversational AI prompts ("vibe-coding"), models prioritize the visual happy path. Consequently, critical engineering requirements—such as multi-tenant authorization (IDOR), secret containment, database pooling, zero-downtime migrations, and mobile viewport resilience—are routinely omitted.

This skill provides:
1. **Automated 6-Pillar Audit:** Scans codebases for 25 high-risk vulnerabilities and edge-case omissions.
2. **Multi-Agent Swarm Orchestration:** Detects whether the hosting AI environment supports sub-agents. If supported, it dispatches specialized audit workers (`agent-sec-auth`, `agent-data-db`, `agent-ux-a11y`, `agent-perf-ops`, `agent-subsystems`) in parallel.
3. **Core Subsystem Blueprints:** Production-ready architectures for Landing Pages, Dashboards, Settings (Profile, Security/2FA, Billing, API Keys), Changelogs, Inboxes, and Dynamic OpenGraph SEO engines.
4. **Phased Remediation Planning:** Delivers a 3-phase engineering roadmap tailored to the target project's tech stack.

---

## 📁 Repository Structure

```text
├── SKILL.md                          # Main agent skill definition and trigger rules
├── commands/
│   └── audit-production-readiness.md # Universal prompt for any AI agent or IDE
├── references/
│   ├── website_architecture_and_ai_pitfalls.md # Comprehensive 1,800+ line master manual
│   ├── database_schema_ddl.sql       # PostgreSQL DDL with Row Level Security (RLS)
│   └── research_notes.md             # Background research notes and failure patterns
└── examples/
    └── sample_audit_report.md        # Example output and compliance scorecard
```

---

## 🚀 Quick Start & Installation

### Option 1: Use with Antigravity / Agent Skills
Place this folder into your custom skills directory:
```bash
# Clone directly into your personal agent skills directory
git clone https://github.com/vevaka2009-coder/production-web-architect-skill.git ~/.gemini/antigravity/skills/production-web-architect
```

### Option 2: Use in Any AI Agent (Claude Code, Cursor, Windsurf, Devin, ChatGPT)
1. Open [`commands/audit-production-readiness.md`](commands/audit-production-readiness.md).
2. Copy the entire markdown content.
3. Paste it directly into your AI chat or prompt window within your project workspace.
4. The AI will inspect your repository and return an executive scorecard with a remediation plan.

---

## 🔍 The 6 Audit Pillars

1. **Security & Identity Governance:** Checks for IDOR vulnerabilities, client-bundle secret leaks (`NEXT_PUBLIC_`), token refresh mutex races, CORS allowlists, sliding-window rate limiters, and prompt output sanitization.
2. **Data Integrity & Persistence:** Enforces zero-downtime migrations (Expand/Contract), serverless connection pooling (PgBouncer/Supabase Pooler), atomic SQL updates, optimistic UI rollbacks, and null-safe property traversal.
3. **UX Resilience & Viewports:** Tests for React Error Boundaries, mobile dynamic viewports (`100dvh`), semantic HTML with WCAG accessibility attributes, and layout-shift-free skeleton loaders.
4. **Performance & Resource Lifecycle:** Validates query pagination, event listener/WebSocket cleanup hooks, eager loading to prevent N+1 queries, and code-split asset bundles.
5. **SEO, Legal & Operations:** Audits server-generated dynamic OpenGraph images, canonical tags, dynamic sitemaps, Consent Mode v2, webhook HMAC verification with idempotency tables, and `/api/health` probes.
6. **Core Subsystems:** Verifies architectures for Landing Pages, Dashboards, Settings, Updates/Changelogs, Inboxes, and Media Captions.

---

## 📄 License
Released under the MIT License. Created by [vevaka2009-coder](https://github.com/vevaka2009-coder).
