🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 17.3 Clonage de disque (Clonezilla, dd)

## Introduction

Le clonage de disque est une technique de sauvegarde particulière qui consiste à créer une copie exacte, bit par bit, d'un disque entier ou d'une partition. C'est comme prendre une "photographie complète" de votre disque dur.

### Qu'est-ce que le clonage de disque ?

Le clonage crée une réplique parfaite de votre disque, incluant :
- Le système d'exploitation complet
- Tous les fichiers et dossiers
- Les partitions et leur structure
- Le secteur de démarrage (bootloader)
- L'espace vide et la structure du disque

C'est différent d'une simple copie de fichiers : le clone est identique jusque dans les moindres détails techniques.

### Différences avec les autres méthodes de sauvegarde

| Méthode | Ce qui est sauvegardé | Cas d'usage |
|---------|----------------------|-------------|
| **Timeshift** | Système Linux seulement | Revenir à un état système antérieur |
| **Déjà Dup / Backintime** | Fichiers personnels | Récupérer des documents perdus |
| **Clonage** | Disque entier, identique | Migrer vers un nouveau disque, backup complet |

### Pourquoi cloner un disque ?

Le clonage est utile dans ces situations :

**1. Migration vers un nouveau disque**
- Remplacer un disque dur par un SSD
- Passer à un disque de plus grande capacité
- Remplacer un disque défaillant

**2. Sauvegarde système complète**
- Avant une modification majeure du système
- Pour avoir une copie de secours bootable
- Protection contre la panne matérielle

**3. Duplication d'installations**
- Installer le même système sur plusieurs ordinateurs
- Créer des postes de travail identiques

**4. Tests et expérimentations**
- Tester des modifications sans risque
- Avoir un système de secours identique

### Clonage vs Image disque

**Clone :** Copie directe disque → disque (le résultat est immédiatement utilisable)

**Image :** Copie disque → fichier (nécessite une restauration pour être utilisable)

Les deux ont leurs avantages. Nous verrons comment faire les deux avec Clonezilla.

## Clonezilla : L'outil de clonage complet

Clonezilla est un logiciel libre et gratuit spécialisé dans le clonage et l'imagerie de disques. Il est puissant, fiable et utilisé par de nombreux professionnels.

### Caractéristiques de Clonezilla

- Interface en mode texte (pas de souris, navigation au clavier)
- Supporte de nombreux systèmes de fichiers
- Peut cloner des disques entiers ou des partitions individuelles
- Compression des images pour économiser de l'espace
- Très rapide et efficace
- Gratuit et open source

**Note pour débutants :** L'interface de Clonezilla peut sembler intimidante au premier abord, mais en suivant les étapes, c'est assez simple !

### Préparation de Clonezilla

#### Téléchargement

1. Allez sur le site officiel : https://clonezilla.org/downloads.php
2. Choisissez **Clonezilla Live** (version la plus simple)
3. Sélectionnez :
   - Type de CPU : **amd64** (pour les PC modernes 64 bits)
   - Type de fichier : **iso**
   - Repository : Choisissez un serveur proche (France)

#### Création de la clé USB bootable

Utilisez un outil comme **Etcher** ou **Rufus** pour créer une clé USB bootable avec l'ISO de Clonezilla.

**Avec Etcher (recommandé, simple) :**
1. Téléchargez et installez Etcher
2. Lancez Etcher
3. Sélectionnez l'ISO de Clonezilla
4. Sélectionnez votre clé USB (min. 1 Go)
5. Cliquez sur "Flash!"

**Important :** Toutes les données sur la clé USB seront effacées !

### Démarrer sur Clonezilla

1. Insérez la clé USB Clonezilla
2. Redémarrez votre ordinateur
3. Accédez au menu de boot (généralement F12, F2, ESC ou Suppr au démarrage)
4. Sélectionnez la clé USB
5. Attendez le chargement de Clonezilla

### Interface de Clonezilla

Au démarrage, vous verrez plusieurs écrans :

