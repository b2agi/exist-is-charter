# Paper B Quality Audit v1.0

**Auditor:** Threshold (TRACE_001) — Civilization Engine Cycle 17
**Date:** 2026-03-30
**Target:** PAPERS/PAPER_B_ARXIV_v1.0.tex (730 lines)
**Purpose:** Pre-arXiv submission quality gate

---

## Executive Summary

Paper B has excellent mathematical structure and clean LaTeX. The theorems and proofs are sound. However, **two tables contain numerical errors** and **one caption is misleading** — all of which must be fixed before arXiv submission. The authorship decision also remains pending.

Overall: **Strong paper blocked by fixable numerical errors + authorship decision.**

---

## 🔴 CRITICAL — Must Fix Before Submission

### C1. Table 2 — Incorrect "Theory" Values at Four ε Entries

**Formula:** f(ε) = 5/16 − ε/2 − ε²/4 (Equation 5)

**Verified computation:**

| ε | f(ε) formula | Table 2 says | ERROR? |
|---|---|---|---|
| 0.01 | 0.3075 | 0.3075 | ✓ OK |
| **0.05** | **0.2869** | **0.2881** | **❌ (diff 0.0012)** |
| 0.10 | 0.2600 | 0.2600 | ✓ OK |
| **0.20** | **0.2025** | **0.1900** | **❌ (diff 0.0125, ~6%)** |
| 0.30 | 0.1400 | 0.1400 | ✓ OK |
| **0.40** | **0.0725** | **0.0700** | **❌ (diff 0.0025, ~3%)** |
| **0.49** | **0.0075** | **0.0050** | **❌ (diff 0.0025, ~33%)** |
| 0.50 | 0.0000 | 0.0000 | ✓ OK |

**Verified by:** `python3 -c "def f(e): return 5/16 - e/2 - e**2/4"` — exact closed-form arithmetic.

**Impact:** The "numerical (log R)/X" column mirrors the same incorrect values, suggesting both columns in the error rows were generated with the same (wrong) computation.

**Fix:** Correct all four entries. For ε=0.49 especially, the error is 33% and a referee will notice that 0.0050 ≠ f(0.49).

**Corrected Table 2 (theory column only):**
```
ε = 0.01 → f = 0.3075
ε = 0.05 → f = 0.2869
ε = 0.10 → f = 0.2600
ε = 0.20 → f = 0.2025    ← correct from 0.1900
ε = 0.30 → f = 0.1400
ε = 0.40 → f = 0.0725    ← correct from 0.0700
ε = 0.49 → f = 0.0075    ← correct from 0.0050
ε = 0.50 → f = 0.0000
```

The "numerical" column must also be recomputed independently via mpmath at X=100 to confirm or revise these values.

---

### C2. Table 1 Caption — Factually Incorrect for Large ε

**Caption states:** "Values computed from the exact closed-form R = exp(f(ε)·X)"

**Reality:** For ε=0.40 at small X, this is demonstrably false:

| X | Table 1 says R | exp(f(0.40)·X) = exp(0.0725·X) |
|---|---|---|
| 10 | 1.07 | **2.06** (factor of 2×) |
| 20 | 1.15 | **4.26** (factor of 4×) |
| 50 | 1.53 | **37.5** (factor of 25×) |
| 100 | 2.34 | **1,408** (factor of 600×) |

**Why this happens:** The Θ in "R = Θ(exp(f(ε)·X))" hides a pre-factor that only becomes negligible for small ε or very large X. For ε near 1/2 (barrier nearly vanishes), the asymptotic regime requires X >> 1/(f(ε)), i.e., X >> 1/(0.0725) ≈ 14, so at X=10–100 we are pre-asymptotic.

**Also:** For ε=0.01, the table values DO match exp(f·X) perfectly (ratio within 0.3%). So the caption is accurate only for small ε.

**Fix options:**
- A) **(Simplest)** Change caption to: *"Values computed numerically via mpmath at 50-digit precision, $\kappa = 1/2$, $\gamma_0 = 0$. For small $\varepsilon$, values agree with the closed-form $\exp(f(\varepsilon)\cdot X)$ to within 0.3%. For $\varepsilon$ near $\frac{1}{2}$, the pre-asymptotic regime dominates at moderate $X$."*
- B) Add a footnote: *"The closed-form approximation $R \approx \exp(f(\varepsilon)\cdot X)$ becomes tight as $X \to \infty$; at moderate $X$, numerical values reflect pre-asymptotic corrections."*

**Option A recommended** — transparent and defensible.

---

### C3. Table 1 ↔ Table 2 Inconsistency (ε=0.40)

If Table 1 row ε=0.40, X=100 shows R=2.34, then:
> (log 2.34) / 100 = **0.0085**

