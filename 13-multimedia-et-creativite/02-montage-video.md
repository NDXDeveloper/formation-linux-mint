🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 13.2 Montage vidéo (Kdenlive, OpenShot, DaVinci Resolve)

## Introduction

Le montage vidéo sous Linux Mint est devenu une réalité professionnelle grâce à des logiciels puissants et gratuits. Que vous souhaitiez créer des vlogs pour YouTube, monter vos vidéos de famille ou réaliser des projets professionnels, Linux propose des outils adaptés à tous les niveaux.

Dans ce chapitre, nous allons explorer les trois principaux logiciels de montage vidéo disponibles sous Linux Mint :

- **Kdenlive** : complet et professionnel, le meilleur compromis
- **OpenShot** : simple et intuitif, idéal pour débuter
- **DaVinci Resolve** : professionnel hollywoodien, très puissant mais exigeant

> **Bon à savoir** : Ces logiciels peuvent gérer des projets de qualité professionnelle, du simple vlog aux documentaires diffusés en télévision.

---

## Concepts de base du montage vidéo

Avant de plonger dans les logiciels, comprenons quelques notions essentielles :

### La timeline (ligne de temps)

C'est la zone principale où vous assemblez vos clips vidéo, audio et effets dans l'ordre chronologique. Imaginez-la comme une partition musicale où chaque élément a sa place dans le temps.

### Les pistes (tracks)

La timeline est composée de plusieurs pistes superposées :
- **Pistes vidéo** : contiennent vos clips vidéo
- **Pistes audio** : contiennent musiques, voix, effets sonores
- Les pistes du haut s'affichent par-dessus celles du bas

### Les formats vidéo courants

- **MP4** : format universel, excellent compromis qualité/taille
- **MOV** : format Apple, haute qualité
- **AVI** : ancien format, volumineux
- **MKV** : conteneur flexible, bonne qualité
- **WebM** : optimisé pour le web

### Résolution et framerate

- **Résolution** : qualité de l'image (1080p, 4K, etc.)
  - 720p HD : 1280x720
  - 1080p Full HD : 1920x1080
  - 4K UHD : 3840x2160

- **Framerate (images par seconde)** :
  - 24 fps : cinéma
  - 25 fps : vidéo PAL (Europe)
  - 30 fps : vidéo NTSC (Amérique)
  - 60 fps : vidéos fluides (gaming, sport)

> **Conseil débutant** : Pour débuter, privilégiez le 1080p à 30 fps, c'est largement suffisant pour YouTube et les réseaux sociaux.

---

## Kdenlive - Le montage professionnel accessible

### Qu'est-ce que Kdenlive ?

Kdenlive (KDE Non-Linear Video Editor) est le logiciel de montage vidéo le plus populaire et complet sous Linux. Il offre un excellent équilibre entre puissance professionnelle et accessibilité pour les débutants.

**Points forts :**
- Interface personnalisable et moderne
- Nombreux effets vidéo et audio
- Stabilité et performances
- Support multi-pistes
- Proxy clips pour ordinateurs moins puissants
- Rendu rapide
- Communauté active

**Utilisations principales :**
- Vlogs et vidéos YouTube
- Vidéos promotionnelles
- Courts-métrages
- Tutoriels et formations
- Montages de mariage et événements

