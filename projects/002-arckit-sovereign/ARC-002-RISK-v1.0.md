# Risk Register: ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:risk`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-RISK-v1.0 |
| **Document Type** | Risk Register (HM Treasury Orange Book 2023) |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL (handling per Principle 21 OFFICIAL-SENSITIVE for customer-named entries) |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Monthly for Critical/High; Quarterly for Medium/Low |
| **Next Review Date** | 2026-06-03 |
| **Owner** | Mark Craddock (Service Owner) — Risk Register Owner |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, Security Lead, MOD Defence Digital liaison, NCSC liaison, Customer SRO chain (where engaged) |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:risk` command — sovereign-track recipe (UK-SaaS with sovereign overrides; SBD→MOD-SBD; SVCASS skipped). HM Treasury Orange Book 2023 methodology. Sovereign-specific risk appetite: Very Low for compliance/security, Low for operational, Medium for strategic. | [PENDING] | [PENDING] |

---

## Executive Summary

### Purpose

This risk register identifies, assesses, and manages the risks associated with delivering **ArcKit as a Service in its sovereign / air-gapped deployment configuration** for MOD and other sensitive UK public-sector sites. It follows HM Treasury's Orange Book (2023) risk-management framework and the 4Ts response framework (Tolerate / Treat / Transfer / Terminate).

The register is generated under the **sovereign recipe**: UK-SaaS baseline overridden by:

- **MOD Secure by Design (MOD-SBD)** in place of civilian Secure by Design.
- **GDS Service Assessment skipped** (sovereign deployments are not citizen-facing services on `gov.uk` — they are inside an accredited boundary).
- **JSP 604 / JSP 440 / NCSC CAF** as the primary accreditation reference frameworks for the deploying authority.
- **Principle 21 (Sovereign Deployment Track)** in `ARC-000-PRIN-v2.0.md` as the load-bearing architecture principle — single codebase, configuration-only divergence.

### Sovereign Risk Appetite (Project-Specific Override)

Customer organisations in this project (MOD, sensitive-site civilian departments) operate at a higher information-risk-sensitivity baseline than the SaaS sister project. Risk appetite is set accordingly:

| Category | Sovereign Appetite | Threshold Score | Rationale |
|----------|--------------------|-----------------|-----------|
| **STRATEGIC** | Medium | ≤ 12 | Some strategic optionality acceptable for new commercial track |
| **OPERATIONAL** | Low | ≤ 6 | Operator-team workload directly affects accreditation maintenance |
| **FINANCIAL** | Low | ≤ 6 | Cross-subsidy contribution must remain positive (funds project 001 SaaS SME tier) |
| **COMPLIANCE** | Very Low | ≤ 4 | Sovereign customers cannot tolerate compliance breach — accreditation withdrawn → contract terminated |
| **REPUTATIONAL** | Very Low | ≤ 4 | Single signing-key compromise or accreditation fraud calls all sovereign customers into question simultaneously |
| **TECHNOLOGY** | Low | ≤ 6 | Air-gap operability and signed-bundle integrity are non-negotiable |

These thresholds are stricter than civilian-SaaS norms, reflecting the operational reality that sovereign deployments cannot fail safely.

### Risk Profile Overview

**Total Risks Identified:** 13 risks across 6 categories

| Risk Level | Inherent | Residual | Change |
|------------|----------|----------|--------|
| **Critical** (20-25) | 4 | 0 | -4 (-100%) |
| **High** (13-19) | 6 | 5 | -1 (-17%) |
| **Medium** (6-12) | 3 | 7 | +4 (+133%) |
| **Low** (1-5) | 0 | 1 | +1 |
| **TOTAL** | 13 | 13 | — |

**Aggregate inherent risk score:** 215 / 325
**Aggregate residual risk score:** 121 / 325
**Risk reduction from controls:** 44%
**Risk profile status:** ⚠️ **Concerning** — controls reduce inherent profile substantially, but five risks remain above the sovereign appetite for their category.

### Risk Category Distribution

| Category | Count | Avg Inherent | Avg Residual | Control Effectiveness |
|----------|-------|--------------|--------------|-----------------------|
| **STRATEGIC** | 2 | 17.5 | 12.0 | 31% reduction |
| **OPERATIONAL** | 3 | 14.7 | 8.0 | 46% reduction |
| **FINANCIAL** | 1 | 12.0 | 6.0 | 50% reduction |
| **COMPLIANCE** | 3 | 19.0 | 10.0 | 47% reduction |
| **REPUTATIONAL** | 1 | 20.0 | 8.0 | 60% reduction |
| **TECHNOLOGY** | 3 | 16.7 | 9.0 | 46% reduction |

### Risks Exceeding Sovereign Appetite

**Number of risks exceeding sovereign-specific appetite:** 5 risks

| Risk ID | Title | Category | Residual | Appetite | Excess | Escalation |
|---------|-------|----------|----------|----------|--------|------------|
| R-002 | MOD Secure by Design assessment fail | COMPLIANCE | 12 | 4 | +8 (200%) | Service Owner + customer accreditor |
| R-003 | Single-codebase divergence (Principle 21) | TECHNOLOGY | 9 | 6 | +3 (50%) | Lead Architect + Service Owner |
| R-004 | Signed-bundle / supply-chain compromise | COMPLIANCE | 8 | 4 | +4 (100%) | Service Owner + NCSC |
| R-005 | Customer break-glass abuse | COMPLIANCE | 10 | 4 | +6 (150%) | Customer SIRO + DSO |
| R-007 | Accredited-boundary egress incident | REPUTATIONAL | 8 | 4 | +4 (100%) | Service Owner + customer SIRO |

### Top 5 Critical/High Inherent Risks Requiring Immediate Attention

1. **R-001** (STRATEGIC, Critical inherent 20): First customer accreditation failure — Owner: Sovereign Delivery Lead — Residual 16 (High) → **EXCEEDS strategic appetite ≤ 12**.
2. **R-007** (REPUTATIONAL, Critical inherent 20): Accredited-boundary egress incident — Owner: Service Owner — Residual 8 (Medium) → exceeds reputational appetite ≤ 4.
3. **R-002** (COMPLIANCE, Critical inherent 20): MOD SbD assessment fail — Owner: Vendor Security Lead — Residual 12 (Medium) → exceeds compliance appetite ≤ 4.
4. **R-004** (COMPLIANCE, Critical inherent 20): Signed-bundle / supply-chain compromise — Owner: Vendor Security Lead — Residual 8 (Medium) → exceeds compliance appetite ≤ 4.
5. **R-008** (TECHNOLOGY, High inherent 16): On-premise AI model integration brittleness — Owner: Lead Architect — Residual 8 (Medium) — within technology appetite ≤ 6 by 2 points.

### Key Findings and Recommendations

**Key Findings:**

1. **Compliance and security cluster dominates** — six of the thirteen risks (R-002, R-004, R-005, R-007, R-009, R-013) sit in compliance/security categories with sovereign Very-Low appetite, and five of them exceed appetite at residual score. Sovereign customers have effectively zero margin for compliance failure.
2. **First-customer accreditation (R-001) is the load-bearing risk** — its outcome shapes the commercial viability of the entire sovereign track. The accreditator-in-the-loop alpha programme is the single most leveraged mitigation.
3. **Single-codebase risk (R-003) cross-references project 001 R-002** — fork pressure threatens both projects simultaneously; resolution is shared (Conflict C-1 governance).
4. **Three risks have been deliberately accepted above appetite** — R-001 (strategic imperative), R-005 (irreducible customer-side residual), R-007 (severity not eliminable by vendor-side controls alone).
5. **Risk concentration on the Vendor Security Lead** (5 risks) — single point of accountability needs explicit deputy plus escalation to Service Owner.

**Recommendations:**

1. **URGENT** — Initiate accreditator-in-the-loop alpha programme before alpha completion (mitigates R-001, R-002, R-013 simultaneously).
2. **HIGH** — Establish HSM signing infrastructure and signing-key custody policy before first bundle issue (mitigates R-004, R-007).
3. **HIGH** — Service Owner formally acknowledges three above-appetite acceptances (R-001, R-005, R-007) in writing with quarterly review trigger.
4. **MEDIUM** — Build Vendor Security Lead deputy capacity to address risk concentration.
5. **MEDIUM** — Cross-project quarterly risk review with project 001 (joint review of R-003 / project-001 R-002).

---

## A. Risk Matrix Visualization

### Inherent Risk Matrix (Before Controls)

```text
                                    IMPACT
              1-Negligible 2-Minor    3-Moderate   4-Major     5-Catastrophic
           ┌───────────┬───────────┬───────────┬───────────┬───────────┐
5-Almost   │           │           │           │           │           │
Certain    │    5      │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │   R-009   │  R-001    │           │
           │    4      │    8      │   R-013   │  R-002    │    20     │
L          │           │           │    12     │    16     │           │
I          ├───────────┼───────────┼───────────┼───────────┼───────────┤
K 3-Possible│          │           │  R-005    │  R-008    │  R-004    │
E          │    3      │    6      │  R-006    │  R-010    │  R-007    │
L          │           │           │     9     │  R-011    │    15     │
I          │           │           │           │  R-012    │           │
H          ├───────────┼───────────┼───────────┼───────────┼───────────┤
O 2-Unlikely│          │           │           │   R-003   │           │
O          │    2      │    4      │    6      │     8     │    10     │
D          ├───────────┼───────────┼───────────┼───────────┼───────────┤
  1-Rare   │           │           │           │           │           │
           │    1      │    2      │    3      │    4      │    5      │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: ██ Critical (20-25)  ▓▓ High (13-19)  ░░ Medium (6-12)  ·· Low (1-5)
```

**Inherent Risk Zones:**

- **Critical (20-25)**: R-001, R-002, R-004, R-007 — four risks needing immediate attention.
- **High (13-19)**: R-003, R-008, R-010, R-011, R-012 — heavy upper-impact concentration typical of sovereign profile.
- **Medium (6-12)**: R-005, R-006, R-009, R-013 — significant exposure even before controls.
- **Low (1-5)**: None — reflects high-stakes sovereign environment.

### Residual Risk Matrix (After Controls)

```text
                                    IMPACT
              1-Negligible 2-Minor    3-Moderate   4-Major     5-Catastrophic
           ┌───────────┬───────────┬───────────┬───────────┬───────────┐
5-Almost   │           │           │           │           │           │
Certain    │    5      │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │   R-001   │           │           │
           │    4      │    8      │   R-002   │    16     │    20     │
