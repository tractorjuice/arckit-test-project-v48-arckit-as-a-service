# Tech Note: UK SME Thresholds 2026 (Companies Act 2006, IR35, ICO Fees)

> **Template Origin**: Official | **ArcKit Version**: 4.19.0 | **Command**: `/arckit:research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | TN-UK-SME-THRESHOLDS-v1.0 |
| **Document Type** | Tech Note |
| **Project** | ArcKit Consulting (Project 003) — also relevant to all ArcKit projects with UK SME context |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-07 |
| **Last Updated** | 2026-05-07 |
| **Owner** | ArcKit Consulting Practice Lead |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-07 | ArcKit AI | Initial creation from `/arckit:research` agent | PENDING | PENDING |

---

## Summary

UK SME thresholds were uplifted with effect from **6 April 2025** under amendments to the Companies Act 2006. This is the first uplift since 2013, and materially affects (a) which companies qualify for SME treatment under various regulations, (b) IR35 / off-payroll working classification, and (c) ICO data protection fee tier. Same uplift carries through to the IR35 small-company exemption with effect from 6 April 2026.

## Key Findings

### Companies Act 2006 SME Thresholds (with effect 6 April 2025)

A company qualifies for a category if it meets at least two of the three thresholds:

#### Micro-entities

- Turnover not exceeding **£1 million**.
- Balance sheet total not exceeding **£500,000**.
- Average employees not exceeding **10**.

#### Small Company

- Turnover not exceeding **£15 million** (uplifted from £10.2m).
- Balance sheet total not exceeding **£7.5 million** (uplifted from £5.1m).
- Average employees not exceeding **50** (unchanged).

#### Medium-Sized Company

- Turnover not exceeding **£54 million** (uplifted from £36m).
- Balance sheet total not exceeding **£27 million** (uplifted from £18m).
- Average employees not exceeding **250** (unchanged).

These thresholds apply for accounting periods commencing on or after 6 April 2025.

### IR35 / Off-Payroll Working — Small Company Exemption

From **6 April 2026**, the IR35 small-company financial thresholds align with the new Companies Act 2006 small thresholds:

- Turnover up to **£15 million** (uplifted from £10.2m).
- Balance sheet total up to **£7.5 million** (uplifted from £5.1m).
- Employee headcount remains at **50**.

Effect: an estimated 14,000 additional UK companies move from "medium" to "small" classification, meaning 14,000 more end-clients are exempt from issuing Status Determination Statements; PSC contractors working with these end-clients revert to determining their own IR35 status.

### ICO Data Protection Fee Tiers (2026)

- **Tier 1 (Micro)**: £52/year — turnover ≤ £632,000 OR ≤ 10 staff.
- **Tier 2 (SMEs)**: £78/year — turnover ≤ £36 million OR ≤ 250 staff.
- **Tier 3 (Large)**: £3,763/year — does not meet tier 1 or tier 2 criteria.

Note that ICO Tier 2 still uses the **old** £36m turnover threshold (not the new Companies Act £54m for medium-sized) — re-verify before relying.

### Procurement Act 2023 SME Definition

For UK procurement purposes, the SME definition is aligned with the Companies Act 2006 thresholds (turnover < £15m for "small", < £54m for "medium" with effect from 6 April 2025), with adjustments for procurement-specific eligibility tests.

## Implications for ArcKit Consulting

- **SME-tier eligibility verification (FR-011)** uses the Companies Act 2006 small-company thresholds (turnover ≤ £15m, balance sheet ≤ £7.5m, headcount ≤ 50). Companies House API enables programmatic verification against filed accounts.
- **ArcKit Consulting itself** will qualify as a small company under the new thresholds for at least 3–5 years; this affects the practice's own statutory reporting and audit obligations.
- **IR35 self-assessment**: ArcKit Consulting's associate engagements will operate under the new April 2026 small-company exemption rules — many medium-sized clients may now revert to PSC-determined IR35 status.

## Relevance to Projects

- **ArcKit Consulting (Project 003)** — direct reference for SME-tier eligibility verification, IR35 process, ICO registration tier.
- **ArcKit as a Service (Project 001)** — Principle 1 SME affordability uses the same SME definition.
- **ArcKit Sovereign (Project 002)** — relevant where MOD or sensitive-site SMEs are in scope.
- **All UK-context ArcKit projects** — any project that defines or uses the SME criterion.

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

### Key URLs

- [UK Gov SME definition (Procurement Act 2023)](https://www.gov.uk/government/publications/procurement-act-2023-short-guides/supplementary-information-small-and-medium-sized-enterprises-definition-html)
- [Teamed UK company size thresholds 2026](https://www.teamed.global/blog/uk-company-size-thresholds-2026-april-2025-changes)
- [Kingsbridge IR35 small company threshold changes 2026](https://www.kingsbridge.co.uk/blog/contractors/ir35/ir35-small-company-threshold-changes-2026/)
- [RSM Companies Act 2006 size limits increase](https://www.rsmuk.com/insights/bridging-the-gaap/companies-act-2006-size-limits-increase-confirmed)
- [Companies Act 2006 Section 382](https://www.legislation.gov.uk/ukpga/2006/46/section/382)
- [UK Gov off-payroll IR35](https://www.gov.uk/guidance/understanding-off-payroll-working-ir35)
- [Greenberg Traurig IR35 threshold changes 2026](https://www.gtlaw.com/en/insights/2026/3/threshold-changes-to-uk-off-payroll-working-rules-ir35-end-user-and-contractor-considerations)
- [ICO Data Protection Fee](https://ico.org.uk/for-organisations/data-protection-fee/)

---

**Generated by**: ArcKit `/arckit:research` agent
**Generated on**: 2026-05-07
**ArcKit Version**: 4.19.0
**Project**: ArcKit Consulting (Project 003)
**Model**: claude-opus-4-7[1m]
