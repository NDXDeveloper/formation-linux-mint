🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9 Web Apps Manager (Transformer des sites en applications)

## Introduction

**Web Apps Manager** est un outil exclusif à Linux Mint qui permet de transformer n'importe quel site web en application autonome. Vous pouvez ainsi accéder à vos sites favoris comme s'ils étaient des applications installées sur votre ordinateur, avec leur propre icône, leur propre fenêtre, et leur propre espace dans le menu.

## Qu'est-ce qu'une Web App ?

### Définition

Une **Web App** (Application Web) est un site web qui fonctionne comme une application indépendante :
- **Icône dédiée** dans le menu et la barre des tâches
- **Fenêtre séparée** du navigateur principal
- **Pas de barre d'adresse** ni d'onglets (interface épurée)
- **Raccourcis directs** sans ouvrir le navigateur

**Exemple concret** :
Au lieu d'ouvrir Firefox → Taper "gmail.com" → Se connecter, vous cliquez simplement sur l'icône "Gmail" dans votre menu, et Gmail s'ouvre directement dans sa propre fenêtre.

### Différence avec un navigateur classique

**Navigateur traditionnel** :
- Une fenêtre Firefox avec plusieurs onglets
- Barre d'adresse, favoris, extensions
- Tous les sites dans la même fenêtre

**Web App** :
- Une fenêtre par application
- Interface minimale (juste le contenu du site)
- Séparation claire entre les sites
- Apparaît comme une application normale

**Analogie** :
C'est comme avoir l'application Gmail installée sur votre ordinateur, mais en réalité c'est juste le site web Gmail dans une fenêtre dédiée.

## Pourquoi utiliser des Web Apps ?

### Avantages

**Organisation** :
- Séparez vie professionnelle et personnelle (Gmail pro / Gmail perso)
- Chaque service dans sa fenêtre
- Pas de mélange d'onglets

**Productivité** :
- Accès direct depuis le menu
- Alt+Tab entre applications comme des logiciels normaux
- Notifications dédiées (selon le site)

**Concentration** :
- Pas de distraction par d'autres onglets
- Interface épurée
- Focus sur une seule tâche

**Simplicité** :
- Plus besoin de chercher l'onglet Gmail parmi 20 autres
- Icône reconnaissable dans la barre des tâches
- Lancez en un clic

### Cas d'usage courants

**Services de messagerie** :
- Gmail, Outlook, ProtonMail
- Chaque compte email = une application

**Outils de productivité** :
- Google Drive, OneDrive
- Notion, Trello, Asana
- Office 365 online

**Communication** :
- WhatsApp Web, Telegram Web
- Discord, Slack, Teams

**Réseaux sociaux** :
- Twitter, LinkedIn, Facebook
- Chaque compte séparé si besoin

**Streaming** :
- YouTube, Netflix, Spotify Web
- Twitch, Disney+

**Autres** :
- Google Maps, Google Calendar
- Banque en ligne
- Sites d'administration spécifiques

## Lancer Web Apps Manager

### Depuis le menu

1. **Menu principal** → **Administration** → **Web Apps**
2. Ou tapez "Web Apps" dans la recherche du menu
3. L'application **Web Apps Manager** s'ouvre

### Interface de Web Apps Manager

**Fenêtre principale** :

**Barre supérieure** :
- Bouton **+** : Créer une nouvelle Web App
- Bouton **Actualiser** : Rafraîchir la liste
- Menu **☰** : Options

**Liste des Web Apps** :
- Toutes vos applications web créées
- Nom, icône, URL
- Navigateur utilisé (Firefox, Chrome, etc.)

**Détails de la Web App sélectionnée** :
- Icône
- Nom
- URL
- Navigateur
- Catégorie
- Options personnalisées

**Boutons d'action** :
- **Lancer** : Ouvrir la Web App
- **Modifier** : Changer les paramètres
- **Supprimer** : Retirer la Web App

## Créer une Web App

### Méthode simple

**Étape par étape** :

