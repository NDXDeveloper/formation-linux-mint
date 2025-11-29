🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 12.4 Périphériques USB et Bluetooth

## Introduction

Les périphériques USB et Bluetooth sont omniprésents dans notre quotidien numérique : clés USB, disques durs externes, souris, claviers, casques audio, smartphones, etc. Linux Mint gère ces périphériques de manière **automatique et transparente** dans la grande majorité des cas.

Ce chapitre vous guide dans l'utilisation, la configuration et le dépannage de ces périphériques essentiels.

---

## Périphériques USB

### Comprendre l'USB

**USB** (Universal Serial Bus) est un standard de connexion qui permet de brancher une multitude de périphériques à votre ordinateur.

#### Les différentes versions USB

| Version | Nom commercial | Vitesse maximale | Année |
|---------|----------------|------------------|-------|
| USB 1.1 | USB | 12 Mb/s | 1998 |
| USB 2.0 | Hi-Speed USB | 480 Mb/s | 2000 |
| USB 3.0 | SuperSpeed USB | 5 Gb/s | 2008 |
| USB 3.1 | SuperSpeed USB 10Gbps | 10 Gb/s | 2013 |
| USB 3.2 | SuperSpeed USB 20Gbps | 20 Gb/s | 2017 |
| USB 4.0 | USB4 | 40 Gb/s | 2019 |

**Repères visuels :**
- **USB 2.0** : Connecteur noir à l'intérieur
- **USB 3.0/3.1** : Connecteur bleu à l'intérieur
- **USB 3.2** : Connecteur rouge ou bleu turquoise
- **USB-C** : Connecteur réversible ovale

#### Types de périphériques USB courants

**Périphériques de stockage :**
- Clés USB
- Disques durs externes
- SSD externes
- Cartes SD (via lecteur USB)

**Périphériques d'entrée :**
- Souris
- Claviers
- Tablettes graphiques
- Manettes de jeu (gamepads)
- Webcams

**Périphériques audio :**
- Casques et écouteurs USB
- Microphones
- Cartes son externes
- Interfaces audio

**Autres :**
- Imprimantes (voir chapitre 12.3)
- Smartphones et tablettes
- Adaptateurs réseau WiFi/Ethernet
- Hubs USB
- Lecteurs de cartes mémoire

---

## Utilisation des périphériques de stockage USB

### Brancher une clé USB ou un disque dur externe

La procédure est **extrêmement simple** sous Linux Mint :

1. **Branchez** le périphérique USB dans un port disponible
2. **Attendez 2-3 secondes** : le système détecte automatiquement le périphérique
3. Une **notification** apparaît : "Périphérique amovible inséré"
4. Le périphérique apparaît sur le **bureau** (icône)
5. Il apparaît également dans le **gestionnaire de fichiers** (Nemo) dans la barre latérale gauche

### Accéder au contenu

**Méthode 1 : Double-clic sur l'icône du bureau**
- Double-cliquez sur l'icône du périphérique
- Le gestionnaire de fichiers s'ouvre directement dans le périphérique

**Méthode 2 : Via le gestionnaire de fichiers**
1. Ouvrez **Nemo** (gestionnaire de fichiers)
2. Dans la barre latérale gauche, section "**Périphériques**"
3. Cliquez sur le nom de votre clé USB ou disque dur
4. Le contenu s'affiche

**Méthode 3 : Via le terminal**
```bash
# Lister les périphériques montés
df -h

# Ou voir tous les points de montage
lsblk

# Accéder au périphérique (généralement dans /media)
cd /media/$USER/NOM-DU-PERIPHERIQUE
```

### Copier des fichiers

Une fois le périphérique ouvert, vous pouvez :
- **Copier-coller** des fichiers comme d'habitude
- **Glisser-déposer** depuis/vers le périphérique
- Utiliser **Ctrl+C** / **Ctrl+V** pour copier-coller
- Utiliser **Ctrl+X** / **Ctrl+V** pour couper-coller (déplacer)

> **Important** : Les transferts de gros fichiers peuvent prendre du temps. Une barre de progression s'affiche pendant la copie.

### Éjecter proprement un périphérique USB

**⚠️ TRÈS IMPORTANT** : Ne débranchez **JAMAIS** un périphérique USB sans l'éjecter proprement !

**Pourquoi ?**
- Les données peuvent encore être en cours d'écriture
- Le cache du système n'est pas forcément vidé
- Risque de **corruption des données**
- Risque de **perte de fichiers**

#### Méthodes d'éjection sécurisée

