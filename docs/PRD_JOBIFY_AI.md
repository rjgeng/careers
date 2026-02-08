# Product Requirements Document (PRD)

## Product Name
**Jobify‑AI — Career System Control Plane**

---

## 1. Purpose

Jobify‑AI is a **career system control plane**, not an auto‑apply tool.

It implements a subset of the career‑system specification defined in this repository and turns it into an interactive, AI‑assisted application.

The product helps a user:
- evaluate roles consistently
- reduce noise in job search decisions
- prepare faster for applications and conversations

---

## 2. Non‑Goals (Explicit)

Jobify‑AI will **not**:
- auto‑apply to jobs
- scrape job boards at scale
- fabricate experience or resume content
- bypass ATS or platform policies

These are intentional constraints.

---

## 3. Target User

Primary user:
- Senior Individual Contributor
- Backend / Full‑stack / Systems‑oriented
- Treats career transitions as an engineering problem

Secondary users (future):
- ICs who want structure without automation abuse

---

## 4. Core Problem Statement

Job search behaves like a noisy system:
- inconsistent role evaluation
- repeated manual parsing of job descriptions
- unstructured preparation
- loss of signal across applications and conversations

Jobify‑AI reduces randomness by enforcing **structure and repeatability**.

---

## 5. Product Principles

- **Human‑in‑the‑loop**: AI assists; user decides
- **Structure over volume**: fewer, better decisions
- **Compliance first**: user‑provided inputs only
- **Signal clarity**: surface red flags early

---

## 6. MVP Feature Set (v0)

### 6.1 Job Intake
- User pastes job description text or URL
- System parses into structured fields:
  - title
  - level
  - stack
  - responsibilities
  - requirements

### 6.2 Role Evaluation
- Fit score based on user role targets
- Red‑flag detection (vague scope, unrealistic stack, agency spam)
- Explicit accept / reject decision

### 6.3 Resume Alignment (Advisory)
- Keyword alignment suggestions only
- No automatic resume rewriting
- Output is hints, not generated resumes

### 6.4 Conversation Preparation
- Recruiter message drafts (short / standard)
- Follow‑up reminder generation

---

## 7. Data Model (High Level)

- Job
- Evaluation
- MessageDraft
- FollowUp
- Notes

All data is user‑owned and editable.

---

## 8. AI Responsibilities

AI is used for:
- text parsing
- summarization
- pattern detection
- draft generation

AI is **not** authoritative.

---

## 9. Architecture (Conceptual)

- Next.js App Router
- Server Actions for AI calls
- Prisma for persistence
- Auth via Clerk
- AI via OpenAI / compatible LLM

---

## 10. Safety & Compliance

- User‑initiated actions only
- No background scraping
- No credential storage
- No automated submissions

---

## 11. Success Metrics (Internal)

- Reduced time to evaluate a role
- Fewer low‑quality applications
- Faster preparation for recruiter conversations

---

## 12. Future Extensions (Out of Scope for v0)

- Multi‑user support
- Analytics across cohorts
- Resume versioning
- Market‑level insights

---

## 13. Positioning Statement

Jobify‑AI is not a job‑hunting bot.

It is a **structured assistant for career decision‑making**, built with the same discipline as production systems.

