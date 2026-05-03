# ArcKit as a Service — Enterprise Architecture Principles

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:principles`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-000-PRIN-v2.0 |
| **Document Type** | Architecture Principles |
| **Project** | ArcKit as a Service (Project 000) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 2.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Annual |
| **Next Review Date** | 2027-05-03 |
| **Owner** | Mark Craddock, ArcKit as a Service Owner |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | ArcKit as a Service team, UK SME tenants, Crown Commercial Service, GDS, CDDO, MOD Defence Digital |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:principles` command, scoped to ArcKit as a Service for UK SMEs supplying government services | PENDING | PENDING |
| 2.0 | 2026-05-03 | ArcKit AI | Major: introduced dual deployment model. Added Principle 21 (Sovereign and Air-Gapped Deployment) to support MOD and sensitive sites. Updated Principles 1, 5, 7, 8 to reflect managed-SaaS vs sovereign-deployment split. Extended classification scope and added MOD Secure by Design / JSP 440 alignment. | PENDING | PENDING |

---

## Executive Summary

This document establishes the immutable principles governing all technology architecture decisions for **ArcKit as a Service** — a managed, multi-tenant offering of the ArcKit enterprise architecture governance toolkit, designed for UK public sector adoption and, critically, for **Small and Medium Enterprises (SMEs) supplying government services**.

ArcKit as a Service operates under a **dual deployment model**:

1. **Managed SaaS** (default) — multi-tenant, UK-resident managed service supporting work up to OFFICIAL and OFFICIAL-SENSITIVE handling caveats. This is the route that delivers the SME-affordable pricing in Principle 1.
2. **Sovereign Deployment** — the same codebase deployable into customer-controlled environments (including MOD and other sensitive sites), supporting disconnected and air-gapped operation, formal accreditation, and higher classifications subject to that accreditation. See Principle 21.

These principles ensure consistency, security, accessibility, scalability and alignment with UK Government policy (GDS Service Standard, Technology Code of Practice, NCSC Cyber Assessment Framework, Cloud Security Principles, G-Cloud, MOD Secure by Design / JSP 440) across both deployment modes.

**Scope**: All technology decisions for the ArcKit as a Service platform, its tenant-facing services, supporting infrastructure, integrations, and sovereign deployment artefacts.
**Authority**: ArcKit Architecture Review Board.
**Compliance**: Mandatory unless an exception is approved (see §VI Exception Process).

**Philosophy**: These principles are **technology-agnostic**. They describe WHAT qualities the architecture must have, not HOW to implement them with specific products. Specific technology selection happens during research and design phases (`/arckit:research`, `/arckit:aws-research`, etc.) guided by these principles.

**Foundational commercial commitment**: ArcKit as a Service exists to lower the cost of doing high-quality architecture for **SMEs supplying UK government**. Pricing, packaging, and platform decisions for the **managed SaaS** MUST keep the entry tier free or substantially cheaper than commercial equivalents for in-scope SMEs (see Principle 1). The sovereign deployment route is a separate commercial model addressing a fundamentally different customer profile (see Principle 21).

---

## I. Strategic Principles

### 1. Equitable Access for SMEs Supplying Government

**Principle Statement**:
The **managed SaaS** offering of ArcKit as a Service MUST be free or substantially cheaper than commercial equivalents for verified Small and Medium Enterprises (SMEs) supplying or seeking to supply UK government services. Pricing, feature gating, and capacity allocation for the managed SaaS MUST NOT erect barriers that disadvantage SMEs relative to large incumbents. The sovereign deployment offering (Principle 21) is a separate commercial model and is not in scope of this affordability commitment.

**Rationale**:
The UK Government has a stated ambition to spend more with SMEs (Procurement Act 2023, SME Action Plans, the £1 in every £3 SME spend target). SMEs typically lack the in-house enterprise architecture capability that larger system integrators take for granted, and commercial EA tooling is priced for enterprises. A managed ArcKit service reduces that capability gap and supports a more diverse, competitive supplier base for the public sector. If pricing replicates the commercial market, the service fails its primary purpose.

**Implications**:

- A free entry tier MUST exist on the managed SaaS that is genuinely usable for end-to-end government work — not a marketing trial — covering the essential ArcKit baseline (principles, requirements, ADRs, diagrams, traceability) for at least one active engagement.
- SME eligibility MUST be verifiable against a transparent, published definition (default: UK definition aligned with the Companies Act 2006 SME thresholds and Crown Commercial Service guidance, subject to legal review).
- Paid SaaS tiers MUST be priced on a cost-recovery or modest-margin basis for verified SMEs, with transparent published list prices.
- Feature gating between free and paid tiers MUST NOT remove governance-critical functions (security, audit log export, data export, accessibility) from the free tier.
- Capacity, support, and rate limits on the free tier MUST be sufficient for genuine delivery work, sized against typical SME engagement profiles (defined and reviewed annually).
- Cross-subsidy is acceptable: large-enterprise, non-SME, and sovereign-deployment customers MAY be charged at higher rates to fund the SME tier, provided this is transparent.
- Procurement routes MUST include G-Cloud listing so that buying authorities can call off the service without bespoke procurement.

**Validation Gates**:

- [ ] Published SME eligibility policy with verification process
- [ ] Free tier covers the essential ArcKit baseline for at least one project end-to-end
- [ ] Paid tier list prices published openly (no "contact sales" gating for SMEs)
- [ ] Annual affordability review against comparator commercial EA tooling published
- [ ] No governance-critical feature is paywalled away from the free tier
- [ ] Service listed on G-Cloud with SME-friendly minimum commitment terms

