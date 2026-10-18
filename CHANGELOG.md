# Changelog

## 20261018.2

### Changed

- The access record holds the rulesets of plan EX-0014 (task
  `task-2026-10-18-002`): every public repository except
  `mission-control-data` requires a pull request, its CI where it exists and a
  merge commit, and no ruleset has a bypass actor. It lists the ruleset and
  required checks per repository, the repositories without CI, the private
  Deployment Repo exception, the merge method that keeps the noreply author,
  the code owners, how to switch on one required approval with task
  `task-2026-10-18-011`, and the break-glass.

### Added

- `.github/CODEOWNERS` naming Bob, because only the owners write this
  repository.

## 20261018.1

### Added

- `access/matrix.md`: the public access matrix of plan EX-0014 (task
  `task-2026-10-18-001`). It lists every repository with the right of each
  Team and person and how GitHub enforces it, the new closed Teams `finance`
  (Bob, Write on `finance`) and `sales` (Alena and Bob, no grant until the
  sales modules exist), and that visitors get no membership or Team.

### Changed

- The access record lists the owners and the member, the base permission,
  the private Deployment Repo `machines`, the installed GitHub Apps and the
  decided roles and restricted access, and points to the matrix for Teams.

## 20261016.2

### Changed

- The access record lists `mission-control-data`, the Team grants on
  `mission-control` and `mission-control-data`, and their rulesets with the
  required checks.

## 2026-10-16

- Translated the repository to English and renamed the company to Lazurio
  Example Organization.
- Recorded the current GitHub state, verified 2026-10-16: the Organization and
  root repository ids and their verified binding, the repositories, the
  `workspace` Team grants, the "main" rulesets and the module port pool. The
  Lazurio for GitHub app is not installed yet.

## 2026-05-23

- Created the local root-level `infra/` repository scope for the company.
- Recorded the first infrastructure and access context: the GitHub
  Organization `LazurioExampleOrganization` exists.
- Published the private GitHub repository `LazurioExampleOrganization/infra`
  and recorded its SSH remote.
