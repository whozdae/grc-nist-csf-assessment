# Healthcare SaaS Security Program Assessment — NIST CSF 2.0

![Framework](https://img.shields.io/badge/Framework-NIST%20CSF%202.0-1F3864)
![Mapped](https://img.shields.io/badge/Mapped-HIPAA%20Security%20Rule%20%C2%B7%20NIST%20800--53-2E5496)
![Artifact](https://img.shields.io/badge/Deliverables-Gap%20Assessment%20%2B%20Risk%20Register-brightgreen)

> I ran a full cybersecurity program assessment for a (fictional) healthcare-SaaS company against the **NIST Cybersecurity Framework 2.0**, cross-mapped every finding to the **HIPAA Security Rule** and **NIST SP 800-53**, built a scored **risk register**, and produced a phased **remediation roadmap**. This is the governance-and-risk counterpart to my hands-on labs — it shows I can *assess and prioritize* a security program, not just build individual controls.

| | |
| :-- | :-- |
| **Client (fictional)** | Meridian Health Analytics — ~60-person healthcare SaaS processing ePHI on Azure/M365, fully remote, prepping for SOC 2 + HIPAA attestation |
| **What I produced** | A CSF 2.0 gap/maturity assessment (22 categories), a 14-item scored risk register, and a 3-phase, 180-day remediation roadmap |
| **Headline result** | Overall maturity **1.2 → 3.0 target** (Initial → Defined); remediation reduces the register from **4 Critical / 8 High to 0 Critical / 0 High** |
| **Skills** | GRC assessment, NIST CSF 2.0, HIPAA Security Rule, NIST 800-53, risk scoring & treatment, roadmapping, executive reporting |

---

## Deliverables
- **[`grc-assessment.xlsx`](grc-assessment.xlsx)** — the workbook (open this first):
  - **Summary** — maturity by CSF function, risk rollup (inherent vs. residual), executive takeaways
  - **CSF Gap Assessment** — all 22 CSF 2.0 categories scored current vs. target (0–4), with observations and HIPAA/800-53 mappings
  - **Risk Register** — 14 risks scored likelihood × impact, with treatment, owner, and residual risk
  - **Remediation Roadmap** — phased 0–30 / 30–90 / 90–180 day actions
- **[`gap-assessment-report.md`](gap-assessment-report.md)** — the formal narrative report (scope, methodology, findings by function, roadmap)

---

## Methodology
- **Framework:** NIST CSF 2.0 — all six functions (Govern, Identify, Protect, Detect, Respond, Recover) across their 22 categories.
- **Maturity scale (0–4):** 0 None · 1 Initial · 2 Developing · 3 Defined · 4 Managed/Optimized. Each category scored **current** and **target**; the gap drives prioritization.
- **Risk scoring:** 5×5 — Likelihood (1–5) × Impact (1–5) = score (1–25), banded Critical (≥16) / High (≥10) / Medium (≥5) / Low. Each risk carries a treatment decision and a **residual** score after the recommended control.
- **Cross-mapping:** every gap and risk is tied to the relevant **HIPAA Security Rule** citation and **NIST 800-53** control family, so the assessment speaks to both a framework audit and a HIPAA posture review.

## Key findings
1. **Overall posture is "Initial" (1.2/4).** The weakest functions are **Govern** (0.8) and **Respond/Recover** — the program has controls but almost no documented governance, risk management, or incident/disaster response.
2. **Three issues drive most of the risk:** standing privileged access with no PIM, security alerts no one monitors (no SIEM), and no tested incident-response or disaster-recovery plan.
3. **HIPAA-specific exposure:** no periodic risk assessment (required by §164.308), lapsed workforce training, untracked Business Associate Agreements, and no breach-notification runbook — which puts the **60-day HIPAA notification deadline** at risk.
4. **The fix is front-loaded and cheap.** Phase 1 (0–30 days) is almost all low-cost policy and configuration work, and it closes the highest-severity gaps first.

## From gap to control — tied to work I've actually built
A GRC assessment is stronger when the assessor can also *implement* the fix. Several register items map directly to labs in my portfolio:

| Risk | Control | Proof |
| :-- | :-- | :-- |
| Standing privileged access (R-01) | PIM + least-privilege RBAC | [AZURE-IAM](https://github.com/whozdae/AZURE-IAM) |
| No access reviews / offboarding (R-02) | Access reviews + JML automation | access-review & JML lifecycle repos |
| Unmonitored alerts (R-05) | SIEM + alert triage | [Home-SOC](https://github.com/whozdae/Home-SOC-in-Azure), [ai-soc-analyst](https://github.com/whozdae/ai-soc-analyst) |
| OAuth consent abuse (R-08) | Consent hardening + detection | [entra-oauth-consent-defense](https://github.com/whozdae/entra-oauth-consent-defense) |
| Patching / cloud misconfig (R-11, R-13) | Vuln mgmt + CIS posture | [azure-cloud-security](https://github.com/whozdae/azure-cloud-security), [pyvulnscan](https://github.com/whozdae/pyvulnscan) |

## How to read the workbook
Open **Summary** for the one-screen picture, then **CSF Gap Assessment** for the control-level detail and **Risk Register** for the scored risks. Color scales run green→red on gaps and risk scores. Every number is a live formula — change a Likelihood or Impact and the score, rating, and rollups recalculate.

## Skills demonstrated
GRC program assessment · NIST CSF 2.0 · HIPAA Security Rule · NIST 800-53 · risk identification, scoring & treatment · residual-risk analysis · remediation roadmapping · executive-level security reporting.

---

*Prepared by Alex "Dae" Adewoyin as a portfolio GRC work sample. Meridian Health Analytics is fictional; all data is illustrative.*
