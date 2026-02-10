🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 2.6 Partitionnement manuel avancé

## Introduction

Le **partitionnement manuel** vous donne un contrôle total sur la façon dont Linux Mint sera installé sur votre disque. C'est une méthode plus technique, mais elle permet d'optimiser votre installation selon vos besoins spécifiques.

### Qu'est-ce que le partitionnement manuel ?

Au lieu de laisser l'installateur créer automatiquement les partitions, vous décidez :
- Combien de partitions créer
- Quelle taille donner à chaque partition
- Quel système de fichiers utiliser
- Où placer chaque élément du système

> 💡 **Analogie** : L'installation automatique est comme acheter un appartement déjà agencé. Le partitionnement manuel, c'est comme construire votre maison en choisissant la taille de chaque pièce.

### Installation automatique vs manuelle

| Critère | Automatique | Manuelle |
|---------|-------------|----------|
| **Difficulté** | ⭐ Très facile | ⭐⭐⭐⭐ Avancé |
| **Temps** | 5 minutes | 15-30 minutes |
| **Contrôle** | Limité | Total |
| **Optimisation** | Standard | Personnalisée |
| **Risques** | Faibles | Moyens si erreur |
| **Recommandé pour** | Débutants | Utilisateurs expérimentés |

---

## Pourquoi utiliser le partitionnement manuel ?

### Cas d'usage du partitionnement manuel

**Vous devriez utiliser le partitionnement manuel si :**

- ✅ **Séparation /home** : Vous voulez séparer vos données personnelles du système
- ✅ **Multi-boot** : Vous installez plusieurs distributions Linux
- ✅ **Partition existante** : Vous voulez utiliser une partition existante
- ✅ **Configuration serveur** : Partitions spécifiques (/var, /tmp, etc.)
- ✅ **Optimisation SSD** : Alignement et optimisations spécifiques
- ✅ **Partage de données** : Partition commune entre systèmes
- ✅ **Contrôle total** : Vous savez exactement ce que vous faites
- ✅ **Chiffrement sélectif** : Chiffrer uniquement certaines partitions

**Utilisez l'installation automatique si :**

- ❌ **Première installation Linux** : Vous n'êtes pas familier avec les partitions
- ❌ **Installation simple** : Vous voulez juste que ça marche
- ❌ **Pas de besoins spécifiques** : La configuration standard suffit
- ❌ **Vous hésitez** : Le doute = automatique

---

## Concepts de base à comprendre

### Qu'est-ce qu'une partition ?

Une **partition** est une section distincte d'un disque dur. C'est comme diviser un gros disque en plusieurs disques virtuels indépendants.

```
┌────────────────────────────────────┐
│         Disque dur 500 GB          │
├────────────┬─────────────┬─────────┤
│ Partition 1│ Partition 2 │Partition│
│   100 GB   │   300 GB    │ 100 GB  │
│    EFI     │   Linux /   │  /home  │
└────────────┴─────────────┴─────────┘
```

### Tables de partitions

**MBR (Master Boot Record) - Ancien**
- Maximum 4 partitions primaires
- Ou 3 primaires + 1 étendue (avec plusieurs logiques)
- Disques jusqu'à 2 To
- Compatible PC anciens (BIOS)

**GPT (GUID Partition Table) - Moderne**
- Jusqu'à 128 partitions
- Disques au-delà de 2 To
- Requis pour UEFI
- Recommandé pour PC récents

> 💡 **Comment savoir ?** PC acheté après 2012 = probablement UEFI/GPT. Avant 2012 = probablement BIOS/MBR.

### Types de partitions

**Partition primaire :**
- Partition principale
- Maximum 4 en MBR
- Peut démarrer un OS

**Partition étendue (MBR seulement) :**
- Conteneur pour partitions logiques
- Permet de dépasser la limite de 4 partitions

**Partition logique (MBR seulement) :**
- À l'intérieur d'une partition étendue
- Nombre quasi illimité

> 💡 En GPT, toutes les partitions sont "primaires" (pas de distinction étendue/logique).

### Systèmes de fichiers

