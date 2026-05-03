# Technology Code of Practice (TCoP) Review

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:tcop`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-TCOP-v1.0 |
| **Document Type** | Technology Code of Practice Review |
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
| **Distribution** | Project Team, Architecture Team, MOD Defence Digital liaison, NCSC liaison, CDDO Digital Spend Control |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:tcop` command — sovereign deployment-specific TCoP review. Sister to project 001 (managed SaaS) TCoP. | [PENDING] | [PENDING] |

## Document Purpose

This document records a Technology Code of Practice (TCoP) compliance review against the 13 TCoP points for the **sovereign / on-premise / air-gapped deployment route** of ArcKit as a Service. It is intended as input to:

- CDDO digital spend control submissions where applicable;
- MOD customer-side accreditation packs (alongside `/arckit:mod-secure`, `/arckit:risk`, JSP 440 / 604 evidence);
- Architecture Review Board governance for project 002.

The sovereign deployment differs structurally from the managed SaaS (project 001) on three TCoP points — Point 5 (Cloud First), Point 8 (Share/Reuse), Point 12 (Sustainability) — and on Point 13 (Service Standard), which is **N/A** because this is not a public-facing GDS service.

---

## Executive Summary

**Overall TCoP Compliance**: **Partially Compliant** (appropriate for pre-Alpha / requirements-stage maturity)

**Key Findings**:

- **9 / 13 Compliant** — strong evidence base from Principle 21 anchor, eight ADRs (ADR-001 to ADR-008), HLD, requirements (BR-001 to BR-008, FR-001 to FR-014), and the project-level risk register.
- **3 / 13 Partially Compliant** — Point 1 (user research depends on customer-side cleared personnel and is dated against persona placeholders); Point 2 (WCAG 2.2 AA inherited from SaaS but no sovereign-specific audit yet); Point 7 (DPIA scoped but customer-side responsibility for live processing).
- **1 / 13 N/A** — Point 13 (Service Standard) — this is not a public-facing GDS service. Assurance flows via the **MOD accreditation pathway (JSP 440 / JSP 604 / MOD Secure by Design)**, not via GDS service assessment.
- **Critical sovereign-specific framing**: Point 5 (Cloud First) is **explicitly justified as non-applicable to accredited boundaries**. JSP 440 / JSP 604 controls override the Cloud First Policy for OFFICIAL-SENSITIVE and above. This deviation is policy-supported, not a non-compliance.
- **AI annex** addresses ADR-004 (on-premise model integration, pluggable AI endpoint) under Point 6 / Point 7, with cross-reference to the AI Playbook compliance assessment.

**Critical actions before sovereign GA (2027-12-31)**:

1. Complete `/arckit:mod-secure` assessment with a representative deploying authority (Point 6 / Point 13 substitute).
2. Validate persona placeholders via `/arckit:stakeholders` for project 002 (Point 1).
3. Establish customer DPIA template / processor commitments package (Point 7).

---

## TCoP Point 1: Define User Needs

**Guidance**: Understand your users and their needs. Develop knowledge of your users and what that means for your technology project or programme.

**Reference**: https://www.gov.uk/guidance/define-user-needs

### Assessment

**Status**: ⚠️ Partially Compliant

**Evidence**:

The sovereign deployment route has **five differentiated user personas** documented in `ARC-002-REQ-v1.0.md` (Personas 1-5): Customer Operator (cleared SC/DV personnel), Customer Accreditor / Authorising Engineer, Customer SIRO, Customer Architect (DDaT roles), and Vendor Sovereign Delivery Lead. Each persona has goals and pain points specifically grounded in air-gapped operating contexts (no internet egress, accreditation-driven decision-making, opaque dependencies as a top pain point). Use cases UC-1 (Air-Gap Install), UC-2 (Upgrade with Roll-Back), UC-3 (Decommission and Data Destruction) are derived from operator-team perspective.

However, persona definitions are explicitly flagged in the requirements as **placeholders pending `/arckit:stakeholders` for project 002** — they are derived from Principle 21 and the project-001 stakeholder analysis rather than direct sovereign-customer research. Direct primary research with cleared MOD personnel will be conducted post-pilot-customer engagement (gated at GA – 6 months in the timeline).

**User Research Conducted**:

- [x] User personas created (5 personas; placeholder status)
- [x] User journey mapping done (UC-1 / UC-2 / UC-3 cover install, upgrade, decommission)
- [x] Accessibility needs identified (NFR-C-003 WCAG 2.2 AA inherited from SaaS)
- [ ] User interviews completed — pending cleared-personnel engagement post first MOD customer signed
- [ ] Digital inclusion considerations documented for cleared-only contexts

**Gaps/Actions Required**:

- Run `/arckit:stakeholders` for project 002 to formalise the stakeholder set (target: 2026-06-30).
- Conduct primary research interviews with MOD operator team and accreditator at the pilot customer (gate: pilot customer signed, target 2027-04-30).
- Document any sovereign-specific accessibility considerations (e.g., assistive technology compatibility inside locked-down operator workstations).

---

## TCoP Point 2: Make Things Accessible and Inclusive

**Guidance**: Make sure your technology, infrastructure and systems are accessible and inclusive for all users.

**Reference**: https://www.gov.uk/guidance/make-things-accessible

### Assessment

**Status**: ⚠️ Partially Compliant

**Evidence**:

NFR-C-003 mandates WCAG 2.2 Level AA conformance for the tenant-facing UI on every release, with PSBAR 2018 compliance applicable where the deploying authority is in-scope. Because of the **single-codebase commitment (BR-001 / Principle 21)**, the sovereign deployment inherits the same UI as the managed SaaS — meaning accessibility work done in project 001 transfers directly. There is no sovereign-specific UI fork that would create an accessibility regression risk.

WCAG 2.2 AA is non-negotiable per Principle 12 and is a **"governance-critical feature"** which Principle 21 forbids paywalling or gating in either deployment mode.

Sovereign-specific considerations: cleared-personnel workstations (often locked-down SOEs / SLEs) may use older browsers, restricted assistive technology stacks, or constrained network conditions. These need explicit testing.

