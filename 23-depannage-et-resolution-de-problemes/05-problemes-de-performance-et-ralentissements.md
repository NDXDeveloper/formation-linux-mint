🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 23.5 Problèmes de performance et ralentissements

## Introduction

Un ordinateur qui ralentit est frustrant, mais heureusement, Linux Mint offre de nombreux outils pour diagnostiquer et résoudre ces problèmes. Contrairement à Windows, Linux ne ralentit généralement pas avec le temps si on suit quelques bonnes pratiques.

Ce guide vous aidera à identifier **pourquoi** votre système ralentit et **comment** y remédier, que vous soyez débutant ou utilisateur plus expérimenté.

**Bonne nouvelle :** La plupart des ralentissements ont des causes simples et des solutions accessibles à tous !

---

## Identifier le type de ralentissement

Avant de chercher une solution, il faut comprendre **quel type** de ralentissement vous rencontrez.

### Type 1 : Ralentissement au démarrage

**Symptômes :**
- L'ordinateur met longtemps à démarrer (plus de 2-3 minutes)
- Le logo Linux Mint reste affiché longtemps
- Beaucoup de temps entre l'écran de connexion et le bureau

**Causes probables :**
- Trop de programmes au démarrage
- Services système lents
- Vérification du disque (fsck) automatique
- Problème réseau (timeout)

---

### Type 2 : Ralentissement général du système

**Symptômes :**
- Toutes les applications sont lentes
- Le curseur saccade
- Les fenêtres mettent du temps à s'ouvrir
- Le système "rame" en permanence

**Causes probables :**
- Mémoire RAM insuffisante ou saturée
- Processeur surchargé
- Swap utilisé intensivement
- Disque dur lent ou plein

---

### Type 3 : Ralentissement progressif (après plusieurs heures)

**Symptômes :**
- Le système est rapide au démarrage
- Mais ralentit au fil des heures
- Devient de plus en plus lent sans redémarrage

**Causes probables :**
- Fuite mémoire (memory leak) d'une application
- Trop d'onglets navigateur ouverts
- Fichiers temporaires qui s'accumulent
- Processus zombie

---

### Type 4 : Ralentissement avec un logiciel spécifique

**Symptômes :**
- Le système est normal
- Mais un logiciel particulier est très lent
- Ou ralentit tout le système quand il est ouvert

**Causes probables :**
- Logiciel mal optimisé
- Fichier de configuration corrompu
- Ressources insuffisantes pour ce logiciel
- Conflit avec un autre programme

---

### Type 5 : Ralentissement de l'interface graphique

**Symptômes :**
- Animations saccadées
- Fenêtres qui "traînent" quand vous les déplacez
- Affichage qui scintille ou ralentit
- Terminal fonctionne bien, mais interface graphique lente

**Causes probables :**
- Problème de pilote graphique
- Effets visuels trop gourmands
- Carte graphique sous-exploitée
- Résolution d'écran mal configurée

---

## Diagnostic : Identifier la ressource saturée

La première étape est de savoir **quelle ressource** pose problème : CPU, RAM, disque, ou réseau.

### Outil 1 : Moniteur système (interface graphique)

C'est l'outil le plus simple pour les débutants.

**Lancement :**
- Menu → Administration → **Moniteur système**
- Ou **Ctrl+Alt+Suppr** (comme Windows)

**Que regarder :**

#### Onglet "Processus"
- **Colonne CPU %** : Quel programme utilise le processeur ?
  - Normal : < 10% au repos
  - Suspect : > 50% en permanence sans raison

- **Colonne Mémoire** : Quel programme utilise la RAM ?
  - Chrome/Firefox : 500 Mo - 2 Go est normal
  - Suspect : Un programme inconnu utilisant plusieurs Go

#### Onglet "Ressources"
- **Graphique CPU** : Utilisation du processeur
  - Vert : OK
  - Rouge constant : Problème

- **Graphique Mémoire** : Utilisation de la RAM
  - Regardez **"Mémoire et swap"**
  - Si le **swap** est utilisé beaucoup → Pas assez de RAM

- **Graphique Réseau** : Trafic réseau
  - Pic occasionnel : Normal
  - Trafic constant élevé sans raison : Suspect

#### Onglet "Système de fichiers"
- **Utilisation disque** : Combien d'espace reste-t-il ?
  - Moins de 10% libre → Problème garanti
  - Moins de 20% libre → Risque de ralentissement

