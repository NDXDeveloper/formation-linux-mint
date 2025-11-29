🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 13.6 Capture d'écran et screencast (Flameshot, OBS)

## Introduction

La capture d'écran et l'enregistrement vidéo de l'écran (screencast) sont devenus essentiels dans de nombreuses situations : créer des tutoriels, documenter des bugs, partager des moments de jeu, réaliser des présentations vidéo ou simplement capturer une information importante.

Linux Mint offre des outils puissants et variés pour toutes ces tâches, depuis les captures d'écran simples jusqu'à l'enregistrement vidéo professionnel avec streaming en direct.

Dans ce chapitre, nous allons découvrir :

- **Les captures d'écran** : outils natifs et Flameshot
- **Le screencast** : OBS Studio, SimpleScreenRecorder
- **Les cas d'usage** : tutoriels, gaming, streaming
- **L'optimisation** : qualité, formats, performances
- **Les fonctionnalités avancées** : annotations, édition, webcam

> **Bon à savoir** : Linux dispose d'outils de capture et d'enregistrement d'écran aussi puissants que les solutions commerciales, et souvent même supérieurs.

---

## Comprendre les différents types de capture

### Capture d'écran (Screenshot)

Une **capture d'écran** est une image fixe de ce qui s'affiche sur votre écran à un instant T.

**Utilisations courantes :**
- Capturer une erreur pour demander de l'aide
- Sauvegarder une recette ou une information
- Illustrer un tutoriel
- Partager une conversation
- Documenter un processus

**Formats de sortie :**
- PNG : sans perte, idéal pour screenshots (recommandé)
- JPEG : compressé, fichier plus petit
- BMP : non compressé, volumineux

### Screencast (Enregistrement vidéo d'écran)

Un **screencast** est une vidéo enregistrant tout ce qui se passe sur votre écran, avec ou sans audio.

**Utilisations courantes :**
- Créer des tutoriels vidéo
- Enregistrer des sessions de gaming
- Documenter des bugs complexes
- Réaliser des présentations
- Former des collaborateurs
- Streaming en direct (Twitch, YouTube)

**Formats de sortie :**
- MP4 (H.264) : universel, bon compromis
- MKV : flexible, haute qualité
- WebM : optimisé web, open source
- FLV : streaming (ancien)

### GIF animé

Un **GIF animé** est une courte animation (quelques secondes) sans son.

**Utilisations :**
- Démonstrations rapides
- Partage sur réseaux sociaux
- Documentation légère
- Memes et humour

---

## Captures d'écran natives de Linux Mint

### Outil de capture intégré

Linux Mint inclut un outil de capture d'écran simple accessible par raccourcis clavier.

#### Raccourcis clavier par défaut

| Raccourci | Action |
|-----------|--------|
| `Impr écran` (Print Screen) | Capture tout l'écran |
| `Alt + Impr écran` | Capture la fenêtre active |
| `Maj + Impr écran` | Capture une zone sélectionnée |
| `Ctrl + Impr écran` | Copie dans presse-papier (au lieu de fichier) |

#### Où sont sauvegardées les captures ?

