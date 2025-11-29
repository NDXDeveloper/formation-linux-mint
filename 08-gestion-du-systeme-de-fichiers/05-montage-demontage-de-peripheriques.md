🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.5 Montage/démontage de périphériques

## Introduction

### Qu'est-ce que le montage ?

Si vous venez de Windows, vous êtes habitué à ce qu'une clé USB apparaisse automatiquement avec une lettre (E:, F:, etc.) quand vous la branchez. Sous Linux, le principe est différent : on parle de **montage** et de **démontage**.

**Montage** = Rendre un périphérique (clé USB, disque dur, partition) accessible dans l'arborescence du système de fichiers.

**Démontage** = Détacher proprement le périphérique de l'arborescence avant de le retirer physiquement.

### Analogie pour comprendre

Imaginez votre système Linux comme une bibliothèque :

**Windows** :
- Vous ajoutez une nouvelle étagère (clé USB)
- Elle devient automatiquement "Étagère E"
- Elle existe indépendamment des autres

**Linux** :
- Vous avez UN SEUL système d'étagères (l'arborescence `/`)
- Quand vous branchez une clé USB, vous devez l'"accrocher" quelque part dans ce système
- Cette action s'appelle **monter**
- L'endroit où vous l'accrochez s'appelle un **point de montage**
- Avant de retirer la clé, vous devez la "décrocher" proprement
- Cette action s'appelle **démonter**

### Pourquoi monter/démonter ?

**Avantages du système Linux** :
- ✅ **Contrôle total** : Vous décidez où et comment monter un périphérique
- ✅ **Sécurité** : Évite les débranchements accidentels avec données non sauvegardées
- ✅ **Flexibilité** : Montage avec options spécifiques (lecture seule, droits, etc.)
- ✅ **Intégration** : Tout s'intègre dans une arborescence cohérente

**En pratique** :
Rassurez-vous, Linux Mint monte **automatiquement** la plupart des périphériques, exactement comme Windows. Vous n'avez généralement rien à faire !

## Montage automatique sous Linux Mint

### Ce qui se monte automatiquement

Quand vous branchez un périphérique, Linux Mint le détecte et le monte automatiquement dans :

```
/media/votrenom/
```

**Exemples** :
```
/media/pierre/CléUSB
/media/pierre/DisqueExterne
/media/pierre/4A3B-F2E1  (si pas de nom)
/media/pierre/CANON_EOS  (appareil photo)
```

### Comment ça fonctionne ?

1. **Vous branchez** une clé USB
2. **udev** (le gestionnaire de périphériques) détecte le branchement
3. **udisks2** (le gestionnaire de disques) monte automatiquement
4. **Le gestionnaire de fichiers** affiche une notification
5. **Le périphérique apparaît** dans la barre latérale de Nemo

### Voir les périphériques montés

**Méthode graphique - Gestionnaire de fichiers (Nemo)** :

1. Ouvrez Nemo
2. Dans la **barre latérale gauche**, sous "Périphériques" :
   - Vos disques durs
   - Clés USB branchées
   - Disques externes
   - Partitions Windows (si dual-boot)

**Méthode graphique - Outil Disques** :

1. **Menu** → **Administration** → **Disques**
2. Tous vos périphériques sont listés à gauche
3. Les partitions montées ont l'icône ▶ visible

**Méthode en ligne de commande** :

```bash
# Voir tous les montages
mount

# Voir seulement les principaux (plus lisible)
df -h

# Liste visuelle des périphériques
lsblk
```

