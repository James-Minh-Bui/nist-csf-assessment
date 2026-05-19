# Meridian Bridge Capital — Company Profile

## At a glance

| | |
|---|---|
| **Name** | Meridian Bridge Capital (MBC) |
| **Tagline** | "Commercial bridge financing for the middle market." |
| **Founded** | 2017 |
| **Headquarters** | Irvine, California |
| **Other offices** | Dallas, TX · Atlanta, GA |
| **Employees** | 210 (FTE) |
| **2025 originations** | $2.4B |
| **Customer base** | ~3,400 active borrowers, primarily real estate investors and small business owners |
| **Funding** | Series C, $180M raised to date; majority institutional backing |

## Business model

MBC is a non-bank lender that originates and services commercial real estate debt with a technology-forward operating model. The platform combines a custom loan origination system (LOS) with traditional human underwriting for a faster-than-bank closing experience targeted at sophisticated real estate investors.

### Product lines

- **Bridge loans** — short-term (6-36 month) financing on commercial properties, typically $1M-$25M
- **Multifamily acquisition loans** — non-recourse permanent financing for 5+ unit apartment buildings
- **SBA 7(a) and 504 loans** — owner-occupied commercial real estate
- **Owner-user financing** — investor-borrower hybrid products for small business operators

## Customers and data

MBC handles a sensitive data mix. Per customer, the LOS typically stores:

- Borrower personal data: SSN, date of birth, driver's license, addresses, phone, email
- Financial data: bank statements (90 days), tax returns (2-3 years), schedule of real estate owned, personal financial statements, credit reports (soft and hard pulls)
- Property data: addresses, valuations, rent rolls, environmental reports
- Loan data: terms, payment history, communications, closing documents
- Employment and business verification

## Technology stack

| Layer | Systems |
|---|---|
| **Cloud (primary)** | AWS — EC2, S3, RDS (Postgres), Lambda, API Gateway, CloudFront, IAM, KMS |
| **Cloud (secondary)** | GCP — BigQuery for analytics |
| **Core LOS** | Custom-built (Python/Django backend, React frontend, hosted on AWS) |
| **CRM** | Salesforce Financial Services Cloud |
| **Productivity** | Microsoft 365 (Email, SharePoint, Teams), Slack, Zoom |
| **Document handling** | DocuSign, custom S3-backed document vault |
| **Third-party integrations** | Plaid (bank verification), Equifax/Experian/TransUnion (credit), CoreLogic (property data), Black Knight (servicing) |
| **Endpoint** | CrowdStrike Falcon EDR, Microsoft Intune (MDM), Jamf (Mac fleet) |
| **Identity** | Okta SSO (most apps), Azure AD (Microsoft 365), local accounts for legacy systems |
| **Security tooling** | AWS Security Hub, GuardDuty, Cloudflare WAF, KnowBe4 (awareness training) |

## Regulatory environment

Because MBC is a non-bank lender that handles sensitive consumer and small-business data, several regulatory frameworks apply:

- **Gramm-Leach-Bliley Act (GLBA)** — Safeguards Rule applies to all customer NPI
- **FTC Safeguards Rule** (2023 amendment) — written information security program, designated qualified individual, risk assessment, access controls, encryption, MFA, monitoring, training
- **Fair Credit Reporting Act (FCRA)** — for credit pulls and dispute handling
- **Bank Secrecy Act / Anti-Money Laundering (BSA/AML)** — though MBC is not a depository institution, certain reporting and customer identification obligations apply
- **State lending licenses** — California Finance Lenders License (CFL), Texas Regulated Loan License, Georgia Residential Mortgage License, plus 18 other state-level licenses
- **CCPA / CPRA** — for California borrowers (most of MBC's portfolio)
- **TILA / RESPA / TRID** — for owner-user / consumer-purpose loan products
- **NMLS** — National Mortgage Licensing System for mortgage loan originators

## Current security and compliance state

MBC has a small but growing security and compliance function. This realistic snapshot drives most of the assessment findings.

### Organization
- 2-person internal security team (Director of Information Security + 1 Security Engineer)
- No dedicated CISO — Director reports to CTO
- Compliance function (3 people) reports to Chief Compliance Officer in Legal
- No formal cybersecurity steering committee or governance forum

### Recent work
- **SOC 2 Type I report** completed Q4 2024 (Security, Availability, Confidentiality)
- Working toward **SOC 2 Type II** with Q3 2026 target
- **FTC Safeguards Rule** compliance project ongoing — designated QI named, written ISP drafted but not yet board-approved
- **GLBA assessment** completed mid-2025 by external advisor

### Known gaps (driving the assessment)
- No formal enterprise risk register
- Vendor risk management is ad hoc; no tiering or recurring re-assessment
- Privileged access reviews performed informally, not on documented cadence
- No tabletop exercises run in the past 12 months
- Incident response plan exists but has not been tested
- Backup recovery testing performed annually but not formally documented
- Some legacy applications (servicing portal) authenticated with local accounts, not SSO
- Threat intelligence consumed informally; no formal CTI program
- Supply chain risk management not addressed as a formal program

### Business pressure points
- Series D fundraise targeted for late 2026 — investors will scrutinize security posture
- Top-5 institutional capital partner requesting SOC 2 Type II report
- Two state regulators have requested information security documentation in the last 18 months
- Recent industry breaches in fintech lending raising board attention
- Growth from 140 to 210 employees in 18 months has stressed onboarding and access provisioning
