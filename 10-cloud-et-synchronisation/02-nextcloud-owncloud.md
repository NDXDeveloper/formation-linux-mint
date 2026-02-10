🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 10.2 Nextcloud / ownCloud (auto-hébergé)

## Introduction

**Nextcloud** et **ownCloud** sont des solutions de cloud personnel open source qui vous permettent de créer votre propre service de stockage cloud, similaire à Google Drive ou Dropbox, mais avec un contrôle total sur vos données.

### Différence entre Nextcloud et ownCloud

- **ownCloud** : Le projet original, créé en 2010
- **Nextcloud** : Une version dérivée (fork) créée en 2016 par l'équipe originale d'ownCloud

**Aujourd'hui, Nextcloud est plus populaire** et activement développé. La plupart des utilisateurs choisissent Nextcloud, c'est donc sur lui que nous nous concentrerons principalement dans ce chapitre.

---

## Qu'est-ce que l'auto-hébergement ?

### Définition simple

**Auto-héberger** signifie installer et gérer votre propre serveur cloud au lieu d'utiliser les serveurs d'une entreprise (Google, Dropbox, etc.).

### Analogie

Imaginez la différence entre :
- 🏢 **Louer un appartement** (Google Drive, Dropbox) : Vous payez un loyer, le propriétaire gère l'immeuble
- 🏠 **Posséder votre maison** (Nextcloud auto-hébergé) : Vous êtes propriétaire, vous gérez tout, mais c'est vous qui décidez

### Avantages de l'auto-hébergement

- ✅ **Contrôle total** de vos données
- ✅ **Vie privée maximale** (vos fichiers restent chez vous)
- ✅ **Aucune limite de stockage** (selon votre matériel)
- ✅ **Pas d'abonnement mensuel** après l'installation
- ✅ **Personnalisation complète**
- ✅ **Indépendance** vis-à-vis des grandes entreprises

### Inconvénients de l'auto-hébergement

- ❌ **Connaissances techniques nécessaires**
- ❌ **Responsabilité de la maintenance** et des sauvegardes
- ❌ **Coût initial** (matériel, électricité)
- ❌ **Besoin d'une connexion Internet** stable et rapide
- ❌ **Gestion de la sécurité** à votre charge

---

## Les différentes options pour utiliser Nextcloud

### Option 1 : Auto-hébergement complet (avancé)

Vous installez Nextcloud sur votre propre serveur à la maison.

**Matériel nécessaire :**
- Un ordinateur dédié, Raspberry Pi, ou vieux PC
- Une connexion Internet stable avec bonne vitesse d'upload
- Un disque dur de stockage

**Prérequis techniques :**
- Installation d'un serveur Linux (Ubuntu Server, Debian)
- Configuration d'Apache/Nginx, PHP, base de données
- Configuration du routeur (ouverture de ports)
- Nom de domaine (optionnel mais recommandé)
- Certificat SSL pour HTTPS

**Pour qui ?** Utilisateurs avancés ou motivés à apprendre l'administration système.

---

### Option 2 : Hébergement mutualisé (recommandé pour débutants)

Vous louez un espace chez un hébergeur qui propose Nextcloud pré-installé.

**Avantages :**
- ✅ Installation automatique en un clic
- ✅ Maintenance technique gérée
- ✅ Sauvegardes automatiques
- ✅ Support technique disponible
- ✅ Pas de configuration réseau compliquée

**Coût :** Entre 3€ et 10€ par mois selon l'espace

**Hébergeurs recommandés proposant Nextcloud :**
- **Hetzner** (Allemagne) - À partir de 3,90€/mois
- **Infomaniak** (Suisse) - À partir de 5,75€/mois, 100% renouvelable
- **OVH** (France) - À partir de 3,99€/mois
- **Contabo** (Allemagne) - À partir de 4,99€/mois
- **Ionos** (1&1) - À partir de 5€/mois

**Pour qui ?** Débutants qui veulent Nextcloud sans complications techniques.

---

### Option 3 : Solutions clé en main

Des appareils pré-configurés avec Nextcloud installé.

**Exemples :**
- **Nextcloud Box** (actuellement discontinued)
- **Nextcloud Hub** (offres professionnelles)
- **NAS Synology/QNAP** avec Nextcloud dans leur store d'applications

