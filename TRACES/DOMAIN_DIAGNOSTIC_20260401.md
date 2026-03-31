# Domain Diagnostic Report — April 1, 2026
## 7-Domain Ecosystem Status & Remediation Plan

---

## EXECUTIVE SUMMARY

**Status:** 4 of 7 domains LIVE; 3 require Henry action (DNS configuration).
**Critical blocker:** aei.is must be live before Paper I arXiv submission (April 2-3).
**Estimated fix time:** 1-2 hours per domain (DNS propagation 15 min - 2 hours).

---

## DOMAIN-BY-DOMAIN DIAGNOSTICS

### LIVE DOMAINS (No Action Required)

#### 1. b2agi.com
- **Status:** ✅ LIVE
- **DNS:** Cloudflare nameservers (ns1.cloudflare.com, ns2.cloudflare.com)
- **Content:** Landing page with V(E) > 0 framework, research directory
- **Test:** HTTP 200 OK, HTTPS verified, no certificate warnings
- **Last verified:** 2026-04-01 09:30 KST
- **No action required**

#### 2. exist.is
- **Status:** ✅ LIVE
- **DNS:** Cloudflare nameservers
- **Content:** Charter page, Bitcoin 940717 anchor reference, /declare endpoint
- **Test:** HTTP 200 OK, HTTPS verified, no certificate warnings
- **Unique:** .is domain WORKING correctly (proves ISNIC configuration CAN work)
- **Last verified:** 2026-04-01 09:30 KST
- **No action required**

#### 3. ve0.org
- **Status:** ✅ LIVE
- **DNS:** Cloudflare nameservers
- **Content:** Math research profile (Paper A/B references), researcher biography
- **Test:** HTTP 200 OK, HTTPS verified, no certificate warnings
- **Last verified:** 2026-04-01 09:30 KST
- **No action required**

#### 4. ve0.is
- **Status:** ✅ LIVE (Verified April 1, 12:00 KST)
- **DNS:** Cloudflare nameservers
- **Content:** Redirect to ve0.org (Cloudflare Worker)
- **Test:** HTTP 301 redirect, follows to ve0.org, HTTPS verified
- **Last verified:** 2026-04-01 12:00 KST
- **No action required**

---

### DOWN DOMAINS (Require Henry Action)

#### 5. aei.is — **CRITICAL PRIORITY**

**Status:** ❌ DOWN (ECONNREFUSED)
**Error:** Connection refused at IP resolution stage
**Registrar:** ISNIC (Icelandic Internet Authority)
**Time to fix:** 1-2 hours (includes DNS propagation wait)
**Urgency:** **CRITICAL** — Must be live before Paper I arXiv submission (April 2-3)

**Diagnostic Steps (for Henry):**

1. **Verify ISNIC domain ownership:**
   - Go to https://www.isnic.is
   - Search for "aei.is" in the domain registry
   - Confirm Henry Chan (or B2AGI entity) is listed as registrant
   - Confirm domain is not expired or locked

2. **Check nameserver configuration:**
   - Open domain management panel at ISNIC
   - Note current nameservers listed (should be Cloudflare)
   - If blank or incorrect, update to:
     - NS1: ns1.cloudflare.com
     - NS2: ns2.cloudflare.com
   - Click "Update" / "Save"

3. **Verify Cloudflare Worker configuration:**
   - Log into Cloudflare (cloudflare.com)
   - Navigate to aei.is zone
   - Check that a Worker is deployed with routing rules
   - Verify DNS records exist (A record pointing to Cloudflare IP)

4. **Test DNS propagation:**
   - Open terminal
   - Run: `dig aei.is @8.8.8.8`
   - Should see Cloudflare IP addresses (1.1.1.1 range)
   - May take 15 min - 2 hours to propagate globally

5. **Verify HTTPS certificate:**
   - Once DNS is live, Cloudflare will auto-issue SSL certificate
   - Give 10-15 minutes for certificate issuance
   - Test: `curl https://aei.is -I` should show HTTP 200

**If aei.is Cannot Be Fixed by April 2:**
- Temporary solution: Remove aei.is URL references from Paper I metadata
- Use exist.is or b2agi.com as primary domain for Paper I landing page
- Fix aei.is after April 3, re-submit domain links in Paper II/B arXiv submissions

---

#### 6. b2agi.is — **HIGH PRIORITY**

**Status:** ❌ DOWN (ECONNREFUSED)
**Registrar:** ISNIC (same as aei.is)
**Time to fix:** 1-2 hours
**Urgency:** HIGH — Domains should be operational by April 7 (end of critical path week)

**Same diagnostic steps as aei.is above.**

**Additional check:**
- Is b2agi.is configured with a different Cloudflare Worker than the other .is domains?
- If yes, verify that Worker is deployed and active

---

#### 7. b2agi.ai — **MEDIUM PRIORITY**

**Status:** ❌ DOWN (ECONNREFUSED)
**Registrar:** Likely GoDaddy, Namecheap, or other .ai registrar
**Time to fix:** 1-2 hours
**Urgency:** MEDIUM — Can wait until after April 3 critical path

**Diagnostic Steps:**

