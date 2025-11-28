🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.3 Client mail Thunderbird

## Introduction

Thunderbird est le client de messagerie par défaut de Linux Mint. Développé par la fondation Mozilla (les créateurs de Firefox), c'est un logiciel libre, gratuit et complet pour gérer vos emails, vos contacts et votre calendrier, directement depuis votre ordinateur.

## Pourquoi utiliser Thunderbird ?

### Avantages d'un client mail local

**Par rapport au webmail (Gmail, Outlook.com dans le navigateur)** :

- **Accès hors ligne** : Consultez vos emails sans connexion Internet
- **Centralisation** : Tous vos comptes email dans une seule application
- **Vie privée** : Vos emails sont sur votre ordinateur, pas analysés pour de la publicité
- **Productivité** : Interface optimisée, raccourcis clavier, recherche avancée
- **Sauvegarde locale** : Vos emails sont automatiquement sur votre disque dur
- **Pas de publicité** : Interface propre sans annonces

### Points forts de Thunderbird

- **Gratuit et open source** : Aucun coût, code auditable
- **Multi-comptes** : Gmail, Outlook, Yahoo, comptes professionnels, etc.
- **Sécurisé** : Chiffrement, protection anti-phishing
- **Extensible** : Des centaines d'extensions disponibles
- **Carnet d'adresses intégré** : Gestion de vos contacts
- **Calendrier** : Avec l'extension Lightning (intégrée par défaut)
- **Multiplateforme** : Disponible aussi sur Windows et macOS

## Premier lancement de Thunderbird

### Ouvrir Thunderbird

1. Menu principal → **Bureautique** → **Thunderbird Mail**
2. Ou tapez "Thunderbird" dans le menu de recherche

### Assistant de configuration

Au premier lancement, Thunderbird vous guide pour configurer votre premier compte email.

**Informations nécessaires** :
- Votre nom complet
- Votre adresse email
- Votre mot de passe

## Configuration d'un compte email

### Comptes automatiques (Gmail, Outlook, Yahoo, etc.)

Pour les fournisseurs populaires, Thunderbird configure tout automatiquement :

1. **Écran d'accueil** : Cliquez sur **Email**
2. **Vos informations** :
   - **Votre nom complet** : Prénom Nom (apparaîtra chez vos destinataires)
   - **Adresse électronique** : votre.email@exemple.com
   - **Mot de passe** : Votre mot de passe email
3. Cliquez sur **Continuer**
4. Thunderbird détecte automatiquement les paramètres
5. Cliquez sur **Terminé**

### Configuration Gmail spécifique

**Important pour Gmail** : Google utilise une connexion sécurisée spéciale.

1. Après avoir cliqué sur **Terminé**, une fenêtre Google s'ouvre
2. Connectez-vous à votre compte Google
3. Google demande : "Autoriser Thunderbird à accéder à votre compte ?"
4. Cliquez sur **Autoriser**
5. Fermez la fenêtre, vous revenez à Thunderbird
6. Vos emails se synchronisent automatiquement

**Authentification à deux facteurs** : Si vous utilisez la vérification en deux étapes, vous devrez peut-être créer un "mot de passe d'application" depuis les paramètres de sécurité Google.

### Configuration manuelle (comptes professionnels, autres)

Si Thunderbird ne détecte pas automatiquement :

1. À l'étape de détection, cliquez sur **Configuration manuelle**
2. Vous devez connaître :
   - **Serveur entrant** (IMAP ou POP3) : `imap.exemple.com`
   - **Port entrant** : généralement 993 (IMAP) ou 995 (POP3)
   - **Serveur sortant** (SMTP) : `smtp.exemple.com`
   - **Port sortant** : généralement 465 ou 587
   - **Sécurité** : SSL/TLS (recommandé)

**Où trouver ces informations ?** :
- Site web de votre fournisseur email
- Email de bienvenue lors de la création du compte
- Contactez votre support technique

### IMAP vs POP3 : Quelle différence ?

**IMAP (recommandé)** :
- Vos emails restent sur le serveur
- Synchronisation sur tous vos appareils
- Si vous supprimez un email sur votre téléphone, il disparaît aussi sur Thunderbird
- Nécessite une connexion pour voir les nouveaux messages

