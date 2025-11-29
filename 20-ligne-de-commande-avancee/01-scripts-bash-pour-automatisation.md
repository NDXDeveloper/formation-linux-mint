🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Scripts bash pour automatisation

## Introduction

Les scripts bash sont des fichiers texte contenant une série de commandes qui s'exécutent automatiquement les unes après les autres. Imaginez-les comme une "recette" que votre ordinateur suit à la lettre pour accomplir une tâche répétitive ou complexe.

Au lieu de taper manuellement 10 commandes à chaque fois que vous voulez effectuer une opération, vous les écrivez une seule fois dans un script, et ensuite il suffit de lancer ce script.

### Pourquoi utiliser des scripts bash ?

- **Gain de temps** : Automatiser les tâches répétitives
- **Fiabilité** : Éviter les erreurs de frappe
- **Reproductibilité** : Exécuter exactement les mêmes étapes à chaque fois
- **Partage** : Transmettre facilement des procédures à d'autres utilisateurs
- **Planification** : Possibilité d'exécuter des scripts automatiquement (avec cron, que nous verrons dans le chapitre suivant)

## Anatomie d'un script bash

### Structure de base

Un script bash minimal ressemble à ceci :

```bash
#!/bin/bash
# Ceci est un commentaire

echo "Bonjour, ceci est mon premier script !"
```

