🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 16.4 - Conky pour le monitoring visuel

## Introduction

**Conky** est l'un des outils les plus puissants et flexibles pour afficher des informations système directement sur votre bureau Linux. Contrairement aux applets et desklets que nous avons vus précédemment, Conky offre une liberté de personnalisation quasi illimitée et peut afficher pratiquement n'importe quelle information de votre système de manière élégante et personnalisée.

Imaginez pouvoir afficher en temps réel : l'utilisation de votre CPU, la RAM, les températures, les disques durs, la météo, vos emails, les titres de musique en cours de lecture, et bien plus encore... tout cela dans un design entièrement personnalisé que vous créez vous-même !

Dans ce chapitre, nous allons découvrir comment installer, configurer et personnaliser Conky pour créer un bureau vraiment unique et informatif.

---

## Qu'est-ce que Conky ?

### Définition

**Conky** est un moniteur système léger, hautement configurable, qui affiche des informations directement sur votre bureau. Il est :

- **Open source** : Gratuit et librement modifiable
- **Léger** : Consomme très peu de ressources système
- **Flexible** : Presque tout est personnalisable
- **Puissant** : Peut afficher une multitude d'informations

### Différence avec les desklets

**Desklets :**
- Interface graphique pour la configuration
- Limités aux options prédéfinies
- Plus faciles pour les débutants
- Personnalisation limitée

**Conky :**
- Configuration via fichier texte
- Personnalisation illimitée
- Courbe d'apprentissage plus élevée
- Design entièrement libre

### À quoi sert Conky ?

**Utilisations courantes :**

1. **Monitoring système**
   - CPU, RAM, températures
   - Processus actifs
   - Utilisation réseau

2. **Information système**
   - Nom de la machine
   - Système d'exploitation
   - Version du kernel
   - Uptime (temps depuis le démarrage)

3. **Disques et stockage**
   - Espace utilisé/disponible
   - Vitesse de lecture/écriture
   - Montages actifs

4. **Réseau**
   - Adresse IP
   - Vitesse upload/download
   - Connexions actives

5. **Informations externes**
   - Météo
   - Flux RSS
   - Emails non lus
   - Lecture musicale en cours

6. **Horloge et calendrier**
   - Heure et date personnalisées
   - Calendrier mensuel
   - Fuseaux horaires multiples

---

## Installation de Conky

### Installation de base

**Via le gestionnaire de logiciels :**
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez **"conky"**
3. Cliquez sur **Installer**

**Via le terminal (recommandé) :**
```bash
sudo apt update
sudo apt install conky-all
```

**Note :** Nous installons `conky-all` qui contient toutes les fonctionnalités. Il existe aussi `conky-std` (version standard, plus limitée).

### Vérifier l'installation

```bash
conky --version
```

Vous devriez voir quelque chose comme :
```
conky 1.11.6 compiled...
```

### Dépendances optionnelles

Pour des fonctionnalités avancées, vous pouvez installer :

```bash
# Pour l'affichage de la météo
sudo apt install curl jq

# Pour les graphiques et effets
sudo apt install lua5.3

# Pour les informations musicales
sudo apt install audacious
```

---

## Premier lancement de Conky

### Lancer Conky avec la configuration par défaut

Ouvrez un terminal et tapez simplement :

```bash
conky
```

**Ce que vous verrez :**
- Un panneau d'informations apparaît sur votre bureau
- Informations système de base
- Design minimaliste par défaut

**Pour arrêter Conky :**
```bash
killall conky
```

Ou fermez simplement le terminal où vous l'avez lancé.

### Configuration par défaut

Conky utilise un fichier de configuration pour savoir quoi afficher et comment.

**Emplacement du fichier de configuration :**
- Configuration utilisateur : `~/.conkyrc` ou `~/.config/conky/conky.conf`
- Configuration système : `/etc/conky/conky.conf`

**Créer votre première configuration :**

Si le fichier n'existe pas déjà, créez-le :

```bash
mkdir -p ~/.config/conky
conky --print-config > ~/.config/conky/conky.conf
```

Cette commande crée un fichier de configuration avec les paramètres par défaut.

---

## Structure d'un fichier de configuration Conky

Le fichier de configuration Conky se divise en deux parties principales :

### 1. Section Settings (Paramètres)

