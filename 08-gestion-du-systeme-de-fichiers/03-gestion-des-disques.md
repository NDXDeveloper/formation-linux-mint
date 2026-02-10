🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.3 Gestion des disques (Disques, GParted)

## Introduction

La gestion des disques et des partitions est une tâche importante sous Linux. Que vous souhaitiez formater une clé USB, créer de nouvelles partitions, ou simplement voir l'état de vos disques, Linux Mint met à votre disposition deux outils graphiques puissants :

- **Disques (Gnome Disks)** : Simple et intuitif, parfait pour les opérations courantes
- **GParted** : Plus avancé et complet, pour le partitionnement détaillé

Ce chapitre vous guidera dans l'utilisation de ces deux outils avec toutes les précautions nécessaires.

⚠️ **AVERTISSEMENT IMPORTANT** : La gestion des disques peut entraîner une **perte totale de données** si vous vous trompez de disque ou de partition. **Lisez attentivement** avant d'effectuer toute opération, et **sauvegardez vos données importantes** avant de manipuler vos partitions.

## Disques (Gnome Disks) - L'outil simple

### Lancer Disques

**Plusieurs méthodes** :
1. **Menu** → **Administration** → **Disques**
2. Rechercher "Disques" dans le menu
3. Terminal : `gnome-disks`

### Interface de Disques

L'interface se divise en deux parties :

**Partie gauche** : Liste de tous vos disques
- Disques durs internes (SSD, HDD)
- Clés USB
- Cartes SD
- Disques externes

**Partie droite** : Détails du disque sélectionné
- Modèle et capacité
- Partitions avec leur taille
- Graphique visuel des partitions
- État de santé (pour les disques SMART)

### Informations affichées

Pour chaque disque, vous verrez :
- **Modèle** : Nom du fabricant et référence
- **Taille** : Capacité totale
- **Type** : HDD (disque dur mécanique) ou SSD (disque à état solide)
- **Partitionnement** : MBR ou GPT
- **Périphérique** : `/dev/sda`, `/dev/nvme0n1`, etc.

Pour chaque partition :
- **Système de fichiers** : ext4, NTFS, FAT32, etc.
- **Taille** : Espace occupé par la partition
- **Point de montage** : Où la partition est accessible (`/`, `/home`, etc.)
- **Étiquette** : Nom personnalisé de la partition

## Opérations courantes avec Disques

### 1. Visualiser un disque

1. **Sélectionnez un disque** dans la liste de gauche
2. **Observez** :
   - Le graphique circulaire montre les partitions
   - Chaque partition est détaillée en dessous
   - Les partitions montées ont une icône de dossier

💡 **Code couleur** : Les partitions utilisées sont souvent en bleu, l'espace libre en gris clair.

### 2. Formater une clé USB ou un disque externe

**Scénario** : Vous voulez effacer complètement une clé USB.

⚠️ **ATTENTION** : Le formatage **efface toutes les données** !

**Étapes** :
1. **Branchez la clé USB**
2. **Sélectionnez-la** dans Disques (vérifiez bien la taille pour ne pas vous tromper !)
3. Cliquez sur le **menu hamburger** (☰) en haut à droite
4. Choisissez **Formater le disque...**
5. Une fenêtre s'ouvre :
   - **Effacement** :
     - "Rapide" : Supprime juste la table des partitions (recommandé)
     - "Compatible avec tous les systèmes" : Écrit des zéros partout (très long)
   - **Partitionnement** :
     - "Compatible avec tous les systèmes et périphériques (MBR/DOS)" : Pour clés USB ≤ 2 To
     - "Pour systèmes Linux uniquement (GPT)" : Pour disques modernes
6. Cliquez sur **Formater...**
7. **Confirmez** en tapant "Formater" (sécurité)

### 3. Créer une partition sur de l'espace libre

**Scénario** : Vous avez de l'espace non alloué et voulez créer une partition.

