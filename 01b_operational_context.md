# Meridian Bridge Capital — Operational Context Addendum

> Supplements the main company profile (`01_company_profile.md`) with operational detail across the six CSF functions. Where the profile describes the business, this document describes how the security program actually runs day-to-day. Use this as the ground truth when scoring subcategories.

---

## Governance and risk management

**Leadership and structure.** Director of Information Security (Sarah Chen, hired 18 months ago from a regional bank) reports to the CTO (David Park). One Security Engineer (Marcus Rivera) reports to Sarah. No CISO role exists. Compliance team of three (one Director, two analysts) reports to the Chief Compliance Officer in Legal. Director of InfoSec attends the monthly Executive Leadership Team meeting but cybersecurity is not a standing agenda item — it surfaces ad hoc when something is pressing. No formal cybersecurity steering committee or risk committee exists. The Board has an Audit Committee that reviews compliance topics quarterly; cybersecurity is covered once a year unless an incident warrants more.

**Risk management practice.** No formal enterprise risk register. The Compliance team maintains a "regulatory compliance tracker" in Smartsheet that tracks state license renewals, regulatory exams, and Safeguards Rule action items. Security risks are tracked informally in a Notion page maintained by the Director of InfoSec — about 30 items, last updated 6 weeks ago, no formal severity scoring. Risk appetite is undocumented. When prioritization decisions come up, they're made in conversations between the CTO and Director of InfoSec.

**Policies.** The following policies exist as Google Docs in the Security shared drive:
- Information Security Policy (drafted 2024, board-approved 2024)
- Acceptable Use Policy (last reviewed 2023, no GenAI language)
- Access Control Policy (drafted as part of SOC 2 Type I work, approved 2024)
- Incident Response Plan (approved 2024, untested)
- Vendor Management Policy (drafted but not approved; sits with Legal for review)

No formal policy review cadence exists. Policies are updated reactively when an audit calls them out.

**Supply chain risk management.** No formal C-SCRM program. Legal performs ad hoc vendor diligence during contracting — usually a security questionnaire is requested for vendors that will handle PII, but completion is inconsistent. No vendor inventory exists in any central system; vendors are tracked in finance (Bill.com), legal (a Google Sheet), and procurement (DocuSign CLM) without a master view. No vendor tiering by criticality. No recurring re-assessment cycle.

---

## Identify (assets, risk assessment, improvement)

**Hardware inventory.** Endpoints managed via Microsoft Intune (Windows) and Jamf (Mac). Combined fleet of ~220 devices auto-discovered and inventoried. Servers and infrastructure are AWS-only — no on-prem servers — and discovered via AWS Config + Resource Explorer. Inventory is reliable for AWS and the laptop fleet; unreliable for "shadow IT" like personal devices that connect to SaaS apps.

