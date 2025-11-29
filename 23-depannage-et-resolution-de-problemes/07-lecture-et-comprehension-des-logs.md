🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 23.7 Lecture et compréhension des logs (journalctl, /var/log)

## Introduction

Les logs (journaux) sont les "carnets de bord" de votre système Linux. Ils enregistrent tout ce qui se passe : démarrages, erreurs, avertissements, connexions, installations de logiciels, et bien plus encore.

Savoir lire les logs est une compétence essentielle pour diagnostiquer des problèmes. C'est comme être détective : les logs contiennent les indices qui vous permettront de comprendre pourquoi quelque chose ne fonctionne pas.

**Rassurez-vous :** Vous n'avez pas besoin de comprendre chaque ligne. Ce guide vous apprendra à trouver les informations importantes et à les interpréter.

---

## Qu'est-ce qu'un log exactement ?

### Définition simple

Un **log** est un fichier texte où le système et les applications écrivent des messages au fur et à mesure :

- **Quand** quelque chose s'est passé (date et heure)
- **Quoi** s'est passé (événement, erreur, action)
- **Qui** l'a fait (programme, service, utilisateur)
- **Niveau** de gravité (information, avertissement, erreur critique)

### Exemple de ligne de log

```
Jan 15 14:23:45 ordinateur systemd[1]: Started CUPS Scheduler
```

