🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 18.3 Surveillance des ressources (htop, btop, moniteur système)

## Introduction

Imaginez votre ordinateur comme une ville : le processeur (CPU) est la centrale électrique, la mémoire vive (RAM) est le réseau routier, et les programmes sont les habitants qui utilisent ces infrastructures. Pour bien gérer cette ville, vous avez besoin de **tableaux de bord** qui vous montrent en temps réel ce qui se passe.

**Dans ce chapitre, vous apprendrez à :**
- Surveiller l'utilisation du CPU, de la RAM et du disque
- Identifier les programmes qui ralentissent votre système
- Comprendre et interpréter les différentes métriques
- Utiliser les outils de surveillance : Moniteur système, htop et btop
- Gérer les processus problématiques (programmes qui ne répondent plus)

**Pourquoi c'est important ?**
- Comprendre pourquoi votre ordinateur ralentit
- Détecter les applications gourmandes en ressources
- Arrêter proprement les programmes bloqués
- Optimiser les performances de votre système

---

## Comprendre les ressources système

Avant d'utiliser les outils de surveillance, comprenons ce que nous allons surveiller.

### Le CPU (Processeur)

Le **CPU** (Central Processing Unit) est le cerveau de votre ordinateur. Il exécute toutes les tâches.

**Mesures importantes :**
- **Utilisation en %** : de 0% (inactif) à 100% (saturé)
- **Nombre de cœurs** : processeurs modernes ont 2, 4, 8 cœurs ou plus
- **Charge moyenne** (load average) : nombre de tâches en attente

**Exemples concrets :**
- **10-30% d'utilisation** : navigation web, bureautique → normal
- **50-70% d'utilisation** : montage vidéo, jeux → normal
- **100% constant** : encodage vidéo, compilation → peut être normal
- **100% au repos** : problème ! Un processus monopolise le CPU

**Processeurs multi-cœurs :**
Si vous avez 4 cœurs, 100% signifie qu'UN cœur est saturé (25% du total). Un logiciel peut utiliser 400% maximum (tous les cœurs à fond).

### La RAM (Mémoire vive)

La **RAM** stocke temporairement les données des programmes en cours d'exécution.

**Mesures importantes :**
- **Utilisée** : mémoire occupée par les applications
- **Disponible** : mémoire libre pour de nouveaux programmes
- **Buffers/Cache** : mémoire utilisée intelligemment par Linux pour accélérer le système
- **Swap** : espace disque utilisé comme extension de RAM (LENT !)

**Exemples concrets :**

Ordinateur avec 8 Go de RAM :
- **2 Go utilisés** : navigation légère → excellent
- **5 Go utilisés** : Firefox avec 50 onglets, LibreOffice, musique → normal
- **7.5 Go utilisés + swap** : trop de programmes ouverts → ralentissements
- **Swap important (>1 Go)** : RAM saturée → il faut fermer des applications ou ajouter de la RAM

**Idée reçue à corriger :**
"Linux utilise toute ma RAM !" → **FAUX**. Linux utilise intelligemment la RAM libre comme cache pour accélérer le système. Ce n'est PAS un problème. Regardez plutôt la RAM "disponible" (available).

### Le Swap (Mémoire d'échange)

Le **swap** est un espace sur votre disque dur/SSD qui sert d'extension à la RAM quand celle-ci est pleine.

