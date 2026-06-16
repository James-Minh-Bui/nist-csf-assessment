# Findings Register — Meridian Bridge Capital
## NIST CSF 2.0 Maturity Assessment

> **Assessment date:** May–June 2026 · **Framework:** NIST CSF 2.0 · **Assessor:** James Bui
> **Scope:** All six CSF functions, 106 subcategories · **Findings:** 10 priority gaps

---

## Summary

| Phase | Findings | Theme |
|-------|----------|-------|
| Phase 1 — Immediate (0–3 months) | F-01, F-02, F-03, F-04, F-05 | Active regulatory exposure; identity and IR control failures |
| Phase 2 — Near-term (3–6 months) | F-06, F-07, F-08, F-09 | Detective controls; recovery validation |
| Phase 3 — Planned (6–12 months) | F-10 | Communications and disclosure readiness |

**Severity scale:** 5 = Critical · 4 = High · 3 = Medium · 2 = Low · 1 = Informational
**Effort scale:** S = <1 week · M = 1–4 weeks · L = 1–3 months · XL = 3+ months

---

## Phase 1 — Immediate (Months 1–3)

---

### F-01 · Unencrypted FTP Transmission to State Regulator

| Field | Detail |
|-------|--------|
| **Function** | Protect |
| **Subcategory** | PR.DS-02 |
| **Severity** | 5 — Critical |
| **Effort** | S |
| **Priority** | High |
| **Owner** | IT / Security |
| **Status** | Open |

**Current state**
An active FTP channel transmits borrower data to a state regulator without encryption. No compensating controls are in place and the issue is documented as an open known issue.

**Risk**
Direct violation of FTC Safeguards Rule and GLBA data-in-transit requirements. Regulatory examination or breach could trigger enforcement action and reputational damage.

**Recommendation**
Replace FTP immediately with SFTP or HTTPS-based file transfer. Enforce a transport encryption policy for all external data transmission. Notify legal to assess regulatory disclosure obligation.

---

### F-02 · No Quarterly Access Reviews or Least-Privilege Enforcement

| Field | Detail |
|-------|--------|
| **Function** | Protect |
| **Subcategory** | PR.AA-05 |
| **Severity** | 5 — Critical |
| **Effort** | L |
| **Priority** | High |
| **Owner** | IT / HR |
| **Status** | Open |

**Current state**
Access entitlements have not been recertified on a quarterly basis. Role definitions have not been updated to reflect 50% headcount growth over 18 months, resulting in widespread overprivileged accounts.

**Risk**
Overprivileged accounts create insider threat risk and lateral movement paths for attackers. This is a near-certain finding in a SOC 2 Type II audit and a GLBA examination.

**Recommendation**
Implement quarterly access review process using structured manual or IAM tooling. Define RBAC profiles for all job functions. Remediate exceptions from the first review cycle within 30 days.

---

### F-03 · IR Plan Untested and External Retainer Expired

| Field | Detail |
|-------|--------|
| **Function** | Respond |
| **Subcategory** | RS.MA-01 |
| **Severity** | 5 — Critical |
| **Effort** | M |
| **Priority** | High |
| **Owner** | Security / Legal |
| **Status** | Open |

**Current state**
Tabletop exercises are overdue per the open known issues log and the Mandiant IR retainer has expired. The IR plan has not been validated against current AWS architecture or personnel changes.

**Risk**
An untested IR plan with no external support creates unacceptable breach response risk for a lender handling borrower PII. GLBA and state breach notification laws impose strict timelines.

**Recommendation**
Renew or replace the IR retainer with a qualified DFIR firm immediately. Conduct a tabletop exercise within 60 days covering ransomware and PII exfiltration scenarios. Update the IR plan to reflect current architecture and personnel.

---

### F-04 · Production Borrower Data Present in Staging Environment

| Field | Detail |
|-------|--------|
| **Function** | Protect |
| **Subcategory** | PR.DS-01 |
| **Severity** | 5 — Critical |
| **Effort** | M |
| **Priority** | High |
| **Owner** | Engineering / Security |
| **Status** | Open |

**Current state**
Production PII including borrower financial data has been identified in the staging environment. Staging access controls are materially less restrictive than production.

**Risk**
Unauthorized access to borrower PII in staging creates GLBA and FTC Safeguards Rule exposure. This is an active open issue with no documented remediation timeline.

**Recommendation**
Immediately purge production data from staging. Implement data masking or synthetic data generation for all non-production environments. Enforce a technical control preventing production data from being copied to lower environments.

---

### F-05 · MFA Not Consistently Enforced Across All Systems

| Field | Detail |
|-------|--------|
| **Function** | Protect |
| **Subcategories** | PR.AA-01, PR.AA-03 |
| **Severity** | 4 — High |
| **Effort** | M |
| **Priority** | High |
| **Owner** | IT / Security |
| **Status** | Open |

**Current state**
MFA is not enforced on all systems including legacy platforms and some internal applications. The legacy servicing portal maintains local accounts outside Active Directory with no MFA requirement.

**Risk**
Credential stuffing and account takeover are active attack vectors for fintech lenders. Inconsistent MFA enforcement leaves high-value systems exposed to credential-based intrusion.

**Recommendation**
Inventory all systems and their MFA coverage. Enforce MFA for all internet-facing systems and privileged access immediately. Develop a 90-day roadmap to extend MFA to remaining internal systems and migrate legacy portal accounts into the IdP.

---

## Phase 2 — Near-term (Months 3–6)

---

### F-06 · No Real-Time Network Monitoring or SIEM

