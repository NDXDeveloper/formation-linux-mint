🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 18.5 Gestion et rotation des logs

## Introduction

Imaginez votre système Linux comme un grand immeuble. Les **logs** (journaux de bord) sont comme les carnets de sécurité où tout est enregistré : qui entre, qui sort, les incidents, les réparations, les alertes, etc. Ces carnets sont essentiels pour comprendre ce qui se passe, mais ils peuvent rapidement remplir des étagères entières !

**Dans ce chapitre, vous apprendrez à :**
- Comprendre ce que sont les logs et pourquoi ils sont importants
- Localiser et lire les logs système
- Utiliser journalctl pour consulter les logs modernes
- Gérer la rotation automatique des logs
- Nettoyer les vieux logs pour libérer de l'espace
- Configurer la rétention des logs selon vos besoins

**Pourquoi c'est important ?**
- **Diagnostic** : comprendre pourquoi quelque chose ne fonctionne pas
- **Sécurité** : détecter les tentatives d'intrusion
- **Optimisation** : identifier les processus problématiques
- **Espace disque** : les logs peuvent occuper plusieurs gigaoctets

---

## Qu'est-ce qu'un log ?

### Définition simple

Un **log** (ou journal) est un fichier texte dans lequel le système et les applications enregistrent chronologiquement tout ce qui se passe :
- Démarrages et arrêts de services
- Erreurs et avertissements
- Connexions utilisateurs
- Installations de logiciels
- Accès réseau
- Et bien plus encore

### Exemple concret de log

Voici à quoi ressemble un extrait de log typique :

```
Nov 29 10:23:15 mint-pc systemd[1]: Started Network Manager.
Nov 29 10:23:16 mint-pc NetworkManager[845]: <info> NetworkManager (version 1.44.2) is starting...
Nov 29 10:23:16 mint-pc NetworkManager[845]: <info> WiFi enabled by radio killswitch
Nov 29 10:23:17 mint-pc kernel: iwlwifi 0000:03:00.0: Detected Intel(R) Wireless AC 9260
Nov 29 10:23:18 mint-pc NetworkManager[845]: <info> WiFi hardware radio set enabled
```

**Décodage :**
- **Nov 29 10:23:15** : date et heure
- **mint-pc** : nom de l'ordinateur
- **systemd[1]** : processus qui a généré le message (ici systemd avec PID 1)
- **Started Network Manager** : le message proprement dit

### Les différents niveaux de gravité

Les logs classifient les messages par niveau d'importance :

| Niveau | Nom | Signification | Exemple |
|--------|-----|---------------|---------|
| 0 | **EMERG** | Urgence, système inutilisable | Noyau en panique |
| 1 | **ALERT** | Action immédiate requise | Disque plein |
| 2 | **CRIT** | Critique | Matériel défaillant |
| 3 | **ERR** | Erreur | Service qui ne démarre pas |
| 4 | **WARNING** | Avertissement | Mémoire basse |
| 5 | **NOTICE** | Notice normale | Service démarré |
| 6 | **INFO** | Information | Connexion utilisateur |
| 7 | **DEBUG** | Débogage | Détails techniques |

**Pour un débutant :**
- **ERR et au-dessus** → Problème à investiguer
- **WARNING** → À surveiller
- **INFO et DEBUG** → Informations normales

### Pourquoi les logs grossissent-ils ?

**Sources de croissance :**
1. **Services bavards** : certains programmes enregistrent beaucoup d'informations
2. **Erreurs répétées** : un service qui plante et redémarre génère beaucoup de logs
3. **Applications web** : serveurs qui enregistrent chaque requête
4. **Pas de nettoyage** : sans rotation, les logs s'accumulent indéfiniment

**Exemple :** Un serveur web peut générer 1 Go de logs par jour !

---

## Où se trouvent les logs ?

### L'arborescence traditionnelle : /var/log

La plupart des logs se trouvent dans le répertoire `/var/log`.

**Voir les logs disponibles :**
```bash
ls -lh /var/log
```

**Structure typique :**
```
/var/log/
├── syslog              # Journal système général (anciennes distributions)
├── kern.log            # Messages du noyau Linux
├── auth.log            # Authentifications et sécurité
├── dpkg.log            # Installations/suppressions de paquets
├── apt/                # Historique des commandes apt
│   ├── history.log
│   └── term.log
├── cups/               # Logs d'impression
├── lightdm/            # Logs du gestionnaire de connexion
├── Xorg.0.log          # Logs du serveur X (interface graphique)
└── journal/            # Logs systemd (binaires)
```

