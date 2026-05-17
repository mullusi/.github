<!--
Purpose: define the repository boundary map for the Mullusi GitHub organization.
Governance scope: repository role, visibility, license posture, production relation, and next control action.
Dependencies: GitHub organization mullusi, GitHub Pages, npm registry, Render deployment blueprint, and Mullusi domain routing.
Invariants: production secrets stay outside source; internal control artifacts are private; public repos describe only supportable claims.
-->

# Mullusi Repository Boundary Map

Observed on 2026-05-16.

## Operating Invariants

1. Public launch surfaces must have branch protection, required CI checks where available, and a documented deployment path.
2. Solo-developer flow must not require a second human reviewer; required checks and non-destructive branch rules are the active gate.
3. Internal operating notebooks, control-plane source, and private research journals must be private unless a public-release review approves disclosure.
4. Package release claims must match registry state. A GitHub release alone is not a package distribution.
5. Every active repository must have one owner, one purpose, one default branch, one verification path, and one rollback path.
6. No repository may store production secrets, credentials, private keys, or unredacted provider tokens.

## Boundary Table

| Repository | Role | Required visibility | License stance | Production relation | Next action |
| --- | --- | --- | --- | --- | --- |
| `mullusi-site` | Public company website for `mullusi.com` | Public | MIT | Production public site through GitHub Pages | Protect `main`; require `validate`; keep reviews optional for solo flow |
| `mullusi-docs` | Public technical documentation for `docs.mullusi.com` | Public | Publication policy proposed in `mullusi-docs#1` | Production docs through GitHub Pages | Protect `main`; require `validate`; keep reviews optional for solo flow |
| `mullusi-io-redirect` | Static redirect from `mullusi.io` to `mullusi.com` | Public | All-rights-reserved public rights boundary present | Launch-support redirect through GitHub Pages; DNS cutover pending | Protect `main`; require `validate`; keep reviews optional for solo flow |
| `msic-sdk` | Private TypeScript SDK for governed symbolic intelligence cell work | Private | MIT | Release candidate source and package source | Keep private merge fallback controls; publish or retract npm install claims |
| `mullusi-control-plane` | API and dashboard control-plane baseline for `api.mullusi.com` and `dashboard.mullusi.com` | Private until launch review | Add explicit license or private-use notice | Deployment blueprint present; production host not verified here | Keep private merge fallback controls; deploy after DNS and host secrets are configured |
| `mullusi-govern-cloud` | Private Govern Cloud backend for `api.mullusi.com` governed evaluation and proof stamps | Private until launch review | Private-use notice recommended | CI and release-image workflow pass; production host, database, DNS, and secrets not verified here | Keep private merge fallback controls; deploy only after persistence and proof-stamp secrets are configured |
| `ops` | Internal operating map and company control notebook | Private | Private-use notice recommended | Source of operational truth, not public product | Keep private merge fallback controls |
| `.github` | Organization defaults, templates, and shared policies | Public | MIT | Governance support repository | Protect `main`; maintain this boundary map; keep reviews optional for solo flow |
| `scc-harness` | Private governed execution harness | Private | Existing nonstandard license | Kernel research and execution substrate | Keep private merge fallback controls; run CI before integration |
| `mullusi-core` | Older public symbolic execution prototype | Public or archive after migration | GPL-3.0 | Legacy or foundation reference | Resolve issue #1; decide revive versus migrate |
| `mullusi-foundation` | Public foundation notes and formal blueprint seed | Archived public | GPL-3.0 | Research reference only | Keep archived until a scoped revival issue exists |
| `mullusi-artifacts` | Public demos and generated symbolic tools | Archived public | Add explicit license or policy notice before revival | Demo/reference material only | Keep archived until scrubbed and indexed |
| `mullusi-journal` | Internal symbolic journal and proof sketches | Private | Private-use notice recommended | Internal memory and research trace | Keep private merge fallback controls |
| `demo-repository` | Generic GitHub demo repository | Archived | None needed after archive | No production relation | Archive to reduce organization noise |

## Change Authority

Repository visibility, archive state, branch protection, and release channels are governance-level controls. Changes require a recorded reason in commit history, issue history, or operator log.

## Verification Commands

```powershell
gh repo list mullusi --limit 200 --json name,visibility,isArchived,defaultBranchRef
gh run list --repo mullusi/mullusi-site --limit 5
gh run list --repo mullusi/mullusi-docs --limit 5
gh run list --repo mullusi/mullusi-io-redirect --limit 5
gh run list --repo mullusi/mullusi-control-plane --limit 5
gh run list --repo mullusi/mullusi-govern-cloud --limit 5
gh run list --repo mullusi/msic-sdk --limit 5
npm.cmd view @mullusi/msic-sdk version dist-tags --json
```

## Proof Record

Outcome target: `SolvedVerified`.

Witness requirements:

1. Active production repos have protected default branches.
2. Internal repos are not public.
3. Demo repository is archived.
4. SDK package distribution state is either published or documentation is corrected.
5. Control-plane deployment is verified by runtime health checks before public launch.
