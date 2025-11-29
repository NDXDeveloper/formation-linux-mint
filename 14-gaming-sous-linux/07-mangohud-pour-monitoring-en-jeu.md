🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 14.7 MangoHud pour monitoring en jeu

## Introduction

MangoHud est un overlay de monitoring des performances pour Linux qui affiche des informations en temps réel pendant que vous jouez. C'est l'équivalent de MSI Afterburner ou RivaTuner sous Windows, mais conçu spécifiquement pour Linux.

**MangoHud affiche :**
- 🎯 FPS (images par seconde)
- 🖥️ Utilisation CPU et GPU
- 🌡️ Températures CPU et GPU
- 💾 Utilisation RAM et VRAM
- ⏱️ Frame time (temps de rendu par image)
- 📊 Graphiques de performances
- 🎮 Informations du jeu (nom, résolution)

**Pourquoi utiliser MangoHud ?**
- Surveiller les performances en temps réel
- Diagnostiquer les problèmes (bottleneck CPU/GPU)
- Vérifier les températures
- Optimiser les paramètres graphiques
- Enregistrer les performances pour analyse
- Comparer avant/après optimisation

## Installation de MangoHud

### Méthode 1 : Via APT (recommandée pour débutants)

```bash
# Installer MangoHud
sudo apt update
sudo apt install mangohud

# Vérifier l'installation
mangohud --version
```

### Méthode 2 : Via le PPA (version plus récente)

```bash
# Ajouter le PPA
sudo add-apt-repository ppa:flexiondotorg/mangohud
sudo apt update

# Installer
sudo apt install mangohud

# Installer aussi goverlay (interface graphique de configuration)
sudo apt install goverlay
```

### Méthode 3 : Via Flatpak (si Steam est en Flatpak)

```bash
# Installer MangoHud pour Flatpak
flatpak install flathub org.freedesktop.Platform.VulkanLayer.MangoHud
```

### Vérifier l'installation

```bash
# Tester MangoHud
mangohud glxgears

# Une fenêtre avec des engrenages s'ouvre avec l'overlay MangoHud visible
```

Appuyez sur **Shift+F12** pour afficher/masquer l'overlay.

## Utilisation de base

### Avec Steam

**Pour tous les jeux** :

1. Ouvrez **Steam**
2. **Steam** (menu) → **Paramètres**
3. **Compatibilité**
4. Cochez **Activer Steam Play pour tous les titres**
5. Dans **Exécuter les autres titres avec**, sélectionnez votre version de Proton
6. Fermez les paramètres

**Ajoutez à toutes les options de lancement** :
```bash
mangohud %command%
```

**Pour un jeu spécifique** :

1. Bibliothèque → Clic droit sur le jeu → **Propriétés**
2. **Options de lancement**
3. Ajoutez : `mangohud %command%`

**Exemple complet avec GameMode** :
```bash
gamemoderun mangohud %command%
```

### Avec Lutris

**Activation globale** :

1. Ouvrez **Lutris**
2. ☰ (menu hamburger) → **Préférences**
3. Onglet **Global options**
4. Section **System options**
5. Cochez **Enable MangoHud**

**Pour un jeu spécifique** :

1. Clic droit sur le jeu → **Configure**
2. Onglet **System options**
3. Cochez **Enable MangoHud**

### Avec Heroic Games Launcher

**Pour un jeu** :

1. Page du jeu → ⚙️ **Settings**
2. Onglet **Advanced** ou **Other**
3. **Enable MangoHud** : ON

**Configuration globale** :

1. **Settings** (général) → **Advanced**
2. **Enable MangoHud** : ON
3. S'applique à tous les nouveaux jeux

### En ligne de commande (n'importe quel jeu)

```bash
# Syntaxe de base
mangohud /chemin/vers/le/jeu

# Exemple avec un jeu Steam
mangohud ~/.steam/steam/steamapps/common/MonJeu/jeu.exe

# Avec un émulateur
mangohud retroarch

# Avec un jeu Wine
mangohud wine MonJeu.exe
```

### Avec des jeux natifs (non-Steam)

```bash
# Lancer avec MangoHud
mangohud ./jeu

# Exemple concret
cd ~/Games/SuperTuxKart/
mangohud ./supertuxkart
```

## Raccourcis clavier

Une fois dans le jeu avec MangoHud actif :

| Raccourci | Action |
|-----------|--------|
| **Shift+F12** | Afficher/Masquer l'overlay |
| **Shift+F2** | Changer de position (9 positions) |
| **Shift+F4** | Recharger la configuration |
| **F12** | Capturer les logs (si activé) |

