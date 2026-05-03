# Architecture Diagram: ArcKit SaaS — Critical Interaction Sequence Flows

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:diagram`

## Document Control

| Field | Value |
|-------|-------|
| Document ID | ARC-001-DIAG-002-v1.0 |
| Document Type | Architecture Diagram (Sequence — Mermaid) |
| Project | ArcKit as a Service (001-arckit-saas) |
| Classification | OFFICIAL |
| Status | DRAFT |
| Version | 1.0 |
| Created Date | 2026-05-03 |
| Last Modified | 2026-05-03 |
| Review Cycle | Quarterly (or on major flow change) |
| Next Review Date | 2026-06-02 |
| Owner | Mark Craddock, Service Owner |
| Reviewed By | [PENDING — Lead Architect] |
| Approved By | [PENDING — Architecture Review Board Chair] |
| Distribution | Project Team, Architecture Team, Security Lead, DPO, Pilot Tenants |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:diagram` command. Five Mermaid sequence diagrams covering the load-bearing interaction flows of the ArcKit SaaS pre-GA Alpha: tenant onboarding, OIDC SSO with tenant_id propagation, AI-assisted generation with sub-processor call, tenant export and exit, and signed-immutable audit-log query. | [PENDING] | [PENDING] |

---

## 1. Document Purpose

This document records the five most architecturally consequential **interaction sequences** in the ArcKit SaaS pre-GA Alpha. It complements:

- `ARC-001-DIAG-001-v1.0` — C4 Context and Container views (structural).
- `ARC-001-DIAG-003-v1.0` — Deployment view (cell topology, AZs, regions).

The sequences here pin down behavioural concerns the structural diagrams cannot show on their own: where `tenant_id` is asserted, where mTLS is required, where audit-log appends are mandatory, and where graceful failure modes apply. Each diagram is anchored to specific requirements (REQ) and decisions (ADR). Each one includes an `alt`-block error path so the failure mode is visible alongside the happy path.

**Audience**: Lead Architect, Security Lead, SRE Lead, DPO, ARB reviewers, pilot DDaT architects (SD-3, SD-6), and the project-002 sovereign-track liaison who will reuse most of these flows behind a customer IdP.

---

## 2. Cross-Cutting Conventions

The following invariants apply to every diagram below. Stating them once here keeps the diagrams uncluttered.

| Invariant | Mechanism | Anchor |
|-----------|-----------|--------|
| **`tenant_id` propagation** | Resolved from OIDC `tid` claim at the API Gateway; carried in request context, on every internal call (header `X-ArcKit-Tenant-Id` plus signed JWT), in every database query (row-level security), in every object-storage prefix, and on every AI-provider call. Default-deny if missing. | ADR-001, ADR-003, NFR-SEC-002 |
| **Service-to-service mTLS** | Every internal service-to-service call inside a cell uses mutual TLS via the service mesh; pod identities are SPIFFE-style; tokens are short-lived (<= 60 minutes for human; <= 5 minutes for service). | ADR-006, NFR-SEC-007 |
| **Audit-log append** | Every state-changing call emits an OpenTelemetry event tagged with `tenant_id`, actor identity, command, timestamp, request_id; the audit pipeline appends to a tamper-evident hash chain (each record's hash includes the prior record's hash). PII is redacted at source. | ADR-005, FR-012, NFR-C-002 |
| **Identity tokens** | OIDC ID tokens for end users (vendor IdP for SMEs, federated for enterprise); WebAuthn hardware-key MFA for operators on a separate IdP; service tokens are workload-bound (mTLS + SPIFFE). | ADR-003, NFR-SEC-001 |
| **Failure-safe defaults** | Manual authoring (FR-003) always works even if AI is down; signup fails closed if Companies House is unreachable for verification; export fails closed (no partial archive). | NFR-A-003, FR-003 |

> **Notation**: solid arrow = synchronous request; dotted arrow = response; `alt` = alternative failure path; `Note over` = invariant or constraint that applies to the bracketed lifelines.

---

## 3. Flow 1 — SME Tenant Self-Service Onboarding with Companies House Verification

**Use Case**: UC-1 (SME tenant onboarding, free tier).
**Requirements**: FR-001 (self-service signup), FR-010 (account lifecycle), INT-003 (Companies House), BR-001 (free tier).
**ADRs**: ADR-001 (tenant_id allocation), ADR-002 (UK residency), ADR-003 (vendor IdP), ADR-008 (default tier quotas).

### 3.1 Narrative

A prospective SME founder visits the marketing site, accepts terms, and creates a tenant. The Tenant Service verifies the company against Companies House (INT-003) — this is the gate that distinguishes a real SME tenant from speculative signup. On success, ADR-001's tenant-allocation flow runs: a `tenant_id` is generated, a vendor-IdP organisation is provisioned, the founder is bound as the first tenant administrator, the tenant is assigned to a cell (C13 Cell Management Service), default-tier quotas are seeded (ADR-008), and a verification email is dispatched. The founder confirms email and signs in. Failure to verify with Companies House short-circuits the flow with a manual-review path; this is the dominant error case in pre-GA Alpha pilots.

### 3.2 Diagram

