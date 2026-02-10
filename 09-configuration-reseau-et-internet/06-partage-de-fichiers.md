🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 9.6 Partage de fichiers (Samba, NFS)

## Introduction

Le partage de fichiers en réseau permet à plusieurs ordinateurs d'accéder aux mêmes fichiers et dossiers, comme si ces fichiers étaient stockés localement sur chaque machine. C'est extrêmement utile pour :

- Partager des documents entre membres d'une famille
- Accéder à vos fichiers depuis plusieurs ordinateurs
- Créer un serveur de médias accessible depuis tous vos appareils
- Collaborer sur des projets en équipe
- Centraliser vos sauvegardes

Dans ce chapitre, nous allons explorer les deux principales méthodes de partage de fichiers sous Linux : **Samba** (compatible avec Windows, Mac et Linux) et **NFS** (optimisé pour Linux).

## Comprendre les protocoles de partage

### Samba (SMB/CIFS)

**Qu'est-ce que Samba ?**

Samba est une implémentation libre du protocole SMB/CIFS utilisé par Windows pour le partage de fichiers. C'est la solution universelle de partage.

**Avantages** :
- Compatible avec Windows, Mac, Linux, Android, iOS
- Facile à configurer
- Supporte l'authentification par utilisateur
- Intégration native dans les explorateurs de fichiers
- Le plus utilisé dans les réseaux domestiques

**Inconvénients** :
- Un peu plus lent que NFS pour Linux-to-Linux
- Plus gourmand en ressources
- Configuration légèrement plus complexe que NFS

**Quand l'utiliser** :
- Réseau mixte (Windows + Linux + Mac)
- Réseau domestique
- Besoin d'accès depuis des appareils mobiles
- Remplacement de serveur de fichiers Windows

### NFS (Network File System)

**Qu'est-ce que NFS ?**

NFS est le protocole natif de partage de fichiers sous Unix/Linux. Il a été conçu spécifiquement pour ces systèmes.

**Avantages** :
- Très performant entre machines Linux
- Configuration simple
- Léger en ressources
- Permissions Unix natives préservées
- Excellent pour les serveurs Linux

**Inconvénients** :
- Principalement pour Linux/Unix (support limité sur Windows)
- Sécurité de base (nécessite configuration supplémentaire pour forte sécurité)
- Pas adapté pour les réseaux non sécurisés

**Quand l'utiliser** :
- Réseau 100% Linux
- Serveurs et clusters Linux
- Besoin de performances maximales
- Montage de partages au démarrage

### Comparaison rapide

| Critère | Samba | NFS |
|---------|-------|-----|
| Compatibilité | Windows, Mac, Linux, Mobile | Principalement Linux/Unix |
| Performance | Bonne | Excellente (Linux-to-Linux) |
| Sécurité | Bonne (avec config) | Moyenne (par défaut) |
| Configuration | Moyenne | Simple |
| Usage typique | Réseau domestique mixte | Serveurs Linux |

## Installation et configuration de Samba

### Installation de Samba

**Installer les paquets nécessaires** :

```bash
sudo apt update  
sudo apt install samba samba-common-bin smbclient cifs-utils  
```

**Explication des paquets** :
- `samba` : Le serveur Samba
- `samba-common-bin` : Outils de configuration
- `smbclient` : Client pour se connecter à des partages
- `cifs-utils` : Outils pour monter des partages

**Vérifier l'installation** :

```bash
# Vérifier la version
smbd --version

# Vérifier que le service fonctionne
sudo systemctl status smbd
```

### Configuration de base via l'interface graphique

Linux Mint propose une interface graphique pour partager facilement des dossiers.

#### Partager un dossier simple

1. **Ouvrez le gestionnaire de fichiers Nemo**

2. **Naviguez jusqu'au dossier à partager** (ex: un dossier "Partage" dans votre dossier personnel)

3. **Clic droit sur le dossier** → **Propriétés**

4. **Onglet "Partage"** :
   - Cochez **"Partager ce dossier"**
   - **Nom du partage** : Le nom qui apparaîtra sur le réseau (évitez les espaces et caractères spéciaux)
   - Cochez **"Autoriser d'autres personnes à modifier mes fichiers"** si vous voulez que d'autres puissent modifier
   - Cochez **"Accès invité"** si vous voulez permettre l'accès sans mot de passe (moins sécurisé)

5. **Cliquez sur "Créer le partage"**

6. **Message d'installation** : Si c'est votre premier partage, Linux Mint peut vous demander d'installer des services supplémentaires. Acceptez.

7. **Permissions** : Si demandé, acceptez d'ajouter les permissions nécessaires au dossier.

**Voilà !** Votre dossier est maintenant partagé sur le réseau local.

#### Vérifier le partage

```bash
# Voir tous les partages actifs
smbstatus --shares

# Ou lister via la commande
net usershare list
```