**Résultat de `lsblk`** :
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 465.8G  0 disk
├─sda1   8:1    0   512M  0 part /boot/efi
├─sda2   8:2    0    50G  0 part /
└─sda3   8:3    0 407.3G  0 part /home
sdb      8:16   1  14.9G  0 disk
└─sdb1   8:17   1  14.9G  0 part /media/pierre/CléUSB
```

## Démontage (éjection) de périphériques

### Pourquoi démonter avant de retirer ?

⚠️ **TRÈS IMPORTANT** : Ne débranchez **JAMAIS** une clé USB ou un disque externe sans l'avoir démonté !

**Raisons** :
1. **Cache d'écriture** : Linux garde des données en mémoire avant de les écrire réellement
2. **Table de fichiers** : Peut être en cours de modification
3. **Corruption** : Retirer sans démonter peut corrompre le système de fichiers

**Conséquence** :
Retirer sans démonter = risque de **perte de données** ou de **corruption du périphérique**.

### Méthode 1 : Via le gestionnaire de fichiers (la plus simple)

**Dans Nemo** :

1. Dans la barre latérale, repérez votre périphérique sous "Périphériques"
2. **Clic droit** sur le périphérique → **Éjecter** ou **Démonter en toute sécurité**
3. Attendez le message de confirmation
4. Vous pouvez maintenant retirer physiquement le périphérique

**Ou** :

1. Cliquez sur l'**icône d'éjection** (▶) à côté du nom du périphérique
2. Attendez qu'il disparaisse de la liste
3. Retirez le périphérique

💡 **Différence Éjecter vs Démonter** :
- **Démonter** : Détache le système de fichiers (le périphérique reste branché)
- **Éjecter** : Démonte ET prépare le retrait physique (recommandé pour USB)

### Méthode 2 : Via l'outil Disques

1. Ouvrez **Disques**
2. Sélectionnez le périphérique à gauche
3. Cliquez sur le bouton **⏹ (Arrêter)** ou **▶ (Démonter)**
4. Attendez la confirmation
5. Retirez le périphérique

### Méthode 3 : En ligne de commande

**Démonter** :
```bash
# Syntaxe
sudo umount /point/de/montage

# Exemple
sudo umount /media/pierre/CléUSB
```

**Ou avec le périphérique** :
```bash
sudo umount /dev/sdb1
```

**Éjecter un CD/DVD** :
```bash
eject
# ou
eject /dev/sr0
```

### Que faire si le démontage échoue ?

**Message d'erreur** : "Le périphérique est occupé" ou "target is busy"

**Cause** : Un programme utilise encore des fichiers sur le périphérique.

**Solutions** :

1. **Fermez tous les programmes** qui pourraient utiliser des fichiers du périphérique
2. **Fermez le terminal** si vous étiez dans un dossier du périphérique
3. **Fermez Nemo** s'il affiche le contenu du périphérique

**Si ça ne suffit pas, voir qui utilise le périphérique** :
```bash
lsof /media/pierre/CléUSB
```

**Forcer le démontage** (en dernier recours) :
```bash
sudo umount -f /media/pierre/CléUSB
# ou encore plus fort (déconseillé)
sudo umount -l /media/pierre/CléUSB
```

⚠️ **Attention** : Forcer peut entraîner une perte de données !

## Montage manuel de périphériques

### Pourquoi monter manuellement ?

La plupart du temps, le montage automatique suffit. Mais parfois vous voudrez :
- Monter une partition qui ne se monte pas automatiquement
- Choisir un point de montage spécifique
- Monter avec des options particulières (lecture seule, droits spéciaux)
- Monter un partage réseau
- Monter une image ISO

### Méthode 1 : Via l'outil Disques (graphique)

**Monter une partition** :

1. Ouvrez **Disques**
2. Sélectionnez le disque à gauche
3. Sélectionnez la partition à monter
4. Cliquez sur le bouton **▶ (Monter la partition)**
5. La partition devient accessible dans `/media/votrenom/`

**Options de montage** :

1. Sélectionnez la partition
2. Cliquez sur **⚙ (Options de montage supplémentaires)**
3. Désactivez **Valeurs par défaut de session utilisateur**
4. Configurez :
   - **Point de montage** : Où monter
   - **Au démarrage** : Monter automatiquement ou non
   - **Options de montage** : `ro` (lecture seule), `noexec` (pas d'exécution), etc.
5. Cliquez sur **OK**

### Méthode 2 : En ligne de commande

**Syntaxe de base** :
```bash
sudo mount [options] PÉRIPHÉRIQUE POINT_DE_MONTAGE
```

**Étapes détaillées** :

**1. Identifier le périphérique** :
```bash
lsblk
# ou
sudo fdisk -l
```

Notez le nom du périphérique, par exemple `/dev/sdb1`

**2. Créer un point de montage** (si nécessaire) :
```bash
sudo mkdir /mnt/ma-cle-usb
```

💡 **Conventions** :
- `/mnt/` : Pour montages temporaires
- `/media/` : Pour périphériques amovibles (géré automatiquement)
- `/home/votrenom/Dossier/` : Évitez, risque de confusion

**3. Monter le périphérique** :
```bash
sudo mount /dev/sdb1 /mnt/ma-cle-usb
```

**4. Vérifier** :
```bash
df -h | grep ma-cle-usb
```

**5. Utiliser** :
```bash
ls /mnt/ma-cle-usb
```

**6. Démonter quand terminé** :
```bash
sudo umount /mnt/ma-cle-usb
```

### Options de montage courantes

**Lecture seule (read-only)** :
```bash
sudo mount -o ro /dev/sdb1 /mnt/ma-cle-usb
```

**Lecture-écriture (read-write)** :
```bash
sudo mount -o rw /dev/sdb1 /mnt/ma-cle-usb
```

**Avec permissions utilisateur** :
```bash
# Pour FAT32/exFAT (pas de permissions natives)
sudo mount -o uid=1000,gid=1000 /dev/sdb1 /mnt/ma-cle-usb
```

💡 **Note** : `1000` est généralement l'UID/GID du premier utilisateur. Trouvez le vôtre avec `id`.

**Spécifier le type de système de fichiers** :
```bash
sudo mount -t ntfs /dev/sdb1 /mnt/ma-cle-usb
# ou
sudo mount -t vfat /dev/sdb1 /mnt/ma-cle-usb  # FAT32
```

**Options multiples** :
```bash
sudo mount -o rw,uid=1000,gid=1000,umask=022 /dev/sdb1 /mnt/ma-cle-usb
```

## Cas d'usage pratiques

### 1. Monter une partition Windows (NTFS)

**Scénario** : Vous êtes en dual-boot et voulez accéder à votre partition Windows.

**Automatique** :
Elle devrait apparaître dans Nemo sous "Périphériques".

**Manuel** :
```bash
# Identifier la partition Windows
sudo fdisk -l | grep NTFS