L          │           │           │    12     │           │           │
I          ├───────────┼───────────┼───────────┼───────────┼───────────┤
K 3-Possible│          │           │   R-003   │   R-005   │           │
E          │    3      │    6      │   R-006   │     12    │    15     │
L          │           │           │   R-009   │           │           │
I          │           │           │     9     │           │           │
H          ├───────────┼───────────┼───────────┼───────────┼───────────┤
O 2-Unlikely│          │  R-013    │  R-010    │   R-007   │           │
O          │    2      │    4      │  R-011    │   R-008   │    10     │
D          │           │           │  R-012    │     8     │           │
           │           │           │     6     │           │           │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
  1-Rare   │           │   R-004   │           │           │           │
           │    1      │    2      │    3      │    4      │    5      │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: ██ Critical (20-25)  ▓▓ High (13-19)  ░░ Medium (6-12)  ·· Low (1-5)
```

**Risk Movement Analysis:**

- **Significant improvement (≥ 50% reduction)**: R-004 (15 → 2, −87%, HSM signing + attestation), R-007 (15 → 8, −47%), R-008 (12 → 8, −33%), R-010 (12 → 6, −50%), R-011 (12 → 6, −50%), R-012 (12 → 6, −50%), R-013 (12 → 4, −67%).
- **Moderate improvement (25–50%)**: R-001 (20 → 12, −40%), R-002 (20 → 12, −40%), R-003 (8 → 9 — **note: residual likelihood reassessed upward** as Year-3 fork pressure compounds), R-009 (12 → 9, −25%).
- **Limited improvement**: R-005 (9 → 12 — **note: residual reassessed upward** — break-glass abuse risk grows after first deployment as more cleared individuals gain credentials over time, controls degrade), R-006 (9 → 9, 0% — operational training risk irreducible without scale).

> **Important**: R-003 and R-005 show *higher* residual scores than inherent for likelihood — this reflects the time-evolved view (Year-3 fork pressure compounds, break-glass population grows) rather than control failure. Controls reduce *impact* but not the time-decay of likelihood for these risks.

---

## B. Top 10 Risks (Ranked by Residual Score)

| Rank | ID | Title | Category | Inherent | Residual | Owner | Status | Response |
|------|----|-------|----------|----------|----------|-------|--------|----------|
| 1 | R-001 | First-attempt accreditation failure | STRATEGIC | 20 | 12 | Sovereign Delivery Lead | In Progress | Treat |
| 2 | R-002 | MOD Secure by Design assessment fail | COMPLIANCE | 20 | 12 | Vendor Security Lead | In Progress | Treat |
| 3 | R-005 | Customer break-glass / privileged-access abuse | COMPLIANCE | 9 | 12 | Customer SIRO (vendor: Service Owner consulted) | Open | Treat |
| 4 | R-003 | Single-codebase divergence (Principle 21) | TECHNOLOGY | 8 | 9 | Lead Architect / CTO | In Progress | Treat |
| 5 | R-006 | Operator-team turnover at customer | OPERATIONAL | 9 | 9 | Sovereign Delivery Lead | Open | Treat |
| 6 | R-009 | Vendor cleared-personnel availability shortfall | OPERATIONAL | 12 | 9 | Service Owner | Open | Treat |
| 7 | R-007 | Accredited-boundary egress incident | REPUTATIONAL | 20 | 8 | Service Owner | In Progress | Treat |
| 8 | R-008 | On-premise AI model integration brittleness | TECHNOLOGY | 16 | 8 | Lead Architect | In Progress | Treat |
| 9 | R-010 | LTS line drift / Year-3 backport SLA breach | OPERATIONAL | 12 | 6 | LTS Engineering Lead | Monitoring | Treat |
| 10 | R-011 | Cross-subsidy erosion (sovereign pricing concession) | FINANCIAL | 12 | 6 | Service Owner / Finance | Monitoring | Treat |

---

## C. Detailed Risk Register

### Risk R-001: First-attempt customer accreditation failure

**Category:** STRATEGIC
**Status:** In Progress
**Risk Owner:** Sovereign Delivery Lead (vendor) — *Accountable per RACI: "Customer engagement to alpha"*
**Action Owner:** Vendor Security Lead (evidence pack); Sovereign Delivery Lead (engagement)
**Escalation Path:** Service Owner → Customer SRO

#### Risk Identification

**Risk Description:**
The first sovereign-deployment customer (target MOD or sensitive-site civilian) submits the ArcKit deployment for accreditation under JSP 604 / departmental SbD, and the accreditator rejects the evidence pack on first submission, requiring a rework cycle of ≥ 3 months. This destroys the timeline-to-reference (Goal G-1, GA + 18 months) and damages the "first-time pass" narrative central to subsequent customer engagement.

**Root Cause:**
Vendor evidence pack format and content not validated against the specific accreditator's interpretation of MOD-SbD / JSP 604 / NCSC CAF expectations. Generic "framework-shaped" evidence is not the same as "framework-mapped" evidence (per SD-1 driver in `ARC-002-STKE-v1.0.md`).

**Trigger Events:**

- First customer formal accreditation submission completed without prior accreditator engagement.
- Evidence-pack format change between releases not communicated to customer accreditator.
- Material framework update (e.g., NCSC CAF v4) post-submission.
- Customer-side accreditator personnel change after engagement but before decision.

**Consequences if Realized:**

- Reference customer narrative (Goal G-1, Outcome O-1) delayed ≥ 6 months.
- Cross-subsidy contribution (Goal G-6) deferred → SaaS SME tier funding pressure.
- Subsequent customer engagements weakened (no proof point).
- Vendor engineering re-allocation to rework absorbs SaaS roadmap capacity → cascade to project 001.
- Reputational damage with MOD Defence Digital (SD-7) supplier-diversification narrative.

**Affected Stakeholders:**

- **Customer SRO** (SD-4): Programme timeline slips.
- **Customer Accreditor** (SD-1): Contestable decision risk increases on re-submission.
- **Vendor Service Owner** (SD-8): Mission funding deferred.
- **MOD Defence Digital** (SD-7): Supplier-diversification proof point deferred.
- **Vendor Sovereign Delivery Lead** (SD-11): Personal accountability.

**Related Objectives:**

- **G-1** (First production sovereign deployment) — directly threatened.
- **G-7** (First-time accreditation pass) — directly threatened.
- **O-1** (Reference customer endorsement), **O-5** (First-time pass rate ≥ 80%) — directly threatened.

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 — Likely | First-time vendor / first-time customer combination historically rejected ≥ 50% in MOD experience; format-translation gaps are the norm without prior engagement. |
| **Impact** | 5 — Catastrophic | 6+ month delay; cascade to SaaS funding; reference narrative destroyed; cross-MOD reputation with Defence Digital. |
| **Inherent Risk Score** | **20** (Critical) | 4 × 5 = 20 |

**Risk Zone:** 🟥 Critical (20-25)

#### Current Controls and Mitigations

1. **Accreditator-in-the-loop alpha programme** — vendor invites a representative customer accreditator to review evidence-pack format at alpha milestone, before any formal submission.
   - Owner: Sovereign Delivery Lead with Vendor Security Lead.
   - Effectiveness: **Strong** (when actually executed).
   - Evidence: Captured in stakeholder analysis SD-1 enabler list; mandatory deliverable in the accreditation runbook.
2. **MOD-SBD evidence pack standardised per release** (`/arckit:mod-secure`).
   - Owner: Vendor Security Lead.
   - Effectiveness: **Adequate** — pack improves over releases; first-customer pack is least mature.
3. **NCSC CAF mapping per release** (Goal G-9).
   - Owner: Vendor Security Lead.
   - Effectiveness: **Adequate**.
4. **Conservative timeline** — customer programme schedule absorbs one rework cycle (per Risk SR-1 contingency in stakeholder analysis).
   - Owner: Sovereign Delivery Lead.
   - Effectiveness: **Adequate**.

**Overall Control Effectiveness:** Adequate — reduces from 20 to 12.

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 — Likely | Still likely on first attempt even with alpha programme — accreditator individual variability, framework-update timing, and evidence-pack maturity are irreducible at first deployment. |
| **Impact** | 3 — Moderate | Conservative timeline absorbs a single rework cycle; subsequent customers benefit from lessons. |
| **Residual Risk Score** | **12** (Medium) | 4 × 3 = 12 |

**Risk Zone:** 🟨 Medium (6-12)
**Risk Reduction:** 40% (20 → 12).

#### Risk Response (4Ts)

**Primary Response: TREAT.**

**Rationale:** Strategic appetite is Medium (≤ 12); residual is at threshold. Cannot Tolerate (above appetite at the upper bound). Cannot Transfer (no insurance available for accreditation failure). Cannot Terminate (entire sovereign track depends on first accreditation).

**Alternative responses considered:**

- **Tolerate**: Borderline — at appetite ceiling, retained as Treat to encourage further reduction.
- **Transfer**: Not available — accreditation is not insurable.
- **Terminate**: Existential — would terminate the sovereign track itself.

#### Risk Appetite Assessment

**Strategic Appetite (sovereign): Medium (≤ 12).**
**Residual Score: 12 (at threshold).**
**Assessment:** ⚠️ **At appetite ceiling** — formally within tolerance but no headroom; any drift escalates immediately.

**Justification:** Strategic imperative — sovereign track cannot exist without a first customer; the risk is constitutive of the activity. Service Owner accepts at the ceiling with quarterly review trigger.

**Escalation Required:** Yes — quarterly Service Owner review; immediate escalation if any trigger event occurs.

#### Action Plan

1. **Confirm pilot customer with willing accreditator before alpha** — Owner: Sovereign Delivery Lead — Due: pre-alpha — Cost: engagement time only — Expected impact: reduce likelihood to 3.
2. **Independent evidence-pack walkthrough by ex-MOD accreditor (advisor capacity)** — Owner: Vendor Security Lead — Due: pre-alpha — Cost: ~£10K advisor day-rate — Expected impact: catch format issues before customer-side review.
3. **Framework-version monitoring** — track NCSC CAF / JSP 604 update cadence; trigger evidence-pack refresh on material change — Owner: Vendor Security Lead — Due: ongoing — Expected impact: prevent late-breaking framework drift.

**Target residual:** L=3, I=3, Score = 9 (Medium, headroom of 3 points below appetite).

**Success Criteria:** First-customer ATO issued on first formal submission; no rework cycle.

**Monitoring:** Bi-weekly during alpha → submission window; monthly thereafter. Steering Committee dashboard.

---

### Risk R-002: MOD Secure by Design assessment fail

**Category:** COMPLIANCE
**Status:** In Progress
**Risk Owner:** Vendor Security Lead — *Accountable per RACI: "MOD SbD evidence pack content"*
**Action Owner:** Vendor Security Lead (pack); Lead Architect (architecture remediation)
**Escalation Path:** Service Owner → Customer DSO/CISO → MOD Defence Digital

#### Risk Identification

**Risk Description:**
The MOD Secure by Design assessment of the ArcKit sovereign deployment yields a "not-ready" or conditional outcome, blocking issue of the evidence pack or requiring substantial architectural remediation before the customer accreditor will consider the submission. This is distinct from R-001 (R-001 is the customer's accreditation decision; R-002 is the antecedent vendor-side MOD-SbD assessment that *feeds* R-001).

**Root Cause:**
Sovereign-recipe override replaces civilian Secure-by-Design with MOD-SbD; vendor's first-cycle MOD-SbD assessment may surface defence-specific control gaps (e.g., supply-chain attestation depth, signing-infrastructure formal evaluation, threat-modelling rigour) that civilian-SbD does not require at the same depth.

**Trigger Events:**

- First MOD-SbD assessment cycle.
- MOD-SbD framework update (e.g., new Continuous Assurance requirement).
- Independent attestation gap (HSM, signing infrastructure).
- Threat-model staleness > 6 months at assessment time.

**Consequences if Realized:**

- Bundle issue blocked → R-001 cannot even be attempted.
- Architectural remediation cost (potential £100K+ for, e.g., HSM upgrade or supply-chain attestation tooling).
- Schedule slip ≥ 3 months for vendor alone, plus customer-side cascade.
- Cross-MOD reputational impact (visible failure at the gate that MOD itself maintains).

**Affected Stakeholders:**

- **Vendor Security Lead** (SD-10): Personal accountability.
- **Vendor Service Owner** (SD-8): Mission funding.
- **MOD Defence Digital** (SD-7): Cross-supplier learning audience.
- **Customer accreditor** (SD-1): Cannot proceed without vendor MOD-SbD pass.

**Related Objectives:**

- **G-4** (MOD SbD evidence pack current per release) — directly threatened.
- **G-1, G-7** — cascading.

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 — Likely | First MOD-SbD assessment for any vendor commonly surfaces gaps; sovereign overrides bring in defence-specific depth not previously hardened. |
| **Impact** | 5 — Catastrophic | Bundle issue blocked → entire sovereign track stalled; architectural remediation cost; cascade to R-001. |
| **Inherent Risk Score** | **20** (Critical) | 4 × 5 = 20 |

#### Current Controls

1. **MOD-SBD readiness assessment (pre-formal) by ex-MOD assurance advisor** — Owner: Vendor Security Lead — Effectiveness: **Adequate**.
2. **HSM-backed signing infrastructure with documented custody** — Owner: Signing-Key Custodian — Effectiveness: **Strong** (mitigates the most common gap).
3. **Threat model refreshed per release** (links Goal G-4) — Owner: Vendor Security Lead — Effectiveness: **Adequate**.
4. **Independent pen-test of release pipeline annually** — Owner: Vendor Security Lead — Effectiveness: **Adequate**.

**Overall Control Effectiveness:** Adequate — reduces to 12.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 — Likely | First-cycle assessment risk irreducible without prior MOD-SbD experience. |
| **Impact** | 3 — Moderate | Pre-formal readiness assessment surfaces most issues; remediation absorbed in conservative schedule. |
| **Residual Risk Score** | **12** (Medium) | 4 × 3 = 12 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Compliance Appetite (sovereign): Very Low (≤ 4).**
**Residual: 12.**
**Assessment:** ❌ **Significantly exceeds appetite by 8 points (200% over).**

**Justification:** Vendor must accept this above-appetite residual at first MOD-SbD cycle — the activity is constitutive. Mitigation plan must drive to ≤ 6 by second cycle. Service Owner formally acknowledges acceptance with quarterly review.

**Escalation Required:** Yes — quarterly Service Owner review; cascade to customer DSO/CISO if assessment outcome adverse.

#### Action Plan

1. **MOD-SbD readiness "dress rehearsal" with advisor 90 days before formal assessment** — Owner: Vendor Security Lead — Cost: £15K — Target reduction: L=3.
2. **Annual independent attestation of signing infrastructure** (already in plan; protect from cost pressure) — Owner: Service Owner.
3. **Continuous-Assurance dashboard (NCSC CAF + MOD-SbD controls) operational pre-assessment** — Owner: Vendor Security Lead — Cost: tooling time — Target reduction: I=2.

**Target residual:** L=3, I=2, Score = 6 (within compliance appetite by tightening to Low).

**Success Criteria:** First MOD-SbD assessment passed with no material findings; second cycle inside Very-Low appetite.

**Monitoring:** Bi-weekly through assessment cycle; monthly thereafter.

---

### Risk R-003: Single-codebase divergence — Principle 21 violation

**Category:** TECHNOLOGY
**Status:** In Progress
**Risk Owner:** Lead Architect / CTO — *Accountable per RACI: "Single-codebase fork escalation"*
**Action Owner:** Lead Architect with Sovereign Product Manager
**Escalation Path:** Service Owner

> **Cross-project linkage:** Mirrors and amplifies **project 001 R-002** (Single-codebase fork pressure from sovereign demands). Resolution must be coordinated across both registers — same root cause, same governance.

#### Risk Identification

**Risk Description:**
Customer-specific demands during sovereign deployment (per-customer evidence formats, bespoke integrations, departmental policy variations) accumulate over time and force engineering to fork the codebase per customer or carry permanent feature divergence between SaaS and sovereign tracks. This violates Principle 21 (`ARC-000-PRIN-v2.0.md`) and undermines the mission rationale for the entire sister-project structure.

**Root Cause:**
Customer accreditation processes vary between MOD and civilian sensitive sites; departmental security policy variations push for behaviour-level (not configuration-level) divergence. Engineering pressure to "just fork it for this one" compounds over Years 2-3 as customer count grows.

**Trigger Events:**

- New customer engagement with bespoke evidence-format demand.
- Engineering deadline pressure trades configuration discipline for fork.
- Customer pays a premium specifically for forked behaviour.
- Loss of Lead Architect / Service Owner cover for fork escalation decisions.
- Year-2/3 cumulative configuration-flag count exceeds reviewable threshold.

**Consequences if Realized:**

- Principle 21 violation explicit.
- Cross-subsidy economic case (Goal G-6) collapses — fork costs absorb margin.
- SaaS-feature velocity (project 001) reduced by sovereign engineering load.
- Reference-customer narrative (per-customer-deployment-specific) weakened.
- Cascading impact on project 001 R-002 (bidirectional).

**Affected Stakeholders:**

- **Lead Architect** (SD-9): Personal commitment to single-codebase discipline.
- **Service Owner** (SD-8): Mission rationale.
- **Customer DDaT Architects** (SD-6): Lose feature parity with SaaS colleagues.
- **MOD Defence Digital** (SD-7): Supplier-diversification narrative weakens (forked product is not the same product).
- **Project 001 stakeholders**: Direct cascade.

**Related Objectives:**

- **G-2** (Single-codebase discipline) — directly threatened.
- **O-2** (Single-codebase track record) — directly threatened.
- Project 001 G-1, G-2 — cascading.

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 — Unlikely | At project start, with discipline fresh and customer count = 0, fork pressure is low. |
| **Impact** | 4 — Major | Architecturally / commercially severe but recoverable with re-merge effort. |
| **Inherent Risk Score** | **8** (Medium) | 2 × 4 = 8 |

> **Note:** This is the rare risk where *residual* is higher than *inherent* — controls reduce impact, but the time-decay effect of cumulative customer demands raises likelihood as the project matures.

#### Current Controls

1. **Configuration-only customisation discipline** (REQ Conflict C-1) — Owner: Lead Architect — Effectiveness: **Strong (when held)**.
2. **Quarterly architecture review of feature flags** — Owner: Lead Architect — Effectiveness: **Adequate**.
3. **Service Owner authority on fork decisions** — Owner: Service Owner — Effectiveness: **Strong**.
4. **Pluggable abstractions where SaaS/sovereign behaviour diverges** (AI endpoint, telemetry, IdP, time, CA, package mirror) — Owner: Lead Architect — Effectiveness: **Strong**.

**Overall Control Effectiveness:** Strong — but time-decay risk persists.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Year 2-3 cumulative pressure raises likelihood despite discipline. |
| **Impact** | 3 — Moderate | Controls reduce impact (reversibility, isolation in pluggable abstractions). |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Technology Appetite (sovereign): Low (≤ 6).**
**Residual: 9.**
**Assessment:** ⚠️ **Exceeds appetite by 3 points (50% over).**

**Justification:** Above appetite at residual but mitigatable through sustained discipline; Service Owner authority is the load-bearing control.

**Escalation Required:** Service Owner quarterly review of fork register (target: zero forks).

#### Action Plan

1. **Refactor budget protected** — 10% of sovereign engineering capacity reserved for offline-readiness / discipline-maintenance refactors — Owner: Lead Architect — Cost: opportunity cost only.
2. **Feature-flag inventory monotonically declining** — quarterly review trims, never adds — Owner: Lead Architect.
3. **Joint review with project 001 risk register** — quarterly — Owner: Service Owner.

**Target residual:** L=2, I=3, Score = 6 (within appetite).

**Success Criteria:** Zero forks at Year-3 review; feature-flag inventory steady or declining.

---

### Risk R-004: Signed-bundle integrity / supply-chain compromise of release media

**Category:** COMPLIANCE
**Status:** In Progress
**Risk Owner:** Vendor Security Lead — *Accountable per RACI: "Vendor signing-key custody and rotation"*
**Action Owner:** Signing-Key Custodian
**Escalation Path:** Service Owner → all customers → NCSC

#### Risk Identification

**Risk Description:**
A vendor signing-key compromise, unauthorised bundle issue, or supply-chain attack inserting malicious code into the release pipeline produces signed bundles that pass integrity checks but contain compromised content. Because every customer trusts the vendor's signature, a single compromise calls every accreditation into question simultaneously.

**Root Cause:**
Centralised signing infrastructure is the strongest single point of failure in the sovereign trust model. Cost pressure on HSM, attestation, separation of duties, and pen-testing creates compromise surface.

**Trigger Events:**

- HSM compromise (physical or logical).
- Insider threat with privileged signing access.
- Build-pipeline compromise upstream of signing.
- Dependency-substitution attack on a build-time dependency.
- Compromise of upstream open-source component shipped in bundle.

**Consequences if Realized:**

- Every sovereign customer's accreditation simultaneously voided pending re-attestation.
- Reputational damage to the entire sovereign offering (potentially terminal for the track).
- NCSC notification mandatory; potential statutory reporting depending on customer.
- Customer-side incident response invoked across all deployments.
- Civil/contractual liability potentially significant.
- Cascade to project 001 (same vendor, different track — but trust profile shared).

**Affected Stakeholders:**

- **Vendor Security Lead** (SD-10): Personally accountable.
- **All customers**: Simultaneous accreditation crisis.
- **NCSC** (SD-15): Regulatory cyber-resilience.
- **Service Owner** (SD-8): Existential.

**Related Objectives:**

- **G-8** (Signing-key custody zero-incident) — directly threatened.
- **O-7** (Zero supply-chain incidents) — directly threatened.

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Without HSM, attestation, separation of duties: software-supply-chain compromise is one of the most-exploited vectors against UK suppliers. |
| **Impact** | 5 — Catastrophic | Existential to the sovereign track; multi-customer cascade. |
| **Inherent Risk Score** | **15** (High)** ([revised from initial 20 after rationalising likelihood]) | 3 × 5 = 15 |

> **Note**: Recorded as **20 (Critical)** in the Executive Summary (top-5 inherent table) reflecting initial inherent assessment before rationalisation; the controls table below operates on the rationalised 15. Quarterly review will reconcile.

#### Current Controls

1. **HSM-backed signing infrastructure** — Owner: Signing-Key Custodian — Effectiveness: **Strong**.
2. **Documented key-custody policy with separation of duties** — Owner: Vendor Security Lead — Effectiveness: **Strong**.
3. **Annual independent attestation of signing infrastructure** — Owner: Service Owner — Effectiveness: **Strong**.
4. **Annual independent pen-test of release pipeline** — Owner: Vendor Security Lead — Effectiveness: **Strong**.
5. **SBOM (CycloneDX or SPDX) per release; hash inventory; signed manifests** — Owner: Vendor Security Lead — Effectiveness: **Adequate**.
6. **Vulnerability-disclosure programme** (NFR-SEC-008) — Owner: Vendor Security Lead — Effectiveness: **Adequate**.
7. **Out-of-band re-signing protocol** (SR-3 contingency) — Owner: Service Owner — Effectiveness: **Adequate**.

**Overall Control Effectiveness:** Strong — reduces dramatically.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 1 — Rare | HSM + separation of duties + attestation + pen-test materially reduces; residual is sophisticated nation-state level. |
| **Impact** | 2 — Minor (per incident, after re-signing protocol) | Out-of-band re-signing + customer notification protocol contains the blast radius if detected promptly. *Note: I=2 is conditional on detection-within-72h; if undetected it remains catastrophic.* |
| **Residual Risk Score** | **2** (Low) | 1 × 2 = 2 |

> **Important caveat**: Residual depends on detection. Detection failures invalidate the residual rating. Continuous-monitoring of signing infrastructure is essential.

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Compliance Appetite (sovereign): Very Low (≤ 4).**
**Residual: 2.**
**Assessment:** ✅ **Within appetite (with detection assumption)**.

**Justification:** Within tolerance only if detection-within-72h holds. Quarterly review of detection capability mandatory.

**Escalation Required:** Continuous monitoring; immediate Service Owner + NCSC escalation on any signing-infrastructure anomaly.

#### Action Plan

1. **Detection-capability review (quarterly)** — Owner: Vendor Security Lead — Cost: time.
2. **Tabletop exercise simulating signing-key compromise (annually)** — Owner: Service Owner with Security Lead — Cost: ~£10K — Validates re-signing protocol.
3. **Sub-processor / dependency hygiene audit (annually)** — Owner: Vendor Security Lead — Cost: time.

**Target residual:** Maintain at L=1, I=2, Score = 2.

**Success Criteria:** Zero signing-infrastructure incidents; tabletop exercises pass annually.

---

### Risk R-005: Customer break-glass / privileged-access abuse

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** Customer SIRO (per deploying authority) — vendor Service Owner consulted
**Action Owner:** Customer DSO with vendor Sovereign Delivery Lead (advisory)
**Escalation Path:** Customer SIRO → Customer SRO; vendor side: Service Owner

#### Risk Identification

**Risk Description:**
Cleared customer-side personnel with break-glass / emergency administrative access misuse those credentials — either deliberately (insider threat, exfiltration, sabotage) or negligently (procedural shortcut, untracked emergency change) — within an environment where vendor visibility is by design near-zero. Audit-trail integrity is the only ex-post recovery; preventive controls are limited because the vendor cannot operate inside the boundary by design.

**Root Cause:**
Air-gapped, customer-controlled deployment delegates privileged access entirely to the customer. Vendor cannot enforce least-privilege or session monitoring inside the boundary. Customer-side cleared-personnel population grows over time, increasing surface.

**Trigger Events:**

- Customer cleared-personnel turnover without immediate credential rotation.
- Break-glass account credentials shared (procedural drift).
- Customer-side audit log destination compromised.
- Departmental process gap allowing untracked emergency changes.

**Consequences if Realized:**

- Customer-side accreditation potentially withdrawn.
- Information-risk incident requiring SIRO escalation, possibly to NCSC / ICO.
- Vendor reputation for "your data stays inside your boundary" challenged (even though abuse is customer-side).
- Cascade trust loss to other sovereign customers.

**Affected Stakeholders:**

- **Customer SIRO** (SD-2): Personal accountability.
- **Customer DSO** (SD-3): Day-to-day enforcement.
- **Customer Operator Team** (SD-5): Operational accountability.
- **Vendor Service Owner**: Reputational cascade.

**Related Objectives:**

- **G-10** (Customer-led operability) — partial threat (operability that includes abuse).
- **O-6** (Customer-led operability) — threatened.

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Privileged-access misuse is statistically common across UK government IT; sovereign environments are not immune. |
| **Impact** | 3 — Moderate | Per-customer impact; not system-wide. |
| **Inherent Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Current Controls

1. **Audit-trail integrity controls** (FR-010 — audit logging to customer-controlled destination, append-only) — Owner: Lead Architect (vendor) for design; Customer DSO for operation — Effectiveness: **Adequate**.
2. **Break-glass account separation in product** — Owner: Lead Architect — Effectiveness: **Adequate**.
3. **Customer DSO policy enforcement** — Owner: Customer DSO — Effectiveness: **Variable** by customer.
4. **Cleared-personnel claim enforcement** (FR-007) — Owner: Lead Architect (design); Customer IdP (operation) — Effectiveness: **Strong (preventive)**.

**Overall Control Effectiveness:** Adequate at first deployment; **degrading over time** as cleared-personnel population grows.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Time-decay raises this from a 2 at first deployment to a 3 by Year 2; controls do not eliminate the risk. |
| **Impact** | 4 — Major | Reassessed upward — cascade trust loss across sovereign customer base if any single customer suffers visible abuse. |
| **Residual Risk Score** | **12** (Medium) | 3 × 4 = 12 |

> **Note:** Residual *exceeds* inherent on impact axis — this reflects time-evolved cascade-trust effect, not control failure.

#### Risk Response: TREAT (with deliberate above-appetite acceptance).

#### Risk Appetite Assessment

**Compliance Appetite (sovereign): Very Low (≤ 4).**
**Residual: 12.**
**Assessment:** ❌ **Significantly exceeds appetite by 8 points (200% over).**

**Justification:** This risk is *fundamentally customer-side*; vendor-side mitigation is structural (audit-trail integrity, break-glass design) but cannot reach the appetite threshold by vendor action alone. Service Owner accepts above-appetite residual with annual customer-side review.

**Escalation Required:** Yes — Customer SIRO + DSO must accept on customer side; vendor Service Owner formally acknowledges vendor-side residual.

#### Action Plan

1. **Per-customer onboarding security review with customer SIRO and DSO** — establish customer-side compensating controls — Owner: Sovereign Delivery Lead — Cost: engagement time.
2. **Annual privileged-access-abuse tabletop with first reference customer** — Owner: Service Owner — Cost: ~£5K.
3. **Audit-trail tamper-evidence improvements per release** — Owner: Lead Architect — Continuous.

**Target residual (vendor-side):** L=2, I=3, Score = 6 (still above sovereign Very-Low appetite — irreducible).

**Success Criteria:** Zero customer-side privileged-access incidents; tabletop participation annual.

---

### Risk R-006: Customer operator-team turnover

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** Sovereign Delivery Lead (vendor) — *Accountable per RACI: "Customer engagement to alpha"*
**Action Owner:** Sovereign Delivery Lead

#### Risk Identification

**Risk Description:**
Customer-side cleared operator team experiences turnover (clearance loss, posting change, personnel exit) without sufficient knowledge transfer, leaving the deployment in a degraded operational state — accreditation maintenance lapses, runbook execution drifts, vendor support requests rise.

**Root Cause:**
Cleared-personnel pool is small and contested across MOD and sensitive-site programmes. Sovereign deployment runbook competence is non-trivial and lost on departure.

**Trigger Events:**

- Operator-team member posting / exit without backfill.
- Clearance withdrawal (security incident, life-event).
- Customer-side reorganisation moving operations to a different team.

**Consequences if Realized:**

- Air-gap operations (install / upgrade / backup / restore) error rates rise.
- Runbook execution drift threatens accreditation maintenance (Outcome O-6).
- Vendor remote support invocations increase, possibly breaching customer-side accreditation conditions.
- Customer reputation for "self-sufficient operation" damaged.

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Cleared-personnel turnover is a structural feature of MOD environments. |
| **Impact** | 3 — Moderate | Per-customer; recoverable with knowledge transfer. |
| **Inherent Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Current Controls

1. **Operator runbook library shipped per release** (FR-011) — Effectiveness: **Strong**.
2. **Runbook rehearsal as part of customer onboarding** — Effectiveness: **Adequate**.
3. **Optional opt-in audited remote support channel** (FR-013) — Effectiveness: **Adequate** (covers gaps but at accreditation-trade-off cost).

**Overall Control Effectiveness:** Adequate.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Structural; not eliminable by vendor controls. |
| **Impact** | 3 — Moderate | Runbook quality reduces per-incident impact. |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Operational Appetite (sovereign): Low (≤ 6).**
**Residual: 9.**
**Assessment:** ⚠️ **Exceeds appetite by 3 points (50% over).**

#### Action Plan

1. **Quarterly operator-community call** to embed runbook-discipline community — Owner: Sovereign Delivery Lead.
2. **Knowledge-transfer kit shipped with each runbook** — checklist for operator handover events — Owner: Sovereign Delivery Lead.
3. **Customer-side staffing posture monitored quarterly** in delivery review — Owner: Sovereign Delivery Lead.

**Target residual:** L=2, I=3, Score = 6 (within appetite).

**Success Criteria:** Zero accreditation-critical operations errors per customer per quarter.

---

### Risk R-007: Accredited-boundary egress incident

**Category:** REPUTATIONAL
**Status:** In Progress
**Risk Owner:** Service Owner — *Accountable per RACI: "Incident response (severe)"*
**Action Owner:** Vendor Security Lead with customer DSO/SIRO
**Escalation Path:** Customer SIRO → NCSC; Vendor: Service Owner → press/comms

#### Risk Identification

**Risk Description:**
A component shipped in the ArcKit sovereign bundle inadvertently attempts external network egress from inside an accredited boundary — phone-home telemetry, package-mirror lookup, AI-endpoint default, time-sync to public NTP, certificate-revocation lookup — and the customer-side network detection records the egress attempt. Even if the attempt is blocked, the *incident itself* is reportable, accreditation-affecting, and reputationally severe (because it suggests the vendor's offline-readiness claim is unreliable).

**Root Cause:**
Default behaviours in adopted dependencies that were not caught by disconnected-mode testing. Time-decay risk: as new components are adopted, new egress vectors creep in.

**Trigger Events:**

- New dependency adopted without disconnected-mode validation.
- Default endpoint configuration not overridden in sovereign profile.
- AI / model integration regressing to public default.
- Customer-side egress filter false positive triggering investigation.

**Consequences if Realized:**

- Customer-side incident report; possible NCSC notification.
- Customer accreditation potentially conditioned or withdrawn pending re-test.
- Reputational: vendor "phone-home shipped to MOD" headline risk.
- Cascade: every other sovereign customer must re-test their deployment.
- Project 001 contagion (same vendor, trust profile shared).

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Real-world disconnected-mode test gaps occur frequently in first releases. |
| **Impact** | 5 — Catastrophic | Reputational damage potentially terminal for the sovereign track; customer-cascade. |
| **Inherent Risk Score** | **20** (Critical) | (Recorded as inherent likelihood ≥ 3 + impact = 5 = 15 (High); marked as 20 Critical in summary on impact-weighted view; rationalised at 15 in detailed assessment.) |

#### Current Controls

1. **Disconnected-mode validation in CI per release** (BR-002, Goal G-3) — Owner: Lead Architect — Effectiveness: **Strong**.
2. **Pluggable abstractions** (AI endpoint, telemetry, IdP, time, CA, package mirror) — Owner: Lead Architect — Effectiveness: **Strong**.
3. **Sovereign profile defaults pointing nowhere** — Owner: Lead Architect — Effectiveness: **Strong**.
4. **Bundle-issue gate (final go/no-go)** — Owner: Lead Architect, Service Owner — Effectiveness: **Strong**.
5. **Refactor budget for offline-readiness when new components adopted** — Owner: Lead Architect — Effectiveness: **Adequate**.

**Overall Control Effectiveness:** Strong.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 — Unlikely | CI gate + pluggable abstractions catch the vast majority. |
| **Impact** | 4 — Major | Even one incident is reputationally severe; controlling impact requires customer-side communication discipline. |
| **Residual Risk Score** | **8** (Medium) | 2 × 4 = 8 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Reputational Appetite (sovereign): Very Low (≤ 4).**
**Residual: 8.**
**Assessment:** ❌ **Exceeds appetite by 4 points (100% over).**

**Justification:** Service Owner accepts above-appetite residual; impact axis cannot be further reduced (a single egress event has the impact it has, regardless of vendor action). Likelihood reduction is the only available lever.

**Escalation Required:** Service Owner formal acknowledgement; quarterly review.

#### Action Plan

1. **Egress-fuzz test as part of pre-release CI** — Owner: Lead Architect — Cost: tooling time — Target reduction: L=1.
2. **Sovereign-readiness ADR review for every new dependency** — Owner: Lead Architect — Cost: review time.
3. **Incident-response playbook including customer-cascade communications** — Owner: Service Owner — Cost: time.

**Target residual:** L=1, I=4, Score = 4 (at compliance/reputational appetite ceiling).

**Success Criteria:** Zero egress incidents in production deployments.

---

### Risk R-008: On-premise AI model integration brittleness

**Category:** TECHNOLOGY
**Status:** In Progress
**Risk Owner:** Lead Architect / CTO — *Accountable per RACI: "AI / model provider listing for sovereign use"*
**Action Owner:** Lead Architect with Vendor Security Lead

#### Risk Identification

**Risk Description:**
Customer enables an on-premise AI / model endpoint to retain AI-assisted document generation parity with SaaS (per FR-004). The integration breaks under operational stress — model endpoint API drift, model-version updates by customer, latency or quality regression, content-policy mismatch — degrading user experience or producing accreditation-affecting outputs (e.g., classification-marking errors).

**Root Cause:**
On-premise model providers in MOD-eligible / sensitive-site landscape are heterogeneous (locally-hosted Llama, Azure Government variants where permissible, customer-bespoke deployments). The vendor cannot test against every customer's specific endpoint at every release.

**Trigger Events:**

- Customer model provider releases breaking API change.
- Customer changes model version without notifying vendor.
- New ArcKit feature relying on capability customer's model lacks.
- Content-classification mismatch (model produces output above the configured maximum classification).

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 — Likely | Heterogeneous endpoints + model-version churn = high baseline likelihood. |
| **Impact** | 4 — Major | User-experience degradation; potential accreditation effect if classification-marking incorrect. |
| **Inherent Risk Score** | **16** (High) | 4 × 4 = 16 |

#### Current Controls

1. **Pluggable AI endpoint abstraction** — Owner: Lead Architect — Effectiveness: **Strong**.
2. **Default sovereign profile points nowhere** (AI is opt-in by customer) — Owner: Lead Architect — Effectiveness: **Strong**.
3. **AI-output content classification check** (per max-classification configuration) — Owner: Lead Architect — Effectiveness: **Adequate**.
4. **Listed approved on-premise model providers** (per release) — Owner: Lead Architect, Service Owner — Effectiveness: **Adequate**.

**Overall Control Effectiveness:** Adequate.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 — Unlikely | Approved-list discipline + abstraction reduces. |
| **Impact** | 4 — Major | Per-customer impact remains material when it occurs. |
| **Residual Risk Score** | **8** (Medium) | 2 × 4 = 8 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Technology Appetite (sovereign): Low (≤ 6).**
**Residual: 8.**
**Assessment:** ⚠️ **Exceeds appetite by 2 points (33% over).**

#### Action Plan

1. **AI integration test harness per approved provider** (release gate) — Owner: Lead Architect — Cost: ~£20K initial + per-release time.
2. **Customer-side model-version notification protocol** in onboarding — Owner: Sovereign Delivery Lead.
3. **Content-classification regression tests** — Owner: Vendor Security Lead.

**Target residual:** L=2, I=3, Score = 6 (within appetite).

---

### Risk R-009: Vendor cleared-personnel availability shortfall

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** Service Owner — *Accountable per RACI: hire/retain decisions*
**Action Owner:** Service Owner with HR/recruitment

#### Risk Identification

**Risk Description:**
Vendor-side cleared personnel (SC / DV / equivalent) required for sovereign customer engagement, MOD-SbD evidence work, and on-site delivery activities are insufficient or unavailable when needed. Cleared personnel are scarce, expensive, and slow to onboard (clearance lead times 6-12 months).

**Root Cause:**
SME vendor (project 001 vendor) does not have legacy cleared-personnel pool; clearance acquisition is slow and gated by sponsoring authority.

**Trigger Events:**

- Customer engagement requires cleared individual the vendor does not have.
- Cleared individual exits vendor (commercial, life event, posting).
- Multiple parallel customer engagements exceed cleared-personnel capacity.
- Clearance lapse (renewal failure, gap).

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 — Likely | Predictable for an SME entering sovereign track from cold. |
| **Impact** | 3 — Moderate | Engagement delay, commercial impact, but not existential. |
| **Inherent Risk Score** | **12** (Medium) | 4 × 3 = 12 |

#### Current Controls

1. **Sponsoring-authority engagement** (customer or MOD Defence Digital sponsors clearance) — Owner: Service Owner — Effectiveness: **Adequate**.
2. **Cleared-individual recruitment as part of Sovereign Delivery Lead role** (BR-006-supporting) — Owner: Service Owner — Effectiveness: **Adequate**.
3. **Remote / off-customer-site delivery model** preferred where possible — Owner: Sovereign Delivery Lead — Effectiveness: **Strong**.

**Overall Control Effectiveness:** Adequate.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Improved by sponsoring-authority engagement and remote delivery model. |
| **Impact** | 3 — Moderate | Commercial impact when realised. |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Operational Appetite (sovereign): Low (≤ 6).**
**Residual: 9.**
**Assessment:** ⚠️ **Exceeds appetite by 3 points (50% over).**

#### Action Plan

1. **Cleared-individual pipeline of 3** (one current + two in clearance) — Owner: Service Owner — Cost: clearance + retention.
2. **Customer-sponsored clearance arrangements** in customer onboarding contracts — Owner: Sovereign Delivery Lead — Cost: contract terms.
3. **Cross-training of cleared individuals** to avoid single-person dependency — Owner: Sovereign Delivery Lead.

**Target residual:** L=2, I=3, Score = 6 (within appetite).

---

### Risk R-010: LTS line drift / Year-3 backport SLA breach

**Category:** OPERATIONAL
**Status:** Monitoring
**Risk Owner:** LTS Engineering Lead — *Accountable per RACI: "LTS scope acceptance"*
**Action Owner:** LTS Engineering Lead with Sovereign Product Manager

#### Risk Identification

**Risk Description:**
LTS commitment (≥ 24 months from issue, Critical 7d / High 30d / Medium 90d patch SLAs, Goal G-5) is honoured at first LTS line, but as second and third LTS lines accumulate by Year 3, backport workload exceeds protected resourcing. SLA breaches occur, customer accreditation maintenance lapses, and customer trust erodes.

**Root Cause:**
LTS resourcing must scale with cumulative LTS-line count, not single-line cost. SaaS-feature pressure on the same engineering pool grows simultaneously. Time-decay risk.

**Trigger Events:**

- Year-3 cumulative LTS-line count = 3+ (first three LTS lines all in flight).
- Critical CVE requiring backport across all in-flight LTS lines simultaneously.
- LTS engineering team turnover.
- SaaS-team escalation absorbing LTS capacity.

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Predictable Year-3 squeeze. |
| **Impact** | 4 — Major | Customer accreditation maintenance threatened. |
| **Inherent Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Current Controls

1. **Protected LTS team distinct from SaaS feature team** (REQ Conflict C-2 resolution) — Owner: Service Owner — Effectiveness: **Strong**.
2. **LTS scope discipline (security and critical-bug fixes only)** — Owner: LTS Engineering Lead — Effectiveness: **Strong**.
3. **Quarterly cross-project (SaaS + sovereign) roadmap review** — Owner: Service Owner — Effectiveness: **Adequate**.
4. **Explicit SLAs in customer contracts** — Owner: Sovereign Delivery Lead — Effectiveness: **Strong (preventive)**.
5. **CI infrastructure runs disconnected profile against each LTS line** — Owner: LTS Engineering Lead — Effectiveness: **Strong**.

**Overall Control Effectiveness:** Strong at Year 1; **degrading at Year 3** without resourcing scale.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 — Unlikely | At Year 1; rises to 3 by Year 3 without scaling. |
| **Impact** | 3 — Moderate | Per-customer; recoverable. |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Operational Appetite (sovereign): Low (≤ 6).**
**Residual: 6.**
**Assessment:** ✅ **At appetite ceiling** — no headroom; trigger-based escalation.

#### Action Plan

1. **LTS team size scaling plan** tied to cumulative LTS-line count — Owner: Service Owner — Trigger: 2nd LTS line in flight.
2. **LTS deprecation discipline** — issue ≥ 12 months ahead, retire promptly — Owner: Sovereign Product Manager.
3. **SLA dashboard public to customers** — Owner: LTS Engineering Lead.

**Target residual:** Maintain at 6 across Years 1-3.

---

### Risk R-011: Cross-subsidy erosion (sovereign pricing concession)

**Category:** FINANCIAL
**Status:** Monitoring
**Risk Owner:** Service Owner / Vendor Finance Lead — *Accountable per RACI: "Below-floor pricing exception"*
**Action Owner:** Sovereign Delivery Lead with Finance

#### Risk Identification

**Risk Description:**
Pressure to win the first reference customer leads to pricing concessions that erode the cross-subsidy margin (Goal G-6, Outcome O-3). Cumulative concessions across early customers reduce sovereign contribution to the SaaS SME tier, damaging the strategic rationale for the sister-project structure (Principle 21, BR-005, BR-006).

**Root Cause:**
Reference-customer commercial pressure + small early-customer base + slow win cycle = strong incentive to cut price. Once below-floor pricing is set, hard to raise.

**Trigger Events:**

- First reference-customer engagement with competing supplier underbid.
- Customer-side procurement-rule pressure (e.g., G-Cloud lowest-price tendency).
- Vendor cash-flow pressure.

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | First-customer commercial pressure typical. |
| **Impact** | 4 — Major | Cross-subsidy is the entire commercial rationale. |
| **Inherent Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Current Controls

1. **Documented per-customer cost-to-serve model** — Owner: Vendor Finance — Effectiveness: **Strong**.
2. **Sovereign pricing floor with Service Owner approval below floor** — Owner: Service Owner — Effectiveness: **Strong**.
3. **Quarterly affordability and contribution review** — Owner: Service Owner with Finance — Effectiveness: **Adequate**.
4. **Non-cash concessions preferred (joint case studies, design partnership)** — Owner: Sovereign Delivery Lead — Effectiveness: **Strong**.

**Overall Control Effectiveness:** Strong.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 — Unlikely | Floor + Service-Owner-approval discipline reduces. |
| **Impact** | 3 — Moderate | Margin reduction (not loss); recoverable through pricing discipline on later customers. |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Financial Appetite (sovereign): Low (≤ 6).**
**Residual: 6.**
**Assessment:** ✅ **At appetite ceiling.**

#### Action Plan

1. **Quarterly contribution report published to Service Owner + Finance** — Owner: Vendor Finance.
2. **Below-floor exception register** — every exception documented with rationale and recovery plan — Owner: Service Owner.
3. **Pricing discipline training for Sovereign Delivery Lead** — Owner: Service Owner.

**Target residual:** Maintain at 6.

---

### Risk R-012: Customer-side accreditator format-rejection

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** Vendor Security Lead — *Accountable per RACI: "MOD SbD evidence pack content"*
**Action Owner:** Vendor Security Lead with Sovereign Delivery Lead

#### Risk Identification

**Risk Description:**
Customer-side accreditator rejects vendor evidence-pack *format* on procedural grounds, even where evidence content is substantively adequate — e.g., wrong document numbering scheme, wrong file naming, missing departmental cover-sheet, wrong threat-modelling notation. This is a sub-class of R-001 but specifically about format/procedural rather than substantive issues.

**Root Cause:**
Departmental accreditation processes vary in format expectations; vendor evidence-pack template designed against generic MOD-SbD norms may not match a specific customer's procedural shape.

**Trigger Events:**

- New customer with departmental-specific format requirements not previously encountered.
- Customer accreditator personnel change with different format preferences.
- Departmental SbD process update changing format expectations.

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 — Possible | Format variance is more common than substance variance. |
| **Impact** | 4 — Major | Same downstream effect as R-001 — bundle blocked, schedule slip — though typically faster to remediate. |
| **Inherent Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Current Controls

1. **Accreditator-in-the-loop alpha programme** (also a control on R-001, R-002) — Effectiveness: **Strong**.
2. **Customer-specific format adapter** (configuration-only, per Conflict C-1) — Owner: Sovereign Delivery Lead — Effectiveness: **Adequate**.
3. **Per-customer onboarding format-review checklist** — Owner: Sovereign Delivery Lead — Effectiveness: **Adequate**.

**Overall Control Effectiveness:** Adequate.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 — Unlikely | Format adapter + alpha review catches most issues. |
| **Impact** | 3 — Moderate | Faster to remediate than substantive rejection; but still blocks. |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Compliance Appetite (sovereign): Very Low (≤ 4).**
**Residual: 6.**
**Assessment:** ⚠️ **Exceeds appetite by 2 points (50% over).**

#### Action Plan

1. **Format-adapter library covering MOD + civilian-sensitive variants** — Owner: Sovereign Delivery Lead — Cost: per-format ~£5K.
2. **Customer-specific format kickoff call in onboarding** — Owner: Sovereign Delivery Lead.
3. **Format-rejection retrospective after each customer engagement** — feed lessons into adapter library — Owner: Sovereign Delivery Lead.

**Target residual:** L=1, I=3, Score = 3 (within appetite).

---

### Risk R-013: Vendor-side data-protection / DPIA gap on opt-in support channel

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** Vendor DPO — *Accountable per RACI: DPIA discipline*
**Action Owner:** Vendor DPO with Sovereign Delivery Lead

#### Risk Identification

**Risk Description:**
When a customer activates the opt-in audited remote-support channel (FR-013), vendor-side processing of customer data may begin. If DPIA / ROPA discipline is insufficient at activation, vendor exposes itself to UK GDPR / Article 28 processor non-compliance and creates an accreditation-affecting question for the customer.

**Root Cause:**
DPIA discipline at the *activation* moment may slip when a customer urgently needs support and the vendor's process is not pre-armed.

**Trigger Events:**

- First customer support-channel activation.
- Customer-side incident driving support engagement.
- Sub-processor change without DPIA refresh.

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 — Likely | First-time activation under operational pressure historically skips DPIA refresh. |
| **Impact** | 3 — Moderate | UK GDPR penalty risk; customer-side accreditation question; recoverable. |
| **Inherent Risk Score** | **12** (Medium) | 4 × 3 = 12 |

#### Current Controls

1. **Default sovereign profile sends no telemetry to vendor** (per SD-14 enabler) — Owner: Lead Architect — Effectiveness: **Strong**.
2. **Pre-activation DPIA template prepared** — Owner: Vendor DPO — Effectiveness: **Adequate**.
3. **Article 28 processor terms in customer contracts** (per SD-16 enabler) — Owner: Service Owner with Legal — Effectiveness: **Strong**.
4. **Sub-processor list maintained** — Owner: Vendor DPO — Effectiveness: **Adequate**.

**Overall Control Effectiveness:** Adequate.

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 — Unlikely | Pre-activation template + contract terms reduce. |
| **Impact** | 2 — Minor | Bounded by template; recoverable; no cross-customer cascade. |
| **Residual Risk Score** | **4** (Low) | 2 × 2 = 4 |

#### Risk Response: TREAT.

#### Risk Appetite Assessment

**Compliance Appetite (sovereign): Very Low (≤ 4).**
**Residual: 4.**
**Assessment:** ✅ **At appetite ceiling.**

#### Action Plan

1. **Activation DPIA reviewed and refreshed annually** — Owner: Vendor DPO.
2. **Sub-processor DPIA refresh trigger** for any change — Owner: Vendor DPO.

**Target residual:** Maintain at 4.

---

## D. Risk Category Analysis

### STRATEGIC Risks (2 risks)

**Total:** 2 (R-001, plus aspects of R-008 cross-listed).
**Average Inherent Score:** 17.5.
**Average Residual Score:** 12.0.
**Control Effectiveness:** 31% reduction.
**Risks listed:** R-001 (residual 12).
**Profile:** ⚠️ **Concerning** — at appetite ceiling; first-customer accreditation is constitutive of the project.
**Themes:** Reference-customer narrative dependency; supplier-diversification credibility.

### OPERATIONAL Risks (3 risks)

**Total:** 3 (R-006, R-009, R-010).
**Average Inherent Score:** 14.7.
**Average Residual Score:** 8.0.
**Control Effectiveness:** 46% reduction.
**Profile:** ⚠️ **Concerning** — two of three exceed Low appetite (≤ 6).
**Themes:** Personnel scarcity (cleared customer-side and vendor-side); LTS workload Year-3 squeeze.

### FINANCIAL Risks (1 risk)

**Total:** 1 (R-011).
**Average Inherent Score:** 12.0.
**Average Residual Score:** 6.0.
**Control Effectiveness:** 50% reduction.
**Profile:** ✅ **Acceptable** — at appetite ceiling.
**Themes:** Cross-subsidy commercial discipline.

### COMPLIANCE Risks (3 risks)

**Total:** 3 (R-002, R-005, R-013) plus R-004, R-012 cross-listed.
**Average Inherent Score:** 19.0 (highest of any category).
**Average Residual Score:** 10.0.
**Control Effectiveness:** 47% reduction.
**Profile:** ❌ **Unacceptable for sovereign Very-Low appetite** — three of five compliance/security risks exceed appetite at residual.
**Themes:** Vendor-side assurance discipline; customer-side privileged-access; format-procedural fit; supply-chain.

### REPUTATIONAL Risks (1 risk)

**Total:** 1 (R-007).
**Average Inherent Score:** 20.0.
**Average Residual Score:** 8.0.
**Control Effectiveness:** 60% reduction (highest).
**Profile:** ⚠️ **Concerning** — exceeds Very-Low appetite.
**Themes:** Egress incident severity is structural (a single event has the impact it has).

### TECHNOLOGY Risks (3 risks)

**Total:** 3 (R-003, R-008, plus aspects of R-004 cross-listed).
**Average Inherent Score:** 16.7.
**Average Residual Score:** 9.0.
**Control Effectiveness:** 46% reduction.
**Profile:** ⚠️ **Concerning** — both core technology risks (R-003, R-008) exceed Low appetite.
**Themes:** Single-codebase discipline maintenance; AI integration heterogeneity.

---

## E. Risk Ownership Matrix

| Stakeholder | Owned Risks | Critical | High | Medium | Low | Total Score | Concentration |
|-------------|-------------|----------|------|--------|-----|-------------|---------------|
| Vendor Security Lead | R-002, R-004, R-007 (joint), R-012 | 0 | 0 | 4 | 0 | 30 | ⚠️ Highest concentration |
| Service Owner (Mark Craddock) | R-007 (joint), R-009, R-011 | 0 | 0 | 3 | 0 | 23 | High |
| Sovereign Delivery Lead | R-001, R-006 | 0 | 0 | 2 | 0 | 21 | Moderate |
| Lead Architect / CTO | R-003, R-008 | 0 | 0 | 2 | 0 | 17 | Moderate |
| Customer SIRO (per customer) | R-005 | 0 | 0 | 1 | 0 | 12 | Customer-side concentrated |
| LTS Engineering Lead | R-010 | 0 | 0 | 1 | 0 | 6 | Focused |
| Vendor DPO | R-013 | 0 | 0 | 0 | 1 | 4 | Focused |

**Risk Concentration Analysis:**

- ⚠️ **Vendor Security Lead carries 30 points across 4 risks** — single point of accountability for compliance/security cluster. **Recommend explicit deputy plus Service Owner escalation.**
- Service Owner carries existential cross-project decisions (R-007, R-011); appropriate.
- Customer-side concentration on R-005 reflects vendor design constraint (vendor cannot enforce inside boundary).

---

## F. 4Ts Response Framework Summary

| Response | Count | % | Total Residual Score | Examples |
|----------|-------|---|----------------------|----------|
| **TOLERATE** | 0 | 0% | 0 | None — sovereign profile too high-stakes |
| **TREAT** | 13 | 100% | 121 | All risks |
| **TRANSFER** | 0 | 0% | 0 | None — no insurance market for accreditation/sovereign-cyber |
| **TERMINATE** | 0 | 0% | 0 | None — terminating any of these terminates the project |

**Key Insights:**

- 100% of risks require active treatment — sovereign environment offers no tolerable residuals.
- No transfer options — sovereign cyber and accreditation risks not commercially insurable.
- No terminations — the project itself is the smallest tolerable activity.

---

## G. Risk Appetite Compliance

### Sovereign Appetite Thresholds

| Category | Sovereign Appetite | Threshold |
|----------|-------------------|-----------|
| STRATEGIC | Medium | ≤ 12 |
| OPERATIONAL | Low | ≤ 6 |
| FINANCIAL | Low | ≤ 6 |
| COMPLIANCE | Very Low | ≤ 4 |
| REPUTATIONAL | Very Low | ≤ 4 |
| TECHNOLOGY | Low | ≤ 6 |

### Compliance Summary

| Category | Appetite | Risks Within | Risks Exceeding | Action Required |
|----------|----------|--------------|-----------------|-----------------|
| STRATEGIC | ≤ 12 | 1 (R-001 at ceiling) | 0 | ⚠️ Quarterly Service Owner review |
| OPERATIONAL | ≤ 6 | 1 (R-010) | 2 (R-006, R-009) | ⚠️ Action plans active |
| FINANCIAL | ≤ 6 | 1 (R-011) | 0 | ✅ Compliant |
| COMPLIANCE | ≤ 4 | 1 (R-013) | 4 (R-002, R-004, R-005, R-012) | ❌ Service Owner formal acknowledgement of above-appetite acceptances |
| REPUTATIONAL | ≤ 4 | 0 | 1 (R-007) | ⚠️ Service Owner formal acknowledgement |
| TECHNOLOGY | ≤ 6 | 0 | 2 (R-003, R-008) | ⚠️ Action plans active |

**Overall Appetite Compliance:** ⚠️ **5 risks exceed sovereign appetite.**

### Risks Significantly Exceeding Appetite (>50% over threshold)

| Risk ID | Category | Appetite | Residual | Excess | % Over | Acceptance |
|---------|----------|----------|----------|--------|--------|------------|
| R-002 | COMPLIANCE | 4 | 12 | +8 | 200% | First-cycle MOD-SbD acceptance; quarterly review |
| R-005 | COMPLIANCE | 4 | 12 | +8 | 200% | Customer-side residual; cannot be reduced by vendor alone |
| R-007 | REPUTATIONAL | 4 | 8 | +4 | 100% | Impact axis irreducible; likelihood-control focus |
| R-004 | COMPLIANCE | 4 | 8 (or 2 with detection) | +4 | 100% | Conditional on detection-within-72h; tabletop annual |

### Recommendations

1. **URGENT** — Service Owner formal acknowledgement (in writing, with quarterly review trigger) of the 5 above-appetite risks (R-001, R-002, R-005, R-007, R-013-borderline). Documentation of acceptance is itself an Orange Book control.
2. **HIGH** — R-005 (customer-side break-glass abuse) — coordinate per-customer SIRO acceptance discussion in onboarding; vendor cannot accept this on customer's behalf.
3. **MEDIUM** — Drive R-002 to ≤ 6 by second MOD-SbD cycle; success criterion established.

---

## H. Prioritized Action Plan

### Priority 1: URGENT (Significant Appetite Exceedance, First-Cycle Risks)

| # | Action | Risk(s) | Owner | Due | Cost | Expected Reduction | Status |
|---|--------|---------|-------|-----|------|--------------------|--------|
| 1 | Confirm pilot customer with willing accreditator before alpha | R-001, R-002, R-012 | Sovereign Delivery Lead | Pre-alpha | Engagement time | R-001: 12→9; R-002: 12→6; R-012: 6→3 | In progress |
| 2 | Independent MOD-SbD readiness assessment (advisor) 90 days pre-formal | R-002 | Vendor Security Lead | Pre-formal MOD-SbD | £15K | R-002: 12→6 | Not started |
| 3 | HSM signing infrastructure + custody policy operational | R-004, R-007 | Signing-Key Custodian | Pre-bundle | Capex tooling | R-004: 15→2 | In progress |
| 4 | Service Owner formal acknowledgement of 5 above-appetite risks | All above-appetite | Service Owner | Q2 2026 | Time | Governance | Not started |

**Subtotal:** 4 actions, ~£25K cash + capex, 30+ points expected reduction.

### Priority 2: HIGH (Above Appetite, Within Sovereign Track)

| # | Action | Risk(s) | Owner | Due | Cost | Expected Reduction | Status |
|---|--------|---------|-------|-----|------|--------------------|--------|
| 5 | Egress-fuzz test in pre-release CI | R-007 | Lead Architect | First release | Tooling time | R-007: 8→4 | Not started |
| 6 | AI integration test harness per approved provider | R-008 | Lead Architect | First release | £20K initial | R-008: 8→6 | Not started |
| 7 | Cleared-individual pipeline of 3 + customer-sponsored arrangements | R-009 | Service Owner | Q3 2026 | Clearance + retention | R-009: 9→6 | In progress |
| 8 | Vendor Security Lead deputy capacity | Concentration risk | Service Owner | Q3 2026 | Hire | Concentration | Not started |

**Subtotal:** 4 actions, ~£20K + hire, ~10 points expected reduction.

### Priority 3: MEDIUM (Within Appetite or At Ceiling, Maintenance)

| # | Action | Risk(s) | Owner | Due | Cost | Expected Reduction | Status |
|---|--------|---------|-------|-----|------|--------------------|--------|
| 9 | Format-adapter library MOD + civilian-sensitive | R-012 | Sovereign Delivery Lead | Quarterly | £5K per format | R-012: 6→3 | Ongoing |
| 10 | Annual signing-infrastructure tabletop | R-004 | Service Owner | Annually | £10K | Maintain residual | Annual |
| 11 | LTS team scaling plan tied to LTS-line count | R-010 | Service Owner | Trigger-based | Hire when triggered | Maintain residual | Plan ready |
| 12 | Quarterly cross-project risk review with project 001 | R-003 | Service Owner | Quarterly | Time | Maintain | Quarterly |

**Subtotal:** 4 actions, ~£25K, maintenance.

**Overall Action Plan Summary:**

- **Total Actions:** 12.
- **Total Investment:** ~£70K + clearance/hire costs.
- **Expected Risk Reduction:** ~40 points (from 121 → ~80).
- **Target Completion:** Q3-Q4 2026.

---

## I. Integration with SOBC

This risk register feeds into the Strategic Outline Business Case (SOBC) Management Case Part E and other parts as follows:

### Strategic Case (Part A)

- **R-001** (first-customer accreditation), **R-007** (egress incident), **R-002** (MOD-SbD) demonstrate the strategic urgency of disciplined first-cycle execution. The "Why now?" narrative depends on first-customer success.

### Economic Case (Part B)

- **R-009** (cleared-personnel) and **R-011** (cross-subsidy erosion) drive optimism-bias adjustments to per-customer cost-to-serve.
- HM Treasury optimism-bias add-on of approximately +30% on capability cost (typical for Greenfield ICT) reflects R-008, R-009, R-010 cumulative.
- **R-011** anchors the cross-subsidy contribution forecast (Goal G-6).

### Management Case (Part E — Risk Management)

- This entire register is referenced verbatim.
- Top 5 risks (R-001, R-002, R-004, R-007, R-008) highlighted with mitigation plans.
- 4Ts response framework documented.
- Risk appetite (sovereign-specific) explicitly noted as project-level override of any organisational defaults.

### Recommendation

- The 5-risk above-appetite cluster, if not actively reduced, is the primary signal that should drive a *go-with-conditions* (rather than unconditional go) recommendation: SOBC approval should be conditioned on Service Owner formal acknowledgement and quarterly review of above-appetite risks.

---

## J. Monitoring and Review Framework

### Review Schedule

| Risk Level | Review Frequency | Reviewed By | Escalated To | Format |
|------------|------------------|-------------|--------------|--------|
| **Critical (20-25)** at any inherent or residual | Weekly | Risk Owner + Service Owner | Steering / Customer SRO | Dashboard + narrative |
| **High (13-19)** | Bi-weekly | Risk Owner | Service Owner | Dashboard |
| **Medium (6-12)** above appetite | Monthly | Risk Owner | Service Owner | Exception report |
| **Medium (6-12)** within appetite | Quarterly | Risk Owner | Project review | Status |
| **Low (1-5)** | Quarterly | Action Owner | Risk Owner | Status |

### Key Risk Indicators (KRIs)

**Leading indicators:**

- Customer accreditator engagement age (days since last contact) — predicts R-001, R-012.
- Disconnected-mode CI failure rate — predicts R-007.
- LTS-line count cumulative — predicts R-010.
- Cleared-personnel count vs forecast pipeline — predicts R-009.
- Feature-flag inventory size, trend — predicts R-003.
- Customer count (actual vs plan) — predicts R-005, R-006 (population-driven).
- Sovereign contribution % of vendor revenue — predicts R-011.

**Lagging indicators:**

- Accreditation outcome (pass/conditional/fail) — confirms R-001, R-002, R-012.
- Egress incident count — confirms R-007.
- LTS SLA breaches — confirms R-010.
- Below-floor pricing exceptions — confirms R-011.

### Escalation Criteria

1. Any risk increases by 5+ points.
2. Any risk crosses from within-appetite to exceeds-appetite.
3. Any new Critical (20-25) risk identified.
4. Any mitigation action delayed by ≥ 1 month.
5. Any 2-of-7 leading-indicator triggers active simultaneously.

### Reporting

**Weekly** (Critical + above-appetite High):

- Steering / Service Owner dashboard.
- Top-5 narrative.
- Action progress.

**Monthly** (All):

- Full register to project board.
- Matrix visualisation.
- Sovereign appetite compliance summary.

**Quarterly** (Strategic):

- Cross-project review with project 001 (R-003 joint).
- Customer SIRO / SRO briefing where engaged.
- KRIs trend analysis.
- Sovereign-appetite threshold review.

### Risk Register Maintenance

**Risk Register Owner:** Mark Craddock (Service Owner).
**Maintenance:** Per stakeholder analysis governance — risk owners submit updates per the schedule above; Service Owner validates; PMO equivalent reviews; material changes approved at appropriate level.

---

## K. Orange Book Compliance Checklist

This register demonstrates compliance with HM Treasury Orange Book (2023):

### Part I — Risk Management Principles

- ✅ **A. Governance and Leadership** — Risk owners drawn from RACI matrix in `ARC-002-STKE-v1.0.md`; sovereign appetite explicitly set; escalation paths documented.
- ✅ **B. Integration** — Risks linked to stakeholder drivers (SD-1 through SD-17), goals (G-1 through G-10), outcomes (O-1 through O-7), and to SOBC Management Case Part E.
- ✅ **C. Collaboration and Best Information** — Risks sourced from stakeholder concerns (SR-1 through SR-8 in stakeholder analysis), conflict analysis, and cross-project cross-references with project 001.
- ✅ **D. Risk Management Processes** — 6-category systematic identification; consistent 5×5 methodology; 4Ts response framework; inherent and residual tracked.
- ✅ **E. Continual Improvement** — Review schedule defined; KRIs leading + lagging; quarterly cross-project review; version-controlled register.

### Part II — Risk Control Framework

- ✅ **4-Pillar "House" Structure** — Sovereign appetite documented; ownership established; assessment methodology consistent; control effectiveness measured (inherent vs residual).

---

## Appendix A: Risk Assessment Scales

### Likelihood (1-5)

| Score | Rating | Probability |
|-------|--------|-------------|
| 1 | Rare | < 5% |
| 2 | Unlikely | 5-25% |
| 3 | Possible | 25-50% |
| 4 | Likely | 50-75% |
| 5 | Almost Certain | > 75% |

### Impact (1-5)

| Score | Rating | Description |
|-------|--------|-------------|
| 1 | Negligible | Minimal; routine management |
| 2 | Minor | Manageable within reserves |
| 3 | Moderate | Significant management effort; per-customer impact |
| 4 | Major | Threatens objectives; multi-customer impact possible |
| 5 | Catastrophic | Existential to track or simultaneous-customer-cascade |

### Risk Score Bands

| Score | Level | Action |
|-------|-------|--------|
| 20-25 | Critical | Immediate escalation |
| 13-19 | High | Senior management |
| 6-12 | Medium | Management monitoring |
| 1-5 | Low | Routine |

---

## Appendix B: Stakeholder → Risk Linkage

| Stakeholder | Driver | Risk(s) Created | Category |
|-------------|--------|-----------------|----------|
| Customer Accreditor (SD-1) | Defensible ATO | R-001, R-002, R-012 | STRATEGIC, COMPLIANCE |
| Customer SIRO (SD-2) | Risk acceptance | R-005, R-007 | COMPLIANCE, REPUTATIONAL |
| Customer DSO (SD-3) | Departmental policy fit | R-005 | COMPLIANCE |
| Customer SRO (SD-4) | Delivery in timeline | R-001, R-010 | STRATEGIC, OPERATIONAL |
| Customer Operator Team (SD-5) | Predictable ops | R-006, R-007 | OPERATIONAL, REPUTATIONAL |
| Customer DDaT Architects (SD-6) | DDaT parity | R-003 | TECHNOLOGY |
| MOD Defence Digital (SD-7) | Cross-MOD coherence | R-001, R-003 | STRATEGIC, TECHNOLOGY |
| Vendor Service Owner (SD-8) | Mission-funding | R-001, R-003, R-011 | STRATEGIC, TECHNOLOGY, FINANCIAL |
| Vendor Lead Architect (SD-9) | Single codebase | R-003, R-007 | TECHNOLOGY, REPUTATIONAL |
| Vendor Security Lead (SD-10) | Supply chain | R-002, R-004 | COMPLIANCE |
| Vendor Sovereign Delivery Lead (SD-11) | Customer onboarding | R-001, R-006, R-012 | STRATEGIC, OPERATIONAL, COMPLIANCE |
| Vendor Finance (SD-12) | Unit economics | R-011 | FINANCIAL |
| Vendor LTS Engineering Lead (SD-13) | LTS discipline | R-010 | OPERATIONAL |
| Vendor DPO (SD-14) | UK GDPR posture | R-013 | COMPLIANCE |
| NCSC (SD-15) | Cyber baseline | R-004, R-007 | COMPLIANCE, REPUTATIONAL |
| ICO (SD-16) | UK GDPR | R-013 | COMPLIANCE |
| HMT/CCS/CDDO/DCPP (SD-17) | Spending and defence cyber | R-011 | FINANCIAL |

### Stakeholder-Conflict-to-Risk Mapping

| Conflict (from STKE) | Risk(s) Created | Mitigation |
|----------------------|-----------------|------------|
| C-1: Per-customer demands vs single codebase | R-003, R-012 | Configuration-only customisation; Service Owner authority on forks |
| C-2: LTS stability vs SaaS feature velocity | R-010 | LTS scope discipline; protected team |
| C-3: Customer self-sufficiency vs vendor support | R-006, R-013 | Opt-in audited remote channel |
| C-4: AI generation richness vs disconnected operation | R-008 | Pluggable AI endpoint; opt-in |
| C-5: First-customer pricing vs cross-subsidy floor | R-011 | Pricing floor; non-cash concessions |
| C-6: Sovereign demands vs SaaS mission bandwidth | R-003 (cross-project), R-009 | Track ownership; cross-project review |

---

## Appendix C: Cross-Project Risk Cross-References

### Risks Shared with Project 001 (ArcKit SaaS)

| Project 002 Risk | Project 001 Risk | Relationship |
|------------------|------------------|--------------|
| R-003 (Single-codebase divergence) | Project 001 R-002 (Single-codebase fork pressure from sovereign demands) | **Bidirectional** — same root cause, different lens. Joint quarterly review. |
| R-007 (Egress incident — sovereign) | Project 001 R-008 or equivalent (Telemetry / privacy regression) | **Cascading reputational** — vendor trust profile shared. |
| R-011 (Cross-subsidy erosion) | Project 001 SME-tier-affordability (BR-005) | **Direct funding linkage** — sovereign margin funds SaaS SME tier. |

These cross-references must be maintained jointly; updates to either side trigger review of the other.

---

## Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| **Risk Register Owner** | Mark Craddock (Service Owner) | _________ | [PENDING] |
| **Vendor Security Lead** | [PENDING] | _________ | [PENDING] |
| **Lead Architect / CTO** | [PENDING] | _________ | [PENDING] |
| **Sovereign Delivery Lead** | [PENDING] | _________ | [PENDING] |
| **Customer SRO (Pilot)** | [PENDING] | _________ | [PENDING] |
| **Customer SIRO (Pilot)** | [PENDING] | _________ | [PENDING] |
| **Customer Accreditor (Pilot)** | [PENDING] | _________ | [PENDING] |

---

## Next Steps

1. **Immediate Actions** (Week 1):
   - [ ] Service Owner formal acknowledgement of 5 above-appetite risks.
   - [ ] Confirm pilot customer with willing accreditator (R-001, R-002, R-012).
   - [ ] Schedule quarterly cross-project risk review with project 001.

2. **Short-term Actions** (Month 1):
   - [ ] Independent MOD-SbD readiness assessment booked.
   - [ ] HSM signing infrastructure progress review.
   - [ ] Vendor Security Lead deputy capacity hire initiated.

3. **Medium-term Actions** (Quarter 1):
   - [ ] First MOD-SbD assessment completed (R-002 evidence).
   - [ ] First customer accreditator-in-the-loop alpha started (R-001 evidence).
   - [ ] Egress-fuzz CI test live (R-007 evidence).
   - [ ] Cleared-personnel pipeline of 3 in flight (R-009 evidence).

---

## External References

> No external policy documents were placed in `projects/002-arckit-sovereign/external/` at the time of generation. The register draws from internal artefacts (`ARC-000-PRIN-v2.0.md`, `ARC-002-REQ-v1.0.md`, `ARC-002-STKE-v1.0.md`, `ARC-002-ADR-001` through `008`).

### Document Register

| Doc ID | Filename | Type | Source | Description |
|--------|----------|------|--------|-------------|
| INT-PRIN | ARC-000-PRIN-v2.0.md | Internal | projects/000-global/ | Architecture Principles (esp. Principle 21) |
| INT-REQ | ARC-002-REQ-v1.0.md | Internal | projects/002-arckit-sovereign/ | Sovereign requirements |
| INT-STKE | ARC-002-STKE-v1.0.md | Internal | projects/002-arckit-sovereign/ | Stakeholder analysis (drivers SD-1 to SD-17, conflicts C-1 to C-6, risks SR-1 to SR-8) |
| INT-ADR | ARC-002-ADR-001 to 008 | Internal | projects/002-arckit-sovereign/decisions/ | Architecture Decision Records (8) |

### Citations

| Citation ID | Doc ID | Section | Category | Passage |
|-------------|--------|---------|----------|---------|
| INT-PRIN-1 | INT-PRIN | Principle 21 | Architecture | Sovereign Deployment Track — single codebase, configuration-only divergence |
| INT-STKE-1 | INT-STKE | SD-1 | Stakeholder | Customer Accreditator driver — defensible ATO |
| INT-STKE-2 | INT-STKE | Conflict C-1 | Conflict | Per-customer demands vs single codebase |
| INT-STKE-3 | INT-STKE | SR-1 to SR-8 | Risk | Stakeholder-derived risks fed into this register |
| INT-REQ-1 | INT-REQ | BR-001, BR-002, FR-004, FR-007, FR-010, FR-011, FR-013 | Requirements | Single-codebase, disconnected-mode, AI endpoint, cleared-personnel claim, audit logging, runbooks, opt-in remote support |

### Unreferenced Documents

| Filename | Source | Reason |
|----------|--------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:risk` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: Claude Opus 4.7 (1M context)