```mermaid
sequenceDiagram
    autonumber
    actor Founder as SME Founder
    participant Web as Web App (C2)
    participant GW as API Gateway (C1)
    participant Tenant as Tenant Service (C3)
    participant CH as Companies House API (INT-003)
    participant IdP as Vendor IdP (ADR-003)
    participant Cell as Cell Mgmt Service (C13)
    participant DB as PostgreSQL (RLS)
    participant Notify as Notification Service (C9)
    participant Audit as Audit Pipeline (ADR-005)

    Founder->>Web: Visit /signup, accept T&Cs, enter company details
    Web->>GW: POST /signup (no tenant_id yet, anonymous)
    GW->>Tenant: createTenant(company_no, email, founder_name)
    Note over GW,Tenant: mTLS, signed service token
    Tenant->>CH: GET /company/{company_no}
    Note over Tenant,CH: TLS 1.3, retry-with-jitter, 5s timeout

    alt Companies House success (active company)
        CH-->>Tenant: 200 {name, status: active, sic_codes}
        Tenant->>Tenant: Allocate tenant_id (ADR-001)
        Tenant->>IdP: POST /orgs (create org, bind founder as admin)
        IdP-->>Tenant: 201 {org_id, user_id}
        Tenant->>Cell: assignTenantToCell(tenant_id)
        Cell-->>Tenant: {cell_id, namespace}
        Tenant->>DB: INSERT tenant, default quotas (ADR-008)
        Note over DB: row-level security; tenant_id NOT NULL
        DB-->>Tenant: OK
        Tenant->>Audit: APPEND {event: tenant.created, tenant_id, actor, ts, hash_chain}
        Tenant->>Notify: sendVerifyEmail(email, verify_url)
        Notify-->>Founder: Verification email
        Tenant-->>GW: 201 {tenant_id, status: pending_email}
        GW-->>Web: 201 (redirect to "check your email")
        Web-->>Founder: "Verify your email to finish setup"
    else Companies House: company not found / dissolved
        CH-->>Tenant: 404 / status: dissolved
        Tenant->>Audit: APPEND {event: tenant.signup_rejected, reason, ts}
        Tenant-->>GW: 422 {error: company_not_verifiable, manual_review_url}
        GW-->>Web: 422
        Web-->>Founder: "We could not verify your company — request manual review"
    else Companies House: timeout / 5xx
        CH--xTenant: timeout after 3 retries
        Tenant->>Audit: APPEND {event: tenant.signup_deferred, reason: ch_unavailable, ts}
        Tenant-->>GW: 503 {error: verification_unavailable, retry_after}
        GW-->>Web: 503
        Web-->>Founder: "Verification service is busy — try again shortly"
    end
```

### 3.3 Notes on Failure Modes

- **Companies House 4xx (not found / dissolved)** is the dominant rejection in pilots. Flow surfaces a manual-review URL; it never silently provisions a tenant. The audit-log append still happens — rejected signups are evidence of fraud-prevention discipline.
- **Companies House 5xx / timeout** must not block legitimate signup permanently; a retry-with-jitter pattern (3 attempts, exponential backoff) precedes a 503. The audit-log records the deferral so SRE can correlate with INT-003 SLA breaches.
- **No tenant is created until Companies House confirms** — defence against speculative or adversarial bulk signups (R-008 cross-tenant blast radius mitigation begins at the door).

---

## 4. Flow 2 — Tenant User OIDC SSO Login with MFA and Tenant_id Propagation

**Use Case**: Prelude to UC-2 (and to every authenticated request).
**Requirements**: FR-007 (SSO), NFR-SEC-001 (MFA), NFR-SEC-002 (tenant isolation), NFR-SEC-003 (authorisation), INT-001 (tenant IdP).
**ADRs**: ADR-001 (claim-based tenant_id resolution), ADR-003 (OIDC/SAML federation), ADR-006 (mTLS in cell).

### 4.1 Narrative

A tenant user — either an SME founder using the vendor IdP, or an enterprise tenant user federating from their own Entra/Okta/Ping IdP — signs into the ArcKit web app. The flow is OIDC Authorization Code with PKCE. MFA is enforced at the IdP (TOTP or WebAuthn for vendor IdP; whatever the federated IdP enforces, with MFA assertion required). The ID token returned contains a `tid` (tenant_id) claim that the API Gateway resolves into the request context. Every subsequent call from the browser to the gateway carries the access token; every internal hop carries the resolved `tenant_id` over mTLS. This is the gate that makes ADR-001 enforceable.

### 4.2 Diagram

```mermaid
sequenceDiagram
    autonumber
    actor User as Tenant User
    participant Web as Web App (C2)
    participant GW as API Gateway (C1)
    participant IdP as Tenant IdP (ADR-003)
    participant Verifier as OIDC Token Verifier (C1 component)
    participant TenantSvc as Tenant Service (C3)
    participant Audit as Audit Pipeline (ADR-005)

    User->>Web: Open app, click "Sign in"
    Web->>GW: GET /auth/login
    GW->>Web: 302 to IdP /authorize (PKCE challenge, state, nonce)
    Web->>IdP: /authorize (browser redirect)
    IdP->>User: Show login + MFA challenge
    User->>IdP: Submit credentials + MFA factor

    alt MFA success
        IdP-->>Web: 302 /callback?code=...&state=...
        Web->>GW: POST /auth/callback (code, PKCE verifier)
        GW->>IdP: POST /token (code, verifier)
        IdP-->>GW: id_token + access_token (JWT, signed)
        GW->>Verifier: verify(id_token)
        Note over Verifier: Validate signature, iss, aud, exp; require mfa_amr; extract tid claim
        Verifier-->>GW: {tenant_id, user_id, mfa: true}

        alt tid claim missing or unrecognised
            GW->>Audit: APPEND {event: auth.rejected_no_tid, ts}
            GW-->>Web: 401 default-deny (ADR-001)
            Web-->>User: "Account not bound to a tenant — contact admin"
        else tid claim valid
            GW->>TenantSvc: getTenantContext(tenant_id)
            Note over GW,TenantSvc: mTLS, short-lived service token
            TenantSvc-->>GW: {tier, status: active, cell_id}
            GW->>Audit: APPEND {event: auth.success, tenant_id, user_id, mfa, ts, hash_chain}
            GW-->>Web: Set HttpOnly session cookie + CSRF token
            Web-->>User: Land on tenant workspace (tenant_id scoped)
        end
    else MFA fail / locked / IdP error
        IdP-->>Web: 302 /callback?error=access_denied
        Web->>GW: POST /auth/callback (error)
        GW->>Audit: APPEND {event: auth.failure, idp, reason, ts}
        GW-->>Web: 401
        Web-->>User: "Sign-in failed — see your IdP for details"
    end
```

