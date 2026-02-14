# Start Here

This repository documents my **career as a system**, not a collection of ad-hoc applications.

It contains ATS-safe resume artifacts, interview preparation materials, role-filtering logic,
and portfolio narratives aligned with real hiring signals.

The goal is to reduce randomness in job search by applying engineering principles:
constraints, feedback loops, and measurable outcomes.

All content is derived from non-proprietary work and personal experience.
Production work lives elsewhere; this repo is strictly **career infrastructure**.

Most readers should start with **Positioning**, **Resume & ATS**, and **Interview Prep**.
The **Job Search Engine** section describes how roles are evaluated and prioritized.

Portfolio summaries map real projects to resume bullets and system-design discussions.
Appendix materials provide context, not requirements.

This repository is intentionally opinionated and pragmatic.
It favors signal clarity over breadth.

Treat it as a reference, not a blog.

---

## Repository Boundary Context

This repository is one component of a deliberately separated career system:

- **Resume** — private, human-authoritative factual history
- **Careers** — process, filters, and decision frameworks (this repository)
- **Jobify-AI** — AI-assisted decision-support tooling

The ownership boundaries and interaction rules between these repositories
are defined in:

> **ADR-010: Repository Boundaries and Interaction Model**

This repository defines **how career decisions are made**.
It does not own personal employment facts and does not automate execution.

## External Authorities (Cross-Repo Contract)

- **careers/** is the **process authority** (targeting, leveling, checklists, interview prep, templates).
- **Resume/** is the **resume content authority** (human-authored resume variants for each person and lane).
- **jobify-ai/** is **advisory + logging only** (analysis, suggestions, decision records), per its governance ADRs.
- This contract applies to all individuals (e.g., engineer, designer/UIUX) and all lanes managed under careers/.
- Jobify-AI MUST NOT redefine career process or overwrite resume truth; it may **only** reference careers rubrics/templates and produce suggestions.

Key references:
- `careers/docs/00_START_HERE.md`
- `careers/docs/` (process artifacts) and `Resume/` (resume outputs)