C'est ici que vous définissez le comportement et l'apparence générale de Conky.

**Exemple de section settings :**

```lua
conky.config = {
    -- Fenêtre et affichage
    alignment = 'top_right',
    background = true,
    border_width = 1,
    cpu_avg_samples = 2,

    -- Comportement
    double_buffer = true,
    no_buffers = true,

    -- Police et texte
    font = 'DejaVu Sans Mono:size=10',

    -- Dimensions
    gap_x = 20,
    gap_y = 60,
    minimum_width = 250,
    minimum_height = 5,

    -- Couleurs
    default_color = 'white',
    default_outline_color = 'black',
    default_shade_color = 'black',

    -- Transparence
    own_window = true,
    own_window_class = 'Conky',
    own_window_type = 'desktop',
    own_window_transparent = true,

    -- Mise à jour
    update_interval = 1.0,

    -- Divers
    use_xft = true,
}
```

### 2. Section TEXT (Contenu)

C'est ici que vous définissez ce qui sera affiché.

**Exemple de section TEXT :**

```lua
conky.text = [[
${color grey}Système:$color $nodename
${color grey}Kernel:$color $kernel
${color grey}Uptime:$color $uptime
$hr
${color grey}CPU:$color $cpu%
${cpubar 4}
${color grey}RAM:$color $mem/$memmax - $memperc%
${membar 4}
${color grey}Swap:$color $swap/$swapmax - $swapperc%
${swapbar 4}
$hr
${color grey}Disque /:$color ${fs_used /}/${fs_size /}
${fs_bar 6 /}
]]
```

---

## Paramètres importants expliqués

Comprendre les paramètres principaux vous aidera à personnaliser Conky selon vos besoins.

### Positionnement

**alignment** : Position de Conky sur l'écran
```lua
alignment = 'top_left'      -- En haut à gauche
alignment = 'top_right'     -- En haut à droite
alignment = 'top_middle'    -- En haut au centre
alignment = 'bottom_left'   -- En bas à gauche
alignment = 'bottom_right'  -- En bas à droite
alignment = 'middle_left'   -- Au milieu à gauche
alignment = 'middle_right'  -- Au milieu à droite
```

**gap_x et gap_y** : Distance depuis le bord de l'écran
```lua
gap_x = 20,  -- 20 pixels depuis le bord horizontal
gap_y = 60,  -- 60 pixels depuis le bord vertical
```

**minimum_width et minimum_height** : Dimensions minimales
```lua
minimum_width = 250,   -- Largeur minimum 250 pixels
minimum_height = 5,    -- Hauteur minimum 5 pixels
maximum_width = 300,   -- Largeur maximum (optionnel)
```

### Apparence de la fenêtre

**own_window** : Crée une fenêtre propre à Conky
```lua
own_window = true,  -- Active la fenêtre propre
```

**own_window_type** : Type de fenêtre
```lua
own_window_type = 'desktop',  -- Se comporte comme le fond d'écran
own_window_type = 'normal',   -- Fenêtre normale
own_window_type = 'override', -- Ignore le gestionnaire de fenêtres
```

**own_window_transparent** : Transparence
```lua
own_window_transparent = true,   -- Fond transparent
own_window_transparent = false,  -- Fond opaque
```

**own_window_argb_visual** : Transparence moderne (avec valeur alpha)
```lua
own_window_argb_visual = true,
own_window_argb_value = 150,  -- Valeur de 0 (transparent) à 255 (opaque)
```

### Couleurs et polices

**default_color** : Couleur par défaut du texte
```lua
default_color = 'white',
default_color = '#FFFFFF',  -- Format hexadécimal
default_color = 'cyan',
```

**font** : Police par défaut
```lua
font = 'DejaVu Sans Mono:size=10',
font = 'Ubuntu:size=12:bold',
font = 'Monospace:size=9',
```

**Autres couleurs :**
```lua
color0 = 'white',      -- Couleur personnalisée 0
color1 = 'cyan',       -- Couleur personnalisée 1
color2 = 'yellow',     -- Couleur personnalisée 2
```

### Mise à jour et performance

**update_interval** : Fréquence de rafraîchissement (en secondes)
```lua
update_interval = 1.0,    -- Mise à jour chaque seconde
update_interval = 2.0,    -- Mise à jour toutes les 2 secondes
update_interval = 0.5,    -- Mise à jour toutes les 0.5 secondes
```