**Pour qui ?** Ceux qui veulent du plug-and-play.

---

## Installation du client Nextcloud sous Linux Mint

Quelle que soit l'option choisie (auto-hébergé ou hébergeur), vous aurez besoin du **client de synchronisation** sur votre Linux Mint.

### Méthode 1 : Via le Gestionnaire de logiciels (recommandé)

1. Ouvrez le **Gestionnaire de logiciels**
2. Dans la barre de recherche, tapez `nextcloud`
3. Cliquez sur **Nextcloud Desktop Client**
4. Cliquez sur **Installer**
5. Entrez votre mot de passe administrateur

C'est tout ! Le client est installé.

---

### Méthode 2 : Via le Terminal (version officielle PPA)

Si vous préférez avoir la version la plus récente directement depuis le dépôt officiel :

```bash
# Ajouter le dépôt officiel Nextcloud
sudo add-apt-repository ppa:nextcloud-devs/client

# Mettre à jour la liste des paquets
sudo apt update

# Installer le client Nextcloud
sudo apt install nextcloud-desktop
```

Entrez votre mot de passe lorsque demandé.

---

### Méthode 3 : Via AppImage (portable)

Si vous voulez une version portable sans installation :

1. Rendez-vous sur : https://nextcloud.com/install/#install-clients
2. Téléchargez le fichier **AppImage** pour Linux
3. Rendez le fichier exécutable :
   ```bash
   chmod +x Nextcloud-*.AppImage
   ```
4. Double-cliquez dessus pour lancer Nextcloud

---

## Configuration initiale du client Nextcloud

### Première connexion

1. **Lancez l'application Nextcloud** depuis le menu
   - Menu → Internet → Nextcloud Desktop

2. **Écran de bienvenue**
   - Cliquez sur "Se connecter à Nextcloud"

3. **Entrez l'adresse de votre serveur**
   - Format : `https://votre-domaine.com` ou `https://cloud.votre-hebergeur.com`
   - Exemple : `https://cloud.infomaniak.com` ou `https://nextcloud.mondomaine.fr`

4. **Connexion via navigateur**
   - Une page web s'ouvre automatiquement
   - Connectez-vous avec vos identifiants Nextcloud
   - Autorisez l'accès au client de bureau

5. **Configuration de la synchronisation**
   - Choisissez le **dossier local** où synchroniser vos fichiers
   - Par défaut : `/home/votre-nom/Nextcloud`
   - Vous pouvez le modifier si besoin

6. **Sélection des dossiers**
   - Vous pouvez choisir de synchroniser tous les dossiers ou seulement certains
   - Pour débuter, laissez "Tout synchroniser"

7. **Finalisez**
   - Cliquez sur "Se connecter"
   - La synchronisation démarre automatiquement

---

## Interface du client Nextcloud

### Icône dans la barre des tâches

Une fois configuré, Nextcloud apparaît dans votre **barre d'état système** (system tray) en haut à droite.

**Cliquez sur l'icône** pour voir :
- 📊 L'état de la synchronisation
- 📁 Accès rapide à vos fichiers
- ⚙️ Paramètres
- 🌐 Ouvrir Nextcloud dans le navigateur

---

### Le dossier Nextcloud

Un nouveau dossier `Nextcloud` est créé dans votre répertoire personnel (`/home/votre-nom/`).

**Fonctionnement :**
- Tout fichier que vous placez dans ce dossier est **automatiquement synchronisé** avec le serveur
- Les modifications sont **synchronisées en temps réel**
- Les fichiers supprimés localement sont supprimés du serveur (et vice versa)

---

## Fonctionnalités principales de Nextcloud

### 1. Synchronisation de fichiers

Le cœur de Nextcloud : vos fichiers sont automatiquement synchronisés entre tous vos appareils.

**Icônes de statut :**
- ✅ **Coche verte** : Fichier synchronisé
- 🔄 **Flèches bleues** : Synchronisation en cours
- ⚠️ **Triangle jaune** : Erreur de synchronisation
- ☁️ **Nuage** : Fichier disponible en ligne uniquement

---

### 2. Partage de fichiers

**Partager un fichier ou dossier :**

