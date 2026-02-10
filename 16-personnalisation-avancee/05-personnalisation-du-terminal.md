🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 16.5 - Personnalisation du terminal (Oh My Zsh, Starship)

## Introduction

Le terminal est l'un des outils les plus puissants de Linux. Si vous avez suivi les chapitres précédents, vous l'avez déjà utilisé à plusieurs reprises. Mais saviez-vous que vous pouvez le transformer en un outil non seulement plus beau, mais aussi beaucoup plus productif ?

La personnalisation du terminal ne se limite pas à l'esthétique : un terminal bien configuré peut vous faire gagner un temps considérable au quotidien grâce à l'autocomplétion intelligente, la coloration syntaxique, les raccourcis, et bien plus encore.

Dans ce chapitre, nous allons découvrir comment transformer votre terminal de base en un outil moderne, élégant et puissant grâce à **Oh My Zsh** et **Starship**.

---

## Comprendre les bases : Shell vs Terminal

Avant de commencer, clarifions quelques termes importants.

### Le Terminal (Émulateur de terminal)

C'est la **fenêtre** que vous ouvrez pour taper des commandes.

**Sur Linux Mint, les terminaux populaires :**
- **GNOME Terminal** (par défaut sur Cinnamon)
- **Xfce Terminal** (sur Xfce)
- **MATE Terminal** (sur MATE)
- **Terminator** (avancé, avec split de fenêtres)
- **Tilix** (moderne, avec tuiles)
- **Alacritty** (ultra-rapide, basé sur GPU)
- **Kitty** (moderne et performant)

### Le Shell

C'est le **programme** qui interprète vos commandes à l'intérieur du terminal.

**Shells courants :**

**1. Bash (Bourne Again Shell)**
- Shell par défaut sur la plupart des distributions Linux
- Très répandu et bien documenté
- Personnalisation via `.bashrc`
- Bon mais basique en termes de fonctionnalités modernes

**2. Zsh (Z Shell)**
- Plus moderne que Bash
- Meilleure autocomplétion
- Thèmes et plugins riches
- Compatible avec les scripts Bash
- **C'est ce que nous utiliserons avec Oh My Zsh**

**3. Fish (Friendly Interactive Shell)**
- Très moderne et convivial
- Autocomplétion intelligente par défaut
- Syntaxe différente de Bash (incompatible)
- Configuration plus simple mais moins de plugins

**Analogie :**
- **Terminal** = La fenêtre de votre navigateur web
- **Shell** = Le moteur du navigateur (Chrome, Firefox, etc.)

---

## Pourquoi personnaliser son terminal ?

### Avantages pratiques

**1. Productivité accrue**
- Autocomplétion intelligente qui devine vos commandes
- Navigation plus rapide dans l'historique
- Affichage d'informations utiles (branche Git, statut, etc.)
- Raccourcis et alias personnalisés

**2. Meilleure lisibilité**
- Coloration syntaxique des commandes
- Mise en évidence des erreurs
- Prompts informatifs et clairs

**3. Informations contextuelles**
- Voir la branche Git actuelle
- Statut des modifications (fichiers modifiés, à commit)
- Temps d'exécution des commandes
- Codes d'erreur

**4. Esthétique**
- Design moderne et agréable
- Icônes et symboles
- Thèmes personnalisables

### Ce que nous allons installer

Dans ce chapitre, nous verrons deux approches principales :

**Approche 1 : Oh My Zsh**
- Framework complet pour Zsh
- Nombreux thèmes et plugins
- Grande communauté
- Configuration via fichiers

**Approche 2 : Starship**
- Prompt universel (fonctionne avec Bash, Zsh, Fish...)
- Configuration moderne (TOML)
- Rapide et léger
- Design minimaliste

**Vous pouvez choisir l'un ou l'autre, ou même combiner les deux !**

---

## Préparation : Installation de Zsh

Avant d'installer Oh My Zsh, nous devons installer Zsh.

### Vérifier si Zsh est déjà installé

```bash
zsh --version
```

Si vous voyez quelque chose comme `zsh 5.8`, c'est déjà installé. Sinon, continuez.

### Installer Zsh

```bash
sudo apt update  
sudo apt install zsh  
```

### Vérifier l'installation

```bash
zsh --version
```

### Tester Zsh sans l'activer

```bash
zsh
```

Vous entrez dans un shell Zsh temporaire. Tapez `exit` pour revenir à Bash.

### Définir Zsh comme shell par défaut

**Important :** Cette commande changera votre shell par défaut. Vous pouvez toujours revenir à Bash si nécessaire.

```bash
chsh -s $(which zsh)
```

**Vous devrez vous déconnecter et reconnecter pour que le changement prenne effet.**

Après reconnexion, vérifiez :
```bash
echo $SHELL
```

Vous devriez voir : `/usr/bin/zsh` ou `/bin/zsh`

---

## Installation et configuration de Oh My Zsh

