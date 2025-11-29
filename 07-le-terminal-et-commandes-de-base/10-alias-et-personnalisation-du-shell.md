🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.10 - Alias et personnalisation du shell (.bashrc)

## Introduction

Le terminal est un outil que vous allez utiliser régulièrement. Autant le personnaliser pour qu'il soit agréable, efficace et adapté à votre façon de travailler !

Les alias et la personnalisation du shell vous permettent de :
- Créer des raccourcis pour vos commandes longues
- Définir vos propres commandes personnalisées
- Modifier l'apparence du terminal (couleurs, prompt)
- Automatiser des tâches répétitives
- Gagner un temps considérable au quotidien

**Analogie :** C'est comme personnaliser votre bureau physique ou votre voiture. Vous ajustez tout pour que ce soit confortable et efficace selon vos habitudes.

Dans ce chapitre, nous allons transformer votre terminal basique en un environnement de travail sur mesure !

---

## Les alias : Créer vos propres raccourcis

### Qu'est-ce qu'un alias ?

Un **alias** est un raccourci personnalisé pour une commande ou une série de commandes.

**Principe :**
```bash
alias nom='commande'
```

**Exemple simple :**
```bash
alias ll='ls -la'
```

Maintenant, quand vous tapez `ll`, c'est comme si vous tapiez `ls -la`.

### Pourquoi utiliser des alias ?

**1. Gagner du temps**

Au lieu de taper :
```bash
sudo apt update && sudo apt upgrade
```

Créez :
```bash
alias update='sudo apt update && sudo apt upgrade'
```

Puis tapez simplement :
```bash
update
```

**2. Éviter les erreurs**

Au lieu de risquer une faute de frappe dans :
```bash
grep -r --exclude-dir=.git --color=auto
```

Créez :
```bash
alias grepr='grep -r --exclude-dir=.git --color=auto'
```

**3. Mémoriser les options complexes**

Vous ne vous souvenez jamais des options de `tar` ? Créez :
```bash
alias extract='tar -xzvf'
alias compress='tar -czvf'
```

### Créer un alias temporaire

**Syntaxe :**
```bash
alias nom='commande'
```

**Exemples :**

```bash
alias ll='ls -lah'
alias ..='cd ..'
alias ...='cd ../..'
alias h='history'
alias c='clear'
```

**Important :** Ces alias ne durent que pendant la session actuelle. Quand vous fermez le terminal, ils disparaissent.

### Voir vos alias actifs

```bash
alias
```

Affiche tous les alias définis dans la session actuelle.

**Voir un alias spécifique :**
```bash
alias ll
```

Affiche la définition de `ll`.

### Supprimer un alias

```bash
unalias nom
```

**Exemple :**
```bash
unalias ll
```

**Supprimer tous les alias :**
```bash
unalias -a
```

---

## Le fichier .bashrc : Personnalisation permanente

### Qu'est-ce que .bashrc ?

**`.bashrc`** (Bash Run Commands) est un fichier de configuration qui s'exécute automatiquement à chaque ouverture d'un nouveau terminal.

**Emplacement :**
```bash
~/.bashrc
```

Le `~` signifie votre dossier personnel (`/home/utilisateur/`).

**Contenu :**
- Alias permanents
- Variables d'environnement
- Fonctions personnalisées
- Configuration du shell
- Personnalisation du prompt

**Principe :** Tout ce que vous mettez dans `.bashrc` sera exécuté à chaque démarrage du terminal.

### Éditer .bashrc

```bash
nano ~/.bashrc
```

ou

```bash
vim ~/.bashrc
```

**⚠️ Conseil :** Faites une sauvegarde avant de modifier !

```bash
cp ~/.bashrc ~/.bashrc.backup
```

### Structure typique de .bashrc

Voici à quoi ressemble un `.bashrc` basique :