### Les logs principaux à connaître

**1. Journal système (méthode moderne : journald)**
```bash
# Géré par systemd, consulté avec journalctl
journalctl
```

**2. auth.log - Sécurité et authentifications**
```bash
sudo cat /var/log/auth.log
```
Enregistre :
- Connexions SSH
- Utilisation de sudo
- Échecs de connexion
- Changements de mots de passe

**3. kern.log - Messages du noyau**
```bash
sudo cat /var/log/kern.log
```
Enregistre :
- Détection de matériel
- Pilotes chargés
- Erreurs matérielles

**4. dpkg.log - Gestion des paquets**
```bash
cat /var/log/dpkg.log
```
Enregistre :
- Installations de logiciels
- Mises à jour
- Suppressions

**5. Xorg.0.log - Serveur graphique**
```bash
cat /var/log/Xorg.0.log
```
Enregistre :
- Initialisation de l'interface graphique
- Problèmes de pilotes graphiques
- Résolutions d'écran

**6. boot.log - Démarrage système**
```bash
sudo journalctl -b
```
Messages générés au démarrage du système.

### Permissions des logs

La plupart des logs nécessitent les droits root pour être lus.

**Lire un log protégé :**
```bash
sudo cat /var/log/auth.log
```

**Lire en temps réel (suivre les nouveaux messages) :**
```bash
sudo tail -f /var/log/auth.log
```

**Note :** `tail -f` affiche les dernières lignes et continue d'afficher les nouvelles en temps réel (pratique pour le débogage).

---

## Lire et comprendre les logs

### Méthode 1 : Avec cat (affichage complet)

**Afficher tout le contenu d'un log :**
```bash
sudo cat /var/log/syslog
```

**Problème :** Les logs peuvent contenir des milliers de lignes. Utilisez plutôt les outils de pagination.

### Méthode 2 : Avec less (navigation confortable)

**Ouvrir un log avec less :**
```bash
sudo less /var/log/syslog
```

**Navigation dans less :**
| Touche | Action |
|--------|--------|
| `Espace` | Page suivante |
| `b` | Page précédente |
| `/mot` | Rechercher "mot" |
| `n` | Occurrence suivante |
| `N` | Occurrence précédente |
| `G` | Aller à la fin du fichier |
| `g` | Aller au début du fichier |
| `q` | Quitter |

**Exemple d'utilisation :**
1. Ouvrez : `sudo less /var/log/syslog`
2. Tapez `/error` pour rechercher le mot "error"
3. Appuyez sur `n` pour passer d'une erreur à l'autre
4. Appuyez sur `q` pour quitter

### Méthode 3 : Avec tail (dernières lignes)

**Afficher les 20 dernières lignes :**
```bash
sudo tail -n 20 /var/log/syslog
```

**Suivre en temps réel (très utile !) :**
```bash
sudo tail -f /var/log/syslog
```

Cela affiche les nouvelles lignes au fur et à mesure qu'elles sont écrites. Parfait pour déboguer un problème en direct.

**Arrêter le suivi :** `Ctrl+C`

### Méthode 4 : Avec head (premières lignes)

**Afficher les 20 premières lignes :**
```bash
sudo head -n 20 /var/log/syslog
```

### Méthode 5 : Avec grep (filtrage)

**Rechercher un mot spécifique :**
```bash
sudo grep "error" /var/log/syslog
```

**Rechercher plusieurs fichiers :**
```bash
sudo grep "error" /var/log/*.log
```

**Ignorer la casse (majuscules/minuscules) :**
```bash
sudo grep -i "error" /var/log/syslog
```

**Afficher les lignes avec contexte (3 lignes avant et après) :**
```bash
sudo grep -C 3 "error" /var/log/syslog
```

**Compter les occurrences :**
```bash
sudo grep -c "error" /var/log/syslog
```

### Combiner les commandes avec des pipes

**Exemple 1 : Voir les 10 dernières erreurs**
```bash
sudo grep "error" /var/log/syslog | tail -n 10
```

**Exemple 2 : Compter les tentatives de connexion échouées**
```bash
sudo grep "Failed password" /var/log/auth.log | wc -l
```

