🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.3 Le gestionnaire de fichiers (Nemo)

## Introduction

Le gestionnaire de fichiers est l'application que vous utiliserez quotidiennement pour organiser vos documents, photos, vidéos, musique et tous vos autres fichiers. C'est l'équivalent de l'**Explorateur Windows** sous Linux Mint.

Sous Cinnamon, ce gestionnaire s'appelle **Nemo** (sous MATE, c'est **Caja**, et sous Xfce, c'est **Thunar**). Dans ce chapitre, nous nous concentrerons sur Nemo, mais les concepts restent très similaires entre les trois.

## Ouvrir Nemo

Il existe plusieurs façons d'ouvrir le gestionnaire de fichiers :

**Méthode 1 : Depuis le panneau**
- Cliquez sur l'icône de dossier dans les lanceurs rapides du panneau
- Généralement, c'est la deuxième ou troisième icône après le menu

**Méthode 2 : Depuis le menu**
- Ouvrez le menu Linux Mint
- Tapez "fichiers" ou "nemo" dans la recherche
- Ou allez dans Accessoires → Fichiers

**Méthode 3 : Raccourci clavier**
- **Super + E** (comme Windows + E sous Windows)
- Fonctionne si configuré dans les raccourcis clavier

**Méthode 4 : Depuis les emplacements rapides**
- Menu → Dossier personnel (dans la colonne de droite)
- Clic sur une icône de dossier sur le bureau

**Méthode 5 : En ligne de commande**
- Ouvrez un terminal et tapez : `nemo`
- Ou `nemo /chemin/vers/dossier` pour ouvrir un dossier précis

## L'interface de Nemo

Découvrons les différentes zones de la fenêtre Nemo.

### 1. La barre de titre

En haut de la fenêtre, elle affiche :
- Le nom du dossier actuel
- Les boutons de contrôle de fenêtre (minimiser, maximiser, fermer)
- Un menu hamburger (≡) pour les options avancées

### 2. La barre d'outils principale

Juste sous la barre de titre, vous trouvez plusieurs éléments importants.

#### Boutons de navigation

**Flèche retour (←)** : revenir au dossier précédent
- Fonctionne comme le bouton "Précédent" d'un navigateur web
- Raccourci : **Alt + ←**

**Flèche avant (→)** : aller au dossier suivant
- Si vous êtes revenu en arrière, permet d'avancer à nouveau
- Raccourci : **Alt + →**

**Flèche vers le haut (↑)** : remonter au dossier parent
- Si vous êtes dans `/home/votre-nom/Documents`, remonte à `/home/votre-nom`
- Raccourci : **Alt + ↑**

**Astuce :** Maintenez le clic sur ces flèches pour voir l'historique !

#### La barre d'adresse (chemin)

Affiche votre emplacement actuel dans l'arborescence.

**Deux modes d'affichage :**

**Mode boutons (par défaut) :**
- Chaque dossier est un bouton cliquable
- Exemple : `Votre-nom > Documents > Travail`
- Cliquez sur n'importe quel bouton pour y accéder directement
- Très pratique pour remonter rapidement

**Mode texte (éditable) :**
- Appuyez sur **Ctrl + L** pour basculer
- Affiche le chemin complet : `/home/votre-nom/Documents/Travail`
- Vous pouvez taper ou coller un chemin directement
- Appuyez sur **Entrée** pour y aller
- **Échap** pour revenir au mode boutons

**Astuce :** En mode boutons, cliquez sur le chevron (▼) à droite d'un dossier pour voir ses sous-dossiers !

#### Boutons d'action rapide

**Rechercher** (icône de loupe) :
- Active la barre de recherche
- Raccourci : **Ctrl + F**

**Affichage** (icône de grille/liste) :
- Bascule entre vue en icônes, liste, ou compacte
- Raccourci : **Ctrl + 1** (icônes), **Ctrl + 2** (liste), **Ctrl + 3** (compacte)

**Menu d'options** (≡ ou ⋮) :
- Ouvre des options supplémentaires
- Préférences, affichage, aide, etc.

### 3. La barre latérale (sidebar)

À gauche de la fenêtre, elle vous donne un accès rapide aux emplacements importants.

#### Emplacements personnels

**Dossier personnel** (maison) :
- Votre répertoire principal : `/home/votre-nom`
- Contient tous vos fichiers personnels