**cpu_avg_samples** : Nombre d'échantillons pour lisser l'affichage CPU
```lua
cpu_avg_samples = 2,  -- Moyenne sur 2 échantillons (recommandé)
```

**double_buffer** : Évite le scintillement
```lua
double_buffer = true,  -- Active le double buffering (recommandé)
```

---

## Variables Conky : Afficher des informations

Conky utilise des **variables** pour afficher des informations. Voici les plus utiles :

### Informations système

```lua
$nodename       -- Nom de la machine
$kernel         -- Version du kernel
$machine        -- Architecture (x86_64, etc.)
$sysname        -- Nom du système (Linux)
$uptime         -- Temps depuis le démarrage
$uptime_short   -- Version courte de uptime
```

**Exemple d'utilisation :**
```lua
Système: $nodename
Kernel: $kernel
Uptime: $uptime
```

### CPU

```lua
$cpu            -- Utilisation CPU totale (%)
$cpu cpu1       -- Utilisation du cœur 1
$cpu cpu2       -- Utilisation du cœur 2
${cpubar}       -- Barre d'utilisation CPU
${cpubar cpu1}  -- Barre pour le cœur 1
${cpugraph}     -- Graphique CPU
$freq           -- Fréquence du CPU (MHz)
$freq_g         -- Fréquence du CPU (GHz)
```

**Exemple d'utilisation :**
```lua
CPU: $cpu%
${cpubar 4}
Core 1: $cpu cpu1%  Core 2: $cpu cpu2%
```

### Mémoire RAM

```lua
$mem            -- Mémoire utilisée
$memmax         -- Mémoire totale
$memperc        -- Pourcentage utilisé
$memfree        -- Mémoire libre
${membar}       -- Barre de mémoire
${memgraph}     -- Graphique de mémoire
```

**Exemple d'utilisation :**
```lua
RAM: $mem / $memmax - $memperc%
${membar 4}
```

### Swap

```lua
$swap           -- Swap utilisé
$swapmax        -- Swap total
$swapperc       -- Pourcentage de swap utilisé
${swapbar}      -- Barre de swap
```

### Disques et systèmes de fichiers

```lua
${fs_used /}         -- Espace utilisé sur /
${fs_free /}         -- Espace libre sur /
${fs_size /}         -- Taille totale de /
${fs_used_perc /}    -- Pourcentage utilisé sur /
${fs_bar /}          -- Barre d'utilisation de /
${diskio}            -- Vitesse disque
${diskio_read}       -- Vitesse de lecture
${diskio_write}      -- Vitesse d'écriture
```

**Exemple d'utilisation :**
```lua
Disque /: ${fs_used /} / ${fs_size /}
${fs_bar 6 /}
Disque /home: ${fs_used /home} / ${fs_size /home}
${fs_bar 6 /home}
```

### Réseau

```lua
${addr eth0}         -- Adresse IP eth0
${addr wlan0}        -- Adresse IP WiFi
${downspeed eth0}    -- Vitesse de download
${upspeed eth0}      -- Vitesse d'upload
${downspeedgraph eth0}   -- Graphique download
${upspeedgraph eth0}     -- Graphique upload
${totaldown eth0}    -- Total téléchargé
${totalup eth0}      -- Total uploadé
```

**Note :** Remplacez `eth0` par le nom de votre interface réseau. Pour le trouver :
```bash
ip link show
```

**Exemple d'utilisation :**
```lua
IP: ${addr wlan0}
Download: ${downspeed wlan0}
Upload: ${upspeed wlan0}
```

### Processus

```lua
${top name 1}        -- Nom du processus #1 (qui consomme le plus)
${top pid 1}         -- PID du processus #1
${top cpu 1}         -- % CPU du processus #1
${top mem 1}         -- % RAM du processus #1

${top_mem name 1}    -- Processus qui consomme le plus de RAM
${top_mem pid 1}
${top_mem mem 1}
```

**Exemple d'utilisation :**
```lua
Processus        CPU%    RAM%
${top name 1}    ${top cpu 1}    ${top mem 1}
${top name 2}    ${top cpu 2}    ${top mem 2}
${top name 3}    ${top cpu 3}    ${top mem 3}
```

### Temps et date