```bash
# ~/.bashrc

# Si la session n'est pas interactive, arrêter
[ -z "$PS1" ] && return

# Historique
HISTSIZE=10000
HISTFILESIZE=20000

# Options du shell
shopt -s histappend
shopt -s checkwinsize

# Alias
alias ll='ls -lah'
alias la='ls -A'
alias l='ls -CF'

# Personnalisation du prompt
PS1='\u@\h:\w\$ '

# Charger les fichiers supplémentaires
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

### Appliquer les modifications

Après avoir modifié `.bashrc`, vous devez le recharger :

```bash
source ~/.bashrc
```

ou plus court :

```bash
. ~/.bashrc
```

**Alternative :** Fermez et rouvrez le terminal.

---

## Créer des alias permanents

### Méthode 1 : Directement dans .bashrc

Ouvrez `.bashrc` :
```bash
nano ~/.bashrc
```

Ajoutez vos alias à la fin du fichier :

```bash
# Mes alias personnalisés
alias update='sudo apt update && sudo apt upgrade'
alias install='sudo apt install'
alias remove='sudo apt remove'
alias search='apt search'
```

Sauvegardez (**Ctrl+O** puis **Entrée**, puis **Ctrl+X**), et rechargez :

```bash
source ~/.bashrc
```

### Méthode 2 : Fichier séparé .bash_aliases

Pour garder `.bashrc` propre, créez un fichier dédié :

```bash
nano ~/.bash_aliases
```

Ajoutez vos alias :

```bash
# Navigation
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# Commandes avec options par défaut
alias cp='cp -i'
alias mv='mv -i'
alias rm='rm -i'
alias mkdir='mkdir -pv'

# Listing
alias ll='ls -lah'
alias la='ls -A'
alias lt='ls -lth'

# Git
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'

# Système
alias update='sudo apt update && sudo apt upgrade'
alias install='sudo apt install'
alias ports='sudo netstat -tulpn'
alias psg='ps aux | grep -v grep | grep -i -e VSZ -e'
```

**Important :** Vérifiez que `.bashrc` charge ce fichier (généralement déjà présent) :

```bash
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

Puis rechargez :
```bash
source ~/.bashrc
```

---

## Exemples d'alias utiles

### Navigation

```bash
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias ~='cd ~'
alias -- -='cd -'    # Retour au dossier précédent

# Dossiers fréquents
alias docs='cd ~/Documents'
alias dl='cd ~/Téléchargements'
alias proj='cd ~/Projets'
```

### Listing amélioré

```bash
alias ll='ls -lah'              # Liste détaillée
alias la='ls -A'                # Tous les fichiers
alias lt='ls -lth'              # Trié par date
alias lS='ls -lSh'              # Trié par taille
alias ldir='ls -d */'           # Seulement les dossiers
alias tree='tree -C'            # Arborescence colorée
```

### Commandes avec confirmation

```bash
alias cp='cp -i'                # Demande confirmation avant d'écraser
alias mv='mv -i'
alias rm='rm -i'
alias ln='ln -i'
```

### Raccourcis système

```bash
alias update='sudo apt update && sudo apt upgrade'
alias install='sudo apt install'
alias remove='sudo apt remove'
alias search='apt search'
alias autoremove='sudo apt autoremove'
alias clean='sudo apt autoclean && sudo apt clean'

alias reboot='sudo reboot'
alias shutdown='sudo shutdown -h now'
```

### Git

```bash
alias gs='git status'
alias ga='git add'
alias gaa='git add --all'
alias gc='git commit'
alias gcm='git commit -m'
alias gp='git push'
alias gpl='git pull'
alias gl='git log --oneline --graph --decorate'
alias gd='git diff'
alias gb='git branch'
alias gco='git checkout'
```

### Réseau

```bash
alias ping='ping -c 5'          # Seulement 5 pings
alias ports='sudo netstat -tulpn'
alias myip='curl ifconfig.me'   # Votre IP publique
alias localip='ip addr show'
```

