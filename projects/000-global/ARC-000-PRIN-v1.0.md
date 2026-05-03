# ArcKit as a Service — Enterprise Architecture Principles

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:principles`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-000-PRIN-v1.0 |
| **Document Type** | Architecture Principles |
| **Project** | ArcKit as a Service (Project 000) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Annual |
| **Next Review Date** | 2027-05-03 |
| **Owner** | Mark Craddock, ArcKit as a Service Owner |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | ArcKit as a Service team, UK SME tenants, Crown Commercial Service, GDS, CDDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:principles` command, scoped to ArcKit as a Service for UK SMEs supplying government services | PENDING | PENDING |

---

## Executive Summary

This document establishes the immutable principles governing all technology architecture decisions for **ArcKit as a Service** — a managed, multi-tenant offering of the ArcKit enterprise architecture governance toolkit, designed for UK public sector adoption and, critically, for **Small and Medium Enterprises (SMEs) supplying government services**.

These principles ensure consistency, security, accessibility, scalability and alignment with UK Government policy (GDS Service Standard, Technology Code of Practice, NCSC Cyber Assessment Framework, G-Cloud) across all tenants and feature work.

**Scope**: All technology decisions for the ArcKit as a Service platform, its tenant-facing services, supporting infrastructure, and integrations.
**Authority**: ArcKit Architecture Review Board.
**Compliance**: Mandatory unless an exception is approved (see §VI Exception Process).

**Philosophy**: These principles are **technology-agnostic**. They describe WHAT qualities the architecture must have, not HOW to implement them with specific products. Specific technology selection happens during research and design phases (`/arckit:research`, `/arckit:aws-research`, etc.) guided by these principles.

**Foundational commercial commitment**: ArcKit as a Service exists to lower the cost of doing high-quality architecture for **SMEs supplying UK government**. Pricing, packaging, and platform decisions MUST keep the entry tier free or substantially cheaper than commercial equivalents for in-scope SMEs (see Principle 1).

---

## I. Strategic Principles

### 1. Equitable Access for SMEs Supplying Government

**Principle Statement**:
ArcKit as a Service MUST be free or substantially cheaper than commercial equivalents for verified Small and Medium Enterprises (SMEs) supplying or seeking to supply UK government services. Pricing, feature gating, and capacity allocation MUST NOT erect barriers that disadvantage SMEs relative to large incumbents.

**Rationale**:
The UK Government has a stated ambition to spend more with SMEs (Procurement Act 2023, SME Action Plans, the £1 in every £3 SME spend target). SMEs typically lack the in-house enterprise architecture capability that larger system integrators take for granted, and commercial EA tooling is priced for enterprises. A managed ArcKit service reduces that capability gap and supports a more diverse, competitive supplier base for the public sector. If pricing replicates the commercial market, the service fails its primary purpose.

**Implications**:

- A free entry tier MUST exist that is genuinely usable for end-to-end government work — not a marketing trial — covering the essential ArcKit baseline (principles, requirements, ADRs, diagrams, traceability) for at least one active engagement.
- SME eligibility MUST be verifiable against a transparent, published definition (default: UK definition aligned with the Companies Act 2006 SME thresholds and Crown Commercial Service guidance, subject to legal review).
- Paid tiers MUST be priced on a cost-recovery or modest-margin basis for verified SMEs, with transparent published list prices.
- Feature gating between free and paid tiers MUST NOT remove governance-critical functions (security, audit log export, data export, accessibility) from the free tier.
- Capacity, support, and rate limits on the free tier MUST be sufficient for genuine delivery work, sized against typical SME engagement profiles (defined and reviewed annually).
- Cross-subsidy is acceptable: large-enterprise or non-SME tenants MAY be charged at higher rates to fund the SME tier, provided this is transparent.
- Procurement routes MUST include G-Cloud listing so that buying authorities can call off the service without bespoke procurement.

**Validation Gates**:

- [ ] Published SME eligibility policy with verification process
- [ ] Free tier covers the essential ArcKit baseline for at least one project end-to-end
- [ ] Paid tier list prices published openly (no "contact sales" gating for SMEs)
- [ ] Annual affordability review against comparator commercial EA tooling published
- [ ] No governance-critical feature is paywalled away from the free tier
- [ ] Service listed on G-Cloud with SME-friendly minimum commitment terms

**Example — Good**:
Free tier permits unlimited principles, ADRs, requirements and diagrams for one active project, with full export. Paid SME tier (≤ £X / user / month, published) adds multi-project workspaces and SSO. Large-enterprise tier funds the SME tier through a higher per-seat rate.

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
The platform MUST scale horizontally to meet aggregate tenant demand and MUST dynamically adjust capacity based on load without manual intervention.

**Rationale**:
Demand is multi-tenant and variable: government delivery cycles, end-of-financial-year procurement, and bid windows produce predictable peaks; viral adoption events produce unpredictable ones. Capacity must follow demand, not the reverse.

**Implications**:

- Stateless application components, replicable across compute nodes
- No hard-coded tenant, document, or user limits in the runtime
- Distributed deployment across multiple availability zones
- Load balancing and auto-scaling driven by demand metrics
- Cost model accounts for variable capacity (see also Principle 17, FinOps)
- Per-tenant fair-use limits enforced separately from platform capacity limits

**Validation Gates**:

- [ ] System demonstrably scales horizontally (add more instances)
- [ ] No single points of failure constrain scaling
- [ ] Load testing demonstrates capacity growth in line with added resources
- [ ] Auto-scaling triggers and metrics defined and tested
- [ ] Cost model accounts for variable capacity

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

**Validation Gates**:

- [ ] Failure modes identified and mitigated
- [ ] Chaos / fault-injection testing performed at least quarterly
- [ ] RTO and RPO defined per service, evidenced by recovery testing
- [ ] Automated failover tested
- [ ] Degraded-mode behaviour documented and visible to tenants

---

### 4. Open Standards and Interoperability

**Principle Statement**:
All tenant-facing functionality MUST be exposed through well-defined, versioned interfaces using open, industry-standard protocols and data formats. Direct database access across system boundaries is prohibited. Tenant data MUST be exportable in open formats with no licensing encumbrance.

**Rationale**:
The Technology Code of Practice (TCoP) and the GDS Service Standard require open standards and the avoidance of vendor lock-in. SMEs in particular depend on portability: a tenant must be able to leave the service and continue their architecture work elsewhere. Open interfaces also enable government buyers to integrate ArcKit outputs with their existing assurance pipelines.

**Implications**:

- HTTP APIs documented with OpenAPI; events documented with AsyncAPI
- Versioning strategy with backward compatibility windows of at least 12 months
- Tenant content stored in open, human-readable formats (e.g., Markdown, JSON, YAML) — never proprietary binary blobs
- Full-fidelity export of all tenant artifacts on demand, without paywall
- No direct database coupling across system boundaries
- Authentication via standard protocols (OIDC / OAuth 2.x / SAML 2.0)

**Validation Gates**:

- [ ] OpenAPI / AsyncAPI specifications published for all public interfaces
- [ ] Versioning and deprecation policy published
- [ ] Tenant export covers 100% of their content in open formats
- [ ] Authentication uses standard protocols
- [ ] No cross-system database coupling

---

### 5. Security by Design (NON-NEGOTIABLE)

**Principle Statement**:
The platform MUST implement defence-in-depth security with zero-trust principles, aligned to the NCSC Cyber Assessment Framework (CAF) and Cloud Security Principles. Security is a foundational requirement, not a feature to be added later.

**Rationale**:
Tenant data includes architecture artefacts that, in aggregate, describe how government services are designed. Even at OFFICIAL classification, this data is sensitive and a target. A breach would damage tenant trust irreversibly and could expose downstream government delivery.

**Zero Trust Pillars**:

1. **Identity-Based Access** — no network-based trust; every request authenticated and authorised
2. **Least Privilege** — minimum necessary permissions, time-boxed where possible
3. **Encryption Everywhere** — data encrypted in transit and at rest using current, industry-standard algorithms
4. **Continuous Verification** — monitor, log, and analyse all access patterns

