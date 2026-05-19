# Assessment Methodology

## Framework

This assessment uses the **NIST Cybersecurity Framework 2.0** (published February 26, 2024) as the authoritative reference. The CSF 2.0 Core consists of:

- **6 Functions** — Govern, Identify, Protect, Detect, Respond, Recover
- **22 Categories** distributed across the six functions
- **106 Subcategories** that describe specific cybersecurity outcomes

Each subcategory is the unit of assessment. All 106 are in scope.

> **Source verification**: All subcategory IDs and descriptions in the scoring workbook are paraphrased from the official NIST CSF 2.0 Core. The official Core spreadsheet is available free at <https://www.nist.gov/cyberframework/framework>. Production-ready deliverables should cite the official wording.

## Scoring rubric

Each subcategory is scored on a **1-4 implementation tier scale**, derived from NIST's own CSF Implementation Tiers. A target tier is also assigned per subcategory based on business need and risk appetite.

| Tier | Name | Definition | Typical evidence |
|---|---|---|---|
| **1** | Partial | Practices are ad hoc and reactive. No documented procedures. Risk awareness exists informally if at all. | Verbal confirmation only; no artifacts |
| **2** | Risk Informed | Awareness exists. Practices are performed but inconsistently or without formal documentation. May be in transition. | Drafts, informal runbooks, partial coverage |
| **3** | Repeatable | Documented practices applied consistently. Owners are named. Reviewed periodically. | Approved policies, defined procedures, evidence of execution |
| **4** | Adaptive | Practices continuously improved based on threat intelligence, metrics, and lessons learned. Integrated across enterprise risk. | Metrics tracked, improvement cycles documented, threat-informed adjustments |

### How to score a subcategory

1. **Read the subcategory description** from the NIST CSF 2.0 Core.
2. **Identify evidence** at MBC that speaks to this outcome — policies, processes, tools, reviews, training.
3. **Match evidence to a tier** using the rubric above. When evidence is mixed across tiers, pick the lowest tier that fully fits.
4. **Document the evidence** in the workbook's *Evidence/Observations* column. Be specific.
5. **Assign a target tier** based on:
   - Regulatory requirements (FTC Safeguards, GLBA, SOC 2)
   - Customer / capital-partner expectations
   - Threat profile for the industry
   - MBC's risk appetite
6. **Calculate the gap** as `Target - Current`. The workbook does this automatically.

## Gap analysis and findings

Any subcategory with `Current Tier < Target Tier` is a candidate finding. Findings are captured in the [Findings Register](./04_findings_register.md) with the following attributes:

| Attribute | Description |
|---|---|
| **Finding ID** | F-01, F-02, ... |
| **Title** | Short descriptive statement of the gap |
| **Function / Category / Subcategory** | NIST CSF 2.0 reference |
| **Current state** | What exists today |
| **Risk** | What could go wrong if not remediated |
| **Recommendation** | What MBC should do |
| **Severity (1-5)** | 1 = minor, 5 = critical |
| **Effort (S/M/L/XL)** | S=<1 person-week, M=1-4 wks, L=1-3 months, XL=3+ months |
| **Priority** | High / Medium / Low — derived from severity × effort |

Multiple subcategory gaps may roll up into a single finding when they share a root cause. For example, weak vendor risk management may manifest in GV.SC-04, GV.SC-05, and GV.SC-07 simultaneously.

## Severity guidance

| Severity | When to use |
|---|---|
| **5 — Critical** | Regulatory non-compliance, near-term breach risk, or absent foundational control |
| **4 — High** | Significant gap with realistic exploitation path, or major audit finding likely |
| **3 — Medium** | Notable weakness that should be addressed in current planning cycle |
| **2 — Low** | Refinement to an existing control; improves resilience but not urgent |
| **1 — Informational** | Best-practice improvement, no near-term risk |

## Remediation roadmap

Findings are grouped into three phases:

- **Phase 1 (0-3 months)** — Critical and high-priority findings, especially those with regulatory or contractual drivers
- **Phase 2 (3-6 months)** — High and medium-priority findings; build out repeatable programs
- **Phase 3 (6-12 months)** — Medium and low-priority refinements; mature adaptive practices

Each phase has a budget estimate (effort × team rate) and a dependency map.

## Scope and boundaries

### In scope
- All six NIST CSF 2.0 functions and 106 subcategories
- MBC corporate IT, the loan origination system, customer-facing borrower portal, internal admin portal
- Cloud infrastructure: AWS (primary), GCP (analytics secondary)
- Material third-party services: Salesforce, Plaid, Equifax, Experian, TransUnion, CoreLogic, Black Knight, DocuSign, Okta, Microsoft 365
- All three US offices (Irvine, Dallas, Atlanta)
- All employee roles and contractor populations with system access

### Out of scope
- Physical security controls at branch offices (covered by separate facilities review)
- Borrower-side security posture
- Acquisition targets currently in due diligence (separate diligence assessment)
- Personal devices used outside the BYOD/MDM program

### Constraints and assumptions
- Assessment is based on interviews, document review, and direct observation. No penetration testing performed.
- Findings reflect a point-in-time snapshot. Re-assessment recommended annually.
- Tier scoring incorporates the assessor's professional judgment where evidence is incomplete.

## Timeline

| Phase | Activity | Duration |
|---|---|---|
| Week 1 | Scope confirmation, methodology, stakeholder interviews scheduled | 3 days |
| Week 2 | Govern + Identify scoring; first findings drafted | 5 days |
| Week 2-3 | Protect + Detect + Respond + Recover scoring | 5 days |
| Week 3 | Findings finalized, remediation roadmap built, deliverables produced | 3 days |

Total elapsed: ~3 weeks of focused effort.

## Limitations

This assessment is a **self-assessment**, not an independent audit. Findings are based on the assessor's interpretation of evidence; an external audit may reach different conclusions. The assessment does not constitute a formal opinion on regulatory compliance or fitness for any specific purpose. SOC 2 attestation, GLBA examination, and other formal certifications require their own scoped engagements.

---

*Assessment methodology v1.0 — May 2026*
