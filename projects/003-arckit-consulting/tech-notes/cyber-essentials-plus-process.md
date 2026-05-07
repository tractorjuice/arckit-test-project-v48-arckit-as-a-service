# Tech Note: Cyber Essentials and Cyber Essentials Plus — Process, Pricing, Lead Times

> **Template Origin**: Official | **ArcKit Version**: 4.19.0 | **Command**: `/arckit:research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | TN-CYBER-ESSENTIALS-v1.0 |
| **Document Type** | Tech Note |
| **Project** | ArcKit Consulting (Project 003) — also relevant to all ArcKit projects requiring CE / CE+ |
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

Cyber Essentials (CE) is the NCSC's basic cyber security certification, delivered through IASME and a network of licensed assessors. Cyber Essentials Plus (CE+) adds an independent on-site/remote audit. Both are annual certifications. CE+ is increasingly a hard requirement on UK public sector procurement frameworks; CE+ assessment lead time of 4–8 weeks is on the critical path for new entrants.

## Key Findings

### IASME Cyber Essentials (Basic) Fees

- **Micro (0–9 staff)**: £300 + VAT
- **Small (10–49 staff)**: £400 + VAT
- **Medium (50–249 staff)**: £450 + VAT
- **Large (250+)**: £500 + VAT

These fees are set by IASME centrally and are consistent across licensed certification bodies.

### Cyber Essentials Plus Pricing

CE+ pricing is set by each licensed certification body (assessor), not by IASME. Typical ranges:

- **SME basic CE+ assessment**: £1,499–£4,000 + VAT.
- **CE+ with remediation support / managed certification**: £1,400–£2,500 + VAT for SMEs at the smaller end; up to £8,000+ + VAT for larger / more complex environments.
- **Re-certification annual** at the same pricing structure.

### Lead Times

- **CE basic**: 1–4 weeks turnaround typical.
- **CE+ booking constraint**: must be booked within **3 months** of basic CE being granted.
- **CE+ assessor lead time**: roughly 3 weeks of lead time before assessment day.
- **CE+ total typical lead time**: **4–8 weeks** once basic CE is granted.

### Assessment Scope (CE+ vs CE)

**Cyber Essentials (basic)** — self-assessment with IASME or licensed body verification:

- Boundary firewalls and gateways.
- Secure configuration.
- Access controls.
- Malware protection.
- Patch management.

**Cyber Essentials Plus** — adds independent on-site / remote audit:

- Verification of CE basic controls against actual systems.
- Vulnerability scanning (internal and external) of in-scope systems.
- Authenticated patch audit.
- Phishing-resistant email validation.
- Sample-based device configuration audit.

### Recommended Assessor Shortlist (NCSC-Licensed Bodies)

(Indicative; verify NCSC's current licensed-body register before selecting):

- **Precursor Security** — published from £1,500 for CE+; SME-friendly.
- **Connection Technologies** — managed CE+ certification with remediation.
- **Intelance** — UK-based managed certification.
- **BM Technologies** — UK-based managed certification.
- **IASME directly** — IASME does deliver some assessments, particularly for organisations seeking IASME Cyber Assurance alongside CE+.

### Recommended Process for ArcKit Consulting (per BR-001)

1. **Day 0–14** (incorporation): set up Microsoft 365 Business Premium with Entra P1 + Intune + Defender. This baseline pre-configures most CE / CE+ controls.
2. **Day 14–30**: complete CE basic self-assessment; submit to IASME / chosen certification body.
3. **Day 30–45**: receive CE basic certificate.
4. **Day 45–60**: book CE+ assessment with chosen certification body.
5. **Day 60–90**: complete CE+ assessment (4–8 weeks lead time).
6. **Day 90 target**: CE+ certified per BR-001 success criterion.

If any step slips, BR-001's 90-day target may be missed; framework applications dependent on CE+ should be planned with this lead time in mind.

## Relevance to Projects

- **ArcKit Consulting (Project 003)** — direct reference for CE / CE+ certification process and timing.
- **ArcKit as a Service (Project 001)** — relevant for the SaaS service's own CE+ certification (separate scope).
- **ArcKit Sovereign (Project 002)** — relevant where the deploying authority requires CE+ certification of the supplier.
- **Any UK-public-sector ArcKit project** — CE+ is a near-universal procurement requirement.

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

- [NCSC Cyber Essentials overview](https://www.ncsc.gov.uk/cyberessentials/overview)
- [IASME Cyber Essentials](https://iasme.co.uk/cyber-essentials/)
- [Connection Technologies CE cost UK 2026](https://connection-technologies.co.uk/blog/cyber-security-cost-uk-2026)
- [Intelance CE cost UK 2026](https://www.intelance.co.uk/cyber-essentials-cost-uk/)
- [Paul Reynolds CE cost 2026 guide](https://paulreynolds.uk/cyber-essentials-certification-cost/)
- [BM Technologies CE cost UK 2026](https://bm-technologies.co.uk/cyber-essentials-cost-uk-2026-what-businesses-need-to-know/)
- [Precursor Security CE assessor](https://www.precursorsecurity.com/services/compliance/cyber-essentials-certification)

---

**Generated by**: ArcKit `/arckit:research` agent
**Generated on**: 2026-05-07
**ArcKit Version**: 4.19.0
**Project**: ArcKit Consulting (Project 003)
**Model**: claude-opus-4-7[1m]