**Bureau** :
- Contenu de votre bureau
- Correspond au dossier `/home/votre-nom/Bureau`

**Documents** :
- Dossier pour vos documents
- `/home/votre-nom/Documents`

**Téléchargements** :
- Fichiers téléchargés depuis Internet
- `/home/votre-nom/Téléchargements`

**Musique** :
- Votre bibliothèque musicale
- `/home/votre-nom/Musique`

**Images** :
- Vos photos et images
- `/home/votre-nom/Images`

**Vidéos** :
- Vos fichiers vidéo
- `/home/votre-nom/Vidéos`

#### Périphériques et emplacements

**Ordinateur** :
- Vue d'ensemble du système de fichiers
- Accès à toutes les partitions et disques

**Corbeille** :
- Fichiers supprimés (récupérables)
- Videz-la régulièrement pour libérer de l'espace

**Réseau** :
- Ordinateurs et partages sur votre réseau local
- Serveurs accessibles

**Disques et partitions montés** :
- Clés USB, disques externes
- Autres partitions de votre disque dur
- Apparaissent automatiquement quand branchés

#### Signets personnalisés

**Ajouter un signet :**
1. Naviguez vers le dossier que vous utilisez souvent
2. Appuyez sur **Ctrl + D**
3. Ou : Menu → Signets → Ajouter un signet

Le dossier apparaît maintenant dans la barre latérale !

**Gérer les signets :**
- Clic droit sur un signet → Renommer ou Retirer
- Glissez-déposez pour réorganiser
- Ou : Menu → Signets → Modifier les signets

**Astuce :** Ajoutez vos dossiers de travail fréquents pour y accéder en un clic !

### 4. La zone d'affichage principale

C'est ici que s'affichent le contenu du dossier actuel : fichiers et sous-dossiers.

#### Les modes d'affichage

**Vue en icônes** (par défaut) :
- Grandes icônes avec aperçu visuel
- Parfait pour les photos et vidéos
- Affiche le nom sous l'icône
- Raccourci : **Ctrl + 1**

**Vue en liste** :
- Affichage tabulaire avec détails
- Colonnes : Nom, Taille, Type, Date de modification
- Permet de trier facilement
- Meilleur pour beaucoup de fichiers
- Raccourci : **Ctrl + 2**

**Vue compacte** :
- Petites icônes, plusieurs colonnes
- Affichage dense pour voir plus d'éléments
- Bon compromis entre les deux
- Raccourci : **Ctrl + 3**

**Changer la taille des icônes :**
- **Ctrl + molette de la souris** : zoom avant/arrière
- Ou : curseur en bas à droite de la fenêtre
- Ou : Menu Affichage → Zoom

#### Tri et organisation

**Trier les fichiers :**
- En vue liste : cliquez sur l'en-tête de colonne (Nom, Taille, Type, Date)
- Clic une fois : tri croissant
- Clic deux fois : tri décroissant
- Clic droit sur en-tête : choisir les colonnes à afficher

**Organiser automatiquement :**
- Clic droit dans une zone vide → "Organiser les éléments du bureau"
- Par nom, taille, type, date de modification
- Ordre croissant ou décroissant

**Astuce :** En vue icônes, maintenez **Ctrl** en plaçant un fichier pour un positionnement libre (sans grille).

### 5. La barre d'état (en bas)

Affiche des informations sur le contenu actuel :
- Nombre d'éléments dans le dossier
- Taille totale (si des fichiers sont sélectionnés)
- Espace disque disponible
- Barre de progression lors d'opérations

### 6. Le menu contextuel (clic droit)

Le clic droit est extrêmement puissant dans Nemo !

**Clic droit sur un fichier/dossier :**
- Ouvrir / Ouvrir avec
- Couper / Copier / Coller
- Dupliquer
- Créer un lien
- Renommer
- Déplacer vers la corbeille
- Compresser (créer une archive)
- Envoyer vers (mail, autre application)
- Propriétés (détails complets)

**Clic droit dans une zone vide :**
- Nouveau document / dossier
- Organiser les éléments
- Coller (si quelque chose est copié)
- Afficher/Masquer les fichiers cachés
- Ouvrir dans un terminal
- Propriétés (du dossier actuel)

