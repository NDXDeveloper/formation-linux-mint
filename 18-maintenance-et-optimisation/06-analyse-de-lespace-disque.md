🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 18.6 Analyse de l'espace disque (Baobab, ncdu)

## Introduction

Imaginez votre disque dur comme un grand entrepôt. Au fil du temps, vous y stockez des cartons (fichiers et dossiers). Certains sont visibles et bien rangés, d'autres sont cachés dans des coins obscurs. Un jour, l'entrepôt est plein et vous ne savez pas par où commencer le tri !

**L'analyse de l'espace disque** vous permet de :
- Visualiser précisément ce qui occupe votre disque
- Identifier les gros fichiers et dossiers inutiles
- Libérer de l'espace intelligemment
- Comprendre où vont vos gigaoctets

**Dans ce chapitre, vous apprendrez à :**
- Utiliser Baobab pour une visualisation graphique intuitive
- Maîtriser ncdu pour une analyse rapide en terminal
- Exploiter les commandes df et du
- Trouver les fichiers les plus volumineux
- Nettoyer efficacement votre disque

**Pourquoi c'est important ?**
- Éviter le message redouté "Disque plein"
- Optimiser les performances (un disque plein ralentit le système)
- Faire de la place avant une grosse mise à jour
- Comprendre votre utilisation réelle du disque

---

## Comprendre l'espace disque

### Les différents types d'espace

Avant d'analyser, comprenons ce qui occupe un disque dur.

**1. Fichiers utilisateur** (visibles)
- Documents, photos, vidéos, musique
- Téléchargements
- Fichiers de travail

**2. Système d'exploitation** (partiellement visible)
- Linux Mint lui-même (~10-15 Go)
- Applications installées
- Bibliothèques et dépendances

**3. Fichiers cachés** (souvent invisibles aux débutants)
- Cache des applications (~/.cache)
- Fichiers de configuration (~/.config)
- Données d'applications (~/.local)
- Miniatures d'images (~/.cache/thumbnails)

**4. Fichiers système** (nécessitent root pour voir)
- Logs (/var/log)
- Cache des paquets (/var/cache/apt)
- Fichiers temporaires (/tmp, /var/tmp)

### Vérification rapide de l'espace disponible

**Commande la plus simple :**
```bash
df -h
```

**Résultat typique :**
```
Sys. de fichiers Taille Utilisé Dispo Uti% Monté sur
/dev/sda2          234G    156G   67G  70% /
/dev/sda1          511M     5.3M 506M   2% /boot/efi
tmpfs              3.1G     2.3M 3.1G   1% /run
```

**Explication :**
- **Taille** : capacité totale de la partition
- **Utilisé** : espace occupé
- **Dispo** : espace libre restant
- **Uti%** : pourcentage d'utilisation
- **Monté sur** : point de montage (/ = partition système principale)

**Ligne importante :** Celle avec `/` à la fin (votre partition système).

**Interprétation :**
- **0-70%** : espace suffisant ✅
- **70-85%** : commencez à surveiller ⚠️
- **85-95%** : nettoyage recommandé 🟠
- **95-100%** : nettoyage urgent ! 🔴

### Où va l'espace disque typiquement ?

**Sur un système de bureau Linux Mint classique :**

| Catégorie | Espace typique | Exemples |
|-----------|----------------|----------|
| Système de base | 10-15 Go | Linux Mint + pilotes |
| Applications | 5-20 Go | Firefox, LibreOffice, GIMP, Steam, etc. |
| Fichiers utilisateur | Variable | Photos, vidéos, documents |
| Cache navigateur | 1-5 Go | Firefox, Chrome |
| Cache système | 2-10 Go | APT, miniatures, logs |
| Jeux (Steam, etc.) | 0-500 Go | Selon votre collection |

**Les gros consommateurs d'espace :**
1. 🎮 **Jeux vidéo** : 20-100 Go par jeu AAA
2. 🎬 **Vidéos** : 1-10 Go par film
3. 📸 **Photos (RAW)** : 20-50 Mo par photo
4. 🎵 **Musique FLAC** : 30-50 Mo par chanson
5. 💾 **Machines virtuelles** : 10-50 Go par VM
6. 🗄️ **Sauvegardes locales** : selon vos données