Par défaut : **~/Images/** (ou **~/Pictures/**)

Format du nom : `Capture d'écran de AAAA-MM-JJ HH-MM-SS.png`

#### Utilisation rapide

1. **Capturer tout l'écran** :
   - Appuyez sur `Impr écran`
   - Le flash indique la capture
   - Fichier sauvegardé dans ~/Images/

2. **Capturer une fenêtre** :
   - Cliquez sur la fenêtre à capturer
   - Appuyez sur `Alt + Impr écran`
   - Seule cette fenêtre est capturée (sans arrière-plan)

3. **Capturer une zone** :
   - Appuyez sur `Maj + Impr écran`
   - Cliquez-glissez pour sélectionner la zone
   - Relâchez pour capturer

4. **Copier dans le presse-papier** :
   - Ajoutez `Ctrl` à n'importe quel raccourci
   - Ex : `Ctrl + Impr écran` pour tout l'écran
   - Collez ensuite avec `Ctrl + V` dans une application

### GNOME Screenshot (outil graphique)

Un outil avec interface graphique est également disponible.

**Lancer l'outil :**
- Menu → Accessoires → **Capture d'écran**
- Ou commande : `gnome-screenshot`

**Options disponibles :**
- **Capturer tout l'écran**
- **Capturer la fenêtre actuelle**
- **Sélectionner une zone à capturer**
- **Délai** : 0-10 secondes (utile pour capturer menus déroulants)
- **Inclure le pointeur** : afficher ou non le curseur de souris
- **Appliquer un effet** : ombre, bordure

**Sauvegarder ou copier :**
- Après capture, fenêtre de prévisualisation
- Bouton **Enregistrer** : choisir nom et emplacement
- Bouton **Copier dans le presse-papier** : pour coller ailleurs

---

## Flameshot - Capture d'écran avancée

### Qu'est-ce que Flameshot ?

Flameshot est un outil de capture d'écran moderne et puissant avec des fonctionnalités d'annotation intégrées. C'est l'équivalent open source d'outils comme Greenshot ou Lightshot.

**Points forts :**
- Interface intuitive et moderne
- Annotations en temps réel
- Formes, flèches, texte, numéros
- Pixelisation (flouter zones sensibles)
- Upload automatique vers services cloud
- Très léger et rapide
- Intégration système

**Utilisations principales :**
- Captures annotées pour tutoriels
- Documentation technique
- Rapports de bugs
- Partage rapide d'informations
- Screenshots professionnels

### Installation de Flameshot

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "Flameshot"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update
sudo apt install flameshot
```

### Premier lancement de Flameshot

**Lancer Flameshot :**
- Menu → Graphisme → **Flameshot**
- Ou commande : `flameshot`

**Icône dans la barre système :**
- Flameshot s'intègre dans votre barre des tâches (system tray)
- Clic sur l'icône pour accéder aux options

### Utiliser Flameshot

#### Mode capture rapide

**Méthode 1 : Via l'icône**
- Clic sur l'icône Flameshot dans la barre
- Sélectionnez **Prendre une capture d'écran**

**Méthode 2 : Raccourci clavier** (recommandé)
- Configurez un raccourci (voir section suivante)
- Ex : `Impr écran` pour lancer Flameshot

#### Interface de capture

Quand vous lancez une capture :

1. **L'écran s'assombrit**
2. **Sélectionnez une zone** : cliquez-glissez
3. **Barre d'outils apparaît** avec les outils d'annotation

**Navigation :**
- **Flèches directionnelles** : ajuster la sélection pixel par pixel
- **Espace** : ouvrir le menu latéral
- **Échap** : annuler

#### Outils d'annotation

Une fois la zone sélectionnée, utilisez les outils :

| Outil | Icône | Utilisation | Raccourci |
|-------|-------|-------------|-----------|
| **Crayon** | Crayon | Dessiner à main levée | `P` |
| **Ligne** | Ligne | Tracer des lignes droites | `L` |
| **Rectangle** | Rectangle | Dessiner des rectangles | `R` |
| **Cercle** | Cercle | Dessiner des cercles | `C` |
| **Flèche** | Flèche | Pointer vers un élément | `A` |
| **Marqueur** | Surligneur | Surligner du texte | `M` |
| **Texte** | T | Ajouter du texte | `T` |
| **Numérotation** | 1,2,3 | Numéros pour étapes | `N` |
| **Pixelisation** | Pixels | Flouter zones sensibles | `B` |
| **Annuler** | Flèche retour | Annuler dernière action | `Ctrl + Z` |

**Personnalisation :**
- **Épaisseur** : curseur pour ajuster
- **Couleur** : palette de couleurs

#### Sauvegarder la capture

Après annotation, plusieurs options :

1. **Copier dans le presse-papier** (icône presse-papier)
   - Collez ensuite avec `Ctrl + V`

2. **Enregistrer dans un fichier** (icône disquette)
   - Choisissez nom et emplacement
   - Format PNG par défaut

3. **Upload sur Imgur** (icône upload)
   - Télécharge sur Imgur
   - Copie le lien automatiquement

4. **Ouvrir dans une application** (icône application)
   - GIMP, éditeur d'images, etc.

**Raccourcis de sauvegarde :**
- `Ctrl + S` : Enregistrer dans fichier
- `Ctrl + C` : Copier dans presse-papier
- `Enter` : Copier dans presse-papier

### Configurer Flameshot comme outil par défaut

#### Méthode 1 : Remplacer le raccourci Impr écran

**Cinnamon (Linux Mint par défaut) :**
1. Menu → **Paramètres système** → **Clavier** → **Raccourcis**
2. Onglet **Screenshots**
3. Désactivez les raccourcis existants (ou notez-les)
4. Cliquez sur **Ajouter un raccourci personnalisé**
   - Nom : `Flameshot capture`
   - Commande : `flameshot gui`
   - Raccourci : appuyez sur `Impr écran`

**Résultat :** `Impr écran` lance maintenant Flameshot

#### Méthode 2 : Lancer au démarrage

Pour avoir Flameshot toujours disponible :

1. **Applications au démarrage** :
   - Menu → **Paramètres système** → **Applications au démarrage**
2. **Ajouter** :
   - Nom : `Flameshot`
   - Commande : `flameshot`
   - Démarrage différé : 5 secondes
3. Cliquez sur **Ajouter**

**Résultat :** Flameshot démarre automatiquement et reste dans la barre système

### Configuration avancée de Flameshot

**Accéder aux paramètres :**
- Clic droit sur l'icône Flameshot → **Configuration**
- Ou : `flameshot config`

**Options principales :**

**Général :**
- **Chemin de sauvegarde** : dossier par défaut pour captures
- **Format du nom** : personnalisez le nom des fichiers
- **Copier automatiquement** : copie dans presse-papier après capture

**Interface :**
- **Couleur d'annotation par défaut**
- **Épaisseur des traits**
- **Afficher le bureau** : voir bureau ou fond noir
- **Afficher les boutons de la barre** : personnalisez les outils visibles

**Raccourcis :**
- Personnalisez tous les raccourcis clavier

### Utilisation en ligne de commande

Pour scripts ou automatisation :

**Capture plein écran :**
```bash
flameshot full -p ~/Images/
```

**Capture avec GUI :**
```bash
flameshot gui
```

**Capture et copie presse-papier :**
```bash
flameshot gui -c
```

**Capture avec délai (5 secondes) :**
```bash
flameshot gui -d 5000
```

**Capture d'une zone spécifique :**
```bash
flameshot gui -r > screenshot.png
```

---

## OBS Studio - Enregistrement et streaming professionnel

### Qu'est-ce qu'OBS Studio ?

OBS (Open Broadcaster Software) Studio est LE logiciel professionnel de référence pour l'enregistrement d'écran et le streaming en direct. Utilisé par des millions de streamers sur Twitch, YouTube et autres plateformes.

**Points forts :**
- Gratuit et open source
- Qualité professionnelle
- Streaming en direct vers toutes plateformes
- Multi-sources (écran, webcam, audio, images)
- Scènes et transitions
- Plugins et extensions
- Performances optimisées
- Encodage GPU (NVENC, AMF, QuickSync)

**Utilisations principales :**
- Streaming sur Twitch, YouTube, Facebook
- Enregistrement de gameplay
- Tutoriels vidéo professionnels
- Webinaires et présentations
- Podcasts vidéo
- Cours en ligne

### Installation d'OBS Studio

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "OBS Studio"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update
sudo apt install obs-studio
```

**Version Flatpak (plus récente) :**
```bash
flatpak install flathub com.obsproject.Studio
```

### Configuration initiale d'OBS

#### Premier lancement - Assistant de configuration

Au premier lancement, OBS propose un assistant :

1. **Optimisation automatique** : cliquez sur Oui
2. **Usage prévu** :
   - **Streaming** : si vous comptez streamer
   - **Enregistrement** : pour enregistrements locaux
   - **Les deux** : utilisations mixtes
3. **Résolution vidéo** :
   - 1920x1080 (Full HD) : recommandé
   - 1280x720 (HD) : si PC moins puissant
4. **Framerate** :
   - 30 FPS : standard, fluide
   - 60 FPS : très fluide (gaming, action)
5. **Informations de streaming** (si applicable) :
   - Sélectionnez service (Twitch, YouTube, etc.)
   - Connectez votre compte

**OBS teste ensuite votre configuration** et optimise automatiquement.

### Interface d'OBS Studio

L'interface se compose de plusieurs panneaux :

**1. Scènes (en bas à gauche) :**
- Différentes configurations que vous pouvez basculer
- Ex : Scène 1 = jeu plein écran, Scène 2 = webcam + jeu

**2. Sources (centre bas) :**
- Éléments de la scène (écran, webcam, images, texte)
- Une scène contient plusieurs sources

**3. Mixeur audio (centre) :**
- Contrôle du volume de chaque source audio
- Vu-mètres en temps réel

**4. Aperçu (centre haut) :**
- Prévisualisation de ce qui sera enregistré/streamé
- Disposition des sources

**5. Contrôles (à droite) :**
- Démarrer/arrêter enregistrement
- Démarrer/arrêter streaming
- Mode studio (prévisualisation)

### Créer votre première scène

#### Scène simple : Capture d'écran

1. **Créer une scène** :
   - Cliquez sur **+** dans le panneau Scènes
   - Nommez : "Bureau"
   - Cliquez OK

2. **Ajouter une source** :
   - Dans Sources, cliquez sur **+**
   - Sélectionnez **Capture d'écran (XSHM)**
   - Nommez : "Mon écran"
   - Cliquez OK

3. **Configuration de la source** :
   - Laissez les paramètres par défaut
   - Cliquez OK

**Votre écran apparaît maintenant dans l'aperçu !**

#### Ajuster la source dans l'aperçu

- **Redimensionner** : cliquez-glissez les coins
- **Déplacer** : cliquez-glissez au centre
- **Maintenir proportions** : maintenez `Maj` en redimensionnant
- **Centrer** : clic droit → Transformer → Centrer à l'écran

### Ajouter une webcam

1. **Ajouter une source** :
   - Sources → **+**
   - Sélectionnez **Périphérique de capture vidéo (V4L2)**
   - Nommez : "Webcam"

2. **Configuration** :
   - **Périphérique** : sélectionnez votre webcam
   - **Résolution** : 1280x720 ou 1920x1080
   - Cliquez OK

3. **Positionner la webcam** :
   - Redimensionnez et placez (généralement coin bas-droit)
   - Taille recommandée : 20-30% de l'écran

**Astuce :** Créez des scènes séparées :
- Scène 1 : Écran seul
- Scène 2 : Écran + webcam
- Scène 3 : Webcam seule (intermèdes)

### Ajouter du texte et des images

**Texte (overlay) :**
1. Sources → **+** → **Texte (FreeType 2)**
2. Nommez : "Mon nom"
3. Tapez votre texte
4. Personnalisez police, taille, couleur
5. Positionnez dans l'aperçu

**Image (logo, watermark) :**
1. Sources → **+** → **Image**
2. Parcourez et sélectionnez l'image
3. Redimensionnez et positionnez

### Configuration audio

#### Sources audio typiques

1. **Micro** :
   - Sources → **+** → **Capture audio d'entrée**
   - Sélectionnez votre micro
   - Nommez : "Micro"

2. **Audio système** :
   - Déjà configuré par défaut (Desktop Audio)
   - Capture sons du PC (jeux, musique, etc.)

#### Ajuster les niveaux

**Dans le Mixeur audio :**
- **Vert** : bon niveau (-12 dB à -6 dB)
- **Jaune** : niveau élevé
- **Rouge** : saturation (BAD - réduisez !)

**Régler le volume :**
- Glissez les faders pour ajuster
- Voix (micro) : pics autour de -12 dB à -6 dB
- Musique/jeu : -20 dB à -12 dB (en fond)

**Supprimer le bruit de fond :**
1. Clic droit sur source audio (Micro)
2. **Filtres**
3. **+** → **Suppression du bruit**
4. Ajustez le seuil

### Enregistrer votre écran

Une fois tout configuré :

1. **Vérifiez l'aperçu** : tout est comme vous voulez ?
2. **Vérifiez l'audio** : parlez, vérifiez les niveaux
3. **Démarrer l'enregistrement** :
   - Cliquez sur **Démarrer l'enregistrement**
   - Ou appuyez sur le raccourci (voir Paramètres)

**Pendant l'enregistrement :**
- Indicateur rouge "REC" en bas à droite
- Durée affichée
- Vous pouvez basculer entre scènes

**Arrêter l'enregistrement :**
- Cliquez sur **Arrêter l'enregistrement**
- Le fichier est sauvegardé automatiquement

**Où sont les enregistrements ?**
- Par défaut : **~/Vidéos/**
- Modifiable : Fichier → Paramètres → Sortie → Chemin d'enregistrement

### Paramètres d'enregistrement optimaux

**Fichier → Paramètres → Sortie :**

**Mode de sortie :** Simple (pour débutants)

**Enregistrement :**
- **Format d'enregistrement** : MP4 (ou MKV pour sécurité)
- **Encodeur** :
  - **NVENC H.264** : si carte NVIDIA (recommandé)
  - **AMD AMF H.264** : si carte AMD
  - **x264** : CPU (si pas de GPU compatible)
- **Qualité** : Haute (ou Indiscernable pour max qualité)

**Audio :**
- **Débit audio** : 192 kbps (ou 320 kbps pour max qualité)

**Sortie → Avancé (pour plus de contrôle) :**
- **Débit** :
  - 1080p 30fps : 6000-8000 kbps
  - 1080p 60fps : 8000-12000 kbps
  - 720p 30fps : 3000-5000 kbps

### Streaming en direct

#### Configuration du service de streaming

1. **Fichier → Paramètres → Stream**
2. **Service** : sélectionnez (Twitch, YouTube, Facebook, etc.)
3. **Connectez votre compte** :
   - Cliquez sur "Connecter le compte"
   - Autorisez OBS

**Ou manuellement :**
- **Serveur** : sélectionnez le plus proche
- **Clé de stream** : copiez depuis votre tableau de bord Twitch/YouTube

#### Lancer le stream

1. Vérifiez votre scène et audio
2. Cliquez sur **Démarrer le streaming**
3. Vous êtes en direct !

**Surveillez :**
- **Indicateur vert** : connexion stable
- **Indicateur rouge/jaune** : problèmes réseau
- **Frames perdues** : réduisez qualité si trop élevé

#### Paramètres de streaming recommandés

**Pour Twitch/YouTube (1080p 60fps) :**
- **Résolution** : 1920x1080
- **FPS** : 60
- **Débit** : 6000 kbps (Twitch max, vérifiez limites de votre plateforme)
- **Encodeur** : NVENC H.264 (si disponible)
- **Preset** : Quality

**Pour connexion Internet limitée (720p 30fps) :**
- **Résolution** : 1280x720
- **FPS** : 30
- **Débit** : 3000 kbps

### Fonctionnalités avancées

#### Scènes et transitions

**Créer plusieurs scènes :**
- Scène "Intro" : image d'introduction
- Scène "Jeu" : capture de jeu + webcam
- Scène "Pause" : écran "De retour bientôt"
- Scène "Fin" : écran de fin + remerciements

**Transitions entre scènes :**
1. Paramètres → **Scène**
2. **Transition** : Fondu, Balayage, etc.
3. **Durée** : 300 ms (rapide) à 1000 ms (lent)

**Basculer entre scènes :**
- Cliquez sur la scène dans le panneau Scènes
- Ou configurez des raccourcis clavier

#### Mode Studio

Active une prévisualisation avant diffusion :
- **Contrôles → Mode Studio**
- Colonne gauche : aperçu (ce qui sera diffusé)
- Colonne droite : prévisualisation (préparation)
- Bouton **Transition** pour basculer

**Utile pour :**
- Préparer la scène suivante
- Éviter erreurs en direct
- Transitions professionnelles

#### Filtres vidéo

Améliorez vos sources avec des filtres :

**Sur une webcam :**
1. Clic droit sur source webcam → **Filtres**
2. **+** (Effets vidéo) :
   - **Correction colorimétrique** : ajuster teinte/saturation
   - **LUT** : appliquer des profils colorimétriques
   - **Netteté** : améliorer netteté
   - **Recadrage** : enlever bords webcam

**Chroma Key (fond vert) :**
1. Filtres → **+** → **Chroma Key**
2. Ajustez la couleur à supprimer (vert standard)
3. Affinez avec les curseurs

### Plugins et extensions

OBS supporte de nombreux plugins :

**Installation de plugins :**
```bash
# Exemple : plugin de replay buffer
sudo apt install obs-studio-plugin-*
```

**Plugins populaires :**
- **obs-websocket** : contrôle à distance
- **obs-streamfx** : effets vidéo avancés
- **obs-move-transition** : transitions animées
- **obs-virtual-cam** : webcam virtuelle (utiliser OBS comme webcam)

**Installer depuis GitHub :**
- Téléchargez le plugin
- Placez dans `~/.config/obs-studio/plugins/`
- Relancez OBS

---

## SimpleScreenRecorder - Alternative simple

### Qu'est-ce que SimpleScreenRecorder ?

SimpleScreenRecorder (SSR) est un enregistreur d'écran léger, simple d'utilisation mais puissant.

**Points forts :**
- Interface très simple
- Excellent pour débutants
- Performances optimales
- Preview en direct
- Moins de ressources qu'OBS
- Idéal pour tutoriels simples

**Installation :**
```bash
sudo apt install simplescreenrecorder
```

### Utiliser SimpleScreenRecorder

#### Configuration rapide

1. **Lancez SimpleScreenRecorder**
2. **Bienvenue** : cliquez Continuer
3. **Entrée** :
   - **Enregistrer tout l'écran** (ou fenêtre/zone)
   - **Résolution** : Native ou réduite
   - **Frame rate** : 30 fps
4. **Audio** :
   - **Enregistrer l'audio** : cochez
   - **Backend** : PulseAudio
   - **Source** : Moniteur (pour audio système) + Micro
5. **Sortie** :
   - **Fichier** : choisissez nom et emplacement
   - **Conteneur** : MP4 (ou MKV)
   - **Codec vidéo** : H.264
   - **Débit** : 5000 kbps (ajustez selon qualité)
6. **Continuer** → **Démarrer l'enregistrement**

#### Pendant l'enregistrement

- **Fenêtre de contrôle** reste ouverte
- **Aperçu** en direct
- **Statistiques** : FPS, débit, taille fichier
- **Pause** : bouton Pause
- **Arrêt** : bouton Stop

**Raccourci :** Par défaut `Ctrl + R` pour démarrer/arrêter

### Quand choisir SimpleScreenRecorder ?

**Utilisez SSR si :**
- ✅ Vous voulez un outil simple et rapide
- ✅ Enregistrements simples (pas de multi-sources)
- ✅ Tutoriels basiques
- ✅ PC peu puissant (SSR est plus léger)
- ✅ Pas besoin de streaming

**Utilisez OBS si :**
- ❌ Streaming en direct
- ❌ Multi-sources (webcam + écran + overlays)
- ❌ Scènes et transitions
- ❌ Production professionnelle

---

## Kazam - Encore plus simple

### Qu'est-ce que Kazam ?

Kazam est un enregistreur d'écran ultra-simple, minimaliste.

**Installation :**
```bash
sudo apt install kazam
```

### Utiliser Kazam

1. Lancez **Kazam**
2. Fenêtre ultra-simple :
   - **Screencast** : enregistrement vidéo
   - **Screenshot** : capture d'écran
3. Cliquez sur **Screencast**
4. Options :
   - **Fullscreen** : tout l'écran
   - **Window** : une fenêtre
   - **Area** : zone spécifique
5. **Capture** : démarre immédiatement

**Arrêter :** Icône Kazam dans barre système → Stop

**Fichier sauvegardé :** ~/Vidéos/

**Idéal pour :** Enregistrements ultra-rapides sans configuration.

---

## Créer des GIFs animés

### Avec Peek

Peek est un outil spécialisé dans la création de GIFs animés.

**Installation :**
```bash
sudo apt install peek
```

**Utilisation :**
1. Lancez **Peek**
2. Fenêtre de sélection apparaît
3. Redimensionnez pour couvrir la zone à enregistrer
4. Cliquez sur le **bouton rouge** (Enregistrer)
5. Faites votre démonstration
6. Cliquez sur **Stop**
7. **Enregistrer sous** : choisissez format (GIF, MP4, WebM)

**Paramètres :**
- **FPS** : 10-15 fps pour GIF (moins = fichier plus petit)
- **Résolution** : réduite pour GIF léger
- **Délai** : ajouter délai au début

**Astuces GIF :**
- Gardez-le court (2-10 secondes)
- Réduisez la résolution (800px de large max)
- Moins de couleurs = fichier plus petit
- Utilisez WebM si GIF trop lourd

### Convertir vidéo en GIF avec FFmpeg

```bash
ffmpeg -i video.mp4 -vf "fps=10,scale=640:-1" -loop 0 output.gif
```

**Optimiser le GIF :**
```bash
ffmpeg -i video.mp4 -vf "fps=10,scale=640:-1,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif
```

---

## Cas d'usage et configurations

### Pour tutoriels informatiques

**Configuration OBS recommandée :**
- **Scène 1** : Écran complet
- **Scène 2** : Écran + webcam (coin) + texte (nom/titre)
- **Audio** : Micro voix claire (traité avec suppression bruit)
- **Résolution** : 1920x1080 30fps
- **Encodeur** : x264 ou NVENC
- **Débit** : 6000-8000 kbps

**Workflow :**
1. Préparez script/plan
2. OBS : démarrez enregistrement
3. Parlez clairement et lentement
4. Utilisez Flameshot pour captures annotées (incorporez dans montage après)
5. Éditez avec Kdenlive/OpenShot si nécessaire

### Pour gaming

**Configuration OBS gaming :**
- **Scène** : Capture de jeu + webcam + overlay (nom, réseau social)
- **Audio** : Jeu + micro + musique (fond très bas)
- **Résolution** : 1920x1080 60fps (ou 720p 60fps si PC limité)
- **Encodeur** : NVENC H.264 (GPU) pour meilleures performances
- **Débit** : 8000-12000 kbps pour 1080p 60fps

**Source de jeu :**
- **Capture de jeu** : pour jeux plein écran
- **Capture de fenêtre** : pour jeux en fenêtré

**Optimisation performances :**
- Encodeur GPU (NVENC/AMF) au lieu de x264
- Réduire résolution/FPS si lag
- Fermer applications en arrière-plan
- Process Priority : High (Paramètres → Avancé)

### Pour streaming Twitch/YouTube

**Configuration Twitch (1080p 60fps) :**
- **Résolution de sortie** : 1920x1080
- **FPS** : 60
- **Encodeur** : NVENC H.264
- **Débit vidéo** : 6000 kbps (max Twitch)
- **Preset** : Quality
- **Débit audio** : 160 kbps
- **Intervalle image clé** : 2

**Scènes typiques streamer :**
- **Starting Soon** : écran d'attente avant stream
- **Jeu + Webcam** : scène principale
- **Just Chatting** : webcam plein écran
- **BRB** : "De retour bientôt"
- **Ending** : écran de fin

**Overlays et alerts :**
- Utilisez StreamElements ou Streamlabs pour alerts
- Import via Sources → Navigateur

### Pour webinaires et présentations

**Configuration webinaire :**
- **Scène 1** : Diaporama (capture fenêtre PowerPoint/Impress)
- **Scène 2** : Diaporama + webcam (présentateur)
- **Scène 3** : Démonstration (capture écran)
- **Audio** : Micro de qualité (casque/micro cravate)

**Résolution :** 1920x1080 30fps suffit

**Plateforme :** Zoom, Google Meet, ou streaming YouTube Live

**Astuce :** Utilisez **OBS Virtual Camera** :
1. OBS : Outils → VirtualCam → Démarrer
2. Dans Zoom/Meet : sélectionnez "OBS Virtual Camera" comme webcam
3. Votre scène OBS devient votre "webcam" avec overlays, multi-sources, etc.

---

## Optimisation et performances

### Réduire l'utilisation CPU/GPU

**Si OBS lag ou ralentit le PC :**

1. **Utilisez encodeur GPU** :
   - NVENC (NVIDIA) ou AMF (AMD) au lieu de x264
   - Paramètres → Sortie → Encodeur

2. **Réduisez résolution/FPS** :
   - 720p au lieu de 1080p
   - 30 fps au lieu de 60 fps

3. **Limitez les sources** :
   - Moins de sources = meilleures performances
   - Désactivez sources inutilisées

4. **Mode Game** (pour gaming) :
   - Paramètres → Avancé → Process Priority : High

5. **Fermez applications** :
   - Navigateurs, Discord, etc.

### Qualité vs taille de fichier

**Enregistrement local (fichier volumineux OK) :**
- Débit élevé : 15000-20000 kbps
- Format : MKV (plus sûr que MP4)
- Qualité : Indiscernable

**Streaming (débit limité) :**
- Respectez limites plateforme (Twitch : 6000 kbps max)
- Équilibrez qualité/fluidité

**Compromis qualité/taille :**
- **x264** : meilleure qualité, plus lent
- **NVENC/AMF** : qualité légèrement inférieure, très rapide
- **Preset** : Plus lent = meilleure qualité

### Format MKV vs MP4

**MKV** (recommandé pour enregistrement) :
- ✅ Récupérable si crash
- ✅ Pas de corruption si arrêt brutal
- ❌ Moins universel

**MP4** :
- ✅ Universel, compatible partout
- ❌ Corrompu si arrêt brutal
- ❌ Perdu si OBS crash

**Workflow recommandé :**
1. Enregistrez en **MKV**
2. Remuxer en MP4 après : Fichier → Remux des enregistrements

---

## Dépannage

### OBS : Écran noir lors de la capture

**Problème :** Capture d'écran affiche un écran noir.

**Solution :**
1. Supprimez la source "Capture d'écran (XSHM)"
2. Ajoutez **Capture d'écran (PipeWire)**
3. Si PipeWire pas disponible :
```bash
sudo apt install xdg-desktop-portal xdg-desktop-portal-gtk
```
4. Redémarrez

### OBS : Pas de son enregistré

**Vérifications :**
1. Paramètres → Audio → Périphérique Desktop Audio : sélectionné ?
2. Mixeur audio : volume pas à zéro ? Pas muet ?
3. Testez une autre source audio
4. Vérifiez PulseAudio/PipeWire fonctionne

**Solution PulseAudio :**
```bash
pulseaudio -k
pulseaudio --start
```

### Flameshot ne se lance pas

**Solution :**
1. Vérifiez installation :
```bash
which flameshot
```
2. Lancez depuis terminal pour voir erreurs :
```bash
flameshot gui
```
3. Réinstallez :
```bash
sudo apt remove flameshot
sudo apt install flameshot
```

### Enregistrement saccadé

**Causes et solutions :**

1. **CPU/GPU surchargé** :
   - Réduisez résolution (720p)
   - Réduisez FPS (30 au lieu de 60)
   - Utilisez encodeur GPU

2. **Disque dur lent** :
   - Enregistrez sur SSD si possible
   - Réduisez le débit

3. **Trop de sources** :
   - Simplifiez la scène
   - Désactivez sources inutilisées

4. **Applications en fond** :
   - Fermez navigateur, Discord, etc.

### SimpleScreenRecorder : décalage audio/vidéo

**Solution :**
1. Paramètres audio → Backend : essayez ALSA au lieu de PulseAudio
2. Ou inversement
3. Réglez "Audio offset" pour corriger décalage

---

## Conseils pour de bonnes captures

### Captures d'écran

**Pour documentation/tutoriels :**
- Nettoyez votre bureau avant capture
- Fermez onglets/fenêtres inutiles
- Utilisez Flameshot pour annoter
- Numérotez les étapes
- Pixelisez informations sensibles (email, nom, etc.)

**Format :**
- PNG pour screenshots (pas de perte)
- JPEG uniquement si taille fichier critique

### Screencast

**Avant l'enregistrement :**
- Fermez notifications (Mode Ne pas déranger)
- Préparez script ou plan
- Testez audio (enregistrez 10s, vérifiez)
- Nettoyez bureau/navigateur

**Pendant l'enregistrement :**
- Parlez clairement et posément
- Laissez quelques secondes en début/fin (pour montage)
- Si erreur : marquez-la verbalement, continuez (coupez au montage)

**Audio :**
- Micro proche de la bouche (10-15 cm)
- Pièce silencieuse
- Fermez fenêtres (bruit extérieur)
- Désactivez ventilateurs/climatisation si possible

**Visuel :**
- Zoom sur zones importantes
- Déplacez souris lentement
- Utilisez curseur de souris visible
- Évitez mouvements brusques

### Streaming

**Checklist pré-stream :**
- ✅ Testez scène et transitions
- ✅ Vérifiez audio (parlez, testez niveaux)
- ✅ Testez connexion Internet (speedtest)
- ✅ Scène "Starting Soon" prête
- ✅ Désactivez notifications
- ✅ Hydratation à portée de main

**Pendant le stream :**
- Interagissez avec le chat
- Surveillez les indicateurs (connexion, frames perdues)
- Ayez des scènes de backup ("BRB", "Technical Difficulties")

---

## Ressources et outils complémentaires

### Montage post-enregistrement

Après enregistrement, éditez avec :
- **Kdenlive** : montage professionnel
- **OpenShot** : simple et accessible
- **Shotcut** : alternative

### Compresser/convertir vidéos

**Handbrake :**
- Compresser vidéos volumineuses
- Convertir formats
- Optimiser pour web

### Musique libre pour vidéos

- YouTube Audio Library
- Incompetech (Kevin MacLeod)
- Bensound
- Epidemic Sound (payant)

### Overlays et assets

- **Nerd or Die** : overlays gratuits/payants
- **Own3d.tv** : themes stream
- **StreamElements** : overlays et alerts
- **Canva** : créer vos propres overlays

### Communautés

- Reddit : r/obs, r/Twitch, r/letsplay
- Forums OBS : forum.obsproject.com
- Discord OBS : serveur officiel

---

## Conclusion

Linux Mint offre une panoplie complète d'outils pour la capture d'écran et l'enregistrement vidéo, du simple screenshot à la production vidéo professionnelle avec streaming en direct.

**Flameshot** est parfait pour les captures d'écran annotées rapides, idéal pour documentation et tutoriels écrits.

**OBS Studio** est l'outil de référence professionnel pour enregistrement et streaming, utilisé par des millions de créateurs de contenu dans le monde entier. Sa puissance et sa flexibilité en font le choix numéro un pour tout projet sérieux.

**SimpleScreenRecorder** et **Kazam** offrent des alternatives plus simples pour enregistrements rapides sans configuration complexe.

**Points clés à retenir :**
- Flameshot pour screenshots avec annotations
- OBS Studio pour enregistrements professionnels et streaming
- SimpleScreenRecorder pour enregistrements simples et rapides
- Peek pour GIFs animés
- Optimisez selon votre matériel (encodeur GPU si disponible)
- Testez toujours audio avant enregistrement important

Avec ces outils, vous êtes équipé pour créer tutoriels, streams, vidéos gaming ou toute autre production vidéo de qualité professionnelle, le tout avec des logiciels gratuits et open source.

**Prochaine étape** : Dans la section suivante, nous découvrirons la gestion de photos sous Linux Mint avec Shotwell et digiKam.

---

*Bonnes captures et bons enregistrements ! 🎥📸*

⏭️ [Gestion de photos (Shotwell, digiKam)](/13-multimedia-et-creativite/07-gestion-de-photos.md)
