# Stakeholder Drivers & Goals Analysis: ArcKit as a Service (Managed SaaS)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:stakeholders`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-STKE-v1.0 |
| **Document Type** | Stakeholder Drivers & Goals Analysis |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
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
| **Distribution** | Project Team, Architecture Team, CCS liaison, GDS, CDDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:stakeholders` command. Primary stakeholder group: UK public sector architects mapped to the DDaT Capability Framework | [PENDING] | [PENDING] |

---

## Executive Summary

### Purpose

This document identifies the stakeholders for **ArcKit as a Service (Managed SaaS)** — Project 001 — and traces their underlying drivers through to measurable goals and outcomes. The analysis answers: who must be persuaded, who must be served, who must approve, and how we will know we have succeeded for each of them.

The user input that anchored this analysis is: *"one of the key stakeholders will be architects within the uk public sector. see here for roles: https://ddat-capability-framework.service.gov.uk/"*. Accordingly, the **DDaT architecture community** is treated as the primary user-stakeholder group, with the seven DDaT architecture roles (Enterprise, Solution, Data, Security, Business, Technical, Network) called out individually.

### Key Findings

- The platform serves two intersecting audiences: (a) **DDaT architects in UK public sector buying authorities** who must trust the artefacts produced by suppliers using ArcKit, and (b) **SME architects supplying those authorities** who must be able to produce credible governance evidence cheaply. These audiences are largely synergistic — better SME governance evidence reduces buyer assurance burden — but they pull on opposite ends of the feature/cost trade-off.
- Three driver clusters dominate: **affordability** (SMEs, HM Treasury, vendor finance), **assurance** (DDaT architects, CDDO, NCSC, ICO, GDS assessors), and **mission delivery** (vendor service owner, sponsors). Most conflicts arise between affordability and assurance.
- The strongest synergy is between the DDaT architecture community and the SME suppliers: both want consistent, credible, low-friction governance artefacts. The platform is the artefact.

### Critical Success Factors

- DDaT architects in buying authorities recognise ArcKit-produced artefacts as credible without bespoke verification (validated through pilot with at least 3 buying authorities before GA).
- SME free-tier users can produce a complete governance pack for a real bid in under 5 working days from sign-up.
- Cross-subsidy economics validated: large-enterprise / non-SME tenants funding the SME tier reach break-even by GA + 18 months.
- Independent assurance evidence (NCSC CAF, NCSC Cloud Security Principles, UK GDPR, WCAG 2.2 AA) available to tenants on demand from GA.
- Service listed and discoverable on G-Cloud at GA.

### Stakeholder Alignment Score

**Overall Alignment**: HIGH

The principal stakeholders agree on the strategic outcome (more, better SME participation in UK government delivery via better governance tooling). Disagreements are primarily on how to balance free-tier richness against cost sustainability (resolved in `ARC-001-REQ-v1.0.md` Conflict C-1) and on AI provider concentration vs portability (Conflict C-2). No fundamental misalignment was identified.

---

## Stakeholder Identification

### Internal Stakeholders (Vendor / Service Provider)

| Stakeholder | Role / Department | Influence | Interest | Engagement Strategy |
|-------------|-------------------|-----------|----------|---------------------|
| Mark Craddock | Service Owner / Sponsor | HIGH | HIGH | Decision authority; weekly steering |
| [PENDING] | Lead Architect / CTO | HIGH | HIGH | Architecture decisions; ADRs |
| [PENDING] | Product Manager | MEDIUM | HIGH | Day-to-day prioritisation; roadmap |
| [PENDING] | Delivery Manager | MEDIUM | HIGH | Cadence, risks, dependencies |
| [PENDING] | Security Lead / SIRO-equivalent | HIGH | HIGH | Threat modelling, CAF, pen tests |
| [PENDING] | Data Protection Officer (DPO) | HIGH | HIGH | UK GDPR, ROPA, sub-processor reviews |
| [PENDING] | Accessibility Lead | MEDIUM | HIGH | WCAG 2.2 AA, PSBAR statement |
| [PENDING] | Finance Lead | HIGH | MEDIUM | Cross-subsidy unit economics; pricing |
| [PENDING] | SRE / Operations Lead | MEDIUM | HIGH | SLOs, runbooks, on-call |
| [PENDING] | Customer Success / Support | LOW | HIGH | Tenant onboarding, NPS |

### Primary External Stakeholder Group: DDaT Architecture Community (UK Public Sector)

Reference: [DDaT Capability Framework](https://ddat-capability-framework.service.gov.uk/). These roles exist in central-government departments, arms-length bodies (ALBs), NHS organisations, and local authorities. ArcKit produces the artefacts these architects review (when their organisation is a buyer) or author (when their organisation is delivering directly).

| DDaT Architecture Role | Typical Setting | Influence | Interest | Engagement Strategy |
|------------------------|-----------------|-----------|----------|---------------------|
| Enterprise Architect | Department / ALB / NHS body | HIGH | HIGH | Manage Closely — design partnerships, validation panels |
| Solution Architect | Programme / project | HIGH | HIGH | Manage Closely — pilots, design feedback |
| Data Architect | Cross-cutting data function | MEDIUM | HIGH | Keep Informed — data-model and DPIA features |
| Security Architect | Departmental security function | HIGH | HIGH | Manage Closely — assurance evidence, CAF mapping |
| Business Architect | Strategy / transformation | MEDIUM | MEDIUM | Keep Informed — stakeholder/requirements features |
| Technical Architect | Platform / engineering | MEDIUM | HIGH | Keep Informed — diagrams, ADRs, traceability |
| Network Architect | Infrastructure | LOW | MEDIUM | Monitor — diagrams (deployment view) |

### Secondary External Stakeholder Groups

#### SME Supplier Community (Primary Commercial Audience)

| Stakeholder | Organisation | Relationship | Influence | Interest |
|-------------|--------------|--------------|-----------|----------|
| SME Architect (DDaT-aligned) | UK SMEs supplying gov | Primary user | LOW (individually) / HIGH (collectively) | HIGH |
| SME Founder / Bid Lead | UK SMEs | Buyer of paid tier | MEDIUM | HIGH |
| SME Delivery Manager | UK SMEs | User | LOW | MEDIUM |

#### UK Government Digital Roles (GovS 005)

> The [Government Functional Standard for Digital (GovS 005)](https://www.gov.uk/government/publications/government-functional-standard-govs-005-digital) defines mandatory digital governance roles. ArcKit produces evidence these roles consume.

| Role | Responsibility | Power / Interest | Engagement Strategy |
|------|----------------|------------------|---------------------|
| Senior Responsible Owner (SRO) — buyer side | Accountable for digital outcomes and spend controls | HIGH / MEDIUM | Keep Satisfied — spend control evidence |
| Service Owner — buyer side | Owns the end-to-end service and user outcomes | HIGH / MEDIUM | Keep Satisfied — service-quality evidence |
| Product Manager — buyer side | Prioritises features against user needs and policy | MEDIUM / MEDIUM | Keep Informed — requirements/roadmap features |
| Delivery Manager — buyer side | Manages delivery cadence, risks, and dependencies | MEDIUM / LOW | Monitor — backlog/plan features |
| CDDO (Central Digital & Data Office) | Assurance, spend control, cross-government standards | HIGH / MEDIUM | Keep Satisfied — TCoP/Service Standard mapping |
| CDIO / CTO — buyer departments | Departmental digital strategy | HIGH / MEDIUM | Keep Satisfied — quarterly briefings |
| DDaT Profession Lead — Architecture | Capability framework and recruitment | LOW / MEDIUM | Monitor — capability mapping |

#### UK Government Security Roles (GovS 007)

> The [Government Functional Standard for Security (GovS 007)](https://www.gov.uk/government/publications/government-functional-standard-govs-007-security) defines mandatory protective security roles.

| Role | Responsibility | Power / Interest | Engagement Strategy |
|------|----------------|------------------|---------------------|
| Senior Information Risk Owner (SIRO) — buyer side | Owns information / cyber risk | HIGH / MEDIUM | Keep Satisfied — ArcKit security evidence |
| Departmental Security Officer (DSO) — buyer side | Day-to-day security policy implementation | MEDIUM / MEDIUM | Keep Informed — security artefact features |

#### UK Government Bodies and Regulators

| Stakeholder | Organisation | Relationship | Power | Interest |
|-------------|--------------|--------------|-------|----------|
| GDS Service Assessors | Government Digital Service / CDDO | Standards arbiter | HIGH | MEDIUM |
| NCSC | National Cyber Security Centre | Standards setter (CAF, Cloud Security Principles) | HIGH | LOW–MEDIUM |
| Crown Commercial Service (CCS) | Cabinet Office | G-Cloud framework owner | HIGH | MEDIUM |
| Information Commissioner's Office (ICO) | Independent regulator | UK GDPR / DPA enforcement | HIGH | LOW |
| Equality and Human Rights Commission (EHRC) | Independent regulator | PSBAR / accessibility enforcement | MEDIUM | LOW |
| HM Treasury | HMG | Spend controls / value for money | HIGH | LOW |
| Government Commercial Function (GCF) | Cabinet Office | Procurement standards | MEDIUM | LOW |
| National Audit Office (NAO) / GIAA | Independent audit | Public spending audit | MEDIUM | LOW |

#### Suppliers and Adjacent Parties

| Stakeholder | Organisation | Relationship | Power | Interest |
|-------------|--------------|--------------|-------|----------|
| AI / LLM provider | Commercial vendor | Supplier (INT-005) | MEDIUM | LOW |
| Cloud / hosting provider | Commercial vendor | Supplier (INT-006) | MEDIUM | LOW |
| Payment processor | Commercial vendor | Supplier (INT-002) | LOW | LOW |
| Companies House | UK Government | Data source (INT-003) | LOW | LOW |
| Existing commercial EA tooling vendors | Various | Competitor / comparator | LOW | LOW (defensive) |

### Stakeholder Power-Interest Grid

```text
                          INTEREST
              Low                         High
        ┌─────────────────────┬─────────────────────┐
        │                     │                     │
        │   KEEP SATISFIED    │   MANAGE CLOSELY    │
   High │                     │                     │
        │  • CCS              │  • Service Owner    │
        │  • HM Treasury      │  • Lead Architect   │
        │  • ICO              │  • Security Lead    │
        │  • NCSC             │  • DPO              │
 P      │  • GDS Assessors    │  • DDaT Enterprise  │
 O      │  • CDDO             │    Architect        │
 W      │  • CDIO/CTO buyers  │  • DDaT Solution    │
 E      │  • SIRO buyer       │    Architect        │
 R      │  • Finance          │  • DDaT Security    │
        │                     │    Architect        │
        ├─────────────────────┼─────────────────────┤
        │                     │                     │
        │      MONITOR        │    KEEP INFORMED    │
   Low  │                     │                     │
        │  • Companies House  │  • SME Architects   │
        │  • Network          │  • SME Founders     │
        │    Architect        │  • DDaT Data /      │
        │  • Competitors      │    Technical /      │
        │  • Adjacent vendors │    Business Arch.   │
        │  • DDaT Profession  │  • Product/Delivery │
        │    Lead             │    Mgr (vendor)     │
        │                     │  • SRE / Support    │
        └─────────────────────┴─────────────────────┘
