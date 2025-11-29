🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.4 Les systèmes de fichiers (ext4, Btrfs, NTFS, FAT32, exFAT)

## Introduction

### Qu'est-ce qu'un système de fichiers ?

Un **système de fichiers** (filesystem en anglais) est la façon dont les données sont organisées et stockées sur un disque dur, une clé USB ou tout autre support de stockage.

**Analogie** : Imaginez un système de fichiers comme le système d'organisation d'une bibliothèque :
- **Le disque dur** = le bâtiment de la bibliothèque
- **Le système de fichiers** = la méthode de rangement (par auteur, par genre, par date, etc.)
- **Les fichiers** = les livres

Différentes bibliothèques peuvent utiliser différentes méthodes d'organisation. De la même manière, différents systèmes d'exploitation utilisent différents systèmes de fichiers pour organiser les données.

### Pourquoi plusieurs systèmes de fichiers ?

Chaque système de fichiers a été conçu avec des objectifs différents :
- **Performance** : Certains sont plus rapides pour certaines tâches
- **Fiabilité** : Protection contre la corruption de données
- **Fonctionnalités** : Snapshots, compression, chiffrement, etc.
- **Compatibilité** : Être lu par différents systèmes d'exploitation
- **Taille maximale** : Limites de fichiers ou de partitions

### Vue d'ensemble rapide

| Système | Origine | Usage principal | Compatibilité |
|---------|---------|-----------------|---------------|
| **ext4** | Linux | Système Linux | Linux seulement |
| **Btrfs** | Linux | Linux moderne | Linux seulement |
| **XFS** | Linux | Hautes performances | Linux seulement |
| **NTFS** | Windows | Système Windows | Windows, Linux (R/W) |
| **FAT32** | Microsoft | Clés USB | Tous systèmes |
| **exFAT** | Microsoft | Clés USB modernes | Tous systèmes |

## Les systèmes de fichiers Linux

### ext4 - Le standard Linux

**ext4** = Fourth Extended Filesystem (quatrième système de fichiers étendu)

#### Caractéristiques

- **Créé en** : 2008
- **Stabilité** : Très mature et fiable
- **Performance** : Excellente pour un usage quotidien
- **Journalisation** : Oui (protection contre les coupures inattendues)
- **Taille maximale d'un fichier** : 16 To
- **Taille maximale de partition** : 1 Exaoctet (1 million de To)
- **Compatible avec** : Linux uniquement (lecture difficile sous Windows)

#### Avantages

- ✅ **Très stable** : Éprouvé depuis des années
- ✅ **Rapide** : Excellent équilibre performance/fiabilité
- ✅ **Bien supporté** : Fonctionne partout sous Linux
- ✅ **Récupération facile** : Outils de récupération nombreux
- ✅ **Peu gourmand** : Fonctionne même sur des machines modestes

#### Inconvénients

- ❌ **Pas de fonctionnalités avancées** : Pas de snapshots natifs, pas de compression
- ❌ **Fragmentation** : Peut se fragmenter avec le temps (très lentement)
- ❌ **Pas de détection d'erreurs silencieuses** : Contrairement à Btrfs/ZFS

#### Quand l'utiliser ?

- **Partition système (/)** : Recommandé pour Linux Mint
- **Partition /home** : Parfait pour vos données personnelles
- **Disques de données** : Usage général sous Linux
- **Serveurs** : Fiable et éprouvé

💡 **Verdict** : **C'est le choix par défaut et recommandé** pour la majorité des utilisateurs de Linux Mint.

---

### Btrfs - Le moderne

**Btrfs** = B-Tree Filesystem (prononcez "butter FS" ou "better FS")

#### Caractéristiques

- **Créé en** : 2009 (stable depuis 2014)
- **Stabilité** : Mature mais plus récent qu'ext4
- **Performance** : Très bonne, avec fonctionnalités avancées
- **Journalisation** : Oui, avancée (Copy-on-Write)
- **Taille maximale d'un fichier** : 16 Exaoctets
- **Taille maximale de partition** : 16 Exaoctets
- **Compatible avec** : Linux uniquement

#### Fonctionnalités avancées