# Créer un point de montage
sudo mkdir /mnt/windows

# Monter
sudo mount -t ntfs-3g /dev/sda3 /mnt/windows

# Accéder
cd /mnt/windows
ls
```

⚠️ **Si Windows est en hibernation** (Fast Startup), le montage sera en lecture seule. Désactivez Fast Startup dans Windows.

### 2. Monter une image ISO

**Scénario** : Vous voulez explorer le contenu d'un fichier .iso sans le graver.

```bash
# Créer le point de montage
sudo mkdir /mnt/iso

# Monter l'ISO (lecture seule)
sudo mount -o loop ~/Téléchargements/ubuntu.iso /mnt/iso

# Explorer
ls /mnt/iso

# Démonter
sudo umount /mnt/iso
```

💡 **Option `-o loop`** : Nécessaire pour monter un fichier comme s'il était un périphérique.

### 3. Monter un partage réseau (Samba/CIFS)

**Scénario** : Accéder à un dossier partagé sur un PC Windows ou un NAS.

**Installer les outils** :
```bash
sudo apt install cifs-utils
```

**Monter le partage** :
```bash
# Créer le point de montage
sudo mkdir /mnt/partage-reseau

# Monter avec authentification
sudo mount -t cifs //192.168.1.10/Partage /mnt/partage-reseau -o username=utilisateur,password=motdepasse

# Ou sans authentification (si partage public)
sudo mount -t cifs //192.168.1.10/Public /mnt/partage-reseau -o guest
```

**Version plus sécurisée** (mot de passe dans un fichier) :
```bash
# Créer un fichier de credentials
echo "username=utilisateur" > ~/.smbcredentials
echo "password=motdepasse" >> ~/.smbcredentials
chmod 600 ~/.smbcredentials

# Monter avec le fichier
sudo mount -t cifs //192.168.1.10/Partage /mnt/partage-reseau -o credentials=/home/votrenom/.smbcredentials
```

### 4. Monter un partage NFS (Linux)

**Scénario** : Accéder à un partage NFS depuis un autre Linux ou NAS.

**Installer les outils** :
```bash
sudo apt install nfs-common
```

**Monter** :
```bash
sudo mkdir /mnt/nfs-partage
sudo mount -t nfs 192.168.1.10:/export/partage /mnt/nfs-partage
```

### 5. Monter une clé USB qui ne se monte pas automatiquement

**Scénario** : Votre clé USB n'apparaît pas automatiquement.

**1. Vérifier qu'elle est détectée** :
```bash
lsblk
# Elle devrait apparaître comme /dev/sdb ou /dev/sdc
```

**2. Vérifier les messages système** :
```bash
dmesg | tail -20
# Cherchez des erreurs
```

**3. Monter manuellement** :
```bash
sudo mkdir /mnt/cle-usb
sudo mount /dev/sdb1 /mnt/cle-usb
```

**4. Si erreur "système de fichiers inconnu"** :
```bash
# Vérifier le type
sudo file -s /dev/sdb1

# Essayer avec type explicite
sudo mount -t vfat /dev/sdb1 /mnt/cle-usb  # FAT32
# ou
sudo mount -t ntfs-3g /dev/sdb1 /mnt/cle-usb  # NTFS
```

### 6. Remonter une partition en lecture-écriture

**Scénario** : Une partition est montée en lecture seule et vous voulez écrire dessus.

```bash
# Remonter avec permissions d'écriture
sudo mount -o remount,rw /point/de/montage