**Clic droit sur la barre latérale :**
- Ajouter un signet
- Supprimer un signet personnalisé
- Éjecter (pour périphériques)

## Navigation dans les fichiers

### Parcourir vos dossiers

**Double-clic** sur un dossier pour l'ouvrir.

**Retour au dossier parent :**
- Bouton flèche haut ↑
- **Alt + ↑**
- Clic sur le nom du dossier parent dans la barre d'adresse

**Navigation rapide par le clavier :**
- **Flèches directionnelles** : se déplacer entre les fichiers
- **Entrée** : ouvrir le fichier/dossier sélectionné
- **Retour arrière** : remonter au dossier parent
- **Début** : aller au premier élément
- **Fin** : aller au dernier élément

**Taper pour chercher (type-ahead) :**
- Commencez simplement à taper le nom d'un fichier
- Nemo met en surbrillance les fichiers correspondants
- Très pratique dans un dossier avec beaucoup de fichiers !

### Ouvrir des fichiers

**Double-clic** sur un fichier pour l'ouvrir avec l'application par défaut.

**Choisir une autre application :**
- Clic droit → "Ouvrir avec"
- Sélectionnez l'application souhaitée
- Ou "Ouvrir avec une autre application" pour plus de choix

**Définir l'application par défaut :**
1. Clic droit sur le fichier → Propriétés
2. Onglet "Ouvrir avec"
3. Sélectionnez l'application souhaitée
4. Cliquez sur "Définir par défaut"

**Glisser-déposer vers une application :**
- Glissez le fichier sur l'icône d'une application dans le panneau
- Ou sur une fenêtre d'application ouverte
- Le fichier s'ouvre dans cette application

### Sélectionner des fichiers

**Sélection simple :**
- **Clic** sur un fichier pour le sélectionner

**Sélection multiple :**
- **Ctrl + Clic** : ajouter/retirer des fichiers individuellement
- **Maj + Clic** : sélectionner une plage (du premier au dernier cliqué)
- **Ctrl + A** : sélectionner tout
- **Ctrl + Maj + A** : inverser la sélection
- **Ctrl + clic-glissé** : sélectionner avec un rectangle (lasso)

**Astuce :** Vous pouvez dessiner un rectangle de sélection en cliquant-glissant dans une zone vide !

## Opérations sur les fichiers

### Copier et coller

**Copier :**
- Sélectionnez les fichiers
- **Ctrl + C** ou clic droit → Copier
- Allez à la destination
- **Ctrl + V** ou clic droit → Coller

**Couper (déplacer) :**
- Sélectionnez les fichiers
- **Ctrl + X** ou clic droit → Couper
- Allez à la destination
- **Ctrl + V** ou clic droit → Coller
- Les fichiers sont déplacés (pas dupliqués)

**Glisser-déposer :**
- **Glisser normalement** entre deux partitions : copie
- **Glisser normalement** sur la même partition : déplace
- **Ctrl + Glisser** : toujours copier
- **Maj + Glisser** : toujours déplacer
- **Alt + Glisser** : créer un lien symbolique

**Voir une progression :**
- Une fenêtre de progression apparaît pour les opérations longues
- Affiche la vitesse, le temps restant, les fichiers en cours
- Vous pouvez mettre en pause ou annuler

### Renommer

**Renommer un fichier/dossier :**
- **Méthode 1** : Sélectionnez et appuyez sur **F2**
- **Méthode 2** : Clic droit → Renommer
- **Méthode 3** : Clic lent deux fois (pas double-clic)

**Renommer plusieurs fichiers (batch rename) :**
1. Sélectionnez plusieurs fichiers
2. Clic droit → Renommer (ou **Ctrl + F2**)
3. Une fenêtre de renommage groupé s'ouvre
4. Options disponibles :
   - Modèle de nom avec numérotation
   - Rechercher et remplacer
   - Ajouter/retirer du texte
   - Changer la casse (majuscules/minuscules)
5. Aperçu avant validation

