🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 23.9 Boot-repair et outils de secours

## Introduction

Même avec les meilleures précautions, il arrive que votre système Linux Mint refuse de démarrer ou que des données importantes soient menacées. C'est là qu'interviennent les outils de secours : des utilitaires spécialisés qui vous permettent de réparer, récupérer et sauvegarder votre système depuis l'extérieur.

Ce guide vous présente Boot-repair (l'outil miracle pour réparer le démarrage) et d'autres outils de secours essentiels. Vous apprendrez à créer des clés USB de secours et à les utiliser efficacement.

**Message rassurant :** Même si votre système ne démarre plus, vos données sont presque toujours récupérables avec les bons outils !

---

## Pourquoi avoir des outils de secours ?

### Scénarios où vous en aurez besoin

1. **GRUB cassé** → Le système ne démarre plus
2. **Partition corrompue** → Impossible d'accéder aux fichiers
3. **Mot de passe oublié** → Bloqué hors du système
4. **Erreurs critiques** → Système instable ou inutilisable
5. **Récupération de données** → Disque dur défaillant
6. **Clonage avant panne** → Sauvegarder avant remplacement matériel
7. **Virus/ransomware** → Nettoyage depuis l'extérieur

### Principe de base

Les outils de secours fonctionnent généralement depuis une **clé USB bootable** qui :
- Démarre indépendamment de votre système installé
- Permet d'accéder et réparer vos disques
- Ne modifie rien sauf si vous le demandez
- Fonctionne même si Linux Mint est complètement cassé

---

## Boot-repair : L'outil miracle pour le GRUB

Boot-repair est **l'outil numéro 1** pour réparer les problèmes de démarrage sous Linux. Il est simple, automatique, et résout 95% des problèmes de GRUB.

### Qu'est-ce que Boot-repair ?

**Boot-repair** est un utilitaire graphique qui :
- Détecte automatiquement les problèmes de bootloader
- Répare GRUB en quelques clics
- Détecte Windows pour dual-boot
- Génère des rapports de diagnostic
- Fonctionne depuis une clé USB Live

**Créé par :** YannUbuntu (développeur français)
**Licence :** Open source (GPL)

---

### Créer une clé USB avec Boot-repair

#### Option 1 : Utiliser Boot-Repair-Disk (recommandé pour débutants)

**Boot-Repair-Disk** est une ISO dédiée avec Boot-repair pré-installé.

**Téléchargement :**
- Site officiel : https://sourceforge.net/projects/boot-repair-cd/

**Créer la clé USB :**

**Depuis Windows :**
1. Téléchargez Boot-Repair-Disk ISO
2. Téléchargez Rufus (https://rufus.ie/)
3. Insérez une clé USB (2 Go minimum)
4. Lancez Rufus
5. Sélectionnez la clé USB
6. Sélectionnez l'ISO Boot-Repair-Disk
7. Cliquez sur "Démarrer"

**Depuis Linux :**
```bash
# Avec dd (remplacez sdX par votre clé)
sudo dd if=boot-repair-disk.iso of=/dev/sdX bs=4M status=progress

# Ou avec Balena Etcher (plus simple)
# Télécharger depuis https://www.balena.io/etcher/
```

---

#### Option 2 : Installer Boot-repair sur une clé Linux Mint Live

Si vous avez déjà une clé USB Linux Mint :

1. **Démarrez sur la clé USB Live**
2. **Connectez-vous à Internet** (WiFi ou Ethernet)
3. **Ouvrez un terminal**
4. **Installez Boot-repair :**

```bash
sudo add-apt-repository ppa:yannubuntu/boot-repair
sudo apt update
sudo apt install -y boot-repair
```

5. **Lancez Boot-repair :**
```bash
boot-repair
```

---

### Utiliser Boot-repair

#### Étape 1 : Démarrer sur la clé USB

1. **Insérez** la clé USB
2. **Redémarrez** l'ordinateur
3. **Appuyez sur F12** (ou F9, F10, Échap selon le fabricant)
4. **Sélectionnez** la clé USB dans le menu de boot
5. **Démarrez** en mode Live

---

#### Étape 2 : Lancer Boot-repair

**Si Boot-Repair-Disk :**
Boot-repair se lance automatiquement.

**Si clé Linux Mint :**
- Menu → Administration → Boot-repair
- Ou terminal : `boot-repair`

---

#### Étape 3 : Réparation recommandée (pour débutants)

**Interface Boot-repair :**

Vous voyez deux boutons principaux :
- **Recommended repair** (Réparation recommandée)
- **Advanced options** (Options avancées)

**Pour 95% des cas, utilisez "Recommended repair" :**

1. Cliquez sur **"Recommended repair"**
2. Boot-repair analyse votre système (peut prendre 1-2 minutes)
3. Suivez les instructions à l'écran
4. Si Boot-repair demande d'exécuter des commandes :
   - Copiez-les exactement
   - Collez dans le terminal
   - Appuyez sur Entrée
5. Attendez la fin du processus (5-10 minutes)
6. Boot-repair affiche un **résumé** et une **URL de rapport**
7. **Notez cette URL** (très utile pour demander de l'aide si besoin)
8. Cliquez sur **OK**
9. **Redémarrez** et retirez la clé USB

**Résultat attendu :**
- Le menu GRUB réapparaît au démarrage
- Linux Mint démarre normalement
- Windows apparaît dans le menu (si dual-boot)

---

#### Étape 4 : Options avancées (pour utilisateurs avertis)

Si la réparation recommandée ne suffit pas, cliquez sur **"Advanced options"**.

**Onglet "GRUB location" :**

Options principales :
- **OS to boot by default** : Système qui démarre par défaut
- **Place GRUB into** : Où installer GRUB (généralement /dev/sda)
- **Separate /boot/efi partition** : Cochez si partition EFI séparée

**Onglet "GRUB options" :**

Options utiles :
- **Purge GRUB before reinstalling it** : Réinstallation complète de GRUB
- **Uncomment GRUB_DISABLE_OS_PROBER** : Active la détection d'autres OS
- **Restore MBR** : Pour systèmes BIOS Legacy
- **Restore EFI backups** : Restaure sauvegardes EFI

**Onglet "MBR options" :**

Pour systèmes BIOS Legacy (pas UEFI) :
- **Restore MBR of sda** : Restaurer le Master Boot Record

**Onglet "Other options" :**

Options diverses :
- **Repair filesystem** : Répare aussi le système de fichiers
- **Add kernel option** : Ajoute des options (nomodeset, etc.)

**Conseil :** Sauf si vous savez exactement ce que vous faites, laissez les options par défaut et utilisez "Recommended repair".

---

### Interpréter le rapport Boot-repair

À la fin, Boot-repair génère un rapport accessible via une URL de type :
```
http://paste.ubuntu.com/p/XXXXXXXXX/
```

**Contenu du rapport :**
- Configuration de vos disques et partitions
- Systèmes d'exploitation détectés
- État de GRUB
- Fichiers de configuration importants
- Messages d'erreur éventuels
- Actions effectuées par Boot-repair

**Utilité :**
- Si le problème persiste, partagez cette URL sur un forum
- Les experts peuvent analyser le rapport pour vous aider
- Historique de la réparation effectuée

---

### Problèmes courants avec Boot-repair

#### Problème : "Please type the following commands in a new terminal..."

**Cause :** Boot-repair a besoin d'exécuter des commandes avec vos privilèges.

**Solution :**
1. Ouvrez un nouveau terminal
2. Copiez-collez exactement les commandes affichées
3. Appuyez sur Entrée
4. Revenez à Boot-repair et continuez

---

#### Problème : "Boot-repair failed to fix your PC"

**Cause :** Problème plus complexe que GRUB cassé.

**Solutions :**
1. Notez l'URL du rapport
2. Essayez les "Advanced options"
3. Vérifiez si le disque dur est détecté : `lsblk`
4. Vérifiez la santé du disque : `sudo smartctl -H /dev/sda`
5. Demandez de l'aide sur un forum avec l'URL du rapport

---

#### Problème : Secure Boot bloque le démarrage après réparation

**Solution 1 : Désactiver Secure Boot (recommandé)**
1. Redémarrez et entrez dans le BIOS/UEFI (F2, Del, F10)
2. Cherchez "Secure Boot"
3. Désactivez-le (Disabled)
4. Sauvegardez et redémarrez

**Solution 2 : Signer les modules GRUB (avancé)**
Garde Secure Boot actif mais nécessite des manipulations complexes.

---

## Super GRUB2 Disk : Le dépanneur de GRUB

**Super GRUB2 Disk** est un outil de démarrage d'urgence qui peut lancer votre système même si GRUB est complètement cassé.

### Qu'est-ce que Super GRUB2 Disk ?

C'est une **mini-distribution bootable** qui :
- Détecte tous les systèmes d'exploitation sur vos disques
- Permet de les démarrer sans GRUB fonctionnel
- Répare certains problèmes de bootloader
- Fonctionne sur BIOS et UEFI

**Site officiel :** https://www.supergrubdisk.org/

---

### Créer une clé USB Super GRUB2 Disk

1. **Téléchargez** l'ISO depuis le site officiel
2. **Créez** la clé USB avec Rufus (Windows) ou Etcher (Linux/Windows)
3. **Gardez** cette clé USB comme outil de secours permanent

---

### Utiliser Super GRUB2 Disk

1. **Démarrez** sur la clé USB Super GRUB2 Disk
2. **Menu principal :** Plusieurs options apparaissent
3. **Sélectionnez :** "Detect and show boot methods"
4. Super GRUB2 Disk **scanne** tous les disques
5. **Liste** tous les systèmes d'exploitation trouvés
6. **Sélectionnez** Linux Mint ou Windows
7. Le système **démarre** normalement

**Important :** Super GRUB2 Disk ne répare rien de façon permanente. C'est un démarrage temporaire. Une fois dans Linux, utilisez Boot-repair pour réparer définitivement.

---

### Autres fonctionnalités de Super GRUB2 Disk

**Activer GRUB :**
- "Enable GRUB's GRUB" : Active le menu GRUB natif

**Lister les disques :**
- "List devices/partitions" : Voir tous les disques et partitions

**Éditer les commandes de boot :**
- "Everything else" → Options avancées pour experts

---

## SystemRescue : La distribution de secours ultime

**SystemRescue** (anciennement SystemRescueCd) est une distribution Linux complète dédiée au dépannage et à la récupération.

### Caractéristiques

**Contient :**
- Outils de partitionnement (GParted, fdisk, parted)
- Récupération de données (TestDisk, PhotoRec)
- Sauvegarde/clonage (Clonezilla, dd, rsync)
- Diagnostic matériel (smartctl, memtest)
- Éditeurs de texte (nano, vim)
- Navigateurs de fichiers
- Accès réseau complet

**Site officiel :** https://www.system-rescue.org/

---

### Créer une clé USB SystemRescue

1. **Téléchargez** l'ISO depuis le site officiel
2. **Créez** la clé USB avec Etcher ou Rufus
3. **Taille recommandée :** 2 Go minimum

---

### Utiliser SystemRescue

1. **Démarrez** sur la clé USB
2. **Menu de démarrage :** Sélectionnez votre option
   - "Boot SystemRescue using default options" (recommandé)
3. **Connexion automatique** en tant que root
4. **Interface :** Terminal + gestionnaire de fenêtres léger

**Commandes principales :**

```bash
# Lancer GParted (partitionnement graphique)
gparted

# Lancer TestDisk (récupération de partitions)
testdisk

# Lancer PhotoRec (récupération de fichiers)
photorec

# Voir les disques
lsblk
fdisk -l

# Monter une partition
mount /dev/sda1 /mnt
```

---

### Cas d'usage SystemRescue

#### Scénario 1 : Réparer une partition corrompue

```bash
# Vérifier et réparer ext4
e2fsck -f /dev/sda1

# Pour autres systèmes de fichiers
fsck /dev/sda1  # Générique
ntfsfix /dev/sda1  # NTFS (Windows)
```

---

#### Scénario 2 : Sauvegarder une partition entière

```bash
# Créer une image disque
dd if=/dev/sda1 of=/media/usb/backup.img bs=4M status=progress

# Compresser pendant la copie
dd if=/dev/sda1 | gzip > /media/usb/backup.img.gz
```

---

#### Scénario 3 : Récupérer des fichiers effacés

```bash
# Lancer PhotoRec
photorec

# Sélectionnez le disque
# Sélectionnez la partition
# Choisissez où sauvegarder les fichiers récupérés
# Attendez la fin du scan
```

---

## TestDisk & PhotoRec : Récupération de données

**TestDisk** et **PhotoRec** sont des outils puissants de récupération développés par CGSecurity.

### TestDisk : Récupérer des partitions perdues

**Ce qu'il fait :**
- Récupère des partitions supprimées ou perdues
- Répare les tables de partition
- Reconstruit le secteur de boot
- Récupère le boot sector NTFS/FAT
- Liste et copie des fichiers (NTFS, FAT, ext2/3/4)

**Installation sur Linux Mint :**
```bash
sudo apt install testdisk
```

**Depuis une clé de secours :** Pré-installé sur SystemRescue.

---

#### Utiliser TestDisk

**Lancement :**
```bash
sudo testdisk
```

**Étapes :**

1. **Créer un log ?** → Oui (Create)
2. **Sélectionnez le disque** → Utilisez les flèches
3. **Type de partition** → Généralement "Intel" (pour PC)
4. **Analyse** → Choisissez "Analyse"
5. **Quick Search** → Recherche rapide de partitions
6. Si insuffisant → **Deeper Search** (plus long)
7. **Listez les partitions** trouvées
8. **Marquez celles** à récupérer (P = Primary, L = Logical)
9. **Write** → Écrire la nouvelle table de partition
10. **Redémarrez**

**⚠️ Attention :** TestDisk modifie la table de partition. Faites une sauvegarde d'abord si possible.

---

### PhotoRec : Récupérer des fichiers effacés

**Ce qu'il fait :**
- Récupère des fichiers effacés
- Fonctionne même si le système de fichiers est corrompu
- Supporte 480+ formats de fichiers
- Ne modifie pas le disque source (lecture seule)

**Installation sur Linux Mint :**
```bash
sudo apt install testdisk  # PhotoRec est inclus avec TestDisk
```

---

#### Utiliser PhotoRec

**Lancement :**
```bash
sudo photorec
```

**Étapes :**

1. **Sélectionnez le disque** à analyser
2. **Sélectionnez la partition** (ou "Whole disk")
3. **Type de système de fichiers** :
   - ext2/ext3/ext4 → Autres (Other)
   - FAT/NTFS → FAT/NTFS/HFS+/ReiferFS
4. **Où sauvegarder** les fichiers récupérés
   - **Important :** Choisissez un disque DIFFÉRENT !
5. **Scan** démarre automatiquement
6. Attendez (peut prendre des heures sur un gros disque)
7. **Fichiers récupérés** dans le dossier choisi

**Résultats :**
- Fichiers dans des dossiers recup_dir.1, recup_dir.2, etc.
- Noms de fichiers perdus (renommés f123456.jpg, etc.)
- Vous devrez trier manuellement

---

#### Conseils PhotoRec

**Avant de lancer :**
- Arrêtez IMMÉDIATEMENT d'utiliser le disque dès que vous réalisez la perte
- Plus vous écrivez sur le disque, moins vous récupérerez
- Ne jamais sauvegarder sur le même disque que celui analysé

**Types de fichiers récupérables :**
- Photos : jpg, png, gif, raw
- Documents : pdf, doc, docx, odt, txt
- Vidéos : mp4, avi, mkv, mov
- Archives : zip, rar, 7z, tar
- Et des centaines d'autres

---

## Clonezilla : Sauvegarde et clonage

**Clonezilla** est un outil de clonage de disques et de partitions, parfait pour :
- Sauvegarder un disque entier avant une opération risquée
- Cloner un disque vers un nouveau (passage HDD → SSD)
- Déployer une installation sur plusieurs machines

### Types de Clonezilla

**Clonezilla Live :** Pour un utilisateur unique
**Clonezilla SE (Server Edition) :** Pour clonage en réseau

Nous nous concentrons sur **Clonezilla Live**.

**Site officiel :** https://clonezilla.org/

---

### Créer une clé USB Clonezilla

1. **Téléchargez** Clonezilla Live ISO
2. **Créez** la clé USB avec Etcher ou Rufus
3. **Préparez** un disque externe pour sauvegarder l'image

---

### Utiliser Clonezilla

**Démarrage :**
1. Boot sur la clé USB Clonezilla
2. Sélectionnez la langue et le clavier
3. Choisissez "Start Clonezilla"

---

#### Mode 1 : device-image (Disque vers image)

**Pour sauvegarder un disque complet :**

1. **device-image** → Disque/partition vers image
2. **local_dev** → Sauvegarde locale (sur disque externe)
3. **Branchez** le disque externe de destination
4. Appuyez sur **Entrée** (Clonezilla détecte le disque)
5. **Sélectionnez** le disque de destination
6. **Sélectionnez** le répertoire où sauvegarder
7. Mode : **Beginner** (pour débutants)
8. **savedisk** → Sauvegarder disque entier
   - Ou **saveparts** pour une partition
9. **Nom de l'image** : Donnez un nom descriptif
10. **Sélectionnez le disque** source (celui à sauvegarder)
11. **Confirmez** et attendez

**Durée :** Variable selon la taille (1-4 heures pour 500 Go)

---

#### Mode 2 : device-device (Disque vers disque)

**Pour cloner directement un disque vers un autre :**

1. **device-device** → Clonage direct
2. Mode : **Beginner**
3. **disk_to_local_disk** → Disque vers disque
4. **Disque source** : Celui à cloner
5. **Disque destination** : Le nouveau disque
6. **⚠️ ATTENTION :** Toutes les données du disque destination seront EFFACÉES
7. **Confirmez** (vous devrez taper "yes" plusieurs fois)
8. Le clonage démarre

---

#### Restaurer une image

1. Démarrez Clonezilla comme pour sauvegarder
2. **device-image** → **local_dev**
3. Sélectionnez le disque contenant l'image
4. Mode : **Beginner**
5. **restoredisk** → Restaurer un disque
6. **Sélectionnez l'image** à restaurer
7. **Sélectionnez le disque** de destination
8. **Confirmez** et attendez

---

### Conseils Clonezilla

**Avant de cloner :**
- Vérifiez que le disque de destination est aussi grand ou plus grand que la source
- Sauvegardez les données importantes du disque de destination (elles seront perdues)
- Assurez-vous d'avoir assez d'espace pour l'image

**Compression :**
Clonezilla propose différents niveaux de compression :
- **-z1** : Gzip (rapide, compression moyenne)
- **-z2** : Bzip2 (lent, meilleure compression)
- **-z0** : Aucune compression (le plus rapide)

**Vérification :**
Activez l'option de vérification pour s'assurer que la sauvegarde est intègre.

---

## Autres outils de secours utiles

### Rescuezilla

**Version graphique simplifiée de Clonezilla.**

**Avantages :**
- Interface graphique moderne
- Plus facile que Clonezilla pour débutants
- Mêmes fonctionnalités de base

**Site :** https://rescuezilla.com/

---

### Redo Rescue

**Outil de backup/restore avec interface graphique.**

**Caractéristiques :**
- Très simple d'utilisation
- Basé sur le web (interface navigateur)
- Sauvegarde/restauration de disques complets

---

### Memtest86+

**Test de mémoire RAM.**

**Utilité :**
- Vérifier si la RAM est défectueuse
- Diagnostiquer crashs aléatoires
- Tester nouvelle RAM

**Déjà inclus dans GRUB :**
Au menu GRUB → "Memory test (memtest86+)"

**Ou clé USB dédiée :**
https://www.memtest.org/

**Utilisation :**
1. Démarrez Memtest86+
2. Les tests démarrent automatiquement
3. Laissez tourner au moins un cycle complet (plusieurs heures)
4. **Aucune erreur** = RAM OK ✅
5. **Erreurs détectées** = RAM défectueuse ❌ → À remplacer

---

### GParted Live

**Gestionnaire de partitions bootable.**

**Site :** https://gparted.org/livecd.php

**Utilité :**
- Redimensionner partitions
- Créer/supprimer partitions
- Changer système de fichiers
- Vérifier et réparer partitions

**Déjà inclus dans SystemRescue** et la plupart des distributions Live.

---

### Hiren's BootCD PE

**Collection d'outils Windows/Linux.**

**Contient :**
- Outils de partition
- Récupération de données
- Tests matériels
- Outils réseau
- Antivirus
- Et bien plus...

**Site :** https://www.hirensbootcd.org/

**Basé sur Windows PE**, mais très utile pour dépanner Windows en dual-boot.

---

## Créer votre kit de secours complet

### Clés USB recommandées

**Kit minimum (2 clés USB) :**

1. **Clé #1 : Linux Mint Live**
   - Pour démarrer et réparer Linux
   - Boot-repair installable
   - Accès aux fichiers

2. **Clé #2 : SystemRescue ou Clonezilla**
   - Pour récupération avancée
   - Clonage de disques
   - Tests matériels

**Kit complet (4 clés USB) :**

1. **Linux Mint Live** + Boot-repair
2. **SystemRescue**
3. **Clonezilla**
4. **Memtest86+** ou **Super GRUB2 Disk**

---

### Clé multi-boot avec Ventoy

**Ventoy** permet de créer une clé USB avec plusieurs ISOs bootables.

**Installation de Ventoy :**

1. **Téléchargez** Ventoy : https://www.ventoy.net/
2. **Installez** Ventoy sur une clé USB (8 Go minimum)
3. **Copiez** les fichiers ISO directement sur la clé
4. **Au boot**, Ventoy liste tous les ISOs disponibles

**Avantage :** Une seule clé USB avec tous vos outils !

**ISOs recommandés sur Ventoy :**
- Linux Mint
- Boot-Repair-Disk
- SystemRescue
- Clonezilla
- Super GRUB2 Disk
- GParted Live
- Memtest86+

---

## Scénarios de récupération complets

### Scénario 1 : GRUB cassé après mise à jour Windows

**Symptômes :** Démarrage direct sur Windows, pas de menu GRUB.

**Solution :**
1. Démarrez sur clé **Boot-Repair-Disk**
2. Lancez **Boot-repair**
3. Cliquez sur **"Recommended repair"**
4. Suivez les instructions
5. Redémarrez

**Durée :** 10-15 minutes

---

### Scénario 2 : Partition système corrompue

**Symptômes :** Erreurs "filesystem corruption", impossible de démarrer.

**Solution :**
1. Démarrez sur **SystemRescue**
2. Identifiez la partition : `lsblk`
3. Vérifiez et réparez : `sudo e2fsck -f /dev/sda1`
4. Répondez **yes** aux questions
5. Redémarrez

**Si ça ne suffit pas :**
- Montez la partition : `mount /dev/sda1 /mnt`
- Sauvegardez vos données importantes
- Envisagez une réinstallation

---

### Scénario 3 : Disque dur qui fait des bruits bizarres

**Symptômes :** Clics, grincements, système très lent.

**⚠️ URGENCE :** Le disque est en train de mourir !

**Actions immédiates :**
1. **Éteignez** l'ordinateur immédiatement
2. **Ne le rallumez plus** pour éviter d'aggraver
3. **Démarrez sur Clonezilla** depuis une clé USB
4. **Clonez** le disque vers un disque externe (device-device)
5. Une fois cloné, installez un nouveau disque
6. **Restaurez** l'image Clonezilla sur le nouveau disque

**Si le clonage échoue :**
- Essayez **ddrescue** (plus tolérant aux erreurs)
- Utilisez **PhotoRec** pour récupérer au moins les fichiers
- En dernier recours : service professionnel de récupération

---

### Scénario 4 : Fichiers importants effacés accidentellement

**Symptômes :** Vous avez supprimé des fichiers et vidé la corbeille.

**Solution :**
1. **STOP !** N'écrivez plus rien sur le disque
2. Démarrez sur **SystemRescue**
3. Lancez **PhotoRec**
4. Sélectionnez la partition concernée
5. Choisissez un disque externe pour la récupération
6. Lancez le scan
7. Triez les fichiers récupérés

**Taux de succès :** Élevé si action rapide, diminue avec le temps.

---

### Scénario 5 : Migration HDD vers SSD

**Objectif :** Transférer tout votre système vers un SSD plus rapide.

**Solution avec Clonezilla :**
1. Connectez le nouveau SSD (USB ou interne)
2. Démarrez sur **Clonezilla**
3. Mode **device-device**
4. **disk_to_local_disk**
5. Source : Ancien HDD
6. Destination : Nouveau SSD
7. Attendez le clonage complet
8. Éteignez, remplacez physiquement les disques
9. Démarrez sur le SSD

**Alternative avec SystemRescue :**
```bash
# Clonage avec dd
dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```

---

## Sauvegardes préventives

### Avant toute opération risquée

**Créez toujours une sauvegarde avant :**
- Mise à jour majeure du système
- Installation de pilotes critiques
- Repartitionnement
- Passage à une nouvelle version de Linux Mint
- Modifications système importantes

**Méthodes de sauvegarde :**

1. **Timeshift** (snapshots système)
   ```bash
   sudo timeshift --create
   ```

2. **Clonezilla** (image complète du disque)

3. **rsync** (sauvegarde des données)
   ```bash
   rsync -av --progress /home/user/ /media/backup/
   ```

---

### Stratégie 3-2-1

**Règle de sauvegarde professionnelle :**
- **3** copies de vos données
- Sur **2** supports différents
- **1** copie hors site (cloud, autre lieu)

**Exemple :**
1. Données sur votre disque principal
2. Sauvegarde sur disque externe #1
3. Sauvegarde sur disque externe #2 (ou cloud)

---

## Matériel recommandé pour kit de secours

### Clés USB

**Recommandations :**
- **Capacité :** 8-16 Go minimum
- **Vitesse :** USB 3.0 minimum (beaucoup plus rapide)
- **Marques fiables :** SanDisk, Kingston, Samsung
- **Quantité :** Au moins 2-3 clés

---

### Disques externes

**Pour sauvegardes et récupération :**
- **Capacité :** Au moins égale à vos disques internes
- **Type :** HDD pour stockage massif, SSD pour rapidité
- **Connexion :** USB 3.0 minimum

---

### Autres accessoires utiles

- **Adaptateur USB-SATA** : Pour connecter des disques internes en externe
- **Hub USB** : Si peu de ports USB
- **Câble Ethernet** : Plus fiable que WiFi pour récupération
- **Tournevis** : Pour ouvrir l'ordinateur si besoin

---

## Tableau récapitulatif des outils

| Outil | Utilité principale | Difficulté | Temps d'action |
|-------|-------------------|------------|----------------|
| **Boot-repair** | Réparer GRUB | ⭐ Facile | 10-15 min |
| **Super GRUB2 Disk** | Démarrer sans GRUB | ⭐ Facile | 5 min |
| **SystemRescue** | Tout-en-un secours | ⭐⭐ Moyen | Variable |
| **TestDisk** | Récup. partitions | ⭐⭐⭐ Difficile | 30+ min |
| **PhotoRec** | Récup. fichiers | ⭐⭐ Moyen | 1-6 heures |
| **Clonezilla** | Clonage disques | ⭐⭐ Moyen | 1-4 heures |
| **Rescuezilla** | Clone GUI | ⭐ Facile | 1-4 heures |
| **GParted Live** | Partitionnement | ⭐⭐ Moyen | 15-60 min |
| **Memtest86+** | Test RAM | ⭐ Facile | 3-8 heures |

---

## Checklist du kit de secours

**☐ Clés USB préparées**
- ☐ Linux Mint Live
- ☐ Boot-Repair-Disk ou SystemRescue
- ☐ Clonezilla
- ☐ (Optionnel) Ventoy avec plusieurs ISOs

**☐ Disques externes**
- ☐ Disque de sauvegarde (assez grand)
- ☐ Vérifié et formaté

**☐ Connaissances**
- ☐ Savoir démarrer sur USB (touche F12, etc.)
- ☐ Notions de base Linux (ls, cd, mount)
- ☐ Ce tutoriel sauvegardé ou imprimé

**☐ Informations système**
- ☐ Notes sur partitions (lsblk)
- ☐ Liste des logiciels installés
- ☐ Configuration spécifique

**☐ Accessoires**
- ☐ Câbles (SATA, Ethernet)
- ☐ Adaptateurs USB
- ☐ Tournevis si ordinateur fixe

**☐ Testez avant d'en avoir besoin !**
- ☐ Vérifiez que vous pouvez démarrer sur les clés
- ☐ Familiarisez-vous avec les outils
- ☐ Faites un test de sauvegarde/restauration

---

## FAQ - Questions fréquentes

### Dois-je vraiment créer ces clés USB maintenant ?

**OUI !** Quand vous en aurez besoin, il sera trop tard pour les créer. Préparez-les tant que votre système fonctionne.

---

### Boot-repair peut-il casser mon système ?

**Non**, Boot-repair lit et répare uniquement le bootloader. Vos données et votre système restent intacts. Dans le pire des cas, si ça ne fonctionne pas, vous êtes au même point qu'avant.

---

### Combien de temps Clonezilla prend-il ?

**Variable selon :**
- Taille du disque : 100 Go = 30-60 min, 500 Go = 1-2h, 1 To = 2-4h
- Vitesse du disque : SSD plus rapide que HDD
- Compression : Sans compression = plus rapide

---

### PhotoRec récupère tout en vrac, comment trier ?

**Méthodes :**
1. Par date de modification (propriétés du fichier)
2. Par type (*.jpg dans un dossier, *.pdf dans un autre)
3. Outils de déduplication (fdupes, rdfind)
4. Tri manuel (patience nécessaire)

**Conseil :** Cherchez les fichiers les plus importants en premier.

---

### Puis-je utiliser ces outils sur un Mac ?

**Boot-repair, TestDisk, PhotoRec :** Oui, fonctionnent sur Mac.

**Clonezilla :** Oui, mais prudence avec les partitions Mac (HFS+, APFS).

**Mieux :** Utilisez les outils Mac natifs (Time Machine, Disk Utility) pour macOS.

---

### Et si mon disque n'est même plus détecté ?

**Causes possibles :**
1. **Câble défectueux** → Tester avec un autre câble
2. **Alimentation insuffisante** → USB avec alimentation externe
3. **Disque mort** → Bruits bizarres, clics
4. **Contrôleur HS** → Le circuit du disque est cassé

**Solutions :**
- Essayez dans un autre ordinateur
- Adaptateur USB-SATA
- Si toujours rien : service professionnel de récupération

---

### Dois-je désactiver Secure Boot pour utiliser ces outils ?

**Généralement oui**, surtout pour :
- Boot-Repair-Disk
- SystemRescue
- Super GRUB2 Disk

**Procédure :**
1. Entrez dans le BIOS/UEFI
2. Cherchez "Secure Boot"
3. Désactivez (Disabled)
4. Sauvegardez et redémarrez

Vous pourrez réactiver après.

---

## Ressources complémentaires

### Sites officiels

- **Boot-repair :** https://help.ubuntu.com/community/Boot-Repair
- **Super GRUB2 Disk :** https://www.supergrubdisk.org/
- **SystemRescue :** https://www.system-rescue.org/
- **TestDisk/PhotoRec :** https://www.cgsecurity.org/
- **Clonezilla :** https://clonezilla.org/
- **Ventoy :** https://www.ventoy.net/

---

### Tutoriels vidéo

**Recherchez sur YouTube :**
- "Boot-repair tutorial"
- "Clonezilla clone disk"
- "PhotoRec file recovery"
- "TestDisk partition recovery"

**Chaînes recommandées :**
- Chris Titus Tech
- LearnLinuxTV
- The Linux Experiment

---

### Forums et aide

- **Forums Linux Mint :** https://forums.linuxmint.com/
- **Ask Ubuntu :** https://askubuntu.com/
- **Reddit r/linux4noobs :** https://reddit.com/r/linux4noobs
- **Reddit r/linuxmint :** https://reddit.com/r/linuxmint

---

## Conclusion

Les outils de secours sont votre **assurance tous risques** sous Linux Mint :

**Points clés à retenir :**

1. **Préparez vos outils AVANT** d'en avoir besoin
2. **Boot-repair résout 95%** des problèmes de démarrage
3. **Clonezilla sauvegarde** tout votre système en une image
4. **PhotoRec récupère** les fichiers même "définitivement" supprimés
5. **SystemRescue** est votre couteau suisse de dépannage
6. **Testez vos clés USB** pour vérifier qu'elles fonctionnent

**Kit minimum recommandé :**
- 1 clé Linux Mint Live (avec Boot-repair)
- 1 clé SystemRescue ou Clonezilla
- 1 disque externe pour sauvegardes

**Routine de sécurité :**
- Sauvegarde Timeshift : Hebdomadaire
- Sauvegarde Clonezilla : Mensuelle ou avant modif importante
- Sauvegarde données : Quotidienne (rsync automatisé)
- Vérification des sauvegardes : Mensuelle

**Philosophie :**
> "Espérez le meilleur, préparez-vous au pire."

Avec ce kit et ces connaissances, vous êtes paré pour faire face à presque tous les problèmes. Un système qui ne démarre plus ou des fichiers perdus ne seront plus une catastrophe, mais un simple inconvénient temporaire !

**N'attendez pas la panne pour vous préparer. Créez vos clés USB de secours dès maintenant !**

---


⏭️ [Communauté et ressources](/24-communaute-et-ressources/README.md)