> **Note** : Certains jeux utilisent déjà F12. Vous pouvez personnaliser les raccourcis (voir section Configuration).

## Configuration de MangoHud

MangoHud se configure via un fichier texte simple.

### Créer le fichier de configuration

```bash
# Créer le dossier de configuration
mkdir -p ~/.config/MangoHud

# Créer le fichier de configuration
nano ~/.config/MangoHud/MangoHud.conf
```

### Configuration de base (recommandée pour débutants)

Copiez-collez cette configuration simple :

```ini
### Configuration MangoHud simple ###

# Position de l'overlay
position=top-left

# Informations affichées
fps
gpu_stats
cpu_stats
ram
vram

# Apparence
font_size=24
background_alpha=0.5
```

**Enregistrez** : `Ctrl+O`, `Entrée`, `Ctrl+X`

### Comprendre les options

#### Position de l'overlay

```ini
# Positions disponibles :
position=top-left        # Haut gauche (défaut)
position=top-right       # Haut droite
position=bottom-left     # Bas gauche
position=bottom-right    # Bas droite
position=top-center      # Haut centre
position=bottom-center   # Bas centre
```

#### Informations à afficher

```ini
# FPS
fps                      # Affiche les FPS
fps_limit=144           # Limite les FPS (optionnel)

# GPU
gpu_stats               # Utilisation et fréquence GPU
gpu_temp                # Température GPU
gpu_power               # Consommation GPU (si supporté)
gpu_mem_clock           # Fréquence mémoire GPU
gpu_core_clock          # Fréquence core GPU

# CPU
cpu_stats               # Utilisation CPU (tous les cœurs)
cpu_temp                # Température CPU
cpu_power               # Consommation CPU (si supporté)
core_load               # Charge par cœur (détaillé)

# Mémoire
ram                     # RAM utilisée
vram                    # VRAM utilisée

# Timing
frame_timing=1          # Graphique de frame time
frametime=1             # Affiche le frame time en ms

# Informations système
engine_version          # Moteur du jeu (Unity, Unreal, etc.)
vulkan_driver           # Version du driver Vulkan
wine                    # Version de Wine/Proton (si applicable)
gamemode                # Indique si GameMode est actif

# Informations de jeu
resolution              # Résolution du jeu
```

### Configurations prêtes à l'emploi

#### Configuration minimale (performances maximales)

```ini
# Minimal - Impact minimal sur performances
position=top-right
fps
gpu_temp
cpu_temp
font_size=20
background_alpha=0.3
```

#### Configuration standard (recommandée)

```ini
# Standard - Bon équilibre
position=top-left

# Stats principales
fps
gpu_stats
gpu_temp
cpu_stats
cpu_temp
ram
vram

# Apparence
font_size=24
background_alpha=0.5
text_color=FFFFFF
```

#### Configuration complète (monitoring avancé)

```ini
# Complète - Toutes les informations
position=top-left

# FPS et timing
fps
frametime=1
frame_timing=1

# GPU détaillé
gpu_stats
gpu_temp
gpu_core_clock
gpu_mem_clock
gpu_power

# CPU détaillé
cpu_stats
cpu_temp
core_load

# Mémoire
ram
vram

# Système
engine_version
vulkan_driver
wine
gamemode

# Graphiques
frame_timing=1
histogram

# Apparence
font_size=22
background_alpha=0.4
```

#### Configuration pour benchmarking

```ini
# Benchmarking - Avec logging
position=top-right

fps
frametime=1
gpu_temp
cpu_temp

# Logging
output_folder=/home/VOTRE_NOM/mangohud-logs
log_duration=60
autostart_log=1

# Apparence minimaliste
font_size=20
background_alpha=0.3
```

> **Remplacez** `VOTRE_NOM` par votre nom d'utilisateur Linux.

### Personnalisation de l'apparence

#### Couleurs

```ini
# Couleurs (format RGB hexadécimal)
text_color=FFFFFF        # Blanc
gpu_color=2E97CB        # Bleu
cpu_color=2E9762        # Vert
vram_color=AD64C1       # Violet
ram_color=C26693        # Rose
engine_color=EB5B5B     # Rouge
background_color=020202 # Noir
```

#### Taille et transparence

