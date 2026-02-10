🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.5 Visionneuse et retouche d'images

## Introduction

Linux Mint propose plusieurs outils pour visualiser et retoucher vos photos et images. De la simple visionneuse pour parcourir vos photos à des logiciels de retouche professionnels comme GIMP, vous avez tous les outils nécessaires pour gérer vos images, que vous soyez débutant ou utilisateur avancé.

## Visionneuses d'images

### Xviewer - La visionneuse par défaut

**Xviewer** (anciennement Eye of GNOME) est la visionneuse d'images installée par défaut sur Linux Mint Cinnamon.

#### Caractéristiques de Xviewer

- **Rapide et légère** : S'ouvre instantanément
- **Simple** : Interface épurée et intuitive
- **Formats supportés** : JPEG, PNG, GIF, BMP, TIFF, WebP, etc.
- **Diaporama** : Pour parcourir vos photos
- **Rotation basique** : Pivoter vos images
- **Zoom** : Agrandir les détails
- **EXIF** : Affichage des métadonnées (appareil photo, date, paramètres)

#### Lancer Xviewer

**Méthode 1 - Double-clic** :
1. Ouvrez le gestionnaire de fichiers (Nemo)
2. Naviguez vers vos photos
3. Double-cliquez sur une image
4. Xviewer s'ouvre

**Méthode 2 - Menu** :
1. Menu principal → **Graphisme** → **Visionneuse d'images**
2. Ou tapez "Xviewer" dans la recherche

**Méthode 3 - Clic droit** :
1. Clic droit sur une image
2. **Ouvrir avec** → **Visionneuse d'images**

#### Interface de Xviewer

**Barre d'outils** (en haut) :
- Précédent / Suivant
- Rotation gauche / droite
- Zoom +/-
- Ajuster à la fenêtre
- Taille réelle (1:1)
- Plein écran
- Menu principal

**Zone d'affichage** :
- Votre image au centre
- Fond gris ou damier (pour transparence)

**Barre d'état** (en bas, optionnelle) :
- Nom du fichier
- Dimensions (largeur × hauteur)
- Zoom actuel

#### Naviguer entre les images

**Flèches de navigation** :
- Cliquez sur **←** ou **→** dans la barre d'outils
- Ou utilisez les **flèches du clavier**
- Ou la **molette de la souris**

**Xviewer charge automatiquement** :
- Toutes les images du même dossier
- Navigation fluide sans fermer/rouvrir

#### Zoomer sur une image

**Zoom avant** :
- Cliquez sur **+** dans la barre d'outils
- Raccourci : `+` ou `Ctrl + Molette haut`
- Double-clic sur l'image

**Zoom arrière** :
- Cliquez sur **-**
- Raccourci : `-` ou `Ctrl + Molette bas`

**Taille réelle (100%)** :
- Bouton **1:1** dans la barre
- Raccourci : `1`

**Ajuster à la fenêtre** :
- Bouton **Ajuster**
- Raccourci : `F`
- L'image s'adapte à la taille de la fenêtre

**Navigation dans le zoom** :
- Cliquez et glissez l'image
- Ou utilisez les barres de défilement

#### Rotation des images

**Pivoter** :
1. Cliquez sur les icônes de rotation dans la barre
2. **Rotation gauche** : Raccourci `Ctrl + R` (ou `[`)
3. **Rotation droite** : Raccourci `Ctrl + Maj + R` (ou `]`)

**Attention** :
- Xviewer tourne uniquement l'affichage
- Pour sauvegarder la rotation, utilisez un éditeur

#### Diaporama

**Lancer un diaporama** :
1. Ouvrez une image dans un dossier
2. Menu **Vue** → **Diaporama**
3. Raccourci : `F5`

**Pendant le diaporama** :
- Les images défilent automatiquement
- `Espace` : Pause
- `←` / `→` : Image précédente/suivante
- `Échap` : Quitter le diaporama

**Configurer** :
- Menu **Édition** → **Préférences** → **Diaporama**
- Durée d'affichage (secondes)
- Boucle (revenir au début)

#### Plein écran

**Activer** :
- Bouton **Plein écran**
- Raccourci : `F11`
- Double-clic sur l'image

**En mode plein écran** :
- Bougez la souris pour afficher les contrôles
- `F11` ou `Échap` pour quitter

#### Afficher les informations EXIF

Les **métadonnées EXIF** contiennent des informations sur la photo :

1. Menu **Image** → **Propriétés**
2. Ou raccourci : `Alt + Entrée`
3. Onglet **Détails** :
   - Appareil photo / Smartphone
   - Date et heure de prise
   - Paramètres (ISO, ouverture, vitesse)
   - Géolocalisation (si disponible)
   - Dimensions et taille

**Utile pour** :
- Vérifier les réglages utilisés
- Savoir quand une photo a été prise
- Connaître les coordonnées GPS

#### Définir comme fond d'écran

**Depuis Xviewer** :
1. Ouvrez l'image souhaitée
2. Menu **Image** → **Définir comme fond d'écran**
3. L'image devient immédiatement votre fond d'écran

