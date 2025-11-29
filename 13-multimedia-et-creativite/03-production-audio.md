🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 13.3 Production audio (Audacity, Ardour)

## Introduction

La production audio sous Linux Mint dispose d'outils professionnels gratuits qui peuvent rivaliser avec des logiciels commerciaux coûteux. Que vous souhaitiez enregistrer un podcast, nettoyer une piste audio, créer de la musique ou produire une bande sonore, Linux offre des solutions adaptées à tous les niveaux.

Dans ce chapitre, nous allons découvrir les deux principaux logiciels de production audio sous Linux :

- **Audacity** : éditeur audio simple et puissant, idéal pour débuter
- **Ardour** : station de travail audio numérique (DAW) professionnelle

> **Bon à savoir** : Ces logiciels sont utilisés par des professionnels du monde entier pour produire musique, podcasts, livres audio et bandes sonores.

---

## Concepts de base de l'audio numérique

Avant de plonger dans les logiciels, familiarisons-nous avec quelques notions essentielles.

### Fréquence d'échantillonnage (Sample Rate)

C'est le nombre de fois par seconde où le son est "échantillonné" (mesuré).

**Valeurs courantes :**
- **44.1 kHz** : standard CD audio, qualité excellente
- **48 kHz** : standard vidéo et production pro
- **96 kHz ou 192 kHz** : très haute qualité (fichiers lourds)

> **Pour débuter** : Utilisez 44.1 kHz pour la musique, 48 kHz pour les vidéos.

### Profondeur de bits (Bit Depth)

Détermine la précision de l'enregistrement et la plage dynamique.

**Valeurs courantes :**
- **16 bits** : standard CD, très bien pour la plupart des usages
- **24 bits** : qualité studio professionnelle
- **32 bits (float)** : pour le traitement et mixage pro

> **Pour débuter** : 16 bits suffit largement pour podcasts et enregistrements personnels.

### Format audio

**Formats sans perte :**
- **WAV** : non compressé, fichiers volumineux, qualité maximale
- **FLAC** : compressé sans perte, bon compromis
- **AIFF** : équivalent Apple du WAV

**Formats avec perte (compressés) :**
- **MP3** : universel, petit fichier, perte de qualité légère
- **OGG Vorbis** : open source, meilleure qualité que MP3 à taille égale
- **AAC** : utilisé par Apple, bonne qualité

> **Règle d'or** : Travaillez toujours en WAV ou FLAC, exportez en MP3 uniquement pour la diffusion finale.

### Mono vs Stéréo

- **Mono** : un seul canal audio (voix parlée, podcast simple)
- **Stéréo** : deux canaux (gauche/droite) pour la spatialisation (musique)

### Décibels (dB)

Unité de mesure du volume sonore. Dans l'audio numérique :
- **0 dB** : volume maximum (ne jamais dépasser = saturation)
- **-6 dB** : niveau recommandé pour les pics de voix
- **-12 à -18 dB** : niveau moyen confortable
- **-∞ dB** : silence absolu

> **Important** : Si vos pics touchent 0 dB, vous avez de la saturation (son distordu). Restez toujours en dessous.

---

## Audacity - L'éditeur audio accessible

### Qu'est-ce qu'Audacity ?

Audacity est un éditeur et enregistreur audio gratuit et open source, devenu le standard de facto pour l'édition audio simple sous toutes les plateformes. C'est l'outil parfait pour débuter.

**Points forts :**
- Interface simple et intuitive
- Courbe d'apprentissage douce
- Nombreux effets intégrés
- Enregistrement multicanal
- Édition non destructive
- Léger et rapide
- Documentation abondante

**Utilisations principales :**
- Enregistrer et éditer des podcasts
- Nettoyer des enregistrements audio
- Convertir des formats audio
- Découper et assembler des pistes
- Appliquer des effets (réverbe, compression, égalisation)
- Restaurer de vieux enregistrements
- Créer des sonneries et samples

