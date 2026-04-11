# Project State

**Project:** Workshop Certificate App — Template Edition
**Milestone:** 1.0 — Template MVP
**Status:** Phase 01 complete — ready for Phase 02

## Current Phase
Phase 02: Certificate Rendering — Planned (5 plans ready, 3 waves)

## Last Completed Phase
Phase 01: Scaffold & Config System — Complete (2026-04-11)

## Phase Status

| # | Phase | Status | Plans |
|---|-------|--------|-------|
| 01 | Scaffold & Config System | ✓ Complete | 5/5 |
| 02 | Certificate Rendering | Not Started | 4 plans |
| 03 | Interactive Features | Not Started | 3 plans |
| 04 | Search & SPA Routing | Not Started | 3 plans |
| 05 | SEO & Structured Data | Not Started | 4 plans |
| 06 | Contribution & Polish | Not Started | 3 plans |

## Completed Phases
- Phase 01: Scaffold & Config System (2026-04-11)

## Accumulated Context

### Decisions
- Stack: Single `index.html`, pure HTML/CSS/Vanilla JS (ES6+), no build pipeline
- CDN libs: qrcode.js v1.0.0, html2pdf.js v0.10.1, Google Fonts (Playfair Display + Lato)
- Hosting: GitHub Pages (static, zero backend)
- Certificate ID convention: email sanitization — `jane.doe@gmail.com` → `jane-doe-at-gmail-com`
- Clean URL paths (e.g. `/john-doe`) explicitly out of scope — conflicts with OG scraper requirement
- v2 deferral: CI validator, certificate gallery, multiple workshops per person, opaque IDs, sitemap

- SRI hashes fetched live from cdnjs API at execution time (qrcode.min.js, html2pdf.bundle.min.js)
- loading-view has no hidden class — visible by default for app init
- Error message hardcoded in HTML — branding config fetch may itself have failed

### Todos
(none yet)

### Blockers
(none)

## Last Updated
April 11, 2026 — Phase 01 complete (5/5 plans executed, verification passed)
