🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 17.5 Restauration en cas de problème

## Introduction

Avoir des sauvegardes, c'est bien. Savoir les restaurer efficacement, c'est indispensable ! Ce chapitre vous guide à travers les différentes procédures de restauration selon le type de problème rencontré.

### L'importance de connaître la restauration

**Analogie :** Une sauvegarde sans savoir restaurer, c'est comme avoir une bouée de sauvetage sans savoir nager. En cas d'urgence, le temps que vous cherchez comment faire, il est déjà trop tard.

**Pourquoi pratiquer AVANT le problème :**
- Moins de stress quand le problème survient
- Procédure fraîche en mémoire
- Confiance en vos sauvegardes
- Détection précoce de problèmes éventuels
- Temps de récupération réduit

### Types de problèmes et solutions

| Problème | Gravité | Solution | Temps |
|----------|---------|----------|-------|
| Fichier supprimé | ⚠️ Faible | Restauration fichier | 5 min |
| Dossier corrompu | ⚠️⚠️ Moyenne | Restauration dossier | 15 min |
| Système instable | ⚠️⚠️⚠️ Élevée | Snapshot Timeshift | 30 min |
| Système ne démarre plus | ⚠️⚠️⚠️⚠️ Critique | Boot rescue + restore | 1-2h |
| Disque dur en panne | ⚠️⚠️⚠️⚠️⚠️ Catastrophique | Nouveau disque + image | 3-6h |

## Scénario 1 : Restauration de fichiers individuels

### Situation

Vous avez accidentellement supprimé un fichier ou un dossier, ou un fichier est corrompu.

### Signes

- Fichier introuvable dans son emplacement habituel
- Fichier dans la corbeille
- Fichier ne s'ouvre plus correctement
- Erreur "fichier corrompu" ou "illisible"

### Solution A : Vérifier la corbeille

**Avant de paniquer, vérifiez la corbeille !**

1. Ouvrez le gestionnaire de fichiers (Nemo)
2. Cliquez sur **Corbeille** dans le panneau latéral
3. Recherchez votre fichier
4. Clic droit → **Restaurer**

Le fichier revient à son emplacement d'origine !

**Limitation :** La corbeille ne conserve les fichiers que temporairement. Si vous avez vidé la corbeille ou si trop de temps s'est écoulé, passez à la solution suivante.

### Solution B : Restauration avec Backintime

Si vous utilisez Backintime pour vos sauvegardes de données :

**Étapes détaillées :**

1. **Ouvrir Backintime**
   - Menu → Back In Time
   - Ou `backintime-qt` dans le terminal

2. **Naviguer dans le temps**
   - À gauche : liste des snapshots (dates)
   - Sélectionnez un snapshot d'avant la suppression
   - Astuce : Si vous savez quand le fichier existait encore, choisissez cette date

3. **Localiser le fichier**
   - À droite : structure des dossiers du snapshot
   - Naviguez comme dans un explorateur normal
   - Utilisez la recherche si besoin

4. **Restaurer le fichier**
   - **Méthode 1 :** Clic droit sur le fichier → **Restore**
   - **Méthode 2 :** Sélectionnez le fichier → Bouton **Restore** dans la barre d'outils

5. **Choisir les options de restauration**
   - **Restore to:** Emplacement de destination
     - Original location : Emplacement d'origine (recommandé)
     - Custom location : Autre emplacement
   - **If the file already exists:**
     - Ask : Demander confirmation
     - Replace : Remplacer automatiquement
     - Keep both : Garder les deux versions

6. **Confirmer**
   - Cliquez sur **OK**
   - Vérifiez que le fichier est bien restauré

**Cas particulier - Comparer les versions :**

Si vous voulez voir différentes versions du fichier avant de restaurer :

1. Sélectionnez le fichier
2. Menu **Snapshots** → **View Snapshot Log**
3. Vous voyez toutes les versions sauvegardées
4. Double-clic pour ouvrir et comparer
5. Restaurez la bonne version

### Solution C : Restauration avec Déjà Dup

Si vous utilisez Déjà Dup :

**Procédure :**

