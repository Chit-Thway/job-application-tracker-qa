# Bug 03: Company extractor treats a Location heading as the company name

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | Medium |
| Priority | High |
| Date reported | 24 August 2026 |
| Area | Company extraction |

## Summary

When a copied posting omits the employer line and places the `Location` heading directly below the job title, the extraction review initially suggested `Location` as the company name.

## Affected area

Company inference in the pasted-text importer.

## Environment

- Application: Job Application Tracker
- Browser: Chrome on Windows
- Host: Local development environment

## Preconditions

1. Sign in.
2. Open **Add application → Paste job text**.

## Steps to reproduce

1. Paste text beginning with:

   ```text
   Graduate Program (Feb 2027)
   Location
   Adelaide, Brisbane, Melbourne, Sydney
   ```

2. Select **Extract and review**.
3. Inspect **Company name**.

## Expected result

Company name remains blank because the source provides no reliable employer evidence. The Location heading identifies only the following location value.

## Actual result

Company name is suggested as `Location`, with evidence claiming it was inferred from the position below the title.

## Impact

Confirming the draft can create an invalid persistent company named `Location`, producing lasting data-quality problems.

- **Severity:** Medium
- **Priority:** High

## Root cause

The stacked-header heuristic considered the line below the title a possible employer but did not exclude known metadata headings.

## Resolution

**Status: Fixed and verified.**

Known metadata headings—including Location, Salary, Work type, and related labels—are no longer eligible company names.

## Regression coverage

- A title followed immediately by a known field heading leaves company blank.
- Confirmation cannot create a company from a metadata label.
- Valid stacked employer names continue to be extracted.

## Traceability

- [Public GitHub issue #3](https://github.com/Chit-Thway/job-application-tracker-qa/issues/3)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
