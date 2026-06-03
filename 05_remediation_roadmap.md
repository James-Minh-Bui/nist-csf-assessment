# Remediation Roadmap — Meridian Bridge Capital
## NIST CSF 2.0 Maturity Assessment

> **Scope:** Protect → Recover functions (52 subcategories, 10 findings)
> **Assessment date:** May–June 2026
> **Roadmap horizon:** 12 months

---

## Prioritization methodology

Findings are sequenced across three phases based on four factors:

1. **Regulatory / legal exposure** — findings tied to active FTC Safeguards Rule, GLBA, or state breach notification requirements are Phase 1 regardless of effort.
2. **Active open issues** — items already documented in MBC's known issues log are treated as Phase 1; they represent acknowledged risk with no current remediation timeline.
3. **Severity × Effort** — high-severity, low-effort findings are pulled into earlier phases; high-severity, high-effort findings begin Phase 1 but complete in Phase 2.
4. **Control dependencies** — foundational controls (identity management, network monitoring) are sequenced before dependent controls (threat correlation, behavioral analytics).

**Effort definitions:** S = under 1 person-week · M = 1–4 person-weeks · L = 1–3 months · XL = 3+ months

**Budget methodology:** Blended internal labor at $200/hr (~160 hrs/person-month). External consulting (DFIR retainer, SIEM implementation support) at $300/hr where applicable.

---

## Phase 1 — Immediate (0–3 months)

**Theme: Close active regulatory exposure and stabilize foundational identity and IR controls.**

MBC has five findings that represent either active regulatory violations or foundational control failures that directly enable other risks. The unencrypted FTP channel to the state regulator is a live compliance violation that must be resolved before any examination or breach event. Access review and MFA gaps are the primary attack surface for credential-based intrusions — the leading threat vector for fintech lenders. The IR plan and retainer situation means MBC currently cannot respond effectively to a breach, which is untenable given borrower PII obligations under GLBA. Production data in staging is both a regulatory exposure and an active data governance failure. These five items are non-negotiable Phase 1 regardless of effort.

| Finding | Title | Severity | Effort | Est. Cost | Owner | Target |
|---------|-------|----------|--------|-----------|-------|--------|
| F-01 | Unencrypted FTP to State Regulator | 5 | S | ~$8K internal | IT / Security | Month 1 |
| F-04 | Production Data in Staging Environment | 5 | M | ~$20K internal | Engineering / Security | Month 2 |
| F-03 | IR Plan Untested, Retainer Expired | 5 | M | ~$40K (retainer + tabletop) | Security / Legal | Month 2 |
| F-05 | MFA Not Consistently Enforced | 4 | M | ~$25K internal | IT / Security | Month 3 |
| F-02 | No Quarterly Access Reviews | 5 | L | ~$50K internal | IT / HR | Month 3 |

**Phase 1 estimated cost: ~$143K**

**Key milestones:**
- Month 1: FTP channel replaced with SFTP/HTTPS. Legal notified to assess disclosure obligation.
- Month 2: Production data purged from staging. Data masking controls implemented. IR retainer signed. Tabletop exercise scheduled.
- Month 3: MFA enforced on all internet-facing systems and privileged access paths. First quarterly access review completed and exceptions remediated. Tabletop exercise conducted and IR plan updated.

---

## Phase 2 — Near-term (3–6 months)

**Theme: Build the detective control layer and validate recovery capability.**

Phase 1 closes the most urgent gaps but leaves MBC without meaningful detection capability. Phase 2 addresses this directly: SIEM deployment and EDR rollout are the two highest-leverage investments MBC can make, as they underpin incident detection, investigation, and response for all future incidents. The BCP update is sequenced here because it depends on the IR plan updates completed in Phase 1. Root cause analysis process and evidence handling are lower effort and can be completed alongside the larger initiatives.

