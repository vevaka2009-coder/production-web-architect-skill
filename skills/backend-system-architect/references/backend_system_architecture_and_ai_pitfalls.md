# Backend System Production Architecture & AI "Vibe-Coding" Field Guide
### Distributed Systems, Reliability Engineering, and Microservice Anti-Patterns

---

## Executive Summary: The Backend "Vibe-Coding" Trap

When AI models synthesize backend services and APIs (Express, Fastify, Go, FastAPI, Spring Boot), they generate controllers and database models that succeed under isolated single-client testing.

However, in production environments (Kubernetes, AWS ECS, Docker clusters, serverless containers), backends run as distributed multi-instance topologies. AI assistants routinely overlook the distributed systems realities:
- Pods are constantly terminated, rescheduled, and scaled by orchestrators.
- Downstream microservices and third-party APIs fail, causing cascading failure storms.
- Multiple instances concurrently update shared database records without distributed coordination.

```
                               THE BACKEND VIBE-CODING TRAP
    Single-Client Velocity
         ▲
         │      /────────────────────────── AI Vibe-Coding (Happy-Path Single Instance)
         │     /
         │    /
         │   /
         │  /                              CRITICAL PRODUCTION FAILURES:
         │ /                               - Dropped HTTP requests during Kubernetes pod deploys
         │/                                - Thundering-herd cascading outages on DB restart
         │                                 - Double-charging / race conditions under concurrency
         │───────┬───────────────────────  - Rogue queries locking tables for hours
         │       │ Production Deployment   - OOM crashes from unbounded JSON body payloads
         │       ▼
         └─────────────────────────────────► Multi-Instance Distributed Scale
```

---

## Part 1: Top 20 Backend AI & Vibe-Coding Blindspots

### 1. Missing Graceful Shutdown (SIGTERM / SIGINT)
* **The Pitfall:** Calling `app.listen(PORT)` without trapping termination signals.
* **Failure Mode:** In Kubernetes or container environments, when rolling out a new deployment, orchestrators send `SIGTERM`. If unhandled, the process terminates immediately, abruptly dropping hundreds of in-flight user payments, file uploads, and active database transactions.
* **Remedy (Node.js / TypeScript):**
  ```typescript
  import http from "http";
  import { pool } from "./db";

  const server = http.createServer(app);

  function gracefulShutdown(signal: string) {
    console.log(`Received ${signal}. Starting graceful shutdown...`);
    
    // 1. Stop accepting new connections
    server.close(async () => {
      console.log("HTTP server closed.");
      try {
        // 2. Drain and close database pool
        await pool.end();
        console.log("Database connection pool drained.");
        process.exit(0);
      } catch (err) {
        console.error("Error during resource teardown:", err);
        process.exit(1);
      }
    });

    // 3. Force exit if cleanup takes longer than 30s
    setTimeout(() => {
      console.error("Graceful shutdown timeout exceeded. Forcing exit.");
      process.exit(1);
    }, 30000).unref();
  }

  process.on("SIGTERM", () => gracefulShutdown("SIGTERM"));
  process.on("SIGINT", () => gracefulShutdown("SIGINT"));
  ```

---

### 2. Conflating Liveness and Readiness Probes in Kubernetes
* **The Pitfall:** Pointing both `livenessProbe` and `readinessProbe` to a single `/health` endpoint that queries the database.
* **Failure Mode:** If the database undergoes a temporary 10-second failover, the liveness probe fails across all application pods simultaneously. Kubernetes interprets this as a fatal crash loop and restarts all pods concurrently, worsening the outage and overloading the database upon recovery.
* **Remedy:** Decouple Liveness from Readiness:
  - **Liveness Probe (`/healthz/liveness`):** Checks only if the process is responsive and not deadlocked (returns 200 without querying external dependencies).
  - **Readiness Probe (`/healthz/readiness`):** Checks if the service is ready to accept traffic (verifies DB ping, Redis connection, and warmup caches). If it fails, Kubernetes stops sending traffic to that pod without killing it.

---

### 3. Concurrency Race Conditions & Missing Distributed Locks
* **The Pitfall:** Reading a balance or inventory count in application memory, performing a check in JavaScript/Python, and writing back:
  ```typescript
  const account = await db.account.findUnique({ where: { id } });
  if (account.balance >= amount) {
    await db.account.update({ where: { id }, data: { balance: account.balance - amount } });
  }
  ```
* **Failure Mode:** Two concurrent requests arrive at the same millisecond across two different server pods. Both read balance = $100. Both approve $100 withdrawals. The user withdraws $200 with only $100 in their account.
* **Remedy:** Use atomic SQL operations or Redis distributed locks (Redlock):
  ```sql
  -- Atomic SQL execution with conditional update
  UPDATE accounts 
  SET balance = balance - 100 
  WHERE id = $1 AND balance >= 100 
  RETURNING balance;
  ```

---

### 4. Circuit Breakers on External Microservices
* **The Pitfall:** Issuing bare HTTP requests to downstream microservices with default infinite timeouts.
* **Failure Mode:** When downstream Service B slows down from 50ms to 15 seconds, all incoming worker threads on Service A block waiting for Service B. Within 60 seconds, Service A runs out of socket connections, memory, and thread pool workers, completely crashing.
* **Remedy:** Wrap all inter-service communications in a Circuit Breaker with explicit request timeouts:
  ```typescript
  import CircuitBreaker from "opossum";

  async function callPaymentGateway(payload: any) {
    return await fetch("https://api.payment.com/v1/charge", {
      method: "POST",
      body: JSON.stringify(payload),
      signal: AbortSignal.timeout(3000), // 3s hard timeout
    });
  }

  const breaker = new CircuitBreaker(callPaymentGateway, {
    timeout: 3000,
    errorThresholdPercentage: 50,
    resetTimeout: 10000,
  });

  breaker.fallback(() => ({ status: "degraded", message: "Service temporarily unavailable" }));
  ```

---

### 5. Missing Statement and Lock Timeouts
* **The Pitfall:** Running database queries without global statement timeouts.
* **Failure Mode:** An unindexed query or an accidental cartesian join blocks a table lock. Subsequent writes queue behind it, exhausting the connection pool and taking down the entire database.
* **Remedy:** Configure strict timeouts at the connection pool level:
  ```sql
  SET statement_timeout = '5000'; -- 5 seconds maximum query execution
  SET lock_timeout = '2000';      -- 2 seconds maximum wait for table locks
  ```

---

### 6. Distributed Tracing & W3C Tracecontext Header Propagation
* **The Pitfall:** Logging unstructured plain text with `console.log("Error occurred")`.
* **Failure Mode:** In a microservice mesh, tracking a request across 4 different services is impossible without correlation IDs.
* **Remedy:** Propagate W3C `traceparent` headers using OpenTelemetry SDK to correlate logs, metrics, and distributed spans end-to-end.

---

## Part 2: Backend System Production Checklist
- [ ] SIGTERM & SIGINT graceful shutdown handlers implemented.
- [ ] In-flight requests drained before process exit.
- [ ] Liveness and Readiness probes decoupled.
- [ ] Database statement and lock timeouts enforced.
- [ ] Distributed locks (Redis Redlock) or atomic SQL used for shared resources.
- [ ] Circuit breakers and request timeouts on all outbound HTTP/gRPC calls.
- [ ] Structured JSON logging with injected trace IDs.
- [ ] Request body size limits enforced to prevent buffer overflow attacks.
- [ ] Docker container executes under an unprivileged non-root user.