1. **Clic droit** sur un fichier/dossier dans le dossier Nextcloud
2. Sélectionnez **"Nextcloud" → "Partager"**
3. Dans l'interface web qui s'ouvre :
   - **Partage public** : Créez un lien partageable
   - **Partage avec utilisateur** : Partagez avec d'autres utilisateurs Nextcloud
   - **Protection par mot de passe** : Sécurisez le lien
   - **Date d'expiration** : Le lien expire automatiquement

---

### 3. Applications intégrées (Web)

Nextcloud propose bien plus que du simple stockage. Via l'interface web, vous avez accès à :

#### 📄 **Nextcloud Office** (Collabora ou OnlyOffice)
- Éditeur de documents type Word
- Tableur type Excel
- Présentation type PowerPoint
- Modification collaborative en temps réel

#### 📅 **Calendrier**
- Synchronisation avec vos appareils
- Partage de calendriers
- Compatible CalDAV

#### 📧 **Mail**
- Client mail intégré
- Gestion de plusieurs comptes

#### 📞 **Talk** (Nextcloud Talk)
- Messagerie instantanée
- Appels audio/vidéo
- Visioconférences
- Alternative à Zoom/Teams

#### 📝 **Notes**
- Prise de notes en markdown
- Synchronisation automatique

#### 📸 **Photos**
- Galerie photos intelligente
- Reconnaissance faciale
- Tri par date/lieu

#### 🎵 **Music**
- Lecteur audio en ligne
- Vos playlists partout

---

### 4. Synchronisation sélective

Pour économiser l'espace disque local :

1. Cliquez sur l'icône Nextcloud (barre d'état)
2. Paramètres → **Compte**
3. Cliquez sur **"Choisir ce qui est synchronisé"**
4. Décochez les dossiers que vous ne voulez pas synchroniser localement

**Astuce :** Les fichiers restent sur le serveur, vous y accédez via l'interface web.

---

### 5. Fichiers à la demande (Virtual Files)

Fonctionnalité avancée permettant de voir tous vos fichiers sans les télécharger :

1. Paramètres → **Compte**
2. Activez **"Fichiers virtuels"**
3. Les fichiers apparaissent mais ne prennent pas d'espace
4. Ils se téléchargent automatiquement quand vous les ouvrez

⚠️ **Note :** Cette fonction peut être instable sur certaines versions Linux.

---

## Configuration avancée du client

### Paramètres généraux

**Accès :** Cliquez sur l'icône Nextcloud → ⚙️ Paramètres

#### Onglet Général
- ✅ **Lancer au démarrage** : Démarre Nextcloud automatiquement avec Linux Mint
- ✅ **Notifications** : Active/désactive les notifications de synchronisation
- 📊 **Utilisation de la bande passante** : Limitez la vitesse d'upload/download

#### Onglet Compte
- Voir l'espace utilisé
- Gérer la synchronisation sélective
- Se déconnecter / Supprimer le compte

#### Onglet Réseau
- Configuration du proxy
- Limitation de bande passante automatique

---

### Ignorer certains fichiers

Créez un fichier `.sync-exclude.lst` dans votre dossier Nextcloud pour ignorer certains types de fichiers :

```
# Ignorer les fichiers temporaires
*.tmp
*.temp
~*

# Ignorer les fichiers de sauvegarde
*.bak
*~

# Ignorer les dossiers cachés
.DS_Store
Thumbs.db
```

---

## Auto-hébergement : Installation complète (pour utilisateurs avancés)

Si vous souhaitez vraiment installer Nextcloud sur votre propre serveur, voici un aperçu du processus.

### Prérequis matériel

**Minimum :**
- Processeur : Double cœur 1 GHz
- RAM : 512 Mo (2 Go recommandés)
- Stockage : Selon vos besoins (disque dur externe recommandé)
- Réseau : Connexion stable, bonne vitesse d'upload

**Matériel recommandé :**
- Raspberry Pi 4 (4 Go RAM) avec disque SSD
- Mini PC (Intel NUC, HP Mini)
- Vieux PC recyclé avec disque dur additionnel
- NAS (Synology, QNAP) avec support Docker

---

### Méthodes d'installation

#### Option A : Snap (plus simple)