# Exemple
sudo mount -o remount,rw /media/pierre/DisqueExterne
```

## Montage automatique au démarrage

### Fichier /etc/fstab

Pour qu'une partition se monte **automatiquement à chaque démarrage**, on l'ajoute au fichier `/etc/fstab` (File System TABle).

⚠️ **ATTENTION** : Une erreur dans `/etc/fstab` peut empêcher le système de démarrer ! Faites une sauvegarde avant de modifier.

**Sauvegarder fstab** :
```bash
sudo cp /etc/fstab /etc/fstab.backup
```

**Voir le contenu actuel** :
```bash
cat /etc/fstab
```

**Exemple de contenu** :
```
# <système de fichiers>  <point de montage>  <type>  <options>  <dump>  <pass>
UUID=abc-123-def         /                   ext4    defaults   0       1
UUID=456-789-ghi         /home               ext4    defaults   0       2
UUID=A4B2-C3D4           /boot/efi           vfat    umask=0077 0       1
```

### Ajouter un montage automatique

**1. Trouver l'UUID de la partition** :
```bash
sudo blkid
```

**Résultat** :
```
/dev/sdb1: UUID="4A3B-F2E1" TYPE="vfat" LABEL="MaCléUSB"
```

Notez l'UUID : `4A3B-F2E1`

**2. Créer le point de montage** :
```bash
sudo mkdir /mnt/mon-disque
```

**3. Éditer /etc/fstab** :
```bash
sudo nano /etc/fstab
```

**4. Ajouter une ligne** :
```
UUID=4A3B-F2E1  /mnt/mon-disque  vfat  defaults,nofail  0  0
```

**Explication des colonnes** :
- **UUID=...** : Identifiant unique de la partition
- **/mnt/mon-disque** : Point de montage
- **vfat** : Type de système de fichiers (FAT32)
- **defaults,nofail** : Options (nofail = continuer à démarrer si échec)
- **0** : Dump (sauvegarde) - 0 = non
- **0** : Pass (vérification) - 0 = non, 1 = en premier, 2 = après

**5. Tester sans redémarrer** :
```bash
sudo mount -a
```

Si pas d'erreur, c'est bon ! Sinon, corrigez le fichier.

**6. Vérifier** :
```bash
df -h | grep mon-disque
```

💡 **Option `nofail`** : Importante ! Sans elle, si le disque n'est pas branché au démarrage, le système peut bloquer.

### Options fstab courantes

**Pour partition Linux (ext4)** :
```
UUID=xxx  /mnt/data  ext4  defaults  0  2
```

**Pour partition Windows (NTFS)** :
```
UUID=xxx  /mnt/windows  ntfs-3g  defaults,permissions  0  0
```

**Pour partition FAT32 accessible par tous** :
```
UUID=xxx  /mnt/partage  vfat  defaults,uid=1000,gid=1000,umask=022  0  0
```

**Pour partition en lecture seule** :
```
UUID=xxx  /mnt/readonly  ext4  ro  0  0
```

**Pour partition à monter manuellement** (mais entrée prête) :
```
UUID=xxx  /mnt/manuel  ext4  noauto  0  0
```

Avec `noauto`, vous pourrez monter avec :
```bash
sudo mount /mnt/manuel
```

## Comprendre les messages d'erreur

### "mount: wrong fs type, bad option, bad superblock..."

**Cause** : Système de fichiers non reconnu ou corrompu.

**Solutions** :
1. Spécifiez le type avec `-t` :
```bash
sudo mount -t ntfs-3g /dev/sdb1 /mnt/test
```

2. Vérifiez si les outils sont installés :
```bash
sudo apt install ntfs-3g exfat-fuse exfat-utils
```

3. Vérifiez l'état du périphérique :
```bash
sudo fsck /dev/sdb1
```

### "mount: /dev/sdb1 is already mounted"

**Cause** : Le périphérique est déjà monté ailleurs.

**Solution** :
```bash
# Voir où il est monté
mount | grep sdb1

# Démonter
sudo umount /dev/sdb1

