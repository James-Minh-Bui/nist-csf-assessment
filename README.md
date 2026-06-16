# NIST CSF 2.0 Maturity Assessment — Meridian Bridge Capital

> An end-to-end cybersecurity governance, risk, and compliance assessment performed against the **NIST Cybersecurity Framework 2.0**, for a fictional commercial real estate fintech lender.

## About this project

This is a self-directed portfolio assessment built to demonstrate practical GRC capability: framework fluency, evidence-based scoring, gap analysis, and remediation roadmapping. The subject organization is fictional, but the company profile, scope, and findings are designed to reflect realistic conditions at a ~180-employee fintech lender operating in a regulated environment.

The assessment evaluates current maturity across all six NIST CSF 2.0 functions, scores all 106 subcategories against a four-tier maturity scale, identifies 10 priority findings, and produces a phased 12-month remediation roadmap with effort and cost estimates.

**Framework:** [NIST Cybersecurity Framework 2.0](https://www.nist.gov/cyberframework) (published February 2024)

---

## Subject organization

**Meridian Bridge Capital (MBC)** is a fictional commercial real estate lending platform offering bridge loans, multifamily acquisition financing, SBA 7(a) and 504 loans, and owner-user products. ~180 employees across Irvine, Dallas, and Atlanta. ~$2.4B in annual originations. AWS-primary tech stack with a custom loan origination system and secondary GCP analytics environment. Handles borrower PII, financial data, and property information subject to GLBA and FTC Safeguards Rule.

[Full company profile →](./01_company_profile.md) · [Operational context →](./01b_operational_context.md)

---

## Scope

**In scope:**
- All six NIST CSF 2.0 functions: Govern, Identify, Protect, Detect, Respond, Recover (106 subcategories)
- Corporate IT, loan origination system, customer-facing portal
- Cloud infrastructure (AWS primary, GCP secondary)
- Third-party integrations (Salesforce, Plaid, credit bureaus, DocuSign)
- All US offices

**Out of scope:**
- Physical security of branch offices (covered by separate facilities review)
- Borrower-side security posture
- Acquisition targets currently in due diligence

---

## Methodology

Each subcategory scored on a **1–4 implementation tier scale** with documented evidence and rationale. Scores are based on the MBC operational profile, known open issues, and realistic control gaps for a fintech lender of this size and regulatory profile.

| Tier | Name | Description |
|------|------|-------------|
| 1 | Partial | Ad hoc, reactive, undocumented |
| 2 | Risk Informed | Aware; informal practices exist |
| 3 | Repeatable | Documented practices applied consistently |
| 4 | Adaptive | Continuously improving, threat-informed |

Findings are consolidated from gap subcategories, rated by severity (1–5) and effort (S/M/L/XL), and sequenced into a three-phase remediation roadmap based on regulatory exposure, control dependencies, and effort-to-impact ratio.

[Full methodology →](./02_methodology.md)

---

## Maturity results

| Function | Subcategories | Avg Current Tier | Avg Target Tier | Avg Gap |
|----------|--------------|-----------------|-----------------|---------|
| Govern   | 31 | 1.55 | 2.97 | 1.42 |
| Identify | 21 | 1.67 | 2.86 | 1.19 |
| Protect  | 22 | 1.82 | 3.23 | 1.41 |
| Detect   | 11 | 1.45 | 3.09 | 1.64 |
| Respond  | 12 | 1.69 | 3.15 | 1.46 |
| Recover  | 8  | 1.50 | 3.00 | 1.50 |
| **Overall** | **106** | **1.63** | **3.04** | **1.41** |

---

## Key findings

| ID | Finding | Function | Severity | Effort | Phase |
|----|---------|----------|----------|--------|-------|
| F-01 | Unencrypted FTP transmission to state regulator | Protect | 5 | S | 1 |
| F-02 | No quarterly access reviews or least-privilege enforcement | Protect | 5 | L | 1 |
| F-03 | IR plan untested, external retainer expired | Respond | 5 | M | 1 |
| F-04 | Production borrower data present in staging environment | Protect | 5 | M | 1 |
| F-05 | MFA not consistently enforced across all systems | Protect | 4 | M | 1 |
| F-06 | No real-time network monitoring or SIEM | Detect | 4 | XL | 2 |
| F-07 | No endpoint detection and response (EDR) deployed | Detect | 4 | M | 2 |
| F-08 | BCP untested and not reflecting current architecture | Recover | 4 | M | 2 |
| F-09 | No root cause analysis process or evidence handling standard | Respond | 3 | S | 2 |
| F-10 | No crisis communications plan for external incident disclosure | Recover | 3 | S | 3 |

[Full findings register →](./03_csf_scoring_workbook.xlsx) · [Scoring workbook →](./03_csf_scoring_workbook.xlsx)

---

## Remediation roadmap summary

| Phase | Timeline | Theme | Est. Cost |
|-------|----------|-------|-----------|
| Phase 1 — Immediate | Months 1–3 | Close active regulatory exposure; stabilize identity and IR controls | ~$143K |
| Phase 2 — Near-term | Months 3–6 | Deploy detective controls (SIEM, EDR); validate recovery capability | ~$195K |
| Phase 3 — Planned | Months 6–12 | Crisis communications, backup testing, threat intelligence | ~$35K |
| **Total** | **12 months** | | **~$373K** |

[Full remediation roadmap →](./05_remediation_roadmap.md)

---

## Deliverables

| File | Description |
|------|-------------|
| [📊 Scoring workbook (XLSX)](./03_csf_scoring_workbook.xlsx) | 52 subcategories scored with current tier, target tier, gap, and rationale. Includes findings register and dashboard tabs. |
| [🗺️ Remediation roadmap (MD)](./05_remediation_roadmap.md) | Phased 12-month roadmap with effort, cost estimates, and prioritization rationale. |
| [📄 Executive summary (PDF)](./06_MBC_Executive_Summary.pdf) | 2-page board-ready summary: maturity scorecard, top 5 findings, roadmap at a glance, business risk rationale. |

---

## About the author

**James Bui** — Security+ certified GRC practitioner in training, transitioning from commercial real estate lending (Cornerstone Lending Group, ~$150MM deal volume) to cybersecurity Governance, Risk, and Compliance. Background spans commercial lending, SBA underwriting, and full-stack software engineering. Targeting GRC Analyst roles in fintech and financial services for late summer / early fall 2026.

[LinkedIn](https://www.linkedin.com/in/jamesminhbui/) · [GitHub](https://github.com/jamesmdang-bui)

---

*This is a fictional assessment for portfolio purposes. Meridian Bridge Capital is not a real company. All findings, vulnerabilities, and remediation steps are illustrative.*
