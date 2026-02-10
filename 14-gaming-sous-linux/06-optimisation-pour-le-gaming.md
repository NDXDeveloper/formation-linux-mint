🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 14.6 Optimisation pour le gaming

## Introduction

L'optimisation gaming consiste à configurer votre système Linux Mint pour obtenir les meilleures performances possibles dans vos jeux. Contrairement à une idée reçue, Linux peut égaler voire surpasser Windows en performances gaming avec la bonne configuration.

**Optimisation gaming, c'est :**
- Installer les bons pilotes graphiques
- Configurer le système pour prioriser les performances
- Utiliser des outils d'optimisation automatique
- Réduire la latence et augmenter les FPS
- Surveiller et diagnostiquer les problèmes
- Ajuster les paramètres selon votre matériel

## Pilotes graphiques : La base absolue

Les pilotes graphiques sont le facteur le plus important pour les performances gaming. Sans les bons pilotes, vos jeux seront lents, même sur un PC puissant.

### Identifier votre carte graphique

**En ligne de commande** :
```bash
# Voir votre GPU
lspci | grep -i vga

# Plus de détails
lspci -v | grep -A 12 VGA

# Ou simplement
inxi -G
```

**Via l'interface graphique** :
1. **Menu** → **Préférences** → **Informations système**
2. Section **Graphiques**

### NVIDIA : Pilotes propriétaires obligatoires

Les cartes NVIDIA **nécessitent** les pilotes propriétaires pour le gaming.

#### Installation automatique (recommandée)

1. **Menu** → **Administration** → **Gestionnaire de pilotes**
2. Attendez que le système détecte votre carte
3. Sélectionnez le pilote recommandé :
   - **nvidia-driver-XXX** (numéro de version le plus élevé)
   - Généralement **nvidia-driver-535** ou plus récent
4. Cliquez sur **Appliquer les changements**
5. **Redémarrez votre ordinateur**

#### Installation manuelle

```bash
# Ajouter le PPA des pilotes graphiques
sudo add-apt-repository ppa:graphics-drivers/ppa  
sudo apt update  

# Installer le pilote recommandé
sudo ubuntu-drivers autoinstall

# Ou installer une version spécifique
sudo apt install nvidia-driver-535

# Redémarrer
sudo reboot
```

#### Vérifier l'installation

```bash
# Vérifier que le pilote NVIDIA est chargé
nvidia-smi
```

Vous devriez voir des informations sur votre GPU, la version du pilote, etc.

#### NVIDIA Settings (configuration)

```bash
# Lancer l'interface de configuration
nvidia-settings
```

**Paramètres recommandés pour le gaming** :
1. **PowerMizer** → **Preferred Mode** : **Prefer Maximum Performance**
2. **OpenGL Settings** → **Sync to VBlank** : OFF (pour plus de FPS)
3. **Antialiasing Settings** : Laissez les applications contrôler

### AMD : Mesa open-source (excellent)

Les cartes AMD fonctionnent excellemment avec les pilotes open-source Mesa.

#### Pilotes par défaut

Linux Mint installe automatiquement les meilleurs pilotes AMD :
- **Mesa** : Pilotes open-source (recommandé)
- **AMDGPU** : Driver kernel moderne

**Aucune action nécessaire** dans la plupart des cas !

#### Vérifier les pilotes AMD

```bash
# Vérifier le pilote utilisé
glxinfo | grep "OpenGL renderer"

# Devrait afficher quelque chose comme :
# OpenGL renderer string: AMD Radeon RX 6800 (NAVI21, DRM 3.XX, ...)
```

#### Optimisations AMD

**Variables d'environnement recommandées** :

```bash
# Créer un fichier de configuration
sudo nano /etc/environment
```

Ajoutez :
```
RADV_PERFTEST=aco  
AMD_VULKAN_ICD=RADV  
```

**Explication** :
- **aco** : Compilateur shader AMD optimisé
- **RADV** : Driver Vulkan open-source

Redémarrez après modification.

#### Mesa-git (pilotes dernière génération)

Pour les cartes AMD très récentes :

```bash
# Ajouter le PPA Mesa
sudo add-apt-repository ppa:kisak/kisak-mesa  
sudo apt update  
sudo apt upgrade  
```

> **Attention** : Plus récent = potentiellement moins stable. Recommandé uniquement si vous avez des problèmes.

### Intel (GPU intégré)

Les GPU Intel utilisent aussi Mesa et fonctionnent bien par défaut.

**Optimisation Intel** :

