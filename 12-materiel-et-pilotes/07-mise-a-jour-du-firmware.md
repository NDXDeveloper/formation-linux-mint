🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 12.7 Mise à jour du firmware (fwupd, UEFI/BIOS)

## Introduction

Le **firmware** est un logiciel de bas niveau intégré directement dans vos composants matériels. Contrairement aux pilotes qui font partie du système d'exploitation, le firmware est **gravé dans le matériel** lui-même et contrôle son fonctionnement fondamental.

Les mises à jour de firmware peuvent :
- ✅ **Corriger des bugs** critiques
- ✅ **Améliorer les performances**
- ✅ **Ajouter de nouvelles fonctionnalités**
- ✅ **Combler des failles de sécurité** (très important !)
- ✅ **Améliorer la compatibilité** avec de nouveaux systèmes

Ce chapitre vous guide dans la mise à jour sécurisée du firmware sous Linux Mint.

---

## Comprendre le firmware

### Qu'est-ce que le firmware ?

**Définition simple :**
Le firmware est un **programme permanent** stocké dans une puce mémoire de votre matériel.

**Analogie :**
- Le **système d'exploitation** (Linux Mint) = le cerveau qui pense
- Les **pilotes** = les nerfs qui transmettent les ordres
- Le **firmware** = les réflexes programmés dans les muscles

### Types de firmware dans votre ordinateur

#### 1. BIOS/UEFI (Firmware de la carte mère)

**Rôle :**
- Premier logiciel exécuté au démarrage
- Initialise le matériel
- Lance le système d'exploitation
- Gère les paramètres système de base

**Noms :**
- **BIOS** (Basic Input/Output System) : Ancienne technologie (pré-2010)
- **UEFI** (Unified Extensible Firmware Interface) : Technologie moderne

**Importance :**
- Le plus critique de tous les firmwares
- Une mauvaise mise à jour peut **rendre l'ordinateur inutilisable**

#### 2. Firmware de périphériques

**Composants concernés :**
- **SSD/Disques durs** : Contrôleur de stockage
- **Carte graphique** : GPU, VBIOS
- **Carte réseau** : WiFi, Ethernet, Bluetooth
- **Webcam** : Capteur, processeur d'image
- **Touchpad** : Contrôleur tactile
- **Batterie** : Contrôleur de charge (laptops)
- **Clavier/Souris** : Microcontrôleur
- **Dock/Hub USB** : Contrôleur de ports
- **Carte son** : DSP audio

**Importance :**
- Généralement plus sûr à mettre à jour que le BIOS
- Risque limité au composant spécifique

#### 3. Firmware embarqué (Embedded Controller)

**Rôle :**
- Gère les fonctions de bas niveau (laptops)
- Ventilateurs
- Indicateurs LED
- Touches de fonction (Fn)
- Capteurs de température

### Pourquoi mettre à jour le firmware ?

#### Raisons de sécurité (prioritaire)

**Vulnérabilités matérielles :**
- **Spectre/Meltdown** : Failles CPU nécessitant mise à jour microcode
- **Thunderspy** : Failles Thunderbolt
- **Failles WiFi** : KRACK, FragAttacks
- **Failles Bluetooth** : BlueBorne

**Ces vulnérabilités permettent :**
- Vol de données
- Prise de contrôle du système
- Espionnage

**Une mise à jour firmware peut être le seul correctif possible !**

#### Raisons fonctionnelles

**Bugs corrigés :**
- Plantages aléatoires
- Problèmes de veille/réveil
- Mauvaise gestion de la batterie
- Incompatibilités matérielles

**Nouvelles fonctionnalités :**
- Support de nouveaux processeurs (BIOS)
- Amélioration des performances
- Support de nouveaux standards (USB4, PCIe 5.0)

**Exemple concret :**
Un SSD Samsung peut voir ses **performances d'écriture doublées** après une mise à jour firmware.

---

## fwupd : L'outil de mise à jour de firmware sous Linux

### Qu'est-ce que fwupd ?

**fwupd** (Firmware Update Daemon) est un projet qui permet de mettre à jour le firmware directement depuis Linux, sans redémarrer sous Windows ou créer de clé USB bootable.

