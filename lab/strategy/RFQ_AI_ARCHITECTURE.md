# RFQ + AI Architecture — Resume Bullets, System Design Answer, Staff Extensions

**Purpose**

Turn the RFQ + AI-first architecture into:

1. **resume bullets** (ATS-friendly)
2. a **system design interview answer** (2–4 minutes)
3. how a **staff engineer** extends it (observability, scaling, failure modes)

This file assumes the implementation described in:

* **4G ENG RFQ System Flow — AI‑First Implementation**

---

## 1) Resume Bullets (ATS-Friendly)

Use these as-is or mix-and-match. Replace placeholders (e.g., latency, cost) once you have numbers.

### Option A — Senior Full‑Stack / AI‑Adjacency

* Built an **AI‑assisted RFQ pipeline** using **Next.js App Router** (Server Actions/Server Components), **FastAPI**, and **PostgreSQL (Supabase)** with a **single‑DB multi‑schema** design (`public` + `ai`).
* Implemented a **secure web→AI boundary**: Next.js **Server Actions** authenticate/validate and forward requests over HTTP to FastAPI, keeping **LLM keys server‑side** and enabling cost controls.
* Designed **failure‑safe enrichment**: RFQ persistence is authoritative; AI summarization/classification is **best‑effort** with **timeouts, retries, and AI_pending/skipped states** to protect conversions.
* Added **guardrails** (rate limits, spam gates, budget checks) to reduce unnecessary AI calls and control spend.

### Option B — AI Systems / Platform Lean

* Designed a two‑service **web layer + AI service** architecture: Next.js orchestrates UX/auth; FastAPI owns AI compute (summarization, classification, optional RAG), both sharing a single Postgres instance.
* Modeled AI telemetry and traceability via `ai.rag_runs` records (prompt versioning, confidence, timestamps) to support audits and iterative prompt improvements.
* Introduced a clear runtime strategy: **Pattern 1** (Server Action → FastAPI) for mutations, **Pattern 2** (Server Component → FastAPI/DB) for fast SSR reads, **Pattern 3** (Client → FastAPI) reserved for streaming.

### Option C — More Traditional Full‑Stack

* Delivered a production RFQ workflow with SSR and server‑side validation, integrating a dedicated AI microservice for enrichment while maintaining a single source of truth in Postgres.
* Implemented resilient request handling with graceful degradation: users always receive confirmation even if AI services are unavailable.

> Tip: In interviews, pair one bullet with a **quick metric** later (p95 latency, AI call rate reduction, conversion impact, error rate).

---

## 2) System Design Interview Answer (2–4 minutes)

Use this as your spoken script.

### 2.1 Problem statement

“I designed an RFQ intake system where users submit requests and we automatically generate an AI summary and routing tags. The key constraints were: protect secrets, keep latency acceptable, control AI cost, and never allow AI failures to block RFQ submission.”

### 2.2 High-level architecture

“I split the system into a **web layer** and an **AI/compute layer**:

* **Next.js App Router** handles the website UX, SSR, auth/cookies, and server-side mutations.
* **FastAPI** hosts AI logic—summarization, classification, and optional lightweight RAG.
* Both share **one Postgres database** (Supabase) using **two schemas**: `public` for user-facing RFQ data and `ai` for AI runs and logs.”

### 2.3 Request flow (key boundary)

“On submit, the browser calls a **Next.js Server Action**. The Server Action validates input, authenticates the user/session, writes the RFQ to `public.rfq_requests`, then calls FastAPI over HTTP to run AI enrichment. FastAPI writes a run record to `ai.rag_runs` and updates the RFQ with `ai_summary`, `ai_tags`, and a routing hint. The confirmation page is server-rendered from the DB.”

### 2.4 Failure modes and reliability

“A core design decision is **RFQ persistence is authoritative**—AI is best-effort. If FastAPI or the LLM provider times out, the RFQ is still accepted, the UI shows ‘AI pending’, and the system can retry asynchronously or via an admin re-run. This protects conversions and avoids user-visible failures.”

### 2.5 Security and cost controls

