# Bug 04: URL import times out when IPv6 stalls before IPv4 fallback

[← Back to the reported bugs index](../README.md)

| Field | Value |
| --- | --- |
| Status | Fixed |
| Severity | Medium |
| Priority | High |
| Date reported | 24 August 2026 |
| Area | Networking / URL import |

## Summary

The safe URL importer could report a timeout for a public job page even when the same host was reachable quickly over IPv4.

## Affected area

Safe outbound HTTP connection handling for URL imports.

## Environment

- Application: Job Application Tracker
- Operating system: Windows
- Network condition: Resolved IPv6 and IPv4 candidates; IPv6 route unavailable
- Import target: Public HTTPS job page

## Preconditions

1. Sign in.
2. Open **Add application → Import public link**.
3. Use a host that resolves to both IPv6 and IPv4 while the local IPv6 route stalls.

## Steps to reproduce

1. Submit a valid public job URL.
2. Wait for the safe importer.
3. Observe the timeout fallback.
4. Request the same URL over IPv4 from the same machine.

## Expected result

The importer reaches the public site through the working address without waiting for one stalled candidate to consume the entire operation timeout.

## Actual result

The first unreachable IPv6 address consumes the shared timeout before the working IPv4 address is attempted.

## Impact

Valid public job pages appear unavailable, forcing users back to manual entry.

- **Severity:** Medium
- **Priority:** High

## Technical evidence

A direct IPv4 request from the same machine returned HTTP 200 HTML in approximately 2.28 seconds, isolating the defect to address-selection behaviour rather than website availability.

## Root cause

Already-validated DNS addresses were attempted sequentially under one timeout budget.

## Resolution

**Status: Fixed and verified.**

Validated IPv6 and IPv4 candidates are interleaved and attempted with a short stagger. The first successful stream wins; unfinished sockets are cancelled and disposed.

## Security and regression coverage

- Deterministic stalled-IPv6/working-IPv4 regression test.
- Private, loopback, link-local, and mixed public/private DNS results remain rejected.
- Existing SSRF protections remain unchanged.
- Locked restore, formatting, zero-warning Release build, 92 automated tests, and Release publish passed.

## Traceability

- [Public GitHub issue #4](https://github.com/Chit-Thway/job-application-tracker-qa/issues/4)
- [Live Job Application Tracker](https://myjobtracker.com.au/)

This report is sanitized for public portfolio use and contains no credentials, private source code, or personal job-search data.
