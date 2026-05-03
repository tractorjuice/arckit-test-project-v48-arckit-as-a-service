# Stakeholder Drivers & Goals Analysis: ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:stakeholders`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-STKE-v1.0 |
| **Document Type** | Stakeholder Drivers & Goals Analysis |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-08-03 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, MOD Defence Digital liaison, NCSC liaison, GDS, CDDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:stakeholders` command. Sovereign-deployment stakeholders, anchored on Principle 21 in `ARC-000-PRIN-v2.0.md` and the requirements in `ARC-002-REQ-v1.0.md` | [PENDING] | [PENDING] |

---

## Executive Summary

### Purpose

This document identifies the stakeholders for **ArcKit as a Service (Sovereign Deployment)** — Project 002 — and traces their underlying drivers through to measurable goals and outcomes. Unlike the sister project 001 (managed SaaS), where the primary commercial commitment is to SMEs and the principal external stakeholder group is the UK public-sector DDaT architecture community broadly, project 002's principal stakeholders are concentrated inside the **deploying authority's own accreditation chain**: MOD SROs, accreditors / authorising engineers (per JSP 604), SIROs, departmental security officers, and the cleared customer operator team that runs the deployment.

The analysis answers: who must accredit, who must operate, who must approve, and how we will know we have succeeded for each of them — within the constraints of an air-gapped, customer-controlled environment.

### Key Findings

- The **single load-bearing stakeholder** is the customer accreditor / authorising engineer. No other approval matters until accreditation completes; conversely, every other approval is contingent on it.
- **Two driver clusters** dominate: **accreditability** (customer accreditor, SIRO, DSO, NCSC, vendor security lead) and **operability** (customer operator team, customer SRO, vendor sovereign delivery lead, customer DDaT architects). These are largely synergistic but pull on opposite ends of the customisation/standardisation trade-off (Conflict C-1).
- The **vendor's commercial driver** here is unusual: sovereign revenue must positively contribute to the cross-subsidy that funds the project-001 SaaS SME tier. The sovereign track exists architecturally (Principle 21) and commercially (BR-006) to **serve the SaaS mission**, not to replace it.
- The **strongest synergy** is between the DDaT Security Architect, the customer accreditor, NCSC, and the vendor Security Lead — all want the same evidence-pack format. Investing once in NCSC CAF / MOD SbD-aligned evidence satisfies four stakeholders.

### Critical Success Factors

- A representative MOD or sensitive-site customer engaged before alpha completion, accreditor-in-the-loop on evidence-pack format.
- First production accreditation achieved on first attempt at the pilot customer (no rejection-and-rework cycle).
- Air-gap install / upgrade / backup / restore validated 100% per release before bundle issue.
- Single codebase preserved across SaaS and sovereign — zero per-customer forks.
- LTS commitment (24-month patching) honoured visibly from the first LTS line onwards.
- Sovereign unit economics positive and visibly contributing to the SaaS SME tier within the same financial year as first production deployment.

### Stakeholder Alignment Score

**Overall Alignment**: MEDIUM–HIGH

The principal customer-side stakeholders agree on the strategic outcome (a credible governance toolkit operable inside their boundary). The main alignment risks are: (a) per-customer feature demands that pressure the single-codebase commitment (Conflict C-1), and (b) vendor-side bandwidth tension between the sovereign track and the SaaS mission (Conflict C-6). Both have documented resolutions but require ongoing discipline.

---

## Stakeholder Identification

### Vendor-Side Internal Stakeholders

| Stakeholder | Role / Department | Influence | Interest | Engagement Strategy |
|-------------|-------------------|-----------|----------|---------------------|
| Mark Craddock | Service Owner / Sponsor | HIGH | HIGH | Decision authority; weekly steering |
| [PENDING] | Lead Architect / CTO | HIGH | HIGH | Single-codebase discipline; ADR review |
| [PENDING] | Security Lead | HIGH | HIGH | Supply-chain, signing, MOD SbD pack |
| [PENDING] | DPO | HIGH | MEDIUM | UK GDPR for vendor-side processing |
| [PENDING] | Sovereign Delivery Lead | MEDIUM | HIGH | Customer onboarding; remote-support model |
| [PENDING] | Product Manager (sovereign track) | MEDIUM | HIGH | LTS line; release cadence |
| [PENDING] | LTS Engineering Lead | MEDIUM | HIGH | Patch backports; SLA discipline |
| [PENDING] | Finance | HIGH | MEDIUM | Sovereign unit economics; cross-subsidy contribution |
| [PENDING] | Accessibility Lead | MEDIUM | MEDIUM | WCAG 2.2 AA parity with SaaS |
| [PENDING] | Vendor signing-key custodian (HSM) | MEDIUM | HIGH | Key custody; rotation; audit |

### Primary External Stakeholders — Deploying Authority Accreditation Chain

These are the load-bearing external stakeholders for project 002. They sit inside the customer organisation and operate under MOD / departmental security policy.

| Stakeholder | Role | Influence | Interest | Engagement Strategy |
|-------------|------|-----------|----------|---------------------|
| Customer SRO | Senior Responsible Owner — accountable to Parliament / department | HIGH | HIGH | Manage Closely — quarterly briefings, accreditation milestones |
| Customer Accreditor / Authorising Engineer | Issues authorisation to operate per JSP 604 (MOD) or departmental SbD process | HIGH | HIGH | Manage Closely — evidence-pack co-design; accreditator-in-the-loop pilot |
| Customer SIRO (GovS 007) | Owns information / cyber risk; signs risk acceptance | HIGH | HIGH | Manage Closely — risk register reviews; residual-risk discussions |
| Customer Departmental Security Officer (DSO) | Day-to-day security policy implementation | HIGH | MEDIUM | Keep Satisfied — policy-mapping reviews |
| Customer CISO | Departmental cyber security oversight | HIGH | MEDIUM | Keep Satisfied — quarterly briefings |
| Customer Operator Team (cleared personnel) | Platform / SRE inside the boundary | MEDIUM | HIGH | Manage Closely — runbook design; install rehearsals |

### Primary External Stakeholders — Deploying Authority User Community

| Stakeholder | Role | Influence | Interest | Engagement Strategy |
|-------------|------|-----------|----------|---------------------|
| Customer Enterprise Architect (DDaT) | Departmental architecture coherence | HIGH | HIGH | Manage Closely — architecture community engagement |
| Customer Solution Architect (DDaT) | Programme / project design | HIGH | HIGH | Manage Closely — design feedback loops |
| Customer Security Architect (DDaT) | Threat modelling, security control design | HIGH | HIGH | Manage Closely — assurance-evidence co-design |
| Customer Data Architect (DDaT) | Data governance and design | MEDIUM | MEDIUM | Keep Informed — data-model and DPIA features |
| Customer Technical Architect (DDaT) | Platform / infrastructure design | MEDIUM | MEDIUM | Keep Informed — diagrams, ADRs |
| Customer Business Architect (DDaT) | Business capability mapping | MEDIUM | LOW | Monitor |
| Customer Network Architect (DDaT) | Network design, segmentation | MEDIUM | MEDIUM | Keep Informed — deployment-view diagrams |
| Customer Service Owner (GovS 005) | End-to-end service responsibility | HIGH | MEDIUM | Keep Satisfied — service-quality metrics |
| Customer Product / Delivery Manager | Cadence, dependencies | MEDIUM | MEDIUM | Keep Informed — roadmap input |

### Cross-Government and Regulatory Stakeholders

| Stakeholder | Organisation | Power | Interest | Engagement Strategy |
|-------------|--------------|-------|----------|---------------------|
| MOD Defence Digital | UK MOD | HIGH | HIGH | Manage Closely — cross-MOD digital coherence; supplier diversification |
| NCSC | National Cyber Security Centre | HIGH | MEDIUM | Keep Satisfied — CAF / Cloud Security Principles / supply-chain |
| Defence Cyber Protection Partnership (DCPP) | MOD / industry partnership | MEDIUM | MEDIUM | Keep Informed — Cyber Risk Profile alignment |
| Crown Commercial Service (CCS) | UK Cabinet Office | HIGH | MEDIUM | Keep Satisfied — G-Cloud / DOS / DPS framework listings |
| MOD Commercial / Defence Equipment & Support (DE&S) | UK MOD | HIGH | LOW | Keep Satisfied — defence-specific procurement |
| HM Treasury | HMG | HIGH | LOW | Keep Satisfied — value for money; spend control |
| CDDO (Central Digital and Data Office) | Cabinet Office | HIGH | LOW | Keep Satisfied — digital spend controls |
| ICO | Independent regulator | HIGH | LOW | Keep Satisfied — UK GDPR posture where personal data |
| EHRC | Independent regulator | MEDIUM | LOW | Monitor — accessibility for citizen-facing deployments |

### Suppliers and Adjacent Parties

| Stakeholder | Organisation | Relationship | Power | Interest |
|-------------|--------------|--------------|-------|----------|
| HSM / signing-key custody provider | Commercial vendor | Supplier | MEDIUM | LOW |
| Approved on-prem AI / model provider | Commercial vendor (sovereign-eligible) | Optional supplier | LOW | LOW |
| Customer-side IdP / SIEM / KMS suppliers | Various | Customer-controlled (vendor configures against) | LOW | LOW |
| Adjacent EA tooling vendors (defence) | Various | Competitor | LOW | LOW (defensive) |

### Stakeholder Power-Interest Grid

```text
                          INTEREST
              Low                         High
        ┌─────────────────────┬─────────────────────┐
        │                     │                     │
        │   KEEP SATISFIED    │   MANAGE CLOSELY    │
   High │                     │                     │
        │  • Customer DSO     │  • Customer SRO     │
        │  • Customer CISO    │  • Customer         │
        │  • Customer Service │    Accreditor       │
        │    Owner            │  • Customer SIRO    │
        │  • CCS              │  • Customer EA / SA │
 P      │  • HM Treasury      │    / SecA (DDaT)    │
 O      │  • CDDO             │  • Service Owner    │
 W      │  • ICO              │    (vendor)         │
 E      │  • NCSC             │  • Lead Architect   │
 R      │  • DCPP             │    (vendor)         │
        │  • MOD Commercial   │  • Security Lead    │
        │                     │    (vendor)         │
        │                     │  • MOD Defence      │
        │                     │    Digital          │
        ├─────────────────────┼─────────────────────┤
        │                     │                     │
        │      MONITOR        │    KEEP INFORMED    │
   Low  │                     │                     │
        │  • EHRC             │  • Customer Operator│
        │  • Adjacent vendors │    Team             │
        │  • Suppliers (HSM,  │  • Customer Data /  │
        │    AI providers)    │    Tech / Network   │
        │  • Customer Business│    Architects       │
        │    Architect        │  • Sovereign        │
        │                     │    Delivery Lead    │
        │                     │  • LTS Engineering  │
        │                     │  • Product Manager  │
        │                     │    (sovereign)      │
        └─────────────────────┴─────────────────────┘