**Développé par :** Red Hat et la communauté Linux
**Support :** Plus de 2000 périphériques de dizaines de fabricants
**Intégration :** Natif dans Linux Mint

**Fabricants participants :**
- Dell, Lenovo, HP
- Logitech (souris, claviers)
- Intel, AMD
- Samsung, Western Digital (SSD)
- 8BitDo (manettes)
- System76, Framework
- Et beaucoup d'autres

### Vérifier si fwupd est installé

**Commande :**
```bash
fwupdmgr --version
```

**Si non installé :**
```bash
sudo apt update
sudo apt install fwupd
```

Linux Mint l'installe généralement par défaut.

### Interface graphique : GNOME Firmware

**Installation :**
```bash
sudo apt install gnome-firmware
```

**Accès :**
- Menu → Administration → **Firmware**
- Ou : `gnome-firmware`

**Interface simple :**
- Liste des périphériques détectés
- Mises à jour disponibles affichées
- Un clic pour installer
- Redémarrage automatique si nécessaire

---

## Utiliser fwupd en ligne de commande

### Vérifier les périphériques compatibles

**Lister tous les périphériques détectés :**
```bash
fwupdmgr get-devices
```

**Exemple de sortie :**
```
UEFI Device Firmware
│   Device ID:          XXXXXXXXXXXX
│   Summary:            System Firmware
│   Current version:    1.12.0
│   Vendor:             Dell Inc.
│   UpdateState:        Success
│
NVMe Storage
│   Device ID:          YYYYYYYYYYYYY
│   Summary:            Samsung SSD 980 PRO
│   Current version:    5B2QGXA7
│   Vendor:             Samsung Electronics
│   Flags:              updatable|needs-reboot
```

**Informations importantes :**
- **Device ID** : Identifiant unique
- **Current version** : Version actuelle du firmware
- **Flags** : Propriétés (updatable = peut être mis à jour)

### Rafraîchir la liste des mises à jour

**Télécharger la liste depuis LVFS (Linux Vendor Firmware Service) :**
```bash
fwupdmgr refresh
```

Cette commande contacte le serveur de mises à jour et récupère la liste des firmwares disponibles.

**LVFS** est une base de données centralisée de firmwares fournis par les fabricants.

### Vérifier les mises à jour disponibles

**Commande :**
```bash
fwupdmgr get-updates
```

**Sortie si mises à jour disponibles :**
```
Devices with no available firmware updates:
 • UEFI Device Firmware
 • Integrated Camera
Devices with the latest available firmware version:
 • USB Hub
Devices that can be updated:
 • Samsung SSD 980 PRO
  │ Update Version: 5B2QGXA8
  │ Update Description: Security and performance improvements
```

**Si aucune mise à jour :**
```
Devices with no available firmware updates: All devices
```

### Mettre à jour le firmware

**⚠️ IMPORTANT : Lisez les précautions avant de continuer !**

**Mise à jour de tous les périphériques :**
```bash
fwupdmgr update
```

**Mise à jour d'un périphérique spécifique :**
```bash
fwupdmgr update DEVICE-ID
```

**Processus :**
1. Téléchargement du firmware
2. Vérification de la signature cryptographique
3. Validation de la compatibilité
4. Installation
5. **Redémarrage** (si nécessaire)

**Pendant le redémarrage :**
- Ne touchez à rien !
- L'écran affiche la progression
- Le système redémarre automatiquement
- Peut prendre 5-15 minutes

### Vérifier l'historique des mises à jour

**Voir les mises à jour effectuées :**
```bash
fwupdmgr get-history
```

**Sortie :**
```
Samsung SSD 980 PRO
│ Previous version: 5B2QGXA7
│ Update Version:   5B2QGXA8
│ Update State:     Success
│ Last modified:    2024-11-30 15:30
```

### Rétrograder un firmware (downgrade)

**Si une mise à jour pose problème, vous pouvez revenir en arrière :**

```bash
# Voir les versions précédentes disponibles
fwupdmgr get-releases DEVICE-ID

# Rétrograder vers une version spécifique
fwupdmgr downgrade DEVICE-ID
```

⚠️ **Attention :** Le downgrade n'est pas toujours possible (certains fabricants le bloquent).

