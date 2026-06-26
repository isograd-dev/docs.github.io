# Prompt — Mettre à jour la documentation `ai/`

> **Note interne** — dossier `_internal/` (préfixe `_`), exclu du site Jekyll publié.
> Copier-coller le bloc ci-dessous dans Claude Code (ouvert sur `isograd_app`)
> pour mettre à jour un ou plusieurs chapitres du manuel.
>
> Remplacer `<CHAPITRE>` par le chapitre visé (ex. `question-module/domains`,
> `candidates`, `sessions`) — ou « tous les chapitres » pour une passe complète.

---

```
Mets à jour la documentation utilisateur du chapitre <CHAPITRE>.

CONTEXTE — deux repos liés :
- App + tests : /Users/marc/Documents/GitHub/isograd_app
- Docs (Jekyll/GitHub Pages, publié sur docs.isograd.com) :
  /Users/marc/Documents/GitHub/docs.github.io

La doc d'un chapitre se compose de :
- la PROSE  : docs.github.io/ai/<lang>/<chapitre>/index.md   (lang = fr et en)
- les IMAGES: docs.github.io/ai/<lang>/<chapitre>/img/NN-*.png + _manifest.json
- la SOURCE des images : un spec Playwright de capture
  isograd_app/tests/specs/ui/.../<chapitre>.manual.spec.mjs (projet
  Playwright `ui-manual-screenshots`).

La prose est rédigée par TOI en analysant le spec de capture, le scénario
fonctionnel correspondant (tests/scenarios/*.md), le code applicatif
(PHP/JS) de la page, et les captures produites. Le `_manifest.json` de
chaque chapitre est le pont entre spec et prose : il liste chaque image
(nom, caption, kind, selector/url). Garde prose, images et manifest
synchronisés.

PROCÉDURE :
1. Lis le spec de capture du chapitre et le `_manifest.json` existant.
   Lis le scénario fonctionnel lié dans tests/scenarios/ et le code de la
   page concernée pour comprendre le comportement réel (ne devine pas).
2. Détermine ce qui a changé dans l'UI / le comportement depuis la dernière
   génération. Si la page a évolué, METS À JOUR LE SPEC DE CAPTURE
   (`*.manual.spec.mjs`) en conséquence : nouvelles captures, captures
   obsolètes retirées, sélecteurs/étapes ajustés.
   - Respecte CLAUDE.md d'isograd_app : sélecteurs stables (#id / data-testid,
     JAMAIS de texte visible), timeouts via la constante T, URLs via
     APP_BASE_URL, nettoyage de TOUTE donnée créée, import de `test` depuis
     fixtures/admin-test.mjs, mode 'serial'.
   - Garde des noms de fichiers de capture stables (NN-slug.png) pour
     écraser en place.
3. Régénère les captures du chapitre, pour les DEUX langues :
     cd /Users/marc/Documents/GitHub/isograd_app/tests
     MANUAL_LANG=fr npx playwright test --project=ui-manual-screenshots <chemin-du-spec>
     MANUAL_LANG=en npx playwright test --project=ui-manual-screenshots <chemin-du-spec>
   (Prérequis : token admin frais dans tests/.env.)
4. Mets à jour la PROSE `index.md` en fr ET en en :
   - conserve le front-matter `layout:` existant (question-manual ou
     admin-manual) ;
   - chaque figure : `![caption](img/NN-nom.png)` avec la caption alignée
     sur celle du `_manifest.json` ;
   - prose précise, fondée sur le comportement réel observé, pas générique ;
   - fr et en doivent décrire le même contenu (traduction, pas divergence).
5. Vérifie la cohérence finale : chaque image du dossier img/ est référencée
   dans index.md et listée dans _manifest.json ; aucune référence morte.

CONTRAINTES :
- N'écris RIEN dans le site publié hors `ai/<lang>/...` (le dossier
  `_internal/` reste interne).
- Ne touche pas à l'envoi d'emails / SES ; emails de test en @mailinator.com.
- Si un changement applicatif est nécessaire pour rendre un test stable
  (ex. ajouter un #id), signale-le et propose la modif PHP/JS minimale.

LIVRABLE : un résumé listant, par langue et par chapitre : specs modifiés,
captures régénérées, sections de prose mises à jour.
```

---

## Aide-mémoire

- **Régénérer TOUTES les captures** (sans toucher la prose) :
  `cd isograd_app/tests && npx playwright test --project=ui-manual-screenshots`
  (défaut `MANUAL_LANG=fr` ; relancer avec `MANUAL_LANG=en` pour l'anglais).
- **Un seul chapitre** : ajouter le chemin du spec en argument.
- Voir `regenerate-screenshots.md` (même dossier) pour le détail des commandes.
- Mapping spec ↔ chapitre : le spec déclare `const CHAPTER = '...'`, qui est
  exactement le chemin `ai/<lang>/<CHAPTER>/`.
