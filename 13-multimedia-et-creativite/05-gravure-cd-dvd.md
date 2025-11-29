🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 13.5 Gravure CD/DVD (Brasero)

## Introduction

Bien que les CD et DVD soient moins utilisés qu'avant (l'ère du cloud et des clés USB), ils restent utiles dans certaines situations : archivage à long terme, compatibilité avec anciens appareils, gravure de CD audio pour la voiture, sauvegarde physique sécurisée, ou création de DVD vidéo pour lecteurs de salon.

Linux Mint inclut tous les outils nécessaires pour graver facilement des CD et DVD, avec **Brasero** comme logiciel principal.

Dans ce chapitre, nous allons découvrir :

- **Les types de disques** : CD, DVD, Blu-ray et leurs variantes
- **Brasero** : le logiciel de gravure par défaut
- **Gravure de données** : sauvegarder vos fichiers
- **CD audio** : créer des compilations musicales
- **Gravure d'images ISO** : installer des systèmes d'exploitation
- **Copie de disques** : dupliquer des CD/DVD
- **Alternatives** : K3b, Xfburn, outils en ligne de commande

> **Bon à savoir** : La gravure sous Linux est stable et fiable. Vous pouvez graver tous types de disques sans logiciels propriétaires.

---

## Comprendre les types de disques

### CD (Compact Disc)

**Capacité standard :** 700 Mo (ou 80 minutes audio)

**Types de CD :**

| Type | Description | Usage |
|------|-------------|-------|
| **CD-R** | Enregistrable une fois | Sauvegarde définitive, CD audio |
| **CD-RW** | Réinscriptible (effaçable) | Sauvegardes temporaires, tests |

**Utilisations :**
- CD audio pour voiture/chaîne hi-fi
- Petites sauvegardes (moins de 700 Mo)
- Distribution de petits fichiers

### DVD (Digital Versatile Disc)

**Capacités courantes :**
- **DVD simple couche** : 4.7 Go
- **DVD double couche** : 8.5 Go

**Types de DVD :**

| Type | Description | Capacité | Usage |
|------|-------------|----------|-------|
| **DVD-R** | Enregistrable une fois | 4.7 Go | Sauvegarde, vidéos |
| **DVD+R** | Enregistrable une fois (variante) | 4.7 Go | Même usage que DVD-R |
| **DVD-RW** | Réinscriptible | 4.7 Go | Sauvegardes réutilisables |
| **DVD+RW** | Réinscriptible (variante) | 4.7 Go | Même usage que DVD-RW |
| **DVD-R DL** | Double couche | 8.5 Go | Grosses sauvegardes |

> **DVD-R ou DVD+R ?** Les deux fonctionnent sur la plupart des graveurs modernes. DVD-R est légèrement plus compatible avec les anciens lecteurs.

**Utilisations :**
- Sauvegardes de données importantes
- DVD vidéo pour lecteurs de salon
- Distribution de logiciels
- Archives à long terme

### Blu-ray

**Capacités :**
- **BD-R simple couche** : 25 Go
- **BD-R double couche** : 50 Go
- **BD-R XL** : 100 Go ou 128 Go

**Types :**
- **BD-R** : Enregistrable une fois
- **BD-RE** : Réinscriptible

**Utilisations :**
- Archivage de très grandes quantités de données
- Sauvegardes vidéo haute qualité
- Films en haute définition

> **Note** : Les graveurs Blu-ray sont plus rares et chers. La plupart des utilisateurs ont des graveurs DVD.

### DVD vs USB vs Cloud : Quand utiliser quoi ?

| Critère | CD/DVD | Clé USB | Cloud |
|---------|--------|---------|-------|
| **Capacité** | 700 Mo - 8.5 Go | 8 Go - 1 To | Illimité (payant) |
| **Vitesse** | Lente | Rapide | Variable (Internet) |
| **Réutilisable** | RW oui, R non | Oui | Oui |
| **Durée de vie** | 10-30 ans (conditions optimales) | 10 ans | Tant que service existe |
| **Transportable** | Oui | Très | Non (besoin Internet) |
| **Coût** | Très faible | Moyen | Récurrent |
| **Sécurité physique** | Excellent (hors ligne) | Bon | Moyen (dépend fournisseur) |