Un **système de fichiers** détermine comment les données sont organisées sur la partition.

**ext4 (Fourth Extended Filesystem)**
- ✅ Système par défaut pour Linux
- ✅ Fiable et performant
- ✅ Journalisation (protection contre les crashes)
- ✅ Recommandé pour Linux Mint

**ext3**
- Ancienne version d'ext4
- Moins performant
- Toujours compatible

**Btrfs (B-tree Filesystem)**
- Système moderne avec fonctionnalités avancées
- Snapshots, compression, déduplication
- Plus expérimental (pour utilisateurs avancés)

**XFS**
- Optimisé pour gros fichiers
- Performant pour serveurs
- Moins utilisé sur desktop

**FAT32**
- Compatible Windows/Linux/Mac
- Limite : fichiers de 4 GB max
- Bon pour partitions de partage

**NTFS**
- Système Windows
- Linux peut lire/écrire (via ntfs-3g)
- Pas recommandé pour partition Linux

**swap**
- Pas vraiment un système de fichiers
- Espace de swap (mémoire virtuelle)
- Utilisé quand RAM pleine

### Points de montage

Un **point de montage** est l'emplacement où une partition est accessible dans l'arborescence Linux.

```
┌─────────────────────────────────────┐
│ Disque /dev/sda                     │
├─────────────────────────────────────┤
│ /dev/sda1 → monté sur /boot/efi     │
│ /dev/sda2 → monté sur /             │
│ /dev/sda3 → swap                    │
│ /dev/sda4 → monté sur /home         │
└─────────────────────────────────────┘
```

**Points de montage essentiels :**

**/ (racine)** - OBLIGATOIRE
- Racine du système
- Contient tout le système d'exploitation
- Minimum 15 Go, recommandé 30-50 Go

**/home** - Optionnel mais recommandé
- Vos fichiers personnels
- Documents, téléchargements, paramètres
- Peut être sur partition séparée
- Taille : autant que possible

**/boot** - Optionnel
- Fichiers de démarrage (kernel)
- Utile si / est chiffré ou sur LVM
- 500 Mo à 1 Go suffisent

**/boot/efi** - OBLIGATOIRE (UEFI)
- Partition EFI système
- Requis pour UEFI
- 512 Mo (déjà créée souvent)
- Format FAT32

**swap** - Recommandé
- Mémoire virtuelle
- Fichier d'hibernation
- Taille = RAM (ou 4-8 Go)

**Autres (avancé) :**
- **/var** : Logs, cache (serveurs)
- **/tmp** : Fichiers temporaires
- **/usr** : Programmes (rarement séparé)

---

## Schémas de partitionnement recommandés

### Schéma 1 : Simple (débutants en partitionnement manuel)

**Configuration minimale :**
```
┌────────────────────────────────────┐
│ /boot/efi    512 MB    FAT32       │  (UEFI seulement)
│ /            30 GB     ext4        │  (Système)
│ swap         4-8 GB    swap        │  (Mémoire virtuelle)
│ /home        Reste     ext4        │  (Données)
└────────────────────────────────────┘
```

**Avantages :**
- ✅ Séparation système/données
- ✅ Réinstallation facile (garde /home)
- ✅ Simple à comprendre

**Pour qui :**
- Premier partitionnement manuel
- Usage desktop classique
- Disques de 128 GB et plus

### Schéma 2 : Très simple (si petit disque)

**Configuration ultra-minimale :**
```
┌────────────────────────────────────┐
│ /boot/efi    512 MB    FAT32       │  (UEFI seulement)
│ /            Reste     ext4        │  (Tout en une partition)
└────────────────────────────────────┘
```

**Avantages :**
- ✅ Plus simple possible
- ✅ Pas de gestion d'espace entre partitions
- ✅ Bon pour SSD petits (< 128 GB)

**Inconvénients :**
- ❌ Pas de séparation /home
- ❌ Réinstallation = perte des données

**Pour qui :**
- Très petits disques (< 64 GB)
- Test ou installation temporaire

### Schéma 3 : Avancé avec /boot

