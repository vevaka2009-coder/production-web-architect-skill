# Production Web Architect & Vibe-Coding Guard 🌐🛡️
### *Built exclusively for Websites & Web Applications: Find what AI missed when vibe-coding websites, understand why it matters, and fix it automatically.*

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Target Scope](https://img.shields.io/badge/Scope-Websites_&_Web_Apps_Only-purple.svg)](README.md)
[![AI Skill](https://img.shields.io/badge/Agent_Skill-v1.0.0-green.svg)](SKILL.md)
[![Vibe Coding](https://img.shields.io/badge/Vibe_Coding-Hardened-orange.svg)](README.md)

---

> ⚠️ **CRITICAL SCOPE NOTICE: WEBSITES ONLY**  
> This skill is **strictly and exclusively built for websites and web applications** (SaaS platforms, web apps, portals, landing pages, e-commerce web stores).  
> **It is NOT for:** Native mobile applications (Android / iOS / Flutter / React Native), desktop software, or standalone backend system automations/CLI scripts. It specifically audits and fixes web architectures (browser DOM, HTTP cookies, mobile responsive viewports `100dvh`, OpenGraph SEO, and web serverless backends).

---

## 💡 Why This Exists

If you are an **AI project builder** or **vibe-coder** creating **websites and web applications** using tools like Cursor, v0, Bolt, Lovable, Devin, Replit, or Claude Code, you know the superpower: *you can build a working web prototype in hours.*

**But here is the catch:**  
AI models optimize for the visual "happy path." They only build what you explicitly remember to ask for. If you don't ask for multi-tenant tenant checks, token refresh mutexes, serverless connection pooling, mobile viewport dynamic heights, zero-downtime migrations, or webhook idempotency, **the AI simply ignores them**. 

Your website looks great on your desktop browser, but the moment real users sign up, it crashes on mobile viewports, leaks tenant data, or drops database connections.

**This skill is your web safety net.** It acts as an autonomous Senior Principal Web Architect that:
1. **Finds what you or the AI missed building into your website** across security, database, performance, UX, and SEO.
2. **Tells you exactly what is missing** in plain, understandable language with a clear compliance scorecard.
3. **Corrects and builds the missing web features**, providing complete code and step-by-step remediation plans tailored to your exact web tech stack (Next.js, Vite, React, Vue, Svelte, Nuxt, Astro, Remix, Supabase, Express, etc.).

---

## 🎯 Scope & Boundaries

| ✅ SUPPORTED (Websites & Web Apps Only) | ❌ NOT SUPPORTED (Out of Scope) |
| :--- | :--- |
| • Modern Full-Stack Web Applications (Next.js, Remix, Astro) | • Native Android Apps (Kotlin, Java) |
| • Single Page Applications (React, Vue, Svelte, Vite) | • Native iOS Apps (Swift, SwiftUI) |
| • SaaS Dashboards & Client Portals | • Cross-platform Mobile Apps (Flutter, React Native) |
| • Marketing Websites & Landing Pages | • Desktop GUI Applications (Electron, Tauri, Qt) |
| • Web E-Commerce Platforms & Member Sites | • OS / System Automations & Local Shell Scripts |
| • Web APIs & Serverless Web Handlers | • Embedded / IoT Firmware |

---

## ⚡ What It Detects and Fixes in Websites

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       THE WEB VIBE-CODING REALITY CHECK                     │
├───────────────────────────────────┬─────────────────────────────────────────┤
│ What AI Commonly Misses in Web    │ What This Skill Detects & Fixes         │
├───────────────────────────────────┼─────────────────────────────────────────┤
│ 🚨 Unprotected backend APIs (IDOR) │ Tenant-scoped database queries & RLS   │
│ 🔑 Leaked secrets in client JS    │ Server-only env isolation & Zod checks  │
│ 💥 DB connection limit crashes    │ PgBouncer / serverless pooler routing   │
│ 📉 Data loss from unsafe pushes   │ Versioned zero-downtime migrations      │
│ 📱 Broken mobile layouts (100vh)  │ Dynamic viewport units (100dvh)         │
│ 🛑 White-screen app crashes       │ Granular React Error Boundaries         │
│ 💳 Duplicate Stripe charges       │ Webhook HMAC checks & idempotency tables│
│ 🔍 Blank social media link cards  │ Dynamic OpenGraph edge image generators │
│ ⚙️ Missing Settings / Inboxes     │ Full blueprints for 6 core web modules  │
└───────────────────────────────────┴─────────────────────────────────────────┘
```

---

## 🤖 Multi-Agent Swarm Orchestration

When you paste this skill into an AI tool that supports multi-agent execution (Antigravity Swarms, Claude Code, Devin, AutoGen, CrewAI):
- It **automatically detects** sub-agent capability.
- It splits the website audit across 5 specialized sub-agents working in parallel:
  * `agent-sec-auth`: Audits Web Security, IDOR, token refresh queues, and secret leaks.
  * `agent-data-db`: Audits web schema migrations, connection pooling, and atomic locks.
  * `agent-ux-a11y`: Audits Error Boundaries, `100dvh` mobile views, and WCAG accessibility.
  * `agent-perf-ops`: Audits query pagination, memory leaks, N+1 queries, and health probes.
  * `agent-subsystems`: Audits standard web pages (Landing vs. App Home, Dashboard, Settings, Updates, Inbox).
- It aggregates their findings into one unified report and hands off remediation tasks to builder agents.

*(If your AI environment does not support sub-agents, it seamlessly runs in single-agent mode, auditing all pillars sequentially.)*

---

## 📁 Repository Structure

```text
├── SKILL.md                          # Standardized Agent Skill definition and rules
├── commands/
│   └── audit-production-readiness.md # The Universal Prompt command to paste in any AI
├── references/
│   ├── website_architecture_and_ai_pitfalls.md # 1,800+ line master reference manual
│   ├── database_schema_ddl.sql       # PostgreSQL DDL with Row Level Security (RLS)
│   └── research_notes.md             # Background research notes and failure patterns
└── examples/
    └── sample_audit_report.md        # Realistic example of what an audit output looks like
```

---

## 🚀 How to Use It

### Method 1: The 10-Second Copy-Paste (Any AI Agent or IDE)
1. Open [`commands/audit-production-readiness.md`](commands/audit-production-readiness.md).
2. Copy the entire prompt.
3. Paste it directly into your AI coding tool (Cursor, Claude Code, ChatGPT, Devin, Windsurf, Copilot, v0) inside your **website project directory**.
4. The AI will audit your website codebase, report everything that is missing, and provide the exact plan and code to fix it.

### Method 2: Install as a Persistent Agent Skill
Clone this repo into your personal or workspace agent skills directory:
```bash
git clone https://github.com/vevaka2009-coder/production-web-architect-skill.git ~/.gemini/antigravity/skills/production-web-architect
```

---

## 📊 The 6 Core Web Audit Pillars

1. **Security & Identity:** Multi-tenant scoping (IDOR elimination), secret isolation, HttpOnly cookies, token refresh mutex queues, CORS allowlists, and sliding-window rate limiters.
2. **Data & Persistence:** Zero-downtime migrations (Expand/Contract), serverless connection poolers, atomic counter updates, optimistic UI rollbacks, and null safety.
3. **UX & Viewports:** Component error boundaries, mobile dynamic viewports (`100dvh`), semantic HTML with WCAG accessibility attributes, and layout-shift-free skeleton loaders.
4. **Performance:** Mandatory query pagination, event listener/WebSocket cleanup hooks, eager loading to prevent N+1 queries, and bundle tree-shaking.
5. **SEO, Legal & Ops:** Server-generated dynamic OpenGraph images, canonical tags, dynamic sitemaps, Consent Mode v2, webhook HMAC verification, and `/api/health` probes.
6. **Core Web Subsystems:** Complete blueprints for Landing Pages, Dashboards, Settings (Profile, Security/2FA, Billing, API Keys), Changelogs, Inboxes, and Media Captions.

---

## 📄 License
Released under the MIT License. Created by [vevaka2009-coder](https://github.com/vevaka2009-coder).
