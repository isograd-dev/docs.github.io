---
layout: question-manual
---

# Aides visuelles

Une **aide visuelle** est un **fichier d'illustration** (image, PDF, document Office, etc.) que l'on peut associer à une ou plusieurs questions pour fournir au candidat le matériel sur lequel répondre : un tableau Excel à analyser, un schéma à interpréter, un extrait de code à débugger, un texte à lire.

Les aides visuelles sont gérées de manière **centralisée** sur la plateforme : on les déclare une fois, on les téléverse, puis on les référence dans les questions par leur nom. Ce design permet :

- De **réutiliser** la même image dans plusieurs questions sans la dupliquer.
- De **mettre à jour** un fichier en un seul endroit, avec propagation immédiate à toutes les questions qui l'utilisent.
- De **garantir la cohérence** linguistique : une aide visuelle est rattachée à une langue, ce qui assure que la version française d'une question affiche le tableau en français et la version anglaise le tableau en anglais.

Accédez à la page via le menu **Aides visuelles**.

![Page "Gestion des aides visuelles"](img/01-liste-aides.png)

Le tableau liste toutes les aides visuelles, avec leur **sujet**, leur **langue**, leur **type**, leur **nom** et un aperçu de leur **contenu** lorsqu'il s'agit d'une image.


## Formats de fichier acceptés {#formats-acceptes}

La plateforme accepte les extensions suivantes :

| Catégorie | Extensions |
|---|---|
| Images | `jpg`, `jpeg`, `png`, `gif`, `bmp`, `svg` |
| Documents Office | `doc`, `docx`, `xlsx` |
| PDF | `pdf` |
| Données | `yml`, `pbix` (Power BI) |
| Archive | `zip` |

Les fichiers dont l'extension n'est pas dans cette liste sont **rejetés côté navigateur**, avant même l'envoi au serveur.

> 💡 **Taille** — Le fichier est envoyé directement au service de stockage : il n'y a pas de limite de taille stricte. Pour les fichiers volumineux (Power BI, gros PDF), assurez-vous néanmoins que le candidat pourra le télécharger dans des délais acceptables — un test surveillé n'attendra pas une connexion lente.


## Créer une aide visuelle {#creer-une-aide}

La création se fait en **deux étapes** : déclaration de la langue et du sujet, puis nommage de l'aide et téléversement du fichier.

### Étape 1 — Déclaration

1. Depuis la page **Gestion des aides visuelles**, cliquez sur **Ajouter une aide visuelle** dans la barre d'actions.

    ![Fenêtre de création d'une aide visuelle](img/02-modal-creation.png)

2. Dans la fenêtre, choisissez :

    - La **langue** de l'aide visuelle, parmi les langues de votre compte. Une aide visuelle est **mono-langue** : si vous avez besoin de la même illustration dans plusieurs langues, créez une aide visuelle par langue.
    - Le **sujet** auquel cette aide visuelle est rattachée. Permet de filtrer la liste et de proposer l'aide dans l'éditeur des questions de ce sujet.

3. Cliquez sur **Enregistrer**. La plateforme crée un enregistrement et vous redirige sur sa fiche d'édition.

### Étape 2 — Métadonnées et téléversement

Sur la fiche d'édition, l'écran est divisé en deux colonnes :

![Fiche d'édition d'une aide visuelle](img/03-fiche-aide.png)

**Colonne de gauche — Métadonnées** :

- L'**identifiant** de l'aide visuelle, affiché en haut.
- **Sujet** — en lecture seule (défini à la création).
- **Langue** — en lecture seule (définie à la création).
- **Type** — la façon dont l'aide est présentée au candidat : **Image** (dans le texte), **Image avec loupe** (s'ouvre au clic), **Document de référence** (document intégré ou proposé sous forme de lien), **Clavier** (image de clavier, non rattachée à un sujet).
- **Nom** — libellé interne. **Attention** : le nom est **simplifié** à l'enregistrement (espaces remplacés par des tirets, accents retirés, etc.) ; il devient aussi le **nom de fichier** stocké, ce qui le rend visible des candidats s'ils inspectent la page. Restez sobre.
- Une ligne d'information indique **où l'aide visuelle est utilisée** : *« Cette aide visuelle n'est utilisée dans aucune question. »* si vide, ou la liste des identifiants de questions qui la référencent.