### 4.3 Notes on Failure Modes

- **`tid` claim missing / unrecognised** = default-deny (ADR-001 invariant). This is the single most important rejection in the entire architecture; the audit-log entry distinguishes "user has no tenant binding" (config bug or stale federation) from "user authenticated but tenant_id was tampered" (attack signal).
- **MFA assertion missing on enterprise federation** must be rejected at the verifier — the gateway requires `amr` to contain an MFA value. Federated IdPs that do not assert MFA are treated as authentication failure.
- **Replay / clock skew** is mitigated by the `nonce` and `exp` checks; tokens are short-lived (<= 60 minutes for ID, <= 15 minutes for access) per ADR-003.

---

## 5. Flow 3 — AI-Assisted Artefact Generation with Sub-Processor Call and Lineage Capture

**Use Case**: UC-2 (AI-assisted artefact drafting).
**Requirements**: FR-004 (AI generation), FR-005 (provenance), INT-005 (AI provider integration), NFR-P-002 (generation latency), NFR-A-003 (graceful degradation), NFR-SEC-002 (tenant isolation extends to AI).
**ADRs**: ADR-001 (tenant_id propagated to AI calls), ADR-002 (UK/EU residency), ADR-004 (provider-agnostic adaptor, no-train default, per-tenant budget, provenance), ADR-005 (audit-log append), ADR-008 (per-tenant AI budget).

### 5.1 Narrative

A tenant user requests an AI-assisted draft of an artefact (for example, a Strategic Outline Business Case or an ADR). The API Gateway resolves `tenant_id` from the session, then enforces the per-tenant AI budget (ADR-008): if the budget is exhausted, the call is rejected with a 429 and the user is offered manual authoring (FR-003). On budget pass, the AI Generation Service (C5) assembles the prompt from ArcKit templates plus only the project context the tenant has authored, calls the provider-agnostic AIAdaptor (ADR-004), which dispatches to the currently-configured provider over a UK/EU-resident endpoint with a no-train header. The response streams back. The Provenance Metadata Recorder writes a generation event with command, model, model version, prompt hash, response hash, token counts, and timestamp. The artefact is offered to the user for human review (FR-002) — never auto-saved, never auto-published. Audit log records the entire chain.

### 5.2 Diagram

```mermaid
sequenceDiagram
    autonumber
    actor User as Tenant User
    participant Web as Web App (C2)
    participant GW as API Gateway (C1)
    participant Budget as AI-Budget Coordinator (C1 / Redis)
    participant AISvc as AI Generation Service (C5)
    participant Adaptor as Provider-Agnostic AIAdaptor (ADR-004)
    participant Provider as AI Sub-Processor (UK/EU region)
    participant ArtSvc as Project & Artefact Service (C4)
    participant DB as PostgreSQL (RLS)
    participant Audit as Audit Pipeline (ADR-005)

    User->>Web: Click "Generate draft" on artefact
    Web->>GW: POST /artefacts/{id}/generate (session cookie)
    Note over GW: Resolve tenant_id from session; require write scope
    GW->>Budget: checkAndReserve(tenant_id, est_tokens, model_tier)

    alt Budget exhausted
        Budget-->>GW: 0 (deny)
        GW->>Audit: APPEND {event: ai.budget_denied, tenant_id, ts}
        GW-->>Web: 429 {error: ai_budget_exhausted, manual_authoring_url}
        Web-->>User: "AI budget reached — please author manually or upgrade tier"
    else Budget OK
        Budget-->>GW: reservation_id
        GW->>AISvc: generate(tenant_id, artefact_id, command)
        Note over GW,AISvc: mTLS, X-ArcKit-Tenant-Id header, signed service token
        AISvc->>ArtSvc: getProjectContext(tenant_id, artefact_id)
        ArtSvc->>DB: SELECT WHERE tenant_id = $1 (RLS)
        DB-->>ArtSvc: project context (tenant-scoped only)
        ArtSvc-->>AISvc: minimised project context
        AISvc->>AISvc: Assemble prompt (ArcKit template + minimised context)
        AISvc->>Adaptor: invoke(prompt, model, tenant_id, no_train: true)

        alt Provider success
            Adaptor->>Provider: POST /completions (UK/EU endpoint, mTLS, no-train header)
            Note over Adaptor,Provider: tenant_id forwarded as opaque header; PII redacted at source
            Provider-->>Adaptor: streamed tokens
            Adaptor-->>AISvc: response + usage (tokens_in, tokens_out, model_version)
            AISvc->>Budget: commit(reservation_id, actual_tokens)
            AISvc->>AISvc: Compute prompt_hash, response_hash
            AISvc->>DB: INSERT generation_event {tenant_id, artefact_id, model, model_version, prompt_hash, response_hash, tokens, ts}
            Note over DB: ADR-004 provenance metadata; ATRS evidence asset
            AISvc->>Audit: APPEND {event: ai.generation, tenant_id, command, model, prompt_hash, ts}
            AISvc-->>GW: 200 {draft, generation_id}
            GW-->>Web: 200 (draft offered for human review — FR-002)
            Web-->>User: Show draft with "accept / edit / discard" controls
        else Provider 5xx / timeout
            Adaptor--xProvider: timeout / 503
            Adaptor-->>AISvc: ProviderError
            AISvc->>Budget: refund(reservation_id)
            AISvc->>Audit: APPEND {event: ai.generation_failed, tenant_id, reason, ts}
            AISvc-->>GW: 503 {error: ai_unavailable, manual_authoring_url}
            GW-->>Web: 503
            Web-->>User: "AI generation unavailable — author manually (FR-003)"
        end
    end
```