### Installation de Kdenlive

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "Kdenlive"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update  
sudo apt install kdenlive  
```

**Version Flatpak (plus récente) :**
```bash
flatpak install flathub org.kde.kdenlive
```

> **Astuce** : La version Flatpak est souvent plus récente et peut offrir de meilleures performances sur certains systèmes.

### Découverte de l'interface Kdenlive

Au premier lancement, l'interface se compose de quatre zones principales :

1. **Moniteurs de projet** (en haut) :
   - **Moniteur source** (gauche) : prévisualisation des clips
   - **Moniteur projet** (droite) : aperçu du montage final

2. **Chutier de projet** (en haut à gauche) :
   - Bibliothèque de tous vos médias (vidéos, images, audio)
   - Organisez avec des dossiers

3. **Timeline** (en bas) :
   - Zone de montage principale
   - Plusieurs pistes vidéo et audio superposées

4. **Panneau d'effets** (à gauche) :
   - Liste des transitions, effets vidéo et audio

### Créer votre premier projet Kdenlive

#### 1. Nouveau projet

- `Projet` → `Nouveau`
- Choisissez :
  - **Nom du projet**
  - **Dossier de travail** (où seront les fichiers)
  - **Profil vidéo** (1080p 30fps recommandé pour débuter)

#### 2. Importer vos médias

**Plusieurs méthodes :**
- Glissez-déposez vos fichiers dans le chutier
- `Projet` → `Ajouter un clip ou un dossier`
- Raccourci : `Ctrl + I`

**Types de médias acceptés :**
- Vidéos (MP4, MOV, AVI, MKV, etc.)
- Images (JPG, PNG, etc.)
- Audio (MP3, WAV, FLAC, etc.)

#### 3. Monter vos clips sur la timeline

**Ajouter un clip :**
- Glissez-déposez depuis le chutier vers la timeline
- Ou cliquez-droit sur un clip → `Insérer dans la timeline`

**Organiser vos clips :**
- **Déplacer** : cliquez-glissez le clip
- **Découper** : placez le curseur, puis `Maj + R` (razor tool)
- **Supprimer** : sélectionnez et appuyez sur `Suppr`
- **Séparer audio/vidéo** : clic droit → `Séparer l'audio`

#### 4. Découper et ajuster les clips

**Rogner un clip (enlever début/fin) :**
- Survolez le bord du clip jusqu'à voir la flèche double
- Cliquez-glissez pour raccourcir

**Couper au milieu :**
- Placez le curseur de lecture où couper
- Appuyez sur `Maj + R` (outil Cutter)
- Supprimez la partie non désirée

**Zoom sur la timeline :**
- `Ctrl + molette` : zoomer/dézoomer
- Utile pour des découpes précises

#### 5. Ajouter des transitions

**Transition entre deux clips :**
- Placez deux clips côte à côte sur la timeline
- Superposez légèrement leurs extrémités
- Glissez-déposez une transition depuis le panneau "Transitions"

**Transitions populaires :**
- **Fondu** : transition douce classique
- **Fondu au noir** : transition via écran noir
- **Balayage** : essuie d'un côté
- **Zoom** : effet de zoom

#### 6. Ajouter du texte et des titres

- `Projet` → `Ajouter un clip titre`
- Ou cliquez sur l'icône **T** dans la barre d'outils
- Tapez votre texte
- Personnalisez police, couleur, position, taille
- Glissez le titre sur une piste vidéo au-dessus de votre vidéo

**Types de titres :**
- Titre simple : texte statique
- Titre avec animation : texte qui bouge
- Générique : texte qui défile

#### 7. Appliquer des effets vidéo

- Sélectionnez un clip sur la timeline
- Dans le panneau "Effets vidéo", glissez un effet sur le clip
- Ajustez les paramètres dans l'onglet "Propriétés"

**Effets utiles pour débuter :**
- **Correction des couleurs** : améliorer luminosité/contraste
- **Recadrage** : zoomer sur une partie
- **Stabilisation** : réduire les tremblements
- **Flou** : flouter une zone (masquer visage, plaque)
- **Vitesse** : ralenti ou accéléré

#### 8. Travailler avec l'audio

**Ajouter une musique de fond :**
- Importez votre fichier audio dans le chutier
- Glissez-le sur une piste audio (en dessous des pistes vidéo)

**Ajuster le volume :**
- Survolez la ligne horizontale sur le clip audio
- Cliquez-glissez vers le bas pour baisser le volume
- Ou utilisez l'effet "Volume"

**Faire un fondu audio :**
- Survolez le coin du clip audio
- Un petit rectangle vert apparaît
- Cliquez-glissez pour créer le fondu

**Couper le son d'une vidéo :**
- Clic droit sur le clip vidéo
- `Séparer l'audio`
- Supprimez la piste audio

#### 9. Utiliser les marqueurs

Les marqueurs vous aident à repérer des moments importants :
- Positionnez le curseur
- Appuyez sur `*` (pavé numérique)
- Nommez votre marqueur
- Navigation rapide vers vos marqueurs

#### 10. Exporter votre vidéo finale

