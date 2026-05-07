# Vendor Profile: Microsoft (M365 Business Premium / Entra ID / Intune / SharePoint)

> **Template Origin**: Official | **ArcKit Version**: 4.19.0 | **Command**: `/arckit:research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | VEN-MICROSOFT-v1.0 |
| **Document Type** | Vendor Profile |
| **Project** | ArcKit Consulting (Project 003) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-07 |
| **Last Modified** | 2026-05-07 |
| **Review Cycle** | Annual |
| **Next Review Date** | 2027-05-07 |
| **Owner** | Mark Craddock (ArcKit Consulting Practice Lead) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | ArcKit Consulting leadership |
| **Confidence** | High (5+ data points: per-seat pricing for M365 BP / Entra P1 / Intune, UK data residency, Cyber Essentials Plus compatibility, public sector ubiquity, integration coverage) |
| **Last Researched** | 2026-05-07 |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-07 | ArcKit AI | Initial creation from `/arckit:research` agent for ArcKit Consulting commercial-model research. (Note: a separate Microsoft Azure profile exists in `projects/001-arckit-saas/vendors/microsoft-azure-profile.md` — this profile is scoped to the M365 / Entra / Intune productivity stack relevant to ArcKit Consulting operating tooling.) | PENDING | PENDING |

---

## Overview

Microsoft is the dominant productivity, identity, and endpoint management vendor in UK public sector. Microsoft 365 Business Premium bundles Office apps, Exchange, SharePoint, Teams, Entra ID Premium P1, Intune, and Defender for Endpoint at a single per-seat price. For ArcKit Consulting, the M365 Business Premium SKU is recommended as the v1 "back-office bundle" because it (a) covers identity, MDM, and endpoint security in one bill (per Sub-Categories 4.6 and 4.7), (b) is the de-facto baseline that public sector buyers recognise, and (c) integrates naturally with the dominant tenant landing zone (Entra ID) in central-civil and NHS environments. Microsoft Azure (the cloud platform) is profiled separately in Project 001.

## Products & Services

For ArcKit Consulting (Project 003) the relevant Microsoft products are:

- **Microsoft 365 Business Premium** — £20.60/user/month (UK, monthly commitment; annual ~£18.10/user). Bundles Office apps (desktop + web), Exchange Online, SharePoint Online, Teams, OneDrive, Entra ID Premium P1, Intune, Defender for Endpoint Plan 1.
- **Microsoft 365 Business Standard** — £11.70/user/month. Office apps + Exchange + SharePoint + Teams; no Entra P1, no Intune.
- **Microsoft Entra ID P1** (standalone) — £6.20/user/month. Conditional Access, FIDO2, passkeys, SSO, group-based access.
- **Microsoft Entra ID P2** — £9/user/month. Adds Privileged Identity Management, Identity Protection, identity governance.
- **Microsoft Intune** (standalone) — £6.20/user/month.
- **Microsoft 365 E3 / E5** — enterprise tiers at £33.10 / £52.50 per user / month respectively (overkill for v1 consulting practice).

## Pricing Model

- **Per-seat subscription** with published UK list prices.
- **Annual commitment** offers modest discount vs monthly.
- **Volume discount** kicks in at 300+ seats (irrelevant for v1 ArcKit Consulting).
- **Cloud Solution Provider (CSP)** channel offers some flexibility for SMEs (e.g., Bytes, SoftwareONE, ITGL) but list price is published.

## UK Government Presence

- G-Cloud listed: Yes (Microsoft is a major G-Cloud supplier; Azure / M365 / Office 365 all listed).
- DOS listed: Not as Microsoft directly (Microsoft is a software vendor); Microsoft partners are listed as digital outcomes / specialist suppliers.
- UK data centres: Yes — UK South (London) and UK West (Cardiff) Azure regions; M365 / Exchange / SharePoint / Teams data resident in UK by default for UK tenants.

## Strengths

- **Bundled value** — M365 Business Premium combines productivity, identity, MDM, endpoint security in one bill. Marginal cost of Entra P1 + Intune over Business Standard is modest (£8.90/user/month).
- **Dominant in UK public sector** — central-civil departments, NHS, MOD all heavy Microsoft tenants. Easier integration with client environments if practice runs Entra ID.
- **Cyber Essentials Plus compatible out of the box** — Defender for Endpoint, Intune compliance policies, Conditional Access map cleanly to CE+ controls.
- **UK data residency** — M365 / Exchange / SharePoint resident in UK for UK tenants; supports Principle 7 / NFR-SEC-001.
- **Mature, stable, supported** — multi-decade product line; SLA 99.9% on most M365 services.
- **Integration ecosystem** — Power Automate / Power BI for reporting; integrates with HubSpot, Harvest, Notion, Adobe Sign, etc.

## Weaknesses

- **Vendor lock-in** — once a practice is on M365, switching costs are non-trivial.
- **Less competitive on Apple management** than Jamf — practices with heavy Mac estates may need Jamf as overlay.
- **Cost rises sharply at E3 / E5 tiers** — overkill for ArcKit Consulting v1 but may pressure expansion later.
- **Power Platform licensing** is opaque and expensive at scale; not relevant for v1.
- **Multinational US-headquartered** — CLOUD Act / Investigatory Powers Act exposure (mitigated for OFFICIAL-classification work; would need re-assessment for OFFICIAL-SENSITIVE).

## Projects Referenced In

- ArcKit Consulting (Project 003) — primary recommendation for Sub-Categories 4.6 (Identity and SSO), 4.7 (MDM), and 4.8 (KM via SharePoint) in `ARC-003-RSCH-v1.0.md`.
- ArcKit as a Service (Project 001) — Microsoft Azure profiled in `projects/001-arckit-saas/vendors/microsoft-azure-profile.md` for cloud platform components.

## External References

> No external (non-ArcKit) source documents provided. Citations are to public web sources captured in `ARC-003-RSCH-v1.0.md`.

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

**Generated by**: ArcKit `/arckit:research` agent
**Generated on**: 2026-05-07
**ArcKit Version**: 4.19.0
**Project**: ArcKit Consulting (Project 003)
**Model**: claude-opus-4-7[1m]