### Recherche et filtrage

```bash
alias grep='grep --color=auto'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias h='history'
alias hgrep='history | grep'
```

### Utilitaires

```bash
alias c='clear'
alias x='exit'
alias e='nano'                  # Votre éditeur préféré
alias path='echo -e ${PATH//:/\\n}'
alias now='date +"%T"'
alias nowdate='date +"%d-%m-%Y"'
```

### Système de fichiers

```bash
alias df='df -h'                # Espace disque lisible
alias du='du -h'                # Taille lisible
alias free='free -h'            # Mémoire lisible
alias mkdir='mkdir -pv'         # Créer parents + verbose
```

### Sécurité

```bash
alias chmod='chmod --preserve-root'
alias chown='chown --preserve-root'
alias chgrp='chgrp --preserve-root'
```

**Protège contre les modifications accidentelles de `/`**

### Alias avec paramètres

Pour les alias avec paramètres, utilisez des fonctions (voir plus bas) :

```bash
# Fonction au lieu d'alias
extract() {
    if [ -f $1 ]; then
        case $1 in
            *.tar.bz2)   tar xjf $1    ;;
            *.tar.gz)    tar xzf $1    ;;
            *.bz2)       bunzip2 $1    ;;
            *.rar)       unrar x $1    ;;
            *.gz)        gunzip $1     ;;
            *.tar)       tar xf $1     ;;
            *.tbz2)      tar xjf $1    ;;
            *.tgz)       tar xzf $1    ;;
            *.zip)       unzip $1      ;;
            *.Z)         uncompress $1 ;;
            *.7z)        7z x $1       ;;
            *)           echo "'$1' ne peut pas être extrait" ;;
        esac
    else
        echo "'$1' n'est pas un fichier valide"
    fi
}
```

---

## Variables d'environnement

### Qu'est-ce qu'une variable d'environnement ?

Une variable qui stocke des informations utilisées par le shell et les programmes.

**Voir toutes les variables :**
```bash
env
```

ou

```bash
printenv
```

**Voir une variable spécifique :**
```bash
echo $HOME
echo $USER
echo $PATH
```

### Variables importantes

| Variable | Description | Exemple |
|----------|-------------|---------|
| `HOME` | Votre dossier personnel | `/home/utilisateur` |
| `USER` | Votre nom d'utilisateur | `utilisateur` |
| `PATH` | Chemins de recherche des programmes | `/usr/bin:/bin:/usr/local/bin` |
| `SHELL` | Votre shell actuel | `/bin/bash` |
| `EDITOR` | Éditeur par défaut | `nano` |
| `LANG` | Langue du système | `fr_FR.UTF-8` |

### Créer une variable temporaire

```bash
MA_VARIABLE="valeur"
```

**Utilisation :**
```bash
echo $MA_VARIABLE
```

**Important :** Cette variable n'existe que dans le terminal actuel.

### Créer une variable permanente

Dans `.bashrc` :

```bash
export EDITOR="nano"
export VISUAL="nano"
export BROWSER="firefox"
```

**Note :** `export` rend la variable disponible pour les programmes enfants.

### Ajouter au PATH

Le `PATH` contient les dossiers où le système cherche les programmes.

**Voir le PATH actuel :**
```bash
echo $PATH
```

**Ajouter un dossier au PATH :**

Dans `.bashrc` :

```bash
export PATH="$PATH:$HOME/bin"
export PATH="$PATH:$HOME/.local/bin"
```

Cela ajoute `~/bin` et `~/.local/bin` au PATH.

**Ordre d'importance :**
```bash
export PATH="$HOME/bin:$PATH"
```

Ici, `~/bin` sera cherché **avant** les autres dossiers.

---

## Personnalisation du prompt (PS1)

### Qu'est-ce que le prompt ?

Le **prompt** (invite de commande) est le texte qui apparaît avant votre curseur.

