🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 13.4 Lecture et organisation multimédia

## Introduction

Linux Mint offre une expérience multimédia complète et fluide, capable de lire pratiquement tous les formats vidéo, audio et image. Que vous souhaitiez regarder des films, écouter de la musique, organiser vos photos ou gérer votre collection multimédia, vous trouverez tous les outils nécessaires.

Dans ce chapitre, nous allons découvrir :

- **Les lecteurs multimédia** : VLC, Celluloid, Clementine et autres
- **L'organisation musicale** : bibliothèques, tags, playlists
- **La gestion de photos** : visionneuses, organisation, métadonnées
- **Les formats et codecs** : comprendre et lire tous les formats
- **Les bibliothèques multimédia** : centraliser et organiser vos médias

> **Bon à savoir** : Linux Mint lit "out of the box" pratiquement tous les formats multimédia, contrairement à certains autres systèmes qui nécessitent des achats de codecs.

---

## Comprendre les formats multimédia

### Formats vidéo courants

| Format | Extension | Description | Usage typique |
|--------|-----------|-------------|---------------|
| **MP4** | .mp4 | Universel, excellent | Vidéos web, films, smartphones |
| **MKV** | .mkv | Conteneur flexible | Films HD, archives |
| **AVI** | .avi | Ancien, compatible | Vieux fichiers |
| **MOV** | .mov | Format Apple | iPhone, Final Cut |
| **WebM** | .webm | Open source, web | Vidéos web, YouTube |
| **FLV** | .flv | Flash (obsolète) | Anciennes vidéos web |
| **WMV** | .wmv | Format Microsoft | Vieux fichiers Windows |
| **M4V** | .m4v | iTunes | Achats iTunes |

### Formats audio courants

| Format | Extension | Type | Qualité | Taille |
|--------|-----------|------|---------|--------|
| **MP3** | .mp3 | Avec perte | Bonne | Petite |
| **FLAC** | .flac | Sans perte | Parfaite | Moyenne |
| **AAC** | .aac, .m4a | Avec perte | Très bonne | Petite |
| **OGG Vorbis** | .ogg | Avec perte (libre) | Très bonne | Petite |
| **WAV** | .wav | Non compressé | Parfaite | Très grande |
| **ALAC** | .m4a | Sans perte Apple | Parfaite | Moyenne |
| **Opus** | .opus | Avec perte (moderne) | Excellente | Très petite |
| **WMA** | .wma | Microsoft | Moyenne | Moyenne |

### Formats image courants

| Format | Extension | Type | Usage |
|--------|-----------|------|-------|
| **JPEG** | .jpg, .jpeg | Compressé avec perte | Photos générales |
| **PNG** | .png | Compressé sans perte | Screenshots, graphiques |
| **GIF** | .gif | Animation | Animations courtes |
| **WebP** | .webp | Moderne, efficace | Web moderne |
| **TIFF** | .tif, .tiff | Non compressé | Photos professionnelles |
| **RAW** | .raw, .cr2, .nef | Non traité | Photos professionnelles |
| **BMP** | .bmp | Non compressé | Windows |
| **SVG** | .svg | Vectoriel | Icônes, logos |

### Qu'est-ce qu'un codec ?

Un **codec** (compresseur-décompresseur) est un programme qui encode et décode les données multimédia.

**Exemples :**
- **H.264** : codec vidéo très répandu (MP4, MKV)
- **H.265/HEVC** : codec vidéo moderne, meilleure compression
- **VP9** : codec vidéo libre (YouTube)
- **AAC** : codec audio de qualité
- **MP3** : codec audio classique

> **Analogie simple** : Un codec est comme une langue. Pour lire un fichier, votre lecteur doit "parler" le même codec que celui utilisé pour créer le fichier.

---

## VLC - Le couteau suisse du multimédia

### Qu'est-ce que VLC ?

VLC Media Player est LE lecteur multimédia universel. Il lit pratiquement tous les formats vidéo et audio existants, sans nécessiter l'installation de codecs supplémentaires.

