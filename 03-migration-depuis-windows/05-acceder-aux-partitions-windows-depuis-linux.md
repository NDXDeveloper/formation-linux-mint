🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.5 - Accéder aux partitions Windows depuis Linux

## Introduction

Si vous avez installé Linux Mint en dual-boot avec Windows, ou si vous possédez un disque dur externe formaté en NTFS (le système de fichiers Windows), vous avez la possibilité d'accéder à vos fichiers Windows directement depuis Linux Mint. C'est très pratique pour récupérer des documents oubliés, partager des fichiers entre les deux systèmes, ou simplement consulter vos données Windows sans redémarrer.

Ce chapitre vous explique comment accéder en toute sécurité à vos partitions Windows depuis Linux Mint.

> 💡 **Bonne nouvelle** : Linux Mint peut lire et écrire sur les partitions Windows (NTFS) sans aucun problème. C'est beaucoup plus simple que l'inverse (Windows ne peut pas lire les partitions Linux natives) !

---

## Pourquoi accéder à Windows depuis Linux ?

### Cas d'usage courants

**1. Configuration dual-boot**
- Récupérer un fichier oublié sur Windows
- Partager des documents entre les deux systèmes
- Accéder à vos photos ou musique stockées sous Windows
- Transférer progressivement vos données vers Linux

**2. Disque externe NTFS**
- Lire des disques durs externes formatés pour Windows
- Clés USB en NTFS
- Partitions de données partagées

**3. Migration et sauvegarde**
- Copier vos fichiers Windows vers Linux
- Faire une sauvegarde de vos données Windows depuis Linux
- Récupérer des données en cas de problème Windows

**4. Dépannage**
- Windows ne démarre plus : récupérer vos fichiers depuis Linux
- Nettoyer Windows depuis Linux (supprimer virus, fichiers corrompus)
- Réparer Windows avec des outils Linux

---

## Comprendre les systèmes de fichiers

### Windows utilise NTFS

**NTFS (New Technology File System)**
- Système de fichiers standard de Windows (depuis Windows XP)
- Supporte les gros fichiers (plus de 4 Go)
- Permissions et sécurité avancées
- Journalisation (résistant aux plantages)

**Linux supporte NTFS grâce à ntfs-3g**
- Pilote open source préinstallé dans Linux Mint
- Permet lecture ET écriture
- Très stable et fiable
- Gère les permissions Windows

### Autres systèmes de fichiers Windows

**FAT32**
- Ancien système de fichiers
- Compatible partout (Windows, Linux, Mac)
- Limite : fichiers maximum 4 Go
- Utilisé pour clés USB

**exFAT**
- Version moderne de FAT32
- Pas de limite de 4 Go
- Bon pour disques externes multi-OS
- Supporté par Linux Mint (avec package exfat-utils)

---

## Identifier vos partitions Windows

### Méthode 1 : Gestionnaire de fichiers (la plus simple)

1. Ouvrez le **Gestionnaire de fichiers** (Nemo)
2. Regardez la barre latérale gauche, section **"Périphériques"**
3. Vous verrez vos partitions listées, par exemple :
   - "500 GB Volume" (disque système Windows)
   - "Données" (partition de stockage)
   - "OS" ou nom personnalisé

**Identification visuelle :**
- Les partitions sont souvent nommées par leur taille
- Les icônes ressemblent à des disques durs
- Le nom peut être celui que vous avez donné sous Windows

### Méthode 2 : Application Disques

**Plus détaillé et informatif**

1. Menu → **Accessoires** → **Disques**
2. Liste de tous vos disques physiques à gauche
3. Sélectionnez un disque pour voir ses partitions
4. Pour chaque partition :
   - **Taille** : capacité totale
   - **Type** : NTFS, ext4, FAT32, etc.
   - **Point de montage** : où elle est accessible
   - **Étiquette** : nom de la partition

