🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.7 /etc/fstab pour montage automatique

## Introduction

### Qu'est-ce que /etc/fstab ?

**fstab** = **F**ile **S**ystem **TAB**le (Table des systèmes de fichiers)

C'est un **fichier de configuration** qui indique à Linux :
- Quelles partitions monter au démarrage
- Où les monter (point de montage)
- Comment les monter (options)

**Analogie** :
Imaginez fstab comme une **liste de tâches** pour le démarrage :
- "Monte cette partition ici"
- "Monte celle-ci là avec ces options"
- "Monte ce partage réseau à cet endroit"

Linux lit cette liste au démarrage et exécute les montages automatiquement.

### Pourquoi utiliser fstab ?

**Sans fstab** :
```bash
# À chaque démarrage, vous devriez taper :
sudo mount /dev/sdb1 /mnt/donnees
sudo mount /dev/sdc1 /mnt/musique
sudo mount //192.168.1.10/partage /mnt/reseau
# Fastidieux !
```

**Avec fstab** :
```bash
# Une seule fois : ajouter les lignes dans fstab
# Ensuite : tout se monte automatiquement à chaque démarrage
# Pratique !
```

### Emplacement et permissions

**Chemin** : `/etc/fstab`

**Permissions** :
- Lecture : Tout le monde
- Écriture : Seulement root
- **Vous devez utiliser sudo** pour le modifier

### ⚠️ Avertissement important

**ATTENTION** : Une erreur dans `/etc/fstab` peut **empêcher votre système de démarrer** !

**Règles de sécurité** :
1. ✅ **Toujours faire une sauvegarde** avant de modifier
2. ✅ **Tester avec `mount -a`** avant de redémarrer
3. ✅ **Utiliser l'option `nofail`** pour les disques externes
4. ✅ **Vérifier deux fois** la syntaxe
5. ✅ **Avoir un Live USB** sous la main en cas de problème

---

## Voir le contenu actuel de fstab

### Afficher fstab

```bash
cat /etc/fstab
```

**Exemple de contenu typique** :
```
# /etc/fstab: static file system information.
#
# <file system>  <mount point>  <type>  <options>  <dump>  <pass>

# Partition système
UUID=abc123-def456-ghi789  /               ext4    errors=remount-ro  0  1

# Partition home
UUID=jkl012-mno345-pqr678  /home           ext4    defaults           0  2

# Partition EFI
UUID=A4B2-C3D4             /boot/efi       vfat    umask=0077         0  1

# Swap
UUID=stu901-vwx234-yza567  none            swap    sw                 0  0
```

**Comprendre les lignes** :
- Lignes commençant par **#** = commentaires (ignorés)
- Lignes vides = ignorées
- Autres lignes = instructions de montage

---

## Structure d'une ligne fstab

### Les 6 colonnes

Chaque ligne de montage contient **6 champs** séparés par des espaces ou tabulations :

```
<système_fichiers>  <point_montage>  <type>  <options>  <dump>  <pass>
```

### Visualisation avec colonnes alignées

```
# Système fichiers    Point montage  Type   Options         Dump  Pass
UUID=abc123-def456    /              ext4   defaults        0     1
UUID=jkl012-mno345    /home          ext4   defaults        0     2
/dev/sdb1             /mnt/donnees   ext4   defaults        0     2
```

Examinons chaque colonne en détail.

---

## Colonne 1 : Système de fichiers

**Qu'est-ce que c'est ?**
Identifie **quel** périphérique ou partition monter.

### Trois façons de spécifier

#### 1. Par UUID (RECOMMANDÉ ⭐)

```
UUID=abc123-def456-ghi789
```

**Avantages** :
- ✅ **Unique et stable** : Ne change jamais
- ✅ **Sûr** : Fonctionne même si l'ordre des disques change
- ✅ **Recommandé par défaut**

**Trouver l'UUID** :
```bash
sudo blkid
```

**Résultat** :
```
/dev/sda1: UUID="A4B2-C3D4" TYPE="vfat"
/dev/sda2: UUID="abc123-def456-ghi789" TYPE="ext4"
/dev/sdb1: UUID="jkl012-mno345-pqr678" TYPE="ext4"
```