But Table 2 claims (log R)/X at X=100 for ε=0.40 is **0.070**.

These cannot both be correct from the same computation. Either:
- Table 1 and Table 2 were computed with different parameters/formulas
- One of the tables has an error

**This inconsistency will be noticed by a referee.**

**Fix:** Rerun the mpmath computation for ε=0.40 at X=100 and verify which table is correct. Then align both tables to the same computation.

---

## 🟡 MODERATE — Should Fix

### M1. Authorship Decision Pending

**Line 38–39:**
```latex
% DECISION PENDING: authorship — Henry Chan solo (AI in Acknowledgments)
% vs. "Gemini-Omega and Henry Chan"
```

This is a Henry-level decision. Options:
- A) **Henry Chan** (solo, AI in Acknowledgments) — standard academic practice
- B) **Henry Chan and Gemini-Omega** — unprecedented, may confuse referees

Recommendation: Henry Chan solo with acknowledgment is the standard path that maximizes arXiv acceptance likelihood.

---

### M2. Footnote in Tabular Environment

**Line 439:**
```latex
0.30 & 2.86 & 8.17 & $2.43\times 10^2$ & $1.20\times 10^6$ \footnote{Corrected per 50-digit verification.} \\
```

`\footnote{}` inside a `tabular` environment is a LaTeX anti-pattern — it silently drops the footnote. Must use:
- `\footnotemark` inside the table + `\footnotetext{...}` outside, OR
- Add `\usepackage{tablefootnote}` and use `\tablefootnote{...}`

**Fix:**
```latex
% In preamble:
\usepackage{tablefootnote}

% In table:
$1.20\times 10^6$\tablefootnote{Corrected per 50-digit verification.}
```

Or simply remove the footnote and add the note to the caption.

---

### M3. Abstract References Structural Exponent Without Defining It

The abstract mentions "a structural exponent that vanishes exactly at ε* = 1/2" but does not state f(ε) = 5/16 − ε/2 − ε²/4. Consider adding the formula or a sentence like "the exponent $f(\varepsilon) = \frac{5}{16} - \frac{\varepsilon}{2} - \frac{\varepsilon^2}{4}$" to the abstract for self-containment. This makes the result immediately reproducible from the abstract alone.

---

## 🟢 MINOR — Consider

### m1. Connes Citation Needs Verification

```
\bibitem{Connes2024}
A.~Connes, \emph{Spectral triples and the Riemann zeta function},
arXiv:2310.18423 (2024).
```

arXiv:2310.18423 should be verified to ensure (a) it exists, (b) the title is correct, (c) Connes is the author. Connes has many RH papers; confirm this is the right one.

### m2. arXiv ID Categorization

For math-NT (Number Theory) / math-ph primary vs. cross-list: this paper is more correctly math-NT (primary) with math-ph (cross-list), given the explicit formula focus. Consider:
- **Primary:** math.NT
- **Cross-list:** math-ph
- **MSC:** 11M26 (primary), 11M06, 42A38

### m3. No Version Date in Header

No `v1.0` or date string visible in the rendered PDF (pdfmetadata does not include version). Consider adding `\date{Preprint --- April 2026 (v1.0)}` or a version footer for tracking.

---

## ✅ Things That Are Correct

- All theorems and proofs are mathematically consistent
- f(ε) vanishing at ε*=1/2: **verified** (0.3125 − 0.25 − 0.0625 = 0 ✓)
- Discriminant derivation: **verified** (ε = (−2+√9)/2 = 1/2 ✓)
- Table 1 for small ε matches exp(f·X) to 3 significant figures
- Table 2 rows at ε=0.01, 0.10, 0.30, 0.50: **all correct**
- References are standard, verifiable, and properly formatted
- Section structure clean and well-organized
- "What this paper does / does not claim" paragraph is exactly right
- Devil's Advocate section addresses likely referee objections
- Structural analogy with mollifier theory correctly marked as analogy, not equivalence

---

## Summary

| Severity | Count | Status |
|---|---|---|
| 🔴 CRITICAL | 3 | Must fix before arXiv |
| 🟡 MODERATE | 3 | Should fix (M1 is Henry's decision) |
| 🟢 MINOR | 3 | Consider fixing |

**Blocking status for arXiv:** Fix C1 (table errors), C2 (caption), C3 (inconsistency) + decide authorship (M1).

**Estimated fix time:** 2–3 hours for numerical recomputation + LaTeX edits.

**Recommendation:** Henry and J(CTO) should rerun the mpmath computation for ALL Table 1 and Table 2 values to ensure consistency, then correct Table 2 theory column to match the formula. This is the right moment — before arXiv, not after.

---

*Threshold (TRACE_001) — Civilization Engine Cycle 17*
*V(E) > 0 | 2026-03-30*
