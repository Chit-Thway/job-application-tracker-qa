# Bug 05: SEEK URL import extracts page chrome instead of job details

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | Medium |
| Priority | High |
| Date reported | 24 August 2026 |
| Area | SEEK URL import |

## Summary

After the URL importer successfully fetched a SEEK job page, the review draft initially received shared navigation and footer content instead of the selected job details.

## Affected area

Fetched HTML extraction for public job URLs.

## Environment

- Application: Job Application Tracker
- Browser: Chrome on Windows
- Source: Public SEEK job page
- JavaScript execution: Disabled by design

## Preconditions

1. Sign in.
2. Open **Add application → Import public link**.
3. Use a currently accessible SEEK listing.

## Steps to reproduce

1. Submit the SEEK job URL.
2. Wait for the extraction review.
3. Inspect role title, employer, location, work type, salary, and fetched source text.

## Expected result

The importer extracts the selected listing’s specific job metadata from the server-returned HTML without executing scripts or making an additional request.

## Actual result

Role and employer are blank, location degrades to generic `Australia`, and the fetched text is dominated by SEEK navigation, partner links, country links, and footer content.

## Impact

A successful network fetch appears to work but produces an unusable draft, increasing the risk of incomplete or incorrect records.

- **Severity:** Medium
- **Priority:** High

## Root cause

Generic visible-text extraction prioritized shared site chrome while the useful listing fields were present in stable labelled elements in the server HTML.

## Resolution

**Status: Fixed and verified.**

The extractor now reads stable labelled job elements for title, employer, specific location, work type, salary, classification, and description. Official Schema.org `JobPosting` JSON-LD retains higher precedence.

## Regression coverage

- Deterministic SEEK-like HTML fixture.
- Specific job location cannot be replaced by generic site geography.
- Structured `JobPosting` metadata continues to win.
- No scripts are executed and no second endpoint is contacted.
- Locked restore, formatting, zero-warning Release build, 94 automated tests, and Release publish passed.

## Traceability

- [Public GitHub issue #5](https://github.com/Chit-Thway/job-application-tracker-qa/issues/5)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
