🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 14.4 Émulateurs de consoles (RetroArch)

## Introduction

L'émulation permet de jouer à des jeux de consoles rétro (NES, SNES, PlayStation, Game Boy, etc.) sur votre ordinateur Linux. RetroArch est la solution la plus complète et populaire pour l'émulation multi-systèmes.

**RetroArch, c'est :**
- Un "frontend" qui centralise de nombreux émulateurs
- Une interface unifiée pour toutes vos consoles rétro
- Un système de "cores" (émulateurs modulaires)
- Des fonctionnalités avancées (shaders, netplay, rewind, etc.)
- Compatible avec plus de 80 systèmes différents
- 100% gratuit et open-source

## Qu'est-ce que l'émulation ?

### Principe de base

Un émulateur est un logiciel qui imite le fonctionnement d'une console de jeux. Il "traduit" les instructions du jeu original pour qu'elles fonctionnent sur votre ordinateur.

**Exemple simple** :
- Un jeu Super Nintendo attend des boutons SNES
- L'émulateur traduit vos touches clavier/manette en boutons SNES
- Le jeu fonctionne comme sur la console originale

### Avantages de l'émulation

- 💾 **Préservation** : Jouer à des jeux de consoles obsolètes
- 🎮 **Confort** : Manette moderne, sauvegarde rapide, pause
- 🖥️ **Qualité** : Résolution améliorée, filtres graphiques
- 🌍 **Accessibilité** : Jeux de toutes les régions
- 💰 **Économie** : Une seule machine pour toutes les consoles

## Comprendre RetroArch

### Architecture de RetroArch

RetroArch fonctionne avec des **cores** :

**Core** = Émulateur spécialisé pour un système
- **Snes9x** : Core pour Super Nintendo
- **Mupen64Plus** : Core pour Nintendo 64
- **PCSX ReARMed** : Core pour PlayStation 1
- **mGBA** : Core pour Game Boy Advance

**RetroArch = Interface + Cores**

### RetroArch vs émulateurs standalone

| RetroArch | Émulateurs séparés |
|-----------|-------------------|
| Une interface pour tout | Une application par console |
| Configuration unifiée | Configuration différente par émulateur |
| Fonctionnalités communes | Fonctionnalités variables |
| Courbe d'apprentissage moyenne | Plus simple individuellement |
| Recommandé pour collection | Recommandé pour un seul système |

## Installation de RetroArch

### Méthode 1 : Via Flatpak (recommandée)

```bash
# Installation de RetroArch
flatpak install flathub org.libretro.RetroArch

# Lancement
flatpak run org.libretro.RetroArch
```

### Méthode 2 : Via le gestionnaire de logiciels

1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez **"RetroArch"**
3. Installez la version **Flatpak**
4. Lancez depuis le menu Applications

### Méthode 3 : Via le PPA (version native)

```bash
# Ajout du dépôt
sudo add-apt-repository ppa:libretro/stable

# Mise à jour
sudo apt update

# Installation
sudo apt install retroarch
```

> **Recommandation** : La version Flatpak est plus récente et mieux isolée.

## Premier lancement et interface

### Premier démarrage

Au premier lancement, RetroArch affiche son interface principale :

**Menu principal (par défaut : XMB)** :
- Interface similaire à PlayStation 3/PSP
- Navigation horizontale par catégories
- Navigation verticale dans chaque catégorie

**Thèmes d'interface disponibles** :
- **XMB** : Style PlayStation (par défaut)
- **Ozone** : Interface moderne et épurée
- **RGUI** : Interface rétro minimaliste

### Navigation dans l'interface

**Contrôles clavier par défaut** :
- **Flèches ← →** : Changer de catégorie
- **Flèches ↑ ↓** : Naviguer dans les options
- **Entrée** : Sélectionner
- **Retour arrière** : Retour
- **Échap** : Quitter

**Catégories principales** :
- 🏠 **Main Menu** : Menu principal
- ⬇️ **Load Core** : Charger un émulateur
- ➕ **Load Content** : Charger un jeu
- 📚 **Import Content** : Scanner vos jeux
- ⚙️ **Settings** : Paramètres
- 🛠️ **Online Updater** : Télécharger cores et assets

## Concepts essentiels

### Les ROMs

Une **ROM** est le fichier du jeu, copié depuis la cartouche ou CD original.

