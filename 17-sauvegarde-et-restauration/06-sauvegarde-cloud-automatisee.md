🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 17.6 Sauvegarde cloud automatisée

## Introduction

La sauvegarde cloud (dans le nuage) consiste à stocker vos données sur des serveurs distants via Internet. C'est un élément essentiel de la règle 3-2-1 : elle représente votre copie "hors site", protégée contre les catastrophes locales (incendie, vol, inondation).

### Qu'est-ce que le cloud ?

Le "cloud" (nuage en anglais) désigne simplement des serveurs informatiques situés ailleurs (datacenters professionnels) auxquels vous accédez via Internet. Vos fichiers sont stockés sur ces serveurs au lieu d'être uniquement sur votre ordinateur.

**Analogie simple :** C'est comme avoir un coffre-fort dans une banque (le datacenter) au lieu de tout garder chez vous. En cas de cambriolage chez vous, vos objets de valeur dans le coffre sont en sécurité.

### Pourquoi automatiser la sauvegarde cloud ?

**Le problème des sauvegardes manuelles :**
- On oublie de les faire régulièrement
- On reporte à plus tard
- On oublie quels fichiers ont été sauvegardés
- Les fichiers modifiés ne sont pas à jour

**Les avantages de l'automatisation :**
- ✅ Sauvegarde continue sans y penser
- ✅ Toujours à jour (synchronisation en temps réel)
- ✅ Versions multiples automatiques
- ✅ Accessible de n'importe où
- ✅ Protection contre perte/vol de l'ordinateur
- ✅ Partage facile avec d'autres appareils

### Avantages et inconvénients du cloud

**Avantages :**
- **Accessibilité** : Vos fichiers partout, sur tous vos appareils
- **Automatique** : Synchronisation transparente
- **Sécurité physique** : Datacenters professionnels (redondance, sécurité)
- **Versions multiples** : Historique des modifications
- **Hors site** : Protection contre catastrophes locales
- **Partage** : Collaboration facile
- **Pas de maintenance** : Pas de disques à gérer

**Inconvénients :**
- **Connexion Internet requise** : Pour synchroniser et accéder
- **Débit limité** : Upload peut être lent pour gros fichiers
- **Coût** : Abonnement pour stockage important
- **Confidentialité** : Vos données chez un tiers
- **Dépendance** : Au fournisseur et à sa disponibilité
- **Espace limité** : Souvent limité dans les offres gratuites

### Cloud vs sauvegarde locale

**Le cloud ne remplace PAS la sauvegarde locale, il la complète !**

| Critère | Cloud | Local (disque externe) |
|---------|-------|------------------------|
| Vitesse | Lente (dépend connexion) | Rapide |
| Accessibilité | Partout (Internet requis) | Physiquement présent |
| Coût | Abonnement récurrent | Achat unique |
| Hors site | ✅ Oui | ❌ Non (sauf si déplacé) |
| Vie privée | Dépend du service | ✅ Contrôle total |
| Capacité | Limitée (payant au-delà) | Importante (To) |

**Recommandation :** Utilisez les deux ! Cloud pour l'accessibilité et la protection hors site, disque local pour la vitesse et les gros volumes.

## Services cloud populaires

### Comparatif des principaux services

| Service | Gratuit | Payant | Chiffrement | Linux natif | Open Source |
|---------|---------|--------|-------------|-------------|-------------|
| **Google Drive** | 15 Go | À partir de 2€/mois (100 Go) | Oui (en transit) | Non officiel | ❌ |
| **Nextcloud** | Illimité (auto-hébergé) | Variable selon hébergeur | Oui (complet) | ✅ Excellent | ✅ |
| **Dropbox** | 2 Go | À partir de 10€/mois (2 To) | Oui | ✅ Bon | ❌ |
| **OneDrive** | 5 Go | À partir de 2€/mois (100 Go) | Oui | Non officiel | ❌ |
| **Mega** | 20 Go | À partir de 5€/mois (400 Go) | ✅ Bout en bout | ✅ | Partiellement |
| **pCloud** | 10 Go | Achat unique 175€ (500 Go) | Payant en plus | ✅ | ❌ |
| **Syncthing** | Illimité | Gratuit (P2P) | ✅ Bout en bout | ✅ Excellent | ✅ |

### Google Drive

**Points forts :**
- 15 Go gratuits (partagés avec Gmail et Photos)
- Intégration Google Workspace
- Très utilisé, fiable
- Applications mobiles excellentes

**Points faibles :**
- Pas de client officiel Linux
- Confidentialité (Google analyse les fichiers)
- Nécessite compte Google

**Qui devrait l'utiliser :**
- Utilisateurs déjà dans l'écosystème Google
- Besoin de collaboration (Google Docs, Sheets)
- Budget limité (15 Go gratuits)

### Nextcloud

**Points forts :**
- Open source, respect de la vie privée
- Auto-hébergeable (contrôle total)
- Client Linux natif excellent
- Nombreuses fonctionnalités (calendrier, contacts, notes, etc.)
- Chiffrement de bout en bout possible

