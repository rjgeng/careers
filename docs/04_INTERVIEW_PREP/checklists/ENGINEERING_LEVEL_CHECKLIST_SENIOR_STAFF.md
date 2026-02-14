---
title: Senior vs Staff Engineer Requirements Checklist
version: 0.1
status: draft
last_updated: 2026-02-13
---

# Senior vs Staff Engineer Requirements Checklist

Use this checklist to self-assess, prep for interviews, or write a role scorecard. It fits backend, full-stack, infra, and AI/ML systems with minor edits.

---

## Scope and Impact

- [ ] Owns a problem area end-to-end (not just tickets).
- [ ] Delivers multi-quarter roadmap-impact work (not one-off features).
- [ ] Improves outcomes at team level (Senior) or org level (Staff).
- [ ] Defines success metrics (latency, cost, reliability, conversion, quality) and tracks them.

---

## Technical Depth

- [ ] Designs systems with explicit tradeoffs (consistency, latency, cost, complexity).
- [ ] Debugs across stack: logs/metrics/traces, reproduction, root-cause analysis.
- [ ] Manages data correctness: schemas, migrations, backfills, idempotency, replay.
- [ ] Performance competence: profiling, hotspots, caching, concurrency.
- [ ] Applies security basics by default: authN/authZ, secrets handling, threat thinking.

---

## System Design and Architecture

- [ ] Writes concise design docs with alternatives and decisions.
- [ ] Defines interfaces/contracts (APIs, events, schemas) with versioning strategy.
- [ ] Establishes guardrails: timeouts, retries, circuit breakers, rate limits.
- [ ] Plans for failure modes and incident response from day 1.
- [ ] Ensures operability: dashboards, SLOs/SLIs, alerts, runbooks.

---

## Execution and Delivery

- [ ] Breaks ambiguous problems into milestones with clear risks/dependencies.
- [ ] Drives alignment across stakeholders; resolves blockers without escalation loops.
- [ ] Ships iteratively; avoids big-bang releases unless justified.
- [ ] Maintains quality under time pressure (tests, review, rollout discipline).
- [ ] Uses postmortems and follow-ups to prevent repeat issues.

---

## Code Quality and Engineering Excellence

- [ ] Writes maintainable code with clear ownership boundaries.
- [ ] Reviews others’ code for correctness, safety, simplicity, and long-term cost.
- [ ] Raises engineering standards (linting, CI, test strategy, release discipline).
- [ ] Retires tech debt that blocks roadmap (not cosmetic refactors).

---

## Cross-Team Influence (Senior → Staff transition point)

- [ ] Senior: influences within team; Staff: influences across teams/org.
- [ ] Creates reusable patterns/platforms others adopt.
- [ ] Leads multi-team initiatives with shared design and phased rollout.
- [ ] Aligns teams on conventions (observability, APIs, reliability practices).

---

## Leadership Without Authority

- [ ] Mentors engineers; improves others’ output and judgment.
- [ ] Communicates clearly in docs and meetings; reduces confusion and rework.
- [ ] Handles disagreement with evidence and tradeoffs; lands decisions.
- [ ] Recognizes people/process constraints; adapts plans accordingly.

---

## Product and Business Thinking

- [ ] Understands user/business goals and translates them into technical priorities.
- [ ] Uses data to validate impact (experiments, metrics, cost curves).
- [ ] Makes cost/speed/reliability tradeoffs explicitly and responsibly.
- [ ] Knows when “good enough” is correct, and when it’s risky.

---

## Reliability and Operations

- [ ] Has owned incidents: detection → mitigation → postmortem → prevention.
- [ ] Builds for safe deploys: canary, feature flags, rollbacks, safe migrations.
- [ ] Defines SLOs and manages error budgets (or equivalent discipline).
- [ ] Reduces pager noise; improves runbooks; runs drills where appropriate.

---

## Typical “Bar” Summary

### Senior Engineer (expected)

- [ ] Independently delivers large features/systems within a team.
- [ ] Strong design + execution + quality.
- [ ] Mentors, raises the bar locally, handles ambiguity.

### Staff Engineer (expected)

- [ ] Defines technical direction for an area across teams.
- [ ] Leads multi-quarter, multi-team initiatives.
- [ ] Creates leverage (platforms, standards, reusable architectures).
- [ ] Strong stakeholder alignment and org-level risk management.

---

## Evidence Checklist (what to show on resume/interviews)

- [ ] 2–4 projects with: problem, constraints, approach, tradeoffs, impact metrics.
- [ ] One example of a hard incident and what changed afterward.
- [ ] One example of cross-team influence (migration, platform, standard, RFC).
- [ ] One example of mentorship/raising quality (process or tooling improvement).

---

## Optional: Rating Scale (quick self-score)

Use a simple 0–2 scale per section:

- 0 = limited evidence
- 1 = some evidence / inconsistent
- 2 = strong evidence / repeated outcomes

Target guidance:
- Senior: mostly 1–2s, with at least a few clear 2s
- Staff: mostly 2s in cross-team influence + leadership + architecture

