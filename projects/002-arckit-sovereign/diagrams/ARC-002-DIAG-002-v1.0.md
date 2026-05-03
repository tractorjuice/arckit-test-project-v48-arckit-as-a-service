# Sequence Diagrams — Sovereign-Specific Interaction Flows

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:diagram`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-DIAG-002-v1.0 |
| **Document Type** | Architecture Diagrams (Sequence) |
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
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:diagram` command. Five sovereign-specific Mermaid sequence diagrams covering bundle-issue-and-verification, JIT elevation, on-prem AI flow, on-site break-glass, and Critical-CVE hotfix flow. Anchored on `ARC-002-HLD-v1.0.md` and ADR-002 / -003 / -004 / -007 / -008. | [PENDING] | [PENDING] |

---

## 1. Document Purpose

This document captures five **sovereign-specific** sequence diagrams that visualise interaction flows distinctive to the air-gapped deployment route (project 002). They complement the C4 / Network DFD / general use-case sequences delivered in ARC-002-DIAG-001 and ARC-002-DIAG-003 by zooming in on flows that have no SaaS equivalent (or that diverge materially from their SaaS counterpart).

The five flows are:

1. **Bundle issue → distribution → customer-side verification ceremony** (anchors: ADR-002, ADR-007).
2. **Cleared-personnel JIT elevation with peer approval and hash-chained audit** (anchor: ADR-003).
3. **AI-assisted artefact generation against an on-premise model endpoint inside the accredited boundary** (anchor: ADR-004).
4. **Customer break-glass on-site procedure with two-person sealed-credential opening** (anchor: ADR-003 §5 Option 2 step 5).
5. **Critical CVE hotfix issue → distribution → customer apply within 7-day SLA** (anchors: ADR-008, ADR-007, ADR-002).

Each diagram is preceded by a brief narrative and followed by an `alt` failure-mode commentary so that adverse paths (signature mismatch, peer approver unavailable, model down, break-glass trigger, hotfix verification failure) are visible inline rather than buried in prose.

---

## 2. Conventions and Notation

- All diagrams use Mermaid `sequenceDiagram` syntax (rendered by GitHub, GitLab, Mermaid Live, and the ArcKit `/arckit:pages` site).
- Lifelines named with their architectural role (Vendor Build, Customer Operator, Customer IdP, etc.) rather than persons.
- `Note over` blocks carry classification and trust-boundary annotations.
- `alt` / `else` blocks express failure modes; `opt` blocks express opt-in behaviour (e.g., FR-013 vendor remote-support); `loop` blocks express repeated steps where used.
- The thick dotted line `==>` is used inside narrative to represent crossing the customer accreditation boundary; in Mermaid sequence syntax we use a `Note over` to mark the boundary because Mermaid does not natively render trust boundaries.
- Every flow ends with the audit emission step (FR-010) so the audit trail is visible end-to-end.

---

## 3. Flow 1 — Bundle Issue, Distribution, and Customer-Side Verification Ceremony

**Anchored on**: ADR-002 (signed bundle, OVM, SLSA L3), ADR-007 (sealed encrypted media + diode option + verification ceremony), HLD §5.5 / §6.2.

**Actors**:

- **Vendor Build CI** — hardened SLSA L3 GitHub-Actions runner that produces the bundle.
- **Vendor HSM** — HMG-CAPS / FIPS 140-2 L3 HSM under M-of-N custody, used only for the OVM signature.
- **Public Rekor** — Sigstore transparency log (used where classification permits; bypassed in `ovm-only` profile).
- **Vendor Dispatch Facility** — controlled-access dispatch room (CCTV, named personnel) writing dual sealed encrypted media.
- **Approved Courier / Diode Operator** — defence-cleared courier for sealed media OR customer-side diode operator if Option 2.
- **Customer Operator A** and **Operator B** — two-person rule for the on-site ceremony.
- **`arckit-verify` CLI** — vendored static binary that performs offline verification; refuses on any check failure.
- **Customer Audit (SIEM)** — customer-controlled SIEM destination receiving the receipt + verification audit events (FR-010).

**Narrative**: A new release (or LTS patch) is built reproducibly; the bundle is hashed, signed keyless, SLSA-L3-attested, and wrapped in an HSM-signed Offline Verification Manifest (OVM). Dual sealed media are produced and dispatched on independent routes. An out-of-band signature manifest is issued by an independent channel. At the customer site, two cleared operators verify seals, run `arckit-verify` fully offline, and the install proceeds only if every check passes. Failure modes — seal serial mismatch, OVM signature mismatch, artefact digest mismatch, SLSA chain failure — each refuse the install and emit a tamper alert.

