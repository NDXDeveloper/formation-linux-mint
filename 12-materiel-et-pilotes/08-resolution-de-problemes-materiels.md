🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 12.8 Résolution de problèmes matériels

## Introduction

Même sous Linux Mint, qui offre une excellente compatibilité matérielle, vous pouvez parfois rencontrer des problèmes avec certains composants. Ce chapitre vous donne une **méthodologie claire** pour identifier, diagnostiquer et résoudre les problèmes matériels.

La bonne nouvelle : **95% des problèmes matériels sous Linux ont une solution** !

---

## Méthodologie générale de diagnostic

### Les 5 étapes du diagnostic

#### 1. Identifier le problème précisément

**Questions à se poser :**
- 🔍 **Quoi** : Quel composant ne fonctionne pas ?
- 🔍 **Quand** : Le problème est-il permanent ou intermittent ?
- 🔍 **Depuis quand** : Après une mise à jour ? Depuis l'installation ?
- 🔍 **Comment** : Le matériel est-il totalement invisible ou partiellement fonctionnel ?

**Exemple :**
- ❌ Mauvais : "Mon son ne marche pas"
- ✅ Bon : "Pas de son depuis la mise à jour du noyau, les haut-parleurs internes ne fonctionnent pas mais le casque USB fonctionne"

#### 2. Vérifier le matériel physiquement

**Avant tout diagnostic logiciel :**

✅ **Vérifications basiques :**
- Le périphérique est-il **allumé** ?
- Les **câbles** sont-ils bien branchés ?
- Les **prises** sont-elles dans le bon port ?
- Y a-t-il un **interrupteur physique** (WiFi, webcam) ?
- La **batterie** est-elle chargée (périphériques sans fil) ?
- Le périphérique fonctionne-t-il sur **un autre ordinateur** ?

**Exemple :** 50% des "pannes WiFi" sont dues à l'interrupteur physique désactivé !

#### 3. Vérifier la détection par le système

**Le système voit-il le matériel ?**

**Commande universelle :**
```bash
# Vue d'ensemble du matériel
sudo lshw -short
```

**Par type :**
```bash
# Périphériques PCI (carte son, réseau, GPU)
lspci

# Périphériques USB
lsusb

# Périphériques bloc (disques, clés USB)
lsblk

# Périphériques d'entrée (clavier, souris)
ls /dev/input/
```

**Si le périphérique apparaît** → Problème de pilote/configuration
**Si le périphérique n'apparaît pas** → Problème matériel ou détection BIOS

#### 4. Consulter les logs système

**Les logs contiennent des informations précieuses :**

```bash
# Messages du noyau (matériel)
dmesg | tail -50

# Logs système complets
journalctl -b -p err
# -b = depuis le dernier boot
# -p err = erreurs seulement

# Logs en temps réel
journalctl -f
```

**Rechercher un périphérique spécifique :**
```bash
dmesg | grep -i wifi
dmesg | grep -i bluetooth
dmesg | grep -i audio
dmesg | grep -i usb
```

#### 5. Rechercher et appliquer la solution

**Sources d'information :**
1. **Forums Linux Mint** : forums.linuxmint.com
2. **ArchWiki** : wiki.archlinux.org (excellente documentation)
3. **Ask Ubuntu** : askubuntu.com (souvent compatible Mint)
4. **Reddit** : r/linuxmint, r/linux4noobs
5. **Wiki du fabricant** : Dell, Lenovo, HP ont des sections Linux

**Formulation de recherche efficace :**
```
linux mint [modèle exact] [problème précis]
```

Exemple : `linux mint dell xps 15 9520 wifi not working`

---

## Outils de diagnostic matériel

### inxi - Vue d'ensemble système

**Installation :**
```bash
sudo apt install inxi
```

**Utilisation :**
```bash
# Vue complète (recommandé pour diagnostic)
inxi -Fxz

# Sections spécifiques :
inxi -A     # Audio
inxi -G     # Graphique
inxi -N     # Réseau
inxi -D     # Disques
inxi -B     # Batterie
inxi -M     # Carte mère
```

