---
name: automation-workflow-architect
description: Exclusively built for background workers, data pipelines, scheduled jobs, crawlers, and workflow engines (BullMQ, Celery, Temporal, Apache Airflow, Cron, n8n, Python automation pipelines). Built for AI project builders and vibe-coders building automations. Detects, reports, and corrects critical automation flaws—including non-idempotent job retries (duplicate actions/double-billing), missing Dead Letter Queues (DLQ), zombie worker crash detection, API rate limit bans, clock drift/timezone bugs, silent exception swallowing, and memory leaks from unbounded batch buffers.
metadata:
  author: vevaka2009-coder
  version: 1.0.0
  tags:
    - automations-only
    - background-jobs
    - queues-and-workers
    - workflow-engines
    - vibe-coding
    - idempotency
---

# Automation & Workflow Architect & Vibe-Coding Guard (Automations Only)

> ⚠️ **STRICT SCOPE NOTICE: AUTOMATIONS & WORKFLOW ENGINES ONLY**  
> This skill is **strictly for background automation pipelines, queues, workers, crawlers, and scheduled tasks** (BullMQ, Celery, Temporal, Airflow, Python scripts, Cron).  
> **DO NOT USE FOR:** Web frontend UIs, native mobile apps, or synchronous REST API handlers. It specifically audits asynchronous job lifecycles, idempotency guarantees, retry policies, backpressure handling, queue monitoring, and worker crash heartbeats.

Built specifically for **AI project builders and vibe-coders** creating automated background workflows, scheduled scrapers, data pipelines, and queue workers. It automatically inspects your automation codebase, identifies critical flaws that cause infinite retry loops, duplicate data processing, or IP bans, and provides the production-grade code and architecture plans to fix them.

## When to Activate This Skill
- When building or reviewing a **background worker, job queue, automated pipeline, or cron automation**.
- When an automation works once on small sample data, but fails when scaled to thousands of jobs.
- When jobs fail and silently disappear without alerts or Dead Letter Queues (DLQ).
- When investigating double-processing, duplicate email sends, or API rate limit blocks.

## What It Does
1. **Detects What AI Missed in Your Automations:** Scans the codebase across 6 essential automation pillars and 20 critical asynchronous failure modes.
2. **Explains the Gaps:** Reports findings in clear technical terms with exact file locations and failure impacts (`✅ Passed`, `⚠️ Partial`, `❌ Missing`).
3. **Corrects & Builds the Missing Pieces:** Generates tailored, production-grade implementations for your queue or workflow framework.
4. **Multi-Agent Orchestration:** Dispatches parallel worker sub-agents (`agent-auto-idempotency`, `agent-auto-dlq`, `agent-auto-rate-limits`, `agent-auto-heartbeats`, `agent-auto-memory`) when running in multi-agent environments.

## Quick Command
To run an instant audit on your automation codebase, run the prompt in `commands/audit-automation-workflow-readiness.md`:
```markdown
/audit-automation-workflow-readiness
```
