<!--
Purpose: define the repository boundary map for the Mullusi GitHub organization.
Governance scope: repository role, visibility, license posture, production relation, and next control action.
Dependencies: GitHub organization mullusi, Cloudflare Pages, GitHub Pages, npm registry, and Mullusi domain routing gates.
Invariants: production secrets stay outside source; internal control artifacts are private; public repos describe only supportable claims.
-->

# Mullusi Repository Boundary Map

Observed on 2026-07-13 through connected GitHub repository metadata and
verified with repository-local governance gates.

## Operating Invariants

1. Public launch surfaces must have branch protection, required CI checks where available, and a documented deployment path.
2. Solo-developer flow must not require a second human reviewer; required checks and non-destructive branch rules are the active gate.
3. Internal operating notebooks, control-plane source, and private research journals must be private unless a public-release review approves disclosure.
4. Package release claims must match registry state. A GitHub release alone is not a package distribution.
5. Every active repository must have one owner, one purpose, one default branch, one verification path, and one rollback path.
6. No repository may store production secrets, credentials, private keys, or unredacted provider tokens.
7. Repository visibility evidence must distinguish required visibility from observed visibility. A public repository that is required to be private is `SolvedUnverified` or `GovernanceBlocked`, never `SolvedVerified`.

## 2026-07-13 Audit Snapshot

| Metric | Observation | Judgment |
| --- | --- | --- |
| Total Mullusi repositories visible to the installed GitHub connector | 15 | Inventory complete for connector-accessible repos |
| Public repositories | `.github`, `mullusi-docs` | Public set matches the strict private-source allowlist |
| Private repositories | `mullusi-company-site`, `mullusi-site`, `mullusi-core`, `mullusi-foundation`, `mullusi-artifacts`, `mullusi-journal`, `demo-repository`, `scc-harness`, `msic-sdk`, `ops`, `mullusi-control-plane`, `mullusi-io-redirect`, `mullusi-govern-cloud` | Website source, internal, control, and research repositories are private |
| Archived private repositories | `mullusi-foundation`, `mullusi-artifacts`, `demo-repository` | Correct low-noise posture |
| Strict public allowlist | `.github`, `mullusi-docs` | Preferred target state |
| Transitional no-budget allowlist | Not active | Private-source hardening is complete for the website repositories |
| Dedicated secret scan | Gitleaks v8.30.1 scanned the complete reachable histories of the two website repositories and the two public repositories | Three detections were classified as synthetic test or commit-reference fixtures; no credential finding remained open |

## Boundary Table

| Repository | Role | Required visibility | Observed 2026-07-13 | License stance | Production relation | Next action |
| --- | --- | --- | --- | --- | --- | --- |
| `mullusi-company-site` | Source package for `mullusi.com` public website | Private | Private | All-rights-reserved source notice | Production website deploys to Cloudflare Pages from private source; live origin and redirects passed after the visibility transition | Keep private; require the strict visibility gate and deployment artifact checks before release |
| `mullusi-site` | Legacy website governance and deployment evidence repository | Private | Private | All-rights-reserved source notice | Not the live DNS origin; retained as private governance and historical evidence | Keep private; do not reintroduce a public source exception |
| `mullusi-docs` | Public technical documentation for `docs.mullusi.com` | Public | Public | Publication policy; no broad reuse grant without explicit license | Production docs through GitHub Pages or Cloudflare Pages; docs-only exception | Keep `KeepPublicBounded`; require docs validation and claim discipline |
| `mullusi-io-redirect` | Redirect artifact for future `mullusi.io` routing | Private | Private | Private until routing gate passes | Not live; `mullusi.io` is SafeHalt until DNS authority and HTTPS are verified | Keep private; resolve DNS authority and HTTPS before publication |
| `msic-sdk` | TypeScript SDK for governed symbolic intelligence cell work | Private | Private | MIT | Release candidate source and package source | Keep private merge fallback controls; publish or retract npm install claims |
| `mullusi-control-plane` | API and dashboard control-plane baseline for `api.mullusi.com` and `dashboard.mullusi.com` | Private until launch review | Private | Add explicit license or private-use notice | Deployment blueprint present; production host not verified here | Keep private merge fallback controls; deploy after DNS and host secrets are configured |
| `mullusi-govern-cloud` | Govern Cloud backend for `api.mullusi.com` governed evaluation and proof stamps | Private until launch review | Private | Private-use notice recommended | CI and release-image workflow pass; production host, database, DNS, and secrets not verified here | Keep private merge fallback controls; deploy only after persistence and proof-stamp secrets are configured |
| `ops` | Internal operating map and company control notebook | Private | Private | Private-use notice recommended | Source of operational truth, not public product | Keep private merge fallback controls |
| `.github` | Organization defaults, templates, and shared policies | Public | Public | MIT for reusable templates/policies only | Governance support repository; no product or runtime source | Keep public only while content is generic policy/template material |
| `scc-harness` | Governed execution harness | Private | Private | Existing nonstandard license | Kernel research and execution substrate | Keep private merge fallback controls; run CI before integration |
| `mullusi-core` | Symbolic execution prototype | Private | Private | Existing license; keep private until review | Legacy or foundation reference | Keep private unless a scoped public release review passes |
| `mullusi-foundation` | Archived foundation notes and formal blueprint seed | Private archived | Private archived | Existing license; keep private until review | Research reference only | Keep archived until a scoped revival issue exists |
| `mullusi-artifacts` | Archived demos and generated symbolic tools | Private archived | Private archived | Add explicit license or policy notice before revival | Demo/reference material only | Keep archived until scrubbed and indexed |
| `mullusi-journal` | Internal symbolic journal and proof sketches | Private | Private | Private-use notice recommended | Internal memory and research trace | Keep private merge fallback controls |
| `demo-repository` | Generic GitHub demo repository | Private archived | Private archived | None needed after archive | No production relation | Keep archived to reduce organization noise |