#### 2. Par périphérique (DÉCONSEILLÉ ⚠️)

```
/dev/sdb1
```

**Inconvénient** :
- ❌ **Peut changer** : `/dev/sdb1` peut devenir `/dev/sdc1` si vous ajoutez un disque
- ❌ **Risque de monter le mauvais disque**

**Quand l'utiliser** :
- Seulement pour des tests temporaires
- Jamais pour des configurations permanentes

#### 3. Par étiquette (LABEL)

```
LABEL=MesDocuments
```

**Quand l'utiliser** :
- Si vous avez donné des noms explicites à vos partitions
- Alternative valable à UUID (plus lisible)

**Trouver les labels** :
```bash
sudo blkid | grep LABEL
```

### Cas spéciaux

**Swap** :
```
UUID=stu901-vwx234-yza567
```

**Partage réseau (Samba/CIFS)** :
```
//192.168.1.10/Partage
```

**Partage NFS** :
```
192.168.1.10:/export/partage
```

**Bind mount** (monter un dossier ailleurs) :
```
/home/pierre/Documents
```

---

## Colonne 2 : Point de montage

**Qu'est-ce que c'est ?**
**Où** la partition sera accessible dans l'arborescence.

### Points de montage standards

```
/                    # Racine du système
/home                # Dossiers utilisateurs
/boot                # Fichiers de démarrage
/boot/efi            # Partition EFI (UEFI)
/tmp                 # Fichiers temporaires
/var                 # Données variables
```

### Points de montage personnalisés

**Conventions** :
- `/mnt/` pour montages temporaires ou manuels
- `/media/` pour périphériques amovibles (géré par le système)
- Évitez `/home/user/` (peut créer des problèmes de permissions)

**Exemples** :
```
/mnt/donnees
/mnt/musique
/mnt/sauvegardes
/mnt/partage-reseau
```

### Cas spécial : swap

Pour le swap, utilisez :
```
none
```

Le swap n'a pas de point de montage visible (c'est de la mémoire virtuelle).

---

## Colonne 3 : Type de système de fichiers

**Qu'est-ce que c'est ?**
Le **type** de système de fichiers de la partition.

### Types courants

| Type | Usage |
|------|-------|
| **ext4** | Partitions Linux (système, données) |
| **ext3** | Ancien système Linux |
| **btrfs** | Système de fichiers moderne Linux |
| **xfs** | Hautes performances Linux |
| **vfat** | FAT32 (clés USB, partition EFI) |
| **ntfs** | Partitions Windows |
| **exfat** | Clés USB modernes |
| **swap** | Mémoire d'échange |
| **cifs** | Partage réseau Windows/Samba |
| **nfs** | Partage réseau Linux |
| **iso9660** | CD/DVD |
| **auto** | Détection automatique |

**Recommandation** : Spécifiez le type exact plutôt que d'utiliser `auto`.

---

## Colonne 4 : Options de montage

**Qu'est-ce que c'est ?**
**Comment** monter la partition (permissions, comportement).

### Option par défaut

```
defaults
```

**Équivaut à** : `rw,suid,dev,exec,auto,nouser,async`

C'est le choix standard pour la plupart des partitions Linux.

### Options courantes

#### Options de lecture/écriture

| Option | Signification |
|--------|---------------|
| **rw** | Lecture-écriture (read-write) |
| **ro** | Lecture seule (read-only) |
| **noexec** | Empêche l'exécution de programmes |
| **nosuid** | Ignore les bits SUID/SGID (sécurité) |
| **nodev** | Ignore les fichiers de périphériques |

#### Options de montage

| Option | Signification |
|--------|---------------|
| **auto** | Monte automatiquement au boot |
| **noauto** | Ne monte pas automatiquement (manuel) |
| **nofail** | Continue le boot même si le montage échoue ⭐ |
| **user** | Permet aux utilisateurs normaux de monter |
| **nouser** | Seul root peut monter |

#### Options de performance

| Option | Signification |
|--------|---------------|
| **async** | Écriture asynchrone (plus rapide) |
| **sync** | Écriture synchrone (plus sûr, plus lent) |
| **noatime** | Ne met pas à jour le temps d'accès (SSD) |
| **relatime** | Met à jour le temps d'accès intelligemment |