**Options de disposition** :
- Ajustez ensuite : Clic droit sur bureau → **Changer le fond d'écran**
- Centré, Étiré, Mosaïque, Zoom, Étendu

#### Copier/Coller une image

**Copier dans le presse-papiers** :
1. Menu **Édition** → **Copier l'image**
2. Raccourci : `Ctrl + C`
3. Collez ensuite dans une application (LibreOffice, GIMP, etc.)

### Autres visionneuses disponibles

#### gThumb

**Caractéristiques** :
- Visionneuse avec organisation
- Édition basique intégrée
- Gestion de catalogues
- Import depuis appareil photo

**Installation** :
```bash
sudo apt install gthumb
```

**Quand l'utiliser** :
- Vous voulez organiser vos photos
- Retouches basiques rapides

#### Gwenview (KDE)

**Caractéristiques** :
- Visionneuse KDE
- Interface moderne
- Édition basique
- Comparaison d'images

**Installation** :
```bash
sudo apt install gwenview
```

#### Nomacs

**Caractéristiques** :
- Multi-plateforme
- Comparaison côte à côte
- Histogrammes
- Interface personnalisable

**Installation** :
```bash
sudo apt install nomacs
```

## Retouche d'images basique

### Outils de retouche rapide

Pour des modifications simples, pas besoin de GIMP :

#### ImageMagick (ligne de commande)

Outil puissant en ligne de commande pour batch processing.

**Installation** :
```bash
sudo apt install imagemagick
```

**Exemples d'usage** :

**Redimensionner** :
```bash
convert photo.jpg -resize 800x600 photo-petite.jpg
```

**Rotation** :
```bash
convert photo.jpg -rotate 90 photo-tournee.jpg
```

**Conversion de format** :
```bash
convert image.png image.jpg
```

**Appliquer un effet** :
```bash
convert photo.jpg -sepia-tone 80% photo-sepia.jpg
```

**Traiter plusieurs fichiers** :
```bash
for i in *.jpg; do convert "$i" -resize 50% "small-$i"; done
```

#### Pinta - Retouche simple avec interface

**Pinta** est une alternative simple à Paint.NET ou MS Paint.

**Installation** :
```bash
sudo apt install pinta
```

**Caractéristiques** :
- Interface intuitive
- Calques
- Outils de dessin basiques
- Effets et ajustements
- Idéal pour débutants