## License Boundary

The MIT license in this repository applies to reusable organization templates,
CODEOWNERS hints, issue templates, pull request templates, and public policy
text stored in `.github`. It does not grant rights to Mullusi private product
source, runtime systems, research kernels, deployment secrets, brand assets, or
other repositories unless those repositories include their own explicit license.

## Change Authority

Repository visibility, archive state, branch protection, and release channels are governance-level controls. Changes require a recorded reason in commit history, issue history, or operator log.

## Visibility Decision Rules

1. If a repository contains source code, runtime implementation, private research, deployment wiring, recovery records, unpublished product logic, or operational notebooks, the default required visibility is private.
2. Public visibility is allowed only for organization templates, public documentation, launch-safe evidence mirrors, or intentionally published packages/artifacts.
3. `mullusi-company-site` and `mullusi-site` are private and are not public transitional exceptions.
4. Do not mark the repository boundary as `SolvedVerified` if the observed public set exceeds the strict public allowlist.
5. A future public-release review may move a repository from private-required to public-allowed only if claims, license, secrets, IP disclosure, build/deploy evidence, and rollback are recorded.

## Verification Commands

```powershell
gh repo list mullusi --limit 200 --json name,visibility,isArchived,defaultBranchRef
gh repo view mullusi/.github --json nameWithOwner,description,visibility,isPrivate,isArchived,repositoryTopics
gh repo view mullusi/mullusi-company-site --json nameWithOwner,visibility,isPrivate,isArchived,defaultBranchRef
gh repo view mullusi/mullusi-site --json nameWithOwner,visibility,isPrivate,isArchived,defaultBranchRef
gh run list --repo mullusi/mullusi-site --limit 5
gh run list --repo mullusi/mullusi-docs --limit 5
gh run list --repo mullusi/mullusi-io-redirect --limit 5
gh run list --repo mullusi/mullusi-control-plane --limit 5
gh run list --repo mullusi/mullusi-govern-cloud --limit 5
gh run list --repo mullusi/msic-sdk --limit 5
npm.cmd view @mullusi/msic-sdk version dist-tags --json
```

## Historical Secret-Scan Receipt

The 2026-07-13 closure audit used checksum-verified Gitleaks v8.30.1 with
100-percent match redaction against every reachable commit in the four
repositories that define the website/public boundary.

| Repository | Commits reported scanned | Raw detections | Classification |
| --- | ---: | ---: | --- |
| `mullusi-company-site` | 716 | 1 | `ops/deployment-current-witness.md` stored a 40-character Git commit reference that resolves to a commit; false positive |
| `mullusi-site` | 575 | 2 | Deterministic values in `backend/tests/test_preflight_release.py`; synthetic test fixtures, not production credentials |
| `.github` | 21 | 0 | Pass |
| `mullusi-docs` | 17 | 0 | Pass |

The two public repositories also report GitHub secret scanning and push
protection enabled. `node scripts/validate-docs.mjs` passed for
`mullusi-docs`. The redacted reports were retained only in the temporary audit
workspace and were not committed.

## Proof Record

Outcome target: `SolvedVerified`.

Current repository-visibility outcome: `SolvedVerified`. The observed public
set matches the strict allowlist, the private-source website remains live
through Cloudflare, and the historical secret-scan detections are resolved.
This outcome does not promote separate SDK publication, control-plane
deployment, or universal availability claims.

Witness requirements:

1. Production website source is private and Cloudflare Pages serves only the public artifact.
2. Public repositories are bounded to documentation, evidence mirrors, or organization templates.
3. Internal repos are not public.
4. Demo and sensitive artifact repositories remain private or archived.
5. SDK package distribution state is either published or documentation is corrected.
6. Control-plane deployment is verified by runtime health checks before public launch.
7. A dedicated current-history secret scan is recorded with every detection classified.

## Immediate Remediation Queue

1. Keep `mullusi-company-site` and `mullusi-site` private.
2. Keep `.github` and `mullusi-docs` public and bounded.
3. Keep `mullusi-control-plane`, `mullusi-govern-cloud`, `ops`, `msic-sdk`, `scc-harness`, `mullusi-core`, and `mullusi-journal` private.
4. Keep archived private repositories archived until a revival issue defines owner, purpose, verifier, license, and scrub plan.
5. Repeat the public-boundary inventory and historical secret scan before any future repository is made public.

STATUS:
  Completeness: 100%
  Invariants verified: strict public allowlist, private website source, bounded public repositories, historical secret scan, Cloudflare continuity
  Open issues: none for repository visibility boundary
  Next action: preserve this boundary and reopen governance review before any future visibility change