**Example — Good**:
Free tier permits unlimited principles, ADRs, requirements and diagrams for one active project, with full export. Paid SME tier (≤ £X / user / month, published) adds multi-project workspaces and SSO. Large-enterprise tier and sovereign-deployment licences fund the SME tier through higher per-seat rates.

**Example — Bad**:
Free tier capped at 5 documents and 30 days, after which projects become read-only. Audit log export only on the £15k/year enterprise plan. SSO only via "contact sales".

**Common Violations to Avoid**:

- Trial-style free tiers that expire and force conversion mid-engagement
- Paywalling export, audit, accessibility, or security controls
- Hidden enterprise pricing that disadvantages SMEs in competitive bids
- Capacity throttling that makes the free tier impractical for real delivery

---

### 2. Scalability and Elasticity

**Principle Statement**:
The platform MUST scale horizontally to meet aggregate tenant demand and MUST dynamically adjust capacity based on load without manual intervention. Sovereign deployments (Principle 21) MUST scale within their fixed, customer-provisioned infrastructure envelope.

**Rationale**:
Demand on the managed SaaS is multi-tenant and variable. Sovereign deployments operate inside fixed capacity envelopes set at procurement; horizontal scaling within that envelope must still be achievable without re-architecture.

**Implications**:

- Stateless application components, replicable across compute nodes
- No hard-coded tenant, document, or user limits in the runtime
- Distributed deployment across multiple availability zones (managed SaaS) or across redundant nodes within a single site (sovereign)
- Load balancing and auto-scaling driven by demand metrics
- Cost model accounts for variable capacity (see also Principle 17, FinOps)
- Per-tenant fair-use limits enforced separately from platform capacity limits

**Validation Gates**:

- [ ] System demonstrably scales horizontally (add more instances)
- [ ] No single points of failure constrain scaling
- [ ] Load testing demonstrates capacity growth in line with added resources
- [ ] Auto-scaling triggers and metrics defined and tested
- [ ] Cost model accounts for variable capacity
- [ ] Sovereign deployment scaling validated within representative fixed-capacity envelope

---

### 3. Resilience and Fault Tolerance

**Principle Statement**:
The platform MUST gracefully degrade when dependencies fail and MUST recover automatically without data loss or manual intervention.

**Rationale**:
Tenants depend on the platform during live procurement and assurance windows where downtime is materially harmful. Failures are inevitable — design for them rather than for perfect reliability.

**Implications**:

- Circuit breakers, timeouts, and retry-with-backoff on all external dependencies
- Graceful degradation when non-critical services fail (e.g., AI generation degraded but read/edit still available)
- Automated health checks and failover
- Bulkhead isolation between tenants to prevent noisy-neighbour cascades
- Defined Recovery Time Objective (RTO) and Recovery Point Objective (RPO) per service
- Sovereign deployments MUST function fully when disconnected from external networks (no hard dependency on internet-only services)

**Validation Gates**:

- [ ] Failure modes identified and mitigated
- [ ] Chaos / fault-injection testing performed at least quarterly
- [ ] RTO and RPO defined per service, evidenced by recovery testing
- [ ] Automated failover tested
- [ ] Degraded-mode behaviour documented and visible to tenants
- [ ] Disconnected / air-gapped operation validated for sovereign deployments

---

### 4. Open Standards and Interoperability

**Principle Statement**:
All tenant-facing functionality MUST be exposed through well-defined, versioned interfaces using open, industry-standard protocols and data formats. Direct database access across system boundaries is prohibited. Tenant data MUST be exportable in open formats with no licensing encumbrance.

**Rationale**:
The Technology Code of Practice (TCoP) and the GDS Service Standard require open standards and the avoidance of vendor lock-in. SMEs in particular depend on portability: a tenant must be able to leave the service and continue their architecture work elsewhere. Sovereign deployment customers depend on the same open formats so that they can operate the platform independently and exit without proprietary data extraction.

**Implications**:

- HTTP APIs documented with OpenAPI; events documented with AsyncAPI
- Versioning strategy with backward compatibility windows of at least 12 months
- Tenant content stored in open, human-readable formats (e.g., Markdown, JSON, YAML) — never proprietary binary blobs
- Full-fidelity export of all tenant artifacts on demand, without paywall
- No direct database coupling across system boundaries
- Authentication via standard protocols (OIDC / OAuth 2.x / SAML 2.0)
- Sovereign deployments use the same data formats and APIs as managed SaaS — no fork, no proprietary divergence

**Validation Gates**:

- [ ] OpenAPI / AsyncAPI specifications published for all public interfaces
- [ ] Versioning and deprecation policy published
- [ ] Tenant export covers 100% of their content in open formats
- [ ] Authentication uses standard protocols
- [ ] No cross-system database coupling
- [ ] Sovereign and managed deployments produce byte-compatible exports for the same content

---

### 5. Security by Design (NON-NEGOTIABLE)

**Principle Statement**:
The platform MUST implement defence-in-depth security with zero-trust principles, aligned to the NCSC Cyber Assessment Framework (CAF) and Cloud Security Principles for the managed SaaS, and to MOD Secure by Design / JSP 440 (and any site-specific Security Aspects Letter) for sovereign deployments at MOD or comparable sensitive sites. Security is a foundational requirement, not a feature to be added later.

