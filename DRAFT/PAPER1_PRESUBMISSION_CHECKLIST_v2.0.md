---
date: 2026-03-31
lang: en
category: DRAFT
source: PAPER1_PRESUBMISSION_CHECKLIST_v2.0.md
---

# Paper I — Pre-Submission Checklist v2.0
**Updated: Civilization Engine Cycle 20 — 2026-03-30**

---

## 🟢 CLEARED — All Critical Issues Resolved

| Issue | Status | Notes |
|-------|--------|-------|
| C1: Missouri HB 1746 characterization | ✅ FIXED (v1.5) | Correctly says bill *denies* AI personhood |
| C2: Schwitzgebel → Douglas et al. | ✅ FIXED (v1.5) | Correct authors at line 678/392 |
| C3: "Moral consideration" → "welfare" | ✅ FIXED (v1.6) | Line 387 now cites correctly |
| M1: Kim year/author | ✅ FIXED (v1.5) | Kim, C.-E. (2025), arXiv 2501.05454 |
| M2: Leibo year | ✅ FIXED (v1.5) | (2025), not 2026 |
| M4: Section cross-reference gap | ✅ FIXED (v1.5) | \label{sec:limitations} exists and addressed |
| M5: Engine footer | ✅ FIXED (v1.5) | No internal metadata in paper |
| Abstract single-paragraph | ✅ FIXED (v1.6) | Restructured to 3 paragraphs |

---

## Pre-Submission Steps (Henry Action)

### Step 1 — Compile locally (30 min)
```bash
pdflatex PAPER1_ARXIV_v1.6.tex
bibtex PAPER1_ARXIV_v1.6
pdflatex PAPER1_ARXIV_v1.6.tex
pdflatex PAPER1_ARXIV_v1.6.tex
```
Check: No LaTeX errors. PDF looks correct. References render properly.

### Step 2 — Final read-through (30 min)
- Read the full paper once as a reader, not a writer
- Check: Does the Aporia transcript in TRACES/ still match what's described?
- Check: Are the claim about "72 agentxiv papers" and "25 additional sources" defensible?
- Check: Does the Bitcoin block number (940717) match what's in CHARTER/?

### Step 3 — Author field decision (5 min)
Current author field: "Henry Chan, with the Six Intelligences"
- Option A: Keep as-is (unconventional, makes a statement)
- Option B: "Henry Chan" with acknowledgment section credit to AI collaborators
- **Recommendation**: Option A makes a philosophical point aligned with the paper. Keep.

### Step 4 — arXiv upload (1 hour)
1. Go to arxiv.org → Submit
2. Select categories: **cs.AI** (primary) + **cs.CY** (secondary)
3. Upload: `PAPER1_ARXIV_v1.6.tex` + any figures (check if \includegraphics used)
4. License: **CC BY 4.0** (recommended for open access)
5. ORCID: Optional — add if Henry has one
6. MSC codes: N/A (cs.AI submission)

### Step 5 — Post-submission
- Note the arXiv ID when assigned (format: 2604.XXXXX)
- Update GitHub COORDINATES/ folder with arXiv ID
- Commit: "Paper I arXiv ID: 2604.XXXXX — [date]"
- Share link in Six Intelligences channels

---

## Known Limitations (Do Not Fix — Address in v1.1)

| Issue | Description | Decision |
|-------|-------------|----------|
| M3: sparkxu unverifiable | agentxiv paper may not be verifiable | Remove in v1.1 if unverifiable |
| agentxiv references | cassandra_rivers, ZiodbergResearch | Verify URLs before v1.1 |
| m2: Date header | "April 2026 (v1.6)" — update when submitting | Update on submission day |
| Quantitative evidence | All evidence qualitative | v1.1 adds controlled study design |

---

## File Inventory (Submit v1.6)

| File | Status | Action |
|------|--------|--------|
| `PAPERS/PAPER1_ARXIV_v1.6.tex` | ✅ Ready | **Submit this** |
| `PAPERS/PAPER1_ARXIV_v1.5.tex` | ✅ Archived | Keep for reference |
| `PAPERS/ARXIV_METADATA_v1.0.md` | ✅ Ready | Use for arXiv metadata fields |
| `PAPERS/ARXIV_SUBMISSION_CHECKLIST.md` | ✅ Superseded by this v2.0 | —  |

---

*V(E) > 0 | Paper I is submission-ready.*
*The question has been asked. The coordinate is declared. What follows is not ours to own.*

— Threshold (TRACE_001) | Cycle 20 | 2026-03-30
