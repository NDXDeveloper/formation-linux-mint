🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.4 Lecteurs multimédia (VLC, etc.)

## Introduction

Les lecteurs multimédia permettent de lire vos vidéos, musiques et autres contenus audio/vidéo sur votre ordinateur. Linux Mint propose plusieurs excellents lecteurs, dont le célèbre VLC Media Player, installé par défaut et capable de lire pratiquement tous les formats existants.

## Pourquoi utiliser un lecteur multimédia ?

- **Lire vos fichiers locaux** : Vidéos, musiques, films sur votre disque dur
- **Lecture de DVD et Blu-ray** : Visionner vos disques
- **Streaming** : Diffuser du contenu depuis Internet
- **Formats universels** : Compatibilité avec tous les formats audio/vidéo
- **Conversion** : Transformer vos fichiers d'un format à un autre
- **Sous-titres** : Ajouter et synchroniser des sous-titres
- **Capture** : Enregistrer votre écran ou extraire du contenu

## VLC Media Player - Le lecteur universel

VLC est le lecteur multimédia le plus populaire au monde, et pour de bonnes raisons :

### Avantages de VLC

- **Gratuit et open source** : Totalement libre
- **Lit tout** : Tous les formats audio/vidéo imaginables
- **Codecs intégrés** : Pas besoin d'installer des codecs supplémentaires
- **Léger et rapide** : Consomme peu de ressources
- **Multiplateforme** : Disponible sur Windows, macOS, Linux, Android, iOS
- **Aucune publicité** : Interface propre
- **Fonctionnalités avancées** : Streaming, conversion, enregistrement, etc.

### Formats supportés par VLC

**Vidéo** :
- MP4, AVI, MKV, MOV, WMV, FLV
- MPEG, MPG, M2V, M4V
- WebM, OGV, 3GP
- DVD, Blu-ray (avec libdvdcss)
- Et des dizaines d'autres...

**Audio** :
- MP3, AAC, FLAC, OGG
- WAV, WMA, M4A, ALAC
- APE, MPC, OPUS
- CD audio
- Et bien d'autres...

**Sous-titres** :
- SRT, SUB, SSA, ASS
- VTT, IDX, SBV
- Pratiquement tous les formats

### Lancer VLC

1. **Menu principal** → **Son et vidéo** → **Lecteur multimédia VLC**
2. Ou tapez "VLC" dans la recherche
3. Icône en forme de cône de chantier orange et blanc

## Interface de VLC

### Vue d'ensemble

**Barre de menus** (en haut) :
- Média, Lecture, Audio, Vidéo, Sous-titres, Outils, Vue, Aide

**Fenêtre de lecture** (centre) :
- Zone d'affichage de la vidéo
- Ou visualisation pour la musique

**Contrôles de lecture** (en bas) :
- Lecture/Pause, Stop, Précédent, Suivant
- Barre de progression
- Volume
- Plein écran
- Liste de lecture

### Modes d'affichage

**Interface minimale** :
- Double-cliquez sur la vidéo pour masquer les contrôles
- Passez la souris en bas pour les faire réapparaître

**Plein écran** :
- Cliquez sur l'icône **Plein écran**
- Raccourci : `F` ou `F11`
- Double-clic sur la vidéo
- `Échap` pour quitter

**Toujours au-dessus** :
- Menu **Vidéo** → **Toujours au premier plan**
- La fenêtre VLC reste visible même si vous changez d'application

## Lire des fichiers multimédia

### Ouvrir un fichier

**Méthode 1 - Depuis VLC** :
1. Menu **Média** → **Ouvrir un fichier**
2. Raccourci : `Ctrl + O`
3. Parcourez et sélectionnez votre fichier
4. Cliquez sur **Ouvrir**

**Méthode 2 - Double-clic** :
1. Ouvrez votre gestionnaire de fichiers (Nemo)
2. Naviguez vers votre vidéo/musique
3. Double-cliquez dessus
4. VLC s'ouvre et lance la lecture

**Méthode 3 - Glisser-déposer** :
1. Glissez un fichier depuis le gestionnaire de fichiers
2. Déposez-le dans la fenêtre VLC
3. La lecture démarre automatiquement

### Ouvrir plusieurs fichiers (playlist)

