# Access matrix

One table says who reaches which repository of Lazurio Example Organization
with which right. GitHub enforces every right in it: repository grants of
Teams, the Organization owner role and the public visibility of the
repositories. This document holds no right of its own; it records GitHub and
must match it. There is no second roster.

Verified 2026-10-18. Source: the GitHub REST API, read with `gh` as an
Organization owner: Organization members and roles, every Team with its
members and repository grants, and the collaborators of every repository.
Decided by plan EX-0014 (task `task-2026-10-18-001`, milestone L1, decisions
D20, D23, D30, D33 and D36).

## How a right is enforced

| Right | Enforced by |
|---|---|
| Admin | The Organization owner role. Every owner is Admin on every repository. The owners are the Owner and Bob. |
| Write, Read in a Team column | The Team's grant on the repository. |
| Write, Read in a person's column | The strongest of the person's owner role and the grants of their Teams. Alena's Write comes only from Team `workspace`. |
| Read (public) | The repository is public, so anyone reads it, with or without a GitHub account. No grant is involved, and public read never gives Write. |
| none | A private repository without a grant. |
| – | The Team has no grant on the repository. |

The Organization's base permission is `none`: membership alone adds nothing
to public read.

Restricted means read without Write (D23): the repository stays public and
Alena reads it, but no Team she belongs to has Write on it. Bob writes
everything as an owner.

## Matrix

| Repository | What it is | `workspace` | `finance` | `sales` | `lazurio-bob` | `lazurio-alena` | Bob | Alena | The Owner | Visitors |
|---|---|---|---|---|---|---|---|---|---|---|
| `LazurioExampleOrganization_GEN3` | Organization root | Read | – | – | – | – | Admin | Read | Admin | Read (public) |
| `knowledgebase` | workspace module | Write | – | – | – | – | Admin | Write | Admin | Read (public) |
| `research` | workspace module | Write | – | – | – | – | Admin | Write | Admin | Read (public) |
| `experiments` | workspace module | Write | – | – | – | – | Admin | Write | Admin | Read (public) |
| `playbooks` | workspace module | Write | – | – | – | – | Admin | Write | Admin | Read (public) |
| `content` | workspace module | Write | – | – | – | – | Admin | Write | Admin | Read (public) |
| `automations` | workspace module | Write | – | – | – | – | Admin | Write | Admin | Read (public) |
| `finance` | workspace module, restricted | – | Write | – | – | – | Admin | Read (public) | Admin | Read (public) |
| `design-system` | root application | Write | – | – | – | – | Admin | Write | Admin | Read (public) |
| `mission-control` | root application (Mission Control v3) | Write | – | – | – | – | Admin | Write | Admin | Read (public) |
| `mission-control-data` | data of Mission Control (branch `v3`) | Write | – | – | – | – | Admin | Write | Admin | Read (public) |
| `infra` | access documentation, restricted | – | – | – | – | – | Admin | Read (public) | Admin | Read (public) |
| `machines` | Deployment Repo, private | – | – | – | – | – | Admin | none | Admin | none |

The private Deployment Repo has one more account: the Lazurio maintainers'
agent account, an outside collaborator with Admin on that repository only.
It is not a member of the Organization and has no right on any other
repository.

Rows name today's repositories. Root decision 0204 (addendum of 2026-10-17)
plans to rename the access documentation `infra` to `infra-example` and the
private Deployment Repo `machines` to `infra`. The rights belong to the role
of the repository, so after the rename only the names in the first column
change.

## People

Members of the GitHub Organization are only the Lazurio maintainers and the
two fictional test accounts (D20).

| Account | Organization role | Teams |
|---|---|---|
| The Owner, a Lazurio maintainer's account | Owner | `workspace` |
| `lazurio-bob` (Bob, fictional test account) | Owner | `finance`, `sales`, `lazurio-bob` |
| `lazurio-alena` (Alena, fictional test account) | Member | `workspace`, `sales`, `lazurio-alena` |

GitHub makes an Organization owner a maintainer of every Team the owner
joins, so the Owner is a maintainer of `workspace` and Bob of his Teams.
Alena is an ordinary Team member.

## Teams

All Teams are closed (visible to members of the Organization) and have no
parent Team.

| Team | Id | Members | Repository grants | Purpose |
|---|---|---|---|---|
| `workspace` | 20129625 | the Owner, Alena | Write on the workspace modules except `finance` and on the root applications; Read on the Organization root | The company's working Team; the Team Environment `team-01` admits it. |
| `finance` | 20175541 | Bob | Write on `finance` | Writes the restricted finance module. |
| `sales` | 20175543 | Alena, Bob | none yet | Shares the sales modules with `workspace` to show that a module can belong to several Teams (D30). |
| `lazurio-bob` | 20162541 | Bob | none | Admits only Bob's Work Environment `lazurio-bob` (D36). |
| `lazurio-alena` | 20175101 | Alena | none | Admits only Alena's Work Environment `lazurio-alena` (D36). |

The per-person Teams `lazurio-bob` and `lazurio-alena` gate entry to a Work
Environment and grant nothing on a repository. Team `sales` gets Write on the
sales modules when they are created in milestone L3, the first being `deals`
(task `task-2026-10-18-009`); until then it has no grant.

## Visitors

Visitors get no account in the GitHub Organization, no Team and no grant
(D20, D33). They enter `try-01`, the Organization's one public Environment,
with any signed-in Lazurio account through its link. Like anyone on the
internet they read the public repositories, and they never reach the private
Deployment Repo.

## Who acts on GitHub in each Environment

- In a Work Environment GitHub acts as the person's own account: Bob in
  `lazurio-bob`, Alena in `lazurio-alena`. The person's column applies.
- In the Team Environment `team-01` GitHub acts as Lazurio for GitHub, the
  Organization's brokered identity. Its rights are the grants of Team
  `workspace` (root decision 0148), and a named person publishes what it
  prepares.
- In `try-01` the public content is read without a GitHub identity. A visitor
  may sign in to their own GitHub account there at their own risk; the
  Organization gives `try-01` no grant.

The full matrix per Environment kind (who enters, AI, the vault and
Integrations) follows in task `task-2026-10-18-006`.

## Modules still to come

Milestone L3 adds modules through the normal creation path; the module charter
(task `task-2026-10-18-007`) names their Teams. Each new module gets its row
here when it is created, and its grants are set on GitHub in the same step.
Already set by the plan:

- The sales modules, the first being `deals`, are shared by `workspace` and
  `sales` (D30).
- `finance` stays restricted, and `pricebook` will be restricted too: Alena
  reads them but cannot write them.

## Keeping the matrix true

GitHub decides; this file follows. A change of a Team or a grant updates this
file in the same step, and the access record
([github-organization.md](github-organization.md)) keeps the Organization,
its repositories and their rulesets. Read the state back with:

```sh
gh api orgs/LazurioExampleOrganization/teams --jq '.[].slug'
gh api orgs/LazurioExampleOrganization/teams/<team>/members --jq '.[].login'
gh api orgs/LazurioExampleOrganization/teams/<team>/repos --jq '.[] | [.name, .role_name]'
gh api 'repos/LazurioExampleOrganization/<repository>/collaborators?affiliation=all' --jq '.[] | [.login, .role_name]'
```
