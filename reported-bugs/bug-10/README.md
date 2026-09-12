# Bug 10: Extraction review creates duplicate companies instead of offering an existing match

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | Medium |
| Priority | High |
| Date reported | 24 August 2026 |
| Area | Company matching |

## Summary

Creating applications through extraction review can produce duplicate owner-scoped company records when the extracted employer has the same name as an existing company but a different extracted location.

## Affected area

Application extraction review, company matching, and company creation.

## Environment

- Application: [Live Job Application Tracker](https://myjobtracker.com.au/)
- Date observed: 24 August 2026
- Browser: Chrome on Windows
- Workflow: Extract job advertisement → review draft → confirm application

## Preconditions

1. Sign in with a verified test account.
2. Create or confirm an application associated with a company named `Accenture`.
3. Import and review a second Accenture role whose extracted location differs from the first company record.

## Steps to reproduce

1. Import the first Accenture job advertisement.
2. Review and confirm the extracted application and company.
3. Import a second Accenture job advertisement with a different extracted location.
4. Review and confirm it without being offered the existing Accenture company.
5. Open **Applications** and verify both applications.
6. Open **Companies** and inspect the company cards.

## Expected result

During review, the application compares the extracted company name with companies owned by the signed-in user.

When a credible same-company candidate exists, the page shows a green **Same company detected** notice and lets the user explicitly choose between:

- reusing the existing company; or
- keeping/creating the extracted company as a separate record.

The application must never merge automatically.

## Actual result

Both applications display the employer as Accenture, but confirmation creates two separate owner-scoped Accenture company rows differentiated only by their extracted locations. The Companies page then displays duplicate Accenture cards.

## Impact

Duplicate companies fragment the user’s application history and company context. Contacts, notes, and later applications can become distributed across records that represent the same employer.

- **Severity:** Medium
- **Priority:** High

## Observed evidence

The Applications page shows two separate saved applications associated with Accenture:

![Applications showing two Accenture roles](https://raw.githubusercontent.com/Chit-Thway/job-application-tracker-qa/main/evidence/issue-10-duplicate-companies/applications-showing-two-accenture-roles.png)

The Companies page shows two separate Accenture cards differentiated by extracted location:

![Companies showing duplicate Accenture cards](https://raw.githubusercontent.com/Chit-Thway/job-application-tracker-qa/main/evidence/issue-10-duplicate-companies/companies-showing-duplicate-accenture-cards.png)

## Matching requirements

Candidate detection must:

- remain strictly owner-scoped;
- normalize harmless differences in case, spacing, and punctuation;
- treat an exact normalized name as a strong candidate;
- allow one normalized name to contain the other only when the shorter value is a meaningful company-name phrase;
- avoid weak substring matches such as short tokens or incidental word fragments;
- show the candidate and decision to the user before confirmation;
- preserve both records when the user deliberately chooses to create the extracted company;
- never merge, rename, or delete companies automatically.

## Acceptance and regression checks

- An owner with existing `Accenture` sees a same-company candidate while reviewing another Accenture role with a different location.
- The user can explicitly reuse the existing company.
- The user can explicitly keep/create the extracted company.
- Equivalent casing, punctuation, and spacing remain detectable.
- Meaningful long-form/short-form company-name variants are detectable.
- Weak substring examples do not produce a candidate.
- A company belonging to another owner is never suggested or reused.
- Manual entry and existing exact company selection continue to work.
- Deterministic unit and integration regression tests cover candidate detection, both user decisions, and owner isolation.
- The full formatting, Release build, automated test, and publish gate passes.
- Manual acceptance is completed before closing.

## Resolution

**Status: Fixed.**

The extraction-review workflow now treats credible owner-scoped company-name matches as an explicit user decision: reuse the detected existing company or keep/create the extracted company. It does not merge records automatically or inspect another owner’s companies.

## Traceability

- [Public GitHub issue #10](https://github.com/Chit-Thway/job-application-tracker-qa/issues/10)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