**Exemple de ce que vous verrez :**
```
Disque : ATA Samsung SSD 500 GB
├── Partition 1 : 100 MB (Système EFI)
├── Partition 2 : 16 MB (Réservé Microsoft)
├── Partition 3 : 200 GB (NTFS) - Windows (C:)
├── Partition 4 : 250 GB (NTFS) - Données (D:)
└── Partition 5 : 50 GB (ext4) - Linux Mint
```

### Méthode 3 : Ligne de commande (pour les curieux)

Ouvrez un terminal (Ctrl+Alt+T) et tapez :

```bash
lsblk -f
```

**Résultat typique :**
```
NAME   FSTYPE LABEL       SIZE MOUNTPOINT
sda                       500G
├─sda1 vfat   EFI         100M /boot/efi
├─sda2                     16M
├─sda3 ntfs   Windows     200G
├─sda4 ntfs   Données     250G
└─sda5 ext4               50G /
```

**Légende :**
- **NAME** : nom du périphérique (sda = premier disque, sda1 = première partition)
- **FSTYPE** : type de système de fichiers (ntfs = Windows)
- **LABEL** : étiquette/nom de la partition
- **SIZE** : taille
- **MOUNTPOINT** : où elle est montée (vide = pas montée)

---

## Accéder à une partition Windows

### Montage automatique (méthode simple)

**Étapes :**

1. **Ouvrez le Gestionnaire de fichiers**
2. **Cliquez sur la partition Windows** dans la barre latérale gauche
3. **La partition se monte automatiquement**
   - Une notification peut apparaître
   - Le nom de la partition devient cliquable/actif
4. **Naviguez dans les fichiers**

**C'est tout !** Linux Mint monte automatiquement la partition quand vous cliquez dessus.

### Où sont montées les partitions ?

Quand vous cliquez sur une partition, Linux la "monte" à un emplacement spécifique :

**Emplacement par défaut :**
```
/media/votre-nom-utilisateur/NomDeLaPartition/
```

**Exemple concret :**
- Votre nom d'utilisateur : "alice"
- Partition nommée "Windows"
- Chemin complet : `/media/alice/Windows/`

**Vérifier le point de montage :**
- Clic droit sur la partition montée → **Propriétés**
- Ou dans l'application **Disques**

### Structure d'une partition Windows

Une fois montée, voici ce que vous trouverez :

```
/media/votre-nom/Windows/
├── Program Files/              (programmes 64 bits)
├── Program Files (x86)/        (programmes 32 bits)
├── Windows/                    (système Windows)
├── PerfLogs/                   (journaux de performance)
├── ProgramData/                (données programmes)
├── Users/                      (IMPORTANT : vos fichiers personnels)
│   ├── VotreNomWindows/
│   │   ├── Desktop/           (Bureau Windows)
│   │   ├── Documents/         (Documents Windows)
│   │   ├── Downloads/         (Téléchargements)
│   │   ├── Pictures/          (Images)
│   │   ├── Music/             (Musique)
│   │   ├── Videos/            (Vidéos)
│   │   └── AppData/           (données applications)
│   └── Public/                (dossier public)
├── $Recycle.Bin/              (Corbeille Windows)
└── autres fichiers système...
```

> 📁 **Important** : Vos fichiers personnels Windows sont dans `/media/votre-nom/Windows/Users/VotreNomWindows/`

### Naviguer vers vos fichiers Windows

**Pour accéder à vos documents Windows :**

1. Partition montée : `/media/votre-nom/Windows/`
2. Allez dans **Users**
3. Entrez dans votre dossier utilisateur Windows
4. Vous retrouvez vos dossiers familiers :
   - **Desktop** = votre Bureau Windows
   - **Documents** = vos Documents
   - **Downloads** = vos Téléchargements
   - **Pictures** = vos Photos
   - **Music** = votre Musique
   - **Videos** = vos Vidéos

**Astuce : Créer un marque-page**