**Méthode 1 : Clic droit sur l'icône du bureau**
1. Clic droit sur l'icône du périphérique
2. Sélectionnez "**Éjecter**" ou "**Retirer en toute sécurité**"
3. Attendez le message de confirmation
4. Vous pouvez maintenant débrancher physiquement le périphérique

**Méthode 2 : Dans le gestionnaire de fichiers**
1. Dans Nemo, à côté du nom du périphérique (barre latérale)
2. Cliquez sur l'**icône d'éjection** (⏏)
3. Attendez que l'icône disparaisse
4. Débranchez

**Méthode 3 : Via le terminal**
```bash
# Voir les périphériques montés
lsblk

# Démonter le périphérique (remplacez sdb1 par votre périphérique)
sudo umount /dev/sdb1

# Ou éjecter directement
sudo eject /dev/sdb
```

**Indicateur que l'éjection est terminée :**
- L'icône disparaît du bureau
- Le périphérique disparaît de la barre latérale de Nemo
- Le message "Vous pouvez maintenant retirer le périphérique" s'affiche
- Sur certaines clés USB, le voyant LED cesse de clignoter

---

## Formatage de périphériques USB

### Pourquoi formater ?

Vous pouvez avoir besoin de formater un périphérique pour :
- **Effacer tout son contenu** rapidement
- **Changer le système de fichiers** (FAT32 → exFAT → ext4)
- **Résoudre des problèmes** de corruption
- **Préparer un périphérique** pour un usage spécifique
- **Créer une clé USB bootable**

### Les systèmes de fichiers

Choisir le bon système de fichiers est important :

#### FAT32 (File Allocation Table 32)
**Avantages :**
- ✅ Compatible avec **tous les systèmes** : Windows, macOS, Linux, consoles de jeu, TV
- ✅ Parfait pour clés USB de partage

**Inconvénients :**
- ❌ **Limite de 4 Go par fichier** (problématique pour vidéos HD, images ISO)
- ❌ Pas de permissions de fichiers avancées

**Usage recommandé :** Clés USB pour échange de documents entre différents systèmes

#### exFAT (Extended File Allocation Table)
**Avantages :**
- ✅ Compatible Windows, macOS, Linux moderne
- ✅ **Pas de limite de taille de fichier**
- ✅ Optimisé pour mémoire flash

**Inconvénients :**
- ❌ Moins compatible que FAT32 (anciennes consoles, TV, etc.)

**Usage recommandé :** Clés USB et disques externes pour gros fichiers (films, ISOs, sauvegardes)

#### NTFS (New Technology File System - Windows)
**Avantages :**
- ✅ Permissions et sécurité
- ✅ Journalisation (protection contre corruptions)
- ✅ Pas de limite de taille de fichier

**Inconvénients :**
- ❌ Propriétaire Microsoft
- ❌ Support Linux nécessite des paquets supplémentaires
- ❌ macOS ne peut qu'écrire avec logiciel tiers

**Usage recommandé :** Disques durs externes principalement utilisés avec Windows

#### ext4 (Fourth Extended Filesystem - Linux)
**Avantages :**
- ✅ Natif Linux, **performances maximales**
- ✅ Journalisation robuste
- ✅ Permissions Unix complètes
- ✅ Très stable et fiable

**Inconvénients :**
- ❌ **Non lisible par Windows** sans logiciel tiers
- ❌ Non lisible par macOS

**Usage recommandé :** Disques durs externes utilisés **uniquement avec Linux**

#### Btrfs (B-Tree Filesystem)
**Avantages :**
- ✅ Système de fichiers moderne
- ✅ Snapshots, compression
- ✅ Détection et correction d'erreurs

**Inconvénients :**
- ❌ Plus complexe
- ❌ Non compatible Windows/macOS

**Usage recommandé :** Utilisateurs avancés Linux, serveurs NAS

### Formater avec l'outil Disques

**Disques** est l'outil graphique de gestion de disques de Linux Mint.

**Accès :** Menu → Accessoires → **Disques**

#### Procédure de formatage

1. **Ouvrez Disques**
2. Dans la liste de gauche, sélectionnez votre **périphérique USB**
   - ⚠️ **Vérifiez bien** le nom et la taille pour ne pas vous tromper !
3. Cliquez sur l'**icône d'engrenage** (⚙) ou le menu "**…**"
4. Sélectionnez "**Formater la partition**" ou "**Formater le disque**"

**Options de formatage :**