1. **Ouvrir Déjà Dup**
   - Menu → Sauvegardes (ou Backups)

2. **Lancer la restauration**
   - Cliquez sur l'onglet **Aperçu** (Overview)
   - Cliquez sur **Restaurer** (Restore)

3. **Choisir la sauvegarde**
   - Déjà Dup affiche les sauvegardes disponibles
   - Sélectionnez celle qui contient le fichier
   - Généralement : la plus récente

4. **Sélectionner les fichiers**
   - **Restore files:** Choisissez
     - **Restore from the latest backup** : Plus récent (recommandé)
     - **Restore from a specific date** : Date précise
   - Cliquez sur **Forward**

5. **Localiser le fichier**
   - Naviguez dans l'arborescence
   - Cochez les fichiers/dossiers à restaurer
   - Vous pouvez restaurer plusieurs fichiers simultanément

6. **Destination**
   - **Restore to:**
     - Original location : Emplacement d'origine
     - Specific folder : Dossier personnalisé
   - Cliquez sur **Forward**

7. **Confirmation**
   - Vérifiez le résumé
   - Cliquez sur **Restore**
   - Entrez le mot de passe si la sauvegarde est chiffrée
   - Attendez la fin de la restauration

### Solution D : Restauration depuis le cloud

Si vos fichiers sont sauvegardés dans le cloud :

**Google Drive :**

1. Ouvrez https://drive.google.com
2. Clic droit dans le dossier → **Corbeille**
3. Ou accédez à la corbeille Google Drive (panneau gauche)
4. Sélectionnez le fichier
5. Clic droit → **Restaurer**

Google Drive garde les fichiers supprimés 30 jours.

**Nextcloud :**

1. Connectez-vous à votre Nextcloud
2. Fichiers → Fichiers supprimés
3. Sélectionnez le fichier
4. Cliquez sur **Restaurer**

Ou utilisez les versions (si activé) :
1. Clic droit sur le fichier → **Versions**
2. Téléchargez la version souhaitée

**OneDrive / Dropbox :**

Procédure similaire : accès à la corbeille via l'interface web, restauration en quelques clics.

### Restauration de plusieurs fichiers

Si vous avez perdu un dossier entier ou de nombreux fichiers :

**Avec Backintime :**
1. Sélectionnez le dossier parent
2. Restaurez le dossier complet
3. Ou maintenez Ctrl et sélectionnez plusieurs fichiers

**Avec Déjà Dup :**
1. Dans l'arborescence de restauration
2. Cochez les dossiers ou fichiers multiples
3. Restaurez en une seule fois

**Conseil :** Pour de gros volumes, restaurez dans un dossier temporaire d'abord, vérifiez, puis déplacez vers l'emplacement final.

## Scénario 2 : Restauration du système avec Timeshift

### Situation

Votre système Linux Mint est instable, ne fonctionne plus correctement après une mise à jour ou une manipulation.

### Signes

- Environnement de bureau ne démarre plus
- Applications système plantent constamment
- Erreurs au démarrage
- Système très lent sans raison
- Après installation d'un pilote problématique

### Quand restaurer avec Timeshift

**Restaurez un snapshot Timeshift si :**
- Le problème est survenu récemment (après une mise à jour, modification)
- Vous avez un snapshot d'avant le problème
- Le système démarre encore (même en mode dégradé)
- Les données personnelles ne sont pas concernées

**N'utilisez PAS Timeshift si :**
- Vos données personnelles sont perdues (Timeshift ne les sauvegarde pas)
- Le disque dur est physiquement défaillant
- Le problème existait déjà dans les snapshots

### Restauration depuis un système fonctionnel

Si vous pouvez encore démarrer Linux Mint (même lentement) :

**Procédure détaillée :**

1. **Ouvrir Timeshift**
   - Menu → Timeshift
   - Entrez votre mot de passe administrateur

2. **Vérifier les snapshots disponibles**
   - Liste des snapshots avec dates
   - Identifiez celui d'AVANT le problème
   - Lisez les commentaires si vous en avez ajouté

3. **Sélectionner le snapshot**
   - Cliquez sur le snapshot désiré
   - Il apparaît en surbrillance

