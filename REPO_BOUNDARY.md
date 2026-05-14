<!--
Purpose: define the repository boundary map for the Mullusi GitHub organization.
Governance scope: repository role, visibility, license posture, production relation, and next control action.
Dependencies: GitHub organization mullusi, GitHub Pages, npm registry, Render deployment blueprint, and Mullusi domain routing.
Invariants: production secrets stay outside source; internal control artifacts are private; public repos describe only supportable claims.
-->

# Mullusi Repository Boundary Map

Observed on 2026-05-14.

## Operating Invariants

1. Public launch surfaces must have branch protection, CI, and a documented deployment path.
2. Internal operating notebooks, control-plane source, and private research journals must be private unless a public-release review approves disclosure.
3. Package release claims must match registry state. A GitHub release alone is not a package distribution.
4. Every active repository must have one owner, one purpose, one default branch, one verification path, and one rollback path.
5. No repository may store production secrets, credentials, private keys, or unredacted provider tokens.

## Boundary Table

| Repository | Role | Required visibility | License stance | Production relation | Next action |
| --- | --- | --- | --- | --- | --- |
| `mullusi-site` | Public company website for `mullusi.com` | Public | MIT | Production public site through GitHub Pages | Protect `main`; keep Pages validation required |
| `mullusi-docs` | Public technical documentation for `docs.mullusi.com` | Public | Add explicit license or policy notice | Production docs through GitHub Pages | Protect `main`; keep docs validation required |
| `msic-sdk` | Private TypeScript SDK for governed symbolic intelligence cell work | Private | MIT | Release candidate source and package source | Protect `main`; publish or retract npm install claims |
| `mullu-control-plane` | API and dashboard control-plane baseline for `api.mullusi.com` and `dashboard.mullusi.com` | Private until launch review | Add explicit license or private-use notice | Deployment blueprint present; production host not verified here | Protect `main`; deploy after DNS and host secrets are configured |
| `ops` | Internal operating map and company control notebook | Private | Private-use notice recommended | Source of operational truth, not public product | Make private; protect `main` |
| `.github` | Organization defaults, templates, and shared policies | Public | MIT | Governance support repository | Protect `main`; maintain this boundary map |
| `scc-harness` | Private governed execution harness | Private | Existing nonstandard license | Kernel research and execution substrate | Protect `master`; run CI before integration |
| `mullusi-core` | Older public symbolic execution prototype | Public or archive after migration | GPL-3.0 | Legacy or foundation reference | Resolve issue #1; decide revive versus migrate |
| `mullusi-foundation` | Public foundation notes and formal blueprint seed | Public | GPL-3.0 | Research reference | Keep public if scrubbed; add structure or archive policy |
| `mullusi-artifacts` | Public demos and generated symbolic tools | Public after scrub | Add explicit license or policy notice | Demo/reference material only | Add artifact index or archive stale material |
| `mullusi-journal` | Internal symbolic journal and proof sketches | Private | Private-use notice recommended | Internal memory and research trace | Make private |
| `demo-repository` | Generic GitHub demo repository | Archived | None needed after archive | No production relation | Archive to reduce organization noise |

## Change Authority

Repository visibility, archive state, branch protection, and release channels are governance-level controls. Changes require a recorded reason in commit history, issue history, or operator log.

## Verification Commands

```powershell
gh repo list mullusi --limit 200 --json name,visibility,isArchived,defaultBranchRef
gh run list --repo mullusi/mullusi-site --limit 5
gh run list --repo mullusi/mullusi-docs --limit 5
gh run list --repo mullusi/mullu-control-plane --limit 5
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
