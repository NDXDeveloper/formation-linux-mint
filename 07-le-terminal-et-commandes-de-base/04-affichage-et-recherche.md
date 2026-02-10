🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.4 - Affichage et recherche (cat, less, head, tail, grep, find)

## Introduction

Vous savez maintenant naviguer dans votre système et manipuler des fichiers. Il est temps d'apprendre à **lire le contenu** des fichiers et à **rechercher** des informations spécifiques dans votre système.

**Analogie :** Si votre système de fichiers est une bibliothèque :
- **cat, less, head, tail** sont comme ouvrir un livre et le lire
- **grep** est comme chercher un mot spécifique dans les pages d'un livre
- **find** est comme chercher un livre dans toute la bibliothèque

Ces commandes sont essentielles pour :
- Consulter des fichiers de configuration
- Analyser des fichiers de log (journaux système)
- Rechercher des informations dans vos documents
- Localiser des fichiers perdus
- Filtrer et extraire des données

**Note importante :** Ces commandes permettent de **lire** les fichiers, pas de les modifier. C'est donc parfaitement sûr pour explorer votre système sans risque.

---

## La commande `cat` : Afficher le contenu complet

### Signification

**cat** signifie **Concatenate** (Concaténer), mais elle est principalement utilisée pour afficher des fichiers.

### Utilisation de base

```bash
cat nom_fichier
```

Affiche tout le contenu du fichier directement dans le terminal.

### Exemples simples

#### Afficher un fichier texte

```bash
cat notes.txt
```

Le contenu apparaît directement dans le terminal.

#### Afficher plusieurs fichiers à la suite

```bash
cat fichier1.txt fichier2.txt fichier3.txt
```

Affiche les trois fichiers l'un après l'autre, sans interruption.

### Quand utiliser `cat` ?

**Idéal pour :**
- Fichiers courts (quelques lignes)
- Vérifier rapidement le contenu
- Combiner avec d'autres commandes (pipes)

**Pas adapté pour :**
- Fichiers longs (le texte défile trop vite)
- Fichiers binaires (images, vidéos, exécutables)

**Exemple avec un fichier trop long :**
```bash
cat /var/log/syslog
# Le texte défile à toute vitesse, illisible !
```

**Solution :** Utilisez `less` pour les fichiers longs (voir plus bas).

### Options utiles

#### `-n` : Numéroter les lignes

```bash
cat -n fichier.txt
```

**Résultat :**
```
     1  Première ligne
     2  Deuxième ligne
     3  Troisième ligne
```

Très utile pour référencer des lignes spécifiques.

#### `-b` : Numéroter seulement les lignes non vides

```bash
cat -b fichier.txt
```

#### `-A` : Afficher tous les caractères (y compris invisibles)

```bash
cat -A fichier.txt
```

Affiche :
- `$` à la fin de chaque ligne
- `^I` pour les tabulations
- Autres caractères spéciaux

Utile pour déboguer des problèmes de formatage.

### Usages avancés

#### Créer un fichier simple

```bash
cat > nouveau_fichier.txt
```

Tapez votre texte, puis appuyez sur **Ctrl+D** pour sauvegarder.

**Note :** Cela écrase le fichier s'il existe déjà !

#### Ajouter du contenu à un fichier

```bash
cat >> fichier_existant.txt
```

Le `>>` ajoute à la fin au lieu d'écraser.

#### Concaténer plusieurs fichiers en un seul

```bash
cat partie1.txt partie2.txt partie3.txt > complet.txt
```

Combine les trois fichiers en un seul.

---

## La commande `less` : Naviguer dans les fichiers

### Signification

**less** est un paginateur qui permet de lire des fichiers longs page par page.

**Histoire amusante :** `less` est l'opposé de `more` (une commande plus ancienne). Le jeu de mots : "less is more" !

### Utilisation de base

```bash
less nom_fichier
```

Le fichier s'ouvre dans une interface de lecture.

### Navigation dans `less`

Une fois dans `less`, utilisez ces touches :

#### Défilement

