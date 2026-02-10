🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 23.8 Outils de diagnostic (inxi, hardinfo)

## Introduction

Quand vous avez un problème avec votre ordinateur sous Linux Mint, ou même simplement pour mieux connaître votre matériel, les outils de diagnostic sont indispensables. Ils vous permettent d'obtenir des informations détaillées sur votre système, votre matériel, vos pilotes, et bien plus encore.

Ce guide vous présente les meilleurs outils de diagnostic disponibles sous Linux Mint, du plus simple au plus avancé, et vous apprend à les utiliser efficacement pour identifier et résoudre des problèmes.

**Bonne nouvelle :** Ces outils sont gratuits, faciles à utiliser, et souvent plus complets que leurs équivalents Windows !

---

## Pourquoi utiliser des outils de diagnostic ?

### Cas d'usage courants

1. **Identifier votre matériel**
   - Quelle carte graphique ai-je exactement ?
   - Combien de RAM est installée ?
   - Quel est mon modèle de processeur ?

2. **Demander de l'aide sur un forum**
   - Fournir des informations précises sur votre système
   - Faciliter le diagnostic par d'autres personnes

3. **Vérifier la compatibilité**
   - Mon matériel est-il bien détecté ?
   - Les pilotes sont-ils correctement installés ?

4. **Diagnostiquer un problème**
   - Pourquoi mon ordinateur est lent ?
   - Quel composant pose problème ?
   - Y a-t-il des erreurs matérielles ?

5. **Avant achat/vente**
   - Vérifier les caractéristiques exactes
   - Générer un rapport complet du système

---

## inxi : L'outil de diagnostic en ligne de commande

`inxi` est **l'outil de référence** pour obtenir des informations système sous Linux. Il est léger, rapide, et extrêmement complet.

### Installation

inxi est généralement pré-installé sur Linux Mint. Si ce n'est pas le cas :

```bash
sudo apt install inxi
```

**Vérifier l'installation :**
```bash
inxi --version
```

---

### Utilisation de base

#### Informations système minimales

```bash
inxi
```

**Résultat exemple :**
```
CPU: quad core Intel Core i5-8250U (-MT MCP-)  
speed/min/max: 800/400/3400 MHz Kernel: 5.15.0-91-generic x86_64  
Up: 3h 42m Mem: 3891.2/7858.2 MiB (49.5%)  
Storage: 476.94 GiB (24.3% used) Procs: 245 Shell: bash 5.1.16  
inxi: 3.3.13  
```

**Informations affichées :**
- Type de processeur
- Vitesse CPU actuelle/min/max
- Version du kernel
- Temps depuis le démarrage (uptime)
- Mémoire utilisée/totale
- Stockage utilisé
- Nombre de processus
- Shell utilisé

---

#### Informations complètes

```bash
inxi -F
```

ou pour encore plus de détails :

```bash
inxi -Fxz
```

**Options :**
- **-F** : Full (complet) - affiche tout
- **-x** : Extra details (détails supplémentaires)
- **-z** : Masque les informations sensibles (adresses IP, MAC, etc.)

**Résultat :** Affiche des dizaines de lignes avec :
- Système d'exploitation
- Machine (fabricant, modèle)
- Batterie (pour portables)
- Processeur
- Carte graphique
- Audio
- Réseau
- Disques
- Partitions
- Capteurs (températures)
- Et bien plus...

---

### Options détaillées par catégorie

#### Système (-S)

```bash
inxi -S
```

**Affiche :**
- Nom de l'hôte
- Kernel et architecture
- Distribution Linux
- Environnement de bureau
- Gestionnaire d'affichage

**Exemple de résultat :**
```
System:
  Host: mon-pc Kernel: 5.15.0-91-generic x86_64 bits: 64
  Desktop: Cinnamon 5.8.4 Distro: Linux Mint 21.3 Virginia
```

---

#### Machine (-M)

```bash
inxi -M
```

**Affiche :**
- Fabricant de l'ordinateur
- Modèle
- BIOS/UEFI
- Type (Desktop, Laptop, etc.)

**Exemple :**
```
Machine:
  Type: Laptop System: Dell product: XPS 15 9570 v: N/A
  Mobo: Dell model: 0H0CC0 v: A00
  UEFI: Dell v: 1.25.0 date: 08/13/2023
```