**Conseils de nommage :**
- Évitez les espaces (utilisez `-` ou `_` à la place)
- Évitez les caractères spéciaux (/, \, *, ?, ", <, >, |)
- Linux est sensible à la casse : `fichier.txt` ≠ `Fichier.txt`

### Supprimer

**Supprimer (vers la corbeille) :**
- Sélectionnez les fichiers
- Appuyez sur **Suppr**
- Ou clic droit → Déplacer vers la corbeille

**Suppression définitive :**
- **Maj + Suppr** : suppression permanente (contourne la corbeille)
- **Attention** : aucune possibilité de récupération !

**Vider la corbeille :**
- Clic droit sur Corbeille (barre latérale) → Vider la corbeille
- Ou ouvrez la corbeille et clic droit → Vider

**Restaurer depuis la corbeille :**
1. Ouvrez la corbeille
2. Sélectionnez les fichiers à restaurer
3. Clic droit → Restaurer
4. Les fichiers retournent à leur emplacement d'origine

### Créer des dossiers et fichiers

**Nouveau dossier :**
- **Ctrl + Maj + N**
- Ou clic droit dans une zone vide → Nouveau dossier
- Donnez-lui un nom et validez

**Nouveau fichier :**
- Clic droit → Nouveau document → Fichier vide
- Ou sélectionnez un type (Texte, Document, etc.)
- Les modèles disponibles dépendent de ce qui est installé

**Créer des modèles personnalisés :**
1. Allez dans votre dossier `/home/votre-nom/Modèles`
2. Placez-y des fichiers à utiliser comme modèles
3. Ils apparaîtront dans le menu "Nouveau document"

### Compresser et extraire

**Créer une archive :**
1. Sélectionnez fichiers/dossiers à compresser
2. Clic droit → Compresser
3. Choisissez le format :
   - **.zip** : compatible Windows, Mac, Linux
   - **.tar.gz** : standard Linux, bonne compression
   - **.7z** : excellente compression
   - **.rar** : nécessite l'installation de rar
4. Nommez l'archive et validez

**Extraire une archive :**
- **Double-clic** sur l'archive : aperçu du contenu
- **Clic droit → Extraire ici** : extrait dans le dossier actuel
- **Clic droit → Extraire vers...** : choisir la destination
- **Glisser-déposer** depuis l'archive vers un dossier

**Astuce :** Pour envoyer plusieurs fichiers par mail, compressez-les d'abord en .zip !

### Propriétés des fichiers

**Accéder aux propriétés :**
- Clic droit sur un fichier/dossier → Propriétés
- Ou sélectionnez et appuyez sur **Alt + Entrée**

**Informations disponibles :**

**Onglet "Basique" :**
- Icône (modifiable par clic)
- Nom (modifiable)
- Type de fichier
- Taille (et taille sur disque)
- Emplacement (chemin complet)
- Volume (partition)
- Dates : créé, modifié, accédé

**Onglet "Permissions" :**
- Propriétaire et groupe
- Permissions de lecture/écriture/exécution
- Pour le propriétaire, le groupe, les autres
- Case "Exécutable" pour les scripts et programmes

**Onglet "Ouvrir avec" :**
- Applications disponibles pour ce type de fichier
- Définir l'application par défaut

**Onglet "Emblèmes" (badges) :**
- Petites icônes décoratives
- Pour marquer visuellement des fichiers (Important, Favori, etc.)

## Recherche de fichiers

### Recherche rapide dans Nemo

**Activer la recherche :**
- Cliquez sur l'icône de loupe (barre d'outils)
- Ou appuyez sur **Ctrl + F**
- Ou commencez simplement à taper (si activé dans les préférences)

**Utiliser la recherche :**
1. Une barre de recherche apparaît
2. Tapez votre requête
3. Nemo cherche dans le dossier actuel et ses sous-dossiers
4. Les résultats s'affichent en temps réel

**Filtres de recherche :**
- Cliquez sur "+" pour ajouter des critères :
  - Type de fichier
  - Date de modification
  - Taille
  - Nom de fichier
- Combinez plusieurs critères pour affiner

**Enregistrer une recherche :**
- Après avoir effectué une recherche
- Menu → Fichier → Enregistrer la recherche
- Créé un fichier .search que vous pouvez rouvrir

### Recherche système avec Catfish

Pour des recherches plus avancées, Linux Mint inclut **Catfish** :

**Lancer Catfish :**
- Menu → Accessoires → Catfish
- Ou via le terminal : `catfish`

**Avantages :**
- Recherche dans tout le système
- Recherche par contenu (dans les fichiers texte)
- Expressions régulières
- Filtres avancés plus complets

## Affichage et préférences

### Options d'affichage