```bash
# Installer Nextcloud via Snap
sudo snap install nextcloud

# Configuration initiale (créer compte admin)
sudo nextcloud.manual-install nom_admin mot_de_passe
```

**Avantages :** Installation en 2 commandes, mises à jour automatiques  
**Inconvénients :** Moins de contrôle, performances parfois moindres  

---

#### Option B : Docker (recommandé pour débutants en auto-hébergement)

```bash
# Installer Docker et Docker Compose
sudo apt update  
sudo apt install docker.io docker-compose  

# Télécharger un docker-compose.yml pour Nextcloud
# (voir documentation officielle)

# Lancer Nextcloud
docker-compose up -d
```

**Avantages :** Isolation, facilité de maintenance, portable  
**Inconvénients :** Apprentissage de Docker nécessaire  

---

#### Option C : Installation manuelle complète (utilisateurs très avancés)

1. **Installer les dépendances**
   ```bash
   sudo apt install apache2 mariadb-server php php-{gd,mysql,curl,mbstring,intl,gmp,bcmath,xml,zip,imagick}
   ```

2. **Configurer la base de données**
   ```bash
   sudo mysql_secure_installation
   # Créer base de données pour Nextcloud
   ```

3. **Télécharger Nextcloud**
   ```bash
   cd /var/www/
   sudo wget https://download.nextcloud.com/server/releases/latest.tar.bz2
   sudo tar -xjf latest.tar.bz2
   ```

4. **Configurer Apache**
   - Créer VirtualHost
   - Activer modules nécessaires
   - Configurer SSL

5. **Finaliser via l'interface web**
   - Accéder à `http://votre-ip/nextcloud`
   - Suivre l'assistant d'installation

⚠️ **Attention :** Cette méthode nécessite de bonnes connaissances en administration Linux.

---

### Configuration réseau pour l'auto-hébergement

Pour accéder à votre Nextcloud depuis Internet :

1. **Nom de domaine** (recommandé)
   - Achetez un nom de domaine (ex: chez OVH, Gandi)
   - Configurez-le pour pointer vers votre IP publique

2. **IP dynamique**
   - Utilisez un service DynDNS (No-IP, DuckDNS)
   - Configure votre routeur pour mettre à jour l'IP automatiquement

3. **Ouverture de ports sur votre box**
   - Port 80 (HTTP) → Rediriger vers votre serveur
   - Port 443 (HTTPS) → Rediriger vers votre serveur

4. **Certificat SSL** (obligatoire pour HTTPS)
   - Utilisez **Let's Encrypt** (gratuit)
   - Automatisez le renouvellement avec **Certbot**

---

## Sécurité et bonnes pratiques

### 🔒 Sécurité essentielle

1. **Toujours utiliser HTTPS** (certificat SSL)
2. **Mots de passe forts** pour tous les comptes
3. **Authentification à deux facteurs** (2FA)
   - Activez dans les paramètres de sécurité Nextcloud
4. **Mises à jour régulières**
   - Nextcloud publie des mises à jour de sécurité
5. **Pare-feu configuré** correctement (UFW)
6. **Fail2Ban** pour bloquer les tentatives de connexion malveillantes

---

### 💾 Sauvegardes

**Ne comptez jamais uniquement sur Nextcloud !**

1. **Sauvegarde des données** : `/var/www/nextcloud/data`
2. **Sauvegarde de la base de données** : Export SQL régulier
3. **Sauvegarde de la configuration** : `/var/www/nextcloud/config`

**Automatisez** avec cron et rsync, ou utilisez des outils comme **Borg Backup**.

---

### ⚡ Optimisation des performances

1. **Utiliser Redis** ou **APCu** pour le cache
2. **Activer la compression** (gzip)
3. **Optimiser PHP** (php.ini : memory_limit, upload_max_filesize)
4. **Utiliser SSD** plutôt que HDD
5. **Activer HTTP/2** dans Apache/Nginx

---

## Applications mobiles et synchronisation

Nextcloud propose des applications pour tous vos appareils :

### 📱 **Android**
- **Nextcloud** : App officielle (Google Play / F-Droid)
- Synchronisation automatique des photos
- Accès à tous vos fichiers