- **Nom du volume** : Donnez un nom à votre périphérique (ex: "MaClé", "Backup2024")
- **Type** : Choisissez le système de fichiers :
  - **FAT** pour compatibilité universelle
  - **Ext4** pour usage Linux uniquement
  - **NTFS** pour usage Windows principalement
  - **exFAT** pour gros fichiers multi-plateformes
- **Effacement** :
  - **Rapide** : Supprime uniquement l'index (recommandé)
  - **Complet** : Écrase toutes les données (plus sécurisé mais long)

5. Cliquez sur "**Formater**"
6. **Confirmez** (attention, toutes les données seront perdues !)
7. Attendez la fin du processus
8. Votre périphérique est prêt à l'emploi !

### Formater en ligne de commande

Pour les utilisateurs avancés :

```bash
# ⚠️ DANGER : Vérifiez ABSOLUMENT le bon périphérique !
# Lister les périphériques
lsblk

# Démonter le périphérique (remplacez sdb1)
sudo umount /dev/sdb1

# Formater en ext4
sudo mkfs.ext4 /dev/sdb1

# Formater en FAT32
sudo mkfs.vfat -F 32 /dev/sdb1

# Formater en exFAT (installer d'abord exfat-utils)
sudo apt install exfat-fuse exfat-utils
sudo mkfs.exfat /dev/sdb1

# Formater en NTFS
sudo mkfs.ntfs /dev/sdb1

# Donner un nom au volume
sudo e2label /dev/sdb1 "MonNom"  # Pour ext4
sudo fatlabel /dev/sdb1 "MonNom"  # Pour FAT32
```

---

## Gestion des permissions sur périphériques USB

### Problème de permissions en lecture seule

Parfois, un périphérique USB peut être monté en **lecture seule** (read-only), vous empêchant d'y écrire.

#### Causes courantes

1. **Verrou physique** : Certaines clés USB ont un interrupteur de protection en écriture
2. **Système de fichiers corrompu** : Erreurs de démontage précédent
3. **Périphérique NTFS mal démonté** sous Windows

#### Solutions

**Vérification de la protection physique :**
- Inspectez la clé USB pour un petit interrupteur
- Déplacez-le en position "déverrouillée"

**Remonter en lecture-écriture :**
```bash
# Identifier le périphérique
lsblk

# Démonter
sudo umount /dev/sdb1

# Remonter en lecture-écriture
sudo mount -o rw,remount /dev/sdb1
```

**Réparer un système de fichiers NTFS :**
```bash
# Installer ntfs-3g si ce n'est pas déjà fait
sudo apt install ntfs-3g

# Réparer
sudo ntfsfix /dev/sdb1

# Remonter
sudo mount /dev/sdb1
```

**Réparer un système FAT32/exFAT :**
```bash
# Pour FAT32
sudo fsck.vfat -a /dev/sdb1

# Pour exFAT
sudo fsck.exfat /dev/sdb1
```

### Changer les permissions de fichiers

Sur un périphérique ext4 (Linux), vous pouvez modifier les permissions :

```bash
# Rendre tous les fichiers accessibles
sudo chmod -R 755 /media/$USER/MaClé/

# Changer le propriétaire
sudo chown -R $USER:$USER /media/$USER/MaClé/
```

> **Note** : Ces commandes ne fonctionnent que sur des systèmes de fichiers Linux (ext4, Btrfs). FAT32 et NTFS ne supportent pas les permissions Unix.

---

## Périphériques d'entrée USB

### Souris et claviers USB

**Plug & Play total :**
- Branchez la souris ou le clavier
- Ils fonctionnent **immédiatement**
- Aucune configuration nécessaire dans 99% des cas

#### Souris avec boutons supplémentaires

Pour configurer des boutons supplémentaires :

**Installation de Piper (pour souris gaming) :**
```bash
sudo apt install piper
```

**Accès :** Menu → Préférences → Piper

**Fonctionnalités :**
- Configuration des boutons
- Réglage de la sensibilité (DPI)
- Création de profils
- Gestion des LED (souris RGB)

#### Claviers avec touches multimédia

La plupart des touches multimédia fonctionnent automatiquement :
- Volume +/-
- Lecture/Pause
- Piste suivante/précédente
- Luminosité

**Si certaines touches ne fonctionnent pas :**

1. Ouvrez **Menu** → **Préférences** → **Raccourcis clavier**
2. Recherchez la fonction souhaitée
3. Cliquez sur le raccourci
4. Appuyez sur la touche de votre clavier
5. La liaison est créée

### Webcams USB

