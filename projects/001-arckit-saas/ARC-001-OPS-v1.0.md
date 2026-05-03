# ArcKit as a Service (Managed SaaS) — Operational Readiness Pack

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:operationalize`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-OPS-v1.0 |
| **Document Type** | Operational Readiness Pack |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Owner** | Mark Craddock — until SRE Lead appointed |
| **Distribution** | SRE, Engineering, Security, Service Owner, ARB |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial pack. Service model, on-call, runbooks index, DR/BCP, incident response, change management, exit/handover. |

---

## 1. Service Model

### 1.1 RACI

| Domain | Accountable | Responsible | Consulted | Informed |
|--------|-------------|-------------|-----------|----------|
| Production operations | SRE Lead | SRE engineers | Security; Lead Architect | Service Owner |
| Security incidents | Security Lead | Security + SRE | DPO; Service Owner | ARB; ICO (if applicable); affected tenants |
| Privacy incidents | DPO | DPO + Security | Service Owner | ARB; ICO; affected tenants |
| Change management | Lead Architect | Engineering | SRE; Security | ARB |
| Tenant support | Service Owner | Support engineers | Engineering | — |
| Release management | Lead Architect | Engineering + SRE | Security | Service Owner |

### 1.2 Service hours

- **Production**: 24×7.
- **Support**: business hours UK (initial); on-call rotation 24×7 for production incidents.
- **Status page**: 24×7 (FR-009).

### 1.3 SLOs

Per `NFR-A-001`/`NFR-P-*`/`NFR-SEC-*`. Burn-rate alerts → on-call.

---

## 2. On-Call

- **Primary on-call** (1 engineer) + **secondary** (1 engineer) per rotation week.
- **Pager** alerts via dedicated channel; escalation to Security Lead for sec-events; to DPO for personal-data events.
- **Severity matrix**:

| Sev | Description | Page? | Comms |
|-----|-------------|-------|-------|
| 1 | Multi-tenant outage; data integrity at risk | Yes immediately | Status page; tenant comms within 30 min |
| 2 | Single-cell or single-feature outage | Yes within 15 min | Status page |
| 3 | Single-tenant or non-critical outage | Working hours | Tenant ticket |
| 4 | Cosmetic / informational | No | Backlog |

- **Incident commander**: SRE on-call by default; security incidents → Security Lead.
- **Post-incident review**: Sev-1/2 within 5 working days; report shared with affected tenants and ARB.

---

## 3. Runbooks (Index)

| Runbook | Purpose | Owner | Cadence test |
|---------|---------|-------|--------------|
| RB-01 Cell provisioning | Stand up a new cell from IaC | SRE | Per cell add |
| RB-02 Cell decommission | Drain + destroy cell | SRE | Annual rehearsal |
| RB-03 Tenant onboarding (operator-assisted) | Override / manual onboarding for enterprise | Support | Per onboarding |
| RB-04 Tenant offboarding + deletion | UC-3 / FR-010 | Support + DPO | Quarterly mock |
| RB-05 DSAR / data-subject erasure | UK GDPR Art 15 / 17 | DPO | Mock per quarter |
| RB-06 Backup + restore | Restore individual tenant or cell | SRE | Quarterly |
| RB-07 Cross-AZ failover | AZ outage handling | SRE | Quarterly chaos |
| RB-08 Cross-region DR rehearsal | Region outage handling | SRE | Annually |
| RB-09 KMS key rotation | Rotate vendor / customer keys | Security | Annual |
| RB-10 Sub-processor incident | A sub-processor reports breach | DPO | Tabletop annually |
| RB-11 Cross-tenant attempt detected | SIEM alert response | Security | Per alert |
| RB-12 Cyber-incident response | NCSC CAF D1; ICO 72-hr breach pathway | Security + DPO | Tabletop annually |
| RB-13 Hotfix release | Fast-track production deploy | SRE + Engineering | Per hotfix |
| RB-14 Cell-management: tenant migration | Move tenant between cells | SRE | Per migration |
| RB-15 Rate-limit / abuse mitigation | Tenant noise; DDoS | SRE | Per event |
| RB-16 AI provider outage | Failover to alternative provider | Engineering | Annual game-day |
| RB-17 IdP outage | Tenant access during IdP outage | Engineering | Annual game-day |
| RB-18 Status-page communication | Tenant / public comms | SRE + Service Owner | Per incident |
| RB-19 G-Cloud / DOS contract triage | Contract-related queries | Service Owner | Per query |
| RB-20 Vulnerability disclosure intake | VDP triage | Security | Per submission |

(Each runbook is a separate Markdown file under `/operations/runbooks/` once Engineering scaffolds the directory.)

---

## 4. DR / BCP

- **RPO**: ≤ 15 min (NFR-A-002).
- **RTO**: ≤ 4 h (NFR-A-002).
- **Backups**: continuous DB WAL + daily snapshot; cross-region storage replication.
- **DR rehearsal**: cell-level quarterly; cross-region annually; report to ARB.
- **BCP**: defined for vendor-side disruptions (key-person dependency mitigation R-006).

---

## 5. Change Management

- **Standard change**: GitOps PR; CI gates; progressive rollout. No CAB needed.
- **Major change**: ADR; ARB sign-off; staged rollout with extended bake.
- **Emergency change**: hotfix path; documented after-the-fact in CAB log.
- **Configuration drift**: detected by GitOps; alerted; remediation as standard change.

---

## 6. Incident Response

### 6.1 Cyber

- Detection: SIEM alerts (ADR-005).
- Triage: severity matrix (§2).
- Containment: isolate affected cell/service; rotate credentials.
- Eradication: patch / rollback; verify.
- Recovery: bring services back; verify with isolation suite.
- Lessons learned: post-incident review; ADR superseding if architectural.

### 6.2 Privacy

- ICO 72-hour breach notification path.
- Tenant notification (per DPA terms).
- DPO leads.

### 6.3 Communications

- Status page: continuous updates.
- Tenant emails for affected tenants.
- Publicly-affected (Sev-1) post-mortem published.

---

## 7. Tenant Lifecycle Operations

- **Onboarding**: UC-1 self-service; operator assists for enterprise (RB-03).
- **Steady state**: tenant-visible dashboards (consumption, audit log, SLO).
- **Offboarding**: UC-3; export then delete (RB-04); deletion confirmed within retention window (FR-010).

---

## 8. Capacity & Scaling

- **Cell-fill discipline** (ADR-001 / ADR-006): provision new cell at 75% of cap.
- **Per-tenant quota review** quarterly (ADR-008).
- **AI provider capacity**: per-tier headroom monitored; alert at 70%.
- **Storage growth**: per-tenant trend monitored; cell rebalancing as needed.

---

## 9. Security Operations

- SIEM rules reviewed per ADR.
- Pen test quarterly (NFR-SEC-006).
- VDP / bug bounty live; triage SLAs.
- Annual NCSC CAF self-assessment.
- Cyber Essentials Plus certification (annual).

---

## 10. Compliance Operations

- DPIA refresh annual.
- Sub-processor inventory updated on change; published.
- TCoP assessment refreshed annually.
- Service Standard re-engagement at major changes.

---

## 11. Exit and Handover (Vendor → Tenant Self-Sufficiency)

This section addresses Crown Commercial Service exit-management expectations and Principle 4 anti-lock-in.

- **Tenant exit**: UC-3; Round-trip CI test gives byte-equality assurance.
- **Vendor exit / customer takes service in-house**: documented in `/operations/exit-plan.md`. Customer can stand up the open-source ArcKit and import the export archive.
- **Exit drill**: annual; report filed with ARB.

---

## 12. Linked Artefacts

- ADRs 001–008.
- HLD; Diagrams 001–003.
- DPIA; SbD; TCoP; AI Playbook.
- Risk Register (R-006, R-013, R-018 are operationally critical).
- Plan; Roadmap; DevOps; FinOps.
- Project 002 cross-link: NFR-M-001 (operator documentation parity).

---

**Generated by**: ArcKit `/arckit:operationalize` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