**Fonctionnalités** :
- Recadrage
- Redimensionnement
- Rotation et retournement
- Ajustements (luminosité, contraste, saturation)
- Effets (flou, netteté, peinture à l'huile)
- Texte
- Formes (rectangles, cercles, flèches)
- Sélections et découpage

**Utilisation de Pinta** :

1. Lancez Pinta : Menu → **Graphisme** → **Pinta**
2. **Fichier** → **Ouvrir** votre image
3. Utilisez les outils dans la barre de gauche
4. **Ajustements** et **Effets** dans les menus
5. **Fichier** → **Enregistrer** ou **Exporter**

## GIMP - Retouche d'images professionnelle

**GIMP** (GNU Image Manipulation Program) est l'équivalent libre et gratuit de Adobe Photoshop.

### Présentation de GIMP

**Caractéristiques** :
- **Gratuit et open source**
- **Professionnel** : Utilisé par des graphistes
- **Calques** : Travail non destructif
- **Retouche photo** : Couleurs, exposition, détails
- **Création graphique** : Logo, web design, affiches
- **Formats** : PSD (Photoshop), XCF (natif), tous les formats courants
- **Extensions** : Plugins et scripts

**Limitations par rapport à Photoshop** :
- Interface moins intuitive au début
- Certaines fonctionnalités avancées manquantes
- CMJN limité (pour impression professionnelle)

**Mais** : Pour 95% des utilisateurs, GIMP est largement suffisant !

### Installation de GIMP

GIMP est généralement préinstallé sur Linux Mint. Sinon :

```bash
sudo apt install gimp
```

**Version Flatpak** (plus récente) :
```bash
flatpak install flathub org.gimp.GIMP
```

### Lancer GIMP

1. Menu principal → **Graphisme** → **GIMP**
2. Ou tapez "GIMP" dans la recherche
3. Au premier lancement, GIMP configure son environnement (quelques secondes)

### Interface de GIMP

Au premier lancement, l'interface peut sembler complexe :

**Fenêtre principale (centre)** :
- Zone de travail
- Votre image s'affiche ici

**Boîte à outils (gauche)** :
- Outils de sélection
- Outils de peinture
- Outils de transformation
- Options de l'outil sélectionné en bas

**Panneaux (droite)** :
- Calques, Canaux, Chemins
- Brosses, Motifs, Dégradés
- Historique d'annulation

**Barre de menus** :
- Fichier, Édition, Sélection, Image, Calque, Couleurs, Outils, Filtres, etc.

**Mode fenêtre unique** :
- Par défaut, GIMP utilise une seule fenêtre (plus facile)
- Si ce n'est pas le cas : **Fenêtres** → **Mode fenêtre unique**

### Ouvrir et créer des images

**Ouvrir une image** :
1. **Fichier** → **Ouvrir**
2. Raccourci : `Ctrl + O`
3. Parcourez et sélectionnez
4. Cliquez sur **Ouvrir**

**Créer une nouvelle image** :
1. **Fichier** → **Nouvelle image**
2. Raccourci : `Ctrl + N`
3. Définissez :
   - Largeur et hauteur (pixels)
   - Résolution (72 dpi pour écran, 300 dpi pour impression)
   - Mode couleur (RVB pour écran)
4. Cliquez sur **Valider**

**Ouvrir depuis le presse-papiers** :
1. Copiez une image ailleurs (navigateur, capture d'écran)
2. GIMP → **Fichier** → **Créer** → **Depuis le presse-papiers**
3. L'image s'ouvre comme nouveau document

### Concepts de base GIMP

#### Les calques

Les **calques** sont comme des feuilles transparentes empilées :
- Chaque élément peut être sur un calque différent
- Modifiez un calque sans affecter les autres
- Changez l'ordre, l'opacité, le mode de fusion

**Panneau Calques** :
- À droite par défaut
- Liste tous vos calques
- Le calque actif est surligné

**Créer un calque** :
1. Cliquez sur l'icône **+** en bas du panneau Calques
2. Ou **Calque** → **Nouveau calque**
3. Nommez-le et validez

**Dupliquer un calque** :
1. Clic droit sur le calque → **Dupliquer le calque**
2. Utile pour essayer des modifications sans perdre l'original

**Supprimer un calque** :
- Clic droit → **Supprimer le calque**
- Ou sélectionnez et cliquez sur l'icône **poubelle**

**Ordre des calques** :
- Glissez-déposez pour réorganiser
- Le calque du haut apparaît devant

#### Les sélections

Les **sélections** définissent la zone sur laquelle vous travaillez.

**Outils de sélection** (barre d'outils) :
- **Rectangle** : Sélection rectangulaire
- **Ellipse** : Sélection circulaire/ovale
- **Libre** : Tracé à main levée
- **Contiguë** : Baguette magique (sélection par couleur)
- **Par couleur** : Sélectionne toutes les zones de même couleur
- **Ciseaux intelligents** : Sélection semi-automatique par contours

**Créer une sélection** :
1. Choisissez un outil de sélection
2. Cliquez et glissez sur l'image
3. Une zone pointillée "fourmis marchantes" apparaît

**Modifier une sélection** :
- **Ajouter** : Maintenez `Maj` et sélectionnez
- **Soustraire** : Maintenez `Ctrl` et sélectionnez
- **Intersection** : `Maj + Ctrl`

**Inverser la sélection** :
- **Sélection** → **Inverser**
- Raccourci : `Ctrl + I`

**Désélectionner** :
- **Sélection** → **Aucune**
- Raccourci : `Maj + Ctrl + A`

#### L'historique d'annulation

GIMP garde un historique de vos actions :

**Annuler** :
- **Édition** → **Annuler**
- Raccourci : `Ctrl + Z`

**Rétablir** :
- **Édition** → **Rétablir**
- Raccourci : `Ctrl + Y`

**Panneau Historique** :
- Affiche toutes les étapes
- Cliquez sur une étape pour revenir à ce moment
- Par défaut : 20 niveaux d'annulation (configurable)

### Retouches basiques avec GIMP

#### Recadrer une image

**Outil de recadrage** :
1. Sélectionnez l'outil **Recadrage** dans la boîte à outils
2. Raccourci : `Maj + C`
3. Cliquez et glissez pour définir la zone à garder
4. Ajustez les coins et bords
5. Appuyez sur `Entrée` ou double-clic à l'intérieur pour valider

**Options** :
- **Fixe** : Ratio fixe (carré, 16:9, etc.)
- **Tiers de règle** : Affiche des lignes pour composition
- **Centre** : Point de focus

#### Redimensionner une image

**Changer la taille** :
1. **Image** → **Échelle et taille de l'image**
2. Entrez les nouvelles dimensions
3. Icône **chaîne** : Lie largeur et hauteur (garde le ratio)
4. Interpolation : **Cubique** (meilleure qualité)
5. Cliquez sur **Échelle**

**Attention** :
- Agrandir dégrade la qualité
- Réduire préserve la qualité

**Taille du canevas** :
- **Image** → **Taille du canevas**
- Change la taille de travail sans redimensionner l'image
- Utile pour ajouter de l'espace autour

#### Rotation et retournement

**Rotation** :
1. **Image** → **Transformation** → **Rotation**
2. Choisissez : 90° horaire, 90° anti-horaire, 180°

**Rotation libre** :
1. Outil **Rotation** dans la boîte à outils
2. Raccourci : `Maj + R`
3. Cliquez sur l'image
4. Ajustez l'angle
5. Cliquez sur **Rotation**

**Retournement** :
- **Image** → **Transformation** → **Retournement horizontal/vertical**

#### Ajustements de couleurs

**Luminosité et contraste** :
1. **Couleurs** → **Luminosité-Contraste**
2. Ajustez les curseurs
3. Aperçu en direct
4. Cliquez sur **Valider**

**Teinte et saturation** :
1. **Couleurs** → **Teinte-Saturation**
2. Ajustez :
   - **Teinte** : Change les couleurs
   - **Saturation** : Intensité des couleurs
   - **Luminosité** : Clarté

**Courbes** (avancé) :
1. **Couleurs** → **Courbes**
2. Ajustez la courbe pour contrôler tons clairs, moyens, foncés
3. Très puissant pour correction colorimétrique

**Niveaux** :
1. **Couleurs** → **Niveaux**
2. Ajustez les points noir, gris, blanc
3. Améliore le contraste

**Balance des couleurs** :
1. **Couleurs** → **Balance des couleurs**
2. Corrigez les dominantes de couleur
3. Ajustez séparément ombres, tons moyens, hautes lumières

**Auto** :
- **Couleurs** → **Auto** → **Normaliser** : Ajustement automatique
- **Balance des blancs** : Correction température couleur

#### Convertir en noir et blanc

**Méthode simple** :
1. **Image** → **Mode** → **Niveaux de gris**
2. Désaturation directe

**Méthode avancée** (meilleur contrôle) :
1. **Couleurs** → **Désaturation** → **Désaturer**
2. Choisissez la méthode :
   - **Luminosité** : Plus naturel
   - **Luminance** : Précis
   - **Moyenne** : Simple

**Noir et blanc artistique** :
1. Gardez l'image en RVB
2. **Couleurs** → **Désaturation**
3. Ajustez ensuite avec **Courbes** pour contraste dramatique

#### Netteté et flou

**Renforcer la netteté** :
1. **Filtres** → **Amélioration** → **Renforcer la netteté**
2. Ajustez le rayon et la quantité
3. Attention à ne pas exagérer (bruit visible)

**Netteté non destructive** :
1. Dupliquez le calque
2. **Filtres** → **Amélioration** → **Renforcer la netteté (masque flou)**
3. Ajustez l'opacité du calque pour doser

**Flou** :
- **Filtres** → **Flou** → **Flou gaussien**
- Ajustez le rayon
- Utile pour arrière-plans, effets artistiques

#### Réduction du bruit

Pour les photos prises en basse lumière (grain, bruit) :

1. **Filtres** → **Amélioration** → **Réduction du bruit**
2. Ajustez les paramètres
3. Prévisualisez avant de valider

#### Supprimer les yeux rouges

**Outil yeux rouges** :
1. Zoomez sur les yeux
2. Sélectionnez l'outil **Suppression des yeux rouges**
3. Cliquez et glissez sur chaque œil rouge
4. GIMP corrige automatiquement

### Retouche photo avancée

#### Outil clonage (tampon)

Pour supprimer des éléments indésirables :

1. Sélectionnez l'outil **Cloner**
2. Raccourci : `C`
3. **Ctrl + clic** sur une zone source (texture similaire)
4. Peignez sur la zone à masquer
5. La zone source est copiée

**Utilité** :
- Supprimer une personne d'une photo
- Effacer un poteau, un fil électrique
- Masquer des imperfections

#### Outil correcteur

Similaire au clonage mais s'adapte mieux :

1. Outil **Correcteur**
2. **Ctrl + clic** sur une zone source
3. Peignez sur la zone à corriger
4. GIMP mélange automatiquement

**Meilleur pour** :
- Retouche de peau
- Suppression de boutons, rides
- Corrections subtiles

#### Dodge et Burn (éclaircir/assombrir)

Technique photo classique :

**Éclaircir** :
1. Outil **Éclaircir/Assombrir**
2. Mode **Éclaircir** (bouton en haut)
3. Peignez sur les zones à éclaircir

**Assombrir** :
1. Même outil
2. Mode **Assombrir**
3. Peignez sur les zones à assombrir

**Utilité** :
- Ajouter de la profondeur
- Mettre en valeur certains éléments
- Corriger l'exposition localement

#### Détourage (séparer sujet et fond)

**Extraction de premier plan** :
1. **Outils** → **Sélection** → **Extraction du premier plan**
2. Tracez grossièrement autour du sujet
3. Fermez le tracé
4. Appuyez sur `Entrée`
5. Peignez à l'intérieur du sujet
6. Appuyez à nouveau sur `Entrée`
7. GIMP sépare le sujet du fond

**Utilité** :
- Changer l'arrière-plan
- Isoler un objet
- Créer des compositions

### Texte et graphisme

#### Ajouter du texte

1. Sélectionnez l'outil **Texte**
2. Raccourci : `T`
3. Cliquez sur l'image
4. Tapez votre texte
5. Ajustez dans l'éditeur de texte :
   - **Police** : Type de caractère
   - **Taille** : En pixels
   - **Couleur** : Cliquez sur le carré de couleur
   - **Gras, Italique**

**Modifier le texte** :
- L'outil Texte reste actif
- Cliquez à nouveau pour éditer
- Le texte est sur son propre calque

**Effets de texte** :
1. Clic droit sur le calque de texte → **Alpha vers sélection**
2. Créez un nouveau calque
3. Remplissez la sélection avec dégradé, motif, etc.
4. Appliquez des filtres (**Filtres** → **Ombre et lumière** → **Ombre portée**)

#### Formes et dessins

**Outils de dessin** :
- **Pinceau** : Dessin à main levée
- **Crayon** : Bords nets
- **Aérographe** : Vaporisation progressive
- **Gomme** : Effacer
- **Pot de peinture** : Remplir une zone

**Formes géométriques** :
1. Utilisez les outils de sélection (rectangle, ellipse)
2. Créez une sélection
3. **Édition** → **Tracer la sélection**
4. Choisissez : Trait ou remplissage

**Options des brosses** :
- Taille : Diamètre du pinceau
- Dureté : Bords nets ou doux
- Opacité : Transparence
- Forme : Ronde, carrée, personnalisée

### Enregistrer votre travail

#### Format natif XCF

**Enregistrer en XCF** (conserve calques, historique) :
1. **Fichier** → **Enregistrer sous**
2. Raccourci : `Maj + Ctrl + S`
3. Format : `.xcf` (natif GIMP)
4. Nommez et enregistrez

**À faire** :
- Toujours sauvegarder en XCF pendant le travail
- Vous pourrez modifier plus tard

#### Exporter pour utilisation

Pour partager ou utiliser votre image :

1. **Fichier** → **Exporter sous**
2. Raccourci : `Maj + Ctrl + E`
3. Choisissez le format :
   - **JPEG** (.jpg) : Photos, petite taille, perte
   - **PNG** (.png) : Transparence, sans perte, graphisme
   - **GIF** (.gif) : Animations, peu de couleurs
   - **TIFF** (.tif) : Professionnel, sans perte
4. Nommez votre fichier avec l'extension
5. Cliquez sur **Exporter**

**Options JPEG** :
- **Qualité** : 85-95% (bon compromis)
- Plus bas = fichier plus petit mais qualité moindre

**Options PNG** :
- **Niveau de compression** : 9 (maximum, sans perte)

### Filtres et effets

GIMP propose des centaines de filtres :

**Accès** : Menu **Filtres**

**Catégories** :

**Flou** :
- Flou gaussien, flou de mouvement, flou radial

**Amélioration** :
- Netteté, réduction du bruit, suppression des yeux rouges

**Distorsions** :
- Ondulation, tourbillon, lentille, relief

**Ombres et lumière** :
- Ombre portée, lens flare, lueur douce

**Artistiques** :
- Peinture à l'huile, bande dessinée, cubisme

**Décoration** :
- Bordure, arrondir les coins, ancien photographe

**Rendu** :
- Nuages, plasma, fractales, grilles

**Utilité** :
- Effets créatifs
- Corrections
- Graphisme web

**Conseil** : Expérimentez ! Les filtres ont un aperçu en direct.

### Raccourcis clavier GIMP essentiels

| Raccourci | Action |
|-----------|--------|
| `Ctrl + N` | Nouvelle image |
| `Ctrl + O` | Ouvrir |
| `Ctrl + S` | Enregistrer (XCF) |
| `Maj + Ctrl + E` | Exporter |
| `Ctrl + Z` | Annuler |
| `Ctrl + Y` | Rétablir |
| `Ctrl + C` | Copier |
| `Ctrl + V` | Coller |
| `Ctrl + A` | Tout sélectionner |
| `Maj + Ctrl + A` | Désélectionner |
| `Ctrl + I` | Inverser sélection |
| `Ctrl + L` | Niveaux |
| `Ctrl + M` | Courbes |
| `R` | Rectangle de sélection |
| `E` | Ellipse de sélection |
| `U` | Sélection floue (baguette) |
| `Maj + O` | Sélection par couleur |
| `C` | Cloner |
| `P` | Pinceau |
| `Maj + P` | Crayon |
| `T` | Texte |
| `M` | Déplacer |
| `Maj + C` | Recadrer |
| `Maj + R` | Rotation |
| `Maj + T` | Mise à l'échelle |
| `F11` | Plein écran |

### Tutoriels et apprentissage

**Ressources pour apprendre GIMP** :

**Officielles** :
- Documentation GIMP : [https://docs.gimp.org/](https://docs.gimp.org/)
- Tutoriels officiels

**YouTube** :
- "GIMP tutoriel français" : Nombreuses vidéos
- Chaînes spécialisées : TutoGIMP, etc.

**Livres gratuits** :
- "Débuter avec GIMP" (ebook gratuit)

**Pratique** :
- Le meilleur apprentissage : Expérimenter !
- Essayez tous les outils
- Suivez des tutoriels pas à pas

## Autres outils de création graphique

### Krita - Dessin et peinture numérique

**Krita** est spécialisé dans le dessin artistique et la peinture numérique.

**Installation** :
```bash
sudo apt install krita
```

**Caractéristiques** :
- **Orientation artiste** : Illustration, concept art, BD
- **Brosses avancées** : Très nombreuses et personnalisables
- **Tablette graphique** : Support excellent
- **Animation** : Création d'animations 2D
- **Stabilisateur de brosse** : Lisse les traits
- **Calques et masques** : Workflow professionnel

**Quand utiliser Krita** :
- Dessin digital (manga, BD, illustration)
- Concept art pour jeux vidéo
- Peinture numérique
- Animation 2D

**Différence avec GIMP** :
- Krita : Création artistique de zéro
- GIMP : Retouche photo et graphisme

### Inkscape - Dessin vectoriel

**Inkscape** est l'équivalent libre d'Adobe Illustrator.

**Installation** :
```bash
sudo apt install inkscape
```

**Caractéristiques** :
- **Dessin vectoriel** : Images qui s'agrandissent sans perte
- **Logos** : Design professionnel
- **Icônes** : Pour applications et sites web
- **Infographies** : Schémas, diagrammes
- **Format SVG** : Standard du web

**Images vectorielles vs matricielles** :

**Matriciel** (bitmap) :
- JPEG, PNG : Pixels
- Taille fixe, perte de qualité si agrandi
- Photos, images complexes

**Vectoriel** :
- SVG, AI : Formules mathématiques
- Redimensionnable à l'infini sans perte
- Logos, icônes, dessins techniques

**Quand utiliser Inkscape** :
- Créer un logo
- Dessiner des icônes
- Affiches, flyers
- Schémas et diagrammes
- Tout ce qui doit être redimensionnable

### Darktable - Développement RAW

**Darktable** est un logiciel de développement photo professionnel.

**Installation** :
```bash
sudo apt install darktable
```

**Caractéristiques** :
- **Fichiers RAW** : Traite les fichiers bruts des appareils photo
- **Non destructif** : Modifications sans altérer l'original
- **Corrections avancées** : Exposition, bruit, aberrations
- **Gestion de bibliothèque** : Organise vos photos
- **Alternative à** : Adobe Lightroom

**Format RAW** :
- Fichiers bruts du capteur (CR2, NEF, ARW, DNG, etc.)
- Plus de latitude pour corrections
- Nécessite traitement avant utilisation

**Quand utiliser Darktable** :
- Vous photographiez en RAW
- Retouche photo sérieuse
- Workflow photographique complet

## Gestion et organisation de photos

### Shotwell - Gestionnaire de photos

**Shotwell** est un organisateur de photos simple et efficace.

**Installation** :
```bash
sudo apt install shotwell
```

**Caractéristiques** :
- **Importation** : Depuis appareil photo, carte SD
- **Organisation** : Par événements, tags, dates
- **Édition basique** : Recadrage, rotation, ajustements
- **Partage** : Export vers Flickr, Facebook, etc.
- **Diaporamas** : Visualisation

**Workflow typique** :
1. Importez vos photos depuis l'appareil
2. Organisez par événements/albums
3. Ajoutez des tags (vacances, famille, etc.)
4. Retouches basiques
5. Exportez ou partagez

### digiKam - Gestion avancée

**digiKam** est une solution professionnelle de gestion photo.

**Installation** :
```bash
sudo apt install digikam
```

**Caractéristiques** :
- **Bibliothèque** : Gestion de milliers de photos
- **Métadonnées** : EXIF, IPTC, XMP
- **Recherche avancée** : Par date, lieu, personne, tag
- **Retouche** : Outils intégrés
- **Géolocalisation** : Cartes
- **Reconnaissance faciale** : Identifie automatiquement les personnes

**Quand utiliser digiKam** :
- Grande collection de photos (> 1000)
- Besoin d'organisation professionnelle
- Métadonnées importantes

## Formats d'images expliqués

### JPEG (.jpg, .jpeg)

**Caractéristiques** :
- **Compression avec perte** : Petite taille mais qualité réduite
- **16 millions de couleurs**
- **Pas de transparence**

**Utilisation** :
- Photos
- Web (images)
- Email (pièces jointes)

**Avantages** :
- Fichiers légers
- Universel

**Inconvénients** :
- Perte de qualité à chaque enregistrement
- Pas de transparence

### PNG (.png)

**Caractéristiques** :
- **Compression sans perte** : Qualité préservée
- **Transparence** : Canal alpha
- **16 millions de couleurs**

**Utilisation** :
- Graphisme web
- Logos avec transparence
- Captures d'écran
- Images nécessitant qualité

**Avantages** :
- Aucune perte
- Transparence

**Inconvénients** :
- Fichiers plus gros que JPEG

### GIF (.gif)

**Caractéristiques** :
- **256 couleurs maximum**
- **Transparence** : Oui/Non (pas d'opacité partielle)
- **Animation** : Plusieurs images

**Utilisation** :
- Animations simples
- Mèmes
- Emojis animés

**Avantages** :
- Animations
- Petits fichiers pour dessins simples

**Inconvénients** :
- Limité en couleurs
- Qualité photo médiocre

### WebP (.webp)

**Caractéristiques** :
- **Moderne** : Développé par Google
- **Compression efficace** : Mieux que JPEG et PNG
- **Transparence** : Supportée

**Utilisation** :
- Web moderne
- Remplacement de JPEG/PNG

**Avantages** :
- Fichiers plus petits
- Qualité équivalente

**Inconvénients** :
- Moins universel (mais de plus en plus supporté)

### TIFF (.tif, .tiff)

**Caractéristiques** :
- **Professionnel** : Impression
- **Sans perte** ou avec compression
- **Calques** : Supportés

**Utilisation** :
- Impression professionnelle
- Archivage
- Édition multi-passes

**Avantages** :
- Qualité maximale
- Professionnel

**Inconvénients** :
- Fichiers très gros
- Pas pour le web

### SVG (.svg)

**Caractéristiques** :
- **Vectoriel** : Mathématique, pas de pixels
- **Redimensionnable** : À l'infini sans perte
- **Texte** : Format XML

**Utilisation** :
- Logos
- Icônes
- Graphiques web
- Illustrations

**Avantages** :
- Taille indépendante
- Modifiable avec éditeur de texte
- Petits fichiers

**Inconvénients** :
- Pas adapté aux photos

### RAW (CR2, NEF, ARW, DNG, etc.)

**Caractéristiques** :
- **Format brut** : Données du capteur
- **Propriétaire** : Différent par marque
- **Nécessite traitement**

**Utilisation** :
- Photographie sérieuse
- Post-traitement avancé

**Avantages** :
- Maximum de données
- Latitude de correction

**Inconvénients** :
- Fichiers énormes
- Nécessite logiciel spécialisé (Darktable, RawTherapee)

### Choisir le bon format

**Pour le web** :
- Photos : **JPEG** (qualité 80-90%)
- Graphiques avec transparence : **PNG**
- Logos : **SVG** ou **PNG**
- Animations : **GIF** ou **WebP**

**Pour l'impression** :
- Haute qualité : **TIFF** ou **PNG**
- Photo standard : **JPEG** (qualité 95-100%)

**Pour l'édition** :
- GIMP : **XCF**
- Photoshop : **PSD**
- Vectoriel : **SVG**

**Pour le partage** :
- Email : **JPEG** (taille réduite)
- Réseaux sociaux : **JPEG** ou **PNG**

## Optimisation et compression d'images

### Réduire la taille des fichiers

**Pourquoi** :
- Accélérer le chargement web
- Économiser l'espace disque
- Faciliter le partage

#### Avec GIMP

1. **Fichier** → **Exporter sous**
2. Choisissez JPEG
3. Ajustez la qualité : 75-85% (bon compromis)
4. **Options** → **Optimiser** et **Progressif**
5. Exportez

#### Avec ImageMagick

**Redimensionner et compresser** :
```bash
convert grande-image.jpg -resize 1920x1080 -quality 85 petite-image.jpg
```

**Batch (plusieurs fichiers)** :
```bash
for i in *.jpg; do convert "$i" -resize 1920x1080 -quality 85 "optimized-$i"; done
```

#### Avec des outils dédiés

**Trimage** :
```bash
sudo apt install trimage
```
- Compresse PNG et JPEG sans perte visible
- Interface simple

**OptiPNG** et **JPEGoptim** :
```bash
sudo apt install optipng jpegoptim
```

**Usage** :
```bash
optipng image.png  # Optimise PNG  
jpegoptim --max=85 photo.jpg  # Optimise JPEG  
```

### Services en ligne

**TinyPNG** : [https://tinypng.com/](https://tinypng.com/)
- Compresse PNG et JPEG
- Excellents résultats

**Squoosh** : [https://squoosh.app/](https://squoosh.app/)
- Application web Google
- Comparaison avant/après
- Nombreux formats

## Captures d'écran

### Outil de capture intégré

Linux Mint a un outil de capture par défaut.

**Prendre une capture** :
- **Impr écran** (Print Screen) : Tout l'écran
- **Alt + Impr écran** : Fenêtre active
- **Maj + Impr écran** : Sélection à la souris

**Où sont enregistrées** :
- Par défaut : `~/Images/` ou `~/Pictures/`
- Nom : Screenshot-YYYY-MM-DD-HH-MM-SS.png

### Flameshot - Outil avancé

**Flameshot** offre plus de fonctionnalités.

**Installation** :
```bash
sudo apt install flameshot
```

**Utilisation** :
```bash
flameshot gui  # Interface de sélection
```

**Fonctionnalités** :
- Annotations (flèches, texte, formes)
- Pixellisation (cacher infos sensibles)
- Copie directe dans le presse-papiers
- Upload vers Imgur

**Configurer comme raccourci** :
1. Paramètres système → **Clavier** → **Raccourcis**
2. Ajoutez un raccourci personnalisé
3. Commande : `flameshot gui`
4. Raccourci : `Impr écran`

### Shutter (outil complet)

**Shutter** est très complet mais plus lourd.

**Installation** :
```bash
sudo apt install shutter
```

**Fonctionnalités** :
- Captures avancées
- Édition intégrée
- Annotations
- Upload vers multiples services

## Astuces et bonnes pratiques

### Organisation des fichiers

**Structure recommandée** :
```
~/Images/
  ├── 2024/
  │   ├── 01-Janvier/
  │   ├── 02-Février/
  │   └── ...
  ├── Vacances/
  ├── Famille/
  └── Screenshots/
```

**Nommage** :
- Évitez les espaces : `photo_plage.jpg` plutôt que `photo plage.jpg`
- Dates : `2024-03-15-paysage.jpg`
- Descriptif : `anniversaire-marie-2024.jpg`

### Sauvegardes

**Règle 3-2-1** :
- **3** copies de vos photos
- Sur **2** supports différents (disque dur, SSD)
- **1** copie hors site (cloud, disque externe ailleurs)

**Solutions cloud** :
- Google Photos (gratuit limité)
- Nextcloud (auto-hébergé)
- Mega, pCloud, etc.

### Métadonnées et EXIF

**Préserver les métadonnées** :
- Évitez de réenregistrer en JPEG (perte)
- Utilisez des outils qui préservent EXIF

**Supprimer les métadonnées** (vie privée) :
```bash
sudo apt install exiftool  
exiftool -all= photo.jpg  # Supprime toutes les métadonnées  
```

**Ou avec GIMP** :
- Lors de l'export JPEG → Décochez "Enregistrer les données EXIF"

### Formats et workflow

**Workflow photo** :
1. **Import** : RAW depuis l'appareil
2. **Tri** : Sélectionner les bonnes photos
3. **Développement** : Darktable (RAW → JPEG/TIFF)
4. **Retouche** : GIMP si nécessaire
5. **Export** : JPEG pour partage
6. **Archivage** : RAW + XCF/PSD conservés

**Sauvegardez les originaux** :
- Ne modifiez jamais directement l'original
- Travaillez sur une copie
- Ou utilisez des formats non destructifs (XCF, RAW)

### Performances GIMP

**Améliorer la vitesse** :
1. **Édition** → **Préférences** → **Système**
2. Augmentez la mémoire cache
3. Activez l'accélération matérielle (OpenCL)

**Pour gros fichiers** :
- Travaillez en résolution réduite
- Agrandissez seulement à la fin

## Ressources et liens utiles

### Documentation officielle

**GIMP** :
- [https://www.gimp.org/](https://www.gimp.org/)
- Docs : [https://docs.gimp.org/](https://docs.gimp.org/)

**Inkscape** :
- [https://inkscape.org/](https://inkscape.org/)

**Krita** :
- [https://krita.org/](https://krita.org/)

### Communauté

- Forums GIMP francophones
- Reddit : r/GIMP
- Forum Linux Mint

### Tutoriels

- YouTube : "GIMP tutoriel français"
- GIMPons.fr : Tutoriels français
- Tuto.com : Formations (payantes)

### Ressources graphiques gratuites

**Brosses GIMP** :
- DeviantArt : Brushes section
- GIMP-FR : Ressources

**Polices** :
- Google Fonts : [https://fonts.google.com/](https://fonts.google.com/)
- DaFont : [https://www.dafont.com/](https://www.dafont.com/)

**Images libres** :
- Unsplash : [https://unsplash.com/](https://unsplash.com/)
- Pexels : [https://www.pexels.com/](https://www.pexels.com/)
- Pixabay : [https://pixabay.com/](https://pixabay.com/)

## Conclusion

Linux Mint offre une panoplie complète d'outils pour la visualisation et la retouche d'images, adaptés à tous les niveaux. De la simple visionneuse Xviewer pour parcourir vos photos, à GIMP pour des retouches professionnelles, en passant par Krita pour le dessin artistique et Inkscape pour le design vectoriel, vous avez tout ce qu'il faut pour créer et éditer vos images.

**Points clés à retenir** :

- **Xviewer** : Visionneuse rapide et simple
- **Pinta** : Retouches basiques accessibles
- **GIMP** : Retouche professionnelle complète (alternative à Photoshop)
- **Krita** : Dessin et peinture numérique
- **Inkscape** : Design vectoriel (logos, icônes)
- **Formats** : JPEG pour photos, PNG pour transparence, SVG pour vectoriel

N'hésitez pas à expérimenter avec ces outils, suivre des tutoriels et pratiquer régulièrement. La retouche d'images est un domaine créatif où la pratique fait la différence. Commencez par des modifications simples (recadrage, luminosité) et progressez graduellement vers des techniques plus avancées.

---


⏭️ [Gestionnaire d'archives](/05-applications-essentielles-et-outils-mint/06-gestionnaire-darchives.md)