**Configuration complète :**
```
┌────────────────────────────────────┐
│ /boot/efi    512 MB    FAT32       │  (UEFI)
│ /boot        1 GB      ext4        │  (Kernel)
│ /            30 GB     ext4        │  (Système)
│ swap         8 GB      swap        │  (RAM virtuelle)
│ /home        Reste     ext4        │  (Données)
└────────────────────────────────────┘
```

**Avantages :**
- ✅ /boot séparé (utile pour chiffrement)
- ✅ Organisation optimale
- ✅ Facilite multi-boot

**Pour qui :**
- Utilisateurs avancés
- Chiffrement du système
- Configuration serveur

### Schéma 4 : Dual-boot Windows + Linux

**Configuration mixte :**
```
┌────────────────────────────────────┐
│ EFI          512 MB    FAT32       │  (Partagée)
│ Windows      250 GB    NTFS        │  (Windows C:)
│ /            30 GB     ext4        │  (Linux /)
│ swap         8 GB      swap        │  (Linux swap)
│ /home        100 GB    ext4        │  (Linux données)
│ Données      Reste     NTFS        │  (Partagée Win/Linux)
└────────────────────────────────────┘
```

**Avantages :**
- ✅ Partition commune pour fichiers
- ✅ Accès depuis Windows et Linux

**Pour qui :**
- Dual-boot Windows/Linux
- Partage de gros fichiers (films, etc.)

---

## Exemples selon la taille du disque

### Disque 128 GB (SSD petit)

```
/boot/efi    512 MB
/            40 GB
swap         4 GB
/home        83 GB
────────────────────
Total:       ~128 GB
```

### Disque 256 GB (SSD standard)

```
/boot/efi    512 MB
/            50 GB
swap         8 GB
/home        197 GB
────────────────────
Total:       ~256 GB
```

### Disque 500 GB (HDD classique)

```
/boot/efi    512 MB
/            50 GB
swap         8 GB
/home        441 GB
────────────────────
Total:       ~500 GB
```

### Disque 1 TB (Grand disque)

```
/boot/efi    512 MB
/            80 GB
swap         16 GB
/home        923 GB
────────────────────
Total:       ~1 TB
```

---

## Guide pas-à-pas : Partitionnement manuel

### Prérequis

- ✅ Clé USB bootable Linux Mint
- ✅ Démarré en mode Live
- ✅ Sauvegarde de vos données (CRITIQUE)
- ✅ Connaissance de base des partitions
- ✅ Schéma de partitionnement décidé

### Étape 1 : Lancer l'installateur

1. Double-cliquez sur **"Install Linux Mint"** sur le bureau
2. Choisissez la langue : **Français**
3. Choisissez le clavier : **Français**
4. Cochez **"Installer les codecs multimédia"** (recommandé)

### Étape 2 : Choisir "Autre chose"

À l'écran **"Type d'installation"** :

```
┌────────────────────────────────────┐
│ ○ Installer à côté de...           │
│ ○ Effacer le disque et installer   │
│ ● Autre chose                      │  ← SÉLECTIONNEZ CECI
│                                    │
│   Créer, redimensionner ou         │
│   supprimer des partitions         │
└────────────────────────────────────┘
```

Cliquez sur **"Continuer"**.

### Étape 3 : Interface de partitionnement

Vous voyez maintenant l'**outil de partitionnement manuel**.

#### Comprendre l'interface

**Tableau des partitions :**
```
Périphérique  Type   Point de montage  Format  Taille  Utilisé
/dev/sda1     efi    /boot/efi                512 MB   50 MB
/dev/sda2     ntfs                           250 GB  180 GB
/dev/sda3     (espace libre)                 249 GB       -
```

**Éléments de l'interface :**
- **Périphérique** : Nom technique de la partition (/dev/sda1, etc.)
- **Type** : Système de fichiers (ext4, ntfs, swap, etc.)
- **Point de montage** : Où sera montée la partition (/, /home, etc.)
- **Format** : Coché = partition sera formatée
- **Taille** : Capacité de la partition
- **Utilisé** : Espace déjà occupé