---

## Mise à jour du BIOS/UEFI

### Précautions CRITIQUES

**⚠️ DANGER - LISEZ ATTENTIVEMENT ⚠️**

La mise à jour du BIOS/UEFI est la **plus risquée** de toutes les mises à jour firmware :

**Risques :**
- ❌ Coupure de courant → Ordinateur **inutilisable**
- ❌ Mauvaise manipulation → BIOS **corrompu**
- ❌ Mauvaise version → Incompatibilité matérielle
- ❌ Interruption du processus → **"Brick"** (ordinateur mort)

**Règles d'or :**
1. ✅ **Ordinateur portable** : Branchez sur secteur ET batterie chargée (>50%)
2. ✅ **Ordinateur fixe** : Utilisez un onduleur (UPS) si possible
3. ✅ **Sauvegardez vos données** importantes avant
4. ✅ **Ne mettez à jour que si nécessaire** (bug grave ou faille de sécurité)
5. ✅ Lisez le changelog : que corrige cette mise à jour ?
6. ✅ **Ne touchez à RIEN** pendant la mise à jour
7. ✅ **Soyez patient** : peut prendre 15 minutes

### Vérifier votre version BIOS/UEFI actuelle

**Méthode 1 : dmidecode**
```bash
sudo dmidecode -s bios-version
```

**Méthode 2 : Information système**
```bash
sudo dmidecode -t bios
```

**Sortie :**
```
BIOS Information
        Vendor: Dell Inc.
        Version: 1.12.0
        Release Date: 08/15/2023
        Revision: 5.20
```

**Méthode 3 : Interface graphique**
- Menu → Informations système → Section "Matériel"

**Méthode 4 : Au démarrage**
- Redémarrez l'ordinateur
- Appuyez sur **F2**, **F10**, **Suppr** ou **Échap** (selon fabricant)
- La version s'affiche dans l'interface BIOS

### Mise à jour UEFI via fwupd (méthode recommandée)

**Vérifier si votre ordinateur supporte fwupd pour le BIOS :**
```bash
fwupdmgr get-devices | grep -i uefi
```

Si vous voyez "UEFI Device Firmware" ou "System Firmware", c'est supporté !

**Procédure :**

1. **Vérifier les mises à jour BIOS disponibles :**
```bash
fwupdmgr get-updates
```

2. **Lire attentivement le changelog :**
Les notes de version indiquent ce qui est corrigé/amélioré.

3. **Brancher l'ordinateur sur secteur**

4. **Lancer la mise à jour :**
```bash
fwupdmgr update
```

Ou pour le BIOS spécifiquement :
```bash
fwupdmgr update UEFI-DEVICE-ID
```

5. **Confirmer** (tapez "y" si demandé)

6. **Le système redémarre automatiquement**

**Pendant la mise à jour UEFI :**
- L'écran affiche "Firmware Update" ou similaire
- Une barre de progression apparaît
- **NE TOUCHEZ À RIEN !**
- **N'ÉTEIGNEZ PAS l'ordinateur !**
- **NE DÉBRANCHEZ PAS !**

7. **Redémarrage automatique**
Une fois terminé, l'ordinateur redémarre normalement.

8. **Vérifier la nouvelle version :**
```bash
sudo dmidecode -s bios-version
```

### Mise à jour BIOS via méthode traditionnelle

Si fwupd ne supporte pas votre ordinateur, utilisez la méthode du fabricant.

#### Dell

**Site officiel :**
- support.dell.com
- Entrez votre numéro de série (Service Tag)
- Section "Drivers & Downloads"
- Téléchargez le fichier BIOS (.exe sous Windows)

**Sous Linux :**
Certains BIOS Dell sont au format `.exe` auto-extractible.

**Méthode 1 : Extraction avec Wine**
```bash
# Installer Wine si nécessaire
sudo apt install wine

# Extraire le BIOS
wine BIOS-Dell-XXX.exe
# Cherchez un fichier .hdr ou .bin
```

**Méthode 2 : Mise à jour depuis le BIOS**
1. Copiez le fichier sur une clé USB FAT32
2. Redémarrez → F12 (Boot Menu)
3. Sélectionnez "BIOS Flash Update"
4. Sélectionnez le fichier sur la clé USB
5. Confirmez et attendez