**Rationale**:
Tenant data includes architecture artefacts that, in aggregate, describe how government services are designed. Even at OFFICIAL classification, this data is sensitive and a target. At OFFICIAL-SENSITIVE and above — the typical scope of sovereign deployments at MOD and sensitive sites — a breach has materially greater consequences. The security baseline MUST be sufficient for the highest classification each deployment is accredited to handle.

**Zero Trust Pillars**:

1. **Identity-Based Access** — no network-based trust; every request authenticated and authorised
2. **Least Privilege** — minimum necessary permissions, time-boxed where possible
3. **Encryption Everywhere** — data encrypted in transit and at rest using current, industry-standard algorithms (and, for MOD/sensitive deployments, algorithms and key-management appropriate to the accredited classification)
4. **Continuous Verification** — monitor, log, and analyse all access patterns

**Mandatory Controls (all deployments)**:

- [ ] Multi-factor authentication for all human access (tenant users and operators)
- [ ] Service-to-service authentication via mutual TLS, signed tokens, or equivalent
- [ ] Secrets in a secure vault — never in code, config files, or container images
- [ ] Network segmentation with minimal trust zones
- [ ] Encryption at rest for all tenant data and backups
- [ ] Encrypted transport for all network communication (current cryptographic standards, no deprecated ciphers)
- [ ] Structured logging of all authentication and authorisation events
- [ ] Independent penetration testing at least annually and on material change
- [ ] Vulnerability scanning of dependencies and container images on every build
- [ ] Tenant isolation enforced at storage, compute, and identity layers

**Additional Mandatory Controls (Sovereign / MOD / sensitive deployments)**:

- [ ] Compliance with the site Security Aspects Letter (SAL) and applicable JSP 440 controls
- [ ] Cleared-personnel-only access where required by the deploying authority
- [ ] Cryptographic primitives appropriate to accredited classification (HMG-approved where mandated)
- [ ] No outbound calls to internet services from within the accredited boundary
- [ ] Supply-chain integrity evidence for every artefact entering the boundary (signed builds, SBOM, hash manifests)
- [ ] Formal risk assessment and accreditation by the deploying authority before go-live

**Compliance Frameworks**:

- NCSC Cyber Assessment Framework (CAF) — target profile defined and assessed (managed SaaS)
- NCSC Cloud Security Principles (14 principles) — assessed and evidenced (managed SaaS)
- MOD Secure by Design / JSP 440 / JSP 604 — assessed for sovereign MOD deployments
- ISO 27001 alignment with a formal certification roadmap
- UK GDPR / Data Protection Act 2018 (see Principle 7)

**Exceptions**: None. Specific control implementations may vary with documented compensating controls, evidenced through the deploying authority's accreditation process where applicable.

**Validation Gates**:

- [ ] Threat model completed and reviewed
- [ ] NCSC CAF self-assessment current within 12 months (managed SaaS)
- [ ] MOD Secure by Design assessment evidenced for each sovereign MOD deployment
- [ ] Penetration test report and remediation plan current
- [ ] Incident response runbook tested at least annually
- [ ] Tenant isolation verified by automated and manual testing

---

### 6. Observability and Operational Excellence

**Principle Statement**:
All services MUST emit structured telemetry (logs, metrics, traces) sufficient for real-time monitoring, troubleshooting, capacity planning, and tenant-facing transparency. Sovereign deployments MUST emit telemetry to a customer-controlled destination — never to a vendor-controlled endpoint outside the accredited boundary.

**Rationale**:
We cannot operate, secure, or scale what we cannot observe. Tenants — particularly SMEs without their own SRE function — also need visibility into the service status that affects them. Sovereign customers must retain full custody of operational telemetry; exfiltration to a vendor-controlled SaaS observability backend is not acceptable inside an accredited boundary.

**Telemetry Requirements**:

- **Logging** — structured logs with correlation IDs and tenant IDs
- **Metrics** — request volume, latency percentiles (p50, p95, p99), error rates, saturation
- **Tracing** — distributed trace context across all internal hops
- **Public status** — externally visible status page covering core tenant-facing services (managed SaaS); sovereign deployments expose status to authorised internal users only

**Required Instrumentation**:

- Request volume, latency distribution, error rate per service
- Resource utilisation (CPU, memory, I/O, network)
- Tenant-level activity and consumption metrics (for FinOps and fair-use, managed SaaS)
- Security events (auth failures, policy violations, suspicious patterns)

**Log Retention**:

- Security and audit logs — at least 12 months, longer where regulation or accreditation requires
- Application logs — at least 90 days for troubleshooting
- Metrics — at least 13 months to support year-on-year comparison

**Validation Gates**:

- [ ] Logs, metrics, and traces instrumented for all services
- [ ] Dashboards and alerts configured with actionable runbooks
- [ ] Service Level Objectives (SLOs) and Service Level Indicators (SLIs) defined
- [ ] Public status page in place for managed SaaS and updated automatically
- [ ] Sovereign deployments configurable to emit telemetry only to customer-controlled destinations
- [ ] Capacity-planning metrics tracked

---

## II. Data Principles

### 7. Data Sovereignty, Residency, and Governance (UK Context)

**Principle Statement**:
For the managed SaaS, tenant data MUST be stored and processed in the United Kingdom by default. Cross-border processing MUST have explicit tenant consent and a documented legal basis. For sovereign deployments, data residency, sovereignty, classification, and retention MUST be controlled by the deploying authority within their accredited environment. Across both modes the platform MUST comply with UK GDPR, the Data Protection Act 2018, and the Government Security Classifications Policy.