```bash
# Vérifier le driver
glxinfo | grep "OpenGL renderer"

# Devrait afficher : Intel HD Graphics XXXX ou Intel Iris
```

**Variables d'environnement** :

```bash
sudo nano /etc/environment
```

Ajoutez :
```
INTEL_DEBUG=perf
```

### Configuration multi-GPU (Laptops avec GPU dédié)

Beaucoup de laptops ont deux GPU :
- GPU intégré (Intel) : Économie d'énergie
- GPU dédié (NVIDIA/AMD) : Performances

#### NVIDIA Optimus / AMD Switchable Graphics

**PRIME Render Offload** (NVIDIA) :

```bash
# Lancer un jeu avec le GPU NVIDIA
__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia %command%
```

**Pour Steam** :
1. Bibliothèque → Clic droit sur le jeu → **Propriétés**
2. **Options de lancement** :
   ```
   __NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia %command%
   ```

**Vérifier quel GPU est utilisé** :

```bash
# Lancer glxinfo et vérifier
__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia glxinfo | grep "OpenGL renderer"
```

## GameMode : Optimisation automatique

GameMode est un outil développé par Feral Interactive qui optimise automatiquement votre système pendant le jeu.

### Qu'est-ce que GameMode fait ?

- **Priorise le CPU** pour le jeu
- **Désactive le screensaver** automatiquement
- **Ajuste le gouverneur CPU** à performance
- **Optimise les processus** en arrière-plan
- **Améliore le scheduling** des threads
- **Active des optimisations GPU** (si configuré)

### Installation

```bash
# Installer GameMode
sudo apt install gamemode

# Vérifier l'installation
gamemoded -s
```

Devrait afficher : **gamemode is active** ou **gamemode is inactive** (normal si aucun jeu ne tourne).

### Utilisation

**Sur Steam** :
1. Bibliothèque → Clic droit sur le jeu → **Propriétés**
2. **Options de lancement** : `gamemoderun %command%`

**Sur Lutris** :
1. Clic droit sur le jeu → **Configure**
2. **System options** → **Enable Feral GameMode** : ON

**Sur Heroic** :
1. Paramètres du jeu → **Advanced**
2. **Enable GameMode** : ON

**En ligne de commande** :
```bash
# Lancer n'importe quel programme avec GameMode
gamemoderun ./mon-jeu
```

### Vérifier que GameMode fonctionne

```bash
# Pendant qu'un jeu tourne avec GameMode
gamemoded -s

# Devrait afficher : gamemode is active
```

### Configuration avancée GameMode

```bash
# Créer un fichier de configuration personnalisé
mkdir -p ~/.config  
nano ~/.config/gamemode.ini  
```

**Configuration recommandée** :

```ini
[general]
; GameMode toujours disponible
renice=10

[gpu]
; Pour NVIDIA : overclock léger (optionnel)
apply_gpu_optimisations=accept-responsibility  
gpu_device=0  
amd_performance_level=high  

[cpu]
; Passer le CPU en mode performance
park_cores=no  
pin_policy=prefer-physical  

[custom]
; Scripts personnalisés (optionnel)
start=notify-send "GameMode activé"  
end=notify-send "GameMode désactivé"  
```

## Gouverneur CPU

Le gouverneur CPU contrôle la fréquence du processeur.

### Modes disponibles

- **powersave** : Économie d'énergie (par défaut)
- **performance** : Performance maximale
- **ondemand** : Ajustement dynamique
- **schedutil** : Moderne, ajustement intelligent

### Vérifier le gouverneur actuel

```bash
cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
```

### Changer le gouverneur

