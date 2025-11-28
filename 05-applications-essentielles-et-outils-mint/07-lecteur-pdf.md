🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7 Lecteur PDF

## Introduction

Le **PDF** (Portable Document Format) est le format standard pour partager des documents tout en préservant leur mise en page exacte. Linux Mint inclut plusieurs outils pour lire, annoter et manipuler vos fichiers PDF, avec **Xreader** comme lecteur par défaut.

## Qu'est-ce qu'un PDF ?

### Présentation du format PDF

**PDF** signifie **Portable Document Format**, créé par Adobe.

**Caractéristiques** :
- **Mise en page fixe** : Apparence identique sur tous les appareils
- **Multiplateforme** : Lisible sur Windows, Mac, Linux, mobiles
- **Sécurisé** : Peut être protégé par mot de passe
- **Non modifiable** : Préserve l'intégrité du document
- **Compact** : Compression efficace

### Pourquoi utiliser des PDF ?

**Cas d'usage courants** :
- **Documents officiels** : Factures, contrats, CV
- **Formulaires** : Administratifs, demandes
- **Livres et magazines** : Ebooks, manuels
- **Présentations** : Diaporamas figés
- **Archives** : Conservation à long terme

**Avantages** :
- Le destinataire voit exactement ce que vous avez créé
- Impossible de modifier accidentellement
- Fonctionne partout
- Peut inclure des liens, formulaires, signatures

## Xreader - Le lecteur PDF par défaut

### Présentation de Xreader

**Xreader** est le lecteur de documents installé par défaut sur Linux Mint.

**Formats supportés** :
- **PDF** : Principal
- **EPUB** : Livres électroniques
- **XPS** : Format Microsoft
- **DjVu** : Documents scannés
- **TIFF** : Images multipage
- **PostScript** : Documents techniques

**Fonctionnalités** :
- Lecture simple et rapide
- Navigation intuitive
- Recherche de texte
- Annotations basiques
- Mode plein écran
- Rotation de pages
- Zoom précis

### Lancer Xreader

**Méthode 1 - Double-clic** :
1. Ouvrez le gestionnaire de fichiers (Nemo)
2. Naviguez vers votre fichier PDF
3. Double-cliquez dessus
4. Xreader s'ouvre automatiquement

**Méthode 2 - Menu** :
1. Menu principal → **Accessoires** → **Visionneuse de documents**
2. Ou tapez "Xreader" dans la recherche

**Méthode 3 - Clic droit** :
1. Clic droit sur un PDF
2. **Ouvrir avec** → **Visionneuse de documents**

### Interface de Xreader

**Barre d'outils** (en haut) :
- Navigation : Précédent, Suivant, Premier, Dernier
- Zoom : +, -, Ajuster, Largeur de page
- Rotation : Pivoter gauche/droite
- Mode d'affichage : Une page, Deux pages, Continu
- Recherche
- Panneau latéral (index)
- Propriétés
- Menu principal

**Zone de lecture** (centre) :
- Document affiché
- Fond gris autour

**Barre d'état** (en bas) :
- Numéro de page actuelle / Total
- Zoom actuel
- Taille du document

**Panneau latéral** (gauche, optionnel) :
- Vignettes des pages
- Table des matières (index)
- Annotations

## Lire des PDF avec Xreader

### Ouvrir un document

**Depuis Xreader** :
1. Lancez Xreader
2. **Fichier** → **Ouvrir**
3. Raccourci : `Ctrl + O`
4. Parcourez et sélectionnez votre PDF
5. Cliquez sur **Ouvrir**

**Glisser-déposer** :
- Glissez un fichier PDF depuis le gestionnaire de fichiers
- Déposez-le dans la fenêtre Xreader
- Le document s'ouvre

### Navigation dans le document

**Avec la souris** :
- **Molette** : Défilement vertical
- **Maj + Molette** : Défilement horizontal
- **Barres de défilement** : Navigation précise

**Avec le clavier** :
- **↓** / **↑** : Défiler
- **Page suivante** / **Page précédente** : Page par page
- **Espace** : Page suivante
- **Maj + Espace** : Page précédente
- **Début** : Première page
- **Fin** : Dernière page

**Boutons de navigation** :
- **←** **→** : Page précédente/suivante
- **⏮** **⏭** : Première/dernière page

**Aller à une page spécifique** :
1. `Ctrl + L` ou cliquez sur le numéro de page
2. Tapez le numéro de page
3. Appuyez sur `Entrée`

