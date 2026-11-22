---
name: backend-system-architect
description: Exclusively built for backend services, distributed systems, APIs, and microservices (Node.js, Go, Python FastAPI/Django, Java Spring, Rust, Docker, Kubernetes). Built for AI project builders and vibe-coders building backends. Detects, reports, and corrects critical system architecture blindspots—including missing graceful shutdown (SIGTERM), broken Kubernetes liveness vs. readiness probes, unhandled distributed race conditions (Redis Redlock), missing circuit breakers, connection pool starvation, secret rotation, rate limiting, and structured OpenTelemetry tracing.
metadata:
  author: vevaka2009-coder
  version: 1.0.0
  tags:
    - backend-systems-only
    - microservices
    - api-architecture
    - distributed-systems
    - vibe-coding
    - reliability
---

# Backend System Architect & Vibe-Coding Guard (Backend Systems Only)

> ⚠️ **STRICT SCOPE NOTICE: BACKEND SYSTEMS ONLY**  
> This skill is **strictly for backend APIs, microservices, and distributed systems** (Node.js, Go, Python, Java, Docker, Kubernetes).  
> **DO NOT USE FOR:** Frontend client UI code, native mobile apps, or simple automation scripts. It specifically audits backend server resilience, graceful shutdown lifecycles, database connection pool management, distributed locks, health probes, and inter-service telemetry.

Built specifically for **AI project builders and vibe-coders** creating backend APIs and microservices. It automatically inspects your backend repository, identifies system-level architectural flaws that cause silent data corruption or cascading outages, and provides the production-grade code and architecture plans to fix them.

## When to Activate This Skill
- When building or reviewing a **backend API, microservice, or distributed server**.
- Before deploying backend services to Kubernetes, AWS ECS, Fly.io, or Railway.
- When an API works fine with one user, but faces connection pool exhaustion or race conditions under concurrency.
- When auditing server lifecycle management: Graceful Shutdown (SIGTERM/SIGINT), Liveness vs. Readiness probes, Circuit Breakers, or OpenTelemetry distributed tracing.

## What It Does
1. **Detects What AI Missed in Your Backend:** Scans the codebase across 6 essential backend system pillars and 20 critical distributed systems failure modes.
2. **Explains the Gaps:** Reports findings in clear technical terms with exact file locations and failure impacts (`✅ Passed`, `⚠️ Partial`, `❌ Missing`).
3. **Corrects & Builds the Missing Pieces:** Generates tailored, production-grade implementations for your backend language and framework.
4. **Multi-Agent Orchestration:** Dispatches parallel worker sub-agents (`agent-backend-lifecycle`, `agent-backend-concurrency`, `agent-backend-resilience`, `agent-backend-telemetry`, `agent-backend-security`) when running in multi-agent environments.

## Quick Command
To run an instant audit on your backend codebase, run the prompt in `commands/audit-backend-system-readiness.md`:
```markdown
/audit-backend-system-readiness
```