Pour accéder rapidement à vos fichiers Windows :
1. Naviguez jusqu'à votre dossier utilisateur Windows
2. Menu **Marque-pages** → **Ajouter un marque-page**
3. Ou : Ctrl+D dans Nemo
4. Le dossier apparaît maintenant dans la barre latérale !

---

## Lire et écrire sur une partition Windows

### Permissions : lecture et écriture

**Par défaut :**
- ✅ **Lecture** : toujours possible
- ✅ **Écriture** : possible si la partition est proprement démontée sous Windows

**Vous pouvez :**
- Copier des fichiers depuis Windows vers Linux
- Copier des fichiers depuis Linux vers Windows
- Modifier des fichiers
- Créer de nouveaux fichiers/dossiers
- Supprimer des fichiers

### Ce qu'il faut éviter

⚠️ **Ne modifiez JAMAIS les dossiers système Windows :**
- `C:\Windows\`
- `C:\Program Files\`
- `C:\Program Files (x86)\`

**Pourquoi ?**
- Risque de casser Windows
- Permissions complexes
- Pas de raison valable de le faire

✅ **Zone sûre :**
- Vos fichiers personnels dans `Users/VotreNom/`
- Partition de données séparée (D:, E:, etc.)
- Documents, Photos, Musique, Vidéos

### Copier des fichiers

**De Windows vers Linux :**
1. Ouvrez deux fenêtres du gestionnaire de fichiers
2. Fenêtre 1 : partition Windows montée
3. Fenêtre 2 : votre dossier Linux (par exemple `/home/votre-nom/Documents/`)
4. Glissez-déposez les fichiers de la fenêtre 1 vers la fenêtre 2

**Raccourcis pratiques :**
- **Ctrl+C** : copier
- **Ctrl+X** : couper
- **Ctrl+V** : coller
- **Glisser-déposer** : copie par défaut
- **Maj+Glisser** : déplacer
- **Ctrl+Glisser** : créer un lien

---

## Le problème du démarrage rapide Windows

### Qu'est-ce que le démarrage rapide ?

**Windows 8/10/11** ont une fonction "Démarrage rapide" (Fast Boot / Fast Startup) qui :
- Met Windows en "hibernation partielle" au lieu d'un arrêt complet
- Accélère le redémarrage de Windows
- **MAIS** : verrouille la partition en "lecture seule" pour Linux

### Symptôme

Quand vous essayez d'écrire sur la partition Windows depuis Linux :
```
Erreur lors de la création du fichier :
Système de fichiers monté en lecture seule
```

Ou :
```
The disk contains an unclean file system (0, 0).
Metadata kept in Windows cache, refused to mount.
```

### Solution : Désactiver le démarrage rapide

**Depuis Windows :**

1. **Ouvrez le Panneau de configuration**
   - Tapez "Panneau de configuration" dans la recherche Windows

2. **Allez dans "Options d'alimentation"**
   - Ou : Matériel et audio → Options d'alimentation

3. **Cliquez sur "Choisir l'action des boutons d'alimentation"**
   - Dans le menu de gauche

4. **Cliquez sur "Modifier des paramètres actuellement non disponibles"**
   - En haut de la fenêtre (nécessite droits admin)

5. **Décochez "Activer le démarrage rapide"**
   - Dans la section "Paramètres d'arrêt"

6. **Enregistrez les modifications**

7. **Arrêtez complètement Windows** (pas de redémarrage)

**Depuis Linux (si Windows ne démarre plus) :**

Si vous ne pouvez pas démarrer Windows, vous pouvez forcer le montage :

```bash
sudo ntfsfix /dev/sdaX
```
(Remplacez `sdaX` par votre partition, ex: `sda3`)

Puis redémarrez et accédez à Windows pour désactiver définitivement le démarrage rapide.

> ⚠️ **Important** : Utilisez `ntfsfix` uniquement en dernier recours. La bonne solution est de désactiver le démarrage rapide depuis Windows.

---

## Montage automatique au démarrage

### Pourquoi monter automatiquement ?

Si vous accédez souvent à votre partition Windows, il peut être pratique de la monter automatiquement à chaque démarrage de Linux.

**Avantages :**
- Partition toujours accessible
- Pas besoin de cliquer à chaque fois
- Pratique pour partage de fichiers

**Inconvénients :**
- Ralentit légèrement le démarrage
- Partition toujours active (consommation disque)

### Méthode graphique : Application Disques

**Étapes :**

1. **Ouvrez l'application Disques**
   - Menu → Accessoires → Disques

2. **Sélectionnez la partition Windows**
   - Cliquez sur le disque à gauche
   - Puis sur la partition NTFS

3. **Cliquez sur l'icône engrenage** ⚙️ sous le graphique

4. **Sélectionnez "Modifier les options de montage"**

5. **Désactivez "Paramètres de session utilisateur"**
   - Bouton en haut de la fenêtre

6. **Configurez les options :**
   - ✅ **Monter au démarrage** : activé
   - **Point de montage** : `/media/votre-nom/NomPartition/` (ou personnalisé)
   - **Options de montage** : `defaults` (ou laissez vide)
   - ✅ **Afficher dans l'interface utilisateur** : activé

7. **Cliquez sur OK**

8. **Entrez votre mot de passe** pour confirmer

**Résultat :** Au prochain démarrage, la partition sera montée automatiquement.

### Méthode manuelle : Éditer /etc/fstab

**Pour utilisateurs avancés**

Le fichier `/etc/fstab` contrôle les montages automatiques.

**Attention :** Une erreur dans fstab peut empêcher Linux de démarrer !

**Étapes sécurisées :**

1. **Identifier l'UUID de la partition**

```bash
sudo blkid
```

Résultat :
```
/dev/sda3: UUID="01D4ABCD12345678" TYPE="ntfs" LABEL="Windows"
```

Notez l'**UUID** de votre partition Windows.

2. **Créer un point de montage**

```bash
sudo mkdir -p /media/windows
```

3. **Sauvegarder fstab**

```bash
sudo cp /etc/fstab /etc/fstab.backup
```

4. **Éditer fstab**

```bash
sudo nano /etc/fstab
```

5. **Ajouter la ligne suivante** (à la fin du fichier) :

```
UUID=01D4ABCD12345678  /media/windows  ntfs-3g  defaults,uid=1000,gid=1000,umask=022  0  0
```

**Explication :**
- `UUID=...` : identifiant unique de la partition
- `/media/windows` : où monter la partition
- `ntfs-3g` : pilote pour NTFS
- `defaults` : options par défaut
- `uid=1000,gid=1000` : vous donne les droits (1000 = premier utilisateur)
- `umask=022` : permissions des fichiers
- `0 0` : pas de vérification au démarrage

6. **Sauvegarder** : Ctrl+O, Entrée, puis Ctrl+X

7. **Tester AVANT de redémarrer** :

```bash
sudo mount -a
```

Si pas d'erreur, c'est bon ! Si erreur, corrigez le fichier.

8. **Redémarrer** pour vérifier

**En cas de problème au démarrage :**
- Mode recovery : Entrée avancée pour Linux
- Restaurer la sauvegarde : `sudo cp /etc/fstab.backup /etc/fstab`

---

## Créer un lien symbolique vers Windows

Une alternative au montage automatique est de créer un **lien symbolique** (raccourci) dans votre dossier personnel.

### Avantages

- Pas besoin de monter automatiquement
- Accès rapide quand la partition est montée
- Organisé comme vous voulez

### Comment faire

**Exemple : Lien vers vos Documents Windows**

1. **Montez votre partition Windows** (clic dans le gestionnaire de fichiers)

2. **Ouvrez un terminal** (Ctrl+Alt+T)

3. **Créez le lien symbolique :**

```bash
ln -s /media/votre-nom/Windows/Users/VotreNomWindows/Documents ~/Documents-Windows
```

**Explication :**
- `ln -s` : créer un lien symbolique
- Premier chemin : source (fichiers Windows)
- Second chemin : destination (où créer le lien)
- `~` = votre dossier personnel

4. **Résultat :** Un dossier "Documents-Windows" apparaît dans votre dossier personnel, pointant vers vos documents Windows !

**Créer plusieurs liens :**

```bash
ln -s /media/votre-nom/Windows/Users/VotreNomWindows/Desktop ~/Bureau-Windows
ln -s /media/votre-nom/Windows/Users/VotreNomWindows/Pictures ~/Images-Windows
ln -s /media/votre-nom/Windows/Users/VotreNomWindows/Music ~/Musique-Windows
```

---

## Cas pratiques d'utilisation

### 1. Transférer progressivement ses données

**Scénario :** Vous venez d'installer Linux, vos fichiers sont encore sur Windows.

**Solution :**
1. Montez la partition Windows
2. Naviguez vers vos documents Windows
3. Sélectionnez ce que vous voulez transférer
4. Copiez vers `/home/votre-nom/Documents/`
5. Vérifiez que tout est bien copié
6. Supprimez de Windows si vous voulez libérer de l'espace

### 2. Partager des fichiers entre Windows et Linux

**Scénario :** Vous utilisez les deux OS et voulez partager des fichiers.

**Solution 1 : Partition de données séparée**
- Créez une partition NTFS dédiée au partage (D:, E:)
- Montez-la automatiquement sous Linux
- Stockez-y vos fichiers communs (musique, vidéos, projets)

**Solution 2 : Dossier dans la partition Windows**
- Créez un dossier "Partage" dans `C:\Users\VotreNom\`
- Accédez-y depuis les deux OS
- Pratique pour fichiers temporaires

### 3. Récupérer un fichier oublié

**Scénario :** Vous êtes sous Linux, besoin urgent d'un fichier Windows.

**Solution :**
1. Gestionnaire de fichiers
2. Cliquez sur partition Windows
3. Naviguez vers le fichier
4. Copiez-le où vous voulez sous Linux

**Pas besoin de redémarrer !**

### 4. Sauvegarder Windows depuis Linux

**Scénario :** Windows est instable, vous voulez sauvegarder vos fichiers.

**Solution :**
1. Démarrez sous Linux
2. Montez la partition Windows
3. Copiez tous vos documents importants vers :
   - Un disque externe
   - Une autre partition Linux
   - Le cloud
4. Vous pouvez ensuite réinstaller Windows sans crainte

### 5. Nettoyer Windows depuis Linux

**Scénario :** Windows est lent, plein de fichiers inutiles.

**Solution :**
1. Montez la partition Windows
2. Supprimez les dossiers volumineux inutiles :
   - `C:\Users\VotreNom\AppData\Local\Temp\` (temporaires)
   - Téléchargements anciens
   - Fichiers doublons
3. Videz la corbeille Windows : supprimez `$Recycle.Bin`

> ⚠️ **Attention** : Ne supprimez que vos fichiers personnels, jamais les dossiers système !

---

## Précautions et bonnes pratiques

### ✅ À faire

1. **Désactivez le démarrage rapide Windows**
   - Évite les problèmes de montage
   - Obligatoire pour écriture fiable

2. **Arrêtez complètement Windows avant de basculer vers Linux**
   - Pas de "Redémarrer" puis choix Linux au boot
   - Faites "Arrêter", puis allumez et choisissez Linux

3. **Démontez proprement avant d'éteindre Linux**
   - Gestionnaire de fichiers → clic sur icône ⏏️ à côté de la partition
   - Ou commande : `sudo umount /media/votre-nom/Windows`

4. **Faites des sauvegardes régulières**
   - Avant toute manipulation importante
   - De vos fichiers critiques

5. **Vérifiez les permissions**
   - Ne modifiez que vos fichiers personnels
   - Laissez les fichiers système tranquilles

### ❌ À éviter

1. **Ne modifiez JAMAIS les dossiers système Windows**
   - C:\Windows\
   - C:\Program Files\
   - Fichiers cachés système

2. **N'interrompez pas un transfert de gros fichiers**
   - Risque de corruption
   - Attendez la fin complète

3. **Ne formatez pas une partition par erreur**
   - Vérifiez bien quelle partition vous manipulez
   - Le formatage est irréversible

4. **N'utilisez pas de permissions trop permissives**
   - Ne donnez pas les droits root à tout le monde
   - Respectez la sécurité

5. **Ne montez pas une partition Windows en cours d'utilisation**
   - Si Windows est en hibernation ou en "Fast Boot"
   - Arrêtez complètement Windows d'abord

---

## Résolution de problèmes courants

### Problème 1 : "Impossible de monter, lecture seule"

**Message d'erreur :**
```
The disk contains an unclean file system (0, 0).
Metadata kept in Windows cache, refused to mount.
```

**Cause :** Démarrage rapide Windows activé, ou arrêt incorrect

**Solutions :**

**Option 1 : Démarrer Windows et arrêter proprement**
1. Démarrez sur Windows
2. Désactivez le démarrage rapide (voir plus haut)
3. Arrêtez complètement Windows
4. Redémarrez sur Linux

**Option 2 : Forcer le nettoyage (à utiliser avec prudence)**
```bash
sudo ntfsfix /dev/sdaX
```
(Remplacez `sdaX` par votre partition)

Cette commande nettoie le "dirty bit" NTFS.

### Problème 2 : "Accès refusé" lors de l'écriture

**Cause :** Permissions insuffisantes

**Solution :**
```bash
sudo chown -R votre-nom:votre-nom /chemin/vers/fichier
```

Ou remontez avec les bonnes options :
```bash
sudo mount -o uid=1000,gid=1000 /dev/sdaX /media/votre-nom/Windows
```

### Problème 3 : Partition ne s'affiche pas

**Cause possible 1 : Partition non formatée**
- Vérifiez dans l'application Disques
- Si "Unallocated", créez une partition

**Cause possible 2 : Type de partition non supporté**
- BitLocker (chiffrement Windows) n'est pas supporté nativement
- Déchiffrez la partition sous Windows d'abord

**Cause possible 3 : Disque endommagé**
- Vérifiez avec Disques
- Testez le disque sous Windows

### Problème 4 : Fichiers avec caractères étranges

**Cause :** Encodage de noms de fichiers différent

**Solution :**
- Généralement cosmétique, les fichiers restent accessibles
- Renommez-les avec des caractères standards si nécessaire

### Problème 5 : Lenteur lors de l'accès

**Causes possibles :**
- Disque fragmenté (vérifier sous Windows avec défragmentation)
- Disque défaillant (vérifier l'état SMART)
- USB 2.0 au lieu de 3.0
- Disque externe avec alimentation insuffisante

**Solutions :**
- Défragmentez sous Windows
- Utilisez USB 3.0
- Vérifiez les câbles et l'alimentation

---

## Différences de comportement Windows/Linux

### Noms de fichiers

**Windows :**
- Insensible à la casse : `Fichier.txt` = `fichier.txt` = `FICHIER.TXT`
- Caractères interdits : `\ / : * ? " < > |`

