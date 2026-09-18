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

## Module Questions : cibler un environnement CUSTOM

Le manuel du module Questions (`ai/<lang>/question-module/`) décrit l'interface
des **environnements custom** (plateformes client, `SystemVariables::isCustomEnvironment()`),
pas celle de la préproduction Isograd : pas de familles de sujets, fiche sujet à
3 onglets, pas de transfert en production, pas de vérification/calibration,
tests en mode client, etc.

Pour régénérer ces captures, `BASE_URL` et `ADMIN_LOGIN_URL` dans
`isograd_app/tests/.env` doivent pointer sur un **environnement custom** (login
d'un administrateur principal de ce client).

**Procédure utilisée (pas d'environnement custom dédié)** : l'utilisateur
bascule temporairement `test.isograd.com` en mode custom en modifiant **sur le
serveur** (pas dans le repo) le fichier `src/system/systemvariables.class.php` :

```php
public static function isCustomEnvironment(): bool
{
    return self::getEnvironment() == Environment::Custom || self::getEnvironment() == Environment::Test;
}
```

Garder `Environment::Test` comme STRID (ne pas changer `EnvVar`) : le login et
les listes d'administrateurs filtrent la base utilisateur sur ce STRID et
casseraient sinon. Une fois les captures faites, l'utilisateur rétablit la
version d'origine. Claude ne peut pas faire cette modification : la demander
avant de lancer les specs. Les specs `tests/specs/ui/preprod/*.manual.spec.mjs`
détectent `body[data-is_cus_env="1"]` pour adapter la création des données de démo.
Pour le chapitre « Éditeur de questions », désigner le sujet de démo de
l'environnement avec `MANUAL_SUBJECT_ID=<sbj_id>`.

Dernière régénération complète (fr + en) : 2026-09-18, sur `test.isograd.com`
temporairement configuré en environnement custom (`isCustomEnvironment()` patché
côté serveur). Limites de ces captures : l'admin utilisé est un compte root
Isograd, donc l'éditeur de questions montre en plus l'onglet « Description YML »
et le bouton « Editer questions liés », la fiche de test s'affiche en mode
avancé (privilège AdvancedTestFormRead) au lieu du mode client, et les données
(types de réponse, sujets, familles) sont celles de la base de test. Pour des
captures fidèles à un client, relancer avec un administrateur principal sans
privilèges root ni AdvancedTestFormRead.
