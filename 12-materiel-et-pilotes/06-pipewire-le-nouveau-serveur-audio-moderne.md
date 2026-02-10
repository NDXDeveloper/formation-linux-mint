🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 12.6 PipeWire : Le nouveau serveur audio moderne

## Introduction

**PipeWire** est le serveur audio et vidéo de nouvelle génération qui remplace progressivement PulseAudio et JACK sous Linux. Intégré à Linux Mint depuis la version 21, PipeWire apporte de nombreuses améliorations pour une expérience audio **plus simple, plus stable et plus performante**.

Ce chapitre vous explique ce qu'est PipeWire, comment l'utiliser, et pourquoi c'est une excellente nouvelle pour les utilisateurs Linux.

---

## Comprendre l'audio sous Linux

### Qu'est-ce qu'un serveur audio ?

Un **serveur audio** est un logiciel qui gère tout ce qui concerne le son sur votre ordinateur :

**Rôle du serveur audio :**
- 🔊 **Mixer** plusieurs sources audio (musique + notifications + vidéos)
- 🎧 **Router** le son vers le bon périphérique (haut-parleurs, casque, Bluetooth)
- 🎚️ **Contrôler** le volume de chaque application indépendamment
- 🔄 **Convertir** les formats audio différents
- 🎵 **Gérer** les périphériques d'entrée/sortie (microphone, carte son)

**Analogie simple :**
Le serveur audio est comme un **chef d'orchestre** qui coordonne tous les sons de votre ordinateur pour qu'ils sortent harmonieusement par vos haut-parleurs ou casque.

### L'évolution des serveurs audio sous Linux

#### OSS (Open Sound System) - Les débuts
- **Années 1990-2000**
- Premier système audio Linux
- Limitations : une seule application à la fois
- Abandonné progressivement

#### ALSA (Advanced Linux Sound Architecture) - La base
- **Depuis 2002**
- Intégré au noyau Linux
- Pilotes pour cartes son
- Niveau bas, pas de mixing automatique
- **Toujours utilisé** comme couche de base

#### PulseAudio - La révolution grand public
- **Depuis 2004**
- Mixer audio pour le bureau
- Support réseau
- Volume par application
- Standard pendant 15+ ans
- **Quelques défauts :** latence, bugs occasionnels, complexité

#### JACK - L'audio professionnel
- **Depuis 2002**
- Latence ultra-faible (< 5ms)
- Routage audio complexe
- Production musicale, enregistrement
- **Problème :** complexe, pas pour le grand public

#### PipeWire - L'unification moderne
- **Depuis 2022** (adoption massive)
- **Remplace à la fois** PulseAudio et JACK
- Meilleur de chaque monde
- Simple pour débutants, puissant pour pros
- **L'avenir de l'audio Linux**

---

## Qu'est-ce que PipeWire ?

### Définition

**PipeWire** est un serveur multimédia moderne qui gère :
- 🔊 **Audio** : lecture, enregistrement, routage
- 🎥 **Vidéo** : capture webcam, partage d'écran
- 📱 **Communication** : appels visio, streaming

**Créé par :** Wim Taymans (aussi créateur de GStreamer)  
**Développé par :** Red Hat et la communauté  
**Première version stable :** 2021  
**Adoption :** Ubuntu, Fedora, Arch, Linux Mint (2022+)  

### Les avantages de PipeWire

#### Pour tous les utilisateurs

**1. Compatibilité totale**
- ✅ Compatible avec les applications **PulseAudio** (99% des apps)
- ✅ Compatible avec les applications **JACK** (audio pro)
- ✅ Compatible avec les applications **ALSA** (anciennes apps)
- → Tout fonctionne sans rien changer !

**2. Meilleure stabilité**
- Moins de bugs audio
- Pas de "crépitements" aléatoires
- Reconnexion automatique des périphériques Bluetooth

**3. Performance améliorée**
- Latence réduite (important pour les jeux)
- Moins de consommation CPU
- Meilleure synchronisation audio/vidéo

**4. Gestion simplifiée**
- Configuration automatique
- Détection intelligente des périphériques
- Basculement fluide entre périphériques