### Configuration manuelle de Samba

Pour plus de contrôle, vous pouvez configurer Samba manuellement.

#### Fichier de configuration principal

Le fichier de configuration principal est `/etc/samba/smb.conf`.

**Sauvegardez d'abord l'original** :
```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
```

**Éditez le fichier** :
```bash
sudo nano /etc/samba/smb.conf
```

#### Structure du fichier smb.conf

Le fichier est divisé en sections :

**Section [global]** : Configuration générale du serveur  
**Sections individuelles** : Chaque partage a sa propre section  

#### Exemple de configuration complète

```ini
# Section globale
[global]
   workgroup = WORKGROUP
   server string = Serveur Samba sur %h
   security = user
   map to guest = Bad User
   dns proxy = no

   # Logs
   log file = /var/log/samba/log.%m
   max log size = 1000

   # Performance
   socket options = TCP_NODELAY IPTOS_LOWDELAY SO_RCVBUF=65536 SO_SNDBUF=65536
   read raw = yes
   write raw = yes

   # Charset (important pour les accents)
   unix charset = UTF-8
   dos charset = CP850

# Partage public (accessible à tous sans mot de passe)
[Public]
   comment = Dossier public accessible à tous
   path = /home/partage/public
   browseable = yes
   writable = yes
   guest ok = yes
   read only = no
   create mask = 0755
   directory mask = 0755

# Partage privé (nécessite authentification)
[Documents]
   comment = Documents personnels
   path = /home/jean/Documents
   browseable = yes
   writable = yes
   valid users = jean, marie
   create mask = 0644
   directory mask = 0755

# Partage en lecture seule
[Archives]
   comment = Archives en lecture seule
   path = /home/partage/archives
   browseable = yes
   writable = no
   guest ok = yes
   read only = yes
```

#### Explications des paramètres importants

**Section [global]** :

- `workgroup` : Nom du groupe de travail (WORKGROUP par défaut pour Windows)
- `server string` : Description du serveur
- `security = user` : Authentification par utilisateur
- `map to guest = Bad User` : Utilisateur invalide = invité
- `unix charset` et `dos charset` : Pour gérer correctement les accents

**Section de partage** :

- `comment` : Description du partage
- `path` : Chemin absolu du dossier à partager
- `browseable` : Visible dans la liste des partages (yes/no)
- `writable` : Écriture autorisée (yes/no)
- `read only` : Lecture seule (yes/no)
- `guest ok` : Accès invité autorisé (yes/no)
- `valid users` : Utilisateurs autorisés (noms séparés par virgules)
- `create mask` : Permissions des nouveaux fichiers (0644 = rw-r--r--)
- `directory mask` : Permissions des nouveaux dossiers (0755 = rwxr-xr-x)

#### Vérifier la configuration

Avant de redémarrer Samba, vérifiez que la configuration est correcte :

```bash
testparm
```

Cette commande affiche votre configuration et signale les erreurs éventuelles.

#### Redémarrer Samba

Après toute modification du fichier de configuration :

```bash
sudo systemctl restart smbd  
sudo systemctl restart nmbd  
```

**nmbd** gère la résolution de noms NetBIOS (permet de voir le serveur par son nom).

### Gestion des utilisateurs Samba

Les utilisateurs Samba doivent être des utilisateurs Linux existants, mais avec un mot de passe Samba séparé.

#### Créer un utilisateur Linux (si nécessaire)

```bash
# Créer un utilisateur sans shell (sécurité)
sudo useradd -M -s /sbin/nologin partage

# Ou avec un répertoire personnel
sudo useradd -m partage
```

#### Ajouter un utilisateur Samba

```bash
# Ajouter l'utilisateur jean à Samba
sudo smbpasswd -a jean

# Vous serez invité à définir un mot de passe Samba
```

**Note** : Ce mot de passe peut être différent du mot de passe Linux de l'utilisateur.

#### Gérer les utilisateurs Samba

```bash
# Activer un utilisateur désactivé
sudo smbpasswd -e jean

# Désactiver un utilisateur
sudo smbpasswd -d jean

# Supprimer un utilisateur Samba
sudo smbpasswd -x jean

# Changer le mot de passe Samba
sudo smbpasswd jean

# Lister les utilisateurs Samba
sudo pdbedit -L -v
```

### Créer un partage pas à pas

**Exemple** : Créer un dossier "Médias" partagé accessible à certains utilisateurs.

#### Étape 1 : Créer le dossier

```bash
# Créer le dossier
sudo mkdir -p /home/partage/medias

# Définir les permissions
sudo chown -R nobody:nogroup /home/partage/medias  
sudo chmod -R 0775 /home/partage/medias  
```

#### Étape 2 : Ajouter à smb.conf

```bash
sudo nano /etc/samba/smb.conf
```

Ajoutez à la fin :