### Qu'est-ce que Oh My Zsh ?

**Oh My Zsh** est un framework open-source pour gérer votre configuration Zsh. Il fournit :
- Plus de 300 plugins
- Plus de 150 thèmes
- Des outils de mise à jour automatique
- Une grande communauté active

### Prérequis

Assurez-vous d'avoir installé :
```bash
sudo apt install git curl
```

### Installation

**Méthode recommandée (via curl) :**

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

**Alternative (via wget) :**

```bash
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

### Ce qui se passe lors de l'installation

1. Le script télécharge Oh My Zsh dans `~/.oh-my-zsh`
2. Crée une copie de sauvegarde de votre ancien `.zshrc` (s'il existe)
3. Crée un nouveau `.zshrc` avec une configuration de base
4. Définit Zsh comme shell par défaut (si ce n'est pas déjà fait)

**Vous verrez un magnifique logo ASCII Oh My Zsh !**

### Structure des fichiers

```
~/.oh-my-zsh/
├── themes/          # Tous les thèmes disponibles
├── plugins/         # Tous les plugins disponibles
├── custom/          # Vos personnalisations
│   ├── themes/      # Vos thèmes personnalisés
│   └── plugins/     # Vos plugins personnalisés
└── tools/           # Scripts de mise à jour, etc.

~/.zshrc             # Votre fichier de configuration principal
```

---

## Configuration de base de Oh My Zsh

### Éditer le fichier de configuration

Ouvrez le fichier `.zshrc` :

```bash
nano ~/.zshrc
```

**Sections importantes du fichier :**

```bash
# Chemin vers Oh My Zsh
export ZSH="$HOME/.oh-my-zsh"

# Thème à utiliser
ZSH_THEME="robbyrussell"

# Plugins à charger
plugins=(git)

# Charger Oh My Zsh
source $ZSH/oh-my-zsh.sh
```

### Changer de thème

**Voir tous les thèmes disponibles :**
```bash
ls ~/.oh-my-zsh/themes/
```

**Ou visitez :** [Thèmes Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)

**Pour changer de thème :**
1. Éditez `~/.zshrc`
2. Modifiez la ligne `ZSH_THEME="nom-du-theme"`
3. Sauvegardez
4. Rechargez la configuration : `source ~/.zshrc`

### Thèmes populaires recommandés

**1. robbyrussell** (par défaut)
- Minimaliste et rapide
- Affiche le dossier actuel et la branche Git
```bash
ZSH_THEME="robbyrussell"
```

**2. agnoster**
- Très populaire et informatif
- Utilise des symboles Powerline (nécessite une police spéciale)
- Affiche utilisateur, dossier, Git, statut
```bash
ZSH_THEME="agnoster"
```

**3. powerlevel10k** (externe, à installer séparément)
- Le thème le plus puissant et personnalisable
- Rapide et riche en fonctionnalités
- Configuration interactive

**4. af-magic**
- Coloré et informatif
- Affiche l'heure, le chemin, Git
```bash
ZSH_THEME="af-magic"
```

**5. jonathan**
- Minimaliste avec horodatage
- Affiche l'heure de chaque commande
```bash
ZSH_THEME="jonathan"
```

**6. bira**
- Design unique avec deux lignes
- Beaucoup d'informations sans être surchargé
```bash
ZSH_THEME="bira"
```

### Tester un thème aléatoire

Si vous ne savez pas quel thème choisir :
```bash
ZSH_THEME="random"
```

À chaque ouverture de terminal, un thème différent sera utilisé. Quand vous en trouvez un que vous aimez, notez son nom affiché et configurez-le.

---

## Installer Powerlevel10k (thème recommandé)

Powerlevel10k est le thème le plus avancé et personnalisable pour Zsh.

### Installation

**1. Cloner le dépôt :**
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

**2. Activer le thème :**
Éditez `~/.zshrc` :
```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

**3. Installer une police Nerd Font (requis) :**

Les polices Nerd Fonts contiennent tous les symboles et icônes nécessaires.

```bash
# Créer le dossier des polices s'il n'existe pas
mkdir -p ~/.local/share/fonts

# Télécharger une police (exemple : MesloLGS NF)
cd ~/.local/share/fonts  
wget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf  
wget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf  
wget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf  
wget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf  

# Mettre à jour le cache des polices
fc-cache -fv
```

**4. Configurer votre terminal pour utiliser la police :**
- Ouvrez votre terminal
- Préférences → Apparence → Police
- Sélectionnez **"MesloLGS NF Regular"** (ou la police installée)

**5. Redémarrer le terminal et lancer la configuration :**

```bash
source ~/.zshrc
```

### Assistant de configuration Powerlevel10k

Lors du premier lancement, un assistant interactif apparaît :

**Questions principales :**

1. **Voyez-vous l'icône en forme de losange ?** (Pour tester les symboles)
   - Répondez selon ce que vous voyez