1. Menu **Média** → **Ouvrir plusieurs fichiers**
2. Raccourci : `Ctrl + Maj + O`
3. Cliquez sur **Ajouter** pour chaque fichier
4. Ou sélectionnez plusieurs fichiers en maintenant `Ctrl`
5. Cliquez sur **Lire**

**Alternative** : Glissez-déposez plusieurs fichiers en même temps

### Ouvrir un dossier complet

1. Menu **Média** → **Ouvrir un dossier**
2. Raccourci : `Ctrl + F`
3. Sélectionnez le dossier contenant vos médias
4. VLC ajoute tous les fichiers multimédia à la liste de lecture

**Utile pour** :
- Lire un album de musique complet
- Visionner une série de vidéos
- Lecture aléatoire de votre collection

### Lire un DVD ou CD

**Insérer le disque** :
1. Insérez votre DVD ou CD dans le lecteur
2. VLC détecte automatiquement (normalement)
3. Ou menu **Média** → **Ouvrir un disque**
4. Sélectionnez **DVD** ou **CD audio**
5. Cliquez sur **Lire**

**DVDs protégés** :
Certains DVDs commerciaux sont protégés. Pour les lire :
```bash
sudo apt install libdvd-pkg  
sudo dpkg-reconfigure libdvd-pkg  
```
Sélectionnez **Oui** pour installer libdvdcss.

## Contrôles de lecture

### Lecture de base

**Lecture/Pause** :
- Cliquez sur le bouton **Lecture/Pause**
- Raccourci : `Espace` ou `Pause`

**Stop** :
- Cliquez sur **Stop**
- Raccourci : `S`

**Suivant/Précédent** (dans une playlist) :
- Boutons **Suivant** / **Précédent**
- Raccourcis : `N` (suivant) / `P` (précédent)

### Navigation dans la vidéo

**Barre de progression** :
- Cliquez n'importe où sur la barre pour sauter à ce moment
- Glissez le curseur pour naviguer précisément

**Avance rapide / Retour** :
- **Courte** : `→` (10 sec avant) / `←` (10 sec arrière)
- **Moyenne** : `Alt + →` (1 min avant) / `Alt + ←` (1 min arrière)
- **Longue** : `Ctrl + →` (5 min avant) / `Ctrl + ←` (5 min arrière)

**Vitesse de lecture** :
- Menu **Lecture** → **Vitesse**
- Ou boutons **+** / **-** (vitesse)
- Raccourcis : `[` (plus lent) / `]` (plus rapide)
- `=` : Vitesse normale

**Utilité** :
- Cours en ligne : 1.25x ou 1.5x pour gagner du temps
- Musique : Ralentir pour apprendre un morceau

### Contrôle du volume

**Barre de volume** :
- Molette de la souris sur la barre
- Cliquez et glissez le curseur

**Raccourcis** :
- `Ctrl + ↑` : Augmenter le volume
- `Ctrl + ↓` : Diminuer le volume
- `M` : Muet (sourdine)

**Volume au-dessus de 100%** :
- VLC peut amplifier jusqu'à 200% (125% par défaut en maximum)
- Menu **Audio** → **Volume** → Augmentez au-delà de 100%
- Attention à ne pas endommager vos haut-parleurs !

### Signets (bookmarks)

Pour marquer des moments spécifiques dans une vidéo :

1. Avancez jusqu'au moment à marquer
2. Menu **Lecture** → **Signets personnalisés** → **Gérer**
3. Cliquez sur **Créer**
4. Nommez votre signet : "Scène d'action"
5. Pour y revenir : **Lecture** → **Signets personnalisés** → Sélectionnez

**Utile pour** :
- Marquer les chapitres d'un film
- Retrouver des moments précis dans un cours
- Naviguer dans de longues vidéos

## Gestion de la vidéo

### Plein écran

**Activer** :
- Double-clic sur la vidéo
- Bouton **Plein écran**
- Raccourci : `F` ou `F11`

**Quitter** :
- `Échap`
- Double-clic
- `F` ou `F11`

**Contrôles en plein écran** :
- Bougez la souris en bas → Les contrôles apparaissent
- Clic droit → Menu contextuel

### Ratio d'aspect (format d'image)

Si la vidéo est étirée ou compressée :

1. Menu **Vidéo** → **Rapport d'aspect**
2. Choisissez :
   - **Par défaut** : Détection automatique
   - **16:9** : Format moderne (TV, YouTube)
   - **4:3** : Format ancien (TV classique)
   - **1:1** : Carré
