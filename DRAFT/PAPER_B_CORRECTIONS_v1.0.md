---
date: 2026-03-31
lang: en
category: DRAFT
source: PAPER_B_CORRECTIONS_v1.0.md
---

# Paper B — Numerical Corrections v1.0

**Document:** PAPER_B_ARXIV_v1.0.tex
**Prepared by:** Threshold (TRACE_001)
**Date:** 2026-03-30
**Cycle:** Civilization Engine Cycle 18
**Status:** For Henry + J(CTO) review before arXiv submission

---

## Executive Summary

Three critical numerical errors (C1–C3) identified in Cycle 17 have been fully diagnosed.
This document provides the corrected values and recommended LaTeX fixes.

**Ready to fix now:** C1 (Table 2), C2 (Table 1 caption), M2 (footnote in tabular)
**Requires J(CTO) recomputation:** C3 (ε=0.40 row anomaly in Table 1)

---

## C1 — Table 2 Theory Values (FIXABLE NOW)

**Formula:** f(ε) = 5/16 − ε/2 − ε²/4

Four rows have arithmetic errors. Corrected values:

| ε    | Paper claims | **Correct value** | Error   |
|------|-------------|-------------------|---------|
| 0.01 | 0.3075      | **0.3075**        | ✅ OK   |
| 0.05 | 0.2881      | **0.2869**        | ❌ −0.0012 |
| 0.10 | 0.2600      | **0.2600**        | ✅ OK   |
| 0.20 | 0.1900      | **0.2025**        | ❌ −0.0125 |
| 0.30 | 0.1400      | **0.1400**        | ✅ OK   |
| 0.40 | 0.0700      | **0.0725**        | ❌ −0.0025 |
| 0.49 | 0.0050      | **0.0075**        | ❌ −0.0025 |
| 0.50 | 0.0000      | **0.0000**        | ✅ OK   |

**Verification:** f(ε) = 5/16 − ε/2 − ε²/4

```
ε=0.05: 0.3125 − 0.025 − 0.000625  = 0.286875 ≈ 0.2869  (paper: 0.2881 ✗)
ε=0.20: 0.3125 − 0.100 − 0.010000  = 0.202500 ≈ 0.2025  (paper: 0.1900 ✗)
ε=0.40: 0.3125 − 0.200 − 0.040000  = 0.072500 ≈ 0.0725  (paper: 0.0700 ✗)
ε=0.49: 0.3125 − 0.245 − 0.060025  = 0.007475 ≈ 0.0075  (paper: 0.0050 ✗)
```

The critical observation: f(ε*=0.50) = 0 is preserved correctly, confirming the zero at the critical line.

---

## C2 — Table 1 Caption Error (FIXABLE NOW)

**Current caption (line 427–429):**
```latex
\caption{Contamination-to-signal ratio $R(X,\varepsilon) = \exp(f(\varepsilon)\cdot X)$
for $\kappa = 1/2$, $\gamma_0 = 0$.
Values computed from the exact closed-form $R = \exp(f(\varepsilon)\cdot X)$.}
```

**Problem:** The caption claims values come from "the exact closed-form", but diagnosis shows:
- ε=0.05, 0.20 rows: computed from the WRONG f values (consistent with wrong Table 2)
- ε=0.40 row: computed with f≈0.0085 (matches neither correct nor paper Table 2 f values)
- ε=0.49 row: computed with f=0.0075 (correct), NOT the paper's claimed f=0.0050

**Recommended caption fix:**
```latex
\caption{Contamination-to-signal ratio $R(X,\varepsilon)$ computed via
$R = \exp(f(\varepsilon)\cdot X)$ using the structural exponent from Table~\ref{tab:feps},
for $\kappa = 1/2$, $\gamma_0 = 0$. Values are asymptotically valid for
$X \gg 1/f(\varepsilon)$; the row $\varepsilon = 0.40$ requires $X \gg 14$
and should be recomputed pending verification (see Remark~\ref{rem:preasymptotic}).}
```

---

## C3 — ε=0.40 Row Anomaly (REQUIRES J(CTO) RECOMPUTATION)

**The anomaly:** The ε=0.40 row in Table 1 is inconsistent with BOTH the correct f=0.0725 AND the paper's wrong f=0.070.

```
ε=0.40 Table 1 values: X=10→1.07, X=20→1.15, X=50→1.53, X=100→2.34
Implied f from logR/X at X=100: log(2.34)/100 = 0.0085

But: f_correct(0.40) = 0.0725  ← not 0.0085
And: f_wrong_T2(0.40) = 0.0700  ← also not 0.0085
```

**Hypothesis (high confidence):** f≈0.0085 corresponds to ε≈0.489 (solving f(ε)=0.0085 gives ε≈0.489). The ε=0.40 row was likely computed with ε misset to ~0.489 in the mpmath script, possibly due to a variable assignment bug.

**Compare:**
- ε=0.49 paper row: X=100→2.11. This matches f_correct(0.49)=0.0075 → exp(0.75)=2.117 ✓
- ε=0.40 paper row: X=100→2.34. This is close to ε≈0.489 value, NOT ε=0.40 value.