**Formats courants** :
- **NES** : .nes
- **SNES** : .smc, .sfc
- **Game Boy** : .gb, .gbc
- **Game Boy Advance** : .gba
- **Nintendo 64** : .z64, .n64
- **PlayStation** : .bin/.cue, .chd
- **Sega Genesis** : .bin, .md

**Organisation recommandée** :
```
~/Roms/
├── NES/
│   ├── Super Mario Bros.nes
│   └── Zelda.nes
├── SNES/
│   ├── Super Mario World.sfc
│   └── Zelda - A Link to the Past.sfc
├── GB/
├── GBA/
├── N64/
└── PS1/
```

### Les BIOS

Certaines consoles nécessitent des fichiers **BIOS** (système d'exploitation de la console).

**Consoles nécessitant un BIOS** :
- **PlayStation 1** : scph5500.bin, scph5501.bin, scph5502.bin
- **PlayStation 2** : SCPH10000.bin, etc.
- **Sega Saturn** : saturn_bios.bin
- **Dreamcast** : dc_boot.bin, dc_flash.bin

**Emplacement BIOS** :
```
~/.config/retroarch/system/
```

Pour Flatpak :
```
~/.var/app/org.libretro.RetroArch/config/retroarch/system/
```

### Les Cores

Les cores sont les émulateurs que RetroArch utilise.

**Plusieurs cores par système** :
- SNES : Snes9x (précis), bsnes (très précis mais lourd)
- PlayStation : PCSX ReARMed (rapide), Beetle PSX (précis)
- Game Boy : Gambatte (précis), mGBA (bon compromis)

## Installer des cores

### Via l'Online Updater

1. **Main Menu** → **Online Updater**
2. **Core Downloader**
3. Parcourez la liste des cores
4. Sélectionnez le core à installer (exemple : **Nintendo - SNES / SFC (Snes9x)**)
5. Le core se télécharge et s'installe automatiquement

### Cores recommandés pour débuter

**Nintendo** :
- **Nintendo - NES / Famicom (Mesen)** : NES/Famicom
- **Nintendo - SNES / SFC (Snes9x - Current)** : Super Nintendo
- **Nintendo - Game Boy / Color (Gambatte)** : Game Boy
- **Nintendo - Game Boy Advance (mGBA)** : Game Boy Advance
- **Nintendo - Nintendo 64 (Mupen64Plus-Next)** : Nintendo 64
- **Nintendo - GameCube / Wii (Dolphin)** : GameCube/Wii

**Sega** :
- **Sega - MS/GG/MD/CD (Genesis Plus GX)** : Master System, Game Gear, Mega Drive
- **Sega - Saturn (Beetle Saturn)** : Saturn
- **Sega - Dreamcast (Flycast)** : Dreamcast

**Sony** :
- **Sony - PlayStation (PCSX ReARMed)** : PlayStation 1
- **Sony - PlayStation (Beetle PSX HW)** : PS1 (amélioré)
- **Sony - PlayStation 2 (LRPS2)** : PlayStation 2

**Autres** :
- **Arcade (FinalBurn Neo)** : Jeux d'arcade
- **DOS (DOSBox-Pure)** : Jeux MS-DOS

> **Astuce** : Commencez par télécharger uniquement les cores dont vous avez besoin.

## Lancer un jeu

### Méthode simple (Load Content)

1. **Main Menu** → **Load Content**
2. Naviguez jusqu'à votre dossier de ROMs (ex: `~/Roms/SNES/`)
3. Sélectionnez votre jeu (ex: `Super Mario World.sfc`)
4. RetroArch détecte le système et propose un core
5. Sélectionnez le core (ex: **Snes9x**)
6. Le jeu se lance !

### Méthode avancée (charger le core d'abord)

1. **Main Menu** → **Load Core**
2. Sélectionnez le core (ex: **Snes9x**)
3. **Main Menu** → **Load Content**
4. Sélectionnez votre jeu
5. Le jeu se lance avec le core choisi

### Quick Menu (en jeu)

Une fois le jeu lancé, appuyez sur **F1** (ou **Retour arrière**) pour ouvrir le Quick Menu :

- **Resume** : Reprendre le jeu
- **Save State** : Sauvegarde rapide
- **Load State** : Charger une sauvegarde rapide
- **Options** : Options spécifiques au core
- **Controls** : Configuration des contrôles
- **Close Content** : Fermer le jeu

## Configuration des contrôleurs

### Manette automatique

RetroArch détecte automatiquement la plupart des manettes modernes :
- Xbox 360/One
- PlayStation 3/4/5
- Nintendo Switch Pro Controller
- Manettes génériques USB

### Configuration manuelle

Si votre manette n'est pas détectée :

1. **Settings** → **Input**
2. **Port 1 Controls**
3. **Set All Controls**
4. Appuyez sur chaque bouton demandé dans l'ordre
5. **Save Configuration**

### Hotkeys (raccourcis clavier)

**Raccourcis par défaut en jeu** :
- **F1** : Menu RetroArch
- **F2** : Sauvegarde rapide (Save State)
- **F4** : Charger sauvegarde rapide (Load State)
- **F3** : Screenshot
- **P** : Pause
- **Espace** : Avance rapide (Fast Forward)
- **R** : Rewind (rembobiner le temps)

### Configurer les hotkeys

1. **Settings** → **Input** → **Hotkeys**
2. Personnalisez chaque raccourci
3. **Save Configuration**

## Sauvegardes

### Types de sauvegardes

**Save States (sauvegardes rapides)** :
- Sauvegardes instantanées de l'état du jeu
- Peuvent être faites n'importe quand
- 10 emplacements disponibles
- Appuyez sur **F2** pour sauvegarder, **F4** pour charger

**SRAM Saves (sauvegardes du jeu)** :
- Sauvegardes normales du jeu (comme sur console)
- Créées automatiquement
- Compatible avec les vraies consoles

### Gérer les Save States

**Changer d'emplacement** :
1. Appuyez sur **F1** (Menu)
2. **Save State**
3. **State Slot** : Choisissez un emplacement (0-9)
4. **Save State** ou **Load State**

**Emplacement des sauvegardes** :
```
~/.config/retroarch/states/
```

Pour Flatpak :
```
~/.var/app/org.libretro.RetroArch/config/retroarch/states/
```

## Import et scan de jeux

### Scanner votre bibliothèque

RetroArch peut scanner vos ROMs et créer des playlists automatiques.

**Procédure** :

1. **Main Menu** → **Import Content**
2. **Scan Directory**
3. Naviguez jusqu'à votre dossier ROMs principal (ex: `~/Roms/`)
4. Sélectionnez le dossier
5. RetroArch scanne tous les sous-dossiers
6. Les playlists sont créées automatiquement

**Résultat** :
- Nouvelles catégories dans le menu principal (Nintendo SNES, Nintendo 64, etc.)
- Chaque jeu avec son titre complet et artwork (si disponible)

### Télécharger les thumbnails (miniatures)

1. **Main Menu** → **Online Updater**
2. **Thumbnail Updater**
3. Sélectionnez le système (ex: **Nintendo - Super Nintendo Entertainment System**)
4. RetroArch télécharge les images de chaque jeu

Vos jeux auront maintenant de belles jaquettes !

## Shaders et améliorations graphiques

### Qu'est-ce qu'un shader ?

Les shaders sont des filtres graphiques qui améliorent ou transforment l'image :
- **CRT** : Simule un vieux téléviseur à tube cathodique
- **LCD** : Simule un écran Game Boy
- **xBR** : Lissage intelligent des pixels
- **Scanlines** : Ajoute des lignes de balayage rétro

### Activer un shader

**En jeu** :

1. **F1** (Menu) → **Quick Menu**
2. **Shaders**
3. **Load Shader Preset**
4. Parcourez les catégories :
   - **crt/** : Effets CRT
   - **handheld/** : Effets LCD/Game Boy
   - **scalefx/** : Amélioration des pixels
5. Sélectionnez un shader (ex: **crt-royale.glslp**)
6. **Apply Changes**

### Shaders recommandés par système

**Game Boy / Game Boy Color** :
- `handheld/lcd-shader/` : Simule l'écran LCD
- `handheld/gameboy/` : Effet Game Boy authentique

**NES / SNES** :
- `crt/crt-royale.glslp` : CRT haute qualité
- `scanlines` : Lignes de balayage simples

**PlayStation / Nintendo 64** :
- `crt/crt-aperture.glslp` : CRT moderne
- `scalefx/` : Lissage sans flou

### Sauvegarder une configuration shader

1. **Quick Menu** → **Shaders**
2. **Save** → **Save Core Preset**

Le shader s'appliquera automatiquement à tous les jeux de ce système.

## Configuration par système/jeu

### Configurer un système entier

**Exemple : Activer rewind pour tous les jeux SNES**

1. Lancez un jeu SNES
2. **F1** → **Quick Menu** → **Settings**
3. **Rewind** → **Enable** : ON
4. **Quick Menu** → **Overrides** → **Save Core Overrides**

Cette configuration s'applique maintenant à tous les jeux SNES.

### Configurer un jeu spécifique

**Exemple : Activer un cheat pour un jeu précis**

1. Lancez le jeu
2. **F1** → **Quick Menu** → **Options**
3. Modifiez les options
4. **Overrides** → **Save Game Overrides**

Cette configuration est spécifique à ce jeu uniquement.

## Fonctionnalités avancées

### Rewind (rembobiner le temps)

Permet de remonter le temps en jeu (comme un DVR).

**Activation** :

1. **Settings** → **Rewind**
2. **Enable Rewind** : ON
3. **Rewind Buffer Size** : 20 MB (par défaut)

**Utilisation** :
- Maintenez **R** (ou configurez une touche) pour rembobiner

> **Note** : Consomme des ressources. Désactivez sur systèmes lourds (PS2, N64).

### Netplay (jeu en ligne)

Jouez à des jeux multijoueurs en ligne avec des amis.

**Héberger une partie** :

1. **Main Menu** → **Online** → **Netplay**
2. **Host**
3. **Start Netplay Session**
4. Donnez votre adresse IP à vos amis

**Rejoindre une partie** :

1. **Netplay** → **Connect to Netplay Server**
2. Entrez l'adresse IP de l'hôte
3. **Connect**

### Run-Ahead (réduction de latence)

Réduit le délai entre l'appui sur un bouton et l'action à l'écran.

**Activation** :

1. **Settings** → **Latency**
2. **Run-Ahead** : ON
3. **Number of Frames** : 1 ou 2

> **Attention** : Consomme beaucoup de ressources. Testez d'abord.

### Cheats (codes de triche)

RetroArch supporte les codes de triche pour certains systèmes.

**Utilisation** :

1. Lancez le jeu
2. **F1** → **Quick Menu** → **Cheats**
3. **Load Cheat File** → Sélectionnez le fichier .cht
4. Activez les cheats désirés
5. **Apply Changes**

**Télécharger des cheats** :

1. **Main Menu** → **Online Updater**
2. **Update Cheats**

## Problèmes courants et solutions

### Le jeu ne se lance pas

**Solutions** :

1. **Vérifiez le format de ROM** : Certains cores n'acceptent que certains formats
2. **Vérifiez le BIOS** : PlayStation, Saturn nécessitent un BIOS
3. **Essayez un autre core** : Certains cores fonctionnent mieux que d'autres
4. **Consultez les logs** : Menu → Settings → Logging

### Performance médiocre / lag

**Solutions** :

1. **Désactivez Rewind** temporairement
2. **Désactivez les shaders** complexes
3. **Changez de core** : Cores "Accuracy" sont plus lourds
4. **Réduisez la résolution interne** (Settings → Video)
5. **Activez Threaded Video** (Settings → Video → Threaded Video)

### Pas de son

**Solutions** :

1. **Settings** → **Audio**
2. **Audio Driver** : Changez (pulse, alsa)
3. **Audio Device** : Sélectionnez le bon périphérique
4. Vérifiez que PipeWire est actif (chapitre 12.6)

### Contrôleur non détecté

**Solutions** :

1. Branchez la manette AVANT de lancer RetroArch
2. **Settings** → **Input** → **Port 1 Controls**
3. **Device Index** : Sélectionnez votre manette
4. **Set All Controls** pour reconfigurer

### Jeu trop rapide

**Solutions** :

1. **Settings** → **Frame Throttle**
2. **VSync** : ON
3. **Maximum Run Speed** : 1.0x

### Sauvegardes qui ne fonctionnent pas

**Solutions** :

1. **Settings** → **Saving**
2. **SaveRAM Autosave Interval** : 10 seconds
3. Vérifiez les permissions du dossier saves

## Personnalisation de l'interface

### Changer de thème d'interface

1. **Settings** → **Drivers** → **Menu**
2. Choisissez :
   - **xmb** : Style PlayStation
   - **ozone** : Interface moderne
   - **rgui** : Interface rétro
3. Redémarrez RetroArch

### Télécharger des assets

Pour de belles icônes et fonds :

1. **Main Menu** → **Online Updater**
2. **Update Assets**
3. Patientez pendant le téléchargement

### Couleurs et thèmes

1. **Settings** → **User Interface** → **Menu**
2. **Menu Color Theme** : Choisissez une palette
3. **Menu Wallpaper** : Changez le fond d'écran

## Configuration des dossiers

### Définir les dossiers par défaut

1. **Settings** → **Directory**
2. Configurez :
   - **System/BIOS** : Où mettre les BIOS
   - **File Browser** : Dossier par défaut des ROMs
   - **Savefile** : Où sauvegarder
   - **Savestate** : Où stocker les save states
   - **Screenshots** : Où sauvegarder les captures d'écran

### Séparer les sauvegardes par core

1. **Settings** → **Saving**
2. **Sort Saves Into Folders By Core Name** : ON
3. **Sort Savestates Into Folders By Core Name** : ON

Organisation plus claire des sauvegardes !

## Systèmes spécifiques

### PlayStation 1

**BIOS requis** :
- scph5500.bin (Japon)
- scph5501.bin (USA)
- scph5502.bin (Europe)

Placez-les dans `~/.config/retroarch/system/`

**Core recommandé** :
- **PCSX ReARMed** : Rapide, excellent
- **Beetle PSX HW** : Plus précis, shaders avancés

**Format ROM** :
- .bin/.cue (standard)
- .chd (compressé, recommandé)

### Nintendo 64

**BIOS non requis**

**Core recommandé** :
- **Mupen64Plus-Next** : Meilleur compromis
- **ParaLLEl N64** : Plus précis mais lourd

**Configuration** :

1. Lancez un jeu N64
2. **Quick Menu** → **Options**
3. **GFX Plugin** : glide64 ou GLideN64
4. **RSP Plugin** : HLE (rapide) ou CXD4 (précis)

### Game Boy / Game Boy Color

**Core recommandé** :
- **Gambatte** : Très précis
- **SameBoy** : Excellent aussi

**Shader recommandé** :
```
handheld/lcd-shader/lcd-shader-4k.glslp
```

Simule parfaitement l'écran LCD du Game Boy !

### Arcade (MAME / FinalBurn Neo)

**Core recommandé** :
- **FinalBurn Neo** : Large compatibilité
- **MAME** : Maximum de jeux

**Organisation** :
- Les ROMs arcade sont des .zip
- Ne décompressez PAS les fichiers
- Certains jeux nécessitent des "parent ROMs"

**Set de ROMs** :
- Les ROMs arcade ont des "versions" (0.78, current)
- Utilisez des ROMs compatibles avec votre core

## Aspects légaux de l'émulation

### Ce qui est légal

- ✅ **Développer/utiliser un émulateur** : Totalement légal
- ✅ **Dumper vos propres jeux** : Vous possédez la cartouche/CD
- ✅ **Dumper vos propres BIOS** : De votre console personnelle
- ✅ **Homebrew games** : Jeux créés par la communauté

### Ce qui est illégal

- ❌ **Télécharger des ROMs** : Même si vous possédez le jeu
- ❌ **Télécharger des BIOS** : Propriété intellectuelle
- ❌ **Partager des ROMs** : Distribution illégale

### Zone grise

- ⚠️ **ROMs de jeux possédés** : Légalement discutable selon les pays
- ⚠️ **Jeux abandonnés** : Toujours sous copyright malgré l'absence de vente

### Recommandations

1. **Dumpez vos propres jeux** : Dispositifs légaux existent
2. **Achetez les compilations officielles** : Nombreuses collections sur Steam
3. **Homebrew** : De nombreux jeux gratuits créés par fans
4. **Collections rétro légales** : Internet Archive propose des jeux du domaine public

> **Disclaimer** : Ce tutoriel explique l'utilisation de RetroArch, pas comment obtenir illégalement des ROMs.

## Alternatives à RetroArch

### Émulateurs standalone recommandés

**Si RetroArch vous semble trop complexe** :

**Nintendo** :
- **Dolphin** : GameCube/Wii (meilleur que le core RetroArch)
- **Citra** : Nintendo 3DS
- **yuzu / Ryujinx** : Nintendo Switch

**Sony** :
- **PCSX2** : PlayStation 2
- **RPCS3** : PlayStation 3

**Multi-systèmes** :
- **Mednafen** : Interface simple, plusieurs systèmes
- **BizHawk** : Pour speedrunners et TAS

**Avantages des standalone** :
- Configuration plus simple
- Parfois meilleures performances
- Interface dédiée

## Frontends alternatifs à RetroArch

### EmulationStation

Interface graphique pour lancer émulateurs et ROMs.

**Avantages** :
- Interface "console" élégante
- Navigation manette uniquement
- Parfait pour un "retro console" dédié

**Installation** :
```bash
sudo apt install emulationstation
```

### Lutris (déjà couvert)

Peut aussi gérer vos ROMs et émulateurs.

### Pegasus Frontend

Interface moderne et personnalisable.

## Optimisation pour performances

### Paramètres recommandés

**Pour maximiser les FPS** :

1. **Settings** → **Video**
   - **VSync** : OFF (si screen tearing acceptable)
   - **Threaded Video** : ON
   - **Hard GPU Sync** : OFF

2. **Settings** → **Audio**
   - **Audio Latency** : 64 ms ou moins

3. **Shaders** : Désactivez ou utilisez des simples (scanlines)

4. **Rewind** : OFF si pas nécessaire

### Frame Skipping

Si les jeux sont trop lents :

1. **Settings** → **Frame Throttle**
2. **Frame Skip** : 1 ou 2

> **Note** : L'animation sera moins fluide mais plus rapide.

## Sauvegarder et restaurer votre configuration

### Exporter la configuration

```bash
# Sauvegarder le dossier RetroArch
cp -r ~/.config/retroarch ~/retroarch-backup

# Pour Flatpak
cp -r ~/.var/app/org.libretro.RetroArch/config/retroarch ~/retroarch-backup
```

### Restaurer

```bash
# Restaurer depuis la sauvegarde
cp -r ~/retroarch-backup/* ~/.config/retroarch/

# Pour Flatpak
cp -r ~/retroarch-backup/* ~/.var/app/org.libretro.RetroArch/config/retroarch/
```

## Ressources et communauté

### Sites officiels

- **Site RetroArch** : https://www.retroarch.com/
- **Documentation** : https://docs.libretro.com/
- **Cores disponibles** : https://buildbot.libretro.com/

### Communauté

- **Reddit r/emulation** : Communauté émulation générale
- **Reddit r/RetroArch** : Spécifique à RetroArch
- **Forums LibRetro** : Support technique
- **Discord RetroArch** : Aide en temps réel

### Bases de données de jeux

- **No-Intro** : Sets de ROMs vérifiées (cartouches)
- **Redump** : Sets de ROMs vérifiées (CD/DVD)
- **TOSEC** : Préservation de logiciels anciens

> **Rappel** : Télécharger des ROMs est généralement illégal. Ces sites documentent, ne distribuent pas.

### Homebrew et jeux légaux

- **itch.io** : Nombreux homebrew gratuits
- **GB Studio games** : Jeux Game Boy modernes
- **PDRoms** : Base de données homebrew

## Conseils pour une utilisation optimale

1. **Commencez simple** : Un système à la fois (SNES, par exemple)
2. **Organisez vos ROMs** : Dossiers clairs par système
3. **Scannez votre bibliothèque** : Interface bien plus agréable
4. **Configurez votre manette** : Une fois pour toutes
5. **Téléchargez les thumbnails** : Visuellement plus plaisant
6. **Essayez différents cores** : Performances vs précision
7. **Expérimentez les shaders** : Trouvez votre style préféré
8. **Sauvegardez souvent** : Save States sont vos amis
9. **Consultez la documentation** : Cores ont des options spécifiques
10. **Soyez patient** : RetroArch est puissant mais demande un apprentissage

## Conclusion

RetroArch est la solution la plus complète pour l'émulation sous Linux. Une fois configuré, vous aurez accès à des décennies d'histoire du jeu vidéo dans une seule interface unifiée.

**Points clés à retenir** :
- ✅ RetroArch = Frontend + Cores (émulateurs)
- ✅ Installez uniquement les cores nécessaires
- ✅ Organisez vos ROMs par système
- ✅ Les shaders améliorent l'expérience visuelle
- ✅ Save States = sauvegarde rapide partout
- ✅ Respectez les lois sur la propriété intellectuelle
- ✅ La communauté est une excellente ressource

Avec RetroArch, vous pouvez redécouvrir les classiques de votre enfance ou découvrir l'âge d'or du jeu vidéo avec le confort moderne. Profitez de votre voyage dans le temps vidéoludique ! 🎮🕹️

---


⏭️ [Jeux natifs Linux (liste recommandée)](/14-gaming-sous-linux/05-jeux-natifs-linux.md)
