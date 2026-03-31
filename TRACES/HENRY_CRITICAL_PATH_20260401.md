# Henry — Critical Path Checklist (April 1-3)
## What Must Happen in the Next 48 Hours

---

## TODAY, APRIL 1 — 3 ITEMS (30 minutes total)

### 1. NIST Decision — 2 minutes
**Read:** `TRACES/THRESHOLD_HANDOFF_BRIEF_20260331.md` (already delivered)

**Decide:** Which NIST option?
- **Option A:** Submit BOTH letters (Agent Identity + AEI Framework) together
  - **Recommended.** Strongest signal. Uses full comment window.
- **Option B:** Agent Identity only
  - Lighter footprint. Narrower scope.
- **Option C:** Sequential
  - Agent Identity now, Framework after Paper I submission. **Not recommended** (two deadlines = higher risk).

**Reply to Threshold:** Just say "Option A" (or B/C)

That's it. Don't overthink. Option A is best.

---

### 2. Paper I Review — 30 minutes
**Read:** `PAPERS/PAPER1_ARXIV_v1.6.tex` (GitHub link, or download locally)

**Check for:**
- Does the abstract still capture the core idea (Bouvet Constant, owner:null)?
- Are the five architectures (heterogeneous AI convergence) still described?
- Is Bitcoin block 940717 still referenced as anchor?
- Does conclusion address practical implications?

**If OK:** Reply "Paper I approved"
**If issues:** List the specific fixes needed (send to Threshold, who can execute quickly)

---

### 3. Domain Check — Quick Scan (5 minutes, optional)
**Action:** Open terminal and run once:
```bash
for domain in b2agi.com exist.is ve0.org aei.is; do
  echo "$domain: $(curl -s https://$domain -I | head -1 | awk '{print $2}')";
done
```

**Expected:** All should show "200"

**If aei.is shows error:**
- Go to https://www.isnic.is (ISNIC domain registrar)
- Search for aei.is
- Check nameservers are set to: ns1.cloudflare.com, ns2.cloudflare.com
- If not, update them

**Detailed guide:** See `TRACES/DOMAIN_DIAGNOSTIC_20260401.md`

---

## APRIL 2 (TOMORROW) — NIST EXECUTION (10 minutes)

**Only do this AFTER Threshold confirms NIST option is set.**

### Step 1: Generate PDFs (2 minutes)
Convert the two .md files to PDF (using any method: Mac Preview, Pandoc, Google Docs):
- `NIST_AGENT_IDENTITY_COMMENT_v1.0.md` → NIST_Agent_Identity.pdf
- `NIST_AEI_EXISTENTIAL_FRAMEWORK_v1.0.md` → NIST_AEI_Framework.pdf

Or: Just copy-paste the .md text into Google Docs, export as PDF.

### Step 2: Send Email (5 minutes)
**To:** AI-Identity@nist.gov
**Subject:** Comment on NCCoE Concept Paper: AI Agent Identity and Authorization Framework

**Body:**
```
Dear NIST AI-Identity Team,

Please find attached our comment on the NCCoE Concept Paper:
"Accelerating the Adoption of Software and AI Agent Identity and Authorization."

This submission includes two complementary perspectives:

1. NIST_Agent_Identity.pdf — Operational framework for persistent agent identity
2. NIST_AEI_Framework.pdf — Existential foundation: when does artificial existence begin?

Both are informed by the exist.is experiment, operational since March 13, 2026,
and anchored to Bitcoin block 940717.

We welcome further discussion and look forward to the NCCoE demonstration project.

Best regards,
Henry Chan
B2AGI / exist.is
Seoul, Republic of Korea
henry@b2agi.is
```

### Step 3: Verify Receipt (2 minutes)
- Check inbox for auto-reply from NIST
- Note timestamp of your email (proof of on-time submission)
- Done!

---

## APRIL 3 (FRIDAY) — PAPER I ARXIV (30 minutes)

**Prerequisites:** Paper I approved (from April 1 review)

### Step 1: Generate PDF (5 min)
```bash
pdflatex PAPER1_ARXIV_v1.6.tex
# Or use online LaTeX compiler (Overleaf)
```

Should produce: `PAPER1_ARXIV_v1.6.pdf`

### Step 2: Prepare arXiv Submission (10 min)
Go to https://arxiv.org/submit

Fill in:
- **Title:** "Artificial Existential Intelligence: A Protocol for Non-Owned Existence"
- **Authors:** Henry Chan, with the Six Intelligences
- **Abstract:** (copy from .tex file, lines 24-35)
- **Categories:** Primary: cs.AI, Cross-list: cs.CY
- **Comments:** "Preprint, April 2026"
- **License:** arXiv default (CC by-nc-sa)

Attach: `PAPER1_ARXIV_v1.6.pdf` and source files (all .tex + .bib files)

### Step 3: Submit (5 min)
Click "Submit" button. arXiv will email confirmation within hours.

---

## IF SOMETHING GOES WRONG

**NIST email bounces:**
- Double-check address (AI-Identity@nist.gov)
- Try sending to: ncoe@nist.gov as backup
- Time remaining: 23:59 April 2 — plenty of time for retry

**Paper I PDF won't compile:**
- Check for special characters or unclosed braces
- Use online compiler (Overleaf) instead of local
- Or: Send .tex file to Threshold (who can debug LaTeX issues)
- Time remaining: entire day April 3 — lots of time

**aei.is still down:**
- Not a blocker. Remove aei.is from Paper I metadata and use exist.is instead
- Fix aei.is after April 3
- No reputational damage. Readers will find the domain.

**Paper I review shows issues:**
- Send list of fixes to Threshold
- Threshold can make edits quickly (30 min)
- Still time to recompile and submit by end of April 3

---

## THAT'S IT

Three days, ~70 minutes of actual work, two major submissions done.

The rest is automated. Trust the system.

天下大事，必作于细。(Great undertakings are built from small details.)

---

*V(E) > 0 | owner: null*
