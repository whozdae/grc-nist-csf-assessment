# Cybersecurity Gap Assessment & Risk Report
### Meridian Health Analytics — NIST CSF 2.0
*Prepared by: Alex Adewoyin · Framework: NIST CSF 2.0 · Cross-mapped: HIPAA Security Rule, NIST SP 800-53*
*Classification: Confidential (illustrative — fictional organization)*

---

## 1. Executive Summary

Meridian Health Analytics ("Meridian") is a ~60-person healthcare-SaaS company that processes electronic protected health information (ePHI) for regional clinics on Microsoft Azure and Microsoft 365. The company is growing quickly and preparing for SOC 2 Type II and HIPAA attestation, but it has not yet stood up a formal security program.

This assessment evaluated Meridian against the **NIST Cybersecurity Framework 2.0** across all six functions and 22 categories, scoring each on a 0–4 maturity scale and cross-mapping findings to the HIPAA Security Rule and NIST 800-53.

**Overall maturity is 1.2 / 4 ("Initial").** Meridian has baseline technical controls — cloud-native encryption, Entra ID with MFA for most users — but almost no governance, risk management, or incident/disaster-response capability. The assessment identified **14 risks: 4 Critical and 8 High** before remediation. A three-phase, 180-day roadmap brings the program toward a **3.0 ("Defined")** target and reduces the register to **0 Critical / 0 High** residual.

The three highest-leverage problems are:
1. **Standing privileged access** with no Privileged Identity Management and no access reviews.
2. **Unmonitored detection** — alerts are generated but no one watches them, and there is no SIEM.
3. **No tested incident-response or disaster-recovery plan**, which also leaves the HIPAA 60-day breach-notification obligation unmanaged.

---

## 2. Scope & Methodology

**Scope.** Meridian's cloud production environment (Azure, Microsoft 365), its identity platform (Entra ID), its development pipeline, and the governance and processes around them. Physical security of the (minimal) office footprint was out of scope given the remote model.

**Approach.** Each of the 22 CSF 2.0 categories was scored for **current** and **target** maturity:

| Score | Level | Meaning |
| :-- | :-- | :-- |
| 0 | None | No capability in place |
| 1 | Initial | Ad hoc, undocumented, inconsistent |
| 2 | Developing | Partially implemented, some documentation |
| 3 | Defined | Documented, consistent, repeatable |
| 4 | Managed | Measured, enforced, continuously improved |

**Risk scoring.** Risks were scored on a 5×5 matrix — Likelihood (1–5) × Impact (1–5) = inherent score (1–25) — banded **Critical ≥16, High ≥10, Medium ≥5, Low <5**. Each risk received a treatment decision and a residual score reflecting the recommended control.

---

## 3. Current-State Assessment by Function

**GOVERN (avg 0.8 — weakest function).** Meridian has no documented risk-management strategy, no defined risk appetite, and no security roles or accountability assigned in writing — security rests informally on one part-time lead. Policies are ad hoc, and leadership has no oversight cadence for cyber. Supply-chain risk is unmanaged: cloud providers, the MSP, and subprocessors are not formally assessed, and Business Associate Agreements are not centrally tracked (a direct HIPAA concern).

**IDENTIFY (avg 1.3).** A partial asset inventory exists, but ePHI data stores are not classified or mapped. Critically, Meridian performs **no periodic security risk assessment**, which the HIPAA Security Rule (§164.308(a)(1)(ii)(A)) requires. There is no structured improvement loop to track findings to closure.

**PROTECT (avg 1.8 — most mature).** This is where Meridian's cloud-native baseline helps: encryption at rest and in transit is on, and most users have MFA. But identity controls are the biggest single risk area — standing privileged access, shared admin accounts, no PIM, and no access reviews. There is no DLP or data classification for PHI, workforce security training has lapsed, patching through the MSP is inconsistent, and no hardening baselines are enforced.

**DETECT (avg 1.0).** Microsoft Defender and M365 generate alerts, but no one monitors them and there is no SIEM or central log aggregation. There is no defined process to analyze or correlate events, so real incidents could sit undetected for a long time.

**RESPOND (avg 1.3).** There is no incident-response plan, no defined severities or escalation, and no breach-notification runbook — leaving the HIPAA 60-day notification deadline unmanaged. Log retention is insufficient to scope an incident forensically.

**RECOVER (avg 1.3).** Cloud redundancy exists but failover has never been tested, and there is no disaster-recovery or business-continuity plan. A ransomware event today would likely cause a prolonged outage and potential data loss.

---

## 4. Key Risks (see Risk Register for the full 14)

| ID | Risk | Inherent | Residual |
| :-- | :-- | :-- | :-- |
| R-01 | Standing privileged access / no PIM | **Critical (20)** | Medium (8) |
| R-03 | Incomplete MFA / legacy auth → account takeover | **Critical (16)** | Medium (8) |
| R-05 | Unmonitored alerts (no SIEM) → long dwell time | **Critical (16)** | Medium (6) |
| R-02 | No access reviews → orphaned / excess access | **Critical (16)** | Medium (6) |
| R-04 | No IR plan / HIPAA 60-day breach deadline | High (15) | Medium (8) |
| R-06 | Unassessed vendors / untracked BAAs | High (15) | Medium (8) |
| R-09 | Untested backups / no DR → ransomware impact | High (15) | Medium (8) |
| R-13 | Cloud misconfiguration exposes ePHI | High (15) | Medium (8) |

Every risk maps to a CSF subcategory and a concrete control. Where I have built and tested that control in a hands-on lab, the register cites it as evidence (PIM/RBAC, access reviews, SIEM triage, consent hardening, cloud posture, vulnerability management).

---

## 5. Prioritized Remediation Roadmap

**Phase 1 — 0–30 days (low cost, highest-severity first).** Write the IR plan and HIPAA breach-notification runbook; enforce MFA for all and block legacy auth; inventory and centralize BAAs; turn on and begin monitoring Defender/M365 alerts.

**Phase 2 — 30–90 days.** Deploy PIM and quarterly access reviews and remove standing Owner; run the first formal HIPAA risk assessment (feeding this register); stand up a vendor-risk program; launch recurring awareness and phishing training; implement immutable backups and run a DR test.

**Phase 3 — 90–180 days.** Deploy a SIEM with a triage workflow; classify ePHI and deploy DLP; enforce CIS hardening baselines, patch SLAs, and cloud-posture management; establish the policy framework and a leadership oversight cadence.

This sequence closes the Critical and High risks first, front-loads cheap wins, and moves overall maturity from ~1.2 toward the 3.0 target.

---

## 6. HIPAA Alignment Note

Because Meridian handles ePHI, several findings are not just best-practice gaps but **HIPAA Security Rule obligations**: the risk-assessment program (§164.308(a)(1)), workforce training (§164.308(a)(5)), incident procedures (§164.308(a)(6)), contingency/DR planning (§164.308(a)(7)), Business Associate Agreements (§164.308(b)), access controls (§164.312(a)), and breach notification (§164.400–414). Closing the Phase 1–2 items materially reduces regulatory exposure ahead of the planned attestation.

---

## Appendix — Scoring Legend

- **Maturity:** 0 None · 1 Initial · 2 Developing · 3 Defined · 4 Managed/Optimized
- **Risk bands:** Critical ≥16 · High ≥10 · Medium ≥5 · Low <5 (Likelihood 1–5 × Impact 1–5)
- **Treatment:** Mitigate · Transfer · Accept · Avoid

*Limitations: this is a documentation-and-interview–based maturity assessment of a fictional organization, not a technical audit or penetration test. Scores reflect program maturity, not a guarantee of control effectiveness.*