**Linux (sur partition Linux) :**
- Sensible à la casse : `Fichier.txt` ≠ `fichier.txt`
- Presque tous les caractères autorisés (sauf `/` et null)

**Sur partition NTFS depuis Linux :**
- Suit les règles Windows (insensible à la casse)
- Caractères Windows interdits

### Permissions

**Windows :**
- Système ACL (Access Control Lists)
- Héritées des dossiers parents
- Complexe

**Linux (sur partition NTFS) :**
- Émulation basique des permissions
- Souvent tous les fichiers ont les mêmes permissions
- Contrôlé par les options de montage

### Liens

**Windows :**
- Raccourcis (.lnk) : ne fonctionnent pas sous Linux
- Liens symboliques NTFS : rares, supportés

**Linux :**
- Liens symboliques : fonctionnent
- Liens durs : fonctionnent sur même partition

---

## Outils utiles

### Application Disques

**Fonctionnalités :**
- Visualiser toutes les partitions
- Monter/démonter
- Formater (⚠️ destructif)
- Vérifier l'état du disque (SMART)
- Benchmark de performance

**Lancer :** Menu → Accessoires → Disques

### GParted (gestionnaire de partitions)

**Installation :**
```bash
sudo apt install gparted
```

**Fonctionnalités :**
- Redimensionner partitions
- Créer/supprimer partitions
- Déplacer partitions
- Convertir types de partitions

