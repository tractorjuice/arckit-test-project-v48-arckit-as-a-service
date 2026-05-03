# ArcKit as a Service (Managed SaaS) — Strategic Outline Business Case (SOBC)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:sobc`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-SOBC-v1.0 |
| **Document Type** | Strategic Outline Business Case (HM Treasury Green Book five-case model) |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Owner** | Mark Craddock (Service Owner / SRO equivalent) |
| **Reviewed By** | [PENDING — ARB; Vendor Finance] |
| **Approved By** | [PENDING — Vendor SLT; ARB] |
| **Distribution** | ARB, Vendor SLT, prospective investors / co-funders, CCS / CDDO (where helpful for procurement) |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial SOBC. Five-case model (Strategic / Economic / Commercial / Financial / Management). Inputs: PRIN, REQ, STKE, RISK, ADRs 001–008. Cost figures indicative; OBC will refine. |

---

## 0. Executive Summary

ArcKit as a Service is the managed, multi-tenant offering of the open-source ArcKit enterprise architecture toolkit, designed to give SMEs supplying UK Government access to the same governance discipline that large system integrators take for granted — at a price point those SMEs can sustain.

**The strategic case** rests on the gap between what UK Government policy expects of suppliers (Service Standard, TCoP, NCSC CAF, Secure by Design) and the in-house architecture capability typical SMEs can afford. ArcKit closes this gap with a free tier sized for genuine SME engagement work and paid tiers for enterprise adopters whose revenue cross-subsidises the SME tier.

**The economic case** prefers the **Recommended Way Forward** — managed SaaS on UK-resident hyperscaler infrastructure (Option A in §2.5) — over self-host (B), single-vendor procurement (C), and do-nothing (D). The recommended option delivers the highest social value (SME supplier diversity, more SMEs winning Government work) at moderate cost and acceptable residual risk.

**The commercial case** anticipates G-Cloud listing as the primary procurement route, transparent published pricing, cross-subsidy economics, and a separate sovereign deployment route (project 002) funding additional capacity for the SME tier.

**The financial case** estimates indicative one-off and ongoing costs to be refined in OBC; the threshold question is whether the cross-subsidy break-even can be reached by GA + 18 months (BR-005) — currently judged plausible at the assumed enterprise-tier pricing and uptake.

**The management case** identifies key-person dependency as the largest delivery risk (RISK R-006) and sequences alpha → public beta → GA with explicit go/no-go gates.

The SOBC recommends **proceed with the Recommended Way Forward**, subject to ARB-level approval of the conditions in §6.

---

## 1. Strategic Case

### 1.1 Strategic context

UK Government has stated ambition to spend more with SMEs (£1 in every £3 SME spend target; SME Action Plans; Procurement Act 2023 reforms emphasise SME participation). At the same time, supplier-side governance bars (Service Standard, TCoP, NCSC CAF, Secure by Design, GDS Service Assessments) have risen. SMEs typically lack the in-house enterprise architecture capability that large system integrators staff as a matter of course; commercial EA tooling is priced for enterprises and is therefore a non-starter at the SME scale.

The result: a structural disadvantage for SMEs. Strong technical proposals from genuine specialists are hampered by weak governance evidence; weaker proposals from incumbents with mature governance teams are advantaged. This narrows the supplier base, reduces competition, and concentrates Government spend.

ArcKit as a Service exists to remove this specific barrier.

### 1.2 Strategic objectives

| ID | Objective | Source |
|----|-----------|--------|
| SO-1 | Provide a free, genuinely usable ArcKit tier to verified UK SMEs supplying Government | Principle 1; BR-001 |
| SO-2 | Provide paid tiers (enterprise; sovereign) whose revenue cross-subsidises the SME tier | BR-005 |
| SO-3 | Be procurable via G-Cloud and (where applicable) DOS / defence frameworks | BR-004; project 002 BR-007 |
| SO-4 | Be auditable against UK Government technical and security policy at all times | TCoP; CAF; SbD |
| SO-5 | Operate without lock-in — tenants retain full data and can exit any time | Principle 4; BR-007; ADR-007 |
| SO-6 | Operate sustainably — cross-subsidy break-even by GA + 18 months (commercial) and per-tenant carbon awareness (operational) | BR-005; Principle 17 |