**Points forts :**
- Lit TOUS les formats (ou presque)
- Gratuit et open source
- Léger et rapide
- Nombreuses fonctionnalités avancées
- Streaming réseau
- Conversion de formats
- Capture d'écran vidéo
- Interface personnalisable

**Utilisations principales :**
- Lire des vidéos (films, séries, clips)
- Écouter de la musique
- Lire des flux streaming (IPTV, radio web)
- Convertir des fichiers multimédia
- Extraire l'audio d'une vidéo
- Lire des DVD et Blu-ray

### Installation de VLC

VLC est généralement préinstallé sur Linux Mint. Si ce n'est pas le cas :

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "VLC"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update
sudo apt install vlc
```

### Interface de VLC

L'interface de VLC est épurée et intuitive :

**Éléments principaux :**
- **Zone de lecture** : affiche la vidéo
- **Barre de contrôle** (en bas) : lecture, pause, stop, volume
- **Barre de progression** : position dans la vidéo
- **Menu** : accès aux fonctionnalités avancées

### Utiliser VLC

#### Ouvrir un fichier

**Méthodes :**
1. Glissez-déposez le fichier sur VLC
2. Double-cliquez sur un fichier vidéo/audio (si VLC est le lecteur par défaut)
3. `Média` → `Ouvrir un fichier` (`Ctrl + O`)
4. Clic droit sur fichier → `Ouvrir avec` → `VLC`

#### Contrôles de lecture de base

| Action | Raccourci |
|--------|-----------|
| **Lecture/Pause** | Espace |
| **Stop** | S |
| **Plein écran** | F |
| **Sortir plein écran** | Échap ou F |
| **Avancer 10s** | Ctrl + → |
| **Reculer 10s** | Ctrl + ← |
| **Avancer 1min** | Alt + → |
| **Reculer 1min** | Alt + ← |
| **Volume +** | Ctrl + ↑ |
| **Volume -** | Ctrl + ↓ |
| **Muet** | M |
| **Image suivante** | E |
| **Ralenti** | - (moins) |
| **Accéléré** | + (plus) |
| **Vitesse normale** | = (égal) |

#### Fonctionnalités vidéo avancées

**Sous-titres :**
- `Sous-titres` → `Ajouter un fichier de sous-titres`
- Ou glissez-déposez le fichier .srt sur VLC pendant la lecture
- `Sous-titres` → `Piste de sous-titres` : changer de piste
- `J` / `H` : avancer/retarder la synchronisation

**Pistes audio :**
- `Audio` → `Piste audio` : choisir la langue
- Utile pour les films multilingues

**Ratio d'aspect :**
- `Vidéo` → `Rapport d'aspect` : 16:9, 4:3, etc.
- Ajuste l'affichage sans déformer

**Recadrage :**
- `Vidéo` → `Recadrer` : enlever les bandes noires

**Rotation :**
- `Outils` → `Effets et filtres` → `Effets vidéo` → `Géométrie`
- Cochez "Transformer" ou "Rotation"

**Capture d'écran :**
- `Vidéo` → `Prendre une capture d'écran`
- Ou `Shift + S`
- Sauvegarde dans ~/Images par défaut

#### Fonctionnalités audio avancées

**Égaliseur :**
- `Outils` → `Effets et filtres` → `Effets audio` → `Égaliseur`
- Ajustez les fréquences selon vos préférences
- Presets : Rock, Jazz, Classique, etc.

**Spatialisation :**
- `Audio` → `Canaux stéréo` : Stéréo, Mono, etc.

**Normalisation du volume :**
- `Outils` → `Préférences` → `Audio`
- Cochez "Normalisation du volume"

#### Lire des flux réseau

**IPTV, webcams, radios web :**
- `Média` → `Ouvrir un flux réseau` (`Ctrl + N`)
- Entrez l'URL du flux (ex: http://...)
- Cliquez sur **Lire**

**Lire un DVD :**
- Insérez le DVD
- `Média` → `Ouvrir un disque`
- Sélectionnez DVD et cliquez sur **Lire**

#### Playlists

**Créer une playlist :**
- `Vue` → `Liste de lecture` (`Ctrl + L`)
- Glissez-déposez plusieurs fichiers
- Sauvegardez : `Média` → `Sauvegarder la liste de lecture`