**Lancer :** Menu → Administration → GParted

> ⚠️ **Danger** : GParted est puissant mais peut détruire des données. Sauvegardez avant toute modification !

### ntfs-3g (pilote NTFS)

**Déjà installé dans Linux Mint**

Commandes utiles :
```bash
# Informations partition NTFS
sudo ntfsinfo /dev/sdaX

# Vérifier et réparer
sudo ntfsfix /dev/sdaX

# Cloner partition NTFS
sudo ntfsclone --save-image --output backup.img /dev/sdaX
```

---

## Commandes en ligne de commande

Pour les utilisateurs avancés qui préfèrent le terminal :

### Lister les partitions
```bash
lsblk
# ou
sudo fdisk -l
# ou
df -h
```

### Monter manuellement
```bash
sudo mount /dev/sdaX /media/windows
```

### Démonter
```bash
sudo umount /media/windows
```

### Monter avec options spécifiques
```bash
sudo mount -t ntfs-3g -o uid=1000,gid=1000,umask=022 /dev/sdaX /media/windows
```

### Vérifier si montée
```bash
mount | grep ntfs
```

### Informations sur une partition
```bash
sudo blkid /dev/sdaX
```

---

## Conclusion

Accéder à vos partitions Windows depuis Linux Mint est simple et pratique. C'est l'un des grands avantages du dual-boot : vous avez accès à toutes vos données, quel que soit le système sur lequel vous démarrez.

