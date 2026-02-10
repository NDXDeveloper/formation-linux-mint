🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 10.5 Synchronisation entre appareils (Syncthing)

## Introduction

**Syncthing** est une solution de synchronisation de fichiers **peer-to-peer** (pair-à-pair) complètement différente des services cloud traditionnels.

### Qu'est-ce que le peer-to-peer (P2P) ?

**Analogie simple :**
- ☁️ **Services cloud traditionnels** (Dropbox, Google Drive) : Vos fichiers passent par un serveur central (comme un entrepôt)
- 🔄 **Syncthing (P2P)** : Vos appareils communiquent **directement** entre eux (comme se passer un objet de main en main)

**Schéma conceptuel :**

```
Cloud traditionnel :  
PC 1 → Serveur Google/Dropbox → PC 2  
      ↓
  Smartphone

Syncthing (P2P) :  
PC 1 ←→ PC 2  
  ↕      ↕
Smartphone
```

Avec Syncthing, il n'y a **aucun serveur intermédiaire**. Vos appareils se synchronisent directement entre eux.

---

## Pourquoi utiliser Syncthing ?

### Avantages

- ✅ **Gratuit et open source** (FOSS)
- ✅ **Pas de serveur central** → Vos données restent chez vous
- ✅ **Aucune limite de stockage** (limité uniquement par vos disques)
- ✅ **Vie privée totale** → Personne ne peut accéder à vos données
- ✅ **Chiffrement de bout en bout** par défaut
- ✅ **Pas d'abonnement** ni de frais
- ✅ **Synchronisation rapide** sur réseau local (LAN)
- ✅ **Multi-plateforme** (Linux, Windows, macOS, Android, BSD)
- ✅ **Gestion fine des permissions** et versions
- ✅ **Pas de quota** ni de limitation

### Inconvénients

- ❌ **Appareils doivent être allumés** pour synchroniser
- ❌ **Pas de stockage cloud externe** (uniquement entre vos appareils)
- ❌ **Configuration initiale plus technique** que Dropbox
- ❌ **Interface moins intuitive** pour débutants
- ❌ **Pas d'accès web** comme Google Drive
- ❌ **Synchronisation dépend de vos appareils** (si tous éteints, pas de synchro)

---

## Cas d'usage parfaits pour Syncthing

### ✅ Scénarios idéaux

1. **Synchroniser PC fixe ↔ Laptop ↔ Smartphone**
   - Vos documents accessibles partout
   - Pas besoin de cloud payant

2. **Sauvegarde automatique entre ordinateurs**
   - PC principal → PC de backup
   - Synchronisation continue

3. **Partage de fichiers en famille**
   - Synchroniser des photos/vidéos
   - Album photo familial synchronisé

4. **Synchronisation sur réseau local ultra-rapide**
   - Transferts à vitesse Gigabit
   - Pas de limite de bande passante Internet

5. **Remplacement de services cloud**
   - Pour ceux qui refusent Dropbox/Google
   - Contrôle total de leurs données

### ❌ Scénarios moins adaptés

1. **Besoin d'accéder depuis n'importe où** sans appareil personnel
   - Mieux : Service cloud classique

2. **Tous les appareils souvent éteints**
   - La synchronisation ne fonctionnera pas

3. **Partage avec des personnes externes**
   - Mieux : Lien Dropbox/Google Drive