**Modes de lecture :**
- Lecture normale (séquentielle)
- Boucle (répéter tout)
- Répéter (répéter le fichier actuel)
- Aléatoire

#### Convertir des fichiers avec VLC

VLC peut convertir entre différents formats :

1. `Média` → `Convertir / Enregistrer` (`Ctrl + R`)
2. `Ajouter` : sélectionnez le(s) fichier(s) source
3. Cliquez sur **Convertir / Enregistrer**
4. Choisissez le **Profil** de sortie :
   - Vidéo : H.264 + MP3 (MP4), WebM, etc.
   - Audio : MP3, OGG Vorbis, FLAC
5. Choisissez le **Fichier de destination**
6. Cliquez sur **Démarrer**

**Cas d'usage courants :**
- Convertir MKV en MP4 (compatibilité)
- Extraire l'audio d'une vidéo (en MP3)
- Réduire la taille d'une vidéo

#### Enregistrer un flux

Pour sauvegarder un flux vidéo/audio :
- `Vue` → `Contrôles avancés`
- Un bouton **Enregistrer** (rond rouge) apparaît
- Lancez la lecture du flux
- Cliquez sur **Enregistrer** pour démarrer/arrêter

### Personnaliser VLC

**Changer l'apparence (skin) :**
- `Outils` → `Préférences` → `Interface`
- Cochez "Utiliser une interface personnalisée"
- Téléchargez des skins sur https://www.videolan.org/vlc/skins.html

**Toujours au premier plan :**
- `Vidéo` → `Toujours au premier plan`
- La vidéo reste visible même en travaillant

**Raccourcis clavier personnalisés :**
- `Outils` → `Préférences` → `Afficher les paramètres` : Tous
- `Interface` → `Raccourcis clavier`

---

## Autres lecteurs vidéo

### Celluloid (ex-GNOME MPV)

Celluloid est un lecteur vidéo moderne et minimaliste basé sur MPV.

**Points forts :**
- Interface très épurée
- Léger et rapide
- Supporte tous les formats (comme VLC)
- Support GPU excellent
- Lecture 4K fluide

**Installation :**
```bash
sudo apt install celluloid
```

**Quand l'utiliser :**
- Si vous préférez une interface minimaliste
- Pour la lecture 4K (meilleur support GPU que VLC)
- Si VLC vous semble trop chargé

### MPV

MPV est un lecteur en ligne de commande (mais avec interface graphique basique).

**Points forts :**
- Ultra-léger
- Qualité d'image exceptionnelle
- Configuration via fichiers texte
- Idéal pour les utilisateurs avancés

**Installation :**
```bash
sudo apt install mpv
```

**Utilisation :**
```bash
mpv fichier_video.mp4
```

**Raccourcis MPV :**
- `Espace` : Lecture/Pause
- `f` : Plein écran
- `s` : Capture d'écran
- `9` / `0` : Volume -/+
- `←` / `→` : Reculer/Avancer 5s

### SMPlayer

Interface graphique pour MPV avec plus de fonctionnalités.

**Installation :**
```bash
sudo apt install smplayer
```

**Points forts :**
- Reprend où vous vous êtes arrêté
- Recherche de sous-titres intégrée
- Nombreuses options de configuration

---

## Lecteurs audio et gestionnaires de musique

### Rhythmbox - Le lecteur par défaut

Rhythmbox est souvent le lecteur audio par défaut de Linux Mint avec GNOME/Cinnamon.

**Points forts :**
- Interface iTunes-like
- Bibliothèque musicale organisée
- Support podcasts
- Radio internet
- Plugins (paroles, visualisations)

**Fonctionnalités principales :**

**Importer de la musique :**
- `Musique` → `Importer un dossier`
- Ou glissez-déposez vos dossiers
- Rhythmbox scanne et organise automatiquement

**Organisation automatique :**
- Par artiste, album, genre, année
- Vue en grille ou liste
- Recherche rapide

**Playlists :**
- `Musique` → `Liste de lecture` → `Nouvelle liste de lecture`
- Glissez-déposez des morceaux
- Playlists intelligentes (critères automatiques)