**Boutons :**
- **[+]** : Créer une nouvelle partition
- **[-]** : Supprimer la partition sélectionnée
- **[Change]** : Modifier une partition existante
- **[Revert]** : Annuler les changements

#### Identifier votre disque

**Exemple de nommage :**
- **/dev/sda** : Premier disque (SATA/SSD)
- **/dev/sdb** : Deuxième disque
- **/dev/nvme0n1** : SSD NVMe

**Partitions :**
- **/dev/sda1** : Première partition du disque sda
- **/dev/sda2** : Deuxième partition
- Etc.

### Étape 4 : Créer l'espace libre

**Si vous avez Windows et voulez un dual-boot :**

1. Sélectionnez la **partition Windows** (généralement la plus grande NTFS)
2. Cliquez sur **"Change"**
3. Réduisez sa taille pour libérer de l'espace
4. Cliquez sur **"OK"**
5. Un espace **"espace libre"** apparaît

**Si vous faites une installation complète :**

1. Sélectionnez **chaque partition** existante
2. Cliquez sur **"-"** (Supprimer)
3. Confirmez la suppression
4. Tout le disque devient **"espace libre"**

> ⚠️ **ATTENTION** : Supprimer des partitions efface définitivement les données. Assurez-vous d'avoir sauvegardé !

### Étape 5 : Créer la partition EFI (si UEFI)

**Si vous avez un PC UEFI et aucune partition EFI :**

1. Sélectionnez **"espace libre"**
2. Cliquez sur **"+"**
3. Configurez :
   - **Taille** : `512` MB
   - **Type de la nouvelle partition** : Primaire
   - **Emplacement** : Début de cet espace
   - **Utiliser comme** : Système de fichiers FAT32
   - **Point de montage** : `/boot/efi`
4. Cliquez sur **"OK"**

**Si une partition EFI existe déjà :**
- Ne la supprimez PAS
- Sélectionnez-la et cliquez **"Change"**
- **Point de montage** : `/boot/efi`
- **Format** : NE PAS cocher (ne pas formater)
- Cliquez **"OK"**

> 💡 La partition EFI peut être partagée entre Windows et Linux.

### Étape 6 : Créer la partition racine (/)

1. Sélectionnez **"espace libre"**
2. Cliquez sur **"+"**
3. Configurez :
   - **Taille** : `30000` à `50000` MB (30-50 GB)
   - **Type** : Primaire (ou logique si MBR avec partition étendue)
   - **Emplacement** : Début de cet espace
   - **Utiliser comme** : Système de fichiers ext4 avec journalisation
   - **Point de montage** : `/`
4. Cliquez sur **"OK"**

> 💡 **Taille recommandée :**
> - Minimum : 20 GB
> - Recommandé : 30-50 GB
> - Large : 80-100 GB (si vous installez beaucoup de logiciels)

### Étape 7 : Créer la partition swap

1. Sélectionnez **"espace libre"**
2. Cliquez sur **"+"**
3. Configurez :
   - **Taille** : Selon votre RAM
     - RAM ≤ 4 GB → swap = 2× RAM
     - RAM 4-8 GB → swap = RAM
     - RAM > 8 GB → swap = 4-8 GB
   - **Type** : Primaire (ou logique)
   - **Emplacement** : Début de cet espace
   - **Utiliser comme** : Aire d'échange (swap)
4. Cliquez sur **"OK"**

**Tableau de référence swap :**

| RAM | Swap recommandé | Si hibernation |
|-----|----------------|----------------|
| 2 GB | 4 GB | 4 GB |
| 4 GB | 4 GB | 6 GB |
| 8 GB | 4-8 GB | 10 GB |
| 16 GB | 4-8 GB | 18 GB |
| 32 GB+ | 4-8 GB | RAM + 2 GB |

> 💡 Si vous n'utilisez jamais l'hibernation, le swap peut être plus petit.

### Étape 8 : Créer la partition /home (optionnel)