**Afficher/masquer les fichiers cachés :**
- **Ctrl + H** pour basculer
- Ou Menu → Affichage → Afficher les fichiers cachés
- Les fichiers cachés commencent par un point (ex: `.bashrc`)

**Afficher/masquer la barre latérale :**
- **F9** pour basculer
- Pratique pour gagner de l'espace à l'écran

**Afficher/masquer les aperçus :**
- Menu → Affichage → Aperçus
- Choix : toujours, pour les fichiers locaux uniquement, jamais
- Les aperçus affichent le contenu des images/vidéos en miniature

### Personnaliser Nemo

**Accéder aux préférences :**
- Menu Édition → Préférences
- Ou icône de menu (≡) → Préférences

**Onglet "Affichage" :**
- Vue par défaut (icônes, liste, compacte)
- Taille par défaut des icônes
- Ordre de tri par défaut
- Afficher les fichiers cachés et de sauvegarde
- Format de date

**Onglet "Comportement" :**
- **Double-clic ou simple-clic** pour ouvrir
- Comportement des fichiers exécutables (demander, exécuter, ouvrir)
- Déplacer ou copier lors du glisser-déposer
- Confirmer avant suppression
- Vider la corbeille avant extinction

**Onglet "Aperçu" :**
- Afficher les aperçus des images
- Aperçus de vidéos
- Afficher le contenu des fichiers texte
- Limite de taille pour les aperçus

**Onglet "Liste des colonnes" :**
- Colonnes à afficher en vue liste
- Ordre des colonnes
- Personnalisez selon vos besoins

**Onglet "Emplacement" :**
- Ouvrir les emplacements dans des onglets ou fenêtres
- Toujours ouvrir dans la fenêtre de navigation
- Gérer le bureau (Nemo peut gérer les icônes du bureau)

**Onglet "Extensions" :**
- Plugins pour étendre Nemo
- Actions personnalisées dans le menu contextuel
- Nous y reviendrons plus tard

**Onglet "Plugins" :**
- Activer/désactiver des fonctionnalités
- Terminal intégré
- Comparaison de fichiers
- Partage

## Fonctionnalités avancées

### Les onglets

Comme un navigateur web, Nemo supporte les onglets !

**Ouvrir un nouvel onglet :**
- **Ctrl + T** : nouvel onglet dans le dossier actuel
- **Clic du milieu** sur un dossier : ouvre dans un nouvel onglet
- **Ctrl + Clic** sur un dossier : ouvre dans un nouvel onglet

**Naviguer entre onglets :**
- **Ctrl + Tab** : onglet suivant
- **Ctrl + Maj + Tab** : onglet précédent
- **Alt + 1**, **Alt + 2**, etc. : aller à l'onglet n°1, 2, etc.

**Fermer un onglet :**
- **Ctrl + W** : ferme l'onglet actif
- **Clic du milieu** sur l'onglet
- Clic sur le × de l'onglet

**Réorganiser les onglets :**
- Glissez-déposez les onglets pour les réorganiser
- Glissez un onglet hors de la fenêtre pour créer une nouvelle fenêtre

**Astuce :** Les onglets sont parfaits pour comparer des dossiers ou déplacer des fichiers entre emplacements !

### Le panneau fractionné (split view)

Affichez deux dossiers côte à côte.

**Activer le panneau fractionné :**
- **F3** pour basculer
- Ou Menu → Affichage → Panneau supplémentaire

**Utilisation :**
- Chaque panneau est indépendant
- Naviguez différemment dans chaque côté
- Glissez-déposez entre les panneaux
- Parfait pour organiser et déplacer des fichiers

**Astuce :** Combine onglets + panneaux fractionnés pour une productivité maximale !

### Ouvrir dans un terminal

**Depuis Nemo :**
- Clic droit dans une zone vide → "Ouvrir dans un terminal"
- Ouvre un terminal déjà positionné dans ce dossier
- **F4** (si configuré)

**Très pratique pour :**
- Exécuter des commandes sur les fichiers du dossier
- Éviter de naviguer en ligne de commande
- Accès rapide au terminal contextualisé

### Actions personnalisées (scripts Nemo)

Vous pouvez ajouter vos propres actions au menu contextuel !

**Emplacement des scripts :**
- `/home/votre-nom/.local/share/nemo/scripts`
- Créez ce dossier s'il n'existe pas

