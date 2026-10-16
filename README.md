# Lazurio Example Organization infra

`infra/` is the root-level nested Git repository for the infrastructure,
access governance and deployment context of Lazurio Example Organization.

It holds the verified state of the GitHub Organization
`LazurioExampleOrganization`. The full access record is in
[`access/github-organization.md`](access/github-organization.md).

## Current state

Verified 2026-10-16.

- GitHub Organization: `LazurioExampleOrganization` (id 325048785), Free plan,
  public repositories. Display name in Lazurio: "Lazurio Example
  Organization".
- Root repository:
  `git@github.com:LazurioExampleOrganization/LazurioExampleOrganization_GEN3.git`
  (id 1421349619). Its Lazurio manifest binds the Organization and the root
  repository by these ids; the binding state is verified.
- Infra repository: `git@github.com:LazurioExampleOrganization/infra.git`. It
  is declared restricted and gets no Team grant.
- Repositories, the `workspace` Team and the rulesets: see the
  [access record](access/github-organization.md).
- Lazurio for GitHub app: not installed yet. The Owner installs it.
- Microsoft 365 Business Premium trial: provisioned with one license assigned
  to Sam Taylor, a mailbox and a SharePoint fixture. Post-support
  billing displays Disabled / recurring On despite Microsoft's no-charge
  assurance. Sam can read the SharePoint fixture; Outlook still fails. See the
  [tenant record](access/microsoft-365.md).
- Entra company app: single-tenant public client with nine delegated Graph
  permissions granted by the administrator; see the
  [verified app configuration](access/microsoft-365.md#entra-company-app).
- Module port pool of the Organization: 25300–25399.
- Production cloud, domain and deployment pipeline: not set up yet.

## What belongs here

- the GitHub Organization, Teams, repository governance and branch protection
  rules
- the access model for people, agents and future workspace administrators
- deployment topology and operational runbooks
- audit notes on the infrastructure

## What does not belong here

- secrets, tokens, OAuth session data or private keys
- customer data
- financial exports and sensitive payment provider statements
- business strategy, which belongs in Mission Control or the knowledgebase

## Source of truth

This repository scope is the source of truth for infrastructure and access
governance. The root manifest `modules.manifest.json` holds only the slot and
the metadata that `infra/` exists as a separate repository.