**Exemple 3 : Afficher uniquement les erreurs d'aujourd'hui**
```bash
sudo grep "Nov 29" /var/log/syslog | grep -i error
```

---

## journalctl : L'outil moderne de consultation des logs

Depuis systemd, Linux utilise **journald** pour centraliser tous les logs. L'outil **journalctl** permet de les consulter facilement.

### Pourquoi journalctl ?

**Avantages par rapport aux fichiers texte classiques :**
- Centralise tous les logs système
- Filtrage puissant (par service, date, priorité...)
- Pas besoin de sudo pour les logs non sensibles
- Format structuré et interrogeable
- Coloration syntaxique automatique

### Commandes journalctl essentielles

#### Afficher tous les logs

```bash
journalctl
```

**Navigation :** Comme `less` (espace, `q` pour quitter)

#### Afficher les logs en temps réel

```bash
journalctl -f
```

Équivalent de `tail -f` pour tous les logs système.

#### Afficher les logs du démarrage actuel

```bash
journalctl -b
```

**Uniquement les logs depuis le dernier démarrage.**

#### Afficher les logs d'un démarrage précédent

**Lister les démarrages disponibles :**
```bash
journalctl --list-boots
```

**Résultat :**
```
-2 abc123... Sat 2024-11-23 09:15:32 CET—Sat 2024-11-24 18:30:45 CET
-1 def456... Sun 2024-11-24 18:31:02 CET—Mon 2024-11-25 22:15:30 CET
 0 ghi789... Mon 2024-11-25 22:16:01 CET—Tue 2024-11-26 10:23:45 CET
```

**Afficher les logs du démarrage précédent :**
```bash
journalctl -b -1
```

**Afficher les logs d'il y a 2 démarrages :**
```bash
journalctl -b -2
```

#### Filtrer par niveau de priorité

**Afficher uniquement les erreurs :**
```bash
journalctl -p err
```

**Niveaux disponibles :**
- `emerg` (0)
- `alert` (1)
- `crit` (2)
- `err` (3)
- `warning` (4)
- `notice` (5)
- `info` (6)
- `debug` (7)

**Afficher erreurs et warnings :**
```bash
journalctl -p warning
```

(Affiche warning et tout ce qui est plus grave : err, crit, alert, emerg)

#### Filtrer par service (unité systemd)

**Afficher les logs de NetworkManager :**
```bash
journalctl -u NetworkManager
```

**Afficher les logs de SSH :**
```bash
journalctl -u ssh
```

**En temps réel :**
```bash
journalctl -u NetworkManager -f
```

#### Filtrer par période

**Depuis aujourd'hui :**
```bash
journalctl --since today
```

**Depuis hier :**
```bash
journalctl --since yesterday
```

**Depuis une heure spécifique :**
```bash
journalctl --since "2024-11-29 10:00:00"
```

**Entre deux dates :**
```bash
journalctl --since "2024-11-28" --until "2024-11-29"
```

**Dernières 2 heures :**
```bash
journalctl --since "2 hours ago"
```

**Derniers 30 minutes :**
```bash
journalctl --since "30 min ago"
```

#### Combiner les filtres

**Erreurs du service SSH depuis aujourd'hui :**
```bash
journalctl -u ssh -p err --since today
```

**Logs de NetworkManager du dernier démarrage :**
```bash
journalctl -b -u NetworkManager
```

#### Afficher en ordre inverse (plus récent en premier)

```bash
journalctl -r
```

#### Afficher uniquement les N dernières lignes

```bash
journalctl -n 50
```

Affiche les 50 dernières lignes (par défaut : 10).

#### Afficher avec plus de détails

```bash
journalctl -o verbose
```

**Formats de sortie disponibles :**
- `short` : format par défaut (concis)
- `verbose` : tous les détails
- `json` : format JSON (pour scripts)
- `cat` : seulement les messages, sans métadonnées

#### Afficher l'utilisation du disque par les logs

```bash
journalctl --disk-usage
```

**Résultat exemple :**
```
Archived and active journals take up 512.2M in the file system.
```

---

## Rotation des logs : Logrotate

### Qu'est-ce que la rotation des logs ?

La **rotation** consiste à :
1. Archiver les vieux logs
2. Compresser les archives
3. Supprimer les très anciennes archives
4. Créer un nouveau fichier de log vide