```ini
# Taille de la police
font_size=24            # Défaut : 24
font_size=18            # Petit
font_size=32            # Grand

# Transparence
background_alpha=0.5    # 50% transparent (défaut)
background_alpha=0.0    # Complètement transparent
background_alpha=1.0    # Opaque

# Arrondi des bords
round_corners=5         # Bords arrondis (en pixels)
```

#### Espacement

```ini
# Espacement
table_columns=3         # Nombre de colonnes
cellpadding_y=-0.085   # Espacement vertical
```

### Graphiques de performances

#### Frame timing graph

```ini
# Graphique de frame time
frame_timing=1          # Active le graphique
histogram              # Histogramme au lieu de ligne
```

Ce graphique montre la régularité des frames. Une ligne plate = bon. Des pics = stutters.

#### Customisation du graphique

```ini
# Couleur du graphique
frametime_color=00FF41  # Vert néon

# Taille du graphique
frame_timing=1
width=280               # Largeur de l'overlay
height=140              # Hauteur
```

## Logging des performances

MangoHud peut enregistrer les performances dans un fichier pour analyse ultérieure.

### Activer le logging

**Dans la configuration** :

```ini
# Dossier de sortie des logs
output_folder=/home/VOTRE_NOM/mangohud-logs

# Durée d'enregistrement (en secondes)
log_duration=60

# Démarrage automatique
autostart_log=1         # Démarre le log automatiquement
```

**OU manuellement avec la touche** :

```ini
# Raccourci pour démarrer/arrêter le log
toggle_logging=F12
```

### Analyser les logs

Les logs sont sauvegardés en format CSV.

**Exemple de fichier** : `MonJeu_2024-01-15_14-30-00.csv`

**Contenu** :
```
fps,frametime,cpu_load,gpu_load,cpu_temp,gpu_temp
60,16.67,45.2,78.3,62,71
59,16.94,46.1,79.1,63,72
...
```

**Ouvrir avec LibreOffice Calc** :
1. Ouvrez le fichier CSV
2. Créez des graphiques
3. Analysez les tendances

**Analyser en ligne de commande** :

```bash
# FPS moyen
awk -F',' 'NR>1 {sum+=$1; count++} END {print "FPS moyen:", sum/count}' fichier.csv

# FPS minimum
awk -F',' 'NR>1 {if(min==""){min=$1}; if($1<min){min=$1}} END {print "FPS min:", min}' fichier.csv
```

## GOverlay : Interface graphique

GOverlay est une interface graphique pour configurer MangoHud facilement.

### Installation

```bash
sudo apt install goverlay
```

### Utilisation

```bash
# Lancer GOverlay
goverlay
```

**Interface GOverlay** :

1. **Onglet MangoHud** :
   - Cochez les informations à afficher
   - Ajustez la position
   - Personnalisez les couleurs
   - Prévisualisez en temps réel

2. **Onglet vkBasalt** :
   - Effets post-processing (shaders)

3. **Onglet ReplaySorcery** :
   - Enregistrement instantané

**Avantages de GOverlay** :
- ✅ Interface visuelle (pas de fichier texte)
- ✅ Prévisualisation en direct
- ✅ Configurations prédéfinies
- ✅ Export/Import de configs

**Inconvénient** :
- ❌ Moins flexible que l'édition manuelle

## Configurations par type de jeu

### FPS compétitifs (CS:GO, Valorant, etc.)

```ini
# Minimal pour FPS max
position=top-right
fps
font_size=18
background_alpha=0.2
no_display              # Masqué par défaut
toggle_hud=Shift+F12    # Afficher sur demande
```

### RPG / Solo (Witcher, Skyrim, etc.)

```ini
# Complet pour surveiller tout
position=top-left
fps
frametime=1
gpu_stats
gpu_temp
cpu_stats
cpu_temp
ram
vram
engine_version
font_size=24
background_alpha=0.5
```

### Jeux rétro / émulation

```ini
# Simple et discret
position=bottom-right
fps
cpu_temp
font_size=20
background_alpha=0.3
```

### Benchmarking / Tests

```ini
# Avec logging automatique
position=top-right
fps
frametime=1
frame_timing=1
gpu_temp
cpu_temp

output_folder=~/benchmark-logs
log_duration=120
autostart_log=1

font_size=22
background_alpha=0.4
```

## Configurations par jeu spécifique

Vous pouvez créer des configurations différentes par jeu.

### Créer une config spécifique

```bash
# Configuration pour un jeu spécifique
nano ~/.config/MangoHud/MonJeu.conf
```

**Activez-la avec** :

