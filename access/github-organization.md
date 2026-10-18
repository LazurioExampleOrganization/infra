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

- A ruleset named "main" applies to the default branch of every public
  repository (`v3` for `mission-control-data`). The private Deployment Repo
  has none, because GitHub Free has no rulesets for private repositories.
- Each ruleset blocks deletion and force push.
- Required status checks: "Organization check" in the root repository,
  "check" in `knowledgebase` and `design-system`, "bun run test
  (ubuntu-latest)" and "bun run test (windows-latest)" in `mission-control`,
  and "validate" in `mission-control-data`.
- No ruleset requires reviews.

## Decided

- Roles (EX-0014 D20): the owners are the Owner and Bob; Alena is a member;
  visitors never become members.
- Restricted repositories (EX-0014 D23): `finance` and `infra` stay public, so
  Alena reads them, but she has no Write; Team `finance` writes `finance`.

## Next

- Required pull requests and CI, CODEOWNERS and, once the review automations
  run, one required approval on every public repository: EX-0014 task
  `task-2026-10-18-002`.

## Guardrails

- No tokens, SSH keys or OAuth session data belong in this repository.
- Record access as rules and audit notes, not as secrets.
- Make real changes in the GitHub Organization only after explicit
  confirmation.
