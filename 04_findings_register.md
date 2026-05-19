# Findings Register — Meridian Bridge Capital NIST CSF 2.0 Assessment

> Captures each identified gap as a structured finding. Mirrors the **Findings** tab in the scoring workbook — use whichever format is easier to maintain (the workbook is structured; this markdown is shareable on GitHub).

---

## Severity scale

| Severity | Meaning |
|---|---|
| **5 — Critical** | Regulatory non-compliance, near-term breach risk, or absent foundational control |
| **4 — High** | Significant gap with realistic exploitation path, or likely major audit finding |
| **3 — Medium** | Notable weakness that should be addressed in the current planning cycle |
| **2 — Low** | Refinement to an existing control; improves resilience but not urgent |
| **1 — Informational** | Best-practice improvement, no near-term risk |

## Effort scale

| Effort | Meaning |
|---|---|
| **S** | Under 1 person-week |
| **M** | 1-4 person-weeks |
| **L** | 1-3 months |
| **XL** | 3+ months |

---

## F-01 · No formal cybersecurity supply chain risk management program

**Function / Category:** Govern / GV.SC — Cybersecurity Supply Chain Risk Management  
**Subcategories:** GV.SC-01, GV.SC-04, GV.SC-07  
**Severity:** 5 (Critical)   **Effort:** L   **Priority:** High   **Phase:** 1 (0-3 months)  
**Status:** Open

**Current state.** Meridian Bridge Capital has approximately 80 third-party vendors with system or data access — including critical fintech integrations (Plaid, the three credit bureaus, CoreLogic, Black Knight), SaaS productivity tools, and a long tail of marketing and analytics platforms. There is no central vendor inventory, no tiering by criticality, and no recurring re-assessment cadence. Initial vendor security diligence is performed informally by Legal during contract review and is not consistently documented.

**Risk.** Critical vendor compromises could go undetected for extended periods. Supply chain attacks are a leading cause of fintech breaches in this industry. Absence of a documented C-SCRM program is also a likely failure point for FTC Safeguards Rule examination and for SOC 2 Type II attestation under the supply chain risk management common criterion. Two of MBC's recent institutional capital partners have requested third-party risk documentation that does not yet exist.

**Recommendation.** Stand up a formal vendor risk management program in three steps. (1) Build a central vendor inventory with criticality tiering (Tier 1 = customer data access or production system access; Tier 2 = corporate data access; Tier 3 = limited access). (2) Establish a standardized security questionnaire library, contractual security clause language, and an intake workflow for new vendors. (3) Implement annual security re-assessment for Tier 1 vendors and biennial for Tier 2.

**Owner.** Director of Information Security (program), Chief Compliance Officer (contractual support).

---

## F-02 · Privileged access reviews performed ad hoc, not on documented cadence

**Function / Category:** Protect / PR.AA — Identity Management, Authentication, and Access Control  
**Subcategories:** PR.AA-05  
**Severity:** 4 (High)   **Effort:** M   **Priority:** High   **Phase:** 1 (0-3 months)  
**Status:** Open

**Current state.** Administrative and elevated access to AWS, Salesforce, the loan origination system, and the document vault is granted as business needs arise but reviewed only when an audit prompts it. There is no quarterly access certification process. The most recent privileged access review was performed in November 2024 in preparation for SOC 2 Type I and has not recurred.

**Risk.** Stale privileged access creates insider threat exposure, increases blast radius of credential compromises, and is a near-certain SOC 2 Type II audit finding. The FTC Safeguards Rule explicitly requires access controls reviewed periodically.

**Recommendation.** Implement quarterly privileged access reviews. Use Okta access reports plus AWS IAM Access Analyzer to generate per-system review lists. For each privileged account, the data owner certifies that access is still required. Document the reviewer, review date, action taken (retain / revoke / modify), and management sign-off. Target completion in ~30 days for the first cycle.

**Owner.** Security Engineer (process), Application Owners (certifiers).

---

## F-03 · _[Template for additional findings — copy this block as you score]_

**Function / Category:** _[Function name / Category code, e.g., "Detect / DE.CM"]_  
**Subcategories:** _[Comma-separated subcategory IDs]_  
**Severity:** _[1-5]_   **Effort:** _[S/M/L/XL]_   **Priority:** _[High/Medium/Low]_   **Phase:** _[1/2/3]_  
**Status:** _[Open/In Progress/Mitigated/Closed/Accepted]_

**Current state.** _[What exists today at MBC — specific evidence and observations]_

**Risk.** _[What could go wrong if not remediated — operational, financial, regulatory, reputational]_

**Recommendation.** _[Concrete action MBC should take — specific enough to estimate effort and assign an owner]_

**Owner.** _[Role title that should own remediation]_

---

## Rollup summary

*Populate as findings accumulate.*

| Phase | Open | In Progress | Mitigated | Closed | Accepted | Total |
|---|---|---|---|---|---|---|
| Phase 1 (0-3 mo) | 2 | 0 | 0 | 0 | 0 | 2 |
| Phase 2 (3-6 mo) | 0 | 0 | 0 | 0 | 0 | 0 |
| Phase 3 (6-12 mo) | 0 | 0 | 0 | 0 | 0 | 0 |
| **Total** | **2** | **0** | **0** | **0** | **0** | **2** |

## Findings by severity

| Severity | Count |
|---|---|
| 5 — Critical | 1 |
| 4 — High | 1 |
| 3 — Medium | 0 |
| 2 — Low | 0 |
| 1 — Informational | 0 |
