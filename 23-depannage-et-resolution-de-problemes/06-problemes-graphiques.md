🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 23.6 Problèmes graphiques (pilotes, résolution)

## Introduction

Les problèmes graphiques sont parmi les plus frustrants sous Linux, car ils affectent directement votre expérience visuelle. La bonne nouvelle, c'est que Linux Mint a fait d'énormes progrès dans la gestion des cartes graphiques, et la plupart des problèmes ont des solutions simples.

Ce guide vous accompagne pour identifier et résoudre les problèmes graphiques les plus courants, que ce soit des soucis de pilotes, de résolution d'écran, d'affichage multi-écrans, ou d'artefacts visuels.

**Rassurez-vous :** Même les problèmes qui semblent graves (écran noir, affichage bizarre) sont généralement réparables sans expertise technique avancée.

---

## Types de problèmes graphiques courants

### Problème Type 1 : Écran noir au démarrage

**Symptômes :**
- Le logo Linux Mint s'affiche
- Puis l'écran devient complètement noir
- Parfois avec un curseur clignotant
- Impossible d'accéder au bureau

**Cause principale :** Pilote graphique incompatible ou mal configuré

**Gravité :** ⭐⭐⭐ (nécessite mode recovery ou nomodeset)

---

### Problème Type 2 : Mauvaise résolution d'écran

**Symptômes :**
- L'affichage est flou ou étiré
- Résolution trop basse (par ex. 1024×768 au lieu de 1920×1080)
- Impossible de sélectionner la résolution native
- Texte trop gros ou trop petit

**Cause principale :** Pilote générique utilisé, EDID non détecté

**Gravité :** ⭐ (facile à résoudre)

---

### Problème Type 3 : Déchirure d'écran (screen tearing)

**Symptômes :**
- L'image semble "coupée" horizontalement quand vous scrollez
- Vidéos qui "sautent" visuellement
- Fenêtres qui laissent des traînées quand vous les déplacez

**Cause principale :** Vsync désactivé, problème de composition

**Gravité :** ⭐⭐ (nécessite ajustements de configuration)

---

### Problème Type 4 : Scintillement ou clignotement

**Symptômes :**
- L'écran clignote par moments
- Flashes blancs ou noirs aléatoires
- Instabilité visuelle générale

**Cause principale :** Pilote instable, fréquence de rafraîchissement incorrecte

**Gravité :** ⭐⭐ (ajustements pilotes/configuration)

---

### Problème Type 5 : Artefacts visuels ou corruption graphique

**Symptômes :**
- Pixels colorés aléatoires à l'écran
- Rectangles bizarres qui apparaissent
- Texte corrompu ou illisible
- Fenêtres qui ne s'affichent pas correctement

**Cause principale :** Surchauffe GPU, VRAM défectueuse, pilote buggé

**Gravité :** ⭐⭐⭐ (peut indiquer un problème matériel)

---

### Problème Type 6 : Multi-écrans qui ne fonctionnent pas

**Symptômes :**
- Deuxième écran non détecté
- Écrans en miroir alors que vous voulez étendre
- Résolution différente sur chaque écran
- Configuration perdue au redémarrage

**Cause principale :** Configuration XRandR, pilotes, connexion physique

**Gravité :** ⭐⭐ (configuration nécessaire)

---

### Problème Type 7 : Performance graphique faible

**Symptômes :**
- Animations lentes ou saccadées
- Jeux qui rament
- Lecture vidéo saccadée
- Effets de bureau désactivés automatiquement

**Cause principale :** Pilote générique au lieu du pilote optimisé

**Gravité :** ⭐⭐ (installation de pilotes)

---

## Identifier votre carte graphique

Avant toute chose, vous devez savoir quelle carte graphique vous avez.

### Méthode 1 : Interface graphique (la plus simple)

**Informations système :**
Menu → Administration → **Informations système**

Cherchez la section "Graphiques" ou "Graphics".

---

### Méthode 2 : Terminal (plus détaillé)

**Commande principale :**
```bash
lspci | grep -i vga
```

**Exemple de résultat :**
```
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 620
01:00.0 VGA compatible controller: NVIDIA Corporation GP107M [GeForce GTX 1050 Mobile]
```

**Interprétation :**
- **Intel** : Carte graphique intégrée Intel
- **NVIDIA** : Carte graphique dédiée NVIDIA
- **AMD** : Carte graphique AMD/ATI

**Version plus détaillée :**
```bash
lspci -v | grep -A 12 VGA
```

---

### Méthode 3 : Commande inxi (recommandée)

```bash
inxi -G
```

**Exemple de résultat :**
```
Graphics:
  Device-1: Intel HD Graphics 620 driver: i915 v: kernel
  Device-2: NVIDIA GeForce GTX 1050 Mobile driver: nvidia v: 535.154.05
  Display: x11 server: X.Org v: 1.21.1.7 driver: X: loaded: nvidia
  Resolution: 1920x1080@60Hz
  OpenGL: renderer: NVIDIA GeForce GTX 1050/PCIe/SSE2 v: 4.6.0
```