---

## Baobab : Analyseur d'utilisation des disques (Interface graphique)

**Baobab** (aussi appelé "Analyseur d'utilisation des disques") est l'outil graphique parfait pour les débutants.

### Lancement de Baobab

**Méthode 1 : Menu**
1. Menu > **Accessoires** > **Analyseur d'utilisation des disques**

**Méthode 2 : Recherche**
1. Appuyez sur `Super` (touche Windows)
2. Tapez "disque" ou "baobab"
3. Cliquez sur l'icône

**Méthode 3 : Terminal**
```bash
baobab &
```

**Vérifier l'installation :**
```bash
which baobab
```

**Si absent, installer :**
```bash
sudo apt install baobab
```

### Première utilisation

Au lancement, Baobab vous propose plusieurs options :

1. **Scanner le dossier personnel** (recommandé pour débuter)
   - Analyse votre /home/votre-nom
   - Ne nécessite pas de droits root
   - Montre vos documents, téléchargements, cache, etc.

2. **Scanner le système de fichiers**
   - Analyse tout le disque (/)
   - Nécessite les droits root
   - Utile pour voir ce qui consomme au niveau système

3. **Scanner un dossier**
   - Choisissez un dossier spécifique
   - Pratique pour analyser un disque externe

**Pour commencer :** Cliquez sur **"Scanner le dossier personnel"**.

### Interface de Baobab

L'interface se compose de plusieurs éléments :

#### 1. Vue en arborescence (à gauche)

Liste les dossiers et leur taille, triés du plus gros au plus petit :

```
📁 Dossier personnel (125 Go)
  📁 .cache (15.2 Go)
  📁 Téléchargements (12.8 Go)
  📁 Vidéos (45.3 Go)
  📁 Images (23.7 Go)
  📁 Documents (8.2 Go)
  📁 .local (6.5 Go)
  ...
```

**Cliquez sur un dossier** pour voir son contenu détaillé.

#### 2. Vue graphique (à droite)

**Deux types de visualisation :**

**a) Diagramme en secteurs (camembert)**
- Chaque secteur représente un dossier
- Plus le secteur est grand, plus le dossier est volumineux
- Les couleurs facilitent l'identification

**b) Vue en anneaux (treemap)**
- Rectangles proportionnels à la taille
- Imbrication visuelle de l'arborescence
- Très intuitif pour repérer les gros fichiers

**Interaction :**
- **Clic** sur un secteur/rectangle : entre dans ce dossier
- **Clic droit** : options (ouvrir, supprimer, etc.)
- **Retour en arrière** : bouton dans la barre d'outils

#### 3. Barre d'outils (en haut)

- **Analyser** : relancer une analyse
- **Arrêter** : stopper l'analyse en cours
- **Accueil** : revenir à l'écran d'accueil
- **Flèches** : naviguer dans l'historique

### Analyser le système complet

Pour voir TOUT ce qui consomme de l'espace (y compris fichiers système) :

1. Cliquez sur **"Scanner le système de fichiers"**
2. Entrez votre mot de passe root
3. Attendez l'analyse (peut prendre 1-5 minutes)

**Résultat typique :**

```
/ (156 Go utilisés sur 234 Go)
  📁 home (85 Go)          ← Vos fichiers personnels
  📁 usr (35 Go)           ← Applications et bibliothèques
  📁 var (20 Go)           ← Logs, cache APT, etc.
  📁 opt (8 Go)            ← Applications tierces (Chrome, etc.)
  📁 boot (500 Mo)         ← Noyaux Linux
  📁 tmp (200 Mo)          ← Fichiers temporaires
  ...
```

**Dossiers importants à surveiller :**

| Dossier | Contenu | Taille normale | Si trop gros... |
|---------|---------|----------------|-----------------|
| `/home` | Vos fichiers | Variable | Triez vos documents/photos |
| `/var/log` | Journaux système | 500 Mo - 2 Go | Voir section 18.5 (rotation logs) |
| `/var/cache/apt` | Paquets téléchargés | 1-3 Go | `sudo apt clean` |
| `/usr` | Applications | 15-40 Go | Désinstallez les apps inutiles |
| `/tmp` | Fichiers temporaires | < 500 Mo | Redémarrer nettoie automatiquement |