| Finding | Title | Severity | Effort | Est. Cost | Owner | Target |
|---------|-------|----------|--------|-----------|-------|--------|
| F-06 | No SIEM or Real-Time Network Monitoring | 4 | XL | ~$120K (tooling + impl.) | Security | Month 5 |
| F-07 | No EDR Deployed | 4 | M | ~$35K (licensing + config) | Security / IT | Month 5 |
| F-08 | BCP Untested, Stale Architecture | 4 | M | ~$30K internal | Security / IT / Ops | Month 6 |
| F-09 | No RCA Process or Evidence Handling Standard | 3 | S | ~$10K internal | Security / Legal | Month 4 |

**Phase 2 estimated cost: ~$195K**

**Key milestones:**
- Month 4: RCA methodology defined and trained. Evidence handling procedure documented. SIEM vendor selected and deployment scoped.
- Month 5: SIEM live with baseline log ingestion (CloudTrail, VPC flow logs, identity logs). EDR deployed across all endpoints. Top 10 detection rules tuned.
- Month 6: BCP updated to reflect current architecture. Full BCP test conducted with documented results. Annual BCP review cycle established.

---

## Phase 3 — Planned (6–12 months)

**Theme: Mature communications, resilience verification, and threat intelligence integration.**

Phase 3 items address important but lower-urgency gaps that build on the foundations established in Phases 1 and 2. Crisis communications planning is only effective once the IR plan is tested and stable (Phase 1 dependency). Backup restoration testing is more meaningful once the BCP is updated (Phase 2 dependency). Threat intelligence integration delivers the most value once the SIEM is operational and able to consume indicators (Phase 2 dependency).

| Finding | Title | Severity | Effort | Est. Cost | Owner | Target |
|---------|-------|----------|--------|-----------|-------|--------|
| F-10 | No Crisis Communications Plan | 3 | S | ~$12K (legal + comms time) | Legal / Comms / Security | Month 8 |
| — | Backup Restoration Testing Program | 3 | S | ~$8K internal | IT / Security | Month 9 |
| — | Threat Intelligence Feed + FS-ISAC | 3 | S | ~$15K/yr (licensing + analyst time) | Security | Month 10 |

**Phase 3 estimated cost: ~$35K**

**Key milestones:**
- Month 8: Crisis communications plan completed and pre-approved templates reviewed by legal.
- Month 9: Quarterly backup restoration test schedule defined. First test completed with documented results.
- Month 10: FS-ISAC membership active. At least one commercial threat intel feed integrated into SIEM detection rules.

---

## Summary

| Phase | Findings | Timeline | Estimated Cost |
|-------|----------|----------|----------------|
| Phase 1 — Immediate | F-01, F-02, F-03, F-04, F-05 | Months 1–3 | ~$143K |
| Phase 2 — Near-term | F-06, F-07, F-08, F-09 | Months 3–6 | ~$195K |
| Phase 3 — Planned | F-10 + 2 supporting items | Months 6–12 | ~$35K |
| **Total** | **10 findings** | **12 months** | **~$373K** |

> **Note:** Cost estimates reflect internal labor and third-party tooling/consulting at blended rates. Actual costs will vary based on vendor selection, existing tooling, and internal resource availability. SIEM and EDR estimates assume a mid-market vendor (e.g., Elastic Security, Microsoft Sentinel, or CrowdStrike Falcon) and do not include multi-year licensing discounts.

---

## Interview talking points

*Common question: "Walk me through how you prioritized these findings."*

The sequencing logic has three layers. First, anything with an active regulatory hook goes to Phase 1 unconditionally — the FTP channel and the production-data-in-staging issue are live compliance violations, not hypothetical risks. Second, foundational controls that other controls depend on get sequenced before their dependents — identity management and IR capability before detection tooling, detection tooling before behavioral analytics. Third, effort-to-impact ratio drives tie-breaking within phases — the RCA process (Effort S, high leverage) gets done in Month 4 before SIEM deployment (Effort XL) completes, because it can be. The $373K total is also defensible to a CFO: the cost of a single GLBA enforcement action or notifiable breach at MBC's loan volume would dwarf this remediation spend.

---

*Remediation roadmap v1.0 — June 2026*
*Assessment performed by: James Bui*
*Framework: NIST Cybersecurity Framework 2.0 (published Feb 26, 2024)*