**Informations clés :**
- **Device** : Modèle de carte graphique
- **driver** : Pilote actuellement utilisé
- **Resolution** : Résolution actuelle
- **OpenGL renderer** : Système de rendu utilisé

---

### Les trois grands fabricants

#### 1. NVIDIA

**Signes :** Nom contient "GeForce", "Quadro", "RTX", "GTX"

**Pilotes disponibles :**
- **nouveau** : Pilote open source (limité)
- **nvidia** : Pilote propriétaire (recommandé pour performances)

**Commande de vérification :**
```bash
nvidia-smi  # Si pilote NVIDIA installé
```

---

#### 2. AMD / ATI

**Signes :** Nom contient "Radeon", "AMD", "ATI"

**Pilotes disponibles :**
- **amdgpu** : Pilote open source moderne (recommandé)
- **radeon** : Ancien pilote open source (pour vieilles cartes)
- **amdgpu-pro** : Pilote propriétaire (pour workstations)

**Commande de vérification :**
```bash
glxinfo | grep "OpenGL renderer"
```

---

#### 3. Intel

**Signes :** Nom contient "Intel", "HD Graphics", "Iris", "UHD"

**Pilotes disponibles :**
- **i915** : Pilote open source (seul disponible, fonctionne bien)

**Note :** Intel n'a pas de pilote propriétaire sous Linux. Le pilote open source est excellent.

---

## Le Gestionnaire de pilotes

C'est l'outil graphique officiel de Linux Mint pour gérer les pilotes.

### Accès

Menu → Administration → **Gestionnaire de pilotes**

Ou en terminal :
```bash
driver-manager
```

### Utilisation

**Première ouverture :**
1. Le système scanne votre matériel (peut prendre 1-2 minutes)
2. Les pilotes disponibles s'affichent
3. Les pilotes recommandés sont marqués

**Interface :**
- **Pilotes libres** : Open source, pré-installés généralement
- **Pilotes propriétaires** : Fermés, mais souvent plus performants
- **Recommandé** : Pilote testé et stable pour votre matériel

**Actions possibles :**
- **Installer** un pilote : Sélectionnez-le et cliquez "Appliquer les changements"
- **Changer** de pilote : Sélectionnez un autre et appliquez
- **Revenir au pilote libre** : Sélectionnez "nouveau" (NVIDIA) ou "X.Org" (autres)

**Important :** Toujours redémarrer après un changement de pilote !

---

## Problèmes spécifiques NVIDIA

NVIDIA est le fabricant le plus "problématique" sous Linux en raison des pilotes propriétaires.

### Symptôme : Écran noir après installation du pilote NVIDIA

**Solution 1 : Démarrer en mode nomodeset**

1. Au menu GRUB, appuyez sur **'e'** pour éditer
2. Trouvez la ligne commençant par `linux`
3. À la fin, ajoutez : `nomodeset`
4. Appuyez sur **F10** pour démarrer

Une fois démarré :

```bash
# Désinstaller le pilote NVIDIA problématique
sudo apt remove --purge nvidia-*
sudo apt autoremove

# Installer le pilote stable
sudo apt update
sudo ubuntu-drivers autoinstall

# Redémarrer
sudo reboot
```

---

**Solution 2 : Utiliser le pilote nouveau (open source)**

En mode nomodeset ou recovery :

```bash
# Installer le pilote nouveau
sudo apt install xserver-xorg-video-nouveau

# Supprimer le pilote propriétaire
sudo apt remove --purge nvidia-*

# Reconfigurer
sudo dpkg-reconfigure xserver-xorg

# Redémarrer
sudo reboot
```

**Note :** Le pilote nouveau est moins performant, mais plus stable.

---

### Symptôme : Plusieurs versions de pilotes NVIDIA disponibles

**Quelle version choisir ?**

Dans le Gestionnaire de pilotes, vous voyez par exemple :
- nvidia-driver-470 (proprietary, tested)
- nvidia-driver-535 (proprietary)
- nvidia-driver-545 (proprietary)

**Recommandation :**
1. **Choisissez "tested"** si disponible (le plus stable)
2. Si plusieurs "tested", prenez le numéro le plus élevé
3. Évitez les versions "open kernel" sauf si vous savez ce que vous faites

**Versions courantes :**
- **470** : Pour cartes anciennes (série 600-700)
- **535** : Version LTS stable (Long Term Support)
- **545+** : Versions récentes (pour nouvelles cartes)

---

### Symptôme : Optimus (double GPU Intel + NVIDIA)

Les ordinateurs portables avec Intel + NVIDIA posent des défis.