```

| Stakeholder | Power | Interest | Quadrant | Engagement Strategy |
|-------------|-------|----------|----------|---------------------|
| Service Owner (Mark Craddock) | HIGH | HIGH | Manage Closely | Weekly steering; decision authority |
| Lead Architect (vendor) | HIGH | HIGH | Manage Closely | Single-codebase discipline; ADR review |
| Security Lead (vendor) | HIGH | HIGH | Manage Closely | Supply-chain integrity; MOD SbD evidence |
| Customer SRO | HIGH | HIGH | Manage Closely | Quarterly briefings; accreditation milestones |
| Customer Accreditor | HIGH | HIGH | Manage Closely | Evidence-pack co-design; in-the-loop alpha |
| Customer SIRO | HIGH | HIGH | Manage Closely | Risk register; residual-risk discussions |
| Customer Enterprise Architect (DDaT) | HIGH | HIGH | Manage Closely | Architecture community; design partnerships |
| Customer Solution Architect (DDaT) | HIGH | HIGH | Manage Closely | Design feedback loops |
| Customer Security Architect (DDaT) | HIGH | HIGH | Manage Closely | Assurance evidence co-design |
| MOD Defence Digital | HIGH | HIGH | Manage Closely | Cross-MOD coherence; supplier diversification |
| Customer DSO | HIGH | MEDIUM | Keep Satisfied | Policy-mapping reviews |
| Customer CISO | HIGH | MEDIUM | Keep Satisfied | Quarterly briefings |
| Customer Service Owner (GovS 005) | HIGH | MEDIUM | Keep Satisfied | Service-quality metrics |
| NCSC | HIGH | MEDIUM | Keep Satisfied | CAF / Cloud Security mapping |
| CCS | HIGH | MEDIUM | Keep Satisfied | Framework listings |
| DCPP | MEDIUM | MEDIUM | Keep Informed | Cyber Risk Profile mapping |
| HM Treasury | HIGH | LOW | Keep Satisfied | Value-for-money narrative; cross-subsidy contribution |
| CDDO | HIGH | LOW | Keep Satisfied | Spend controls; standards |
| MOD Commercial / DE&S | HIGH | LOW | Keep Satisfied | Procurement liaison |
| ICO | HIGH | LOW | Keep Satisfied | UK GDPR posture where applicable |
| Customer Operator Team | MEDIUM | HIGH | Keep Informed | Runbook design; install rehearsals |
| Customer Data / Tech / Network Architects | MEDIUM | MEDIUM | Keep Informed | Quarterly user group |
| Sovereign Delivery Lead (vendor) | MEDIUM | HIGH | Keep Informed | Weekly customer-engagement review |
| LTS Engineering Lead (vendor) | MEDIUM | HIGH | Keep Informed | Sprint reviews; backport queue |
| Product Manager (sovereign, vendor) | MEDIUM | HIGH | Keep Informed | Roadmap synchronisation with SaaS |
| DPO (vendor) | HIGH | MEDIUM | Keep Satisfied | UK GDPR; vendor-side processing minimisation |
| Finance (vendor) | HIGH | MEDIUM | Keep Satisfied | Quarterly affordability and contribution review |
| Accessibility Lead (vendor) | MEDIUM | MEDIUM | Keep Informed | Parity with SaaS WCAG 2.2 AA conformance |
| Customer Business Architect | MEDIUM | LOW | Monitor | Roadmap newsletter |
| EHRC | MEDIUM | LOW | Monitor | Accessibility statement (citizen-facing deployments) |
| HSM / AI / supplier vendors | LOW–MEDIUM | LOW | Monitor | Quarterly vendor reviews |

---

## Stakeholder Drivers Analysis

### SD-1: Customer Accreditor / Authorising Engineer — Defensible Authorisation to Operate

**Stakeholder**: Accreditor / Authorising Engineer at the deploying authority (per JSP 604 for MOD; equivalent role under departmental SbD for civilian sensitive sites).

**Driver Category**: COMPLIANCE + RISK + PERSONAL.

**Driver Statement**: "I need to issue a defensible authorisation to operate within an accreditation timeline that does not slip. Vendor evidence must map directly to my framework — JSP 604 / JSP 440 / NCSC CAF — without my team having to translate it."

**Context & Background**: The accreditor is the single load-bearing role for sovereign deployment. Their decision is contestable at audit, and they live with the consequences if they get it wrong. Vendor evidence packs that are framework-shaped but not framework-mapped extend the accreditation cycle by months and create personal risk.

**Driver Intensity**: CRITICAL.

**Enablers**:

- MOD SbD evidence pack provided per release (`/arckit:mod-secure`).
- NCSC CAF mapping per release.
- Signed SBOM (CycloneDX or SPDX), hash inventory, signed manifests.
- Customer-side SAL template ready to populate.
- Accreditator-in-the-loop alpha programme (vendor invites the accreditor to review evidence format before formal submission).

**Blockers**:

- Generic "ISO 27001-shaped" vendor evidence not mapped to MOD frameworks.
- Unsigned bundles or unverifiable cryptographic provenance.
- Bespoke evidence formats varying release to release.

**Related Stakeholders**: SD-2 (SIRO), SD-3 (DSO), SD-9 (Security Lead, vendor), SD-15 (NCSC).

---

### SD-2: Customer SIRO — Defensible Information Risk Acceptance

**Stakeholder**: Senior Information Risk Owner at the deploying authority (GovS 007).

**Driver Category**: COMPLIANCE + RISK + PERSONAL.

**Driver Statement**: "I sign the residual-risk acceptance. I need a complete, current information-risk picture, including supply-chain risk and the implications of each cryptographic and AI choice — and I need to revisit it on every material change."

**Context & Background**: SIROs are personally accountable for information risk. Surprises that surface during accreditation, after they have already signed, are career-defining events.

**Driver Intensity**: CRITICAL.

**Enablers**:

- Comprehensive threat model per release.
- Explicit cryptographic provenance (HMG-approved primitives where mandated).
- Pluggable AI / model endpoint with the default profile pointing nowhere (no implicit data egress).
- Vendor-side incident-response runbook compatible with customer-side incident reporting.

**Blockers**:

- Supply-chain blind spots (un-attested dependencies).
- Vendor-imposed remote-access defaults.
- AI / model integrations with implicit external endpoints.

**Related Stakeholders**: SD-1, SD-3, SD-9.

---

### SD-3: Customer DSO — Departmental Security Policy Fit

**Stakeholder**: Departmental Security Officer (GovS 007).

**Driver Category**: COMPLIANCE + OPERATIONAL.

**Driver Statement**: "Day-to-day, I need ArcKit's behaviour to fit our departmental security policy — clearance enforcement, classification marking, audit logging to our SIEM, key management within our HSM."

**Driver Intensity**: HIGH.

**Enablers**:

- Configurable maximum classification (FR-012), cleared-personnel claim enforcement (FR-007).
- Audit logging to a customer-controlled destination (FR-010).
- Customer-controlled key management (INT-007).

**Blockers**:

- Hard-coded classification ceilings or audit destinations.
- Vendor-managed keys.

**Related Stakeholders**: SD-1, SD-2.

---

### SD-4: Customer SRO — Delivery Within Accreditation Timeline

**Stakeholder**: Senior Responsible Owner at the deploying authority (GovS 005).

**Driver Category**: STRATEGIC + RISK + PERSONAL.

**Driver Statement**: "The deployment must achieve authority-to-operate within my programme timeline, with no surprises that escalate to me late. Accreditation slippage means programme slippage."

**Driver Intensity**: CRITICAL.

**Enablers**:

- Predictable accreditation timeline driven by quality of evidence pack (links to SD-1).
- Vendor-side delivery cadence aligned with customer programme milestones.
- Regular SRO-level briefings on accreditation progress.

**Blockers**:

- Late-surfacing accreditation findings.
- Vendor-side LTS slips that force unscheduled customer upgrades.

**Related Stakeholders**: SD-1, SD-11 (vendor Sovereign Delivery Lead).

---

### SD-5: Customer Operator Team (Cleared Personnel) — Predictable Operations Inside the Boundary

**Stakeholder**: Customer-side platform / SRE team — the people who actually run the deployment.

**Driver Category**: OPERATIONAL + PERSONAL.

**Driver Statement**: "I need install, upgrade, backup, restore, key rotation, incident response, and decommission to all be defined runbooks I can execute inside the boundary, every time, with predictable outcomes — and I need them to keep working when the vendor is not on the call."

**Context & Background**: Customer operators carry the cognitive load of every system inside the boundary. Vendor systems that "just work on the internet" but break offline drain operator time and erode trust. Predictability is the operator's currency.

**Driver Intensity**: HIGH.

**Enablers**:

- Operator runbook library shipped per release (FR-011).
- Disconnected-mode validation in CI per release (BR-002).
- LTS line decoupled from SaaS feature cadence (BR-005).
- Self-sufficient support model with optional, audited remote channel (FR-013).

**Blockers**:

- Hidden dependencies (phone-home, package-mirror assumptions).
- Frequent forced upgrades.
- Vendor support that requires breaking accreditation.

**Related Stakeholders**: SD-1, SD-3, SD-4, SD-11.

---

### SD-6: Customer DDaT Architects (Inside the Boundary) — Same Drivers as Project 001 SD-1 to SD-5, Adapted

**Stakeholder**: Enterprise / Solution / Security / Data / Technical / Network / Business Architects working inside the deploying authority.

**Driver Category**: OPERATIONAL + COMPLIANCE.

**Driver Statement**: "I want the same DDaT-recognisable artefact set inside my accredited boundary that my colleagues elsewhere in government use on the SaaS — same templates, same conventions, same quality bar — without external dependencies that breach my accreditation."

**Context & Background**: Architects in MOD and sensitive sites are part of the same DDaT capability framework as their colleagues in civilian departments. They lose if the sovereign deployment is a stripped-down "community edition" — they want full feature parity.

**Driver Intensity**: HIGH.

**Enablers**:

- Single codebase preserved (BR-001).
- Same artefact set in sovereign as in SaaS (FR-008).
- Same `ARC-{PROJECT}-{TYPE}-v{VERSION}` document conventions.
- AI-assisted generation available where the customer enables it (FR-004).

**Blockers**:

- Per-customer feature drift (Conflict C-1 risk).
- Forked sovereign code lagging the SaaS feature set.

**Related Stakeholders**: SD-7 (MOD Defence Digital), project 001 SD-1 to SD-5 (analogous roles in civilian departments).

---

### SD-7: MOD Defence Digital — Cross-MOD Digital Coherence and Supplier Diversification

**Stakeholder**: MOD Defence Digital function.

**Driver Category**: STRATEGIC.

**Driver Statement**: "Promote cross-MOD digital coherence by encouraging the use of recognisable governance artefacts across MOD programmes, while supporting supplier diversification including SMEs supplying MOD."

**Context & Background**: MOD Defence Digital sits across the cross-MOD digital portfolio and has a strategic interest in supplier diversification (mirroring HMG SME spend ambition but in defence-specific frameworks). ArcKit's sovereign route is a credibility bridge: SMEs that bid for MOD work using SaaS-produced artefacts can demonstrate that the same toolkit is acceptable for the most sensitive deployments.

**Driver Intensity**: HIGH.

**Enablers**:

- ArcKit sovereign deployments inside MOD with positive accreditation outcomes.
- Single-codebase track record (no fork).
- Clear narrative connecting SaaS / sovereign reuse to defence supplier diversification.

**Blockers**:

- Sovereign deployment that is materially divergent from SaaS.
- Supplier-diversification narrative blocked by accreditation friction.

**Related Stakeholders**: SD-4 (Customer SRO), SD-15 (NCSC), SD-17 (HM Treasury / CCS / DCPP).

---

### SD-8: Vendor Service Owner (Mark Craddock) — Sovereign Funds Mission, Not Distracts From It

**Stakeholder**: ArcKit as a Service Owner / Sponsor.

**Driver Category**: STRATEGIC + PERSONAL + FINANCIAL.

**Driver Statement**: "Make the sovereign track succeed commercially so that it visibly contributes to the SaaS SME tier (project 001 BR-005) — without letting sovereign demands distract engineering from the core mission of cheap, credible governance tooling for SMEs."

**Context & Background**: The Service Owner deliberately separated sovereign as a sister project (project 002, separate REQ from project 001) to preserve clarity. Sovereign exists to fund the mission, not to redirect it.

**Driver Intensity**: CRITICAL.

**Enablers**:

- BR-001 single-codebase discipline (no engineering bifurcation).
- BR-006 cost-recovery-plus-margin pricing.
- Quarterly cross-project review aligning sovereign delivery with SaaS roadmap.

**Blockers**:

- Sovereign customer feature requests displacing SaaS roadmap.
- Sovereign engineering bandwidth absorbing capacity that the SaaS depends on.

**Related Stakeholders**: SD-9 (Lead Architect), SD-12 (Finance), Conflict C-6.

---

### SD-9: Vendor Lead Architect / CTO — Single-Codebase and Sovereign-Ready Engineering

**Stakeholder**: Lead Architect / CTO at the ArcKit vendor.

**Driver Category**: OPERATIONAL + STRATEGIC + PERSONAL.

**Driver Statement**: "Maintain one codebase that runs both SaaS and sovereign without forking. Every dependency, every default, every integration must support offline operation — that is the engineering line in the sand."

**Driver Intensity**: HIGH.

**Enablers**:

- Pluggable abstractions where SaaS and sovereign behaviour diverge (AI endpoint, telemetry, IdP, time, CA, package mirror).
- Disconnected-mode test profile in CI run on every release.
- Refactoring budget for offline-readiness when new components are adopted.

**Blockers**:

- Time-to-market pressure resulting in SaaS-only integrations.
- Customer-specific feature requests that pressure forking.

**Related Stakeholders**: SD-8, SD-10 (Security Lead), Conflict C-1.

---

### SD-10: Vendor Security Lead — Supply-Chain Integrity and Signing-Key Custody

**Stakeholder**: Vendor Security Lead.

**Driver Category**: COMPLIANCE + RISK + PERSONAL.

**Driver Statement**: "Maintain supply-chain integrity end-to-end: every artefact entering a customer boundary signed; SBOM current; hash inventory verifiable; signing keys protected by HSM with documented custody and rotation."

**Context & Background**: A signing-key compromise is, for sovereign, a worst-of-worst incident — every customer accreditation is in question simultaneously. The Security Lead lives that risk personally.

**Driver Intensity**: CRITICAL.

**Enablers**:

- HSM-backed signing infrastructure.
- Documented key-custody policy with separation of duties.
- Annual independent attestation of signing infrastructure.
- Independent pen testing of release pipeline.

**Blockers**:

- Cost pressure on HSM / attestation.
- Key custody concentrated in one individual.

**Related Stakeholders**: SD-1, SD-9, SD-15.

---

### SD-11: Vendor Sovereign Delivery Lead — Predictable Customer Onboarding

**Stakeholder**: Vendor-side Sovereign Delivery Lead (new role for project 002).

**Driver Category**: OPERATIONAL + PERSONAL.

**Driver Statement**: "Deliver a predictable customer onboarding experience: from initial engagement, through accreditation support, through first install, through first upgrade — with clear handovers to the customer operator team."

**Driver Intensity**: HIGH.

**Enablers**:

- Standard accreditation evidence pack (`/arckit:mod-secure`).
- Standard onboarding runbook.
- LTS commitment respected (links to SD-13).

**Blockers**:

- Customer demands that require codebase forks.
- LTS slips that force unscheduled customer interventions.

**Related Stakeholders**: SD-4 (Customer SRO), SD-5 (Customer Operator Team), SD-13 (vendor LTS Engineering Lead).

---

### SD-12: Vendor Finance — Sovereign Unit Economics Positive and Contributing

**Stakeholder**: Vendor Finance Lead.

**Driver Category**: FINANCIAL + STRATEGIC.

**Driver Statement**: "Sovereign deployments must recover full cost-to-serve plus a margin that visibly contributes to the cross-subsidy funding the SaaS SME tier. The contribution must be auditable and reportable to HM Treasury and CCS as part of the value-for-money narrative."

**Driver Intensity**: HIGH.

**Enablers**:

- Documented per-customer cost-to-serve model (engineering, support, accreditation effort, signing infrastructure, LTS backporting).
- Quarterly affordability and contribution review.
- Sovereign pricing floor below which Service Owner approval required.

**Blockers**:

- Pricing concessions to win the first reference customer that undermine the floor.
- Hidden customer-specific engineering costs absorbed without margin.

**Related Stakeholders**: SD-8, SD-17 (HM Treasury / CCS).

---

### SD-13: Vendor LTS Engineering Lead — Patch Backport Discipline

**Stakeholder**: Vendor LTS Engineering Lead.

**Driver Category**: OPERATIONAL + COMPLIANCE.

**Driver Statement**: "Maintain LTS lines for ≥ 24 months from issue with documented patch SLAs (Critical 7d / High 30d / Medium 90d) without backporting features."

**Driver Intensity**: HIGH.

**Enablers**:

- Disciplined LTS scope (security and critical-bug fixes only).
- CI infrastructure that runs the disconnected profile against each LTS line.
- Resource allocation protected from feature-development pressure.

**Blockers**:

- Customer pressure for feature backports.
- Resource pressure from SaaS roadmap.

**Related Stakeholders**: SD-9, SD-11, SD-5.

---

### SD-14: Vendor DPO — UK GDPR Posture for Vendor-Side Processing

**Stakeholder**: Vendor DPO.

**Driver Category**: COMPLIANCE + RISK.

**Driver Statement**: "Minimise vendor-side processing of customer data — sovereign customers run their own deployment; the vendor should generally never see customer artefact content. Where vendor-side processing is unavoidable (telemetry from vendor-hosted CI, support-channel data when activated), keep ROPA and DPIA current."

**Driver Intensity**: MEDIUM.

**Enablers**:

- Default sovereign profile sends no telemetry to vendor.
- Opt-in audited remote support (FR-013) with explicit DPIA when first activated by a customer.

**Blockers**:

- Telemetry leakage from internal vendor tooling.
- Insufficient DPIA discipline for new support modalities.

**Related Stakeholders**: SD-10, SD-16 (ICO).

---

### SD-15: NCSC — UK Cyber Resilience Baseline

**Stakeholder**: National Cyber Security Centre.

**Driver Category**: STRATEGIC + COMPLIANCE.

**Driver Statement**: "Raise the UK cyber-resilience baseline; encourage adoption of CAF and Cloud Security Principles; promote good supply-chain practice across UK government suppliers."

**Driver Intensity**: HIGH (regulatory).

**Enablers**:

- Public, accurate, current evidence of CAF mapping per release.
- Adoption of NCSC supply-chain guidance for the signed-bundle model.
- Vulnerability disclosure programme (NFR-SEC-008) aligned with NCSC guidance.

**Blockers**:

- CAF mapping out of date.
- Material changes without re-assessment.

**Related Stakeholders**: SD-1, SD-10, SD-17.

---

### SD-16: ICO — UK GDPR Where Personal Data Is Processed

**Stakeholder**: Information Commissioner's Office.

**Driver Category**: COMPLIANCE + STRATEGIC.

**Driver Statement**: "Maintain a high standard of UK GDPR / DPA 2018 compliance. Where sovereign deployments process personal data, the deploying authority is primarily responsible, but the vendor's processor commitments must be defensible."

**Driver Intensity**: MEDIUM (vendor-side; the customer is the data controller for their own data).

**Enablers**:

- Up-to-date vendor-side ROPA and DPIA inputs.
- Article 28 processor terms in customer contracts.
- Sub-processor list current.

**Related Stakeholders**: SD-14.

---

### SD-17: HM Treasury, CCS, CDDO, DCPP — Public Spending and Defence Cyber

**Stakeholder**: HM Treasury (value for money), CCS (frameworks), CDDO (digital spend controls), DCPP (defence cyber risk profile).

**Driver Category**: FINANCIAL + STRATEGIC + COMPLIANCE.

**Driver Statement**: "Increase value for money and supplier diversity in public spending; maintain digital and security standards; for defence specifically, conform to the Defence Cyber Protection Partnership Cyber Risk Profile."

**Driver Intensity**: HIGH.

**Enablers**:

- G-Cloud / DOS / DPS listings (BR-007).
- Quantitative evidence of sovereign cross-subsidy contribution (SD-12).
- DCPP Cyber Risk Profile mapping.

**Related Stakeholders**: SD-7 (MOD Defence Digital), SD-12.

---

## Driver-to-Goal Mapping

### Goal G-1: First Production Sovereign Deployment (Reference)

**Derived From Drivers**: SD-1, SD-2, SD-4, SD-5, SD-7, SD-8, SD-11.

**Goal Owner**: Service Owner with Sovereign Delivery Lead.

**Goal Statement**: Achieve first production sovereign deployment at an MOD or comparable sensitive-site customer with positive accreditation outcome by GA + 18 months, with the customer willing to act as a reference (subject to accreditation constraints on disclosure).

**Success Metrics**: ≥ 1 production deployment with ATO; reference case study published (subject to consent).
**Baseline**: 0 (pre-GA).
**Target**: GA + 18 months.
**Risks**: Accreditation cycle longer than estimated; customer-specific features required; signing-infrastructure delays.

---

### Goal G-2: Single-Codebase Discipline Maintained

**Derived From Drivers**: SD-6, SD-7, SD-8, SD-9, project 001 SD-9.

**Goal Owner**: Lead Architect.

**Goal Statement**: Maintain one source-of-truth codebase serving both SaaS and sovereign deployment, with zero per-customer forks and zero permanent feature divergence.

**Success Metrics**: Quarterly review confirms zero forks; feature-flag inventory reviewed and trimmed; same artefact set across modes.

---

### Goal G-3: Air-Gap Operability Validated Per Release

**Derived From Drivers**: SD-2, SD-5, SD-9.

**Goal Owner**: Lead Architect with LTS Engineering Lead.

**Goal Statement**: Air-gap install, upgrade (forward and roll-back), backup, restore validated end-to-end in CI representative environment 100% per release before bundle issue.

**Success Metrics**: 100% pass rate per release; documented evidence in release notes.

---

### Goal G-4: MOD Secure by Design Evidence Pack Current

**Derived From Drivers**: SD-1, SD-2, SD-3, SD-10, SD-15.

**Goal Owner**: Vendor Security Lead.

**Goal Statement**: MOD Secure by Design evidence pack current per release; NCSC CAF mapping current per release; SBOM, signed manifests, hash inventory, threat model included in bundle.

**Success Metrics**: Pack dated within last release; pack delivered with every bundle.

---

### Goal G-5: LTS Line Maintained for ≥ 24 Months

**Derived From Drivers**: SD-4, SD-5, SD-13.

**Goal Owner**: Vendor Product Manager (sovereign track) with LTS Engineering Lead.

**Goal Statement**: Each LTS release line supported with security patches at documented SLAs (Critical 7d / High 30d / Medium 90d) for ≥ 24 months from issue; LTS deprecation notice ≥ 12 months ahead.

**Success Metrics**: SLA adherence reported quarterly; deprecation notices issued on schedule.

---

### Goal G-6: Sovereign Cross-Subsidy Contribution

**Derived From Drivers**: SD-8, SD-12, SD-17.

**Goal Owner**: Service Owner with Finance.

**Goal Statement**: Sovereign deployments collectively recover full cost-to-serve plus contribution margin that visibly funds the SaaS SME tier within the same financial year as the first production sovereign deployment.

**Success Metrics**: Quarterly affordability and contribution report shows positive contribution; reportable to HM Treasury / CCS.

---

### Goal G-7: First-Time Accreditation Pass

**Derived From Drivers**: SD-1, SD-4, SD-11.

**Goal Owner**: Sovereign Delivery Lead with Vendor Security Lead.

**Goal Statement**: First customer accreditation cycle achieves ATO on first attempt — no rejection-and-rework cycle.

**Success Metrics**: ATO issued on first submission; lessons captured for subsequent customers.
**Why**: Accreditator-in-the-loop alpha programme (engaging an accreditor before formal submission) is the most reliable way to achieve this.

---

### Goal G-8: Signing-Key Custody Zero-Incident

**Derived From Drivers**: SD-1, SD-10.

**Goal Owner**: Vendor Security Lead with Signing-Key Custodian.

**Goal Statement**: Zero signing-key compromise events; HSM-backed signing infrastructure with documented custody, separation of duties, annual rotation, and annual independent attestation.

**Success Metrics**: 0 incidents; annual attestation report current.

---

### Goal G-9: NCSC CAF Mapping Per Release

**Derived From Drivers**: SD-1, SD-15.

**Goal Owner**: Vendor Security Lead.

**Goal Statement**: NCSC CAF mapping current per release; refreshed on material change; published with the evidence pack.

---

### Goal G-10: Customer-Led Operability

**Derived From Drivers**: SD-3, SD-5, SD-11.

**Goal Owner**: Sovereign Delivery Lead.

**Goal Statement**: Customer operator teams execute install / upgrade / backup / restore / key rotation / decommission without vendor remote intervention except via opt-in audited channel.

**Success Metrics**: Zero unscheduled vendor remote interventions for accreditation-critical operations after first install.

---

## Goal-to-Outcome Mapping

### Outcome O-1: Reference Customer Endorsement

**Supported Goals**: G-1, G-4, G-7, G-9.

**Outcome Statement**: At least one MOD or comparable sensitive-site customer in production with positive accreditation outcome and willing to endorse the sovereign offering (subject to accreditation-related disclosure constraints).

**KPI**: Production deployments with ATO. **Target**: ≥ 1 by GA + 18 months. **Lagging indicator**: subsequent customer engagements citing the reference.

---

### Outcome O-2: Single-Codebase Track Record

**Supported Goals**: G-2, G-3.

**Outcome Statement**: Single codebase serves both SaaS and sovereign across all releases — zero forks, zero permanent divergence — proving Principle 21 in production.

**KPI**: Forks count (target: 0); feature-flag inventory size (target: monotonically declining or stable).

---

### Outcome O-3: Sovereign Cross-Subsidy Contribution Proven

**Supported Goals**: G-6.

**Outcome Statement**: Sovereign revenue measurably contributes to the SaaS SME tier funding model; HM Treasury / CCS able to point to the cross-subsidy as evidence of value for money.

**KPI**: Quarterly contribution figure published; year-on-year growth in absolute and relative terms.

---

### Outcome O-4: Air-Gap Operability Proven Across Releases

**Supported Goals**: G-3, G-5.

**Outcome Statement**: Disconnected install / upgrade / backup / restore validated 100% per release in a representative isolated CI environment before any bundle is issued to a customer.

**KPI**: Per-release pass rate; cumulative releases without an air-gap regression.

---

### Outcome O-5: First-Time Accreditation Pass Rate

**Supported Goals**: G-7.

**Outcome Statement**: New customers achieve ATO on first formal accreditation submission, evidencing maturity of the evidence pack and the accreditator-in-the-loop programme.

**KPI**: First-time pass rate (target: ≥ 80% across cumulative customers).

---

### Outcome O-6: Customer-Led Operability

**Supported Goals**: G-10.

**Outcome Statement**: Customer operator teams routinely execute accreditation-critical operations without vendor remote intervention, evidencing runbook quality.

**KPI**: Unscheduled remote-support invocations per customer per quarter (target: 0 for accreditation-critical operations).

---

### Outcome O-7: Zero Supply-Chain Incidents

**Supported Goals**: G-4, G-8, G-9.

**Outcome Statement**: Zero signing-key compromise; zero supply-chain incidents traced to vendor artefacts.

**KPI**: Incident count (target: 0); annual attestation current.

---

## Complete Traceability Matrix

### Stakeholder → Driver → Goal → Outcome

| Stakeholder | Driver ID | Driver Summary | Goal ID | Goal Summary | Outcome ID |
|-------------|-----------|----------------|---------|--------------|------------|
| Customer Accreditor | SD-1 | Defensible ATO | G-1, G-4, G-7, G-9 | Reference + evidence + first-pass + CAF | O-1, O-5, O-7 |
| Customer SIRO | SD-2 | Defensible risk acceptance | G-3, G-4 | Air-gap + evidence | O-4, O-5, O-7 |
| Customer DSO | SD-3 | Departmental policy fit | G-3, G-10 | Air-gap + customer-led ops | O-4, O-6 |
| Customer SRO | SD-4 | Delivery in timeline | G-1, G-5, G-7 | Reference + LTS + first-pass | O-1, O-5 |
| Customer Operator Team | SD-5 | Predictable ops | G-3, G-5, G-10 | Air-gap + LTS + customer-led ops | O-4, O-6 |
| Customer DDaT Architects | SD-6 | DDaT-recognisable parity | G-2 | Single codebase | O-2 |
| MOD Defence Digital | SD-7 | Cross-MOD coherence | G-1, G-2 | Reference + single codebase | O-1, O-2 |
| Vendor Service Owner | SD-8 | Mission-funding | G-1, G-2, G-6 | Reference + codebase + contribution | O-1, O-2, O-3 |
| Vendor Lead Architect | SD-9 | Single codebase | G-2, G-3 | Codebase + air-gap | O-2, O-4 |
| Vendor Security Lead | SD-10 | Supply chain | G-4, G-8, G-9 | Evidence + signing + CAF | O-7 |
| Vendor Sovereign Delivery Lead | SD-11 | Customer onboarding | G-1, G-7, G-10 | Reference + first-pass + customer-led | O-1, O-5, O-6 |
| Vendor Finance | SD-12 | Unit economics | G-6 | Contribution | O-3 |
| Vendor LTS Engineering Lead | SD-13 | LTS discipline | G-5 | LTS | O-4 |
| Vendor DPO | SD-14 | UK GDPR posture | G-4 | Evidence | O-7 |
| NCSC | SD-15 | Cyber baseline | G-4, G-8, G-9 | Evidence + signing + CAF | O-7 |
| ICO | SD-16 | UK GDPR | G-4 | Evidence | O-7 |
| HM Treasury / CCS / CDDO / DCPP | SD-17 | Spending and defence cyber | G-1, G-6 | Reference + contribution | O-1, O-3 |

### Conflict Analysis

**Competing Drivers**:

- **Conflict 1 — Per-customer demands vs single codebase**. SD-1 / SD-3 may push for bespoke evidence formats or behaviour to fit local policy; SD-9 / SD-7 / SD-8 require single codebase. **Resolution**: per `ARC-002-REQ-v1.0.md` Conflict C-1 — configuration-only customisation, no per-customer code branches. New customer requirement either fits within existing configuration surface or triggers a configuration extension that benefits all customers. Decision authority: Lead Architect with Service Owner.

- **Conflict 2 — LTS stability vs SaaS feature velocity**. SD-5 / SD-13 / SD-4 want LTS stability; project 001 stakeholders want SaaS feature velocity. **Resolution**: per REQ Conflict C-2 — LTS accepts security and critical-bug fixes only; features land in `main` and are available in the next LTS. Customers choose their LTS upgrade cadence.

- **Conflict 3 — Customer self-sufficiency vs vendor support**. SD-3 / SD-5 want operator-only operation; SD-11 needs effective support. **Resolution**: per REQ Conflict C-3 — opt-in audited remote channel + reproducible synthetic environments inside vendor infrastructure.

- **Conflict 4 — AI generation richness vs disconnected operation**. SD-6 / project 001 SD-1 want AI generation; SD-2 / SD-5 / SD-9 require offline default. **Resolution**: per REQ Conflict C-4 — pluggable AI endpoint, sovereign default points nowhere, customer-controlled approved endpoint optional.

- **Conflict 5 — First-customer pricing concession vs cross-subsidy floor**. To win the first reference customer (G-1), pricing concessions might be tempting; they would erode the cross-subsidy contribution (G-6). **Resolution**: PRIORITIZE — reference customers may receive non-cash concessions (joint case studies, design partnership) but pricing remains at or above documented floor. Service Owner approval required for any below-floor pricing.

- **Conflict 6 — Sovereign track demands vs SaaS strategic mission bandwidth**. SD-11 / SD-13 want engineering capacity; SD-8 / project 001 SD-8 want SaaS feature velocity. **Resolution**: PHASE / PRIORITIZE — separate track ownership at engineering level (LTS team distinct from SaaS feature team); sovereign demand backlog managed by Sovereign Product Manager; quarterly SaaS / sovereign roadmap review by Service Owner protects SaaS roadmap from sovereign-driven displacement.

**Synergies**:

- **Synergy 1**: SD-1, SD-3, SD-10, SD-15 align on MOD SbD / NCSC CAF evidence — one investment serves four stakeholders.
- **Synergy 2**: SD-4, SD-5, SD-11 align on predictable delivery and operations — runbook quality, LTS discipline, and cadence serve all three.
- **Synergy 3**: SD-7, SD-8, SD-17 align on supplier-diversification narrative — sovereign deployments inside MOD strengthen the cross-subsidy narrative for HM Treasury / CCS.
- **Synergy 4**: SD-6 (Customer DDaT architects) aligns with project 001 SD-1 to SD-5 (analogous roles in civilian departments) — same artefact set, same conventions, same quality bar.

---

## Communication & Engagement Plan

### Customer-Side Accreditation Chain (SROs, Accreditors, SIROs, DSOs)

**Primary Message**: "ArcKit's sovereign deployment ships with a current MOD Secure by Design / NCSC CAF evidence pack and a signed, hashed, SBOM-backed bundle. Engage your accreditor early; we will support an accreditator-in-the-loop alpha programme to validate evidence format before formal submission."

**Frequency**: Quarterly briefings; per-release evidence-pack updates.
**Channels**: MOD Defence Digital community; cross-government EA / accreditor communities; direct customer engagement.

---

### Customer Operator Team

**Primary Message**: "Operator runbooks ship with every release. Disconnected install, upgrade, backup, restore, and decommission validated in CI before the bundle is issued. LTS support for ≥ 24 months. Optional opt-in audited remote support — but you decide."

**Frequency**: Per-release runbook update; quarterly operator community call.
**Channels**: Direct customer relationship; in-bundle documentation.

---

### Customer DDaT Architecture Community (Same DDaT Roles As Project 001)

**Primary Message**: "Same artefact set, same conventions, same quality bar as the SaaS — inside your accredited boundary. AI-assisted generation available where you choose to enable it against your own approved model deployment."

**Frequency**: Quarterly user group across SaaS and sovereign customers (subject to disclosure constraints).
**Channels**: Cross-government architecture communities; customer-internal DDaT communities.

---

### MOD Defence Digital and NCSC

**Primary Message**: "Sovereign ArcKit lifts the floor of supplier-side governance quality across MOD and sensitive-site programmes, with first-class alignment to MOD SbD / JSP 440 / JSP 604 / NCSC CAF — and a single codebase that connects defence-grade governance back to SME-friendly SaaS."

**Frequency**: Quarterly liaison; ad-hoc on policy change.

---

### CCS / HM Treasury / CDDO / DCPP

**Primary Message**: "Sovereign customers fund the SaaS SME tier through the documented cross-subsidy. Listed on G-Cloud / DOS, ready for DPS / defence-specific frameworks. Cyber Risk Profile-aligned for defence engagements."

**Frequency**: Annual review; framework cycle.

---

### Vendor Internal

**Primary Message**: Operational excellence cadence — weekly sovereign delivery review, monthly architecture forum (cross-project with SaaS), quarterly cross-project roadmap review with Service Owner protecting SaaS mission.

---

## Change Impact Assessment

### Impact on Stakeholders

| Stakeholder | Current State | Future State | Change Magnitude | Resistance Risk | Mitigation |
|-------------|---------------|--------------|------------------|-----------------|------------|
| Customer Accreditor | Bespoke vendor evidence per supplier | Standard MOD-SbD-aligned ArcKit pack | MEDIUM | LOW | Accreditator-in-the-loop alpha; format consistency |
| Customer SIRO | Variable supply-chain visibility | Signed SBOM, hash inventory, signed bundle | MEDIUM | LOW | Per-release evidence delivery |
| Customer Operator Team | Vendor-administered or no-tooling status quo | Runbook-driven self-sufficient operation | HIGH | LOW (positive) | Onboarding rehearsals; runbook reviews |
| Customer DDaT Architects | No tooling or bespoke departmental tooling | ArcKit inside the boundary, parity with SaaS | HIGH | LOW (positive) | Architecture community engagement |
| MOD Defence Digital | Variable governance quality from suppliers | Recognisable ArcKit format across MOD programmes | MEDIUM | LOW | Cross-MOD coherence narrative |
| Vendor LTS Engineering | Greenfield — does not exist yet | Long-term backport discipline | HIGH | MEDIUM | Hire / rotate; protected resourcing |
| Vendor SaaS Engineering | SaaS-only delivery focus | Cross-project discipline; offline-readiness budget | MEDIUM | LOW | Quarterly cross-project review |
| Vendor Finance | SaaS-only commercial model | Two-track model with cross-subsidy reporting | MEDIUM | LOW | Quarterly affordability and contribution review |

### Change Readiness

**Champions**:

- Service Owner — strategic alignment.
- Lead Architect — single-codebase discipline aligns with engineering values.
- MOD Defence Digital — supplier diversification narrative.
- Customer DDaT architects — feature parity with SaaS.

**Fence-sitters**:

- Customer accreditators who have not yet seen vendor evidence — convince via accreditator-in-the-loop alpha.
- Customer SIROs — convince via complete supply-chain evidence.
- Vendor SaaS engineering team — needs assurance that sovereign track will not absorb their roadmap.

**Resisters**:

- Adjacent commercial defence-EA tooling vendors — competitive pressure (low influence).
- Internal voices at vendor advocating for either SaaS-only or sovereign-only focus — managed via Service Owner-level cross-project discipline.

---

## Risk Register (Stakeholder-Related)

### Risk SR-1: First Customer Accreditation Failure

**Related Stakeholders**: SD-1, SD-2, SD-4, SD-11.
**Description**: First customer accreditation rejected, requiring rework cycle and damaging reference-customer narrative.
**Impact on Goals**: G-1, G-7, O-1, O-5.
**Probability**: MEDIUM. **Impact**: HIGH.
**Mitigation**: Accreditator-in-the-loop alpha programme; standard evidence pack iterated against accreditor feedback before formal submission.
**Contingency**: Programme schedule includes one rework cycle absorbed; transparent customer communication.

---

### Risk SR-2: Single-Codebase Pressure Forces Fork

**Related Stakeholders**: SD-9, SD-8, SD-6, SD-7.
**Description**: Customer-specific demands or commercial pressure force per-customer code branches.
**Impact on Goals**: G-2, O-2.
**Probability**: LOW–MEDIUM. **Impact**: HIGH.
**Mitigation**: Configuration-only customisation discipline (REQ Conflict C-1); quarterly architecture review of feature flags; refactor budget; Service Owner authority on fork decisions.

---

### Risk SR-3: Signing-Key Compromise

**Related Stakeholders**: SD-10, SD-1, all customers.
**Description**: Vendor signing-key compromise calls every customer accreditation into question simultaneously.
**Impact on Goals**: G-4, G-8, O-7; existential platform risk for sovereign track.
**Probability**: LOW. **Impact**: CRITICAL.
**Mitigation**: HSM-backed signing; documented custody policy; separation of duties; annual rotation; annual independent attestation.
**Contingency**: Out-of-band re-signing protocol; coordinated customer notification.

---

### Risk SR-4: LTS SLA Slippage

**Related Stakeholders**: SD-13, SD-5, SD-4.
**Description**: LTS patching SLA missed under SaaS-feature pressure.
**Impact on Goals**: G-5, O-4, O-6.
**Probability**: MEDIUM. **Impact**: HIGH.
**Mitigation**: Protected LTS team; SaaS / sovereign roadmap review; explicit SLAs in customer contracts.
**Contingency**: Customer notification protocol; mitigation patches; contractual remedy.

---

### Risk SR-5: Cross-Subsidy Erosion

**Related Stakeholders**: SD-12, SD-8, SD-17, project 001 SD-7 / SD-8.
**Description**: Sovereign pricing concessions undermine cross-subsidy contribution; SME tier funding model weakens.
**Impact on Goals**: G-6, O-3.
**Probability**: MEDIUM. **Impact**: MEDIUM.
**Mitigation**: Documented pricing floor; Service Owner approval below floor; quarterly affordability review.

---

### Risk SR-6: Sovereign Track Distracts SaaS Mission

**Related Stakeholders**: SD-8, vendor SaaS team, project 001 SD-8.
**Description**: Sovereign customer demands and engineering load displace SaaS roadmap, weakening the SME-affordability mission.
**Impact on Goals**: project 001 G-1 (DDaT-recognisable artefacts), G-2 (SME 5-day pack); project 002 G-2 (single codebase).
**Probability**: MEDIUM. **Impact**: MEDIUM.
**Mitigation**: Conflict C-6 resolution — separate track ownership; cross-project roadmap review; Service Owner protects SaaS roadmap.

---

### Risk SR-7: Accreditation Cycle Longer Than Estimate

**Related Stakeholders**: SD-1, SD-4, SD-11.
**Description**: First-customer accreditation longer than vendor estimate, eroding G-1 timeline and reference-customer commercial case.
**Impact on Goals**: G-1, O-1.
**Probability**: MEDIUM. **Impact**: MEDIUM.
**Mitigation**: Conservative timeline; accreditator-in-the-loop alpha to surface evidence-pack gaps early.

---

### Risk SR-8: Critical Dependency Cannot Operate Offline

**Related Stakeholders**: SD-9, SD-5.
**Description**: Component adopted for SaaS that cannot operate fully offline, blocking sovereign release.
**Impact on Goals**: G-2, G-3, O-2, O-4.
**Probability**: MEDIUM. **Impact**: HIGH.
**Mitigation**: Offline-criterion gate in component selection; pluggable abstractions; component ADRs reviewed with sovereign-readiness lens.

---

## Governance & Decision Rights

### Decision Authority Matrix (RACI)

| Decision Type | Responsible | Accountable | Consulted | Informed |
|---------------|-------------|-------------|-----------|----------|
| Per-customer feature request triage | Sovereign Product Manager | Service Owner | Lead Architect, Security Lead | Customer SRO, Customer Accreditor |
| Single-codebase fork escalation | Lead Architect | Service Owner | All Manage-Closely | All staff |
| LTS scope acceptance (security/critical-bug only, or wider) | LTS Engineering Lead | Service Owner | Lead Architect, Sovereign PM | All customers |
| Sovereign pricing for new customer | Sovereign Delivery Lead | Service Owner | Finance, Lead Architect | CCS liaison |
| Below-floor pricing exception | Sovereign Delivery Lead | Service Owner | Finance | Finance, Service Owner |
| Customer engagement to alpha (accreditator-in-the-loop) | Sovereign Delivery Lead | Service Owner | Security Lead, Lead Architect | All customers |
| Vendor signing-key custody and rotation | Signing-Key Custodian | Security Lead | Service Owner, Lead Architect | All staff |
| AI / model provider listing for sovereign use | Lead Architect | Service Owner | Security Lead, DPO | Customers (per release) |
| MOD SbD evidence pack content | Security Lead | Service Owner | Lead Architect, Sovereign Delivery Lead | Customer accreditors |
| Bundle issue (final go / no-go) | Lead Architect | Service Owner | Security Lead, Sovereign Delivery Lead | All customers |
| LTS deprecation timing | Sovereign Product Manager | Service Owner | Customer SROs (consulted ≥ 12 months ahead) | All customers |
| Incident response (severe; e.g., signing-key compromise) | Service Owner | Service Owner | Security Lead, DPO, Legal, all customers | NCSC, ICO if applicable |

### Escalation Path

1. **Level 1 — Day-to-day**: Sovereign Delivery Lead / LTS Engineering Lead / customer-side single point of contact.
2. **Level 2 — Material issue**: Lead Architect / Security Lead / Sovereign Product Manager — to Service Owner.
3. **Level 3 — Strategic / cross-project / cross-subsidy**: Service Owner.
4. **Level 4 — Regulatory / legal / national-security**: Security Lead and DPO initiate; engagement with NCSC, ICO, customer accreditator, legal counsel.

---

## Validation & Sign-off

### Stakeholder Review

| Stakeholder | Review Date | Comments | Status |
|-------------|-------------|----------|--------|
| Service Owner (Mark Craddock) | [PENDING] | | [PENDING] |
| Lead Architect (vendor) | [PENDING] | | [PENDING] |
| Security Lead (vendor) | [PENDING] | | [PENDING] |
| Sovereign Delivery Lead (vendor) | [PENDING] | | [PENDING] |
| DPO (vendor) | [PENDING] | | [PENDING] |
| Pilot customer SRO | [PENDING] | | [PENDING] |
| Pilot customer Accreditor | [PENDING] | | [PENDING] |
| MOD Defence Digital liaison | [PENDING] | | [PENDING] |

### Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Service Owner | Mark Craddock | _________ | [PENDING] |
| Lead Architect | [PENDING] | _________ | [PENDING] |
| Security Lead | [PENDING] | _________ | [PENDING] |

---

## Appendices

### Appendix A: Cross-Project Stakeholder Alignment

This document focuses on stakeholders specific to the sovereign deployment (project 002). Stakeholders in common with project 001 (managed SaaS) — particularly the DDaT architecture community in civilian departments, regulators (ICO, EHRC), and HMG bodies (HM Treasury, CCS, CDDO) — are documented in `projects/001-arckit-saas/ARC-001-STKE-v1.0.md`. The shared synergy is recorded in this document under **Synergy 4** and operationally addressed via the cross-project quarterly architecture community engagement.

### Appendix B: References

- `projects/000-global/ARC-000-PRIN-v2.0.md` — Architecture Principles, Principle 21 anchors this project
- `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md` — Requirements (current)
- `projects/001-arckit-saas/ARC-001-REQ-v1.0.md` — SaaS sister project requirements
- `projects/001-arckit-saas/ARC-001-STKE-v1.0.md` — SaaS sister project stakeholder analysis (DDaT capability framework treatment)
- DDaT Capability Framework — https://ddat-capability-framework.service.gov.uk/
- Government Functional Standard for Digital (GovS 005)
- Government Functional Standard for Security (GovS 007)
- MOD Secure by Design
- JSP 440 — Defence Manual of Security
- JSP 604 — Defence Manual for the Authorisation of Information Systems
- NCSC Cyber Assessment Framework; NCSC Cloud Security Principles; NCSC supply-chain guidance
- Defence Cyber Protection Partnership Cyber Risk Profile
- HMG Government Security Classifications Policy
- UK GDPR / Data Protection Act 2018

### Appendix C: Open Items

- Engage one MOD or sensitive-site customer for the accreditator-in-the-loop alpha programme.
- Recruit and onboard the Vendor Sovereign Delivery Lead.
- Establish the LTS engineering team and signing-key custody arrangements.
- Align on quarterly cross-project (SaaS + sovereign) architecture forum cadence.

---

## External References

> No external policy documents were placed in `projects/002-arckit-sovereign/external/` at the time of generation.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| — | — | — | — | — |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:stakeholders` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: Claude Opus 4.7 (1M context)
