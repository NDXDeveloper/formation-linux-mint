🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.4 - Alternatives aux logiciels Windows courants

## Introduction

L'une des principales inquiétudes lors de la migration vers Linux concerne les logiciels : "Vais-je retrouver mes applications préférées ?" La bonne nouvelle, c'est que pour la grande majorité des usages, il existe d'excellentes alternatives sous Linux, souvent gratuites et open source.

Ce chapitre vous présente les meilleures alternatives Linux pour remplacer vos logiciels Windows habituels, avec leurs avantages, leurs limites, et comment les installer.

> 💡 **Important** : "Alternative" ne signifie pas "copie identique". Certains logiciels Linux sont différents mais tout aussi puissants, voire supérieurs. Gardez l'esprit ouvert !

---

## Comment lire ce guide

Pour chaque catégorie, vous trouverez :

- 🎯 **Alternative recommandée** : le meilleur choix pour débuter
- 📦 **Installation** : comment l'obtenir
- ✅ **Avantages** : ce qui fonctionne bien
- ⚠️ **À savoir** : limitations ou différences importantes
- 🔄 **Autres options** : alternatives secondaires

**Légende pour l'installation :**
- ✨ = Préinstallé dans Linux Mint
- 📦 = Disponible dans le Gestionnaire de logiciels
- 🌐 = Téléchargement depuis le site officiel
- 💻 = Installation en ligne de commande

---

## 📄 Bureautique

### Microsoft Word → LibreOffice Writer

**Type :** Traitement de texte

**Installation :** ✨ Préinstallé

**Description :**
LibreOffice Writer est l'alternative open source à Microsoft Word. C'est un traitement de texte complet et professionnel qui ouvre et enregistre les documents .docx.