- 🚀 **Snapshots** : Créer des instantanés du système (comme des points de restauration)
- 🚀 **Compression transparente** : Économise de l'espace automatiquement
- 🚀 **Détection d'erreurs** : Checksums pour détecter la corruption de données
- 🚀 **Auto-réparation** : Corrige les erreurs automatiquement (avec RAID)
- 🚀 **Sous-volumes** : Créer des "partitions virtuelles" sans repartitionner
- 🚀 **Snapshots incrémentaux** : Sauvegardes efficaces

#### Avantages

- ✅ **Fonctionnalités modernes** : Snapshots, compression, déduplication
- ✅ **Protection des données** : Détection et correction d'erreurs
- ✅ **Flexible** : Sous-volumes faciles à gérer
- ✅ **Économie d'espace** : Compression transparente
- ✅ **Sauvegardes intelligentes** : Snapshots quasi-instantanés

#### Inconvénients

- ❌ **Plus complexe** : Courbe d'apprentissage plus élevée
- ❌ **Peut être plus lent** : Avec certaines charges de travail (bases de données)
- ❌ **Consomme plus de ressources** : CPU pour compression/checksums
- ❌ **Moins mature** : Que ext4 (bien que stable)

#### Quand l'utiliser ?

- **Système avec snapshots** : Si vous voulez Timeshift avec snapshots Btrfs
- **Compression nécessaire** : Pour économiser de l'espace
- **Utilisateurs avancés** : Qui veulent exploiter les fonctionnalités
- **Machines récentes** : Avec CPU et RAM suffisants

💡 **Verdict** : **Excellent choix pour utilisateurs avancés** qui veulent des fonctionnalités modernes et la protection maximale des données.

---

### XFS - Les hautes performances

**XFS** = Extent File System

#### Caractéristiques

- **Créé en** : 1993 (par SGI, porté sur Linux en 2001)
- **Stabilité** : Très mature
- **Performance** : Excellent pour gros fichiers
- **Journalisation** : Oui
- **Taille maximale d'un fichier** : 8 Exaoctets
- **Taille maximale de partition** : 8 Exaoctets

#### Avantages

- ✅ **Très rapide** : Surtout pour les gros fichiers
- ✅ **Excellent en parallèle** : Multithreading performant
- ✅ **Allocation intelligente** : Réduit la fragmentation
- ✅ **Scalabilité** : Parfait pour très gros volumes

#### Inconvénients

- ❌ **Ne peut pas rétrécir** : Vous ne pouvez que l'agrandir, pas le réduire
- ❌ **Moins de choix de récupération** : Moins d'outils que ext4
- ❌ **Moins adapté aux petits fichiers** : Optimisé pour les gros volumes

#### Quand l'utiliser ?

- **Serveurs médias** : Gros fichiers vidéo
- **Serveurs de fichiers** : Stockage en réseau
- **Bases de données** : Performances élevées
- **Vidéo/Audio professionnel** : Gros projets

💡 **Verdict** : **Spécialisé pour serveurs et gros fichiers**. Pas nécessaire pour un usage bureautique classique.

---

## Les systèmes de fichiers Windows

### NTFS - Le système Windows moderne

**NTFS** = New Technology File System

#### Caractéristiques

- **Créé en** : 1993 (Windows NT)
- **Stabilité** : Très mature
- **Journalisation** : Oui
- **Taille maximale d'un fichier** : 16 Exaoctets (théorique)
- **Taille maximale de partition** : 256 To (pratique)
- **Compatible avec** : Windows (natif), Linux (lecture/écriture), macOS (lecture seule)

#### Avantages

- ✅ **Permissions avancées** : Contrôle d'accès granulaire (ACL)
- ✅ **Compression** : Compression de fichiers native
- ✅ **Chiffrement** : EFS (Encrypting File System)
- ✅ **Journalisation** : Protection contre les crashs
- ✅ **Pas de limite de 4 Go** : Contrairement à FAT32

#### Inconvénients sous Linux

