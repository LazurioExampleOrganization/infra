# GitHub Organization LazurioExampleOrganization

First recorded: 2026-05-23

## State

Verified 2026-10-18. Source: the GitHub REST API (Organization, members,
Teams, repositories, collaborators, rulesets and app installations), read on
2026-10-18, and the root `lazurio.organization.json`, read on 2026-10-16.

- Organization: `LazurioExampleOrganization` (id 325048785)
- URL: `https://github.com/LazurioExampleOrganization`
- Plan: Free. Every repository is public except the private Deployment Repo
  `machines`.
- Base permission of members: none. Two-factor authentication is required.
- Owners: the Owner (a Lazurio maintainer's account) and Bob
  (`lazurio-bob`). Member: Alena (`lazurio-alena`). Members are only the
  Lazurio maintainers and the fictional test accounts (EX-0014 D20).
- Display name in Lazurio: "Lazurio Example Organization"
- Root repository:
  `git@github.com:LazurioExampleOrganization/LazurioExampleOrganization_GEN3.git`
  (id 1421349619). Its Lazurio manifest binds the Organization and the root
  repository by these ids; the binding state is verified.
- Infra repository: `git@github.com:LazurioExampleOrganization/infra.git`
- GitHub Apps: Lazurio for GitHub and Lazurio Administration Access are
  installed on all repositories (installed 2026-10-16).

## Repositories

- `LazurioExampleOrganization_GEN3` (root)
- `infra`
- `design-system`
- `mission-control`
- `mission-control-data` (default branch `v3`)
- `knowledgebase`
- `research`
- `experiments`
- `playbooks`
- `content`
- `finance`
- `automations`
- `machines` (private Deployment Repo)

## Teams and rights

The Teams, their members and grants, and the right of every person on every
repository are in the [access matrix](matrix.md). In short: Team `workspace`
writes the workspace modules except `finance` and the root applications,
Team `finance` (Bob) writes `finance`, Team `sales` has no grant until the
sales modules exist, and the per-person Teams `lazurio-bob` and
`lazurio-alena` only admit their Work Environments.

## Rulesets

Verified 2026-10-18 by reading every ruleset back with `gh` (EX-0014 task
`task-2026-10-18-002`, milestone L1).

GitHub Free has no Organization rulesets, so each public repository has its
own repository ruleset, named "main", on its default branch. Every ruleset:

- blocks deletion and force push;
- requires a pull request: nothing reaches the default branch by a direct
  push, not even a fast-forward to a commit that was green on a pull request;
- allows only the merge commit as merge method (see
  [Merge method](#merge-method));
- requires zero approvals until the review automations run (see
  [One required approval](#one-required-approval-task-011));
- requires the repository's CI checks, from GitHub Actions, where CI exists;
- has no bypass actor. Nobody bypasses it: not Lazurio for GitHub, not
  Lazurio Administration Access, not an Organization owner. An owner changes
  a ruleset only as the [break-glass](#break-glass).

| Repository | Default branch | Ruleset id | Pull request | Required checks |
|---|---|---|---|---|
| `LazurioExampleOrganization_GEN3` | `main` | 25202734 | required | "Organization check" |
| `automations` | `main` | 25202742 | required | none, no CI yet |
| `content` | `main` | 25202741 | required | none, no CI yet |
| `design-system` | `main` | 25204916 | required | "check" |
| `experiments` | `main` | 25202744 | required | none, no CI yet |
| `finance` | `main` | 25202740 | required | none, no CI yet |
| `infra` | `main` | 25202739 | required | none, no CI yet |
| `knowledgebase` | `main` | 25202737 | required | "check" |
| `mission-control` | `main` | 25208607 | required | "bun run test (ubuntu-latest)", "bun run test (windows-latest)" |
| `mission-control-data` | `v3` | 25206628 | not required, held | "validate" |
| `playbooks` | `main` | 25202743 | required | none, no CI yet |
| `research` | `main` | 25202746 | required | none, no CI yet |
| `machines` (private) | `main` | none | the exception | none |

### Repositories without CI

`automations`, `content`, `experiments`, `finance`, `infra`, `playbooks` and
`research` have no CI workflow yet, so their rulesets require a pull request
but no check. No check is invented for them. When one of them gets a workflow
that runs on `pull_request`, its check is added to that repository's ruleset
in the same step.

### Held: `mission-control-data`

The ruleset of `v3` is unchanged: it blocks deletion and force push and
requires "validate", but it does not require a pull request. The Mission
Control App publishes a reviewed draft by one ordinary fast-forward push
straight to `v3`, and a required pull request would switch that off. The
Owner decides how `v3` gets the same rules
([mission-control-data#5](https://github.com/LazurioExampleOrganization/mission-control-data/issues/5)).
That issue also records that the required "validate" check probably rejects
the App's direct push already.

### The exception: the private Deployment Repo

`machines` is private, and GitHub Free has neither rulesets nor branch
protection for private repositories: the API answers HTTP 403. Its default
branch is therefore protected by process, not by GitHub. Only the owners and
the maintainers' agent account reach it, and the same rules apply there as a
rule of work: a change goes through a pull request merged with a merge
commit, and nobody force-pushes to or deletes `main`. GitHub does not enforce
them, so a direct push there still succeeds. A paid GitHub plan would let the
same ruleset apply.

### Who is affected

A direct push to the default branch of any public repository except
`mission-control-data` is rejected, for people and agents alike. Agents that
used to push to `main`, or to fast-forward `main` to a green pull request
head, now open a pull request and merge it. The rules of `v3` are unchanged
(see [Held](#held-mission-control-data)).

## Merge method

Merge a pull request with a merge commit ("Create a merge commit",
`gh pr merge --merge`); the rulesets allow no other method. The pull
request's commits keep their author, the noreply address of whoever wrote
them, and GitHub writes the merge commit itself with the merging account's
noreply address when that account keeps its email private, as the Owner's
does (infra#10, merge 442877d2).

A squash merge would replace the commits with a new one authored with the
merging account's default commit email, which need not be the noreply
address. The root `MIGRATION.md` records how this exposed an email in the
first root pull requests. Fast-forwarding `main` to the green head, the way
used during the migration, is a direct push that the rulesets now reject.

## Code owners

Every public repository except `mission-control-data` has
`.github/CODEOWNERS` with one rule for every path. GitHub asks the code
owners for a review when a pull request opens. Their approval is not
required, because no ruleset requires a code owner review.

| Code owner | Repositories | Why |
|---|---|---|
| Team `workspace` | `automations`, `content`, `design-system`, `experiments`, `knowledgebase`, `mission-control`, `playbooks`, `research` | The Team writes these repositories. |
| Bob (`@lazurio-bob`) | `finance` | Finance belongs to Bob: Team `finance` (Bob only) writes this restricted module. |
| Bob (`@lazurio-bob`) | `LazurioExampleOrganization_GEN3`, `infra` | Only the owners write these. GitHub accepts a code owner only with Write, and Team `workspace` has Read on the root and no grant on `infra`, so the Team cannot be named. Bob is the owner named. |

The pricing module, planned as `pricebook`, gets Bob as code owner when it is
created in milestone L3. `mission-control-data` gets its file together with
its ruleset decision. Check a file with:

```sh
gh api repos/LazurioExampleOrganization/<repository>/codeowners/errors --jq '.errors'
```

## One required approval (task 011)

Not switched on yet. When the review automations of task
`task-2026-10-18-011` run, an owner sets one required approval in the
ruleset of every repository above that requires a pull request, and reads it
back:

```sh
repo=<repository>; id=<ruleset id>
gh api repos/LazurioExampleOrganization/$repo/rulesets/$id \
  --jq '{name, target, enforcement, bypass_actors, conditions, rules}' \
  | jq '(.rules[] | select(.type == "pull_request") | .parameters)
        |= (.required_approving_review_count = 1
            | .require_last_push_approval = true)' \
  | gh api -X PUT repos/LazurioExampleOrganization/$repo/rulesets/$id --input -
gh api repos/LazurioExampleOrganization/$repo/rulesets/$id \
  --jq '.rules[] | select(.type == "pull_request") | .parameters'
```

GitHub never counts the author's own approval, so the approval comes from
another account. With `require_last_push_approval` the approval must also
come from someone other than the last pusher, so a push after the approval
needs a new one.

## Break-glass

No ruleset has a bypass actor. In an emergency an Organization owner, who is
Admin on every repository, edits the ruleset of the one affected repository:
removes the blocking rule or sets `enforcement` to `disabled`, makes the
change, and restores the ruleset at once. GitHub keeps every version of a
ruleset (`gh api repos/LazurioExampleOrganization/<repository>/rulesets/<id>/history`).
The owner records what was done and why in an issue in this repository.

### Read the rulesets back

```sh
gh api repos/LazurioExampleOrganization/<repository>/rulesets/<id> \
  --jq '{enforcement, bypass_actors, conditions, rules}'
gh api repos/LazurioExampleOrganization/<repository>/rules/branches/<default branch> \
  --jq '[.[].type]'
```

## Decided

- Roles (EX-0014 D20): the owners are the Owner and Bob; Alena is a member;
  visitors never become members.
- Restricted repositories (EX-0014 D23): `finance` and `infra` stay public, so
  Alena reads them, but she has no Write; Team `finance` writes `finance`.
- Governance (EX-0014 task `task-2026-10-18-002`): every public repository
  requires a pull request, its CI where it exists and a merge commit, has a
  CODEOWNERS file and has no bypass actor, as recorded in
  [Rulesets](#rulesets); `mission-control-data` is held.

## Next

- One required approval on every public repository once the review
  automations run: EX-0014 task `task-2026-10-18-011`, as described in
  [One required approval](#one-required-approval-task-011).
- A required pull request, CODEOWNERS and the approval for
  `mission-control-data`, after the Owner's decision in
  [mission-control-data#5](https://github.com/LazurioExampleOrganization/mission-control-data/issues/5).
- Required checks for the repositories without CI, when each gets its
  workflow.

## Guardrails

- No tokens, SSH keys or OAuth session data belong in this repository.
- Record access as rules and audit notes, not as secrets.
- Make real changes in the GitHub Organization only after explicit
  confirmation.
