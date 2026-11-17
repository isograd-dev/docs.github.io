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

- Deux tokens admin frais dans `isograd_app/tests/.env` :
  - `ADMIN_LOGIN_URL` — manuel administrateur (tous les chapitres hors module
    Questions et module de correction) ;
  - `ADMIN_PEDAGOGY_LOGIN_URL` — module Questions et module de correction,
    capturés sur l'**environnement pedagogy** (voir ci-dessous).
- Projet exclu de la CI — à lancer explicitement.

## Module Questions et module de correction : environnement pedagogy

Toutes les captures du **module Questions** (`tests/specs/ui/preprod/*.manual.spec.mjs`)
et du **module de correction** (`tests/specs/ui/clientadmin/grading/*.manual.spec.mjs`)
sont réalisées sur l'**environnement pedagogy**, avec le login
`ADMIN_PEDAGOGY_LOGIN_URL`. Les autres chapitres restent sur `ADMIN_LOGIN_URL`.
La commande unique ci-dessus régénère toujours l'ensemble : chaque spec choisit
son environnement.

Mécanisme : ces specs importent `test` depuis `tests/fixtures/pedagogy-admin-test.mjs`
(et non `fixtures/admin-test.mjs`). Ce module remplace `ADMIN_LOGIN_URL` par
`ADMIN_PEDAGOGY_LOGIN_URL` dans le worker avant le chargement de
`scripts/constants.mjs` : `APP_BASE_URL`, `goToPage()` et `ensureAdminLoggedIn()`
visent alors pedagogy. Pour une nouvelle spec de captures de ces deux modules,
cet import doit être le **premier import** du fichier (une vérification fait
échouer la spec avec un message explicite sinon). Si `ADMIN_PEDAGOGY_LOGIN_URL`
est absent, la spec échoue immédiatement.

Le manuel du module Questions (`ai/<lang>/question-module/`) décrit l'interface
des **environnements custom** (plateformes client, `SystemVariables::isCustomEnvironment()`),
pas celle de la préproduction Isograd : pas de familles de sujets, fiche sujet à
3 onglets, pas de transfert en production, pas de vérification/calibration,
tests en mode client, etc. Les specs détectent `body[data-is_cus_env="1"]` pour
adapter la création des données de démo. L'usage de pedagogy remplace l'ancienne
procédure (bascule temporaire de `test.isograd.com` en mode custom par un patch
de `isCustomEnvironment()` sur le serveur).

Pour des captures fidèles à un client, le compte de `ADMIN_PEDAGOGY_LOGIN_URL`
doit être un administrateur principal sans privilèges root ni
AdvancedTestFormRead : un compte root ajoute l'onglet « Description YML » et le
bouton « Editer questions liés » dans l'éditeur, et affiche la fiche de test en
mode avancé. Pour le chapitre « Éditeur de questions », désigner le sujet de
démo de l'environnement pedagogy avec `MANUAL_SUBJECT_ID=<sbj_id>`.

Dernière régénération du manuel administrateur (fr + en) : 2026-11-17 sur `test.isograd.com` (10 chapitres ; nouvelles captures : fenêtre et aperçu de l'import de candidats, fenêtre de création d'un groupe, candidats d'une session en cours, onglet API du compte). Module Questions et module de correction : régénérés (fr + en) le 2026-11-17 sur `pedagogy.isograd.com`, avec `MANUAL_SUBJECT_ID=529` (sujet DEMO) pour l'éditeur de questions. Reste à refaire : `question-editor` 11 (test de saisie, type de réponse absent de pedagogy), encore issue de la génération d'octobre. Module Questions : dernière régénération complète (fr + en) 2026-10-09, sur `test.isograd.com`
temporairement configuré en environnement custom, avec un compte root Isograd
(d'où l'onglet YML, le mode avancé des tests et les données de la base de test
visibles sur ces captures) — pas encore régénéré sur pedagogy.