1. Ouvrez **Web Apps Manager**
2. Cliquez sur le bouton **+** (en haut à gauche)
3. Une fenêtre s'ouvre : **Nouvelle Web App**

**Champs à remplir** :

**Nom** :
- Nom de l'application (affiché dans le menu)
- Exemple : "Gmail", "YouTube", "Notion"

**Adresse** :
- URL complète du site
- Exemple : `https://mail.google.com`
- Exemple : `https://www.youtube.com`

**Icône** :
- Par défaut : Favicon du site (récupéré automatiquement)
- Cliquez sur l'icône pour changer
- Parcourez pour choisir une image personnalisée
- Ou laissez par défaut

**Catégorie** :
- Où l'application apparaît dans le menu
- Exemples : Bureautique, Internet, Multimédia, Développement
- Choisissez selon votre organisation

**Navigateur** :
- Quel navigateur utiliser pour cette Web App
- Options : Firefox, Chromium, Chrome (si installés)
- Par défaut : Firefox

**Navigation** :
- **Isolée** (recommandé) : La Web App reste sur le site défini
- **Ouverte** : Permet de suivre les liens externes

**Barre de navigation** :
- Cochez pour afficher une barre avec boutons retour/avant
- Décochez pour interface minimale (recommandé)

**Options avancées** (clic sur la flèche) :

**Paramètres personnalisés** :
- Arguments supplémentaires pour le navigateur
- Pour utilisateurs avancés
- Laissez vide par défaut

**Isolement** :
- Cookie et stockage séparés du navigateur principal
- Recommandé activé

4. Cliquez sur **OK**

**Résultat** :
- La Web App apparaît dans la liste
- Elle est maintenant dans votre menu (catégorie choisie)
- Icône dans le lanceur d'applications

### Exemples de création

#### Créer une Web App Gmail

1. **Web Apps Manager** → **+**
2. **Nom** : Gmail
3. **Adresse** : `https://mail.google.com`
4. **Icône** : Laissez par défaut (logo Gmail)
5. **Catégorie** : Internet
6. **Navigateur** : Firefox
7. **Navigation** : Isolée
8. **Barre de navigation** : Non
9. **OK**

**Utilisation** :
- Menu → Internet → Gmail
- Gmail s'ouvre dans sa fenêtre dédiée
- Connexion séparée de Firefox

#### Créer une Web App YouTube

1. **Web Apps Manager** → **+**
2. **Nom** : YouTube
3. **Adresse** : `https://www.youtube.com`
4. **Catégorie** : Multimédia
5. **OK**

#### Créer une Web App WhatsApp Web

1. **+**
2. **Nom** : WhatsApp
3. **Adresse** : `https://web.whatsapp.com`
4. **Catégorie** : Internet
5. **OK**

**Première utilisation** :
- Lancez l'app WhatsApp
- Scannez le QR code avec votre téléphone
- Restez connecté

#### Créer plusieurs comptes Gmail

**Scénario** : Vous avez un Gmail personnel et un Gmail professionnel.

**Gmail Personnel** :
1. **Nom** : Gmail Perso
2. **Adresse** : `https://mail.google.com`
3. **Catégorie** : Internet
4. **OK**

**Gmail Pro** :
1. **Nom** : Gmail Pro
2. **Adresse** : `https://mail.google.com`
3. **Catégorie** : Bureautique
4. **OK**

**Résultat** :
- Deux applications distinctes
- Connexions séparées (compte différent dans chaque)
- Icônes différentes pour les distinguer (changez-les manuellement)

### Trouver l'URL correcte

**Pour certains services** :

**Services Google** :
- Gmail : `https://mail.google.com`
- Google Drive : `https://drive.google.com`
- Google Calendar : `https://calendar.google.com`
- Google Keep : `https://keep.google.com`
- YouTube : `https://www.youtube.com`

**Microsoft** :
- Outlook : `https://outlook.live.com` ou `https://outlook.office.com`
- OneDrive : `https://onedrive.live.com`
- Office Online : `https://www.office.com`

