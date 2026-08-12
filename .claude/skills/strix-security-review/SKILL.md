---
name: strix-security-review
description: Authorized security assessment wrapper for the pinned Strix runtime. Use only on systems, applications, repositories, APIs, or environments the user owns or is explicitly authorized to test.
---

# Strix Security Review — Authorized Targets Only

Use the pinned upstream Strix runtime at `tools/strix/` only for security testing of user-owned or explicitly authorized targets.

## Controls
- Confirm authorization and exact scope before active testing.
- Prefer local/staging systems over production.
- Do not test unrelated third-party services or shared infrastructure.
- Do not perform destructive actions, denial of service, persistence, malware deployment, credential spraying, lateral movement, or stealth/evasion.
- Do not exfiltrate secrets or personal data; redact sensitive evidence.
- Keep API/provider credentials in environment secrets, never in source control.
- Route remediation through a branch and pull request; do not silently patch production or auto-merge unless explicitly requested.

## Workflow
Scope → passive review → authorized active test → validate finding → severity/impact → remediation PR → retest.

Read `tools/strix/README.md` and upstream docs before runtime activation.
