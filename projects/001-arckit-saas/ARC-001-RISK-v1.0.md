# Risk Register: ArcKit as a Service (Managed SaaS)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:risk`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RISK-v1.0 |
| **Document Type** | Risk Register (HM Treasury Orange Book 2023) |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Weekly (Critical/High) / Monthly (Medium) / Quarterly (Low) |
| **Next Review Date** | 2026-06-03 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner — Risk Register Owner / SRO-equivalent) |
| **Reviewed By** | [PENDING] Lead Architect, Security Lead, DPO |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, CCS liaison, NCSC liaison (post-pilot) |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:risk` command. 17 risks identified across 6 Orange Book categories. Owners drawn from `ARC-001-STKE-v1.0.md` RACI matrix. | [PENDING] | [PENDING] |

---

## Executive Summary

### Risk Profile Overview

**Total Risks Identified:** 17 risks across 6 Orange Book categories

| Risk Level | Inherent | Residual | Change |
|------------|----------|----------|--------|
| **Critical** (20-25) | 2 | 0 | ↓ 100% |
| **High** (13-19) | 3 | 0 | ↓ 100% |
| **Medium** (6-12) | 11 | 11 | — |
| **Low** (1-5) | 1 | 6 | ↑ |
| **TOTAL** | 17 | 17 | — |

### Risk Category Distribution

| Category | Count | Avg Inherent | Avg Residual | Control Effectiveness |
|----------|-------|--------------|--------------|----------------------|
| **STRATEGIC** | 3 | 14.7 | 7.0 | 52% reduction |
| **OPERATIONAL** | 2 | 9.0 | 5.0 | 44% reduction |
| **FINANCIAL** | 2 | 12.0 | 7.5 | 38% reduction |
| **COMPLIANCE** | 4 | 14.5 | 5.8 | 60% reduction |
| **REPUTATIONAL** | 2 | 9.5 | 5.0 | 47% reduction |
| **TECHNOLOGY** | 4 | 12.0 | 5.5 | 54% reduction |

### Overall Risk Assessment

**Overall Inherent Risk Score:** 211 / 425 maximum (50% saturation)
**Overall Residual Risk Score:** 101 / 425 maximum (24% saturation)
**Risk Reduction from Controls:** 52% reduction from inherent risk
**Risk Profile Status:** ⚠️ **Concerning** — 4 COMPLIANCE risks exceed the very-low appetite (≤4) and 1 FINANCIAL risk sits at the appetite ceiling. Project may proceed with explicit acceptance of the residual COMPLIANCE position by the Service Owner (SIRO-equivalent), DPO, and Security Lead, conditional on the priority-1 actions in §H landing before GA.

### Risks Exceeding Appetite

**Number of risks exceeding organisational appetite:** 5 risks (4 COMPLIANCE + 1 REPUTATIONAL at threshold)

| Risk ID | Title | Category | Residual | Appetite | Excess | Escalation |
|---------|-------|----------|----------|----------|--------|------------|
| R-008 | Cross-tenant data leakage (existential) | COMPLIANCE | 5 | 4 | +1 | DPO + SIRO acceptance; ICO posture review |
| R-009 | GDS Service Assessment failure | COMPLIANCE | 6 | 4 | +2 | Service Owner acceptance; pilot evidence pack |
| R-010 | AI Playbook scope drift (ATRS / transparency) | COMPLIANCE | 6 | 4 | +2 | Service Owner + DPO acceptance |
| R-011 | UK GDPR breach via AI sub-processor | COMPLIANCE | 6 | 4 | +2 | DPO acceptance; quarterly sub-processor review |
| R-013 | SME failure visibly attributed to ArcKit artefact | REPUTATIONAL | 6 | 6 | 0 | At threshold — monitor |

### Top 5 Risks Requiring Immediate Attention (by inherent score, then residual)

1. **R-008** (COMPLIANCE, Inherent 25 / Residual 5): Cross-tenant data leakage — Owner: Service Owner (SIRO-equivalent) — Status: In Progress (defence-in-depth from ADR-001)
2. **R-014** (TECHNOLOGY, Inherent 20 / Residual 8): Tenant isolation defect (ADR-001) — Owner: Lead Architect — Status: In Progress (CI tenant-isolation tests, NFR-SEC-002)
3. **R-001** (STRATEGIC, Inherent 16 / Residual 9): Cross-subsidy break-even fails by GA+18m — Owner: Service Owner with Finance Lead — Status: In Progress
4. **R-002** (STRATEGIC, Inherent 16 / Residual 6): MOD sovereign-route divergence (codebase fork) — Owner: Lead Architect — Status: In Progress (Principle 21 enforcement)
5. **R-009** (COMPLIANCE, Inherent 12 / Residual 6): GDS Service Assessment failure blocks G-Cloud listing — Owner: Service Owner with CCS liaison — Status: Open

### Key Findings

- **Compliance risks dominate the residual profile**: 4 of 5 risks exceeding appetite are COMPLIANCE. UK Government's very-low appetite for compliance breach is hard to satisfy with a multi-tenant AI-touching SaaS. Acceptance, not further mitigation, is the realistic path for the 1-2 point excesses.
- **Tenant-isolation defence-in-depth is doing the heavy lifting**: R-008 (the existential cross-tenant leak) drops from 25 to 5 because of layered controls — namespace isolation (ADR-001), CI isolation tests (NFR-SEC-002), default-deny network policy, signed-immutable audit log, bulkhead patterns. Loss of any one layer would push residual back into critical territory.
- **Vendor concentration on AI and managed K8s carries through**: R-015 (K8s lock-in, ADR-006) and R-017 (AI provider, ADR-004) both rely on portability ADRs that are credible on paper but have not yet been exercised. Quarterly portability rehearsals are the load-bearing control.
- **MOD sovereign-route divergence (R-002) is uniquely strategic**: Principle 21 (single codebase, two deployment routes) is a binding architectural constraint — not advisory. The risk is high inherent, well controlled, but requires continuous engineering discipline.
- **Department / pilot escalation overload (R-004) is the most likely operational failure mode pre-GA**. A small vendor team facing requests from three pilot DDaT functions will be tempted to fork features per pilot. Product Manager + Service Owner gating is the fix.

### Recommendations

1. **Before GA**: Complete the priority-1 actions in §H — independent pen test (R-008/R-014), pluggability rehearsal on alt cloud profile (R-015), AI provider failover drill (R-017), pilot evidence pack walk-through with one buying-authority Service Assessor (R-009).
2. **At GA**: Service Owner to formally accept residual position on R-008, R-009, R-010, R-011 with DPO + Security Lead countersignature. Capture in `ARC-001-SbD-v1.0.md` (Secure by Design) and `ARC-001-DPIA-v1.0.md`.
3. **Continuously**: Weekly steering review for R-008 and R-014; monthly review of cross-subsidy KRIs feeding R-001 and R-006; quarterly portability rehearsal for R-015 / R-017.

---

## A. Risk Matrix Visualisation

### Inherent Risk Matrix (Before Controls)

```text
                                    IMPACT
              1-Negligible 2-Minor    3-Moderate   4-Major    5-Catastrophic
           ┌───────────┬───────────┬───────────┬───────────┬───────────┐
5-Almost   │           │           │           │           │   R-008   │
Certain    │    5      │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │ R-006     │  R-001    │   R-014   │
           │           │           │ R-007     │  R-002    │           │
           │    4      │    8      │ R-004 12  │    16     │    20     │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 3-Possible│          │           │ R-013     │ R-003     │           │
K          │           │           │ R-015     │ R-009     │           │
E          │           │           │ R-017 9   │ R-010 12  │           │
L          │    3      │    6      │ R-011 9   │    12     │    15     │
I          ├───────────┼───────────┼───────────┼───────────┼───────────┤
H 2-Unlikely│          │   R-005   │           │           │   R-012   │
O          │           │           │           │           │   R-016   │
O          │    2      │    4      │    6      │    8      │    10     │
D          ├───────────┼───────────┼───────────┼───────────┼───────────┤
  1-Rare   │           │           │           │           │           │
           │    1      │    2      │    3      │    4      │    5      │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: ██ Critical (20-25)  ▓▓ High (13-19)  ░░ Medium (6-12)  ·· Low (1-5)
```

**Inherent Risk Zones:**

- **Critical (20-25)**: R-008, R-014 — cross-tenant leak, isolation defect
- **High (13-19)**: R-001, R-002, R-003 — strategic / cross-subsidy / DDaT recognition
- **Medium (6-12)**: R-004, R-005, R-006, R-007, R-009, R-010, R-011, R-012, R-013, R-015, R-016, R-017
- **Low (1-5)**: None at inherent

### Residual Risk Matrix (After Controls)

```text
                                    IMPACT
              1-Negligible 2-Minor    3-Moderate   4-Major    5-Catastrophic
           ┌───────────┬───────────┬───────────┬───────────┬───────────┐