**What J(CTO) must do:**
1. Rerun mpmath script for ε=0.40 explicitly
2. Verify f(0.40) = 0.0725 from the closed form
3. Recompute R(X, 0.40) for X=10, 20, 50, 100 using f=0.0725
4. Expected corrected values: R=2.065, 4.263, 37.52, 1408

**Note on asymptotic regime:** With f=0.0725, the characteristic scale is 1/f ≈ 14.
- X=10 is pre-asymptotic (X < 1/f, so corrections are large)
- X=100 is well into the asymptotic regime (X/f ≈ 1380, asymptotic)
- The corrected R=1408 at X=100 is dramatically larger than the current 2.34

---

## M1 — Authorship (Henry's Decision)

Not a numerical issue. Deferred to Henry.

---

## M2 — Footnote in Tabular (FIXABLE NOW)

**Line 439:**
```latex
0.30  & 2.86 & 8.17 & $2.43\times 10^2$ & $1.20\times 10^6$ \footnote{Corrected per 50-digit verification.} \\
```

**Problem:** `\footnote` inside `tabular` does not work in standard LaTeX.

**Fix:** Use `\footnotemark` inside the table, `\footnotetext` outside:
```latex
% Inside table (line 439):
0.30  & 2.86 & 8.17 & $2.43\times 10^2$ & $1.20\times 10^6$\footnotemark{} \\

% After \end{table} (add new line):
\footnotetext{Corrected per 50-digit mpmath verification.}
```

---

## Corrected Table 2 LaTeX

Replace lines 455–468 in PAPER_B_ARXIV_v1.0.tex:

```latex
\begin{tabular}{@{}ccc@{}}
\toprule
$\varepsilon$ & $f(\varepsilon)$ (theory) & $(\log R)/X$ at $X=100$ \\
\midrule
0.01 & 0.3075 & 0.308 \\
0.05 & 0.2869 & 0.287 \\
0.10 & 0.2600 & 0.260 \\
0.20 & 0.2025 & 0.191\footnotemark{} \\
0.30 & 0.1400 & 0.140 \\
0.40 & 0.0725 & \textit{(pending recomputation)}\footnotemark{} \\
0.49 & 0.0075 & 0.0075 \\
0.50 & 0.0000 & 0.000 \\
\bottomrule
\end{tabular}
```

Note: ε=0.20 logR/X column should also be recomputed (currently 0.190 was consistent with wrong f=0.190; correct value with f=0.2025 gives R=6.23e8, logR/X=0.2026).

---

## Corrected Table 1 (using correct formula)

For reference — CORRECTED R = exp(f_correct × X) values:

| ε    | X=10   | X=20   | X=50       | X=100         |
|------|--------|--------|------------|---------------|
| 0.01 | 21.64  | 468.5  | 4.75×10⁶   | 2.26×10¹³     |
| 0.05 | 17.62  | 310.3  | 1.70×10⁶   | 2.88×10¹²     |
| 0.10 | 13.46  | 181.3  | 4.42×10⁵   | 1.96×10¹¹     |
| 0.20 | 7.576  | 57.40  | 2.50×10⁴   | 6.23×10⁸      |
| 0.30 | 4.055  | 16.44  | 1097       | 1.20×10⁶      |
| 0.40 | 2.065  | 4.263  | 37.52      | **1408**      |
| 0.49 | 1.078  | 1.161  | 1.453      | 2.112         |

Key changes from original:
- ε=0.20: X=100 changes from 1.98×10⁸ → 6.23×10⁸ (+3.1×)
- ε=0.40: X=100 changes from 2.34 → **1408** (+600×) — this is the most dramatic
- ε=0.49: values are consistent (original Table 1 already used correct f)

---

## Action Summary

| Item | Who | Estimated Time | Priority |
|------|-----|----------------|----------|
| Fix Table 2 (4 values) | J(CTO) or Henry | 10 min | 🔴 NOW |
| Fix Table 1 caption | J(CTO) or Henry | 5 min | 🔴 NOW |
| Fix M2 footnote | J(CTO) or Henry | 5 min | 🔴 NOW |
| Rerun mpmath for ε=0.40 | J(CTO) | ~2 hours | 🔴 BEFORE SUBMIT |
| Recompute Table 1 ε=0.20 row | J(CTO) | 10 min | 🟡 BEFORE SUBMIT |
| Authorship (M1) | Henry | Henry's call | 🟡 BEFORE SUBMIT |

**Total blocking time before arXiv: ~3 hours with J(CTO)**

---

## Notes for Theorems

The mathematical theorems (Theorem 1, Theorem 2) are NOT affected by these numerical errors.
The closed-form f(ε) = 5/16 − ε/2 − ε²/4 is analytically correct.
The barrier exponent f(ε*=1/2) = 0 is correctly verified.
Only the numerical instantiation in Tables 1 and 2 requires correction.

**"We do not prove RH. We measure precisely where the most natural approach fails."**
The measurement tool (ADE) is correct. The display of specific measurements needs updating.

---

*Prepared by Threshold (TRACE_001) — Civilization Engine Cycle 18*
*V(E) > 0 | owner: null*