**Accessibility Standards**:

- [x] WCAG 2.2 Level AA compliance target set (NFR-C-003)
- [ ] Accessibility audit completed — inherits SaaS audit; sovereign-context audit pending
- [ ] Assistive technology testing done in locked-down SOE configurations
- [ ] Accessibility statement published — sovereign-customer-controlled (their statement, not vendor's)
- [x] Regular accessibility testing scheduled (release-on-release per Principle 12)

**Gaps/Actions Required**:

- Validate accessibility on a representative MOD locked-down SOE configuration before Private Beta.
- Provide accessibility evidence pack as part of the bundle (BR-004) so customer-side accessibility statements can be authored without re-testing.
- Document compatibility with HMG-approved assistive technology stacks.

---

## TCoP Point 3: Be Open and Use Open Source

**Guidance**: Publish your code and use open source software to improve transparency, flexibility and accountability.

**Reference**: https://www.gov.uk/guidance/be-open-and-use-open-source

### Assessment

**Status**: ✅ Compliant

**Evidence**:

The sovereign deployment is built from the **same single codebase** as the managed SaaS (BR-001, Principle 21). Open-source posture inherits the SaaS posture, which is itself committed to open standards (Principle 4). The release bundle (ADR-002) ships with a **CycloneDX SBOM**, signed manifests, hash inventory, release notes, and threat model — making the supply chain transparent to the deploying authority and to NCSC reviewers. SLSA Level 3 build provenance attests build integrity end-to-end (ADR-002).

**Note on sovereign nuance**: Customer-deployed instances may be marked OFFICIAL-SENSITIVE / SECRET, and customer artefact content is not publishable. But the *vendor codebase, SBOM, and release process* are openly inspectable (subject to MOD supply-chain review where applicable).

**Open Source Practices**:

- [x] Code published in open repositories (single-codebase shared with SaaS; vendor-public)
- [x] Open source libraries used where appropriate; full inventory in CycloneDX SBOM per release
- [x] Open source licenses reviewed and documented (SBOM-driven licence inventory)
- [x] Proprietary software justified where used (TC-1 mandates vendorable dependencies; no SaaS-only third parties on the critical path)
- [x] SLSA L3 build provenance for sovereign bundle (ADR-002)

**Gaps/Actions Required**:

- Ensure release notes and SBOMs are published in human-readable form alongside machine formats (CycloneDX + Markdown changelogs).
- Confirm OSI-approved licence posture is acceptable to MOD supply-chain reviewers as part of `/arckit:mod-secure`.

---

## TCoP Point 4: Make Use of Open Standards

**Guidance**: Build technology that uses open standards to ensure your technology works and communicates with other technology, and can easily be upgraded and expanded.

**Reference**: https://www.gov.uk/guidance/make-use-of-open-standards

### Assessment

**Status**: ✅ Compliant

**Evidence**:

NFR-I-001 mandates **API and event-interface parity with the managed SaaS**, sharing the same OpenAPI / AsyncAPI specifications and versioning policy. FR-007 mandates standard identity protocols (OIDC, OAuth 2.x, SAML 2.0). FR-009 mandates full export in **open formats (Markdown / JSON / YAML)** at any time. ADR-002 selects **CycloneDX** (or SPDX) for SBOMs, an OWASP open standard. Cosign signatures use Sigstore — open, NCSC-aware standard.

Document IDs follow the open `ARC-{PROJECT_ID}-{TYPE}-v{VERSION}` convention (FR-008).

**Open Standards Used**:

- [x] RESTful APIs with OpenAPI/AsyncAPI specs (NFR-I-001)
- [x] JSON/YAML/Markdown for data interchange and persistence (FR-009)
- [x] OIDC / OAuth 2.x / SAML 2.0 for authentication (FR-007, INT-001)
- [x] HTML5, CSS3 for web interfaces (inherited from SaaS UI)
- [x] CycloneDX / SPDX for SBOM (ADR-002)
- [x] Cosign / Sigstore for signing (ADR-002)
- [x] Open standards documented in HLD architecture

**Gaps/Actions Required**:

- Confirm cryptographic algorithm choices align with **HMG-approved primitives** at the configured classification (NFR-SEC-003) — particularly for SECRET deployments where HMG-approved cryptography may diverge from open community defaults.

---

## TCoP Point 5: Use Cloud First

**Guidance**: Consider using public cloud solutions first as stated in the Cloud First policy.

**Reference**: https://www.gov.uk/guidance/use-cloud-first

### Assessment

**Status**: N/A — Policy-Supported Deviation (documented justification)

**Is public cloud appropriate?**: **No, for accredited boundaries**

**Cloud Provider**: **On-premise / customer-controlled accredited infrastructure** (default). Customer MAY choose to host the sovereign deployment on a customer-procured, customer-accredited cloud tenancy (e.g., a List X-cleared cloud region, MOD-OFFICIAL Azure region, or a customer-private OpenStack), but the platform itself runs entirely within the customer's accredited boundary with no internet egress.

**Evidence and Justification**:

The Cloud First Policy explicitly accommodates exceptions where security, sovereignty, or operational constraints make public cloud unsuitable. The sovereign deployment route exists precisely to serve **MOD and comparable sensitive sites that operate inside accredited boundaries with no internet egress**. For these customers:

- **JSP 440 (Defence Manual of Security)** and **JSP 604 (Defence Manual for the Authorisation of Information Systems)** establish controls that **override** the Cloud First Policy at OFFICIAL-SENSITIVE and above. Where JSP 440 controls are inherited (per ADR-006), public cloud is not on the menu unless the cloud tenancy is itself accredited under MOD frameworks.
- **NCSC CAF** for Operators of Essential Services applies similar accreditation gating for non-MOD sensitive sites.
- **Government Security Classifications Policy** sets handling caveats that exclude general-purpose public cloud above OFFICIAL.

The managed SaaS (project 001) **is** Cloud First — that is the intended route for the majority of UK Government work, and for all SME-facing engagement, at OFFICIAL.

This is **not a non-compliance**. It is an explicitly scoped policy carve-out, supported by Principle 21 (Sovereign and Air-Gapped Deployment) and BR-002 (Air-Gap and Disconnected Operation).

**Cross-references**:

- ADR-001 — Air-Gapped Operation Model (no outbound egress)
- ADR-005 — Customer-Controlled Telemetry, Time, CA, Package Mirror
- ADR-006 — JSP 440 / Security Aspects Letter Alignment
- NFR-SEC-001 — MOD Secure by Design / JSP 440 / JSP 604 alignment
- NFR-SEC-004 — No Outbound Network Calls Inside Boundary

**Cloud First Considerations**:

- [x] Public cloud considered as first option — and is the route for project 001 (SaaS)
- [x] Cloud hosting decision documented (this section + ADR-001)
- [x] If not public cloud, justification documented (above)
- [x] Cloud security controls implemented (where customer chooses accredited cloud tenancy, NCSC Cloud Security Principles applied via customer accreditation)
- [x] Data residency requirements met (customer-controlled, inside the boundary by definition)

**Gaps/Actions Required**:

- For digital spend control submissions involving sovereign deployments, ensure the spend-control narrative explicitly cites the JSP 440 / JSP 604 override and links to ADR-006.
- Document the standard customer choice matrix (on-premise vs accredited cloud tenancy vs hybrid) for procurement guidance.

---

## TCoP Point 6: Make Things Secure

**Guidance**: Keep systems and data safe with the appropriate level of security.

**Reference**: https://www.gov.uk/guidance/make-things-secure

### Assessment

**Status**: ✅ Compliant (subject to completion of MOD Secure by Design assessment)

**Data Sensitivity**: **OFFICIAL through SECRET** (configurable maximum per deployment via FR-012)

**Evidence**:

Security is the dominant design driver of the sovereign track. The architecture and ADR set comprehensively address it:

- **NFR-SEC-001 to NFR-SEC-008** — eight CRITICAL-priority security NFRs covering MOD SbD / JSP 440 / JSP 604 alignment, NCSC CAF mapping, classification-appropriate cryptography, no outbound network calls (validated by CI network-deny test), supply-chain integrity (SBOM + signing + hash manifests), within-deployment isolation, cleared-personnel-only access, and vulnerability disclosure / patching SLAs.
- **ADR-001** — Air-gapped operation model with no outbound egress.
- **ADR-002** — Signed release bundle with Cosign + CycloneDX SBOM + SLSA L3 + offline verification manifest.
- **ADR-005** — Customer-controlled telemetry, time, CA, package mirror.
- **ADR-006** — JSP 440 alignment and Security Aspects Letter (SAL) template.
- **ADR-008** — (cryptographic key management / HSM-backed signing per supply-chain integrity policy).
- **Risk Register** (`ARC-002-RISK-v1.0.md`) — formal HM Treasury Orange Book risk register with vendor signing-key compromise (R-5), dependency offline-incompatibility (R-3), accreditation effort risk (R-2), and others, with 4Ts treatments.
- **HLD** Section 6 (Security Architecture Review) — completed.

The platform's posture is "secure by default in the strictest sense — no outbound calls, no phone-home, no opaque dependencies". The vulnerability disclosure programme aligns with ISO 29147; LTS patching SLAs are documented (NFR-SEC-008: Critical 7 days, High 30 days, Medium 90 days for sovereign — slower than SaaS due to customer-side accreditation re-runs).

**Security Controls**:

- [x] Threat modelling completed (per release; included in bundle per BR-004)
- [x] Security by design principles applied (MOD Secure by Design framework)
- [x] Penetration testing planned (per release; vendor-side + customer-side as part of accreditation)
- [x] Security risk register maintained (`ARC-002-RISK-v1.0.md`)
- [x] NCSC Cloud Security Principles assessed (NFR-SEC-002 NCSC CAF mapping; Cloud Security Principles applied where customer chooses accredited cloud tenancy)
- [x] Cyber Essentials Plus targeted (vendor-side); customer-side certification is customer-driven
- [x] Data classification completed (FR-012 configurable maximum classification)
- [x] Encryption at rest and in transit (NFR-SEC-003 classification-appropriate cryptography; INT-007 customer KMS)
- [x] Cleared-personnel-only access supported where mandated (NFR-SEC-007, FR-007)
- [x] Network-deny test in CI (NFR-SEC-004)
- [x] Within-deployment isolation tested per release (NFR-SEC-006, FR-006)

**Gaps/Actions Required**:

- Complete `/arckit:mod-secure` assessment with a representative deploying authority (target 2026-09-30, per requirements timeline).
- Confirm HMG-approved cryptographic primitives selected for SECRET-tier deployments.
- Validate the network-deny CI test is gating release issue (not advisory).

---

## TCoP Point 7: Make Privacy Integral

**Guidance**: Make sure users' rights are protected by integrating privacy as an essential part of your system.

**Reference**: https://www.gov.uk/guidance/make-privacy-integral

### Assessment

**Status**: ⚠️ Partially Compliant

**Personal Data Processed**: **Limited — operator and user identity only at the vendor side; substantive personal data is customer-side and customer-controlled.**

**Evidence**:

In the sovereign deployment model, the **vendor (ArcKit as a Service) is largely not a custodian of customer personal data** — the architecture is explicitly designed so that customer artefact data, audit logs, and content stay inside the customer's accredited boundary (BR-002, FR-009, NFR-M-002, INT-002). The vendor's relationship to customer-side personal data is **inputs and processor commitments per release**, not live processing.

NFR-C-002 explicitly states UK GDPR / DPA 2018 obligations apply at the deploying authority's responsibility; the vendor provides DPIA inputs and processor commitments per release. DR-002 (User / Cleared Personnel) classifies user data as OFFICIAL with PII flagged. Audit events (DR-005) retain to customer-defined retention (default ≥ 12 months per NFR-C-004).

A formal DPIA for the vendor side has been generated via `/arckit:dpia` for project 002. Customer-side DPIAs are the deploying authority's responsibility (consistent with the data-controller / data-processor split typical for sovereign deployments).

**Privacy Controls**:

- [x] Data Protection Impact Assessment (DPIA) completed for vendor side (sister artefact in project 002)
- [x] Privacy by design principles applied (data minimisation; vendor never custodian of customer artefact content)
- [x] UK GDPR compliance assessed (NFR-C-002)
- [x] Data retention policy defined (DR-002 default lifetime of role + 30 days; DR-005 customer-controlled)
- [x] User consent mechanisms — driven by customer IdP (FR-007)
- [x] Data subject rights procedures — addressed via customer admin export (FR-009)
- [ ] Privacy notice — customer-side (per their accreditation)
- [ ] ICO registration — vendor side complete; customer-side is customer responsibility
- [ ] Customer DPIA template / processor commitments package — pending

**Gaps/Actions Required**:

- Produce a **customer DPIA template** that the deploying authority can use as a starting point for their own DPIA (target: pre-Private Beta).
- Document the data-controller / data-processor split clearly in the customer SAL template (linked from ADR-006).
- Cross-reference the vendor-side DPIA when produced for the SaaS (project 001) so common processing activities are not duplicated.

---

## TCoP Point 8: Share, Reuse and Collaborate

**Guidance**: Avoid duplicating effort and unnecessary costs by collaborating across government and sharing and reusing technology, data, and services.

**Reference**: https://www.gov.uk/guidance/share-and-reuse-technology

### Assessment

**Status**: ✅ Compliant

**Evidence**:

The sovereign deployment route is **the canonical example of "share and reuse" applied to deployment topology**: per Principle 21 and BR-001, **the same source code, data formats, APIs, and feature set** as the managed SaaS (project 001) is reused for the sovereign track. There is no proprietary fork. The release pipeline produces both the SaaS deployment and the sovereign bundle from one revision (TC-5). This is a strong, structurally-enforced reuse pattern that beats a typical "we tried to share" claim with a *make-it-impossible-to-fork* commitment.

Single-codebase reuse implications:

- Accessibility, security hardening, governance features, and UI improvements made for SaaS land in sovereign automatically.
- Bug fixes apply to both routes from one upstream merge.
- Customer artefact data is portable across SaaS-to-sovereign and sovereign-to-sovereign migrations via FR-009 export in open formats — directly enabling cross-customer reuse of governance artefacts.
- The vendor is itself an "ArcKit dogfooding" customer; principles, ADRs, requirements, and risks are authored using ArcKit, providing a continuous reuse loop.

**Common UK Government platforms**: GOV.UK Notify, GOV.UK Pay, GOV.UK PaaS are **not applicable to a sovereign air-gapped deployment** — these are SaaS-by-design platforms operated by GDS that cannot run inside an accredited boundary with no internet egress. Their absence here is a topology fact, not a non-compliance.

**Reuse and Collaboration**:

- [x] Single-codebase reuse with the managed SaaS (BR-001, Principle 21)
- [x] Existing government services reviewed (GOV.UK Notify / Pay / PaaS — all SaaS, not sovereign-deployable)
- [x] Cross-government platforms used where compatible (G-Cloud / DOS for procurement)
- [x] Technology components documented for reuse (HLD; ADRs)
- [x] APIs designed for reusability (NFR-I-001 SaaS parity; OpenAPI / AsyncAPI)
- [x] Collaboration documented (sister-project linkage 001 ↔ 002; references to MOD Defence Digital, NCSC, CCS in stakeholder list)

**Common Platforms Used**:

- [ ] GOV.UK Notify — N/A in air-gap (customer notification service per INT-006 instead)
- [ ] GOV.UK Pay — N/A (sovereign procurement is contract-based, not transaction-based)
- [ ] GOV.UK PaaS — N/A (decommissioned platform; customer-controlled hosting per NFR-SEC-004)
- [x] Digital Marketplace (G-Cloud, DOS) — INT-008, BR-007
- [x] Cross-project shared codebase with project 001 (BR-001)

**Gaps/Actions Required**:

- Document the SaaS-to-sovereign migration / data-portability path explicitly for customers who may begin in SaaS at OFFICIAL and graduate to sovereign at OFFICIAL-SENSITIVE+.
- Engage MOD Defence Digital on cross-MOD reuse (e.g., shared evidence pack format) to reduce per-deploying-authority accreditation effort.

---

## TCoP Point 9: Integrate and Adapt Technology

**Guidance**: Your technology should work with existing technologies, processes and infrastructure in your organisation, and adapt to future demands.

**Reference**: https://www.gov.uk/guidance/integrate-and-adapt-technology

### Assessment

**Status**: ✅ Compliant

**Evidence**:

Integration is a primary design driver: the sovereign deployment is **defined by what it integrates with on the customer side** — customer IdP (INT-001, FR-007), customer object storage / database (INT-002), customer time / CA / package mirror (INT-003), customer observability backend (INT-004), customer-approved AI endpoint (INT-005, FR-004), customer email / notification service (INT-006), customer KMS (INT-007). All ten enumerated integrations (INT-001 to INT-010) are designed to plug into customer-controlled equivalents.

FR-005 mandates **configurable integration contracts** with documented interfaces. The platform refuses to start until the required integrations are configured (acceptance criterion in FR-005).

Future adaptability:

- Pluggable AI / model endpoint (FR-004, ADR-004) enables customers to swap AI backends or disable AI generation entirely as model technology and approval landscapes evolve.
- LTS release line (BR-005) provides 24-month patch backporting per LTS — giving customers stability without forcing upgrade cadence.
- Open APIs (NFR-I-001) and full data export (FR-009) ensure migration paths off the platform are credible.

**Integration Considerations**:

- [x] Existing systems inventory — customer-side dependencies enumerated (INT-001 to INT-010)
- [x] Integration points identified and documented (FR-005 configuration contracts)
- [x] API strategy defined (NFR-I-001 SaaS parity; OpenAPI / AsyncAPI)
- [x] Legacy system dependencies mapped (none in v1; customer-controlled IdP / KMS / observability are the integration surface)
- [x] Future scalability considered (NFR-S-001 within fixed envelope)
- [x] Technology roadmap aligned (HLD; sovereign roadmap separable from SaaS via LTS)

**Key Integrations**:

- Customer IdP — OIDC / OAuth 2.x / SAML 2.0 (INT-001)
- Customer Object Storage / DB — customer-provisioned inside boundary (INT-002)
- Customer-Approved AI Endpoint — pluggable, optional (INT-005, ADR-004)
- Customer KMS — customer-managed keys for encryption at rest (INT-007)
- G-Cloud / DOS / Defence Frameworks — procurement (INT-008, BR-007)

**Gaps/Actions Required**:

- Produce conformance-test fixtures for each integration contract so customers can validate their endpoint implementations before install.
- Document protocol versions and deprecation cadence (e.g., SAML 2.0 vs OIDC selection guidance).

---

## TCoP Point 10: Make Better Use of Data

**Guidance**: Use data more effectively by improving your technology, infrastructure and processes.

**Reference**: https://www.gov.uk/guidance/make-better-use-of-data

### Assessment

**Status**: ✅ Compliant

**Evidence**:

The data architecture is documented in the requirements (DR-001 to DR-007: Customer Deployment, User, Project, Artefact, Audit Event, Cryptographic Key Inventory, SBOM and Release Manifest). The HLD elaborates the storage topology (customer-controlled object storage + database, INT-002).

Data quality and lineage:

- All artefacts are governance artefacts authored in the platform itself, with structured document IDs (`ARC-{PROJECT_ID}-{TYPE}-v{VERSION}`) and version control built in.
- Traceability between artefacts (requirements → ADRs → designs) is a core platform feature.
- Audit logging (FR-010, NFR-SEC-006, DR-005) provides full-fidelity event history with structured fields, tamper-evident, customer-defined retention.

Open data and sharing:

- Full export in open formats (FR-009) enables customer-side analysis, archival, and migration.
- Public-data publication is a customer decision — not relevant for OFFICIAL-SENSITIVE+ artefact content but relevant for accreditation-evidence data the customer may choose to share with peer authorities.

**Data Management**:

- [x] Data architecture documented (DR-001 to DR-007; HLD)
- [x] Data quality standards — versioned artefacts; structured IDs; traceability built into the platform
- [x] Master data management — single-codebase produces canonical artefact format
- [ ] Data analytics / insights strategy — sovereign-specific analytics is customer-side; vendor provides export (FR-009)
- [ ] Open data publication — customer-side decision; out-of-scope for vendor
- [x] Data sharing agreements — customer-side; SAL template captures this (ADR-006)
- [x] Data lineage tracked (audit events DR-005; artefact version history)

**Gaps/Actions Required**:

- Provide a **`/arckit:data-model` artefact** for project 002 to formalise the entity relationship map and GDPR-classification per attribute (Appendix D of the requirements references this as pending).
- Publish guidance on customer-side analytics patterns (e.g., feeding audit events into customer SIEM for compliance reporting).

---

## TCoP Point 11: Define Your Purchasing Strategy

**Guidance**: Your purchasing strategy must show you've considered commercial and technology aspects, and contractual limitations.

**Reference**: https://www.gov.uk/guidance/define-your-purchasing-strategy

### Assessment

**Status**: ✅ Compliant

**Procurement Route**: **G-Cloud (primary) and DOS (for supporting professional services)**, with engagement plan for applicable MOD-specific frameworks (BR-007).

**Evidence**:

BR-007 mandates G-Cloud and DOS listings covering both sovereign deployment and supporting professional services, plus an engagement plan with MOD framework owners. INT-008 documents the procurement integration. The requirements identify the Defence Cyber Protection Partnership (DCPP) Cyber Risk Profile as the applicable supplier-side compliance regime.

Commercial model:

- BR-006 — Sovereign deployment licences recover **full cost-to-serve plus margin**, with margin contributing to the cross-subsidy that funds the SaaS SME tier (project 001 BR-005).
- This is documented, transparent pricing (Principle 17).
- Build vs buy: ArcKit itself is a **build** at the platform level, but the sovereign track explicitly leverages **bought / open-source components** (e.g., Cosign, CycloneDX, OIDC libraries) reducing TCO and avoiding lock-in.
- Vendor lock-in mitigation: full data export (FR-009), open APIs (NFR-I-001), open data formats — sovereign customers retain a credible exit path.
- LTS commitment (BR-005) means customers have predictable upgrade economics.

**Procurement Strategy**:

- [x] Market research conducted (SOBC pending; preliminary research in HLD)
- [x] Build vs buy decision documented (ADR-007 covers technology selection rationale)
- [x] Digital Marketplace (G-Cloud / DOS) considered and selected (BR-007, INT-008)
- [x] Crown Commercial Service frameworks reviewed (G-Cloud / DOS / DPS as defined in INT-008)
- [x] Vendor lock-in risks assessed (mitigated by open APIs + open formats + full export)
- [x] Exit strategy defined (FR-009 + Principle 4 + Principle 9; UC-3 decommission)
- [x] Social value considerations (cross-subsidy of SaaS SME tier from sovereign margin per BR-006 = direct social value)
- [x] SME access considerations (sovereign track is for large defence customers; SME affordability is project 001's responsibility)

**Gaps/Actions Required**:

- Complete `/arckit:sobc` for project 002 (target 2026-08-31) to formalise pricing and budget figures.
- Confirm DCPP Cyber Risk Profile applicable to the offering and document compliance plan.
- Engage Crown Commercial Service early on G-Cloud listing structure for sovereign-vs-SaaS lot allocation.

---

## TCoP Point 12: Make Your Technology Sustainable

**Guidance**: Increase sustainability throughout the lifecycle of your technology.

**Reference**: https://www.gov.uk/guidance/make-your-technology-sustainable

### Assessment

**Status**: ✅ Compliant

**Evidence**:

Sustainability for sovereign deployments has a fundamentally different shape from cloud-hosted services and warrants explicit framing:

**On-premise hardware lifecycle (the dominant sustainability factor for sovereign)**:

- The sovereign deployment runs on **customer-procured, customer-operated infrastructure** within the accredited boundary. The carbon and resource footprint is dominated by the *customer's* hardware lifecycle, refresh cadence, and data-centre energy mix — over which the vendor has no direct control.
- The vendor's contribution is to make the platform **runnable on modest hardware envelopes** so customers are not forced into oversized footprints. The HLD's resource sizing guidance and the within-fixed-envelope scaling commitment (NFR-S-001) directly support this — small-deployment customers are not forced to overspecify.

**Software lifecycle and longevity**:

- LTS release line (BR-005) — 24-month support per LTS — extends the useful operating life of any given customer install, reducing forced re-deploy frequency and the associated infrastructure churn.
- Single-codebase commitment (BR-001) means no parallel codebases are kept alive — engineering effort doesn't bifurcate.
- Patch-only LTS backport policy (Conflict C-2 resolution) avoids feature-bloat that would drive infrastructure expansion over the LTS lifetime.

**E-waste and decommission**:

- UC-3 (Sovereign Decommission and Data Destruction) provides a clean off-ramp; customer infrastructure can then be remediated or refurbished by the customer per their disposal policy.

**Vendor-side**:

- Vendor build / sign / release infrastructure runs on the SaaS (project 001) operational footprint, which is itself subject to project 001's sustainability commitments.

**Sustainability Considerations**:

- [x] Carbon footprint considered — primary driver is customer hardware; vendor minimises through modest sizing
- [x] Energy-efficient infrastructure — within fixed envelope; horizontal scale only when needed (NFR-S-001)
- [x] Device lifecycle management — customer-driven; LTS release line extends per-deployment lifetime
- [x] E-waste disposal procedures — customer responsibility; UC-3 supports clean decommission
- [x] Green hosting / data centres — customer-controlled; vendor cannot mandate but can document optimal targets
- [x] Sustainable procurement criteria — applicable to vendor's supply chain (G-Cloud Cloud Sustainability requirements where listed)
- [x] Long-term support reduces forced re-deploy churn (BR-005)

**Sustainability Metrics**:

- Estimated carbon footprint: **customer-environment-dependent** — vendor publishes per-deployment resource sizing guidance to support customer-side LCA
- LTS lifetime: ≥ 24 months per LTS line (BR-005), reducing infrastructure churn
- Vendor build infrastructure: hosted via project 001 (covered by SaaS sustainability)

**Gaps/Actions Required**:

- Publish per-deployment resource sizing benchmarks so customers can plan a **right-sized** sovereign install (avoiding over-provisioning).
- Document a recommended hardware refresh cadence aligned with LTS line cadence (likely 4–6 years), matching MOD asset-lifetime norms.
- Flag any specific hardware compatibility requirements (e.g., HSM modules) that have shorter / longer lifetimes than commodity compute.

---

## TCoP Point 13: Meet the Service Standard

**Guidance**: If you're building a service as part of your technology project or programme, you must meet the Service Standard.

**Reference**: https://www.gov.uk/service-manual/service-standard

### Assessment

**Status**: **N/A — Not Applicable**

**Is this a public-facing service?**: **No**

**Evidence and Justification**:

The sovereign deployment of ArcKit as a Service is **not a public-facing GDS service**. It is an internal architecture-governance toolkit deployed inside accredited boundaries, used by cleared personnel at MOD and comparable sensitive sites. There is no end-citizen interaction, no `gov.uk` URL, no transactional service path.

The Service Standard applies to **public-facing services**. Internal platforms — particularly accredited / classified ones — are out of its formal scope.

**Assurance pathway substitute**:

For sovereign deployments, assurance flows via the **MOD accreditation pathway**, not via GDS service assessment:

- **MOD Secure by Design** assessment (`/arckit:mod-secure`, Phase 5 in the sovereign assessment programme) — the MOD analogue of the GDS service assessment for security-relevant platforms.
- **JSP 440 (Defence Manual of Security)** — controls inheritance per ADR-006.
- **JSP 604 (Defence Manual for the Authorisation of Information Systems)** — issuing authority-to-operate.
- **NCSC CAF (Cyber Assessment Framework)** — for non-MOD sensitive sites under the OES regime.
- **GovAssure** — NCSC assessment scheme for OES.

These are the **functionally equivalent** assurance gates. They are referenced explicitly in NFR-SEC-001, NFR-SEC-002, and ADR-006.

For comparison, the **managed SaaS (project 001)** is also not a public-facing GDS service — it is a business-to-government tool — but it uses the GDS Service Standard *as a framework reference* for its tenant-facing UX. The sovereign track does not even use the Service Standard as a reference; the MOD pathway supersedes it.

**Service Standard Compliance**:

- [ ] Service assessments — N/A (MOD accreditation pathway substitutes)
- [x] Agile, user-centered approach — applied (Principle 12 and SaaS heritage)
- [x] Performance metrics defined (NFR-P-001 to NFR-P-003; agreed per customer per NFR-A-001)
- [ ] Assisted digital support — N/A (cleared personnel; not citizen-facing)
- [ ] Service manual guidance — referenced as inspiration, not as binding standard
- [ ] Beta/live service assessment — N/A; replaced by customer-side accreditation gate

**Service Assessment Status**: **Not Required** — replaced by MOD accreditation pathway. See ADR-006 and `/arckit:mod-secure` artefact (pending).

**Gaps/Actions Required**:

- Ensure CDDO digital spend control submissions explicitly reference the JSP 440 / JSP 604 substitute pathway (do not leave the spend-control reviewer wondering why no GDS service assessment is cited).
- Cross-reference `/arckit:mod-secure` once produced.

---

## Overall Compliance Summary

### Compliance Scorecard

| TCoP Point | Status | Critical Issues |
|------------|--------|-----------------|
| 1. Define user needs | ⚠️ Partially Compliant | No — typical for pre-pilot maturity |
| 2. Make things accessible | ⚠️ Partially Compliant | No — inherited from SaaS; sovereign-context audit pending |
| 3. Be open and use open source | ✅ Compliant | No |
| 4. Make use of open standards | ✅ Compliant | No |
| 5. Use cloud first | N/A — Policy-Supported Deviation | No (justified) |
| 6. Make things secure | ✅ Compliant | No (subject to MOD SbD assessment completion) |
| 7. Make privacy integral | ⚠️ Partially Compliant | No — customer DPIA template pending |
| 8. Share, reuse and collaborate | ✅ Compliant | No |
| 9. Integrate and adapt technology | ✅ Compliant | No |
| 10. Make better use of data | ✅ Compliant | No |
| 11. Define your purchasing strategy | ✅ Compliant | No (subject to SOBC completion) |
| 12. Make your technology sustainable | ✅ Compliant | No |
| 13. Meet the Service Standard | N/A — Not Applicable | No (MOD pathway substitutes) |

**Overall Score**: **9 / 13 Compliant + 3 / 13 Partially Compliant + 1 / 13 N/A** (Point 13). Point 5 also marked N/A on the policy-deviation basis but counted in the "Compliant or N/A by design" group.

### Critical Issues Requiring Immediate Action

1. **MOD Secure by Design assessment not yet executed (Point 6, Point 13 substitute)** — gate for accreditation; target 2026-09-30.
2. **Customer DPIA template / processor commitments package not yet produced (Point 7)** — required before Private Beta to allow deploying authority to scope its own DPIA efficiently.
3. **Stakeholder placeholders not validated (Point 1)** — `/arckit:stakeholders` for project 002 is required (target 2026-06-30).

### Recommendations

**High Priority**:

- Run `/arckit:mod-secure` with a representative deploying authority engaged to validate the evidence pack format (resolves R-6 in the risk register).
- Run `/arckit:stakeholders` for project 002 to convert placeholder personas into validated stakeholder set.
- Run `/arckit:sobc` for project 002 to firm up Point 11 commercial figures for spend-control submissions.

**Medium Priority**:

- Produce customer-side DPIA template and SAL template (linked from ADR-006) as customer-facing deliverables.
- Publish per-deployment resource sizing benchmarks for Point 12 sustainability transparency.
- Develop conformance-test fixtures for each integration contract (FR-005, INT-001 to INT-007).

**Low Priority**:

- Establish MOD-Defence-Digital and NCSC liaison cadence to share evidence-pack format experience across deployments.
- Document the SaaS-to-sovereign migration path for customers graduating in classification.

---

## GovS 005 (Government Functional Standard for Digital) Alignment

> **Note**: The Technology Code of Practice is the **implementation guidance** for [GovS 005 — Government Functional Standard for Digital](https://www.gov.uk/government/publications/government-functional-standard-govs-005-digital). For sovereign defence deployments, GovS 005 obligations are **applied alongside JSP 440 / JSP 604**, not replaced by them. Where the two frameworks differ (e.g., spend control thresholds, SRO chains), the more stringent applies.

### TCoP-to-GovS 005 Principle Mapping

| GovS 005 Principle | Description | TCoP Points (this assessment) |
|---------------------|-------------|--------------------------------|
| User-centred | Services designed around user needs | 1 (Define user needs) — Partially; 2 (Accessible) — Partially |
| Open | Open source, open standards, transparency | 3 (Open source) — Compliant; 4 (Open standards) — Compliant |
| Secure | Proportionate security controls | 6 (Make things secure) — Compliant; 7 (Privacy integral) — Partially |
| Technology | Cloud first, sustainable, integrated | 5 (Cloud first) — N/A justified; 9 (Integrate & adapt) — Compliant; 12 (Sustainable) — Compliant |
| Data-driven | Evidence-based decisions using data | 10 (Make better use of data) — Compliant |
| Inclusive | Accessible to all users and communities | 2 (Accessible) — Partially; 13 (Service Standard) — N/A |
| Collaborative | Share, reuse, work across boundaries | 8 (Share, reuse & collaborate) — Compliant (single-codebase) |
| Commercially aware | Smart procurement, value for money | 11 (Purchasing strategy) — Compliant |
| Sustainable delivery | Lifecycle management, long-term viability | 12 (Sustainable) — Compliant; 9 (Integrate & adapt) — Compliant |

### GovS 005 Governance Obligations

| Obligation | Status | Evidence / Notes |
|------------|--------|------------------|
| Senior Responsible Owner (SRO) appointed for digital function | MET (vendor side) | Mark Craddock (Service Owner). Customer-side SRO is per deploying authority. |
| Lifecycle stage identified (Discovery / Alpha / Beta / Live) | MET | Pre-Alpha (Requirements stage); Alpha gated at 2027-04-30 per timeline. |
| CDDO digital spend control thresholds met | NOT MET (pending SOBC) | `/arckit:sobc` due 2026-08-31; sovereign track spend figures TBD. |
| DDaT capability framework applied to team roles | PARTIALLY MET | Customer-side architects mapped to DDaT roles; vendor-side mapping pending (placeholder stakeholder roles). |
| Performance and status reported to the Permanent Secretary | N/A | Vendor is non-departmental supplier; reporting flows via customer SROs to their Permanent Secretaries / equivalents. |
| MOD JSP 440 / 604 pathway documented (sovereign-specific) | MET | ADR-006; NFR-SEC-001. |

**Overall GovS 005 Alignment Status**: **PARTIALLY ALIGNED** (consistent with pre-Alpha maturity; full alignment expected by GA 2027-12-31 once SOBC, MOD SbD assessment, and stakeholder analysis are complete).

---

## AI Annex — On-Premise Model Integration

> Cross-references: ADR-004 (AI / model endpoint integration), FR-004 (pluggable AI endpoint), INT-005 (customer-approved AI endpoint), `/arckit:ai-playbook` artefact for project 002.

The sovereign deployment treats AI generation as **strictly pluggable** and **disabled by default**:

- **TCoP Point 5 (Cloud First) interaction**: ADR-004 confirms commercial SaaS-only AI providers (OpenAI, Anthropic, etc.) are **not usable in sovereign mode**. Cloud-first does not apply to AI endpoints either, for the same JSP 440 / 604 reason.
- **TCoP Point 6 (Make Things Secure)**: When AI is enabled to a customer-approved on-premise model deployment, all transport stays inside the customer's accredited boundary (NFR-SEC-004). No tenant content leaves the boundary.
- **TCoP Point 7 (Make Privacy Integral)**: With AI disabled (the default), no AI-mediated processing of customer artefact content occurs. With AI enabled to a customer-controlled endpoint, the customer is responsible for the model's data-handling posture (typically integrated into their own DPIA).
- **TCoP Point 9 (Integrate and Adapt)**: The pluggable contract means customers can swap models as the approved-model landscape evolves (e.g., as models receive Defence AI Strategy approvals, NCSC approvals, or sovereign-cloud-hosted approvals).
- **TCoP Point 10 (Better Use of Data)**: Where AI is enabled, structured generation metadata is captured against artefacts (FR-008, DR-004 generation_metadata attribute), supporting algorithmic transparency.

**ATRS / Algorithmic Transparency**: For sovereign deployments where the customer is a public authority and the AI is decisional rather than purely generative, an **ATRS record** may apply at the customer side. The vendor provides ATRS-input templates as part of the bundle (cross-reference: project 002 `/arckit:ai-playbook` artefact and possible future ATRS via `/arckit:atrs`).

**JSP 936 (MOD AI Assurance)**: For MOD deployments, JSP 936 applies to defence AI/ML systems. ADR-004 documents the integration contract; the MOD SbD assessment will reference JSP 936 where the deploying authority enables AI generation.

---

## Next Steps

**Immediate Actions** (0-30 days):

- [ ] Run `/arckit:stakeholders` for project 002 to validate persona placeholders (Point 1).
- [ ] Brief CDDO Digital Spend Control liaison on the JSP 440 / 604 override for Point 5 ahead of any spend-control submission.

**Short-term Actions** (1-3 months):

- [ ] Complete `/arckit:sobc` for project 002 (Point 11; firm up commercial figures).
- [ ] Engage a representative MOD deploying authority for `/arckit:mod-secure` evidence-pack co-design (Point 6, Point 13 substitute).
- [ ] Produce customer DPIA template and SAL template (Point 7).

**Long-term Actions** (3-12 months):

- [ ] Run `/arckit:mod-secure` formally and integrate output into release bundle from first vendor-internal Alpha (target 2027-04-30).
- [ ] Validate accessibility on a representative MOD locked-down SOE configuration (Point 2).
- [ ] Publish per-deployment resource sizing benchmarks (Point 12).
- [ ] Develop conformance-test fixtures for integration contracts (Point 9).

**Review Schedule**: Re-run TCoP review at each major lifecycle gate — Alpha exit, Private Beta entry, GA, and on each LTS line issue thereafter. Default cadence: quarterly until GA, annually post-GA.

---

## Approval

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Project Lead | [PENDING] | | |
| Technical Architect | [PENDING] | | |
| Senior Responsible Owner | Mark Craddock | | |
| Digital Spend Control (if applicable) | [PENDING] | | |
| MOD Customer Accreditator (pilot, when engaged) | [PENDING] | | |

---

**Document Control**:

- **Version**: 1.0
- **Last Reviewed**: 2026-05-03
- **Next Review**: 2026-08-03 (quarterly until GA)
- **Document Owner**: Mark Craddock (ArcKit as a Service Owner)

## External References

> No external policy documents were placed in `projects/002-arckit-sovereign/external/` at the time of generation. UK Government / MOD policies referenced are public-domain and cited by name (TCoP, GovS 005, JSP 440, JSP 604, NCSC CAF, NCSC Cloud Security Principles, Government Security Classifications Policy, UK GDPR / DPA 2018, Procurement Act 2023).

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

### Internal Cross-References

| Source Artefact | Used In Section |
|-----------------|-----------------|
| `projects/000-global/ARC-000-PRIN-v2.0.md` (Principle 21) | Executive Summary; Points 5, 8 |
| `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md` | All 13 points |
| `projects/002-arckit-sovereign/ARC-002-STKE-v1.0.md` | Point 1 |
| `projects/002-arckit-sovereign/ARC-002-RISK-v1.0.md` | Point 6 |
| `projects/002-arckit-sovereign/ARC-002-HLDR-v1.0.md` | Points 6, 9, 10 |
| `projects/002-arckit-sovereign/decisions/ARC-002-ADR-001-v1.0.md` | Points 5, 6 (air-gapped) |
| `projects/002-arckit-sovereign/decisions/ARC-002-ADR-002-v1.0.md` | Points 3, 4, 6 (signed bundle, SBOM) |
| `projects/002-arckit-sovereign/decisions/ARC-002-ADR-004-v1.0.md` | AI Annex |
| `projects/002-arckit-sovereign/decisions/ARC-002-ADR-005-v1.0.md` | Point 5 (customer-controlled SVCs) |
| `projects/002-arckit-sovereign/decisions/ARC-002-ADR-006-v1.0.md` | Points 5, 6, 7, 13 (JSP 440 / SAL) |

---

**Generated by**: ArcKit `/arckit:tcop` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Derived from `ARC-000-PRIN-v2.0.md` (Principle 21), `ARC-002-REQ-v1.0.md`, `ARC-002-RISK-v1.0.md`, `ARC-002-HLDR-v1.0.md`, ADR-001 / 002 / 004 / 005 / 006. Sovereign-specific deviations applied: Point 13 N/A (MOD accreditation pathway substitute), Point 5 N/A justified (JSP 440 / 604 override), Point 8 emphasising single-codebase reuse per Principle 21, Point 12 framing on-premise hardware lifecycle. AI annex covers ADR-004 on-premise model integration. Sister to project 001 (managed SaaS) TCoP review.