**Rendu du projet :**
- `Projet` → `Rendre` (ou `Ctrl + Entrée`)
- Choisissez un profil de rendu :
  - **MP4 (h264)** : recommandé pour YouTube, polyvalent
  - **WebM** : pour le web
  - **MP4 haute qualité** : pour archivage

**Paramètres importants :**
- **Nom du fichier** et destination
- **Résolution** : gardez celle du projet
- **Bitrate** : plus élevé = meilleure qualité mais fichier plus lourd
  - YouTube 1080p : 8000-12000 kbps recommandé
- **Audio** : AAC, 192 kbps ou 256 kbps

**Lancer le rendu :**
- Cliquez sur "Rendre dans un fichier"
- Patientez (peut prendre du temps selon durée et puissance PC)

### Fonctionnalités avancées de Kdenlive

#### Clips proxy (pour ordinateurs lents)

Si votre ordinateur rame avec des vidéos 4K :
- `Paramètres` → `Configurer Kdenlive` → `Proxy`
- Activez la génération automatique de proxies
- Kdenlive créera des versions basse résolution pour le montage
- Le rendu final utilisera les fichiers originaux

#### Keyframes (images-clés)

Permettent d'animer des effets dans le temps :
- Sélectionnez un effet sur un clip
- Activez les keyframes (icône horloge)
- Créez des points à différents moments
- Variez les valeurs entre ces points

**Exemple** : Faire un zoom progressif
- Effet "Transform" avec keyframes
- Position 0s : échelle 100%
- Position 5s : échelle 150%
- La vidéo zoomera progressivement

#### Multicam (plusieurs angles)

Pour monter des vidéos avec plusieurs caméras :
- Importez tous vos angles
- Synchronisez-les (audio, marqueurs)
- `Timeline` → `Insérer un clip multi-caméra`
- Basculez entre les angles en temps réel

### Astuces et raccourcis Kdenlive

| Raccourci | Action |
|-----------|--------|
| `Espace` | Lecture/Pause |
| `I` | Point d'entrée |
| `O` | Point de sortie |
| `Maj + R` | Couper le clip |
| `Ctrl + Z` | Annuler |
| `Ctrl + S` | Sauvegarder |
| `J` / `L` | Reculer/Avancer image par image |
| `+` / `-` | Zoom timeline |

---

## OpenShot - Simplicité et intuitivité

### Qu'est-ce qu'OpenShot ?

OpenShot est conçu pour être le logiciel de montage le plus simple et accessible sous Linux. Si Kdenlive vous semble intimidant, OpenShot est fait pour vous.

**Points forts :**
- Interface ultra-intuitive
- Courbe d'apprentissage très douce
- Parfait pour débuter
- Animations 3D de titres intégrées
- Effets et transitions nombreux

**Points faibles :**
- Moins stable que Kdenlive sur gros projets
- Performances variables
- Moins de fonctionnalités avancées

**Utilisations principales :**
- Montages simples et rapides
- Vidéos familiales
- Premiers pas dans le montage
- Projets courts (moins de 10 minutes)