#### Lenovo

**Site officiel :**
- support.lenovo.com
- Cherchez votre modèle
- Téléchargez le "BIOS Update (Bootable CD)"
- Format ISO ou format Linux (script .sh)

**Si script Linux (.sh) :**
```bash
# Rendre exécutable
chmod +x flash_bios.sh

# Exécuter en root
sudo ./flash_bios.sh
```

**Si ISO bootable :**
1. Créez une clé USB bootable avec l'ISO
2. Démarrez dessus
3. Suivez les instructions à l'écran

#### HP

**Site officiel :**
- support.hp.com

**Formats disponibles :**
- .exe pour Windows
- Mise à jour depuis le BIOS (HP System BIOS)

**Procédure :**
1. Téléchargez le fichier
2. Extrayez sur clé USB FAT32
3. Redémarrez → F10 (BIOS Setup)
4. Advanced → BIOS Update
5. Sélectionnez le fichier
6. Confirmez

#### ASUS

**Méthode EZ Flash (depuis le BIOS) :**
1. Téléchargez le fichier BIOS (.CAP)
2. Copiez sur clé USB FAT32
3. Redémarrez → F2 (BIOS)
4. Advanced Mode → Tool → ASUS EZ Flash Utility
5. Sélectionnez le fichier
6. Confirmez et attendez

#### MSI

**M-Flash (depuis le BIOS) :**
1. Téléchargez le fichier BIOS (format MSI)
2. Clé USB FAT32
3. Redémarrez → Suppr (BIOS)
4. M-Flash
5. Sélectionnez le fichier
6. Flash

### Vérification post-mise à jour

**Après la mise à jour BIOS :**

1. **Vérifiez la version :**
```bash
sudo dmidecode -s bios-version
```

2. **Testez le démarrage :**
   - L'ordinateur démarre-t-il normalement ?
   - Le système d'exploitation se charge-t-il ?

3. **Vérifiez les paramètres BIOS :**
   - Certaines mises à jour réinitialisent les paramètres
   - Vérifiez :
     - Ordre de boot
     - Secure Boot (activé/désactivé selon vos besoins)
     - Virtualisation (VT-x/AMD-V)
     - Paramètres d'économie d'énergie

4. **Testez les fonctionnalités :**
   - Suspension/Réveil
   - Ports USB
   - Webcam
   - WiFi/Bluetooth

---

## Mise à jour du microcode CPU

### Qu'est-ce que le microcode ?

Le **microcode** est un firmware du processeur qui corrige des bugs au niveau matériel.

**Importance :**
- Corrige les failles de sécurité (Spectre, Meltdown, etc.)
- Améliore la stabilité du CPU
- Nécessaire pour certaines fonctionnalités

**Bonne nouvelle :** Linux Mint installe automatiquement les microcodes Intel et AMD.

### Vérifier le microcode actuel

**Pour processeurs Intel :**
```bash
# Vérifier si le microcode Intel est installé
dpkg -l | grep intel-microcode

# Voir la version du microcode chargé
dmesg | grep microcode
```

**Pour processeurs AMD :**
```bash
# Vérifier si le microcode AMD est installé
dpkg -l | grep amd64-microcode

# Voir la version
dmesg | grep microcode
```

**Sortie attendue :**
```
microcode: microcode updated early to revision 0xXX
```

### Installer/Mettre à jour le microcode

**Intel :**
```bash
sudo apt update
sudo apt install intel-microcode
```

**AMD :**
```bash
sudo apt update
sudo apt install amd64-microcode
```

**Application du microcode :**
Le microcode est chargé au démarrage. Redémarrez après installation :
```bash
sudo reboot
```

**Vérification post-redémarrage :**
```bash
dmesg | grep microcode
```

La version devrait être plus récente.

---

## Mise à jour firmware de périphériques spécifiques

### SSD (Disques SSD)

**Importance :**
- Corrections de bugs pouvant causer perte de données
- Amélioration des performances
- Gestion améliorée de l'usure

#### Avec fwupd