| Touche | Action |
|--------|--------|
| **Espace** ou **Page Down** | Page suivante |
| **b** ou **Page Up** | Page précédente |
| **Flèche bas ↓** | Ligne suivante |
| **Flèche haut ↑** | Ligne précédente |
| **g** | Aller au début du fichier |
| **G** (majuscule) | Aller à la fin du fichier |
| **50g** | Aller à la ligne 50 |

#### Recherche

| Touche | Action |
|--------|--------|
| **/mot** | Rechercher "mot" vers le bas |
| **?mot** | Rechercher "mot" vers le haut |
| **n** | Occurrence suivante |
| **N** (majuscule) | Occurrence précédente |

**Exemple :**
1. Tapez `/erreur` puis **Entrée**
2. `less` surligne le mot "erreur"
3. Appuyez sur **n** pour aller à l'occurrence suivante

#### Autres commandes utiles

| Touche | Action |
|--------|--------|
| **q** | Quitter `less` |
| **h** | Afficher l'aide |
| **F** | Mode suivi (comme `tail -f`) |
| **v** | Éditer le fichier (ouvre l'éditeur) |

### Exemples pratiques

#### Lire un fichier log système

```bash
less /var/log/syslog
```

Naviguez tranquillement avec **Espace** et **b**.

#### Lire avec numéros de ligne

```bash
less -N fichier.txt
```

L'option `-N` affiche les numéros de ligne.

#### Lire plusieurs fichiers

```bash
less fichier1.txt fichier2.txt
```

Utilisez **:n** (fichier suivant) et **:p** (fichier précédent) dans `less`.

### Pourquoi utiliser `less` plutôt que `cat` ?

**`less` est préférable pour :**
- Fichiers longs (logs, documentation)
- Rechercher des informations spécifiques
- Explorer sans charger tout le fichier en mémoire

**`cat` est préférable pour :**
- Fichiers courts (quelques lignes)
- Affichage rapide
- Combiner avec d'autres commandes (pipes)

---

## La commande `head` : Afficher le début d'un fichier

### Signification

**head** affiche les premières lignes d'un fichier (la "tête").

### Utilisation de base

```bash
head nom_fichier
```

Par défaut, affiche les **10 premières lignes**.

### Exemples

#### Voir le début d'un fichier

```bash
head rapport.txt
```

Affiche les 10 premières lignes de "rapport.txt".

#### Spécifier le nombre de lignes

```bash
head -n 5 fichier.txt
```

Affiche les 5 premières lignes.

**Forme courte :**
```bash
head -5 fichier.txt
```

#### Afficher les premiers octets

```bash
head -c 100 fichier.txt
```

Affiche les 100 premiers caractères (octets).

### Usages pratiques

#### Vérifier le format d'un fichier CSV

```bash
head -3 donnees.csv
```

Affiche les en-têtes et les premières lignes de données.

#### Voir le début de plusieurs fichiers

```bash
head fichier1.txt fichier2.txt
```

Affiche le début de chaque fichier avec un en-tête indiquant le nom.

#### Extraire l'en-tête d'un fichier de configuration

```bash
head -20 /etc/apache2/apache2.conf
```

Souvent, les commentaires et explications sont au début des fichiers de config.

---

## La commande `tail` : Afficher la fin d'un fichier

### Signification

**tail** affiche les dernières lignes d'un fichier (la "queue").

### Utilisation de base

```bash
tail nom_fichier
```

Par défaut, affiche les **10 dernières lignes**.

### Exemples

#### Voir la fin d'un fichier

```bash
tail rapport.txt
```

#### Spécifier le nombre de lignes

```bash
tail -n 20 fichier.txt
```

Affiche les 20 dernières lignes.

**Forme courte :**
```bash
tail -20 fichier.txt
```

#### Afficher à partir d'une ligne spécifique

```bash
tail -n +50 fichier.txt
```

Affiche à partir de la ligne 50 jusqu'à la fin.

### L'option `-f` : Suivre en temps réel (très utile !)

```bash
tail -f /var/log/syslog
```

**Le mode "follow" :**
- Affiche les dernières lignes
- Reste ouvert et affiche les nouvelles lignes en temps réel
- Parfait pour surveiller les logs

**Pour quitter :** Appuyez sur **Ctrl+C**

#### Variante améliorée : `-F`

```bash
tail -F /var/log/syslog
```

L'option `-F` (majuscule) continue à suivre même si le fichier est recréé ou renommé.

### Usages pratiques

#### Surveiller les logs système

```bash
tail -f /var/log/syslog
```

Vous voyez les événements système en direct.

#### Suivre plusieurs fichiers

```bash
tail -f /var/log/syslog /var/log/auth.log
```

Affiche les nouvelles lignes des deux fichiers.

#### Voir les dernières lignes de plusieurs fichiers

```bash
tail *.log
```

Affiche la fin de tous les fichiers .log du dossier actuel.

#### Combiner avec grep (filtrer)

```bash
tail -f /var/log/syslog | grep error
```

Affiche uniquement les lignes contenant "error" en temps réel.

---

## Combiner `head` et `tail` : Extraire des lignes spécifiques

### Afficher les lignes 20 à 30

```bash
head -30 fichier.txt | tail -10
```

**Explication :**
1. `head -30` : Les 30 premières lignes
2. `tail -10` : Les 10 dernières de ces 30 (donc lignes 21-30)

### Afficher une ligne spécifique

```bash
head -42 fichier.txt | tail -1
```

Affiche uniquement la ligne 42.

### Voir le milieu d'un fichier

```bash
head -100 fichier.txt | tail -20
```

Affiche les lignes 81 à 100.

---

## La commande `grep` : Rechercher du texte

### Signification

**grep** signifie **Global Regular Expression Print** (Affichage d'expression régulière globale).

C'est l'un des outils les plus puissants pour rechercher du texte !

### Utilisation de base

```bash
grep "mot_recherché" fichier.txt
```

Affiche toutes les lignes contenant "mot_recherché".

### Exemples simples

#### Rechercher un mot dans un fichier

```bash
grep "erreur" logs.txt
```

Affiche toutes les lignes contenant le mot "erreur".

#### Rechercher dans plusieurs fichiers

```bash
grep "TODO" *.txt
```

Cherche "TODO" dans tous les fichiers .txt du dossier actuel.

### Options essentielles

#### `-i` : Ignorer la casse (majuscules/minuscules)

```bash
grep -i "erreur" logs.txt
```

Trouve : "erreur", "Erreur", "ERREUR", "ErReUr", etc.

#### `-n` : Afficher les numéros de ligne

```bash
grep -n "erreur" logs.txt
```

**Résultat :**
```
15:Une erreur s'est produite
42:Erreur de connexion
```

#### `-v` : Inverser (lignes qui NE contiennent PAS le motif)

```bash
grep -v "commentaire" config.txt
```

Affiche toutes les lignes sauf celles contenant "commentaire".

Utile pour filtrer les commentaires :
```bash
grep -v "^#" /etc/ssh/sshd_config
```

Le `^#` signifie : lignes commençant par `#`.

#### `-r` ou `-R` : Recherche récursive (dans les sous-dossiers)

```bash
grep -r "fonction_test" ~/Projets/
```

Cherche dans tous les fichiers du dossier Projets et ses sous-dossiers.

#### `-l` : Afficher seulement les noms de fichiers

```bash
grep -l "erreur" *.log
```

Affiche uniquement les noms des fichiers contenant "erreur", pas les lignes.

#### `-c` : Compter les occurrences

```bash
grep -c "erreur" logs.txt
```

Affiche le nombre de lignes contenant "erreur".

#### `-w` : Mot entier seulement

```bash
grep -w "test" fichier.txt
```

Trouve "test" mais pas "testing" ou "contest".

#### `-A` et `-B` : Contexte après et avant

```bash
grep -A 3 "erreur" logs.txt    # 3 lignes après  
grep -B 2 "erreur" logs.txt    # 2 lignes avant  
grep -C 2 "erreur" logs.txt    # 2 lignes avant ET après  
```

**Très utile pour comprendre le contexte d'une erreur !**

### Combiner plusieurs options

```bash
grep -rni "erreur" /var/log/
```

- `-r` : Récursif
- `-n` : Numéros de ligne
- `-i` : Ignorer la casse

### Recherche avec expressions régulières (regex)

#### Rechercher un motif

```bash
grep "^Erreur" fichier.txt    # Lignes commençant par "Erreur"  
grep "fin$" fichier.txt       # Lignes se terminant par "fin"  
grep "err.*" fichier.txt      # Lignes contenant "err" suivi de n'importe quoi  
```

#### Rechercher plusieurs mots

```bash
grep -E "erreur|avertissement|critique" logs.txt
```

L'option `-E` active les expressions régulières étendues.

Le `|` signifie "OU".

### Exemples pratiques

#### Trouver une adresse IP dans les logs

```bash
grep -E "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" logs.txt
```

#### Trouver les lignes vides

```bash
grep "^$" fichier.txt
```

#### Trouver les lignes non vides

```bash
grep -v "^$" fichier.txt
```

#### Rechercher dans les fichiers de configuration

```bash
grep -v "^#" /etc/ssh/sshd_config | grep -v "^$"
```

Affiche la config SSH sans commentaires ni lignes vides.

### Combiner `grep` avec d'autres commandes

#### Filtrer la sortie de `ls`

```bash
ls -l | grep "\.txt$"
```

Liste seulement les fichiers .txt.

#### Rechercher un processus

```bash
ps aux | grep firefox
```

Affiche les processus Firefox en cours.

#### Compter les fichiers d'un type

```bash
ls | grep "\.jpg$" | wc -l
```

Compte le nombre de fichiers .jpg.

---

## La commande `find` : Rechercher des fichiers et dossiers

### Signification

**find** recherche des fichiers et dossiers selon divers critères (nom, taille, date, etc.).

### Utilisation de base

```bash
find chemin -name "nom_fichier"
```

### Exemples de recherche par nom

#### Trouver un fichier par son nom exact

```bash
find ~ -name "rapport.txt"
```

Cherche "rapport.txt" dans votre dossier personnel.

#### Recherche insensible à la casse

```bash
find ~ -iname "rapport.txt"
```

Trouve : "rapport.txt", "Rapport.txt", "RAPPORT.TXT", etc.

#### Utiliser des jokers

```bash
find ~ -name "*.pdf"          # Tous les PDF  
find ~ -name "photo*"         # Fichiers commençant par "photo"  
find ~ -name "*2024*"         # Fichiers contenant "2024"  
```

**Important :** Mettez les jokers entre guillemets pour éviter que le shell ne les interprète !

### Rechercher par type

#### Fichiers seulement

```bash
find ~ -type f -name "*.txt"
```

#### Dossiers seulement

```bash
find ~ -type d -name "Projets"
```

#### Liens symboliques

```bash
find ~ -type l
```

### Rechercher par taille

```bash
find ~ -size +100M        # Fichiers > 100 Mo  
find ~ -size -1M          # Fichiers < 1 Mo  
find ~ -size 50k          # Fichiers = 50 Ko (environ)  
```

**Unités :**
- `c` : octets (bytes)
- `k` : kilo-octets
- `M` : méga-octets
- `G` : giga-octets

### Rechercher par date de modification

```bash
find ~ -mtime -7          # Modifiés dans les 7 derniers jours  
find ~ -mtime +30         # Modifiés il y a plus de 30 jours  
find ~ -mtime 0           # Modifiés aujourd'hui  
```

**Autres options temporelles :**
- `-atime` : Date d'accès
- `-ctime` : Date de changement de métadonnées
- `-mmin` : Modification en minutes

```bash
find ~ -mmin -60          # Modifiés dans les 60 dernières minutes
```

### Rechercher par permissions

```bash
find ~ -perm 777          # Permissions exactes 777  
find ~ -perm -644         # Au moins les permissions 644  
```

### Rechercher par propriétaire

```bash
find /home -user utilisateur     # Appartenant à "utilisateur"  
find /var -group www-data        # Appartenant au groupe "www-data"  
```

### Limiter la profondeur de recherche

```bash
find ~ -maxdepth 2 -name "*.txt"
```

Cherche seulement dans le dossier et ses sous-dossiers directs (2 niveaux max).

```bash
find ~ -mindepth 2 -name "*.txt"
```

Ignore le dossier courant, commence la recherche au niveau 2.

### Combiner plusieurs critères

#### ET logique (par défaut)

```bash
find ~ -type f -name "*.log" -size +10M
```

Fichiers .log ET plus de 10 Mo.

#### OU logique

```bash
find ~ -name "*.jpg" -o -name "*.png"
```

Fichiers .jpg OU .png.

#### Négation

```bash
find ~ -type f -not -name "*.txt"
```

Tous les fichiers SAUF les .txt.

### Exécuter des commandes sur les résultats

#### `-exec` : Exécuter une commande

```bash
find ~ -name "*.tmp" -exec rm {} \;
```

Supprime tous les fichiers .tmp.

**Syntaxe :**
- `{}` : Remplacé par chaque fichier trouvé
- `\;` : Marque la fin de la commande

#### `-exec` avec confirmation

```bash
find ~ -name "*.tmp" -exec rm -i {} \;
```

Demande confirmation avant chaque suppression.

#### Alternative : `-ok` (demande toujours confirmation)

```bash
find ~ -name "*.tmp" -ok rm {} \;
```

#### Exemples pratiques avec `-exec`

**Copier tous les PDF dans un dossier :**
```bash
find ~ -name "*.pdf" -exec cp {} ~/Documents/PDFs/ \;
```

**Changer les permissions :**
```bash
find ~ -name "*.sh" -exec chmod +x {} \;
```

Rend tous les fichiers .sh exécutables.

**Afficher la taille :**
```bash
find ~ -name "*.mp4" -exec ls -lh {} \;
```

### Utiliser `-delete` (attention !)

```bash
find ~ -name "*.tmp" -delete
```

**⚠️ ATTENTION :** Pas de confirmation ! Testez d'abord sans `-delete` :

```bash
find ~ -name "*.tmp"           # Voir ce qui sera supprimé  
find ~ -name "*.tmp" -delete   # Puis supprimer  
```

### Exemples pratiques courants

#### Trouver les gros fichiers

```bash
find ~ -type f -size +500M -exec ls -lh {} \; | sort -k5 -h
```

#### Trouver les fichiers récents

```bash
find ~ -type f -mtime -1
```

Fichiers modifiés dans les dernières 24 heures.

#### Nettoyer les fichiers temporaires

```bash
find /tmp -type f -mtime +7 -delete
```

Supprime les fichiers dans /tmp de plus de 7 jours.

#### Trouver les dossiers vides

```bash
find ~ -type d -empty
```

#### Trouver et compresser

```bash
find ~/Documents -name "*.txt" -exec gzip {} \;
```

Compresse tous les fichiers .txt.

#### Rechercher dans les fichiers système

```bash
sudo find /etc -name "*.conf"
```

Trouve tous les fichiers de configuration.

---

## Combiner les commandes : Exemples puissants

### Trouver et afficher

```bash
find ~ -name "*.log" -exec head -5 {} \;
```

Affiche les 5 premières lignes de chaque fichier .log.

### Trouver et rechercher dedans

```bash
find ~/Documents -name "*.txt" -exec grep -l "mot_clé" {} \;
```

Liste les fichiers .txt contenant "mot_clé".

**Alternative plus simple :**
```bash
grep -r "mot_clé" ~/Documents/*.txt
```

### Pipeline avec `xargs` (plus efficace)

```bash
find ~ -name "*.txt" | xargs grep "erreur"
```

`xargs` passe les résultats de `find` à `grep` plus efficacement que `-exec`.

### Rechercher et compter

```bash
find ~ -name "*.jpg" | wc -l
```

Compte le nombre de fichiers .jpg.

---

## Comparaison des commandes de recherche

| Commande | Recherche quoi ? | Vitesse | Flexibilité |
|----------|------------------|---------|-------------|
| `grep` | Contenu de fichiers | Rapide | Très flexible (regex) |
| `find` | Fichiers/dossiers | Moyenne | Très flexible (critères) |
| `locate` | Noms de fichiers | Très rapide | Limitée (base de données) |

### La commande `locate` (bonus)

```bash
locate nom_fichier
```

Recherche ultra-rapide dans une base de données pré-indexée.

**Installation (si nécessaire) :**
```bash
sudo apt install mlocate  
sudo updatedb    # Mettre à jour la base de données  
```

**Avantages :** Extrêmement rapide  
**Inconvénients :** Base de données pas toujours à jour  

---

## Astuces et bonnes pratiques

### 1. Tester avant d'agir

Avant d'utiliser `find` avec `-delete` ou `-exec rm` :

```bash
find ~ -name "*.tmp"                    # Vérifier ce qui sera affecté  
find ~ -name "*.tmp" | wc -l            # Compter  
find ~ -name "*.tmp" -delete            # Puis supprimer  
```

### 2. Sauvegarder les résultats

```bash
find ~ -name "*.pdf" > liste_pdf.txt
```

Sauvegarde la liste dans un fichier.

### 3. Utiliser `-print0` et `xargs -0` pour les noms avec espaces

```bash
find ~ -name "*.txt" -print0 | xargs -0 grep "mot"
```

Gère correctement les fichiers avec espaces dans le nom.

### 4. Limiter les résultats de `grep`

```bash
grep -m 5 "erreur" fichier.log
```

S'arrête après 5 correspondances.

### 5. Colorer les résultats de `grep`

```bash
grep --color=auto "erreur" fichier.log
```

Le mot recherché apparaît en couleur.

**Alias permanent (dans ~/.bashrc) :**
```bash
alias grep='grep --color=auto'
```

---

## Erreurs courantes et solutions

### Erreur 1 : `grep` ne trouve rien

**Problème :**
```bash
grep "Erreur" fichier.txt
# (rien ne s'affiche)
```

**Solutions :**
- Vérifiez la casse : `grep -i "erreur" fichier.txt`
- Vérifiez que le mot est bien dans le fichier : `cat fichier.txt`
- Essayez sans guillemets : `grep erreur fichier.txt`

### Erreur 2 : `find` trop lent

**Problème :** La recherche prend trop de temps.

**Solutions :**
- Limitez la profondeur : `find ~ -maxdepth 3 -name "fichier"`
- Restreignez le chemin de recherche : `find ~/Documents` au lieu de `find ~`
- Utilisez `locate` pour les recherches simples

### Erreur 3 : Permission refusée avec `find`

**Problème :**
```bash
find / -name "config"
# find: '/root': Permission non accordée
# find: '/var/log': Permission non accordée
```

**Solutions :**
```bash
find / -name "config" 2>/dev/null    # Masque les erreurs  
sudo find / -name "config"           # Avec droits admin  
```

### Erreur 4 : `cat` avec un fichier binaire

**Problème :** Terminal illisible après `cat image.jpg`

**Solution :**
```bash
reset    # Réinitialise le terminal
```

**Prévention :** Utilisez `file` pour vérifier le type :
```bash
file image.jpg    # image.jpg: JPEG image data
```

---

## Récapitulatif des commandes

### Affichage

| Commande | Usage | Quand l'utiliser |
|----------|-------|------------------|
| `cat fichier` | Afficher tout | Fichiers courts |
| `less fichier` | Lecture paginée | Fichiers longs |
| `head fichier` | Début du fichier | Voir les premières lignes |
| `head -n 5 fichier` | 5 premières lignes | Personnaliser |
| `tail fichier` | Fin du fichier | Voir les dernières lignes |
| `tail -f fichier` | Suivi en temps réel | Surveiller les logs |

### Recherche de contenu

| Commande | Usage | Exemple |
|----------|-------|---------|
| `grep "mot" fichier` | Chercher dans fichier | `grep "erreur" log.txt` |
| `grep -r "mot" dir/` | Chercher récursivement | `grep -r "TODO" ~/Projets` |
| `grep -i "mot" fichier` | Ignorer la casse | `grep -i "error" log.txt` |
| `grep -n "mot" fichier` | Avec numéros de ligne | `grep -n "function" code.py` |

### Recherche de fichiers

| Commande | Usage | Exemple |
|----------|-------|---------|
| `find ~ -name "fichier"` | Par nom | `find ~ -name "*.pdf"` |
| `find ~ -type f` | Fichiers seulement | `find ~ -type f -name "*.txt"` |
| `find ~ -size +100M` | Par taille | `find ~ -size +1G` |
| `find ~ -mtime -7` | Par date | `find ~ -mtime -1` |

---

## Exemples de workflows complets

### Workflow 1 : Analyser des logs

```bash
# Voir les dernières erreurs
tail -100 /var/log/syslog | grep -i error

# Suivre en temps réel
tail -f /var/log/syslog | grep --color -i "error\|warning"

# Compter les erreurs
grep -c "error" /var/log/syslog
```

### Workflow 2 : Nettoyer les fichiers temporaires

```bash
# Voir ce qui sera supprimé
find ~/Téléchargements -name "*.tmp" -o -name "*.temp"

# Compter
find ~/Téléchargements -name "*.tmp" -o -name "*.temp" | wc -l

# Supprimer
find ~/Téléchargements \( -name "*.tmp" -o -name "*.temp" \) -delete
```

### Workflow 3 : Trouver des informations dans les projets

```bash
# Trouver tous les fichiers Python
find ~/Projets -name "*.py"

# Chercher une fonction spécifique
grep -rn "def ma_fonction" ~/Projets

# Lister les fichiers la contenant
grep -rl "def ma_fonction" ~/Projets
```

### Workflow 4 : Surveillance système

```bash
# Processus consommant de la mémoire
ps aux | grep -v grep | head -20

# Fichiers logs récents
find /var/log -type f -mtime -1

# Erreurs récentes
journalctl -p err -S today
```

---

## Commandes bonus complémentaires

### `wc` : Compter lignes, mots, caractères

```bash
wc fichier.txt           # Lignes, mots, caractères  
wc -l fichier.txt        # Nombre de lignes seulement  
wc -w fichier.txt        # Nombre de mots  
wc -c fichier.txt        # Nombre de caractères  
```

### `sort` : Trier

```bash
sort fichier.txt         # Tri alphabétique  
sort -n fichier.txt      # Tri numérique  
sort -r fichier.txt      # Tri inversé  
```

### `uniq` : Supprimer les doublons

```bash
sort fichier.txt | uniq         # Lignes uniques  
sort fichier.txt | uniq -c      # Avec compteur  
```

### `cut` : Extraire des colonnes

```bash
cut -d: -f1 /etc/passwd    # Premier champ (noms utilisateurs)  
cut -c1-10 fichier.txt     # 10 premiers caractères  
```

---

## Résumé

Vous maîtrisez maintenant les outils essentiels pour afficher et rechercher :

**Pour afficher :**
- **cat** : Affichage rapide de fichiers courts
- **less** : Navigation confortable dans les fichiers longs
- **head** : Début de fichier
- **tail** : Fin de fichier (et suivi en temps réel avec `-f`)

**Pour rechercher :**
- **grep** : Recherche de texte dans les fichiers
- **find** : Recherche de fichiers et dossiers selon divers critères

**Conseils clés :**
- Utilisez `less` pour les fichiers longs
- `tail -f` est parfait pour surveiller les logs
- `grep -r` pour chercher dans tout un dossier
- Testez `find` sans `-delete` avant de supprimer
- Combinez les commandes avec pipes (`|`) pour plus de puissance

**Commandes favorites à retenir :**
```bash
less fichier.log                              # Lecture confortable  
tail -f /var/log/syslog                       # Surveiller les logs  
grep -rni "mot" ~/Documents                   # Recherche complète  
find ~ -name "*.pdf" -mtime -7                # PDFs récents  
cat fichier.txt | grep "mot" | wc -l          # Compter occurrences  
```

Dans le prochain chapitre, nous verrons comment éditer des fichiers directement dans le terminal avec `nano` et `vim`.

⏭️ [Édition de texte (nano, vim)](/07-le-terminal-et-commandes-de-base/05-edition-de-texte.md)