“LLM keys never touch the browser. I added gates: minimum message length, spam heuristics, rate limits per IP/email, and a budget guardrail. If the system is degraded or budgets are exceeded, AI enrichment can be skipped or deferred while still capturing the RFQ.”

### 2.6 Scaling approach

“Scale the web layer and AI layer independently. Next.js scales with web traffic; FastAPI scales with AI workloads. The DB remains the source of truth; AI tables are append-heavy and can be optimized separately.”

### 2.7 Tradeoffs

“The main tradeoff is introducing a second service adds operational overhead, but it pays off when AI logic evolves quickly, needs background jobs, or must scale independently from the UI.”

---

## 3) Staff Engineer Extensions (Observability, Scaling, Failure Modes)

This is how you extend the v1 design to production-grade v2/v3.

### 3.1 Observability (must-have)

**Metrics**

* RFQ submit rate, success rate
* AI enrichment rate (% of RFQs enriched)
* p50/p95/p99 latency for:

  * Server Action
  * FastAPI endpoint
  * LLM provider call
* AI failure rate by cause (timeout, provider error, rate limit)
* Cost metrics:

  * calls/day
  * tokens/day
  * $/day and $/RFQ

**Tracing**

* Add a `request_id` generated in Next.js Server Action.
* Propagate `request_id` to FastAPI via header.
* Store `request_id` in `ai.rag_runs`.

**Logging**

* Structured JSON logs in both services including:

  * request_id, rfq_id
  * user/email hash
  * prompt_version, model
  * latency_ms, status

### 3.2 Reliability & failure modes (beyond v1)

**Timeouts**

* Server Action → FastAPI: 3–8s with circuit breaker behavior.
* FastAPI → LLM: short timeout + 1 retry max.

**Circuit breaker**

* If FastAPI or provider failures exceed X% over Y minutes:

  * automatically switch AI mode to **DEFER** (skip in request path)

**Idempotency**

* RFQ submission idempotency key (email+hash(message)+timestamp bucket) to avoid duplicates.
* AI enrichment idempotency key per rfq_id + prompt_version.

**Queues / async jobs (v2)**

* Move AI enrichment off the synchronous path:

  * Server Action writes RFQ + enqueues job
  * Worker calls FastAPI/LLM
  * UI polls or uses SSE for completion

### 3.3 Scaling strategy

**Web layer (Next.js)**

* Cache read pages where possible.
* Keep server actions fast; offload heavy work.

**AI layer (FastAPI)**

* Horizontal scale FastAPI behind a load balancer.
* Separate worker pool for AI jobs.
* Add concurrency control per model/provider.

**Database**

* Partition/retention policy for `ai.rag_runs` (append-heavy):

  * keep 30–90 days hot
  * archive old runs
* Add indexes on `rfq_id`, `created_at`, `request_id`.

### 3.4 Security extensions

* Ensure FastAPI endpoints require:

  * internal network access OR
  * signed requests from Next.js (HMAC header) OR
  * OAuth/JWT between services
* Avoid passing raw PII into logs; hash emails.

### 3.5 Product / quality controls

* Prompt versioning: store `prompt_version` in `ai.rag_runs`.
* Offline evaluation set: sample RFQs to measure classification accuracy.
* Human override: allow manual routing changes.

---

## 4) Quick “Tell Me About a Project” Story (STAR-ish)

* **Situation:** Needed reliable RFQ intake with AI summarization/routing.
* **Task:** Keep secrets safe, control cost, ensure RFQ success even if AI fails.
* **Action:** Next.js Server Actions as secure gateway; FastAPI for AI; single Postgres multi-schema; best-effort enrichment with retries + cost gates.
* **Result:** Reliable pipeline with graceful degradation; scalable separation of web vs AI compute; audit-ready AI run tracking.

---

## 5) Replace-With-Metrics TODO (when ready)

Fill these in after you implement:

* p95 RFQ submit latency: ___ ms
* AI enrichment rate: ___%
* AI failure rate: ___%
* Cost per RFQ (avg): $___
* Spam/duplicate AI calls avoided: ___% reduction

**Status:** Ready to paste into resume, interviews, and system design narratives.