**Étapes** :
1. Sélectionnez le disque contenant l'espace libre
2. Cliquez sur la zone **"Espace libre"** dans le graphique
3. Cliquez sur le bouton **+** (ou "Créer une partition")
4. Configurez :
   - **Taille de la partition** : Utilisez le curseur ou entrez une valeur
   - **Type** :
     - "Données Linux (Ext4)" : Pour Linux
     - "Autres" → "FAT" : Pour compatibilité Windows/Mac
     - "Autres" → "NTFS" : Pour Windows
   - **Nom** : Donnez un nom descriptif (ex: "Donnees", "Sauvegardes")
5. Cliquez sur **Créer**

💡 **Astuce** : La partition sera automatiquement formatée dans le système de fichiers choisi.

### 4. Monter et démonter une partition

**Monter** (rendre accessible) :
1. Sélectionnez la partition
2. Cliquez sur le bouton **▶ (Monter la partition)**
3. Elle devient accessible dans `/media/votrenom/`

**Démonter** :
1. Sélectionnez la partition montée
2. Cliquez sur le bouton **⏹ (Démonter la partition)**

⚠️ **Important** : Démontez toujours vos clés USB avant de les retirer physiquement !

### 5. Changer le nom (étiquette) d'une partition

1. Sélectionnez la partition
2. Cliquez sur le bouton **⚙ (Paramètres)** sous la partition
3. Choisissez **Éditer le système de fichiers...**
4. Changez l'**étiquette**
5. Cliquez sur **Changer**

💡 **Note** : Certains systèmes de fichiers ont des limitations (FAT32 : 11 caractères max, pas d'espaces).

### 6. Vérifier l'état de santé d'un disque (SMART)

**Pour les SSD et HDD modernes** :

1. Sélectionnez le disque (pas une partition, le disque entier)
2. Cliquez sur le **menu hamburger** (☰)
3. Choisissez **Données SMART et auto-tests...**
4. Observez :
   - **État global** : SAIN / DÉFAILLANT
   - **Température** : Normale si < 50°C
   - **Secteurs réalloués** : Indicateur d'usure
   - **Heures sous tension** : Âge du disque

⚠️ **Si le statut est "DÉFAILLANT"** : Sauvegardez immédiatement vos données et remplacez le disque !

### 7. Créer une image disque (sauvegarde)

**Sauvegarder complètement une clé USB ou une partition** :

1. Sélectionnez la partition
2. Menu **hamburger** → **Créer une image du disque...**
3. Choisissez où enregistrer le fichier `.img`
4. Attendez la fin de la copie

**Restaurer l'image** :
1. Menu **hamburger** → **Restaurer l'image du disque...**
2. Sélectionnez le fichier `.img`
3. Confirmez

💡 **Utilité** : Pratique pour dupliquer une clé USB bootable ou sauvegarder une partition système.

## GParted - L'outil avancé

### Qu'est-ce que GParted ?

**GParted** (Gnome Partition Editor) est l'outil de référence pour le partitionnement sous Linux. Plus puissant que Disques, il permet :
- Redimensionner des partitions sans perte de données
- Déplacer des partitions
- Créer des tables de partitions complexes
- Convertir entre systèmes de fichiers
- Gérer tous les types de partitions

### Installation

GParted n'est pas toujours installé par défaut :

**Terminal** :
```bash
sudo apt update  
sudo apt install gparted  
```

**Gestionnaire de logiciels** :
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "GParted"
3. Cliquez sur **Installer**

### Lancer GParted

⚠️ **Privilèges administrateur requis** : GParted demande votre mot de passe au lancement.

**Méthodes** :
1. **Menu** → **Administration** → **GParted**
2. Terminal : `sudo gparted`

### Interface de GParted

**Barre d'outils en haut** :
- Sélecteur de disque (coin supérieur droit)
- Boutons d'actions (Nouveau, Supprimer, Redimensionner, etc.)

**Zone principale** :
- Graphique visuel des partitions (barres horizontales)
- Liste détaillée des partitions

**Zone inférieure** :
- File d'attente des opérations en attente

**Barre de statut** :
- Informations sur la partition sélectionnée

### Caractéristiques importantes de GParted

#### Système de file d'attente

🔄 **CONCEPT CLÉ** : GParted ne modifie **RIEN immédiatement** !

1. Vous effectuez des opérations (créer, redimensionner, supprimer)
2. Elles s'ajoutent à la **file d'attente**
3. Vous pouvez les **annuler** avant de les appliquer
4. Vous cliquez sur le **bouton Appliquer** (✓ vert) pour exécuter toutes les opérations

💡 **Avantage** : Vous pouvez planifier plusieurs modifications et les appliquer d'un coup, ou tout annuler si vous changez d'avis.

#### Code couleur des systèmes de fichiers

GParted utilise des couleurs pour identifier rapidement :
- **Vert clair** : ext4 (Linux)
- **Bleu foncé** : NTFS (Windows)
- **Rose/Violet** : FAT32 / exFAT
- **Orange** : Espace non alloué
- **Jaune** : Swap Linux
- **Gris** : Partition EFI

## Opérations avancées avec GParted

### 1. Redimensionner une partition

**Scénario** : Vous voulez réduire une partition pour créer de l'espace libre.

⚠️ **PRÉCAUTIONS** :
- **Sauvegardez vos données** avant toute opération
- Ne redimensionnez **jamais** une partition en cours d'utilisation (démontez-la d'abord)
- Pour la partition système (`/`), démarrez sur un Live USB

