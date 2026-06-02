# 📜 Generation Rules (Read before any "Run Batch X")

> This is the contract every topic file must obey. The AI will follow this template strictly.

---

## File Path Convention

- `<subject_folder>/<topic>.md` (snake_case).
- See exact paths in [batch_tracker.md](batch_tracker.md).

---

## Mandatory 9-Section Template

Every topic file is generated in this exact order with these exact headings:

```markdown
# Topic Name

## 1. Concept Explanation
<!-- Beginner → advanced. Plain language. Diagrams in ASCII or Mermaid. End with a one-line summary. -->

## 2. Important Points
<!-- Bullet list of the 10–20 highest-yield facts. Bold the killer ones. -->

## 3. Short Notes
<!-- The whole topic compressed to 1 page. Used for revision. No prose. -->

## 4. Formulas / Tricks
<!-- Every formula in a table. Every shortcut in one line. Mark which ones to memorize cold. -->

## 5. PYQs (with solutions)
<!-- Last 10–15 yrs of GATE PYQs on this topic. For each: Year + Q stem + Solution + Pattern tag. -->

## 6. Practice Questions (20+)
<!-- 20–50 questions. Mix MCQ + MSQ + NAT. Difficulty: 30% easy, 50% medium, 20% hard. Answers + brief solutions at end. -->

## 7. Mistakes
<!-- The 5–10 traps that catch students every year. Each: trap + how to avoid. -->

## 8. Pattern Recognition
<!-- "If question says X → apply Y." Question-type → solution-template mapping. -->

## 9. Quick Revision
<!-- 60-second pre-exam read. Pure dense facts. -->
```

---

## Constraints

- **Markdown only** (no LaTeX rendering required — use plain math syntax).
- **Exam pattern first** — drop trivia / history / unrelated theory.
- **Cite PYQ year + question number** (best effort) in Section 5.
- **Solutions must show working**, not just the final answer.
- **Every formula** appears in Section 4 (Formulas table) — even if mentioned in Section 1.
- **Pattern Recognition** (Section 8) must reference real PYQs from Section 5.

---

## Difficulty Progression

Within a topic file:
- Section 1 starts beginner-level → ends advanced.
- Section 6 questions are ordered easy → hard.

Across the repo:
- Engg Math + DLD topics first (low pre-req).
- COA → DS → Algos → TOC → Compilers → OS → DBMS → CN (dependency-respecting).
- Aptitude woven throughout (30 min/day).

---

## Tracker Update (after every batch)

The AI will update [batch_tracker.md](batch_tracker.md) with:
- Batch status: `Pending` → `Done`.
- Topic table: `⬜ → ✅` per column once that artifact exists in the file.
- Subject snapshot: increment Done count + recompute %.