2. **Voyez-vous l'icône de cadenas ?**
   - Idem

3. **Tous les symboles s'affichent correctement ?**
   - Si oui, continuez. Sinon, réinstallez la police.

4. **Style de prompt :**
   - **Lean** : Minimaliste, sur une ligne
   - **Classic** : Style traditionnel
   - **Rainbow** : Coloré avec segments
   - **Pure** : Inspiré de Pure prompt

5. **Encodage de caractères :** Unicode

6. **Afficher l'heure actuelle ?** Oui/Non

7. **Style des séparateurs :** Angles, rond, etc.

8. **Têtes de branche Git :** Formes variées

9. **Espacement :** Compact ou espacé

10. **Icônes :** Beaucoup ou peu

11. **Flux du prompt :** Concis ou détaillé

12. **Activer le mode instant prompt ?** Oui (recommandé)

**À la fin :** Votre prompt sera magnifiquement configuré !

### Reconfigurer Powerlevel10k

Si vous voulez changer vos choix plus tard :
```bash
p10k configure
```

---

## Plugins Oh My Zsh essentiels

Les plugins ajoutent des fonctionnalités à votre shell.

### Activer des plugins

Éditez `~/.zshrc` et modifiez la ligne `plugins=()` :

```bash
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
  sudo
  web-search
  jsontools
  colored-man-pages
)
```

**Important :** Rechargez après modification :
```bash
source ~/.zshrc
```

### Plugins intégrés (déjà installés)

**1. git**
- Ajoute des alias Git pratiques
- Exemples : `gst` (git status), `ga` (git add), `gc` (git commit)

**2. sudo**
- Appuyez sur `Esc` deux fois pour ajouter `sudo` devant la dernière commande
- Très utile quand vous oubliez sudo

**3. web-search**
- Recherche Google depuis le terminal
- Exemple : `google "linux mint"`
- Autres : `duckduckgo`, `github`, `stackoverflow`

**4. colored-man-pages**
- Pages de manuel colorées (plus lisibles)

**5. extract**
- Commande universelle pour extraire toute archive
- `extract fichier.zip`, `extract fichier.tar.gz`, etc.

**6. command-not-found**
- Suggère des paquets à installer si une commande n'existe pas

**7. history**
- Alias pour l'historique : `h` (historique), `hs mot` (recherche)

**8. jsontools**
- Outils pour travailler avec JSON
- `pp_json` pour formater du JSON

**9. docker** (si vous utilisez Docker)
- Autocomplétion pour Docker

**10. npm** / **yarn** (si vous développez en Node.js)
- Autocomplétion pour npm et yarn

### Plugins externes à installer

Certains plugins très utiles doivent être installés séparément.

#### 1. zsh-autosuggestions

**Fonction :** Suggestions basées sur votre historique (texte gris que vous pouvez accepter)

**Installation :**
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

**Activation :**
Ajoutez dans `~/.zshrc` :
```bash
plugins=(... zsh-autosuggestions)
```

**Usage :**
- Tapez une commande
- Une suggestion grise apparaît
- Appuyez sur `→` (flèche droite) pour l'accepter

#### 2. zsh-syntax-highlighting

**Fonction :** Coloration syntaxique en temps réel des commandes

**Installation :**
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

**Activation :**
```bash
plugins=(... zsh-syntax-highlighting)
```

**Ce qu'il fait :**
- Commandes valides : vertes
- Commandes invalides : rouges
- Chemins existants : soulignés

#### 3. zsh-completions

**Fonction :** Autocomplétion améliorée pour de nombreuses commandes

**Installation :**
```bash
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions
```

**Activation :**
Ajoutez dans `~/.zshrc` avant `source $ZSH/oh-my-zsh.sh` :
```bash
fpath+=${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions/src
```

Puis dans plugins :
```bash
plugins=(... zsh-completions)
```

---

## Starship : L'alternative moderne

Starship est un prompt universel, rapide et minimaliste qui fonctionne avec n'importe quel shell.

### Pourquoi choisir Starship ?

**Avantages :**
- **Rapide** : Écrit en Rust, très performant
- **Universel** : Fonctionne avec Bash, Zsh, Fish, PowerShell...
- **Simple** : Configuration en TOML (facile à lire)
- **Moderne** : Design épuré par défaut
- **Informations contextuelles** : Détecte automatiquement Git, langages, etc.

**Peut être utilisé :**
- Seul avec Bash (sans installer Zsh)
- Avec Zsh à la place d'un thème Oh My Zsh
- En combinaison avec Oh My Zsh (remplace juste le prompt)

### Installation

**Méthode 1 : Via le script d'installation (recommandée)**

```bash
curl -sS https://starship.rs/install.sh | sh
```

**Méthode 2 : Via les gestionnaires de paquets**

```bash
# Via cargo (si vous avez Rust installé)
cargo install starship --locked

# Via snap
sudo snap install starship
```

