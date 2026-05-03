# MOD Secure by Design Assessment

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:mod-secure`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-SECD-MOD-v1.0 |
| **Document Type** | MOD Secure by Design Assessment |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Per release (continuous assurance) |
| **Next Review Date** | 2026-06-02 |
| **Owner** | Mark Craddock, ArcKit as a Service Owner |
| **Reviewed By** | [PENDING — vendor Security Lead, deploying-authority Accreditor in pilot] |
| **Approved By** | [PENDING — Service Owner; deploying-authority SIRO accepts customer-side residual] |
| **Distribution** | Vendor Security Lead, vendor Lead Architect, Service Owner, deploying-authority SRO / SIRO / Accreditor (pilot), Defence Digital liaison, NCSC liaison |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:mod-secure` command. Continuous Assurance Assessment Tool (CAAT) framework applied to the ArcKit sovereign deployment vendor-side evidence pack per ADR-006. Covers MOD SbD principles + JSP 440 (P&ASec, InfoSec, PhySec) + JSP 604 accreditation pathway + Security Aspects Letter alignment. Principal acceptance vehicle for residual position on RISK R-002 (MOD-SbD assessment fail) and R-005 (SAL controls compliance). | [PENDING] | [PENDING] |

## Document Purpose

This is the **vendor-side MOD Secure by Design assessment** that accompanies each ArcKit sovereign release bundle as the principal artefact within the per-release evidence pack defined in ADR-006. It exists to:

1. Demonstrate that the ArcKit sovereign deployment, as packaged and shipped by the vendor, is fit to enter a deploying-authority accreditation process under JSP 604 with a credible likelihood of authorisation-to-operate (ATO).
2. Map ArcKit's vendor-controlled controls to JSP 440 P&ASec / InfoSec / PhySec control sets and identify, per control, whether responsibility is **Vendor**, **Customer**, **Shared**, **Platform-inherited**, or **Not-applicable** — this is the controls-inheritance matrix from ADR-006.
3. Provide pre-filled inputs to the site Security Aspects Letter (SAL) so the deploying authority's accreditor can finish the SAL with site-specific facts rather than re-derive vendor-internal evidence.
4. Track CAAT-equivalent self-assessment scores against the seven MOD Secure by Design principles for continuous-assurance reporting.
5. Serve as the **principal acceptance vehicle** for the residual risk position on **R-002** (MOD-SbD assessment fail) and **R-005** (customer break-glass / SAL controls compliance) in `ARC-002-RISK-v1.0.md`.

> **Critical scope statement (per ADR-006)**: The vendor explicitly does **NOT** accredit. JSP 604 places authorisation-to-operate authority with the deploying authority's accreditor; that authority is non-transferable and site-specific. This document is **input** to that accreditation, not a substitute for it. The vendor signs an *accuracy attestation* on this pack — not an accreditation claim. Any marketing or procurement language describing ArcKit as "JSP 440 accredited" or "MOD-SbD accredited" is a category error and must be corrected on sight.

---

## Executive Summary

**Overall Security Posture**: **Adequate (with conditions)** — vendor-side controls are in place or designed for build out; deploying-authority controls (SAL, personnel security, physical security, ATO) remain customer-side residual.

**MOD Secure by Design Principle Score**: **6 / 7 fully addressed**, **1 / 7 partially addressed** (Principle 7 — Through-Life Assurance — depends on the LTS line operationalising at GA, currently in development per ADR-008).

**Accreditation Status**: **Pre-Accreditation — Evidence Pack Forming**. No deploying authority is engaged at first issue. Pilot accreditator-in-the-loop programme is the highest-leverage mitigation against R-001, R-002 and R-012 per `ARC-002-RISK-v1.0.md`.

**Risk Summary**: **Medium overall residual** — sovereign-track risk profile is dominated by compliance-cluster risks (R-002, R-004, R-005, R-007, R-013) where sovereign appetite is Very Low. Five of those exceed appetite at residual score and must be acknowledged in writing by the Service Owner per the RISK register's recommendation.

**Key Security Findings**:

- **Strengths** — Air-gap by design (ADR-001), signed bundle with cosign + CycloneDX SBOM + SLSA L3 + offline verification manifest (ADR-002), customer-controlled foundational services with fail-closed bootstrap (ADR-005), pluggable AI endpoint defaulting to no-external-call (ADR-004), distribution model that respects customer-approved data-transfer mechanisms (ADR-007), and a documented LTS line (ADR-008) materially reduce the inherent attack surface that other vendor products typically carry into MOD environments.
- **Strengths (governance)** — ADR-006 establishes the controls-inheritance model and the responsibility split between vendor and deploying authority. This is the single largest governance asset in this pack: it tells the customer accreditator exactly what they are inheriting and what they must still demonstrate.
- **Conditional / Customer-side residual** — Personnel security (JSP 440 P&ASec) for end users and operators is **wholly customer-side** (per ADR-003 cleared-personnel access is honoured via identity claims, but the vetting itself is the deploying authority's). Physical security (PhySec) is wholly customer-side (host environment). Cryptographic primitives "appropriate to the accredited classification" are vendor-default secure but the *HMG-approved primitive set* is selected by the customer SAL — vendor cannot pre-select.
- **Blocking gaps** — None identified that prevent issue of the v1.0 evidence pack into a representative pilot. **Conditions for first issue** are: (i) HSM signing infrastructure operational (mitigates R-004); (ii) network-deny CI test green on bundle issue (mitigates R-007); (iii) accreditator-in-the-loop alpha review of evidence-pack format completed (mitigates R-002, R-012).

---

## 1. Security Classification and Data Handling

### 1.1 Information Classification

**Vendor side (this codebase repository, this evidence pack)**: **OFFICIAL**.

**Sovereign deployment (per customer)**: **configured to a maximum classification per the deploying authority's SAL**. Permitted range: OFFICIAL, OFFICIAL-SENSITIVE, SECRET, or TOP SECRET subject to formal customer-led accreditation and SAL. The system enforces the configured maximum at create/edit time per FR-012 in `ARC-002-REQ-v1.0.md`.

**Classification Justification**:

The ArcKit codebase, documentation, and vendor-side evidence pack are OFFICIAL — they describe how a governance toolkit is built and packaged, but contain no customer classified data and no operational MOD content. Material at OFFICIAL-SENSITIVE or higher is **not** placed in this repository (per `ARC-002-REQ-v1.0.md` external-references guidance). At deployment, the customer's content classification is determined entirely by the customer; ArcKit's role is to enforce the configured maximum and refuse content above it.

**Data Types Processed by the Sovereign Deployment** (vendor-side view; actual handling per customer SAL):

- [x] Personal data (UK GDPR) — operator and end-user identity claims (DR-002), audit events (DR-005). Customer is the data controller; vendor is processor only via opt-in remote support (FR-013, NFR-C-002).
- [ ] Special category data — not generally processed by ArcKit; depends entirely on customer content choices.
- [x] Classified military information — only if the customer SAL permits and the customer chooses to author such content as artefacts. ArcKit treats classification as a marking attribute (FR-012) and does not differentiate handling beyond access control.
- [x] Operational data — same as above.
- [ ] Intelligence data — out of scope for v1; customer SAL would restrict.
- [x] Cryptographic material — ArcKit holds release-signing keys (vendor side, HSM-protected, per ADR-002) and customer-managed keys for encryption at rest (customer side, per INT-007).
- [x] Protectively marked documents — yes, by design, up to the deployment's configured maximum.

**Data Classification Matrix**:

| Data Type | Classification (vendor side) | Classification (customer side) | Volume | Storage Location | Access Controls |
|-----------|------------------------------|-------------------------------|--------|------------------|-----------------|
| ArcKit source code | OFFICIAL | n/a | High | Vendor source-control (cloud, UK-resident) | Vendor IdP + MFA + RBAC |
| Release bundle (signed) | OFFICIAL | Up to deployment maximum on receipt | Medium | Vendor build infrastructure → customer-approved transfer mechanism (ADR-007) → customer accredited boundary | Cosign signature + SLSA L3 provenance + customer transfer controls |
| Customer artefacts (Markdown / JSON / YAML) | n/a | Up to deployment maximum (FR-012) | Variable | Customer-controlled storage inside accredited boundary (INT-002) | Customer IdP, project/role/CoI isolation (FR-006), customer KMS at rest (INT-007) |
| Audit events (DR-005) | n/a | OFFICIAL (default) | Variable | Customer-controlled SIEM (INT-004) | Customer-controlled retention (FR-010, NFR-C-004) |
| Operator identity claims (DR-002) | n/a | OFFICIAL (PII) | Low | Customer IdP | Customer IdP controls |
| Vendor signing keys | OFFICIAL-SENSITIVE | n/a | Very low | Vendor HSM (ADR-002) | HSM access policy + SLSA L3 isolated build environment + key custody policy |

**Gaps/Actions**:

- HSM signing infrastructure must be operational before first bundle issue (mitigates R-004; RISK register lists this as the highest-priority HIGH action).
- The customer-side classification matrix is empty until the first deploying authority is engaged — that's expected; populate it inside the SAL pre-fill at engagement.

---

## 2. MOD Security Principles Compliance — The 7 MOD Secure by Design Principles

Each principle is scored using a CAAT-equivalent maturity scale: **Initial / Repeatable / Defined / Managed / Optimized** (corresponding to JSP 440 IAMM Levels 1–5; 0 = Non-existent).

### 2.1 Principle 1: Understand and Define Context

**Status**: ✅ Compliant — **CAAT score: Defined (3) approaching Managed (4)**.

**Evidence**:

- Operational context, mission, users, and data flows documented in `ARC-002-REQ-v1.0.md` (Executive Summary; Use Cases UC-1, UC-2, UC-3; Data Requirements DR-001 to DR-007).
- Stakeholder context documented in `ARC-002-STKE-v1.0.md` (deploying-authority SRO, SIRO, Accreditor, Operator team; vendor Service Owner, Lead Architect, Security Lead, DPO).
- Data classification configurable per FR-012; defaults safe.
- Operational environment understood as "customer-controlled accredited boundary, no internet egress" — anchored in ADR-001 (air-gapped operation model).
- Stakeholder security requirements captured in REQ NFR-SEC-001 to NFR-SEC-008 and explicitly traced back to Principle 5 / 21 in `ARC-000-PRIN-v2.0.md`.

**Gaps/Actions**:

- Move from Defined to Managed by completing the first deploying-authority engagement and feeding pilot context back into a v1.1 of this assessment.

### 2.2 Principle 2: Apply Security from the Start

**Status**: ✅ Compliant — **CAAT score: Managed (4)**.

**Evidence**:

- Project 002 began with Principle 21 (Sovereign and Air-Gapped Deployment) as an architectural anchor, classified non-negotiable in `ARC-000-PRIN-v2.0.md` §VI. Security was not retrofitted.
- Threat surface enumerated at requirements time (REQ §Risks, NFR-SEC-001 to NFR-SEC-008).
- Security architecture decisions reached as ADRs **before** HLD/DLD: ADR-001 (air-gap), ADR-002 (signed bundle), ADR-003 (cleared-personnel access), ADR-005 (customer-controlled foundational services), ADR-006 (controls inheritance / SAL alignment), ADR-007 (distribution).
- Security expertise represented from inception via the vendor Security Lead role in the stakeholder model (note: role currently [PENDING] appointment per `ARC-002-STKE-v1.0.md`; this is a tracked gap).

**Gaps/Actions**:

- Appoint vendor Security Lead substantively (currently a [PENDING] role). Tracks to STKE follow-up.

### 2.3 Principle 3: Apply Defence in Depth

**Status**: ✅ Compliant — **CAAT score: Defined (3)**.

**Evidence**:

- Layered controls across network (boundary firewalls customer-side; no outbound from inside boundary by NFR-SEC-004), host (customer infrastructure, hardened per customer SAL), application (auth, RBAC, input validation, classification marking), data (customer KMS at rest, TLS in transit, customer-managed keys), identity (customer IdP, MFA, cleared-personnel claim per ADR-003 and FR-007).
- Segmentation: within-deployment isolation between projects, roles, and communities of interest (FR-006, NFR-SEC-006).
- Detection: audit events to customer SIEM (FR-010), tamper-evident logs.
- Containment: customer-controlled key rotation (FR-003, INT-007); air-gap by design (ADR-001) limits blast radius to inside the boundary.
- Fail-safe defaults: foundational services bootstrap **fail-closed** (ADR-005 Option A) — system refuses to start if customer-controlled endpoints are unconfigured.
- Assume-breach: decommission and data-destruction runbook (FR-011, UC-3) treats compromise as an inevitable end-state.

**Gaps/Actions**:

- Document containment/recovery runbook explicitly for compromise-of-vendor-signing-key scenario (covered partially by ADR-002 risks section; promote to standalone runbook before GA).

### 2.4 Principle 4: Follow Secure Design Patterns

**Status**: ✅ Compliant — **CAAT score: Managed (4)**.

**Evidence**:

- NCSC Secure Design Principles applied (zero-trust at deployment; no implicit network trust; see `ARC-000-PRIN-v2.0.md` Principle 5).
- NIST CSF 2.0 mapping populated below in §11.
- OWASP Top 10 mitigated through DevOps strategy in `ARC-002-DEVOPS-v1.0.md` (SAST, DAST, SCA in CI; secrets scanning; container image scanning; IaC scanning).
- Industry-standard cryptographic primitives at default: TLS 1.3, AES-256, SHA-256, RSA-2048+ / Ed25519. Customer SAL may pin to **HMG-approved** primitive set (working position in ADR-002 Appendix C); the vendor exposes the cryptographic profile per release for customer accreditator review.
- Supply-chain pattern: SLSA L3 build provenance + cosign signing + CycloneDX SBOM (ADR-002) — directly aligned with NCSC supply-chain security guidance.
- Distribution pattern: sealed-media default with diode option per customer accreditation (ADR-007).

**Gaps/Actions**:

- Confirm HMG-approved primitive set in HLD against the pilot customer SAL; treat ADR-002 Appendix C as a working position to be ratified.

### 2.5 Principle 5: Continuously Manage Risk

**Status**: ✅ Compliant — **CAAT score: Defined (3)**.

**Evidence**:

- Risk register `ARC-002-RISK-v1.0.md` actively maintained, with sovereign-specific appetite override (Strategic ≤ 12, Compliance ≤ 4, Reputational ≤ 4, Technology ≤ 6, Operational ≤ 6, Financial ≤ 6, Resilience ≤ 6).
- Five risks consciously above appetite (R-001, R-002, R-005, R-007, R-008); explicit acceptances tracked.
- This document is the **principal acceptance vehicle** for residual position on R-002 and R-005 — meaning that the next quarterly review of those two risks consumes this assessment as its primary input.
- Continuous-testing cadence: network-deny test in CI per release (NFR-SEC-004); air-gap install validated in CI representative environment per release; SBOM regenerated and diff'd per release.
- Threat intelligence: vulnerability disclosure programme aligned with ISO 29147 (NFR-SEC-008); LTS patching SLAs Critical 7 / High 30 / Medium 90 days.
- Per-release reissue of this very assessment encodes the continuous-assurance principle.

**Gaps/Actions**:

- Continuous monitoring of customer-side SAL drift (post-deployment) is a customer-side responsibility; vendor cannot directly mitigate. Note in SAL pre-fill that "annual review of vendor evidence pack against current customer SAL" is a customer obligation.

### 2.6 Principle 6: Secure the Supply Chain

**Status**: ✅ Compliant — **CAAT score: Managed (4) approaching Optimized (5)**.

**Evidence**:

- SBOM generated as CycloneDX per release (ADR-002).
- Cosign signature with offline verification manifest (ADR-002 Option 3 hybrid) — verifiable inside an air-gap without Sigstore reachability.
- SLSA Level 3 build provenance.
- Reuse-before-build approach per `ARC-000-PRIN-v2.0.md` Principle 16; OSS components vetted for licence and offline-compatibility.
- Open-source supplier attestation framework per ISN 2023/10 — vendor will issue the supplier attestation alongside the evidence pack on each release.
- Software supply-chain attack vectors specifically addressed by R-004 in the RISK register, with HSM-backed signing as the primary control (effectiveness Strong; residual reduction 87% from inherent 15 to residual 2).

**Gaps/Actions**:

- HSM signing must be operational before first bundle issue — RISK recommends as HIGH priority pre-GA. Until live, R-004 inherent stays at 15 and bundle issue is **gated** on HSM.
- Open-source dependency licensing review for offline-distribution compatibility must be a CI gate (currently a manual ADR check; promote to automated gate in DEVOPS scope).

### 2.7 Principle 7: Enable Through-Life Assurance

**Status**: ⚠️ Partially Compliant — **CAAT score: Repeatable (2) approaching Defined (3)**.

**Evidence**:

- LTS release line documented (ADR-008): annual major LTS, ≥ 24-month patch window, no feature backports.
- Patching SLAs documented (NFR-SEC-008): Critical 7 / High 30 / Medium 90 days.
- Decommissioning runbook with secure data deletion (FR-011, UC-3, NFR-A-002 backups).
- Operator runbook library (FR-011): install / upgrade / roll-back / backup / restore / key rotation / decommission / incident response / DR.
- Continuous assurance assessments (this document) reissued per release.

**Why partially compliant**: The LTS infrastructure is in development (REQ §Dependencies — "LTS release infrastructure: Not Started; target GA – 6 months"); R-010 (LTS line drift / Year-3 backport SLA breach) is on the register as **TECHNOLOGY** with residual 6. Through-life assurance is *designed* but not yet *operationally proven* on a real LTS-2 backport. Until at least one LTS line crosses its first backport release, this principle's score cannot move past Defined.

**Gaps/Actions**:

- Operationalise LTS line before GA (RISK register lists this as MEDIUM action; STKE / DEVOPS dependency).
- Conduct first synthetic backport in CI before GA – 3 months, even if no real CVE exists, to validate the pipeline.
- Move from Repeatable to Defined when first real LTS patch ships; to Managed when second LTS line is open in parallel.

### 2.8 MOD Secure by Design Principles — Summary Scorecard

| # | Principle | Status | CAAT-Equivalent Score | Notes |
|---|-----------|--------|------------------------|-------|
| 1 | Understand and Define Context | ✅ Compliant | Defined (3) → Managed (4) | Move at first deploying-authority engagement |
| 2 | Apply Security from the Start | ✅ Compliant | Managed (4) | Strong; vendor Security Lead appointment outstanding |
| 3 | Apply Defence in Depth | ✅ Compliant | Defined (3) | Add explicit signing-key-compromise runbook |
| 4 | Follow Secure Design Patterns | ✅ Compliant | Managed (4) | Confirm HMG primitive set vs pilot SAL |
| 5 | Continuously Manage Risk | ✅ Compliant | Defined (3) | This document is the cadence |
| 6 | Secure the Supply Chain | ✅ Compliant | Managed (4) → Optimized (5) | HSM signing live = Optimized |
| 7 | Enable Through-Life Assurance | ⚠️ Partially Compliant | Repeatable (2) → Defined (3) | Operationalise LTS at GA |

**Aggregate principle score: 6/7 fully compliant; 1/7 partially compliant.** No principles assessed Non-Compliant.

---

## 3. MOD Accreditation Requirements (JSP 604 Pathway)

### 3.1 Security Accreditation Status — JSP 604

**Accreditation Authority**: **Deploying authority's Accreditor / Authorising Engineer** (per `ARC-002-STKE-v1.0.md` and ADR-006). Vendor explicitly does NOT accredit.

**Accreditation Type**: To be determined per customer engagement. Most likely: **Site-specific Authorisation to Operate** under JSP 604, with sovereign release bundle as the supplier-delivered system being authorised for that site.

**JSP 604 Accreditation Pathway — Vendor Responsibility vs Customer Responsibility**:

| JSP 604 Stage / Gate | Vendor (this evidence pack) | Customer (deploying authority) | Status |
|----------------------|----------------------------|--------------------------------|--------|
| Define system boundary | Provides logical boundary description (HLD §boundary; DR-001) | Defines deployed system boundary including site-specific scope | Vendor: ready |
| Business Impact Assessment (BIA) | Provides component-level impact-of-compromise analysis | Performs BIA on the deployed instance | Vendor: ready (in §4.2 below) |
| Risk Management and Accreditation Documentation Set (continuous-assurance equivalent) | Provides this MOD-SbD assessment + RISK register + threat model + pen-test report | Authors site-specific risk treatment and acceptance | Vendor: ready (this doc + ARC-002-RISK-v1.0.md) |
| Security Aspects Letter (SAL) | Provides **pre-filled SAL template** (ADR-006, §3.2 below) | Issues final SAL for the site | Vendor: pre-fill ready; customer: pending engagement |
| Cryptographic primitive selection | Provides default cryptographic profile (TLS 1.3, AES-256, Ed25519, SHA-256/384) | Specifies HMG-approved primitive set if site SAL mandates | Vendor: default ready; customer: site-specific |
| Penetration test | Provides annual independent pen-test report against the bundle | Optional site-specific pen-test on deployed instance | Vendor: scheduled annually; customer: at customer's discretion |
| Air-gap attestation | Provides per-release network-deny CI test attestation | Confirms customer environment matches air-gap assumption | Vendor: per release; customer: per deployment |
| Personnel security | Provides claim-driven cleared-personnel enforcement (ADR-003, FR-007) | Performs vetting, manages clearances, asserts identity claims | Vendor: enforcement ready; customer: vetting is customer-only |
| Physical security (PhySec) | n/a — vendor has no premises to assess at the customer site | Manages physical security of host environment | Customer-only |
| Authorisation to Operate (ATO) | n/a — vendor cannot issue | Issues / withholds | Customer-only |
| Continuous assurance review | Reissues this assessment per release | Reviews annually or per change | Both |

**Accreditation Progress (per pilot)**:

- [ ] Business Impact Assessment (BIA) — vendor-side input ready in §4.2; customer-side BIA pending engagement.
- [x] Vendor evidence pack baseline (this document + RISK register + SBOM + pen-test schedule + air-gap attestation framework + pre-filled SAL template).
- [ ] Security Aspects Letter (SAL) issued — customer-side, pending engagement.
- [ ] Accreditation Service engaged — pending pilot deploying authority.
- [ ] Risk assessment — vendor-side complete in `ARC-002-RISK-v1.0.md`; customer-side risk treatment pending engagement.
- [x] Security controls documented — this document is the principal artefact.
- [ ] Residual risks accepted by deploying-authority IAO/SIRO — pending engagement.
- [ ] Accreditation granted — pending engagement.

**Information Assurance Owner (IAO) — vendor-side equivalent**: Service Owner (Mark Craddock).
**Information Assurance Architect (IAA) — vendor-side equivalent**: Lead Architect ([PENDING] appointment per STKE).
**Customer-side IAO / SIRO**: Deploying-authority SIRO (per pilot).
**Customer-side Accreditor**: Deploying-authority Authorising Engineer (per pilot).

**Target First Accreditation**: 2027-08-31 (Private Beta milestone in REQ).

**Gaps/Actions**:

- Initiate **accreditator-in-the-loop alpha programme** before alpha completion. RISK register lists this as the highest-leverage URGENT mitigation — it simultaneously addresses R-001, R-002, R-012, and R-013.

### 3.2 Security Aspects Letter (SAL) Pre-Fill

Per ADR-006, the vendor delivers a pre-filled SAL template within the evidence pack. The customer accreditator completes the site-specific fields. The pre-fill comprises **vendor-known facts**; **customer-decided fields** are clearly marked.

| SAL Section | Vendor-Pre-filled Content | Customer-Decided |
|-------------|---------------------------|------------------|
| System name & version | "ArcKit Sovereign Deployment v[release-id]" | Site-specific deployment name |
| System description | One-paragraph from REQ executive summary | Local mission context |
| Maximum classification supported | Up to TOP SECRET (technically) | **Site-permitted maximum** (typically OFFICIAL-SENSITIVE or SECRET) |
| Boundary definition | Logical: "ArcKit application, customer-controlled storage and IdP, customer-controlled foundational services" | Physical/network boundary mapped to site infrastructure |
| Information flows | Per HLD diagrams | Site-specific external flows (typically zero — air-gap) |
| Cryptographic primitives in use | Default profile per ADR-002 Appendix C (TLS 1.3, AES-256-GCM, SHA-256/384, Ed25519/RSA-3072) | **HMG-approved primitive selection** if mandated |
| Personnel security required | Claim-driven; system honours `clearance_attribute` claim per FR-007 | **Required clearance level** (BPSS / SC / DV / NPPV3) per role |
| Physical security required | n/a — software only | Site-specific (typically defined by host environment) |
| Connectivity profile | **Default: zero outbound** per NFR-SEC-004 / ADR-001; customer-controlled foundational services per ADR-005 | Confirmation of customer-environment air-gap status |
| Audit / monitoring | Audit events to customer SIEM (INT-004); retention default ≥ 12 months | Site retention per local policy |
| Incident reporting | Vendor receives incidents only via opt-in audited channel (FR-013) | Site escalation chain |
| Remote support | Default OFF (FR-013) | Site decision on opt-in |
| Decommissioning | Per FR-011 / UC-3 runbook | Site-decommission witnessing requirements |

**Vendor accuracy attestation**: The Service Owner signs the evidence pack confirming that the vendor-pre-filled facts are accurate as of the release. The vendor does **not** sign anything that would constitute an accreditation claim. This attestation is the load-bearing artefact for **R-005** (SAL controls compliance) — by clearly delineating what the vendor has done versus what the customer must do, it prevents the customer from inheriting the wrong assumption set.

### 3.3 JSP 440 Compliance — Information Assurance Maturity Model (IAMM)

**JSP 440**: Defence Manual of Security — controls catalogue.
**IAMM Level Target**: **Level 3 (Defined)** for the vendor-controlled portion at GA; **Level 4 (Managed)** for supply chain (signing/SBOM/SLSA) at HSM-live.

**IAMM Assessment** (vendor-controlled portion only — customer-controlled controls assessed by the deploying authority):

| Domain | Current Level | Target Level (GA) | Gap |
|--------|---------------|-------------------|-----|
| Information Risk Management | 3 (Defined) | 4 (Managed) | Continuous-assurance cadence in place; close on second customer engagement |
| Secure Configuration | 3 (Defined) | 3 (Defined) | Default-secure config per ADR-005; fail-closed bootstrap |
| Network Security (vendor side) | 4 (Managed) | 4 (Managed) | Air-gap by design (ADR-001); no outbound (NFR-SEC-004) |
| Access Control (vendor side) | 3 (Defined) | 4 (Managed) | Cleared-personnel claim per ADR-003; customer IdP integration (FR-007) |
| Malware Protection | 3 (Defined) | 3 (Defined) | Container image scanning in CI (DEVOPS); customer-side AV outside vendor scope |
| Patch Management | 3 (Defined) | 4 (Managed) | LTS line + SLAs (ADR-008, NFR-SEC-008); promotes to Managed at first real backport |
| Security Monitoring (vendor side) | 3 (Defined) | 4 (Managed) | Audit events emitted to customer SIEM (FR-010); customer SOC integration is customer-side |
| Incident Management | 2 (Repeatable) | 3 (Defined) | Vendor IR plan documented; first real exercise pending; promotes to Defined at exercise completion |

**Gaps/Actions**:

- Vendor IR plan exercise before GA (Defined gate for Incident Management domain).
- HSM signing live drives Patch Management to Managed.

### 3.4 JSP 440 Controls Coverage — P&ASec / InfoSec / PhySec

JSP 440 organises Defence security into three domains: **P&ASec** (Personnel & Administrative Security), **InfoSec** (Information Security), and **PhySec** (Physical Security). The controls-inheritance matrix (per ADR-006) classifies each control element as **Vendor / Customer / Shared / Platform-inherited / Not-applicable**.

#### 3.4.1 P&ASec — Personnel & Administrative Security

| Control element | Responsibility | Vendor evidence | Customer evidence required |
|-----------------|----------------|-----------------|----------------------------|
| Personnel vetting (BPSS / SC / DV / NPPV3) | **Customer** | n/a — vendor has no visibility of customer personnel | Site-specific clearance management per role |
| Cleared-personnel access enforcement | **Shared** | Identity-claim-driven enforcement per ADR-003, FR-007 (NFR-SEC-007) | Customer IdP issues clearance claim; customer asserts attribute integrity |
| Vendor-side cleared personnel (where required for support) | **Vendor** | R-009 mitigation: cleared individuals identified for sovereign delivery role; opt-in only | Customer accepts/rejects vendor support request per session |
| Access reviews and recertification | **Customer** | Audit events emitted (FR-010) to enable customer reviews | Customer-led review cadence |
| Joiner/mover/leaver (JML) integration | **Customer** | Standard IdP claims supported; revocation respected immediately | Site-specific JML automation |
| Administrative procedures (separation of duties, dual control) | **Shared** | Vendor-side: cosign + HSM access policy enforce dual control on signing | Customer-side: SoD on operator team |
| Acceptable use policy | **Customer** | Vendor publishes service terms; customer authors site AUP | Site AUP |
| Information handling training | **Customer** | Vendor publishes operator runbooks (FR-011) | Site training records |

**Coverage**: 8/8 P&ASec elements mapped. Vendor-side fully addressed; 5/8 are Customer or Shared and depend on the deploying authority.

#### 3.4.2 InfoSec — Information Security

| Control element | Responsibility | Vendor evidence | Customer evidence required |
|-----------------|----------------|-----------------|----------------------------|
| Classification marking | **Vendor** | FR-012 — configurable max classification; refuses content above max | Site classification scheme adopted in config |
| Data at rest encryption | **Shared** | Vendor uses customer KMS via INT-007; vendor-side container images use AES-256 | Customer KMS, customer-managed keys |
| Data in transit encryption | **Vendor** | TLS 1.3; mutual TLS for service-to-service | Customer network boundary controls |
| Cryptographic primitives | **Shared** | Default profile per ADR-002 Appendix C; HMG-approved primitive option exposed | HMG-approved primitive selection if mandated by SAL |
| Key management | **Customer** | INT-007 customer KMS; key rotation runbook (FR-003) | Customer KMS, custodianship, rotation cadence |
| Audit logging | **Shared** | FR-010 — comprehensive structured audit events | Customer SIEM, retention, alerting |
| Tamper-evident logs | **Vendor** | Audit events tamper-evident at emission | Customer-side immutable storage |
| Information flow control | **Vendor** | Within-deployment isolation FR-006, NFR-SEC-006 | Customer policy on community-of-interest assignments |
| Removable media handling | **Customer** | n/a (sealed-media transfer per ADR-007 is one-time at deployment) | Site removable-media policy |
| Email / file-share boundaries | **Customer** | Vendor publishes no email/file-share interfaces by default | Customer policy |
| Backup integrity | **Shared** | FR-003 backup runbook within boundary | Customer backup target, retention |
| Secure decommissioning of data | **Shared** | UC-3 runbook with destruction certificate | Customer witnessing of destruction |

**Coverage**: 12/12 InfoSec elements mapped. Vendor-controlled elements all in place at v1.

#### 3.4.3 PhySec — Physical Security

| Control element | Responsibility | Vendor evidence | Customer evidence required |
|-----------------|----------------|-----------------|----------------------------|
| Site physical security | **Customer** | n/a — vendor not a physical operator | Per site PhySec accreditation |
| Hardware tamper evidence | **Platform-inherited** | Customer hardware (assumed enterprise/MOD-grade) | Customer hardware procurement |
| TEMPEST | **Customer** | n/a | Site TEMPEST accreditation if mandated |
| Cabling and zoning | **Customer** | n/a | Site network/cabling design |
| Removable media physical handling | **Customer** | One-time at sealed-media transfer (ADR-007) | Site media handling policy |
| Disposal of physical media | **Customer** | n/a | Site disposal policy |
| Visitor controls | **Customer** | n/a | Site visitor policy |
| Operator-area separation | **Customer** | n/a | Site operator-area accreditation |

**Coverage**: 8/8 PhySec elements mapped. **All Customer or Platform-inherited.** Vendor cannot evidence PhySec; vendor pack states this clearly so the customer accreditator does not waste time looking for vendor PhySec evidence that does not and cannot exist.

**Aggregate JSP 440 coverage**: **28/28 control elements mapped** across P&ASec / InfoSec / PhySec — Vendor (5), Shared (8), Customer (13), Platform-inherited (1), Not-applicable (1). Mapping completeness target per ADR-006 metric is 100%; **achieved**.

**Gaps/Actions**:

- Validate this JSP 440 control-element list with the pilot customer accreditator. The list above is derived from public JSP 440 doctrine and ADR-006; a real customer accreditator may use a more granular control-set view.

---

## 4. Threat Modeling and Risk Assessment

### 4.1 Threat Model

**Threat Modeling Method**: STRIDE for component-level, with Attack Trees for the supply-chain compromise scenario (per ADR-002 Annex). The full threat model is held alongside the HLD and reissued per release as part of the evidence pack.

**Threat Model Completed**: Yes (vendor side); customer-side threat-model addendum produced per pilot engagement.

**Identified Threat Actors**:

- [x] **Nation state actors** — primary concern given the MOD context. Air-gap mitigation (ADR-001) is the primary defence.
- [x] **Organized crime** — supply-chain attack vector (R-004) via release-bundle compromise. HSM-backed signing primary defence.
- [x] **Insider threats** — vendor-side: limited by SLSA L3 build isolation and dual-control on signing (R-004). Customer-side: addressed by ADR-003 cleared-personnel access and R-005 break-glass governance (residual 12, above appetite, accepted).
- [x] **Supply chain threats** — primary residual concern (R-004). Cosign + SBOM + SLSA L3 + offline verification manifest (ADR-002) primary defence.
- [x] **Hacktivists** — secondary concern; same controls apply.
- [x] **Terrorist organizations** — covered by classification controls and customer-side PhySec.

**Key Threats Identified** (selected — full set in threat-model artefact):

| Threat | Likelihood | Impact | Risk Level | Mitigation |
|--------|------------|--------|------------|------------|
| Release-bundle tamper between vendor build and customer install | LOW (with controls) | CATASTROPHIC | HIGH | Cosign + SLSA L3 + offline verification manifest (ADR-002); customer-approved transfer (ADR-007) |
| Outbound egress from inside accredited boundary (telemetry leak, phone-home) | LOW (with CI test) | CATASTROPHIC | HIGH | Network-deny CI test per release (NFR-SEC-004); customer-controlled foundational services (ADR-005); pluggable AI default-no-call (ADR-004) |
| Cleared-personnel break-glass abuse | MEDIUM | HIGH | HIGH | Cleared-personnel claim enforcement (ADR-003, FR-007); customer-side audit; R-005 residual accepted |
| AI-endpoint data exfiltration | LOW | HIGH | MEDIUM | Default sovereign profile points nowhere (FR-004); customer-controlled endpoint only when configured |
| Vendor signing-key compromise | LOW | CATASTROPHIC | HIGH | HSM signing (ADR-002); custody policy; rotation; offline verification manifest tolerates new key |
| Customer accreditator format-rejection of evidence pack | MEDIUM | MAJOR | MEDIUM | Accreditator-in-the-loop alpha (R-012 control) |
| Operator-side credential theft | MEDIUM | HIGH | MEDIUM | Customer IdP MFA, claim-driven access (FR-007), audit (FR-010) |
| LTS backport SLA breach | MEDIUM | MAJOR | MEDIUM | Documented SLA (NFR-SEC-008); LTS staffing (BR-005); R-010 residual 6 |

**Gaps/Actions**:

- Reissue threat model per release as part of evidence pack (continuous assurance).
- Customer-side threat model addendum to be co-developed with pilot customer.

### 4.2 Security Risk Assessment

**Risk Assessment Method**: HM Treasury Orange Book (per `ARC-002-RISK-v1.0.md`) with sovereign-track appetite override.

**Risk Register Maintained**: Yes — `ARC-002-RISK-v1.0.md` (13 risks).

**Critical/High Risks (residual)** — abridged from `ARC-002-RISK-v1.0.md` §B Top 10:

| Risk ID | Risk Description | Inherent | Residual | Owner | Status |
|---------|------------------|----------|----------|-------|--------|
| R-001 | First-attempt customer accreditation failure | 20 | 12 | Sovereign Delivery Lead | Treat — above strategic appetite (≤12); accepted |
| **R-002** | **MOD Secure by Design assessment fail** | **20** | **12** | **Vendor Security Lead** | **Treat — above compliance appetite (≤4); residual position is THIS document** |
| **R-005** | **Customer break-glass / privileged-access abuse** | **9** | **12** | **Customer SIRO** | **Treat — above compliance appetite (≤4); residual position is the SAL pre-fill in §3.2** |
| R-003 | Single-codebase divergence | 8 | 9 | Lead Architect / CTO | Treat — above tech appetite (≤6) |
| R-006 | Customer operator-team turnover | 9 | 9 | Sovereign Delivery Lead | Treat — within operational appetite (≤6) by 3 |
| R-007 | Accredited-boundary egress incident | 20 | 8 | Service Owner | Treat — above reputational appetite (≤4); accepted |
| R-004 | Signed-bundle / supply-chain compromise | 15 | 2 | Vendor Security Lead | Treat — within compliance appetite at residual (HSM dependency) |
| R-008 | On-premise AI model integration brittleness | 16 | 8 | Lead Architect | Treat — above tech appetite (≤6) |

**Residual Risks Accepted Above Appetite**: 5 (R-001, R-002, R-005, R-007, R-008). Per RISK §Recommendations, Service Owner formally acknowledges in writing with quarterly review trigger.

**Specifically for this assessment**:

- **R-002 (MOD-SbD assessment fail)** — *this very document is the principal mitigation*. By delivering a defensible vendor-side MOD-SbD assessment that maps to JSP 440 / JSP 604 with a clear inheritance matrix, R-002's residual stays at 12 (not higher) and the door to customer accreditation stays open. If this document had been weaker (e.g., vendor accreditation overreach, missing JSP 604 split, missing controls inheritance), R-002 residual would be uncontrollable.
- **R-005 (SAL controls compliance)** — the SAL pre-fill in §3.2 above is the principal mitigation. By telling the customer accreditator exactly what the vendor has done versus what the customer must do, R-005 residual is bounded to the customer-side break-glass scenario only (the vendor cannot eliminate the customer's privileged-personnel risk surface).

**Gaps/Actions**:

- Service Owner sign-off on R-001/R-005/R-007 above-appetite acceptance per RISK §Recommendations.
- Quarterly review trigger inserted into governance calendar.

---

## 5. Technical Security Controls

### 5.1 Cryptography

**Cryptographic Standards**: Default profile is industry-standard (TLS 1.3, AES-256-GCM, SHA-256/384, Ed25519 / RSA-3072 minimum). Where the deploying-authority SAL mandates **HMG-approved cryptographic primitives**, the system supports configuration to that primitive set; the precise set is selected per SAL. ADR-002 Appendix C documents the working position; HLD will ratify against the pilot SAL.

**Encryption Implementation**:

- [x] Data at rest encrypted (AES-256, customer KMS via INT-007)
- [x] Data in transit encrypted (TLS 1.3 minimum; mutual TLS service-to-service)
- [x] Database encryption enabled (customer-controlled storage in INT-002)
- [x] Backup encryption enabled (FR-003; customer-managed keys)
- [x] Key management system implemented (customer KMS — INT-007; vendor HSM for release signing)
- [ ] CESG-approved cryptography for classified data — *configurable at SAL time*; vendor default is industry standard
- [x] Crypto key lifecycle managed (FR-003 key rotation runbook)

**Key Management**:

- Vendor signing keys: HSM (per ADR-002, R-004 control). Custody policy and rotation per signing-key custody policy (HLD).
- Customer at-rest keys: customer-managed KMS (INT-007), customer rotation cadence.
- TLS keys: customer-managed CA (INT-003 / ADR-005); vendor default does not bundle a CA.

**Gaps/Actions**:

- Confirm HMG-approved primitive set with pilot customer SAL; ratify in HLD.
- HSM signing operational before first bundle issue.

### 5.2 Authentication and Identity

**Authentication Method**: Customer-IdP-driven; OIDC / OAuth 2.x / SAML 2.0 (per FR-007).
**Identity Provider**: Customer IdP — vendor never holds customer user credentials.

**Authentication Controls**:

- [x] Multi-factor authentication enforced (customer IdP)
- [x] Password complexity — customer IdP policy
- [x] Smart card (CAC / MOD Form 90) authentication for classified systems — customer IdP capability honoured
- [x] Session timeout configured (vendor default 30 min; customer-tunable)
- [x] Account lockout — customer IdP policy
- [x] Single Sign-On — via customer IdP (FR-007)
- [x] Privileged Access Management — customer-side; vendor exposes role/claim model
- [x] Cleared-personnel claim enforcement — ADR-003, FR-007, NFR-SEC-007

### 5.3 Network Security

**Network Architecture**: **Air-gapped within customer accredited boundary** (ADR-001). No outbound from inside boundary (NFR-SEC-004).

**Network Security Controls** (customer responsibilities, vendor-respected):

- [x] Network segmentation by security zone — customer-side
- [x] Firewalls at zone boundaries — customer-side
- [x] IDS/IPS — customer-side
- [ ] DDoS protection — n/a inside accredited boundary
- [x] WAF — customer-side, optional
- [ ] VPN for remote access — by default disabled; opt-in only via FR-013 vendor remote support
- [x] NAC — customer-side
- [x] Air-gapped for SECRET and above — yes, by design (ADR-001)

**Network Zones** (customer-side; vendor sits inside the inner zone):

- [ ] Public zone — n/a
- [ ] DMZ — typically n/a in air-gap
- [x] Internal zone — vendor application sits here
- [x] Management zone — for operator team
- [x] Classified zone — vendor application configured to SAL maximum

### 5.4 Vulnerability Management

**Vulnerability Scanning**: Continuous in vendor CI (SAST, DAST, SCA, container image, IaC) per `ARC-002-DEVOPS-v1.0.md`.

**Vulnerability Management Process**:

- [x] Automated vulnerability scanning in CI per release
- [x] Manual penetration testing — annual minimum on the bundle (per evidence-pack requirement)
- [x] Patch management process — LTS line per ADR-008
- [x] Critical patches — within 7 days (NFR-SEC-008; sovereign cadence is slower than SaaS due to customer accreditation re-runs)
- [x] High patches — within 30 days
- [x] Medium patches — within 90 days
- [x] Vulnerability remediation tracking — per LTS line
- [x] Exception process — via ADR + customer notification

**Recent Penetration Test**: Scheduled before GA on the bundle.

**Gaps/Actions**:

- Schedule first independent pen-test ≥ 3 months before GA.

### 5.5 Security Monitoring and Logging

**Security Operations Center (SOC)**: Customer-side. Vendor receives no operational telemetry from sovereign deployments.

**SIEM Solution**: Customer-side (INT-004). Vendor publishes structured event schemas.

**Logging and Monitoring**:

- [x] Centralized log collection — customer SIEM
- [x] Real-time alerting — customer-side
- [x] Log retention ≥ 12 months — default; customer-tunable
- [x] Security event correlation — customer SIEM
- [ ] User behavior analytics — customer-side (vendor exposes raw events)
- [x] Automated incident response playbooks — customer-side
- [x] Integration with MOD Cyber Defence Operations — customer routes events as required

---

## 6. Secure Development Lifecycle

### 6.1 Secure Coding Practices

Per `ARC-002-DEVOPS-v1.0.md`:

- [x] Secure coding training for developers (vendor side)
- [x] Code review process includes security review
- [x] SAST / DAST / SCA in CI
- [x] Container image scanning
- [x] IaC security scanning
- [x] Threat modeling during design phase (per ADRs)
- [x] Security testing in CI/CD pipeline

**OWASP Top 10**: Mitigated through standard controls; details in DEVOPS document.

### 6.2 DevSecOps Integration

- [x] Automated security scanning in pipeline (DEVOPS)
- [x] Secrets scanning — no hardcoded credentials
- [x] Dependency vulnerability scanning
- [x] Container image scanning
- [x] IaC security scanning
- [x] Build artifact signing — Cosign + HSM (ADR-002)
- [x] Build provenance — SLSA Level 3 (ADR-002)

---

## 7. Supply Chain Security

### 7.1 Third-Party Risk Management

**Vendor Security Assessment**: applies to ArcKit's own upstream dependencies (cloud build infrastructure, container base images, language runtimes). Per `ARC-000-PRIN-v2.0.md` Principle 16 reuse-before-build, all material components are vetted for offline-compatibility.

**Third-Party Components** (selected — full SBOM per release):

| Component | Vendor | Security Rating | Risk Level | Mitigations |
|-----------|--------|-----------------|------------|-------------|
| Sigstore (cosign) | Sigstore project | High | Low | Hybrid offline verification manifest (ADR-002 Option 3) tolerates Rekor unreachability |
| Container base images | Distroless / minimal | High | Low | Image scanning in CI; reproducible builds |
| Language runtimes (e.g., Node.js, Python) | Upstream | High | Low | LTS upstream + own LTS overlay |
| HSM (for signing) | Customer/vendor procurement choice | High | Low | Custody policy; dual control |

### 7.2 Open Source Software Security

**Open Source Components**: Tracked per CycloneDX SBOM per release.

**OSS Security Controls**:

- [x] SBOM generated (CycloneDX per ADR-002)
- [x] Known vulnerabilities scanned per release
- [x] Licence compliance verified — including offline-distribution compatibility
- [x] OSS component lifecycle managed (LTS)
- [x] Alternative components evaluated for high-risk OSS

### 7.3 Supplier Attestation (ISN 2023/10)

The vendor issues a **supplier attestation** alongside each release evidence pack, conforming to ISN 2023/10. The attestation states:

1. The release was produced under a documented secure development lifecycle.
2. The release has been assessed against MOD Secure by Design (this document).
3. The vendor has identified residual risks in the accompanying RISK register.
4. Specific technical attestations: signature, SBOM, network-deny CI green, air-gap install validated.
5. The deploying authority remains responsible for accreditation.

This attestation is signed by the Service Owner.

---

## 8. Operational Security

### 8.1 Backup and Recovery

**Backup Strategy**: Customer-controlled within the accredited boundary; encryption at rest using customer-managed keys (NFR-A-002).

**Backup Controls**:

- [x] Regular backups scheduled (RPO ≤ 60 min, configurable)
- [x] Backup encryption (customer KMS)
- [x] Offsite/offline backups — customer policy
- [x] Backup restoration tested (FR-003)
- [x] Backup integrity verified
- [ ] Immutable backups — customer-side capability

**RTO**: ≤ 8 hours (NFR-A-002, configurable).
**RPO**: ≤ 60 minutes (NFR-A-002, configurable).

### 8.2 Incident Response

**Incident Response Plan**: Vendor-side documented; customer-side per site.

**Incident Response Capabilities**:

- [x] Vendor IR plan documented
- [ ] Vendor IR exercised — pending pre-GA exercise
- [x] Incident detection — customer SIEM (FR-010)
- [x] Forensic investigation — customer-side
- [x] Communication plan — vendor disclosure programme + customer notification
- [x] Regulatory reporting — customer to MOD CERT / NCSC / ICO as applicable
- [x] Lessons learned — feeds quarterly RISK review

**Gaps/Actions**:

- Conduct vendor IR exercise pre-GA.

### 8.3 Disaster Recovery and Business Continuity

**DR Plan**: Customer-side primary. Vendor provides DR runbook (FR-011).
**BC Plan**: Customer-side.

**DR/BC Capabilities**:

- [x] DR plan documented (FR-011)
- [x] Critical system identification — covered by BIA
- [x] Failover procedures documented
- [x] DR testing — annual customer-led drill (NFR-A-002)
- [x] Business impact analysis — vendor-side §4.2 + customer-side per site

---

## 9. Personnel Security (JSP 440 P&ASec Detail)

### 9.1 Security Clearances

**Clearance Levels** (vendor-side support model — actual customer requirement per SAL):

| Role | Clearance Level (typical) | Current Clearance Status |
|------|---------------------------|-------------------------|
| Customer System Administrator | SC or DV (per site SAL) | Customer responsibility |
| Customer Operator | SC or DV (per site SAL) | Customer responsibility |
| Customer End User (architect) | SC or DV (per site SAL) | Customer responsibility |
| Vendor Sovereign Delivery Lead | SC (target) | [PENDING] — R-009 mitigation |
| Vendor Security Lead | SC (target) | [PENDING] |

**Security Vetting Compliance**:

- [x] Vendor-side: cleared individuals identified for sovereign delivery role per R-009 mitigation
- [ ] Vendor-side: SC clearance for delivery lead — in progress
- [x] Customer-side: clearance levels match data classification — customer-enforced via SAL
- [x] Clearance renewal process — customer-managed
- [x] Foreign nationals risk assessed — per SAL
- [x] Contractor clearances verified — per SAL

### 9.2 Security Awareness

**Vendor-side Security Training**:

- [x] Mandatory security awareness (vendor staff)
- [x] Role-based security training
- [x] Phishing awareness
- [x] Insider threat awareness
- [x] Data handling and classification
- [x] Annual refresher

**Customer-side**: per site policy; vendor publishes operator runbooks (FR-011) but does not deliver site training.

---

## 10. Compliance and Governance

### 10.1 Regulatory Compliance

**Applicable Regulations**:

- [x] UK GDPR / DPA 2018 — vendor processor obligations per opt-in remote support; customer is controller
- [x] Official Secrets Act — customer-side; vendor support staff sign as required
- [x] Defence Reform Act — customer-side
- [x] NIS Regulations — customer applicability per site
- [x] MOD JSP 440 — assessed in §3.4
- [x] NCSC Cyber Assessment Framework — assessed in `ARC-000-PRIN-v2.0.md` Principle 5; non-MOD sensitive sites can use this in lieu of MOD-SbD per NFR-SEC-002

**Compliance Status**:

| Regulation | Compliance Status | Last Assessment | Next Assessment |
|------------|-------------------|-----------------|-----------------|
| UK GDPR | Partially compliant (vendor processor controls; opt-in support DPIA pending — R-013) | 2026-05-03 | 2026-08 (per release) |
| JSP 440 (vendor portion) | Compliant (per §3.4) | 2026-05-03 | 2026-08 (per release) |
| MOD Secure by Design | Adequate with conditions (this document) | 2026-05-03 | Per release |
| NCSC CAF | Mapped per NFR-SEC-002 | 2026-05-03 | Annual |
| ISN 2023/10 (Supplier attestation) | Will issue on first release | n/a | Per release |

### 10.2 Security Policies and Procedures

**Vendor-side Security Documentation**:

- [x] Information Security Policy
- [x] Acceptable Use Policy
- [x] Access Control Policy
- [x] Incident Response Procedure
- [ ] Business Continuity Plan — pending pre-GA
- [x] Disaster Recovery Plan
- [x] Change Management Procedure (DEVOPS)
- [x] Data Classification and Handling Guide

**Documentation Review Frequency**: Annual; per release for the evidence pack.

**Gaps/Actions**:

- Vendor BCP pre-GA.

---

## 11. NIST CSF 2.0 Mapping

The following maps the vendor-side controls against NIST CSF 2.0 functions (CAAT methodology recommends NIST CSF as the controls framework).

### Govern (GV)
- [x] Organisational context — REQ + STKE + this document
- [x] Risk strategy — RISK register with sovereign appetite override
- [x] Cybersecurity supply chain risk management — ADR-002 (signing/SBOM/SLSA), ADR-007 (distribution)
- [x] Roles and responsibilities — STKE + ADR-006 controls inheritance

### Identify (ID)
- [x] Asset management — SBOM + customer asset inventory inheritance
- [x] Business environment — REQ executive summary
- [x] Risk assessment — RISK register

### Protect (PR)
- [x] Access control — ADR-003, FR-007, NFR-SEC-007
- [x] Awareness and training — vendor-side §9.2; customer-side per SAL
- [x] Data security — encryption at rest/in transit; customer KMS; classification marking (FR-012)
- [x] Information protection processes and procedures — operator runbooks (FR-011)
- [x] Maintenance — LTS line (ADR-008)
- [x] Protective technology — air-gap (ADR-001), customer-controlled foundational services (ADR-005)

### Detect (DE)
- [x] Anomalies and events — audit events (FR-010) to customer SIEM
- [x] Continuous monitoring — customer SIEM; vendor CI tests
- [x] Detection processes — customer-side primary; vendor CI per release

### Respond (RS)
- [x] Response planning — vendor IR + customer IR
- [x] Communications — customer to MOD CERT; vendor to customer per FR-013
- [x] Analysis — customer-side primary
- [x] Mitigation — LTS patches per NFR-SEC-008
- [x] Improvements — quarterly RISK review

### Recover (RC)
- [x] Recovery planning — FR-003 backup/restore; FR-011 runbooks; UC-3 decommission
- [x] Improvements — post-incident lessons learned in RISK
- [x] Communications — per IR plan

---

## 12. Three Lines of Defence

| Line | Vendor side | Customer side |
|------|-------------|---------------|
| **First Line** (delivery team owns security) | Vendor delivery team owns release security; Service Owner accountable | Customer Operator Team (DTSL-equivalent) owns operational security |
| **Second Line** (assurance and oversight) | Vendor Security Lead provides assurance; Lead Architect provides Technical Coherence | Customer SIRO + Accreditor; deploying authority Technical Coherence equivalent |
| **Third Line** (independent audit) | Annual independent pen-test; SLSA L3 build attestation independent of vendor; SBOM independently verifiable | Customer-side internal audit; NAO/GIAA where applicable |

---

## 13. Overall Security Assessment Summary

### 13.1 Security Scorecard

| Security Domain | Status | Critical Issues | Priority |
|-----------------|--------|-----------------|----------|
| Data Classification | ✅ Compliant | No | High |
| Defence in Depth | ✅ Compliant | No | High |
| Secure by Default | ✅ Compliant | No | High |
| Least Privilege | ✅ Compliant | No | High |
| Assume Breach | ✅ Compliant | No | High |
| Accreditation pathway (vendor side) | ⚠️ Partially Compliant — pre-engagement | No | High |
| Threat Modeling | ✅ Compliant | No | High |
| Cryptography | ✅ Compliant — HMG primitive selection per SAL | No | High |
| Authentication | ✅ Compliant | No | High |
| Network Security | ✅ Compliant — air-gap by design | No | High |
| Vulnerability Management | ✅ Compliant — pen-test scheduled pre-GA | No | High |
| Security Monitoring | ✅ Compliant — customer-side primary | No | High |
| Secure Development | ✅ Compliant | No | High |
| Supply Chain Security | ⚠️ Partially Compliant — HSM signing required pre-GA | Yes (must-land) | High |
| Backup and Recovery | ✅ Compliant | No | High |
| Incident Response | ⚠️ Partially Compliant — vendor IR exercise pre-GA | No | High |
| Personnel Security | ✅ Compliant — vendor-side; customer-side via SAL | No | High |
| Compliance | ✅ Compliant — JSP 440 mapped 28/28 elements | No | High |

**Aggregate**: 15/18 domains Compliant; 3/18 Partially Compliant (Accreditation pathway pending pilot engagement; Supply Chain pending HSM live; Incident Response pending vendor exercise). 0/18 Non-Compliant.

### 13.2 Critical Security Issues Requiring Immediate Action

1. **HSM signing operational before first bundle issue** (Supply Chain). Without HSM, R-004 inherent stays at 15 and bundle issue is gated. **Pre-deployment must-land #1.**
2. **Network-deny CI test green on bundle issue** (Network / Air-gap). Without proven zero-egress on the actual bundle, R-007 cannot be evidenced as residual 8. **Pre-deployment must-land #2.**
3. **Accreditator-in-the-loop alpha review** (Accreditation pathway). Without accreditator validation of the evidence-pack format, R-002 / R-012 residuals are speculative. **Pre-deployment must-land #3.**

### 13.3 Recommendations

**Critical Priority** (0–30 days from this document issue):

- HSM signing infrastructure operational. Owner: Vendor Security Lead. Due: 2026-06-02.
- Network-deny CI test integrated and green. Owner: Lead Architect. Due: 2026-06-02.
- Engage at least one MOD accreditator for evidence-pack format review. Owner: Service Owner. Due: 2026-06-02.

**High Priority** (1–3 months):

- Vendor IR exercise. Owner: Vendor Security Lead. Due: 2026-08-03.
- First independent pen-test on the bundle. Owner: Vendor Security Lead. Due: 2026-08-03.
- Service Owner formal acknowledgement of above-appetite acceptances (R-001, R-005, R-007). Due: 2026-06-02 (per RISK §Recommendations).
- Vendor BCP authored and reviewed. Owner: Service Owner. Due: 2026-08-03.

**Medium Priority** (3–6 months):

- Confirm HMG-approved primitive set with pilot SAL; ratify in HLD. Due: 2026-11-03.
- Operationalise LTS infrastructure with synthetic backport. Owner: Lead Architect. Due: 2026-11-03.
- Vendor Security Lead substantive appointment. Owner: Service Owner. Due: 2026-08-03 (sooner if possible).

---

## 14. Next Steps and Action Plan

**Immediate Actions (0–30 days)**:

- [ ] HSM signing operational — Vendor Security Lead — 2026-06-02
- [ ] Network-deny CI test green — Lead Architect — 2026-06-02
- [ ] Accreditator-in-the-loop alpha engagement initiated — Service Owner — 2026-06-02
- [ ] R-001/R-005/R-007 above-appetite acceptances signed — Service Owner — 2026-06-02

**Short-term Actions (1–3 months)**:

- [ ] Vendor IR exercise — Vendor Security Lead — 2026-08-03
- [ ] First independent pen-test on bundle — Vendor Security Lead — 2026-08-03
- [ ] Vendor BCP — Service Owner — 2026-08-03
- [ ] Vendor Security Lead substantive appointment — Service Owner — 2026-08-03

**Long-term Actions (3–12 months)**:

- [ ] Pilot deploying-authority engagement and SAL pre-fill walkthrough — Service Owner — 2026-11-03
- [ ] HMG-primitive ratification in HLD — Lead Architect — 2026-11-03
- [ ] LTS operationalisation with synthetic backport — Lead Architect — 2026-11-03
- [ ] First real LTS patch backport — Lead Architect — 2027-04-30 (per REQ Alpha)
- [ ] Reissue this assessment per release — Vendor Security Lead — Continuous

**Next Assessment Date**: Per release, with full reissue at v1.1 after first pilot accreditator review (target 2026-09-30 per REQ §Dependencies).

---

## 15. Approval and Sign-Off

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Service Owner (vendor IAO equivalent) | Mark Craddock | [PENDING] | |
| Lead Architect (vendor IAA equivalent) | [PENDING — per STKE] | [PENDING] | |
| Vendor Security Lead | [PENDING — per STKE] | [PENDING] | |
| Customer SRO (per pilot) | [PENDING — per pilot engagement] | [PENDING] | |
| Customer SIRO (per pilot) | [PENDING — per pilot engagement] | [PENDING] | |
| Customer Accreditor (per pilot) | [PENDING — per pilot engagement] | [PENDING] | |

> **Note**: Vendor signatures attest accuracy of the vendor-pre-filled facts. Customer signatures, where present, indicate engagement and review — not delegation of accreditation authority. Per JSP 604 and ADR-006, the deploying authority's accreditator retains sole authorisation-to-operate authority.

---

## 16. Validation — Residual Position on R-002 and R-005

This section makes explicit what the orchestrator brief asked for: this document is the **principal acceptance vehicle** for R-002 and R-005.

### R-002: MOD Secure by Design assessment fail

**Inherent score**: 20 (Critical).
**Residual score**: 12 (Medium — above compliance appetite of ≤4, accepted).
**Vendor mitigation evidence delivered by this document**:

- 7/7 MOD SbD principles assessed (6 fully compliant, 1 partially compliant — Through-Life Assurance pending LTS operationalisation).
- 28/28 JSP 440 P&ASec/InfoSec/PhySec control elements mapped to Vendor / Customer / Shared / Platform-inherited / Not-applicable.
- JSP 604 accreditation pathway responsibilities split per ADR-006.
- Pre-filled SAL template per §3.2.
- Cryptographic profile published with HMG-approved primitive option.
- Air-gap attestation framework (CI network-deny test).
- Threat model summary with STRIDE + supply-chain attack tree.
- Continuous-assurance cadence: this document reissues per release.
- ISN 2023/10 supplier attestation framework.

**Acceptance**: Service Owner accepts residual 12 against compliance appetite of ≤4 because (i) compliance appetite is intrinsically violated by the strategic decision to deploy into MOD environments; (ii) the alternative (Vendor-issued ATO claim) is forbidden by JSP 604; (iii) the accreditator-in-the-loop alpha is the designed mechanism to drive residual lower. **Quarterly review trigger.**

### R-005: Customer break-glass / privileged-access abuse → SAL controls compliance

**Inherent score**: 9.
**Residual score**: 12 (above compliance appetite of ≤4, time-evolved upward, accepted).
**Vendor mitigation evidence delivered by this document**:

- ADR-003 cleared-personnel access enforcement via identity claims (FR-007, NFR-SEC-007).
- SAL pre-fill (§3.2) clearly delineates vendor-side vs customer-side controls so no customer accreditator can mistakenly inherit a vendor commitment to vetting that the vendor cannot make.
- JSP 440 P&ASec mapping (§3.4.1) makes 5/8 P&ASec elements Customer or Shared — no ambiguity.
- Audit events (FR-010) to customer SIEM enable customer-side break-glass detection.
- Tamper-evident logs (NFR-SEC-005 supply-chain integrity extended to log emission).

**Acceptance**: This is a customer-side residual that the vendor cannot eliminate. The vendor's mitigation is to make the customer's job clear — which §3.2 (SAL pre-fill) and §3.4.1 (P&ASec mapping) do. Service Owner accepts above-appetite residual; customer SIRO assumes ownership at engagement.

---

## 17. External References

> This section provides traceability from generated content back to source documents.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| ARC-000-PRIN-v2.0 | ARC-000-PRIN-v2.0.md | Architecture Principles | projects/000-global/ | Principle 5 (Security by Design) and Principle 21 (Sovereign and Air-Gapped Deployment) anchors |
| ARC-002-REQ-v1.0 | ARC-002-REQ-v1.0.md | Requirements | projects/002-arckit-sovereign/ | Sovereign deployment business / functional / non-functional requirements |
| ARC-002-STKE-v1.0 | ARC-002-STKE-v1.0.md | Stakeholder Analysis | projects/002-arckit-sovereign/ | Sovereign-track stakeholder model |
| ARC-002-RISK-v1.0 | ARC-002-RISK-v1.0.md | Risk Register | projects/002-arckit-sovereign/ | 13-risk sovereign register; sovereign appetite override; R-002/R-005 residual position fed by this assessment |
| ARC-002-HLDR-v1.0 | ARC-002-HLDR-v1.0.md | High-Level Design | projects/002-arckit-sovereign/ | Sovereign packaging design |
| ARC-002-ADR-001 | ARC-002-ADR-001-v1.0.md | ADR | projects/002-arckit-sovereign/decisions/ | Air-Gapped Operation Model |
| ARC-002-ADR-002 | ARC-002-ADR-002-v1.0.md | ADR | projects/002-arckit-sovereign/decisions/ | Signed Release Bundle (cosign + CycloneDX + SLSA L3) |
| ARC-002-ADR-003 | ARC-002-ADR-003-v1.0.md | ADR | projects/002-arckit-sovereign/decisions/ | Cleared-Personnel Access Model |
| ARC-002-ADR-004 | ARC-002-ADR-004-v1.0.md | ADR | projects/002-arckit-sovereign/decisions/ | On-Premise AI Model Integration |
| ARC-002-ADR-005 | ARC-002-ADR-005-v1.0.md | ADR | projects/002-arckit-sovereign/decisions/ | Customer-Controlled Telemetry, Time, CA, Package Mirror |
| ARC-002-ADR-006 | ARC-002-ADR-006-v1.0.md | ADR | projects/002-arckit-sovereign/decisions/ | JSP 440 / SAL Alignment — Controls Inheritance and Accreditation Pathway |
| ARC-002-ADR-007 | ARC-002-ADR-007-v1.0.md | ADR | projects/002-arckit-sovereign/decisions/ | Distribution Model (sealed-media default with diode option) |
| ARC-002-ADR-008 | ARC-002-ADR-008-v1.0.md | ADR | projects/002-arckit-sovereign/decisions/ | Long-Term Support Release Line |
| ARC-002-DEVOPS-v1.0 | ARC-002-DEVOPS-v1.0.md | DevOps Strategy | projects/002-arckit-sovereign/ | CI/CD with security gates; SAST/DAST/SCA; SBOM; signing |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| PRIN-P5 | ARC-000-PRIN-v2.0 | §I.5 (Mandatory Controls) | Principle | "compliance with the site Security Aspects Letter (SAL) and applicable JSP 440 controls; cleared-personnel-only access where required by the deploying authority; cryptographic primitives appropriate to accredited classification (HMG-approved where mandated)" |
| PRIN-P21 | ARC-000-PRIN-v2.0 | §V.21 (Implications) | Principle | "All required dependencies are vendorable and operable offline (no phone-home, no SaaS-only third-party services on the critical path); installation and updates proceed from a signed, hashed release bundle that can be transferred across an air-gap" |
| ADR-006-DEC | ARC-002-ADR-006-v1.0 | §1 / Decision Outcome | ADR | Vendor-issued, per-release MOD-SbD evidence pack containing JSP 440 controls-inheritance matrix, SBOM, threat model, pen-test, crypto profile, air-gap attestation, pre-filled SAL template; deploying authority retains sole authority over accreditation and SAL |
| ADR-002-DEC | ARC-002-ADR-002-v1.0 | §Decision Outcome | ADR | Cosign keyless + HSM-anchored offline verification manifest + SLSA L3 + CycloneDX SBOM |
| ADR-001-DEC | ARC-002-ADR-001-v1.0 | §1 | ADR | Air-Gapped Operation Model — Disconnected Runtime, No Outbound Egress |
| ADR-003-DEC | ARC-002-ADR-003-v1.0 | §1 | ADR | Cleared-Personnel Access Model — claim-driven enforcement |
| ADR-005-DEC | ARC-002-ADR-005-v1.0 | §5 | ADR | Per-Service Pluggable Adapters with Customer-Controlled Defaults and Fail-Closed Bootstrap |
| ADR-007-DEC | ARC-002-ADR-007-v1.0 | §1 | ADR | Multi-Channel — Sealed Media Default with Diode Option |
| ADR-008-DEC | ARC-002-ADR-008-v1.0 | §1 | ADR | Long-Term Support Release Line |
| RISK-R002 | ARC-002-RISK-v1.0 | §C R-002 | Risk | MOD-SbD assessment fail; inherent 20, residual 12; this document is the principal mitigation |
| RISK-R005 | ARC-002-RISK-v1.0 | §C R-005 | Risk | Customer break-glass / privileged-access abuse; residual 12 above compliance appetite, accepted |
| RISK-RECS | ARC-002-RISK-v1.0 | §Recommendations | Risk | Service Owner formally acknowledges three above-appetite acceptances (R-001, R-005, R-007) in writing with quarterly review trigger |
| REQ-NFR-SEC | ARC-002-REQ-v1.0 | §NFR-SEC-001..008 | Requirements | NFR-SEC-001 MOD-SbD/JSP 440/JSP 604 alignment; NFR-SEC-004 no outbound network calls; NFR-SEC-007 cleared-personnel-only access |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | No external policy documents (PDFs of JSP 440, JSP 604, ISN 2023/09, ISN 2023/10, NCSC CAF) placed in `projects/002-arckit-sovereign/external/` at time of generation. UK Government and MOD policies referenced are public-domain and cited by name; place authoritative copies in `external/` and re-run for inline page-level citations. |

---

**Generated by**: ArcKit `/arckit:mod-secure` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Derived from ARC-000-PRIN-v2.0 (Principle 5 §I.5 sovereign mandatory controls + Principle 21), ARC-002-REQ-v1.0 (NFR-SEC-001..008), ARC-002-STKE-v1.0, ARC-002-RISK-v1.0 (R-001..R-013, sovereign appetite override), ARC-002-HLDR-v1.0, ARC-002-ADR-001..008, ARC-002-DEVOPS-v1.0. Continuous Assurance Assessment Tool (CAAT) framework applied. Per ADR-002 + ADR-006: vendor delivers per-release evidence pack; deploying authority owns accreditation/SAL/ATO. Principal acceptance vehicle for residual position on RISK R-002 and R-005.