### Installation d'Audacity

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "Audacity"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update
sudo apt install audacity
```

**Version Flatpak (plus récente) :**
```bash
flatpak install flathub org.audacityteam.Audacity
```

> **Note** : En 2024, Audacity a connu des changements de propriétaire. La version des dépôts Ubuntu/Mint est stable et recommandée. La version Flatpak est plus récente mais peut avoir quelques différences.

### Découverte de l'interface Audacity

L'interface d'Audacity est simple et claire :

**Zones principales :**

1. **Barre d'outils de transport** (en haut) :
   - Lecture, Pause, Stop, Enregistrement
   - Aller au début/fin

2. **Barre d'outils d'édition** :
   - Outils de sélection, zoom, déplacement temporel

3. **Compteurs de niveau** (en haut à droite) :
   - Vu-mètres d'enregistrement et lecture
   - Indicateurs de saturation (rouge = mauvais)

4. **Pistes audio** (zone centrale) :
   - Forme d'onde de vos enregistrements
   - Plusieurs pistes peuvent être superposées

5. **Timeline** (règle en haut des pistes) :
   - Affiche le temps en secondes ou minutes

### Premier enregistrement avec Audacity

#### 1. Vérifier les paramètres d'entrée

Avant d'enregistrer :
- Vérifiez le **périphérique d'enregistrement** dans le menu déroulant (barre du haut)
- Choisissez votre micro (Built-in, USB, etc.)
- Vérifiez le **canal** : Mono pour la voix, Stéréo pour la musique

#### 2. Régler le niveau d'enregistrement

- Cliquez sur le **microphone** à droite du vu-mètre d'enregistrement
- Testez votre voix et ajustez le curseur
- Les pics doivent atteindre environ **-12 à -6 dB** (zone jaune)
- Ne jamais toucher 0 dB (rouge = saturation)

#### 3. Lancer l'enregistrement

- Appuyez sur le **bouton rouge** (Enregistrement) ou `R`
- Parlez dans votre micro
- La forme d'onde s'affiche en temps réel
- Appuyez sur **Pause** pour faire une pause
- Appuyez sur **Stop** (carré) ou `Espace` pour arrêter

#### 4. Écouter votre enregistrement

- Appuyez sur **Lecture** (triangle vert) ou `Espace`
- Utilisez la **barre d'espace** pour Lecture/Pause

### Éditer votre audio avec Audacity

#### 1. Sélectionner une portion

- **Outil de sélection** (I-beam) : cliquez et glissez sur la forme d'onde
- Double-clic : sélectionne tout
- `Ctrl + A` : sélectionne tout

#### 2. Couper, copier, coller

Comme un traitement de texte :
- `Ctrl + X` : couper
- `Ctrl + C` : copier
- `Ctrl + V` : coller
- `Suppr` : supprimer la sélection
- `Ctrl + Z` : annuler

#### 3. Supprimer les silences

Pour enlever un passage :
- Sélectionnez la portion à supprimer
- Appuyez sur `Ctrl + K` ou `Suppr`
- Les parties se rapprochent automatiquement

#### 4. Fondu enchaîné (Fade in/out)

**Fondu d'ouverture (Fade in) :**
- Sélectionnez le début de votre audio (1-2 secondes)
- `Effet` → `Fondu en ouverture`

**Fondu de fermeture (Fade out) :**
- Sélectionnez la fin de votre audio
- `Effet` → `Fondu en fermeture`

#### 5. Normaliser le volume

Augmente le volume au maximum sans saturation :
- Sélectionnez tout (`Ctrl + A`)
- `Effet` → `Normaliser`
- Cochez "Normaliser l'amplitude de crête à" : -1.0 dB
- Cliquez sur OK

#### 6. Supprimer le bruit de fond

**Processus en deux étapes :**

**Étape 1 : Capturer le profil de bruit**
- Sélectionnez une portion où il n'y a QUE du bruit (2-3 secondes de silence)
- `Effet` → `Réduction du bruit`
- Cliquez sur "Prendre le profil de bruit"

**Étape 2 : Appliquer la réduction**
- Sélectionnez toute la piste (`Ctrl + A`)
- `Effet` → `Réduction du bruit`
- Ajustez les paramètres (valeurs par défaut = bon départ)
- Cliquez sur OK

> **Attention** : Une réduction trop agressive crée un son "robotique". Allez-y progressivement.

#### 7. Égalisation (EQ)

Ajuster les fréquences pour améliorer le son :
- `Effet` → `Égalisation et filtres` → `Égaliseur graphique`
- Boostez légèrement les **basses fréquences** (80-200 Hz) pour la chaleur
- Boostez les **hautes fréquences** (8-12 kHz) pour la clarté
- Coupez autour de 300 Hz si la voix sonne "boueuse"

**Presets courants :**
- **Voix parlée** : boost léger à 200 Hz et 5 kHz
- **Podcast** : coupe à 80 Hz (enlever rumble), boost à 3-5 kHz

#### 8. Compression

Réduit la différence entre les parties fortes et faibles :
- `Effet` → `Compresseur`
- **Seuil** : -12 dB
- **Ratio** : 3:1
- **Attaque** : 5 ms
- **Relâchement** : 50 ms

> **Résultat** : Volume plus uniforme, plus agréable à écouter.

#### 9. Amplifier

Augmente le volume de manière linéaire :
- `Effet` → `Amplifier`
- Entrez une valeur en dB (ex: +3 dB)
- OU cochez "Autoriser la saturation" (déconseillé)

> **Préférez Normaliser** à Amplifier pour éviter la saturation.

### Travailler avec plusieurs pistes

#### Importer un fichier audio

- `Fichier` → `Importer` → `Audio`
- Sélectionnez votre fichier (musique, effet sonore, etc.)
- Il s'ajoute sur une nouvelle piste

#### Mixer plusieurs pistes

**Exemple : Podcast avec musique de fond**

1. **Piste 1** : Votre enregistrement principal
2. **Piste 2** : Musique de fond

**Ajuster les volumes :**
- Cliquez sur le **curseur de volume** (en haut à gauche de chaque piste)
- Baissez la musique à environ **-12 à -18 dB** pour qu'elle reste en fond
- La voix doit toujours être clairement audible

**Synchroniser :**
- Utilisez l'**outil de déplacement temporel** (double flèche)
- Glissez une piste pour la décaler dans le temps

#### Créer un fondu croisé

Pour une transition douce entre deux musiques :
- Superposez légèrement les deux pistes
- Appliquez un Fade out à la première
- Appliquez un Fade in à la seconde

### Effets audio utiles

Audacity propose des dizaines d'effets. Voici les plus utiles :

| Effet | Utilisation | Paramètres de base |
|-------|-------------|-------------------|
| **Réduction du bruit** | Enlever bruit de fond | Profil + application |
| **Normaliser** | Volume maximum sans saturation | -1.0 dB |
| **Compresseur** | Uniformiser le volume | Seuil -12, Ratio 3:1 |
| **Égaliseur** | Ajuster les fréquences | Selon voix/musique |
| **Réverbe** | Ajouter de l'espace, écho | Taille de salle 50% |
| **Changer la hauteur** | Modifier la tonalité | En demi-tons |
| **Changer la vitesse** | Accélérer/ralentir | En % |
| **Auto-Duck** | Baisser musique sous voix | Seuil -30 dB |
| **Cliquer/pop** | Enlever clics (vinyles) | Seuil 200 |

### Exporter votre projet

#### Sauvegarder le projet (format Audacity)

Pour continuer plus tard :
- `Fichier` → `Enregistrer le projet` → `Enregistrer le projet sous`
- Format : `.aup3` (fichier projet Audacity)
- Conserve toutes les pistes et modifications

> **Important** : Le fichier .aup3 n'est PAS un fichier audio lisible. C'est uniquement pour Audacity.

#### Exporter en fichier audio

Pour créer un fichier écouTable :
- `Fichier` → `Exporter` → `Exporter l'audio`