**Éditer les tags :**
- Clic droit sur morceau → `Propriétés`
- Modifiez titre, artiste, album, genre, etc.

**Radio internet :**
- Onglet **Radio**
- Liste de stations pré-configurées
- Ajoutez vos propres URLs

### Clementine - L'alternative puissante

Clementine est un gestionnaire de musique très complet, inspiré d'Amarok.

**Points forts :**
- Interface personnalisable
- Support de nombreux services cloud
- Analyseur audio intégré
- Paroles synchronisées
- Conversion de formats
- Éditeur de tags puissant

**Installation :**
```bash
sudo apt install clementine
```

**Fonctionnalités uniques :**
- **Services en ligne** : intégration Google Drive, Dropbox, Spotify, etc.
- **Transcoder** : convertir fichiers audio
- **Égaliseur graphique** : 10 bandes
- **Visualisations** : spectres audio

**Configuration de la bibliothèque :**
1. `Outils` → `Préférences` → `Bibliothèque musicale`
2. Ajoutez vos dossiers de musique
3. Clementine scanne automatiquement

### Audacious - Léger et simple

Lecteur audio léger avec interface Winamp-like.

**Points forts :**
- Très léger
- Démarrage instantané
- Skins Winamp compatibles
- Égaliseur graphique

**Installation :**
```bash
sudo apt install audacious
```

**Idéal pour :**
- Ordinateurs anciens/peu puissants
- Écoute simple sans bibliothèque
- Nostalgie de Winamp

### Spotify

Le service de streaming musical fonctionne sous Linux.

**Installation :**
```bash
sudo snap install spotify
```

**Ou via Flatpak :**
```bash
flatpak install flathub com.spotify.Client
```

> **Note** : Version officielle Spotify avec toutes les fonctionnalités.

---

## Gestion et organisation de photos

### Visionneuses d'images

#### Xviewer / Eye of MATE

Visionneuse d'images légère préinstallée sur Linux Mint.

**Fonctionnalités :**
- Visualisation rapide
- Diaporama
- Rotation basique
- Zoom
- Navigation par flèches

**Raccourcis utiles :**
- `F11` : Plein écran
- `+` / `-` : Zoom
- `←` / `→` : Image précédente/suivante
- `F5` : Diaporama
- `R` / `Shift + R` : Rotation

#### gThumb

Visionneuse et organisateur de photos plus avancé.

**Installation :**
```bash
sudo apt install gthumb
```

**Fonctionnalités :**
- Gestion de catalogue
- Retouches basiques (recadrage, rotation, ajustements)
- Import depuis appareil photo
- Organisation par tags
- Recherche de doublons
- Conversion par lot

**Utilisation :**
- **Importer** : `Fichier` → `Importer de` → appareil/dossier
- **Catalogues** : organisez par événements/dates
- **Retouches** : sélectionnez photo → bouton "Éditer"

#### Nomacs

Visionneuse d'images moderne et rapide.

**Installation :**
```bash
sudo apt install nomacs
```

**Points forts :**
- Aperçu en miniatures
- Comparaison côte-à-côte
- Métadonnées EXIF visibles
- Synchronisation multi-fenêtres

### Gestionnaires de photos avancés

#### Shotwell

Gestionnaire de photos complet, similaire à iPhoto/Photos.

**Installation :**
```bash
sudo apt install shotwell
```

**Fonctionnalités :**
- Import depuis appareil photo
- Organisation chronologique
- Albums et événements
- Tags et notes
- Reconnaissance des visages (basique)
- Retouches simples
- Export vers services web (Flickr, etc.)
- Diaporama

**Workflow typique :**
1. **Importer** : connectez appareil → Shotwell détecte → importez
2. **Organiser** : créez des événements, ajoutez des tags
3. **Retoucher** : recadrer, ajuster couleurs, yeux rouges
4. **Partager** : exportez ou publiez directement

#### digiKam

Gestionnaire de photos professionnel pour photographes sérieux.

**Installation :**
```bash
sudo apt install digikam
```