**Exemple de sortie :**
```
Graphics:
  Device-1: Intel TigerLake-LP GT2 [Iris Xe Graphics] driver: i915 v: kernel
  Device-2: NVIDIA GA107M [GeForce RTX 3050 Mobile] driver: nvidia v: 535.129
  Display: x11 server: X.Org v: 1.21.1.7 driver: X: loaded: modesetting,nvidia
  unloaded: fbdev,nouveau,vesa gpu: i915 resolution: 1920x1200~60Hz
```

**Interprétation :**
- **Device** : Matériel détecté
- **driver** : Pilote utilisé
- **loaded/unloaded** : Pilotes chargés/non chargés

### lshw - Matériel détaillé

**Commande :**
```bash
# Résumé
sudo lshw -short

# Détails complets
sudo lshw

# Classe spécifique
sudo lshw -C display    # Cartes graphiques
sudo lshw -C network    # Cartes réseau
sudo lshw -C multimedia # Audio
sudo lshw -C disk       # Stockage
sudo lshw -C input      # Périphériques d'entrée
sudo lshw -C memory     # Mémoire RAM
sudo lshw -C processor  # CPU
```

**Générer un rapport HTML :**
```bash
sudo lshw -html > rapport-materiel.html
```

### hwinfo - Diagnostic approfondi

**Installation :**
```bash
sudo apt install hwinfo
```

**Utilisation :**
```bash
# Vue d'ensemble
sudo hwinfo --short

# Matériel spécifique
sudo hwinfo --gfxcard
sudo hwinfo --netcard
sudo hwinfo --sound
sudo hwinfo --usb
sudo hwinfo --bluetooth
```

### hardinfo - Interface graphique

**Installation :**
```bash
sudo apt install hardinfo
```

**Lancement :**
- Menu → Système → **Informations et tests du système**
- Ou : `hardinfo`

**Fonctionnalités :**
- Vue d'ensemble du matériel
- Températures
- Benchmarks simples
- Exportation en HTML

### Outils de test

#### memtest86+ - Test de RAM

**Accès :**
- Au démarrage → Menu GRUB → **Memory Test**

**Usage :**
- Teste la RAM pour détecter les erreurs
- Essentiel si plantages aléatoires
- Laissez tourner plusieurs heures (idéalement une nuit)

**Interprétation :**
- **0 erreur** : RAM OK
- **Erreurs détectées** : RAM défectueuse → remplacement nécessaire

#### smartctl - Santé des disques

**Installation :**
```bash
sudo apt install smartmontools
```

**Vérifier la santé d'un disque :**
```bash
# État de santé global
sudo smartctl -H /dev/sda

# Informations complètes
sudo smartctl -a /dev/sda

# Lancer un test court
sudo smartctl -t short /dev/sda

# Voir les résultats
sudo smartctl -l selftest /dev/sda
```

**Interprétation :**
```
SMART overall-health self-assessment test result: PASSED
```
✅ Disque en bonne santé

```
SMART overall-health self-assessment test result: FAILED
```
❌ Disque défaillant → **Sauvegarde immédiate + remplacement**

#### stress-ng - Test de stabilité

**Installation :**
```bash
sudo apt install stress-ng
```

**Tests :**
```bash
# Stresser le CPU (4 cœurs, 60 secondes)
stress-ng --cpu 4 --timeout 60s

# Stresser la RAM (utilise 80% de la RAM)
stress-ng --vm 2 --vm-bytes 80% --timeout 60s

# Test complet (CPU + RAM + I/O)
stress-ng --cpu 4 --vm 2 --io 2 --timeout 120s
```

**Usage :**
- Tester la stabilité après overclock
- Vérifier le refroidissement
- Diagnostiquer les plantages aléatoires

**Surveiller pendant le test :**
```bash
# Dans un autre terminal
sensors    # Températures
htop       # Utilisation CPU/RAM
```

---

## Problèmes par catégorie de matériel

### Problèmes d'affichage (GPU)

#### Écran noir au démarrage

**Causes courantes :**
1. Pilote graphique incompatible
2. Paramètres de résolution incorrects
3. Conflit entre GPU intégré et dédié (Optimus)

**Solutions :**

