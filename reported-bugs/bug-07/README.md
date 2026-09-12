# Bug 07: Browser extension misses LinkedIn focused job details

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | Medium |
| Priority | High |
| Date reported | 24 August 2026 |
| Area | LinkedIn browser extension |

## Summary

On signed-in LinkedIn job-search pages, the browser extension captures the source site but misses the job displayed in LinkedIn’s focused right-hand detail pane.

## Affected area

Chrome extension capture for LinkedIn search results.

## Environment

- Extension: Job Application Tracker companion extension
- Browser: Chrome on Windows
- Tracker: [Live Job Application Tracker](https://myjobtracker.com.au/)
- Website: LinkedIn Jobs split search-results layout
- Permission model: Explicit user click and active tab only

## Preconditions

1. Sign in to LinkedIn.
2. Open a Jobs search-results page.
3. Select a job so its full details appear in the right-hand pane.
4. Open the tracker extension.

## Steps to reproduce

1. Select **Capture and review**.
2. Inspect the generated draft.
3. Compare the draft with the focused job-detail pane.

## Expected result

The draft contains the focused job’s role title, employer, Australian location, work type when present, full description, and current job reference. It must not read a different result from the left list.

## Actual result

Only the source site is captured. Title, employer, location, work type, and description are blank.

## Impact

LinkedIn users cannot benefit from one-click capture and must copy or re-enter most job information manually.

- **Severity:** Medium
- **Priority:** High

## Probable cause

The selected job is rendered inside LinkedIn’s dedicated focused-detail container, which is not covered by the current generic selectors.

## Acceptance and regression checks

- Anchor extraction to the focused LinkedIn job-detail container.
- Never select a title or employer from an unselected left-side result card.
- Capture the current job reference when available.
- Add a deterministic LinkedIn-like fixture.
- Preserve SEEK, Indeed, generic-page, and Schema.org behaviour.
- Keep explicit-click/no-remote-request permissions unchanged.
- Complete manual retest and the full quality gate before closing.

## Implemented resolution

The extension now anchors extraction to LinkedIn’s focused job-detail container instead of the left results list. Automated coverage verifies the focused title, employer, location, work type, description, and current job reference while preserving the explicit-click permission model.

The implementation is merged into the website repository and the complete quality gate passed as part of a combined fix release: 104 unit tests, 96 integration tests, 3 browser journeys, formatting, dependency audit, zero-warning Release build, JavaScript checks, and publish.

## Status

**Fixed and verified.** The focused-pane capture fix is merged into the current release line. The current extension source is version `1.0.4`, and the LinkedIn workflow has been accepted after regression testing.

## Traceability

- [Public GitHub issue #7](https://github.com/Chit-Thway/job-application-tracker-qa/issues/7)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