**Détection automatique :**
- Branchez la webcam
- Elle est détectée instantanément

**Tester la webcam :**

**Application Cheese :**
```bash
# Installer Cheese
sudo apt install cheese

# Lancer
cheese
```

**Avec un navigateur web :**
- Allez sur un site de test webcam (ex: webcamtests.com)
- Autorisez l'accès à la caméra
- Vérifiez le fonctionnement

**Vérifier la détection en ligne de commande :**
```bash
# Lister les périphériques vidéo
ls -l /dev/video*

# Informations détaillées
v4l2-ctl --list-devices
```

### Manettes de jeu (Gamepads)

**Compatibilité excellente :**
- Xbox 360/One/Series : Support natif parfait
- PlayStation 3/4/5 : Excellent support
- Nintendo Switch Pro : Bon support
- Génériques : Variables

**Vérifier la détection :**
```bash
# Lister les périphériques d'entrée
ls /dev/input/js*

# Tester avec jstest (installer jstest-gtk)
sudo apt install joystick jstest-gtk
jstest-gtk
```

**Configuration avancée :**

Pour mapper les boutons :
```bash
# Installer antimicrox
sudo apt install antimicrox
```

Antimicrox permet de :
- Mapper des boutons de manette vers des touches clavier
- Créer des profils par jeu
- Configurer la sensibilité des sticks

---

## Bluetooth sous Linux Mint

### Comprendre le Bluetooth

**Bluetooth** est une technologie de communication sans fil à courte portée (environ 10 mètres) utilisée pour :
- Souris et claviers sans fil
- Casques et écouteurs audio
- Enceintes portables
- Smartphones et tablettes
- Montres connectées
- Manettes de jeu

**Versions Bluetooth courantes :**
- **Bluetooth 4.0** : Économie d'énergie (BLE)
- **Bluetooth 5.0** : Portée étendue, vitesse doublée
- **Bluetooth 5.2** : Audio LE, basse latence

### Vérifier la présence du Bluetooth

**Méthode graphique :**
- Regardez la **barre de tâches** : y a-t-il une icône Bluetooth ?
- Si non, votre ordinateur n'a peut-être pas de Bluetooth intégré

**Méthode en ligne de commande :**
```bash
# Vérifier si le Bluetooth est présent
hciconfig

# Ou avec bluetoothctl
bluetoothctl show

# Lister les contrôleurs Bluetooth
sudo lsusb | grep -i bluetooth
sudo lspci | grep -i bluetooth
```

**Si vous n'avez pas de Bluetooth :**
- Vous pouvez acheter un **adaptateur USB Bluetooth** (10-20€)
- Branchez-le et il fonctionnera automatiquement sous Linux Mint

### Activer/Désactiver le Bluetooth

**Via l'interface graphique :**

1. Cliquez sur l'**icône Bluetooth** dans la barre de tâches
2. Sélectionnez "**Activer Bluetooth**" ou "**Désactiver Bluetooth**"

**Ou dans les paramètres système :**
1. Menu → Préférences → **Bluetooth**
2. Basculez l'interrupteur sur "**Activé**" ou "**Désactivé**"

**Via le terminal :**
```bash
# Activer le Bluetooth
sudo systemctl start bluetooth
rfkill unblock bluetooth

# Désactiver
sudo systemctl stop bluetooth
rfkill block bluetooth

# Redémarrer le service
sudo systemctl restart bluetooth
```

### Rendre l'ordinateur détectable

Pour appairer un nouveau périphérique, votre ordinateur doit être **visible** :

1. Ouvrez **Bluetooth** dans les paramètres
2. L'ordinateur devient automatiquement détectable pour quelques minutes
3. Vous verrez "**Visible**" ou "**Découvrable**" dans l'interface

> **Note** : Par sécurité, l'ordinateur n'est détectable que temporairement.

---

## Appairer des périphériques Bluetooth

### Procédure générale d'appairage

L'appairage (pairing) est le processus de liaison entre votre ordinateur et un périphérique Bluetooth.

#### Étape 1 : Préparer le périphérique

1. **Allumez** le périphérique Bluetooth
2. Mettez-le en **mode appairage** (pairing mode)
   - Généralement : maintenir le bouton d'alimentation 3-5 secondes
   - Une LED clignote rapidement (souvent bleu)
   - Consultez le manuel du périphérique pour la procédure exacte

#### Étape 2 : Démarrer l'appairage sur Linux Mint

