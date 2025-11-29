🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 13.1 Retouche d'images (GIMP, Krita, Inkscape)

## Introduction

Linux Mint offre d'excellents outils professionnels pour la création et la retouche d'images, tous gratuits et open source. Que vous souhaitiez retoucher des photos de vacances, créer des illustrations ou concevoir un logo, vous trouverez l'outil adapté à vos besoins.

Dans ce chapitre, nous allons découvrir les trois principaux logiciels de retouche et création graphique sous Linux :

- **GIMP** : pour la retouche photo et la manipulation d'images
- **Krita** : pour le dessin numérique et la peinture digitale
- **Inkscape** : pour le dessin vectoriel et la création de logos

> **Bon à savoir** : Ces trois logiciels sont des alternatives professionnelles et gratuites à des logiciels payants comme Photoshop (GIMP), Corel Painter (Krita) ou Adobe Illustrator (Inkscape).

---

## GIMP - Le couteau suisse de la retouche photo

### Qu'est-ce que GIMP ?

GIMP (GNU Image Manipulation Program) est un logiciel de retouche photo et de manipulation d'images très puissant. C'est l'équivalent libre et gratuit de Photoshop.

**Utilisations principales :**
- Retouche de photos (correction de couleurs, luminosité, contraste)
- Suppression d'éléments indésirables
- Montages photo et photomontages
- Création de graphiques pour le web
- Redimensionnement et optimisation d'images
- Application d'effets et de filtres

### Installation de GIMP