4. **Lancer la restauration**
   - Cliquez sur le bouton **Restaurer**
   - Ou clic droit → Restaurer

5. **Options de restauration**
   Timeshift affiche les options :

   **Partition de destination :**
   - Normalement : votre partition système actuelle (/)
   - Ne changez que si vous savez ce que vous faites

   **Fichiers à restaurer :**
   - Par défaut : tous (recommandé)
   - Avancé : sélection manuelle (pour experts)

6. **Confirmation**
   - Timeshift affiche un résumé
   - **Lisez attentivement** ce qui sera restauré
   - Cliquez sur **Suivant** (Next)

7. **Confirmation finale**
   - Dernière chance d'annuler
   - Timeshift vous demande de confirmer
   - Tapez votre mot de passe
   - Cliquez sur **Restaurer** (Restore)

8. **Processus de restauration**
   - **NE TOUCHEZ À RIEN** pendant le processus
   - Une barre de progression s'affiche
   - Durée : 10-30 minutes selon la taille
   - **N'éteignez pas** et **ne redémarrez pas** l'ordinateur

9. **Fin de restauration**
   - Message de succès
   - Timeshift recommande de redémarrer
   - Cliquez sur **Redémarrer** (Restart)

10. **Après redémarrage**
    - Le système est revenu à l'état du snapshot
    - Vérifiez que tout fonctionne
    - Testez les applications principales

**Important :** Après restauration, toutes les modifications faites APRÈS la date du snapshot sont perdues (installations, mises à jour, configurations). Vos données personnelles (/home) ne sont pas affectées.

### Restauration depuis le menu de démarrage (GRUB)

Si le système ne démarre plus normalement mais GRUB s'affiche :

**Procédure :**

1. **Au démarrage**
   - Allumez l'ordinateur
   - Le menu GRUB apparaît (liste des systèmes)
   - Si le menu n'apparaît pas, maintenez **Shift** ou **Esc** au démarrage

2. **Accéder aux anciennes versions**
   - Dans GRUB, sélectionnez **Advanced options for Linux Mint**
   - Appuyez sur **Entrée**

3. **Choisir un kernel précédent**
   - Vous voyez une liste de kernels (versions Linux)
   - Sélectionnez une version antérieure
   - Appuyez sur **Entrée**

4. **Démarrer en mode recovery**
   - Ou sélectionnez la ligne avec **(recovery mode)**
   - Appuyez sur **Entrée**

5. **Menu Recovery**
   - Sélectionnez **root** (Drop to root shell)
   - Appuyez sur **Entrée**
   - Un terminal s'ouvre

6. **Restaurer avec Timeshift en ligne de commande**
   ```bash
   # Lister les snapshots
   sudo timeshift --list

   # Restaurer un snapshot spécifique
   sudo timeshift --restore --snapshot '2024-11-29_10-00-00'
   ```

7. **Suivre les instructions**
   - Confirmez quand demandé
   - Attendez la fin
   - Redémarrez : `sudo reboot`

### Restauration depuis un Live USB

Si le système ne démarre plus du tout :

**Préparation :**
- Clé USB avec Linux Mint Live (celle de votre installation)
- Ou créez-en une nouvelle sur un autre ordinateur

**Procédure :**

1. **Démarrer sur le Live USB**
   - Insérez la clé USB
   - Redémarrez l'ordinateur
   - Accédez au menu de boot (F12, F2, Esc selon PC)
   - Sélectionnez la clé USB
   - Choisissez **Start Linux Mint** (sans installation)

2. **Attendre le bureau Live**
   - Le bureau Linux Mint Live s'affiche
   - Vous êtes en mode "essai", rien n'est modifié sur votre disque

3. **Ouvrir Timeshift**
   - Menu → Timeshift
   - Pas besoin de mot de passe (vous êtes en Live)

4. **Timeshift détecte automatiquement**
   - Timeshift scanne vos disques
   - Il trouve automatiquement vos snapshots existants
   - Message : "Snapshots found on device /dev/sdaX"

5. **Sélectionner le périphérique de sauvegarde**
   - Si demandé, sélectionnez où sont vos snapshots
   - Généralement détecté automatiquement

