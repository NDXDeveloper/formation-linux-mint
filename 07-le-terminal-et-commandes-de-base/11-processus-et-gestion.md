🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.11 - Processus et gestion (ps, top, kill)

## Introduction

Quand vous lancez un programme sous Linux (Firefox, un script, une commande), le système crée un **processus**. Savoir gérer les processus est essentiel pour :
- Voir ce qui tourne sur votre système
- Trouver et arrêter les programmes qui plantent
- Optimiser les performances
- Comprendre pourquoi votre ordinateur ralentit
- Résoudre les problèmes de programmes bloqués

**Analogie :** Si votre ordinateur est une cuisine :
- Les **processus** sont les plats en cours de préparation
- Le **CPU** est le chef cuisinier
- La **mémoire (RAM)** est le plan de travail
- **ps** et **top** sont comme regarder dans la cuisine pour voir ce qui se passe
- **kill** est comme arrêter la cuisson d'un plat

Dans ce chapitre, nous allons apprendre à surveiller et contrôler tous les programmes qui tournent sur votre système.

---

## Qu'est-ce qu'un processus ?

### Définition

Un **processus** est une instance d'un programme en cours d'exécution.

**Exemples :**
- Vous ouvrez Firefox → Un processus Firefox est créé
- Vous tapez `ls` dans le terminal → Un processus ls est créé (puis se termine)
- Le système démarre → Des dizaines de processus systèmes sont créés

### Caractéristiques d'un processus

Chaque processus possède :

| Propriété | Description |
|-----------|-------------|
| **PID** | Process ID - Numéro unique du processus |
| **PPID** | Parent Process ID - PID du processus qui l'a créé |
| **Utilisateur** | Propriétaire du processus |
| **État** | Running, Sleeping, Stopped, Zombie |
| **CPU** | Pourcentage d'utilisation du processeur |
| **Mémoire** | Quantité de RAM utilisée |
| **Priorité** | Niveau de priorité (nice value) |
| **TTY** | Terminal associé (si applicable) |

### Les états d'un processus

| État | Code | Description |
|------|------|-------------|
| **Running** | R | En cours d'exécution |
| **Sleeping** | S | En attente (interruptible) |
| **Stopped** | T | Arrêté/Suspendu |
| **Zombie** | Z | Terminé mais pas encore nettoyé |
| **Uninterruptible Sleep** | D | En attente (non interruptible) |

**Processus zombie :** Un processus qui a terminé mais dont le parent n'a pas encore récupéré le statut de sortie. Généralement sans danger, mais peut indiquer un problème si nombreux.

---

## La commande `ps` : Voir les processus

### Signification

**ps** signifie **Process Status** (État des processus).

### Utilisation de base

```bash
ps
```

Affiche les processus de l'utilisateur actuel dans le terminal actuel.

**Exemple de sortie :**
```
  PID TTY          TIME CMD
 1234 pts/0    00:00:00 bash
 5678 pts/0    00:00:00 ps
```

**Colonnes :**
- **PID** : Numéro unique du processus
- **TTY** : Terminal associé
- **TIME** : Temps CPU utilisé
- **CMD** : Commande qui a lancé le processus

### Options courantes de ps

#### `ps aux` : Tous les processus de tous les utilisateurs

```bash
ps aux
```

**La commande la plus utilisée !**

**Exemple de sortie :**
```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 169316 11984 ?        Ss   10:30   0:02 /sbin/init
utilisateur 1234  2.5  3.2 2456789 256000 ?    Sl   11:00   1:23 /usr/lib/firefox/firefox
```

**Colonnes importantes :**
- **USER** : Propriétaire du processus
- **PID** : Numéro du processus
- **%CPU** : Pourcentage d'utilisation CPU
- **%MEM** : Pourcentage d'utilisation mémoire
- **VSZ** : Mémoire virtuelle (Ko)
- **RSS** : Mémoire physique réelle (Ko)
- **TTY** : Terminal (? = pas de terminal)
- **STAT** : État (S=sleep, R=running, Z=zombie, etc.)
- **START** : Heure de démarrage
- **TIME** : Temps CPU cumulé
- **COMMAND** : Commande complète