### Identifier et supprimer les gros fichiers

**Scénario :** Vous voyez que `.cache` fait 15 Go dans votre dossier personnel.

**Étapes :**

1. **Cliquez sur `.cache`** dans Baobab
2. Vous voyez le détail :
   ```
   .cache (15 Go)
     📁 mozilla/firefox (8 Go)
     📁 thumbnails (4 Go)
     📁 chromium (2 Go)
     📁 tracker (1 Go)
   ```

3. **Clic droit sur `thumbnails`** (miniatures d'images)
4. Sélectionnez **"Déplacer vers la corbeille"**
5. Confirmez

**⚠️ Attention :**
- Les miniatures seront régénérées automatiquement quand nécessaire
- Ne supprimez pas de dossiers système sans savoir ce qu'ils contiennent
- En cas de doute, cherchez sur internet avant de supprimer

### Cas pratique avec Baobab

**Objectif :** Vous avez 90% de disque utilisé et devez libérer 20 Go.

**Étape 1 : Scanner le dossier personnel**
```
Résultat :
  Vidéos : 45 Go
  Téléchargements : 12 Go
  .cache : 15 Go
```

**Étape 2 : Trier les vidéos**
- Entrez dans `/Vidéos`
- Identifiez les vieux films que vous avez déjà vus
- Supprimez-les → **Gain : 20 Go** ✅

**Étape 3 : Nettoyer les téléchargements**
- Entrez dans `/Téléchargements`
- Supprimez les fichiers d'installation (.deb, .iso) déjà utilisés
- **Gain : 5 Go** ✅

**Étape 4 : Vider le cache**
- Supprimez `.cache/thumbnails` → **Gain : 4 Go** ✅
- Lancez `sudo apt clean` dans un terminal → **Gain : 2 Go** ✅

**Total libéré : 31 Go** 🎉

---

## ncdu : Analyseur en ligne de commande

**ncdu** (NCurses Disk Usage) est un outil terminal ultra-rapide et efficace.

### Pourquoi utiliser ncdu ?

**Avantages par rapport à Baobab :**
- ⚡ **Très rapide** : analyse 100 Go en quelques secondes
- 💻 **Fonctionne en SSH** : analyser un serveur distant
- 🪶 **Ultra-léger** : consomme très peu de ressources
- ⌨️ **Navigation au clavier** : très efficace une fois maîtrisé
- 📊 **Tri instantané** : par taille, nom, nombre de fichiers

**Inconvénient :** Interface texte (mais très intuitive)

### Installation de ncdu

**Vérifier s'il est installé :**
```bash
ncdu --version
```

**Si absent, installer :**
```bash
sudo apt install ncdu
```

### Lancement de ncdu

**Analyser le dossier actuel :**
```bash
ncdu
```

**Analyser un dossier spécifique :**
```bash
ncdu /home/votre-nom
```

**Analyser tout le système (nécessite root) :**
```bash
sudo ncdu /
```

**Analyser avec exclusion de certains dossiers :**
```bash
ncdu --exclude /proc --exclude /sys /
```

### Interface de ncdu

Une fois lancé, ncdu affiche une interface comme celle-ci :

```
ncdu 1.18 ~ Use the arrow keys to navigate, press ? for help
--- /home/pierre -----------------------------------------------
  45.3 GiB [##########] /Vidéos
  23.7 GiB [#####     ] /Images
  15.2 GiB [###       ] /.cache
  12.8 GiB [##        ] /Téléchargements
   8.2 GiB [#         ] /Documents
   6.5 GiB [#         ] /.local
   3.1 GiB [          ] /Musique
   2.8 GiB [          ] /.config
   1.5 GiB [          ] /.mozilla
 512.0 MiB [          ] /Bureau
```

**Explication :**
- **Colonne de gauche** : taille du dossier
- **Barres de progression** : visualisation proportionnelle
- **Nom du dossier** : à droite

**Tri par défaut :** Du plus gros au plus petit

### Navigation dans ncdu

**Touches essentielles :**

| Touche | Action |
|--------|--------|
| `↑` `↓` | Naviguer entre les dossiers/fichiers |
| `Entrée` | Entrer dans le dossier sélectionné |
| `←` ou `Retour arrière` | Revenir au dossier parent |
| `d` | Supprimer le fichier/dossier sélectionné |
| `n` | Trier par nom |
| `s` | Trier par taille |
| `C` | Trier par nombre d'éléments |
| `g` | Afficher/masquer le graphique en pourcentage |
| `e` | Afficher/masquer les fichiers cachés |
| `i` | Afficher les informations du fichier sélectionné |
| `r` | Recalculer les tailles (après suppression) |
| `q` | Quitter ncdu |
| `?` | Aide |

### Utilisation pas à pas

**Scénario :** Trouver ce qui consomme de l'espace dans votre dossier personnel.

**Étape 1 : Lancer ncdu**
```bash
ncdu ~
```

Attendez l'analyse (5-30 secondes selon la quantité de fichiers).

**Étape 2 : Identifier le plus gros dossier**

Vous voyez :
```
  45.3 GiB [##########] /Vidéos
```

**Étape 3 : Entrer dans ce dossier**

Appuyez sur `Entrée` (sur la ligne `/Vidéos`).

**Étape 4 : Explorer le contenu**

```
--- /home/pierre/Vidéos ----------------------------------------
  15.2 GiB [#####     ]  film_vacances_2019.mp4
  12.8 GiB [####      ]  conference_3_heures.mkv
   8.5 GiB [###       ]  tuto_linux_complet.mp4
   5.2 GiB [##        ]  serie_complete/
   3.6 GiB [#         ]  vieux_films/
```

**Étape 5 : Supprimer un gros fichier inutile**

1. Naviguez jusqu'à `conference_3_heures.mkv` (que vous n'avez jamais regardée)
2. Appuyez sur `d`
3. Confirmez avec `yes`

