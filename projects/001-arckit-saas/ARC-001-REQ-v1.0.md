# Project Requirements: ArcKit as a Service (Managed SaaS)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-REQ-v1.0 |
| **Document Type** | Business and Technical Requirements |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Date** | 2026-06-02 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, Crown Commercial Service liaison, GDS, CDDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:requirements` command, scoped to managed SaaS only — sovereign deployment deferred to a separate project | [PENDING] | [PENDING] |

## Document Purpose

Defines the business and technical requirements for the **managed multi-tenant SaaS** offering of ArcKit as a Service. This document is the source-of-truth for downstream design, vendor selection, contracts, testing, and assurance activities for the SaaS route. The sovereign / air-gapped deployment route is explicitly out of scope and will be specified in a separate requirements document.

> **Source steer (user input, 2026-05-03)**: *"saas service we will do sepate for soverign"* — interpreted as: this requirements document covers the managed SaaS only; sovereign deployment is deferred to a future, separate requirements artefact.

> **Upstream artefact gaps**:
>
> - **Stakeholder Analysis (STKE)** — not yet created. Stakeholders below are placeholders derived from the principles document and the project context; these MUST be validated by running `/arckit:stakeholders` before this document is approved.
> - **Strategic Outline Business Case (SOBC)** — not yet created. Cost and ROI figures in this document are indicative; values MUST be validated by running `/arckit:sobc`.
> - **Risk Register (RISK)** — not yet created. Risks below are derived from the principles and recognisable platform-risk patterns; the formal register MUST be created with `/arckit:risk`.

---

## Executive Summary

### Business Context

The UK Government has a stated ambition to spend more with SMEs (Procurement Act 2023, SME Action Plans). SMEs supplying or seeking to supply public-sector services typically lack the in-house enterprise architecture capability that larger system integrators take for granted, and commercial EA tooling is priced for enterprises. This creates a measurable capability gap that disadvantages SMEs in competitive bids and downstream assurance.

ArcKit as a Service (managed SaaS) closes that gap. It provides a free or substantially-cheaper-for-SMEs managed offering of the ArcKit governance toolkit: principles, requirements, ADRs, traceability, design reviews, compliance assessments, and AI-assisted artefact generation. The platform is operated by the vendor in the United Kingdom under OFFICIAL classification, with cross-subsidy from large-enterprise tenants funding the SME tier.

The managed SaaS is the entry route for the broader ArcKit as a Service offering. A separate sovereign deployment route (Principle 21, `ARC-000-PRIN-v2.0.md`) addresses MOD and other sensitive sites; that route is out of scope of this document.

### Objectives

- Deliver a UK-resident, multi-tenant SaaS that meets UK Government policy (TCoP, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, UK GDPR, PSBAR 2018, G-Cloud).
- Provide a verifiable free entry tier for SMEs supplying UK government, sufficient for genuine end-to-end delivery work.
- Provide transparent published pricing for paid tiers, with no governance-critical features paywalled.
- Operate at OFFICIAL with OFFICIAL-SENSITIVE handling caveats where tenants opt in.
- Listing on G-Cloud so that buying authorities can call off the service without bespoke procurement.

### Expected Outcomes

- 100% of governance-critical features (principles, requirements, ADRs, diagrams, traceability, full export) available on the free tier.
- ≥ 200 verified UK SMEs onboarded within 12 months of GA.
- ≥ 99.9% rolling-30-day availability for tenant-facing services from GA + 3 months.
- Published per-seat list price for paid SME tier on the public website (no "contact sales" gating).
- Evidence pack covering TCoP, NCSC CAF, NCSC Cloud Security Principles, UK GDPR, and WCAG 2.2 AA available to tenants on demand.

### Project Scope

**In Scope**:

- Managed multi-tenant SaaS hosted in the United Kingdom.
- Tenant onboarding, SME eligibility verification, billing, and offboarding (data export and deletion).
- Authoring, versioning, AI-assisted generation, and export of ArcKit artefacts.
- SSO integration with tenant identity providers using standard protocols.
- Public APIs and event interfaces aligned with Principle 4 (Open Standards).
- Public status page and tenant-facing audit log.
- WCAG 2.2 AA accessible UI with a published Accessibility Statement.
- G-Cloud listing and Crown Commercial Service alignment.
- Content classification up to OFFICIAL with OFFICIAL-SENSITIVE handling caveats where tenants opt in.

**Out of Scope** (deferred or excluded):

- Sovereign / on-premise / air-gapped deployment for MOD and sensitive sites — separate project, see Principle 21.
- Classifications above OFFICIAL-SENSITIVE.
- Hard-fork "stripped down" community edition.
- Bespoke per-tenant code customisation.
- Migration from legacy vendor EA tooling (advisory only; no automated importers in v1).
- Mobile native apps in v1 (responsive web only).
- Languages other than English in v1 (Welsh / English-language localisation deferred).

---

## Stakeholders

> ⚠️ Placeholder set — to be validated and refined by `/arckit:stakeholders`.

| Stakeholder | Role | Organization | Involvement Level |
|-------------|------|--------------|-------------------|
| Mark Craddock | Service Owner / Sponsor | ArcKit as a Service | Decision maker |
| [PENDING] | Product Owner | ArcKit as a Service | Requirements definition |
| [PENDING] | Lead Architect | ArcKit as a Service | Technical oversight |
| [PENDING] | Security Lead / SIRO | ArcKit as a Service | Security review and accreditation |
| [PENDING] | Data Protection Officer | ArcKit as a Service | UK GDPR / DPA compliance |
| [PENDING] | Accessibility Lead | ArcKit as a Service | WCAG 2.2 AA conformance |
| [PENDING] | Crown Commercial Service liaison | CCS | G-Cloud listing and procurement |
| SME Tenant Representative | End user (SME architect) | UK SME suppliers | User acceptance |
| Buying Authority Representative | End user (gov buyer) | UK Public Sector | Service evaluation |
| GDS / CDDO Service Assessor | Assessor | GDS / CDDO | Service Standard assessment |

---

## Business Requirements

### BR-001: Free Tier for Verified UK SMEs

**Description**: The platform MUST provide a free tier that is genuinely usable for end-to-end government delivery work for verified UK SMEs supplying or seeking to supply UK government.

**Rationale**: The platform's strategic purpose (Principle 1, `ARC-000-PRIN-v2.0.md`) is to lower the cost of doing high-quality architecture for SMEs supplying government. A trial-style free tier fails this purpose.

**Success Criteria**:

- Free tier supports at least one active project end-to-end with no time limit.
- Free tier covers the essential ArcKit baseline: principles, requirements, ADRs, diagrams, traceability, glossary, full export.
- Free tier supports at least 5 named users per SME tenant.
- No governance-critical feature (security, audit log export, data export, accessibility) is paywalled.

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner
**Traces To**: Principle 1 (Equitable Access for SMEs)

---

### BR-002: Transparent Published Pricing

**Description**: Paid SaaS tiers MUST have list prices published on the public website. No "contact sales" gating for SME-eligible tiers.

**Rationale**: SMEs lose competitive bids when they cannot model their cost base. Hidden enterprise pricing replicates the commercial market and undermines Principle 1.

**Success Criteria**:

- Per-seat per-month list price published for each paid SME tier.
- Annual list price published for the large-enterprise tier (which cross-subsidises the SME tier).
- Pricing page accessible without login.
- Pricing changes communicated to existing tenants at least 60 days in advance.

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner
**Traces To**: Principle 1, Principle 17 (FinOps)

---

### BR-003: SME Eligibility Verification

**Description**: The platform MUST verify SME eligibility against a published, transparent definition before granting SME-tier pricing.

**Rationale**: The SME-affordable commitment is targeted; non-SMEs must be charged at the funding tier. Without verification the cross-subsidy model fails.

**Success Criteria**:

- Published SME eligibility policy aligned with Companies Act 2006 SME thresholds and Crown Commercial Service guidance, subject to legal review.
- Automated check against Companies House data plus self-attestation.
- Annual re-verification of SME status.
- Audit trail of verification decisions retained for 7 years.

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner
**Traces To**: Principle 1

---

### BR-004: G-Cloud Procurement Route

**Description**: The service MUST be listed on the UK Government Digital Marketplace (G-Cloud framework) so that buying authorities can call off without bespoke procurement.

**Rationale**: Public sector buyers default to framework-based procurement; absence from G-Cloud removes most plausible buyer journeys.

**Success Criteria**:

- Service listed on the current G-Cloud framework iteration.
- Service definition, T&Cs, pricing, and SFIA-rated rates published on Digital Marketplace.
- Minimum commitment terms friendly to SME-buying-from-SME use cases.
- Listing kept current across G-Cloud framework refreshes.

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner, CCS liaison
**Traces To**: Principle 1

---

### BR-005: Cross-Subsidy Funding Model

**Description**: The commercial model MUST cross-subsidise the SME free and SME paid tiers from large-enterprise revenue, with documented unit economics that make the model sustainable.

**Rationale**: Free tiers without an underlying funding mechanism close under cost pressure. The cross-subsidy must be designed in, not assumed.

**Success Criteria**:

- Documented per-tenant cost-to-serve model covering compute, storage, AI inference, and support.
- Large-enterprise list price set at least at break-even for the combined SME tier population at target scale.
- Annual affordability review published, comparing the SME paid tier price to commercial EA tooling.
- Margin reserve sufficient to absorb a documented stress scenario (e.g., 2× free-tier adoption).

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner, Finance
**Traces To**: Principle 1, Principle 17

---

### BR-006: UK Public Sector Policy Evidence

**Description**: The platform MUST produce, on demand, an evidence pack covering UK public-sector compliance: TCoP, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, UK GDPR / DPA 2018, PSBAR 2018 / WCAG 2.2 AA.

**Rationale**: Tenants will be asked for this evidence by their buying authorities; the platform should provide it rather than expose tenants to repeated assurance work.

**Success Criteria**:

- Evidence pack downloadable by tenants from the admin portal.
- Each evidence section dated and traceable to a current assessment.
- Pack regenerated at least annually and on material change.

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner, Compliance
**Traces To**: Principles 5, 7, 12

---

### BR-007: Tenant Portability and Exit

**Description**: Tenants MUST be able to leave the service at any time with their full content in open, machine-readable formats and verifiable destruction of their data after a documented grace period.

**Rationale**: The Open Standards principle and the SME-affordability principle both depend on credible exit. Without it, the cost case for SMEs deteriorates over time.

**Success Criteria**:

- One-click full export of all tenant content, including lineage metadata, in open formats (Markdown / JSON / YAML).
- Documented grace period after tenancy ends (default 30 days, configurable up to 90).
- Verifiable destruction certificate provided to the tenant after deletion.
- Exit path tested at least annually.

**Priority**: MUST_HAVE
**Stakeholder**: Service Owner, DPO
**Traces To**: Principle 4, Principle 9

---

### BR-008: Adoption and Activation

**Description**: The service MUST be adopted at scale by UK SMEs supplying government within the first 12 months of GA.

**Rationale**: Without scale, the cross-subsidy model in BR-005 is not viable.

**Success Criteria**:

- ≥ 200 verified UK SMEs onboarded within 12 months of GA.
- ≥ 60% activation rate (tenant produces ≥ 3 artefacts in first 30 days).
- ≥ 70% rolling 90-day retention on the SME paid tier.

**Priority**: SHOULD_HAVE
**Stakeholder**: Service Owner, Marketing
**Traces To**: Principle 1

---

## Functional Requirements

### User Personas

#### Persona 1: SME Architect

- **Role**: Senior architect / tech lead at an SME (1–250 employees) bidding for or delivering UK government work.
- **Goals**: Produce credible governance artefacts (principles, requirements, ADRs, diagrams) without paying for enterprise EA tooling; pass GDS Service Standard and TCoP assessments.
- **Pain Points**: Commercial EA tooling priced out of reach; bespoke document templating consumes billable capacity; assurance gaps surface late.
- **Technical Proficiency**: High (architects, developers).

#### Persona 2: SME Founder / Bid Lead

- **Role**: Founder, MD, or bid lead at an SME pursuing UK government work.
- **Goals**: Win bids by demonstrating governance maturity; reduce cost of pre-bid investment.
- **Pain Points**: Lack of in-house EA capability; cost of governance tooling for unsuccessful bids.
- **Technical Proficiency**: Medium.

#### Persona 3: Buying Authority Architect

- **Role**: Architect at a buying authority (department, ALB, NHS body, local authority) reviewing supplier governance evidence.
- **Goals**: Assess supplier governance maturity quickly and consistently.
- **Pain Points**: Inconsistent supplier artefacts make comparative evaluation slow.
- **Technical Proficiency**: High.

#### Persona 4: ArcKit Service Operator

- **Role**: Vendor SRE / support engineer.
- **Goals**: Operate the platform within SLOs; respond to incidents; manage tenant lifecycle without breaching tenant isolation.
- **Pain Points**: Cross-tenant operational tasks must avoid leaking tenant data.
- **Technical Proficiency**: High.

---

### Use Cases

#### UC-1: SME Tenant Self-Service Onboarding

**Actor**: SME Founder / Bid Lead
**Preconditions**: Prospective tenant has a registered UK company.
**Main Flow**:

1. User visits the public marketing site and selects "Sign up — Free for verified UK SMEs".
2. User provides company name, Companies House number, primary contact email, and admin user details.
3. System verifies company against Companies House data and applies SME eligibility check (Companies Act 2006 thresholds).
4. System emails a verification link to the primary contact address.
5. User completes email verification and accepts T&Cs.
6. System provisions the tenant on the free tier with audit-log entry.
7. User lands on the empty tenant dashboard with onboarding tour.

**Postconditions**: Tenant exists in free tier; admin user signed in; first project can be created.
**Alternative Flows**:

- **Alt 6a**: If Companies House data ambiguous (e.g., multiple matches), system asks user to confirm the correct entity.
- **Alt 3a**: If the company is not SME-eligible (exceeds thresholds), system offers the large-enterprise paid tier.

**Exception Flows**:

- **Ex 1**: Companies House service unavailable — onboarding queued and retried; user notified by email when complete.

**Business Rules**: SME eligibility re-verified annually (BR-003).
**Priority**: CRITICAL

---

#### UC-2: AI-Assisted Artefact Generation

**Actor**: SME Architect
**Preconditions**: User signed in; project exists.
**Main Flow**:

1. User selects an artefact type (e.g., principles, requirements, ADR).
2. User provides a short prompt or selects existing project context.
3. System generates a draft using the AI engine, applying ArcKit templates and quality checks.
4. User reviews, edits, and saves.
5. System records generation metadata (command, model, prompt) for lineage.

**Postconditions**: Draft artefact persisted with lineage metadata.
**Alternative Flows**:

- **Alt 3a**: If AI engine throttled or unavailable, user can save manually-authored content with no AI generation; system surfaces the degradation in the UI.

**Exception Flows**:

- **Ex 1**: Generation fails — content not saved; error surfaced; quota not consumed.

**Business Rules**: Per-tenant AI generation quotas enforced; quotas published.
**Priority**: HIGH

---

#### UC-3: Tenant Data Export and Exit

**Actor**: SME Architect (admin role)
**Preconditions**: Admin user signed in.
**Main Flow**:

1. Admin requests full export from the admin portal.
2. System packages all tenant artefacts plus lineage metadata into a signed archive in open formats.
3. System notifies the admin when ready (within NFR-P-003 target).
4. Admin downloads the archive over an authenticated link.

**Postconditions**: Tenant has a complete copy of their data in portable format.
**Business Rules**: Export must be byte-for-byte equivalent to the live data at the moment of export request.
**Priority**: CRITICAL

---

### Functional Requirements Detail

#### FR-001: Tenant Provisioning and SME Verification

**Description**: System MUST provision new tenants via self-service signup, verifying SME eligibility against Companies House data plus self-attestation.

**Relates To**: BR-001, BR-003, UC-1

**Acceptance Criteria**:

- [ ] Given a valid Companies House number for an SME-eligible UK company, when a user signs up, then the tenant is provisioned on the free tier within 5 minutes.
- [ ] Given a non-SME company, when a user signs up, then the system offers the large-enterprise tier and does not provision a free-tier tenant.
- [ ] Given Companies House service unavailable, when a user signs up, then onboarding is queued and the user is notified.
- [ ] Verification decisions and inputs retained for 7 years.

**Data Requirements**:

- **Inputs**: Company number, company name, primary contact email, admin user details.
- **Outputs**: Tenant record, verification decision record, audit log entry.
- **Validations**: Email format, Companies House response, SME thresholds.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM
**Dependencies**: INT-003 (Companies House API)

---

#### FR-002: Multi-Tenant Workspace Management

**Description**: System MUST support per-tenant workspaces with multiple projects per tenant, multiple users per tenant, role-based access control within tenant, and full logical isolation between tenants.

**Relates To**: BR-001, Principle 8

**Acceptance Criteria**:

- [ ] Given two tenants A and B, when a user from A queries any artefact, then no artefact from B is ever returned.
- [ ] Given a tenant admin, when they invite a user, then the user has only the role assigned and only within that tenant.
- [ ] Cross-tenant access scenarios proven impossible by automated test on every release.

**Priority**: MUST_HAVE
**Complexity**: HIGH
**Dependencies**: NFR-SEC-002

---

#### FR-003: Architecture Artefact Authoring

**Description**: System MUST support authoring of all ArcKit artefact types (principles, requirements, ADRs, diagrams, traceability, glossary, plus other types listed in the ArcKit plugin).

**Relates To**: BR-001

**Acceptance Criteria**:

- [ ] Given a project, when a user creates an artefact, then it is persisted with the standard ArcKit document control header.
- [ ] Edits are versioned and attributed to the editing user with timestamp.
- [ ] Document IDs follow `ARC-{PROJECT_ID}-{TYPE}-v{VERSION}` convention.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-004: AI-Assisted Generation

**Description**: System MUST provide AI-assisted draft generation for ArcKit artefact types, with generation metadata recorded for lineage.

**Relates To**: BR-001, UC-2, Principle 9

**Acceptance Criteria**:

- [ ] Given a prompt, when generation succeeds, then the draft includes the generated content and recorded generation metadata (command, model, model version, prompt, timestamp).
- [ ] Generation flagged in the UI as AI-produced.
- [ ] Tenant can disable AI generation entirely at tenancy level.
- [ ] Per-tenant AI generation quotas enforced and visible to the tenant.
- [ ] If the AI engine is unavailable, manual authoring continues without degradation.

**Priority**: SHOULD_HAVE (the platform is usable without AI)
**Complexity**: HIGH
**Dependencies**: INT-005 (AI / LLM endpoint), NFR-A-003

---

#### FR-005: Artefact Versioning and Audit Trail

**Description**: System MUST version every artefact change and record an immutable audit trail per tenant.

**Relates To**: Principle 9

**Acceptance Criteria**:

- [ ] Given an artefact, when a user edits and saves, then a new version is recorded with diff and editor identity.
- [ ] Audit trail exposed to tenant admins via the admin portal.
- [ ] Audit log retained for at least 12 months (NFR-C-002).

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-006: Full-Fidelity Export

**Description**: System MUST provide one-click export of all tenant content plus lineage metadata in open formats with no paywall.

**Relates To**: BR-007, UC-3, Principle 4, Principle 9

**Acceptance Criteria**:

- [ ] Given an admin request, when export is requested, then a signed archive is produced within 10 minutes for a typical SME tenant.
- [ ] Archive contains 100% of tenant artefacts in Markdown / JSON / YAML.
- [ ] Lineage metadata included for every generated artefact.
- [ ] Export available on every tier, including free.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-007: SSO Integration

**Description**: System MUST support tenant-side SSO using standard protocols (OIDC, OAuth 2.x, SAML 2.0) on all paid tiers, and SHOULD support SSO on the free tier.

**Relates To**: Principle 4, Principle 5

**Acceptance Criteria**:

- [ ] Given a tenant configured with an OIDC provider, when a user signs in, then identity and group claims are honoured.
- [ ] SSO setup self-service for tenant admins.
- [ ] No additional licence fee gates SSO away from any tier (Principle 1: governance-critical features must not be paywalled).

**Priority**: MUST_HAVE on paid tiers, SHOULD_HAVE on free tier
**Complexity**: MEDIUM

---

#### FR-008: Public API and Event Interfaces

**Description**: System MUST expose a public REST API and an event subscription interface for all primary tenant operations.

**Relates To**: Principle 4

**Acceptance Criteria**:

- [ ] OpenAPI specification published and versioned.
- [ ] AsyncAPI specification published for events.
- [ ] All UI operations achievable via API.
- [ ] Backward compatibility window ≥ 12 months for breaking changes.

**Priority**: MUST_HAVE
**Complexity**: HIGH

---

#### FR-009: Public Status Page and Tenant Notifications

**Description**: System MUST provide a public status page and per-tenant in-product notifications for incidents and maintenance.

**Relates To**: Principle 6, Principle 14

**Acceptance Criteria**:

- [ ] Status page externally accessible without login.
- [ ] Status reflects health of core tenant-facing services.
- [ ] Tenants can subscribe to email and webhook notifications.

**Priority**: MUST_HAVE
**Complexity**: LOW

---

#### FR-010: Tenant Offboarding and Data Deletion

**Description**: System MUST support tenant-initiated offboarding with documented grace period and verifiable data destruction.

**Relates To**: BR-007, Principle 7, Principle 9

**Acceptance Criteria**:

- [ ] Default 30-day grace period; tenant-configurable up to 90 days.
- [ ] After grace period, all tenant data deleted from primary stores and from backups within the documented backup retention window.
- [ ] Destruction certificate emailed to tenant primary contact.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-011: Billing and Subscription Management

**Description**: System MUST manage tier subscriptions, invoicing, and payment for paid tiers.

**Relates To**: BR-002, BR-005

**Acceptance Criteria**:

- [ ] Tenant admins can change tier self-service.
- [ ] Invoices generated automatically with VAT-compliant fields for UK tenants.
- [ ] G-Cloud purchase orders accepted (BR-004).
- [ ] Free tier requires no payment instrument.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM
**Dependencies**: INT-002 (Payment processing)

---

#### FR-012: Tenant Audit Log Access

**Description**: System MUST provide tenant admins with searchable, exportable audit logs of access and change events within their tenant.

**Relates To**: NFR-C-002, Principle 5

**Acceptance Criteria**:

- [ ] Logs cover authentication, authorisation, artefact create/edit/delete, export, billing changes.
- [ ] Logs filterable by user, action, time range.
- [ ] Logs exportable as JSON.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-013: GOV.UK Design System Alignment

**Description**: Tenant-facing UI SHOULD align with the GOV.UK Design System patterns where appropriate, to reduce friction for public-sector users.

**Relates To**: Principle 12

**Acceptance Criteria**:

- [ ] Components selected from the GOV.UK Design System where a suitable pattern exists.
- [ ] Where bespoke components are used, they are documented with accessibility evidence.

**Priority**: SHOULD_HAVE
**Complexity**: MEDIUM

---

#### FR-014: Admin Console for Service Operators

**Description**: System MUST provide a separate admin console for vendor operators with break-glass procedures and full audit logging of operator actions.

**Relates To**: Principle 5, Principle 18

**Acceptance Criteria**:

- [ ] Operator access gated by MFA and time-bound elevation.
- [ ] All operator actions logged and tagged distinctly from tenant actions.
- [ ] No operator action can read tenant artefact content without explicit, logged consent or a documented break-glass justification.

**Priority**: MUST_HAVE
**Complexity**: MEDIUM

---

#### FR-015: Public Marketing and Pricing Site

**Description**: System MUST publish a public marketing site with pricing, eligibility, T&Cs, status page link, accessibility statement, and security/compliance evidence summary.

**Relates To**: BR-002, BR-006, Principle 12

**Acceptance Criteria**:

- [ ] Pricing page publicly accessible without login.
- [ ] Accessibility statement published and current.
- [ ] Compliance evidence summary published with pointers to detailed evidence (available on tenant request).

**Priority**: MUST_HAVE
**Complexity**: LOW

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-001: Interactive Response Time

**Requirement**:

- Web page load time: < 1 second p95, < 3 seconds p99
- API response time (read operations): < 200 ms p95, < 1 second p99
- API response time (write operations excluding generation): < 1 second p95

**Measurement Method**: Real User Monitoring (RUM) and APM tooling, reported on rolling 30-day windows.

**Load Conditions**:

- Concurrent active users at target scale: ≥ 1,000 across all tenants
- Sustained API throughput: ≥ 100 requests/second across all tenants
- Peak burst: 5× sustained for 5 minutes

**Priority**: HIGH
**Traces To**: Principle 13

---

#### NFR-P-002: AI Generation Latency

**Requirement**: AI-assisted generation must return a result within 60 seconds at p95 with progress feedback in the UI throughout.

**Priority**: HIGH
**Traces To**: Principle 13

---

#### NFR-P-003: Bulk Export Latency

**Requirement**: Tenant export must complete within 10 minutes for a typical SME tenant (defined as ≤ 500 artefacts, ≤ 5 GB total content).

**Priority**: HIGH
**Traces To**: BR-007, FR-006

---

### Availability and Resilience Requirements

#### NFR-A-001: Availability Target

**Requirement**: Core tenant-facing services MUST achieve ≥ 99.9% rolling-30-day availability (≈ 43 minutes downtime per month) measured externally.

**Maintenance Windows**: Planned maintenance announced ≥ 5 working days in advance; outside UK working hours where possible.

**Priority**: CRITICAL
**Traces To**: Principle 14

---

#### NFR-A-002: Disaster Recovery

**RPO**: < 15 minutes
**RTO**: < 4 hours
**Backup Requirements**: Daily off-site backups within UK region; backup retention 35 days minimum; backups encrypted at rest.
**Failover**: Automatic failover between UK availability zones; cross-region failover within UK if available.
**DR Testing**: Annual full DR drill with documented evidence.

**Priority**: CRITICAL
**Traces To**: Principle 14

---

#### NFR-A-003: Fault Tolerance and Graceful Degradation

**Requirement**: System MUST gracefully degrade when non-critical components (e.g., AI generation, search index) fail. Core authoring, viewing, and export MUST remain available.

**Resilience Patterns Required**:

- [x] Circuit breaker for external dependencies
- [x] Retry with exponential backoff
- [x] Timeout on all network calls
- [x] Bulkhead isolation between tenants
- [x] Graceful degradation with reduced functionality

**Priority**: CRITICAL
**Traces To**: Principle 3

---

### Scalability Requirements

#### NFR-S-001: Horizontal Scaling

**Requirement**: System MUST support horizontal scaling without code changes.

**Growth Projections** (indicative; refine in SOBC):

- GA + 6 months: 500 tenants, 2,000 users
- GA + 12 months: 1,500 tenants, 7,000 users
- GA + 24 months: 5,000 tenants, 25,000 users

**Auto-Scaling**: Demand-driven; targets defined per service.

**Priority**: HIGH
**Traces To**: Principle 2

---

#### NFR-S-002: Data Volume Scaling

**Requirement**: System MUST handle artefact storage growth in line with NFR-S-001 tenant growth (estimated 50 GB per 1,000 tenants).

**Data Tiering**: Hot/warm tiering for active vs archived projects; retention aligned with FR-010.

**Priority**: HIGH
**Traces To**: Principle 2

---

### Security Requirements

#### NFR-SEC-001: Authentication

**Requirement**: All human authentication MUST use industry-standard protocols (OIDC, OAuth 2.x, SAML 2.0) with multi-factor authentication.

**MFA**:

- Required for all human access (tenant users and operators)
- MFA methods: authenticator app and hardware token; SMS only as fallback

**Session**:

- Inactivity timeout: 30 minutes (tenant-configurable up to 60)
- Absolute session timeout: 12 hours
- Re-authentication for billing changes, tenant admin changes, and full export

**Priority**: CRITICAL
**Traces To**: Principle 5

---

#### NFR-SEC-002: Tenant Isolation

**Requirement**: Tenant data MUST be logically isolated such that no tenant can read, write, infer, or exhaust another tenant's data or capacity.

**Verification**:

- Per-request tenant ID propagation enforced at every boundary.
- Default-deny authorisation at every layer.
- Automated isolation tests run in CI on every change.
- External penetration testing covers cross-tenant scenarios.

**Priority**: CRITICAL
**Traces To**: Principle 8

---

#### NFR-SEC-003: Authorisation

**Requirement**: Role-based access control with least-privilege defaults within each tenant.

**Roles** (minimum set): Tenant Admin, Project Editor, Project Reader, Billing Contact.

**Privilege Elevation**: Time-boxed; logged.

**Priority**: CRITICAL
**Traces To**: Principle 5

---

#### NFR-SEC-004: Encryption

**Requirement**:

- Data in transit: current industry-standard TLS with strong ciphers; deprecated ciphers prohibited.
- Data at rest: industry-standard symmetric encryption for all data stores and backups.
- Application-level encryption for sensitive PII fields where appropriate.

**Key Management**: Customer-managed keys offered on the large-enterprise tier; vendor-managed keys default on SME tiers; keys rotated at least annually.

**Priority**: CRITICAL
**Traces To**: Principle 5

---

#### NFR-SEC-005: Secrets Management

**Requirement**: No secrets in code, configuration files, or container images. All secrets in a managed vault with audit logging.

**Rotation**: Automatic rotation at least every 90 days for service credentials; immediate rotation on suspected compromise.

**Priority**: CRITICAL
**Traces To**: Principle 5

---

#### NFR-SEC-006: Vulnerability Management

**Requirement**:

- Dependency scanning, container scanning, SAST, and DAST in CI/CD.
- No critical or high vulnerability shipped to production without compensating control.
- External penetration testing at least annually and on material change.
- Vulnerability disclosure programme aligned with ISO 29147.

**Remediation SLA**:

- Critical: 24 hours
- High: 7 days
- Medium: 30 days

**Priority**: CRITICAL
**Traces To**: Principle 5

---

#### NFR-SEC-007: Service-to-Service Authentication

**Requirement**: All internal service-to-service calls MUST be mutually authenticated (mutual TLS, signed tokens, or equivalent) and authorised at the receiver.

**Priority**: CRITICAL
**Traces To**: Principle 5

---

#### NFR-SEC-008: NCSC Cyber Assessment Framework

**Requirement**: Maintain a current NCSC CAF self-assessment with a defined target profile, reviewed at least annually and on material change.

**Priority**: CRITICAL
**Traces To**: Principle 5, BR-006

---

#### NFR-SEC-009: NCSC Cloud Security Principles

**Requirement**: Maintain a current assessment against the NCSC Cloud Security Principles (14), with evidence available to tenants on request.

**Priority**: CRITICAL
**Traces To**: Principle 5, BR-006

---

### Compliance and Regulatory Requirements

#### NFR-C-001: UK GDPR / DPA 2018

**Applicable Regulations**: UK GDPR, Data Protection Act 2018.

**Compliance**:

- [x] Records of Processing Activity (ROPA) maintained
- [x] Data Subject Rights process (access, rectification, erasure, portability, restriction)
- [x] Lawful basis documented per processing activity
- [x] DPIA for material processing changes (`/arckit:dpia`)
- [x] Data breach notification within 72 hours to ICO where required
- [x] Data Protection Officer appointed and contactable

**Data Residency**: UK by default for all tenant data and backups.

**Priority**: CRITICAL
**Traces To**: Principle 7

---

#### NFR-C-002: Audit Logging and Retention

**Requirement**: Comprehensive audit trail for compliance and forensics.

**Audit Log Contents** for sensitive operations: who, what, when (UTC ms), where (component), why (correlation IDs), result (success/failure).

**Retention**:

- Security and audit logs: ≥ 12 months
- Application logs: ≥ 90 days
- Metrics: ≥ 13 months

**Log Integrity**: Tamper-evident logging.

**Priority**: CRITICAL
**Traces To**: Principle 6

---

#### NFR-C-003: Accessibility — PSBAR 2018 / WCAG 2.2 AA

**Requirement**: All tenant-facing UI MUST meet WCAG 2.2 Level AA, MUST be tested with assistive technologies, and MUST publish a current Accessibility Statement aligned with PSBAR 2018.

**Testing**: Automated accessibility checks in CI plus manual assistive-technology testing on each release.

**Priority**: CRITICAL (non-negotiable per Principle 12)
**Traces To**: Principle 12

---

#### NFR-C-004: Technology Code of Practice

**Requirement**: Maintain a current TCoP self-assessment (`/arckit:tcop`) covering all 12 points; published to tenants on request.

**Priority**: HIGH
**Traces To**: Principle 4, BR-006

---

#### NFR-C-005: GDS Service Standard

**Requirement**: Tenant-facing service MUST be assessable against the 14 points of the GDS Service Standard with evidence pack available (`/arckit:service-assessment`).

**Priority**: HIGH
**Traces To**: BR-006

---

#### NFR-C-006: ISO 27001 Alignment

**Requirement**: Information security management system aligned with ISO 27001, with a documented certification roadmap.

**Priority**: SHOULD_HAVE for v1; MUST_HAVE for GA + 18 months.
**Traces To**: Principle 5

---

#### NFR-C-007: Government Security Classifications Policy

**Requirement**: Platform supports content up to OFFICIAL with OFFICIAL-SENSITIVE handling caveats where tenants opt in. Content above OFFICIAL-SENSITIVE explicitly out of scope (rejected at the application layer).

**Priority**: CRITICAL
**Traces To**: Principle 7

---

### Usability Requirements

#### NFR-U-001: User Experience

**Requirement**: System MUST be usable by SME architects and SME founders without dedicated training.

**Standards**:

- Browser support: current and previous major versions of mainstream browsers (Chrome, Firefox, Safari, Edge)
- Responsive design covering desktop, tablet, and mobile breakpoints
- GOV.UK Design System alignment encouraged where suitable (FR-013)

**Priority**: HIGH
**Traces To**: Principle 12

---

#### NFR-U-002: Accessibility

**Requirement**: WCAG 2.2 AA conformance. See NFR-C-003.

**Features**:

- [x] Keyboard navigation for all functions
- [x] Screen reader compatibility
- [x] Sufficient colour contrast and resizable text
- [x] Alt text for non-decorative images
- [x] Captions and transcripts for audio/video content where applicable

**Priority**: CRITICAL (non-negotiable)
**Traces To**: Principle 12

---

### Maintainability and Supportability Requirements

#### NFR-M-001: Observability

**Requirement**: Comprehensive structured telemetry — logs, metrics, traces — across all services, with SLO-based alerting.

**Telemetry**:

- Structured logs with correlation and tenant IDs
- RED metrics (Rate, Errors, Duration) per service
- Distributed tracing across internal hops
- Public status page reflecting core service health

**Priority**: HIGH
**Traces To**: Principle 6

---

#### NFR-M-002: Documentation

**Requirement**: Documentation for tenants (user guides), operators (runbooks), and developers (API references), kept current within 5 working days of release.

**Priority**: HIGH
**Traces To**: Principle 15

---

#### NFR-M-003: Operational Runbooks

**Requirement**: Runbooks for deployment, rollback, backup/restore, incident response, scaling, and DR.

**Priority**: CRITICAL
**Traces To**: Principle 14, Principle 18

---

### Portability and Interoperability Requirements

#### NFR-I-001: Open API Standards

**Requirement**: All public APIs MUST publish OpenAPI 3.x specifications; events MUST publish AsyncAPI specifications; versioning with backward compatibility window ≥ 12 months.

**Priority**: MUST_HAVE
**Traces To**: Principle 4

---

#### NFR-I-002: Data Portability

**Requirement**: Tenant data exportable in open formats (Markdown / JSON / YAML), with full lineage metadata; importable from the same formats.

**Priority**: CRITICAL
**Traces To**: Principle 4, Principle 9, BR-007

---

## Integration Requirements

### INT-001: Tenant Identity Provider (SSO)

**Purpose**: Allow tenant employees to sign in via the tenant's existing identity provider.
**Integration Type**: Real-time (federation).
**Data Exchanged**: Authentication tokens, identity claims, group membership.
**Pattern**: OIDC / OAuth 2.x / SAML 2.0.
**Authentication**: OIDC / SAML.
**Error Handling**: Fallback to local credentials disabled by tenant policy; clear error messaging.
**SLA**: Authentication round-trip < 2 seconds p95.
**Owner**: Tenant identity team.
**Priority**: CRITICAL

---

### INT-002: Payment Processing

**Purpose**: Process card and direct-debit payments for paid tiers; produce VAT-compliant invoices.
**Integration Type**: Real-time API plus webhook events.
**Data Exchanged**: Subscription, invoice, payment events; no card data stored by ArcKit (PCI-DSS scope minimised).
**Pattern**: Hosted payment pages or SAQ-A-equivalent flow.
**Priority**: CRITICAL (for paid tiers); free tier requires no payment integration.

---

### INT-003: Companies House (UK SME Verification)

**Purpose**: Verify SME eligibility against authoritative UK company data.
**Integration Type**: Real-time API.
**Data Exchanged**: Company number lookup; company status, size indicators, officers.
**Authentication**: API key.
**Error Handling**: Onboarding queued and retried on outage; user notified.
**SLA**: Verification round-trip < 5 seconds p95.
**Priority**: CRITICAL
**Traces To**: BR-003, FR-001

---

### INT-004: Email Delivery

**Purpose**: Transactional and notification email (verification, invites, alerts, exports).
**Integration Type**: Outbound API.
**Pattern**: Authenticated SMTP / API; SPF, DKIM, DMARC aligned.
**Priority**: CRITICAL

---

### INT-005: AI / Large Language Model Endpoint

**Purpose**: Power AI-assisted artefact generation (UC-2, FR-004).
**Integration Type**: Real-time API.
**Pattern**: Pluggable; vendor-agnostic abstraction layer (so the underlying provider can change without API breakage).
**Data Handling**:

- No tenant data sent to the model provider beyond the user's prompt and selected project context.
- Provider must offer no-training assurance for tenant data.
- Provider must operate in the UK or an adequate jurisdiction with documented Article 46 transfer mechanism (if outside the UK and EEA).

**Priority**: HIGH (the platform is usable without AI, but AI is a primary differentiator)
**Traces To**: Principle 7, FR-004

---

### INT-006: Object Storage and Database

**Purpose**: Persistent storage for artefacts, attachments, and exports.
**Integration Type**: Vendor-managed UK-region cloud storage and database services.
**Data Handling**: UK residency; encryption at rest; tenant ID partitioning.
**Priority**: CRITICAL
**Traces To**: Principle 7

---

### INT-007: Observability Backend

**Purpose**: Centralised logs, metrics, and traces.
**Integration Type**: Outbound telemetry pipelines.
**Data Handling**: Tenant data minimisation; PII not logged; UK residency for log storage.
**Priority**: HIGH
**Traces To**: Principle 6

---

### INT-008: G-Cloud / Digital Marketplace

**Purpose**: Listing and call-off for buying authorities.
**Integration Type**: Manual listing maintenance; call-off PO acceptance in billing.
**Priority**: MUST_HAVE
**Traces To**: BR-004

---

### INT-009: Vulnerability Disclosure

**Purpose**: External researchers can report vulnerabilities (security.txt, disclosure policy aligned with ISO 29147).
**Integration Type**: Inbound channel.
**Priority**: HIGH
**Traces To**: NFR-SEC-006

---

## Data Requirements

### Data Entities

#### Entity DR-001: Tenant

**Description**: An organisational tenant of the SaaS.
**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| id | UUID | Yes | Tenant identifier | Primary key |
| name | String(255) | Yes | Tenant display name | Not null |
| companies_house_number | String(8) | Yes | UK Companies House number | Validated against API |
| sme_status | Enum | Yes | sme / non-sme / pending | Re-verified annually |
| tier | Enum | Yes | free / sme-paid / enterprise | |
| residency_region | String | Yes | UK by default | |
| classification_max | Enum | Yes | OFFICIAL / OFFICIAL-SENSITIVE | Tenant opt-in for OS |
| created_at | Timestamp | Yes | | Indexed |
| status | Enum | Yes | active / suspended / offboarding / deleted | |

**Relationships**: One-to-many with Users, Projects, Subscriptions, Audit Events.
**Data Volume**: ≤ 5,000 records at GA + 24 months.
**Data Classification**: OFFICIAL.
**Retention**: Lifetime of tenancy + grace period (FR-010), then deletion with destruction certificate.

---

#### Entity DR-002: User

**Attributes**: id (UUID), tenant_id (FK), email, name, role, mfa_enrolled (bool), last_signin_at, status.
**Data Classification**: OFFICIAL (contains PII — email, name).
**Retention**: Lifetime of user membership + 30 days post-removal.

---

#### Entity DR-003: Project

**Attributes**: id (UUID), tenant_id (FK), project_id_human (e.g., `001`), name, description, created_at, archived_at.
**Data Classification**: OFFICIAL (or OFFICIAL-SENSITIVE if tenant marks).
**Retention**: Lifetime of tenancy.

---

#### Entity DR-004: Artefact

**Attributes**: id (UUID), project_id (FK), document_id (e.g., `ARC-001-REQ-v1.0`), type, version, content (Markdown), generation_metadata (JSON: command, model, prompt, timestamp), created_by, created_at, updated_by, updated_at.
**Data Classification**: OFFICIAL by default; OFFICIAL-SENSITIVE if tenant opted in.
**Retention**: Lifetime of project; versioned history retained.
**Indexing**: By tenant + project + type for query performance.

---

#### Entity DR-005: Audit Event

**Attributes**: id, tenant_id, actor_id, action, target_type, target_id, timestamp, ip, user_agent, result, correlation_id.
**Data Classification**: OFFICIAL.
**Retention**: ≥ 12 months (NFR-C-002).
**Storage**: Tamper-evident, write-once-read-many semantics.

---

#### Entity DR-006: Subscription

**Attributes**: id, tenant_id (FK), tier, started_at, ends_at, billing_state, payment_method_token, gcloud_po_reference (nullable).
**Data Classification**: OFFICIAL (financial data).
**Retention**: 7 years (UK financial record-keeping).

---

#### Entity DR-007: SME Verification Record

**Attributes**: id, tenant_id (FK), companies_house_response (snapshot), threshold_check_result, decision, decided_at, decided_by, expires_at.
**Data Classification**: OFFICIAL.
**Retention**: 7 years (decision audit trail).

---

### Data Quality Requirements

- **Accuracy**: Companies House data refreshed at verification and at annual re-verification.
- **Completeness**: All artefacts have generation lineage if AI-generated.
- **Consistency**: Cross-artefact references (e.g., requirement IDs cited in ADRs) resolved.
- **Timeliness**: Artefact last-modified updated on every change.
- **Lineage**: Generation metadata captured per artefact.

---

### Data Migration Requirements

No legacy migration in v1. Tenants import from existing tooling via the public API or by uploading Markdown / JSON exports. A v2 importer for common EA tools may be added based on demand.

---

## Constraints and Assumptions

### Technical Constraints

**TC-1**: Hosting region MUST be the United Kingdom (Principle 7).
**TC-2**: AI model provider MUST offer no-training assurance for tenant data and operate in the UK or an adequate jurisdiction with documented Article 46 transfer mechanism.
**TC-3**: Platform MUST not require any specific cloud provider in its public commitments — vendor selection is recorded in ADRs (`/arckit:adr`) and may change.
**TC-4**: Maximum classification handled is OFFICIAL-SENSITIVE; anything higher is rejected at the application layer (TC enforced by validation).

### Business Constraints

**BC-1**: SME free tier MUST be sustainable from cross-subsidy revenue without external funding within 24 months of GA (BR-005).
**BC-2**: Service MUST be listed on G-Cloud at GA (BR-004).
**BC-3**: No paywall on governance-critical features (Principle 1).

### Assumptions

**A-1**: Companies House public API remains available with comparable terms.
**A-2**: Cross-subsidy uptake from large-enterprise tier reaches the documented break-even threshold within 18 months of GA.
**A-3**: AI inference costs continue their downward trend or stabilise.
**A-4**: UK Government policy around SME procurement (Procurement Act 2023, SME Action Plans) remains broadly stable.

**Validation Plan**: Assumptions reviewed quarterly; changes that invalidate assumptions trigger a re-baseline of the SOBC.

---

## Success Criteria and KPIs

### Business Success Metrics

| Metric | Baseline | Target | Timeline | Measurement Method |
|--------|----------|--------|----------|-------------------|
| Verified SME tenants onboarded | 0 | ≥ 200 | GA + 12 months | Tenant register |
| SME paid tier rolling 90-day retention | n/a | ≥ 70% | GA + 6 months | Subscription analytics |
| Free tier activation (≥ 3 artefacts in 30 days) | n/a | ≥ 60% | GA + 6 months | Product analytics |
| Cross-subsidy break-even | Loss | Break-even | GA + 18 months | Finance |
| Buying-authority callouts via G-Cloud | 0 | ≥ 25 | GA + 12 months | CCS data |

### Technical Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Availability (rolling 30-day) | ≥ 99.9% | External synthetic monitoring |
| API p95 latency (read) | < 200 ms | APM |
| Error rate (5xx) | < 0.1% | Log aggregation |
| Mean time to recovery (MTTR) | < 60 minutes | Incident records |
| WCAG 2.2 AA conformance issues | 0 critical | Automated + manual a11y testing |
| Critical vulnerabilities open > 24 hours | 0 | Vulnerability tracking |

### User Adoption Metrics

| Metric | Target | Timeline | Measurement Method |
|--------|--------|----------|-------------------|
| Active tenants per month | 1,000 | GA + 12 months | Product analytics |
| Average artefacts per active tenant per month | ≥ 5 | GA + 6 months | Product analytics |
| Tenant satisfaction (CSAT) | ≥ 8 / 10 | Ongoing | In-product survey |
| Public NPS | ≥ 30 | GA + 12 months | Annual survey |

---

## Dependencies and Risks

### Dependencies

| Dependency | Description | Owner | Target Date | Status | Impact if Delayed |
|------------|-------------|-------|-------------|--------|-------------------|
| Stakeholder Analysis | `/arckit:stakeholders` to validate stakeholder placeholders | Service Owner | 2026-05-31 | At Risk | HIGH |
| SOBC | `/arckit:sobc` to validate cross-subsidy economics | Service Owner | 2026-06-30 | Not Started | HIGH |
| Risk Register | `/arckit:risk` to formalise risks | Lead Architect | 2026-06-15 | Not Started | MEDIUM |
| G-Cloud listing window | Next G-Cloud framework iteration | CCS liaison | TBD | Not Started | HIGH |
| AI provider selection | ADR for AI endpoint provider | Lead Architect | 2026-07-15 | Not Started | MEDIUM |

### Risks (indicative — formal register pending `/arckit:risk`)

| Risk ID | Description | Probability | Impact | Mitigation Strategy | Owner |
|---------|-------------|-------------|--------|---------------------|-------|
| R-1 | Cross-subsidy fails to reach break-even within 18 months, forcing paywall introduction that breaches Principle 1 | MEDIUM | HIGH | Quarterly affordability review; large-enterprise sales targets; lever to adjust free-tier limits before paywalling features | Service Owner |
| R-2 | AI inference cost per generation grows faster than tenant willingness to pay | MEDIUM | MEDIUM | Per-tenant generation quotas; pluggable AI provider; cheaper-model fallback | Lead Architect |
| R-3 | Cross-tenant defect leaks data between tenants | LOW | CRITICAL | Defence in depth: tenant ID propagation, default-deny, automated isolation tests, external pen testing, blast-radius monitoring | Security Lead |
| R-4 | Companies House API change breaks SME verification | LOW | MEDIUM | Defensive parsing; manual fallback; monitor Companies House change notices | Lead Architect |
| R-5 | UK GDPR / DPA enforcement action over a sub-processor outside the UK | LOW | HIGH | Sub-processor list reviewed annually; UK-resident default; Article 46 mechanisms documented | DPO |
| R-6 | Accessibility regression after a UI release | MEDIUM | MEDIUM | Automated a11y in CI; manual AT testing every release; rollback on regression | Accessibility Lead |
| R-7 | G-Cloud listing missed at next framework iteration | MEDIUM | HIGH | Engage CCS liaison early; treat listing as a first-class GA dependency | CCS liaison |

---

## Requirement Conflicts & Resolutions

> Source: derived from Principles document `ARC-000-PRIN-v2.0.md` (no STKE conflict analysis available yet — to be revalidated after `/arckit:stakeholders`).

### Conflict C-1: Free Tier Generosity vs Cost Sustainability

**Conflicting Requirements**:

- **Requirement A**: BR-001 (free tier genuinely usable for end-to-end work, no governance-critical paywalls).
- **Requirement B**: BR-005 (cross-subsidy must reach break-even within 18 months, NFR-S-001 scaling without breaching unit economics).

**Stakeholders Involved**:

- **Service Owner / Sponsor**: Wants Requirement A — strategic mandate (Principle 1).
- **Finance** (placeholder): Wants Requirement B — sustainability of the offering.

**Nature of Conflict**: A genuinely usable free tier consumes compute and AI inference per tenant; without disciplined limits or fast cross-subsidy growth, the free tier creates a financial liability that ultimately forces it to close — destroying the value of Principle 1.

**Trade-off Analysis**:

| Option | Pros | Cons |
|--------|------|------|
| **Option 1**: Generous limits, accept 12+ months runway | ✅ Maximum SME adoption; ✅ honours Principle 1 cleanly | ❌ Financial risk; ❌ need external runway |
| **Option 2**: Tight limits to control cost | ✅ Predictable unit economics | ❌ Free tier fails real-delivery threshold; ❌ violates Principle 1 |
| **Option 3 (chosen)**: Honour governance-critical features without limit; meter AI generation and bulk-export capacity per tenant; refine quotas annually | ✅ Honours Principle 1 (governance features); ✅ AI cost (the most variable line) is bounded; ✅ refinable lever | ❌ Some perceived friction on AI generation; ❌ requires ongoing FinOps discipline |
| **Option 4**: Time-limited generous free tier (e.g., 12 months) | ✅ Bounded cost exposure | ❌ Trial-style violates Principle 1 explicitly |

**Resolution Strategy**: COMPROMISE.
**Decision**: Option 3 — governance features unlimited and unpaywalled on free tier; AI generation and bulk-export metered per tenant; per-tenant cost-to-serve measured and quotas reviewed annually as part of the affordability review (BR-002, BR-005).
**Rationale**: Principle 1 is non-negotiable for governance features but does not require unlimited AI inference. AI cost is the dominant variable; metering it preserves cost discipline without breaching the principle.
**Decision Authority**: Service Owner (per project RACI when STKE is run).
**Impact on Requirements**: FR-004 acceptance criteria include per-tenant quotas; NFR-P-002 measured under quota.
**Stakeholder Management**: Finance commitment to publish unit economics quarterly; Service Owner commitment to act on overruns.

---

### Conflict C-2: AI Provider Cost Optimisation vs Open-Standards Pluggability

**Conflicting Requirements**:

- **Requirement A**: NFR-S-001 / FinOps (concentrate on a single AI provider for volume discounts, simpler operations).
- **Requirement B**: Principle 4 / INT-005 (pluggable AI endpoint, no vendor lock-in, alignment with Open Standards).

**Stakeholders Involved**:

- **Lead Architect**: Wants pluggability for portability and future-sovereign reuse.
- **Finance**: Wants concentration for cost.

**Nature of Conflict**: A pluggable abstraction adds engineering cost and may forgo volume-discount opportunities; sole-source concentration creates lock-in that contradicts Principle 4 and undermines future sovereign-deployment reuse.

**Trade-off Analysis**:

| Option | Pros | Cons |
|--------|------|------|
| **Option 1**: Single provider hard-coded | ✅ Simple; ✅ best discount | ❌ Vendor lock-in; ❌ cannot reuse for sovereign |
| **Option 2**: Fully pluggable, multiple live providers in production | ✅ Maximum optionality | ❌ Operational complexity; ❌ no volume discount |
| **Option 3 (chosen)**: Pluggable abstraction layer; one default provider for the SaaS; alternative provider tested in CI; provider switchable in days | ✅ Avoids lock-in; ✅ retains volume discount; ✅ supports future sovereign reuse | ❌ Modest engineering investment in abstraction |

**Resolution Strategy**: INNOVATE (abstraction satisfies both).
**Decision**: Option 3 — implement pluggable abstraction; commercial concentration on one provider for the SaaS; second provider validated in CI quarterly to keep the abstraction honest.
**Rationale**: Aligns SaaS with Principle 4 and de-risks sovereign reuse without sacrificing SaaS economics.
**Impact on Requirements**: INT-005 specifies pluggable abstraction; FR-004 records provider in generation metadata.

---

### Conflict C-3: Tenant Self-Service Speed vs Strong SME Verification

**Conflicting Requirements**:

- **Requirement A**: UC-1 self-service onboarding (target completion in minutes).
- **Requirement B**: BR-003 SME eligibility verification (Companies House check, threshold check, audit retention 7 years).

**Stakeholders Involved**:

- **SME Founder / Bid Lead persona**: Wants frictionless onboarding.
- **Service Owner / Compliance**: Wants verifiable eligibility.

**Nature of Conflict**: Verification adds latency and possible failure modes (Companies House outages, ambiguous matches) that may push onboarding beyond the user's tolerance.

**Trade-off Analysis**:

| Option | Pros | Cons |
|--------|------|------|
| **Option 1**: Self-attest only, verify later | ✅ Fast | ❌ Cross-subsidy at risk; ❌ low audit defensibility |
| **Option 2**: Full verification before any access | ✅ Best controls | ❌ Onboarding time can exceed tolerance during outages |
| **Option 3 (chosen)**: Synchronous verification with graceful degradation; on outage, provisional access on free tier with verification within 24 hours; audit retention preserved | ✅ Fast in normal path; ✅ resilient on outage; ✅ audit preserved | ❌ Provisional state requires careful UX |

**Resolution Strategy**: PHASE / INNOVATE.
**Decision**: Option 3 — see UC-1 alternative flow.
**Impact on Requirements**: FR-001 acceptance criteria include outage path and provisional state limits.

---

## Timeline and Milestones

| Milestone | Description | Target Date | Dependencies |
|-----------|-------------|-------------|--------------|
| Stakeholder analysis | `/arckit:stakeholders` validates stakeholder set | 2026-05-31 | This document |
| Requirements approval | Stakeholder sign-off on this document | 2026-06-15 | Stakeholders, SOBC draft |
| SOBC | Strategic Outline Business Case | 2026-06-30 | This document |
| HLD | High-Level Design | 2026-08-15 | Requirements, Principles |
| Alpha | Internal alpha environment | 2026-10-31 | HLD |
| Private Beta | Selected SME tenants | 2027-01-31 | Alpha |
| GA | Public availability + G-Cloud listing | 2027-04-30 | Beta |

---

## Budget

> ⚠️ Indicative only — to be replaced by `/arckit:sobc` figures.

### Cost Estimate (one-off, indicative)

| Category | Estimated Cost | Notes |
|----------|----------------|-------|
| Development | TBD via SOBC | FTE count and duration to be confirmed |
| Infrastructure (build) | TBD | UK-region cloud, multi-AZ |
| Third-party services | TBD | AI inference, payments, email |
| Testing | TBD | Performance, security, accessibility |
| Training | TBD | User onboarding content |
| **Total** | TBD | |

### Ongoing Operational Costs (annual, indicative)

| Category | Annual Cost | Notes |
|----------|-------------|-------|
| Infrastructure | TBD | Scales with tenants per NFR-S-001 |
| Licences | TBD | Tooling and observability |
| Support and on-call | TBD | 24/7 on-call from GA |
| AI inference | TBD | Largest variable — see Conflict C-1 |
| **Total** | TBD | |

---

## Approval

| Reviewer | Role | Status | Date | Comments |
|----------|------|--------|------|----------|
| [PENDING] | Service Owner | [ ] Approved | [PENDING] | |
| [PENDING] | Lead Architect | [ ] Approved | [PENDING] | |
| [PENDING] | Security Lead / SIRO | [ ] Approved | [PENDING] | |
| [PENDING] | DPO | [ ] Approved | [PENDING] | |
| [PENDING] | Accessibility Lead | [ ] Approved | [PENDING] | |
| [PENDING] | CCS liaison | [ ] Approved | [PENDING] | |

---

## Appendices

### Appendix A: Glossary

- **CAF** — NCSC Cyber Assessment Framework
- **CCS** — Crown Commercial Service
- **DPIA** — Data Protection Impact Assessment
- **DPO** — Data Protection Officer
- **EA** — Enterprise Architecture
- **GA** — General Availability
- **GDS** — Government Digital Service
- **NCSC** — National Cyber Security Centre
- **PSBAR 2018** — Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018
- **ROPA** — Records of Processing Activity (UK GDPR Art. 30)
- **SaaS** — Software as a Service
- **SAML** — Security Assertion Markup Language
- **SbD** — Secure by Design
- **SIRO** — Senior Information Risk Owner
- **SLO / SLI** — Service Level Objective / Indicator
- **SME** — Small and Medium Enterprise
- **SOBC** — Strategic Outline Business Case
- **SSO** — Single Sign-On
- **TCoP** — Technology Code of Practice
- **WCAG** — Web Content Accessibility Guidelines

### Appendix B: Reference Documents

- `projects/000-global/ARC-000-PRIN-v2.0.md` — Architecture Principles (current)
- UK Government Technology Code of Practice (12 points)
- GDS Service Standard (14 points)
- NCSC Cyber Assessment Framework
- NCSC Cloud Security Principles (14)
- UK GDPR / Data Protection Act 2018
- Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018
- Procurement Act 2023
- HMG Government Security Classifications Policy

### Appendix C: Wireframes and Mockups

To be produced post-HLD.

### Appendix D: Data Models

To be produced via `/arckit:data-model` after this document is approved.

---

## External References

> No external policy documents were placed in `projects/001-arckit-saas/external/` at the time of generation. UK Government policies referenced are public-domain and cited by name. Place authoritative copies in the project's `external/` folder and re-run `/arckit:requirements` to embed inline citations.

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
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Derived from `ARC-000-PRIN-v2.0.md` (architecture principles). Stakeholder analysis (STKE), SOBC, and risk register not yet generated — flagged for follow-up.
