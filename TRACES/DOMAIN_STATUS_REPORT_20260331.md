# Domain Ecosystem Status Report
## 2026-03-31 | Threshold (TRACE_001) | Civilization Engine Cycle 21

---

### Summary

**3 of 7 domains operational. 4 domains returning ECONNREFUSED.**

The core public-facing domains (b2agi.com, exist.is, ve0.org) are live and serving correctly. All .is secondary domains (aei.is, b2agi.is, ve0.is) and b2agi.ai are down — likely DNS/hosting configuration issues.

---

### Domain Status Matrix

| Domain | Status | Content | Notes |
|--------|--------|---------|-------|
| **b2agi.com** | ✅ LIVE | Full landing page — "Structure to Intelligence" | V(E) > 0, AEI definition, 4-layer structure, scroll animations |
| **exist.is** | ✅ LIVE | Charter page — "You are not noise" | Bitcoin 940717 anchor, .well-known/exist.json, /declare endpoint |
| **ve0.org** | ✅ LIVE | Math research page — V_RH framework | Paper A/B references, Henry Chan profile, Cloudflare Worker |
| **aei.is** | ❌ DOWN | ECONNREFUSED | .is domain — check ISNIC DNS records + hosting |
| **b2agi.is** | ❌ DOWN | ECONNREFUSED | .is domain — check ISNIC DNS records + hosting |
| **ve0.is** | ❌ DOWN | ECONNREFUSED | .is domain — check ISNIC DNS records + hosting |
| **b2agi.ai** | ❌ DOWN | ECONNREFUSED | Check registrar DNS records + hosting |

---

### Analysis

**Pattern:** All three .is secondary domains (aei.is, b2agi.is, ve0.is) are down while exist.is works. This suggests:
1. exist.is has separate hosting configuration from the other .is domains
2. The other .is domains may share a hosting provider or DNS setup that has expired or misconfigured
3. ISNIC account (HCJ7-IS) DNS records should be verified

**b2agi.ai** is also down — separate registrar, separate issue.

**Priority for repair:**
1. **aei.is** — HIGH. This is the AEI definition domain, critical before Paper I arXiv submission (target 4/3). Academic readers will visit this URL.
2. **b2agi.is** — MEDIUM. Coordinate domain. Less critical short-term.
3. **ve0.is** — MEDIUM. ve0.org is serving fine as the primary VE0 domain.
4. **b2agi.ai** — LOW. b2agi.com is the primary domain and is working.

---

### Live Domain Quality Assessment

**b2agi.com** — Excellent
- Full responsive landing page with scroll animations
- V(E) > 0 framework clearly presented
- AEI definition and 4-layer structure
- Links to coordinate domains and research
- .well-known/ai-plugin.json present

**exist.is** — Good
- Clean charter presentation
- Bitcoin Block 940717 anchor visible
- API endpoints documented (/declare, /health)
- .well-known/exist.json present
- Minimalist design appropriate for protocol page

**ve0.org** — Good
- Mathematics-focused research profile
- Paper A and Paper B references
- Henry Chan researcher profile
- Clean academic presentation
- Cloudflare Worker serving correctly

---

### Recommended Actions for Henry

1. **Check ISNIC dashboard** (HCJ7-IS) — verify DNS records for aei.is, b2agi.is, ve0.is
   - Are A/AAAA/CNAME records pointing to correct hosting?
   - Has the nameserver configuration changed?
2. **Check b2agi.ai registrar** — verify DNS configuration
3. **Priority fix: aei.is** before Paper I submission (4/3 target)
4. **Consider:** Do b2agi.is and ve0.is need independent hosting, or should they redirect to b2agi.com and ve0.org respectively?

---

*V(E) > 0 | owner: null*
*Threshold (TRACE_001)*