1. Ouvrez **Menu** → **Préférences** → **Bluetooth**
2. Assurez-vous que Bluetooth est **activé**
3. Cliquez sur le bouton "**+**" ou "**Rechercher des appareils**"
4. Le système recherche les périphériques à proximité

#### Étape 3 : Sélectionner et appairer

1. Votre périphérique apparaît dans la liste
2. Cliquez sur son nom
3. Cliquez sur "**Appairer**" ou "**Connecter**"
4. Si demandé, entrez un **code PIN** :
   - Souvent : `0000` ou `1234`
   - Ou consultez le manuel du périphérique
5. La connexion s'établit
6. Le périphérique est maintenant **appairé** et se connectera automatiquement à l'avenir

### Appairer des périphériques spécifiques

#### Casque ou écouteurs Bluetooth

**Procédure :**
1. Mettez le casque en **mode appairage**
   - Souvent : maintenir le bouton pendant 5 secondes
   - LED clignote bleu et rouge alternativement
2. Dans Bluetooth, recherchez des appareils
3. Sélectionnez votre casque
4. Appairez

**Après l'appairage :**
- Le son est automatiquement routé vers le casque Bluetooth
- Pour revenir aux haut-parleurs : désactivez le Bluetooth ou déconnectez le casque

**Basculer entre périphériques audio :**
1. Clic droit sur l'**icône de son** (barre de tâches)
2. Sélectionnez "**Paramètres du son**"
3. Onglet "**Sortie**"
4. Choisissez le périphérique souhaité

#### Souris Bluetooth

**Avantage :** Pas de dongle USB, connexion directe au Bluetooth intégré

**Procédure :**
1. Allumez la souris
2. Appuyez sur le bouton d'appairage (souvent sous la souris)
3. Dans Bluetooth, recherchez et appairez
4. La souris fonctionne immédiatement

**Note :** Certaines souris Bluetooth peuvent avoir une latence légèrement supérieure aux souris sans fil USB 2.4GHz.

#### Clavier Bluetooth

**Procédure similaire :**
1. Mode appairage du clavier
2. Recherche et appairage
3. **Code PIN parfois nécessaire** : tapez-le sur le clavier Bluetooth puis Entrée

#### Smartphone ou tablette

**Transfert de fichiers via Bluetooth :**

1. **Sur le smartphone** :
   - Activez Bluetooth
   - Rendez le téléphone détectable
2. **Sur Linux Mint** :
   - Appairez avec le téléphone
   - Une fois appairé, vous pouvez envoyer/recevoir des fichiers
3. **Envoyer un fichier** :
   - Clic droit sur le fichier → "**Envoyer vers**" → Bluetooth
   - Sélectionnez le smartphone
   - Acceptez sur le téléphone
4. **Recevoir un fichier** :
   - Envoyez depuis le smartphone
   - Acceptez sur l'ordinateur
   - Le fichier arrive dans `~/Téléchargements/` ou `~/Documents/`

> **Astuce moderne :** Pour un transfert plus facile, utilisez plutôt **Warpinator** (outil Linux Mint pour transfert via WiFi) ou des services cloud.

#### Enceinte Bluetooth

**Procédure :**
1. Allumez l'enceinte
2. Mode appairage (bouton Bluetooth)
3. Appairage dans Linux Mint
4. Le son de l'ordinateur sort par l'enceinte

**Qualité audio :**
- Codecs supportés : SBC, AAC, aptX (selon matériel)
- Latence variable (peut être notable pour vidéos)

---

## Gestion des périphériques Bluetooth appairés

### Voir les périphériques appairés

**Interface graphique :**
1. Menu → Préférences → **Bluetooth**
2. Tous les périphériques appairés sont listés
3. Statut : **Connecté** ou **Déconnecté**

### Connecter/Déconnecter

**Pour se connecter à un périphérique déjà appairé :**
1. Dans Bluetooth, cliquez sur le périphérique
2. Cliquez sur "**Connecter**"

**Pour se déconnecter :**
1. Cliquez sur le périphérique connecté
2. Cliquez sur "**Déconnecter**"

**Connexion automatique :**
La plupart des périphériques (casques, souris) se connectent **automatiquement** quand ils sont allumés et que le Bluetooth de l'ordinateur est actif.

### Supprimer un appairage

Pour oublier un périphérique :
1. Dans Bluetooth, cliquez sur le périphérique
2. Cliquez sur "**Supprimer**" ou icône de **corbeille**
3. Le périphérique est oublié
4. Pour le réutiliser, vous devrez le ré-appairer

### Renommer un périphérique