| Field | Detail |
|-------|--------|
| **Function** | Detect |
| **Subcategories** | DE.CM-01, DE.AE-03 |
| **Severity** | 4 — High |
| **Effort** | XL |
| **Priority** | High |
| **Owner** | Security |
| **Status** | Open |

**Current state**
VPC flow logs are collected but no SIEM aggregates or analyzes them in real time. Log sources across network, endpoint, application, and identity are siloed with no cross-source correlation capability.

**Risk**
No real-time detection capability creates high adversarial dwell time. Multi-stage attacks spanning system boundaries cannot be detected or investigated. This gap undermines the effectiveness of all other detective controls.

**Recommendation**
Deploy a SIEM with ingestion of VPC flow logs, CloudTrail, and application logs as a baseline. Define detection rules for the top threat scenarios for fintech lenders. Establish alert SLAs and an on-call triage workflow.

---

### F-07 · No Endpoint Detection and Response (EDR) Deployed

| Field | Detail |
|-------|--------|
| **Function** | Detect |
| **Subcategory** | DE.CM-03 |
| **Severity** | 4 — High |
| **Effort** | M |
| **Priority** | High |
| **Owner** | Security / IT |
| **Status** | Open |

**Current state**
No EDR tooling is deployed on corporate endpoints or servers. Workstation and server activity is invisible to the security function, and no user behavior analytics exists to identify anomalous internal activity.

**Risk**
Insider threats and endpoint-based intrusions cannot be detected or investigated. EDR is a foundational control expected by SOC 2 auditors, cyber insurers, and institutional capital partners.

**Recommendation**
Deploy EDR across all corporate endpoints and servers. Configure baseline detection for credential theft, lateral movement, and persistence. Integrate EDR alerts into the incident triage workflow.

---

### F-08 · BCP Untested and Not Reflecting Current Architecture

| Field | Detail |
|-------|--------|
| **Function** | Recover |
| **Subcategories** | RC.RP-01, RC.RP-02 |
| **Severity** | 4 — High |
| **Effort** | M |
| **Priority** | Medium |
| **Owner** | Security / IT / Ops |
| **Status** | Open |

**Current state**
The BCP has not been tested in over 18 months and does not reflect the current AWS architecture, headcount growth, or system additions. RTO/RPO are defined for the LOS but not for the customer portal or secondary services.

**Risk**
An untested, stale BCP provides false assurance and will fail under real incident conditions. Incomplete recovery objectives mean restoration prioritization during an incident will be ad hoc.

**Recommendation**
Update the BCP to reflect current architecture and personnel. Conduct a full BCP test within 90 days with documented results. Define RTO/RPO for all critical systems and establish an annual review and test cycle.

---

### F-09 · No Root Cause Analysis Process or Post-Incident Review Standard

| Field | Detail |
|-------|--------|
| **Function** | Respond |
| **Subcategories** | RS.AN-03, RS.AN-06 |
| **Severity** | 3 — Medium |
| **Effort** | S |
| **Priority** | Medium |
| **Owner** | Security / Legal |
| **Status** | Open |

**Current state**
Post-incident reviews occur sporadically without a defined RCA methodology, required participants, or findings tracking. Analyst activity during investigations is captured informally in Slack with no chain-of-custody process.

**Risk**
Without systematic RCA, recurring control failures go unaddressed. Informal evidence handling is insufficient for regulatory inquiries, litigation, or cyber insurance claims.

**Recommendation**
Define a mandatory post-incident RCA process for all Severity 1 and 2 incidents with completion required within 14 days of closure. Establish an evidence handling procedure with tamper-evident logging and a case management tool.

---

## Phase 3 — Planned (Months 6–12)

---

### F-10 · No Crisis Communications Plan for External Incident Disclosure

| Field | Detail |
|-------|--------|
| **Function** | Recover |
| **Subcategories** | RC.CO-04, RS.CO-02 |
| **Severity** | 3 — Medium |
| **Effort** | S |
| **Priority** | Medium |
| **Owner** | Legal / Comms / Security |
| **Status** | Open |

**Current state**
No crisis communications plan exists and no pre-approved messaging templates have been developed for external or public disclosure. Stakeholder notification obligations are understood at a general level but no SLAs or contact lists are defined.

**Risk**
Drafting public statements during an active incident without prior legal approval increases regulatory and reputational risk. Undefined notification SLAs create GLBA and state breach notification law exposure.

**Recommendation**
Develop a crisis communications plan covering regulators, capital partners, and public channels. Create pre-approved templates for the top three incident scenarios reviewed by legal. Establish a defined approval workflow and notification SLAs.

---

## Additional observations

The following subcategories are not captured as standalone findings but represent notable gaps worth tracking as the program matures:

- **GV.RM-02 / GV.RM-03** — No documented risk appetite statement and no ERM process. These are foundational to a mature GRC program and will surface in a SOC 2 Type II audit.
- **GV.SC-01 through GV.SC-10** — No C-SCRM program. With 80+ vendors including high-risk integrations (Plaid, credit bureaus, Black Knight), this is a significant long-term gap.
- **ID.RA-03 / ID.RA-04 / ID.RA-05** — No formal threat modeling or risk assessment methodology. Prioritization of all other remediation work is weaker without this foundation.
- **PR.AT-02** — No role-based security training for developers, cloud ops, or finance personnel handling PII.

These items are candidates for a Phase 3 or Year 2 remediation plan as the Phase 1 and 2 work progresses.

---

*Findings register v1.0 — June 2026*
*Assessment performed by: James Bui*
*Framework: NIST Cybersecurity Framework 2.0 (published Feb 26, 2024)*
*This is a fictional assessment for portfolio purposes. Meridian Bridge Capital is not a real company.*