**Décomposition :**
- `Jan 15 14:23:45` : Date et heure
- `ordinateur` : Nom de l'ordinateur
- `systemd[1]` : Programme qui a généré le message (ici systemd, processus #1)
- `Started CUPS Scheduler` : Le message lui-même (démarrage du service d'impression)

---

## Les deux systèmes de logs sous Linux Mint

Linux Mint utilise deux systèmes de logs complémentaires :

### 1. journalctl (systemd journal)

**Caractéristiques :**
- **Format binaire** (pas directement lisible avec un éditeur de texte)
- **Très rapide** à interroger
- **Gestion avancée** (filtres, recherches)
- **Temporaire** par défaut (effacé au redémarrage, sauf configuration)

**Utilisation principale :**
- Logs système en temps réel
- Services systemd
- Démarrage du système
- Kernel (noyau Linux)

---

### 2. /var/log (fichiers de logs traditionnels)

**Caractéristiques :**
- **Fichiers texte** (lisibles directement)
- **Persistants** (conservés après redémarrage)
- **Organisés par service** (un fichier par application/service)
- **Rotation automatique** (archivage des anciens logs)

**Utilisation principale :**
- Logs des applications
- Historique des événements
- Analyse sur longue période
- Sauvegarde et archivage

---

## Niveaux de gravité des logs

Les messages de logs ont différents niveaux d'importance :

| Niveau | Nom | Signification | Action requise |
|--------|-----|---------------|----------------|
| 0 | **emerg** | Urgence, système inutilisable | Immédiate ! |
| 1 | **alert** | Alerte, action immédiate nécessaire | Très rapide |
| 2 | **crit** | Critique, erreur grave | Rapide |
| 3 | **err** | Erreur | À investiguer |
| 4 | **warning** | Avertissement | À surveiller |
| 5 | **notice** | Notice importante mais normale | Information |
| 6 | **info** | Information | Lecture optionnelle |
| 7 | **debug** | Débogage (détails techniques) | Développeurs |

**Pour le dépannage :**
- Concentrez-vous sur : **crit**, **err**, **warning**
- Ignorez généralement : **info**, **debug** (trop verbeux)

---

## Utiliser journalctl (systemd journal)

`journalctl` est l'outil moderne pour consulter les logs système.

### Commandes de base

#### Voir tous les logs

```bash
journalctl
```

**Navigation dans journalctl :**
- **Espace** : Page suivante
- **b** : Page précédente
- **g** : Aller au début
- **G** : Aller à la fin
- **/** : Rechercher
- **q** : Quitter

---

#### Voir les logs depuis le dernier démarrage

```bash
journalctl -b
```

**Variantes :**
```bash
journalctl -b 0   # Démarrage actuel
journalctl -b -1  # Démarrage précédent
journalctl -b -2  # Avant-dernier démarrage
```

**Lister les démarrages :**
```bash
journalctl --list-boots
```

**Résultat exemple :**
```
-2 a1b2c3d4... Sun 2025-01-12 08:15:22 CET—Sun 2025-01-12 22:34:11 CET
-1 e5f6g7h8... Mon 2025-01-13 09:02:45 CET—Mon 2025-01-13 23:55:32 CET
 0 i9j0k1l2... Tue 2025-01-14 08:45:12 CET—Tue 2025-01-14 18:22:09 CET
```

---

#### Voir les logs en temps réel (comme tail -f)

```bash
journalctl -f
```

**Très utile pour :**
- Surveiller ce qui se passe en direct
- Déboguer un problème en cours
- Voir les logs pendant une action (installation, démarrage de service)

**Pour arrêter :** Ctrl+C

---

#### Filtrer par niveau de gravité

```bash
# Voir uniquement les erreurs
journalctl -p err

# Voir les erreurs et les critiques
journalctl -p crit

# Voir les avertissements et plus grave
journalctl -p warning
```

**Niveaux disponibles :**
- `emerg`, `alert`, `crit`, `err`, `warning`, `notice`, `info`, `debug`

---

#### Filtrer par période de temps

```bash
# Depuis une heure
journalctl --since "1 hour ago"

# Depuis aujourd'hui à 00:00
journalctl --since today

# Depuis hier
journalctl --since yesterday

# Entre deux dates
journalctl --since "2025-01-10" --until "2025-01-15"

# Depuis une heure précise
journalctl --since "2025-01-14 14:30:00"

# Dernière heure
journalctl --since "60 minutes ago"
```

---

#### Filtrer par service ou unité

```bash
# Logs d'un service spécifique
journalctl -u nom-du-service

# Exemples :
journalctl -u apache2         # Serveur web
journalctl -u bluetooth       # Bluetooth
journalctl -u NetworkManager  # Gestion réseau
journalctl -u lightdm         # Gestionnaire d'affichage
```

**Combiner avec temps réel :**
```bash
journalctl -u apache2 -f
```

---

#### Filtrer par processus (PID)

```bash
# Logs d'un processus spécifique
journalctl _PID=1234
```

**Trouver le PID d'abord :**
```bash
pidof firefox
journalctl _PID=$(pidof firefox)
```

---

#### Afficher avec détails étendus

```bash
journalctl -xe
```

**Options :**
- **-x** : Ajoute des explications aux messages (très utile !)
- **-e** : Saute directement à la fin

**Combinaison utile pour dépannage :**
```bash
journalctl -xep err
```
→ Erreurs avec explications, à la fin du journal

---

#### Limiter le nombre de lignes

```bash
# Dernières 50 lignes
journalctl -n 50

# Dernières 100 lignes
journalctl -n 100

# Dernières 20 lignes en temps réel
journalctl -n 20 -f
```

---

#### Rechercher dans les logs

```bash
# Chercher un mot-clé
journalctl | grep "error"

# Chercher sans tenir compte de la casse
journalctl | grep -i "failed"

# Chercher une adresse IP
journalctl | grep "192.168.1.100"
```

**Ou utiliser la recherche intégrée :**
1. `journalctl`
2. Taper `/` puis votre recherche
3. **n** pour occurrence suivante
4. **N** pour occurrence précédente

---

### Cas d'usage pratiques avec journalctl

#### Diagnostic : Système lent au démarrage

```bash
# Temps de démarrage de chaque service
systemd-analyze blame

# Journal du dernier démarrage, uniquement erreurs
journalctl -b -p err
```

---

#### Diagnostic : Problème réseau

```bash
# Logs NetworkManager depuis 1 heure
journalctl -u NetworkManager --since "1 hour ago"

# Chercher les erreurs réseau
journalctl -p err | grep -i network
```

---

#### Diagnostic : Application qui plante

```bash
# Logs d'une application (exemple Firefox)
journalctl | grep -i firefox

# Ou chercher par nom de processus
journalctl _COMM=firefox
```

---

#### Diagnostic : Après une mise à jour problématique

```bash
# Logs depuis la date de la mise à jour
journalctl --since "2025-01-13 18:00:00"

# Avec uniquement erreurs et critiques
journalctl --since "2025-01-13 18:00:00" -p err
```

---

#### Diagnostic : Problème de démarrage (depuis mode recovery)

```bash
# Logs du démarrage précédent (celui qui a échoué)
journalctl -b -1 -p err
```

---

### Gestion de l'espace disque des logs journalctl

Les logs peuvent prendre beaucoup d'espace.

#### Vérifier l'espace utilisé

```bash
journalctl --disk-usage
```

**Exemple de résultat :**
```
Archived and active journals take up 512.0M in the file system.
```

---

#### Nettoyer les anciens logs

```bash
# Garder seulement les 7 derniers jours
sudo journalctl --vacuum-time=7d

# Garder seulement 500 Mo
sudo journalctl --vacuum-size=500M

# Garder seulement les 5 derniers démarrages
sudo journalctl --vacuum-files=5
```

---

#### Limiter la taille automatiquement

```bash
sudo nano /etc/systemd/journald.conf

# Décommenter et modifier :
SystemMaxUse=500M
MaxRetentionSec=7day

# Redémarrer le service
sudo systemctl restart systemd-journald
```

---

### Exporter les logs journalctl

#### Vers un fichier texte

```bash
# Exporter tout
journalctl > ~/logs-complets.txt

# Exporter uniquement les erreurs
journalctl -p err > ~/logs-erreurs.txt

# Exporter depuis le dernier démarrage
journalctl -b > ~/logs-boot.txt
```

---

#### Format JSON (pour analyse automatisée)

```bash
journalctl -o json > ~/logs.json
journalctl -o json-pretty > ~/logs-readable.json
```

---

## Explorer /var/log (fichiers de logs traditionnels)

Le répertoire `/var/log` contient les logs sous forme de fichiers texte.

### Structure de /var/log

```bash
ls -lh /var/log/
```

**Fichiers et dossiers importants :**

| Fichier/Dossier | Contenu |
|-----------------|---------|
| **syslog** | Messages système généraux |
| **kern.log** | Messages du kernel (noyau) |
| **auth.log** | Authentifications (connexions, sudo) |
| **apt/** | Installations/mises à jour de paquets |
| **Xorg.0.log** | Serveur graphique X11 |
| **lightdm/** | Gestionnaire de connexion |
| **cups/** | Système d'impression |
| **dpkg.log** | Historique des paquets installés |
| **boot.log** | Messages de démarrage |
| **dmesg** | Messages du kernel au boot |

---

### Lire les fichiers de logs

#### Avec cat (afficher tout)

```bash
cat /var/log/syslog
```

**Problème :** Trop de contenu, défile trop vite.

---

#### Avec less (navigation)

```bash
less /var/log/syslog
```

**Navigation :**
- **Espace** : Page suivante
- **b** : Page précédente
- **/** : Rechercher
- **q** : Quitter

---

#### Avec tail (dernières lignes)

```bash
# 20 dernières lignes
tail /var/log/syslog

# 50 dernières lignes
tail -n 50 /var/log/syslog

# Suivi en temps réel
tail -f /var/log/syslog
```

**Très utile :** `tail -f` pour surveiller un log en direct.

---

#### Avec head (premières lignes)

```bash
# 20 premières lignes
head /var/log/syslog

# 100 premières lignes
head -n 100 /var/log/syslog
```

---

#### Avec grep (recherche)

```bash
# Chercher "error" dans syslog
grep "error" /var/log/syslog

# Chercher sans casse (Error, ERROR, error)
grep -i "error" /var/log/syslog

# Chercher et afficher 3 lignes avant et après
grep -C 3 "error" /var/log/syslog

# Chercher dans tous les fichiers syslog (y compris archivés)
grep "error" /var/log/syslog*

# Chercher récursivement dans tout /var/log
sudo grep -r "error" /var/log/
```

---

### Logs spécifiques importants

#### auth.log : Authentifications et sécurité

**Contenu :**
- Connexions utilisateurs (réussies et échouées)
- Commandes sudo
- Connexions SSH
- Tentatives de connexion suspectes

**Exemples :**

```bash
# Voir les connexions réussies
grep "session opened" /var/log/auth.log

# Voir les échecs de connexion
grep "authentication failure" /var/log/auth.log

# Voir les commandes sudo
grep "sudo" /var/log/auth.log

# Tentatives de connexion SSH échouées
grep "Failed password" /var/log/auth.log
```

**Cas d'usage :**
- Vérifier qui s'est connecté et quand
- Détecter tentatives de piratage (nombreux échecs de connexion)
- Audit de sécurité

---

#### kern.log : Kernel (noyau Linux)

**Contenu :**
- Messages du kernel
- Détection de matériel
- Pilotes chargés/déchargés
- Erreurs matérielles

**Exemples :**

```bash
# Erreurs kernel
grep -i "error" /var/log/kern.log

# Détection USB
grep -i "usb" /var/log/kern.log

# Problèmes disque
grep -i "disk\|sda\|nvme" /var/log/kern.log

# Problèmes mémoire
grep -i "memory\|oom" /var/log/kern.log
```

**Cas d'usage :**
- Problèmes matériels (disque, RAM)
- Périphériques USB non reconnus
- Erreurs de pilotes

---

#### Xorg.0.log : Serveur graphique

**Contenu :**
- Démarrage du serveur X
- Détection écrans et résolutions
- Chargement pilotes graphiques
- Erreurs d'affichage

**Exemples :**

```bash
# Voir les erreurs graphiques
grep -i "error\|failed" /var/log/Xorg.0.log

# Résolutions détectées
grep -i "modeline" /var/log/Xorg.0.log

# Pilote graphique chargé
grep -i "driver" /var/log/Xorg.0.log
```

**Cas d'usage :**
- Écran noir au démarrage
- Mauvaise résolution
- Problèmes de pilote graphique

---

#### apt/history.log : Historique des paquets

**Contenu :**
- Tous les paquets installés/supprimés
- Dates d'installation
- Mises à jour effectuées

**Exemples :**

```bash
# Voir les dernières installations
tail -n 50 /var/log/apt/history.log

# Chercher quand un paquet a été installé
grep "firefox" /var/log/apt/history.log

# Voir toutes les installations d'une date
grep "2025-01-14" /var/log/apt/history.log
```

**Cas d'usage :**
- Savoir quand un logiciel a été installé
- Identifier une mise à jour problématique
- Audit des modifications système

---

#### dpkg.log : Gestion détaillée des paquets

**Contenu :**
- Installation/suppression/configuration de paquets
- Très détaillé, niveau bas

**Exemples :**

```bash
# Dernières opérations dpkg
tail -n 100 /var/log/dpkg.log

# Rechercher un paquet spécifique
grep "nvidia-driver" /var/log/dpkg.log
```

---

#### dmesg : Messages kernel au boot

**Contenu :**
- Messages du kernel depuis le démarrage
- Détection matériel
- Initialisations

**Commande :**

```bash
# Voir dmesg
dmesg

# Avec couleurs et pagination
dmesg -H

# Derniers messages
dmesg | tail -50

# Chercher USB
dmesg | grep -i usb

# Erreurs kernel
dmesg | grep -i error

# Niveau d'erreur uniquement
dmesg -l err,crit,alert,emerg
```

**Différence dmesg vs /var/log/kern.log :**
- **dmesg** : Buffer en mémoire (effacé au redémarrage)
- **kern.log** : Fichier sur disque (persistant)

---

### Logs archivés et rotation

Les logs ne grandissent pas indéfiniment. Un système de **rotation** les archive automatiquement.

**Exemple avec syslog :**

```bash
ls -lh /var/log/syslog*
```

**Résultat :**
```
-rw-r----- 1 syslog adm  2.1M Jan 14 18:30 syslog
-rw-r----- 1 syslog adm  1.8M Jan 13 23:59 syslog.1
-rw-r----- 1 syslog adm  512K Jan 12 23:59 syslog.2.gz
-rw-r----- 1 syslog adm  498K Jan 11 23:59 syslog.3.gz
```

**Explication :**
- **syslog** : Log actuel (aujourd'hui)
- **syslog.1** : Hier
- **syslog.2.gz** : Avant-hier (compressé)
- **syslog.3.gz** : Il y a 3 jours (compressé)

---

**Lire les logs compressés :**

```bash
# Voir un fichier .gz sans le décompresser
zcat /var/log/syslog.2.gz

# Chercher dans un .gz
zgrep "error" /var/log/syslog.2.gz

# Chercher dans tous les syslog (actuels et archivés)
zgrep "error" /var/log/syslog*
```

---

**Configuration de la rotation :**

```bash
cat /etc/logrotate.d/rsyslog
```

**Exemple de configuration :**
```
/var/log/syslog
{
    rotate 7          # Garder 7 jours
    daily             # Rotation quotidienne
    missingok         # Ne pas générer d'erreur si le fichier manque
    notifempty        # Ne pas tourner si vide
    delaycompress     # Compresser le jour suivant
    compress          # Compresser les anciens
}
```

---

### Permissions des logs

La plupart des logs nécessitent les droits root pour être lus.

**Vérifier les permissions :**

```bash
ls -l /var/log/syslog
```

**Résultat :**
```
-rw-r----- 1 syslog adm 2156789 Jan 14 18:30 /var/log/syslog
```

**Interprétation :**
- **Propriétaire** (syslog) : Lecture et écriture
- **Groupe** (adm) : Lecture seule
- **Autres** : Aucun accès

**Pour lire :**
- Soit utilisez `sudo` : `sudo cat /var/log/syslog`
- Soit ajoutez-vous au groupe `adm` : `sudo usermod -aG adm votre-nom`

---

## Outils graphiques pour lire les logs

### GNOME Logs (Journaux système)

Menu → Administration → **Journaux système**

**Fonctionnalités :**
- Interface graphique simple
- Filtres par catégorie (Matériel, Applications, Système, Sécurité)
- Filtres par priorité
- Recherche textuelle
- Navigation par date

**Avantages :**
- Très accessible pour débutants
- Pas de ligne de commande
- Présentation claire

**Limites :**
- Moins puissant que journalctl
- Filtrage basique

---

### KSystemLog

Pour les utilisateurs KDE/Plasma (pas par défaut sur Cinnamon).

```bash
# Installer si besoin
sudo apt install ksystemlog

# Lancer
ksystemlog
```

**Fonctionnalités :**
- Lecture de multiples types de logs
- Filtres avancés
- Coloration syntaxique
- Alertes configurables

---

### Logwatch (rapports par email)

Outil qui envoie des résumés de logs par email.

```bash
# Installer
sudo apt install logwatch

# Générer un rapport (afficher dans terminal)
sudo logwatch --detail High --range today --output stdout

# Configurer pour envoi email quotidien
sudo nano /etc/cron.daily/00logwatch
```

**Utile pour :**
- Surveillance de serveurs
- Rapports réguliers automatisés
- Détection d'anomalies

---

## Scénarios de dépannage pratiques

### Scénario 1 : L'ordinateur a redémarré tout seul

**Objectif :** Comprendre pourquoi.

**Méthode :**

```bash
# Voir le dernier démarrage
journalctl -b -1

# Chercher juste avant le redémarrage (à la fin du boot -1)
journalctl -b -1 -e

# Chercher des panics kernel
journalctl -b -1 | grep -i "panic\|oops\|segfault"

# Chercher problèmes de température
journalctl -b -1 | grep -i "temperature\|thermal"

# Vérifier /var/log/syslog pour la dernière session
sudo tail -1000 /var/log/syslog.1 | grep -i "shutdown\|reboot"
```

**Causes courantes :**
- Kernel panic (erreur critique)
- Surchauffe (thermal shutdown)
- Problème d'alimentation
- Mise à jour automatique avec redémarrage

---

### Scénario 2 : Un service ne démarre pas

**Exemple :** Apache ne démarre pas.

**Méthode :**

```bash
# Statut du service
sudo systemctl status apache2

# Logs spécifiques au service
journalctl -u apache2 -n 50

# Avec détails étendus
journalctl -xeu apache2

# Chercher dans les logs Apache
sudo tail -50 /var/log/apache2/error.log
```

**Causes courantes :**
- Port déjà utilisé
- Erreur de configuration
- Permissions fichiers
- Dépendance manquante

---

### Scénario 3 : Connexion Internet perdue

**Méthode :**

```bash
# Logs NetworkManager
journalctl -u NetworkManager --since "30 minutes ago"

# Chercher déconnexions
journalctl | grep -i "disconnected\|down"

# État actuel du réseau
ip link show
nmcli device status

# Logs kernel réseau
dmesg | grep -i "network\|eth\|wlan"
```

---

### Scénario 4 : Disque plein, identifier le coupable

**Méthode :**

```bash
# Vérifier l'espace disque
df -h

# Si /var est plein, souvent à cause des logs
du -sh /var/log/*

# Identifier les gros fichiers de log
sudo find /var/log -type f -size +100M -exec ls -lh {} \;

# Nettoyer journalctl si nécessaire
sudo journalctl --vacuum-size=100M
```

---

### Scénario 5 : Application qui plante régulièrement

**Exemple :** Firefox plante.

**Méthode :**

```bash
# Chercher "firefox" dans journalctl
journalctl | grep -i firefox

# Chercher les segfaults (plantages)
journalctl | grep -i "segfault" | grep -i firefox

# Logs système liés
grep -i firefox /var/log/syslog

# Vérifier les core dumps
coredumpctl list
coredumpctl info firefox
```

---

### Scénario 6 : Tentatives de connexion SSH suspectes

**Méthode :**

```bash
# Voir toutes les tentatives SSH
grep "sshd" /var/log/auth.log

# Échecs de connexion
grep "Failed password" /var/log/auth.log

# Voir les IPs qui tentent de se connecter
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr

# Connexions réussies
grep "Accepted" /var/log/auth.log
```

---

### Scénario 7 : Identifier une mise à jour problématique

**Objectif :** Savoir quelle mise à jour a causé un problème.

**Méthode :**

```bash
# Voir l'historique des mises à jour
tail -100 /var/log/apt/history.log

# Chercher par date (jour du problème)
grep "2025-01-14" /var/log/apt/history.log

# Voir les paquets installés ce jour-là
grep "2025-01-14" /var/log/dpkg.log | grep " install "

# Voir les détails d'une mise à jour spécifique
grep "nvidia" /var/log/apt/history.log
```

---

## Commandes avancées pour analyse de logs

### Combiner plusieurs filtres

```bash
# Erreurs du dernier boot, uniquement NetworkManager
journalctl -b -p err -u NetworkManager

# Logs d'hier entre 14h et 16h
journalctl --since "yesterday 14:00" --until "yesterday 16:00"

# Erreurs critiques depuis 3 jours
journalctl --since "3 days ago" -p crit

# Logs d'un PID précis, avec explications
journalctl _PID=1234 -x
```

---

### Statistiques et comptage

```bash
# Compter les erreurs dans syslog
grep -c "error" /var/log/syslog

# Top 10 des messages les plus fréquents
journalctl -b | awk '{print $5}' | sort | uniq -c | sort -nr | head -10

# Compter par niveau de gravité
journalctl -b | grep -c "ERROR"
journalctl -b | grep -c "WARNING"
```

---

### Exporter pour analyse externe

```bash
# Tout depuis le dernier boot vers fichier
journalctl -b > ~/boot-logs.txt

# Erreurs uniquement, format JSON
journalctl -p err -o json > ~/errors.json

# Logs d'une période précise
journalctl --since "2025-01-10" --until "2025-01-15" > ~/semaine-logs.txt
```

---

### Surveillance continue (monitoring)

```bash
# Surveiller plusieurs logs en parallèle
# Terminal 1
tail -f /var/log/syslog

# Terminal 2
journalctl -f -p err

# Terminal 3
dmesg -w  # (-w = wait, suivi en temps réel)
```

---

## Comprendre les messages de logs courants

### Messages normaux (à ignorer)

Ces messages sont normaux et peuvent être ignorés :

```
systemd[1]: Starting User Manager for UID 1000...
NetworkManager[567]: <info> device (wlan0): state change: activated -> activated
CRON[1234]: (root) CMD (/usr/lib/update-notifier/update-motd-updates-available)
```

**Caractéristiques :**
- Niveau **info** ou **notice**
- Verbes comme "Starting", "Started", "Activated"
- Pas de mot "error", "failed", "critical"

---

### Messages à surveiller (warnings)

```
kernel: [Hardware Error]: Machine check events logged
systemd[1]: Unit some-service.service entered failed state
NetworkManager[567]: <warn> connection timeout
```

**Caractéristiques :**
- Niveau **warning**
- Peuvent indiquer un problème futur
- À investiguer si récurrents

---

### Messages critiques (à traiter)

```
kernel: Out of memory: Kill process 1234 (firefox) score 856 or sacrifice child
systemd[1]: Failed to start Apache Web Server.
kernel: I/O error, dev sda, sector 12345678
SMART: Device: /dev/sda, 1 Currently unreadable sectors
```

**Caractéristiques :**
- Niveau **err**, **crit**, **alert**
- Mots-clés : "failed", "error", "critical", "kill"
- Action immédiate requise

---

### Exemples de messages décodés

#### "Out of memory: Kill process..."

**Signification :** Le système manque de RAM et a tué un processus.

**Action :**
- Ajouter de la RAM
- Optimiser l'utilisation mémoire
- Augmenter le swap

---

#### "SMART: Device /dev/sda has bad sectors"

**Signification :** Votre disque dur a des secteurs défectueux.

**Action :**
- Sauvegarder immédiatement vos données
- Vérifier l'état SMART : `sudo smartctl -a /dev/sda`
- Remplacer le disque si nécessaire

---

#### "authentication failure; logname= uid=0 euid=0"

**Signification :** Tentative d'authentification échouée (mauvais mot de passe).

**Action :**
- Si c'est vous : normal
- Si nombreuses tentatives d'IPs inconnues : tentative d'intrusion

---

#### "systemd[1]: Failed to start [service]"

**Signification :** Un service n'a pas pu démarrer.

**Action :**
- Vérifier les logs du service : `journalctl -u nom-service`
- Vérifier la configuration du service
- Vérifier les dépendances

---

## Bonnes pratiques

### 1. Consultez les logs régulièrement

**Routine hebdomadaire :**
```bash
# Vérifier les erreurs de la semaine
journalctl --since "7 days ago" -p err

# Vérifier les connexions suspectes
sudo grep "Failed password" /var/log/auth.log | tail -20
```

---

### 2. Nettoyez les logs régulièrement

```bash
# Nettoyer journalctl (garder 7 jours)
sudo journalctl --vacuum-time=7d

# Nettoyer les anciens logs compressés (si disque plein)
sudo find /var/log -name "*.gz" -mtime +30 -delete
```

---

### 3. Sauvegardez les logs importants

Avant une opération critique (mise à jour majeure, modification système) :

```bash
# Créer un dossier de sauvegarde
mkdir -p ~/logs-backup-$(date +%Y%m%d)

# Sauvegarder journalctl
journalctl -b > ~/logs-backup-$(date +%Y%m%d)/journalctl.txt

# Sauvegarder les logs principaux
sudo cp /var/log/syslog ~/logs-backup-$(date +%Y%m%d)/
sudo cp /var/log/auth.log ~/logs-backup-$(date +%Y%m%d)/
sudo cp /var/log/Xorg.0.log ~/logs-backup-$(date +%Y%m%d)/
```

---

### 4. Utilisez des alias pour les commandes fréquentes

Ajoutez dans `~/.bashrc` :

```bash
# Alias pour logs
alias logerr='journalctl -p err -xe'
alias logboot='journalctl -b -xe'
alias logfollow='journalctl -f'
alias logsyslog='sudo tail -f /var/log/syslog'
alias logauth='sudo tail -f /var/log/auth.log'
```

Rechargez :
```bash
source ~/.bashrc
```

Maintenant vous pouvez taper simplement `logerr` au lieu de `journalctl -p err -xe`.

---

### 5. Documentez vos découvertes

Quand vous résolvez un problème grâce aux logs, notez-le :

```bash
# Créer un fichier de notes
nano ~/problemes-resolus.txt

# Exemple d'entrée :
# Date : 2025-01-14
# Problème : Firefox plantait au démarrage
# Log trouvé : journalctl | grep firefox → segfault dans libgtk
# Solution : Réinstallé libgtk-3-0
# Commande : sudo apt install --reinstall libgtk-3-0
```

---

## Outils supplémentaires

### lnav (Log Navigator)

Outil avancé de navigation dans les logs.

```bash
# Installer
sudo apt install lnav

# Lancer (charge automatiquement les logs courants)
sudo lnav

# Ou spécifier des fichiers
lnav /var/log/syslog /var/log/auth.log
```

**Fonctionnalités :**
- Coloration syntaxique automatique
- Détection automatique de formats
- Recherche puissante
- Statistiques en temps réel
- Timeline visuelle

**Navigation :**
- **e/E** : Erreur suivante/précédente
- **w/W** : Warning suivant/précédent
- **/** : Rechercher
- **?** : Aide

---

### multitail

Afficher plusieurs logs côte à côte.

```bash
# Installer
sudo apt install multitail

# Exemples
multitail /var/log/syslog /var/log/auth.log
multitail -s 2 /var/log/syslog /var/log/kern.log  # 2 colonnes
```

---

### ccze

Colorisation de logs pour meilleure lisibilité.

```bash
# Installer
sudo apt install ccze

# Utiliser
tail -f /var/log/syslog | ccze -A

# Ou avec journalctl
journalctl -f | ccze -A
```

---

## FAQ - Questions fréquentes

### Où sont les logs de tel programme ?

**Applications système :** journalctl ou /var/log/syslog

**Applications utilisateur :**
- Vérifiez `~/.local/share/` ou `~/.cache/`
- Ou lancez l'application en terminal pour voir les messages

**Applications spécifiques :**
- Apache : `/var/log/apache2/`
- MySQL : `/var/log/mysql/`
- Nginx : `/var/log/nginx/`

---

### Les logs ralentissent-ils mon système ?

**Non**, l'impact est négligible.

**Exception :** Si le disque est plein à cause des logs, cela peut ralentir le système.

**Solution :** Nettoyez régulièrement (voir sections nettoyage ci-dessus).

---

### Puis-je supprimer des fichiers de logs ?

**Oui**, mais :
- Utilisez `sudo` (permissions nécessaires)
- Ne supprimez pas les fichiers actifs (ceux sans numéro ou .gz)
- Préférez vider plutôt que supprimer :

```bash
# Vider un log (le fichier reste mais est vidé)
sudo truncate -s 0 /var/log/syslog
```

---

### Comment activer la persistance de journalctl ?

Par défaut, journalctl ne persiste pas après redémarrage.

**Activer la persistance :**

```bash
# Créer le répertoire
sudo mkdir -p /var/log/journal

# Configurer
sudo nano /etc/systemd/journald.conf

# Modifier :
Storage=persistent

# Redémarrer le service
sudo systemctl restart systemd-journald
```

---

### Comment augmenter la verbosité des logs ?

Pour un service spécifique :

```bash
# Exemple avec NetworkManager
sudo nano /etc/NetworkManager/NetworkManager.conf

# Ajouter :
[logging]
level=DEBUG

# Redémarrer
sudo systemctl restart NetworkManager
```

**⚠️ Attention :** Mode DEBUG génère BEAUCOUP de logs.

---

## Commandes de référence rapide

### journalctl

```bash
# Basique
journalctl                    # Tous les logs
journalctl -b                 # Depuis le dernier boot
journalctl -f                 # Temps réel
journalctl -xe                # Fin + explications

# Filtres
journalctl -p err             # Uniquement erreurs
journalctl -u apache2         # Service spécifique
journalctl --since "1h ago"   # Depuis 1h
journalctl -n 50              # 50 dernières lignes

# Combinaisons
journalctl -b -p err -xe      # Erreurs du boot avec explications
journalctl -u nginx -f        # Nginx en temps réel

# Gestion
journalctl --disk-usage       # Espace utilisé
sudo journalctl --vacuum-time=7d  # Nettoyer (garder 7j)
```

### /var/log

```bash
# Lecture
tail /var/log/syslog          # Dernières lignes
tail -f /var/log/syslog       # Temps réel
less /var/log/syslog          # Navigation
grep "error" /var/log/syslog  # Recherche

# Logs spécifiques
sudo tail /var/log/auth.log   # Authentifications
tail /var/log/kern.log        # Kernel
tail /var/log/Xorg.0.log      # Serveur X
tail /var/log/apt/history.log # Installations

# Archives
zcat /var/log/syslog.2.gz     # Lire .gz
zgrep "error" /var/log/syslog*.gz  # Chercher dans .gz
```

### Recherche

```bash
# Grep basique
grep "error" fichier.log
grep -i "error" fichier.log   # Ignore casse
grep -r "error" /var/log/     # Récursif

# Grep avancé
grep -C 3 "error" fichier     # 3 lignes de contexte
grep -v "normal" fichier      # Inverse (exclure)
grep -E "error|fail" fichier  # Plusieurs mots (regex)
```

---

## Checklist de dépannage avec les logs

**☐ 1. Identifier le problème**
- Quand est-il apparu ?
- Quel composant est concerné ?

**☐ 2. Commencer par journalctl**
```bash
journalctl -xe
journalctl -b -p err
```

**☐ 3. Si problème spécifique à un service**
```bash
journalctl -u nom-service -xe
```

**☐ 4. Chercher dans les logs traditionnels**
```bash
sudo tail -100 /var/log/syslog | grep -i error
```

**☐ 5. Vérifier les logs spécialisés**
- Graphique → /var/log/Xorg.0.log
- Réseau → journalctl -u NetworkManager
- Sécurité → /var/log/auth.log

**☐ 6. Identifier le message d'erreur exact**
- Copier le message complet
- Noter l'heure exacte

**☐ 7. Rechercher la solution**
- Copier l'erreur dans Google
- Consulter forums Linux Mint / Ubuntu
- Vérifier la documentation du logiciel concerné

**☐ 8. Documenter la solution**
- Noter ce qui a fonctionné
- Pour référence future

---

## Conclusion

La lecture des logs est une compétence essentielle pour tout utilisateur Linux, du débutant à l'expert :

**Points clés à retenir :**

1. **Deux systèmes complémentaires** : journalctl (moderne) et /var/log (traditionnel)
2. **journalctl** est votre outil principal pour le diagnostic rapide
3. **/var/log** contient l'historique persistant et les logs des applications
4. **Concentrez-vous sur les erreurs** (niveaux err, crit, alert)
5. **Les logs ne mentent pas** : la réponse est toujours quelque part
6. **Nettoyez régulièrement** pour économiser l'espace disque
7. **Documentez vos découvertes** pour gagner du temps à l'avenir

**Méthodologie :**
- Identifiez le problème
- Consultez journalctl en premier
- Affinez avec des filtres (service, période, gravité)
- Recherchez dans les logs traditionnels si nécessaire
- Copiez l'erreur exacte pour chercher la solution

Avec la pratique, lire les logs deviendra une seconde nature, et vous serez capable de diagnostiquer et résoudre la plupart des problèmes par vous-même !

---

## Ressources complémentaires

- [Arch Wiki - systemd/Journal](https://wiki.archlinux.org/title/Systemd/Journal)
- [Ubuntu Wiki - Logs](https://help.ubuntu.com/community/LinuxLogFiles)
- [Freedesktop - journalctl](https://www.freedesktop.org/software/systemd/man/journalctl.html)
- [Logrotate documentation](https://linux.die.net/man/8/logrotate)

---

⏭️ [Outils de diagnostic (inxi, hardinfo)](/23-depannage-et-resolution-de-problemes/08-outils-de-diagnostic.md)