**Points clés à retenir :**

1. ✅ Linux lit et écrit parfaitement sur NTFS
2. ✅ Cliquez simplement sur la partition pour la monter
3. ⚠️ Désactivez le démarrage rapide Windows
4. ⚠️ Ne modifiez jamais les fichiers système Windows
5. ✅ Vos fichiers personnels Windows sont dans `Users/VotreNom/`
6. ✅ Créez des liens symboliques pour un accès rapide
7. ✅ Montage automatique possible via fstab ou Disques

Avec ces connaissances, vous pouvez maintenant profiter pleinement de vos deux systèmes et partager facilement vos fichiers entre Windows et Linux !

> 🎯 **Vous avez terminé le chapitre Migration** ! Vous savez maintenant préparer votre migration, transférer vos données, retrouver vos repères, trouver des alternatives à vos logiciels, et accéder à Windows depuis Linux. Vous êtes prêt à utiliser Linux Mint au quotidien !

---

## Mémo rapide

**Pour accéder rapidement à Windows :**
1. Gestionnaire de fichiers
2. Clic sur partition Windows (barre latérale)
3. Users → VotreNomWindows → vos fichiers

**Pour désactiver démarrage rapide Windows :**
1. Panneau de configuration
2. Options d'alimentation
3. Choisir l'action des boutons d'alimentation
4. Modifier paramètres non disponibles
5. Décocher "Activer le démarrage rapide"

**En cas de problème "lecture seule" :**
```bash
sudo ntfsfix /dev/sdaX
```
(En dernier recours, préférez arrêt complet Windows)

⏭️ [Découverte de l'environnement de bureau](/04-decouverte-de-lenvironnement-de-bureau/README.md)