#### `ps -ef` : Format alternatif

```bash
ps -ef
```

Affiche tous les processus avec le PPID (parent).

#### `ps -e` : Tous les processus

```bash
ps -e
```

Liste simple de tous les processus.

### Filtrer et rechercher

#### Processus d'un utilisateur spécifique

```bash
ps -u utilisateur
```

#### Processus par nom

```bash
ps aux | grep firefox
```

Affiche tous les processus contenant "firefox".

**Astuce :** Pour éviter que `grep` apparaisse dans les résultats :
```bash
ps aux | grep firefox | grep -v grep
```

Ou plus élégant :
```bash
ps aux | grep [f]irefox
```

#### Trier par utilisation CPU

```bash
ps aux --sort=-%cpu | head -20
```

Affiche les 20 processus utilisant le plus de CPU.

#### Trier par utilisation mémoire

```bash
ps aux --sort=-%mem | head -20
```

#### Processus en arborescence

```bash
ps auxf
```

ou

```bash
ps -ejH
```

Affiche les relations parent-enfant.

**Alternative meilleure :** `pstree`

```bash
pstree
```

Affiche un arbre visuel des processus.

**Avec PIDs :**
```bash
pstree -p
```

**Pour un utilisateur :**
```bash
pstree utilisateur
```

### Format personnalisé

```bash
ps -eo pid,user,%cpu,%mem,cmd
```

Affiche seulement les colonnes spécifiées.

**Exemple :**
```bash
ps -eo pid,user,%cpu,%mem,cmd --sort=-%mem | head -10
```

Top 10 des processus par mémoire avec colonnes personnalisées.

---

## La commande `top` : Surveillance en temps réel

### Présentation

**top** affiche les processus en temps réel et se met à jour automatiquement (par défaut toutes les 3 secondes).

### Lancer top

```bash
top
```

**Interface :**
```
top - 14:30:25 up 3:45, 2 users, load average: 0.52, 0.58, 0.59
Tasks: 245 total,   1 running, 244 sleeping,   0 stopped,   0 zombie
%Cpu(s):  5.3 us,  2.1 sy,  0.0 ni, 92.3 id,  0.2 wa,  0.0 hi,  0.1 si,  0.0 st
MiB Mem :  15923.5 total,   3234.2 free,   8234.5 used,   4454.8 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   6234.2 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
 1234 user      20   0 2456789 256000  89234 S   5.3   1.6   1:23.45 firefox
 5678 user      20   0  345678  45678  23456 S   2.1   0.3   0:12.34 gnome-shell
```

### Comprendre l'en-tête de top

#### Première ligne
```
top - 14:30:25 up 3:45, 2 users, load average: 0.52, 0.58, 0.59
```

- **14:30:25** : Heure actuelle
- **up 3:45** : Système allumé depuis 3h45
- **2 users** : 2 utilisateurs connectés
- **load average** : Charge moyenne sur 1, 5 et 15 minutes

**Load average :**
- < 1.0 : Système peu chargé
- = 1.0 : Système à capacité
- > 1.0 : Système surchargé (processus en attente)

#### Deuxième ligne : Tasks (Tâches)
```
Tasks: 245 total, 1 running, 244 sleeping, 0 stopped, 0 zombie
```

Nombre de processus par état.

#### Troisième ligne : %CPU
```
%Cpu(s): 5.3 us, 2.1 sy, 0.0 ni, 92.3 id, 0.2 wa, 0.0 hi, 0.1 si, 0.0 st
```

- **us** (user) : Temps passé en userspace
- **sy** (system) : Temps passé en kernel
- **ni** (nice) : Processus avec priorité modifiée
- **id** (idle) : **Temps d'inactivité** (92.3% ici = CPU peu utilisé)
- **wa** (wait) : Attente I/O (disque)
- **hi** (hardware interrupts) : Interruptions matérielles
- **si** (software interrupts) : Interruptions logicielles
- **st** (steal) : Temps volé (virtualisation)

**L'important :** **id** doit être élevé pour un système sain.

#### Quatrième ligne : Mémoire RAM
```
MiB Mem : 15923.5 total, 3234.2 free, 8234.5 used, 4454.8 buff/cache
```