**Formats recommandés :**

**Pour la qualité maximale (archivage) :**
- Format : **WAV** (Microsoft)
- Encodage : 16-bit PCM
- Résultat : fichier volumineux, qualité parfaite

**Pour la diffusion (podcast, web) :**
- Format : **MP3**
- Qualité : 192-320 kbps (320 = meilleure qualité)
- Mode : Joint Stereo (ou Mono pour podcast parlé)

**Pour l'open source (alternative MP3) :**
- Format : **OGG Vorbis**
- Qualité : 5-8 (8 = meilleure)

#### Exporter plusieurs pistes séparément

Si vous avez plusieurs pistes et voulez les exporter individuellement :
- `Fichier` → `Exporter` → `Exporter plusieurs`
- Choisissez d'exporter par piste ou par label

### Restaurer de vieux enregistrements

Audacity excelle dans la restauration audio :

**Pour enlever les craquements (vinyles) :**
- `Effet` → `Cliquer/pop`
- Ajustez le seuil (commencez par 200)

**Pour enlever le souffle (cassettes) :**
- `Effet` → `Réduction du bruit`
- Même méthode que pour le bruit de fond

**Pour améliorer la clarté :**
- `Effet` → `Égaliseur`
- Boost léger des hautes fréquences (5-8 kHz)

### Raccourcis clavier essentiels Audacity

| Raccourci | Action |
|-----------|--------|
| `Espace` | Lecture/Pause |
| `R` | Démarrer l'enregistrement |
| `Ctrl + R` | Ajouter enregistrement sur nouvelle piste |
| `Shift + A` | Ajouter nouveau piste audio |
| `Ctrl + A` | Sélectionner tout |
| `Ctrl + 1` | Zoomer |
| `Ctrl + 3` | Dézoomer |
| `Ctrl + F` | Ajuster à la fenêtre |
| `Ctrl + Z` | Annuler |
| `Ctrl + Y` | Rétablir |
| `Ctrl + K` | Supprimer sélection |
| `Ctrl + L` | Silence (remplir sélection de silence) |