```ini
[Medias]
   comment = Bibliothèque multimédia familiale
   path = /home/partage/medias
   browseable = yes
   writable = yes
   valid users = jean, marie, paul
   create mask = 0664
   directory mask = 0775
   force user = nobody
   force group = nogroup
```

#### Étape 3 : Vérifier et redémarrer

```bash
# Vérifier la configuration
testparm

# Redémarrer Samba
sudo systemctl restart smbd
```

#### Étape 4 : Créer les utilisateurs (si nécessaire)

```bash
sudo smbpasswd -a jean  
sudo smbpasswd -a marie  
sudo smbpasswd -a paul  
```

### Accéder aux partages Samba

#### Depuis Linux Mint

**Méthode 1 : Via le gestionnaire de fichiers**

1. Ouvrez **Nemo** (gestionnaire de fichiers)
2. Dans la barre latérale, cliquez sur **"Réseau"**
3. Vous verrez les ordinateurs du réseau avec Samba
4. Double-cliquez sur un ordinateur
5. Cliquez sur le partage souhaité
6. Entrez les identifiants si demandé

**Méthode 2 : Via l'adresse directe**

1. Dans Nemo, appuyez sur **Ctrl+L** pour afficher la barre d'adresse
2. Tapez : `smb://nom-ordinateur/nom-partage`
   - Exemple : `smb://serveur-maison/Medias`
3. Ou avec l'IP : `smb://192.168.1.100/Medias`
4. Entrez les identifiants si demandé

**Méthode 3 : Monter manuellement**

```bash
# Créer un point de montage
mkdir -p ~/Reseau/Medias

# Monter le partage
sudo mount -t cifs //192.168.1.100/Medias ~/Reseau/Medias -o username=jean,password=motdepasse

# Ou sans mot de passe en clair (plus sécurisé)
sudo mount -t cifs //192.168.1.100/Medias ~/Reseau/Medias -o username=jean
# Le mot de passe sera demandé
```

**Montage permanent dans /etc/fstab** :

```bash
sudo nano /etc/fstab
```

Ajoutez :
```
//192.168.1.100/Medias /home/jean/Reseau/Medias cifs credentials=/home/jean/.smbcredentials,uid=1000,gid=1000 0 0
```

Créez le fichier de credentials :
```bash
nano ~/.smbcredentials
```

Contenu :
```
username=jean  
password=votre_mot_de_passe  
```

Sécurisez-le :
```bash
chmod 600 ~/.smbcredentials
```

#### Depuis Windows

1. Ouvrez **l'Explorateur de fichiers**
2. Dans la barre d'adresse, tapez : `\\adresse-ip\nom-partage`
   - Exemple : `\\192.168.1.100\Medias`
3. Entrez les identifiants si demandé
4. Cochez "Mémoriser mes informations d'identification" pour ne pas retaper

**Mapper un lecteur réseau** :
1. Clic droit sur **Ce PC** → **Connecter un lecteur réseau**
2. Choisissez une lettre (ex: Z:)
3. Dossier : `\\192.168.1.100\Medias`
4. Cochez "Se reconnecter à l'ouverture de session"
5. Cochez "Se connecter à l'aide d'informations d'identification différentes" si nécessaire

#### Depuis macOS

1. Dans le **Finder**, menu **Aller** → **Se connecter au serveur**
2. Adresse : `smb://192.168.1.100/Medias`
3. Cliquez sur **Se connecter**
4. Entrez les identifiants

#### Depuis Android/iOS

Utilisez des applications comme :
- **ES File Explorer** (Android)
- **File Explorer** (iOS)
- **VLC** (pour médias)

Configuration : SMB, adresse IP, identifiants.

## Installation et configuration de NFS

NFS est plus simple à configurer mais principalement utilisé entre machines Linux.

### Installation du serveur NFS

**Sur le serveur (machine qui partage)** :

```bash
sudo apt update  
sudo apt install nfs-kernel-server  
```

**Vérifier l'installation** :

```bash
# Vérifier que le service fonctionne
sudo systemctl status nfs-kernel-server

# Voir la version
nfsstat -v
```

### Installation du client NFS

**Sur le client (machine qui accède aux partages)** :

```bash
sudo apt update  
sudo apt install nfs-common  
```

### Configuration de NFS

#### Fichier de configuration /etc/exports

Le fichier `/etc/exports` définit quels dossiers sont partagés et avec qui.

**Éditer le fichier** :

```bash
sudo nano /etc/exports
```

**Syntaxe générale** :
```
/chemin/à/partager    adresse_client(options)
```

#### Exemples de configuration

**Partage simple pour un client spécifique** :
```
/home/partage/public    192.168.1.100(rw,sync,no_subtree_check)
```

**Partage pour tout un sous-réseau** :
```
/home/partage/public    192.168.1.0/24(rw,sync,no_subtree_check)
```

