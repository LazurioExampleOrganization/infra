# GitHub organizace LazurioExampleOrganization

Datum záznamu: 2026-05-23

## Stav

AgentMint má založenou GitHub organizaci:

- Organizace: `AgentMint`
- URL: `https://github.com/LazurioExampleOrganization`
- Super-repo workspace: `git@github.com:LazurioExampleOrganization/LazurioExampleOrganization_GEN3.git`
- Infra repo: `git@github.com:LazurioExampleOrganization/infra.git`

## Zatím nerozhodnuto

- branch protection pravidla pro `main`
- týmy a role v GitHub organizaci
- kdo bude mít přístup k restricted repozitářům
- branch protection pro `LazurioExampleOrganization/infra`

## Guardrails

- Do tohoto repa nepatří žádné tokeny, SSH klíče ani OAuth session data.
- Přístupy se mají zapisovat jako pravidla a auditní poznámky, ne jako secrets.
- Reálné změny v GitHub organizaci dělej až po explicitním potvrzení.