### Modes d'affichage

**Une seule page** :
- Affiche une page à la fois
- Idéal pour lecture normale
- Raccourci : `Ctrl + 1`

**Deux pages (double page)** :
- Affiche deux pages côte à côte
- Comme un livre ouvert
- Utile pour magazines, livres
- Raccourci : `Ctrl + 2`

**Mode continu** :
- Toutes les pages défilent en continu
- Pas de coupure entre pages
- Raccourci : `Ctrl + 3`

**Choisir** :
- Menu **Affichage** → Mode
- Ou icônes dans la barre d'outils

### Zoom

**Niveaux de zoom** :

**Ajuster à la fenêtre** :
- La page s'adapte à la hauteur de la fenêtre
- Raccourci : `Ctrl + 0`

**Ajuster à la largeur** :
- La page s'adapte à la largeur
- Permet de voir toute la largeur sans défilement horizontal
- Raccourci : `Ctrl + W`

**Taille réelle** :
- 100% (taille d'impression)
- Raccourci : `Ctrl + Maj + A`

**Zoom personnalisé** :
- `Ctrl + +` : Zoom avant
- `Ctrl + -` : Zoom arrière
- `Ctrl + Molette` : Zoom progressif
- Menu déroulant : Pourcentages prédéfinis (50%, 75%, 100%, 150%, 200%, etc.)

**Navigation dans le zoom** :
- Cliquez et glissez pour déplacer la vue
- Ou utilisez les barres de défilement

### Rotation des pages

**Pivoter le document** :
- **Rotation gauche** : `Ctrl + ←` ou icône dans la barre
- **Rotation droite** : `Ctrl + →` ou icône dans la barre
- Utile pour PDFs mal orientés

**Attention** :
- La rotation est temporaire (affichage seulement)
- Pour sauvegarder, utilisez un éditeur PDF (voir section manipulation)

### Recherche de texte

**Rechercher dans le document** :
1. **Édition** → **Rechercher**
2. Raccourci : `Ctrl + F`
3. Une barre de recherche apparaît en haut
4. Tapez votre texte
5. Xreader surligne les résultats

**Navigation dans les résultats** :
- **Entrée** ou **Suivant** : Résultat suivant
- **Maj + Entrée** ou **Précédent** : Résultat précédent
- Nombre de résultats affiché

**Options de recherche** :
- **Respecter la casse** : Différencie majuscules/minuscules
- **Mots entiers uniquement** : Pas de correspondances partielles

**Fermer la recherche** :
- `Échap` ou cliquez sur **×**

### Panneau latéral

**Afficher/masquer** :
- `F9` ou icône **Panneau latéral**
- Menu **Affichage** → **Panneau latéral**

**Onglets du panneau** :

**Vignettes** :
- Aperçu miniature de toutes les pages
- Cliquez sur une vignette pour y aller directement
- Utile pour repérage visuel rapide

**Index** (Table des matières) :
- Structure du document
- Signets et chapitres
- Clic sur un élément → Va à cette section
- Disponible seulement si le PDF contient un index

**Annotations** :
- Liste de vos annotations
- Cliquez pour aller à l'annotation

### Plein écran

**Activer le mode plein écran** :
- `F11` ou bouton **Plein écran**
- Menu **Affichage** → **Plein écran**

**En mode plein écran** :
- Document occupe tout l'écran
- Bougez la souris → Contrôles apparaissent
- Idéal pour présentations ou lecture immersive

**Quitter** :
- `F11` ou `Échap`

### Mode présentation

**Pour diaporamas** :
- `F5` ou menu **Affichage** → **Présentation**
- Similaire au plein écran mais optimisé pour présentations
- Navigation : Clic, Flèches, Espace
- `Échap` pour quitter

### Propriétés du document

**Voir les informations** :
1. **Fichier** → **Propriétés**
2. Raccourci : `Alt + Entrée`

**Informations affichées** :
- **Titre** : Titre du document (si défini)
- **Auteur** : Créateur
- **Sujet** : Description
- **Mots-clés** : Tags
- **Créateur** : Logiciel utilisé pour créer
- **Producteur** : Logiciel de conversion en PDF
- **Date de création** : Quand le PDF a été créé
- **Date de modification** : Dernière modification
- **Nombre de pages**
- **Taille du fichier**
- **Version PDF** : 1.4, 1.5, 1.7, etc.
- **Sécurité** : Protégé par mot de passe, permissions

### Copier du texte

**Sélectionner et copier** :
1. Cliquez et glissez sur le texte à sélectionner
2. Le texte se surligne
3. `Ctrl + C` pour copier
4. Collez ailleurs avec `Ctrl + V`

**Tout sélectionner** :
- `Ctrl + A` : Sélectionne tout le texte de la page actuelle

**Limitations** :
- Ne fonctionne que si le PDF contient du texte (pas sur PDFs scannés)
- Mise en forme perdue lors de la copie
- Images non copiables directement (utilisez capture d'écran)

### Imprimer un PDF

**Imprimer le document** :
1. **Fichier** → **Imprimer**
2. Raccourci : `Ctrl + P`
3. Sélectionnez votre imprimante
4. Options :
   - **Toutes** : Tout le document
   - **Pages** : Spécifiez (ex: 1-5, 8, 12-15)
   - **Page courante** : Juste la page affichée
5. **Copies** : Nombre d'exemplaires
6. **Recto-verso** : Si imprimante compatible
7. Cliquez sur **Imprimer**

**Imprimer en PDF** :
- Utile pour "extraire" certaines pages
- Choisissez **Imprimer dans un fichier**
- Format : **PDF**
- Spécifiez les pages à extraire
- Enregistrez

## Annotations et surlignage

### Outils d'annotation (limités dans Xreader)

**Xreader a des fonctionnalités limitées** pour l'annotation. Pour des annotations avancées, voir section "Alternatives".

**Ce que Xreader permet** :
- Surlignage basique (certaines versions)
- Ajout de notes (limité)

**Ce qui nécessite un autre outil** :
- Annotations riches
- Dessins
- Formes
- Signatures

**Pour annotations avancées**, utilisez :
- Okular (voir section Alternatives)
- LibreOffice Draw
- Xournal++ (spécialisé annotations)

## Formulaires PDF

### Remplir des formulaires

**Formulaires interactifs** :

Certains PDFs contiennent des champs à remplir (formulaires administratifs, etc.).

**Avec Xreader** :
1. Ouvrez le formulaire PDF
2. Cliquez dans les champs
3. Tapez vos informations
4. **Fichier** → **Enregistrer sous** pour sauvegarder

**Limitations** :
- Support basique
- Pour formulaires complexes, utilisez Okular ou LibreOffice Draw

**Si les champs ne fonctionnent pas** :
- Le PDF n'est peut-être pas un formulaire interactif
- Imprimez-le et remplissez à la main
- Ou utilisez un éditeur PDF comme LibreOffice Draw

### Signer un PDF

**Signature manuscrite** :

Xreader ne supporte pas les signatures directement.

**Solutions** :
1. Imprimez le document
2. Signez à la main
3. Scannez
4. Ou utilisez Xournal++ pour signature numérique

## Documents protégés par mot de passe

### Ouvrir un PDF protégé

**Si le PDF est chiffré** :
1. Double-cliquez sur le PDF
2. Une fenêtre demande le mot de passe
3. Entrez le mot de passe
4. Cliquez sur **Déverrouiller**
5. Le document s'ouvre

**Si mot de passe incorrect** :
- Impossible d'ouvrir
- Vérifiez le mot de passe
- Contactez l'expéditeur

### Permissions restreintes

**Certains PDFs ont des restrictions** :
- Impression interdite
- Copie de texte interdite
- Modification interdite

**Xreader respecte ces restrictions** :
- Les options sont grisées
- Pour contourner (légalement, avec autorisation), utilisez des outils spécialisés

## Raccourcis clavier Xreader

| Raccourci | Action |
|-----------|--------|
| `Ctrl + O` | Ouvrir un fichier |
| `Ctrl + S` | Enregistrer une copie |
| `Ctrl + P` | Imprimer |
| `Ctrl + W` | Fermer le document |
| `Ctrl + Q` | Quitter Xreader |
| `Ctrl + F` | Rechercher |
| `Ctrl + +` | Zoom avant |
| `Ctrl + -` | Zoom arrière |
| `Ctrl + 0` | Ajuster à la fenêtre |
| `Ctrl + W` | Ajuster à la largeur |
| `Ctrl + 1` | Une page |
| `Ctrl + 2` | Deux pages |
| `F9` | Panneau latéral |
| `F11` | Plein écran |
| `F5` | Mode présentation |
| `Ctrl + →` | Rotation droite |
| `Ctrl + ←` | Rotation gauche |
| `Page suivante` | Page suivante |
| `Page précédente` | Page précédente |
| `Début` | Première page |
| `Fin` | Dernière page |
| `Espace` | Page suivante |
| `Maj + Espace` | Page précédente |

## Alternatives à Xreader

### Okular - Lecteur avancé

**Okular** est le lecteur PDF de KDE, plus complet que Xreader.

**Installation** :
```bash
sudo apt install okular
```

**Avantages** :
- **Annotations riches** : Surlignage, notes, formes, dessins
- **Formulaires** : Meilleur support
- **Signatures** : Possibilité de signer
- **Onglets** : Plusieurs documents ouverts
- **Plus de formats** : Support étendu

**Inconvénient** :
- Plus lourd (dépendances KDE)
- Interface plus complexe

**Fonctionnalités d'Okular** :

**Annotations** :
- Outils **Révision** dans le menu
- Surlignage de couleurs
- Notes adhésives
- Formes géométriques
- Tampon (Approuvé, Confidentiel, etc.)

**Sauvegarder les annotations** :
- **Fichier** → **Enregistrer sous**
- Ou exporter juste les annotations

**Formulaires** :
- Remplissage avancé
- Cases à cocher, boutons radio
- Sauvegarde possible

### Evince (GNOME)

**Evince** est le lecteur GNOME (similaire à Xreader).

```bash
sudo apt install evince
```

**Caractéristiques** :
- Très similaire à Xreader
- Interface GNOME native
- Léger et rapide

**Différence avec Xreader** :
- Minime, Xreader est un fork d'Evince
- Utilisez celui que vous préférez

### PDF Arranger

**PDF Arranger** permet de **réorganiser** les pages PDF.

**Installation** :
```bash
sudo apt install pdfarranger
```

**Fonctionnalités** :
- Réorganiser l'ordre des pages (glisser-déposer)
- Fusionner plusieurs PDFs
- Supprimer des pages
- Rotation permanente
- Diviser un PDF

**Usage typique** :
1. Ouvrez un ou plusieurs PDFs
2. Glissez-déposez les pages pour réorganiser
3. Supprimez les pages inutiles
4. **Fichier** → **Enregistrer**

**Cas d'usage** :
- Retirer des pages d'un PDF
- Combiner plusieurs PDFs
- Changer l'ordre des pages

### Xournal++ - Annotations manuscrites

**Xournal++** est spécialisé dans les annotations manuscrites (avec stylet/souris).

**Installation** :
```bash
sudo apt install xournalpp
```

**Fonctionnalités** :
- Annotations manuscrites fluides
- Support stylet et tablette graphique
- Surlignage, formes
- Texte
- Couches (layers)

**Usage** :
1. **Fichier** → **Annoter un PDF**
2. Sélectionnez votre PDF
3. Annotez avec les outils
4. **Fichier** → **Exporter en PDF**

**Idéal pour** :
- Étudiants prenant des notes sur documents
- Enseignants corrigeant des copies
- Annotations avec tablette graphique

### LibreOffice Draw - Éditeur PDF

**LibreOffice Draw** peut ouvrir et **modifier** des PDFs.

**Déjà installé** sur Linux Mint.

**Usage** :
1. Clic droit sur un PDF → **Ouvrir avec** → **LibreOffice Draw**
2. Le PDF s'ouvre comme document éditable
3. Modifiez texte, ajoutez images, formes, annotations
4. **Fichier** → **Exporter en PDF**

**Avantages** :
- Édition complète
- Ajout d'éléments
- Annotations riches

**Limitations** :
- PDFs complexes peuvent mal se convertir
- Mise en page parfois altérée
- Mieux pour PDFs simples

**Idéal pour** :
- Remplir formulaires non interactifs
- Ajouter une signature scannée
- Modifier légèrement un PDF simple

## Manipulation de PDF en ligne de commande

### PDFtk - Outil puissant

**PDFtk** (PDF Toolkit) permet de manipuler des PDFs via terminal.

**Installation** :
```bash
sudo apt install pdftk
```

**Exemples d'usage** :

**Fusionner des PDFs** :
```bash
pdftk fichier1.pdf fichier2.pdf fichier3.pdf cat output fusion.pdf
```

**Extraire des pages** :
```bash
pdftk document.pdf cat 1-5 output pages1-5.pdf
```

**Extraire pages spécifiques** :
```bash
pdftk document.pdf cat 1 3 5 10-15 output selection.pdf
```

**Rotation de pages** :
```bash
pdftk document.pdf cat 1-endeast output rotated.pdf
```
- `east` : Rotation 90° droite
- `west` : Rotation 90° gauche
- `south` : Rotation 180°

**Diviser par page** :
```bash
pdftk document.pdf burst
```
Crée un fichier PDF pour chaque page.

**Ajouter un mot de passe** :
```bash
pdftk document.pdf output protege.pdf user_pw MOTDEPASSE
```

**Retirer un mot de passe** :
```bash
pdftk protege.pdf input_pw MOTDEPASSE output deprotege.pdf
```

### Ghostscript - Compression et conversion

**Ghostscript** est un processeur PostScript/PDF.

**Compresser un PDF** :
```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook \
   -dNOPAUSE -dQUIET -dBATCH -sOutputFile=compresse.pdf original.pdf
```

**Niveaux de compression** :
- `/screen` : Très compressé (écran uniquement, 72 dpi)
- `/ebook` : Bon compromis (150 dpi)
- `/printer` : Qualité impression (300 dpi)
- `/prepress` : Qualité professionnelle (300 dpi, CMYK)

**Convertir PDF en images** :
```bash
gs -sDEVICE=jpeg -r300 -o page-%03d.jpg document.pdf
```
Crée une image JPEG par page.

### ImageMagick - Conversion

**Convertir images en PDF** :
```bash
convert image1.jpg image2.jpg image3.jpg document.pdf
```

**Fusionner images dans un PDF** :
```bash
convert *.jpg album-photos.pdf
```

**PDF vers images** :
```bash
convert -density 300 document.pdf page.png
```

### qpdf - Manipulation avancée

**qpdf** est un outil de manipulation structurelle.

**Installation** :
```bash
sudo apt install qpdf
```

**Déchiffrer un PDF** :
```bash
qpdf --password=MOTDEPASSE --decrypt protege.pdf deprotege.pdf
```

**Linéariser** (optimiser pour web) :
```bash
qpdf --linearize document.pdf optimise.pdf
```

**Fusionner** :
```bash
qpdf --empty --pages fichier1.pdf fichier2.pdf -- fusion.pdf
```

## Créer des PDF

### Depuis LibreOffice

**Méthode la plus simple** :

1. Créez votre document dans LibreOffice (Writer, Calc, Impress)
2. **Fichier** → **Exporter au format PDF**
3. Options :
   - **Plage** : Toutes les pages ou sélection
   - **Images** : Qualité de compression
   - **Sécurité** : Mot de passe, permissions
   - **Signet** : Créer des signets depuis les titres
   - **Liens** : Préserver les hyperliens
4. Cliquez sur **Exporter**
5. Nommez et enregistrez

**Raccourci direct** :
- Icône **Exporter au format PDF** dans la barre d'outils
- Export rapide avec paramètres par défaut

### Imprimer en PDF (universel)

**Depuis n'importe quelle application** :

1. **Fichier** → **Imprimer** (`Ctrl + P`)
2. Sélectionnez **Imprimer dans un fichier**
3. Format de sortie : **PDF**
4. Nommez le fichier
5. Choisissez l'emplacement
6. Cliquez sur **Imprimer**

**Fonctionne depuis** :
- Navigateur web (Firefox, Chrome)
- Éditeurs de texte
- Visionneuses d'images
- Pratiquement toute application

**Cas d'usage** :
- Convertir une page web en PDF
- Sauvegarder un email en PDF
- Créer un PDF depuis une image

### Scanner vers PDF

**Avec Simple Scan** :

1. Lancez **Simple Scan**
2. Scannez votre document
3. **Document** → **Enregistrer sous**
4. Format : **PDF**
5. Enregistrez

**Plusieurs pages dans un PDF** :
- Scannez la première page
- Cliquez sur **+** pour ajouter une page
- Scannez les pages suivantes
- Enregistrez tout en un seul PDF

### Outils de création avancée

**Scribus** (PAO - Publication Assistée par Ordinateur) :

**Installation** :
```bash
sudo apt install scribus
```

**Usage** :
- Création professionnelle (magazines, brochures, livres)
- Contrôle total sur la mise en page
- Export PDF haute qualité
- Courbe d'apprentissage importante

**Inkscape** (dessin vectoriel) :

**Export PDF** :
- Créez votre design vectoriel
- **Fichier** → **Enregistrer sous**
- Format : **PDF**
- Ou **Fichier** → **Enregistrer une copie** → PDF

**Usage** :
- Affiches, flyers, logos
- Illustrations vectorielles
- PDF avec graphiques de qualité

## Compression et optimisation de PDF

### Réduire la taille d'un PDF

**Pourquoi compresser** :
- PDFs trop gros pour email (limite ~25 Mo)
- Économiser de l'espace disque
- Accélérer les téléchargements

**Méthode 1 - Ghostscript** :

```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook \
   -dNOPAUSE -dQUIET -dBATCH -sOutputFile=compresse.pdf original.pdf
```

**Choisir le niveau** :
- `/screen` : Fichier très petit (qualité écran)
- `/ebook` : Bon compromis (recommandé)
- `/printer` : Qualité impression maintenue

**Méthode 2 - PDF Arranger** :

1. Ouvrez le PDF dans PDF Arranger
2. **Fichier** → **Enregistrer**
3. Ajustez les options de qualité

**Méthode 3 - LibreOffice** :

1. Ouvrez le PDF dans LibreOffice Draw
2. **Fichier** → **Exporter au format PDF**
3. Réduisez la qualité des images
4. Exportez

**Attention** :
- Compression = perte de qualité
- Testez le résultat avant de supprimer l'original
- Pour documents importants, gardez l'original en qualité maximale

### Optimiser pour le web

**Linéarisation** (Fast Web View) :

Permet l'affichage progressif dans les navigateurs.

```bash
qpdf --linearize document.pdf optimise-web.pdf
```

**Avantage** :
- La première page s'affiche pendant le téléchargement du reste
- Meilleure expérience utilisateur sur le web

## OCR (Reconnaissance de texte)

### Qu'est-ce que l'OCR ?

**OCR** = Optical Character Recognition (Reconnaissance Optique de Caractères)

**Convertit** :
- Images scannées → Texte sélectionnable et cherchable
- PDFs "images" → PDFs avec texte

**Utilité** :
- Rechercher dans des documents scannés
- Copier du texte depuis des scans
- Éditer le contenu

### OCRmyPDF - Ajout OCR aux PDFs

**Installation** :
```bash
sudo apt install ocrmypdf
sudo apt install tesseract-ocr-fra  # Langue française
```

**Usage de base** :
```bash
ocrmypdf document-scanne.pdf document-avec-texte.pdf
```

**Avec langue française** :
```bash
ocrmypdf -l fra document-scanne.pdf document-avec-texte.pdf
```

**Options utiles** :

**Deskew** (redresser) :
```bash
ocrmypdf --deskew document-scanne.pdf document-avec-texte.pdf
```

**Optimisation** :
```bash
ocrmypdf --optimize 3 document.pdf optimise.pdf
```
- Niveau 1-3 (3 = maximum)

**Forcer OCR** (même si texte déjà présent) :
```bash
ocrmypdf --force-ocr document.pdf nouveau.pdf
```

**Résultat** :
- Le PDF ressemble visuellement identique
- Mais le texte est maintenant sélectionnable et cherchable

### Tesseract - OCR direct

**Tesseract** peut aussi faire de l'OCR sur des images.

**Installation** :
```bash
sudo apt install tesseract-ocr tesseract-ocr-fra
```

**Extraire texte d'une image** :
```bash
tesseract image.png sortie -l fra
```

Crée `sortie.txt` avec le texte extrait.

**PDF en sortie** :
```bash
tesseract image.png sortie -l fra pdf
```

Crée `sortie.pdf` avec texte sélectionnable.

## Sécurité des PDF

### Protéger un PDF par mot de passe

**Avec PDFtk** :
```bash
pdftk document.pdf output protege.pdf user_pw MOTDEPASSE
```

**Avec qpdf** :
```bash
qpdf --encrypt MOTDEPASSE_USER MOTDEPASSE_OWNER 256 -- document.pdf protege.pdf
```

**user_pw** : Mot de passe pour ouvrir
**owner_pw** : Mot de passe pour modifier les permissions

**Avec LibreOffice** :
1. Créez votre document
2. **Fichier** → **Exporter au format PDF**
3. Onglet **Sécurité**
4. **Définir un mot de passe d'ouverture**
5. Entrez le mot de passe
6. Exportez

### Définir des permissions

**Restrictions possibles** :
- Interdire l'impression
- Interdire la copie de texte
- Interdire les modifications
- Interdire l'extraction de pages

**Avec qpdf** :
```bash
qpdf --encrypt USERPASS OWNERPASS 256 \
     --print=none --modify=none --extract=n \
     -- document.pdf restreint.pdf
```

**Avec LibreOffice** (export PDF) :
- Onglet **Sécurité** → **Définir les permissions**
- Cochez/décochez les autorisations

**Note** : Ces restrictions ne sont pas inviolables, mais découragent l'usage non autorisé.

### Signature numérique

**Signature certifiée** nécessite un certificat numérique.

**Solutions** :
- **LibreOffice** : Peut signer avec certificat
- **Okular** : Support de signature
- **Logiciels spécialisés** : Adobe Acrobat (payant)

**Pour usage simple** :
- Ajoutez une image de votre signature manuscrite avec LibreOffice Draw
- Pas de certification cryptographique, mais visuellement signé

## Astuces et bonnes pratiques

### Organiser ses PDFs

**Nommage cohérent** :

**Bonnes pratiques** :
- **Date** : `2024-03-15-Facture-Electricite.pdf`
- **Descriptif** : `Contrat-Location-Appartement-Paris.pdf`
- **Numéros** : `Facture-2024-001.pdf`, `Facture-2024-002.pdf`

**Mauvais exemples** :
- `document.pdf` (trop vague)
- `sans titre (3).pdf` (générique)
- `aaaa.pdf` (incompréhensible)

**Structure de dossiers** :
```
~/Documents/
  ├── Administratif/
  │   ├── Impôts/
  │   ├── Banque/
  │   └── Assurances/
  ├── Travail/
  │   ├── Contrats/
  │   └── Fiches-de-paie/
  └── Personnel/
      ├── Certificats/
      └── Diplomes/
```

### Combinaison de PDFs

**Cas d'usage** : Envoyer plusieurs documents en un seul fichier.

**Avec PDFtk** :
```bash
pdftk CV.pdf Lettre-Motivation.pdf Diplomes.pdf cat output Candidature-Complete.pdf
```

**Avec PDF Arranger** (graphique) :
1. **Fichier** → **Importer** les PDFs
2. Réorganisez l'ordre si nécessaire
3. **Fichier** → **Enregistrer**

### Extraction de pages

**Extraire certaines pages** :

**Avec PDFtk** :
```bash
pdftk manuel.pdf cat 10-20 output chapitre2.pdf
```

**Avec Xreader** (via impression) :
1. Ouvrez le PDF
2. **Fichier** → **Imprimer**
3. **Pages** : Spécifiez la plage (ex: 10-20)
4. **Imprimer dans un fichier** → PDF
5. Enregistrez

### Réduire le nombre de pages

**Impression multiple pages par feuille** :

**Cas d'usage** : Imprimer un document de 100 pages sur 25 feuilles (4 pages par feuille).

1. **Fichier** → **Imprimer**
2. **Pages par feuille** : 2, 4, 6, 9, 16
3. **Ordre** : De gauche à droite, de haut en bas
4. Imprimez

**Économie de papier** et création de livrets.

### PDF depuis captures d'écran

**Créer un PDF de plusieurs captures** :

1. Prenez vos captures d'écran (images PNG/JPG)
2. Terminal :
```bash
convert capture1.png capture2.png capture3.png tutoriel.pdf
```

**Ou avec LibreOffice Writer** :
1. Insérez les captures comme images
2. Exportez en PDF

### Marque-pages (signets)

**Pour navigation rapide dans gros PDFs** :

**Lors de la création** (LibreOffice) :
- Utilisez les styles de titre (Titre 1, Titre 2, etc.)
- Lors de l'export PDF, cochez **Créer des signets**
- Les titres deviennent des marque-pages cliquables

**Résultat** :
- Panneau latéral dans Xreader/Okular affiche la structure
- Navigation rapide par chapitres

## Accessibilité

### PDF accessibles

**Pour personnes malvoyantes** :

**Bonnes pratiques** :
- **Texte sélectionnable** : Pas d'images de texte
- **Structure logique** : Titres, paragraphes bien définis
- **Texte alternatif** : Description des images
- **Contraste** : Couleurs lisibles

**Création dans LibreOffice** :
1. Utilisez les styles correctement
2. Ajoutez du texte alternatif aux images
3. Exportez en PDF avec options d'accessibilité

**Lecteur d'écran** :
- Orca (lecteur d'écran Linux) peut lire les PDFs accessibles
- Texte sélectionnable essentiel

### Agrandir le texte

**Pour meilleure lecture** :
- Zoom important (`Ctrl + +`)
- Mode **Ajuster à la largeur** pour éviter défilement horizontal
- Plein écran pour immersion

## Dépannage

### PDF ne s'ouvre pas

**Causes possibles** :

**Fichier corrompu** :
- Téléchargement incomplet
- Re-téléchargez le fichier

**Format invalide** :
- Vérifiez l'extension (doit être `.pdf`)
- Ouvrez avec un éditeur de texte : Doit commencer par `%PDF-`

**Permissions** :
- Vérifiez les droits de lecture
```bash
ls -l fichier.pdf
chmod +r fichier.pdf
```

**Solution** :
- Essayez avec un autre lecteur (Okular, Evince)
- Essayez dans le navigateur (Firefox)

### Texte non sélectionnable

**PDF "image"** (scanné sans OCR) :

**Solution** :
- Utilisez OCRmyPDF pour ajouter du texte
```bash
ocrmypdf -l fra scan.pdf scan-avec-texte.pdf
```

### PDF trop lent

**Gros PDF (centaines de pages, beaucoup d'images)** :

**Solutions** :
- Utilisez un lecteur plus léger (Xreader est déjà léger)
- Fermez autres applications
- Compressez le PDF si possible
- Augmentez la RAM de l'ordinateur

### Impossible de modifier

**PDF en lecture seule** :

**Si vous devez modifier** :
1. Ouvrez avec LibreOffice Draw
2. Modifiez
3. Exportez en nouveau PDF

**Ou** :
- Convertissez en document Word (LibreOffice Writer peut importer PDF)
- Modifiez
- Re-exportez en PDF

**Note** : Modification de PDF n'est pas toujours parfaite, mise en page peut changer.

## Ressources et liens

### Documentation

**Xreader** :
- Pas de site dédié, partie de Linux Mint
- Documentation Linux Mint couvre Xreader

**Okular** :
- [https://okular.kde.org/](https://okular.kde.org/)

**PDFtk** :
- [https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/](https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/)

### Communauté

- Forums Linux Mint
- Ask Ubuntu (applicable à Mint)
- Reddit : r/linux4noobs

### Outils en ligne (alternatives)

**Si aucun outil local ne fonctionne** :

**Smallpdf** : [https://smallpdf.com/](https://smallpdf.com/)
- Compression, fusion, conversion
- Gratuit avec limitations

**PDFescape** : [https://www.pdfescape.com/](https://www.pdfescape.com/)
- Édition de PDF en ligne
- Formulaires, annotations

**iLovePDF** : [https://www.ilovepdf.com/](https://www.ilovepdf.com/)
- Multiples outils PDF
- Interface simple

**Attention** :
- Données envoyées sur Internet
- Risques de confidentialité
- Privilégiez les outils locaux pour documents sensibles

## Conclusion

Linux Mint offre tous les outils nécessaires pour travailler efficacement avec des PDF, de la simple lecture avec Xreader aux manipulations avancées en ligne de commande. Que vous ayez besoin de lire des factures, annoter des documents, remplir des formulaires, ou créer des PDFs professionnels, les solutions sont là.

**Points clés à retenir** :

- **Xreader** : Lecteur simple et efficace (par défaut)
- **Okular** : Pour annotations et formulaires avancés
- **LibreOffice** : Création et export de PDFs
- **PDFtk / Ghostscript** : Manipulation en ligne de commande
- **OCRmyPDF** : Ajouter du texte aux scans
- **PDF Arranger** : Réorganiser et fusionner (graphique)

**Pour débuter** :
1. Utilisez Xreader pour lire vos PDFs
2. Créez vos PDFs depuis LibreOffice
3. Explorez Okular si vous avez besoin d'annoter

**Pour aller plus loin** :
- Automatisez avec PDFtk et scripts
- Maîtrisez OCR pour documents scannés
- Sécurisez vos PDFs importants

Le format PDF est universel et Linux Mint vous donne tout ce qu'il faut pour en tirer le meilleur parti, gratuitement et en toute liberté !

---


⏭️ [Warpinator (Échange de fichiers sur le réseau local)](/05-applications-essentielles-et-outils-mint/08-warpinator.md)
