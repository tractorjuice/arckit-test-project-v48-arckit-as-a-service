# Project 003 — ArcKit Consulting

**Project ID**: 003
**Project Name**: ArcKit Consulting
**Created**: 2026-05-07
**Owner**: Mark Craddock

## Description

ArcKit Consulting is the consulting arm of the ArcKit ecosystem. It uses the ArcKit enterprise architecture governance toolkit to deliver advisory, design, and assurance engagements for the **UK Public Sector** — central government departments, arm's-length bodies, devolved administrations, local authorities, NHS bodies, MOD where appropriate, and **Small and Medium Enterprises (SMEs) supplying public-sector services**.

The consulting practice is a complementary commercial channel to:

- **Project 001 — ArcKit as a Service (managed SaaS)** — the multi-tenant cloud product
- **Project 002 — ArcKit Sovereign** — the air-gapped / on-premise deployment for MOD and sensitive sites

ArcKit Consulting differs from those product projects: it is a **professional services** offering, not a software platform. It exists to:

1. Help public sector buyers and SME suppliers actually adopt ArcKit and produce assurance-grade governance artefacts.
2. Generate revenue that cross-subsidises the free SME tier of the managed SaaS (Principle 1, ARC-000-PRIN-v2.0).
3. Drive product feedback from real engagements back into the platform.
4. Build a public corpus of reusable patterns, ADRs, and case studies.

## Project Structure

- `ARC-003-*.md` — top-level architecture artefacts
- `decisions/` — Architecture Decision Records (ADRs)
- `diagrams/` — architecture diagrams
- `research/` — research artefacts (RSCH, RSCH variants)
- `tech-notes/` — supporting tech notes
- `external/` — external reference documents (RFP, ITT, SOWs, policy papers placed here for citation)

## Suggested Next Commands

After this requirements document, recommended sequence:

1. `/arckit:stakeholders` — formal stakeholder analysis (currently a gap)
2. `/arckit:sobc` — Strategic Outline Business Case (Green Book 5-case model)
3. `/arckit:risk` — risk register (Orange Book)
4. `/arckit:research` — market research for tooling and frameworks
5. `/arckit:gov-reuse` — government code reuse for any platform components
6. `/arckit:adr` — capture key decisions (commercial model, framework strategy, etc.)
