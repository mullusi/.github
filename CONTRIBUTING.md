<!--
Purpose: define default contribution rules for Mullusi repositories.
Governance scope: change intake, verification evidence, public/private boundary discipline, and rollback expectation.
Dependencies: repository-specific README files, SECURITY.md, REPO_BOUNDARY.md, pull request template, and CI workflows.
Invariants: no secrets enter commits; public claims stay bounded; every accepted change has a verifier or explicit evidence gap.
-->

# Contributing

Mullusi accepts changes only when the repository boundary, causal effect, verification path, and rollback path are explicit.

## Change Contract

Every contribution must state:

1. Repository and module boundary changed.
2. Reason for the change.
3. Files and interfaces affected.
4. Verification command or evidence record.
5. Rollback path if the change misbehaves.

## Public Boundary

Do not include:

1. Production secrets, credentials, private keys, cookies, or provider tokens.
2. Internal roadmap, operational notebooks, private costs, or private deployment details.
3. Unsupported production claims.
4. Ethiopian script processing that decomposes fidel units, applies root-letter models, or normalizes fidel codepoints.

## Verification

Run the repository-specific verifier before requesting review. When no verifier exists, add one or document the explicit evidence gap in the pull request.

## Review Standard

A review checks boundary fit, causal trace, tests or validation evidence, security exposure, and rollback readiness. Formatting-only approval is not enough for runtime, deployment, release, or governance changes.