GIMP est souvent préinstallé sur Linux Mint. Pour vérifier ou l'installer :

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "GIMP"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update
sudo apt install gimp
```

### Première utilisation de GIMP

Au premier lancement, l'interface peut sembler intimidante avec ses nombreuses fenêtres et outils. Pas de panique, c'est normal !

**L'interface se compose de :**
- **La fenêtre centrale** : zone de travail où s'affiche votre image
- **La boîte à outils** (à gauche) : tous les outils de sélection, dessin, retouche
- **Les palettes** (à droite) : calques, brosses, dégradés, historique

> **Conseil débutant** : Si vous perdez une fenêtre, allez dans le menu **Fenêtres** → **Dialogues ancrables** pour la retrouver.

### Fonctionnalités essentielles de GIMP

#### 1. Ouvrir et enregistrer une image

- **Ouvrir** : `Fichier` → `Ouvrir` (ou `Ctrl + O`)
- **Enregistrer en format GIMP** : `Fichier` → `Enregistrer sous` (format .xcf, conserve les calques)
- **Exporter pour le web** : `Fichier` → `Exporter sous` (formats .jpg, .png, etc.)

> **Important** : Le format natif de GIMP (.xcf) conserve tous les calques et modifications. Utilisez "Exporter" pour créer des fichiers image classiques (JPG, PNG).

#### 2. Les outils de base

| Outil | Icône approximative | Utilisation |
|-------|---------------------|-------------|
| **Rectangle de sélection** | Rectangle pointillé | Sélectionner une zone rectangulaire |
| **Sélection elliptique** | Cercle pointillé | Sélectionner une zone circulaire |
| **Baguette magique** | Baguette | Sélectionner par couleur similaire |
| **Recadrage** | Ciseaux | Recadrer l'image |
| **Pinceau** | Brosse | Dessiner à main levée |
| **Gomme** | Gomme | Effacer des pixels |
| **Texte** | A | Ajouter du texte |
| **Remplissage** | Pot de peinture | Remplir une zone de couleur |

#### 3. Retouches courantes

**Améliorer une photo :**
- `Couleurs` → `Auto` → `Normaliser` : amélioration automatique
- `Couleurs` → `Luminosité-Contraste` : ajuster manuellement
- `Couleurs` → `Teinte-Saturation` : modifier les couleurs

**Redimensionner une image :**
- `Image` → `Échelle et taille de l'image`
- Décochez la chaîne pour modifier proportions
- Vérifiez la résolution (72 dpi pour le web, 300 dpi pour l'impression)

**Rogner/Recadrer :**
- Sélectionnez l'outil **Découpage** dans la boîte à outils
- Tracez la zone à conserver
- Appuyez sur **Entrée**

#### 4. Les calques : concept fondamental

Les calques fonctionnent comme des feuilles transparentes empilées. Vous pouvez :
- Ajouter un calque : `Calque` → `Nouveau calque`
- Supprimer un calque : clic droit sur le calque → `Supprimer le calque`
- Changer l'ordre : glisser-déposer dans la palette des calques
- Régler l'opacité : curseur en haut de la palette des calques

> **Analogie simple** : Imaginez que vous travaillez avec plusieurs transparents superposés. Chaque calque est un transparent sur lequel vous pouvez dessiner ou coller des éléments.

#### 5. Filtres et effets

GIMP propose des centaines de filtres accessibles via le menu `Filtres` :

**Filtres populaires :**
- `Flou` → `Flou gaussien` : créer un effet de profondeur de champ
- `Amélioration` → `Netteté` : rendre l'image plus nette
- `Distorsions` → divers effets créatifs
- `Ombres et lumières` → `Ombre portée` : ajouter une ombre

### Ressources pour apprendre GIMP

- Documentation officielle : https://docs.gimp.org/
- Tutoriels vidéo francophones sur YouTube
- Forums GIMP pour poser des questions

---

## Krita - Le logiciel de peinture numérique

### Qu'est-ce que Krita ?

Krita est spécialement conçu pour le **dessin numérique** et la **peinture digitale**. Contrairement à GIMP qui est orienté retouche photo, Krita est fait pour créer des illustrations à partir de zéro.

**Utilisations principales :**
- Illustration numérique
- Concept art
- Bande dessinée et manga
- Peinture digitale
- Animation 2D
- Design de personnages

### Installation de Krita

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "Krita"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update
sudo apt install krita
```

**Alternative Flatpak (version plus récente) :**
```bash
flatpak install flathub org.kde.krita
```

### Première utilisation de Krita

Krita est optimisé pour le dessin avec tablette graphique, mais fonctionne aussi très bien à la souris.

**L'interface comprend :**
- **Zone de dessin centrale** : votre toile
- **Barre d'outils** (à gauche) : pinceaux, sélection, formes
- **Sélecteur de brosses** (en haut à droite) : préréglages de pinceaux
- **Palette de calques** (en bas à droite) : gestion des calques
- **Palette de couleurs** (en bas) : sélection des couleurs

### Fonctionnalités essentielles de Krita

#### 1. Créer un nouveau document

- `Fichier` → `Nouveau`
- Choisissez un modèle prédéfini ou personnalisez :
  - Taille (A4, 1920x1080, format personnalisé)
  - Résolution (300 ppi pour impression, 72 pour écran)
  - Couleur de fond

#### 2. Les brosses : le cœur de Krita

Krita excelle dans la simulation de brosses réalistes :

**Préréglages de brosses populaires :**
- **Basic-5 Size** : brosse simple et polyvalente
- **Ink** : pour l'encrage de bande dessinée
- **Watercolor** : effet aquarelle
- **Airbrush** : aérographe
- **Charcoal** : fusain

**Modifier une brosse :**
- Appuyez sur `F5` pour ouvrir l'éditeur de brosses
- Ajustez la taille, l'opacité, le flux
- Sauvegardez vos propres préréglages

> **Astuce** : Utilisez les raccourcis clavier pour gagner du temps :
> - `E` : gomme
> - `B` : pinceau
> - `[` et `]` : diminuer/augmenter la taille de la brosse
> - `X` : échanger couleur de premier plan et d'arrière-plan

#### 3. Les calques dans Krita

Comme GIMP, Krita utilise des calques, mais avec des fonctionnalités supplémentaires :

**Types de calques :**
- **Calque de peinture** : calque normal pour dessiner
- **Calque de groupe** : organiser plusieurs calques
- **Calque de filtre** : appliquer un effet non destructif
- **Calque de remplissage** : remplissage de couleur ou motif

**Modes de fusion :**
Les modes de fusion changent la façon dont les calques interagissent (Normal, Multiplier, Superposer, etc.)

#### 4. Outils de sélection et transformation

- **Sélection rectangulaire/elliptique** : formes de base
- **Sélection polygonale** : sélection à main levée
- **Sélection de couleur similaire** : comme la baguette magique
- **Outil de transformation** : redimensionner, pivoter, déformer

#### 5. Stabilisateur de brosse

Une fonctionnalité unique de Krita très utile pour dessiner à la souris :

- Activez-le dans la barre d'outils (icône de main tremblante)
- Réglez le niveau de stabilisation
- Vos traits seront lissés automatiquement

#### 6. Animation 2D (fonctionnalité avancée)

Krita inclut un outil d'animation :
- `Paramètres` → `Vues` → `Chronologie`
- Créez des images clés
- Exportez en GIF ou vidéo

### Pourquoi choisir Krita plutôt que GIMP ?

Utilisez **Krita** si vous voulez :
- Dessiner, illustrer, peindre numériquement
- Créer des personnages, du concept art
- Travailler avec une tablette graphique
- Faire de l'animation 2D

Utilisez **GIMP** si vous voulez :
- Retoucher des photos existantes
- Faire des montages photo
- Optimiser des images pour le web
- Créer des designs basés sur des photos

---

## Inkscape - Le dessin vectoriel

### Qu'est-ce qu'Inkscape ?

Inkscape est un logiciel de **dessin vectoriel**. Contrairement aux images matricielles (pixels), les images vectorielles sont composées de formes mathématiques, ce qui les rend redimensionnables à l'infini sans perte de qualité.

**Utilisations principales :**
- Création de logos
- Illustrations techniques
- Icônes et pictogrammes
- Affiches et flyers
- Schémas et diagrammes
- Typographie et lettering

### Différence pixel vs vectoriel

**Image matricielle (GIMP/Krita) :**
- Composée de pixels
- Perd en qualité si agrandie
- Idéale pour photos et peinture numérique
- Formats : JPG, PNG, GIF

**Image vectorielle (Inkscape) :**
- Composée de formes mathématiques
- Redimensionnable à l'infini
- Idéale pour logos et illustrations
- Format principal : SVG

> **Exemple concret** : Un logo d'entreprise doit être vectoriel pour être utilisable sur une carte de visite (petit) comme sur un panneau publicitaire (grand).

### Installation d'Inkscape

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "Inkscape"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update
sudo apt install inkscape
```

### Première utilisation d'Inkscape

**L'interface se compose de :**
- **Zone de travail centrale** : votre page/plan de travail
- **Barre d'outils** (à gauche) : outils de dessin et sélection
- **Barre de contrôle** (en haut) : options de l'outil actif
- **Palettes de couleurs** (en bas) : couleurs de remplissage et contour

### Fonctionnalités essentielles d'Inkscape

#### 1. Créer un nouveau document

- `Fichier` → `Nouveau`
- Définissez les propriétés du document :
  - `Fichier` → `Propriétés du document`
  - Choisissez la taille (A4, format personnalisé, etc.)

#### 2. Les outils de base

**Outils de dessin :**
- **Rectangle** (`F4`) : dessiner des rectangles/carrés
- **Cercle** (`F5`) : dessiner des cercles/ellipses
- **Étoile** (`*`) : créer des étoiles et polygones
- **Courbe de Bézier** (`B`) : dessiner des formes personnalisées
- **Crayon** (`F6`) : dessin à main levée
- **Texte** (`F8`) : ajouter du texte

**Outils de modification :**
- **Sélection** (`F1` ou `S`) : sélectionner et déplacer
- **Nœuds** (`F2` ou `N`) : modifier les points d'une forme
- **Zoom** (`F3`) : zoomer dans le document

#### 3. Travailler avec les formes

**Créer un rectangle avec coins arrondis :**
1. Sélectionnez l'outil Rectangle (`F4`)
2. Dessinez un rectangle
3. Avec l'outil Nœuds (`F2`), faites glisser les poignées circulaires

**Convertir en chemin :**
- Sélectionnez une forme
- `Chemin` → `Objet en chemin`
- Permet de modifier librement la forme avec l'outil Nœuds

#### 4. Couleurs et remplissages

**Appliquer une couleur :**
- **Clic simple** sur une couleur en bas : change le remplissage
- **Shift + clic** : change le contour
- **Clic droit** sur l'objet → `Remplissage et contour` : options avancées

**Types de remplissage :**
- **Aplat** : couleur unie
- **Dégradé linéaire** : transition entre couleurs
- **Dégradé radial** : dégradé circulaire
- **Motif** : répétition d'un motif

#### 5. Alignement et distribution

Pour aligner plusieurs objets :
- Sélectionnez plusieurs objets (Shift + clic)
- `Objet` → `Aligner et distribuer` (`Ctrl + Shift + A`)
- Choisissez l'alignement souhaité (centre, gauche, espacement égal, etc.)

#### 6. Opérations booléennes

Combiner des formes entre elles :
- **Union** : fusionner deux formes
- **Différence** : soustraire une forme d'une autre
- **Intersection** : garder uniquement la partie commune
- **Exclusion** : inverse de l'intersection

Menu : `Chemin` → `Union/Différence/Intersection/Exclusion`

#### 7. Texte et typographie

**Ajouter du texte :**
1. Outil Texte (`F8`)
2. Cliquez pour texte court ou glissez pour zone de texte
3. Tapez votre texte
4. Changez la police et la taille dans la barre du haut

**Convertir texte en chemin :**
- Utile pour créer des effets typographiques
- `Chemin` → `Objet en chemin`
- Chaque lettre devient modifiable

#### 8. Exporter votre travail

**Export PNG (pour le web) :**
- `Fichier` → `Exporter au format PNG`
- Choisissez la zone d'export
- Définissez la résolution
- Exportez

**Enregistrer en SVG :**
- `Fichier` → `Enregistrer sous`
- Format SVG natif d'Inkscape
- Conserve toutes les possibilités d'édition

### Cas d'usage typiques d'Inkscape

1. **Logo d'entreprise** : formes simples, texte, vectoriel = redimensionnable
2. **Icônes** : dessins précis, export en différentes tailles
3. **Infographies** : combinaison de formes, texte et données
4. **Illustrations techniques** : schémas, plans, diagrammes
5. **Carte de visite** : design précis avec typographie

---

## Comparaison rapide des trois logiciels

| Critère | GIMP | Krita | Inkscape |
|---------|------|-------|----------|
| **Type** | Retouche photo | Peinture numérique | Dessin vectoriel |
| **Équivalent commercial** | Photoshop | Corel Painter | Adobe Illustrator |
| **Meilleur pour** | Photos, montages | Illustration, dessin | Logos, icônes |
| **Format de fichier** | .xcf (export jpg/png) | .kra (export jpg/png) | .svg (export png) |
| **Avec tablette** | Possible mais limité | Excellent | Peu utilisé |
| **Niveau débutant** | Moyen | Moyen | Facile à moyen |
| **Qualité agrandissement** | Se dégrade (pixels) | Se dégrade (pixels) | Parfaite (vecteurs) |

---

## Quel logiciel choisir selon vos besoins ?

### Choisissez GIMP si vous voulez :
- ✅ Retoucher vos photos de famille
- ✅ Supprimer un élément d'une photo
- ✅ Créer un photomontage
- ✅ Améliorer luminosité/contraste d'images
- ✅ Préparer des images pour un site web

### Choisissez Krita si vous voulez :
- ✅ Dessiner des illustrations
- ✅ Créer des personnages
- ✅ Faire de la peinture numérique
- ✅ Utiliser une tablette graphique
- ✅ Créer des animations 2D simples

### Choisissez Inkscape si vous voulez :
- ✅ Créer un logo professionnel
- ✅ Designer des icônes
- ✅ Faire des affiches ou flyers
- ✅ Créer des schémas techniques
- ✅ Avoir un design redimensionnable à l'infini

> **Conseil** : Ces trois logiciels sont complémentaires ! De nombreux professionnels les utilisent tous les trois selon leurs projets.

---

## Installer les trois d'un coup

Si vous voulez tout installer rapidement :

```bash
sudo apt update
sudo apt install gimp krita inkscape
```

---

## Ressources pour progresser

### Documentation officielle
- **GIMP** : https://docs.gimp.org/
- **Krita** : https://docs.krita.org/
- **Inkscape** : https://inkscape.org/learn/

### Communautés francophones
- Forums Linux Mint
- Reddit : r/GIMP, r/krita, r/Inkscape
- Groupes Facebook de graphistes Linux

### Tutoriels vidéo
- YouTube regorge de tutoriels gratuits en français
- Recherchez par logiciel et par projet spécifique

### Formations en ligne
- Certains sites proposent des formations complètes
- Des cours gratuits sont disponibles sur YouTube et certaines plateformes

---

## Conseils pour bien débuter

1. **Commencez simple** : ne cherchez pas à maîtriser tous les outils d'un coup
2. **Suivez des tutoriels** : reproduisez des créations pour apprendre les techniques
3. **Pratiquez régulièrement** : 30 minutes par jour valent mieux qu'une journée par mois
4. **Expérimentez** : n'ayez pas peur de tester les différents outils et filtres
5. **Rejoignez une communauté** : partagez vos créations et demandez des conseils
6. **Soyez patient** : la maîtrise de ces logiciels demande du temps

---

## Alternatives et mentions honorables

**Autres logiciels de retouche disponibles sur Linux :**
- **Darktable** : spécialisé dans le développement RAW (photos professionnelles)
- **RawTherapee** : également pour le traitement de fichiers RAW
- **Pinta** : alternative plus simple à GIMP pour retouches basiques
- **MyPaint** : spécialisé dans la peinture numérique, interface minimaliste

---

## Conclusion

Linux Mint vous offre tous les outils nécessaires pour la création graphique professionnelle, et ce, gratuitement. Que vous soyez photographe amateur, illustrateur en herbe ou designer, vous trouverez votre bonheur parmi ces trois géants de la création graphique open source.

**GIMP**, **Krita** et **Inkscape** sont utilisés par des professionnels du monde entier et n'ont rien à envier aux solutions commerciales coûteuses. La seule limite est votre créativité et votre motivation à apprendre.

N'hésitez pas à installer les trois logiciels et à les tester sur de petits projets pour vous familiariser avec leurs interfaces et leurs philosophies respectives.

**Prochaine étape** : Dans la section suivante, nous découvrirons le montage vidéo sous Linux Mint avec des outils comme Kdenlive et OpenShot.

---

*Bon apprentissage et bonnes créations ! 🎨*

⏭️ [Montage vidéo (Kdenlive, OpenShot, DaVinci Resolve)](/13-multimedia-et-creativite/02-montage-video.md)