**Partage en lecture seule** :
```
/home/partage/archives    192.168.1.0/24(ro,sync,no_subtree_check)
```

**Plusieurs clients avec permissions différentes** :
```
/home/partage/data    192.168.1.100(rw,sync) 192.168.1.101(ro,sync)
```

**Partage accessible par tous (dangereux !)** :
```
/home/partage/public    *(rw,sync,no_subtree_check,insecure)
```

#### Options importantes

**Permissions** :
- `rw` : Lecture et écriture
- `ro` : Lecture seule

**Synchronisation** :
- `sync` : Synchronisation immédiate (recommandé)
- `async` : Asynchrone (plus rapide mais risque de perte de données)

**Sécurité** :
- `no_subtree_check` : Désactive la vérification des sous-arbres (améliore performance)
- `subtree_check` : Active la vérification (plus sécurisé mais plus lent)
- `no_root_squash` : Root distant = root local (DANGEREUX)
- `root_squash` : Root distant = nobody local (par défaut, sécurisé)
- `all_squash` : Tous les utilisateurs distants = nobody local

**Mappage d'utilisateurs** :
- `anonuid=1000` : UID pour utilisateurs anonymes
- `anongid=1000` : GID pour utilisateurs anonymes

**Autres** :
- `insecure` : Autoriser les ports > 1024 (nécessaire pour certains clients)
- `no_wdelay` : Désactive le délai d'écriture

#### Configuration complète exemple

```bash
# /etc/exports

# Partage documents - accès complet pour le réseau local
/home/partage/documents    192.168.1.0/24(rw,sync,no_subtree_check)

# Partage médias - lecture seule pour tous
/home/partage/medias       192.168.1.0/24(ro,sync,no_subtree_check)

# Partage backup - accès restreint à un serveur spécifique
/home/backup               192.168.1.50(rw,sync,no_root_squash,no_subtree_check)

# Partage web - accessible depuis plusieurs serveurs
/var/www/html              192.168.1.10(rw,sync) 192.168.1.11(rw,sync) 192.168.1.12(rw,sync)
```

### Créer un partage NFS pas à pas

**Exemple** : Partager un dossier "Données" avec le réseau local.

#### Étape 1 : Créer le dossier

```bash
# Créer le dossier
sudo mkdir -p /srv/nfs/donnees

# Définir les permissions
sudo chown -R nobody:nogroup /srv/nfs/donnees  
sudo chmod -R 755 /srv/nfs/donnees  
```

#### Étape 2 : Ajouter à /etc/exports

```bash
sudo nano /etc/exports
```

Ajoutez :
```
/srv/nfs/donnees    192.168.1.0/24(rw,sync,no_subtree_check)
```

#### Étape 3 : Appliquer la configuration

```bash
# Recharger la configuration
sudo exportfs -ra

# Vérifier les partages actifs
sudo exportfs -v
```

#### Étape 4 : Redémarrer le service

```bash
sudo systemctl restart nfs-kernel-server
```

### Accéder aux partages NFS (côté client)

#### Monter manuellement

```bash
# Créer un point de montage
sudo mkdir -p /mnt/nfs/donnees

# Monter le partage
sudo mount -t nfs 192.168.1.100:/srv/nfs/donnees /mnt/nfs/donnees

# Vérifier le montage
df -h | grep nfs  
mount | grep nfs  
```

#### Monter automatiquement au démarrage

**Éditer /etc/fstab** :

```bash
sudo nano /etc/fstab
```

Ajoutez :
```
192.168.1.100:/srv/nfs/donnees    /mnt/nfs/donnees    nfs    defaults,_netdev    0    0
```

**Options utiles pour /etc/fstab** :
- `defaults` : Options par défaut
- `_netdev` : Attend que le réseau soit disponible avant de monter
- `soft` : Timeout si serveur indisponible (évite le gel)
- `hard` : Continue d'essayer indéfiniment (par défaut)
- `timeo=30` : Timeout de 30 dixièmes de seconde (3 secondes)
- `retrans=2` : Nombre de retransmissions

**Exemple avec options avancées** :
```
192.168.1.100:/srv/nfs/donnees    /mnt/nfs/donnees    nfs    soft,timeo=30,retrans=2,_netdev    0    0
```

#### Tester le montage depuis fstab

```bash
# Monter tous les systèmes de fichiers de fstab
sudo mount -a

# Vérifier
df -h /mnt/nfs/donnees
```

#### Démonter un partage NFS

```bash
# Démonter
sudo umount /mnt/nfs/donnees

# Force (si occupé)
sudo umount -f /mnt/nfs/donnees

# Force et lazy (détache immédiatement mais nettoie en arrière-plan)
sudo umount -l /mnt/nfs/donnees
```

### Gérer les exports NFS