---

#### Processeur (-C)

```bash
inxi -C
```

**Affiche :**
- Modèle de CPU
- Nombre de cœurs
- Vitesse actuelle/min/max
- Cache
- Architecture

**Exemple :**
```
CPU:
  Info: quad core model: Intel Core i5-8250U bits: 64 type: MT MCP
  cache: L2: 1024 KiB
  Speed (MHz): avg: 800 min/max: 400/3400
```

**Avec plus de détails :**
```bash
inxi -Cxx
```

---

#### Carte graphique (-G)

```bash
inxi -G
```

**Affiche :**
- Modèle de carte graphique
- Pilote utilisé
- Serveur d'affichage (X11/Wayland)
- Résolution d'écran
- Renderer OpenGL

**Exemple :**
```
Graphics:
  Device-1: Intel UHD Graphics 620 driver: i915 v: kernel
  Device-2: NVIDIA GeForce GTX 1050 Mobile driver: nvidia v: 535.154.05
  Display: x11 server: X.Org v: 1.21.1.7 driver: X: loaded: nvidia
  Resolution: 1920x1080@60Hz
  OpenGL: renderer: NVIDIA GeForce GTX 1050/PCIe/SSE2 v: 4.6.0
```

**Très utile pour :**
- Vérifier quel pilote graphique est utilisé
- Identifier des problèmes d'affichage
- Confirmer qu'une carte GPU est bien détectée

---

#### Audio (-A)

```bash
inxi -A
```

**Affiche :**
- Carte son
- Pilote audio
- Serveur son (PulseAudio, PipeWire)

**Exemple :**
```
Audio:
  Device-1: Intel Sunrise Point-LP HD Audio driver: snd_hda_intel
  Sound Server-1: PulseAudio v: 15.99.1 running: yes
  Sound Server-2: PipeWire v: 0.3.48 running: yes
```

---

#### Réseau (-N et -n)

```bash
# Cartes réseau
inxi -N

# Informations réseau détaillées
inxi -n
```

**-N affiche :**
- Cartes réseau (Ethernet, WiFi)
- Pilotes utilisés

**-n affiche en plus :**
- Interfaces actives
- État (connecté/déconnecté)
- Adresse IP (masquée avec -z)

**Exemple :**
```
Network:
  Device-1: Intel Wireless 8265 / 8275 driver: iwlwifi
  IF: wlan0 state: up mac: <filter>
  Device-2: Realtek RTL8111/8168/8411 driver: r8169
  IF: enp3s0 state: down mac: <filter>
```

---

#### Disques et partitions (-D et -P)

```bash
# Disques
inxi -D

# Partitions
inxi -P
```

**-D affiche :**
- Disques installés
- Modèle et capacité
- Type (HDD, SSD, NVMe)

**-P affiche :**
- Partitions montées
- Système de fichiers
- Espace utilisé/disponible

**Exemple :**
```
Drives:
  Local Storage: total: 476.94 GiB used: 115.8 GiB (24.3%)
  ID-1: /dev/nvme0n1 vendor: Samsung model: SSD 970 EVO 500GB
  size: 465.76 GiB

Partition:
  ID-1: / size: 457.45 GiB used: 115.35 GiB (25.2%) fs: ext4
  dev: /dev/nvme0n1p2
```

---

#### Capteurs et températures (-s)

```bash
inxi -s
```

**Affiche :**
- Températures CPU
- Températures GPU
- Vitesse des ventilateurs
- Tensions

**Exemple :**
```
Sensors:
  System Temperatures: cpu: 45.0 C mobo: 42.0 C gpu: nvidia temp: 38 C
  Fan Speeds (RPM): cpu: 2400
```

**Note :** Nécessite le paquet `lm-sensors` :
```bash
sudo apt install lm-sensors  
sudo sensors-detect  # Configuration initiale  
```

---

#### Batterie (-B)

```bash
inxi -B
```

**Affiche :**
- État de la batterie
- Charge actuelle
- État de charge (Charging/Discharging)
- Condition (santé de la batterie)

**Exemple :**
```
Battery:
  ID-1: BAT0 charge: 45.2 Wh (95.0%) condition: 47.6/56.0 Wh (85.0%)
  volts: 12.8 min: 11.4
```