```lua
${time %H:%M:%S}     -- Heure (HH:MM:SS)
${time %d/%m/%Y}     -- Date (JJ/MM/AAAA)
${time %A}           -- Jour de la semaine
${time %B}           -- Mois
${time %Y}           -- Année
```

**Formats personnalisés :**
```lua
${time %H:%M}        -- 14:30
${time %d %b %Y}     -- 29 Nov 2024
${time %A %d %B}     -- Vendredi 29 Novembre
```

### Batterie (pour laptops)

```lua
${battery_percent}   -- Pourcentage de batterie
${battery_time}      -- Temps restant
${battery_short}     -- Statut court
${battery_bar}       -- Barre de batterie
```

### Températures

```lua
${hwmon 0 temp 1}    -- Température du capteur 1
${acpitemp}          -- Température ACPI
${nvidia temp}       -- Température GPU NVIDIA (si installé)
```

**Trouver vos capteurs :**
```bash
sensors
```

---

## Mise en forme du texte

Conky supporte diverses options de formatage pour rendre l'affichage plus agréable.

### Couleurs

**Changer de couleur :**
```lua
${color red}Texte en rouge$color
${color cyan}Texte en cyan$color
${color #FF0000}Texte en rouge (hex)$color
${color0}Utilise la couleur0 définie$color
```

**Exemple :**
```lua
${color grey}CPU:$color $cpu%
${color red}Température:$color ${hwmon 0 temp 1}°C
```

### Alignement

```lua
${alignr}Texte aligné à droite
${alignc}Texte centré
${offset 50}Décale de 50 pixels à droite
```

### Police

```lua
${font Ubuntu:size=14}Grand texte$font
${font Monospace:bold:size=12}Gras$font
${font Sans:italic:size=10}Italique$font
```

### Séparateurs et espaces

```lua
$hr                  -- Ligne horizontale
${voffset 10}        -- Espace vertical de 10 pixels
${goto 100}          -- Va à la position x=100
```

### Barres de progression

```lua
${cpubar}            -- Barre par défaut
${cpubar 8}          -- Barre de hauteur 8
${cpubar 4,200}      -- Barre de hauteur 4 et largeur 200
${membar 6}          -- Barre de mémoire hauteur 6
```

### Graphiques

```lua
${cpugraph}          -- Graphique CPU
${cpugraph 40,200}   -- Graphique hauteur 40, largeur 200
${memgraph 30,150 FF0000 00FF00}  -- Avec couleurs personnalisées
${downspeedgraph wlan0 40,200}    -- Graphique réseau
```

---

## Exemples de configurations complètes

### Configuration simple et élégante

**Fichier : ~/.config/conky/conky.conf**

```lua
conky.config = {
    alignment = 'top_right',
    background = true,
    border_width = 1,
    cpu_avg_samples = 2,
    default_color = 'white',
    default_outline_color = 'white',
    default_shade_color = 'white',
    double_buffer = true,
    draw_borders = false,
    draw_graph_borders = true,
    draw_outline = false,
    draw_shades = false,
    use_xft = true,
    font = 'DejaVu Sans Mono:size=10',
    gap_x = 20,
    gap_y = 60,
    minimum_height = 5,
    minimum_width = 250,
    net_avg_samples = 2,
    no_buffers = true,
    out_to_console = false,
    out_to_stderr = false,
    extra_newline = false,
    own_window = true,
    own_window_class = 'Conky',
    own_window_type = 'desktop',
    own_window_transparent = true,
    stippled_borders = 0,
    update_interval = 1.0,
    uppercase = false,
    use_spacer = 'none',
    show_graph_scale = false,
    show_graph_range = false
}

conky.text = [[
${color grey}Informations Système
${color grey}$hr
${color grey}Nom:$color $nodename
${color grey}Kernel:$color $kernel
${color grey}Uptime:$color $uptime

${color grey}Processeur
${color grey}$hr
${color grey}Utilisation:$color $cpu%
${cpubar 4}
${color grey}Fréquence:$color $freq_g GHz

${color grey}Mémoire
${color grey}$hr
${color grey}RAM:$color $mem/$memmax - $memperc%
${membar 4}
${color grey}Swap:$color $swap/$swapmax - $swapperc%
${swapbar 4}

${color grey}Disques
${color grey}$hr
${color grey}Racine /:$color ${fs_used /}/${fs_size /}
${fs_bar 6 /}
${color grey}Home:$color ${fs_used /home}/${fs_size /home}
${fs_bar 6 /home}

${color grey}Réseau
${color grey}$hr
${color grey}IP:$color ${addr wlan0}
${color grey}Download:$color ${downspeed wlan0}
${color grey}Upload:$color ${upspeed wlan0}

${color grey}Processus (CPU)
${color grey}$hr
${color grey}${top name 1} ${alignr}${top cpu 1}%
${color grey}${top name 2} ${alignr}${top cpu 2}%
${color grey}${top name 3} ${alignr}${top cpu 3}%
]]
```

