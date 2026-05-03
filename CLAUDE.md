# CLAUDE.md

## Project: ArcKit as a Service

ArcKit as a Service for UK Government — a managed, multi-tenant offering of the ArcKit enterprise architecture governance toolkit, designed for UK public sector adoption (GDS Service Standard, TCoP, NCSC CAF, G-Cloud).

## Architecture Toolkit

This project uses the **ArcKit plugin** (v4.12.3) for enterprise architecture governance. All commands are provided by the plugin — no local command files are needed.

### Key Commands

- `/arckit.principles` - Architecture principles (start here)
- `/arckit.stakeholders` - Stakeholder analysis
- `/arckit.requirements` - Requirements specification
- `/arckit.sobc` - Strategic Outline Business Case
- `/arckit.adr` - Architecture Decision Records
- `/arckit.diagram` - Architecture diagrams (C4, sequence, etc.)

### Project Structure

- `projects/000-global/` - Cross-project artifacts (principles, standards)
- `projects/001-*/` - Numbered project directories with architecture documents
- `docs/` - Documentation and guides

### Document Naming Convention

All documents follow: `ARC-{PROJECT_ID}-{TYPE_CODE}-v{VERSION}.md`
- Example: `ARC-001-REQ-v1.0.md` (Requirements for project 001)
- Multi-instance types (ADR, DIAG): `ARC-001-ADR-001-v1.0.md`