6. **Restaurer**
   - Même procédure que depuis le système
   - Sélectionnez le snapshot
   - Cliquez **Restaurer**
   - **Important :** Sélectionnez bien la partition système de votre disque (pas celle du Live USB !)
   - Confirmez

7. **Attendre la fin**
   - Plus long depuis Live USB (selon connexion USB)
   - 20-45 minutes possibles
   - Patience !

8. **Redémarrer**
   - Une fois terminé, retirez la clé USB
   - Redémarrez normalement
   - Votre système devrait être restauré

**Astuce :** En mode Live, vous pouvez aussi accéder à vos fichiers personnels pour les copier sur une clé USB avant restauration (par sécurité).

## Scénario 3 : Restauration depuis une image Clonezilla

### Situation

Votre disque dur est tombé en panne, ou vous voulez revenir à une image système complète créée précédemment.

### Prérequis

- Une image Clonezilla créée auparavant
- Un disque de destination (peut être le même après remplacement ou un nouveau)
- Clé USB Clonezilla bootable
- Patience (processus long)

### Procédure complète

**1. Préparation**

- Installez le nouveau disque dur (si remplacement)
- Branchez le disque contenant l'image Clonezilla
- Insérez la clé USB Clonezilla

**2. Démarrer sur Clonezilla**

- Redémarrez
- Accédez au menu de boot
- Sélectionnez la clé USB Clonezilla
- Attendez le chargement

**3. Configuration initiale Clonezilla**

- **Langue :** Sélectionnez votre langue
- **Clavier :** Choisissez "Ne pas modifier" ou votre clavier
- **Mode :** Sélectionnez **Start Clonezilla**

**4. Type de tâche**

- Sélectionnez **device-image** (restaurer depuis une image)
- Mode : **Beginner** (débutant)

**5. Montage de l'image**

- **local_dev** : Si image sur disque externe
- Clonezilla scanne les périphériques
- Sélectionnez le disque contenant l'image
- Appuyez sur **Entrée**

**6. Navigation vers l'image**

- Naviguez avec les flèches dans l'arborescence
- Trouvez le dossier contenant votre image
- Il devrait contenir des fichiers comme :
  - Partition-info
  - sda1.ext4-ptcl-img.gz.*
  - etc.
- Sélectionnez le dossier
- **Entrée** puis **Entrée** pour confirmer

**7. Type de restauration**

- Sélectionnez **restoredisk** (restaurer un disque entier)
- Ou **restoreparts** (restaurer des partitions spécifiques)

**8. Sélection de l'image**

- Clonezilla liste les images disponibles
- Sélectionnez celle à restaurer
- Le nom devrait être explicite (date, description)

**9. Disque de destination**

- **ATTENTION CRITIQUE :** Sélectionnez le BON disque !
- Toutes les données de ce disque seront EFFACÉES
- Vérifiez la taille, le nom
- Exemple : sda (500 GB)
- Appuyez sur **Entrée**

**10. Options avancées**

Pour débutants : acceptez les options par défaut
- Appuyez simplement sur **Entrée** à chaque fois

**11. Vérification**

- Clonezilla demande si vous voulez vérifier l'image avant restauration
- Recommandé : **Yes, check the image before restoring**
- Cela prend plus de temps mais évite les mauvaises surprises

**12. Action après restauration**

- Choisissez ce qui se passe après :
  - **Reboot** : Redémarrer
  - **Poweroff** : Éteindre
  - **Command prompt** : Ligne de commande
- Pour débutants : **Reboot**

**13. Confirmation**

- Clonezilla demande **deux fois** confirmation
- Lisez bien : **ALL DATA WILL BE OVERWRITTEN**
- Tapez **y** puis **Entrée**
- Puis tapez **y** à nouveau et **Entrée**

**14. Restauration en cours**

- Le processus démarre
- Barre de progression affichée
- **Durée :** 30 minutes à plusieurs heures selon :
  - Taille du disque
  - Vitesse des disques
  - Compression de l'image
- **NE DÉBRANCHEZ RIEN**
- **NE REDÉMARREZ PAS**

