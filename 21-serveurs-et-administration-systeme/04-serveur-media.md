🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 21.4 Serveur média (Plex, Jellyfin)

## Introduction

### Qu'est-ce qu'un serveur média ?

Un serveur média est un logiciel qui organise votre collection de films, séries TV, musique et photos, puis les rend accessibles sur tous vos appareils (TV, smartphone, tablette, ordinateur) via une interface élégante, similaire à Netflix ou Spotify.

**En termes simples :** Transformez votre ordinateur Linux Mint en votre propre Netflix personnel avec vos propres films et séries !

### Pourquoi créer un serveur média ?

- **Centralisation** : Toutes vos vidéos, films, séries au même endroit
- **Accessibilité** : Regardez vos médias partout dans la maison, ou même à l'étranger
- **Organisation automatique** : Affiches, descriptions, notes automatiquement téléchargées
- **Multi-appareils** : Smart TV, smartphone, tablette, navigateur web
- **Qualité** : Conservez vos fichiers en haute qualité, pas de compression comme sur les services de streaming
- **Indépendance** : Pas d'abonnement streaming, vous possédez votre contenu

### Cas d'usage courants

- Collection de films et séries personnelle
- Photos de famille accessibles sur tous les appareils
- Bibliothèque musicale centralisée
- Vidéos de vacances et souvenirs
- Contenus éducatifs pour enfants
- Podcasts et vidéos YouTube téléchargées

---

## Plex vs Jellyfin : Le grand débat

### Plex Media Server

**Avantages :**
- Interface ultra-polée et professionnelle
- Applications officielles pour tous les appareils
- Facile à configurer
- Excellent support de transcoding
- Fonctionnalités avancées (DVR TV, détection des intros)
- Grande communauté d'utilisateurs

**Inconvénients :**
- Nécessite un compte en ligne (même pour usage local)
- Certaines fonctionnalités nécessitent Plex Pass (abonnement payant)
- Logiciel propriétaire (code fermé)
- Collecte de données d'utilisation
- Dépend des serveurs Plex pour certaines fonctionnalités

**Prix :** Gratuit (avec limitations) ou Plex Pass : 5€/mois, 40€/an, 120€ à vie

### Jellyfin

**Avantages :**
- Complètement gratuit et open source
- Aucun compte requis
- Pas de télémétrie ni collecte de données
- Toutes les fonctionnalités débloquées gratuitement
- Contrôle total de vos données
- Communauté active et engagée

**Inconvénients :**
- Interface moins raffinée que Plex
- Moins d'applications officielles
- Configuration parfois plus technique
- Transcoding moins optimisé
- Métadonnées parfois moins précises

**Prix :** Entièrement gratuit

### Emby (mention)

Une troisième option existe : **Emby**. C'était autrefois open source mais est devenu propriétaire. Jellyfin est né d'un fork (version dérivée) d'Emby quand celui-ci est devenu payant.

### Lequel choisir ?

**Choisissez Plex si :**
- Vous voulez la meilleure expérience utilisateur
- Vous avez un budget pour Plex Pass
- Vous utilisez beaucoup d'appareils différents
- Vous voulez quelque chose qui "fonctionne simplement"

**Choisissez Jellyfin si :**
- Vous préférez l'open source et la confidentialité
- Vous ne voulez pas créer de compte en ligne
- Vous êtes à l'aise avec un peu de configuration
- Vous voulez un contrôle total gratuit

**Bonne nouvelle :** Vous pouvez installer les deux et tester !

---

## Installation de Plex Media Server

### Méthode 1 : Installation via le site officiel (recommandée)

#### Télécharger Plex