**Mandatory Controls**:

- [ ] Multi-factor authentication for all human access (tenant users and operators)
- [ ] Service-to-service authentication via mutual TLS, signed tokens, or equivalent
- [ ] Secrets in a secure vault — never in code, config files, or container images
- [ ] Network segmentation with minimal trust zones
- [ ] Encryption at rest for all tenant data and backups
- [ ] Encrypted transport for all network communication (current TLS, no deprecated ciphers)
- [ ] Structured logging of all authentication and authorisation events
- [ ] Independent penetration testing at least annually and on material change
- [ ] Vulnerability scanning of dependencies and container images on every build
- [ ] Tenant isolation enforced at storage, compute, and identity layers

**Compliance Frameworks**:

- NCSC Cyber Assessment Framework (CAF) — target profile defined and assessed
- NCSC Cloud Security Principles (14 principles) — assessed and evidenced
- ISO 27001 alignment with a formal certification roadmap
- UK GDPR / Data Protection Act 2018 (see Principle 7)

**Exceptions**: None. Specific control implementations may vary with documented compensating controls.

**Validation Gates**:

- [ ] Threat model completed and reviewed
- [ ] NCSC CAF self-assessment current within 12 months
- [ ] Penetration test report and remediation plan current
- [ ] Incident response runbook tested at least annually
- [ ] Tenant isolation verified by automated and manual testing

---

### 6. Observability and Operational Excellence

**Principle Statement**:
All services MUST emit structured telemetry (logs, metrics, traces) sufficient for real-time monitoring, troubleshooting, capacity planning, and tenant-facing transparency.

**Rationale**:
We cannot operate, secure, or scale what we cannot observe. Tenants — particularly SMEs without their own SRE function — also need visibility into the service status that affects them.

**Telemetry Requirements**:

- **Logging** — structured logs with correlation IDs and tenant IDs
- **Metrics** — request volume, latency percentiles (p50, p95, p99), error rates, saturation
- **Tracing** — distributed trace context across all internal hops
- **Public status** — externally visible status page covering core tenant-facing services

**Required Instrumentation**:

- Request volume, latency distribution, error rate per service
- Resource utilisation (CPU, memory, I/O, network)
- Tenant-level activity and consumption metrics (for FinOps and fair-use)
- Security events (auth failures, policy violations, suspicious patterns)

**Log Retention**:

- Security and audit logs — at least 12 months, longer where regulation requires
- Application logs — at least 90 days for troubleshooting
- Metrics — at least 13 months to support year-on-year comparison

**Validation Gates**:

- [ ] Logs, metrics, and traces instrumented for all services
- [ ] Dashboards and alerts configured with actionable runbooks
- [ ] Service Level Objectives (SLOs) and Service Level Indicators (SLIs) defined
- [ ] Public status page in place and updated automatically
- [ ] Capacity-planning metrics tracked

---

## II. Data Principles

### 7. Data Sovereignty, Residency, and Governance (UK Context)

**Principle Statement**:
Tenant data MUST be stored and processed in the United Kingdom by default. Cross-border processing MUST have explicit tenant consent and a documented legal basis. Data classification, retention, and access MUST comply with UK GDPR, the Data Protection Act 2018, and the Government Security Classifications Policy.

**Data Classification**:

The platform handles data at a maximum of OFFICIAL (including OFFICIAL-SENSITIVE handling caveats where tenants opt in). Higher classifications (SECRET, TOP SECRET) are explicitly out of scope.

**Data Residency**:

- Default UK region for all tenant data, backups, and replicas
- Cross-border processing only with explicit per-tenant consent and a documented Article 46 transfer mechanism
- Sub-processors disclosed, located preferentially in the UK or adequate jurisdictions, and reviewed annually

**Data Retention**:

- Tenant content retained for the lifetime of the tenancy plus a documented grace period
- Automatic deletion after tenancy ends, with verifiable destruction evidence
- Backup retention aligned with RPO and regulatory requirements
- Legal hold process available

