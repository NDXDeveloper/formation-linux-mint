🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 16.1 - Thèmes et icônes (téléchargement et installation)

## Introduction

La personnalisation de l'apparence de votre système Linux Mint est l'un des grands avantages de cette distribution. Contrairement à d'autres systèmes d'exploitation, vous avez un contrôle total sur l'aspect visuel de votre bureau. Les thèmes et les icônes sont deux éléments essentiels pour personnaliser votre environnement de travail et le rendre vraiment unique.

Dans ce chapitre, nous allons découvrir comment télécharger, installer et appliquer des thèmes et des packs d'icônes pour transformer l'apparence de votre Linux Mint.

---

## Qu'est-ce qu'un thème ?

Un **thème** est un ensemble d'éléments visuels qui modifie l'apparence de votre interface. Il peut inclure :

- **L'apparence des fenêtres** : bordures, barres de titre, boutons de fermeture/réduction
- **Les contrôles** : boutons, menus déroulants, barres de défilement
- **Les couleurs** : palette générale de l'interface
- **Les effets** : ombres, transparence, animations

Il existe plusieurs types de thèmes :
- **Thèmes GTK** : pour les applications utilisant GTK (la plupart des applications Linux)
- **Thèmes de fenêtres** : pour l'apparence des bordures et décorations de fenêtres
- **Thèmes complets** : qui incluent les deux

---

## Qu'est-ce qu'un pack d'icônes ?

Un **pack d'icônes** est un ensemble cohérent d'icônes qui remplace les icônes par défaut de votre système. Cela inclut :

- Les icônes d'applications dans le menu
- Les icônes de fichiers et dossiers
- Les icônes de la barre des tâches
- Les icônes système (réseau, son, batterie, etc.)

Les packs d'icônes peuvent avoir différents styles : plat, minimaliste, coloré, 3D, etc.

---

## Où trouver des thèmes et icônes ?

### 1. Le gestionnaire de thèmes intégré

Linux Mint dispose d'un système intégré pour télécharger des thèmes directement depuis l'interface :

**Pour y accéder :**
1. Ouvrez le **Menu** → **Préférences** → **Thèmes**
2. Dans les onglets du haut, vous verrez plusieurs sections
3. Descendez en bas de chaque section et cliquez sur **"Ajouter/Supprimer"**

Cette méthode est la plus simple et la plus sûre pour les débutants.

### 2. Sites web spécialisés

Plusieurs sites proposent des milliers de thèmes et d'icônes gratuits :

**Sites principaux :**