**Étapes** :
1. **Démontez la partition** : Clic droit → Démonter
2. **Clic droit** sur la partition → **Redimensionner/Déplacer**
3. Une fenêtre s'ouvre avec :
   - **Graphique interactif** : Faites glisser les bords
   - **Espace libre précédent** : Espace avant la partition
   - **Nouvelle taille** : Taille de la partition
   - **Espace libre suivant** : Espace après la partition
4. **Ajustez** :
   - Glissez le bord droit vers la gauche pour réduire
   - Glissez vers la droite pour agrandir (si espace disponible)
5. Cliquez sur **Redimensionner/Déplacer**
6. Cliquez sur **Appliquer** (✓ vert) pour lancer l'opération

⏱️ **Durée** : Peut prendre de quelques minutes à plusieurs heures selon la taille et la quantité de données.

### 2. Créer une nouvelle partition

**Étapes** :
1. **Sélectionnez l'espace non alloué** (en orange/gris)
2. Clic sur **Nouvelle** ou clic droit → **Nouveau**
3. Configurez :
   - **Taille** : Utilisez tout l'espace ou une partie
   - **Créer en tant que** : Partition principale (ou logique si MBR étendu)
   - **Système de fichiers** :
     - `ext4` : Linux (recommandé pour /home, données Linux)
     - `ntfs` : Windows
     - `fat32` : Clés USB, compatibilité multiplateforme (max 4 Go/fichier)
     - `exfat` : Clés USB modernes, pas de limite
     - `linux-swap` : Mémoire d'échange
   - **Étiquette** : Nom de la partition
4. Cliquez sur **Ajouter**
5. Cliquez sur **Appliquer** (✓ vert)

### 3. Supprimer une partition

⚠️ **DANGER** : Suppression = **perte définitive** de toutes les données !

**Étapes** :
1. **Démontez** la partition si elle est montée
2. **Clic droit** sur la partition → **Supprimer**
3. La partition devient **espace non alloué**
4. Cliquez sur **Appliquer** (✓ vert)

🛡️ **Vérifiez trois fois** que c'est bien la bonne partition avant d'appliquer !

### 4. Formater une partition

**Différence avec "supprimer"** : Formater conserve la partition mais efface son contenu.

**Étapes** :
1. **Démontez** la partition
2. **Clic droit** → **Formater vers** → Choisissez le système de fichiers
3. Cliquez sur **Appliquer** (✓ vert)

### 5. Changer l'étiquette d'une partition

1. **Clic droit** sur la partition → **Étiquette du système de fichiers**
2. Entrez le nouveau nom
3. Cliquez sur **Appliquer** (✓ vert)

### 6. Vérifier et réparer un système de fichiers

**Utilité** : Corriger les erreurs après une extinction brutale ou des problèmes de disque.

