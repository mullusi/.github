<!--
Purpose: require proof, boundary, and rollback evidence for Mullusi pull requests.
Governance scope: repository changes, workflow changes, release changes, and launch-facing surfaces.
Dependencies: repository verifiers, GitHub Actions, ops runbooks, and reviewer judgment.
Invariants: no pull request claims completion without verification evidence or an explicit blocker.
-->

## Boundary

Repository:
Surface:
Change type:

## Causal Change

What changed:

Why this change is required:

What must not change:

## Verification

Run the relevant checks and paste the result summary.

```text
command:
result:
```

Required when applicable:

- [ ] Source tests or static validation passed
- [ ] GitHub Actions passed or blocker is linked
- [ ] `verify-authority-gates.ps1` result recorded for launch/authority changes
- [ ] `verify-control-plane.ps1` result recorded for control-plane changes
- [ ] `verify-domains.ps1` result recorded for domain or Pages changes
- [ ] npm package state checked for SDK release changes

## Governance

- [ ] No secrets, private keys, cookies, or provider tokens are committed
- [ ] Public/private boundary is unchanged or explicitly justified
- [ ] Rollback path is known
- [ ] Open external authority blockers are linked
- [ ] Mfidel atomicity is preserved for Ethiopian script handling

## Linked Evidence

Issues:
Runs:
Docs:
