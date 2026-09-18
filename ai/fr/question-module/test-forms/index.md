---
layout: question-manual
---

# Tests

Un **test** est l'assemblage final qui devient passable par un candidat. C'est le point de jonction où vous prenez une **sélection de questions** de votre base, choisissez l'**ordre des questions**, fixez des **paramètres** (durée, navigation, feedback, etc.), et obtenez un livrable que les administrateurs de votre compte peuvent inscrire à des candidats.

Chaque test inscrit à un candidat sur la plateforme est défini par l'un de ces tests.

Accédez à la page via le menu **Tests**. Il est affiché aux administrateurs disposant du privilège de lecture des tests.

![Page de gestion des tests](img/01-liste-formulaires.png)

Le tableau (titre **Gestion des tests**) liste tous les tests, avec leur **identifiant**, **nom**, **sujet**, **langue**, **type** et **algorithme**. Lorsqu'une période est renseignée dans les filtres, une colonne supplémentaire affiche le **nombre de passages** sur cette période.


## Concepts {#concepts}

### Ordre des questions

Un test fixe soit la liste exacte des questions, soit les tire au hasard au début de chaque session. C'est le paramètre **Ordre des questions** du test :

- **Ordonné** — vous choisissez les questions une à une ; chaque candidat reçoit les mêmes questions dans le même ordre.
- **Aléatoire** — vous fixez le **nombre de questions** et le vivier dans lequel tirer ; chaque candidat reçoit un ordre différent.

### Seules les questions en Production sont posées

