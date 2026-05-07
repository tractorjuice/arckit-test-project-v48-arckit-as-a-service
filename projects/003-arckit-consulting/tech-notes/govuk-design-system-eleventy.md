# Tech Note: GOV.UK Design System and Eleventy for Non-Government Public Websites

> **Template Origin**: Official | **ArcKit Version**: 4.19.0 | **Command**: `/arckit:research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | TN-GOVUK-DS-ELEVENTY-v1.0 |
| **Document Type** | Tech Note |
| **Project** | ArcKit Consulting (Project 003) — also relevant to ArcKit as a Service public marketing site (Project 001) |
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

Eleventy (11ty) is a simpler, zero-config-to-start static site generator commonly used to build accessible, fast, low-attack-surface public websites. The GOV.UK Design System is the authoritative design language for UK government services — but it is **reserved for UK public sector services** and may not be used directly by private companies (including consultancies that serve the public sector). The pattern for non-government practices is to use the GOV.UK Design System as **inspiration**, in combination with Eleventy plugins like `x-govuk` that adapt the styling without claiming the brand. This combination delivers WCAG 2.2 AA accessible static sites at low build effort and low hosting cost.

## Key Findings

### Eleventy

- Open-source static site generator; zero-config to start.
- Does not require a JavaScript framework (zero client-side JS by default across the board).
- Renders Markdown, Nunjucks, Liquid, Handlebars, Mustache, EJS, Haml, Pug, JS template literals, and more.
- Suitable for any static file host (Netlify, Cloudflare Pages, GitHub Pages, S3 / CloudFront, Vercel).
- Strong UK Government adoption: GOV.UK Design History project, GOV.UK Publishing Design Guide, alphagov product-page-example-11ty, all use Eleventy.

### GOV.UK Design System

- The official design language for UK government services.
- Components, patterns, and styles from the GOV.UK Design System are derived from extensive user research with UK citizens.
- WCAG 2.2 AA compliant by design.
- **Reserved for UK public sector services** — private companies (including consultancies serving the public sector) cannot use the GOV.UK brand directly.
- Source: design-system.service.gov.uk.

### x-govuk Eleventy Plugin

- An Eleventy plugin that adapts GOV.UK Design System patterns for use in non-government contexts.
- Provides GOV.UK-style components (buttons, summary lists, tag, error summary, etc.) without the GOV.UK branding.
- Maintained at govuk-eleventy-plugin.x-govuk.org.
- Allows consultancies and other non-government organisations to deliver GOV.UK-quality user experience without claiming the GOV.UK brand.

### Related Eleventy + GOV.UK Templates

- `Nikolaos-Gkionis/govuk-11ty` — Eleventy template using GOV.UK Design System for prototypes.
- `wearefuturegov/gov-uk-eleventy-kit` — simple 11ty starter kit primed for the GOV.UK Design System; "great for prototypes or quick betas".
- `x-govuk/govuk-design-history` — GOV.UK Design History project, built using Eleventy.
- `alphagov/product-page-example-11ty` — Eleventy-based static site generator for GDS Portfolio product pages.

### Recommended Stack for ArcKit Consulting Public Website

- **Static site generator**: Eleventy.
- **Design pattern source**: GOV.UK Design System (as inspiration, not direct use).
- **CSS / components**: x-govuk Eleventy plugin or comparable GOV.UK-inspired theme.
- **Hosting**: Netlify, Cloudflare Pages, or GitHub Pages — UK / EU edge nodes.
- **Build effort**: 5–15 person-days at first build; thereafter content-only changes via Markdown.

## Relevance to Projects

- **ArcKit Consulting (Project 003)** — recommended for the public website (FR-019 in Project 003).
- **ArcKit as a Service (Project 001)** — relevant for the SaaS product's public marketing site if outside the SaaS application itself.
- **Future ArcKit projects** — any project building a UK-aligned, accessible, simple public website.

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

- [Eleventy.dev official](https://www.11ty.dev/)
- [Nikolaos Gkionis govuk-11ty](https://github.com/Nikolaos-Gkionis/govuk-11ty/)
- [wearefuturegov gov-uk-eleventy-kit](https://github.com/wearefuturegov/gov-uk-eleventy-kit)
- [x-govuk GOV.UK Eleventy Plugin](https://govuk-eleventy-plugin.x-govuk.org/get-started/design/)
- [GOV.UK Design System](https://design-system.service.gov.uk/)
- [alphagov product-page-example-11ty](https://github.com/alphagov/product-page-example-11ty)
- [Inside GOV.UK creating publishing design guide](https://insidegovuk.blog.gov.uk/2025/02/25/creating-the-gov-uk-publishing-design-guide/)
- [X-GOVUK GovUK Design History](https://x-govuk.github.io/govuk-design-history/get-started/)

---

**Generated by**: ArcKit `/arckit:research` agent
**Generated on**: 2026-05-07
**ArcKit Version**: 4.19.0
**Project**: ArcKit Consulting (Project 003)
**Model**: claude-opus-4-7[1m]