### Configuration pour Bash

Si vous utilisez Bash (shell par défaut), ajoutez à la fin de `~/.bashrc` :

```bash
eval "$(starship init bash)"
```

Puis rechargez :
```bash
source ~/.bashrc
```

### Configuration pour Zsh

Si vous utilisez Zsh (avec ou sans Oh My Zsh), ajoutez à la fin de `~/.zshrc` :

```bash
eval "$(starship init zsh)"
```

**Note :** Si vous utilisez Oh My Zsh, Starship remplacera le thème. Commentez la ligne `ZSH_THEME=` dans `.zshrc` ou laissez-la (Starship aura la priorité).

Puis rechargez :
```bash
source ~/.zshrc
```

### Premier lancement

Après configuration, ouvrez un nouveau terminal. Vous verrez un prompt minimaliste et élégant !

**Ce que Starship affiche par défaut :**
- Dossier courant
- Branche Git (si dans un dépôt)
- Langage du projet détecté (Python, Node.js, Rust, etc.)
- Statut Git (fichiers modifiés, etc.)
- Temps d'exécution (si > 2 secondes)

---

## Personnaliser Starship

### Fichier de configuration

Starship utilise un fichier de configuration au format **TOML**.

**Créer le fichier de configuration :**

```bash
mkdir -p ~/.config  
touch ~/.config/starship.toml  
```

**Éditer :**
```bash
nano ~/.config/starship.toml
```

### Configurations populaires

#### Configuration minimaliste

```toml
# Format du prompt
format = """
$username\
$hostname\
$directory\
$git_branch\
$git_status\
$character"""

[character]
success_symbol = "[➜](bold green)"  
error_symbol = "[✗](bold red)"  

[directory]
truncation_length = 3  
truncate_to_repo = true  
```

#### Configuration avec icônes

```toml
format = """
$username\
$hostname\
$directory\
$git_branch\
$git_status\
$python\
$nodejs\
$rust\
$golang\
$php\
$docker_context\
$character"""

[character]
success_symbol = "[❯](bold green)"  
error_symbol = "[❯](bold red)"  

[directory]
style = "bold cyan"  
truncation_length = 4  
truncate_to_repo = true  

[git_branch]
symbol = " "  
style = "bold purple"  

[git_status]
style = "bold red"  
conflicted = "🏳"  
ahead = "⇡${count}"  
behind = "⇣${count}"  
diverged = "⇕⇡${ahead_count}⇣${behind_count}"  
untracked = "🤷"  
stashed = "📦"  
modified = "📝"  
staged = '[++\($count\)](green)'  
renamed = "👅"  
deleted = "🗑"  

[python]
symbol = " "  
style = "bold yellow"  

[nodejs]
symbol = " "  
style = "bold green"  

[rust]
symbol = " "  
style = "bold orange"  
```

#### Configuration deux lignes

```toml
format = """
[┌─](bold green)$username$hostname$directory$git_branch$git_status
[└─](bold green)$character"""

[character]
success_symbol = "[❯](bold green)"  
error_symbol = "[❯](bold red)"  
```

#### Configuration complète et colorée

```toml
format = """
[╭─](bold green)$username@$hostname in $directory $git_branch$git_status
[╰─](bold green)$character"""

[username]
style_user = "bold yellow"  
style_root = "bold red"  
show_always = true  

[hostname]
ssh_only = false  
style = "bold yellow"  

[directory]
style = "bold cyan"  
truncation_length = 3  
truncate_to_repo = true  

[git_branch]
symbol = " "  
style = "bold purple"  

[git_status]
style = "bold red"  
ahead = "⇡${count}"  
diverged = "⇕⇡${ahead_count}⇣${behind_count}"  
behind = "⇣${count}"  
```

### Modules disponibles

Starship détecte automatiquement de nombreux contextes :

**Langages de programmation :**
- Python, Node.js, Rust, Go, PHP, Ruby, Java, etc.

**Outils de développement :**
- Git, Docker, Kubernetes, Terraform, etc.

**Environnements :**
- Python venv, Node version, etc.

**Système :**
- Batterie, temps d'exécution, code d'erreur, etc.

**Exemple de configuration avec modules :**

```toml
[python]
symbol = "🐍 "  
pyenv_version_name = true  

[nodejs]
symbol = "⬢ "  
format = "via [$symbol($version )]($style)"  

[docker_context]
symbol = "🐳 "  
format = "via [$symbol$context]($style) "  

[battery]
full_symbol = "🔋 "  
charging_symbol = "⚡️ "  
discharging_symbol = "💀 "  

[[battery.display]]
threshold = 10  
style = "bold red"  

[[battery.display]]
threshold = 30  
style = "bold yellow"  
```

### Presets Starship

Starship propose des configurations prédéfinies (presets).