### Installation d'OpenShot

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "OpenShot"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update  
sudo apt install openshot-qt  
```

**Version Flatpak :**
```bash
flatpak install flathub org.openshot.OpenShot
```

### Interface d'OpenShot

L'interface d'OpenShot est volontairement épurée :

1. **Fichiers du projet** (en haut à gauche) :
   - Vos médias importés

2. **Prévisualisation** (en haut au centre) :
   - Aperçu de votre montage

3. **Propriétés** (en haut à droite) :
   - Paramètres du clip sélectionné

4. **Timeline** (en bas) :
   - Zone de montage avec pistes

5. **Panneau de transitions et effets** (en bas à gauche)

### Utiliser OpenShot

#### 1. Créer un projet

- Au lancement, OpenShot vous demande :
  - **Nom du projet**
  - **Profil vidéo** (HD 720p, Full HD 1080p, 4K, etc.)
  - **FPS** (25, 30 ou 60)

> **Conseil** : Choisissez le même profil que vos vidéos sources pour éviter les conversions.

#### 2. Importer des fichiers

**Méthodes d'importation :**
- Glissez-déposez vos fichiers dans la zone "Fichiers du projet"
- Clic droit → `Importer des fichiers`
- Menu `Fichier` → `Importer des fichiers`

#### 3. Monter sur la timeline

**Ajouter des clips :**
- Glissez vos clips depuis "Fichiers du projet" vers la timeline
- Les clips vidéo vont automatiquement sur les pistes vidéo
- Les clips audio sur les pistes audio

**Éditer les clips :**
- **Découper** : survolez le bord du clip et glissez
- **Couper** : clic droit sur clip → `Séparer le clip`
- **Supprimer** : sélectionnez et appuyez sur `Suppr`

#### 4. Transitions

OpenShot excelle dans les transitions :
- Onglet "Transitions" (en bas)
- Glissez une transition entre deux clips
- Ajustez la durée en étirant la transition

**Transitions disponibles :**
- Fondus (classiques)
- Balayages (wipes)
- Zoom
- Barres
- Et bien d'autres

#### 5. Effets visuels

- Onglet "Effets" (en bas)
- Glissez un effet sur un clip de la timeline
- Modifiez les paramètres dans le panneau "Propriétés"

**Effets populaires :**
- Luminosité et contraste
- Saturation
- Négatif
- Flou
- Chrominance (fond vert)

#### 6. Titres animés

OpenShot intègre **Blender** pour créer des titres 3D animés :
- Menu `Titre` → `Titre`
- Choisissez un modèle animé
- Personnalisez le texte
- Le titre s'ajoute automatiquement à la timeline

**Types de titres :**
- Titres simples 2D
- Titres 3D animés (rotation, zoom)
- Génériques déroulants

#### 7. Audio

**Ajuster le volume :**
- Clic droit sur clip audio → `Volume` → `Niveau`
- Ou utilisez les propriétés du clip

**Séparer audio de la vidéo :**
- Clic droit sur clip vidéo → `Séparer l'audio`
- L'audio apparaît sur une piste séparée

#### 8. Exporter la vidéo

- Menu `Fichier` → `Exporter le projet` → `Exporter la vidéo`
- Choisissez :
  - **Profil** : YouTube-HD, Web, DVD, etc.
  - **Qualité vidéo** : Faible, Moyenne, Haute, Très haute
  - **Nom et destination** du fichier

- Cliquez sur **Exporter la vidéo**
- Suivez la progression dans la barre en bas

> **Astuce** : Pour YouTube, choisissez "YouTube-HD" avec qualité "Haute".

### Quand choisir OpenShot ?

**OpenShot est idéal si :**
- ✅ Vous débutez complètement en montage
- ✅ Vous voulez un logiciel simple et rapide à prendre en main
- ✅ Vos projets sont courts (5-15 minutes)
- ✅ Vous ne cherchez pas des fonctionnalités ultra-avancées
- ✅ Vous voulez des titres 3D animés facilement

**Préférez Kdenlive si :**
- ❌ Vos projets sont longs et complexes
- ❌ Vous avez besoin de stabilité maximale
- ❌ Vous voulez plus de contrôle précis
- ❌ Vous travaillez avec beaucoup de pistes

---

## DaVinci Resolve - Le géant professionnel

### Qu'est-ce que DaVinci Resolve ?

DaVinci Resolve est un logiciel de montage vidéo professionnel utilisé à Hollywood. Il est gratuit (avec version payante Studio) et disponible sous Linux, mais plus exigeant en ressources et configuration.

**Points forts :**
- Étalonnage colorimétrique de pointe
- Niveau professionnel absolu
- Effets visuels intégrés (Fusion)
- Mix audio professionnel (Fairlight)
- Utilisé pour des films et séries
- Version gratuite très complète

**Points faibles :**
- Configuration matérielle exigeante
- Courbe d'apprentissage raide
- Installation plus complexe sous Linux
- GPU puissant recommandé
- Ne supporte pas tous les codecs vidéo en natif

**Utilisations principales :**
- Production vidéo professionnelle
- Courts-métrages et films
- Publicités et clips musicaux
- Étalonnage colorimétrique avancé
- Post-production complète

### Configuration requise pour DaVinci Resolve

**Minimum :**
- GPU avec 2 Go de VRAM minimum (NVIDIA ou AMD récent)
- 16 Go de RAM (32 Go recommandé)
- Processeur moderne (Intel i7 ou AMD Ryzen 7)
- Espace disque : 50 Go pour installation + projets

