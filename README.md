# Production Architect & Vibe-Coding Guard Suite 🛡️
### *The Complete Autonomous Safety Net for AI Project Builders & Vibe-Coders*

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![AI Skills Suite](https://img.shields.io/badge/Agent_Skills-4_Domains-green.svg)](skills/)
[![Vibe Coding](https://img.shields.io/badge/Vibe_Coding-Production_Hardened-orange.svg)](README.md)
[![Multi-Agent](https://img.shields.io/badge/Multi--Agent-Swarm_Enabled-purple.svg)](README.md)

---

## 💡 The Problem This Suite Solves

When people build projects using AI coding assistants (Cursor, Claude, Devin, ChatGPT, v0, Bolt, Lovable, Replit)—whether they are seasoned developers or vibe-coders with zero formal coding experience—**AI models consistently build for the visual "happy path."**

The AI generates code that looks impressive on a local machine, but silently misses the critical engineering foundations needed for real-world production. It doesn't build what you don't explicitly remember to ask for.

**This suite fixes that permanently.**

When you paste one of these skills into any AI agent, it automatically:
1. **Detects Sub-Agent Capabilities:** If your AI tool supports sub-agents, it spawns specialized workers in parallel to inspect each pillar. If not, it runs sequentially.
2. **Deep-Scans the Entire Codebase:** Compares your code against 20–25 domain-specific production failure modes.
3. **Explains What Was Missed:** Gives a clear, jargon-free **Compliance Scorecard** (`✅ Passed`, `⚠️ Partial`, `❌ Missing`) explaining exactly what is lacking and why it will crash or fail in production.
4. **Builds the Missing Architecture:** Delivers the exact, production-grade code, database schemas, and a step-by-step implementation plan tailored specifically to your project.

---

## 🧭 The 4 Specialized Domain Skills

| Domain | Skill Name & Folder | Target Technologies | Primary Failures Prevented |
| :--- | :--- | :--- | :--- |
| 🌐 **Websites & Web Apps** | [`website-architect`](skills/website-architect/) | Next.js, React, Vue, Svelte, Nuxt, Astro, Vite, Supabase | IDOR security leaks, leaked client secrets, DB connection starvation, mobile viewport bugs (`100dvh`), missing error boundaries, blank social OG previews. |
| 📱 **Mobile Applications** | [`mobile-app-architect`](skills/mobile-app-architect/) | React Native, Expo, Flutter, iOS Swift, Android Kotlin | Runtime permission crashes, notch/Dynamic Island clipping, insecure token storage in AsyncStorage, App Store account deletion rejections, image OOM crashes. |
| ⚙️ **Backend Systems** | [`backend-system-architect`](skills/backend-system-architect/) | Node.js, Go, Python, Java, Docker, Kubernetes, microservices | Dropped requests on deploy (missing SIGTERM), liveness/readiness probe crashes, distributed race conditions, missing circuit breakers, rogue DB locks. |
| ⚡ **Automations & Workflows** | [`automation-workflow-architect`](skills/automation-workflow-architect/) | BullMQ, Celery, Temporal, Airflow, Cron, Python crawlers | Duplicate credit card charges on retry, infinite retry storms without DLQs, zombie workers from lock timeouts, scraping IP bans, memory leaks. |

---

## 🚀 How to Use Any Skill (10-Second Guide)

### Method 1: Instant Copy-Paste (Any AI Agent, IDE, or Chat)
Pick the skill matching your project, open its command file, and paste it into your AI assistant (Cursor, Claude Code, Devin, ChatGPT, Windsurf, Copilot, v0):

* **For Websites:** Copy from [`skills/website-architect/commands/audit-website-readiness.md`](skills/website-architect/commands/audit-website-readiness.md)
* **For Mobile Apps:** Copy from [`skills/mobile-app-architect/commands/audit-mobile-app-readiness.md`](skills/mobile-app-architect/commands/audit-mobile-app-readiness.md)
* **For Backend Services:** Copy from [`skills/backend-system-architect/commands/audit-backend-system-readiness.md`](skills/backend-system-architect/commands/audit-backend-system-readiness.md)
* **For Background Automations:** Copy from [`skills/automation-workflow-architect/commands/audit-automation-workflow-readiness.md`](skills/automation-workflow-architect/commands/audit-automation-workflow-readiness.md)

### Method 2: Install as Persistent Agent Skills (Antigravity / Gemini CLI)
Clone the repository directly into your personal agent skills directory:
```bash
git clone https://github.com/vevaka2009-coder/production-web-architect-skill.git ~/.gemini/antigravity/skills/production-architect-suite
```

---

## 🤖 Multi-Agent Swarm Orchestration

Every skill in this suite features **automated runtime capability detection**:

```
                       ┌────────────────────────────────────────┐
                       │       AI AGENT RUNTIME DETECTOR        │
                       └───────────────────┬────────────────────┘
                                           │
                    Can the AI spawn sub-agents or workers?
                                           │
                 ┌─────────────────────────┴─────────────────────────┐
                 ▼ YES                                               ▼ NO
   ┌──────────────────────────────┐                    ┌──────────────────────────────┐
   │    MULTI-AGENT SWARM MODE    │                    │     SINGLE-AGENT AUTO MODE   │
   ├──────────────────────────────┤                    ├──────────────────────────────┤
   │ Spawns 5 parallel workers:   │                    │ Agent inspects all 6 pillars │
   │ • Security / Hardware Agent  │                    │ sequentially in a single     │
   │ • Database / State Agent     │                    │ thread, generating the full  │
   │ • UX / Insets Agent          │                    │ report and action plan.      │
   │ • Performance / Queue Agent  │                    └──────────────────────────────┘
   │ • Core Subsystems Agent      │
   │ Aggregates findings and      │
   │ assigns tasks to builders.   │
   └──────────────────────────────┘
```

---

## 📁 Repository Directory Structure

```text
├── README.md                                    # Master Suite Documentation
├── skills/
│   ├── website-architect/                       # 🌐 Website & Web App Skill
│   │   ├── SKILL.md
│   │   ├── commands/audit-website-readiness.md
│   │   └── references/website_architecture_and_ai_pitfalls.md
│   │   └── references/database_schema_ddl.sql
│   │
│   ├── mobile-app-architect/                    # 📱 Mobile Application Skill
│   │   ├── SKILL.md
│   │   ├── commands/audit-mobile-app-readiness.md
│   │   └── references/mobile_app_architecture_and_ai_pitfalls.md
│   │
│   ├── backend-system-architect/                # ⚙️ Backend & Microservice Skill
│   │   ├── SKILL.md
│   │   ├── commands/audit-backend-system-readiness.md
│   │   └── references/backend_system_architecture_and_ai_pitfalls.md
│   │
│   └── automation-workflow-architect/           # ⚡ Automation & Workflow Skill
│       ├── SKILL.md
│       ├── commands/audit-automation-workflow-readiness.md
│       └── references/automation_workflow_architecture_and_ai_pitfalls.md
```

---

## 📄 License
Released under the MIT License. Created by [vevaka2009-coder](https://github.com/vevaka2009-coder).
