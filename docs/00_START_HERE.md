# Start Here

This repository defines my **career system**—a structured, repeatable, and measurable approach to targeting roles, preparing for interviews, and managing long-term professional positioning.
It replaces ad-hoc job searching with **deliberate engineering practice**: clarity of constraints, explicit decision rules, and traceable improvement loops.

Everything here is **process**, not personal history.
Personal employment facts live in the **Resume** repository.
AI-assisted analysis and suggestions live in **Jobify-AI**, constrained by governance ADRs.

This repository is intentionally minimal, authoritative, and optimized for signal.

---

## Purpose

The goal of this system is to:

* create a **stable targeting strategy** grounded in market reality
* maintain **ATS-safe and lane-specific resume variants**
* provide **checklists and rubrics** for Senior/Staff-level preparation
* reduce randomness through deliberate iteration
* support multiple individuals (engineer, UI/UX) with the same operating model

It is not a blog or a scrapbook.
It is a **decision system**.

---

## Boundary Model (Canonical)

This repository is one of three authoritative components:

### **1. Resume Repository — Human Truth Authority**

* Owns all personal, factual history
* Contains resume variants per role lane
* The only place where resume content is modified

### **2. Careers Repository — Process Authority (this repo)**

* Defines signals, leveling, lane selection
* Owns ATS rules, positioning, prep checklists
* Provides reusable frameworks for multiple individuals

### **3. Jobify-AI — Advisory + Logging Only**

* Provides analysis, suggestions, and summaries
* Cannot modify resume truth
* Must reference careers positioning and rubrics
* Governed by ADR-010, ADR-011, ADR-012

These boundaries are mandatory for system integrity.

---

## Cross-Repo Navigation Index

Use this map whenever adding or updating career system artifacts.

### **Resume/**

*What is true*

* `base.md` — canonical fact store
* Role-lane resume variants
* LinkedIn update checklist

### **Careers/**

*How decisions are made*

* Positioning (lanes, differentiation, signals)
* Resume & ATS (rules, playbooks)
* Interview prep (checklists, rubrics)
* Role filtering logic (job search engine)

### **Jobify-AI/**

*Advisory only*

* AI analysis of roles
* Resume suggestions
* Logged recommendations
* Governance constraints

---

## How to Use This Repository (Engineer + UI/UX)

1. **Choose a lane** using Positioning frameworks
2. **Update factual history** in Resume/base.md
3. **Use ATS rules** to generate role-specific variants
4. **Prepare using checklists** in Interview Prep
5. **Run role filtering** with the Job Search Engine
6. For UI/UX career track, use:

   * `docs/03_LINKEDIN/templates/DESIGNER_UIUX.md`
   * shared leveling rules (Senior/Staff signals)

This system supports multiple people following the same professional scaffolding.

---

## Staff-Level Interpretation

Senior → executes independently
Staff → **shapes systems** (process, decision-rules, constraints)

This repository encodes Staff-level behavior by:

* drawing clear ownership boundaries
* separating truth from process from tooling
* enforcing reproducibility
* maintaining canonical ADRs for governance
* using checklists instead of intuition
* capturing reasoning, not just results

This is what Staff looks like at the process layer.

---

## What This Repository Is Not

* ❌ not a resume storage location
* ❌ not a personal journal
* ❌ not a portfolio website
* ❌ not an AI-generated artifact dump
* ❌ not a mixed collection of ideas

It is a **precision tool** for making high-quality career decisions.

---

## You Are Here

If you are new to this repository, start with:

1. **`docs/01_POSITIONING/DIFFERENTIATION.md`**
2. **`docs/02_RESUME_ATS/ATS_PLAYBOOK.md`**
3. **`docs/04_INTERVIEW_PREP/GENERAL_PREP.md`**
4. **`docs/05_JOB_SEARCH_ENGINE/ROLE_FILTER_CHECKLIST.md`**

Then move upward through checklists until you reach Staff-level exp