**Vérifier les mises à jour SSD :**
```bash
fwupdmgr get-devices | grep -i nvme
fwupdmgr get-devices | grep -i ssd
```

**Mettre à jour :**
```bash
fwupdmgr update SSD-DEVICE-ID
```

#### Avec les outils du fabricant

**Samsung SSD :**

Samsung fournit **Samsung Magician** pour Windows seulement, mais le firmware peut être mis à jour avec un ISO bootable.

1. Téléchargez l'ISO de mise à jour depuis samsung.com
2. Créez une clé USB bootable :
```bash
sudo dd if=samsung-firmware.iso of=/dev/sdX bs=4M status=progress
```
3. Démarrez sur la clé
4. Suivez les instructions

**Crucial/Micron :**

Crucial propose un outil Linux :
```bash
# Téléchargez depuis crucial.com
wget https://.../.../crucial-firmware-tool.tar.gz
tar -xzf crucial-firmware-tool.tar.gz
cd crucial-firmware-tool
sudo ./update-firmware.sh
```

**Western Digital / SanDisk :**

Utilisez le **WD Dashboard** (version Windows) ou ISO bootable disponible sur leur site.

### Carte graphique (GPU VBIOS)

**⚠️ Attention :** La mise à jour du VBIOS GPU est **très risquée**.

**Quand mettre à jour :**
- Jamais, sauf bug critique documenté
- Carte graphique instable/plantages fréquents
- Instruction spécifique du fabricant

**NVIDIA :**
Les mises à jour VBIOS NVIDIA sont rares et généralement intégrées au pilote.

**AMD :**
Idem, les mises à jour sont gérées par le pilote AMDGPU.

**Ne tentez une mise à jour VBIOS que si :**
- Vous êtes expérimenté
- Vous avez une carte identique de secours
- Le fabricant fournit un outil officiel

### Carte réseau WiFi/Bluetooth

**Généralement géré par fwupd :**
```bash
fwupdmgr get-devices | grep -i wireless
fwupdmgr get-devices | grep -i bluetooth
```

**Fabricants courants :**

**Intel WiFi :**
Excellent support, mises à jour via fwupd ou via le paquet linux-firmware :
```bash
sudo apt install linux-firmware
```

**Broadcom :**
Support limité, souvent pas de mise à jour firmware nécessaire.

**Realtek :**
Support variable, vérifier le site du fabricant.

### Touchpad et clavier (laptops)

**Souvent mis à jour via fwupd :**
```bash
fwupdmgr get-devices | grep -i touchpad
fwupdmgr get-devices | grep -i keyboard
```

**Fabricants supportant fwupd :**
- Dell
- Lenovo
- HP
- Framework
- System76

### Webcam

```bash
fwupdmgr get-devices | grep -i camera
fwupdmgr get-devices | grep -i webcam
```

### Dock USB / Hub / Thunderbolt

**Excellente compatibilité fwupd :**

**Docks Dell, HP, Lenovo :**
Bien supportés, mises à jour fréquentes.

**Thunderbolt :**
Critiques pour la sécurité (failles Thunderspy).

```bash
fwupdmgr get-devices | grep -i thunderbolt
fwupdmgr update
```

---

## Problèmes et dépannage

### Mise à jour BIOS échouée

**Symptômes :**
- Ordinateur ne démarre plus
- Écran noir
- Bips d'erreur

**Solutions selon le fabricant :**

#### Recovery BIOS (Dell, HP, Lenovo)

La plupart des cartes mères modernes ont un **BIOS de secours** (backup BIOS).

**Procédure générale :**
1. Éteignez complètement l'ordinateur
2. Maintenez **Ctrl + Esc** (ou **Fn + Esc** selon modèle)
3. Appuyez sur le bouton d'alimentation
4. Gardez **Ctrl + Esc** enfoncé 30 secondes
5. Le BIOS de récupération démarre
6. Insérez une clé USB avec le BIOS correct
7. Suivez les instructions de récupération

#### BIOS Flashback (ASUS, MSI)

Certaines cartes mères ont un bouton "BIOS Flashback" :

