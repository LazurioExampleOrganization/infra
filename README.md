# AgentMint Infra

`infra/` je root-level nested Git repo pro infrastrukturu, access governance a
deployment kontext AgentMintu.

Zatím tady držíme jen první ověřený stav: AgentMint má založenou GitHub
organizaci `LazurioExampleOrganization`.

## Aktuální stav

- GitHub organizace: `AgentMint`
- Super-repo: `git@github.com:LazurioExampleOrganization/LazurioExampleOrganization_GEN3.git`
- Infra repo: `git@github.com:LazurioExampleOrganization/infra.git`
- Produkční cloud, doména a deployment pipeline: zatím nenastaveno

## Co sem patří

- GitHub organizace, týmy, repo governance a branch protection pravidla
- access model pro lidi, agenty a budoucí správce workspace
- deployment topologie a provozní runbooky
- auditní poznámky k infrastruktuře

## Co sem nepatří

- secrets, tokeny, OAuth session data ani privátní klíče
- zákaznická data
- finanční exporty a citlivé payment provider výpisy
- business strategie, která patří do Mission Control nebo knowledgebase

## Source of truth

Tento repo scope je source of truth pro infrastructure a access governance.
Root workspace manifest `company/scripts/modules.manifest.json` drží pouze
slot a metadata o tom, že `infra/` existuje jako samostatné repo.