**Communication** :
- WhatsApp Web : `https://web.whatsapp.com`
- Telegram Web : `https://web.telegram.org`
- Discord : `https://discord.com/app`
- Slack : `https://app.slack.com`

**Productivité** :
- Notion : `https://www.notion.so`
- Trello : `https://trello.com`
- Asana : `https://app.asana.com`

**Astuce** :
- Connectez-vous au service dans votre navigateur
- Copiez l'URL depuis la barre d'adresse
- C'est l'URL à utiliser

## Utiliser une Web App

### Lancer une Web App

**Depuis le menu** :
1. Menu principal
2. Catégorie choisie lors de la création
3. Cliquez sur l'icône de la Web App

**Depuis la recherche** :
1. Menu principal
2. Tapez le nom de la Web App
3. Cliquez sur le résultat

**Épingler à la barre des tâches** :
1. Lancez la Web App
2. Clic droit sur l'icône dans la barre des tâches
3. **Épingler**
4. L'icône reste même après fermeture
5. Accès en un clic

### Naviguer dans une Web App

**Mode Isolé** (par défaut) :
- Liens internes : S'ouvrent dans la Web App
- Liens externes : S'ouvrent dans le navigateur principal
- Exemple : Clic sur un lien Twitter dans Gmail → S'ouvre dans Firefox