**Temporaire (jusqu'au redémarrage)** :

```bash
# Passer en mode performance
echo performance | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
```

**Permanent** :

```bash
# Installer cpufrequtils
sudo apt install cpufrequtils

# Configurer
sudo nano /etc/default/cpufrequtils
```

Ajoutez :
```
GOVERNOR="performance"
```

Redémarrez ou :
```bash
sudo systemctl restart cpufrequtils
```

> **Note** : GameMode fait cela automatiquement pendant le jeu.

### GUI pour gérer le gouverneur

```bash
# Installer indicator-cpufreq
sudo apt install indicator-cpufreq
```

Une icône apparaît dans la barre système pour changer facilement le gouverneur.

## Optimisations système

### Swappiness (gestion de la mémoire virtuelle)

Le swappiness contrôle à quel point le système utilise le swap.

**Valeur par défaut** : 60  
**Recommandé pour gaming** : 10  

```bash
# Vérifier la valeur actuelle
cat /proc/sys/vm/swappiness

# Changer temporairement
sudo sysctl vm.swappiness=10

# Changer définitivement
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
```

### Cache Pressure

Contrôle la conservation des caches en mémoire.

```bash
# Recommandé pour gaming
echo "vm.vfs_cache_pressure=50" | sudo tee -a /etc/sysctl.conf
```

### Désactiver watchdog (laptops)

Le watchdog système peut créer des micro-stutters.

```bash
# Désactiver temporairement
sudo modprobe -r iTCO_wdt iTCO_vendor_support

# Désactiver définitivement
echo "blacklist iTCO_wdt" | sudo tee /etc/modprobe.d/blacklist-watchdog.conf  
echo "blacklist iTCO_vendor_support" | sudo tee -a /etc/modprobe.d/blacklist-watchdog.conf  
```

Redémarrez.

### Désactiver Mitigations (boost de performance)

Les mitigations protègent contre Spectre/Meltdown mais réduisent les performances (~10-20%).

> **Attention** : Réduit la sécurité. À faire en connaissance de cause.

```bash
# Éditer GRUB
sudo nano /etc/default/grub
```

Trouvez la ligne `GRUB_CMDLINE_LINUX_DEFAULT` et ajoutez `mitigations=off` :

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash mitigations=off"
```

Mettez à jour GRUB :
```bash
sudo update-grub  
sudo reboot  
```

### Augmenter les limites de fichiers ouverts

Certains jeux peuvent atteindre la limite de fichiers.

```bash
# Vérifier la limite actuelle
ulimit -n

# Augmenter temporairement
ulimit -n 524288

# Augmenter définitivement
echo "* soft nofile 524288" | sudo tee -a /etc/security/limits.conf  
echo "* hard nofile 524288" | sudo tee -a /etc/security/limits.conf  
```

### Optimisation Esync/Fsync

**Esync** et **Fsync** améliorent les performances Wine/Proton.

**Fsync** (kernel 5.16+) :
```bash
# Vérifier le support
uname -r

# Si > 5.16, Fsync est supporté automatiquement
```

**Pour l'activer** (Steam/Proton) :
1. Paramètres du jeu → **Options de lancement** : `PROTON_NO_ESYNC=0 PROTON_NO_FSYNC=0 %command%`

**Augmenter la limite Esync** :

```bash
# Éditer les limites
sudo nano /etc/security/limits.conf
```

Ajoutez :
```
yourusername hard nofile 524288
```

Remplacez `yourusername` par votre nom d'utilisateur.

## Optimisation réseau (gaming en ligne)

### Réduire la latence réseau

```bash
# Éditer sysctl
sudo nano /etc/sysctl.conf
```

Ajoutez :
```
# TCP optimizations for gaming
net.ipv4.tcp_fastopen=3  
net.ipv4.tcp_low_latency=1  
net.ipv4.tcp_timestamps=0  
net.core.netdev_max_backlog=16384  
net.core.rmem_default=1048576  
net.core.rmem_max=16777216  
net.core.wmem_default=1048576  
net.core.wmem_max=16777216  
net.ipv4.tcp_rmem=4096 1048576 2097152  
net.ipv4.tcp_wmem=4096 65536 16777216  
```

Appliquez :
```bash
sudo sysctl -p
```

### QoS (Quality of Service)

Priorise le trafic gaming sur votre réseau.

**Méthode simple via router** :
1. Accédez à votre routeur (généralement 192.168.1.1)
2. Cherchez **QoS** ou **Qualité de Service**
3. Priorisez votre PC/IP pour le gaming

## Optimisation SSD

### Activer TRIM

TRIM améliore les performances et la longévité des SSD.

```bash
# Vérifier si TRIM est supporté
sudo fstrim -v /

# Activer TRIM hebdomadaire automatique
sudo systemctl enable fstrim.timer  
sudo systemctl start fstrim.timer  
```

### Désactiver l'indexation (optionnel)

```bash
# Vérifier si noatime est activé
mount | grep "on / "

# Si absent, ajouter noatime
sudo nano /etc/fstab
```

Modifiez la ligne du système de fichiers racine :
```
UUID=xxx / ext4 defaults,noatime 0 1
```

> **Note** : noatime réduit les écritures SSD et améliore légèrement les performances.

## Paramètres de jeu

### Résolution et fullscreen

**Recommandations** :
- **Fullscreen exclusif** : Meilleures performances que borderless
- **Résolution native** : Évitez le scaling
- **VSync** : OFF pour plus de FPS (mais screen tearing possible)
- **G-Sync/FreeSync** : ON si votre écran le supporte

### Paramètres graphiques

**Prioriser ces paramètres** (impact sur FPS) :

**Impact ÉNORME** :
- Résolution
- Anti-aliasing (MSAA/SSAA)
- Ombres
- Ray-tracing

**Impact MOYEN** :
- Textures (si VRAM limitée)
- Post-processing
- Distance d'affichage

**Impact FAIBLE** :
- Anisotropic filtering
- Détails de texture
- Effets de particules

**Stratégie** :
1. Commencez en **Medium**
2. Augmentez progressivement
3. Visez 60 FPS minimum (ou 144 si écran 144Hz)

### FPS vs Qualité

**60 FPS** : Minimum pour gaming fluide  
**144 FPS** : Idéal pour écran 144Hz  
**30 FPS** : Acceptable pour RPG/stratégie  

**Monitorer les FPS** : Utilisez MangoHud (voir section suivante).

## Monitoring des performances

### MangoHud : Overlay de performances

MangoHud affiche FPS, utilisation CPU/GPU, température, etc.

#### Installation

```bash
sudo apt install mangohud
```

#### Utilisation

**Steam** :
```
Options de lancement : mangohud %command%
```

**Lutris** :
- Activer **MangoHud** dans les options système

**Heroic** :
- Activer **MangoHud** dans les paramètres du jeu

**Ligne de commande** :
```bash
mangohud ./mon-jeu
```

#### Raccourcis clavier

- **Shift+F12** : Afficher/masquer l'overlay
- **Shift+F2** : Changer de position
- **Shift+F4** : Recharger la configuration

#### Configuration MangoHud

```bash
# Créer le fichier de config
mkdir -p ~/.config/MangoHud  
nano ~/.config/MangoHud/MangoHud.conf  
```

**Configuration recommandée** :

```ini
# Position
position=top-left

# Informations affichées
fps  
gpu_stats  
gpu_temp  
cpu_stats  
cpu_temp  
ram  
vram  
frame_timing=1  

# Apparence
font_size=24  
background_alpha=0.4  

# Limite FPS (optionnel)
fps_limit=144
```

### htop : Monitoring système

```bash
# Installer htop
sudo apt install htop

# Lancer
htop
```

**Raccourcis** :
- **F5** : Vue arborescente
- **Espace** : Taguer un processus
- **F9** : Tuer un processus
- **F10** : Quitter

### nvtop : GPU monitoring

Pour surveiller l'utilisation GPU.

```bash
# Installer nvtop
sudo apt install nvtop

# Lancer
nvtop
```

Fonctionne avec NVIDIA et AMD.

### glxinfo et vulkaninfo

**Vérifier OpenGL** :
```bash
glxinfo | grep "OpenGL"
```

**Vérifier Vulkan** :
```bash
vulkaninfo | head -n 20
```

## Désactiver les effets visuels

Cinnamon a de beaux effets mais qui consomment des ressources.

### Désactiver les effets

1. **Menu** → **Préférences** → **Effets**
2. Désactivez :
   - Transitions de fenêtres
   - Effets de maximisation
   - Ombres portées (optionnel)

Ou désactivez complètement :
```bash
# Désactiver les effets Cinnamon
cinnamon-settings effects
```

## Processus en arrière-plan

### Identifier les processus gourmands

```bash
# Voir les processus par utilisation CPU
top
# Ou mieux :
htop
```

### Désactiver services inutiles

```bash
# Voir tous les services
systemctl list-unit-files --type=service

# Désactiver un service
sudo systemctl disable nom-du-service  
sudo systemctl stop nom-du-service  
```

**Services potentiellement inutiles pour le gaming** :
- **cups** (impression) : Si pas d'imprimante
- **bluetooth** : Si pas de Bluetooth
- **avahi-daemon** : Découverte réseau locale

**Exemple** :
```bash
sudo systemctl disable cups  
sudo systemctl stop cups  
```

> **Attention** : Ne désactivez que ce dont vous êtes sûr de ne pas avoir besoin.

## Température et refroidissement

### Monitorer la température

```bash
# Installer sensors
sudo apt install lm-sensors

# Détecter les capteurs
sudo sensors-detect

# Voir les températures
sensors
```

**Températures saines** :
- **CPU** : <80°C en charge
- **GPU** : <85°C en charge

### Améliorer le refroidissement

**Logiciel** :

```bash
# Installer TLP (gestion énergie laptop)
sudo apt install tlp tlp-rdw

# Activer
sudo tlp start

# Configuration
sudo nano /etc/tlp.conf
```

**TLP Gaming mode** :
```
CPU_SCALING_GOVERNOR_ON_AC=performance  
CPU_SCALING_GOVERNOR_ON_BAT=powersave  
```

**Physique** :
- Nettoyez les ventilateurs
- Pâte thermique (si ancien PC)
- Support laptop avec ventilation
- Undervolt CPU (avancé)

## Kernel optimisé gaming

### Kernel Xanmod

Kernel optimisé pour desktop et gaming.

```bash
# Ajouter le dépôt Xanmod
echo 'deb http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-kernel.list

# Ajouter la clé GPG
wget -qO - https://dl.xanmod.org/gpg.key | sudo apt-key add -

# Installer
sudo apt update  
sudo apt install linux-xanmod-x64v3  

# Redémarrer
sudo reboot
```

**Avantages** :
- Latence réduite
- Meilleures performances gaming
- Fsync intégré

**Vérifier le kernel** :
```bash
uname -r
# Devrait afficher : x.xx.x-xanmod1
```

### Kernel Liquorix (alternative)

Autre kernel optimisé.

```bash
# Ajouter le dépôt
sudo add-apt-repository ppa:damentz/liquorix  
sudo apt update  

# Installer
sudo apt install linux-image-liquorix-amd64

# Redémarrer
sudo reboot
```

> **Note** : Testez. Si problèmes, revenez au kernel standard via GRUB au boot.

## Overclocking (Avancé - Prudence)

### NVIDIA

```bash
# Activer l'overclocking
sudo nvidia-xconfig --cool-bits=28

# Redémarrer
sudo reboot

# Utiliser nvidia-settings
nvidia-settings
```

Onglet **PowerMizer** : Ajustez GPU clock, Memory clock.

> **Attention** : Augmentez progressivement (+25MHz à la fois), testez la stabilité.

### AMD

AMD overclocking nécessite CoreCtrl.

```bash
# Installer CoreCtrl
sudo apt install corectrl

# Lancer
corectrl
```

Créez un profil gaming avec fréquences augmentées.

> **Attention** : L'overclocking peut endommager le matériel. À vos risques et périls.

## Optimisation RAM

### Dual Channel

**Vérifiez** :
- 2 barrettes RAM identiques
- Slots corrects (consultez manuel carte mère)
- Dual channel = ~20% de performances en plus

### XMP/DOCP Profile

Active les fréquences RAM annoncées.

**Dans le BIOS** :
1. Redémarrez → Touche DEL/F2 pour BIOS
2. Cherchez **XMP** (Intel) ou **DOCP** (AMD)
3. Activez le profil
4. Sauvegardez et redémarrez

## Liste de vérification optimisation

### Checklist débutant (essentiel)

- [ ] Pilotes graphiques propriétaires installés (NVIDIA)
- [ ] GameMode installé et activé
- [ ] Gouverneur CPU en performance (ou géré par GameMode)
- [ ] Swappiness à 10
- [ ] Effets visuels réduits
- [ ] Processus inutiles fermés pendant le jeu

### Checklist intermédiaire

- [ ] TRIM activé (SSD)
- [ ] Fsync/Esync configuré
- [ ] MangoHud installé (monitoring)
- [ ] Optimisations réseau appliquées
- [ ] XMP/DOCP activé (BIOS)
- [ ] Températures monitorées

### Checklist avancée

- [ ] Kernel optimisé (Xanmod/Liquorix)
- [ ] Mitigations désactivées (si accepté)
- [ ] Variables AMD/NVIDIA optimisées
- [ ] Configuration GameMode personnalisée
- [ ] TLP configuré (laptop)

## Benchmarking

### Tester les améliorations

**Avant/Après chaque optimisation** :

1. **Unigine Heaven** (benchmark gratuit)
   ```bash
   # Télécharger depuis unigine.com
   ```

2. **glxgears** (test simple)
   ```bash
   vblank_mode=0 glxgears
   # Note les FPS
   ```

3. **Un jeu que vous connaissez**
   - Même zone
   - Même paramètres
   - Notez les FPS (avec MangoHud)

**Gardez des notes** :
- FPS moyen
- FPS minimum
- Utilisation CPU/GPU
- Température

## Problèmes de performance courants

### FPS bas malgré bon matériel

**Causes** :
1. Pas de pilote propriétaire (NVIDIA)
2. Utilise le GPU intégré au lieu du dédié
3. V-Sync activé limitant à 60 FPS
4. Gouverneur CPU en powersave
5. Surchauffe (throttling)

**Solutions** :
- Vérifiez le pilote : `nvidia-smi` ou `glxinfo`
- Forcez le GPU dédié (voir section multi-GPU)
- Désactivez V-Sync
- Activez GameMode
- Vérifiez températures : `sensors`

### Micro-stutters

**Causes** :
- Swap utilisé
- Processus en arrière-plan
- Shader compilation
- Gouverneur CPU instable

**Solutions** :
- Swappiness à 10
- Fermez les applications inutiles
- Attendez la fin de la compilation (première session)
- GameMode

### Latence souris/clavier

**Causes** :
- V-Sync
- Trop de FPS (GPU saturé)
- USB polling rate bas

**Solutions** :
- Désactivez V-Sync
- Limitez les FPS (200-240 max)
- Branchez périphériques USB 2.0 sur port USB 2.0

### Artefacts graphiques

**Causes** :
- Pilote corrompu
- Overclocking instable
- Surchauffe GPU

**Solutions** :
- Réinstallez le pilote
- Réduisez l'overclock
- Améliorez le refroidissement

## Scripts d'optimisation automatique

### Script "Gaming Mode"

Créez un script qui active tout automatiquement.

```bash
nano ~/gaming-mode.sh
```

Contenu :
```bash
#!/bin/bash

echo "🎮 Activation Gaming Mode..."

# Gouverneur CPU performance
echo performance | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor

# Swappiness
sudo sysctl vm.swappiness=10

# Fermer processus inutiles
killall -9 thunderbird 2>/dev/null  
killall -9 transmission-gtk 2>/dev/null  

# Notification
notify-send "Gaming Mode" "Système optimisé pour le gaming !"

echo "✅ Gaming Mode activé !"
```

Rendez-le exécutable :
```bash
chmod +x ~/gaming-mode.sh
```

Lancez avant de jouer :
```bash
./gaming-mode.sh
```

### Script "Normal Mode"

Pour revenir à la normale :

```bash
nano ~/normal-mode.sh
```

Contenu :
```bash
#!/bin/bash

echo "🔄 Retour mode normal..."

# Gouverneur CPU powersave
echo powersave | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor

# Swappiness par défaut
sudo sysctl vm.swappiness=60

# Notification
notify-send "Mode Normal" "Configuration restaurée"

echo "✅ Mode normal activé !"
```

## Ressources et outils

### Sites utiles

**Benchmarks** :
- Phoronix Test Suite
- Unigine Benchmarks
- 3DMark (via Proton)

**Guides** :
- https://www.phoronix.com/
- https://www.gamingonlinux.com/
- https://wiki.archlinux.org/title/Gaming

### Outils recommandés

```bash
# Suite complète
sudo apt install \
    gamemode \
    mangohud \
    nvtop \
    htop \
    lm-sensors \
    cpufrequtils \
    linux-tools-common
```

## Conclusion

L'optimisation gaming sur Linux Mint est un processus progressif. Ne changez pas tout d'un coup, mais testez chaque optimisation individuellement pour mesurer son impact.

**Priorités par ordre d'importance** :

1. ⭐⭐⭐⭐⭐ **Pilotes graphiques** (NVIDIA propriétaires)
2. ⭐⭐⭐⭐⭐ **GameMode**
3. ⭐⭐⭐⭐ **Gouverneur CPU**
4. ⭐⭐⭐⭐ **Swappiness**
5. ⭐⭐⭐ **Fsync/Esync**
6. ⭐⭐⭐ **Effets visuels désactivés**
7. ⭐⭐ **Kernel optimisé**
8. ⭐⭐ **Optimisations réseau**
9. ⭐ **Overclocking** (risqué, gain marginal)

**Règles d'or** :
- ✅ Changez une chose à la fois
- ✅ Mesurez avant/après (MangoHud)
- ✅ Documentez ce qui fonctionne
- ✅ Gardez le système stable avant tout
- ✅ Sauvegardez avant les modifications majeures

Avec une configuration optimisée, Linux Mint peut égaler voire surpasser Windows en performances gaming. Bon gaming optimisé ! 🎮🚀

---

⏭️ [MangoHud pour monitoring en jeu](/14-gaming-sous-linux/07-mangohud-pour-monitoring-en-jeu.md)
