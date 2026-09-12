# Bug 01: Pasted-text importer misses realistic unlabelled job-board layouts

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | Medium |
| Priority | High |
| Date reported | 24 August 2026 |
| Area | Pasted-text importer |

## Summary

The pasted-text importer handled tidy `Label: Value` examples but initially failed to extract useful metadata from realistic job-board content where the title, employer, location, salary, and deadline appeared as stacked unlabelled lines.

## Affected area

Pasted-text job advertisement importer and extraction review.

## Environment

- Application: Job Application Tracker
- Runtime: .NET / ASP.NET Core MVC
- Browser: Chrome on Windows
- Host: Local development environment

## Preconditions

1. Sign in with a verified test account.
2. Open **Add application → Paste job text**.

## Steps to reproduce

1. Copy a realistic job advertisement containing a stacked role title, company, Australian location, salary, and application deadline.
2. Paste the complete advertisement into the importer.
3. Select **Extract and review**.
4. Inspect the suggested fields.

## Expected result

Clearly supported values such as role title, company, location, salary, and an explicit deadline are suggested. Uncertain fields remain blank for user review.

## Actual result

Most or all useful fields remain blank because the original extraction rules expect explicit labels.

## Impact

The user must retype information that is visibly present, undermining the purpose of the importer.

- **Severity:** Medium
- **Priority:** High

## Sanitized evidence

The failure was reproduced using layouts shaped like:

```text
2027 Computer Science Graduate Program - Cybersecurity
Example Consulting
Sydney NSW
$70,000 - $80,000 a year
...
Applications close on Sunday, 16 August.
```

## Resolution

**Status: Fixed and verified.**

Deterministic heuristics were added for stacked job-board headers, Australian locations, salary formats, platform phrases, and explicit closing/apply-by sentences. The solution remains rule-based and does not call an AI service.

## Regression coverage

- Synthetic SEEK-style and LinkedIn-style fixtures.
- Uncertain values remain blank.
- Existing labelled extraction continues to pass.
- Full formatting, Release build, automated test, and publish gate completed.

## Traceability

- [Public GitHub issue #1](https://github.com/Chit-Thway/job-application-tracker-qa/issues/1)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
