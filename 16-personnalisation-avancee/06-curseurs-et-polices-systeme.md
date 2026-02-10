🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 16.6 - Curseurs et polices système

## Introduction

Les polices et les curseurs sont des éléments visuels que vous voyez constamment lors de l'utilisation de votre ordinateur. Bien que souvent négligés, ils ont un impact considérable sur le confort visuel et l'expérience utilisateur globale.

Une police bien choisie améliore la lisibilité et réduit la fatigue oculaire, tandis qu'un curseur adapté rend la navigation plus agréable et peut même améliorer la productivité. Dans ce chapitre, nous allons découvrir comment personnaliser ces éléments essentiels de votre système Linux Mint.

---

## Comprendre les polices système

### Qu'est-ce qu'une police système ?

Une **police système** est la typographie utilisée pour afficher le texte dans l'interface de votre système d'exploitation :
- Menus et barres d'outils
- Noms de fichiers et dossiers
- Titres de fenêtres
- Texte dans les applications

**À ne pas confondre avec :**
- **Polices de documents** : Utilisées dans LibreOffice, etc.
- **Polices web** : Affichées dans les navigateurs
- **Polices de terminal** : Vues dans le chapitre précédent

Bien que techniquement vous utilisez les mêmes fichiers de polices, leur usage dans le système est géré différemment.

### Types de polices

**1. Polices Serif (avec empattements)**
- Exemples : Times New Roman, Georgia
- Caractéristiques : Petits traits aux extrémités des lettres
- Usage : Documents imprimés, textes longs
- Lisibilité : Excellente sur papier

**2. Polices Sans-Serif (sans empattements)**
- Exemples : Arial, Ubuntu, Roboto
- Caractéristiques : Lettres sans ornements
- Usage : Interfaces, écrans
- Lisibilité : Excellente sur écran

**3. Polices Monospace (chasse fixe)**
- Exemples : Courier, DejaVu Sans Mono
- Caractéristiques : Toutes les lettres ont la même largeur
- Usage : Code, terminal, tableaux
- Lisibilité : Parfaite pour l'alignement

**4. Polices Script/Decorative**
- Exemples : Comic Sans, Brush Script
- Caractéristiques : Stylistiques, parfois manuscrites
- Usage : Décorations, titres
- Lisibilité : Variable, non recommandé pour le système

### Formats de polices

**TrueType (.ttf)**
- Format le plus courant
- Bonne compatibilité
- Qualité correcte à toutes les tailles

**OpenType (.otf)**
- Format moderne et avancé
- Meilleure gestion des glyphes
- Supporte plus de caractères

**Web Fonts (.woff, .woff2)**
- Optimisés pour le web
- Rarement utilisés pour le système

---

## Polices par défaut de Linux Mint

### Polices préinstallées

Linux Mint vient avec plusieurs familles de polices :

**Famille Ubuntu**
- Ubuntu (Sans-Serif)
- Ubuntu Mono (Monospace)
- Ubuntu Condensed

**Famille DejaVu**
- DejaVu Sans
- DejaVu Serif
- DejaVu Sans Mono

**Famille Liberation**
- Liberation Sans (similaire à Arial)
- Liberation Serif (similaire à Times New Roman)
- Liberation Mono (similaire à Courier)

**Autres polices système**
- Noto Sans (support Unicode étendu)
- FreeSans, FreeSerif, FreeMono

### Configuration par défaut

**Cinnamon :**
- Police d'interface : Ubuntu 10
- Police de fenêtres : Ubuntu Bold 10
- Police de documents : Sans 11
- Police monospace : Monospace 11

---

## Installer de nouvelles polices

### Méthode 1 : Via le gestionnaire de polices (GUI)

C'est la méthode la plus simple pour les débutants.

**Étapes :**

1. **Téléchargez une police**
   - Depuis un site de polices (voir section suivante)
   - Format `.ttf` ou `.otf`

2. **Double-cliquez sur le fichier de police**
   - Un aperçu s'ouvre automatiquement
   - Vous voyez l'apparence de la police