**Étapes** :
1. **Démontez** la partition
2. **Partition** → **Vérifier** (ou clic droit → Vérifier)
3. GParted lance l'outil approprié :
   - `e2fsck` pour ext4
   - `ntfsfix` pour NTFS
   - `fsck.fat` pour FAT32

💡 **Note** : Les erreurs détectées seront affichées. La plupart peuvent être corrigées automatiquement.

### 7. Définir les drapeaux (flags) d'une partition

**Drapeaux courants** :
- **boot** : Partition bootable (pour anciennes installations)
- **esp** : EFI System Partition (partition système EFI)
- **msftdata** : Données Microsoft
- **swap** : Partition d'échange Linux

**Comment faire** :
1. **Clic droit** sur la partition → **Gérer les drapeaux**
2. Cochez ou décochez les cases nécessaires
3. Fermez (appliqué immédiatement)

⚠️ **Attention** : Ne modifiez pas ces drapeaux sans savoir ce que vous faites, surtout pour `boot` et `esp` !

### 8. Copier et coller une partition

**Utilité** : Dupliquer une partition vers un autre disque ou emplacement.

**Étapes** :
1. **Clic droit** sur la partition source → **Copier**
2. **Clic droit** sur l'espace non alloué de destination → **Coller**
3. Ajustez la taille si nécessaire
4. Cliquez sur **Appliquer** (✓ vert)

⏱️ **Durée** : Peut être très long selon la taille des données.

## Cas d'usage pratiques

### Cas 1 : Préparer une clé USB multi-usage

**Objectif** : Moitié pour Linux (ext4), moitié compatible tous systèmes (exFAT).

**Avec GParted** :
1. Supprimez toutes les partitions de la clé
2. Créez une partition de 50% en exFAT (étiquette "PARTAGE")
3. Créez une partition de 50% en ext4 (étiquette "LINUX")
4. Appliquez

### Cas 2 : Agrandir la partition /home

**Scénario** : Votre partition système (/) a trop d'espace, vous voulez en donner à /home.

⚠️ **Prérequis** : Démarrez sur un Live USB de Linux Mint pour modifier les partitions système.

**Étapes** :
1. Dans GParted, réduisez `/` (par exemple de 100 Go à 50 Go)
2. Agrandissez `/home` avec l'espace libéré
3. Appliquez

### Cas 3 : Créer une partition swap

**Si vous n'avez pas créé de swap à l'installation** :

1. Créez une partition de 4-8 Go
2. Système de fichiers : **linux-swap**
3. Appliquez
4. Notez l'UUID avec : `sudo blkid | grep swap`
5. Ajoutez-la dans `/etc/fstab` (voir chapitre 8.7)

### Cas 4 : Convertir FAT32 en exFAT

**Pourquoi ?** : FAT32 limite les fichiers à 4 Go, exFAT n'a pas cette limite.

⚠️ **Attention** : Nécessite de formater (perte de données).

1. **Sauvegardez** le contenu de la partition
2. Dans GParted, formatez la partition en **exfat**
3. Appliquez
4. **Restaurez** vos fichiers

## Créer une nouvelle table de partitions

⚠️ **TRÈS DANGEREUX** : Efface **toutes** les partitions du disque !

**Quand le faire ?** :
- Nouveau disque jamais utilisé
- Conversion MBR → GPT ou GPT → MBR
- Disque complètement corrompu

**Types de tables** :
- **GPT** (GUID Partition Table) : Moderne, recommandé
  - Supporte les disques > 2 To
  - Requis pour UEFI
  - Jusqu'à 128 partitions

- **MBR** (Master Boot Record) : Ancien
  - Limité à 2 To
  - Maximum 4 partitions principales (ou 3 + 1 étendue)
  - Compatible avec vieux systèmes BIOS

**Étapes** :
1. **Périphérique** → **Créer une table de partitions...**
2. Choisissez **gpt** (recommandé) ou **msdos** (= MBR)
3. **Confirmez** (tout sera effacé !)

## Précautions et bonnes pratiques

### ✅ Avant toute opération