Visitez [plex.tv/downloads](https://www.plex.tv/downloads/) et téléchargez la version pour Linux (fichier .deb).

Ou en ligne de commande :

```bash
cd ~/Téléchargements
wget https://downloads.plex.tv/plex-media-server-new/1.40.0.7998-c29d4c0c8/debian/plexmediaserver_1.40.0.7998-c29d4c0c8_amd64.deb
```

**Note :** Le numéro de version change. Vérifiez sur le site pour la dernière version.

#### Installer le paquet

```bash
sudo dpkg -i plexmediaserver_*.deb
```

Si des dépendances manquent :

```bash
sudo apt-get install -f
```

#### Démarrer Plex

Plex démarre automatiquement après l'installation. Vérifiez :

```bash
sudo systemctl status plexmediaserver
```

Vous devriez voir "active (running)" en vert.

### Méthode 2 : Installation via le dépôt officiel

Ajoutez le dépôt Plex :

```bash
echo deb https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
```

Ajoutez la clé GPG :

```bash
curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -
```

Installez Plex :

```bash
sudo apt update
sudo apt install plexmediaserver
```

### Configuration initiale de Plex

#### Accéder à l'interface web

Ouvrez votre navigateur et allez sur :

```
http://localhost:32400/web
```

ou

```
http://votre_ip:32400/web
```

#### Créer un compte Plex

Vous devez créer un compte gratuit sur plex.tv ou vous connecter avec Google/Facebook.

**Important :** Même pour un usage 100% local, Plex nécessite un compte.

#### Assistant de configuration

1. **Donnez un nom à votre serveur** : "Serveur Média Maison", "Plex de Jean", etc.

2. **Cochez "Autoriser l'accès à mon média en dehors de mon domicile"** si vous voulez y accéder depuis Internet

3. Cliquez sur "Suivant"

#### Ajouter des bibliothèques

Organisez vos fichiers médias dans des dossiers :

```
/home/votre_nom/Médias/
├── Films/
│   ├── Le Seigneur des Anneaux (2001).mkv
│   ├── Inception (2010).mp4
│   └── ...
├── Séries/
│   ├── Breaking Bad/
│   │   ├── Saison 01/
│   │   │   ├── Breaking Bad - S01E01.mkv
│   │   │   └── ...
│   │   └── Saison 02/
│   └── ...
├── Musique/
│   ├── Artiste 1/
│   │   └── Album/
│   └── ...
└── Photos/
    ├── Vacances 2023/
    └── ...
```

**Conventions de nommage importantes :**
- **Films :** `Titre (Année).extension`
- **Séries :** `Nom Série - S01E01.extension` (S = Saison, E = Épisode)

Dans Plex, cliquez sur **"Ajouter une bibliothèque"** :

1. Choisissez le type : Films, Séries TV, Musique, Photos
2. Cliquez sur "Parcourir les dossiers"
3. Sélectionnez le dossier contenant vos médias
4. Cliquez sur "Ajouter"

Plex va scanner vos fichiers et télécharger automatiquement :
- Affiches et images d'arrière-plan
- Synopsis et descriptions
- Notes et évaluations
- Acteurs et équipe technique

### Optimiser les permissions

Plex s'exécute sous l'utilisateur `plex`. Donnez-lui accès à vos médias :

```bash
sudo usermod -aG votre_nom plex
sudo chmod 755 /home/votre_nom
sudo chmod -R 755 /home/votre_nom/Médias
```

Redémarrez Plex :

```bash
sudo systemctl restart plexmediaserver
```

### Configurer le pare-feu

```bash
sudo ufw allow 32400/tcp
```

---

## Installation de Jellyfin

### Méthode 1 : Installation via le dépôt officiel (recommandée)

#### Ajouter le dépôt Jellyfin

Installez les prérequis :

```bash
sudo apt install apt-transport-https
```

Ajoutez la clé GPG :

```bash
wget -O- https://repo.jellyfin.org/jellyfin_team.gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/jellyfin-archive-keyring.gpg >/dev/null
```

Ajoutez le dépôt :

```bash
echo "deb [signed-by=/usr/share/keyrings/jellyfin-archive-keyring.gpg arch=$( dpkg --print-architecture )] https://repo.jellyfin.org/$( awk -F'=' '/^ID=/{ print $NF }' /etc/os-release ) $( awk -F'=' '/^VERSION_CODENAME=/{ print $NF }' /etc/os-release ) main" | sudo tee /etc/apt/sources.list.d/jellyfin.list
```

Installez Jellyfin :

```bash
sudo apt update
sudo apt install jellyfin
```

#### Démarrer Jellyfin

```bash
sudo systemctl start jellyfin
sudo systemctl enable jellyfin
```

Vérifiez :

```bash
sudo systemctl status jellyfin
```

### Méthode 2 : Installation via le fichier .deb

Téléchargez depuis [jellyfin.org/downloads](https://jellyfin.org/downloads):

```bash
cd ~/Téléchargements
wget https://repo.jellyfin.org/releases/server/ubuntu/stable/server/jellyfin-server_10.8.13+deb12_amd64.deb
wget https://repo.jellyfin.org/releases/server/ubuntu/stable/web/jellyfin-web_10.8.13+deb12_all.deb
```

Installez :

```bash
sudo dpkg -i jellyfin-*.deb
sudo apt-get install -f
```

### Configuration initiale de Jellyfin

#### Accéder à l'interface web

Ouvrez votre navigateur :

```
http://localhost:8096
```

ou

```
http://votre_ip:8096
```

#### Assistant de configuration

1. **Choisir la langue** : Français

2. **Créer un compte administrateur**
   - Nom d'utilisateur : votre choix
   - Mot de passe : choisissez un mot de passe fort
   - **Important :** Contrairement à Plex, ce compte est local, pas sur Internet

3. **Ajouter des bibliothèques médias**
   - Cliquez sur "Ajouter une bibliothèque multimédia"
   - Type de contenu : Films, Séries, Musique, Photos, etc.
   - Dossiers : Sélectionnez votre dossier de médias
   - Langue des métadonnées : Français

4. **Langue des métadonnées préférée** : Français

5. **Configuration à distance**
   - Activez si vous voulez accéder depuis Internet
   - Désactivez si utilisation locale uniquement

6. Cliquez sur "Terminer"

### Optimiser les permissions pour Jellyfin

Jellyfin s'exécute sous l'utilisateur `jellyfin` :

```bash
sudo usermod -aG votre_nom jellyfin
sudo chmod 755 /home/votre_nom
sudo chmod -R 755 /home/votre_nom/Médias
```

Redémarrez Jellyfin :

```bash
sudo systemctl restart jellyfin
```

### Configurer le pare-feu

```bash
sudo ufw allow 8096/tcp
```

---

## Organisation de votre bibliothèque média

### Structure de dossiers recommandée

```
/home/votre_nom/Médias/
├── Films/
│   ├── Action/
│   ├── Comédie/
│   ├── Documentaires/
│   └── Science-Fiction/
├── Séries/
│   ├── Breaking Bad/
│   │   ├── Saison 01/
│   │   ├── Saison 02/
│   │   └── ...
│   └── Game of Thrones/
├── Musique/
│   ├── Rock/
│   ├── Jazz/
│   └── Classique/
├── Photos/
│   ├── 2023/
│   └── 2024/
└── Livres Audio/
```

### Conventions de nommage

#### Films

**Format recommandé :**
```
Titre du Film (Année).extension
```

**Exemples :**
```
Inception (2010).mkv
Le Parrain (1972).mp4
Intouchables (2011).avi
```

**Avec qualité et source (optionnel) :**
```
Avatar (2009) [1080p BluRay].mkv
Matrix (1999) [4K HDR].mkv
```

#### Séries TV

**Format recommandé :**
```
Nom de la Série/Saison XX/Nom de la Série - SXXEXX - Titre Episode.extension
```

**Exemples :**
```
Breaking Bad/
├── Saison 01/
│   ├── Breaking Bad - S01E01 - Pilot.mkv
│   ├── Breaking Bad - S01E02 - Cat's in the Bag.mkv
│   └── ...
└── Saison 02/
    └── ...
```

**Format alternatif (compatible) :**
```
Breaking Bad - S01E01.mkv
Breaking Bad - 1x01.mkv
```

#### Musique

**Format recommandé :**
```
Artiste/Album (Année)/Numéro - Titre.extension
```

**Exemple :**
```
Pink Floyd/
└── The Dark Side of the Moon (1973)/
    ├── 01 - Speak to Me.mp3
    ├── 02 - Breathe.mp3
    └── ...
```

### Métadonnées et pochettes

#### Affiches personnalisées

Placez une image nommée `poster.jpg` ou `folder.jpg` dans le dossier du film/série :

```
Inception (2010)/
├── Inception (2010).mkv
└── poster.jpg
```

#### Fichiers NFO (métadonnées)

Créez un fichier `.nfo` avec les informations :

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<movie>
    <title>Inception</title>
    <year>2010</year>
    <plot>Dom Cobb est un voleur expérimenté...</plot>
    <rating>8.8</rating>
</movie>
```

---

## Accès depuis différents appareils

### Ordinateur (navigateur web)

**Plex :**
```
http://votre_ip:32400/web
```

**Jellyfin :**
```
http://votre_ip:8096
```

### Smart TV

#### Plex
- Téléchargez l'application Plex depuis le store de votre TV (Samsung, LG, Android TV, etc.)
- Connectez-vous avec votre compte Plex
- Votre serveur apparaîtra automatiquement

#### Jellyfin
- **Android TV :** Téléchargez depuis le Play Store
- **Samsung/LG :** Pas d'application officielle, utilisez le navigateur web
- **Apple TV :** Application disponible sur l'App Store

### Smartphone et tablette

#### Android

**Plex :** [Play Store - Plex](https://play.google.com/store/apps/details?id=com.plexapp.android)
**Jellyfin :** [Play Store - Jellyfin](https://play.google.com/store/apps/details?id=org.jellyfin.mobile)

#### iOS

**Plex :** [App Store - Plex](https://apps.apple.com/app/plex/id383457673)
**Jellyfin :** [App Store - Jellyfin](https://apps.apple.com/app/jellyfin-mobile/id1480192618)

### Box TV et lecteurs média

- **Roku :** Application Plex et Jellyfin disponibles
- **Fire TV :** Applications disponibles
- **Chromecast :** Castez depuis l'application mobile
- **Kodi :** Plugin Plex et Jellyfin disponibles

### Console de jeux

- **PlayStation :** Application Plex disponible (PS4, PS5)
- **Xbox :** Application Plex disponible

---

## Transcoding et performances

### Qu'est-ce que le transcoding ?

Le transcoding convertit vos vidéos à la volée pour qu'elles soient compatibles avec votre appareil de lecture.

**Exemple :** Votre fichier est en 4K mais votre smartphone ne peut lire que du 1080p. Le serveur convertit en temps réel.

### Transcoding matériel vs logiciel

#### Transcoding logiciel (CPU)
- Utilise le processeur
- Compatible avec tous les processeurs
- Plus lent et consomme beaucoup de ressources
- Gratuit

#### Transcoding matériel (GPU)
- Utilise la carte graphique
- Beaucoup plus rapide et efficace
- Nécessite une carte graphique compatible (Intel QuickSync, NVIDIA NVENC, AMD VCE)
- **Plex :** Nécessite Plex Pass
- **Jellyfin :** Gratuit

### Activer le transcoding matériel

#### Plex (avec Plex Pass)

1. Paramètres → Transcoder
2. Activez "Utiliser l'accélération matérielle si disponible"
3. Choisissez votre GPU

#### Jellyfin

1. Tableau de bord → Lecture
2. Activez "Activer l'encodage accéléré par le matériel"
3. Sélectionnez votre type de GPU (VAAPI pour Intel/AMD, NVENC pour NVIDIA)

### Configuration requise

**Pour lecture directe (pas de transcoding) :**
- Processeur double cœur
- 2 GB RAM
- Connexion réseau stable

**Pour 1-2 streams avec transcoding :**
- Processeur quad-core (4 cœurs)
- 4 GB RAM
- GPU compatible (recommandé)

**Pour 3+ streams simultanés :**
- Processeur 6-8 cœurs ou GPU puissant
- 8 GB RAM minimum
- SSD pour la bibliothèque

### Optimiser les performances

#### Prétraiter vos vidéos

Utilisez HandBrake pour convertir vos vidéos dans un format compatible avant de les ajouter :

```bash
sudo apt install handbrake
```

Format recommandé :
- Conteneur : MP4 ou MKV
- Vidéo : H.264 ou H.265 (HEVC)
- Audio : AAC ou AC3

#### Utiliser un SSD

Stockez votre bibliothèque sur un SSD plutôt qu'un disque dur pour de meilleures performances.

#### Limiter le nombre de streams simultanés

Dans Plex/Jellyfin, limitez le nombre de lectures simultanées pour préserver les performances.

---

## Accès distant (depuis Internet)

### Attention aux risques

Exposer votre serveur média à Internet comporte des risques :
- Consommation de bande passante
- Possible violation de droits d'auteur si vous partagez avec d'autres
- Sécurité de votre réseau

**Recommandation :** Utilisez toujours HTTPS et des mots de passe forts.

### Plex - Accès distant

#### Configuration automatique (recommandée)

Plex configure automatiquement l'accès distant via leurs serveurs :

1. Paramètres → Réseau
2. Activez "Montrer les paramètres avancés"
3. Vérifiez "Activer l'accès à distance"

Plex tentera de configurer automatiquement la redirection de port (UPnP).

#### Configuration manuelle

Si la configuration automatique échoue :

1. Accédez à votre box (192.168.1.1 généralement)
2. Configurez une redirection de port :
   - Port externe : 32400
   - Port interne : 32400
   - Protocole : TCP
   - IP : Adresse IP de votre serveur

3. Dans Plex :
   - Paramètres → Réseau
   - "Port externe défini manuellement" : 32400

#### Accès depuis l'extérieur

Connectez-vous simplement sur [app.plex.tv](https://app.plex.tv) avec votre compte. Votre serveur apparaîtra automatiquement !

### Jellyfin - Accès distant

Jellyfin ne dispose pas de serveurs relais comme Plex. Vous devez configurer manuellement.

#### Option 1 : Redirection de port simple

1. Configurez votre box pour rediriger le port 8096
2. Trouvez votre IP publique : `curl ifconfig.me`
3. Accédez via : `http://votre_ip_publique:8096`

**Problème :** Votre IP change régulièrement.

#### Option 2 : DDNS (recommandé)

Utilisez un service DDNS gratuit (voir chapitre 21.3) :

1. Configurez DuckDNS : `monserveur.duckdns.org`
2. Redirigez le port 8096 sur votre box
3. Accédez via : `http://monserveur.duckdns.org:8096`

#### Option 3 : VPN (le plus sécurisé)

Installez un serveur VPN (WireGuard, OpenVPN) sur votre réseau. Connectez-vous au VPN pour accéder à Jellyfin comme si vous étiez chez vous.

### Sécuriser avec HTTPS (SSL/TLS)

#### Plex

Plex utilise déjà HTTPS via ses serveurs. Pour un accès direct :

1. Obtenez un certificat Let's Encrypt
2. Paramètres → Réseau
3. "Chemins de certificat personnalisés"
4. Indiquez les chemins de votre certificat et clé

#### Jellyfin avec Reverse Proxy (Nginx)

Configuration recommandée pour HTTPS :

Installez Nginx :

```bash
sudo apt install nginx certbot python3-certbot-nginx
```

Configurez un virtual host :

```bash
sudo nano /etc/nginx/sites-available/jellyfin
```

Ajoutez :

```nginx
server {
    listen 80;
    server_name monserveur.duckdns.org;

    location / {
        proxy_pass http://localhost:8096;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_buffering off;
    }
}
```

Activez :

```bash
sudo ln -s /etc/nginx/sites-available/jellyfin /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

Obtenez un certificat SSL :

```bash
sudo certbot --nginx -d monserveur.duckdns.org
```

Maintenant, accédez via `https://monserveur.duckdns.org` !

---

## Plugins et extensions

### Plex

#### Activer les plugins

1. Paramètres → Plugins
2. Installez depuis le catalogue Plex

**Plugins populaires :**
- **WebTools** : Gestion avancée du serveur
- **Trakt.tv** : Synchronisation des vues avec Trakt
- **Sub-Zero** : Téléchargement automatique de sous-titres

#### Installer WebTools

```bash
cd "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Plug-ins"
sudo git clone https://github.com/ukdtom/WebTools.bundle.git
sudo systemctl restart plexmediaserver
```

Accédez à : `http://localhost:33400`

### Jellyfin

#### Installer des plugins

1. Tableau de bord → Plugins
2. Catalogue → Installer

**Plugins utiles :**
- **Open Subtitles** : Sous-titres automatiques
- **Trakt** : Suivi des épisodes regardés
- **Fanart** : Amélioration des images
- **Playback Reporting** : Statistiques de lecture
- **LDAP Authentication** : Authentification avancée

---

## Gestion des utilisateurs

### Plex

#### Créer des utilisateurs

1. Paramètres → Utilisateurs et partage → Amis Plex
2. Invitez par email
3. L'utilisateur reçoit une invitation et crée un compte Plex

#### Partager des bibliothèques

1. Sélectionnez l'utilisateur
2. Cochez les bibliothèques à partager
3. Définissez les restrictions (notes, labels)

#### Profils utilisateur

Créez des profils pour enfants avec restrictions de contenu :

1. Paramètres → Profils gérés
2. Créez un profil "Enfants"
3. Limitez aux contenus appropriés

### Jellyfin

#### Créer des utilisateurs

1. Tableau de bord → Utilisateurs
2. Ajouter un utilisateur
3. Définissez nom, mot de passe et bibliothèques accessibles

#### Permissions

Définissez finement les permissions :
- Lecture streaming
- Téléchargement de médias
- Suppression de médias
- Accès administrateur

#### Contrôle parental

1. Créez un utilisateur pour votre enfant
2. Activez le contrôle parental
3. Définissez les classifications autorisées

---

## Sous-titres

### Plex

#### Activer les sous-titres

1. Pendant la lecture, cliquez sur l'icône de sous-titres
2. Sélectionnez la langue

#### Télécharger automatiquement

Nécessite un plugin comme Sub-Zero ou OpenSubtitles.

### Jellyfin

#### Configurer OpenSubtitles

1. Tableau de bord → Plugins
2. Installez "Open Subtitles"
3. Configurez avec votre compte OpenSubtitles.org (gratuit)

#### Télécharger des sous-titres

1. Bibliothèque → Sélectionnez un film/épisode
2. "..." → "Rechercher des sous-titres"
3. Sélectionnez et téléchargez

---

## Surveillance et statistiques

### Plex

#### Tableau de bord

Accédez au tableau de bord pour voir :
- Qui regarde quoi en temps réel
- Bande passante utilisée
- Historique de lecture

#### Tautulli (anciennement PlexPy)

Application tierce pour statistiques avancées :

```bash
sudo apt install python3-pip
pip3 install plexapi
git clone https://github.com/Tautulli/Tautulli.git
cd Tautulli
python3 Tautulli.py
```

Accédez à : `http://localhost:8181`

### Jellyfin

#### Tableau de bord intégré

Tableau de bord → Activité

Affiche :
- Sessions actives
- Utilisateurs connectés
- Transcoding en cours

#### Plugin Playback Reporting

Installez le plugin pour des statistiques détaillées.

---

## Maintenance et optimisation

### Nettoyer la base de données

#### Plex

```bash
sudo systemctl stop plexmediaserver
sudo -u plex sqlite3 "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Plug-in Support/Databases/com.plexapp.plugins.library.db" "VACUUM;"
sudo systemctl start plexmediaserver
```

#### Jellyfin

Jellyfin nettoie automatiquement sa base de données.

### Rafraîchir les métadonnées

Si les affiches ou infos sont incorrectes :

**Plex :**
1. Clic droit sur le média → "Faire correspondre"
2. Sélectionnez la bonne correspondance

**Jellyfin :**
1. Sélectionnez le média → "Éditer les métadonnées"
2. "Actualiser les métadonnées"

### Sauvegarder la configuration

#### Plex

Sauvegardez le dossier :

```bash
sudo tar -czf plex-backup.tar.gz "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server"
```

#### Jellyfin

Sauvegardez :

```bash
sudo tar -czf jellyfin-backup.tar.gz /var/lib/jellyfin /etc/jellyfin
```

---

## Dépannage courant

### Serveur inaccessible

**Vérifiez le service :**

Plex :
```bash
sudo systemctl status plexmediaserver
```

Jellyfin :
```bash
sudo systemctl status jellyfin
```

**Redémarrez le service :**

```bash
sudo systemctl restart plexmediaserver  # ou jellyfin
```

### Médias non détectés

**Vérifiez les permissions :**

```bash
ls -la /home/votre_nom/Médias
```

Assurez-vous que `plex` ou `jellyfin` peut lire les fichiers :

```bash
sudo chmod -R 755 /home/votre_nom/Médias
```

**Forcez un scan :**

Plex : Bibliothèque → Scanner les fichiers de la bibliothèque
Jellyfin : Tableau de bord → Scanner la bibliothèque

### Métadonnées incorrectes

**Renommez correctement vos fichiers** selon les conventions.

**Forcez une correspondance manuelle.**

### Buffering / Lecture saccadée

**Causes possibles :**
- Transcoding trop demandant pour le CPU
- Connexion réseau faible
- Disque dur lent

**Solutions :**
- Activez le transcoding matériel
- Réduisez la qualité de lecture
- Utilisez un SSD
- Optimisez vos vidéos avec HandBrake

### "Serveur non disponible" en accès distant

**Plex :**
- Vérifiez les paramètres d'accès distant
- Testez la redirection de port

**Jellyfin :**
- Vérifiez la redirection de port sur votre box
- Vérifiez que le pare-feu autorise le port
- Testez avec votre IP publique

---

## Alternatives et compléments

### Autres serveurs médias

#### Kodi
- Centre multimédia complet
- S'installe sur chaque appareil (pas de serveur centralisé)
- Interface très personnalisable

#### Universal Media Server
- Simple et gratuit
- Compatible DLNA
- Moins de fonctionnalités que Plex/Jellyfin

#### Subsonic / Airsonic
- Spécialisé dans la musique
- Streaming audio léger

### Outils complémentaires

#### Sonarr / Radarr
- Gestion automatique de séries TV (Sonarr) et films (Radarr)
- Téléchargement automatique (si vous avez Usenet ou BitTorrent)
- S'intègre avec Plex et Jellyfin

#### Ombi
- Système de requêtes pour vos utilisateurs
- Les utilisateurs peuvent demander des films/séries
- Vous approuvez et ajoutez à votre bibliothèque

#### Tdarr
- Optimisation et transcoding de votre bibliothèque
- Convertit automatiquement vos vidéos dans des formats optimaux

---

## Comparaison finale Plex vs Jellyfin

| Critère | Plex | Jellyfin |
|---------|------|----------|
| **Prix** | Gratuit (limité) / Plex Pass payant | Totalement gratuit |
| **Open Source** | ❌ Non | ✅ Oui |
| **Compte requis** | ✅ Oui (obligatoire) | ❌ Non |
| **Interface** | ⭐⭐⭐⭐⭐ Excellente | ⭐⭐⭐⭐ Très bonne |
| **Applications** | ⭐⭐⭐⭐⭐ Tous les appareils | ⭐⭐⭐⭐ Majorité des appareils |
| **Transcoding** | ⭐⭐⭐⭐⭐ Excellent | ⭐⭐⭐⭐ Bon |
| **Métadonnées** | ⭐⭐⭐⭐⭐ Très précises | ⭐⭐⭐⭐ Bonnes |
| **Facilité** | ⭐⭐⭐⭐⭐ Très facile | ⭐⭐⭐⭐ Facile |
| **Confidentialité** | ⭐⭐⭐ Moyenne | ⭐⭐⭐⭐⭐ Excellente |
| **Performances** | ⭐⭐⭐⭐⭐ Optimisées | ⭐⭐⭐⭐ Bonnes |

### Recommandation finale

**Choisissez Plex si :**
- Vous voulez la meilleure expérience utilisateur
- Vous avez beaucoup d'appareils différents
- Vous êtes prêt à payer pour Plex Pass
- Vous ne vous souciez pas d'avoir un compte en ligne

**Choisissez Jellyfin si :**
- Vous valorisez l'open source et la confidentialité
- Vous ne voulez rien payer
- Vous voulez un contrôle total
- Vous êtes à l'aise avec un peu de configuration technique

**Conseil :** Installez les deux et testez pendant quelques jours pour voir lequel correspond le mieux à vos besoins !

---

## Conclusion

Vous êtes maintenant capable de transformer votre Linux Mint en un véritable serveur média professionnel !

**Points clés à retenir :**
1. Plex est plus facile et poli, Jellyfin est gratuit et libre
2. Organisez correctement vos fichiers médias (nommage crucial)
3. Le transcoding matériel améliore grandement les performances
4. Sécurisez toujours l'accès distant avec HTTPS
5. Les deux solutions sont excellentes, le choix dépend de vos priorités

**Prochaines étapes :**
- Organisez votre bibliothèque selon les conventions
- Testez l'accès depuis différents appareils
- Configurez le transcoding matériel si possible
- Explorez les plugins et extensions
- Partagez avec famille et amis (légalement !)

Profitez de votre propre Netflix maison ! 🎬🍿

---

## Ressources supplémentaires

### Documentation officielle
- Plex : [support.plex.tv](https://support.plex.tv/)
- Jellyfin : [jellyfin.org/docs/](https://jellyfin.org/docs/)

### Communautés
- r/PleX (Reddit)
- r/jellyfin (Reddit)
- Forums Plex et Jellyfin officiels

### Guides utiles
- Trash Guides : Conventions de nommage parfaites
- ServarrWiki : Automatisation avec Sonarr/Radarr
- TRaSH Guides : Optimisation des serveurs médias

Bon streaming ! 🎥

⏭️ [Virtualisation (VirtualBox, KVM/QEMU)](/21-serveurs-et-administration-systeme/05-virtualisation.md)