**Points forts :**
- Gestion de collections énormes (dizaines de milliers)
- Base de données SQLite ou MySQL
- Métadonnées EXIF/IPTC complètes
- Géolocalisation (carte des photos)
- Reconnaissance faciale avancée
- Retouches RAW (développement)
- Recherche floue (par similarité)
- Étiquetage hiérarchique

**Idéal pour :**
- Photographes amateurs/pros
- Collections de plus de 10 000 photos
- Gestion de fichiers RAW
- Workflow professionnel

**Premier lancement :**
1. Choisissez l'emplacement de votre collection
2. Configurez la base de données (SQLite suffit pour débuter)
3. Scannez vos dossiers photos
4. Laissez digiKam analyser et créer les miniatures

#### Darktable

Gestionnaire et développeur RAW professionnel (alternative à Lightroom).

**Installation :**
```bash
sudo apt install darktable
```

**Points forts :**
- Développement RAW non destructif
- Gestion de bibliothèque
- Retouches avancées
- Modules professionnels
- Export en haute qualité

**Utilisateurs cibles :**
- Photographes qui shootent en RAW
- Besoin de développement pro
- Workflow Lightroom-like

> **Note** : Darktable est complexe. Nécessite apprentissage mais très puissant.

---

## Organisation de votre collection multimédia

### Structure de dossiers recommandée

Organisez vos médias de manière claire et cohérente :

```
~/Vidéos/
├── Films/
│   ├── Action/
│   ├── Comédie/
│   ├── Documentaires/
│   └── Séries/
├── Personnel/
│   ├── Vacances_2024/
│   ├── Anniversaire_Sophie/
│   └── Mariage_Paul/
└── Tutoriels/

~/Musique/
├── Par_Artiste/
│   ├── The_Beatles/
│   │   ├── Abbey_Road/
│   │   └── Revolver/
│   └── Pink_Floyd/
│       └── Dark_Side_of_the_Moon/
└── Playlists/

~/Images/
├── Photos/
│   ├── 2024/
│   │   ├── 01_Janvier/
│   │   ├── 02_Février/
│   │   └── ...
│   └── 2023/
├── Screenshots/
└── Téléchargements/
```

### Nommage de fichiers

**Bonnes pratiques :**
- **Évitez** : espaces, caractères spéciaux, accents
- **Préférez** : underscores `_` ou tirets `-`
- **Date** : format ISO (AAAA-MM-JJ) pour tri chronologique
- **Descriptif** : nom clair et significatif

**Exemples :**
- ✅ `2024-07-15_vacances_bretagne.jpg`
- ✅ `documentaire_ocean_HD.mp4`
- ✅ `pink_floyd-dark_side_of_the_moon-01-speak_to_me.flac`
- ❌ `VID20240715(1).mp4`
- ❌ `Photo été 2024 & vacances.jpg`

### Tags et métadonnées

**Métadonnées EXIF (photos) :**
- Automatiques : date, appareil, paramètres
- Modifiables : titre, description, copyright, GPS

**Tags ID3 (musique) :**
- Titre, Artiste, Album, Genre
- Année, Numéro de piste
- Pochette (album art)

**Éditeurs de tags recommandés :**
- **Photos** : digiKam, Shotwell, ExifTool
- **Musique** : EasyTAG, Kid3, Picard (MusicBrainz)

#### EasyTAG - Éditeur de tags audio

**Installation :**
```bash
sudo apt install easytag
```

**Fonctionnalités :**
- Édition par lot
- Renommage automatique depuis tags
- Tags depuis nom de fichier
- Pochettes d'album
- Support MP3, FLAC, OGG, etc.

**Workflow :**
1. Ouvrez votre dossier musique
2. Sélectionnez plusieurs fichiers
3. Éditez les champs communs (album, artiste, année)
4. Sauvegardez

#### Picard - Tags depuis MusicBrainz

**Installation :**
```bash
sudo apt install picard
```

**Fonctionnalités :**
- Reconnaissance audio (AcoustID)
- Tags automatiques depuis base de données MusicBrainz
- Pochettes haute résolution
- Très précis

**Utilisation :**
1. Glissez-déposez vos fichiers
2. Cliquez sur **Cluster**
3. Cliquez sur **Lookup** (ou **Scan** pour reconnaissance audio)
4. Vérifiez les correspondances
5. Sauvegardez