**1. Choix de la langue**
- Sélectionnez votre langue avec les flèches du clavier
- Validez avec Entrée

**2. Choix du clavier**
- Sélectionnez "Conserver le clavier" ou choisissez "fr" pour français
- Validez avec Entrée

**3. Mode Clonezilla**
- **Start Clonezilla** : Mode normal (recommandé)
- Autres options : Pour utilisateurs avancés

**4. Type de tâche**

Vous aurez deux choix principaux :

- **device-device** : Clonage direct disque → disque ou partition → partition
- **device-image** : Créer ou restaurer une image disque

### Cloner un disque entier (device-device)

C'est la méthode la plus simple pour copier un disque vers un autre.

#### Prérequis

- Un disque source (à cloner)
- Un disque destination (doit être de taille égale ou supérieure)
- **ATTENTION** : Toutes les données du disque destination seront effacées !

#### Étapes détaillées

**1. Mode de clonage**
- Sélectionnez **device-device**
- Choisissez **Beginner mode** (mode débutant)

**2. Type de clonage**
- **disk_to_local_disk** : Pour cloner un disque entier
- Validez avec Entrée

**3. Sélection du disque source**
- Clonezilla affiche la liste des disques détectés
- Identifiez votre disque source (par sa taille et son nom)
- Sélectionnez-le avec les flèches et validez

**Exemple :** `sda 500GB WDC WD5000...` = disque de 500 Go

**4. Sélection du disque destination**
- Sélectionnez le disque qui recevra le clone
- **VÉRIFIEZ BIEN** que vous avez choisi le bon disque !

**5. Options avancées (généralement, acceptez les valeurs par défaut)**
- Clonezilla propose plusieurs options
- Pour les débutants : appuyez simplement sur Entrée pour les valeurs par défaut
- Ces options incluent la vérification du système de fichiers, etc.

**6. Confirmation**
- Clonezilla vous demande de confirmer l'opération
- **Lisez attentivement** : toutes les données du disque destination seront perdues
- Tapez **y** puis Entrée pour confirmer
- Tapez à nouveau **y** pour la confirmation finale

**7. Processus de clonage**
- Le clonage démarre
- Une barre de progression s'affiche
- La durée dépend de la taille du disque (peut prendre 1-3 heures pour 500 Go)
- **Ne débranchez rien et ne redémarrez pas l'ordinateur pendant le processus !**

**8. Fin du clonage**
- Clonezilla affiche un message de réussite
- Appuyez sur Entrée
- Choisissez de redémarrer ou d'éteindre
- Retirez la clé USB Clonezilla

### Créer une image de disque (device-image)

Au lieu de cloner directement, vous pouvez créer un fichier image du disque.

#### Avantages de l'image disque

- Stockable sur un disque externe
- Peut être compressée (prend moins de place)
- Une image peut être restaurée plusieurs fois
- Peut être archivée pour conservation long terme

#### Prérequis

- Un emplacement de stockage (disque externe, partition, NAS)
- Espace suffisant pour l'image (dépend de la taille des données et de la compression)

#### Étapes de création d'image

**1. Préparez le stockage**
- Branchez votre disque externe où sera stockée l'image
- Assurez-vous qu'il a assez d'espace

**2. Mode de clonage**
- Sélectionnez **device-image**
- Choisissez **Beginner mode**

**3. Point de montage**
- Sélectionnez **local_dev** (périphérique local)
- Clonezilla scanne les périphériques disponibles
- Sélectionnez votre disque externe
- Choisissez le dossier où stocker l'image

**4. Type d'action**
- Sélectionnez **savedisk** (sauvegarder un disque entier)
- Ou **saveparts** (sauvegarder des partitions spécifiques)

**5. Nom de l'image**
- Donnez un nom descriptif à votre image
- Exemple : `linux-mint-2024-11-29` ou `sauvegarde-disque-principal`

**6. Sélection du disque source**
- Choisissez le disque à sauvegarder