> ⚠️ **Sujet et langue verrouillés** — Si vous vous êtes trompé de sujet ou de langue à la création, supprimez l'aide et recréez-la — vous ne pouvez plus les modifier ici.

**Colonne de droite — Contenu** :

Une zone de dépôt indique *« Déposez ici l'image ou le document PDF »* / *« Cliquez ici pour sélectionner un fichier sur votre ordinateur »*.

- **Glissez-déposez** le fichier dans la zone, ou
- **Cliquez** sur la zone pour ouvrir le sélecteur de fichier de votre système.

Le **nom** et le **type** doivent être renseignés avant le téléversement. Une fois le fichier choisi, l'envoi démarre automatiquement. Si l'extension est valide, l'aperçu apparaît dans la zone :

- Pour une **image**, vous voyez la vignette.
- Pour un **PDF**, un aperçu intégré.
- Pour les autres formats (Office, archive…), seul un lien de téléchargement est affiché.

Un bouton **Supprimer le contenu** sous l'aperçu retire le fichier tout en conservant l'enregistrement.

> 💡 **Remplacer un fichier** — Déposez simplement un nouveau fichier dans la zone : il remplace l'ancien. La nouvelle version est immédiatement disponible pour toutes les questions qui référencent cette aide.


## Utiliser une aide visuelle dans une question {#utiliser-dans-une-question}

Côté éditeur de questions, la zone de **recherche d'aides visuelles** à droite liste les aides du sujet et de la langue de la question : saisissez au moins trois caractères du nom, puis cliquez sur l'aide pour insérer sa **balise de référence** dans l'énoncé ou dans une réponse. Le rendu côté candidat remplace la balise par l'image ou le document.

Une aide visuelle peut être référencée par :

- L'**énoncé** de la question.
- Les **propositions de réponse**.
- Les **paramètres spécifiques** de la question, pour certains types interactifs.

> 💡 **Vérifier l'utilisation** — La fiche d'une aide visuelle indique en bas de la colonne de gauche **les questions qui l'utilisent**. Ouvrez la page **Questions** et recherchez ces identifiants pour les explorer.


## Filtres {#filtres}

Le panneau **Filtres** propose :

- **Rechercher** — texte libre sur le nom.
- **Sujet** — sélection multiple sur le sujet de rattachement.
- **Langue** — langue de l'aide.
- **Type** — Image, Image avec loupe, Document de référence, Clavier.

Le tri est disponible sur chaque colonne.


## Supprimer une aide visuelle {#supprimer-une-aide}

1. Sur la ligne de l'aide, cliquez sur l'icône **Supprimer**.
2. Confirmez sur la page qui s'ouvre.

> ⚠️ **Aide référencée par des questions** — Si l'aide visuelle est référencée dans le texte, les réponses ou les paramètres spécifiques d'**au moins une question**, la suppression est **refusée** avec le message « Impossible de supprimer une aide visuelle utilisée dans des questions ». Avant suppression :
>
> 1. Identifiez les questions qui utilisent l'aide (listées sur sa fiche).
> 2. Modifiez ces questions pour pointer vers une autre aide ou retirer la référence.
> 3. Réessayez la suppression.


## Bonnes pratiques {#bonnes-pratiques}

- **Nommez clairement** vos aides visuelles : `tableau-ventes-2024-fr` plutôt que `image1`. Le nom de fichier devient public dans la page rendue — un nom évocateur évite les confusions et facilite le débogage.
- **Compressez vos images** avant téléversement : une page candidat qui charge 10 images de 5 Mo chacune est inutilisable sur connexion mobile. Cible : 200 Ko / image en JPG.
- **Limitez les PDF** au strict nécessaire. Un PDF complexe consomme beaucoup côté navigateur et peut rendre le test inaccessible aux candidats avec un navigateur ancien.
- **Une aide visuelle par langue** : ne mélangez pas les langues dans une même image. Une capture d'écran d'Excel en anglais ne convient pas pour la version française du test.