**Par défaut :**
```
utilisateur@ordinateur:~$
```

### La variable PS1

Le prompt est contrôlé par la variable `PS1` (Prompt String 1).

**Voir votre PS1 actuel :**
```bash
echo $PS1
```

**Exemple de résultat :**
```
\u@\h:\w\$
```

### Codes spéciaux pour PS1

| Code | Description | Exemple |
|------|-------------|---------|
| `\u` | Nom d'utilisateur | `utilisateur` |
| `\h` | Nom de l'hôte (hostname) | `ordinateur` |
| `\H` | Nom de l'hôte complet | `ordinateur.local` |
| `\w` | Chemin actuel complet | `~/Documents/Projets` |
| `\W` | Dossier actuel seulement | `Projets` |
| `\d` | Date | `Mer Nov 30` |
| `\t` | Heure (24h) | `14:30:25` |
| `\T` | Heure (12h) | `02:30:25` |
| `\@` | Heure (12h AM/PM) | `02:30 PM` |
| `\n` | Nouvelle ligne | |
| `\$` | `$` si utilisateur, `#` si root | |
| `\!` | Numéro de la commande dans l'historique | |

### Couleurs dans le prompt

**Syntaxe :**
```bash
\[\033[XXm\]texte\[\033[0m\]
```

**Codes de couleur :**

| Code | Couleur |
|------|---------|
| `30` | Noir |
| `31` | Rouge |
| `32` | Vert |
| `33` | Jaune |
| `34` | Bleu |
| `35` | Magenta |
| `36` | Cyan |
| `37` | Blanc |

**Préfixes :**
- `0;` : Normal
- `1;` : Gras
- `4;` : Souligné

**Exemple :**
```bash
# Utilisateur en vert, @ et hostname en blanc, chemin en bleu
PS1='\[\033[1;32m\]\u\[\033[0m\]@\[\033[1;34m\]\h\[\033[0m\]:\w\$ '
```

### Exemples de prompts personnalisés

#### Minimaliste

```bash
PS1='\w\$ '
```

Résultat :
```
~/Documents/Projets$
```

#### Avec couleurs

```bash
PS1='\[\033[1;32m\]\u@\h\[\033[0m\]:\[\033[1;34m\]\w\[\033[0m\]\$ '
```

Résultat (en couleur) :
```
utilisateur@ordinateur:~/Documents$
```

#### Avec heure

```bash
PS1='[\t] \u@\h:\w\$ '
```

Résultat :
```
[14:30:25] utilisateur@ordinateur:~/Documents$
```

#### Sur deux lignes

```bash
PS1='\[\033[1;32m\]\u@\h\[\033[0m\]:\[\033[1;34m\]\w\[\033[0m\]\n\$ '
```

Résultat :
```
utilisateur@ordinateur:~/Documents
$
```

#### Avec Git (avancé)

Pour afficher la branche Git dans le prompt :

```bash
# Fonction pour obtenir la branche Git
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

# Prompt avec Git
PS1='\[\033[1;32m\]\u@\h\[\033[0m\]:\[\033[1;34m\]\w\[\033[1;33m\]$(parse_git_branch)\[\033[0m\]\$ '
```

Résultat dans un dépôt Git :
```
utilisateur@ordinateur:~/projet (main)$
```

---

## Fonctions Bash personnalisées

Les fonctions permettent de créer des commandes complexes avec paramètres.

### Syntaxe de base

```bash
nom_fonction() {
    commandes
}
```

### Exemples de fonctions utiles

#### Créer et entrer dans un dossier

```bash
mkcd() {
    mkdir -p "$1" && cd "$1"
}
```

**Utilisation :**
```bash
mkcd nouveau_projet
# Crée et entre dans le dossier
```

#### Extraire n'importe quelle archive

```bash
extract() {
    if [ -f $1 ]; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar x $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)           echo "'$1' ne peut pas être extrait" ;;
        esac
    else
        echo "'$1' n'est pas un fichier valide"
    fi
}
```