**Recommandé :**
- GPU NVIDIA avec 4-8 Go de VRAM
- 32 Go de RAM ou plus
- SSD rapide pour les projets
- Carte graphique récente pour accélération GPU

> **Important** : DaVinci Resolve est très exigeant. Si votre ordinateur a moins de 16 Go de RAM ou pas de carte graphique dédiée, préférez Kdenlive ou OpenShot.

### Installation de DaVinci Resolve

**Installation manuelle (recommandée) :**

1. **Téléchargez DaVinci Resolve** :
   - Rendez-vous sur https://www.blackmagicdesign.com/products/davinciresolve
   - Téléchargez la version Linux (gratuite)
   - Remplissez le formulaire (optionnel)

2. **Installez les dépendances** :
```bash
sudo apt update  
sudo apt install libssl1.1 ocl-icd-opencl-dev  
```

3. **Extrayez et installez** :
```bash
# Rendez le fichier exécutable
chmod +x DaVinci_Resolve_*_Linux.run

# Lancez l'installation (nécessite sudo)
sudo ./DaVinci_Resolve_*_Linux.run

# Suivez l'assistant d'installation
```

4. **Lancez Resolve** :
   - Cherchez "DaVinci Resolve" dans le menu
   - Ou tapez `davinci-resolve` dans le terminal

> **Note** : L'installation peut être délicate. Consultez les forums Linux Mint si vous rencontrez des problèmes.

### Particularités de DaVinci Resolve sous Linux

**Codecs supportés :**
DaVinci Resolve (version gratuite) ne supporte pas nativement les codecs H.264/H.265 des appareils photo/smartphones.

**Solutions :**
1. **Convertir vos vidéos** en DNxHR ou ProRes (via Handbrake ou FFmpeg)
2. **Acheter DaVinci Resolve Studio** (version payante avec tous les codecs)
3. **Utiliser des proxies**

**Exemple de conversion avec FFmpeg :**
```bash
ffmpeg -i video_source.mp4 -c:v dnxhd -profile:v dnxhr_hq -c:a pcm_s16le video_dnxhr.mov
```

### Interface de DaVinci Resolve

DaVinci Resolve est organisé en **7 pages** (modules) :

1. **Media** : importer et organiser vos médias
2. **Cut** : montage rapide et simplifié
3. **Edit** : montage avancé (timeline classique)
4. **Fusion** : effets visuels et compositions
5. **Color** : étalonnage colorimétrique
6. **Fairlight** : mixage audio professionnel
7. **Deliver** : export et rendu

Pour débuter, concentrez-vous sur **Edit**, **Color** et **Deliver**.

### Workflow de base dans DaVinci Resolve

#### 1. Créer un nouveau projet

- Lancez DaVinci Resolve
- Cliquez sur "New Project"
- Nommez votre projet
- Définissez la timeline : `Timeline` → `Timeline Settings`
  - Résolution : 1920x1080 (Full HD)
  - Frame rate : 25, 30 ou 60 fps

#### 2. Importer des médias (Page Media)

- Cliquez sur l'onglet **Media** en bas
- Naviguez dans vos dossiers (panneau de gauche)
- Glissez-déposez vos fichiers dans le "Media Pool" (centre)

#### 3. Montage (Page Edit)

- Passez à l'onglet **Edit**
- L'interface ressemble à Kdenlive/Premiere Pro :
  - Viewer (aperçu) en haut
  - Media Pool en haut à gauche
  - Timeline en bas

**Ajouter des clips :**
- Glissez depuis le Media Pool vers la timeline
- Ou double-cliquez pour prévisualiser, puis `I` (in) et `O` (out) pour marquer, puis glissez

**Outils de montage :**
- **Trim** : ajuster les bords des clips
- **Blade** (`B`) : couper un clip
- **Selection** (`A`) : sélectionner et déplacer

#### 4. Étalonnage colorimétrique (Page Color)

C'est la force de DaVinci Resolve :
- Passez à l'onglet **Color**
- Sélectionnez un clip sur la timeline
- Utilisez les roues colorimétriques (Lift/Gamma/Gain)
- Ajustez température, teinte, saturation, contraste