**Exemple de rotation :**
```
syslog           ← Log actuel (nouvelles entrées)
syslog.1         ← Rotation d'hier (non compressé)
syslog.2.gz      ← Rotation d'avant-hier (compressé)
syslog.3.gz      ← Rotation d'il y a 3 jours
...
syslog.7.gz      ← Rotation d'il y a 7 jours (sera supprimé demain)
```

**Sans rotation :** Un seul fichier `syslog` de 50 Go !

**Avec rotation :** 7 fichiers compressés totalisant 500 Mo.

### Logrotate : Le gestionnaire de rotation

**logrotate** est l'outil standard pour gérer la rotation des logs sous Linux.

**Vérifier qu'il est installé :**
```bash
logrotate --version
```

**Fichier de configuration principal :**
```bash
cat /etc/logrotate.conf
```

**Configurations spécifiques par application :**
```bash
ls /etc/logrotate.d/
```

**Résultat :**
```
apt
cups
dpkg
rsyslog
nginx
mysql
...
```

Chaque fichier configure la rotation pour un service spécifique.

### Exemple de configuration logrotate

**Voir la configuration de rsyslog :**
```bash
cat /etc/logrotate.d/rsyslog
```

**Contenu typique :**
```
/var/log/syslog
{
    rotate 7
    daily
    missingok
    notifempty
    delaycompress
    compress
    postrotate
        /usr/lib/rsyslog/rsyslog-rotate
    endscript
}
```

**Explication ligne par ligne :**

- `/var/log/syslog` : fichier concerné
- `rotate 7` : conserve 7 rotations (7 jours de logs)
- `daily` : rotation quotidienne
- `missingok` : pas d'erreur si le fichier n'existe pas
- `notifempty` : ne pas faire de rotation si le fichier est vide
- `delaycompress` : compresse la rotation précédente (pas celle d'aujourd'hui)
- `compress` : utilise gzip pour compresser
- `postrotate ... endscript` : commande à exécuter après rotation

**Autres options courantes :**

- `weekly` : rotation hebdomadaire
- `monthly` : rotation mensuelle
- `size 100M` : rotation quand le fichier atteint 100 Mo
- `maxage 90` : supprime les logs de plus de 90 jours
- `create 0640 root adm` : crée le nouveau fichier avec ces permissions

### Tester une configuration logrotate

**Tester sans réellement faire la rotation (mode debug) :**
```bash
sudo logrotate -d /etc/logrotate.conf
```

**Forcer la rotation immédiatement :**
```bash
sudo logrotate -f /etc/logrotate.conf
```

**Forcer uniquement pour rsyslog :**
```bash
sudo logrotate -f /etc/logrotate.d/rsyslog
```

### Créer sa propre configuration de rotation

**Exemple : Vous avez une application qui génère des logs dans `/var/log/monapp.log`**

1. Créez un fichier de configuration :
```bash
sudo nano /etc/logrotate.d/monapp
```

2. Ajoutez la configuration :
```
/var/log/monapp.log {
    daily
    rotate 30
    compress
    missingok
    notifempty
    create 0644 user user
}
```

3. Sauvegardez et testez :
```bash
sudo logrotate -d /etc/logrotate.d/monapp
```

**Cette configuration :**
- Rotation quotidienne
- Conserve 30 jours de logs
- Compresse les anciennes rotations
- Crée le nouveau fichier avec les permissions 0644

---

## Gestion des logs systemd (journald)

### Configuration de journald

Les logs systemd (journald) sont configurés dans `/etc/systemd/journald.conf`.

**Voir la configuration :**
```bash
cat /etc/systemd/journald.conf
```

