---
name: production-web-architect
description: Purpose-built for AI project builders and vibe-coders. Detects, reports, and corrects everything you or the AI forgot to build in your web application—including IDOR security vulnerabilities, database connection pool exhaustion, missing zero-downtime migrations, broken mobile viewports (100dvh), missing error boundaries, and standard subsystems (Settings, Inboxes, Updates/Changelogs, Dashboards, and Dynamic OpenGraph SEO).
metadata:
  author: vevaka2009-coder
  version: 1.0.0
  tags:
    - vibe-coding
    - ai-builders
    - security-audit
    - web-architecture
    - multi-agent-orchestration
---

# Production Web Architect & Vibe-Coding Guard

Built specifically for **AI project builders and vibe-coders** who create applications using AI tools (Cursor, v0, Bolt, Lovable, Devin, Replit, Claude, ChatGPT). It automatically inspects your repository, tells you what was missed or neglected, and writes the code and architecture plans to correct it.

## When to Activate This Skill
- When building a website or app using AI coding tools or "vibe-coding" and wanting a comprehensive production-readiness check.
- When an AI-generated app works on the happy path, but needs production hardening (security, database scaling, error handling, responsiveness).
- When scaffolding or verifying standard subsystems: Landing vs. App Home, Dashboard, Settings (Profile, Security, Preferences, Billing, API Keys), Updates/Changelog, Inbox/Notifications, or SEO/Meta engines.
- To detect and fix silent vulnerabilities: IDOR, leaked secrets in frontend bundles, token refresh race conditions, connection pool starvation, and unhandled optimistic UI errors.

## Core Capabilities
1. **Detects What AI Missed:** Scans the codebase across 6 essential engineering pillars and 25 critical failure modes.
2. **Explains the Gaps:** Reports findings in plain, actionable language with file paths and risk levels (`✅ Passed`, `⚠️ Partial`, `❌ Missing`).
3. **Corrects & Builds the Missing Pieces:** Generates tailored, copy-pasteable production implementations and migration steps for your specific framework.
4. **Multi-Agent Orchestration:** Dispatches parallel worker sub-agents (`agent-sec-auth`, `agent-data-db`, `agent-ux-a11y`, `agent-perf-ops`, `agent-subsystems`) when running in multi-agent environments.

## Quick Command
To run an instant audit on the active codebase, run the prompt in `commands/audit-production-readiness.md`:
```markdown
/audit-production-readiness
```