Quel que soit l'ordre, un test ne peut poser que des questions au statut **Production** : le sélecteur de questions ne liste que celles-là, et le tirage aléatoire ignore les autres. Passez vos questions en Production avant de construire le test (voir l'[Éditeur de questions](/ai/fr/question-module/question-editor/#actions-finales)).


## Créer un test {#creer-un-formulaire}

La création passe par une fenêtre minimale, suivie de la page d'édition.

1. Depuis la page **Gestion des tests**, cliquez sur **Créer un test** dans la barre d'actions.

    ![Fenêtre de création](img/02-modal-creation.png)

2. Choisissez la **langue** présentée au candidat.

3. Cliquez sur **Enregistrer**. La plateforme crée le test et vous amène sur sa page d'édition.


## Onglets de la page d'édition {#onglets-mode-avance}

La page d'édition propose quatre onglets. Un message d'aide en haut rappelle que le test est construit à partir des questions de **votre** base.

![Onglets de la page d'édition d'un test](img/03-onglets-avance.png)

| Onglet | Contenu |
|---|---|
| **Caractéristiques générales** | Tout ce qui définit le test : statut, nom et description, ordre des questions, sélection des questions, options côté candidat. |
| **Gestion du temps** | La durée allouée. |
| **Messages de début et de fin de test & prompt d'analyse** | Les textes d'introduction et de fin affichés au candidat, et les consignes pour l'analyse IA des résultats. |
| **Statistiques** | Graphique d'utilisation sur les derniers mois et, dès qu'assez de résultats existent, un indicateur de fiabilité du test. |

### Onglet « Caractéristiques générales »

- **Créé par** — l'administrateur qui a créé le test.
- **Actif** (Oui / Non) — un test inactif ne peut plus être inscrit à de nouveaux candidats mais reste disponible pour les résultats déjà enregistrés. C'est ainsi qu'on retire un test.
- **Nom et description du test** — un bloc par langue de votre compte. La description est affichée aux administrateurs lorsqu'ils inscrivent le test.
- **Nécessite une surveillance** — si le test doit être passé sous surveillance à distance.
- **A une accessibilité augmentée** — variante de l'interface destinée aux candidats malvoyants.
- **Ordre des questions** — *Ordonné* ou *Aléatoire* (voir [Concepts](#concepts)).
- **Nombre de questions** — pour un test aléatoire, combien de questions chaque candidat reçoit.
- **Sujet**, **Jeux de questions**, **Domaines** — pour un test aléatoire, le vivier dans lequel tirer : les questions des jeux sélectionnés, et éventuellement un nombre de questions par domaine (noté `identifiant du domaine:nombre`, séparés par des espaces).
- **Sélection de questions** — la liste des questions du test. Cliquez sur **Choisir** pour ouvrir le sélecteur de questions : filtrez par **sujet**, **domaine**, **difficulté**, **jeu de questions** ou texte libre, cochez les questions et validez. Pour un test ordonné, glissez les lignes pour fixer l'ordre. Jusqu'à 1 000 questions peuvent être sélectionnées.
- **Type de résultat** — comment le score est calculé et présenté (par exemple nombre de bonnes réponses ou pourcentage).
- **Navigation entre les questions** — permet au candidat d'aller et venir entre les questions au lieu d'y répondre dans l'ordre.
- **Afficher la liste des questions** — affiche la liste des questions au candidat pendant le test.
- **Fournir la bonne réponse après chaque question** — mode feedback immédiat.
- **Afficher le bouton « Abandonner la question »** — permet au candidat de passer une question.
- **Afficher le bouton « Tutoriel » en bas de chaque question** — donne accès au tutoriel rédigé par l'auteur.
- **Afficher le bouton permettant de lire la question** — synthèse vocale de l'énoncé.

> 💡 **Durée suggérée** — Une fois les questions choisies, l'onglet **Gestion du temps** affiche une durée suggérée calculée à partir du temps alloué à chaque question sélectionnée.

### Onglet « Gestion du temps »

- **Durée du test** — en minutes. Laissez vide pour ne pas imposer de limite de temps.

### Onglet « Messages de début et de fin de test & prompt d'analyse »

- **Message de début** — message affiché avant la première question.
- **Message de fin** — message affiché à la fin du test. Un texte par défaut est proposé à la création du test.
- **Texte de la boîte de dialogue du choix de version** — optionnel, pour les tests qui laissent le candidat choisir entre plusieurs versions.
- **Consignes pour l'analyse IA des résultats** — optionnel, consignes utilisées lorsqu'un administrateur demande une analyse IA des résultats d'un candidat.

### Boutons d'en-tête

- **Enregistrer** — sauvegarde l'ensemble de la fiche.
- **Enregistrer & essayer votre test** — enregistre, puis lance le test pour vous-même tel qu'un candidat le verrait.
- **Exporter les commentaires** — télécharge les commentaires laissés par les candidats sur les questions de ce test.
- **Analyse IA du test** — demande à l'IA une revue de la conception du test (couverture, équilibre, formulation).


## Modifier un test {#modifier-un-formulaire}

1. Sur la ligne du test, cliquez sur l'icône **Modifier** (crayon).
2. Naviguez entre les onglets et ajustez les valeurs souhaitées.
3. Cliquez sur **Enregistrer** en haut à droite.

> ⚠️ **Tests en cours d'utilisation** — Modifier un test **déjà inscrit** à des candidats peut affecter leur expérience. Pour des changements profonds (liste des questions, ordre), préférez créer un **nouveau test** ou **dupliquer** l'existant, et passez l'ancien en inactif.


## Dupliquer un test {#dupliquer-un-formulaire}

La duplication est l'outil le plus rapide pour créer une variante d'un test existant (autre langue, ajustement local, version courte).

1. Sur la ligne du test à dupliquer, cliquez sur l'icône **Dupliquer**.
2. La plateforme crée une copie et vous amène sur sa page d'édition.
3. **Renommez** la copie pour éviter la confusion : elle porte le même nom que l'original.

> 💡 **La duplication conserve** — la liste des questions, l'ordre des questions, les paramètres, les descriptions, les messages de début et de fin. Les questions elles-mêmes sont partagées, pas copiées.


## Supprimer un test {#supprimer-un-formulaire}

1. Sur la ligne du test, cliquez sur l'icône **Supprimer**.
2. Confirmez sur la page qui s'ouvre.

> ⚠️ **Préférer la désactivation** — Supprimer un test retire définitivement sa définition. Pour un test déjà passé, passez plutôt **Actif** à *Non* dans l'onglet Caractéristiques générales : le test ne peut plus être inscrit mais les résultats historiques restent consultables.


## Filtres {#filtres}

Le panneau **Filtres** propose :

- **Rechercher** — texte libre sur le nom ou l'identifiant.
- **Langue** — par langue du test.
- **Sujet** — par sujet associé.
- **Inclure les tests inactifs** — commutateur, désactivé par défaut.
- **Afficher le nombre de passages du / au** — une période ; lorsqu'elle est renseignée, le tableau affiche le nombre de passages de chaque test sur cette période.

Le tri par colonne est disponible en cliquant sur les en-têtes.


## Exporter la liste {#exporter-la-liste}

Le bouton **Exporter vers Excel** de la barre d'actions génère un fichier `.xlsx` listant tous les tests actuellement filtrés. Précieux pour les revues périodiques du catalogue de tests.