### 5.3 Notes on Failure Modes

- **Budget exhaustion** is a normal, expected condition under ADR-008's per-tenant ceiling. The user is always offered manual authoring (FR-003) — the service is never bricked by AI failure.
- **Provider outage** triggers a budget refund (so the tenant is not charged for a non-event), an audit append, and a graceful 503. NFR-A-003 graceful degradation is preserved.
- **Provenance is non-optional** — even on a successful generation, the provenance event must persist before the user receives the draft. Without it, AI Playbook compliance (transparency, accountability) is unprovable.
- **No auto-save**: the draft is offered for human review (FR-002 always-human-in-the-loop). The audit-log records that AI generated content; a separate event records when (or if) the user accepts it.

---

## 6. Flow 4 — Tenant Data Export and Exit with Verifiable Destruction Certificate

**Use Case**: UC-3 (tenant export and exit).
**Requirements**: FR-006 (export), FR-011 (offboarding + destruction), BR-007 (G-Cloud exit plan), NFR-I-002 (open-format round-trip), NFR-C-001 (UK GDPR Articles 17 and 20), NFR-P-003 (export performance).
**ADRs**: ADR-001 (tenant_id-scoped export), ADR-005 (audit-log append for the entire flow), ADR-007 (Markdown + JSON manifest + YAML lineage in a Cosign-signed tarball with CI-tested round-trip).

### 6.1 Narrative

A tenant administrator initiates exit. The flow is two-phase by design: first **export** (the tenant takes its data away in a verified, open format); then **destruction** with a signed certificate (the vendor proves the data is gone). The Export Service (C6) assembles a tarball containing every artefact as Markdown, a JSON manifest with hashes per file, and a YAML lineage file (decision history, generation provenance from ADR-004). The tarball is signed with Cosign and a SHA-256 manifest. A signed URL (24-hour expiry) is delivered. The tenant administrator confirms receipt and then triggers destruction. Destruction runs across PostgreSQL (delete tenant_id-scoped rows), object storage (delete prefix), search index (delete partition), backups (suppress on next rotation per retention policy). On completion, a destruction certificate is issued — itself signed, itself written to the tamper-evident audit log — confirming that destruction is verifiable, not merely asserted.

### 6.2 Diagram

```mermaid
sequenceDiagram
    autonumber
    actor Admin as Tenant Admin
    participant Web as Web App (C2)
    participant GW as API Gateway (C1)
    participant Tenant as Tenant Service (C3)
    participant Export as Export Service (C6)
    participant DB as PostgreSQL (RLS)
    participant Obj as Object Storage (per-tenant prefix)
    participant Search as Search Index
    participant Sign as Signing Service (Cosign)
    participant Audit as Audit Pipeline (ADR-005)
    participant Notify as Notification Service (C9)

    Admin->>Web: Settings → Export & Exit → Request export
    Web->>GW: POST /tenants/{tenant_id}/export
    GW->>Export: startExport(tenant_id, requestor)
    Note over GW,Export: mTLS; export rate-limit (ADR-008); tenant_id from session
    Export->>Audit: APPEND {event: export.started, tenant_id, actor, ts}
    Export->>DB: SELECT artefacts, decisions, lineage WHERE tenant_id = $1 (RLS)
    DB-->>Export: rows
    Export->>Obj: GET attachments under prefix tenants/{tenant_id}/
    Obj-->>Export: blobs
    Export->>Export: Build tarball — Markdown artefacts + JSON manifest + YAML lineage (ADR-007)
    Export->>Sign: sign(tarball)
    Sign-->>Export: cosign signature + SHA-256 manifest

    alt Export success
        Export->>Obj: PUT signed tarball under exports/{tenant_id}/
        Export->>Export: Issue signed URL (24h expiry)
        Export->>Audit: APPEND {event: export.completed, tenant_id, sha256, size, ts}
        Export->>Notify: emailExportReady(admin, signed_url, sha256)
        Notify-->>Admin: Export ready (URL, SHA-256, signature instructions)
        Export-->>GW: 200 {export_id, expires_at}
        GW-->>Web: 200
        Web-->>Admin: "Download ready — verify signature before destruction"

        Admin->>Admin: Download tarball, verify Cosign + SHA-256 (CI-tested round-trip on tenant side)
        Admin->>Web: Confirm exit → Initiate destruction
        Web->>GW: POST /tenants/{tenant_id}/destroy (requires re-auth + step-up MFA)
        GW->>Tenant: destroyTenant(tenant_id)
        Tenant->>Audit: APPEND {event: destroy.started, tenant_id, actor, ts}
        par Destroy across stores
            Tenant->>DB: DELETE WHERE tenant_id = $1 (cascade; RLS-scoped)
            DB-->>Tenant: rows deleted
        and
            Tenant->>Obj: DELETE prefix tenants/{tenant_id}/
            Obj-->>Tenant: prefix removed
        and
            Tenant->>Search: DELETE partition tenant_id
            Search-->>Tenant: partition removed
        end
        Tenant->>Tenant: Schedule backup-rotation suppression (35-day cycle)
        Tenant->>Sign: sign(destruction_certificate {tenant_id, ts, scope, operator_attestation})
        Sign-->>Tenant: signed certificate
        Tenant->>Audit: APPEND {event: destroy.completed, tenant_id, certificate_hash, ts, hash_chain}
        Tenant->>Notify: emailDestructionCertificate(admin, certificate)
        Notify-->>Admin: Signed destruction certificate (UK GDPR Art. 17 evidence)
        Tenant-->>GW: 200 {certificate_id}
        GW-->>Web: 200
        Web-->>Admin: "Tenant destroyed — certificate sent"
    else Export build failure (DB / Obj error)
        Export->>Audit: APPEND {event: export.failed, tenant_id, reason, ts}
        Export-->>GW: 503 {error: export_failed, support_ref}
        GW-->>Web: 503
        Web-->>Admin: "Export failed — no destruction will run; ticket opened"
        Note over Admin,Audit: Destruction NEVER runs without successful, verified export
    end
```

