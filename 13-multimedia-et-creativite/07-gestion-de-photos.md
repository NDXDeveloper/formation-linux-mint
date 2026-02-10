🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 13.7 Gestion de photos (Shotwell, digiKam)

## Introduction

Avec nos smartphones et appareils photo numériques, nous accumulons des milliers de photos. Sans organisation, retrouver une photo précise devient un cauchemar. Linux Mint offre d'excellents outils pour importer, organiser, retoucher et partager vos photos de manière efficace.

Dans ce chapitre, nous allons découvrir :

- **Shotwell** : gestionnaire de photos simple et intégré, parfait pour débuter
- **digiKam** : gestionnaire professionnel pour photographes exigeants
- **Organisation** : albums, tags, événements, reconnaissance faciale
- **Retouches** : corrections basiques intégrées
- **Métadonnées** : EXIF, GPS, mots-clés
- **Sauvegarde** : protéger vos souvenirs précieux

> **Bon à savoir** : Ces gestionnaires sont des alternatives libres et gratuites à iPhoto, Google Photos ou Adobe Lightroom, avec parfois même plus de fonctionnalités.

---

## Pourquoi utiliser un gestionnaire de photos ?

### Sans gestionnaire (dossiers simples)

**Avantages :**
- ✅ Simple et direct
- ✅ Contrôle total sur l'arborescence
- ✅ Pas de base de données

**Inconvénients :**
- ❌ Difficile de retrouver une photo parmi des milliers
- ❌ Pas de recherche par date, lieu, personne
- ❌ Import manuel fastidieux
- ❌ Pas de reconnaissance de doublons
- ❌ Retouches destructrices (modifient fichier original)

### Avec un gestionnaire de photos

**Avantages :**
- ✅ Import automatique depuis appareils
- ✅ Organisation chronologique automatique
- ✅ Albums virtuels (une photo dans plusieurs albums)
- ✅ Tags et mots-clés pour recherche rapide
- ✅ Reconnaissance faciale
- ✅ Géolocalisation sur carte
- ✅ Retouches non destructrices (fichier original intact)
- ✅ Détection de doublons
- ✅ Diaporamas et partage facilités

**Inconvénients :**
- ❌ Courbe d'apprentissage initiale
- ❌ Base de données à sauvegarder (en plus des photos)
- ❌ Peut être plus lent sur très grandes collections

> **Verdict** : Pour plus de 500 photos, un gestionnaire devient indispensable.

---

## Shotwell - Le gestionnaire accessible

### Qu'est-ce que Shotwell ?

Shotwell est le gestionnaire de photos par défaut de nombreuses distributions Linux avec GNOME. Il offre un excellent équilibre entre simplicité et fonctionnalités, comparable à iPhoto d'Apple.

**Points forts :**
- Interface claire et intuitive
- Courbe d'apprentissage douce
- Import automatique d'appareils photo
- Organisation par événements
- Retouches basiques intégrées
- Reconnaissance faciale simple
- Export vers services web (Flickr, etc.)
- Diaporamas
- Léger et rapide

**Utilisations principales :**
- Gestion de collection familiale (5 000 - 50 000 photos)
- Import et tri de photos vacances
- Retouches basiques (recadrage, yeux rouges, ajustements)
- Création de diaporamas
- Partage sur réseaux sociaux

### Installation de Shotwell

Shotwell est généralement préinstallé. Si ce n'est pas le cas :

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "Shotwell"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update  
sudo apt install shotwell  
```

### Premier lancement de Shotwell

**Lancer Shotwell :**
- Menu → Graphisme → **Shotwell**
- Ou commande : `shotwell`

**Au premier lancement :**
- Shotwell scanne automatiquement `~/Images/` (~/Pictures/)
- Crée sa base de données dans `~/.local/share/shotwell/`
- Affiche les photos trouvées

### Interface de Shotwell

L'interface est organisée en zones claires :

**Barre latérale gauche :**
- **Bibliothèque** : toutes vos photos
- **Dernière importation** : photos récemment importées
- **Signalées** : photos marquées comme favorites
- **Événements** : groupes par date/événement
- **Albums** : vos albums personnalisés
- **Tags** : organisation par mots-clés
- **Personnes** : reconnaissance faciale

**Zone centrale :**
- Miniatures de vos photos
- Vue en grille ajustable

**Barre du haut :**
- Recherche
- Tri et filtres
- Outils d'édition

**Barre du bas (quand photo sélectionnée) :**
- Informations : date, taille, appareil
- Métadonnées EXIF
- Tags et titre

---

## Importer des photos dans Shotwell

### Importer depuis un appareil photo ou smartphone

1. **Connectez votre appareil** via USB
2. Shotwell détecte automatiquement l'appareil
3. Fenêtre d'import s'ouvre :
   - **Aperçu** des photos sur l'appareil
   - **Sélection** : toutes ou seulement certaines

**Options d'import :**
- **Copier** : copie les photos (recommandé)
- **Déplacer** : supprime de l'appareil après import
- **Créer un événement** : nomme l'import (ex: "Vacances Bretagne 2024")
- **Appliquer des tags** : ajoutez des mots-clés immédiatement

4. Cliquez sur **Importer**
5. Shotwell copie les photos dans `~/Images/` et les ajoute à la bibliothèque

**Destination :**
Par défaut : `~/Images/AAAA/MM/JJ/`

Exemple : `~/Images/2024/11/29/`

### Importer depuis un dossier existant

**Méthode 1 : Ajouter à la bibliothèque**
- `Fichier` → `Importer à partir d'un dossier`
- Sélectionnez le dossier
- Shotwell copie ou référence les photos