**Mode Ouvert** :
- Tous les liens s'ouvrent dans la Web App
- Vous pouvez "sortir" du site initial
- Moins recommandé (perd l'isolation)

**Boutons de navigation** (si activés) :
- **←** : Page précédente
- **→** : Page suivante
- **⟳** : Actualiser

### Fermer une Web App

**Comme une application normale** :
- Cliquez sur **×** (fermer)
- Ou `Alt + F4`

**La Web App se ferme** :
- Session souvent conservée (restez connecté)
- Au prochain lancement, vous retrouvez votre session

### Notifications

**Certains sites envoient des notifications** :

**Première fois** :
- Le site demande l'autorisation
- Exemple : "Gmail souhaite envoyer des notifications"
- Acceptez ou refusez

**Si accepté** :
- Vous recevez des notifications de bureau
- Même quand la Web App est fermée (selon le site)
- Nouveaux emails, messages, etc.

**Gérer les notifications** :
- Paramètres système → **Notifications**
- Désactivez pour applications spécifiques

## Gérer les Web Apps

### Modifier une Web App

**Changer les paramètres** :

1. **Web Apps Manager**
2. Sélectionnez la Web App dans la liste
3. Cliquez sur **Modifier**
4. Modifiez :
   - Nom
   - URL
   - Icône
   - Catégorie
   - Navigateur
   - Options
5. **OK** pour sauvegarder

**Cas d'usage** :
- Corriger une URL
- Changer l'icône pour mieux distinguer
- Déplacer dans une autre catégorie

### Changer l'icône

**Personnaliser l'apparence** :

1. **Modifier** la Web App
2. Cliquez sur l'icône actuelle
3. **Parcourir** et sélectionnez une image
4. Formats supportés : PNG, JPG, SVG
5. **OK**

**Trouver des icônes** :

**Icônes officielles** :
- Site du service (section presse/brand)
- Exemple : Google fournit ses icônes

**Banques d'icônes gratuites** :
- [https://www.flaticon.com/](https://www.flaticon.com/)
- [https://icons8.com/](https://icons8.com/)
- [https://www.iconfinder.com/](https://www.iconfinder.com/)

**Icônes système** :
- `/usr/share/icons/` ou `/usr/share/pixmaps/`
- Icônes déjà sur votre système

**Taille recommandée** :
- 256×256 pixels minimum
- Format PNG avec transparence idéal

### Supprimer une Web App

**Retirer définitivement** :

1. **Web Apps Manager**
2. Sélectionnez la Web App
3. Cliquez sur **Supprimer**
4. Confirmez

**Résultat** :
- Web App disparaît du menu
- Icône retirée
- Sessions et données supprimées

**Note** : Vous pouvez toujours accéder au site via navigateur normal.

### Exporter/Importer des Web Apps

**Partager votre configuration** :

**Export** :
1. **Web Apps Manager** → Menu **☰**
2. **Exporter**
3. Choisissez l'emplacement
4. Fichier `.webapp` créé

**Import** :
1. **Web Apps Manager** → Menu **☰**
2. **Importer**
3. Sélectionnez le fichier `.webapp`
4. La Web App est ajoutée

**Utilité** :
- Réinstallation du système
- Partage avec d'autres utilisateurs
- Sauvegarde de votre configuration

## Paramètres et options avancées

### Navigateur par défaut

**Choisir le navigateur utilisé** :

Chaque Web App peut utiliser un navigateur différent :
- **Firefox** : Par défaut
- **Chromium** : Si installé
- **Google Chrome** : Si installé
- **Autres navigateurs** : Selon installation

**Pourquoi changer** :
- Compatibilité (certains sites mieux sur Chrome)
- Performances
- Préférences personnelles

**Exemple** :
- Gmail → Firefox
- Google Meet → Chrome (meilleure compatibilité)
- Spotify → Chromium

### Isolation des données

**Sessions séparées** :

**Activé** (recommandé) :
- Cookies séparés du navigateur principal
- Historique indépendant
- Connexions distinctes

**Exemple** :
- Gmail dans Firefox : Compte A
- Gmail en Web App : Compte B
- Pas de conflit

**Désactivé** :
- Partage cookies avec navigateur
- Moins d'isolation
- Une seule session

### Navigation isolée vs ouverte

**Isolée** (recommandé) :
- Reste sur le domaine défini
- Liens externes → Navigateur principal
- Expérience "application"

**Ouverte** :
- Suit tous les liens
- Peut naviguer partout
- Moins isolé

**Conseil** : Laissez sur Isolée pour vraie expérience application.

### Paramètres personnalisés

**Options avancées** (champ "Paramètres personnalisés") :

**Arguments de ligne de commande** pour le navigateur.

**Exemples** :

**Démarrer en plein écran** :
```
--start-fullscreen
```

**Désactiver les extensions** :
```
--disable-extensions
```

**Mode kiosque** :
```
--kiosk
```

**Mode sombre** (Chromium) :
```
--force-dark-mode
```

**Note** : Pour utilisateurs avancés. Laissez vide si incertain.

## Exemples d'usage pratiques

### Configuration productivité

**Espace de travail numérique** :

**Communication** :
- Gmail Pro
- Slack équipe
- Zoom / Google Meet

**Outils** :
- Notion (documentation)
- Trello (gestion projets)
- Google Drive Pro

**Résultat** :
- Tout accessible en un clic
- Organisation claire
- Séparation pro/perso

### Configuration étudiant

**Outils d'étude** :

- Gmail Université
- Google Drive Cours
- Google Calendar Emploi du temps
- Notion Notes
- YouTube (playlists cours)

**Avantages** :
- Tout centralisé
- Pas de distraction par onglets personnels
- Alt+Tab entre outils d'étude

### Configuration famille

**Plusieurs comptes** :

**Papa** :
- Gmail Papa
- YouTube Papa

**Maman** :
- Gmail Maman
- Facebook Maman

**Enfants** :
- YouTube Kids
- Applications éducatives

**Chacun sa session**, pas de mélange.

### Configuration streaming

**Divertissement** :

- Netflix
- YouTube
- Spotify Web
- Twitch

**Chaque service** dans sa fenêtre, interface épurée.

### Web Apps pour services bancaires

**Banque en ligne** :

1. Créez une Web App pour votre banque
2. **Nom** : Ma Banque
3. **Adresse** : URL de connexion
4. **Catégorie** : Bureautique ou créez "Finance"
5. Session dédiée, sécurisée

**Avantages sécurité** :
- Session isolée
- Pas de risque de phishing dans onglets mélangés
- Icône dédiée, facile à repérer

## Astuces et conseils

### Organisation du menu

**Créer des catégories personnalisées** :

Vous pouvez créer vos propres catégories :
1. Lors de création Web App
2. Champ **Catégorie** → Tapez un nouveau nom
3. Exemple : "Streaming", "Travail", "Réseaux sociaux"

**Résultat** :
- Nouvelle catégorie dans le menu
- Toutes vos Web Apps organisées logiquement

### Distinguer les Web Apps similaires

**Plusieurs comptes du même service** :

**Problème** : Deux Web Apps Gmail avec même icône.

**Solution** :
1. Modifiez l'icône de l'une
2. Ou changez le nom : "Gmail Perso" vs "Gmail Travail"
3. Ou les deux

**Icônes colorées** :
- Gmail Perso → Icône bleue
- Gmail Travail → Icône rouge

### Raccourcis clavier

**Personnaliser** :

Linux Mint permet d'assigner des raccourcis :
1. **Paramètres système** → **Clavier** → **Raccourcis**
2. Ajoutez un raccourci personnalisé
3. **Nom** : Ouvrir Gmail
4. **Commande** : `/usr/bin/webapp-manager-launcher gmail`
   (Remplacez "gmail" par l'ID de votre Web App)
5. Assignez un raccourci : `Super + G`

**Résultat** :
- `Super + G` → Gmail s'ouvre instantanément

### Synchronisation multi-appareils

**Accès partout** :

Les Web Apps utilisent les sites web, donc :
- Données synchronisées automatiquement
- Accédez depuis n'importe quel appareil
- Même configuration sur plusieurs PC (réimportez vos .webapp)

### Web Apps hors ligne

**PWA (Progressive Web Apps)** :

Certains sites supportent le mode hors ligne :
- Gmail : Brouillons accessibles
- Google Drive : Fichiers marqués disponibles hors ligne
- Notion : Pages en cache

**Fonctionne automatiquement** si le site le supporte.

### Nettoyer les données

**Réinitialiser une Web App** :

Si problèmes (session corrompue, bugs) :

**Solution 1** : Supprimer et recréer la Web App

**Solution 2** : Nettoyer le cache navigateur
- Ouvrez le navigateur normalement
- Paramètres → Vie privée → Effacer les données
- Sélectionnez le domaine concerné

## Dépannage

### Web App ne se lance pas

**Causes possibles** :

**Navigateur manquant** :
- La Web App est configurée pour un navigateur non installé
- Solution : Modifiez la Web App, changez le navigateur

**URL incorrecte** :
- Vérifiez l'adresse
- Testez dans le navigateur normal
- Corrigez l'URL

**Permissions** :
- Vérifiez que vous avez les droits
- Essayez de recréer la Web App

### Site ne s'affiche pas correctement

**Problèmes d'affichage** :

**User-Agent** :
- Certains sites détectent le navigateur
- Peuvent bloquer ou mal afficher

**Solution** :
- Essayez un autre navigateur (Chrome au lieu de Firefox)
- Ou ajoutez un User-Agent personnalisé (avancé)

**Mode mobile forcé** :
- Certains sites s'affichent en mobile
- Agrandissez la fenêtre
- Ou configurez un paramètre de navigateur

### Impossible de se connecter

**Sessions multiples** :

**Problème** : Le site limite les sessions simultanées.

**Solution** :
- Déconnectez-vous du navigateur principal
- Ou utilisez mode incognito dans navigateur
- Ou certains sites ont des limites strictes

### Notifications ne fonctionnent pas

**Vérifications** :

1. **Autorisations site** : Le site a-t-il demandé l'autorisation ?
2. **Paramètres système** : Notifications activées pour la Web App ?
3. **Navigateur** : Vérifiez paramètres notifications du navigateur

**Réactiver** :
- Dans la Web App, allez aux paramètres du site
- Autorisations → Notifications → Autoriser

### Web App très lente

**Performances** :

**Trop de Web Apps ouvertes** :
- Chaque Web App = instance de navigateur
- Consomme RAM
- Fermez celles inutilisées

**Site gourmand** :
- Certains sites sont lourds
- Normal, pas un problème de Web App

**Navigateur lourd** :
- Essayez un navigateur plus léger
- Firefox vs Chromium (testez)

## Alternatives et compléments

### Utilisateur avancé : Créer manuellement

**Fichiers .desktop** :

Linux utilise des fichiers `.desktop` pour les lanceurs.

**Créer manuellement** :
1. Créez un fichier `~/.local/share/applications/gmail.desktop`
2. Contenu :
```
[Desktop Entry]
Name=Gmail
Exec=firefox --new-window https://mail.google.com
Icon=gmail
Type=Application
Categories=Network;Email;
```
3. Enregistrez
4. Rafraîchissez le menu

**Avantage** : Contrôle total
**Inconvénient** : Plus complexe, Web Apps Manager plus simple

### Applications Electron natives

**Certains services ont des apps dédiées** :

**Disponibles** :
- **Slack** : Version desktop (Flatpak, .deb)
- **Discord** : Application native
- **VS Code** : Éditeur basé Electron
- **Signal** : Messagerie

**Différence avec Web Apps** :
- App native : Installée, peut-être plus de fonctionnalités
- Web App : Plus léger, toujours à jour automatiquement

**Conseil** : Testez les deux, gardez ce qui vous convient.

### Extensions navigateur

**Alternative dans Firefox/Chrome** :

**Extensions "App Mode"** :
- Certaines extensions créent des raccourcis similaires
- Moins intégré que Web Apps Manager

**Avantage Web Apps Manager** :
- Intégration système native
- Gestion centralisée
- Indépendant du navigateur

### Franz / Ferdi

**Gestionnaires de services web** :

**Franz** / **Ferdi** regroupent plusieurs services :
- Messageries (WhatsApp, Telegram, Slack)
- Tous dans une seule application
- Onglets internes

**Différence** :
- Franz/Ferdi : Tout dans une app
- Web Apps Manager : Une app par service

**Préférence** : Question d'organisation personnelle

## Sécurité et confidentialité

### Isolation des sessions

**Avantage sécurité** :

Chaque Web App est isolée :
- Cookies séparés
- Pas de croisement de tracking
- Comptes multiples sans confusion

**Exemple** :
- Gmail perso : Pas de tracking publicitaire lié au Gmail pro
- Vraie séparation vie privée/professionnelle

### Sites sensibles

**Banque, administration** :

Web Apps idéal pour :
- Session dédiée, sécurisée
- Icône reconnaissable (anti-phishing)
- Pas de risque de confusion avec onglets malveillants

**Toujours vérifier l'URL** au premier lancement.

### Données stockées

**Où sont les données ?** :

Les Web Apps utilisent :
- Profils Firefox/Chrome isolés
- Stockage dans `~/.local/share/`
- Cookies, cache, LocalStorage du site

**Supprimer données** :
- Supprimez la Web App
- Ou nettoyez cache navigateur pour ce domaine

## Limitations

### Ce que Web Apps Manager ne fait pas

**Pas de mode hors ligne natif** :
- Dépend du site web
- Si le site nécessite Internet, la Web App aussi

**Pas de fonctionnalités système avancées** :
- Pas d'intégration webcam/micro améliorée
- Pas d'accès fichiers système étendu
- Ce sont toujours des sites web

**Dépendance navigateur** :
- Si le navigateur a un bug, la Web App aussi
- Mises à jour via le navigateur

**Certains sites incompatibles** :
- Sites très complexes peuvent mal fonctionner
- Flash, technologies obsolètes non supportées

### Quand ne pas utiliser Web Apps

**Sites occasionnels** :
- Pas besoin de Web App pour un site visité rarement
- Gardez les favoris navigateur

**Sites nécessitant extensions** :
- Si vous utilisez extensions navigateur sur ce site
- Web Apps isolées n'ont pas accès aux extensions (selon config)

**Performance limitée** :
- PC ancien avec peu de RAM
- Chaque Web App consomme ~100-300 Mo
- Limitez le nombre simultané

## Conseils d'utilisation

### Combien de Web Apps créer ?

**Recommandations** :

**Débutant** : 3-5 Web Apps
- Services utilisés quotidiennement
- Gmail, YouTube, WhatsApp Web

**Utilisateur régulier** : 10-15 Web Apps
- Organisation par usage (perso, pro, loisirs)

**Power user** : 20+ Web Apps
- Granularité fine
- Chaque service important isolé

**Limite** : RAM de votre PC. Chaque Web App ouverte consomme.

### Organisation recommandée

**Par contexte** :

**Travail** :
- Catégorie "Bureautique" ou "Travail"
- Gmail Pro, Drive Pro, Slack, Notion

**Personnel** :
- Catégorie "Internet"
- Gmail Perso, Réseaux sociaux

**Divertissement** :
- Catégorie "Multimédia"
- Streaming, musique

**Résultat** : Menu organisé, navigation intuitive

### Mise à jour

**Pas besoin de mettre à jour les Web Apps** :
- Le site web est toujours à jour
- Seul le navigateur nécessite mises à jour
- Mises à jour système s'occupent de tout

## Ressources et liens

### Documentation

**Web Apps Manager** :
- Outil exclusif Linux Mint
- Pas de site dédié
- Documentation dans le blog Linux Mint

**Linux Mint Blog** :
- Annonces et fonctionnalités
- [https://blog.linuxmint.com/](https://blog.linuxmint.com/)

### Communauté

**Forums Linux Mint** :
- Section applications
- Partage de Web Apps
- Astuces et conseils

**Reddit** :
- r/linuxmint
- Discussions sur Web Apps

### Listes de Web Apps populaires

**Services courants** :

**Communication** :
- Gmail, Outlook, ProtonMail
- WhatsApp Web, Telegram Web
- Discord, Slack, Microsoft Teams

**Productivité** :
- Notion, Evernote, Google Keep
- Trello, Asana, Monday.com
- Google Drive, OneDrive, Dropbox

**Streaming** :
- YouTube, Netflix, Disney+
- Spotify Web, Deezer, SoundCloud
- Twitch

**Réseaux sociaux** :
- Twitter, LinkedIn, Facebook
- Instagram Web, TikTok Web

**Outils Google** :
- Gmail, Drive, Calendar, Keep
- Photos, Meet, Chat
- Maps, YouTube, YouTube Music

**Microsoft** :
- Outlook, OneDrive, Teams
- Office Online (Word, Excel, PowerPoint)

**Autres** :
- Canva (design graphique)
- Figma (design UI/UX)
- GitHub, GitLab
- ChatGPT, services IA

## Conclusion

Web Apps Manager est un outil simple mais puissant pour transformer votre expérience de navigation web en expérience applicative. En créant des applications dédiées pour vos services web préférés, vous gagnez en organisation, productivité et clarté.

**Points clés à retenir** :

- **Simple** : Créer une Web App prend 30 secondes
- **Pratique** : Accès direct depuis le menu, comme une vraie application
- **Organisation** : Séparez vos contextes (pro/perso, comptes multiples)
- **Gratuit** : Outil exclusif Linux Mint, aucun coût
- **Flexible** : Créez autant de Web Apps que nécessaire

**Pour commencer** :
1. Lancez Web Apps Manager
2. Créez votre première Web App (Gmail, YouTube...)
3. Testez et appréciez l'expérience
4. Ajoutez progressivement vos services favoris

**Cas d'usage idéaux** :
- Plusieurs comptes du même service (Gmail perso/pro)
- Services utilisés quotidiennement (Slack, Notion, etc.)
- Séparation nette de vos activités en ligne

Web Apps Manager transforme votre navigateur web en suite d'applications dédiées, offrant une expérience plus proche de celle des applications natives tout en conservant les avantages du web (toujours à jour, accessible partout). Essayez-le dès aujourd'hui avec vos services favoris !

---


⏭️ [Hypnotix (Lecteur IPTV pour la TV par Internet)](/05-applications-essentielles-et-outils-mint/10-hypnotix.md)