### 6.3 Notes on Failure Modes

- **Destruction never runs without a successful, verified export** — this is the contractual promise of BR-007 and ADR-007's CI-tested round-trip. Failure to export = abort, ticket, no data loss.
- **Destruction is multi-store and parallelised** (`par` block) — DB, object storage, and search index are destroyed concurrently; backup rotation is scheduled to suppress the next cycle (the residual 35-day backup window is documented in the certificate).
- **The destruction certificate is itself signed** and itself written to the tamper-evident audit chain — so the tenant has crypto-verifiable evidence even after their account is gone, satisfying UK GDPR Article 17 and G-Cloud exit-plan defensibility.
- **Step-up MFA is required** for the destruction call — the gateway re-prompts (irreversible action; ADR-003 step-up flow).

---

## 7. Flow 5 — Audit-Log Query by Tenant Administrator with Signed-Immutable Verification

**Use Case**: Tenant-side governance and incident response.
**Requirements**: FR-012 (tenant-visible audit log), NFR-SEC-004 (immutable audit log), NFR-C-002 (audit retention >= 12 months), NFR-M-001 (observability).
**ADRs**: ADR-001 (tenant_id-scoped query), ADR-005 (OpenTelemetry + tamper-evident hash chain + tenant_id native + UK-resident backend).

### 7.1 Narrative

A tenant administrator opens the Audit Log surface in the web app to investigate a sign-in or to produce evidence for an internal review (or for ICO disclosure). The Audit & Tenant Log Service (C7) serves a tenant_id-scoped slice of the OpenTelemetry-derived audit pipeline. Crucially, every record displayed includes its hash and its prior-record hash; the service can re-compute and verify the chain on demand. If the tenant administrator wants to assert immutability externally (for example, in an investigation), they request a signed export of the queried slice. The service emits a Cosign-signed slice with the chain head + tail hashes, so a third party can verify the slice has not been tampered with after retrieval. The flow itself is audited — querying the audit log is itself an auditable event.

### 7.2 Diagram

```mermaid
sequenceDiagram
    autonumber
    actor Admin as Tenant Admin
    participant Web as Web App (C2)
    participant GW as API Gateway (C1)
    participant AuditSvc as Audit & Tenant Log Service (C7)
    participant OTEL as OTel Backend (UK-resident, ADR-005)
    participant SIEM as Managed SIEM (ADR-005)
    participant Sign as Signing Service (Cosign)
    participant Audit as Audit Pipeline (ADR-005)

    Admin->>Web: Open "Audit Log" → filter (date range, actor, event types)
    Web->>GW: GET /audit?from=...&to=...&filters=... (session cookie)
    Note over GW: Resolve tenant_id from session; require admin scope
    GW->>AuditSvc: query(tenant_id, filters)
    Note over GW,AuditSvc: mTLS, signed service token, tenant_id default-deny
    AuditSvc->>Audit: APPEND {event: audit.queried, tenant_id, actor, filters, ts}
    AuditSvc->>OTEL: SELECT WHERE tenant_id = $1 AND ts BETWEEN ... (tenant_id-native partition)
    OTEL-->>AuditSvc: records (each: prev_hash, payload, hash)

    alt Hash chain verifies
        AuditSvc->>AuditSvc: Re-compute hash chain over returned slice
        AuditSvc-->>GW: 200 {records, chain_head_hash, chain_tail_hash, verified: true}
        GW-->>Web: 200
        Web-->>Admin: Show records with green "Chain verified" badge

        opt Admin requests signed export
            Admin->>Web: Click "Export signed slice"
            Web->>GW: POST /audit/export (filters, format: jsonl)
            GW->>AuditSvc: signSlice(tenant_id, filters)
            AuditSvc->>Sign: sign({records, head_hash, tail_hash, tenant_id, ts})
            Sign-->>AuditSvc: cosign signature + SHA-256
            AuditSvc->>Audit: APPEND {event: audit.signed_export, tenant_id, slice_hash, ts}
            AuditSvc-->>GW: 200 {signed_url, sha256, signature}
            GW-->>Web: 200
            Web-->>Admin: Download signed slice (verifiable by third party)
        end
    else Hash chain breaks (tampering detected)
        AuditSvc->>SIEM: ALERT {severity: critical, tenant_id, gap_at_record_id}
        Note over AuditSvc,SIEM: Suspected tamper or storage corruption — paged 24/7
        AuditSvc->>Audit: APPEND {event: audit.chain_break_detected, tenant_id, ts}
        AuditSvc-->>GW: 500 {error: integrity_check_failed, incident_id}
        GW-->>Web: 500
        Web-->>Admin: "Integrity check failed — incident raised; slice withheld pending forensics"
    end
```