**Configuration par défaut (commentée avec #) :**
```
[Journal]
#Storage=auto
#Compress=yes
#Seal=yes
#SplitMode=uid
#SyncIntervalSec=5m
#RateLimitIntervalSec=30s
#RateLimitBurst=10000
#SystemMaxUse=
#SystemKeepFree=
#SystemMaxFileSize=
#SystemMaxFiles=100
#RuntimeMaxUse=
#RuntimeKeepFree=
#RuntimeMaxFileSize=
#RuntimeMaxFiles=100
#MaxRetentionSec=
#MaxFileSec=1month
#ForwardToSyslog=yes
#ForwardToKMsg=no
#ForwardToConsole=no
#ForwardToWall=yes
#TTYPath=/dev/console
#MaxLevelStore=debug
#MaxLevelSyslog=debug
#MaxLevelKMsg=notice
#MaxLevelConsole=info
#MaxLevelWall=emerg
#LineMax=48K
#ReadKMsg=yes
#Audit=yes
```

### Options importantes à connaître

**Limiter l'espace disque utilisé :**

Éditez le fichier :
```bash
sudo nano /etc/systemd/journald.conf
```

Décommentez et modifiez :
```
SystemMaxUse=500M
```

Cela limite les logs journald à 500 Mo maximum.

**Autres options utiles :**

```
SystemMaxUse=500M         # Taille max totale des logs
SystemKeepFree=1G         # Espace à laisser libre sur le disque
SystemMaxFileSize=100M    # Taille max d'un fichier de log
MaxRetentionSec=2week     # Supprime les logs de plus de 2 semaines
MaxFileSec=1month         # Un fichier de log par mois maximum
```

**Appliquer les changements :**
```bash
sudo systemctl restart systemd-journald
```

### Nettoyer manuellement les logs journald

#### Voir l'espace utilisé

```bash
journalctl --disk-usage
```

**Résultat :**
```
Archived and active journals take up 1.2G in the file system.
```

#### Supprimer les logs de plus de X jours

**Supprimer les logs de plus de 3 jours :**
```bash
sudo journalctl --vacuum-time=3d
```

**Supprimer les logs de plus de 2 semaines :**
```bash
sudo journalctl --vacuum-time=2weeks
```

**Supprimer les logs de plus de 1 mois :**
```bash
sudo journalctl --vacuum-time=1month
```

#### Limiter la taille totale des logs

**Réduire à 500 Mo maximum :**
```bash
sudo journalctl --vacuum-size=500M
```

**Réduire à 1 Go maximum :**
```bash
sudo journalctl --vacuum-size=1G
```

#### Garder seulement N fichiers de logs

**Garder seulement les 5 derniers fichiers :**
```bash
sudo journalctl --vacuum-files=5
```

#### Vérifier le gain après nettoyage

```bash
journalctl --disk-usage
```

### Rotation automatique avec journald

Journald effectue automatiquement une rotation basée sur la configuration.

**Par défaut :**
- Un nouveau fichier journal est créé chaque mois (`MaxFileSec=1month`)
- Les anciens fichiers sont conservés tant qu'ils ne dépassent pas `SystemMaxUse`

**Pour une rotation plus agressive :**

```bash
sudo nano /etc/systemd/journald.conf
```

Modifiez :
```
SystemMaxUse=500M
MaxRetentionSec=1week
MaxFileSec=1day
```

Redémarrez :
```bash
sudo systemctl restart systemd-journald
```

**Cette configuration :**
- Limite à 500 Mo
- Supprime les logs de plus d'une semaine
- Crée un nouveau fichier chaque jour

---

## Nettoyage manuel des vieux logs

### Supprimer les logs compressés anciens

**Supprimer tous les fichiers .gz de plus de 30 jours :**
```bash
sudo find /var/log -name "*.gz" -type f -mtime +30 -delete
```

**Explication :**
- `find /var/log` : cherche dans /var/log
- `-name "*.gz"` : fichiers se terminant par .gz
- `-type f` : seulement les fichiers (pas les dossiers)
- `-mtime +30` : modifiés il y a plus de 30 jours
- `-delete` : supprime

**⚠️ Attention :** Testez d'abord SANS `-delete` :
```bash
sudo find /var/log -name "*.gz" -type f -mtime +30
```

Vérifiez la liste, puis ajoutez `-delete` si tout est OK.

### Vider un log sans le supprimer

**Pour vider complètement un fichier log tout en le conservant :**
```bash
sudo truncate -s 0 /var/log/syslog
```

**Ou :**
```bash
sudo sh -c '> /var/log/syslog'
```

**Cas d'usage :** Un log a gonflé à 10 Go et vous voulez repartir de zéro.

### Supprimer les logs de dpkg (paquets)

Les logs dpkg peuvent occuper beaucoup d'espace.

**Voir la taille :**
```bash
du -sh /var/log/dpkg.log*
```

**Supprimer les vieilles rotations :**
```bash
sudo rm /var/log/dpkg.log.*.gz
```

**Garder seulement dpkg.log et dpkg.log.1 :**
```bash
sudo rm /var/log/dpkg.log.{2..12}.gz
```

### Nettoyer les logs apt

```bash
sudo rm /var/log/apt/*.gz
```

---

## Surveiller la taille des logs

### Commande du : Voir l'espace utilisé

**Taille totale de /var/log :**
```bash
sudo du -sh /var/log
```

**Résultat :**
```
1.2G    /var/log
```

**Taille de chaque sous-dossier :**
```bash
sudo du -h /var/log | sort -rh | head -n 20
```

**Explication :**
- `du -h /var/log` : taille de chaque dossier
- `sort -rh` : trie par taille décroissante
- `head -n 20` : affiche les 20 plus gros

**Résultat typique :**
```
1.2G    /var/log
850M    /var/log/journal
200M    /var/log/apt
50M     /var/log/lightdm
...
```

### Script de surveillance automatique

Créez un script qui vous alerte si les logs dépassent 1 Go :

```bash
nano ~/check-logs-size.sh
```

Contenu :
```bash
#!/bin/bash

LOG_SIZE=$(sudo du -sm /var/log | cut -f1)

if [ "$LOG_SIZE" -gt 1000 ]; then
    notify-send "⚠️ Logs volumineux" "Les logs occupent ${LOG_SIZE} Mo. Pensez à nettoyer !"
    echo "$(date): Logs à ${LOG_SIZE} Mo" >> ~/logs-alerts.txt
fi
```

Rendez-le exécutable :
```bash
chmod +x ~/check-logs-size.sh
```

**Automatisez avec cron (chaque semaine) :**
```bash
crontab -e
```

Ajoutez :
```
0 10 * * 1 ~/check-logs-size.sh
```

(S'exécute tous les lundis à 10h)

---

## Outils graphiques pour consulter les logs

### 1. Logs (gnome-logs) - Recommandé pour débutants

**Installation :**
```bash
sudo apt install gnome-logs
```

**Lancement :**
Menu > **Administration** > **Journaux** (ou "Logs")

**Fonctionnalités :**
- Interface graphique simple et épurée
- Lecture des logs systemd (journalctl)
- Filtrage par importance, démarrage, application
- Recherche intégrée
- Pas besoin de sudo

**Utilisation :**
1. Lancez l'application
2. Sélectionnez la catégorie (Tout, Important, Système, Sécurité, Matériel)
3. Cliquez sur un démarrage pour voir les logs de ce boot
4. Utilisez la barre de recherche pour filtrer

**Parfait pour :** Débutants qui veulent consulter les logs sans ligne de commande.

### 2. KSystemLog (KDE)

Si vous utilisez KDE Plasma :

**Installation :**
```bash
sudo apt install ksystemlog
```

**Fonctionnalités :**
- Lecture de multiples fichiers logs
- Onglets pour chaque type de log
- Filtrage et recherche
- Coloration syntaxique

### 3. Gestionnaire de journaux système (autre nom pour gnome-logs)

Déjà préinstallé dans certaines versions de Linux Mint.

---

## Cas pratiques : Diagnostiquer avec les logs

### Problème : L'ordinateur a redémarré tout seul

**Étape 1 : Vérifier les logs du dernier boot**
```bash
journalctl -b -1 -p err
```

Cherchez des messages comme :
- `kernel panic`
- `Out of memory`
- `Hardware error`

**Étape 2 : Vérifier les logs du noyau**
```bash
sudo grep -i "kernel" /var/log/syslog | tail -n 50
```

### Problème : Une application ne démarre pas

**Étape 1 : Voir les logs de cette application (exemple : nginx)**
```bash
journalctl -u nginx -n 50
```

**Étape 2 : Vérifier les erreurs**
```bash
journalctl -u nginx -p err
```

### Problème : Tentatives de connexion suspectes

**Voir les échecs de connexion SSH :**
```bash
sudo grep "Failed password" /var/log/auth.log
```

**Compter le nombre de tentatives :**
```bash
sudo grep "Failed password" /var/log/auth.log | wc -l
```

**Identifier les adresses IP :**
```bash
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -rn
```

### Problème : Ralentissements après le démarrage

**Voir quels services ont pris du temps au démarrage :**
```bash
systemd-analyze blame
```

**Voir les erreurs au boot :**
```bash
journalctl -b -p err
```

### Problème : Disque plein

**Vérifier si ce sont les logs :**
```bash
sudo du -sh /var/log
journalctl --disk-usage
```

**Nettoyer :**
```bash
sudo journalctl --vacuum-size=500M
sudo find /var/log -name "*.gz" -mtime +30 -delete
```

---

## Configuration optimale pour différents profils

### Profil 1 : Utilisateur de bureau standard

**Objectif :** Équilibre entre diagnostic et espace disque

**Configuration journald :**
```bash
sudo nano /etc/systemd/journald.conf
```

```
SystemMaxUse=500M
MaxRetentionSec=2weeks
MaxFileSec=1week
```

**Rotation logrotate :**
Garder la configuration par défaut (7 jours pour la plupart des logs).

**Nettoyage mensuel :**
```bash
sudo journalctl --vacuum-time=2weeks
sudo find /var/log -name "*.gz" -mtime +14 -delete
```

### Profil 2 : Utilisateur avec SSD limité (128 Go)

**Objectif :** Minimiser l'espace utilisé par les logs

**Configuration journald :**
```bash
sudo nano /etc/systemd/journald.conf
```

```
SystemMaxUse=200M
MaxRetentionSec=1week
MaxFileSec=3days
```

**Rotation logrotate plus agressive :**
```bash
sudo nano /etc/logrotate.d/rsyslog
```

Changez `rotate 7` en `rotate 3`.

**Nettoyage hebdomadaire automatisé :**
Créez `/etc/cron.weekly/clean-logs` :
```bash
#!/bin/bash
journalctl --vacuum-time=1week
find /var/log -name "*.gz" -mtime +7 -delete
```

### Profil 3 : Développeur / Administrateur système

**Objectif :** Garder beaucoup d'historique pour diagnostic

**Configuration journald :**
```bash
sudo nano /etc/systemd/journald.conf
```

```
SystemMaxUse=2G
MaxRetentionSec=3months
MaxFileSec=1month
```

**Rotation logrotate :**
```bash
sudo nano /etc/logrotate.d/rsyslog
```

```
rotate 30
compress
```

**Logs de debug activés :**
Pour certains services critiques, activez les logs détaillés.

---

## Bonnes pratiques de gestion des logs

### ✅ À faire régulièrement

1. **Vérifier l'espace disque des logs** (une fois par mois)
   ```bash
   sudo du -sh /var/log
   journalctl --disk-usage
   ```

2. **Nettoyer les vieux logs** (tous les 3 mois)
   ```bash
   sudo journalctl --vacuum-time=1month
   sudo find /var/log -name "*.gz" -mtime +30 -delete
   ```

3. **Consulter les erreurs récentes** (hebdomadaire)
   ```bash
   journalctl -p err --since "1 week ago"
   ```

4. **Vérifier la rotation automatique** (une fois)
   ```bash
   sudo logrotate -d /etc/logrotate.conf
   ```

### ❌ À éviter

1. **Ne supprimez jamais** `/var/log` complètement
2. **Ne videz pas** les logs actifs (non-rotationnés) sans raison
3. **Ne désactivez pas** complètement les logs (besoin pour diagnostics)
4. **N'éditez pas** manuellement les fichiers logs (risque de corruption)

### 🎯 Objectifs de taille

**Système de bureau standard :**
- `/var/log` : < 1 Go
- journald : < 500 Mo
- Logs de plus de 1 mois : supprimés

**Serveur :**
- `/var/log` : 2-5 Go (selon l'activité)
- journald : 1-2 Go
- Logs de plus de 3 mois : archivés ou supprimés

---

## Script de maintenance complet des logs

Voici un script tout-en-un pour maintenir vos logs propres :

```bash
nano ~/maintenance-logs.sh
```

Contenu :
```bash
#!/bin/bash

echo "🧹 Maintenance des logs système"
echo "==============================="
echo ""

# 1. Afficher l'espace actuel
echo "📊 Espace disque des logs AVANT nettoyage :"
echo "-------------------------------------------"
sudo du -sh /var/log
journalctl --disk-usage
echo ""

# 2. Nettoyer journald (garder 2 semaines)
echo "🗑️  Nettoyage de journald (conservation : 2 semaines)..."
sudo journalctl --vacuum-time=2weeks

# 3. Supprimer les .gz de plus de 30 jours
echo "🗑️  Suppression des logs compressés de plus de 30 jours..."
DELETED=$(sudo find /var/log -name "*.gz" -type f -mtime +30 | wc -l)
sudo find /var/log -name "*.gz" -type f -mtime +30 -delete
echo "   → $DELETED fichiers supprimés"

# 4. Nettoyer les logs apt
echo "🗑️  Nettoyage des logs APT..."
sudo rm -f /var/log/apt/*.gz

# 5. Afficher l'espace final
echo ""
echo "📊 Espace disque des logs APRÈS nettoyage :"
echo "-------------------------------------------"
sudo du -sh /var/log
journalctl --disk-usage
echo ""

echo "✅ Maintenance terminée !"
echo ""
echo "💡 Conseils :"
echo "  - Lancez ce script tous les 3 mois"
echo "  - Vérifiez les erreurs avec : journalctl -p err --since today"
echo "  - Surveillez l'espace avec : df -h"
```

Rendez-le exécutable :
```bash
chmod +x ~/maintenance-logs.sh
```

Exécutez-le :
```bash
~/maintenance-logs.sh
```

**Automatisation recommandée :**
Ajoutez à cron pour exécution trimestrielle :
```bash
crontab -e
```

Ajoutez :
```
0 3 1 */3 * ~/maintenance-logs.sh
```

(S'exécute le 1er jour de chaque trimestre à 3h du matin)

---

## Résumé des commandes essentielles

### Consultation des logs

| Commande | Utilité |
|----------|---------|
| `journalctl` | Tous les logs systemd |
| `journalctl -f` | Suivre en temps réel |
| `journalctl -b` | Logs du démarrage actuel |
| `journalctl -p err` | Uniquement les erreurs |
| `journalctl -u service` | Logs d'un service spécifique |
| `journalctl --since today` | Logs d'aujourd'hui |
| `sudo tail -f /var/log/syslog` | Suivre syslog en temps réel |
| `sudo grep "error" /var/log/syslog` | Rechercher dans les logs |

### Nettoyage des logs

| Commande | Utilité |
|----------|---------|
| `journalctl --disk-usage` | Voir l'espace utilisé |
| `sudo journalctl --vacuum-time=2weeks` | Supprimer logs > 2 semaines |
| `sudo journalctl --vacuum-size=500M` | Limiter à 500 Mo |
| `sudo find /var/log -name "*.gz" -mtime +30 -delete` | Supprimer .gz > 30 jours |
| `sudo du -sh /var/log` | Taille totale de /var/log |

### Configuration

| Fichier | Rôle |
|---------|------|
| `/etc/systemd/journald.conf` | Configuration journald |
| `/etc/logrotate.conf` | Configuration globale logrotate |
| `/etc/logrotate.d/` | Configurations spécifiques |
| `/var/log/` | Répertoire des logs |

---

## Conclusion

La gestion des logs est un aspect **essentiel** mais souvent négligé de la maintenance système.

**Les points clés à retenir :**

1. **Les logs sont vos alliés** pour diagnostiquer les problèmes
2. **journalctl** est l'outil moderne à maîtriser
3. **La rotation automatique** est activée par défaut (logrotate)
4. **Nettoyez régulièrement** pour éviter de saturer le disque
5. **Configurez intelligemment** selon votre profil d'utilisation

**Configuration recommandée pour la plupart des utilisateurs :**
- journald limité à 500 Mo
- Rétention de 2 semaines
- Nettoyage manuel tous les 3 mois
- Consultation des erreurs en cas de problème

**Avec ces connaissances, vous maîtrisez maintenant la gestion des logs comme un pro !** 📝🚀

---

## Pour aller plus loin

- **Section 18.1** : Nettoyage du système (libérer de l'espace disque)
- **Section 18.3** : Surveillance des ressources (htop, btop)
- **Section 18.4** : Optimisation SSD (éviter l'usure par logs excessifs)
- **Section 23.7** : Lecture et compréhension des logs (diagnostic approfondi)
- **Section 20.2** : Cron et tâches planifiées (automatiser le nettoyage)

**Documentation :**
- `man journalctl`
- `man logrotate`
- `man rsyslog`
- Documentation systemd : https://www.freedesktop.org/software/systemd/man/journald.conf.html

⏭️ [Analyse de l'espace disque (Baobab, ncdu)](/18-maintenance-et-optimisation/06-analyse-de-lespace-disque.md)