---

## Ardour - La station de travail audio professionnelle

### Qu'est-ce qu'Ardour ?

Ardour est une station de travail audio numérique (DAW - Digital Audio Workstation) professionnelle, équivalente à Pro Tools, Logic Pro ou Cubase. C'est l'outil de choix pour la production musicale, le mixage multi-pistes et la post-production audio complexe.

**Points forts :**
- Niveau professionnel absolu
- Enregistrement multi-pistes illimité
- Automation avancée
- Support MIDI complet
- VST/LV2 plugins
- Mixage et routing complexe
- Édition non destructive
- Utilisé en studio professionnel

**Points faibles :**
- Courbe d'apprentissage raide
- Interface dense
- Peut être intimidant pour débutants
- Nécessite configuration audio (JACK ou PulseAudio)

**Utilisations principales :**
- Production musicale multi-instruments
- Enregistrement de groupes/orchestres
- Mixage professionnel
- Mastering
- Post-production audio pour film/vidéo
- Création de bandes sonores complexes

### Installation d'Ardour

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "Ardour"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update
sudo apt install ardour
```

**Version officielle (recommandée pour pros) :**
- Téléchargeable sur https://ardour.org
- Version payante (contribution libre) avec support
- Binaires optimisés

> **Note** : Ardour est gratuit et open source, mais les développeurs proposent une version payante compilée pour soutenir le projet.

### Configuration audio pour Ardour

Ardour fonctionne mieux avec **JACK Audio Connection Kit**, un serveur audio basse latence.

#### Installer JACK

```bash
sudo apt install jackd2 qjackctl
```

#### Configurer JACK avec QjackCtl

1. Lancez **QjackCtl** depuis le menu
2. Cliquez sur **Setup**
3. Paramètres recommandés pour débuter :
   - **Sample Rate** : 48000 Hz
   - **Frames/Period** : 1024 (basse latence = 256-512, mais plus exigeant)
   - **Periods/Buffer** : 2
4. Cliquez sur **OK**
5. Cliquez sur **Start** pour démarrer JACK

> **Alternative** : Ardour peut aussi fonctionner avec PulseAudio (plus simple mais moins pro).

### Découverte de l'interface Ardour

L'interface d'Ardour est complexe mais logique :

**Zones principales :**

1. **Editor Window** (fenêtre principale) :
   - Timeline : ligne de temps horizontale
   - Pistes : affichent les régions audio/MIDI
   - Mixer à droite

2. **Mixer Window** (fenêtre de mixage) :
   - Console de mixage virtuelle
   - Faders, pan, inserts, sends
   - Vu-mètres

3. **Transport** (en haut) :
   - Contrôles de lecture, enregistrement
   - Indicateur de position
   - Tempo et signature temporelle

### Créer votre premier projet Ardour

#### 1. Lancer Ardour et créer une session

- Lancez **Ardour**
- Cliquez sur **New Session**
- Remplissez :
  - **Session Name** : nom de votre projet
  - **Session Folder** : où sauvegarder
  - **Sample Rate** : 48 kHz (recommandé)
  - **Template** : Empty Session (pour débuter)

#### 2. Ajouter des pistes

- Clic droit dans la zone de pistes → **Add Track/Bus/VCA**
- Ou menu `Session` → `Add Track, Bus or VCA`

**Types de pistes :**
- **Audio Track** : pour enregistrer du son (voix, instruments)
- **MIDI Track** : pour enregistrer des notes MIDI (clavier, synthé)
- **Audio Bus** : pour grouper et router l'audio

**Paramètres :**
- **Track name** : nommez votre piste (ex: "Voix principale", "Guitare")
- **Configuration** : Mono (voix), Stereo (instruments)
- **Record mode** : Normal
- Nombre de pistes : ajoutez-en plusieurs si besoin

#### 3. Préparer l'enregistrement

**Armer la piste :**
- Cliquez sur le **bouton rouge** à gauche de la piste
- La piste est maintenant "armée" pour l'enregistrement

**Sélectionner l'entrée :**
- Cliquez sur le nom de l'entrée (sous le bouton rouge)
- Choisissez votre source (micro, ligne, etc.)

**Vérifier le niveau :**
- Parlez/jouez dans votre micro
- Vérifiez le vu-mètre à droite
- Les pics doivent être autour de -12 à -6 dB

#### 4. Enregistrer

- Placez le curseur de lecture au début (touche `Début`)
- Cliquez sur le **bouton rouge** dans la barre de transport (en haut)
- Ou appuyez sur `Espace` (si configuré pour enregistrer)
- Jouez/chantez
- Cliquez sur **Stop** (carré) pour arrêter

**L'enregistrement apparaît comme une "région" sur la piste.**

#### 5. Écouter

- Désarmez la piste (cliquez à nouveau sur le bouton rouge de la piste)
- Appuyez sur **Play** (triangle) ou `Espace`

### Éditer l'audio dans Ardour

#### Modes d'édition

Ardour a plusieurs modes (barre du haut) :
- **Select/Move Objects** (G) : sélectionner et déplacer régions
- **Select/Move Ranges** (R) : sélectionner des plages temporelles
- **Draw** (D) : dessiner des automations
- **Cut** (C) : couper des régions

#### Opérations de base

**Déplacer une région :**
- Mode "Select/Move Objects"
- Cliquez-glissez la région

**Découper une région :**
- Mode "Select/Move Objects"
- Placez le curseur où couper
- `S` : séparer à la position du curseur

**Dupliquer une région :**
- Sélectionnez la région
- `Alt + D` : dupliquer

**Rogner (trim) une région :**
- Survolez le bord de la région
- Le curseur devient une double flèche
- Cliquez-glissez pour raccourcir/allonger

**Supprimer :**
- Sélectionnez et appuyez sur `Suppr`

#### Fondus (Fades)

**Créer un fondu :**
- Survolez le coin supérieur de la région
- Un petit carré apparaît
- Cliquez-glissez pour créer le fondu
- **Haut gauche** : Fade in
- **Haut droit** : Fade out

**Fondu croisé entre deux régions :**
- Superposez légèrement deux régions
- Ardour crée automatiquement un crossfade

### Mixer dans Ardour

#### Fenêtre de mixage

- Menu `Window` → `Show Mixer`
- Ou appuyez sur `Ctrl + M`

**Éléments du mixer :**
- **Fader** : volume de la piste
- **Pan** : balance gauche/droite (stéréo)
- **Inserts** : effets sur la piste
- **Sends** : envois vers bus/effets
- **Vu-mètre** : niveau audio
- **Solo/Mute** : isoler/couper la piste

#### Ajuster les volumes

**Fader de piste :**
- Cliquez-glissez le fader vertical
- Maintenez `Ctrl` pour ajustements fins
- Double-clic : reset à 0 dB

**Automation de volume :**
- Mode "Draw" (D)
- Cliquez sur la piste pour créer des points
- Créez une courbe de volume qui évolue dans le temps

#### Pan (panoramique)

- Contrôle la position gauche/droite dans le champ stéréo
- Cliquez-glissez le contrôle Pan
- Utile pour positionner les instruments dans l'espace

### Effets et plugins

#### Ajouter un effet (plugin)

**Sur une piste :**
1. Clic droit sur la piste → `Edit` → `Processors`
2. Ou dans le mixer, clic droit dans la zone "Inserts"
3. Choisissez un plugin :
   - **ACE** : plugins intégrés Ardour (EQ, compresseur, etc.)
   - **LV2** : format de plugin Linux
   - **VST** : plugins Windows (via Wine/LinVST)

**Plugins essentiels :**
- **ACE EQ** : égaliseur
- **ACE Compressor** : compression dynamique
- **ACE Reverb** : réverbération
- **ACE Delay** : écho/délai

#### Chaîne d'effets typique pour voix

1. **EQ** : couper les basses fréquences (<80 Hz)
2. **De-esser** : réduire les sifflantes
3. **Compressor** : uniformiser le volume
4. **EQ** : boost léger des médiums (2-4 kHz)
5. **Reverb** (sur send) : ajouter de l'espace

### MIDI dans Ardour

#### Créer une piste MIDI

- `Session` → `Add Track, Bus or VCA`
- Type : **MIDI Track**
- Connectez-la à un synthétiseur virtuel

#### Synthétiseurs virtuels

Ardour ne génère pas de son MIDI lui-même. Il faut ajouter un synthé :

**Installer des synthés :**
```bash
# Synthétiseurs basiques
sudo apt install yoshimi zynaddsubfx qsynth