- **total** : Mémoire totale
- **free** : Mémoire libre
- **used** : Mémoire utilisée
- **buff/cache** : Mémoire en cache (récupérable)

**Mémoire réellement disponible :** free + buff/cache

#### Cinquième ligne : Swap
```
MiB Swap: 2048.0 total, 2048.0 free, 0.0 used. 6234.2 avail Mem
```

**Swap :** Espace disque utilisé comme mémoire supplémentaire (beaucoup plus lent).

**Bon signe :** Swap non utilisé ou peu utilisé.

### Colonnes de la liste des processus

- **PID** : Process ID
- **USER** : Propriétaire
- **PR** : Priorité
- **NI** : Nice value (-20 à 19)
- **VIRT** : Mémoire virtuelle
- **RES** : Mémoire résidente (physique)
- **SHR** : Mémoire partagée
- **S** : État (S, R, Z, T, D)
- **%CPU** : Utilisation CPU
- **%MEM** : Utilisation mémoire
- **TIME+** : Temps CPU total
- **COMMAND** : Nom du programme

### Commandes interactives dans top

Une fois dans top, vous pouvez utiliser ces touches :

| Touche | Action |
|--------|--------|
| **q** | Quitter |
| **h** | Aide |
| **k** | Tuer un processus (kill) |
| **r** | Renice (changer priorité) |
| **u** | Filtrer par utilisateur |
| **M** | Trier par utilisation mémoire |
| **P** | Trier par utilisation CPU |
| **T** | Trier par temps |
| **c** | Afficher commande complète |
| **1** | Afficher tous les CPU séparément |
| **d** | Changer intervalle de rafraîchissement |
| **Space** | Rafraîchir manuellement |

**Exemples :**
1. Lancez `top`
2. Appuyez sur **M** pour trier par mémoire
3. Appuyez sur **k**, entrez le PID, puis **Entrée** pour tuer un processus
4. Appuyez sur **q** pour quitter

### Options de lancement de top

```bash
top -u utilisateur     # Seulement les processus d'un utilisateur
top -p 1234            # Seulement le processus PID 1234
top -d 1               # Rafraîchir chaque seconde
top -b -n 1            # Mode batch (pour scripts)
```

---

## Alternatives à top : htop et btop

### htop : Version améliorée de top

**Installation :**
```bash
sudo apt install htop
```

**Lancement :**
```bash
htop
```

**Avantages :**
- Interface colorée et plus lisible
- Navigation avec souris
- Affichage graphique CPU et mémoire
- Gestion plus facile des processus
- Recherche intégrée
- Arborescence des processus

**Raccourcis dans htop :**
- **F1** : Aide
- **F2** : Configuration
- **F3** : Rechercher
- **F4** : Filtrer
- **F5** : Arborescence
- **F6** : Trier
- **F9** : Tuer un processus
- **F10** : Quitter
- **Space** : Marquer un processus
- **u** : Filtrer par utilisateur

### btop : Version moderne et visuelle

**Installation :**
```bash
sudo apt install btop
```

**Lancement :**
```bash
btop
```

**Avantages :**
- Interface moderne avec graphiques
- Très esthétique
- Informations détaillées
- Personnalisable
- Surveillance réseau et disque

**Recommandation :** Utilisez `htop` ou `btop` plutôt que `top` pour une meilleure expérience !

---

## La commande `kill` : Arrêter des processus

### Signification

**kill** envoie un **signal** à un processus.

**Attention au nom :** "kill" ne veut pas toujours dire "tuer". C'est envoyer un signal (qui peut être "termine-toi poliment" ou "arrête-toi immédiatement").

### Les signaux

Les signaux sont des messages envoyés aux processus.

**Signaux principaux :**

| Signal | Numéro | Nom | Effet |
|--------|--------|-----|-------|
| **SIGTERM** | 15 | Terminate | Arrêt normal (défaut) |
| **SIGKILL** | 9 | Kill | Arrêt immédiat forcé |
| **SIGHUP** | 1 | Hangup | Relancer/Recharger config |
| **SIGINT** | 2 | Interrupt | Interruption (Ctrl+C) |
| **SIGSTOP** | 19 | Stop | Pause |
| **SIGCONT** | 18 | Continue | Reprendre |