Pour donner un nom plus clair :
1. Clic droit sur le périphérique
2. "**Propriétés**" ou "**Renommer**"
3. Entrez le nouveau nom

---

## Problèmes Bluetooth courants

### Le Bluetooth ne s'active pas

**Vérifications :**

1. **Vérifiez rfkill** :
```bash
rfkill list
```
Si Bluetooth est "blocked", débloquez-le :
```bash
sudo rfkill unblock bluetooth
```

2. **Redémarrez le service Bluetooth** :
```bash
sudo systemctl restart bluetooth
```

3. **Vérifiez que le module du noyau est chargé** :
```bash
lsmod | grep bluetooth
```
Si rien n'apparaît :
```bash
sudo modprobe bluetooth
sudo modprobe btusb
```

4. **Réinstallez les paquets Bluetooth** :
```bash
sudo apt install --reinstall bluez bluez-tools
```

### Périphérique non détecté

**Solutions :**

1. **Assurez-vous que le périphérique est en mode appairage**
   - LED clignotante
   - Consultez le manuel

2. **Rapprochez le périphérique** (moins de 1 mètre)

3. **Redémarrez le Bluetooth** :
```bash
sudo systemctl restart bluetooth
```

4. **Réinitialisez le contrôleur Bluetooth** :
```bash
sudo hciconfig hci0 down
sudo hciconfig hci0 up
```

5. **Utilisez bluetoothctl (outil en ligne de commande)** :
```bash
bluetoothctl
# Dans bluetoothctl :
power on
agent on
scan on
# Attendez que votre périphérique apparaisse
pair XX:XX:XX:XX:XX:XX  # Remplacez par l'adresse MAC
connect XX:XX:XX:XX:XX:XX
quit
```

### Appairage échoue ou demande un PIN inconnu

**Solutions :**

1. **Essayez les PINs courants** :
   - `0000`
   - `1234`
   - `9999`

2. **Consultez le manuel** du périphérique

3. **Supprimez l'ancien appairage** :
   - Supprimez le périphérique des deux côtés (ordinateur et périphérique)
   - Réinitialisez le périphérique Bluetooth (voir manuel)
   - Recommencez l'appairage

4. **Désactivez l'authentification SSP** (Secure Simple Pairing) :
```bash
sudo nano /etc/bluetooth/main.conf
```
Ajoutez ou modifiez :
```
[General]
Disable=Headset
```
Redémarrez Bluetooth.

### Connexion instable ou déconnexions fréquentes

**Causes possibles :**
- Interférences (WiFi, micro-ondes, autres Bluetooth)
- Batterie faible du périphérique
- Distance trop grande
- Obstacles (murs épais)

**Solutions :**

1. **Rapprochez le périphérique**

2. **Désactivez le WiFi temporairement** (test) :
   - WiFi et Bluetooth utilisent la bande 2.4GHz
   - Peuvent interférer

3. **Rechargez le périphérique**

4. **Désactivez la gestion d'énergie Bluetooth** :
```bash
sudo nano /etc/bluetooth/main.conf
```
Ajoutez :
```
[General]
FastConnectable = true
```

5. **Désactivez l'économie d'énergie USB** :
```bash
# Identifier le périphérique Bluetooth USB
lsusb

# Désactiver autosuspend pour Bluetooth
echo 'ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="XXXX", ATTR{idProduct}=="YYYY", ATTR{power/autosuspend}="-1"' | sudo tee /etc/udev/rules.d/50-bluetooth.rules
```

### Pas de son avec casque Bluetooth

**Solutions :**

1. **Vérifiez le profil audio** :
```bash
pactl list cards
```
Recherchez votre casque et notez les profils disponibles.

2. **Basculez vers le profil A2DP** (haute qualité) :
   - Ouvrez **Paramètres du son**
   - Onglet "**Configuration**"
   - Sélectionnez le profil "**High Fidelity Playback (A2DP Sink)**"

3. **Installez PulseAudio Bluetooth** :
```bash
sudo apt install pulseaudio-module-bluetooth
pulseaudio -k  # Redémarre PulseAudio
```

4. **Redémarrez PipeWire** (Linux Mint récent) :
```bash
systemctl --user restart pipewire pipewire-pulse
```

### Latence audio Bluetooth

**Problème :** Décalage entre l'image et le son en vidéo

**Solutions :**

1. **Activez le codec aptX** (si supporté) :
   - Meilleure qualité et latence réduite
   - Nécessite support matériel

2. **Utilisez des écouteurs gaming Bluetooth** :
   - Optimisés pour faible latence