**Points faibles :**
- Auto-hébergement nécessite compétences techniques
- Hébergement payant si vous ne l'auto-hébergez pas

**Qui devrait l'utiliser :**
- Utilisateurs soucieux de confidentialité
- Ceux qui veulent le contrôle total
- Besoin de fonctionnalités étendues
- Techniquement à l'aise (pour auto-hébergement)

### Dropbox

**Points forts :**
- Client Linux officiel et excellent
- Très stable et fiable
- Synchronisation rapide et efficace
- Historique 30 jours (gratuit) ou illimité (payant)

**Points faibles :**
- Seulement 2 Go gratuits (très limité)
- Prix élevé pour grandes capacités
- Politique de confidentialité discutable

**Qui devrait l'utiliser :**
- Besoin de stabilité maximale sous Linux
- Petits volumes de données
- Collaboration professionnelle

### OneDrive

**Points forts :**
- 5 Go gratuits
- Inclus avec Microsoft 365
- Bon pour utilisateurs Windows/Office

**Points faibles :**
- Pas de client officiel Linux
- Solutions tierces instables
- Pas idéal pour Linux pur

**Qui devrait l'utiliser :**
- Déjà abonné Microsoft 365
- Utilise Windows en dual-boot
- Pas recommandé comme solution principale Linux

### Mega

**Points forts :**
- 20 Go gratuits (généreux)
- Chiffrement de bout en bout
- Respect de la vie privée
- Client Linux disponible

**Points faibles :**
- Limites de transfert (gratuit)
- Interface parfois lente
- Historique du fondateur controversé

**Qui devrait l'utiliser :**
- Besoin de chiffrement fort
- Budget limité (20 Go gratuits)
- Gros fichiers occasionnels

### Syncthing

**Points forts :**
- Gratuit et open source
- Pas de serveur central (P2P)
- Confidentialité totale (vos appareils uniquement)
- Aucune limite de stockage
- Excellent sous Linux

**Points faibles :**
- Pas de serveur cloud (synchronise entre VOS appareils)
- Nécessite au moins 2 appareils allumés
- Configuration initiale plus technique

**Qui devrait l'utiliser :**
- Synchronisation entre ses propres appareils
- Confidentialité maximale
- Pas besoin d'accès web
- Aucune limite de stockage

## Configuration de la synchronisation automatique

### Nextcloud : La solution recommandée pour Linux

Nextcloud est le choix idéal pour Linux : open source, respectueux de la vie privée, et excellent support Linux.

#### Option 1 : Nextcloud hébergé (le plus simple)

**Fournisseurs d'hébergement Nextcloud :**
- Nextcloud.com (officiel) : à partir de 2-5€/mois
- OVH, Hetzner, et autres hébergeurs européens
- Chatons.org : hébergeurs associatifs français

**Avantages :** Pas de configuration serveur, support professionnel, sauvegardes automatiques.

#### Option 2 : Auto-hébergement (pour avancés)

Nécessite : serveur personnel, Raspberry Pi, ou VPS.

**Nous nous concentrons sur l'option hébergée pour les débutants.**

#### Installation du client Nextcloud

**1. Installation**

```bash
# Méthode 1 : AppImage (recommandé, toujours à jour)
# Téléchargez depuis https://nextcloud.com/install/#install-clients
# Rendez-le exécutable
chmod +x Nextcloud-*.AppImage
./Nextcloud-*.AppImage

# Méthode 2 : Dépôt officiel
sudo add-apt-repository ppa:nextcloud-devs/client  
sudo apt update  
sudo apt install nextcloud-desktop  

# Méthode 3 : Flatpak
flatpak install flathub com.nextcloud.desktopclient.nextcloud
```

**2. Premier lancement**

1. Lancez Nextcloud depuis le menu
2. Assistant de configuration s'ouvre

**3. Configuration du compte**

- **Server Address :** L'URL de votre Nextcloud (ex: https://cloud.example.com)
- Cliquez **Next**
- Connexion au navigateur s'ouvre
- **Connectez-vous** avec vos identifiants Nextcloud
- **Autorisez** l'accès
- Retournez au client desktop

**4. Configuration de la synchronisation**

- **Sync everything :** Synchroniser tout
- **Choose what to sync :** Sélectionner des dossiers spécifiques (recommandé)

**Recommandation pour débutants :**
```
✅ Documents
✅ Images
✅ Bureau
❌ Téléchargements (trop volumineux généralement)
❌ Vidéos (trop volumineuses, utilisez stockage local)
```

- **Local folder :** Où synchroniser localement
  - Par défaut : `~/Nextcloud`
  - Ou choisissez un autre emplacement

**5. Options avancées**

Cliquez sur **Advanced** pour :
- **Use virtual files :** Fichiers à la demande (ne télécharge que quand nécessaire)
- **Start on system startup :** Démarrer automatiquement (recommandé ✅)
- **Ask for confirmation before downloading folders larger than :** Alerte pour gros dossiers

**6. Finalisation**