**Liste complète :**
```bash
kill -l
```

### Utilisation de kill

**Syntaxe de base :**
```bash
kill PID
```

Envoie SIGTERM (15) au processus.

**Exemple :**
```bash
kill 1234
```

Demande poliment au processus 1234 de s'arrêter.

### Forcer l'arrêt avec SIGKILL

Si le processus ne répond pas à SIGTERM :

```bash
kill -9 PID
```

ou

```bash
kill -SIGKILL PID
```

**SIGKILL (9) :** Terminaison forcée immédiate, sans nettoyage.

**⚠️ Attention :** Utilisez -9 en dernier recours seulement !

**Ordre recommandé :**
1. `kill PID` (SIGTERM - arrêt propre)
2. Attendez quelques secondes
3. Si ça ne fonctionne pas : `kill -9 PID` (SIGKILL - force)

### Workflow typique

**1. Trouver le PID du processus problématique :**

```bash
ps aux | grep firefox
```

**Résultat :**
```
user  1234  5.3  3.2 2456789 256000 ?  Sl  11:00  1:23 /usr/lib/firefox/firefox
```

Le PID est **1234**.

**2. Arrêter le processus :**

```bash
kill 1234
```

**3. Vérifier qu'il est arrêté :**

```bash
ps aux | grep 1234
```

Si rien ne s'affiche, le processus est terminé.

**4. Si le processus persiste, forcer :**

```bash
kill -9 1234
```

### Autres signaux utiles

#### Recharger la configuration (SIGHUP)

```bash
kill -HUP PID
```

Utile pour les services (Apache, Nginx) pour recharger la config sans redémarrer.

#### Suspendre un processus (SIGSTOP)

```bash
kill -STOP PID
```

Met en pause le processus.

#### Reprendre un processus (SIGCONT)

```bash
kill -CONT PID
```

Relance un processus en pause.

---

## Commandes complémentaires

### `killall` : Tuer par nom

**Syntaxe :**
```bash
killall nom_programme
```

Tue tous les processus portant ce nom.

**Exemples :**

```bash
killall firefox          # Tue tous les Firefox
killall -9 chrome        # Force l'arrêt de tous les Chrome
```

**⚠️ Attention :** Tue TOUS les processus de ce nom !

### `pkill` : Tuer par motif

**Syntaxe :**
```bash
pkill motif
```

Plus flexible que `killall`.

**Exemples :**

```bash
pkill fire               # Tue tout ce qui contient "fire"
pkill -u utilisateur     # Tue tous les processus d'un utilisateur
pkill -9 python          # Force l'arrêt de tous les processus Python
```

### `pgrep` : Trouver les PIDs

**Syntaxe :**
```bash
pgrep motif
```

Affiche les PIDs correspondants (sans tuer).

**Exemples :**

```bash
pgrep firefox            # Affiche les PIDs de Firefox
pgrep -u root            # PIDs des processus de root
pgrep -l firefox         # Avec le nom du processus
```

**Combinaison avec kill :**
```bash
kill $(pgrep firefox)
```

Tue tous les Firefox en une ligne.

### `pidof` : PID d'un programme

```bash
pidof firefox
```

Affiche le(s) PID(s) de Firefox.

**Exemple d'utilisation :**
```bash
kill $(pidof firefox)
```

---

## Gestion des processus en arrière-plan

### Premier plan vs Arrière-plan

**Premier plan (foreground) :** Le processus occupe le terminal, vous ne pouvez rien faire d'autre.

**Arrière-plan (background) :** Le processus tourne sans bloquer le terminal.

### Lancer un processus en arrière-plan

**Méthode 1 : Avec `&` à la fin**

```bash
commande &
```

**Exemple :**
```bash
firefox &
```

Firefox se lance en arrière-plan, le terminal reste utilisable.

**Le système affiche :**
```
[1] 1234
```

- **[1]** : Numéro du job
- **1234** : PID du processus

### Suspendre un processus : Ctrl+Z

Si un processus tourne au premier plan et bloque le terminal :

1. Appuyez sur **Ctrl+Z**
2. Le processus est **suspendu** (mis en pause)