4. **Sauvegarde unique** (besoin d'un stockage permanent)
   - Mieux : Cloud externe ou NAS

---

## Installation de Syncthing sur Linux Mint

### Méthode 1 : Via les dépôts officiels (recommandé)

```bash
# Ajouter la clé GPG officielle
sudo curl -o /usr/share/keyrings/syncthing-archive-keyring.gpg https://syncthing.net/release-key.gpg

# Ajouter le dépôt Syncthing
echo "deb [signed-by=/usr/share/keyrings/syncthing-archive-keyring.gpg] https://apt.syncthing.net/ syncthing stable" | sudo tee /etc/apt/sources.list.d/syncthing.list

# Mettre à jour et installer
sudo apt update  
sudo apt install syncthing  
```

### Méthode 2 : Via le gestionnaire de logiciels

1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez **"syncthing"**
3. Installez **Syncthing** ou **Syncthing-GTK** (interface graphique)
4. Cliquez sur **Installer**

**Note :** Syncthing de base fonctionne via interface web. Syncthing-GTK ajoute une interface graphique native.

### Méthode 3 : Version portable (AppImage/binaire)

```bash
# Télécharger le binaire depuis le site officiel
wget https://github.com/syncthing/syncthing/releases/download/v1.27.0/syncthing-linux-amd64-v1.27.0.tar.gz

# Extraire
tar -xzf syncthing-linux-amd64-v1.27.0.tar.gz

# Lancer
cd syncthing-linux-amd64-v1.27.0
./syncthing
```

---

## Premier lancement et configuration

### Démarrer Syncthing

**En ligne de commande :**
```bash
syncthing
```

**Ou depuis le menu :**
- Menu → Internet → Syncthing (si Syncthing-GTK installé)

### Interface web

1. **Syncthing se lance** et ouvre automatiquement votre navigateur
2. **URL par défaut :** `http://127.0.0.1:8384`
3. **Interface web** apparaît (c'est votre tableau de bord)

**Si le navigateur ne s'ouvre pas automatiquement :**
- Ouvrez manuellement : `http://localhost:8384`

---

### Configuration initiale (première fois)

#### Étape 1 : Sécuriser l'interface

Au premier lancement, Syncthing recommande de **sécuriser l'interface web**.

**Actions :**
1. Cliquez sur **Settings** (en haut à droite) → **GUI**
2. **GUI Authentication User** : Choisissez un nom d'utilisateur
3. **GUI Authentication Password** : Choisissez un mot de passe fort
4. Cliquez sur **Save**

**Pourquoi ?** Pour empêcher quiconque sur votre réseau d'accéder à Syncthing.

#### Étape 2 : Configurer le nom de l'appareil

1. **Actions** → **Settings** → **General**
2. **Device Name** : Donnez un nom explicite à cet appareil
   - Exemple : "PC-Bureau-Linux", "Laptop-Travail", "PC-Chambre"
3. **Save**

**Important :** Un nom clair aide à identifier vos appareils.

#### Étape 3 : Activer le démarrage automatique

Pour que Syncthing démarre avec votre système :

**Méthode systemd (recommandé) :**
```bash
# Activer Syncthing au démarrage pour votre utilisateur
systemctl --user enable syncthing.service  
systemctl --user start syncthing.service  

# Vérifier le statut
systemctl --user status syncthing.service
```

**Méthode alternative (application de démarrage) :**
1. Menu → **Préférences** → **Applications au démarrage**
2. Cliquez sur **Ajouter**
3. **Nom :** Syncthing
4. **Commande :** `syncthing`
5. **Enregistrer**

---

## Ajouter un autre appareil

Pour synchroniser des fichiers, vous devez **connecter au moins 2 appareils**.

### Installer Syncthing sur l'autre appareil

**Sur le 2ème appareil** (PC, laptop, smartphone) :
- **Linux/Windows/Mac** : Téléchargez sur https://syncthing.net
- **Android** : Installez depuis Google Play Store ou F-Droid
- **iOS** : Utilisez Möbius Sync (application tierce)

### Processus de connexion

Les appareils Syncthing s'identifient mutuellement via leur **Device ID** (identifiant unique).

#### Sur l'appareil 1 (Linux Mint) :

1. Interface web → **Actions** → **Show ID**
2. Un **QR Code** et un **Device ID** apparaissent
3. **Gardez cette fenêtre ouverte** ou notez le Device ID

#### Sur l'appareil 2 :

**Scénario A : Ajouter depuis l'appareil 2**
1. Interface Syncthing de l'appareil 2
2. **Add Remote Device**
3. **Scannez le QR Code** de l'appareil 1 (pratique sur smartphone)
4. Ou **collez le Device ID** manuellement
5. Donnez un nom à l'appareil (ex: "PC-Linux-Bureau")
6. **Sharing** : Sélectionnez les dossiers à partager (on y revient)
7. Cliquez sur **Save**

**Scénario B : Accepter une demande automatique**

Syncthing détecte automatiquement les appareils sur le même réseau local.

1. L'appareil 1 **détecte automatiquement** l'appareil 2
2. Une **notification** apparaît : "New Device"
3. Cliquez sur **Add Device**
4. Vérifiez le Device ID
5. Donnez un nom
6. **Save**

⚠️ **Important :** Vérifiez toujours le Device ID avant d'accepter un appareil !

---

## Créer et partager un dossier

### Créer un dossier partagé

#### Sur l'appareil 1 (Linux Mint) :

1. **Add Folder** (bouton en bas à droite)
2. **General tab :**
   - **Folder Label** : Nom descriptif (ex: "Documents-Travail", "Photos-Famille")
   - **Folder Path** : Chemin du dossier à synchroniser
     - Exemple : `/home/votre-nom/Documents/Sync`
     - Ou cliquez sur **Browse** pour sélectionner

3. **Sharing tab :**
   - **Cochez les appareils** avec qui partager ce dossier
   - Exemple : Cochez "Laptop-Travail" et "Smartphone"

4. **File Versioning tab (optionnel) :**
   - Activez le versioning si vous voulez garder l'historique
   - **Simple File Versioning** : Garde les versions précédentes
   - **Trash Can** : Déplace les fichiers supprimés dans une corbeille

5. **Cliquez sur Save**

#### Sur l'appareil 2 :

1. Une **notification** apparaît : "Folder partage demandé"
2. Cliquez sur **Add**
3. Choisissez où stocker ce dossier localement
4. **Save**

**C'est tout !** Les fichiers commencent à se synchroniser. 🎉

---

## Comprendre l'interface web

### Vue d'ensemble

**Interface principale divisée en 3 sections :**

#### 1. **Folders (Dossiers)**
Liste tous vos dossiers synchronisés.

**Informations affichées :**
- 📁 Nom du dossier
- 📊 État : "Up to Date" (à jour) ou "Syncing..." (en cours)
- 💾 Taille totale
- 📝 Nombre de fichiers
- 🔄 Appareils qui le partagent

**Actions possibles :**
- **Edit** : Modifier les paramètres du dossier
- **Rescan** : Forcer une nouvelle analyse
- **Override Changes** : Écraser les modifications (prudence !)
- **Remove** : Supprimer le dossier de Syncthing

#### 2. **Remote Devices (Appareils distants)**
Liste tous les appareils connectés.

**Informations :**
- 💻 Nom de l'appareil
- 🟢 État : Connected (connecté) ou Disconnected (déconnecté)
- 📊 Statistiques de synchronisation
- 🌐 Adresse IP (si connecté)

**Actions :**
- **Edit** : Modifier les paramètres
- **Pause** : Mettre en pause la synchronisation
- **Remove** : Retirer l'appareil

#### 3. **This Device (Cet appareil)**
Informations sur l'appareil local.

**Données affichées :**
- 📊 Statistiques globales
- 💾 Espace utilisé
- 🔄 Taux de transfert

---

### Barre d'état (en haut)

**Indicateurs :**
- 🟢 **Vert** : Tout fonctionne bien
- 🔵 **Bleu** : Synchronisation en cours
- 🟡 **Jaune** : Avertissements (attention requise)
- 🔴 **Rouge** : Erreurs (action nécessaire)

**Icônes :**
- ⏸️ **Pause** : Mettre toute synchronisation en pause
- 🔄 **Rescan All** : Forcer l'analyse de tous les dossiers
- ⚙️ **Settings** : Accéder aux paramètres
- 🆘 **Actions** : Menu d'actions diverses

---

## Types de synchronisation

Syncthing propose différents modes de partage de dossiers.

### 1. Send & Receive (Envoyer et Recevoir)

**Mode par défaut** : Synchronisation bidirectionnelle complète.

- Modifications de l'appareil 1 → Appareil 2
- Modifications de l'appareil 2 → Appareil 1
- **Comme Dropbox**, synchronisation dans les deux sens

**Quand l'utiliser :** Travailler sur les mêmes fichiers depuis plusieurs appareils.

---

### 2. Send Only (Envoi uniquement)

Cet appareil **envoie** les fichiers mais **n'accepte pas** les modifications.

**Exemple :** PC principal en "Send Only" → Laptop en "Receive Only"
- PC modifie les fichiers → Laptop les reçoit
- Laptop NE PEUT PAS modifier les fichiers sur le PC

**Quand l'utiliser :**
- Sauvegardes unidirectionnelles
- Distribuer des fichiers sans risque de modification

---

### 3. Receive Only (Réception uniquement)

Cet appareil **reçoit** les fichiers mais **ne les envoie pas**.

**Exemple :** Smartphone (photos) en "Send Only" → PC en "Receive Only"
- Smartphone envoie photos → PC les reçoit
- PC ne peut pas modifier/supprimer les photos sur le smartphone

**Quand l'utiliser :**
- Backup automatique de photos
- Archives en lecture seule

---

### Tableau récapitulatif

| Mode | Modifications locales | Modifications distantes | Usage |
|------|----------------------|------------------------|--------|
| **Send & Receive** | ✅ Envoyées | ✅ Reçues | Travail collaboratif |
| **Send Only** | ✅ Envoyées | ❌ Ignorées | Source principale |
| **Receive Only** | ❌ Ignorées | ✅ Reçues | Copie de backup |

---

## Versioning (Historique des versions)

Le **versioning** permet de conserver les anciennes versions de fichiers.

### Types de versioning

#### 1. **Trash Can File Versioning**

Les fichiers supprimés/modifiés vont dans une **corbeille**.

**Paramètres :**
- **Clean out after (jours)** : Combien de jours garder (ex: 30)

**Utilisation :**
- Protection contre suppressions accidentelles
- Récupération facile

#### 2. **Simple File Versioning**

Garde un **nombre défini** d'anciennes versions.

**Paramètres :**
- **Keep Versions** : Nombre de versions à garder (ex: 5)

**Exemple :** Vous modifiez `document.txt` 10 fois, Syncthing garde les 5 dernières versions.

#### 3. **Staggered File Versioning**

Versioning **intelligent** : garde plus de versions récentes, moins d'anciennes.

**Paramètres :**
- **Maximum Age (jours)** : Durée maximale de conservation
- **Versions Path** : Où stocker les versions

**Utilisation :** Équilibre entre historique et espace disque.

#### 4. **External File Versioning**

Utilise un **script personnalisé** pour gérer les versions.

**Pour utilisateurs avancés** : Intégration avec des outils de backup externes.

---

### Configuration du versioning

1. **Edit Folder** → **File Versioning tab**
2. Sélectionnez le type de versioning
3. Configurez les paramètres
4. **Save**

**Recommandation débutants :** **Trash Can** avec 30 jours de rétention.

---

## Paramètres avancés

### Settings → General

**Options importantes :**

- **Device Name** : Nom de cet appareil
- **Default Folder Path** : Où créer les nouveaux dossiers par défaut
- **Theme** : Light/Dark (thème clair/sombre)
- **Rate Limits** : Limiter la bande passante upload/download

---

### Settings → Connections

**Contrôle des connexions réseau :**

#### Listen Addresses
- Ports utilisés par Syncthing
- Défaut : `default` (automatique)
- **Ne modifiez pas** sauf besoin spécifique

#### Global Discovery
- ✅ **Activé** : Vos appareils peuvent se trouver via Internet
- ❌ **Désactivé** : Synchronisation uniquement sur réseau local

#### Local Discovery
- ✅ **Activé** : Détection automatique sur le réseau local
- Recommandé de garder activé

#### NAT Traversal
- Aide à connecter des appareils derrière des routeurs
- ✅ Gardez activé

#### Relay
- Serveurs relais publics pour connecter des appareils sans connexion directe
- ✅ Activé par défaut
- ⚠️ Plus lent qu'une connexion directe

---

### Settings → GUI

**Interface web :**

- **GUI Listen Address** : `127.0.0.1:8384` (local seulement)
- **GUI Authentication** : Nom d'utilisateur/mot de passe (important !)
- **GUI Theme** : Thème de l'interface
- **Enable HTTPS** : Activer SSL (recommandé si accès depuis réseau)

---

## Synchronisation avec différents systèmes

### Android

1. **Installer Syncthing** depuis Play Store ou F-Droid
2. **Ouvrir l'application**
3. **Menu** → **Show device ID**
4. **Scanner le QR Code** de votre PC Linux
5. **Accepter** la connexion sur le PC
6. **Ajouter un dossier** (ex: Camera pour synchroniser photos)
7. **Partager** avec le PC

**Astuce :** Activez "Sync only on Wi-Fi" pour économiser les données mobiles.

---

### Windows

1. **Télécharger** : https://syncthing.net
2. **Installer** SyncTrayzor (interface graphique recommandée pour Windows)
3. **Configurer** comme sur Linux (interface web identique)
4. **Connecter** aux autres appareils

---

### macOS

1. **Télécharger** : https://syncthing.net
2. **Installer** Syncthing-macOS (wrapper GUI)
3. Configuration identique

---

### iOS (iPhone/iPad)

⚠️ **Pas d'application officielle** Syncthing pour iOS.

**Alternative :** **Möbius Sync** (application tierce, payante)

Limitations iOS rendent la synchronisation compliquée (restrictions système).

---

## Cas d'usage pratiques

### Cas 1 : Synchroniser Documents entre PC et Laptop

**Configuration :**
- **PC fixe** : `~/Documents` en "Send & Receive"
- **Laptop** : `~/Documents` en "Send & Receive"

**Résultat :** Travaillez sur n'importe quel appareil, les fichiers sont toujours à jour.

---

### Cas 2 : Backup automatique des photos smartphone

**Configuration :**
- **Smartphone** : Dossier `Camera` en "Send Only"
- **PC Linux** : `~/Photos/Backup-Phone` en "Receive Only"

**Résultat :** Photos sauvegardées automatiquement sur PC quand smartphone connecté au Wi-Fi.

---

### Cas 3 : Synchroniser musique vers smartphone

**Configuration :**
- **PC** : `~/Musique` en "Send Only"
- **Smartphone** : `/sdcard/Music` en "Receive Only"

**Résultat :** Ajoutez de la musique sur PC, elle apparaît automatiquement sur smartphone.

---

### Cas 4 : Backup entre 2 PC

**Configuration :**
- **PC principal** : `~` (dossier home) en "Send Only"
- **PC de backup** : `/media/backup/PC-principal` en "Receive Only"

**Résultat :** Backup automatique continu de votre PC principal.

---

### Cas 5 : Partage de fichiers familial

**Configuration :**
- Créez un dossier `Photos-Famille` partagé entre tous les appareils
- Mode "Send & Receive" sur tous
- Chacun peut ajouter des photos

**Résultat :** Album photo familial synchronisé en temps réel.

---

## Syncthing sur réseau local (LAN)

### Avantages de la synchronisation LAN

Quand vos appareils sont sur le **même réseau local** (Wi-Fi maison) :

- ✅ **Vitesse maximale** : Gigabit (jusqu'à 125 Mo/s)
- ✅ **Pas de limite de bande passante** Internet
- ✅ **Pas de consommation** de quota Internet
- ✅ **Latence minimale**

**Exemple :** Transférer 100 Go de photos :
- Via Internet (20 Mbps upload) : ~11 heures
- Via LAN (1 Gbps) : ~15 minutes

### Configuration optimale LAN

1. **Assurez-vous que Local Discovery est activé**
   - Settings → Connections → Local Discovery ✅

2. **Vérifiez la connexion directe**
   - Remote Devices → Cliquez sur un appareil
   - Regardez l'adresse : doit être une IP locale (192.168.x.x)

3. **Désactivez le Relay** (optionnel, pour forcer connexion directe)
   - Settings → Connections → Enable Relaying ❌

---

## Sécurité et confidentialité

### Chiffrement

**Syncthing chiffre automatiquement toutes les communications** entre appareils.

- **TLS 1.3** : Chiffrement de transport
- **Certificats auto-signés** : Chaque appareil a son certificat unique
- **Device ID** : Dérivé du certificat (impossible de falsifier)

**Résultat :** Personne ne peut intercepter vos fichiers pendant le transfert.

---

### Authentification

**Device ID = Clé publique** de l'appareil.

**Processus sécurisé :**
1. Vous acceptez uniquement les appareils dont vous **vérifiez le Device ID**
2. Impossible pour un tiers de se faire passer pour votre appareil
3. Même sur réseau public, connexion sécurisée

**Bonne pratique :** Vérifiez toujours le Device ID avant d'accepter un appareil.

---

### Pas de serveur central

- ✅ **Vos données ne transitent jamais** par des serveurs tiers
- ✅ **Impossible pour Syncthing ou un tiers** d'accéder à vos fichiers
- ✅ **Vous contrôlez totalement** où vos données sont stockées

**Exception :** Serveurs de découverte (discovery) et relais (relay) publics.

#### Serveurs de découverte

**Rôle :** Aident vos appareils à se trouver via Internet.

**Données transmises :**
- ✅ Device ID
- ✅ Adresse IP publique
- ❌ **Aucun fichier**
- ❌ **Aucun nom de fichier**
- ❌ **Aucune donnée sensible**

**Désactiver :** Settings → Connections → Global Discovery ❌

#### Serveurs relais (Relay)

**Rôle :** Relaient les données si connexion directe impossible.

**Chiffrement :** Données **toujours chiffrées** même via relay.

**Désactiver :** Settings → Connections → Enable Relaying ❌

**Note :** Désactiver rend la synchronisation impossible si pas de connexion directe.

---

### Configuration sécurisée

**Checklist sécurité :**

1. ✅ **GUI Authentication activée** (nom d'utilisateur + mot de passe)
2. ✅ **HTTPS sur GUI** si accès depuis réseau
3. ✅ **Vérifier Device ID** avant d'ajouter un appareil
4. ✅ **Partage sélectif** : Ne partagez que les dossiers nécessaires
5. ✅ **Versioning activé** pour récupération en cas d'erreur
6. ✅ **Firewall configuré** correctement (UFW)

---

## Performances et optimisation

### Facteurs influençant la vitesse

1. **Réseau** : LAN (rapide) vs Internet (plus lent)
2. **Nombre de fichiers** : Beaucoup de petits fichiers = plus lent
3. **Type de stockage** : SSD (rapide) vs HDD (plus lent)
4. **CPU** : Chiffrement/déchiffrement consomme du CPU
5. **Nombre d'appareils** : Plus d'appareils = plus de connexions

---

### Optimiser les performances

#### 1. Limiter le nombre de fichiers surveillés

**Ignorer des fichiers/dossiers :**

Edit Folder → **Ignore Patterns**

**Exemples de patterns :**
```
# Ignorer tous les fichiers temporaires
*.tmp
*.temp
~*

# Ignorer node_modules (développement)
node_modules

# Ignorer les caches
.cache
Cache  
Thumbs.db  
.DS_Store

# Ignorer les fichiers volumineux
*.iso
*.vmdk
```

#### 2. Ajuster les paramètres de scan

Settings → Advanced → **Folder Configuration**

- **Rescan Interval** : Fréquence de vérification (défaut : 60s)
  - Augmentez à 300s (5 min) pour moins de charge CPU
  - Diminuez à 10s pour synchronisation quasi-instantanée

#### 3. Limiter la bande passante (optionnel)

Settings → Connections → **Rate Limits**

- **Download Rate** : Limite en Ko/s
- **Upload Rate** : Limite en Ko/s

**Utile si :** Syncthing sature votre connexion Internet.

---

## Dépannage

### Problème : Appareils ne se connectent pas

**Vérifications :**

1. ✅ **Les deux appareils sont allumés** et Syncthing lancé
2. ✅ **Device ID correct** des deux côtés
3. ✅ **Connexion Internet** active (si pas sur LAN)
4. ✅ **Pare-feu** n'empêche pas Syncthing
5. ✅ **Global Discovery** activé (si connexion via Internet)

**Solution pare-feu (UFW) :**
```bash
# Autoriser Syncthing
sudo ufw allow syncthing

# Ou autoriser les ports spécifiques
sudo ufw allow 22000/tcp  # Transfert de données  
sudo ufw allow 21027/udp  # Local discovery  
```

---

### Problème : Synchronisation bloquée

**Causes possibles :**
- Fichier verrouillé/ouvert
- Permissions insuffisantes
- Conflit de versions

**Solutions :**
1. **Rescan** le dossier (bouton dans l'interface)
2. Vérifiez les **logs** : Actions → Logs
3. **Redémarrez Syncthing** :
   ```bash
   systemctl --user restart syncthing
   ```

---

### Problème : "Out of Sync" (Désynchronisé)

**Signification :** Les fichiers locaux diffèrent de ceux attendus.

**Solution :**
1. Edit Folder → **Advanced** → **Override Changes**
2. Choisissez la source de vérité (local ou distant)
3. Les fichiers seront resynchronisés

⚠️ **Attention :** Peut écraser des modifications non synchronisées.

---

### Problème : Conflit de fichiers

**Format :** `fichier.sync-conflict-DATE-TIME.ext`

**Cause :** Fichier modifié simultanément sur plusieurs appareils.

**Solution :**
1. Ouvrez les deux versions
2. Fusionnez manuellement les modifications
3. Supprimez le fichier conflit
4. Gardez la version fusionnée

**Prévention :** Évitez de modifier le même fichier simultanément.

---

### Problème : Syncthing consomme trop de CPU

**Causes :**
- Nombreux fichiers à scanner
- Synchronisation intensive en cours

**Solutions :**
1. Augmentez **Rescan Interval** (Settings → Advanced)
2. Ignorez les dossiers inutiles (node_modules, cache, etc.)
3. Limitez le nombre de dossiers synchronisés

---

### Problème : Synchronisation lente

**Vérifications :**
1. ✅ Connexion réseau (Wi-Fi vs Ethernet)
2. ✅ Connexion directe (pas via relay)
   - Remote Device → Regardez l'adresse
   - Doit être IP locale ou publique, pas "relay"
3. ✅ Pas de limitation de bande passante active

**Optimisation :**
- Synchronisez sur LAN quand possible
- Utilisez Ethernet au lieu de Wi-Fi
- Compressez les gros fichiers avant synchronisation

---

## Comparaison : Syncthing vs autres solutions

| Critère | Syncthing | Dropbox | Google Drive | Nextcloud |
|---------|-----------|---------|--------------|-----------|
| **Prix** | Gratuit | 2 Go gratuit | 15 Go gratuit | Gratuit (hébergement à payer) |
| **Serveur central** | ❌ Non | ✅ Oui | ✅ Oui | ✅ Oui |
| **Limite stockage** | ∞ (vos disques) | 2 Go-2 To | 15 Go-2 To | ∞ (votre serveur) |
| **Vie privée** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Facilité** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Accès sans appareil** | ❌ Non | ✅ Web | ✅ Web | ✅ Web |
| **Vitesse (LAN)** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐ |
| **Open source** | ✅ Oui | ❌ Non | ❌ Non | ✅ Oui |

---

## Bonnes pratiques

### 🗂️ Organisation

1. **Nommage clair** des dossiers
   - ✅ "Documents-Travail", "Photos-Vacances-2024"
   - ❌ "Dossier1", "Nouveau dossier"

2. **Synchronisation sélective**
   - Ne synchronisez que ce dont vous avez besoin
   - Évitez de synchroniser tout votre disque

3. **Structure cohérente** entre appareils
   - Utilisez les mêmes chemins si possible
   - Facilite la gestion

---

### 💾 Sauvegarde

**Syncthing ≠ Sauvegarde !**

**Pourquoi ?**
- Suppression sur appareil 1 → Suppression sur appareil 2
- Malware/ransomware → Se propage à tous les appareils
- Pas de copie permanente hors ligne

**Solution :** Combinez Syncthing avec :
1. **Timeshift** : Snapshots système
2. **Versioning** : Activé dans Syncthing
3. **Backup externe** : Disque dur déconnecté ou cloud

**Règle 3-2-1 :**
- **3** copies de vos données
- Sur **2** supports différents
- **1** copie hors site

---

### 🔒 Sécurité

1. **Vérifiez Device ID** avant d'accepter
2. **GUI Authentication** activée
3. **Partagez seulement** ce qui est nécessaire
4. **Mots de passe forts** sur tous les appareils
5. **Chiffrez les appareils** (LUKS sur Linux, BitLocker sur Windows)

---

### ⚡ Performance

1. **Utilisez SSD** pour dossiers synchronisés
2. **Connexion filaire** (Ethernet) quand possible
3. **Ignorez fichiers inutiles** (.cache, node_modules, etc.)
4. **Limitez à 3-5 appareils** maximum par dossier

---

## Syncthing-GTK (Interface graphique)

Pour ceux qui préfèrent une **interface graphique native** au lieu de l'interface web :

### Installation

```bash
sudo apt install syncthing-gtk
```

### Avantages

- ✅ **Intégration système** (icône dans la barre des tâches)
- ✅ **Notifications desktop** natives
- ✅ **Plus intuitif** pour débutants
- ✅ **Gestion fichiers** par glisser-déposer

### Utilisation

1. Lancez **Syncthing-GTK** depuis le menu
2. Interface similaire à Dropbox/MEGA
3. Toutes les fonctionnalités de Syncthing accessibles
4. Interface web toujours disponible si besoin

---

## Ressources et documentation

### 📚 Documentation officielle

- Site officiel : https://syncthing.net
- Documentation complète : https://docs.syncthing.net
- FAQ : https://docs.syncthing.net/users/faq.html

### 🎓 Tutoriels

- Getting Started : https://docs.syncthing.net/intro/getting-started.html
- Vidéos tutoriels : Cherchez "Syncthing tutorial" sur YouTube

### 💬 Communauté

- Forum officiel : https://forum.syncthing.net
- Reddit : r/Syncthing
- GitHub : https://github.com/syncthing/syncthing

### 🛠️ Outils complémentaires

- **Syncthing-Android** : Application mobile officielle
- **SyncTrayzor** : Interface Windows
- **syncthing-macos** : Wrapper macOS

---

## Alternatives à Syncthing

Si Syncthing ne correspond pas à vos besoins :

### **Resilio Sync** (ex-BitTorrent Sync)

- Similaire à Syncthing (P2P)
- Interface plus moderne
- ❌ Propriétaire (non open source)
- Gratuit pour usage personnel

### **Seafile**

- Client-serveur (comme Nextcloud)
- Meilleure performance pour gros fichiers
- Moins d'applications intégrées

### **Synology Drive** / **QNAP Sync**

- Si vous possédez un NAS de ces marques
- Intégration native

---

## Conclusion

**Syncthing est parfait pour :**

- ✅ Ceux qui veulent **contrôle total** de leurs données
- ✅ Synchroniser entre **appareils personnels** (PC, laptop, smartphone)
- ✅ Éviter les **abonnements mensuels**
- ✅ **Vie privée maximale** (pas de serveur tiers)
- ✅ **Synchronisation LAN ultra-rapide**
- ✅ **Aucune limite de stockage**

**Syncthing n'est PAS idéal pour :**

- ❌ Accès depuis **n'importe où** sans appareil personnel
- ❌ Partage avec des **personnes externes**
- ❌ Besoin d'une **interface web** comme Google Drive
- ❌ Tous vos appareils sont **souvent éteints**

**Recommandation :**

- **Usage personnel uniquement** : Syncthing est excellent
- **Besoin de partage externe** : Combinez avec Dropbox/Google Drive
- **Meilleur des deux mondes** : Syncthing pour vos appareils + cloud pour partage

**Syncthing complète parfaitement** une stratégie cloud multi-services :
- Nextcloud : Auto-hébergement avec interface web
- Syncthing : Synchronisation rapide entre vos appareils
- Dropbox/MEGA : Partage avec l'extérieur

Vous avez maintenant toutes les clés pour maîtriser la synchronisation entre vos appareils avec Syncthing ! 🔄

---

**Bon sync ! 🚀**

⏭️ [Gestion des utilisateurs et sécurité](/11-gestion-des-utilisateurs-et-securite/README.md)