```

| Stakeholder | Power | Interest | Quadrant | Engagement Strategy |
|-------------|-------|----------|----------|---------------------|
| Service Owner (Mark Craddock) | HIGH | HIGH | Manage Closely | Weekly steering; decision authority |
| Lead Architect / CTO (vendor) | HIGH | HIGH | Manage Closely | ADR review; weekly architecture forum |
| Security Lead (vendor) | HIGH | HIGH | Manage Closely | Risk forum; CAF reviews |
| DPO (vendor) | HIGH | HIGH | Manage Closely | DPIA cadence; ROPA reviews |
| DDaT Enterprise Architect (buyer) | HIGH | HIGH | Manage Closely | Design partnership; quarterly user group |
| DDaT Solution Architect (buyer) | HIGH | HIGH | Manage Closely | Pilot programme; feedback panel |
| DDaT Security Architect (buyer) | HIGH | HIGH | Manage Closely | Assurance evidence reviews |
| DDaT Data Architect (buyer) | MEDIUM | HIGH | Keep Informed | Quarterly user group |
| DDaT Technical Architect (buyer) | MEDIUM | HIGH | Keep Informed | Quarterly user group |
| DDaT Business Architect (buyer) | MEDIUM | MEDIUM | Keep Informed | Roadmap newsletter |
| DDaT Network Architect (buyer) | LOW | MEDIUM | Monitor | Annual update |
| SME Architect | LOW | HIGH | Keep Informed | In-product changelog; community forum |
| SME Founder / Bid Lead | MEDIUM | HIGH | Keep Informed | Pricing transparency; case studies |
| CDDO | HIGH | MEDIUM | Keep Satisfied | TCoP / Service Standard alignment evidence |
| GDS Service Assessors | HIGH | MEDIUM | Keep Satisfied | Service Standard evidence pack |
| NCSC | HIGH | LOW–MEDIUM | Keep Satisfied | CAF and Cloud Security evidence |
| Crown Commercial Service | HIGH | MEDIUM | Keep Satisfied | G-Cloud listing maintenance |
| ICO | HIGH | LOW | Keep Satisfied | UK GDPR posture; sub-processor list |
| EHRC | MEDIUM | LOW | Monitor | Accessibility Statement |
| HM Treasury | HIGH | LOW | Keep Satisfied | Value-for-money narrative |
| Finance Lead (vendor) | HIGH | MEDIUM | Keep Satisfied | Quarterly affordability review |
| Product Manager (vendor) | MEDIUM | HIGH | Keep Informed | Sprint reviews |
| Delivery Manager (vendor) | MEDIUM | HIGH | Keep Informed | Stand-ups; risk log |
| SRE / Operations (vendor) | MEDIUM | HIGH | Keep Informed | Release notifications |
| Customer Success / Support (vendor) | LOW | HIGH | Keep Informed | Weekly tenant signal review |
| Accessibility Lead (vendor) | MEDIUM | HIGH | Keep Informed | A11y testing in CI |
| AI / Cloud / Payment providers | MEDIUM | LOW | Monitor | Quarterly vendor reviews |
| Companies House | LOW | LOW | Monitor | API change-notice mailing list |
| Competitor EA vendors | LOW | LOW | Monitor | Annual market scan |

---

## Stakeholder Drivers Analysis

### SD-1: DDaT Enterprise Architect (Buyer) — Consistent, Credible Supplier Governance Evidence

**Stakeholder**: Enterprise Architects in UK public-sector buying authorities (departments, ALBs, NHS bodies, local authorities).

**Driver Category**: STRATEGIC + COMPLIANCE + RISK

**Driver Statement**: "I need supplier governance artefacts that I can trust without re-auditing them, that map cleanly to TCoP, GDS Service Standard, NCSC CAF, and the security classifications policy, so that I can recommend SME suppliers without taking on disproportionate assurance risk."

**Context & Background**: DDaT Enterprise Architects are accountable for departmental architecture coherence. When a department procures from an SME, the EA function inherits assurance work — disproportionate scrutiny is the single biggest reason buyers default to large incumbents. The Procurement Act 2023 and Cabinet Office SME Action Plans pressure them to widen the supplier base, but they will not accept materially higher assurance risk to do it.

**Driver Intensity**: HIGH

**Enablers**:

- ArcKit-produced artefacts that follow recognised conventions (TCoP, Service Standard) verbatim
- Clear, durable IDs (ARC-{PROJECT}-{TYPE}-v{VERSION}) that make cross-document references checkable
- Lineage metadata showing what was AI-generated vs human-authored
- Independent assurance evidence (CAF, Cloud Security Principles) available without supplier intermediation

**Blockers**:

- Bespoke or proprietary formats that the EA cannot read, search, or version-control alongside their own artefacts
- AI-generated content that cannot be distinguished from human content
- Inconsistent quality between SMEs using ArcKit (tooling alone is insufficient if quality is uncapped)

**Related Stakeholders**: SD-3 (DDaT Security Architect), SD-7 (CDDO), SD-9 (GDS Assessors).

---

### SD-2: DDaT Solution Architect (Buyer) — Decision Traceability and ADRs

**Stakeholder**: Solution Architects in UK public-sector buying authorities, working at the programme/project level.

**Driver Category**: OPERATIONAL + COMPLIANCE

**Driver Statement**: "When I review a supplier's design, I need to see why decisions were made — not just what was decided — and I need to be able to follow each decision back to a requirement, a principle, and a risk."

**Context & Background**: Solution Architects spend most of their time in design reviews. The cost of design-review work is dominated by chasing context. Suppliers who provide ADRs with proper context, alternatives considered, and consequence analysis save the buyer days per review and reduce the chance of a defect surfacing late.

**Driver Intensity**: HIGH

**Enablers**:

- ADR templates with mandatory alternatives-and-consequences sections
- Forward and backward traceability between requirements, principles, ADRs, designs, and tests
- Diagrams that follow C4 / Mermaid conventions and are version-controlled

**Blockers**:

- ADRs that record "what" without "why"
- Diagram drift (PNGs stored separately from text rationale)
- Suppliers using ArcKit as a template generator without filling content

**Related Stakeholders**: SD-1, SD-4 (DDaT Technical Architect).

---

### SD-3: DDaT Security Architect (Buyer) — CAF, Secure by Design, Threat Modelling

**Stakeholder**: Security Architects in UK public-sector buying authorities; SIROs and DSOs in their reporting line.

**Driver Category**: COMPLIANCE + RISK

**Driver Statement**: "I need to know that supplier-produced services meet NCSC Secure by Design and that I can map their controls to the Cyber Assessment Framework and to my department's risk appetite — without having to translate a bespoke vendor security model into UK Government language."

**Context & Background**: NCSC Secure by Design (now mandatory in central government) and the CAF (used in GovAssure for OES) define the language buyers expect. Suppliers who do not produce evidence in that language create translation friction that ends in rejection or in costly bespoke assurance.

**Driver Intensity**: CRITICAL

**Enablers**:

- ArcKit assessments that map directly to NCSC SbD principles, CAF outcomes, and Cloud Security Principles
- Tenant-side ability to run `/arckit:secure` and `/arckit:tcop` and produce defensible evidence
- DPIA generation aligned with UK ICO templates

**Blockers**:

- Generic "ISO 27001-shaped" assessments that are not framework-specific
- Missing threat models or risk registers
- Auditing claims without evidence (e.g., "encrypted in transit" without TLS-cipher inventory)

**Related Stakeholders**: SD-1, SD-7 (CDDO), SD-12 (NCSC).

---

### SD-4: DDaT Data and Technical Architects (Buyer) — Diagrams, Data Models, Integration Clarity

**Stakeholder**: Data Architects and Technical Architects in UK public-sector buying authorities.

**Driver Category**: OPERATIONAL

**Driver Statement**: "I need supplier designs to include diagrams I can read, data models with classifications and PII flagged, and integration patterns that make trust boundaries explicit."

**Context & Background**: Architects of these specialisms deal with the artefacts most likely to leak risk — undocumented integrations, unclassified data, ambiguous trust boundaries. Tooling that makes these things hard to omit raises the median quality of supplier output.

**Driver Intensity**: HIGH

**Enablers**:

- C4 / Mermaid diagrams generated alongside text artefacts
- Data models with classification, retention, and lineage fields mandatory
- Integration requirements (INT-xxx) captured with auth, data, error handling

**Blockers**:

- Diagram-only artefacts without supporting rationale
- Data models that omit classification or residency

**Related Stakeholders**: SD-1, SD-2.

---

### SD-5: DDaT Business and Network Architects (Buyer) — Business Capability and Infrastructure View

**Stakeholder**: Business Architects and Network Architects in UK public-sector buying authorities.

**Driver Category**: OPERATIONAL

**Driver Statement**: "I want supplier artefacts that link technology choices back to business capabilities (Business Architect) or that make the deployment topology and network boundaries explicit (Network Architect)."

**Driver Intensity**: MEDIUM (these roles are less likely to be primary reviewers but their presence at design reviews matters)

**Enablers**:

- Stakeholder-driver-goal-outcome traceability that connects business capability to system features
- Deployment-view diagrams showing zones, segments, and ingress/egress

**Blockers**:

- Pure technology-stack artefacts with no business rationale
- Missing deployment diagrams

**Related Stakeholders**: SD-1, SD-2, SD-4.

---

### SD-6: SME Architect — Affordable, Credible, Fast Governance Evidence

**Stakeholder**: Architects employed by UK SMEs supplying or seeking to supply UK government services.

**Driver Category**: FINANCIAL + STRATEGIC + PERSONAL

**Driver Statement**: "I need to produce governance artefacts that pass DDaT-architect scrutiny with the time and money my SME actually has — not the time and money a large SI has — so that we can win bids and deliver them confidently."

**Context & Background**: SME architects are typically the most senior technical person in a small business. They juggle delivery, bid work, line management, and pre-sales. They cannot afford enterprise EA tooling, but they cannot afford to produce weak governance evidence either, because losing one bid wipes out the savings on tooling many times over.

**Driver Intensity**: CRITICAL

**Enablers**:

- Free tier that covers the essential ArcKit baseline end-to-end (BR-001)
- AI-assisted generation that produces defensible drafts in minutes (FR-004)
- Templates that match what DDaT architects expect (alignment with SD-1 to SD-5)

**Blockers**:

- Trial-style free tiers that expire mid-bid
- AI generation that produces generic content without project context
- Tooling that requires bespoke setup before useful output

**Related Stakeholders**: SD-7 (SME Founder), SD-1 (the buyer their work will reach).

---

### SD-7: SME Founder / Bid Lead — Win Rate and Cost Predictability

**Stakeholder**: SME founders, MDs, and bid leads.

**Driver Category**: FINANCIAL + STRATEGIC

**Driver Statement**: "I need predictable, low-cost tooling that lets me bid for more government work, win at a higher rate, and recover the bid cost on the work that wins."

**Context & Background**: Bid economics are brutal: most bids lose. Every pound spent on bid infrastructure is loss-making until a bid wins, and even then only over time. A free or near-free EA tool that materially raises win rate is one of the highest-leverage bid investments an SME can make.

**Driver Intensity**: HIGH

**Enablers**:

- Transparent published pricing (BR-002)
- G-Cloud listing for buyer-side procurement ease (BR-004)
- Visible track record of SME wins using ArcKit-produced artefacts

**Blockers**:

- Hidden / "contact sales" pricing
- Per-bid pricing pressure as the SME grows (cliff-edge from free tier to expensive paid tier)

**Related Stakeholders**: SD-6, SD-13 (HM Treasury).

---

### SD-8: Vendor Service Owner (Mark Craddock) — Mission and Sustainability

**Stakeholder**: ArcKit as a Service Owner / Sponsor.

**Driver Category**: STRATEGIC + PERSONAL

**Driver Statement**: "I want to deliver on Principle 1 — genuinely affordable, credible architecture tooling for SMEs supplying UK government — at scale and indefinitely, without the mission collapsing under cost pressure or compliance failure."

**Context & Background**: The strategic rationale for ArcKit as a Service is the SME-affordability commitment. If that commitment fails, the platform's reason for existing fails with it. The Service Owner therefore has both a strategic stake (the mission) and a personal/reputational one (the platform's success or failure is his).

**Driver Intensity**: CRITICAL

**Enablers**:

- Cross-subsidy unit economics that work (BR-005)
- Credible compliance posture (NFR-C-* family)
- Adoption above the cross-subsidy threshold

**Blockers**:

- Free-tier abuse; underestimated AI inference cost
- Compliance failure (e.g., ICO action) wiping out trust
- Slow adoption keeping the cross-subsidy below break-even

**Related Stakeholders**: All — the Service Owner is the integrator.

---

### SD-9: Vendor Lead Architect / CTO — Sustainable Engineering Foundation

**Stakeholder**: Lead Architect / CTO at the ArcKit vendor.

**Driver Category**: OPERATIONAL + STRATEGIC + PERSONAL

**Driver Statement**: "Build a platform that is observable, secure, scalable, and pluggable from day one — so that we can sustain the SME free tier through cost discipline, satisfy enterprise tenants, and reuse the same code for the future sovereign deployment route without a fork."

**Driver Intensity**: HIGH

**Enablers**:

- Adherence to the principles in `ARC-000-PRIN-v2.0.md` (especially open standards, observability, FinOps, IaC, automated testing, CI/CD, sovereign-ready packaging).
- Pluggable AI provider abstraction (Conflict C-2 resolution).
- Tenant isolation testing in CI.

**Blockers**:

- Time pressure leading to expedient single-provider integrations.
- Feature requests that fork the codebase between SaaS and sovereign.

**Related Stakeholders**: SD-8, SD-10 (Security Lead), SD-11 (DPO).

---

### SD-10: Vendor Security Lead — Audit-Defensible Posture and No Cross-Tenant Incidents

**Stakeholder**: Vendor Security Lead (SIRO-equivalent role).

**Driver Category**: COMPLIANCE + RISK + PERSONAL

**Driver Statement**: "Maintain an audit-defensible security posture (NCSC CAF, Cloud Security Principles, ISO 27001 trajectory) and ensure zero cross-tenant data incidents."

**Context & Background**: Multi-tenant SaaS is a single high-blast-radius failure mode away from existential damage. The security lead lives that risk professionally. Their personal accountability is mainly about not being the named SIRO when an avoidable incident happens.

**Driver Intensity**: CRITICAL

**Enablers**:

- Defence in depth (Principle 5)
- Automated tenant-isolation tests in CI (NFR-SEC-002)
- Annual independent pen testing
- Vulnerability disclosure programme

**Blockers**:

- Time-to-market pressure pushing security-test budgets
- AI-generation feature work bypassing tenant ID enforcement

**Related Stakeholders**: SD-3, SD-9, SD-11, SD-12.

---

### SD-11: Vendor Data Protection Officer — UK GDPR Posture and Sub-Processor Discipline

**Stakeholder**: Vendor DPO.

**Driver Category**: COMPLIANCE + RISK

**Driver Statement**: "Maintain a current UK GDPR / DPA 2018 posture, with ROPA, DPIA, and a sub-processor inventory that withstands ICO scrutiny — particularly around AI-model providers and any non-UK processing."

**Driver Intensity**: HIGH

**Enablers**:

- UK-residency default (Principle 7, NFR-C-001)
- AI-provider no-training assurances and Article 46 transfer mechanisms where applicable (INT-005)
- Tenant-facing transparency (sub-processor list)

**Blockers**:

- Sub-processor changes without notice
- Ad-hoc AI-vendor selection without DPIA refresh

**Related Stakeholders**: SD-10, SD-12 (ICO).

---

### SD-12: NCSC and ICO — Sectoral Posture and Regulatory Compliance

**Stakeholder**: National Cyber Security Centre and Information Commissioner's Office.

**Driver Category**: COMPLIANCE + STRATEGIC

**Driver Statement (NCSC)**: "Raise the UK cyber-resilience baseline; encourage adoption of CAF and Cloud Security Principles."
**Driver Statement (ICO)**: "Maintain a high standard of UK GDPR / DPA 2018 compliance and act on enforcement priorities."

**Driver Intensity**: HIGH (regulatory)

**Enablers**:

- Public, accurate, current evidence of CAF and Cloud Security Principles posture
- Up-to-date sub-processor lists, DPIA on AI processing, breach-notification readiness

**Blockers**:

- Out-of-date evidence
- Material change without re-assessment

**Related Stakeholders**: SD-3, SD-10, SD-11.

---

### SD-13: HM Treasury, CCS, CDDO — Public Spending and Supplier Diversity

**Stakeholder**: HM Treasury (value for money), CCS (G-Cloud / SME spend), CDDO (digital spend controls and standards).

**Driver Category**: FINANCIAL + STRATEGIC + COMPLIANCE

**Driver Statement**: "Increase the share of public spending that goes to SMEs, while maintaining standards (TCoP, Service Standard) and demonstrable value for money."

**Context & Background**: Procurement Act 2023 and SME Action Plans drive this. CDDO's spend-control function and CCS's G-Cloud framework are the two principal levers. ArcKit aligns directly with the policy intent — but only if it is visibly used and visibly delivers.

**Driver Intensity**: HIGH

**Enablers**:

- G-Cloud listing (BR-004)
- Quantitative evidence of SME-bid wins associated with ArcKit usage
- TCoP / Service Standard alignment evidence

**Blockers**:

- Service unavailable on G-Cloud or with minimum commitments unfriendly to small buyers
- Value-for-money claim not evidenced

**Related Stakeholders**: SD-7, SD-8.

---

### SD-14: GDS Service Assessors — Service Standard Quality

**Stakeholder**: GDS / CDDO Service Assessors.

**Driver Category**: STANDARDS + RISK

**Driver Statement**: "Assess services against the GDS Service Standard quickly and consistently. Tools that produce assessment-ready evidence raise the quality of services we see."

**Driver Intensity**: MEDIUM

**Enablers**:

- `/arckit:service-assessment` mapping
- Accessibility evidence (WCAG 2.2 AA) embedded in the artefact set

**Blockers**:

- Assessment evidence that cherry-picks Service Standard points
- Accessibility statements that exist but are not maintained

**Related Stakeholders**: SD-1, SD-13.

---

## Driver-to-Goal Mapping

### Goal G-1: DDaT-Recognisable Artefacts

**Derived From Drivers**: SD-1, SD-2, SD-3, SD-4, SD-5, SD-14.

**Goal Owner**: Vendor Lead Architect / CTO.

**Goal Statement**: By GA, ArcKit-produced artefacts MUST be recognised as credible by at least three UK public-sector buying authorities' DDaT architecture functions in independent piloting, with no requirement for bespoke verification.

**Why This Matters**: This is the central value claim of the platform for the buyer side. Without it, SME suppliers who use ArcKit get no advantage in front of buyers and the synergy collapses.

**Success Metrics**:

- **Primary**: ≥ 3 buying authority pilots completed with positive review of artefact credibility.
- **Secondary**: ≥ 80% of pilot artefacts pass review without supplier rework.
- **Secondary**: 0 instances of bespoke verification required by pilot reviewers.

**Baseline**: 0 (pre-GA).
**Target**: 3 successful pilots by GA – 60 days.
**Measurement Method**: Pilot review reports signed by participating EA / SA functions.
**Dependencies**: Pilot programme funded; pilot tenants identified; buyer EAs willing to participate.
**Risks**: Pilot reviewers find quality gaps that require platform changes (mitigation: alpha + private beta cycles ahead of pilot).

---

### Goal G-2: SME Time-to-First-Bid Pack

**Derived From Drivers**: SD-6, SD-7.

**Goal Owner**: Product Manager (vendor).

**Goal Statement**: A new SME tenant on the free tier MUST be able to produce a complete bid-quality governance pack (principles, requirements, ADRs, diagrams, traceability) within 5 working days of sign-up, with no paid-tier upgrade required.

**Success Metrics**:

- **Primary**: ≥ 60% of new SME tenants reach 5 saved artefacts within 5 working days (FR-004 telemetry).
- **Secondary**: NPS ≥ 30 from SME free-tier users at 30-day mark.

**Baseline**: 0 (pre-GA).
**Target**: From GA onwards.
**Measurement Method**: Product analytics + in-product survey.
**Dependencies**: AI generation quality (FR-004), template clarity, free-tier limits not biting (BR-001).

---

### Goal G-3: Cross-Subsidy Break-Even

**Derived From Drivers**: SD-8, SD-13, vendor Finance.

**Goal Owner**: Service Owner with Finance Lead.

**Goal Statement**: Achieve cross-subsidy break-even — large-enterprise tenant revenue ≥ aggregate SME-tier cost-to-serve — by GA + 18 months.

**Success Metrics**:

- **Primary**: Quarterly cost-to-serve report shows break-even by GA + 18 months.
- **Secondary**: Free-tier cost per active tenant within forecast band ± 15%.

**Baseline**: Loss (pre-revenue).
**Target**: Break-even by 2028-10-31 (assuming GA 2027-04-30).
**Measurement Method**: Finance ledger + FinOps tagging (Principle 17).
**Dependencies**: Adoption (BR-008); enterprise sales motion; AI inference cost trajectory (Conflict C-1).
**Risks**: Free-tier abuse; AI inference cost growth; enterprise-tenant slow take-up.

---

### Goal G-4: NCSC CAF and Cloud Security Principles Posture

**Derived From Drivers**: SD-3, SD-10, SD-12.

**Goal Owner**: Vendor Security Lead.

**Goal Statement**: Maintain a current NCSC CAF self-assessment with a defined target profile and a current assessment against all 14 NCSC Cloud Security Principles, refreshed at least annually and on material change.

**Success Metrics**:

- **Primary**: Both assessments dated within last 12 months at any point in time post-GA.
- **Secondary**: Independent pen-test report current within 12 months.

**Baseline**: None (pre-GA).
**Target**: First assessment complete by GA.
**Measurement Method**: Document register; tenant-evidence pack version control.

---

### Goal G-5: UK GDPR and DPA Posture

**Derived From Drivers**: SD-11, SD-12.

**Goal Owner**: DPO.

**Goal Statement**: Maintain a current ROPA, sub-processor inventory, DPIA on material processing (including AI), and 72-hour ICO breach-notification readiness.

**Success Metrics**: ROPA reviewed quarterly; sub-processor list reviewed annually; DPIA refreshed on material change; tabletop breach-notification exercise annually.

---

### Goal G-6: WCAG 2.2 AA / PSBAR Conformance

**Derived From Drivers**: SD-14, EHRC, vendor Accessibility Lead, all DDaT architects.

**Goal Owner**: Accessibility Lead.

**Goal Statement**: Maintain WCAG 2.2 AA conformance with current Accessibility Statement; zero critical accessibility regressions in production.

**Success Metrics**: Automated a11y in CI green; manual AT testing per release; statement reviewed annually.

---

### Goal G-7: G-Cloud Listing and Procurement Reach

**Derived From Drivers**: SD-13, SD-7.

**Goal Owner**: Service Owner with CCS liaison.

**Goal Statement**: Service listed on G-Cloud at GA and across subsequent framework iterations; minimum commitment terms friendly to SME-buying-from-SME.

**Success Metrics**: Listed at GA; ≥ 25 buying-authority callouts via G-Cloud within 12 months of GA.

---

### Goal G-8: Pluggable AI Provider for Future Sovereign Reuse

**Derived From Drivers**: SD-9, Principle 4, sovereign deployment scope (out of scope of project 001 but architecturally connected).

**Goal Owner**: Lead Architect.

**Goal Statement**: AI provider integrated through a pluggable abstraction with a second provider validated in CI quarterly; provider switchable in days not weeks.

**Success Metrics**: Quarterly CI run on alternative provider passes; ADR captured for provider abstraction.

---

## Goal-to-Outcome Mapping

### Outcome O-1: Buyer Trust in ArcKit Artefacts

**Supported Goals**: G-1, G-4, G-5, G-6.

**Outcome Statement**: DDaT architects in UK public-sector buying authorities accept ArcKit-produced artefacts at face value for the standard supplier governance set, reducing buyer assurance time per supplier engagement.

**Measurement Details**:

- **KPI**: % of buying-authority engagements (where the supplier used ArcKit) that complete supplier-governance review without bespoke document requests.
- **Current Value**: 0 (no GA).
- **Target Value**: ≥ 70% by GA + 12 months.
- **Frequency**: Quarterly (sample of buying-authority feedback).
- **Data Source**: Buyer-side survey + pilot reports.

**Business Value**:

- **Strategic**: Establishes ArcKit as a recognised quality signal — the foundation for everything else.
- **Operational**: Reduces buyer-side review time by an estimated 30–50% per engagement (to be measured in pilots).
- **Customer**: SME suppliers experience fewer assurance-cycle blockers.

**Timeline**:

- Months 1–3 post-GA: pilot reviews; baseline.
- Months 4–6: refinement; evidence pack revision.
- Months 7–12: target attainment.

**Stakeholder Benefits**:

- DDaT EAs / SAs / SecAs (buyers): less translation work.
- SME suppliers: fewer governance-cycle delays.
- CDDO / GDS: more consistent supplier evidence.

**Leading Indicators**: Pilot review scores; in-product evidence-pack download counts.
**Lagging Indicators**: Buyer NPS toward suppliers using ArcKit; share of SME wins associated with ArcKit usage.

---

### Outcome O-2: Material SME Adoption and Activation

**Supported Goals**: G-2, G-7.

**Outcome Statement**: At least 200 verified UK SMEs onboarded within 12 months of GA, with ≥ 60% activating (≥ 3 saved artefacts in 30 days) and ≥ 70% rolling 90-day retention on the SME paid tier.

**Measurement Details**:

- **KPI**: SME tenant register; activation funnel; retention cohort.
- **Target**: 200 / 60% / 70% at GA + 12 months.
- **Frequency**: Monthly cohort report.
- **Data Source**: Tenant register + product analytics.

**Business Value**:

- **Strategic**: Brings cross-subsidy economics within reach (links to O-3).
- **Customer**: More SMEs equipped to win government work.

**Stakeholder Benefits**:

- SME founders: realised win-rate uplift.
- HM Treasury / CCS / CDDO: SME-spend share lifted measurably.

---

### Outcome O-3: Sustainable Cross-Subsidy Economics

**Supported Goals**: G-3, G-7, G-8.

**Outcome Statement**: Cross-subsidy break-even achieved by GA + 18 months and sustained without paywalling governance-critical features.

**Measurement Details**:

- **KPI**: Quarterly affordability report (per Principle 17).
- **Target**: Break-even at month 18; positive contribution thereafter.
- **Data Source**: FinOps tagging; finance ledger.

**Business Value**:

- **Financial**: Breaks the dependency on external runway for the SME tier.
- **Strategic**: Validates Principle 1 as commercially sustainable.

**Stakeholder Benefits**:

- Service Owner: mission protected.
- Finance: predictable model.
- All SME tenants: durable free / low-cost access.

---

### Outcome O-4: No Cross-Tenant Security or Privacy Incidents

**Supported Goals**: G-4, G-5.

**Outcome Statement**: Zero cross-tenant data incidents; zero ICO enforcement actions; zero confirmed breach incidents above the regulatory notification threshold.

**Measurement Details**:

- **KPI**: Incident register; ICO correspondence log; pen-test findings.
- **Target**: 0 / 0 / 0 — sustained.
- **Frequency**: Continuous, reported monthly.

**Business Value**:

- **Strategic**: Tenant trust is a one-strike asset; this outcome protects it.
- **Risk**: Avoids existential reputational damage.

---

### Outcome O-5: G-Cloud-Driven Buyer Reach

**Supported Goals**: G-7.

**Outcome Statement**: ≥ 25 distinct UK buying authorities have either procured directly or hosted SME suppliers using ArcKit via G-Cloud within 12 months of GA.

**Measurement Details**:

- **KPI**: G-Cloud callout records; buyer attribution.
- **Target**: 25 by GA + 12 months.

---

### Outcome O-6: Accessibility Conformance Sustained

**Supported Goals**: G-6.

**Outcome Statement**: WCAG 2.2 AA conformance maintained release on release; Accessibility Statement current; zero critical regressions.

**Measurement Details**:

- **KPI**: CI a11y green; manual-AT report per release; EHRC complaints log.
- **Target**: 100% / 100% / 0.

---

### Outcome O-7: Pluggable AI Architecture Validated

**Supported Goals**: G-8.

**Outcome Statement**: Quarterly CI run on the alternative AI provider passes; provider switch achievable in ≤ 5 working days.

**Measurement Details**:

- **KPI**: Quarterly CI report; documented switch test.

---

## Complete Traceability Matrix

### Stakeholder → Driver → Goal → Outcome

| Stakeholder | Driver ID | Driver Summary | Goal ID | Goal Summary | Outcome ID | Outcome Summary |
|-------------|-----------|----------------|---------|--------------|------------|-----------------|
| DDaT Enterprise Architect (buyer) | SD-1 | Trustable supplier artefacts | G-1, G-4, G-5, G-6 | DDaT-recognisable artefacts | O-1 | Buyer trust |
| DDaT Solution Architect (buyer) | SD-2 | Decision traceability / ADRs | G-1 | DDaT-recognisable artefacts | O-1 | Buyer trust |
| DDaT Security Architect (buyer) | SD-3 | CAF / SbD / threat modelling | G-1, G-4 | DDaT artefacts + CAF posture | O-1, O-4 | Buyer trust + zero incidents |
| DDaT Data / Technical Architect | SD-4 | Diagrams, data models, integration | G-1 | DDaT-recognisable artefacts | O-1 | Buyer trust |
| DDaT Business / Network Architect | SD-5 | Business + infra views | G-1 | DDaT-recognisable artefacts | O-1 | Buyer trust |
| SME Architect | SD-6 | Affordable credible evidence | G-1, G-2 | DDaT artefacts + 5-day pack | O-1, O-2 | Buyer trust + SME adoption |
| SME Founder / Bid Lead | SD-7 | Win rate / cost predictability | G-2, G-7 | 5-day pack + G-Cloud reach | O-2, O-5 | SME adoption + buyer reach |
| Vendor Service Owner | SD-8 | Mission and sustainability | G-3, G-1 | Cross-subsidy + DDaT artefacts | O-3, O-1 | Sustainable economics |
| Vendor Lead Architect | SD-9 | Sustainable engineering | G-1, G-8 | Artefacts + pluggable AI | O-1, O-7 | Buyer trust + pluggability |
| Vendor Security Lead | SD-10 | Audit-defensible posture | G-4 | CAF / Cloud Sec posture | O-4 | Zero incidents |
| Vendor DPO | SD-11 | UK GDPR posture | G-5 | UK GDPR / DPA posture | O-4 | Zero incidents |
| NCSC | SD-12 | Sectoral posture | G-4 | CAF / Cloud Sec | O-4 | Zero incidents |
| ICO | SD-12 | UK GDPR enforcement | G-5 | UK GDPR / DPA | O-4 | Zero incidents |
| HM Treasury / CCS / CDDO | SD-13 | SME spend share | G-7, G-3 | G-Cloud + cross-subsidy | O-2, O-3, O-5 | Adoption + economics + reach |
| GDS Assessors | SD-14 | Service Standard quality | G-1, G-6 | Artefacts + accessibility | O-1, O-6 | Buyer trust + a11y |

### Conflict Analysis

**Competing Drivers**:

- **Conflict 1 — Free-tier richness vs cost sustainability**. SD-6 / SD-7 want the free tier as rich as possible; SD-8 / SD-13 / vendor Finance need the cross-subsidy to break even (G-3). **Resolution**: per `ARC-001-REQ-v1.0.md` Conflict C-1 — governance-critical features unpaywalled, AI generation and bulk export metered, quotas reviewed annually. Decision authority: Service Owner.

- **Conflict 2 — AI provider concentration vs portability**. Vendor Finance and SD-9 partly conflict: cost pressure pushes single-provider concentration; SD-9 / Principle 4 push pluggability. **Resolution**: per Conflict C-2 — pluggable abstraction with a single live SaaS provider and a second provider validated quarterly in CI. Decision authority: Lead Architect with Service Owner ratification.

- **Conflict 3 — Self-service speed vs SME verification rigour**. SD-7 wants instant onboarding; SD-8 / SD-11 require Companies House verification + audit retention. **Resolution**: per Conflict C-3 — synchronous verification with provisional access on outage. Decision authority: Service Owner.

- **Conflict 4 — Buyer-side feature demand (deep) vs SME-side feature demand (broad and simple)**. DDaT EAs in big departments may push for advanced features (lineage to specific departmental standards, bespoke evidence templates) that complicate the SME-friendly product. **Resolution**: maintain a strict baseline-features-on-free-tier line (Principle 1); advanced/department-specific features ship in paid tiers or as enterprise add-ons; SME tier remains opinionated and curated. Decision authority: Product Manager with Service Owner.

**Synergies**:

- **Synergy 1**: SD-1 / SD-2 / SD-3 (buyer DDaT) and SD-6 / SD-7 (SME) align around credible, DDaT-aligned artefacts. Investment that satisfies the buyer satisfies the SME.
- **Synergy 2**: SD-3 (buyer Security Architect), SD-10 (vendor Security Lead), SD-12 (NCSC) align around CAF and Cloud Security Principles posture. One assessment evidences for all three audiences.
- **Synergy 3**: SD-13 (HMG SME spend) and SD-7 (SME founder win rate) align directly: every SME win is HMG progress against its own SME-spend target.
- **Synergy 4**: SD-14 (GDS assessors) and SD-1 / SD-2 align around Service Standard alignment; assessor-friendly artefacts are buyer-EA-friendly artefacts.

---

## Communication & Engagement Plan

### DDaT Architecture Community (Buyer Side)

**Primary Message**: "ArcKit produces architecture artefacts in the language and format your DDaT colleagues expect — TCoP-aligned, Service-Standard-mappable, NCSC-friendly. SME suppliers using ArcKit cost you less to assure."

**Key Talking Points**:

- Format conventions (ARC-* IDs, ADR alternatives sections, traceability matrices).
- Independent assurance evidence (CAF, Cloud Security Principles) one click away.
- AI-generated content explicitly flagged and traceable.

**Frequency**: Quarterly user group; monthly newsletter; design partnerships with up to 3 buying authorities pre-GA.
**Channels**: GovCamp / cross-government EA meet-ups; CDDO architecture community; LinkedIn DDaT communities.
**Success story**: A buying authority EA reviews a supplier-produced ArcKit pack and signs off without bespoke verification.

---

### SME Architects and Founders

**Primary Message**: "Free for verified UK SMEs. Produce a credible bid-quality governance pack in days. Owned, exportable, portable — your work, your data."

**Key Talking Points**:

- Free tier covers the essentials end-to-end; no time limits.
- Published pricing for paid tier; no "contact sales".
- Full export at any time, no paywall.

**Frequency**: In-product changelog (per release); community forum; case studies (quarterly).
**Channels**: Product website; GovTech communities; SME Action Plan partner channels.
**Success story**: An SME wins a G-Cloud callout and credits ArcKit-produced governance evidence.

---

### CDDO / GDS / NCSC / ICO

**Primary Message**: "ArcKit lifts the floor of supplier-side governance quality across UK Government, with first-class alignment to your standards."

**Key Talking Points**:

- TCoP / Service Standard / CAF / Cloud Security Principles / WCAG 2.2 AA mapping.
- Quarterly evidence-pack updates.
- Adoption metrics that connect to Procurement Act 2023 SME-spend goals.

**Frequency**: Quarterly liaison meetings; ad-hoc on policy change.
**Channels**: Direct email; GovCamp; cross-government architecture community.

---

### CCS / HM Treasury

**Primary Message**: "ArcKit is on G-Cloud, increases SME-supplier readiness, and operates a transparent cross-subsidy model that visibly delivers value for money for HMG."

**Frequency**: Annual review; G-Cloud framework cycle.
**Channels**: G-Cloud framework liaison; CCS supplier engagement.

---

### Vendor Internal Stakeholders (Service Owner, Architect, Security, DPO, Finance, A11y, SRE)

**Primary Message**: Operational excellence cadence — weekly delivery, monthly architecture forum, monthly FinOps review, quarterly affordability and security forum.

---

## Change Impact Assessment

### Impact on Stakeholders

| Stakeholder | Current State | Future State | Change Magnitude | Resistance Risk | Mitigation |
|-------------|---------------|--------------|------------------|-----------------|------------|
| DDaT EAs / SAs (buyers) | Bespoke supplier-doc translation | Recognised ArcKit format | MEDIUM | LOW | Pilots; design partnerships; format consistency |
| DDaT Sec Architects (buyers) | Vendor-specific security docs | NCSC-aligned ArcKit evidence | MEDIUM | LOW | NCSC-aligned templates; evidence pack |
| SME Architects | Bespoke or ad-hoc EA artefacts | ArcKit free tier | HIGH | LOW (positive change) | Onboarding tour; community examples |
| SME Founders | Manual bid governance investment | Off-the-shelf credible pack | HIGH | LOW | Case studies; pricing transparency |
| CDDO / GDS | Inconsistent supplier evidence | Standardised ArcKit packs | MEDIUM | LOW | Standards mapping documentation |
| NCSC | Variable supplier security posture | NCSC-aligned ArcKit evidence | LOW | LOW | CAF mapping; Cloud Security Principles mapping |
| Vendor SRE | Greenfield ops | Multi-tenant SaaS at scale | HIGH | MEDIUM | Runbooks; SLO discipline; on-call rotation |
| Vendor Finance | No revenue model | Cross-subsidy model | HIGH | MEDIUM | Quarterly affordability reviews; FinOps tagging |

### Change Readiness

**Champions**:

- Service Owner — strategic mission alignment.
- Lead Architect — pluggable architecture appeals to engineering values.
- DDaT EAs at SME-friendly departments — positive policy alignment.
- SME Architects — mostly net positive change (cheaper better tools).

**Fence-sitters**:

- DDaT EAs at large departments with mature in-house EA — must be persuaded ArcKit complements rather than replaces.
- Vendor Finance — needs evidence that cross-subsidy works.

**Resisters**:

- Adjacent commercial EA tooling vendors — competitive pressure (low influence).
- Some SI suppliers who benefit from the SME assurance gap — minor resistance, no direct lever.

---

## Risk Register (Stakeholder-Related)

### Risk SR-1: DDaT-Recognition Failure

**Related Stakeholders**: SD-1, SD-2, SD-3, SD-4, SD-5.
**Description**: Pilot buying authorities reject ArcKit artefact format as not credible enough.
**Impact on Goals**: G-1.
**Probability**: MEDIUM. **Impact**: HIGH.
**Mitigation**: Run alpha + private beta with at least one buying-authority EA in the loop; iterate on format before pilot.
**Contingency**: Format-adjustment release before GA; defer GA if needed.

### Risk SR-2: Cross-Subsidy Slippage

**Related Stakeholders**: SD-8, SD-13, vendor Finance.
**Description**: Adoption (BR-008) below cross-subsidy break-even threshold by GA + 18 months.
**Impact on Goals**: G-3.
**Probability**: MEDIUM. **Impact**: HIGH.
**Mitigation**: Quarterly affordability review; AI-cost lever (Conflict C-1); enterprise sales motion.
**Contingency**: Adjust quotas (not feature paywalls); seek targeted public-sector / philanthropic co-funding.

### Risk SR-3: Cross-Tenant Incident

**Related Stakeholders**: SD-10, SD-11, all tenants.
**Description**: Defect or operator error leaks data between tenants.
**Impact on Goals**: G-4, G-5; existential platform risk.
**Probability**: LOW. **Impact**: CRITICAL.
**Mitigation**: Tenant-isolation tests in CI; default-deny; pen testing; bulkhead patterns.
**Contingency**: Incident response plan; ICO notification within 72 hours; transparent post-incident review.

### Risk SR-4: AI Provider Lock-In or Disruption

**Related Stakeholders**: SD-9, vendor Finance.
**Description**: Selected AI provider changes terms, prices, or availability.
**Impact on Goals**: G-8.
**Probability**: MEDIUM. **Impact**: MEDIUM.
**Mitigation**: Pluggable abstraction; quarterly CI on second provider.
**Contingency**: Provider switch within 5 working days.

### Risk SR-5: Accessibility Regression Discovered Externally

**Related Stakeholders**: SD-14, EHRC.
**Description**: External user (or EHRC) reports an accessibility defect not caught in CI.
**Impact on Goals**: G-6.
**Probability**: MEDIUM. **Impact**: MEDIUM.
**Mitigation**: Automated a11y in CI plus manual AT testing per release; vulnerability-disclosure-like channel for accessibility.
**Contingency**: Hot-fix release; updated Accessibility Statement.

### Risk SR-6: G-Cloud Listing Slippage

**Related Stakeholders**: SD-13.
**Description**: G-Cloud framework iteration deadline missed.
**Impact on Goals**: G-7, O-5.
**Probability**: MEDIUM. **Impact**: HIGH.
**Mitigation**: Engage CCS liaison early; treat listing as a first-class GA dependency.
**Contingency**: List in next iteration; bridge with direct procurement support for early buyers.

### Risk SR-7: SME Verification Brittleness

**Related Stakeholders**: SD-7, SD-8.
**Description**: Companies House change or outage disrupts onboarding.
**Impact on Goals**: G-2, O-2.
**Probability**: LOW. **Impact**: MEDIUM.
**Mitigation**: Defensive parsing; provisional access on outage (Conflict C-3 resolution).
**Contingency**: Manual verification fallback.

---

## Governance & Decision Rights

### Decision Authority Matrix (RACI)

| Decision Type | Responsible | Accountable | Consulted | Informed |
|---------------|-------------|-------------|-----------|----------|
| Pricing tier changes | Product Manager | Service Owner | Finance, Lead Architect, CCS liaison | All staff, tenant communications |
| SME eligibility policy changes | Product Manager | Service Owner | DPO, Legal, Finance | All staff, tenants |
| Architecture decisions (ADRs) | Lead Architect | Lead Architect | Security Lead, DPO, Service Owner | All engineering |
| Security control acceptance | Security Lead | Service Owner (SIRO-equivalent) | DPO, Lead Architect | All engineering |
| DPIA decisions | DPO | Service Owner | Security Lead, Lead Architect | All staff |
| AI provider selection | Lead Architect | Service Owner | DPO, Security Lead, Finance | All engineering |
| G-Cloud listing content | Product Manager | Service Owner | CCS liaison, Finance | All staff |
| Free-tier limit changes | Product Manager | Service Owner | Finance, Lead Architect, SME tenant council | All staff, tenants |
| Pilot acceptance with buying authority | Service Owner | Service Owner | Lead Architect, Product Manager, DDaT EA pilot lead | All staff |
| Incident response decisions (severe) | Service Owner | Service Owner | Security Lead, DPO, Legal, comms | All staff, ICO/NCSC if applicable |
| Go / no-go for GA | Service Owner | Service Owner | All Manage-Closely stakeholders | All |

### Escalation Path

1. **Level 1 — Day-to-day operational decisions**: Product Manager / Delivery Manager / SRE on-call.
2. **Level 2 — Material scope, pricing, or risk**: Lead Architect / Security Lead / DPO / Finance — to Service Owner.
3. **Level 3 — Strategic, mission-critical, or external escalation**: Service Owner.
4. **Level 4 — Regulatory or legal escalation**: ICO / NCSC / legal counsel as required (DPO and Security Lead initiate).

---

## Validation & Sign-off

### Stakeholder Review

| Stakeholder | Review Date | Comments | Status |
|-------------|-------------|----------|--------|
| Service Owner (Mark Craddock) | [PENDING] | | [PENDING] |
| Lead Architect (vendor) | [PENDING] | | [PENDING] |
| Security Lead (vendor) | [PENDING] | | [PENDING] |
| DPO (vendor) | [PENDING] | | [PENDING] |
| Accessibility Lead (vendor) | [PENDING] | | [PENDING] |
| CCS liaison | [PENDING] | | [PENDING] |
| Pilot DDaT EA (buyer) | [PENDING] | | [PENDING] |
| SME tenant representative | [PENDING] | | [PENDING] |

### Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Service Owner | Mark Craddock | _________ | [PENDING] |
| Lead Architect | [PENDING] | _________ | [PENDING] |
| DPO | [PENDING] | _________ | [PENDING] |

---

## Appendices

### Appendix A: DDaT Architecture Role Reference

Source: [DDaT Capability Framework](https://ddat-capability-framework.service.gov.uk/). Each role has skill levels (Awareness, Working, Practitioner, Expert). Architects in the public sector typically span two levels in any given skill.

| Role | Primary Focus | Typical ArcKit Use |
|------|---------------|--------------------|
| Enterprise Architect | Departmental coherence, target architectures, portfolio steering | `/arckit:strategy`, `/arckit:roadmap`, `/arckit:principles-compliance` |
| Solution Architect | End-to-end programme/project design, design reviews | `/arckit:adr`, `/arckit:hld-review`, `/arckit:dld-review`, `/arckit:traceability` |
| Data Architect | Enterprise data design, data governance | `/arckit:data-model`, `/arckit:dpia`, `/arckit:data-mesh-contract` |
| Security Architect | Threat modelling, security control design, CAF alignment | `/arckit:secure`, `/arckit:tcop`, `/arckit:risk` |
| Business Architect | Capability mapping, business architecture | `/arckit:stakeholders`, `/arckit:strategy`, `/arckit:requirements` |
| Technical Architect | Platform / infrastructure design, build/buy/reuse calls | `/arckit:research`, `/arckit:diagram`, `/arckit:adr` |
| Network Architect | Network design, topology, segmentation | `/arckit:diagram` (deployment view) |

### Appendix B: References

- `projects/000-global/ARC-000-PRIN-v2.0.md` — Architecture Principles (current)
- `projects/001-arckit-saas/ARC-001-REQ-v1.0.md` — Requirements (current)
- DDaT Capability Framework — https://ddat-capability-framework.service.gov.uk/
- Government Functional Standard for Digital (GovS 005)
- Government Functional Standard for Security (GovS 007)
- UK Government Technology Code of Practice
- GDS Service Standard
- NCSC Cyber Assessment Framework; NCSC Cloud Security Principles
- UK GDPR / Data Protection Act 2018
- Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018
- Procurement Act 2023; Cabinet Office SME Action Plan

### Appendix C: Open Items

- Validate stakeholder set with the Service Owner.
- Recruit ≥ 3 buying-authority pilots before GA – 60 days.
- Recruit ≥ 1 representative from each DDaT architecture role for the user research panel.
- Establish quarterly cadence for the cross-government EA user group.

---

## External References

> No external policy documents were placed in `projects/001-arckit-saas/external/` at the time of generation. UK Government policies referenced are public-domain and cited by name.

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
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