**Exemple :**
```bash
nano fichier.txt
# Ctrl+Z
[1]+  Stopped    nano fichier.txt
```

### Reprendre en arrière-plan : `bg`

```bash
bg
```

Relance le dernier processus suspendu en arrière-plan.

**Exemple complet :**
```bash
nano fichier.txt
# Ctrl+Z (suspend)
bg
# nano continue en arrière-plan (mais ce n'est pas très utile pour nano !)
```

**Plus utile avec des commandes longues :**
```bash
cp gros_fichier.iso /destination/
# Ctrl+Z
bg
# La copie continue en arrière-plan
```

### Revenir au premier plan : `fg`

```bash
fg
```

Ramène le dernier processus en arrière-plan au premier plan.

**Avec numéro de job :**
```bash
fg %1
```

Ramène le job numéro 1 au premier plan.

### Voir les jobs : `jobs`

```bash
jobs
```

Affiche les processus lancés depuis ce terminal.

**Exemple de sortie :**
```
[1]-  Running    firefox &
[2]+  Stopped    nano fichier.txt
```

- **[1], [2]** : Numéros de jobs
- **+** : Job actuel
- **-** : Job précédent
- **Running** : En cours
- **Stopped** : Suspendu

### Tuer un job

```bash
kill %1
```

Tue le job numéro 1.

---

## Priorités des processus : nice et renice

### Qu'est-ce que la priorité ?

Chaque processus a une priorité qui détermine combien de temps CPU il obtient.

**Nice value (NI) :**
- Plage : **-20** (priorité maximale) à **+19** (priorité minimale)
- Par défaut : **0**
- Seul root peut définir des valeurs négatives

**Principe :**
- NI = -20 : Processus très prioritaire
- NI = 0 : Priorité normale
- NI = 19 : Processus peu prioritaire (gentil avec les autres = "nice")

### `nice` : Lancer avec une priorité

**Syntaxe :**
```bash
nice -n VALEUR commande
```

**Exemples :**

```bash
nice -n 10 ./script_lourd.sh
```

Lance le script avec faible priorité (NI = 10).

```bash
nice -n -5 programme_important
```

Lance avec priorité élevée (nécessite sudo pour valeurs négatives).

**Cas d'usage :** Lancer un script de sauvegarde ou une compilation sans ralentir le système :

```bash
nice -n 15 make -j8
```

### `renice` : Modifier la priorité d'un processus en cours

**Syntaxe :**
```bash
renice VALEUR -p PID
```

**Exemples :**

```bash
renice 10 -p 1234
```

Réduit la priorité du processus 1234.

```bash
sudo renice -5 -p 5678
```

Augmente la priorité du processus 5678 (nécessite sudo).

**Pour tous les processus d'un utilisateur :**
```bash
sudo renice 10 -u utilisateur
```

**Dans top ou htop :**
- Appuyez sur **r**
- Entrez le PID
- Entrez la nouvelle valeur

---

## Cas pratiques et dépannage

### Cas 1 : Programme qui ne répond plus

**Symptômes :** Une application est figée, ne répond plus aux clics.

**Solution :**

1. Ouvrir le terminal
2. Trouver le PID :
```bash
ps aux | grep nom_programme
```

3. Arrêter proprement :
```bash
kill PID
```

4. Si ça ne fonctionne pas après 5 secondes :
```bash
kill -9 PID
```

**Alternative avec pkill :**
```bash
pkill -9 nom_programme
```

### Cas 2 : Système ralenti, trouver le coupable

**Solution :**

1. Lancer htop ou top :
```bash
htop
```

2. Trier par CPU (touche **P**) ou mémoire (touche **M**)

3. Identifier le processus problématique

4. Décider de l'action :
   - Arrêter si non nécessaire
   - Réduire la priorité avec **renice**
   - Investiguer pourquoi il consomme autant

### Cas 3 : Script qui tourne en arrière-plan

**Lancer un script lourd sans bloquer le terminal :**

```bash
./script_long.sh > sortie.log 2>&1 &
```

- `> sortie.log` : Sortie dans un fichier
- `2>&1` : Erreurs aussi dans le fichier
- `&` : En arrière-plan

