🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 10.3 Synchronisation Google Drive (Insync, rclone)

## Le problème : Google Drive et Linux

**Google ne propose pas de client officiel Google Drive pour Linux.**

Contrairement à Windows et macOS qui ont une application Google Drive native, les utilisateurs Linux doivent utiliser des solutions tierces pour synchroniser leurs fichiers Google Drive.

### Pourquoi c'est important ?

Si vous utilisez déjà Google Drive (15 Go gratuits) et que vous migrez vers Linux Mint, vous voulez probablement :
- ✅ Continuer à accéder à vos fichiers
- ✅ Synchroniser automatiquement vos données
- ✅ Ne pas perdre vos habitudes de travail

**Bonne nouvelle :** Plusieurs excellentes solutions existent pour Linux Mint !

---

## Aperçu des solutions disponibles

### 1. **Insync** (Payant - Recommandé pour débutants)
- ✅ Interface graphique simple
- ✅ Synchronisation bidirectionnelle complète
- ✅ Support de plusieurs comptes Google
- ✅ Très stable et fiable
- ❌ Payant (~30€ achat unique)

### 2. **rclone** (Gratuit - Pour utilisateurs intermédiaires)
- ✅ Totalement gratuit et open source
- ✅ Très puissant et flexible
- ✅ Supporte 40+ services cloud
- ❌ Ligne de commande uniquement
- ❌ Configuration plus technique

### 3. **GNOME Online Accounts** (Gratuit - Basique)
- ✅ Intégré à Linux Mint
- ✅ Gratuit
- ❌ Accès limité (pas de synchronisation complète)
- ❌ Uniquement via le gestionnaire de fichiers

### 4. **ODrive** (Gratuit avec limitations)
- ✅ Interface graphique
- ✅ Support multi-cloud
- ❌ Version gratuite limitée
- ❌ Synchronisation premium payante

---

## Solution 1 : Insync (Recommandé pour débutants)

**Insync** est la solution la plus simple et la plus proche de l'expérience Google Drive sur Windows/Mac.

### Avantages d'Insync

- ✅ **Interface graphique intuitive** - Pas besoin de ligne de commande
- ✅ **Synchronisation bidirectionnelle** - Les modifications se font dans les deux sens
- ✅ **Synchronisation sélective** - Choisissez quels dossiers synchroniser
- ✅ **Multi-comptes** - Gérez plusieurs comptes Google
- ✅ **Support Google Photos, Drive partagé, Google Docs**
- ✅ **Conversion automatique** des Google Docs en formats Office
- ✅ **Excellent support client**

### Inconvénients

- ❌ **Payant** : ~29,99$ pour une licence à vie (1 compte)
- ❌ **Chaque compte Google nécessite une licence** (mais souvent des packs disponibles)

### Prix (2024)

- **License unique** : ~29,99$ (1 compte Google)
- **Pack 3 comptes** : ~59,99$
- **Pack 5 comptes** : ~89,99$

**Note :** Achat unique, pas d'abonnement mensuel. Mises à jour incluses.

---

### Installation d'Insync

#### Étape 1 : Télécharger Insync

1. Rendez-vous sur le site officiel : https://www.insynchq.com/downloads
2. Téléchargez la version pour **Ubuntu/Debian** (fichier `.deb`)
3. Le fichier se télécharge dans votre dossier `Téléchargements`

#### Étape 2 : Installer le fichier .deb

**Méthode graphique :**
1. Ouvrez votre dossier `Téléchargements`
2. **Double-cliquez** sur le fichier `insync_*.deb`
3. Le **Gestionnaire de paquets** s'ouvre
4. Cliquez sur **Installer**
5. Entrez votre mot de passe administrateur

**Méthode terminal :**
```bash
cd ~/Téléchargements
sudo dpkg -i insync_*.deb
sudo apt install -f  # Pour installer les dépendances manquantes
```

#### Étape 3 : Lancer Insync

1. Menu → Internet → **Insync**
2. Ou tapez `insync start` dans le terminal

---

### Configuration d'Insync

#### Première connexion

1. **Écran de bienvenue**
   - Cliquez sur "Sign in with Google"

2. **Choix du type de compte**
   - Sélectionnez **Google Drive**
   - (Insync supporte aussi OneDrive)

