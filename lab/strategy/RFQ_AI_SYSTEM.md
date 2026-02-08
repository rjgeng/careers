# RFQ AI System — Resume, Interview, and Staff-Level Extensions

**Purpose**

This document translates the RFQ AI system into:

1. **Resume bullets** (ATS‑safe, senior‑level)
2. **System design interview answer** (clear, structured)
3. **Staff‑level extensions** (observability, scaling, failure modes)

It is derived from:

* *4G ENG RFQ System Flow — AI‑First Implementation*

---

## 1. Resume Bullets (Senior / Staff‑Ready)

Use these verbatim or lightly adapt them.

### Core Architecture

* Designed and implemented an **AI‑assisted RFQ pipeline** using **Next.js App Router** (web layer) and **FastAPI** (AI/compute layer), sharing a **single PostgreSQL database** with multi‑schema isolation.
* Defined a clear **web vs AI service boundary**, routing all AI requests through server‑side execution (Server Actions / Server Components) to protect secrets and control cost.

### Data & Reliability

* Modeled RFQ workflows with **authoritative writes** (RFQ persistence) and **best‑effort AI enrichment**, ensuring business operations remain available during AI degradation.
* Implemented **partial‑success semantics** (AI pending / failed / skipped) to prevent AI outages from impacting user trust or core workflows.

### AI Integration

* Built AI summarization and classification as a **supporting feature**, including optional lightweight RAG, with explicit **timeout, retry, and budget guardrails**.
* Introduced **cost‑control gates** (signal thresholds, rate limits, budget caps) to prevent unnecessary LLM invocations.

### Systems Thinking

* Applied **production‑grade patterns**: single source of truth, service isolation, schema ownership, and forward‑compatible extension points for background workers and agents.

---

## 2. System Design Interview Answer (Canonical)

### Problem

Design an RFQ system where AI assists with summarization and routing without compromising reliability or cost.

### High‑Level Architecture

```
Browser
  ↓
Next.js (Web Layer)
  - Auth, validation, SSR
  - Server Actions / Server Components
  ↓ HTTP
FastAPI (AI Layer)
  - Summarization
  - Classification
  - Optional RAG
  ↓
PostgreSQL (Single DB, multi‑schema)
```

### Key Design Decisions

* **Separation of concerns**: Next.js owns UX, auth, and orchestration; FastAPI owns AI compute.
* **Single database**: one Postgres instance with schema‑level ownership avoids duplication while preserving isolation.
* **AI as best‑effort**: RFQ persistence is authoritative; AI enrichment is optional and non‑blocking.

### Request Flow

1. User submits RFQ from the browser.
2. Next.js Server Action validates, authenticates, and stores the RFQ.
3. Next.js forwards the request to FastAPI over HTTP.
4. FastAPI performs AI summarization/classification and writes results.
5. Next.js Server Component renders the confirmation view with AI output if available.

### Failure Handling

* AI timeouts or errors never block RFQ submission.
* AI failures are recorded and surfaced as “pending” to the user.
* Retries are handled asynchronously, never in the user request path.

### Cost Control

* AI calls gated by signal quality, rate limits, and daily budget caps.
* System degrades gracefully by skipping AI when limits are exceeded.

**Why this works:** The business pipeline remains reliable, while AI adds value opportunistically.

---

## 3. Staff‑Level Extensions (How This Evolves)

This section shows how a **staff engineer** would extend the same system without changing its core principles.

---

### 3.1 Observability

Add structured telemetry across boundaries:

* **Request tracing**

  * Correlate RFQ ID across Next.js → FastAPI → DB
* **Metrics**

  * RFQs submitted / minute
  * AI calls / minute
  * AI success vs failure rate
  * P95 latency (web vs AI)
* **Logging**

  * Prompt version, model, cost estimate per AI run

This enables:

* cost forecasting
* prompt regression detection
* fast incident diagnosis

---

### 3.2 Scaling Strategy

* **Web layer (Next.js)**

  * Scales horizontally with traffic
  * SSR cached where possible

* **AI layer (FastAPI)**

  * Scales independently based on AI load
  * Can add background workers for ingestion or retries

* **Database**

  * Read replicas for analytics / dashboards
  * Separate AI‑heavy queries into `ai.*` schema

---

### 3.3 Failure Modes & Degradation

Explicitly design for:

* **LLM provider outage** → skip AI, mark RFQs pending
* **FastAPI partial outage** → accept RFQs, defer enrichment
* **Budget exhaustion** → automatically disable AI paths

Golden rule:

> Business workflows must continue even if AI is fully unavailable.

---

### 3.4 Future Evolution (Without Rewrite)

Because the boundary is clean:

* Add async queues (Celery / RQ) behind FastAPI
* Add richer RAG pipelines
* Introduce agent workflows
* Replace or add new LLM providers

All without changing the Next.js UI or RFQ persistence logic.

---

## 4. One‑Line Staff Summary

> “We treat AI as an assistive, cost‑bounded service behind a stable web layer, preserving reliability while allowing AI capability to evolve independently.”

---

**Status:** Resume‑ready, interview‑ready, and staff‑scalable.