**Méthode 2 : Surveiller un dossier**
- `Édition` → `Préférences` → `Bibliothèque`
- **Surveiller le dossier de la bibliothèque** : coché
- Toute photo ajoutée à `~/Images/` apparaît automatiquement

### Importer depuis une carte SD

1. Insérez la carte SD
2. Shotwell la détecte comme appareil
3. Suivez le processus d'import normal

---

## Organiser vos photos avec Shotwell

### Événements

Les **événements** regroupent automatiquement les photos par date. C'est le premier niveau d'organisation.

**Afficher les événements :**
- Barre latérale → **Événements**
- Shotwell groupe par jour, mois ou année

**Fusionner des événements :**
1. Vue Événements
2. Sélectionnez plusieurs événements (Ctrl + clic)
3. Clic droit → **Fusionner**
4. Nommez l'événement fusionné (ex: "Mariage Sophie")

**Renommer un événement :**
- Clic droit sur événement → **Renommer l'événement**
- Donnez un nom significatif

**Séparation automatique :**
- `Édition` → `Préférences` → `Événements`
- Choisissez intervalle : 1 jour, 1 semaine, 1 mois

### Albums

Les **albums** sont des collections virtuelles que vous créez manuellement.

**Créer un album :**
1. Sélectionnez des photos (Ctrl + clic pour multiples)
2. Clic droit → **Nouvel album**
3. Nommez l'album (ex: "Meilleures photos 2024")

**Ou :**
- Barre latérale → Albums → **+** (Nouveau)

**Ajouter des photos à un album existant :**
- Glissez-déposez photos sur l'album dans la barre latérale
- Ou sélectionnez photos → clic droit → **Ajouter à l'album**

