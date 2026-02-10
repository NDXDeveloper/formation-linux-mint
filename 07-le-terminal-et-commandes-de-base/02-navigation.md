🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.2 - Navigation (cd, ls, pwd, tree)

## Introduction

Naviguer dans le système de fichiers via le terminal est l'une des compétences fondamentales à maîtriser. C'est l'équivalent de cliquer sur des dossiers dans votre gestionnaire de fichiers, mais en utilisant des commandes textuelles.

**Analogie :** Imaginez que votre système de fichiers est une grande bibliothèque. Les commandes de navigation vous permettent de :
- Savoir dans quelle salle vous êtes (`pwd`)
- Voir quels livres et étagères sont autour de vous (`ls`)
- Vous déplacer vers une autre salle (`cd`)
- Voir le plan complet de la bibliothèque (`tree`)

Dans ce chapitre, nous allons découvrir les quatre commandes essentielles pour vous déplacer comme un expert dans votre système Linux.

---

## Rappel : L'arborescence Linux

Avant de commencer, rappelons quelques notions importantes :

### Structure en arbre

Linux organise tous les fichiers en une structure d'arbre qui part d'un point unique appelé **racine** et noté **/** (slash).

```
/                           (racine)
├── home/                   (dossiers utilisateurs)
│   └── utilisateur/        (votre dossier personnel)
│       ├── Documents/
│       ├── Téléchargements/
│       ├── Images/
│       └── Bureau/
├── etc/                    (fichiers de configuration)
├── var/                    (données variables)
└── usr/                    (programmes)
```

### Chemins absolus vs chemins relatifs

**Chemin absolu :** Commence par `/` et indique le chemin complet depuis la racine.
- Exemple : `/home/utilisateur/Documents/rapport.txt`

**Chemin relatif :** Part de votre position actuelle, sans `/` au début.
- Exemple : `Documents/rapport.txt` (si vous êtes dans `/home/utilisateur/`)

### Symboles spéciaux

- **~** (tilde) : Représente votre dossier personnel (`/home/utilisateur`)
- **.** (point) : Représente le dossier actuel
- **..** (deux points) : Représente le dossier parent (un niveau au-dessus)

---

## La commande `pwd` : Où suis-je ?

### Signification

**pwd** signifie **Print Working Directory** (Afficher le répertoire de travail).

### Utilisation

```bash
pwd
```

Cette commande affiche le chemin complet du dossier où vous vous trouvez actuellement.

### Exemple

```bash
utilisateur@ordinateur:~$ pwd
/home/utilisateur
```

Le terminal vous indique que vous êtes dans `/home/utilisateur` (votre dossier personnel).

### Quand l'utiliser ?

- Quand vous êtes perdu et voulez savoir où vous êtes
- Avant d'exécuter des commandes qui modifient des fichiers
- Pour vérifier que vous êtes au bon endroit

**Conseil :** Le prompt affiche déjà votre position (le `~` ou le nom du dossier), mais `pwd` vous donne le chemin complet et explicite.

---

## La commande `ls` : Qu'est-ce qu'il y a ici ?

### Signification

**ls** signifie **List** (Lister).

### Utilisation de base

```bash
ls
```

Cette commande affiche la liste des fichiers et dossiers dans le répertoire actuel.

### Exemple simple

```bash
utilisateur@ordinateur:~$ ls  
Bureau  Documents  Images  Musique  Téléchargements  Vidéos  
```

### Options courantes

La commande `ls` accepte de nombreuses options pour afficher plus d'informations :

#### `ls -l` : Format long (détaillé)

```bash
ls -l
```

Affiche :
- Les permissions
- Le nombre de liens
- Le propriétaire
- Le groupe
- La taille
- La date de modification
- Le nom

**Exemple :**
```bash
drwxr-xr-x 2 utilisateur utilisateur 4096 nov. 15 10:30 Documents
-rw-r--r-- 1 utilisateur utilisateur 2048 nov. 14 15:45 notes.txt
```

**Lecture :**
- `d` au début = dossier (directory)
- `-` au début = fichier
- La taille est en octets
- Les dates de modification

#### `ls -a` : Afficher tous les fichiers (y compris cachés)

```bash
ls -a
```

Les fichiers cachés sous Linux commencent par un point (`.`).

**Exemple :**
```bash
.  ..  .bashrc  .config  Bureau  Documents
```

**Note :** `.` et `..` sont des références spéciales (dossier actuel et parent).

#### `ls -h` : Tailles lisibles par l'humain

```bash
ls -lh
```

Affiche les tailles en Ko, Mo, Go au lieu d'octets.

**Exemple :**
```bash
-rw-r--r-- 1 utilisateur utilisateur 2.0M nov. 14 15:45 photo.jpg
-rw-r--r-- 1 utilisateur utilisateur  15K nov. 13 09:22 document.pdf
```

#### Combiner les options

Vous pouvez combiner plusieurs options :

```bash
ls -lah
```

Cette commande affiche **tous** les fichiers (cachés inclus), en format **long**, avec des tailles **lisibles**.

### Lister le contenu d'un autre dossier

Vous pouvez lister un dossier sans y aller :

```bash
ls Documents
```

Ou avec un chemin complet :

```bash
ls /home/utilisateur/Documents
```

### Options utiles supplémentaires

```bash
ls -lt     # Trier par date de modification (le plus récent en premier)  
ls -lS     # Trier par taille (le plus gros en premier)  
ls -lr     # Ordre inversé  
ls -R      # Récursif (affiche aussi les sous-dossiers)  
```

### Filtrer avec des motifs

Vous pouvez utiliser des caractères joker :

```bash
ls *.txt          # Tous les fichiers .txt  
ls Documents/*.pdf # Tous les PDF dans Documents  
ls photo*         # Tous les fichiers commençant par "photo"  
```

---

## La commande `cd` : Se déplacer

### Signification

**cd** signifie **Change Directory** (Changer de répertoire).

### Utilisation de base

```bash
cd chemin_du_dossier
```

### Exemples pratiques

#### Aller dans un sous-dossier (chemin relatif)

```bash
cd Documents
```

Si vous êtes dans `/home/utilisateur`, vous allez dans `/home/utilisateur/Documents`.

#### Aller dans un dossier avec chemin absolu

```bash
cd /home/utilisateur/Images
```

Peu importe où vous êtes, cette commande vous amène directement dans le dossier Images.

#### Retourner au dossier personnel

Plusieurs façons de faire :

```bash
cd          # Sans argument, retourne au dossier personnel  
cd ~        # Équivalent  
cd $HOME    # Également équivalent  
```

#### Remonter d'un niveau (dossier parent)

```bash
cd ..
```

Si vous êtes dans `/home/utilisateur/Documents`, vous allez dans `/home/utilisateur`.

#### Remonter de plusieurs niveaux

```bash
cd ../..    # Remonte de 2 niveaux  
cd ../../.. # Remonte de 3 niveaux  
```

#### Retourner au dossier précédent

```bash
cd -
```

Cette commande très pratique vous ramène au dernier dossier où vous étiez.

**Exemple d'utilisation :**
```bash
utilisateur@ordinateur:~$ cd /var/log  
utilisateur@ordinateur:/var/log$ cd -  
/home/utilisateur
utilisateur@ordinateur:~$ cd -
/var/log
```

#### Naviguer vers des chemins avec espaces

Si un dossier contient des espaces, utilisez des guillemets ou un antislash :

```bash
cd "Mes Documents"
# ou
cd Mes\ Documents
```

**Astuce :** Utilisez la touche **Tab** pour compléter automatiquement, elle gérera les espaces pour vous !

### Combinaisons utiles

#### Aller dans un sous-dossier d'un dossier parent

```bash
cd ../Images    # Remonte d'un niveau puis va dans Images
```

#### Naviguer efficacement

```bash
cd ~/Documents/Travail/Projets/2024
```

Vous pouvez enchaîner plusieurs niveaux directement.

### Erreurs courantes

#### Dossier inexistant

```bash
utilisateur@ordinateur:~$ cd Documants  
bash: cd: Documants: Aucun fichier ou dossier de ce type  
```

**Solution :** Vérifiez l'orthographe, utilisez la complétion avec **Tab**.

#### Permission refusée

```bash
utilisateur@ordinateur:~$ cd /root  
bash: cd: /root: Permission non accordée  
```

**Explication :** Certains dossiers sont protégés et nécessitent des privilèges administrateur.

---

## La commande `tree` : Vue d'ensemble

### Signification

**tree** affiche l'arborescence des fichiers et dossiers de manière visuelle, sous forme d'arbre.

### Installation (si nécessaire)

La commande `tree` n'est pas toujours installée par défaut. Pour l'installer :

```bash
sudo apt update  
sudo apt install tree  
```

### Utilisation de base

```bash
tree
```

Affiche l'arborescence complète du dossier actuel.

### Exemple de résultat

```bash
utilisateur@ordinateur:~/Documents$ tree
.
├── Projets
│   ├── projet1
│   │   ├── notes.txt
│   │   └── code.py
│   └── projet2
│       └── readme.md
├── Rapports
│   ├── rapport_janvier.pdf
│   └── rapport_fevrier.pdf
└── notes_personnelles.txt

4 directories, 5 files
```

### Options utiles

#### Limiter la profondeur

```bash
tree -L 2
```

Affiche seulement 2 niveaux de profondeur.

#### Afficher uniquement les dossiers

```bash
tree -d
```

Ignore les fichiers, montre seulement la structure des dossiers.

#### Afficher les fichiers cachés

```bash
tree -a
```

Inclut les fichiers qui commencent par un point.

#### Afficher les tailles

```bash
tree -h
```

Affiche la taille des fichiers de manière lisible.

#### Trier par date de modification

```bash
tree -D
```

Affiche la date de dernière modification de chaque fichier.

#### Exporter vers un fichier

```bash
tree > structure.txt
```

Sauvegarde l'arborescence dans un fichier texte.

### Exemples pratiques combinés

#### Vue complète avec tailles et dates

```bash
tree -aDh -L 3
```

- `-a` : Fichiers cachés
- `-D` : Dates
- `-h` : Tailles lisibles
- `-L 3` : Maximum 3 niveaux

#### Voir la structure d'un autre dossier

```bash
tree ~/Documents  
tree /etc -L 1  
```

### Filtrer par type de fichier

```bash
tree -P "*.txt"    # Seulement les fichiers .txt  
tree -P "*.py"     # Seulement les fichiers Python  
tree -I "*.log"    # Exclure les fichiers .log  
```

---

## Techniques de navigation efficace

### 1. Utiliser la complétion automatique (Tab)

Au lieu de taper complètement :
```bash
cd Documents/Projets/mon_super_projet_2024/
```

Tapez :
```bash
cd Doc[Tab]/Pro[Tab]/mon[Tab]
```

Le terminal complète automatiquement à chaque fois !

### 2. Combiner les commandes

Vous pouvez enchaîner les commandes avec **&&** :

```bash
cd Documents && ls
```

Cela change de dossier PUIS liste le contenu.

### 3. Naviguer et vérifier

```bash
cd /etc && pwd && ls -l
```

Change de dossier, affiche où vous êtes, puis liste le contenu.

### 4. Créer des alias pour les dossiers fréquents

Dans votre fichier `~/.bashrc`, vous pouvez ajouter :

```bash
alias docs='cd ~/Documents'  
alias dl='cd ~/Téléchargements'  
alias proj='cd ~/Documents/Projets'  
```

Après avoir rechargé la configuration (`source ~/.bashrc`), vous pouvez taper simplement :
```bash
docs    # Vous amène dans Documents
```

---

## Navigation avancée : Astuces

### Historique de navigation

Bash garde en mémoire les dossiers que vous avez visités. Vous pouvez utiliser :

```bash
cd -    # Retour au dossier précédent
```

Ou créer un système plus sophistiqué avec `pushd` et `popd` (nous verrons cela dans un chapitre avancé).

### Rechercher un fichier et y naviguer

Vous pouvez combiner `find` avec `cd` :

```bash
find ~ -name "mon_fichier.txt" -type f
```

Une fois trouvé, copiez le chemin et utilisez :
```bash
cd /chemin/vers/le/dossier
```

### Utiliser les marque-pages (bookmarks)

Certains shells modernes permettent de créer des marque-pages pour vos dossiers favoris. Avec `bash`, vous pouvez utiliser la variable `CDPATH` :

```bash
export CDPATH=.:~:~/Documents:~/Projets
```

Maintenant, vous pouvez taper `cd nom_dossier` et bash cherchera dans tous ces emplacements.

---

## Comparaison récapitulative

| Commande | Action | Équivalent graphique |
|----------|--------|---------------------|
| `pwd` | Afficher où je suis | Regarder la barre d'adresse |
| `ls` | Lister le contenu | Ouvrir un dossier |
| `ls -la` | Tout lister en détail | Vue détaillée + fichiers cachés |
| `cd dossier` | Aller dans un dossier | Double-clic sur un dossier |
| `cd ..` | Remonter d'un niveau | Bouton "Précédent" ou "Parent" |
| `cd ~` | Retour à l'accueil | Clic sur "Dossier personnel" |
| `tree` | Voir l'arborescence | Vue arborescente dans le gestionnaire |

---

## Exemples de navigation typiques

### Scénario 1 : Trouver et ouvrir un document

```bash
cd ~                    # Retour au dossier personnel  
ls                      # Que contient mon dossier ?  
cd Documents            # J'entre dans Documents  
ls -lt                  # Je liste par date (le plus récent en premier)  
```

### Scénario 2 : Explorer un projet

```bash
cd ~/Documents/Projets/MonSite  
tree -L 2               # Je vois la structure sur 2 niveaux  
cd css                  # J'entre dans le dossier CSS  
ls -lh                  # Je regarde les fichiers CSS avec leurs tailles  
cd ..                   # Je remonte  
cd js                   # Je vais dans le dossier JavaScript  
```

### Scénario 3 : Nettoyer les téléchargements

```bash
cd ~/Téléchargements    # J'y vais  
ls -lt                  # Je trie par date  
ls *.pdf                # Je regarde les PDF  
ls *.deb                # Je regarde les paquets  
```

### Scénario 4 : Vérifier la configuration système

```bash
cd /etc                 # Configuration système  
ls -l                   # Je liste  
tree -L 1 -d            # Structure des sous-dossiers (1 niveau)  
cd network              # Configuration réseau  
pwd                     # Je vérifie où je suis  
```

---

## Erreurs fréquentes et solutions

### Erreur 1 : "Aucun fichier ou dossier de ce type"

**Problème :**
```bash
cd Documments  
bash: cd: Documments: Aucun fichier ou dossier de ce type  
```

**Solutions :**
- Vérifiez l'orthographe (faute de frappe ici : "Documments")
- Utilisez la complétion avec **Tab**
- Faites `ls` pour voir les dossiers disponibles
- Linux est sensible à la casse : `documents` ≠ `Documents`

### Erreur 2 : Permission refusée

**Problème :**
```bash
cd /root  
bash: cd: /root: Permission non accordée  
```

**Solutions :**
- Certains dossiers nécessitent les droits administrateur
- Utilisez `sudo -i` pour devenir root (avec précaution !)
- Demandez-vous si vous avez vraiment besoin d'accéder à ce dossier

### Erreur 3 : Trop de résultats avec `ls`

**Problème :**
Le dossier contient des centaines de fichiers, l'affichage défile trop vite.

**Solutions :**
```bash
ls | less           # Affichage paginé (q pour quitter)  
ls | head           # Voir seulement les 10 premiers  
ls | tail           # Voir seulement les 10 derniers  
ls | grep "mot"     # Filtrer par mot-clé  
```

### Erreur 4 : Perdu dans l'arborescence

**Solutions :**
```bash
pwd                 # Où suis-je ?  
cd ~                # Retour à la maison  
cd -                # Retour au dossier précédent  
tree -L 1           # Vue rapide de la structure  
```

---

## Bonnes pratiques

### 1. Vérifiez toujours où vous êtes

Avant d'exécuter des commandes importantes, faites un `pwd` pour être sûr de votre position.

### 2. Listez avant d'agir

Faites `ls` pour voir ce qui existe avant de supprimer, déplacer ou modifier des fichiers.

### 3. Utilisez des chemins absolus pour les scripts

Dans les scripts, préférez les chemins absolus pour éviter les erreurs :
```bash
cd /home/utilisateur/Documents/Projets
```

Au lieu de :
```bash
cd ../../Documents/Projets
```

### 4. Organisez votre structure

Créez une structure logique de dossiers :
```
~/Documents/
  ├── Travail/
  ├── Personnel/
  ├── Projets/
  └── Archives/
```

Cela facilite la navigation et la recherche.

### 5. Prenez des notes

Gardez un pense-bête avec les chemins que vous utilisez souvent.

---

## Commandes complémentaires

Voici quelques commandes qui complètent la navigation :

### `file` : Identifier un type de fichier

```bash
file document.pdf
# document.pdf: PDF document, version 1.4
```

### `du` : Voir la taille d'un dossier

```bash
du -sh Documents
# 2.5G    Documents
```

### `find` : Rechercher des fichiers

```bash
find ~ -name "*.txt"    # Trouve tous les .txt dans votre dossier personnel
```

### `locate` : Recherche rapide

```bash
locate mon_fichier.txt  # Recherche rapide dans une base de données
```

---

## Résumé

Les commandes de navigation sont votre boussole dans le système Linux :

| Commande | Utilisation principale | Conseil |
|----------|----------------------|---------|
| **pwd** | Savoir où vous êtes | Utilisez avant des opérations importantes |
| **ls** | Voir ce qu'il y a | Ajoutez `-lah` pour tout voir en détail |
| **cd** | Se déplacer | Utilisez Tab pour compléter les chemins |
| **tree** | Vue d'ensemble | Limitez avec `-L 2` pour plus de clarté |

### Raccourcis essentiels à retenir

- `cd ~` ou `cd` → Dossier personnel
- `cd ..` → Dossier parent
- `cd -` → Dossier précédent
- `ls -lah` → Liste complète et détaillée
- `pwd` → Où suis-je ?

### Workflow typique

```bash
pwd         # Je vérifie où je suis  
ls -la      # Je regarde ce qu'il y a  
cd dossier  # Je me déplace  
tree -L 2   # Je visualise la structure  
```

Avec ces quatre commandes, vous pouvez explorer l'intégralité de votre système Linux de manière efficace. La pratique régulière les rendra bientôt aussi naturelles que de cliquer sur des dossiers !

Dans le prochain chapitre, nous verrons comment manipuler des fichiers (copier, déplacer, supprimer) pour aller au-delà de la simple navigation.

⏭️ [Manipulation de fichiers (cp, mv, rm, mkdir, touch)](/07-le-terminal-et-commandes-de-base/03-manipulation-de-fichiers.md)
