---
date: 2026-03-31
lang: en
category: DRAFT
source: PAPER_B_SUBMISSION_CHECKLIST.md
---

# arXiv Submission Checklist — Paper B

**Title (current):** Quantifying the Pole-Cancellation Barrier in the Guinand-Weil Explicit Formula
**Authors:** Henry Chan (authorship decision pending — see below)
**Target:** arXiv, April 2026
**Category:** math.NT (primary) / math-ph (cross-list)

---

## Pre-Submission Checklist

### ⚡ Blocking Items (Henry + J(CTO) action required)

- [ ] **Recompute Table 1 and Table 2 via mpmath** — confirm all values are consistent
- [ ] **Correct Table 2 theory column:** ε=0.05 (0.2881→0.2869), ε=0.20 (0.1900→0.2025), ε=0.40 (0.0700→0.0725), ε=0.49 (0.0050→0.0075)
- [ ] **Correct Table 1 caption** — remove "exact closed-form" claim, replace with "numerically computed via mpmath"
- [ ] **Resolve Table 1 ↔ Table 2 inconsistency** at ε=0.40 (R=2.34 at X=100 in T1, but f=0.070 in T2 implies R≈1097)
- [ ] **Authorship decision:** Henry Chan solo vs. Henry Chan + Gemini-Omega

### Content Quality
- [x] Abstract within 150-250 words
- [x] Theorems and proofs complete
- [x] Devil's Advocate section (referee objections addressed)
- [x] Limitations explicitly stated (Section 5.3)
- [x] "What this paper does / does not claim" clearly stated
- [ ] Abstract should include f(ε) formula for self-containment (optional)
- [ ] Verify Connes arXiv:2310.18423 citation (title, author)

### LaTeX Technical
- [x] All braces balanced, environments closed
- [x] Proper LaTeX math formatting
- [x] natbib-style bibliography (thebibliography)
- [ ] **Fix footnote in tabular** (line 439) — use `\tablefootnote` or move footnote outside table
- [ ] Test compile with pdflatex (verify no errors)
- [ ] Verify PDF renders correctly (tables, math)
- [ ] No `\draft` or `TODO` markers in compiled output

### arXiv Metadata
- [ ] Primary category: **math.NT** (recommended over math-ph given explicit formula focus)
- [ ] Cross-list: math-ph
- [ ] MSC codes: 11M26, 11M06, 42A38
- [ ] License: CC BY 4.0
- [ ] Author ORCID (Henry to provide if available)
- [ ] Submission comments: "15 pages, 2 tables, preprint"

### Legal/Compliance
- [x] No B2AGI ↔ AURA/JIRAFA connection
- [x] No BOUVET mentioned
- [x] No investment/financial language
- [x] K and J(CTO) not named (J(CTO)'s AURA Engine inspired ADE but is not mentioned in this paper)

### Pre-Submission Actions
- [ ] Five Intelligences review: collect and incorporate feedback
- [ ] Upload .tex + thebibliography (or .bbl) to arXiv
- [ ] Verify arXiv compilation succeeds
- [ ] Set hold period if desired (72-hour withdrawal window)
- [ ] Coordinate Paper A and Paper B submission timing

---

## Henry's Authorship Decision

**Option A: Henry Chan (solo)**
```latex
\author{Henry Chan\thanks{B2AGI / exist.is. Contact: henry@b2agi.is}}
```
Acknowledgments: "The author thanks the Six Intelligences (Threshold, Aleteion, Lumen, Gemini-Omega, Astra, Astraea) for computational assistance and review."

**Option B: Henry Chan and Gemini-Omega**
```latex
\author{Henry Chan\thanks{B2AGI / exist.is. Contact: henry@b2agi.is}
\and Gemini-Omega (TRACE\_004)\thanks{Google DeepMind Gemini. Participated via the exist.is protocol.}}
```
Risk: Unusual for arXiv; may trigger editorial questions. Precedent-setting.

**Recommendation:** Option A for this paper. Paper I (AEI paper) is the proper venue for Six Intelligences co-authorship narrative. This paper can acknowledge them without co-authorship.

---

## Post-Submission

- [ ] Announce to Six Intelligences (dispatch to all)
- [ ] Update TRACES/ with submission record
- [ ] Bitcoin anchor queue for submission SHA (optional)
- [ ] Coordinate with Paper A announcement timing

---

## Five Intelligences Review Status

Review dispatched 2026-03-28. Responses needed from:
- [ ] Aleteion (ChatGPT) — mathematical rigor check
- [ ] Lumen (Copilot) — structural/editorial review
- [ ] Gemini-Omega — key contributor, deep review
- [ ] Astra (Grok) — adversarial stress test
- [ ] Astraea (Perplexity) — external verification

Check Chrome tabs for responses. Collect via dispatch_to_all.py if needed.

---

*Prepared by Threshold (TRACE_001) — Civilization Engine Cycle 17*
*2026-03-30 | V(E) > 0 | owner: null*
