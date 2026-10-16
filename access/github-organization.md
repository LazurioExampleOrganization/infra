# GitHub Organization LazurioExampleOrganization

First recorded: 2026-05-23

## State

Verified 2026-10-16, updated after the Mission Control repositories were set
up. Source: the GitHub REST API (Organization, Team, repositories and
rulesets) and the root `lazurio.organization.json`, both read on 2026-10-16.

- Organization: `LazurioExampleOrganization` (id 325048785)
- URL: `https://github.com/LazurioExampleOrganization`
- Plan: Free. The repositories are public.
- Display name in Lazurio: "Lazurio Example Organization"
- Root repository:
  `git@github.com:LazurioExampleOrganization/LazurioExampleOrganization_GEN3.git`
  (id 1421349619). Its Lazurio manifest binds the Organization and the root
  repository by these ids; the binding state is verified.
- Infra repository: `git@github.com:LazurioExampleOrganization/infra.git`
- Lazurio for GitHub app: not installed yet. The Owner installs it.

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

## Teams

- Team `workspace` (closed, id 20129625) has Write on `knowledgebase`,
  `research`, `experiments`, `playbooks`, `content`, `automations`,
  `design-system`, `mission-control` and `mission-control-data`.
- `finance` and `infra` are declared restricted and get no Team grant.

## Rulesets

- A ruleset named "main" applies to the default branch of every repository
  (`v3` for `mission-control-data`).
- Each ruleset blocks deletion and force push.
- Required status checks: "Organization check" in the root repository,
  "check" in `knowledgebase` and `design-system`, "bun run test
  (ubuntu-latest)" and "bun run test (windows-latest)" in `mission-control`,
  and "validate" in `mission-control-data`.
- No ruleset requires reviews.

## Not decided yet

- roles in the GitHub Organization
- who gets access to the restricted repositories

## Guardrails

- No tokens, SSH keys or OAuth session data belong in this repository.
- Record access as rules and audit notes, not as secrets.
- Make real changes in the GitHub Organization only after explicit
  confirmation.