# Banques de sons
sudo apt install fluid-soundfont-gm
```

**Ajouter un synthé à une piste MIDI :**
1. Clic droit sur piste MIDI → `Edit` → `Processors`
2. Ajoutez un plugin instrument (ex: **ACE Fluid Synth**)
3. Chargez une banque de sons

#### Éditer MIDI

- Double-cliquez sur une région MIDI
- L'éditeur de piano roll s'ouvre
- Cliquez pour ajouter des notes
- Cliquez-glissez pour changer hauteur/longueur

### Exporter votre mixage

#### Export audio

- `Session` → `Export` → `Export to Audio File(s)`

**Paramètres importants :**
- **Format** : WAV (qualité max) ou FLAC (compressé sans perte)
- **Sample Rate** : 48 kHz (ou celui de votre session)
- **Bit Depth** : 24-bit (ou 16-bit pour CD)
- **Normalization** : Cochez "Normalize to" -1.0 dB

**Plage d'export :**
- **Session** : tout le projet
- **Range** : seulement une section

Cliquez sur **Export** et choisissez la destination.

### Sauvegarde dans Ardour

**Sauvegarder la session :**
- `Session` → `Save` (Ctrl + S)
- Sauvegarde régulièrement (toutes les 10 minutes)

**Sauvegarder une copie :**
- `Session` → `Save As`
- Crée une copie complète du projet

**Snapshots :**
- `Session` → `Snapshot (keep working on current version)`
- Crée un point de sauvegarde sans dupliquer les fichiers audio

### Ardour vs Audacity : Quand utiliser quoi ?

| Critère | Audacity | Ardour |
|---------|----------|--------|
| **Courbe d'apprentissage** | Facile | Difficile |
| **Type** | Éditeur audio | DAW (station complète) |
| **Multi-pistes** | Basique (peu de pistes) | Professionnel (illimité) |
| **MIDI** | Non | Oui |
| **Automation** | Limitée | Complète |
| **Plugins** | Basiques | Professionnels |
| **Mixage** | Simple | Console pro |
| **Enregistrement live** | Simple | Multi-pistes simultané |
| **Production musicale** | Non adapté | Excellent |
| **Podcast simple** | Parfait | Surdimensionné |
| **Ressources système** | Léger | Plus exigeant |

---

## Choix du logiciel selon vos besoins

### Utilisez Audacity si vous voulez :

- ✅ Enregistrer et éditer un podcast simple
- ✅ Nettoyer un enregistrement audio
- ✅ Découper et assembler des fichiers audio
- ✅ Appliquer des effets basiques
- ✅ Convertir entre formats audio
- ✅ Débuter rapidement sans configuration complexe
- ✅ Restaurer de vieux enregistrements
- ✅ Travailler sur une ou quelques pistes

### Utilisez Ardour si vous voulez :

- ✅ Produire de la musique multi-instruments
- ✅ Enregistrer un groupe de musique
- ✅ Faire du mixage professionnel
- ✅ Travailler avec des dizaines de pistes
- ✅ Utiliser MIDI et synthétiseurs virtuels
- ✅ Avoir un contrôle précis sur chaque aspect
- ✅ Créer des bandes sonores complexes
- ✅ Automatiser le volume, pan, effets

### Workflow recommandé

**Pour un podcast avec musique :**
1. Enregistrez les voix dans **Audacity**
2. Nettoyez et éditez dans Audacity
3. Exportez en WAV
4. Importez tout dans **Ardour** pour le mixage final
5. Ajoutez musique, effets, automation
6. Exportez le master final

**Pour de la musique :**
1. Enregistrez directement dans **Ardour**
2. Éditez, mixez, masterisez dans Ardour
3. Exportez en WAV (archivage) et MP3 (diffusion)

---

## Compléments et outils audio Linux

### JACK Audio Connection Kit

**Qu'est-ce que JACK ?**
- Serveur audio professionnel basse latence
- Permet de router l'audio entre applications
- Indispensable pour Ardour et production sérieuse

**QjackCtl : Interface graphique pour JACK**
```bash
sudo apt install qjackctl
```

### Plugins et effets supplémentaires

**Calf Studio Gear (excellents plugins) :**
```bash
sudo apt install calf-plugins
```

**x42-plugins (outils de mastering) :**
```bash
sudo apt install x42-plugins
```

**LSP Plugins (mastering professionnel) :**
- Télécharger sur https://lsp-plug.in/

### Synthétiseurs virtuels

**ZynAddSubFX (synthé puissant) :**
```bash
sudo apt install zynaddsubfx
```

**Yoshimi (synthé léger) :**
```bash
sudo apt install yoshimi
```

**Helm (synthé moderne) :**
- Télécharger sur https://tytel.org/helm/

### Éditeurs de partition

**MuseScore (notation musicale) :**
```bash
sudo apt install musescore3
```

### Analyseurs audio

**Baudline (analyseur spectral) :**
- Outil d'analyse avancé

**Sonic Visualiser :**
```bash
sudo apt install sonic-visualiser
```

---

## Matériel recommandé pour la production audio

### Interface audio USB

Pour un enregistrement de qualité, investissez dans une interface audio :

**Entrée de gamme (50-100€) :**
- Behringer U-Phoria UMC22
- Focusrite Scarlett Solo
- M-Audio M-Track Solo

**Intermédiaire (100-200€) :**
- Focusrite Scarlett 2i2
- PreSonus AudioBox USB
- Behringer U-Phoria UMC202HD

> **Important** : Vérifiez la compatibilité Linux sur linuxmusicians.com ou linuxaudio.org.

### Microphones

**Dynamiques (robustes, peu chers) :**
- Shure SM58 (classique, 100€)
- Behringer XM8500 (budget, 20€)

**À condensateur (meilleure qualité, plus chers) :**
- Audio-Technica AT2020 (100€)
- Rode NT1-A (200€)
- Blue Yeti USB (150€, plug-and-play)

### Monitoring (écoute)

**Casques :**
- Audio-Technica ATH-M40x (100€)
- Sony MDR-7506 (100€)
- Beyerdynamic DT 770 PRO (150€)

**Enceintes de monitoring :**
- KRK Rokit 5 (300€ la paire)
- Yamaha HS5 (400€ la paire)

> **Conseil** : Casque d'abord, enceintes ensuite si budget le permet.

---

## Optimiser Linux pour l'audio professionnel

### 1. Installer un noyau basse latence

Pour réduire la latence audio (important pour enregistrement live) :

```bash
sudo apt install linux-lowlatency
```

Redémarrez et sélectionnez le noyau lowlatency dans GRUB.

### 2. Configurer les priorités audio

Ajoutez votre utilisateur au groupe audio :
```bash
sudo usermod -aG audio $USER
```

Déconnectez-vous et reconnectez-vous.

### 3. Ajuster les limites système

Créez/éditez `/etc/security/limits.d/audio.conf` :
```bash
sudo nano /etc/security/limits.d/audio.conf
```

Ajoutez :
```
@audio   -  rtprio     95
@audio   -  memlock    unlimited
```

### 4. Désactiver le WiFi pendant l'enregistrement

Le WiFi peut causer des cracklements :
```bash
sudo rfkill block wifi
```

Pour réactiver :
```bash
sudo rfkill unblock wifi
```

---

## Conseils pour des enregistrements de qualité

### 1. Traiter votre pièce

**Problèmes courants :**
- Réverbération excessive
- Échos
- Bruits de fond

**Solutions simples :**
- Enregistrez dans une petite pièce (chambre)
- Ajoutez des textiles (couettes, rideaux épais)
- Évitez les pièces vides et carrelées
- Utilisez un filtre anti-pop (10€)

### 2. Positionnement du micro

**Voix parlée (podcast) :**
- Distance : 10-15 cm
- Légèrement hors axe (pas directement en face)
- Filtre anti-pop entre vous et le micro

**Chant :**
- Distance : 15-30 cm
- Angle légèrement vers le bas
- Filtre anti-pop obligatoire

**Instruments acoustiques :**
- Expérimentez les positions
- Commencez à 30 cm, ajustez selon le rendu

### 3. Niveaux d'enregistrement

**Règle d'or :**
- Pics à **-12 à -6 dB**
- Moyenne à **-18 à -12 dB**
- **Jamais au-dessus de -3 dB**
- 0 dB = saturation = son détruit

> **Mieux vaut enregistrer trop bas que trop haut**. Vous pouvez toujours augmenter après, mais la saturation est irréversible.

### 4. Monitoring (écoute pendant l'enregistrement)

**Audacity :**
- Activez "Software Playthrough" dans les préférences
- Attention : peut causer de la latence

**Ardour :**
- Utilisez le monitoring direct de votre interface audio
- Ou activez le monitoring dans Ardour (bouton de casque)

### 5. Enregistrez en haute qualité

**Paramètres recommandés :**
- Sample Rate : 48 kHz (ou 44.1 kHz)
- Bit Depth : 24 bits (ou 16 bits minimum)
- Format : WAV pendant le travail

> **Ne passez en MP3 qu'à la toute fin**, pour la diffusion.

---

## Workflow typique d'un podcast

### 1. Préparation

- Écrire un plan/script
- Tester le niveau d'enregistrement
- Vérifier que tout fonctionne
- Fermer les applications bruyantes

### 2. Enregistrement (Audacity)

- Enregistrer voix principale
- Faire des pauses si besoin (respiration, eau)
- Ne vous interrompez pas pour les erreurs (on coupera après)

### 3. Montage (Audacity)

- Supprimer les erreurs, silences, hésitations
- Couper les respirations trop bruyantes
- Garder le naturel (ne pas trop couper)

### 4. Nettoyage (Audacity)

- Réduction du bruit de fond
- Normaliser le volume
- Égalisation légère (voix)
- Compression (uniformiser)

### 5. Musique et habillage (Audacity ou Ardour)

- Intro musicale (5-10 secondes)
- Musique de fond (très basse, -18 dB)
- Jingles de transition
- Outro musicale

### 6. Mixage final

- Vérifier que tout est audible
- Pas de saturation
- Volume cohérent du début à la fin

### 7. Export

- WAV 48 kHz 16-bit (archivage)
- MP3 192 kbps (diffusion)
- Métadonnées : titre, auteur, année

---

## Ressources pour progresser

### Documentation officielle

- **Audacity** : https://manual.audacityteam.org/
- **Ardour** : https://manual.ardour.org/

### Communautés francophones

- Forums Linux Mint (section multimédia)
- LinuxMAO (Linux et Musique Assistée par Ordinateur)
- Audiofanzine (forums audio)

### Tutoriels vidéo

- YouTube : nombreux tutoriels Audacity en français
- Ardour : tutoriels en anglais principalement

### Sites de ressources audio

**Effets sonores gratuits :**
- Freesound.org
- Zapsplat.com
- BBC Sound Effects (bbc.co.uk/sounds/play/p07r5s36)

**Musiques libres de droits :**
- YouTube Audio Library
- Incompetech (Kevin MacLeod)
- FreePD.com
- Bensound.com

> **Important** : Vérifiez toujours les licences avant utilisation commerciale.

### Livres et formations

- "The Computer Music Tutorial" (Curtis Roads)
- "Mixing Secrets for the Small Studio" (Mike Senior)
- Formations en ligne (Udemy, OpenClassrooms)

---

## Dépannage courant

### Audacity : Pas de son à l'enregistrement

**Solutions :**
1. Vérifiez le périphérique d'entrée sélectionné
2. Ouvrez les paramètres système audio de Linux Mint
3. Vérifiez que le micro n'est pas muet
4. Testez le micro avec "Sound Recorder" (autre app)

### Audacity : Son haché ou saccadé

**Solutions :**
1. Fermez les applications gourmandes
2. Augmentez la taille du buffer audio :
   - `Édition` → `Préférences` → `Enregistrement`
   - Augmentez "Audio to buffer"
3. Réduisez la fréquence d'échantillonnage (44.1 kHz au lieu de 96 kHz)

### Ardour : Latence importante

**Solutions :**
1. Réduire la taille du buffer JACK (dans QjackCtl)
   - Frames/Period : 256 ou 128
   - Attention : plus de charge CPU
2. Utiliser le noyau lowlatency
3. Activer le monitoring direct de l'interface audio

### Ardour : JACK ne démarre pas

**Solutions :**
1. Fermez toutes les applications audio (navigateur, VLC, etc.)
2. Redémarrez PulseAudio :
```bash
pulseaudio -k
pulseaudio --start
```
3. Relancez JACK
4. Ou configurez JACK pour utiliser PulseAudio comme backend

### Cracklements et clics (xruns)

**Solutions :**
1. Augmentez la taille du buffer JACK
2. Fermez les applications inutiles
3. Désactivez WiFi/Bluetooth temporairement
4. Utilisez le noyau lowlatency
5. Réduisez le nombre de pistes/plugins actifs

---

## Conclusion

Linux Mint offre des outils audio professionnels de premier ordre, que ce soit pour l'édition simple avec **Audacity** ou la production musicale complexe avec **Ardour**. Ces logiciels sont utilisés par des professionnels du monde entier et n'ont rien à envier aux solutions commerciales coûteuses.

**Audacity** est parfait pour débuter : enregistrer des podcasts, nettoyer de l'audio, effectuer des montages simples. Son interface claire et sa documentation abondante en font un choix idéal pour les débutants.

**Ardour** est un outil professionnel complet pour ceux qui veulent aller plus loin : production musicale multi-pistes, mixage avancé, automation complexe, intégration MIDI. Sa courbe d'apprentissage est plus raide, mais le résultat en vaut la peine.

**Notre recommandation :**
1. Commencez avec **Audacity** pour vous familiariser avec les concepts
2. Explorez **Ardour** si vous voulez produire de la musique sérieusement
3. Investissez dans du matériel de base (interface audio, micro décent)
4. Pratiquez régulièrement et expérimentez
5. Rejoignez la communauté LinuxMAO pour apprendre et partager

L'audio sous Linux est un domaine mature et professionnel. Avec de la patience et de la pratique, vous pouvez produire des résultats de qualité studio, le tout avec des outils gratuits et open source.

**Prochaine étape** : Dans la section suivante, nous découvrirons la lecture et l'organisation multimédia sous Linux Mint.

---

*Bonne production audio et que vos créations sonnent parfaitement ! 🎵*

⏭️ [Lecture et organisation multimédia](/13-multimedia-et-creativite/04-lecture-et-organisation-multimedia.md)