**Vérifier si vous avez Optimus :**
```bash
lspci | grep -i vga
```

Si vous voyez Intel ET NVIDIA, vous avez Optimus.

**Solutions :**

#### Option 1 : Prime Select (recommandé)

```bash
# Installer prime-select
sudo apt install nvidia-prime

# Vérifier le mode actuel
prime-select query

# Utiliser NVIDIA uniquement (performances)
sudo prime-select nvidia

# Utiliser Intel uniquement (économie batterie)
sudo prime-select intel

# Mode hybride (automatique, nécessite pilote récent)
sudo prime-select on-demand

# Redémarrer
sudo reboot
```

---

#### Option 2 : Interface graphique NVIDIA X Server

Si installé :
```bash
nvidia-settings
```

Allez dans **PRIME Profiles** et sélectionnez :
- **NVIDIA (Performance Mode)** : Utilise toujours NVIDIA
- **Intel (Power Saving Mode)** : Utilise toujours Intel
- **NVIDIA On-Demand** : Choix par application

---

### Symptôme : Déchirure d'écran (tearing) avec NVIDIA

**Solution : Activer ForceCompositionPipeline**

```bash
# Ouvrir la configuration NVIDIA
sudo nvidia-settings
```

1. Allez dans **X Server Display Configuration**
2. Sélectionnez votre écran
3. Cliquez sur **Advanced**
4. Cochez **Force Composition Pipeline**
5. Cliquez **Save to X Configuration File**
6. Redémarrez

**Ou en ligne de commande :**

```bash
# Créer le fichier de configuration
sudo nano /etc/X11/xorg.conf.d/20-nvidia.conf

# Ajouter :
Section "Screen"
    Identifier     "Screen0"
    Option         "metamodes" "nvidia-auto-select +0+0 {ForceCompositionPipeline=On}"
EndSection

# Sauvegarder et redémarrer
sudo reboot
```

---

### Symptôme : nvidia-smi ne fonctionne pas

```bash
nvidia-smi
```

**Si erreur "NVIDIA-SMI has failed..." :**

```bash
# Réinstaller le pilote NVIDIA
sudo apt install --reinstall nvidia-driver-535  # Remplacer par votre version

# Vérifier que le module est chargé
lsmod | grep nvidia

# Si pas chargé, le charger manuellement
sudo modprobe nvidia

# Redémarrer
sudo reboot
```

---

## Problèmes spécifiques AMD

AMD est généralement mieux supporté grâce aux pilotes open source.

### Symptôme : Mauvaises performances avec carte AMD récente

**Vérifier le pilote utilisé :**
```bash
lspci -k | grep -A 3 -i vga
```

Cherchez la ligne "Kernel driver in use".

**Devrait être :**
- **amdgpu** : Pour cartes récentes (RX 400 et plus récent)
- **radeon** : Pour vieilles cartes (R9 et antérieur)

**Si "radeon" sur une carte récente :**

```bash
# Forcer l'utilisation d'amdgpu
sudo nano /etc/modprobe.d/amdgpu.conf

# Ajouter (selon votre carte) :
options amdgpu si_support=1
options amdgpu cik_support=1

# Blacklister radeon
sudo nano /etc/modprobe.d/blacklist-radeon.conf

# Ajouter :
blacklist radeon

# Mettre à jour initramfs
sudo update-initramfs -u

# Redémarrer
sudo reboot
```

---

### Symptôme : Scintillement ou artefacts avec AMD

**Solution : Ajuster les paramètres de TearFree**

```bash
# Créer fichier de configuration
sudo nano /etc/X11/xorg.conf.d/20-amdgpu.conf

# Ajouter :
Section "Device"
    Identifier "AMD"
    Driver "amdgpu"
    Option "TearFree" "true"
    Option "DRI" "3"
EndSection

# Sauvegarder et redémarrer
sudo reboot
```

---

### Symptôme : Ventilateur AMD qui tourne fort en permanence

**Vérifier la température :**
```bash
sensors
```

**Installer les outils AMD :**
```bash
sudo apt install radeontop

# Monitoring GPU
radeontop
```

**Ajuster la vitesse du ventilateur (avancé) :**
```bash
# Activer le contrôle manuel (temporaire)
echo manual | sudo tee /sys/class/drm/card0/device/hwmon/hwmon*/pwm1_enable

# Définir la vitesse (0-255, exemple 128 = 50%)
echo 128 | sudo tee /sys/class/drm/card0/device/hwmon/hwmon*/pwm1
```

**⚠️ Attention :** Surveiller la température pour éviter la surchauffe !

---

## Problèmes spécifiques Intel

Les cartes Intel sont généralement bien supportées, mais peuvent avoir quelques soucis.

### Symptôme : Déchirure d'écran avec Intel

**Solution : Activer TearFree**