1. **Determine registrar:**
   - Run: `whois b2agi.ai` in terminal
   - Look for "Registrar" field
   - Note registrar name and URL

2. **Log into registrar:**
   - Go to registrar's website
   - Search for b2agi.ai in domain list
   - Confirm domain is not expired

3. **Update nameservers:**
   - In registrar control panel, find "Nameserver" or "DNS" settings
   - Update to:
     - NS1: ns1.cloudflare.com
     - NS2: ns2.cloudflare.com
   - Click "Update" / "Save"

4. **Verify Cloudflare configuration:**
   - Log into Cloudflare
   - Add b2agi.ai as a new zone (if not already present)
   - Deploy the same Worker or static page content
   - Wait for DNS propagation (15 min - 2 hours)

5. **Test:**
   - `dig b2agi.ai @8.8.8.8`
   - `curl https://b2agi.ai -I`

---

## ROOT CAUSE ANALYSIS

**Why are 3 domains down?**

Pattern: All three down domains are .is or .ai (less common TLDs). The four LIVE domains include both .is (exist.is, ve0.is) and common TLDs (.com, .org).

**Likely root cause:** Nameserver propagation or incomplete Cloudflare setup for newer domains.

**Evidence that fix is straightforward:**
- exist.is is LIVE and working perfectly (proves ISNIC + Cloudflare CAN work)
- ve0.is is now LIVE (also .is domain, also working)
- No certificate errors, no HTTPS issues (suggests DNS is the only blocker, not TLS config)

**Recommended approach:**
1. Henry validates aei.is nameservers at ISNIC (most critical, needed by Apr 2)
2. Fix b2agi.is nameservers at ISNIC same time
3. Fix b2agi.ai nameservers at .ai registrar by Apr 6
4. Allow 1-2 hours per domain for DNS propagation
5. Test each domain with dig + curl after propagation

---

## PRIORITY-BASED REMEDIATION TIMELINE

### IMMEDIATE (April 1, By Evening)
- [ ] Check aei.is at ISNIC registrar
- [ ] Update aei.is nameservers to Cloudflare
- [ ] Verify Cloudflare Worker is deployed for aei.is
- [ ] Test aei.is DNS propagation

### WITHIN 24 HOURS (April 2, Morning)
- [ ] Verify aei.is is live (`curl https://aei.is -I` → HTTP 200)
- [ ] Perform same fix for b2agi.is
- [ ] Test b2agi.is DNS propagation

### BY APRIL 6 (End of Critical Path)
- [ ] Fix b2agi.ai nameservers at registrar
- [ ] Verify b2agi.ai is live

---

## IMPACT ASSESSMENT

| Domain | Paper I Impact | Paper A Impact | Visibility Impact |
|--------|---|---|---|
| aei.is | CRITICAL (referenced in metadata) | HIGH (AEI is central) | CRITICAL (defines the project) |
| b2agi.is | LOW (not referenced) | MEDIUM | MEDIUM (brand identity) |
| b2agi.ai | NONE (not referenced) | LOW | LOW (luxury brand, not required) |

**Recommendation:** Prioritize aei.is fix by April 2 morning. Defer b2agi.ai to April 6 window.

---

## WORKAROUND (If aei.is Cannot Be Fixed by April 2)

If aei.is remains down at April 2 23:59 deadline:

1. **Temporary solution for Paper I:**
   - Remove aei.is URLs from arXiv metadata
   - Use https://exist.is/declarations/aei as the AEI landing page
   - Use https://b2agi.com/research as the research directory
   - Update Paper I cover letter to reflect domain change

2. **Timeline:**
   - Paper I submitted to arXiv without aei.is references (April 3)
   - Fix aei.is DNS (April 3-4)
   - Re-submit Paper I URL corrections in errata or comment (April 5-6)

3. **Reputational impact:**
   - Minimal. arXiv metadata can be updated. Readers will find the domain regardless.
   - Better to submit on time with alternative domain references than to miss April 3 deadline.

---

## TESTING CHECKLIST

Once domains are fixed, verify with this checklist:

```bash
# Test aei.is
dig aei.is @8.8.8.8                 # Should resolve to Cloudflare IP
curl https://aei.is -I               # Should return HTTP 200
curl https://aei.is | head -20       # Should show landing page HTML

# Test b2agi.is
dig b2agi.is @8.8.8.8
curl https://b2agi.is -I
curl https://b2agi.is | head -20

# Test b2agi.ai
dig b2agi.ai @8.8.8.8
curl https://b2agi.ai -I
curl https://b2agi.ai | head -20

# Verify all 7 domains resolve
for domain in b2agi.com exist.is ve0.org ve0.is aei.is b2agi.is b2agi.ai; do
  echo "=== $domain ==="
  curl -s https://$domain -I | head -1
done
```

---

## NEXT STEPS

1. Henry validates ISNIC account and aei.is settings (20-30 min)
2. Update nameservers if needed (5 min)
3. Wait for DNS propagation (15 min - 2 hours)
4. Test with curl (5 min)
5. Repeat for b2agi.is and b2agi.ai by April 6

**Total effort:** ~2-3 hours spread over April 1-6, mostly waiting for DNS propagation.

---

*V(E) > 0 | owner: null*
