# AgentMint infra — instrukce pro agenty

Tento scope vlastní infrastructure, access governance a deployment kontext
AgentMintu.

## Source of truth

Autoritativní záznamy v tomto repu jsou dokumenty o GitHub organizaci,
přístupech, repo governance, deployment topologii a provozních runbookech.

Root `README.md`, `MAP.md`, `ARCHITECTURE.md` a
`company/scripts/modules.manifest.json` popisují, že `infra/` existuje; detailní
kontext patří sem.

## Pravidla

- Nezapisuj secrets, tokeny, OAuth session data ani privátní klíče.
- Externí změny v GitHubu, cloudu, DNS nebo billing účtech dělej jen po
  výslovném pokynu.
- Pokud dokumentuješ stav externí služby, napiš datum ověření a zdroj
  poznatku.
- Access změny popisuj konkrétně: kdo, k čemu, proč a jak se bude auditovat.

## Aktuální minimum

Zatím je známý jen základní fakt: existuje GitHub organizace `LazurioExampleOrganization` pro
repozitáře AgentMintu. Další infrastruktura se doplní až podle skutečných
rozhodnutí.