3. **Connexion Google**
   - Une page web s'ouvre
   - Connectez-vous avec votre compte Google
   - **Autorisez Insync** à accéder à Google Drive
   - ⚠️ Lisez bien les permissions demandées

4. **Choix du dossier de synchronisation**
   - Par défaut : `/home/votre-nom/Google Drive`
   - Vous pouvez le modifier (exemple : `/home/votre-nom/GoogleDrive`)
   - Cliquez sur **Next**

5. **Synchronisation sélective**

   Trois options :

   **Option A : Tout synchroniser** (recommandé pour débuter)
   - Tous vos fichiers Google Drive seront téléchargés localement

   **Option B : Synchronisation sélective**
   - Cochez uniquement les dossiers que vous voulez synchroniser
   - Économise de l'espace disque
   - Recommandé si vous avez beaucoup de fichiers

   **Option C : Pas de synchronisation locale (streaming)**
   - Les fichiers restent dans le cloud
   - Vous les téléchargez à la demande
   - Économise énormément d'espace

6. **Conversion des Google Docs**

   Insync peut convertir vos Google Docs en formats Office :
   - Google Docs → `.docx` (Word)
   - Google Sheets → `.xlsx` (Excel)
   - Google Slides → `.pptx` (PowerPoint)

   **Recommandation :** Activez cette option si vous travaillez souvent hors ligne.

7. **Finalisation**
   - Cliquez sur **Finish**
   - La synchronisation démarre !

---

### Utilisation quotidienne d'Insync

#### Icône dans la barre d'état

Insync apparaît dans votre **barre d'état système** (en haut à droite).

**Cliquez sur l'icône** pour :
- 📊 Voir l'état de la synchronisation
- ⏸️ Mettre en pause la synchronisation
- ⚙️ Accéder aux paramètres
- 📁 Ouvrir le dossier Google Drive
- 🌐 Ouvrir Google Drive dans le navigateur

**Codes couleur de l'icône :**
- 🟢 **Vert** : Tout est synchronisé
- 🔵 **Bleu** : Synchronisation en cours
- 🔴 **Rouge** : Erreur de synchronisation
- ⚪ **Gris** : En pause

---

#### Le dossier Google Drive

Après installation, vous avez un dossier `Google Drive` dans votre répertoire personnel.

**Fonctionnement :**
- Les fichiers ajoutés ici sont **automatiquement uploadés** vers Google Drive
- Les modifications locales sont **synchronisées** vers le cloud
- Les modifications cloud sont **téléchargées** localement
- Les suppressions fonctionnent dans les deux sens

**C'est exactement comme sur Windows/Mac !**

---

#### Fonctionnalités avancées d'Insync

##### 🔗 **Partage rapide**
- Clic droit sur un fichier → **Insync** → **Share**
- Génère un lien de partage Google Drive instantanément

##### 📋 **Copier le lien**
- Clic droit → **Insync** → **Copy Web Link**
- Copie le lien Google Drive du fichier

##### 🔄 **Forcer la synchronisation**
- Clic droit → **Insync** → **Force Sync**
- Utile si un fichier semble bloqué

##### 📌 **Épingler/Désépingler**
- Clic droit → **Insync** → **Pin/Unpin**
- Les fichiers épinglés restent toujours synchronisés localement

---

### Paramètres avancés d'Insync

**Accès :** Icône Insync → ⚙️ **Preferences**

#### Onglet Account
- Ajouter d'autres comptes Google
- Gérer les dossiers synchronisés
- Changer le dossier de synchronisation

#### Onglet General
- ✅ **Démarrer au lancement** de Linux Mint
- 📢 **Notifications** de synchronisation
- 🔔 **Sons** de notification

#### Onglet Bandwidth
- 📊 **Limiter la bande passante** upload/download
- Utile si Insync ralentit votre connexion
- Exemple : Limiter à 1 Mbps en journée, illimité la nuit

#### Onglet Selective Sync
- Modifier les dossiers synchronisés
- Ajouter/retirer des dossiers à tout moment

#### Onglet Advanced
- **Conversion des Google Docs**
- **Proxy** settings
- **Gestion du cache**
- **Base de données** de synchronisation

---

### Gestion de plusieurs comptes Google

Insync peut gérer plusieurs comptes Google simultanément.

**Ajouter un compte :**
1. Icône Insync → **Add Account**
2. Sélectionnez **Google Drive**
3. Connectez-vous avec le 2ème compte
4. Choisissez un dossier différent (ex: `Google Drive 2`)