**Utilisez les CD/DVD pour :**
- ✅ Archives à long terme (photos de famille)
- ✅ CD audio pour voiture
- ✅ Distribution physique (pas de connexion Internet)
- ✅ Sauvegardes hors ligne (protection ransomware)
- ✅ Compatibilité avec anciens appareils

**Préférez USB/Cloud pour :**
- ❌ Transferts fréquents (USB plus pratique)
- ❌ Grosses quantités de données (> 8.5 Go)
- ❌ Accès rapide et régulier
- ❌ Partage facile en ligne

---

## Brasero - Le logiciel de gravure

### Qu'est-ce que Brasero ?

Brasero est le logiciel de gravure par défaut sur Linux Mint (environnements GNOME/Cinnamon). Il offre une interface simple et intuitive pour graver tous types de disques.

**Points forts :**
- Interface claire et simple
- Support CD, DVD, Blu-ray
- Gravure de données, audio, vidéo, ISO
- Copie de disques
- Effacement de disques réinscriptibles
- Vérification après gravure
- Création d'images ISO

**Fonctionnalités principales :**
- Projet de données (fichiers et dossiers)
- Projet audio (CD audio)
- Projet vidéo (DVD vidéo)
- Copie de disque
- Gravure d'image (fichiers ISO)
- Effacement de disque

### Installation de Brasero

Brasero est généralement préinstallé. Si ce n'est pas le cas :

**Via le Gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "Brasero"
3. Cliquez sur **Installer**

**Via le terminal :**
```bash
sudo apt update
sudo apt install brasero
```

### Interface de Brasero

Au lancement, Brasero affiche un écran d'accueil avec les options principales :

1. **Projet audio** : créer un CD audio
2. **Projet de données** : graver fichiers et dossiers
3. **Projet vidéo** : créer un DVD vidéo
4. **Copie de disque** : dupliquer un CD/DVD
5. **Graver une image** : graver un fichier ISO

En bas de la fenêtre :
- **Disque à utiliser** : sélection du graveur
- **Espace disponible** : barre indiquant l'espace utilisé/restant

---

## Graver un CD/DVD de données

### Créer un projet de données

Un projet de données vous permet de graver n'importe quels fichiers et dossiers sur un disque.

#### 1. Lancer un nouveau projet

- Ouvrez **Brasero**
- Cliquez sur **Projet de données**

Vous voyez maintenant :
- Zone supérieure vide : le contenu de votre futur disque
- Zone inférieure : votre système de fichiers (explorateur)
- Barre en bas : espace utilisé sur le disque

#### 2. Ajouter des fichiers

**Méthodes pour ajouter du contenu :**

**Glisser-déposer :**
- Ouvrez votre gestionnaire de fichiers (Nemo)
- Glissez-déposez vos fichiers/dossiers dans la zone supérieure de Brasero

**Depuis Brasero :**
- Naviguez dans la zone inférieure de Brasero
- Cliquez sur le bouton **+** (Ajouter)
- Sélectionnez fichiers/dossiers

**Menu :**
- `Édition` → `Ajouter des fichiers`

#### 3. Organiser le contenu

Vous pouvez organiser les fichiers sur le disque :
- **Créer un dossier** : clic droit dans zone supérieure → `Nouveau dossier`
- **Renommer** : clic droit sur fichier → `Renommer`
- **Supprimer** : sélectionnez et appuyez sur `Suppr`
- **Déplacer** : glissez-déposez dans les dossiers

#### 4. Vérifier l'espace

Surveillez la barre en bas :
- **Vert** : espace utilisé
- **Gris** : espace restant
- **Rouge** : dépassement (trop de données)

**Capacités rappel :**
- CD : 700 Mo
- DVD : 4.7 Go (ou 8.5 Go double couche)

#### 5. Options de gravure

Avant de graver, cliquez sur le bouton **Graver** (icône de disque en feu).

**Fenêtre d'options :**

**Onglet "Options" :**
- **Vitesse de gravure** : choisissez une vitesse (voir section suivante)
- **Simulation** : teste la gravure sans écrire (option avancée)