**Caractéristiques :**
- Beaucoup plus lent que la RAM (jusqu'à 1000x plus lent avec un HDD)
- Utilisation occasionnelle = normal
- Utilisation intensive = problème de RAM insuffisante

**Quand s'inquiéter :**
- Swap > 500 Mo constamment → envisagez d'ajouter de la RAM
- Swap qui augmente rapidement → fermez des applications

### Les processus

Un **processus** est un programme en cours d'exécution. Chaque application peut lancer plusieurs processus.

**Informations importantes :**
- **PID** (Process ID) : numéro unique d'identification
- **Utilisateur** : qui a lancé le processus (vous, root, système)
- **Priorité** : importance du processus (niceness)
- **État** : en cours (Running), en attente (Sleeping), zombie, etc.

**Types de processus :**
- **Interactifs** : Firefox, LibreOffice → haute priorité
- **Services système** : NetworkManager, cron → arrière-plan
- **Processus zombie** : terminé mais non nettoyé → généralement inoffensif

---

## Le Moniteur système (Interface graphique)

Linux Mint inclut un **Moniteur système** graphique, similaire au Gestionnaire des tâches de Windows.

### Ouvrir le Moniteur système

**Méthode 1 : Menu**
1. Menu > **Administration** > **Moniteur système**

**Méthode 2 : Recherche**
1. Appuyez sur `Super` (touche Windows)
2. Tapez "moniteur système"
3. Cliquez sur l'icône

**Méthode 3 : Terminal**
```bash
gnome-system-monitor &
```

**Méthode 4 : Raccourci clavier**
`Ctrl + Alt + Suppr` (selon la configuration)

### Onglet "Processus"

Cet onglet affiche tous les programmes en cours d'exécution.

**Colonnes principales :**

| Colonne | Signification |
|---------|---------------|
| **Nom du processus** | Nom du programme |
| **État** | En cours d'exécution, en veille, arrêté, zombie |
| **% CPU** | Pourcentage d'utilisation du processeur |
| **Mémoire** | RAM consommée en Mo ou Go |
| **ID** | Numéro unique du processus (PID) |
| **Utilisateur** | Qui a lancé le processus |

**Astuces d'utilisation :**

1. **Trier par consommation CPU** : cliquez sur la colonne "% CPU"
2. **Trier par consommation RAM** : cliquez sur la colonne "Mémoire"
3. **Rechercher un processus** : tapez son nom dans la barre de recherche

**Filtres de vue :**
- **Tous les processus** : affiche tout, y compris les processus système
- **Mes processus** : uniquement vos applications
- **Processus actifs** : seulement ceux qui utilisent du CPU

**Recommandation pour débutants :** Utilisez "Processus actifs" pour voir facilement ce qui consomme des ressources.

### Onglet "Ressources"

Cet onglet affiche des **graphiques en temps réel** de l'utilisation des ressources.

**Informations affichées :**

1. **Historique du processeur**
   - Graphique de l'utilisation CPU sur les dernières 60 secondes
   - Une ligne par cœur de processeur (ou une ligne totale selon la vue)
   - Pourcentage d'utilisation actuel

2. **Historique de la mémoire et du swap**
   - Graphique de la RAM utilisée/disponible
   - Graphique du swap (s'il est utilisé)
   - Valeurs en Mo/Go

3. **Historique du réseau**
   - Débit de réception (téléchargement)
   - Débit d'envoi (upload)
   - Vitesse en Ko/s ou Mo/s

**Utilisation pratique :**
Laissez cet onglet ouvert pendant que vous utilisez votre ordinateur. Si tout devient lent, regardez quel graphique explose !

### Onglet "Systèmes de fichiers"

Affiche l'utilisation de l'espace disque sur vos partitions.

**Informations par partition :**
- **Périphérique** : nom technique (/dev/sda1, /dev/nvme0n1p2, etc.)
- **Répertoire** : point de montage (/, /home, etc.)
- **Type** : système de fichiers (ext4, ntfs, vfat)
- **Total** : capacité totale
- **Libre** : espace disponible
- **Utilisé** : espace occupé

**Alerte :** Si une partition dépasse 90% d'utilisation, pensez à faire du nettoyage (voir section 18.1).

### Gérer les processus depuis le Moniteur système

#### Arrêter un processus (kill)

Quand une application ne répond plus (figée, bloquée) :

1. Trouvez le processus dans la liste
2. **Clic droit** sur le processus
3. Choisissez l'une de ces options :

**Options d'arrêt (du plus doux au plus brutal) :**

1. **Terminer le processus** (SIGTERM)
   - Demande poliment au programme de se fermer
   - Permet au programme de sauvegarder ses données
   - **À essayer en premier**

2. **Tuer le processus** (SIGKILL)
   - Force la fermeture immédiate
   - Le programme n'a pas le temps de sauvegarder
   - **Uniquement si "Terminer" ne fonctionne pas**

3. **Arrêter le processus** (SIGSTOP)
   - Met en pause le processus (il reste en mémoire)
   - Rare d'avoir besoin de cette option

**Exemple pratique :**
Firefox est bloqué et ne répond plus :
1. Ouvrez le Moniteur système
2. Recherchez "firefox"
3. Clic droit > **Terminer le processus**
4. Si rien ne se passe après 10 secondes > **Tuer le processus**

#### Modifier la priorité d'un processus

Vous pouvez augmenter ou diminuer la priorité d'un processus.

1. Clic droit sur le processus
2. **Changer la priorité**
3. Choisissez :
   - **Très haute** : le processus aura priorité sur tout
   - **Haute** : priorité importante
   - **Normale** : par défaut
   - **Basse** : le processus s'exécute quand les autres n'ont rien à faire
   - **Très basse** : le processus ralentit les autres au minimum

**Cas d'usage :**
- Encodage vidéo long → mettre en "Basse" pour continuer à utiliser l'ordinateur
- Jeu vidéo qui lag → mettre en "Haute" (mais attention aux autres applications)

**⚠️ Attention :** Ne mettez jamais un processus système en priorité "Très basse", cela peut bloquer votre système.

---

## htop : Le moniteur système en mode terminal

**htop** est un outil de surveillance en ligne de commande, plus puissant et plus esthétique que le `top` traditionnel.

### Pourquoi utiliser htop ?

**Avantages par rapport au Moniteur système graphique :**
- Plus léger (consomme moins de ressources)
- Accessible à distance via SSH
- Interface colorée et intuitive
- Navigation au clavier ultra-rapide
- Tri et filtrage plus flexibles
- Affichage détaillé de tous les processus

### Installation de htop

htop n'est pas toujours installé par défaut.

**Vérifier s'il est installé :**
```bash
htop --version
```

**Si absent, installez-le :**
```bash
sudo apt install htop
```

### Lancer htop

Ouvrez un terminal et tapez :
```bash
htop
```

Vous verrez une interface colorée en plein écran.

### Comprendre l'interface htop

#### En-tête (partie supérieure)

**Barres de CPU** (une par cœur)
```
1 [||||||||||||||||||||||||||||||||        65.2%]
2 [||||||||||||||                          32.5%]
3 [||||||||||||||||||||||||||||||||||||    78.9%]
4 [||||||||                                18.6%]
```

**Code couleur des barres CPU :**
- **Vert** : processus normaux utilisateur
- **Rouge** : processus système (kernel)
- **Bleu** : processus de basse priorité (nice)
- **Orange** : IRQ (interruptions matérielles)

**Informations mémoire :**
```
Mem [|||||||||||||||||||                    3.85G/15.6G]
Swp [                                        0K/2.00G]
```

- **Mem** : RAM utilisée / RAM totale
- **Swp** : Swap utilisé / Swap total

**Autres informations :**
```
Tasks: 247, 893 thr; 2 running
Load average: 1.23 0.98 0.76
Uptime: 2 days, 14:23:45
```

- **Tasks** : nombre de processus (247) et threads (893)
- **running** : processus actifs en ce moment
- **Load average** : charge moyenne sur 1, 5 et 15 minutes
- **Uptime** : temps depuis le dernier démarrage

#### Liste des processus (partie inférieure)

Affiche tous les processus en cours avec :
- **PID** : identifiant du processus
- **USER** : utilisateur qui a lancé le processus
- **PRI** : priorité
- **NI** : valeur "nice" (gentillesse, -20 à 19)
- **VIRT** : mémoire virtuelle totale
- **RES** : mémoire physique (RAM) réellement utilisée
- **SHR** : mémoire partagée avec d'autres processus
- **S** : état (R=running, S=sleeping, Z=zombie, etc.)
- **CPU%** : pourcentage d'utilisation CPU
- **MEM%** : pourcentage d'utilisation RAM
- **TIME+** : temps CPU total utilisé
- **Command** : nom du programme

### Navigation dans htop

**Touches essentielles :**

| Touche | Action |
|--------|--------|
| `↑` `↓` | Naviguer entre les processus |
| `F5` ou `t` | Vue en arbre (voir les processus parents/enfants) |
| `F6` ou `>` | Choisir le critère de tri |
| `F4` ou `\` | Filtrer par nom |
| `F3` ou `/` | Rechercher un processus |
| `F9` ou `k` | Envoyer un signal (kill) |
| `F10` ou `q` | Quitter htop |
| `Space` | Sélectionner/déselectionner un processus |
| `u` | Filtrer par utilisateur |
| `I` | Inverser l'ordre de tri |
| `H` | Masquer/afficher les threads |

### Trier les processus dans htop

**Pour trier par consommation CPU :**
1. Appuyez sur `F6`
2. Sélectionnez "PERCENT_CPU"
3. Appuyez sur `Entrée`

Les processus les plus gourmands en CPU apparaissent en haut.

**Pour trier par consommation RAM :**
1. Appuyez sur `F6`
2. Sélectionnez "PERCENT_MEM"
3. Appuyez sur `Entrée`

**Raccourcis rapides :**
- `P` : tri par CPU (le plus courant)
- `M` : tri par mémoire
- `T` : tri par temps CPU total

### Rechercher un processus spécifique

**Exemple :** Trouver tous les processus Firefox

1. Appuyez sur `F4` (ou `\`)
2. Tapez "firefox"
3. Appuyez sur `Entrée`

Seuls les processus contenant "firefox" s'affichent.

**Pour annuler le filtre :**
1. Appuyez à nouveau sur `F4`
2. Effacez le texte
3. Appuyez sur `Entrée`

### Arrêter un processus avec htop

**Méthode complète :**

1. Naviguez jusqu'au processus avec `↑` ou `↓`
2. Appuyez sur `F9` (ou `k` pour "kill")
3. Choisissez le signal :
   - **15 SIGTERM** : fermeture propre (par défaut, recommandé)
   - **9 SIGKILL** : fermeture forcée (en dernier recours)
4. Appuyez sur `Entrée`

**Raccourci ultra-rapide :**
Positionnez-vous sur le processus et appuyez sur `F9` puis `Entrée` (utilise SIGTERM par défaut).

### Changer la priorité d'un processus

1. Sélectionnez le processus
2. Appuyez sur `F7` (diminuer la priorité, augmente "nice")
3. Ou appuyez sur `F8` (augmenter la priorité, diminue "nice")

**Rappel sur "nice" :**
- Nice = -20 : priorité maximale (pas gentil avec les autres)
- Nice = 0 : priorité normale
- Nice = 19 : priorité minimale (très gentil, laisse passer les autres)

### Affichage en arbre (mode tree)

Pour voir la relation parent/enfant entre processus :

1. Appuyez sur `F5` (ou `t`)

**Exemple d'affichage :**
```
firefox (PID 1234)
  ├─ Web Content (PID 1235)
  ├─ Web Content (PID 1236)
  └─ WebExtensions (PID 1237)
```

Cela montre que Firefox (processus parent) a lancé plusieurs processus enfants.

**Pour revenir à la vue normale :**
Appuyez à nouveau sur `F5`.

### Personnaliser htop

**Accéder aux paramètres :**
Appuyez sur `F2` pour ouvrir le menu de configuration.

**Options intéressantes :**

1. **Display options** :
   - Cocher "Tree view" pour démarrer en mode arbre
   - Cocher "Hide kernel threads" pour masquer les processus kernel (plus lisible pour débutants)
   - Cocher "Show custom thread names" pour voir les noms des threads

2. **Meters** (gauges dans l'en-tête) :
   - Personnalisez l'affichage des barres CPU, RAM, etc.
   - Ajoutez/supprimez des indicateurs

3. **Colors** :
   - Choisissez un jeu de couleurs (Monochrome, Noir et blanc, MC, Broken Gray)

**Sauvegarder la configuration :**
Appuyez sur `F10` pour quitter et sauvegarder automatiquement dans `~/.config/htop/htoprc`.

---

## btop : Le moniteur système moderne et esthétique

**btop** (ou btop++) est un moniteur système encore plus moderne et visuellement impressionnant que htop.

### Pourquoi utiliser btop ?

**Avantages par rapport à htop :**
- Interface graphique superbe avec des graphiques en ASCII art
- Affichage simultané : CPU, RAM, réseau, disques, processus
- Thèmes personnalisables
- Détection automatique de la souris dans le terminal
- Plus d'informations visibles d'un coup d'œil
- Graphiques historiques pour chaque ressource

**Inconvénient :**
Consomme un peu plus de ressources que htop (mais reste léger).

### Installation de btop

**btop** n'est généralement pas préinstallé.

**Installation depuis les dépôts (si disponible) :**
```bash
sudo apt install btop
```

**Si btop n'est pas dans les dépôts officiels (version ancienne de Mint) :**

```bash
# Ajouter le dépôt personnel (PPA)
sudo add-apt-repository ppa:bashtop-monitor/bashtop
sudo apt update
sudo apt install btop
```

**Ou installation via snap (si vous l'avez activé) :**
```bash
snap install btop
```

**Vérifier l'installation :**
```bash
btop --version
```

### Lancer btop

Dans un terminal :
```bash
btop
```

Vous verrez une interface complète en plein écran avec :
- Graphiques CPU (en haut à gauche)
- Graphiques RAM/Swap (en haut à droite)
- Réseau (milieu gauche)
- Disques (milieu droite)
- Processus (en bas)

### Comprendre l'interface btop

#### Zone CPU (haut gauche)

Affiche des **graphiques en temps réel** pour chaque cœur de processeur :
- Graphique d'utilisation sur les 60 dernières secondes
- Pourcentage d'utilisation actuel
- Fréquence actuelle (en GHz)
- Température (si disponible)

**Code couleur :**
Généralement un dégradé du bleu (faible utilisation) au rouge (forte utilisation).

#### Zone RAM et Swap (haut droite)

- Graphique de consommation RAM
- RAM utilisée / totale (en Go)
- Graphique Swap
- Détails sur les buffers et cache

#### Zone Réseau (milieu gauche)

- Interface réseau active (WiFi, Ethernet)
- Débit de téléchargement (Download)
- Débit d'upload
- Graphiques historiques

#### Zone Disques (milieu droite)

- Liste de tous les disques et partitions
- Utilisation en lecture/écriture
- Activité en temps réel
- Pourcentage d'utilisation de l'espace

#### Zone Processus (bas)

Liste détaillée des processus avec :
- PID
- Utilisateur
- Priorité
- Threads
- % CPU
- % RAM
- Commande

### Navigation dans btop

**Touches principales :**

| Touche | Action |
|--------|--------|
| `↑` `↓` | Naviguer dans la liste des processus |
| `Esc` | Retour au menu principal |
| `q` | Quitter btop |
| `m` | Afficher le menu complet |
| `f` | Filtrer les processus |
| `p` | Trier par CPU |
| `m` (dans processus) | Trier par RAM |
| `k` | Envoyer un signal kill |
| `t` | Vue en arbre |
| `+` / `-` | Zoom dans les graphiques |

**Souris :**
Si votre terminal le supporte, vous pouvez **cliquer** directement sur les processus et les boutons !

### Thèmes et personnalisation

**Changer de thème :**

1. Lancez btop
2. Appuyez sur `m` pour ouvrir le menu
3. Naviguez jusqu'à "Options"
4. Changez "Color theme"

**Thèmes disponibles :**
- Default
- TTY
- Monokai
- Solarized Dark
- Gruvbox Dark
- Nord
- Et bien d'autres...

**Tester plusieurs thèmes :** Utilisez les flèches pour parcourir, le changement est instantané.

### Arrêter un processus avec btop

1. Naviguez jusqu'au processus avec `↑` `↓`
2. Appuyez sur `k`
3. Choisissez le signal (15 SIGTERM recommandé)
4. Confirmez avec `Entrée`

### Filtrer par utilisateur

Pour voir uniquement vos processus :

1. Appuyez sur `f` (filter)
2. Tapez votre nom d'utilisateur
3. Appuyez sur `Entrée`

---

## Comparaison des outils

| Critère | Moniteur système | htop | btop |
|---------|------------------|------|------|
| **Interface** | Graphique (GUI) | Terminal simple | Terminal moderne |
| **Facilité** | ⭐⭐⭐⭐⭐ Très facile | ⭐⭐⭐⭐ Facile | ⭐⭐⭐⭐ Facile |
| **Ressources utilisées** | Moyen | Faible | Moyen-faible |
| **Graphiques** | Oui, simples | Non | Oui, magnifiques |
| **Vue d'ensemble** | Onglets séparés | Limitée | ⭐ Excellente |
| **Personnalisation** | Limitée | Moyenne | ⭐ Excellente |
| **Accès SSH** | Non | Oui | Oui |
| **Souris** | Oui | Non (clavier) | Oui (si terminal compatible) |

**Recommandation :**
- **Débutants** : Moniteur système (graphique)
- **Utilisateurs avancés** : htop (léger et rapide)
- **Enthousiastes** : btop (beau et complet)

---

## Commandes terminal complémentaires

### La commande top (ancêtre de htop)

**top** est l'outil historique de surveillance, moins convivial mais toujours présent.

```bash
top
```

**Touches utiles dans top :**
- `q` : quitter
- `k` : kill un processus (entrer le PID puis le signal)
- `P` : trier par CPU
- `M` : trier par mémoire
- `h` : aide

**Conseil :** Préférez htop si disponible, beaucoup plus intuitif.

### La commande ps (liste des processus)

**ps** affiche un instantané des processus à un moment donné (pas en temps réel).

**Afficher tous les processus :**
```bash
ps aux
```

**Explication :**
- `a` : tous les processus de tous les utilisateurs
- `u` : format détaillé avec utilisateur
- `x` : inclut les processus sans terminal

**Résultat :**
```
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1 168832 11232 ?        Ss   Nov23   0:05 /sbin/init
root           2  0.0  0.0      0     0 ?        S    Nov23   0:00 [kthreadd]
pierre      1234  5.2  2.3 2843952 378432 ?      Sl   09:15  12:34 /usr/lib/firefox/firefox
```

**Rechercher un processus spécifique :**
```bash
ps aux | grep firefox
```

### La commande pgrep (trouver un PID par nom)

```bash
pgrep firefox
```

Affiche tous les PID des processus contenant "firefox".

**Avec détails :**
```bash
pgrep -a firefox
```

### La commande pidof

Alternative simple pour trouver le PID d'un programme :

```bash
pidof firefox
```

### La commande kill (arrêter un processus)

**Syntaxe de base :**
```bash
kill [signal] PID
```

**Signaux courants :**

| Signal | Numéro | Action | Quand l'utiliser |
|--------|--------|--------|------------------|
| SIGTERM | 15 | Fermeture propre | **En premier** |
| SIGKILL | 9 | Fermeture forcée | Si SIGTERM échoue |
| SIGHUP | 1 | Recharger config | Services |
| SIGSTOP | 19 | Mettre en pause | Rarement |

**Exemples :**

Arrêter proprement Firefox (PID 1234) :
```bash
kill 1234
```
Ou explicitement :
```bash
kill -15 1234
```

Forcer l'arrêt si ça ne répond pas :
```bash
kill -9 1234
```

**Raccourci : killall (par nom)**

Arrêter tous les processus Firefox :
```bash
killall firefox
```

Forcer l'arrêt :
```bash
killall -9 firefox
```

**⚠️ Attention :** `killall` tue TOUS les processus portant ce nom. Soyez sûr de ce que vous faites !

### La commande pkill (kill par nom partiel)

Plus souple que killall :

```bash
pkill firefox
```

**Avec signal spécifique :**
```bash
pkill -9 firefox
```

### La commande nice et renice

**Lancer un programme avec une priorité spécifique :**

```bash
nice -n 10 programme
```

- `-n 10` : priorité basse (gentil avec les autres)
- `-n -10` : priorité haute (nécessite sudo)

**Exemple :** Lancer un encodage vidéo en basse priorité
```bash
nice -n 15 ffmpeg -i video.mp4 output.mp4
```

**Modifier la priorité d'un processus en cours :**

```bash
renice -n 5 -p PID
```

**Exemple :**
```bash
renice -n 10 -p 1234
```

Met le processus 1234 en priorité basse.

---

## Comprendre la charge système (Load Average)

La **charge moyenne** (load average) représente le nombre de processus en attente d'exécution.

**Affichage typique :**
```
load average: 1.23, 0.98, 0.76
```

**Signification :**
- **Premier chiffre** : charge moyenne sur 1 minute
- **Deuxième chiffre** : charge moyenne sur 5 minutes
- **Troisième chiffre** : charge moyenne sur 15 minutes

**Interprétation (pour un processeur 4 cœurs) :**

| Load average | Signification |
|--------------|---------------|
| 0.00 - 2.00 | Système fluide |
| 2.00 - 4.00 | Système chargé mais normal |
| 4.00 - 8.00 | Système surchargé |
| > 8.00 | Système saturé |

**Règle générale :**
Load average < nombre de cœurs = OK

**Voir la load average :**
```bash
uptime
```

Résultat :
```
10:23:45 up 2 days, 14:23,  1 user,  load average: 1.23, 0.98, 0.76
```

---

## Identifier et résoudre les problèmes courants

### Problème : Ordinateur très lent

**Diagnostic :**

1. Ouvrez htop ou btop
2. Regardez :
   - CPU à 100% ? → Identifiez le processus gourmand
   - RAM saturée + Swap utilisé ? → Trop de programmes ouverts
   - Load average élevée ? → Système surchargé

**Solutions :**

**Si un processus monopolise le CPU :**
- Vérifiez si c'est normal (encodage vidéo, compilation)
- Si anormal, arrêtez le processus

**Si la RAM est saturée :**
- Fermez les applications inutiles
- Fermez les onglets de navigateur
- Envisagez d'ajouter de la RAM

### Problème : Un programme ne répond plus

**Symptômes :**
- Fenêtre grisée avec "(Ne répond pas)" dans le titre
- Impossible de cliquer
- Curseur en forme de sablier

**Solution étape par étape :**

1. Attendez 30 secondes (parfois il reprend)
2. Ouvrez htop : `htop`
3. Trouvez le processus (touche `F4` puis tapez le nom)
4. Appuyez sur `F9` puis `Entrée` (SIGTERM)
5. Attendez 10 secondes
6. Si toujours bloqué : `F9` puis choisissez signal `9` (SIGKILL)

**Raccourci rapide :**
```bash
killall -9 nom-du-programme
```

### Problème : Le bureau est lent/laggy

**Causes possibles :**
- Processus en arrière-plan gourmand
- Pilote graphique problématique
- Effets visuels trop lourds

**Diagnostic :**

1. Ouvrez btop ou htop
2. Triez par CPU (`P`)
3. Identifiez les processus utilisant >20% de CPU au repos

**Processus suspects courants :**
- `tracker-miner-fs` : indexation de fichiers (peut être désactivé)
- `baloo_file` : indexation KDE (peut être désactivé)
- Antivirus (si installé)

**Désactiver l'indexation de fichiers (Tracker) :**
```bash
tracker3 daemon --kill
gsettings set org.freedesktop.Tracker3.Miner.Files crawling-interval -2
```

### Problème : Beaucoup de processus zombie

**Qu'est-ce qu'un processus zombie ?**
Un processus terminé mais dont l'entrée n'a pas été nettoyée par son parent.

**Identification dans htop :**
Colonne "S" affiche "Z" (zombie).

**Ce n'est généralement PAS un problème :**
- Les zombies ne consomment pas de ressources (CPU, RAM)
- Ils disparaissent quand le processus parent se termine ou redémarre

**Si vous avez des centaines de zombies :**
1. Trouvez le processus parent (PPID)
2. Redémarrez ce processus parent

---

## Automatisation de la surveillance

### Script d'alerte si CPU > 80%

Créez un script qui vous alerte si le CPU dépasse 80% :

```bash
nano ~/check-cpu.sh
```

Contenu :

```bash
#!/bin/bash

CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')
CPU_INT=${CPU_USAGE%.*}

if [ "$CPU_INT" -gt 80 ]; then
    notify-send "⚠️ Alerte CPU" "Utilisation CPU: ${CPU_INT}%"
    echo "$(date): CPU à ${CPU_INT}%" >> ~/cpu-alerts.log
fi
```

Rendez-le exécutable :
```bash
chmod +x ~/check-cpu.sh
```

**Automatisez avec cron (toutes les 5 minutes) :**
```bash
crontab -e
```

Ajoutez :
```
*/5 * * * * ~/check-cpu.sh
```

### Enregistrer l'utilisation des ressources

Pour analyser rétrospectivement :

```bash
while true; do
    date >> ~/resource-log.txt
    top -bn1 | head -15 >> ~/resource-log.txt
    echo "---" >> ~/resource-log.txt
    sleep 300  # toutes les 5 minutes
done
```

---

## Bonnes pratiques de surveillance

### ✅ À faire régulièrement

1. **Vérifiez l'utilisation RAM** : assurez-vous de ne pas utiliser le swap constamment
2. **Surveillez les processus gourmands** : identifiez les applications problématiques
3. **Contrôlez la température CPU** (laptops) : utilisez `sensors` ou btop
4. **Vérifiez l'espace disque** : évitez la saturation

### ❌ À éviter

1. **Ne tuez jamais** des processus système (root) sans savoir ce qu'ils font
2. **N'utilisez pas** systématiquement `kill -9` : essayez d'abord `kill -15`
3. **Ne vous inquiétez pas** si Linux utilise beaucoup de RAM : c'est normal (cache)
4. **Ne désactivez pas** la surveillance : elle consomme peu de ressources

### 🎯 Objectifs de performance

**Système sain :**
- CPU au repos : < 10%
- RAM disponible : > 20% du total
- Swap utilisé : < 100 Mo (idéalement 0)
- Load average : < nombre de cœurs CPU

**Si ces valeurs sont dépassées :**
- Fermez des applications
- Identifiez les processus problématiques
- Envisagez un upgrade matériel (RAM, SSD)

---

## Outils complémentaires

### glances

Moniteur système qui combine tout : CPU, RAM, disque, réseau, processus.

**Installation :**
```bash
sudo apt install glances
```

**Lancement :**
```bash
glances
```

Interface similaire à btop mais avec plus d'informations techniques.

### nmon

Outil de monitoring orienté serveur.

**Installation :**
```bash
sudo apt install nmon
```

**Lancement :**
```bash
nmon
```

Appuyez sur `c` (CPU), `m` (RAM), `d` (disques) pour activer les vues.

### bashtop

Prédécesseur de btop, écrit en Bash.

**Installation :**
```bash
sudo apt install bashtop
```

**Note :** btop (écrit en C++) est plus rapide et moderne. Préférez btop.

---

## Résumé des commandes essentielles

| Commande | Utilité |
|----------|---------|
| `htop` | Moniteur système terminal complet |
| `btop` | Moniteur système moderne et graphique |
| `top` | Moniteur système basique (préinstallé) |
| `ps aux` | Liste instantanée des processus |
| `pgrep nom` | Trouver le PID d'un processus |
| `kill PID` | Arrêter proprement un processus |
| `kill -9 PID` | Forcer l'arrêt d'un processus |
| `killall nom` | Arrêter tous les processus d'un nom |
| `pkill nom` | Arrêter par nom partiel |
| `nice -n 10 cmd` | Lancer avec priorité basse |
| `renice -n 5 -p PID` | Changer la priorité |
| `uptime` | Voir load average et uptime |

---

## Conclusion

La surveillance des ressources est **essentielle** pour :
- Comprendre le comportement de votre système
- Identifier les ralentissements
- Optimiser les performances
- Gérer les applications problématiques

**Les trois outils à retenir :**

1. **Moniteur système** (GUI) : pour les débutants, simple et visuel
2. **htop** : léger, rapide, parfait pour le terminal
3. **btop** : moderne, complet, magnifique

**Commencez par le Moniteur système**, puis explorez htop quand vous serez à l'aise avec le terminal, et enfin btop pour une expérience optimale.

**Avec ces outils, vous avez le contrôle total sur votre système Linux Mint !** 🚀

---

## Pour aller plus loin

- **Section 18.2** : Gestion des services au démarrage (systemd)
- **Section 18.4** : Optimisation SSD
- **Section 20.1** : Scripts bash pour automatisation
- **Section 23.5** : Problèmes de performance et ralentissements
- **Section 23.7** : Lecture et compréhension des logs

**Documentation :**
- `man htop`
- `man ps`
- `man kill`
- GitHub btop : https://github.com/aristocratos/btop

⏭️ [Optimisation SSD (TRIM, noatime)](/18-maintenance-et-optimisation/04-optimisation-ssd.md)