- Cliquez **Connect**
- La synchronisation démarre automatiquement
- Icône Nextcloud apparaît dans la barre système

#### Utilisation quotidienne

**Synchronisation automatique :**
- Tout fichier placé dans `~/Nextcloud` est automatiquement uploadé
- Tout changement en ligne est téléchargé automatiquement
- Icône de la barre système montre le statut (✓ = synchronisé)

**Accéder à vos fichiers :**
- **Localement :** Ouvrez le dossier `~/Nextcloud` normalement
- **En ligne :** Via navigateur sur votre instance Nextcloud
- **Mobile :** Application Nextcloud iOS/Android

**Partage de fichiers :**
1. Clic droit sur fichier/dossier dans Nextcloud
2. **Nextcloud** → **Share**
3. Créez un lien de partage
4. Définissez permissions (lecture seule, modification, expiration)

**Gestion des versions :**
- Nextcloud garde automatiquement les versions précédentes
- Via interface web : clic droit → Versions
- Restaurez une version antérieure si besoin

#### Paramètres du client

Clic droit icône Nextcloud → **Settings**

**Onglet General :**
- Launch on system startup : ✅ Activé
- Show desktop notifications : ✅ Utile
- Use monochrome icons : Selon préférence

**Onglet Network :**
- Download bandwidth : Illimité (sauf connexion limitée)
- Upload bandwidth : Limité (pour ne pas saturer votre connexion)
  - Recommandé : 80% de votre upload maximum
  - Exemple : connexion 100 Mbps → limite à 80 Mbps

**Onglet Account :**
- Storage usage : Voir espace utilisé
- Enable virtual file support : Fichiers à la demande

### Google Drive avec rclone

Comme Google Drive n'a pas de client officiel Linux, nous utilisons rclone, un outil en ligne de commande puissant.

#### Installation de rclone

```bash
# Installation depuis les dépôts
sudo apt update  
sudo apt install rclone  

# Ou dernière version depuis le site officiel
curl https://rclone.org/install.sh | sudo bash
```

#### Configuration de Google Drive

**1. Lancer la configuration**

```bash
rclone config
```

**2. Créer une nouvelle configuration**

```
n) New remote
```
Appuyez sur **n** puis **Entrée**

**3. Nom de la configuration**

```
name> gdrive
```
Tapez un nom (exemple: gdrive) puis **Entrée**

**4. Type de stockage**

```
Storage>
```
Tapez **drive** (ou le numéro correspondant à Google Drive) puis **Entrée**

**5. Client ID et Secret**

```
client_id>  
client_secret>  
```
Laissez vides (appuyez juste **Entrée** pour les deux)

**6. Scope (permissions)**

```
scope> 1
```
Choisissez **1** (Full access) puis **Entrée**

**7. Service Account**

```
service_account_file>
```
Laissez vide, **Entrée**

**8. Configuration avancée**

```
Edit advanced config? (y/n)  
y/n> n  
```
**n** puis **Entrée**

**9. Autorisation**

```
Use auto config?  
y/n> n  
```

Répondez **n** si vous configurez sur un serveur sans interface graphique, **y** si sur votre desktop.

Si **y** :
- Un navigateur s'ouvre
- Connectez-vous à Google
- Autorisez rclone
- Revenez au terminal

Si **n** :
- Suivez les instructions pour autoriser depuis un autre appareil

**10. Configuration en équipe**

```
Configure this as a Shared Drive (Team Drive)?  
y/n> n  
```
**n** puis **Entrée** (sauf si vous utilisez Google Workspace)

**11. Confirmation**

```
y) Yes this is OK (default)  
e) Edit this remote  
d) Delete this remote  
y/e/d> y  
```
**y** puis **Entrée**

**12. Quitter**

```
e/n/d/r/c/s/q> q
```
**q** pour quitter

#### Utilisation de rclone avec Google Drive

**Lister les fichiers :**
```bash
rclone ls gdrive:
```

**Copier un fichier vers Google Drive :**
```bash
rclone copy /home/user/Documents/important.pdf gdrive:Documents/
```

**Synchroniser un dossier entier :**
```bash
# Synchronisation unidirectionnelle (local → cloud)
rclone sync /home/user/Documents gdrive:Documents

# ⚠️ ATTENTION : sync supprime les fichiers du cloud qui ne sont pas en local !
```

**Synchronisation bidirectionnelle (recommandé) :**
```bash
rclone bisync /home/user/Documents gdrive:Documents --resync

# Puis pour les syncs suivants :
rclone bisync /home/user/Documents gdrive:Documents
```

**Monter Google Drive comme dossier local :**
```bash
# Créez un point de montage
mkdir ~/GoogleDrive

# Montez Google Drive
rclone mount gdrive: ~/GoogleDrive &

# Maintenant ~/GoogleDrive contient vos fichiers Google Drive
# Accédez-y comme un dossier normal
```

Pour démonter :
```bash
fusermount -u ~/GoogleDrive
```

#### Automatisation avec rclone

**Créer un script de sauvegarde :**

```bash
nano ~/scripts/backup-gdrive.sh
```