**1. Démarrer en mode graphique de secours :**
- Au GRUB, appuyez sur **'e'**
- Trouvez la ligne commençant par `linux`
- Ajoutez `nomodeset` à la fin
- Appuyez sur **F10** pour démarrer

**2. Installer le pilote propriétaire :**
```bash
# Mode nomodeset actif, installer le pilote NVIDIA
sudo ubuntu-drivers autoinstall
sudo reboot
```

**3. Blacklister le pilote nouveau (NVIDIA) :**
```bash
sudo nano /etc/modprobe.d/blacklist-nouveau.conf
```

Ajoutez :
```
blacklist nouveau
options nouveau modeset=0
```

Mettez à jour initramfs :
```bash
sudo update-initramfs -u
sudo reboot
```

#### Résolution incorrecte

**Diagnostic :**
```bash
xrandr
```

**Forcer une résolution :**
```bash
# Créer un mode personnalisé
cvt 1920 1080 60  # Génère les paramètres

# Ajouter le mode
xrandr --newmode "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync

# Ajouter au périphérique
xrandr --addmode HDMI-1 "1920x1080_60.00"

# Appliquer
xrandr --output HDMI-1 --mode "1920x1080_60.00"
```

**Rendre permanent :**
Ajoutez les commandes à `~/.xprofile` ou aux paramètres d'affichage.

#### Problème multi-écrans

**Détection :**
```bash
xrandr --listmonitors
```

**Configuration graphique :**
- Menu → Préférences → **Affichage**
- Glissez-déposez les écrans pour les positionner
- Définissez l'écran principal

**En ligne de commande :**
```bash
# Écran principal à gauche, secondaire à droite
xrandr --output eDP-1 --primary --mode 1920x1080 --output HDMI-1 --mode 1920x1080 --right-of eDP-1
```

#### Tearing (déchirement d'image)

**Pour NVIDIA :**
```bash
sudo nvidia-settings
```
- X Server Display Configuration → Advanced
- Activez "**Force Full Composition Pipeline**"

**Pour Intel :**
```bash
sudo nano /etc/X11/xorg.conf.d/20-intel.conf
```

Ajoutez :
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "TearFree" "true"
EndSection
```

**Pour AMD :**
```bash
sudo nano /etc/X11/xorg.conf.d/20-amdgpu.conf
```

Ajoutez :
```
Section "Device"
   Identifier  "AMD Graphics"
   Driver      "amdgpu"
   Option      "TearFree" "true"
EndSection
```

Redémarrez X (Ctrl+Alt+Backspace) ou redémarrez le système.

### Problèmes audio

#### Pas de son du tout

**Diagnostic :**

1. **Vérifier ALSA :**
```bash
aplay -l  # Liste les périphériques
speaker-test -c 2  # Test son
```

2. **Vérifier PulseAudio/PipeWire :**
```bash
pactl info
pactl list sinks
```

3. **Vérifier que rien n'est muet :**
```bash
alsamixer
```
Utilisez les flèches pour naviguer, **'M'** pour activer/désactiver mute.

**Solutions :**

**1. Redémarrer le serveur audio :**
```bash
# PipeWire
systemctl --user restart pipewire pipewire-pulse

# Ou PulseAudio (ancien)
pulseaudio -k
pulseaudio --start
```

**2. Forcer la carte son :**
```bash
# Voir les cartes
cat /proc/asound/cards

# Définir par défaut (dans ~/.asoundrc)
defaults.pcm.card 0
defaults.ctl.card 0
```

**3. Réinstaller les paquets audio :**
```bash
sudo apt install --reinstall alsa-base alsa-utils pulseaudio
```

#### Son crachotant/coupures

**Solutions :**

**1. Augmenter la taille du buffer :**
```bash
sudo nano /etc/pulse/daemon.conf
```

Décommentez et modifiez :
```
default-fragments = 5
default-fragment-size-msec = 2
```

**2. Désactiver suspension audio :**
```bash
sudo nano /etc/pulse/default.pa
```

Commentez :
```
#load-module module-suspend-on-idle
```

**3. Pour PipeWire :**
```bash
nano ~/.config/pipewire/pipewire.conf
```

Augmentez le quantum :
```
default.clock.quantum = 256
```

#### Microphone ne fonctionne pas

**Vérifications :**

1. **Test simple :**
```bash
arecord -d 5 test.wav
aplay test.wav
```

2. **Vérifier dans pavucontrol :**
```bash
pavucontrol
```
Onglet "Périphériques d'entrée" → Volume > 0, pas en mute

3. **Permissions :**
```bash
# Ajouter au groupe audio
sudo usermod -a -G audio $USER
```

Déconnectez-vous et reconnectez-vous.

### Problèmes WiFi

#### WiFi non détecté

**Diagnostic :**

```bash
# Lister les interfaces réseau
ip link show