**15. Fin de restauration**

- Message : "The disk was successfully restored"
- Appuyez sur **Entrée**
- L'ordinateur redémarre (si vous avez choisi Reboot)

**16. Premier démarrage**

- Retirez la clé USB Clonezilla
- Le système démarre normalement
- Vous retrouvez votre système tel qu'au moment de l'image

**Vérifications post-restauration :**

```bash
# Vérifier les partitions
lsblk

# Vérifier l'espace disque
df -h

# Vérifier le boot
sudo update-grub
```

## Scénario 4 : Restauration complète après catastrophe

### Situation

Ordinateur volé, détruit, ou perte totale. Vous recommencez de zéro.

### Plan de reprise étape par étape

**Phase 1 : Nouveau matériel (Jour 1)**

1. **Acquisition**
   - Achetez un nouvel ordinateur ou disque dur
   - Ou récupérez un ordinateur de rechange

2. **Installation de base**
   - Si ordinateur vierge : installez Linux Mint
   - Suivez l'installation standard
   - Configuration initiale (utilisateur, réseau)

**Phase 2 : Récupération système (Jour 1-2)**

**Option A : Si vous avez une image Clonezilla**
- Suivez la procédure Clonezilla ci-dessus
- Temps : 2-6 heures
- Résultat : système identique restauré

**Option B : Sans image système**
- Réinstallez Linux Mint depuis zéro
- Installez les logiciels de base
- Temps : 3-5 heures
- Passez ensuite à la restauration des données

**Phase 3 : Restauration des données (Jour 2)**

**Depuis disque externe :**

1. **Connectez le disque de sauvegarde**
   - Disque externe qui était rangé hors site
   - Ou récupérez-le depuis le lieu de stockage

2. **Installez Backintime ou Déjà Dup**
   ```bash
   sudo apt install backintime-qt
   # ou
   sudo apt install deja-dup
   ```

3. **Restaurez vos données**
   - Ouvrez Backintime
   - Sélectionnez le disque de sauvegarde
   - Restaurez /home complet
   - Ou fichiers spécifiques

**Depuis le cloud :**

1. **Installez le client cloud**
   - Google Drive : installez Insync ou utilisez le web
   - Nextcloud : installez le client desktop
   - Dropbox, etc.

2. **Connectez votre compte**
   - Entrez vos identifiants
   - La synchronisation démarre automatiquement

3. **Attendez la synchronisation complète**
   - Peut prendre plusieurs heures pour beaucoup de données
   - Priorisez les fichiers essentiels

**Phase 4 : Reconfiguration (Jour 2-3)**

1. **Applications**
   - Réinstallez vos applications favorites
   - Liste dans votre documentation (vous l'avez créée, n'est-ce pas ?)
   - Ou parcourez le gestionnaire de logiciels

2. **Configuration**
   - Rétablissez vos configurations personnalisées
   - Thèmes, extensions, préférences
   - Si sauvegardées : restaurez .config, .local

3. **Comptes et connexions**
   - Reconnectez vos comptes emails
   - Services online (Spotify, etc.)
   - Gestionnaire de mots de passe

**Phase 5 : Vérification (Jour 3)**

1. **Testez tout**
   - Ouvrez vos documents importants
   - Vérifiez les photos
   - Testez les applications
   - Imprimante, scanner, périphériques

2. **Vérifiez l'intégrité**
   - Comparez la taille des dossiers restaurés
   - Spot-check : vérifiez aléatoirement des fichiers

3. **Mettez à jour**
   ```bash
   sudo apt update
   sudo apt upgrade
   ```

**Phase 6 : Nouvelle sauvegarde (Jour 3)**

1. **Configurez immédiatement les sauvegardes**
   - Timeshift : snapshots automatiques
   - Backintime : sauvegardes quotidiennes
   - Cloud : synchronisation continue

2. **Créez un snapshot manuel**
   - De ce nouveau système restauré
   - Comme point de départ

### Temps total estimé

- **Avec image Clonezilla** : 1-2 jours
- **Sans image, restauration données** : 2-3 jours
- **Restauration cloud seul** : 2-4 jours (selon taille/débit)