```mermaid
sequenceDiagram
    autonumber
    participant CI as Vendor Build CI<br/>(SLSA L3 hardened runner)
    participant HSM as Vendor HSM<br/>(HMG-CAPS, M-of-N)
    participant Rekor as Public Rekor<br/>(transparency log, optional)
    participant Disp as Vendor Dispatch Facility
    participant Courier as Approved Courier<br/>/ Diode Operator
    participant OpA as Customer Operator A
    participant OpB as Customer Operator B
    participant Verify as arckit-verify CLI<br/>(static, offline, in-bundle)
    participant SIEM as Customer SIEM<br/>(audit, FR-010)

    Note over CI,HSM: Vendor side — outside customer boundary
    CI->>CI: Build OCI images from tagged source revision
    CI->>CI: Reproducibility cross-build (second runner, hashes must match)
    CI->>CI: Syft scan -> CycloneDX 1.5 + SPDX 2.3
    CI->>CI: cosign sign --keyless (Fulcio short-lived cert)
    opt Transparency profile = rekor+ovm (classification permits)
        CI->>Rekor: Submit signature; receive inclusion proof
        Rekor-->>CI: Rekor inclusion proof
    end
    CI->>CI: slsa-github-generator -> SLSA L3 provenance
    CI->>CI: Assemble OVM body (digests, SBOMs, provenance, Rekor proofs, trust-root snapshots)
    CI->>HSM: Submit OVM body for HSM signing (M-of-N approval gate)
    HSM-->>CI: HSM-signed OVM (RSA-PSS-4096-SHA512 or ECDSA P-384)
    CI->>Disp: Bundle (artefacts + OVM + arckit-verify static binary + IaC)

    Note over Disp,Courier: Vendor dispatch ceremony — controlled facility
    Disp->>Disp: Write to TWO independent encrypted media (primary + verification copy)
    Disp->>Disp: Tamper-evident seals applied; serials logged
    Disp->>Courier: Dispatch under signed Chain-of-Custody form (separate routes)
    Disp-->>OpA: Out-of-band signature manifest (signed email / portal):<br/>media serials, SHA-256/512, key fingerprints

    Note over OpA,Verify: ===== Customer accreditation boundary =====
    Courier->>OpA: Sealed media delivered
    OpA->>OpA: Receipt logged; CoC counter-signed
    OpA->>OpB: Two-person rule invoked
    OpA->>OpB: Compare seal serials to out-of-band manifest

    alt Seal serial mismatch OR tamper-evident seal broken
        OpA->>SIEM: TAMPER_ALERT event (FR-010)
        OpA->>Disp: Reject delivery; quarantine media
        Note over OpA,Disp: Install does not proceed; vendor incident raised
    else Seals intact and serials match
        OpA->>Verify: arckit-verify ./bundle --hsm-cert <pinned>
        Verify->>Verify: Verify OVM HSM signature (offline)
        alt OVM HSM signature invalid
            Verify-->>OpA: FAIL_HSM_SIG
            OpA->>SIEM: VERIFY_FAIL_HSM_SIG event
            Note over Verify,OpA: Install refuses to start (FR-001)
        else OVM HSM signature valid
            Verify->>Verify: Verify every artefact SHA-256 + SHA-512
            alt Any artefact digest mismatch
                Verify-->>OpA: FAIL_DIGEST
                OpA->>SIEM: VERIFY_FAIL_DIGEST event
                Note over Verify,OpA: Install refuses to start
            else All digests match
                Verify->>Verify: Validate embedded SLSA L3 + Rekor inclusion proof OFFLINE<br/>(against snapshotted Fulcio root + Rekor pubkey)
                alt SLSA / Rekor offline chain invalid
                    Verify-->>OpA: FAIL_PROVENANCE
                    OpA->>SIEM: VERIFY_FAIL_PROVENANCE event
                    Note over Verify,OpA: Install refuses to start
                else Chain valid
                    Verify-->>OpA: ALL_PASS (verification < 60s p95)
                    OpA->>OpB: Co-sign install authorisation
                    OpA->>SIEM: BUNDLE_VERIFIED event (release_id, sha512, ovm_id)
                    Note over OpA,SIEM: Install proceeds via IaC bundled in package
                end
            end
        end
    end
```

**Failure-mode coverage**:

| Failure | Detection point | Response |
|---------|-----------------|----------|
| Seal tampered en route | OpA + OpB visual + serial check | Reject; quarantine; vendor incident (R-ADR7-3 in ADR-007) |
| OVM HSM signature mismatch | `arckit-verify` step 1 | Install refuses; SIEM `VERIFY_FAIL_HSM_SIG` |
| Artefact digest mismatch | `arckit-verify` step 2 | Install refuses; SIEM `VERIFY_FAIL_DIGEST` |
| SLSA / Rekor offline chain failure | `arckit-verify` step 3 | Install refuses; SIEM `VERIFY_FAIL_PROVENANCE` |
| Out-of-band manifest channel compromised | Independent HSM-signed manifest verified against pinned vendor public key | Manifest signature check fails; ceremony refuses (R-ADR7-4) |

---

## 4. Flow 2 — Cleared-Personnel JIT Elevation With Peer Approval

**Anchored on**: ADR-003 §5 Option 2 step 3 (JIT elevation), §5 Option 2 step 6 (audit), HLD §6.2.

**Actors**:

- **Operator (Requester)** — cleared operator with the standing `Operator` role (e.g., SC-cleared).
- **Operator (Approver)** — second cleared operator drawn from the JIT-approver pool (must be at or above the requester's clearance attribute).
- **Customer IdP** — OIDC / SAML provider; authoritative source of the typed `clearance_attribute` claim.
- **ArcKit Web UI** — browser-based, no client agent, customer-IdP-authenticated.
- **JIT Elevation Service** — first-party component issuing time-boxed elevated role grants.
- **Audit Pipeline** — hash-chained, append-only emitter to customer SIEM.
- **Customer SIEM** — customer-controlled audit destination.

**Narrative**: A privileged operation (e.g., classification-ceiling change, key rotation, audit-purge boundary) is requested. The system requires a JIT elevation. The requester logs in via the customer IdP, asserts a `reason-for-access`, and the request is queued. A second cleared operator approves with a co-signed reason; the system issues an `Operator-Privileged` role for a configured TTL (default 30 min, max 4 h); auto-revokes; every step is hash-chained to the customer SIEM. JIT elevation never grants a role above the clearance the requester's IdP claim permits.

```mermaid
sequenceDiagram
    autonumber
    participant Req as Operator (Requester)<br/>standing role: Operator (SC)
    participant App as Operator (Approver)<br/>pool member (>= SC)
    participant IdP as Customer IdP<br/>(OIDC/SAML, INT-001)
    participant UI as ArcKit Web UI
    participant JIT as JIT Elevation Service
    participant Audit as Audit Pipeline<br/>(hash-chained)
    participant SIEM as Customer SIEM<br/>(FR-010, INT-004)

    Req->>UI: Initiate privileged operation (e.g., key rotation)
    UI->>UI: Detect role gap: requires Operator-Privileged
    UI->>Req: Prompt for elevation: reason-for-access + requested TTL
    Req->>UI: Submit reason + TTL (<= 4h)
    UI->>JIT: POST /elevation/request {subject, op, reason, ttl}
    JIT->>IdP: Validate session + read clearance_attribute claim

    alt clearance_attribute absent OR below required floor
        IdP-->>JIT: clearance insufficient
        JIT-->>UI: 403 clearance_floor_not_met
        JIT->>Audit: ELEVATION_DENIED_CLEARANCE event
        Audit->>SIEM: hash-chain append
        Note over JIT,UI: No elevation granted; user sees standard error
    else clearance_attribute present and at/above floor
        IdP-->>JIT: clearance OK
        JIT->>Audit: ELEVATION_REQUESTED event (request_id, requester, op, reason)
        Audit->>SIEM: hash-chain append
        JIT->>App: Notify approver pool (web UI inbox + optional email)

        alt No approver responds within 15 min (configurable)
            JIT-->>UI: 408 elevation_timeout
            JIT->>Audit: ELEVATION_TIMEOUT event
            Audit->>SIEM: hash-chain append
            Note over JIT,Req: Requester re-queues OR escalates to break-glass<br/>(see Flow 4) if genuinely urgent
        else Approver picks up request
            App->>UI: Open elevation request review
            UI->>JIT: GET /elevation/request/{request_id}
            JIT-->>UI: request body (op, reason, requester clearance)
            App->>App: Verify reason, requester identity, op scope
            alt Approver rejects (insufficient justification)
                App->>JIT: POST /elevation/reject {reason}
                JIT-->>UI: elevation_rejected
                JIT->>Audit: ELEVATION_REJECTED event (approver, reason)
                Audit->>SIEM: hash-chain append
            else Approver approves with co-signed reason
                App->>JIT: POST /elevation/approve {co_signed_reason}
                JIT->>JIT: Mint Operator-Privileged role grant (TTL bound)
                JIT->>Audit: ELEVATION_GRANTED event (request_id, approver, ttl_expiry)
                Audit->>SIEM: hash-chain append
                JIT-->>UI: elevation_granted (session-scoped capability token)
                UI->>Req: Privileged operation now permitted
                Req->>UI: Execute the operation (within TTL)
                UI->>Audit: PRIVILEGED_OP_EXECUTED event (op, sub-resource refs)
                Audit->>SIEM: hash-chain append

                Note over JIT,Audit: TTL expiry timer running
                JIT->>JIT: Auto-revoke role at TTL expiry
                JIT->>Audit: ELEVATION_EXPIRED event
                Audit->>SIEM: hash-chain append
            end
        end
    end
```

**Failure-mode coverage**:

| Failure | Detection point | Response |
|---------|-----------------|----------|
| `clearance_attribute` claim missing or below floor | JIT validation step | `403 clearance_floor_not_met`; SIEM `ELEVATION_DENIED_CLEARANCE`; no elevation |
| No approver available (e.g., out-of-hours) | 15-min approval timeout | `408 elevation_timeout`; SIEM `ELEVATION_TIMEOUT`; user may escalate to break-glass (Flow 4) only if genuinely urgent |
| Approver rejects | Approver review | `elevation_rejected`; SIEM `ELEVATION_REJECTED` with reason |
| Privileged op outlives TTL | Auto-revoke timer | Role removed mid-session; in-flight operation completes; new attempt requires new elevation |
| Hash-chain integrity broken (covert log tamper) | SIEM-side chain validation (operator-side, not depicted) | Customer-side incident; SIEM raises chain-break alarm |

---

## 5. Flow 3 — AI-Assisted Artefact Generation Against On-Premise Model Endpoint

**Anchored on**: ADR-004 §5 Option 1 (`AIAdaptor` reuse, OpenAI-compatible wire contract, fail-closed default, install-time validator refuses public hostnames), HLD §5.3 / §5.5.

**Actors**:

- **Author (User)** — cleared user with `Author` standing role, generating an artefact via an AI-assisted template.
- **ArcKit Web UI** — same code as SaaS; renders streaming generation via SSE.
- **AI Adaptor** — provider-agnostic interface (parent: project 001 ADR-004); sovereign profile is `customer-endpoint`.
- **Customer KMS** — holds bearer token / mTLS material referenced by `ai.endpoint.auth` (INT-007).
- **Customer Internal CA** — issues TLS for the AI endpoint (INT-003).
- **Customer AI Endpoint** — TGI / vLLM / Triton serving stack hosting the customer's accredited open-weight model, RFC1918 only.
- **Audit Pipeline** + **Customer SIEM** — emits prompt-shape, model name, latency, outcome (full prompt content NOT logged by default).

**Narrative**: At install, the validator confirmed `ai.endpoint.url` resolves to RFC1918 / customer-internal and `ai.classification_max` is set; the bundle's network-deny test confirmed the AI flow makes no other outbound calls. An `Author` invokes an AI-assisted template; the adaptor scopes prompt context by project / role / community-of-interest (FR-006); calls the customer endpoint over OpenAI-compatible chat-completions; streams back via SSE; emits a provenance record identical in shape to the SaaS. If the model is down, the UI fails-closed with a `503 ai_unavailable` and manual authoring continues.

```mermaid
sequenceDiagram
    autonumber
    participant Author as Author (User)<br/>standing role: Author
    participant UI as ArcKit Web UI
    participant Adapt as AI Adaptor<br/>(provider: customer-endpoint)
    participant KMS as Customer KMS<br/>(INT-007)
    participant CA as Customer Internal CA<br/>(INT-003)
    participant AI as Customer AI Endpoint<br/>(TGI / vLLM / Triton, RFC1918)
    participant Audit as Audit Pipeline
    participant SIEM as Customer SIEM

    Note over UI,AI: All endpoints inside customer accreditation boundary; zero outbound calls
    Author->>UI: Open AI-assisted template (e.g., requirements draft)
    UI->>UI: Check ai.provider config

    alt ai.provider = none (default sovereign install)
        UI-->>Author: AI features disabled banner; manual authoring fully available (NFR-A-003)
    else ai.provider = customer-endpoint
        Author->>UI: Submit prompt variables (template_id + context refs)
        UI->>Adapt: generateStream(template_id, vars, scope={project, role, CoI})
        Adapt->>Adapt: Apply within-deployment isolation (FR-006, NFR-SEC-006)
        Adapt->>Adapt: Check ai.classification_max ceiling against artefact classification
        alt Artefact classification > ai.classification_max
            Adapt-->>UI: 403 ai_classification_blocked
            UI-->>Author: AI disabled for this artefact at this classification
            Adapt->>Audit: AI_BLOCKED_CLASSIFICATION event
            Audit->>SIEM: append
        else Within ceiling
            Adapt->>KMS: Fetch bearer / mTLS material (per ai.endpoint.auth.kind)
            KMS-->>Adapt: credential reference (short-lived where possible)
            Adapt->>CA: Resolve TLS trust against customer CA bundle
            CA-->>Adapt: trust chain
            Adapt->>AI: POST /v1/chat/completions (stream=true, model=ai.model.name)<br/>over mTLS or bearer

            alt AI endpoint timeout (> ai.timeout_ms) OR connection refused
                AI-->>Adapt: timeout / connection error
                Adapt-->>UI: 503 ai_unavailable
                UI-->>Author: "AI is currently unavailable; manual authoring remains available"
                Adapt->>Audit: AI_CALL_FAILED event (model, latency, error_class)
                Audit->>SIEM: append
                Note over UI,Author: Fail-closed; user falls back to manual<br/>(P-3, NFR-A-003)
            else AI returns stream
                loop SSE chunks
                    AI-->>Adapt: data: {delta}
                    Adapt-->>UI: SSE chunk
                    UI-->>Author: streamed token render
                end
                AI-->>Adapt: data: [DONE] + usage tokens
                Adapt->>Adapt: Build provenance record (model, version, timestamp, template_id,<br/>deployment_id, project_id, user_id) — schema parity with SaaS
                Adapt-->>UI: Final artefact draft + provenance
                UI->>Author: Render draft with AI-generated banner + provenance link
                Adapt->>Audit: AI_CALL_OK event (template_id, prompt_token_count,<br/>completion_token_count, latency_ms, model.name)
                Note right of Adapt: Full prompt content NOT logged by default<br/>(operator-opt-in retention only)
                Audit->>SIEM: append
            end
        end
    end
```

**Failure-mode coverage**:

| Failure | Detection point | Response |
|---------|-----------------|----------|
| `ai.provider = none` (default) | UI provider check | AI features disabled; manual authoring intact (NFR-A-003) |
| Artefact classification exceeds `ai.classification_max` | Adaptor entry | `403 ai_classification_blocked`; SIEM event |
| KMS / CA material unavailable | Adaptor pre-flight | `503 ai_unavailable`; same fail-closed UX |
| AI endpoint down or > `ai.timeout_ms` | Adaptor timeout | `503 ai_unavailable`; SIEM `AI_CALL_FAILED`; fail-closed (Principle 21 fail-closed default) |
| Public hostname configured by mistake (post-install) | Network-deny test in CI + install-time validator | Refuses to start; Principle 21 §validation gate |
| Model below minimum spec (parameter / context) | Install-time warning + admin acknowledgement (audited) | Operates with logged caveat; quality may degrade |

---

## 6. Flow 4 — Customer Break-Glass On-Site Procedure (Two-Person Sealed-Credential Opening)

**Anchored on**: ADR-003 §5 Option 2 step 5 (break-glass, on-site only, two-person, sealed credentials in two physically separate safes), HLD §6.2.

**Actors**:

- **Operator A** and **Operator B** — both cleared and physically present at the host inside the boundary.
- **Safe 1** and **Safe 2** — two physically separate safes inside the boundary, each holding one half of the break-glass credential (split-secret or M-of-N). HSM-backed where available, paper-and-tamper-seal where SAL prescribes.
- **Authorised Workstation** — workstation inside the boundary with the necessary clearance posture.
- **ArcKit Host** — the deployed system; accepts break-glass only when both halves are presented.
- **Audit Pipeline** + **Customer SIEM** — captures activation, every command, and post-incident review (FR-010).
- **Customer SIRO / DSO (post-incident)** — receives the mandatory post-incident review before re-sealing.

**Narrative**: Normal access has failed (e.g., IdP outage, JIT approver pool exhausted during a genuine incident, fundamental config error). Two cleared operators each retrieve one half of the break-glass credential from physically separate safes, attest the seal integrity of both halves, present both halves at the host's authorised workstation, and the system grants a constrained break-glass session. Every command in the session is recorded to customer SIEM. After the incident, a post-incident review with SIRO/DSO is mandatory before either safe is re-sealed; credentials are rotated immediately. Vendor staff cannot trigger break-glass.

```mermaid
sequenceDiagram
    autonumber
    participant OpA as Operator A (cleared, on-site)
    participant OpB as Operator B (cleared, on-site)
    participant Safe1 as Safe 1 (Boundary-internal)
    participant Safe2 as Safe 2 (Boundary-internal)
    participant Wks as Authorised Workstation<br/>(inside boundary)
    participant Host as ArcKit Host
    participant Audit as Audit Pipeline
    participant SIEM as Customer SIEM
    participant SIRO as Customer SIRO / DSO<br/>(post-incident review)

    Note over OpA,Host: Trigger: normal access fails (IdP outage, approver pool exhausted, config breakage)
    OpA->>OpA: Confirm trigger meets break-glass policy threshold
    OpA->>OpB: Two-person rule invoked; co-witness break-glass activation

    par Retrieve credential halves from physically separate safes
        OpA->>Safe1: Open Safe 1 (audited, CCTV)
        Safe1-->>OpA: Sealed envelope / HSM token (half A)
        OpA->>OpA: Inspect tamper seal; record serial
    and
        OpB->>Safe2: Open Safe 2 (audited, CCTV)
        Safe2-->>OpB: Sealed envelope / HSM token (half B)
        OpB->>OpB: Inspect tamper seal; record serial
    end

    alt Either seal broken / serial mismatch
        OpA->>SIEM: BREAK_GLASS_TAMPER_SUSPECTED event
        OpA->>SIRO: Immediate escalation; abort break-glass
        Note over OpA,SIRO: Abort; SIRO runs incident; credentials rotated;<br/>no system access via this path
    else Both seals intact and serials valid
        OpA->>Wks: Login (workstation has standing clearance posture)
        OpB->>Wks: Co-witness; both present at console
        OpA->>Host: Submit half A
        OpB->>Host: Submit half B
        Host->>Host: Combine halves; validate against break-glass policy

        alt Halves do not combine (corrupt, expired, wrong release)
            Host-->>OpA: BREAK_GLASS_REJECTED
            Host->>Audit: BREAK_GLASS_REJECTED event (cause)
            Audit->>SIEM: append
            OpA->>SIRO: Escalate; treat as suspected compromise
        else Halves combine and policy satisfied
            Host->>Host: Open break-glass session (TTL <= configured, e.g., 60 min)
            Host->>Audit: BREAK_GLASS_ACTIVATED event (operators, reason, TTL)
            Audit->>SIEM: append (with full session-recording start marker)
            loop Every command issued in break-glass session
                OpA->>Host: command
                Host->>Audit: BG_CMD event (cmd, args-hash, exit_code)
                Audit->>SIEM: append
            end
            Host->>Host: TTL expires OR operators close session
            Host->>Audit: BREAK_GLASS_CLOSED event (duration, command_count)
            Audit->>SIEM: append + session-recording end marker

            Note over OpA,SIRO: Mandatory post-incident review BEFORE re-sealing
            OpA->>SIRO: Submit incident report + session recording
            OpB->>SIRO: Co-sign incident report
            SIRO->>SIRO: Review; confirm policy compliance
            SIRO->>OpA: Authorise credential rotation + re-seal

            par Rotate and re-seal both halves
                OpA->>Safe1: Place new sealed half A; record new serial
            and
                OpB->>Safe2: Place new sealed half B; record new serial
            end
            OpA->>Audit: BREAK_GLASS_RESEALED event (new serials, rotation_id)
            Audit->>SIEM: append
        end
    end

    Note over Host,SIEM: Vendor staff CANNOT trigger break-glass at any step (ADR-003)
```

**Failure-mode coverage**:

| Failure | Detection point | Response |
|---------|-----------------|----------|
| Either seal broken or serial mismatch | OpA / OpB visual + serial check | Abort; SIEM `BREAK_GLASS_TAMPER_SUSPECTED`; SIRO incident |
| Halves fail to combine (corruption, expired) | Host policy validation | `BREAK_GLASS_REJECTED`; treated as suspected compromise |
| Single-person attempt (e.g., OpB unavailable) | Two-person rule enforced at host | Refused; standard JIT path (Flow 2) is the next-best option |
| Vendor-side attempted activation (e.g., via FR-013 channel) | Host policy: break-glass not exposed remotely | Always refused regardless of session origin |
| Re-seal skipped post-incident | SIRO sign-off gate | Site cannot return to normal access state until re-seal logged |

---

## 7. Flow 5 — Critical CVE Hotfix Issue, Distribution, and Customer Apply (within 7-day NFR-SEC-008 SLA)

**Anchored on**: ADR-008 §5 Option 2 (LTS line, monthly cadence + out-of-band Critical 7d / High 30d / Medium 90d), ADR-007 (sealed media + diode default channels), ADR-002 (signing reused).

**Actors**:

- **NCSC / Security Researcher / Internal Triage** — vulnerability inbound (ISO 29147 / NCSC vulnerability disclosure, INT-010).
- **Vendor Security Lead** — triages CVSS, declares Critical severity.
- **LTS Engineering Lead + Backport Engineer** — produces backport against the affected LTS line.
- **LTS CI** — full test suite incl. disconnected/offline profile and air-gap install/upgrade/roll-back tests.
- **Vendor HSM** — same OVM signing path as full release (reused per ADR-002).
- **Vendor Dispatch / Diode** — same channels as ADR-007; bias toward diode where the customer has one (lowest latency).
- **Customer Operator A + B** — same two-person ceremony.
- **`arckit-verify` CLI** — same offline verifier.
- **ArcKit Host** — applies the patch bundle without full re-deploy (FR-014).
- **Customer SIEM** — patch-applied audit event.

**Narrative**: A Critical CVE is reported. The vendor triages within 24 h, the Backport Engineer cherry-picks the fix to each currently-supported LTS line, the LTS CI runs the full air-gap test suite, the OVM is signed identically to a full release, and the bundle is dispatched on the diode (where the customer has one) or as sealed media (default fallback). At the customer site, the ceremony is the same as Flow 1 (`arckit-verify`), but install applies the patch via FR-014 without a full re-deploy and without re-accreditation (LTS hotfix scope per ADR-008 backport policy). Failure modes (verify failure, broken backport, diode outage) each fall back to a defined alternative.

```mermaid
sequenceDiagram
    autonumber
    participant Reporter as NCSC / Researcher / Internal<br/>(INT-010 inbound)
    participant SecLead as Vendor Security Lead
    participant BPE as LTS Backport Engineer
    participant LTSci as LTS CI<br/>(disconnected profile + air-gap tests)
    participant HSM as Vendor HSM<br/>(M-of-N)
    participant Disp as Vendor Dispatch / Diode Operator
    participant OpA as Customer Operator A
    participant OpB as Customer Operator B
    participant Verify as arckit-verify CLI
    participant Host as ArcKit Host
    participant SIEM as Customer SIEM

    Note over Reporter,SIEM: NFR-SEC-008 SLA: Critical = 7 days from disclosure to customer-applied
    Reporter->>SecLead: CVE submission (reproducer + impact)
    SecLead->>SecLead: Triage; CVSS scoring; severity = CRITICAL
    SecLead->>BPE: Authorise Critical hotfix backport against currently-supported LTS lines (max 2)
    BPE->>BPE: Cherry-pick fix; minimal-change patch (no schema/API drift, ADR-008)
    BPE->>LTSci: Push backport branch -> CI pipeline
    LTSci->>LTSci: Full test suite incl. network-deny + air-gap install/upgrade/rollback
    alt LTS CI fails on backport (regression / non-determinism)
        LTSci-->>BPE: FAIL
        BPE->>BPE: Re-engineer backport
        Note over BPE,LTSci: Loop back to backport step;<br/>SLA clock continues running
    else LTS CI passes (incl. reproducibility cross-build)
        LTSci->>LTSci: cosign keyless sign + SLSA L3 + SBOM (CycloneDX + SPDX)
        LTSci->>HSM: OVM signing job (M-of-N; same path as full release per ADR-002)
        HSM-->>LTSci: HSM-signed OVM
        LTSci->>LTSci: Build patch bundle <name>-LTS-<N>.<patch.M> (FR-014, signed identically)
        LTSci->>Disp: Patch bundle ready for dispatch
        LTSci-->>SecLead: Advisory feed entry (signed text); ready for dispatch

        par Channel selection per customer (ADR-007)
            Disp->>Disp: Customer has diode? (lowest latency, minutes)
            Note right of Disp: Choose diode where available;<br/>else dual sealed-media courier (48-72h)
        end

        alt Diode channel outage on chosen path
            Disp->>Disp: Failover to sealed media (Option 1)
            Note over Disp,OpA: SLA still achievable: 48-72h courier + ceremony < 7d
        else Channel healthy
            Disp->>OpA: Out-of-band patch advisory + signature manifest
            Disp->>OpA: Patch bundle delivered (diode pull OR sealed media)
        end

        Note over OpA,Host: ===== Customer accreditation boundary =====
        OpA->>OpB: Two-person rule; verify advisory authenticity
        OpA->>Verify: arckit-verify ./patch-bundle --hsm-cert <pinned>
        Verify->>Verify: Same chain as Flow 1 (HSM sig + digests + SLSA + Rekor offline)

        alt Patch verification fails (any check)
            Verify-->>OpA: FAIL_VERIFY
            OpA->>SIEM: PATCH_VERIFY_FAIL event (cve_id, failure_class)
            OpA->>Disp: Reject patch; quarantine; request re-issue
            Note over OpA,Disp: SLA jeopardy; vendor incident raised;<br/>second media (verification copy) used as fallback
        else Patch verification passes
            OpA->>Host: Apply patch (FR-014; no full re-deploy)
            Host->>Host: Pre-apply backup (RPO <= 60 min, NFR-A-002)
            Host->>Host: Apply backported fix; restart affected components

            alt Patch apply fails at runtime (smoke test fails post-apply)
                Host->>Host: Auto-rollback to pre-apply state
                Host->>SIEM: PATCH_APPLY_ROLLED_BACK event (cve_id, reason)
                OpA->>Disp: Vendor incident raised; root-cause analysis
                Note over OpA,Disp: System remains on prior LTS patch level;<br/>SLA breach risk; customer + vendor co-manage
            else Patch apply OK; smoke tests pass
                Host->>SIEM: PATCH_APPLIED event (cve_id, lts_line, patch_id, sha512)
                OpA->>OpB: Co-sign apply attestation
                OpA->>SIEM: HOTFIX_CLOSED event (cve_id, sla_consumed_hours)
                Note over OpA,SIEM: Within 7d SLA: NFR-SEC-008 satisfied;<br/>no re-accreditation required (backport policy ADR-008)
            end
        end
    end
```

**Failure-mode coverage**:

| Failure | Detection point | Response |
|---------|-----------------|----------|
| Backport fails LTS CI | LTSci pipeline | Re-engineer; SLA clock keeps running; vendor escalates if 7-day window threatened |
| Diode channel outage | Dispatch | Failover to sealed media (Option 1); SLA still achievable |
| Patch verification fails at customer site | `arckit-verify` | Quarantine; request re-issue; verification-copy media used; vendor incident |
| Patch apply fails smoke test post-install | Host smoke tests | Auto-rollback to pre-apply state; SLA-breach risk; vendor + customer co-manage |
| Customer cannot meet 7-day window (logistics) | Pre-engagement assessment | Documented at engagement (ADR-007 R) — SLA constrained for that customer; alternative mitigations agreed |
| Reproducibility cross-build mismatch on backport | LTSci reproducibility stage | Halt pipeline; root-cause non-determinism; re-run (R-ADR2-4) |

---

## 8. Cross-Cutting Themes (Observable Across All Five Flows)

These themes are visible end-to-end and are the load-bearing architectural concerns that the orchestrator's diagrams must make visible:

1. **Zero outbound from the customer boundary** (NFR-SEC-004; Principle 21). Every flow shows the customer-side actors interacting only with customer-controlled endpoints (Customer IdP, Customer KMS, Customer CA, Customer SIEM, Customer AI Endpoint). The only inbound traffic is the bundle / patch crossing the boundary via an approved data-transfer mechanism (ADR-007), and every such crossing is signed-and-verified offline.
2. **Hash-chained customer SIEM is the single audit destination** (FR-010; ADR-003 step 6; ADR-005). Every flow ends in SIEM emission. There is no vendor-side observability of customer audit data — Principle 7 / Principle 21 / BR-003.
3. **Two-person rule + tamper-evident artefacts** (ADR-007 + ADR-003). Flows 1, 4, and 5 each invoke a two-person rule with co-signed events. Flows 2 and 3 enforce the equivalent through peer approval (Flow 2) and config-time validators (Flow 3).
4. **Fail-closed defaults at every decision point**. Flow 1 / 5 install refuses on any verifier failure (FR-001). Flow 3 falls back to manual authoring when AI is down (NFR-A-003). Flow 2 denies elevation when clearance attribute is absent. Flow 4 aborts on tamper suspicion. The architectural answer to ambiguity is "do nothing", per Principle 5 sovereign block.
5. **Single codebase across SaaS and sovereign** (BR-001; ADR-002 § reproducibility; ADR-004 adaptor reuse; ADR-008 no feature backports). The diagrams show no sovereign-only code paths that are not configuration-only behaviours. The same `AIAdaptor`, the same audit pipeline, and the same signing pipeline serve both deployment models — the differences are config, not fork.

---

## 9. Traceability

| Flow | Primary ADR(s) | HLD section(s) | REQ items |
|------|----------------|----------------|-----------|
| 1 — Bundle issue + verification ceremony | ADR-002, ADR-007 | §5.5, §6.2, §11 BLOCKING-01 | BR-002, BR-004, FR-001, FR-014, NFR-SEC-003/004/005 |
| 2 — JIT elevation | ADR-003 | §6.2 | FR-007, FR-010, NFR-SEC-006/007 |
| 3 — On-prem AI flow | ADR-004 | §5.3, §5.5 | FR-004, FR-005, FR-006, NFR-SEC-004/006, NFR-A-003 |
| 4 — Break-glass on-site | ADR-003 | §6.2 | FR-007, FR-010, NFR-SEC-007 |
| 5 — Critical CVE hotfix | ADR-008, ADR-007, ADR-002 | §5.5, §6.2, §10 | FR-014, NFR-SEC-008, NFR-C-005 |

Principle anchors: **Principle 5 (sovereign block)**, **Principle 7**, **Principle 21** (all five flows); **Principle 6** (audit emission, all flows); **Principle 20** (CI/CD reproducibility, Flows 1 + 5); **Principle 16** (open-source verifier tooling, Flows 1 + 5).

---

## 10. Open Items / Items Deferred to DLD

- **OVM schema** — finalised in DLD (cf. ADR-002 Appendix A indicative schema).
- **`arckit-verify` CLI exit-code matrix** — to be specified in DLD so that operator runbooks (FR-011) can branch deterministically on each `FAIL_*` code in Flows 1 and 5.
- **Break-glass split-secret algorithm** — Shamir M-of-N vs paper-and-tamper-seal selection per customer SAL (ADR-003 §5 Option 2 step 5). DLD will document both variants.
- **JIT approver-pool composition rules** — minimum pool size, after-hours rota, escalation to break-glass thresholds (Flow 2 advisory; ADR-003 ADVISORY in HLD).
- **AI dialect adapters** for TGI / vLLM / Triton OpenAI front-end quirks (Flow 3 con noted in ADR-004 §5 Option 1 cons).
- **Out-of-band advisory feed authenticity** — separate signing identity vs OVM-key reuse (Flow 5; ADR-008 §6 Communication).

---

## External References

> No external (third-party) documents were placed in `projects/002-arckit-sovereign/external/` at the time of this generation. UK Government, MOD, and standards-body materials referenced (MOD Secure by Design, JSP 440, JSP 604, NCSC CAF, NCSC Cloud Security Principles, NCSC Supply Chain Security guidance, HMG Government Security Classifications Policy, HMG Personnel Security Standards (BPSS / SC / DV / STRAP), UK GDPR / DPA 2018, ISO 29147, OIDC / OAuth 2.x / SAML 2.0 specifications, CycloneDX 1.5, SPDX 2.3, SLSA Framework v1.0, Sigstore / Cosign, FIPS 140-2 / 140-3, HMG-CAPS, OpenAI-compatible chat-completions wire format, HuggingFace TGI, vLLM, NVIDIA Triton) are public-domain and cited by name.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| HLDR-002-v1.0 | ARC-002-HLD-v1.0.md | Internal — HLD Review | projects/002-arckit-sovereign/ | Anchoring HLD review |
| ADR-002-002 | ARC-002-ADR-002-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Signed Release Bundle + OVM |
| ADR-002-003 | ARC-002-ADR-003-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Cleared-Personnel Access Model |
| ADR-002-004 | ARC-002-ADR-004-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | On-Premise AI Integration |
| ADR-002-007 | ARC-002-ADR-007-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Distribution Model + Verification Ceremony |
| ADR-002-008 | ARC-002-ADR-008-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | LTS Release Line |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| ADR2-OVM | ADR-002-002 | §6.1 / Appendix A | Decision | "HSM-anchored Offline Verification Manifest (OVM) ... verified at the customer side by a vendored static `arckit-verify` CLI with zero network calls" |
| ADR3-BG | ADR-002-003 | §5 Option 2 step 5 | Decision | "Break-glass is on-site only — a sealed-credential procedure performed by cleared personnel physically present at the host" |
| ADR4-FAIL | ADR-002-004 | §5 Option 1 fail-closed | Decision | "ai.provider = none -> all AI generation entry points return 403 ai_disabled ... Manual authoring (FR-008) unaffected" |
| ADR7-CER | ADR-002-007 | §5 Option 1 step 6 | Decision | "two-person rule for unsealing; ceremony uses customer-trusted standard tools (sha256sum, cosign verify, gpg verify); ceremony refuses to proceed if any check fails" |
| ADR8-SLA | ADR-002-008 | §5 Option 2 | Decision | "out-of-band patches for Critical-rated vulnerabilities within 7 days, High within 30 days, Medium within 90 days, for 24 months from issue" |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | No external documents placed in `projects/002-arckit-sovereign/external/` at time of generation. |

---

**Generated by**: ArcKit `/arckit:diagram` command
**Generated on**: 2026-05-03 GMT
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: claude-opus-4-7[1m]
**Generation Context**: Five sovereign-specific Mermaid sequence diagrams (bundle ceremony, JIT elevation, on-prem AI flow, break-glass, Critical-CVE hotfix) anchored on `ARC-002-HLD-v1.0.md` and ADR-002 / -003 / -004 / -007 / -008. Intended as wave-5 input to BLOCKING-01 of the HLD review. Sibling DIAGs (DIAG-001 C4 + DIAG-003 deployment) authored in parallel.