Contenu du script :
```bash
#!/bin/bash

# Script de sauvegarde automatique vers Google Drive

# Configuration
SOURCE="/home/$USER/Documents"  
DESTINATION="gdrive:Sauvegardes/Documents"  
LOG_FILE="/home/$USER/.rclone-backup.log"  

# Date et heure
echo "===== Sauvegarde du $(date) =====" >> $LOG_FILE

# Synchronisation
rclone sync "$SOURCE" "$DESTINATION" \
    --progress \
    --log-file=$LOG_FILE \
    --log-level INFO \
    --exclude ".cache/**" \
    --exclude "*.tmp"

# Vérification
if [ $? -eq 0 ]; then
    echo "✓ Sauvegarde réussie" >> $LOG_FILE
    notify-send "Sauvegarde Google Drive" "Sauvegarde terminée avec succès"
else
    echo "✗ Erreur lors de la sauvegarde" >> $LOG_FILE
    notify-send -u critical "Sauvegarde Google Drive" "Erreur lors de la sauvegarde"
fi

echo "" >> $LOG_FILE
```

**Rendre le script exécutable :**
```bash
chmod +x ~/scripts/backup-gdrive.sh
```

**Tester le script :**
```bash
~/scripts/backup-gdrive.sh
```

**Automatiser avec cron (quotidien à 2h du matin) :**

```bash
crontab -e
```

Ajoutez :
```
0 2 * * * /home/VOTRENOM/scripts/backup-gdrive.sh
```

**Ou avec systemd timer (méthode moderne) :**

Créez le service :
```bash
nano ~/.config/systemd/user/gdrive-backup.service
```

Contenu :
```ini
[Unit]
Description=Google Drive Backup

[Service]
Type=oneshot  
ExecStart=/home/VOTRENOM/scripts/backup-gdrive.sh  
```

Créez le timer :
```bash
nano ~/.config/systemd/user/gdrive-backup.timer
```

Contenu :
```ini
[Unit]
Description=Daily Google Drive Backup

[Timer]
OnCalendar=daily  
OnCalendar=02:00  
Persistent=true  

[Install]
WantedBy=timers.target
```

Activez :
```bash
systemctl --user enable gdrive-backup.timer  
systemctl --user start gdrive-backup.timer  

# Vérifiez le statut
systemctl --user list-timers
```

### Dropbox

Dropbox offre un client officiel pour Linux, facile à installer et utiliser.

#### Installation de Dropbox

**Méthode 1 : Via le site officiel (recommandé)**

1. Visitez https://www.dropbox.com/install-linux
2. Téléchargez le .deb pour Ubuntu/Debian
3. Double-clic pour installer

**Méthode 2 : En ligne de commande**

```bash
cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
~/.dropbox-dist/dropboxd
```

**Méthode 3 : Via le gestionnaire de logiciels**

Recherchez "Dropbox" et installez.

#### Configuration initiale

1. **Premier lancement**
   - Lancez Dropbox depuis le menu
   - Ou `dropbox start -i` en terminal

2. **Connexion**
   - Page web s'ouvre
   - Connectez-vous à votre compte Dropbox
   - Ou créez un compte

3. **Choix du plan**
   - Basic (gratuit, 2 Go)
   - Ou plan payant

4. **Dossier de synchronisation**
   - Par défaut : `~/Dropbox`
   - Ou choisissez un autre emplacement

5. **Synchronisation sélective**
   - "Not everything, I'll choose what to sync later"
   - Vous pourrez sélectionner les dossiers plus tard

6. **Finalisation**
   - Dropbox démarre la synchronisation
   - Icône dans la barre système

#### Utilisation de Dropbox

**Synchronisation automatique :**
- Tout fichier dans `~/Dropbox` est automatiquement synchronisé
- Modifications en temps réel
- Fonctionne même si vous éditez avec n'importe quelle application

**Synchronisation sélective :**
Clic droit icône Dropbox → Preferences → Sync → Selective Sync
- Décochez les dossiers à ne pas synchroniser localement
- Ils restent dans le cloud mais ne prennent pas de place locale

**Partage :**
1. Clic droit sur fichier/dossier
2. Dropbox → Share
3. Invitez des personnes ou créez un lien

**Historique :**
- Dropbox garde 30 jours d'historique (gratuit)
- 180 jours (plan Plus) ou illimité (plan Professional)
- Récupérez via interface web

**Notifications :**
Preferences → General → Show desktop notifications

### Mega avec MEGAcmd

Mega offre un client en ligne de commande puissant pour Linux.

#### Installation

**Via le site officiel :**

1. Visitez https://mega.io/desktop
2. Téléchargez le package pour votre distribution
3. Installez le .deb :
```bash
sudo dpkg -i megacmd-*.deb  
sudo apt install -f  # Résoudre les dépendances  
```

**Via les dépôts :**

```bash
# Ajoutez le dépôt Mega
wget -O - https://mega.nz/linux/MEGAsync/Debian_10.0/amd64/megasync-Debian_10.0_amd64.deb  
sudo apt install ./megasync-*.deb  
```