**Validation Gates**:

- [ ] Default UK residency for all tenant data
- [ ] Data classification recorded for every data store
- [ ] Sub-processor list published and current
- [ ] Retention and deletion automated, with deletion certificates available to tenants
- [ ] UK GDPR Records of Processing Activity (ROPA) maintained

---

### 8. Tenant Isolation and Single Source of Truth

**Principle Statement**:
Every tenant's data MUST be logically isolated such that no tenant can read, write, infer, or exhaust another tenant's data or capacity. Each data domain MUST have a single authoritative source, with derived copies clearly labelled and synchronised.

**Rationale**:
Multi-tenancy is the commercial enabler for the SME-affordable pricing in Principle 1. It is also the largest source of platform risk: one cross-tenant defect destroys trust for all tenants. A single source of truth prevents the reconciliation drift that becomes acute at scale.

**Implications**:

- Tenant ID propagated on every request and enforced at every storage and compute boundary
- Authorisation checks fail closed — default-deny at every layer
- Per-tenant resource quotas to prevent noisy-neighbour exhaustion
- System of record identified for each data entity; derived stores read-only and labelled
- Automated tests verifying isolation on every release
- No bidirectional synchronisation without an explicit conflict-resolution strategy

**Validation Gates**:

- [ ] Tenant isolation tested in CI on every change
- [ ] Per-tenant quotas configured and enforced
- [ ] System of record identified for each entity
- [ ] Derived copies documented with sync frequency
- [ ] Cross-tenant access scenarios proven impossible by automated test

---

### 9. Data Quality, Lineage, and Tenant Portability

**Principle Statement**:
Tenant artefacts MUST be of provable quality and end-to-end lineage, and MUST be exportable by the tenant at any time in open, machine-readable formats with no degradation.

**Rationale**:
ArcKit produces governance artefacts that downstream consumers (tenants, government buyers, assurance bodies) rely on. Quality and lineage make the artefacts trustworthy. Portability honours the open-standards principle and prevents lock-in.

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
Loose coupling enables independent deployment, technology diversity, team autonomy, and the safe evolution of the platform without breaking tenants.

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
Non-real-time interactions SHOULD use asynchronous patterns (events, queues) to improve resilience and decoupling.

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

---

## IV. Quality Attributes

### 12. Accessibility (NON-NEGOTIABLE for Public Sector)

**Principle Statement**:
All tenant-facing user interfaces MUST meet WCAG 2.2 Level AA as a minimum, MUST be tested with assistive technologies, and MUST publish an up-to-date Accessibility Statement aligned with the Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018.

**Rationale**:
The platform is intended for public sector use and SMEs supplying public sector services; accessibility is a legal obligation for those use cases (PSBAR 2018) and a baseline expectation under the GDS Service Standard. Inaccessible tooling silently excludes disabled architects and disabled SME founders.

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

- Core tenant-facing services: target > 99.9% (≈ 43 min/month) measured over a rolling 30 days
- Recovery Time Objective (RTO): < 4 hours for full service
- Recovery Point Objective (RPO): < 15 minutes of tenant data loss

**High Availability Patterns**:

- Redundancy across UK availability zones
- Automated health checks and failover
- Active-active where practical
- Regular disaster recovery testing — at least annually

**Validation Gates**:

- [ ] Availability SLO defined and reported publicly
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
Where a credible open-source or government-published component exists that meets the requirement, the team MUST evaluate reuse before commissioning a bespoke build. Where the platform builds new capability that has reuse value beyond ArcKit, it SHOULD be released under an OSI-approved open-source licence on a public repository.

**Rationale**:
The TCoP and the UK Government Service Manual prefer open source. Reuse aligns with the SME-affordability principle: every component we don't have to build is one we don't have to charge for. Contributing back strengthens the ecosystem ArcKit's tenants depend on.

**Implications**:

