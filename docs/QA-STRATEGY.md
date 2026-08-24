# QA Strategy

## Purpose

This strategy defines how the private Job Application Tracker is assessed and how sanitized results are presented in this public QA portfolio.

## Quality objectives

Testing aims to confirm that:

1. users can create, review, update, and retain their own job-search records;
2. extracted values are supported by source evidence and remain editable before confirmation;
3. job-board-specific layouts do not override the selected job with page chrome, account greetings, or unrelated result cards;
4. responsive navigation remains operable with keyboard, pointer, and touch-sized viewports;
5. network imports fail safely without weakening private-network and SSRF protections;
6. fixes do not regress existing import methods or supported job sites.

## Scope

### In scope

- authenticated application workflows;
- companies and applications;
- pasted-text extraction;
- safe public-URL imports;
- Chrome extension capture;
- extraction review and confirmation;
- responsive navigation;
- data plausibility and encoding;
- security regression around outbound URL fetching.

### Out of scope for this public repository

- production credentials and infrastructure configuration;
- private source-code review;
- real user or job-search data;
- destructive production testing;
- complete third-party job advertisements;
- load and penetration testing against third-party job sites.

## Test environments

| Layer | Environment |
| --- | --- |
| Web application | Local ASP.NET Core development/release build |
| Data store | Isolated development PostgreSQL database |
| Desktop browser | Current Chrome on Windows |
| Extension | Unpacked development build with explicit-click active-tab access |
| Mobile checks | Chrome responsive viewport, including 390 px width |
| External compatibility | Public SEEK, Indeed, LinkedIn, and generic job pages using sanitized results |

Third-party pages change frequently, so deterministic local HTML fixtures protect the regression suite from live-site instability.

## Test techniques

- exploratory testing with realistic user workflows;
- equivalence partitioning for salary and metadata formats;
- boundary and plausibility checks for ratings, counts, pay rates, and dates;
- negative testing for missing or ambiguous employer evidence;
- integration testing across fetch, extraction, review, and confirmation;
- responsive and keyboard interaction testing;
- cross-browser-page compatibility testing;
- security regression for public/private address handling;
- deterministic automated regression tests for every practical defect.

## Severity model

| Severity | Definition |
| --- | --- |
| Critical | Security compromise, unrecoverable data loss, or application-wide outage |
| High | A primary workflow is blocked or the product is unusable for an affected device/site |
| Medium | A workflow completes incorrectly or requires substantial manual correction |
| Low | Limited usability, presentation, or clarity problem with a practical workaround |

## Priority model

| Priority | Definition |
| --- | --- |
| High | Fix before the affected milestone is accepted or released |
| Medium | Fix in the next planned quality pass |
| Low | Schedule when higher-impact work is complete |

Severity describes user impact; priority describes when the team intends to act.

## Defect workflow

```text
Observed → Reproduced → Documented → Fixed → Automated regression → Full gate → Manual retest → Closed
```

A report stays open until the implemented behaviour is manually accepted and the relevant regression gate passes.

## Entry criteria

Testing begins when:

- the intended feature is available in a local build;
- required migrations and test data are ready;
- the tester can reach the workflow with a dedicated account;
- expected behaviour and safety constraints are known.

## Exit criteria

A completed defect requires:

- the original reproduction no longer fails;
- a deterministic regression test where practical;
- no regression in adjacent import methods or layouts;
- formatting and Release build success;
- the complete automated test suite passing;
- publish/package verification where applicable;
- manual acceptance by the tester.

## Evidence and privacy

Preferred evidence, in order:

1. sanitized screenshot or short recording;
2. minimal deterministic HTML/text fixture;
3. exact error or evidence message;
4. repeatable environment and timing observation.

Evidence is omitted rather than published when it could expose credentials, personal information, private code, inaccessible repository links, or copyrighted job advertisements in full. Synthetic evidence is clearly described and is never presented as an original screenshot.

## Traceability

The private engineering repository holds implementation branches, commits, pull requests, and automated tests. This public repository records the externally understandable QA narrative without revealing private source history. Public issue state provides the authoritative portfolio status:

- **Open:** reproduced, not yet accepted as fixed.
- **Closed:** fixed, regression-tested, and manually verified.