**7. Options de compression**
Si proposé, vous pouvez choisir le niveau de compression :
- **-z1p** : Compression rapide (recommandé)
- **-z2p** : Compression normale
- **-z9p** : Compression maximale (plus lent)

**8. Vérification**
- Recommandé : activez la vérification de l'image après création
- Cela prend plus de temps mais garantit l'intégrité

**9. Lancement**
- Confirmez en tapant **y**
- Le processus démarre
- Attendez la fin (peut prendre plusieurs heures pour de gros disques)

**10. Fin de l'opération**
- L'image est créée dans le dossier choisi
- Notez son nom et emplacement
- Vous pouvez maintenant redémarrer

### Restaurer une image de disque

Pour restaurer une image précédemment créée :

**1. Démarrez sur Clonezilla**

**2. Mode de restauration**
- Choisissez **device-image**
- **Beginner mode**

**3. Point de montage**
- Sélectionnez **local_dev**
- Choisissez le disque contenant votre image
- Naviguez jusqu'au dossier contenant l'image

**4. Type d'action**
- Sélectionnez **restoredisk** (restaurer un disque)

**5. Sélection de l'image**
- Clonezilla liste les images disponibles
- Sélectionnez celle à restaurer

**6. Disque de destination**
- Choisissez le disque où restaurer l'image
- **ATTENTION** : Toutes les données seront écrasées !

**7. Confirmation et restauration**
- Confirmez l'opération
- Le processus démarre
- Attendez la fin

### Cloner une partition spécifique

Si vous ne voulez cloner qu'une partition :

**1. Mode partition**
- Choisissez **part_to_local_part** (device-device)
- Ou **saveparts** / **restoreparts** (device-image)

**2. Sélection**
- Sélectionnez la partition source (ex: sda1, sda2)
- Sélectionnez la partition destination

**3. Le reste est identique au clonage de disque**

## dd : L'outil de clonage en ligne de commande

dd (disk duplicator) est un outil Unix très puissant mais aussi très dangereux si mal utilisé. Il fonctionne entièrement en ligne de commande.

### Avertissements importants sur dd

⚠️ **DANGER** : dd est surnommé "disk destroyer" car une erreur peut détruire toutes vos données !

- **Pas de confirmation** : dd exécute immédiatement la commande
- **Pas d'annulation** : Une fois lancé, impossible de revenir en arrière
- **Destructif** : Écrase les données sans avertissement
- **Rapide** : Peut détruire un disque en quelques secondes

**Règle d'or** : Vérifiez TROIS FOIS votre commande avant d'appuyer sur Entrée !

### Quand utiliser dd ?

dd est utile pour :
- Créer des clés USB bootables
- Cloner des partitions en ligne de commande
- Sauvegardes rapides de petites partitions
- Scripts de sauvegarde automatisés
- Copier le secteur de boot (MBR)

### Identifier vos disques

Avant d'utiliser dd, identifiez vos disques :

```bash
lsblk
```

