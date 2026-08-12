---
name: strix-security-review
description: Authorized security assessment wrapper for the pinned Strix runtime. Use only on systems, applications, repositories, APIs, or environments the user owns or is explicitly authorized to test.
---

# Strix Security Review — Authorized Targets Only

## Purpose
Use the pinned Strix runtime at `tools/strix/` as an offensive-security capable validation layer for applications and codebases the user is authorized to assess.

## Mandatory authorization gate
Before any active scanning, exploitation, payload delivery, credential testing, authenticated probing, or destructive/security-impacting action:
1. Confirm the target is owned by the user or that the user has explicit authorization to test it.
2. Define scope precisely: domains, repositories, environments, endpoints, accounts, and test windows.
3. Exclude third-party infrastructure, shared SaaS tenants, production systems, customer data, and external services unless explicitly authorized.
4. Prefer staging/local environments over production whenever possible.
5. Do not run destructive actions, persistence, denial-of-service, data deletion, credential spraying, lateral movement, malware deployment, or stealth/evasion techniques.
6. Never exfiltrate secrets or personal data. Redact sensitive values in logs and reports.

## Change-control gate
Security findings may inform fixes, but fixes must follow normal Git workflow:
- create a branch;
- implement narrowly scoped remediation;
- add/adjust tests;
- open a PR describing the finding, impact, fix, validation, and rollback;
- do not auto-merge security changes unless explicitly requested.

## Safe workflow
Scope → passive review → authorized active testing → validate finding → classify severity → propose remediation → branch/PR → retest after fix.

## Integration
Coordinate with Code Review Graph for impact analysis, ECC/gstack for review and testing, Task Observer for process improvements, Claude-Mem for prior decisions, and existing CI where appropriate. Do not duplicate scanners unnecessarily.

## Upstream reference
Read `tools/strix/README.md` and upstream docs before runtime activation. Keep credentials and provider keys in environment secrets only; never commit them to GitHub.