1. **Sauvegardez vos données importantes** : Ne faites jamais confiance à 100%
2. **Vérifiez trois fois** le disque et la partition sélectionnés
3. **Assurez-vous d'avoir du temps** : Ne lancez pas d'opération longue si vous devez partir
4. **Branchez l'ordinateur** : Pas d'opération sur batterie !
5. **Ne touchez pas à /dev/sda** si c'est votre disque système (sauf si vous savez ce que vous faites)

### ⚠️ Pendant l'opération

1. **N'interrompez jamais** une opération en cours
2. **Ne débranchez pas** le périphérique
3. **N'éteignez pas** l'ordinateur
4. **Attendez la fin** même si ça semble long

### 🔧 Dépannage

**Si GParted ne démarre pas** :
```bash
# Mettez à jour la liste des paquets
sudo apt update

# Réinstallez GParted
sudo apt install --reinstall gparted
```

**Si une partition ne se démonte pas** :
```bash
# Voir qui utilise la partition
lsof /point/de/montage

# Forcer le démontage (attention !)
sudo umount -f /point/de/montage
```

**Si l'opération échoue** :
- Lisez le message d'erreur dans la fenêtre de détails
- Vérifiez que le disque n'est pas défectueux
- Redémarrez et réessayez
- Utilisez un Live USB si c'est la partition système

## Différences entre Disques et GParted

| Fonctionnalité | Disques | GParted |
|----------------|---------|---------|
| **Interface** | Simple, épurée | Plus technique |
| **Redimensionner** | Non | Oui |
| **Créer partition** | Oui (basique) | Oui (avancé) |
| **Formater** | Oui | Oui |
| **File d'attente** | Non (immédiat) | Oui |
| **SMART** | Oui | Non |
| **Image disque** | Oui | Non |
| **Déplacer partition** | Non | Oui |
| **Conversion système fichiers** | Non | Oui (avec formatage) |
| **Copier partition** | Non | Oui |
| **Débutant** | ✅ Recommandé | ⚠️ Avec prudence |

**Conseil** :
- Utilisez **Disques** pour les tâches courantes (formater clé USB, voir état disque)
- Utilisez **GParted** pour le partitionnement avancé (redimensionner, réorganiser)

## Commandes en ligne de commande (bonus)

Pour les curieux, voici les équivalents terminal :

**Lister les disques et partitions** :
```bash
lsblk
# ou
sudo fdisk -l
```

**Voir l'utilisation de l'espace** :
```bash
df -h
```

**Informations détaillées sur les partitions** :
```bash
sudo parted -l
```

**Formater une partition** :
```bash
# En ext4
sudo mkfs.ext4 /dev/sdX1

# En FAT32
sudo mkfs.vfat /dev/sdX1

# En NTFS
sudo mkfs.ntfs /dev/sdX1
```

⚠️ **Attention** : Remplacez `/dev/sdX1` par votre partition réelle !

## Résumé

**Points clés à retenir** :

1. **Deux outils principaux** :
   - **Disques** : Simple, pour usage quotidien
   - **GParted** : Avancé, pour partitionnement

2. **Opérations courantes** :
   - Visualiser : Voir les disques et partitions
   - Formater : Effacer et préparer un disque
   - Créer : Nouvelle partition
   - Redimensionner : Modifier la taille (GParted uniquement)

3. **Sécurité** :
   - Toujours sauvegarder avant modification
   - Vérifier 3 fois la partition sélectionnée
   - Ne jamais interrompre une opération

4. **GParted** :
   - Travaille avec une file d'attente
   - Rien n'est modifié avant de cliquer sur Appliquer
   - Nécessite un démontage des partitions

5. **Systèmes de fichiers** :
   - `ext4` → Linux
   - `ntfs` → Windows
   - `exfat` → Compatibilité universelle
   - `fat32` → Clés USB (limite 4 Go/fichier)

La gestion des disques peut sembler intimidante, mais avec les bonnes précautions et en commençant par des opérations simples (formater une clé USB), vous gagnerez rapidement en confiance !

⏭️ [Les systèmes de fichiers (ext4, Btrfs, NTFS, FAT32, exFAT)](/08-gestion-du-systeme-de-fichiers/04-les-systemes-de-fichiers.md)