**Gain : 12.8 Go libérés** ✅

**Étape 6 : Revenir en arrière**

Appuyez sur `←` pour remonter d'un niveau.

**Étape 7 : Actualiser l'affichage**

Appuyez sur `r` pour recalculer les tailles après suppression.

### Supprimer des fichiers avec ncdu

**⚠️ Attention : La suppression avec ncdu est IMMÉDIATE et DÉFINITIVE !**

Contrairement à Baobab qui déplace vers la corbeille, ncdu **supprime directement**.

**Procédure sécurisée :**

1. Positionnez-vous sur le fichier/dossier
2. Appuyez sur `d`
3. ncdu affiche :
   ```
   Delete "/home/pierre/Vidéos/vieux_film.mp4"?
   yes/no/all
   ```
4. **Lisez attentivement le chemin complet**
5. Tapez `yes` et `Entrée` pour confirmer
6. Ou `no` pour annuler

**Supprimer tout le contenu d'un dossier :**

1. Positionnez-vous sur le dossier
2. Appuyez sur `d`
3. Tapez `all` pour supprimer le dossier ET son contenu

**Ne JAMAIS faire :**
- Supprimer des dossiers système (`/usr`, `/var`, `/etc`, `/bin`, etc.)
- Supprimer sans vérifier le chemin complet
- Utiliser `all` sans être absolument certain

### Astuces avancées avec ncdu

#### Sauvegarder l'analyse pour consultation ultérieure

**Exporter l'analyse :**
```bash
ncdu -o analyse-home.json ~
```

**Consulter plus tard :**
```bash
ncdu -f analyse-home.json
```

**Utilité :** Comparer l'utilisation disque avant/après nettoyage.

#### Analyser plusieurs disques

**Analyser un disque externe :**
```bash
ncdu /media/votre-nom/MonDisque
```

#### Exclure des dossiers de l'analyse

**Exclure les dossiers système virtuels (plus rapide) :**
```bash
sudo ncdu --exclude /proc --exclude /sys --exclude /dev --exclude /run /
```

#### Afficher uniquement les 20 plus gros dossiers

**Avec l'option -1 :**
```bash
ncdu -1 ~
```