```bash
# Steam - Options de lancement
MANGOHUD_CONFIG=MonJeu mangohud %command%
```

**Ou créez un fichier par nom de jeu** :

```bash
# MangoHud cherche automatiquement un fichier nommé comme l'exécutable
~/.config/MangoHud/csgo.conf        # Pour CS:GO
~/.config/MangoHud/witcher3.conf    # Pour The Witcher 3
```

## Résolution de problèmes

### MangoHud ne s'affiche pas

**Vérifications** :

1. **MangoHud est installé ?**
   ```bash
   mangohud --version
   ```

2. **Le jeu utilise Vulkan ou OpenGL ?**
   - MangoHud fonctionne avec Vulkan et OpenGL
   - Certains jeux DirectX nécessitent DXVK/VKD3D

3. **Testé avec un jeu simple ?**
   ```bash
   mangohud glxgears
   ```

4. **Fichier de configuration corrompu ?**
   ```bash
   # Renommer temporairement
   mv ~/.config/MangoHud/MangoHud.conf ~/.config/MangoHud/MangoHud.conf.bak
   ```

### L'overlay cause du lag

**Solutions** :

1. **Réduisez les informations affichées**
   ```ini
   # Configuration ultra-light
   fps
   font_size=18
   ```

2. **Désactivez les graphiques**
   ```ini
   # Pas de frame_timing
   # frame_timing=0
   ```

3. **Augmentez l'intervalle de rafraîchissement**
   ```ini
   fps_sampling_period=500  # Rafraîchit toutes les 500ms
   ```

### Certaines infos ne s'affichent pas

**GPU temperature ne fonctionne pas** :

```bash
# Vérifier les permissions sensors
sudo sensors-detect

# Ajouter votre utilisateur au groupe
sudo usermod -a -G video $USER

# Redémarrer
sudo reboot
```

**CPU/GPU power ne s'affiche pas** :

Certains matériels ne supportent pas ces mesures. C'est normal.

### Conflit avec overlay Steam

```bash
# Désactiver l'overlay Steam
# Steam → Paramètres → En jeu → Décochez "Activer l'overlay Steam"
```

### MangoHud avec Flatpak

**Si Steam est en Flatpak** :

```bash
# Installer la couche Vulkan MangoHud pour Flatpak
flatpak install flathub org.freedesktop.Platform.VulkanLayer.MangoHud

# Activer globalement
flatpak override --user --env=MANGOHUD=1 com.valvesoftware.Steam
```

## Variables d'environnement

Vous pouvez contrôler MangoHud via variables d'environnement.

### Variables utiles

```bash
# Activer/Désactiver
MANGOHUD=1              # Active MangoHud
MANGOHUD=0              # Désactive MangoHud

# Configuration spécifique
MANGOHUD_CONFIG=fichier # Utilise ~/fichier.conf
MANGOHUD_CONFIGFILE=/chemin/complet/config.conf

# Options en ligne
MANGOHUD_CONFIG=fps,gpu_temp,cpu_temp

# Exemple d'utilisation
MANGOHUD=1 MANGOHUD_CONFIG=fps,gpu_temp ./jeu
```

### Steam avec variables

**Options de lancement** :
```bash
MANGOHUD=1 MANGOHUD_CONFIG=fps,gpu_temp,cpu_temp mangohud %command%
```

## Comparer les performances

### Avant/Après optimisation

1. **Jouez 5 minutes avec logging**
   ```ini
   log_duration=300
   autostart_log=1
   ```

2. **Notez** :
   - FPS moyen
   - FPS minimum
   - Températures

3. **Appliquez une optimisation** (ex: GameMode)

4. **Rejouez dans la même zone**

5. **Comparez les logs**

### Benchmarking standardisé

**Créez un "parcours de benchmark"** :
1. Même zone du jeu
2. Même durée (ex: 2 minutes)
3. Même actions (marcher, regarder autour)
4. Notez tous les résultats

**Exemple avec The Witcher 3** :
- Zone : Novigrad, place du marché
- Durée : 120 secondes
- Action : Marcher en cercle
- Météo : Ensoleillé, midi

## Alternatives à MangoHud

### GALLIUM HUD (OpenGL seulement)

Intégré aux drivers Mesa.

```bash
# Activer
GALLIUM_HUD=fps glxgears

# Infos CPU/GPU
GALLIUM_HUD="fps,cpu,gpu-load" ./jeu
```

**Avantages** :
- Déjà installé (pas de dépendance)
- Très léger