#### Configuration et utilisation

**Connexion :**
```bash
mega-login votreemail@example.com votre-mot-de-passe
```

**Lister les fichiers :**
```bash
mega-ls
```

**Upload :**
```bash
mega-put /path/to/local/file /Remote/Path
```

**Download :**
```bash
mega-get /Remote/Path /local/path
```

**Synchronisation :**
```bash
mega-sync /home/user/Documents /Documents
```

**Interface graphique (MEGAsync) :**

Si vous préférez une interface graphique :
```bash
sudo apt install megasync
```

Lancez MEGAsync depuis le menu, connectez-vous, configurez la synchronisation.

## Synchronisation multi-cloud avec rclone

rclone peut gérer plusieurs services cloud simultanément.

### Configuration multi-services

Vous pouvez configurer plusieurs "remotes" :
- gdrive : Google Drive
- dropbox : Dropbox
- onedrive : OneDrive
- mega : Mega
- etc.

Pour chaque service, lancez `rclone config` et ajoutez un nouveau remote.

### Script de sauvegarde redondante

Sauvegardez sur plusieurs clouds pour redondance maximale :

```bash
#!/bin/bash
# Sauvegarde redondante multi-cloud

SOURCE="/home/$USER/Documents"

# Sauvegarde sur Google Drive
echo "Sauvegarde vers Google Drive..."  
rclone sync "$SOURCE" gdrive:Backup/Documents  

# Sauvegarde sur Dropbox
echo "Sauvegarde vers Dropbox..."  
rclone sync "$SOURCE" dropbox:Backup/Documents  

# Sauvegarde sur Mega
echo "Sauvegarde vers Mega..."  
rclone sync "$SOURCE" mega:Backup/Documents  

echo "Sauvegarde multi-cloud terminée !"
```

### Montage unifié

Montez tous vos clouds dans un seul dossier avec rclone union :

```bash
# Montez plusieurs clouds ensemble
rclone mount \
    --vfs-cache-mode full \
    --union gdrive:Docs \
    --union dropbox:Docs \
    --union mega:Docs \
    ~/AllClouds &
```

Maintenant `~/AllClouds` contient tous vos fichiers de tous les clouds.

## Syncthing : Synchronisation P2P

Syncthing synchronise vos fichiers directement entre vos appareils, sans serveur cloud central.

### Installation de Syncthing

```bash
# Méthode 1 : Dépôt officiel (recommandé)
sudo curl -o /usr/share/keyrings/syncthing-archive-keyring.gpg https://syncthing.net/release-key.gpg  
echo "deb [signed-by=/usr/share/keyrings/syncthing-archive-keyring.gpg] https://apt.syncthing.net/ syncthing stable" | sudo tee /etc/apt/sources.list.d/syncthing.list  
sudo apt update  
sudo apt install syncthing  

# Méthode 2 : Flatpak
flatpak install flathub me.kozec.syncthingtk
```

### Configuration de Syncthing

**1. Démarrer Syncthing**

```bash
syncthing
```

Ou activez le service pour démarrage automatique :
```bash
systemctl --user enable syncthing.service  
systemctl --user start syncthing.service  
```

**2. Accéder à l'interface web**

- Ouvrez un navigateur
- Allez sur http://localhost:8384
- L'interface Syncthing s'affiche

**3. Configuration initiale**

- Définissez un nom pour cet appareil
- Configurez un mot de passe (si accès depuis réseau)

**4. Ajouter un dossier à synchroniser**

- Cliquez **Add Folder**
- **Folder Label :** Nom descriptif (ex: "Documents")
- **Folder Path :** Chemin local (ex: `/home/user/Documents`)
- **Folder ID :** Généré automatiquement (ou personnalisez)
- Cliquez **Save**

**5. Ajouter un autre appareil**

Sur votre autre appareil (téléphone, autre PC) :
- Installez Syncthing
- Notez son Device ID

Retour sur le premier appareil :
- Cliquez **Add Remote Device**
- **Device ID :** Collez l'ID de l'autre appareil
- **Device Name :** Nom descriptif
- Onglet **Sharing** : Sélectionnez les dossiers à partager
- **Save**

Sur l'autre appareil :
- Acceptez la demande de connexion
- Choisissez les dossiers à synchroniser

**6. Synchronisation**

La synchronisation commence automatiquement !
- Bidirectionnelle par défaut
- Temps réel
- Aucune limite de taille

### Fonctionnalités avancées Syncthing

**Versioning (versions des fichiers) :**
- Dossier → Edit → File Versioning
- Types disponibles :
  - **Trash Can :** Versions dans la corbeille
  - **Simple :** Garde N versions
  - **Staggered :** Versions espacées dans le temps
  - **External :** Script personnalisé

**Ignorer certains fichiers :**
- Dossier → Edit → Ignore Patterns
- Syntaxe type .gitignore
- Exemple :
  ```
  *.tmp
  .cache
  node_modules
  ```