**POP3** :
- Les emails sont téléchargés et supprimés du serveur
- Pas de synchronisation entre appareils
- Tous vos emails sont en local (bon pour la confidentialité)
- Peut saturer le serveur si vous ne videz jamais

**Conseil** : Utilisez IMAP sauf raison spécifique.

## Interface de Thunderbird

### Vue d'ensemble

L'interface est divisée en plusieurs zones :

**Panneau de gauche** :
- Liste de vos comptes email
- Dossiers : Boîte de réception, Envoyés, Brouillons, Corbeille, etc.
- Dossiers locaux

**Panneau central** :
- Liste des messages du dossier sélectionné
- Colonnes : Expéditeur, Sujet, Date, Taille, etc.

**Panneau de droite** (optionnel) :
- Aperçu du message sélectionné
- Ou désactivé pour plus d'espace

**Barre d'outils en haut** :
- Relever, Écrire, Répondre, Transférer, etc.

### Personnaliser l'affichage

**Afficher/masquer le panneau d'aperçu** :
- `F8` ou Menu **Affichage** → **Disposition** → **Panneau des messages**

**Changer la disposition** :
- Menu **Affichage** → **Disposition** → Classique, Large, Verticale

**Densité de l'affichage** :
- Menu **☰** (trois barres) → **Densité** → Compact, Normal, Relax

## Gérer vos emails

### Relever les nouveaux messages

**Automatique** :
- Par défaut, Thunderbird vérifie automatiquement toutes les 10 minutes
- Un son peut jouer à l'arrivée d'un nouveau message

**Manuel** :
- Cliquez sur **Relever** dans la barre d'outils
- Raccourci : `Ctrl + Maj + T` (tous les comptes)
- Raccourci : `Ctrl + T` (compte actuel uniquement)

### Lire un email

**Deux façons** :
1. **Simple clic** : Affiche le message dans le panneau d'aperçu (en bas ou à droite)
2. **Double-clic** : Ouvre le message dans une nouvelle fenêtre

**Navigation** :
- `F` : Message suivant
- `B` : Message précédent

### Écrire un nouveau message

