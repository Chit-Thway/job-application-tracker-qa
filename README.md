# Job Application Tracker — QA Portfolio

A public quality-assurance portfolio documenting real defects discovered while manually testing a live .NET job-application tracking system.

## Live project

- **Application:** [Open Job Application Tracker](https://chit-thway-job-tracker-b9bpfvb5csccb5hb.australiaeast-01.azurewebsites.net/)
- **Public read-only demo:** [Explore the synthetic dashboard](https://chit-thway-job-tracker-b9bpfvb5csccb5hb.australiaeast-01.azurewebsites.net/demo)
- **Extension privacy information:** [Review the browser-extension privacy page](https://chit-thway-job-tracker-b9bpfvb5csccb5hb.australiaeast-01.azurewebsites.net/extension/privacy)

The public demo uses fictional in-memory records and does not expose authenticated user data. The private tracker requires an invited, verified account.

> The application source repository is intentionally private. This repository contains sanitized defect reports, reproducible test evidence, resolution summaries, and regression results without exposing credentials, personal data, proprietary source code, or private commit history.

## Project under test

The Job Application Tracker is a private authenticated web application that helps users:

- record job applications and companies;
- import job advertisements from pasted text or public URLs;
- capture job details through a Chrome extension;
- review extracted information before saving it;
- manage contacts, follow-up tasks, appointments, and application status history;
- retain selected applications while applying time-based cleanup rules to unsaved records.

The application uses ASP.NET Core MVC on .NET, PostgreSQL through Supabase, and automated unit and integration testing.

## Current quality status

| Status | Count | Meaning |
| --- | ---: | --- |
| Fixed | 9 | The defect has been corrected; individual reports contain their available verification evidence. |
| Open | 1 | The LinkedIn extension fix awaits public release verification. |
| Total documented defects | 10 | All reports originated from hands-on acceptance or exploratory testing. |

## Defect register

| ID | Defect | Area | Status |
| --- | --- | --- | --- |
| [#1](../../issues/1) | Realistic unlabelled job-board text was not extracted | Pasted-text importer | Fixed |
| [#2](../../issues/2) | Employer rating was mistaken for salary | Data extraction | Fixed |
| [#3](../../issues/3) | A Location heading was mistaken for a company | Data extraction | Fixed |
| [#4](../../issues/4) | URL import timed out before IPv4 fallback | Networking | Fixed |
| [#5](../../issues/5) | SEEK page chrome was extracted instead of job details | URL importer | Fixed |
| [#6](../../issues/6) | Evidence text displayed corrupted punctuation | Encoding/UI | Fixed |
| [#7](../../issues/7) | LinkedIn focused job details are missed | Browser extension | Release verification pending |
| [#8](../../issues/8) | Mobile navigation covers content and cannot be dismissed reliably | Responsive UI | Fixed |
| [#9](../../issues/9) | Indeed capture selected the page heading instead of the focused job | Browser extension | Fixed |
| [#10](../../issues/10) | Extraction review creates duplicate companies instead of offering an existing match | Company matching | Fixed |

## Supporting documentation

- [QA strategy](docs/QA-STRATEGY.md) — scope, environments, test techniques, severity model, entry/exit criteria, regression gate, and evidence policy.
- [Structured bug-report form](../../issues/new?template=bug-report.yml) — reusable public issue template with required reproduction and privacy checks.

## Test approach

The reports demonstrate several complementary QA techniques:

- **Exploratory testing:** realistic job-board content was used rather than only tidy synthetic examples.
- **Boundary and plausibility testing:** ratings, review counts, annual salaries, and hourly pay ranges were compared.
- **Integration testing:** URL fetching, DNS address selection, HTML extraction, and draft creation were exercised together.
- **Cross-site compatibility testing:** SEEK, Indeed, LinkedIn, and generic job pages were assessed separately.
- **Responsive testing:** authenticated and demo navigation were checked at a narrow mobile viewport.
- **Regression testing:** each completed fix received a deterministic automated test where practical, followed by the full build/test/publish gate.
- **Security regression:** URL-import fixes retained the existing SSRF and private-network protections.

## Defect lifecycle

Each report follows the same traceable workflow:

1. Observe unexpected behaviour during manual testing.
2. Reproduce the behaviour consistently.
3. Record environment, preconditions, steps, expected result, and actual result.
4. Assess severity, priority, and user impact.
5. Isolate the probable cause without publishing private implementation details.
6. Implement and automate a regression check in the private engineering repository.
7. Run the complete quality gate.
8. Retest manually and close only after verification.

## Report structure

Every public defect includes:

- summary and affected area;
- environment and preconditions;
- numbered reproduction steps;
- expected and actual results;
- impact, severity, and priority;
- sanitized evidence;
- resolution and regression coverage for completed defects;
- verification status.

## Labels

The repository deliberately uses a minimal label set:

- `bug` — a reproducible product defect.

Issue state communicates the outcome: open issues remain unresolved; closed issues have been fixed and verified.

## Evidence policy

Screenshots are useful but not mandatory when a deterministic text fixture, exact error message, or repeatable URL scenario provides stronger reproduction evidence. Images are included only when they are available and contain no personal data, authentication details, private source code, or secrets.

## Privacy

This repository is documentation-only. It does not contain:

- application source code;
- production data;
- credentials or database connection details;
- private repository links;
- personal job-search information;
- third-party copyrighted job advertisements in full.

## Author

Created and tested by **Chit-Thway** as part of a practical full-stack engineering and software-quality portfolio.
