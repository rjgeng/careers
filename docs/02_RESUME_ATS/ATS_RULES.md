# Google ATS & LinkedIn Parsing

*A practical, engineering‑style guide using **Rongjun Geng’s resume** as a concrete example.*

---

## 1. Is This “New Stuff”?

**Short answer:** *No — the mechanisms are not new. The importance is new.*

### Timeline (simplified)

* **1999–2005** — Early ATS systems (keyword scanning, basic parsing)
* **2005–2015** — Enterprise ATS adoption (Workday, Taleo, iCIMS)
* **2015–2020** — LinkedIn parsing + recruiter search dominates hiring
* **2020–Now** — AI/ML‑assisted ranking, but still **parser‑first**

👉 The core parser logic is **old and conservative**. What changed is:

* Volume of applicants
* AI‑assisted filtering
* Fewer human eyes per resume

**Result:** Parsing quality now determines visibility.

---

## 2. What “Parsing” Means (Engineering View)

Parsing = converting a human document into a structured record.

```
PDF / DOCX
   ↓
Text extraction
   ↓
Section detection
   ↓
Entity mapping
   ↓
Candidate profile
```

Typical extracted fields:

```
Name
Title
Skills[]
Company
Role
StartDate / EndDate
Education
```

If extraction fails → fields are empty or incorrect → ranking drops.

---

## 3. Google ATS vs LinkedIn Parsing

### Google ATS (company portals)

* Used when uploading resumes to company career sites
* Often older or heavily customized
* Strict assumptions about:

  * Section headers
  * Linear layout
  * Date formats

**Failure mode:** Resume looks great to humans, but parses poorly.

### LinkedIn Parsing

* Used by:

  * Easy Apply
  * Profile auto‑fill
  * Recruiter search indexing

**Failure mode:** Skills or titles not indexed → recruiter never sees you.

---

## 4. Why Senior Engineers Are Hit Harder

Junior resumes:

* Few roles
* Few skills
* Simple layout

Senior resumes:

* Many skills
* Long timelines
* Architecture language
* Multiple domains (AI + UI + systems + hardware)

➡️ **Parsing errors compound with seniority.**

This is why experienced engineers feel “invisible”.

---

## 5. Resume Demo — What ATS Sees in *Your* Resume

From your updated resume, a **good parser extracts**:

```
Name: Rongjun Geng
Title: AI Systems Engineer
Location: Vallejo, CA
Skills:
  Python, C/C++, Rust, React, Next.js,
  FastAPI, RAG, LLM, AWS, Linux,
  FPGA, SDR
Company:
  4G ENG
Role:
  Software Engineer / AI Systems Engineer
Dates:
  2015 – Present
```

This works **because**:

* Title is explicit
* Skills are written as text (not icons)
* Sections are standard

---

## 6. What Breaks Parsing (and Why)

### ❌ Common mistakes

| Mistake           | Why it breaks                    |
| ----------------- | -------------------------------- |
| Two‑column layout | Text order becomes scrambled     |
| Tables for skills | Skills not detected individually |
| Icons / emojis    | Text extractor ignores them      |
| Creative headers  | Section not recognized           |
| Graphics / charts | Ignored completely               |

Example:

```
🧠 About Me
```

Parser sees: *unknown section*

---

## 7. Why Your Updated Resume Parses Well

### Key design choices

* One‑column layout
* Standard headers:

  * SUMMARY
  * TECHNICAL SKILLS
  * PROFESSIONAL EXPERIENCE
  * EDUCATION
* Explicit keywords:

  * “AI Systems Engineer”
  * “LLM”
  * “RAG”
  * “FastAPI”
  * “React / Next.js”

These map directly to recruiter searches.

---

## 8. Keyword Reality (No Hype)

ATS does **not** understand meaning. It matches **tokens**.

Recruiter search example:

```
("AI Systems Engineer" OR "AI Platform")
AND RAG
AND FastAPI
AND React
```

If a word is missing → you fail the filter.

Your resume now **passes this filter cleanly**.

---

## 9. Google Docs Best Practices (Important)

When using Google Docs:

✅ Use default fonts (Arial, Calibri)
✅ Use real bullet points
✅ Avoid tables for layout
✅ Export to PDF *after* finalizing

❌ Avoid columns
❌ Avoid text boxes
❌ Avoid icons for headings

---

## 10. How to Self‑Test Parsing (Do This Once)

1. Upload resume to LinkedIn
2. Let LinkedIn auto‑fill your profile
3. Inspect:

   * Job titles
   * Skills
   * Dates

If LinkedIn parses it correctly → ATS likely will too.

---

## 11. Key Mental Model (Pin This)

> **Your resume has two readers: a machine and a human. The machine decides whether the human ever sees it.**

Design for the machine first.

---

## 12. Final Takeaway

* ATS parsing is **not new**
* AI hiring made it **more decisive**
* Senior engineers must design resumes like **APIs**
* Your updated resume is **parser‑safe and senior‑credible**

---

*End of guide.*