#### Options spécifiques FAT32/NTFS

| Option | Signification |
|--------|---------------|
| **uid=1000** | Propriétaire des fichiers (votre utilisateur) |
| **gid=1000** | Groupe des fichiers |
| **umask=022** | Permissions par défaut |
| **iocharset=utf8** | Encodage des caractères |

### Combiner plusieurs options

**Syntaxe** : Séparées par des virgules (sans espaces) :

```
defaults,noatime,nofail
ro,noexec,nodev
rw,uid=1000,gid=1000,umask=022
```

### Exemples courants

**Partition Linux standard** :
```
defaults
```

**Partition Windows (NTFS)** :
```
defaults,permissions,nofail
```

**Clé USB (FAT32)** :
```
defaults,uid=1000,gid=1000,umask=022,nofail
```

**Partition en lecture seule** :
```
ro,noexec,nodev
```

**SSD optimisé** :
```
defaults,noatime,discard
```

**Disque externe (peut être débranché)** :
```
defaults,nofail
```

💡 **Option `nofail`** : **ESSENTIELLE** pour les disques externes ! Sans elle, le système peut bloquer au démarrage si le disque n'est pas branché.

---

## Colonne 5 : Dump

**Qu'est-ce que c'est ?**
Indique si la partition doit être sauvegardée par l'utilitaire `dump` (ancien outil de sauvegarde).

**Valeurs** :
- **0** = Non sauvegardé (recommandé par défaut)
- **1** = Sauvegardé

**En pratique** :
L'outil `dump` est **rarement utilisé** de nos jours. Mettez **0** partout sauf si vous utilisez spécifiquement cet outil.

---

## Colonne 6 : Pass (ordre de vérification)

**Qu'est-ce que c'est ?**
Ordre de vérification du système de fichiers au démarrage avec `fsck`.

**Valeurs** :
- **0** = Pas de vérification
- **1** = Vérifié en premier (réservé pour `/`)
- **2** = Vérifié ensuite (autres partitions)

**Règles** :

```
/         →  1  (partition racine)
/home     →  2  (autre partition Linux)
/boot/efi →  1  (partition de boot)
swap      →  0  (pas de vérification)
NTFS      →  0  (Windows le vérifie)
Réseau    →  0  (pas de vérification)
```

---

## Exemples de lignes fstab complètes

### Partition Linux (ext4)

```
UUID=abc123-def456-ghi789  /home  ext4  defaults  0  2
```

### Partition Windows (NTFS)

```
UUID=AB12CD34EF567890  /mnt/windows  ntfs-3g  defaults,permissions,nofail  0  0
```

### Clé USB (FAT32) - montage automatique

```
UUID=A4B2-C3D4  /mnt/cle-usb  vfat  defaults,uid=1000,gid=1000,umask=022,nofail  0  0
```

### Partition swap

```
UUID=stu901-vwx234-yza567  none  swap  sw  0  0
```

### Partition EFI

```
UUID=A4B2-C3D4  /boot/efi  vfat  umask=0077  0  1
```

### Disque externe (peut être débranché)

```
UUID=jkl012-mno345-pqr678  /mnt/backup  ext4  defaults,nofail  0  0
```

### Partition en lecture seule

```
UUID=xyz789-abc012-def345  /mnt/archives  ext4  ro,noexec  0  2
```

### Partage réseau Samba

```
//192.168.1.10/Partage  /mnt/nas  cifs  credentials=/home/pierre/.smbcredentials,nofail  0  0
```

### Partage NFS

```
192.168.1.10:/export/data  /mnt/nfs  nfs  defaults,nofail  0  0
```

### Bind mount (monter un dossier ailleurs)

```
/home/pierre/Dropbox  /mnt/dropbox  none  bind  0  0
```

---

## Modifier /etc/fstab en sécurité

### Étape 1 : Sauvegarder

**TOUJOURS** sauvegarder avant de modifier :

```bash
sudo cp /etc/fstab /etc/fstab.backup
```

**Pour restaurer en cas de problème** :
```bash
sudo cp /etc/fstab.backup /etc/fstab
```

### Étape 2 : Préparer les informations