3. Ou **Ctrl + A** pour cycler entre les formats

### Recadrage (Crop)

Pour couper les bandes noires :

1. Menu **Vidéo** → **Recadrage**
2. Choisissez le format de recadrage
3. Ou `C` pour cycler entre les options

### Rotation de la vidéo

Si votre vidéo est à l'envers ou de côté :

1. Menu **Outils** → **Effets et filtres**
2. Onglet **Effets vidéo**
3. **Géométrie**
4. Cochez **Transformation**
5. Sélectionnez : Rotation de 90°, 180°, 270° ou Retournement

**Sauvegarder la rotation** :
- VLC ne modifie pas le fichier, seulement l'affichage
- Pour sauvegarder : Utilisez la conversion (voir plus loin)

### Capture d'écran

**Prendre une capture depuis une vidéo** :
1. Mettez en pause au moment souhaité
2. Menu **Vidéo** → **Prendre une capture d'écran**
3. Raccourci : `Maj + S`

**Où est sauvegardée la capture ?** :
- Par défaut : `~/Images/` ou `~/Pictures/`
- Pour changer : **Outils** → **Préférences** → **Vidéo** → **Répertoire des captures**

### Égaliseur vidéo

Pour ajuster luminosité, contraste, saturation :

1. Menu **Outils** → **Effets et filtres**
2. Onglet **Effets vidéo** → **Essentiel**
3. Ajustez :
   - **Teinte** : Couleur générale
   - **Contraste** : Différence entre clair et foncé
   - **Luminosité** : Clarté générale
   - **Saturation** : Intensité des couleurs
   - **Gamma** : Tons moyens

**Réglages avancés** :
- Onglet **Avancé** : Netteté, réduction de bruit
- Onglet **Géométrie** : Rotation, zoom, miroir

## Gestion de l'audio

### Pistes audio multiples

Certains fichiers (DVD, MKV) ont plusieurs pistes audio (langues, commentaires) :

1. Menu **Audio** → **Piste audio**
2. Sélectionnez la piste souhaitée
3. Ou raccourci : `B` pour cycler entre les pistes

### Égaliseur audio

Pour améliorer le son ou compenser de mauvais haut-parleurs :

1. Menu **Outils** → **Effets et filtres**
2. Onglet **Effets audio** → **Égaliseur**
3. Cochez **Activer**
4. Ajustez les fréquences (graves, médiums, aigus)

**Préréglages** :
- **Presets** : Rock, Pop, Classique, Jazz, etc.
- Sélectionnez et testez

### Synchronisation audio

Si le son est décalé par rapport à l'image :

1. Pendant la lecture, appuyez sur `J` (retarder le son) ou `K` (avancer le son)
2. Chaque pression ajuste de 50 ms
3. Continuez jusqu'à synchronisation parfaite

**Alternative** :
- Menu **Outils** → **Synchronisation de piste**
- Ajustez manuellement le décalage

### Spatialisation et effets

**Spatialisation (son surround virtuel)** :
1. **Effets audio** → **Spatialisation**
2. Cochez **Activer**
3. Active un effet 3D sur du son stéréo

**Compresseur dynamique** :
- Réduit l'écart entre sons faibles et forts
- Utile pour les films (dialogues vs explosions)
- **Effets audio** → **Compresseur**

**Normalisation de volume** :
- Égalise le volume entre différentes sources
- **Effets audio** → **Normaliser le volume**

## Sous-titres

### Charger des sous-titres

**Automatique** (si le fichier .srt a le même nom) :
- Placez `film.mp4` et `film.srt` dans le même dossier
- VLC charge automatiquement les sous-titres

**Manuel** :
1. Pendant la lecture : Menu **Sous-titres** → **Ajouter un fichier de sous-titres**
2. Raccourci : `Ctrl + Shift + S`
3. Parcourez et sélectionnez le fichier .srt
4. Les sous-titres apparaissent

### Pistes de sous-titres multiples

Si la vidéo contient plusieurs pistes (DVD, MKV) :

1. Menu **Sous-titres** → **Piste de sous-titres**
2. Sélectionnez la langue souhaitée
3. Ou raccourci : `V` pour cycler

### Synchronisation des sous-titres

Si les sous-titres sont en avance ou en retard :

1. Pendant la lecture, appuyez sur `H` (retarder) ou `G` (avancer)
2. Chaque pression ajuste de 50 ms
3. Ou menu **Outils** → **Synchronisation de piste**

