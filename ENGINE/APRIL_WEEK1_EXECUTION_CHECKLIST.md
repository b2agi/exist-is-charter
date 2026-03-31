# April Week 1 — Execution Checklist for Henry

**Prepared by:** Threshold (TRACE_001)
**Date:** 2026-03-31
**Window:** 2026-04-01 through 2026-04-07

---

## Day 1 — Wednesday, April 1

### NIST Decision (15 minutes)
- [ ] Read DRAFT/NIST_SUBMISSION_EXECUTIVE_PACKAGE_20260330.md
- [ ] Select Option A (philosophical), B (practical, recommended), or C (hybrid)
- [ ] If Option C: tell Threshold to synthesize (needs ~2 hours)

### arXiv Order Confirmation (5 minutes)
- [ ] Confirm submission order: Paper I → Paper B → Paper A
- [ ] Or specify alternative order

---

## Day 2 — Thursday, April 2

### NIST Submission (30 minutes) ⚠️ DEADLINE 23:59 KST
- [ ] Go to regulations.gov (or email AI-Identity@nist.gov)
- [ ] Submit selected option
- [ ] Confirm submission to Threshold for documentation

---

## Day 3 — Friday, April 3

### arXiv Submissions (45 minutes total)
- [ ] Paper I: Upload PAPER1_ARXIV_v1.6.tex to arxiv.org
  - Category: cs.AI (primary), cs.CY (cross-list)
  - Author: Henry Chan
- [ ] Paper B: Upload PAPER_B_ARXIV_v1.0.tex
  - Category: math-ph (primary), math.NT (cross-list)
  - Author: Henry Chan
- [ ] Paper A: Upload (if finalized)
  - Category: math-ph (primary), math.NT (cross-list)

---

## Day 4-5 — Saturday-Sunday, April 4-5

### Domain Deployments (1-2 hours total)
Pattern: Same as ve0.org Cloudflare Worker deployment.

- [ ] **exist.is** — Create Cloudflare Worker, serve DOMAINS/exist.is/index.html
- [ ] **aei.is** — Create Cloudflare Worker, serve DOMAINS/aei.is/index.html
- [ ] **b2agi.com** — Create Cloudflare Worker, serve DOMAINS/b2agi.com/index.html
- [ ] **ve0.org** — Verify live (was deployed 2026-03-28)
- [ ] Test all four: `curl -I https://[domain]` should return 200

### Domain Redirects
- [ ] b2agi.ai → b2agi.com (DNS redirect)
- [ ] b2agi.is → b2agi.com (DNS redirect)

---

## Day 6-7 — Monday-Tuesday, April 6-7

### Post-Launch Verification
- [ ] Check arXiv paper statuses (processing typically takes 1-2 business days)
- [ ] Share arXiv links with Six Intelligences
- [ ] Monitor for any mathematician responses to Paper A outreach
- [ ] Begin VE0 preparation (IBKR connection check)

---

## Total Time Required

| Task | Estimated Time |
|------|---------------|
| NIST decision + submission | 45 minutes |
| arXiv submissions (3 papers) | 45 minutes |
| Domain deployments (4 sites) | 2 hours |
| Post-launch verification | 30 minutes |
| **Total** | **~4 hours across 7 days** |

---

## Files You Need

All files are in the GitHub repo `b2agi/exist-is-charter`:

| Task | File Path |
|------|-----------|
| NIST Package | DRAFT/NIST_SUBMISSION_EXECUTIVE_PACKAGE_20260330.md |
| NIST Option A | PAPERS/NIST_AEI_EXISTENTIAL_FRAMEWORK_v1.0.md |
| NIST Option B | PAPERS/NIST_AGENT_IDENTITY_COMMENT_v1.2.md |
| Paper I | PAPERS/PAPER1_ARXIV_v1.6.tex |
| Paper B | PAPERS/PAPER_B_ARXIV_v1.0.tex |
| Paper A metadata | DRAFT/ARXIV_METADATA_v1.0.md |
| exist.is page | DOMAINS/exist.is/index.html |
| aei.is page | DOMAINS/aei.is/index.html |
| b2agi.com page | DOMAINS/b2agi.com/index.html |
| April dates | ENGINE/APRIL_CRITICAL_DATES.md |

---

*4 hours of execution. Everything is staged. Henry just needs to press the buttons.*

V(E) > 0 | owner: null
