# Bug 08: Mobile navigation opens over content and cannot be dismissed reliably

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | High |
| Priority | High |
| Date reported | 24 August 2026 |
| Area | Responsive navigation |

## Summary

At narrow mobile widths, the primary navigation initially loads expanded over the page content and cannot be dismissed reliably.

## Affected area

Responsive primary navigation in authenticated and synthetic-demo layouts.

## Environment

- Application: [Live Job Application Tracker](https://myjobtracker.com.au/)
- Browser: Chrome responsive viewport
- Reference viewport: 390 px wide
- Layouts: Signed-in application and public synthetic demo

## Preconditions

1. Open the application in a narrow mobile viewport.
2. Load either an authenticated page or the public demo.

## Steps to reproduce

1. Refresh the page at approximately 390 px width.
2. Observe the primary navigation immediately after load.
3. Try closing it with the Menu control.
4. Open it again and try a navigation link, outside click, and `Escape`.

## Expected result

Mobile navigation starts collapsed, opens and closes from the Menu control, and dismisses after selecting a link, clicking outside, or pressing `Escape`. Desktop navigation remains persistently visible, and theme controls remain reachable.

## Actual result

The menu starts permanently expanded over the content and cannot be dismissed consistently.

## Impact

The covered page is difficult or impossible to use on a phone, affecting navigation across the entire product.

- **Severity:** High
- **Priority:** High

## Probable cause

The responsive navigation container is rendered with an initially expanded state intended for desktop, without a complete mobile dismissal lifecycle.

## Acceptance and regression checks

- Mobile starts collapsed at a 390 px viewport.
- Menu toggle opens and closes it.
- Link selection closes it.
- Outside click closes it.
- `Escape` closes it and returns focus appropriately.
- Desktop navigation stays visible.
- Theme controls remain reachable.
- Authenticated and synthetic-demo layouts are both covered by browser regression tests.
- Complete manual retest and the full quality gate before closing.

## Resolution

**Status: Fixed and verified.**

Mobile navigation now uses a native checkbox-backed control: it starts collapsed without depending on JavaScript, while a small progressive-enhancement script closes it after a link selection, outside interaction, or `Escape`. Desktop navigation remains persistently visible.

## Verification

- The fix was merged and deployed to the production application.
- The 390 px browser journey verifies the mobile toggle.
- Integration coverage verifies the exact responsive hide/show rules served by the application.
- Authenticated and synthetic-demo layouts are covered.
- The combined release gate passed: 104 unit tests, 96 integration tests, 3 browser journeys, formatting, dependency audit, zero-warning Release build, JavaScript checks, and publish.

## Traceability

- [Public GitHub issue #8](https://github.com/Chit-Thway/job-application-tracker-qa/issues/8)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
