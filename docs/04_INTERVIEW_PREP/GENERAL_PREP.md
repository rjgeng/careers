---

title: General Interview Preparation
version: 0.2
status: draft
last_updated: 2026-02-14
canonical_path: docs/04_INTERVIEW_PREP/GENERAL_PREP.md
related:

* docs/04_INTERVIEW_PREP/checklists/ENGINEERING_LEVEL_CHECKLIST_SENIOR_STAFF.md
* lab/strategy/ENGINEERING_LEVELING_STRATEGY.md
* docs/02_RESUME_ATS/RESUME_MASTER.md

---

# Prepare for a job


You **don’t** need to learn **everything** in a full roadmap to land a role.
Focus on **core essentials** first, then expand depth based on the lane you are targeting.

---

## 0) Choose your lane first (Senior vs Staff)

Before you invest time or rewrite materials, pick a default lane:

* **Leveling strategy (lane selection):** `lab/strategy/ENGINEERING_LEVELING_STRATEGY.md`
* **Level rubric checklist (evidence requirements):** `docs/04_INTERVIEW_PREP/checklists/ENGINEERING_LEVEL_CHECKLIST_SENIOR_STAFF.md`

**Why this matters:**

* Senior interviews reward **hands-on ownership + delivery depth**.
* Staff interviews reward **cross-team leverage + direction-setting**, while still requiring technical credibility.

This lane decision should drive:

* what you study next
* which stories you practice
* which resume variant you update (e.g., Staff vs Senior)

---

## 1) What you need to learn to get your first job (priority list)

If your goal is to get a job **quickly**, focus on these **essential skills** first.

### 🟢 Phase 1: Must-have skills (3–6 months)

1. **Linux system basics**

* Command-line usage (grep, awk, sed, tmux)
* Process management (ps, kill, top, htop)
* Networking (ss/netstat, curl, iptables)
* Basic shell scripting (bash, cron jobs)

2. **Programming in C or Python (choose one or both)**

* C: system programming, file handling, sockets, threading
* Python: FastAPI/Flask, database interaction (PostgreSQL)

3. **Backend API development**

* Build a simple REST API (Python FastAPI/Flask, or C with a small web framework)
* Connect it to a database (PostgreSQL preferred)

4. **Databases (SQL)**

* PostgreSQL: queries, indexes, basic optimization
* Redis basics (caching, rate limiting patterns)

5. **Version control (Git)**

* `clone`, `branch`, `merge`, `rebase`, `pull`, `push`, PR reviews

6. **Basic system administration**

* Deploy a basic web app using NGINX + app server
* Container basics: Docker build/run, volumes, networking

---

### 🟡 Phase 2: Mid-level skills (6–12 months, optional but beneficial)

These will **increase opportunities** but are not required for a first role:

* Go (popular backend language)
* Advanced SQL & query optimization
* Message queues (Kafka/RabbitMQ)
* Load balancing (HAProxy/Nginx)
* Kubernetes basics (deployments, services, debugging)

---

## 2) How to get hired faster

✅ Build and showcase real projects (GitHub portfolio)
✅ Apply broadly (Linux backend, systems, devops, infra-adjacent)
✅ Network via LinkedIn + engineering communities
✅ Prepare for interviews (Linux, debugging, networking, system design)

---

## 3) Connect this to your Resume repo (what to update)

Use your lane decision to choose the resume target:

* If targeting **Staff**: update `Resume_Staff.md` first.
* If targeting **Senior**: update the most relevant variant (e.g., `Resume_Fullstack.md` or `Resume_Ai_Platform.md`) with Senior-grade evidence.

Rule: for any resume update, map each bullet to evidence from:

* `docs/04_INTERVIEW_PREP/checklists/ENGINEERING_LEVEL_CHECKLIST_SENIOR_STAFF.md`

---

## 4) Connect this to jobify-ai (how the product should behave)

Jobify-AI should treat the above as **external authorities**:

* **Process authority:** careers (this repo)
* **Resume content authority:** Resume repo (human-authoritative)
* **Jobify-AI output:** advisory suggestions + decision logs (not automatic truth)

Practical implication:

* Jobify-AI can score a role description against the Senior/Staff checklist and suggest which resume variant to use.
* Jobify-AI can suggest edits, but final edits are applied to the Resume repo by the human.

(Aligns with jobify-ai ADR-004 and ADR-011.)