#### Pour les utilisateurs avancés

**5. Latence ultra-faible**
- Possible d'atteindre < 5ms (production musicale)
- Remplace JACK pour l'audio professionnel

**6. Routage audio flexible**
- Graphe de routage visuel
- Connexions complexes faciles
- Effets en temps réel

**7. Support Bluetooth amélioré**
- Meilleurs codecs (LDAC, aptX)
- Reconnexion automatique
- Moins de problèmes de synchronisation

**8. Sécurité renforcée**
- Isolation des applications (Flatpak/Snap)
- Permissions granulaires

---

## PipeWire sous Linux Mint

### Vérifier si PipeWire est actif

Linux Mint 21+ utilise PipeWire par défaut, mais vous pouvez vérifier :

**Méthode 1 : Interface graphique**
1. Ouvrez le **Menu**
2. Tapez "Son" ou "Audio"
3. Si vous voyez "PipeWire" dans les informations, c'est actif

**Méthode 2 : Ligne de commande**
```bash
# Vérifier si PipeWire fonctionne
pactl info | grep "Server Name"
```

**Sortie attendue :**
```
Server Name: PulseAudio (on PipeWire 0.3.XX)
```

Cela signifie que PipeWire est actif avec une couche de compatibilité PulseAudio.

**Ou directement :**
```bash
# Vérifier le processus PipeWire
ps aux | grep pipewire
```

Vous devriez voir plusieurs processus :
- `pipewire` : Le serveur principal
- `pipewire-pulse` : Compatibilité PulseAudio
- `wireplumber` : Gestionnaire de session

**Vérifier la version :**
```bash
pipewire --version
```

### Architecture de PipeWire

PipeWire se compose de plusieurs éléments :

#### 1. pipewire
Le **serveur principal** qui gère les flux audio/vidéo.

#### 2. pipewire-pulse
Une **couche de compatibilité PulseAudio**.
- Les applications pensent communiquer avec PulseAudio
- Mais c'est PipeWire qui gère réellement

#### 3. WirePlumber
Le **gestionnaire de session**.
- Détecte les périphériques
- Applique les règles de routage
- Gère la configuration
- Remplace l'ancien pipewire-media-session

#### 4. pipewire-alsa
Permet aux applications ALSA de fonctionner avec PipeWire.

#### 5. pipewire-jack
Permet aux applications JACK (audio pro) de fonctionner.

**Schéma simplifié :**
```
Applications → pipewire-pulse/jack/alsa → PipeWire → ALSA (pilotes) → Carte son
```

---

## Configuration audio de base

### Accéder aux paramètres audio

**Méthode 1 : Via l'icône de volume**
1. Clic droit sur l'**icône de volume** (barre de tâches)
2. Sélectionnez "**Paramètres du son**"

**Méthode 2 : Via le menu système**
1. Menu → Préférences → **Son**

### Interface des paramètres audio

#### Onglet "Sortie" (Output)

**Périphériques de sortie :**
- Liste de tous les périphériques audio disponibles :
  - Haut-parleurs internes
  - Casque (prise jack)
  - Sortie HDMI
  - Casque/Enceinte Bluetooth
  - Carte son USB

**Pour chaque périphérique :**
- **Volume** : Curseur de 0 à 100% (ou plus avec suramplification)
- **Balance** : Gauche/Droite
- **Test** : Bouton pour tester le son

**Sélectionner le périphérique actif :**
- Cliquez sur le périphérique souhaité
- Le son est immédiatement redirigé

#### Onglet "Entrée" (Input)

**Périphériques d'entrée :**
- Microphone interne
- Microphone externe (USB, jack)
- Microphone Bluetooth
- Line-in (entrée ligne)

**Contrôles :**
- **Volume d'entrée** : Sensibilité du microphone
- **Indicateur de niveau** : Barres visuelles montrant le niveau sonore
- **Muet** : Couper le microphone

**Tester le microphone :**
- Parlez normalement
- Les barres de niveau doivent bouger
- Si pas de mouvement : microphone inactif ou volume trop bas