### Configuration avec graphiques

```lua
conky.config = {
    alignment = 'top_right',
    background = true,
    border_width = 1,
    cpu_avg_samples = 2,
    default_color = 'cyan',
    default_outline_color = 'white',
    default_shade_color = 'white',
    double_buffer = true,
    draw_borders = false,
    draw_graph_borders = true,
    draw_outline = false,
    draw_shades = false,
    use_xft = true,
    font = 'Ubuntu:size=10',
    gap_x = 30,
    gap_y = 60,
    minimum_height = 5,
    minimum_width = 300,
    net_avg_samples = 2,
    no_buffers = true,
    out_to_console = false,
    out_to_stderr = false,
    extra_newline = false,
    own_window = true,
    own_window_class = 'Conky',
    own_window_type = 'desktop',
    own_window_transparent = true,
    own_window_argb_visual = true,
    own_window_argb_value = 180,
    stippled_borders = 0,
    update_interval = 1.0,
    uppercase = false,
    use_spacer = 'none',
    show_graph_scale = false,
    show_graph_range = false
}

conky.text = [[
${font Ubuntu:bold:size=12}${color cyan}SYSTÈME${color}${font}
$hr
${color grey}Nom:$color $nodename
${color grey}Uptime:$color $uptime_short

${font Ubuntu:bold:size=12}${color cyan}PROCESSEUR${color}${font}
$hr
${color grey}Usage:$color $cpu% ${alignr}${color grey}Freq:$color $freq_g GHz
${cpugraph 40,300 00ff00 ff0000}
${color grey}Core 1:$color ${cpu cpu1}% ${cpubar cpu1 6}
${color grey}Core 2:$color ${cpu cpu2}% ${cpubar cpu2 6}
${color grey}Core 3:$color ${cpu cpu3}% ${cpubar cpu3 6}
${color grey}Core 4:$color ${cpu cpu4}% ${cpubar cpu4 6}

${font Ubuntu:bold:size=12}${color cyan}MÉMOIRE${color}${font}
$hr
${color grey}RAM:$color $mem/$memmax ${alignr}$memperc%
${memgraph 40,300 00ff00 ff0000}
${membar 6}

${font Ubuntu:bold:size=12}${color cyan}RÉSEAU${color}${font}
$hr
${color grey}IP:$color ${addr wlan0}
${color grey}Download:$color ${downspeed wlan0}/s ${alignr}${totaldown wlan0}
${downspeedgraph wlan0 30,300 00ff00 ff0000}
${color grey}Upload:$color ${upspeed wlan0}/s ${alignr}${totalup wlan0}
${upspeedgraph wlan0 30,300 ff0000 00ff00}

${font Ubuntu:bold:size=12}${color cyan}TOP PROCESSUS${color}${font}
$hr
${color grey}${top name 1}${alignr}${top cpu 1}%
${color grey}${top name 2}${alignr}${top cpu 2}%
${color grey}${top name 3}${alignr}${top cpu 3}%
]]
```

### Configuration minimaliste

```lua
conky.config = {
    alignment = 'top_left',
    background = true,
    border_width = 0,
    cpu_avg_samples = 2,
    default_color = 'white',
    double_buffer = true,
    draw_borders = false,
    draw_graph_borders = false,
    draw_outline = false,
    draw_shades = false,
    use_xft = true,
    font = 'Monospace:size=9',
    gap_x = 20,
    gap_y = 40,
    minimum_height = 5,
    minimum_width = 200,
    no_buffers = true,
    own_window = true,
    own_window_type = 'desktop',
    own_window_transparent = true,
    update_interval = 2.0,
    uppercase = false,
}

conky.text = [[
${time %H:%M}
${time %A %d %B}

CPU  $cpu%
RAM  $memperc%
/    ${fs_used_perc /}%

${downspeed wlan0} ↓
${upspeed wlan0} ↑
]]
```

