# Phase 02: Certificate Rendering — Validation Architecture

**Phase:** 02-certificate-rendering
**Created:** 2026-04-11
**Source:** Extracted from 02-RESEARCH.md Validation Architecture section

---

## Test Framework Reality

This project uses **pure vanilla JS with no build pipeline, no npm, no Node.js**. Standard automated test frameworks (Jest, Vitest, Playwright) require Node.js and npm to install — which are prohibited by the locked stack constraints.

**There is no viable automated test framework for this stack without violating Phase 01 constraints.**

All plans use inline PowerShell `Select-String` / file-exist checks as automated verification. Manual browser verification is the gate for functional behavior.

---

## Phase Requirements → Validation Map

| Req ID | Behavior | Test Type | Method |
|--------|----------|-----------|--------|
| APP-02 | `/?id=sample-id` renders certificate | Manual browser verification | Open `index.html?id=jane-doe-at-example-com` |
| APP-05 | Config + attendee fetch in parallel | Manual: Network tab in DevTools | Check waterfall — both requests start within 1 frame |
| DATA-03 | Attendee fetched from `data/{id}.json` | Manual: Network tab | Confirm request to `data/jane-doe-at-example-com.json` |
| DATA-04 | Invalid ID → error with attempted ID | Manual browser verification | Open `/?id=fake-id` — error must quote "fake-id" |
| CERT-01 | All fields populated | Manual visual check | Compare rendered cert against sample.json values |
| CERT-02 | Broken seal → no broken icon | Manual: Edit seal_url to 404 path | Flag absent, no broken img icon visible |
| CERT-03 | A4 landscape proportions | DevTools element ruler / print preview | Certificate wrapper ~1.41:1 width/height ratio |
| CERT-04 | Correct fonts applied | DevTools Computed tab | `font-family` resolves to Playfair Display / Lato |
| CERT-05 | show_description:false hides description | Manual: Set config flag | Description absent even with `data/sample.json` having one |
| CERT-06 | Certificate ID in muted text at bottom | Manual visual check | ID text visible at bottom of certificate |
| CERT-07 | Border from config | Manual: Change border_color in config | Certificate border color updates on reload |

---

## Automated Checks (per plan)

Each plan uses inline PowerShell in `<verify>` blocks:

| Plan | Automated Checks |
|------|-----------------|
| 02-01 | `Select-String` for `cert-name`, `cert-workshop`, `cert-logo`, `cert-id-label`, `error-message`, `error-detail` in index.html |
| 02-02 | `Select-String` for `aspect-ratio: 297`, `@page`, `A4 landscape` in styles.css; absence of `--cert-` names |
| 02-03 | `Select-String` for `Promise.all`, `fetchAttendee`, `validateAttendee` in app.js |
| 02-04 | `Select-String` for `renderCertificateView`, `setImageGraceful` in app.js |
| 02-05 | N/A — human checkpoint |

---

## Wave 0 Gaps

None — no test files need to be created. Manual verification is the gate for this phase. All in-plan `<automated>` verify commands are PowerShell checks that run without any test runner or npm.