**Onglet "Options avancées" :**
- **Burnproof** : protection contre les erreurs (laissez coché)
- **Éjecter le disque** : éjection automatique après gravure
- **Vérifier les données** : vérifie l'intégrité après gravure (recommandé)

#### 6. Graver

- Insérez un disque vierge dans votre graveur
- Cliquez sur **Graver**
- Patientez pendant la gravure (ne touchez pas l'ordinateur)
- À la fin, le disque s'éjecte (si option activée)

**Durée de gravure :**
- Dépend de la vitesse choisie et de la quantité de données
- Environ 5-15 minutes pour un DVD complet

### Vitesse de gravure : quelle vitesse choisir ?

**Règle générale :** Plus lent = plus fiable

| Vitesse | Usage recommandé | Fiabilité |
|---------|------------------|-----------|
| **Maximum** | Données temporaires, tests | Moyenne |
| **8x - 16x** | Usage général, bon compromis | Bonne |
| **4x - 8x** | Données importantes, archivage | Très bonne |
| **2x - 4x** | Archivage long terme, compatibilité max | Excellente |

**Conseils :**
- Pour archives importantes : 4x maximum
- Pour compatibilité avec vieux lecteurs : 4x
- Pour disques de marque bas de gamme : réduire la vitesse
- Pour disques de qualité (Verbatim, TDK) : 8x-16x acceptable

### Multisession : ajouter des données plus tard

Par défaut, Brasero grave en session fermée (finalisée). Vous pouvez activer la **multisession** pour ajouter des données ultérieurement.

**Activer la multisession :**
1. Dans les options de gravure
2. Onglet "Options avancées"
3. Décochez **Finaliser le disque** (ou cochez "Multisession")

**Ajouter des données à un disque multisession :**
1. Insérez le disque
2. Créez un nouveau projet de données
3. Brasero détecte les données existantes
4. Ajoutez de nouveaux fichiers
5. Gravez

> **Attention** : Les disques multisession sont parfois moins compatibles avec certains lecteurs.

---

## Créer un CD audio

Un CD audio est un disque lisible par les chaînes hi-fi, autoradios et lecteurs CD classiques.

### Différence CD audio vs CD de données MP3

**CD audio :**
- Format standard Red Book
- Lisible sur TOUS les lecteurs CD
- Environ 80 minutes de musique
- Fichiers convertis en format CDDA (pistes audio)

**CD de données MP3 :**
- Simple CD de données contenant des fichiers MP3
- Lisible uniquement sur lecteurs compatibles MP3
- Peut contenir 100-200 chansons (selon qualité MP3)
- Pas compatible chaînes hi-fi basiques

### Créer un CD audio avec Brasero

#### 1. Nouveau projet audio

- Ouvrez **Brasero**
- Cliquez sur **Projet audio**

#### 2. Ajouter vos morceaux

**Glisser-déposer :**
- Depuis votre gestionnaire de fichiers
- Glissez vos fichiers audio dans Brasero

**Via le bouton + :**
- Cliquez sur **+** (Ajouter)
- Sélectionnez vos morceaux

**Formats supportés :**
- MP3, FLAC, OGG, WAV, AAC, M4A, etc.
- Brasero convertit automatiquement en format CD audio

#### 3. Organiser les pistes

**Ordre des pistes :**
- Glissez-déposez pour réorganiser
- L'ordre dans la liste = ordre sur le CD

**Informations des pistes :**
- Titre, artiste, durée affichés
- Éditable : clic droit → `Propriétés`

**Pauses entre pistes :**
- Par défaut : 2 secondes
- Modifiable : `Édition` → `Propriétés du projet`

#### 4. Vérifier la durée totale

- En bas : durée totale et espace utilisé
- Maximum : environ 80 minutes (ou 700 Mo)
- Barre rouge si dépassement

#### 5. Options spécifiques CD audio

**Normalisation audio :**
- `Édition` → `Propriétés du projet`
- Cochez **Normaliser** : égalise le volume de toutes les pistes

**Texte CD (CD-Text) :**
- Permet d'afficher titre/artiste sur lecteurs compatibles
- Activable dans les options avancées

#### 6. Graver le CD audio

- Insérez un CD-R vierge (pas CD-RW pour compatibilité)
- Cliquez sur **Graver**
- Choisissez une vitesse modérée (4x-8x recommandé)
- Cochez **Finaliser le disque**
- Lancez la gravure

**Durée :** Environ 10-20 minutes pour un CD complet

> **Astuce** : Utilisez des CD-R de marque (Verbatim, TDK, Sony) pour meilleure compatibilité et longévité.

---

## Graver une image ISO

Une image ISO est un fichier qui contient l'intégralité d'un CD/DVD. Cas d'usage typique : installer Linux ou un autre système d'exploitation.

### Qu'est-ce qu'un fichier ISO ?

Un fichier **ISO** (extension `.iso`) est une copie exacte (image) d'un disque. Il contient :
- Tous les fichiers et dossiers
- La structure du disque
- Les informations de boot (démarrage)

**Utilisations courantes :**
- Installer Linux (Linux Mint, Ubuntu, etc.)
- Installer Windows
- Logiciels de récupération système
- Jeux sur DVD

### Graver un ISO avec Brasero

#### Méthode 1 : Depuis Brasero

1. Ouvrez **Brasero**
2. Cliquez sur **Graver une image**
3. Cliquez sur **Cliquer ici pour sélectionner une image disque**
4. Naviguez vers votre fichier `.iso`
5. Sélectionnez le graveur
6. **Important** : Choisissez vitesse modérée (4x-8x)
7. Cochez **Vérifier le disque après la gravure** (crucial pour ISO bootables)
8. Cliquez sur **Créer une image**

#### Méthode 2 : Depuis le fichier ISO

1. Clic droit sur le fichier `.iso`
2. `Ouvrir avec` → `Brasero`
3. Brasero s'ouvre directement en mode gravure d'image
4. Suivez les étapes comme ci-dessus

### Vérification après gravure

**Très important pour ISO bootables :**
- Cochez toujours **Vérifier les données gravées**
- Brasero compare le disque gravé à l'ISO original
- Si erreurs : le disque est inutilisable, recommencez

**Pourquoi vérifier ?**
- ISO bootable corrompu = PC qui ne boot pas
- Perte de temps si découvert après
- Quelques minutes de vérification évitent frustrations

### Créer une image ISO à partir d'un disque

Vous pouvez aussi faire l'inverse : créer un fichier ISO depuis un CD/DVD existant.

1. Insérez le disque à copier
2. Brasero : **Copie de disque**
3. Sélectionnez le lecteur source
4. Cochez **Image disque** comme destination
5. Choisissez nom et emplacement du fichier ISO
6. Cliquez sur **Créer une image**

**Utilité :**
- Sauvegarder un disque important
- Partager le contenu sans le disque physique
- Créer plusieurs copies sans re-graver depuis l'original

---

## Copier un CD/DVD

Brasero permet de dupliquer facilement des CD/DVD.

### Copie disque à disque

**Si vous avez un seul graveur :**

1. Brasero : **Copie de disque**
2. Sélectionnez le lecteur source
3. Cochez **Image temporaire** (Brasero crée une copie sur disque dur)
4. Cliquez sur **Copier**
5. Brasero lit le disque source
6. Insérez un disque vierge quand demandé
7. Brasero grave la copie

**Si vous avez deux lecteurs :**

1. Brasero : **Copie de disque**
2. Source : lecteur avec le disque à copier
3. Destination : graveur avec disque vierge
4. Cliquez sur **Copier**
5. Copie directe sans étape intermédiaire

### Restrictions légales

**Important :** Ne copiez que ce que vous avez le droit de copier.

**Autorisé :**
- ✅ Vos propres créations (photos, musique, données)
- ✅ Logiciels libres et open source
- ✅ Distributions Linux
- ✅ Sauvegardes personnelles légales

**Interdit dans la plupart des pays :**
- ❌ Films commerciaux (DVDs du commerce)
- ❌ Jeux vidéo commerciaux
- ❌ Logiciels propriétaires (sauf licence le permettant)
- ❌ CDs de musique commerciaux (sauf usage privé selon pays)

> **Note** : Les lois varient selon les pays. Renseignez-vous sur votre législation locale.

---

## Effacer un disque réinscriptible

Les disques RW (CD-RW, DVD-RW) peuvent être effacés et réutilisés.

### Effacement rapide

1. Insérez le disque RW à effacer
2. Brasero : `Outils` → `Effacer`
3. Sélectionnez le lecteur
4. Choisissez **Effacement rapide**
5. Cliquez sur **Effacer**

**Durée :** 1-2 minutes

**Résultat :** Le disque semble vide, mais données techniquement récupérables.

### Effacement complet

Pour effacement sécurisé (données irrécupérables) :

1. Même processus
2. Choisissez **Effacement complet**
3. Cliquez sur **Effacer**

**Durée :** 20-60 minutes (écrit des zéros partout)

**Résultat :** Données définitivement effacées.

---

## Alternatives à Brasero

### K3b - L'outil KDE

K3b est le logiciel de gravure de l'environnement KDE, très complet et puissant.

**Points forts :**
- Interface riche en fonctionnalités
- Plus d'options que Brasero
- Excellent pour utilisateurs avancés
- Support DVD vidéo avancé
- Rippage de CD audio

**Installation :**
```bash
sudo apt install k3b
```

**Note :** Installera des dépendances KDE (environ 100-200 Mo).

**Fonctionnalités supplémentaires :**
- Création de DVD vidéo (menus, chapitres)
- Extraction (ripping) de CD audio en MP3/FLAC
- Normalisation audio avancée
- Plus d'options de formats

**Quand utiliser K3b :**
- Si vous avez déjà un environnement KDE
- Pour création de DVD vidéo avec menus
- Pour extraction de CD audio
- Si vous trouvez Brasero trop limité

### Xfburn - Léger et simple

Xfburn est le logiciel de gravure de Xfce, très léger.

**Installation :**
```bash
sudo apt install xfburn
```

**Points forts :**
- Très léger (peu de dépendances)
- Interface simple et claire
- Rapide au démarrage

**Idéal pour :**
- Environnement Xfce
- Ordinateurs peu puissants
- Utilisateurs cherchant la simplicité

### Outils en ligne de commande

Pour les utilisateurs avancés ou scripts.

#### wodim (gravure)

Graver un ISO :
```bash
wodim -v dev=/dev/sr0 speed=4 fichier.iso
```

Graver des données :
```bash
genisoimage -o image.iso -R -J /chemin/vers/dossier
wodim -v dev=/dev/sr0 speed=4 image.iso
```

#### cdrecord (ancien nom de wodim)

```bash
cdrecord -v dev=/dev/sr0 speed=4 fichier.iso
```

#### dd (copie bit à bit)

**Attention :** Très puissant mais dangereux si mal utilisé.

Graver un ISO :
```bash
sudo dd if=fichier.iso of=/dev/sr0 bs=4M status=progress
```

> **DANGER** : Vérifiez bien le périphérique (`/dev/sr0`). Une erreur peut effacer votre disque dur !

---

## Créer un DVD vidéo

Un DVD vidéo est un disque lisible sur les lecteurs DVD de salon (pas simplement des fichiers vidéo).

### Avec DeVeDe

DeVeDe est un créateur de DVD vidéo graphique.

**Installation :**
```bash
sudo apt install devede
```

**Processus :**
1. Lancez **DeVeDe**
2. Choisissez **DVD vidéo**
3. **Ajoutez** vos fichiers vidéo
4. Configurez titre, sous-titres, menus
5. **Précédent** → Vérifiez paramètres
6. **Créer ISO** ou **Graver DVD**

**Options disponibles :**
- Menu simple ou personnalisé
- Chapitres
- Sous-titres
- Plusieurs vidéos sur un DVD
- Qualité/compression ajustable

**Durée :**
- Encodage : 30 min - 2h (selon durée vidéo et puissance PC)
- Gravure : 10-30 min

### Avec K3b

K3b offre aussi création de DVD vidéo :
1. **Nouveau projet DVD vidéo**
2. Ajoutez vos vidéos
3. Configurez menus (optionnel)
4. Gravez

---

## Problèmes courants et solutions

### Le graveur n'est pas détecté

**Solutions :**

1. **Vérifiez la connexion :**
   - Disque inséré ?
   - Graveur externe : câble bien branché ?

2. **Vérifiez dans le système :**
```bash
lsblk
```
Cherchez `/dev/sr0` (ou sr1, sr2)

3. **Vérifiez les permissions :**
```bash
sudo chmod a+rw /dev/sr0
```

4. **Redémarrez l'ordinateur**

### Erreur pendant la gravure

**Causes courantes :**
- Disque de mauvaise qualité
- Vitesse trop élevée
- Trop d'applications en arrière-plan
- Disque rayé/sale
- Problème matériel graveur

**Solutions :**

1. **Utilisez des disques de marque** (Verbatim, TDK, Sony)
2. **Réduisez la vitesse** : 4x maximum
3. **Fermez toutes les applications**
4. **Ne touchez pas l'ordinateur** pendant la gravure
5. **Nettoyez le disque** avec un chiffon doux
6. **Essayez un autre disque** pour tester le graveur

### Le disque gravé n'est pas lisible

**Vérifications :**

1. **Le disque a-t-il été finalisé ?**
   - Nécessaire pour compatibilité avec lecteurs

2. **Format compatible ?**
   - CD audio : compatible tous lecteurs
   - DVD vidéo : compatible lecteurs DVD
   - DVD de données : peut nécessiter lecteur récent

3. **Testez sur un autre lecteur**
   - Le lecteur peut être en cause

4. **Vérifiez la vitesse de gravure**
   - Gravure trop rapide = erreurs
   - Recommencez à 4x

5. **Utilisez l'option de vérification**
   - Détecte les erreurs immédiatement

### Brasero plante ou se bloque

**Solutions :**

1. **Mettez à jour Brasero :**
```bash
sudo apt update
sudo apt upgrade brasero
```

2. **Supprimez la configuration :**
```bash
rm -rf ~/.config/brasero
```
Relancez Brasero

3. **Essayez une alternative :**
   - K3b ou Xfburn

4. **Vérifiez les logs :**
```bash
journalctl -xe | grep brasero
```

### CD audio ne lit pas dans la voiture

**Causes possibles :**

1. **CD-RW utilisé :** certains autoradios ne lisent pas les CD-RW
   - Solution : utilisez CD-R

2. **Vitesse de gravure trop élevée**
   - Solution : gravez à 4x maximum

3. **Disque non finalisé**
   - Solution : cochez "Finaliser le disque"

4. **Marque de disque incompatible**
   - Solution : testez autre marque (Verbatim recommandé)

### Espace insuffisant sur le disque

**Solutions :**

1. **Vérifiez la capacité réelle :**
   - CD : 700 Mo
   - DVD : 4.7 Go (en réalité ~4.3 Go utilisables)

2. **Compressez vos fichiers** (si possible)

3. **Utilisez DVD double couche** (8.5 Go)

4. **Séparez en plusieurs disques**

5. **Pour CD audio :** réduisez le nombre de pistes

---

## Conseils pour la gravure et archivage

### Choisir des disques de qualité

**Marques recommandées :**
- **Verbatim** : excellent rapport qualité/prix
- **TDK** : très bonne qualité
- **Sony** : fiable
- **Taiyo Yuden** : qualité pro (cher)

**Évitez :**
- Disques génériques sans marque
- Packs très bon marché (1€ les 100)
- Disques colorés/imprimables bas de gamme

### Vitesse de gravure optimale

**Pour archivage long terme :**
- CD : 4x maximum
- DVD : 4x-8x maximum
- Blu-ray : 4x maximum

**Pourquoi plus lent = mieux ?**
- Meilleure qualité d'écriture
- Moins d'erreurs
- Durée de vie prolongée
- Compatibilité maximale

### Stockage et conservation

**Conditions optimales :**
- **Température** : 15-25°C
- **Humidité** : 20-50%
- **Lumière** : éviter exposition directe au soleil
- **Position** : vertical dans boîtier (pas empilés)

**Protection :**
- Boîtiers individuels (jewel case ou slim case)
- Évitez les pochettes papier (rayures)
- N'écrivez pas sur le disque (sauf marqueurs CD spéciaux)
- Manipulez par les bords

**Durée de vie :**
- **Conditions optimales** : 10-30 ans
- **Conditions moyennes** : 5-10 ans
- **Mauvaises conditions** : 2-5 ans

> **Astuce** : Pour archives importantes, gravez deux copies et stockez dans lieux différents.

### Étiquetage

**Options d'étiquetage :**

1. **Marqueur CD permanent :**
   - Spécialement conçu pour CD/DVD
   - N'endommage pas la couche réfléchissante
   - Simple et rapide

2. **Étiquettes autocollantes :**
   - Rendu professionnel
   - Peut déséquilibrer le disque (à éviter graveurs rapides)
   - Utiliser uniquement étiquettes prévues pour CD/DVD

3. **Impression directe (LightScribe, LabelFlash) :**
   - Nécessite graveur et disques compatibles
   - Résultat pro
   - Plus cher

4. **Boîtier étiqueté :**
   - Solution la plus sûre
   - Étiquetez le boîtier, pas le disque

**Informations à noter :**
- Contenu du disque
- Date de gravure
- Logiciel/format utilisé (si pertinent)

### Vérification et tests

**Après gravure :**
1. **Vérification immédiate** : option dans Brasero
2. **Test de lecture** : ouvrez quelques fichiers
3. **Test sur autre appareil** : vérifiez compatibilité

**Régulièrement (tous les 2-3 ans) :**
- Testez vos archives sur disque
- Recopiez sur nouveaux disques si dégradation
- Migration vers supports modernes (cloud, disques durs)

### Alternative moderne : archivage sur disques M-DISC

**M-DISC** :
- Technologie spéciale gravure
- Durée de vie annoncée : 100-1000 ans
- Compatible graveurs DVD/Blu-ray standard
- Plus cher que disques normaux
- Idéal pour archives vraiment importantes

**Disponible en :**
- DVD M-DISC : 4.7 Go
- Blu-ray M-DISC : 25 Go, 50 Go, 100 Go

---

## Alternatives aux CD/DVD

### Pour sauvegardes

**Disques durs externes :**
- ✅ Très grande capacité (1-5 To)
- ✅ Rapides
- ❌ Fragiles (chocs)
- ❌ Durée de vie : 5-10 ans

**Clés USB :**
- ✅ Compactes et transportables
- ✅ Rapides
- ❌ Capacité limitée (256 Go généralement)
- ❌ Durée de vie : 10 ans

**Cloud :**
- ✅ Accessible partout
- ✅ Sauvegarde automatique
- ❌ Nécessite Internet
- ❌ Coût récurrent
- ❌ Confidentialité (dépend du fournisseur)

**NAS (Network Attached Storage) :**
- ✅ Grande capacité
- ✅ Accessible sur réseau local
- ✅ Redondance possible (RAID)
- ❌ Prix initial élevé
- ❌ Consommation électrique

### Recommandation stratégie 3-2-1

**Pour données importantes :**
1. **3** copies de vos données
2. Sur **2** supports différents
3. **1** copie hors site (autre lieu physique)

**Exemple :**
- Copie 1 : disque dur principal (ordinateur)
- Copie 2 : disque dur externe (chez vous)
- Copie 3 : DVD archivés (chez parents/amis) ou cloud

---

## Conclusion

La gravure de CD/DVD reste pertinente pour certains usages spécifiques : archivage à long terme, compatibilité avec anciens appareils, distribution physique ou création de CD audio pour la voiture.

Linux Mint, via **Brasero**, offre une solution simple et efficace pour tous vos besoins de gravure. L'interface intuitive permet même aux débutants de créer facilement des CD audio, graver des ISO ou sauvegarder des données.

**Points clés à retenir :**
- Brasero couvre 90% des besoins de gravure
- Vitesse réduite (4x-8x) = meilleure qualité et compatibilité
- Utilisez des disques de marque pour archivage important
- Vérifiez toujours après gravure (surtout ISO bootables)
- Stockez vos disques dans de bonnes conditions (température, humidité)
- Pour archives critiques : doublez les copies et diversifiez les supports

Bien que les technologies cloud et USB soient plus modernes, les CD/DVD conservent leur place pour l'archivage physique sécurisé et la compatibilité universelle.

**Prochaine étape** : Dans la section suivante, nous découvrirons la capture d'écran et le screencast sous Linux Mint.

---

*Gravez en toute sérénité ! 💿*

⏭️ [Capture d'écran et screencast (Flameshot, OBS)](/13-multimedia-et-creativite/06-capture-decran-et-screencast.md)