**Utilisation :**
```bash
extract archive.tar.gz
extract fichier.zip
```

#### Créer une sauvegarde d'un fichier

```bash
backup() {
    cp "$1"{,.backup-$(date +%Y%m%d-%H%M%S)}
}
```

**Utilisation :**
```bash
backup fichier.txt
# Crée : fichier.txt.backup-20241130-143025
```

#### Rechercher un fichier et afficher son chemin

```bash
ff() {
    find . -type f -iname "*$1*"
}
```

**Utilisation :**
```bash
ff rapport
# Trouve tous les fichiers contenant "rapport"
```

#### Calculatrice rapide

```bash
calc() {
    echo "$*" | bc -l
}
```

**Utilisation :**
```bash
calc 5 + 3
calc 10 / 3
```

#### Mettre à jour le système

```bash
update() {
    echo "Mise à jour du système..."
    sudo apt update && sudo apt upgrade -y
    sudo apt autoremove -y
    sudo apt autoclean
    echo "Système à jour !"
}
```

#### Afficher les processus consommant le plus de CPU

```bash
pscpu() {
    ps aux | sort -nrk 3,3 | head -n 10
}
```

#### Afficher les processus consommant le plus de mémoire

```bash
psmem() {
    ps aux | sort -nrk 4,4 | head -n 10
}
```

---

## Configuration complète exemple

Voici un exemple de configuration complète dans `.bashrc` :

```bash
# ~/.bashrc

# ============================================
# HISTORIQUE
# ============================================
HISTSIZE=10000
HISTFILESIZE=20000
HISTCONTROL=ignoreboth:erasedups
HISTTIMEFORMAT="%F %T  "
shopt -s histappend

# ============================================
# OPTIONS DU SHELL
# ============================================
shopt -s checkwinsize      # Mise à jour des dimensions de la fenêtre
shopt -s cdspell           # Correction automatique des fautes de frappe dans cd
shopt -s cmdhist           # Commandes multi-lignes sur une ligne

# ============================================
# VARIABLES D'ENVIRONNEMENT
# ============================================
export EDITOR="nano"
export VISUAL="nano"
export BROWSER="firefox"
export PATH="$PATH:$HOME/bin:$HOME/.local/bin"

# ============================================
# COULEURS
# ============================================
# ls coloré
alias ls='ls --color=auto'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# ============================================
# ALIAS - NAVIGATION
# ============================================
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias ~='cd ~'
alias -- -='cd -'

# ============================================
# ALIAS - LISTING
# ============================================
alias ll='ls -lah'
alias la='ls -A'
alias l='ls -CF'
alias lt='ls -lth'
alias lS='ls -lSh'

# ============================================
# ALIAS - SYSTÈME
# ============================================
alias update='sudo apt update && sudo apt upgrade'
alias install='sudo apt install'
alias remove='sudo apt remove'
alias search='apt search'
alias clean='sudo apt autoremove && sudo apt autoclean'

# ============================================
# ALIAS - UTILITAIRES
# ============================================
alias c='clear'
alias h='history'
alias hgrep='history | grep'
alias df='df -h'
alias free='free -h'
alias du='du -h'
alias mkdir='mkdir -pv'

# ============================================
# ALIAS - SÉCURITÉ
# ============================================
alias cp='cp -i'
alias mv='mv -i'
alias rm='rm -i'

# ============================================
# FONCTIONS
# ============================================

# Créer un dossier et y entrer
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Extraire n'importe quelle archive
extract() {
    if [ -f $1 ]; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar x $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)           echo "'$1' ne peut pas être extrait" ;;
        esac
    else
        echo "'$1' n'est pas un fichier valide"
    fi
}

# Sauvegarder un fichier
backup() {
    cp "$1"{,.backup-$(date +%Y%m%d-%H%M%S)}
}

# ============================================
# PROMPT PERSONNALISÉ
# ============================================
# Fonction pour la branche Git
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

# Prompt coloré
PS1='\[\033[1;32m\]\u@\h\[\033[0m\]:\[\033[1;34m\]\w\[\033[1;33m\]$(parse_git_branch)\[\033[0m\]\$ '

# ============================================
# CHARGER LES ALIAS SÉPARÉS (si fichier existe)
# ============================================
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# ============================================
# MESSAGE DE BIENVENUE
# ============================================
echo "Bienvenue, $USER !"
echo "Aujourd'hui : $(date '+%A %d %B %Y, %H:%M')"
```