**LUTs (Look-Up Tables) :**
- Profils colorimétriques préréglés
- Clic droit sur clip → `3D LUT` → chargez un fichier .cube
- Donnent instantanément un look cinématographique

#### 5. Export (Page Deliver)

- Passez à l'onglet **Deliver**
- Choisissez un preset :
  - **YouTube** : H.264, qualité optimale pour le web
  - **Vimeo** : haute qualité
  - **Custom** : personnalisé

**Paramètres importants :**
- Format : MP4 ou MOV
- Codec : H.264 (si supporté) ou DNxHR
- Résolution : 1920x1080
- Frame rate : identique au projet
- Bitrate : 15000-20000 kbps pour haute qualité

- Nommez le fichier et choisissez la destination
- Cliquez sur **Add to Render Queue**
- Puis **Start Render**

### DaVinci Resolve : Pour qui ?

**Utilisez DaVinci Resolve si :**
- ✅ Vous avez un ordinateur puissant (16+ Go RAM, bon GPU)
- ✅ Vous visez une qualité professionnelle
- ✅ L'étalonnage colorimétrique est crucial pour vous
- ✅ Vous travaillez sur des projets longs et complexes
- ✅ Vous voulez apprendre un outil utilisé dans l'industrie

**Évitez si :**
- ❌ Votre ordinateur est modeste (moins de 16 Go RAM)
- ❌ Vous débutez et voulez quelque chose de simple
- ❌ Vous n'avez pas de GPU dédié
- ❌ Vous travaillez principalement avec des vidéos smartphone H.264

---

## Comparaison détaillée des trois logiciels

| Critère | Kdenlive | OpenShot | DaVinci Resolve |
|---------|----------|----------|-----------------|
| **Niveau** | Intermédiaire | Débutant | Avancé/Pro |
| **Courbe d'apprentissage** | Modérée | Facile | Difficile |
| **Stabilité** | Excellente | Moyenne | Très bonne |
| **Performances** | Bonnes | Moyennes | Excellentes (bon PC) |
| **Config minimale** | 4 Go RAM | 4 Go RAM | 16 Go RAM + GPU |
| **Effets** | Nombreux | Moyens | Professionnels |
| **Étalonnage couleur** | Basique | Basique | Exceptionnel |
| **Support codecs** | Excellent | Bon | Limité (gratuit) |
| **Export** | Rapide | Moyen | Rapide |
| **Audio** | Bon | Basique | Professionnel |
| **Titres** | Bons | Excellents (3D) | Professionnels |
| **Proxy** | Oui | Non | Oui |
| **Multicam** | Oui | Limité | Oui |
| **Communauté** | Grande | Moyenne | Très grande |
| **Utilisé pro** | Oui (petites prod) | Non | Oui (Hollywood) |

---

## Quel logiciel choisir selon vos besoins ?

### Pour débuter absolument (jamais fait de montage)
**→ OpenShot**
- Interface simple et claire
- Prise en main en 30 minutes
- Résultats rapides

### Pour des projets YouTube/Vlog réguliers
**→ Kdenlive**
- Équilibre parfait puissance/simplicité
- Stable et rapide
- Support excellent de tous les formats
- Communauté active

### Pour apprendre le montage sérieusement
**→ Kdenlive** puis **DaVinci Resolve**
- Commencez par Kdenlive pour les bases
- Passez à Resolve quand vous êtes à l'aise
- Compétences transférables vers l'industrie

### Pour des projets professionnels/cinéma
**→ DaVinci Resolve** directement
- Si vous avez le matériel nécessaire
- Étalonnage incomparable
- Standard de l'industrie

### Pour des montages rapides et simples
**→ OpenShot** ou **Kdenlive**
- OpenShot si ultra-simple suffit
- Kdenlive si vous voulez un peu plus de contrôle

---

## Autres alternatives disponibles

### Shotcut
- Similaire à Kdenlive et OpenShot
- Interface différente
- Bon compromis

**Installation :**
```bash
sudo apt install shotcut
```

### Flowblade
- Montage non-linéaire rapide
- Interface minimaliste
- Moins connu mais efficace

**Installation :**
```bash
sudo apt install flowblade
```