Résultat typique :
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 465.8G  0 disk
├─sda1   8:1    0   512M  0 part /boot/efi
├─sda2   8:2    0 456.3G  0 part /
└─sda3   8:3    0     9G  0 part [SWAP]
sdb      8:16   1  14.9G  0 disk
└─sdb1   8:17   1  14.9G  0 part /media/usb
```

**Lecture :**
- `sda` : Premier disque (généralement le disque principal)
- `sdb` : Deuxième disque (souvent une clé USB)
- `sda1, sda2` : Partitions du disque sda

**Important :** Notez bien les noms ! Confondre sda et sdb peut être catastrophique.

### Syntaxe de base de dd

```bash
dd if=/source of=/destination [options]
```

- `if=` : Input File (fichier/disque source)
- `of=` : Output File (fichier/disque destination)
- `bs=` : Block Size (taille des blocs de copie)
- `status=progress` : Affiche la progression

### Exemples pratiques avec dd

#### 1. Cloner une partition vers une autre

```bash
sudo dd if=/dev/sda1 of=/dev/sdb1 bs=4M status=progress
```

**Explication :**
- `if=/dev/sda1` : Source (partition sda1)
- `of=/dev/sdb1` : Destination (partition sdb1)
- `bs=4M` : Copie par blocs de 4 Mo (plus rapide)
- `status=progress` : Affiche la progression

**⚠️ ATTENTION :** Ceci écrase complètement sdb1 !

#### 2. Créer une image de partition

```bash
sudo dd if=/dev/sda1 of=~/sauvegarde_sda1.img bs=4M status=progress
```

Ceci crée un fichier image de la partition sda1.

#### 3. Restaurer une image de partition

```bash
sudo dd if=~/sauvegarde_sda1.img of=/dev/sda1 bs=4M status=progress
```

Restaure l'image sur la partition sda1.

#### 4. Cloner un disque entier

```bash
sudo dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```

Clone le disque sda complet vers sdb.

**⚠️ TRÈS DANGEREUX :** Le disque sdb sera complètement écrasé !

#### 5. Créer une clé USB bootable

```bash
sudo dd if=~/Téléchargements/linuxmint.iso of=/dev/sdb bs=4M status=progress && sync
```

**Explication :**
- Copie l'ISO sur la clé USB (sdb)
- `sync` à la fin vide les buffers (assure que tout est écrit)

**Note :** Utilisez `/dev/sdb` (le disque) et non `/dev/sdb1` (la partition) pour une clé bootable.

#### 6. Sauvegarder le MBR (Master Boot Record)

```bash
sudo dd if=/dev/sda of=~/mbr_backup.img bs=512 count=1
```

Sauvegarde uniquement les 512 premiers octets (le MBR) du disque sda.

#### 7. Restaurer le MBR

```bash
sudo dd if=~/mbr_backup.img of=/dev/sda bs=512 count=1
```

### Compresser une image avec dd

Pour économiser de l'espace, compressez l'image :

```bash
sudo dd if=/dev/sda1 bs=4M status=progress | gzip > sauvegarde_sda1.img.gz
```

Restaurer une image compressée :

```bash
gunzip -c sauvegarde_sda1.img.gz | sudo dd of=/dev/sda1 bs=4M status=progress
```

### Vérifier l'intégrité avec dd

Comparer deux disques pour vérifier qu'ils sont identiques :

```bash
sudo dd if=/dev/sda | md5sum
sudo dd if=/dev/sdb | md5sum
```

Si les deux md5sum sont identiques, les disques sont parfaitement identiques.

### Options utiles de dd

| Option | Description |
|--------|-------------|
| `bs=4M` | Taille de bloc (4M est un bon compromis vitesse/fiabilité) |
| `status=progress` | Affiche la progression |
| `conv=sync,noerror` | Continue même en cas d'erreur |
| `count=N` | Copie seulement N blocs |
| `skip=N` | Saute N blocs au début de la source |
| `seek=N` | Saute N blocs au début de la destination |

### Sécurité avec dd : Checklist

Avant chaque commande dd, vérifiez :

✅ **1. Ai-je identifié le bon disque source ?**
   - Relancez `lsblk` pour vérifier

✅ **2. Ai-je identifié le bon disque destination ?**
   - Vérifiez la taille, le nom, le point de montage

✅ **3. Ai-je démonté les partitions concernées ?**
   ```bash
   sudo umount /dev/sdb1
   ```

✅ **4. Ai-je une sauvegarde des données de destination ?**
   - Si c'est important, sauvegardez d'abord !

✅ **5. Ai-je assez d'espace disque ?**
   - Vérifiez avec `df -h`

✅ **6. Ai-je relu ma commande trois fois ?**
   - if= et of= sont-ils dans le bon ordre ?

### Alternatives plus sûres à dd

Si dd vous semble trop dangereux (et c'est légitime !), utilisez des alternatives :

**dcfldd** : Version améliorée de dd avec plus de sécurité
```bash
sudo apt install dcfldd
sudo dcfldd if=/dev/sda of=/dev/sdb
```

**ddrescue** : Pour disques avec secteurs défectueux
```bash
sudo apt install gddrescue
sudo ddrescue /dev/sda /dev/sdb rescue.log
```

## Comparaison Clonezilla vs dd

| Critère | Clonezilla | dd |
|---------|------------|-----|
| **Interface** | Texte guidé | Ligne de commande |
| **Facilité** | Moyen | Difficile |
| **Compression** | Oui | Avec pipe |
| **Sécurité** | Confirmations multiples | Aucune |
| **Vitesse** | Rapide | Très rapide |
| **Flexibilité** | Bonne | Totale |
| **Idéal pour** | Clonage disque complet | Scripts, petites tâches |
| **Débutants** | ✅ Oui (avec attention) | ❌ Non recommandé |

## Cas d'usage pratiques

### Cas 1 : Migrer vers un SSD

**Situation :** Vous voulez remplacer votre disque dur par un SSD.

**Solution Clonezilla :**
1. Installez le SSD en plus du disque actuel (temporairement)
2. Démarrez sur Clonezilla
3. Clonez le disque dur vers le SSD (device-device)
4. Éteignez, retirez le disque dur
5. Démarrez sur le SSD
6. Redimensionnez les partitions si le SSD est plus grand

**Avantage :** Système identique, aucune réinstallation !

### Cas 2 : Sauvegarde complète avant mise à jour majeure

**Situation :** Mise à jour majeure de Linux Mint à venir.

**Solution :**
1. Créez une image Clonezilla sur disque externe
2. Effectuez la mise à jour
3. Si problème : restaurez l'image
4. Si tout va bien : gardez l'image quelques semaines puis supprimez-la

### Cas 3 : Plusieurs PC identiques

**Situation :** Configuration de 5 ordinateurs identiques pour un bureau.

**Solution :**
1. Configurez complètement le premier PC
2. Créez une image Clonezilla
3. Clonez cette image sur les 4 autres PC
4. Personnalisez ensuite (nom d'hôte, etc.)

**Gain de temps :** Énorme !

### Cas 4 : Sauvegarde du secteur de boot

**Situation :** Vous allez manipuler les partitions.

**Solution dd :**
```bash
sudo dd if=/dev/sda of=~/mbr_backup.img bs=512 count=1
```

En cas de problème, restaurez :
```bash
sudo dd if=~/mbr_backup.img of=/dev/sda bs=512 count=1
```

## Bonnes pratiques de clonage

### Avant le clonage

1. **Sauvegardez vos données importantes** ailleurs (au cas où)
2. **Vérifiez l'état du disque source** avec `smartctl` ou GSmartControl
3. **Assurez-vous que la destination est assez grande**
4. **Notez vos UUIDs** si nécessaire (`sudo blkid`)
5. **Fermez tous les programmes** avant de démarrer sur Clonezilla

### Pendant le clonage

1. **Ne touchez à rien** pendant le processus
2. **Assurez une alimentation stable** (branchez votre laptop)
3. **Ne débranchez aucun câble**
4. **Soyez patient** : ça peut être long

### Après le clonage

1. **Testez le clone** avant de supprimer l'original
2. **Vérifiez que tout fonctionne** (démarrage, données, applications)
3. **Adaptez /etc/fstab** si vous avez changé de disque
4. **Mettez à jour GRUB** si nécessaire
5. **Documentez** ce que vous avez fait (date, taille, etc.)

### Gestion des clones et images

- **Datez vos images** : `backup-2024-11-29.img`
- **Stockez-les en sécurité** (disque externe déconnecté)
- **Vérifiez régulièrement** qu'elles sont lisibles
- **Supprimez les anciennes** après quelques mois
- **Compressez** si possible pour économiser l'espace

## Limitations et précautions

### Limitations du clonage

**1. Taille du disque**
- La destination doit être ≥ à la source
- Même si la source est peu remplie, toute sa taille compte

**2. UUIDs et identifiants**
- Deux clones ont les mêmes UUIDs (peut poser problème)
- Changez-les si nécessaire avec `tune2fs`

**3. Configuration matérielle**
- Un clone peut ne pas booter sur un PC très différent
- Drivers, UEFI vs BIOS, etc.

**4. Licences logicielles**
- Certains logiciels sont liés au matériel
- Vérifiez les licences avant de cloner

### Précautions essentielles

⚠️ **Ne jamais cloner pendant que le système est en cours d'utilisation**
- Démarrez toujours sur un Live USB (Clonezilla)
- Les fichiers en cours de modification seront corrompus

⚠️ **Vérifiez toujours les identifiants de disque**
- `/dev/sda` et `/dev/sdb` peuvent changer au redémarrage
- Utilisez `lsblk` à chaque fois

⚠️ **Testez vos sauvegardes**
- Une sauvegarde non testée n'est pas fiable
- Restaurez-la dans une VM ou sur un disque de test

⚠️ **Chiffrement et clonage**
- Le clonage de disques chiffrés nécessite des précautions spéciales
- Documentez-vous avant de cloner un système chiffré

## Dépannage

### Problèmes courants avec Clonezilla

**Clonezilla ne démarre pas**
- Vérifiez que le BIOS/UEFI est configuré pour booter sur USB
- Recréez la clé USB avec un autre outil
- Essayez un autre port USB

**Le disque destination n'apparaît pas**
- Vérifiez les branchements
- Le disque est peut-être défectueux
- Certains disques nécessitent des drivers spéciaux

**Erreur "No space left on device"**
- La destination est trop petite
- Nettoyez le disque source avant de cloner
- Utilisez une compression plus forte

**Le clone ne boot pas**
- UEFI vs BIOS : vérifiez le mode de boot
- Réparez GRUB après clonage
- Vérifiez le drapeau "boot" sur la bonne partition

### Problèmes courants avec dd

**dd est très lent**
- Augmentez le bs (ex: `bs=1M` ou `bs=4M`)
- Vérifiez les câbles USB (USB 2.0 vs 3.0)
- Le disque source est peut-être défaillant

**Erreur "Permission denied"**
- Utilisez `sudo` devant dd
- Vérifiez que les disques ne sont pas montés

**Erreur "No space left on device"**
- La destination est trop petite
- Vérifiez avec `lsblk` les tailles exactes

**Le clone créé avec dd ne boot pas**
- Vous avez peut-être copié une partition au lieu du disque entier
- Vérifiez que le secteur de boot est copié

## Outils complémentaires

### GParted

Pour redimensionner les partitions après clonage :
```bash
sudo apt install gparted
```

Utile si le nouveau disque est plus grand.

### fsarchiver

Alternative à Clonezilla pour sauvegarder des partitions :
```bash
sudo apt install fsarchiver
```

### partclone

Le moteur utilisé par Clonezilla, utilisable en ligne de commande :
```bash
sudo apt install partclone
```

## En résumé

Le clonage de disque est une technique puissante pour :
- Migrer vers un nouveau disque
- Créer des sauvegardes système complètes
- Dupliquer des installations

**Pour les débutants :**
- Utilisez **Clonezilla** pour cloner des disques
- Créez des **images de disque** sur disque externe
- Évitez **dd** tant que vous n'êtes pas très à l'aise

**Pour les utilisateurs avancés :**
- **dd** offre flexibilité et puissance
- Mais demande rigueur et précision
- Toujours vérifier trois fois avant Entrée

**Bonnes pratiques universelles :**
- Testez vos clones avant de supprimer l'original
- Sauvegardez vos données importantes avant de cloner
- Documentez vos clones (date, contenu, emplacement)
- Combinez avec Timeshift et sauvegardes de données pour protection complète

Le clonage est un outil complémentaire dans votre arsenal de sauvegarde. Utilisé correctement, il peut vous sauver la mise lors d'une migration ou d'une panne matérielle !

⏭️ [Stratégies de sauvegarde (règle 3-2-1)](/17-sauvegarde-et-restauration/04-strategies-de-sauvegarde.md)