### 1.3 Strategic dependencies

- UK Government continues to pursue SME-supplier ambition.
- NCSC / GDS / CDDO continue to publish stable, public technical standards (TCoP, CAF, Service Standard).
- Hyperscaler UK regions remain available with acceptable DPA terms.
- AI provider market continues to offer at least two viable UK-residency-compatible providers.

### 1.4 Strategic risks

See `ARC-001-RISK-v1.0.md`. Strategic-tier risks are R-002 (cross-subsidy fails), R-006 (key-person dependency), R-013 (early reputation).

### 1.5 Outcomes / measurable benefits (Green Book BCR-relevant)

| Outcome | Beneficiary | Measure |
|---------|-------------|---------|
| Verified UK SMEs adopting ArcKit free tier | SME suppliers; UK Government | # SMEs by GA + 12 months (BR-008 target: TBD) |
| SMEs winning Government work supported by ArcKit-generated governance evidence | SMEs; buying authorities | # / £ value won (tenant-reported) |
| Buying authorities accepting ArcKit governance evidence at procurement | Buying authorities | Survey at GA + 12 months |
| Cross-subsidy break-even | Vendor; mission sustainability | Break-even by GA + 18 months (BR-005) |
| Sovereign deployment adoption (project 002) | Sensitive sites; vendor | # sovereign deployments (project 002 KPI) |

---

## 2. Economic Case

### 2.1 Critical success factors

- Affordability for SMEs (Principle 1; BR-001).
- Demonstrable Government compliance posture (TCoP / CAF / SbD evidenced).
- Tenant isolation guaranteed (ADR-001) — a single defect would set the mission back years.
- Single codebase serves SaaS and sovereign (Principle 21).

### 2.2 Long-list of options

A. **Managed SaaS on UK-resident hyperscaler** with cross-subsidy (Recommended).
B. **Self-host on UK colocation** — vendor-owned hardware.
C. **Single-vendor closed-source procurement** — no managed service; sell licences only.
D. **Do nothing** — leave the market to existing commercial EA vendors.
E. **Open-source-only / no managed offering** — publish ArcKit but do not host it.

### 2.3 Short-list rationale

- **A** is the only option that delivers the SME-affordable managed service the strategic case requires.
- **B** breaks SME affordability and operational maturity needs (R-019 territory).
- **C** is the existing market and addresses none of the strategic objectives.
- **D** leaves the strategic gap uncorrected.
- **E** is part of the offering (open source under-pins both routes) but does not on its own deliver the SME-affordable hosted service most SMEs need.

Short-listed: **A** vs **D** (do-nothing baseline).

### 2.4 Long-list of options (table)

| Option | Strategic fit | SME affordability | Cost-to-vendor | Risk | Conclusion |
|--------|---------------|-------------------|----------------|------|------------|
| A — Managed SaaS (UK hyperscaler, cross-subsidy) | ✅ | ✅ | Moderate | Moderate | Recommended |
| B — Self-host on colocation | ⚠️ | ❌ | High | High | Rejected |
| C — Single-vendor closed source | ❌ | ❌ | Low | Low | Rejected |
| D — Do nothing | ❌ | n/a | nil | n/a | Comparator only |
| E — Open source only, no managed | ⚠️ | ⚠️ | Low | Low | Subset of A — kept as part of offering |

### 2.5 Recommended Way Forward

**Option A — Managed SaaS on UK-resident hyperscaler with cross-subsidy economics, sovereign route (project 002) as separate but co-engineered offering, open-source codebase under-pinning both.**