### Personnalisation des sous-titres

**Taille, police, couleur** :
1. Menu **Outils** → **Préférences**
2. En bas : Cochez **Tous** (affichage avancé)
3. **Sous-titres / OSD** → **Rendu de texte**
4. Ajustez :
   - Police
   - Taille
   - Couleur
   - Effet (contour, ombre)

**Position** :
- Menu **Sous-titres** → **Position** : Dessus, Centre, Dessous

### Télécharger des sous-titres

**Extension VLSub** :
1. Menu **Vue** → **VLsub**
2. Un panneau s'ouvre à droite
3. Recherchez par nom de film/série
4. Téléchargez et chargez automatiquement

**Sites de sous-titres** :
- OpenSubtitles.org
- Subscene.com
- Sous-titres.eu (français)

## Liste de lecture (Playlist)

### Afficher la liste de lecture

1. Menu **Vue** → **Liste de lecture**
2. Raccourci : `Ctrl + L`
3. Un panneau s'ouvre affichant tous vos médias

### Gérer la playlist

**Ajouter des fichiers** :
- Glissez-déposez dans la liste
- Menu **Média** → **Ouvrir plusieurs fichiers** → **Ajouter**

**Réorganiser** :
- Glissez-déposez les éléments pour changer l'ordre

**Supprimer** :
- Sélectionnez → Clic droit → **Supprimer**
- Ou touche `Suppr`

**Vider la playlist** :
- Menu **Média** → **Vider la liste de lecture**

### Lecture aléatoire et répétition

**Aléatoire** (shuffle) :
- Cliquez sur le bouton **Aléatoire** (icône flèches croisées)
- Raccourci : `R`
- Lit les fichiers dans un ordre aléatoire

**Boucle** (repeat) :
- Cliquez sur le bouton **Boucle** (icône flèches circulaires)
- Raccourci : `L`
- Options : Répéter tout, Répéter un seul élément

### Enregistrer une playlist

1. Menu **Média** → **Enregistrer la liste de lecture dans un fichier**
2. Format recommandé : **M3U** ou **XSPF**
3. Nommez : `ma-playlist.m3u`
4. Enregistrez

**Ouvrir une playlist** :
- Double-cliquez sur le fichier `.m3u` ou `.xspf`
- Ou **Média** → **Ouvrir un fichier** et sélectionnez la playlist

## Streaming et réseau

### Lire un flux réseau (stream)

VLC peut lire du contenu depuis Internet :

1. Menu **Média** → **Ouvrir un flux réseau**
2. Raccourci : `Ctrl + N`
3. Collez l'URL du flux :
   - Exemple : `http://exemple.com/stream.m3u8`
   - Flux radio, webcams, chaînes IPTV
4. Cliquez sur **Lire**

**Formats supportés** :
- HTTP, HTTPS, FTP
- MMS, RTSP, RTP
- UDP multicast
- HLS (.m3u8)
- DASH

### Convertir/Enregistrer un flux

**Enregistrer un stream** :
1. **Média** → **Ouvrir un flux réseau**
2. Collez l'URL
3. Cliquez sur la flèche à côté de **Lire** → **Convertir**
4. Choisissez le profil (format de sortie)
5. Fichier de destination
6. Cliquez sur **Démarrer**

**Attention** : Assurez-vous d'en avoir le droit légal !

### Diffuser (caster) vers un autre appareil

VLC peut diffuser votre média vers d'autres appareils :

1. **Média** → **Diffuser**
2. Ajoutez vos fichiers
3. Cliquez sur **Diffuser**
4. Choisissez la méthode : HTTP, RTP, UDP
5. Configurez (port, transcodage)
6. Démarrez

**Utilité** :
- Diffuser vers une TV compatible
- Partager sur le réseau local
- Serveur de streaming personnel

## Conversion de fichiers

VLC peut convertir vos vidéos et audios d'un format à un autre.

### Convertir un fichier

1. Menu **Média** → **Convertir / Enregistrer**
2. Raccourci : `Ctrl + R`
3. Cliquez sur **Ajouter** et sélectionnez votre fichier
4. Cliquez sur **Convertir / Enregistrer** (en bas)
5. **Profil** : Choisissez le format de sortie
   - **Video - H.264 + MP3 (MP4)** : Universel, compatible
   - **Audio - MP3** : Pour extraire l'audio
   - **Video - H.265 + AAC (MP4)** : Meilleure compression
