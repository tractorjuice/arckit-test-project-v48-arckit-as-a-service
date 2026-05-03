# Project Requirements: ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-REQ-v1.0 |
| **Document Type** | Business and Technical Requirements |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Date** | 2026-06-02 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, MOD Defence Digital liaison, NCSC liaison, GDS, CDDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:requirements` command, scoped to the sovereign / air-gapped deployment route per Principle 21 (`ARC-000-PRIN-v2.0.md`). Sister to project 001 (managed SaaS) | [PENDING] | [PENDING] |

## Document Purpose

Defines the business and technical requirements for the **sovereign / on-premise / air-gapped deployment** route of ArcKit as a Service, supporting UK Ministry of Defence and other sensitive sites. This document is the source of truth for downstream design, vendor selection, packaging, accreditation support, and operations specific to the sovereign route. The managed multi-tenant SaaS route is specified in `projects/001-arckit-saas/ARC-001-REQ-v1.0.md`.

> **Source steer (user input, 2026-05-03)**: *"soverign"* — interpreted as: create requirements for the sovereign deployment route deferred from project 001.

> **Architectural anchor**: Principle 21 (Sovereign and Air-Gapped Deployment) in `ARC-000-PRIN-v2.0.md` mandates that the sovereign route MUST share the same source code, data formats, and APIs as the managed SaaS, MUST be installable, operable, updatable, and uninstallable without any reliance on vendor-controlled services or outbound network connectivity, and MUST evidence MOD Secure by Design / JSP 440 alignment for MOD deployments.

> **Upstream artefact gaps**:
>
> - **Stakeholder Analysis (STKE) for project 002** — not yet created. Sovereign-specific stakeholders below are placeholders derived from Principle 21 and from the project-001 stakeholder analysis (where relevant). MUST be validated by running `/arckit:stakeholders` for project 002.
> - **Strategic Outline Business Case (SOBC) for project 002** — not yet created. Sovereign commercial model figures are indicative and MUST be validated by `/arckit:sobc`.
> - **Risk Register (RISK) for project 002** — not yet created. Risks below are derived; formal register MUST be created with `/arckit:risk`.
> - **MOD Secure by Design assessment** — to be created with `/arckit:mod-secure` when a representative deploying authority is engaged.

---

## Executive Summary

### Business Context

A material portion of the UK public-sector audience for the ArcKit governance toolkit — including the Ministry of Defence, intelligence community partners, and accredited operators of essential services — cannot lawfully or operationally use a public managed SaaS for some or all of their work. Their networks operate at OFFICIAL-SENSITIVE and above, often inside accredited boundaries with no internet egress. If ArcKit is only available as a SaaS, those users either cannot adopt it at all or adopt fragmented alternatives, undermining the consistency that the platform exists to deliver.

The sovereign deployment route addresses that audience. The same codebase that powers the managed SaaS (project 001) is packaged into a signed, air-gap-transferable release bundle that customer operators install, run, upgrade, back up, and decommission entirely within their accredited boundary. The vendor commercial model for sovereign deployments is separate from the SME-affordability commitment that governs the managed SaaS — sovereign customers pay full cost-to-serve plus margin, and that margin contributes to the cross-subsidy that funds the SME tier in project 001.

### Objectives

- Deploy ArcKit into UK MOD and comparable sensitive-site environments fully disconnected from vendor-controlled services, with formal accreditation evidence.
- Share a single source-of-truth codebase between SaaS and sovereign deployments — no fork, no feature-drift.
- Provide all governance-critical functionality from the SaaS in the sovereign deployment, with pluggable AI / model endpoints honoured.
- Issue signed, hashed release bundles with full SBOM, release notes, and offline operator runbooks on each release.
- Support customer-led accreditation against MOD Secure by Design / JSP 440 / JSP 604 / NCSC CAF.

### Expected Outcomes

- ≥ 1 successful sovereign deployment in production at an MOD or comparable sensitive-site customer within 18 months of GA.
- Disconnected install / upgrade / backup / restore validated end-to-end in CI on every release before bundle issue.
- 100% of governance-critical features parity with managed SaaS.
- Sovereign-deployment unit economics positive and contributing margin to the SME tier (links to project 001 BR-005 / Goal G-3).
- Long-term support release line documented and honoured (sovereign customers may stay on a pinned LTS release independently of the SaaS release cadence).

### Project Scope

**In Scope**:

- Single-codebase sovereign deployment route shared with the managed SaaS.
- Air-gap-transferable, signed release bundle with SBOM and operator runbooks.
- Disconnected installation, operation, upgrade (forward + roll-back), backup, restore, key rotation, and decommission within a customer-controlled accredited boundary.
- Pluggable AI / model endpoint integration (default sovereign profile points at no external provider).
- Configurable telemetry destination, time source, certificate authority, package mirror, and identity provider.
- Operator runbooks, support model, and remote-support arrangements respecting the customer's accreditation.
- Long-term support release line decoupled from the SaaS release cadence.
- MOD Secure by Design / JSP 440 / JSP 604 evidence per release; NCSC CAF mapping for non-MOD sensitive sites.
- Within-deployment isolation between projects, roles, and communities of interest.

**Out of Scope**:

- The managed multi-tenant SaaS (covered by project 001).
- Multi-tenant SaaS commercial model (free tier, SME pricing, G-Cloud-only listing).
- Companies House SME verification (irrelevant in sovereign mode).
- Public payment processing (sovereign customers pay through standard government / defence procurement contracts).
- Vendor-hosted observability / status-page exposure of sovereign-customer telemetry.
- Native mobile apps in v1.
- Languages other than English in v1.
- Top-level platform changes that would require a SaaS / sovereign codebase fork.

---

## Stakeholders

> ⚠️ Placeholder set for project 002 — to be validated and refined by `/arckit:stakeholders` for this project.

| Stakeholder | Role | Organization | Involvement Level |
|-------------|------|--------------|-------------------|
| Mark Craddock | Service Owner / Sponsor | ArcKit as a Service | Decision maker |
| [PENDING] | Lead Architect | ArcKit as a Service | Technical oversight; sovereign packaging design |
| [PENDING] | Security Lead / SIRO-equivalent | ArcKit as a Service | MOD SbD / JSP 440 mapping; supply chain |
| [PENDING] | Product Manager (sovereign track) | ArcKit as a Service | LTS release line; customer engagement |
| [PENDING] | Sovereign Delivery Lead | ArcKit as a Service | Customer onboarding; on-site support liaison |
| [PENDING] | DPO | ArcKit as a Service | UK GDPR for sovereign data handling at vendor side |
| MOD Customer SRO | Senior Responsible Owner | Customer (deploying authority) | Accountable for customer-side deployment |
| MOD Customer Accreditor | Accreditor / Authorising Engineer | Customer (deploying authority) | Issues authorisation to operate (per JSP 604) |
| MOD Customer SIRO | Senior Information Risk Owner | Customer (deploying authority) | Information risk acceptance |
| Customer Operator Team | Platform / SRE team | Customer (deploying authority) | Day-to-day operation within boundary |
| MOD Defence Digital | Digital function | UK MOD | Cross-MOD digital oversight |
| NCSC | Standards setter | NCSC | CAF / Cloud Security / supply chain guidance |
| Crown Commercial Service | Procurement | UK Cabinet Office | Framework procurement route (G-Cloud / DOS / DPS) |
| HM Treasury | Spend control | HMG | Value for money |

---

## Business Requirements

### BR-001: Single-Codebase Sovereign Deployment

**Description**: The sovereign deployment MUST share the same source code, data formats, APIs, and feature set as the managed SaaS. No proprietary fork, no permanent feature gating between SaaS and sovereign.

**Rationale**: Principle 21 mandates this. A fork would erode interoperability, double engineering cost, and ultimately fail at one of the two routes. Single codebase preserves the open-standards commitment and makes sovereign customers' exit path credible.

**Success Criteria**:

- All ArcKit artefact types available in sovereign mode that are available in SaaS mode.
- Same artefact byte-for-byte equivalent across modes for the same content.
- Single Git repository serves both modes; release pipeline produces SaaS deployment and sovereign bundle from one revision.
- Any feature flag that distinguishes SaaS and sovereign behaviour is documented and reviewed quarterly.

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner, Lead Architect
**Traces To**: Principle 21, Principle 4, project-001 SD-9.

---

### BR-002: Air-Gap and Disconnected Operation

**Description**: The sovereign deployment MUST be installable, operable, updatable, and uninstallable without any outbound internet connectivity from inside the customer's accredited boundary.

**Rationale**: MOD and comparable sensitive sites operate inside accredited boundaries with no internet egress. Any phone-home or internet-dependency makes the platform non-deployable.

**Success Criteria**:

- Bundle install validated in a representative isolated environment with no internet egress.
- Network-deny test in CI: zero outbound connections during install, run, upgrade, backup, restore, decommission.
- All required dependencies are vendorable: package mirror, time source, certificate authority, AI endpoint, telemetry destination — each configurable to a customer-controlled endpoint.

**Priority**: MUST_HAVE
**Stakeholder**: Customer Operator Team, Lead Architect
**Traces To**: Principle 21.

---

### BR-003: Customer-Controlled Deployment

**Description**: The sovereign deployment MUST be installable, operable, and decommissionable by the customer's own operator team — without any vendor remote access except via mechanisms permitted by the customer's accreditation.

**Rationale**: Sovereign customers will not accept vendor-administered systems inside their boundary. Vendor remote support must be opt-in and accreditation-compliant.

**Success Criteria**:

- Operator runbook covers install / upgrade / backup / restore / key rotation / decommission, executable end-to-end by trained operator team without vendor presence.
- Vendor remote support model documented; default is no remote access.
- Customer can verify, audit, and disable any optional remote support mechanism.

**Priority**: MUST_HAVE
**Stakeholder**: Customer Operator Team, MOD Customer SIRO
**Traces To**: Principle 21, Principle 5.

---

### BR-004: Formal Accreditation Support

**Description**: Each sovereign release MUST be accompanied by an evidence pack supporting customer-led accreditation against the customer's applicable framework (MOD Secure by Design / JSP 440 / JSP 604 for MOD; NCSC CAF / GovAssure for OES; departmental SbD for civilian sensitive sites).

**Rationale**: Accreditation is the gating activity for sovereign deployment. Vendor evidence that does not map to the customer's framework forces the customer to reverse-translate at their cost; many will simply choose another supplier.

**Success Criteria**:

- MOD SbD evidence pack provided per release (`/arckit:mod-secure`).
- NCSC CAF mapping provided per release.
- SBOM (CycloneDX or SPDX), signed manifests, hash inventory, release notes, and threat model included in the bundle.
- Customer-side template for the Security Aspects Letter (SAL) provided.

**Priority**: MUST_HAVE
**Stakeholder**: MOD Customer Accreditor, MOD Customer SIRO, vendor Security Lead
**Traces To**: Principle 5, Principle 21.

---

### BR-005: Long-Term Support Release Line

**Description**: A documented Long-Term Support (LTS) release line MUST be maintained, decoupled from the SaaS release cadence, with security patches issued for at least 24 months from each LTS release.

**Rationale**: Sovereign customers cannot upgrade as often as a SaaS — accreditation re-runs are expensive. LTS gives them predictability and patching without a forced upgrade cadence.

**Success Criteria**:

- Documented LTS release schedule (typically annual major LTS line).
- Each LTS line supported with security patches for ≥ 24 months from issue.
- Patch backports tested in CI against the disconnected profile.
- Notice of LTS deprecation given ≥ 12 months in advance.

**Priority**: MUST_HAVE
**Stakeholder**: Customer Operator Team, MOD Customer Accreditor, vendor Product Manager
**Traces To**: Principle 21.

---

### BR-006: Sovereign Commercial Model Funds Cross-Subsidy

**Description**: Sovereign deployment licences MUST recover full cost-to-serve plus a margin that contributes to the cross-subsidy funding the SaaS SME tier (project 001 BR-005).

**Rationale**: Sovereign customers are paying-customers by virtue of size, sector, and accreditation cost; pricing them at SME-tier rates would breach Principle 17 and undermine the SME-affordability mission.

**Success Criteria**:

- Documented sovereign pricing covering engineering, support, accreditation effort, and contribution margin.
- Quarterly affordability review (project 001 BR-005) demonstrates sovereign contribution to the SME tier.
- No sovereign deal priced below documented cost-to-serve floor without explicit Service Owner approval.

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner, Finance
**Traces To**: Principle 17, project 001 BR-005.

---

### BR-007: Defence and Sensitive-Site Procurement Routes

**Description**: The sovereign offering MUST be available through procurement routes used by MOD and sensitive-site customers, including G-Cloud, Digital Outcomes and Specialists (DOS), and any applicable defence-specific frameworks.

**Rationale**: These customers do not contract bespoke; they call off framework agreements.

**Success Criteria**:

- G-Cloud and DOS listings covering sovereign deployment and the supporting professional services.
- Engagement plan with applicable MOD framework owners.
- Compliance with the Defence Cyber Protection Partnership Cyber Risk Profile relevant to the engagement.

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner, CCS liaison
**Traces To**: project 001 BR-004 (related procurement experience).

---

### BR-008: Reference Customer in MOD or Comparable Site

**Description**: Achieve a successful production sovereign deployment at an MOD or comparable sensitive-site customer within 18 months of GA, with the customer willing to act as a reference.

**Rationale**: A reference customer collapses the trust gap for subsequent customers.

**Success Criteria**:

- ≥ 1 production sovereign deployment with positive accreditation outcome by GA + 18 months.
- Reference case study published (subject to customer consent).

**Priority**: SHOULD_HAVE
**Stakeholder**: Service Owner
**Traces To**: BR-004.

---

## Functional Requirements

### User Personas

#### Persona 1: Customer Operator (Cleared Personnel)

- **Role**: Platform / SRE / cyber-defence team at an MOD unit, ALB, or sensitive-site customer.
- **Goals**: Install ArcKit, keep it running, patch it on schedule, operate within the accredited boundary, and decommission cleanly.
- **Pain Points**: Vendor systems that "just work" when on the internet but break in air-gap; opaque dependencies; phone-home defaults.
- **Technical Proficiency**: High.
- **Clearance**: Typically SC or DV depending on site.

#### Persona 2: Customer Accreditor / Authorising Engineer

- **Role**: Information assurance role at the deploying authority responsible for issuing or recommending the authorisation to operate.
- **Goals**: Confirm the system meets MOD SbD / JSP 440 / JSP 604 / NCSC CAF as applicable; sign off the SAL; manage residual risk.
- **Pain Points**: Vendor evidence that does not map to the customer's framework; missing or unsigned SBOMs; unclear cryptographic provenance.

#### Persona 3: Customer SIRO

- **Role**: Senior Information Risk Owner at the deploying authority.
- **Goals**: Information risk register accurately reflects the platform; risk acceptance defensible at audit.
- **Pain Points**: Surprises during accreditation that escalate to SIRO late.

#### Persona 4: Customer Architect (DDaT — same as project 001 personas)

- **Role**: Enterprise / Solution / Security Architect at the deploying authority — same DDaT roles as project 001 SD-1 to SD-5.
- **Goals**: Use ArcKit to author and review their own architecture artefacts inside the boundary.
- **Pain Points**: Tooling that imposes external dependencies in environments that forbid them.

#### Persona 5: Vendor Sovereign Delivery Lead

- **Role**: Vendor-side liaison for sovereign customer onboarding and support.
- **Goals**: Smooth installs; predictable LTS; minimise vendor-side custodianship of customer data.
- **Pain Points**: Vendor-imposed escalation paths that breach customer accreditation.

---

### Use Cases

#### UC-1: Sovereign Deployment Install (Air-Gapped)

**Actor**: Customer Operator Team.
**Preconditions**: Customer environment provisioned within accredited boundary; release bundle transferred via approved data-transfer mechanism; customer-controlled endpoints (time, CA, package mirror, telemetry, identity provider, AI) provisioned and reachable inside the boundary.
**Main Flow**:

1. Operator verifies bundle signature and hash against an out-of-band signature manifest.
2. Operator extracts the bundle to the install host.
3. Operator runs the install runbook against the configuration profile, providing endpoints for time, CA, package mirror, identity provider, and (if used) AI endpoint.
4. System validates configuration; refuses to start if any required customer-controlled endpoint is missing.
5. System completes install; emits structured logs to customer-controlled telemetry endpoint.
6. Operator runs the post-install verification suite within the boundary; suite passes with no outbound network attempts.

**Postconditions**: ArcKit running inside the boundary; no outbound connectivity attempted.
**Alternative Flows**:

- **Alt 1a**: Bundle signature invalid — install refuses to start; operator returns to data-transfer mechanism for re-acquisition.

**Exception Flows**:

- **Ex 1**: Customer-controlled endpoint unreachable during install — install fails fast with explicit message; no partial state persisted.

**Business Rules**: No outbound connectivity attempts during any install phase; all dependencies vendored in the bundle.
**Priority**: CRITICAL.

---

#### UC-2: Sovereign Upgrade Including Roll-Back

**Actor**: Customer Operator Team.
**Preconditions**: Existing sovereign deployment; new release bundle transferred and signature verified.
**Main Flow**:

1. Operator runs upgrade dry-run against a non-production environment within the boundary.
2. Operator schedules the upgrade window; backs up current state.
3. Operator applies upgrade following the runbook.
4. System runs post-upgrade self-tests; reports pass / fail.
5. If pass, operator decommissions the previous version.
6. If fail, operator initiates roll-back from backup.

**Postconditions**: Either the new version running and the prior version decommissioned, or the prior version restored; in both cases the state is consistent and accreditation evidence updated.
**Priority**: CRITICAL.

---

#### UC-3: Sovereign Decommission and Data Destruction

**Actor**: Customer Operator Team.
**Preconditions**: Customer has decided to decommission the deployment.
**Main Flow**:

1. Operator initiates decommission per runbook.
2. System exports residual artefacts to a customer-controlled archive in open formats.
3. System deletes data from primary stores and from backups within the configured retention window.
4. Operator generates and retains the destruction certificate.

**Postconditions**: All ArcKit data removed from customer infrastructure; destruction evidence retained for audit.
**Priority**: CRITICAL.

---

### Functional Requirements Detail

#### FR-001: Air-Gap Install From Signed Release Bundle

**Description**: System MUST install end-to-end from a signed, hashed release bundle without any outbound network connectivity.

**Relates To**: BR-001, BR-002, BR-003, UC-1.

**Acceptance Criteria**:

- [ ] Given a valid bundle and a representative isolated environment, when the operator runs install, then install completes within documented duration with no outbound network attempts.
- [ ] Given an invalid signature or hash, when the operator runs install, then install refuses to start.
- [ ] Given a missing customer-controlled endpoint, when the operator runs install, then install fails fast with a clear message and no partial state.

**Priority**: MUST_HAVE
**Complexity**: HIGH

---

#### FR-002: Air-Gap Upgrade With Forward and Roll-Back Paths

**Description**: System MUST support upgrade and roll-back without outbound network connectivity, with state preservation across upgrades.

**Relates To**: BR-001, BR-002, UC-2.

**Acceptance Criteria**:

- [ ] Given a previous-version deployment, when the upgrade runbook is followed, then the new version is operational within documented duration and prior-version data is preserved.
- [ ] Given a failed upgrade, when the roll-back runbook is followed, then the prior version is restored from backup with no data loss beyond the documented RPO.

**Priority**: MUST_HAVE
**Complexity**: HIGH

---

#### FR-003: Air-Gap Backup, Restore, and Key Rotation

**Description**: System MUST support backup, restore, and key rotation procedures within the accredited boundary, with no vendor involvement and no outbound calls.

**Relates To**: BR-002, BR-003.

**Acceptance Criteria**:

- [ ] Backup runs to a customer-controlled storage target within the boundary.
- [ ] Restore reproduces the deployment state to a verifiable known-good point.
- [ ] Key rotation procedure documented and tested per release.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-004: Pluggable AI / Model Endpoint

**Description**: System MUST treat the AI / model endpoint as pluggable; the default sovereign profile MUST point at no external provider; configuration MUST allow the customer to point at a customer-controlled approved model deployment, or to disable AI generation entirely.

**Relates To**: BR-001, BR-002, project 001 INT-005, Conflict C-2 in `ARC-001-REQ-v1.0.md`.

**Acceptance Criteria**:

- [ ] Default sovereign install does not invoke any external AI service.
- [ ] Configuration profile permits a customer-controlled endpoint conforming to the documented contract.
- [ ] Configuration profile permits disabling AI generation entirely; manual authoring remains fully functional.
- [ ] No tenant content is transmitted to any AI endpoint other than the configured customer-controlled one.

**Priority**: MUST_HAVE
**Complexity**: HIGH

---

#### FR-005: Configurable Telemetry, Time, CA, Package Mirror, Identity Provider

**Description**: System MUST expose configuration for telemetry destination, time source, certificate authority, package mirror, and identity provider, all defaulting to no external endpoints in sovereign mode.

**Relates To**: BR-002, BR-003.

**Acceptance Criteria**:

- [ ] Each integration has a documented configuration contract.
- [ ] Default configuration profile in sovereign mode sets all of these to placeholder customer-controlled endpoints; system refuses to start until they are filled.
- [ ] System operates correctly with all five integrations on customer-controlled endpoints inside the boundary.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-006: Within-Deployment Isolation (Single-Tenant Mode)

**Description**: In sovereign single-tenant mode, the system MUST enforce isolation between projects, roles, and communities of interest within the customer's user base, with default-deny authorisation.

**Relates To**: BR-001, Principle 8, project 001 NFR-SEC-002.

**Acceptance Criteria**:

- [ ] Project-level access rules configurable by customer admins.
- [ ] Community-of-interest separation supported (e.g., labels and visibility scopes).
- [ ] Automated isolation tests in CI cover within-deployment scenarios.

**Priority**: MUST_HAVE
**Complexity**: HIGH

---

#### FR-007: Customer-Controlled Identity and Cleared-Personnel Authentication

**Description**: System MUST authenticate users via the customer's identity provider using standard protocols (OIDC, OAuth 2.x, SAML 2.0). Where the customer's accreditation requires cleared-personnel-only access, the system MUST honour that constraint via identity claims.

**Relates To**: BR-002, BR-004, Principle 5.

**Acceptance Criteria**:

- [ ] System integrates with customer IdP via standard protocols.
- [ ] Group / role claims drive authorisation.
- [ ] System refuses access if required claims (e.g., clearance attribute as defined by customer) are absent.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-008: Same Artefact Authoring as SaaS

**Description**: System MUST support authoring of the same ArcKit artefact types as the managed SaaS (principles, requirements, ADRs, diagrams, traceability, glossary, all assessment types).

**Relates To**: BR-001.

**Acceptance Criteria**:

- [ ] Sovereign-mode artefact set is byte-for-byte equivalent to SaaS-mode for the same content.
- [ ] Document IDs follow `ARC-{PROJECT_ID}-{TYPE}-v{VERSION}` convention identically.

**Priority**: MUST_HAVE
**Complexity**: LOW (existing capability)

---

#### FR-009: Tenant Data Export and Portability

**Description**: System MUST support full export of all artefacts and lineage metadata in open formats by customer admins at any time.

**Relates To**: BR-001, Principle 4, Principle 9, UC-3.

**Acceptance Criteria**:

- [ ] One-command export by customer admin produces an open-format archive within documented duration.
- [ ] Export contains 100% of customer artefacts and lineage metadata.
- [ ] Export operates with no outbound network connectivity.

**Priority**: MUST_HAVE
**Complexity**: LOW (existing SaaS capability adapted)

---

#### FR-010: Audit Logging With Customer-Controlled Retention

**Description**: System MUST emit comprehensive audit events to a customer-controlled storage / SIEM destination, with retention controlled by the customer.

**Relates To**: BR-002, BR-004, Principle 6.

**Acceptance Criteria**:

- [ ] All authentication, authorisation, artefact, and operator-action events logged with structured fields.
- [ ] Audit destination configurable; default rejects unconfigured state.
- [ ] Logs are tamper-evident.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-011: Operator Runbook Library

**Description**: System MUST ship with operator runbooks for install, upgrade, roll-back, backup, restore, key rotation, decommission, incident response, and DR — usable end-to-end without vendor presence.

**Relates To**: BR-003, BR-004.

**Acceptance Criteria**:

- [ ] Runbook set ships with each release bundle.
- [ ] Runbooks validated annually in a representative isolated environment.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-012: Configurable Classification Marking

**Description**: System MUST allow the customer to configure the maximum classification permitted in the deployment, and MUST mark every artefact accordingly. System MUST refuse to accept content marked above the configured maximum.

**Relates To**: BR-004, Principle 7.

**Acceptance Criteria**:

- [ ] Configurable maximum classification (OFFICIAL / OFFICIAL-SENSITIVE / SECRET / TOP SECRET).
- [ ] Validation enforced at create / edit time.
- [ ] Configured maximum visible in UI footer per artefact.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-013: Vendor Remote Support Channel (Opt-In, Accreditation-Compliant)

**Description**: System MAY offer an opt-in vendor remote support channel; if offered, the channel MUST be subject to customer accreditation, customer-toggleable, and fully audited.

**Relates To**: BR-003.

**Acceptance Criteria**:

- [ ] Default state: no remote support channel active.
- [ ] If activated, the channel uses a customer-approved transport, requires explicit customer approval per session, and logs all activity to customer audit destination.

**Priority**: MAY_HAVE
**Complexity**: MEDIUM

---

#### FR-014: Long-Term Support Patch Delivery

**Description**: System MUST support delivery of LTS security patches via signed bundle into the accredited boundary using the same packaging as full releases.

**Relates To**: BR-005.

**Acceptance Criteria**:

- [ ] Patch bundle install does not require a full re-deploy.
- [ ] Patch signatures and SBOM updates included.
- [ ] Patch backports tested in CI against the LTS line.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-001: Interactive Response Time (Within Fixed Capacity Envelope)

**Requirement**: Within the customer's provisioned capacity envelope, interactive page operations meet p95 < 1 second, p99 < 3 seconds; API read p95 < 200 ms.
**Measurement**: Customer-controlled APM / RUM tooling.
**Priority**: HIGH.

---

#### NFR-P-002: AI Generation Latency (When Configured)

**Requirement**: AI-assisted generation, when configured to a customer-controlled endpoint, returns a result within 60 seconds at p95 with progress feedback. When AI is disabled, manual authoring performance is unaffected.
**Priority**: HIGH.

---

#### NFR-P-003: Bulk Export Latency

**Requirement**: Customer admin export completes within 10 minutes for a typical sovereign customer (defined as ≤ 5,000 artefacts, ≤ 50 GB total content).
**Priority**: HIGH.

---

### Availability and Resilience Requirements

#### NFR-A-001: Availability Target

**Requirement**: Availability targets agreed with the deploying authority; typical target ≥ 99.5% within working hours, constrained by the host environment.
**Priority**: CRITICAL (to the customer).

---

#### NFR-A-002: Disaster Recovery

**RPO**: ≤ 60 minutes (configurable).
**RTO**: ≤ 8 hours (configurable; constrained by host environment).
**Backup**: Customer-controlled within the accredited boundary; encryption at rest using customer-managed keys.
**DR Drill**: Annual customer-led DR drill with vendor support if requested.
**Priority**: CRITICAL.

---

#### NFR-A-003: Disconnected-Mode Fault Tolerance

**Requirement**: System MUST function fully when external networks are disconnected; non-critical features (AI generation) MAY be degraded but core authoring, viewing, and export MUST remain available.
**Priority**: CRITICAL.

---

### Scalability Requirements

#### NFR-S-001: Scaling Within Fixed Envelope

**Requirement**: Within the customer's provisioned capacity envelope, system MUST scale horizontally to meet demand without re-architecture; representative envelope stress-tested.
**Priority**: HIGH.

---

### Security Requirements

#### NFR-SEC-001: MOD Secure by Design / JSP 440 / JSP 604 Alignment

**Requirement**: Each release MUST be supported by a current MOD Secure by Design assessment and JSP 440 / JSP 604 mapping where the deploying authority is MOD.
**Priority**: CRITICAL (non-negotiable for MOD deployments).

---

#### NFR-SEC-002: NCSC CAF Mapping (For Non-MOD Sensitive Sites)

**Requirement**: Each release MUST be supported by a current NCSC CAF mapping for non-MOD sensitive-site customers.
**Priority**: CRITICAL.

---

#### NFR-SEC-003: Cryptography Appropriate to Classification

**Requirement**: Cryptographic primitives and key management MUST be appropriate to the accredited classification and MUST be HMG-approved where mandated.
**Priority**: CRITICAL.

---

#### NFR-SEC-004: No Outbound Network Calls Inside Boundary

**Requirement**: In sovereign mode, no outbound network call to any endpoint outside the customer's accredited boundary, validated by network-deny test in CI.
**Priority**: CRITICAL.

---

#### NFR-SEC-005: Supply-Chain Integrity

**Requirement**: Every artefact entering the customer boundary MUST be signed; SBOM (CycloneDX or SPDX) MUST be provided; hash manifest MUST be verifiable independently.
**Priority**: CRITICAL.

---

#### NFR-SEC-006: Within-Deployment Isolation

**Requirement**: Within-deployment isolation between projects, roles, and communities of interest enforced by automated and manual testing on every release.
**Priority**: CRITICAL.

---

#### NFR-SEC-007: Cleared-Personnel-Only Access (Where Mandated)

**Requirement**: Where the deploying authority requires cleared-personnel-only access, system MUST honour the constraint via identity claims and refuse access if claim absent.
**Priority**: CRITICAL.

---

#### NFR-SEC-008: Vulnerability Disclosure and Patching Window

**Requirement**: Vulnerability disclosure programme aligned with ISO 29147; LTS line patched within documented SLAs (Critical 7 days, High 30 days, Medium 90 days for sovereign — slower than SaaS due to customer-side accreditation re-runs).
**Priority**: CRITICAL.

---

### Compliance Requirements

#### NFR-C-001: Government Security Classifications Policy

**Requirement**: Each deployment configured to a maximum classification per the Government Security Classifications Policy; content above maximum rejected by validation.
**Priority**: CRITICAL.

---

#### NFR-C-002: UK GDPR / DPA 2018 (Where Personal Data Processed)

**Requirement**: Where the sovereign deployment processes personal data, UK GDPR and DPA 2018 obligations apply at the deploying authority's responsibility; vendor provides DPIA inputs and processor commitments per release.
**Priority**: CRITICAL.

---

#### NFR-C-003: Accessibility — WCAG 2.2 AA

**Requirement**: Tenant-facing UI meets WCAG 2.2 Level AA; PSBAR 2018 applies to public-sector deployments. Conformance maintained release on release.
**Priority**: CRITICAL (non-negotiable per Principle 12).

---

#### NFR-C-004: Audit Logging Retention

**Requirement**: Audit log retention configurable by customer to meet their accreditation; default ≥ 12 months.
**Priority**: CRITICAL.

---

#### NFR-C-005: Long-Term Support and Patching SLA

**Requirement**: LTS line maintained for ≥ 24 months from issue, with documented patching SLA (BR-005, NFR-SEC-008).
**Priority**: CRITICAL.

---

### Maintainability and Supportability

#### NFR-M-001: Operator Documentation

**Requirement**: Runbooks (FR-011) ship with each release; updated within 5 working days of any release.
**Priority**: HIGH.

---

#### NFR-M-002: Customer-Controlled Observability

**Requirement**: Logs, metrics, and traces emitted to customer-controlled destinations only (FR-005); no vendor-side observability for sovereign customer data.
**Priority**: HIGH.

---

### Portability and Interoperability

#### NFR-I-001: Open Standards Parity With SaaS

**Requirement**: Public APIs and event interfaces identical to those of the managed SaaS, with the same OpenAPI / AsyncAPI specifications and same versioning policy.
**Priority**: MUST_HAVE.

---

#### NFR-I-002: Data Portability

**Requirement**: Full-fidelity export in open formats (Markdown / JSON / YAML) at any time (FR-009).
**Priority**: CRITICAL.

---

## Integration Requirements

### INT-001: Customer Identity Provider

**Purpose**: Authenticate operator and user access via customer IdP (FR-007).
**Pattern**: OIDC / OAuth 2.x / SAML 2.0.
**Priority**: CRITICAL.

---

### INT-002: Customer-Controlled Object Storage / Database

**Purpose**: Persistent storage within the accredited boundary; vendor never custodian of customer artefact data.
**Pattern**: Customer-provisioned storage and database services inside the boundary.
**Priority**: CRITICAL.

---

### INT-003: Customer-Controlled Time Source, CA, Package Mirror

**Purpose**: Foundational services internal to the boundary (FR-005).
**Priority**: CRITICAL.

---

### INT-004: Customer-Controlled Observability Backend

**Purpose**: Logs, metrics, traces emitted within the boundary only (FR-005, NFR-M-002).
**Priority**: CRITICAL.

---

### INT-005: Customer-Approved AI / Model Endpoint (Optional)

**Purpose**: AI-assisted generation when the customer chooses to enable it (FR-004).
**Pattern**: Pluggable abstraction; default sovereign profile points nowhere.
**Priority**: MAY_HAVE (operationally; the abstraction is MUST_HAVE).

---

### INT-006: Customer Email / Notification Service

**Purpose**: Transactional notifications within the boundary.
**Priority**: HIGH.

---

### INT-007: Customer Key Management Service

**Purpose**: Customer-managed keys for encryption at rest; key rotation per FR-003.
**Priority**: CRITICAL.

---

### INT-008: G-Cloud / DOS / Defence Frameworks

**Purpose**: Procurement route (BR-007).
**Priority**: MUST_HAVE.

---

### INT-009: Vendor Remote Support Channel (Optional)

**Purpose**: Opt-in vendor support per FR-013 within the customer's accreditation envelope.
**Priority**: MAY_HAVE.

---

### INT-010: Vulnerability Disclosure Inbound

**Purpose**: External researchers can report vulnerabilities (NFR-SEC-008).
**Priority**: HIGH.

---

## Data Requirements

### DR-001: Customer Deployment

Attributes: deployment_id, customer_org, accreditation_level, max_classification, region (customer-defined), environment (prod / non-prod).
Classification: OFFICIAL.

### DR-002: User (Cleared Personnel)

Attributes: user_id, clearance_attribute (SC / DV / NPPV3 / etc., customer-defined claim), role, last_signin_at.
Classification: OFFICIAL (PII).
Retention: per customer accreditation; default lifetime of role + 30 days.

### DR-003: Project

Attributes: project_id_human, name, classification (≤ deployment maximum), community_of_interest, created_at, archived_at.
Classification: ≤ deployment maximum.

### DR-004: Artefact

Attributes: artefact_id, document_id, type, version, content (Markdown), classification, generation_metadata, created_by, updated_by.
Classification: ≤ deployment maximum (FR-012).

### DR-005: Audit Event

Attributes: event_id, actor_id, action, target_type, target_id, timestamp, ip, user_agent, result, correlation_id.
Classification: OFFICIAL.
Retention: per customer (FR-010).

### DR-006: Cryptographic Key Inventory

Attributes: key_id, purpose, algorithm, rotation_due_at, owner, attestation.
Classification: OFFICIAL-SENSITIVE.

### DR-007: SBOM and Release Manifest

Attributes: release_id, bundle_hash, sbom_format (CycloneDX / SPDX), sbom_uri, signature_uri.
Classification: OFFICIAL.
Retention: lifetime of release line.

### Data Migration

Sovereign customers do not typically migrate existing tooling content as part of v1; tenant import is via the public API or by uploading Markdown / JSON exports. Migration from project-001 SaaS to sovereign deployment supported via the export/import path (Principle 4 / 9).

---

## Constraints and Assumptions

### Technical Constraints

**TC-1**: All external dependencies MUST be vendorable for offline operation (no phone-home, no SaaS-only third parties on the critical path).
**TC-2**: Every artefact entering the customer boundary MUST be signed; vendor signing keys protected per supply-chain integrity policy.
**TC-3**: Bundle delivery MUST use the customer's approved data-transfer mechanism (e.g., approved one-way diode, approved sealed-media transfer).
**TC-4**: AI / model endpoint MUST be pluggable; default sovereign profile points nowhere (FR-004).
**TC-5**: Single source-of-truth Git repository; sovereign and SaaS produced from one revision (BR-001).

### Business Constraints

**BC-1**: No paywall on governance-critical features (Principle 1) applies in modified form: the sovereign offering is paid in its entirety, but feature parity with the SaaS governance set is preserved.
**BC-2**: Sovereign release LTS line independent of SaaS release cadence (BR-005).
**BC-3**: Sovereign pricing covers full cost-to-serve plus contribution margin (BR-006).

### Assumptions

**A-1**: Defence Cyber Protection Partnership (DCPP) Cyber Risk Profile applicable to the customer is identifiable at engagement.
**A-2**: Customers will provision the customer-controlled endpoints (time, CA, package mirror, observability, identity, AI) before install.
**A-3**: Customer accreditors will accept a vendor-provided MOD SbD evidence pack as input to (not replacement for) their own accreditation process.
**A-4**: Customer-side cleared personnel are available for operator role.

---

## Success Criteria and KPIs

### Business Success Metrics

| Metric | Baseline | Target | Timeline |
|--------|----------|--------|----------|
| Production sovereign deployments | 0 | ≥ 1 | GA + 18 months |
| Sovereign LTS adoption rate | n/a | 100% of sovereign customers on a current LTS line | Continuous |
| Sovereign accreditation outcome | n/a | All deployments achieve authority-to-operate | Per customer |
| Sovereign cost-to-serve recovery | n/a | ≥ 100% | Continuous |
| Contribution to SaaS SME tier | n/a | ≥ documented threshold | Quarterly |

### Technical Success Metrics

| Metric | Target |
|--------|--------|
| Air-gap install success rate in CI representative environment | 100% per release |
| Network-deny test pass rate | 100% per release |
| Disconnected upgrade with roll-back tested | 100% per release |
| Bundle signature / hash verifiable independently | 100% per release |
| Patch-delivery SLA (Critical / High / Medium) | 7 / 30 / 90 days |
| MOD SbD evidence pack current | Per release |

---

## Dependencies and Risks

### Dependencies

| Dependency | Owner | Target Date | Status |
|------------|-------|-------------|--------|
| Stakeholder analysis (project 002) | Service Owner | 2026-06-30 | At Risk |
| SOBC (project 002) | Service Owner | 2026-08-31 | Not Started |
| Risk Register (project 002) | Lead Architect | 2026-07-31 | Not Started |
| MOD Secure by Design assessment | Vendor Security Lead | 2026-09-30 | Not Started |
| Pluggable AI abstraction | Lead Architect | Aligned with project 001 ADR | Not Started |
| LTS release infrastructure | Lead Architect | GA – 6 months | Not Started |
| Customer engagement (≥ 1 MOD or sensitive-site customer for pilot) | Service Owner | GA – 6 months | Not Started |

### Risks (indicative — formal register pending)

| ID | Description | Probability | Impact | Mitigation |
|----|-------------|-------------|--------|------------|
| R-1 | Single-codebase pressure forces a fork between SaaS and sovereign | LOW | HIGH | Quarterly architecture review of feature flags; refactor budget; BR-001 enforcement |
| R-2 | Accreditation effort per customer exceeds estimate, undermining unit economics | MEDIUM | HIGH | Standardised evidence pack; customer-side runbook; pricing sized for variability |
| R-3 | Critical dependency (e.g., observability or DB tech) cannot operate offline | MEDIUM | HIGH | Component review against offline criterion before adoption; fallback options identified |
| R-4 | LTS patching commitments slip due to engineering resource pressure | MEDIUM | HIGH | LTS staffing model; explicit patch SLA in customer contracts |
| R-5 | Vendor signing-key compromise | LOW | CRITICAL | HSM-backed signing; key custody policy; rotation; audit logging |
| R-6 | Customer accreditator rejects vendor evidence format | MEDIUM | MEDIUM | Engage one MOD accreditor early; iterate evidence pack against their feedback |
| R-7 | Sovereign track distracts from SaaS strategic mission | MEDIUM | MEDIUM | Separate track ownership; clear gate on sovereign track funding from SaaS revenue not the other way around |

---

## Requirement Conflicts & Resolutions

> Source: derived from Principle 21, project 001 conflict analysis, and the sovereign-specific tensions surfaced during this requirements pass. Validate after `/arckit:stakeholders` for project 002 is complete.

### Conflict C-1: Single Codebase vs Customer-Specific Feature Demands

**Conflicting Requirements**:

- **A**: BR-001 (single codebase, no fork).
- **B**: Customer-specific feature demands (often surfaced during accreditation: bespoke headers, audit-event field renaming, classification labels in non-standard formats).

**Stakeholders Involved**:

- **Customer Accreditor**: wants bespoke specifics that match local policy.
- **Vendor Lead Architect**: wants no fork.

**Trade-off Analysis**:

| Option | Pros | Cons |
|--------|------|------|
| Per-customer fork | Maximum customer fit | ❌ Breaks BR-001; doubles engineering cost |
| Refuse all customisation | Pure single codebase | ❌ Some customers cannot accredit |
| Configuration-only customisation (chosen) | ✅ Single codebase preserved; ✅ accommodates real customer variation | ❌ Configuration surface grows; ❌ requires discipline |

**Resolution**: COMPROMISE / INNOVATE. All customer-specific behaviour expressed as configuration; new customer requirement either fits within the existing configuration surface or triggers a configuration extension that benefits all customers. No per-customer code branches. Decision authority: Lead Architect with Service Owner.

---

### Conflict C-2: LTS Stability vs SaaS Feature Velocity

**Conflicting Requirements**:

- **A**: BR-005 (LTS for ≥ 24 months).
- **B**: SaaS rapid release cadence (project 001).

**Trade-off Analysis**: Backporting security fixes from `main` to LTS lines is engineering work that competes with new SaaS features.

**Resolution**: PHASE. LTS line accepts only security and critical-bug fixes — no feature backports. SaaS features land in `main` and are available in the next LTS. Customers may upgrade to a newer LTS at their own cadence (typically annually). Decision authority: Product Manager with Lead Architect.

---

### Conflict C-3: Customer Self-Sufficiency vs Vendor Support Model

**Conflicting Requirements**:

- **A**: BR-003 (no vendor remote access by default).
- **B**: Vendor support obligations (debugging customer issues efficiently).

**Trade-off Analysis**: Without remote access, vendor cannot reproduce or fix customer-specific issues quickly. With unrestricted remote access, customer accreditation breaks.

**Resolution**: INNOVATE. Vendor support relies on (a) detailed runbooks (FR-011), (b) opt-in, audited, accreditation-compliant remote support channel (FR-013), (c) reproducible synthetic environments inside the vendor's own development infrastructure that mirror customer-typical configurations.

---

### Conflict C-4: AI Generation Richness vs Disconnected Operation

**Conflicting Requirements**:

- **A**: AI generation a primary differentiator (project 001 FR-004).
- **B**: Sovereign default profile MUST NOT call any external service (BR-002).

**Trade-off Analysis**: Major commercial AI providers operate as SaaS only.

**Resolution**: PHASE / INNOVATE. AI endpoint is pluggable (FR-004). Customers who run an approved on-prem model (or have an accredited path to a customer-controlled cloud endpoint) can enable AI generation. Customers who do not get full functionality minus AI generation; manual authoring is unaffected. Decision authority: Lead Architect.

---

## Timeline and Milestones

| Milestone | Description | Target Date | Dependencies |
|-----------|-------------|-------------|--------------|
| Stakeholder analysis (project 002) | `/arckit:stakeholders` | 2026-06-30 | This document |
| Requirements approval | Stakeholder sign-off | 2026-07-31 | Stakeholder analysis |
| SOBC | Strategic Outline Business Case | 2026-08-31 | Requirements |
| MOD SbD assessment | `/arckit:mod-secure` | 2026-09-30 | Requirements |
| HLD | High-Level Design (sovereign packaging) | 2026-10-31 | Requirements, SbD |
| Customer engagement (≥ 1) | Sovereign pilot customer signed | 2027-04-30 | HLD, GA-proximity |
| Alpha (vendor-internal) | Bundle install validated in CI representative environment | 2027-04-30 | HLD |
| Private Beta (1 customer) | First sovereign deployment | 2027-08-31 | Alpha |
| GA | Sovereign offering generally available | 2027-12-31 | Beta |

---

## Budget

> ⚠️ Indicative only — replace with `/arckit:sobc` figures.

### One-Off (Build)

| Category | Estimate | Notes |
|----------|----------|-------|
| Engineering (sovereign packaging, LTS infrastructure) | TBD | |
| Security and accreditation evidence | TBD | MOD SbD pack, NCSC CAF mapping |
| Documentation (operator runbooks, customer-facing) | TBD | |
| Customer engagement / pre-sales | TBD | MOD framework engagement |
| **Total** | TBD | |

### Ongoing (Annual)

| Category | Estimate | Notes |
|----------|----------|-------|
| LTS patch backporting | TBD | Two parallel LTS lines |
| Customer support (cleared personnel where required) | TBD | |
| Accreditation refresh | TBD | Per customer per year |
| Annual DR / install validation | TBD | Representative environment |
| **Total** | TBD | |

---

## Approval

| Reviewer | Role | Status | Date |
|----------|------|--------|------|
| [PENDING] | Service Owner | [ ] Approved | [PENDING] |
| [PENDING] | Lead Architect | [ ] Approved | [PENDING] |
| [PENDING] | Security Lead | [ ] Approved | [PENDING] |
| [PENDING] | DPO | [ ] Approved | [PENDING] |
| [PENDING] | MOD Customer Accreditor (pilot) | [ ] Approved | [PENDING] |

---

## Appendices

### Appendix A: Glossary

- **SAL** — Security Aspects Letter
- **SbD** — Secure by Design
- **JSP 440** — Defence Manual of Security
- **JSP 604** — Defence Manual for the Authorisation of Information Systems
- **CAF** — NCSC Cyber Assessment Framework
- **GovAssure** — NCSC assessment scheme for OES
- **DCPP** — Defence Cyber Protection Partnership
- **DOS** — Digital Outcomes and Specialists
- **G-Cloud** — UK Government cloud framework
- **HSM** — Hardware Security Module
- **LTS** — Long-Term Support
- **OES** — Operator of Essential Services
- **SBOM** — Software Bill of Materials (CycloneDX or SPDX)
- **SC / DV / NPPV3** — UK personnel security clearance levels
- **SIRO** — Senior Information Risk Owner

### Appendix B: Reference Documents

- `projects/000-global/ARC-000-PRIN-v2.0.md` — Architecture Principles (Principle 21 anchors this project)
- `projects/001-arckit-saas/ARC-001-REQ-v1.0.md` — Sister project requirements (managed SaaS)
- `projects/001-arckit-saas/ARC-001-STKE-v1.0.md` — Sister project stakeholder analysis (DDaT architects detailed)
- MOD Secure by Design — assessment methodology
- JSP 440 — Defence Manual of Security
- JSP 604 — Defence Manual for the Authorisation of Information Systems
- NCSC Cyber Assessment Framework (CAF)
- NCSC Cloud Security Principles (14)
- HMG Government Security Classifications Policy
- UK GDPR / Data Protection Act 2018
- Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018
- Defence Cyber Protection Partnership Cyber Risk Profile

### Appendix C: Wireframes and Mockups

To be produced post-HLD.

### Appendix D: Data Models

To be produced via `/arckit:data-model` after this document is approved.

---

## External References

> No external policy documents were placed in `projects/002-arckit-sovereign/external/` at the time of generation. UK Government and MOD policies referenced are public-domain and cited by name. Material at OFFICIAL-SENSITIVE or higher should not be placed in this repository unless the hosting environment is accredited to handle that classification.

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
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Derived from `ARC-000-PRIN-v2.0.md` Principle 21, sister project 001 (REQ + STKE), MOD Secure by Design / JSP 440 / JSP 604 / NCSC CAF reference frameworks. Stakeholder analysis (STKE), SOBC, risk register, and MOD SbD assessment for project 002 not yet generated — flagged for follow-up.