### 2.6 Economic appraisal (indicative; OBC will refine)

| Stream | Year 1 (DRAFT/Alpha) | Year 2 (Public beta / GA) | Year 3 (Steady state) |
|--------|----------------------|---------------------------|------------------------|
| Engineering effort (FTE-equiv) | 4 | 6 | 6 |
| Cloud infra cost | low | medium | medium-high |
| Sub-processors (IdP, AI, observability, email) | low | medium | medium |
| Compliance (pen test, audit, CE+) | low | medium | medium |
| Sales / marketing | low | medium | medium |
| Revenue (cross-subsidy) | nil | low (paid SME + early enterprise) | medium (enterprise + sovereign) |
| Net | -X | -Y (smaller) | break-even target Y3 (BR-005) |

(Specific currency figures intentionally out of scope of SOBC; OBC will populate.)

### 2.7 Social value / wider benefits

- More diverse supplier base for UK Government → better competition, lower prices, lower concentration risk.
- More SMEs surviving the procurement process → growth; jobs.
- Open codebase contribution to UK public sector → cross-government reuse.
- Ethical AI exemplar (AI Playbook conformance) for SMEs adopting AI.

---

## 3. Commercial Case

### 3.1 Procurement route

- Primary: **G-Cloud** listing (BR-004).
- Secondary: **DOS** (Digital Outcomes and Specialists) where buying authorities prefer.
- Tertiary: **direct procurement** for early adopters; **defence frameworks** for sovereign route (project 002).

### 3.2 Pricing model

| Tier | Description | Pricing approach |
|------|-------------|------------------|
| Free SME | Verified UK SMEs supplying Government | Free; cost-recovered via cross-subsidy |
| Paid SME | SMEs needing higher quotas / paid features | Cost-recovery + modest margin; published list price |
| Enterprise | Large suppliers / non-SME tenants | Margin pricing; published; subsidises free tier |
| Sovereign (project 002) | Sensitive-site customers | Per-engagement pricing; subsidises mission |

### 3.3 Contract structure

- Standard ToS + DPA for SME tiers (online acceptance).
- Negotiated MSA + DPA for enterprise.
- Bespoke contract per sovereign engagement.

### 3.4 Risk allocation

- Vendor responsible for processor obligations under UK GDPR (UK GDPR Art 28).
- Tenant responsible for lawful basis and tenant-content compliance.
- Sub-processor risks held by vendor and disclosed.

### 3.5 Commercial risks

- R-007 G-Cloud delay — mitigated.
- R-019 Cyber-insurance unaffordable — mitigated.
- R-002 Cross-subsidy fails — mitigated.

---

## 4. Financial Case

### 4.1 Funding sources

- Vendor capital (founder; potentially co-funders / angel).
- Cross-subsidy from enterprise / sovereign customers (BR-005).
- Optional UK funding programmes (e.g., Innovate UK, GovTech) — out of scope of SOBC; opportunistic.

### 4.2 Affordability

The recommended option is affordable subject to enterprise / sovereign uptake projection (BR-005). Year-1 funding requirement is the largest absolute spend; funding adequacy reviewed at each go/no-go gate.

### 4.3 Sensitivity analysis (qualitative)

| Sensitivity | Direction | Impact |
|-------------|-----------|--------|
| AI inference cost per generation | Higher | Free-tier per-tenant cost rises → cross-subsidy needs more enterprise revenue |
| Enterprise uptake | Lower | Cross-subsidy stretches → SME tier may need quota tightening (Principle 1 risk) |
| Sovereign uptake (project 002) | Lower | Less cross-subsidy contribution; SaaS still standalone-viable |
| Hyperscaler price | Higher | Cell unit economics affected; ADR-002 alternative providers pre-evaluated |
| Sterling FX (AI provider often USD-denominated) | Adverse | AI cost rises; partial hedge possible in contracts |