**Synchronisation send-only ou receive-only :**
- Dossier → Edit → Folder Type
- **Send Only :** Envoie uniquement, ne reçoit pas de modifications
- **Receive Only :** Reçoit uniquement, changements locaux ignorés

## Chiffrement et sécurité

### Pourquoi chiffrer vos sauvegardes cloud ?

**Sans chiffrement :**
- Le fournisseur cloud peut lire vos fichiers
- Risque en cas de piratage du service
- Problèmes de confidentialité
- Obligation légale pour données sensibles

**Avec chiffrement :**
- ✅ Vous seul pouvez lire vos fichiers
- ✅ Protection contre piratage du service
- ✅ Respect de la vie privée
- ✅ Conformité RGPD pour données personnelles

### Chiffrement côté client avec Cryptomator

Cryptomator chiffre vos fichiers AVANT de les envoyer au cloud.

#### Installation de Cryptomator

```bash
# Méthode 1 : AppImage (recommandé)
# Téléchargez depuis https://cryptomator.org/downloads/linux
chmod +x cryptomator-*.AppImage
./cryptomator-*.AppImage

# Méthode 2 : PPA
sudo add-apt-repository ppa:sebastian-stenzel/cryptomator  
sudo apt update  
sudo apt install cryptomator  
```

#### Configuration

**1. Créer un coffre (vault)**
- Lancez Cryptomator
- **Add Vault** → **Create New Vault**
- **Nom :** Nom descriptif
- **Location :** Dans votre dossier cloud sync
  - Exemple : `~/Nextcloud/Coffre-Chiffre`
- **Mot de passe :** Choisissez un mot de passe FORT
  - ⚠️ Si vous le perdez, vos données sont perdues !
- **Save** le recovery key dans un endroit sûr

**2. Déverrouiller le coffre**
- Sélectionnez le coffre
- **Unlock**
- Entrez le mot de passe
- Le coffre apparaît comme un lecteur virtuel

**3. Utiliser le coffre**
- Placez vos fichiers sensibles dans le coffre déverrouillé
- Ils sont automatiquement chiffrés
- Les fichiers chiffrés sont synchronisés au cloud
- Sur le cloud : fichiers incompréhensibles
- Localement (déverrouillé) : fichiers normaux

**4. Verrouiller le coffre**
- **Lock** quand vous avez fini
- Fichiers chiffrés restent, mais inaccessibles

#### Workflow avec Cryptomator

```
Vos fichiers sensibles
        ↓
Coffre Cryptomator (déverrouillé)
        ↓
Chiffrement automatique
        ↓
Dossier cloud (Nextcloud/Dropbox/etc.)
        ↓
Synchronisation au cloud
        ↓
Stockage cloud chiffré ✅
```

Sur un autre appareil :
- Installez Cryptomator
- Pointez vers le coffre synchronisé
- Déverrouillez avec le même mot de passe
- Accédez aux fichiers déchiffrés

### Chiffrement avec rclone crypt

rclone peut chiffrer vos fichiers avant upload.

#### Configuration

```bash
rclone config
```

**1. Créer un remote chiffré**
```
n) New remote  
name> gdrive-crypt  
Storage> crypt  
remote> gdrive:encrypted  # Où stocker les fichiers chiffrés  
filename_encryption> standard  
directory_name_encryption> true  
password> [Votre mot de passe fort]  
password2> [Confirmation]  
```

**2. Utilisation**

```bash
# Copier vers le remote chiffré
rclone copy /home/user/Documents/secret.pdf gdrive-crypt:

# Les fichiers sont automatiquement chiffrés
# Sur Google Drive, ils apparaissent illisibles

# Pour récupérer :
rclone copy gdrive-crypt:secret.pdf /home/user/Téléchargements/
# Automatiquement déchiffré
```

**3. Automatisation**

Modifiez votre script de sauvegarde pour utiliser le remote chiffré :
```bash
rclone sync /home/user/Documents gdrive-crypt:Documents
```

### Comparaison des solutions de chiffrement

| Solution | Complexité | Performance | Compatible | Use Case |
|----------|------------|-------------|-----------|----------|
| **Cryptomator** | Facile | Bonne | Tous clouds | Débutants, interface graphique |
| **rclone crypt** | Moyenne | Excellente | Tous clouds | Scripts, automatisation |
| **VeraCrypt** | Difficile | Moyenne | Fichiers locaux | Containers chiffrés |
| **Chiffrement intégré** | Facile | Excellente | Service spécifique | Mega, Nextcloud E2E |

## Gestion de la bande passante

### Pourquoi limiter la bande passante ?

**Problèmes sans limitation :**
- Upload cloud sature votre connexion
- Navigation web devient lente
- Visioconférences saccadées
- Autres appareils affectés

**Solution :** Limiter l'upload cloud à 70-80% de votre capacité maximale.

### Limitation dans les clients cloud

**Nextcloud :**
- Settings → Network
- Upload bandwidth limit : 5000 KB/s (exemple)
- Download bandwidth limit : Laissez illimité généralement

**Dropbox :**
- Preferences → Network
- Upload rate : Limit to XX KB/s
- Download rate : Don't limit (généralement)

