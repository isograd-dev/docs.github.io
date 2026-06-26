# Régénérer les captures d'écran du manuel

> **Note interne** — ce dossier `_internal/` commence par `_`, donc Jekyll
> l'exclut du site publié (`docs.isograd.com`). Visible uniquement dans le repo.

Les captures du manuel sont générées par les specs Playwright `*.manual.spec.mjs`
du repo `isograd_app`, regroupées dans le projet Playwright `ui-manual-screenshots`.
Elles écrivent les PNG dans `../docs/manual/<chapitre>/img/`.

## Tout régénérer en une commande

```bash
cd /Users/marc/Documents/GitHub/isograd_app/tests
npx playwright test --project=ui-manual-screenshots
```

## Un seul chapitre

```bash
cd /Users/marc/Documents/GitHub/isograd_app/tests
npx playwright test --project=ui-manual-screenshots specs/ui/preprod/
```

## Prérequis

- Un token admin frais dans `isograd_app/tests/.env` (login admin requis).
- Projet exclu de la CI — à lancer explicitement.
