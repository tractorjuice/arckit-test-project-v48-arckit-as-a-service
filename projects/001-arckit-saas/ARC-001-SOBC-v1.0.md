# Strategic Outline Business Case (SOBC): ArcKit as a Service (Managed SaaS)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:sobc`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-SOBC-v1.0 |
| **Document Type** | Strategic Outline Business Case (SOBC) |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | At each Green Book gate (SOBC -> OBC -> FBC) |
| **Next Review Date** | 2026-09-30 (pre-Beta gate; convert to OBC after `/arckit:requirements` deepening) |
| **Owner** | Mark Craddock (Service Owner / SRO-equivalent) |
| **Reviewed By** | [PENDING] Lead Architect, Finance Lead, DPO, Security Lead |
| **Approved By** | [PENDING] Service Owner; Steering Committee at Beta gate |
| **Distribution** | Project Team, Architecture Team, CCS liaison, GDS, CDDO, prospective Steering Committee |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:sobc` command. Managed SaaS route only — sovereign deployment route is the subject of a separate SOBC under Project 002. | [PENDING] | [PENDING] |

## Document Purpose

This SOBC justifies the strategic, economic, commercial, financial, and management cases for taking ArcKit as a Service through Alpha and Beta to GA on the **managed SaaS route only**. It is the upstream Green Book artefact that authorises continued investment ahead of `/arckit:requirements` deepening, OBC, and FBC.

---

## Executive Summary

**Purpose**: ArcKit as a Service (managed SaaS) lowers the cost of producing credible UK Government architecture governance evidence (TCoP, GDS Service Standard, NCSC CAF, UK GDPR, WCAG 2.2 AA) for SMEs supplying the UK public sector, in service of the Procurement Act 2023 SME-spend objective and Architecture Principle 1 (Equitable Access for SMEs Supplying Government — NON-NEGOTIABLE).

**Problem Statement**: SMEs are systematically disadvantaged in UK Government bids by the cost and capability gap in enterprise architecture tooling. Buyers default to large incumbents because supplier-side governance evidence is inconsistent and disproportionately expensive to assure. The Procurement Act 2023 SME-spend objective and Cabinet Office SME Action Plans cannot be met without raising the floor of SME-side governance quality.

**Proposed Solution**: A multi-tenant, UK-resident, OFFICIAL-classification managed SaaS offering of the ArcKit toolkit, with a genuinely usable free tier for verified UK SMEs, transparent published pricing for SME paid tier, and a large-enterprise tier whose price funds the SME tier through an explicit cross-subsidy (BR-005). Listed on G-Cloud at GA.

**Strategic Fit**: Direct alignment with Procurement Act 2023, SME Action Plan, TCoP, GDS Service Standard, NCSC Secure by Design, and the architecture principle base (Principle 1 SME affordability NON-NEGOTIABLE; Principle 17 FinOps; Principle 21 sovereign-ready single codebase enabling Project 002).

**Investment Required (3-year, ROM ±30%, before optimism bias)**:

- Capital (build through Beta + GA hardening): £1.65M
- Operational (Years 1-3 run cost across all tiers including SME free): £2.85M
- **Subtotal 3-year TCO**: **£4.50M**
- HMT optimism-bias uplift (~12% blended, per RISK §I): **+£0.54M**
- **Risk-adjusted 3-year TCO**: **£5.04M**

**Expected Benefits (3-year, ROM)**: £8.4M cross-subsidy revenue + £4.6M attributable SME-bid public value uplift = £13.0M

**Return on Investment (3.5% HMT discount, risk-adjusted)**:

- NPV: **+£6.9M**
- Benefit-Cost Ratio (BCR): **~2.7**
- Payback Period: **~22 months from GA** (cross-subsidy break-even at GA + 18 months per Goal G-3 / R-001)
- ROI (undiscounted, 3-year): ~158%

**Recommended Option**: **Option 2 — Balanced Managed SaaS with Cross-Subsidy and G-Cloud Listing**

**Key Risks** (from `ARC-001-RISK-v1.0.md`, full register included by reference in Part E):

1. R-001: Cross-subsidy break-even fails by GA + 18 months (residual 9 — STRATEGIC)
2. R-006: AI inference cost overrun (residual 9 — FINANCIAL, at appetite ceiling)
3. R-008: Cross-tenant data leakage (residual 5 — COMPLIANCE, at-floor on impact, existential)

**Go/No-Go Recommendation**: **PROCEED**

**Rationale**: Option 2 is the only option that holds Principle 1 (SME affordability NON-NEGOTIABLE) credible while producing positive risk-adjusted NPV with manageable residual risk. Option 1 (minimal) breaks the Principle 1 commitment; Option 3 (comprehensive day-one) is unaffordable in Alpha; Option 0 (do nothing) leaves the SME-spend objective unsupported.

**Next Steps if Approved**:

1. Re-affirm `/arckit:requirements` (BR-001 through BR-008) — already complete at v1.0; refresh after Alpha pilot feedback (target 2026-09-30).
2. Beta gate: convert this SOBC to an Outline Business Case (OBC) once Alpha pilot data is in (target 2027-01-31).
3. Pre-GA: full pen test, AI provider failover drill, three buying-authority pilots (per RISK §H priority-1 actions).
4. GA gate: convert OBC to a Full Business Case (FBC) once GA-readiness evidence is in (target 2027-04-30).

---

# PART A: STRATEGIC CASE

## A1. Strategic Context

### A1.1 Problem Statement

**Current Situation**: The UK Government has set, and re-affirmed under the Procurement Act 2023 and successive SME Action Plans, an objective to widen the SME share of public spending. SMEs cannot meet the supplier-side governance bar economically because:

- Commercial enterprise architecture tooling is priced for large System Integrators (SIs) and is materially out of reach for sub-50-person SMEs.
- DDaT architects in buying authorities (Enterprise, Solution, Security, Data, Technical, Business, Network) inherit assurance work whenever supplier governance evidence is bespoke or low quality, which biases buyers toward large incumbents (per stakeholder driver SD-1).
- The Procurement Act 2023 objective and the assurance cost together create a structural drag on SME participation that cannot be solved by procurement policy alone — supplier-side capability has to rise.

**Specific Pain Points** (mapped from `ARC-001-STKE-v1.0.md`):

| Stakeholder | Driver ID | Pain Point | Impact | Intensity |
|-------------|-----------|------------|--------|-----------|
| SME Architect | SD-6 | Cannot afford enterprise EA tooling, cannot afford weak governance evidence | Reduced bid win rate; unbillable bid governance time | CRITICAL |
| SME Founder / Bid Lead | SD-7 | No predictable, low-cost EA tooling priced for SME bid economics | Each lost bid with weak governance is sunk cost; chilling effect on bidding | HIGH |
| DDaT Enterprise Architect (buyer) | SD-1 | Bespoke supplier governance evidence forces re-audit; biases buyer toward large incumbents | Procurement Act 2023 SME-spend objective at risk | HIGH |
| DDaT Security Architect (buyer) | SD-3 | Generic ISO-shaped supplier security evidence not mapped to NCSC CAF / Secure by Design | Translation friction in assurance; rejection or bespoke assurance | CRITICAL |
| Service Owner (vendor) | SD-8 | Without cross-subsidy, the free-tier mission collapses under cost pressure | Principle 1 commitment fails; platform's reason for existing fails | CRITICAL |

**Consequences of Inaction (Do Nothing — Option 0)**:

- Procurement Act 2023 SME-spend objective remains structurally constrained by the supplier-side governance gap.
- Continued bias toward large SI incumbents, undermining the diversity-of-supply objective and value-for-money outcomes.
- Existing commercial EA tooling vendors continue to underserve SMEs (their commercial logic does not change), perpetuating the gap.
- ArcKit AI Plugin remains a free CLI tool unsupported by managed services, leaving the SME audience to deploy and operate it themselves — a barrier that cancels most of the affordability gain.

### A1.2 Strategic Drivers

**Link to Stakeholder Analysis**: Drivers SD-1 through SD-14 are documented in `ARC-001-STKE-v1.0.md`. The dominant clusters are: **affordability** (SMEs, HMT), **assurance** (DDaT architects, CDDO, NCSC, ICO, GDS assessors), and **mission delivery** (vendor Service Owner).

**Primary Drivers**:

| Driver ID | Stakeholder | Driver Type | Driver Description | Strategic Imperative |
|-----------|-------------|-------------|-------------------|---------------------|
| SD-1 | DDaT Enterprise Architect (buyer) | STRATEGIC + COMPLIANCE | Trustable supplier governance evidence | Reduce buyer assurance burden -> enable SME-spend objective |
| SD-3 | DDaT Security Architect (buyer) | COMPLIANCE + RISK | NCSC CAF / Secure by Design alignment | Sectoral compliance posture |
| SD-6 | SME Architect | FINANCIAL + STRATEGIC | Affordable, credible, fast governance evidence | SME competitiveness in bids |
| SD-7 | SME Founder / Bid Lead | FINANCIAL + STRATEGIC | Predictable low-cost tooling raising win rate | SME bid economics |
| SD-8 | Service Owner (vendor) | STRATEGIC + PERSONAL | Mission and sustainability of Principle 1 | Cross-subsidy must work or platform fails |
| SD-13 | HMT / CCS / CDDO | FINANCIAL + COMPLIANCE | SME-spend share + value for money | Procurement Act 2023 implementation |

**Strategic Alignment**:

- **Procurement Act 2023 + SME Action Plan**: ArcKit raises supplier-side governance quality at SME prices, the missing leg of the SME-spend objective.
- **Architecture Principle 1 (Equitable Access for SMEs — NON-NEGOTIABLE)**: This SOBC operationalises Principle 1 commercially. Failure to deliver is a principle violation, not a delivery slip.
- **Architecture Principle 17 (Cost Transparency and FinOps)**: Cross-subsidy unit economics (BR-005) are explicit, monitored, and reviewed annually. No hidden enterprise pricing.
- **Architecture Principle 21 (Sovereign and Air-Gapped Deployment)**: The managed SaaS route in this SOBC and the sovereign deployment in Project 002 share a single codebase. Investment in the SaaS route is also the foundation for sovereign reuse.
- **TCoP, GDS Service Standard, NCSC CAF, NCSC Secure by Design, UK GDPR / DPA 2018, PSBAR 2018 / WCAG 2.2 AA**: Evidence pack (BR-006) is a first-class output, not a retrofit.

### A1.3 Stakeholder Goals

**Goals Addressed** (mapped from `ARC-001-STKE-v1.0.md` Goals G-1 to G-8):

| Goal ID | Stakeholder | SMART Goal | Current State | Target State | Timeline |
|---------|-------------|------------|---------------|--------------|----------|
| G-1 | Vendor Lead Architect | DDaT-recognisable artefacts validated by 3+ buying-authority pilots | 0 pilots | 3 successful pilots | by GA - 60 days |
| G-2 | Vendor Product Manager | SME free-tier user produces complete bid pack within 5 working days | 0 (pre-GA) | >= 60% SME activation | from GA |
| G-3 | Service Owner + Finance Lead | Cross-subsidy break-even (large-enterprise revenue >= aggregate SME cost-to-serve) | Pre-revenue loss | Break-even | GA + 18 months (target 2028-10-31) |
| G-4 | Vendor Security Lead | Current NCSC CAF + Cloud Security Principles posture | None pre-GA | Annual + on-change | from GA |
| G-5 | Vendor DPO | Current ROPA / sub-processor / DPIA / 72h breach readiness | None pre-GA | Maintained | from GA |
| G-6 | Accessibility Lead | WCAG 2.2 AA conformance with current Accessibility Statement | Partial | Sustained, zero critical regressions | from Beta |
| G-7 | Service Owner + CCS liaison | G-Cloud listing + SME-friendly minimum commitments | Not listed | Listed at GA + maintained | by GA |
| G-8 | Lead Architect | Pluggable AI provider, second provider validated quarterly in CI | Single provider | Switchable in <= 5 working days | by GA |

### A1.4 Scope

**In Scope (Project 001 — this SOBC)**:

- Multi-tenant managed SaaS in UK (OFFICIAL classification).
- Free tier for verified UK SMEs (BR-001).
- Paid SME tier (BR-002).
- Large-enterprise tier (cross-subsidy funder under BR-005).
- G-Cloud listing (BR-004).
- AI-assisted artefact generation (FR-004) with pluggable AI provider abstraction (G-8 / Conflict C-2).
- Tenant portability and exit (BR-007).
- Compliance evidence pack (BR-006: TCoP / Service Standard / CAF / Cloud Security Principles / UK GDPR / WCAG 2.2 AA).

**Out of Scope (deferred or separate)**:

- **Sovereign / air-gapped deployment** -> Project 002, separate SOBC. Architectural compatibility (Principle 21) is in scope here; sovereign productisation, MOD-grade variants, and air-gapped CI are not.
- **Managed services for non-OFFICIAL classifications** (OFFICIAL-SENSITIVE-with-handling, SECRET) -> not in scope of Project 001.
- **Bespoke buying-authority forks** of templates -> deferred to enterprise add-ons after GA (Conflict C-4 resolution).

**Interfaces** (from REQ INT-001 to INT-006):

- Companies House API (INT-003) — SME eligibility verification.
- AI / LLM provider (INT-005) — AI-assisted generation (pluggable per G-8).
- Cloud / hosting provider (INT-006) — UK-region hosted compute / storage.
- Payment processor (INT-002) — paid-tier billing.
- Identity provider (INT-001) — federated login / SSO on paid tiers.
- Email / notifications provider (INT-004) — verification / notifications.

**Assumptions**:

1. The Procurement Act 2023 SME-spend objective and the SME Action Plan remain policy through GA. **Risk if wrong**: strategic relevance falls; SOBC must be re-tested.
2. NCSC CAF, Cloud Security Principles, and GDS Service Standard remain the buyer-side language. **Risk if wrong**: evidence-pack templates rework — manageable, not existential.
3. AI inference unit cost trajectory does not deteriorate >25% / quarter beyond forecast. **Risk if wrong**: cross-subsidy break-even slips (R-006 -> R-001).
4. At least 200 verified UK SMEs onboard within 12 months of GA (BR-008). **Risk if wrong**: cross-subsidy break-even slips (R-001).
5. Cross-subsidy from large-enterprise tier alone is sufficient at modelled mix; no public-sector co-funding required. **Risk if wrong**: contingency funding sought (per R-001 mitigation).

**Dependencies**:

- **Internal**: Architecture principle base (`ARC-000-PRIN-v2.0.md`), risk register (`ARC-001-RISK-v1.0.md`), DPIA (`ARC-001-DPIA-v1.0.md`), Secure by Design (`ARC-001-SBD-v1.0.md`), TCoP review (`ARC-001-TCOP-v1.0.md`), AI Playbook (`ARC-001-AIP-v1.0.md`).
- **External**: G-Cloud framework iteration calendar (CCS); Companies House API stability; AI provider commercial terms; NCSC / ICO / GDS standards velocity.

### A1.5 Why Now?

**Urgency Factors**:

- Procurement Act 2023 has live commencement; SME-spend objective is being measured now, not later.
- AI-assisted artefact generation is at the maturity point where SMEs can plausibly produce DDaT-quality artefacts in days rather than weeks. Window-of-opportunity advantage erodes once large SIs internalise the same AI capability.
- Cross-subsidy break-even is sensitive to time-to-GA: every quarter of slip moves the break-even date and increases R-001 inherent score.

**Opportunity Cost of Delay** (per R-001 commentary):

- Each quarter of GA slip pushes cross-subsidy break-even by approximately one quarter.
- Each lost cohort of SME bidders represents foregone SME-share progress against the Procurement Act 2023 objective.

**Window of Opportunity**:

- AI inference cost is currently amortisable inside SME affordability constraints. If frontier-model pricing rises faster than commodity-model pricing falls, the cost envelope tightens (R-006).
- G-Cloud framework iteration cycle (BR-004) creates a natural GA window — missing it costs ~12-18 months of buyer reach (R SR-6 in stakeholder register).

---

# PART B: ECONOMIC CASE

## B1. Critical Success Factors

CSFs are derived from stakeholder Outcomes O-1 through O-7 in `ARC-001-STKE-v1.0.md` and from Goal G-3 cross-subsidy economics.

1. **CSF-1: DDaT-recognisable artefacts** (Outcome O-1, Goal G-1)
   - **Measure**: % of buying-authority engagements where ArcKit artefacts pass review without bespoke document requests.
   - **Threshold**: >= 70% by GA + 12 months; >= 3 successful pilots by GA - 60 days.
2. **CSF-2: Material SME adoption and activation** (Outcome O-2, Goal G-2, BR-008)
   - **Measure**: Verified SMEs onboarded; activation rate (>= 3 artefacts in 30 days); 90-day retention on SME paid tier.
   - **Threshold**: 200 SMEs / 60% activation / 70% retention by GA + 12 months.
3. **CSF-3: Cross-subsidy break-even** (Outcome O-3, Goal G-3, BR-005)
   - **Measure**: Quarterly cost-to-serve report; large-enterprise revenue >= aggregate SME cost-to-serve.
   - **Threshold**: Break-even by GA + 18 months (target 2028-10-31, assuming GA 2027-04-30).
4. **CSF-4: Zero cross-tenant security or privacy incidents** (Outcome O-4, Goals G-4 + G-5)
   - **Measure**: Incident register; ICO correspondence log; pen-test findings.
   - **Threshold**: 0 / 0 / 0 — sustained.
5. **CSF-5: G-Cloud-driven buyer reach** (Outcome O-5, Goal G-7, BR-004)
   - **Measure**: Distinct UK buying authorities procuring or hosting SME suppliers using ArcKit via G-Cloud.
   - **Threshold**: >= 25 by GA + 12 months.
6. **CSF-6: WCAG 2.2 AA accessibility sustained** (Outcome O-6, Goal G-6)
   - **Measure**: CI a11y green; manual AT report per release.
   - **Threshold**: 100% / 100% / 0 critical regressions.
7. **CSF-7: Pluggable AI architecture validated** (Outcome O-7, Goal G-8)
   - **Measure**: Quarterly CI run on alternative AI provider; documented switch test.
   - **Threshold**: Quarterly pass; switch achievable in <= 5 working days.

## B2. Options Analysis (Four Options — Standard Green Book Set)

> **Cost basis**: ROM (±30%) for Option 2, ROM (±40%) for Options 1 and 3, present-day prices, 3-year horizon. **Optimism bias**: ~12% blended add-on per RISK §I (Economic Case integration), driven by R-006 (+15% AI), R-007 (+10% free-tier cost), R-008 (capital insurance/pen-test recurrence), R-015 (+5% engineering for portability rehearsal). All options use the same blended uplift for comparability.

### Option 0: Do Nothing (Baseline)

**Description**: Continue with the free CLI ArcKit AI Plugin only; no managed SaaS; SMEs deploy and operate ArcKit themselves or not at all.

**Costs (3-year)**:

- Capital: £0
- Operational: £0 (vendor side); SME-side self-host effort priced at ~£3-5k per SME per project, total external cost burden ~£0.6-1.0M across the achievable population — this cost falls on SMEs, not the vendor, but is a public-value cost.

**Benefits**: £0 vendor revenue. Public value: limited to existing CLI plugin reach. Procurement Act 2023 SME-spend objective remains structurally constrained.

**Stakeholder Goals Met**: ~10% (CLI plugin meets a fraction of SD-6 / SD-7 needs; nothing for SD-1 / SD-3 buyer trust).

**Pros**:

- No vendor capital outlay
- No vendor operational risk

**Cons**:

- Principle 1 commitment unfulfilled
- SME-spend objective unsupported on the supply side
- DDaT architects continue to inherit assurance work; SME bias toward large incumbents persists

**Risks**: Principle 1 exception register grows; reputational risk for the architecture programme as a whole.

**Recommendation**: **REJECT** — Unacceptable baseline. The Strategic Case is not addressed.

---

### Option 1: Minimal Managed SaaS (Paid-Only, No Cross-Subsidy)

**Description**: Multi-tenant managed SaaS, paid tier only. SMEs charged at modest cost-recovery rate. No free tier; no cross-subsidy from large-enterprise tier; no G-Cloud listing in Year 1.

**Scope**:

- Multi-tenant SaaS, UK-resident, OFFICIAL.
- Single paid tier (cost-recovery price per seat).
- Manual SME verification (no Companies House integration in MVP).
- AI-assisted generation behind paid wall.
- No bespoke evidence pack — tenants generate their own using artefacts.

**Costs (3-year, ROM ±40%, before optimism bias)**:

- Capital: £0.85M
  - Platform build (multi-tenant baseline): £0.55M
  - SaaS billing + tenancy: £0.15M
  - AI integration (single provider, no abstraction): £0.10M
  - Pen test + minimum compliance: £0.05M
- Operational: £1.50M (3-year)
  - Cloud / hosting: £0.60M
  - AI inference: £0.30M
  - Support + SRE: £0.45M
  - Compliance maintenance: £0.15M
- **Subtotal**: **£2.35M**
- Optimism-bias uplift (~12% blended): **+£0.28M**
- **Risk-adjusted 3-year TCO**: **£2.63M**

**Benefits (3-year)**: £2.8M revenue (paid-only adoption modelled at ~30% of Option 2 SME volume due to no free tier funnel) — net benefit modest, public value contribution modest.

**Stakeholder Goals Met**: ~40%.

- G-1 (DDaT artefacts): partial — produced but pilot scale unfunded.
- G-2 (5-day SME pack): NOT MET — paid wall blocks the funnel.
- G-3 (cross-subsidy): NOT APPLICABLE — no cross-subsidy.
- G-4 / G-5 (CAF / UK GDPR): minimum compliance.
- G-7 (G-Cloud listing): NOT MET in Year 1.

**Pros**:

- Lowest absolute cost
- Lowest implementation risk
- Fastest to revenue

**Cons** (decisive):

- **VIOLATES Principle 1** (SME affordability NON-NEGOTIABLE). The free tier is the substantive expression of the principle; removing it removes the principle.
- Procurement Act 2023 SME-spend objective unsupported.
- Funnel collapse — no top-of-funnel route to enterprise tier conversion.
- Reputational risk: published as ArcKit but contradicts the core architecture principle.

**Risks**: Principle 1 violation triggers exception process per `ARC-000-PRIN-v2.0.md` §VI. Stakeholder withdrawal (Service Owner SD-8 mission failure).

**Recommendation**: **REJECT** — fails Principle 1; non-starter.

---

### Option 2: Balanced Managed SaaS with Cross-Subsidy and G-Cloud Listing (RECOMMENDED)

**Description**: Multi-tenant managed SaaS, UK-resident, OFFICIAL. Free tier for verified UK SMEs (BR-001), paid SME tier (BR-002), large-enterprise tier funding the SME tier through documented cross-subsidy unit economics (BR-005). G-Cloud listing at GA (BR-004). AI-assisted generation through pluggable abstraction (G-8). Full evidence pack (BR-006). Tenant portability and exit (BR-007).

**Scope** (== current `/arckit:requirements` scope at REQ v1.0):

- BR-001 Free tier for verified UK SMEs (genuinely usable, no time limit, no governance-critical paywalls).
- BR-002 Transparent published pricing (no "contact sales" gating for SME-eligible tiers).
- BR-003 SME eligibility verification (Companies House + self-attestation, 7-year audit retention).
- BR-004 G-Cloud listing at GA.
- BR-005 Cross-subsidy unit economics — documented per-tenant cost-to-serve, large-enterprise list price set at >= break-even for combined SME population, annual affordability review, margin reserve for 2x free-tier adoption stress.
- BR-006 UK public-sector evidence pack (TCoP / Service Standard / CAF / Cloud Security Principles / UK GDPR / WCAG 2.2 AA).
- BR-007 Tenant portability and exit (open formats, destruction certificate).
- BR-008 Adoption (>= 200 SMEs in 12 months post-GA).

**Costs (3-year, ROM ±30%, before optimism bias)**:

| Capital line | Cost |
|---|---|
| Platform build (multi-tenant SaaS, isolation, audit log) | £0.85M |
| SME verification + Companies House integration (FR-001) | £0.10M |
| Billing + tenancy + paid-tier UX | £0.20M |
| AI integration with pluggable abstraction (Conflict C-2 resolution; G-8) | £0.20M |
| Compliance evidence pack (BR-006) | £0.10M |
| Accessibility programme (BR-007 + Principle 12) | £0.10M |
| Pen testing pre-GA (per RISK §H Priority-1) | £0.05M |
| Implementation / training contingency (15%) | £0.05M |
| **Total CapEx** | **£1.65M** |

| Operational line (3-year total) | Cost |
|---|---|
| Cloud / hosting (UK region) | £0.85M |
| AI inference (multi-tier; +15% optimism bias = R-006) | £0.50M |
| SRE / on-call / support | £0.65M |
| DPO / Security / compliance maintenance | £0.30M |
| Customer success (SME activation) | £0.20M |
| Annual pen-test recurrence + cyber insurance | £0.20M |
| FinOps + tenant-cost-to-serve telemetry | £0.15M |
| **Total OpEx** | **£2.85M** |

- **Subtotal**: **£4.50M**
- Optimism-bias uplift (~12% blended, RISK §I): **+£0.54M**
- **Risk-adjusted 3-year TCO**: **£5.04M**

**Benefits (3-year)** — see B3 mapping:

| Benefit ID | Description | Stakeholder Goal | Type | Year 1 | Year 2 | Year 3 | 3-Year Total |
|------------|-------------|------------------|------|--------|--------|--------|--------------|
| B-001 | Large-enterprise tier revenue (cross-subsidy fund) | G-3 / BR-005 | FINANCIAL | £0.6M | £2.6M | £5.0M | £8.2M |
| B-002 | SME paid-tier revenue | BR-002 | FINANCIAL | £0.05M | £0.10M | £0.15M | £0.30M (modest by design) |
| B-003 | Public value: SME-bid wins attributable to ArcKit-produced artefacts | SD-13 / Procurement Act 2023 | STRATEGIC | £0.4M | £1.6M | £2.6M | £4.6M |
| B-004 | Buyer-side assurance time saving (DDaT EAs / SAs / SecAs) | O-1 | OPERATIONAL | £0.05M | £0.20M | £0.30M | £0.55M |
| B-005 | Compliance risk avoidance (UK GDPR, NCSC posture) | G-4 / G-5 | RISK | qualitative | qualitative | qualitative | qualitative |
| **Total quantified benefits** | | | | **£1.10M** | **£4.50M** | **£8.05M** | **£13.65M** |

**Net Present Value (3.5% HMT discount, risk-adjusted)**:

| Year | Costs (risk-adj) | Benefits | Net Cashflow | Discount Factor | Present Value |
|------|------------------|----------|--------------|-----------------|---------------|
| 0 (build) | £1.65M | £0 | -£1.65M | 1.000 | -£1.65M |
| 1 | £1.10M | £1.10M | £0.00M | 0.966 | £0.00M |
| 2 | £1.20M | £4.50M | +£3.30M | 0.934 | +£3.08M |
| 3 | £1.09M | £8.05M | +£6.96M | 0.902 | +£6.28M |
| **Sum** | **£5.04M** | **£13.65M** | **+£8.61M** | | **+£7.71M (NPV undiscounted ref £8.61M; HMT-discounted £7.71M; using risk-adjusted costs)** |

> Headline: **NPV ~ +£6.9M** with conservative trimming (5% reduction for unmodelled drag). **BCR ~ 2.7**. **Payback at GA + ~22 months** (cross-subsidy break-even at GA + 18 months per Goal G-3, full project payback ~4 months later once Year-3 enterprise revenue accrues).

**Pros**:

- Honours Principle 1 (NON-NEGOTIABLE).
- Honours Principle 17 (FinOps, transparent unit economics).
- Honours Principle 21 (sovereign-ready single codebase — Project 002 reuse).
- Highest stakeholder-goal coverage (~85%) of viable options.
- Positive NPV after HMT optimism-bias uplift (+£6.9M).
- Cross-subsidy break-even achievable on modelled adoption (BR-008).
- G-Cloud listing at GA delivers buyer reach (G-7 / O-5).

**Cons**:

- Higher upfront capital than Option 1 (+£0.80M).
- 12-18 month build to GA — schedule pressure on cross-subsidy clock (R-001).
- AI inference cost trajectory is the principal exogenous risk (R-006, at appetite ceiling).
- Tenant-isolation defence-in-depth (R-008 / R-014) requires sustained engineering discipline — control degradation is an immediate critical risk return.

**Stakeholder Impact**:

- G-1 (DDaT-recognisable artefacts): MET (3+ pilots planned pre-GA).
- G-2 (5-day SME pack): MET (FR-004 AI-assisted generation, free tier covers baseline).
- G-3 (cross-subsidy break-even): MET on plan (target GA + 18 months).
- G-4 (CAF + Cloud Security Principles): MET (annual + on-change).
- G-5 (UK GDPR / DPA): MET (DPIA in place at v1.0).
- G-6 (WCAG 2.2 AA): MET (Principle 12, CI a11y).
- G-7 (G-Cloud listing): MET (BR-004 at GA).
- G-8 (pluggable AI): MET (G-8 ADR + quarterly CI).

**Stakeholder Goals Met**: **~85%**.

**Risks** (full list in Part E; top items):

- R-001 (cross-subsidy break-even): TREAT — quarterly affordability review; AI-cost lever (Conflict C-1); enterprise sales motion.
- R-006 (AI inference cost overrun): TREAT — pluggable AI provider; ADR-008 per-tenant quotas.
- R-008 (cross-tenant data leakage): TREAT — defence-in-depth (residual 5, at-floor on impact).

---

### Option 3: Comprehensive Managed SaaS (Day-One Sovereign-Equivalent)

**Description**: Option 2 plus day-one sovereign-equivalent feature parity, day-one ISO 27001 certification, day-one second-AI-provider live (not just CI-validated), full multi-region UK active-active, day-one bespoke-template marketplace for buying authorities.

**Costs (3-year, ROM ±40%, before optimism bias)**:

- Capital: £2.80M (vs £1.65M for Option 2)
- Operational: £4.50M (vs £2.85M)
- Subtotal: £7.30M
- Optimism-bias uplift: +£0.88M
- **Risk-adjusted 3-year TCO**: **£8.18M** (~62% more than Option 2)

**Benefits (3-year)**: ~£14.5M (marginally higher than Option 2 — most uplift unrealised inside 3 years; sovereign feature parity primarily benefits Project 002, not this SOBC's payback case).

**Stakeholder Goals Met**: 100% (over-engineered relative to Year-1 demand).

**Pros**:

- 100% goal coverage
- Sovereign-equivalent reuse on day one (would shorten Project 002 timeline)
- Maximum resilience posture

**Cons**:

- Capital ~70% higher; operational ~58% higher
- 24-month build (vs 12-15 for Option 2) — cross-subsidy clock starts later
- NPV materially lower (~+£3.2M vs +£6.9M for Option 2) due to upfront cost weight and discount factor
- Diminishing returns: most extra spend funds Project 002 reuse, which has its own SOBC

**Stakeholder Impact**: All goals met; cost-effectiveness lower; payback longer.

**Risks**: R-001 worsens (longer time-to-cross-subsidy-break-even). R-002 (sovereign divergence) reduces, but at the cost of Project 001 economics.

**Recommendation**: **REJECT for Project 001** — diminishing returns; sovereign features properly belong in Project 002 with its own funding and OBC.

---

## B3. Benefits Mapping (Option 2 — Stakeholder-Goal Traceability)

| Benefit ID | Stakeholder Goal | Stakeholder Driver | Outcome | Type | 3-Year Value |
|------------|------------------|--------------------|---------|------|--------------|
| B-001 | G-3 (cross-subsidy break-even) | SD-8 (Service Owner mission), SD-13 (HMT/CCS/CDDO) | O-3 | FINANCIAL | £8.2M (large-enterprise revenue) |
| B-002 | BR-002 (transparent SME paid pricing) | SD-7 (SME founder cost predictability) | O-2 | FINANCIAL | £0.30M (modest by design — SME tier is cost-recovery) |
| B-003 | BR-008 / Procurement Act 2023 SME spend | SD-13, SD-7 | O-2, O-5 | STRATEGIC (public value) | £4.6M (attributable SME-bid public value uplift) |
| B-004 | G-1 (DDaT-recognisable artefacts) | SD-1, SD-2, SD-3 | O-1 | OPERATIONAL | £0.55M (buyer assurance time saving) |
| B-005 | G-4 / G-5 (CAF + UK GDPR posture) | SD-3, SD-10, SD-11, SD-12 | O-4 | RISK avoidance | qualitative — avoidance of single-incident existential damage |

**B-003 derivation note**: 200 verified SMEs at 12 months post-GA (BR-008); average government bid value floor £150k; attributable bid-win uplift modelled at conservative 5-7% on total bidding population that uses ArcKit-produced governance evidence; only the public-value (additional supplier diversity / value-for-money) component, not the SME revenue itself, is counted to avoid double-attribution. This benefit is the principal Procurement Act 2023 alignment indicator and is qualitatively reinforced by Outcome O-5 (G-Cloud-driven buyer reach).

## B4. Cost Estimates Summary (Option 2)

| Cost line | 3-Year (pre-bias) | 3-Year (post-bias, +12%) |
|-----------|-------------------|--------------------------|
| Capital | £1.65M | £1.85M |
| Operational | £2.85M | £3.19M |
| **TCO** | **£4.50M** | **£5.04M** |

## B5. Sensitivity Analysis

| Sensitivity | NPV impact (Option 2) | Notes |
|-------------|-----------------------|-------|
| Costs +20% | NPV ~ +£5.6M | Still positive; BCR ~ 2.2 |
| Benefits -20% | NPV ~ +£4.2M | Still positive; BCR ~ 2.2 |
| Costs +20% AND Benefits -20% (combined stress) | NPV ~ +£2.9M | Still positive; BCR ~ 1.8 (above HMT 1.0 threshold) |
| Cross-subsidy break-even slips to GA + 24 months | NPV ~ +£4.0M | Driven by R-001 — manageable but reduces headroom |
| AI inference cost +50% (R-006 stress) | NPV ~ +£3.5M | Conflict C-1 quotas + AI provider switch (G-8) compensate |
| BR-008 adoption shortfall (100 SMEs at 12 months instead of 200) | NPV ~ +£1.8M | Risk SR-2 / R-001 — quotas adjusted, contingency funding sought |

## B6. Recommended Option

**Option 2 — Balanced Managed SaaS with Cross-Subsidy and G-Cloud Listing**

**Rationale**:

1. **Only option that preserves Principle 1 (NON-NEGOTIABLE)**. Option 0 fails by inaction; Option 1 fails by paywall; Option 3 is over-engineered for Year 1.
2. **Best NPV**: +£6.9M risk-adjusted, BCR ~ 2.7, comfortably above HMT 1.0 threshold even under combined stress.
3. **Stakeholder coverage**: ~85% — covers all CRITICAL drivers (SD-3, SD-6, SD-8, SD-10).
4. **Affordability**: £5.04M risk-adjusted 3-year TCO is consistent with Service Owner / vendor funding envelope.
5. **Deliverability**: 12-15 month build to GA is realistic given existing artefacts (REQ, RISK, DPIA, SBD, TCoP, AIP all at v1.0).
6. **Risk profile**: Top residual risks (R-001, R-006, R-008) are within or at appetite — no risk requires escalation beyond the Service Owner / SIRO-equivalent acceptance regime defined in `ARC-001-RISK-v1.0.md` §G.

---

# PART C: COMMERCIAL CASE

## C1. Procurement Strategy

### C1.1 Market Assessment

**Market Maturity**:

- The UK Government managed-SaaS market for governance / EA tooling is fragmented. Existing commercial EA tooling (LeanIX, Ardoa, Bizzdesign, etc.) is priced for enterprises and is structurally not addressable by SMEs at SME unit economics.
- Buying authorities' current default is bespoke supplier-side governance — hence the assurance-cost problem (SD-1, SD-3).
- ArcKit as a Service occupies an underserved niche: SME-priced, UK-Gov-aligned, evidence-pack-ready managed SaaS.

**Supplier Landscape (vendor inputs to ArcKit SaaS, not ArcKit-as-vendor competitors)**:

- AI / LLM provider (INT-005): commercial market, 3+ credible UK-region-capable providers (Conflict C-2 / G-8 pluggability requirement).
- Cloud / hosting (INT-006): UK-region hyperscalers + UK sovereign cloud providers — viable competition.
- Companies House: monopoly upstream; mitigation already in `ARC-001-RISK-v1.0.md` R-005 (SME onboarding brittleness).
- Payment processor (INT-002): commodity competition.

**UK Government Digital Marketplace Assessment**:

- **G-Cloud 14 (or current iteration at GA)**: ArcKit-as-a-Service to be listed as Lot 2 (Cloud Software) — SaaS service definition + T&Cs + pricing + SFIA-rated rates published.
- **DOS (Digital Outcomes & Specialists)**: not the primary route; managed SaaS is procured via G-Cloud, not DOS.
- **SME participation (vendor side)**: ArcKit vendor itself is an SME — Procurement Act 2023 SME-supplier alignment is direct, not aspirational.

### C1.2 Sourcing Route (for SaaS upstream services)

**For the AI provider (highest commercial-risk upstream)**:

- **Recommended route**: Direct contract with selected provider; pluggable abstraction (G-8) means second provider can be brought in without re-architecture.
- **Article 28 / DPA**: AI sub-processor DPA must include UK GDPR Article 28 controller-processor terms, no-training assurances, sub-processor change notice (>= 30 days), and Article 46 transfer mechanisms where applicable (per RISK R-011).
- **AI Sub-Processor DPA Specifics**:
  - Explicit no-training-on-tenant-data clause.
  - Sub-processor list maintained with tenant-facing transparency (per `ARC-001-DPIA-v1.0.md`).
  - 30-day change notification requirement.
  - Audit / inspection rights consistent with Article 28(3)(h).
  - Termination assistance and data return / deletion timelines.

**For the cloud provider (INT-006)**:

- **Recommended route**: UK-region commercial agreement. Sovereign-cloud option (Project 002) is a separate procurement.
- Standard hyperscaler T&Cs reviewed by DPO + Security Lead; cloud-region pinned to UK; data residency telemetry per Principle 7.

**For the SaaS itself (downstream — buyer route to ArcKit)**:

- **Buyers route**: G-Cloud Lot 2 (Cloud Software) — call-off without bespoke procurement (BR-004). Minimum commitment terms friendly to SME-buying-from-SME (per `ARC-001-STKE-v1.0.md` SD-13 enablers).

**Alternative Routes Considered**:

| Route | Pros | Cons | Recommendation |
|-------|------|------|----------------|
| Direct sale outside G-Cloud | Higher margin per deal | Limits buyer reach; bespoke procurement burden falls on every buyer | REJECT |
| DOS (Digital Outcomes & Specialists) | Some buyer familiarity | Wrong framework — DOS is for outcomes / specialists, not SaaS | REJECT |
| Crown Hosting | UK sovereign hosting baseline | Out of scope for managed SaaS; relevant to Project 002 | DEFER to Project 002 |
| **G-Cloud Lot 2 (Cloud Software)** | **Correct framework; buyer route of least friction; SME-friendly minimum commitments** | **Annual listing cycle requires discipline (R SR-6)** | **ACCEPT** |

### C1.3 Contract Approach (SaaS terms with tenants)

**Proposed contract type**:

- **Free SME tier**: Click-through T&Cs — no minimum commitment, no time limit, no governance-critical paywalls (BR-001).
- **Paid SME tier**: Per-seat per-month subscription, transparent published list price (BR-002), no "contact sales" gating.
- **Large-enterprise tier**: Annual subscription, transparent list price (BR-002 amendment), with the cross-subsidy unit economics (BR-005) explicit in the published affordability review.
- **G-Cloud purchase orders**: Accepted in lieu of bespoke MSAs (BR-004 / REQ acceptance criterion line 570).

**Contract duration**:

- Free tier: indefinite (subject to fair-use under ADR-008 quotas).
- Paid tiers: monthly or annual, no multi-year lock-in for SMEs.
- Large-enterprise tier: annual, with up to 3-year option at customer election.

**Payment structure**:

- Free tier: £0.
- Paid SME tier: monthly or annual, in advance.
- Large-enterprise tier: annual in advance.

**Key contract terms**:

- **SLAs**: Availability, RTO/RPO, support response time per `ARC-001-REQ-v1.0.md` NFR section.
- **Tenant portability and exit**: Open formats (Markdown / JSON / YAML); destruction certificate (BR-007).
- **Sub-processor list**: Transparent and current; 30-day notice on change (R-011).
- **AI lineage**: AI-generated content metadata mandatory and downloadable (FR-004 lineage).
- **IP**: Tenant content remains tenant property; ArcKit retains platform IP.
- **Termination**: 30-day grace period default (configurable up to 90 days per BR-007).

### C1.4 Social Value (UK Government 10% minimum weighting)

ArcKit-as-a-Service is itself a social-value vehicle:

1. **Economic**: Lowers SME bidding cost; expands SME-supplier diversity in UK Government.
2. **Social**: UK SME vendor; published transparent pricing (no hidden enterprise pricing); UK-resident OFFICIAL data handling.
3. **Environmental**: AI inference cost discipline (FinOps Principle 17) + cloud-region pinning (Principle 7) reduce avoidable carbon overhead from gratuitous cross-region traffic.

**Evaluation approach (when buyers procure)**: ArcKit aligns with standard G-Cloud / Procurement Act 2023 social-value weighting (10% minimum in evaluation); the platform's own existence as an SME-affordability vehicle is a material social-value claim.

---

# PART D: FINANCIAL CASE

## D1. Budget Requirement

**Total investment required (Option 2, risk-adjusted)**: **£5.04M over 3 years** (£1.85M CapEx + £3.19M OpEx after 12% blended optimism-bias uplift).

### D1.1 Capital Expenditure (CapEx) — Option 2

| Item | Year 0 (Build) | Year 1 (GA Hardening) | Year 2 | Year 3 | Total (pre-bias) |
|------|----------------|------------------------|--------|--------|------------------|
| Platform build (multi-tenant + isolation + audit log) | £0.65M | £0.20M | £0 | £0 | £0.85M |
| SME verification + Companies House (FR-001) | £0.10M | £0 | £0 | £0 | £0.10M |
| Billing + tenancy + paid-tier UX | £0.15M | £0.05M | £0 | £0 | £0.20M |
| AI integration + pluggable abstraction (G-8 / Conflict C-2) | £0.15M | £0.05M | £0 | £0 | £0.20M |
| Compliance evidence pack (BR-006) | £0.07M | £0.03M | £0 | £0 | £0.10M |
| Accessibility programme | £0.07M | £0.03M | £0 | £0 | £0.10M |
| Pen testing pre-GA (RISK §H Priority-1) | £0.03M | £0.02M | £0 | £0 | £0.05M |
| Implementation contingency (15%) | £0.03M | £0.02M | £0 | £0 | £0.05M |
| **Total CapEx (pre-bias)** | **£1.25M** | **£0.40M** | **£0** | **£0** | **£1.65M** |

### D1.2 Operational Expenditure (OpEx) — Option 2

| Item | Year 1 | Year 2 | Year 3 | 3-Year Total (pre-bias) |
|------|--------|--------|--------|--------------------------|
| Cloud / hosting (UK region) | £0.20M | £0.30M | £0.35M | £0.85M |
| AI inference (incl. R-006 +15%) | £0.10M | £0.18M | £0.22M | £0.50M |
| SRE / on-call / support | £0.18M | £0.22M | £0.25M | £0.65M |
| DPO / Security / compliance maintenance | £0.10M | £0.10M | £0.10M | £0.30M |
| Customer success (SME activation) | £0.05M | £0.07M | £0.08M | £0.20M |
| Annual pen-test recurrence + cyber insurance | £0.05M | £0.07M | £0.08M | £0.20M |
| FinOps + cost-to-serve telemetry | £0.04M | £0.05M | £0.06M | £0.15M |
| **Total OpEx (pre-bias)** | **£0.72M** | **£0.99M** | **£1.14M** | **£2.85M** |

### D1.3 Total Cost of Ownership (TCO)

| | Year 0 | Year 1 | Year 2 | Year 3 | 3-Year Total |
|---|--------|--------|--------|--------|---------------|
| CapEx (pre-bias) | £1.25M | £0.40M | £0 | £0 | £1.65M |
| OpEx (pre-bias) | £0 | £0.72M | £0.99M | £1.14M | £2.85M |
| **TCO (pre-bias)** | **£1.25M** | **£1.12M** | **£0.99M** | **£1.14M** | **£4.50M** |
| HMT optimism-bias (~12%, RISK §I) | +£0.15M | +£0.13M | +£0.12M | +£0.14M | **+£0.54M** |
| **TCO (risk-adjusted)** | **£1.40M** | **£1.25M** | **£1.11M** | **£1.28M** | **£5.04M** |

**Notes**:

- All costs in 2026 prices.
- Excludes VAT.
- Optimism-bias uplift is HMT-recommended treatment per Green Book; ~12% blended is the integrated total per `ARC-001-RISK-v1.0.md` §I (R-006 +15% AI line; R-007 +10% free-tier cost line; R-008 capital insurance / pen-test recurrence; R-015 +5% engineering for portability rehearsal).

## D2. Funding Source

**Vendor-funded** in the first instance (Mark Craddock as Service Owner / sponsor).

**Funding tiers**:

1. **Year 0 build (£1.40M risk-adjusted)**: Vendor working capital + retained earnings + (optionally) targeted public-sector / philanthropic co-funding for SME-tier capacity.
2. **Year 1 onward**: Funded by paid-tier and large-enterprise revenue; cross-subsidy economics begin to validate from quarter 5 post-GA.
3. **Reserve / contingency**: Margin reserve sufficient to absorb 2x free-tier adoption stress (BR-005 acceptance criterion).

**Approval thresholds**:

- Below £5M aggregate capital: vendor-internal Service Owner approval (this SOBC).
- If contingency funding sought from public sector (per R-001 mitigation): standard CCS / DCMS / DSIT / Innovate UK grant routes; would need a separate FBC.

**Funding gaps** (if BR-008 adoption shortfall — Risk SR-2):

- Forecast gap up to £0.5M in Year 2.
- **Mitigation**: adjust quotas (not feature paywalls per Conflict C-1 resolution); seek targeted co-funding; defer non-critical features.

## D3. Affordability

**Vendor budget context**:

- ArcKit vendor is an SME (Procurement Act 2023 SME definition).
- 3-year risk-adjusted TCO (£5.04M) is the controlling commitment; staged across years (£1.40M / £1.25M / £1.11M / £1.28M).
- Largest single-year commitment: Year 0 build at £1.40M (~28% of 3-year TCO).
- **Assessment**: Affordable conditional on adoption (BR-008) — at modelled enterprise-tier mix the cross-subsidy clears the cost-to-serve from quarter 5 post-GA.

**Cash flow**:

- Largest single payment commitment: Year 0 platform build (£0.65M pre-bias engineering spend, ~£0.73M post-bias).
- **Cashflow risk**: Year 0 to Quarter 4 of Year 1 (build through GA hardening) is the negative-cashflow window. Mitigation: phased build; pen-test deferral on a portion to Quarter 4 of Year 1; contingency call on co-funding if BR-008 shortfall.

**Ongoing affordability**:

- Year 3+ steady-state OpEx ~ £1.14M/year pre-bias (~£1.28M post-bias).
- Funded by combined paid-SME + large-enterprise tier revenue at modelled adoption levels.
- Margin reserve required by BR-005 acceptance criterion.

## D4. Financial Appraisal

### D4.1 Economic Appraisal (HMT Green Book)

**Discount rate**: 3.5% (HMT social time preference rate).

**NPV calculation (Option 2, risk-adjusted)**:

| Year | Costs (risk-adj) | Benefits | Net Cashflow | Discount Factor | PV |
|------|------------------|----------|--------------|-----------------|----|
| 0 | £1.40M | £0 | -£1.40M | 1.000 | -£1.40M |
| 1 | £1.25M | £1.10M | -£0.15M | 0.966 | -£0.14M |
| 2 | £1.11M | £4.50M | +£3.39M | 0.934 | +£3.16M |
| 3 | £1.28M | £8.05M | +£6.77M | 0.902 | +£6.10M |
| **Total** | **£5.04M** | **£13.65M** | **+£8.61M** | | **+£7.71M (NPV)** |

After ~10% conservative trim for unmodelled drag and benefit-attribution conservatism on B-003 public value:

- **Headline NPV ~ +£6.9M**
- **BCR ~ 2.7**

### D4.2 Return on Investment

- **ROI (undiscounted, 3-year)**: (£13.65M - £5.04M) / £5.04M = **~170%** (~158% after conservative B-003 trim).
- **Payback period**:
  - Cross-subsidy break-even (large-enterprise revenue >= aggregate SME cost-to-serve): **GA + 18 months** per Goal G-3.
  - Full project payback (cumulative net cashflow turns positive after build): **~22 months from GA** (within Year 3).

### D4.3 Value for Money Assessment

- **Economy**: G-Cloud route + transparent pricing + UK-region cloud commodity competition + pluggable AI provider abstraction reduces vendor lock-in cost premium.
- **Efficiency**: AI-assisted artefact generation (FR-004) compresses SME governance-pack production from weeks to days (Goal G-2: <= 5 working days for first complete pack on free tier).
- **Effectiveness**: ~85% stakeholder-goal coverage; meets all CRITICAL drivers (SD-3, SD-6, SD-8, SD-10).

**Overall VfM rating**: **HIGH** — BCR of 2.7 (after risk adjustment, optimism bias, and conservative benefits trim) clears HMT thresholds with significant headroom; aligns with stated public-value objectives (Procurement Act 2023 SME spend).

---

# PART E: MANAGEMENT CASE

> **Note**: This Management Case incorporates **`ARC-001-RISK-v1.0.md` in full by reference** (per RISK §I "Management Case (Part E — Risk Management)"). The full register, top-10 ranking, risk matrices, appetite, KRIs, and monitoring framework are included by reference and should be presented at SOBC sign-off.

## E1. Governance

### E1.1 Roles and Responsibilities (RACI)

Mapped from `ARC-001-STKE-v1.0.md` Decision Authority Matrix.

| Decision / Activity | Responsible | Accountable | Consulted | Informed |
|---------------------|-------------|-------------|-----------|----------|
| Overall programme success | Lead Architect / CTO | Service Owner (Mark Craddock — SRO-equivalent) | Steering Committee | All stakeholders |
| Pricing tier changes | Product Manager | Service Owner | Finance, Lead Architect, CCS liaison | All staff, tenants |
| SME eligibility policy | Product Manager | Service Owner | DPO, Legal, Finance | All staff, tenants |
| Architecture decisions (ADRs) | Lead Architect | Lead Architect | Security Lead, DPO, Service Owner | All engineering |
| Security control acceptance | Security Lead | Service Owner (SIRO-equivalent) | DPO, Lead Architect | All engineering |
| DPIA decisions | DPO | Service Owner | Security Lead, Lead Architect | All staff |
| AI provider selection | Lead Architect | Service Owner | DPO, Security Lead, Finance | All engineering |
| G-Cloud listing content | Product Manager | Service Owner | CCS liaison, Finance | All staff |
| Free-tier limit changes | Product Manager | Service Owner | Finance, Lead Architect, SME tenant council | All staff, tenants |
| Pilot acceptance with buying authority | Service Owner | Service Owner | Lead Architect, Product Manager, DDaT EA pilot lead | All staff |
| Severe incident response | Service Owner | Service Owner | Security Lead, DPO, Legal, Comms | All staff, ICO/NCSC if applicable |
| Go / no-go for GA | Service Owner | Service Owner | All Manage-Closely stakeholders | All |

**Senior Responsible Owner (SRO-equivalent)**: Mark Craddock (Service Owner). For UK Government this would be discharged by the Permanent Secretary's delegate; in this private-sector ArcKit-vendor context the Service Owner holds the equivalent accountability.

**Steering Committee** (at GA):

- Service Owner (Chair)
- Lead Architect / CTO
- Security Lead (SIRO-equivalent)
- DPO
- Finance Lead
- Product Manager
- CCS liaison (advisory)
- Pilot DDaT EA representative (advisory)

**Meeting frequency**: Weekly during pre-GA; monthly post-GA (with weekly during R-008 / R-014 critical-control reviews).

### E1.2 Approval Gates

| Gate | Criteria | Approving Body | Target Timing |
|------|----------|----------------|---------------|
| **Gate 0: SOBC approval** (this document) | This SOBC approved; funding pathway confirmed | Service Owner; Steering Committee at convene | 2026-06-30 |
| **Gate 1: Alpha entry** | REQ v1.0 + RISK v1.0 + DPIA + SBD + TCoP + AIP all at v1.0 (status today) | Service Owner | 2026-07-15 |
| **Gate 2: Private Beta** | Alpha pilot data; pilot-1 buying-authority feedback; isolation tests in CI green | Steering Committee | 2026-12-31 |
| **Gate 3: OBC conversion** | OBC produced (this SOBC + Alpha actuals + tightened cost ranges) | Service Owner | 2027-01-31 |
| **Gate 4: Pre-GA pen test + AI failover drill** | Independent pen test clean; AI provider failover proven | Security Lead + Service Owner | 2027-03-15 |
| **Gate 5: GA approval** | All RISK §H Priority-1 actions complete; G-Cloud listed; FBC produced | Steering Committee | 2027-04-30 |
| **Gate 6: Cross-subsidy break-even review** | Quarterly affordability report; G-3 metrics tracking | Service Owner + Finance Lead | 2028-10-31 (GA + 18 months) |
| **Gate 7: 12-month benefits realisation** | BR-008 adoption; Outcome O-1 / O-2 / O-3 metrics | Service Owner | 2028-04-30 |

## E2. Project Approach

**Methodology**: Agile (Scrum) with phased Green Book / GDS gates. Inception -> Discovery -> Alpha -> Private Beta -> Public Beta -> GA -> Live. ArcKit's own command suite is used to govern itself (`/arckit:plan`, `/arckit:adr`, `/arckit:risk`, etc.) — eat-your-own-dog-food governance.

**Phases**:

1. **Discovery (already complete)**: REQ + RISK + STKE + PRIN + DPIA + SBD + TCoP + AIP all at v1.0.
2. **Alpha (2026-07 to 2026-12)**: Private build; first pilot with one buying-authority EA in the loop (per RISK §H Priority-1).
3. **Private Beta (2027-01 to 2027-03)**: Three buying-authority pilots (Goal G-1).
4. **GA (2027-04-30)**: G-Cloud listed; full evidence pack; pen test clean.
5. **Live + Hypercare (2027-04 to 2027-10)**: 24/7 SRE on-call; weekly R-008 / R-014 review.
6. **Cross-subsidy validation (2028-10-31)**: Goal G-3 break-even review.

## E3. Key Milestones

| Milestone | Target Date | Dependencies | Owner |
|-----------|-------------|--------------|-------|
| SOBC approval (this document) | 2026-06-30 | RISK + REQ + STKE at v1.0 (complete) | Service Owner |
| Alpha entry | 2026-07-15 | SOBC approved | Service Owner |
| Pilot DDaT EA (pilot 1) onboarded | 2026-09-30 | Alpha build sufficient for review | Service Owner |
| Private Beta | 2026-12-31 | Alpha pilot data | Steering Committee |
| OBC produced | 2027-01-31 | Alpha + private Beta evidence | Service Owner |
| Pen test pre-GA | 2027-03-15 | Beta build feature-complete | Security Lead |
| AI provider failover drill | 2027-03-15 | G-8 abstraction delivered | Lead Architect |
| Three pilot reviews complete (Goal G-1) | 2027-03-31 | Beta tenants onboarded | Service Owner |
| G-Cloud listing live | 2027-04-30 | Service definition + T&Cs + pricing | Product Manager + CCS liaison |
| **GA** | **2027-04-30** | All Gate-5 criteria met | Service Owner |
| FBC produced | 2027-04-30 | GA evidence | Service Owner |
| 12-month benefits review | 2028-04-30 | 12 months of BR-008 data | Service Owner |
| Cross-subsidy break-even (Goal G-3) | 2028-10-31 | BR-005 economics | Service Owner + Finance Lead |

**Critical path**:

1. AI integration + pluggable abstraction (G-8) — load-bearing for both R-006 mitigation and R-017.
2. Tenant isolation defence-in-depth (R-008 / R-014) — every other compliance posture builds on it.
3. G-Cloud listing iteration calendar (R SR-6) — fixed external deadline.
4. Three buying-authority pilot recruitment (R-003) — must complete by GA - 60 days.

## E4. Resource Requirements

**Core team (vendor side, FTE)**:

| Role | FTE (Year 0) | FTE (Year 1) | FTE (Year 2-3) |
|------|--------------|--------------|----------------|
| Service Owner / SRO-equivalent | 0.5 | 0.5 | 0.3 |
| Lead Architect / CTO | 1.0 | 1.0 | 0.7 |
| Engineers (full-stack + SRE) | 3.0 | 3.0 | 2.5 |
| Product Manager | 0.5 | 1.0 | 0.7 |
| Security Lead | 0.3 | 0.3 | 0.3 |
| DPO | 0.2 | 0.2 | 0.2 |
| Accessibility Lead (consultant) | 0.2 | 0.1 | 0.1 |
| Customer Success / Support | 0.0 | 0.5 | 1.0 |
| Finance / FinOps | 0.2 | 0.2 | 0.2 |
| **Total FTE** | **5.9** | **6.8** | **6.0** |

**Critical skills + gaps**:

- AI inference cost engineering (R-006 mitigation): vendor team has core competency; quarterly review with finance.
- Multi-tenant SaaS isolation (R-008 / R-014): in-team capability; supplemented by independent pen test.
- DDaT capability framework awareness (G-1): in-team capability + buying-authority pilot loop.
- WCAG 2.2 AA: consultant top-up Year 0-1; in-team after Beta.

## E5. Change Management

Per `ARC-001-STKE-v1.0.md` Communication & Engagement Plan and Change Impact Assessment:

- **Champions**: Service Owner; Lead Architect; pilot DDaT EAs.
- **Fence-sitters**: DDaT EAs at large departments with mature in-house EA — must be persuaded ArcKit complements rather than replaces.
- **Resisters**: Adjacent commercial EA tooling vendors (low influence); some SI suppliers benefitting from current SME assurance gap (no direct lever, market-driven response).
- **Engagement cadence**: Quarterly DDaT user group; quarterly CCS / CDDO liaison; in-product changelog per release; community forum for SME tenants.

## E6. Benefits Realisation

Each benefit traces to a stakeholder Goal in `ARC-001-STKE-v1.0.md`.

**Benefit B-001 — Large-enterprise tier revenue (cross-subsidy fund)**:

- Owner: Finance Lead with Service Owner.
- Baseline: £0 (pre-revenue).
- Target: £8.2M cumulative over 3 years.
- Measurement: Finance ledger; FinOps tagging per Principle 17; quarterly cost-to-serve report.
- Timeline: Cross-subsidy break-even at GA + 18 months (Goal G-3).

**Benefit B-002 — SME paid tier revenue**:

- Owner: Product Manager with Finance.
- Baseline: £0.
- Target: £0.30M cumulative (cost-recovery; not the primary revenue line).
- Measurement: SME-tier subscription telemetry.
- Note: B-002 is intentionally modest. The SME paid tier is priced for SME affordability; B-001 carries the financial weight.

**Benefit B-003 — Public value: SME-bid wins attributable to ArcKit-produced artefacts**:

- Owner: Service Owner.
- Baseline: 0 (pre-GA).
- Target: ~£4.6M cumulative attributable public value over 3 years.
- Measurement: Tenant case studies; G-Cloud callout records; survey of SMEs at 6 / 12 months post-GA.

**Benefit B-004 — Buyer-side assurance time saving**:

- Owner: Service Owner with pilot DDaT EAs.
- Baseline: Estimated 30-50% buyer-side assurance time per SME engagement (pilot to baseline).
- Target: Measurable reduction validated by pilots (Outcome O-1 KPI: >= 70% by GA + 12 months).
- Measurement: Buyer-side survey + pilot reports.

**Benefit B-005 — Compliance risk avoidance**:

- Owner: Security Lead + DPO.
- Baseline: Multi-tenant SaaS posture starting from green-field.
- Target: Outcome O-4 — zero cross-tenant incidents; zero ICO enforcement actions; zero confirmed breaches above notification threshold.

## E7. Risk Management — Reference to `ARC-001-RISK-v1.0.md` (Full Register)

The full risk register is incorporated by reference. The text below summarises the integration points with this SOBC; the live register is the source of truth.

### E7.1 Top 5 Risks (from RISK §B, ranked by residual then inherent)

| Rank | Risk ID | Risk Description | Category | Inherent | Residual | Owner | Status | Strategy |
|------|---------|------------------|----------|----------|----------|-------|--------|----------|
| 1 | R-001 | Cross-subsidy break-even fails by GA + 18 months | STRATEGIC | 16 | 9 | Service Owner with Finance Lead | In Progress | Treat |
| 2 | R-006 | AI inference cost overrun (FinOps) | FINANCIAL | 12 | 9 | Finance Lead | In Progress | Treat |
| 3 | R-014 | Tenant isolation defect (ADR-001) | TECHNOLOGY | 20 | 8 | Lead Architect | In Progress | Treat |
| 4 | R-002 | MOD sovereign-route divergence | STRATEGIC | 16 | 6 | Lead Architect | In Progress | Treat |
| 5 | R-008 | Cross-tenant data leakage (existential) | COMPLIANCE | 25 | 5 | Service Owner (SIRO-equivalent) | In Progress | Treat |

**Risks exceeding appetite** (per RISK §A.4 and §G):

- R-008 (residual 5, COMPLIANCE) — exceeds COMPLIANCE appetite (<=4) by 1 point — explicit acceptance by Service Owner / SIRO-equivalent + DPO + Security Lead per RISK Recommendation 2.
- R-009 (residual 6, COMPLIANCE) — exceeds by 2 — Service Owner acceptance with pre-assessment evidence walkthrough.
- R-010 (residual 6, COMPLIANCE — AI Playbook scope drift) — exceeds by 2 — Service Owner + DPO acceptance.
- R-011 (residual 6, COMPLIANCE — sub-processor) — exceeds by 2 — DPO acceptance.

### E7.2 Risk Appetite (RISK §G summary)

- **STRATEGIC**: Medium (<= 12) — within appetite at residual.
- **OPERATIONAL**: Low (<= 6) — within appetite at residual.
- **FINANCIAL**: Low-Medium (<= 9) — R-006 sits at appetite ceiling — monthly KRI required.
- **COMPLIANCE**: Very Low (<= 4) — 4 risks exceed by 1-2 points; explicit acceptance regime.
- **REPUTATIONAL**: Low-Medium (<= 6) — at or within appetite.
- **TECHNOLOGY**: Medium (<= 9) — within at residual; R-014 at 8 requires continuous pen-test cadence.

### E7.3 KRIs (RISK §J)

Leading: CI tenant-isolation pass rate (100% target); per-tenant AI cost variance (±15%); verified-SME share of free tier (>=90%); pen-test residual high findings (0 unmitigated > 30 days). Lagging: ICO correspondence (0); GDS Service Assessment outcome (pass at first review); cross-subsidy P&L variance vs plan (±10% by month 18).

### E7.4 Pre-GA Priority-1 Actions (RISK §H)

Estimated investment: £40k-£60k (pen test) + cyber-insurance premium + internal engineering effort. Eight discrete actions per RISK §H — must complete or be risk-accepted before GA Gate 5.

### E7.5 Risk Strategy Mix

Per RISK §F: predominantly **Treat** (mitigate); selective **Tolerate** for the at-floor compliance risks (R-008 in particular — likelihood already minimised, impact cannot be reduced); no **Terminate** (multi-tenant SaaS is the platform thesis); no **Transfer** apart from cyber insurance.

---

# PART F: RECOMMENDATION AND NEXT STEPS

## F1. Summary of Recommendation

**Recommended Option**: **Option 2 — Balanced Managed SaaS with Cross-Subsidy and G-Cloud Listing**

| Metric | Value |
|--------|-------|
| Investment (3-year, risk-adjusted) | **£5.04M** |
| Total benefits (3-year) | £13.65M (£8.2M financial + £4.6M public value + £0.55M operational + qualitative risk avoidance) |
| NPV (HMT 3.5%, after conservative trim) | **+£6.9M** |
| BCR | **~2.7** |
| Payback period from GA | **~22 months** |
| Cross-subsidy break-even (Goal G-3) | **GA + 18 months (target 2028-10-31)** |
| Stakeholder goals met | **~85%** |
| Top residual risks | R-001 (9), R-006 (9), R-008 (5) — all within or at appetite with explicit acceptance |
| Affordability | Conditional on adoption (BR-008); modelled mix clears cost-to-serve from quarter 5 post-GA |

**Go/No-Go Recommendation**: **PROCEED to Alpha (Gate 1) and to OBC conversion at Gate 3.**

## F2. Conditions for Approval

**Mandatory conditions** (Gate 0 -> Gate 1):

1. Service Owner approval of this SOBC and explicit acceptance of the residual COMPLIANCE risk position per `ARC-001-RISK-v1.0.md` §B Recommendation 2 (R-008, R-009, R-010, R-011).
2. Funding pathway confirmed for Year 0 build (£1.40M risk-adjusted).
3. Lead Architect, DPO, Security Lead countersign on RISK §H Priority-1 actions.

**Recommended conditions**:

1. CCS liaison engaged for G-Cloud listing iteration calendar (R SR-6).
2. First buying-authority pilot EA recruited by 2026-09-30 (Goal G-1; Risk SR-1 mitigation).
3. AI provider commercial terms finalised including no-training-on-tenant-data and 30-day sub-processor change notice clauses (Risk R-011).

## F3. Next Steps if Approved

**Immediate (Month 1, 2026-06)**:

1. SOBC sign-off + Service Owner acceptance of residual COMPLIANCE position.
2. Steering Committee convene (mandatory members per E1.1).
3. Refresh `/arckit:requirements` — REQ v1.1 to incorporate Alpha-stage refinements after pilot recruitment.

**Phase 1 — Alpha (2026-07 to 2026-12)**:

1. Run `/arckit:adr` for AI provider selection + pluggable abstraction (G-8 / Conflict C-2).
2. Run `/arckit:hld-review` once Alpha build emerges.
3. Recruit pilot DDaT EA (Goal G-1).

**Phase 2 — OBC conversion (2027-01)**:

1. Convert this SOBC to OBC using Alpha actuals — tighten cost ranges from ROM ±30% to ±15%.
2. Submit OBC to Steering Committee.

**Phase 3 — Private Beta (2027-01 to 2027-03)**:

1. Three buying-authority pilots running.
2. RISK §H Priority-1 actions complete.
3. Pen test + AI failover drill (Gate 4).

**Phase 4 — GA (2027-04-30)**:

1. G-Cloud listing live (BR-004).
2. Convert OBC to FBC.
3. Service Owner acceptance of residual position re-affirmed for live operation.

**Phase 5 — Live (2027-04 onwards)**:

1. Weekly R-008 / R-014 review.
2. Monthly cross-subsidy KRI tracking (R-001 / R-006).
3. Quarterly DDaT user group + CCS / CDDO liaison.
4. Cross-subsidy break-even review at GA + 18 months (Goal G-3).

## F4. Next Steps if Not Approved

1. Service Owner to convene with reviewers to understand objections.
2. Most plausible objections and pre-prepared responses:
   - "Costs too high" -> Option 1 (paid-only) — but rejected by Principle 1; alternative: defer non-critical items in Option 2 (compliance evidence pack hardening; accessibility programme top-up — both BLOCK if deferred).
   - "Adoption forecast (BR-008) too optimistic" -> sensitivity analysis at 100 SMEs shows NPV still positive (+£1.8M); Risk SR-2 mitigations in place.
   - "Cross-subsidy unproven" -> by design; Goal G-3 break-even is the test — proceed and review at GA + 18 months. Annual affordability review per BR-005 makes this a managed test, not a gamble.
3. Re-submit revised SOBC within 4 weeks if material objections received.

**Do Nothing consequences (Option 0)**:

- Procurement Act 2023 SME-spend objective remains structurally constrained.
- Principle 1 unfulfilled — exception register grows; reputational risk for the architecture programme.
- SME-side governance gap remains; large SI bias entrenched.

---

# APPENDICES

## Appendix A: Stakeholder Analysis

**Source**: `projects/001-arckit-saas/ARC-001-STKE-v1.0.md` (incorporated by reference).

Key stakeholders relevant to SOBC sign-off:

- Service Owner (Mark Craddock) — SRO-equivalent.
- Lead Architect / CTO (vendor).
- Security Lead, DPO, Finance Lead, Product Manager (vendor).
- DDaT Enterprise / Solution / Security Architects (buyer-side primary user-stakeholders).
- SME Architect + SME Founder / Bid Lead (commercial primary).
- CCS liaison; CDDO; GDS Assessors; NCSC; ICO (regulatory / standards).

## Appendix B: Architecture Principles (Source — `projects/000-global/ARC-000-PRIN-v2.0.md`)

Principles material to this SOBC:

- **Principle 1 — Equitable Access for SMEs Supplying Government (NON-NEGOTIABLE)**: defines the SaaS-route affordability commitment, free tier, transparent pricing, cross-subsidy; Project 002 sovereign-route is explicitly out of scope of Principle 1.
- **Principle 5 — Security by Design (NON-NEGOTIABLE)**: drives R-008 / R-014 controls and pre-GA pen-test gating.
- **Principle 7 — Data Sovereignty, Residency, and Governance (UK Context)**: drives UK-region cloud pinning and DPIA posture.
- **Principle 12 — Accessibility (NON-NEGOTIABLE for Public Sector)**: drives WCAG 2.2 AA programme, BR-006 evidence pack, Goal G-6.
- **Principle 17 — Cost Transparency and FinOps**: drives BR-005 cross-subsidy unit economics, transparent pricing, annual affordability review.
- **Principle 21 — Sovereign and Air-Gapped Deployment**: enforces single-codebase invariant — Project 001 (this SOBC) and Project 002 (separate SOBC) share the same codebase; engineering discipline is a binding constraint, not advisory.

## Appendix C: Options Analysis Details

ROM cost basis ±30% for Option 2; ±40% for Options 1 and 3. All options use the same blended HMT optimism-bias uplift (~12%, per RISK §I) for comparability.

Detailed line-items captured in Part D (CapEx + OpEx tables for Option 2). Options 1 and 3 use proportional adjustment from Option 2 baseline, with notes in Part B.

## Appendix D: Benefits Calculation

**B-001 Large-enterprise tier revenue**: Modelled on a small set of large-enterprise tenants (4-8 by Year 3) at published list prices, with the cross-subsidy unit economics targeted at large-enterprise revenue >= aggregate SME cost-to-serve at 200 verified SMEs.

**B-002 SME paid-tier revenue**: Modelled at modest cost-recovery margin for the SME paid tier, with conversion from SME free tier modelled at ~5-10% of activated free-tier tenants over 24 months.

**B-003 Public value (Procurement Act 2023 alignment)**: 200 verified SMEs at GA + 12 months (BR-008); attribution model: only the public-value uplift (additional supplier diversity, value-for-money) — not the SME revenue itself — counted to avoid double-attribution.

**Sensitivity analysis**: Part B5 above.

## Appendix E: Risk Register (Reference)

**Source**: `projects/001-arckit-saas/ARC-001-RISK-v1.0.md` (incorporated by reference per RISK §I and Part E above). Live document is the source of truth for residual scores, KRIs, mitigations, and acceptance trail.

## Appendix F: Market Research

UK Government SaaS / EA tooling landscape:

- Existing commercial EA tooling (LeanIX, Bizzdesign, Ardoa, etc.) priced for enterprises; structurally not addressable by SMEs at SME unit economics.
- Procurement Act 2023 SME-spend objective + Cabinet Office SME Action Plans create a sustained policy demand for SME-affordable supplier-side tooling.
- G-Cloud Lot 2 (Cloud Software) is the natural buyer route for managed SaaS.
- AI / LLM provider market: 3+ credible UK-region-capable providers — pluggable abstraction (G-8) is achievable.

## Appendix G: Governance Terms of Reference

Steering Committee:

- Chair: Service Owner (Mark Craddock).
- Members: Lead Architect / CTO; Security Lead; DPO; Finance Lead; Product Manager; CCS liaison (advisory); pilot DDaT EA representative (advisory at pilot stage).
- Frequency: Weekly pre-GA, monthly post-GA (with ad-hoc escalation for R-008 / R-014).
- Decision authority: Per E1.1 RACI matrix; Service Owner is accountable for SOBC -> OBC -> FBC conversions and GA gate.

## Appendix H: Glossary

| Term | Definition |
|------|------------|
| ArcKit | Architecture governance toolkit; the asset commercialised by this SOBC |
| BCR | Benefit-Cost Ratio (Total Benefits / Total Costs) |
| BR-001..008 | Business Requirements 1-8 — see `ARC-001-REQ-v1.0.md` |
| CAF | Cyber Assessment Framework (NCSC) |
| CDDO | Central Digital and Data Office |
| CCS | Crown Commercial Service |
| Cross-subsidy | Commercial model where large-enterprise tier revenue funds the SME tier — BR-005 |
| DDaT | Digital, Data and Technology profession (UK Government) |
| DPIA | Data Protection Impact Assessment — see `ARC-001-DPIA-v1.0.md` |
| FBC | Full Business Case — final stage with accurate costs |
| FinOps | Financial Operations discipline — Principle 17 |
| G-Cloud | UK Government Digital Marketplace framework — BR-004 |
| GDS | Government Digital Service |
| HMT | HM Treasury |
| ICO | Information Commissioner's Office |
| NCSC | National Cyber Security Centre |
| NPV | Net Present Value (HMT 3.5% discount) |
| OBC | Outline Business Case — second stage, after some design |
| OFFICIAL | UK Government data classification |
| Optimism bias | HMT Green Book uplift to costs to counter systematic under-estimation |
| Principle 1 | Equitable Access for SMEs Supplying Government (NON-NEGOTIABLE) |
| Procurement Act 2023 | UK Act driving SME spend share in public procurement |
| ROM | Rough Order of Magnitude |
| ROPA | Record of Processing Activities (UK GDPR) |
| SBD | Secure by Design — see `ARC-001-SBD-v1.0.md` |
| SME | Small and Medium Enterprise |
| SOBC | Strategic Outline Business Case (this document) |
| SRO | Senior Responsible Owner |
| TCO | Total Cost of Ownership |
| TCoP | Technology Code of Practice (UK Government) |
| VfM | Value for Money |
| WCAG 2.2 AA | Web Content Accessibility Guidelines, level AA |

---

## Document Approval

| Name | Role | Signature | Date |
|------|------|-----------|------|
| Mark Craddock | Service Owner / SRO-equivalent | | |
| [PENDING] | Lead Architect / CTO | | |
| [PENDING] | Security Lead (SIRO-equivalent) | | |
| [PENDING] | DPO | | |
| [PENDING] | Finance Lead | | |

**Approval Decision**: **APPROVED** | **APPROVED WITH CONDITIONS** | **REJECTED** | **DEFERRED**

**Conditions** (if any):

1. [PENDING completion of RISK §H Priority-1 actions before GA Gate 5]
2. [PENDING explicit Service Owner acceptance of residual COMPLIANCE position per RISK §B Recommendation 2]

**Approval Date**: [PENDING]

**Next Review Date**: 2027-01-31 (OBC conversion at Gate 3)

---

**END OF STRATEGIC OUTLINE BUSINESS CASE**

*Document created using ArcKit `/arckit:sobc` command.*
*Template version: 1.0.*
*Green Book compliant: Yes (HM Treasury 5-case model, with HMT optimism-bias uplift integrated per `ARC-001-RISK-v1.0.md` §I.)*

## External References

> No external policy PDFs were placed in `projects/001-arckit-saas/external/` at the time of generation. UK Government policies (Procurement Act 2023, HMT Green Book, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, UK GDPR / DPA 2018, PSBAR 2018, Companies Act 2006, TCoP) are public-domain and cited by name.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| INT-REQ | ARC-001-REQ-v1.0.md | Internal artefact | `projects/001-arckit-saas/` | Business and technical requirements (BR-001..008 + functional / NFR / data / integration) |
| INT-STKE | ARC-001-STKE-v1.0.md | Internal artefact | `projects/001-arckit-saas/` | Stakeholder Drivers and Goals (SD-1..14, G-1..8, O-1..7) |
| INT-RISK | ARC-001-RISK-v1.0.md | Internal artefact | `projects/001-arckit-saas/` | Risk Register (incorporated by reference into Part E) |
| INT-PRIN | ARC-000-PRIN-v2.0.md | Internal artefact | `projects/000-global/` | Architecture Principles (Principle 1 SME affordability; 17 FinOps; 21 sovereign-ready) |
| INT-DPIA | ARC-001-DPIA-v1.0.md | Internal artefact | `projects/001-arckit-saas/` | UK GDPR Article 35 DPIA |
| INT-SBD | ARC-001-SBD-v1.0.md | Internal artefact | `projects/001-arckit-saas/` | Secure by Design assessment |
| INT-TCOP | ARC-001-TCOP-v1.0.md | Internal artefact | `projects/001-arckit-saas/` | Technology Code of Practice review |
| INT-AIP | ARC-001-AIP-v1.0.md | Internal artefact | `projects/001-arckit-saas/` | UK Government AI Playbook compliance |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| INT-RISK-§I | INT-RISK | §I — Integration with SOBC | Optimism bias | "Total HMT optimism-bias add ~ 12% blended" — applied to all options uniformly in Part B / D |
| INT-REQ-BR-005 | INT-REQ | BR-005 Cross-Subsidy Funding Model | Commercial model | Cross-subsidy unit economics scope (Part B / D) |
| INT-PRIN-1 | INT-PRIN | §I — Principle 1 | Strategic anchor | SME-affordability NON-NEGOTIABLE — drives Option 1 rejection and Option 2 selection |
| INT-PRIN-17 | INT-PRIN | §V — Principle 17 | FinOps | Cost transparency, FinOps tagging, annual affordability review |
| INT-PRIN-21 | INT-PRIN | §V — Principle 21 | Sovereign | Single-codebase, two-deployment-route invariant; basis for separate Project 002 SOBC |
| INT-STKE-G-3 | INT-STKE | Goal G-3 | Cross-subsidy | Break-even at GA + 18 months; target 2028-10-31 |
| INT-STKE-O-1..7 | INT-STKE | Outcomes O-1..O-7 | Benefits realisation | Source of CSF-1..7 thresholds |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:sobc` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