#### Onglet "Applications"

**Volume par application :**
- Liste toutes les applications produisant du son
- **Volume indépendant** pour chaque application
- Possibilité de **muter** une app spécifique

**Exemple d'usage :**
- Musique (Spotify) à 100%
- Notification à 30%
- Jeu à 80%
- Navigateur (YouTube) à 50%

**Changer le périphérique de sortie par application :**
- Vous pouvez envoyer une app vers un périphérique spécifique
- Exemple : musique vers Bluetooth, notifications vers haut-parleurs

#### Onglet "Configuration"

**Profils de périphériques :**
Chaque carte son a plusieurs "profils" selon ses capacités :

**Exemples de profils :**
- **Analogique Stéréo Duplex** : Entrée + sortie simultanées (recommandé)
- **Analogique Stéréo Output** : Sortie uniquement
- **Digital Stereo (HDMI)** : Sortie numérique
- **Off** : Périphérique désactivé

**Sélectionner le bon profil :**
- "Duplex" si vous utilisez micro + haut-parleurs
- "Output" si sortie uniquement

---

## PulseAudio Volume Control (pavucontrol)

### Qu'est-ce que pavucontrol ?

**pavucontrol** est un **mixeur audio avancé** beaucoup plus complet que les paramètres de base.

Malgré son nom (PulseAudio), il fonctionne **parfaitement avec PipeWire** grâce à la couche de compatibilité.

### Installation

```bash
sudo apt install pavucontrol
```

### Accès

**Lancement :**
- Menu → Son et Vidéo → **PulseAudio Volume Control**
- Ou terminal : `pavucontrol`

### Interface de pavucontrol

#### Onglet "Lecture" (Playback)

**Flux audio en cours :**
- Chaque application qui joue du son apparaît ici
- **Volume individuel** par app (0-150%, suramplification possible)
- **Mute** par app
- **Sélection du périphérique** de sortie par app

**Colonnes :**
- Nom de l'application
- Curseur de volume avec pourcentage
- Menu déroulant pour choisir le périphérique

#### Onglet "Enregistrement" (Recording)

**Applications qui enregistrent :**
- Affiche les apps utilisant le microphone
- Contrôle du volume d'entrée
- Choix du microphone source

**Utile pour :**
- Vérifier qu'une app accède bien au micro
- Diagnostiquer pourquoi le micro ne fonctionne pas en visio

#### Onglet "Périphériques de sortie" (Output Devices)

**Tous les périphériques audio disponibles :**
- Haut-parleurs
- Casques
- HDMI
- Bluetooth
- USB

**Contrôles détaillés :**
- **Volume principal** du périphérique
- **Canaux séparés** (gauche/droite, avant/arrière pour surround)
- **Balance** et **Fade** (avant/arrière)
- **Port** : Sélectionner la prise physique (jack casque vs haut-parleurs)
- **Latence** : Affichage du délai

**Avancé :**
- Bouton "**Définir comme périphérique par défaut**"
- Icône de cadenas pour "verrouiller les canaux ensemble"

#### Onglet "Périphériques d'entrée" (Input Devices)

**Tous les microphones disponibles :**
- Contrôles similaires aux périphériques de sortie
- Indicateur de niveau en temps réel
- Boost du microphone si disponible

#### Onglet "Configuration"

**Profils de carte son :**
- Identique aux paramètres système
- Plus de détails sur chaque profil
- Possibilité de désactiver complètement une carte

---

## Helvum et qpwgraph : Routage audio visuel

### Helvum - L'interface simple

**Helvum** est un outil de routage audio **graphique** pour PipeWire.

#### Installation

```bash
sudo apt install helvum
```

#### Utilisation

**Lancement :**
- Menu → Son et Vidéo → **Helvum**
- Ou terminal : `helvum`

**Interface :**
- **Graphe de nœuds** : Chaque app/périphérique est un "nœud"
- **Connexions** : Lignes entre les nœuds
- **Glisser-déposer** : Créer/supprimer des connexions

**Exemple de nœuds :**
- Firefox (sortie audio)
- Haut-parleurs (entrée audio)
- Microphone (sortie audio)
- Discord (entrée audio pour enregistrement)