1. Sélectionnez **"espace libre"** (tout le reste)
2. Cliquez sur **"+"**
3. Configurez :
   - **Taille** : (laissez le maximum)
   - **Type** : Primaire (ou logique)
   - **Emplacement** : Début de cet espace
   - **Utiliser comme** : Système de fichiers ext4 avec journalisation
   - **Point de montage** : `/home`
4. Cliquez sur **"OK"**

> 💡 Donnez tout l'espace restant à /home. C'est là que vos fichiers personnels seront stockés.

### Étape 9 : Vérification finale

**Vérifiez votre schéma :**

```
Périphérique  Type   Point de montage  Format  Taille
/dev/sda1     fat32  /boot/efi         □      512 MB
/dev/sda2     ext4   /                 ☑      40 GB
/dev/sda3     swap                     ☑      8 GB
/dev/sda4     ext4   /home             ☑      79 GB
```

**Checklist de vérification :**

- [ ] ✅ Une partition montée sur **/** (racine) existe
- [ ] ✅ Elle fait au moins **20 GB**
- [ ] ✅ Son système de fichiers est **ext4**
- [ ] ✅ Une partition **swap** existe (recommandé)
- [ ] ✅ Si UEFI : partition **/boot/efi** existe et n'est PAS formatée (si partagée)
- [ ] ✅ Si /home séparé : partition **/home** existe
- [ ] ✅ Les partitions à formater sont bien cochées
- [ ] ✅ Les partitions à conserver ne sont PAS cochées
- [ ] ⚠️ Vous n'avez PAS formaté de partitions Windows par erreur

### Étape 10 : Configurer le chargeur de démarrage

En bas de l'écran :

```
Périphérique où sera installé le programme de démarrage :
[/dev/sda ▼]
```

**Sélectionnez votre disque principal** :
- **/dev/sda** (pas /dev/sda1, /dev/sda2, etc.)
- C'est le disque entier, pas une partition

> ⚠️ **Important** : GRUB doit être installé sur le DISQUE, pas sur une partition.

### Étape 11 : Lancer l'installation

1. Vérifiez **une dernière fois** tout votre schéma
2. Cliquez sur **"Installer maintenant"**
3. Une fenêtre de confirmation apparaît :

```
┌─────────────────────────────────────────┐
│  Les changements suivants seront        │
│  écrits sur le disque :                 │
│                                         │
│  Formater /dev/sda2 en ext4             │
│  Formater /dev/sda3 en swap             │
│  Formater /dev/sda4 en ext4             │
│  Utiliser /dev/sda1 en /boot/efi        │
│                                         │
│  ⚠️ Cette action est IRRÉVERSIBLE       │
│                                         │
│  [Retour]  [Continuer]                  │
└─────────────────────────────────────────┘
```

4. **Lisez attentivement** la liste des changements
5. Si tout est correct, cliquez **"Continuer"**

> 🔴 **C'est le DERNIER POINT de non-retour**. Après ce clic, les partitions seront créées/formatées.

### Étape 12 : Continuer l'installation

Maintenant, suivez les étapes normales :
1. Choisissez votre fuseau horaire
2. Créez votre compte utilisateur
3. Attendez la fin de l'installation
4. Redémarrez

---

## Cas spéciaux et configurations avancées

### Partition /boot séparée

**Quand l'utiliser :**
- Chiffrement complet du système (sauf /boot)
- Multi-boot avec plusieurs kernels
- Configuration RAID

**Configuration :**
```
Taille : 1 GB  
Type : ext4  
Point de montage : /boot  
```

### Partition /var séparée (serveurs)

**Quand l'utiliser :**
- Serveur web (logs volumineux)
- Serveur mail
- Éviter que les logs remplissent /

**Configuration :**
```
Taille : 10-20 GB (ou plus selon usage)  
Type : ext4  
Point de montage : /var  
```

### Partition /tmp séparée

**Quand l'utiliser :**
- Serveurs multi-utilisateurs
- Sécurité (montage avec noexec)

**Configuration :**
```
Taille : 2-5 GB  
Type : ext4  
Point de montage : /tmp  
```

### Partition de partage Windows/Linux