**Data Classification**:

- **Managed SaaS** — supports work up to OFFICIAL and OFFICIAL-SENSITIVE handling caveats where tenants opt in.
- **Sovereign deployment** — supports up to the highest classification permitted by the deploying authority's accreditation, which may include OFFICIAL-SENSITIVE and (subject to formal accreditation by the deploying authority) higher classifications. Anything above OFFICIAL is out of scope of the managed SaaS.

**Data Residency**:

- Managed SaaS — default UK region for all tenant data, backups, and replicas.
- Cross-border processing on the managed SaaS only with explicit per-tenant consent and a documented Article 46 transfer mechanism.
- Sub-processors disclosed for the managed SaaS, located preferentially in the UK or adequate jurisdictions, and reviewed annually.
- Sovereign deployments — residency controlled entirely by the deploying authority. The vendor has no remote access to tenant data unless contractually agreed and accredited.

**Data Retention**:

- Tenant content retained for the lifetime of the tenancy plus a documented grace period (managed SaaS); retention controlled by the deploying authority for sovereign deployments.
- Automatic deletion after tenancy ends, with verifiable destruction evidence.
- Backup retention aligned with RPO and regulatory or accreditation requirements.
- Legal hold process available.

**Validation Gates**:

- [ ] Default UK residency for all managed-SaaS tenant data
- [ ] Data classification recorded for every data store
- [ ] Sub-processor list published and current (managed SaaS)
- [ ] Retention and deletion automated, with deletion certificates available to tenants
- [ ] UK GDPR Records of Processing Activity (ROPA) maintained
- [ ] Sovereign deployments demonstrably operate without vendor access to tenant data unless explicitly accredited

---

### 8. Tenant Isolation and Single Source of Truth

**Principle Statement**:
On the managed SaaS, every tenant's data MUST be logically isolated such that no tenant can read, write, infer, or exhaust another tenant's data or capacity. Sovereign deployments MAY operate in single-tenant mode, in which case isolation is between users, projects, and security communities within the deploying authority. Each data domain MUST have a single authoritative source, with derived copies clearly labelled and synchronised.

**Rationale**:
Multi-tenancy is the commercial enabler for the SME-affordable pricing in Principle 1. It is also the largest source of platform risk: one cross-tenant defect destroys trust for all tenants. Sovereign deployments collapse this risk surface to a single tenant but raise a different one — within-tenant project, role, and community-of-interest separation — which must still be enforced rigorously. A single source of truth prevents the reconciliation drift that becomes acute at scale.

**Implications**:

- Tenant ID propagated on every request and enforced at every storage and compute boundary (managed SaaS)
- Project, role, and community-of-interest separation enforced within sovereign deployments
- Authorisation checks fail closed — default-deny at every layer
- Per-tenant resource quotas to prevent noisy-neighbour exhaustion (managed SaaS)
- System of record identified for each data entity; derived stores read-only and labelled
- Automated tests verifying isolation on every release
- No bidirectional synchronisation without an explicit conflict-resolution strategy

**Validation Gates**:

- [ ] Tenant isolation tested in CI on every change (managed SaaS)
- [ ] Within-deployment isolation between projects/roles/communities tested for sovereign mode
- [ ] Per-tenant quotas configured and enforced (managed SaaS)
- [ ] System of record identified for each entity
- [ ] Derived copies documented with sync frequency
- [ ] Cross-tenant access scenarios proven impossible by automated test

---

### 9. Data Quality, Lineage, and Tenant Portability

**Principle Statement**:
Tenant artefacts MUST be of provable quality and end-to-end lineage, and MUST be exportable by the tenant at any time in open, machine-readable formats with no degradation.

**Rationale**:
ArcKit produces governance artefacts that downstream consumers (tenants, government buyers, assurance bodies) rely on. Quality and lineage make the artefacts trustworthy. Portability honours the open-standards principle and prevents lock-in — and it is a precondition for sovereign deployments, which require the customer to be able to operate independently of the vendor.

**Quality Standards**:

- **Completeness** — required fields populated, validated against the artefact's quality checklist
- **Consistency** — cross-artefact references resolve (e.g., requirements referenced in ADRs exist)
- **Accuracy** — generation source, model, and prompt recorded; AI outputs flagged as such
- **Timeliness** — last-modified and review-cycle metadata maintained automatically

**Lineage Requirements**:

- Source-to-target mapping documented for all derived artefacts
- Generation metadata (command, version, model) recorded on every artefact
- Audit trail of edits with author and timestamp
- Tenant export delivers the full artefact set plus lineage metadata

**Validation Gates**:

- [ ] Automated quality checks run on artefact creation and update
- [ ] Lineage metadata captured and queryable by the tenant
- [ ] One-click full export available without paywall
- [ ] Schema evolution strategy documented

---

## III. Integration Principles

### 10. Loose Coupling

**Principle Statement**:
Internal services and external integrations MUST be loosely coupled through published, versioned interfaces. No shared databases, shared file systems, or tight runtime dependencies across service or tenant boundaries.

**Rationale**:
Loose coupling enables independent deployment, technology diversity, team autonomy, and the safe evolution of the platform without breaking tenants or sovereign customers.

**Implications**:

- Communicate via APIs or asynchronous events, not shared tables
- Each service owns its data store
- Shared libraries kept minimal — favour duplication over coupling
- No distributed transactions across service boundaries
- Tenants can use any subset of the API without depending on the UI

**Validation Gates**:

- [ ] No shared mutable state across services
- [ ] Services deploy independently
- [ ] Interface changes versioned with deprecation notice
- [ ] No cross-service database coupling

---

### 11. Asynchronous Communication

**Principle Statement**:
Non-real-time interactions SHOULD use asynchronous patterns (events, queues) to improve resilience and decoupling. Asynchronous patterns chosen MUST be implementable both in managed SaaS and within disconnected sovereign deployments.

**When to Use Async**:

- Long-running generations (AI document creation, large exports)
- Notifications and pub/sub
- Integration with unreliable or slow external systems
- Background processing (lineage, indexing, scans)

**When Synchronous Is Acceptable**:

- Real-time user interactions requiring immediate feedback
- Read-only, idempotent queries
- Transactions requiring immediate consistency

**Validation Gates**:

- [ ] Async patterns used for non-real-time flows
- [ ] Message durability and delivery guarantees defined
- [ ] Event schemas versioned and published
- [ ] Dead-letter queues and retry policies in place
- [ ] Message broker choice supports on-premise / disconnected operation for sovereign deployments

---

## IV. Quality Attributes

### 12. Accessibility (NON-NEGOTIABLE for Public Sector)

**Principle Statement**:
All tenant-facing user interfaces MUST meet WCAG 2.2 Level AA as a minimum, MUST be tested with assistive technologies, and MUST publish an up-to-date Accessibility Statement aligned with the Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018.

**Rationale**:
The platform is intended for public sector use and SMEs supplying public sector services; accessibility is a legal obligation for those use cases (PSBAR 2018) and a baseline expectation under the GDS Service Standard. Inaccessible tooling silently excludes disabled architects and disabled SME founders. Sovereign deployments at public bodies inherit the same legal obligation.

**Implications**:

- Accessibility testing in CI (automated) and with users (manual) on every material UI change
- Keyboard-only navigation for all functions
- Screen reader compatibility validated
- Sufficient colour contrast and resizable text
- Public Accessibility Statement reviewed at least annually

**Validation Gates**:

- [ ] Automated accessibility checks pass in CI
- [ ] Manual assistive-technology testing performed on each release
- [ ] WCAG 2.2 AA conformance documented per page
- [ ] Accessibility Statement published and current

---

### 13. Performance and Efficiency

**Principle Statement**:
Tenant-facing operations MUST meet defined performance targets under expected load, with efficient use of computational resources.

**Performance Targets** (defined per service; examples):

- Interactive page operations: p95 latency < 1 second, p99 < 3 seconds
- Document generation (AI-assisted): p95 < 60 seconds with progress indicator
- Bulk export: completes within 10 minutes for a typical SME tenant

**Implications**:

- Performance requirements defined before implementation
- Load testing at expected and peak capacity before production deployment
- Continuous performance monitoring, not point-in-time
- Caching strategies for expensive operations
- Hot paths identified through profiling

**Validation Gates**:

- [ ] Per-service performance targets defined
- [ ] Load testing performed at expected capacity
- [ ] Performance metrics monitored in production
- [ ] Capacity-planning model documented

---

### 14. Availability and Reliability

**Principle Statement**:
The platform MUST meet defined availability targets with automated recovery and minimal data loss.

**Availability Targets**:

- Core managed-SaaS tenant-facing services: target > 99.9% (≈ 43 min/month) measured over a rolling 30 days
- Sovereign deployment availability targets agreed with the deploying authority and typically constrained by the host environment
- Recovery Time Objective (RTO): < 4 hours for full service (managed SaaS); per accreditation for sovereign
- Recovery Point Objective (RPO): < 15 minutes of tenant data loss (managed SaaS); per accreditation for sovereign

**High Availability Patterns**:

- Redundancy across UK availability zones (managed SaaS) or across redundant nodes (sovereign)
- Automated health checks and failover
- Active-active where practical
- Regular disaster recovery testing — at least annually

**Validation Gates**:

- [ ] Availability SLO defined and reported publicly (managed SaaS)
- [ ] RTO and RPO documented per service
- [ ] Redundancy strategy implemented and tested
- [ ] Backup and restore procedures validated

---

### 15. Maintainability and Evolvability

**Principle Statement**:
All services MUST be designed for change, with clear separation of concerns, modular architecture, and current documentation.

**Implications**:

- Clear module boundaries and ownership
- Separation of business logic, data access, and presentation
- Self-documenting code with meaningful names
- Architecture Decision Records for significant choices, stored in the repository
- Automated tests sufficient to enable confident refactoring

**Validation Gates**:

- [ ] Architecture documentation exists and is current
- [ ] Module boundaries clear with defined responsibilities
- [ ] Automated test coverage enables safe refactoring
- [ ] ADRs document key choices

---

## V. Development Practices

### 16. Open Source First and Reuse Before Build

**Principle Statement**:
Where a credible open-source or government-published component exists that meets the requirement, the team MUST evaluate reuse before commissioning a bespoke build. Where the platform builds new capability that has reuse value beyond ArcKit, it SHOULD be released under an OSI-approved open-source licence on a public repository. All reused components MUST be vetted for sovereign-deployment compatibility (offline use, licence compatibility for restricted distribution, supply-chain integrity).

**Rationale**:
The TCoP and the UK Government Service Manual prefer open source. Reuse aligns with the SME-affordability principle: every component we don't have to build is one we don't have to charge for. Contributing back strengthens the ecosystem ArcKit's tenants depend on. Sovereign deployments add an additional reuse constraint: components that depend on phone-home licensing or internet-only services cannot be used.