**Supprimer de l'album :**
- Dans l'album, sélectionnez photo
- Clic droit → **Supprimer de l'album**
- (Photo reste dans bibliothèque, juste retirée de l'album)

> **Important** : Les albums sont virtuels. Une photo peut être dans plusieurs albums sans être dupliquée.

### Tags (mots-clés)

Les **tags** permettent d'attribuer des mots-clés aux photos pour recherche et filtrage.

**Créer et attribuer un tag :**
1. Sélectionnez photo(s)
2. `Tags` → **Ajouter des tags**
3. Tapez le tag (ex: "famille", "voyage", "paysage")
4. Appuyez sur Entrée

**Tags hiérarchiques :**
Utilisez `/` pour hiérarchie : `voyage/france/bretagne`

**Rechercher par tag :**
- Barre latérale → **Tags**
- Cliquez sur un tag pour filtrer

**Combiner tags :**
- Maintenez Ctrl et cliquez sur plusieurs tags
- Shotwell affiche photos ayant tous ces tags

### Personnes (reconnaissance faciale)

Shotwell peut reconnaître et regrouper les visages.

**Activer la détection de visages :**
1. `Édition` → `Préférences` → `Personnes`
2. Cochez **Détecter les visages**
3. Shotwell scanne la bibliothèque (peut prendre du temps)

**Nommer les personnes :**
1. Barre latérale → **Personnes**
2. Shotwell affiche groupes de visages similaires
3. Cliquez sur un groupe
4. Saisissez le nom de la personne
5. Shotwell apprend et améliore la reconnaissance

**Rechercher par personne :**
- Barre latérale → Personnes → clic sur personne
- Affiche toutes photos de cette personne

### Signaler (favoris)

**Marquer comme favorite :**
- Sélectionnez photo
- Appuyez sur `/` (slash)
- Ou clic droit → **Signaler**

**Afficher les favorites :**
- Barre latérale → **Signalées**

**Utile pour :**
- Marquer meilleures photos d'un événement
- Sélection pour album photo papier
- Photos à partager en priorité

### Notation

Shotwell permet de noter vos photos (1 à 5 étoiles).

**Attribuer une note :**
- Sélectionnez photo
- Appuyez sur `1`, `2`, `3`, `4` ou `5`
- Ou clic droit → **Définir la note**

**Filtrer par note :**
- Menu `Affichage` → **Filtrer les photos**
- Choisissez note minimale

### Recherche

**Barre de recherche (en haut) :**
- Recherche dans titres, tags, noms de fichiers
- Temps réel pendant la frappe

**Recherche avancée :**
- Combinez événements, tags, personnes, notes
- Date range (affichage par timeline)

---

## Visualiser et organiser

### Modes d'affichage

**Vue miniatures :**
- `Affichage` → **Agrandir les miniatures** (`+`) / **Réduire** (`-`)
- Ou molette de souris

**Vue plein écran :**
- Double-clic sur photo
- Ou appuyez sur `F`
- Navigation : flèches ← →
- Sortie : `F` ou `Échap`

**Diaporama :**
- Sélectionnez photos (ou album/événement)
- `Affichage` → **Diaporama** (ou `F5`)
- Paramètres : durée, transitions, musique

### Tri

**Trier par :**
- `Affichage` → **Trier les photos**
- Options :
  - Titre
  - Date d'exposition (prise de vue)
  - Note
  - Nom de fichier

**Ordre croissant/décroissant**

### Comparer des photos

**Vue côte-à-côte :**
1. Sélectionnez 2 photos (Ctrl + clic)
2. Appuyez sur `C`
3. Comparez pour choisir la meilleure

---

## Retouches basiques dans Shotwell

Shotwell intègre des outils de retouche simples mais efficaces.

**Accéder au mode édition :**
- Double-clic sur photo
- Ou sélectionnez et appuyez sur `Enter`
- Barre d'outils apparaît en haut

### Outils disponibles

#### 1. Rotation

**Faire pivoter :**
- Boutons rotation 90° gauche/droite
- Raccourcis : `[` (gauche) et `]` (droite)

**Redresser (ajustement fin) :**
- Outil **Redresser**
- Curseur pour ajuster angle (lignes de grille aident)

#### 2. Recadrage

1. Cliquez sur **Recadrer**
2. Sélectionnez ratio :
   - **Libre** : dimensions personnalisées
   - **Original** : conserve proportions
   - **Formats standards** : 4:3, 16:9, carré, etc.
3. Ajustez le cadre (glissez coins/bords)
4. Cliquez **Appliquer** (ou `Enter`)

#### 3. Correction automatique

**Amélioration automatique :**
- Bouton **Améliorer** (baguette magique)
- Shotwell ajuste luminosité, contraste, couleurs automatiquement
- Résultat souvent bon pour photos underexposées

#### 4. Yeux rouges

1. Cliquez sur **Yeux rouges**
2. Cliquez sur chaque œil rouge
3. Shotwell corrige automatiquement

#### 5. Ajustements manuels

**Exposition :**
- Curseur pour éclaircir/assombrir
- Équivalent à luminosité

**Saturation :**
- Rend couleurs plus ou moins intenses
- Vers gauche : noir et blanc
- Vers droite : couleurs vives

**Teinte :**
- Ajuste balance des couleurs
- Correction dominante colorée

**Température :**
- Plus froid (bleuté) ou plus chaud (orangé)
- Correction balance des blancs

**Ombres :**
- Éclaircit uniquement les zones sombres
- Utile pour photos à contre-jour

#### 6. Effets

Shotwell propose quelques effets prédéfinis :
- Noir et blanc
- Sépia
- Négatif
- Autres variations

### Appliquer ou annuler

**Pendant l'édition :**
- **Appliquer** : valide les modifications
- **Annuler** : retour au précédent état
- **Rétablir les originaux** : annule TOUTES les modifications

**Sortir du mode édition :**
- Bouton **Terminé**
- Ou `Échap`

### Modifications non destructrices

**Important :** Shotwell ne modifie jamais l'original.

**Comment ça fonctionne :**
- Fichier original conservé intact
- Modifications stockées dans base de données
- Affichage = original + modifications appliquées

**Revenir à l'original :**
- En mode édition → **Rétablir les originaux**
- Toutes modifications annulées instantanément

**Exporter version modifiée :**
- `Fichier` → `Exporter`
- Crée nouveau fichier avec modifications intégrées

---

## Métadonnées et informations

### Afficher les métadonnées EXIF

**Métadonnées EXIF** : informations enregistrées par l'appareil photo.

**Afficher :**
- Sélectionnez photo
- Barre du bas affiche infos basiques
- `Affichage` → **Métadonnées étendues** pour détails complets

**Informations disponibles :**
- **Date et heure** de prise de vue
- **Appareil** : marque, modèle
- **Paramètres** : ISO, vitesse d'obturation, ouverture, focale
- **GPS** : coordonnées si appareil compatible
- **Dimensions** : pixels, taille fichier

### Modifier titre et commentaire

**Titre :**
- Sélectionnez photo
- Barre du bas → cliquez dans **Titre**
- Saisissez titre descriptif

**Commentaire :**
- Icône commentaire (bulle) ou `Ctrl + M`
- Ajoutez description, contexte, notes

### GPS et géolocalisation

Si vos photos ont données GPS :
- Shotwell affiche coordonnées
- Lien vers carte (ouvre navigateur avec localisation)

**Utilité :**
- Retrouver lieu exact d'une photo
- Organiser par lieux visités

---

## Partager et exporter

### Exporter des photos

**Export simple :**
1. Sélectionnez photo(s)
2. `Fichier` → **Exporter**
3. Choisissez :
   - **Dossier de destination**
   - **Format** : JPEG (qualité ajustable), PNG, TIFF, BMP
   - **Taille** : originale ou redimensionnée
   - **Métadonnées** : conserver ou supprimer
4. Cliquez **OK**

**Cas d'usage :**
- Partage par email (taille réduite)
- Upload web
- Sauvegarde version retouchée

### Publier sur services web

Shotwell peut publier directement sur certains services.

**Services supportés :**
- Flickr
- Facebook
- YouTube (pour vidéos)
- Piwigo

**Configuration :**
1. `Fichier` → **Publier**
2. Sélectionnez service
3. Autorisez Shotwell (compte web)
4. Sélectionnez photos
5. Configurez album, visibilité
6. Publiez

> **Note** : Support limité aux anciens services. Pour Instagram, Google Photos, etc., utilisez navigateur ou applications dédiées.

### Diaporama

**Créer un diaporama :**
1. Sélectionnez photos (album, événement ou sélection manuelle)
2. `Affichage` → **Diaporama** (ou `F5`)

**Paramètres :**
- `Édition` → `Préférences` → `Diaporama`
- **Durée** : secondes par photo
- **Transition** : fondu, aucune
- **Répéter** : boucle
- **Afficher titre** : superpose titre photo

**Pendant diaporama :**
- `Espace` : pause/lecture
- `Échap` : sortir
- Flèches : précédent/suivant

---

## digiKam - Le gestionnaire professionnel

### Qu'est-ce que digiKam ?

digiKam est un gestionnaire de photos professionnel, comparable à Adobe Lightroom. Il offre des fonctionnalités avancées pour photographes sérieux et grandes collections.

**Points forts :**
- Gestion de collections énormes (100 000+ photos)
- Base de données MySQL ou SQLite
- Reconnaissance faciale avancée (AI)
- Géolocalisation avec carte interactive
- Métadonnées EXIF/IPTC/XMP complètes
- Tags hiérarchiques illimités
- Recherche floue (similarité visuelle)
- Workflow professionnel
- Gestion de fichiers RAW
- Retouches avancées
- Visionneuse RAW (développement basique)
- Batch processing (traitement par lot)

**Utilisations principales :**
- Collections photographiques professionnelles
- Gestion de dizaines de milliers de photos
- Workflow RAW
- Catalogage méticuleux
- Archivage à long terme

### Installation de digiKam

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "digiKam"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update  
sudo apt install digikam  
```

> **Note :** digiKam installe des dépendances KDE (environ 200-300 Mo). C'est normal.

### Configuration initiale

#### Premier lancement

Au premier lancement, assistant de configuration :

**1. Emplacement de la collection :**
- Choisissez où sont vos photos
- Généralement `~/Images/`
- Plusieurs emplacements possibles (disques externes, NAS)

**2. Type de base de données :**

**SQLite (recommandé pour débuter) :**
- ✅ Simple, automatique
- ✅ Pas de configuration
- ✅ Parfait jusqu'à 50 000-100 000 photos
- ❌ Légèrement plus lent sur très grandes collections

**MySQL/MariaDB (pour pros) :**
- ✅ Très rapide sur grandes collections
- ✅ Serveur distant possible (partage réseau)
- ❌ Configuration plus complexe
- ❌ Nécessite installation serveur MySQL

**3. Métadonnées :**
- **Écrire dans fichiers** : métadonnées sauvées dans EXIF/XMP (recommandé)
- Permet portabilité (base de données recréable depuis fichiers)

**4. Scan initial :**
- digiKam scanne votre collection
- Crée miniatures
- Lit métadonnées
- Peut prendre 10 min - 2h selon taille collection

### Interface de digiKam

Interface complexe mais logique :

**Barre latérale gauche (navigation) :**
- **Albums** : structure de dossiers
- **Tags** : organisation par mots-clés
- **Labels** : couleurs, notes, flags
- **Dates** : calendrier/timeline
- **Recherches** : recherches enregistrées
- **Personnes** : reconnaissance faciale
- **Lieux** : carte géographique

**Zone centrale :**
- Miniatures des photos
- Taille ajustable (zoom)

**Barre latérale droite (propriétés) :**
- **Propriétés** : infos fichier
- **Métadonnées** : EXIF complet
- **Couleurs** : histogramme
- **Tags** : gestion tags
- **Commentaires** : annotations
- **Personnes** : visages détectés

**Barre d'outils du haut :**
- Import, export
- Édition
- Recherche
- Outils divers

### Importer des photos dans digiKam

#### Import depuis appareil

1. Connectez appareil photo/smartphone
2. digiKam détecte automatiquement
3. **Import** (icône caméra) → sélectionnez appareil
4. Fenêtre d'import avancée :
   - **Aperçu** des photos
   - **Sélection** : toutes ou filtrées
   - **Album de destination**
   - **Renommage** : pattern personnalisable
   - **Métadonnées** : tags, note, auteur
   - **Scripts post-import** : automatisations
5. **Télécharger les images sélectionnées**

**Renommage automatique :**
Utilisez patterns : `[date]_[file]` → `2024-11-29_IMG_001.jpg`

#### Import depuis dossiers

**Ajouter un dossier à la collection :**
1. `Paramètres` → `Configurer digiKam` → **Collections**
2. **Ajouter une collection**
3. Sélectionnez dossier racine
4. digiKam scanne et indexe

**Import de fichiers :**
- `Import` → `Ajouter des images`
- Copie vers collection gérée

---

## Organisation avancée dans digiKam

### Système de tags hiérarchiques

digiKam excelle dans les tags avec hiérarchie illimitée.

**Structure recommandée :**
```
Personnes/
  ├── Famille/
  │   ├── Paul
  │   ├── Marie
  │   └── Sophie
  └── Amis/
      ├── Jean
      └── Luc

Événements/
  ├── Vacances/
  │   ├── 2024/
  │   │   ├── Bretagne
  │   │   └── Italie
  │   └── 2023/
  └── Mariages/

Sujets/
  ├── Paysages/
  │   ├── Mer
  │   ├── Montagne
  │   └── Forêt
  ├── Architecture/
  └── Animaux/
```

**Créer tag hiérarchique :**
1. Barre latérale → **Tags**
2. Clic droit → **Nouveau tag**
3. Nommez et choisissez parent (ou racine)

**Attribuer tags :**
- Glissez photo sur tag
- Ou sélectionnez photo → barre droite → Tags → cochez

**Recherche par tags :**
- Cliquez sur tag → affiche photos
- Ctrl + clic : combiner plusieurs tags

### Reconnaissance faciale avancée

digiKam utilise AI pour reconnaissance faciale.

**Activer reconnaissance :**
1. `Paramètres` → `Configurer digiKam` → **Reconnaissance de visages**
2. **Activer la détection** : coché
3. **Base de données** : choisir modèle (standard suffit)

**Scan des visages :**
1. `Outils` → **Rechercher des personnes**
2. digiKam scanne toutes photos
3. Détecte et regroupe visages similaires

**Nommer les personnes :**
1. Barre latérale → **Personnes**
2. Groupes de visages **Inconnus**
3. Cliquez sur groupe
4. Saisissez nom de la personne
5. Confirmez visages corrects (cochez)
6. digiKam apprend et améliore

**Affiner reconnaissance :**
- Plus vous identifiez, plus l'IA apprend
- Correction d'erreurs améliore précision
- Peut atteindre 90%+ de précision

### Géolocalisation et carte

**Afficher la carte :**
- Barre latérale → **Lieux**
- Carte interactive (OpenStreetMap)

**Photos avec GPS :**
- Apparaissent automatiquement sur carte
- Cliquez sur marqueur → affiche photos de ce lieu

**Ajouter GPS manuellement :**
1. Sélectionnez photo(s)
2. Barre droite → **GPS**
3. Cliquez sur carte ou entrez coordonnées
4. **Appliquer**

**Recherche géographique :**
- Dessinez zone sur carte
- Affiche toutes photos dans cette zone

**Reverse geocoding :**
- digiKam peut convertir GPS en noms de lieux
- Ex: 48.8566, 2.3522 → Paris, France

### Labels et notations

**Notes (0-5 étoiles) :**
- Sélectionnez photo
- Barre droite → **Note** → cliquez étoiles
- Ou raccourcis : `Ctrl + 0` à `Ctrl + 5`

**Labels de couleur :**
- Rouge, Orange, Jaune, Vert, Bleu, etc.
- Utilisation personnelle (ex: Rouge = à imprimer, Vert = publiées)
- Clic droit sur photo → **Affecter un label**

**Flags (drapeaux) :**
- Rejected (rejeté) : photo à supprimer
- Pending (en attente) : à trier
- Accepted (accepté) : validée

**Filtrer par labels :**
- Barre latérale → **Labels**
- Cliquez pour filtrer

### Recherche avancée

digiKam offre recherche très puissante.

**Recherche simple :**
- Barre de recherche en haut
- Cherche dans noms fichiers, tags, commentaires

**Recherche avancée :**
1. `Rechercher` → **Recherche avancée** (`Ctrl + F`)
2. Fenêtre avec critères multiples :
   - **Date** : plage
   - **Tags** : tous, aucun, au moins un
   - **Note** : minimum, exact
   - **Métadonnées** : appareil, objectif, ISO, etc.
   - **Géolocalisation** : rayon autour d'un point
   - **Fichier** : nom, taille, format
   - **Couleurs** : dominante colorée

3. Combinez critères (ET/OU)
4. **Rechercher**

**Enregistrer recherche :**
- Après recherche, **Enregistrer la recherche**
- Apparaît dans barre latérale → Recherches
- Recherche dynamique (se met à jour)

**Recherche par similarité :**
- Clic droit sur photo → **Rechercher des photos similaires**
- Algorithme trouve photos visuellement proches
- Utile pour trouver doublons ou variantes

### Collections multiples

digiKam peut gérer plusieurs collections (emplacements).

**Cas d'usage :**
- Collection principale : disque interne
- Collection archives : disque externe
- Collection RAW : disque rapide
- Collection exports : dossier partagé

**Ajouter collection :**
1. `Paramètres` → **Configurer digiKam** → **Collections**
2. **Ajouter**
3. Chemin vers dossier
4. Type : Local, Réseau, Amovible

**Basculer entre collections :**
- Barre latérale → Albums → liste déroulante en haut

---

## Édition et retouches dans digiKam

### Éditeur d'images

digiKam intègre un éditeur d'images complet.

**Ouvrir en édition :**
- Double-clic sur photo
- Ou `F4`

**Interface éditeur :**
- Aperçu central
- Barre d'outils gauche : outils
- Barre d'outils droite : paramètres outil actif
- Historique : annuler/rétablir

### Outils de retouche disponibles

**Corrections basiques :**
- **Rotation** : 90°, redresser
- **Recadrage** : ratios prédéfinis ou libre
- **Redimensionner** : changer dimensions

**Ajustements couleur :**
- **Luminosité/Contraste**
- **Niveaux** : histogramme
- **Courbes** : contrôle précis
- **Teinte/Saturation**
- **Balance des couleurs**
- **Balance des blancs**
- **Correction gamma**

**Filtres :**
- **Netteté** : améliorer détails
- **Flou** : adoucir
- **Réduction du bruit** : photos ISO élevé
- **Correction distorsion** : objectif grand-angle
- **Vignettage** : assombrir bords

**Retouches locales :**
- **Yeux rouges**
- **Tampon de clonage** : dupliquer zones
- **Correcteur** : supprimer imperfections
- **Restauration** : vieilles photos

**Effets :**
- **Noir et blanc** : conversion avancée
- **Sépia**
- **Effets de texture**
- **Ajout de grain**

### Modifications non destructrices

Comme Shotwell, digiKam conserve originaux.

**Versioning :**
- Original toujours intact
- Versions modifiées sauvées séparément
- Gestion de versions multiples

**Revenir à original :**
- Clic droit → **Revenir à original**

---

## Traitement par lots (Batch Processing)

digiKam permet de traiter plusieurs photos simultanément.

### Batch Queue Manager

**Ouvrir :**
- `Outils` → **Gestionnaire de files d'attente**

**Ajouter photos :**
- Glissez photos depuis album vers file d'attente

**Appliquer traitements :**
1. Sélectionnez file
2. **Onglet Paramètres de base** : format sortie, qualité
3. **Onglet Outils** : ajoutez opérations
   - Redimensionner
   - Convertir format
   - Ajouter watermark (filigrane)
   - Ajuster couleurs
   - Renommer
   - Et bien d'autres

**Chaîne de traitements :**
- Ajoutez plusieurs outils séquentiellement
- Ex: Redimensionner → Watermark → Convertir JPEG

**Exécuter :**
- Cliquez **Exécuter**
- digiKam traite toutes photos
- Sauvegarde dans dossier choisi

**Sauvegarder preset :**
- Sauvegardez vos chaînes fréquentes
- Réutilisez en 1 clic

### Renommage par lot

**Renommer plusieurs photos :**
1. Sélectionnez photos
2. `Outils` → **Renommer**
3. Pattern : `[date]_[file]`, `Vacances_[###]`, etc.
4. Aperçu des nouveaux noms
5. **Renommer**

---

## Gestion de fichiers RAW

digiKam gère excellemment les fichiers RAW.

### Qu'est-ce qu'un fichier RAW ?

**RAW** : données brutes du capteur, non traitées.

**Avantages :**
- Qualité maximale
- Très grande latitude de retouche
- Récupération ombres/hautes lumières
- Balance des blancs ajustable après coup

**Inconvénients :**
- Fichiers volumineux (20-50 Mo)
- Nécessite "développement"
- Formats propriétaires (.CR2, .NEF, .ARW, etc.)

### Affichage et organisation RAW

digiKam :
- Affiche RAW via miniatures
- Organise comme tout autre fichier
- Tags, notes, tout fonctionne

### Développement RAW basique

digiKam intègre développeur RAW basique.

**Ouvrir RAW en édition :**
- Double-clic sur RAW
- Interface éditeur avec outils RAW

**Ajustements RAW :**
- **Exposition** : ±2-3 stops
- **Balance des blancs** : température, teinte
- **Récupération** : hautes lumières, ombres
- **Clarté** : contraste local
- **Vibrance** : saturation intelligente

**Export :**
- Développez avec réglages
- Exportez en JPEG/TIFF

**Pour développement pro :**
- Utilisez **Darktable** ou **RawTherapee** (outils dédiés)
- digiKam peut ouvrir dans ces outils : clic droit → **Ouvrir avec**

---

## Comparaison Shotwell vs digiKam

| Critère | Shotwell | digiKam |
|---------|----------|---------|
| **Interface** | Simple, épurée | Complexe, riche |
| **Courbe apprentissage** | Facile | Modérée à difficile |
| **Collection max recommandée** | 50 000 photos | Illimité (500 000+) |
| **Base de données** | SQLite intégré | SQLite ou MySQL |
| **Reconnaissance faciale** | Basique | Avancée (IA) |
| **Tags** | Simples | Hiérarchiques illimités |
| **Géolocalisation** | Affichage | Carte interactive |
| **Recherche** | Basique | Très avancée |
| **RAW** | Support lecture | Développement basique |
| **Retouches** | Basiques | Avancées |
| **Batch processing** | Non | Oui |
| **Métadonnées** | EXIF basique | EXIF/IPTC/XMP complet |
| **Vitesse** | Rapide | Plus lent (grandes collections) |
| **Ressources** | Légères | Moyennes |
| **Idéal pour** | Familles, débutants | Photographes, pros |

---

## Quel gestionnaire choisir ?

### Choisissez Shotwell si :

- ✅ Vous débutez en gestion de photos
- ✅ Collection < 50 000 photos
- ✅ Vous voulez simplicité et rapidité
- ✅ Retouches basiques suffisent
- ✅ Vous ne travaillez pas en RAW
- ✅ Organisation simple par événements/albums

### Choisissez digiKam si :

- ✅ Collection > 20 000 photos (ou prévoyez croissance)
- ✅ Vous êtes photographe amateur/pro
- ✅ Vous shootez en RAW
- ✅ Vous voulez organisation méthodique (tags hiérarchiques)
- ✅ Géolocalisation importante
- ✅ Reconnaissance faciale avancée nécessaire
- ✅ Workflow professionnel requis
- ✅ Vous n'avez pas peur de la complexité

### Workflow hybride

Certains utilisent les deux :
- **digiKam** : catalogage, organisation, tags
- **Darktable/RawTherapee** : développement RAW
- **GIMP** : retouches poussées

---

## Sauvegarde de vos photos

### Stratégie de sauvegarde 3-2-1

**Règle d'or :**
- **3** copies de vos données
- Sur **2** supports différents
- **1** copie hors site

**Exemple :**
1. Photos originales : disque dur ordinateur
2. Sauvegarde 1 : disque dur externe chez vous
3. Sauvegarde 2 : cloud (Google Photos, Nextcloud) ou disque chez famille

### Que sauvegarder ?

**Essentiel :**
- ✅ Fichiers photos (évidemment)
- ✅ Base de données gestionnaire :
  - Shotwell : `~/.local/share/shotwell/`
  - digiKam : `~/.config/digikam*` et base de données

**Optionnel :**
- Exports et versions retouchées (peuvent être regénérés)

### Outils de sauvegarde

**rsync (ligne de commande) :**
```bash
# Sauvegarder photos vers disque externe
rsync -av --progress ~/Images/ /media/disque_externe/Backup_Photos/

# Sauvegarder base Shotwell
rsync -av ~/.local/share/shotwell/ /media/disque_externe/Backup_Shotwell/
```

**Déjà Dup (graphique) :**
```bash
sudo apt install deja-dup
```
- Paramétrez sauvegardes automatiques
- Incluez ~/Images/ et bases de données

**Back In Time :**
```bash
sudo apt install backintime-qt
```
- Snapshots réguliers
- Restauration facile

### Cloud pour photos

**Google Photos :**
- 15 Go gratuit
- Qualité originale ou compressée (illimité)
- Reconnaissance faciale
- Recherche puissante

**Nextcloud (auto-hébergé) :**
- Contrôle total
- Illimité (selon espace disque)
- Synchronisation automatique
- Apps mobiles

**Autres services :**
- pCloud : 10 Go gratuit
- MEGA : 20 Go gratuit
- Amazon Photos : illimité avec Prime

---

## Astuces et bonnes pratiques

### Organisation des fichiers

**Structure recommandée sur disque :**
```
~/Images/
├── 2024/
│   ├── 2024-01_Janvier/
│   ├── 2024-02_Fevrier/
│   └── ...
├── 2023/
│   ├── 2023-01_Janvier/
│   └── ...
└── Archives_anciennes/
```

**Dans le gestionnaire (albums/tags) :**
- Organisation virtuelle, indépendante des dossiers
- Plus flexible et puissante

### Workflow d'import recommandé

1. **Import depuis appareil**
   - Nommez événement clairement
   - Ajoutez tags généraux immédiatement

2. **Tri initial (dans les 24h)**
   - Supprimez ratés (flous, mauvais cadrage)
   - Marquez meilleures (favoris ou 4-5 étoiles)

3. **Organisation détaillée**
   - Tags spécifiques
   - Identification personnes
   - Commentaires si nécessaire

4. **Retouches**
   - Meilleures photos uniquement
   - Export versions finales

5. **Partage/archivage**
   - Partagez sélection
   - Sauvegarde complète

### Nettoyage régulier

**Tous les 3-6 mois :**
- Recherchez doublons
- Supprimez photos ratées gardées "au cas où"
- Vérifiez tags et organisation
- Contrôlez espace disque

**digiKam - Chercher doublons :**
- `Outils` → **Chercher des éléments en double**
- Recherche par similarité
- Décidez lesquels garder

### Performance

**Si gestionnaire lent :**

**Shotwell :**
- Limitez taille collection
- Réglez génération miniatures : `Édition` → `Préférences` → `Modifications`

**digiKam :**
- Utilisez MySQL au lieu de SQLite (grandes collections)
- Stockez miniatures sur SSD
- Ajustez qualité miniatures : `Paramètres` → `Configurer digiKam` → **Album**
- Désactivez scan automatique si pas nécessaire

---

## Conclusion

La gestion de photos sous Linux Mint est mature et puissante, avec des outils adaptés à tous les niveaux.

**Shotwell** est parfait pour les utilisateurs quotidiens qui veulent une solution simple, rapide et efficace pour organiser leurs souvenirs de famille. Son interface claire et ses fonctionnalités bien pensées en font un excellent choix pour débuter.

**digiKam** s'adresse aux photographes plus exigeants et à ceux qui gèrent de très grandes collections. Sa richesse fonctionnelle et ses capacités d'organisation en font un outil professionnel comparable aux meilleures solutions commerciales.

**Points clés à retenir :**
- Importez régulièrement pour éviter l'accumulation
- Organisez au fur et à mesure (événements, tags)
- Sauvegardez selon règle 3-2-1
- Choisissez l'outil adapté à votre usage
- Les retouches sont non destructrices (originaux protégés)
- Reconnaissance faciale facilite grandement l'organisation

Vos photos sont vos souvenirs. Avec les bons outils et une organisation rigoureuse, vous pourrez les retrouver, les apprécier et les partager facilement, aujourd'hui comme dans 20 ans.

**Prochaine étape** : Vous avez maintenant toutes les connaissances pour gérer, organiser et retoucher vos collections de photos sous Linux Mint !

---

*Bonnes photos et bonne organisation ! 📷✨*

⏭️ [Gaming sous Linux](/14-gaming-sous-linux/README.md)