**Vérifier que ça tourne :**
```bash
jobs
# ou
ps aux | grep script_long
```

**Surveiller la progression :**
```bash
tail -f sortie.log
```

### Cas 4 : Tuer tous les processus d'un utilisateur

**Scénario :** Un utilisateur a lancé plein de processus qu'il faut arrêter.

```bash
sudo pkill -u nom_utilisateur
```

**⚠️ Attention :** Tue TOUS les processus de cet utilisateur !

### Cas 5 : Relancer un service système

**Exemples :**

```bash
sudo systemctl restart apache2
# ou avec kill
sudo pkill -HUP apache2
```

Le signal HUP (1) demande souvent au service de recharger sa configuration.

### Cas 6 : Processus zombie

**Symptômes :** `top` affiche des processus zombie (état Z).

**Explication :** Processus terminé dont le parent n'a pas récupéré le statut.

**Solution :**
1. Identifier le parent (PPID) :
```bash
ps aux | grep defunct
```

2. Tuer le parent :
```bash
kill PPID
```

Le parent va nettoyer ses enfants zombies en mourant.

**Note :** Les zombies n'utilisent pas de ressources, ils sont juste un peu "sales" dans la liste.

### Cas 7 : Trop de processus du même type

**Exemple :** Vous avez accidentellement lancé 50 instances de Firefox.

```bash
killall firefox
```

Ou pour forcer :
```bash
killall -9 firefox
```

---

## Surveillance système avancée

### Commande `uptime`

```bash
uptime
```

Affiche depuis combien de temps le système tourne et la charge moyenne.

**Exemple de sortie :**
```
14:30:25 up 3:45, 2 users, load average: 0.52, 0.58, 0.59
```

### Commande `free`

```bash
free -h
```

Affiche l'utilisation de la mémoire et du swap.

**Exemple de sortie :**
```
              total       used       free     shared  buff/cache   available
Mem:           15Gi       8.0Gi      3.1Gi      256Mi       4.3Gi       6.0Gi
Swap:         2.0Gi          0B      2.0Gi
```

### Commande `vmstat`

```bash
vmstat 1
```

Statistiques virtuelles de mémoire, actualisées chaque seconde.

### Commande `iostat`

```bash
iostat
```

Statistiques d'entrée/sortie (disque).

**Installation si nécessaire :**
```bash
sudo apt install sysstat
```

### Commande `lsof`

```bash
lsof
```

Liste tous les fichiers ouverts (List Open Files).

**Fichiers ouverts par un processus :**
```bash
lsof -p PID
```

**Processus utilisant un fichier :**
```bash
lsof /chemin/fichier
```

**Processus écoutant sur un port :**
```bash
sudo lsof -i :80
```

---

## Commandes système

### `systemctl` : Gérer les services

```bash
sudo systemctl status nom_service     # Voir l'état
sudo systemctl start nom_service      # Démarrer
sudo systemctl stop nom_service       # Arrêter
sudo systemctl restart nom_service    # Redémarrer
sudo systemctl enable nom_service     # Activer au démarrage
sudo systemctl disable nom_service    # Désactiver au démarrage
```

**Exemples :**
```bash
sudo systemctl status apache2
sudo systemctl restart networking
sudo systemctl enable ssh
```

### `service` : Ancienne méthode

```bash
sudo service nom_service start
sudo service nom_service stop
sudo service nom_service restart
sudo service nom_service status
```

---

## Bonnes pratiques

### 1. Toujours essayer SIGTERM avant SIGKILL

```bash
kill PID        # Essayer d'abord
# Attendre quelques secondes
kill -9 PID     # Si nécessaire
```

SIGTERM permet au processus de se terminer proprement (sauvegarder, nettoyer).

### 2. Utiliser htop plutôt que top

**Installation :**
```bash
sudo apt install htop
```

Interface plus claire et intuitive.

### 3. Ne pas tuer les processus système

**Évitez de tuer :**
- PID 1 (init/systemd)
- Processus système critiques

**Vérifiez toujours** ce que vous allez tuer :
```bash
ps aux | grep PID
```

### 4. Réduire la priorité au lieu de tuer

Pour un processus qui consomme trop sans être bloqué :