**Pour partager des fichiers entre Windows et Linux :**

**Configuration :**
```
Taille : Selon besoin (50-200 GB)  
Type : NTFS ou exFAT  
Point de montage : /mnt/partage (ou /media/partage)  
```

**Montage automatique :**
Ajoutez dans `/etc/fstab` après installation :
```
/dev/sda5  /mnt/partage  ntfs-3g  defaults,uid=1000,gid=1000  0  0
```

### LVM (Logical Volume Manager)

**Avantages :**
- Redimensionnement facile des partitions
- Snapshots du système
- Gestion flexible de l'espace

**Inconvénients :**
- Plus complexe
- Légère baisse de performance
- Récupération plus difficile en cas de problème

> 💡 **Pour débutants** : LVM n'est pas nécessaire. Utilisez-le seulement si vous savez pourquoi.

### RAID logiciel

**Pour redondance ou performance :**
- RAID 0 : Performance (striping)
- RAID 1 : Redondance (mirroring)
- RAID 5/6 : Redondance + performance

> 💡 **Configuration RAID** : Très avancé, non couvert ici. Consultez la documentation spécifique.

---

## Réutiliser une partition /home existante

**Scénario :** Vous réinstallez Linux mais voulez garder votre /home.

### Précautions CRITIQUES

> 🔴 **SAUVEGARDEZ d'abord** votre /home, même si vous ne comptez pas la formater !

### Procédure

1. Dans l'outil de partitionnement, **identifiez** votre ancienne partition /home
2. Sélectionnez-la et cliquez **"Change"**
3. Configurez :
   - **Utiliser comme** : ext4
   - **Point de montage** : `/home`
   - **Format** : **NE PAS COCHER** ❌
4. Cliquez **"OK"**

5. Créez les autres partitions (/, swap, etc.) sur l'espace libre

6. **Installez normalement**

### Important après installation

**Permissions :**
Votre ancien /home a des permissions de l'ancienne installation. Si votre nouvel utilisateur a un **UID différent**, vous devrez corriger :

```bash
# Vérifier l'UID actuel
id -u

# Si nécessaire, changer les permissions (remplacez 1000 par votre UID)
sudo chown -R 1000:1000 /home/votre-nom
```

**Fichiers de configuration :**
Certains fichiers cachés (`.bashrc`, `.config/*`) peuvent causer des conflits. Si vous avez des problèmes, renommez le dossier `.config` :

```bash
cd ~  
mv .config .config.old  
```

---

## Chiffrement des partitions

### Chiffrement complet (lors de l'installation)

L'installateur propose l'option de chiffrer automatiquement. Mais en partitionnement manuel, vous devez le faire avant :

**Via GParted en mode Live :**
1. Installez cryptsetup : `sudo apt install cryptsetup`
2. Créez une partition chiffrée : Complexe, au-delà de ce tutoriel

> 💡 **Pour débutants** : Si vous voulez du chiffrement, utilisez l'installation automatique avec l'option "Chiffrer".

### Chiffrement du /home uniquement

**Avantage :** Seules vos données personnelles sont chiffrées, pas le système.

**Lors de la création du compte utilisateur :**
- Cochez **"Chiffrer mon dossier personnel"**
- Utilisez ecryptfs automatiquement

---

## Dépannage du partitionnement

### Erreur : "Aucun système de fichiers racine défini"

**Cause :** Pas de partition montée sur `/`