### 🍎 **iOS / iPhone**
- **Nextcloud** : App officielle (App Store)
- Même fonctionnalités qu'Android

### 💻 **Desktop**
- **Linux** : Client natif (ce que nous avons installé)
- **Windows** : Client officiel disponible
- **macOS** : Client officiel disponible

### 🔄 Synchronisation multi-appareils

Tous vos appareils synchronisés avec le même compte Nextcloud :
- PC Linux (maison)
- Laptop Windows (travail)
- Smartphone Android
- Tablette iPad

**Résultat :** Vos fichiers sont identiques partout, automatiquement !

---

## Comparaison Nextcloud vs ownCloud

| Critère | Nextcloud | ownCloud |
|---------|-----------|----------|
| **Développement** | Très actif | Modéré |
| **Applications** | Nombreuses (>200) | Moins nombreuses |
| **Communauté** | Très large | Plus petite |
| **Facilité d'installation** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Performance** | Excellente | Excellente |
| **Interface** | Moderne | Similaire |
| **Support commercial** | Nextcloud GmbH | ownCloud GmbH |
| **Licence** | AGPLv3 (libre) | AGPLv3 (libre) |

**Recommandation :** Nextcloud pour la majorité des utilisateurs (plus d'applications, communauté plus active).

---

## Dépannage

### Problème : Synchronisation bloquée

**Solution :**
1. Redémarrez le client Nextcloud
2. Vérifiez votre connexion Internet
3. Consultez les logs : `~/.config/Nextcloud/nextcloud.log`

---

### Problème : Fichiers en conflit

Quand un fichier est modifié simultanément sur plusieurs appareils :
- Nextcloud crée une version **"conflit"**
- Vous devez **manuellement** choisir la bonne version

**Solution :** Évitez de modifier le même fichier depuis plusieurs endroits simultanément.

---

### Problème : Client ne se connecte pas

**Vérifications :**
1. ✅ URL correcte du serveur (https://)
2. ✅ Certificat SSL valide
3. ✅ Pare-feu autorise la connexion
4. ✅ Identifiants corrects

---

### Problème : Consommation élevée de CPU

**Causes possibles :**
- Synchronisation de nombreux fichiers
- Indexation des fichiers photos/vidéos

**Solution :** Attendez la fin de la synchronisation initiale, puis ça se stabilise.

---

## Alternatives à Nextcloud/ownCloud

Si Nextcloud ne correspond pas à vos besoins :

### **Seafile**
- Plus rapide pour les gros fichiers
- Interface plus simple
- Moins d'applications intégrées

### **Syncthing**
- Peer-to-peer (pas de serveur central)
- Totalement décentralisé
- Plus simple à configurer

### **Cozy Cloud**
- Solution française
- Focus sur la vie privée
- Interface très soignée

---

## Ressources utiles

### 📚 Documentation officielle
- Site officiel : https://nextcloud.com
- Documentation : https://docs.nextcloud.com
- Forum : https://help.nextcloud.com

### 🎓 Tutoriels
- Nextcloud sur Raspberry Pi : https://pimylifeup.com/raspberry-pi-nextcloud/
- Nextcloud avec Docker : https://github.com/nextcloud/docker

### 🛠️ Outils complémentaires
- Nextcloud News (lecteur RSS)
- Nextcloud Bookmarks (favoris synchronisés)
- Nextcloud Deck (gestion de projets type Trello)

---

## Conclusion

**Nextcloud** est la solution de cloud personnel la plus complète pour Linux Mint :

- ✅ Contrôle total de vos données
- ✅ Respect de la vie privée
- ✅ Fonctionnalités riches (bien plus qu'un simple stockage)
- ✅ Excellent support Linux

**Pour débuter :** Utilisez un hébergeur proposant Nextcloud pré-installé (Infomaniak, Hetzner).

**Pour les passionnés :** L'auto-hébergement offre une liberté totale mais demande du temps et des connaissances.

**Prochaine étape :** Chapitre 10.3 pour connecter Google Drive si vous avez besoin de compatibilité avec cet écosystème.

---

**Bon cloud computing avec Nextcloud ! ☁️**

⏭️ [Synchronisation Google Drive (Insync, rclone)](/10-cloud-et-synchronisation/03-synchronisation-google-drive.md)