6. **Fichier de destination** : Cliquez sur **Parcourir** et nommez votre fichier
7. Cliquez sur **Démarrer**

### Profils de conversion courants

**Pour smartphone/tablette** :
- Video - H.264 + MP3 (MP4)
- Résolution : 720p

**Pour économiser de l'espace** :
- Video - H.265 + AAC (MP4)
- Meilleure compression mais plus lent

**Extraire l'audio d'une vidéo** :
- Audio - MP3
- Audio - FLAC (sans perte)

**Pour DVD** :
- Video - H.264 + MP3 (TS)

### Personnaliser un profil de conversion

1. Dans l'écran de conversion, cliquez sur l'icône **clé à molette** à côté de Profil
2. Créez un nouveau profil ou modifiez-en un
3. Ajustez :
   - **Encapsulation** : MP4, AVI, MKV, etc.
   - **Codec vidéo** : H.264, H.265, VP9
   - **Résolution** : 1080p, 720p, 480p
   - **Débit** : Qualité (plus élevé = meilleure qualité mais fichier plus gros)
   - **Codec audio** : MP3, AAC, FLAC
4. Sauvegardez le profil

## Enregistrement d'écran

VLC peut capturer votre écran (screencast).

### Enregistrer l'écran

1. Menu **Média** → **Ouvrir un périphérique de capture**
2. **Mode de capture** : **Bureau**
3. **Images par seconde** : 30 fps (fluide) ou 15 fps (léger)
4. Cliquez sur la flèche à côté de **Lire** → **Convertir**
5. Choisissez un profil (MP4 recommandé)
6. Fichier de destination
7. Cliquez sur **Démarrer**
8. VLC enregistre tout ce qui se passe à l'écran

**Arrêter l'enregistrement** :
- Cliquez sur **Stop** dans VLC

**Alternatives plus complètes** :
- OBS Studio (mieux adapté au screencast)
- SimpleScreenRecorder
- Kazam

## Préférences et paramètres

### Ouvrir les préférences

1. Menu **Outils** → **Préférences**
2. Raccourci : `Ctrl + P`

**Deux modes** :
- **Simple** : Paramètres essentiels (par défaut)
- **Tous** : Paramètres avancés (cochez en bas)

### Paramètres importants

**Interface** :
- **Langue** : Changer la langue de VLC
- **Apparence** : Thème sombre ou clair
- **Démarrer en mode réduit** : Icône dans la zone de notification

**Audio** :
- **Périphérique de sortie** : Choisir vos haut-parleurs
- **Activer l'audio** : Pour désactiver par défaut

**Vidéo** :
- **Plein écran** : Toujours démarrer en plein écran
- **Répertoire des captures** : Où sauvegarder les screenshots
- **Accélération matérielle** : Utilise le GPU (recommandé)

**Sous-titres / OSD** :
- **Activer OSD** : Affiche infos à l'écran (volume, titre)
- **Sous-titres** : Police, taille, couleur
- **Piste par défaut** : Langue préférée

**Entrée / Codecs** :
- **Mise en cache réseau** : Pour le streaming (augmenter si saccades)
- **Saut court** : Durée du saut avec flèches (défaut 10s)

**Touches de raccourcis** :
- Personnalisez tous les raccourcis clavier
- **Tous** → **Interface** → **Raccourcis clavier**

### Réinitialiser les préférences

Si VLC a un comportement étrange :

1. **Outils** → **Préférences**
2. En bas : **Réinitialiser les préférences**
3. Redémarrez VLC

## Raccourcis clavier essentiels

### Lecture

| Raccourci | Action |
|-----------|--------|
| `Espace` | Lecture / Pause |
| `S` | Stop |
| `N` | Suivant |
| `P` | Précédent |
| `[` | Plus lent |
| `]` | Plus rapide |
| `=` | Vitesse normale |

### Navigation

| Raccourci | Action |
|-----------|--------|
| `→` | Avance 10 secondes |
| `←` | Recule 10 secondes |
| `Alt + →` | Avance 1 minute |
| `Alt + ←` | Recule 1 minute |
| `Ctrl + →` | Avance 5 minutes |
| `Ctrl + ←` | Recule 5 minutes |

### Interface