### 7.3 Notes on Failure Modes

- **Hash-chain breaks are never silently masked** — they raise a SIEM alert, an audit-log append (about the break itself), and the slice is **withheld** rather than served. Serving an unverifiable slice would defeat the immutability claim.
- **Querying the audit log is itself audited** (note `audit.queried` and `audit.signed_export` events) — investigators leave a trace, which is itself defence against insider misuse.
- **Tenant_id default-deny** applies even here — an admin of tenant A cannot read records of tenant B. RLS at OTEL backend partitioning level + claim-resolution at the gateway provide defence-in-depth (ADR-001 layered).
- **Signed export uses the same Cosign primitive as ADR-007 export**, deliberately — one signing primitive, two surfaces, one operational discipline.

---

## 8. Component Inventory (Across All Five Flows)

| Component | Container | Responsibility | Anchor |
|-----------|-----------|----------------|--------|
| API Gateway | C1 | OIDC verification, tenant_id resolution, rate-limit, AI-budget, export rate-limit, default-deny | ADR-001, ADR-003, ADR-008 |
| Web Application | C2 | Tenant UI, GOV.UK Design System aligned, WCAG 2.2 AA | FR-013, NFR-C-003 |
| Tenant Service | C3 | Tenant lifecycle, Companies House verification, destruction | FR-001, FR-010, FR-011, INT-003 |
| Project & Artefact Service | C4 | Tenant-scoped project context for AI, RLS-enforced reads | FR-002, FR-005 |
| AI Generation Service | C5 | Provider-agnostic generation, provenance recorder, golden-prompt regression | FR-004, ADR-004 |
| Export Service | C6 | Markdown + JSON + YAML signed tarball, CI-tested round-trip | FR-006, ADR-007 |
| Audit & Tenant Log Service | C7 | Tenant-visible audit slice, hash-chain verification, signed export | FR-012, ADR-005 |
| Notification Service | C9 | Transactional email (verification, export-ready, destruction certificate) | FR-009, FR-010, INT-004 |
| Cell Mgmt Service | C13 | Tenant-to-cell assignment at signup | ADR-001, ADR-006 |
| Vendor IdP / Federated IdP | external | OIDC token issuance, MFA enforcement | ADR-003, INT-001 |
| Companies House API | external | SME company verification | INT-003 |
| AI Sub-Processor | external | UK/EU-resident inference, no-train, contractual DPA | ADR-002, ADR-004 |
| OTel Backend / SIEM | external (UK-resident managed) | Tamper-evident audit chain, tenant_id-native partitioning | ADR-005 |
| Signing Service (Cosign) | shared | Signs export tarball + destruction certificate + audit slice | ADR-007 |

---

## 9. Cross-Diagram Themes

The five sequences share three load-bearing themes that make this architecture defensible at ARB and at NCSC CAF assessment:

1. **`tenant_id` is asserted at every boundary, every time** — at the gateway from the OIDC `tid` claim (Flow 2), on every internal mTLS call, on every database query (RLS), on every object-storage prefix, and on every AI-provider call (Flow 3). Default-deny if missing. Five layers of independently-testable defence.
2. **Audit-log append is non-optional on every state change** — onboarding (Flow 1), authentication (Flow 2), AI generation (Flow 3), export and destruction (Flow 4), and even querying the audit log itself (Flow 5). The hash chain is the integrity backbone; signed exports turn audit data into third-party-verifiable evidence.
3. **Failure modes are explicit and graceful** — every flow has at least one `alt` block with an audited rejection path. Companies House outage does not silently provision tenants; AI outage falls back to manual authoring; export failure aborts destruction; audit chain breaks withhold the slice. NFR-A-003 (graceful degradation) is engineered, not asserted.

---

## 10. Requirements Traceability

| Flow | Use Case | Requirements Covered | ADRs Anchored |
|------|----------|----------------------|---------------|
| 1 — Onboarding | UC-1 | FR-001, FR-010, INT-003, BR-001 | ADR-001, ADR-002, ADR-003, ADR-008 |
| 2 — SSO + MFA | UC-2 prelude (every authenticated request) | FR-007, INT-001, NFR-SEC-001/002/003 | ADR-001, ADR-003, ADR-006 |
| 3 — AI generation | UC-2 | FR-004, FR-005, INT-005, NFR-P-002, NFR-A-003, NFR-SEC-002 | ADR-001, ADR-002, ADR-004, ADR-005, ADR-008 |
| 4 — Export + Exit | UC-3 | FR-006, FR-011, BR-007, NFR-I-002, NFR-C-001, NFR-P-003 | ADR-001, ADR-005, ADR-007 |
| 5 — Audit-log query | tenant-side governance + incident response | FR-012, NFR-SEC-004, NFR-C-002, NFR-M-001 | ADR-001, ADR-005, ADR-007 (Cosign reuse) |