**rclone :**

```bash
# Limiter à 5 MB/s
rclone sync /source dest: --bwlimit 5M

# Limiter différemment selon l'heure
rclone sync /source dest: --bwlimit "08:00,512k 19:00,10M"
# 512 KB/s de 8h à 19h, 10 MB/s le reste du temps
```

### Planification des synchronisations

Synchronisez aux heures creuses pour ne pas gêner votre utilisation.

**Avec Nextcloud :**
- Pas de planification native
- Utilisez pause/resume manuellement
- Ou script avec cron pour arrêter/démarrer le client

**Avec rclone :**

Script intelligent :
```bash
#!/bin/bash
# Sauvegarde uniquement la nuit

HOUR=$(date +%H)

# Entre 2h et 6h du matin
if [ $HOUR -ge 2 ] && [ $HOUR -lt 6 ]; then
    echo "Heure creuse, synchronisation complète"
    rclone sync /home/user/Documents gdrive:Documents --bwlimit 0  # Sans limite
else
    echo "Heures pleines, synchronisation limitée"
    rclone sync /home/user/Documents gdrive:Documents --bwlimit 1M
fi
```

## Surveillance et notifications

### Vérifier l'état de synchronisation

**Nextcloud :**
- Icône barre système : vert = synchronisé, orange = en cours
- Clic sur icône : détails de la synchronisation
- Paramètres → Activity : historique complet

**Dropbox :**
- Icône verte = OK
- Icône bleue = synchronisation en cours
- Interface web : Recent pour voir les modifications

**rclone :**

Vérifier la dernière synchronisation :
```bash
rclone check /local/path remote:path
```

Différences :
```bash
rclone check /local/path remote:path --one-way
```

### Notifications automatiques

**Script avec notifications :**

```bash
#!/bin/bash

# Sauvegarde avec notification
rclone sync /home/user/Documents gdrive:Documents 2>&1 | tee /tmp/rclone.log

if [ ${PIPESTATUS[0]} -eq 0 ]; then
    notify-send "☁️ Sauvegarde Cloud" "Synchronisation réussie ✅"
else
    notify-send -u critical "☁️ Sauvegarde Cloud" "Erreur de synchronisation ❌\nVoir /tmp/rclone.log"
fi
```

**Surveillance avec systemd :**

```bash
# Voir le statut du service Nextcloud
systemctl --user status nextcloud

# Voir les logs
journalctl --user -u nextcloud -f
```

**Alertes par email :**

Configurez rclone pour envoyer des emails en cas d'erreur :
```bash
rclone sync /source dest: --log-file=/tmp/backup.log

# Script pour vérifier et envoyer email si erreur
if grep -i "error" /tmp/backup.log; then
    echo "Erreurs détectées" | mail -s "Erreur sauvegarde cloud" votre@email.com
fi
```

## Bonnes pratiques

### Stratégie cloud complète

**1. Séparation des données**

- **Cloud public (Google Drive, Dropbox) :** Documents bureautiques, photos
- **Cloud privé (Nextcloud) :** Données sensibles, professionnelles
- **Syncthing :** Synchronisation locale entre vos appareils
- **Local (disque externe) :** Vidéos volumineuses, archives

**2. Organisation des dossiers**

```
~/Cloud/
├── Nextcloud/        # Auto-sync cloud privé
│   ├── Documents/
│   ├── Photos/
│   └── Projets/
├── Dropbox/          # Auto-sync collaboratif
│   └── Travail/
└── GoogleDrive/      # Via rclone, manuel/script
    └── Archives/
```

**3. Règle du 3-2-1 avec cloud**

- **3 copies :** Original + disque externe + cloud
- **2 supports :** Local (disque interne + externe) + Cloud
- **1 hors site :** Cloud (naturellement hors site)

### Sécurité et confidentialité

**1. Chiffrez les données sensibles**
- Cryptomator pour données personnelles sensibles
- rclone crypt pour scripts automatisés
- Nextcloud E2E pour maximum de sécurité

**2. Authentification forte**
- Activez 2FA (double authentification) sur tous les comptes cloud
- Utilisez des mots de passe uniques et forts
- Gestionnaire de mots de passe (Bitwarden, KeePassXC)

**3. Vérifiez les partages**
- Révisez régulièrement les partages actifs
- Supprimez les anciens liens de partage
- Définissez des dates d'expiration

**4. Lisez les conditions d'utilisation**
- Comprenez ce que le fournisseur peut faire avec vos données
- Préférez des services respectueux de la vie privée
- Solutions européennes (RGPD) pour données personnelles

### Optimisation des performances

**1. Synchronisation sélective**
- Ne synchronisez que ce qui est nécessaire
- Utilisez les "fichiers à la demande" si disponible
- Excluez les gros fichiers inutiles

**2. Compression**

```bash
# rclone peut compresser à la volée (économise bande passante)
rclone sync /source dest: --compress
```

**3. Transferts multi-threads**

```bash
# Accélère les transferts
rclone sync /source dest: --transfers 16 --checkers 16
```

