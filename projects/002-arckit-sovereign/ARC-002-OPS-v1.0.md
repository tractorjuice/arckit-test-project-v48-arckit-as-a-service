# Operational Readiness Pack: ArcKit as a Service — Sovereign Deployment Route

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:operationalize`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-OPS-v1.0 |
| **Document Type** | Operational Readiness Pack |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Per release; on every LTS branch cut; on customer onboarding |
| **Next Review Date** | 2026-08-03 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, Vendor Security Lead, Sovereign Delivery Lead, LTS Engineering Lead, HSM Custody Officers, Customer Operator Liaison, MOD Defence Digital liaison, NCSC liaison |

## Revision History

| Version | Date | Author | Changes | Approved By |
|---------|------|--------|---------|-------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation. Vendor-side operational readiness for the sovereign release pipeline; customer-side handover model at accreditation. | [PENDING] |

---

## 0. Reading Note — Scope Boundary

**This OPS document is fundamentally different from a SaaS OPS pack.** The vendor does **not** operate the deployed instance. The deploying authority operates the deployed instance inside its accredited boundary, under its own Security Aspects Letter (SAL) and Authority To Operate (ATO) per ADR-006. This document scopes:

| Scope | Operated by | Documented here |
|-------|-------------|-----------------|
| **Vendor-side** — bundle issue + signing pipeline; LTS patch production; opt-in audited remote support; accreditation-evidence pack refresh; vulnerability disclosure + patch SLAs | Vendor (ArcKit as a Service) | YES — full SLOs, runbooks, on-call, DR/BCP |
| **Customer-side** — deployed-instance lifecycle; incident response inside boundary; access control; audit; deployed-instance DR/BCP | Deploying authority | NO — pointer only; customer's own OPS document |

The vendor-side operational scope is narrow and ceremony-driven; it is also non-negotiable in its supply-chain integrity guarantees.

---

## 1. Service Overview

### 1.1 Service Description

The "service" the vendor operates is the **sovereign release pipeline** plus the **customer-facing supply-chain and support functions** that sit around it. There is no live vendor-operated runtime serving customer traffic. The vendor's operational outputs are:

1. **Signed sovereign release bundles** (`arckit-sovereign-{LTS_YEAR}.{MINOR}.{PATCH}.bundle`) — produced from `main` and from each active LTS branch via the pipeline in `ARC-002-DEVOPS-v1.0.md`.
2. **LTS patch stream** — annual LTS cuts, monthly patch tags, out-of-band Critical/High hotfixes (per ADR-008).
3. **Per-release accreditation evidence pack** — MOD SbD assessment, NCSC CAF mapping, dual SBOM, SLSA L3 provenance, signing/custody attestations (per ADR-006).
4. **Opt-in audited remote support sessions** — only at customer request, only to cleared-personnel customers, never default-on (per ADR-003 / FR-013).
5. **Vulnerability disclosure intake + patch coordination** — ISO 29147 / 30111 aligned (per ADR-008 / NFR-SEC-008).

### 1.2 Service Tier

**Tier**: **Critical** for vendor-side supply-chain functions (signing pipeline, HSM custody, evidence-pack production).
**Tier**: **Important** for customer-facing support coordination (advisory channel, escalation triage).

**Justification**: Compromise or unavailability of the signing pipeline blocks every customer's ability to receive trusted updates, including security patches that may be running against the NFR-SEC-008 SLA. HSM custody compromise is the highest-impact failure mode in the entire architecture (ADR-002 R-ADR2-1). Conversely, the absence of vendor-operated customer runtime means traditional "tier-1 24/7 service availability" framing does not apply to the deployed instance.

### 1.3 Key Stakeholders

| Role | Owner | Responsibility |
|------|-------|----------------|
| Service Owner | Mark Craddock | Sponsor; LTS commitments; commercial sign-off; M-of-N HSM custody officer |
| Vendor Security Lead | [PENDING] | Supply-chain integrity; HSM custody; vulnerability triage; pen-test coordination |
| LTS Engineering Lead | [PENDING] | Backport workflow; patch SLA discipline; LTS branch maintenance |
| Sovereign Delivery Lead | [PENDING] | Bundle distribution; customer onboarding; verification ceremony support; advisory channel operator |
| Platform / SRE Lead | [PENDING] | Pipeline hardened-runner fleet; reproducibility cross-build; offline-CI environment |
| HSM Custody Officers (M-of-N) | [PENDING] panel | OVM signing quorum; key rotation; compromise response |
| Vendor DPO | [PENDING] | Distribution-metadata processing only (per DPIA vendor-narrow scope) |
| Customer Operator Liaison (per engagement) | [PENDING] | Single point of contact during opt-in remote support |

### 1.4 Dependencies

**Upstream (vendor pipeline depends on)**:

- Sigstore Fulcio + Rekor (transparency-profile selectable per ADR-002; `ovm-only` profile removes runtime dependency).
- HSM provider (FIPS 140-2 L3 / HMG-CAPS approved); single-vendor concentration risk per ADR-002 R-ADR2-8.
- Vendor-internal package mirror (snapshotted per release); upstream OSS registries (npm, PyPI, container registries) populate the mirror.
- GitHub (or equivalent) source-control + CI runner host.
- Vendor-internal observability (pipeline metrics; never customer runtime).

**Downstream (vendor pipeline output consumed by)**:

- Customer deploying authorities (MOD units, operators of essential services).
- Customer accreditators (consume evidence pack).
- Customer Operator Teams (consume bundle + runbooks).

---

## 2. Service Level Objectives (SLOs)

### 2.1 SLI / SLO Catalogue (Vendor-Side)

| ID | SLI | SLO Target | Error Budget | Source |
|----|-----|------------|--------------|--------|
| **SLO-OPS-001** | Bundle signing pipeline availability for scheduled LTS cuts and patch cycles | 99.0% of scheduled release windows met within 24 h | 1 missed window per 100 scheduled | DEVOPS §16.1 |
| **SLO-OPS-002** | End-to-end pipeline lead time from commit to releasable bundle | ≤ 4 hours wall-clock for full release pipeline | 5% of releases may exceed | DEVOPS §3.3 |
| **SLO-OPS-003** | Critical CVE patch bundle issuance | 100% within 7 calendar days | Zero tolerance — any miss is a P1 incident | NFR-SEC-008, ADR-008 |
| **SLO-OPS-004** | High CVE patch bundle issuance | 100% within 30 calendar days | Zero tolerance | NFR-SEC-008, ADR-008 |
| **SLO-OPS-005** | Medium CVE patch bundle issuance | ≥ 95% within 90 calendar days | 5% may slip with documented risk acceptance | NFR-SEC-008, ADR-008 |
| **SLO-OPS-006** | Reproducibility cross-build pass rate | 100% per release | Zero — any mismatch blocks release | DEVOPS §16.2 |
| **SLO-OPS-007** | Network-deny smoke pass rate | 100% per release | Zero | DEVOPS §16.2 |
| **SLO-OPS-008** | Bundle distribution time (vendor → customer accredited boundary) | ≤ 10 working days from bundle GA to delivered media for routine releases; ≤ 5 working days for Critical hotfixes | 10% may slip with customer agreement | ADR-007 |
| **SLO-OPS-009** | Advisory channel response (customer escalation acknowledged) | ≤ 4 working hours during UK business hours; ≤ 1 working day out-of-hours for Critical | 5% may slip | ADR-003 / FR-013 |
| **SLO-OPS-010** | Accreditation evidence pack production | 100% attached at GA of every release | Zero — gate in pipeline | ADR-006 |

### 2.2 SLO Breach Response

| SLO | Breach response |
|-----|-----------------|
| SLO-OPS-003 (Critical 7d) | P1 incident; Service Owner + Security Lead engaged within 1 h; customer advisory issued at miss notification; root cause within 5 working days |
| SLO-OPS-006 / 007 (reproducibility / network-deny) | Pipeline halt; release blocked; engineering investigation; customer advisory only if a previously released bundle is implicated |
| SLO-OPS-009 (advisory channel) | Sovereign Delivery Lead escalation to Service Owner; review of staffing model |

### 2.3 What Is Deliberately Not an SLO

- **Deployed-instance availability** — not the vendor's SLO; belongs to the deploying authority's own OPS document.
- **Mean Time To Recover for a customer-side incident** — same; vendor cannot observe.
- **End-user latency** — same; constrained by customer host envelope (NFR-P-001).

---

## 3. Support Model

### 3.1 Vendor-Side Support Tiers

| Tier | Function | Hours | Channel |
|------|----------|-------|---------|
| **L1 — Sovereign Delivery Desk** | Customer onboarding queries; bundle delivery logistics; verification-ceremony support; routine advisory triage | UK business hours (Mon–Fri 09:00–17:30) | Encrypted email + dedicated phone line; pre-agreed at onboarding |
| **L2 — Engineering Triage** | Bundle defect reports; reproducibility / verification failures; patch SLA escalations; opt-in remote support session arrangement | UK business hours, with on-call escalation for Critical | L1 escalation only |
| **L3 — Architecture / Security Lead** | Material design issues; vulnerability disclosures (ISO 29147); HSM custody events; release-pipeline compromise indicators | 24/7 on-call for P1 only | L2 escalation; or direct VDP intake (INT-010) |

### 3.2 Customer-Side Support Boundary (per ADR-003)

- **No default vendor remote access.** Vendor cannot SSH, RDP, or otherwise reach into the customer's accredited boundary as a default capability.
- **Opt-in audited remote support (FR-013)** is the only remote channel. Triggered by customer request; routed through the customer's own jump host or "watch-and-talk" telephony; bounded duration; full session recording delivered to customer SIEM; cleared-personnel-only on the vendor side.
- **Diagnostic-export tool** (ships in bundle) is the alternative — customer operator runs it inside boundary, customer chooses what (if anything) to release to vendor, transfer is via the same out-of-band channels as the inbound bundle.

### 3.3 Escalation Matrix

| Severity | Vendor-side response | Customer notification | Pager target |
|----------|----------------------|----------------------|--------------|
| **P1 — pipeline compromise indicator / suspected HSM key compromise / Critical CVE missed SLA** | < 15 min ack; war-room within 1 h | All active customers within 4 h via advisory channel | Service Owner + Security Lead + LTS Eng Lead + on-call SRE |
| **P2 — bundle defect requiring re-issue; reproducibility failure on a released bundle; missed High CVE SLA** | < 1 h ack | Affected customers within 24 h | Security Lead + LTS Eng Lead |
| **P3 — single-customer ceremony failure; advisory channel outage** | < 4 working hours | Affected customer | Sovereign Delivery Lead |
| **P4 — routine query; documentation clarification** | < 1 working day | Originating customer | L1 |

### 3.4 On-Call Rotation

Vendor on-call covers **pipeline + supply-chain + advisory channel**, not customer runtime.

| Rota | Members | Schedule | Triggers |
|------|---------|----------|----------|
| Pipeline / SRE | 4 engineers minimum | 1-week shifts, 24/7 for P1 | Pipeline halt, reproducibility failure, signing job failure, distribution staging failure |
| Security on-call | Security Lead + 1 deputy | 1-week shifts, 24/7 for P1 | VDP intake, suspected compromise, missed Critical patch SLA |
| HSM custody quorum | M-of-N officers | Always-available roster (any M reachable within 24 h) | OVM signing job; out-of-band hotfix |

Burnout-prevention guard-rails: maximum 1-in-4 frequency per engineer; mandatory week off on-call after a P1; quarterly rota review.

### 3.5 Out-of-Hours Procedures

UK out-of-hours (after 17:30 weekday, all weekend, public holidays): only P1 triggers active-page; P2 and below queue to next working day with email acknowledgement. Customer advisory channel publishes a brief out-of-hours response statement on each release window.

---

## 4. Monitoring & Observability (Vendor Pipeline Only)

### 4.1 Vendor Pipeline Health

| Signal | Source | Dashboard | Alert |
|--------|--------|-----------|-------|
| Pipeline run success/fail | CI runner | Sovereign Pipeline dashboard | P2 on fail of release-tagged run |
| Reproducibility digest match | Cross-build job | Sovereign Pipeline dashboard | P2 on mismatch |
| Network-deny smoke packet count | Offline-test runner | Sovereign Pipeline dashboard | P1 if non-zero |
| HSM signing job success | Signing runner | Custody dashboard | P1 on fail |
| HSM access events | HSM provider audit log | Custody dashboard | P1 on unauthorised access pattern |
| Bundle hash manifest publication | Public hash endpoint | Distribution dashboard | P2 on fail |
| Advisory channel queue depth | Sovereign Delivery Desk | Support dashboard | P3 if SLA at risk |
| LTS patch-SLA timer (per CVE) | Vulnerability tracker | LTS Health dashboard | P1 at -24 h, P2 at -7 days |

### 4.2 Customer-Runtime Observability

**The vendor sees nothing inside the customer's accredited boundary.** This is by design (Principle 6 sovereign clause + Principle 21 + ADR-005). Customer operates its own SIEM, dashboards, and alerting. The bundle ships reference dashboard configurations (Grafana / equivalent) that the customer may import into its own observability stack — no telemetry returns to the vendor.

### 4.3 Health-Check Endpoints (Bundle-Shipped)

Documented in the bundle's operator runbook set, executed inside the customer boundary, never reachable from outside it.

---

## 5. Alerting Strategy

### 5.1 Alert Routing

| Alert | Routing |
|-------|---------|
| P1 pipeline / supply-chain | PagerDuty (or equivalent) → Pipeline on-call + Security on-call simultaneously; auto-creates war-room channel |
| P2 release defect | PagerDuty → Security on-call + LTS Eng Lead |
| P3 distribution / advisory | Email + ticket queue → Sovereign Delivery Desk |
| Customer-originated VDP intake | Dedicated mailbox + ticket; auto-acknowledge; Security on-call paged for Critical/High self-reported severity |

### 5.2 Severity Definitions

P1: Customer-trust impact (signing key suspect; released bundle proven defective; missed Critical patch SLA).
P2: Pipeline blocked or imminent SLA risk.
P3: Single-customer or non-blocking issue.
P4: Routine.

### 5.3 Alert Fatigue Controls

- Reproducibility-drift alerts deduplicated by digest pair; one ticket per pair per 24 h.
- Network-deny packet alerts grouped by destination CIDR; one ticket per destination.
- HSM access "expected-quorum" events suppressed when quorum approval is in-flight.
- Quarterly alert review with the SRE rota; targets: < 5 false-positive P1s per quarter.

---

## 6. Runbooks (Vendor-Side)

The vendor-side runbook library covers **pipeline operations + supply-chain ceremony + customer-facing coordination**. Customer-side runbooks (install, upgrade, backup, restore, key rotation, decommission, incident response inside boundary) ship in the bundle per FR-011 and are the deploying authority's responsibility to execute.

### 6.1 RB-VEN-001 — Bundle Issue (Routine LTS Cut or Monthly Patch)

**Purpose**: Produce, sign, and stage a sovereign release bundle for distribution.

**Prerequisites**: Signed commit on `main` (annual cut) or active `release/lts-YYYY` branch; release approver sign-offs (Service Owner + Product Manager sovereign track + Security Lead); HSM custody quorum reachable.

**Detection**: Calendar-driven (annual LTS cut date; monthly patch cycle date) or trigger-driven (Critical/High CVE — see RB-VEN-002).

**Steps**:

1. Tag the release: `git tag arckit-sovereign-{LTS_YEAR}.{MINOR}.{PATCH}` on the appropriate branch; push tag.
2. Verify CI fires the `sovereign-release` workflow (`pipelines/sovereign/release.yml`); confirm runner pool is hardened-SLSA-L3.
3. Monitor build job; on completion, confirm reproducibility cross-build digest match (SLO-OPS-006).
4. Monitor offline-profile + network-deny smoke; confirm zero outbound packets (SLO-OPS-007).
5. Monitor SBOM emission (CycloneDX 1.5 + SPDX 2.3) and SLSA L3 provenance attestation; confirm Cosign keyless signatures applied to all images.
6. Trigger HSM signing job; convene M-of-N custody quorum approval (in-person or via secure channel per custody policy); confirm OVM signed.
7. Confirm bundle assembly produces `arckit-sovereign-{version}.bundle` with all artefacts, OVM, embedded trust roots, `arckit-verify` static binary, and operator runbook set.
8. Publish bundle hash manifest to vendor public endpoint.
9. Hand bundle to Sovereign Delivery Lead for distribution staging (RB-VEN-004).
10. Update release register; attach evidence pack (RB-VEN-003).

**Verification**: Pipeline dashboard shows all gates green; OVM signature verifies against pinned HSM cert on a clean test environment; bundle hash manifest matches OVM-recorded digest.

**Escalation**: Any gate fail → P2; HSM signing failure or quorum unreachable → P1 to Security Lead.

**Rollback**: Revert tag; cut a new tag; re-run pipeline. Defective bundles are *superseded* (not revoked) per DEVOPS §4.5.

### 6.2 RB-VEN-002 — Hotfix Release (Critical / High CVE)

**Purpose**: Produce, sign, and stage an out-of-band patch bundle within NFR-SEC-008 SLA (Critical 7d / High 30d).

**Prerequisites**: VDP intake or self-discovered CVE; severity classified by Security Lead; fix landed on `main`; backport branches identified (every active LTS).

**Detection**: VDP intake mailbox; CVE feeds against current SBOM; pen-test finding.

**Steps**:

1. Security Lead classifies severity and starts SLA timer (Critical 7d / High 30d / Medium 90d). Log timer in vulnerability tracker.
2. Engineering creates fix on `main`; commits with `sec(crit):` or `sec(high):` prefix.
3. LTS Engineering Lead assigns backport tickets to every active LTS branch.
4. Each backport PR runs the full sovereign pipeline (reproducibility, network-deny, dual SBOM, SLSA L3, HSM OVM signing).
5. On all green: tag `arckit-sovereign-{LTS_YEAR}.{MINOR}.{PATCH}-cveXXXX` on each affected LTS; trigger RB-VEN-001 from step 4.
6. Trigger expedited distribution (RB-VEN-004 with Critical-priority courier scheduling — 5 working day target).
7. Issue customer advisory (RB-VEN-005) at bundle GA, *not* at fix-availability — avoid pre-disclosure.
8. Track customer-by-customer install confirmation; close SLA timer on each customer's confirmed install or on a documented customer-side risk acceptance.

**Verification**: Vulnerability tracker shows fix landed on every active LTS within SLA; advisory issued; all customers acknowledged.

**Escalation**: SLA timer < 24 h with backport not green → P1 to Service Owner. Customer cannot install within their accreditation window → coordinated with customer's own change board; not a vendor SLA breach.

**Rollback**: Same as RB-VEN-001 — supersession only.

### 6.3 RB-VEN-003 — Accreditation Evidence Pack Refresh

**Purpose**: Produce the per-release evidence pack consumed by customer accreditators (per ADR-006).

**Prerequisites**: Bundle GA candidate; current MOD SbD assessment; current NCSC CAF mapping; current DPIA; current risk register.

**Detection**: Pipeline gate "MOD SbD evidence pack current" (DEVOPS Appendix A item 8) — runs as an automated CI job (`/arckit:mod-secure` invocation).

**Steps**:

1. Run `/arckit:mod-secure` for project 002 against the candidate release; verify diff vs prior release is clean (no new high-confidence findings unaddressed).
2. Refresh NCSC CAF mapping (Section 15 of DEVOPS); attach to release.
3. Refresh DPIA delta (vendor-narrow scope per ARC-002-DPIA-v1.0).
4. Refresh risk register delta (per ARC-002-RISK-v1.0).
5. Bundle dual SBOM (CycloneDX 1.5 + SPDX 2.3) + SLSA L3 provenance into evidence pack.
6. Sign evidence pack alongside bundle (OVM contains evidence-pack hash).
7. Make evidence pack available to customer accreditators via the pre-agreed delivery channel (typically same as bundle).

**Verification**: Evidence pack hash recorded in OVM; customer accreditator receipt confirmed.

**Escalation**: New unaddressed high-confidence finding → P2; Security Lead reviews; release may proceed with documented risk acceptance only with Service Owner sign-off.

**Rollback**: N/A — evidence pack tracks the bundle; supersession applies.

### 6.4 RB-VEN-004 — Patch-Bundle Distribution (Sealed Media or Diode)

**Purpose**: Move signed bundle from vendor staging into customer accredited boundary per ADR-007.

**Prerequisites**: Bundle complete; OVM signed; hash manifest published; customer transfer mechanism agreed at onboarding (sealed media default; diode option).

**Detection**: RB-VEN-001 step 9 hand-off.

**Steps (sealed media — default)**:

1. Sovereign Delivery Lead writes bundle to encrypted media (AES-256, customer-supplied or pre-agreed encryption key per onboarding).
2. Compute media-level integrity hash (SHA-512); cross-check against OVM-recorded bundle digest.
3. Apply tamper-evident seals; record seal serial numbers in chain-of-custody log.
4. Engage approved courier (per onboarding contract); manifest released only to courier and named customer recipient.
5. Track courier; receive delivery confirmation; record in CoC log.
6. Customer Operator Liaison confirms seal intact + media decrypts; runs verification ceremony (DEVOPS §4.4 Appendix C); confirms PASS.

**Steps (one-way diode — option)**:

1. Sovereign Delivery Lead delivers bundle to customer-accredited diode operator.
2. Bundle traverses diode; vendor side observes diode-acknowledged write completion; no return signal.
3. Customer operator runs verification ceremony.
4. Any return signal (e.g., verification failure report) flows via separate runbook (advisory channel) — never back through the diode.

**Verification**: Customer ceremony PASS confirmation logged in CoC.

**Escalation**: Seal compromise during transit → P1 (treat as potential supply-chain compromise); bundle re-issued; courier audit.

**Rollback**: Re-issue and re-distribute; old bundle marked superseded in OVM advisory.

### 6.5 RB-VEN-005 — Customer Escalation Through Cleared Support Channel

**Purpose**: Handle a customer-originated escalation (defect report, suspected vulnerability, install/ceremony failure, upgrade issue) without breaching ADR-003 default-deny remote-access posture.

**Prerequisites**: Customer onboarding complete; advisory channel encryption keys exchanged; cleared-personnel roster published to customer; opt-in remote support template signed (or signable) at customer choice.

**Detection**: Customer-initiated message on advisory channel; or VDP intake (INT-010) if vulnerability-classified.

**Steps**:

1. L1 Sovereign Delivery Desk acknowledges within SLO-OPS-009 (4 working hours UK business hours).
2. Triage by severity and class (defect / vulnerability / install / advisory).
3. If vulnerability: route to Security Lead (RB-VEN-002 if Critical/High).
4. If defect / install / upgrade: L2 engineering triage; reproduce in vendor-side replica environment (DEVOPS Section 8.3 — `sovereign-offline-test`); issue diagnostic guidance to customer.
5. If reproduction fails or customer requests deeper engagement: offer **opt-in audited remote support** per ADR-003:
   1. Customer approves session (SIRO-level approval if required by their SAL).
   2. Customer provisions jump host or watch-and-talk telephony.
   3. Vendor-side cleared personnel (named on roster) join.
   4. Session recorded; recording delivered to customer SIEM; audit-event hash chain extended.
   5. Session bounded (typical 2 h max; explicit extension only).
6. Alternative: **diagnostic-export tool** runs inside customer boundary; customer chooses what to release; transfer via inbound advisory channel.
7. Resolution; root-cause documented; if defect → RB-VEN-001 supersession path; if security-relevant → RB-VEN-002.

**Verification**: Customer confirms resolution; ticket closed with classification (defect/vuln/operator/advisory); session recording delivered (if remote support used).

**Escalation**: Customer reports active compromise indicator → P1 immediately (vendor + customer joint war room within 4 h, *no* vendor reach into customer environment).

**Rollback**: N/A.

### 6.6 RB-VEN-006 — HSM Key Compromise / Suspected Compromise Response

**Purpose**: Respond to suspected or confirmed HSM signing-key compromise (per ADR-002 §11 + DEVOPS §9.4).

**Detection**: HSM custody-officer report; unauthorised access pattern in HSM audit log; pen-test finding; external disclosure.

**Steps**:

1. Security Lead declares P1; Service Owner notified within 15 min.
2. Pipeline halt — no further OVM signing until compromise scope determined.
3. War room: Security Lead + Service Owner + Lead Architect + HSM Custody Officers (M-of-N); HSM provider engaged.
4. Forensic preservation of HSM audit logs; sealed.
5. Customer advisory issued within 4 h (advisory channel) — guidance to halt installs of any in-flight bundles signed under suspect key window.
6. New HSM key commissioned (RB-VEN-007 — key rotation, accelerated).
7. All in-flight bundles re-signed under new key; new HSM cert distributed to customers out-of-band (multiple channels, per DEVOPS §9.2).
8. Customers pin new cert; verify new bundles; supersede compromised-window bundles.
9. Public post-incident review (redacted as appropriate); NCSC notified per supply-chain guidance.

**Verification**: All customers confirmed pinning new cert; old key marked revoked in custody log.

**Escalation**: National-level if exploitation evidence → NCSC + cross-government per agreed contact tree.

**Rollback**: N/A — supersession only.

### 6.7 RB-VEN-007 — HSM Key Rotation (Routine Annual)

**Purpose**: Annual rotation of long-lived HSM signing key (per ADR-002 R-ADR2-1 mitigation).

**Prerequisites**: New HSM key generation ceremony scheduled; M-of-N custody officers booked; customer-coordination window agreed.

**Steps**:

1. Generate new HSM key inside HSM (never extracted); record new public cert.
2. M-of-N custody officers attest key generation event.
3. Distribute new HSM cert to customers via multiple out-of-band channels (G-Cloud register, onboarding pack, contract envelope, advisory channel) with ≥ 60-day notice before first bundle signed under new key.
4. Customer pins new cert in addition to old (transition window).
5. First post-rotation bundle signed under new key + cross-signed under old key for transition (per ADR-002 OVM dual-signature option).
6. Subsequent bundles signed new-key-only.
7. Old key retired (still in HSM, marked retired in custody log; not destroyed for forensic continuity).

**Verification**: All customers confirmed pinning new cert before old-key retirement.

**Escalation**: Any customer fails to pin new cert in window → P2; coordinated extension or per-customer mitigation.

### 6.8 RB-VEN-008 — Pipeline Reproducibility Failure

**Purpose**: Diagnose and resolve reproducibility cross-build digest mismatch (DEVOPS §3.2 Stage 2).

**Detection**: Pipeline dashboard reports digest mismatch between two hardened runners.

**Steps**:

1. Pipeline halts at reproducibility gate; release blocked.
2. SRE on-call collects build logs from both runners; preserves intermediate artefacts.
3. Engineering investigates non-determinism source (timestamp baked in, locale, build-tool version drift, unpinned dependency).
4. Fix on `main`; re-run pipeline; confirm reproducibility passes.
5. If a previously released bundle is implicated (i.e., the non-determinism existed in past pipelines): customer advisory; supersede affected bundles; treat as potential P1 supply-chain integrity event.

**Verification**: Two independent runners produce byte-identical digests for at least 3 consecutive release-tagged builds.

**Escalation**: Recurring (> 2 in a quarter) → architecture review of build hermeticity; INFO-only if isolated.

### 6.9 RB-VEN-009 — Network-Deny Smoke Failure

**Purpose**: Investigate non-zero outbound packet capture during offline-profile smoke test.

**Detection**: Packet-capture log shows ≥ 1 outbound packet during install / upgrade / backup / restore / decommission test.

**Steps**:

1. Pipeline halts; release blocked (Principle 21 validation gate failed).
2. Identify destination CIDR/host of outbound packet; identify source process.
3. Trace to feature-flag default in `profiles/sovereign.yaml` (likely a new endpoint introduced without default-deny).
4. Engineering fix: add feature flag; default-deny in sovereign profile; re-run.
5. PR review root-cause: enforce PR-level "new outbound endpoint?" check (DEVOPS §3.2 Stage 1 sovereign gate).

**Verification**: Network-deny smoke records zero outbound packets across full lifecycle.

**Escalation**: Same destination repeats → architecture review of dependency.

### 6.10 RB-VEN-010 — Vulnerability Disclosure Intake

**Purpose**: Process inbound vulnerability disclosure per ISO 29147, ADR-008, INT-010.

**Detection**: VDP mailbox; coordinated disclosure from researcher / customer / partner; bug bounty (if active).

**Steps**:

1. Acknowledge within 1 working day; assign tracking ID; engage Security Lead.
2. Verify and reproduce in vendor-side replica.
3. Classify severity (CVSS + customer-impact judgement); start SLA timer (NFR-SEC-008).
4. Coordinate disclosure timeline with reporter (default: 90-day standard disclosure; expedited for actively exploited).
5. Trigger RB-VEN-002 (hotfix release).
6. Issue advisory at bundle GA (RB-VEN-005 path).
7. Public CVE entry (where appropriate); credit reporter (where consented).

**Verification**: SLA timer closed; reporter informed; advisory issued; CVE published.

**Escalation**: Active exploitation → P1; cross-customer rapid notification.

---

## 7. Disaster Recovery (Vendor-Side Pipeline)

### 7.1 Strategy

**Active-passive** for the build / signing pipeline. Primary vendor build region (UK-resident, per Principle 7) with a warm-standby second region. HSM has its own DR construct via the HSM provider (M-of-N quorum reachable from a second site; key material never leaves HSM cluster).

### 7.2 RTO / RPO (Vendor Pipeline)

| Asset | RTO | RPO |
|-------|-----|-----|
| Source-control + CI runner pool | 4 h | 0 (Git is content-addressable; replicated) |
| HSM signing service | 8 h (HSM provider DR + new quorum convening) | 0 (signing is event-based; no state to recover) |
| Vendor-internal package mirror snapshot store | 24 h | 0 (signed, content-addressable) |
| Bundle artefact cold storage | 24 h | 0 (immutable, replicated to second UK region) |
| Vulnerability tracker + LTS health dashboard | 24 h | < 1 h (continuous replication) |
| Advisory channel (encrypted email + ticket queue) | 4 h | < 1 h |

### 7.3 Failover Procedure

1. Service Owner declares DR event.
2. CI runner pool standby promoted; build can resume.
3. HSM provider DR procedure invoked (provider-led); new quorum site convened.
4. Bundle artefact storage replication confirmed; new uploads route to surviving region.
5. Customer advisory issued (advisory channel) — SLA timers on in-flight Critical CVEs may pause with customer agreement.

### 7.4 Failback

Once primary recovers: re-replicate any drift; resume primary; standby returns to warm.

### 7.5 DR Test Schedule

- Annual full DR exercise (commit → bundle in DR region only).
- Quarterly partial drill (CI runner failover; HSM provider drill in their cadence).
- **Last DR test**: NOT YET RUN (vendor pipeline pre-GA — first full DR exercise scheduled before first customer install per BLOCKING-03 from HLD review).

### 7.6 Customer-Side DR/BCP — Pointer Only

**The deployed instance's DR/BCP is the deploying authority's responsibility.** Per ADR-001 §10.2 and FR-003, the bundle ships:

- Backup runbook (customer-managed KMS keys; offline encrypted backup).
- Restore runbook with point-in-time recovery against customer storage.
- DR-failover runbook for customer's own multi-site deployment if provisioned.
- RPO ≤ 60 min and RTO ≤ 8 h targets per NFR-A-002 — these targets are **achievable** given the runbook + customer hardware envelope, but the **achievement** is the customer's operational responsibility, validated annually in their own DR drill (NFR-A-002).

The vendor will NOT operate, observe, or validate the customer's deployed-instance DR. The vendor may, on opt-in audited remote support (RB-VEN-005), advise on a runbook step the customer is executing.

---

## 8. Business Continuity (Vendor-Side)

### 8.1 Business Impact Analysis

| Vendor function | Impact of loss | RTO commitment |
|-----------------|----------------|----------------|
| Bundle signing pipeline | Cannot issue patches; SLA breaches accumulate; customer trust impact | 8 h (HSM DR) |
| Advisory channel | Cannot communicate to customers; incident coordination impaired | 4 h |
| LTS engineering rota | Backports stall; SLAs at risk (discovered, not immediate) | 2 working days (re-staffing) |
| Customer onboarding capacity | New customer engagements stall; commercial pipeline impact | 5 working days |

### 8.2 Manual Workarounds

- **Pipeline outage** — pre-staged "emergency hotfix" workflow on a hardened laptop with HSM access (M-of-N officers physically convened) can produce a single signed bundle if the main CI is unavailable for > 48 h. Constrained, audited, exception-only.
- **Advisory channel outage** — fallback to pre-agreed alternate channel (per onboarding pack); typically a second encrypted-email domain plus phone.
- **Customer install partner unavailable (vendor side)** — customer self-serve via runbooks shipped in bundle; vendor not on critical path.

### 8.3 Communication Plan

| Audience | Trigger | Channel | Owner |
|----------|---------|---------|-------|
| All active customers | P1 with customer-trust impact | Advisory channel + per-customer phone roster | Sovereign Delivery Lead |
| MOD Defence Digital liaison | P1 affecting MOD-classified deployments | Pre-agreed liaison contact | Service Owner |
| NCSC liaison | Supply-chain compromise indicator | Pre-agreed liaison contact | Security Lead |
| Internal team | Any P1 | War-room channel | On-call lead |
| Commercial contacts | Material disruption > 48 h | Email + phone | Service Owner |

### 8.4 BCP Activation Criteria

Service Owner declares BCP on: pipeline outage > 24 h, suspected HSM compromise, advisory channel outage > 4 h during active P1, key personnel unavailability for > 48 h with active SLA timer.

### 8.5 Recovery Priorities

1. Restore signing pipeline integrity (HSM + CI runner).
2. Restore advisory channel.
3. Restore evidence-pack production (RB-VEN-003).
4. Restore LTS engineering capacity.
5. Restore customer onboarding capacity.

---

## 9. Backup & Restore (Vendor-Side)

| Asset | Backup | Retention | Verification |
|-------|--------|-----------|--------------|
| Source-control | Git mirror, second UK region, hourly | LTS lifetime + 2 y | Daily clone test |
| CI configuration | IaC, version-controlled | Same as source | Re-apply test quarterly |
| Bundle artefacts (cold storage) | Object store, second UK region, immediate replication | LTS lifetime + 2 y | Quarterly restore-and-verify |
| SBOM / SLSA / Rekor archive | Object store, replicated | LTS lifetime + 2 y | Quarterly hash-match |
| HSM custody log | Append-only, replicated, signed | 7 y minimum (legal hold) | Continuous integrity check |
| Vulnerability tracker | DB backup, daily | 7 y | Quarterly restore drill |

Customer-side backups are not vendor-administered. The bundle ships backup runbooks for customer use (FR-003).

---

## 10. Capacity Planning (Vendor-Side)

| Capacity dimension | Current baseline (pre-GA) | 6-mo | 12-mo | 24-mo |
|--------------------|---------------------------|------|-------|-------|
| Active LTS lines | 0 | 1 (first cut) | 2 (current + previous) | 2 (steady-state per ADR-008) |
| Active customers | 0 | 1 (pilot) | 3–5 | 8–12 |
| Releases/year per LTS | — | 12 (monthly) + ad hoc CRIT | 12 + ~4 CRIT | 12 + ~4 CRIT × 2 LTS lines |
| HSM signing events/year | — | ~16 | ~32 | ~64 |
| Advisory tickets/month | — | < 10 | 20–40 | 60–100 |
| LTS engineering FTE | 0 | 2 | 3 | 4 |

Scaling triggers: > 3 active customers → add Sovereign Delivery Desk capacity; > 2 LTS lines → re-evaluate ADR-008 24-month commitment; HSM signing events > 100/y → capacity-plan HSM provider tier.

---

## 11. Security Operations

### 11.1 Access Management (Vendor Side)

- Cleared-personnel only on the named roster published to each customer (per ADR-003); roster signed; rotation documented.
- HSM custody quorum membership rotated annually (DEVOPS §9.3).
- Pipeline access via short-lived OIDC identities; no long-lived credentials.
- Audit log of all vendor-side pipeline + HSM access events; ≥ 7 y retention.

### 11.2 Secret Rotation

- HSM long-lived signing key — annual (RB-VEN-007) or on suspicion (RB-VEN-006).
- Vendor pipeline OIDC certs — short-lived per build.
- Customer-pinned HSM cert — same lifecycle as HSM key.

### 11.3 Vulnerability Scanning

- Continuous SBOM-driven scanning of all dependencies in active LTS bundles against CVE feeds.
- Weekly scheduled scans against the vendor build environment.
- Annual independent pen test of build pipeline + `arckit-verify` (NFR-SEC-005).
- NCSC VMS — vendor build estate enrolled where applicable; NCSC VMS is not directly applicable to the customer-deployed instance (it sits inside the customer boundary), but the vendor-side scanning evidence references VMS-comparable benchmarks (8-day domain / 32-day general) for vendor infrastructure, while the customer-deployed-instance patching is governed by the bundle SLAs below.

### 11.4 Vulnerability Remediation SLAs

Per ADR-008 / NFR-SEC-008, time-to-bundle-issue:

| Severity | SLA | Source |
|----------|-----|--------|
| Critical | 7 calendar days from triage | NFR-SEC-008, SLO-OPS-003 |
| High | 30 calendar days | NFR-SEC-008, SLO-OPS-004 |
| Medium | 90 calendar days | NFR-SEC-008, SLO-OPS-005 |
| Low | Next monthly patch cycle (≤ 30 days typical) | ADR-008 |

These SLAs measure **vendor time to issue a signed patch bundle**. The customer's time to install is governed by the customer's own change-management and accreditation process — not a vendor SLA.

### 11.5 Patch Management

- Monthly patch tag from each active LTS branch.
- Out-of-band tag for Critical/High CVEs.
- Patches are signed identically to full bundles; same verification ceremony; same distribution channel.
- Compliance metrics tracked on LTS Health dashboard; 100% adherence target.

### 11.6 Penetration Testing

- Annual on build pipeline + `arckit-verify` (independent assessor).
- Customer-side pen test of deployed instance is the customer's responsibility; vendor provides reference test scope.

### 11.7 Security Incident Contacts

| Type | Contact |
|------|---------|
| VDP intake | INT-010 / pre-agreed VDP mailbox |
| HSM compromise | Security Lead 24/7 page |
| Customer-reported active exploitation | Sovereign Delivery Lead → Security Lead P1 |
| NCSC liaison | Pre-agreed contact tree |
| MOD Defence Digital liaison | Pre-agreed contact tree |

---

## 12. Deployment & Release

Vendor-side "deployment" is *bundle issue + distribution staging*; customer-side install/upgrade is the deploying authority's job. See DEVOPS Sections 3, 4, 13 for full pipeline; this OPS section documents only the operational checklist:

- Annual LTS cut on fixed calendar date.
- Monthly patch cycle on fixed monthly date per LTS line.
- Out-of-band hotfixes on Critical/High SLA timers.
- Rollback = supersession (no certificate revocation; offline customers cannot reach a CRL).
- Database migrations are customer-side; bundle includes forward + rollback migrations executable inside boundary.
- No vendor blue-green or canary at customer site; customer chooses install pattern (typically dry-run on `customer-non-prod`, then `customer-prod`).

---

## 13. Knowledge Transfer & Training

### 13.1 Vendor-Side Training

| Audience | Training | Cadence |
|----------|----------|---------|
| New SRE / pipeline engineer | Day-1 verification ceremony walkthrough on a sample bundle (DEVOPS §10.3) | Per joiner |
| HSM custody officer | M-of-N quorum drills + custody policy | Annual + per-officer rotation |
| Sovereign Delivery Desk (L1) | Customer ceremony coaching scripts + advisory channel etiquette | Quarterly refresh |
| Security on-call | Compromise-response RB-VEN-006 tabletop | Annual |
| LTS engineering | Backport tooling + SLA discipline | Per joiner + quarterly refresh |

### 13.2 Customer-Side Training (Onboarding Hand-Over)

At customer accreditation hand-over (Section 14 below), the vendor delivers:

- Operator runbook walkthrough (install / upgrade / backup / restore / key rotation / decommission, FR-011).
- Verification ceremony rehearsal (using a sample bundle).
- Advisory channel onboarding (encryption keys exchanged, named contacts, escalation tree).
- Diagnostic-export tool walkthrough.
- Reference dashboards import (customer choice to use).
- Q&A and runbook-tailoring session for customer-specific topology.

### 13.3 Knowledge Base

- Vendor-internal: pipeline runbooks, on-call playbooks, incident post-mortems.
- Customer-facing: bundle-shipped runbook set + advisory archive.
- ADRs (ADR-001..008) are required reading for every new engineer touching the sovereign overlay.

---

## 14. Customer Accreditation Hand-Over Model

This section is the **load-bearing operational hand-over** that distinguishes sovereign OPS from SaaS OPS.

### 14.1 Hand-Over Trigger

When the deploying authority issues its ATO under JSP 604 (or comparable civilian SbD process) for a specific deployed instance, the vendor's role for that instance shifts from "delivery / install support" to "supply chain + LTS patch stream + opt-in support". The hand-over event is the operational pivot.

### 14.2 Hand-Over Checklist (Vendor → Customer)

Vendor confirms before hand-over:

- [ ] Bundle delivered, verified, installed in `customer-prod`.
- [ ] Operator runbook walkthrough completed; customer signs off.
- [ ] Verification ceremony rehearsed at customer site.
- [ ] Advisory channel keys exchanged; named contact tree confirmed both sides.
- [ ] HSM cert pinned in customer accredited environment.
- [ ] Diagnostic-export tool walkthrough completed.
- [ ] Reference IaC for foundational services (NTP, CA, mirror, IdP, KMS, observability, AI endpoint stub) handed over.
- [ ] Customer SIEM ingesting hash-chained audit (FR-010).
- [ ] Patch-cadence calendar (annual LTS + monthly) communicated; first quarter dates booked.
- [ ] Vulnerability disclosure expectations agreed (customer reports findings; vendor RB-VEN-010 intake).
- [ ] Opt-in remote support template signed (or signable-on-demand) per ADR-003.
- [ ] Customer-side DR/BCP plan in place (customer responsibility; vendor confirms presence, not contents).
- [ ] Accreditation evidence pack delivered + accepted by customer accreditator.
- [ ] Hand-over signed by Service Owner + Sovereign Delivery Lead + Customer Operator Liaison + Customer Accreditator + Customer SIRO.

### 14.3 Post-Hand-Over Vendor Obligations

After hand-over, the vendor's obligations narrow to:

- Continue producing signed bundles + LTS patches per SLO catalogue.
- Maintain advisory channel.
- Honour vulnerability disclosure SLAs (NFR-SEC-008).
- Refresh evidence pack each release.
- Provide opt-in remote support on request.
- Notify customer ≥ 12 months before LTS line deprecation (BR-005).
- **Not** operate, monitor, or audit the deployed instance.

### 14.4 Post-Hand-Over Customer Obligations

After hand-over, the deploying authority's obligations are documented in **its own** OPS pack (not this one). For traceability the vendor expects the customer to operate:

- Deployed-instance availability monitoring.
- Incident response inside boundary.
- Access control (cleared-personnel via customer IdP).
- Audit log review (customer SIEM).
- Backup, restore, key rotation, DR (using bundle-shipped runbooks).
- Re-accreditation cadence (per JSP 604 / department SbD).
- Engagement with vendor advisory channel for upgrades and patches.

### 14.5 Decommission Hand-Back

When the customer decommissions the deployed instance:

- Customer follows decommission runbook in bundle (FR-011 / UC-3).
- Customer destroys keys per its own KMS lifecycle.
- Customer confirms decommission to Sovereign Delivery Desk (advisory channel).
- Vendor closes the customer's entry in the active customer register; HSM cert continues for any other active customers.
- Audit log and accreditation evidence archived per customer's own retention policy (vendor archives its own copy of the evidence pack delivered).

---

## 15. Operational Metrics

| Metric | Target | Source |
|--------|--------|--------|
| MTTR — vendor pipeline P1 | < 24 h to issue corrected bundle | DEVOPS §16.1 |
| MTTR — advisory channel P3 | < 4 working hours | SLO-OPS-009 |
| MTBF — pipeline major incident | > 12 months between P1s | tracked on SRE dashboard |
| Change failure rate (release-tagged bundles) | 0 customer-impacting failures | DEVOPS §16.1 |
| Deployment frequency | Annual LTS + monthly patch + on-demand CRIT/HIGH | DEVOPS §16.1 |
| Toil percentage (vendor SRE / signing rota) | < 50% | Quarterly survey |
| Critical CVE SLA adherence | 100% within 7 days | SLO-OPS-003 |
| High CVE SLA adherence | 100% within 30 days | SLO-OPS-004 |
| Reproducibility cross-build pass rate | 100% | SLO-OPS-006 |
| Network-deny smoke pass rate | 100% | SLO-OPS-007 |
| Customer first-time accreditation pass | 100% pilot, ≥ 80% cumulative | DEVOPS §16.2 |

---

## 16. UK Government Considerations

| Requirement | Treatment |
|-------------|-----------|
| **GDS Service Standard 14** (operate a reliable service) | Vendor operates a reliable *supply chain*; customer operates the *service*. Reliability of supply chain measured via SLO catalogue. |
| **NCSC operational security** | Network-deny smoke + signed bundle + HSM custody + cleared-personnel access (ADR-003). |
| **NCSC VMS** | Vendor build estate enrolled where applicable; not applicable to customer-deployed instance (inside customer boundary). Customer-side patching governed by NFR-SEC-008 SLAs. |
| **Cabinet Office TCoP** | TCoP 6 (data security) — air-gap; TCoP 8 (reuse) — Sigstore/Syft; TCoP 11 (open) — OSS-first; per DEVOPS §15. |
| **MOD Secure by Design / JSP 440 / 604** | Evidence pack refreshed per release (RB-VEN-003); customer accreditator consumes (ADR-006). |
| **HMG Government Security Classifications Policy** | Per-deployment ceiling enforced (FR-012); bundle classification metadata honours ceiling. |
| **UK GDPR / DPA 2018** | DPIA vendor-narrow scope (ARC-002-DPIA-v1.0); customer is data controller for deployed instance. |
| **Cross-government services** | None depended on — sovereign route is intentionally self-contained. |

---

## 17. Traceability

| Operational element | Source artefact |
|---------------------|-----------------|
| SLO-OPS-003..005 (CVE SLAs) | NFR-SEC-008, ADR-008 |
| SLO-OPS-006/007 (reproducibility / network-deny) | Principle 21 validation gates, ADR-001, ADR-002, DEVOPS §3.2 |
| SLO-OPS-008 (distribution time) | ADR-007 |
| SLO-OPS-010 (evidence pack) | ADR-006 |
| RB-VEN-001 (bundle issue) | DEVOPS §3, ADR-002, ADR-007 |
| RB-VEN-002 (hotfix) | ADR-008, NFR-SEC-008 |
| RB-VEN-003 (evidence pack) | ADR-006 |
| RB-VEN-004 (distribution) | ADR-007 |
| RB-VEN-005 (customer escalation) | ADR-003, FR-013, INT-009 |
| RB-VEN-006 (HSM compromise) | ADR-002 §11 |
| RB-VEN-007 (HSM rotation) | ADR-002 R-ADR2-1 |
| RB-VEN-010 (VDP intake) | ADR-008, INT-010, ISO 29147 |
| Section 14 hand-over | ADR-006, FR-011, BR-003 |
| Customer-side DR pointer | ADR-001 §10.2, NFR-A-002 |
| Vendor pipeline DR | Principle 7 (UK residency), DEVOPS §9 |
| Section 11.7 contacts | ADR-003 cleared-personnel roster |
| No vendor remote default | ADR-003, FR-013 |

Cross-references back to the principles document anchor the load-bearing controls in Principle 21 (sovereign and air-gapped deployment — non-negotiable) and Principle 5 (security by design — sovereign block).

---

## 18. Handover Checklist (Vendor Production-Readiness)

Vendor confirms before going live with the sovereign release pipeline:

- [ ] All vendor-side runbooks (RB-VEN-001..010) written and dry-run.
- [ ] Pipeline dashboards live; alerts configured and tested.
- [ ] On-call rotations staffed (Pipeline / SRE; Security; HSM custody quorum).
- [ ] DR test of vendor pipeline run end-to-end at least once.
- [ ] Backups verified (RB-VEN-008 quarterly restore drills scheduled).
- [ ] Sovereign Delivery Desk staffed and trained.
- [ ] Advisory channel infrastructure live and rehearsed.
- [ ] HSM custody officer roster (M-of-N) named, trained, and rota'd.
- [ ] Vulnerability tracker live; SLA timers wired.
- [ ] LTS Health dashboard live.
- [ ] Knowledge base populated.
- [ ] SLOs agreed with Service Owner; SLO catalogue reviewed.
- [ ] First customer onboarding pack ready (Section 14).
- [ ] Critical vulnerability remediation runbook (RB-VEN-002) tabletop-rehearsed.
- [ ] HSM compromise runbook (RB-VEN-006) tabletop-rehearsed.
- [ ] First annual pen test booked.
- [ ] First annual MOD SbD assessment refresh booked.
- [ ] First DR drill booked.
- [ ] Service Owner sign-off recorded.

Customer-side handover checklist (Section 14.2) is repeated **per customer engagement**.

---

## External References

> No external operational documents were placed in `projects/002-arckit-sovereign/external/` at the time of generation. UK Government, MOD, NCSC, ISO references are public-domain and cited by name.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| PRIN-v2.0 | ARC-000-PRIN-v2.0.md | Internal — Architecture Principles | projects/000-global/ | Principle 21 (non-negotiable) anchor |
| HLD-002 | ARC-002-HLD-v1.0.md | Internal — HLD | projects/002-arckit-sovereign/ | Architecture under operationalisation |
| DEVOPS-002 | ARC-002-DEVOPS-v1.0.md | Internal — DevOps | projects/002-arckit-sovereign/ | 5-stage pipeline; LTS branching |
| RISK-002 | ARC-002-RISK-v1.0.md | Internal — Risk register | projects/002-arckit-sovereign/ | Operational risk inputs |
| DPIA-002 | ARC-002-DPIA-v1.0.md | Internal — DPIA | projects/002-arckit-sovereign/ | Vendor-narrow incident scope |
| ADR-002-001 | ARC-002-ADR-001-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Air-gap |
| ADR-002-002 | ARC-002-ADR-002-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Signed bundle |
| ADR-002-003 | ARC-002-ADR-003-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Cleared-personnel access |
| ADR-002-006 | ARC-002-ADR-006-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | JSP 440 / SAL alignment |
| ADR-002-007 | ARC-002-ADR-007-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | Distribution model |
| ADR-002-008 | ARC-002-ADR-008-v1.0.md | Internal — ADR | projects/002-arckit-sovereign/decisions/ | LTS — patch SLAs |

### Citations

| Citation ID | Doc ID | Section | Category | Quoted Passage |
|-------------|--------|---------|----------|----------------|
| ADR8-SLA | ADR-002-008 | NFR-SEC-008 anchor | Patch SLA | "Critical 7d / High 30d / Medium 90d." |
| ADR3-NoRemote | ADR-002-003 | §1 | Access model | "Cleared-Personnel-Only Access Model with Just-in-Time Elevation, On-Site Break-Glass, and No Default Vendor Remote Access." |
| ADR7-Channel | ADR-002-007 | §1 | Distribution | "Multi-Channel with Sealed Encrypted Media as Default and One-Way Diode as Option." |
| HLD-Scope | HLD-002 | §0 (this document) | Scope | "vendor does NOT operate the deployed instance — that is the deploying authority's job inside the accredited boundary." |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | No external operational PDFs placed in `projects/002-arckit-sovereign/external/` |

---

**Generated by**: ArcKit `/arckit:operationalize` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: claude-opus-4-7[1m]
**Generation Context**: Vendor-side operational readiness for sovereign release pipeline; customer-side deployed-instance operations explicitly out of scope (deploying authority's responsibility per ADR-006). Anchored on Principle 21 (`ARC-000-PRIN-v2.0.md`) and ADRs ADR-001 / ADR-002 / ADR-003 / ADR-006 / ADR-007 / ADR-008. Operationalises the 5-stage pipeline of `ARC-002-DEVOPS-v1.0.md` and the patch SLAs of NFR-SEC-008.
