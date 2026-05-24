<!--
Purpose: define the repository boundary map for the Mullusi GitHub organization.
Governance scope: repository role, visibility, license posture, production relation, and next control action.
Dependencies: GitHub organization mullusi, Cloudflare Pages, GitHub Pages, npm registry, and Mullusi domain routing gates.
Invariants: production secrets stay outside source; internal control artifacts are private; public repos describe only supportable claims.
-->

# Mullusi Repository Boundary Map

Observed on 2026-05-24.

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
| `mullusi-company-site` | Private source for `mullusi.com` public website | Private | All-rights-reserved source notice | Production website through Cloudflare Pages | Keep `main` validated; deploy only `dist`; preserve Cloudflare handoff gates |
| `mullusi-site` | Public governance mirror for website deployment evidence | Public | All-rights-reserved public evidence boundary | Not a live DNS origin; production source remains `mullusi-company-site` | Keep evidence-only; do not add strategic source changes |
| `mullusi-docs` | Public technical documentation for `docs.mullusi.com` | Public | Publication policy; no broad reuse grant without explicit license | Production docs through GitHub Pages; docs-only exception | Keep `KeepPublicBounded`; require docs validation and claim discipline |
| `mullusi-io-redirect` | Private redirect artifact for future `mullusi.io` routing | Private | Private until routing gate passes | Not live; `mullusi.io` is SafeHalt under Namecheap forwarding/parking | Resolve DNS authority and HTTPS before publication |
| `msic-sdk` | Private TypeScript SDK for governed symbolic intelligence cell work | Private | MIT | Release candidate source and package source | Keep private merge fallback controls; publish or retract npm install claims |
| `mullusi-control-plane` | API and dashboard control-plane baseline for `api.mullusi.com` and `dashboard.mullusi.com` | Private until launch review | Add explicit license or private-use notice | Deployment blueprint present; production host not verified here | Keep private merge fallback controls; deploy after DNS and host secrets are configured |
| `mullusi-govern-cloud` | Private Govern Cloud backend for `api.mullusi.com` governed evaluation and proof stamps | Private until launch review | Private-use notice recommended | CI and release-image workflow pass; production host, database, DNS, and secrets not verified here | Keep private merge fallback controls; deploy only after persistence and proof-stamp secrets are configured |
| `ops` | Internal operating map and company control notebook | Private | Private-use notice recommended | Source of operational truth, not public product | Keep private merge fallback controls |
| `.github` | Organization defaults, templates, and shared policies | Public | MIT for reusable templates/policies only | Governance support repository; no product or runtime source | Maintain this boundary map; keep public only while content is generic policy/template material |
| `scc-harness` | Private governed execution harness | Private | Existing nonstandard license | Kernel research and execution substrate | Keep private merge fallback controls; run CI before integration |
| `mullusi-core` | Private symbolic execution prototype | Private | Existing license; keep private until review | Legacy or foundation reference | Keep private unless a scoped public release review passes |
| `mullusi-foundation` | Private archived foundation notes and formal blueprint seed | Private archived | Existing license; keep private until review | Research reference only | Keep archived until a scoped revival issue exists |
| `mullusi-artifacts` | Private archived demos and generated symbolic tools | Private archived | Add explicit license or policy notice before revival | Demo/reference material only | Keep archived until scrubbed and indexed |
| `mullusi-journal` | Internal symbolic journal and proof sketches | Private | Private-use notice recommended | Internal memory and research trace | Keep private merge fallback controls |
| `demo-repository` | Generic GitHub demo repository | Private archived | None needed after archive | No production relation | Keep archived to reduce organization noise |

## License Boundary

The MIT license in this repository applies to reusable organization templates,
CODEOWNERS hints, issue templates, pull request templates, and public policy
text stored in `.github`. It does not grant rights to Mullusi private product
source, runtime systems, research kernels, deployment secrets, brand assets, or
other repositories unless those repositories include their own explicit license.

## Change Authority

Repository visibility, archive state, branch protection, and release channels are governance-level controls. Changes require a recorded reason in commit history, issue history, or operator log.

## Verification Commands

```powershell
gh repo list mullusi --limit 200 --json name,visibility,isArchived,defaultBranchRef
gh repo view mullusi/.github --json nameWithOwner,description,visibility,isPrivate,isArchived,repositoryTopics
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

1. Production website source is private and Cloudflare Pages serves only the public artifact.
2. Public repositories are bounded to documentation, evidence mirrors, or organization templates.
3. Internal repos are not public.
4. Demo and sensitive artifact repositories remain private or archived.
5. SDK package distribution state is either published or documentation is corrected.
6. Control-plane deployment is verified by runtime health checks before public launch.