### Olive (en développement)
- Nouveau venu prometteur
- Encore en alpha/beta
- Interface moderne inspirée de Premiere Pro

---

## Optimiser les performances de montage

### 1. Utiliser des proxies

Les proxies sont des versions basse résolution de vos vidéos pour le montage.

**Avantages :**
- Montage fluide même sur PC modeste
- Utile pour vidéos 4K
- Le rendu final utilise les fichiers originaux

**Dans Kdenlive :**
- `Paramètres` → `Configurer Kdenlive` → `Proxy`
- Activez la génération automatique

**Dans DaVinci Resolve :**
- Clic droit sur clip → `Generate Optimized Media`

### 2. Fermer les applications inutiles

Le montage vidéo est gourmand en ressources :
- Fermez navigateur, messagerie, etc.
- Libérez de la RAM

### 3. Utiliser un SSD

- Installez vos logiciels sur SSD
- Stockez vos projets en cours sur SSD
- Archivez les projets terminés sur HDD

### 4. Optimiser la timeline

- Ne gardez que les pistes nécessaires
- Désactivez les aperçus d'effets inutilisés
- Rendez les effets complexes avant l'export final

### 5. Résolution de travail réduite

Dans les paramètres du projet, travaillez en 720p si votre vidéo finale est en 1080p, puis exportez en résolution native.

---

## Conseils pour réussir vos montages

### 1. Organisation des fichiers

Créez une structure de dossiers claire :
```
Mon_Projet_Video/
├── 00_Brut/          # Vidéos originales
├── 01_Audio/         # Musiques et sons
├── 02_Images/        # Photos et graphiques
├── 03_Projet/        # Fichier de projet (.kdenlive, .osp)
├── 04_Export/        # Vidéos finales
└── 05_Archive/       # Versions précédentes
```

### 2. Sauvegardez régulièrement

- `Ctrl + S` toutes les 10 minutes
- Faites des versions (`Fichier` → `Enregistrer sous`)
- Exemple : `Mon_Projet_v1`, `Mon_Projet_v2`, etc.

### 3. Travaillez avec des couches audio séparées

- Piste 1 : Audio de la vidéo
- Piste 2 : Musique de fond
- Piste 3 : Voix off
- Piste 4 : Effets sonores

### 4. Le rythme est crucial

- Coupez les temps morts
- Variez la longueur des plans
- Utilisez le rythme de la musique

### 5. Transitions : moins c'est mieux

- Utilisez principalement des coupes franches
- Les fondus pour changements de scène/temps
- Évitez les transitions fantaisistes (sauf effet comique)

### 6. Étalonnage basique

Même avec Kdenlive ou OpenShot, faites au minimum :
- Ajustez luminosité/contraste
- Corrigez la balance des blancs
- Augmentez légèrement la saturation

### 7. Audio de qualité = 50% du résultat

- Niveaux audio cohérents (-6 dB à -3 dB pour dialogue)
- Musique de fond à -18 dB à -12 dB
- Pas de saturation (pic rouge)
- Ajoutez des fondus au début/fin des musiques

---

## Ressources pour apprendre

### Tutoriels YouTube (français)

**Pour Kdenlive :**
- Chaînes spécialisées en montage Linux
- Tutoriels officiels Kdenlive
- Communauté francophone active

**Pour DaVinci Resolve :**
- Chaîne officielle Blackmagic Design
- Nombreux tutoriels pros français
- Formation complète disponible gratuitement

**Pour OpenShot :**
- Tutoriels débutants nombreux
- Documentation officielle traduite

### Sites et forums

- **Forum Linux Mint** : section multimédia
- **Reddit** : r/kdenlive, r/davinciresolve
- **Documentation officielle** de chaque logiciel
- **YouTube** : mine d'or de tutoriels gratuits

### Chaînes YouTube recommandées (montage en général)

- Techniques de narration visuelle
- Théorie du montage
- Étalonnage colorimétrique
- Sound design

### Musiques libres de droits

**Sites recommandés :**
- YouTube Audio Library (gratuit)
- Incompetech (Kevin MacLeod - gratuit avec attribution)
- FreePD (domaine public)
- Bensound (gratuit pour usage perso)
- Epidemic Sound (payant, très pro)