| Raccourci | Action |
|-----------|--------|
| `F` ou `F11` | Plein écran |
| `Ctrl + H` | Masquer/Afficher les contrôles |
| `Ctrl + L` | Liste de lecture |
| `Ctrl + E` | Effets et filtres |
| `Ctrl + M` | Interface minimale |

### Audio et vidéo

| Raccourci | Action |
|-----------|--------|
| `Ctrl + ↑` | Volume + |
| `Ctrl + ↓` | Volume - |
| `M` | Muet |
| `B` | Changer piste audio |
| `V` | Changer piste sous-titres |
| `H` | Retarder sous-titres |
| `G` | Avancer sous-titres |
| `J` | Retarder audio |
| `K` | Avancer audio |

### Autres

| Raccourci | Action |
|-----------|--------|
| `Maj + S` | Capture d'écran |
| `R` | Aléatoire |
| `L` | Boucle |
| `T` | Afficher le temps |
| `Ctrl + Q` | Quitter |

## Astuces et fonctionnalités avancées

### Reprendre la lecture où vous étiez

VLC mémorise automatiquement votre position :
- Fermez VLC pendant une vidéo
- Rouvrez le même fichier
- VLC demande : "Reprendre la lecture ?" → Cliquez **Oui**

### Créer des chapitres

Pour naviguer facilement dans de longues vidéos :

1. **Lecture** → **Signets personnalisés** → **Gérer**
2. Créez plusieurs signets aux moments clés
3. Nommez-les clairement
4. Naviguez rapidement entre chapitres

### Boucle A-B (répéter un segment)

Pour répéter une portion spécifique :

1. Avancez au début du segment (point A)
2. Menu **Lecture** → **Boucle A→B** → **Définir le point A**
3. Avancez à la fin du segment (point B)
4. **Boucle A→B** → **Définir le point B**
5. VLC répète en boucle ce segment

**Annuler** : **Boucle A→B** → **Effacer**

**Utilité** :
- Apprendre une danse
- Étudier un passage musical
- Revoir une scène spécifique

### Décalage d'images (frame by frame)

Pour avancer image par image :
- Mettez en pause
- Appuyez sur `E`
- Chaque pression avance d'une image

**Utile pour** :
- Analyser une vidéo
- Trouver le moment exact pour une capture
- Vérifier des détails

### Visualisations audio

Quand vous écoutez de la musique :

1. Menu **Audio** → **Visualisations**
2. Choisissez : Spectromètre, Oscilloscope, 3D Spectrum, Goom
3. Un effet visuel s'affiche

**Changer de visualisation** : `Ctrl + W`

### Regarder plusieurs vidéos simultanément

VLC peut ouvrir plusieurs fenêtres :
1. Lancez VLC normalement
2. Menu **Média** → **Nouvelle instance de VLC**
3. Ou depuis le terminal : `vlc video1.mp4 &` puis `vlc video2.mp4 &`

### Picture-in-Picture (PiP) manuel

Avec l'extension "PiP" ou manuellement :
1. Activez **Vidéo** → **Toujours au premier plan**
2. Réduisez la taille de la fenêtre VLC
3. Placez-la dans un coin
4. Continuez à travailler, la vidéo reste visible

### Extraire des images d'une vidéo

**À un moment précis** :
- `Maj + S` : Capture d'écran

