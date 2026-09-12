# Reported bugs

This directory contains the detailed QA records for defects discovered through acceptance and exploratory testing of the Job Application Tracker.

Select a bug number below to open its reproduction steps, impact assessment, resolution, and regression evidence.

| ID | Defect | Area | Severity | Status |
| --- | --- | --- | --- | --- |
| [Bug 01](bug-01/README.md) | Pasted-text importer misses realistic unlabelled job-board layouts | Pasted-text importer | Medium | Fixed |
| [Bug 02](bug-02/README.md) | Salary extractor uses employer rating instead of advertised pay range | Salary extraction | Medium | Fixed |
| [Bug 03](bug-03/README.md) | Company extractor treats a Location heading as the company name | Company extraction | Medium | Fixed |
| [Bug 04](bug-04/README.md) | URL import times out when IPv6 stalls before IPv4 fallback | Networking / URL import | Medium | Fixed |
| [Bug 05](bug-05/README.md) | SEEK URL import extracts page chrome instead of job details | SEEK URL import | Medium | Fixed |
| [Bug 06](bug-06/README.md) | Extraction evidence displays corrupted punctuation | Encoding / extraction UI | Low | Fixed |
| [Bug 07](bug-07/README.md) | Browser extension misses LinkedIn focused job details | LinkedIn browser extension | Medium | Fixed |
| [Bug 08](bug-08/README.md) | Mobile navigation opens over content and cannot be dismissed reliably | Responsive navigation | High | Fixed |
| [Bug 09](bug-09/README.md) | Browser extension captures Indeed page heading instead of selected job | Indeed browser extension | Medium | Fixed |
| [Bug 10](bug-10/README.md) | Extraction review creates duplicate companies instead of offering an existing match | Company matching | Medium | Fixed |

## Reading the reports

Each report uses the same practical workflow:

1. Establish the environment and preconditions.
2. Reproduce the defect using numbered steps.
3. Compare the expected and actual results.
4. assess severity, priority, and user impact.
5. Record the implemented resolution.
6. Confirm regression coverage and closure.

All 10 defects in this report set are fixed and their corresponding GitHub issues are closed.

[← Return to the portfolio overview](../README.md)
