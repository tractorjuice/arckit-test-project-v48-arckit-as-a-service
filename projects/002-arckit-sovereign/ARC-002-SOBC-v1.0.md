# ArcKit as a Service (Sovereign Deployment) — Strategic Outline Business Case

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:sobc`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-SOBC-v1.0 |
| **Document Type** | Strategic Outline Business Case (Green Book five-case) |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Owner** | Mark Craddock (Service Owner) |
| **Distribution** | ARB; Vendor SLT; MOD Defence Digital (where helpful for partnership conversations) |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial SOBC for sovereign route. Pairs with project 001 SOBC; cross-subsidy contribution argument explicit. |

---

## 0. Executive Summary

The sovereign deployment route exists for two reasons:

1. **Mission**: serve sites that cannot use the multi-tenant SaaS — MOD, sensitive central-government departments, regulated industries — while keeping the codebase single (Principle 21).
2. **Commercial**: produce per-engagement margin that contributes to the SaaS cross-subsidy (project 001 BR-005), helping fund the SME free tier (Principle 1).

The recommended way forward is a **single signed bundle** for air-gapped install (project 002 ADR-001), an **LTS line** for patches (ADR-002), customer-controlled identity (ADR-003) and AI (ADR-004) — co-engineered with the SaaS so that no codebase fork develops.

---

## 1. Strategic Case

### 1.1 Strategic context

Some UK Government and regulated-industry sites cannot use multi-tenant SaaS. They require a copy of the service that runs entirely within their controlled boundary, often air-gapped, often under formal accreditation (MOD Authority to Operate; sectoral equivalents). Today such sites either build bespoke architecture tooling, do without, or rely on documents-and-spreadsheets. None of these scales to the governance bar that NCSC / GDS / TCoP / SbD requires.

### 1.2 Strategic objectives

| ID | Objective |
|----|-----------|
| SO-1 | Provide the same ArcKit value to sites that cannot use multi-tenant SaaS, with no engineering bifurcation |
| SO-2 | Generate per-engagement margin that contributes to project 001 cross-subsidy |
| SO-3 | Support customer accreditation against MOD SbD / NCSC CAF / sector-equivalent standards |
| SO-4 | Deliver LTS patches predictably under published SLA |
| SO-5 | Deliver and operate the route without overwhelming a small vendor team |

### 1.3 Outcomes

| Outcome | Beneficiary | Measure |
|---------|-------------|---------|
| Reference customer in MOD or comparable site | Vendor; mission credibility | BR-008 |
| Sovereign customers reach Authority to Operate | Customer; vendor pipeline | Per engagement |
| LTS patch SLA met | Customer; vendor reputation | NFR-C-005 |
| Sovereign margin contribution to project 001 SaaS cross-subsidy | SMEs (indirectly) | Project 001 BR-005 |

---

## 2. Economic Case

### 2.1 Long-list

A. **Single signed bundle + LTS** (Recommended).
B. **Per-customer custom build**.
C. **No sovereign route** (focus on SaaS only).
D. **Sovereign-only** (drop SaaS).

### 2.2 Short-list rationale

- A is co-engineered with SaaS, single codebase, repeatable.
- B breaks single-codebase, multiplies operational cost.
- C abandons the mission for sites that can't use SaaS, and forfeits the cross-subsidy contribution.
- D abandons the SME-affordability mission entirely.

### 2.3 Recommended

**Option A** — single signed bundle, LTS patch line, customer-controlled identity / AI / KMS / observability, single codebase with SaaS.

### 2.4 Economic appraisal (indicative)

| Stream | Year 1 (alpha→GA) | Year 2 | Year 3 |
|--------|-------------------|--------|--------|
| Engineering FTE — incremental over SaaS | 1–2 (sovereign deliv. + LTS) | 2 | 2–3 |
| HSM + signing infrastructure | one-off | low | low |
| Sales / partnership effort | low | medium | medium |
| Per-engagement delivery cost | low | medium | medium |
| Per-engagement margin contribution to 001 BR-005 | nil (alpha) | low | medium |

---

## 3. Commercial Case

### 3.1 Procurement routes

- G-Cloud (where appropriate).
- DOS for outcome-based engagements.
- Defence frameworks (DCPP / cyber-cleared supplier routes) for MOD.
- Direct procurement for non-government regulated industries.

### 3.2 Pricing

Per-engagement pricing — bundle delivery + initial install + LTS subscription. Pricing covers cost-to-deliver plus margin contribution to project 001 cross-subsidy.

### 3.3 Contract structure

- Bespoke per-engagement MSA + SLA + DPA.
- LTS subscription separately priced.
- Optional vendor remote support channel (INT-009).

---

## 4. Financial Case

- Year 1: investment phase; low revenue; HSM and pipeline build.
- Year 2: first paying engagements; margin starts contributing to 001 BR-005.
- Year 3: steady cadence; margin contribution material.

Threshold question: per-engagement margin × engagement count > sovereign incremental engineering cost. Currently judged plausible at 3–5 engagements/year by year 3.

---

## 5. Management Case

### 5.1 Delivery approach

Phased: alpha (build pipeline + first reference customer dry-run) → GA (first paid engagement) → steady cadence. See `ARC-002-PLAN-v1.0.md`.

### 5.2 Governance

Vendor SLT + ARB; per-engagement: customer SIRO and Accreditor.

### 5.3 Key roles

- Sovereign Delivery Lead (PENDING).
- LTS Engineering Lead (PENDING).
- Vendor Security Lead (shared with project 001).
- Vendor DPO (shared with project 001).

### 5.4 Risks

- SR-002 (codebase bifurcation) — largest engineering risk.
- SR-005 (customer accreditation slips) — largest commercial risk.
- SR-020 / project 001 R-006 (key-person) — largest delivery risk.

---

## 6. Recommendations and Conditions

Proceed with Option A subject to:

1. Sovereign Delivery Lead and LTS Engineering Lead appointed before alpha.
2. HSM procured and key ceremony complete.
3. Reference-customer engagement (BR-008) targeted for first GA window.
4. Project 001 SaaS alpha gate cleared first (sequence; per project 001 plan).
5. ARB approval of per-engagement risk-appetite annex template (MOD SbD Action M-1).

---

## 7. Linked Artefacts

- Principles, REQ, STKE, RISK (project 002).
- ADRs 001 / 002 / 003 / 004 (project 002).
- MOD SbD; DPIA (project 002).
- Plan, HLD (project 002).
- Project 001 SOBC (parent commercial framing).

---

## 8. External References

- HM Treasury Green Book: https://www.gov.uk/government/publications/the-green-book-appraisal-and-evaluation-in-central-governent
- Defence Cyber Protection Partnership (DCPP): https://www.gov.uk/government/groups/defence-cyber-protection-partnership-dcpp

---

**Generated by**: ArcKit `/arckit:sobc` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