**Explications :**
- `#!/bin/bash` : C'est le "shebang". Il indique au système quel interpréteur utiliser pour exécuter le script (ici, bash)
- `#` : Tout ce qui suit ce symbole est un commentaire (ignoré lors de l'exécution)
- `echo` : Affiche du texte à l'écran

### Créer votre premier script

**Étape 1 : Créer le fichier**

Ouvrez un terminal et créez un nouveau fichier :

```bash
nano mon_premier_script.sh
```

L'extension `.sh` indique qu'il s'agit d'un script shell (c'est une convention, pas une obligation).

**Étape 2 : Écrire le script**

Dans nano, tapez :

```bash
#!/bin/bash
# Mon premier script bash
# Auteur : Votre nom
# Date : 2024

echo "=================================="
echo "  Bienvenue dans mon script !"
echo "=================================="
echo ""
echo "Nom d'utilisateur : $USER"
echo "Répertoire actuel : $PWD"
echo "Date et heure : $(date)"
echo ""
echo "Script terminé avec succès !"
```

Sauvegardez avec `Ctrl+O`, puis quittez avec `Ctrl+X`.

**Étape 3 : Rendre le script exécutable**

Par défaut, votre fichier n'est qu'un simple fichier texte. Pour le transformer en programme exécutable :

```bash
chmod +x mon_premier_script.sh
```

**Étape 4 : Exécuter le script**

```bash
./mon_premier_script.sh
```

Le `./` indique que le script se trouve dans le répertoire courant.

## Variables dans les scripts

Les variables permettent de stocker des informations pour les réutiliser plus tard.

### Variables simples

```bash
#!/bin/bash

# Définir des variables
nom="Linux Mint"
version="21.3"
bureau="Cinnamon"

# Utiliser les variables
echo "Système d'exploitation : $nom"
echo "Version : $version"
echo "Environnement de bureau : $bureau"
```

**Important :**
- Pas d'espace autour du signe `=`
- Pour utiliser une variable, on la préfixe avec `$`

### Variables système prédéfinies

Bash propose de nombreuses variables déjà définies :

```bash
#!/bin/bash

echo "Nom d'utilisateur : $USER"
echo "Répertoire personnel : $HOME"
echo "Répertoire actuel : $PWD"
echo "Shell utilisé : $SHELL"
echo "Nom de la machine : $HOSTNAME"
```

### Récupérer des entrées utilisateur

Vous pouvez demander des informations à l'utilisateur :

```bash
#!/bin/bash

echo "Comment vous appelez-vous ?"
read nom

echo "Bonjour $nom, bienvenue !"
```

La commande `read` attend que l'utilisateur tape quelque chose et appuie sur Entrée.

## Exemples de scripts utiles

### Script de sauvegarde simple

```bash
#!/bin/bash
# Script de sauvegarde de documents

# Variables
SOURCE="$HOME/Documents"
DESTINATION="$HOME/Sauvegardes"
DATE=$(date +%Y-%m-%d_%H-%M-%S)
NOM_ARCHIVE="documents_$DATE.tar.gz"

# Création du répertoire de destination si nécessaire
mkdir -p "$DESTINATION"

# Affichage d'un message
echo "Début de la sauvegarde..."

# Création de l'archive
tar -czf "$DESTINATION/$NOM_ARCHIVE" "$SOURCE"

# Vérification du succès
if [ $? -eq 0 ]; then
    echo "Sauvegarde réussie : $NOM_ARCHIVE"
else
    echo "Erreur lors de la sauvegarde !"
fi
```

**Ce que fait ce script :**
1. Définit des variables pour la source et la destination
2. Crée un nom d'archive avec la date et l'heure actuelles
3. Crée le répertoire de destination s'il n'existe pas
4. Compresse les documents dans une archive
5. Vérifie que tout s'est bien passé

### Script de nettoyage système

```bash
#!/bin/bash
# Script de nettoyage basique

echo "======================================="
echo "  Script de nettoyage du système"
echo "======================================="
echo ""

# Mise à jour de la liste des paquets
echo "1. Mise à jour de la liste des paquets..."
sudo apt update

# Suppression des paquets inutiles
echo ""
echo "2. Suppression des paquets inutiles..."
sudo apt autoremove -y

# Nettoyage du cache
echo ""
echo "3. Nettoyage du cache APT..."
sudo apt autoclean

# Vider la corbeille
echo ""
echo "4. Vidage de la corbeille..."
rm -rf ~/.local/share/Trash/*

# Affichage de l'espace disque
echo ""
echo "5. Espace disque disponible :"
df -h / | tail -n 1

echo ""
echo "Nettoyage terminé !"
```

### Script d'information système

```bash
#!/bin/bash
# Affiche des informations sur le système

clear
echo "╔════════════════════════════════════════╗"
echo "║   INFORMATIONS SYSTÈME - LINUX MINT    ║"
echo "╔════════════════════════════════════════╗"
echo ""

echo "📅 DATE ET HEURE"
echo "   $(date '+%A %d %B %Y - %H:%M:%S')"
echo ""

echo "👤 UTILISATEUR"
echo "   Nom : $USER"
echo "   Répertoire : $HOME"
echo ""

echo "💻 SYSTÈME"
echo "   Distribution : $(lsb_release -d | cut -f2)"
echo "   Noyau : $(uname -r)"
echo "   Architecture : $(uname -m)"
echo ""

echo "🖥️  MATÉRIEL"
echo "   Processeur : $(grep "model name" /proc/cpuinfo | head -1 | cut -d: -f2 | xargs)"
echo "   Mémoire RAM : $(free -h | grep Mem | awk '{print $2}')"
echo ""

echo "💾 ESPACE DISQUE"
df -h / | tail -n 1 | awk '{print "   Total : " $2 "\n   Utilisé : " $3 "\n   Disponible : " $4 "\n   Utilisation : " $5}'
echo ""

echo "🌐 RÉSEAU"
echo "   Adresse IP locale : $(hostname -I | awk '{print $1}')"
echo "   Nom de la machine : $HOSTNAME"
echo ""

echo "⏱️  TEMPS DE FONCTIONNEMENT"
echo "   $(uptime -p)"
echo ""
```

## Conditions (if/else)

Les conditions permettent à votre script de prendre des décisions.

### Structure de base

```bash
#!/bin/bash

if [ condition ]; then
    # code si la condition est vraie
else
    # code si la condition est fausse
fi
```

### Exemple pratique

```bash
#!/bin/bash
# Vérifier si un fichier existe

echo "Entrez le nom d'un fichier :"
read fichier

if [ -f "$fichier" ]; then
    echo "Le fichier existe !"
    echo "Taille : $(du -h "$fichier" | cut -f1)"
else
    echo "Le fichier n'existe pas."
fi
```

### Opérateurs de comparaison courants

**Pour les fichiers :**
- `-f fichier` : Le fichier existe et est un fichier régulier
- `-d dossier` : Le dossier existe
- `-e chemin` : Le chemin existe (fichier ou dossier)
- `-r fichier` : Le fichier est lisible
- `-w fichier` : Le fichier est modifiable
- `-x fichier` : Le fichier est exécutable

**Pour les nombres :**
- `-eq` : égal à
- `-ne` : différent de
- `-lt` : inférieur à
- `-le` : inférieur ou égal à
- `-gt` : supérieur à
- `-ge` : supérieur ou égal à

**Pour les chaînes de caractères :**
- `=` : égal à
- `!=` : différent de
- `-z` : chaîne vide
- `-n` : chaîne non vide

### Exemple avec plusieurs conditions

```bash
#!/bin/bash
# Vérifier l'espace disque

espace_libre=$(df / | tail -1 | awk '{print $5}' | sed 's/%//')

if [ $espace_libre -lt 50 ]; then
    echo "✅ Espace disque OK ($espace_libre% utilisé)"
elif [ $espace_libre -lt 80 ]; then
    echo "⚠️  Attention : $espace_libre% d'espace utilisé"
else
    echo "🚨 ALERTE : Espace disque critique ($espace_libre% utilisé) !"
fi
```

## Boucles

Les boucles permettent de répéter des actions.

### Boucle for

```bash
#!/bin/bash
# Afficher les nombres de 1 à 5

for i in 1 2 3 4 5; do
    echo "Nombre : $i"
done
```

### Boucle for avec une séquence

```bash
#!/bin/bash
# Créer plusieurs dossiers

for i in {1..10}; do
    mkdir -p "dossier_$i"
    echo "Dossier $i créé"
done
```

### Boucle for sur des fichiers

```bash
#!/bin/bash
# Renommer tous les fichiers .txt en .md

for fichier in *.txt; do
    nouveau="${fichier%.txt}.md"
    mv "$fichier" "$nouveau"
    echo "Renommé : $fichier → $nouveau"
done
```

### Boucle while

```bash
#!/bin/bash
# Compte à rebours

compte=10

while [ $compte -gt 0 ]; do
    echo "Compte à rebours : $compte"
    sleep 1
    compte=$((compte - 1))
done

echo "Décollage !"
```

## Fonctions

Les fonctions permettent de réutiliser du code et de mieux organiser vos scripts.

```bash
#!/bin/bash

# Définition d'une fonction
dire_bonjour() {
    echo "Bonjour $1 !"
}

# Fonction avec calcul
additionner() {
    resultat=$(($1 + $2))
    echo "Le résultat de $1 + $2 = $resultat"
}

# Utilisation des fonctions
dire_bonjour "Alice"
dire_bonjour "Bob"
additionner 5 3
additionner 12 8
```

### Exemple de fonction utile

```bash
#!/bin/bash

# Fonction pour vérifier si un logiciel est installé
verifier_logiciel() {
    if command -v $1 &> /dev/null; then
        echo "✅ $1 est installé"
        return 0
    else
        echo "❌ $1 n'est pas installé"
        return 1
    fi
}

# Vérifier plusieurs logiciels
echo "Vérification des logiciels..."
echo ""
verifier_logiciel "firefox"
verifier_logiciel "git"
verifier_logiciel "htop"
verifier_logiciel "code"
```

## Arguments de ligne de commande

Vos scripts peuvent accepter des paramètres lorsqu'on les lance.

```bash
#!/bin/bash
# Script qui utilise des arguments

echo "Nom du script : $0"
echo "Premier argument : $1"
echo "Deuxième argument : $2"
echo "Nombre d'arguments : $#"
echo "Tous les arguments : $@"
```

Si vous lancez ce script avec `./script.sh fichier1.txt fichier2.txt`, vous obtiendrez :
- `$0` : `./script.sh`
- `$1` : `fichier1.txt`
- `$2` : `fichier2.txt`
- `$#` : `2`
- `$@` : `fichier1.txt fichier2.txt`

### Exemple pratique : Script de conversion d'images

```bash
#!/bin/bash
# Convertir une image en différents formats

if [ $# -eq 0 ]; then
    echo "Usage : $0 <fichier_image>"
    exit 1
fi

fichier=$1

if [ ! -f "$fichier" ]; then
    echo "Erreur : Le fichier '$fichier' n'existe pas"
    exit 1
fi

nom_base="${fichier%.*}"

echo "Conversion de $fichier..."
convert "$fichier" "${nom_base}.png"
convert "$fichier" "${nom_base}.jpg"
convert "$fichier" "${nom_base}.webp"

echo "Conversion terminée !"
echo "Fichiers créés :"
ls -lh "${nom_base}".{png,jpg,webp}
```

## Gestion des erreurs

Il est important de gérer les erreurs pour que vos scripts soient robustes.

### Vérifier le code de retour

```bash
#!/bin/bash
# Créer un dossier et gérer les erreurs

mkdir /tmp/test_dossier

if [ $? -eq 0 ]; then
    echo "✅ Dossier créé avec succès"
else
    echo "❌ Erreur lors de la création du dossier"
    exit 1
fi
```

### Utiliser set -e

```bash
#!/bin/bash
# Arrêter le script à la première erreur
set -e

echo "Mise à jour du système..."
sudo apt update
sudo apt upgrade -y

echo "Installation de logiciels..."
sudo apt install -y htop neofetch

echo "Tout s'est bien passé !"
```

Avec `set -e`, le script s'arrêtera automatiquement si une commande échoue.

### Mode verbeux pour le débogage

```bash
#!/bin/bash
# Afficher chaque commande avant de l'exécuter
set -x

mkdir test
cd test
touch fichier.txt
ls -la
```

`set -x` affiche chaque commande avant son exécution, très utile pour comprendre ce qui se passe.

## Script avancé : Sauvegarde automatique complète

Voici un exemple de script plus complet qui combine plusieurs concepts :

```bash
#!/bin/bash
#
# Script de sauvegarde automatique avec rotation
# Usage : ./sauvegarde.sh [dossier_source]
#

# Configuration
SOURCE="${1:-$HOME/Documents}"
DESTINATION="$HOME/Sauvegardes"
MAX_SAUVEGARDES=7
DATE=$(date +%Y-%m-%d_%H-%M-%S)
NOM_ARCHIVE="backup_$DATE.tar.gz"
LOG_FILE="$DESTINATION/backup.log"

# Fonction pour logger
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

# Fonction pour afficher les erreurs
erreur() {
    log "ERREUR: $1"
    exit 1
}

# Vérifications préliminaires
if [ ! -d "$SOURCE" ]; then
    erreur "Le dossier source '$SOURCE' n'existe pas"
fi

# Création du répertoire de destination
mkdir -p "$DESTINATION" || erreur "Impossible de créer le répertoire de destination"

# Début de la sauvegarde
log "=========================================="
log "Début de la sauvegarde"
log "Source : $SOURCE"
log "Destination : $DESTINATION/$NOM_ARCHIVE"

# Calcul de la taille à sauvegarder
taille=$(du -sh "$SOURCE" | cut -f1)
log "Taille à sauvegarder : $taille"

# Création de l'archive
log "Création de l'archive en cours..."
if tar -czf "$DESTINATION/$NOM_ARCHIVE" "$SOURCE" 2>/dev/null; then
    taille_archive=$(du -h "$DESTINATION/$NOM_ARCHIVE" | cut -f1)
    log "✅ Sauvegarde réussie : $NOM_ARCHIVE ($taille_archive)"
else
    erreur "Échec de la création de l'archive"
fi

# Rotation des anciennes sauvegardes
log "Nettoyage des anciennes sauvegardes..."
nb_sauvegardes=$(ls -1 "$DESTINATION"/backup_*.tar.gz 2>/dev/null | wc -l)

if [ $nb_sauvegardes -gt $MAX_SAUVEGARDES ]; then
    nb_a_supprimer=$((nb_sauvegardes - MAX_SAUVEGARDES))
    log "Suppression de $nb_a_supprimer ancienne(s) sauvegarde(s)"

    ls -1t "$DESTINATION"/backup_*.tar.gz | tail -n $nb_a_supprimer | while read fichier; do
        rm -f "$fichier"
        log "Supprimé : $(basename $fichier)"
    done
fi

# Résumé
log "Nombre de sauvegardes conservées : $(ls -1 "$DESTINATION"/backup_*.tar.gz | wc -l)/$MAX_SAUVEGARDES"
log "Espace disque utilisé par les sauvegardes : $(du -sh "$DESTINATION" | cut -f1)"
log "Sauvegarde terminée avec succès"
log "=========================================="

# Notification
notify-send "Sauvegarde terminée" "La sauvegarde de $SOURCE a été effectuée avec succès" -i dialog-information
```

## Bonnes pratiques

### 1. Toujours commencer par le shebang

```bash
#!/bin/bash
```

### 2. Commenter votre code

```bash
# Description de ce que fait le script
# Auteur et date si pertinent
# Exemple d'utilisation
```

### 3. Utiliser des variables pour les valeurs importantes

```bash
# ✅ Bon
DESTINATION="/chemin/vers/destination"
cp fichier.txt "$DESTINATION"

# ❌ Moins bon
cp fichier.txt /chemin/vers/destination
```

### 4. Vérifier les conditions d'erreur

```bash
if [ ! -f "$fichier" ]; then
    echo "Erreur : fichier introuvable"
    exit 1
fi
```

### 5. Utiliser des guillemets autour des variables

```bash
# ✅ Sûr
rm "$fichier"

# ❌ Peut causer des problèmes si le nom contient des espaces
rm $fichier
```

### 6. Rendre vos scripts portables

Évitez les chemins absolus quand c'est possible :

```bash
# ✅ Bon
SCRIPT_DIR="$(cd "$(dirname "$0")" && pwd)"

# ❌ Moins portable
SCRIPT_DIR="/home/utilisateur/scripts"
```

### 7. Tester vos scripts

Testez toujours vos scripts avec différentes conditions avant de les utiliser en production, surtout s'ils modifient ou suppriment des fichiers.

## Où placer vos scripts ?

### Pour un usage personnel

Créez un dossier dédié dans votre répertoire personnel :

```bash
mkdir -p ~/scripts
```

Ajoutez ce dossier à votre PATH en modifiant `~/.bashrc` :

```bash
echo 'export PATH="$HOME/scripts:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Maintenant, vous pourrez lancer vos scripts depuis n'importe où sans `./`

### Pour une utilisation système

Pour que vos scripts soient accessibles à tous les utilisateurs :

```bash
sudo cp mon_script.sh /usr/local/bin/mon_script
sudo chmod +x /usr/local/bin/mon_script
```

## Ressources pour aller plus loin

Les scripts bash peuvent devenir très complexes. Voici quelques ressources pour approfondir :

- **Guide Bash avancé** : [abs.traduc.org](https://abs.traduc.org/) (en français)
- **ShellCheck** : Un outil en ligne pour vérifier vos scripts ([shellcheck.net](https://www.shellcheck.net/))
- **Man pages** : `man bash` pour la documentation complète

## Conclusion

Les scripts bash sont un outil puissant pour automatiser vos tâches quotidiennes sous Linux. Commencez par de petits scripts simples, et progressivement vous pourrez créer des outils complexes et personnalisés qui vous feront gagner un temps précieux.

N'ayez pas peur d'expérimenter, et n'oubliez pas : chaque expert a commencé par un simple `echo "Bonjour monde !"` 🚀

⏭️ [Cron et tâches planifiées (crontab, anacron)](/20-ligne-de-commande-avancee/02-cron-et-taches-planifiees.md)
