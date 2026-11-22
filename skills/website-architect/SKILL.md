---
name: production-web-architect
description: Exclusively built for websites and web applications. Tailored for AI project builders and vibe-coders building websites. Detects, reports, and corrects everything you or the AI forgot to build into your website—including IDOR security vulnerabilities, database connection pool exhaustion, missing zero-downtime migrations, broken mobile viewports (100dvh), missing error boundaries, and standard web subsystems (Settings, Inboxes, Updates/Changelogs, Dashboards, and Dynamic OpenGraph SEO). NOT for Android/iOS mobile apps or system automations.
metadata:
  author: vevaka2009-coder
  version: 1.0.0
  tags:
    - websites-only
    - web-architecture
    - vibe-coding
    - ai-builders
    - security-audit
---

# Production Web Architect & Vibe-Coding Guard (Websites Only)

> ⚠️ **STRICT SCOPE NOTICE: WEBSITES ONLY**  
> This skill is **strictly for websites and web applications** (SaaS platforms, web portals, marketing sites, blogs, and e-commerce stores).  
> **DO NOT USE FOR:** Native Android/iOS apps, desktop software, or OS/system automations. It specifically checks browser environments, responsive web viewports, web cookies, and web backend architectures.

Built specifically for **AI project builders and vibe-coders** who create websites using AI tools (Cursor, v0, Bolt, Lovable, Devin, Replit, Claude, ChatGPT). It automatically inspects your website repository, tells you what was missed or neglected during generation, and writes the code and architecture plans to correct it.

## When to Activate This Skill
- When building a **website or web application** using AI coding tools or "vibe-coding" and wanting a comprehensive production-readiness check.
- When an AI-generated website works on the happy path, but needs web production hardening (security, database scaling, error handling, mobile responsiveness).
- When scaffolding or verifying standard web subsystems: Landing vs. App Home, Dashboard, Settings (Profile, Security, Preferences, Billing, API Keys), Updates/Changelog, Inbox/Notifications, or SEO/Meta engines.
- To detect and fix silent web vulnerabilities: IDOR, leaked secrets in frontend bundles, token refresh race conditions, connection pool starvation, and unhandled optimistic UI errors.

## What It Does
1. **Detects What AI Missed in Your Website:** Scans the codebase across 6 essential engineering pillars and 25 critical web failure modes.
2. **Explains the Gaps:** Reports findings in plain, actionable language with file paths and risk levels (`✅ Passed`, `⚠️ Partial`, `❌ Missing`).
3. **Corrects & Builds the Missing Pieces:** Generates tailored, copy-pasteable production implementations and migration steps for your specific web framework (Next.js, Vite, React, Vue, Svelte, Nuxt, Astro, Remix, Supabase, Express, etc.).
4. **Multi-Agent Orchestration:** Dispatches parallel worker sub-agents (`agent-sec-auth`, `agent-data-db`, `agent-ux-a11y`, `agent-perf-ops`, `agent-subsystems`) when running in multi-agent environments.

## Quick Command
To run an instant audit on the active website codebase, run the prompt in `commands/audit-production-readiness.md`:
```markdown
/audit-production-readiness
```