**4. Cache local**

```bash
# rclone mount avec cache
rclone mount gdrive: ~/GoogleDrive \
    --vfs-cache-mode full \
    --cache-dir ~/.cache/rclone
```

### Monitoring de l'espace

**Vérifiez régulièrement :**

```bash
# Espace utilisé Nextcloud (via client)
# Visible dans les paramètres

# Espace Google Drive
rclone about gdrive:

# Espace Dropbox
dropbox status
```

**Nettoyage régulier :**
- Supprimez les anciens fichiers
- Videz les corbeilles des services cloud
- Compressez les archives
- Déplacez les gros fichiers vers stockage local

### Sauvegarde de la configuration

**Sauvegardez vos configurations cloud !**

```bash
# Configuration rclone
cp ~/.config/rclone/rclone.conf ~/Documents/config-backup/

# Configuration Nextcloud (si personnalisée)
cp ~/.config/Nextcloud/* ~/Documents/config-backup/Nextcloud/

# Scripts de sauvegarde
cp ~/scripts/backup-*.sh ~/Documents/config-backup/scripts/
```

Chiffrez ce backup et mettez-le en sécurité !

## Dépannage

### Problème : "Synchronisation bloquée"

**Nextcloud / Dropbox :**
- Vérifiez la connexion Internet
- Vérifiez l'espace disque local et cloud
- Redémarrez le client
- Vérifiez les permissions de fichiers
- Consultez les logs

```bash
# Logs Nextcloud
cat ~/.local/share/Nextcloud/nextcloud.log

# Logs Dropbox
cat ~/.dropbox/dropbox.log
```

### Problème : "Fichiers en conflit"

**Cause :** Modifications simultanées sur plusieurs appareils

**Solution :**
- Les services créent des versions conflictuelles
- Fichier original + fichier "conflict"
- Comparez manuellement
- Gardez la bonne version
- Supprimez l'autre

**Prévention :** Évitez de modifier le même fichier sur plusieurs appareils simultanément

### Problème : "rclone : token expiré"

```bash
# Reconnectez-vous
rclone config reconnect gdrive:
```

Suivez les instructions pour réautoriser.

### Problème : "Quota cloud dépassé"

**Solutions :**
1. Nettoyez les fichiers inutiles
2. Videz la corbeille du cloud
3. Passez à un plan supérieur
4. Ajoutez un autre service cloud
5. Déplacez gros fichiers vers stockage local

### Problème : "Synchronisation très lente"

**Diagnostic :**
```bash
# Testez votre vitesse upload
speedtest-cli

# Vérifiez la limite configurée
# Nextcloud : Settings → Network
```

**Solutions :**
- Augmentez la limite de bande passante si connexion le permet
- Synchronisez aux heures creuses
- Activez la compression (rclone)
- Vérifiez qu'aucun autre processus ne sature la connexion

## En résumé

La sauvegarde cloud automatisée est essentielle pour une protection complète :

### Configuration recommandée pour débutants

**Solution simple :**
- **Nextcloud** (hébergé) : Documents, photos (10-20€/an pour 100-200 Go)
- Client desktop : synchronisation automatique
- Application mobile : accès nomade
- **+** Disque externe local : sauvegarde complète

**Solution gratuite :**
- **Google Drive** (15 Go gratuits) : Documents importants
- **Mega** (20 Go gratuits) : Photos
- **rclone** : automatisation
- **Syncthing** : synchronisation entre vos appareils

### Configuration recommandée pour intermédiaires

**Multi-cloud redondant :**
- **Nextcloud** : Cloud principal
- **Dropbox ou Google Drive** : Cloud secondaire
- **rclone** : scripts automatisés pour redondance
- **Cryptomator** : chiffrement données sensibles
- Disque externe : sauvegarde locale complète

### Points clés à retenir

✅ **À faire :**
- Automatisez les synchronisations
- Chiffrez les données sensibles
- Activez la 2FA sur tous les comptes
- Testez régulièrement les restaurations
- Combinez cloud + local (règle 3-2-1)
- Surveillez l'espace utilisé

❌ **À éviter :**
- Dépendre d'un seul service cloud
- Uploader des données sensibles non chiffrées
- Saturer votre connexion (limitez la bande passante)
- Oublier de tester les restaurations
- Utiliser le cloud comme seule sauvegarde

### Votre checklist cloud

```
□ Service cloud choisi et configuré
□ Client desktop installé et connecté
□ Synchronisation automatique activée
□ Fichiers sensibles chiffrés (Cryptomator)
□ 2FA activé sur le compte cloud
□ Bande passante limitée pour ne pas saturer
□ Sauvegarde locale en complément
□ Test de restauration effectué
□ Documentation des configurations
□ Surveillance de l'espace disponible
```

Avec une sauvegarde cloud bien configurée, vos données sont protégées contre les catastrophes locales, accessibles de partout, et synchronisées automatiquement. C'est la tranquillité d'esprit numérique !

⏭️ [Maintenance et optimisation](/18-maintenance-et-optimisation/README.md)