- ❌ **Support Linux pas optimal** : Peut avoir des problèmes de performances
- ❌ **Permissions complexes** : Incompatibilité entre ACL Windows et permissions Linux
- ❌ **Hibernation Windows** : Le disque peut être verrouillé si Windows est en veille prolongée

#### Quand l'utiliser ?

- **Partition Windows** : Pour votre installation Windows
- **Disque partagé Windows/Linux** : Si vous avez un dual-boot
- **Disque externe** : Pour échanger avec des PC Windows

💡 **Astuce Linux** : Linux peut lire et écrire sur NTFS grâce au pilote `ntfs-3g`, installé par défaut sur Mint.

⚠️ **Problème dual-boot** : Si Windows est en hibernation (Fast Startup), Linux ne pourra pas écrire sur les partitions NTFS. Désactivez le démarrage rapide dans Windows.

---

### FAT32 - Le vieux compatible

**FAT32** = File Allocation Table 32-bit

#### Caractéristiques

- **Créé en** : 1996 (Windows 95 OSR2)
- **Stabilité** : Très simple et fiable
- **Journalisation** : Non
- **Taille maximale d'un fichier** : **4 Go** (limitation majeure)
- **Taille maximale de partition** : 2 To (sous Windows), 8 To (théorique)
- **Compatible avec** : Tous les systèmes (Windows, Linux, macOS, consoles, TV, etc.)

#### Avantages

- ✅ **Compatibilité universelle** : Fonctionne partout
- ✅ **Simple** : Peu de ressources nécessaires
- ✅ **Fiable** : Peu de risque de corruption
- ✅ **Récupération facile** : Nombreux outils disponibles

#### Inconvénients

❌ **Limite de 4 Go par fichier** : IMPOSSIBLE de copier un fichier > 4 Go
❌ **Pas de permissions** : Tout le monde peut tout lire/écrire
❌ **Pas de journalisation** : Sensible aux coupures brutales
❌ **Fragmentation** : Se fragmente rapidement

#### Quand l'utiliser ?

- **Vieilles clés USB** : Compatibilité maximale
- **Consoles de jeux** : PS4, Xbox (parfois)
- **Télévisions** : Certaines TV ne lisent que FAT32
- **Partage multi-OS** : Si vous n'avez jamais de fichiers > 4 Go

💡 **Limite des 4 Go** : Vous **ne pourrez pas** copier une ISO de Linux (souvent 2-3 Go, ça passe) mais **pas** un film Blu-ray (souvent > 4 Go).

---

### exFAT - Le FAT32 moderne

**exFAT** = Extended File Allocation Table

#### Caractéristiques

- **Créé en** : 2006 (Windows Vista)
- **Stabilité** : Mature
- **Journalisation** : Non
- **Taille maximale d'un fichier** : 16 Exaoctets (pas de limite pratique)
- **Taille maximale de partition** : 128 Pétaoctets
- **Compatible avec** : Windows, Linux (depuis kernel 5.4), macOS, consoles modernes

#### Avantages

- ✅ **Pas de limite de 4 Go** : Vous pouvez copier des gros fichiers
- ✅ **Compatibilité excellente** : Windows, Linux, Mac, consoles
- ✅ **Optimisé pour flash** : Conçu pour clés USB et cartes SD
- ✅ **Simple** : Comme FAT32 mais sans ses limitations

#### Inconvénients

- ❌ **Pas de permissions** : Pas de contrôle d'accès
- ❌ **Pas de journalisation** : Sensible aux débranchements brutaux
- ❌ **Ancien Linux** : Nécessite kernel récent (Mint 20+ OK)

#### Quand l'utiliser ?

- **Clés USB modernes** : Pour échanger entre Windows/Linux/Mac
- **Cartes SD** : Appareil photo, dashcam
- **Disques externes** : Partage de fichiers volumineux
- **Consoles modernes** : PS5, Xbox Series

💡 **Verdict** : **Le meilleur choix pour les périphériques amovibles** si vous avez des fichiers > 4 Go.

---

## Comparaison détaillée

### Tableau récapitulatif