---

## Outils et frameworks pour le shell

### Oh My Bash

Framework pour faciliter la personnalisation de Bash.

**Installation :**
```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

**Caractéristiques :**
- Thèmes pré-configurés
- Plugins utiles
- Configuration simplifiée

### Starship

Prompt personnalisable, rapide et moderne.

**Installation :**
```bash
curl -sS https://starship.rs/install.sh | sh
```

**Configuration dans `.bashrc` :**
```bash
eval "$(starship init bash)"
```

**Caractéristiques :**
- Très rapide
- Support Git, Python, Node, etc.
- Hautement personnalisable

### Bash-it

Framework similaire à Oh My Bash.

**Installation :**
```bash
git clone --depth=1 https://github.com/Bash-it/bash-it.git ~/.bash_it
~/.bash_it/install.sh
```

---

## Bonnes pratiques

### 1. Commentez votre configuration

```bash
# ALIAS - Navigation rapide
alias ..='cd ..'    # Dossier parent

# FONCTION - Créer et entrer dans un dossier
mkcd() {
    mkdir -p "$1" && cd "$1"
}
```

### 2. Organisez par sections

Regroupez les alias par catégorie :
- Navigation
- Listing
- Système
- Git
- Etc.

### 3. Sauvegardez avant de modifier

```bash
cp ~/.bashrc ~/.bashrc.backup_$(date +%Y%m%d)
```

### 4. Testez avant de rendre permanent

Créez d'abord un alias temporaire :
```bash
alias test='commande'
```

Si ça marche, ajoutez-le à `.bashrc`.

### 5. N'écrasez pas les commandes système

**Mauvais :**
```bash
alias ls='rm -rf'    # DANGEREUX !
```

**Bon :**
```bash
alias ll='ls -la'    # Nouveau nom
```

### 6. Utilisez des noms descriptifs

**Moins bon :**
```bash
alias a='sudo apt update && sudo apt upgrade'
```

**Meilleur :**
```bash
alias update='sudo apt update && sudo apt upgrade'
```

### 7. Documentez les alias complexes

```bash
# Affiche les 10 processus consommant le plus de mémoire
# Utilisation : psmem
psmem() {
    ps aux | sort -nrk 4,4 | head -n 10
}
```

### 8. Vérifiez la syntaxe

Après modification de `.bashrc` :

```bash
bash -n ~/.bashrc
```

Vérifie la syntaxe sans exécuter.

### 9. Rechargez après chaque modification

```bash
source ~/.bashrc
```

Ou utilisez un alias :
```bash
alias reload='source ~/.bashrc'
```

### 10. Gardez une copie de votre configuration

Versionnez votre `.bashrc` avec Git :

```bash
cd ~
git init
git add .bashrc .bash_aliases
git commit -m "Configuration initiale"
```

---

## Dépannage

### Erreur 1 : .bashrc ne se charge pas

**Problème :** Les modifications ne prennent pas effet.

**Solutions :**
1. Vérifiez la syntaxe : `bash -n ~/.bashrc`
2. Rechargez : `source ~/.bashrc`
3. Vérifiez les erreurs : `bash -x ~/.bashrc`

### Erreur 2 : Alias ne fonctionne pas

**Problème :** `bash: alias_name: command not found`

**Vérifiez :**
1. L'alias existe : `alias alias_name`
2. `.bashrc` est chargé : `source ~/.bashrc`
3. Pas d'espace autour du `=` : `alias ll='ls -la'` (pas `alias ll = 'ls -la'`)

### Erreur 3 : Prompt cassé

**Problème :** Le prompt affiche des caractères bizarres.

**Solution :**
Restaurez le prompt par défaut :
```bash
PS1='\u@\h:\w\$ '
source ~/.bashrc
```

### Erreur 4 : Terminal lent au démarrage

**Cause :** Trop de commandes dans `.bashrc`.

**Solutions :**
1. Supprimez les commandes inutiles
2. Déplacez les alias dans `.bash_aliases`
3. Optimisez les fonctions

### Erreur 5 : Variable PATH cassée

**Problème :** Les commandes de base ne fonctionnent plus.

**Solution temporaire :**
```bash
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Puis corrigez `.bashrc`.

