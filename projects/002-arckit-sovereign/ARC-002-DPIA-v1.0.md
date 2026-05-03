# Data Protection Impact Assessment (DPIA): ArcKit as a Service (Sovereign Deployment) — Vendor-Narrow Scope

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:dpia`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-DPIA-v1.0 |
| **Document Type** | Data Protection Impact Assessment (UK GDPR Article 35) |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL-SENSITIVE |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Assessment Date** | 2026-05-03 |
| **Next Review Date** | 2027-05-03 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Author** | Vendor DPO (with Lead Architect, Security Lead, Sovereign Delivery Lead) |
| **Reviewed By** | [PENDING — Vendor DPO, Security Lead, Lead Architect] |
| **Approved By** | [PENDING — Service Owner] |
| **Distribution** | Vendor leadership; vendor DPO; pilot deploying authority DPO (subject to NDA); MOD Defence Digital liaison |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation via `/arckit:dpia` for the **vendor-narrow** scope of Project 002 (sovereign deployment). Distinct from `ARC-001-DPIA-v1.0.md` (SaaS) because the **deploying authority is the data controller** for tenant content in sovereign mode and the vendor is a software supplier, not a processor, for that content. | [PENDING] | [PENDING] |

---

## Executive Summary

### Why This DPIA Exists

For the **sovereign deployment** of ArcKit, the deploying authority (e.g., an MOD unit, ALB, or sensitive-site customer) installs, runs, and operates ArcKit entirely within their accredited boundary. The deploying authority is therefore the **data controller** under UK GDPR for any personal data processed by their ArcKit instance, and the vendor (ArcKit as a Service) does not handle, host, or have access to that data.

This means:

- The **deploying-authority DPIA** — covering tenant content, end-user clearance attributes, audit logs, etc. — is conducted by the deploying authority under their own ROPA, on their own accreditation timeline, against their own threat model. The vendor provides DPIA inputs (architecture diagrams, data-flow documentation, SBOMs, signed manifests, threat model) but is not the assessor.
- This **vendor-narrow DPIA** covers only the small surface that the vendor itself processes in connection with sovereign deployments: licence-management data, accreditation evidence drafts, opt-in support-channel records (only when activated and audited by the customer), and opt-in engineering telemetry (default OFF).

The result is a deliberately small DPIA. Most of the "interesting" data-protection content sits with the deploying authority, by design — that is the architectural intent of sovereign mode (Principle 21 of `ARC-000-PRIN-v2.0.md`) and the commercial intent of ADR-001 / ADR-003 / ADR-004 / ADR-005.

### ICO 9-Criteria Screening Outcome (vendor scope)

**0 of 9 criteria met** for vendor-side processing on its own. A DPIA is therefore **not strictly required by Article 35** at the vendor side. However, this DPIA is generated as a deliberate **transparency artefact**:

- It evidences the vendor's processing minimisation posture for accreditators, deploying authority DPOs, and the ICO.
- It demonstrates the boundary clearly so that deploying authorities can scope their own DPIAs without ambiguity.
- It pre-empts later disputes about whether the vendor is a controller, joint controller, or processor in sovereign mode.

### Top Vendor-Side Privacy Risks (Vendor Scope Only)

| ID | Risk | Severity (post-mitigation) |
|----|------|----------------------------|
| DPIA-001 | Engineering telemetry inadvertently captures customer-identifiable content if a customer opts in without proper redaction | LOW |
| DPIA-002 | Accreditation-evidence drafts (SAL templates, threat models) inadvertently include personal data of cleared personnel | LOW |
| DPIA-003 | Audited opt-in remote support session captures personal data of cleared personnel during a debugging session | LOW |

All three are LOW residual after mitigation. None trigger ICO prior consultation.

### Deploying-Authority Responsibilities — Clearly Delineated

**YES.** Section 11 (Data Subject Rights) and Section 4 (Necessity / Proportionality) explicitly delineate which obligations sit with the deploying authority (the controller for tenant content) and which sit with the vendor (the controller for vendor-narrow data only).

---

## Section 1: Need for DPIA — ICO 9-Criteria Screening (Vendor Scope)

### 1.1 Screening (Vendor-Side Processing Only)

| # | ICO Criterion | Met? | Evidence (vendor scope) |
|---|---------------|------|-------------------------|
| 1 | Evaluation or scoring | NO | Vendor performs no scoring or profiling of customer personnel. Licence-management data is org-level. |
| 2 | Automated decision-making with legal/significant effect | NO | None at vendor side. AI generation (when enabled) runs entirely inside the customer boundary (ADR-004). |
| 3 | Systematic monitoring | NO | No vendor-side monitoring of deployments. Telemetry is OPT-IN per customer (ADR-005) and customer-controlled. |
| 4 | Sensitive (special category) data | NO | Vendor processes no special-category data. Clearance attributes never leave the deploying-authority boundary. |
| 5 | Large scale | NO | Vendor processes a small number of contacts per customer organisation. |
| 6 | Matching datasets | NO | No data matching at vendor side. |
| 7 | Vulnerable subjects | NO | Data subjects are professional adults (procurement contacts, cleared personnel where opt-in). Children N/A. |
| 8 | Innovative technology | NO | Vendor-internal processing is conventional (CRM, ticket tracker, signed-bundle infrastructure). |
| 9 | Prevents rights exercise | NO | SARs / erasure / portability for vendor-held data handled via standard vendor procedures. |

**Vendor-side score**: 0 / 9.
**Article 35 obligation at vendor**: NOT triggered.
**Decision**: Conduct DPIA anyway as a transparency / accountability artefact (UK GDPR Article 5(2) accountability principle).

### 1.2 Deploying-Authority-Side Screening (NOT in scope of this document)

The deploying authority performs their own ICO 9-criteria screening as part of **their** DPIA. That screening is likely to score higher (e.g., Criterion 4 if special-category clearance attributes are processed, Criterion 3 if continuous audit logging is in scope, possibly Criterion 8 if AI generation is enabled against a customer-controlled model). That assessment is the deploying authority's responsibility and is **out of scope** for this document.

### 1.3 Vendor's DPIA-Input Pack to the Deploying Authority

The vendor provides — per release — the following inputs to support the deploying authority's own DPIA:

- Architecture diagrams (`ARC-002-HLD-v1.0.md` and successors).
- Data-flow documentation (this document, Section 2.5).
- Threat model (in MOD SbD evidence pack, `/arckit:mod-secure`).
- Signed SBOM (CycloneDX or SPDX) and manifest hashes.
- ADRs covering data-protection-relevant decisions: ADR-001 (no outbound), ADR-003 (cleared-personnel access), ADR-004 (on-prem AI), ADR-005 (customer-controlled telemetry).
- A blank Security Aspects Letter (SAL) template the deploying authority can adapt.
- This vendor-narrow DPIA, demonstrating that no tenant content crosses the boundary to the vendor.

---

## Section 2: Description of Processing (Vendor Scope)

### 2.1 Project Context

The sovereign deployment is delivered as a signed, hashed, air-gap-transferable release bundle (BR-002, FR-001 in `ARC-002-REQ-v1.0.md`). The deploying authority installs, operates, upgrades, backs up, restores, and decommissions ArcKit entirely inside their accredited boundary. There is no vendor-hosted runtime component for sovereign deployments. The vendor's role is software supplier, accreditation-evidence provider, and (only if explicitly contracted and accreditation-compliant) opt-in support partner.

### 2.2 Processing Purposes (Vendor Scope)

| ID | Purpose | Description | Data Subjects |
|----|---------|-------------|---------------|
| PP-1 | Licence and contract management | Track which deploying authority has licensed which release, contract terms, contact persons | Procurement / commercial contacts at deploying authority |
| PP-2 | Accreditation-evidence preparation | Prepare and version vendor evidence packs (MOD SbD, NCSC CAF mapping, SBOM, threat model, SAL template) | None inherently — but draft inputs may incidentally include named cleared personnel |
| PP-3 | Vulnerability disclosure intake | Receive, triage, and acknowledge security vulnerability disclosures from researchers / customers | Researchers / reporters who choose to identify themselves |
| PP-4 | Opt-in audited remote support (when activated by customer) | Where the customer activates and audits a vendor remote support session per FR-013, debug a specific issue | Customer operator(s) on the session; possibly cleared personnel referenced in logs shared during the session |
| PP-5 | Opt-in engineering telemetry (when activated by customer) | Where the customer activates outbound telemetry to the vendor (default OFF, ADR-005), receive aggregate operational metrics for product improvement | None inherent (aggregate); risk that customer opts in without redaction — see DPIA-001 |

PP-1 to PP-3 are **always-on** vendor processing. PP-4 and PP-5 are **opt-in only** and gated by explicit, auditable customer activation.

### 2.3 Nature of Processing

- **Collection**: PP-1 / PP-2 / PP-3 collected through standard vendor business systems (CRM, contract repository, vulnerability-disclosure inbox). PP-4 / PP-5 only when a customer explicitly activates the relevant capability and only via the contracted channel.
- **Storage**: Vendor-side systems hosted in the UK. CRM and ticket store inside the vendor's existing managed-tenancy of an enterprise SaaS (out of scope for this document; covered by vendor's general ROPA). Accreditation-evidence drafts in vendor source control (Git).
- **Use**: Strictly for the purposes named in 2.2.
- **Disclosure**: Disclosure to third parties limited to (a) sub-processors of the vendor's general business stack (CRM provider, etc.) under Article 28 terms, (b) NCSC / customer accreditators where a vulnerability disclosure or accreditation evidence is shared, (c) ICO if a breach reaches Article 33 thresholds.
- **Retention**: Per Section 2.6.
- **Deletion**: At end of retention or on request (Section 11).

### 2.4 Scope of Processing

**Data subjects (vendor scope only)**:

- Procurement / commercial contacts at deploying authorities — typically 2–5 named individuals per deploying authority.
- Vulnerability researchers / customer staff who report vulnerabilities — small number, self-selected.
- Customer operators participating in opt-in remote support sessions — small, audited, customer-led.
- (Theoretical) Cleared personnel named in accreditation-evidence drafts shared by the customer — minimised by drafting convention (use roles, not names, where possible).

**Geographic scope (vendor scope)**: UK only. Vendor business operations and data storage in the UK. No international transfer of vendor-side data — see Section 12.

### 2.5 Data Categories and Data-Flow Boundary

#### 2.5.1 Data the Vendor Processes (Always)

| Category | Field examples | Lawful basis (Art. 6) | Special category? |
|----------|----------------|-----------------------|-------------------|
| Licence-management data (PP-1) | Customer org name, deployment ID, licensed release, LTS line, contract reference | (b) Contract; (f) Legitimate interests for management | No |
| Contact-person data (PP-1) | Name, role, work email, work phone | (b) Contract; (f) Legitimate interests | No |
| Vulnerability-disclosure data (PP-3) | Reporter name (optional), reporter contact (optional), description of vulnerability | (c) Legal obligation (NIS-aligned); (f) Legitimate interests in security | No |
| Accreditation-evidence drafts (PP-2) | Document content; in principle no personal data, occasionally incidental named cleared personnel | (f) Legitimate interests in product accreditation | No (by drafting discipline — see DPIA-002) |

#### 2.5.2 Data the Vendor Processes ONLY If Customer Opts In

| Category | Default | Activation | Lawful basis when active |
|----------|---------|-----------|--------------------------|
| Opt-in audited remote support records (PP-4) | OFF | Customer activates per FR-013, per session | (b) Contract — support clause; customer accredits the channel |
| Opt-in engineering telemetry (PP-5) | OFF (ADR-005) | Customer activates and configures outbound telemetry endpoint to vendor; customer is responsible for redaction at source | (f) Legitimate interests in product improvement, with customer transparency notice obligation |

#### 2.5.3 Data the Vendor NEVER Processes (Boundary Affirmation)

The vendor **does not** process:

- **Tenant artefact content** (architecture documents, requirements, ADRs, principles authored inside the deploying authority's ArcKit instance). This stays inside the deploying authority's accredited boundary (Principle 21; ADR-001 no outbound).
- **End-user identity data** of the deploying authority's user community (clearance attributes, OIDC claims, group memberships). Identity is asserted by the customer's IdP entirely inside the boundary (FR-007).
- **Audit logs** generated by the customer's ArcKit instance. They are written to a customer-controlled SIEM (FR-010).
- **Encryption keys**. Customer-managed via INT-007.
- **AI prompt / response content**. AI generation, when enabled, runs entirely on a customer-controlled approved on-premise model (ADR-004) — no vendor sub-processor data flow.
- **Operational telemetry** unless the customer opts in (ADR-005).
- **Backups**. Customer-controlled (FR-003).

This boundary is enforced architecturally by NFR-SEC-004 (no outbound network calls inside boundary) validated by network-deny CI tests on every release.

### 2.6 Data Sources and Destinations

| Source | Destination | Movement | Frequency |
|--------|-------------|----------|-----------|
| Deploying authority procurement contact | Vendor CRM | Inbound to vendor | At contract or amendment |
| Vendor source control | Customer site (via approved transfer) | Outbound from vendor (signed bundle only) | Per release / patch |
| Vulnerability researcher | Vendor disclosure inbox | Inbound to vendor | Ad-hoc |
| Customer ArcKit deployment | (Stays inside customer boundary) | NEVER crosses to vendor | Continuous (within boundary only) |
| Customer-managed SIEM | (Stays inside customer boundary) | NEVER crosses to vendor | Continuous (within boundary only) |
| Customer-managed AI endpoint | (Stays inside customer boundary) | NEVER crosses to vendor | Per AI invocation (within boundary only) |
| Customer (when opted in) | Vendor telemetry sink | Outbound from customer to vendor | Configurable; default OFF |
| Customer (when opted in) | Vendor support channel | Bidirectional, audited per session | Per session; default OFF |

### 2.7 Retention Periods (Vendor Scope)

| Category | Retention | Trigger for deletion |
|----------|-----------|----------------------|
| Licence-management and contact data (PP-1) | Contract term + 7 years (HMG public-record obligations) | End of retention; or earlier on request once contract obligations satisfied |
| Vulnerability-disclosure records (PP-3) | 7 years from disclosure closure | End of retention |
| Accreditation-evidence drafts (PP-2) | Lifetime of the LTS release line + 24 months | LTS deprecation + 24 months |
| Opt-in remote-support records (PP-4) | 12 months from session close (or per customer instruction if shorter) | End of retention |
| Opt-in engineering telemetry (PP-5) | 13 months rolling window; aggregates retained indefinitely | Rolling deletion |

---

## Section 3: Consultation

### 3.1 Internal Consultation (Vendor Side)

| Stakeholder | Role | Consulted on |
|-------------|------|--------------|
| Vendor DPO | UK GDPR posture | Lawful bases; retention; this document |
| Vendor Security Lead | Supply chain; accreditation evidence | PP-2; DPIA-002 mitigation |
| Vendor Lead Architect | Architecture and boundary | Sections 2.5.3; DPIA-001 mitigation; ADR alignment |
| Vendor Sovereign Delivery Lead | Customer onboarding | PP-4 mitigation; opt-in workflow |
| Vendor Service Owner | Strategic alignment | Whole document — accountable owner |

### 3.2 Consultation Approach for Data Subjects: SURVEYS

**Selection rationale (per worker template default)**: Surveys are the proportionate, scalable, documented mechanism for the small population of vendor-side data subjects (procurement contacts, vulnerability researchers).

| Population | Mechanism | Cadence |
|-----------|-----------|---------|
| Procurement / commercial contacts at deploying authorities | Annual privacy-notice survey covering vendor processing, retention, rights | Annual; on material change |
| Vulnerability researchers using the disclosure programme | Privacy notice at point of submission; opt-in survey on programme-experience | At point of submission; quarterly programme review |
| Customer operators participating in opt-in remote support | Pre-session privacy notice with explicit acknowledgement; post-session survey | Per session |

**Cleared personnel of the deploying authority are NOT directly consulted by the vendor** because the vendor is not the controller for their data; their consultation rights are exercised through the deploying authority's own consultation processes (e.g., the deploying authority's privacy notices, internal staff communications, and DPO).

### 3.3 External Consultation (Deploying Authority and Cross-Government)

| Stakeholder | Consulted on |
|-------------|--------------|
| Pilot deploying authority DPO | Vendor-narrow DPIA and DPIA-input pack — do they fit your own DPIA scope cleanly? |
| Pilot deploying authority Accreditator | Section 2.5.3 boundary affirmations — match what you expect to see in the SAL? |
| MOD Defence Digital liaison | Cross-MOD data-protection coherence |
| ICO (no formal consultation; Section 7) | Not consulted as no residual high risk |

---

## Section 4: Necessity and Proportionality

### 4.1 Lawful Basis (Vendor Scope)

| Purpose | Article 6 lawful basis | Article 9 condition |
|---------|------------------------|---------------------|
| PP-1 Licence and contract management | (b) Performance of contract; (f) Legitimate interests for ongoing administration | N/A — no special-category data |
| PP-2 Accreditation-evidence preparation | (f) Legitimate interests — vendor's interest in producing accreditable software | N/A — drafting discipline avoids special-category data |
| PP-3 Vulnerability-disclosure intake | (c) Legal obligation; (f) Legitimate interests in product security | N/A |
| PP-4 Opt-in remote support | (b) Performance of contract | N/A |
| PP-5 Opt-in engineering telemetry | (f) Legitimate interests in product improvement; transparency obligation | N/A |

### 4.2 Necessity Test

Each purpose passes the necessity test because:

- PP-1 is contractually unavoidable (the vendor must know who has licensed what).
- PP-2 is required to support customer accreditation (BR-004).
- PP-3 is good-practice and aligned with NCSC vulnerability-disclosure guidance and ISO 29147.
- PP-4 is only invoked when the customer judges it necessary to debug an issue.
- PP-5 is the minimum viable mechanism for product improvement, only operative when customer opts in.

### 4.3 Proportionality Test

- Personal-data fields collected are limited to what is needed for each purpose (licence contacts only need name / role / work email).
- Special-category data is structurally excluded by architecture (Section 2.5.3 boundary affirmations).
- Children's data N/A — all vendor-side data subjects are professional adults.
- Vendor processing is **smaller in scope than the SaaS DPIA equivalent** by design — the sovereign architecture deliberately moves the bulk of personal-data processing to the deploying authority where it can be governed under their own controls.

### 4.4 Data Minimisation Posture

- ADR-001 (no outbound) — most powerful minimisation control: tenant content cannot reach the vendor by architecture.
- ADR-005 (customer-controlled telemetry) — operational telemetry default OFF; customer must opt in.
- ADR-003 (cleared-personnel access) — clearance attributes asserted at the customer IdP, never travel to the vendor.
- ADR-004 (on-premise AI) — AI prompts and responses do not generate vendor sub-processor data flow.
- Drafting discipline for accreditation evidence — use roles not names where feasible (DPIA-002 mitigation).

These ADRs together implement Privacy by Design (UK GDPR Article 25) at the architectural level.

### 4.5 Map to Architecture Principles

| Principle | Sovereign DPIA reflection |
|-----------|---------------------------|
| Principle 4 — Open standards / portability | Customer can export and leave at any time; no vendor data hostage |
| Principle 5 — Security by design | NFR-SEC-001..008 in the requirements; this DPIA aligns |
| Principle 7 — Sovereign deployments residency / sovereignty controlled by deploying authority | Anchors the boundary in Section 2.5.3 |
| Principle 21 — Sovereign / air-gapped deployment | Anchors the entire vendor-narrow scope of this DPIA |

---

## Section 5: Risk Assessment

### 5.1 Scope and Methodology

Risks below are scored against impact on **individuals' rights and freedoms** (UK GDPR Article 35(1)), not organisational risk. Scoring uses the ICO matrix:

- Likelihood: Remote / Possible / Probable.
- Severity: Minimal / Significant / Severe.
- Overall: Low (green) / Medium (amber) / High (red).

### 5.2 Risk Register (DPIA Scope)

#### DPIA-001: Inadvertent capture of customer-identifiable content in opt-in engineering telemetry

- **Description**: A customer activates opt-in telemetry (PP-5) without configuring redaction at source. Operational metrics or stack traces inadvertently include user IDs, project names containing personal data, or freeform text containing names.
- **Affected data subjects**: Cleared personnel and architects in the deploying authority.
- **Source**: PP-5; ADR-005.
- **Inherent likelihood / severity**: Possible / Significant. Inherent overall: MEDIUM.
- **Mitigations**:
  - **Technical (M-1.1)**: Telemetry schema documented and restricted to numeric / categorical fields only by default; freeform text fields not in default schema.
  - **Technical (M-1.2)**: Redaction filter at customer egress (sample regex / allow-list shipped with bundle).
  - **Organisational (M-1.3)**: Customer activation workflow requires named approval and acknowledgement of the redaction obligation.
  - **Procedural (M-1.4)**: Quarterly vendor-side telemetry sample audit by DPO; any unexpected personal data triggers customer notification and source-side fix.
- **Residual likelihood / severity**: Remote / Minimal. Residual overall: **LOW**.
- **Risk owner**: Vendor DPO with Lead Architect.
- **Linked register**: Add as DPIA-001 in `ARC-002-RISK-v1.0.md`.

#### DPIA-002: Accreditation-evidence drafts inadvertently include personal data of cleared personnel

- **Description**: Threat models, SAL drafts, or design notes shared with the vendor for accreditation evidence (PP-2) include the names of specific cleared personnel (e.g., "operator X performed install").
- **Affected data subjects**: Cleared personnel of the deploying authority.
- **Source**: PP-2.
- **Inherent likelihood / severity**: Possible / Significant. Inherent overall: MEDIUM.
- **Mitigations**:
  - **Procedural (M-2.1)**: Drafting convention — use roles ("Operator A", "Accreditator") not names. Codified in evidence-pack template.
  - **Procedural (M-2.2)**: Vendor pre-publication review by DPO scans drafts for inadvertent personal data.
  - **Organisational (M-2.3)**: Customer DPO informed of the drafting convention so the customer can mirror it on their side.
- **Residual likelihood / severity**: Remote / Minimal. Residual overall: **LOW**.
- **Risk owner**: Vendor Security Lead with DPO.
- **Linked register**: Add as DPIA-002 in `ARC-002-RISK-v1.0.md`.

#### DPIA-003: Opt-in audited remote-support session captures personal data during debugging

- **Description**: During an opt-in audited support session (PP-4, FR-013), the customer shares a log excerpt or screenshot containing personal data of cleared personnel referenced in audit events.
- **Affected data subjects**: Cleared personnel of the deploying authority.
- **Source**: PP-4.
- **Inherent likelihood / severity**: Possible / Significant. Inherent overall: MEDIUM.
- **Mitigations**:
  - **Technical (M-3.1)**: Vendor-side support workspace ephemeral — wiped at end of session unless customer requests retention.
  - **Procedural (M-3.2)**: Pre-session privacy notice acknowledged by customer operator; redaction guidance shared.
  - **Procedural (M-3.3)**: All session activity logged to customer SIEM by design (FR-013 audit requirement); vendor support channel does not retain copies beyond minimum needed for ticket closure.
  - **Organisational (M-3.4)**: 12-month retention cap on session records (Section 2.7).
- **Residual likelihood / severity**: Remote / Minimal. Residual overall: **LOW**.
- **Risk owner**: Sovereign Delivery Lead with DPO.
- **Linked register**: Add as DPIA-003 in `ARC-002-RISK-v1.0.md`.

#### DPIA-004: Vulnerability-disclosure reporter identification leaks beyond intake

- **Description**: A vulnerability reporter (PP-3) provides their name in confidence; that identification is later shared inappropriately during cross-vendor coordination.
- **Affected data subjects**: External researchers; possibly customer staff.
- **Inherent likelihood / severity**: Remote / Significant. Inherent overall: LOW.
- **Mitigations**:
  - **Procedural (M-4.1)**: Vendor disclosure-programme privacy notice at point of submission; reporter chooses whether to be named in any public advisory.
  - **Procedural (M-4.2)**: Coordinated-disclosure workflow defaults to anonymised attribution unless the reporter explicitly requests credit.
- **Residual likelihood / severity**: Remote / Minimal. Residual overall: **LOW**.
- **Risk owner**: Vendor Security Lead.

#### DPIA-005: Boundary mis-configuration causes outbound call from sovereign deployment

- **Description**: A bug or mis-configuration causes the customer's ArcKit instance to attempt an outbound call carrying tenant content to a vendor or third-party endpoint, breaching the boundary.
- **Affected data subjects**: All deploying-authority users.
- **Inherent likelihood / severity**: Remote / Severe. Inherent overall: MEDIUM.
- **Mitigations**:
  - **Technical (M-5.1)**: NFR-SEC-004 network-deny CI test: zero outbound connections during install / run / upgrade / backup / restore / decommission. Pass required per release.
  - **Technical (M-5.2)**: Default configuration profile in sovereign mode sets all external endpoints to placeholder customer-controlled values; system refuses to start until they are filled (FR-005).
  - **Organisational (M-5.3)**: Bundle-issue gate requires Lead Architect sign-off (RACI, STKE Section governance).
  - **Procedural (M-5.4)**: Incident-response runbook defines coordinated customer notification if an outbound call is detected post-deployment; vendor coordinates with customer accreditator and ICO if Article 33 thresholds are reached.
- **Residual likelihood / severity**: Remote / Significant. Residual overall: **LOW**.
- **Risk owner**: Lead Architect with Security Lead.
- **Linked register**: Cross-references existing risk SR-2 / SR-8 in `ARC-002-RISK-v1.0.md`.

### 5.3 Risk Summary

| Severity | Inherent count | Residual count |
|----------|----------------|----------------|
| HIGH (red) | 0 | 0 |
| MEDIUM (amber) | 4 | 0 |
| LOW (green) | 1 | 5 |
| **Total** | **5** | **5** |

No residual high risks. ICO prior consultation **NOT** required.

---

## Section 6: Mitigations

Consolidated from Section 5. Cross-referenced to existing security controls (HLD, REQ NFR-SEC) where applicable.

| ID | Control | Type | Linked requirement / ADR |
|----|---------|------|--------------------------|
| M-1.1 | Telemetry schema restricted to numeric/categorical fields | Technical | ADR-005; FR-005 |
| M-1.2 | Redaction filter at customer egress | Technical | ADR-005 |
| M-1.3 | Customer activation workflow with named approval | Organisational | ADR-005 |
| M-1.4 | Quarterly DPO sample audit | Procedural | This DPIA |
| M-2.1 | Drafting convention (roles, not names) | Procedural | BR-004 evidence pack |
| M-2.2 | DPO pre-publication review of drafts | Procedural | This DPIA |
| M-2.3 | Customer DPO awareness | Organisational | This DPIA Section 3 |
| M-3.1 | Ephemeral support workspace | Technical | FR-013 |
| M-3.2 | Pre-session privacy notice | Procedural | FR-013 |
| M-3.3 | Session activity to customer SIEM | Technical | FR-013, FR-010 |
| M-3.4 | 12-month retention cap | Procedural | Section 2.7 |
| M-4.1 | Disclosure-programme privacy notice | Procedural | NFR-SEC-008 |
| M-4.2 | Anonymised attribution default | Procedural | NFR-SEC-008 |
| M-5.1 | Network-deny CI test, 100% per release | Technical | NFR-SEC-004; BR-002 |
| M-5.2 | Default config refuses to start without endpoints | Technical | FR-005 |
| M-5.3 | Bundle-issue gate (Lead Architect sign-off) | Organisational | STKE RACI |
| M-5.4 | Boundary-breach IR runbook | Procedural | FR-011 |

---

## Section 7: ICO Prior Consultation

**Required: NO.**

No residual risk is rated HIGH after mitigation (Section 5.3). Article 36 prior consultation with the ICO is therefore not triggered for the vendor-narrow scope.

The deploying authority will make their own ICO-consultation determination as part of their own DPIA, using the inputs from this document.

---

## Section 8: Sign-Off and Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Vendor DPO | [PENDING] | _________ | [PENDING] |
| Vendor Security Lead | [PENDING] | _________ | [PENDING] |
| Vendor Lead Architect | [PENDING] | _________ | [PENDING] |
| Vendor Sovereign Delivery Lead | [PENDING] | _________ | [PENDING] |
| Service Owner / SRO (vendor) | Mark Craddock | _________ | [PENDING] |
| Pilot deploying authority DPO (acknowledgement, not approval) | [PENDING] | _________ | [PENDING] |

---

## Section 9: Review and Monitoring

### 9.1 Review Triggers

- Scheduled annual review (next: 2027-05-03).
- Material change to vendor processing (new sub-processor; new opt-in capability).
- Activation of opt-in remote support or telemetry by a new customer (per-customer micro-DPIA addendum if processing scope changes).
- Material change to architecture that could affect the boundary (e.g., new integration default-on).
- Data breach reaching Article 33 thresholds.
- ICO guidance update affecting any of the lawful bases relied on.
- Any LTS deprecation that changes accreditation-evidence retention.

### 9.2 Monitoring KPIs

| KPI | Target | Frequency | Owner |
|-----|--------|-----------|-------|
| Quarterly telemetry sample audit clean | 100% (no inadvertent personal data) | Quarterly | DPO |
| Network-deny CI test pass | 100% per release | Per release | Lead Architect |
| Pre-publication evidence-pack review pass | 100% | Per release | DPO |
| Vendor-side UK GDPR breaches | 0 | Continuous | DPO |
| ICO complaints citing vendor scope | 0 | Continuous | DPO |

---

## Section 10: Traceability

### 10.1 Source Artefacts

- `projects/000-global/ARC-000-PRIN-v2.0.md` — Architecture principles (esp. Principle 7, Principle 21).
- `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md` — Requirements (esp. BR-002, BR-003, BR-004, FR-001, FR-004, FR-005, FR-007, FR-010, FR-013, NFR-SEC-001..008, NFR-C-002).
- `projects/002-arckit-sovereign/ARC-002-STKE-v1.0.md` — Stakeholder analysis (esp. SD-1, SD-2, SD-10, SD-14, SD-16; G-4, G-8; SR-1, SR-3).
- `projects/002-arckit-sovereign/ARC-002-RISK-v1.0.md` — Project risk register.
- `projects/002-arckit-sovereign/decisions/ARC-002-ADR-001-v1.0.md` — No outbound — no third-party exfil risk.
- `projects/002-arckit-sovereign/decisions/ARC-002-ADR-003-v1.0.md` — Cleared-personnel access — admin auditability.
- `projects/002-arckit-sovereign/decisions/ARC-002-ADR-004-v1.0.md` — On-prem AI — no AI sub-processor data flow.
- `projects/002-arckit-sovereign/decisions/ARC-002-ADR-005-v1.0.md` — Customer-controlled telemetry — no vendor logging by default.

### 10.2 DPIA Risk IDs and Cross-Links

| DPIA risk | Project risk register link | Architectural mitigation |
|-----------|---------------------------|--------------------------|
| DPIA-001 | New (to be added) | ADR-005; FR-005 |
| DPIA-002 | New (to be added) | BR-004 evidence pack discipline |
| DPIA-003 | New (to be added) | FR-013; FR-010 |
| DPIA-004 | New (to be added) | NFR-SEC-008 |
| DPIA-005 | Cross-references SR-2, SR-8 | NFR-SEC-004; BR-002; FR-005 |

---

## Section 11: Data Subject Rights

### 11.1 Vendor-Held Data (Vendor Is the Controller)

For data the vendor holds about procurement contacts, vulnerability researchers, opt-in support participants:

| Right | Implementation (vendor scope) |
|-------|-------------------------------|
| Subject Access Request | Vendor SAR procedure; published in vendor privacy notice. Response within UK GDPR statutory period. |
| Rectification | Direct request to vendor DPO; updated in CRM / ticket store. |
| Erasure | On request, subject to retention obligations (Section 2.7); contractual / legal retentions noted. |
| Portability | Limited applicability (most processing is contract / legal). Where (a) lawful basis applies, structured export provided. |
| Objection | Rights to object to PP-2 / PP-3 / PP-5 considered case-by-case. |
| Restriction | Available; flagged in CRM. |
| Automated decision-making rights (Art. 22) | Not applicable — vendor performs no automated decision-making on these data subjects. |

### 11.2 Tenant-Content Data (Deploying Authority Is the Controller)

For data the deploying authority holds about its end users (cleared personnel, architects), tenant artefact content, audit logs:

| Right | Implementation (deploying-authority responsibility) |
|-------|-----------------------------------------------------|
| Subject Access Request | Handled by deploying authority via their existing SAR process; ArcKit functionality assists (e.g., audit-log retrieval for the data subject's actions). |
| Rectification | Deploying authority through their admin functions. |
| Erasure | Deploying authority via FR-009 export and project / artefact deletion. |
| Portability | Deploying authority via FR-009 export in open formats. |
| Objection | Deploying authority. |
| Restriction | Deploying authority via project / role configuration. |
| Automated decision-making | Deploying authority — note: AI generation in sovereign mode is human-in-the-loop architecting; not Article 22 decisions. |

The vendor's role on tenant-content rights is **supplier**, not **controller** — the architecture provides the rights mechanisms (FR-009 export, FR-010 audit, configurable retention), and the deploying authority operates them.

This delineation is **explicit and unambiguous**.

---

## Section 12: International Transfers

### 12.1 Vendor Scope

**No international transfers occur for vendor-side data.** Vendor business operations and data storage are UK-based. No Article 46 transfer mechanism is required at the vendor side.

If the vendor's general business stack (e.g., CRM provider) involves transfers covered by adequacy decisions or SCCs, those are covered under the vendor's general ROPA — out of scope for this document — and they do not include sovereign-customer tenant content (which never leaves the customer boundary).

### 12.2 Sovereign Deployment Boundary

**No transfers occur for tenant content.** ADR-001 (no outbound) ensures tenant content does not leave the deploying authority's accredited boundary. Therefore Article 46 / Schrems-II considerations do not apply for tenant content under vendor processing.

The deploying authority is responsible for any internal transfers within their own boundary (e.g., between sites), under their own ROPA.

---

## Section 13: Children's Data

**Not applicable.** All vendor-side data subjects are professional adults (procurement contacts, vulnerability researchers, customer operators, cleared personnel). No children's data is processed in either the vendor scope or the broader sovereign architecture (the deploying authority's user community is by definition cleared adult personnel).

---

## Section 14: AI / Algorithmic Processing

**Not applicable at vendor side.** Vendor performs no AI / ML processing of customer data.

In the broader sovereign architecture, AI-assisted generation (FR-004) — where the deploying authority enables it — runs entirely against a customer-controlled approved on-premise model (ADR-004). No prompts, completions, or model interactions reach the vendor. There is no vendor sub-processor data flow for AI in sovereign mode.

If the deploying authority's accreditation requires an Algorithmic Transparency Recording Standard (ATRS) record for the on-premise model, that ATRS is the deploying authority's responsibility (under their ROPA / model card), not the vendor's.

This contrasts with the SaaS DPIA (`ARC-001-DPIA-v1.0.md`) where AI processing is in scope.

---

## Section 15: Summary and Action Plan

### 15.1 Summary

| Field | Value |
|-------|-------|
| Vendor-side ICO 9-criteria score | 0 / 9 |
| Vendor-side DPIA legally required? | No (transparency artefact) |
| Total DPIA risks | 5 |
| Residual high risks | 0 |
| Residual medium risks | 0 |
| Residual low risks | 5 |
| ICO prior consultation required | No |
| International transfers (vendor) | None |
| Special category data (vendor) | None |
| Children's data | N/A |
| Deploying-authority responsibilities clearly delineated | YES (Sections 4, 11) |

### 15.2 Action Plan

| ID | Action | Owner | Due |
|----|--------|-------|-----|
| A-1 | Add DPIA-001..005 to `ARC-002-RISK-v1.0.md` (Data Protection category) | Lead Architect | 2026-06-15 |
| A-2 | Codify telemetry schema and redaction filter (M-1.1, M-1.2) | Lead Architect | Before alpha |
| A-3 | Quarterly telemetry sample audit procedure | DPO | 2026-09-30 |
| A-4 | Drafting convention (roles, not names) added to evidence-pack template (M-2.1) | Security Lead | 2026-06-30 |
| A-5 | DPO pre-publication review process for evidence drafts (M-2.2) | DPO | 2026-06-30 |
| A-6 | Pre-session privacy notice and ephemeral workspace for opt-in support (M-3.1, M-3.2) | Sovereign Delivery Lead | Before first opt-in activation |
| A-7 | Network-deny CI test gate enforced on every release (M-5.1) | Lead Architect | Continuous |
| A-8 | Vendor public privacy notice updated to reflect sovereign-narrow scope | DPO | 2026-07-31 |
| A-9 | Pilot deploying authority DPO acknowledgement of DPIA-input pack | Sovereign Delivery Lead | At pilot kick-off |
| A-10 | 12-month review (next assessment date) | DPO | 2027-05-03 |

### 15.3 Validation Result

**PASS.** This DPIA:

- Performs ICO 9-criteria screening (vendor scope: 0/9; transparency-DPIA proceeds anyway).
- Identifies all vendor-narrow personal-data categories and lawful bases.
- States the data-flow boundary explicitly (Section 2.5.3) and links it to ADR-001 / ADR-003 / ADR-004 / ADR-005.
- Distinguishes vendor responsibilities from deploying-authority responsibilities (Sections 4, 11).
- Risk-assesses each vendor-side processing purpose with mitigations to LOW residual.
- Concludes ICO prior consultation NOT required.
- Records traceability to REQ, STKE, principles, and ADRs.
- Establishes 12-month review and monitoring KPIs.
- Classified OFFICIAL-SENSITIVE.

---

## External References

> No external policy documents were placed in `projects/002-arckit-sovereign/external/` at the time of generation. UK GDPR / DPA 2018 / ICO DPIA guidance referenced are public-domain.

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

## References

- UK GDPR Article 35 — DPIAs: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/data-protection-impact-assessments-dpias/
- UK GDPR Article 25 — Data Protection by Design and by Default
- UK GDPR Article 28 — Processor obligations
- UK GDPR Article 36 — ICO prior consultation
- DPA 2018
- ICO DPIA Screening Checklist
- Government Security Classifications Policy
- MOD Secure by Design / JSP 440 / JSP 604
- NCSC Cyber Assessment Framework

---

**Generated by**: ArcKit `/arckit:dpia` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Vendor-narrow DPIA distinct from `ARC-001-DPIA-v1.0.md` (SaaS). Anchored on Principle 21, ADR-001 / ADR-003 / ADR-004 / ADR-005, and the deploying-authority-as-controller posture for sovereign deployments.