---

### Outil 2 : top (terminal simple)

Pour ceux qui préfèrent le terminal, `top` est léger et efficace.

```bash
top
```

**Lecture de l'affichage :**

```
top - 14:23:15 up 2:34,  1 user,  load average: 0.52, 0.58, 0.59
Tasks: 245 total,   1 running, 244 sleeping,   0 stopped,   0 zombie
%Cpu(s):  5.2 us,  1.8 sy,  0.0 ni, 92.8 id,  0.2 wa,  0.0 hi,  0.0 si
MiB Mem :   7876.5 total,   1234.2 free,   4567.3 used,   2075.0 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   2891.7 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
 1234 user      20   0 4123456 567890  12345 S   8.3   7.2   12:34.56 firefox
```

**Ce qui est important :**

- **load average** : Charge système
  - < 1.0 : Très bien (sur un CPU à 1 cœur)
  - < nombre de cœurs : Bien
  - > nombre de cœurs : Surchargé

- **%Cpu(s)** :
  - **id** (idle) = repos → Plus c'est élevé, mieux c'est
  - **wa** (wait) = attente disque → Si > 10%, disque lent

- **MiB Mem** :
  - **free** : RAM libre
  - **used** : RAM utilisée
  - Si **Swap used** > 0 régulièrement → Manque de RAM

- **Colonne %CPU** : Processus qui consomme le plus de CPU
- **Colonne %MEM** : Processus qui consomme le plus de RAM

**Commandes utiles dans top :**
- **q** : Quitter
- **k** : Tuer un processus (demande le PID)
- **M** : Trier par utilisation mémoire
- **P** : Trier par utilisation CPU
- **1** : Afficher chaque cœur CPU séparément

---

### Outil 3 : htop (terminal amélioré)

`htop` est une version améliorée et colorée de `top`.

**Installation :**
```bash
sudo apt install htop
```

**Lancement :**
```bash
htop
```

**Avantages :**
- Interface colorée et visuelle
- Navigation facile (flèches)
- Barres graphiques pour CPU et RAM
- Fonction de recherche (F3)
- Tuer un processus facilement (F9)

**Navigation :**
- **F1** : Aide
- **F3** : Rechercher un processus
- **F4** : Filtrer
- **F5** : Vue arbre (voir les processus parents/enfants)
- **F6** : Changer le tri
- **F9** : Tuer un processus
- **F10** ou **q** : Quitter

---

### Outil 4 : btop (terminal moderne)

`btop` est un outil de monitoring très moderne et esthétique.

**Installation :**
```bash
sudo apt install btop
```

**Lancement :**
```bash
btop
```

**Avantages :**
- Interface magnifique avec graphiques
- Toutes les ressources visibles en un coup d'œil
- Utilisation réseau en temps réel
- Températures si disponibles

---

## Solutions par type de problème

### Problème : CPU constamment à 100%

#### Diagnostic

Ouvrez le Moniteur système ou `htop` et identifiez le processus qui consomme.

#### Solution 1 : Processus légitime mais gourmand

Si c'est un programme que vous utilisez (Firefox, LibreOffice, etc.) :

**Firefox/Chrome :**
```bash
# Vérifier les onglets ouverts
# Fermez ceux inutiles
# Désactivez les extensions gourmandes
```

**Astuce Firefox :** Tapez `about:performance` dans la barre d'adresse pour voir les onglets gourmands.

#### Solution 2 : Processus système anormal

Si c'est un processus système suspect :

**Exemples de processus à surveiller :**

- **tracker-miner-fs** (indexation de fichiers)
```bash
# Désactiver l'indexation si problématique
gsettings set org.freedesktop.Tracker.Miner.Files crawling-interval -2
```

- **baloo_file** (indexation KDE - rare sur Mint)
```bash
balooctl disable
```