- `/arckit:gov-reuse` and equivalent searches considered before new builds
- Build-vs-reuse decision recorded as an ADR for material components
- Bespoke components with cross-cutting value released as open source where licence and security allow
- Security and supply-chain controls applied to all reused components (SBOM, vulnerability scanning, licence review)

**Validation Gates**:

- [ ] Reuse assessment completed for material components
- [ ] Build-vs-reuse decisions captured as ADRs
- [ ] Open-source release plan documented for reusable components
- [ ] SBOM produced and current

---

### 17. Cost Transparency and FinOps

**Principle Statement**:
Platform cost MUST be allocable to tenant, service, and feature, MUST be reviewed continuously, and MUST be optimised to sustain the SME-affordable pricing required by Principle 1.

**Rationale**:
Equitable SME pricing is only sustainable if the underlying cost base is understood and managed. Without FinOps discipline, the free tier becomes a financial risk that pressure ultimately closes.

**Implications**:

- Tagging strategy for all infrastructure to allocate cost by tenant tier, service, and environment
- Monthly cost review with action items
- Reserved/committed-use discounts where stable consumption justifies it
- Egress and AI-inference costs (typically the largest variables) tracked per tenant and per feature
- Annual published affordability review (linked to Principle 1)

**Validation Gates**:

- [ ] Cost allocation tagging implemented and audited
- [ ] Monthly FinOps review run with documented actions
- [ ] Per-tenant cost-to-serve calculable
- [ ] AI-inference and egress costs tracked separately

---

### 18. Infrastructure as Code

**Principle Statement**:
All infrastructure MUST be defined as code, version-controlled, peer-reviewed, and deployed through automated pipelines. Manual production changes are prohibited except under documented break-glass procedure.

**Implications**:

- Declarative IaC for all environments
- Infrastructure changes go through code review
- Environments reproducible from code
- Infrastructure versioned alongside the application code that depends on it
- Break-glass changes logged, reviewed, and reconciled back into IaC within a defined window

**Validation Gates**:

- [ ] Infrastructure defined as code
- [ ] Infrastructure code version-controlled and reviewed
- [ ] Automated pipeline for infrastructure deployment
- [ ] Break-glass procedure documented and audited

---

### 19. Automated Testing

**Principle Statement**:
All code changes MUST be validated through automated testing — functional, security, accessibility, performance, and resilience — before deployment to production.

**Test Pyramid**:

- Unit tests (fast, isolated) — 70–80% of tests
- Integration tests — 15–20%
- End-to-end tests for critical journeys — 5–10%

**Required Test Types**:

- Functional, performance, security, accessibility, resilience
- Multi-tenant isolation tests (see Principle 8)

**Validation Gates**:

- [ ] Automated tests pass before merge
- [ ] Coverage thresholds defined and met
- [ ] Critical paths covered by end-to-end tests
- [ ] Tenant isolation tests run on every release

---

### 20. Continuous Integration and Deployment

**Principle Statement**:
All code changes MUST flow through automated build, test, and deployment pipelines with quality gates at each stage.

**Pipeline Stages**:

1. Source control — all changes committed
2. Build — automated compilation and packaging with SBOM generation
3. Test — automated test execution
4. Security scan — dependency, container, and code vulnerability scanning
5. Deployment — automated, with progressive rollout

**Quality Gates**:

- All tests pass
- No critical or high security vulnerabilities unaddressed
- Code review approval required
- Production deployment gated by readiness checklist

**Validation Gates**:

- [ ] Automated CI/CD pipeline exists
- [ ] Pipeline includes security and supply-chain scanning
- [ ] Deployment automated and repeatable
- [ ] Rollback capability tested

---

## VI. Exception Process

### Requesting Architecture Exceptions

Principles are mandatory unless a documented exception is approved by the ArcKit Architecture Review Board. **Principle 1 (SME affordability), Principle 5 (Security by Design), Principle 7 (UK data sovereignty), and Principle 12 (Accessibility) are non-negotiable** and not subject to exception.

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
3. Document the exception in the relevant project artefacts
4. Quarterly review of all open exceptions

---

## VII. Governance and Compliance

### UK Public Sector Alignment