```bash
# Voir tous les partages exportés
sudo exportfs -v

# Recharger /etc/exports sans redémarrer
sudo exportfs -ra

# Exporter un dossier immédiatement (temporaire)
sudo exportfs -o rw,sync 192.168.1.100:/srv/nfs/test

# Retirer un export
sudo exportfs -u 192.168.1.100:/srv/nfs/test

# Retirer tous les exports
sudo exportfs -ua
```

## Sécurité du partage de fichiers

### Sécurité Samba

#### Configuration pare-feu

```bash
# Autoriser Samba dans le pare-feu
sudo ufw allow Samba

# Ou manuellement
sudo ufw allow 137,138/udp  
sudo ufw allow 139,445/tcp  

# Limiter à votre réseau local
sudo ufw allow from 192.168.1.0/24 to any app Samba
```

#### Désactiver l'accès invité

Dans `/etc/samba/smb.conf`, section [global] :

```ini
map to guest = Never
```

Cela force l'authentification pour tous les partages.

#### Limiter l'accès par IP

Dans une section de partage :

```ini
[Documents]
   path = /home/partage/docs
   valid users = jean
   hosts allow = 192.168.1. 127.
   hosts deny = ALL
```

#### Utiliser le chiffrement

Pour Samba 4.x, activez le chiffrement SMB3 :

```ini
[global]
   server min protocol = SMB3
   smb encrypt = required
```

#### Auditer les connexions

```bash
# Voir qui est connecté actuellement
smbstatus

# Voir les connexions détaillées
smbstatus -v

# Voir les fichiers ouverts
smbstatus -L

# Logs Samba
sudo tail -f /var/log/samba/log.smbd
```

### Sécurité NFS

#### Configuration pare-feu

```bash
# Autoriser NFS dans le pare-feu
sudo ufw allow from 192.168.1.0/24 to any port 2049

# Ou
sudo ufw allow nfs
```

#### Limiter par IP dans /etc/exports

```bash
# Accepter seulement des IP spécifiques
/srv/nfs/data    192.168.1.100(rw,sync) 192.168.1.101(rw,sync)

# Ou un sous-réseau
/srv/nfs/data    192.168.1.0/24(rw,sync)
```

#### Utiliser root_squash

Toujours utiliser `root_squash` (activé par défaut) :

```
/srv/nfs/data    192.168.1.0/24(rw,sync,root_squash)
```

N'utilisez `no_root_squash` que si absolument nécessaire et comprenez les risques.

#### NFSv4 avec Kerberos (avancé)

Pour une sécurité maximale, utilisez NFSv4 avec authentification Kerberos. Cela dépasse le cadre de ce tutoriel débutant, mais c'est la configuration recommandée pour les environnements professionnels.

#### Surveiller l'activité NFS

```bash
# Voir les statistiques NFS
nfsstat

# Voir les connexions actives
sudo netstat -an | grep :2049

# Logs système
sudo tail -f /var/log/syslog | grep nfs
```

### Bonnes pratiques générales

#### Principe du moindre privilège

- N'accordez que les permissions nécessaires (ro au lieu de rw si possible)
- Limitez les utilisateurs autorisés
- Restreignez par IP ou sous-réseau

#### Mots de passe forts

```bash
# Générer un mot de passe fort pour Samba
openssl rand -base64 16
```

Utilisez des mots de passe différents pour chaque utilisateur.

#### Séparation des données

- Créez des partages séparés pour différents types de données
- Documents sensibles : partage privé
- Médias : partage lecture seule
- Dossier public : partage avec accès limité

#### Surveillance et logs

Activez les logs détaillés dans Samba :

```ini
[global]
   log level = 2
   max log size = 5000
```

Consultez régulièrement :
```bash
sudo tail -f /var/log/samba/log.smbd
```

#### Sauvegardes

Les partages réseau ne remplacent pas les sauvegardes ! Sauvegardez régulièrement vos données partagées.

## Résolution des problèmes courants

### Problèmes Samba

#### Impossible de voir le serveur dans le réseau

**Solutions** :

1. **Vérifier que Samba fonctionne** :
```bash
sudo systemctl status smbd  
sudo systemctl status nmbd  
sudo systemctl restart smbd  
sudo systemctl restart nmbd  
```

2. **Vérifier le pare-feu** :
```bash
sudo ufw status  
sudo ufw allow Samba  
```

3. **Vérifier le nom du groupe de travail** :
```bash
# Dans /etc/samba/smb.conf
workgroup = WORKGROUP  # Doit correspondre à celui de Windows
```

4. **Installer Avahi** (découverte réseau) :
```bash
sudo apt install avahi-daemon  
sudo systemctl restart avahi-daemon  
```

#### Erreur "Permission denied" lors de l'accès

**Solutions** :

1. **Vérifier les permissions du dossier** :
```bash
ls -ld /chemin/vers/partage  
sudo chmod 755 /chemin/vers/partage  
```

