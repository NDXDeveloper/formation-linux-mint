🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.2 Les partitions et points de montage

## Introduction

Si vous venez de Windows, vous êtes habitué à voir vos disques durs comme C:, D:, E:, etc. Sous Linux, les choses fonctionnent différemment : au lieu d'avoir des lettres de lecteurs séparées, tout s'intègre dans une **arborescence unique** grâce au concept de **point de montage**.

Ce chapitre va vous expliquer ce que sont les partitions et comment Linux les "monte" dans son arborescence pour les rendre accessibles.

## Qu'est-ce qu'une partition ?

### Définition simple

Une **partition** est une division logique d'un disque dur physique. C'est comme diviser un grand terrain en plusieurs parcelles distinctes.

### Pourquoi partitionner ?

**Avantages des partitions** :
- **Organisation** : séparer le système des données personnelles
- **Sécurité** : isoler les données importantes
- **Multi-boot** : avoir plusieurs systèmes d'exploitation sur le même disque
- **Performance** : optimiser différentes zones selon leur usage
- **Facilité de sauvegarde** : sauvegarder uniquement certaines partitions

### Exemple concret

Imaginez un disque dur de 500 Go que vous pourriez diviser ainsi :
- **Partition 1** : 100 Go pour Linux Mint
- **Partition 2** : 300 Go pour vos documents et fichiers personnels
- **Partition 3** : 100 Go pour Windows (dual-boot)

## Différence entre Windows et Linux

### Sous Windows

```
C:\ ──→ Disque principal (partition 1)
D:\ ──→ Deuxième partition ou disque
E:\ ──→ Clé USB
F:\ ──→ Lecteur DVD
```

Chaque partition ou périphérique a sa **propre lettre** et est **indépendant**.

### Sous Linux

```
/
├── home/          ──→ peut être sur la partition 1
├── var/           ──→ peut être sur la partition 2
└── media/
    └── cle-usb/   ──→ peut être la partition 3 montée ici
```

Tout est **intégré dans une arborescence unique** qui commence par `/`. Les différentes partitions sont "accrochées" (montées) à différents endroits de cette arborescence.

## Le concept de point de montage

### Qu'est-ce qu'un point de montage ?

Un **point de montage** est un **dossier** dans l'arborescence Linux où une partition est rendue accessible. C'est comme une porte d'entrée vers le contenu d'une partition.

### Analogie pour comprendre

Imaginez votre système de fichiers comme un grand arbre :
- L'arbre principal est votre partition système
- Vous pouvez "greffer" d'autres branches (partitions) à différents endroits de l'arbre
- Chaque endroit où vous greffez une branche est un **point de montage**

### Exemple visuel

```
Disque physique /dev/sda (500 Go)
│
├── /dev/sda1 (partition EFI - 512 Mo)    ──→ montée sur /boot/efi
├── /dev/sda2 (partition système - 100 Go) ──→ montée sur /
├── /dev/sda3 (partition swap - 8 Go)      ──→ mémoire d'échange
└── /dev/sda4 (partition données - 391 Go) ──→ montée sur /home

Résultat visible pour l'utilisateur :
/
├── boot/
│   └── efi/        ← contenu de /dev/sda1
├── home/           ← contenu de /dev/sda4
│   └── pierre/
│       ├── Documents/
│       └── Images/
└── [reste du système] ← contenu de /dev/sda2
```

## Nomenclature des disques et partitions sous Linux

### Identification des disques

Linux nomme les disques différemment de Windows :