**Voir les presets :**
[Starship Presets](https://starship.rs/presets/)

**Exemple : Preset Nerd Font Symbols**

```bash
starship preset nerd-font-symbols -o ~/.config/starship.toml
```

**Autres presets populaires :**
- `bracketed-segments` : Segments entre crochets
- `plain-text-symbols` : Sans icônes spéciales
- `no-runtime-versions` : Cache les versions
- `pastel-powerline` : Style Powerline avec couleurs pastel

---

## Polices avec icônes (Nerd Fonts)

Pour afficher correctement les symboles et icônes, vous avez besoin d'une police Nerd Font.

### Qu'est-ce qu'une Nerd Font ?

Les **Nerd Fonts** sont des polices patchées avec des milliers d'icônes supplémentaires :
- Icônes de fichiers et dossiers
- Logos de langages de programmation
- Symboles Git
- Icônes système
- Symboles Powerline

### Installation de Nerd Fonts

**Méthode 1 : Téléchargement manuel**

1. Visitez [Nerd Fonts](https://www.nerdfonts.com/)
2. Téléchargez une police (recommandations : FiraCode, JetBrainsMono, Hack, Meslo)
3. Extrayez le fichier `.zip`
4. Copiez les fichiers `.ttf` dans `~/.local/share/fonts/`
5. Mettez à jour le cache : `fc-cache -fv`

**Méthode 2 : Via script**

```bash
# Créer le dossier
mkdir -p ~/.local/share/fonts

# Télécharger et installer FiraCode Nerd Font
cd ~/.local/share/fonts  
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/FiraCode.zip  
unzip FiraCode.zip  
rm FiraCode.zip  

# Mettre à jour le cache
fc-cache -fv
```

**Méthode 3 : Toutes les polices (grand téléchargement)**

```bash
git clone --depth 1 https://github.com/ryanoasis/nerd-fonts.git  
cd nerd-fonts  
./install.sh
```

### Polices Nerd Font recommandées

**1. FiraCode Nerd Font**
- Excellente pour le code
- Ligatures (symboles combinés)
- Très lisible

**2. JetBrainsMono Nerd Font**
- Créée pour les développeurs
- Ligatures
- Hauteur de ligne optimisée

**3. Hack Nerd Font**
- Simple et claire
- Bonne pour les petites tailles

**4. MesloLGS NF**
- Recommandée par Powerlevel10k
- Complète et bien testée

**5. Cascadia Code**
- Police de Microsoft
- Moderne et élégante

### Configurer le terminal pour utiliser une Nerd Font

**GNOME Terminal / MATE Terminal :**
1. Édition → Préférences
2. Sélectionnez votre profil
3. Onglet "Texte"
4. Décochez "Utiliser la police du système"
5. Cliquez sur "Police"
6. Sélectionnez votre Nerd Font (ex: "FiraCode Nerd Font Regular")
7. Taille : 11 ou 12 (selon préférence)

**Xfce Terminal :**
1. Édition → Préférences
2. Apparence
3. Police → Sélectionnez votre Nerd Font

**Terminator :**
1. Clic droit → Préférences
2. Profils
3. Police personnalisée → Sélectionnez Nerd Font

---

## Alias et fonctions personnalisés

Les alias et fonctions vous font gagner énormément de temps.

### Alias de base

Les alias sont des raccourcis pour des commandes.

**Ajouter des alias :**

Éditez `~/.zshrc` (ou `~/.bashrc` si vous utilisez Bash) :

```bash
# Alias système
alias ll='ls -alF'  
alias la='ls -A'  
alias l='ls -CF'  
alias ..='cd ..'  
alias ...='cd ../..'  
alias ....='cd ../../..'  

# Alias de sécurité
alias rm='rm -i'  
alias cp='cp -i'  
alias mv='mv -i'  

# Alias de productivité
alias update='sudo apt update && sudo apt upgrade'  
alias install='sudo apt install'  
alias remove='sudo apt remove'  
alias search='apt search'  

# Alias Git
alias gs='git status'  
alias ga='git add'  
alias gc='git commit'  
alias gp='git push'  
alias gl='git log --oneline --graph'  

# Alias réseau
alias myip='curl ifconfig.me'  
alias ports='netstat -tulanp'  

# Alias système
alias meminfo='free -m -l -t'  
alias cpuinfo='lscpu'  
alias diskspace='df -h'  

# Alias navigation rapide
alias home='cd ~'  
alias docs='cd ~/Documents'  
alias dl='cd ~/Téléchargements'  
alias dev='cd ~/Développement'  
```

**Recharger la configuration :**
```bash
source ~/.zshrc
```

### Fonctions personnalisées

Les fonctions sont plus puissantes que les alias car elles peuvent prendre des paramètres.

**Exemples de fonctions utiles :**

```bash
# Créer un dossier et y entrer directement
mkcd() {
    mkdir -p "$1" && cd "$1"
}
# Usage: mkcd mon-nouveau-dossier

# Extraire n'importe quelle archive
extract() {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar e $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)     echo "'$1' ne peut pas être extrait" ;;
        esac
    else
        echo "'$1' n'est pas un fichier valide"
    fi
}
# Usage: extract fichier.zip

# Rechercher un processus
psg() {
    ps aux | grep -v grep | grep -i -e VSZ -e $1
}
# Usage: psg firefox

# Créer une sauvegarde d'un fichier
backup() {
    cp "$1" "$1.backup-$(date +%Y%m%d-%H%M%S)"
}
# Usage: backup fichier.txt

# Afficher les fichiers les plus volumineux
bigfiles() {
    du -h --max-depth=1 | sort -hr | head -n 10
}

# Calculatrice rapide
calc() {
    echo "scale=3; $*" | bc -l
}
# Usage: calc 5*7+3
```

### Organiser vos alias et fonctions

Pour garder `.zshrc` propre, créez des fichiers séparés :

**Créer un fichier pour les alias :**
```bash
nano ~/.zsh_aliases
```

**Créer un fichier pour les fonctions :**
```bash
nano ~/.zsh_functions
```

**Charger ces fichiers depuis `.zshrc` :**

Ajoutez dans `~/.zshrc` :
```bash
# Charger les alias
if [ -f ~/.zsh_aliases ]; then
    source ~/.zsh_aliases
fi

# Charger les fonctions
if [ -f ~/.zsh_functions ]; then
    source ~/.zsh_functions
fi
```

---

## Couleurs et thèmes du terminal

### Personnaliser les couleurs

**Couleurs de base du terminal :**

La plupart des terminaux permettent de personnaliser :
- Couleur de fond
- Couleur du texte
- Palette de 16 couleurs
- Couleurs des liens

**Accéder aux paramètres (GNOME Terminal) :**
1. Édition → Préférences
2. Profils → Couleurs
3. Décochez "Utiliser les couleurs du thème système"
4. Personnalisez :
   - Texte et fond
   - Couleurs de la palette
   - Couleur du curseur

### Schémas de couleurs populaires

**1. Dracula**
- Thème sombre très populaire
- Couleurs violettes et roses
- Doux pour les yeux

**2. Gruvbox**
- Palette rétro et chaleureuse
- Variantes clair et sombre

**3. Nord**
- Couleurs froides (bleus, gris)
- Élégant et professionnel

**4. Solarized**
- Scientifiquement conçu pour réduire la fatigue
- Variantes clair et sombre

**5. One Dark**
- Inspiré d'Atom
- Moderne et équilibré

### Installer un thème de terminal

**Exemple : Installer Dracula pour GNOME Terminal**

```bash
# Installer dconf-cli si nécessaire
sudo apt install dconf-cli

# Cloner le thème
git clone https://github.com/dracula/gnome-terminal  
cd gnome-terminal  

# Installer
./install.sh
```

Puis dans Terminal → Préférences → Profils, sélectionnez "Dracula".

### Gogh : Collection de thèmes

**Gogh** est une collection de plus de 250 thèmes pour terminal.

**Installation et usage :**

```bash
bash -c "$(curl -sLo- https://git.io/vQgMr)"
```

Suivez les instructions interactives pour choisir et installer un thème.

---

## Configuration avancée de Zsh

### Historique amélioré

Ajoutez dans `~/.zshrc` :

```bash
# Taille de l'historique
HISTSIZE=10000  
SAVEHIST=10000  
HISTFILE=~/.zsh_history  

# Options d'historique
setopt HIST_IGNORE_ALL_DUPS  # Pas de doublons  
setopt HIST_FIND_NO_DUPS     # Pas de doublons dans la recherche  
setopt HIST_SAVE_NO_DUPS     # Pas de doublons sauvegardés  
setopt HIST_REDUCE_BLANKS    # Supprime les espaces inutiles  
setopt SHARE_HISTORY         # Partage l'historique entre sessions  
setopt APPEND_HISTORY        # Ajoute à l'historique (ne remplace pas)  
```

### Autocomplétion avancée

```bash
# Autocomplétion améliorée
autoload -Uz compinit  
compinit  

# Options de complétion
zstyle ':completion:*' menu select  
zstyle ':completion:*' matcher-list 'm:{a-zA-Z}={A-Za-z}'  
zstyle ':completion:*' list-colors "${(s.:.)LS_COLORS}"  
```

### Navigation intelligente

```bash
# Correction automatique
setopt CORRECT  
setopt CORRECT_ALL  

# Navigation cd améliorée
setopt AUTO_CD              # Tape juste le nom du dossier pour y aller  
setopt AUTO_PUSHD           # cd ajoute au stack  
setopt PUSHD_IGNORE_DUPS    # Pas de doublons dans le stack  
setopt PUSHD_SILENT         # Pas de message  

# Glob amélioré
setopt EXTENDED_GLOB
```

### Variables d'environnement

Définir des variables utiles dans `~/.zshrc` :

```bash
# Éditeur par défaut
export EDITOR='nano'  
export VISUAL='nano'  

# Couleurs pour ls
export LS_COLORS='di=34:ln=35:so=32:pi=33:ex=31:bd=34;46:cd=34;43:su=30;41:sg=30;46:tw=30;42:ow=30;43'

# Couleurs pour less (man pages)
export LESS_TERMCAP_mb=$'\e[1;32m'  
export LESS_TERMCAP_md=$'\e[1;32m'  
export LESS_TERMCAP_me=$'\e[0m'  
export LESS_TERMCAP_se=$'\e[0m'  
export LESS_TERMCAP_so=$'\e[01;33m'  
export LESS_TERMCAP_ue=$'\e[0m'  
export LESS_TERMCAP_us=$'\e[1;4;31m'  
```

---

## Comparaison : Oh My Zsh vs Starship vs Bash

### Tableau comparatif

| Aspect | Bash | Oh My Zsh | Starship |
|--------|------|-----------|----------|
| **Installation** | Préinstallé | Facile | Très facile |
| **Vitesse** | Rapide | Moyen | Très rapide |
| **Personnalisation** | Manuelle | Thèmes/plugins | Configuration TOML |
| **Courbe d'apprentissage** | Faible | Moyenne | Faible |
| **Communauté** | Énorme | Très grande | Croissante |
| **Plugins** | Manuels | 300+ | Modules intégrés |
| **Compatibilité** | Universel | Zsh uniquement | Multi-shell |

### Quelle option choisir ?

**Choisissez Bash (shell par défaut) si :**
- Vous débutez totalement
- Vous voulez la compatibilité maximale
- Vous préférez la simplicité
- Vous n'avez pas besoin de fonctionnalités avancées

**Choisissez Oh My Zsh si :**
- Vous voulez un maximum de plugins
- Vous aimez personnaliser en profondeur
- Vous cherchez une grande communauté
- Vous ne craignez pas une configuration plus complexe

**Choisissez Starship si :**
- Vous voulez quelque chose de moderne et rapide
- Vous préférez une configuration simple (TOML)
- Vous voulez pouvoir changer de shell facilement
- Vous aimez le minimalisme

**Combinaison recommandée pour débutants :**
- **Zsh + Oh My Zsh + plugins essentiels** (autosuggestions, syntax-highlighting)
- **OU : Bash + Starship** (si vous voulez rester simple)

**Combinaison recommandée pour utilisateurs avancés :**
- **Zsh + Oh My Zsh + Powerlevel10k**
- **OU : Zsh + Starship** (plus rapide)

---

## Astuces et raccourcis utiles

### Raccourcis Zsh essentiels

**Navigation :**
- `Ctrl + A` : Début de ligne
- `Ctrl + E` : Fin de ligne
- `Ctrl + ←` / `Ctrl + →` : Mot précédent/suivant
- `Ctrl + U` : Supprimer tout avant le curseur
- `Ctrl + K` : Supprimer tout après le curseur
- `Ctrl + W` : Supprimer le mot précédent

**Historique :**
- `↑` / `↓` : Commandes précédentes/suivantes
- `Ctrl + R` : Recherche dans l'historique
- `!!` : Répéter la dernière commande
- `!$` : Dernier argument de la dernière commande

**Autocomplétion :**
- `Tab` : Compléter
- `Tab Tab` : Afficher toutes les possibilités

### Commandes Zsh spéciales

```bash
# Expansion de globbing
ls **/*.txt           # Tous les .txt récursivement  
ls *.{jpg,png}        # Tous les jpg et png  
ls file<1-10>.txt     # file1.txt à file10.txt  

# Corrections
cd /usr/lcoal/bin     # Zsh propose: /usr/local/bin ?

# Stack de dossiers
dirs                  # Voir le stack  
pushd /chemin         # Aller dans /chemin et empiler  
popd                  # Revenir au dossier précédent  
```

---

## Dépannage

### Problèmes courants

**1. Les symboles ne s'affichent pas correctement**

**Solution :**
- Installez une Nerd Font
- Configurez votre terminal pour l'utiliser
- Vérifiez que la police est bien installée : `fc-list | grep Nerd`

**2. Zsh est lent au démarrage**

**Solutions :**
- Désactivez des plugins non essentiels
- Utilisez le profiling :
  ```bash
  time zsh -i -c exit
  ```
- Utilisez `zsh-defer` pour charger des plugins en différé

**3. L'autocomplétion ne fonctionne pas**

**Solution :**
```bash
# Reconstruire le cache
rm ~/.zcompdump*  
compinit  
```

**4. "Command not found" après installation**

**Solution :**
```bash
# Recharger la configuration
source ~/.zshrc

# Vérifier le PATH
echo $PATH
```

**5. Conflit entre Powerlevel10k et Starship**

**Solution :**
- Choisissez l'un ou l'autre
- Pour Powerlevel10k : Commentez `eval "$(starship init zsh)"`
- Pour Starship : Mettez `ZSH_THEME=""` dans `.zshrc`

**6. Retourner à Bash**

Si vous voulez revenir à Bash :
```bash
chsh -s $(which bash)
```

Puis déconnectez-vous et reconnectez-vous.

---

## Configuration complète recommandée pour débutants

Voici une configuration `.zshrc` complète et commentée, parfaite pour débuter :

```bash
# ============================================
# CONFIGURATION ZSH POUR DÉBUTANTS
# ============================================

# Chemin vers Oh My Zsh
export ZSH="$HOME/.oh-my-zsh"

# Thème (choisissez-en un)
# ZSH_THEME="robbyrussell"              # Simple
# ZSH_THEME="agnoster"                  # Riche (nécessite Nerd Font)
ZSH_THEME="powerlevel10k/powerlevel10k" # Recommandé (nécessite Nerd Font)

# Plugins
plugins=(
  git                      # Alias Git
  zsh-autosuggestions      # Suggestions intelligentes
  zsh-syntax-highlighting  # Coloration syntaxique
  sudo                     # Esc Esc pour ajouter sudo
  extract                  # Extraction universelle
  colored-man-pages        # Pages man colorées
  command-not-found        # Suggestions de paquets
)

# Charger Oh My Zsh
source $ZSH/oh-my-zsh.sh

# ============================================
# HISTORIQUE
# ============================================
HISTSIZE=10000  
SAVEHIST=10000  
HISTFILE=~/.zsh_history  
setopt HIST_IGNORE_ALL_DUPS  
setopt SHARE_HISTORY  

# ============================================
# ALIAS
# ============================================

# Navigation
alias ..='cd ..'  
alias ...='cd ../..'  
alias ....='cd ../../..'  

# Listings
alias ll='ls -alF'  
alias la='ls -A'  
alias l='ls -CF'  

# Sécurité
alias rm='rm -i'  
alias cp='cp -i'  
alias mv='mv -i'  

# Système
alias update='sudo apt update && sudo apt upgrade'  
alias install='sudo apt install'  
alias search='apt search'  

# Git
alias gs='git status'  
alias ga='git add'  
alias gc='git commit'  
alias gp='git push'  
alias gl='git log --oneline --graph'  

# Réseau
alias myip='curl ifconfig.me'

# ============================================
# FONCTIONS
# ============================================

# Créer un dossier et y entrer
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Extraire n'importe quelle archive
extract() {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar e $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)     echo "Format non reconnu" ;;
        esac
    else
        echo "Fichier invalide"
    fi
}

# ============================================
# STARSHIP (optionnel, décommentez pour l'utiliser)
# ============================================
# eval "$(starship init zsh)"

# ============================================
# POWERLEVEL10K INSTANT PROMPT
# ============================================
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh
```

---

## Aller plus loin

### Terminaux alternatifs

Une fois à l'aise, explorez d'autres terminaux :

**Alacritty :**
- Le terminal le plus rapide (GPU-accelerated)
- Configuration en YAML
- Minimaliste

**Kitty :**
- Rapide et riche en fonctionnalités
- Support d'images dans le terminal
- Split windows natif

**Terminator :**
- Splits multiples
- Layout sauvegardables
- Parfait pour le multitasking

### Multiplexeurs de terminal

**Tmux / Screen :**
- Sessions persistantes
- Multiples fenêtres et panneaux
- Détachement/rattachement
- Parfait pour les serveurs distants

### Outils CLI modernes

Remplacez les outils classiques par des versions modernes :

```bash
# bat : un 'cat' amélioré avec coloration syntaxique
sudo apt install bat

# exa : un 'ls' moderne
cargo install exa

# fd : un 'find' plus rapide
sudo apt install fd-find

# ripgrep : un 'grep' ultra-rapide
sudo apt install ripgrep

# htop/btop : 'top' amélioré
sudo apt install htop
```

---

## Résumé

Dans ce chapitre, vous avez appris :

- ✅ La différence entre terminal et shell
- ✅ Comment installer et configurer Zsh
- ✅ Comment installer et utiliser Oh My Zsh
- ✅ Les meilleurs plugins pour Oh My Zsh
- ✅ Comment installer et configurer Powerlevel10k
- ✅ Comment installer et utiliser Starship
- ✅ L'importance des Nerd Fonts et comment les installer
- ✅ Comment créer des alias et fonctions utiles
- ✅ Comment personnaliser les couleurs du terminal
- ✅ Les raccourcis et astuces pour être plus productif
- ✅ Comment dépanner les problèmes courants

Un terminal bien configuré transforme votre expérience Linux. Prenez le temps d'expérimenter avec différents thèmes, plugins et configurations jusqu'à trouver le setup parfait pour votre workflow !

---

⏭️ [Curseurs et polices système](/16-personnalisation-avancee/06-curseurs-et-polices-systeme.md)