1. Téléchargez le BIOS correct
2. Renommez-le selon les instructions (ex: MSI.ROM)
3. Copiez sur clé USB FAT32
4. Branchez la clé dans le port spécifique
5. Appuyez sur le bouton "BIOS Flashback"
6. Attendez (LED clignote, puis s'éteint = terminé)

#### Dual BIOS (Gigabyte)

Cartes Gigabyte avec Dual BIOS :

1. Éteignez
2. Alternez entre les deux BIOS avec le switch sur la carte mère
3. Démarrez avec le BIOS de secours
4. Reflashez le BIOS principal

**En dernier recours :**
- Retour en garantie (si sous garantie)
- Reprogrammation du BIOS par technicien (SOIC/SPI programmer)
- Remplacement de la carte mère

### fwupd ne détecte pas mon périphérique

**Causes possibles :**

1. **Périphérique non supporté par LVFS**
   - Vérifiez sur https://fwupd.org/lvfs/devices
   - Cherchez votre modèle

2. **Pilote manquant**
   - Installez les pilotes nécessaires d'abord

3. **Périphérique USB nécessite l'activation**
   ```bash
   # Activer tous les périphériques USB
   fwupdmgr enable-remote lvfs
   fwupdmgr enable-remote lvfs-testing
   ```

4. **Version fwupd trop ancienne**
   ```bash
   # Mettre à jour fwupd
   sudo apt update
   sudo apt install --only-upgrade fwupd
   ```

### Erreur "Signature verification failed"

**Cause :** Firmware corrompu ou non signé.

**Solution :**
1. Ne forcez JAMAIS l'installation d'un firmware non signé
2. Téléchargez à nouveau depuis le site officiel
3. Vérifiez l'intégrité avec le checksum si fourni

### Périphérique "bricked" après mise à jour

**Clé USB / Souris / Clavier :**
- Généralement récupérable par le fabricant
- Contactez le support

**SSD :**
- Utilisez l'outil de récupération du fabricant (souvent disponible)
- Samsung : Samsung Magician recovery mode
- Crucial : Crucial Storage Executive recovery

**Dock USB :**
- Certains ont un bouton de reset
- Débrancher 30 secondes, rebrancher

---

## Bonnes pratiques et recommandations

### Quand mettre à jour le firmware

**✅ Mettez à jour si :**
- **Faille de sécurité** critique corrigée (Spectre, Meltdown, etc.)
- **Bug grave** affectant votre utilisation (plantages, perte de données)
- **Nouveau matériel** nécessitant support (nouveau CPU, RAM)
- **Recommandation du fabricant** pour votre modèle spécifique
- **Amélioration significative** documentée

**❌ Ne mettez PAS à jour si :**
- "Just because" (juste pour avoir la dernière version)
- Tout fonctionne parfaitement
- Pas de changelog clair
- Firmware en version bêta/expérimentale (sauf test volontaire)

**Règle d'or :** *"If it ain't broke, don't fix it"*
(Si ça marche, ne touchez pas)

### Avant chaque mise à jour

**Checklist :**

1. ✅ **Sauvegardez vos données importantes**
2. ✅ **Lisez le changelog** : que corrige/améliore cette mise à jour ?
3. ✅ **Recherchez des retours** : forums, Reddit, sites tech
4. ✅ **Notez votre version actuelle** (pour downgrade si besoin)
5. ✅ **Vérifiez l'alimentation** :
   - Portable : >50% batterie + branché secteur
   - Fixe : Onduleur recommandé
6. ✅ **Fermez toutes les applications**
7. ✅ **Assurez une connexion stable** (pas de WiFi instable)
8. ✅ **Prévoyez du temps** (ne faites pas ça 5 min avant un RDV !)

### Pendant la mise à jour

**🚫 NE JAMAIS :**
- Éteindre l'ordinateur
- Débrancher l'alimentation
- Fermer le terminal/l'application
- Appuyer sur des touches
- Déplacer/bouger l'ordinateur
- Utiliser d'autres applications

**✅ TOUJOURS :**
- Être patient (peut prendre 15-20 minutes)
- Laisser le processus se terminer complètement
- Attendre le redémarrage automatique
- Ne toucher à rien pendant les écrans de progression

### Après la mise à jour

**Vérifications :**

1. ✅ **Version mise à jour** :
   ```bash
   fwupdmgr get-devices
   # Ou pour BIOS
   sudo dmidecode -s bios-version
   ```

2. ✅ **Système fonctionne normalement** :
   - Démarrage OK
   - Tous les périphériques détectés
   - Performances normales

3. ✅ **Tester les fonctionnalités critiques** :
   - Suspension/réveil
   - WiFi/Bluetooth
   - Ports USB
   - Webcam si utilisée

4. ✅ **Vérifier les paramètres BIOS** (si mise à jour BIOS)
   - Peuvent avoir été réinitialisés
   - Vérifiez Secure Boot, Virtualization, etc.

### Automatisation prudente

**fwupd peut s'exécuter automatiquement :**

```bash
# Voir la configuration
cat /etc/fwupd/daemon.conf
```

**Option UpdateMotd :**
- `true` : Affiche les mises à jour disponibles au login
- `false` : N'affiche rien

**Recommandation :**
- ❌ **Ne PAS** activer les mises à jour automatiques de firmware
- ✅ **Vérifiez manuellement** régulièrement (1 fois/mois)
- ✅ **Choisissez** quand et quoi mettre à jour

---

## Surveillance et maintenance

### Vérifications régulières

**Fréquence recommandée : 1 fois par mois**

```bash
# Rafraîchir la base de données
fwupdmgr refresh

# Vérifier les mises à jour
fwupdmgr get-updates

# Voir tous les périphériques
fwupdmgr get-devices
```

**Ajoutez à votre calendrier** un rappel mensuel.

### S'informer sur les vulnérabilités

**Sources fiables :**
- **Site du fabricant** : Dell Support, Lenovo Support, etc.
- **LVFS Blog** : https://fwupd.org/
- **CVE Database** : https://cve.mitre.org/
- **Forums Linux** : Reddit r/linux, forums Linux Mint

**Alertes importantes :**
Abonnez-vous aux alertes de sécurité de votre fabricant.

### Documenter vos mises à jour

**Créez un fichier de suivi :**

```bash
nano ~/firmware-updates.txt
```

**Exemple de contenu :**
```
Firmware Update Log
===================

2024-11-15 - BIOS Update
- Model: Dell XPS 15 9520
- Previous: 1.10.0
- New: 1.12.0
- Reason: Security patch for Spectre variant
- Result: Success
- Notes: All working fine

2024-10-20 - SSD Firmware
- Model: Samsung 980 PRO 1TB
- Previous: 5B2QGXA7
- New: 5B2QGXA8
- Reason: Performance improvement
- Result: Success
- Notes: Write speeds improved 15%
```

---

## Outils et ressources

### Outils de diagnostic firmware

**dmidecode - Informations système**
```bash
# Tout voir
sudo dmidecode

# BIOS seulement
sudo dmidecode -t bios

# Carte mère
sudo dmidecode -t baseboard

# Mémoire
sudo dmidecode -t memory
```

**lshw - Vue d'ensemble matériel**
```bash
# Tout le matériel
sudo lshw

# Format court
sudo lshw -short

# Classe spécifique (disk, network, etc.)
sudo lshw -C disk
```

**hwinfo - Informations détaillées**
```bash
sudo apt install hwinfo
sudo hwinfo --short
```

**inxi - Résumé système**
```bash
# Vue d'ensemble
inxi -Fxz

# BIOS et carte mère
inxi -M
```

### Sites web utiles

**LVFS (Linux Vendor Firmware Service) :**
- https://fwupd.org/
- Base de données de firmwares
- Recherche par périphérique

**Fabricants :**
- **Dell** : support.dell.com
- **Lenovo** : support.lenovo.com
- **HP** : support.hp.com
- **ASUS** : asus.com/support
- **MSI** : msi.com/support
- **Gigabyte** : gigabyte.com/support

**Communauté :**
- **Forums Linux Mint** : forums.linuxmint.com
- **ArchWiki** (excellente doc) : wiki.archlinux.org
- **Reddit** : r/linuxhardware, r/Dell, r/Lenovo, etc.

### Documentation fwupd

```bash
# Pages man
man fwupd
man fwupdmgr

# Aide en ligne
fwupdmgr --help
fwupdmgr update --help
```

**Documentation complète :**
https://github.com/fwupd/fwupd/wiki

---

## Cas particuliers

### Ordinateurs Framework

**Framework Laptop** a un excellent support fwupd.

**Tous les modules sont mis à jour séparément :**
- Carte mère
- Embedded Controller
- Modules d'extension
- Carte WiFi
- Webcam

```bash
fwupdmgr get-devices
# Montre tous les modules Framework
```

**Recommandation :** Mettez à jour régulièrement, Framework publie fréquemment.

### Ordinateurs System76

**System76** fournit un excellent support Linux.

**Outil dédié : system76-firmware**
```bash
# Installer
sudo apt install system76-firmware system76-firmware-daemon

# Vérifier les mises à jour
sudo system76-firmware-cli schedule
```

Interface graphique incluse dans Pop!_OS, mais fonctionne aussi sur Mint.

### Chromebooks (Coreboot/MrChromebox)

Si vous avez installé Linux sur un Chromebook :

**MrChromebox UEFI Firmware :**
- Permet d'installer un UEFI complet
- https://mrchromebox.tech/

**⚠️ Avancé** : Nécessite ouverture du Chromebook et manipulation du write-protect.

### Raspberry Pi et ARM

**Raspberry Pi** utilise un firmware propriétaire pour le GPU.

**Mise à jour :**
```bash
sudo rpi-update
```

**Autres SBCs ARM :**
Variable selon le fabricant (Odroid, Pine64, etc.).

---

## Sécurité du firmware

### Secure Boot et UEFI Signing

**Secure Boot** vérifie que le firmware et le bootloader sont signés.

**Avantages :**
- Protection contre rootkits et bootkits
- Chaîne de confiance depuis le firmware

**Sous Linux :**
- Supporte Secure Boot avec shim
- Certains firmwares nécessitent Secure Boot désactivé (vieux matériel)

**Vérifier l'état Secure Boot :**
```bash
mokutil --sb-state
```

### TPM (Trusted Platform Module)

**TPM** est une puce de sécurité qui stocke des clés cryptographiques.

**Usage :**
- Chiffrement de disque (BitLocker sous Windows, LUKS sous Linux)
- Attestation matérielle
- Mesures de démarrage sécurisé

**Vérifier TPM :**
```bash
# Installer
sudo apt install tpm2-tools

# Vérifier présence
sudo tpm2_getcap properties-fixed
```

### Protection contre Downgrade

Certains fabricants empêchent le **downgrade firmware** pour des raisons de sécurité.

**Exemple :** Un firmware corrige une faille critique, le downgrade est bloqué pour éviter l'exploitation.

**Implication :** Une fois mis à jour, vous ne pouvez parfois plus revenir en arrière.

---

## Conclusion

La mise à jour du firmware est un aspect **important mais délicat** de la maintenance d'un ordinateur sous Linux.

**Points clés à retenir :**

- ✅ **fwupd simplifie énormément** la mise à jour de firmware sous Linux
- ✅ **Mises à jour BIOS/UEFI** : Soyez **très prudent**, suivez les règles
- ✅ **Ne mettez à jour que si nécessaire** : sécurité ou bug grave
- ✅ **Lisez toujours le changelog** avant de mettre à jour
- ✅ **Sauvegardez vos données** et **branchez l'alimentation**
- ✅ **Ne touchez à rien** pendant le processus
- ✅ **Vérifications régulières** : 1 fois par mois

**Avec fwupd :**
- Plus de 2000 périphériques supportés
- Processus sécurisé et automatisé
- Signatures cryptographiques vérifiées
- Historique et rollback possibles

**La mise à jour de firmware sous Linux est devenue aussi simple (voire plus simple) que sous Windows**, grâce à fwupd et à la participation croissante des fabricants.

Gardez votre système à jour, mais avec discernement et précaution !

Dans le prochain chapitre, nous aborderons la **résolution de problèmes matériels**, pour diagnostiquer et corriger les soucis hardware sous Linux Mint.

⏭️ [Résolution de problèmes matériels](/12-materiel-et-pilotes/08-resolution-de-problemes-materiels.md)