---

## Serveurs multimédia et streaming local

### Plex Media Server

Plex transforme votre ordinateur en serveur multimédia accessible depuis tous vos appareils.

**Points forts :**
- Interface magnifique
- Apps sur toutes les plateformes
- Streaming à distance
- Métadonnées et pochettes automatiques
- Transcodage automatique
- Utilisateurs multiples

**Installation :**
1. Téléchargez depuis https://www.plex.tv/downloads/
2. Choisissez la version Linux (.deb)
3. Installez :
```bash
sudo dpkg -i plexmediaserver_*.deb
```

**Configuration :**
1. Ouvrez http://localhost:32400/web
2. Créez un compte Plex
3. Ajoutez vos bibliothèques (Films, Séries, Musique)
4. Plex scanne et organise automatiquement

**Utilisation :**
- Accédez depuis navigateur, application mobile, TV
- Streamez votre bibliothèque partout
- Partagez avec famille/amis

### Jellyfin - Alternative libre à Plex

Jellyfin est 100% open source et gratuit, sans compte requis.

**Installation :**
```bash
# Ajout du dépôt Jellyfin
curl https://repo.jellyfin.org/install-debuntu.sh | sudo bash
```

**Avantages sur Plex :**
- Totalement gratuit
- Pas de compte cloud requis
- Plus de contrôle
- Pas de télémétrie

**Configuration similaire à Plex :**
1. Ouvrez http://localhost:8096
2. Créez votre compte administrateur local
3. Ajoutez vos bibliothèques

### Kodi - Centre multimédia

Kodi transforme votre PC en centre multimédia complet (home theater).

**Installation :**
```bash
sudo apt install kodi
```

**Points forts :**
- Interface 10-foot (pour TV)
- Plugins nombreux
- Skins magnifiques
- Contrôle manette/télécommande
- Perfect pour HTPC (Home Theater PC)

**Utilisation :**
- Lancez Kodi en plein écran
- Ajoutez vos sources vidéo/audio
- Naviguez avec clavier/manette/télécommande

---

## Codecs et support multimédia

### Installer les codecs complets

Linux Mint inclut la plupart des codecs, mais pour être certain :

```bash
sudo apt install ubuntu-restricted-extras
```

**Ceci installe :**
- Codecs audio : MP3, AAC
- Codecs vidéo : H.264, MPEG-4
- Fonts Microsoft (Arial, Times New Roman, etc.)
- Support Flash (obsolète mais parfois utile)

### Support DVD

**Pour lire des DVD commerciaux (chiffrés) :**
```bash
sudo apt install libdvd-pkg
sudo dpkg-reconfigure libdvd-pkg
```

> **Note** : La légalité varie selon les pays. Vérifiez votre législation locale.

### Codecs additionnels

**Pour support étendu :**
```bash
sudo apt install ffmpeg gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly
```

### Vérifier les codecs installés

**Dans VLC :**
- `Outils` → `Informations sur les codecs`
- Liste de tous les codecs disponibles

---

## Convertir et manipuler les médias

### Handbrake - Conversion vidéo

Handbrake est LE logiciel de conversion et compression vidéo.

**Installation :**
```bash
sudo apt install handbrake
```

**Utilisations :**
- Compresser des vidéos volumineuses
- Convertir entre formats
- Ripper des DVD
- Encoder pour appareils spécifiques

**Workflow basique :**
1. **Source** : ouvrez votre vidéo
2. **Destination** : choisissez nom et emplacement
3. **Preset** : sélectionnez un preset (ex: "Fast 1080p30")
4. **Start Encode** : lancez la conversion

**Presets courants :**
- **Fast 1080p30** : bon compromis qualité/taille
- **HQ 1080p30 Surround** : haute qualité
- **Android/iPhone** : optimisé pour mobiles

### FFmpeg - Outil en ligne de commande

FFmpeg est l'outil le plus puissant pour manipulation multimédia (en ligne de commande).

**Installation :**
```bash
sudo apt install ffmpeg
```

**Exemples d'utilisation :**