**Implications**:

- `/arckit:gov-reuse` and equivalent searches considered before new builds
- Build-vs-reuse decision recorded as an ADR for material components
- Bespoke components with cross-cutting value released as open source where licence and security allow
- Security and supply-chain controls applied to all reused components (SBOM, vulnerability scanning, licence review)
- Component dependencies must support fully offline operation and offline licence verification for sovereign deployments

**Validation Gates**:

- [ ] Reuse assessment completed for material components
- [ ] Build-vs-reuse decisions captured as ADRs
- [ ] Open-source release plan documented for reusable components
- [ ] SBOM produced and current
- [ ] No component requires phone-home or internet-only licensing for sovereign deployments

---

### 17. Cost Transparency and FinOps

**Principle Statement**:
Platform cost MUST be allocable to tenant, service, and feature, MUST be reviewed continuously, and MUST be optimised to sustain the SME-affordable pricing required by Principle 1. Sovereign deployment commercial models MUST recover their full cost-to-serve so that they cross-subsidise — never undermine — the SME tier.

**Rationale**:
Equitable SME pricing is only sustainable if the underlying cost base is understood and managed. Without FinOps discipline, the free tier becomes a financial risk that pressure ultimately closes. Sovereign deployments are higher-cost-to-serve and must be priced accordingly.

**Implications**:

- Tagging strategy for all infrastructure to allocate cost by tenant tier, service, and environment
- Monthly cost review with action items
- Reserved/committed-use discounts where stable consumption justifies it
- Egress and AI-inference costs (typically the largest variables) tracked per tenant and per feature
- Annual published affordability review (linked to Principle 1)
- Sovereign deployment pricing covers engineering, support, accreditation effort, and contributes margin to the SME tier

**Validation Gates**:

- [ ] Cost allocation tagging implemented and audited
- [ ] Monthly FinOps review run with documented actions
- [ ] Per-tenant cost-to-serve calculable
- [ ] AI-inference and egress costs tracked separately
- [ ] Sovereign-deployment unit economics documented and contribute to SME-tier funding model

---

### 18. Infrastructure as Code

**Principle Statement**:
All infrastructure MUST be defined as code, version-controlled, peer-reviewed, and deployed through automated pipelines. Manual production changes are prohibited except under documented break-glass procedure. Sovereign deployment topology MUST be defined in the same IaC repository, parameterised for offline / disconnected execution.

**Implications**:

- Declarative IaC for all environments
- Infrastructure changes go through code review
- Environments reproducible from code, including sovereign environments from a sealed release bundle
- Infrastructure versioned alongside the application code that depends on it
- Break-glass changes logged, reviewed, and reconciled back into IaC within a defined window

**Validation Gates**:

- [ ] Infrastructure defined as code
- [ ] Infrastructure code version-controlled and reviewed
- [ ] Automated pipeline for infrastructure deployment
- [ ] Break-glass procedure documented and audited
- [ ] Sovereign deployment reproducible end-to-end from a signed release bundle

---

### 19. Automated Testing

**Principle Statement**:
All code changes MUST be validated through automated testing — functional, security, accessibility, performance, and resilience — before deployment to production. Test suites MUST run successfully in disconnected environments equivalent to sovereign deployment topology.

**Test Pyramid**:

- Unit tests (fast, isolated) — 70–80% of tests
- Integration tests — 15–20%
- End-to-end tests for critical journeys — 5–10%

**Required Test Types**:

- Functional, performance, security, accessibility, resilience
- Multi-tenant isolation tests (see Principle 8)
- Sovereign-mode tests (single-tenant, offline, signed-bundle install)

**Validation Gates**:

- [ ] Automated tests pass before merge
- [ ] Coverage thresholds defined and met
- [ ] Critical paths covered by end-to-end tests
- [ ] Tenant isolation tests run on every release
- [ ] Disconnected/offline test profile run on every release

---

### 20. Continuous Integration and Deployment

**Principle Statement**:
All code changes MUST flow through automated build, test, and deployment pipelines with quality gates at each stage. The release pipeline MUST produce both a managed-SaaS deployment and a sovereign-deployment release bundle from the same source revision.

**Pipeline Stages**:

1. Source control — all changes committed
2. Build — automated compilation and packaging with SBOM generation and signed artefacts
3. Test — automated test execution, including offline profile
4. Security scan — dependency, container, and code vulnerability scanning
5. Deployment — automated to managed SaaS; signed sealed bundle produced for sovereign customers

**Quality Gates**:

- All tests pass
- No critical or high security vulnerabilities unaddressed
- Code review approval required
- Production deployment gated by readiness checklist
- Sovereign release bundle signed, hashed, and accompanied by SBOM and release notes

**Validation Gates**:

- [ ] Automated CI/CD pipeline exists
- [ ] Pipeline includes security and supply-chain scanning
- [ ] Deployment automated and repeatable
- [ ] Rollback capability tested
- [ ] Sovereign release bundle reproducible byte-for-byte from the same revision

---

### 21. Sovereign and Air-Gapped Deployment

**Principle Statement**:
The platform MUST support deployment into customer-controlled environments — including UK Ministry of Defence and other sensitive sites — operating fully in disconnected or air-gapped mode. The sovereign deployment MUST share the same source code, data formats, and APIs as the managed SaaS, and MUST be installable, operable, updatable, and uninstallable without any reliance on vendor-controlled services or outbound network connectivity.