**Facteurs d'accélération :**
- Bonne documentation de votre système
- Sauvegardes bien organisées
- Connexion Internet rapide
- Automatisation des installations (scripts)

## Problèmes courants et solutions

### Problème 1 : "Timeshift ne trouve aucun snapshot"

**Causes possibles :**
- Snapshots sur un disque non monté
- Partition de sauvegarde non accessible
- Snapshots corrompus ou effacés

**Solutions :**

1. **Vérifiez le disque de sauvegarde**
   ```bash
   lsblk
   # Montez manuellement si nécessaire
   sudo mount /dev/sdb1 /mnt
   ```

2. **Vérifiez le dossier Timeshift**
   ```bash
   ls -la /run/timeshift/backup/timeshift/snapshots/
   ```

3. **Redémarrez Timeshift**
   - Fermez Timeshift
   - Rouvrez-le
   - Rescannez les périphériques

4. **En dernier recours**
   - Si snapshots perdus : restaurez depuis une autre sauvegarde
   - Leçon : importance de la règle 3-2-1 !

### Problème 2 : "Erreur lors de la restauration Timeshift"

**Message typique :** "rsync returned an error"

**Solutions :**

1. **Vérifiez l'espace disque**
   ```bash
   df -h
   # Libérez de l'espace si nécessaire
   ```

2. **Vérifiez les permissions**
   ```bash
   # Depuis un Live USB
   sudo chown -R root:root /mnt/restore_target
   ```

3. **Tentez une restauration partielle**
   - Décochez certains dossiers
   - Restaurez en plusieurs fois

4. **Utilisez le mode manuel**
   - Montez manuellement les partitions
   - Copiez manuellement avec rsync

### Problème 3 : "Le système restauré ne démarre pas"

**Symptômes :** Écran noir, erreur GRUB, ou boucle de redémarrage

**Solutions :**

**1. Réparer GRUB**

Depuis un Live USB :

```bash
# Montez votre partition système
sudo mount /dev/sda2 /mnt
sudo mount /dev/sda1 /mnt/boot/efi  # Si UEFI

# Montez les systèmes de fichiers nécessaires
sudo mount --bind /dev /mnt/dev
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys

# Chroot dans votre système
sudo chroot /mnt

# Réinstallez GRUB
grub-install /dev/sda  # BIOS
# ou
grub-install --target=x86_64-efi --efi-directory=/boot/efi  # UEFI

# Mettez à jour la configuration
update-grub

# Sortez et redémarrez
exit
sudo reboot
```

**2. Vérifiez le mode de boot (UEFI vs BIOS)**
- Entrez dans le BIOS/UEFI
- Vérifiez le mode de boot
- Changez si nécessaire pour correspondre à votre installation

**3. Vérifiez /etc/fstab**

Si restauration sur un disque différent :

```bash
# Vérifiez les UUIDs
sudo blkid

# Éditez fstab si nécessaire
sudo nano /etc/fstab
# Corrigez les UUIDs si ils ont changé
```

### Problème 4 : "Fichier restauré mais vide ou corrompu"

**Causes :**
- Sauvegarde elle-même corrompue
- Interruption pendant la sauvegarde originale
- Problème de disque

**Solutions :**

1. **Tentez une version antérieure**
   - Restaurez depuis un snapshot plus ancien
   - Vérifiez l'intégrité

2. **Vérifiez la sauvegarde**
   ```bash
   # Vérifiez l'intégrité des fichiers de sauvegarde
   sha256sum fichier_sauvegarde
   ```

3. **Utilisez des outils de récupération**
   ```bash
   # Pour ext4
   sudo apt install testdisk photorec
   sudo photorec
   ```

4. **Leçon pour l'avenir**
   - Vérifications régulières des sauvegardes
   - Sauvegardes multiples (3-2-1 !)
   - Tests de restauration périodiques

### Problème 5 : "Clonezilla : erreur 'No space left'"

**Cause :** Disque destination trop petit

**Solutions :**

1. **Vérifiez les tailles**
   - Le disque destination doit être ≥ disque source
   - Même si le source est peu rempli