3. **Cliquez sur "Installer"**
   - La police est installée pour votre utilisateur
   - Elle devient immédiatement disponible

**Alternative : Gestionnaire de polices**

1. Ouvrez le **Gestionnaire de polices**
   - Menu → Préférences → Polices
   - Ou lancez `gnome-font-viewer`

2. Cliquez sur le bouton **"+"** ou **"Installer"**

3. Sélectionnez votre fichier de police

4. Confirmez l'installation

### Méthode 2 : Installation manuelle (pour votre utilisateur)

Cette méthode vous donne plus de contrôle.

**Pour votre utilisateur uniquement :**

```bash
# Créer le dossier de polices s'il n'existe pas
mkdir -p ~/.local/share/fonts

# Copier vos fichiers de polices
cp /chemin/vers/police.ttf ~/.local/share/fonts/

# Mettre à jour le cache des polices
fc-cache -fv
```

**Vérifier l'installation :**
```bash
fc-list | grep "NomDeLaPolice"
```

### Méthode 3 : Installation système (pour tous les utilisateurs)

**Pour tous les utilisateurs du système :**

```bash
# Copier dans le dossier système
sudo cp /chemin/vers/police.ttf /usr/share/fonts/truetype/

# Ou créer un dossier spécifique
sudo mkdir -p /usr/share/fonts/truetype/ma-police  
sudo cp /chemin/vers/police.ttf /usr/share/fonts/truetype/ma-police/  

# Mettre à jour le cache
sudo fc-cache -fv
```

### Méthode 4 : Installer plusieurs polices d'un coup

**Si vous avez un dossier avec plusieurs polices :**

```bash
# Copier tout le dossier
cp -r /chemin/vers/dossier-polices/* ~/.local/share/fonts/

# Mettre à jour le cache
fc-cache -fv
```

### Installer depuis un fichier .zip

Beaucoup de polices sont distribuées en archives.

**Étapes :**

```bash
# Se placer dans le dossier de téléchargement
cd ~/Téléchargements

# Extraire l'archive
unzip nom-police.zip -d nom-police

# Installer les polices
cp nom-police/*.ttf ~/.local/share/fonts/

# Mettre à jour le cache
fc-cache -fv
```

---

## Où trouver des polices gratuites ?

### Sites de polices recommandés

