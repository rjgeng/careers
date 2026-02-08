# ATS / LinkedIn Parsing Playbook (Canonical + Role-Family Variants)

Owner: Rongjun Geng  
Goal: Keep resume parser-safe, minimize iteration, and avoid per-company tailoring.

---

## 0) One mental model (pin this)

**Resume = serialization format for a candidate object.**  
Machines parse first; humans read second.

Pipeline:

PDF/DOCX → Text extraction → Section detection → Token indexing → Candidate record → Ranking/Visibility

---

## 1) What is “new” vs “not new”

### Not new
- ATS parsing is conservative and rule-based (keywords + section recognition)
- LinkedIn indexing is token-driven

### New (impact)
- AI-assisted filtering reduces human review
- Lower error tolerance → small parsing mistakes become visibility loss

**Conclusion:** Same mechanics, higher stakes.

---

## 2) Canonical Resume (Freeze)

### Canonical file
- `canonical_ai_systems_engineer.pdf`
- Also keep source: `canonical_ai_systems_engineer.docx` (or Google Doc)

### Canonical rules (do not break)
- One column
- Standard headers (SUMMARY, CORE SKILLS, EXPERIENCE, EDUCATION)
- No tables / text boxes / columns / icons for structure
- Dates in consistent format (e.g., `Aug 2015 – Present`)
- Skills as plain tokens (not graphics)

**Change policy:** Only update canonical when:
- New major project/impact
- New role/title shift
- Every 6–12 months

---

## 3) Self-test (do once per major change)

### LinkedIn parse test
1. Upload resume / use profile auto-fill
2. Check extracted:
   - Title
   - Company + role
   - Dates
   - Skills

If LinkedIn parses correctly, most ATS will too.

---

## 4) Role-family variants (NOT per company)

We maintain 2–3 variants, each changing <5% text.

### Variant A — Applied AI Systems Engineer (Meta-leaning)
**Title:**
AI Systems Engineer | Applied LLM Platforms

**Minimal adds:**
- SUMMARY (one line):
  “Experience deploying applied machine-learning and LLM systems used by internal and external users at scale.”
- CORE SKILLS tokens:
  “Machine Learning, Distributed systems”

**Use when:**
- Meta-style “Applied AI” / product AI systems
- Roles mentioning ML + production + platform

---

### Variant B — AI Infrastructure / Systems Engineer (OpenAI-leaning)
**Title:**
AI Systems Engineer | LLM Infrastructure & Inference

**Minimal adds:**
- 4G ENG bullet (one bullet):
  “Designed reliable LLM inference services with streaming, concurrency control, and cost-aware routing.”
- Optional token (only if true/space allows):
  “Inference optimization”

**Use when:**
- Platform / infra / inference / performance heavy
- Less frontend, more systems correctness

---

### Variant C — AI Platform Engineer (Anthropic-leaning)
**Title:**
AI Systems Engineer | AI Platforms & Agentic Systems

**Minimal adds:**
- SUMMARY (one line):
  “Focused on safe, interpretable AI platform design with clear separation between model reasoning and system authority.”
- CORE SKILLS tokens:
  “AI agents, Evaluation pipelines”

**Use when:**
- Agent/tool-use, eval, reliability, safety framing
- “Responsible AI” tone without claiming research

---

## 5) “Surgical keyword diff” method (no bloat)

When a JD arrives:

1. Extract high-signal tokens from JD:
   - Title synonyms
   - Required skills/tools
   - System keywords (distributed systems, inference, evaluation)
2. Compare against resume tokens
3. Add only missing tokens that are:
   - Truthful
   - High-frequency in ATS
   - Minimal (1–3 tokens or 1 sentence)
4. Never rewrite the whole resume for one job.

**Goal:** Pass filters, preserve clarity.

---

## 6) File layout

Recommended:
resume/
├── canonical_ai_systems_engineer.pdf
├── applied_ai_systems_engineer_meta.pdf
├── ai_infrastructure_engineer_openai.pdf
└── ai_platform_engineer_anthropic.pdf

docs/resume/
└── ats-linkedin-playbook.md

---

## 7) Stop condition (important)

If:
- Canonical parses well
- One variant matches the role family
- Only 1–3 truthful tokens are missing

→ Do the minimal patch and apply.

No further optimization. Move on to applications + interviews.

---