2. **Réduisez les partitions source**
   - Avant de créer l'image
   - Avec GParted
   - Puis recréez l'image

3. **Utilisez un disque plus grand**
   - Parfois inévitable

4. **Mode expert : clonage proportionnel**
   - Clonezilla peut redimensionner à la volée
   - Mode expert requis

### Problème 6 : "Restauration cloud très lente"

**Causes :** Connexion Internet lente, beaucoup de données

**Solutions :**

1. **Priorisez**
   - Restaurez d'abord les fichiers essentiels
   - Utilisez le mode "fichiers à la demande" si disponible

2. **Synchronisation sélective**
   - Ne synchronisez pas tout immédiatement
   - Choisissez les dossiers importants d'abord

3. **Connexion filaire**
   - Utilisez Ethernet au lieu de WiFi
   - Plus stable et rapide

4. **Téléchargement direct**
   - Téléchargez l'archive complète depuis le web
   - Puis décompressez localement
   - Plus rapide pour gros volumes

### Problème 7 : "Permissions incorrectes après restauration"

**Symptômes :** Fichiers inaccessibles, "permission denied"

**Solutions :**

```bash
# Réparez les permissions de votre home
sudo chown -R $USER:$USER /home/$USER

# Permissions standards
chmod 755 /home/$USER
chmod 700 /home/$USER/.ssh
chmod 600 /home/$USER/.ssh/*

# Pour les dossiers
find /home/$USER -type d -exec chmod 755 {} \;

# Pour les fichiers
find /home/$USER -type f -exec chmod 644 {} \;
```

## Checklist post-restauration

Après toute restauration, vérifiez systématiquement :

### Vérifications immédiates

```
□ Le système démarre correctement
□ Connexion réseau fonctionne
□ Environnement de bureau s'affiche
□ Clavier et souris répondent
□ Son fonctionne
□ Affichage correct (résolution, multi-écran)
```

### Vérifications des données

```
□ Dossiers principaux présents (Documents, Images, etc.)
□ Fichiers récents accessibles
□ Fichiers importants s'ouvrent correctement
□ Taille des dossiers cohérente
□ Dates de modification préservées
□ Permissions correctes
```

### Vérifications système

```
□ Applications habituelles installées et fonctionnelles
□ Imprimante détectée et fonctionnelle
□ Périphériques USB reconnus
□ Connexions réseau (VPN, etc.) configurées
□ Comptes emails fonctionnent
□ Accès aux partages réseau OK
```

### Vérifications de sécurité

```
□ Mises à jour système disponibles installées
□ Pare-feu activé
□ Mots de passe changés si nécessaire (en cas de vol)
□ Connexions suspectes vérifiées
□ Antivirus (si utilisé) actif
```

### Configuration des nouvelles sauvegardes

```
□ Timeshift configuré et premier snapshot créé
□ Backintime/Déjà Dup configuré
□ Synchronisation cloud active
□ Test rapide de sauvegarde effectué
□ Calendrier de sauvegardes automatiques vérifié
```

## Bonnes pratiques de restauration

### Avant la restauration

**1. Évaluez la situation**
- Le problème est-il vraiment grave ?
- Une solution plus simple existe-t-elle ?
- Quelle sauvegarde est la plus appropriée ?

**2. Sauvegardez l'état actuel si possible**
- Même si système instable
- Copiez les fichiers récents sur clé USB
- Créez un snapshot Timeshift (si possible)

**3. Documentez**
- Notez ce qui ne va pas
- Quand le problème est apparu
- Quelle sauvegarde vous allez utiliser

**4. Préparez le matériel**
- Clés USB nécessaires
- Disques externes
- Connexion Internet stable

### Pendant la restauration

**1. Patience**
- Ne touchez à rien pendant le processus
- N'interrompez jamais une restauration
- Prévoyez du temps (pas en urgence)

**2. Alimentation**
- Ordinateur portable : branché sur secteur
- Onduleur si possible
- Évitez les coupures de courant

**3. Surveillance**
- Restez à proximité
- Vérifiez les messages d'erreur
- Notez tout comportement anormal

### Après la restauration