**Résultat :** Vous aurez deux dossiers séparés :
- `/home/votre-nom/Google Drive` (compte 1)
- `/home/votre-nom/Google Drive 2` (compte 2)

⚠️ **Attention :** Chaque compte nécessite une licence Insync séparée.

---

### Dépannage Insync

#### Problème : Synchronisation bloquée

**Solutions :**
1. Vérifiez votre connexion Internet
2. Pause → Reprendre la synchronisation
3. Redémarrez Insync : `insync quit` puis `insync start`
4. Vérifiez les logs : Preferences → Advanced → View Logs

#### Problème : Fichiers en conflit

Si un fichier est modifié simultanément localement et dans le cloud :
- Insync crée une copie avec `(conflit)` dans le nom
- Vous devez manuellement fusionner les versions

#### Problème : Insync consomme trop de CPU

**Causes :**
- Synchronisation initiale en cours (normal)
- Nombreux petits fichiers (ralentit la synchro)

**Solutions :**
- Attendez la fin de la synchro initiale
- Limitez la bande passante
- Excluez les dossiers avec beaucoup de petits fichiers

---

## Solution 2 : rclone (Gratuit - Ligne de commande)

**rclone** est un outil en ligne de commande puissant et totalement gratuit pour synchroniser Google Drive (et 40+ autres services cloud).

### Avantages de rclone

- ✅ **Gratuit et open source**
- ✅ **Très puissant et flexible**
- ✅ **Supporte 40+ services cloud** (Google Drive, Dropbox, OneDrive, etc.)
- ✅ **Cryptage côté client** possible
- ✅ **Automatisation avec scripts**
- ✅ **Très performant**
- ✅ **Consomme peu de ressources**

### Inconvénients