- **snapd** (si vous l'avez activé)
```bash
# Désactiver snap si vous ne l'utilisez pas
sudo systemctl disable snapd
sudo systemctl stop snapd
```

#### Solution 3 : Limiter un processus gourmand

Si un processus est nécessaire mais trop gourmand :

```bash
# Installer cpulimit
sudo apt install cpulimit

# Limiter un processus à 50% CPU (exemple avec firefox)
cpulimit -e firefox -l 50 &
```

---

### Problème : RAM saturée (mémoire pleine)

#### Diagnostic

**Vérifier l'utilisation RAM :**
```bash
free -h
```

**Résultat exemple :**
```
              total        used        free      shared  buff/cache   available
Mem:          7.7Gi       5.2Gi       1.1Gi       234Mi       1.4Gi       2.0Gi
Swap:         2.0Gi       512Mi       1.5Gi
```

**Interprétation :**
- **Mem total** : RAM totale installée
- **Mem used** : RAM utilisée par les programmes
- **Mem available** : RAM réellement disponible (le plus important)
- **Swap used** : Si > 0, signe de manque de RAM

**Problème si :**
- **available** < 500 Mo
- **Swap used** > 1 Go

#### Solution 1 : Identifier les applications gourmandes

```bash
# Lister les 10 processus utilisant le plus de RAM
ps aux --sort=-%mem | head -11
```

**Tueurs de RAM courants :**
- **Navigateurs** (Firefox, Chrome) : Normal jusqu'à 2-3 Go
- **Electron apps** (Discord, Slack, VS Code) : 300-500 Mo chacune
- **Java applications** : Peuvent consommer beaucoup

**Actions :**
- Fermez les onglets inutiles du navigateur
- Fermez les applications inutilisées
- Redémarrez les applications qui fuient la mémoire

#### Solution 2 : Optimiser Firefox/Chrome

**Firefox :**

Tapez `about:config` dans la barre d'adresse et modifiez :
```
browser.cache.memory.capacity = 51200  (limite cache à 50 Mo)
browser.sessionhistory.max_entries = 10  (historique de session)
```

Installez des extensions anti-fuite :
- **Auto Tab Discard** : Décharge les onglets inactifs
- **OneTab** : Regrouper les onglets en liste

**Chrome/Chromium :**
- Utilisez l'extension **The Great Suspender**
- Activez le mode économie de mémoire dans chrome://settings/performance

#### Solution 3 : Ajuster la swappiness

La **swappiness** contrôle à quel point Linux utilise le swap.

**Vérifier la valeur actuelle :**
```bash
cat /proc/sys/vm/swappiness
```

Par défaut : **60** (assez agressif)

**Modifier temporairement :**
```bash
sudo sysctl vm.swappiness=10
```

**Modifier définitivement :**
```bash
sudo nano /etc/sysctl.conf

# Ajouter à la fin :
vm.swappiness=10

# Sauvegarder (Ctrl+O, Entrée, Ctrl+X)
```

**Valeurs recommandées :**
- **10** : Pour SSD, évite l'usure
- **60** : Défaut Linux
- **100** : Utilise le swap agressivement

#### Solution 4 : Nettoyer la RAM (temporaire)

**Vider les caches système :**
```bash
# Synchroniser les données sur disque
sync

# Vider les caches (nécessite root)
sudo sh -c 'echo 3 > /proc/sys/vm/drop_caches'
```

**⚠️ Attention :** Cette commande est sûre mais temporaire. Le cache se reconstituera (c'est normal et utile).

#### Solution 5 : Ajouter de la RAM (matériel)

Si votre système utilise constamment tout le swap :
- **4 Go de RAM** : Minimum pour Linux Mint (juste pour navigation web légère)
- **8 Go de RAM** : Recommandé pour usage normal
- **16 Go de RAM** : Confortable pour multitâche et développement

**Vérifier la RAM installée :**
```bash
sudo dmidecode --type memory | grep "Size"
```

---

### Problème : Disque dur lent ou saturé

#### Diagnostic

**Vérifier l'espace disque :**
```bash
df -h
```

**Problème si :**
- Partition `/` (racine) > 90% pleine
- Partition `/home` > 95% pleine

**Vérifier l'activité disque :**
```bash
iotop
```
(Si pas installé : `sudo apt install iotop`)

Cela montre quels processus lisent/écrivent sur le disque.

#### Solution 1 : Libérer de l'espace disque

**Nettoyage automatique :**
```bash
# Nettoyer le cache des paquets
sudo apt clean

# Supprimer les paquets inutilisés
sudo apt autoremove

# Supprimer les anciens kernels (garde les 2 derniers)
sudo apt autoremove --purge
```

**Nettoyage manuel avec BleachBit :**
```bash
# Installer BleachBit
sudo apt install bleachbit

# Lancer (en utilisateur normal, pas sudo !)
bleachbit
```

Cochez :
- Cache système
- Fichiers temporaires
- Corbeille
- Logs anciens

**Trouver les gros fichiers :**
```bash
# Installer ncdu (analyseur d'espace disque)
sudo apt install ncdu

# Analyser votre dossier personnel
ncdu ~

# Analyser tout le système (en root)
sudo ncdu /
```

Navigation dans ncdu :
- **Flèches** : Naviguer
- **Entrée** : Entrer dans un dossier
- **d** : Supprimer (soyez prudent !)
- **q** : Quitter

**Gros fichiers courants :**
- `~/.cache/` : Cache utilisateur (peut être supprimé)
- `~/.local/share/Trash/` : Corbeille (vider régulièrement)
- `/var/log/` : Logs système (peut être nettoyé)
- `/var/cache/apt/archives/` : Paquets téléchargés (nettoyé par apt clean)

#### Solution 2 : Optimiser pour SSD

Si vous avez un SSD, activez TRIM :

**Vérifier si TRIM est activé :**
```bash
sudo systemctl status fstrim.timer
```

**Activer TRIM hebdomadaire :**
```bash
sudo systemctl enable fstrim.timer
sudo systemctl start fstrim.timer
```

**Optimiser /etc/fstab pour SSD :**
```bash
sudo nano /etc/fstab
```

Ajoutez l'option `noatime` à vos partitions SSD :
```
UUID=xxx-xxx-xxx / ext4 noatime,errors=remount-ro 0 1
```

Cela évite d'écrire la date d'accès à chaque lecture de fichier.

#### Solution 3 : Vérifier la santé du disque

**Pour disques durs (HDD) :**
```bash
sudo apt install smartmontools

# Vérifier l'état SMART
sudo smartctl -H /dev/sda  # Remplacez sda par votre disque

# Infos détaillées
sudo smartctl -a /dev/sda
```

**Résultat sain :**
```
SMART overall-health self-assessment test result: PASSED
```

**Si FAILED :** Votre disque est en train de mourir, sauvegardez vos données immédiatement !

**Pour SSD :**
```bash
# Vérifier l'usure
sudo smartctl -a /dev/sda | grep -i wear
```

---

### Problème : Swap utilisé excessivement

#### Diagnostic

Le swap est une zone du disque utilisée comme "extension" de la RAM quand celle-ci est pleine.

**Problème :** Le disque est **beaucoup plus lent** que la RAM → Si swap utilisé massivement, ralentissements garantis.

**Vérifier l'utilisation du swap :**
```bash
free -h
swapon --show
```

#### Solution 1 : Vider le swap

```bash
# Désactiver temporairement le swap
sudo swapoff -a

# Le réactiver
sudo swapon -a
```

**⚠️ Attention :** Ne faites ceci que si vous avez assez de RAM libre. Sinon, des programmes peuvent planter.

#### Solution 2 : Augmenter la taille du swap

Si vous manquez de RAM, augmenter le swap peut aider (temporairement).

**Créer un fichier de swap supplémentaire :**
```bash
# Créer un fichier de 4 Go
sudo fallocate -l 4G /swapfile

# Sécuriser les permissions
sudo chmod 600 /swapfile

# Formater en swap
sudo mkswap /swapfile

# Activer
sudo swapon /swapfile

# Rendre permanent
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

**Vérifier :**
```bash
swapon --show
```

#### Solution 3 : Utiliser zram (swap compressé en RAM)

**zram** crée un swap compressé dans la RAM (plus rapide que le disque).

```bash
# Installer zram-config
sudo apt install zram-config

# Redémarrer pour activer
sudo reboot
```

**Vérifier :**
```bash
zramctl
```

---

### Problème : Démarrage lent

#### Diagnostic

**Analyser le temps de démarrage :**
```bash
systemd-analyze
```

**Résultat exemple :**
```
Startup finished in 3.2s (kernel) + 12.5s (userspace) = 15.7s
```

**Identifier les services lents :**
```bash
systemd-analyze blame
```

Cela liste les services par temps de démarrage (du plus lent au plus rapide).

**Identifier le chemin critique :**
```bash
systemd-analyze critical-chain
```

Montre la chaîne de dépendances qui ralentit le démarrage.

#### Solution 1 : Désactiver les services inutiles

**Services souvent inutiles :**

```bash
# Bluetooth (si vous ne l'utilisez pas)
sudo systemctl disable bluetooth.service

# Imprimante (si vous n'imprimez pas)
sudo systemctl disable cups.service
sudo systemctl disable cups-browsed.service

# ModemManager (si pas de modem 3G/4G)
sudo systemctl disable ModemManager.service

# Avahi (découverte réseau, souvent inutile)
sudo systemctl disable avahi-daemon.service

# Snapd (si vous n'utilisez pas snap)
sudo systemctl disable snapd.service
```

**⚠️ Attention :** Ne désactivez que ce dont vous êtes sûr de ne pas avoir besoin.

**Vérifier l'état :**
```bash
systemctl is-enabled bluetooth.service
```

**Réactiver si besoin :**
```bash
sudo systemctl enable bluetooth.service
```

#### Solution 2 : Réduire le timeout GRUB

Le menu GRUB attend 10 secondes par défaut.

```bash
sudo nano /etc/default/grub

# Modifier :
GRUB_TIMEOUT=3  # Au lieu de 10

# Sauvegarder et mettre à jour
sudo update-grub
```

#### Solution 3 : Optimiser les applications au démarrage

**Liste des applications au démarrage :**
Menu → Préférences → **Applications au démarrage**

**Désactivez** :
- Applications inutiles
- Mises à jour automatiques si vous préférez contrôler
- Gestionnaires cloud si vous ne les utilisez pas

**Commande alternative :**
```bash
gnome-session-properties  # Pour voir/éditer les applications de démarrage
```

---

### Problème : Interface graphique lente ou saccadée

#### Diagnostic

**Vérifier le pilote graphique utilisé :**
```bash
glxinfo | grep "OpenGL renderer"
```

**Résultats possibles :**
- **llvmpipe** : Rendu logiciel (très lent, pas de pilote)
- **NVIDIA** : Pilote propriétaire
- **Intel** : Pilote open source
- **AMD/Radeon** : Pilote open source ou AMDGPU

**Si "llvmpipe" :** Vous n'avez PAS de pilote graphique matériel → Très lent !

#### Solution 1 : Installer les pilotes graphiques

**Méthode graphique :**
Menu → Administration → **Gestionnaire de pilotes**

Sélectionnez le pilote recommandé et installez.

**Méthode terminal pour NVIDIA :**
```bash
# Lister les pilotes disponibles
ubuntu-drivers devices

# Installer le pilote recommandé
sudo ubuntu-drivers autoinstall

# Ou installer une version spécifique
sudo apt install nvidia-driver-535

# Redémarrer
sudo reboot
```

#### Solution 2 : Réduire les effets visuels

**Cinnamon :**
Menu → Préférences → **Effets**

Désactivez ou réduisez :
- Effets de bureau
- Animations
- Transparence

**Ou basculer vers un mode allégé :**
Menu → Préférences → **Paramètres système** → **Général** → Cochez "Mode dégradé"

#### Solution 3 : Utiliser un environnement plus léger

Si votre ordinateur est vraiment ancien :

**MATE** (plus léger que Cinnamon) :
```bash
sudo apt install mint-meta-mate
```

Au prochain démarrage, sélectionnez la session MATE.

**Xfce** (encore plus léger) :
```bash
sudo apt install mint-meta-xfce
```

**LXQt** (ultra-léger) :
```bash
sudo apt install lxqt
```

#### Solution 4 : Vérifier la résolution d'écran

Une mauvaise résolution ou fréquence de rafraîchissement peut causer des saccades.

**Vérifier la résolution :**
Menu → Préférences → **Affichage**

Assurez-vous que la **résolution native** de votre écran est sélectionnée.

---

### Problème : Navigateur web lent

Les navigateurs sont souvent la cause principale de ralentissements.

#### Solution 1 : Gérer les onglets

**Règle d'or :** Pas plus de 10-15 onglets ouverts simultanément.

**Firefox :**
- Tapez `about:performance` pour voir les onglets gourmands
- Installez **Auto Tab Discard** pour suspendre les onglets inactifs

**Chrome/Chromium :**
- Paramètres → Performances → Activez "Mode économie de mémoire"

#### Solution 2 : Désactiver les extensions inutiles

**Firefox :**
Menu → Extensions et thèmes → Désactivez celles inutilisées

**Chrome :**
chrome://extensions/ → Désactivez celles inutilisées

**Extensions gourmandes courantes :**
- Bloqueurs de pub lourds (uBlock Origin est léger et efficace)
- Extensions de traduction
- VPN permanents

#### Solution 3 : Vider le cache

**Firefox :**
```bash
# Fermer Firefox puis
rm -rf ~/.cache/mozilla/firefox/
```

**Chrome :**
```bash
# Fermer Chrome puis
rm -rf ~/.cache/google-chrome/
```

#### Solution 4 : Profil Firefox propre

Parfois, un profil Firefox corrompu ralentit tout :

```bash
# Sauvegarder les marque-pages d'abord !
# Lancer Firefox avec le gestionnaire de profils
firefox -ProfileManager

# Créer un nouveau profil
# Tester avec ce nouveau profil
```

#### Solution 5 : Alternatives plus légères

- **Brave** : Basé sur Chromium, plus rapide, bloqueur de pub intégré
- **Vivaldi** : Chromium avec gestion d'onglets avancée
- **Midori** : Ultra-léger (fonctionnalités basiques)
- **GNOME Web (Epiphany)** : Simple et léger

---

## Optimisations système générales

### 1. Nettoyer régulièrement

**Script de nettoyage hebdomadaire :**

```bash
#!/bin/bash
# Créer ce fichier : ~/nettoyage.sh

echo "Nettoyage du système..."

# Nettoyer APT
sudo apt autoremove -y
sudo apt autoclean
sudo apt clean

# Vider les corbeilles
rm -rf ~/.local/share/Trash/*

# Nettoyer les logs (garder 7 jours)
sudo journalctl --vacuum-time=7d

# Nettoyer les caches utilisateur
rm -rf ~/.cache/thumbnails/*

echo "Nettoyage terminé !"
```

**Rendre exécutable et lancer :**
```bash
chmod +x ~/nettoyage.sh
~/nettoyage.sh
```

### 2. Désactiver l'indexation de fichiers

Si vous n'utilisez pas la recherche de fichiers par contenu :

```bash
# Désactiver tracker (indexation Gnome/Cinnamon)
gsettings set org.freedesktop.Tracker.Miner.Files crawling-interval -2

# Arrêter les processus d'indexation
tracker reset --hard
```

### 3. Optimiser les I/O du disque

**Pour SSD (recommandé) :**
```bash
sudo nano /etc/fstab

# Ajouter l'option noatime
UUID=xxx / ext4 noatime,errors=remount-ro 0 1
```

**Pour HDD (optionnel) :**
```bash
# Installer preload (précharge les applications fréquentes)
sudo apt install preload
```

### 4. Ajuster les paramètres du noyau

```bash
sudo nano /etc/sysctl.conf

# Ajouter à la fin :

# Réduire l'utilisation du swap
vm.swappiness=10

# Améliorer la réactivité du système
vm.vfs_cache_pressure=50

# Augmenter le cache des fichiers ouverts
fs.file-max=100000

# Sauvegarder et appliquer
sudo sysctl -p
```

### 5. Utiliser un DNS rapide

Des DNS lents peuvent ralentir la navigation web.

**Changer pour des DNS rapides :**

Menu → Préférences → **Connexions réseau** → Votre connexion → **Paramètres IPv4**

**DNS recommandés :**
- **Cloudflare :** 1.1.1.1, 1.0.0.1
- **Google :** 8.8.8.8, 8.8.4.4
- **Quad9 :** 9.9.9.9, 149.112.112.112

---

## Outils de monitoring avancés

### 1. Glances (monitoring complet)

```bash
# Installer
sudo apt install glances

# Lancer
glances
```

**Affiche :**
- CPU, RAM, disque, réseau
- Processus
- Températures (si capteurs disponibles)
- Alertes automatiques

### 2. nmon (monitoring professionnel)

```bash
# Installer
sudo apt install nmon

# Lancer
nmon

# Touches :
# c = CPU
# m = Mémoire
# d = Disques
# n = Réseau
# t = Top processus
```

### 3. Netdata (monitoring web temps réel)

```bash
# Installer
bash <(curl -Ss https://my-netdata.io/kickstart.sh)

# Accéder via navigateur
http://localhost:19999
```

Interface web magnifique avec tous les graphiques en temps réel.

---

## Cas particuliers

### Ordinateur ancien (< 4 Go RAM)

**Optimisations spécifiques :**

1. **Utiliser Xfce ou MATE** au lieu de Cinnamon
2. **Navigateur léger** : Midori ou Falkon
3. **Swap important** : Au moins 4 Go
4. **Zram** : Swap compressé en RAM
5. **Désactiver tous les effets visuels**

**Alternative :** Linux Mint Xfce ou Debian + LXDE

---

### Ordinateur portable (gestion batterie)

**Installer TLP (gestion d'énergie) :**

```bash
sudo apt install tlp tlp-rdw

# Démarrer TLP
sudo tlp start

# État de la batterie
sudo tlp-stat -b
```

TLP optimise automatiquement pour économiser la batterie.

**Alternatives :**
- **laptop-mode-tools**
- **powertop** (diagnostic consommation)

---

### Plusieurs utilisateurs sur la même machine

Si plusieurs personnes utilisent le même ordinateur :

```bash
# Limiter la mémoire par utilisateur
sudo nano /etc/security/limits.conf

# Ajouter (exemple pour user1, max 2 Go RAM) :
user1 hard as 2000000

# Redémarrage requis
```

---

## Quand le matériel est la limite

Parfois, le problème vient du matériel, pas du logiciel.

### Signes que le matériel est insuffisant

- **RAM constamment pleine** même après optimisations
- **CPU à 100%** pour des tâches simples
- **Disque dur très lent** (< 50 Mo/s en lecture)
- **Système de > 10 ans** avec composants d'époque

### Solutions matérielles

**Par ordre d'efficacité :**

1. **Ajouter de la RAM** (impact ++++)
   - Facile et peu coûteux
   - Passer de 4 à 8 Go change tout

2. **Remplacer HDD par SSD** (impact ++++)
   - Énorme différence de réactivité
   - Même un SSD SATA de base est 5-10x plus rapide

3. **Changer de processeur** (impact ++)
   - Plus complexe et coûteux
   - Souvent implique de changer la carte mère

4. **Améliorer la carte graphique** (impact + pour usage graphique)
   - Si vous faites du jeu ou de la 3D
   - Moins utile pour usage bureautique

---

## Maintenance préventive

Pour éviter les ralentissements futurs :

### Routine hebdomadaire (5 minutes)

```bash
# Nettoyer le système
sudo apt autoremove
sudo apt clean

# Vider la corbeille
# Fermer les onglets navigateur inutiles
# Redémarrer si uptime > 7 jours
```

### Routine mensuelle (15 minutes)

```bash
# Vérifier l'espace disque
df -h

# Analyser les gros fichiers
ncdu ~

# Mettre à jour le système
sudo apt update && sudo apt upgrade

# Vérifier les services au démarrage
systemd-analyze blame

# Vérifier la santé du disque (HDD)
sudo smartctl -H /dev/sda
```

### Routine annuelle (30 minutes)

- **Sauvegarde complète** de vos données
- **Vérification approfondie** du disque avec fsck (en recovery mode)
- **Nettoyage physique** de l'ordinateur (poussière)
- **Évaluer** si une mise à jour matérielle est nécessaire

---

## Checklist de dépannage rapide

Quand votre système ralentit, suivez cette checklist :

**☐ 1. Identifier la ressource saturée**
- Ouvrir le Moniteur système
- Regarder CPU, RAM, disque, swap

**☐ 2. Si CPU élevé :**
- Identifier le processus
- Le fermer si inutile
- Le limiter si nécessaire

**☐ 3. Si RAM pleine :**
- Fermer les applications gourmandes
- Vider le cache navigateur
- Vérifier le swap

**☐ 4. Si disque plein (> 90%) :**
- `sudo apt clean && sudo apt autoremove`
- Vider la corbeille
- Analyser avec `ncdu`

**☐ 5. Si disque lent :**
- Vérifier avec `iotop` quel processus écrit
- Vérifier la santé SMART
- Envisager un SSD

**☐ 6. Si ralentissement graphique :**
- Vérifier les pilotes (Gestionnaire de pilotes)
- Réduire les effets visuels

**☐ 7. Si rien ne fonctionne :**
- Redémarrer (libère la RAM)
- Vérifier les mises à jour
- Chercher les logs d'erreur : `journalctl -p err`

---

## FAQ - Questions fréquentes

### Mon système ralentit après quelques heures sans redémarrage

**Cause probable :** Fuite mémoire (memory leak) dans une application.

**Solution :**
```bash
# Voir l'uptime
uptime

# Identifier le processus avec le plus de mémoire
ps aux --sort=-%mem | head -10

# Redémarrer l'application fautive
# Ou redémarrer le système si > 7 jours d'uptime
```

### Est-ce que Linux ralentit avec le temps comme Windows ?

**Non**, pas vraiment. Linux ne s'alourdit pas naturellement. Si ralentissement :
- Disque qui se remplit
- Logiciels qui s'accumulent au démarrage
- Base de données des paquets corrompue

**Solution :** Nettoyer régulièrement, comme indiqué dans "Maintenance préventive".

### Combien de RAM me faut-il pour Linux Mint ?

**Minimum :** 2 Go (navigation web très légère)
**Recommandé :** 4 Go (usage bureautique normal)
**Confortable :** 8 Go (multitâche, développement)
**Idéal :** 16 Go+ (machines virtuelles, montage vidéo)

### Dois-je défragmenter mon disque sous Linux ?

**Non !** Les systèmes de fichiers Linux (ext4, btrfs, xfs) ne se fragmentent pratiquement pas.

**Exception :** Si vous avez un très vieux système avec ext3, la fragmentation peut exister, mais c'est rare.

### Mon SSD est-il bien configuré ?

**Vérifiez :**
```bash
# TRIM activé ?
sudo systemctl status fstrim.timer

# noatime dans fstab ?
cat /etc/fstab | grep noatime

# Swappiness faible ?
cat /proc/sys/vm/swappiness  # Devrait être <= 10
```

### Quelle est une température CPU normale ?

**Au repos :** 30-50°C
**Sous charge :** 60-80°C
**Critique :** > 90°C (throttling, ralentissements)

**Vérifier la température :**
```bash
# Installer sensors
sudo apt install lm-sensors
sudo sensors-detect  # Répondre YES à tout

# Lire les températures
sensors
```

### Pourquoi mon ventilateur tourne constamment ?

**Causes :**
- Processus gourmand en CPU (vérifier avec `htop`)
- Poussière dans l'ordinateur (nettoyage physique)
- Pilote graphique mal configuré
- Pâte thermique à refaire (sur vieux ordinateurs)

---

## Commandes de référence rapide

### Diagnostic

```bash
# Vue d'ensemble ressources
htop
btop
glances

# Utilisation disque
df -h
ncdu /

# Mémoire
free -h

# Processus les plus gourmands CPU
ps aux --sort=-%cpu | head -10

# Processus les plus gourmands RAM
ps aux --sort=-%mem | head -10

# Activité disque
iotop
sudo iotop

# Temps de démarrage
systemd-analyze
systemd-analyze blame

# Température
sensors
```

### Nettoyage

```bash
# Nettoyage APT
sudo apt clean
sudo apt autoremove
sudo apt autoclean

# Vider les caches utilisateur
rm -rf ~/.cache/*

# Nettoyer les logs
sudo journalctl --vacuum-time=7d

# Vider la corbeille
rm -rf ~/.local/share/Trash/*
```

### Optimisation

```bash
# Réduire swappiness
sudo sysctl vm.swappiness=10

# Vider le swap
sudo swapoff -a && sudo swapon -a

# Activer TRIM (SSD)
sudo systemctl enable fstrim.timer

# Désactiver services inutiles
sudo systemctl disable bluetooth.service
sudo systemctl disable cups.service
```

---

## Conclusion

Les ralentissements sous Linux Mint ont généralement des causes identifiables et des solutions accessibles :

**Points clés à retenir :**

1. **Identifiez d'abord** la ressource saturée (CPU, RAM, disque)
2. **Le Moniteur système** est votre premier outil
3. **Le navigateur web** est souvent le coupable principal
4. **Le manque de RAM** cause l'utilisation du swap (très lent)
5. **Un SSD** change radicalement les performances d'un vieux PC
6. **La maintenance régulière** prévient les ralentissements
7. **Linux ne ralentit pas** naturellement avec le temps

**Approche méthodique :**
- Diagnostiquer (quelle ressource ?)
- Identifier (quel processus ?)
- Résoudre (action ciblée)
- Prévenir (maintenance régulière)

Avec ces outils et connaissances, vous pouvez maintenir un système Linux Mint rapide et réactif, même sur du matériel modeste !

---

## Ressources complémentaires

- [Arch Wiki - Améliorer les performances](https://wiki.archlinux.org/title/Improving_performance)
- [Ubuntu Wiki - Performance](https://wiki.ubuntu.com/Performance)
- [Linux Mint Forums - Performance](https://forums.linuxmint.com/)

---


⏭️ [Problèmes graphiques (pilotes, résolution)](/23-depannage-et-resolution-de-problemes/06-problemes-graphiques.md)