2. **Vérifier l'utilisateur Samba** :
```bash
sudo pdbedit -L
# Si l'utilisateur n'existe pas :
sudo smbpasswd -a utilisateur
```

3. **Vérifier le fichier smb.conf** :
```bash
testparm
# Vérifier valid users, writable, etc.
```

4. **Vérifier les permissions SELinux** (si applicable) :
```bash
sudo getsebool -a | grep samba  
sudo setsebool -P samba_enable_home_dirs on  
```

#### Lenteur du partage Samba

**Solutions** :

1. **Optimiser smb.conf** :
```ini
[global]
   socket options = TCP_NODELAY IPTOS_LOWDELAY SO_RCVBUF=131072 SO_SNDBUF=131072
   read raw = yes
   write raw = yes
   min receivefile size = 16384
   use sendfile = true
   aio read size = 16384
   aio write size = 16384
```

2. **Désactiver les oplocks** (si problèmes de corruption) :
```ini
oplocks = no  
level2 oplocks = no  
```

3. **Vérifier la connexion réseau** :
```bash
ping adresse_serveur  
iperf3 -s  # Sur le serveur  
iperf3 -c adresse_serveur  # Sur le client  
```

#### Impossible de se connecter avec mot de passe

**Solutions** :

1. **Réinitialiser le mot de passe Samba** :
```bash
sudo smbpasswd -d utilisateur  # Désactiver  
sudo smbpasswd -a utilisateur  # Réactiver avec nouveau mot de passe  
sudo smbpasswd -e utilisateur  # Activer  
```

2. **Vérifier que l'authentification utilisateur est activée** :
```ini
[global]
   security = user
```

3. **Vérifier le mappage des utilisateurs** :
```bash
# Créer un fichier de mappage si nécessaire
sudo nano /etc/samba/smbusers
```

Contenu :
```
jean = "Jean Dupont" jean_dupont
```

Dans smb.conf :
```ini
[global]
   username map = /etc/samba/smbusers
```

### Problèmes NFS

#### Impossible de monter le partage

**Solutions** :

1. **Vérifier que NFS fonctionne** :
```bash
sudo systemctl status nfs-kernel-server  
sudo systemctl restart nfs-kernel-server  
```

2. **Vérifier les exports** :
```bash
sudo exportfs -v
# Si vide ou incorrect :
sudo exportfs -ra
```

3. **Vérifier le pare-feu** :
```bash
sudo ufw allow from 192.168.1.0/24 to any port 2049
```

4. **Tester avec showmount** :
```bash
# Sur le client
showmount -e 192.168.1.100
# Devrait lister les partages disponibles
```

5. **Vérifier les logs** :
```bash
sudo tail -f /var/log/syslog | grep nfs  
dmesg | grep nfs  
```

#### Erreur "Permission denied" sur NFS

**Solutions** :

1. **Vérifier les permissions du dossier** :
```bash
ls -ld /srv/nfs/partage  
sudo chmod 755 /srv/nfs/partage  
```

2. **Vérifier le mappage des utilisateurs** :
```bash
# Sur le serveur, vérifier les options d'export
sudo exportfs -v
# Assurez-vous que root_squash n'empêche pas l'accès
```

3. **Vérifier les UID/GID** :
Les UID/GID doivent correspondre entre client et serveur pour un accès correct.

```bash
# Sur le serveur
id utilisateur

# Sur le client
id utilisateur
# Doivent être identiques
```

4. **Utiliser all_squash si nécessaire** :
```
/srv/nfs/partage    192.168.1.0/24(rw,sync,all_squash,anonuid=1000,anongid=1000)
```

#### Le montage NFS fige le système

**Solutions** :

1. **Utiliser l'option soft** :
```bash
sudo mount -t nfs -o soft,timeo=30 192.168.1.100:/srv/nfs/data /mnt/data
```

2. **Démonter en force** :
```bash
sudo umount -f /mnt/data
# Ou lazy unmount
sudo umount -l /mnt/data
```

3. **Modifier /etc/fstab** pour éviter le problème :
```
192.168.1.100:/srv/nfs/data /mnt/data nfs soft,timeo=30,retrans=2,_netdev 0 0
```

#### Problèmes de performance NFS

**Solutions** :

1. **Augmenter rsize et wsize** :
```bash
sudo mount -t nfs -o rsize=32768,wsize=32768 192.168.1.100:/srv/nfs/data /mnt/data
```

2. **Utiliser async** (attention aux risques) :
```
/srv/nfs/data    192.168.1.0/24(rw,async,no_subtree_check)
```

3. **Augmenter le nombre de threads NFS** :
```bash
sudo nano /etc/default/nfs-kernel-server
```

Modifiez :
```
RPCNFSDCOUNT=16  # Par défaut 8, augmentez selon vos besoins
```