**1. Google Fonts**
- URL : [fonts.google.com](https://fonts.google.com/)
- **Avantages :** Toutes gratuites et libres, haute qualité
- **Polices populaires :** Roboto, Open Sans, Montserrat, Lato

**2. Font Squirrel**
- URL : [fontsquirrel.com](https://www.fontsquirrel.com/)
- **Avantages :** Uniquement des polices libres d'usage commercial
- **Sélection :** Très bien triée et testée

**3. DaFont**
- URL : [dafont.com](https://www.dafont.com/)
- **Avantages :** Énorme collection
- **Attention :** Vérifiez les licences (usage personnel vs commercial)

**4. 1001 Fonts**
- URL : [1001fonts.com](https://www.1001fonts.com/)
- **Avantages :** Grande variété
- **Attention :** Vérifiez les licences

**5. Font Library**
- URL : [fontlibrary.org](https://fontlibrary.org/)
- **Avantages :** Uniquement des polices open source
- **Qualité :** Variable mais légal

**6. Adobe Fonts (Creative Cloud)**
- URL : [fonts.adobe.com](https://fonts.adobe.com/)
- **Avantages :** Polices professionnelles
- **Inconvénient :** Nécessite un abonnement Adobe

### Installer toutes les polices Google Fonts

Si vous voulez avoir accès à toutes les Google Fonts :

```bash
# Installer le paquet
sudo apt install fonts-google-fonts

# Ou via Git pour avoir les dernières versions
git clone https://github.com/google/fonts.git  
sudo cp -r fonts/* /usr/share/fonts/truetype/  
sudo fc-cache -fv  
```

**Attention :** Cela installera des centaines de polices et peut ralentir le chargement des menus de polices dans certaines applications.

---

## Configurer les polices système

### Accéder aux paramètres de polices

**Sur Cinnamon :**

1. **Menu** → **Préférences** → **Polices**

Ou :

1. **Menu** → **Paramètres système**
2. **Apparence** → **Polices**

**Sur MATE :**

1. **Menu** → **Préférences** → **Apparence**
2. Onglet **Polices**

**Sur Xfce :**

1. **Menu** → **Paramètres** → **Apparence**
2. Onglet **Polices**

### Paramètres disponibles

**1. Police d'application**
- Texte dans les menus, boutons, dialogues
- Recommandation : Sans-Serif, 10-11pt
- Exemple : Ubuntu 10

**2. Police de document**
- Contenu des documents par défaut
- Recommandation : Sans-Serif ou Serif, 11-12pt
- Exemple : Sans 11

**3. Police de bureau**
- Noms des icônes sur le bureau
- Recommandation : Sans-Serif, 10-11pt
- Exemple : Ubuntu 11

**4. Police de titre de fenêtre**
- Titres des fenêtres (barre supérieure)
- Recommandation : Sans-Serif Bold, 10-11pt
- Exemple : Ubuntu Bold 10

**5. Police à chasse fixe**
- Terminal, éditeurs de code
- Recommandation : Monospace, 10-12pt
- Exemple : DejaVu Sans Mono 10

### Réglages avancés

**Anticrénelage (Antialiasing)**
- Lisse les bords des caractères
- Options : Aucun, Sous-pixel, Standard
- Recommandation : **Sous-pixel** pour LCD, **Standard** pour les autres

**Hinting (Optimisation)**
- Ajuste les polices pour les aligner sur la grille de pixels
- Options : Aucun, Léger, Moyen, Complet
- Recommandation : **Léger** ou **Moyen**

**Ordre RGB sous-pixel**
- Important pour l'anticrénelage sous-pixel
- Options : RGB, BGR, VRGB, VBGR
- Recommandation : **RGB** (pour la plupart des écrans)

**Facteur d'échelle**
- Taille globale du texte
- Valeurs : 0.5 à 3.0 (1.0 = normal)
- Usage : Écrans haute résolution (HiDPI)

### Exemples de configurations

**Configuration "Productivité" (lisible, moderne)**
```
Police d'application : Noto Sans 10  
Police de document : Noto Sans 11  
Police de bureau : Noto Sans 10  
Police de titre : Noto Sans Bold 10  
Police monospace : JetBrains Mono 11  
```

**Configuration "Élégante" (style Ubuntu)**
```
Police d'application : Ubuntu 10  
Police de document : Ubuntu 11  
Police de bureau : Ubuntu 11  
Police de titre : Ubuntu Bold 10  
Police monospace : Ubuntu Mono 11  
```

**Configuration "Classique" (style Windows)**
```
Police d'application : Liberation Sans 10  
Police de document : Liberation Serif 11  
Police de bureau : Liberation Sans 10  
Police de titre : Liberation Sans Bold 10  
Police monospace : Liberation Mono 10  
```

**Configuration "Grande lisibilité" (pour malvoyants)**
```
Police d'application : Noto Sans 14  
Police de document : Noto Sans 14  
Police de bureau : Noto Sans 14  
Police de titre : Noto Sans Bold 14  
Police monospace : DejaVu Sans Mono 13  
Facteur d'échelle : 1.25  
```

---

## Polices recommandées pour Linux

### Polices d'interface (Sans-Serif)

**1. Roboto**
- Créée par Google
- Moderne et très lisible
- Variantes : Light, Regular, Medium, Bold
- **Installation :** Via Google Fonts
```bash
sudo apt install fonts-roboto
```

**2. Noto Sans**
- Créée par Google
- Support Unicode exceptionnel
- Couvre presque toutes les langues
```bash
sudo apt install fonts-noto
```

**3. Inter**
- Optimisée pour les interfaces
- Excellente à petites tailles
- Très moderne
```bash
# Via téléchargement depuis GitHub
wget https://github.com/rsms/inter/releases/download/v3.19/Inter-3.19.zip  
unzip Inter-3.19.zip  
cp Inter\ Desktop/*.ttf ~/.local/share/fonts/  
fc-cache -fv  
```

**4. SF Pro / SF Compact (style macOS)**
- Élégante et moderne
- Nécessite téléchargement manuel
- Excellente lisibilité

**5. Cantarell**
- Police par défaut de GNOME
- Optimisée pour les écrans
```bash
sudo apt install fonts-cantarell
```

### Polices monospace (pour le code)

**1. Fira Code**
- Avec ligatures pour le code
- Très populaire chez les développeurs
```bash
sudo apt install fonts-firacode
```

**2. JetBrains Mono**
- Créée pour l'IDE IntelliJ
- Excellente lisibilité
```bash
# Via téléchargement
wget https://download.jetbrains.com/fonts/JetBrainsMono-2.304.zip  
unzip JetBrainsMono-2.304.zip  
cp fonts/ttf/*.ttf ~/.local/share/fonts/  
fc-cache -fv  
```

**3. Cascadia Code**
- Police de Microsoft
- Ligatures optionnelles
```bash
# Via téléchargement depuis GitHub
wget https://github.com/microsoft/cascadia-code/releases/download/v2111.01/CascadiaCode-2111.01.zip
```

**4. Source Code Pro**
- Créée par Adobe
- Très claire et lisible
```bash
sudo apt install fonts-source-code-pro
```

**5. Hack**
- Spécialement conçue pour le code
- Distinctions claires (0 vs O, l vs 1)
```bash
sudo apt install fonts-hack
```

---

## Comprendre les curseurs

### Qu'est-ce qu'un curseur ?

Le **curseur** (ou **pointeur de souris**) est l'icône qui représente la position de votre souris à l'écran. Il change de forme selon le contexte :
- **Flèche** : Navigation normale
- **Main** : Lien cliquable
- **I-beam** : Sélection de texte
- **Sablier/Roue** : Chargement
- **Double flèche** : Redimensionnement
- **Croix** : Sélection précise

### Thèmes de curseurs

Un **thème de curseurs** est un ensemble complet de curseurs cohérents, incluant toutes les variations nécessaires (normal, chargement, redimensionnement, etc.).

**Curseurs par défaut sur Linux Mint :**
- DMZ-White (blanc)
- DMZ-Black (noir)
- Adwaita (curseur GNOME)

---

## Installer des thèmes de curseurs

### Méthode 1 : Via le gestionnaire de paramètres

**Sur Cinnamon :**

1. **Menu** → **Préférences** → **Thèmes**
2. Cliquez sur l'onglet **"Pointeurs"** (ou **"Curseurs"**)
3. Cliquez sur **"Ajouter/Supprimer"** en bas
4. Parcourez les thèmes disponibles
5. Cliquez sur **"Installer"** ou **"Télécharger"**

**Appliquer un curseur :**
1. Revenez à l'onglet "Pointeurs"
2. Sélectionnez le curseur dans la liste
3. Le changement est immédiat

### Méthode 2 : Installation manuelle

**Pour votre utilisateur uniquement :**

```bash
# Créer le dossier des curseurs
mkdir -p ~/.icons

# Télécharger et extraire un thème
unzip theme-curseur.zip -d ~/.icons/

# Le thème devrait apparaître dans les paramètres
```

**Pour tous les utilisateurs :**

```bash
# Extraire dans le dossier système
sudo unzip theme-curseur.zip -d /usr/share/icons/
```

**Note :** Le nom du dossier extrait doit contenir un fichier `index.theme` et un dossier `cursors/`.

### Structure d'un thème de curseurs

```
nom-du-theme/
├── index.theme          # Métadonnées du thème
└── cursors/             # Dossier contenant tous les curseurs
    ├── default
    ├── pointer
    ├── hand
    ├── text
    ├── wait
    └── ...
```

---

## Où trouver des thèmes de curseurs ?

### Sites recommandés

**1. Gnome-look.org (section Cursors)**
- URL : [gnome-look.org/browse?cat=107](https://www.gnome-look.org/browse?cat=107)
- Plus grande collection
- Notes et commentaires
- Téléchargements faciles

**2. Pling.com**
- URL : [pling.com](https://www.pling.com/)
- Interface moderne
- Même contenu que Gnome-look

**3. DeviantArt**
- Recherchez "Linux cursor theme"
- Beaucoup de créations artistiques
- Qualité variable

**4. GitHub**
- Recherchez "cursor theme"
- Souvent les versions les plus récentes
- Parfois plus technique à installer

### Thèmes de curseurs populaires

**1. Bibata**
- Moderne et élégant
- Plusieurs variantes (Original, Modern, Ice)
- Différentes tailles disponibles
- **Installation :**
```bash
wget https://github.com/ful1e5/Bibata_Cursor/releases/download/v2.0.3/Bibata-Modern-Classic.tar.gz  
tar -xvf Bibata-Modern-Classic.tar.gz  
mv Bibata-Modern-Classic ~/.icons/  
```

**2. Capitaine Cursors**
- Inspiré de macOS
- Épuré et professionnel
- Plusieurs couleurs
```bash
wget https://github.com/keeferrourke/capitaine-cursors/releases/download/r4/capitaine-cursors-r4.tar.gz  
tar -xvf capitaine-cursors-r4.tar.gz  
mv capitaine-cursors* ~/.icons/  
```

**3. Breeze (KDE)**
- Curseur par défaut de KDE Plasma
- Sobre et moderne
```bash
sudo apt install breeze-cursor-theme
```

**4. Numix**
- Curseurs circulaires
- Design minimaliste
```bash
sudo apt install numix-icon-theme-circle
```

**5. Vimix**
- Curseurs blancs sur fond noir (ou inverse)
- Très contrastés
- Bonne visibilité

**6. Oreo**
- Design coloré
- Plusieurs variantes
- Moderne et ludique

**7. Oxygen (KDE)**
- Curseur classique de KDE
- Fiable et bien testé
```bash
sudo apt install oxygen-cursor-theme
```

---

## Configurer les curseurs

### Taille du curseur

**Via l'interface graphique :**

1. **Menu** → **Préférences** → **Thèmes**
2. Onglet **"Pointeurs"**
3. Sélectionnez la taille : **Petite**, **Normale**, **Grande**, **Énorme**

**Ou modifiez via Tweaks (si installé) :**
```bash
sudo apt install gnome-tweaks
```

Puis : Tweaks → Apparence → Curseur

### Taille personnalisée

**Méthode avancée (via fichier de configuration) :**

Éditez `~/.Xresources` :
```bash
nano ~/.Xresources
```

Ajoutez :
```
Xcursor.size: 24
```

Appliquez :
```bash
xrdb -merge ~/.Xresources
```

**Tailles courantes :**
- 16 : Très petit
- 24 : Petit (par défaut)
- 32 : Moyen
- 48 : Grand
- 64 : Très grand

### Curseur pour gauchers

Certains thèmes proposent des versions "left-handed" (miroir du curseur).

**Changer l'orientation :**
1. Paramètres → Souris
2. Option "Main primaire" → Gauche

**Note :** Cela change aussi les boutons de la souris.

---

## Configurations recommandées

### Configuration "Productivité professionnelle"

**Polices :**
```
Interface : Inter 10  
Document : Inter 11  
Bureau : Inter 10  
Titre : Inter Semibold 10  
Monospace : JetBrains Mono 11  
```

**Curseur :**
- Bibata Modern Classic
- Taille : 24 ou 32

**Avantages :**
- Très lisible
- Moderne et sobre
- Parfait pour de longues sessions

### Configuration "Développeur"

**Polices :**
```
Interface : Roboto 10  
Document : Roboto 11  
Bureau : Roboto 10  
Titre : Roboto Bold 10  
Monospace : Fira Code 11 (avec ligatures)  
```

**Curseur :**
- Capitaine Cursors
- Taille : 24

**Avantages :**
- Code très lisible
- Ligatures pour symboles de code
- Curseur discret

### Configuration "Créative"

**Polices :**
```
Interface : SF Pro 10  
Document : SF Pro 11  
Bureau : SF Pro 10  
Titre : SF Pro Semibold 10  
Monospace : SF Mono 11  
```

**Curseur :**
- Oreo Cursors
- Taille : 32

**Avantages :**
- Esthétique macOS
- Moderne et élégant
- Curseur visible et stylé

### Configuration "Accessibilité"

**Polices :**
```
Interface : Noto Sans 14  
Document : Noto Sans 15  
Bureau : Noto Sans 14  
Titre : Noto Sans Bold 14  
Monospace : DejaVu Sans Mono 13  
Facteur d'échelle : 1.3  
```

**Curseur :**
- DMZ-Black ou Breeze
- Taille : 48 ou 64

**Avantages :**
- Très lisible pour malvoyants
- Curseur grande taille
- Contraste élevé

---

## Gérer vos polices et curseurs

### Lister les polices installées

**Via commande :**
```bash
# Lister toutes les polices
fc-list

# Lister par famille
fc-list : family

# Rechercher une police spécifique
fc-list | grep -i "roboto"

# Afficher les chemins
fc-list : file
```

**Via GUI :**
```bash
# Gestionnaire de polices
gnome-font-viewer
```

### Désinstaller une police

**Police utilisateur :**
```bash
# Supprimer le fichier
rm ~/.local/share/fonts/nom-police.ttf

# Mettre à jour le cache
fc-cache -fv
```

**Police système :**
```bash
# Supprimer
sudo rm /usr/share/fonts/truetype/nom-police/nom-police.ttf

# Mettre à jour le cache
sudo fc-cache -fv
```

### Désinstaller un thème de curseurs

**Curseur utilisateur :**
```bash
rm -rf ~/.icons/nom-theme-curseur
```

**Curseur système :**
```bash
sudo rm -rf /usr/share/icons/nom-theme-curseur
```

### Organiser vos polices

**Créer des catégories :**
```bash
mkdir -p ~/.local/share/fonts/Sans-Serif  
mkdir -p ~/.local/share/fonts/Serif  
mkdir -p ~/.local/share/fonts/Monospace  
mkdir -p ~/.local/share/fonts/Decoratives  
```

**Organiser par projet :**
```bash
mkdir -p ~/.local/share/fonts/Projet-A  
mkdir -p ~/.local/share/fonts/Projet-B  
```

---

## Polices et curseurs pour cas spécifiques

### Pour développeurs

**Polices monospace avec ligatures :**
- Fira Code
- JetBrains Mono
- Cascadia Code
- Hasklig

**Configuration VS Code :**
```json
{
  "editor.fontFamily": "'JetBrains Mono', 'Fira Code', monospace",
  "editor.fontLigatures": true,
  "editor.fontSize": 13
}
```

### Pour designers

**Polices élégantes :**
- SF Pro (macOS style)
- Raleway
- Montserrat
- Poppins

**Curseurs précis :**
- Bibata
- Capitaine Cursors

### Pour gamers

**Polices futuristes :**
- Orbitron
- Exo
- Audiowide

**Curseurs thématiques :**
- Recherchez "gaming cursor theme" sur Gnome-look

### Pour étudiants/rédaction

**Polices lisibles :**
- Noto Sans/Serif
- Liberation Sans/Serif
- Linux Libertine (excellent pour les documents)

**Curseur neutre :**
- DMZ-White
- Adwaita

---

## Optimisation des polices

### Améliorer le rendu des polices

**Fichier de configuration : ~/.config/fontconfig/fonts.conf**

Créez le fichier s'il n'existe pas :
```bash
mkdir -p ~/.config/fontconfig  
nano ~/.config/fontconfig/fonts.conf  
```

**Configuration optimale :**
```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <!-- Antialiasing -->
  <match target="font">
    <edit name="antialias" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

  <!-- Hinting -->
  <match target="font">
    <edit name="hinting" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

  <!-- Hinting style -->
  <match target="font">
    <edit name="hintstyle" mode="assign">
      <const>hintslight</const>
    </edit>
  </match>

  <!-- Sous-pixel RGB -->
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>rgb</const>
    </edit>
  </match>

  <!-- LCD filter -->
  <match target="font">
    <edit name="lcdfilter" mode="assign">
      <const>lcddefault</const>
    </edit>
  </match>
</fontconfig>
```

**Appliquer les changements :**
```bash
fc-cache -fv
```

### Polices pour écrans HiDPI (haute résolution)

**Augmenter le facteur d'échelle :**

1. Paramètres → Polices
2. Facteur d'échelle : 1.25, 1.5, ou 2.0

**Ou via variable d'environnement :**
```bash
# Ajouter dans ~/.profile
export GDK_SCALE=2  
export GDK_DPI_SCALE=0.5  
```

### Polices légères pour anciennes machines

**Polices peu gourmandes :**
- DejaVu (standard, bien optimisée)
- Liberation (légère)
- Droid Sans (simple)

**Désactiver l'antialiasing :**
- Paramètres → Polices → Anticrénelage : Aucun
- Améliore les performances sur matériel ancien

---

## Dépannage

### Les polices ne s'affichent pas après installation

**Solutions :**

1. **Mettre à jour le cache**
```bash
fc-cache -fv
```

2. **Vérifier que la police est installée**
```bash
fc-list | grep "NomPolice"
```

3. **Redémarrer les applications**
   - Fermez et rouvrez l'application
   - Certaines applications ne rechargent les polices qu'au démarrage

4. **Se déconnecter/reconnecter**
   - Pour les polices système, parfois nécessaire

### Le curseur ne change pas

**Solutions :**

1. **Vérifier le fichier index.theme**
```bash
cat ~/.icons/nom-theme/index.theme
```
Doit contenir une section `[Icon Theme]`

2. **Appliquer via gsettings (Cinnamon)**
```bash
gsettings set org.cinnamon.desktop.interface cursor-theme 'nom-theme'  
gsettings set org.cinnamon.desktop.interface cursor-size 24  
```

3. **Créer un lien symbolique**
```bash
ln -s ~/.icons/nom-theme/cursors ~/.icons/default
```

4. **Redémarrer Cinnamon**
   - `Alt+F2` → tapez `r` → Entrée
   - Ou déconnexion/reconnexion

### Les caractères spéciaux ne s'affichent pas

**Solutions :**

1. **Installer Noto Fonts (support Unicode complet)**
```bash
sudo apt install fonts-noto fonts-noto-cjk fonts-noto-color-emoji
```

2. **Installer les polices de langues spécifiques**
```bash
# Arabe
sudo apt install fonts-arabeyes

# Chinois
sudo apt install fonts-noto-cjk

# Japonais
sudo apt install fonts-takao

# Coréen
sudo apt install fonts-nanum
```

### Polices floues ou pixelisées

**Solutions :**

1. **Activer l'antialiasing**
   - Paramètres → Polices → Anticrénelage : Sous-pixel

2. **Ajuster le hinting**
   - Essayez "Léger" ou "Moyen"

3. **Vérifier le DPI**
```bash
xdpyinfo | grep resolution
```
Si différent de 96, ajustez dans Paramètres → Polices

4. **Installer une meilleure version de la police**
   - Les versions OTF sont parfois meilleures que TTF

### Le curseur disparaît ou devient invisible

**Solutions :**

1. **Changer de thème de curseur**
   - Sélectionnez DMZ-White ou DMZ-Black

2. **Augmenter la taille**
   - Paramètres → Curseurs → Taille : Grande

3. **Vérifier les pilotes graphiques**
```bash
sudo ubuntu-drivers devices
```

4. **Réinitialiser les paramètres**
```bash
gsettings reset org.cinnamon.desktop.interface cursor-theme  
gsettings reset org.cinnamon.desktop.interface cursor-size  
```

---

## Créer votre propre thème de curseurs

Pour les utilisateurs avancés qui veulent aller plus loin.

### Outils nécessaires

**Inkscape :** Pour créer les images SVG
```bash
sudo apt install inkscape
```

**xcursorgen :** Pour compiler les curseurs
```bash
sudo apt install x11-apps
```

### Processus de base

1. **Créer les images** (PNG, 24x24, 32x32, 48x48, etc.)
2. **Créer un fichier de configuration** (.cursor)
3. **Compiler avec xcursorgen**
4. **Créer index.theme**
5. **Tester**

**Exemple de fichier .cursor :**
```
24 12 12 pointer.png
32 16 16 pointer-32.png
48 24 24 pointer-48.png
```

**Compiler :**
```bash
xcursorgen pointer.cursor cursors/pointer
```

---

## Synchroniser polices et curseurs entre machines

### Sauvegarder votre configuration

**Polices :**
```bash
# Archiver vos polices personnelles
tar -czf mes-polices.tar.gz ~/.local/share/fonts/
```

**Curseurs :**
```bash
# Archiver vos curseurs
tar -czf mes-curseurs.tar.gz ~/.icons/
```

**Paramètres :**
```bash
# Exporter les paramètres
dconf dump /org/cinnamon/desktop/interface/ > interface-settings.dconf
```

### Restaurer sur une autre machine

**Polices :**
```bash
tar -xzf mes-polices.tar.gz -C ~/  
fc-cache -fv  
```

**Curseurs :**
```bash
tar -xzf mes-curseurs.tar.gz -C ~/
```

**Paramètres :**
```bash
dconf load /org/cinnamon/desktop/interface/ < interface-settings.dconf
```

---

## Ressources et inspiration

### Sites pour trouver des inspirations

**Polices :**
- [Google Fonts](https://fonts.google.com/)
- [FontPair](https://fontpair.co/) - Combinaisons de polices
- [Typewolf](https://www.typewolf.com/) - Tendances typographiques

**Curseurs :**
- [Gnome-look Cursors](https://www.gnome-look.org/browse?cat=107)
- [DeviantArt](https://www.deviantart.com/) - Recherche "cursor theme"

### Communautés

**Reddit :**
- r/unixporn - Configurations visuelles
- r/typography - Pour les polices

**Forums :**
- Linux Mint Forums - Section Customization
- GNOME Forums

---

## Aller plus loin

### Polices variables

Les **polices variables** sont une technologie moderne qui permet d'ajuster le poids, la largeur, etc. dynamiquement.

**Exemples :**
- Inter (version variable)
- Recursive
- Anybody

**Support :** Nécessite des applications récentes et fontconfig moderne.

### Emoji et symboles

**Installer une police emoji :**
```bash
sudo apt install fonts-noto-color-emoji
```

**Configurer l'affichage des emojis :**
Ajoutez dans `~/.config/fontconfig/fonts.conf` :
```xml
<alias>
  <family>sans-serif</family>
  <prefer>
    <family>Noto Sans</family>
    <family>Noto Color Emoji</family>
  </prefer>
</alias>
```

---

## Résumé

Dans ce chapitre, vous avez appris :

- ✅ La différence entre les types de polices (Serif, Sans-Serif, Monospace)
- ✅ Comment installer des polices (GUI et terminal)
- ✅ Où trouver des polices gratuites et de qualité
- ✅ Comment configurer les polices système
- ✅ Les polices recommandées pour différents usages
- ✅ Ce que sont les curseurs et thèmes de curseurs
- ✅ Comment installer et configurer des curseurs
- ✅ Les curseurs populaires et où les trouver
- ✅ Comment optimiser le rendu des polices
- ✅ Le dépannage des problèmes courants
- ✅ Des configurations complètes pour différents cas d'usage

Les polices et curseurs sont des détails qui peuvent sembler mineurs, mais qui ont un impact majeur sur votre confort quotidien. Prenez le temps de trouver la combinaison qui rend votre expérience Linux Mint vraiment agréable !

---


⏭️ [Animations et effets](/16-personnalisation-avancee/07-animations-et-effets.md)