**1. Vérification méthodique**
- Suivez la checklist complète
- Ne pressez pas les vérifications
- Testez réellement, ne présumez pas

**2. Analyse de la cause**
- Qu'est-ce qui a causé le problème ?
- Comment l'éviter à l'avenir ?
- Faut-il modifier la stratégie de sauvegarde ?

**3. Documentation**
- Notez ce qui s'est passé
- Procédure suivie
- Problèmes rencontrés
- Solutions appliquées

**4. Améliorations**
- Ajustez vos sauvegardes si besoin
- Ajoutez des sauvegardes si la règle 3-2-1 n'était pas respectée
- Automatisez ce qui ne l'était pas

## Prévention : éviter d'avoir à restaurer

**Mieux vaut prévenir que guérir !**

### Mesures préventives système

1. **Mises à jour régulières mais prudentes**
   - Appliquez les mises à jour de sécurité
   - Attendez quelques jours pour les grosses mises à jour
   - Snapshot Timeshift avant chaque mise à jour majeure

2. **N'installez que des logiciels de confiance**
   - Dépôts officiels prioritairement
   - Vérifiez la réputation avant d'installer des PPA
   - Évitez les sources non fiables

3. **Sauvegardez AVANT toute manipulation**
   - Modification de partitions
   - Installation de pilotes
   - Modifications système importantes

### Mesures préventives données

1. **Réfléchissez avant de supprimer**
   - Vérifiez deux fois avant de vider la corbeille
   - Utilisez Shift+Suppr avec précaution
   - Archivez plutôt que supprimer si vous hésitez

2. **Organisez vos données**
   - Structure claire de dossiers
   - Nommage cohérent
   - Évite les suppressions accidentelles

3. **Versioning pour documents importants**
   - Numérotez les versions (document_v1, document_v2)
   - Ou utilisez Git pour le versioning automatique
   - Cloud avec historique activé

### Surveillance proactive

**Surveillez la santé du disque :**
```bash
# Installez smartmontools
sudo apt install smartmontools

# Vérifiez la santé
sudo smartctl -a /dev/sda | grep -i health
```

**Surveillez l'espace disque :**
```bash
# Vérifiez régulièrement
df -h

# Alerte automatique si <10%
df -h | awk '{if(NR>1)print $5,$6}' | grep -v media
```

**Vérifiez régulièrement les logs :**
```bash
# Erreurs récentes
sudo journalctl -p 3 -xb

# Problèmes disque
sudo dmesg | grep -i error
```

## En résumé

La restauration est la partie la plus importante de votre stratégie de sauvegarde :

### Points clés

**Préparez-vous :**
- Testez vos restaurations régulièrement
- Documentez les procédures
- Gardez les outils de récupération accessibles

**Connaissez vos options :**
- Restauration fichiers : Backintime, Déjà Dup, cloud
- Restauration système : Timeshift (rapide et simple)
- Restauration complète : Clonezilla (tout le disque)

**Soyez méthodique :**
- Évaluez la gravité du problème
- Choisissez la bonne méthode de restauration
- Suivez la procédure étape par étape
- Vérifiez complètement après restauration

**Gardez votre calme :**
- La panique mène aux erreurs
- Vous avez des sauvegardes (c'est pour ça !)
- Prenez le temps de faire les choses bien

### La meilleure restauration...

... est celle que vous n'avez jamais à faire !

**Prévention > Restauration**

Mais quand vous devez restaurer :
- Vous savez maintenant comment faire
- Vous avez les procédures
- Vous avez les sauvegardes
- Vous allez y arriver !

**Dernière recommandation :** Imprimez ou sauvegardez ce guide hors de votre ordinateur. Le jour où vous en aurez besoin, votre ordinateur pourrait ne pas démarrer !

Gardez précieusement :
- Ce guide de restauration
- Vos mots de passe de sauvegarde
- L'emplacement de vos sauvegardes
- Les contacts d'aide (forum, ami technicien)

Avec ces informations et vos sauvegardes, vous êtes paré pour faire face à n'importe quel problème !

⏭️ [Sauvegarde cloud automatisée](/17-sauvegarde-et-restauration/06-sauvegarde-cloud-automatisee.md)