1. Cliquez sur **Écrire** dans la barre d'outils
2. Ou raccourci : `Ctrl + N`
3. Une nouvelle fenêtre s'ouvre :
   - **À** : Adresse du destinataire
   - **Cc** : Copie (destinataires qui voient qui d'autre reçoit)
   - **Cci** : Copie invisible (personne ne voit qui d'autre reçoit)
   - **Sujet** : Objet du message
   - **Corps** : Votre message

**Saisie des destinataires** :
- Tapez l'adresse email complète
- Ou commencez à taper un nom, Thunderbird propose vos contacts
- Pour plusieurs destinataires, séparez par des virgules

**Barre d'outils de rédaction** :
- Gras, italique, souligné
- Couleur du texte
- Listes à puces ou numérotées
- Alignement
- Insertion d'image, de lien, etc.

### Joindre un fichier

**Méthode 1** :
1. Dans la fenêtre de rédaction, cliquez sur **Joindre**
2. Parcourez et sélectionnez le(s) fichier(s)
3. Cliquez sur **Ouvrir**
4. Le fichier apparaît en haut du message

**Méthode 2** :
- Glissez-déposez le fichier depuis le gestionnaire de fichiers

**Taille limite** :
- La plupart des serveurs limitent à 25 Mo par email
- Pour les gros fichiers, utilisez un service de partage (Google Drive, WeTransfer, etc.)

### Envoyer un email

1. Vérifiez les destinataires et le sujet
2. Relisez votre message
3. Cliquez sur **Envoyer**
4. Ou raccourci : `Ctrl + Entrée`

**Brouillon automatique** :
- Thunderbird enregistre automatiquement votre message en cours dans **Brouillons**
- Vous pouvez fermer la fenêtre et reprendre plus tard

### Répondre à un email

**Répondre** :
1. Sélectionnez le message
2. Cliquez sur **Répondre**
3. Ou raccourci : `Ctrl + R`
4. Seul l'expéditeur sera en destinataire

**Répondre à tous** :
1. Cliquez sur **Répondre à tous**
2. Ou raccourci : `Ctrl + Maj + R`
3. Tous les destinataires du message original recevront votre réponse

**Conseil** :
- Utilisez "Répondre" pour une réponse personnelle
- Utilisez "Répondre à tous" pour poursuivre une discussion de groupe
- Attention à ne pas faire "Répondre à tous" par erreur !

### Transférer un email

1. Sélectionnez le message
2. Cliquez sur **Transférer**
3. Ou raccourci : `Ctrl + L`
4. Le message original est inclus
5. Les pièces jointes sont conservées
6. Ajoutez vos destinataires et votre message

### Marquer comme lu/non lu

**Marquer comme lu** :
- Clic droit → **Marquer** → **Comme lu**
- Raccourci : `M`

**Marquer comme non lu** :
- Clic droit → **Marquer** → **Comme non lu**
- Raccourci : `Maj + M`

**Marquer tout comme lu** :
- Clic droit sur un dossier → **Marquer le dossier comme lu**

### Marquer comme important (étoile)

1. Cliquez sur l'**étoile** à gauche du message
2. Ou sélectionnez le message et appuyez sur `S`
3. L'étoile devient dorée
4. Vous pouvez filtrer pour voir uniquement les messages importants

### Supprimer un email

**Supprimer** :
1. Sélectionnez le message
2. Appuyez sur `Suppr` ou cliquez sur l'icône **Supprimer**
3. Le message va dans la **Corbeille**

**Vider la corbeille** :
1. Clic droit sur **Corbeille**
2. **Vider la corbeille**
3. Les messages sont définitivement supprimés

**Suppression définitive directe** :
- `Maj + Suppr` : Supprime sans passer par la corbeille (attention !)

## Organisation des emails

### Les dossiers par défaut

**Boîte de réception** : Nouveaux emails non classés

**Brouillons** : Messages en cours de rédaction

**Envoyés** : Copies des messages envoyés

**Corbeille** : Messages supprimés (temporairement)

**Courrier indésirable** : Spam détecté automatiquement

**Archives** : Pour archiver des emails importants à conserver

### Créer des dossiers personnalisés

**Exemple** : Créer des dossiers "Travail", "Famille", "Factures", etc.

1. Clic droit sur votre compte email
2. **Nouveau dossier**
3. Donnez un nom : "Travail"
4. Cliquez sur **Créer un dossier**

**Sous-dossiers** :
- Clic droit sur un dossier → **Nouveau sous-dossier**
- Exemple : "Travail" → "Projets" → "Projet-A"

### Déplacer des messages

**Glisser-déposer** :
1. Sélectionnez un ou plusieurs messages
2. Glissez vers le dossier de destination

**Par menu** :
1. Clic droit sur le message
2. **Déplacer vers** → Choisissez le dossier

**Raccourci** :
- `M` : Menu rapide pour déplacer

### Archiver des messages

**Archivage** :
1. Sélectionnez le(s) message(s)
2. Cliquez sur **Archiver** ou appuyez sur `A`
3. Le message va dans le dossier **Archives**
4. Il disparaît de la boîte de réception mais n'est pas supprimé

**Pourquoi archiver ?** :
- Garde la boîte de réception propre
- Conserve les emails importants
- Libère visuellement l'espace sans perdre d'information

## Filtres de messages (Règles automatiques)

Les filtres permettent d'organiser automatiquement vos emails entrants.

### Créer un filtre simple

**Exemple** : Tous les emails de "patron@entreprise.com" vont dans le dossier "Travail"

1. Menu **☰** → **Filtres de messages**
2. Sélectionnez le compte concerné
3. Cliquez sur **Nouveau**
4. **Nom du filtre** : "Emails du patron"
5. **Appliquer le filtre quand** : "Réception d'un nouveau message"
6. **Critères** :
   - "De" "est" "patron@entreprise.com"
7. **Actions** :
   - "Déplacer le message vers" → Sélectionnez "Travail"
8. Cliquez sur **OK**

### Exemples de filtres utiles

**Newsletters** :
- Critère : "Sujet" "contient" "Newsletter"
- Action : Déplacer vers "Newsletters"

**Factures** :
- Critère : "Sujet" "contient" "Facture"
- Action : Déplacer vers "Factures" ET Marquer comme important

**Spam personnalisé** :
- Critère : "De" "contient" "publicite"
- Action : Supprimer le message

**Combiner plusieurs critères** :
- "Correspondre à tous" : ET logique (toutes les conditions doivent être vraies)
- "Correspondre à au moins un" : OU logique (au moins une condition vraie)

### Tester et modifier un filtre

**Exécuter manuellement** :
1. Menu **☰** → **Filtres de messages**
2. Sélectionnez le filtre
3. Cliquez sur **Lancer maintenant**
4. Choisissez le dossier à analyser

**Modifier** :
1. Ouvrez les filtres
2. Double-cliquez sur le filtre à modifier
3. Ajustez les paramètres

**Désactiver temporairement** :
- Décochez la case à côté du nom du filtre

## Étiquettes (Tags)

Les étiquettes permettent de catégoriser vos emails avec des couleurs.

### Appliquer une étiquette

1. Sélectionnez un message
2. Clic droit → **Étiqueter** → Choisissez une étiquette
3. Le message est coloré dans la liste

**Étiquettes par défaut** :
- Important (rouge)
- Travail (orange)
- Personnel (vert)
- À faire (bleu)
- Plus tard (violet)

### Créer une étiquette personnalisée

1. Menu **☰** → **Paramètres** → **Général**
2. Descendez à **Étiquettes**
3. Cliquez sur **Nouvelle étiquette**
4. Nom : "Urgent"
5. Choisissez une couleur
6. Cliquez sur **OK**

### Filtrer par étiquette

En haut de la liste des messages :
- Cliquez sur l'icône de filtre (entonnoir)
- Sélectionnez l'étiquette à afficher
- Seuls les messages avec cette étiquette s'affichent

## Recherche de messages

### Recherche rapide

**Barre de recherche** (en haut) :
1. Tapez un mot-clé (nom, sujet, contenu)
2. Thunderbird affiche les résultats en temps réel
3. `Ctrl + K` : Focus sur la barre de recherche

**Filtres rapides** :
- À côté de la barre de recherche, filtrez par :
  - Non lus
  - Importants
  - Avec pièce jointe
  - Contacts
  - Etc.

### Recherche avancée

1. Menu **Édition** → **Rechercher dans les messages**
2. Ou `Ctrl + Maj + F`
3. Définissez vos critères :
   - **De, À, Sujet** : Contient tel mot
   - **Date** : Entre telle et telle date
   - **Taille** : Plus grand/petit que X Mo
   - **Pièce jointe** : Oui/Non
   - **Lu/Non lu**
4. Cliquez sur **Rechercher**
5. Les résultats s'affichent dans une nouvelle fenêtre

**Enregistrer une recherche** :
- Après une recherche avancée, cliquez sur **Enregistrer comme dossier de recherche**
- Nommez-le
- Il apparaît dans le panneau de gauche comme un dossier virtuel

## Carnet d'adresses

Le carnet d'adresses stocke vos contacts.

### Ouvrir le carnet d'adresses

1. Menu **☰** → **Carnet d'adresses**
2. Ou cliquez sur l'icône dans la barre d'outils
3. Raccourci : `Ctrl + Maj + B`

### Ajouter un contact manuellement

1. Dans le carnet d'adresses, cliquez sur **Nouveau contact**
2. Remplissez les informations :
   - **Nom**
   - **Prénom**
   - **Email** (obligatoire)
   - **Téléphone, Adresse**, etc. (optionnel)
3. Cliquez sur **OK**

### Ajouter depuis un email reçu

**Méthode rapide** :
1. Dans un email, clic droit sur l'adresse de l'expéditeur
2. **Ajouter au carnet d'adresses** → **Adresses personnelles**

**Thunderbird mémorise automatiquement** :
- Les adresses auxquelles vous écrivez sont ajoutées à **Adresses collectées**
- Vous pouvez les déplacer vers **Adresses personnelles** ensuite

### Créer des listes de diffusion

**Exemple** : Groupe "Famille" pour envoyer un email à toute la famille en une fois

1. Carnet d'adresses → **Nouvelle liste**
2. **Nom de la liste** : "Famille"
3. Ajoutez les membres :
   - Tapez les emails un par un
   - Ou glissez des contacts depuis le carnet
4. Cliquez sur **OK**

**Utiliser la liste** :
- Lors de la rédaction d'un email, tapez "Famille" dans le champ **À**
- Thunderbird envoie à tous les membres de la liste

### Importer/Exporter des contacts

**Importer** :
1. Carnet d'adresses → **Outils** → **Importer**
2. Choisissez le format (vCard, CSV, LDIF)
3. Sélectionnez le fichier
4. Importez

**Exporter** :
1. Carnet d'adresses → **Outils** → **Exporter**
2. Choisissez le carnet à exporter
3. Format recommandé : vCard (.vcf) ou CSV
4. Enregistrez

## Calendrier

Thunderbird intègre un calendrier complet.

### Afficher le calendrier

1. Cliquez sur l'onglet **Calendrier** en haut
2. Ou `Ctrl + Maj + C`

### Vue du calendrier

**Différentes vues** :
- **Jour** : Planning de la journée
- **Semaine** : Vue hebdomadaire
- **Mois** : Vue mensuelle
- **Multiweek** : Plusieurs semaines

**Changer de vue** :
- Boutons en haut du calendrier
- Raccourcis : `1` (jour), `2` (semaine), `3` (multiweek), `4` (mois)

### Créer un événement

**Méthode rapide** :
1. Double-cliquez sur une date/heure dans le calendrier
2. Tapez le titre de l'événement
3. Appuyez sur `Entrée`

**Méthode complète** :
1. Clic droit sur une date → **Nouvel événement**
2. Ou cliquez sur **Nouvel événement** dans la barre d'outils
3. Remplissez :
   - **Titre** : "Réunion"
   - **Lieu** : "Bureau"
   - **Date et heure** : Début et fin
   - **Description** : Détails supplémentaires
   - **Rappel** : 15 minutes avant, 1 heure avant, etc.
   - **Répéter** : Si événement récurrent
4. Cliquez sur **Enregistrer et fermer**

### Créer une tâche (To-Do)

1. Onglet **Tâches** (à côté de Calendrier)
2. Cliquez sur **Nouvelle tâche**
3. Remplissez :
   - **Titre** : "Appeler le dentiste"
   - **Échéance** : Date limite
   - **Priorité** : Faible, Normale, Élevée
   - **Statut** : À faire, En cours, Terminé
4. Enregistrez

**Marquer comme terminée** :
- Cochez la case à côté de la tâche

### Inviter des personnes (événement)

1. Lors de la création d'un événement
2. Section **Participants**
3. Cliquez sur **Inviter des participants**
4. Ajoutez les adresses email
5. Enregistrez l'événement
6. Thunderbird enverra automatiquement des invitations par email

### Synchroniser avec Google Calendar

**Installer l'extension** :
1. Menu **☰** → **Modules complémentaires et thèmes**
2. Recherchez "Provider for Google Calendar"
3. Installez l'extension
4. Redémarrez Thunderbird

**Ajouter Google Calendar** :
1. Calendrier → Clic droit dans le panneau calendrier
2. **Nouveau calendrier**
3. **Sur le réseau**
4. Sélectionnez **Google Calendar**
5. Connectez-vous à Google
6. Autorisez Thunderbird
7. Sélectionnez vos calendriers à synchroniser

## Paramètres importants

### Accéder aux paramètres

Menu **☰** → **Paramètres** (ou **Préférences**)

### Paramètres de compte

**Paramètres du serveur** :
1. **Paramètres** → **Paramètres des comptes**
2. Sélectionnez votre compte → **Paramètres du serveur**
3. Configuration :
   - **Vérifier les nouveaux messages toutes les X minutes** : 10 par défaut
   - **Supprimer les messages du serveur après téléchargement** (POP3)
   - **Conserver les messages** (options de nettoyage)

**Copies et dossiers** :
- Où enregistrer les brouillons
- Où enregistrer les messages envoyés
- Où placer les archives

**Identité** :
- Votre nom affiché
- Adresse de réponse
- Signature (texte ajouté automatiquement en bas de vos emails)

### Créer une signature

1. **Paramètres des comptes** → Sélectionnez votre compte → **Identité**
2. Section **Signature**
3. Tapez votre signature :
   ```
   Cordialement,
   Prénom Nom
   Titre
   Entreprise
   Téléphone : 01 23 45 67 89
   ```
4. Cochez **Utiliser HTML** si vous voulez du formatage
5. Sauvegardez

**Signature depuis un fichier** :
- Cochez **Utiliser le fichier à la place**
- Créez un fichier .txt ou .html avec votre signature
- Sélectionnez-le

### Affichage

**Police et couleurs** :
1. **Paramètres** → **Général** → **Langue et apparence**
2. Ajustez la taille des polices

**Thème** :
- **Clair**, **Sombre**, ou **Système** (suit le thème de Linux Mint)

**Densité** :
- **Compact**, **Normal**, **Relax** (espacement)

### Notifications

1. **Paramètres** → **Général**
2. Section **Notifications**
3. Cochez **Afficher une alerte** pour les nouveaux messages
4. **Jouer un son** : Choisissez ou désactivez

**Notifications système** :
- Linux Mint affiche une notification de bureau quand un email arrive
- Paramètres système → **Notifications** pour ajuster

### Composer des messages

1. **Paramètres** → **Composition**
2. Options importantes :
   - **Vérifier l'orthographe avant l'envoi**
   - **Format par défaut** : Texte brut ou HTML
   - **Citation automatique du message original** (lors d'une réponse)
   - **Police par défaut**

**Texte brut vs HTML** :
- **HTML** : Formatage (gras, couleurs, images)
- **Texte brut** : Simple texte, universel, plus léger

**Conseil** : HTML pour les emails personnels, texte brut pour les professionnels ou listes de diffusion.

### Confidentialité et sécurité

1. **Paramètres** → **Confidentialité et sécurité**

**Courrier indésirable (Spam)** :
- **Activer les contrôles adaptatifs pour ce compte**
- Thunderbird apprend au fil du temps

**Contenu distant** :
- Les emails peuvent charger des images externes (trackers)
- **Bloquer les contenus distants dans les messages** (recommandé)
- Vous pouvez autoriser au cas par cas

**Anti-hameçonnage** :
- **Signaler les messages suspects** : Activé par défaut
- Thunderbird détecte les tentatives de phishing

**Antivirus** :
- **Autoriser les logiciels antivirus à mettre en quarantaine les messages**

## Sécurité et chiffrement

### Certificats et signatures numériques

**Signature numérique** :
- Prouve que l'email vient bien de vous
- Nécessite un certificat numérique

**Chiffrement** :
- Rend le contenu illisible sans la clé
- Nécessite un certificat pour vous et le destinataire

**OpenPGP intégré** :
- Thunderbird supporte maintenant OpenPGP nativement
- **Paramètres des comptes** → **Chiffrement de bout en bout**

**Pour débuter** :
1. Générez une paire de clés OpenPGP
2. Échangez votre clé publique avec vos correspondants
3. Chiffrez vos emails sensibles

### Mots de passe

**Gestionnaire de mots de passe** :
1. **Paramètres** → **Confidentialité et sécurité**
2. **Mots de passe enregistrés**
3. Voyez et gérez tous vos mots de passe

**Mot de passe principal** :
- Protège tous vos mots de passe email
- **Utiliser un mot de passe principal**
- Vous devez le saisir au démarrage de Thunderbird

## Extensions (Modules complémentaires)

Les extensions ajoutent des fonctionnalités à Thunderbird.

### Installer une extension

1. Menu **☰** → **Modules complémentaires et thèmes**
2. Onglet **Extensions**
3. Recherchez une extension
4. Cliquez sur **Ajouter à Thunderbird**
5. Redémarrez si nécessaire

### Extensions recommandées

**Lightning** :
- Calendrier intégré (normalement déjà installé)

**Provider for Google Calendar** :
- Synchronise avec Google Calendar

**Thunderbird Conversations** :
- Affichage des emails comme une conversation (style Gmail)

**Send Later** :
- Planifier l'envoi d'un email à une date/heure précise

**QuickText** :
- Modèles de réponses rapides

**ImportExportTools NG** :
- Import/export avancé de messages et dossiers

**ThunderStats** :
- Statistiques sur vos emails

### Gérer les extensions

**Désactiver** :
1. **Modules complémentaires**
2. Trouvez l'extension
3. Basculez l'interrupteur

**Supprimer** :
- Cliquez sur les trois points → **Supprimer**

## Raccourcis clavier

### Navigation

| Raccourci | Action |
|-----------|--------|
| `F` | Message suivant |
| `B` | Message précédent |
| `N` | Suivant non lu |
| `P` | Précédent non lu |
| `F8` | Afficher/Masquer le panneau de messages |

### Actions sur les messages

| Raccourci | Action |
|-----------|--------|
| `Ctrl + N` | Nouveau message |
| `Ctrl + R` | Répondre |
| `Ctrl + Maj + R` | Répondre à tous |
| `Ctrl + L` | Transférer |
| `Suppr` | Supprimer |
| `Maj + Suppr` | Supprimer définitivement |
| `M` | Marquer comme lu |
| `Maj + M` | Marquer comme non lu |
| `S` | Important (étoile) |
| `A` | Archiver |
| `J` | Marquer comme indésirable |
| `Maj + J` | Marquer comme légitime |

### Rédaction

| Raccourci | Action |
|-----------|--------|
| `Ctrl + Entrée` | Envoyer le message |
| `Ctrl + S` | Enregistrer comme brouillon |
| `Ctrl + Maj + A` | Joindre un fichier |

### Dossiers et comptes

| Raccourci | Action |
|-----------|--------|
| `Ctrl + T` | Relever (compte actuel) |
| `Ctrl + Maj + T` | Relever tous les comptes |
| `Ctrl + K` | Recherche rapide |
| `Ctrl + Maj + F` | Recherche avancée |
| `Ctrl + Maj + B` | Carnet d'adresses |

### Calendrier

| Raccourci | Action |
|-----------|--------|
| `Ctrl + Maj + C` | Ouvrir le calendrier |
| `Ctrl + I` | Nouvel événement |
| `Ctrl + D` | Nouvelle tâche |
| `1` | Vue jour |
| `2` | Vue semaine |
| `3` | Vue multisemaine |
| `4` | Vue mois |

## Astuces et bonnes pratiques

### Organisation efficace

**Règle Inbox Zero** :
- Ne laissez rien dans la boîte de réception
- Traitez chaque email : Répondre, Archiver, Supprimer, ou Déplacer

**Utilisez les filtres** :
- Automatisez le tri dès réception
- Gain de temps considérable

**Archivez au lieu de supprimer** :
- L'archivage garde les emails au cas où
- Libère la boîte de réception
- Toujours accessible via recherche

### Sécurité

**Méfiez-vous du phishing** :
- Ne cliquez jamais sur un lien suspect
- Vérifiez l'adresse de l'expéditeur (pas juste le nom affiché)
- Votre banque ne vous demandera JAMAIS votre mot de passe par email

**Vérifiez avant de répondre** :
- "Répondre à tous" peut révéler des adresses email
- Attention aux faux expéditeurs

**Pièces jointes** :
- N'ouvrez jamais une pièce jointe d'un expéditeur inconnu
- Même d'un contact connu, soyez vigilant si inattendu

### Productivité

**Raccourcis clavier** :
- Apprenez les raccourcis de base
- Gain de temps énorme sur le long terme

**Signatures** :
- Une signature professionnelle donne une image sérieuse
- Incluez vos coordonnées importantes

**Modèles de réponse** :
- Pour les réponses répétitives, créez des modèles
- Extension **QuickText** très utile

**Dossiers de recherche** :
- Créez des vues virtuelles
- Exemple : "Tous les non lus de tous les comptes"

### Sauvegarde

**Localisation du profil** :
- `~/.thunderbird/` (dossier caché dans votre home)
- Contient tous vos emails, paramètres, contacts

**Sauvegarde recommandée** :
- Copiez régulièrement `~/.thunderbird/`
- Ou utilisez Timeshift (sauvegarde système complète)

**Export manuel** :
- Emails : Sélectionnez → Clic droit → **Enregistrer sous**
- Contacts : Carnet d'adresses → **Exporter**
- Calendrier : Calendrier → Clic droit → **Exporter**

## Dépannage courant

### Les emails n'arrivent pas

**Vérifications** :
1. Connexion Internet active ?
2. **Relever** manuellement (`Ctrl + Maj + T`)
3. Vérifiez les paramètres du serveur
4. Dossier **Courrier indésirable** (spam)
5. Quota du serveur atteint ?

### Impossible d'envoyer des emails

**Solutions** :
1. Vérifiez les paramètres SMTP
2. Certains FAI bloquent le port 25, utilisez 587
3. Vérifiez le mot de passe
4. Authentification requise pour le serveur sortant ?

### Thunderbird est lent

**Solutions** :
1. Compactez les dossiers : Clic droit sur dossier → **Compacter**
2. Videz la corbeille et le dossier indésirable
3. Désactivez les extensions inutilisées
4. Réindexez la base de données : Menu → **Outils** → **Reconstruire l'index**

### Messages dupliqués

**Cause** : Souvent lié à IMAP et synchronisation

**Solution** :
1. Supprimez les doublons
2. Extension **Remove Duplicate Messages**

### Profil corrompu

**Symptômes** : Crashs, ne démarre pas

**Solution** :
1. Créez un nouveau profil
2. Terminal : `thunderbird -ProfileManager`
3. Créez un profil de test
4. Si ça fonctionne, migrez vos données

### Certificat SSL/TLS invalide

**Symptôme** : Erreur de connexion sécurisée

**Solution** :
1. Vérifiez la date/heure système
2. **Paramètres** → **Confidentialité et sécurité** → **Certificats**
3. **Voir les certificats** → Supprimez l'ancien si problème
4. Reconnectez-vous

## Synchronisation multi-appareils

### IMAP : Synchronisation automatique

Avec IMAP :
- Vos emails sont sur le serveur
- Thunderbird sur PC, téléphone, webmail : tous synchronisés
- Un email lu sur le téléphone apparaît lu sur Thunderbird

### Synchroniser le carnet d'adresses

**Google Contacts** :
1. Extension **gContactSync** ou **Provider for Google Calendar** (inclut contacts)
2. Connectez votre compte Google
3. Vos contacts se synchronisent

**CardDAV** (pour autres services) :
1. Extension **CardBook**
2. Configurez votre serveur CardDAV (Nextcloud, etc.)

### Synchroniser le calendrier

**Google Calendar** :
- Extension **Provider for Google Calendar** (vu précédemment)

**CalDAV** (Nextcloud, etc.) :
1. Nouveau calendrier → **Sur le réseau**
2. **CalDAV**
3. URL de votre serveur
4. Authentification

## Alternatives à Thunderbird

Si Thunderbird ne vous convient pas :

### Evolution
- Client mail complet de GNOME
- Similaire à Outlook
- Bien intégré dans certains environnements

### Geary
- Simple et épuré
- GNOME native
- Moins de fonctionnalités qu'Thunderbird

### Mailspring
- Interface moderne et élégante
- Gratuit avec version Pro payante
- Bonne recherche et productivité

### Webmail
- Simplement utiliser votre navigateur
- Gmail, Outlook.com, etc.
- Avantage : Accessible partout
- Inconvénient : Nécessite Internet

## Migration depuis un autre client

### Depuis Windows Mail / Outlook

**Emails** :
1. Dans Outlook, exportez en fichier `.pst`
2. Utilisez un convertisseur PST vers Mbox
3. Importez le Mbox dans Thunderbird

**Plus simple** : Configurez le même compte IMAP dans Thunderbird

**Contacts** :
1. Outlook → Exporter en CSV
2. Thunderbird → Carnet d'adresses → Importer → CSV

### Depuis Gmail (webmail)

**Configuration simple** :
1. Ajoutez votre compte Gmail à Thunderbird (méthode vue précédemment)
2. Tous vos emails se synchronisent automatiquement via IMAP

**Contacts** :
- Extension pour synchroniser Google Contacts

## Ressources et aide

### Documentation officielle

- Site officiel : [https://www.thunderbird.net/](https://www.thunderbird.net/)
- Support : [https://support.mozilla.org/fr/products/thunderbird](https://support.mozilla.org/fr/products/thunderbird)

### Communauté

- Forum Mozilla francophone
- Forum Linux Mint (section applications)
- Reddit : r/Thunderbird

### Guides et tutoriels

- Documentation officielle très complète
- YouTube : Nombreux tutoriels vidéo en français

## Conclusion

Thunderbird est un client de messagerie mature, puissant et gratuit, idéal pour gérer professionnellement vos emails sur Linux Mint. Sa compatibilité avec tous les fournisseurs d'email, son carnet d'adresses intégré et son calendrier en font une solution complète.

Prenez le temps de configurer correctement vos comptes, de créer des filtres pour automatiser l'organisation, et d'explorer les extensions qui correspondent à vos besoins. Avec un peu de pratique, Thunderbird deviendra un outil indispensable de votre quotidien numérique.

---


⏭️ [Lecteurs multimédia (VLC, etc.)](/05-applications-essentielles-et-outils-mint/04-lecteurs-multimedia.md)
