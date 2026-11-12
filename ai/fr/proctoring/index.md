---
layout: admin-manual
---

# Surveillance des tests

La **surveillance à distance** (« proctoring ») permet de garantir l'intégrité d'un test passé à distance, sans surveillant physique en présentiel. La plateforme propose plusieurs niveaux de surveillance — du plein écran obligatoire jusqu'à l'enregistrement vidéo et audio — et la revue *a posteriori* des incidents détectés.

Ce chapitre couvre trois pages complémentaires :

- **[Profils de surveillance](#profils-de-surveillance)** — configurez **comment** vos tests sont surveillés (quelles vérifications, quels enregistrements).
- **[Gestion des tests surveillés](#gestion-des-tests-surveilles)** — examinez **les passages** déjà effectués et validez ou invalidez chaque test à partir des éléments collectés.
- **[Surveillance en direct](#surveillance-en-direct)** — suivez **en temps réel** la caméra et l'écran des candidats d'une session de passage.

> 💡 **Disponibilité** — La surveillance à distance est une option du compte. Si vous ne voyez pas les pages décrites ici dans le menu, contactez votre interlocuteur Isograd pour activer la fonctionnalité.


## Profils de surveillance {#profils-de-surveillance}

Un **profil de surveillance** est un jeu de réglages qui détermine ce que la plateforme vérifie et enregistre pendant le test. Vous pouvez créer plusieurs profils (par exemple, *« Examen léger »* vs *« Certification stricte »*) pour appliquer le bon niveau de contrôle au bon contexte : le profil se choisit **lors de l'inscription** d'un candidat à un test, ou est **imposé par une [session de passage](/ai/fr/sessions/) surveillée en direct**.

Accédez à cette page via le menu **Surveillance → Profils de surveillance**.

![Page "Gestion des profils de surveillance"](img/01-page-profils.png)

La page liste vos profils existants. Si votre compte est neuf et n'a encore aucun profil défini, vous verrez simplement *« Vous n'avez pas encore créé de profil de surveillance. »*. Chaque ligne indique le **nom** du profil, un repère **Par défaut** pour le profil utilisé quand aucun n'est explicitement choisi, et son **Identifiant (API / LTI)**, à utiliser pour désigner le profil depuis une intégration. Un champ de recherche filtre la liste.

### Créer un profil de surveillance

La création se fait en **deux étapes** : nommer le profil, puis configurer ses options dans la fenêtre d'édition qui s'ouvre automatiquement.

#### Étape 1 — Nommer le profil

1. Cliquez sur **Ajouter un profil de surveillance** dans la barre d'actions.

    ![Fenêtre d'ajout d'un profil de surveillance](img/02-modal-profil-ajout.png)

2. Renseignez la **Description** du profil — c'est le libellé qui apparaîtra dans la liste et dans les fenêtres d'inscription aux tests. Choisissez un nom parlant comme « Certification stricte » ou « Examen interne léger ».

3. Cliquez sur **Enregistrer**. La plateforme crée le profil et ouvre aussitôt la fenêtre d'édition de ses options.

#### Étape 2 — Configurer les options de surveillance

Dans la fenêtre d'édition du profil, activez les **options de surveillance** souhaitées. Deux options principales :

| Option | Effet |
|---|---|
| **Empêcher le candidat d'ouvrir d'autres fenêtres ou onglets** | Le test doit être passé en plein écran, sans autre fenêtre ni onglet. Une sortie génère un incident. |
| **Utiliser la surveillance à distance et / ou un navigateur sécurisé** | Active la surveillance à distance et fait apparaître les options ci-dessous. |

Les options de la surveillance à distance n'apparaissent que lorsque la seconde option est activée :

| Option | Effet |
|---|---|
| **Demander un document d'identité** | Le candidat doit photographier sa pièce d'identité avant de démarrer. La photo est consultable a posteriori dans la revue. |
| **Effectuer un scan de la pièce** | Avant le test, le candidat fait un tour à 360° de sa pièce avec sa webcam pour montrer qu'il est seul et que son poste de travail est conforme. |
| **Enregistrer la vidéo et l'audio** | La webcam et le micro du candidat sont enregistrés pendant tout le test (la webcam et le micro sont donc obligatoires). La vidéo, avec le son, est consultable à la revue. Cette option est requise pour la [surveillance en direct](#surveillance-en-direct). |
| **Prendre des captures régulières de l'écran** | Captures d'écran périodiques de l'écran et de la webcam pendant le test. |
| **Nécessite le navigateur sécurisé** | Le test ne peut être passé que dans **Safe Exam Browser**, un navigateur d'examen qui verrouille le poste du candidat. Voir [la section dédiée](#navigateur-securise) ci-dessous. |

Cliquez sur **Enregistrer** pour persister la configuration. Le profil peut alors être choisi lors de l'[inscription d'un candidat à un test](#activer-surveillance) ou imposé par une [session surveillée en direct](#surveillance-en-direct).

### Le navigateur sécurisé (Safe Exam Browser) {#navigateur-securise}

L'option **Nécessite le navigateur sécurisé** impose le passage du test dans **Safe Exam Browser (SEB)**, un navigateur d'examen gratuit (Windows et macOS) qui verrouille le poste pendant toute la durée du test : le candidat ne peut ni changer d'application, ni ouvrir d'autres sites, ni utiliser le copier-coller vers l'extérieur.

Côté candidat, le parcours est le suivant :

1. Il installe **Safe Exam Browser** une seule fois sur sa machine (le lien de téléchargement lui est proposé au lancement du test).
2. Quand il démarre un test qui exige le navigateur sécurisé, la plateforme lui fait télécharger un **fichier d'examen personnel** (`.seb`). En l'ouvrant, SEB se lance directement sur son test, déjà connecté à son compte.
3. La plateforme vérifie **à chaque page** que le test se déroule bien dans SEB — il est impossible de démarrer dans SEB puis de continuer dans un navigateur classique.
4. À la fin du test, SEB se ferme automatiquement.

Selon le contenu du test, SEB autorise automatiquement ce qui est nécessaire — et uniquement cela : les applications requises par les questions à dépôt de fichier (par exemple **Excel** pour une question de classeur à compléter), ou la navigation vers le site d'exercice pour les tests **WordPress**. Aucune autre application ni aucun autre site ne sont accessibles.

Règles d'interaction avec les autres options du profil :

- Activer le navigateur sécurisé **coche et verrouille « Empêcher le candidat d'ouvrir d'autres fenêtres ou onglets »** (le verrouillage est garanti par SEB lui-même) et **désactive la liste blanche de sites** (le filtrage des sites est intégré au navigateur sécurisé).
- **Captures d'écran** — les captures régulières de l'écran ne sont **pas disponibles** avec le navigateur sécurisé, quel que soit le système : l'option **Prendre des captures régulières de l'écran** est décochée et grisée, et une note l'explique sous les options. L'enregistrement **audio et vidéo** fonctionne normalement. Dans une session surveillée en direct, aucune capture n'est enregistrée mais l'écran du candidat reste visible par le surveillant.

    ![Profil avec navigateur sécurisé](img/05-modal-profil-seb.png)

- Désactiver **Utiliser la surveillance à distance et / ou un navigateur sécurisé** remet à zéro toutes ses options, y compris le navigateur sécurisé.

> ⚠️ **Contenus vidéo sous Windows** — Safe Exam Browser pour Windows ne lit pas les vidéos au format MP4/H.264. Si votre test contient des vidéos dans ce format, contactez votre interlocuteur Isograd avant d'activer le navigateur sécurisé.

### Définir un profil par défaut

Le profil **par défaut** est appliqué automatiquement à tous les tests surveillés pour lesquels aucun profil n'est explicitement choisi à l'inscription.

1. Sur la ligne du profil, cliquez sur **Définir comme profil de surveillance par défaut**.
2. Confirmez. L'étiquette **Par défaut** se déplace vers ce profil ; l'ancien profil par défaut reste actif mais n'est plus appliqué automatiquement.

### Modifier un profil

1. Sur la ligne du profil, cliquez sur l'icône **Modifier** (crayon).
2. Ajustez les options.
3. **Enregistrer**.

> ⚠️ **Effet sur les tests en cours** — La modification d'un profil **n'affecte pas** les tests déjà démarrés ou terminés : seuls les **futurs** tests qui utiliseront ce profil auront les nouvelles options. Les enregistrements existants restent ceux du profil au moment du démarrage.

### Supprimer un profil

1. Sur la ligne du profil, cliquez sur l'icône **Supprimer**.
2. Confirmez.

> ⚠️ **Profil utilisé** — Si le profil est associé à des tests, une **seconde confirmation** vous indique leur nombre : après la suppression, ces tests sont considérés comme **non surveillés** (les tests en attente sont recrédités de leur crédit de surveillance). La suppression est **refusée** dans deux cas : si votre compte n'a aucun pack de crédits de surveillance permettant ce recrédit, ou si le profil est utilisé par une [session surveillée en direct](#surveillance-en-direct) qui n'est pas terminée.


## Gestion des tests surveillés {#gestion-des-tests-surveilles}

Une fois vos tests passés sous surveillance, cette page vous permet de **revoir les incidents détectés** et de **valider ou invalider** chaque passage en fonction de la conformité observée.

Accédez à cette page via le menu **Surveillance → Surveillance**.

![Page "Gestion des tests surveillés"](img/03-page-tests-surveilles.png)

Chaque ligne du tableau représente **un test passé sous surveillance** :

| Colonne | Contenu |
|---|---|
| **ID** | Identifiant interne de l'inscription. |
| **Nom complet** | Identité du candidat. |
| **Test** | Nom du sujet passé. |
| **Date de passage** | Date et heure du passage. |
| **Type de surveillance** | Profil de surveillance utilisé (vidéo, plein écran, etc.). |
| **Statut de validation** | État actuel — **En attente**, **Validé**, **Non valide**. |
| **Incident** | Nombre et nature des incidents détectés automatiquement. |

### Filtres

Le panneau de filtres permet de cibler :

- **Rechercher** — texte libre sur le candidat.
- **Période** — dates de début et de fin de passage ; par défaut, la page affiche les tests d'hier et d'aujourd'hui. Élargissez la période pour retrouver des passages plus anciens.
- **Type de surveillance** — restreindre par type de surveillance, lorsque la colonne est affichée.
- **Statut de validation** — par exemple ne voir que les tests **En attente** de revue.
- **Incident** — ne voir que les tests avec ou sans incident.

### Examiner un test surveillé

Les boutons d'action en bout de ligne dépendent du type de surveillance et du statut :

- **Afficher les photos prises pendant le test** (icône caméra) — ouvre la revue du test, organisée en onglets : **Photos**, **Vidéo du test**, **Captures d'écran**, **Interruptions du test** et **Pièce d'identité**, selon ce que le profil a enregistré. Dans les onglets d'images, le commutateur **Afficher uniquement les images suspectes** filtre les captures où une IA a détecté une anomalie ; le bloc **Motifs relevés par l'IA** liste alors les motifs détectés, du plus fréquent au moins fréquent, avec leur nombre d'occurrences (visage peu visible, second appareil ou écran, document à portée de main, conversation avec un tiers, écouteurs, autre personne présente, autre onglet visible, logiciel de partage d'écran ou de contrôle à distance…). Cliquez sur un motif pour n'afficher que les images signalées pour ce motif ; cliquez de nouveau pour toutes les réafficher.

    <!-- Capture à régénérer (nécessite un test surveillé avec photos sur l'environnement) :
    ![Photos prises pendant le test](img/04-modal-photos.png) -->

- **Afficher la pièce d'identité** (icône silhouette) — affiche la photo de la pièce d'identité fournie par le candidat au démarrage.
- **Commentaire de revue du protocole** (icône loupe), selon le type de surveillance — pour les tests avec **incident**, cette fenêtre détaille chaque incident, sa nature, et offre un champ pour saisir l'explication du surveillant ou pour demander des informations au candidat.
- **Historique du chat** (icône bulles) — sur les tests passés dans une session [surveillée en direct](#surveillance-en-direct) : affiche le fil des messages échangés entre le candidat et les surveillants, avec les écoutes et conversations audio. Les signalements des surveillants (*Signalé par*) et ces échanges figurent aussi dans l'onglet **Interruptions du test** de la revue.

### Valider ou invalider un test

Une fois la revue effectuée, vous tranchez :

- **Valider** (icône ✓ verte) — le test est conforme. Le résultat du candidat est officialisé et les diplômes/rapports sont émis.
- **Invalider** (icône ✗ rouge) — le test n'est pas conforme (triche détectée, condition non respectée). Le résultat est marqué invalide ; aucun diplôme n'est émis.

Pour une **action en masse**, sélectionnez plusieurs tests via les cases en début de ligne, puis utilisez les boutons **Valider les examens sélectionnés** ou **Invalider les examens sélectionnés** dans la barre d'actions.

### Statuts de validation

| Statut | Signification |
|---|---|
| **En attente de détails** | Un incident a été détecté (par exemple, sortie du plein écran) mais aucune explication n'a encore été fournie. Vous devez détailler les raisons, ou demander au candidat de le faire. |
| **Détail en cours de validation** | Une explication a été saisie et est en attente d'examen par l'équipe Isograd (pour les certifications). |
| **Explication validée** | L'équipe Isograd a validé l'explication ; le test est conforme. |
| **Validé** | Le test a été validé par un administrateur du compte. |
| **Non valide** | Le test a été invalidé par un administrateur du compte. |

### Demander des explications au candidat

Pour les certifications avec incident, vous pouvez demander au candidat de **justifier l'incident** :

1. Sur la ligne, cliquez sur l'icône **Envoyer une demande de pièce d'identité** (ou l'équivalent pour un incident).
2. Le candidat reçoit un email l'invitant à fournir l'explication dans son espace.
3. Une fois sa réponse soumise, le statut passe à **Détail en cours de validation** et vous pouvez la consulter dans la fenêtre **Commentaire de revue du protocole**.

> 💡 **Bonnes pratiques de validation** — Pour les certifications officielles, soyez exigeant sur les incidents (sortie de plein écran > 60 secondes, présence d'une seconde personne sur les captures). Pour les évaluations internes en entreprise, vous pouvez être plus souple — la surveillance reste un outil dissuasif autant que punitif.


## Surveillance en direct {#surveillance-en-direct}

La **surveillance en direct** complète la surveillance à distance enregistrée : pendant une **session de passage** surveillée en direct, des **surveillants** de votre compte voient en temps réel la **caméra** et l'**écran** de chaque candidat, peuvent lui écrire, lui parler, l'avertir, signaler un incident ou arrêter son test — comme dans une salle d'examen.

### Prérequis

- Votre compte utilise la **surveillance à distance Isograd** (sinon la fonctionnalité n'apparaît pas).
- Un **profil de surveillance** à distance Isograd avec **Enregistrer la vidéo et l'audio** coché : c'est le seul type de profil compatible.
- Les surveillants disposent du privilège **Surveiller en direct les sessions de passage** (voir [Modifier les privilèges](/ai/fr/admins/#modifier-les-privileges)). Un surveillant ne voit que les sessions dont il est surveillant, sauf s'il a aussi le privilège **Voir toutes les sessions surveillées en direct**.
- Une [session de passage](/ai/fr/sessions/#creer-une-session) créée avec le commutateur **Surveillance en direct** activé, son profil de surveillance et ses surveillants. Le profil de la session est **imposé à tous les tests** qui lui sont rattachés.

### Les sessions en cours

Accédez à cette page via le menu **Surveillance → Surveillance en direct**.

![Page "Surveillance en direct"](img/06-page-sessions-direct.png)

La page liste les sessions surveillées en direct **actuellement ouvertes** (entre leur date de début et leur date de fin) dont vous êtes surveillant, avec pour chacune le nombre de **tests inscrits**, de **candidats connectés**, de **réunions actives** et la liste des **surveillants**. Le champ **Rechercher** filtre la liste sur le nom ou l'identifiant de la session. Cliquez sur **Voir les réunions** (icône caméra) en bout de ligne pour ouvrir la session.

### Les réunions d'une session

![Page "Réunions de la session"](img/07-page-reunions.png)

Les candidats d'une session sont répartis automatiquement en **réunions** d'au plus douze candidats : une nouvelle réunion s'ouvre d'elle-même quand des candidats supplémentaires démarrent leur test. Chaque carte indique le nombre de candidats connectés, le nombre de surveillants présents et l'heure d'ouverture ; la liste se rafraîchit toutes les dix secondes. Tant qu'aucun candidat n'a démarré de test, la page indique simplement qu'aucune réunion n'est en cours. Cliquez sur **Entrer dans la réunion** pour rejoindre une réunion.

### Dans la réunion

La page de la réunion porte le nom de la session et le numéro de la réunion. Chaque candidat connecté y apparaît dans une **carte** à son nom, avec son **écran** et sa **caméra**. Cliquez sur une carte, ou sur son bouton **Agrandir**, pour l'afficher en grand et en meilleure qualité ; **Réduire** la ramène à sa taille normale. Tant qu'aucun candidat n'est connecté, la page l'indique. La liste des candidats se rafraîchit toutes les dix secondes.

Aucun son n'est transmis par défaut : le micro du candidat est requis, mais vous ne l'entendez que pendant une écoute ou une conversation que vous ouvrez.

La barre en haut de la page affiche l'état de votre **connexion** à la réunion, le sélecteur **Changer de réunion** (avec le nombre de candidats connectés dans chaque réunion de la session), les **surveillants présents** et le bouton **Quitter la réunion**. Pendant une écoute ou une conversation, elle affiche aussi le nom du candidat concerné, la durée écoulée et le bouton **Arrêter l'audio**.

Pour chaque candidat, vous disposez des actions suivantes :

| Action | Effet |
|---|---|
| **Messages** | Ouvre un volet de conversation écrite avec le candidat. Vous y retrouvez l'historique des messages, y compris ceux des autres surveillants, identifiés par leur nom. Une pastille rouge sur le bouton compte les messages du candidat que vous n'avez pas encore lus. Les messages sont conservés avec le test. |
| **Écouter** | Ouvre une écoute : vous entendez le candidat, lui ne vous entend pas. |
| **Parler** | Ouvre une conversation audio dans les deux sens ; votre navigateur vous demande l'accès à votre micro. |
| **Avertir** | Affiche un message de votre choix sur l'écran du candidat pendant vingt secondes. |
| **Signaler** | Enregistre un **incident** avec votre description ; il apparaît ensuite, avec votre nom, dans la revue du test et dans le [procès-verbal de la session](/ai/fr/sessions/#proces-verbal). |
| **Arrêter** / **Reprendre** | Après confirmation, interrompt le test du candidat, qui est renvoyé à sa liste de tests. Sa carte reste affichée avec la mention *Test arrêté par un surveillant* et le bouton devient **Reprendre** : la reprise lui rend le temps écoulé pendant l'arrêt. C'est la même action que depuis la fiche du candidat. |

> 💡 **Une seule conversation audio à la fois** — Une réunion n'admet qu'une écoute ou conversation audio à la fois, tous surveillants confondus : tant qu'un surveillant en a ouvert une, les boutons audio des autres cartes sont désactivés et la carte concernée indique son nom. L'audio s'arrête automatiquement après dix minutes ; cliquez de nouveau sur le bouton actif, ou sur **Arrêter l'audio**, pour l'arrêter plus tôt. Si le candidat ne répond pas à la demande ou si son micro n'est pas disponible, un message vous l'indique.

Pour interrompre **tous** les candidats à la fois, utilisez la [mise en pause de la session](/ai/fr/sessions/#mettre-en-pause-une-session) depuis la page des sessions.

> 💡 **Navigateur sécurisé** — Avec un profil qui impose le navigateur sécurisé, aucune capture d'écran n'est enregistrée, mais l'écran du candidat reste visible par le surveillant pendant la surveillance en direct.

> 💡 **Trace dans la revue** — Ce qui se passe en direct est conservé avec le test : sur la page **Gestion des tests surveillés**, les signalements des surveillants, les messages échangés et les écoutes et conversations audio (avec leur durée) apparaissent dans la revue du test, onglet **Interruptions du test**, et le bouton **Historique du chat** affiche le fil des échanges. Les avertissements affichés à l'écran du candidat ne sont pas conservés : pour garder une trace, utilisez **Signaler** ou **Messages**.


## Activer la surveillance sur un test {#activer-surveillance}

La surveillance ne s'active **pas** à la pièce sur cette page : elle est décidée **au moment de l'inscription** d'un candidat à un test. Pour activer la surveillance sur un test :

1. Inscrivez le candidat au test (voir [Inscrire un candidat à un test](/ai/fr/candidates/#inscrire-un-candidat-a-un-test)).
2. Dans la fenêtre d'inscription, activez l'option **Surveillance à distance**.
3. Choisissez le **profil de surveillance** à appliquer dans la liste ; à défaut, le **profil par défaut** s'applique automatiquement.

Si le candidat est inscrit sur une [session surveillée en direct](#surveillance-en-direct), le profil de la session est imposé : le sélecteur est verrouillé et un message l'indique.