5-Almost   │           │           │           │           │           │
Certain    │    5      │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │           │           │           │
           │    4      │    8      │    12     │    16     │    20     │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 3-Possible│          │   R-007   │   R-001   │           │           │
K          │           │           │   R-006   │           │           │
E          │    3      │    6      │    9      │    12     │    15     │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 2-Unlikely│          │ R-004     │ R-002     │  R-014    │           │
H          │           │ R-005 4   │ R-009     │           │           │
O          │           │ R-013     │ R-010     │           │           │
O          │    2      │ R-017 4   │ R-003 6   │    8      │    10     │
D          │           │           │ R-011     │           │           │
           │           │           │ R-015 6   │           │           │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
  1-Rare   │           │           │           │ R-012     │   R-008   │
           │           │           │           │ R-016 4   │    5      │
           │    1      │    2      │    3      │    4      │    5      │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: ██ Critical (20-25)  ▓▓ High (13-19)  ░░ Medium (6-12)  ·· Low (1-5)
```

**Risk Movement Analysis:**

- **Existential controlled**: R-008 (25→5) and R-014 (20→8) — defence-in-depth working as designed; control degradation = immediate critical risk return.
- **Strategic controlled**: R-001 (16→9), R-002 (16→6), R-003 (12→6) — process and engineering controls reducing risk to Medium / Low.
- **Compliance compressed but still over appetite**: R-009 (12→6), R-010 (9→6), R-011 (9→6), R-008 (25→5) — all sit 1-2 points above the very-low compliance appetite.
- **Vendor concentration partially mitigated**: R-015 (9→6), R-017 (9→4) — pluggability ADRs drop the residual but require live rehearsal.

---

## B. Top 10 Risks (Ranked by Residual Score, then Inherent)

| Rank | ID | Title | Category | Inherent | Residual | Owner | Status | Response |
|------|----|-------|----------|----------|----------|-------|--------|----------|
| 1 | R-001 | Cross-subsidy break-even fails | STRATEGIC | 16 | 9 | Service Owner | In Progress | Treat |
| 2 | R-006 | AI inference cost overrun | FINANCIAL | 12 | 9 | Finance Lead | In Progress | Treat |
| 3 | R-014 | Tenant isolation defect (ADR-001) | TECHNOLOGY | 20 | 8 | Lead Architect | In Progress | Treat |
| 4 | R-002 | MOD sovereign-route divergence | STRATEGIC | 16 | 6 | Lead Architect | In Progress | Treat |
| 5 | R-003 | DDaT pilot recognition failure | STRATEGIC | 12 | 6 | Service Owner | In Progress | Treat |
| 6 | R-009 | GDS Service Assessment failure | COMPLIANCE | 12 | 6 | Service Owner | Open | Treat |
| 7 | R-010 | AI Playbook scope drift | COMPLIANCE | 9 | 6 | DPO | Open | Treat |
| 8 | R-011 | UK GDPR breach via AI sub-processor | COMPLIANCE | 9 | 6 | DPO | In Progress | Treat |
| 9 | R-013 | SME failure attributed to ArcKit | REPUTATIONAL | 9 | 6 | Service Owner | Open | Treat |
| 10 | R-015 | Managed K8s vendor lock-in (ADR-006) | TECHNOLOGY | 9 | 6 | Lead Architect | In Progress | Treat |

---

## C. Detailed Risk Register

### Risk R-001: Cross-Subsidy Break-Even Fails by GA + 18 Months

**Category:** STRATEGIC
**Status:** In Progress
**Risk Owner:** Mark Craddock, Service Owner (RACI: Accountable for go/no-go and pricing)
**Action Owner:** Finance Lead (vendor)

#### Risk Identification

**Risk Description:** Aggregate revenue from large-enterprise and paid-SME tenants does not reach the cost-to-serve floor for the SME free tier within 18 months of GA, undermining Goal G-3 and threatening the Principle-1 commitment that gives the platform its strategic reason to exist.

**Root Cause:** Cross-subsidy depends on three independent variables — enterprise sales velocity, SME free-tier cost trajectory (driven mostly by AI inference cost — see R-006), and free-tier abuse rate (R-007). All three carry forecast error.

**Trigger Events:**

- Enterprise sales pipeline below quarterly target for 2 consecutive quarters
- AI inference cost per active SME tenant runs > 15% above forecast band for 2 consecutive months
- Free-tier abuse rate (synthetic / non-SME accounts) > 5% of registered tenants

**Consequences if Realised:**

- Forced to paywall governance-critical features → breaks Principle 1 → mission failure
- Commercial restructure / external runway request to sponsor
- Reputational damage among the SME audience (the platform's reason for existing)

**Affected Stakeholders:**

- **Service Owner (Mark Craddock)** (`ARC-001-STKE-v1.0.md` SD-8): Mission collapse
- **HM Treasury / CCS / CDDO** (SD-13): SME-spend strategic alignment loses delivery vehicle
- **All SME tenants** (SD-6, SD-7): Free / cheap access withdrawn

**Related Objectives:**

- Goal G-3 (Cross-subsidy break-even) — directly threatened
- Outcome O-3 (Sustainable cross-subsidy economics) — directly threatened

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | Cross-subsidy SaaS models routinely miss the first break-even window; multiple unknowns compound |
| **Impact** | 4 - Major | Forces violation of Principle 1; existential for SME tier |
| **Inherent Risk Score** | **16** (High) | 4 × 4 = 16 |

#### Current Controls and Mitigations

1. **Quarterly affordability review** (Principle 17, NFR-FIN-001) — Owner: Service Owner with Finance Lead — Effectiveness: **Adequate** — Evidence: cadence in `ARC-000-PRIN-v2.0.md`.
2. **FinOps tagging by tenant tier** (Principle 17) — Owner: SRE Lead — Effectiveness: **Adequate** — provides per-tier cost-to-serve telemetry.
3. **AI cost lever (Conflict C-1 resolution)** — Owner: Product Manager — Effectiveness: **Adequate** — quotas can be tuned annually without paywalling features.
4. **Pluggable AI provider abstraction (ADR-004)** — Owner: Lead Architect — Effectiveness: **Strong** — protects against single-provider price shock.

**Overall Control Effectiveness:** Adequate — reduces from 16 to 9 (Medium).

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | With telemetry and quarterly review, drift is detected before threshold |
| **Impact** | 3 - Moderate | Quotas can flex without paywalling features |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

**Risk Reduction:** 44% (16 → 9).

#### Risk Response (4Ts)

**Primary Response:** TREAT — controls are effective and proportionate; further mitigation is in §H.

**Risk Appetite Assessment:** STRATEGIC appetite Medium (≤12). Residual 9 — **Within Appetite**. No escalation required.

#### Action Plan

- Pre-GA enterprise pipeline target: 5 paying enterprise tenants signed (Service Owner + Sales)
- AI inference cost forecast band locked at GA, reviewed monthly (Finance + Lead Architect)
- Free-tier abuse detection and remediation runbook (Product + SRE) — see R-007

**Target Residual:** 9 (Medium) — already at target.

---

### Risk R-002: MOD Sovereign-Route Codebase Divergence

**Category:** STRATEGIC
**Status:** In Progress
**Risk Owner:** Lead Architect (RACI: Accountable for architecture decisions)
**Action Owner:** Lead Architect

#### Risk Identification

**Risk Description:** Time-pressured feature work for SaaS tenants introduces dependencies (managed services, SaaS-only APIs, untracked configuration drift) that cannot be replicated in the sovereign / air-gapped deployment route, forcing a codebase fork between Project 001 (SaaS) and Project 002 (Sovereign) and breaking Principle 21 (Sovereign-Ready Packaging).

**Root Cause:** Principle 21 is binding but the sovereign team is downstream of SaaS feature delivery. Without explicit gates, expedient SaaS-only choices accumulate.

**Trigger Events:**

- Sovereign smoke-test pipeline fails for 3+ consecutive SaaS releases
- Any ADR for a SaaS feature that does not document sovereign-route impact
- A managed cloud service introduced without a documented air-gapped substitute

**Consequences if Realised:**

- Project 002 (Sovereign) blocked / delayed
- Principle 21 violated — breaks the dual-deployment commitment
- MOD opportunity lost; sovereign-business-case erosion

**Affected Stakeholders:**

- **Vendor Lead Architect** (SD-9), **Service Owner** (SD-8)
- Project 002 stakeholders (cross-reference `projects/002-arckit-sovereign/ARC-002-STKE-v1.0.md`)
- MOD prospective tenants

**Related Objectives:**

- Principle 21 (single codebase, two deployment routes)
- Project 002 strategic delivery

#### Inherent Risk Assessment

| | Rating | Justification |
|--|--|--|
| **Likelihood** | 4 - Likely | SaaS / sovereign codebase divergence is the historical default for products that try this dual model |
| **Impact** | 4 - Major | Project 002 blocked; Principle 21 violated |
| **Inherent Score** | **16** (High) | |

#### Current Controls

1. **Principle 21 explicit in `ARC-000-PRIN-v2.0.md`** — Strong (governance gate at ADR review)
2. **ADR-006 (Deployment Topology) requires sovereign-profile parity** — Strong
3. **CI smoke test on sovereign profile per release** — Adequate (when implemented; see action below)
4. **Cross-project ADR review** — Adequate

**Overall Effectiveness:** Strong — reduces 16 → 6.

#### Residual Risk Assessment

| | Rating | Justification |
|--|--|--|
| **Likelihood** | 2 - Unlikely | CI parity gate + ADR review catch most drift |
| **Impact** | 3 - Moderate | If detected, recoverable within a release cycle |
| **Residual Score** | **6** (Medium) | |

#### Risk Response

**TREAT** — sovereign-CI smoke gate must be live before GA.

**Appetite Assessment:** STRATEGIC ≤12. Residual 6 — **Within Appetite**.

#### Action Plan

- Implement sovereign-profile CI smoke pipeline before GA (Lead Architect, due GA – 60 days)
- Add "sovereign impact" mandatory section to ADR template for project 001 (Lead Architect, due 2026-06-30)
- Quarterly cross-project architecture forum (Lead Architect)

**Target Residual:** 6 (Medium).

---

### Risk R-003: DDaT Pilot Recognition Failure (Goal G-1)

**Category:** STRATEGIC
**Status:** In Progress
**Risk Owner:** Service Owner
**Action Owner:** Product Manager

#### Risk Identification

**Risk Description:** Pilot buying-authority DDaT architects (≥3 required by Goal G-1) reject ArcKit-produced artefacts as not credible without bespoke verification, undermining the central buyer-side value proposition.

**Root Cause:** Format conventions, AI-content lineage, or quality variance fall outside what Enterprise / Solution / Security Architects in mature departments expect.

**Trigger Events:** Pilot review reports flag ≥3 substantive format / quality issues per pack; pilot reviewer requests bespoke document set; alpha / beta feedback indicates AI-content not traceable to project context.

**Consequences if Realised:** GA delayed; format-change release required; SME-side value proposition reduced.

**Affected Stakeholders:** SD-1, SD-2, SD-3, SD-4, SD-5 (DDaT architects); SD-6, SD-7 (SMEs whose pitch hinges on artefact credibility).

**Related Objectives:** G-1, O-1.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 3 | 4 | 12 (Medium) |
| Residual | 2 | 3 | 6 (Medium) |

#### Current Controls

- Alpha + private beta cycles with at least one buying-authority EA in the loop (per STKE Risk SR-1)
- AI-content lineage metadata mandatory (FR-004)
- ADR alternatives-and-consequences sections enforced by template
- Quarterly DDaT user group post-GA

**TREAT.** Within appetite (STRATEGIC ≤12). Action: pre-pilot evidence pack walkthrough with one Service Assessor + one pilot DDaT EA.

---

### Risk R-004: Department / Pilot Escalation Overload

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** Product Manager
**Action Owner:** Product Manager with Service Owner

#### Risk Identification

**Risk Description:** Three pilot DDaT architecture functions request bespoke features in parallel (departmental templates, lineage to local standards, custom evidence formats), overwhelming the small vendor team and driving codebase fragmentation across pilot tenants. The "manage closely" engagement strategy in `ARC-001-STKE-v1.0.md` for pilot DDaT EAs / SAs / SecAs creates a real-but-bounded escalation channel that must be triaged.

**Root Cause:** Conflict 4 in STKE — buyer-side feature demand (deep) vs SME-side feature demand (broad and simple). Without a strict gate, expedient bespoke work crowds out core SME-tier delivery.

**Trigger Events:** > 3 bespoke-feature requests per pilot per month; pilot-driven release content > 30% of any release; pilot tenant requesting source-controlled fork for departmental adaptation.

**Consequences:** SME-tier delivery slowed; quality variance across pilots; engineering morale risk.

**Affected Stakeholders:** Vendor PM / Lead Architect / Delivery Manager / SREs; SD-6 SMEs (deferred features).

**Related Objectives:** G-2 (5-day pack), Conflict 4 resolution (Principle 1).

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 4 | 3 | 12 (Medium) |
| Residual | 2 | 2 | 4 (Low) |

#### Current Controls

- Conflict 4 resolution in STKE (strict baseline-features-on-free-tier line)
- Product Manager + Service Owner gating on bespoke pilot work
- Pilot acceptance criteria defined in pilot MoU
- Roadmap published in advance per release

**TREAT / partial TOLERATE.** Within OPERATIONAL appetite (≤6).

---

### Risk R-005: SME Onboarding Brittleness (Companies House Dependency)

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** Product Manager
**Action Owner:** Lead Architect (integration design)

#### Risk Identification

**Risk Description:** Companies House API change or outage breaks SME-eligibility verification, blocking new free-tier sign-ups (BR-001 / Conflict C-3 in STKE).

**Trigger Events:** Companies House schema change without notice; rate-limit reduction; outage > 4 hours.

**Consequences:** Sign-up funnel halt; pilot embarrassment; SME-trust erosion.

**Affected Stakeholders:** SD-7 (SME founder), SD-8 (Service Owner), SD-13 (CCS).

**Related Objectives:** G-2.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 2 | 3 | 6 (Medium) |
| Residual | 2 | 2 | 4 (Low) |

#### Current Controls

- Defensive parsing (Conflict C-3 resolution)
- Provisional access on outage with manual verification fallback (24 h SLA)
- API change-notice mailing list subscription
- Status-page entry for verification subsystem

**TREAT.** Within OPERATIONAL appetite.

---

### Risk R-006: AI Inference Cost Overrun (FinOps)

**Category:** FINANCIAL
**Status:** In Progress
**Risk Owner:** Finance Lead
**Action Owner:** Lead Architect

#### Risk Identification

**Risk Description:** Aggregate AI inference cost per active SME tenant exceeds forecast by > 25% over a quarter, eroding cross-subsidy headroom (links to R-001) and threatening Goal G-3.

**Root Cause:** AI usage patterns highly variable per tenant; provider price changes; abuse of free-tier generation features.

**Trigger Events:** Per-tenant inference token consumption > 2× median for > 5% of tenants; provider list-price increase; new model variant required for quality.

**Consequences:** Cross-subsidy slips; quarterly affordability review prompts quota tightening (not paywalling).

**Affected Stakeholders:** SD-8 (Service Owner), SD-9 (Lead Architect), SD-11 (DPO if provider change required), SD-13 (HMG VFM narrative).

**Related Objectives:** G-3, Outcome O-3.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 4 | 3 | 12 (Medium) |
| Residual | 3 | 3 | 9 (Medium) |

#### Current Controls

- ADR-004 pluggable AI provider abstraction — Strong
- ADR-008 per-tenant quotas, rate limits, fair-use — Strong
- FinOps tagging per tenant tier (Principle 17) — Adequate
- Quarterly CI alternative-provider validation (Goal G-8) — Adequate

**TREAT.** Sits at FINANCIAL appetite ceiling (≤9) — **At Appetite**. Acceptance with monthly KRI monitoring.

---

### Risk R-007: Free-Tier Abuse (Cost-to-Serve Blow-Out)

**Category:** FINANCIAL
**Status:** Open
**Risk Owner:** Finance Lead
**Action Owner:** Product Manager

#### Risk Identification

**Risk Description:** Non-SME accounts (synthetic shells, non-UK SMEs, sole-traders gaming Companies House data) consume free-tier AI generation disproportionately, inflating cost-to-serve and eroding cross-subsidy headroom.

**Trigger Events:** Verified-SME share < 90% of free-tier active accounts; aggregate free-tier AI spend > forecast for 2 consecutive months.

**Consequences:** Cross-subsidy slippage (R-001 cascading).

**Affected Stakeholders:** SD-7, SD-8, SD-13, vendor Finance.

**Related Objectives:** G-2, G-3.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 4 | 3 | 12 (Medium) |
| Residual | 3 | 2 | 6 (Medium) |

#### Current Controls

- Companies House verification on sign-up (FR-002)
- ADR-008 per-tenant quotas, rate limits, fair-use
- Anomaly detection on per-tenant AI consumption (SRE)
- Audit-retention of verification artefacts
- Periodic re-verification on tenancy renewal

**TREAT.** Within FINANCIAL appetite (≤9).

---

### Risk R-008: Cross-Tenant Data Leakage (Existential)

**Category:** COMPLIANCE
**Status:** In Progress
**Risk Owner:** Mark Craddock, Service Owner (SIRO-equivalent — RACI: Accountable for security control acceptance)
**Action Owner:** Security Lead and Lead Architect

#### Risk Identification

**Risk Description:** A defect, mis-configuration, or operator error causes one tenant's OFFICIAL / OFFICIAL-SENSITIVE data — including draft architecture artefacts, requirements, and stakeholder analysis — to be visible or retrievable by another tenant. Materialised, this triggers ICO notification (within 72 hours), potential enforcement action under UK GDPR / DPA 2018, and existential reputational damage to the SME-trust mission.

**Root Cause:** Multi-tenancy is a single high-blast-radius failure mode away from existential damage (per STKE SD-10). Layered isolation is essential because any one layer can fail.

**Trigger Events:** CI tenant-isolation test failure; pen-test finding showing cross-tenant retrieval; tenant-reported visibility of foreign content; audit-log anomaly (tenant ID mismatch on access).

**Consequences if Realised:**

- ICO breach notification within 72 h; potential monetary penalty
- Mass tenant exodus; mission failure (Principle 1 unrecoverable in practice)
- Public coverage; parliamentary questions; G-Cloud listing review
- Civil liability to affected tenants

**Affected Stakeholders:** All — every tenant, ICO, NCSC, GDS, CCS, and the SME ecosystem.

**Related Objectives:** Goal G-4, Goal G-5, Outcome O-4.

#### Inherent Risk Assessment

| | Rating | Justification |
|--|--|--|
| **Likelihood** | 5 - Almost Certain (without controls) | Multi-tenant SaaS with no isolation defence-in-depth ≈ inevitable |
| **Impact** | 5 - Catastrophic | ICO action; existential reputational damage; mission failure |
| **Inherent Score** | **25** (Critical) | 5 × 5 |

#### Current Controls (Defence in Depth)

1. **Namespace-per-tenant isolation (ADR-001)** — Strong — Owner: Lead Architect
2. **Default-deny network policy (ADR-006)** — Strong — Owner: SRE
3. **Tenant-ID enforcement at every data access boundary** (NFR-SEC-002) — Strong — Owner: Lead Architect
4. **CI tenant-isolation tests on every PR** — Strong — fail-closed
5. **Signed, immutable per-tenant audit log (ADR-005)** — Strong — Owner: Security Lead
6. **Bulkhead patterns on shared-service paths (ADR-003 / ADR-004)** — Adequate
7. **Annual independent pen test (Goal G-4)** — Strong
8. **Vulnerability disclosure programme** — Adequate

**Overall Effectiveness:** Strong — reduces 25 → 5.

#### Residual Risk Assessment

| | Rating | Justification |
|--|--|--|
| **Likelihood** | 1 - Rare | Defence-in-depth requires multi-layer failure |
| **Impact** | 5 - Catastrophic | Impact is inherent — controls reduce likelihood, not impact |
| **Residual Score** | **5** (Low) | 1 × 5 |

**Risk Reduction:** 80% (25 → 5).

#### Risk Response

**TREAT** primary; **TRANSFER** secondary (cyber liability insurance, SD-10 contingency).

**Appetite Assessment:** COMPLIANCE appetite Very Low (≤4). Residual 5 — **Exceeds Appetite by 1 point** owing to the Catastrophic-impact floor. Acceptance is the only realistic path because impact cannot be reduced — likelihood is already at the lowest score.

**Escalation Required:** Yes — formal acceptance by Service Owner (SIRO-equivalent), DPO, and Security Lead before GA. Recorded in `ARC-001-SbD-v1.0.md` Secure-by-Design assessment.

#### Action Plan

- Pre-GA independent pen test specifically targeting tenant isolation (Security Lead, due GA – 60 days, ~ £40k–£60k)
- Tenant-isolation test coverage report published quarterly to Security Forum (Lead Architect)
- Bulkhead pattern review per ADR-003 / ADR-004 (Lead Architect, due 2026-07-31)
- Cyber liability insurance procured at GA (Service Owner with Finance, transfer secondary)
- Incident runbook with ICO-72h-notification template (DPO, due GA – 30 days)

**Target Residual:** 5 (Low) — already at floor; objective is to maintain.

#### Monitoring

- Weekly review by Service Owner + Security Lead until GA, monthly thereafter
- KRIs: CI isolation-test pass rate (must be 100%); audit-log anomalies; pen-test residual findings

---

### Risk R-009: GDS Service Assessment Failure → G-Cloud Listing Blocked

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** Service Owner
**Action Owner:** Product Manager with CCS liaison

#### Risk Identification

**Risk Description:** ArcKit as a Service fails to pass a GDS / CDDO Service Standard assessment at Alpha or Beta gate, blocking G-Cloud listing (BR-004) and therefore the planned procurement reach (Goal G-7, Outcome O-5).

**Root Cause:** Service Standard 14-point assessment is comprehensive; common failure points are user research breadth (point 1), accessibility (point 5), continuity / observability (point 12), and team capability (point 4). A small vendor team can underweight any of these.

**Trigger Events:** Internal pre-assessment scoring < 70%; pilot DDaT review highlights a Standard-aligned gap; accessibility regression discovered in CI.

**Consequences:** G-Cloud listing delay (cascades to O-5); pilot momentum lost; SME audience reach significantly reduced.

**Affected Stakeholders:** SD-13 (HMG SME spend), SD-14 (GDS), SD-7 (SME founder).

**Related Objectives:** G-7, O-5.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 3 | 4 | 12 (Medium) |
| Residual | 2 | 3 | 6 (Medium) |

#### Current Controls

- Pre-assessment with `/arckit:service-assessment` skill (existing tooling)
- WCAG 2.2 AA in CI (NFR-A-001) — point 5 covered
- Accessibility Statement maintained — point 5
- User research panel (DDaT EA / SA / SecA + SME architects) — point 1
- Multi-region observability (ADR-005) — point 12
- AI Playbook compliance (cross-reference R-010) — point 6

**TREAT.** **Exceeds COMPLIANCE appetite (≤4) by 2.** Acceptance required from Service Owner — pre-assessment pack to be walked through with one Service Assessor + one pilot DDaT EA before booking the formal review.

---

### Risk R-010: AI Playbook Scope Drift / Algorithmic Transparency Gap

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** DPO
**Action Owner:** Product Manager

#### Risk Identification

**Risk Description:** ArcKit AI-assisted artefact generation (FR-004) crosses the threshold into UK Government AI Playbook scope without adequate algorithmic-transparency, ATRS (Algorithmic Transparency Recording Standard) registration, or Article 22 GDPR safeguards. This becomes more likely as AI features evolve from "drafting assistance" to "decision support" without an explicit boundary review.

**Root Cause:** Feature drift from drafting (clearly non-decisional) toward recommendation surfaces (e.g., "this ADR option is preferred") without DPIA refresh.

**Trigger Events:** AI surface that recommends among options; AI surface that scores or prioritises requirements; AI surface used by a buyer-side reviewer to triage suppliers.

**Consequences:** ICO concern; AI Playbook non-compliance public-sector signal; ATRS retrofit required; potential pause in feature roll-out.

**Affected Stakeholders:** DPO, Service Owner, Lead Architect, ICO, CDDO.

**Related Objectives:** G-1 (artefact credibility), G-5 (UK GDPR posture).

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 3 | 3 | 9 (Medium) |
| Residual | 2 | 3 | 6 (Medium) |

#### Current Controls

- AI-content lineage metadata mandatory (FR-004) — distinguishes generated vs human content
- DPIA with explicit AI-processing scope (ARC-001-DPIA, when generated)
- AI Playbook assessment via `/arckit:ai-playbook` skill at each major AI feature change
- ATRS register entry maintained
- Article 22 statement that AI does not perform solely-automated decisions of legal / significant effect on tenants

**TREAT.** **Exceeds COMPLIANCE appetite by 2.** Acceptance + quarterly DPO review.

#### Action Plan

- Define AI feature-scope boundary explicitly (DPO + Lead Architect, due 2026-07-31): drafting OK, recommendation requires DPIA refresh + ATRS update
- ATRS record published before any recommendation-class AI surface ships
- Quarterly `/arckit:ai-playbook` re-run

---

### Risk R-011: UK GDPR Breach via AI Sub-Processor

**Category:** COMPLIANCE
**Status:** In Progress
**Risk Owner:** DPO
**Action Owner:** DPO with Lead Architect

#### Risk Identification

**Risk Description:** Selected AI provider (sub-processor under UK GDPR / DPA 2018) materially changes terms — training-on-customer-data flag flipped, residency change, sub-processor chain expansion — without notice, breaching tenant DPA terms and triggering ICO interest.

**Trigger Events:** Provider terms change; residency change; new sub-processor introduced upstream of provider; provider security incident.

**Consequences:** Tenant DPA breach; ICO notification; sub-processor switch within 5 working days (Goal G-8 / Outcome O-7).

**Affected Stakeholders:** DPO, Service Owner, Lead Architect, ICO, all tenants.

**Related Objectives:** G-5, G-8, O-4, O-7.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 3 | 3 | 9 (Medium) |
| Residual | 2 | 3 | 6 (Medium) |

#### Current Controls

- Tenant DPA + sub-processor list maintained (FR-002, BR-006)
- AI-provider no-training assurance + Article 46 transfer mechanism (where applicable)
- Quarterly sub-processor review (DPO)
- Pluggable provider abstraction (ADR-004) — ≤ 5 working days switch
- Tenant-facing 30-day sub-processor change notice

**TREAT.** **Exceeds COMPLIANCE appetite by 2.** Acceptance + quarterly review.

---

### Risk R-012: Cross-Tenant Trust Collapse (Reputational)

**Category:** REPUTATIONAL
**Status:** Open
**Risk Owner:** Service Owner
**Action Owner:** Service Owner with Communications

#### Risk Identification

**Risk Description:** Even a contained or near-miss security incident becomes public (vulnerability disclosure programme, media, parliamentary question) and trust in multi-tenant ArcKit collapses for the SME audience whose mission-trust is the platform's reason for existing. Distinct from R-008 — this risk is the *narrative* failure mode independent of whether actual data was lost.

**Trigger Events:** Vulnerability disclosure published; near-miss incident leaks via tenant; media or LinkedIn coverage of architecture risk.

**Consequences:** SME-tenant churn; pilot tenant withdrawal; SME-spend strategic narrative damaged.

**Affected Stakeholders:** Service Owner, all SMEs, SD-13 HMG.

**Related Objectives:** Outcome O-1, O-2.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 2 | 5 | 10 (Medium) |
| Residual | 1 | 4 | 4 (Low) |

#### Current Controls

- Vulnerability disclosure programme with coordinated disclosure
- Incident communications template (transparent post-incident review)
- No-blame post-incident reviews shared publicly (Principle 19)
- Pre-prepared ICO 72-h notification template
- Pilot-tenant communications channel for early signal

**TREAT.** Within REPUTATIONAL appetite (≤6).

---

### Risk R-013: SME Failure Visibly Attributed to ArcKit-Produced Artefact

**Category:** REPUTATIONAL
**Status:** Open
**Risk Owner:** Service Owner
**Action Owner:** Product Manager

#### Risk Identification

**Risk Description:** A high-profile SME bid or in-flight delivery fails on the buyer side, and a DDaT architect publicly attributes the failure to weak ArcKit-produced governance evidence (drift, AI-generic content, missing traceability). Damages G-1 narrative.

**Trigger Events:** Pilot-attached failure; LinkedIn / GovCamp public criticism; CDDO / GDS internal note flagging artefact quality.

**Consequences:** Buyer-side trust erosion; SME-side participation decline.

**Affected Stakeholders:** Service Owner, SD-1 to SD-5 buyer architects, SD-6 / SD-7 SMEs, SD-14 GDS.

**Related Objectives:** G-1, O-1.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 3 | 3 | 9 (Medium) |
| Residual | 2 | 3 | 6 (Medium) |

#### Current Controls

- AI-content lineage labelling (FR-004) — clearly flags generated content
- Quality validation gates per ArcKit skill output (template-built-in)
- Pilot-feedback loop pre-GA
- Public examples / case studies showing well-completed packs
- Quarterly DDaT user group post-GA

**TREAT.** At REPUTATIONAL appetite (≤6) — **At Appetite**, monitor.

---

### Risk R-014: Tenant Isolation Defect (ADR-001)

**Category:** TECHNOLOGY
**Status:** In Progress
**Risk Owner:** Lead Architect
**Action Owner:** Lead Architect

#### Risk Identification

**Risk Description:** A code-level defect in the tenant-isolation enforcement (namespace separation, tenant-ID propagation, RBAC) creates a path for cross-tenant access despite the layered controls of ADR-001. This is the technology-level twin of R-008 — R-008 expresses the *outcome* (data leakage), R-014 expresses the *cause* (engineering defect).

**Root Cause:** Tenant-ID enforcement requires every developer on every change to think about it. Single missed enforcement point = breach surface.

**Trigger Events:** CI tenant-isolation test failure; pen-test finding; code-review escape.

**Consequences:** Same as R-008 if exploited.

**Affected Stakeholders:** Lead Architect, Security Lead, all engineering, all tenants.

**Related Objectives:** G-4, NFR-SEC-002.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 4 | 5 | 20 (Critical) |
| Residual | 2 | 4 | 8 (Medium) |

#### Current Controls

- ADR-001 namespace-per-tenant model — Strong
- CI tenant-isolation test suite on every PR — Strong (fail-closed)
- Mandatory code review with security-aware checklist — Adequate
- Annual independent pen test — Strong
- Static analysis for tenant-ID propagation patterns — Adequate
- Default-deny network policy at namespace boundary — Strong

**TREAT.** Within TECHNOLOGY appetite (≤9). Linked to R-008 mitigation.

---

### Risk R-015: Managed K8s Vendor Lock-In (ADR-006)

**Category:** TECHNOLOGY
**Status:** In Progress
**Risk Owner:** Lead Architect
**Action Owner:** Lead Architect with SRE Lead

#### Risk Identification

**Risk Description:** Despite ADR-006's commitment to OCI-standard containers and GitOps, accumulated dependence on a managed K8s provider's value-added features (proprietary load-balancer behaviours, vendor-specific operators, IAM-integrated service mesh) makes provider switching expensive and slow, undermining the sovereign-route portability claim (Principle 21) and exposing to provider price / posture changes.

**Trigger Events:** ADRs introducing vendor-specific operators without portable substitute; SRE runbooks dependent on vendor-only CLI / console; sovereign-profile CI gap.

**Consequences:** Cost lever lost; sovereign-route divergence (cascades to R-002); negotiating leverage with provider lost.

**Affected Stakeholders:** Lead Architect, Service Owner, Project 002 stakeholders.

**Related Objectives:** Principle 21, ADR-006 portability commitment.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 3 | 3 | 9 (Medium) |
| Residual | 2 | 3 | 6 (Medium) |

#### Current Controls

- ADR-006 mandates OCI-standard containers and GitOps from day one
- IaC across cloud-portable abstractions (no vendor-only modules unless documented)
- Sovereign-profile smoke CI (gates against drift — links to R-002)
- ADR template "sovereign impact" mandatory section (action under R-002)
- Quarterly portability rehearsal (action below)

**TREAT.** Within TECHNOLOGY appetite (≤9).

#### Action Plan

- Pre-GA portability rehearsal: deploy on alternative cloud profile in CI (Lead Architect, due GA – 30 days)
- Quarterly portability re-rehearsal post-GA (Lead Architect)
- Vendor-specific feature inventory maintained as ADR addendum (Lead Architect, ongoing)

---

### Risk R-016: Shared Identity Service Compromise (ADR-003)

**Category:** TECHNOLOGY
**Status:** In Progress
**Risk Owner:** Security Lead
**Action Owner:** Lead Architect with Security Lead

#### Risk Identification

**Risk Description:** The shared identity service (ADR-003) is a single high-blast-radius component — compromise of the identity layer would expose all tenant SSO surfaces simultaneously. Mitigation is bulkhead patterns and short-lived tokens; the residual remains because shared-IdP architecture is inherently a higher-blast-radius choice than per-tenant IdP.

**Trigger Events:** Token leakage; IdP-software CVE; OIDC mis-configuration; admin credential phishing.

**Consequences:** Mass session hijack potential; ICO action; tenant trust loss.

**Affected Stakeholders:** Security Lead, Lead Architect, DPO, all tenants.

**Related Objectives:** G-4, ADR-003.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 2 | 5 | 10 (Medium) |
| Residual | 1 | 4 | 4 (Low) |

#### Current Controls

- ADR-003 short-lived tokens, refresh-rotation
- Tenant-scoped audience claims; defence-in-depth tenant-ID enforcement (R-014)
- WAF + IdP-aware DDoS protection
- IdP-component patching SLO (≤ 7 days for high CVE)
- Annual pen test with IdP focus
- Bulkhead patterns (rate-limited per tenant)

**TREAT.** Within TECHNOLOGY appetite.

---

### Risk R-017: AI Provider Lock-In or Disruption (ADR-004)

**Category:** TECHNOLOGY
**Status:** In Progress
**Risk Owner:** Lead Architect
**Action Owner:** Lead Architect

#### Risk Identification

**Risk Description:** Selected primary AI provider deprecates a model, raises prices materially, changes residency, or has an outage that the abstraction layer (ADR-004) does not cleanly route around. Re-states STKE Risk SR-4 in formal scoring and links to R-006 (cost) and R-011 (compliance). Requires the pluggable abstraction to be genuinely live, not theoretical.

**Trigger Events:** Provider deprecation notice; price > 25% jump; > 1-hour outage; UK-residency change.

**Consequences:** Service degradation; emergency switch; cost spike (R-006); GDPR gap (R-011).

**Affected Stakeholders:** Lead Architect, Service Owner, DPO, Finance, all tenants.

**Related Objectives:** G-8, O-7, ADR-004.

#### Inherent / Residual

| | L | I | Score |
|--|--|--|--|
| Inherent | 3 | 3 | 9 (Medium) |
| Residual | 2 | 2 | 4 (Low) |

#### Current Controls

- ADR-004 pluggable abstraction with second provider validated quarterly in CI (Goal G-8)
- DPIA refresh on provider change (R-011 controls)
- Documented switch-test runbook (Outcome O-7)

**TREAT.** Within TECHNOLOGY appetite.

#### Action Plan

- Pre-GA failover drill: actually switch to alternative provider in production-like environment (Lead Architect, due GA – 30 days)

---

## D. Risk Category Analysis

### STRATEGIC Risks

**Total:** 3 — R-001, R-002, R-003.
**Average Inherent:** 14.7. **Average Residual:** 7.0. **Reduction:** 52%.
**Risk List:**

- R-001: Cross-subsidy break-even fails — Residual 9 (Medium)
- R-002: MOD sovereign-route divergence — Residual 6 (Medium)
- R-003: DDaT pilot recognition failure — Residual 6 (Medium)

**Key Themes:** Cross-subsidy economics; dual-deployment discipline (Principle 21); buyer-side recognition validation.

**Profile:** ✅ Acceptable — all within appetite (≤12).

### OPERATIONAL Risks

**Total:** 2 — R-004, R-005.
**Average Inherent:** 9.0. **Average Residual:** 4.0. **Reduction:** 56%.
**Key Themes:** Pilot-engagement discipline; external-API dependency (Companies House).
**Profile:** ✅ Acceptable — within appetite (≤6).

### FINANCIAL Risks

**Total:** 2 — R-006, R-007.
**Average Inherent:** 12.0. **Average Residual:** 7.5. **Reduction:** 38%.
**Key Themes:** AI inference cost; free-tier abuse.
**Profile:** ⚠️ Concerning — R-006 sits at appetite ceiling. Monthly KRI required.

### COMPLIANCE Risks

**Total:** 4 — R-008, R-009, R-010, R-011.
**Average Inherent:** 14.5. **Average Residual:** 5.8. **Reduction:** 60%.
**Key Themes:** Multi-tenant data isolation; GDS Service Standard; AI transparency; sub-processor discipline.
**Profile:** ⚠️ Concerning — all 4 risks **exceed the very-low compliance appetite** (≤4). Acceptance with explicit governance trail.

### REPUTATIONAL Risks

**Total:** 2 — R-012, R-013.
**Average Inherent:** 9.5. **Average Residual:** 5.0. **Reduction:** 47%.
**Key Themes:** Trust collapse from contained incidents; visible SME-failure attribution.
**Profile:** ✅ Acceptable — at or within appetite.

### TECHNOLOGY Risks

**Total:** 4 — R-014, R-015, R-016, R-017.
**Average Inherent:** 12.0. **Average Residual:** 5.5. **Reduction:** 54%.
**Key Themes:** Tenant isolation engineering; managed-K8s portability; shared-IdP blast radius; AI-provider portability.
**Profile:** ✅ Acceptable — within appetite (≤9), but R-014 (8) requires continuous pen-test cadence to keep it there.

---

## E. Risk Ownership Matrix

| Stakeholder | Role | Owned Risks | Critical | High | Medium | Low | Total Residual | Concentration |
|-------------|------|-------------|----------|------|--------|-----|----------------|---------------|
| Mark Craddock | Service Owner (SIRO-equiv) | R-001, R-008, R-009, R-012, R-013 | 0 | 0 | 4 | 1 | 32 | ⚠️ Heavy — strategic + compliance |
| Lead Architect | CTO-equivalent | R-002, R-014, R-015, R-017 | 0 | 0 | 4 | 0 | 24 | Heavy on technology |
| DPO | Data Protection Officer | R-010, R-011 | 0 | 0 | 2 | 0 | 12 | Compliance focus |
| Security Lead | SIRO-support | R-016 | 0 | 0 | 0 | 1 | 4 | Light |
| Finance Lead | CFO-equivalent | R-006, R-007 | 0 | 0 | 2 | 0 | 15 | Financial focus |
| Product Manager | PM | R-004, R-005 | 0 | 0 | 1 | 1 | 8 | Operational focus |

**Risk Concentration Analysis:**

- ⚠️ **Service Owner owns 5 risks totalling 32 residual points** — appropriate (Service Owner = SIRO-equivalent and accountable for strategic + compliance acceptance) but Service Owner overload is itself a continuity risk; consider deputised review during absence.
- **Lead Architect concentration on technology risks** — appropriate.
- **DPO compliance focus** — appropriate; DPO and Service Owner co-sign R-010, R-011 acceptance.
- Compliance acceptance routes via Service Owner (SIRO-equivalent) + DPO + Security Lead joint sign-off (per `ARC-001-STKE-v1.0.md` decision authority matrix).

**Escalation Paths (from STKE Decision Authority Matrix):**

- Strategic / cross-subsidy (R-001) → Service Owner (final authority)
- Tenant isolation (R-008, R-014) → Service Owner (SIRO-equivalent) with Security Lead + Lead Architect counsel
- Compliance acceptance (R-008, R-009, R-010, R-011) → Service Owner + DPO + Security Lead
- Architecture / portability (R-002, R-015, R-017) → Lead Architect (final authority on ADRs) with Service Owner ratification on cost / strategic implications

---

## F. 4Ts Response Framework Summary

| Response | Count | % | Sum of Residual | Key Examples |
|----------|-------|---|-----------------|--------------|
| **TOLERATE** | 0 | 0% | 0 | (None at present — all risks have active controls) |
| **TREAT** | 16 | 94% | 96 | All except R-008 |
| **TRANSFER** | 1 | 6% | 5 | R-008 (cyber liability insurance — secondary to TREAT) |
| **TERMINATE** | 0 | 0% | 0 | None considered |
| **TOTAL** | 17 | 100% | 101 | |

**Response by Category:**

| Category | Tolerate | Treat | Transfer | Terminate | Predominant |
|----------|----------|-------|----------|-----------|-------------|
| STRATEGIC | 0 | 3 | 0 | 0 | Treat (100%) |
| OPERATIONAL | 0 | 2 | 0 | 0 | Treat (100%) |
| FINANCIAL | 0 | 2 | 0 | 0 | Treat (100%) |
| COMPLIANCE | 0 | 4 | 0 | 0 | Treat (100%) |
| REPUTATIONAL | 0 | 2 | 0 | 0 | Treat (100%) |
| TECHNOLOGY | 0 | 4 | 0 | 0 | Treat (100%) |

**Key Insights:**

- **94% TREAT response** — every risk has active mitigation; no tolerated-by-default position.
- **TRANSFER is secondary, not primary** — cyber-liability insurance for R-008 is contingency; controls are the primary defence.
- **No TERMINATE** — multi-tenant SaaS is the platform thesis; the only "terminate" option would be to abandon the platform, which is not in appetite.

---

## G. Risk Appetite Compliance

**Risk Appetite (UK Government / OFFICIAL classification, multi-tenant SaaS):**

| Category | Appetite Level | Threshold Score | Rationale |
|----------|---------------|-----------------|-----------|
| STRATEGIC | Medium | ≤ 12 | Mission requires accepting moderate strategic risk |
| OPERATIONAL | Low | ≤ 6 | Pilot-stage tolerance for ops disruption is low |
| FINANCIAL | Medium | ≤ 9 | Cross-subsidy depends on bounded financial variance |
| COMPLIANCE | Very Low | ≤ 4 | UK Gov / ICO posture demands minimal compliance breach risk |
| REPUTATIONAL | Low | ≤ 6 | Trust is one-strike asset for SME mission |
| TECHNOLOGY | Medium | ≤ 9 | Multi-tenant SaaS is technology-risk-bearing by nature |

**Compliance Summary:**

| Category | Appetite | Within | Exceeds | Avg Excess | Action |
|----------|----------|--------|---------|------------|--------|
| STRATEGIC | ≤12 | 3 (100%) | 0 | — | ✅ Compliant |
| OPERATIONAL | ≤6 | 2 (100%) | 0 | — | ✅ Compliant |
| FINANCIAL | ≤9 | 2 (100%) | 0 | — | ✅ At ceiling for R-006 |
| COMPLIANCE | ≤4 | 0 (0%) | 4 (100%) | +1.75 | ❌ Acceptance required |
| REPUTATIONAL | ≤6 | 1 (50%) | 0 (R-013 at threshold) | — | ✅ Compliant |
| TECHNOLOGY | ≤9 | 4 (100%) | 0 | — | ✅ Compliant |

**Overall Appetite Compliance:** 76% of risks within appetite; the COMPLIANCE category is the binding constraint.

**Risks Exceeding Appetite (all COMPLIANCE):**

| Risk | Appetite | Residual | Excess | Escalation |
|------|----------|----------|--------|------------|
| R-008 | 4 | 5 | +1 | Service Owner + DPO + Security Lead joint acceptance; cyber insurance |
| R-009 | 4 | 6 | +2 | Service Owner acceptance; pre-assessment walkthrough |
| R-010 | 4 | 6 | +2 | Service Owner + DPO acceptance; quarterly review |
| R-011 | 4 | 6 | +2 | DPO acceptance; quarterly sub-processor review |

**Recommendations:**

1. Formally accept the four COMPLIANCE residual positions before GA — recorded in `ARC-001-SbD-v1.0.md` (Secure by Design) and `ARC-001-DPIA-v1.0.md`.
2. Track each acceptance in a Compliance Acceptance Register with quarterly re-affirmation.
3. Where impact alone drives the excess (R-008), accept that residual likelihood is already at floor (1) and impact is inherent to the platform thesis.

---

## H. Prioritised Action Plan

### Priority 1: URGENT (pre-GA, must-land)

| # | Action | Risk(s) | Owner | Due | Cost | Expected Impact |
|---|--------|---------|-------|-----|------|-----------------|
| 1 | Independent pen test specifically targeting tenant isolation | R-008, R-014 | Security Lead | GA – 60 days | £40k–£60k | Validate residual 5 / 8 |
| 2 | Sovereign-profile CI smoke pipeline | R-002, R-015 | Lead Architect | GA – 60 days | Internal | Validate Principle 21 gate |
| 3 | Cloud-portability rehearsal on alternative profile | R-015 | Lead Architect | GA – 30 days | Internal | Prove portability claim |
| 4 | AI provider failover drill in production-like env | R-017, R-011 | Lead Architect | GA – 30 days | Internal | Prove ≤ 5-day switch (Outcome O-7) |
| 5 | Pre-assessment evidence pack walkthrough with one Service Assessor + one pilot DDaT EA | R-009, R-003 | Product Manager | GA – 60 days | Internal | De-risk Service Standard |
| 6 | Cyber-liability insurance procurement | R-008 (transfer) | Service Owner with Finance | GA – 30 days | Premium TBD | Loss-recovery floor |
| 7 | Incident runbook with ICO-72h-notification template | R-008, R-011, R-012 | DPO | GA – 30 days | Internal | Time-to-notify SLA met |
| 8 | Compliance Acceptance Register entries for R-008, R-009, R-010, R-011 | R-008, R-009, R-010, R-011 | Service Owner with DPO + Security Lead | GA – 14 days | Internal | Governance trail |

### Priority 2: HIGH (first 90 days post-GA)

| # | Action | Risk(s) | Owner | Due | Expected Impact |
|---|--------|---------|-------|-----|-----------------|
| 9 | AI feature-scope boundary defined (drafting / recommendation) | R-010 | DPO + Lead Architect | GA + 60 days | ATRS + DPIA boundary clarity |
| 10 | Bulkhead-pattern review across ADR-003 / ADR-004 | R-008, R-016 | Lead Architect | GA + 90 days | Extra defence-in-depth layer |
| 11 | Free-tier abuse detection + remediation runbook | R-007, R-001 | Product Manager + SRE | GA + 60 days | Cost-to-serve protection |
| 12 | Quarterly portability + AI-failover rehearsal cadence locked | R-002, R-015, R-017 | Lead Architect | GA + 30 days | Ongoing portability assurance |

### Priority 3: MEDIUM (continuous)

| # | Action | Risk(s) | Owner | Cadence |
|---|--------|---------|-------|---------|
| 13 | Quarterly affordability review + KRI dashboard | R-001, R-006, R-007 | Service Owner with Finance | Quarterly |
| 14 | Quarterly sub-processor review | R-011 | DPO | Quarterly |
| 15 | Quarterly DDaT user group | R-003, R-013, R-009 | Product Manager | Quarterly |
| 16 | Annual independent pen test | R-008, R-014, R-016 | Security Lead | Annual |
| 17 | Annual NCSC CAF + Cloud Security Principles refresh | R-008 family | Security Lead | Annual |
| 18 | Vulnerability disclosure programme | R-008, R-012 | Security Lead | Continuous |

**Action Plan Summary:**

- **Total pre-GA actions:** 8 — must complete or risk-accept before GA.
- **Estimated investment:** £40k–£60k (pen test) + cyber-insurance premium + internal engineering effort (sovereign CI, portability rehearsal, failover drill, evidence-pack walkthrough).
- **Expected residual risk reduction:** Maintain current residual scores under load; further reduction unlikely without trade-offs against velocity or cost.

---

## I. Integration with SOBC

### Strategic Case (Part A — Why Now?)

- **R-002** (MOD sovereign divergence): demonstrates urgency for Principle 21 single-codebase architecture from the outset.
- **R-001** (cross-subsidy fail): if SaaS does not launch on time, the cross-subsidy clock starts late and break-even slips.

### Economic Case (Part B — Risk-Adjusted Costing)

| Risk | Driver | Optimism-Bias Add |
|------|--------|--------------------|
| R-006 (AI inference) | AI cost forecast variance | +15% AI line item |
| R-007 (free-tier abuse) | Cost-to-serve variance | +10% free-tier cost line item |
| R-008 (cross-tenant) | Insurance premium + pen-test recurrence | Capital line item |
| R-015 (K8s lock-in) | Portability rehearsal effort | +5% engineering line item |
| Total HMT optimism-bias add | | ~ 12% blended |

### Commercial Case (Part C)

- **R-011** (sub-processor): drives DPA and Article 28 contractual terms.
- **R-009** (Service Assessment): drives G-Cloud listing dependency and procurement timing.

### Financial Case (Part D)

- **R-001 / R-006 / R-007** flow into the cross-subsidy financial model assumptions.

### Management Case (Part E — Risk Management)

- This register is included in full.
- Top 5 in §B + Risk Ownership Matrix in §E presented at SOBC sign-off.
- Compliance Acceptance Register cross-referenced.

---

## J. Monitoring and Review Framework

### Review Schedule

| Risk Level | Frequency | Reviewed By | Escalated To | Format |
|------------|-----------|-------------|--------------|--------|
| **Critical (20-25)** | Weekly | Risk Owner + Service Owner | Steering | Dashboard + narrative |
| **High (13-19)** | Bi-weekly | Risk Owner | Service Owner | Dashboard |
| **Medium (6-12)** | Monthly | Risk Owner | Service Owner | Exception report |
| **Low (1-5)** | Quarterly | Risk Owner | Service Owner | Status update |

Note: at residual, no risk is Critical or High — the table above governs *inherent* class for any risk that drifts back toward inherent.

### Key Risk Indicators (KRIs)

**Leading Indicators:**

- CI tenant-isolation test pass rate (target: 100%) → R-008, R-014
- Sovereign-profile smoke-CI pass rate (target: 100%) → R-002, R-015
- Per-tenant AI cost variance vs forecast (target: ±15%) → R-006, R-001
- Verified-SME share of free tier (target: ≥ 90%) → R-007
- Pen-test residual high findings (target: 0 unmitigated > 30 days) → R-008, R-014
- AI-feature scope events (target: tracked, none uncategorised) → R-010
- Sub-processor change events (target: 30-day notice on every change) → R-011

**Lagging Indicators:**

- ICO correspondence count (target: 0) → R-008, R-011
- Tenant-reported isolation anomalies (target: 0) → R-008
- GDS Service Assessment outcomes (target: pass at first review) → R-009
- Cross-subsidy P&L variance vs plan (target: ±10% by month 18) → R-001

### Escalation Triggers (Automatic)

1. Any KRI breach → Risk Owner immediate review
2. Any risk score increases by 3+ points → Service Owner notification
3. Any new Critical (≥20) risk → Steering Committee within 5 working days
4. Any Priority-1 mitigation action delayed > 2 weeks → Service Owner
5. Any compliance-acceptance breach not re-affirmed quarterly → DPO + Service Owner

### Reporting

- **Weekly:** R-008, R-014 KRI dashboard to Service Owner + Security Lead
- **Monthly:** Full register + Compliance Acceptance Register to Service Owner
- **Quarterly:** Risk profile, KRI trend, action-plan status to sponsor and CCS liaison
- **Annual:** Risk-appetite review with all owners

### Risk Register Maintenance

**Risk Register Owner:** Mark Craddock (Service Owner).

**Update Process:**

1. Risk Owners submit updates monthly (or on KRI breach).
2. Risk Register Owner consolidates and validates.
3. Quarterly Service Owner sign-off, recorded in Revision History.
4. Material changes → minor version bump (1.1, 1.2).
5. Structural revision (new risks, changed appetite) → major version bump (2.0).

---

## K. Orange Book Compliance Checklist

### Part I — Risk Management Principles

- ✅ **A. Governance and Leadership** — Risk owners assigned from STKE RACI; Service Owner = SIRO-equivalent; escalation path documented.
- ✅ **B. Integration** — Every risk linked to stakeholder drivers (SD-1..SD-14), goals (G-1..G-8), outcomes (O-1..O-7), and ADRs / requirements; SOBC integration in §I.
- ✅ **C. Collaboration and Best Information** — Risks sourced from STKE conflict / synergy analysis, ADR consequences, NFRs, and recognised UK-Gov SaaS risk patterns.
- ✅ **D. Risk Management Processes** — Six Orange Book categories covered; consistent 5×5 inherent and residual scoring; 4Ts response; KRIs defined.
- ✅ **E. Continual Improvement** — Review cadence at each risk class; quarterly + annual reviews; Compliance Acceptance Register re-affirmed quarterly; version-controlled register.

### Part II — Risk Control Framework (4-Pillar House)

- ✅ Risk appetite defined per category (§G) — explicit, calibrated to OFFICIAL UK-Gov SaaS.
- ✅ Risk ownership and governance — RACI from STKE, escalation in §E.
- ✅ Risk-assessment methodology — likelihood × impact 1–5, inherent and residual, in §C.
- ✅ Control effectiveness — measured via inherent → residual delta (§A, §D).

---

## Appendix A: Risk Assessment Scales

### Likelihood (1–5)

| Score | Rating | Probability |
|-------|--------|-------------|
| 1 | Rare | < 5% |
| 2 | Unlikely | 5–25% |
| 3 | Possible | 25–50% |
| 4 | Likely | 50–75% |
| 5 | Almost Certain | > 75% |

### Impact (1–5)

| Score | Rating | Financial | Schedule | Stakeholder | Mission |
|-------|--------|-----------|----------|-------------|---------|
| 1 | Negligible | < £25k | < 1 week | Minimal concern | Routine |
| 2 | Minor | £25k–£100k | 1–4 weeks | Minor concern | Manageable |
| 3 | Moderate | £100k–£500k | 1–3 months | Significant concern | Requires intervention |
| 4 | Major | £500k–£2M | 3–6 months | Severe concern | Threatens objectives |
| 5 | Catastrophic | > £2M | > 6 months | Existential threat | Mission failure |

### Risk Score Matrix

| Score | Level | Color | Action |
|-------|-------|-------|--------|
| 20–25 | Critical | 🟥 Red | Immediate escalation |
| 13–19 | High | 🟧 Orange | Senior management attention |
| 6–12 | Medium | 🟨 Yellow | Management monitoring |
| 1–5 | Low | 🟩 Green | Routine monitoring |

---

## Appendix B: Stakeholder → Risk Linkage

| Stakeholder | Driver | Risk(s) | Cat. | Residual |
|-------------|--------|---------|------|----------|
| Service Owner | SD-8 Mission and sustainability | R-001, R-008, R-009, R-012, R-013 | Multi | 32 |
| Lead Architect | SD-9 Sustainable engineering | R-002, R-014, R-015, R-017 | Multi | 24 |
| Security Lead | SD-10 Audit-defensible posture | R-014 (action), R-016 | TECH | 4 (own) + 8 (action share) |
| DPO | SD-11 UK GDPR posture | R-010, R-011 | COMP | 12 |
| NCSC / ICO | SD-12 Sectoral posture | R-008, R-010, R-011 (oversight) | COMP | n/a (regulator) |
| HMG / CCS / CDDO | SD-13 SME spend | R-001, R-009 | STRA | 15 |
| GDS Assessors | SD-14 Service Standard quality | R-009, R-013 | Multi | 12 |
| Finance Lead | (vendor internal) | R-006, R-007 | FIN | 15 |
| Product Manager | (vendor internal) | R-004, R-005 | OPS | 8 |
| DDaT Architects (buyer) | SD-1..SD-5 | R-003, R-013 | Multi | 12 |
| SME Architects / Founders | SD-6, SD-7 | R-001, R-007, R-013 | Multi | 21 |

**Conflict-Driven Risks (from STKE Conflict Analysis):**

| Conflict | Risk | Mitigation |
|----------|------|------------|
| C-1 Free-tier richness vs cost sustainability | R-001, R-006, R-007 | Quotas as cost lever; quarterly affordability review |
| C-2 AI provider concentration vs portability | R-011, R-017 | Pluggable abstraction; quarterly CI on alt provider |
| C-3 Self-service speed vs SME verification rigour | R-005, R-007 | Provisional access on outage; periodic re-verification |
| C-4 Buyer-feature depth vs SME-feature simplicity | R-004, R-013 | Strict baseline-features-on-free-tier line |

**STKE Risk-Section Cross-Reference:** Risks SR-1..SR-7 in `ARC-001-STKE-v1.0.md` are the precursor signal set; this register supersedes them with formal Orange Book scoring. Mapping: SR-1 → R-003; SR-2 → R-001; SR-3 → R-008 / R-014; SR-4 → R-017; SR-5 → not formalised here (accessibility risk handled in `ARC-001-SbD-v1.0.md` and CI a11y gates); SR-6 → R-009 (subsumed); SR-7 → R-005.

---

## Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| **Risk Register Owner** | Mark Craddock (Service Owner) | _________ | [PENDING] |
| **Lead Architect** | [PENDING] | _________ | [PENDING] |
| **Security Lead** | [PENDING] | _________ | [PENDING] |
| **DPO** | [PENDING] | _________ | [PENDING] |

---

## Next Steps

1. **Immediate (this week):**
   - Walk this register through with Lead Architect, Security Lead, DPO, Finance Lead.
   - Initiate Priority-1 actions 1, 2, 5 (pen test, sovereign-CI, evidence-pack walkthrough).
   - Open the Compliance Acceptance Register.
2. **Pre-GA (next 60 days):**
   - Complete all eight Priority-1 actions.
   - Joint sign-off on R-008, R-009, R-010, R-011 acceptance positions.
3. **Post-GA (continuous):**
   - Monthly KRI dashboard.
   - Quarterly affordability + sub-processor + DDaT-user-group reviews.
   - Annual pen test + CAF refresh + appetite review.

---

## External References

> No external policy documents were placed in `projects/001-arckit-saas/external/` at the time of generation. UK Government and HM Treasury policies referenced are public-domain and cited by name.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| — | — | — | — | — |

### Internal Cross-References

| Reference | Source | Use |
|-----------|--------|-----|
| `ARC-000-PRIN-v2.0.md` | Architecture Principles | Principle 1 (SME affordability), Principle 17 (FinOps), Principle 21 (sovereign-ready packaging) |
| `ARC-001-REQ-v1.0.md` | Requirements | NFR-SEC-002, FR-002, FR-004, BR-001..BR-008 |
| `ARC-001-STKE-v1.0.md` | Stakeholders | RACI (risk owners), conflict analysis (risk sources), SR-1..SR-7 precursor signals |
| `projects/001-arckit-saas/decisions/ARC-001-ADR-001-v1.0.md` | Tenant Isolation | R-008, R-014, R-016 |
| `ARC-001-ADR-002-v1.0.md` | Cloud Region & Storage | R-002, R-015 |
| `ARC-001-ADR-003-v1.0.md` | Identity & SSO | R-016 |
| `ARC-001-ADR-004-v1.0.md` | AI Provider Abstraction | R-006, R-011, R-017 |
| `ARC-001-ADR-005-v1.0.md` | Observability | R-008 (audit log), R-014 |
| `ARC-001-ADR-006-v1.0.md` | Deployment Topology | R-002, R-015 |
| `ARC-001-ADR-007-v1.0.md` | Data Portability | R-008 (export controls), R-001 (no-paywall commitment) |
| `ARC-001-ADR-008-v1.0.md` | Per-Tenant Quotas | R-006, R-007 |
| `projects/002-arckit-sovereign/` | Sovereign route | R-002 cross-project link |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:risk` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