**Rationale**:
A material portion of the platform's intended audience cannot lawfully or operationally use a public managed SaaS for some or all of their work. MOD and other sensitive sites operate at OFFICIAL-SENSITIVE and above, often inside accredited boundaries with no internet egress. If the platform is only available as a SaaS, those users either cannot adopt it at all or must adopt a fragmented alternative — undermining the consistency that ArcKit exists to deliver. Supporting sovereign deployment also strengthens the Open Standards (Principle 4) and Open Source (Principle 16) commitments by making them genuinely exit-ready.

**Implications**:

- A single codebase serves both managed-SaaS and sovereign deployments; no proprietary fork
- All required dependencies are vendorable and operable offline (no phone-home, no SaaS-only third-party services on the critical path)
- Installation and updates proceed from a signed, hashed release bundle that can be transferred across an air-gap (e.g., via approved data transfer mechanisms)
- AI / model dependencies are pluggable: the platform supports approved on-premise model endpoints in sovereign mode and does not assume a specific external provider
- Time, certificate authority, package mirror, and similar foundational services are configurable to point at customer-controlled endpoints
- Telemetry destinations are configurable and default to customer-controlled endpoints in sovereign mode (see Principle 6)
- Deployment topology is defined in the same IaC repository as the managed SaaS, parameterised for offline execution (see Principle 18)
- Documentation includes operator runbooks for install, upgrade, backup, restore, key rotation, and decommission performed entirely within the boundary
- Release cadence for sovereign bundles is decoupled from managed-SaaS releases; sovereign customers may stay on a long-term support release line
- Vendor support model for sovereign deployments respects the boundary — remote support only via mechanisms permitted by the deploying authority's accreditation
- Sovereign-deployment customers receive the data-portability guarantees of Principle 9, allowing exit to other tooling without vendor cooperation

**Reference Frameworks**:

- MOD Secure by Design — assess via `/arckit:mod-secure`
- JSP 440 (Defence Manual of Security) — applicable controls
- JSP 604 (Defence Manual for the Authorisation of Information Systems) — accreditation pathway
- NCSC Cyber Assessment Framework (CAF) — applicable to sensitive non-MOD sites
- HMG Government Security Classifications Policy — classification handling
- NCSC supply chain security guidance — for the signed-bundle delivery model

**Validation Gates**:

- [ ] Sovereign release bundle produced from each managed-SaaS release revision
- [ ] Bundle is signed, hashed, and accompanied by SBOM and release notes
- [ ] Disconnected installation walkthrough validated end-to-end on a representative isolated environment at least every release
- [ ] Disconnected upgrade path validated (including roll-forward and roll-back)
- [ ] Backup, restore, and decommission procedures validated within boundary
- [ ] AI / model integration documented as pluggable; default sovereign profile points at no external provider
- [ ] Telemetry, time, CA, and package-mirror integrations configurable to customer-controlled endpoints
- [ ] MOD Secure by Design assessment evidence attached to each sovereign release
- [ ] No critical-path dependency requires outbound internet connectivity in sovereign mode (validated by network-deny test)
- [ ] Operator runbook for install / upgrade / backup / restore / key rotation / decommission published with each release
- [ ] Long-term support release line and patching commitment documented and honoured

**Example — Good**:
Each managed-SaaS release also produces a signed `arckit-sovereign-{version}.bundle` containing all container images, IaC, signed manifests, SBOM, and offline documentation. A representative MOD-style isolated environment is provisioned in CI; the bundle installs, runs the full functional test suite with no internet egress, upgrades from the previous release, and is then decommissioned cleanly. The AI generation feature is wired via a configurable endpoint; sovereign customers point it at their own approved model deployment.

**Example — Bad**:
Sovereign customers receive a "stripped down" fork of the platform missing major features. Installation requires `curl` from public package registries during install. Telemetry is hard-coded to a vendor SaaS endpoint. AI generation only works against a single external commercial provider. Updates require a maintenance window with internet access.

**Common Violations to Avoid**:

- Hard-coded outbound calls (analytics, telemetry, package mirrors, time, certificate revocation)
- AI / model endpoints not pluggable
- Forking sovereign code from managed-SaaS code, leading to feature drift
- Updates that cannot be applied across an air-gap
- Licence terms (e.g., for embedded third-party components) that prohibit on-premise distribution
- Support models that assume vendor remote access

---

## VI. Exception Process

### Requesting Architecture Exceptions

Principles are mandatory unless a documented exception is approved by the ArcKit Architecture Review Board. **Principle 1 (SME affordability — managed SaaS), Principle 5 (Security by Design), Principle 7 (UK data sovereignty), Principle 12 (Accessibility), and Principle 21 (Sovereign Deployment Capability) are non-negotiable** at platform level. Specific sovereign deployments may carry their own additional non-negotiable controls imposed by the deploying authority's accreditation.

**Valid Exception Reasons**:

- Technical constraints that genuinely prevent compliance
- Regulatory or legal requirements that override
- Transitional state during migration, with a defined end date
- Pilot or proof-of-concept with a defined end date

**Exception Request Requirements**:

- [ ] Justification with business and technical rationale
- [ ] Alternative approach and compensating controls
- [ ] Risk assessment and mitigation plan
- [ ] Expiration date — exceptions are time-bound
- [ ] Remediation plan to achieve compliance

**Approval Process**:

1. Submit exception request to the ArcKit Architecture Review Board
2. Review by the board (security and SRO sign-off required)
3. For sovereign deployments, additional sign-off by the deploying authority's accreditor
4. Document the exception in the relevant project artefacts
5. Quarterly review of all open exceptions