**Utile pour :**
- Vérifier la santé de la batterie
- Identifier une batterie défectueuse

---

#### Référentiels et paquets (-r)

```bash
inxi -r
```

**Affiche :**
- Dépôts APT configurés
- PPAs actifs

**Exemple :**
```
Repos:
  Active apt repos in: /etc/apt/sources.list.d/official-package-repositories.list
  1: deb http://packages.linuxmint.com virginia main upstream import
  2: deb http://archive.ubuntu.com/ubuntu jammy main restricted universe
  Active apt repos in: /etc/apt/sources.list.d/graphics-drivers-ubuntu-ppa-jammy.list
  1: deb https://ppa.launchpadcontent.net/graphics-drivers/ppa/ubuntu jammy main
```

---

### Combinaison d'options

Vous pouvez combiner plusieurs options :

```bash
# CPU + GPU + Disques
inxi -CDG

# Système + Réseau + Audio
inxi -SNA

# Températures + Batterie
inxi -sB

# Tout avec détails et masquage
inxi -Fxz
```

---

### Options de formatage

#### Sortie colorée (par défaut dans le terminal)

```bash
inxi -F  # Couleurs automatiques
```

#### Sans couleur

```bash
inxi -F -c 0
```

#### Sortie pour forum/IRC

```bash
inxi -F -c 94
```

Cette option formate la sortie pour être facilement copiée sur des forums.

---

### Sauvegarder les informations dans un fichier

```bash
# Sauvegarder dans un fichier texte
inxi -Fxz > ~/info-systeme.txt

# Voir le fichier
cat ~/info-systeme.txt
```

**Très utile pour :**
- Garder une trace de votre configuration
- Envoyer les infos à quelqu'un pour diagnostic
- Poster sur un forum

---

### Cas d'usage pratiques avec inxi

#### Scénario 1 : Demander de l'aide sur un forum

**Commande recommandée :**
```bash
inxi -Fxz
```

Copiez la sortie complète dans votre message de forum. Le **-z** masque les informations sensibles (IP, MAC, etc.).

---

#### Scénario 2 : Identifier pourquoi le système est lent

**Commandes utiles :**
```bash
# Voir la vitesse CPU actuelle
inxi -C

# Voir l'utilisation disque
inxi -P

# Voir les températures (si surchauffe)
inxi -s
```

---

#### Scénario 3 : Vérifier après installation de pilote graphique

```bash
inxi -G
```

**Vérifiez que :**
- Le bon pilote est chargé (nvidia au lieu de nouveau, par exemple)
- OpenGL renderer correspond à votre carte

---

#### Scénario 4 : Préparer la vente de votre ordinateur

```bash
inxi -Fxz > ~/specs-ordinateur.txt
```

Vous avez maintenant un document avec toutes les caractéristiques techniques.

---

## hardinfo : L'interface graphique complète

`hardinfo` (Hardware Info) est un outil graphique très complet pour diagnostiquer et benchmarker votre système.

### Installation

```bash
sudo apt install hardinfo
```

### Lancement

**Méthode 1 : Menu**
Menu → Administration → **System Profiler and Benchmark**

**Méthode 2 : Terminal**
```bash
hardinfo
```

---

### Interface de hardinfo

L'interface est divisée en deux parties :

**Panneau de gauche :** Catégories d'informations  
**Panneau de droite :** Détails de la catégorie sélectionnée  

---

### Catégories disponibles

#### Computer (Ordinateur)

**Summary (Résumé)**
- Vue d'ensemble du système
- OS, Kernel, Hostname
- Uptime
- Utilisateur actuel

**Operating System**
- Distribution Linux complète
- Version du kernel
- Bibliothèques importantes (libc, GTK+, etc.)
- Locales et langue

**Kernel Modules**
- Liste de tous les modules kernel chargés
- Très utile pour vérifier les pilotes

---

#### Devices (Périphériques)

**Processor**
- Informations détaillées CPU
- Nombre de cœurs
- Fréquences
- Cache
- Extensions supportées (SSE, AVX, etc.)
- **Benchmark CPU inclus !**