| Caractéristique | ext4 | Btrfs | XFS | NTFS | FAT32 | exFAT |
|-----------------|------|-------|-----|------|-------|-------|
| **Max fichier** | 16 To | 16 Eo | 8 Eo | 16 Eo | **4 Go** | 16 Eo |
| **Max partition** | 1 Eo | 16 Eo | 8 Eo | 256 To | 2 To | 128 Po |
| **Journalisation** | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Snapshots** | ❌ | ✅ | ❌ | ✅* | ❌ | ❌ |
| **Compression** | ❌ | ✅ | ❌ | ✅ | ❌ | ❌ |
| **Permissions** | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Windows** | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| **Linux** | ✅ | ✅ | ✅ | R/W | R/W | R/W |
| **macOS** | ❌ | ❌ | ❌ | RO | R/W | R/W |
| **Performances** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ |

**Légende** : Eo = Exaoctet, Po = Pétaoctet, RO = Lecture seule, R/W = Lecture/Écriture, * = Via VSS (Volume Shadow Copy)

### Performance comparée

**Vitesse d'écriture** (ordre général) :
1. XFS (gros fichiers)
2. ext4 (équilibré)
3. Btrfs (avec compression désactivée)
4. exFAT
5. NTFS (sous Linux)
6. FAT32

**Fiabilité** (protection des données) :
1. Btrfs (checksums + snapshots)
2. ext4 (journalisation éprouvée)
3. XFS (journalisation avancée)
4. NTFS (journalisation)
5. exFAT (pas de journalisation)
6. FAT32 (pas de journalisation)

## Guide de choix du système de fichiers

### Pour votre partition système Linux (/)

**Recommandé : ext4**
```
Pourquoi ?
✅ Stable et éprouvé
✅ Excellent support
✅ Récupération facile en cas de problème
✅ Performances fiables
```

**Alternative : Btrfs** (utilisateurs avancés)
```
Si vous voulez :
✅ Snapshots système (avec Timeshift)
✅ Compression transparente
✅ Protection maximale des données
```

### Pour votre partition /home (données personnelles)

**Recommandé : ext4**
```
Pour la majorité des utilisateurs
✅ Fiable
✅ Rapide
✅ Pas de complications
```

**Alternative : Btrfs**
```
Si vous voulez :
✅ Snapshots de vos données
✅ Compression pour économiser de l'espace
✅ Détection d'erreurs
```

### Pour une clé USB

**< 32 Go et fichiers < 4 Go** : **FAT32**
```
✅ Compatibilité maximale
✅ Fonctionne sur toutes les TV, consoles, etc.
```

**> 32 Go ou fichiers > 4 Go** : **exFAT**
```
✅ Pas de limite de taille
✅ Compatible Windows/Linux/Mac/Consoles
✅ Optimisé pour USB
```

**Usage Linux uniquement** : **ext4**
```
✅ Permissions Linux
✅ Performances optimales
✅ Fiabilité maximale
```

### Pour un disque externe partagé Windows/Linux

**Fichiers > 4 Go** : **NTFS** ou **exFAT**
```
NTFS :
✅ Permissions (si besoin)
✅ Compression
⚠️ Désactiver Fast Startup Windows

exFAT :
✅ Plus simple
✅ Pas de problème d'hibernation
❌ Pas de permissions
```

**Fichiers < 4 Go** : **FAT32**
```
✅ Compatibilité maximale
✅ Aucun problème
```

### Pour un serveur média/NAS

**Recommandé : XFS** ou **Btrfs**
```
XFS :
✅ Excellent pour gros fichiers vidéo
✅ Performances élevées

Btrfs :
✅ Snapshots
✅ Compression
✅ Protection des données
```

## Support sous Linux Mint

### Systèmes de fichiers supportés nativement

Linux Mint supporte **en lecture et écriture** :
- ✅ **ext2, ext3, ext4** : Natif (système de fichiers Linux)
- ✅ **Btrfs** : Natif
- ✅ **XFS** : Natif
- ✅ **FAT12, FAT16, FAT32** : Natif
- ✅ **exFAT** : Natif (depuis Mint 20 / kernel 5.4+)
- ✅ **NTFS** : Via ntfs-3g (installé par défaut)
- ✅ **swap** : Natif

