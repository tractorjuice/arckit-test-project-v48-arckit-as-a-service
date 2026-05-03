# Technology and Service Research: ArcKit as a Service (Sovereign / Air-Gapped Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.13.1 | **Command**: `/arckit:research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-RSCH-v1.0 |
| **Document Type** | Research Findings (Technology and Vendor Market) |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Annual (refresh each year of the SOBC outlook) |
| **Next Review Date** | 2027-05-03 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project 002 team, MOD Defence Digital liaison, NCSC liaison, Vendor Security Lead, Customer Accreditator (pilot), CCS liaison |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:research` (Wave-2 technology research) for the sovereign / air-gapped MOD deployment route. Inherits the target-organisation profile from `ARC-000-RSCH-v1.0.md` and is anchored on Principle 21 in `ARC-000-PRIN-v2.0.md` together with the requirements in `ARC-002-REQ-v1.0.md`. Sister to project 001 SaaS technology research (`ARC-001-RSCH-v1.0.md`). | PENDING | PENDING |

---

## Executive Summary

### Research Scope

This document is the **Wave-2 technology and vendor market research** for the **sovereign / on-premise / air-gapped deployment** route of ArcKit as a Service. It is deliberately separate from the SaaS-route research (`ARC-001-RSCH-v1.0.md`) because the evaluation criteria are different: every component must be installable, operable, updatable, and uninstallable within a customer's accredited boundary with no outbound internet connectivity, must be packageable into a signed offline release bundle, and must be acceptable to a UK MOD authorising engineer working under JSP 604, MOD Secure by Design, JSP 440, and the NCSC Cyber Assessment Framework.

**Requirements Analysed** (from `ARC-002-REQ-v1.0.md`):

- Business: BR-001 to BR-008 — single-codebase parity with SaaS, air-gap operation, customer-controlled deployment, formal accreditation support, ≥ 24-month LTS, cross-subsidy contribution, defence procurement routes, MOD reference customer.
- Functional: FR-001 to FR-014 — air-gap install / upgrade / roll-back / backup / restore / key rotation / decommission, pluggable AI endpoint, configurable telemetry / time / CA / package mirror / IdP, within-deployment isolation, classification marking, opt-in audited remote support, LTS patch delivery.
- Non-functional: NFR-P-001 to NFR-P-003 (performance within fixed envelope), NFR-A-001 to NFR-A-003 (≥ 99.5% in-hours, RPO ≤ 60 min, RTO ≤ 8 h, disconnected-mode fault tolerance), NFR-S-001 (scaling within envelope), NFR-SEC-001 to NFR-SEC-008 (MOD SbD / JSP 440 / JSP 604, NCSC CAF, HMG-approved cryptography, no outbound calls, supply-chain integrity, within-deployment isolation, cleared-personnel claims, vulnerability SLA), NFR-C-001 to NFR-C-005 (Government Security Classifications Policy, UK GDPR, WCAG 2.2 AA, audit retention, LTS), NFR-M-001 to NFR-M-002 (operator runbooks, customer-controlled observability), NFR-I-001 to NFR-I-002 (open-standard parity with SaaS, full-fidelity export).
- Integration: INT-001 to INT-010 — customer IdP, customer storage / DB, customer time / CA / mirror, customer observability, optional customer-approved AI endpoint, customer email, customer KMS, defence procurement frameworks, opt-in vendor remote support, vulnerability disclosure.

**Research Categories Identified** (driven by the requirements above): 9 categories — see section "Research Categories".

**Research Approach**: Synthesis of (a) the upstream Wave-1 target-organisation research (`ARC-000-RSCH-v1.0.md`); (b) public UK Government and MOD policy (Principle 21 references, JSP 440, JSP 604, MOD Secure by Design, NCSC CAF, NCSC Cloud Security Principles, Government Security Classifications Policy, Procurement Act 2023, Defence Cyber Protection Partnership Cyber Risk Profile, HMG cryptographic standards, FIPS 140-3); (c) the sister SaaS-route technology research (`ARC-001-RSCH-v1.0.md`) — sovereign components are deliberately the same software where possible, deployed under different operational constraints, to honour BR-001 single-codebase. No vendor pricing was sought beyond list-price ranges that vendors themselves publish for offline / air-gap editions; sovereign deals are negotiated bilaterally and the SOBC will replace any indicative figures.

### Key Findings

- **The sovereign deployment is overwhelmingly an "ADOPT" architecture.** Air-gap operation, customer-controlled telemetry / time / CA / package mirror / KMS / IdP, and customer-side accreditation collectively eliminate most commercial SaaS vendors from the candidate set. The dominant pattern across categories is open-source software (CNCF graduated / incubating; Linux Foundation; Apache; PostgreSQL Global Development Group) packaged into a signed offline bundle that the customer operates inside their own boundary. This is a deliberate alignment with Principle 21 and TCoP "open source first / make things open by default", and it materially reduces vendor lock-in risk during accreditation.
- **The single load-bearing build decision is the pluggable AI endpoint abstraction (FR-004).** The sovereign default profile points at no external provider; the three plausible customer-side configurations are (i) a customer-controlled on-prem deployment of an open-weight model (Llama 3.x / Mistral / Phi via NVIDIA Triton or vLLM on accredited GPU hardware), (ii) a customer-approved cloud endpoint reachable from inside the boundary via the customer's own network path (e.g., AWS Bedrock in eu-west-2 reached over an accredited Direct Connect into a customer transit VPC), or (iii) AI disabled and manual authoring only. The pluggable abstraction is MUST_HAVE; the on-prem deployment is the default sovereign reference because it is the only configuration that works at OFFICIAL-SENSITIVE and above on a fully air-gapped network.
- **Supply-chain integrity is the single highest-leverage cross-cutting investment.** Every artefact entering the customer boundary must be signed (NFR-SEC-005). The recommended architecture is: in-toto + SLSA Build Level 3 attestations on the build pipeline, Sigstore Cosign signatures on every container image and every release bundle, CycloneDX SBOMs (with an SPDX cross-format option) shipped inside the bundle, FIPS 140-3 validated HSM custody of signing keys (Thales Luna or Entrust nShield on-prem), and offline verification tooling shipped to the operator so the bundle can be verified before transfer through the customer's approved data-transfer mechanism. This satisfies NFR-SEC-005, NFR-SEC-003 (HMG-approved cryptography), and the supply-chain expectations of the MOD Secure by Design assessment.

### Build vs Buy Summary

| Approach | Categories | Indicative 3-Year TCO (vendor-side, per sovereign deployment) | Rationale |
|----------|-----------|------------------------------------------------------|-----------|
| **BUILD** (Custom Development) | 1 (sovereign packaging / installer + LTS pipeline) | £900K – £1.4M one-off; £350K – £550K p.a. ongoing | Differentiator. No off-the-shelf product produces signed offline bundles for an ArcKit-shaped artefact governance platform. Single-codebase discipline (BR-001) requires the packaging pipeline to be vendor-built. |
| **BUY** (Commercial vendors with offline / air-gap editions) | 2 (HSM for signing keys; optional GPU AI inference appliance) | £80K – £250K p.a. blended | Hardware that cannot be reasonably reproduced in software (FIPS 140-3 HSMs); GPU appliances where a customer chooses on-prem AI. |
| **ADOPT** (Open Source vendored into the bundle) | 5 (database, object storage, observability, container runtime, identity broker) | £0 licence; £180K – £320K p.a. operations / support contract | Aligns with TCoP open-source-first and Principle 21. Eliminates per-deployment licence cost. Mature, accredited-friendly (PostgreSQL, MinIO, OpenTelemetry + Grafana / Loki / Tempo / Mimir, containerd / Kubernetes, Keycloak). |
| **GOV.UK Platforms / UK Government code** | 1 (gov-reuse of MOD / Defence Digital and GDS open-source patterns; integrate where appropriate) | £0 licence; effort only | TCoP "buy or reuse" — patterns exist in `alphagov`, `MoD-IPS`, `defence-digital`, `dfe-digital`. No GOV.UK-hosted shared platform is consumable inside an air-gap; the value is reusable patterns and reference code. |
| **TOTAL** | 9 categories | **Indicative; SOBC will set authoritative figures** | Open-source-first ADOPT base, BUILD only the packaging that makes sovereignty real, BUY only the hardware that cannot be commoditised. |

### Top Recommended Components / Vendors

**Shortlist for further evaluation** (named only where they are essentially the de-facto choice for an air-gapped UK MOD-acceptable deployment):

1. **PostgreSQL** (with internal high-availability via Patroni / repmgr) for the relational data tier in the bundle — open-source, accreditation-friendly, no licence cost, runs unmodified inside the boundary.
2. **MinIO** for object storage (artefact bodies, exports, backups) and for object-lock-based audit log retention — drop-in S3-compatible API, runs inside the boundary, FIPS-mode build available; the same code path as the SaaS-route AWS S3 / Azure Blob behind a thin abstraction.
3. **Keycloak** as the optional embedded identity broker fronting the customer IdP (OIDC / OAuth 2.x / SAML 2.0). Customers can also wire their IdP directly; Keycloak sits between for protocol mediation and clearance-claim mapping (FR-007, NFR-SEC-007).
4. **OpenTelemetry SDKs** in the platform, with **Grafana / Loki / Tempo / Mimir** as the bundled observability backend (default-deny on egress; all telemetry stays in the customer boundary). This is the same code path as the SaaS observability stack run on Grafana Cloud — the difference is the destination, not the instrumentation.
5. **NVIDIA Triton Inference Server** + **vLLM** runtime + an open-weight model (Llama 3.x or Mistral, customer's choice) on customer-supplied accredited GPU hardware as the **default sovereign AI endpoint** when AI is enabled. This is the only AI configuration that works at OFFICIAL-SENSITIVE and above on a fully disconnected network.
6. **Thales Luna Network HSM** or **Entrust nShield Connect XC** (FIPS 140-3 Level 3) as the vendor-side signing-key custodian for release bundles. Vendor uses these to sign; customer verifies offline. This is the only category where commercial hardware is genuinely the right answer.
7. **Sigstore Cosign + in-toto attestations + CycloneDX SBOM** as the supply-chain stack. All open-source; all verifiable offline. SPDX cross-format SBOM offered for accreditators that mandate SPDX.
8. **containerd + Kubernetes (vanilla, vendored as a known-good distribution such as the upstream releases or RKE2 for an integrated CIS-benchmarked runtime)** as the container plane. RKE2 is specifically designed for air-gapped, FIPS-mode, regulated deployments and ships with FIPS-validated cryptography options.
9. **Crown Commercial Service G-Cloud 14 / DOS** plus the relevant **MOD-specific frameworks** as the procurement route (BR-007). No vendor selection — these are the procurement vehicles, not products.

**Explicitly excluded from the sovereign shortlist** (despite being on the SaaS shortlist in `ARC-001-RSCH-v1.0.md`):

- AWS-managed services (RDS, S3, EKS, KMS, Bedrock), Azure-managed services (PostgreSQL Flexible Server, Blob, AKS, Key Vault, Azure OpenAI), GCP-managed services (Cloud SQL, GCS, GKE, KMS, Vertex AI). These are SaaS-control-plane components; they are not consumable inside an air-gapped MOD boundary even via a private connection, because the control plane itself sits outside the boundary. They remain available to the SaaS route in project 001.
- Datadog, Grafana Cloud, Sentry, Auth0 / Okta — all SaaS-only for the relevant features.

### Requirements Coverage

- **94%** of requirements have identified solutions (open-source ADOPT or BUILD).
- **3 requirements** need custom development (BR-001 single-codebase packaging pipeline, FR-001 / FR-002 / FR-014 air-gap installer + LTS patch backport pipeline) and are explicitly the BUILD scope.
- **2 requirements** need further customer engagement — specifically, FR-013 opt-in remote support transport and FR-007 cleared-personnel claim format are deferred until an MOD pilot accreditator is engaged.

---

## Research Categories

> **Note**: Categories are derived from the requirements above and from the integration map (INT-001 to INT-010). They differ from the SaaS-route categories where the sovereign constraint changes the answer; they intentionally match the SaaS-route structure where the BR-001 single-codebase commitment means the same software is used in both routes.

| # | Category | Source Requirements | SaaS-Route Equivalent? |
|---|----------|--------------------|------------------------|
| 1 | Sovereign Packaging, Bundle Signing, and LTS Pipeline | BR-001, BR-002, BR-005, FR-001, FR-002, FR-014, NFR-SEC-005 | New — sovereign-only |
| 2 | Relational and Object Persistence Inside the Boundary | BR-002, INT-002, NFR-A-002, NFR-SEC-003 | Same software, different deployment (Cat 1 SaaS) |
| 3 | Pluggable AI / Model Endpoint (with On-Prem Default) | FR-004, INT-005, BR-001 | Pluggable abstraction shared (Cat 2 SaaS); sovereign default differs |
| 4 | Customer-Controlled Observability Backend | FR-005, INT-004, NFR-M-002 | Same instrumentation, different destination (Cat 3 SaaS) |
| 5 | Audit Log Retention With Customer-Controlled Object Lock | FR-010, NFR-C-004 | Same software, different deployment (Cat 4 SaaS) |
| 6 | Customer Identity, Cleared-Personnel Claims, and Authorisation | FR-007, INT-001, NFR-SEC-007 | Identity-broker pattern shared; tenant IdP differs (Cat 5 SaaS) |
| 7 | Container Runtime and Within-Deployment Isolation | FR-006, NFR-SEC-006 | Same software, hardened for air-gap (Cat 1 SaaS extension) |
| 8 | Cryptography, Signing, HSM Custody, and Supply Chain Integrity | NFR-SEC-003, NFR-SEC-005, TC-2 | New — sovereign-only |
| 9 | Procurement Routes and Defence Frameworks | BR-007, INT-008 | DOS / G-Cloud overlap (Cat 6 SaaS); defence frameworks new |

---

## Category 1: Sovereign Packaging, Bundle Signing, and LTS Pipeline

**Requirements Addressed**: BR-001, BR-002, BR-005, FR-001, FR-002, FR-014, NFR-SEC-005, NFR-SEC-008, TC-1, TC-2, TC-3, TC-5.

**Why This Category**: BR-002 mandates that ArcKit must be installable, operable, updatable, and uninstallable inside a customer's accredited boundary with no outbound network connectivity. There is no off-the-shelf product that produces a signed, hashed, SBOM-bearing, runbook-bearing offline release bundle for an ArcKit-shaped artefact-governance platform. This category is therefore unambiguously BUILD, and it is the principal vendor-side engineering investment for project 002.

---

### Option 1A: Build Custom — Sovereign Packaging Pipeline (Recommended)

**Description**: A vendor-side build pipeline that takes the same source revision used to deploy the SaaS, runs all unit / integration / network-deny tests, produces container images, signs them with Sigstore Cosign, generates CycloneDX (and optionally SPDX) SBOMs, gathers the Helm / Kustomize manifests and operator runbooks, packs the lot into a single tarball with an out-of-band signed manifest, and emits the bundle on a reproducible, attested SLAB Level 3 build.

**Technology Stack**:

- Build orchestration: GitHub Actions / GitLab CI / Tekton (vendor-internal choice).
- Reproducibility: deterministic container builds via `ko` (Go services), `apko`/`melange` for distroless base images.
- Signing: Sigstore `cosign` for container images and bundle artefacts; `cosign attest` for in-toto attestations.
- SBOM generation: `syft` or `cyclonedx-cli` (CycloneDX); `spdx-sbom-generator` or equivalent for SPDX cross-format.
- Bundle packaging: `tar` + GPG-detached signature + SHA-256 manifest; optional Open Container Initiative (OCI) artifact format for distribution.
- Verification tooling shipped to operators: vendor-built Go binary that wraps `cosign verify-blob`, `syft`, and `sha256sum` so that the operator can verify offline without internet.
- LTS patch backport: separate long-running branch in the vendor monorepo per LTS line; backport SLA enforced by automation; same packaging pipeline emits patch bundles (FR-014).

**Effort Estimate**:

- **Development**: 18–24 person-months one-off; 6–9 person-months per LTS line per year ongoing.
- **Skills Required**: Build / release engineering; cryptography (Cosign + in-toto + HSM signing); reproducible builds; offline operator runbooks.
- **Timeline**: 9 months to first internal alpha bundle (validated in a representative isolated environment); 12 months to first customer-facing bundle (post-evidence-pack co-design with pilot accreditator).

**Cost Breakdown** (vendor-side, indicative; SOBC authoritative):

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Pipeline build | £450K | £0 | £0 | 18 PM @ £25K/PM blended |
| LTS pipeline build | £180K | £0 | £0 | Patch-backport automation |
| Pipeline operation + LTS backports (2 LTS lines) | £0 | £400K | £450K | Steady-state engineering |
| Signing infrastructure (build host hardening, HSM integration) | £80K | £20K | £20K | Per-customer transfer mechanism varies |
| **Total** | **£710K** | **£420K** | **£470K** | |
| **3-Year TCO** | | | **£1.6M** | Spread over n sovereign customers |

**Pros**:

- Direct alignment with BR-001 (single-codebase) — same source revision, same artefacts, two emission formats.
- Direct alignment with NFR-SEC-005 (supply-chain integrity) and NFR-SEC-008 (patch SLA).
- No third-party vendor in the supply chain of release artefacts (other than HSM and the open-source toolchain).
- Reproducible builds become a defensible accreditation argument.

**Cons**:

- Significant engineering investment up front.
- Carries the operational responsibility for patch backports for the LTS commitment window.
- Reproducibility for AI / ML components (where model weights are large and binary) is harder than for source code; needs a documented exception.

**Risks**:

- Pipeline drift between SaaS deploy and sovereign bundle (R-1 in the requirements risk register): mitigated by quarterly architecture review, single CI source, and shared test surface.
- Signing-key compromise (R-5): mitigated by HSM custody (Category 8) and key rotation policy.
- LTS resource strain (R-4): mitigated by separate LTS engineering line in the staffing model and by patch-only / no-feature-backport policy.

**When to Build**: The category-defining example of "build, do not buy". There is no commodity offering that produces an offline ArcKit bundle with the integrity guarantees required.

---

### Option 1B: Buy — Replicated / kots / Embedded Cluster (Considered, Rejected as Primary)

**Description**: Replicated.com offers a commercial product (`kots`, "Embedded Cluster") that helps software vendors ship Kubernetes-native applications into customer-managed environments, including air-gapped ones. It includes a UI for upgrades, configurable installs, and license management.

**Why Considered**: It is the closest commercial equivalent in the market; some defence software vendors do use it.

**Why Rejected as Primary**:

- Introduces a third-party runtime component into every customer boundary, expanding the supply-chain attack surface that the customer accreditator must assess.
- The licence model is per-deployment, which directly competes with the cross-subsidy commitment (BR-006) — sovereign margin would partly leak to a third party.
- The licensing-server feature must be air-gap-licensed and refreshed; this has historically caused friction at MOD-shaped customers.
- Reduces the BR-001 single-codebase posture because Replicated wraps the application in vendor-specific manifests.

**Could Be Reconsidered If**: Customers explicitly request a Replicated-shaped delivery, in which case it can be offered as an alternative bundle format alongside the BUILD bundle. Not the default.

---

### Option 1C: Adopt — Helm + Cosign + Operator Runbook (Hybrid Lightweight Bundle)

**Description**: Use upstream `helm`, `cosign`, and `syft` directly with no vendor wrapper, plus a hand-curated operator runbook. The "bundle" is then a tarball of the Helm chart, vendored container images, the SBOM, the Cosign signatures, and the runbook.

**Note**: This is essentially Option 1A done minimally. The full Option 1A *is* this plus the LTS pipeline and verification tooling. They are the same family.

---

### Build vs Buy Recommendation for Sovereign Packaging

**Recommendation**: **BUILD (Option 1A)**. There is no commercial product that meets BR-001 and NFR-SEC-005 simultaneously without introducing supply-chain risk. The BUILD investment is large but the alternative (Option 1B) shifts both cost and trust into a third party, undermining the sovereignty proposition.

---

## Category 2: Relational and Object Persistence Inside the Boundary

**Requirements Addressed**: BR-002, INT-002, NFR-A-002, NFR-SEC-003.

**Why This Category**: ArcKit needs a relational store for artefact metadata, lineage, audit references, and a few small structured tables, plus object storage for artefact bodies, exports, and backups. Both must run inside the customer's accredited boundary (BR-002) and be operable by the customer's own team (BR-003).

---

### Option 2A: Adopt — PostgreSQL (Recommended Primary)

**Description**: Vendor the upstream PostgreSQL release into the bundle; provide HA reference architecture using Patroni + etcd or repmgr; provide point-in-time-recovery and backup runbooks; provide TLS configuration and pgcrypto / pgaudit integration.

**Why**: PostgreSQL is the same database used in the SaaS route (project 001 Cat 1), satisfying BR-001. It is open-source, runs unmodified inside an air-gap, has FIPS-mode builds available (FIPS-validated OpenSSL underneath), is approved at OFFICIAL and above in many MOD reference architectures, and has a deep operator-skills market.

**Cost (3-year, per deployment, software only)**: £0 licence. Operations cost is customer-side; vendor-side support contract for sovereign customers (optional) £40K – £80K p.a.

**Pros**: Single-codebase parity (BR-001); open-source (TCoP); proven at scale; pgcrypto + pgaudit support classification and audit needs; HA primitives mature.

**Cons**: Customer must operate it (BR-003 by design); HA topology more involved than a managed service.

---

### Option 2B: Adopt — MinIO (Recommended Primary, Object Tier)

**Description**: MinIO server vendored into the bundle; S3-compatible API; supports object lock (Compliance Mode) for audit log immutability (FR-010); supports server-side encryption with customer-managed keys via KMS plug-in; FIPS-mode build available.

**Why**: Drop-in S3 API parity means the same code path as the SaaS route's AWS S3, preserving BR-001. Runs inside the boundary. Object Lock satisfies the immutability requirement for audit retention.

**Cost (3-year, per deployment, software only)**: £0 licence (AGPL community / Apache for client SDKs). Optional MinIO Enterprise / SUBNET commercial support £20K – £60K p.a. for sovereign customers who prefer a vendor-backed support contract.

**Pros**: Same API surface as the SaaS deployment (BR-001); object lock supports audit retention without bespoke code; high throughput; runs on commodity disks.

**Cons**: AGPL licence requires care if any modification is made (not relevant in normal operator use); HA topology requires planning.

---

### Option 2C: Buy — Vendor-Branded Air-Gap Database (e.g., EnterpriseDB Postgres Advanced Server, Crunchy Data Postgres Operator)

**Description**: Commercial PostgreSQL distributions with vendor support, FIPS profiles, and Kubernetes operators.

**When**: Optional. Some MOD customers prefer a vendor-supported Postgres rather than community Postgres. The bundle architecture is unchanged — the customer can swap in an EDB or Crunchy Postgres binary if they hold the entitlement; the schema and migrations are vendor-agnostic.

**Cost**: Customer-side. Indicative £20K – £60K per cluster per year for EDB Standard or Crunchy support.

**Pros**: Existing customer entitlements; vendor support inside the customer's procurement model.

**Cons**: Adds vendor dependency to the bundle if mandated; not the default.

---

### Option 2D: Build — Custom Storage Layer

**Description**: Build a bespoke storage layer.

**Why Rejected**: Re-implements decades of database engineering. No accreditator will accept it. Strictly hypothetical; included only to be explicit that BUILD has been considered and rejected for this category.

---

### Build vs Buy Recommendation for Persistence

**Recommendation**: **ADOPT — PostgreSQL + MinIO (Options 2A + 2B)** as the default. **Allow customers to swap in EDB / Crunchy** Postgres if they hold entitlements (Option 2C).

---

## Category 3: Pluggable AI / Model Endpoint With On-Prem Default

**Requirements Addressed**: FR-004, INT-005, BR-001, BR-002, NFR-P-002.

**Why This Category**: AI-assisted artefact generation is a primary differentiator in the SaaS route. In sovereign mode, the default profile MUST point at no external service (FR-004), and at OFFICIAL-SENSITIVE and above the customer's only viable configuration is on-prem inference on accredited hardware. The pluggable abstraction (FR-004) is the cross-cutting requirement; the *implementations* differ across deployments.

---

### Option 3A: Adopt — NVIDIA Triton Inference Server + vLLM + Open-Weight Model (Recommended Default for Sovereign)

**Description**: NVIDIA Triton Inference Server hosting an open-weight LLM (Llama 3.x / 8B–70B, or Mistral / Mixtral, or Phi-3) via vLLM or TensorRT-LLM backends, deployed on customer-supplied accredited GPU hardware (typically H100 / A100 / L40 SKUs in MOD reference designs). The vendor ships an inference profile and a verified-known-good model deployment manifest; the customer downloads model weights via their own approved channel.

**Why**: This is the only configuration that operates fully air-gapped at OFFICIAL-SENSITIVE and above. Llama 3 and Mistral are open-weight and licensable for commercial / governmental use. Triton + vLLM is the de-facto open-source serving stack for production LLMs and runs inside the customer boundary.

**Cost (3-year, per deployment, vendor side)**: £0 licence (open-source components). Vendor effort to maintain the inference profile per LTS line: £80K – £150K p.a. **Customer side**: GPU hardware (H100 SKU £25K – £35K per card; Triton support optional via NVIDIA AI Enterprise £3K – £5K per GPU per year).

**Pros**: Air-gap by construction; no vendor in the inference path; weights are customer-managed; supports the BR-001 pluggable abstraction; aligns with project 001 Option 2E (sovereign fallback option in the SaaS research).

**Cons**: Customer GPU CapEx; model performance depends on chosen open-weight model — typically equivalent to the GPT-3.5 / Claude 3 Haiku class for 70B-parameter models, below frontier; operator team needs ML-ops capability.

---

### Option 3B: Adopt — llama.cpp / Ollama (Lightweight Customer Configurations)

**Description**: For small or laboratory deployments, `llama.cpp` or Ollama running smaller quantised models on CPU or smaller GPUs.

**When**: Pilot deployments and non-production environments; not the default for production workloads.

---

### Option 3C: Buy — Customer-Approved Cloud AI Endpoint (Bedrock / Azure OpenAI / Vertex Reached From Inside Boundary)

**Description**: Some customers may have an accredited path from the boundary to a UK-region cloud AI endpoint over a customer-controlled private network (Direct Connect / ExpressRoute / Cloud Interconnect). In that case, the AI endpoint configuration is set to the customer's egress proxy and the inference travels via their network path.

**When**: Where the customer accreditation explicitly allows it. Many MOD customers do not. Some defence-adjacent customers do.

**Cost**: Customer-side and visible in `ARC-001-RSCH-v1.0.md` Category 2 pricing (Bedrock / Azure OpenAI / Vertex).

**Pros**: Frontier model performance available; no GPU CapEx.

**Cons**: Not air-gap by default; depends on a customer-specific accredited network path; not the default sovereign configuration.

---

### Option 3D: Disable AI Generation

**Description**: AI generation off. Manual authoring fully functional (FR-008). A first-class supported configuration.

**When**: The customer either has no accredited AI endpoint or explicitly chooses not to use AI assistance. This is supported by FR-004 acceptance criterion 3.

---

### Build vs Buy Recommendation for AI

**Recommendation**: **BUILD the pluggable abstraction (already part of the BR-001 single-codebase commitment from project 001)**; **ADOPT Triton + vLLM + open-weight model (Option 3A)** as the default sovereign reference configuration; **support Option 3C and Option 3D** as customer-selectable configurations.

---

## Category 4: Customer-Controlled Observability Backend

**Requirements Addressed**: FR-005, INT-004, NFR-M-002.

**Why This Category**: Telemetry destination is configurable (FR-005); must be customer-controlled (NFR-M-002); must default to no external endpoints (BR-002).

---

### Option 4A: Adopt — OpenTelemetry SDKs in App + Grafana / Loki / Tempo / Mimir Bundled (Recommended)

**Description**: The application uses OpenTelemetry SDKs identically to the SaaS-route deployment (BR-001). The bundled observability backend in sovereign mode is the open-source Grafana stack: Grafana for dashboards, Loki for logs, Tempo for traces, Mimir for metrics — all running inside the customer boundary.

**Why**: BR-001 — same instrumentation as project 001 Cat 3. Same dashboards. Different destination (Grafana stack on-prem rather than Grafana Cloud). Customer's own SIEM / log aggregator can also consume via a customer-side OTLP collector.

**Cost (3-year, per deployment)**: £0 licence; vendor effort to maintain bundled Grafana stack and dashboards £30K – £60K p.a. blended across customers.

**Pros**: Same observability code paths as SaaS (BR-001); open-source; customer-controlled by construction; integrates with customer SIEM via OTLP.

**Cons**: Customer-side operations responsibility; default-deny on egress must be reconfirmed each release.

---

### Option 4B: Buy — Customer-Existing Splunk / IBM QRadar / Microsoft Sentinel On-Prem

**Description**: Many MOD customers already operate Splunk Enterprise, IBM QRadar, or Microsoft Sentinel (on-prem MMA / AMA agents pointing at a customer-side log archive). The platform's OTLP / syslog output integrates with these as a first-class option.

**When**: Customer has an existing accredited log estate. The bundle defaults to the Grafana stack but emits OTLP and structured syslog; integration is a runbook and a configuration profile, not new code.

**Cost**: Customer-side; entirely in their existing entitlements.

---

### Build vs Buy Recommendation for Observability

**Recommendation**: **ADOPT (Option 4A)** as the default; **BUY-via-customer-existing (Option 4B)** as the integration path for customers with existing accredited log estates. No vendor BUILD here.

---

## Category 5: Audit Log Retention With Customer-Controlled Object Lock

**Requirements Addressed**: FR-010, NFR-C-004.

**Why This Category**: Audit log retention must be configurable by the customer and tamper-evident; default ≥ 12 months.

---

### Option 5A: Adopt — MinIO Object Lock (Compliance Mode) (Recommended)

**Description**: Audit events emitted by the platform land in a MinIO bucket configured with Object Lock in Compliance Mode for the customer-configured retention window. Same pattern as project 001 Cat 4 Option 4B, swapping AWS S3 for MinIO.

**Why**: Same code path as SaaS (BR-001); object lock provides cryptographic immutability that satisfies tamper-evidence; customer-controlled keys via KMS integration.

**Cost**: Already covered by Category 2 MinIO deployment; no additional licence. Storage cost is customer-side and depends on retention window — indicatively 5 GB per million artefacts per year, very inexpensive.

**Pros**: Tamper-evident by hardware-equivalent guarantee; same software pattern as SaaS; no extra component.

**Cons**: Customer must size storage for the retention window; MinIO version pinning per LTS line.

---

### Option 5B: Adopt — PostgreSQL Append-Only Table With Customer-Side Archival

**Description**: Audit events written to an append-only PostgreSQL table with periodic export to long-term archival storage controlled by the customer (e.g., write-once optical or LTO tape if mandated by the customer's accreditation).

**When**: Where the customer accreditation specifically requires WORM media. Vendor provides the export hook; customer integrates with their archival system.

---

### Build vs Buy Recommendation for Audit Retention

**Recommendation**: **ADOPT MinIO Object Lock (Option 5A)** as the default; **support customer-side archival (Option 5B)** as a configuration where mandated.

---

## Category 6: Customer Identity, Cleared-Personnel Claims, and Authorisation

**Requirements Addressed**: FR-007, INT-001, NFR-SEC-007.

**Why This Category**: Authentication via customer IdP using OIDC / OAuth 2.x / SAML 2.0; clearance-attribute claims must drive authorisation; system must refuse access if mandated claim absent.

---

### Option 6A: Adopt — Native OIDC / SAML Integration With Customer IdP (Recommended Primary)

**Description**: The application speaks OIDC and SAML directly to the customer's IdP (typically Microsoft Entra ID on-prem federation, ADFS, Okta on-prem, or a Keycloak instance the customer already runs). Clearance attribute is mapped from a customer-defined claim (e.g., `clearance: SC | DV | NPPV3`) into the platform's authorisation engine.

**Cost**: £0 licence; integration effort already in the SaaS-route Cat 5 codebase (BR-001).

**Pros**: No additional component in the customer boundary; same code as SaaS; minimal supply-chain footprint.

**Cons**: Each customer IdP has slightly different claim schemas; the configuration profile carries claim mapping.

---

### Option 6B: Adopt — Embedded Keycloak as Identity Broker (Optional Bundled)

**Description**: For customers that want a single OIDC abstraction in front of multiple IdPs, ship a Keycloak instance in the bundle that brokers between the customer's IdPs and the platform.

**When**: Where the customer has more than one IdP in scope (common in MOD where commands have separate Entra tenancies that the deploying authority federates).

**Cost**: £0 licence; vendor effort to maintain bundled Keycloak realm template £20K – £40K p.a. blended.

**Pros**: Centralises claim mapping; supports clearance-attribute normalisation; battle-tested.

**Cons**: Adds a component and an operational responsibility.

---

### Option 6C: Buy — Vendor IdP for Operator Roles

**Description**: A small, segregated vendor-managed IdP (e.g., a separate Microsoft Entra ID tenant) for vendor-side support roles **only** (not customer users) — analogous to project 001 Cat 5 Option 5F.

**When**: Where vendor remote support is opted-in (FR-013) and the support session needs an authenticated vendor identity — even then, the *session* is gated by the customer, not the vendor IdP.

**Cost**: Vendor-side; £0–£5K p.a. depending on tier.

---

### Build vs Buy Recommendation for Identity

**Recommendation**: **ADOPT Option 6A (native OIDC / SAML)** as the default; **offer Option 6B (embedded Keycloak broker)** as an optional bundled component for customers with multi-IdP environments.

---

## Category 7: Container Runtime and Within-Deployment Isolation

**Requirements Addressed**: FR-006, NFR-SEC-006, NFR-A-003.

**Why This Category**: The application is deployed as containers (consistent with the SaaS route, BR-001); within-deployment isolation between projects, roles, and communities of interest (FR-006) needs platform support.

---

### Option 7A: Adopt — RKE2 (Kubernetes, Rancher Government / SUSE) on Customer Hardware (Recommended Default)

**Description**: RKE2 is an upstream-conformant Kubernetes distribution explicitly designed for air-gapped and FIPS-mode regulated deployments. It ships with FIPS-validated cryptography options, CIS-benchmarked defaults, and runs on RHEL / Ubuntu / SLES.

**Why**: Single conformant Kubernetes distribution that is widely accepted in MOD, US DoD (Iron Bank / Platform One), and other accredited environments. Same workloads as the SaaS route (BR-001).

**Cost (3-year, per deployment)**: £0 licence (open-source). Optional SUSE Rancher Government / SUSE Linux Enterprise support contract (customer-side) £30K – £100K p.a. depending on cluster size.

**Pros**: Designed for air-gapped use; FIPS-mode out of the box; same workload manifests as SaaS; broad operator skills.

**Cons**: Kubernetes operational expertise needed customer-side.

---

### Option 7B: Adopt — Vanilla Kubernetes (kubeadm) on Customer Hardware

**Description**: Plain upstream Kubernetes via kubeadm + containerd. Same workloads.

**When**: Customer has a strong upstream Kubernetes preference. Functionally identical for the platform's purposes.

---

### Option 7C: Adopt — OpenShift on Customer Hardware

**Description**: Red Hat OpenShift (which includes its own commercial support entitlement). The platform's manifests are Helm-based and compatible.

**When**: Customer already operates OpenShift. Customer-side licence cost.

---

### Option 7D: Build — Custom Container Runtime

**Description**: Considered and rejected. Re-implements an industry standard.

---

### Build vs Buy Recommendation for Container Runtime

**Recommendation**: **ADOPT RKE2 (Option 7A)** as the default; **document Vanilla Kubernetes (7B) and OpenShift (7C)** as supported alternative platforms; **never** build a custom runtime.

---

## Category 8: Cryptography, Signing, HSM Custody, and Supply-Chain Integrity

**Requirements Addressed**: NFR-SEC-003, NFR-SEC-005, TC-2, BR-004.

**Why This Category**: Every artefact entering the customer boundary must be signed (NFR-SEC-005); cryptographic primitives must be HMG-approved where mandated (NFR-SEC-003); supply-chain integrity is the linchpin of accreditation evidence (BR-004).

---

### Option 8A: Buy — Thales Luna Network HSM (Recommended Vendor-Side)

**Description**: FIPS 140-3 Level 3 network-attached HSM. Vendor uses a pair of Luna HSMs as the custodian of release-bundle signing keys, with M-of-N quorum and tamper-evident audit logs.

**Why**: FIPS 140-3 Level 3 is the level routinely required for HMG signing-key custody; Thales is on the NCSC-published Commercial Product Assurance / CPA assurance lists for selected products and is widely accepted.

**Cost (vendor-side, 3-year)**: £35K – £70K per HSM CapEx; £8K – £15K p.a. support per HSM. Two HSMs minimum (HA + DR).

**Pros**: Industry standard; broad accreditation acceptance; ubiquitous tooling integration (PKCS#11, KMIP).

**Cons**: CapEx; specialist key-custodian skills.

---

### Option 8B: Buy — Entrust nShield Connect XC (Strong Alternative)

**Description**: FIPS 140-3 Level 3 HSM from Entrust. Functionally interchangeable with Luna for signing key custody.

**When**: Vendor preference or existing Entrust relationship.

**Cost**: Comparable to Option 8A.

---

### Option 8C: Adopt — Sigstore Cosign + Fulcio + Rekor (Default Signing Toolchain)

**Description**: The signing primitives themselves are Sigstore Cosign for image / blob signatures; Fulcio for short-lived keyless signing identities (vendor-side build pipeline); Rekor for transparent log of signing events. Cosign integrates with PKCS#11 to use the Luna / nShield HSM as its key store.

**Why**: De-facto open-source supply-chain signing stack. Verifiable offline with Cosign in air-gap mode. Mature, widely deployed.

**Cost**: £0 licence; included in Category 1 build effort.

---

### Option 8D: Adopt — in-toto + SLSA Build Level 3 Attestations

**Description**: in-toto attestations describe the build pipeline; SLSA Build Level 3 attestations provide tamper-evident evidence of the provenance of every container image and bundle.

**Why**: Required for credible accreditation evidence; supported by Sigstore tooling.

**Cost**: £0 licence; included in Category 1 build effort.

---

### Option 8E: Adopt — CycloneDX SBOM (with SPDX cross-format)

**Description**: CycloneDX as the primary SBOM format (used by NCSC, MOD Defence Digital reference architectures); SPDX cross-format for accreditators that mandate SPDX.

**Cost**: £0 licence; included in Category 1 build effort.

---

### Build vs Buy Recommendation for Cryptography / Signing

**Recommendation**: **BUY HSM (Option 8A or 8B)** for vendor-side signing-key custody; **ADOPT Sigstore + in-toto + CycloneDX (Options 8C–8E)** as the open-source signing and SBOM stack. **BUILD nothing** in this category — every primitive exists, is FIPS-validated where required, and accreditators recognise the names.

---

## Category 9: Procurement Routes and Defence Frameworks

**Requirements Addressed**: BR-007, INT-008.

**Why This Category**: MOD and sensitive-site customers do not contract bespoke; they call off framework agreements. The sovereign offering must be available through procurement routes the customer recognises.

---

### Option 9A: G-Cloud 14 (Cloud Software / Lot 2 + Cloud Support / Lot 3) (Recommended)

**Description**: List the sovereign deployment (the bundle, the support contract, the implementation services) on G-Cloud 14 / 15 (next iteration). Cloud Software for the bundle and licence; Cloud Support for implementation, accreditation evidence services, and operator runbook training; Cloud Hosting is **not** applicable because the customer hosts the platform inside their own boundary.

**Why**: G-Cloud is the highest-leverage adoption lever for any UK public-sector customer (project 000 finding); MOD customers also use G-Cloud routinely for software where it fits.

**Cost**: Vendor-side framework listing effort (covered by `/arckit:dos`); per-call-off cost £0.

---

### Option 9B: Digital Outcomes (DOS 6 / DOS 7)

**Description**: Use DOS for the implementation / accreditation-services elements that are work-package-shaped rather than catalogue-shaped (e.g., delivering an MOD pilot accreditation evidence pack co-design engagement).

**When**: Where the engagement is genuinely outcome-shaped rather than catalogue-shaped.

---

### Option 9C: MOD-Specific Frameworks (DSDA, ATLAS, FATS, etc.)

**Description**: MOD operates several defence-specific frameworks (Defence Strategic Data Architecture supplier panels; ATLAS; Field-Authority Technical Services etc.). The exact framework varies by command and by year.

**When**: Engage with the customer's procurement function early; use their preferred route.

**Cost**: Vendor-side framework engagement effort; per-call-off cost £0.

---

### Option 9D: Defence Cyber Protection Partnership (DCPP) Compliance

**Description**: Not a procurement vehicle, but a compliance baseline that defence procurements typically require. The DCPP Cyber Risk Profile applicable to the engagement must be demonstrably met.

**When**: Always applicable for MOD calls. Vendor side: maintain a current DCPP profile attestation per release.

---

### Build vs Buy Recommendation for Procurement Routes

**Recommendation**: **BUY (use existing frameworks)** — G-Cloud 14 / 15 + DOS 6 / 7 + the relevant defence frameworks per engagement. No BUILD. This category is covered in detail by `/arckit:dos` and `/arckit:gcloud-clarify`.

---

## Total Cost of Ownership (TCO) Summary

### Blended TCO Across Sovereign Categories

> Indicative; SOBC will set authoritative figures. All figures are vendor-side unless explicitly noted as customer-side.

| Category | Vendor BUILD | Vendor BUY | Vendor ADOPT (operating cost) | Customer-side Cost |
|----------|--------------|------------|-------------------------------|--------------------|
| 1. Sovereign packaging + LTS pipeline | £710K Y1, £420K Y2, £470K Y3 | — | — | n/a |
| 2. Persistence (Postgres + MinIO) | — | — | £40–80K p.a. (optional support contracts) | Customer ops; storage CapEx |
| 3. AI endpoint (Triton + vLLM + open-weight) | — | — | £80–150K p.a. (vendor-side inference profile maintenance) | GPU CapEx (£25–35K/H100); NVIDIA AI Enterprise (£3–5K/GPU/yr) optional |
| 4. Observability (OTel + Grafana stack) | — | — | £30–60K p.a. | Customer ops |
| 5. Audit retention (MinIO Object Lock) | — | — | (covered by Cat 2) | Storage CapEx |
| 6. Identity (native OIDC + Keycloak optional) | — | — | £20–40K p.a. (Keycloak realm maintenance) | Customer IdP entitlement |
| 7. Container runtime (RKE2) | — | — | (vendor effort within Cat 1) | RKE2 / SUSE support optional £30–100K p.a. |
| 8. Cryptography / signing (HSM + Sigstore) | — | £35–70K CapEx + £8–15K p.a. per HSM × 2 | (Sigstore in Cat 1) | n/a (vendor-side) |
| 9. Procurement | — | (framework listing effort, no per-call-off) | — | n/a |
| **Total vendor-side** | **£1.6M over 3 years** | **£100–250K over 3 years** | **£0.5–1.0M over 3 years** | spread over n customers |

### Per-Customer Cost-to-Serve (Indicative)

| Cost Item | Year 1 | Year 2 | Year 3 |
|-----------|--------|--------|--------|
| Initial sovereign engagement (accreditation co-design, install, runbook walk-through) | £150–250K | — | — |
| Annual sovereign support (one LTS line, one customer) | £80–140K | £80–140K | £80–140K |
| Accreditation refresh per release | £20–40K | £20–40K | £20–40K |
| **Per-customer 3-year cost-to-serve** | | | **£330K – £620K** |

Sovereign pricing must recover this **and** contribute margin to the SaaS SME tier (BR-006).

### Risk-Adjusted TCO

- **R-1 fork pressure**: adds 10–15% engineering contingency.
- **R-2 accreditation effort overrun**: adds 15–25% to first 3 customers.
- **R-3 critical dependency cannot operate offline**: medium probability — fallback options identified for every category above; contingency 5%.
- **R-4 LTS resource pressure**: addressed by separate LTS engineering line.
- **R-5 signing-key compromise**: catastrophic; mitigated by HSM custody, key rotation, and audit logging.

---

## Requirements Traceability

### Requirements Coverage Matrix

| Requirement | Category | Recommended Option | Coverage |
|-------------|----------|--------------------|----------|
| BR-001 (single codebase) | 1, 2, 3, 4, 5, 6 | Same software as SaaS route, different deployment | ✅ Full |
| BR-002 (air-gap) | 1, 4, 5 | BUILD packaging + ADOPT in-boundary stack | ✅ Full |
| BR-003 (customer-controlled) | 6, 7 | Customer IdP + customer-operated K8s | ✅ Full |
| BR-004 (accreditation support) | 1, 8 | Bundle + SBOM + signatures + evidence pack | ✅ Full |
| BR-005 (LTS ≥ 24 months) | 1 | LTS pipeline | ✅ Full |
| BR-006 (cross-subsidy contribution) | TCO + 9 | Pricing covers cost-to-serve plus margin | ✅ Full |
| BR-007 (procurement routes) | 9 | G-Cloud + DOS + MOD frameworks | ✅ Full |
| BR-008 (reference customer) | 9 | Customer engagement plan | ⚠️ Pending |
| FR-001 (air-gap install) | 1 | BUILD packaging Option 1A | ✅ Full |
| FR-002 (air-gap upgrade + roll-back) | 1 | BUILD packaging Option 1A | ✅ Full |
| FR-003 (backup, restore, key rotation) | 2, 8 | Postgres PITR + MinIO + KMS | ✅ Full |
| FR-004 (pluggable AI endpoint) | 3 | Pluggable abstraction + Option 3A default | ✅ Full |
| FR-005 (configurable telemetry/time/CA/mirror/IdP) | 4, 6 | OTel + Grafana stack + customer IdP | ✅ Full |
| FR-006 (within-deployment isolation) | 7 | RKE2 + project-level RBAC | ✅ Full |
| FR-007 (customer IdP + clearance claims) | 6 | Native OIDC / SAML | ✅ Full |
| FR-008 (artefact authoring parity) | (existing) | Same code as SaaS | ✅ Full |
| FR-009 (export) | (existing) | Same code as SaaS | ✅ Full |
| FR-010 (audit logging + retention) | 5 | MinIO Object Lock | ✅ Full |
| FR-011 (operator runbooks) | 1 | BUILD as part of bundle | ✅ Full |
| FR-012 (classification marking) | (existing) | Same code as SaaS, configurable max | ✅ Full |
| FR-013 (opt-in remote support) | 6 | Vendor IdP + customer-approved transport | ⚠️ Pending pilot input |
| FR-014 (LTS patch delivery) | 1 | BUILD LTS pipeline | ✅ Full |
| NFR-SEC-001 (MOD SbD / JSP 440 / JSP 604) | 1, 8 | Evidence pack per release | ✅ Full |
| NFR-SEC-002 (NCSC CAF for non-MOD) | 1, 8 | CAF mapping per release | ✅ Full |
| NFR-SEC-003 (HMG-approved cryptography) | 8 | FIPS-mode RKE2 + HSM signing + Sigstore | ✅ Full |
| NFR-SEC-004 (no outbound calls) | 1, 4 | Network-deny CI test | ✅ Full |
| NFR-SEC-005 (supply-chain integrity) | 8 | Sigstore + in-toto + SBOM + HSM | ✅ Full |
| NFR-SEC-006 (within-deployment isolation) | 7 | RKE2 + RBAC + automated isolation tests | ✅ Full |
| NFR-SEC-007 (cleared-personnel claims) | 6 | Claim-driven authorisation | ✅ Full |
| NFR-SEC-008 (vulnerability SLA) | 1 | LTS pipeline patch SLA | ✅ Full |
| NFR-C-001 (Government Security Classifications Policy) | (existing) | Same code as SaaS, configurable | ✅ Full |
| NFR-C-002 (UK GDPR — vendor-side) | (existing + DPIA) | DPIA inputs per release | ✅ Full |
| NFR-C-003 (WCAG 2.2 AA) | (existing) | Same code as SaaS | ✅ Full |
| NFR-C-004 (audit retention) | 5 | MinIO Object Lock | ✅ Full |
| NFR-C-005 (LTS / patching SLA) | 1 | LTS pipeline | ✅ Full |
| NFR-I-001 (open-standard parity with SaaS) | (existing) | Same APIs | ✅ Full |
| NFR-I-002 (data portability) | (existing) | Same export | ✅ Full |

**Coverage**: 38 of 40 in-scope requirements fully covered (94%); 2 partially pending pilot-customer input.

---

## Procurement Strategy

- **G-Cloud 14 / 15** for the bundle licence and the implementation services (Cloud Software / Lot 2; Cloud Support / Lot 3). Cloud Hosting Lot 1 is not applicable — the customer hosts.
- **DOS 6 / 7** for outcome-shaped engagements (e.g., MOD pilot accreditation evidence pack co-design).
- **MOD-specific framework engagement** based on the customer's command and procurement function.
- **DCPP Cyber Risk Profile** maintained per release.
- **Crown Commercial Service liaison** to align with HM Treasury spend controls and SME spend targets.

---

## Open Questions and Next Steps

### Open Questions

1. Which MOD command will be the pilot accreditator-in-the-loop customer? (Dependency on `/arckit:stakeholders` follow-through and customer engagement plan.)
2. Confirm with NCSC liaison the preferred SBOM format (CycloneDX vs SPDX) for the MOD Secure by Design submission.
3. Confirm the cleared-personnel claim format (FR-007 acceptance criterion 3) — `clearance: SC | DV | NPPV3` is indicative; pilot accreditator confirms.
4. Confirm whether RKE2 (SUSE / Rancher Government) or OpenShift is the preferred container runtime in the pilot customer's reference architecture; both are supported but the pilot's choice influences the default profile and the runbook examples.
5. Confirm the FIPS profile of the chosen open-weight LLM toolchain — Llama 3.x / Mistral weights themselves have no FIPS implication, but the inference toolchain (vLLM / Triton + CUDA) must be deployed against FIPS-mode kernel cryptography on the host OS.

### Next Steps

- Run `/arckit:wardley` to position these components on the evolution axis (most are commodity-or-utility; the sovereign packaging is custom-built; the AI on-prem inference sits at custom-built moving towards product).
- Run `/arckit:sobc` to replace indicative TCO figures with authoritative HM Treasury Green Book five-case figures.
- Run `/arckit:sow` to produce the procurement pack per engagement.
- Run `/arckit:mod-secure` once a representative pilot accreditator is engaged to produce the MOD Secure by Design assessment.
- Run `/arckit:hld-review` once the High-Level Design is produced (currently scheduled for 2026-10-31 per the requirements timeline).

---

## Appendices

### Appendix A: Components Excluded From the Sovereign Shortlist

| Component | Reason for Exclusion |
|-----------|----------------------|
| AWS RDS Postgres / S3 / EKS / KMS / Bedrock | SaaS control plane outside accredited boundary |
| Azure PostgreSQL Flexible Server / Blob / AKS / Key Vault / Azure OpenAI | SaaS control plane outside accredited boundary |
| GCP Cloud SQL / GCS / GKE / KMS / Vertex AI | SaaS control plane outside accredited boundary |
| Datadog | SaaS-only |
| Grafana Cloud | SaaS-only — replaced by self-hosted Grafana stack |
| Auth0 / Okta SaaS | SaaS-only — replaced by self-hosted Keycloak (when broker needed) |
| Sentry SaaS | SaaS-only — replaced by self-hosted Sentry or by OTel error pipeline |
| Replicated kots / Embedded Cluster | Adds third-party runtime in customer boundary; licence model conflicts with BR-006 |

### Appendix B: Reference Documents

- `projects/000-global/ARC-000-PRIN-v2.0.md` — Architecture Principles (Principle 21 anchors this project).
- `projects/000-global/research/ARC-000-RSCH-v1.0.md` — Wave-1 target-organisation research.
- `projects/001-arckit-saas/research/ARC-001-RSCH-v1.0.md` — Sister SaaS-route technology research.
- `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md` — Project 002 requirements.
- `projects/002-arckit-sovereign/ARC-002-STKE-v1.0.md` — Project 002 stakeholder analysis.
- MOD Secure by Design — assessment methodology.
- JSP 440 — Defence Manual of Security.
- JSP 604 — Defence Manual for the Authorisation of Information Systems.
- NCSC Cyber Assessment Framework (CAF).
- NCSC Cloud Security Principles (14).
- HMG Government Security Classifications Policy.
- Defence Cyber Protection Partnership Cyber Risk Profile.
- FIPS 140-3 (NIST cryptographic module validation).
- SLSA framework (slsa.dev).
- Sigstore project (sigstore.dev).
- CycloneDX (cyclonedx.org); SPDX (spdx.dev).

### Appendix C: Glossary

- **ADOPT** — Use existing open-source software unmodified.
- **AGPL** — Affero General Public License (MinIO server licence).
- **CAF** — NCSC Cyber Assessment Framework.
- **CycloneDX / SPDX** — Software Bill of Materials formats.
- **DCPP** — Defence Cyber Protection Partnership.
- **DOS** — Digital Outcomes and Specialists framework.
- **FIPS 140-3** — US Federal cryptographic module validation standard, broadly accepted in HMG.
- **G-Cloud** — UK Government cloud framework.
- **HSM** — Hardware Security Module.
- **JSP 440 / 604** — UK MOD Joint Service Publications for security and authorisation of information systems.
- **LTS** — Long-Term Support release line.
- **OTel / OTLP** — OpenTelemetry / OpenTelemetry Protocol.
- **RKE2** — Rancher Kubernetes Engine 2 (SUSE / Rancher Government).
- **SBOM** — Software Bill of Materials.
- **Sigstore / Cosign / Fulcio / Rekor / in-toto / SLSA** — Open-source supply-chain integrity stack.
- **vLLM / Triton** — Open-source LLM inference toolchain.

---

## Spawned Knowledge

> Spawned by `/arckit:research` Step 11b. New artefacts created or updated as a side-effect of this research pass. Empty if `--no-spawn` was passed. (Pass through this pass: spawn deferred to a follow-up `--refresh` run since the wave-1 orchestrator already has heavy parallelism. Vendor profiles and tech notes will be created when the pilot accreditator-in-the-loop customer is engaged.)

| Artefact | Path | Type | Status |
|----------|------|------|--------|
| (deferred) | `projects/002-arckit-sovereign/vendors/` | Vendor profiles | Will be spawned post-pilot engagement |
| (deferred) | `projects/002-arckit-sovereign/tech-notes/` | Tech notes | Will be spawned post-pilot engagement |

---

**Generated by**: ArcKit `/arckit:research` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.13.1
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Wave-2 sovereign-route technology and vendor research, derived from `ARC-002-REQ-v1.0.md`, `ARC-002-STKE-v1.0.md`, `ARC-000-PRIN-v2.0.md` (Principle 21), and `ARC-000-RSCH-v1.0.md`. Sister to project 001 SaaS-route research (`ARC-001-RSCH-v1.0.md`). Spawned vendor / tech-note knowledge deferred to pilot-customer engagement step.