**Convertir vidéo :**
```bash
ffmpeg -i input.mkv -c:v libx264 -crf 23 -c:a aac output.mp4
```

**Extraire audio d'une vidéo :**
```bash
ffmpeg -i video.mp4 -vn -c:a copy audio.m4a
```

**Redimensionner vidéo :**
```bash
ffmpeg -i input.mp4 -vf scale=1280:720 output.mp4
```

**Couper vidéo (de 00:01:30 à 00:03:45) :**
```bash
ffmpeg -i input.mp4 -ss 00:01:30 -to 00:03:45 -c copy output.mp4
```

**Convertir audio :**
```bash
ffmpeg -i musique.wav -c:a libmp3lame -b:a 320k musique.mp3
```

**Créer GIF depuis vidéo :**
```bash
ffmpeg -i video.mp4 -vf "fps=10,scale=320:-1" -t 5 output.gif
```

> **Note** : FFmpeg est complexe mais extrêmement puissant. Consultez la documentation pour plus d'options.

### SoundConverter - Conversion audio graphique

Interface graphique simple pour conversion audio.

**Installation :**
```bash
sudo apt install soundconverter
```

**Fonctionnalités :**
- Conversion par lot
- Nombreux formats (MP3, OGG, FLAC, AAC, WAV)
- Conservation des tags
- Simple et rapide

**Utilisation :**
1. Glissez-déposez vos fichiers audio
2. Choisissez le format de sortie
3. Cliquez sur **Convertir**

---

## Astuces et optimisations

### Définir le lecteur par défaut

**Par type de fichier :**
1. Clic droit sur un fichier vidéo/audio
2. `Propriétés`
3. Onglet `Ouvrir avec`
4. Sélectionnez le lecteur souhaité
5. Cliquez sur **Définir par défaut**

### Activer l'accélération matérielle

**VLC :**
- `Outils` → `Préférences`
- `Entrée / Codecs`
- `Décodage accéléré par matériel` : Automatique ou VDPAU/VA-API

**MPV/Celluloid :**
- Activé par défaut sur matériel compatible

> **Résultat** : Lecture plus fluide, moins de CPU, meilleure autonomie (laptop).

### Lecture de fichiers lourds (4K, HEVC)

**Si vidéos 4K saccadées :**
1. Activez accélération matérielle
2. Utilisez MPV/Celluloid plutôt que VLC
3. Fermez autres applications
4. Vérifiez pilotes graphiques à jour

### Synchronisation audio/vidéo

**Dans VLC :**
- `Outils` → `Synchronisation de piste`
- Ajustez "Avance de la piste audio"
- Ou raccourcis : `K` (avancer audio), `J` (retarder audio)

### Capturer la pochette d'album manquante

**Avec Clementine :**
- Clic droit sur album sans pochette
- `Chercher la pochette`
- Clementine cherche automatiquement en ligne

**Avec Picard :**
- Lookup automatique trouve les pochettes haute résolution

**Manuellement :**
- Recherchez "nom_album cover" sur Google Images
- Sauvegardez en JPG (environ 500x500 px minimum)
- Nommez `cover.jpg` ou `folder.jpg`
- Placez dans le dossier de l'album

---

## Sauvegarder et archiver vos médias

### Stratégie de sauvegarde

**Règle 3-2-1 :**
- **3** copies de vos données
- Sur **2** supports différents (disque dur + NAS/cloud)
- **1** copie hors site (cloud, chez famille)

**Médias à sauvegarder en priorité :**
- Photos de famille irremplaçables
- Vidéos personnelles
- Musique achetée/rare

**Médias pouvant être re-téléchargés :**
- Films du commerce
- Séries
- Musique sur streaming

### Outils de sauvegarde

**rsync (ligne de commande) :**
```bash
rsync -av --progress ~/Images/ /media/disque_externe/Backup_Images/
```

**Déjà Dup (graphique) :**
```bash
sudo apt install deja-dup
```

**Back In Time :**
```bash
sudo apt install backintime-qt
```

### Cloud pour photos