**Coverage gaps deliberately not in this document**: structural views (C4 Context, Container, Deployment) are in DIAG-001 and DIAG-003; data model is in the data-model artefact; threat model is in BLOCKING-01 condition of HLD review.

---

## 11. Integration Points (External Systems)

| External System | Protocol | Direction | SLA / Constraint | Anchor |
|-----------------|----------|-----------|------------------|--------|
| Companies House API | HTTPS / TLS 1.3, JSON | outbound | <= 5s timeout, 3 retries with jitter; manual-review fallback | INT-003, Flow 1 |
| Tenant IdP (vendor or federated OIDC/SAML) | OIDC Authorization Code + PKCE / SAML 2.0 | inbound (browser redirect) + outbound (token endpoint) | MFA required; <= 60min ID token, <= 15min access token | INT-001, ADR-003, Flow 2 |
| AI Sub-Processor | HTTPS / TLS 1.3, JSON streaming, no-train header, mTLS | outbound | UK/EU residency; per-call DPA; quarterly review (ADR-004) | INT-005, Flow 3 |
| OpenTelemetry Backend + SIEM | OTLP over mTLS | outbound (logs/metrics/traces); inbound (queries) | UK-resident; tenant_id-native; tamper-evident chain; >= 12-month retention | ADR-005, Flow 5 |
| Object Storage (managed) | S3 API over TLS | outbound (signed URLs out) | per-tenant prefix policy; 24-hour signed-URL expiry | Flow 4 |
| Email / Notification (transactional) | SMTPS or provider API | outbound | SPF/DKIM/DMARC aligned | INT-004, Flows 1 + 4 |

---

## 12. Security Architecture (Sequence-Level)

| Concern | Where Enforced | Mechanism |
|---------|----------------|-----------|
| Authentication | Gateway (Flow 2) | OIDC verifier, signature + iss + aud + exp + nonce + amr (MFA) |
| Authorisation (tenant scope) | Gateway + Repository layer | tenant_id from `tid` claim; RLS in PostgreSQL; default-deny if missing |
| Service-to-service auth | Inside cell (all flows) | mTLS via service mesh, SPIFFE-style pod identities, short-lived tokens |
| Data-at-rest | DB + object storage + audit backend | KMS-encrypted; per-tenant prefix; tenant_id-native partitions |
| Data-in-transit | Every hop | TLS 1.3 externally, mTLS internally |
| AI sub-processor handling | AIAdaptor (Flow 3) | UK/EU endpoint, no-train header, prompt minimisation, PII redaction at source |
| Export integrity | Export Service (Flow 4) | Cosign signature + SHA-256 manifest + CI-tested round-trip |
| Destruction verifiability | Tenant Service (Flow 4) | Signed destruction certificate; multi-store parallel delete; backup rotation suppression |
| Audit immutability | Audit pipeline (Flow 5) | Tamper-evident hash chain; signed slice export; chain-break = SIEM alert + slice withheld |
| Step-up MFA on destructive actions | Gateway (Flow 4) | Re-prompt before tenant destruction (ADR-003 step-up) |

---

## 13. NFR Coverage in the Sequences

| NFR | Target | How the sequences achieve it |
|-----|--------|------------------------------|
| NFR-P-002 (AI generation latency) | p95 < 30s end-to-end for typical artefact | Streaming response from provider (Flow 3); minimised prompt; tier-based default model |
| NFR-A-003 (graceful degradation) | Service continues without AI | Flow 3 falls back to manual authoring on provider failure; budget refund issued |
| NFR-SEC-001 (MFA) | MFA on write actions; phishing-resistant for operators | Flow 2 requires `amr` MFA assertion; Flow 4 step-up MFA; operators on separate IdP (ADR-003) |
| NFR-SEC-002 (tenant isolation) | Cross-tenant access architecturally impossible | tenant_id propagated and enforced in every flow; RLS; default-deny |
| NFR-SEC-004 (immutable audit log) | Tamper-evident; tenant-visible | Flow 5 hash-chain re-verify on read; chain-break = withhold |
| NFR-C-001 (UK GDPR) | Lawful basis, residency, Articles 17/20 | Flow 4 signed export (Article 20) + signed destruction certificate (Article 17) |
| NFR-C-002 (audit retention) | >= 12 months | ADR-005 backend; Flow 5 |
| NFR-I-002 (open-format round-trip) | CI-tested | Flow 4 — Markdown + JSON manifest + YAML lineage tarball, signed |
| NFR-P-003 (export performance) | Bounded by tenant data volume | Flow 4 streams from DB and object store; signed URL avoids re-streaming on download |

---

## 14. UK Government Compliance Anchors

| Compliance Item | Where Visible |
|-----------------|---------------|
| GDS Service Standard Point 9 (security) | Flow 2 (MFA), Flow 4 (verifiable destruction), Flow 5 (immutable audit) |
| TCoP Point 5 (Cloud First) | UK-resident managed services across all flows (ADR-002, ADR-005) |
| TCoP Point 8 (Share & Reuse) | Same Cosign primitive used for export and audit-slice signing (Flows 4 + 5) |
| AI Playbook (transparency, accountability) | Flow 3 — provenance metadata recorded before user sees draft; ATRS evidence asset |
| AI Playbook (human-in-the-loop) | Flow 3 — draft offered for human review (FR-002), never auto-saved |
| NCSC CAF (B3 Data Security, B5 Resilient Networks) | mTLS + tenant_id propagation (all flows); tamper-evident audit (Flow 5) |
| UK GDPR Article 17 (erasure) | Flow 4 — signed destruction certificate |
| UK GDPR Article 20 (portability) | Flow 4 — open-format signed export |
| Companies House verification | Flow 1 — INT-003, fraud-prevention gate |

