# Lazurio Example Organization infra: instructions for agents

This scope owns the infrastructure, access governance and deployment context
of Lazurio Example Organization.

## Source of truth

The authoritative records in this repository are the documents about the
GitHub Organization, access, repository governance, deployment topology and
operational runbooks.

The root `README.md`, `MAP.md`, `ARCHITECTURE.md` and `modules.manifest.json`
describe that `infra/` exists; the detailed context belongs here.

## Rules

- Do not write secrets, tokens, OAuth session data or private keys.
- Make external changes in GitHub, the cloud, DNS or billing accounts only on
  explicit instruction.
- When you document the state of an external service, write the date of
  verification and the source of the finding.
- Describe access changes concretely: who, to what, why and how it will be
  audited.

## Current minimum

The GitHub Organization `LazurioExampleOrganization` holds the repositories of
Lazurio Example Organization. Its verified access state is recorded in
`access/github-organization.md`. Further infrastructure is added only as real
decisions are made.