---

## Lancer Conky automatiquement au démarrage

### Méthode 1 : Applications au démarrage (GUI)

1. Ouvrez **Menu** → **Préférences** → **Applications au démarrage**
2. Cliquez sur **"Ajouter"** ou **"+"**
3. Remplissez :
   - **Nom :** Conky
   - **Commande :** `conky -d -p 10`
   - **Commentaire :** Monitoring système
4. Cochez la case pour l'activer
5. Cliquez sur **"Ajouter"**

**Explication de la commande :**
- `-d` : Lance en mode daemon (arrière-plan)
- `-p 10` : Attend 10 secondes avant de démarrer (laisse le temps au système de charger)

### Méthode 2 : Script de démarrage

Créez un script dans `~/.config/autostart/` :

```bash
nano ~/.config/autostart/conky.desktop
```

Contenu du fichier :
```
[Desktop Entry]
Type=Application
Name=Conky
Exec=sh -c 'sleep 10 && conky -d'
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
```

Sauvegardez et fermez (`Ctrl+O`, `Entrée`, `Ctrl+X`).

### Méthode 3 : Plusieurs configurations Conky

Si vous avez plusieurs fichiers de configuration :

**Script de lancement :**
```bash
nano ~/start-conky.sh
```

Contenu :
```bash
#!/bin/bash
sleep 10
conky -c ~/.config/conky/conky1.conf &
sleep 2
conky -c ~/.config/conky/conky2.conf &
sleep 2
conky -c ~/.config/conky/conky3.conf &
```

Rendez-le exécutable :
```bash
chmod +x ~/start-conky.sh
```

Ajoutez dans Applications au démarrage avec la commande :
```
~/start-conky.sh
```

---

## Thèmes Conky prêts à l'emploi

Au lieu de créer votre propre configuration, vous pouvez utiliser des thèmes existants.

### Où trouver des thèmes ?

