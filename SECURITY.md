<!--
Purpose: define default security reporting and response policy for Mullusi repositories.
Governance scope: vulnerability reports, secret exposure, governance bypasses, and launch-blocking safety issues.
Dependencies: GitHub issues, private disclosure by email, repository maintainers, and the Mullusi ops notebook.
Invariants: do not publish exploit details before triage; do not place secrets in issues, pull requests, or commits.
-->

# Security Policy

## Reporting

Report security issues privately by email:

```text
security contact: support@mullusi.com
operator contact: tamirat@mullusi.com
```

Use GitHub issues only for non-sensitive tracking after secrets, exploit steps,
and private provider details have been removed.

## Scope

Security reports include:

1. Secret exposure, credential leakage, or unsafe token handling.
2. Authorization or authentication bypass.
3. Unsafe deployment, DNS, package, or release authority.
4. Governance bypass in repository rules, release workflows, or runtime gates.
5. Mfidel atomicity violations in Ethiopian script handling.
6. Data exposure through logs, errors, artifacts, or public repositories.

## Response Contract

| Step | Requirement |
| --- | --- |
| Triage | Confirm affected repository, surface, and authority boundary |
| Containment | Revoke or rotate exposed credentials before public discussion |
| Repair | Patch source, workflow, host setting, or DNS/package authority |
| Verification | Run the relevant verifier before closure |
| Record | Link the issue, commit, release, or ops note that proves closure |

## Required Verifiers

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\verify-authority-gates.ps1
powershell -ExecutionPolicy Bypass -File .\scripts\verify-domains.ps1
```

Repository-specific verifiers may add stricter gates. The stricter gate wins.

## Non-Disclosure Boundary

Do not put the following in public artifacts:

1. Live tokens, private keys, cookies, or session values.
2. Provider account IDs that are not already public.
3. Exploit instructions before the affected surface is contained.
4. Private roadmap or operational notebook details.

## Resolution Stamp

A security issue is resolved only when:

1. The vulnerable state is no longer reachable.
2. The relevant verifier passes or records an explicit external blocker.
3. Follow-up authority work is tracked in an issue or ops note.
