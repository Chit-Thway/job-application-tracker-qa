# Bug 09: Browser extension captures Indeed page heading instead of selected job

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | Medium |
| Priority | High |
| Date reported | 24 August 2026 |
| Area | Indeed browser extension |

## Summary

In Indeed’s split search-results layout, the browser extension initially captured a generic page heading rather than the job selected in the focused detail panel.

## Affected area

Chrome extension capture for Indeed search results.

## Environment

- Extension: Job Application Tracker companion extension
- Browser: Chrome on Windows
- Website: Indeed split search-results page
- Permission model: Explicit user click and active tab only

## Preconditions

1. Sign in to Indeed with a test account.
2. Open a search-results page.
3. Select a job so its details appear in the focused panel.
4. Open the tracker extension.

## Steps to reproduce

1. Select **Capture and review**.
2. Inspect the generated draft.
3. Compare it with the selected job panel.

## Expected result

The draft contains the selected role, employer, location, labelled pay, job type, description, and job reference.

## Actual result

The role can become a generic account greeting such as `Welcome, [user]` or a search heading such as `jobs in Perth WA`. Employer, location, pay, job type, and description remain blank.

## Impact

The extension captures the wrong context and produces an incomplete draft that the user must substantially rewrite.

- **Severity:** Medium
- **Priority:** High

## Sanitized evidence

Two reproduced examples included decimal hourly ranges such as:

```text
$33.50 - $90.00 an hour
$35 - $40 an hour
```

These values must remain valid salary text rather than being rejected by annual-salary assumptions.

## Root cause

Generic page-level selectors had precedence over Indeed’s focused job-detail panel.

## Resolution

**Status: Fixed and verified.**

Indeed’s selected-panel fields now override generic page headings. The capture includes title, employer, location, labelled hourly pay, job type, description, and the `vjk` job reference.

## Regression coverage

- Generic greeting and search headings cannot become the role.
- Decimal hourly ranges remain valid.
- SEEK, generic page, and Schema.org capture tests continue to pass.
- Explicit-click access remains unchanged; no background browsing, broad host permission, or remote API was added.
- Complete gate passed with 107 automated tests plus JavaScript checks and Release publish.

## Traceability

- [Public GitHub issue #9](https://github.com/Chit-Thway/job-application-tracker-qa/issues/9)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
