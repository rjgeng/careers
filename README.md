# Careers

This repository is the **process authority** for the career system.
Jobify-AI is a downstream implementation that encodes a subset of these rules as software.
Repo boundaries are governed by Jobify-AI ADRs (ADR-010/011/012).

Career infrastructure that treats job search as a **system**, not a series of ad-hoc applications.

This repository contains **career operations infrastructure**: positioning frameworks, ATS-safe resume rules, interview preparation plans, and role selection workflows.

It is not a personal blog, a resume repository, or a collection of job applications.

---

## What This Repository Is

- A **career-ops playbook** applying engineering discipline to job search
- Structured around inputs (roles, signals), processing (filters, preparation), and outputs (applications, interviews)
- Focused on **clarity, signal quality, and realism**, not volume

The scope is intentionally aligned to **Senior Individual Contributor** roles in:
- backend systems
- full-stack engineering
- applied AI / platform engineering

---

## What This Repository Is Not

- Not a system of record for resumes or personal employment history
- Not an auto-apply or recruiter outreach tool
- Not a substitute for production engineering work

Resume content is maintained separately as a private, human-authoritative artifact.  
This repository documents **process and rules**, not private resume facts.

---

## How to Navigate

- Start with `docs/00_START_HERE.md`
- Canonical, recruiter-safe material lives in `docs/`
- `lab/` contains internal analysis and drafts (non-essential reading)
- `ops/` captures repeatable routines and execution templates

This repository is designed to be **referenced selectively**, not read end-to-end.

---

## Design Principle

Career work is treated like system work:

> define constraints → apply filters → execute deliberately → review outcomes

This repository complements, but does not replace, production systems or professional engineering repositories.

### System Invariant

This repository defines **career process and judgment**.

It does not store personal resume facts and does not automate applications.
Those boundaries are intentional and documented in
**ADR-010: Repository Boundaries and Interaction Model**.