> **Attention** : Vérifiez toujours les licences. Pour YouTube, utilisez uniquement de la musique libre de droits ou créée par vous.

---

## Dépannage courant

### Problème : Kdenlive plante au lancement

**Solutions :**
1. Supprimez le fichier de configuration :
```bash
rm -rf ~/.config/kdenliverc
```
2. Réinstallez via Flatpak au lieu d'APT
3. Vérifiez les pilotes graphiques

### Problème : OpenShot lent et lag

**Solutions :**
1. Réduisez la qualité d'aperçu (icône engrenage dans le viewer)
2. Utilisez moins de pistes
3. Fermez les applications en arrière-plan
4. Convertissez vos vidéos en format plus léger avant import

### Problème : DaVinci Resolve ne démarre pas

**Solutions :**
1. Vérifiez les pilotes GPU (NVIDIA propriétaires)
2. Installez les dépendances manquantes :
```bash
sudo apt install libssl1.1
```
3. Lancez depuis le terminal pour voir les erreurs :
```bash
/opt/resolve/bin/resolve
```

### Problème : Vidéo exportée de mauvaise qualité

**Solutions :**
1. Augmentez le bitrate (15000-20000 kbps pour 1080p)
2. Vérifiez que la résolution d'export = résolution projet
3. Utilisez le codec H.264 (meilleur compromis)
4. Pour Kdenlive : profil "MP4-H264 Haute Qualité"

### Problème : Audio et vidéo désynchronisés

**Solutions :**
1. Vérifiez le framerate du projet = framerate des clips
2. Ne mélangez pas 25fps et 30fps
3. Rendez la timeline avant export final
4. Convertissez les clips problématiques avec Handbrake

---

## Formats d'export recommandés par plateforme

### YouTube
- **Format** : MP4 (H.264)
- **Résolution** : 1920x1080 (Full HD) ou 3840x2160 (4K)
- **Framerate** : 30 fps ou 60 fps
- **Bitrate vidéo** : 12-15 Mbps (1080p), 35-45 Mbps (4K)
- **Audio** : AAC, 192 kbps, stéréo

### Instagram
- **Format** : MP4
- **Résolution** : 1080x1080 (carré) ou 1080x1920 (story/reel)
- **Durée max** : 60s (feed), 90s (reel)
- **Bitrate** : 5-8 Mbps

### TikTok
- **Format** : MP4
- **Résolution** : 1080x1920 (vertical)
- **Framerate** : 30 fps
- **Durée max** : 10 minutes (mais courts = mieux)

### Facebook
- **Format** : MP4
- **Résolution** : 1920x1080
- **Bitrate** : 8-12 Mbps
- **Audio** : AAC, 128 kbps

### Archivage personnel
- **Format** : MP4 ou MKV
- **Codec** : H.264 ou H.265 (HEVC, plus compact)
- **Bitrate** : Maximum qualité (20+ Mbps)
- **Audio** : AAC ou FLAC (sans perte)

---

## Conclusion

Le montage vidéo sous Linux Mint est une réalité mature et professionnelle. Vous avez le choix entre trois excellents outils :

**OpenShot** pour la simplicité et les débuts.  
**Kdenlive** pour l'équilibre parfait et l'usage régulier.  
**DaVinci Resolve** pour le niveau professionnel absolu.  

Quel que soit votre choix, vous disposez d'outils gratuits et puissants qui rivalisent avec les solutions commerciales payantes. La seule limite est votre créativité et votre motivation à apprendre.

**Notre recommandation pour débuter :**
1. Commencez avec **OpenShot** pour vous familiariser avec les concepts
2. Passez à **Kdenlive** quand vous êtes à l'aise
3. Explorez **DaVinci Resolve** si vous visez le niveau professionnel

N'oubliez pas : le meilleur logiciel est celui que vous maîtrisez. Choisissez-en un, pratiquez régulièrement, et vous produirez rapidement des vidéos de qualité professionnelle.

**Prochaine étape** : Dans la section suivante, nous explorerons la production audio avec Audacity et Ardour pour créer et éditer vos bandes sonores.

---

*Bon montage et que vos créations brillent ! 🎬*

⏭️ [Production audio (Audacity, Ardour)](/13-multimedia-et-creativite/03-production-audio.md)
