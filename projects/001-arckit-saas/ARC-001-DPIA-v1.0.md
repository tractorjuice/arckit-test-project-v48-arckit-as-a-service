# Data Protection Impact Assessment (DPIA): ArcKit as a Service (Managed SaaS)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:dpia`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-DPIA-v1.0 |
| **Document Type** | Data Protection Impact Assessment (UK GDPR Article 35) |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL-SENSITIVE |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Assessment Date** | 2026-05-03 |
| **Next Review Date** | 2027-05-03 (annual; or sooner on material change) |
| **Owner** | [PENDING] Vendor Data Protection Officer |
| **Reviewed By** | [PENDING] Service Owner / SIRO-equivalent, Security Lead, Lead Architect |
| **Approved By** | [PENDING] Service Owner (data controller for vendor processing) |
| **Distribution** | Project Team, Architecture Team, ICO (on request), CCS liaison |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:dpia` command. Pre-GA assessment of the managed SaaS personal-data processing — tenant admin/user identities, authentication metadata, audit-log records, billing records, aggregated usage telemetry, and AI sub-processor (ADR-004) Article 46 transfer in scope. Sourced from REQ, STKE, RISK, TCOP, SBD, ADR-001/003/004/005, and PRIN. **Note**: data model artefact (`ARC-001-DM-v1.0.md`) is pending; this DPIA derives the personal-data inventory directly from REQ + ADR-001/003/004/005 + the user-supplied scope. Refresh on data-model issuance. | [PENDING] | [PENDING] |

## Document Purpose

A DPIA conducted under UK GDPR Article 35 and the ICO Code of Practice for the managed SaaS of ArcKit as a Service (Project 001), prior to GA. The sovereign deployment route (Project 002) has its own DPIA on a per-deployment basis with the deploying authority as data controller.

This DPIA is the controlling artefact for:

- ICO 9-criteria screening for the managed SaaS.
- Lawful-basis register and ROPA scaffolding.
- Article 46 transfer assessment for the AI sub-processor (`ARC-001-ADR-004-v1.0.md`).
- Privacy-risk identification, mitigation, and residual-risk acceptance — feeding back to `ARC-001-RISK-v1.0.md` R-010 (AI Playbook scope drift) and R-011 (UK GDPR breach via AI sub-processor).
- Data-subject-rights mechanism inventory and gap list.

---

## 1. Need for a DPIA: ICO 9-Criteria Screening

### 1.1 Screening Result

**Screening Score**: 1/9 criteria explicitly met + 1/9 partially → **DPIA RECOMMENDED** (and produced, given the AI sub-processor and Article 46 international-transfer dimension that warrant a documented assessment).

| # | ICO Criterion | Result | Justification |
|---|---------------|--------|---------------|
| 1 | Evaluation or scoring | ❌ No | AI is drafting-only (FR-004); no profiling, no scoring of data subjects, no Article 22 solely-automated decisions of legal / significant effect (RISK R-010 control). |
| 2 | Automated decision-making with legal / significant effect | ❌ No | Human-in-the-loop architecture — every AI-generated artefact is reviewed and edited by a human author before any external use. AI does not make decisions affecting tenant users. |
| 3 | Systematic monitoring | ⚠️ Partial | Audit logging captures admin / user actions within their own tenancy (security monitoring obligation). Not surveillance; not third-party-facing; access scoped to the tenant's own admins. |
| 4 | Sensitive (special category) data | ❌ No | No Article 9 special-category data (health, racial / ethnic origin, political opinion, religion, trade-union membership, genetic, biometric, sex life / orientation). No Article 10 criminal-conviction data. Tenant administrator / user identity is general-personal-data only. |
| 5 | Large scale | ❌ No | Target population: ~200 SME tenants × ~5 users + ~10 large-enterprise tenants × ~50 users = ~1500–2000 data subjects at 12 months post-GA (per `ARC-001-REQ-v1.0.md` BR-008 and BR-001). Below ICO "large scale" threshold; UK / EEA-only data subjects. |
| 6 | Matching of datasets | ❌ No | Companies House data (used for SME-eligibility verification, FR-001) is *organisation* data, not personal data; admin contact email is provided directly by the registrant, not derived. No cross-tenant matching. |
| 7 | Vulnerable data subjects | ❌ No | Data subjects are professional adults using the service in a work context (DDaT architects, SME architects, founders, vendor operators). No children, no patients, no asylum-seeker / refugee / domestic-abuse contexts. |
| 8 | Innovative technology | ✅ Yes | AI / LLM is used for artefact-generation assistance (FR-004, ADR-004). Although drafting-only, AI is "innovative technology" by ICO definition and warrants assessment. |
| 9 | Prevents rights exercise | ❌ No | All UK GDPR rights are mechanically supported: SAR via tenant export (BR-007), erasure via tenancy termination + verifiable destruction certificate (BR-007 + Principle 7), portability via open-format export (Principle 4 + ADR-007), rectification via in-product editing, objection / restriction via DPO contact + DPA. |

**Decision**: Although the formal ICO threshold is **2/9**, this DPIA proceeds because (a) criterion 8 (AI) is met, (b) the architecture relies on an Article 46 international transfer to the AI sub-processor in some configurations (ADR-004), and (c) the service has multi-tenant SaaS thesis where cross-tenant data leakage risk (R-008) has Catastrophic impact even if the inherent likelihood is reduced to Rare. ICO guidance recommends a DPIA whenever there is "any possibility of high risk" — defence-of-position is the right move.

### 1.2 Why This DPIA Now

- Pre-GA Alpha-stage; no live processing yet — DPIA produced *before* processing begins, in line with UK GDPR Article 35(10).
- Identified as critical pre-GA blocker by `ARC-001-TCOP-v1.0.md` (Point 7) and `ARC-001-SBD-v1.0.md` (§3 + §9.1 #2).
- Enables RISK R-008/R-010/R-011 acceptance position (`ARC-001-SBD-v1.0.md` §10).

---

## 2. Description of the Processing

### 2.1 Project Context

The managed SaaS provides architecture-governance tooling — principles, requirements, ADRs, diagrams, traceability, compliance assessments, AI-assisted artefact generation — to UK SMEs supplying or seeking to supply UK Government, plus large-enterprise tenants whose subscriptions cross-subsidise the SME tier (Principle 1). Hosted in the UK by default (Principle 7).

### 2.2 Processing Purposes

| ID | Purpose | Source | Justification |
|----|---------|--------|---------------|
| PUR-1 | Provision and administer tenant accounts | FR-001, BR-001/003 | Necessary to provide the contracted service |
| PUR-2 | Authenticate and authorise tenant users | ADR-003 | Necessary to provide contracted service securely |
| PUR-3 | Maintain audit trail of administrative and content actions | ADR-005, NFR-SEC-004 | Legal / regulatory obligation (UK GDPR accountability, NCSC CAF) + legitimate-interest in security and abuse detection |
| PUR-4 | Bill the tenant on the agreed tier | BR-002, BR-005 | Necessary to provide contracted service |
| PUR-5 | Operate, monitor, and improve the service | Principle 6, ADR-005 | Legitimate interest in service quality; aggregated, not user-identifying |
| PUR-6 | Generate AI-assisted draft artefacts on user request | FR-004, ADR-004 | User-initiated, contractual feature of the service |
| PUR-7 | Verify SME eligibility for the SME tier | FR-001, BR-003 | Necessary to provide contracted (SME-tiered) service; uses Companies House (organisation, not personal, data) plus user-attested contact |

### 2.3 Nature of Processing

- **Collection**: at sign-up (admin contact details + organisation), at user invitation (user name + work email + role), continuously during use (auth events, action audit, usage metrics), at billing event (payment processor reference).
- **Storage**: encrypted at rest (NFR-SEC-001); UK region by default (Principle 7).
- **Use**: authentication, authorisation, audit-trail integrity, usage-tier billing, AI-draft generation (only on user request), aggregated service-improvement analytics.
- **Disclosure**:
  - To the tenant's own administrators — by design; that is the service.
  - To AI sub-processor (during user-initiated generation) — only the prompt content + contextual artefact data the user submits; no identity tokens passed in the prompt.
  - To payment processor — billing-contact details and tenant-organisation reference only.
  - To Companies House — outbound queries only; no personal data sent.
  - To the ICO — on request (regulator).
- **Deletion**: on tenancy termination + grace period (default 30 days, configurable up to 90 per BR-007); verifiable destruction certificate provided.

### 2.4 Scope of Processing

- **Data subjects**: tenant administrators, tenant invited users (typically architects / engineers / bid leads), vendor operators (SREs, support).
- **Geographic scope**: data subjects predominantly UK; system data residency UK (Principle 7); AI sub-processor processing may be non-UK subject to Article 46 mechanism (see §12).
- **Volume**: target ~1500–2000 data subjects at GA + 12 months (per BR-008 onboarding target).
- **Duration**: ongoing, while tenancy active; 30–90-day grace period after tenancy ends; security audit logs retained 12 months minimum (Principle 6).

### 2.5 Personal Data Inventory

> Pending generation of `ARC-001-DM-v1.0.md` (data model). Inventory below derived from REQ, ADR-001, ADR-003, ADR-005, and the user-supplied DPIA scope.

| Entity | Personal Data Fields | Special Category? | Retention | Lawful Basis | Source ADR / Req |
|--------|----------------------|-------------------|-----------|--------------|--------------------|
| **Tenant administrator** | Full name, work email, organisation, role title, optional photo | No | Lifetime of tenancy + 30–90-day grace period | Contract (Art. 6(1)(b)) | FR-001, BR-001 |
| **Tenant user** | Full name, work email, role, optional photo, last-login timestamp | No | Lifetime of tenancy + grace period | Contract (Art. 6(1)(b)) | FR-002, ADR-003 |
| **Authentication metadata** | OIDC / SAML claims (subject ID, audience, scope), MFA state, session tokens (short-lived), device fingerprint (rough — IP + user-agent) | No | Session: short-lived; security audit: 12 months minimum | Legitimate interest (Art. 6(1)(f)) for security; Contract for service auth | ADR-003 |
| **Audit log records** | User ID + tenant ID + action + timestamp + (optionally) before/after state of artefact metadata | No | 12 months minimum (Principle 6); longer if regulated | Legal obligation (Art. 6(1)(c)) for accountability + legitimate interest (Art. 6(1)(f)) for security / abuse detection | ADR-005, NFR-SEC-004 |
| **Billing records** | Organisation legal name, billing contact name + email + role, payment-processor reference (e.g., Stripe customer ID), invoice history | No (no card numbers — held by payment processor only) | 7 years (HMRC tax record retention); after that, anonymised aggregate only | Legal obligation (Art. 6(1)(c)) — tax and accounting; Contract (Art. 6(1)(b)) | BR-002, BR-005, INT-002 |
| **Usage telemetry** | Per-tenant aggregated metrics; per-user anonymised activity counters used to detect abuse / abandonment patterns | No | 13 months for trend analysis; longer if anonymised | Legitimate interest (Art. 6(1)(f)) | Principle 6, ADR-005 |
| **AI generation context (transient)** | Prompt content (artefact draft input — user-authored, may incidentally include user names, work emails, project metadata); tenant ID context (technical correlation only) | No (any incidental personal data is artefact metadata, not data-subject-of-processing data) | Transient — not retained by sub-processor under no-training-on-customer-data assurance; held in audit trail of generation events for 90 days | Legitimate interest (Art. 6(1)(f)) for service feature; tenant has full visibility of what was sent | FR-004, ADR-004 |
| **Companies House data (verification check)** | Public organisation data: company number, name, status, officers (organisation data — not personal data of *our* data subjects) | No | Only the verification *outcome* retained (eligible / not / pending) for audit purposes; raw Companies House response not stored beyond 24 hours | Legitimate interest (Art. 6(1)(f)) | FR-001 |

**No special-category data (Article 9)** is processed by the managed SaaS.
**No criminal-conviction data (Article 10)** is processed.
**No children's data (under 13 / under 18 depending on context)** is processed — service is B2B, professional adults only.

### 2.6 Data Sources

| Source | What | When |
|--------|------|------|
| Self-attestation by tenant administrator | Org details, primary contact, admin user identity | Sign-up |
| Self-attestation by tenant user | Name, role | On invitation |
| Tenant IdP | OIDC / SAML claims | At each authenticated session |
| Companies House API (organisation data) | Eligibility verification — outcome retained, raw not retained | Sign-up + annual re-verification |
| Payment processor | Billing reference | At each billing event |

### 2.7 Data Recipients (Processors and Sub-Processors)

| Recipient | Role | Data Provided | Safeguard |
|-----------|------|---------------|-----------|
| Vendor (controller for vendor-internal operational data; processor for tenant content) | Controller / Processor | All categories above per role | This DPIA + ROPA + Principle 5 controls |
| Cloud provider (hosting + storage) | Sub-processor | All categories at rest + in transit (encrypted) | DPA, ISO 27001, NCSC Cloud Security Principles |
| AI / LLM provider (ADR-004) | Sub-processor | Generation prompt + context only — no identity tokens | DPA + no-training-on-customer-data + Article 46 mechanism (Standard Contractual Clauses) where non-UK |
| Payment processor (INT-002) | Independent controller for card data; processor for billing-contact data | Billing-contact details + tenant organisation reference (no card data passes through vendor) | DPA, PCI DSS Level 1 |
| Companies House | Independent controller (public-register source) | Outbound queries only — vendor sends company number; no personal data outbound | Public-register status |
| SIEM (INT-004 — tenant SIEM forwarding, post-GA) | Tenant data controller (their own SIEM) | Selected security events only, on tenant opt-in | Tenant-side responsibility |

**Sub-processor list** is published pre-GA and refreshed annually + on change with 30-day tenant notice (Principle 7; RISK R-011 control).

### 2.8 Retention Periods

| Category | Retention | Trigger | Verification |
|----------|-----------|---------|--------------|
| Tenant content (incl. user identity within the tenancy) | Lifetime of tenancy + 30–90-day grace | Tenancy termination | Verifiable destruction certificate (BR-007) |
| Authentication metadata (session) | Short-lived (token TTL) | Session end | Token expiry + revocation list |
| Security audit log | 12 months minimum (Principle 6) — extended if regulatory hold | Time-based | Append-only signed log (ADR-005); deletion is automated and audited |
| Billing records | 7 years (HMRC tax retention) | Time-based | Automated purge schedule |
| Usage telemetry (raw) | 13 months | Time-based | Automated purge |
| Usage telemetry (anonymised aggregate) | Indefinite | N/A — anonymised | Anonymisation method documented |
| Companies House verification | Outcome retained for tenancy lifetime; raw response 24 hours | Time-based | Automated purge of raw response |

---

## 3. Consultation

### 3.1 Internal Stakeholders

| Stakeholder | Role | Consulted? | Input |
|-------------|------|------------|-------|
| Service Owner | Data controller (vendor-internal) / SIRO-equivalent | Yes | Mission and proportionality framing |
| Lead Architect | Architecture and ADRs | Yes | Technical safeguards; ADR-001/003/004/005 |
| DPO | Author and accountable for this DPIA | Yes | UK GDPR posture |
| Security Lead | Security control acceptance | Yes | Defence-in-depth review; SbD §10 acceptance |
| Accessibility Lead | Inclusive privacy notice / SAR / portability flows | Yes | Accessibility of rights-exercise mechanisms |
| Finance Lead | Billing-data flow | Yes | Tax-retention requirements |

### 3.2 External Stakeholders

**Data subjects**: consultation will be conducted by **survey** (Recommended approach in skill prompt; aligned with `ARC-001-STKE-v1.0.md` quarterly user group) — not interviews / workshops — for proportionality given the population is professional adults using a B2B service in a work context. Survey items (sample): "Are you content with audit-logging of your in-service actions?" "Do the privacy notice and sub-processor list give you the information you need?" "Are the SAR / export / deletion mechanisms easy to find and use?"

**Data subject categories consulted**:

- SME tenant administrators (via in-product survey at GA + 30 days)
- SME tenant users (annual user-group survey)
- Pilot DDaT architects (face-to-face during pilot programme)
- Vendor operators (vendor-team survey)

**External experts**: pre-GA consultation with NCSC liaison (informal advisory) and a privacy-law counsel review for the privacy notice. ICO not consulted at this stage (no residual high risk requires Article 36 prior consultation — see §7).

### 3.3 Data Processors and Sub-Processors

All sub-processors named in §2.7 have signed (or will sign pre-GA) a UK GDPR Article 28-compliant DPA. AI sub-processor's DPA includes explicit no-training-on-customer-data clause and Article 46 transfer mechanism. Quarterly DPO review (RISK R-011 control) re-tests these positions.

---

## 4. Necessity and Proportionality

### 4.1 Lawful Basis Register

| Processing Purpose | Article 6 Basis | Article 9 Condition | Justification |
|--------------------|-----------------|---------------------|---------------|
| PUR-1 Provision tenant accounts | (b) Performance of contract | N/A | Necessary to deliver the service the tenant contracted for |
| PUR-2 Authenticate users | (b) Performance of contract | N/A | Inseparable from contract performance |
| PUR-3 Audit trail | (c) Legal obligation + (f) Legitimate interest | N/A | UK GDPR accountability + service security (LIA below) |
| PUR-4 Billing | (b) Contract + (c) Legal obligation (HMRC) | N/A | Tax-record retention is a legal obligation |
| PUR-5 Operate / monitor service | (f) Legitimate interest | N/A | LIA below |
| PUR-6 AI generation | (b) Contract — user-initiated feature | N/A | Provided only on user request |
| PUR-7 SME-eligibility verification | (b) Contract (for SME-tier eligibility) | N/A | Necessary for tier-pricing terms |

**Legitimate Interest Assessment (LIA)** for PUR-3 (audit trail) and PUR-5 (operate/monitor):

- **Purpose**: service security, abuse detection, capacity planning, service improvement.
- **Necessity**: cannot be achieved with less data — security monitoring requires action attribution to a tenant user; operate-and-improve requires usage telemetry.
- **Balancing**: data subjects are professional adults using a work service; expectations of operational logging are well-established in the industry; data is not used for marketing or third-party sharing; aggregated where possible; transparency provided in privacy notice; opt-out for non-essential telemetry available via tenant admin settings.
- **Outcome**: legitimate interest is appropriate and proportionate.

### 4.2 Necessity Test

For each processing purpose, the data collected is the **minimum necessary** to achieve the purpose:

| Purpose | Minimum Data Justification |
|---------|----------------------------|
| Authenticate user | Identity claim (subject ID) + role; no biographical data required |
| Audit log | User ID + action + timestamp; no broader context retained |
| Bill tenant | Organisation legal entity + billing contact (one person per tenant); no card data held by vendor |
| Operate / monitor | Aggregated counters; no per-user content sampling |
| AI generation | Only user-supplied prompt + the user's own project context; no cross-tenant data |
| SME verification | Outcome only retained; raw Companies House response purged in 24 hours |

### 4.3 Proportionality

The processing is proportionate. A less-intrusive design (e.g., no audit log) is not feasible because tenant security and accountability under UK GDPR mandate it. A less-intrusive design (e.g., no telemetry) would prevent operate-and-improve activity that is itself a legitimate-interest requirement for the cross-subsidy economics (RISK R-001 / R-006 controls).

### 4.4 Data Minimisation

- No collection of personal data beyond the §2.5 inventory.
- No sensitive (Article 9) data.
- No collection of unnecessary biographical fields.
- No tracking cookies; no third-party analytics.
- AI prompts contain only the user's own project content — no cross-tenant data, no identity tokens.
- Telemetry aggregated; per-user metrics anonymised before retention beyond 13 months.

---

## 5. Risk Assessment

> Risk = Likelihood × Severity (impact on individuals' rights and freedoms). Severity scaled per ICO guidance (Minimal / Significant / Severe). Privacy risks below are distinct from organisation-impact risks in `ARC-001-RISK-v1.0.md`, but cross-referenced where they share controls.

| ID | Risk to Individuals | Likelihood | Severity | Inherent | Mitigated By | Residual | Linked Org Risk |
|----|---------------------|------------|----------|----------|--------------|----------|-----------------|
| **DPIA-001** | Cross-tenant exposure of one tenant's user list / artefact metadata to another tenant | Probable (without controls) | Severe (loss of confidentiality of professional identity + project intent) | 🔴 High | ADR-001 namespace per tenant + tenant-ID enforcement + CI iso tests + audit log + bulkhead (`ARC-001-SBD-v1.0.md` §1 B3 + §10 R-008) | 🟢 Low (likelihood Remote; severity unchanged at Severe — defence-in-depth working as designed) | RISK R-008, R-014 |
| **DPIA-002** | AI sub-processor uses user-supplied prompt (which may incidentally include user names) for model training, against tenant DPA | Possible (without controls) | Significant | 🟠 Medium | Contractual no-training-on-customer-data clause (ADR-004); pluggable abstraction enabling ≤ 5-day switch; quarterly DPO review (RISK R-011 control) | 🟢 Low | RISK R-011 |
| **DPIA-003** | Personal data sent to AI sub-processor in non-UK jurisdiction without adequate safeguards | Possible | Significant | 🟠 Medium | Article 46 Standard Contractual Clauses + Transfer Risk Assessment (TRA) where non-UK; tenant transparency + sub-processor list + 30-day notice | 🟢 Low | RISK R-011 |
| **DPIA-004** | Audit log retention exceeds purpose — long-term accumulation of user-identifying activity | Possible | Significant | 🟠 Medium | 12-month minimum, no maximum imposed by default; explicit retention policy with automated purge after policy period; tenant configurability for short retention | 🟢 Low | — |
| **DPIA-005** | Tenant administrator misuses audit log to surveil tenant users (work-context surveillance) | Remote | Significant | 🟢 Low | Audit log designed for security / accountability, not productivity tracking; tenant DPA imposes employer-side data-protection obligations on the tenant; user-facing transparency that audit log exists | 🟢 Low | — |
| **DPIA-006** | Failure to honour SAR within 1 month timeline | Possible | Significant | 🟠 Medium | Tenant export (BR-007) is one-click + completes within NFR-P-003 target; documented SAR runbook; DPO escalation path | 🟢 Low | — |
| **DPIA-007** | Failure to honour erasure right (deletion + verifiable destruction) | Possible | Significant | 🟠 Medium | BR-007 + Principle 7 mandate verifiable destruction certificate; 30–90-day grace period communicated; automated deletion with audit trail | 🟢 Low | — |
| **DPIA-008** | AI sub-processor security incident exposes prompt content (which may include data-subject names within artefact metadata) | Remote | Significant | 🟢 Low | Sub-processor with strong security posture (DPA + provider security disclosure); pluggable provider so switch in ≤ 5 working days (Outcome O-7); incident-notification SLA in DPA | 🟢 Low | RISK R-011, R-017 |
| **DPIA-009** | Rights-of-subject (rectification, restriction, objection, portability) not fully implemented for all categories | Possible | Significant | 🟠 Medium | Rectification: in-product editing; Portability: BR-007 export; Restriction: tenant-admin role suspension; Objection: DPO contact + handling SLA; gap analysis below | 🟢 Low | — |
| **DPIA-010** | Privacy notice unclear / out-of-date / inaccessible | Possible | Significant | 🟠 Medium | Pre-GA publication of WCAG 2.2 AA-conformant notice; annual review + on-change update; sub-processor list maintained inline | 🟢 Low | — |
| **DPIA-011** | Breach not notified to ICO within 72 hours | Possible | Severe | 🔴 High | Incident runbook + ICO 72-h notification template (RISK §H Priority-1 action 7); pre-prepared template; on-call rotation | 🟢 Low | RISK R-008 |
| **DPIA-012** | AI generation output produces hallucinated personal data attributed to data subjects in artefacts | Possible | Significant | 🟠 Medium | AI is drafting-only; lineage-metadata flags AI vs human content (FR-004); user is the artefact author and reviews before publication; AI doesn't factor user data into output (no fine-tuning on customer data) | 🟢 Low | RISK R-010 |
| **DPIA-013** | Insider threat: vendor operator accesses tenant content beyond the support scope | Possible | Severe | 🔴 High | Privileged Access Management (PAM, SbD §1 B2 — pending pre-GA); just-in-time elevated access with audit; quarterly access review; signed audit log; cyber liability insurance secondary control | 🟢 Low | RISK R-008 (T8) |
| **DPIA-014** | Re-identification of data subjects in "anonymised" aggregate telemetry | Remote | Significant | 🟢 Low | Anonymisation thresholds documented; k-anonymity ≥ 5 for any disclosed aggregate; periodic re-identification risk assessment | 🟢 Low | — |
| **DPIA-015** | Companies House outage forces relaxation of SME verification — wrong tier or wrong basis applied | Possible | Minimal | 🟢 Low | Conflict C-3 resolution: provisional access on outage with manual verification fallback (RISK R-005 control) | 🟢 Low | RISK R-005 |

**Risk Summary**: 0 residual High; 0 residual Medium; 15 residual Low. ICO Article 36 prior consultation is **NOT REQUIRED** — see §7.

---

## 6. Mitigations

Mitigations below are extracted from `ARC-001-SBD-v1.0.md`, `ARC-000-PRIN-v2.0.md`, and ADR-001/003/004/005 — this DPIA inherits them rather than restating in detail. Where a control has not yet been deployed, it is listed as a Priority-1 pre-GA action.

### 6.1 Technical Mitigations (Inherited from `ARC-001-SBD-v1.0.md`)

| Mitigation | DPIA Risks Addressed | Status | Reference |
|------------|----------------------|--------|-----------|
| Namespace-per-tenant + tenant-ID enforcement | DPIA-001 | Implemented | ADR-001 |
| Default-deny network policy | DPIA-001 | Implemented | ADR-006 |
| CI tenant-isolation tests on every PR | DPIA-001 | Implemented | NFR-SEC-002 |
| Encryption at rest + in transit | DPIA-001, DPIA-008, DPIA-013 | Implemented | NFR-SEC-001/003 |
| Signed immutable audit log | DPIA-001, DPIA-005, DPIA-013 | Implemented | ADR-005 |
| Independent pen test pre-GA | DPIA-001, DPIA-013 | Pre-GA – 60 days | RISK §H action 1 |
| MFA for tenants and operators | DPIA-013 | Implemented | Principle 5 |
| Privileged Access Management | DPIA-013 | Pre-GA – 30 days | SbD §1 B2 |
| EDR / runtime threat detection | DPIA-013 | Pre-GA – 30 days | SbD §1 B4 |
| Sub-processor DPA with no-training clause + Article 46 SCCs | DPIA-002, DPIA-003 | Implemented | ADR-004 |
| Pluggable AI provider — ≤ 5-day switch | DPIA-002, DPIA-003, DPIA-008 | Implemented | ADR-004 |
| Anonymisation k-anonymity ≥ 5 for aggregate telemetry | DPIA-014 | Implemented | Principle 6 |

### 6.2 Organisational Mitigations

| Mitigation | DPIA Risks Addressed | Status | Reference |
|------------|----------------------|--------|-----------|
| Tenant DPA imposes employer-side responsibilities | DPIA-005 | Implemented | BR-006 |
| Quarterly DPO review of sub-processors | DPIA-002, DPIA-003, DPIA-008 | Implemented | RISK R-011 control |
| Quarterly access review | DPIA-013 | Pre-GA – 30 days | SbD §1 B2 |
| Annual phishing-awareness training | DPIA-013 | Pre-GA – 30 days | SbD §1 B6 |
| Vulnerability disclosure programme | DPIA-001, DPIA-008 | Pre-GA – 30 days | SbD §1 B6 |
| AI Playbook / ATRS scope-boundary gate | DPIA-012 | Pre-GA per RISK R-010 P2 action | `ARC-001-AIP-v1.0.md` (pending) |
| Privacy notice review cadence | DPIA-010 | Annual + on-change | This DPIA |

### 6.3 Procedural Mitigations

| Mitigation | DPIA Risks Addressed | Status | Reference |
|------------|----------------------|--------|-----------|
| Incident runbook + ICO 72-h notification template | DPIA-011 | Pre-GA – 30 days | SbD §1 D1 / RISK §H action 7 |
| SAR runbook + 1-month SLA monitoring | DPIA-006 | Pre-GA | This DPIA §11 |
| Erasure runbook + destruction certificate | DPIA-007 | Pre-GA | BR-007 |
| Sub-processor change 30-day tenant notice | DPIA-003 | Implemented | RISK R-011 control |
| Tenant transparency: sub-processor list, privacy notice, audit-log access | DPIA-005, DPIA-010 | Pre-GA | BR-006 |

---

## 7. ICO Prior Consultation (UK GDPR Article 36)

**ICO Prior Consultation Required?**: ❌ **NOT REQUIRED**.

**Rationale**: All 15 DPIA risks reduce to Low residual after mitigations. No residual High remains. The mitigations are proportionate and feasible. The Article 35 DPIA conclusion is favourable.

**Re-trigger conditions** for reopening Article 36 consideration:

- Any DPIA risk that re-emerges at residual High in a refreshed assessment.
- Any new processing purpose introducing special-category data, large-scale processing, vulnerable subjects, or solely-automated decision-making with legal / significant effect.
- Any sub-processor change where the new sub-processor's safeguards are materially weaker.
- Any actual data breach with ICO-significant impact.

---

## 8. Sign-off and Approval

> Pre-GA sign-off is conditional on the §6 Pre-GA actions (PAM, EDR, VDP, incident runbook, ROPA, privacy notice, AI feature-scope boundary, ATRS) landing.

| Role | Name | Decision | Date | Signature |
|------|------|----------|------|-----------|
| Data Controller (Vendor) | Mark Craddock, Service Owner | [PENDING] Approve DPIA conditional on §6 pre-GA actions | [PENDING] | _________ |
| DPO | [PENDING] | [PENDING] Endorse DPIA findings and mitigations | [PENDING] | _________ |
| Senior Responsible Owner / SIRO-equivalent | Mark Craddock, Service Owner | [PENDING] Accept residual privacy risk position | [PENDING] | _________ |
| Lead Architect | [PENDING] | [PENDING] Confirm technical mitigations as designed | [PENDING] | _________ |
| Security Lead | [PENDING] | [PENDING] Confirm security mitigations | [PENDING] | _________ |

---

## 9. Review and Monitoring

### 9.1 Review Triggers

- **Time-based**: 12-month review (next 2027-05-03).
- **Event-based**:
  - Any change in personal-data inventory (§2.5).
  - Any change in sub-processor (AI / cloud / payment / SIEM forwarding).
  - Any change to AI feature surface (drafting → recommendation; new model class).
  - Any data breach.
  - Any ICO guidance update relevant to multi-tenant SaaS / AI processing.
  - Any change in tenant data-subject categories (e.g., adding non-professional users).
  - Sovereign deployment scope-creep into Project 001.
- **Cyclical**: quarterly DPO sub-processor review re-validates key mitigations (DPIA-002, -003, -008).

### 9.2 KPIs / KRIs (linked to RISK §J)

- SAR / erasure / portability response times (target: SAR < 30 days; erasure < 30 days).
- Sub-processor-change events (target: 30-day notice on every change, with no exception).
- Audit-log access by vendor operators (target: zero un-justified access in quarterly review).
- AI feature-scope events (target: tracked, none uncategorised).
- ICO correspondence count (target: 0).

---

## 10. Traceability

| Source / Sibling Artefact | Use |
|---------------------------|-----|
| `ARC-000-PRIN-v2.0.md` | Principles 5 (Security by Design), 7 (UK Sovereignty + Residency + Governance), 8 (Tenant Isolation), 9 (Data Quality / Lineage / Portability) |
| `ARC-001-REQ-v1.0.md` | NFR-SEC-001..004; BR-001..008 (esp. BR-006 evidence pack, BR-007 portability); FR-001 (verification), FR-002 (multi-tenant workspace), FR-004 (AI generation) |
| `ARC-001-STKE-v1.0.md` | SD-11 (DPO driver), SD-12 (ICO regulator), Goal G-5 (UK GDPR posture); Conflict C-2 / C-3 |
| `ARC-001-RISK-v1.0.md` | R-008 / R-010 / R-011 / R-014 / R-017 cross-referenced; this DPIA is the privacy-impact lens on the same controls |
| `ARC-001-TCOP-v1.0.md` | Point 7 (Privacy Integral) — DPIA closes the principal Point-7 gap |
| `ARC-001-SBD-v1.0.md` | §3 UK GDPR; §10 acceptance vehicle for R-010 / R-011 — this DPIA grounds the §10 position |
| `ARC-001-ADR-001-v1.0.md` | Tenant Isolation — DPIA-001 control |
| `ARC-001-ADR-003-v1.0.md` | Identity & SSO — auth metadata processing |
| `ARC-001-ADR-004-v1.0.md` | AI Provider Abstraction — DPIA-002, DPIA-003, DPIA-008, DPIA-012 |
| `ARC-001-ADR-005-v1.0.md` | Observability + audit log — DPIA-001, DPIA-004, DPIA-005, DPIA-013 |
| `ARC-001-AIP-v1.0.md` | (Pending generation) AI Playbook — DPIA-012 cross-reference |
| `ARC-001-DM-v1.0.md` | (Pending generation) Data Model — formalises the inventory at §2.5 |

---

## 11. Data Subject Rights — Implementation Inventory

| Right | UK GDPR Art. | Mechanism | Status | Gaps |
|-------|--------------|-----------|--------|------|
| **Subject Access Request (SAR)** | 15 | Tenant-administrator self-service export (BR-007) for tenant-scoped content; DPO mailbox for vendor-held metadata (auth, billing) | Implemented (export); DPO mailbox standing up pre-GA | Document SAR runbook + 1-month SLA monitor |
| **Rectification** | 16 | In-product editing of tenant content + admin user attributes | Implemented | — |
| **Erasure ("right to be forgotten")** | 17 | Tenancy termination → automated deletion + 30–90-day grace + verifiable destruction certificate (BR-007 + Principle 7) | Implemented | Document erasure runbook |
| **Restriction of processing** | 18 | Tenant-admin role suspension; DPO mailbox for individual restriction requests | Implemented | Restriction runbook (LOW priority) |
| **Data portability** | 20 | One-click full export in open formats (Markdown / JSON / YAML / SBOM) — BR-007, ADR-007, Principle 9 | Implemented | — |
| **Objection** | 21 | DPO contact; LIA-applicable purposes only (PUR-3, PUR-5); on legitimate-interest grounds the controller must demonstrate compelling grounds | Implemented; runbook pre-GA | Objection runbook |
| **Automated decision-making** | 22 | N/A — no solely-automated decisions of legal / significant effect (RISK R-010 control) | Compliant | Maintain via R-010 P2 boundary review |
| **Right to be informed** | 13/14 | Privacy notice publication (pre-GA) + sub-processor list + audit-log transparency | Pre-GA | Publish privacy notice |
| **Right to lodge complaint with ICO** | 77 | Privacy notice signposts ICO contact; DPO mailbox does not gate complaint route | Pre-GA | Publish privacy notice |

**Gap summary**: 7 rights fully implemented; 4 require runbook documentation pre-GA (SAR, erasure, restriction, objection); privacy notice publication closes the §13/14 right-to-be-informed gap. All gaps Priority-1 pre-GA.

---

## 12. International Transfers

### 12.1 Transfer Inventory

| Sub-processor | Data Sent | Destination | Mechanism |
|---------------|-----------|-------------|-----------|
| AI / LLM provider (ADR-004) | Generation prompt + context (no identity tokens) | UK / EEA where available; potentially non-UK depending on configuration | Article 46 Standard Contractual Clauses (where non-UK); Transfer Risk Assessment (TRA) on file |
| Cloud provider (ADR-002, ADR-006) | All content at rest + in transit | UK regions only by default (Principle 7) | UK residency; no transfer outside UK by default |
| Payment processor | Billing-contact details + tenant org reference | Per processor's residency posture | DPA + Article 46 mechanism if non-UK |
| Companies House | Outbound query — no personal data sent | UK | N/A (UK to UK) |

### 12.2 Transfer Risk Assessment Summary

For the AI sub-processor where non-UK processing occurs:

- **Country / regime**: assessed against UK / EU adequacy + onward-transfer risk + government-access regimes (per ICO TIA template).
- **Supplementary measures**: encryption in transit; no identity tokens passed in prompt; pluggable abstraction enables exit without prejudice.
- **Documented in**: this DPIA + DPA + sub-processor register; refreshed quarterly.

### 12.3 Tenant-Side Transfer Decisions

Tenants may opt out of non-UK processing (Principle 7 commitment); on such opt-out, AI provider is configured to UK-region processing, or AI feature is disabled for the tenant.

---

## 13. Children's Data

**Not applicable** — service is B2B; data subjects are professional adults using the service in a work context. Sign-up T&Cs require user to be ≥ 16 years old (UK GDPR ICO digital-services minimum) and to be acting in a work capacity. No special children's-data assessment required. If ever the use case changes (e.g., university student SMEs), a refresh is triggered.

---

## 14. AI / Algorithmic Processing

> Cross-references: `ARC-001-AIP-v1.0.md` (pending generation via `/arckit:ai-playbook`); `ARC-001-RISK-v1.0.md` R-010 (AI Playbook scope drift); ADR-004 (AI Provider Abstraction).

### 14.1 AI Use Case in Scope

AI is used **only for drafting assistance** (FR-004): the user provides a prompt or selects existing project context, AI returns a draft, the user reviews and edits before saving. AI does **not**:

- Make decisions affecting the tenant or any data subject.
- Score / rank / triage suppliers, users, or organisations.
- Profile data subjects.
- Use customer data for model training (contractual no-training clause in DPA).

This places the AI use squarely outside Article 22 (no solely-automated decisions of legal / significant effect).

### 14.2 AI-Specific DPIA Risks

- **DPIA-008**: AI sub-processor security incident exposes prompt content (mitigated to Low).
- **DPIA-012**: AI hallucinates personal data attributed to data subjects in artefacts (mitigated to Low — drafting-only, lineage flags AI vs human content, user is artefact author and reviewer).

### 14.3 Algorithmic Transparency

- Lineage metadata flags AI-generated content vs human content (FR-004).
- ATRS (Algorithmic Transparency Recording Standard) record published before any recommendation-class AI surface ships (RISK R-010 control + `ARC-001-AIP-v1.0.md`).
- Tenant-facing documentation explains AI use in plain English.
- Quarterly DPO review of AI feature surface area (RISK R-010 P2 action).

### 14.4 Bias Mitigation

For drafting-only AI, bias risk is limited (no decision-impact on data subjects). The principal residual concern is over-reliance on AI in artefact authoring; this is mitigated by (a) the platform's audit-log lineage flagging AI content, (b) explicit user-reviewer role before publication, (c) DDaT-architect feedback loops in the pilot programme.

### 14.5 Human Oversight

Every AI output is reviewed and edited by a human author before any external use. The platform does not auto-publish AI output. Human-in-the-loop is architectural.

---

## 15. Summary and Action Plan

### 15.1 Summary Table

| Area | Result |
|------|--------|
| ICO 9-criteria screening | 1/9 + 1 partial → DPIA recommended (and produced) |
| Personal data categories | 8 categories — all general personal data; no Article 9; no Article 10; no children's data |
| Lawful basis | Mostly Art. 6(1)(b) Contract + (1)(c) Legal obligation (audit, billing) + (1)(f) Legitimate interest (LIA documented) |
| Data subjects | ~1500–2000 professional adults at GA + 12 months; no vulnerable groups |
| International transfers | AI sub-processor (Article 46 SCCs + TRA); cloud is UK-only by default |
| Total privacy risks identified | 15 |
| Risk distribution (residual) | 0 High / 0 Medium / 15 Low |
| Mitigations | 12 technical + 7 organisational + 5 procedural — most inherited from `ARC-001-SBD-v1.0.md` |
| ICO prior consultation | ❌ NOT REQUIRED |
| Data subject rights | 7 implemented + 1 N/A (Art. 22) + 1 (privacy notice) pending pre-GA |
| Children's data | N/A (B2B professional service) |
| AI/ML processing | Drafting-only; Article 22-safe; ATRS publication pre-GA |
| Sign-off | Pending — Service Owner + DPO + SIRO-equivalent + Lead Architect + Security Lead |
| Review cycle | 12 months + event-based + quarterly DPO sub-processor cadence |

### 15.2 Action Plan

| # | Action | Owner | Priority | Due |
|---|--------|-------|----------|-----|
| 1 | Publish privacy notice + sub-processor list | DPO | CRITICAL | GA |
| 2 | Document SAR / erasure / restriction / objection runbooks with SLA monitors | DPO | HIGH | GA – 30 days |
| 3 | Finalise ROPA | DPO | CRITICAL | GA |
| 4 | Generate `ARC-001-AIP-v1.0.md` and publish ATRS record | DPO + Lead Architect | CRITICAL | GA |
| 5 | Define AI feature-scope boundary (drafting / recommendation) — RISK R-010 P2 | DPO + Lead Architect | HIGH | 2026-07-31 |
| 6 | Procure cyber liability insurance (RISK §H action 6) | Service Owner + Finance | HIGH | GA – 30 days |
| 7 | Generate `ARC-001-DM-v1.0.md` to formalise §2.5 inventory | Lead Architect | MEDIUM | GA + 60 days |
| 8 | Quarterly sub-processor review cadence locked | DPO | MEDIUM | GA + 30 days |
| 9 | Publish tenant-facing audit-log access mechanism | Lead Architect | HIGH | GA |
| 10 | Run data-subject consultation survey | DPO | MEDIUM | GA + 30 days |
| 11 | Annual DPIA review scheduled | DPO | LOW | 2027-05-03 |

---

## External References

> No external policy documents were placed in `projects/001-arckit-saas/external/` at the time of generation. UK GDPR / ICO guidance / Standard Contractual Clauses are public-domain and cited by name.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| — | — | — | — | — |

### References

- UK GDPR Article 35: <https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/data-protection-impact-assessments-dpias/>
- ICO DPIA Guidance: <https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/data-protection-impact-assessments-dpias/what-is-a-dpia/>
- ICO Article 46 Transfer Tool / SCCs: <https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/international-transfers/international-data-transfer-agreement-and-guidance/>
- ICO Algorithmic Transparency Recording Standard: <https://www.gov.uk/government/publications/algorithmic-transparency-recording-standard-hub>
- UK Government AI Playbook: cross-referenced in `ARC-001-AIP-v1.0.md` (pending)

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:dpia` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Sourced from ARC-000-PRIN-v2.0, ARC-001-REQ-v1.0, ARC-001-STKE-v1.0, ARC-001-RISK-v1.0, ARC-001-TCOP-v1.0, ARC-001-SBD-v1.0, ADR-001/003/004/005, and the user-supplied personal-data scope. Pre-GA Alpha-stage assessment. Refresh on `ARC-001-DM-v1.0.md` issuance and on AI feature-scope boundary review.