```bash
sudo nano /etc/X11/xorg.conf.d/20-intel.conf

# Ajouter :
Section "Device"
    Identifier "Intel Graphics"
    Driver "intel"
    Option "TearFree" "true"
    Option "DRI" "3"
EndSection

# Sauvegarder et redémarrer
sudo reboot
```

---

### Symptôme : Performances faibles avec Intel récent

**Vérifier que le bon driver est utilisé :**
```bash
glxinfo | grep "OpenGL renderer"
```

**Devrait afficher :** Intel HD/UHD/Iris + numéro

**Si "llvmpipe" apparaît** (rendu logiciel) :

```bash
# Réinstaller les pilotes Intel
sudo apt install --reinstall xserver-xorg-video-intel

# Ou pour les cartes très récentes, utiliser modesetting :
sudo nano /etc/X11/xorg.conf.d/20-intel.conf

# Ajouter :
Section "Device"
    Identifier "Intel Graphics"
    Driver "modesetting"
EndSection

# Redémarrer
sudo reboot
```

---

## Problèmes de résolution d'écran

### Symptôme : Résolution trop basse, impossible de la changer

**Diagnostic :**

```bash
# Voir les résolutions disponibles
xrandr
```

**Exemple de sortie :**
```
Screen 0: minimum 320 x 200, current 1024 x 768, maximum 16384 x 16384
HDMI-1 connected 1024x768+0+0 (normal left inverted right x axis y axis) 527mm x 296mm
   1920x1080     60.00 +
   1024x768      60.00*
```

**Interprétation :**
- **current** : Résolution actuelle (1024×768)
- **+** : Résolution native préférée (1920×1080)
- ***** : Résolution actuellement utilisée

---

**Solution 1 : Changer via l'interface graphique**

Menu → Préférences → **Affichage**

Sélectionnez la résolution native (celle avec la plus haute valeur).

---

**Solution 2 : Forcer une résolution avec xrandr**

Si la résolution souhaitée n'apparaît pas dans la liste :

```bash
# Créer un nouveau mode (exemple pour 1920x1080 à 60 Hz)
cvt 1920 1080 60

# Résultat donne une ligne "Modeline", exemple :
# Modeline "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync

# Créer le nouveau mode
xrandr --newmode "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync

# Ajouter le mode à votre sortie (HDMI-1, DP-1, etc.)
xrandr --addmode HDMI-1 "1920x1080_60.00"

# Appliquer
xrandr --output HDMI-1 --mode "1920x1080_60.00"
```

---

**Solution 3 : Rendre permanent (fichier de configuration X11)**

```bash
sudo nano /etc/X11/xorg.conf.d/10-monitor.conf

# Ajouter :
Section "Monitor"
    Identifier "HDMI-1"
    Modeline "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
    Option "PreferredMode" "1920x1080_60.00"
EndSection

Section "Screen"
    Identifier "Screen0"
    Monitor "HDMI-1"
    DefaultDepth 24
    SubSection "Display"
        Modes "1920x1080_60.00"
    EndSubSection
EndSection

# Sauvegarder et redémarrer
sudo reboot
```

---

### Symptôme : Texte ou interface trop petits/grands (problème de DPI)

**Solution : Ajuster l'échelle dans Cinnamon**

Menu → Préférences → **Paramètres système** → **Affichage**

Ajustez "Interface scaling" :
- **Auto** : Détection automatique
- **Normal** : 1× (100%)
- **Double (HiDPI)** : 2× (200%)
- **Valeur personnalisée** : 1.25×, 1.5×, etc.

**En ligne de commande :**

```bash
# Vérifier le DPI actuel
xdpyinfo | grep resolution

# Forcer un DPI spécifique (exemple 96 DPI standard)
sudo nano /etc/X11/xorg.conf.d/90-dpi.conf

# Ajouter :
Section "Monitor"
    Identifier "<default monitor>"
    DisplaySize 508 285  # Taille en mm (calculer selon votre écran)
EndSection

# Ou forcer directement :
Section "Device"
    Identifier "Device0"
    Option "DPI" "96 x 96"
EndSection

# Redémarrer
sudo reboot
```

---

## Multi-écrans (configuration multiple)

### Configuration graphique (recommandé)

Menu → Préférences → **Affichage**

**Options disponibles :**
- **Miroir** : Même affichage sur tous les écrans
- **Étendre** : Bureau étendu sur plusieurs écrans
- **Écran unique** : Utiliser un seul écran