- **[Gnome-look.org](https://www.gnome-look.org/)** : La référence pour les thèmes GTK et les icônes
  - Section GTK 3/4 Themes pour les thèmes
  - Section Full Icon Themes pour les icônes complètes

- **[Cinnamon-Spices](https://cinnamon-spices.linuxmint.com/)** : Le site officiel de Linux Mint
  - Thèmes spécialement compatibles avec Cinnamon

- **[Pling.com](https://www.pling.com/)** : Plateforme regroupant plusieurs catégories
  - Interface moderne et bien organisée

### 3. GitHub

De nombreux développeurs publient leurs créations sur GitHub. C'est souvent là que vous trouverez les versions les plus récentes et les plus à jour.

---

## Installation des thèmes

### Méthode 1 : Via le gestionnaire de thèmes (recommandée pour débutants)

**Étapes :**

1. Ouvrez **Menu** → **Préférences** → **Thèmes**
2. Cliquez sur l'onglet **"Bureau"** ou **"Fenêtres"** selon ce que vous voulez modifier
3. En bas de la liste, cliquez sur **"Ajouter/Supprimer"**
4. Une nouvelle fenêtre s'ouvre avec une liste de thèmes disponibles
5. Parcourez la liste et cliquez sur **"Télécharger"** à côté du thème qui vous plaît
6. Une fois téléchargé, le thème apparaît dans votre liste et vous pouvez l'appliquer immédiatement

**Avantages :**
- Simple et rapide
- Installation automatique
- Pas besoin de manipuler des fichiers

### Méthode 2 : Installation manuelle (téléchargement depuis un site)

Lorsque vous trouvez un thème sur un site web, voici comment l'installer :

**Étapes :**

1. **Téléchargez le thème** depuis le site (généralement un fichier `.zip` ou `.tar.gz`)

2. **Extrayez l'archive** :
   - Clic droit sur le fichier téléchargé
   - Choisissez **"Extraire ici"** ou **"Extraire vers..."**

3. **Placez le dossier du thème au bon endroit** :

   Vous avez deux options :

   - **Installation pour votre utilisateur uniquement** (recommandé) :
     - Ouvrez le gestionnaire de fichiers (Nemo)
     - Appuyez sur `Ctrl + H` pour afficher les fichiers cachés
     - Naviguez vers : `/home/votre-nom-utilisateur/.themes/`
     - Si le dossier `.themes` n'existe pas, créez-le (clic droit → Nouveau dossier)
     - Copiez le dossier extrait du thème dans `.themes/`

   - **Installation pour tous les utilisateurs** :
     - Ouvrez le terminal
     - Tapez : `sudo cp -r /chemin/vers/le/dossier/theme /usr/share/themes/`
     - Remplacez `/chemin/vers/le/dossier/theme` par le chemin réel

4. **Appliquez le thème** :
   - Ouvrez **Menu** → **Préférences** → **Thèmes**
   - Votre nouveau thème devrait apparaître dans la liste
   - Cliquez dessus pour l'appliquer

### Méthode 3 : Via le terminal (pour utilisateurs avancés)

Certains thèmes proposent des scripts d'installation automatique :

```bash
# Exemple générique (suivez toujours les instructions du thème)
cd ~/Téléchargements  
git clone https://github.com/utilisateur/nom-du-theme.git  
cd nom-du-theme  
./install.sh
```

---

## Installation des packs d'icônes

Le processus est très similaire à celui des thèmes.

### Méthode 1 : Via le gestionnaire de thèmes

1. Ouvrez **Menu** → **Préférences** → **Thèmes**
2. Cliquez sur l'onglet **"Icônes"**
3. Cliquez sur **"Ajouter/Supprimer"** en bas de la liste
4. Parcourez et téléchargez le pack d'icônes de votre choix
5. Une fois téléchargé, sélectionnez-le dans la liste pour l'appliquer

### Méthode 2 : Installation manuelle

**Étapes :**

1. **Téléchargez le pack d'icônes** (fichier `.zip` ou `.tar.gz`)

2. **Extrayez l'archive**

3. **Placez le dossier au bon endroit** :

   - **Pour votre utilisateur uniquement** :
     - Appuyez sur `Ctrl + H` dans le gestionnaire de fichiers
     - Naviguez vers : `/home/votre-nom-utilisateur/.icons/`
     - Créez le dossier `.icons` s'il n'existe pas
     - Copiez le dossier du pack d'icônes dans `.icons/`

   - **Pour tous les utilisateurs** :
     - Via terminal : `sudo cp -r /chemin/vers/icones /usr/share/icons/`

4. **Appliquez le pack d'icônes** :
   - Menu → Préférences → Thèmes → Onglet Icônes
   - Sélectionnez votre nouveau pack

**Note importante :** Après avoir copié un pack d'icônes, vous devrez peut-être actualiser le cache :

```bash
gtk-update-icon-cache ~/.icons/nom-du-pack-icones
```

---

## Appliquer et gérer vos thèmes

### Accéder aux paramètres de thèmes

**Menu** → **Préférences** → **Thèmes**

Vous verrez plusieurs onglets :

- **Bureau** : L'apparence générale des fenêtres et contrôles
- **Icônes** : Le pack d'icônes actif
- **Pointeurs** : L'apparence du curseur de la souris
- **Fenêtres** : Les bordures et décorations de fenêtres
- **Autres paramètres** : Options supplémentaires

### Appliquer un thème complet

Pour un look cohérent, vous pouvez :

1. Choisir un thème dans l'onglet **Bureau**
2. Choisir un pack d'icônes assorti dans l'onglet **Icônes**
3. Ajuster les curseurs si nécessaire dans l'onglet **Pointeurs**

**Astuce :** Beaucoup de créateurs proposent des ensembles complets (thème + icônes + curseurs) pour une harmonie parfaite.

### Prévisualiser avant d'appliquer

- Dans la fenêtre de Thèmes, vous pouvez voir un aperçu en miniature
- Cliquez simplement sur différents thèmes/icônes pour les prévisualiser instantanément
- Il n'y a aucun risque : vous pouvez toujours revenir au thème précédent

### Revenir au thème par défaut

Si un thème ne vous convient pas ou cause des problèmes :

1. Ouvrez **Menu** → **Préférences** → **Thèmes**
2. Sélectionnez **"Mint-Y"** ou **"Mint-X"** (thèmes par défaut de Mint)
3. Pour les icônes, choisissez **"Mint-Y"** ou **"Mint-X"**

---

## Conseils et bonnes pratiques

### Pour les débutants

1. **Commencez simple** : Utilisez d'abord le gestionnaire intégré plutôt que l'installation manuelle

2. **Vérifiez la compatibilité** :
   - Assurez-vous que le thème est compatible avec votre version de Cinnamon
   - Regardez les commentaires et évaluations sur les sites de téléchargement

3. **Lisez les instructions** :
   - Chaque thème peut avoir des particularités
   - Certains nécessitent des ajustements supplémentaires

4. **Testez progressivement** :
   - Changez d'abord juste les icônes
   - Puis testez un nouveau thème
   - Évitez de tout changer en même temps

### Problèmes courants et solutions

**Le thème ne s'affiche pas après installation :**
- Vérifiez que vous l'avez bien placé dans `.themes` (avec le point)
- Assurez-vous d'avoir extrait le dossier complet (pas juste les fichiers)
- Redémarrez la session (déconnexion/reconnexion)

**Certaines applications ne suivent pas le thème :**
- C'est normal pour certaines applications (Flatpak, Snap)
- Les applications Qt (KDE) nécessitent parfois des thèmes spécifiques

**Les icônes sont incomplètes :**
- Certains packs ne couvrent pas toutes les applications
- Le système utilisera les icônes par défaut pour ce qui manque
- Vous pouvez combiner plusieurs packs (mais c'est complexe)

**Performances ralenties :**
- Certains thèmes avec beaucoup d'effets peuvent ralentir les ordinateurs anciens
- Privilégiez les thèmes "légers" ou "light"
- Désactivez les animations dans les paramètres

### Recommandations de sécurité

- **Téléchargez uniquement depuis des sources fiables** :
  - Sites officiels mentionnés plus haut
  - Dépôts GitHub vérifiés
  - Évitez les sites douteux

- **Vérifiez les permissions** :
  - Un thème ne devrait jamais demander sudo lors de l'application
  - Méfiez-vous des scripts d'installation suspects

- **Lisez les avis** :
  - Consultez les commentaires sur Gnome-look
  - Vérifiez les notes et le nombre de téléchargements

### Thèmes populaires recommandés

Voici quelques thèmes et icônes populaires et fiables :

**Thèmes GTK :**
- **Arc** : Moderne et élégant, plusieurs variantes
- **Adapta** : Design Material, très propre
- **Nordic** : Inspiré de Nord, tons bleus apaisants
- **Dracula** : Pour les amateurs de thèmes sombres
- **Gruvbox** : Palette de couleurs chaudes et rétro

**Packs d'icônes :**
- **Papirus** : Très complet, style moderne et coloré
- **Numix-Circle** : Icônes circulaires minimalistes
- **Tela** : Design moderne et cohérent
- **Candy** : Coloré et ludique
- **La Capitaine** : Style macOS

---

## Aller plus loin

Une fois à l'aise avec les thèmes et icônes, vous pouvez explorer :

- **Les extensions Cinnamon** (voir chapitre 16.2) pour ajouter des fonctionnalités
- **Les desklets et applets** (voir chapitre 16.3) pour personnaliser le bureau
- **La personnalisation du terminal** (voir chapitre 16.5)
- **Les curseurs personnalisés** (voir chapitre 16.6)

N'ayez pas peur d'expérimenter ! C'est en testant différents styles que vous trouverez l'apparence qui vous convient le mieux et dans laquelle vous serez le plus productif.

---

## Résumé

Dans ce chapitre, vous avez appris :

- ✅ Ce que sont les thèmes et les packs d'icônes
- ✅ Où trouver des thèmes de qualité
- ✅ Comment installer des thèmes via le gestionnaire intégré
- ✅ Comment installer manuellement des thèmes téléchargés
- ✅ Comment appliquer et gérer vos personnalisations
- ✅ Les bonnes pratiques pour une personnalisation réussie

La personnalisation de Linux Mint est un processus amusant et sans risque. N'hésitez pas à tester différentes combinaisons jusqu'à trouver celle qui rend votre expérience quotidienne la plus agréable !

---


⏭️ [Extensions Cinnamon (ou MATE/Xfce)](/16-personnalisation-avancee/02-extensions-cinnamon.md)
