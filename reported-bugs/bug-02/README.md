# Bug 02: Salary extractor uses employer rating instead of advertised pay range

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | Medium |
| Priority | High |
| Date reported | 24 August 2026 |
| Area | Salary extraction |

## Summary

When copied job-board text contains an early `Salary` heading followed by an employer rating and a later `Salary` heading followed by the genuine pay range, the review draft initially selected the rating as salary.

## Affected area

Salary extraction and review-draft evidence.

## Environment

- Application: Job Application Tracker
- Browser: Chrome on Windows
- Input: Pasted graduate-program advertisement

## Preconditions

1. Sign in.
2. Open **Add application → Paste job text**.

## Steps to reproduce

1. Paste text containing:

   ```text
   Salary
   4.2

   116 reviews
   ...
   Salary
   AUD 70,000 - 75,000 / Year
   ```

2. Select **Extract and review**.
3. Inspect the **Salary** field.

## Expected result

`4.2` and `116 reviews` are rejected as implausible salary values. The suggested salary is `AUD 70,000 - 75,000 / Year`.

## Actual result

The field contains `4.2` with high-confidence evidence because it immediately follows the first Salary heading.

## Impact

Confirming the draft stores incorrect compensation information and can mislead later comparisons.

- **Severity:** Medium
- **Priority:** High

## Root cause

The multiline label rule accepted the next non-empty line without applying salary-specific plausibility checks or continuing to a later duplicate heading.

## Resolution

**Status: Fixed and verified.**

Salary candidates now reject ratings, review counts, and vague text while retaining annual ranges, compact `70k–80k` values, decimal hourly ranges, and daily or weekly rates.

## Regression coverage

- Duplicate Salary-heading fixture.
- Employer ratings and review counts remain invalid.
- Annual, hourly, daily, and weekly pay formats remain valid.
- Manual retest returned the advertised pay range.

## Traceability

- [Public GitHub issue #2](https://github.com/Chit-Thway/job-application-tracker-qa/issues/2)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