```bash
renice 15 -p PID
```

### 5. Utiliser les outils de surveillance

**Surveiller régulièrement :**
```bash
htop
```

Permet de détecter les problèmes avant qu'ils deviennent graves.

### 6. Logs pour comprendre les crashes

Si un processus plante souvent :

```bash
journalctl -u nom_service
# ou
tail -f /var/log/syslog
```

### 7. Automatiser la surveillance

Créer des alias dans `~/.bashrc` :

```bash
alias cpu='ps aux --sort=-%cpu | head -10'
alias mem='ps aux --sort=-%mem | head -10'
alias processes='htop'
```

---

## Résumé

### Commandes essentielles

```bash
# Voir les processus
ps aux                      # Tous les processus
ps aux | grep firefox       # Chercher un processus
pgrep firefox               # PID de Firefox
pidof firefox               # PID de Firefox

# Surveillance
top                         # Surveillance basique
htop                        # Surveillance améliorée (recommandé)
btop                        # Surveillance moderne

# Tuer des processus
kill PID                    # Arrêt normal
kill -9 PID                 # Arrêt forcé
killall firefox             # Tuer tous les Firefox
pkill firefox               # Tuer par nom

# Arrière-plan
commande &                  # Lancer en arrière-plan
Ctrl+Z                      # Suspendre
bg                          # Reprendre en arrière-plan
fg                          # Ramener au premier plan
jobs                        # Voir les jobs

# Priorités
nice -n 10 commande         # Lancer avec faible priorité
renice 10 -p PID            # Modifier la priorité
```

### États des processus

| État | Signification |
|------|---------------|
| **R** | Running - En cours |
| **S** | Sleeping - En attente |
| **T** | Stopped - Arrêté |
| **Z** | Zombie - Terminé mais pas nettoyé |
| **D** | Uninterruptible sleep |

### Signaux importants

| Signal | Numéro | Usage |
|--------|--------|-------|
| **SIGTERM** | 15 | Arrêt normal (défaut) |
| **SIGKILL** | 9 | Arrêt forcé immédiat |
| **SIGHUP** | 1 | Recharger configuration |
| **SIGSTOP** | 19 | Mettre en pause |
| **SIGCONT** | 18 | Reprendre |

### Workflow de dépannage

1. **Identifier le problème**
   ```bash
   htop          # Voir ce qui consomme
   ```

2. **Trouver le processus**
   ```bash
   ps aux | grep nom
   pgrep nom
   ```

3. **Décider de l'action**
   - Réduire priorité : `renice 15 -p PID`
   - Arrêter proprement : `kill PID`
   - Forcer l'arrêt : `kill -9 PID`

4. **Vérifier**
   ```bash
   ps aux | grep PID
   ```

### Checklist de surveillance

- [ ] Installer htop : `sudo apt install htop`
- [ ] Lancer htop régulièrement pour voir l'état du système
- [ ] Surveiller la mémoire (libre vs utilisée)
- [ ] Surveiller le CPU (idle % doit être élevé)
- [ ] Vérifier qu'il n'y a pas de processus zombie nombreux
- [ ] Identifier les processus qui consomment le plus
- [ ] Arrêter les processus inutiles

**La gestion des processus est essentielle pour maintenir un système sain et performant.** Avec `ps`, `top`/`htop`, et `kill`, vous avez tous les outils nécessaires pour surveiller et contrôler ce qui tourne sur votre machine.

N'ayez pas peur d'explorer et d'expérimenter ! Le pire qui puisse arriver est de devoir relancer un programme que vous avez arrêté par erreur.

---

**Félicitations !** Vous avez terminé le chapitre 7 sur le terminal et les commandes de base. Vous maîtrisez maintenant les fondamentaux de Linux en ligne de commande. Ces compétences sont la base de tout ce que vous ferez ensuite avec Linux !

**Prochaines étapes :** Les chapitres suivants couvriront la gestion du système de fichiers, la configuration réseau, la sécurité, et bien d'autres sujets avancés pour faire de vous un utilisateur Linux complet.

⏭️ [Gestion du système de fichiers](/08-gestion-du-systeme-de-fichiers/README.md)