**Memory**
- RAM totale
- RAM utilisée/libre
- Swap
- Détails sur les barrettes de RAM (si BIOS/UEFI fournit l'info)

**PCI Devices**
- Tous les périphériques PCI
- Carte graphique, réseau, audio, etc.

**USB Devices**
- Périphériques USB connectés
- Fabricant et modèle

**Printers**
- Imprimantes configurées

**Battery**
- État de la batterie (portables)
- Capacité et santé

**Sensors**
- Températures
- Vitesses ventilateurs
- Tensions

**Input Devices**
- Clavier, souris, touchpad
- Autres périphériques d'entrée

---

#### Network (Réseau)

**Network Interfaces**
- Liste de toutes les interfaces réseau
- État, adresse IP, MAC
- Statistiques (paquets envoyés/reçus)

**Connections**
- Connexions réseau actives
- Ports ouverts

**Routing Table**
- Table de routage réseau

**DNS Servers**
- Serveurs DNS configurés

---

#### Benchmarks

hardinfo inclut plusieurs benchmarks intégrés :

**CPU Blowfish**
- Test de cryptographie
- Compare votre CPU à d'autres

**CPU CryptoHash**
- Test de hachage cryptographique

**CPU Fibonacci**
- Calcul de la suite de Fibonacci

**CPU N-Queens**
- Problème des N reines

**FPU Raytracing**
- Test du processeur à virgule flottante

**GPU Drawing**
- Test de performances graphiques

**Comment utiliser :**
1. Cliquez sur un benchmark
2. Cliquez sur "Perform Benchmark"
3. Attendez la fin (peut prendre quelques minutes)
4. Voyez votre score et la comparaison avec d'autres systèmes

---

### Générer un rapport

Une fonctionnalité très utile de hardinfo : générer un rapport HTML complet.

**Procédure :**
1. Menu **Information** → **Generate Report**
2. Cochez les sections à inclure (ou "Select All")
3. Choisissez le format (HTML recommandé)
4. Cliquez sur **Generate**
5. Choisissez où sauvegarder le fichier

**Résultat :**
Un fichier HTML professionnel avec toutes les informations système, prêt à être partagé ou archivé.

---

## Autres outils de diagnostic utiles

### lshw (List Hardware)

Outil puissant pour lister tout le matériel.

**Installation :**
```bash
sudo apt install lshw lshw-gtk
```

**Utilisation en ligne de commande :**
```bash
# Vue complète
sudo lshw

# Vue courte
sudo lshw -short

# Format HTML
sudo lshw -html > ~/materiel.html

# Classe spécifique
sudo lshw -C network   # Réseau  
sudo lshw -C disk      # Disques  
sudo lshw -C memory    # Mémoire  
```

**Utilisation graphique :**
```bash
sudo lshw-gtk
```

Interface graphique similaire à hardinfo mais parfois plus détaillée.

---

### hwinfo

Outil très détaillé de détection matérielle.

**Installation :**
```bash
sudo apt install hwinfo
```

**Utilisation :**
```bash
# Tout le matériel
sudo hwinfo

# Résumé
sudo hwinfo --short

# Catégorie spécifique
sudo hwinfo --cpu  
sudo hwinfo --gfxcard  
sudo hwinfo --netcard  
sudo hwinfo --disk  
```

**Très verbeux :** hwinfo donne BEAUCOUP de détails, parfois trop pour un débutant.

---

### dmidecode

Lit les informations du BIOS/UEFI (DMI/SMBIOS).

**Utilisation :**
```bash
# Tout
sudo dmidecode

# Type spécifique
sudo dmidecode -t bios      # BIOS  
sudo dmidecode -t system    # Système  
sudo dmidecode -t baseboard # Carte mère  
sudo dmidecode -t processor # CPU  
sudo dmidecode -t memory    # RAM  
sudo dmidecode -t chassis   # Châssis  
```

**Exemple pratique - Voir les emplacements RAM :**
```bash
sudo dmidecode -t memory | grep -A 20 "Memory Device"
```

Utile pour savoir :
- Combien d'emplacements RAM vous avez
- Lesquels sont utilisés
- Quelle RAM est installée (DDR3, DDR4, vitesse, etc.)

---

### lspci et lsusb

Lister les périphériques PCI et USB.

#### lspci (PCI)

```bash
# Liste simple
lspci

# Liste détaillée
lspci -v

# Très détaillée
lspci -vv

# Format lisible
lspci -k  # Montre les pilotes kernel utilisés

# Catégorie spécifique
lspci | grep -i vga      # Carte graphique  
lspci | grep -i network  # Carte réseau  
lspci | grep -i audio    # Carte son  
```

**Exemple pratique :**
```bash
# Voir quelle carte réseau et quel pilote
lspci -k | grep -A 3 -i network
```

---

#### lsusb (USB)

```bash
# Liste simple
lsusb

# Détaillée
lsusb -v

# Arborescence (montre les hubs USB)
lsusb -t
```

**Exemple pratique :**
```bash
# Surveiller branchement/débranchement USB
watch -n 1 lsusb
```

---

### lsblk

Lister les disques et partitions.

```bash
# Vue simple
lsblk

# Avec système de fichiers
lsblk -f

# Avec UUID
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINT,UUID
```

**Très utile pour :**
- Identifier les disques et partitions
- Voir les points de montage
- Trouver les UUID pour /etc/fstab

---

### df et du

Espace disque.

#### df (Disk Free)

```bash
# Espace disque
df -h

# Uniquement les vrais disques (pas tmpfs, etc.)
df -h -x tmpfs -x devtmpfs
```

---

#### du (Disk Usage)

```bash
# Taille d'un dossier
du -sh /home/user/Documents

# Top 10 des plus gros dossiers
du -sh /* 2>/dev/null | sort -h | tail -10

# Analyser le dossier actuel
du -h --max-depth=1 | sort -h
```

---

### free

Utilisation de la mémoire RAM.

```bash
# Mémoire
free -h

# Avec rafraîchissement (chaque seconde)
free -h -s 1
```

---

### uptime

Temps depuis le démarrage et charge système.

```bash
uptime
```

**Résultat exemple :**
```
18:34:12 up 3:42, 1 user, load average: 0.52, 0.58, 0.59
```

**Interprétation :**
- 18:34:12 : Heure actuelle
- up 3:42 : Système allumé depuis 3h42
- 1 user : 1 utilisateur connecté
- load average : Charge système (1, 5, 15 minutes)

---

### sensors

Températures et capteurs.

**Installation :**
```bash
sudo apt install lm-sensors  
sudo sensors-detect  # Détection (répondre YES à tout)  
```

**Utilisation :**
```bash
sensors

# Avec rafraîchissement
watch -n 2 sensors
```

---

### smartctl

Santé des disques durs (SMART).

**Installation :**
```bash
sudo apt install smartmontools
```

**Utilisation :**
```bash
# Santé globale
sudo smartctl -H /dev/sda

# Informations complètes
sudo smartctl -a /dev/sda

# Test court
sudo smartctl -t short /dev/sda

# Test long (peut prendre des heures)
sudo smartctl -t long /dev/sda

# Voir les résultats du test
sudo smartctl -l selftest /dev/sda
```

**Interpréter la santé :**
- **PASSED** : Disque en bonne santé ✅
- **FAILED** : Disque défectueux, sauvegarder immédiatement ! ❌

---

### uname

Informations kernel et système.

```bash
# Tout
uname -a

# Kernel seulement
uname -r

# Architecture
uname -m

# Nom de machine
uname -n
```

---

### neofetch / screenfetch

Affichage esthétique des informations système.

**Installation :**
```bash
sudo apt install neofetch
# ou
sudo apt install screenfetch
```

**Utilisation :**
```bash
neofetch
# ou
screenfetch
```

**Résultat :**
Un affichage coloré avec le logo de votre distribution et les informations clés.

**Utile pour :**
- Captures d'écran "stylées"
- Affichage rapide des specs
- Signatures de forum

---

## Outils de monitoring en temps réel

### htop

Moniteur de processus amélioré.

```bash
sudo apt install htop  
htop  
```

**Navigation :**
- **F1** : Aide
- **F3** : Rechercher un processus
- **F4** : Filtrer
- **F5** : Vue arbre
- **F6** : Trier
- **F9** : Tuer un processus
- **F10** : Quitter

---

### btop

Version moderne et très esthétique.

```bash
sudo apt install btop  
btop  
```

Interface magnifique avec graphiques en temps réel.

---

### glances

Monitoring complet en un seul outil.

```bash
sudo apt install glances  
glances  
```

**Affiche :**
- CPU, RAM, Swap
- Réseau (up/down)
- Disques I/O
- Processus
- Températures (si capteurs)
- Alertes automatiques

---

### nmon

Outil de performance système.

```bash
sudo apt install nmon  
nmon  
```

**Touches :**
- **c** : CPU
- **m** : Mémoire
- **d** : Disques
- **n** : Réseau
- **t** : Top processus
- **q** : Quitter

---

## Benchmarking et tests de performance

### stress et stress-ng

Tester la stabilité du système sous charge.

**Installation :**
```bash
sudo apt install stress stress-ng
```

**Utilisation :**
```bash
# Stresser CPU pendant 60 secondes
stress --cpu 4 --timeout 60

# Stress CPU + RAM
stress --cpu 4 --vm 2 --vm-bytes 1G --timeout 60

# Stress complet avec stress-ng
stress-ng --cpu 4 --io 2 --vm 1 --vm-bytes 1G --timeout 60s
```

**⚠️ Attention :** Surveiller les températures pendant le stress test !

---

### sysbench

Benchmark de performances.

```bash
sudo apt install sysbench
```

**Tests disponibles :**

```bash
# Test CPU
sysbench cpu --cpu-max-prime=20000 run

# Test mémoire
sysbench memory run

# Test threads
sysbench threads run

# Test I/O fichiers
sysbench fileio --file-test-mode=seqwr prepare  
sysbench fileio --file-test-mode=seqwr run  
sysbench fileio cleanup  
```

---

### hdparm

Tester vitesse de lecture disque.

```bash
sudo apt install hdparm

# Test de vitesse
sudo hdparm -Tt /dev/sda

# Infos disque
sudo hdparm -I /dev/sda
```

---

### speedtest-cli

Tester vitesse Internet.

```bash
sudo apt install speedtest-cli

# Lancer le test
speedtest-cli

# Simple (juste vitesse)
speedtest-cli --simple

# Partager le résultat
speedtest-cli --share
```

---

## Diagnostic réseau avancé

### ping

```bash
# Tester connexion
ping google.com

# Limiter à 4 paquets
ping -c 4 google.com
```

---

### traceroute

```bash
sudo apt install traceroute

# Tracer le chemin vers un serveur
traceroute google.com
```

---

### netstat / ss

```bash
# Connexions actives
netstat -tuln

# Ou avec ss (plus moderne)
ss -tuln

# Programmes utilisant le réseau
sudo netstat -tulnp  
sudo ss -tulnp  
```

---

### iftop

Utilisation réseau en temps réel.

```bash
sudo apt install iftop

# Lancer
sudo iftop

# Interface spécifique
sudo iftop -i wlan0
```

---

### nmap

Scanner réseau.

```bash
sudo apt install nmap

# Scanner votre réseau local
nmap 192.168.1.0/24

# Scanner les ports ouverts sur votre machine
nmap localhost
```

---

## Créer un rapport de diagnostic complet

### Script personnalisé

Créez un script pour générer un rapport complet :

```bash
#!/bin/bash
# Script de diagnostic système

RAPPORT=~/diagnostic-$(date +%Y%m%d-%H%M).txt

echo "=== RAPPORT DE DIAGNOSTIC SYSTÈME ===" > $RAPPORT  
echo "Date : $(date)" >> $RAPPORT  
echo "" >> $RAPPORT  

echo "=== SYSTÈME ===" >> $RAPPORT  
inxi -Sxz >> $RAPPORT  
echo "" >> $RAPPORT  

echo "=== MATÉRIEL ===" >> $RAPPORT  
inxi -Fxz >> $RAPPORT  
echo "" >> $RAPPORT  

echo "=== DISQUES ===" >> $RAPPORT  
df -h >> $RAPPORT  
echo "" >> $RAPPORT  

echo "=== MÉMOIRE ===" >> $RAPPORT  
free -h >> $RAPPORT  
echo "" >> $RAPPORT  

echo "=== TEMPÉRATURES ===" >> $RAPPORT  
sensors 2>/dev/null >> $RAPPORT  
echo "" >> $RAPPORT  

echo "=== PROCESSUS TOP 10 CPU ===" >> $RAPPORT  
ps aux --sort=-%cpu | head -11 >> $RAPPORT  
echo "" >> $RAPPORT  

echo "=== PROCESSUS TOP 10 RAM ===" >> $RAPPORT  
ps aux --sort=-%mem | head -11 >> $RAPPORT  
echo "" >> $RAPPORT  

echo "=== UPTIME ===" >> $RAPPORT  
uptime >> $RAPPORT  
echo "" >> $RAPPORT  

echo "Rapport généré : $RAPPORT"
```

**Utilisation :**
```bash
chmod +x ~/diagnostic.sh
~/diagnostic.sh
```

---

## Tableau comparatif des outils

| Outil | Type | Difficulté | Complétude | Meilleur pour |
|-------|------|------------|------------|---------------|
| **inxi** | CLI | Facile | ⭐⭐⭐⭐⭐ | Vue d'ensemble rapide |
| **hardinfo** | GUI | Très facile | ⭐⭐⭐⭐ | Exploration visuelle |
| **lshw** | CLI/GUI | Facile | ⭐⭐⭐⭐⭐ | Détails matériels |
| **hwinfo** | CLI | Moyen | ⭐⭐⭐⭐⭐ | Détection matériel |
| **dmidecode** | CLI | Moyen | ⭐⭐⭐⭐ | Info BIOS/UEFI |
| **lspci** | CLI | Facile | ⭐⭐⭐ | Périph. PCI |
| **lsusb** | CLI | Facile | ⭐⭐⭐ | Périph. USB |
| **sensors** | CLI | Facile | ⭐⭐⭐ | Températures |
| **smartctl** | CLI | Moyen | ⭐⭐⭐⭐ | Santé disques |
| **htop** | CLI | Facile | ⭐⭐⭐⭐ | Monitoring live |
| **glances** | CLI | Facile | ⭐⭐⭐⭐⭐ | Monitoring complet |

---

## Quand utiliser quel outil ?

### Je veux juste connaître mes specs rapidement
→ **inxi -F** ou **neofetch**

### Je veux explorer visuellement mon matériel
→ **hardinfo**

### Je dois fournir mes infos sur un forum
→ **inxi -Fxz** (copier la sortie)

### Je veux vérifier si un composant est détecté
→ **lspci** (PCI) ou **lsusb** (USB)

### Mon ordinateur chauffe trop
→ **sensors** ou **inxi -s**

### Je veux vérifier la santé de mon disque dur
→ **sudo smartctl -H /dev/sda**

### Je veux surveiller les performances en temps réel
→ **htop** ou **glances**

### Je veux benchmarker mon système
→ **hardinfo** (benchmarks intégrés) ou **sysbench**

### Je veux tout savoir sur ma RAM
→ **sudo dmidecode -t memory**

### Je veux tester ma connexion Internet
→ **speedtest-cli**

---

## FAQ - Questions fréquentes

### inxi affiche "llvmpipe" pour ma carte graphique, c'est grave ?

**Oui**, cela signifie que vous utilisez le rendu logiciel (pas d'accélération matérielle).

**Solution :** Installer les pilotes graphiques appropriés via le Gestionnaire de pilotes.

---

### Comment savoir si mon SSD ou HDD est en bonne santé ?

```bash
sudo smartctl -H /dev/sda
```

**PASSED** = OK ✅  
**FAILED** = Problème, sauvegarder immédiatement ! ❌  

---

### Mon ordinateur a combien de RAM exactement ?

```bash
# Vue simple
free -h

# Détails (emplacements, vitesse, etc.)
sudo dmidecode -t memory
```

---

### Comment vérifier si mon WiFi est bien détecté ?

```bash
inxi -N
# ou
lspci | grep -i network
```

---

### Quelle est la température normale de mon CPU ?

**Au repos :** 30-50°C  
**Sous charge :** 60-80°C  
**Critique :** > 90°C (throttling, ralentissements)  

**Vérifier :**
```bash
sensors
# ou
inxi -s
```

---

### Comment générer un rapport pour le support technique ?

**Méthode 1 - inxi :**
```bash
inxi -Fxz > ~/rapport-systeme.txt
```

**Méthode 2 - hardinfo :**
1. Ouvrir hardinfo
2. Information → Generate Report
3. Sauvegarder en HTML

---

### Quelle commande pour tout voir d'un coup ?

```bash
inxi -Fxxxz
```

Le **-xxx** donne le niveau de détail maximum.

---

### Comment savoir si je suis en BIOS ou UEFI ?

```bash
[ -d /sys/firmware/efi ] && echo "UEFI" || echo "BIOS Legacy"
```

**Ou :**
```bash
inxi -M | grep BIOS
```

---

## Commandes de référence rapide

### Informations système

```bash
# Vue d'ensemble
inxi -F  
inxi -Fxz  # Avec détails et masquage  

# Par catégorie
inxi -S    # Système  
inxi -M    # Machine  
inxi -C    # CPU  
inxi -G    # GPU  
inxi -A    # Audio  
inxi -N    # Réseau  
inxi -D    # Disques  
inxi -P    # Partitions  
inxi -s    # Capteurs  
inxi -B    # Batterie  
```

### Matériel détaillé

```bash
# Tout le matériel
sudo lshw  
sudo lshw-gtk  # GUI  

# PCI et USB
lspci  
lsusb  

# BIOS/UEFI info
sudo dmidecode -t bios  
sudo dmidecode -t memory  
```

### Diagnostics spécifiques

```bash
# Températures
sensors

# Santé disque
sudo smartctl -H /dev/sda

# Mémoire
free -h

# Disques
df -h  
lsblk  

# Réseau
ip a  
nmcli device status  
speedtest-cli  
```

### Monitoring

```bash
# Processus
htop  
btop  

# Complet
glances

# Ressources
top  
nmon  
```

---

## Checklist de diagnostic

**☐ 1. Informations système de base**
```bash
inxi -S
```

**☐ 2. Identifier le matériel**
```bash
inxi -F
```

**☐ 3. Vérifier les pilotes graphiques**
```bash
inxi -G
```

**☐ 4. Vérifier les températures**
```bash
sensors
```

**☐ 5. Vérifier l'espace disque**
```bash
df -h
```

**☐ 6. Vérifier la mémoire**
```bash
free -h
```

**☐ 7. Vérifier la santé du disque**
```bash
sudo smartctl -H /dev/sda
```

**☐ 8. Vérifier les processus gourmands**
```bash
htop
```

**☐ 9. Générer un rapport complet si nécessaire**
```bash
inxi -Fxz > ~/diagnostic.txt
```

**☐ 10. Documenter les résultats**
- Noter les anomalies
- Sauvegarder les rapports

---

## Conclusion

Les outils de diagnostic sont vos meilleurs alliés pour comprendre, maintenir, et dépanner votre système Linux Mint :

**Points clés à retenir :**

1. **inxi** est l'outil universel à connaître absolument
2. **hardinfo** offre une interface graphique complète et accessible
3. **Combinez les outils** pour un diagnostic précis
4. **Sauvegardez les rapports** pour historique et comparaisons
5. **Les informations système** sont essentielles pour demander de l'aide

**Méthodologie de diagnostic :**
- Commencez par **inxi -F** pour vue d'ensemble
- Utilisez des outils spécialisés pour creuser
- Surveillez les températures et santé disque régulièrement
- Générez des rapports complets avant modifications importantes

**Pour débutants :**
- **inxi -F** : Commande magique pour tout savoir
- **hardinfo** : Interface graphique conviviale
- **htop** : Voir ce qui se passe en temps réel

**Pour utilisateurs avancés :**
- Maîtrisez les options d'inxi (-x, -xx, -xxx)
- Explorez lshw, hwinfo, dmidecode
- Automatisez avec des scripts personnalisés

Avec ces outils, vous avez tout ce qu'il faut pour devenir autonome dans le diagnostic de votre système Linux Mint !

---

## Ressources complémentaires

- [Page man inxi](https://smxi.org/docs/inxi.htm)
- [GitHub hardinfo](https://github.com/lpereira/hardinfo)
- [lm-sensors documentation](https://github.com/lm-sensors/lm-sensors)
- [smartmontools wiki](https://www.smartmontools.org/wiki)

---

⏭️ [Boot-repair et outils de secours](/23-depannage-et-resolution-de-problemes/09-boot-repair-et-outils-de-secours.md)