**Software inventory.** Less mature. SaaS applications are tracked in Okta (~80 apps integrated), but not all SaaS is behind SSO. Some teams use unsanctioned tools (Marketing uses several SaaS products that aren't in Okta). No formal software asset management tool. The Security Engineer maintains a spreadsheet of approved SaaS apps, updated quarterly.

**Data inventory.** A data classification project completed in 2024 identified four data classes (Public, Internal, Confidential, Restricted). The classification matrix exists as a Google Doc. Specific data assets (the LOS database, the document vault, Salesforce data, BigQuery analytics warehouse) are tagged in AWS using cost-allocation tags, but a formal data inventory mapping data types to locations doesn't exist. Borrower PII clearly flows through the LOS, document vault, Salesforce, and several integrations — this is documented at a high level in the SOC 2 Type I scoping but not maintained as a living inventory.

**Network diagrams.** Architecture diagrams exist in Lucidchart, last updated approximately 6 months ago. Reasonably accurate for production but doesn't reflect three recent SaaS integrations (a new analytics tool, a new marketing automation platform, a new e-signature backup vendor). Data flow diagrams exist for the loan origination flow specifically (SOC 2 evidence) but not for other workflows.

**Vulnerability management.** Tenable Nessus deployed for infrastructure scanning, runs monthly across AWS environments. Web application scanning via Tenable Web App Scanning, runs monthly on the borrower portal and admin portal. AWS Inspector enabled for EC2 and ECR. Endpoint vulnerabilities tracked via CrowdStrike Falcon Spotlight. Findings are reviewed by the Security Engineer; no formal SLA exists for remediation but critical findings typically patched within 2-3 weeks. No vulnerability disclosure program (no public security.txt, no bug bounty).

**Threat intelligence.** Informal. The Director of InfoSec subscribes to a few industry newsletters (SANS NewsBites, Risky Business, KrebsOnSecurity), monitors fintech-specific Slack communities, and gets feeds from CrowdStrike and AWS GuardDuty. No structured threat intel program, no commercial threat intel feed, no formal threat modeling exercises.

**Improvement processes.** Lessons learned from incidents are captured ad hoc in Notion. No post-incident review template exists. Tabletop exercises haven't been run in 12+ months. Internal security tests haven't been performed; the most recent penetration test was a vendor-conducted external test as part of SOC 2 Type I prep in late 2024.

---

## Protect (identity, training, data security, platform security, infrastructure)

**Identity and access management.** Okta SSO covers ~80 SaaS apps including all SOC 2 in-scope systems. Azure AD handles Microsoft 365 (federated with Okta). AWS access uses AWS IAM Identity Center (formerly SSO) federated with Okta. MFA enforced via Okta Verify push or hardware key for all SSO-protected apps; AWS console access requires MFA. **Gaps:** legacy servicing portal uses local accounts with password-only auth (no MFA); some database direct access uses static credentials managed in AWS Secrets Manager but not rotated on a schedule; service accounts in the LOS are not centrally tracked. Access provisioning is largely manual — a JIRA ticket triggers Okta group assignment by IT.

**Access reviews.** Annual review performed for SOC 2 Type I scope in late 2024. No quarterly cadence. No automated entitlement reporting. Privileged AWS access (Administrator, PowerUser) granted to 8 individuals; reviewed once during SOC 2 prep, not since.

**Awareness and training.** KnowBe4 deployed. Annual mandatory security training assigned to all employees, completion rate ~94%. Monthly phishing simulations run by the Security Engineer — most recent phish-prone rate was 11% (industry average ~5%). No specialized training for developers, finance team (high BEC target), or executives.

**Data protection at rest.** AWS resources encrypted using AWS-managed KMS keys by default. RDS, S3, EBS all encrypted at rest. Customer-managed KMS keys used for the document vault S3 bucket and the LOS database. Endpoint encryption via BitLocker (Windows) and FileVault (Mac), enforced through Intune/Jamf policies. Mobile devices (BYOD program for ~40 people) require device encryption and PIN via Intune MDM.

**Data protection in transit.** TLS 1.2+ enforced on all customer-facing endpoints via Cloudflare. Internal AWS traffic uses VPC private endpoints where supported. Email uses Microsoft 365 with TLS enforced. SFTP for batch file transfers to credit bureaus (Equifax, Experian, TransUnion). One legacy integration with a state regulator still uses unencrypted FTP for monthly reporting — known issue, on the remediation backlog for 6 months.

**Data in use.** Limited specific controls. No DLP solution deployed beyond Microsoft 365 native DLP rules (basic — SSN and credit card patterns flagged). No production data masking in non-prod environments — full prod data clones used in staging, which is a known SOC 2 finding.

**Backups.** RDS automated backups with 35-day retention. Document vault S3 versioning enabled with replication to a secondary region. Salesforce data exported weekly to S3 via OwnBackup. **Backup restoration tested annually** as part of DR exercise, last test February 2026 — restore worked but full procedure not documented step-by-step. Backup integrity verification automatic via AWS Backup; no separate integrity validation process.

**Configuration management.** AWS infrastructure mostly managed via Terraform (~80% IaC coverage; some manual configurations remain especially for early-stage projects). CIS Benchmarks not formally adopted; AWS Security Hub enabled with AWS Foundational Security Best Practices and PCI-DSS standards (since the document vault touches some payment data via SBA loan disbursements). Endpoint baselines enforced via Intune and Jamf using a custom baseline derived loosely from CIS Level 1.

**Patching and software maintenance.** Endpoint OS patching automatic via Intune/Jamf with a 14-day delay for staged rollout. Server patching (the few EC2 instances still in use) handled via AWS Systems Manager Patch Manager, monthly schedule. Application dependencies (Python packages, npm) scanned via GitHub Dependabot; alerts reviewed during sprint planning but no formal SLA. The LOS gets feature releases every 2 weeks; security patches expedited to weekly when needed.

**Logging.** AWS CloudTrail enabled across all accounts (org-level trail to a central log archive S3 bucket). VPC Flow Logs enabled for production VPCs. Application logs from the LOS shipped to Datadog. Okta logs streamed to Datadog. CrowdStrike telemetry retained in Falcon Insight (90-day retention). **Gaps:** no SIEM correlation across all sources (Datadog used as log aggregator, not SIEM); some SaaS apps don't ship logs anywhere; log retention beyond 1 year is inconsistent.

**Unauthorized software prevention.** CrowdStrike Falcon has application control policies for endpoints. AWS uses SCPs (Service Control Policies) to restrict regions and risky services at the organization level. Developers can install dev tools without approval; sales/marketing teams can install SaaS apps without security review (known gap).

**Secure development.** The LOS team (12 engineers) uses GitHub Enterprise. Branch protection on main, required code review, required CI checks. SAST via GitHub Advanced Security (CodeQL). Dependency scanning via Dependabot. No SCA beyond Dependabot. No DAST. No formal threat modeling. Security training for developers is annual general KnowBe4 only; no role-specific secure coding training.

**Network protection.** Cloudflare in front of public web properties (WAF, DDoS, bot management). AWS WAF on the borrower portal. VPC segmentation between production, staging, and corporate. AWS Network Firewall in production VPC. No internal microsegmentation between LOS tiers. No formal network access control (NAC) for office networks.

**Environmental and physical resilience.** AWS multi-AZ for production databases and critical compute. Multi-region backup for the document vault. Office facilities (Irvine, Dallas, Atlanta) leased in commercial buildings with building-managed access control (card readers, security desk). No company-managed physical security beyond office front-door badging. No company-owned data centers.

**Capacity management.** AWS Auto Scaling configured for the borrower portal and LOS API. Capacity reviewed during quarterly engineering reviews. No formal capacity model; scaling decisions are reactive based on monitoring alerts.

---

## Detect (continuous monitoring, adverse event analysis)

**Network monitoring.** AWS GuardDuty enabled in all production accounts. VPC Flow Logs analyzed by Datadog with custom dashboards for anomalous traffic. Cloudflare logs reviewed informally by the Security Engineer during weekly check-ins. No 24/7 SOC; alerts queue overnight and weekends.

**Endpoint monitoring.** CrowdStrike Falcon EDR on all managed devices (Windows, Mac). Real-time detection with alerts to the Security Engineer's phone for high-severity events. Falcon Insight provides threat hunting capability but no scheduled hunts performed.

**User activity monitoring.** Okta logs all authentication events. Datadog has dashboards for anomalous login patterns. No formal UEBA solution. No data access monitoring on the LOS database beyond CloudTrail for AWS-level events.

**Physical monitoring.** Office security is building-managed; MBC doesn't run its own physical monitoring. Some office spaces have basic CCTV at suite entrances (building-provided footage retained 30 days).

**External service monitoring.** AWS Health and Service Health Dashboard monitored via Datadog. Status pages for Okta, Salesforce, Plaid, credit bureau APIs monitored manually. No formal third-party SLA tracking.

**Runtime monitoring.** AWS Security Hub aggregates findings from GuardDuty, Inspector, Config, and Macie. CrowdStrike Falcon for endpoints. No container runtime security tooling despite some workloads moving to ECS. Datadog APM for application performance; not formally a security monitoring tool but used for anomaly detection.

**Adverse event analysis.** When alerts fire, the Security Engineer triages first. Multi-source correlation is manual — log into Datadog, GuardDuty, CrowdStrike, Okta, look for patterns. No SOAR platform. No formal playbooks for common alert types. Threat intel context applied informally based on Director of InfoSec's reading.

**Impact and scope assessment.** Documented during incident response only. No formal pre-incident impact modeling. Incident scope determined ad hoc by interviewing system owners.

**Event communication.** Critical alerts go to the Security Engineer via PagerDuty. Director of InfoSec gets a daily digest email. Adverse event info shared with leadership only when it becomes an incident.

**Incident declaration criteria.** Defined in the Incident Response Plan: any event meeting specific severity, customer impact, or data confidentiality thresholds escalates to "declared incident." Criteria are documented but not always consistently applied — in practice, the Director of InfoSec makes the call.

---

## Respond (incident management, analysis, communication, mitigation)

**IR plan.** Incident Response Plan exists, board-approved 2024. Defines roles (Incident Commander, Technical Lead, Communications Lead, Legal Liaison), escalation paths, severity levels (Sev1-4), and basic playbooks for: data exfiltration, credential compromise, ransomware, third-party breach notification received. **Plan has not been tested via tabletop exercise in 12+ months.** Plan references "the third-party IR retainer" (Mandiant) but the retainer agreement is currently expired — known issue.

**Triage and validation.** First-pass triage by the Security Engineer. Validation typically involves checking multiple log sources and confirming with affected system owners. No formal triage SLA.

**Categorization and prioritization.** Sev1-4 scale defined; in practice, most events get classified Sev2 or Sev3 and there's some judgment drift.

**Escalation.** Sev1 escalates to CTO immediately, then to CEO and Legal within an hour. Sev2 goes to Director of InfoSec and CTO within 4 hours. Sev3/4 batched into weekly review.

**Recovery initiation criteria.** Documented in the IR plan — recovery starts when containment is confirmed and forensic evidence is preserved.

**Analysis and forensics.** Security Engineer handles initial forensics. For anything beyond scope, the (currently expired) Mandiant retainer would be activated. Evidence preservation procedures documented in IR plan but not regularly practiced. CrowdStrike Real Time Response used for endpoint investigation; AWS CloudTrail and Detective used for cloud investigation.

**Investigation documentation.** Incidents documented in a Notion incident log. Investigation actions captured in Jira tickets associated with the incident. Chain of custody procedures defined but not consistently followed.

**Magnitude estimation.** Done case-by-case during incident response. No formal impact estimation framework.

**Stakeholder notification.** IR plan defines internal notification matrix (CTO, CEO, Legal, Compliance, affected business owners). External notification (regulators, affected customers, capital partners) handled by Legal and Compliance per applicable regulation (state breach laws, GLBA, FTC Safeguards notification requirements). Notification templates exist for common scenarios.

**Information sharing.** Incident information shared internally via Slack incident channel (auto-created by PagerDuty). Customer-facing communication routes through Customer Success and Legal. No formal information-sharing agreements with industry ISACs.

**Containment and eradication.** Playbooks define containment steps for common scenarios (isolate endpoint via CrowdStrike, disable Okta user, rotate AWS credentials, take application offline). Eradication procedures less documented — typically figured out during the incident.

---

## Recover (recovery execution, communication)

**Recovery plan execution.** Recovery portion of the IR plan defines roles and high-level steps. Disaster Recovery procedures exist as a separate document for major outage scenarios (loss of AWS region, complete LOS outage). DR plan tested annually — most recent test February 2026 — and the test exercised recovery of the LOS to a secondary region. Test was partially successful (recovery completed in 6 hours against a 4-hour RTO target; identified several documentation gaps that have not yet been remediated).

**Recovery action selection.** Recovery priorities defined in DR plan: borrower portal, LOS API, internal admin tools, analytics — in that order. Selection happens during the incident.

**Backup integrity verification.** Backups are auto-validated by AWS Backup. Before restoration during the February 2026 DR test, the team verified backup checksums but did not perform a full integrity test (e.g., restore to isolated environment and validate data correctness).

**Critical mission alignment.** Recovery prioritization reflects business criticality (revenue-generating systems first). Documented in the DR plan with input from the business.

**Restoration verification.** Post-restore verification includes smoke tests on critical user flows, but no formal acceptance criteria for declaring restoration complete.

**Recovery completion.** Declared by the Incident Commander based on criteria in the IR plan: systems operational, monitoring confirms normal patterns, business sign-off received.

**Recovery communication.** Internal updates via incident Slack channel and stakeholder briefings. Customer-facing updates published to status.meridianbridge.example (status page). Capital partner notifications handled directly by the CFO for material incidents. Public statements drafted by Comms in conjunction with Legal.

**Public updates methodology.** Status page used for service updates. Press statements drafted only for material incidents (none in past 24 months). Templates exist in the IR plan for common scenarios.

---

## Cross-cutting context

**SOC 2 Type I scope.** The Type I report covered the LOS, borrower portal, document vault, and supporting AWS infrastructure. Trust Services Criteria included: Security, Availability, Confidentiality. Type II is in progress targeting Q3 2026 with the same scope.

**Audit history.** SOC 2 Type I (2024), external pen test (late 2024, 4 findings, 3 remediated), GLBA advisory assessment (mid-2025, 12 findings, 7 remediated), FTC Safeguards readiness review (ongoing internal). No recent regulatory examination by state lending regulators.

**Open known issues (the unprioritized backlog).** Unencrypted FTP to state regulator; production data in staging; expired Mandiant retainer; legacy servicing portal local accounts; no formal C-SCRM program; no quarterly access reviews; tabletop exercises overdue; vendor management policy unapproved; AUP needs GenAI update; CSPM coverage gaps in the analytics GCP environment.

**Recent organizational changes.** Headcount grew from 140 to 210 in the past 18 months. Two new offices opened. A Series D fundraise is targeted for late 2026 — investors will scrutinize security posture during diligence.

---

*Operational addendum v1.0 — supplements `01_company_profile.md`. Use both documents together when scoring CSF subcategories.*