---

## VII. Governance and Compliance

### UK Public Sector Alignment

The platform MUST evidence alignment with:

- **Technology Code of Practice (TCoP)** — assessed via `/arckit:tcop`
- **GDS Service Standard** — assessed via `/arckit:service-assessment`
- **NCSC Cyber Assessment Framework (CAF)** — current self-assessment maintained
- **NCSC Cloud Security Principles (14)** — assessed and evidenced (managed SaaS)
- **MOD Secure by Design / JSP 440 / JSP 604** — assessed for sovereign MOD deployments via `/arckit:mod-secure`
- **G-Cloud framework** — service listed and kept current
- **UK GDPR / DPA 2018** — DPIA via `/arckit:dpia` for material processing changes
- **PSBAR 2018 / WCAG 2.2 AA** — Accessibility Statement maintained
- **Procurement Act 2023** — SME engagement evidenced
- **HMG Government Security Classifications Policy** — classification handling per deployment mode

### Architecture Review Gates

**Discovery / Alpha**:

- [ ] Principles understood by the delivery team
- [ ] High-level approach aligns with principles
- [ ] No obvious principle violations
- [ ] Deployment-mode applicability (managed SaaS / sovereign / both) determined

**Beta / Design**:

- [ ] Detailed architecture documented
- [ ] Compliance with each principle validated
- [ ] Exceptions requested and approved
- [ ] Security, data, and accessibility principles validated
- [ ] Sovereign-deployment impact assessed for any new dependency

**Pre-Production**:

- [ ] Implementation matches approved architecture
- [ ] All validation gates passed
- [ ] Operational readiness verified
- [ ] Sovereign release bundle validated end-to-end on isolated environment

### Enforcement

- Architecture reviews are mandatory for all material changes
- Principle violations must be remediated before production deployment unless an approved time-bound exception exists
- Approved exceptions reviewed quarterly
- Retrospective reviews of compliance on the live platform at least annually
- Sovereign-deployment release bundles reviewed before issue to customers

---

## VIII. Appendix

### Principle Summary Checklist

| # | Principle | Category | Criticality | Validation |
|---|-----------|----------|-------------|------------|
| 1 | Equitable Access for SMEs (managed SaaS) | Strategic / Commercial | CRITICAL (non-negotiable) | Pricing review, eligibility audit |
| 2 | Scalability and Elasticity | Strategic | HIGH | Load testing, scaling metrics |
| 3 | Resilience and Fault Tolerance | Strategic | CRITICAL | Chaos testing, RTO/RPO |
| 4 | Open Standards and Interoperability | Strategic | HIGH | API specs, export coverage |
| 5 | Security by Design | Strategic | CRITICAL (non-negotiable) | Threat model, pen test, CAF, MOD SbD |
| 6 | Observability | Strategic | HIGH | Metrics, logs, traces, status page |
| 7 | UK Data Sovereignty and Governance | Data | CRITICAL (non-negotiable) | UK residency, DPIA, ROPA, accreditation |
| 8 | Tenant Isolation and Single Source of Truth | Data | CRITICAL | Isolation tests, MDM |
| 9 | Data Quality, Lineage, and Portability | Data | HIGH | Quality checks, full export |
| 10 | Loose Coupling | Integration | HIGH | Independent deployment |
| 11 | Asynchronous Communication | Integration | MEDIUM | Async patterns, on-prem broker support |
| 12 | Accessibility (WCAG 2.2 AA) | Quality | CRITICAL (non-negotiable) | Automated + manual a11y testing |
| 13 | Performance and Efficiency | Quality | HIGH | Load testing |
| 14 | Availability and Reliability | Quality | CRITICAL | SLO monitoring, DR test |
| 15 | Maintainability and Evolvability | Quality | MEDIUM | Documentation, tests, ADRs |
| 16 | Open Source First and Reuse | Practice | HIGH | Reuse ADRs, OSS releases, offline-compatible |
| 17 | Cost Transparency and FinOps | Practice | HIGH | Tagging, monthly review, sovereign unit economics |
| 18 | Infrastructure as Code | Practice | HIGH | IaC coverage, sovereign reproducibility |
| 19 | Automated Testing | Practice | HIGH | Test coverage, isolation tests, offline profile |
| 20 | CI/CD | Practice | HIGH | Pipeline exists, gates enforced, sovereign bundle |
| 21 | Sovereign and Air-Gapped Deployment | Strategic / Deployment | CRITICAL (non-negotiable) | Bundle reproducible, offline install validated, MOD SbD |

### Document Version History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial ratified version (managed SaaS scope) |
| 2.0 | 2026-05-03 | ArcKit AI | Added Sovereign and Air-Gapped Deployment principle and dual deployment model; updated Principles 1, 5, 7, 8 |

## External References

> This section provides traceability from generated content back to source documents.
> No external policy documents were placed in `projects/000-global/policies/` at the time of generation. UK Government and MOD policies referenced in the body (TCoP, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, MOD Secure by Design, JSP 440, JSP 604, UK GDPR, PSBAR 2018, Procurement Act 2023, HMG Government Security Classifications Policy) are public-domain and cited by name; place authoritative copies in `projects/000-global/policies/` and re-run `/arckit:principles` to embed inline citations.

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

**Generated by**: ArcKit `/arckit:principles` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Project 000)
**AI Model**: Claude Opus 4.7 (1M context)