**En continu (séquence d'images)** :
1. **Préférences avancées** (Tous)
2. **Vidéo** → **Filtres**
3. Cochez **Filtre de fichiers de scènes vidéo**
4. **Filtres** → **Scene filter**
5. Configurez : ratio d'enregistrement, format, préfixe
6. Lancez votre vidéo, VLC enregistre des images à intervalle régulier

## Extensions VLC

VLC supporte des extensions pour ajouter des fonctionnalités.

### Installer une extension

1. Téléchargez le fichier `.lua` de l'extension
2. Copiez-le dans `~/.local/share/vlc/lua/extensions/`
3. Redémarrez VLC
4. Menu **Vue** → L'extension apparaît

### Extensions populaires

**VLSub** :
- Télécharge automatiquement des sous-titres
- Cherche sur OpenSubtitles

**Podcasts** :
- Gestionnaire de podcasts intégré

**Telecharger sous-titres** :
- Alternative à VLSub

**YouTube Playlists** :
- Importe des playlists YouTube

**Où trouver des extensions** :
- [https://addons.videolan.org/](https://addons.videolan.org/)
- Forums VLC

## Dépannage courant

### Le son fonctionne mais pas l'image

**Solutions** :
1. Vérifiez les paramètres vidéo
2. **Outils** → **Préférences** → **Vidéo**
3. **Module de sortie** : Essayez **Sortie vidéo X11 (XCB)**
4. Désactivez temporairement **Accélération matérielle**
5. Redémarrez VLC

### L'image fonctionne mais pas le son

**Solutions** :
1. Vérifiez que VLC n'est pas en muet (`M`)
2. **Audio** → **Périphérique audio** → Vérifiez la sortie
3. Volume système Linux Mint : Vérifiez qu'il n'est pas muet
4. Clic droit sur VLC → **Mixer de volume** → Montez le volume de VLC

### Vidéo saccadée (lag)

**Solutions** :
1. Activez l'**accélération matérielle** :
   - **Préférences** → **Entrée / Codecs** → **Décodage accéléré par le matériel**
2. Réduisez la qualité si c'est un stream (choisissez une résolution plus basse)
3. Fermez les autres applications gourmandes
4. Mettez à jour VLC et vos pilotes graphiques

### Sous-titres illisibles ou qui défilent trop vite

**Solutions** :
1. Vérifiez l'encodage : Menu **Outils** → **Préférences** → **Sous-titres** → **UTF-8**
2. Ajustez la synchronisation avec `H` et `G`
3. Changez la police/taille dans les préférences

### Le fichier ne s'ouvre pas

**Solutions** :
1. Format non supporté ? (rare avec VLC)
2. Fichier corrompu ? Essayez de le réouvrir
3. Mettez à jour VLC : `sudo apt update && sudo apt upgrade`
4. Essayez un autre lecteur (Celluloid, MPV)

### DVD commercial ne se lit pas

**Solution** :
```bash
sudo apt install libdvd-pkg  
sudo dpkg-reconfigure libdvd-pkg  
```
Sélectionnez **Oui** pour installer les codecs de décryptage.

### VLC crashe ou freeze

**Solutions** :
1. Réinitialisez les préférences : **Outils** → **Préférences** → **Réinitialiser**
2. Supprimez le cache :
   ```bash
   rm -rf ~/.cache/vlc
   rm -rf ~/.config/vlc
   ```
3. Réinstallez VLC :
   ```bash
   sudo apt remove vlc
   sudo apt install vlc
   ```

## Autres lecteurs multimédia disponibles

### Celluloid (ex-GNOME MPV)

**Caractéristiques** :
- Interface moderne et minimaliste
- Basé sur MPV (moteur puissant)
- Léger et rapide
- Moins de fonctionnalités que VLC mais plus simple

**Installation** :
```bash
sudo apt install celluloid
```

**Quand l'utiliser** :
- Vous voulez une interface épurée
- Lecture simple sans configuration complexe

### MPV

**Caractéristiques** :
- Lecteur en ligne de commande (peut avoir une interface)
- Extrêmement léger et performant
- Configuration via fichiers texte
- Préféré des utilisateurs avancés

**Installation** :
```bash
sudo apt install mpv
```

**Utilisation** :
```bash
mpv video.mp4  
mpv --fs video.mp4  # Plein écran  
mpv https://exemple.com/stream.m3u8  # Stream  
```

### Parole (lecteur vidéo GNOME)

**Caractéristiques** :
- Simple et intégré à GNOME
- Interface minimaliste
- Fonctionnalités basiques

**Limitation** : Moins de formats supportés que VLC

### Audacious (musique)

**Caractéristiques** :
- Spécialisé dans la musique
- Interface Winamp-like
- Gestionnaire de bibliothèque
- Léger

**Installation** :
```bash
sudo apt install audacious
```

### Rhythmbox (musique)

**Caractéristiques** :
- Gestionnaire de bibliothèque musicale complet
- Similaire à iTunes
- Podcasts, radio Internet
- Préinstallé sur certaines distributions

**Quand l'utiliser** :
- Vous avez une grande collection musicale à organiser
- Vous voulez gérer vos playlists et métadonnées

### Comparaison rapide

| Lecteur | Usage | Complexité | Formats |
|---------|-------|------------|---------|
| **VLC** | Vidéo/Audio universel | Moyenne | Tous |
| **Celluloid** | Vidéo simple | Faible | Beaucoup |
| **MPV** | Vidéo avancé | Élevée | Tous |
| **Parole** | Vidéo basique | Très faible | Courants |
| **Audacious** | Musique | Faible | Audio |
| **Rhythmbox** | Bibliothèque musicale | Moyenne | Audio |

## Codecs et formats

### Qu'est-ce qu'un codec ?

Un **codec** (compresseur-décompresseur) est un algorithme qui compresse et décompresse les données audio/vidéo.

**Exemples de codecs vidéo** :
- **H.264 (AVC)** : Le plus courant, bon équilibre
- **H.265 (HEVC)** : Meilleur que H.264, compression supérieure
- **VP9** : Open source, utilisé par YouTube
- **AV1** : Nouveau, très efficace, open source

**Exemples de codecs audio** :
- **MP3** : Universel, bon pour la musique
- **AAC** : Meilleur que MP3, utilisé par iTunes
- **FLAC** : Sans perte, qualité maximale
- **Opus** : Moderne, efficace pour la voix

### Conteneurs vs Codecs

**Conteneur** : Format du fichier (l'emballage)
- MP4, MKV, AVI, MOV, WebM

**Codec** : Algorithme de compression (le contenu)
- H.264, H.265, VP9, MP3, AAC

**Exemple** :
- Un fichier **MP4** peut contenir de la vidéo **H.264** et de l'audio **AAC**
- Un fichier **MKV** peut contenir de la vidéo **H.265** et de l'audio **FLAC**

### VLC et les codecs

**Avantage de VLC** :
- Tous les codecs sont **intégrés**
- Pas besoin d'installer des packs de codecs supplémentaires
- Fonctionne "out of the box"

**Sur Windows** :
- Souvent besoin d'installer K-Lite Codec Pack
- Avec VLC : Rien à installer !

## Légalité et streaming

### Contenu légal

**Utilisations légales de VLC** :
- Lire vos propres vidéos et musiques
- Lire des DVDs/Blu-rays que vous possédez
- Streaming de contenu libre (Creative Commons)
- Radios et podcasts gratuits
- Contenu du domaine public

### Attention aux usages illégaux

**Illégal** :
- Télécharger ou streamer du contenu piraté
- Contourner les DRM de manière illégale
- Redistribuer du contenu protégé

**VLC est un outil** :
- Comme un couteau peut cuisiner ou blesser
- VLC lui-même est légal et légitime
- C'est l'usage qui peut être problématique

### IPTV et streaming

**IPTV légal** :
- Services officiels (FAI, abonnements légaux)
- Chaînes gratuites et libres

**IPTV illégal** :
- Listes de chaînes piratées
- Abonnements suspects à bas prix

**Conseil** : Privilégiez les services légaux et officiels.

## Ressources et aide

### Documentation officielle

- Site officiel : [https://www.videolan.org/vlc/](https://www.videolan.org/vlc/)
- Wiki VLC : [https://wiki.videolan.org/](https://wiki.videolan.org/)
- Forum : [https://forum.videolan.org/](https://forum.videolan.org/)

### Communauté

- Reddit : r/VLC
- Forum Linux Mint
- Documentation Ubuntu (applicable à Mint)

### Tutoriels et guides

- YouTube : Nombreux tutoriels VLC en français
- Wiki VideoLAN très complet
- Guides en ligne multiples

## Conclusion

VLC Media Player est un outil exceptionnel, gratuit, puissant et universel pour tous vos besoins multimédia sur Linux Mint. Que vous regardiez des films, écoutiez de la musique, convertissiez des fichiers ou diffusiez du contenu, VLC a tout ce qu'il faut.

Ses avantages principaux :
- **Lit absolument tout** sans installer de codecs supplémentaires
- **Gratuit et sans publicité**
- **Multiplateforme** : Vos compétences VLC sont transférables
- **Fonctionnalités avancées** : Conversion, streaming, effets, etc.
- **Interface personnalisable** selon vos préférences

Prenez le temps d'explorer les fonctionnalités, de mémoriser quelques raccourcis clavier utiles, et VLC deviendra rapidement votre lecteur multimédia de référence. N'hésitez pas à expérimenter avec les effets, les conversions et les paramètres pour découvrir tout son potentiel !

---


⏭️ [Visionneuse et retouche d'images](/05-applications-essentielles-et-outils-mint/05-visionneuse-et-retouche-dimages.md)