# Remonter au bon endroit
sudo mount /dev/sdb1 /mnt/nouveau-point
```

### "mount: only root can do that"

**Cause** : Vous avez oublié `sudo`.

**Solution** :
```bash
sudo mount /dev/sdb1 /mnt/test
```

### "mount: mount point does not exist"

**Cause** : Le point de montage n'existe pas.

**Solution** :
```bash
sudo mkdir /mnt/test
sudo mount /dev/sdb1 /mnt/test
```

### "umount: target is busy"

**Cause** : Des fichiers sont encore ouverts ou vous êtes dans le dossier.

**Solutions** :
1. Sortez du dossier :
```bash
cd ~
```

2. Fermez tous les programmes qui utilisent des fichiers

3. Voir qui utilise le point de montage :
```bash
lsof /mnt/test
```

4. Forcer (en dernier recours) :
```bash
sudo umount -l /mnt/test
```

## Outils graphiques supplémentaires

### Gestionnaire de disques USB

**Certains environnements** ont un outil dédié pour gérer les USB :

```bash
# Installer usbmount (montage automatique avancé)
sudo apt install usbmount
```

### GNOME Disks (déjà installé)

L'outil **Disques** que nous avons vu est parfait pour :
- Voir tous les périphériques
- Monter/démonter graphiquement
- Configurer les montages automatiques

## Bonnes pratiques

### ✅ À faire

1. **Toujours démonter** avant de retirer un périphérique USB
2. **Utiliser UUID** dans `/etc/fstab` plutôt que `/dev/sdX`
3. **Ajouter `nofail`** pour les disques externes dans fstab
4. **Tester avec `mount -a`** après modification de fstab
5. **Créer des points de montage** dans `/mnt/` pour vos montages personnels

### ⚠️ À éviter

1. **Ne débranchez jamais** sans démonter (risque de corruption)
2. **Ne modifiez pas fstab** sans sauvegarde
3. **N'utilisez pas `/dev/sdX`** dans fstab (peut changer au redémarrage)
4. **Ne forcez pas** le démontage sauf en dernier recours
5. **N'oubliez pas `sudo`** pour les montages/démontages

### 🔧 Dépannage rapide

**Périphérique non détecté** :
```bash
lsusb  # Voir les périphériques USB
dmesg | tail -20  # Voir les messages du kernel
```

**Partition corrompue** :
```bash
sudo fsck /dev/sdb1  # Vérifier et réparer
```

**Problème de permissions** :
```bash
# Pour FAT32/exFAT
sudo mount -o uid=$(id -u),gid=$(id -g) /dev/sdb1 /mnt/test
```

## Commandes de référence rapide

**Lister les périphériques** :
```bash
lsblk                    # Vue arborescente
df -h                    # Espace disque
mount                    # Tous les montages
sudo fdisk -l            # Détails complets
sudo blkid               # UUID et types
```

**Monter** :
```bash
sudo mount /dev/sdb1 /mnt/point            # Montage basique
sudo mount -t ntfs /dev/sdb1 /mnt/point    # Avec type
sudo mount -o ro /dev/sdb1 /mnt/point      # Lecture seule
sudo mount -a                              # Monter tout dans fstab
```

**Démonter** :
```bash
sudo umount /mnt/point           # Démontage normal
sudo umount /dev/sdb1            # Par périphérique
sudo umount -f /mnt/point        # Forcer
sudo umount -l /mnt/point        # Lazy (attend que libre)
eject /dev/sr0                   # Éjecter CD/DVD
```

**Diagnostiquer** :
```bash
lsof /mnt/point                  # Qui utilise ?
mount | grep sdb1                # Où est monté ?
sudo fsck /dev/sdb1              # Vérifier/réparer
```

## Résumé

### Points clés à retenir

1. **Montage** : Rendre un périphérique accessible dans l'arborescence
2. **Démontage** : Détacher proprement avant retrait physique
3. **Automatique** : Linux Mint monte automatiquement dans `/media/votrenom/`
4. **Toujours démonter** : Avant de retirer une clé USB (risque de corruption sinon)
5. **fstab** : Pour montages automatiques au démarrage
6. **UUID** : Identifiant stable pour fstab

### Commandes essentielles

```bash
lsblk                           # Lister les périphériques
sudo mount /dev/sdb1 /mnt/test  # Monter
sudo umount /mnt/test           # Démonter
sudo blkid                      # Voir les UUID
```

### Pour aller plus loin

Une fois à l'aise, vous pourrez :
- Configurer des montages réseau permanents
- Monter des partitions chiffrées
- Utiliser des montages bind
- Créer des scripts de montage personnalisés

Mais pour débuter, **laissez Linux Mint gérer automatiquement**, et utilisez simplement l'icône d'éjection dans Nemo avant de retirer vos clés USB. C'est simple et sûr !

⏭️ [Liens symboliques et liens durs](/08-gestion-du-systeme-de-fichiers/06-liens-symboliques-et-liens-durs.md)