### Installer le support pour systèmes supplémentaires

**Pour exFAT** (si ancien système) :
```bash
sudo apt install exfat-fuse exfat-utils
```

**Pour Btrfs** (outils supplémentaires) :
```bash
sudo apt install btrfs-progs
```

**Pour XFS** (outils supplémentaires) :
```bash
sudo apt install xfsprogs
```

**Pour F2FS** (système pour SSD/flash) :
```bash
sudo apt install f2fs-tools
```

## Formater une partition dans un système de fichiers

### Avec l'outil graphique Disques

1. Ouvrez **Disques**
2. Sélectionnez la partition
3. Cliquez sur **⚙ Options** → **Formater la partition...**
4. Choisissez :
   - **Type** : Le système de fichiers
   - **Nom** : Étiquette de la partition
   - **Effacement** : Rapide (recommandé)
5. Cliquez sur **Formater**

### Avec GParted

1. Ouvrez **GParted**
2. Démontez la partition
3. Clic droit → **Formater vers** → Choisissez le système
4. Appliquez

### En ligne de commande

⚠️ **ATTENTION** : Vérifiez bien la partition avant de formater !

**ext4** :
```bash
sudo mkfs.ext4 -L "NomPartition" /dev/sdX1
```

**Btrfs** :
```bash
sudo mkfs.btrfs -L "NomPartition" /dev/sdX1
```

**XFS** :
```bash
sudo mkfs.xfs -L "NomPartition" /dev/sdX1
```

**NTFS** :
```bash
sudo mkfs.ntfs -L "NomPartition" /dev/sdX1
```

**FAT32** :
```bash
sudo mkfs.vfat -n "NOMPARTITI" /dev/sdX1
```
*(Note : FAT32 limite les noms à 11 caractères majuscules)*

**exFAT** :
```bash
sudo mkfs.exfat -n "NomPartition" /dev/sdX1
```

## Conversion entre systèmes de fichiers

### Règle générale

⚠️ **Il n'existe PAS de conversion directe** entre la plupart des systèmes de fichiers.

**Processus** :
1. **Sauvegardez** toutes les données
2. **Formatez** dans le nouveau système de fichiers
3. **Restaurez** les données

### Cas particulier : ext3 → ext4

**Seule exception** : On peut convertir ext3 en ext4 sans perdre de données :

```bash
# Convertir ext3 en ext4 (sans perte)
sudo tune2fs -O extents,uninit_bg,dir_index /dev/sdX1
sudo e2fsck -fD /dev/sdX1
```

⚠️ **Attention** : Ne faites ceci que si vous savez ce que vous faites et après une sauvegarde !

### Migration sécurisée

**Méthode recommandée** :
1. Créez une nouvelle partition avec le nouveau système de fichiers
2. Copiez les données avec `rsync` :
```bash
sudo rsync -av /ancien/point/montage/ /nouveau/point/montage/
```
3. Vérifiez que tout est bien copié
4. Supprimez l'ancienne partition

## Caractéristiques avancées

### Journalisation (Journaling)

**Qu'est-ce que c'est ?**
Un journal qui enregistre les modifications avant qu'elles soient appliquées.

**Avantage** :
En cas de coupure de courant, le système peut "rejouer" le journal pour éviter la corruption.

**Systèmes avec journalisation** :
- ✅ ext4, Btrfs, XFS, NTFS
- ❌ FAT32, exFAT

### Copy-on-Write (CoW)

**Principe** : Quand on modifie un fichier, au lieu de le modifier directement, le système crée une nouvelle version.

**Avantages** :
- Protection contre la corruption
- Snapshots instantanés
- Pas de fragmentation

**Systèmes CoW** :
- ✅ Btrfs
- ❌ ext4, XFS (modification sur place)

### Checksums (sommes de contrôle)

**Principe** : Calcul d'une empreinte pour chaque bloc de données.

**Avantage** :
Détection automatique de la corruption silencieuse (bit-rot).

**Systèmes avec checksums** :
- ✅ Btrfs (sur données et métadonnées)
- ❌ ext4, XFS

### Compression transparente