**Configuration :**
1. Sélectionnez un écran
2. Définissez sa position (glisser-déposer dans l'interface)
3. Choisissez la résolution
4. Définissez l'écran principal
5. Appliquez

---

### Configuration avec xrandr (terminal)

**Lister les écrans connectés :**
```bash
xrandr --query
```

**Exemples de configuration :**

```bash
# Étendre l'affichage : HDMI-1 à droite de eDP-1
xrandr --output eDP-1 --auto --output HDMI-1 --auto --right-of eDP-1

# Écran HDMI comme principal, laptop éteint
xrandr --output HDMI-1 --auto --primary --output eDP-1 --off

# Miroir (même affichage)
xrandr --output HDMI-1 --auto --same-as eDP-1

# Résolutions différentes
xrandr --output eDP-1 --mode 1920x1080 --output HDMI-1 --mode 2560x1440 --right-of eDP-1
```

---

### Sauvegarder la configuration multi-écrans

**Problème :** La configuration se perd au redémarrage.

**Solution 1 : ARandR (interface graphique pour xrandr)**

```bash
# Installer
sudo apt install arandr

# Lancer
arandr
```

1. Configurez vos écrans graphiquement
2. **Layout** → **Save As**
3. Sauvegardez le script (exemple : `mon-setup.sh`)

**Appliquer au démarrage :**

Menu → Préférences → **Applications au démarrage**

Ajoutez :
- Nom : Multi-écrans
- Commande : `sh /home/votre-nom/mon-setup.sh`

---

**Solution 2 : Script xrandr permanent**

```bash
# Créer le script
nano ~/.config/monitors.sh

# Ajouter votre configuration xrandr (exemple) :
#!/bin/bash
xrandr --output eDP-1 --mode 1920x1080 --primary
xrandr --output HDMI-1 --mode 1920x1080 --right-of eDP-1

# Rendre exécutable
chmod +x ~/.config/monitors.sh

# Ajouter au démarrage (voir ci-dessus)
```

---

### Problème : Écran externe non détecté

**Vérifications :**

1. **Câble bien branché** (évident mais important)
2. **Bon port utilisé** (HDMI, DisplayPort, USB-C)
3. **Écran allumé** et sur la bonne source

**Diagnostic :**

```bash
# Forcer la détection
xrandr --auto

# Voir tous les ports disponibles
xrandr --query
```

**Si l'écran n'apparaît toujours pas :**

```bash
# Vérifier que le port est détecté par le système
cat /sys/class/drm/card*/card*-*/status

# Devrait afficher "connected" pour les écrans branchés
```

**Solutions :**

```bash
# Redémarrer le serveur graphique (Ctrl+Alt+F2 puis) :
sudo systemctl restart lightdm

# Ou forcer le rechargement du pilote (exemple NVIDIA) :
sudo rmmod nvidia_drm nvidia_modeset nvidia
sudo modprobe nvidia nvidia_modeset nvidia_drm
```

---

## Déchirure d'écran (Screen Tearing)

Problème très courant où l'image semble "coupée" horizontalement.

### Solution 1 : Activer Vsync dans Cinnamon

Menu → Préférences → **Paramètres système** → **Général**

Cochez **"Vsync"** (si disponible)

Ou dans les effets :
Menu → Préférences → **Effets**

Activez la synchronisation verticale.

---

### Solution 2 : Forcer le compositeur

```bash
# Vérifier que le compositeur est actif
pgrep -a cinnamon

# Le redémarrer
killall cinnamon
nohup cinnamon --replace &
```

---

### Solution 3 : Configuration par fabricant

Voir les sections NVIDIA, AMD, Intel ci-dessus pour :
- **NVIDIA** : ForceCompositionPipeline
- **AMD** : Option TearFree
- **Intel** : Option TearFree

---

## Problèmes avec Wayland vs X11

Linux Mint utilise X11 par défaut, mais Wayland est disponible expérimentalement.

### Vérifier votre session actuelle

```bash
echo $XDG_SESSION_TYPE
```

**Résultat :**
- **x11** : Session X11 (défaut)
- **wayland** : Session Wayland

---

### Passer de X11 à Wayland (ou inversement)

À l'écran de connexion :
1. Entrez votre nom d'utilisateur
2. **AVANT** de taper le mot de passe
3. Cliquez sur l'icône engrenage (session)
4. Sélectionnez "Cinnamon (Wayland)" ou "Cinnamon"
5. Connectez-vous

---

### Problèmes spécifiques Wayland

**Avantages Wayland :**
- Meilleure sécurité
- Pas de tearing par défaut
- Meilleure gestion HiDPI

**Problèmes courants Wayland :**
- Certaines applications ne fonctionnent pas (notamment avec NVIDIA)
- Enregistrement d'écran limité
- Partage d'écran Discord/Zoom problématique

**Recommandation :** Restez sur X11 avec Linux Mint, sauf si vous avez une raison spécifique.

---

## Outils de diagnostic graphique

### glxinfo (informations OpenGL)

```bash
# Installer
sudo apt install mesa-utils

# Informations OpenGL
glxinfo | grep "OpenGL"

# Version OpenGL
glxinfo | grep "OpenGL version"

# Renderer utilisé
glxinfo | grep "OpenGL renderer"
```

**Si "llvmpipe" apparaît** → Vous utilisez le rendu logiciel (pas d'accélération matérielle) !

---

### glxgears (test de performances)

```bash
glxgears
```

Une fenêtre avec des engrenages tournants s'affiche. Le FPS s'affiche dans le terminal.

**Interprétation :**
- **> 1000 FPS** : Accélération matérielle active (bon)
- **< 60 FPS** : Rendu logiciel ou problème (mauvais)

**Note :** glxgears n'est pas un vrai benchmark, juste un test de base.

---

### nvidia-smi (monitoring NVIDIA)

```bash
nvidia-smi

# En continu (rafraîchissement)
watch -n 1 nvidia-smi
```

**Informations affichées :**
- Température GPU
- Utilisation GPU (%)
- Mémoire VRAM utilisée
- Processus utilisant le GPU

---

### radeontop (monitoring AMD)

```bash
sudo apt install radeontop
radeontop
```

Équivalent de nvidia-smi pour AMD.

---

### intel_gpu_top (monitoring Intel)

```bash
sudo apt install intel-gpu-tools
sudo intel_gpu_top
```

Monitoring pour cartes Intel.

---

### xrandr (configuration affichage)

```bash
# Informations complètes
xrandr --verbose

# Juste les résolutions
xrandr | grep '*'
```

---

## Problèmes de couleurs

### Symptôme : Couleurs bizarres ou délavées

**Vérifier la profondeur de couleur :**

```bash
xdpyinfo | grep "depth of root"
```

**Devrait être :** 24 ou 32

**Si 16 :** Configuration incorrecte

```bash
sudo nano /etc/X11/xorg.conf.d/10-color.conf

# Ajouter :
Section "Screen"
    Identifier "Screen0"
    DefaultDepth 24
EndSection

# Redémarrer
sudo reboot
```

---

### Symptôme : Gamma ou luminosité incorrecte

**Ajuster le gamma avec xrandr :**

```bash
# Augmenter la luminosité (1.0 = normal, 1.5 = +50%)
xrandr --output HDMI-1 --brightness 1.2

# Ajuster le gamma (R:G:B)
xrandr --output HDMI-1 --gamma 1.0:0.9:0.8
```

**Rendre permanent :**

Ajoutez la commande dans votre script de démarrage (voir multi-écrans).

---

### Gestion des profils de couleur

```bash
# Installer les outils de gestion de couleur
sudo apt install gnome-color-manager

# Lancer
gnome-control-center color
```

Vous pouvez importer des profils ICC pour calibrer votre écran.

---

## Mode sans échec graphique (nomodeset)

Le paramètre **nomodeset** désactive le pilote kernel mode setting et force un mode graphique basique.

### Quand l'utiliser ?

- Écran noir au démarrage
- Impossible de démarrer l'interface graphique
- Après installation d'un pilote problématique

### Comment l'utiliser ?

**Temporaire (une seule fois) :**

1. Au menu GRUB, sélectionnez Linux Mint
2. Appuyez sur **'e'** pour éditer
3. Trouvez la ligne `linux /boot/vmlinuz...`
4. À la fin (après `quiet splash`), ajoutez : `nomodeset`
5. Appuyez sur **F10** pour démarrer

---

**Permanent (jusqu'à correction) :**

```bash
# Depuis un démarrage en nomodeset ou recovery
sudo nano /etc/default/grub

# Modifier la ligne :
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"

# Mettre à jour GRUB
sudo update-grub

# Redémarrer
sudo reboot
```

**⚠️ Important :** nomodeset est un **dépannage temporaire**. Vous devez ensuite corriger le problème de pilote et retirer nomodeset.

---

## Réinitialiser la configuration graphique

Si tout est cassé et que vous voulez repartir de zéro :

### Supprimer toutes les configurations X11

```bash
# Sauvegarder d'abord (au cas où)
sudo cp -r /etc/X11 /etc/X11.backup

# Supprimer les configurations personnalisées
sudo rm -rf /etc/X11/xorg.conf
sudo rm -rf /etc/X11/xorg.conf.d/*.conf

# Laisser le système reconfigurer automatiquement
sudo dpkg-reconfigure xserver-xorg

# Redémarrer
sudo reboot
```

---

### Réinitialiser les paramètres Cinnamon

```bash
# Réinitialiser TOUS les paramètres Cinnamon
dconf reset -f /org/cinnamon/

# Ou sauvegarder puis supprimer le dossier de config
mv ~/.cinnamon ~/.cinnamon.backup
mv ~/.config/cinnamon ~/.config/cinnamon.backup

# Redémarrer la session
```

---

## Cas particuliers

### Écrans HiDPI (4K, Retina)

**Problème :** Tout est trop petit sur un écran 4K.

**Solution :**

Menu → Préférences → **Affichage** → **Interface scaling** → **Double (HiDPI)**

Ou pour un scaling personnalisé :

```bash
# 150% de taille
gsettings set org.cinnamon.desktop.interface scaling-factor 2

# Dans ~/.Xresources pour les apps X11
echo "Xft.dpi: 144" >> ~/.Xresources
xrdb -merge ~/.Xresources
```

---

### Télévision comme écran (underscan/overscan)

**Problème :** L'image est coupée sur les bords de la TV.

**Solution (NVIDIA) :**

```bash
nvidia-settings
```

Allez dans **X Screen** → **ViewPortIn** et **ViewPortOut**, ajustez manuellement.

**Solution (AMD) :**

```bash
# Créer la configuration
sudo nano /etc/X11/xorg.conf.d/20-amdgpu.conf

# Ajouter :
Section "Device"
    Identifier "AMD"
    Driver "amdgpu"
    Option "underscan" "on"
    Option "underscan hborder" "48"
    Option "underscan vborder" "27"
EndSection

# Ajustez les valeurs hborder et vborder selon besoin
```

---

### VirtualBox (machine virtuelle)

**Problème :** Résolution bloquée à 1024×768 dans VirtualBox.

**Solution :**

```bash
# Installer les Guest Additions
# Dans VirtualBox : Périphériques → Insérer l'image CD des Additions invité

# Monter le CD
sudo mkdir /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom

# Installer
cd /mnt/cdrom
sudo sh ./VBoxLinuxAdditions.run

# Redémarrer
sudo reboot
```

Après redémarrage, la résolution devrait s'adapter automatiquement.

---

### Carte graphique non reconnue (très récente)

Pour du matériel très récent, les pilotes du système peuvent être trop vieux.

**Solution : Utiliser un PPA avec pilotes récents**

**Pour NVIDIA :**

```bash
# PPA Graphics Drivers
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update

# Lister les nouveaux pilotes disponibles
ubuntu-drivers list

# Installer le plus récent
sudo apt install nvidia-driver-550  # Exemple

# Redémarrer
sudo reboot
```

**Pour AMD :**

Le pilote amdgpu est dans le kernel. Mettez à jour le kernel :

```bash
# Installer le kernel le plus récent via Update Manager
# Ou utiliser ukuu pour kernel mainline
```

---

## FAQ - Questions fréquentes

### Comment savoir si j'utilise bien mon pilote graphique ?

```bash
glxinfo | grep "OpenGL renderer"
```

**Bon signe :**
- NVIDIA GeForce [modèle]
- AMD Radeon [modèle]
- Intel HD/UHD Graphics [modèle]

**Mauvais signe :**
- llvmpipe (rendu logiciel, très lent)

---

### Est-ce que le pilote open source (nouveau) est suffisant pour NVIDIA ?

**Pour bureautique :** Oui, largement suffisant.

**Pour gaming/3D :** Non, le pilote propriétaire nvidia est indispensable pour de bonnes performances.

**Différence de performance :** ~50-70% moins de FPS avec nouveau vs nvidia.

---

### Pourquoi mes jeux sont lents alors que j'ai une bonne carte graphique ?

**Vérifications :**

1. **Bon pilote installé ?** (nvidia propriétaire, pas nouveau)
2. **GPU réellement utilisé ?** (vérifier avec `nvidia-smi` pendant le jeu)
3. **Vsync activé ?** (peut limiter les FPS)
4. **Résolution trop élevée ?**

---

### Mon écran externe fonctionne en HDMI mais pas en DisplayPort

**Causes probables :**
- Câble DP défectueux (plus fragile que HDMI)
- Version DP incompatible (1.2 vs 1.4)
- Détection EDID échouée

**Solutions :**
- Tester un autre câble DP
- Forcer la détection avec `xrandr --auto`
- Vérifier les paramètres de l'écran (mode DP 1.2 activé ?)

---

### Dois-je désactiver Secure Boot pour que les pilotes NVIDIA fonctionnent ?

**Pas forcément**, mais ça peut aider.

**Options :**
1. **Désactiver Secure Boot** dans le BIOS (plus simple)
2. **Signer les modules NVIDIA** (plus complexe mais garde Secure Boot)

Pour signer (avancé) :
```bash
sudo apt install mokutil
sudo mokutil --import /var/lib/shim-signed/mok/MOK.der
```

---

### Mon écran clignote au démarrage, c'est grave ?

**Probablement non**, c'est le passage du mode texte au mode graphique.

**Clignotements normaux :**
- Logo fabricant → écran noir → Logo Linux Mint → Bureau

**Clignotements anormaux :**
- Écran qui flashe en continu pendant l'utilisation
- Artefacts visuels qui persistent

---

## Commandes de référence rapide

### Identification

```bash
# Carte graphique
lspci | grep -i vga
inxi -G

# Pilote actuel
lsmod | grep -i nvidia  # NVIDIA
lsmod | grep -i amdgpu  # AMD
lsmod | grep -i i915    # Intel

# Renderer OpenGL
glxinfo | grep "OpenGL renderer"

# Session (X11 ou Wayland)
echo $XDG_SESSION_TYPE
```

### Tests

```bash
# Test OpenGL basique
glxgears

# Infos OpenGL
glxinfo | head -20

# Résolutions disponibles
xrandr
```

### Configuration

```bash
# Gestionnaire de pilotes
driver-manager

# Configuration NVIDIA
nvidia-settings

# Configuration multi-écrans graphique
arandr

# Résolution temporaire
xrandr --output HDMI-1 --mode 1920x1080

# Brightness temporaire
xrandr --output HDMI-1 --brightness 1.2
```

### Dépannage

```bash
# Redémarrer serveur graphique
sudo systemctl restart lightdm

# Désinstaller NVIDIA
sudo apt remove --purge nvidia-*
sudo apt autoremove

# Reconfigurer X11
sudo dpkg-reconfigure xserver-xorg

# Logs graphiques
cat /var/log/Xorg.0.log | grep -i error
journalctl -b | grep -i gpu
```

---

## Tableau récapitulatif des pilotes

| Fabricant | Carte | Pilote recommandé | Installation |
|-----------|-------|-------------------|--------------|
| NVIDIA | Toutes | nvidia (propriétaire) | Gestionnaire de pilotes |
| NVIDIA | < GTX 600 | nvidia-470 | `sudo apt install nvidia-driver-470` |
| NVIDIA | GTX 600-900 | nvidia-535 | `sudo apt install nvidia-driver-535` |
| NVIDIA | RTX série | nvidia-545+ | Gestionnaire de pilotes |
| AMD | < RX 400 | radeon | Pré-installé |
| AMD | RX 400+ | amdgpu | Pré-installé |
| AMD | Workstation | amdgpu-pro | Site AMD |
| Intel | Toutes | i915 | Pré-installé |

---

## Checklist de dépannage graphique

**☐ 1. Identifier la carte graphique**
```bash
lspci | grep -i vga
```

**☐ 2. Vérifier le pilote actuel**
```bash
inxi -G
glxinfo | grep "OpenGL renderer"
```

**☐ 3. Installer le bon pilote si nécessaire**
- Via Gestionnaire de pilotes
- Ou manuellement

**☐ 4. Redémarrer après installation pilote**

**☐ 5. Si problème persiste :**
- Tester en nomodeset
- Vérifier les logs : `/var/log/Xorg.0.log`
- Chercher l'erreur spécifique

**☐ 6. Pour problèmes de résolution :**
- Vérifier avec `xrandr`
- Créer mode personnalisé si besoin

**☐ 7. Pour déchirure d'écran :**
- Activer Vsync / TearFree
- Configuration spécifique fabricant

**☐ 8. Si tout échoue :**
- Réinitialiser configuration X11
- Utiliser pilote générique temporairement
- Demander de l'aide sur forums avec logs

---

## Conclusion

Les problèmes graphiques sous Linux Mint peuvent sembler intimidants, mais la majorité ont des solutions bien documentées :

**Points clés à retenir :**

1. **Identifiez votre matériel** avant toute chose (lspci, inxi)
2. **Le Gestionnaire de pilotes** résout 80% des problèmes
3. **NVIDIA** nécessite le pilote propriétaire pour de bonnes performances
4. **AMD et Intel** fonctionnent bien avec pilotes open source
5. **nomodeset** est votre bouée de sauvetage en cas d'écran noir
6. **xrandr** est l'outil universel pour gérer résolutions et multi-écrans
7. **Les logs** (/var/log/Xorg.0.log) contiennent les réponses

**Méthodologie :**
- Diagnostiquer (quel GPU, quel pilote actuel ?)
- Installer le bon pilote
- Configurer (résolution, multi-écrans, optimisations)
- Tester et affiner

Avec ces connaissances, vous pouvez résoudre la grande majorité des problèmes graphiques sous Linux Mint, du simple réglage de résolution à la configuration complexe de multi-GPU.

---

## Ressources complémentaires

- [Ubuntu Wiki - Graphics](https://wiki.ubuntu.com/X)
- [NVIDIA Linux Drivers](https://www.nvidia.com/en-us/drivers/unix/)
- [AMD Linux Drivers](https://www.amd.com/en/support/linux-drivers)
- [Arch Wiki - Xorg](https://wiki.archlinux.org/title/Xorg)
- [Forums Linux Mint](https://forums.linuxmint.com/)

---

⏭️ [Lecture et compréhension des logs (journalctl, /var/log)](/23-depannage-et-resolution-de-problemes/07-lecture-et-comprehension-des-logs.md)