**Solution :**
1. Créez ou modifiez une partition
2. Assignez le point de montage **/**
3. Vérifiez qu'elle est en ext4

### Erreur : "Impossible de créer plus de X partitions"

**Cause (MBR) :** Limite de 4 partitions primaires atteinte

**Solution :**
1. Créez une **partition étendue** (qui compte pour 1)
2. À l'intérieur, créez des partitions **logiques**

**Procédure :**
1. Créez une partition en choisissant type **"Étendue"**
2. Taille = tout l'espace restant
3. Ensuite, créez des partitions logiques dedans

### Erreur : "La partition EFI n'est pas de type FAT"

**Cause :** La partition /boot/efi n'est pas en FAT32

**Solution :**
1. Sélectionnez la partition EFI
2. **Utiliser comme** : Système de fichiers FAT32
3. Point de montage : `/boot/efi`

### La partition Windows n'apparaît plus dans GRUB

**Cause :** GRUB n'a pas détecté Windows

**Solution (après installation) :**
```bash
sudo update-grub
```

GRUB détectera Windows et l'ajoutera au menu.

### Partition de swap non détectée

**Vérification :**
```bash
sudo swapon --show
```

**Si vide, activez manuellement :**
```bash
sudo mkswap /dev/sda3  # Remplacez par votre partition swap  
sudo swapon /dev/sda3  
```

**Rendre permanent** (ajoutez dans /etc/fstab) :
```
/dev/sda3  none  swap  sw  0  0
```

### Mauvaises performances sur SSD

**Vérification TRIM :**
```bash
sudo fstrim -v /
```

**Activer TRIM automatique :**
```bash
sudo systemctl enable fstrim.timer  
sudo systemctl start fstrim.timer  
```

### Partition pleine alors qu'il reste de l'espace

**Cause :** Espace réservé root (5% par défaut)

**Réduire l'espace réservé :**
```bash
sudo tune2fs -m 1 /dev/sda2  # Réduit à 1%
```

---

## Optimisations et bonnes pratiques

### Alignement des partitions (SSD)

**Vérifier l'alignement :**
```bash
sudo parted /dev/sda align-check optimal 1
```

**Lors de la création** : GParted et l'installateur Linux Mint alignent automatiquement les partitions pour SSD (alignement 1 MB).

### Options de montage optimales

**Pour SSD** (après installation, dans /etc/fstab) :
```
/dev/sda2  /  ext4  defaults,noatime,discard  0  1
```

- **noatime** : Ne met pas à jour l'heure d'accès (moins d'écritures)
- **discard** : Active TRIM automatique

**Pour /tmp** (plus sécurisé) :
```
tmpfs  /tmp  tmpfs  defaults,noatime,mode=1777,nosuid,nodev,noexec  0  0
```

### Réserver de l'espace libre

**Laissez 10-20% d'espace libre** sur les partitions :
- Meilleures performances (surtout SSD)
- Place pour fichiers temporaires
- Évite fragmentation (HDD)

### Labels de partitions

**Donner des noms explicites** aux partitions :

```bash
sudo e2label /dev/sda2 "mint-root"  
sudo e2label /dev/sda4 "mint-home"  
```

**Avantage :** Identification facile, montage par label au lieu de /dev/sdXY.

---

## Outils de partitionnement alternatifs

### GParted (pendant l'installation)

Si vous voulez plus de contrôle avant de lancer l'installateur :

1. En mode Live, lancez **GParted** : `sudo gparted`
2. Créez vos partitions exactement comme vous voulez
3. Fermez GParted
4. Lancez l'installateur
5. Dans "Autre chose", assignez simplement les points de montage

**Avantages :**
- Interface plus complète
- Aperçu visuel clair
- Plus d'options

### Terminal (pour experts)

**fdisk, gdisk, parted :**
```bash
sudo fdisk /dev/sda   # MBR  
sudo gdisk /dev/sda   # GPT  
sudo parted /dev/sda  # Les deux  
```

> 💡 Ligne de commande = risque élevé d'erreur. Utilisez GParted à la place.

---

## Questions fréquentes

### Quelle taille donner à / et /home ?

**Règle générale :**
- **/** : 30-50 GB (suffisant pour le système et logiciels)
- **/home** : Le reste (toutes vos données)

**Si vous installez beaucoup de logiciels/jeux :**
- **/** : 80-100 GB
- **/home** : Le reste

### Faut-il séparer /home ?

**Avantages :**
- ✅ Réinstallation sans perdre vos données
- ✅ Changement de distribution facile
- ✅ Organisation logique

**Inconvénients :**
- ❌ Gestion de l'espace entre deux partitions
- ❌ Légèrement plus complexe

**Recommandation :** Oui pour une installation durable, non pour un test temporaire.