Redémarrez :
```bash
sudo systemctl restart nfs-kernel-server
```

## Cas d'usage pratiques

### Serveur multimédia domestique

**Objectif** : Partager films, musiques, photos avec toute la famille.

**Configuration Samba** :

```ini
[Medias]
   comment = Bibliothèque multimédia familiale
   path = /home/partage/medias
   browseable = yes
   writable = yes
   valid users = @famille
   create mask = 0664
   directory mask = 0775
   force group = famille
```

**Structure des dossiers** :
```
/home/partage/medias/
├── Films/
├── Series/
├── Musique/
└── Photos/
```

**Créer le groupe et ajouter les utilisateurs** :
```bash
sudo groupadd famille  
sudo usermod -aG famille jean  
sudo usermod -aG famille marie  
sudo usermod -aG famille paul  
sudo chown -R :famille /home/partage/medias  
sudo chmod -R 775 /home/partage/medias  
```

**Accès depuis** :
- PC Windows/Linux/Mac : Montage réseau
- TV/Box Android : Application Kodi, VLC
- Smartphone : Applications comme VLC, Plex

### Serveur de fichiers professionnel

**Objectif** : Partager documents de travail avec permissions granulaires.

**Configuration Samba** :

```ini
[Direction]
   comment = Documents direction
   path = /srv/entreprise/direction
   valid users = @direction
   writable = yes
   create mask = 0660
   directory mask = 0770

[Comptabilite]
   comment = Documents comptabilité
   path = /srv/entreprise/comptabilite
   valid users = @compta
   read list = @direction
   write list = @compta
   create mask = 0660
   directory mask = 0770

[Public]
   comment = Documents publics
   path = /srv/entreprise/public
   browseable = yes
   writable = yes
   valid users = @employes
   create mask = 0664
   directory mask = 0775
```

**Gestion des groupes** :
```bash
sudo groupadd direction  
sudo groupadd compta  
sudo groupadd employes  

sudo usermod -aG direction pdg  
sudo usermod -aG compta, employes comptable1  
sudo usermod -aG employes employe1  
```

### Cluster de calcul Linux (NFS)

**Objectif** : Partager données de calcul entre nœuds Linux.

**Sur le serveur de stockage** :

```bash
# /etc/exports
/srv/cluster/data       192.168.10.0/24(rw,sync,no_root_squash,no_subtree_check)
/srv/cluster/home       192.168.10.0/24(rw,sync,root_squash,no_subtree_check)
/srv/cluster/software   192.168.10.0/24(ro,sync,no_subtree_check)
```

**Sur chaque nœud de calcul** :

```bash
# /etc/fstab
192.168.10.1:/srv/cluster/data      /data       nfs    hard,intr,rsize=32768,wsize=32768,_netdev    0 0
192.168.10.1:/srv/cluster/home      /home       nfs    hard,intr,_netdev    0 0
192.168.10.1:/srv/cluster/software  /opt/soft   nfs    ro,hard,intr,_netdev    0 0
```

### Sauvegarde réseau automatique

**Objectif** : Sauvegarder automatiquement plusieurs machines sur un serveur central.

**Sur le serveur de sauvegarde (NFS)** :

```bash
# Créer les dossiers
sudo mkdir -p /srv/backups/{pc1,pc2,pc3}

# /etc/exports
/srv/backups/pc1    192.168.1.10(rw,sync,no_subtree_check)
/srv/backups/pc2    192.168.1.11(rw,sync,no_subtree_check)
/srv/backups/pc3    192.168.1.12(rw,sync,no_subtree_check)
```

**Sur chaque client (script cron)** :

```bash
#!/bin/bash
# backup-to-nfs.sh

# Monter si nécessaire
if ! mountpoint -q /mnt/backup; then
    sudo mount -t nfs 192.168.1.100:/srv/backups/pc1 /mnt/backup
fi

# Sauvegarder avec rsync
rsync -avz --delete /home/jean/Documents/ /mnt/backup/documents/  
rsync -avz --delete /home/jean/Images/ /mnt/backup/images/  

echo "Sauvegarde terminée $(date)" >> /var/log/backup.log
```

**Automatiser avec cron** :
```bash
crontab -e
```

Ajoutez :
```
0 2 * * * /home/jean/scripts/backup-to-nfs.sh
```

## Outils graphiques de gestion

### System-config-samba

Interface graphique pour configurer Samba.

**Installation** :
```bash
sudo apt install system-config-samba
```

**Utilisation** :
```bash
sudo system-config-samba
```

Interface simple pour créer et gérer des partages Samba.

### Webmin

Interface web complète pour l'administration système, incluant Samba et NFS.

**Installation** :
```bash
curl -o setup-repos.sh https://raw.githubusercontent.com/webmin/webmin/master/setup-repos.sh  
sudo sh setup-repos.sh  
sudo apt install webmin  
```