**Inconvénients** :
- OpenGL uniquement (pas Vulkan)
- Moins configurable

### Steam FPS counter

**Activer** :
1. Steam → Paramètres → En jeu
2. **Affichage fréquence d'images dans le jeu** : Position au choix

**Avantages** :
- Intégré à Steam
- Très simple

**Inconvénients** :
- FPS uniquement
- Pas de température, CPU, GPU, etc.

### NVIDIA FrameView (NVIDIA uniquement)

Outil NVIDIA pour monitoring détaillé.

**Limitations** :
- NVIDIA seulement
- Windows principalement (Linux expérimental)

## Conseils d'utilisation

### Positionnement optimal

**Top-left** : Bon pour streaming (pas sur interface jeu)
**Top-right** : Classique, peu intrusif
**Bottom-right** : Si interface jeu en haut
**Bottom-left** : Si map du jeu en bas à droite

### Informations essentielles

**Minimum vital** :
- FPS
- GPU temp
- CPU temp

**Pour diagnostic** :
- + GPU load / CPU load
- + Frame timing

**Pour benchmarking** :
- Tout + logging

### Performance impact

MangoHud a un impact minimal mais réel :

**Configuration minimale** : ~1-2% impact
**Configuration complète** : ~3-5% impact
**Avec graphiques** : ~5-8% impact

**Recommandation** : Ajustez selon vos besoins.

### Couleurs personnalisées

**Schéma "Matrix"** :
```ini
text_color=00FF00
gpu_color=00AA00
cpu_color=00FF00
background_color=000000
```

**Schéma "Cyberpunk"** :
```ini
text_color=FF00FF
gpu_color=00FFFF
cpu_color=FFFF00
background_color=1A001A
```

**Schéma "Discret"** :
```ini
text_color=CCCCCC
gpu_color=999999
cpu_color=999999
background_alpha=0.2
```

## Exemples de configurations complètes

### Configuration "Pro Gamer"

```ini
# Minimal, haute performance, top-right
position=top-right
no_display
toggle_hud=Shift+F12

fps
font_size=20
text_color=00FF00
background_alpha=0.2
```

### Configuration "Streamer"

```ini
# Complète, visible, professionnelle
position=top-left

fps
frametime=1
gpu_stats
gpu_temp
cpu_stats
cpu_temp
ram
vram
gamemode
resolution

font_size=24
background_alpha=0.5
text_color=FFFFFF
round_corners=8
```

### Configuration "Benchmark"

```ini
# Logging automatique, données complètes
position=top-right

fps
frametime=1
frame_timing=1
gpu_stats
gpu_temp
gpu_power
cpu_stats
cpu_temp
ram
vram

output_folder=~/mangohud-benchmarks
log_duration=300
autostart_log=1

font_size=22
background_alpha=0.4
```

### Configuration "Laptop"

```ini
# Focus température et batterie
position=top-right

fps
gpu_temp
cpu_temp
battery

font_size=22
background_alpha=0.4
text_color=FFAA00
```

## Documentation et ressources

### Documentation officielle

- **GitHub MangoHud** : https://github.com/flightlessmango/MangoHud
- **README** : Liste complète des options

### Communauté

- **Reddit r/linux_gaming** : Partage de configurations
- **Discord FlightlessMango** : Support direct
- **GitHub Issues** : Bugs et demandes de fonctionnalités

### Configurations partagées

Cherchez "mangohud config" sur GitHub pour des configurations partagées.

## Conclusion

MangoHud est un outil indispensable pour tout joueur Linux sérieux. Il permet de surveiller les performances, diagnostiquer les problèmes et optimiser l'expérience de jeu.

**Points clés à retenir** :
- ✅ Installation simple via APT
- ✅ Configuration par fichier texte (ou GOverlay)
- ✅ Fonctionne avec Steam, Lutris, Heroic
- ✅ Impact minimal sur les performances
- ✅ Logging pour analyse approfondie
- ✅ Hautement personnalisable

**Configuration recommandée pour débuter** :
```ini
position=top-left
fps
gpu_stats
gpu_temp
cpu_stats
cpu_temp
ram
vram
font_size=24
background_alpha=0.5
```

Avec MangoHud, vous avez un contrôle total sur les performances de vos jeux et pouvez facilement identifier et résoudre les problèmes. Bon monitoring ! 🎮📊

---


⏭️ [GameMode pour performances](/14-gaming-sous-linux/08-gamemode-pour-performances.md)