# Détails WiFi
iwconfig

# État rfkill
rfkill list
```

**Solutions :**

**1. Débloquer rfkill :**
```bash
sudo rfkill unblock all
```

**2. Vérifier le pilote :**
```bash
lspci -k | grep -A 3 -i network
```

**3. Installer le firmware manquant :**
```bash
# Pour Broadcom
sudo apt install bcmwl-kernel-source

# Pour Intel
sudo apt install firmware-iwlwifi

# Pour Realtek
sudo apt install firmware-realtek
```

**4. Redémarrer le module :**
```bash
# Identifier le module (exemple: iwlwifi)
lsmod | grep -i wifi

# Redémarrer
sudo modprobe -r iwlwifi
sudo modprobe iwlwifi
```

#### WiFi lent ou instable

**Optimisations :**

**1. Désactiver gestion d'énergie :**
```bash
sudo nano /etc/NetworkManager/conf.d/wifi-powersave.conf
```

Ajoutez :
```
[connection]
wifi.powersave = 2
```

```bash
sudo systemctl restart NetworkManager
```

**2. Changer le canal WiFi :**
Utilisez l'interface de votre routeur pour choisir un canal moins encombré.

**3. Préférer la bande 5GHz :**
Moins d'interférences, plus rapide (mais portée réduite).

### Problèmes Bluetooth

#### Bluetooth ne s'active pas

**Diagnostic :**
```bash
hciconfig
sudo systemctl status bluetooth
```

**Solutions :**

**1. Redémarrer le service :**
```bash
sudo systemctl restart bluetooth
```

**2. Débloquer :**
```bash
sudo rfkill unblock bluetooth
```

**3. Recharger le module :**
```bash
sudo modprobe -r btusb
sudo modprobe btusb
```

**4. Réinstaller :**
```bash
sudo apt install --reinstall bluez
```

#### Périphérique ne s'appaire pas

**Solutions :**

**1. Supprimer l'ancien appairage :**
```bash
bluetoothctl
# Dans bluetoothctl :
remove XX:XX:XX:XX:XX:XX
scan on
pair XX:XX:XX:XX:XX:XX
connect XX:XX:XX:XX:XX:XX
trust XX:XX:XX:XX:XX:XX
```

**2. Réinitialiser le périphérique :**
Consultez le manuel pour réinitialiser le périphérique Bluetooth.

### Problèmes USB

#### Périphérique USB non reconnu

**Diagnostic :**
```bash
# Avant de brancher
lsusb

# Après branchement
lsusb
# Le périphérique devrait apparaître

# Messages du noyau
dmesg | tail -20
```

**Solutions :**

**1. Tester un autre port USB :**
Préférez un port USB 2.0 (noir) pour compatibilité maximale.

**2. Vérifier l'alimentation :**
```bash
lsusb -t
```
Si "500mA" et le périphérique nécessite plus, utilisez un hub USB alimenté.

**3. Réinitialiser le bus USB :**
```bash
# Trouver le périphérique
lsusb
# Bus 002 Device 004: ...

