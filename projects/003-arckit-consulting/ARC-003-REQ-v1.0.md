# Project Requirements: ArcKit Consulting (UK Public Sector Practice)

> **Template Origin**: Official | **ArcKit Version**: 4.19.0 | **Command**: `/arckit:requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-003-REQ-v1.0 |
| **Document Type** | Business and Technical Requirements |
| **Project** | ArcKit Consulting (Project 003) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-07 |
| **Last Modified** | 2026-05-07 |
| **Review Cycle** | 6-monthly |
| **Next Review Date** | 2026-11-07 |
| **Owner** | Mark Craddock (ArcKit Consulting Practice Lead) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | ArcKit Consulting leadership, Architecture Review Board, Crown Commercial Service liaison, prospective consultants |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-07 | ArcKit AI | Initial creation from `/arckit:requirements` command. Establishes ArcKit Consulting as a UK Public Sector enterprise architecture delivery practice using the ArcKit toolkit. | [PENDING] | [PENDING] |

## Document Purpose

Defines the business and technical requirements for **ArcKit Consulting** — the professional-services arm that uses the ArcKit enterprise architecture governance toolkit to deliver advisory, design, and assurance engagements for the UK Public Sector and the SMEs that supply it. This document is the source-of-truth for downstream operating-model design, framework applications (G-Cloud, DOS, MCF), engagement-tooling decisions, vendor selection, internal controls, and quality assurance for the consulting practice.

ArcKit Consulting is a **complementary channel** to:

- **Project 001 — ArcKit as a Service (managed SaaS)** — the multi-tenant product
- **Project 002 — ArcKit Sovereign** — the air-gapped / sensitive-site deployment

This document covers ArcKit Consulting only. The product projects have their own requirements documents.

> **Upstream artefact gaps** (must be remedied before this document is approved):
>
> - **Stakeholder Analysis (STKE-003)** — not yet created. Stakeholders below are derived from the principles, the consulting model, and the project context. They MUST be validated by running `/arckit:stakeholders` for project 003.
> - **Strategic Outline Business Case (SOBC-003)** — not yet created. Cost, revenue, and ROI figures in this document are indicative target ranges only; values MUST be validated by running `/arckit:sobc` for project 003.
> - **Risk Register (RISK-003)** — not yet created. Risks below are derived from recognisable consulting-business and public-sector-procurement risk patterns; the formal register MUST be created with `/arckit:risk` for project 003.
> - **Architecture Principles** — global principles `ARC-000-PRIN-v2.0.md` apply (ArcKit-as-a-Service is the platform context); a focused review of which principles apply to a *consulting* business may be warranted via `/arckit:principles` if material gaps are found.

---

## Executive Summary

### Business Context

The UK Government is committed to spending more with SMEs (Procurement Act 2023; SME Action Plans; the £1-in-£3 SME spend ambition) and to faster, more digital delivery of public services (CDDO Cloud Strategy; GDS Service Standard; Technology Code of Practice). Two recurring frictions impede that ambition:

1. **Capability asymmetry**. SMEs supplying government rarely have the in-house enterprise-architecture capability that large System Integrators take for granted. Without it they struggle to produce the assurance evidence (security, accessibility, data protection, code-of-practice) that buyers now expect by default.
2. **Adoption gap of governance tooling**. Even where buyers and SMEs adopt structured governance toolkits like ArcKit, the gap between "tool installed" and "evidence-grade artefacts produced and owned by the team" is wide. It is closed by people, not licences.

ArcKit Consulting closes both gaps. It deploys experienced consultants — using the ArcKit toolkit as the delivery medium — into engagements with UK government departments, ALBs, devolved administrations, local authorities, NHS bodies, MOD (where appropriate), and the SMEs supplying them. Engagements range from short discovery / readiness assessments through full design and assurance support to long-running advisory retainers.

The practice is operated under **OFFICIAL** classification by default, with **OFFICIAL-SENSITIVE** handling caveats where engagements require it. Engagements at OFFICIAL-SENSITIVE and above on sensitive sites are delivered using the Sovereign deployment (Project 002) rather than the managed SaaS (Project 001).

### Objectives

- Establish ArcKit Consulting as a recognised, listed UK public-sector enterprise-architecture delivery practice within 12 months of GA.
- Deliver evidence-grade governance artefacts (principles, requirements, ADRs, designs, compliance assessments) that withstand independent assurance.
- Cross-subsidise the SME-affordable free tier of ArcKit as a Service (Principle 1, `ARC-000-PRIN-v2.0.md`) by generating profitable revenue from larger public sector and enterprise engagements.
- Build a public corpus of reusable patterns, anonymised case studies, and contributions to government open code (Principle 16, Open Source First and Reuse Before Build).
- Provide a permanent, structured feedback channel from real client engagements back into the ArcKit product roadmap.

### Expected Outcomes

- **Listings**: live G-Cloud listing and Digital Outcomes (DOS) listing on the Crown Commercial Service Digital Marketplace within 6 months of GA.
- **Pipeline**: at least 25 qualified opportunities and 8 won engagements in year 1.
- **Delivery quality**: 100% of client deliverables pass the ArcKit quality checklist before sign-off; client NPS ≥ +40.
- **SME affordability**: a documented and externally verifiable pro-bono / pro-rata pricing tier delivers at least 5 SME engagements in year 1 at zero or substantially-reduced cost.
- **Cross-subsidy**: at least 10% of consulting net margin earmarked annually to the ArcKit-as-a-Service SME free tier.
- **Reuse contribution**: at least 4 anonymised case studies and 2 reusable open-source artefacts published in year 1.
- **Compliance**: Cyber Essentials Plus, ICO data-controller registration, and (where headcount/turnover thresholds are crossed) modern slavery and gender pay gap statements published.

### Project Scope

**In Scope**:

- A UK-resident professional-services consulting practice trading under the ArcKit Consulting brand.
- Engagement lifecycle from opportunity identification through contracting, delivery, sign-off, and warranty.
- Use of the ArcKit toolkit (Project 001 SaaS for OFFICIAL; Project 002 sovereign for sensitive sites) as the delivery medium for engagements.
- A consultant operating model: roles, levels, capacity, utilisation, capability development, security clearances.
- Knowledge management: anonymised IP, template library, lessons learned.
- Client-data confidentiality controls separating each engagement.
- Routes to market: G-Cloud, DOS, sub-contracting under existing Crown CS frameworks and prime contractors, direct SME outreach.
- Pricing models: day-rate, fixed-price, outcome-based, retainer, pro-bono SME tier.
- Quality assurance and peer review of all deliverables.
- Regulatory compliance for the consulting entity itself (UK GDPR, ICO registration, Companies Act, HMRC obligations, employment law, Cyber Essentials Plus).

**Out of Scope** (deferred or explicitly excluded):

- Operating the ArcKit SaaS or sovereign deployments (those are products in Projects 001 and 002).
- Licence resale of third-party EA tooling (ArcKit Consulting is not a software reseller).
- Engagements outside the UK Public Sector and SMEs supplying it (e.g., pure private-sector enterprise advisory beyond cross-subsidy capacity is excluded in v1).
- Engagements that require classifications above OFFICIAL-SENSITIVE *unless* delivered through Project 002 sovereign with appropriate accreditation by the deploying authority.
- Permanent staff placement / recruitment as a primary service line.
- Bespoke software build engagements where ArcKit governance is not the centre of the work (refer to specialist build partners; ArcKit Consulting may co-deliver as architecture lead).

---

## Stakeholders

> ⚠️ Placeholder set — to be validated and refined by `/arckit:stakeholders` for project 003.

| Stakeholder | Role | Organisation | Involvement Level |
|-------------|------|--------------|-------------------|
| Mark Craddock | Practice Lead / SRO | ArcKit Consulting | Decision maker |
| [TBD] | Engagement Director (Practice Operations) | ArcKit Consulting | Day-to-day operational lead |
| [TBD] | Quality Assurance Lead | ArcKit Consulting | Deliverable sign-off, peer-review oversight |
| [TBD] | Commercial Lead (Bid & Contracts) | ArcKit Consulting | Bidding, framework listings, contract negotiation |
| [TBD] | Talent Lead | ArcKit Consulting | Consultant recruitment, capability development, clearances |
| [TBD] | DPO / Information Governance Lead | ArcKit Consulting | Information governance, ICO liaison |
| Crown Commercial Service framework managers | Framework owners | CCS | Framework eligibility and conduct |
| GDS / CDDO Service Assessment teams | Assurance bodies | Cabinet Office | Service Standard evidence consumers |
| Client Senior Responsible Owners | Buyer | Various UK gov bodies | Engagement sponsors |
| Client Architect / SME Founder | Engagement counterpart | Various | Day-to-day delivery counterpart |
| Sub-contractor partners | Delivery capacity | Various SMEs / boutiques | Capacity flex, specialist skills |
| ArcKit Product team (Project 001 / 002) | Internal partner | ArcKit | Tooling support, feedback recipient |
| HMRC, ICO, Companies House | Regulators | UK Gov | Statutory compliance |
| ArcKit Architecture Review Board | Internal governance | ArcKit | Cross-project alignment, exception approval |

---

## Business Requirements

### BR-001: Establish a UK Public Sector EA delivery practice

**Description**: Stand up ArcKit Consulting as a registered UK trading entity with the legal, financial, regulatory, and brand foundations needed to operate as a UK public sector consulting supplier.

**Rationale**: A consulting practice cannot bid for, deliver against, or invoice public sector engagements without the underlying legal and compliance foundations. Public sector buyers require evidence of corporate standing, regulatory registrations, and minimum security posture before any engagement begins.

**Success Criteria**:

- UK limited company (or appropriate vehicle) incorporated and Companies House records public.
- ICO data-controller registration in place.
- Cyber Essentials Plus certified within 90 days of incorporation.
- Public website live with services, pricing principles, accessibility statement, and contact route.
- Insurance in place: professional indemnity (≥ £5m), public liability (≥ £5m), employer's liability (≥ £10m where staff present), cyber liability proportionate to engagement portfolio.
- HMRC registrations complete (corporation tax, PAYE if applicable, VAT once threshold crossed).

**Priority**: MUST_HAVE

**Stakeholder**: Practice Lead, Commercial Lead, DPO

---

### BR-002: List on relevant UK public sector procurement frameworks

**Description**: Achieve listings on the Crown Commercial Service Digital Marketplace frameworks that buyers most commonly use to procure enterprise architecture services — at minimum **G-Cloud** (Cloud Software / Cloud Support) and **Digital Outcomes (DOS)** as a specialist supplier.

**Rationale**: Most UK public sector EA engagements are awarded through framework call-off rather than open tender. Without framework listings, the practice is excluded from the majority of the addressable market. Framework listing is also evidence to clients of basic supplier standing.

**Success Criteria**:

- G-Cloud listing live with at least one Cloud Support service entry covering ArcKit-led architecture services, accurate service definition, transparent published pricing, and SLAs aligned to NFRs in this document.
- DOS listing live as a "Specialist" supplier covering at minimum: enterprise architect, business architect, security architect, data architect, and digital architect roles.
- Sub-contractor relationships established with at least 2 prime contractors holding Management Consultancy Framework (MCF) or equivalent positions.
- Listings refreshed each iteration of the framework without lapse.

**Priority**: MUST_HAVE

**Stakeholder**: Commercial Lead, Practice Lead

**Compliance**: Procurement Act 2023; Crown Commercial Service framework terms; PPN compliance (e.g., PPN 03/23 prompt payment, PPN 06/21 cyber, PPN 09/22 modern slavery).

---

### BR-003: Onboard a baseline cohort of qualified consultants

**Description**: Recruit, contract, and onboard a baseline cohort of consultants — substantively employed and / or under associate / sub-contractor agreements — covering the role mix needed to deliver typical engagements end-to-end.

**Rationale**: Consulting capacity is the deliverable. Without a credible bench, the practice cannot honour engagements it wins, and listing applications cannot evidence relevant case studies. Cohort design must balance employment cost against utilisation realism.

**Success Criteria**:

- Baseline cohort live within 6 months of GA: at least 1 Practice Lead, 2 Principal Consultants, 3 Senior Consultants, 2 Consultants, plus a panel of at least 5 trusted associates available for surge.
- Each consultant: signed contract, NDA, conflicts-of-interest declaration, baseline DBS / right-to-work check, ArcKit toolkit accreditation, IR35 status determination where relevant.
- Consultants requiring access to OFFICIAL-SENSITIVE engagements: BPSS as a baseline; SC clearance application initiated where engagements likely require it.
- Documented capability matrix mapping consultants to engagement types and architectures.

**Priority**: MUST_HAVE

**Stakeholder**: Talent Lead, Practice Lead

**Compliance**: Employment Rights Act 1996; IR35 / off-payroll working rules; Equality Act 2010; Modern Slavery Act 2015 (statement once turnover threshold crossed); HMG Baseline Personnel Security Standard (BPSS); Government Security Vetting (SC, DV) where required by client.

---

### BR-004: Generate sustainable revenue and margin

**Description**: Generate engagement revenue at a level and margin that funds the practice's operating costs, pays competitive consultant rates, and contributes a material cross-subsidy to the SME free tier of ArcKit as a Service.

**Rationale**: A consulting practice that does not generate sustainable margin is not a going concern, cannot honour future engagement commitments, and cannot fund the cross-subsidy to the SME tier required by Principle 1 of `ARC-000-PRIN-v2.0.md`. Margin discipline, not revenue maximisation, is the steering metric.

**Success Criteria** (year 1 targets, indicative — to be validated by SOBC):

- Year-1 booked revenue ≥ £750k (target range £750k–£1.5m subject to SOBC).
- Net consulting margin ≥ 20% after consultant costs, framework fees, tooling, insurance, and overhead.
- ≥ 10% of post-tax net margin earmarked annually as cross-subsidy to ArcKit-as-a-Service SME free-tier capacity (per Principle 17).
- Days-Sales-Outstanding (DSO) ≤ 45 days; aged-debt > 90 days as a percentage of debtors ≤ 5%.
- No engagement loss-making at gross margin level without an explicit pre-approved business reason (e.g., SME pro-bono, deliberate brand investment).

**Priority**: MUST_HAVE

**Stakeholder**: Practice Lead, Commercial Lead

---

### BR-005: Run an SME-affordable engagement tier

**Description**: Provide an explicit, externally verifiable pro-bono / pro-rata engagement tier for verified UK SMEs supplying or seeking to supply public-sector services — directly mirroring the affordability commitment of Principle 1.

**Rationale**: The strategic reason ArcKit exists is to lower the cost of high-quality EA for SMEs supplying UK government. The consulting practice cannot credibly preach SME affordability if it only takes large-fee engagements. The SME tier must be visible, accessible, and not a token gesture.

**Success Criteria**:

- Published SME eligibility policy aligned with the SaaS Principle 1 definition (Companies Act 2006 SME thresholds, supplying or seeking to supply UK gov).
- Pricing structure for SME tier published openly: e.g., capped day rates, fixed-price discovery packages, or pro-bono short engagements.
- ≥ 5 SME engagements delivered in year 1 under the SME tier.
- Cross-subsidy mechanism (per BR-004) explicitly funds the tier; the tier does not depend on volunteer time alone.
- An anonymised SME case study published per quarter.

**Priority**: SHOULD_HAVE

**Stakeholder**: Practice Lead

**Linked Principles**: Principle 1 (Equitable Access for SMEs), Principle 17 (Cost Transparency and FinOps).

---

### BR-006: Deliver evidence-grade governance artefacts

**Description**: Every engagement deliverable produced by ArcKit Consulting MUST meet the ArcKit quality checklist standard, withstand independent assurance review (e.g., GDS Service Assessment, NCSC Cyber Essentials assessment, internal audit), and be accepted by the client as their owned artefact rather than vendor-attached IP.

**Rationale**: The differentiator over generic strategy consulting is **evidence-grade output**. The brand depends on it. A single highly-public failed assurance event would unwind years of brand-building. Deliverables must also be transferable: clients must be able to maintain them after the engagement ends without continuing dependence on the practice.

**Success Criteria**:

- 100% of client deliverables pass the ArcKit quality checklist (`references/quality-checklist.md`) before sign-off.
- 0 instances of a client deliverable failing an external assurance event for an issue introduced or missed by the consulting practice (target).
- Client retention / repeat-engagement rate ≥ 50% in year 2 onwards.
- Average client NPS ≥ +40 across engagements.
- All deliverables produced in open Markdown / OpenAPI / Mermaid formats portable by the client without ArcKit Consulting involvement (Principle 4).

**Priority**: MUST_HAVE

**Stakeholder**: QA Lead, Practice Lead

**Linked Principles**: Principle 4 (Open Standards), Principle 9 (Data Quality, Lineage, and Tenant Portability), Principle 15 (Maintainability and Evolvability).

---

### BR-007: Curate reusable IP and contribute back to government open code

**Description**: Capture, anonymise, and curate engagement IP into a reusable template / pattern library; publish appropriate components openly under OSI-approved licences and to government open-code repositories where they have cross-government reuse value.

**Rationale**: Reuse compounds margin and shortens delivery time on future engagements; equally important, contributing back honours Principle 16 (Open Source First and Reuse Before Build) and the Technology Code of Practice. Without a deliberate IP-curation discipline, the practice rebuilds the same artefacts engagement after engagement, eroding margin and offering nothing back to the wider public sector.

**Success Criteria**:

- IP-capture step is mandatory in the engagement closure checklist (per FR-014).
- Internal pattern library covers ≥ 80% of typical engagement deliverable types within year 1.
- ≥ 4 anonymised case studies published in year 1 (with explicit client consent).
- ≥ 2 reusable artefacts (e.g., template extensions, code patterns, ADR libraries) released as open source / contributed to a UK Government open-code repository in year 1.
- All client engagement contracts include an IP clause permitting anonymised pattern reuse and case-study publication subject to client consent.

**Priority**: SHOULD_HAVE

**Stakeholder**: Practice Lead, QA Lead

**Linked Principles**: Principle 4 (Open Standards), Principle 16 (Open Source First and Reuse).

---

### BR-008: Maintain provable confidentiality and information governance

**Description**: Operate the practice with information governance proportionate to the highest classification handled (default OFFICIAL; OFFICIAL-SENSITIVE on opt-in engagements), with provable controls such that a single client breach does not compromise other clients and a single departing consultant does not exfiltrate client work.

**Rationale**: Confidentiality is the single largest brand and contractual risk for any consulting practice handling government data. Cross-client contamination — accidental or deliberate — destroys trust at scale. Departing-consultant exfiltration is a recognised industry pattern and must be designed out.

**Success Criteria**:

- Each engagement isolated in a dedicated data store / workspace with per-engagement access control.
- Consultants assigned to engagements on a need-to-know basis with auditable access grants and timely revocation on rotation off.
- Cyber Essentials Plus maintained continuously.
- Annual independent penetration test of practice internal systems with material findings remediated within agreed SLA.
- Documented and tested incident response process for: data breach, lost device, departing consultant, client-disclosed breach.
- 0 cross-client data leakage incidents (target).

**Priority**: MUST_HAVE

**Stakeholder**: DPO, Practice Lead

**Linked Principles**: Principle 5 (Security by Design), Principle 7 (UK Data Sovereignty and Governance), Principle 8 (Tenant Isolation).

---

### BR-009: Build a qualified opportunity pipeline

**Description**: Build and maintain a qualified opportunity pipeline that gives the practice forward visibility of demand, supports utilisation planning, and de-risks revenue concentration on any single client or framework.

**Rationale**: Without pipeline, the practice oscillates between bench cost and over-commitment. Without pipeline diversity, the practice is exposed to single-client / single-framework concentration risk. Pipeline discipline is the operational hedge.

**Success Criteria**:

- Pipeline-coverage ratio (qualified opportunity value / forward 90-day capacity) ≥ 3.0 sustained.
- No single client > 30% of forward 90-day booked revenue.
- No single framework > 60% of forward 12-month booked revenue.
- Win-rate on bid opportunities tracked, with quarterly review of declines and losses.
- Pipeline reviewed weekly at practice leadership level.

**Priority**: SHOULD_HAVE

**Stakeholder**: Commercial Lead, Practice Lead

---

### BR-010: Provide structured product feedback to ArcKit (Projects 001 and 002)

**Description**: Operate a structured, periodic feedback loop from live client engagements back to the ArcKit product roadmap (managed SaaS Project 001 and sovereign Project 002), with anonymisation and client-consent controls preserved.

**Rationale**: Real client engagements are the highest-signal product-feedback channel available to a tooling vendor. Squandering that signal — by not capturing it, or by capturing it but failing to relay it to the product team — wastes the strategic asset of running both a product and a consulting arm. Feedback must be structured to be actionable and anonymised to be lawful.

**Success Criteria**:

- Quarterly product-feedback review meeting with the ArcKit product team (Projects 001 / 002).
- Standing template for engagement-derived product feedback (anonymised; tied to capability area / template).
- ≥ 10 product change requests / enhancement suggestions raised per quarter once steady-state.
- Acknowledged process for clients to opt out of feedback derivation (with default opt-in, transparent to clients).

**Priority**: SHOULD_HAVE

**Stakeholder**: Practice Lead, ArcKit Product Owner

---

## Functional Requirements

### User Personas

#### Persona 1: Practice Lead / Director

- **Role**: Senior responsible owner; commercial accountability; final QA sign-off on material engagements.
- **Goals**: Sustainable practice; deliver Principle 1 cross-subsidy; protect brand.
- **Pain Points**: Pipeline visibility, consultant utilisation realism, framework administration overhead, commoditisation pressure on day rates.
- **Technical Proficiency**: High.

#### Persona 2: Engagement Manager

- **Role**: Owns delivery of one or more concurrent engagements end-to-end.
- **Goals**: Deliver scope on time, on budget, at quality; protect consultant team from scope creep; capture lessons.
- **Pain Points**: Client scope creep without contract change; consultant churn mid-engagement; QA gates that slip.
- **Technical Proficiency**: High.

#### Persona 3: Consultant (Senior / Principal / Associate)

- **Role**: Hands-on producer of artefacts using the ArcKit toolkit on client engagements.
- **Goals**: Produce evidence-grade work; develop capability; reasonable utilisation; clear feedback loop.
- **Pain Points**: Context-switching between engagements; inconsistent client tooling access; unclear handover at engagement end.
- **Technical Proficiency**: High.

#### Persona 4: Client SRO (Senior Responsible Owner)

- **Role**: Public-sector buyer authorising the engagement; accountable for engagement outcomes within their organisation.
- **Goals**: Outcome delivered; assurance evidence in hand; team built up; value-for-money defensible at audit.
- **Pain Points**: Lift-and-shift consultancies that leave nothing reusable; rate inflation; consultants whose work doesn't survive independent assurance.
- **Technical Proficiency**: Variable (digital-native to non-digital-native).

#### Persona 5: Client Architect / Counterpart

- **Role**: Embedded client-side architect / engineer working day-to-day with the engagement team.
- **Goals**: Learn through partnership; own the artefacts after handover; not be patronised.
- **Pain Points**: Consultants who hoard knowledge; consultants who don't understand the client's existing context; tooling friction.
- **Technical Proficiency**: High.

#### Persona 6: SME Founder / Architect

- **Role**: SME supplier counterpart on the SME-tier engagements.
- **Goals**: Get to assurance-passing evidence quickly; affordable; learn enough to maintain afterwards.
- **Pain Points**: Cost; consultants who don't grasp SME constraints; tooling priced for enterprises.
- **Technical Proficiency**: High but resource-constrained.

#### Persona 7: Sub-contractor / Associate Partner

- **Role**: External delivery capacity engaged to flex into specific engagements.
- **Goals**: Steady stream of work; clear scoping; prompt payment; preserved long-term relationship.
- **Pain Points**: Late payment; scope drift between practice and end client; ambiguous QA standards.
- **Technical Proficiency**: High.

#### Persona 8: Commercial Lead

- **Role**: Owns bid pipeline, framework listings, contracts, pricing, and procurement compliance.
- **Goals**: Win the right work at the right margin; stay framework-compliant; minimise commercial admin burden on consultants.
- **Pain Points**: Manual bid effort; inconsistent rate cards; framework refresh cycles.
- **Technical Proficiency**: Medium.

---

### Use Cases

#### UC-1: Win a public-sector engagement (bid → contract)

**Actor**: Commercial Lead (primary), Practice Lead, Engagement Manager.

**Preconditions**:

- Practice listed on a relevant framework or directly invited by client / prime.
- Capacity available within the engagement window (or sub-contractor capacity confirmable).

**Main Flow**:

1. Opportunity identified (framework call-off published, direct invitation, partner referral).
2. Qualification check against eligibility, capacity, conflict of interest, capability match, and SME-tier policy if applicable.
3. Bid plan drafted including consultant allocation, sub-contractor needs, and price.
4. Proposal / SOW generated using ArcKit `/arckit:sow` and / or `/arckit:dos` skills, customised for the client.
5. Internal review against pricing floor, capacity, and quality standards; sign-off by Practice Lead.
6. Submission via the framework portal or direct route, within deadline.
7. Clarification questions handled during evaluation.
8. On award: contract negotiated and signed; engagement created in delivery toolchain; kick-off scheduled.

**Postconditions**:

- Signed contract on file.
- Engagement record created with engagement ID, classification, allocated consultants, dates, scope, value, framework reference.
- Pipeline status updated; CRM updated.

**Alternative Flows**:

- **Alt 7a**: If clarification reveals scope drift, re-price and seek client agreement before continuing.
- **Alt 8a**: If lost, capture decline reason; debrief with client where allowed; update pipeline.

**Exception Flows**:

- **Ex 1**: Eligibility check fails (e.g., conflict of interest, framework lapsed) — no-bid recorded with reason.

**Business Rules**:

- No bid below pricing floor without explicit Practice Lead exception (per BR-004).
- No bid that cannot be staffed without a documented sub-contractor capacity plan.

**Priority**: CRITICAL

---

#### UC-2: Deliver an engagement using ArcKit

**Actor**: Engagement Manager (primary), Consultants, Client counterparts.

**Preconditions**:

- Signed contract (UC-1 complete).
- Consultants assigned, NDAs in place, access provisioned to client systems where needed.
- ArcKit deployment selected (managed SaaS for OFFICIAL; sovereign for OFFICIAL-SENSITIVE on sensitive sites).

**Main Flow**:

1. Kick-off meeting with client SRO and counterpart team. Scope, milestones, governance, communications, and security handling agreed.
2. Engagement workspace created in selected ArcKit deployment (per the engagement classification).
3. Discovery: stakeholder analysis (`/arckit:stakeholders`), principles review (`/arckit:principles`), requirements (`/arckit:requirements`).
4. Design / assurance phase: ADRs, designs, compliance assessments, traceability — produced in collaboration with client counterparts (knowledge-transfer-by-doing).
5. Periodic QA gate at agreed milestones — internal peer review against the ArcKit quality checklist.
6. Client review and acceptance per milestone with structured feedback capture.
7. Engagement closure: handover deck, knowledge-transfer session, full export of artefacts to client-controlled storage, IP capture (anonymised), client NPS captured.

**Postconditions**:

- Client owns all engagement artefacts in open formats (Principle 9).
- Anonymised IP captured into the practice's pattern library (per BR-007 and FR-014).
- Engagement record closed; financials reconciled; lessons learned recorded.

**Alternative Flows**:

- **Alt 4a**: If a deliverable type is best supported by the sovereign deployment (Project 002), engagement workspace migrates to sovereign with explicit client agreement.
- **Alt 6a**: If client requests scope change beyond contract: change request raised; re-priced; signed change before further work.

**Exception Flows**:

- **Ex 1**: Quality checklist failure — gate held; rework before client review.
- **Ex 2**: Consultant departure mid-engagement — replacement assigned; client informed; re-induction tracked.

**Business Rules**:

- No deliverable goes to client without QA gate sign-off.
- All client-classified materials handled per client classification regardless of any ArcKit defaults.
- Engagement artefacts accessible only to consultants explicitly assigned to that engagement.

**Priority**: CRITICAL

---

#### UC-3: Onboard a new consultant

**Actor**: Talent Lead (primary), Practice Lead, DPO.

**Preconditions**:

- Approved hire (employee or associate).
- Right-to-work check passed.

**Main Flow**:

1. Contract issued (employment / associate); signed before any system access.
2. NDAs and conflict-of-interest declaration signed.
3. BPSS check completed; SC application initiated where engagement profile likely requires it.
4. ArcKit toolkit accreditation completed (training + assessment).
5. Practice handbook and information-governance training completed.
6. Identity provisioned in practice systems (SSO account, email, time recording).
7. Capability matrix updated; bench availability confirmed.
8. First engagement allocated.

**Postconditions**:

- Consultant fully onboarded with documented evidence of contract, checks, training, and accreditations.
- Consultant searchable in capability matrix and bookable to engagements.

**Exception Flows**:

- **Ex 1**: BPSS or right-to-work issue — onboarding paused; legal review.

**Business Rules**:

- No engagement allocation before all onboarding steps complete.
- No engagement allocation requiring SC clearance until SC granted.

**Priority**: HIGH

---

#### UC-4: Reuse engagement IP for a similar future engagement

**Actor**: Engagement Manager (primary), Consultants.

**Preconditions**:

- Source engagement closed with IP captured per BR-007 and FR-014.
- Source-engagement client consent for anonymised reuse logged.

**Main Flow**:

1. New engagement scoping identifies a pattern match in the IP library.
2. Pattern retrieved with original engagement reference and any caveats / lessons.
3. Pattern applied as starting point — never copy-pasted with client identifiers.
4. Customisation logged so future capture differentiates pattern-derived from new IP.
5. Original engagement archive *not* exposed to the new engagement team beyond the anonymised pattern.

**Business Rules**:

- Reuse must operate from the anonymised pattern library, never from the source engagement workspace.
- Client identifiers, sensitive design specifics, and any data covered by client confidentiality MUST NOT cross engagements.

**Priority**: HIGH

---

#### UC-5: SME pro-bono engagement intake

**Actor**: Practice Lead, Commercial Lead.

**Preconditions**:

- SME tier eligibility policy published.
- Capacity reservation for the SME tier in the current quarter.

**Main Flow**:

1. SME applies via published intake route.
2. Eligibility checked: Companies Act 2006 SME thresholds; supplying or seeking to supply UK gov; not a circumvention of the standard tier (e.g., a captive SME of a large enterprise).
3. Outcome and scope agreed with the SME (typically time-boxed discovery / readiness / specific compliance deliverable).
4. Lightweight contract issued — clearly identifies SME tier and IP / case-study terms.
5. Engagement delivered (as per UC-2 with reduced ceremony where appropriate).
6. Anonymised case study drafted; SME consents (or declines).

**Postconditions**:

- SME has assurance-grade artefacts; practice has potential case study; cross-subsidy expense logged against margin pool (BR-004).

**Business Rules**:

- SME tier capacity is a published commitment, not an ad-hoc favour. Failure to deliver the planned SME engagements in a year is a Principle-1 compliance issue.

**Priority**: HIGH

---

#### UC-6: Quality assure deliverables before client sign-off

**Actor**: QA Lead (primary), Engagement Manager, Independent Reviewer (consultant not on the engagement).

**Preconditions**:

- Deliverable in DRAFT or IN_REVIEW state in the engagement workspace.
- ArcKit quality checklist applicable to the deliverable type identified.

**Main Flow**:

1. Engagement Manager raises QA request once deliverable is review-ready.
2. Independent reviewer assigned (must not be on the engagement).
3. Reviewer applies the relevant ArcKit quality checklist (Common + per-type).
4. Findings logged with severity (blocker / major / minor).
5. Engagement team remediates blocker / major findings; minor findings logged for follow-up.
6. Reviewer re-checks remediation.
7. QA gate marked passed; deliverable cleared for client review.

**Postconditions**:

- Deliverable status updated; QA log retained as audit evidence.

**Exception Flows**:

- **Ex 1**: Repeated QA failure (≥ 2 cycles on the same deliverable) — Practice Lead escalation; root-cause review.

**Priority**: CRITICAL

---

### Functional Requirements Detail

#### FR-001: Opportunity capture and qualification

**Description**: The practice MUST maintain a structured opportunity register capturing each identified opportunity from initial sighting through to bid / no-bid decision, with mandatory qualification fields.

**Relates To**: BR-002, BR-009, UC-1.

**Acceptance Criteria**:

- [ ] Each opportunity has a unique ID, source (framework, prime, direct), client name, classification, indicative value, indicative dates, decision status.
- [ ] Mandatory qualification questions answered before bid go / no-go: capability fit, capacity fit, conflict-of-interest check, framework eligibility, SME-tier applicability.
- [ ] Pipeline-coverage ratio computed weekly against forward 90-day capacity (BR-009).
- [ ] No single-client or single-framework concentration thresholds breached without escalation (BR-009).

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

**Dependencies**: Identity / SSO provisioned (FR-018); CRM / pipeline tooling chosen (INT-009).

---

#### FR-002: Proposal and SOW generation

**Description**: The practice MUST generate proposals and Statements of Work using the ArcKit `/arckit:sow` skill (or `/arckit:dos` for DOS specialist roles), with practice-customised templates that comply with framework rules and embed standard contract and information-governance clauses.

**Relates To**: BR-002, UC-1.

**Acceptance Criteria**:

- [ ] Proposal templates customised in `.arckit/templates/` for the practice (per `/arckit:customize`).
- [ ] Proposal templates include: scope, deliverables with acceptance criteria, price, milestones, IP / reuse clause, information-governance clause, cross-subsidy disclosure where SME tier applies.
- [ ] Average proposal turnaround ≤ 5 working days from RFP receipt to internal sign-off.
- [ ] SOWs cite framework reference, applicable PPNs, classification, and deliverable acceptance criteria.

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

**Dependencies**: BR-002 (framework listings), template customisation discipline.

---

#### FR-003: Engagement creation and classification

**Description**: On contract award, the practice MUST create an engagement record linked to the source opportunity, with mandatory classification, scope, dates, value, allocated consultants, and selected ArcKit deployment (SaaS / sovereign).

**Relates To**: BR-008, UC-1, UC-2.

**Acceptance Criteria**:

- [ ] Engagement ID auto-generated and unique.
- [ ] Classification set explicitly (OFFICIAL / OFFICIAL-SENSITIVE) — no default-permissive setting.
- [ ] Engagement workspace created in the selected ArcKit deployment with isolation per client.
- [ ] Allocated consultants and engagement counterparts captured with role and start date.
- [ ] Engagement immutable fields (contract reference, framework reference, classification) protected from later edit without audit log.

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

**Dependencies**: ArcKit Project 001 / 002 platforms.

---

#### FR-004: Engagement workspace isolation

**Description**: Each engagement MUST be delivered in a dedicated workspace that prevents cross-engagement data access. Consultants gain access only when explicitly assigned to that engagement and lose access on rotation off.

**Relates To**: BR-008, NFR-SEC-001, NFR-SEC-002, Principle 8.

**Acceptance Criteria**:

- [ ] Per-engagement access control: consultant assignment ↔ access grant.
- [ ] Access revocation within 1 working day of consultant rotation off the engagement.
- [ ] No shared "all engagements" view exists for non-leadership consultants.
- [ ] Audit log of all access grants, revocations, and engagement-workspace document opens.
- [ ] Automated test on a quarterly basis demonstrating cross-workspace access is impossible.

**Priority**: MUST_HAVE.

**Complexity**: HIGH.

**Dependencies**: ArcKit Project 001 (managed SaaS isolation); identity / SSO provider.

---

#### FR-005: Consultant capability matrix and capacity tracking

**Description**: The practice MUST maintain a current capability matrix mapping each consultant to skills, certifications, clearances, sector experience, and current engagement load, used for allocation decisions and pipeline sizing.

**Relates To**: BR-003, BR-009, UC-3.

**Acceptance Criteria**:

- [ ] Each consultant has a profile with skills (taxonomy-defined), levels, sector experience, current clearance, current engagements, and forward bookings.
- [ ] Capacity reports generated weekly: utilisation %, bench %, forward-90-day load, role-mix gaps.
- [ ] Allocation tool surfaces matching consultants for a given opportunity profile.
- [ ] Consultant view of their own profile and bookings (with self-update for skills).

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

**Dependencies**: HR / time-recording integrations (INT-007, INT-009).

---

#### FR-006: Consultant onboarding workflow

**Description**: The practice MUST execute a defined onboarding workflow for each new consultant that gates engagement allocation on completion of contract, NDA, conflict-of-interest, baseline checks, training, and toolkit accreditation.

**Relates To**: BR-003, UC-3.

**Acceptance Criteria**:

- [ ] Workflow steps tracked: contract, NDA, conflicts, BPSS, ArcKit accreditation, IG training, identity provisioning, capability matrix entry.
- [ ] Engagement allocation blocked until all mandatory steps complete.
- [ ] Audit log of all onboarding steps with timestamps and approvers.
- [ ] Re-attestation of NDAs / IG training annually.

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

**Dependencies**: HR / identity / training systems (INT-007, INT-009).

---

#### FR-007: Time recording and engagement financials

**Description**: Consultants MUST record time against engagements daily; the practice MUST reconcile time to budget, invoice clients per the contract schedule, and report margin per engagement and per consultant level.

**Relates To**: BR-004, NFR-C-001, INT-005, INT-006.

**Acceptance Criteria**:

- [ ] Daily time entry with engagement ID, role / activity code, hours.
- [ ] Weekly reminder for any unsubmitted timesheets; missing-timesheet rate ≤ 5% over rolling 4 weeks.
- [ ] Invoice generation aligned to contract milestones / monthly schedule; invoices issued within 5 working days of milestone or month end.
- [ ] Engagement margin computed monthly; loss-leading engagements escalated.
- [ ] Days Sales Outstanding reported monthly (BR-004 target ≤ 45 days).

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

**Dependencies**: Time-recording / accounting integrations (INT-005, INT-006).

---

#### FR-008: Quality assurance gate

**Description**: All client deliverables MUST pass an independent QA gate against the ArcKit quality checklist (`references/quality-checklist.md`) before client sign-off, with the reviewer not assigned to the engagement.

**Relates To**: BR-006, UC-6, NFR-Q-001.

**Acceptance Criteria**:

- [ ] Independent reviewer assignment recorded for every QA gate; same-engagement assignment blocked.
- [ ] Quality checklist Common + per-type checks applied and logged.
- [ ] Findings recorded with severity; blockers and majors must be remediated before pass.
- [ ] QA log retained as an engagement audit artefact.
- [ ] 100% of client-bound deliverables have a passed QA log.

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

**Dependencies**: ArcKit quality checklist; reviewer pool sized to demand.

---

#### FR-009: Client feedback and NPS capture

**Description**: At each milestone and at engagement closure, the practice MUST capture structured client feedback including a Net Promoter Score, qualitative narrative, and named feedback themes.

**Relates To**: BR-006, BR-010.

**Acceptance Criteria**:

- [ ] Feedback questionnaire deployed to a named client respondent at each milestone and closure.
- [ ] NPS computed per engagement and rolled up monthly / quarterly.
- [ ] Qualitative themes coded and surfaced into the product feedback loop (BR-010) where applicable.
- [ ] Client opt-in for case-study reuse captured during closure feedback.

**Priority**: SHOULD_HAVE.

**Complexity**: LOW.

---

#### FR-010: Sub-contractor and associate management

**Description**: Sub-contractors and associates engaged on practice work MUST be onboarded under associate agreements with NDAs, IR35 status determinations where relevant, prompt-payment commitments aligned to PPN 03/23, and the same QA standards as employees.

**Relates To**: BR-003, BR-008, NFR-C-005.

**Acceptance Criteria**:

- [ ] Associate agreement template covers IP, NDA, IR35 status, prompt payment, IG obligations.
- [ ] Each engagement uses an associate registered in the capability matrix with current onboarding status.
- [ ] Same QA gate applied to associate-produced deliverables (FR-008).
- [ ] Associate payment terms ≤ 30 days, evidenced (PPN 03/23 alignment).

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

---

#### FR-011: SME-tier intake and verification

**Description**: The practice MUST operate a published SME-tier intake route with eligibility verification against Companies Act 2006 SME thresholds and a documented "supplying or seeking to supply UK gov" criterion.

**Relates To**: BR-005, UC-5, Principle 1.

**Acceptance Criteria**:

- [ ] Public-facing SME tier policy and intake form live on the practice website.
- [ ] Eligibility verification against Companies House data and a self-declared UK-gov supplier statement.
- [ ] Quarterly capacity reservation for the SME tier published openly.
- [ ] SME engagements tracked and reported separately to confirm BR-005 outcomes.

**Priority**: SHOULD_HAVE.

**Complexity**: MEDIUM.

**Dependencies**: Companies House API / data lookup (INT-003).

---

#### FR-012: Knowledge / IP curation library

**Description**: The practice MUST operate a curated, anonymised pattern / template library that captures reusable engagement IP and is the only authorised reuse channel between engagements.

**Relates To**: BR-007, UC-4.

**Acceptance Criteria**:

- [ ] Library separated logically from any engagement workspace; cross-engagement access from engagement workspaces is impossible.
- [ ] Each pattern has provenance metadata (source-engagement reference, reviewer, date, anonymisation evidence) and reuse caveats.
- [ ] Patterns reviewed for currency at least annually; superseded patterns archived not deleted.
- [ ] Search / browse interface for consultants by capability / engagement type.

**Priority**: SHOULD_HAVE.

**Complexity**: MEDIUM.

---

#### FR-013: Public case-study and open-source contribution workflow

**Description**: A documented workflow for moving anonymised engagement IP to **public** case-study or open-source publication, gated on explicit client consent and information-governance review.

**Relates To**: BR-007, BR-010, Principle 16.

**Acceptance Criteria**:

- [ ] Client consent template captured during engagement closure (FR-014).
- [ ] Anonymisation review by DPO / IG Lead before any external publication.
- [ ] Open-source releases use OSI-approved licences; SBOM provided where applicable; published to a public repository / `code.gov.uk` style index.
- [ ] Case studies follow a published narrative template covering challenge, approach, outcome, lessons.

**Priority**: SHOULD_HAVE.

**Complexity**: MEDIUM.

---

#### FR-014: Engagement closure and IP capture

**Description**: Each engagement MUST execute a closure checklist that includes client artefact handover, knowledge transfer, NPS capture, IP capture into the pattern library, lessons-learned recording, and access revocation.

**Relates To**: BR-006, BR-007, BR-008, UC-2.

**Acceptance Criteria**:

- [ ] Closure checklist mandatory before engagement marked CLOSED.
- [ ] Full export of artefacts to client-controlled storage in open formats (Markdown / OpenAPI / Mermaid / JSON).
- [ ] Anonymisation review of any IP captured into the library.
- [ ] Consultant access revoked within 1 working day of closure.
- [ ] Lessons-learned added to a searchable corpus.

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

---

#### FR-015: Engagement classification handling

**Description**: Engagements at OFFICIAL-SENSITIVE MUST be flagged at creation and routed to controls appropriate to that classification, including (where applicable) sovereign deployment (Project 002), SC-cleared consultant allocation, and restricted distribution.

**Relates To**: BR-008, NFR-SEC-001, NFR-SEC-003, Principle 7.

**Acceptance Criteria**:

- [ ] Classification flag mandatory at engagement creation and propagated to all artefacts in the workspace.
- [ ] OFFICIAL-SENSITIVE engagements blocked from allocation to non-cleared consultants (where SC required by client).
- [ ] OFFICIAL-SENSITIVE engagements default to sovereign deployment (Project 002) unless the client explicitly accepts SaaS at OS-handling caveat.
- [ ] Distribution lists for engagement materials respect classification.

**Priority**: MUST_HAVE.

**Complexity**: HIGH.

**Dependencies**: Project 002 sovereign deployment availability.

---

#### FR-016: Conflict-of-interest checking

**Description**: Each opportunity and each consultant assignment MUST trigger a conflict-of-interest check against current and recent engagements, with declared interests and known affiliations.

**Relates To**: BR-002, NFR-C-008.

**Acceptance Criteria**:

- [ ] Consultant declares interests on onboarding and updates annually or on change.
- [ ] Opportunity qualification (FR-001) includes a CoI check.
- [ ] Consultant assignment to an engagement (FR-005) includes a CoI check.
- [ ] CoI conflicts escalated to Practice Lead with documented decision (decline / mitigate / proceed).

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

---

#### FR-017: Internal incident management

**Description**: The practice MUST operate an information-security and quality-incident register with structured severity, response runbooks, and escalation paths to the Practice Lead, DPO, and (where required) the ICO and / or affected clients.

**Relates To**: BR-008, NFR-SEC-005, NFR-A-002, Principle 5.

**Acceptance Criteria**:

- [ ] Incident register live with severity definitions and response runbooks.
- [ ] 72-hour ICO notification path tested annually for personal-data breaches (UK GDPR).
- [ ] Client-notification clauses honoured per engagement contract.
- [ ] Annual tabletop exercise covering at least: data breach, lost device, departing-consultant exfiltration, framework non-compliance.

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

---

#### FR-018: Identity and SSO

**Description**: All practice systems (engagement workspaces, time recording, CRM, knowledge library, accounting) MUST authenticate via a single sign-on identity provider with MFA enforced and access tied to current employment / associate status.

**Relates To**: BR-008, NFR-SEC-001.

**Acceptance Criteria**:

- [ ] Single IdP (OIDC / SAML 2.0) for all internal systems.
- [ ] MFA enforced for all users; phishing-resistant MFA for privileged accounts.
- [ ] Joiner / mover / leaver workflow updates IdP within 1 working day of HR event.
- [ ] Privileged-access roles separated from standard consultant access.

**Priority**: MUST_HAVE.

**Complexity**: MEDIUM.

**Dependencies**: IdP selection (INT-009).

---

#### FR-019: Public website and accessibility

**Description**: The practice MUST operate a public website that publishes services, pricing principles, SME-tier policy, accessibility statement, contact route, modern slavery statement (where applicable), and ICO registration reference, conforming to WCAG 2.2 AA.

**Relates To**: BR-001, BR-005, NFR-U-002, Principle 12.

**Acceptance Criteria**:

- [ ] Website live with required content listed above.
- [ ] WCAG 2.2 AA conformance evidenced and statement published per PSBAR 2018 (where applicable to the practice as a public-sector supplier touching public-facing services).
- [ ] Automated accessibility checks in deploy pipeline.
- [ ] Manual assistive-tech testing on each material content change.

**Priority**: MUST_HAVE.

**Complexity**: LOW.

---

#### FR-020: Pipeline and CRM management

**Description**: The practice MUST maintain a single CRM / pipeline tool of record covering opportunities, contacts, activities, bid status, and forecast.

**Relates To**: BR-009, FR-001.

**Acceptance Criteria**:

- [ ] Single tool of record; no parallel pipeline spreadsheets.
- [ ] Weekly pipeline review report auto-generated.
- [ ] Concentration metrics (BR-009) computed automatically.
- [ ] GDPR-compliant contact handling with retention rules.

**Priority**: SHOULD_HAVE.

**Complexity**: MEDIUM.

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-001: Proposal turnaround

**Requirement**: Median proposal / SOW turnaround from RFP receipt to internal sign-off ≤ 5 working days; 95th percentile ≤ 8 working days. SME-tier intake decision ≤ 3 working days.

**Measurement Method**: Pipeline tool timestamps from opportunity creation to bid sign-off.

**Priority**: HIGH.

---

#### NFR-P-002: QA gate cycle time

**Requirement**: Median QA gate cycle ≤ 2 working days for standard deliverables; ≤ 4 working days for major artefacts (e.g., HLD Review, Service Assessment).

**Measurement Method**: QA log timestamps.

**Priority**: HIGH.

---

#### NFR-P-003: Engagement closure latency

**Requirement**: Engagement closure (full export to client + access revocation + IP capture) completed within 5 working days of final acceptance.

**Measurement Method**: Engagement record timestamps.

**Priority**: HIGH.

---

### Security Requirements

#### NFR-SEC-001: Workspace isolation

**Requirement**: Each engagement workspace MUST be logically isolated such that consultants not assigned to that engagement cannot read, write, or infer its content.

**Measurement Method**: Quarterly automated isolation tests; manual penetration test of isolation boundary annually.

**Priority**: CRITICAL.

**Linked Principles**: Principle 8.

---

#### NFR-SEC-002: Least-privilege access

**Requirement**: Consultant access to systems and engagement workspaces follows least privilege; access granted only on assignment; revoked within 1 working day of rotation off; privileged access (admin, finance, identity) restricted to named individuals with phishing-resistant MFA.

**Measurement Method**: Quarterly access review; IdP audit logs; spot-checks on rotation-off events.

**Priority**: CRITICAL.

---

#### NFR-SEC-003: Personnel security clearances

**Requirement**: BPSS as a baseline for all consultants. SC clearance pursued for consultants engaging on engagements where clients require it; engagement allocation blocked if SC not in place where contractually required.

**Measurement Method**: HR record audit; engagement allocation block confirmation.

**Priority**: CRITICAL.

---

#### NFR-SEC-004: Encryption in transit and at rest

**Requirement**: All practice systems handling client data MUST encrypt data in transit (TLS 1.3+) and at rest (AES-256 or equivalent) using current cryptographic standards.

**Measurement Method**: Configuration audit; vendor SOC 2 / ISO 27001 evidence; pen test.

**Priority**: CRITICAL.

**Linked Principles**: Principle 5.

---

#### NFR-SEC-005: Vulnerability management

**Requirement**: Cyber Essentials Plus certified continuously. Annual independent penetration test of practice internal systems. Critical vulnerabilities remediated within 7 calendar days; high within 30; medium within 90.

**Measurement Method**: Cyber Essentials Plus certificate; pen test reports; vulnerability tracker.

**Priority**: CRITICAL.

---

#### NFR-SEC-006: Endpoint security

**Requirement**: All consultant endpoints MUST run a managed-device profile with disk encryption, MDM enrolment, EDR, automatic patching, screen lock, and remote-wipe capability. BYOD prohibited for client-data handling.

**Measurement Method**: MDM compliance reports; quarterly audit.

**Priority**: HIGH.

---

#### NFR-SEC-007: Departing-consultant control

**Requirement**: On consultant departure, all access (IdP, engagement workspaces, email, time recording, knowledge library) MUST be revoked within 1 working day; devices recovered or remote-wiped; outstanding NDA obligations re-affirmed; final exit interview includes information-asset return confirmation.

**Measurement Method**: Leaver checklist audit; access logs cross-checked against HR leaver dates.

**Priority**: CRITICAL.

---

### Availability and Resilience Requirements

#### NFR-A-001: Engagement continuity

**Requirement**: Single-consultant illness, leave, or departure MUST NOT cause an engagement milestone to slip by more than 5 working days; cover plan documented per engagement.

**Measurement Method**: Engagement milestone variance reports; cover-plan audit during engagement creation.

**Priority**: HIGH.

---

#### NFR-A-002: Engagement artefact backup

**Requirement**: Engagement artefacts MUST be backed up (within the chosen ArcKit deployment) with RPO ≤ 1 hour and RTO ≤ 8 hours for the engagement workspace. On engagement closure, full export delivered to client-controlled storage.

**Measurement Method**: Backup test reports; closure-export evidence.

**Priority**: HIGH.

**Linked Principles**: Principle 14.

---

#### NFR-A-003: Practice business continuity

**Requirement**: The practice MUST maintain a documented and tested business-continuity plan covering loss of premises, IdP outage, primary-tooling outage, and key-person unavailability. Annual exercise.

**Measurement Method**: BCP document currency; exercise reports.

**Priority**: HIGH.

---

### Scalability and Capacity Requirements

#### NFR-S-001: Concurrent-engagement capacity

**Requirement**: Operating model MUST scale from 5 concurrent engagements at GA to 20 concurrent engagements within 18 months without re-architecture of processes, tooling, or QA capacity.

**Measurement Method**: Capacity modelling; quarterly concurrent-engagement headroom report.

**Priority**: HIGH.

---

#### NFR-S-002: Bench utilisation target

**Requirement**: Steady-state consultant utilisation in the range 65–80% (chargeable hours / contracted hours), accounting for QA, learning, capability development, and bench. Outside this range triggers leadership review.

**Measurement Method**: Time-recording reports.

**Priority**: HIGH.

---

### Compliance and Regulatory Requirements

#### NFR-C-001: UK GDPR / DPA 2018

**Requirement**: The practice MUST comply with UK GDPR and the Data Protection Act 2018 as a controller of practice / consultant / client-contact personal data and as a processor (per contract) of any client-supplied personal data on engagements.

**Compliance Requirements**:

- [ ] ICO data-controller registration in place.
- [ ] Records of Processing Activity (ROPA) maintained.
- [ ] Privacy notice published on the website.
- [ ] DPA / Article 28 clauses present in client engagement contracts where the practice processes client personal data.
- [ ] DPIA conducted for any high-risk processing on a per-engagement basis (`/arckit:dpia`).
- [ ] 72-hour breach notification process tested.

**Measurement Method**: ICO register check; ROPA audit; contract clause review; DPIA register.

**Priority**: CRITICAL.

---

#### NFR-C-002: Companies Act and HMRC

**Requirement**: Statutory filings (annual accounts, confirmation statement, corporation tax, PAYE if applicable, VAT once threshold crossed) MUST be filed on time. Audit thresholds reviewed annually.

**Measurement Method**: Companies House and HMRC portal records.

**Priority**: CRITICAL.

---

#### NFR-C-003: Crown Commercial Service framework compliance

**Requirement**: While listed on G-Cloud, DOS, or any other CCS framework, the practice MUST comply with the framework agreement terms (eligibility, conduct, reporting, prompt-payment, MI returns).

**Measurement Method**: CCS portal; quarterly internal compliance check.

**Priority**: CRITICAL.

---

#### NFR-C-004: Procurement Act 2023 conduct

**Requirement**: Bidding behaviour MUST comply with the Procurement Act 2023 transparency and conduct provisions (no collusion, accurate disclosures, conflict declarations, exclusion-ground self-assessment).

**Measurement Method**: Bid governance records.

**Priority**: CRITICAL.

---

#### NFR-C-005: Cyber Essentials Plus

**Requirement**: Continuous Cyber Essentials Plus certification (a baseline expectation of UK gov suppliers handling OFFICIAL data; PPN 09/14 / PPN 09/23 contexts).

**Measurement Method**: Annual recertification.

**Priority**: CRITICAL.

---

#### NFR-C-006: Modern Slavery and ethical supply

**Requirement**: Once turnover threshold (£36m) reached, publish a Modern Slavery Statement (Modern Slavery Act 2015). Even below threshold, maintain ethical-supply due diligence on associate / sub-contractor relationships.

**Measurement Method**: Statement publication; supplier due-diligence records.

**Priority**: HIGH.

---

#### NFR-C-007: Equality and Inclusion

**Requirement**: Operate equality-of-opportunity recruitment and engagement allocation aligned with the Equality Act 2010. Once headcount threshold (250) reached, publish gender pay gap data.

**Measurement Method**: HR policy records; statutory publications where threshold reached.

**Priority**: HIGH.

---

#### NFR-C-008: Anti-bribery and conflicts of interest

**Requirement**: Bribery Act 2010 compliance with documented anti-bribery policy, gifts-and-hospitality register, and conflict-of-interest register reviewed quarterly. Conflicts material to bidding declared per Procurement Act 2023.

**Measurement Method**: Policy and register audit.

**Priority**: CRITICAL.

---

#### NFR-C-009: PSBAR 2018 and accessibility of practice properties

**Requirement**: Public-facing properties operated by the practice MUST meet WCAG 2.2 AA per the Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018 where in scope, with an Accessibility Statement published.

**Measurement Method**: Automated and manual accessibility tests; statement currency.

**Priority**: HIGH.

**Linked Principles**: Principle 12.

---

#### NFR-C-010: Audit logging and retention

**Requirement**: Comprehensive, tamper-evident audit logs of: identity events, access grants / revocations, engagement-workspace document access, QA gate decisions, financial transactions. Retention ≥ 7 years for financial records, ≥ 6 years for client-contract evidence, ≥ 12 months for technical access logs.

**Measurement Method**: Log integrity checks; retention policy audit.

**Priority**: CRITICAL.

---

### Quality Requirements

#### NFR-Q-001: Deliverable quality

**Requirement**: 100% of client deliverables pass the ArcKit quality checklist (`references/quality-checklist.md`, Common + per-type) before client sign-off.

**Measurement Method**: QA gate logs (FR-008); independent sample audit quarterly.

**Priority**: CRITICAL.

**Linked Principles**: Principle 9, Principle 15.

---

#### NFR-Q-002: Client satisfaction

**Requirement**: Rolling 12-month engagement-weighted Net Promoter Score ≥ +40 across closed engagements; investigation triggered for any single-engagement NPS < 0.

**Measurement Method**: FR-009 NPS data.

**Priority**: HIGH.

---

#### NFR-Q-003: Independent assurance pass-through

**Requirement**: Where a client deliverable is subjected to independent assurance (GDS Service Assessment, NCSC review, internal-audit review, external regulator review), 0 substantive failures attributable to consulting practice work (rolling 12-month target).

**Measurement Method**: Post-assurance review; root-cause analysis on any failure.

**Priority**: HIGH.

---

### Usability and Accessibility Requirements

#### NFR-U-001: Internal-tooling accessibility

**Requirement**: Internal tooling used by consultants (CRM, time recording, knowledge library, ArcKit deployment) MUST be accessible to consultants with disabilities, meeting WCAG 2.2 AA where vendor-controlled and tested with assistive technology where vendor-controlled tooling claims conformance.

**Measurement Method**: Vendor accessibility statements; internal user feedback.

**Priority**: HIGH.

**Linked Principles**: Principle 12.

---

#### NFR-U-002: Public website accessibility

**Requirement**: WCAG 2.2 AA on the public practice website with published Accessibility Statement (linked to NFR-C-009 / FR-019).

**Measurement Method**: Automated and manual checks.

**Priority**: HIGH.

---

### Maintainability and Supportability Requirements

#### NFR-M-001: Operational runbooks

**Requirement**: Documented runbooks for: opportunity-to-engagement lifecycle, consultant onboarding / offboarding, QA gate, incident response, framework refresh, IdP outage, data subject access request, breach notification.

**Measurement Method**: Runbook register; quarterly tabletop / spot exercise.

**Priority**: HIGH.

---

#### NFR-M-002: Documentation currency

**Requirement**: Practice handbook, runbooks, and policies reviewed at least annually and on material change. Version-controlled in a single source of truth.

**Measurement Method**: Last-reviewed metadata audit.

**Priority**: HIGH.

---

#### NFR-M-003: Capability development

**Requirement**: Each consultant has ≥ 5% chargeable-equivalent time per quarter for capability development, including ArcKit toolkit currency, frameworks (TCoP, GDS Service Standard, NCSC CAF, MOD SbD where relevant), and sector context.

**Measurement Method**: Time-recording allocation reports.

**Priority**: HIGH.

---

### Portability and Interoperability Requirements

#### NFR-I-001: Open formats

**Requirement**: All client-bound deliverables produced in open formats — Markdown, OpenAPI, AsyncAPI, Mermaid, JSON, CSV — never in proprietary binary formats that lock the client into a specific vendor tool.

**Measurement Method**: Engagement-closure export audit.

**Priority**: CRITICAL.

**Linked Principles**: Principle 4, Principle 9.

---

#### NFR-I-002: Toolchain portability

**Requirement**: Practice tooling choices for client-engagement work MUST allow client takeover at engagement end without continuing dependence on any practice-controlled SaaS account or licence.

**Measurement Method**: Closure handover audit; client-takeover dry-run on representative engagement annually.

**Priority**: HIGH.

---

## Integration Requirements

### External System Integrations

#### INT-001: ArcKit as a Service (Project 001 — managed SaaS)

**Purpose**: Primary delivery platform for OFFICIAL-classification engagements.

**Integration Type**: Tenant of the SaaS; identity-federated; per-engagement workspaces.

**Data Exchanged**: Engagement workspace content (artefacts, audit logs).

**Authentication**: Federated SSO via the practice IdP; MFA required.

**SLA**: Aligned to Project 001 published SLAs.

**Owner**: ArcKit Product (Project 001).

**Priority**: CRITICAL.

---

#### INT-002: ArcKit Sovereign (Project 002)

**Purpose**: Delivery platform for OFFICIAL-SENSITIVE engagements on sensitive sites where the managed SaaS is not appropriate.

**Integration Type**: Customer-deployed instance per site; the practice deploys consultants to operate within the customer's accredited boundary.

**Authentication**: Per the deploying authority's accreditation (customer-controlled).

**SLA**: Per the customer's accreditation and contract.

**Owner**: ArcKit Product (Project 002); deploying authority.

**Priority**: CRITICAL (for OFFICIAL-SENSITIVE engagements).

---

#### INT-003: Companies House

**Purpose**: SME eligibility verification for the SME tier (FR-011); supplier diligence on associates / clients.

**Integration Type**: Companies House public data API.

**Authentication**: API key (free public API).

**Priority**: HIGH.

---

#### INT-004: Crown Commercial Service Digital Marketplace

**Purpose**: Framework listings (G-Cloud, DOS), call-off opportunities, MI submissions.

**Integration Type**: Web portal; manual operation; periodic API access where available.

**Authentication**: Supplier portal account.

**Priority**: CRITICAL.

---

#### INT-005: Accounting / invoicing system

**Purpose**: Invoice generation, debtor tracking, financial reporting (BR-004, FR-007).

**Integration Type**: SaaS accounting tool with HMRC Making Tax Digital integration.

**Authentication**: SSO via practice IdP.

**Priority**: CRITICAL.

---

#### INT-006: HMRC (Making Tax Digital, PAYE, VAT)

**Purpose**: Statutory tax filings (NFR-C-002).

**Integration Type**: Via accounting system MTD APIs.

**Authentication**: HMRC Government Gateway credentials.

**Priority**: CRITICAL.

---

#### INT-007: HR / payroll / pension provider

**Purpose**: Employment records, payroll, auto-enrolment pensions, leaver / joiner / mover events.

**Integration Type**: SaaS; integrated with IdP for joiner / leaver provisioning (FR-018).

**Authentication**: SSO; admin access restricted.

**Priority**: HIGH.

---

#### INT-008: Email and collaboration platform

**Purpose**: Day-to-day comms, calendaring, document collaboration internal-only and with clients.

**Integration Type**: SaaS; integrated with IdP and MDM.

**Authentication**: SSO; MFA enforced.

**Priority**: HIGH.

---

#### INT-009: Identity provider (IdP) / SSO and CRM / pipeline tool

**Purpose**: FR-018 (IdP) and FR-001 / FR-020 (CRM).

**Integration Type**: SaaS.

**Authentication**: Privileged-account-protected admin; SSO for end users.

**Priority**: CRITICAL (IdP), HIGH (CRM).

---

#### INT-010: Background-check / vetting partner

**Purpose**: BPSS and SC application sponsorship (BR-003, NFR-SEC-003).

**Integration Type**: Service relationship; manual referrals; secure document exchange.

**Priority**: HIGH.

---

#### INT-011: ICO

**Purpose**: Data-controller registration, breach notifications.

**Integration Type**: Web portal.

**Priority**: CRITICAL.

---

## Data Requirements

### Data Entities

#### Entity 1: Engagement

**Description**: A single client engagement instance (e.g., one SOW or call-off).

**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| engagement_id | UUID | Yes | Unique identifier | Primary key |
| client_id | UUID | Yes | Link to Client | Foreign key |
| classification | Enum | Yes | OFFICIAL / OFFICIAL-SENSITIVE | Default OFFICIAL; immutable post-creation |
| framework_ref | String | No | CCS framework reference | Where applicable |
| contract_ref | String | Yes | Internal contract reference | Indexed |
| start_date | Date | Yes | Engagement start | |
| end_date | Date | No | Engagement end (NULL = open) | |
| value | Money | Yes | Contract value (GBP) | |
| sme_tier | Boolean | Yes | Whether this is an SME-tier engagement | Default false |
| status | Enum | Yes | PROPOSED / ACTIVE / CLOSED / WARRANTY | |
| arckit_deployment | Enum | Yes | SAAS / SOVEREIGN | |
| created_at | Timestamp | Yes | Creation | Indexed |
| updated_at | Timestamp | Yes | Last update | Indexed |

**Relationships**:

- One-to-many with Engagement Allocation (consultants on engagement).
- One-to-many with Engagement Artefact (deliverables).
- Many-to-one with Client.
- One-to-many with QA Gate event.
- One-to-many with Time Entry.
- One-to-many with Invoice.

**Data Volume**: ≤ 50 active engagements steady-state (per NFR-S-001); historical records retained 6+ years.

**Data Classification**: Engagement metadata OFFICIAL; engagement content per engagement classification.

**Data Retention**: Engagement metadata 7 years post-closure; engagement content per contract (typically 6 years).

---

#### Entity 2: Client

**Description**: A buying organisation (gov body, ALB, NHS body, MOD body, SME).

**Attributes** (summary): client_id (UUID PK), legal_name, trading_name, companies_house_number (where applicable), classification_default, primary_contact_id, sector, sme_status (boolean, evidence reference).

**Data Classification**: OFFICIAL.

**Data Retention**: 7 years post-final-engagement-closure (financial records).

---

#### Entity 3: Consultant

**Description**: An employee or associate available for engagement allocation.

**Attributes** (summary): consultant_id (UUID PK), name, employment_type (employee / associate / sub-contractor), level, skills (JSON), clearance_status (BPSS / SC / DV), clearance_dates, current_engagements, capacity_pct, bench_status, contract_ref, ndas_signed (JSON), conflicts_declared (JSON).

**Data Classification**: OFFICIAL (HR / personnel data — special category not stored).

**Data Retention**: Per UK GDPR — 6 years post-employment / contract end for HR, longer where statutory.

---

#### Entity 4: Engagement Artefact

**Description**: A deliverable produced on an engagement.

**Attributes** (summary): artefact_id (UUID PK), engagement_id (FK), arckit_doc_id (e.g., ARC-NNN-XXX-vV.V), doc_type, classification, status (DRAFT / IN_REVIEW / APPROVED / DELIVERED), qa_log_ref, file_pointer (storage in chosen ArcKit deployment).

**Data Classification**: Per artefact (inherits engagement classification minimum).

**Data Retention**: Per contract.

---

#### Entity 5: Time Entry

**Description**: A unit of consultant time recorded against an engagement and activity code.

**Attributes** (summary): time_entry_id, consultant_id, engagement_id, activity_code, hours, date, status (DRAFT / SUBMITTED / APPROVED / INVOICED).

**Data Classification**: OFFICIAL.

**Data Retention**: 7 years (financial / HMRC).

---

#### Entity 6: Pipeline Opportunity

**Description**: A pre-contract sales opportunity.

**Attributes** (summary): opportunity_id, source, prospective_client, indicative_value, indicative_dates, probability, status (IDENTIFIED / QUALIFIED / BIDDING / WON / LOST / NO-BID), classification, conflict_check_status, sme_tier_eligible.

**Data Classification**: OFFICIAL.

**Data Retention**: 6 years post-decision (procurement audit).

---

#### Entity 7: Pattern / IP Library Item

**Description**: An anonymised, reusable engagement pattern.

**Attributes** (summary): pattern_id, source_engagement_ref, anonymisation_review_ref, capability_area, engagement_type, last_reviewed, supersedes (self-reference), open_source_release_ref (where applicable).

**Data Classification**: OFFICIAL (anonymised).

**Data Retention**: Indefinite while currency-reviewed.

---

#### Entity 8: Personal Data Inventory (Client Contacts and Consultants)

**Description**: Personal data held under UK GDPR.

**Attributes** (summary): subject_id, role_type (CONSULTANT / CLIENT_CONTACT / SUPPLIER_CONTACT), data_categories (ROPA-aligned), legal_basis, retention_until.

**Data Classification**: OFFICIAL with personal-data caveats.

**Data Retention**: Per ROPA.

---

### Data Quality Requirements

- **Accuracy**: Engagement metadata immutability for classification, contract reference, framework reference once set; changes require audit log.
- **Completeness**: Mandatory fields enforced at creation (classification, contract ref, allocated consultants).
- **Consistency**: ArcKit doc IDs follow `ARC-{PROJECT_ID}-{TYPE}-v{VERSION}` (`references/quality-checklist.md` Common Check 2).
- **Timeliness**: Time entries within 7 days of work date; pipeline updates within 1 working day of material change.
- **Lineage**: IP library items retain source-engagement reference and anonymisation review reference (FR-012).

### Data Migration Requirements

Initial state — no legacy data to migrate. Future migration in scope:

- If the practice is acquired or reorganised, engagement records and IP library MUST migrate via the open formats specified in NFR-I-001 / Principle 9 — no proprietary lock-in.

---

## Constraints and Assumptions

### Technical Constraints

- **TC-1**: All practice data hosted in the United Kingdom by default (Principle 7); cross-border processing only with explicit Client agreement and a documented Article 46 transfer mechanism.
- **TC-2**: Engagement delivery uses the ArcKit toolkit (Project 001 SaaS for OFFICIAL; Project 002 sovereign for sensitive sites) — no parallel proprietary EA tooling adopted as the primary medium.
- **TC-3**: Identity is centralised on a single IdP (FR-018); no per-tool local accounts for consultants except documented break-glass.
- **TC-4**: Open formats (NFR-I-001) are mandatory for client-bound deliverables.

### Business Constraints

- **BC-1**: SME-tier capacity reservation is a published commitment (BR-005, FR-011) — not negotiable down without external statement and Architecture Review Board approval.
- **BC-2**: Cross-subsidy to ArcKit-as-a-Service SME free tier — minimum 10% of post-tax net margin (BR-004) — is non-negotiable per Principle 1 alignment.
- **BC-3**: Day-rate floors apply (per BR-004 pricing-floor rule) and require Practice Lead exception to bid below.
- **BC-4**: No engagements that conflict with the integrity of the ArcKit product line (e.g., engagements seeking to deprive a public body of data portability) accepted.

### Assumptions

- **A-1**: ArcKit Project 001 (managed SaaS) reaches GA on or before this practice's GA, providing the primary engagement-delivery platform.
- **A-2**: ArcKit Project 002 (sovereign) is operable for sensitive-site engagements where required.
- **A-3**: Crown Commercial Service framework cycles continue at current pace (G-Cloud annually; DOS roughly biennially) and continue to admit small specialist suppliers.
- **A-4**: Public sector demand for ArcKit-style governance support persists at or above current observed levels (validated by SOBC).
- **A-5**: SC clearance pipelines for nominated consultants meet typical timelines (3–9 months); engagement allocation planning accommodates this.

**Validation Plan**: A-1 through A-5 validated as part of `/arckit:sobc` and `/arckit:risk` for project 003.

---

## Success Criteria and KPIs

### Business Success Metrics

| Metric | Baseline | Target | Timeline | Measurement Method |
|--------|----------|--------|----------|-------------------|
| Year-1 booked revenue | £0 | £750k–£1.5m (SOBC-validated) | End of Y1 | Accounting system |
| Net consulting margin | n/a | ≥ 20% | Steady-state from Q3 of Y1 | Accounting system |
| Cross-subsidy to ArcKit SaaS SME tier | £0 | ≥ 10% of post-tax net margin | Annual | Accounting / Principle 17 review |
| Concurrent engagements | 0 | 5 → 20 | GA → 18 months | Engagement records |
| SME-tier engagements delivered | 0 | ≥ 5 in Y1 | End of Y1 | Engagement records |
| Anonymised case studies published | 0 | ≥ 4 in Y1 | End of Y1 | Public website |
| Open-source contributions | 0 | ≥ 2 in Y1 | End of Y1 | Public repos |

### Technical / Operational Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Deliverables passing ArcKit quality checklist | 100% | QA gate logs |
| QA gate cycle time (median, standard deliverables) | ≤ 2 working days | QA log timestamps |
| Engagement closure latency | ≤ 5 working days | Engagement records |
| Cross-engagement data leakage incidents | 0 | Incident register |
| Cyber Essentials Plus certification | Continuous | Certification records |
| 72-hour breach-notification readiness | Tested annually | Tabletop reports |
| Pipeline-coverage ratio | ≥ 3.0 sustained | Pipeline reports |

### Client / Stakeholder Adoption Metrics

| Metric | Target | Timeline | Measurement Method |
|--------|--------|----------|-------------------|
| Client NPS (rolling 12-month, engagement-weighted) | ≥ +40 | Post-GA + 12 months | FR-009 |
| Client retention / repeat-engagement rate | ≥ 50% Y2+ | From Y2 onwards | Engagement records |
| Independent-assurance failures attributable to practice | 0 (rolling 12-month) | Continuous | Post-assurance reviews |
| Framework listings active | G-Cloud + DOS | Within 6 months of GA | CCS portal |

---

## Dependencies and Risks

> ⚠️ Risk register below is a *placeholder* derived from recognisable consulting-business risk patterns. Run `/arckit:risk` for project 003 to produce the formal Orange-Book aligned register.

### Dependencies

| Dependency | Description | Owner | Target Date | Status | Impact if Delayed |
|------------|-------------|-------|-------------|--------|-------------------|
| ArcKit Project 001 GA | Managed SaaS GA — primary delivery platform | ArcKit Product | TBD | At Risk | HIGH |
| ArcKit Project 002 GA | Sovereign deployment for sensitive engagements | ArcKit Product | TBD | At Risk | MEDIUM (SaaS-only Y1 if delayed) |
| G-Cloud / DOS framework cycle | Listing window for the next iteration | CCS | TBD | On Track | HIGH |
| Cyber Essentials Plus certification | Pre-bid baseline | External assessor | GA + 90 days | On Track | CRITICAL |
| Initial consultant cohort | BR-003 cohort live | Talent Lead | GA + 6 months | On Track | HIGH |

### Risks (placeholder)

| Risk ID | Description | Probability | Impact | Mitigation Strategy | Owner |
|---------|-------------|-------------|--------|---------------------|-------|
| R-1 | Pipeline concentration on a single client / framework | MEDIUM | HIGH | BR-009 concentration thresholds enforced; framework diversification | Commercial Lead |
| R-2 | Cross-engagement data leakage (process or system) | LOW | CRITICAL | FR-004 isolation; quarterly isolation tests; FR-017 incident response | DPO |
| R-3 | Departing consultant exfiltrates client material | LOW | HIGH | NFR-SEC-007 leaver controls; managed devices; remote wipe | DPO, Talent Lead |
| R-4 | SME-tier capacity diluted under commercial pressure | MEDIUM | HIGH | BC-1 published commitment; cross-subsidy pre-allocated | Practice Lead |
| R-5 | Quality failure on a high-profile assurance event | LOW | CRITICAL | FR-008 independent QA; NFR-Q-001 100% checklist pass; root-cause loop | QA Lead |
| R-6 | Framework non-compliance discovered in audit | LOW | HIGH | NFR-C-003 framework-compliance check quarterly; bid governance | Commercial Lead |
| R-7 | IR35 misclassification of associate engagements | MEDIUM | MEDIUM | FR-010 IR35 status determinations; HMRC CEST evidence | Talent Lead, Finance |
| R-8 | Project 001 / 002 GA delays force lower-grade tooling | MEDIUM | HIGH | Contingency tooling stance documented; transparent client communication | Practice Lead |
| R-9 | Day-rate compression from market dynamics | MEDIUM | MEDIUM | BR-004 pricing floor; outcome-based and retainer pricing options | Commercial Lead |
| R-10 | Brand damage from a publicised engagement failure | LOW | CRITICAL | FR-008 QA; FR-017 incident response; client-feedback NPS investigation trigger | Practice Lead |

---

## Requirement Conflicts & Resolutions

> Source: Conflicts derive from competing stakeholder drivers and from the dual nature of this practice — commercial sustainability vs the SME-affordability mission of Principle 1. STKE-003 (`/arckit:stakeholders`) will refine these.

### Conflict C-1: SME-tier affordability vs sustainable margin

**Conflicting Requirements**:

- **Requirement A**: BR-005 (run an SME-affordable engagement tier), with FR-011 published capacity reservation.
- **Requirement B**: BR-004 (≥ 20% net consulting margin sustained).

**Stakeholders Involved**:

- **Practice Lead / SRO**: Wants both (A) to honour Principle 1 and (B) to keep the practice solvent and able to fund the cross-subsidy.
- **Commercial Lead**: Wants (B) — pressure on margin from below-cost SME work makes commercial planning harder.
- **Client SMEs**: Want (A) — affordable access to consulting expertise.
- **Architecture Review Board**: Wants (A) honoured per Principle 1.

**Nature of Conflict**: Pure pro-bono SME work has zero or negative gross margin; if the SME tier consumes too much capacity it erodes the margin needed to keep funding the cross-subsidy, *eventually* destroying the SME tier itself.

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| Option 1: Hard-cap SME tier capacity (e.g., 5% chargeable capacity) and cross-subsidise from margin | Predictable; sustainable | Caps SME impact even when margin is high | Both partially satisfied |
| Option 2: SME pricing floor (capped day rate, not pro-bono) | Margin-positive even on SME engagements | Less affordable; some SMEs still excluded | Margin protected; mission diluted |
| Option 3: Pro-bono only when margin pool exceeds threshold (variable capacity) | Self-regulating; funded by surplus | Unpredictable SME availability; messaging hard | SME tier unreliable |
| Option 4: Hybrid — fixed SME capacity reservation + pricing-floor for additional SME demand | Predictable headline commitment + flex | More complex to administer | Both well satisfied |

**Resolution Strategy**: COMPROMISE (Hybrid).

**Decision**: **Option 4** — fixed SME capacity reservation per quarter (published, BC-1) backed by cross-subsidy (BC-2); additional SME demand met at a published SME pricing floor that remains margin-positive but visibly cheaper than the standard rate card.

**Rationale**: Honours Principle 1's "free-or-substantially-cheaper" wording — the reserved capacity is the "free / pro-bono" expression; the pricing floor is the "substantially-cheaper" expression. Sustainability protected because pro-bono is capacity-bounded.

**Decision Authority**: Practice Lead, with Architecture Review Board oversight on annual affordability review (Principle 1 validation gate).

**Impact on Requirements**:

- **Modified**: BR-005 success criterion clarified to require *both* a quarterly published capacity reservation *and* a published SME pricing floor.
- **Reinforced**: BR-004 cross-subsidy floor (≥ 10% net margin) is the funding for the reserved capacity.

**Stakeholder Management**:

- **Commercial Lead**: gets the pricing-floor floor and capacity discipline.
- **SMEs**: get a predictable, externally-published commitment plus an affordable paid path beyond the reservation.

---

### Conflict C-2: Speed of bid response vs proposal quality

**Conflicting Requirements**:

- **Requirement A**: NFR-P-001 — proposal turnaround ≤ 5 working days median.
- **Requirement B**: NFR-Q-001 — proposals (as deliverables) pass the ArcKit quality checklist before submission.

**Stakeholders Involved**:

- **Commercial Lead**: Wants (A) to maximise win rate.
- **QA Lead**: Wants (B) to protect brand and legal exposure (mis-stated capacity, scope, or compliance claims in a proposal damage downstream).

**Nature of Conflict**: Quality QA on every proposal extends turnaround; rapid turnaround risks errors entering proposals.

**Resolution Strategy**: INNOVATE — pre-built proposal templates and modular content blocks (FR-002), reviewed once and reusable, so per-bid effort is mostly customisation. QA gate applied to the per-bid customisation, not to the rebuilt-from-scratch document.

**Decision**: Adopt template-driven proposal generation with a lightweight QA review focused on: scope accuracy, conflict-of-interest, capacity assertion, and pricing alignment. Full QA only triggers if proposal departs from template patterns by more than a defined threshold.

**Decision Authority**: Practice Lead.

**Impact on Requirements**:

- **Reinforced**: FR-002 mandates customised proposal templates as a precondition for bidding velocity.

---

### Conflict C-3: Reuse of IP vs client confidentiality

**Conflicting Requirements**:

- **Requirement A**: BR-007 — capture and reuse engagement IP across engagements; publish openly.
- **Requirement B**: BR-008 — provable confidentiality; cross-engagement isolation.

**Stakeholders Involved**:

- **Practice Lead, QA Lead**: Want (A) — reuse compounds margin and contributes to public sector.
- **DPO, Clients**: Want (B) — confidentiality is non-negotiable.

**Resolution Strategy**: INNOVATE — separate the IP library from any engagement workspace (FR-012); mandate anonymisation review before any cross-engagement use; require client consent before any external publication; never permit copy-paste from a source engagement workspace into another.

**Decision**: All reuse flows through the anonymised pattern library only (FR-012, UC-4). Source engagement workspaces remain isolated (FR-004) with no cross-engagement read paths.

**Decision Authority**: DPO with Practice Lead.

**Impact on Requirements**:

- **Reinforced**: FR-004 (workspace isolation) and FR-012 (separated library).
- **Added**: FR-013 (case-study / open-source workflow) requires explicit client consent and DPO sign-off.

---

### Conflict C-4: Senior consultant utilisation vs delivery quality

**Conflicting Requirements**:

- **Requirement A**: NFR-S-002 — utilisation 65–80% (chargeable hours).
- **Requirement B**: NFR-Q-001 — 100% deliverable quality and NFR-M-003 — capability development time.

**Resolution Strategy**: COMPROMISE — utilisation target deliberately below 80% to reserve capacity for QA reviewing (FR-008), capability development (NFR-M-003), and bench cover (NFR-A-001).

**Decision**: 65–80% range stands. Anything > 80% sustained triggers a leadership review (NFR-S-002) — chronic over-utilisation degrades quality before it is visible in NPS.

---

### Conflict C-5: Open knowledge sharing vs competitive advantage

**Conflicting Requirements**:

- **Requirement A**: BR-007 — publish anonymised case studies and open-source contributions.
- **Requirement B**: Unstated implicit pressure to retain proprietary methods as competitive advantage.

**Stakeholders Involved**:

- **Practice Lead**: Wants (A) per Principle 16 and TCoP alignment.
- **Some commercial advisers**: Argue for (B).

**Resolution Strategy**: PRIORITIZE (A). Principle 16 (Open Source First and Reuse) is mandatory for the ArcKit ecosystem; competitive advantage is built on **delivery quality and brand**, not on hoarded patterns. Hoarded EA patterns generally have low half-life.

**Decision**: Publish per BR-007 schedule. Confidentiality of *client* material is non-negotiable; *method* publication is non-negotiable in the other direction.

**Decision Authority**: Architecture Review Board.

---

## Timeline and Milestones

### High-Level Milestones

| Milestone | Description | Target Date | Dependencies |
|-----------|-------------|-------------|--------------|
| Requirements Approval | Stakeholder sign-off on this document | 2026-06-30 | This document, STKE-003, SOBC-003 |
| Practice incorporation and registrations | UK ltd; ICO; HMRC; insurance | 2026-07-31 | BR-001 |
| Cyber Essentials Plus | Pre-bid baseline | 2026-09-30 | BR-001, NFR-C-005 |
| Initial consultant cohort live | BR-003 cohort onboarded | 2026-10-31 | BR-003, FR-006 |
| First framework listing live | G-Cloud listing | 2026-11-30 | BR-002 |
| GA — first paid engagement begun | First commercial delivery | 2026-12-15 | All MUST_HAVE FRs and NFRs |
| First SME-tier engagement closed | BR-005 evidence | 2027-03-31 | FR-011 |
| First anonymised case study published | BR-007 evidence | 2027-06-30 | FR-013, FR-014 |
| Year-1 review (Principle 1 affordability) | Annual affordability and cross-subsidy review | 2027-12-15 | All Y1 metrics |

> Dates indicative; finalised in `/arckit:plan` for project 003.

---

## Budget

> ⚠️ Indicative ranges only. Authoritative figures to come from `/arckit:sobc` for project 003. Figures here exist to scope the order of magnitude.

### Initial Setup Cost (one-off)

| Category | Estimated Cost (GBP) | Notes |
|----------|----------------|-------|
| Legal / incorporation / contracts | £8k – £15k | Setup, contract templates, NDA / IR35 templates |
| Insurance (year 1) | £5k – £15k | PI, PL, EL, cyber |
| Cyber Essentials Plus (year 1) | £3k – £6k | External assessor |
| Tooling setup (IdP, MDM, accounting, CRM, time recording) | £10k – £25k | Configuration; subscriptions in ongoing |
| Framework listing application effort | £5k – £15k | Internal time; legal review of clauses |
| Website + accessibility evidence | £10k – £20k | Build + audit |
| Initial brand / sales collateral | £5k – £15k | Plus per-engagement customisation |
| **Total setup** | **£46k – £111k** | |

### Ongoing Annual Cost

| Category | Estimated Annual Cost (GBP) | Notes |
|----------|---------------------------------|-------|
| Tooling subscriptions (IdP, MDM, accounting, CRM, etc.) | £15k – £40k | |
| Insurance (renewal) | £8k – £25k | Scales with engagement portfolio |
| Cyber Essentials Plus (renewal) + pen test | £6k – £20k | |
| Framework listing maintenance | £5k – £10k | |
| Capability development (NFR-M-003) | 5% of consultant cost | Embedded in consultant cost |
| Practice management (Lead, Commercial, QA, DPO time) | Variable | Embedded in consultant cost |
| **Indicative ongoing (excl consultants)** | **£34k – £95k** | Plus consultant cost |

---

## Approval

### Requirements Review

| Reviewer | Role | Status | Date | Comments |
|----------|------|--------|------|----------|
| [PENDING] | Practice Lead / SRO | [ ] Approved | [PENDING] | |
| [PENDING] | Commercial Lead | [ ] Approved | [PENDING] | |
| [PENDING] | QA Lead | [ ] Approved | [PENDING] | |
| [PENDING] | DPO / IG Lead | [ ] Approved | [PENDING] | |
| [PENDING] | Architecture Review Board | [ ] Approved | [PENDING] | Cross-project alignment with Projects 001, 002 |

### Sign-Off

By signing below, stakeholders confirm that requirements are complete, understood, and approved to proceed to design / operating-model phase.

| Stakeholder | Signature | Date |
|-------------|-----------|------|
| Mark Craddock, Practice Lead | _________ | [PENDING] |
| [PENDING], DPO | _________ | [PENDING] |

---

## Appendices

### Appendix A: Glossary

- **ArcKit**: the enterprise architecture governance toolkit and the family of projects in this repository.
- **ArcKit Consulting**: the professional-services arm — the subject of this document (Project 003).
- **ArcKit as a Service / SaaS**: the managed, multi-tenant ArcKit product (Project 001).
- **ArcKit Sovereign**: the air-gapped / on-premise ArcKit deployment for sensitive sites (Project 002).
- **BPSS**: HMG Baseline Personnel Security Standard.
- **CCS**: Crown Commercial Service.
- **CDDO**: Central Digital and Data Office.
- **DOS**: Digital Outcomes and Specialists framework.
- **DPO**: Data Protection Officer.
- **DSIT**: Department for Science, Innovation and Technology.
- **Framework call-off**: a procurement of services under an existing framework agreement.
- **GDS**: Government Digital Service.
- **G-Cloud**: Crown Commercial Service Cloud framework.
- **Independent assurance**: review of deliverables by a body external to the engagement (e.g., GDS Service Assessment, NCSC, internal audit).
- **MCF**: Management Consultancy Framework (CCS).
- **MOD SbD**: MOD Secure by Design.
- **MOD**: Ministry of Defence.
- **NCSC**: National Cyber Security Centre.
- **NCSC CAF**: NCSC Cyber Assessment Framework.
- **NPS**: Net Promoter Score.
- **OFFICIAL / OFFICIAL-SENSITIVE**: HMG Government Security Classification levels.
- **PI / PL / EL**: Professional Indemnity / Public Liability / Employer's Liability insurance.
- **PPN**: Procurement Policy Note.
- **PSBAR 2018**: Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018.
- **SC**: Security Check (HMG personnel security clearance).
- **SME**: Small and Medium Enterprise (Companies Act 2006 thresholds).
- **SOW**: Statement of Work.
- **TCoP**: Technology Code of Practice.

### Appendix B: Reference Documents

- ArcKit Architecture Principles — `projects/000-global/ARC-000-PRIN-v2.0.md` (Principles 1, 4, 5, 7, 8, 9, 12, 16, 17 most directly relevant to this practice).
- ArcKit Project 001 Requirements — `projects/001-arckit-saas/ARC-001-REQ-v1.0.md` (managed SaaS that this practice deploys for OFFICIAL engagements).
- ArcKit Project 002 Requirements — `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md` (sovereign deployment for sensitive engagements).
- UK Government policies referenced (cited by name, no documents placed in `external/`):
  - Procurement Act 2023; PPN 03/23 (prompt payment); PPN 06/21 (cyber); PPN 09/14 / PPN 09/23 (cyber baselines); PPN 09/22 (modern slavery).
  - Technology Code of Practice; GDS Service Standard; CDDO Cloud Strategy.
  - NCSC CAF; NCSC Cloud Security Principles; Cyber Essentials Plus.
  - UK GDPR; Data Protection Act 2018; PSBAR 2018; WCAG 2.2 AA.
  - Modern Slavery Act 2015; Bribery Act 2010; Equality Act 2010.
  - HMG Government Security Classifications Policy; HMG Baseline Personnel Security Standard.
  - Companies Act 2006 (SME thresholds).

### Appendix C: Linked Architecture Principles (`ARC-000-PRIN-v2.0.md`)

| Requirement | Linked Principle(s) |
|-------------|---------------------|
| BR-005, FR-011, BC-1, BC-2 | Principle 1 (Equitable Access for SMEs), Principle 17 (Cost Transparency / FinOps) |
| BR-006, NFR-Q-001, NFR-I-001 | Principle 4 (Open Standards), Principle 9 (Data Quality, Lineage, Portability), Principle 15 (Maintainability and Evolvability) |
| BR-008, FR-004, FR-015, FR-017, NFR-SEC-001 to 007 | Principle 5 (Security by Design), Principle 7 (UK Sovereignty), Principle 8 (Tenant Isolation) |
| BR-007, FR-012, FR-013 | Principle 4 (Open Standards), Principle 16 (Open Source First and Reuse) |
| FR-019, NFR-C-009, NFR-U-001 / U-002 | Principle 12 (Accessibility — non-negotiable) |
| NFR-A-001, A-002, A-003 | Principle 14 (Availability and Reliability) |
| BR-010 | Principle 16 (reuse), Principle 9 (lineage) |

### Appendix D: Out-of-Scope Topics Pointing to Future Artefacts

- Detailed operating model: future `/arckit:operationalize` for project 003.
- ADRs for commercial model, framework prioritisation, and tooling selection: future `/arckit:adr` calls for project 003.
- Risk register: `/arckit:risk` for project 003 (replaces the placeholder above).
- Stakeholder analysis: `/arckit:stakeholders` for project 003 (replaces the placeholder above).
- SOBC: `/arckit:sobc` for project 003.

---

## External References

> No external policy documents were placed in `projects/003-arckit-consulting/external/` at the time of generation. Public-domain UK Government and CCS policies referenced in the body (TCoP, GDS Service Standard, CCS frameworks, NCSC CAF, Procurement Act 2023, PPNs, UK GDPR, PSBAR 2018, Modern Slavery Act 2015, Bribery Act 2010, Equality Act 2010, HMG Classifications Policy, BPSS, Companies Act 2006) are cited by name. Place authoritative copies in `projects/003-arckit-consulting/external/` and re-run `/arckit:requirements` to embed inline citations.

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

**Generated by**: ArcKit `/arckit:requirements` command
**Generated on**: 2026-05-07
**ArcKit Version**: 4.19.0
**Project**: ArcKit Consulting (Project 003)
**AI Model**: claude-opus-4-7[1m]
**Generation Context**: Generated using the `/arckit:requirements` command with the user input "003 ArcKitConsulting a consulting arm that uses arckit to delivery projects within the UK Public Sector". Anchored on architecture principles `ARC-000-PRIN-v2.0.md`, with cross-references to the managed-SaaS requirements (`projects/001-arckit-saas/ARC-001-REQ-v1.0.md`) and an awareness of the sovereign project (Project 002). STKE-003, SOBC-003, and RISK-003 do not yet exist; placeholders flagged in-document with explicit calls to run `/arckit:stakeholders`, `/arckit:sobc`, and `/arckit:risk` for project 003 to refine.