**Trouver l'UUID** :
```bash
sudo blkid
```

**Créer le point de montage** :
```bash
sudo mkdir /mnt/mon-disque
```

**Trouver votre UID/GID** (pour FAT32/NTFS) :
```bash
id
# Résultat : uid=1000(pierre) gid=1000(pierre) ...
```

### Étape 3 : Éditer le fichier

**Avec nano (éditeur simple)** :
```bash
sudo nano /etc/fstab
```

**Avec vim** :
```bash
sudo vim /etc/fstab
```

**Avec un éditeur graphique** :
```bash
sudo xed /etc/fstab
```

### Étape 4 : Ajouter votre ligne

**Exemple d'ajout** :
```
# Mon disque de données
UUID=jkl012-mno345-pqr678  /mnt/donnees  ext4  defaults,nofail  0  2
```

💡 **Conseils** :
- Ajoutez un commentaire (ligne commençant par #) pour vous rappeler à quoi sert le montage
- Alignez les colonnes pour plus de lisibilité
- Une seule ligne par montage

### Étape 5 : Sauvegarder

**Dans nano** : `Ctrl+O` puis `Entrée` puis `Ctrl+X`
**Dans vim** : `:wq` puis `Entrée`
**Dans xed** : Menu Fichier → Enregistrer

### Étape 6 : Tester SANS redémarrer

**Commande magique** :
```bash
sudo mount -a
```

**Ce qu'elle fait** :
- Monte toutes les entrées de fstab qui ne sont pas encore montées
- Révèle les erreurs de syntaxe AVANT le redémarrage

**Si succès** :
```bash
# Aucun message = tout va bien !

# Vérifier que c'est monté :
df -h | grep mon-disque
```

**Si erreur** :
```bash
mount: wrong fs type, bad option, bad superblock...
# Il y a un problème ! Corrigez avant de redémarrer
```

### Étape 7 : Vérifier et redémarrer

**Vérifier que tout est OK** :
```bash
mount | grep mon-disque
ls /mnt/mon-disque
```

**Si tout fonctionne** :
```bash
sudo reboot
# Après redémarrage, vérifiez que tout est toujours monté
```

---

## Cas d'usage pratiques

### 1. Monter automatiquement une partition Windows

**Scénario** : Dual-boot, accès à la partition Windows depuis Linux.

**1. Trouver l'UUID** :
```bash
sudo blkid | grep ntfs
# /dev/sda3: UUID="AB12CD34EF567890" TYPE="ntfs"
```

**2. Créer le point de montage** :
```bash
sudo mkdir /mnt/windows
```

**3. Ajouter à fstab** :
```bash
sudo nano /etc/fstab
```

**Ajouter** :
```
# Partition Windows C:
UUID=AB12CD34EF567890  /mnt/windows  ntfs-3g  defaults,permissions,nofail  0  0
```

**4. Tester** :
```bash
sudo mount -a
ls /mnt/windows
```

⚠️ **Note** : Désactivez Fast Startup dans Windows, sinon la partition peut être en lecture seule.

### 2. Monter un disque de données au démarrage

**Scénario** : Disque dur secondaire pour vos fichiers.

```bash
# UUID
sudo blkid /dev/sdb1

# Point de montage
sudo mkdir /mnt/donnees

# Ligne fstab
UUID=jkl012-mno345-pqr678  /mnt/donnees  ext4  defaults  0  2

# Tester
sudo mount -a
```

### 3. Monter un disque externe (amovible)

**Scénario** : Disque USB externe qui n'est pas toujours branché.

```bash
# Ligne fstab avec nofail (important !)
UUID=xyz789-abc012-def345  /mnt/backup  ext4  defaults,nofail  0  0
```

💡 **`nofail`** permet au système de démarrer même si le disque n'est pas branché.

### 4. Partition swap supplémentaire

**Scénario** : Ajouter une partition swap.

```bash
# Créer la partition swap (avec GParted)
# Puis trouver l'UUID :
sudo blkid | grep swap

# Ligne fstab
UUID=stu901-vwx234-yza567  none  swap  sw  0  0

# Activer
sudo swapon -a

# Vérifier
swapon --show
```

### 5. Partage réseau Samba permanent

**Scénario** : Monter un dossier partagé Windows/NAS au démarrage.

**1. Créer le fichier de credentials** :
```bash
nano ~/.smbcredentials
```

**Contenu** :
```
username=votre_utilisateur
password=votre_mot_de_passe
domain=WORKGROUP
```

**Protéger le fichier** :
```bash
chmod 600 ~/.smbcredentials
```

**2. Créer le point de montage** :
```bash
sudo mkdir /mnt/nas
```

**3. Ligne fstab** :
```
//192.168.1.10/Partage  /mnt/nas  cifs  credentials=/home/pierre/.smbcredentials,uid=1000,gid=1000,nofail  0  0
```

**4. Tester** :
```bash
sudo mount -a
ls /mnt/nas
```

### 6. Optimisation SSD

**Scénario** : Partition sur SSD avec optimisations.

```bash
# Ligne fstab avec options SSD
UUID=abc123-def456-ghi789  /  ext4  defaults,noatime,discard  0  1
```

**Options** :
- **noatime** : N'enregistre pas le temps d'accès (moins d'écritures)
- **discard** : Active TRIM (nettoyage des cellules supprimées)

### 7. Montage manuel (noauto)

**Scénario** : Partition disponible mais pas montée automatiquement.

```bash
# Ligne fstab avec noauto
UUID=jkl012-mno345-pqr678  /mnt/archives  ext4  noauto,defaults  0  0

# Pour monter quand vous en avez besoin :
sudo mount /mnt/archives

# Pour démonter :
sudo umount /mnt/archives
```

**Avantage** : La ligne est prête, vous pouvez monter rapidement avec juste `sudo mount /mnt/archives`.

---

## Dépannage

### Problème : Le système ne démarre plus

**Cause** : Erreur dans fstab.

**Solution (avec Live USB)** :

1. **Démarrez sur un Live USB** de Linux Mint
2. **Montez votre partition système** :
   ```bash
   sudo mkdir /mnt/system
   sudo mount /dev/sda2 /mnt/system  # Adaptez à votre partition
   ```
3. **Éditez fstab** :
   ```bash
   sudo nano /mnt/system/etc/fstab
   ```
4. **Corrigez l'erreur** ou commentez la ligne problématique (ajoutez # au début)
5. **Sauvegardez et redémarrez**

### Problème : mount -a donne une erreur

**Erreur courante** :
```
mount: wrong fs type, bad option, bad superblock...
```

**Causes possibles** :
1. **UUID incorrect** → Vérifiez avec `sudo blkid`
2. **Type de système de fichiers incorrect** → Vérifiez avec `sudo file -s /dev/sdX1`
3. **Options incompatibles** → Relisez la documentation du système de fichiers
4. **Point de montage inexistant** → `sudo mkdir /point/montage`
5. **Syntaxe incorrecte** → Vérifiez les virgules, pas d'espaces dans les options

### Problème : Disque monté en lecture seule

**Causes** :
1. **Windows en hibernation** (Fast Startup) → Désactivez-le dans Windows
2. **Option `ro` dans fstab** → Changez en `rw` ou `defaults`
3. **Erreurs sur le disque** → `sudo fsck /dev/sdX1`

**Solution temporaire** :
```bash
sudo mount -o remount,rw /point/montage
```

### Problème : Permissions refusées sur partition NTFS/FAT32

**Cause** : Pas d'options uid/gid.

**Solution** :
```bash
# Dans fstab, ajouter :
uid=1000,gid=1000,umask=022

# Exemple complet :
UUID=ABC123  /mnt/data  ntfs-3g  defaults,uid=1000,gid=1000,umask=022  0  0
```

### Problème : Le partage réseau ralentit le démarrage

**Cause** : Pas d'option `nofail`, le système attend le montage.

**Solution** : Ajoutez `nofail` :
```
//192.168.1.10/Partage  /mnt/nas  cifs  credentials=...,nofail  0  0
```

---

## Commandes utiles

### Voir les montages actuels

```bash
mount                    # Tous les montages
df -h                    # Utilisation de l'espace
findmnt                  # Arbre des montages (lisible)
cat /proc/mounts         # Montages du kernel
```

### Tester fstab

```bash
sudo mount -a            # Monter tout ce qui n'est pas monté
sudo umount -a           # Démonter (attention !)
```

### Vérifier un système de fichiers

```bash
sudo fsck /dev/sdX1      # Vérifier et réparer
sudo fsck -n /dev/sdX1   # Vérifier sans réparer (simulation)
```

### Démonter une partition

```bash
sudo umount /point/montage
sudo umount /dev/sdX1
```

### Remonter avec nouvelles options

```bash
sudo mount -o remount,rw /point/montage
```

---

## Bonnes pratiques

### ✅ À faire

1. **Toujours sauvegarder fstab** avant modification
2. **Utiliser UUID** plutôt que /dev/sdX
3. **Ajouter nofail** pour disques externes et partages réseau
4. **Tester avec mount -a** avant de redémarrer
5. **Ajouter des commentaires** pour documenter vos montages
6. **Créer les points de montage** avant de monter
7. **Vérifier les permissions** avec `ls -l /point/montage`

### ⚠️ À éviter

1. **Ne modifiez pas sans sauvegarde**
2. **N'utilisez pas /dev/sdX** pour des montages permanents
3. **N'oubliez pas nofail** pour les disques amovibles
4. **Ne redémarrez pas** sans tester avec mount -a
5. **Ne mettez pas d'espaces** dans les options (utilisez des virgules)
6. **Ne montez pas dans /home/user/** (problèmes de permissions)

### 🔧 En cas de problème

1. **Gardez un Live USB** accessible
2. **Documentez vos modifications** (commentaires dans fstab)
3. **Prenez des captures d'écran** de votre configuration
4. **Testez toujours** avant de redémarrer

---

## Alternatives à fstab

### systemd mount units (avancé)

Alternative moderne à fstab utilisant systemd :

```bash
# Créer un fichier .mount dans /etc/systemd/system/
sudo nano /etc/systemd/system/mnt-donnees.mount
```

**Plus flexible** mais **plus complexe**. Fstab reste recommandé pour les débutants.

### Montage par automount (systemd)

Monte automatiquement quand on accède au dossier :

```bash
sudo nano /etc/systemd/system/mnt-donnees.automount
```

**Avantage** : Ne monte que si nécessaire.

### AutoFS

Système de montage automatique à la demande, plus ancien.

---

## Résumé

### Points clés à retenir

1. **fstab** = fichier de configuration pour montages automatiques
2. **6 colonnes** : système, point, type, options, dump, pass
3. **UUID** : Toujours préférable à /dev/sdX
4. **nofail** : Essentiel pour disques externes
5. **Tester** : `sudo mount -a` avant de redémarrer
6. **Sauvegarder** : `sudo cp /etc/fstab /etc/fstab.backup`

### Syntaxe de base

```
UUID=...  /point/montage  type  options  0  0
```

### Exemples rapides

```bash
# Partition Linux
UUID=abc-123  /mnt/data  ext4  defaults  0  2

# Partition Windows
UUID=AB12CD34  /mnt/win  ntfs-3g  defaults,nofail  0  0

# Clé USB
UUID=A4B2-C3D4  /mnt/usb  vfat  defaults,uid=1000,nofail  0  0

# Swap
UUID=xyz-789  none  swap  sw  0  0

# Partage réseau
//192.168.1.10/share  /mnt/nas  cifs  credentials=/home/user/.creds,nofail  0  0
```

### Commandes essentielles

```bash
sudo blkid                          # Voir les UUID
sudo nano /etc/fstab               # Éditer
sudo mount -a                      # Tester
df -h                              # Vérifier
sudo cp /etc/fstab /etc/fstab.bak  # Sauvegarder
```

### Pour aller plus loin

Une fois à l'aise avec fstab, vous pourrez :
- Monter des partitions chiffrées automatiquement
- Configurer des montages réseau complexes
- Utiliser systemd mount units
- Optimiser finement les performances

Mais pour débuter, **utilisez la syntaxe simple** avec UUID, defaults, nofail, et testez toujours avec `mount -a` avant de redémarrer. La sécurité avant tout !

⏭️ [Configuration réseau et Internet](/09-configuration-reseau-et-internet/README.md)