**Sites populaires :**
- [DeviantArt - Conky](https://www.deviantart.com/tag/conky)
- [GitHub - Conky Themes](https://github.com/topics/conky-theme)
- [Conky Configurations sur Reddit](https://www.reddit.com/r/Conky/)

### Installer un thème

**Étapes générales :**

1. **Téléchargez le thème** (généralement un fichier `.zip` ou dépôt Git)

2. **Extrayez les fichiers**
   ```bash
   unzip conky-theme.zip -d ~/.config/conky/mon-theme
   ```

3. **Lisez le README**
   - Vérifiez les dépendances
   - Notez les polices requises
   - Lisez les instructions spécifiques

4. **Installez les polices nécessaires** (si besoin)
   ```bash
   # Exemple : copier des polices
   cp mon-theme/fonts/* ~/.local/share/fonts/
   fc-cache -fv
   ```

5. **Lancez le thème**
   ```bash
   conky -c ~/.config/conky/mon-theme/conky.conf
   ```

### Thèmes populaires recommandés

**1. Conky-Vision**
- Design moderne et élégant
- Graphiques colorés
- Facile à personnaliser

**2. Conky-Grapes**
- Style minimaliste
- Couleurs douces
- Parfait pour les petits écrans

**3. Conky Seamod**
- Design professionnel
- Nombreuses informations
- Très complet

**4. Harmattan**
- Style météo/horloge
- Design sophistiqué
- Nécessite une configuration météo

**5. gotham**
- Thème sombre
- Style cyberpunk
- Graphiques néon

---

## Personnalisation avancée

### Utiliser Lua pour des fonctionnalités avancées

Conky supporte des scripts Lua pour des personnalisations poussées.

**Exemple simple : Anneaux de monitoring**

De nombreux thèmes utilisent Lua pour créer des anneaux circulaires.

**Structure :**
```lua
conky.config = {
    lua_load = '~/.config/conky/rings.lua',
    lua_draw_hook_pre = 'ring_stats',
    -- ... autres paramètres
}
```

**Note :** La création de scripts Lua dépasse le cadre de ce tutoriel débutant, mais sachez que c'est possible pour des designs très avancés.

### Afficher la météo

**Utiliser un service météo :**

Vous aurez besoin :
1. D'une clé API (gratuite) d'un service météo comme OpenWeatherMap
2. D'un script qui récupère les données

**Exemple basique avec curl :**

```lua
${execi 600 curl -s "wttr.in/Paris?format=3"}
```

Cette commande affiche la météo pour Paris, mise à jour toutes les 10 minutes (600 secondes).

**Format plus détaillé :**
```lua
${color grey}Météo Paris:
${execi 600 curl -s "wttr.in/Paris?format=%c+%t+%w"}
```

### Afficher les informations musicales

**Avec Audacious :**
```lua
${if_running audacious}
${color grey}Lecture en cours:
${color}${audacious_title}
${color grey}Artiste:$color ${audacious_artist}
${else}
${color grey}Aucune musique${endif}
```

**Avec Spotify (via playerctl) :**
```bash
# Installer playerctl
sudo apt install playerctl
```

Dans Conky :
```lua
${execi 2 playerctl metadata --format "{{artist}} - {{title}}"}
```

### Icônes et symboles

Utilisez des polices d'icônes pour un design moderne :

**Installer Font Awesome :**
```bash
sudo apt install fonts-font-awesome
```

**Utiliser dans Conky :**
```lua
${font FontAwesome:size=16}${font} CPU: $cpu%
${font FontAwesome:size=16}${font} RAM: $memperc%
```

**Symboles Unicode courants :**
- CPU:
- RAM:
- Disque:
- Réseau:
- Download: ↓
- Upload: ↑
- Température: 🌡

---

## Optimisation et performances

### Conseils pour réduire l'impact système

**1. Augmentez l'intervalle de mise à jour**
```lua
update_interval = 2.0,  -- Au lieu de 1.0
```

**2. Réduisez le nombre d'échantillons**
```lua
cpu_avg_samples = 2,  -- Ne pas mettre plus de 4
net_avg_samples = 2,
```

**3. Limitez les commandes externes**
```lua
${execi 600 ...}  -- Utilisez execi avec de longs intervalles
```

**4. Désactivez ce que vous n'utilisez pas**
- Supprimez les graphiques si non nécessaires
- Limitez le nombre de processus affichés
- Enlevez les informations redondantes

**5. Utilisez double_buffer**
```lua
double_buffer = true,  -- Réduit le scintillement et améliore les performances
```

### Mesurer l'impact de Conky

**Voir l'utilisation CPU de Conky :**
```bash
top -p $(pgrep -d',' conky)
```

**Usage typique :**
- Configuration simple : 0.5-1% CPU
- Configuration avec graphiques : 1-2% CPU
- Configuration complexe avec Lua : 2-4% CPU

---

## Dépannage

### Conky ne démarre pas

**Vérifiez les erreurs :**
```bash
conky -c ~/.config/conky/conky.conf
```

Regardez les messages d'erreur dans le terminal.

**Erreurs courantes :**

1. **"Syntax error"** : Erreur dans le fichier de configuration
   - Vérifiez les virgules
   - Vérifiez les crochets `{}` et `[[]]`
   - Vérifiez les guillemets

2. **"Unknown setting"** : Paramètre non reconnu
   - Vérifiez l'orthographe
   - Assurez-vous que le paramètre existe dans votre version

3. **"Can't open display"** : Problème d'affichage X11
   ```bash
   export DISPLAY=:0
   conky
   ```

### Conky s'affiche derrière le bureau

**Solution :**
```lua
own_window_type = 'desktop',  -- Ou 'override'
own_window = true,
```

Si cela ne fonctionne pas :
```lua
own_window_type = 'normal',
own_window_hints = 'undecorated,below,sticky,skip_taskbar,skip_pager',
```

### Texte flou ou mal rendu

**Solution :**
```lua
use_xft = true,
xftalpha = 1.0,
override_utf8_locale = true,
```

**Changez la police :**
```lua
font = 'DejaVu Sans Mono:size=10',  -- Police plus nette
```

### Conky disparaît quand je maximise une fenêtre

**C'est normal si :**
```lua
own_window_type = 'desktop',
```

**Pour qu'il reste visible :**
```lua
own_window_type = 'normal',
own_window_hints = 'undecorated,above,sticky,skip_taskbar,skip_pager',
```

### Les graphiques ne s'affichent pas

**Assurez-vous que :**
```lua
draw_graph_borders = true,
show_graph_scale = false,
show_graph_range = false,
```

**Vérifiez la syntaxe :**
```lua
${cpugraph 40,200}  -- Hauteur 40, largeur 200
```

### Transparence ne fonctionne pas

**Pour transparence moderne :**
```lua
own_window = true,
own_window_type = 'desktop',
own_window_transparent = false,  -- Important!
own_window_argb_visual = true,
own_window_argb_value = 150,  -- 0-255
```

**Pour transparence simple :**
```lua
own_window = true,
own_window_type = 'desktop',
own_window_transparent = true,
```

---

## Cas d'usage et configurations spécialisées

### Pour développeur

```lua
${color grey}GIT STATUS
$hr
${execi 10 cd ~/projet && git branch | grep \* | cut -d ' ' -f2}
${execi 60 cd ~/projet && git status -s | wc -l} fichiers modifiés

${color grey}DOCKER
$hr
${execi 10 docker ps --format "table {{.Names}}" | tail -n +2 | wc -l} conteneurs actifs
```

### Pour gamer

```lua
${color grey}GAMING
$hr
${color grey}GPU:$color ${nvidia gpuutil}%
${color grey}GPU Temp:$color ${nvidia temp}°C
${color grey}VRAM:$color ${nvidia memutil}%
${color grey}FPS:$color ${exec cat /sys/class/drm/card0/fps 2>/dev/null || echo "N/A"}
```

### Pour serveur

```lua
${color grey}SERVEUR
$hr
${color grey}Services actifs:
${if_running apache2}${color green}● Apache$color${else}${color red}○ Apache$color${endif}
${if_running mysql}${color green}● MySQL$color${else}${color red}○ MySQL$color${endif}
${if_running sshd}${color green}● SSH$color${else}${color red}○ SSH$color${endif}

${color grey}Connexions SSH actives:
${color}${execi 30 netstat -tn | grep :22 | wc -l}
```

---

## Ressources et inspiration

### Galeries de configurations

**Reddit :**
- r/unixporn : Configurations visuelles impressionnantes
- r/Conky : Dédié spécifiquement à Conky

**DeviantArt :**
- [DeviantArt Conky Group](https://www.deviantart.com/conkygroup)

**GitHub :**
- Recherchez "conky config" ou "conky theme"

### Documentation officielle

- [Conky Wiki](https://github.com/brndnmtthws/conky/wiki)
- [Liste complète des variables](https://github.com/brndnmtthws/conky/wiki/Configs)
- [Configuration Reference](https://github.com/brndnmtthws/conky/wiki/Configuration-Settings)

### Communautés

**Forums :**
- [Linux Mint Forums - Customization](https://forums.linuxmint.com/)
- [Ubuntu Forums - Desktop Customization](https://ubuntuforums.org/)

**Discord/IRC :**
- Serveurs Discord Linux généralistes
- #conky sur Freenode IRC

---

## Aller plus loin

Après avoir maîtrisé Conky, vous pouvez explorer :

- **Scripts Lua avancés** : Créer des widgets complexes
- **Combinaison avec d'autres outils** : i3status, polybar
- **Conky Manager** : GUI pour gérer plusieurs configurations (non maintenu mais parfois utile)
- **Automatisation** : Changer de configuration selon l'heure ou l'activité

---

## Résumé

Dans ce chapitre, vous avez appris :

- ✅ Ce qu'est Conky et en quoi il diffère des desklets
- ✅ Comment installer et configurer Conky
- ✅ La structure d'un fichier de configuration Conky
- ✅ Les variables principales pour afficher des informations système
- ✅ Comment personnaliser l'apparence avec couleurs, polices et graphiques
- ✅ Comment utiliser des thèmes existants
- ✅ Comment lancer Conky automatiquement au démarrage
- ✅ L'optimisation des performances
- ✅ Le dépannage des problèmes courants
- ✅ Des exemples de configurations pour différents cas d'usage

Conky est un outil incroyablement puissant qui peut transformer votre bureau en un tableau de bord informatif et élégant. Prenez le temps d'expérimenter, de tester différentes configurations, et de créer l'affichage parfait pour vos besoins !

---


⏭️ [Personnalisation du terminal (Oh My Zsh, Starship)](/16-personnalisation-avancee/05-personnalisation-du-terminal.md)
