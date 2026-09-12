# Bug 06: Extraction evidence displays corrupted punctuation

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | Low |
| Priority | Medium |
| Date reported | 24 August 2026 |
| Area | Encoding / extraction UI |

## Summary

Evidence messages in the extraction review displayed mojibake sequences such as `â€”` and `â€™` instead of normal punctuation.

## Affected area

Human-readable extraction evidence and source-file encoding.

## Environment

- Application: Job Application Tracker
- Browser: Chrome on Windows
- Page: Import review draft

## Preconditions

1. Import a supported job advertisement.
2. Open the generated review draft.
3. Display evidence beneath an extracted field.

## Steps to reproduce

1. Read the evidence sentence beneath a field populated by fetched-page labelled metadata.
2. Observe the punctuation between confidence and evidence details.

## Expected result

Evidence is readable, for example:

```text
High confidence — read from the page’s labelled job details.
```

## Actual result

The text contains damaged sequences:

```text
High confidence â€” read from the pageâ€™s labelled job details.
```

## Impact

The application looks broken or unprofessional and the evidence is harder to read, even though the underlying extracted values are correct.

- **Severity:** Low
- **Priority:** Medium

## Root cause

UTF-8 punctuation had previously been saved into source as already-corrupted Windows-1252/UTF-8 text. Razor correctly rendered the damaged string it received.

## Resolution

**Status: Fixed and verified.**

The damaged tracked string was replaced with valid UTF-8 punctuation, and the repository was scanned for common mojibake markers.

## Regression coverage

- Exact evidence sentence assertion.
- Scan for common mojibake markers.
- Existing fetched-page extraction behaviour preserved.
- Formatting, zero-warning Release build, 94 automated tests, and Release publish passed.

## Traceability

- [Public GitHub issue #6](https://github.com/Chit-Thway/job-application-tracker-qa/issues/6)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