### 4.4 Whole-life cost

Whole-life cost is sensitive to tenant scale; the cell-based architecture (ADR-001/006) enables incremental capacity growth aligned to revenue, not big-bang capex.

---

## 5. Management Case

### 5.1 Delivery approach

Phased delivery: Discovery → Alpha → Private beta → Public beta → GA (see `ARC-001-PLAN-v1.0.md`).

### 5.2 Governance

- Vendor SLT (when constituted) — accountable.
- ARB (when constituted) — design decisions, ADR approval.
- Service Owner — day-to-day; SRO equivalent.
- DPO (PENDING) — UK GDPR.
- Security Lead (PENDING) — security posture.

### 5.3 Key roles to be filled

- Vendor Lead Architect / CTO.
- Vendor Security Lead.
- DPO.
- SRE Lead.
- Vendor Sovereign Delivery Lead (project 002).

### 5.4 Risks to delivery

R-006 (key-person dependency) is the largest; R-012 (engineering velocity) the second largest. Both have explicit mitigations.

### 5.5 Programme assumptions

- Phased GA acceptable to first-wave tenants.
- ARB constituted in time for ADR sign-off pre-alpha.
- Hyperscaler / AI provider DPA terms remain acceptable.
- No regulatory shock (e.g., EU AI Act or UK AI Bill) materially reclassifies the use case in 12 months.

### 5.6 Evaluation

| Phase | Go / no-go criteria |
|-------|---------------------|
| Pre-alpha | ARB constituted; Security Lead appointed; CI isolation suite live; first DR rehearsal pass; DPIA APPROVED; risk residual ≤ ARB-acceptable |
| Pre-public-beta | First pen test green; sub-processor inventory published; Service Standard alpha assessment passed; first paid tenant onboarded |
| Pre-GA | Cyber Essentials Plus achieved; Service Standard beta assessment passed; cross-subsidy track on plan |
| Post-GA + 18 months | Cross-subsidy break-even (BR-005) |

---

## 6. Recommendations and Conditions

The SOBC recommends **proceed** with the Recommended Way Forward (Option A), subject to:

1. ARB constituted and Lead Architect / Security Lead / DPO appointed before alpha.
2. CI isolation suite live before alpha.
3. First DR rehearsal passes before alpha.
4. DPIA progressed to APPROVED before public beta.
5. G-Cloud submission planned for 6 months pre-GA.
6. Cross-subsidy assumptions re-tested at each go/no-go gate.
7. OBC commissioned to refine financial figures with supplier-quoted hyperscaler / AI / IdP / observability prices, before commitments above £100k.

---

## 7. Linked Artefacts

- Principles: `projects/000-global/ARC-000-PRIN-v2.0.md`.
- Requirements: `ARC-001-REQ-v1.0.md`.
- Stakeholders: `ARC-001-STKE-v1.0.md`.
- Risk: `ARC-001-RISK-v1.0.md`.
- ADRs: 001 (isolation), 002 (region), 003 (identity), 004 (AI), 005 (observability), 006 (deployment), 007 (export), 008 (quotas).
- TCoP: `ARC-001-TCOP-v1.0.md`.
- Plan: `ARC-001-PLAN-v1.0.md`.
- Roadmap: `ARC-001-ROADMAP-v1.0.md`.

---

## 8. External References

- HM Treasury Green Book: https://www.gov.uk/government/publications/the-green-book-appraisal-and-evaluation-in-central-governent
- Better Business Cases (5-case model): https://www.gov.uk/government/publications/the-five-case-model
- Procurement Act 2023: https://www.gov.uk/government/collections/procurement-act-2023-guidance-documents
- G-Cloud framework: https://www.crowncommercial.gov.uk/agreements/RM1557.13
- SME Action Plans: https://www.gov.uk/government/publications/small-business-action-plans

---

**Generated by**: ArcKit `/arckit:sobc` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
