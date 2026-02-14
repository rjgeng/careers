# ADR-002 — Resume-UIUX Repository Boundary

**Status:** Accepted  
**Date:** 2026-02-14  
**Scope:** Careers System / Resume Repository Architecture

---

## 1. Decision
A new resume repository — **Resume-UIUX** — is formally registered as the **resume content authority** for the UI/UX career lane. Its structure, ownership rules, and interaction with the **Careers** and **Jobify-AI** repositories are now defined.

This ADR establishes:
- authority boundaries
- interaction rules
- non-goals
- traceability expectations
- future extension model

This is a **governance ADR** and MUST NOT be modified in place.

---

## 2. Context
The 4G‑ENG career system uses a **multi-repository authority model**:

- **Careers/** → process authority (targeting, leveling, signals, rubrics)
- **Resume/** repos → content authority (human-authored resumes per person/lane)
- **Jobify-AI/** → advisory + logging only (analysis, suggestions, decision records)

With the introduction of a new lane (UI/UX), a dedicated resume repo (**Resume-UIUX**) is required to:
- maintain clean separation of process vs. content
- support lane-specific resume variants
- host Staff-level UI/UX rubrics derived from Careers
- avoid polluting the main Resume repo
- enable future autonomy for the UI/UX designer

---

## 3. Decision Details

### 3.1 Repository Authority
**Resume-UIUX/** becomes the single source of truth for:
- factual career history (`base.md`)
- UI/UX resume variants (ATS-safe)
- role-specific framing
- lane-specific strategy
- public-safe rubrics derived from Careers

It MUST contain **human-authored** content only.

---

### 3.2 Careers → Resume-UIUX (Process → Content)
The Careers repository remains responsible for:
- leveling rubrics
- targeting frameworks
- Staff vs Senior definitions
- role archetypes
- positioning models
- interview preparation

Resume-UIUX may **reference**, but **not redefine**, these artifacts.

All staff-level framing in Resume-UIUX must trace to:
- `careers/docs/01_POSITIONING/`
- `careers/docs/04_INTERVIEW_PREP/`
- `careers/lab/strategy/ENGINEERING_LEVELING_STRATEGY.md`

---

### 3.3 Jobify-AI → Resume-UIUX Interaction
Jobify-AI:
- MAY read the Resume-UIUX repo
- MAY generate suggestions
- MUST log decisions
- MUST NOT overwrite resume content
- MUST NOT generate canonical resume truth

This mirrors:
- ADR‑011 (*Why Careers Is the Process Authority*)
- ADR‑012 (*Why Resume Versioning Is Out of Scope*)

---

### 3.4 Expected Repo Structure
Resume-UIUX MUST use the following hierarchy:

```
Resume-UIUX/
├── README.md
├── base.md
├── Resume_UIUX.md
└── strategy/
    ├── CAREER_LANE_UIUX.md
    └── STAFF_RUBRIC_UIUX.md
```

All strategy documents must explicitly state:
"This file derives process authority from the Careers repository."

---

## 4. Non‑Goals
This ADR does **not**:
- define UI/UX leveling (lives in Careers)
- generate resume content automatically
- create personal or private data
- require Resume-UIUX to be private (it may be public-safe)

---

## 5. Consequences

### Positive
- Clean separation of concerns across repos
- UI/UX designer gains independent resume lifecycle
- Jobify-AI remains advisory-only
- Careers repo can evolve without entangling resume files
- Public-safe documentation structure

### Risks / Mitigations
- **Risk:** Resume-UIUX drifts from Careers rubrics  
  **Mitigation:** Required cross-repo references in README + strategy docs

- **Risk:** Jobify-AI suggests changes that imply canonical truth  
  **Mitigation:** ADR‑012 remains in effect; Resume-UIUX stays human-controlled

---

## 6. Future Extensions
This ADR enables future lane-specific resume repos:
- Resume-Backend
- Resume-Fullstack
- Resume-Engineering-Manager
- Resume-Product-Design

Each must:
- follow this boundary model
- introduce its own ADR
- reference Careers positioning and leveling

---

## 7. References
- ADR‑010 — Repository Boundaries and Interaction Model
- ADR‑011 — Why Careers Is the Process Authority
- ADR‑012 — Why Resume Versioning Is Out of Scope
- Careers positioning docs: `docs/01_POSITIONING/`
- Careers leveling strategy: `lab/strategy/ENGINEERING_LEVELING_STRATEGY.md`

---

**End of ADR‑020**

