# GitHub Organization LazurioExampleOrganization

First recorded: 2026-05-23

## State

Verified 2026-10-18. Source: the GitHub REST API (Organization, members,
Teams, repositories, collaborators, rulesets and app installations), read on
2026-10-18, and the root `lazurio.organization.json`, read on 2026-10-16.
The repositories, their visibility, the Teams' repository grants and the
rulesets were read back on 2026-11-08 (plan DEV-6593); the members and the
[access matrix](matrix.md) are as of 2026-10-18.

- Organization: `LazurioExampleOrganization` (id 325048785)
- URL: `https://github.com/LazurioExampleOrganization`
- Plan: Free. Every repository is public except three private ones: the
  Deployment Repo `machines` and the Time Tracker repositories `time-tracker`
  and `time-tracker-data`.
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

Seventeen repositories, read back on 2026-11-08. All are public except the
three marked private.

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
- `app-access`
- `presentations` (public since 2026-11-06, see [`presentations`](#presentations))
- `machines` (private Deployment Repo)
- `time-tracker` (private)
- `time-tracker-data` (private, default branch `v3`)

## Teams and rights

The Teams, their members and grants, and the right of every person on every
repository are in the [access matrix](matrix.md). In short: Team `workspace`
writes the workspace modules except `finance` and the root applications,
Team `finance` (Bob) writes `finance`, Team `sales` has no grant until the
sales modules exist, and the per-person Teams `lazurio-bob` and
`lazurio-alena` only admit their Work Environments. Team `steward`, the
review account, has Maintain on every public repository and no grant on
the private ones, so it can review their pull requests (read back on
2026-11-08); Team
`server-services` reads the root.

## Rulesets

Verified 2026-10-18 by reading every ruleset back with `gh` (EX-0014 task
`task-2026-10-18-002`, milestone L1).

GitHub Free has no Organization rulesets, so each public repository has its
own repository ruleset, named "main", on its default branch. The one
exception is `presentations`, public since 2026-11-06, whose ruleset an owner
still creates (see [`presentations`](#presentations)); until then nothing
protects its `main`. Every ruleset:

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
| `mission-control` | `main` | 25208607 | required | "bun run check (ubuntu-latest)" (proposed with Mission Control 4.x, see below) |
| `mission-control-data` | `v3` | 25206628 | not required, held | "validate" |
| `playbooks` | `main` | 25202743 | required | none, no CI yet |
| `research` | `main` | 25202746 | required | none, no CI yet |
| `app-access` | `main` | 26692581 | required | none |
| `presentations` | `main` | none yet, see [`presentations`](#presentations) | proposed: required | proposed: "check" |
| `machines` (private) | `main` | none | the exception | none |
| `time-tracker` (private) | `main` | none | the exception | none |
| `time-tracker-data` (private) | `v3` | none | the exception | none |

### Mission Control 4.x: the required check (proposed 2026-11-06)

Read back on 2026-11-06 and again on 2026-11-08: ruleset 25208607 requires
only "bun run test (ubuntu-latest)" (not also "bun run test (windows-latest)"
as recorded on 2026-10-18). Mission Control 4.x, the Lazurio Marketplace
template the Organization takes at 4.1.1 in
[mission-control#7](https://github.com/LazurioExampleOrganization/mission-control/pull/7),
renames its Linux job to "bun run check (ubuntu-latest)". Its Windows job
"bun run check (windows-latest)" runs only when a pull request changes the
App, the templates or a workflow, so it cannot be required. Until the
ruleset requires the new name, #7 cannot be merged; after it does, no pull
request built on 3.1.0 can. So an owner changes the one context in the same
window as merging #7: Settings → Rules → Rulesets → "main" → Require status
checks, replace "bun run test (ubuntu-latest)" with
"bun run check (ubuntu-latest)" (GitHub Actions), and reads it back:

```sh
gh api repos/LazurioExampleOrganization/mission-control/rulesets/25208607 \
  --jq '.rules[] | select(.type=="required_status_checks") | .parameters.required_status_checks'
```

The data repository's required check stays "validate": the 4.x workflow
keeps that job name, so ruleset 25206628 of `mission-control-data` needs no
change.

### `presentations`

Created on 2026-11-06 by `lazurio module create` for the Marketplace
adoption of Presentations (plan DEV-6593), private like every module the
command creates. The same day, after a check of its tree and history, it was
made public like the Organization's other modules and got their Team grants:
`workspace` Write and `steward` Maintain (read back on 2026-11-08). A public
repository can have a ruleset on GitHub Free, but it has none yet, and no
`.github/CODEOWNERS`.

The owner's step, after
[presentations#1](https://github.com/LazurioExampleOrganization/presentations/pull/1)
brings the workflow `Check` with its job "check" to `main`: create the
ruleset "main" like that of `design-system` and read it back.

```sh
gh api -X POST repos/LazurioExampleOrganization/presentations/rulesets --input - <<'JSON'
{"name": "main", "target": "branch", "enforcement": "active",
 "conditions": {"ref_name": {"include": ["~DEFAULT_BRANCH"], "exclude": []}},
 "bypass_actors": [],
 "rules": [
  {"type": "deletion"},
  {"type": "non_fast_forward"},
  {"type": "required_status_checks", "parameters": {
    "strict_required_status_checks_policy": false, "do_not_enforce_on_create": false,
    "required_status_checks": [{"context": "check", "integration_id": 15368}]}},
  {"type": "pull_request", "parameters": {
    "allowed_merge_methods": ["merge"], "required_approving_review_count": 0,
    "dismiss_stale_reviews_on_push": false, "require_code_owner_review": false,
    "require_last_push_approval": false, "required_review_thread_resolution": false}}
 ]}
JSON
gh api repos/LazurioExampleOrganization/presentations/rulesets \
  --jq '.[] | {id, name, enforcement}'
```

Then the ruleset id goes into the table above.

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

### The exception: the private repositories

`machines`, `time-tracker` and `time-tracker-data` are private, and GitHub
Free has neither rulesets nor branch protection for private repositories:
the API answers HTTP 403 (read back on 2026-11-08). Their default branches
are therefore protected by process, not by GitHub. Only the owners and the
maintainers' agent account reach `machines`, and the same rules apply there
as a rule of work: a change goes through a pull request merged with a merge
commit, and nobody force-pushes to or deletes `main`. GitHub does not enforce
them, so a direct push there still succeeds. A paid GitHub plan would let the
same ruleset apply.

### Who is affected

A direct push to the default branch of any public repository except
`mission-control-data`, and `presentations` until its ruleset exists, is
rejected, for people and agents alike. Agents that
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

Every public repository except `mission-control-data` and `presentations`
has `.github/CODEOWNERS` with one rule for every path. GitHub asks the code
owners for a review when a pull request opens. Their approval is not
required, because no ruleset requires a code owner review.

| Code owner | Repositories | Why |
|---|---|---|
| Team `workspace` | `app-access`, `automations`, `content`, `design-system`, `experiments`, `knowledgebase`, `mission-control`, `playbooks`, `research` | The Team writes these repositories. |
| Bob (`@lazurio-bob`) | `finance` | Finance belongs to Bob: Team `finance` (Bob only) writes this restricted module. |
| Bob (`@lazurio-bob`) | `LazurioExampleOrganization_GEN3`, `infra` | Of the people's Teams, none writes these: Team `workspace` has Read on the root and no grant on `infra`, and GitHub accepts a code owner only with Write, so it cannot be named. The owners write them, and Team `steward`, the review account, has Maintain on them to review. Bob is the owner named. |

The pricing module, planned as `pricebook`, gets Bob as code owner when it is
created in milestone L3. `presentations` has no file yet; it gets Team
`workspace` like the other workspace modules. `mission-control-data` gets its file together with
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
  [Rulesets](#rulesets); `mission-control-data` is held, and `presentations`
  gets its ruleset and CODEOWNERS file as described in
  [`presentations`](#presentations).

## Next

- One required approval on every public repository once the review
  automations run: EX-0014 task `task-2026-10-18-011`, as described in
  [One required approval](#one-required-approval-task-011).
- A required pull request, CODEOWNERS and the approval for
  `mission-control-data`, after the Owner's decision in
  [mission-control-data#5](https://github.com/LazurioExampleOrganization/mission-control-data/issues/5).
- Required checks for the repositories without CI, when each gets its
  workflow.
- The ruleset "main" and `.github/CODEOWNERS` for `presentations`, as
  described in [`presentations`](#presentations).

## Guardrails

- No tokens, SSH keys or OAuth session data belong in this repository.
- Record access as rules and audit notes, not as secrets.
- Make real changes in the GitHub Organization only after explicit
  confirmation.