---

## 15. Quality Gate (Per-Diagram)

| # | Criterion | Target | Result | Status |
|---|-----------|--------|--------|--------|
| 1 | Edge crossings | minimal for sequence (lifelines linear) | 0 — no edge crossings (sequence is inherently top-to-bottom) | PASS |
| 2 | Visual hierarchy | actor leftmost, external systems rightmost | actor placed first; externals (CH, IdP, AI Provider, OTel, Cosign) on right | PASS |
| 3 | Grouping | related lifelines proximate | gateway adjacent to verifier; storage stores adjacent in Flow 4 | PASS |
| 4 | Flow direction | top-to-bottom (sequence default) | consistent | PASS |
| 5 | Relationship traceability | each arrow source → target unambiguous | yes; no overlapping arrows | PASS |
| 6 | Abstraction level | one interaction scope per diagram | each flow is one use case | PASS |
| 7 | Edge label readability | labels concise, no overlap | labels limited to method + key params | PASS |
| 8 | Node placement | connected lifelines adjacent | adjacency reflects call sequence | PASS |
| 9 | Element count | <= 8 lifelines per diagram (Step 5b threshold) | Flow 1: 9, Flow 2: 6, Flow 3: 9, Flow 4: 10, Flow 5: 7 | PARTIAL — Flows 1, 3, 4 exceed by 1–2 lifelines |

**Accepted trade-off on element count**: Flows 1, 3, and 4 use 9–10 lifelines each instead of the recommended <= 8. Splitting these would obscure the cross-cutting invariant (audit-log append on every state change must be visible alongside the primary flow, not factored into a sub-diagram). Each extra lifeline (Audit, Notify, Sign, Cell) carries one specific architectural promise; removing it would weaken the diagram's evidentiary value at ARB and at NCSC CAF assessment. The diagrams remain readable on a 1080p screen and on a printed A3 page.

---

## 16. Linked Artefacts

- **Requirements**: `projects/001-arckit-saas/ARC-001-REQ-v1.0.md` (UC-1, UC-2, UC-3, FR-001..015, NFR-*).
- **HLD**: `projects/001-arckit-saas/ARC-001-HLDR-v1.0.md` (Section 3.2 container layer; Section 3.3 component layer).
- **ADR-001**: `projects/001-arckit-saas/decisions/ARC-001-ADR-001-v1.0.md` (Tenant isolation, tenant_id propagation).
- **ADR-002**: `projects/001-arckit-saas/decisions/ARC-001-ADR-002-v1.0.md` (UK residency).
- **ADR-003**: `projects/001-arckit-saas/decisions/ARC-001-ADR-003-v1.0.md` (Identity & SSO).
- **ADR-004**: `projects/001-arckit-saas/decisions/ARC-001-ADR-004-v1.0.md` (AI provider abstraction).
- **ADR-005**: `projects/001-arckit-saas/decisions/ARC-001-ADR-005-v1.0.md` (Observability & audit).
- **ADR-006**: `projects/001-arckit-saas/decisions/ARC-001-ADR-006-v1.0.md` (Managed Kubernetes, mTLS).
- **ADR-007**: `projects/001-arckit-saas/decisions/ARC-001-ADR-007-v1.0.md` (Data portability & exit).
- **ADR-008**: `projects/001-arckit-saas/decisions/ARC-001-ADR-008-v1.0.md` (Tier quotas).
- **DPIA**: `projects/001-arckit-saas/ARC-001-DPIA-v1.0.md` (cross-references Flow 4 destruction, Flow 5 audit).
- **Companion diagrams**: ARC-001-DIAG-001 (C4 Context + Container — to be created); ARC-001-DIAG-003 (Deployment — to be created).

---

## 17. Next Steps

- Cross-validate Flow 1 against Companies House API rate-limits at pilot scale.
- Cross-validate Flow 3 with the AI sub-processor's mTLS and no-train header on the actual provider — ADR-004 is provider-agnostic but pilot must prove it on at least two.
- Lock the JSON manifest schema in Flow 4 — currently described in ADR-007; needs an OpenAPI-style schema artefact in DLD.
- Add a sixth flow (deferred) for **break-glass operator action** — separate IdP, hardware-key MFA, SIEM-alerted audit append (covered by ADR-003 + ADR-005 but not yet drawn).
- Re-run quality gate after DLD when component-level naming may shift.

---

**Generated by**: ArcKit `/arckit:diagram` command
**Generated on**: 2026-05-03 GMT
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Project 001)
**AI Model**: claude-opus-4-7 (1M context)
**Generation Context**: Synthesised from ARC-001-HLDR-v1.0 (Section 3.2/3.3 container + component), ARC-001-REQ-v1.0 (UC-1/2/3, FR-001/004/006/007/011/012, NFR-SEC/C/I/P/A), and ADR-001/002/003/004/005/006/007/008. Five Mermaid sequence diagrams covering the load-bearing interaction flows of the ArcKit SaaS pre-GA Alpha.