# Réinitialiser
echo -n "0000:00:14.0" | sudo tee /sys/bus/pci/drivers/xhci_hcd/unbind
sleep 1
echo -n "0000:00:14.0" | sudo tee /sys/bus/pci/drivers/xhci_hcd/bind
```

**4. Désactiver autosuspend :**
```bash
# Temporaire
echo -1 | sudo tee /sys/bus/usb/devices/*/power/autosuspend
```

#### Clé USB en lecture seule

**Diagnostic :**
```bash
mount | grep sdb1
```

Si "ro" (read-only) apparaît :

**Solutions :**

**1. Remonter en lecture-écriture :**
```bash
sudo mount -o remount,rw /dev/sdb1
```

**2. Vérifier/réparer le système de fichiers :**
```bash
# Démonter d'abord
sudo umount /dev/sdb1

# Vérifier et réparer
sudo fsck -y /dev/sdb1  # Pour ext4
sudo dosfsck -a /dev/sdb1  # Pour FAT32
```

**3. Vérifier la protection en écriture physique :**
Certaines clés USB ont un interrupteur de protection.

### Problèmes touchpad (laptop)

#### Touchpad non détecté

**Diagnostic :**
```bash
xinput list
sudo libinput list-devices
```

**Solutions :**

**1. Activer dans les paramètres :**
Menu → Préférences → **Souris et Touchpad**

**2. Charger le module :**
```bash
sudo modprobe -r psmouse
sudo modprobe psmouse
```

**3. Activer via synclient :**
```bash
synclient TouchpadOff=0
```

#### Touchpad trop/pas assez sensible

**Configuration :**
```bash
synclient -l  # Voir paramètres actuels

# Ajuster la sensibilité
synclient MinSpeed=0.5
synclient MaxSpeed=1.0
synclient AccelFactor=0.05
```

**Rendre permanent :**
Ajoutez à `~/.xprofile` :
```bash
synclient MinSpeed=0.5
synclient MaxSpeed=1.0
```

#### Désactiver le touchpad quand on tape

```bash
# Désactiver pendant 1 seconde après frappe
synclient PalmDetect=1
synclient PalmMinWidth=10
```

### Problèmes webcam

#### Webcam non détectée

**Diagnostic :**
```bash
ls /dev/video*
v4l2-ctl --list-devices
```

**Solutions :**

**1. Vérifier l'interrupteur physique :**
Beaucoup de laptops ont un bouton ou un cache physique.

**2. Installer v4l-utils :**
```bash
sudo apt install v4l-utils
```

**3. Charger le module :**
```bash
sudo modprobe uvcvideo
```

**4. Tester :**
```bash
# Installer Cheese
sudo apt install cheese
cheese
```

#### Mauvaise qualité d'image

**Ajuster les paramètres :**
```bash
# Lister les contrôles disponibles
v4l2-ctl -d /dev/video0 --list-ctrls

# Ajuster luminosité
v4l2-ctl -d /dev/video0 --set-ctrl=brightness=128

# Ajuster contraste
v4l2-ctl -d /dev/video0 --set-ctrl=contrast=32
```

### Problèmes de batterie (laptop)

#### Batterie non détectée

**Diagnostic :**
```bash
upower -i /org/freedesktop/UPower/devices/battery_BAT0
acpi -V
```

**Solutions :**

**1. Réinitialiser la batterie :**
- Éteignez l'ordinateur
- Débranchez l'alimentation
- Retirez la batterie (si amovible)
- Maintenez le bouton d'alimentation 30 secondes
- Remettez la batterie
- Redémarrez

**2. Vérifier le module ACPI :**
```bash
lsmod | grep battery
sudo modprobe battery
```

#### Autonomie très faible

**Diagnostic :**
```bash
# État de santé
upower -i /org/freedesktop/UPower/devices/battery_BAT0 | grep capacity

# Applications gourmandes
powertop
```

**Solutions :**

**1. Installer TLP :**
```bash
sudo apt install tlp
sudo tlp start
```

**2. Optimiser avec PowerTop :**
```bash
sudo powertop --auto-tune
```

**3. Réduire luminosité, désactiver WiFi/Bluetooth si non utilisés**

### Problèmes de ventilateur/température

#### Ventilateur toujours au maximum

**Diagnostic :**
```bash
# Installer sensors
sudo apt install lm-sensors
sudo sensors-detect  # Répondez "yes" à tout

# Voir températures
sensors
```

**Solutions :**

**1. Nettoyer physiquement :**
Poussière = ennemi n°1. Nettoyez les grilles de ventilation.

**2. Installer un contrôle de ventilateur :**

**Pour ThinkPad :**
```bash
sudo apt install thinkfan
```

**Pour autres laptops :**
```bash
# fancontrol (générique)
sudo apt install fancontrol
sudo pwmconfig  # Configuration guidée
sudo systemctl enable fancontrol
```

**3. Limiter la fréquence CPU :**
```bash
# Passer en mode powersave
sudo cpupower frequency-set -g powersave
```

#### Surchauffe

**Vérifications :**
```bash
sensors
```

Si température > 90°C en idle → **problème sérieux**

**Solutions :**

**1. Vérifier les processus :**
```bash
htop
```
Identifiez et arrêtez les processus gourmands.

**2. Repâte thermique :**
Si ancien ordinateur (>3 ans), la pâte thermique est peut-être sèche.
→ Remplacement par un professionnel ou vous-même (avancé).

**3. Support ventilé :**
Utilisez un support pour laptop avec ventilateurs additionnels.

---

## Problèmes de compatibilité matérielle

### Vérifier la compatibilité avant achat

**Bases de données :**
- **Linux Hardware Database** : linux-hardware.org
- **Ubuntu Certified Hardware** : ubuntu.com/certified
- **ArchWiki Hardware** : wiki.archlinux.org/title/Hardware

**Recherche spécifique :**
```
[modèle exact] linux compatibility
```

Exemple : `dell xps 15 9520 linux`

### Matériel problématique sous Linux

**Généralement problématiques :**
- ❌ WiFi Broadcom (ancien)
- ❌ Cartes graphiques NVIDIA récentes (sans pilote propriétaire)
- ❌ Scanners/imprimantes très récents
- ❌ Périphériques gaming RGB (logiciel Windows uniquement)

**Généralement excellents :**
- ✅ WiFi Intel
- ✅ Cartes graphiques AMD (pilote libre excellent)
- ✅ Imprimantes HP
- ✅ Périphériques Logitech

### Contournements courants

#### Dual GPU (NVIDIA Optimus)

**Problème :** Laptop avec Intel + NVIDIA, conflits possibles.

**Solution :**
```bash
# Installer NVIDIA Prime
sudo apt install nvidia-prime

# Basculer entre GPU
sudo prime-select intel  # Économie batterie
sudo prime-select nvidia  # Performance
sudo prime-select on-demand  # Hybride (recommandé)

# Redémarrer
sudo reboot
```

#### Périphérique nécessitant firmware non-libre

**Solution :**
```bash
# Activer les dépôts non-free
sudo apt install software-properties-common
sudo add-apt-repository multiverse
sudo apt update

# Installer firmware supplémentaire
sudo apt install linux-firmware
sudo apt install firmware-misc-nonfree
```

---

## Logs et fichiers de diagnostic

### Principaux fichiers de logs

```bash
# Logs noyau (kernel)
/var/log/kern.log

# Messages système
/var/log/syslog

# Xorg (affichage)
~/.local/share/xorg/Xorg.0.log

# Journal systemd
journalctl
```

### Commandes de diagnostic avancées

```bash
# Erreurs matérielles récentes
dmesg -l err,warn

# Périphériques PCI avec pilotes
lspci -v

# Périphériques USB détaillés
lsusb -v

# Modules du noyau chargés
lsmod

# Informations sur un module
modinfo [nom_module]

# Dépendances matérielles
sudo hwinfo --log=materiel.txt
```

### Générer un rapport de bug complet

**Script rapide :**
```bash
#!/bin/bash
# rapport-materiel.sh

echo "=== Informations système ===" > rapport.txt
inxi -Fxz >> rapport.txt

echo -e "\n=== Matériel détecté ===" >> rapport.txt
sudo lshw -short >> rapport.txt

echo -e "\n=== Erreurs récentes ===" >> rapport.txt
journalctl -b -p err >> rapport.txt

echo -e "\n=== Messages noyau ===" >> rapport.txt
dmesg | tail -100 >> rapport.txt

echo "Rapport généré : rapport.txt"
```

**Utilisation :**
```bash
chmod +x rapport-materiel.sh
./rapport-materiel.sh
```

---

## Solutions par fabricant

### Dell

**Outils Dell pour Linux :**
```bash
# Dell Command Configure (sur certains modèles)
# Disponible sur support.dell.com

# Vérifier les mises à jour firmware
fwupdmgr get-updates
```

**Problèmes courants :**
- **Webcam** : Souvent désactivée dans le BIOS
  - F2 au démarrage → Security → Camera → Enable
- **WiFi Killer** : Parfois problématique
  - Installer firmware-iwlwifi

### Lenovo (ThinkPad)

**Excellente compatibilité Linux en général.**

**Outils spécifiques :**
```bash
# Gestion alimentation
sudo apt install tlp tlp-rdw
sudo apt install tp-smapi-dkms  # ThinkPad SMAPI

# Ventilateurs
sudo apt install thinkfan
```

**TrackPoint :**
```bash
# Ajuster sensibilité
xinput list  # Trouver le TrackPoint
xinput set-prop [ID] "Device Accel Constant Deceleration" 0.5
```

### HP

**Support variable selon modèles.**

**Problèmes courants :**
- **Touches fonction inversées** : F1-F12 nécessitent Fn
  - Solution : Paramètre BIOS "Action Keys Mode"

**Outils :**
```bash
# HPLIP pour imprimantes/scanners
sudo apt install hplip hplip-gui
```

### ASUS

**Compatibilité moyenne, nécessite parfois ajustements.**

**Problèmes courants :**
- **Clavier RGB** : Pas de contrôle natif
  - Solution : rogauracore ou asusctl (communauté)

**Installer asusctl (ROG) :**
```bash
sudo add-apt-repository ppa:lukejenkins/asusctl
sudo apt update
sudo apt install asusctl
```

### System76 / Framework

**Conçus pour Linux, compatibilité parfaite.**

**Framework :**
Tous les modules ont un support fwupd excellent.

---

## Quand le matériel est vraiment défectueux

### Signes de défaillance matérielle

**RAM défectueuse :**
- Plantages aléatoires (kernel panic)
- Erreurs dans memtest86+
- Écrans bleus/gelages

**Disque dur défectueux :**
- Bruits anormaux (clics, grincements)
- Ralentissements extrêmes
- Erreurs I/O dans les logs
- SMART status: FAILED

**GPU défectueux :**
- Artefacts visuels (pixels colorés aléatoires)
- Écran noir après quelques minutes
- Plantages sous charge graphique
- Surchauffe excessive

**Carte mère défectueuse :**
- Aucun POST (Power-On Self Test)
- Bips d'erreur au démarrage
- Périphériques qui disparaissent aléatoirement
- Pas de démarrage même en mode sans échec

### Tests finaux

**Test ultime : Live USB**

Créez une clé USB Linux Mint Live et démarrez dessus :
- **Si le problème persiste** → Matériel défectueux
- **Si le problème disparaît** → Problème logiciel/configuration

**Test sur un autre OS :**
- Démarrez sur Windows (dual-boot) ou une autre distribution
- Si le problème persiste → Défaillance matérielle confirmée

### Recours

**Sous garantie :**
- Contactez le fabricant
- Documentation : logs, tests effectués
- Souvent remplacement gratuit

**Hors garantie :**
- Réparation par professionnel
- Remplacement du composant défectueux
- Récupération de données si disque

---

## Ressources et communauté

### Forums d'aide

**Francophones :**
- Forums Linux Mint FR : forum.ubuntu-fr.org
- LinuxFr : linuxfr.org
- Debian-facile : debian-facile.org

**Anglophones :**
- Linux Mint Forums : forums.linuxmint.com
- Ask Ubuntu : askubuntu.com
- Reddit : r/linuxmint, r/linux4noobs

### Comment poser une question efficacement

**Informations à fournir :**

1. **Modèle exact de l'ordinateur**
   ```bash
   sudo dmidecode -s system-product-name
   ```

2. **Version de Linux Mint**
   ```bash
   cat /etc/os-release
   ```

3. **Kernel version**
   ```bash
   uname -r
   ```

4. **Description du problème**
   - Symptômes précis
   - Depuis quand
   - Ce qui a changé récemment

5. **Ce que vous avez déjà tenté**

6. **Logs pertinents**
   ```bash
   dmesg | grep -i erreur > erreurs.txt
   ```

**Exemple de bonne question :**
```
Sujet : WiFi Intel AX201 non détecté - Dell XPS 15 9520

Bonjour,

Matériel : Dell XPS 15 9520
OS : Linux Mint 21.2 Cinnamon
Kernel : 5.15.0-91-generic

Problème : La carte WiFi Intel AX201 n'est pas détectée.
- `ip link` ne montre aucune interface wlan
- `lspci` liste la carte : "Network controller: Intel Corporation Wi-Fi 6 AX201"
- Le problème existe depuis l'installation

J'ai essayé :
- sudo apt install firmware-iwlwifi (déjà à jour)
- rfkill unblock all (pas d'effet)
- Vérification BIOS : WiFi activé

Logs dmesg : [joindre fichier]

Merci d'avance pour votre aide !
```

### Documentation technique

**ArchWiki** (excellente, même pour Ubuntu/Mint) :
- wiki.archlinux.org

**Ubuntu Wiki** :
- help.ubuntu.com

**Kernel Documentation** :
- kernel.org/doc/html/latest/

### Canaux IRC / Discord

**IRC Libera.Chat :**
- #linuxmint
- #ubuntu (aide générale)

**Discord :**
- Serveur Linux Mint (lien sur le site officiel)

---

## Aide-mémoire des commandes

### Diagnostic rapide

```bash
# Vue d'ensemble matériel
inxi -Fxz

# Périphériques PCI
lspci

# Périphériques USB
lsusb

# Erreurs récentes
journalctl -b -p err

# Messages noyau
dmesg | tail -50

# Températures
sensors

# Disques
lsblk
sudo smartctl -H /dev/sda

# Réseau
ip link show
iwconfig

# Audio
pactl list sinks

# Batterie
acpi -V

# RAM
free -h

# CPU
lscpu
```

### Redémarrages de services

```bash
# Réseau
sudo systemctl restart NetworkManager

# Bluetooth
sudo systemctl restart bluetooth

# Audio (PipeWire)
systemctl --user restart pipewire pipewire-pulse

# Audio (PulseAudio)
pulseaudio -k && pulseaudio --start

# Affichage (redémarre session)
sudo systemctl restart display-manager
```

### Chargement/Déchargement modules

```bash
# Lister modules
lsmod

# Charger un module
sudo modprobe [nom_module]

# Décharger un module
sudo modprobe -r [nom_module]

# Recharger un module
sudo modprobe -r [nom_module] && sudo modprobe [nom_module]

# Blacklister un module (permanent)
echo "blacklist [nom_module]" | sudo tee /etc/modprobe.d/blacklist-custom.conf
```

---

## Conclusion

La résolution de problèmes matériels sous Linux Mint suit une **méthodologie logique** et dispose d'excellents **outils de diagnostic**.

**Points clés à retenir :**

✅ **Méthodologie en 5 étapes** :
1. Identifier précisément le problème
2. Vérifier le matériel physiquement
3. Vérifier la détection système
4. Consulter les logs
5. Rechercher et appliquer la solution

✅ **Outils essentiels** :
- `inxi -Fxz` : Vue d'ensemble
- `lspci` / `lsusb` : Périphériques
- `dmesg` : Messages noyau
- `journalctl` : Logs système

✅ **95% des problèmes ont une solution** :
- Pilote manquant/incorrect
- Configuration à ajuster
- Module à recharger
- Firmware à mettre à jour

✅ **Communauté très active** :
- Forums d'entraide
- Documentation riche
- Nombreux tutoriels

**N'ayez pas peur d'expérimenter** (avec sauvegarde préalable) et **n'hésitez pas à demander de l'aide** à la communauté !

La compatibilité matérielle de Linux s'améliore constamment, et Linux Mint fait un excellent travail pour rendre le matériel fonctionnel "out of the box".

Avec ce chapitre, vous disposez maintenant des connaissances pour diagnostiquer et résoudre la plupart des problèmes matériels que vous pourriez rencontrer.

**Bon dépannage !** 🔧

⏭️ [Kernel et mises à jour du kernel](/12-materiel-et-pilotes/09-kernel-et-mises-a-jour-du-kernel.md)