✅ **Avantages :**
- Gratuit et sans publicité
- Compatible avec les fichiers Word (.doc, .docx)
- Interface familière (barre d'outils similaire)
- Fonctions avancées (publipostage, table des matières, etc.)
- Export en PDF natif
- Pas de compte Microsoft requis
- Léger et rapide

⚠️ **À savoir :**
- Mise en page complexe peut légèrement varier à l'ouverture de fichiers Word
- Certaines polices Microsoft ne sont pas incluses (installables)
- Macros VBA non supportées (sauf avec extension)
- Interface légèrement différente de Word

**Astuce compatibilité :** Pour une meilleure compatibilité avec Word, installez les polices Microsoft :
```bash
sudo apt install ttf-mscorefonts-installer
```

🔄 **Autres alternatives :**
- **OnlyOffice** (📦) : Interface quasi-identique à Microsoft Office, excellente compatibilité
- **WPS Office** (🌐) : Ressemble beaucoup à MS Office, gratuit mais propriétaire
- **AbiWord** (📦) : Léger, pour usage basique
- **Google Docs** (🌐) : En ligne, synchronisation cloud

---

### Microsoft Excel → LibreOffice Calc

**Type :** Tableur

**Installation :** ✨ Préinstallé

**Description :**
LibreOffice Calc est le tableur de la suite LibreOffice, équivalent d'Excel.

✅ **Avantages :**
- Compatible fichiers Excel (.xls, .xlsx)
- Formules similaires à Excel
- Graphiques et tableaux croisés dynamiques
- Gestion de grandes feuilles de calcul
- Macros (avec langage Basic)

⚠️ **À savoir :**
- Certaines fonctions Excel avancées peuvent manquer
- Macros VBA Excel non compatibles directement
- Limite de 1 048 576 lignes (comme Excel moderne)
- Interface différente mais logique similaire

**Pour qui :** Parfait pour usage personnel, professionnel courant, comptabilité personnelle

🔄 **Autres alternatives :**
- **OnlyOffice Spreadsheet** (📦) : Meilleure compatibilité Excel
- **Gnumeric** (📦) : Tableur léger et rapide
- **Google Sheets** (🌐) : En ligne, collaboratif

---

### Microsoft PowerPoint → LibreOffice Impress

**Type :** Présentation

**Installation :** ✨ Préinstallé

**Description :**
LibreOffice Impress crée des présentations professionnelles.

✅ **Avantages :**
- Ouvre et enregistre les fichiers PowerPoint (.ppt, .pptx)
- Transitions et animations
- Mode présentateur
- Export PDF et HTML
- Templates variés

⚠️ **À savoir :**
- Animations complexes PowerPoint peuvent être simplifiées
- Certains effets visuels peuvent différer
- Templates moins nombreux qu'Office 365

🔄 **Autres alternatives :**
- **OnlyOffice Presentation** (📦)
- **Google Slides** (🌐)

---

### Microsoft Outlook → Thunderbird

**Type :** Client email et calendrier

**Installation :** ✨ Préinstallé

**Description :**
Thunderbird est un client email complet développé par Mozilla (créateurs de Firefox).

✅ **Avantages :**
- Multi-comptes (Gmail, Outlook, etc.)
- Calendrier intégré
- Carnet d'adresses
- Filtres anti-spam efficaces
- Extensions disponibles
- Import depuis Outlook possible
- Open source et respectueux de la vie privée

⚠️ **À savoir :**
- Interface différente d'Outlook
- Synchronisation Exchange nécessite une extension
- Pas de tâches aussi avancées qu'Outlook

**Configuration facile :** Thunderbird détecte automatiquement les paramètres des principaux fournisseurs (Gmail, Yahoo, Outlook.com, etc.)

🔄 **Autres alternatives :**
- **Evolution** (📦) : Similaire à Outlook, intégration Exchange
- **Geary** (📦) : Minimaliste et moderne
- **Mailspring** (🌐) : Interface élégante
- **Gmail/Outlook.com** (🌐) : Version web dans le navigateur

---

### Microsoft OneNote → Joplin

**Type :** Prise de notes

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
Joplin est une application de notes open source avec synchronisation.

✅ **Avantages :**
- Organisation en carnets et notes
- Markdown supporté
- Synchronisation cloud (Dropbox, OneDrive, Nextcloud)
- Pièces jointes
- Chiffrement de bout en bout
- Applications mobiles disponibles

⚠️ **À savoir :**
- Pas d'import direct depuis OneNote (export/import nécessaire)
- Interface différente
- Moins de fonctionnalités de dessin

🔄 **Autres alternatives :**
- **Standard Notes** (🌐) : Focus sur la sécurité et la vie privée
- **Simplenote** (🌐) : Minimaliste
- **Obsidian** (🌐) : Pour notes liées (Zettelkasten)
- **CherryTree** (📦) : Notes hiérarchiques
- **Notion** (🌐) : En ligne, très complet

---

### Notepad / Bloc-notes → Éditeur de texte (xed)

**Type :** Éditeur de texte simple

**Installation :** ✨ Préinstallé

**Description :**
Éditeur de texte simple préinstallé dans Linux Mint.

✅ **Avantages :**
- Ouverture rapide
- Coloration syntaxique (code)
- Rechercher/remplacer
- Numérotation des lignes
- Plugins disponibles

🔄 **Autres alternatives :**
- **gedit** (📦) : Éditeur GNOME
- **Kate** (📦) : Éditeur avancé KDE
- **Sublime Text** (🌐) : Puissant (gratuit avec rappels)
- **VS Code** (🌐) : Pour développement

---

## 🌐 Navigation Internet

### Microsoft Edge / Internet Explorer → Firefox

**Type :** Navigateur web

**Installation :** ✨ Préinstallé

**Description :**
Firefox est le navigateur par défaut de Linux Mint.

✅ **Avantages :**
- Respectueux de la vie privée
- Extensions nombreuses
- Synchronisation entre appareils
- Performance excellente
- Open source
- Bloqueur de publicités intégré
- Protection contre le pistage

⚠️ **À savoir :**
- Certains sites optimisés uniquement pour Chrome peuvent avoir des problèmes (rare)

🔄 **Autres alternatives :**
- **Google Chrome** (🌐) : Version Google de Chromium
- **Chromium** (📦) : Version open source de Chrome
- **Brave** (🌐) : Focus sur la vie privée, bloqueur de pubs intégré
- **Vivaldi** (🌐) : Hautement personnalisable
- **Opera** (🌐) : VPN intégré

**Import des favoris :** Firefox peut importer vos favoris depuis Edge/Chrome lors du premier lancement.

---

## 🎨 Retouche d'images et création graphique

### Adobe Photoshop → GIMP

**Type :** Retouche photo professionnelle

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
GIMP (GNU Image Manipulation Program) est l'alternative open source à Photoshop.

✅ **Avantages :**
- Gratuit et open source
- Très puissant (calques, masques, filtres)
- Supporte les fichiers PSD (Photoshop)
- Plugins et scripts disponibles
- Communauté active
- Fonctionne aussi sous Windows/Mac

⚠️ **À savoir :**
- Interface différente de Photoshop (nécessite adaptation)
- Courbe d'apprentissage
- Certains effets Photoshop avancés absents
- CMJN limité (RVB principalement)
- Mode de fusion des calques parfois différent

**Pour qui :** Retouche photo, création graphique, designers web, photographes

**Astuce interface :** Pour avoir une interface en fenêtre unique comme Photoshop : Fenêtres → Mode fenêtre unique

🔄 **Autres alternatives :**
- **Krita** (📦) : Excellent pour le dessin et la peinture numérique
- **Photopea** (🌐) : Clone Photoshop en ligne (gratuit)
- **Darktable** (📦) : Développement RAW (comme Lightroom)
- **RawTherapee** (📦) : Traitement RAW
- **Pinta** (📦) : Retouche simple (comme Paint.NET)

---

### Adobe Illustrator → Inkscape

**Type :** Dessin vectoriel

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
Inkscape est le logiciel de dessin vectoriel open source de référence.

✅ **Avantages :**
- Gratuit et open source
- Format SVG natif (standard web)
- Outils professionnels complets
- Import/export de nombreux formats
- Communauté et tutoriels abondants

⚠️ **À savoir :**
- Interface différente d'Illustrator
- Fichiers AI (Illustrator) parfois partiellement supportés
- Certains effets Adobe absents

**Pour qui :** Logos, icônes, illustrations vectorielles, design graphique

🔄 **Autres alternatives :**
- **Vectr** (🌐) : Vectoriel en ligne, simple
- **Gravit Designer** (🌐) : Alternative moderne
- **Figma** (🌐) : Design UI/UX en ligne

---

### Paint / Paint 3D → Pinta / Krita

**Type :** Dessin simple

**Installation :** 📦 Gestionnaire de logiciels

**Pinta :**
- ✅ Clone de Paint.NET, interface simple
- ✅ Calques de base
- ✅ Idéal pour retouche rapide

**Krita :**
- ✅ Puissant pour le dessin artistique
- ✅ Pinceaux et brosses avancés
- ✅ Idéal pour tablette graphique

🔄 **Autres alternatives :**
- **Drawing** (📦) : Équivalent MS Paint, très simple
- **MyPaint** (📦) : Peinture numérique
- **Tux Paint** (📦) : Pour les enfants

---

## 🎬 Multimédia - Vidéo

### Windows Media Player → VLC

**Type :** Lecteur multimédia

**Installation :** ✨ Préinstallé (ou 📦)

**Description :**
VLC est LE lecteur multimédia universel. Si un fichier vidéo ou audio existe, VLC peut le lire.

✅ **Avantages :**
- Lit TOUS les formats (MP4, MKV, AVI, FLV, etc.)
- Pas de codec à installer
- Streaming vidéo/audio
- Conversion de formats
- Capture d'écran vidéo
- Léger et rapide
- Gratuit et open source

⚠️ **À savoir :**
- Interface basique (mais fonctionnelle)
- Pas de gestion de bibliothèque multimédia

**Pour qui :** Tout le monde ! C'est l'incontournable.

🔄 **Autres alternatives :**
- **MPV** (📦) : Minimaliste, très performant
- **Celluloid** (📦) : Interface moderne pour MPV
- **SMPlayer** (📦) : Riche en fonctionnalités

---

### Adobe Premiere Pro → Kdenlive

**Type :** Montage vidéo professionnel

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
Kdenlive est un logiciel de montage vidéo non-linéaire open source.

✅ **Avantages :**
- Interface professionnelle
- Multi-pistes audio/vidéo
- Effets et transitions nombreux
- Proxy pour montage de vidéos lourdes
- Titre et sous-titres
- Export de nombreux formats

⚠️ **À savoir :**
- Moins stable que Premiere (mais s'améliore constamment)
- Courbe d'apprentissage
- Certains effets Adobe absents

**Pour qui :** YouTubers, créateurs de contenu, monteurs vidéo

🔄 **Autres alternatives :**
- **DaVinci Resolve** (🌐) : Version gratuite très puissante (semi-professionnel)
- **OpenShot** (📦) : Plus simple, débutant-friendly
- **Shotcut** (📦) : Bon compromis simplicité/puissance
- **Blender** (📦) : Pour 3D + montage vidéo

---

### Windows Movie Maker → OpenShot

**Type :** Montage vidéo simple

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
OpenShot est parfait pour débuter en montage vidéo.

✅ **Avantages :**
- Interface intuitive
- Glisser-déposer simple
- Transitions et titres
- Animation d'images-clés
- Gratuit et open source

⚠️ **À savoir :**
- Moins stable que les solutions payantes
- Fonctionnalités limitées pour usage pro

**Pour qui :** Montage familial, débutants, projets simples

---

## 🎵 Multimédia - Audio

### Windows Media Player (musique) → Rhythmbox

**Type :** Lecteur de musique

**Installation :** ✨ Souvent préinstallé (ou 📦)

**Description :**
Rhythmbox est un lecteur de musique avec gestion de bibliothèque.

✅ **Avantages :**
- Gestion de bibliothèque musicale
- Podcasts
- Radio Internet
- Synchronisation iPod/smartphone
- Lecture de formats variés

🔄 **Autres alternatives :**
- **Clementine** (📦) : Inspiré d'Amarok, très populaire
- **Strawberry** (📦) : Fork moderne de Clementine
- **Audacious** (📦) : Léger, style Winamp
- **Spotify** (📦) : Streaming (version Linux officielle)

---

### Audacity → Audacity

**Type :** Édition audio

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
Bonne nouvelle : Audacity existe aussi sous Linux, identique à la version Windows !

✅ **Avantages :**
- Même logiciel que sous Windows
- Enregistrement et édition audio
- Effets nombreux
- Gratuit et open source

**Pour qui :** Podcasters, musiciens, édition audio

🔄 **Autres alternatives :**
- **Ardour** (📦) : Station audio numérique (DAW) professionnelle
- **LMMS** (📦) : Production musicale électronique
- **Mixxx** (📦) : DJing

---

## 📸 Photo et gestion d'images

### Windows Photos → Visionneuse d'images

**Type :** Visionneuse simple

**Installation :** ✨ Préinstallé

**Description :**
Visionneuse d'images légère préinstallée (xviewer ou eog selon la version).

✅ **Avantages :**
- Rapide
- Rotation, zoom
- Diaporama
- Simple et efficace

🔄 **Autres alternatives :**
- **gThumb** (📦) : Visionneuse + retouche basique
- **Shotwell** (📦) : Gestion de bibliothèque photo (comme Photos)
- **digiKam** (📦) : Gestion professionnelle de photos

---

### Adobe Lightroom → Darktable

**Type :** Développement RAW et catalogage

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
Darktable est l'alternative open source à Lightroom.

✅ **Avantages :**
- Gestion RAW professionnelle
- Table lumineuse (catalogage)
- Retouches non-destructives
- Exports variés
- Gratuit et puissant

⚠️ **À savoir :**
- Interface complexe (courbe d'apprentissage)
- Différent de Lightroom
- Très puissant mais nécessite apprentissage

**Pour qui :** Photographes professionnels et amateurs avancés

🔄 **Autres alternatives :**
- **RawTherapee** (📦) : Autre logiciel RAW excellent
- **Photivo** (📦) : Workflow RAW

---

## 💬 Communication

### Skype → Skype / Alternatives

**Type :** Visioconférence

**Installation :** 📦 Gestionnaire de logiciels (Skype disponible)

**Description :**
Skype existe officiellement sous Linux, mais de nombreuses alternatives existent.

✅ **Skype Linux :**
- Version officielle disponible
- Fonctionne bien

🔄 **Alternatives recommandées :**
- **Zoom** (🌐) : Client Linux disponible
- **Microsoft Teams** (🌐) : Version web ou client Linux
- **Discord** (📦 ou 🌐) : Gaming et communautés
- **Jitsi Meet** (🌐) : Open source, navigateur
- **Signal** (📦) : Messagerie sécurisée avec appels
- **Telegram Desktop** (📦) : Messagerie

---

### WhatsApp Desktop → WhatsApp Web / Alternatives

**Type :** Messagerie instantanée

**Installation :** 🌐 Version web dans le navigateur

**Description :**
WhatsApp fonctionne parfaitement via le navigateur web.

✅ **Solution :**
- WhatsApp Web (web.whatsapp.com)
- Créez un lanceur avec Web Apps Manager (préinstallé dans Mint)

🔄 **Alternatives :**
- **Telegram Desktop** (📦) : Excellente alternative, client natif
- **Signal Desktop** (📦) : Focus sur la vie privée
- **Element** (📦) : Messagerie décentralisée (Matrix)

---

## 🎮 Gaming

### Steam → Steam

**Type :** Plateforme de jeux

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
Steam fonctionne nativement sous Linux avec Proton pour les jeux Windows.

✅ **Avantages :**
- Même compte que Windows
- Proton permet de jouer aux jeux Windows
- De plus en plus de jeux natifs Linux
- Steam Deck = Linux

⚠️ **À savoir :**
- Tous les jeux Windows ne fonctionnent pas (vérifier ProtonDB)
- Anti-cheat peut poser problème
- Performance parfois légèrement inférieure

**Voir chapitre 14 (Gaming sous Linux) pour plus de détails**

🔄 **Autres plateformes :**
- **Lutris** (📦) : Gestionnaire multi-plateformes
- **Heroic Games Launcher** (📦) : Epic Games, GOG
- **itch.io** (🌐) : Jeux indés

---

## 🗜️ Compression et archives

### WinRAR / 7-Zip → Gestionnaire d'archives

**Type :** Compression/décompression

**Installation :** ✨ Préinstallé

**Description :**
Le gestionnaire d'archives de Linux Mint gère tous les formats.

✅ **Avantages :**
- ZIP, RAR, 7Z, TAR.GZ, etc.
- Intégré au clic droit
- Extraction et création
- Gratuit (pas de nag screen comme WinRAR !)

**Utilisation :** Clic droit sur archive → "Extraire ici" ou "Extraire vers..."

---

## 📥 Téléchargement

### Internet Download Manager → uGet / JDownloader

**Type :** Gestionnaire de téléchargements

**Installation :** 📦 Gestionnaire de logiciels

**uGet :**
- ✅ Interface simple
- ✅ Reprendre téléchargements
- ✅ Téléchargements planifiés

**JDownloader :**
- ✅ Hébergeurs de fichiers
- ✅ Automatisation
- ✅ Même version que Windows

🔄 **Autres alternatives :**
- **Xtreme Download Manager** (🌐) : Puissant
- **aria2** (💻) : En ligne de commande, très rapide

---

### BitTorrent / uTorrent → qBittorrent / Transmission

**Type :** Client BitTorrent

**Installation :** 📦 Gestionnaire de logiciels

**qBittorrent :**
- ✅ Open source, sans publicité
- ✅ Interface similaire à uTorrent
- ✅ Recherche intégrée
- ✅ Streaming torrent

**Transmission :**
- ✅ Léger et simple
- ✅ Interface web disponible
- ✅ Préinstallé sur certaines distributions

---

## 🔐 Sécurité et utilitaires

### Antivirus (Windows Defender, etc.) → ClamAV (optionnel)

**Type :** Antivirus

**Installation :** 📦 Gestionnaire de logiciels (si vraiment souhaité)

**Important :**
⚠️ **Linux n'a généralement PAS besoin d'antivirus**
- Architecture sécurisée
- Séparation des privilèges
- Très peu de malwares Linux

**Quand installer ClamAV :**
- Scanner des fichiers Windows (partage réseau)
- Vérifier pièces jointes email
- Serveur de fichiers

---

### CCleaner → BleachBit

**Type :** Nettoyage système

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
BleachBit nettoie fichiers inutiles et historiques.

✅ **Avantages :**
- Nettoyage cache navigateurs
- Fichiers temporaires
- Historiques
- Open source

⚠️ **À savoir :**
- Moins nécessaire sous Linux qu'Windows
- Pas de registre à nettoyer (n'existe pas)

**Nettoyage système natif :**
```bash
sudo apt autoremove  
sudo apt autoclean  
```

---

### TeamViewer → TeamViewer / Alternatives

**Type :** Accès à distance

**Installation :** 🌐 TeamViewer existe pour Linux

**Description :**
TeamViewer fonctionne sous Linux, mais des alternatives existent.

✅ **TeamViewer Linux :**
- Version officielle
- Compatible avec Windows

🔄 **Alternatives :**
- **AnyDesk** (🌐) : Similaire à TeamViewer
- **Remmina** (📦) : Client VNC/RDP/SSH intégré
- **RustDesk** (🌐) : Open source, auto-hébergeable

---

### Virtual CloneDrive → Montage automatique

**Type :** Montage d'images disque

**Installation :** ✨ Fonctionnalité native

**Description :**
Linux monte automatiquement les fichiers ISO.

✅ **Comment faire :**
- Clic droit sur fichier .iso
- "Ouvrir avec Gestionnaire d'archives" ou "Monter"
- L'image apparaît comme un lecteur

**Pas besoin de logiciel tiers !**

---

## 📹 Capture et streaming

### OBS Studio → OBS Studio

**Type :** Streaming et enregistrement d'écran

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
OBS existe sous Linux, identique à Windows !

✅ **Avantages :**
- Même logiciel que Windows
- Streaming Twitch, YouTube, etc.
- Enregistrement écran
- Scènes et sources

**Pour qui :** Streamers, créateurs de tutoriels, YouTubers

---

### Snipping Tool → Capture d'écran / Flameshot

**Type :** Capture d'écran

**Installation :** ✨ Préinstallé / 📦 Flameshot

**Outil préinstallé :**
- Touche Impr. écran = capture écran complet
- Maj + Impr. écran = sélection de zone

**Flameshot (recommandé) :**
- ✅ Annotations instantanées
- ✅ Flèches, texte, formes
- ✅ Upload automatique
- ✅ Très pratique

🔄 **Autres alternatives :**
- **Shutter** (📦) : Annotations et édition
- **Spectacle** (📦) : Capture KDE

---

## 🗂️ Gestion de fichiers avancée

### Total Commander → Krusader / Double Commander

**Type :** Gestionnaire de fichiers double panneau

**Installation :** 📦 Gestionnaire de logiciels

**Krusader :**
- ✅ Double panneau
- ✅ Très puissant
- ✅ Raccourcis clavier nombreux

**Double Commander :**
✅ Similaire à Total Commander  
✅ Multi-plateforme  
✅ Plugins

---

### Everything (recherche) → Catfish / fsearch

**Type :** Recherche rapide de fichiers

**Installation :** 📦 Gestionnaire de logiciels

**Catfish :**
- ✅ Interface simple
- ✅ Recherche rapide
- ✅ Filtres avancés

**fsearch :**
- ✅ Indexation rapide
- ✅ Similaire à Everything
- ✅ Résultats instantanés

---

## 💾 Sauvegarde et synchronisation

### Acronis / Backup Windows → Timeshift / Déjà Dup

**Type :** Sauvegarde

**Installation :** ✨ Timeshift préinstallé / 📦 Déjà Dup

**Timeshift :**
- ✅ Snapshots système (comme Restauration système Windows)
- ✅ Sauvegarde incrémentale
- ✅ Restauration facile

**Déjà Dup :**
- ✅ Sauvegarde données personnelles
- ✅ Chiffrement
- ✅ Planification

**Voir chapitre 17 (Sauvegarde et restauration) pour détails**

---

### Dropbox → Dropbox / Nextcloud / Syncthing

**Type :** Synchronisation cloud

**Installation :** 🌐 Dropbox Linux / 📦 Nextcloud/Syncthing

**Dropbox :**
- Client officiel Linux disponible

**Nextcloud :**
- ✅ Open source
- ✅ Auto-hébergeable
- ✅ Alternative complète

**Syncthing :**
- ✅ Sync peer-to-peer
- ✅ Pas de cloud central
- ✅ Totalement gratuit

**Voir chapitre 10 (Cloud et synchronisation) pour détails**

---

## 🖨️ PDF

### Adobe Acrobat Reader → Lecteur de documents / PDF Arranger

**Type :** Lecture et édition PDF

**Installation :** ✨ Lecteur préinstallé / 📦 PDF Arranger

**Lecteur de documents :**
- ✅ Lecture PDF
- ✅ Annotations basiques
- ✅ Léger et rapide

**PDF Arranger :**
- ✅ Fusionner PDF
- ✅ Diviser PDF
- ✅ Réorganiser pages

🔄 **Autres alternatives :**
- **Okular** (📦) : Lecteur avancé avec annotations
- **Master PDF Editor** (🌐) : Édition complète (version gratuite limitée)
- **LibreOffice Draw** : Édition PDF basique

---

## 🎓 Éducation et scientifique

### MATLAB → GNU Octave

**Type :** Calcul numérique

**Installation :** 📦 Gestionnaire de logiciels

**Description :**
Octave est compatible avec la syntaxe MATLAB.

✅ **Avantages :**
- Gratuit et open source
- Compatible scripts MATLAB (majoritairement)
- Interface graphique disponible

---

### Microsoft Visio → Dia / Draw.io

**Type :** Diagrammes et organigrammes

**Installation :** 📦 Dia / 🌐 Draw.io (web ou app)

**Dia :**
- ✅ Diagrammes techniques
- ✅ Nombreux modèles
- ✅ Export variés

**Draw.io :**
- ✅ Moderne et puissant
- ✅ Version web et desktop
- ✅ Intégration cloud

---

## 📊 Tableau récapitulatif par popularité

### Logiciels essentiels (usage quotidien)

| Windows | Linux Mint | Préinstallé | Difficulté |
|---------|-----------|-------------|------------|
| **Microsoft Word** | LibreOffice Writer | ✅ | ⭐ Facile |
| **Excel** | LibreOffice Calc | ✅ | ⭐ Facile |
| **PowerPoint** | LibreOffice Impress | ✅ | ⭐ Facile |
| **Edge/Chrome** | Firefox (ou Chrome) | ✅ | ⭐ Facile |
| **Outlook** | Thunderbird | ✅ | ⭐⭐ Moyen |
| **Windows Media Player** | VLC | ✅ | ⭐ Facile |
| **Photos** | Visionneuse d'images | ✅ | ⭐ Facile |
| **WinRAR** | Gestionnaire d'archives | ✅ | ⭐ Facile |

### Logiciels créatifs

| Windows | Linux Mint | Préinstallé | Difficulté |
|---------|-----------|-------------|------------|
| **Photoshop** | GIMP | ❌ | ⭐⭐⭐ Complexe |
| **Illustrator** | Inkscape | ❌ | ⭐⭐⭐ Complexe |
| **Premiere Pro** | Kdenlive | ❌ | ⭐⭐⭐ Complexe |
| **Lightroom** | Darktable | ❌ | ⭐⭐⭐ Complexe |
| **Paint** | Pinta | ❌ | ⭐ Facile |
| **Audacity** | Audacity | ❌ | ⭐⭐ Moyen |

---

## 💡 Conseils pour choisir vos alternatives

### Étape 1 : Identifiez vos besoins réels

Avant d'installer une alternative, demandez-vous :
- **Qu'est-ce que je fais vraiment avec ce logiciel ?**
- **Ai-je besoin de toutes ses fonctionnalités ?**
- **Puis-je utiliser une solution plus simple ?**

Exemple : Beaucoup utilisent Photoshop juste pour redimensionner des images. GIMP (ou même Pinta) suffit largement !

### Étape 2 : Testez progressivement

- **N'installez pas tout d'un coup**
- Commencez par les logiciels que vous utilisez le plus
- Testez plusieurs alternatives si la première ne convient pas
- Donnez-vous du temps pour vous adapter

### Étape 3 : Acceptez les différences

- L'alternative ne sera pas identique à votre logiciel Windows
- Cela ne signifie pas qu'elle est "moins bien"
- Parfois, elle est meilleure !
- La courbe d'apprentissage existe mais elle est temporaire

### Étape 4 : Utilisez les ressources

- **Tutoriels YouTube** : cherchez "[nom logiciel] tutorial Linux"
- **Documentation officielle** : souvent en anglais mais très complète
- **Forums** : la communauté Linux est accueillante
- **Ce guide** : revenez-y régulièrement

---

## 🚀 Plan d'action : par où commencer ?

### Semaine 1 : Les essentiels

Installez et testez ces logiciels en premier :
1. **Bureautique** : LibreOffice (déjà là)
2. **Navigation** : Firefox (déjà là)
3. **Multimédia** : VLC (déjà là)
4. **Email** : Thunderbird (déjà là)

**Objectif :** Vérifier que vous pouvez faire votre travail quotidien

### Semaine 2 : Les utilitaires

Ajoutez selon vos besoins :
1. **Capture d'écran** : Flameshot
2. **Nettoyage** : BleachBit
3. **Notes** : Joplin
4. **Messagerie** : Discord, Telegram

### Semaine 3 : Les logiciels spécialisés

Selon votre usage :
1. **Retouche photo** : GIMP ou Krita
2. **Montage vidéo** : Kdenlive ou OpenShot
3. **Gaming** : Steam
4. **Développement** : VS Code, Git

---

## ⚠️ Cas particuliers : logiciels sans alternative satisfaisante

Certains logiciels Windows n'ont pas d'équivalent Linux parfait :

### Logiciels très spécialisés

**Adobe Suite complète**
- Alternatives existent mais workflow différent
- **Solution** : Dual-boot ou VM Windows pour usage pro

**Microsoft Office (compatibilité 100%)**
- LibreOffice excellent mais pas 100% identique
- **Solution** : OnlyOffice meilleure compatibilité, ou Office 365 web

**AutoCAD**
- Pas d'alternative Linux native
- **Solution** : FreeCAD (différent), ou Wine, ou dual-boot

**Jeux avec anti-cheat invasif**
- Certains ne fonctionnent pas sous Linux
- **Solution** : Dual-boot pour gaming

### Solutions de contournement

1. **Dual-boot** : Gardez Windows pour ces logiciels spécifiques
2. **Machine virtuelle** : Windows dans VirtualBox (si pas trop gourmand)
3. **Wine/Bottles** : Faire tourner certains .exe sous Linux
4. **Version web** : Beaucoup de logiciels ont une version navigateur
5. **Cloud/Remote** : Accès à distance à un PC Windows

**Voir chapitres 15 (Applications Windows sous Linux) et 21 (Virtualisation)**

---

## 📝 Fiche mémo : mes logiciels essentiels

Créez votre propre liste de remplacement :

| Mon logiciel Windows | Alternative Linux | Installé ? | Testé ? | Adopté ? |
|---------------------|-------------------|-----------|---------|----------|
| Word | LibreOffice Writer | ✅ | ⬜ | ⬜ |
| Excel | LibreOffice Calc | ✅ | ⬜ | ⬜ |
| Chrome | Firefox/Chrome | ✅ | ⬜ | ⬜ |
| ... | ... | ... | ... | ... |

---

## Conclusion

La grande majorité des usages courants ont d'excellentes alternatives sous Linux Mint, souvent gratuites et parfois même meilleures que leurs équivalents Windows. La clé est de :

1. **Garder l'esprit ouvert** : différent ≠ moins bien
2. **Se donner du temps** : la courbe d'apprentissage est normale
3. **Tester plusieurs options** : choisissez ce qui VOUS convient
4. **Demander de l'aide** : la communauté est là

Pour les rares cas où aucune alternative satisfaisante n'existe, le dual-boot ou la virtualisation sont des solutions valables.

> 🎯 **Prochaine étape** : Le chapitre suivant vous montrera comment accéder à vos partitions Windows depuis Linux Mint pour récupérer des fichiers ou données oubliées.

---

## 🔗 Ressources utiles

**Sites de référence :**
- **AlternativeTo** (alternativeto.net) : Trouver des alternatives à n'importe quel logiciel
- **ProtonDB** (protondb.com) : Compatibilité jeux Windows sous Linux
- **WineHQ** (winehq.org) : Base de données compatibilité logiciels Windows

**Installer facilement :**
- Ouvrez le **Gestionnaire de logiciels**
- Tapez le nom du logiciel
- Cliquez sur **Installer**
- Entrez votre mot de passe
- C'est tout !

⏭️ [Accéder aux partitions Windows depuis Linux](/03-migration-depuis-windows/05-acceder-aux-partitions-windows-depuis-linux.md)