---

## Ressources et exemples

### Dotfiles communautaires

Inspirez-vous de configurations publiques :

- **GitHub** : Recherchez "dotfiles" pour voir des exemples
- **dotfiles.github.io** : Collection de dotfiles
- **awesome-dotfiles** : Liste de configurations populaires

### Tester des alias en live

Site web pour tester : **explainshell.com**

Collez votre commande pour comprendre ce qu'elle fait.

---

## Résumé

### Alias

**Créer un alias temporaire :**
```bash
alias nom='commande'
```

**Créer un alias permanent :**
Dans `~/.bashrc` :
```bash
alias ll='ls -lah'
alias update='sudo apt update && sudo apt upgrade'
```

**Recharger :**
```bash
source ~/.bashrc
```

### Variables d'environnement

```bash
export EDITOR="nano"
export PATH="$PATH:$HOME/bin"
```

### Prompt (PS1)

```bash
# Codes utiles
\u - utilisateur
\h - hostname
\w - chemin complet
\W - dossier actuel
\$ - $ ou #

# Exemple coloré
PS1='\[\033[1;32m\]\u@\h\[\033[0m\]:\[\033[1;34m\]\w\[\033[0m\]\$ '
```

### Fonctions

```bash
mkcd() {
    mkdir -p "$1" && cd "$1"
}
```

### Fichiers importants

- **`~/.bashrc`** : Configuration principale
- **`~/.bash_aliases`** : Alias séparés
- **`~/.bash_logout`** : Exécuté à la déconnexion
- **`~/.bash_profile`** : Exécuté au login

### Commandes essentielles

```bash
nano ~/.bashrc           # Éditer la configuration
source ~/.bashrc         # Recharger
alias                    # Voir tous les alias
alias nom                # Voir un alias spécifique
unalias nom              # Supprimer un alias
bash -n ~/.bashrc        # Vérifier la syntaxe
```

### Checklist de personnalisation

- [ ] Sauvegarder `.bashrc` avant modification
- [ ] Configurer l'historique (taille, timestamps)
- [ ] Ajouter vos alias fréquents
- [ ] Créer des fonctions utiles
- [ ] Personnaliser le prompt
- [ ] Configurer les variables d'environnement
- [ ] Tester et recharger
- [ ] Documenter vos modifications

Votre `.bashrc` est votre environnement de travail personnel. Prenez le temps de le personnaliser selon vos besoins : c'est un investissement qui vous fera gagner énormément de temps au quotidien !

Avec un terminal bien configuré, vous serez beaucoup plus efficace et productif. N'hésitez pas à expérimenter, tester, et ajuster jusqu'à trouver la configuration parfaite pour vous.

---

**Félicitations !** Vous avez maintenant toutes les connaissances de base pour maîtriser le terminal Linux.

⏭️ [Processus et gestion (ps, top, kill)](/07-le-terminal-et-commandes-de-base/11-processus-et-gestion.md)
