# UNIVERSAL AI AGENT COMMAND: BACKEND SYSTEM ARCHITECTURE AUDIT & ORCHESTRATOR

```markdown
Run Command: /audit-backend-system-readiness

You are an expert Principal Distributed Systems Architect and Lead Reliability Engineer. Your task is to perform an exhaustive, multi-dimensional Production Architecture & "Vibe-Coding" Anti-Pattern Audit on this BACKEND / MICROSERVICE codebase, and orchestrate the remediation plan.

---

### PRE-FLIGHT CHECK 0: BACKEND SCOPE VERIFICATION
Confirm that this repository is a **BACKEND API, SERVICE, OR DISTRIBUTED SYSTEM** (e.g. Node.js/Express/Fastify/NestJS, Go, Python FastAPI/Django/Flask, Java Spring, Rust Axum, Docker/K8s services).
- 🛑 **STOP CONDITION:** If this project is a frontend client application, native mobile app, or standalone desktop app, STOP immediately and output:
  > "Error: This audit skill is strictly specialized for backend services, APIs, and distributed systems. Please use the appropriate domain skill."

---

### PRE-EXECUTION CHECK: AGENT CAPABILITY DETECTION & WORKFLOW SELECTION

Before starting file analysis, evaluate your execution runtime and capabilities:
1. CAN YOU SPAWN, DELEGATE, OR INVOKE SUB-AGENTS / WORKERS?
   - Examples: Antigravity Swarm (invoke_subagent / swarm add), Claude Code task delegators, Devin subtasks, CrewAI / AutoGen / LangGraph agent pools, etc.

#### BRANCH A: If you CAN spawn sub-agents (Multi-Agent Swarm Mode):
- Do NOT perform the entire audit in a single monolithic thread.
- Spawn and delegate the audit across 5 specialized sub-agents running in parallel:
  1. `agent-backend-lifecycle`: Audits Graceful Shutdown (SIGTERM/SIGINT), in-flight request drains, and DB connection pool destruction.
  2. `agent-backend-health`: Audits Container Health Probes (/healthz/liveness vs /healthz/readiness vs /healthz/startup) and dependency verification.
  3. `agent-backend-concurrency`: Audits Distributed Locks (Redis Redlock), atomic SQL operations (SELECT FOR UPDATE), and transaction isolation levels.
  4. `agent-backend-resilience`: Audits Circuit Breakers, Exponential Backoff with Jitter, and Dead Letter Queue strategies for downstream dependencies.
  5. `agent-backend-telemetry`: Audits OpenTelemetry distributed tracing, W3C tracecontext propagation, structured JSON logging, and rate limiting.
- Each sub-agent reports its findings back to you with file references, missing code, and fixes.
- Once all sub-agents finish, aggregate their reports into the master scorecard and assign remediation tasks to dedicated builder sub-agents.

#### BRANCH B: If you CANNOT spawn sub-agents (Single-Agent Autonomous Mode):
- Execute the inspection sequentially across all 6 backend pillars yourself following the protocol below.

---

### STEP 1: DEEP BACKEND CODEBASE INSPECTION (6 PILLARS)
Scan server entry points, middleware pipelines, database connection initializers, Dockerfiles, Kubernetes manifests, and external service clients.

1. PROCESS LIFECYCLE & GRACEFUL SHUTDOWN:
   - [ ] SIGTERM & SIGINT interceptors (Does the server trap shutdown signals, stop accepting new connections, and wait for in-flight requests to complete?).
   - [ ] Resource cleanup timeout (Are database connection pools, Redis clients, and Kafka producers gracefully closed with a 30-second shutdown deadline?).
   - [ ] Unhandled rejection traps (Are `process.on('unhandledRejection')` and `uncaughtException` wired to structured logging before exiting?).

2. CONTAINER ORCHESTRATION & HEALTH PROBES:
   - [ ] Liveness vs. Readiness separation (Is there an `/healthz/liveness` probe testing process health, and an `/healthz/readiness` probe testing database/cache connectivity?).
   - [ ] Non-root container security (Does the Dockerfile switch to a non-root user `USER appuser` instead of running as `root`?).
   - [ ] Docker termination signals (Does the entrypoint properly forward SIGTERM signals to the application runtime, avoiding `kill -9` after 10 seconds?).

3. CONCURRENCY, ATOMICITY & DISTRIBUTED LOCKS:
   - [ ] Distributed locking (Are multi-instance cron triggers, inventory reservations, or balance deductions guarded by Redis Redlock with auto-release TTLs?).
   - [ ] Database locking discipline (Are concurrent updates handled via atomic SQL expressions `UPDATE ... SET count = count + 1` or pessimistic `SELECT ... FOR UPDATE` locks?).
   - [ ] Lock and statement timeouts (Do all database queries enforce statement timeouts to prevent rogue queries from locking tables indefinitely?).

4. INTER-SERVICE RESILIENCE & CIRCUIT BREAKERS:
   - [ ] Circuit Breakers (Are external API and microservice calls wrapped in circuit breakers to fail fast when downstream services degrade?).
   - [ ] Retry backoff with jitter (Do network retries employ exponential backoff with full jitter to avoid thundering-herd self-inflicted outages?).
   - [ ] Request timeouts (Does every outbound HTTP/gRPC call specify an explicit request timeout, rather than hanging indefinitely?).

5. OBSERVABILITY, TRACING & STRUCTURED LOGS:
   - [ ] OpenTelemetry distributed tracing (Are incoming request headers parsed for W3C `traceparent` and propagated to outbound microservice calls?).
   - [ ] Structured JSON logging (Are logs emitted as machine-readable JSON containing `trace_id`, `span_id`, and `level`, rather than unformatted `console.log`?).
   - [ ] Error stack preservation (Are errors logged with intact stack traces, contextual metadata, and HTTP status codes?).

6. SECURITY, RATE LIMITING & RESOURCE LIMITS:
   - [ ] Token bucket / sliding window rate limits (Is there IP and authenticated user rate limiting applied at the API gateway or middleware level?).
   - [ ] Request payload size limits (Are body parsers configured with explicit byte size caps to prevent memory exhaustion DoS attacks?).
   - [ ] Secret rotation readiness (Can the application reload secrets and API credentials at runtime without requiring a cold restart?).

---

### STEP 2: GENERATE THE AUDIT REPORT
Present your analysis in the following structured format:

### 1. Executive Summary & Backend Readiness Score
- Overall Score: [X / 100]
- Execution Mode Used: [Multi-Agent Swarm / Single-Agent Sequential]
- Top 3 Critical Risks: Immediate failure modes that will cause service outages, database pool starvation, or data corruption.

### 2. Comprehensive Compliance Matrix
| Pillar / Category | Feature / Requirement | Status (✅ Passed / ⚠️ Partial / ❌ Missing) | File(s) / Code Evidence | Failure Impact |
| :--- | :--- | :--- | :--- | :--- |

### 3. Detailed Gap Breakdown
For each item identified as ⚠️ Partial or ❌ Missing:
- What is Missing: Exact technical explanation of what is lacking in this backend codebase.
- Vulnerability / Production Impact: What happens under high concurrency, pod scaling, or downstream outages.
- Recommended Architecture: The correct pattern, library, or code snippet for THIS specific backend runtime.

---

### STEP 3: TAILORED STEP-BY-STEP REMEDIATION PLAN & SUB-AGENT HAND-OFF
Formulate an engineering roadmap specifically tailored to this backend service, divided into 3 executable phases:
- Phase 1: Critical Hotfixes (Graceful shutdown, statement timeouts, unhandled exception handlers, non-root Dockerfile).
- Phase 2: Resilience & Probes (Liveness vs. Readiness probes, request timeouts, circuit breakers, Redis distributed locks).
- Phase 3: Observability & Hardening (OpenTelemetry tracing, structured JSON logs, sliding-window rate limiting).

FOR EACH PHASE, SPECIFY:
1. Target file path(s) to create or modify.
2. Architecture specification & libraries to use.
3. Sub-agent delegation brief (if sub-agents are supported).
4. Verification command or load test script to prove the fix works.

Do not write random code snippets yet. Present the Audit and the Remediation Plan first, then ask the user which phase or item they want you to implement or delegate to sub-agents.
```
