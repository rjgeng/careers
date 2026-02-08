# DB Interview Cheat Card — FAANG / Staff‑Level Framing (Postgres‑First)

## Executive Framing (how Staff engineers start)

**Postgres is the default system of record (SoR).**
The primary goal is **risk reduction and long‑term operability**, not premature scale.
We scale by **exhausting simplicity** before introducing irreversible complexity.

---

## Staff‑Level Mental Model

* **System of Record (Postgres)**

  * invariants, constraints, transactions, migrations
  * correctness > performance
* **Acceleration Layer (add only when measured)**

  * Redis → latency, rate‑limiting, coordination
  * pgvector / vector DB → semantic retrieval
  * Search engine → advanced text search
* **Distribution Layer (last resort)**

  * Vitess / PlanetScale → horizontal write sharding

> Staff signal: *each layer increases blast radius and operational surface area.*

---

## System‑Design Decision Tree (FAANG‑style whiteboard)

```text
Start: correctness + operability
  |
  v
Need transactions / constraints?
  → Yes → Postgres (SoR)
        |
        |-- Read bottleneck?
        |      → replicas / Redis cache
        |
        |-- Write bottleneck?
        |      → schema/indexing → vertical scale → replicas
        |
        |-- AI / semantic access?
        |      → pgvector → external vector DB (if scale demands)
        |
        |-- Sustained write hotspots?
               → consider sharding (Vitess / PlanetScale)
```

---

## 🔔 Readiness Signals for Vitess / PlanetScale (Staff bar)

Sharding is justified **only if all are true**:

* Sustained **high write QPS** (steady‑state, not spikes)
* **Hot shard keys** are inherent to the domain (tenant/org/user)
* Top tenants dominate load and cannot be isolated with replicas
* Vertical scaling ceiling reached (CPU, IO, lock contention)
* Team owns **resharding, schema coordination, and cross‑shard limits**

> Staff heuristic: *If sharding is optional, it is premature.*

---

## 🚨 Common False Positives (explicitly call these out)

* “High traffic” (reads ≠ writes)
* Slow queries (indexing / plans first)
* Large datasets (size ≠ contention)
* Viral‑growth fear
* Multi‑tenancy without hotspots
* ORM overhead masking schema issues

Sharding solves **write‑contention physics**, not general performance anxiety.

---

## 45‑Second FAANG Interview Answer

> “We anchor on Postgres as the system of record to preserve correctness and operability. We scale vertically, then add read replicas and Redis for latency and coordination. For AI features, we start with pgvector and externalize only if retrieval scale demands it. We treat sharding via Vitess or PlanetScale as a last‑resort decision, justified only by sustained write hotspots and organizational readiness, because it permanently increases system complexity.”

---

## Staff‑Level Resume Bullets

* Led **Postgres‑first** data architecture as system of record, prioritizing correctness and operability
* Scaled production systems via **vertical growth, replicas, and Redis** before introducing sharding
* Integrated **vector search** while preserving transactional integrity
* Evaluated and deferred **Vitess/PlanetScale** adoption until write‑hotspot pressure justified complexity

---

## Whiteboard Closing Line (strong signal)

> “We treat distributed databases as an organizational decision, not just a technical one.”


## Next 


Ask ChatGPT

-   Tailor this **per FAANG company** (Google vs Meta vs Amazon vs Apple)
-   Convert it into a **spoken 60-second script** you can rehearse
-   Or map it directly to a **real system prompt** (e.g., chat app, ads system, AI product)