| Type de disque | Nomenclature | Exemples |
|----------------|--------------|----------|
| Disque SATA/SSD | `/dev/sd*` | `/dev/sda`, `/dev/sdb` |
| Ancien disque IDE | `/dev/hd*` | `/dev/hda` (rare aujourd'hui) |
| Disque NVMe (SSD moderne) | `/dev/nvme*` | `/dev/nvme0n1` |
| Carte SD | `/dev/mmcblk*` | `/dev/mmcblk0` |

**Explication** :
- `sd` = SCSI Disk (utilisé pour SATA et USB aussi)
- La lettre qui suit indique l'ordre : `a` pour le premier, `b` pour le deuxième, etc.

### Identification des partitions

Les partitions sont numérotées après le nom du disque :

**Pour un disque SATA/SSD** :
- `/dev/sda` → le disque entier
- `/dev/sda1` → première partition
- `/dev/sda2` → deuxième partition
- `/dev/sda3` → troisième partition

**Pour un disque NVMe** :
- `/dev/nvme0n1` → le disque entier
- `/dev/nvme0n1p1` → première partition
- `/dev/nvme0n1p2` → deuxième partition

💡 **Astuce** : Le "p" dans NVMe signifie "partition" pour éviter la confusion.

## Types de partitions courants sous Linux

### 1. Partition système (/)

- **Point de montage** : `/` (racine)
- **Taille recommandée** : 30-50 Go minimum (50-100 Go confortable)
- **Système de fichiers** : ext4 (le plus courant)
- **Contenu** : Le système d'exploitation Linux Mint et les applications

### 2. Partition /home (optionnelle mais recommandée)

- **Point de montage** : `/home`
- **Taille recommandée** : Le reste de l'espace disponible
- **Système de fichiers** : ext4
- **Contenu** : Vos fichiers personnels, documents, images, etc.

**Avantage majeur** : Vous pouvez réinstaller Linux sans perdre vos données !

### 3. Partition swap (mémoire d'échange)

- **Point de montage** : aucun (c'est une partition spéciale)
- **Taille recommandée** :
  - 8 Go de RAM ou moins → swap = RAM
  - Plus de 8 Go de RAM → swap = 4-8 Go (ou aucun si vous avez beaucoup de RAM)
- **Type** : linux-swap
- **Utilité** : Extension de la RAM sur le disque (comme le fichier pagefile.sys sous Windows)

💡 **Note moderne** : Avec 16 Go de RAM ou plus, le swap est moins critique, mais reste utile pour l'hibernation.

### 4. Partition EFI (sur les systèmes UEFI)

- **Point de montage** : `/boot/efi`
- **Taille** : 512 Mo à 1 Go
- **Système de fichiers** : FAT32
- **Contenu** : Chargeur de démarrage (GRUB) et fichiers UEFI

⚠️ **Important** : Si vous êtes en dual-boot avec Windows, Windows a déjà créé cette partition, ne la supprimez pas !

### 5. Partition /boot (optionnelle)

- **Point de montage** : `/boot`
- **Taille** : 1 Go
- **Utilité** : Séparer les fichiers de démarrage (utile pour le chiffrement complet du disque)

## Comment fonctionne le montage ?

### Montage automatique au démarrage

Lorsque Linux Mint démarre, il lit le fichier `/etc/fstab` (File System TABle) qui contient la liste des partitions à monter automatiquement.

**Exemple simplifié de /etc/fstab** :
```
# Partition    Point-montage  Type    Options         Dump  Pass
/dev/sda2      /              ext4    defaults        0     1
/dev/sda4      /home          ext4    defaults        0     2
/dev/sda1      /boot/efi      vfat    umask=0077      0     1
/dev/sda3      none           swap    sw              0     0
```

### Montage automatique des périphériques amovibles

Les clés USB, disques externes et autres périphériques sont automatiquement montés dans `/media/votrenom/` :

```
/media/
└── pierre/
    ├── CléUSB/          ← clé USB insérée
    ├── DisqueExterne/   ← disque USB externe
    └── DONNEES/         ← autre partition détectée
```

## Voir les partitions montées

### Méthode graphique : Utilitaire de disques

1. **Menu** → **Administration** → **Disques** (ou "Disks")
2. Sélectionnez un disque dans la liste de gauche
3. Vous verrez toutes ses partitions avec :
   - Leur taille
   - Leur système de fichiers
   - Leur point de montage

### Méthode en ligne de commande

**Commande `lsblk`** (list block devices) :
```bash
lsblk
```

**Résultat exemple** :
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 465.8G  0 disk
├─sda1   8:1    0   512M  0 part /boot/efi
├─sda2   8:2    0    50G  0 part /
├─sda3   8:3    0     8G  0 part [SWAP]
└─sda4   8:4    0 407.3G  0 part /home
```

**Commande `df -h`** (disk free - human readable) :
```bash
df -h
```

**Résultat exemple** :
```
Sys. de fichiers Taille Utilisé Dispo Uti% Monté sur
/dev/sda2           50G     15G   33G  31% /
/dev/sda4          400G    120G  260G  32% /home
/dev/sda1          511M    5.3M  506M   2% /boot/efi
```

## Schémas de partitionnement courants

### Installation simple (un seul disque, débutant)

**Configuration minimale** :
```
Disque de 256 Go
├── /dev/sda1 - 512 Mo  - EFI    → /boot/efi
├── /dev/sda2 - 247 Go  - ext4   → / (système + /home ensemble)
└── /dev/sda3 - 8 Go    - swap   → [SWAP]
```

**Avantage** : Simple, tout en un
**Inconvénient** : Réinstallation = perte des données

### Installation recommandée (un seul disque)

**Configuration avec /home séparé** :
```
Disque de 512 Go
├── /dev/sda1 - 512 Mo  - EFI    → /boot/efi
├── /dev/sda2 - 50 Go   - ext4   → / (système)
├── /dev/sda3 - 8 Go    - swap   → [SWAP]
└── /dev/sda4 - 453 Go  - ext4   → /home (données)
```

**Avantage** : Vos données restent intactes lors d'une réinstallation
**Utilisation** : Configuration idéale pour la plupart des utilisateurs

### Configuration dual-boot Windows + Linux

**Disque de 512 Go** :
```
├── /dev/sda1 - 512 Mo  - EFI     → /boot/efi (partagée Windows/Linux)
├── /dev/sda2 - 128 Mo  - MSR     → Microsoft Reserved (Windows)
├── /dev/sda3 - 200 Go  - NTFS    → C:\ (Windows)
├── /dev/sda4 - 50 Go   - ext4    → / (Linux)
├── /dev/sda5 - 8 Go    - swap    → [SWAP]
└── /dev/sda6 - 253 Go  - ext4    → /home (Linux)
```

### Configuration avec SSD + HDD

**SSD 256 Go (rapide)** :
```
├── /dev/sda1 - 512 Mo  - EFI    → /boot/efi
├── /dev/sda2 - 247 Go  - ext4   → / (système)
└── /dev/sda3 - 8 Go    - swap   → [SWAP]
```

**HDD 2 To (stockage)** :
```
└── /dev/sdb1 - 2 To    - ext4   → /home (données)
```

**Avantage** : Système rapide sur SSD, beaucoup d'espace pour les données sur HDD

## Points de montage personnalisés

Vous pouvez monter une partition n'importe où dans l'arborescence :

**Exemples d'utilisation** :
- `/media/donnees` → partition de stockage
- `/mnt/partage` → partition partagée avec Windows
- `/mnt/sauvegardes` → disque de sauvegarde
- `/srv` → serveur web

**Exemple pratique** :
```
Vous avez un disque externe de 4 To pour vos films et séries
↓
Vous le montez sur /media/films
↓
Résultat : vos films sont accessibles depuis /media/films/
```

## UUID : l'identifiant unique de partition

### Qu'est-ce qu'un UUID ?

**UUID** = Universally Unique IDentifier

Chaque partition a un identifiant unique qui ne change jamais, même si vous réorganisez vos disques.

**Pourquoi c'est important ?** :
- `/dev/sda` peut devenir `/dev/sdb` si vous ajoutez un disque
- L'UUID reste le même toujours

### Voir les UUID

**Commande** :
```bash
sudo blkid
```

**Résultat exemple** :
```
/dev/sda1: UUID="A4B2-C3D4" TYPE="vfat" PARTUUID="..."
/dev/sda2: UUID="a1b2c3d4-e5f6-..." TYPE="ext4" PARTUUID="..."
/dev/sda3: UUID="12345678-abcd-..." TYPE="swap" PARTUUID="..."
```

### Utilisation dans /etc/fstab

Au lieu de `/dev/sda2`, on utilise l'UUID :
```
UUID=a1b2c3d4-e5f6-...  /      ext4  defaults  0  1
```

💡 **Avantage** : Votre système démarrera toujours, même si l'ordre des disques change.

## Monter et démonter manuellement

### Monter une partition

**Syntaxe** :
```bash
sudo mount /dev/sdX /point/de/montage
```

**Exemple** :
```bash
# Créer un point de montage
sudo mkdir /mnt/donnees

# Monter la partition
sudo mount /dev/sdb1 /mnt/donnees
```

### Démonter une partition

**Syntaxe** :
```bash
sudo umount /point/de/montage
```

**Exemple** :
```bash
sudo umount /mnt/donnees
```

⚠️ **Attention** : Vous ne pouvez pas démonter une partition si des fichiers sont en cours d'utilisation !

### Retirer une clé USB proprement

**Méthode graphique** : Clic droit sur l'icône → "Éjecter" ou "Démonter"

**Méthode terminal** :
```bash
sudo umount /media/votrenom/CleUSB
```

💡 **Pourquoi c'est important ?** : Cela garantit que toutes les données ont bien été écrites sur le périphérique avant de le retirer physiquement.

## Systèmes de fichiers

Chaque partition utilise un **système de fichiers** qui définit comment les données sont organisées.

### Les plus courants sous Linux

| Système | Usage | Caractéristiques |
|---------|-------|------------------|
| **ext4** | Linux (standard) | Fiable, journalisé, performant |
| **Btrfs** | Linux (moderne) | Snapshots, compression, plus avancé |
| **XFS** | Linux (hautes performances) | Pour gros fichiers et serveurs |
| **FAT32** | Clés USB, compatibilité | Limité à 4 Go par fichier |
| **exFAT** | Clés USB modernes | Sans limite de taille, compatible Windows/Mac |
| **NTFS** | Windows | Lecture/écriture possible sous Linux |
| **swap** | Mémoire d'échange | Pas de fichiers, extension RAM |

### Compatibilité Windows/Linux

**Pour partager des fichiers entre Windows et Linux** :
- **Recommandé** : exFAT (nécessite parfois des paquets supplémentaires)
- **Alternative** : NTFS (bien supporté sous Linux)
- **À éviter pour partage** : ext4 (Windows ne peut pas le lire nativement)

## Précautions et bonnes pratiques

### ✅ Bonnes pratiques

1. **Séparer /home** : Facilite les réinstallations sans perte de données
2. **Utiliser des UUID** : Plus fiable que /dev/sdX
3. **Toujours démonter proprement** : Évite la corruption de données
4. **Faire des sauvegardes** : Avant de manipuler les partitions
5. **Vérifier deux fois** : Avant de formater ou supprimer une partition

### ⚠️ Erreurs à éviter

1. **Ne jamais formater /dev/sda** : C'est le disque entier, pas une partition !
2. **Ne pas modifier les partitions en cours d'utilisation** : Démarrez sur un Live USB
3. **Ne pas supprimer la partition EFI** : Votre système ne démarrerait plus
4. **Attention aux permissions** : Les partitions NTFS peuvent avoir des restrictions

### 🔒 Sécurité

- Une partition montée en lecture seule (`ro`) ne peut pas être modifiée
- Les permissions Linux (chmod, chown) ne fonctionnent que sur ext4, Btrfs, XFS
- Sur FAT32/NTFS, tous les fichiers sont accessibles à tous

## Résumé

**Les points essentiels à retenir** :

1. **Partition** = division d'un disque dur en sections indépendantes
2. **Point de montage** = dossier où une partition est accessible dans l'arborescence
3. **Tout est intégré** = contrairement à Windows, pas de lettres de lecteurs séparées
4. **Nomenclature** : `/dev/sda1`, `/dev/sdb2`, `/dev/nvme0n1p1`
5. **Partitions courantes** :
   - `/` → système (30-50 Go minimum)
   - `/home` → données utilisateur (le reste)
   - `swap` → mémoire d'échange (4-8 Go)
   - `/boot/efi` → démarrage UEFI (512 Mo)
6. **Montage automatique** : défini dans `/etc/fstab`
7. **UUID** : identifiant unique et stable de chaque partition
8. **Démonter proprement** : toujours avant de retirer un périphérique

## Pour aller plus loin

Une fois que vous serez à l'aise avec ces concepts, vous pourrez :
- Créer vos propres schémas de partitionnement personnalisés
- Utiliser des systèmes de fichiers avancés comme Btrfs
- Configurer des montages automatiques personnalisés
- Chiffrer vos partitions pour plus de sécurité

Mais pour débuter, comprendre que Linux "accroche" les partitions dans son arborescence plutôt que de leur donner des lettres est déjà un grand pas !

⏭️ [Gestion des disques (Disques, GParted)](/08-gestion-du-systeme-de-fichiers/03-gestion-des-disques.md)