**Accès** :
Ouvrez votre navigateur sur `https://votre-ip:10000`

### NFS-Ganesha

Alternative moderne à NFS traditionnel avec interface de gestion plus avancée.

Configuration avancée, consultez la documentation officielle.

## Surveillance et maintenance

### Surveiller Samba

**Voir les connexions actives** :
```bash
# Résumé
smbstatus

# Détaillé
smbstatus -v

# Fichiers ouverts
smbstatus -L

# Par utilisateur
smbstatus -u jean
```

**Logs Samba** :
```bash
# Logs généraux
sudo tail -f /var/log/samba/log.smbd

# Logs par machine
ls /var/log/samba/

# Rechercher des erreurs
sudo grep -i error /var/log/samba/log.smbd
```

### Surveiller NFS

**Statistiques NFS** :
```bash
# Statistiques générales
nfsstat

# Statistiques serveur
nfsstat -s

# Statistiques client
nfsstat -c

# Montrer les opérations les plus fréquentes
nfsstat -o all
```

**Connexions actives** :
```bash
# Voir les montages distants actifs
sudo netstat -an | grep :2049

# Ou avec ss (plus moderne)
sudo ss -tn | grep :2049
```

### Nettoyer les connexions orphelines

**Samba** :
```bash
# Tuer toutes les connexions d'un utilisateur
sudo smbcontrol smbd close-share nom_partage

# Forcer déconnexion
sudo smbcontrol all close-share nom_partage
```

**NFS** :
```bash
# Forcer le démontage côté client
sudo umount -f /mnt/nfs/partage

# Relancer les exports côté serveur
sudo exportfs -ra
```

### Sauvegardes de configuration

**Sauvegarder Samba** :
```bash
# Sauvegarder smb.conf
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup-$(date +%Y%m%d)

# Sauvegarder base utilisateurs
sudo pdbedit -e tdbsam:/root/samba-users-backup.tdb
```

**Sauvegarder NFS** :
```bash
# Sauvegarder exports
sudo cp /etc/exports /etc/exports.backup-$(date +%Y%m%d)
```

## Résumé des commandes essentielles

### Samba

```bash
# Installation
sudo apt install samba smbclient cifs-utils

# Gestion du service
sudo systemctl start smbd  
sudo systemctl stop smbd  
sudo systemctl restart smbd  
sudo systemctl status smbd  

# Configuration
sudo nano /etc/samba/smb.conf  
testparm                                      # Vérifier config  
sudo systemctl restart smbd                   # Appliquer  

# Gestion utilisateurs
sudo smbpasswd -a utilisateur                 # Ajouter  
sudo smbpasswd -e utilisateur                 # Activer  
sudo smbpasswd -d utilisateur                 # Désactiver  
sudo smbpasswd -x utilisateur                 # Supprimer  
sudo pdbedit -L                               # Lister  

# Surveillance
smbstatus                                     # Connexions actives  
smbstatus -L                                  # Fichiers ouverts  
net usershare list                            # Partages utilisateurs  

# Montage côté client
sudo mount -t cifs //serveur/partage /mnt/partage -o username=user
```

### NFS

```bash
# Installation serveur
sudo apt install nfs-kernel-server

# Installation client
sudo apt install nfs-common

# Configuration
sudo nano /etc/exports                        # Éditer  
sudo exportfs -ra                             # Recharger  
sudo exportfs -v                              # Voir exports  
sudo exportfs -u client:/partage              # Retirer export  

# Gestion du service
sudo systemctl start nfs-kernel-server  
sudo systemctl stop nfs-kernel-server  
sudo systemctl restart nfs-kernel-server  
sudo systemctl status nfs-kernel-server  

# Montage côté client
sudo mount -t nfs serveur:/partage /mnt/partage  
showmount -e serveur                          # Lister partages disponibles  

# Surveillance
nfsstat                                       # Statistiques  
nfsstat -s                                    # Stats serveur  
nfsstat -c                                    # Stats client  
```

---

**Points clés à retenir** :
- Samba est universel (Windows, Mac, Linux) mais un peu plus complexe
- NFS est optimal pour Linux-to-Linux mais limité aux systèmes Unix
- Toujours sécuriser vos partages (pare-feu, permissions, authentification)
- Utilisez des mots de passe forts et distincts pour Samba
- Limitez l'accès par IP quand c'est possible
- root_squash est votre ami en NFS (ne le désactivez qu'en connaissance de cause)
- Testez toujours votre configuration avant de l'appliquer en production
- Sauvegardez régulièrement vos fichiers de configuration
- Les partages réseau ne remplacent pas les sauvegardes !
- Surveillez les logs pour détecter des tentatives d'accès non autorisées

⏭️ [Bureau à distance (VNC, RDP)](/09-configuration-reseau-et-internet/07-bureau-a-distance.md)