The platform MUST evidence alignment with:

- **Technology Code of Practice (TCoP)** — assessed via `/arckit:tcop`
- **GDS Service Standard** — assessed via `/arckit:service-assessment`
- **NCSC Cyber Assessment Framework (CAF)** — current self-assessment maintained
- **NCSC Cloud Security Principles (14)** — assessed and evidenced
- **G-Cloud framework** — service listed and kept current
- **UK GDPR / DPA 2018** — DPIA via `/arckit:dpia` for material processing changes
- **PSBAR 2018 / WCAG 2.2 AA** — Accessibility Statement maintained
- **Procurement Act 2023** — SME engagement evidenced

### Architecture Review Gates

**Discovery / Alpha**:

- [ ] Principles understood by the delivery team
- [ ] High-level approach aligns with principles
- [ ] No obvious principle violations

**Beta / Design**:

- [ ] Detailed architecture documented
- [ ] Compliance with each principle validated
- [ ] Exceptions requested and approved
- [ ] Security, data, and accessibility principles validated

**Pre-Production**:

- [ ] Implementation matches approved architecture
- [ ] All validation gates passed
- [ ] Operational readiness verified

### Enforcement

- Architecture reviews are mandatory for all material changes
- Principle violations must be remediated before production deployment unless an approved time-bound exception exists
- Approved exceptions reviewed quarterly
- Retrospective reviews of compliance on the live platform at least annually

---

## VIII. Appendix

### Principle Summary Checklist

| # | Principle | Category | Criticality | Validation |
|---|-----------|----------|-------------|------------|
| 1 | Equitable Access for SMEs | Strategic / Commercial | CRITICAL (non-negotiable) | Pricing review, eligibility audit |
| 2 | Scalability and Elasticity | Strategic | HIGH | Load testing, scaling metrics |
| 3 | Resilience and Fault Tolerance | Strategic | CRITICAL | Chaos testing, RTO/RPO |
| 4 | Open Standards and Interoperability | Strategic | HIGH | API specs, export coverage |
| 5 | Security by Design | Strategic | CRITICAL (non-negotiable) | Threat model, pen test, CAF |
| 6 | Observability | Strategic | HIGH | Metrics, logs, traces, status page |
| 7 | UK Data Sovereignty and Governance | Data | CRITICAL (non-negotiable) | UK residency, DPIA, ROPA |
| 8 | Tenant Isolation and Single Source of Truth | Data | CRITICAL | Isolation tests, MDM |
| 9 | Data Quality, Lineage, and Portability | Data | HIGH | Quality checks, full export |
| 10 | Loose Coupling | Integration | HIGH | Independent deployment |
| 11 | Asynchronous Communication | Integration | MEDIUM | Async patterns used |
| 12 | Accessibility (WCAG 2.2 AA) | Quality | CRITICAL (non-negotiable) | Automated + manual a11y testing |
| 13 | Performance and Efficiency | Quality | HIGH | Load testing |
| 14 | Availability and Reliability | Quality | CRITICAL | SLO monitoring, DR test |
| 15 | Maintainability and Evolvability | Quality | MEDIUM | Documentation, tests, ADRs |
| 16 | Open Source First and Reuse | Practice | HIGH | Reuse ADRs, OSS releases |
| 17 | Cost Transparency and FinOps | Practice | HIGH | Tagging, monthly review |
| 18 | Infrastructure as Code | Practice | HIGH | IaC coverage |
| 19 | Automated Testing | Practice | HIGH | Test coverage, isolation tests |
| 20 | CI/CD | Practice | HIGH | Pipeline exists, gates enforced |

### Document Version History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial ratified version |

## External References

> This section provides traceability from generated content back to source documents.
> No external policy documents were placed in `projects/000-global/policies/` at the time of generation. UK Government policies referenced in the body (TCoP, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, UK GDPR, PSBAR 2018, Procurement Act 2023, Government Security Classifications Policy) are public-domain and cited by name; place authoritative copies in `projects/000-global/policies/` and re-run `/arckit:principles` to embed inline citations.

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
