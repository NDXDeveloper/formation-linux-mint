🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 10.4 Dropbox, OneDrive et autres

## Introduction

Après avoir exploré Nextcloud et Google Drive dans les chapitres précédents, nous allons maintenant découvrir d'autres services cloud populaires et leur compatibilité avec Linux Mint.

Dans ce chapitre, vous apprendrez à utiliser :
- **Dropbox** (client officiel disponible)
- **OneDrive** (solutions tierces nécessaires)
- **MEGA** (client officiel disponible)
- **pCloud** (client officiel disponible)
- **Autres services** (Proton Drive, Box, etc.)

---

## Dropbox

**Dropbox** est l'un des services cloud les plus anciens et populaires. C'est aussi l'un des rares à proposer un **client officiel pour Linux**.

### Caractéristiques principales

- ✅ **Client officiel Linux** disponible
- ✅ **Très stable** et éprouvé
- ✅ **Synchronisation rapide** et fiable
- ✅ **Partage facile** de fichiers et dossiers
- ✅ **Historique des versions** (30 jours gratuit, 180 jours payant)
- ✅ **Récupération de fichiers supprimés**

- ❌ **Seulement 2 Go gratuits** (extensible via parrainage)
- ❌ **Prix élevé** pour les formules payantes
- ❌ **Client Linux** parfois en retard sur les fonctionnalités

### Offres Dropbox

| Plan | Espace | Prix |
|------|--------|------|
| **Basic** | 2 Go | Gratuit |
| **Plus** | 2 To | ~11,99€/mois |
| **Professional** | 3 To | ~19,99€/mois |
| **Family** | 2 To (6 utilisateurs) | ~19,99€/mois |