- ❌ **Ligne de commande uniquement** (pas d'interface graphique officielle)
- ❌ **Configuration initiale plus technique**
- ❌ **Courbe d'apprentissage**
- ❌ **Pas de synchronisation automatique en temps réel** (nécessite configuration)

---

### Installation de rclone

#### Méthode 1 : Via le gestionnaire de paquets (recommandé)

```bash
sudo apt update
sudo apt install rclone
```

#### Méthode 2 : Script officiel (version la plus récente)

```bash
curl https://rclone.org/install.sh | sudo bash
```

#### Vérifier l'installation

```bash
rclone version
```

Vous devriez voir la version installée.

---

### Configuration de rclone avec Google Drive

#### Étape 1 : Lancer la configuration

```bash
rclone config
```

#### Étape 2 : Créer un nouveau remote

```
n) New remote
```
Tapez `n` puis Entrée.

#### Étape 3 : Nommer le remote

```
name> gdrive
```
Vous pouvez choisir n'importe quel nom. On utilise ici `gdrive`.

#### Étape 4 : Choisir le type de stockage

```
Storage> drive
```
Tapez `drive` (ou le numéro correspondant à Google Drive dans la liste).

#### Étape 5 : Client ID et Secret (optionnel)

```
client_id>
client_secret>
```
Laissez vide (appuyez juste sur Entrée) pour utiliser les valeurs par défaut.

⚠️ **Note :** Pour un usage intensif, créez votre propre Client ID via Google Cloud Console.

#### Étape 6 : Scope (permissions)

```
scope> 1
```
- **1 = Full access** (accès complet) - Recommandé
- 2 = Read only (lecture seule)
- 3 = Access to specific files only

#### Étape 7 : Root folder ID

```
root_folder_id>
```
Laissez vide pour accéder à tout Google Drive.

#### Étape 8 : Service account file

```
service_account_file>
```
Laissez vide (pour usage personnel).

#### Étape 9 : Auto config

```
Use auto config?
y) Yes
n) No
```

- Si vous êtes sur votre **PC Linux Mint avec interface graphique** : Tapez `y`
- Si vous êtes sur un **serveur sans interface** : Tapez `n`

Pour Linux Mint : **Tapez `y`**

#### Étape 10 : Autorisation Google

Un navigateur web s'ouvre automatiquement :
1. **Connectez-vous** à votre compte Google
2. **Autorisez rclone** à accéder à Google Drive
3. Vous verrez "Success!"
4. Revenez au terminal

#### Étape 11 : Configurer comme Team Drive ?

```
Configure this as a team drive?
n) No
```
Tapez `n` (sauf si vous utilisez Google Workspace avec drives partagés).

#### Étape 12 : Confirmer la configuration

```
y) Yes this is OK
```
Tapez `y` pour confirmer.

#### Étape 13 : Quitter

```
q) Quit config
```
Tapez `q` pour quitter.

**Félicitations ! rclone est configuré avec Google Drive.**

---

### Utilisation de base de rclone

#### Lister les fichiers sur Google Drive

```bash
rclone ls gdrive:
```

Cela affiche tous vos fichiers Google Drive.

#### Lister uniquement les dossiers

```bash
rclone lsd gdrive:
```

#### Copier un fichier local vers Google Drive

```bash
rclone copy /chemin/local/fichier.txt gdrive:Documents/
```

Copie `fichier.txt` vers le dossier `Documents` sur Google Drive.

#### Copier un fichier de Google Drive vers local

```bash
rclone copy gdrive:Documents/fichier.txt /home/votre-nom/Téléchargements/
```

#### Synchroniser un dossier local vers Google Drive

```bash
rclone sync /home/votre-nom/Documents gdrive:Documents
```

⚠️ **Attention :** `sync` rend la destination identique à la source. Fichiers supprimés localement seront supprimés sur Drive.

#### Synchronisation bidirectionnelle (plus sûr)

```bash
rclone bisync /home/votre-nom/Documents gdrive:Documents
```

**Note :** `bisync` est une fonctionnalité expérimentale mais très utile.

---

### Commandes rclone essentielles

| Commande | Description |
|----------|-------------|
| `rclone copy source dest` | Copie les fichiers (ne supprime rien) |
| `rclone sync source dest` | Synchronise (destination = source) |
| `rclone bisync path1 path2` | Synchronisation bidirectionnelle |
| `rclone move source dest` | Déplace les fichiers |
| `rclone delete remote:path` | Supprime des fichiers |
| `rclone mkdir remote:path` | Crée un dossier |
| `rclone ls remote:` | Liste les fichiers |
| `rclone lsd remote:` | Liste les dossiers |
| `rclone size remote:path` | Taille totale d'un dossier |
| `rclone check source dest` | Vérifie si source = dest |

---

### Synchronisation automatique avec rclone

Pour synchroniser automatiquement toutes les heures :

#### Méthode 1 : Avec cron

1. **Ouvrir crontab**
   ```bash
   crontab -e
   ```

2. **Ajouter cette ligne** (synchronisation toutes les heures)
   ```
   0 * * * * rclone sync /home/votre-nom/Documents gdrive:Documents
   ```

3. **Sauvegarder et quitter**
   - Ctrl+O (sauvegarder)
   - Ctrl+X (quitter)

#### Méthode 2 : Script avec systemd timer (plus moderne)

**1. Créer un script de synchronisation**

```bash
nano ~/sync-gdrive.sh
```

Contenu du script :
```bash
#!/bin/bash
rclone bisync /home/votre-nom/Documents gdrive:Documents -v
```

**2. Rendre le script exécutable**
```bash
chmod +x ~/sync-gdrive.sh
```

**3. Créer un service systemd**
```bash
sudo nano /etc/systemd/system/gdrive-sync.service
```

Contenu :
```ini
[Unit]
Description=Google Drive Sync

[Service]
Type=oneshot
ExecStart=/home/votre-nom/sync-gdrive.sh
User=votre-nom
```

**4. Créer un timer systemd**
```bash
sudo nano /etc/systemd/system/gdrive-sync.timer
```

Contenu :
```ini
[Unit]
Description=Run Google Drive Sync hourly

[Timer]
OnBootSec=5min
OnUnitActiveSec=1h

[Install]
WantedBy=timers.target
```

**5. Activer et démarrer le timer**
```bash
sudo systemctl enable gdrive-sync.timer
sudo systemctl start gdrive-sync.timer
```

**6. Vérifier le statut**
```bash
systemctl status gdrive-sync.timer
```

---

### Interface graphique pour rclone (optionnel)

Bien que rclone soit principalement en ligne de commande, des interfaces graphiques existent :

#### **RcloneBrowser** (GUI simple)

Installation :
```bash
sudo add-apt-repository ppa:rclone-browser/rclone-browser
sudo apt update
sudo apt install rclone-browser
```

**Fonctionnalités :**
- Interface graphique pour parcourir vos fichiers
- Upload/download par glisser-déposer
- Gestion des remotes

#### **rclone webui** (Interface web)

```bash
rclone rcd --rc-web-gui
```

Ouvrez votre navigateur : `http://localhost:5572`

**Fonctionnalités :**
- Interface web moderne
- Gestion des transferts
- Configuration des remotes

---

### Options avancées de rclone

#### Limiter la bande passante

```bash
# Limiter à 10 Mbps
rclone sync /home/votre-nom/Documents gdrive:Documents --bwlimit 10M

# Limiter différemment selon l'heure (10M en journée, illimité la nuit)
rclone sync /home/votre-nom/Documents gdrive:Documents --bwlimit "08:00,10M 23:00,off"
```

#### Filtrer les fichiers

```bash
# Synchroniser uniquement les fichiers .pdf
rclone sync /home/votre-nom/Documents gdrive:Documents --include "*.pdf"

# Exclure les fichiers temporaires
rclone sync /home/votre-nom/Documents gdrive:Documents --exclude "*.tmp"

# Exclure un dossier
rclone sync /home/votre-nom/Documents gdrive:Documents --exclude "/cache/**"
```

#### Mode dry-run (test sans modifier)

```bash
rclone sync /home/votre-nom/Documents gdrive:Documents --dry-run
```

Affiche ce qui serait fait **sans rien modifier**. Très utile pour tester !

#### Crypter les fichiers sur Google Drive

```bash
rclone config  # Créer un remote "crypt" qui chiffre "gdrive"
```

Vos fichiers sont **chiffrés avant upload**, Google ne peut pas les lire.

---

### Comparaison rclone vs Insync

| Critère | rclone | Insync |
|---------|--------|--------|
| **Prix** | Gratuit | ~30€ |
| **Interface** | Ligne de commande | Graphique |
| **Facilité débutants** | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Flexibilité** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Performance** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Synchronisation temps réel** | ❌ (cron) | ✅ Automatique |
| **Multi-cloud** | ✅ 40+ services | ✅ Google/OneDrive |
| **Cryptage** | ✅ Intégré | ❌ |
| **Automatisation** | ✅ Scripts | ⭐⭐ |

**Recommandation :**
- **Débutants** → Insync (simple, efficace, vaut son prix)
- **Utilisateurs intermédiaires/avancés** → rclone (gratuit, puissant, flexible)
- **Budget serré** → rclone avec interface web
- **Synchronisation temps réel obligatoire** → Insync

---

## Solution 3 : GNOME Online Accounts (Intégré)

Une solution simple déjà présente dans Linux Mint.

### Activation

1. **Paramètres système** → **Comptes en ligne**
2. Cliquez sur **Google**
3. Connectez-vous avec votre compte Google
4. Autorisez l'accès

### Fonctionnalités

- ✅ Accès à Google Drive via le **gestionnaire de fichiers** (Nemo)
- ✅ Synchronisation **Calendrier** Google
- ✅ Synchronisation **Contacts** Google
- ✅ Intégration mail (Thunderbird/Evolution)

### Limitations

- ❌ **Pas de synchronisation locale** automatique des fichiers
- ❌ **Accès lecture/écriture** mais fichiers restent dans le cloud
- ❌ **Pas de mode hors ligne** pour les fichiers

### Utilisation

Dans **Nemo** (gestionnaire de fichiers) :
- Barre latérale → **Google Drive** apparaît
- Vous pouvez parcourir, copier, modifier les fichiers
- Mais ils ne sont **pas téléchargés** automatiquement localement

**Idéal pour :** Accès occasionnel, pas de besoin de synchronisation complète.

---

## Comparaison globale des solutions

| Solution | Prix | Difficulté | Synchro complète | Recommandé pour |
|----------|------|------------|------------------|-----------------|
| **Insync** | 30€ | ⭐ Facile | ✅ Oui | Débutants, usage quotidien |
| **rclone** | Gratuit | ⭐⭐⭐ Moyen | ✅ Oui (config) | Utilisateurs techniques, budget limité |
| **GNOME Online** | Gratuit | ⭐ Facile | ❌ Non | Accès occasionnel |
| **Interface web** | Gratuit | ⭐ Très facile | ❌ Non | Accès ponctuel |

---

## Conseils de sécurité

### 🔒 Authentification à deux facteurs (2FA)

**Activez-la sur votre compte Google !**

1. Compte Google → Sécurité → Validation en deux étapes
2. Suivez les instructions
3. Utilisez une app d'authentification (Google Authenticator, Authy)

### 🔑 Mots de passe d'application

Si vous avez activé 2FA et utilisez rclone :
1. Google Account → Sécurité → Mots de passe d'application
2. Générez un mot de passe spécifique pour rclone
3. Utilisez-le au lieu de votre mot de passe principal

### 🛡️ Vérifiez les permissions

Régulièrement :
1. Compte Google → Sécurité → Gérer les accès
2. Vérifiez quelles applications ont accès
3. Révoquez les accès suspects

---

## Dépannage général

### Problème : "Quota dépassé"

**Google Drive gratuit = 15 Go** (partagés avec Gmail et Photos)

**Solutions :**
- Libérez de l'espace (supprimez des fichiers)
- Videz la corbeille Google Drive
- Passez à Google One (payant)

### Problème : Synchronisation lente

**Causes possibles :**
- Connexion Internet lente (surtout upload)
- Nombreux petits fichiers (ralentit tout)
- Limitation de Google (trop de requêtes)

**Solutions :**
- Limitez le nombre de fichiers simultanés
- Compressez les nombreux petits fichiers en archives
- Utilisez rclone avec `--transfers 4` (limite les transferts parallèles)

### Problème : Fichiers non synchronisés

**Vérifications :**
1. ✅ Nom de fichier valide (pas de caractères spéciaux interdits)
2. ✅ Taille < 5 To (limite Google Drive)
3. ✅ Connexion Internet active
4. ✅ Espace disponible sur Google Drive

---

## Bonnes pratiques

### 📁 Organisation

1. **Créez une structure claire** de dossiers
2. **Ne synchronisez pas tout** si vous manquez d'espace local
3. **Utilisez la synchronisation sélective** (Insync ou rclone avec filtres)

### 💾 Sauvegardes

1. **Google Drive n'est pas une sauvegarde** mais une synchronisation
2. **Gardez toujours une copie locale** de vos fichiers importants
3. **Utilisez Timeshift** pour sauvegarder votre système
4. **Règle 3-2-1** : 3 copies, 2 supports différents, 1 hors site

### ⚡ Performances

1. **Évitez de synchroniser** :
   - Dossiers avec des milliers de petits fichiers
   - Machines virtuelles (fichiers volumineux)
   - node_modules, .git (dossiers de développement)

2. **Utilisez .rcloneignore** ou Insync ignore rules

---

## Alternatives rapides

Si ni Insync ni rclone ne vous conviennent :

### **ODrive**
- Interface graphique
- Support multi-cloud
- Gratuit avec limitations

### **Celeste**
- Interface GTK native pour Linux
- Open source
- Encore en développement

### **google-drive-ocamlfuse**
- Monte Google Drive comme un système de fichiers
- Gratuit et open source
- Ligne de commande

---

## Ressources utiles

### 📚 Documentation
- Insync : https://www.insynchq.com/help
- rclone : https://rclone.org/docs/
- rclone Google Drive : https://rclone.org/drive/

### 🎓 Tutoriels
- rclone guide complet : https://rclone.org/commands/
- Forum Insync : https://forums.insynchq.com/

### 🛠️ Outils complémentaires
- RcloneBrowser : Interface graphique pour rclone
- Cron job generator : https://crontab.guru

---

## Conclusion

**Pour débutants :** **Insync** est l'option la plus simple et vaut largement son prix (~30€) pour une expérience fluide et sans prise de tête.

**Pour utilisateurs techniques :** **rclone** offre une solution gratuite et ultra-puissante avec un peu d'apprentissage.

**Pour accès occasionnel :** **GNOME Online Accounts** ou l'interface web Google Drive suffisent amplement.

Quelle que soit la solution choisie, vous pouvez continuer à utiliser Google Drive sur Linux Mint sans problème ! 🚀

**Prochaine étape :** Chapitre 10.4 pour découvrir Dropbox, OneDrive et d'autres services cloud.

---

**Bon cloud computing ! ☁️**

⏭️ [Dropbox, OneDrive et autres](/10-cloud-et-synchronisation/04-dropbox-onedrive-et-autres.md)