**Services compatibles :**
- **Google Photos** : 15 Go gratuit (via navigateur)
- **Nextcloud** : auto-hébergé, illimité
- **pCloud** : jusqu'à 10 Go gratuit
- **MEGA** : 20 Go gratuit

**Synchronisation automatique :**
- rclone : outil en ligne de commande pour tous les clouds
- Insync : client Google Drive payant
- Nextcloud client : pour Nextcloud

---

## Dépannage courant

### VLC : Vidéo saccadée

**Solutions :**
1. Activez l'accélération matérielle (voir plus haut)
2. Augmentez le cache : `Outils` → `Préférences` → `Entrée / Codecs` → "Cache" : 1000 ms
3. Fermez autres applications
4. Essayez MPV/Celluloid

### Audio décalé de la vidéo

**VLC :**
- Ajustez avec `K` / `J` pendant la lecture
- Ou `Outils` → `Synchronisation de piste`

**Permanent (fichier défectueux) :**
- Utilisez Handbrake pour ré-encoder

### Pas de son

**Vérifications :**
1. Volume système non muet
2. Bonne sortie audio sélectionnée (Paramètres → Son)
3. Dans VLC : `Audio` → `Périphérique audio` → essayez différentes sorties
4. Redémarrez PulseAudio :
```bash
pulseaudio -k
pulseaudio --start
```

### Sous-titres mal encodés (caractères bizarres)

**Dans VLC :**
- `Sous-titres` → `Sous-piste` → `Ouvrir un fichier`
- Au bas de la fenêtre, changez **Encodage** : essayez UTF-8, Windows-1252, ISO-8859-1

### VLC ne lit pas les DVD commerciaux

**Installez libdvdcss :**
```bash
sudo apt install libdvd-pkg
sudo dpkg-reconfigure libdvd-pkg
```

### Photos RAW non reconnues

**Installez support RAW :**
```bash
sudo apt install rawtherapee darktable
```

Ou ouvrez directement avec RawTherapee/Darktable.

---

## Ressources et bibliothèques libres

### Musique libre de droits

**Sites recommandés :**
- **Free Music Archive** : freemusicarchive.org
- **Incompetech** (Kevin MacLeod) : incompetech.com
- **YouTube Audio Library** : via YouTube Studio
- **Jamendo** : jamendo.com
- **ccMixter** : ccmixter.org

### Vidéos libres de droits

- **Pexels Videos** : pexels.com/videos
- **Pixabay Videos** : pixabay.com/videos
- **Videvo** : videvo.net
- **Coverr** : coverr.co

### Images libres de droits

- **Unsplash** : unsplash.com
- **Pexels** : pexels.com
- **Pixabay** : pixabay.com
- **Wikimedia Commons** : commons.wikimedia.org

> **Important** : Vérifiez toujours la licence (CC0, CC-BY, etc.) avant utilisation commerciale.

---

## Conclusion

Linux Mint offre une expérience multimédia complète et riche, capable de rivaliser avec n'importe quel système d'exploitation. Que vous soyez un simple consommateur de médias ou un organisateur méticuleux de collections, vous trouverez tous les outils nécessaires.

**VLC** reste le couteau suisse universel pour la lecture, capable de tout lire sans configuration complexe. Pour l'organisation, **Rhythmbox**, **Clementine**, **Shotwell** et **digiKam** offrent des solutions adaptées à tous les niveaux.

**Points clés à retenir :**
- VLC lit pratiquement tout, toujours
- Organisez vos médias avec une structure claire
- Utilisez les tags et métadonnées pour faciliter la recherche
- Sauvegardez vos médias précieux (règle 3-2-1)
- Explorez Plex/Jellyfin pour un serveur multimédia personnel
- FFmpeg est votre ami pour conversions avancées

Avec ces outils, vous disposez d'un système multimédia complet, gratuit et puissant. La seule limite est la taille de votre disque dur !

**Prochaine étape** : Dans la section suivante, nous découvrirons la gravure de CD/DVD sous Linux Mint.

---

*Profitez pleinement de vos médias ! 🎬🎵📷*

⏭️ [Gravure CD/DVD (Brasero)](/13-multimedia-et-creativite/05-gravure-cd-dvd.md)