**Astuce :** Obtenez 500 Mo supplémentaires par parrainage (jusqu'à 16 Go gratuits).

---

### Installation de Dropbox sur Linux Mint

#### Méthode 1 : Téléchargement depuis le site officiel (recommandé)

1. **Rendez-vous sur** : https://www.dropbox.com/install-linux
2. Téléchargez le fichier **.deb** pour Ubuntu
3. **Double-cliquez** sur le fichier téléchargé
4. Cliquez sur **Installer** dans le Gestionnaire de paquets
5. Entrez votre mot de passe administrateur

#### Méthode 2 : Via le terminal

```bash
# Télécharger le paquet Dropbox
cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -

# Lancer Dropbox (télécharge le daemon)
~/.dropbox-dist/dropboxd
```

Le client se télécharge automatiquement au premier lancement.

#### Méthode 3 : Via les dépôts officiels

```bash
# Ajouter le dépôt Dropbox
sudo sh -c 'echo "deb [arch=amd64] https://linux.dropbox.com/ubuntu jammy main" > /etc/apt/sources.list.d/dropbox.list'

# Ajouter la clé GPG
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1C61A2656FB57B7E4DE0F4C1FC918B335044912E

# Installer Dropbox
sudo apt update
sudo apt install dropbox
```

---

### Configuration initiale de Dropbox

1. **Lancement automatique**
   - Après installation, Dropbox se lance automatiquement
   - Sinon, cherchez "Dropbox" dans le menu

2. **Écran de connexion**
   - **Connexion** si vous avez déjà un compte
   - **Inscription** pour créer un nouveau compte

3. **Choix du forfait**
   - Sélectionnez **Basic (gratuit)** ou une offre payante
   - Vous pouvez toujours changer plus tard

4. **Sélection du dossier**
   - Par défaut : `/home/votre-nom/Dropbox`
   - Vous pouvez choisir un autre emplacement si souhaité
   - Cliquez sur **Suivant**

5. **Synchronisation sélective**

   Trois options :
   - **Sync everything** : Tout synchroniser (recommandé pour débuter)
   - **Sync only these folders** : Sélectionner des dossiers spécifiques
   - **Save space automatically** : Dropbox gère l'espace (fichiers à la demande)

6. **Tour guidé**
   - Dropbox vous montre les fonctionnalités de base
   - Suivez le tour ou passez-le

7. **Finalisation**
   - La synchronisation démarre automatiquement
   - Une icône Dropbox apparaît dans la barre d'état système

---

### Utilisation de Dropbox

#### Icône dans la barre d'état

L'icône Dropbox (en haut à droite) change selon l'état :

- 📁 **Blanc/Gris** : À jour, tout synchronisé
- 🔄 **Bleu avec flèches** : Synchronisation en cours
- ⚠️ **Rouge avec X** : Erreur de synchronisation
- ⏸️ **Pause** : Synchronisation en pause

**Clic sur l'icône** pour :
- 📊 Voir l'état de la synchronisation
- 📂 Ouvrir le dossier Dropbox
- ⏸️ Mettre en pause la synchronisation
- ⚙️ Accéder aux préférences
- 🌐 Ouvrir Dropbox sur le web

---

#### Le dossier Dropbox

Un dossier **Dropbox** est créé dans votre répertoire personnel.

**Fonctionnement :**
- Glissez des fichiers → Synchronisés automatiquement
- Modifications → Synchronisées en temps réel
- Suppressions → Synchronisées (fichiers en corbeille Dropbox 30 jours)

**Icônes de statut** (sur les fichiers) :
- ✅ **Coche verte** : Synchronisé
- 🔄 **Flèches circulaires** : En cours de synchronisation
- ❌ **Croix rouge** : Erreur
- ➖ **Tiret gris** : Ignoré (non synchronisé)

---

#### Partage de fichiers et dossiers

**Partager un fichier/dossier :**

1. **Clic droit** sur un fichier ou dossier dans Dropbox
2. Sélectionnez **Dropbox** → **Share...**
3. Interface web qui s'ouvre avec options :
   - **Créer un lien** : Lien public de partage
   - **Inviter des personnes** : Par email avec permissions
   - **Voir qui a accès** : Gérer les accès existants

**Types de partage :**
- 🔗 **Lien partagé** : Accès en lecture seule
- 👥 **Dossier partagé** : Collaboration avec édition
- 🔒 **Lien protégé par mot de passe** (uniquement formules payantes)

---

#### Fonctionnalités utiles

##### 📋 **Copier le lien Dropbox**
- Clic droit → **Dropbox** → **Copy Dropbox Link**
- Crée instantanément un lien partageable

##### 📜 **Historique des versions**
- Interface web → Cliquez sur un fichier → **Version history**
- Restaurez une version précédente (30 jours gratuit)

##### 🗑️ **Récupérer des fichiers supprimés**
- Interface web → **Fichiers supprimés**
- Restaurez dans les 30 jours (180 jours avec formule payante)

##### 📸 **Importation automatique de photos**
- Connectez votre smartphone
- Dropbox propose d'importer automatiquement vos photos
- Gagnez 3 Go gratuits avec Camera Upload

---

### Paramètres avancés de Dropbox

**Accès :** Icône Dropbox → ⚙️ **Preferences**

#### Onglet General
- ✅ **Start Dropbox on system startup** : Lancer au démarrage
- 📁 **Dropbox folder location** : Changer l'emplacement du dossier

#### Onglet Account
- 📊 Voir l'espace utilisé
- 💳 Gérer l'abonnement
- 🔗 Lier/délier des appareils

#### Onglet Bandwidth
- 📥 **Download rate** : Limiter la vitesse de téléchargement
- 📤 **Upload rate** : Limiter la vitesse d'upload
- Utile pour ne pas saturer votre connexion

#### Onglet Sync (Synchronisation sélective)
- **Selective Sync** : Choisir les dossiers à synchroniser
- Décochez les dossiers que vous ne voulez pas en local
- Ils restent accessibles via l'interface web

#### Onglet Proxies
- Configuration proxy si nécessaire
- Pour réseaux d'entreprise

---

### Dropbox Smart Sync (formules payantes)

**Smart Sync** permet de voir tous vos fichiers sans les télécharger localement.

**Types de fichiers :**
- **En ligne uniquement** : Visible mais non téléchargé (économise de l'espace)
- **Local** : Toujours disponible hors ligne
- **Automatique** : Dropbox décide selon l'utilisation

⚠️ **Note :** Fonctionnalité réservée aux abonnés payants.

---

### Dépannage Dropbox

#### Problème : Dropbox ne démarre pas

**Solutions :**
1. Vérifiez si le processus tourne : `ps aux | grep dropbox`
2. Redémarrez Dropbox :
   ```bash
   dropbox stop
   dropbox start
   ```
3. Réinstallez le daemon :
   ```bash
   ~/.dropbox-dist/dropboxd
   ```

#### Problème : Icône absente de la barre d'état

**Cause :** Incompatibilité avec certains environnements de bureau.

**Solution :**
```bash
# Installer l'indicateur système
sudo apt install libappindicator1

# Redémarrer Dropbox
dropbox stop && dropbox start
```

#### Problème : Synchronisation lente

**Solutions :**
1. Vérifiez votre connexion Internet
2. Limitez les téléchargements/uploads simultanés (Preferences → Bandwidth)
3. Évitez de synchroniser des milliers de petits fichiers
4. Vérifiez que Dropbox n'est pas en pause

#### Problème : Fichiers en conflit

Format : `fichier (conflit copie de Nom DATE).ext`

**Cause :** Fichier modifié simultanément sur plusieurs appareils

**Solution :** Fusionnez manuellement les versions et supprimez les doublons

---

## OneDrive (Microsoft)

**OneDrive** est le service cloud de Microsoft, intégré à Windows et Microsoft 365.

⚠️ **Microsoft ne propose PAS de client officiel pour Linux.**

### Caractéristiques

- ✅ **5 Go gratuits**
- ✅ **1 To avec Microsoft 365** (abonnement)
- ✅ **Intégration Microsoft Office** en ligne
- ✅ **Partage facile**

- ❌ **Pas de client officiel Linux**
- ❌ **Nécessite des solutions tierces**

---

### Solutions pour OneDrive sur Linux

#### Solution 1 : rclone (Gratuit)

**rclone** (vu au chapitre 10.3) supporte aussi OneDrive.

##### Configuration de OneDrive avec rclone

```bash
# Lancer la configuration
rclone config

# Créer un nouveau remote
n) New remote
name> onedrive

# Choisir le type
Storage> onedrive

# Client ID/Secret (laisser vide)
client_id> [Enter]
client_secret> [Enter]

# Choisir le type OneDrive
1 / OneDrive Personal or Business
2 / Sharepoint site
3 / Type search for a Sharepoint site
4 / Type in driveID
Choose: 1

# Auto config
Use auto config? y

# Se connecter dans le navigateur
# Autoriser rclone

# Choisir le drive
0 / OneDrive Personal
1 / OneDrive Business
Choose: 0

# Confirmer
y) Yes this is OK

# Quitter
q) Quit config
```

##### Utiliser OneDrive avec rclone

```bash
# Lister les fichiers
rclone ls onedrive:

# Synchroniser un dossier local vers OneDrive
rclone sync ~/Documents onedrive:Documents

# Synchronisation bidirectionnelle
rclone bisync ~/Documents onedrive:Documents
```

**Voir le chapitre 10.3** pour plus de détails sur rclone et l'automatisation.

---

#### Solution 2 : OneDrive-D (Client non officiel)

**OneDrive-D** est un client de synchronisation non officiel pour OneDrive.

⚠️ **Attention :** Projet communautaire, pas toujours à jour.

##### Installation

```bash
# Installer les dépendances
sudo apt install python3-pip

# Installer onedrive-d
pip3 install --user onedrive-d
```

##### Configuration

```bash
# Lancer la configuration
onedrive-d

# Suivre les instructions à l'écran
# Autoriser l'accès via le navigateur
```

**Note :** OneDrive-D peut être instable, rclone est plus fiable.

---

#### Solution 3 : OneDrive (abraunegg) - Recommandé

**OneDrive Client** d'abraunegg est le client Linux le plus abouti.

##### Installation

```bash
# Ajouter le dépôt
sudo add-apt-repository ppa:yann1ck/onedrive
sudo apt update

# Installer
sudo apt install onedrive
```

##### Configuration

```bash
# Première configuration
onedrive

# Autoriser l'accès (lien fourni dans le terminal)
# Collez l'URL de retour

# Synchroniser
onedrive --synchronize
```

##### Synchronisation automatique

```bash
# Activer le service systemd
systemctl --user enable onedrive
systemctl --user start onedrive

# Vérifier le statut
systemctl --user status onedrive
```

##### Configuration avancée

Fichier de configuration : `~/.config/onedrive/config`

```
# Synchronisation sélective
sync_dir = "~/OneDrive"
skip_file = "~*|.~*|*.tmp"
skip_dir = "Cache|Temp"
```

---

#### Solution 4 : Interface web uniquement

La solution la plus simple : utilisez **OneDrive via le navigateur web**.

1. Allez sur : https://onedrive.live.com
2. Connectez-vous avec votre compte Microsoft
3. Utilisez l'interface web pour :
   - Upload/download de fichiers
   - Édition de documents Office en ligne
   - Partage de fichiers

**Avantages :**
- ✅ Fonctionne partout
- ✅ Aucune installation
- ✅ Toujours à jour

**Inconvénients :**
- ❌ Pas de synchronisation automatique
- ❌ Pas de mode hors ligne
- ❌ Upload/download manuel

---

### Comparaison des solutions OneDrive

| Solution | Prix | Difficulté | Synchronisation | Fiabilité |
|----------|------|------------|-----------------|-----------|
| **rclone** | Gratuit | ⭐⭐⭐ | Manuelle/Script | ⭐⭐⭐⭐⭐ |
| **OneDrive (abraunegg)** | Gratuit | ⭐⭐ | Automatique | ⭐⭐⭐⭐ |
| **OneDrive-D** | Gratuit | ⭐⭐ | Automatique | ⭐⭐ |
| **Interface web** | Gratuit | ⭐ | Aucune | ⭐⭐⭐⭐⭐ |

**Recommandation :**
- **Débutants** → Interface web ou rclone avec RcloneBrowser
- **Utilisateurs avancés** → OneDrive (abraunegg) ou rclone automatisé

---

## MEGA

**MEGA** offre le plus généreux plan gratuit (20 Go) et un client officiel pour Linux.

### Caractéristiques

- ✅ **20 Go gratuits** (le plus généreux)
- ✅ **Client officiel Linux** (MEGAsync)
- ✅ **Chiffrement de bout en bout** (E2EE)
- ✅ **Bonne vitesse** de transfert
- ✅ **Respect de la vie privée**

- ❌ **Interface parfois moins intuitive**
- ❌ **Historique controversé** du fondateur

### Offres MEGA

| Plan | Espace | Prix |
|------|--------|------|
| **Free** | 20 Go | Gratuit |
| **Pro Lite** | 400 Go | ~4,99€/mois |
| **Pro I** | 2 To | ~9,99€/mois |
| **Pro II** | 8 To | ~19,99€/mois |
| **Pro III** | 16 To | ~29,99€/mois |

---

### Installation de MEGA (MEGAsync)

#### Méthode 1 : Téléchargement depuis le site

1. Rendez-vous sur : https://mega.io/desktop
2. Téléchargez le fichier **.deb** pour Ubuntu
3. Double-cliquez sur le fichier téléchargé
4. Cliquez sur **Installer**

#### Méthode 2 : Via les dépôts officiels

```bash
# Ajouter le dépôt MEGA
wget -O - https://mega.nz/linux/repo/xUbuntu_22.04/Release.key | sudo apt-key add -
echo "deb https://mega.nz/linux/repo/xUbuntu_22.04/ ./" | sudo tee /etc/apt/sources.list.d/megasync.list

# Installer MEGAsync
sudo apt update
sudo apt install megasync
```

---

### Configuration de MEGA

1. **Lancer MEGAsync**
   - Menu → Internet → MEGAsync

2. **Connexion/Inscription**
   - Connectez-vous ou créez un compte
   - ⚠️ **Important :** Notez votre clé de récupération !

3. **Type d'installation**
   - **Installation complète** : Synchronisation bidirectionnelle
   - **Sélective** : Choisir les dossiers
   - Recommandé : Installation complète pour débuter

4. **Dossier local**
   - Par défaut : `/home/votre-nom/MEGA`
   - Personnalisable

5. **Dossier distant**
   - Choisissez les dossiers MEGA à synchroniser
   - Ou synchronisez tout

6. **Finalisation**
   - La synchronisation démarre
   - Icône MEGA dans la barre d'état

---

### Utilisation de MEGA

#### Interface de MEGAsync

**Icône dans la barre d'état :**
- Clic sur l'icône pour accéder à :
  - 📊 État de la synchronisation
  - 📁 Ouvrir le dossier MEGA
  - ⚙️ Paramètres
  - 🌐 Ouvrir MEGA dans le navigateur
  - ⏸️ Pause/Reprise

#### Fonctionnalités principales

##### 🔒 **Chiffrement de bout en bout**
- Vos fichiers sont chiffrés **avant** l'upload
- MEGA ne peut pas lire vos fichiers
- ⚠️ **Ne perdez jamais votre mot de passe !**

##### 🔗 **Partage sécurisé**
- Clic droit → **Get MEGA link**
- Liens chiffrés
- Protection par mot de passe disponible

##### 💬 **MEGAchat**
- Messagerie chiffrée intégrée
- Appels audio/vidéo
- Alternative à Zoom/WhatsApp

##### 📤 **MEGAcmd** (ligne de commande)
- Version terminal de MEGA
- Automatisation possible

---

### Paramètres MEGAsync

**Accès :** Icône MEGA → **Settings**

#### General
- ✅ **Start on startup** : Lancement automatique
- 🔔 **Notifications**
- 🌐 **Langue**

#### Syncs
- Ajouter/modifier des synchronisations
- Synchronisation sélective
- Gestion des exclusions

#### Bandwidth
- Limiter upload/download
- Planification de bande passante

#### Advanced
- Proxy settings
- Cache size
- Network settings

---

## pCloud

**pCloud** est un service cloud suisse avec option d'achat à vie (pas d'abonnement).

### Caractéristiques

- ✅ **10 Go gratuits**
- ✅ **Client Linux natif**
- ✅ **Achat à vie** disponible (pas d'abonnement)
- ✅ **Serveurs en Europe** (Suisse)
- ✅ **Chiffrement client** disponible (pCloud Crypto - payant)

- ❌ **Crypto est payant en supplément**
- ❌ **Prix d'achat élevé** (mais unique)

### Offres pCloud

| Plan | Espace | Prix |
|------|--------|------|
| **Free** | 10 Go | Gratuit |
| **Premium** | 500 Go | ~49,99€/an ou 175€ à vie |
| **Premium Plus** | 2 To | ~99,99€/an ou 350€ à vie |
| **+ Crypto** | Chiffrement | +125€ à vie |

**Intéressant :** Option d'achat à vie pour éviter les abonnements mensuels.

---

### Installation de pCloud

#### Téléchargement

1. Rendez-vous sur : https://www.pcloud.com/download-free-online-cloud-file-storage.html
2. Téléchargez **pCloud Drive** pour Linux
3. Fichier **AppImage** (portable)

#### Installation et lancement

```bash
# Rendre le fichier exécutable
chmod +x pcloud*.AppImage

# Lancer pCloud
./pcloud*.AppImage
```

**Optionnel : Créer un raccourci**

```bash
# Déplacer dans un dossier accessible
sudo mv pcloud*.AppImage /opt/pcloud

# Créer un lien symbolique
sudo ln -s /opt/pcloud /usr/local/bin/pcloud

# Lancer avec : pcloud
```

---

### Configuration de pCloud

1. **Connexion**
   - Email et mot de passe
   - Ou inscription

2. **Mode de fonctionnement**

   **pCloud Drive** fonctionne comme un **disque virtuel** :
   - Les fichiers restent dans le cloud
   - Téléchargés à la demande quand vous les ouvrez
   - Économise beaucoup d'espace disque

3. **Synchronisation optionnelle**
   - Vous pouvez aussi créer des dossiers synchronisés
   - Similaire à Dropbox/MEGA

4. **Point de montage**
   - Par défaut : `~/pCloudDrive`
   - Apparaît comme un disque externe dans le gestionnaire de fichiers

---

### Utilisation de pCloud

#### pCloud Drive (Virtual Drive)

**Avantage principal :** Tous vos fichiers visibles, espace disque minimal utilisé.

**Fonctionnement :**
- Parcourez vos fichiers comme s'ils étaient locaux
- Ouvrez un fichier → Téléchargé automatiquement
- Modifiez → Uploadé automatiquement
- Fermez → Peut être supprimé localement (reste dans le cloud)

#### pCloud Sync (Synchronisation classique)

**Si vous préférez la synchronisation traditionnelle :**
1. Settings → **Sync**
2. Créez une synchronisation
3. Choisissez dossier local ↔ dossier cloud

---

### pCloud Crypto (Chiffrement)

**pCloud Crypto** chiffre vos fichiers côté client avant upload.

**Fonctionnalités :**
- Dossier **Crypto** séparé
- Chiffrement AES-256
- Clé de chiffrement uniquement chez vous
- ⚠️ Payant : +125€ à l'achat

**Note :** Même sans Crypto, pCloud chiffre les fichiers sur leurs serveurs (mais ils ont les clés).

---

## Autres services cloud

### Proton Drive

**Service axé sur la confidentialité** de Proton (créateurs de ProtonMail).

**Caractéristiques :**
- ✅ Chiffrement de bout en bout
- ✅ Basé en Suisse
- ✅ 5 Go gratuits
- ❌ Pas encore de client Linux natif (en développement)
- ❌ Accès web uniquement pour l'instant

**Utilisation actuelle sur Linux :**
- Interface web : https://drive.proton.me
- Client Linux : En développement (2024-2025)

**Recommandation :** Attendez le client Linux ou utilisez l'interface web.

---

### Box

**Service cloud professionnel** populaire en entreprise.

**Caractéristiques :**
- ✅ 10 Go gratuits
- ✅ Excellente collaboration
- ❌ Pas de client officiel Linux
- ❌ Orienté entreprise

**Solutions pour Linux :**
- Interface web : https://www.box.com
- rclone : Support natif de Box
- WebDAV : Montage via le gestionnaire de fichiers

---

### Koofr

**Service cloud européen** (Slovénie).

**Caractéristiques :**
- ✅ 10 Go gratuits
- ✅ Client Linux (AppImage)
- ✅ Agrégateur : Connectez Google Drive, OneDrive, Dropbox
- ✅ Respectueux de la vie privée

**Installation :**
1. Téléchargez sur : https://koofr.eu/desktop
2. AppImage pour Linux

---

### Tresorit

**Cloud ultra-sécurisé** pour professionnels.

**Caractéristiques :**
- ✅ Chiffrement de bout en bout
- ✅ Client Linux natif
- ❌ Pas d'offre gratuite
- ❌ Très cher (~10€/mois minimum)

**Utilisation :** Réservé aux besoins professionnels de haute sécurité.

---

### Resilio Sync (ex-BitTorrent Sync)

**Synchronisation peer-to-peer** (pas de serveur central).

**Caractéristiques :**
- ✅ Gratuit pour usage personnel
- ✅ Pas de limite de stockage
- ✅ Client Linux
- ✅ Synchronisation directe entre appareils
- ❌ Pas de stockage cloud externe

**Similaire à :** Syncthing (vu au chapitre 10.5)

---

## Tableau comparatif global

| Service | Client Linux | Gratuit | Facilité | Vie privée | Recommandé |
|---------|--------------|---------|----------|------------|------------|
| **Dropbox** | ✅ Officiel | 2 Go | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ✅ Oui |
| **OneDrive** | ❌ Tiers | 5 Go | ⭐⭐ | ⭐⭐ | ⚠️ Avec réserves |
| **MEGA** | ✅ Officiel | 20 Go | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ✅ Oui |
| **pCloud** | ✅ Officiel | 10 Go | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ✅ Oui |
| **Proton Drive** | ❌ Web | 5 Go | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⏳ Bientôt |
| **Box** | ❌ Web/rclone | 10 Go | ⭐⭐ | ⭐⭐⭐ | ⚠️ Entreprise |
| **Koofr** | ✅ AppImage | 10 Go | ⭐⭐⭐ | ⭐⭐⭐⭐ | ✅ Oui |
| **Tresorit** | ✅ Officiel | ❌ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | 💼 Pro uniquement |

---

## Stratégies d'utilisation multi-cloud

### Pourquoi utiliser plusieurs services ?

1. **Espace total augmenté** : 2 Go + 5 Go + 20 Go = 37 Go gratuits !
2. **Redondance** : Si un service tombe, vous avez des copies ailleurs
3. **Spécialisation** : Chaque service pour un usage différent

### Exemples de stratégies

#### Stratégie 1 : Séparation par type de données

- **Dropbox** → Documents professionnels (partage facile)
- **MEGA** → Sauvegardes personnelles (20 Go, chiffrement)
- **Google Drive** → Photos et collaboration (Google Docs)

#### Stratégie 2 : Redondance maximale

- Fichiers importants → Synchronisés sur 2-3 services différents
- Utiliser rclone pour copier automatiquement entre services

#### Stratégie 3 : Économique

- MEGA (20 Go gratuits) comme stockage principal
- Dropbox pour partages professionnels
- Interface web pour OneDrive (Microsoft 365 gratuit)

---

## Gestion multi-cloud avec rclone

**rclone** peut synchroniser entre plusieurs services cloud !

### Exemple : Sauvegarder Dropbox sur MEGA

```bash
# Copier de Dropbox vers MEGA
rclone copy dropbox: mega:Backup_Dropbox

# Synchroniser bidirectionnellement
rclone sync dropbox:Documents mega:Documents_Backup
```

### Exemple : Agrégateur de clouds

Montez tous vos clouds comme un seul système de fichiers :

```bash
# Installer rclone mount
sudo apt install fuse

# Monter tous les clouds
rclone mount --daemon multi-cloud: ~/CloudsUnified
```

Créez un remote `multi-cloud` qui combine plusieurs services.

---

## Conseils de sécurité

### 🔒 Authentification à deux facteurs (2FA)

**Activez 2FA sur tous vos services cloud !**

- Dropbox : Settings → Security → Two-step verification
- MEGA : Settings → Security → Two-Factor Authentication
- pCloud : Settings → Security → 2-Step Verification
- OneDrive : Compte Microsoft → Sécurité → Vérification en deux étapes

### 🔑 Gestionnaire de mots de passe

Utilisez des mots de passe **uniques et forts** pour chaque service.

**Gestionnaires recommandés :**
- **Bitwarden** (open source, gratuit)
- **KeePassXC** (local, gratuit)
- **1Password** (payant, excellent)

### 🔐 Chiffrement

Pour les données sensibles :
1. **Chiffrez avant upload** (VeraCrypt, LUKS)
2. Utilisez des services avec E2EE (MEGA, Proton Drive)
3. Utilisez pCloud Crypto ou rclone crypt

### 🗂️ Ne stockez jamais en clair

❌ Évitez de stocker :
- Mots de passe
- Informations bancaires
- Documents d'identité (sans chiffrement)
- Clés privées SSH/GPG

---

## Bonnes pratiques

### 📁 Organisation

1. **Structure claire** de dossiers
2. **Nommage cohérent** des fichiers
3. **Ne stockez pas tout** (soyez sélectif)

### 💾 Sauvegarde

**Le cloud n'est PAS une sauvegarde complète !**

**Règle 3-2-1 :**
- **3** copies de vos données
- Sur **2** supports différents
- **1** copie hors site (cloud)

**Exemple :**
1. PC principal
2. Disque dur externe (Timeshift, rsync)
3. Cloud (Dropbox, MEGA)

### 🔄 Synchronisation sélective

Ne synchronisez pas :
- ❌ Machines virtuelles (fichiers énormes)
- ❌ node_modules, .git (développement)
- ❌ Cache, fichiers temporaires
- ❌ Dossiers système

### 📊 Surveillance de l'espace

1. Vérifiez régulièrement l'espace utilisé
2. Nettoyez les vieux fichiers
3. Videz les corbeilles cloud
4. Compressez les archives anciennes

---

## Dépannage général

### Problème : Synchronisation lente

**Solutions universelles :**
1. Vérifiez votre connexion Internet (speedtest)
2. Limitez la bande passante dans les paramètres
3. Évitez de synchroniser beaucoup de petits fichiers
4. Vérifiez qu'aucun autre transfert n'est en cours

### Problème : Fichiers ne se synchronisent pas

**Vérifications :**
1. ✅ Connexion Internet active
2. ✅ Service cloud non en pause
3. ✅ Espace disponible (cloud et local)
4. ✅ Nom de fichier valide (pas de caractères interdits)
5. ✅ Pas de fichiers verrouillés/ouverts

### Problème : Quota dépassé

**Solutions :**
1. Libérez de l'espace (supprimez des fichiers)
2. Videz la corbeille du service cloud
3. Passez à une offre payante
4. Utilisez plusieurs services gratuits

### Problème : Conflits de fichiers

**Prévention :**
1. Évitez de modifier le même fichier simultanément
2. Attendez la fin de la synchronisation avant de modifier
3. Utilisez la collaboration en temps réel (Google Docs, Office Online)

**Résolution :**
1. Comparez les versions en conflit
2. Fusionnez manuellement
3. Supprimez les doublons

---

## Optimisation des performances

### Conseils généraux

1. **SSD recommandé** pour les dossiers synchronisés
2. **RAM suffisante** (les clients cloud consomment de la mémoire)
3. **Bande passante adéquate** (surtout upload)
4. **Évitez trop de clients simultanés** (max 2-3)

### Limiter la consommation de ressources

```bash
# Limiter CPU (avec nice)
nice -n 19 dropbox start

# Limiter RAM (avec cgroups - avancé)
systemd-run --user --scope -p MemoryLimit=500M dropbox start
```

---

## Alternatives pour besoins spécifiques

### Pour développeurs

**GitHub** : Gratuit, illimité pour code
**GitLab** : Alternative avec CI/CD intégré
**Bitbucket** : Intégration Atlassian

### Pour photos

**Google Photos** : Stockage gratuit (qualité réduite)
**Amazon Photos** : Illimité avec Prime
**Flickr** : 1000 photos gratuites

### Pour backup uniquement

**Backblaze B2** : Très économique (0,005$/Go/mois)
**Wasabi** : Pas de frais de sortie
**Borg Backup** + serveur personnel : Contrôle total

---

## Ressources utiles

### Documentation officielle

- Dropbox Help : https://help.dropbox.com
- MEGA Help : https://help.mega.io
- pCloud Support : https://www.pcloud.com/help
- rclone Docs : https://rclone.org/docs

### Communauté

- Forum Linux Mint : https://forums.linuxmint.com
- r/linux (Reddit) : Discussions cloud
- r/selfhosted : Alternatives auto-hébergées

### Outils complémentaires

- **Insync** : Pour Google Drive/OneDrive (payant mais excellent)
- **RcloneBrowser** : GUI pour rclone
- **Maestral** : Client Dropbox léger et open source (alternatif)

---

## Conclusion

**Pour Linux Mint, les meilleurs choix sont :**

🥇 **MEGA** : 20 Go gratuits, client natif, chiffrement E2EE, excellent pour Linux
🥈 **Dropbox** : Client officiel stable, familier, mais seulement 2 Go gratuits
🥉 **pCloud** : 10 Go gratuits, achat à vie intéressant, bon compromis

**Pour OneDrive :** Utilisez rclone ou le client abraunegg si vous avez déjà un abonnement Microsoft 365.

**Pour Google Drive :** Voir chapitre 10.3 (Insync ou rclone).

**Stratégie recommandée :**
- Utilisez **MEGA** comme stockage principal (20 Go gratuits)
- Ajoutez **Dropbox** pour collaboration professionnelle
- Complétez avec **Google Drive** si vous utilisez l'écosystème Google
- Total gratuit : **37 Go !**

**N'oubliez pas :** Le cloud est un **complément**, pas un **remplacement** des sauvegardes locales !

**Prochaine étape :** Chapitre 10.5 pour découvrir Syncthing et la synchronisation peer-to-peer entre vos propres appareils.

---

**Bon stockage cloud ! ☁️**

⏭️ [Synchronisation entre appareils (Syncthing)](/10-cloud-et-synchronisation/05-synchronisation-entre-appareils.md)
