# Vendor Profile: Notion

> **Template Origin**: Official | **ArcKit Version**: 4.19.0 | **Command**: `/arckit:research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | VEN-NOTION-v1.0 |
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
| **Confidence** | Medium-High (4 data points: tier pricing, GDPR posture, comparison to Confluence / SharePoint, integration coverage) |
| **Last Researched** | 2026-05-07 |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-07 | ArcKit AI | Initial creation from `/arckit:research` agent for ArcKit Consulting commercial-model research. | PENDING | PENDING |

---

## Overview

Notion is a US-headquartered (San Francisco) all-in-one workspace combining notes, wikis, databases, and lightweight project management. Increasingly used by consultancies and professional services firms for knowledge management and IP curation because of its flexible blocks model and database functionality. For ArcKit Consulting, Notion is recommended for the FR-012 pattern library / IP curation use case, in combination with SharePoint (M365 bundled) for client engagement workspaces.

## Products & Services

- **Notion Free** — limited (collaborative workspaces capped at small block counts).
- **Notion Plus** — $8/user/month annual ($10 monthly). Unlimited blocks, file uploads, version history.
- **Notion Business** — $15/user/month annual ($18 monthly). Private team spaces, advanced page analytics, bulk PDF export.
- **Notion Enterprise** — custom pricing. SAML SSO, audit log, advanced permissions, data residency options.
- **Notion AI** — $10/user/month add-on. Generative AI capabilities (writing, summarising, Q&A over workspace content).

## Pricing Model

- **Per-seat subscription** with published list prices for Plus and Business; Enterprise custom.
- **Annual billing** ~20% discount vs monthly.
- **Educators / non-profits** discounted; not directly applicable.

## UK Government Presence

- G-Cloud listed: Unknown / not directly listed under "Notion" brand at the search performed; some resellers may list.
- DOS listed: No.
- UK data centres: No (US-hosted; EU residency available on Enterprise tier; UK GDPR-aligned DPA standard).

## Strengths

- **Most flexible blocks model** of the major KM platforms — pages can mix text, databases, embeds, code, and structured templates.
- **Database functionality** as first-class — pattern library can be a structured database with metadata (capability, engagement type, review status, anonymisation evidence) per FR-012.
- **Modern UI** — better discoverability for consultants browsing the library; lower training overhead.
- **Templates and integrations** — large community template library; integrates with Slack, GitHub, Google Drive, Figma.
- **API** — workspace content addressable via REST API, supporting future integration with ArcKit toolkit.
- **Notion AI** add-on enables retrieval over the pattern library — useful for Knowledge Compounding (Principle 16-adjacent).

## Weaknesses

- **US-hosted** by default — UK / EU residency only on Enterprise tier; UK GDPR Article 28 DPA available but not equivalent to UK-hosted.
- **Less mature for regulated environments** than SharePoint — fewer audit / compliance controls below the Enterprise tier.
- **Multi-tenant client isolation** is workspace-based, not true multi-tenant — care needed when storing engagement content. ArcKit Consulting should reserve Notion for the **anonymised pattern library** only; client-engagement content lives in SharePoint per FR-004 isolation requirements.
- **Vendor lock-in risk** — Notion's data format is proprietary; export to Markdown is supported but full-fidelity export (with database schema preserved) is more limited.
- **Performance** at very large workspace size can degrade — relevant only at scale beyond v1 needs.

## Projects Referenced In

- ArcKit Consulting (Project 003) — recommended for Sub-Category 4.8 (Knowledge / Document Management — pattern library use case) in `ARC-003-RSCH-v1.0.md`.

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