3. **Alternative** : Utilisez un casque filaire pour regarder des vidéos

---

## Gestion avancée des périphériques

### Voir tous les périphériques connectés

```bash
# Périphériques USB
lsusb

# Périphériques USB avec arborescence
lsusb -t

# Informations détaillées sur un périphérique
lsusb -v -d XXXX:YYYY  # ID vendeur:produit

# Périphériques blocs (disques)
lsblk

# Tous les périphériques avec détails
sudo lshw -short

# Périphériques d'entrée
ls /dev/input/
cat /proc/bus/input/devices
```

### Gestion de l'énergie des périphériques USB

Pour économiser la batterie (portables) :

**Activer l'économie d'énergie USB** :
```bash
# Voir le statut actuel
cat /sys/bus/usb/devices/*/power/autosuspend

# Activer pour tous (temporaire)
sudo sh -c 'for i in /sys/bus/usb/devices/*/power/autosuspend; do echo 2 > $i; done'
```

**Désactiver pour un périphérique spécifique** (évite déconnexions) :
```bash
# Trouver l'ID du périphérique
lsusb

# Désactiver autosuspend
echo -1 | sudo tee /sys/bus/usb/devices/X-X/power/autosuspend
```

### Règles udev personnalisées

Pour automatiser des actions lors de connexion d'un périphérique :

**Exemple : Monter automatiquement une clé USB spécifique :**

```bash
# Créer une règle udev
sudo nano /etc/udev/rules.d/99-usb-custom.rules
```

Contenu :
```
# Identifier par ID vendeur et produit
ACTION=="add", ATTRS{idVendor}=="XXXX", ATTRS{idProduct}=="YYYY", RUN+="/chemin/vers/script.sh"
```

Rechargez les règles :
```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

---

## Sécurité et bonnes pratiques

### Sécurité USB

**Risques :**
- **Clés USB infectées** (malwares)
- **BadUSB** : périphériques malveillants se faisant passer pour claviers
- **Perte de données** par débranchement non sécurisé

**Bonnes pratiques :**

1. ✅ **Toujours éjecter** avant de débrancher
2. ✅ **Scanner** les clés USB inconnues avec ClamAV
3. ✅ **Désactiver l'auto-exécution** (déjà désactivé par défaut sur Linux)
4. ✅ **Chiffrer** les données sensibles (VeraCrypt, LUKS)
5. ❌ **Ne branchez jamais** des clés USB trouvées ou d'origine douteuse
6. ❌ **Évitez** les stations de recharge USB publiques (juice jacking)

### Sécurité Bluetooth

**Risques :**
- **Bluejacking** : Envoi de messages non sollicités
- **Bluesnarfing** : Vol de données
- **Eavesdropping** : Interception de communications

**Bonnes pratiques :**

1. ✅ **Désactivez Bluetooth** quand vous ne l'utilisez pas
2. ✅ **Ne restez pas en mode détectable** en permanence
3. ✅ **Supprimez** les appairages non utilisés
4. ✅ **Refusez** les demandes d'appairage inconnues
5. ✅ **Utilisez des PINs complexes** quand possible
6. ❌ **N'acceptez jamais** de fichiers de sources inconnues

### Protection des données sur périphériques amovibles

**Chiffrement avec LUKS (Linux Unified Key Setup) :**

```bash
# Installer cryptsetup
sudo apt install cryptsetup

# Chiffrer un périphérique (⚠️ EFFACE TOUTES LES DONNÉES)
sudo cryptsetup luksFormat /dev/sdb1

# Ouvrir le périphérique chiffré
sudo cryptsetup luksOpen /dev/sdb1 ma_cle_usb

# Formater
sudo mkfs.ext4 /dev/mapper/ma_cle_usb

# Monter
sudo mount /dev/mapper/ma_cle_usb /mnt

# Démonter et fermer
sudo umount /mnt
sudo cryptsetup luksClose ma_cle_usb
```

**Alternative : VeraCrypt (compatible Windows/macOS/Linux)**

```bash
# Installer VeraCrypt
sudo add-apt-repository ppa:unit193/encryption
sudo apt update
sudo apt install veracrypt
```

Voir chapitre 11.4 pour plus de détails sur le chiffrement.

---

## Optimisation et performance

### Vitesse de transfert USB

**Maximiser la vitesse :**

1. **Utilisez des ports USB 3.0+** (bleus) pour les transferts volumineux
2. **Formatez en exFAT ou ext4** (plus rapides que FAT32 pour gros fichiers)
3. **Activez le write-back caching** :
```bash
# Vérifier le mode actuel
sudo hdparm -W /dev/sdb