### Swap : fichier ou partition ?

**Partition swap :**
- ✅ Plus performant
- ✅ Hibernation plus fiable
- ❌ Taille fixe

**Fichier swap :**
- ✅ Flexible (redimensionnable)
- ✅ Plus simple
- ❌ Légèrement moins performant

**Recommandation :** Partition pour desktop, fichier pour serveur ou configuration flexible.

### Puis-je redimensionner les partitions après installation ?

**Oui, mais avec précautions :**

1. Sauvegardez vos données
2. Démarrez sur clé USB Live
3. Lancez GParted
4. Redimensionnez les partitions démontées
5. Vérifiez avec `sudo e2fsck -f /dev/sdaX`

> ⚠️ Redimensionner une partition montée (en cours d'utilisation) est dangereux et complexe.

### MBR ou GPT pour dual-boot Windows/Linux ?

**Utilisez ce que Windows utilise :**
- Si Windows est en UEFI → GPT
- Si Windows est en BIOS → MBR

**Vérifier sous Windows :**
```
Gestion des disques → Clic droit sur disque → Propriétés → Onglet Volumes → Style de partition
```

### Que faire si j'ai fait une erreur ?

**Pendant le partitionnement (avant "Installer maintenant") :**
- Cliquez **"Revert"** pour annuler les changements
- Ou quittez l'installateur et recommencez

**Après avoir cliqué "Installer maintenant" :**
- Trop tard pour annuler facilement
- Restaurez depuis votre sauvegarde

### Peut-on convertir MBR en GPT sans tout effacer ?

**Oui, avec gdisk** (avancé, risqué) :
```bash
sudo gdisk /dev/sda
```

Mais il est **plus sûr** de :
1. Sauvegarder toutes les données
2. Effacer le disque
3. Créer une nouvelle table GPT
4. Réinstaller

---

## Ressources et documentation

### Outils graphiques recommandés

- **GParted** : Partitionnement graphique complet
- **KDE Partition Manager** : Alternative à GParted
- **GNOME Disks** : Simple et intégré

### Documentation officielle

- 📖 [Guide Ubuntu sur le partitionnement](https://help.ubuntu.com/community/PartitioningSchemes)
- 📖 [ArchWiki - Partitioning](https://wiki.archlinux.org/title/Partitioning) (très complet)
- 📖 [Système de fichiers Linux](https://wiki.archlinux.org/title/File_systems)

### Lectures recommandées

- 🔗 [Comprendre l'arborescence Linux](https://fr.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)
- 🔗 [Guide BTRFS pour débutants](https://btrfs.wiki.kernel.org/)
- 🔗 [LVM Guide](https://wiki.ubuntu.com/Lvm)

---

## Conclusion

Le partitionnement manuel vous donne un **contrôle total** sur votre installation Linux Mint. C'est plus technique, mais aussi plus flexible et optimisable.

### Points clés à retenir

1. ✅ **Sauvegardez** avant toute manipulation
2. ✅ Au minimum : partition **/** obligatoire
3. ✅ Recommandé : **/** + **swap** + **/home** séparés
4. ✅ UEFI nécessite **/boot/efi** en FAT32
5. ✅ **ext4** est le système de fichiers standard Linux
6. ✅ Vérifiez **trois fois** avant de cliquer "Installer maintenant"
7. ✅ Le chargeur de démarrage va sur le **disque**, pas une partition

### Prochaines étapes

➡️ **[2.7 Premier démarrage et configuration initiale](./07-premier-demarrage-et-configuration-initiale.md)**

Optimisez votre système fraîchement installé.

➡️ **[8. Gestion du système de fichiers](/08-gestion-du-systeme-de-fichiers/README.md)**

Apprenez à gérer vos partitions et disques après installation.

---

**Bon partitionnement ! 🎯**

**N'oubliez pas : en cas de doute, choisissez l'installation automatique ! 🛡️**

⏭️ [Premier démarrage et configuration initiale](/02-preparation-et-installation/07-premier-demarrage-et-configuration-initiale.md)