**Cas d'usage :**
- **Routage simple** : Envoyer Firefox vers Bluetooth
- **Routage multiple** : Une source vers plusieurs destinations
- **Enregistrement** : Capturer la sortie d'une app

**Avantages :**
- Visuel et intuitif
- Temps réel
- Idéal pour débutants

### qpwgraph - L'interface pro

**qpwgraph** est une alternative plus complète, inspirée de QjackCtl (JACK).

#### Installation

```bash
sudo apt install qpwgraph
```

#### Utilisation

**Lancement :**
```bash
qpwgraph
```

**Interface :**
- **Graphe de patch** : Similaire à Helvum mais plus détaillé
- **Catégories** : Audio, MIDI, Vidéo séparées
- **Connexions précises** : Canal par canal

**Fonctionnalités avancées :**
- Sauvegarde de "patchbays" (configurations de routage)
- Gestion MIDI (pour instruments virtuels)
- Graphe de vidéo (caméras, partage d'écran)

**Pour qui :**
- Producteurs de musique
- Streamers
- Utilisateurs avancés nécessitant du routage complexe

---

## Gestion des périphériques audio

### Ajouter/Retirer des périphériques

**Détection automatique :**
- Branchez un casque USB → Détection instantanée
- Connectez un casque Bluetooth → Apparaît automatiquement
- Branchez un câble HDMI → Sortie audio HDMI disponible

**Basculer rapidement :**
1. Clic sur l'**icône de volume**
2. Dans le menu, sélectionnez le périphérique souhaité
3. Ou utilisez **pavucontrol** pour plus de contrôle

### Périphérique par défaut

**Définir le périphérique par défaut :**

**Méthode 1 : pavucontrol**
1. Ouvrez pavucontrol
2. Onglet "**Périphériques de sortie**"
3. Bouton "**Définir par défaut**" (icône de coche verte)

**Méthode 2 : Ligne de commande**
```bash
# Lister les périphériques (sinks)
pactl list short sinks

# Définir par défaut (remplacez par le nom de votre périphérique)
pactl set-default-sink alsa_output.pci-0000_00_1f.3.analog-stereo
```

**Méthode 3 : WirePlumber (permanent)**
Créez un fichier de configuration :
```bash
mkdir -p ~/.config/wireplumber/main.lua.d/  
nano ~/.config/wireplumber/main.lua.d/51-default-sink.lua  
```

Contenu :
```lua
rule = {
  matches = {
    {
      { "node.name", "equals", "alsa_output.pci-0000_00_1f.3.analog-stereo" },
    },
  },
  apply_properties = {
    ["node.name"] = "Mes-Haut-parleurs",
    ["priority.session"] = 1000,
  },
}

table.insert(alsa_monitor.rules, rule)
```

Redémarrez PipeWire :
```bash
systemctl --user restart pipewire
```

### Casque Bluetooth

**Connexion :**
1. Appairez le casque Bluetooth (voir chapitre 12.4)
2. Le casque apparaît automatiquement dans pavucontrol
3. Sélectionnez-le comme périphérique de sortie

**Choisir le profil :**
Dans pavucontrol, onglet "Configuration" :
- **A2DP Sink** : Haute qualité audio (musique) - Pas de micro
- **HSP/HFP** : Qualité réduite mais avec microphone (appels)

**Problèmes courants :**
- Pas de son : Vérifiez le profil (A2DP)
- Mauvaise qualité : Passez de HSP à A2DP
- Micro ne fonctionne pas : Utilisez le profil HSP/HFP

**Codecs Bluetooth :**
PipeWire supporte :
- **SBC** : Standard (qualité moyenne)
- **AAC** : Bonne qualité
- **aptX** : Haute qualité (si casque compatible)
- **LDAC** : Très haute qualité (Sony)

```bash
# Vérifier les codecs disponibles
pactl list | grep -i codec
```

---

## Audio professionnel et latence faible

### Mode JACK avec PipeWire

PipeWire peut **remplacer JACK** pour la production audio.

**Avantages :**
- Pas besoin d'installer JACK séparément
- Latence aussi faible que JACK
- Applications système continuent de fonctionner
- Plus simple à configurer

#### Activer le mode faible latence

**1. Modifier la configuration PipeWire :**

```bash
# Copier la config par défaut
mkdir -p ~/.config/pipewire/  
cp /usr/share/pipewire/pipewire.conf ~/.config/pipewire/  

# Éditer
nano ~/.config/pipewire/pipewire.conf
```

**2. Ajuster les paramètres :**

Cherchez la section `default.clock` et modifiez :
```
default.clock.rate = 48000          # Fréquence d'échantillonnage  
default.clock.quantum = 64          # Taille du buffer (latence)  
default.clock.min-quantum = 64  
default.clock.max-quantum = 1024  
```

**Latence selon quantum :**
- **256** : ~5ms (usage normal, recommandé)
- **128** : ~2.7ms (musique avec monitoring)
- **64** : ~1.3ms (enregistrement critique)
- **32** : ~0.7ms (ultra-faible, nécessite matériel performant)

**3. Redémarrer PipeWire :**
```bash
systemctl --user restart pipewire
```

#### Vérifier la latence actuelle

```bash
pw-top
```

**Sortie :**
```
DRIVER   QUANT  RATE  
pipewire    64 48000   # Quantum = 64, 48kHz  
```

Latence = (64 / 48000) × 1000 = 1.33ms

### Applications audio professionnelles

**DAWs compatibles avec PipeWire :**
- **Ardour** : DAW complète
- **Reaper** : DAW professionnelle
- **Bitwig Studio** : Production moderne
- **LMMS** : Production beats et électro
- **Audacity** : Édition audio simple

**Installation exemple (Ardour) :**
```bash
sudo apt install ardour
```

**Configuration dans l'application :**
1. Ouvrez les préférences audio
2. Backend : **JACK** (PipeWire émule JACK)
3. Latence : selon vos besoins
4. Fréquence : 48000 Hz (standard)

### Plugins et effets temps réel

**Formats supportés :**
- **LADSPA** : Ancien format Linux
- **LV2** : Format moderne recommandé
- **VST/VST3** : Avec Wine ou plugins natifs

**Installation de plugins :**
```bash
# Suite de plugins de base
sudo apt install ladspa-sdk lv2-dev

# Plugins Calf (excellents)
sudo apt install calf-plugins

# Plugins EQ et dynamiques
sudo apt install tap-plugins swh-plugins
```

**Application des effets :**
Utilisez **EasyEffects** (anciennement PulseEffects) :

```bash
sudo apt install easyeffects
```

**Fonctionnalités :**
- Égaliseur graphique
- Compresseur
- Limiteur
- Réverbération
- Effets divers
- Presets par application

---

## Configuration avancée

### Fichiers de configuration PipeWire

**Emplacements importants :**
```
/usr/share/pipewire/          # Configuration par défaut (ne pas modifier)
~/.config/pipewire/           # Configuration utilisateur (prioritaire)
~/.config/wireplumber/        # Configuration WirePlumber
```

**Principaux fichiers :**
- `pipewire.conf` : Configuration serveur
- `pipewire-pulse.conf` : Compatibilité PulseAudio
- `client.conf` : Configuration clients

### Règles WirePlumber personnalisées

WirePlumber utilise des règles en **Lua** pour gérer les périphériques.

**Exemple : Auto-basculer vers casque Bluetooth :**

```bash
mkdir -p ~/.config/wireplumber/main.lua.d/  
nano ~/.config/wireplumber/main.lua.d/50-auto-switch-bluetooth.lua  
```

Contenu :
```lua
rule = {
  matches = {
    {
      { "device.name", "matches", "*bluez*" },
    },
  },
  apply_properties = {
    ["device.disabled"] = false,
    ["priority.session"] = 2000,  # Priorité élevée
  },
}

table.insert(bluez_monitor.rules, rule)
```

**Redémarrer :**
```bash
systemctl --user restart wireplumber
```

### Variables d'environnement

**Ajuster la latence globalement :**
```bash
# Dans ~/.bashrc ou ~/.profile
export PIPEWIRE_LATENCY=64/48000
```

**Désactiver la suspension automatique (évite coupures) :**
```bash
export PIPEWIRE_SUSPEND=false
```

---

## Problèmes courants et solutions

### Pas de son du tout

**Diagnostic :**

1. **Vérifier que PipeWire fonctionne :**
```bash
systemctl --user status pipewire pipewire-pulse
```

Si "inactive" ou "failed" :
```bash
systemctl --user restart pipewire pipewire-pulse wireplumber
```

2. **Vérifier le volume :**
- Ouvrez pavucontrol
- Vérifiez que rien n'est en mute
- Volume > 0%

3. **Vérifier le périphérique :**
- Bon périphérique sélectionné ?
- Câbles bien branchés ?
- Casque/haut-parleurs allumés ?

4. **Tester avec un son simple :**
```bash
speaker-test -t wav -c 2
```

### Crépitements ou coupures audio

**Causes possibles :**
- Buffer trop petit
- CPU surchargé
- Pilote audio problématique

**Solutions :**

1. **Augmenter le quantum (buffer) :**
Éditez `~/.config/pipewire/pipewire.conf` :
```
default.clock.quantum = 256  # Au lieu de 64
```

2. **Désactiver l'économie d'énergie audio :**
```bash
echo 0 | sudo tee /sys/module/snd_hda_intel/parameters/power_save
```

3. **Améliorer les priorités temps réel :**
```bash
sudo nano /etc/security/limits.d/audio.conf
```

Ajoutez :
```
@audio   -  rtprio     95
@audio   -  memlock    unlimited
```

Ajoutez votre utilisateur au groupe audio :
```bash
sudo usermod -a -G audio $USER
```

Déconnectez-vous et reconnectez-vous.

### Son de mauvaise qualité

**Solutions :**

1. **Vérifier la fréquence d'échantillonnage :**
```bash
# Voir la config actuelle
pw-metadata -n settings

# Forcer 48kHz
pw-metadata -n settings 0 clock.force-rate 48000
```

2. **Désactiver le rééchantillonnage de mauvaise qualité :**
Éditez `~/.config/pipewire/pipewire.conf` :
```
resample.quality = 4  # 0=worst, 4=best
```

### Microphone ne fonctionne pas

**Diagnostic :**

1. **Vérifier dans pavucontrol :**
- Onglet "Périphériques d'entrée"
- Parlez : les barres de niveau bougent ?
- Volume suffisant ?
- Pas en mute ?

2. **Tester l'enregistrement :**
```bash
# Enregistrer 5 secondes
arecord -d 5 test.wav

# Lire
aplay test.wav
```

3. **Vérifier les permissions :**
Applications Flatpak peuvent avoir besoin de permissions :
```bash
flatpak permission-set microphone APPID yes
```

### Bluetooth : qualité audio médiocre

**Cause :** Profil HSP/HFP actif au lieu de A2DP

**Solution :**
1. Ouvrez pavucontrol
2. Onglet "Configuration"
3. Pour le casque Bluetooth, sélectionnez "**High Fidelity Playback (A2DP Sink)**"

**Si A2DP ne fonctionne pas :**
```bash
# Installer les codecs supplémentaires
sudo apt install libspa-0.2-bluetooth

# Redémarrer Bluetooth et PipeWire
sudo systemctl restart bluetooth  
systemctl --user restart pipewire  
```

### Applications ne produisent pas de son

**Certaines apps anciennes ou Flatpak :**

1. **Vérifier dans pavucontrol → Lecture :**
L'app apparaît-elle ?

2. **Forcer l'utilisation de PipeWire :**
```bash
# Pour les apps PulseAudio
PULSE_SERVER=unix:/run/user/$(id -u)/pulse/native application

# Pour les apps ALSA
ALSA_PLUGIN_DIR=/usr/lib/x86_64-linux-gnu/alsa-lib application
```

### Latence trop élevée (jeux, vidéos)

**Réduire la latence :**

Éditez `~/.config/pipewire/pipewire.conf` :
```
default.clock.quantum = 128  # Au lieu de 256 ou plus
```

**Pour les jeux spécifiquement :**
```bash
# Lancer avec latence faible
PIPEWIRE_LATENCY=64/48000 ./mon_jeu
```

---

## Outils en ligne de commande

### pw-cli - Interface interactive

**Lancement :**
```bash
pw-cli
```

**Commandes utiles :**
```
help                  # Aide  
list-objects          # Lister tous les objets  
dump                  # Dump complet de l'état  
quit                  # Quitter  
```

### pw-top - Moniteur temps réel

**Affiche :**
- Latence actuelle
- Taux d'échantillonnage
- Quantum
- Clients actifs
- Utilisation CPU

```bash
pw-top
```

**Navigation :**
- **P** : Pause
- **Q** : Quitter
- **R** : Rafraîchir

### pw-dump - État complet du système

```bash
# Dump JSON de tout le graphe audio
pw-dump

# Filtrer les périphériques de sortie
pw-dump | grep -A 20 "Audio/Sink"
```

### pactl - Contrôle PulseAudio (compatible PipeWire)

```bash
# Lister les périphériques de sortie
pactl list short sinks

# Lister les périphériques d'entrée
pactl list short sources

# Changer le volume (0-65536, 65536=100%)
pactl set-sink-volume 0 50%

# Mute/Unmute
pactl set-sink-mute 0 toggle

# Informations complètes
pactl info

# Statistiques
pactl stat
```

### wpctl - Contrôle WirePlumber

**Commandes utiles :**
```bash
# Lister tous les périphériques
wpctl status

# Définir le volume (0.0 à 1.5, >1.0 = suramplification)
wpctl set-volume @DEFAULT_AUDIO_SINK@ 0.5

# Mute
wpctl set-mute @DEFAULT_AUDIO_SINK@ toggle

# Définir périphérique par défaut
wpctl set-default 47  # Remplacez 47 par l'ID du périphérique
```

---

## Comparaison PulseAudio vs PipeWire

| Fonctionnalité | PulseAudio | PipeWire |
|----------------|------------|----------|
| **Latence minimale** | ~20-30ms | ~1-5ms |
| **Compatibilité PulseAudio** | Native | 100% via émulation |
| **Compatibilité JACK** | Non | Oui |
| **Audio professionnel** | Limité | Excellent |
| **Stabilité Bluetooth** | Moyenne | Excellente |
| **Codecs Bluetooth** | SBC, AAC | SBC, AAC, aptX, LDAC |
| **Routage graphique** | Non natif | Oui (Helvum) |
| **Consommation CPU** | Normale | Réduite |
| **Gestion vidéo** | Non | Oui |
| **Support Flatpak** | Bon | Excellent |
| **Configuration** | Complexe | Moderne |
| **État actuel** | Maintenance | Développement actif |

**Verdict :** PipeWire est **supérieur** dans tous les domaines.

---

## Migration de PulseAudio vers PipeWire

### Si vous êtes encore sur PulseAudio

Linux Mint 21+ utilise PipeWire par défaut. Si vous êtes sur une version plus ancienne :

**Installation :**
```bash
# Installer PipeWire et ses composants
sudo apt install pipewire pipewire-audio-client-libraries  
sudo apt install wireplumber pipewire-pulse  

# Supprimer PulseAudio (optionnel, PipeWire peut coexister)
sudo apt remove pulseaudio

# Redémarrer
sudo reboot
```

**Vérification post-installation :**
```bash
pactl info | grep "Server Name"
# Devrait afficher "PipeWire"
```

### Transférer la configuration PulseAudio

La plupart des réglages PulseAudio sont **automatiquement respectés** par PipeWire.

**Volumes sauvegardés :** Préservés  
**Périphérique par défaut :** Conservé  
**Applications :** Fonctionnent sans changement  

---

## Optimisations et astuces

### Désactiver la suspension automatique

Par défaut, PipeWire peut suspendre les périphériques inactifs (économie d'énergie).

**Désactiver globalement :**
```bash
mkdir -p ~/.config/pipewire/pipewire.conf.d/  
nano ~/.config/pipewire/pipewire.conf.d/no-suspend.conf  
```

Contenu :
```
context.properties = {
    default.clock.allowed-rates = [ 48000 96000 ]
}

context.modules = [
    {   name = libpipewire-module-suspend-node
        args = { }
        flags = [ ifexists nofail ]
    }
]
```

Ou éditez `~/.config/pipewire/pipewire.conf` et commentez :
```
#    { name = libpipewire-module-suspend-node }
```

### Égaliseur système avec EasyEffects

**Installation :**
```bash
sudo apt install easyeffects
```

**Usage :**
1. Lancez EasyEffects
2. Ajoutez un "Equalizer" dans la chaîne
3. Ajustez les fréquences selon vos goûts
4. Sauvegardez le preset
5. Activez "Autostart" pour lancer au démarrage

**Presets disponibles :**
- Bass Boost
- Vocal Clarity
- Laptop Speakers Correction
- Headphone Enhancement

### Enregistrement de ce qui est joué (loopback)

**Capturer l'audio système :**

1. **Méthode graphique (Helvum) :**
   - Connectez la sortie système vers l'entrée d'enregistrement

2. **Méthode ligne de commande :**
```bash
# Créer un module loopback
pactl load-module module-loopback latency_msec=1
```

**Enregistrer avec OBS, Audacity, etc. en sélectionnant le "Monitor"**

### Mode nuit / Réduction du bruit

**EasyEffects permet d'ajouter :**
- **Noise Reduction** : Suppression bruit de fond (micro)
- **Compressor** : Égalisation dynamique (évite sons trop forts)
- **Limiter** : Protection auditive (évite distorsion)

---

## Ressources et documentation

### Documentation officielle

**Sites web :**
- PipeWire : https://pipewire.org/
- GitLab PipeWire : https://gitlab.freedesktop.org/pipewire/pipewire
- Wiki ArchLinux (excellent) : https://wiki.archlinux.org/title/PipeWire
- WirePlumber : https://pipewire.pages.freedesktop.org/wireplumber/

### Communauté

**Forums :**
- Forums Linux Mint
- Reddit : r/linux, r/linuxaudio
- Discord PipeWire

### Aide en ligne de commande

```bash
man pipewire  
man pipewire.conf  
man wireplumber  
man pw-cli  
```

### Logs et diagnostic

```bash
# Logs PipeWire
journalctl --user -u pipewire

# Logs WirePlumber
journalctl --user -u wireplumber

# Mode debug (verbeux)
PIPEWIRE_DEBUG=3 pipewire
```

---

## Conclusion

**PipeWire** représente l'avenir de l'audio sous Linux. C'est une **amélioration majeure** qui unifie et simplifie l'écosystème audio Linux.

**Points clés à retenir :**

- ✅ **Compatibilité totale** : Toutes vos applications fonctionnent sans changement
- ✅ **Meilleure stabilité** : Moins de bugs, meilleure gestion Bluetooth
- ✅ **Latence réduite** : Excellent pour le gaming et l'audio professionnel
- ✅ **Configuration simple** : Fonctionne "out of the box"
- ✅ **Outils graphiques** : pavucontrol, Helvum pour faciliter la gestion
- ✅ **Puissance professionnelle** : Remplace JACK pour la production audio

**Pour la plupart des utilisateurs :**
- PipeWire fonctionne **automatiquement** sans configuration
- Utilisez **pavucontrol** pour les réglages de base
- C'est tout !

**Pour les utilisateurs avancés :**
- Latence ultra-faible possible
- Routage audio complexe avec Helvum/qpwgraph
- Production musicale sans JACK séparé
- Contrôle total via configuration

PipeWire a transformé l'audio Linux d'un point faible en un **point fort** du système. Profitez-en !

Dans le prochain chapitre, nous aborderons la **mise à jour du firmware** (BIOS/UEFI et composants matériels).

⏭️ [Mise à jour du firmware (fwupd, UEFI/BIOS)](/12-materiel-et-pilotes/07-mise-a-jour-du-firmware.md)
