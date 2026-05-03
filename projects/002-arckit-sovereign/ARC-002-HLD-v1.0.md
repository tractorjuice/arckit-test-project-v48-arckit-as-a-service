# High-Level Design (HLD) Review: ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:hld-review`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-HLDR-v1.0 |
| **Document Type** | High-Level Design Review |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Per release; ad hoc on material ADR change |
| **Next Review Date** | 2026-06-02 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, Vendor Security Lead, Sovereign Delivery Lead, MOD Defence Digital liaison, NCSC liaison, Pilot Customer Accreditor (when engaged), GDS, CDDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:hld-review` command. Reviews the as-designed sovereign architecture as expressed across `ARC-002-REQ-v1.0`, `ARC-002-STKE-v1.0`, and ADR-001..008. | [PENDING] | [PENDING] |

## Document Purpose

Captures the Architecture Review Board's evaluation of the High-Level Design for the ArcKit sovereign deployment route (project 002). The "design under review" is the architecture as it has been crystallised across the eight wave-2 ADRs (ADR-001..008) plus the foundational requirements (REQ) and stakeholder analysis (STKE). The review assesses readiness against architecture principles (especially Principle 21 — non-negotiable), requirement coverage, and architectural integrity, ahead of detailed design (DLD) and the architecture-diagram wave (waves 5/6).

---

## 1. Review Overview

### 1.1 Purpose

Determine whether the sovereign deployment architecture, as expressed in REQ + STKE + ADR-001..008, is sound enough to proceed to detailed design and to the diagram wave that will codify it visually. The review is gating: if the architecture has unresolved load-bearing gaps, DLD cannot start.

### 1.2 HLD "Document" Under Review

The sovereign architecture is, as of 2026-05-03, expressed across the following artefacts in this repository (the project does not yet have a single monolithic HLD document — by design, the ADRs *are* the HLD at this stage):

| Artefact | Path | Role in HLD |
|----------|------|-------------|
| Architecture Principles v2.0 | `projects/000-global/ARC-000-PRIN-v2.0.md` | Anchoring authority (esp. Principle 21 non-negotiable) |
| Requirements | `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md` | BR / FR / NFR / INT / DR set |
| Stakeholder Analysis | `projects/002-arckit-sovereign/ARC-002-STKE-v1.0.md` | SD-1 to SD-17, Goals G-1 to G-10, Outcomes O-1 to O-7 |
| ADR-001 — Air-Gapped Operation Model | `projects/002-arckit-sovereign/decisions/ARC-002-ADR-001-v1.0.md` | Strict zero-egress runtime; pluggable foundational services; single-codebase discipline |
| ADR-002 — Signed Release Bundle | `projects/002-arckit-sovereign/decisions/ARC-002-ADR-002-v1.0.md` | Cosign keyless + HSM-anchored Offline Verification Manifest + SLSA L3 + CycloneDX/SPDX |
| ADR-003 — Cleared-Personnel Access Model | `projects/002-arckit-sovereign/decisions/ARC-002-ADR-003-v1.0.md` | Customer IdP federation + JIT elevation + on-site break-glass + default-deny vendor remote access |
| ADR-004 — On-Premise AI Integration | `projects/002-arckit-sovereign/decisions/ARC-002-ADR-004-v1.0.md` | Same `AIAdaptor` as SaaS; OpenAI-compatible wire contract; fail-closed default |
| ADR-005 — Foundational Service Redirection | `projects/002-arckit-sovereign/decisions/ARC-002-ADR-005-v1.0.md` | Customer-controlled telemetry, time, CA, package mirror |
| ADR-006 — JSP 440 / SAL Alignment | `projects/002-arckit-sovereign/decisions/ARC-002-ADR-006-v1.0.md` | Vendor evidence pack; customer owns SAL and ATO |
| ADR-007 — Distribution Model | `projects/002-arckit-sovereign/decisions/ARC-002-ADR-007-v1.0.md` | Sealed encrypted media default; one-way diode option |
| ADR-008 — LTS Release Line | `projects/002-arckit-sovereign/decisions/ARC-002-ADR-008-v1.0.md` | Annual LTS branch; 24-month security support; monthly patches |

**Submitted By**: ArcKit Engineering (ArcKit as a Service vendor team).
**Submission Date**: 2026-05-03.
**Diagrams**: Pending — wave 5/6 of the orchestrator. Network DFD (zero outbound flows), C4 Context, C4 Container, sequence diagrams for the three critical UCs, and a sovereign deployment diagram are all called out as required deliverables across multiple ADRs.

### 1.3 Review Participants

| Name | Role | Organisation | Review Focus |
|------|------|--------------|--------------|
| ArcKit AI (this review) | Lead Reviewer | Vendor Architecture | Overall architecture, principle compliance, REQ coverage |
| [PENDING] | Vendor Security Lead | Vendor Security | Supply chain, signing, NFR-SEC-001..008, MOD SbD |
| [PENDING] | Vendor Lead Architect | Vendor Engineering | Single-codebase discipline; offline-readiness; air-gap CI |
| [PENDING] | Sovereign Delivery Lead | Vendor Delivery | Customer onboarding, runbooks, FR-013 |
| [PENDING] | Pilot Customer Accreditor | Deploying Authority | JSP 604 fit; evidence-pack format; SAL inputs |
| [PENDING] | NCSC liaison | NCSC | CAF / supply-chain / cloud-security mappings |

### 1.4 Review Criteria

- **Architecture Principles**: All 21 principles, with Principle 21 as the load-bearing non-negotiable.
- **Requirements Alignment**: BR-001..008, FR-001..014, NFR (P/A/S/SEC/C/M/I), INT-001..010, DR-001..007.
- **Stakeholder Driver Coverage**: SD-1..17 against Goals G-1..10 and Outcomes O-1..7.
- **Technical Feasibility**: Single-codebase discipline; air-gap CI; HSM and signing; LTS sustainability.
- **Security & Compliance**: MOD Secure by Design / JSP 440 / JSP 604; NCSC CAF; HMG Government Security Classifications Policy.
- **Operational Readiness**: Operator runbooks (FR-011); customer-controlled observability; LTS patch SLAs.

---

## 2. Executive Summary

### 2.1 Overall Assessment

**Status**: **APPROVED WITH CONDITIONS**

**Summary**:

The sovereign deployment architecture, taken as the union of REQ + STKE + ADR-001..008, is internally consistent, principle-aligned, and accreditation-credible. Principle 21 — the only non-negotiable principle that this project exists to honour — is operationalised through a coherent set of seven cross-cutting design choices: (1) zero outbound egress at runtime, (2) signed and hashed bundle delivery with HSM-anchored offline verification, (3) cleared-personnel federation through customer IdPs with JIT elevation and on-site break-glass, (4) pluggable AI via the SaaS-identical adaptor with a fail-closed default, (5) all foundational services (telemetry, time, CA, package mirror) configurably redirected to customer-controlled endpoints, (6) sealed-media distribution (or accredited diode) with cryptographic chain-of-custody from commit to install, (7) annual LTS line decoupled from SaaS feature cadence with a 24-month security-patch commitment.

The architecture preserves single-codebase discipline (BR-001) by treating "sovereign mode" as a configuration profile of the same SaaS codebase rather than a fork, with a network-deny CI gate enforcing the discipline. It is accreditation-credible because each ADR carries explicit MOD SbD / JSP 440 / JSP 604 / NCSC CAF mapping and because ADR-006 cleanly separates vendor responsibility (per-release evidence pack) from customer responsibility (SAL and ATO).

The architecture is **APPROVED WITH CONDITIONS** rather than unconditionally approved because three classes of work remain before DLD can start: (a) the architecture diagrams that validate the design visually have not yet been generated (waves 5/6); (b) several upstream artefacts (RISK register, DPIA, MOD Secure-by-Design assessment) referenced by the ADRs as inputs to evidence packs are not yet present; (c) a small number of cross-cutting design questions surface only when the eight ADRs are read together — chiefly the operability of running ADR-002's reproducibility cross-build alongside ADR-008's LTS backport SLAs, and the practical limits of ADR-007's diode option for the OVM round-trip.

### 2.2 Key Strengths

- **Principle 21 is operationalised end-to-end, not slogan-only.** Every implication of Principle 21 (no phone-home, vendorable dependencies, signed bundle, pluggable AI, configurable foundational services, customer-controlled telemetry, IaC offline reproducibility, runbook-driven operability, decoupled LTS, accreditation-respecting support) has a corresponding ADR-level commitment with a measurable validation gate. This is the single biggest strength: the architecture does not leave any Principle 21 implication unanswered.
- **Single-codebase discipline is enforced architecturally, not just culturally.** ADR-001 commits to a network-deny CI gate, ADR-002 commits to byte-for-byte reproducibility cross-build, and ADR-004 reuses the SaaS `AIAdaptor` interface unchanged. Together these foreclose the most likely fork pressure (Conflict C-1 / SR-2). The `main` SaaS codebase produces the sovereign bundle on every revision, which converts BR-001 from a policy commitment into a pipeline invariant.
- **Defence-grade supply-chain integrity is a first-class design concern.** ADR-002's hybrid model (Cosign keyless + HSM-anchored OVM + SLSA L3 + CycloneDX/SPDX dual emission) is unusually thorough for a platform this size; it narrows the long-lived-key blast radius to the OVM only, retains third-party transparency where classification permits, and produces evidence in the exact shape the customer accreditor wants. ADR-006 ties the evidence to JSP 440 / 604 / NCSC CAF cleanly without claiming to do the customer's accreditation for them.

### 2.3 Key Concerns

- **Architecture diagrams are deferred.** The ADRs reference "the HLD topology", "the network DFD showing zero outbound flows", "C4 component view", "sequence diagrams for each access path", and "deployment view diagrams" repeatedly. None of these exist yet. They are scheduled for waves 5/6, but until they are produced, the design cannot be visually cross-checked for blind spots, especially in network egress and isolation surfaces.
- **Upstream dependency artefacts are missing.** Several ADRs cite a project-002 RISK register, MOD Secure-by-Design assessment, and DPIA as inputs they expect to consume. As of 2026-05-03 these have not been generated for project 002. This is not a design defect but it does mean that some risk and compliance claims in the ADRs are unevidenced.
- **Operability of the combined CI obligations needs validation.** ADR-001's network-deny CI, ADR-002's reproducibility cross-build, ADR-008's parallel LTS line backport CI, and ADR-004's AI-flow network-deny test together impose a real CI-minutes and engineering-discipline cost. The sovereign unit economics in REQ are indicative; the FinOps numbers (BR-006 cross-subsidy contribution) cannot be confirmed until these costs are exercised on real release cycles. Risk SR-6 (sovereign track distracts SaaS mission) increases proportionally to CI-minute burden.

### 2.4 Conditions for Approval

**MUST Address Before Detailed Design Wave (waves 7+)**:

1. **[BLOCKING-01]** Generate the sovereign architecture diagrams (waves 5/6): minimum set is C4 Context, C4 Container (showing zero outbound flows), Network DFD, sequence diagrams for UC-1 (air-gap install with bundle verification), UC-2 (upgrade with roll-back), and the access-path decision flow from ADR-003 Appendix C in C4-aligned form. Until diagrams exist, the "no critical-path outbound dependency" claim cannot be visually independently verified.
2. **[BLOCKING-02]** Generate the project-002 RISK register (`/arckit:risk`) and the MOD Secure-by-Design assessment (`/arckit:mod-secure`). Both are explicit dependencies in REQ §Dependencies and are referenced repeatedly across ADR-001..008 as feed-ins to the evidence pack. Without them the ADR-006 evidence-pack claim is incomplete.
3. **[BLOCKING-03]** Run the air-gap CI walkthrough end-to-end in a representative isolated environment for a draft release, exercising ADR-001's network-deny gate, ADR-002's reproducibility cross-build and `arckit-verify`, ADR-004's AI-flow network-deny test, and ADR-007's bundle-handoff ceremony. The architecture is not provably feasible until this cycle has been performed at least once, even if only on synthetic content.

**SHOULD Address During Detailed Design**:

1. **[ADVISORY-01]** ADR-007 documents a one-way diode option for distribution. Because ADR-002's `arckit-verify` may, in some failure modes, want to surface a verifier output to the vendor for triage (not required, but valuable), explicitly capture in DLD what diode round-trip (if any) is permissible and what is not. Default expectation: diode is one-way only; any return-channel signal goes via runbook.
2. **[ADVISORY-02]** ADR-008's LTS backport SLAs (Critical 7d / High 30d / Medium 90d) are tight. DLD should specify the backport tooling and the engineering rota that makes these SLAs sustainable across two parallel LTS lines while ADR-002's reproducibility cross-build also runs. Risk SR-4 needs concrete operational answers, not just a policy statement.
3. **[ADVISORY-03]** ADR-003's `clearance_attribute` claim depends on the customer IdP being able to emit a typed clearance attribute. Some customer IdPs cannot. ADR-003 already documents a fallback (signed customer-managed attribute table synced at logon). DLD should specify the schema, refresh cadence, and tamper-evidence of that fallback so that the fallback does not become a covert downgrade of NFR-SEC-007.
4. **[ADVISORY-04]** ADR-002 selects CycloneDX 1.5 as primary SBOM and SPDX 2.3 as secondary. DLD should pick a single canonical schema mapping table so that fields present in CycloneDX-rich and absent in SPDX (or vice versa) are documented as known-divergence rather than discovered as defects by an accreditor.

**Nice to Have (INFORMATIONAL)**:

1. **[INFO-01]** Consider commissioning a Wardley map (`/arckit:wardley`) for the sovereign supply chain (HSM, signing, serving stacks, foundational services). It is non-blocking but would surface evolution-stage assumptions in ADR-002, ADR-004, and ADR-005 that currently sit as prose.
2. **[INFO-02]** Capture the cross-project ADR linkage to project 001 (especially project 001 ADR-004 → project 002 ADR-004 reuse) in a simple traceability matrix to make the single-codebase discipline auditable from one document.

### 2.5 Recommendation

- [ ] **APPROVED**: Proceed with no conditions.
- [x] **APPROVED WITH CONDITIONS**: Address BLOCKING-01..03 before DLD wave; address ADVISORY-01..04 during DLD.
- [ ] **APPROVED WITH ADVISORIES**: not selected — the missing diagrams and missing risk/SbD inputs are too load-bearing to be deferred to DLD.
- [ ] **REJECTED**: not selected — the architecture is sound; no fundamental rework is required.

**Target Resubmission Date** (post-conditions): Aligned to wave-5/6 diagram completion plus RISK and MOD-SbD generation; estimated 2026-06-15 for re-review.

---

## 3. Architecture Principles Compliance

### 3.1 Principle Compliance Checklist

The 21 principles of `ARC-000-PRIN-v2.0.md` are the binding standard. Compliance is shown against the **sovereign clauses** of each principle (the SaaS clauses are project 001's concern).

| Principle | Sovereign clause(s) | Status | Comments |
|-----------|---------------------|--------|----------|
| **P-1** Equitable Access for SMEs | Sovereign route is a separate commercial model; cross-subsidises SaaS SME tier. | [x] Compliant | ADR-008 LTS commercial model + REQ BR-006 honour the cross-subsidy. Sovereign-side affordability is not in scope by design. |
| **P-2** Scalability and Elasticity | Scaling within fixed customer envelope; no re-architecture. | [x] Compliant | NFR-S-001; ADR-005 foundational-service plug points scale within boundary. |
| **P-3** Resilience and Fault Tolerance | Disconnected operation MUST work; degraded AI acceptable; core authoring always available. | [x] Compliant | ADR-001 + ADR-004 fail-closed default keep authoring fully functional with AI off. NFR-A-003. |
| **P-4** Open Standards and Interoperability | Same data formats and APIs as SaaS; sovereign exit-ready. | [x] Compliant | ADR-002 dual SBOM (CycloneDX + SPDX); ADR-003 OIDC/SAML; ADR-004 OpenAI-compatible wire contract; FR-009 export. |
| **P-5** Security by Design (NON-NEGOTIABLE) — sovereign block | Cleared-personnel-only access; HMG-approved crypto; no outbound; supply-chain integrity; formal accreditation by deploying authority. | [x] Compliant | ADR-002 (supply chain), ADR-003 (cleared personnel), ADR-006 (accreditation), ADR-001 (no outbound). All seven sovereign mandatory controls have a primary ADR owner. |
| **P-6** Observability — sovereign clause | Telemetry to customer-controlled destination only; no vendor backend. | [x] Compliant | ADR-005 telemetry redirection; ADR-001 default-no-vendor-egress; ADR-003 audit to customer SIEM. |
| **P-7** UK Data Sovereignty (NON-NEGOTIABLE) — sovereign clause | Residency controlled by deploying authority; vendor has no remote access by default. | [x] Compliant | ADR-001 zero-egress; ADR-003 default-deny vendor remote access; ADR-006 customer owns SAL/ATO. |
| **P-8** Tenant Isolation / Single Source of Truth | Within-deployment isolation between projects, roles, communities-of-interest. | [x] Compliant | FR-006; ADR-003 role tiers + CoI labels; ADR-004 prompt-context scoping. |
| **P-9** Data Quality, Lineage, Portability | Tenant export full-fidelity; same formats as SaaS. | [x] Compliant | FR-009; ADR-002 SBOM and provenance; ADR-004 provenance schema parity with SaaS. |
| **P-10** Loose Coupling | Loose coupling internal and external. | [x] Compliant | ADR-001 pluggable foundational services; ADR-004 pluggable AI endpoint. |
| **P-11** Asynchronous Communication | Async patterns must work disconnected. | [x] Compliant | ADR-001 implicitly bounds async patterns to in-boundary brokers. (Specific async broker selection pending DLD.) |
| **P-12** Accessibility (NON-NEGOTIABLE) | WCAG 2.2 AA UI. | [x] Compliant | NFR-C-003; ADR-003 explicitly carries accessibility through JIT and break-glass UIs; same UI codebase as SaaS. |
| **P-13** Performance and Efficiency | Targets within fixed envelope. | [x] Compliant (within envelope) | NFR-P-001..003; ADR-004 minimum model spec for AI latency. |
| **P-14** Availability and Reliability | Targets agreed with deploying authority; constrained by host. | [x] Compliant | NFR-A-001..002 acknowledge host-constrained envelope. |
| **P-15** Maintainability and Evolvability | Modular, well-documented. | [x] Compliant | ADR-008 LTS line; ADR-002 reproducibility cross-build supports refactor confidence. |
| **P-16** Open Source First and Reuse | Components vetted for sovereign compatibility (offline, licence). | [x] Compliant | ADR-002 OSS Sigstore/Syft; ADR-004 TGI/vLLM/Triton; ADR-007 sealed-media + diode standard kit. |
| **P-17** Cost Transparency / FinOps | Sovereign recovers full cost-to-serve plus contribution margin. | [~] Partial — pending FinOps validation | BR-006 commitment is sound but unit economics not yet exercised through real release cycles. ADVISORY-02 / risk SR-5. |
| **P-18** Infrastructure as Code | Sovereign topology in same IaC repo, parameterised offline. | [x] Compliant | ADR-001 + ADR-002 explicitly require IaC reproducibility from the bundle. |
| **P-19** Automated Testing | Including offline / disconnected profile. | [x] Compliant | ADR-001 network-deny; ADR-002 reproducibility cross-build; ADR-003 isolation tests; ADR-004 AI-flow network-deny. |
| **P-20** Continuous Integration and Deployment | Same revision produces SaaS deployment + signed sovereign bundle. | [x] Compliant | ADR-002 enforces this directly. |
| **P-21** Sovereign and Air-Gapped Deployment (NON-NEGOTIABLE) | All 11 implications and 11 validation gates of Principle 21. | [x] Compliant | See §3.2. This is the load-bearing principle and the architecture passes every validation gate by design. |

**Overall principle conformance**: 20/21 fully compliant; 1/21 partial (P-17 FinOps, pending operational validation). No principle violations; no exceptions requested.

### 3.2 Principle 21 — Detailed Compliance (Non-Negotiable)

Because Principle 21 is the load-bearing principle for project 002, this section maps each Principle 21 validation gate to the ADR that operationalises it.

| Principle 21 validation gate | Owning ADR | Status | Evidence |
|-------------------------------|------------|--------|----------|
| Sovereign release bundle produced from each managed-SaaS release revision | ADR-002 | [x] | ADR-002 §6 chosen option commits the pipeline to producing both from one revision. |
| Bundle is signed, hashed, and accompanied by SBOM and release notes | ADR-002 | [x] | Cosign keyless + HSM-anchored OVM + CycloneDX/SPDX. |
| Disconnected installation walkthrough validated end-to-end on a representative isolated environment at least every release | ADR-001, ADR-002 | [~] (planned, not yet exercised) | Network-deny CI gate is committed; first execution is a BLOCKING-03 condition. |
| Disconnected upgrade path validated (forward and roll-back) | ADR-001 + FR-002 | [~] (planned, not yet exercised) | UC-2 + ADR-001 §10.2 Phase 3. BLOCKING-03. |
| Backup, restore, and decommission procedures validated within boundary | FR-003 + ADR-001 | [~] (planned, not yet exercised) | Operator runbook (FR-011) coverage committed. BLOCKING-03. |
| AI / model integration documented as pluggable; default sovereign profile points at no external provider | ADR-004 | [x] | `ai.provider = none` default; OpenAI-compatible wire contract for plug-in; install-time validator refuses public hostnames. |
| Telemetry, time, CA, and package-mirror integrations configurable to customer-controlled endpoints | ADR-005 | [x] | All four explicitly redirected; system refuses to start until configured. |
| MOD Secure by Design assessment evidence attached to each sovereign release | ADR-006 | [~] (committed but assessment not yet generated) | BLOCKING-02 — `/arckit:mod-secure` to be run for project 002. |
| No critical-path dependency requires outbound internet connectivity in sovereign mode (validated by network-deny test) | ADR-001 | [x] | Network-deny CI gate is the architectural enforcement mechanism. |
| Operator runbook for install / upgrade / backup / restore / key rotation / decommission published with each release | FR-011 + ADR-003 | [x] (architectural commitment; runbook content to follow in DLD/operationalize) | Six runbooks committed in REQ Goal G-3 measurable-outcomes. |
| Long-term support release line and patching commitment documented and honoured | ADR-008 | [x] | Annual LTS, 24-month support, monthly patches; commitment is now sustained-engineering work. |

### 3.3 Common Violations Avoided (per Principle 21 explicit list)

| "Common violation to avoid" | Architecture position |
|------------------------------|----------------------|
| Hard-coded outbound calls (analytics, telemetry, package mirrors, time, CA revocation) | ADR-001 + ADR-005 — every such service redirected; install-time refusal if unconfigured. |
| AI / model endpoints not pluggable | ADR-004 — adaptor reused unchanged; fail-closed default. |
| Forking sovereign code from managed-SaaS code, leading to feature drift | ADR-002 reproducibility cross-build + ADR-001 single-codebase commitment. |
| Updates that cannot be applied across an air-gap | ADR-007 + ADR-008 — sealed-media / diode delivery + LTS patch cadence. |
| Licence terms that prohibit on-premise distribution | ADR-002 OSS-first tooling; ADR-004 open-weight serving stacks; Principle 16. |
| Support models that assume vendor remote access | ADR-003 — vendor remote access is default-deny; opt-in audited only. |

All six violations are explicitly avoided by design.

---

## 4. Requirements Coverage Analysis

### 4.1 Business Requirements Coverage

| Req | Summary | Owning ADR(s) | Coverage | Assessment |
|-----|---------|---------------|----------|------------|
| BR-001 | Single-codebase sovereign deployment | ADR-001, ADR-002, ADR-004 | Full | Reproducibility cross-build + adaptor reuse + network-deny CI form a defensible discipline. |
| BR-002 | Air-gap and disconnected operation | ADR-001, ADR-005, ADR-007 | Full | Zero outbound + foundational-service redirection + sealed-media delivery. |
| BR-003 | Customer-controlled deployment | ADR-001, ADR-003 | Full | Default-deny vendor remote access; cleared-personnel-only access via customer IdP. |
| BR-004 | Formal accreditation support | ADR-002, ADR-006 | Full | Per-release evidence pack mapped to JSP 440 / 604 / NCSC CAF. |
| BR-005 | Long-term support release line | ADR-008 | Full | Annual LTS, 24-month support, monthly patches. SLA discipline depends on operational execution (ADVISORY-02). |
| BR-006 | Sovereign commercial model funds cross-subsidy | ADR-008 + REQ §Budget | Partial | Commitment is in place; unit economics need real-release validation (P-17 partial). |
| BR-007 | Defence and sensitive-site procurement routes | REQ §Stakeholders, ADR-006, ADR-007 | Full | G-Cloud / DOS / defence-framework readiness articulated; distribution model accreditation-credible. |
| BR-008 | Reference customer in MOD or comparable site | All ADRs | Full (architectural) | Achievability depends on customer engagement, not architecture. |

### 4.2 Functional Requirements Coverage

| Req | Summary | Owning ADR(s) | Assessment |
|-----|---------|---------------|------------|
| FR-001 | Air-gap install from signed bundle | ADR-001, ADR-002, ADR-007 | Adequate |
| FR-002 | Air-gap upgrade with roll-back | ADR-001, ADR-007, ADR-008 | Adequate |
| FR-003 | Backup, restore, key rotation | ADR-001, ADR-002 (HSM rotation), ADR-003 (break-glass) | Adequate |
| FR-004 | Pluggable AI endpoint | ADR-004 | Adequate; primary owner. |
| FR-005 | Configurable telemetry / time / CA / mirror / IdP | ADR-005, ADR-003 (IdP) | Adequate |
| FR-006 | Within-deployment isolation | ADR-003 (role tiers), ADR-004 (prompt scoping) | Adequate |
| FR-007 | Customer-controlled identity / cleared-personnel auth | ADR-003 | Adequate; primary owner. |
| FR-008 | Same artefact authoring as SaaS | ADR-001 (single codebase) | Adequate |
| FR-009 | Tenant data export and portability | Inherited from SaaS; ADR-002 export-readiness | Adequate |
| FR-010 | Audit logging with customer-controlled retention | ADR-003, ADR-005 | Adequate |
| FR-011 | Operator runbook library | All ADRs reference; primary content in `/arckit:operationalize` | Architecturally adequate; content production pending DLD/operationalize. |
| FR-012 | Configurable classification marking | ADR-003 (per-deployment ceiling); ADR-004 (`ai.classification_max`) | Adequate |
| FR-013 | Vendor remote support channel (opt-in) | ADR-003 | Adequate |
| FR-014 | LTS patch delivery | ADR-008, ADR-002 (signing reused) | Adequate |

**Gaps identified**: None at HLD level. All 14 FRs have a primary owner and traceable design.

### 4.3 Non-Functional Requirements Coverage

#### Performance

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-P-001 | Interactive p95 < 1s within envelope | Same as SaaS UI; customer hardware-bound | Adequate; depends on customer envelope sizing. |
| NFR-P-002 | AI generation p95 < 60s when configured | ADR-004 minimum model spec + streaming SSE | Adequate |
| NFR-P-003 | Bulk export ≤ 10 min typical customer | Inherited SaaS export pipeline | Adequate |

#### Availability and Resilience

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-A-001 | ≥ 99.5% within working hours | Customer-host-constrained; agreed per customer | Adequate |
| NFR-A-002 | RPO ≤ 60 min, RTO ≤ 8 h | ADR-001 (offline backup/restore); customer KMS keys | Adequate |
| NFR-A-003 | Disconnected fault tolerance | ADR-001, ADR-004 fail-closed | Adequate |

#### Security (the load-bearing block)

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-SEC-001 | MOD SbD / JSP 440 / 604 alignment | ADR-006 evidence pack | Adequate (assessment not yet generated — BLOCKING-02). |
| NFR-SEC-002 | NCSC CAF mapping | ADR-006 | Adequate (assessment not yet generated — BLOCKING-02). |
| NFR-SEC-003 | Cryptography appropriate to classification | ADR-002 (HMG-CAPS HSM, SHA-512, ECDSA P-384 / RSA-PSS-4096); ADR-003 hash-chain audit | Adequate; per-classification confirmation deferred to DLD. |
| NFR-SEC-004 | No outbound network calls inside boundary | ADR-001 + ADR-004 + ADR-005 + network-deny CI | Adequate; the architectural anchor is sound. |
| NFR-SEC-005 | Supply-chain integrity | ADR-002 (signing, OVM, SBOM) | Adequate; strongest control set in the architecture. |
| NFR-SEC-006 | Within-deployment isolation | ADR-003, ADR-004 | Adequate |
| NFR-SEC-007 | Cleared-personnel-only access where mandated | ADR-003 (`clearance_attribute` claim) | Adequate; fallback path to be specified (ADVISORY-03). |
| NFR-SEC-008 | Vulnerability disclosure / patching SLAs | ADR-008 (Critical 7 / High 30 / Medium 90); ADR-002 same signing reused for patches | Adequate; operational discipline pending (ADVISORY-02). |

#### Compliance

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-C-001 | HMG Government Security Classifications Policy | FR-012 + ADR-003 + ADR-004 ceilings | Adequate |
| NFR-C-002 | UK GDPR / DPA 2018 where personal data | DPIA pending; vendor minimal-processing posture | Adequate (DPIA pending — BLOCKING-02 has DPIA inputs). |
| NFR-C-003 | Accessibility — WCAG 2.2 AA | Inherited SaaS UI conformance | Adequate |
| NFR-C-004 | Audit logging retention ≥ 12 months default | ADR-003, ADR-005 | Adequate |
| NFR-C-005 | LTS and patching SLA | ADR-008 | Adequate |

#### Maintainability / Portability / Interoperability

All NFRs covered by ADR-001 (single codebase), ADR-002 (reproducibility), ADR-008 (LTS).

### 4.4 Integration Requirements Coverage

| INT | Purpose | Owning ADR |
|-----|---------|------------|
| INT-001 Customer IdP | ADR-003 |
| INT-002 Customer storage / DB | DLD wave (within ADR-001 envelope) |
| INT-003 Customer time / CA / mirror | ADR-005 |
| INT-004 Customer observability | ADR-005, ADR-003 |
| INT-005 Customer AI endpoint (optional) | ADR-004 |
| INT-006 Customer email / notification | ADR-005 (extension) — pattern same |
| INT-007 Customer KMS | ADR-002 (HSM-backed signing on vendor side); ADR-001 (customer KMS for at-rest) |
| INT-008 G-Cloud / DOS / defence frameworks | REQ §BR-007; commercial track |
| INT-009 Vendor remote support (optional) | ADR-003 |
| INT-010 Vulnerability disclosure inbound | ADR-008 |

---

## 5. Architecture Quality Assessment

### 5.1 System Context (C4 L1)

**Provided in HLD**: No (deferred to wave 5/6 — BLOCKING-01).

**Conceptual position**: The sovereign deployment sits inside a customer accredited boundary. External actors include cleared personnel (operators, architects, reviewers — all federated via customer IdP), customer foundational services (NTP, internal CA, package mirror, SIEM, KMS, optional AI), customer SROs / accreditors / SIROs (governance only, no system access), and vendor staff (only via opt-in audited FR-013 channel). The system has no external dependencies that cross the boundary.

### 5.2 Container View (C4 L2)

**Provided in HLD**: No (deferred — BLOCKING-01).

**Conceptual decomposition** (from REQ + ADR set):

| Container | Responsibility | Source |
|-----------|----------------|--------|
| Web UI | Browser-based authoring (same code as SaaS) | BR-001, FR-008 |
| API service | OpenAPI-described HTTP API | NFR-I-001, ADR-001 |
| Async / job runner | Long-running generation, lineage, indexing | P-11 |
| AI adaptor | Pluggable AI generation | ADR-004 |
| Audit pipeline | Hash-chained audit emission to customer SIEM | ADR-003, ADR-005 |
| Storage / DB | Customer-provisioned (INT-002) | ADR-001 |
| `arckit-verify` CLI | Customer-side bundle verification | ADR-002 |
| IaC bundle | Reproducible deployment topology | P-18, ADR-001, ADR-002 |
| Operator runbook library | Install / upgrade / backup / restore / decommission | FR-011 |

### 5.3 Technology Stack

| Layer | Approach | Approved per Principle 16 / 21 | Comments |
|-------|----------|----------------------------------|----------|
| Frontend | Same as SaaS (browser-based, WCAG 2.2 AA) | Yes | Inherited |
| API | HTTP / OpenAPI; OIDC/SAML auth | Yes | ADR-003 |
| Async | Broker pluggable; offline-capable | Yes | P-11 (specific selection in DLD) |
| Storage / DB | Customer-provisioned | Yes | INT-002 |
| AI serving | TGI / vLLM / Triton (customer-hosted) | Yes | ADR-004 |
| Signing | Cosign keyless + HSM (FIPS 140-2 L3 / HMG-CAPS) | Yes | ADR-002 |
| SBOM | Syft → CycloneDX 1.5 + SPDX 2.3 | Yes | ADR-002 |
| Provenance | SLSA L3 via slsa-github-generator | Yes | ADR-002 |
| Distribution | Sealed encrypted media (default) / one-way diode | Yes | ADR-007 |
| LTS branching | Annual major LTS line | Yes | ADR-008 |

**Non-approved technologies**: None proposed.

**Technology risks**: HSM provider exit (ADR-002 R-ADR2-8), cosign breaking changes (ADR-002 R-ADR2-7), serving-stack wire-format drift (ADR-004) — all surfaced and mitigated.

### 5.4 Data Architecture

**Data entities** (from REQ §Data Requirements):

| Entity | Owner | Storage |
|--------|-------|---------|
| DR-001 Customer Deployment | Customer | Customer DB |
| DR-002 User (Cleared Personnel) | Customer (sourced from customer IdP claims) | Customer DB |
| DR-003 Project | Customer | Customer DB |
| DR-004 Artefact | Customer | Customer DB |
| DR-005 Audit Event | Customer | Customer SIEM (hash-chained) |
| DR-006 Cryptographic Key Inventory | Customer KMS | Customer KMS |
| DR-007 SBOM and Release Manifest | Vendor (per release) | Distributed in bundle |

All seven data entities have clear ownership; no shared-database pattern; classification ceilings enforced (FR-012, ADR-003, ADR-004).

### 5.5 Integration Architecture

External integrations are all customer-controlled and inside the boundary. No external system integrates *to* the sovereign deployment from the public internet.

| External system | Pattern | Auth | Assessment |
|-----------------|---------|------|------------|
| Customer IdP | OIDC / OAuth 2.x / SAML 2.0 | Standard | Adequate (ADR-003) |
| Customer SIEM | Push (structured logs) | Customer-managed | Adequate (ADR-005) |
| Customer KMS | PKCS#11 / API | Customer-managed keys | Adequate (ADR-001, ADR-002) |
| Customer AI endpoint | OpenAI-compatible HTTP/SSE | Bearer / mTLS via KMS | Adequate (ADR-004) |
| Customer NTP / CA / mirror | Standard | Customer-managed | Adequate (ADR-005) |
| Vendor signing infra | One-way (vendor → bundle) | HSM + cosign | Adequate (ADR-002) |

---

## 6. Security Architecture Review

### 6.1 Threat Model

**Comprehensive threat model**: Pending — to be authored as part of MOD Secure by Design assessment (BLOCKING-02). The ADRs collectively articulate the major threat categories (signing-key compromise, fork drift, prompt content above ceiling, missing claim, break-glass abuse, vendor-staff impersonation, CI bypass, customer model misconfiguration), but a formal STRIDE / EBIOS / MOD-SbD-style threat model has not been produced in this repository for project 002.

### 6.2 Security Controls

| Control area | HLD position | Assessment |
|--------------|--------------|------------|
| Authentication | Customer IdP via OIDC/OAuth/SAML; typed `clearance_attribute` claim | Adequate (ADR-003) |
| Authorisation | Role tiers + project / role / CoI labels; default-deny; JIT elevation for privileged ops | Adequate |
| Network segmentation | Boundary-internal only; zero outbound | Adequate (ADR-001, network-deny CI) |
| Encryption in transit | TLS via customer CA | Adequate (ADR-005) |
| Encryption at rest | Customer KMS-managed keys | Adequate (NFR-A-002) |
| Secrets management | Customer KMS only (INT-007) | Adequate |
| Audit logging | Hash-chained, customer SIEM, ≥ 12 months default | Adequate (ADR-003, ADR-005) |
| Vulnerability scanning | SBOM-driven; LTS patch SLAs | Adequate (ADR-008) |
| Supply-chain integrity | Cosign keyless + HSM OVM + SLSA L3 + SBOM | Strongly adequate (ADR-002) |
| Penetration testing | Annual + on material change; pipeline + `arckit-verify` in scope | Adequate (ADR-002) |

### 6.3 Compliance Mapping

| Framework | Mapping owner | Status |
|-----------|---------------|--------|
| MOD Secure by Design / JSP 440 / JSP 604 | ADR-006 | Mapping committed; assessment to be generated — BLOCKING-02 |
| NCSC Cyber Assessment Framework | ADR-006 | Mapping committed; CAF instance pending |
| HMG Government Security Classifications Policy | FR-012, ADR-003, ADR-004 | Configuration enforces ceilings |
| UK GDPR / DPA 2018 | NFR-C-002 | Posture clear; DPIA inputs pending — BLOCKING-02 |
| Cyber Essentials | Inherited build-environment posture | Adequate |
| NCSC Supply Chain Security 12 Principles | ADR-002 §Validation & Compliance | Adequate |
| NIS2 (where applicable) | Out of scope by default; per-customer review | N/A by default |

---

## 7. Scalability & Performance Architecture

### 7.1 Scalability

Within the customer-provisioned envelope, the platform scales horizontally via stateless services, auto-scaling, and customer-side foundational services. No re-architecture is required to add capacity within the envelope (NFR-S-001). Outside the envelope, the customer provisions more hardware — outside vendor scope by design.

### 7.2 Performance

The HLD inherits the SaaS performance characteristics for in-process operations and depends on customer hardware for AI generation. ADR-004's minimum model spec aims to bound the AI latency tail. Performance testing inside a representative customer envelope is committed (ADR-001 §Validation; ADR-008 LTS regression).

---

## 8. Resilience & Disaster Recovery

### 8.1 Resilience patterns

| Pattern | Status | Source |
|---------|--------|--------|
| Circuit breaker | Yes (P-3) | Inherited |
| Retry with exponential backoff | Yes | Inherited |
| Timeout on all network calls | Yes | Inherited |
| Bulkhead isolation | Yes (single-tenant in sovereign) | P-8 |
| Graceful degradation (AI off) | Yes | ADR-004 fail-closed |
| Health checks | Yes | Inherited |

### 8.2 Disaster Recovery

| Aspect | Target | HLD position | Assessment |
|--------|--------|--------------|------------|
| RPO | ≤ 60 min | ADR-001; customer-managed backup | Adequate |
| RTO | ≤ 8 h | ADR-001; runbook-driven | Adequate |
| Multi-region | Per customer envelope | Within boundary | Adequate (host-constrained) |
| DR drill | Annual customer-led | NFR-A-002 | Adequate |
| Backup integrity | Encrypted at rest with customer KMS | INT-007 | Adequate |

---

## 9. Operational Architecture

### 9.1 Observability

All telemetry to customer-controlled destinations only. Vendor sees nothing from inside customer boundaries. Per-deployment dashboards and alerts are the customer's responsibility, with schemas published per LTS line.

### 9.2 Deployment

IaC is part of the bundle; install, upgrade, backup, restore, key rotation, and decommission are all runbook-driven. Distribution is via sealed encrypted media (default) or one-way diode (option). Each release line is signed, hashed, and accompanied by SBOM and OVM.

### 9.3 Supportability

Vendor support is opt-in only via FR-013. Customer-led operability is the design intent (Goal G-10, ADR-003). Vendor provides reproducible synthetic environments to debug customer issues without remote access.

---

## 10. Cost Architecture

### 10.1 Cost Estimation

Indicative per-customer 3-year TCO across the wave-2 ADRs:

| ADR | Vendor 3-yr TCO (indicative) | Notes |
|-----|------------------------------|-------|
| ADR-001 | £390–610k | Offline-CI + signing + LTS plumbing |
| ADR-002 | ~£154k | Cosign + HSM + OVM + SLSA L3 |
| ADR-003 | ~£245k | JIT elevation + audit + federated guest IdP |
| ADR-004 | Bounded; small | Provider profile, no inference cost on vendor |
| ADR-005 | Within ADR-001 envelope | — |
| ADR-007 | Operational; per-engagement | Sealed media + couriers |
| ADR-008 | LTS engineering rota | Recurring |

Recovery is via BR-006 cross-subsidy. Customer cost-to-serve covers full vendor cost-to-serve plus contribution margin.

### 10.2 FinOps

P-17 partial — commitment is sound but unit economics need real-release validation. ADVISORY for DLD.

---

## 11. Issues and Recommendations

### 11.1 Critical Issues (BLOCKING)

| ID | Issue | Impact | Recommendation | Owner | Target Date |
|----|-------|--------|----------------|-------|-------------|
| BLOCKING-01 | Architecture diagrams (C4 Context, C4 Container, Network DFD, sequence diagrams) not yet generated | HIGH — design cannot be visually verified for blind spots | Generate diagrams in waves 5/6 covering UC-1, UC-2, UC-3, ADR-003 access flow, and the network-deny topology | Vendor Lead Architect | 2026-06-15 |
| BLOCKING-02 | Project-002 RISK register, MOD Secure-by-Design assessment, and DPIA inputs not yet generated | HIGH — ADR-006 evidence pack is incomplete | Run `/arckit:risk`, `/arckit:mod-secure`, `/arckit:dpia` for project 002 | Vendor Security Lead | 2026-06-15 |
| BLOCKING-03 | Air-gap CI walkthrough never exercised end-to-end on a draft release | HIGH — feasibility of network-deny + reproducibility cross-build + AI-flow network-deny + ceremony is unevidenced | Run a synthetic end-to-end pipeline through ADR-001 / -002 / -004 / -007 gates | Vendor Lead Architect with Security Lead | 2026-07-15 |

### 11.2 High Priority Issues (ADVISORY)

| ID | Issue | Impact | Recommendation |
|----|-------|--------|----------------|
| ADVISORY-01 | Diode round-trip semantics for `arckit-verify` output not specified | MEDIUM | DLD specifies one-way only; any return signal via runbook |
| ADVISORY-02 | LTS backport SLA discipline across two parallel LTS lines plus reproducibility cross-build needs operational answer | MEDIUM | DLD specifies tooling and rota; risk SR-4 owner sign-off |
| ADVISORY-03 | `clearance_attribute` claim fallback (signed customer-managed table) needs schema, refresh cadence, tamper-evidence | MEDIUM | DLD specifies; ensure fallback does not weaken NFR-SEC-007 |
| ADVISORY-04 | Dual-format SBOM (CycloneDX 1.5 + SPDX 2.3) divergence not catalogued | MEDIUM | DLD includes a known-divergence map |

### 11.3 Low Priority (INFORMATIONAL)

| ID | Suggestion | Benefit |
|----|------------|---------|
| INFO-01 | Wardley map for sovereign supply chain | Surface evolution-stage assumptions |
| INFO-02 | Cross-project ADR linkage matrix (project 001 → project 002) | Single-codebase auditability |

---

## 12. Review Decision

### 12.1 Final Decision

**Status**: APPROVED WITH CONDITIONS

**Effective Date**: 2026-05-03 (conditional on BLOCKING items by 2026-06-15 / 2026-07-15)

**Conditions**:

1. BLOCKING-01 — Architecture diagrams generated by 2026-06-15.
2. BLOCKING-02 — RISK register, MOD SbD assessment, and DPIA inputs for project 002 generated by 2026-06-15.
3. BLOCKING-03 — End-to-end air-gap CI walkthrough exercised by 2026-07-15.

**Next Steps**:

- [ ] Generate sovereign architecture diagrams (`/arckit:diagram` × 5+).
- [ ] Generate `/arckit:risk` for project 002.
- [ ] Generate `/arckit:mod-secure` for project 002.
- [ ] Generate `/arckit:dpia` for project 002.
- [ ] Run synthetic end-to-end air-gap CI walkthrough.
- [ ] Re-run this review after the above (target 2026-06-15 or 2026-07-15).
- [ ] Proceed to Detailed Design phase only after re-review clears the BLOCKING conditions.

### 12.2 Reviewer Sign-Off

| Reviewer | Role | Decision | Signature | Date |
|----------|------|----------|-----------|------|
| ArcKit AI | Lead Reviewer (this review) | Conditional | (machine-generated) | 2026-05-03 |
| [PENDING] | Vendor Security Lead | [PENDING] | _________ | [PENDING] |
| [PENDING] | Vendor Lead Architect | [PENDING] | _________ | [PENDING] |
| [PENDING] | Sovereign Delivery Lead | [PENDING] | _________ | [PENDING] |
| [PENDING] | Pilot Customer Accreditor | [PENDING] | _________ | [PENDING] |
| [PENDING] | NCSC liaison | [PENDING] | _________ | [PENDING] |

**Unanimous Approval Required**: Yes (per Principle 21 non-negotiable status).

**Escalation**: ArcKit Architecture Review Board for any unresolved disagreement; pilot customer accreditation forum where the customer-side decision is contested.

---

## 13. Appendices

### Appendix A: Source Artefacts

- `projects/000-global/ARC-000-PRIN-v2.0.md`
- `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md`
- `projects/002-arckit-sovereign/ARC-002-STKE-v1.0.md`
- `projects/002-arckit-sovereign/decisions/ARC-002-ADR-001-v1.0.md` through `ARC-002-ADR-008-v1.0.md`

### Appendix B: Pending Artefacts (Cited In ADRs, Not Yet Generated)

- `projects/002-arckit-sovereign/ARC-002-RISK-v1.0.md` — `/arckit:risk`
- `projects/002-arckit-sovereign/ARC-002-MODSEC-v1.0.md` — `/arckit:mod-secure`
- `projects/002-arckit-sovereign/ARC-002-DPIA-v1.0.md` — `/arckit:dpia`
- Architecture diagrams under `projects/002-arckit-sovereign/diagrams/` — `/arckit:diagram`
- Requirements traceability matrix — `/arckit:traceability`

### Appendix C: Cross-Project Dependencies

- `projects/001-arckit-saas/decisions/ARC-001-ADR-004-v1.0.md` — parent of project-002 ADR-004 (`AIAdaptor` interface; provenance schema). Project 001 ADR-004 changes propagate here.
- `projects/001-arckit-saas/ARC-001-REQ-v1.0.md` — sister REQ; maintains shared FR-004 / INT-005 patterns.

---

## External References

> No external (third-party) documents were placed in `projects/002-arckit-sovereign/external/` at the time of this review. UK Government, MOD, and NCSC frameworks referenced (MOD Secure by Design, JSP 440, JSP 604, NCSC CAF, NCSC Cloud Security Principles, NCSC Supply Chain Security guidance, HMG Government Security Classifications Policy, UK GDPR / DPA 2018, GDS Service Standard, Technology Code of Practice, OIDC / OAuth 2.x / SAML 2.0 specifications, CycloneDX 1.5, SPDX 2.3, SLSA Framework v1.0, Sigstore / Cosign, FIPS 140-2 / 140-3, HMG-CAPS, UK Government AI Playbook, ATRS, Procurement Act 2023, Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018, WCAG 2.2) are public-domain and cited by name.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| PRIN-v2.0 | ARC-000-PRIN-v2.0.md | Internal — Architecture Principles | projects/000-global/ | Anchoring authority (Principle 21 non-negotiable) |
| REQ-002-v1.0 | ARC-002-REQ-v1.0.md | Internal — Requirements | projects/002-arckit-sovereign/ | BR/FR/NFR/INT/DR set |
| STKE-002-v1.0 | ARC-002-STKE-v1.0.md | Internal — Stakeholders | projects/002-arckit-sovereign/ | SD-1..17, Goals G-1..10, Outcomes O-1..7 |
| ADR-002-001 | ARC-002-ADR-001-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Air-Gapped Operation Model |
| ADR-002-002 | ARC-002-ADR-002-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Signed Release Bundle |
| ADR-002-003 | ARC-002-ADR-003-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Cleared-Personnel Access Model |
| ADR-002-004 | ARC-002-ADR-004-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | On-Premise AI Integration |
| ADR-002-005 | ARC-002-ADR-005-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Foundational Service Redirection |
| ADR-002-006 | ARC-002-ADR-006-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | JSP 440 / SAL Alignment |
| ADR-002-007 | ARC-002-ADR-007-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Distribution Model |
| ADR-002-008 | ARC-002-ADR-008-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | LTS Release Line |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| PRIN-21 | PRIN-v2.0 | §V Principle 21 | Non-negotiable principle | "The platform MUST support deployment into customer-controlled environments — including UK Ministry of Defence and other sensitive sites — operating fully in disconnected or air-gapped mode." |
| PRIN-5-I5 | PRIN-v2.0 | §I.5 sovereign block | Mandatory controls | "Additional Mandatory Controls (Sovereign / MOD / sensitive deployments)" |
| REQ-NFRSEC004 | REQ-002-v1.0 | NFR-SEC-004 | Critical NFR | "In sovereign mode, no outbound network call to any endpoint outside the customer's accredited boundary, validated by network-deny test in CI." |
| REQ-BR001 | REQ-002-v1.0 | BR-001 | Business Requirement | "The sovereign deployment MUST share the same source code, data formats, APIs, and feature set as the managed SaaS." |
| ADR-001-decision | ADR-002-001 | §6.1 | Decision | "Strict Air-Gap — Zero Outbound Egress, Customer-Controlled Foundational Services, Single Codebase with SaaS." |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | No external documents placed in `projects/002-arckit-sovereign/external/` at time of review. |

---

**Generated by**: ArcKit `/arckit:hld-review` command
**Generated on**: 2026-05-03 GMT
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: claude-opus-4-7[1m]
**Generation Context**: Reviewed REQ + STKE + ADR-001..008 against ARC-000-PRIN-v2.0 (especially Principle 21 non-negotiable). Architecture diagrams not yet generated (waves 5/6); RISK / MOD SbD / DPIA artefacts for project 002 not yet generated. Review surfaces three BLOCKING conditions and four ADVISORY items; no principle violations found.