Affiche seulement le premier niveau (plus rapide pour une vue d'ensemble).

---

## La commande du : Analyse basique

**du** (Disk Usage) est la commande classique pour analyser l'espace disque.

### Syntaxe de base

```bash
du [options] [dossier]
```

### Options essentielles

**-h : Human readable (tailles lisibles)**
```bash
du -h
```

Affiche en Ko, Mo, Go au lieu d'octets.

**-s : Summary (résumé)**
```bash
du -sh /home/pierre
```

Affiche uniquement le total du dossier (pas les sous-dossiers).

**-a : All (tout)**
```bash
du -ah ~
```

Affiche fichiers ET dossiers (par défaut, seulement les dossiers).

**-c : Total (cumul)**
```bash
du -ch ~/Documents
```

Ajoute un total à la fin.

**--max-depth=N : Profondeur maximale**
```bash
du -h --max-depth=1 ~
```

Affiche seulement N niveaux de profondeur.

### Exemples pratiques

#### Taille totale du dossier personnel

```bash
du -sh ~
```

**Résultat :**
```
125G    /home/pierre
```

#### Taille de chaque sous-dossier (1er niveau)

```bash
du -h --max-depth=1 ~ | sort -rh
```

**Résultat :**
```
125G    /home/pierre
45G     /home/pierre/Vidéos
24G     /home/pierre/Images
15G     /home/pierre/.cache
13G     /home/pierre/Téléchargements
8.2G    /home/pierre/Documents
...
```

**Explication :**
- `du -h --max-depth=1 ~` : taille de chaque sous-dossier
- `sort -rh` : trie par taille décroissante (-r = reverse, -h = human-readable)

#### Trouver les 10 plus gros dossiers

```bash
du -h --max-depth=2 ~ | sort -rh | head -n 10
```

**Résultat :**
```
125G    /home/pierre
45G     /home/pierre/Vidéos
24G     /home/pierre/Images
15G     /home/pierre/.cache
13G     /home/pierre/Téléchargements
12G     /home/pierre/Vidéos/Films
8.2G    /home/pierre/Documents
6.5G    /home/pierre/.local
5.8G    /home/pierre/Images/Photos_2023
4.2G    /home/pierre/.cache/mozilla
```

#### Taille des dossiers cachés

```bash
du -sh ~/.[^.]*
```

**Résultat :**
```
15G     /home/pierre/.cache
6.5G    /home/pierre/.local
2.8G    /home/pierre/.config
1.5G    /home/pierre/.mozilla
...
```

#### Analyser tout le système (root)

```bash
sudo du -h --max-depth=1 / | sort -rh
```

**Résultat :**
```
156G    /
85G     /home
35G     /usr
20G     /var
8.0G    /opt
...
```

---

## Trouver les plus gros fichiers

### Avec find et sort

**Trouver les 20 plus gros fichiers dans votre dossier personnel :**

```bash
find ~ -type f -exec du -h {} + | sort -rh | head -n 20
```

**Résultat :**
```
15G     /home/pierre/Vidéos/film_vacances_2019.mp4
12G     /home/pierre/Téléchargements/ubuntu-22.04.iso
8.5G    /home/pierre/Vidéos/tuto_linux.mp4
5.2G    /home/pierre/.local/share/Steam/steamapps/common/game/data.pak
...
```

**Explication :**
- `find ~ -type f` : trouve tous les fichiers (pas les dossiers)
- `-exec du -h {} +` : calcule leur taille
- `sort -rh` : trie par taille décroissante
- `head -n 20` : affiche les 20 premiers

### Fichiers de plus de 1 Go

**Trouver tous les fichiers de plus de 1 Go :**

```bash
find ~ -type f -size +1G -exec du -h {} +
```

**Ou avec ls pour plus de détails :**

```bash
find ~ -type f -size +1G -exec ls -lh {} \;
```

**Résultat :**
```
-rw-r--r-- 1 pierre pierre 15G nov.  15 10:23 /home/pierre/Vidéos/film.mp4
-rw-r--r-- 1 pierre pierre 12G nov.  10 14:15 /home/pierre/Téléchargements/ubuntu.iso
...
```

### Fichiers non modifiés depuis longtemps

**Fichiers de plus de 500 Mo non utilisés depuis 1 an :**

```bash
find ~ -type f -size +500M -mtime +365 -exec ls -lh {} \;
```

**Explication :**
- `-size +500M` : plus de 500 Mo
- `-mtime +365` : modifiés il y a plus de 365 jours

**Candidats parfaits pour suppression :** Vieux fichiers volumineux que vous n'avez pas touchés depuis un an.

---

## Outils complémentaires

### dust : Alternative moderne à du

**dust** est une version moderne et colorée de `du`.

**Installation :**
```bash
cargo install du-dust
```

**Ou via les dépôts (si disponible) :**
```bash
sudo apt install dust
```

**Utilisation :**
```bash
dust
```

**Affiche automatiquement :**
- Tailles en ordre décroissant
- Graphiques en couleurs
- Arborescence visuelle

### qdirstat : Version graphique avancée

**qdirstat** est une alternative à Baobab avec plus de fonctionnalités.

**Installation :**
```bash
sudo apt install qdirstat
```

**Fonctionnalités supplémentaires :**
- Détection des fichiers en double
- Statistiques avancées
- Filtrage par type de fichier
- Actions personnalisables

### filelight : Analyseur KDE

Pour les utilisateurs KDE :

**Installation :**
```bash
sudo apt install filelight
```

**Visualisation :** Diagramme circulaire interactif très intuitif.

---

## Scénarios de nettoyage pratiques

### Scénario 1 : Le disque est plein à 95%

**Diagnostic avec ncdu :**

```bash
sudo ncdu /
```

**Résultat typique :**
```
  85 GiB [########  ] /home
  35 GiB [###       ] /usr
  20 GiB [##        ] /var
```

**Plan d'action :**

1. **Nettoyer /var (logs et cache APT)**
   ```bash
   sudo apt clean
   sudo journalctl --vacuum-size=500M
   sudo find /var/log -name "*.gz" -delete
   ```
   **Gain attendu : 5-15 Go**

2. **Nettoyer le dossier personnel**
   ```bash
   ncdu ~
   ```
   Supprimez :
   - Vieux téléchargements
   - Vidéos déjà visionnées
   - Cache navigateur (rm -rf ~/.cache/mozilla ~/.cache/chromium)
   **Gain attendu : 10-30 Go**

3. **Désinstaller applications inutilisées**
   ```bash
   sudo apt autoremove
   ```
   **Gain attendu : 1-5 Go**

### Scénario 2 : Vous ne savez pas où sont vos fichiers

**Rechercher tous les fichiers vidéo de plus de 500 Mo :**

```bash
find ~ -type f \( -name "*.mp4" -o -name "*.mkv" -o -name "*.avi" \) -size +500M -exec du -h {} + | sort -rh
```

**Rechercher toutes les images de plus de 10 Mo :**

```bash
find ~ -type f \( -name "*.jpg" -o -name "*.png" -o -name "*.raw" \) -size +10M -exec du -h {} + | sort -rh
```

### Scénario 3 : Cache navigateur trop gros

**Vérifier la taille du cache Firefox :**

```bash
du -sh ~/.cache/mozilla/firefox
```

**Vider le cache Firefox :**
```bash
rm -rf ~/.cache/mozilla/firefox/*
```

**Vider le cache Chromium :**
```bash
rm -rf ~/.cache/chromium
```

**Gain typique : 2-8 Go**

### Scénario 4 : Miniatures d'images

Les miniatures (thumbnails) peuvent occuper plusieurs Go.

**Vérifier :**
```bash
du -sh ~/.cache/thumbnails
```

**Supprimer :**
```bash
rm -rf ~/.cache/thumbnails/*
```

**Note :** Elles seront régénérées automatiquement quand vous naviguerez dans vos photos.

---

## Script d'analyse automatique

Créez un script qui vous donne un rapport complet de l'utilisation disque.

```bash
nano ~/analyse-disque.sh
```

Contenu :

```bash
#!/bin/bash

echo "========================================"  
echo "📊 Rapport d'analyse de l'espace disque"  
echo "========================================"  
echo ""  

# 1. Vue d'ensemble du système
echo "💽 Vue d'ensemble des partitions :"  
echo "-----------------------------------"  
df -h | grep -E "^/dev"  
echo ""  

# 2. Espace utilisé vs disponible
USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')  
if [ "$USAGE" -gt 85 ]; then  
    echo "⚠️  ATTENTION : Disque utilisé à ${USAGE}% !"
elif [ "$USAGE" -gt 70 ]; then
    echo "⚠️  Surveillance recommandée : Disque à ${USAGE}%"
else
    echo "✅ Espace disque OK : ${USAGE}% utilisé"
fi  
echo ""  

# 3. Top 10 des plus gros dossiers dans /home
echo "📁 Top 10 des plus gros dossiers dans votre profil :"  
echo "----------------------------------------------------"  
du -h --max-depth=1 ~ 2>/dev/null | sort -rh | head -n 10  
echo ""  

# 4. Taille des caches
echo "🗃️  Taille des fichiers de cache :"  
echo "-----------------------------------"  
echo "Cache navigateur (Firefox) : $(du -sh ~/.cache/mozilla 2>/dev/null | cut -f1)"  
echo "Cache miniatures : $(du -sh ~/.cache/thumbnails 2>/dev/null | cut -f1)"  
echo "Cache total : $(du -sh ~/.cache 2>/dev/null | cut -f1)"  
echo ""  

# 5. Fichiers de plus de 1 Go
echo "📦 Fichiers de plus de 1 Go dans votre profil :"  
echo "------------------------------------------------"  
find ~ -type f -size +1G -exec du -h {} + 2>/dev/null | sort -rh | head -n 5  
echo ""  

# 6. Espace récupérable
echo "♻️  Espace potentiellement récupérable :"  
echo "----------------------------------------"  
APT_CACHE=$(du -sh /var/cache/apt/archives 2>/dev/null | cut -f1)  
JOURNAL=$(journalctl --disk-usage 2>/dev/null | grep -oP '\d+\.\d+[GM]' | head -n1)  
echo "Cache APT : $APT_CACHE (exécutez : sudo apt clean)"  
echo "Journaux système : $JOURNAL (exécutez : sudo journalctl --vacuum-size=500M)"  
echo ""  

# 7. Recommandations
echo "💡 Recommandations :"  
echo "--------------------"  
if [ "$USAGE" -gt 85 ]; then  
    echo "1. Supprimez les gros fichiers inutiles"
    echo "2. Videz le cache : rm -rf ~/.cache/*"
    echo "3. Nettoyez APT : sudo apt clean && sudo apt autoremove"
    echo "4. Vérifiez les téléchargements et vidéos"
elif [ "$USAGE" -gt 70 ]; then
    echo "1. Surveillez l'espace disque régulièrement"
    echo "2. Envisagez un nettoyage léger des caches"
else
    echo "Aucune action urgente nécessaire. Système sain !"
fi  
echo ""  

echo "✅ Analyse terminée !"  
echo "Pour une analyse interactive : ncdu ~ ou baobab"  
```

Rendez-le exécutable :
```bash
chmod +x ~/analyse-disque.sh
```

Exécutez-le :
```bash
~/analyse-disque.sh
```

**Automatisation :**

Pour recevoir un rapport hebdomadaire :
```bash
crontab -e
```

Ajoutez :
```
0 9 * * 1 ~/analyse-disque.sh | mail -s "Rapport disque hebdomadaire" votre@email.com
```

---

## Bonnes pratiques d'analyse et nettoyage

### ✅ À faire régulièrement

**Hebdomadaire :**
- Vérifier l'espace disponible avec `df -h`
- Vider la corbeille manuellement

**Mensuel :**
- Analyser avec Baobab ou ncdu
- Supprimer les vieux téléchargements
- Vider le cache navigateur

**Trimestriel :**
- Nettoyage complet avec script automatique
- Désinstaller les applications inutilisées
- Nettoyer les logs (voir section 18.5)

### ❌ À éviter

1. **Ne supprimez jamais** :
   - Dossiers système (`/bin`, `/usr`, `/lib`, `/etc`)
   - Fichiers dont vous ne connaissez pas l'utilité
   - Tout ce qui commence par `.` sans savoir ce que c'est

2. **N'utilisez pas** `rm -rf /` ou variations dangereuses

3. **Ne videz pas** `/tmp` manuellement (le système le fait au redémarrage)

4. **Ne supprimez pas** les fichiers cachés `.config` sans savoir (configurations d'applications)

### 🎯 Objectifs de stockage

**Partition système (/) :**
- **Idéal** : 30-50% utilisé
- **Acceptable** : 50-80% utilisé
- **Attention** : 80-90% utilisé
- **Critique** : >90% utilisé

**Partition home (/home) :**
- Dépend de vos fichiers personnels
- Gardez au moins 10-15% libre

### 📊 Fréquence d'analyse recommandée

| Profil | Fréquence Baobab/ncdu | Fréquence script | Nettoyage |
|--------|-----------------------|------------------|-----------|
| Utilisateur léger (< 100 Go) | Mensuel | Trimestriel | Tous les 3 mois |
| Utilisateur moyen (100-500 Go) | Bimensuel | Mensuel | Tous les 2 mois |
| Utilisateur intensif (> 500 Go) | Hebdomadaire | Hebdomadaire | Mensuel |
| Créateur de contenu (vidéo/photo) | Hebdomadaire | Hebdomadaire | Mensuel |

---

## Résumé des outils

### Comparatif rapide

| Outil | Type | Rapidité | Facilité | Précision | Interactivité |
|-------|------|----------|----------|-----------|---------------|
| **Baobab** | GUI | Moyen | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **ncdu** | CLI | Rapide | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **du** | CLI | Rapide | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ |
| **df** | CLI | Instantané | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐ |

**Recommandation par profil :**
- **Débutant** : Baobab (interface graphique intuitive)
- **Utilisateur confirmé** : ncdu (rapide et efficace)
- **Administrateur système** : du + scripts personnalisés
- **Analyse rapide** : df -h

---

## Commandes essentielles récapitulatives

### Analyse rapide

```bash
# Vue d'ensemble du disque
df -h

# Taille d'un dossier
du -sh ~/Dossier

# Top 10 des plus gros dossiers
du -h --max-depth=1 ~ | sort -rh | head -n 10

# Lancer Baobab
baobab &

# Lancer ncdu
ncdu ~
```

### Recherche de gros fichiers

```bash
# Fichiers de plus de 1 Go
find ~ -type f -size +1G -exec du -h {} + | sort -rh

# Top 20 des plus gros fichiers
find ~ -type f -exec du -h {} + | sort -rh | head -n 20

# Fichiers non utilisés depuis 1 an (> 500 Mo)
find ~ -type f -size +500M -mtime +365 -exec ls -lh {} \;
```

### Nettoyage ciblé

```bash
# Cache navigateur
rm -rf ~/.cache/mozilla  
rm -rf ~/.cache/chromium  

# Miniatures
rm -rf ~/.cache/thumbnails/*

# Cache système
sudo apt clean  
sudo apt autoremove  
```

---

## Conclusion

L'analyse de l'espace disque est une compétence **essentielle** pour maintenir un système sain et performant.

**Les outils à retenir :**

1. 🖥️ **Baobab** : parfait pour les débutants, interface visuelle claire
2. ⚡ **ncdu** : ultra-rapide, idéal pour les utilisateurs confirmés
3. 📊 **du** : commande de base pour scripts et analyses rapides
4. 💾 **df** : vérification instantanée de l'espace disponible

**Workflow recommandé :**

1. **Vérification quotidienne** : `df -h` (2 secondes)
2. **Analyse mensuelle** : Baobab ou ncdu (5 minutes)
3. **Nettoyage trimestriel** : Script automatique + désinstallations (30 minutes)
4. **Sauvegarde** : Avant tout gros nettoyage (voir section 17)

**Règle d'or :** Ne supprimez que ce que vous comprenez. En cas de doute, cherchez des informations avant de supprimer.

**Avec ces outils et connaissances, vous maîtrisez parfaitement la gestion de votre espace disque !** 💾🚀

---

## Pour aller plus loin

- **Section 18.1** : Nettoyage du système (BleachBit, apt clean)
- **Section 18.4** : Optimisation SSD (garder de l'espace libre)
- **Section 18.5** : Gestion des logs (réduire l'espace occupé)
- **Section 17** : Sauvegardes (avant gros nettoyage)
- **Section 8.3** : Gestion des disques (partitionnement)

**Documentation :**
- `man du`
- `man df`
- `man find`
- `man ncdu`
- Site officiel Baobab : https://wiki.gnome.org/Apps/DiskUsageAnalyzer

⏭️ [Vérification de l'intégrité du système](/18-maintenance-et-optimisation/07-verification-de-lintegrite-du-systeme.md)
