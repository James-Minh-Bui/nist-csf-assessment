# NIST CSF 2.0 Maturity Assessment — Meridian Bridge Capital

> An end-to-end cybersecurity governance, risk, and compliance assessment performed against the **NIST Cybersecurity Framework 2.0**, for a fictional commercial real estate fintech lender.

## About this project

This is a self-directed portfolio assessment built to demonstrate practical GRC capability: framework fluency, evidence-based scoring, gap analysis, and remediation roadmapping. The subject organization is fictional, but the company profile, scope, and findings are designed to reflect realistic conditions at a ~200-employee fintech lender operating in a regulated environment.

The assessment evaluates current maturity across all six CSF 2.0 functions (Govern, Identify, Protect, Detect, Respond, Recover), identifies the highest-priority gaps, and produces a phased remediation roadmap with effort and impact estimates.

**Framework:** [NIST Cybersecurity Framework 2.0](https://www.nist.gov/cyberframework) (published February 2024)

## Subject organization

**Meridian Bridge Capital (MBC)** is a fictional commercial real estate lending platform offering bridge loans, multifamily acquisition financing, SBA 7(a) and 504 loans, and owner-user products. ~210 employees across Irvine, Dallas, and Atlanta. ~$2.4B in annual originations. AWS-primary tech stack with custom loan origination system. Handles borrower PII, financial data, and property information.

[Full company profile →](./01_company_profile.md)

## Scope

In scope:
- All six NIST CSF 2.0 functions and 106 subcategories
- Corporate IT, loan origination system, customer-facing portal
- Cloud infrastructure (AWS primary, GCP secondary)
- Third-party services (Salesforce, Plaid, credit bureaus, DocuSign)
- All US offices

Out of scope:
- Physical security of branch offices (covered by separate facilities review)
- Borrower-side security posture
- Acquisition targets currently in due diligence

## Methodology

Assessment performed against the NIST CSF 2.0 Core. Each of the 106 subcategories scored on a **1-4 implementation tier scale** with documented evidence:

| Tier | Name | Description |
|------|------|-------------|
| 1 | Partial | Ad hoc, reactive, undocumented |
| 2 | Risk Informed | Aware and informal practices exist |
| 3 | Repeatable | Documented practices applied consistently |
| 4 | Adaptive | Continuously improving, threat-informed |

Each finding is captured with severity (1-5), effort (S/M/L/XL), and a recommended remediation. Findings are then prioritized and grouped into a phased roadmap (0-3 months, 3-6 months, 6-12 months).

[Full methodology →](./02_methodology.md)

## Key findings (preview)

*Populated after scoring is complete in Week 3.*

| # | Finding | Function | Severity | Effort |
|---|---------|----------|----------|--------|
| F-01 | _[example]_ No formal cybersecurity supply chain risk management program | GV.SC | 4 | L |
| F-02 | _[example]_ Privileged access reviews performed ad hoc, not on a defined cadence | PR.AA | 4 | M |
| F-03 | _[example]_ No tabletop exercises performed in the last 12 months | RS.MA | 3 | S |

[Full findings register →](./04_findings_register.md)

## Deliverables

- [📊 Scoring workbook (XLSX)](./03_csf_scoring_workbook.xlsx) — all 106 subcategories with tier scores and evidence
- [📋 Findings register](./04_findings_register.md) — prioritized gaps with severity and effort
- [🗺️ Remediation roadmap](./05_remediation_roadmap.md) — phased remediation plan
- [📄 Executive summary (PDF)](./deliverables/executive_summary.pdf) *(Week 3)*
- [📑 Full assessment report (PDF)](./deliverables/full_assessment_report.pdf) *(Week 3)*
- [📈 Maturity dashboard (PNG)](./deliverables/maturity_dashboard.png) *(Week 3)*

## About the author

**James Bui** — Security+ certified, transitioning from commercial real estate lending to cybersecurity Governance, Risk, and Compliance. Currently building a portfolio of GRC artifacts targeting a GRC Analyst role for late summer / early fall 2026.

[LinkedIn](https://www.linkedin.com/in/your-profile) · [Portfolio site](https://your-portfolio.example)

---

*This is a fictional assessment for portfolio purposes. Meridian Bridge Capital is not a real company. All findings, vulnerabilities, and remediation steps are illustrative.*