**Créer une action simple :**
1. Créez un fichier texte dans le dossier scripts
2. Écrivez votre script bash
3. Rendez-le exécutable : `chmod +x nom-du-script`
4. Il apparaît dans : Clic droit → Scripts → nom-du-script

**Exemples d'actions utiles :**
- Redimensionner des images
- Convertir des fichiers audio/vidéo
- Envoyer par email
- Téléverser vers un service cloud
- Créer des PDF

**Note :** De nombreux scripts sont disponibles en ligne, cherchez "nemo scripts" !

### Montage de partages réseau

**Accéder à un partage réseau :**
1. **Ctrl + L** pour activer la barre d'adresse en mode texte
2. Tapez l'adresse du partage :
   - Samba/Windows : `smb://adresse-serveur/partage`
   - FTP : `ftp://adresse-serveur`
   - SSH : `sftp://adresse-serveur`
3. Entrez vos identifiants si nécessaire
4. Le partage s'affiche dans Nemo

**Ajouter aux signets :**
- Une fois connecté, ajoutez-le aux signets (**Ctrl + D**)
- Accès rapide pour les prochaines fois !

**Déconnecter :**
- Clic droit sur le partage (barre latérale) → Démonter/Éjecter

## Raccourcis clavier essentiels

### Navigation
- **Alt + ↑** : Dossier parent
- **Alt + ←** : Précédent
- **Alt + →** : Suivant
- **Ctrl + L** : Barre d'adresse en mode texte
- **Alt + Début** : Aller au dossier personnel
- **/** (barre oblique) : Aller à la racine du système

### Affichage
- **Ctrl + 1** : Vue en icônes
- **Ctrl + 2** : Vue en liste
- **Ctrl + 3** : Vue compacte
- **Ctrl + H** : Afficher/masquer fichiers cachés
- **F9** : Afficher/masquer barre latérale
- **F3** : Panneau fractionné
- **Ctrl + +** / **Ctrl + -** : Zoom

### Sélection
- **Ctrl + A** : Tout sélectionner
- **Ctrl + I** : Inverser la sélection
- **Flèches** : Se déplacer
- **Ctrl + Clic** : Sélection multiple
- **Maj + Clic** : Sélection en plage

### Opérations
- **Ctrl + C** : Copier
- **Ctrl + X** : Couper
- **Ctrl + V** : Coller
- **F2** : Renommer
- **Suppr** : Déplacer vers corbeille
- **Maj + Suppr** : Supprimer définitivement
- **Ctrl + D** : Ajouter un signet
- **Ctrl + Maj + N** : Nouveau dossier

### Onglets et fenêtres
- **Ctrl + T** : Nouvel onglet
- **Ctrl + W** : Fermer l'onglet
- **Ctrl + Q** : Fermer la fenêtre
- **Ctrl + N** : Nouvelle fenêtre
- **Ctrl + Tab** : Onglet suivant
- **Alt + 1, 2, 3...** : Aller à l'onglet 1, 2, 3...

### Recherche et autres
- **Ctrl + F** : Rechercher
- **Alt + Entrée** : Propriétés
- **F4** : Ouvrir dans un terminal (si configuré)
- **Ctrl + Maj + G** : Aller à l'emplacement (chemin)

## Comparaison avec d'autres gestionnaires

### Caja (MATE) vs Nemo

**Similitudes :**
- Interface très proche
- Mêmes concepts de base
- Fonctionnalités similaires

**Différences :**
- Caja : un peu plus léger
- Nemo : quelques fonctionnalités supplémentaires
- Nemo : développé activement pour Cinnamon

### Thunar (Xfce) vs Nemo

**Thunar :**
- Plus léger et plus rapide
- Interface plus simple
- Moins de fonctionnalités intégrées
- Personnalisable via plugins

**Nemo :**
- Plus complet et moderne
- Davantage d'options intégrées
- Consomme un peu plus de ressources

## Astuces et bonnes pratiques

### 1. Organisation des fichiers

**Structure recommandée :**
```
/home/votre-nom/
├── Documents/
│   ├── Travail/
│   ├── Personnel/
│   └── Finances/
├── Images/
│   ├── 2024/
│   ├── Famille/
│   └── Screenshots/
├── Téléchargements/
├── Musique/
└── Vidéos/
```

**Conseils :**
- Créez des sous-dossiers par année, projet, ou catégorie
- Utilisez des noms descriptifs
- Videz régulièrement Téléchargements et Corbeille

### 2. Utilisez les signets

Ajoutez en signets :
- Vos dossiers de projets actifs
- Dossiers consultés quotidiennement
- Disques externes fréquents
- Partages réseau réguliers

### 3. Maîtrisez les raccourcis

Apprenez au moins :
- **Ctrl + C/X/V** : copier/couper/coller
- **F2** : renommer
- **Ctrl + H** : fichiers cachés
- **Ctrl + L** : barre d'adresse
- **Alt + ↑** : dossier parent

### 4. Personnalisez vos vues

- Vue liste pour dossiers avec beaucoup de fichiers
- Vue icônes pour photos et images
- Ajustez la taille des icônes selon vos besoins

### 5. Utilisez les onglets

Ne multipliez pas les fenêtres, utilisez les onglets !
- Plus organisé
- Moins de consommation mémoire
- Facilite les opérations entre dossiers

### 6. Nommage cohérent

Pour faciliter le tri :
- Dates au format AAAA-MM-JJ (ex: 2024-11-28_rapport.pdf)
- Numéros avec zéros de tête (01, 02... au lieu de 1, 2...)
- Évitez espaces et caractères spéciaux

### 7. Sauvegardez régulièrement

- Configurez Timeshift pour le système
- Sauvegardez vos données personnelles régulièrement
- Utilisez le dossier Documents, pas le Bureau

## Dépannage

### Nemo est lent ou se fige

**Solutions :**
1. Désactivez les aperçus pour les gros fichiers :
   - Préférences → Aperçu → Limiter la taille
2. Désactivez l'indexation dans les dossiers réseau
3. Redémarrez Nemo :
   - Terminal : `nemo -q` puis relancez Nemo

### Impossible d'accéder à un dossier

**Vérifiez les permissions :**
- Clic droit → Propriétés → Permissions
- Assurez-vous d'avoir les droits de lecture

**Pour accéder en tant que root (DANGER) :**
- Terminal : `sudo nemo`
- **Attention** : n'utilisez que si nécessaire !

### Les miniatures ne s'affichent pas

**Solutions :**
1. Préférences → Aperçu → Vérifier les paramètres
2. Supprimez le cache des miniatures :
   ```
   rm -rf ~/.cache/thumbnails
   ```
3. Redémarrez Nemo

### Nemo ne répond plus

**Solutions :**
1. **Ctrl + Alt + Échap** puis cliquez sur la fenêtre Nemo
2. Ou terminal : `killall nemo` puis relancez
3. Redémarrez la session si le problème persiste

### Les fichiers Windows ne s'affichent pas correctement

**Si partition NTFS :**
- Installez `ntfs-3g` si pas déjà fait
- Vérifiez que la partition est montée correctement

**Noms de fichiers bizarres :**
- Problème d'encodage, généralement sans gravité
- Les fichiers restent utilisables

## Conclusion

Nemo est un gestionnaire de fichiers complet et intuitif qui facilite l'organisation et la manipulation de vos données sous Linux Mint. Sa philosophie "utilisateur d'abord" en fait un outil accessible aux débutants tout en offrant des fonctionnalités avancées pour les utilisateurs expérimentés.

**Points clés à retenir :**

**Interface :**
- Barre latérale pour navigation rapide
- Barre d'outils pour actions courantes
- Modes d'affichage adaptables

**Navigation :**
- Les signets accélèrent l'accès
- Les onglets organisent le travail
- Le panneau fractionné facilite les transferts

**Opérations :**
- Copier/Couper/Coller comme sous Windows
- Glisser-déposer avec modificateurs (Ctrl, Maj)
- Clic droit pour le menu contextuel

**Personnalisation :**
- Préférences complètes
- Actions personnalisées possibles
- Totalement adaptable à votre flux de travail

Prenez le temps d'explorer Nemo, ajustez-le à vos besoins, et il deviendra vite un outil indispensable de votre quotidien sous Linux Mint !

---

**Prochaine étape :** Les espaces de travail virtuels

⏭️ [Les espaces de travail virtuels](/04-decouverte-de-lenvironnement-de-bureau/04-les-espaces-de-travail-virtuels.md)