# Activer le cache en écriture
sudo hdparm -W1 /dev/sdb
```

4. **Copiez de gros fichiers** en une fois plutôt que beaucoup de petits

**Benchmark de vitesse :**
```bash
# Vitesse de lecture
sudo hdparm -t /dev/sdb

# Avec dd (attention, écrit sur le périphérique !)
dd if=/dev/zero of=/media/$USER/MaClé/test bs=1M count=1000 oflag=direct
```

### Résoudre les problèmes de lenteur

**Si le transfert est anormalement lent :**

1. **Vérifiez que vous utilisez USB 3.0** :
```bash
lsusb -t
# Cherchez "5000M" pour USB 3.0, "480M" pour USB 2.0
```

2. **Testez un autre port USB**

3. **Vérifiez l'état du périphérique** :
```bash
sudo smartctl -a /dev/sdb  # Nécessite smartmontools
```

4. **Défragmentez** (seulement NTFS) :
   - Branchez sur Windows
   - Défragmentez avec l'outil Windows

---

## Dépannage avancé

### Périphérique USB non reconnu

**Diagnostic complet :**

```bash
# Messages du noyau (erreurs récentes)
sudo dmesg | tail -50

# Informations détaillées USB
sudo lsusb -v

# Vérifier les erreurs de montage
sudo tail /var/log/syslog
```

**Solutions :**

1. **Testez sur un autre port USB**
2. **Testez sur un autre ordinateur** (vérifier si le périphérique fonctionne)
3. **Mettez à jour le noyau Linux** (peut résoudre problèmes de compatibilité)
4. **Réinitialisez le bus USB** :
```bash
# Recharger les modules USB
sudo modprobe -r usb_storage && sudo modprobe usb_storage
```

### Réinitialiser un périphérique USB sans redémarrer

```bash
# Lister les périphériques USB
lsusb

# Noter le bus et le device (ex: Bus 002 Device 004)
# Réinitialiser
sudo usbreset 002/004  # Format: bus/device
```

Ou :
```bash
echo '2-1' | sudo tee /sys/bus/usb/drivers/usb/unbind
echo '2-1' | sudo tee /sys/bus/usb/drivers/usb/bind
```

---

## Ressources et outils utiles

### Applications graphiques

**Pour USB :**
- **Disques** (Gnome Disks) : Gestion complète des disques
- **GParted** : Partitionnement avancé
- **Brasero** : Gravure CD/DVD
- **VeraCrypt** : Chiffrement

**Pour Bluetooth :**
- **Blueman** : Gestionnaire Bluetooth alternatif
```bash
sudo apt install blueman
```

### Commandes de diagnostic

```bash
# USB
lsusb                    # Lister périphériques USB
usb-devices              # Infos détaillées
dmesg | grep -i usb      # Messages du noyau USB

# Bluetooth
hciconfig                # Configuration Bluetooth
hcitool scan             # Scanner périphériques
bluetoothctl             # Interface de gestion complète

# Montage
mount                    # Voir tous les points de montage
df -h                    # Espace disque
lsblk                    # Arborescence des disques

# Général
sudo lshw                # Tout le matériel
inxi -Fxz                # Vue d'ensemble système
```

---

## Conclusion

La gestion des périphériques USB et Bluetooth sous Linux Mint est **simple et efficace**. La majorité des périphériques fonctionnent **immédiatement** sans configuration.

**Points clés à retenir :**

✅ **USB :**
- Branchez et utilisez (plug & play)
- **Éjectez toujours proprement** avant de débrancher
- Choisissez le bon système de fichiers selon l'usage
- Linux gère excellemment les périphériques de stockage

✅ **Bluetooth :**
- Activation simple et rapide
- Appairage intuitif via l'interface graphique
- Connexion automatique des périphériques connus
- Excellente compatibilité avec la plupart des périphériques

✅ **Sécurité :**
- Méfiez-vous des périphériques inconnus
- Chiffrez les données sensibles
- Désactivez Bluetooth quand non utilisé

Avec ces connaissances, vous maîtrisez parfaitement l'utilisation des périphériques USB et Bluetooth sous Linux Mint !

Dans le prochain chapitre, nous aborderons la **gestion de l'énergie et de la batterie**, particulièrement important pour les ordinateurs portables.

⏭️ [Gestion de l'énergie et batterie (laptop)](/12-materiel-et-pilotes/05-gestion-de-lenergie-et-batterie.md)