**Principe** : Les fichiers sont automatiquement compressés à l'écriture et décompressés à la lecture.

**Avantage** :
Économie d'espace disque sans rien faire.

**Systèmes avec compression** :
- ✅ Btrfs (zlib, lzo, zstd)
- ✅ NTFS (compression Windows)
- ❌ ext4, XFS

## FAQ - Questions fréquentes

### Puis-je accéder à mes fichiers Windows depuis Linux ?

**Oui !** Linux peut lire et écrire sur les partitions NTFS sans problème.

⚠️ **Sauf si** Windows est en hibernation (Fast Startup) - dans ce cas, désactivez cette option dans Windows.

### Quel système de fichiers pour un dual-boot ?

**Pour Linux** : ext4 ou Btrfs
**Pour Windows** : NTFS
**Pour partager** : NTFS ou exFAT

💡 **Astuce** : Créez une partition NTFS ou exFAT séparée pour partager des fichiers entre Windows et Linux.

### FAT32 ou exFAT pour ma clé USB ?

**FAT32** si :
- Votre clé fait moins de 32 Go
- Vous n'avez jamais de fichiers > 4 Go
- Vous voulez la compatibilité maximale (vieilles TV, etc.)

**exFAT** si :
- Votre clé fait plus de 32 Go
- Vous copiez des films, ISOs, images disque > 4 Go
- Vous avez un matériel récent

### Btrfs est-il stable ?

**Oui**, Btrfs est stable depuis 2014 pour un usage normal.

✅ **Stable** :
- Partition système
- Partition de données
- Snapshots
- Compression

⚠️ **Moins mature** :
- RAID 5/6 (encore considéré instable)
- Certaines fonctionnalités très avancées

### Puis-je utiliser Btrfs pour tout ?

**Oui**, mais :
- Certaines applications de bases de données préfèrent ext4 ou XFS
- Nécessite un peu plus de ressources
- Courbe d'apprentissage pour exploiter les fonctionnalités

**Recommandation** : Commencez par ext4, passez à Btrfs quand vous êtes à l'aise avec Linux.

### Comment voir quel système de fichiers j'utilise ?

**Commande** :
```bash
df -T
```

**Résultat** :
```
Sys. fichiers   Type     Taille Utilisé Dispo Uti% Monté sur
/dev/sda2       ext4       50G     15G   33G  31% /
/dev/sda4       ext4      400G    120G  260G  32% /home
```

### Puis-je changer de système de fichiers sans formater ?

**Non**, sauf pour ext3 → ext4.

Vous **devez** :
1. Sauvegarder vos données
2. Formater dans le nouveau système
3. Restaurer vos données

## Résumé

### Choix recommandés pour débutants

**Système Linux (/) et /home** → **ext4**
- Fiable, rapide, éprouvé
- Aucune complication

**Clé USB < 32 Go** → **FAT32**
- Compatibilité maximale

**Clé USB > 32 Go ou gros fichiers** → **exFAT**
- Pas de limite de 4 Go
- Compatible partout

**Partition partagée Windows/Linux** → **NTFS** ou **exFAT**
- Accessible des deux côtés

### Points clés à retenir

1. **ext4** : Le standard Linux, fiable et rapide
2. **Btrfs** : Moderne avec fonctionnalités avancées (snapshots, compression)
3. **NTFS** : Le système Windows, utilisable sous Linux
4. **FAT32** : Universel mais limité à 4 Go/fichier
5. **exFAT** : FAT32 moderne sans limitation
6. **Pas de conversion** : Il faut sauvegarder, formater, restaurer

### Pour aller plus loin

Une fois à l'aise, vous pourrez :
- Expérimenter avec Btrfs et ses snapshots
- Utiliser la compression Btrfs pour économiser l'espace
- Configurer des systèmes de fichiers chiffrés
- Explorer XFS pour des cas d'usage spécifiques

Mais pour débuter, **ext4 pour Linux et exFAT pour les clés USB** sont des choix parfaits qui vous serviront sans problème !

⏭️ [Montage/démontage de périphériques](/08-gestion-du-systeme-de-fichiers/05-montage-demontage-de-peripheriques.md)
