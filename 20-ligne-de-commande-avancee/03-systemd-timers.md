🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Systemd timers (alternative moderne à cron)

## Introduction

**Systemd timers** est le système de planification de tâches moderne de Linux, intégré directement dans systemd (le gestionnaire de système et de services de Linux Mint). C'est une alternative plus puissante et flexible à cron traditionnel.

Imaginez systemd timers comme une version améliorée de cron, avec une meilleure intégration au système, des logs plus détaillés, et des fonctionnalités avancées.

### Pourquoi systemd timers ?

Vous vous demandez peut-être : "Pourquoi apprendre systemd timers alors que cron fonctionne bien ?"

**Avantages des systemd timers** :
- **Logs détaillés** : Intégration complète avec journalctl pour voir exactement ce qui s'est passé
- **Dépendances** : Peut attendre que d'autres services soient démarrés
- **Précision** : Planification à la microseconde (cron = minute minimum)
- **Gestion des ressources** : Contrôle fin sur l'utilisation CPU et mémoire
- **Statut en temps réel** : Voir facilement l'état de toutes vos tâches
- **Persistance** : Les tâches manquées peuvent être rattrapées
- **Conditions** : Exécution basée sur des conditions système complexes

### Systemd timers vs Cron

| Caractéristique | Cron | Systemd Timers |
|----------------|------|----------------|
| Syntaxe | Simple mais cryptique | Plus verbeux mais clair |
| Logs | Basiques (syslog) | Détaillés (journalctl) |
| Précision | Minutes | Microsecondes |
| Dépendances | Non | Oui |
| Gestion ressources | Non | Oui |
| Interface | Texte simple | Fichiers structurés |
| Persistance | Non | Oui (avec option) |
| État en temps réel | Limité | Complet |

**Quand utiliser quoi ?** :
- **Cron** : Tâches simples, scripts rapides, compatibilité universelle
- **Systemd timers** : Tâches système complexes, besoin de logs détaillés, dépendances

## Comprendre systemd timers

### Les deux fichiers nécessaires

Pour créer un timer systemd, vous avez besoin de **deux fichiers** :

1. **Fichier `.service`** : Définit CE qui doit être exécuté
2. **Fichier `.timer`** : Définit QUAND cela doit être exécuté

Par exemple :
- `backup.service` : Contient la commande de sauvegarde
- `backup.timer` : Indique quand lancer la sauvegarde

### Où placer ces fichiers ?

**Pour l'utilisateur courant** :
```bash
~/.config/systemd/user/
```

**Pour le système (root)** :
```bash
/etc/systemd/system/
```

Nous allons principalement utiliser les timers utilisateur, car ils ne nécessitent pas les droits root.

## Créer votre premier timer

### Exemple simple : Rappel quotidien

Créons un timer qui affiche une notification tous les jours à 9h.

**Étape 1 : Créer le répertoire**

```bash
mkdir -p ~/.config/systemd/user
```

**Étape 2 : Créer le fichier service**

```bash
nano ~/.config/systemd/user/rappel-quotidien.service
```

Contenu :

```ini
[Unit]
Description=Rappel quotidien matinal  
Documentation=man:notify-send(1)  

[Service]
Type=oneshot  
ExecStart=/usr/bin/notify-send "Bonjour !" "N'oubliez pas de faire votre sauvegarde quotidienne" --icon=dialog-information  
```

**Étape 3 : Créer le fichier timer**

```bash
nano ~/.config/systemd/user/rappel-quotidien.timer
```

Contenu :

```ini
[Unit]
Description=Timer pour le rappel quotidien  
Requires=rappel-quotidien.service  

[Timer]
OnCalendar=*-*-* 09:00:00  
Persistent=true  

[Install]
WantedBy=timers.target
```

**Étape 4 : Activer et démarrer le timer**

```bash
# Recharger systemd pour qu'il voit les nouveaux fichiers
systemctl --user daemon-reload

# Activer le timer (démarre automatiquement au boot)
systemctl --user enable rappel-quotidien.timer

# Démarrer le timer maintenant
systemctl --user start rappel-quotidien.timer
```

**Étape 5 : Vérifier l'état**

```bash
systemctl --user status rappel-quotidien.timer
```

Vous verrez quand le timer sera déclenché la prochaine fois.

### Lister tous vos timers

```bash
systemctl --user list-timers --all
```

Cette commande affiche :
- Tous vos timers actifs et inactifs
- La prochaine exécution planifiée
- La dernière exécution
- Le temps restant

## Anatomie d'un fichier .service

Décortiquons le fichier service :

```ini
[Unit]
Description=Description courte de ce que fait le service  
Documentation=man:commande(1)  
After=network.target  # Optionnel : attendre que le réseau soit actif  

[Service]
Type=oneshot          # Type d'exécution (oneshot = une fois puis s'arrête)  
User=utilisateur      # Optionnel : utilisateur qui exécute la commande  
WorkingDirectory=/home/utilisateur  # Optionnel : répertoire de travail  
ExecStart=/chemin/vers/commande     # La commande à exécuter  
StandardOutput=journal              # Où envoyer la sortie (journal = logs systemd)  
StandardError=journal               # Où envoyer les erreurs  

# Gestion des ressources (optionnel)
CPUQuota=20%          # Limiter à 20% du CPU  
MemoryLimit=500M      # Limiter à 500 Mo de RAM  

[Install]
WantedBy=multi-user.target  # Pour les services système
```

### Types de service

- **`oneshot`** : S'exécute une fois puis se termine (parfait pour les timers)
- **`simple`** : Processus principal qui reste en cours
- **`forking`** : Service qui se met en arrière-plan

Pour les timers, utilisez presque toujours **`oneshot`**.

## Anatomie d'un fichier .timer

Décortiquons le fichier timer :

```ini
[Unit]
Description=Description du timer  
Requires=mon-service.service  # Service associé (même nom sans .timer)  

[Timer]
# QUAND le timer se déclenche
OnCalendar=daily              # Chaque jour à minuit
# OU
OnBootSec=5min                # 5 minutes après le démarrage
# OU
OnUnitActiveSec=1h            # 1 heure après la dernière exécution

# Options
Persistent=true               # Rattraper les exécutions manquées  
AccuracySec=1min             # Fenêtre de précision (économie d'énergie)  
RandomizedDelaySec=10min     # Délai aléatoire (éviter surcharges simultanées)  

[Install]
WantedBy=timers.target        # Cible pour activation automatique
```

### Options de planification

#### OnCalendar (planification calendaire)

Format : `DayOfWeek Year-Month-Day Hour:Minute:Second`

**Exemples de syntaxe OnCalendar** :

```ini
# Tous les jours à minuit
OnCalendar=daily
# OU
OnCalendar=*-*-* 00:00:00

# Tous les jours à 14h30
OnCalendar=*-*-* 14:30:00

# Tous les lundis à 9h
OnCalendar=Mon *-*-* 09:00:00

# Le premier jour de chaque mois à 8h
OnCalendar=*-*-01 08:00:00

# Toutes les heures
OnCalendar=hourly
# OU
OnCalendar=*-*-* *:00:00

# Toutes les 15 minutes
OnCalendar=*-*-* *:00,15,30,45:00

# Du lundi au vendredi à 8h
OnCalendar=Mon..Fri *-*-* 08:00:00

# Deux fois par jour (10h et 22h)
OnCalendar=*-*-* 10,22:00:00

# Chaque trimestre (1er janvier, avril, juillet, octobre)
OnCalendar=*-01,04,07,10-01 00:00:00
```

**Raccourcis pratiques** :

| Raccourci | Équivalent | Signification |
|-----------|------------|---------------|
| `minutely` | `*-*-* *:*:00` | Chaque minute |
| `hourly` | `*-*-* *:00:00` | Chaque heure |
| `daily` | `*-*-* 00:00:00` | Chaque jour à minuit |
| `weekly` | `Mon *-*-* 00:00:00` | Chaque lundi |
| `monthly` | `*-*-01 00:00:00` | Le 1er de chaque mois |
| `yearly` | `*-01-01 00:00:00` | Le 1er janvier |

#### OnBootSec (relatif au démarrage)

```ini
# 5 minutes après le démarrage
OnBootSec=5min

# 1 heure après le démarrage
OnBootSec=1h

# 30 secondes après le démarrage
OnBootSec=30s
```

#### OnUnitActiveSec (relatif à la dernière exécution)

```ini
# 1 heure après la dernière exécution
OnUnitActiveSec=1h

# 30 minutes après la dernière exécution
OnUnitActiveSec=30min
```

Utile pour créer des tâches répétitives qui s'exécutent à intervalle fixe.

### Tester la syntaxe OnCalendar

Systemd fournit un outil pour vérifier votre syntaxe :

```bash
systemd-analyze calendar "Mon..Fri *-*-* 09:00:00"
```

Résultat :
```
  Original form: Mon..Fri *-*-* 09:00:00
Normalized form: Mon..Fri *-*-* 09:00:00
    Next elapse: Mon 2024-01-15 09:00:00 CET
       (in UTC): Mon 2024-01-15 08:00:00 UTC
       From now: 2 days 5h left
```

## Exemples pratiques

### Exemple 1 : Sauvegarde quotidienne

**Fichier : `~/.config/systemd/user/backup-documents.service`**

```ini
[Unit]
Description=Sauvegarde quotidienne des documents  
After=network.target  

[Service]
Type=oneshot  
ExecStart=/usr/bin/tar -czf /home/utilisateur/Sauvegardes/docs_%Y%m%d.tar.gz /home/utilisateur/Documents  
StandardOutput=journal  
StandardError=journal  
```

**Fichier : `~/.config/systemd/user/backup-documents.timer`**

```ini
[Unit]
Description=Timer pour sauvegarde quotidienne  
Requires=backup-documents.service  

[Timer]
OnCalendar=daily  
Persistent=true  

[Install]
WantedBy=timers.target
```

**Activation** :

```bash
systemctl --user daemon-reload  
systemctl --user enable --now backup-documents.timer  
```

### Exemple 2 : Nettoyage hebdomadaire

**Fichier : `~/.config/systemd/user/nettoyage-hebdo.service`**

```ini
[Unit]
Description=Nettoyage hebdomadaire du système

[Service]
Type=oneshot  
ExecStart=/bin/bash -c 'rm -rf ~/.cache/thumbnails/* && rm -rf ~/.local/share/Trash/*'  
StandardOutput=journal  
```

**Fichier : `~/.config/systemd/user/nettoyage-hebdo.timer`**

```ini
[Unit]
Description=Timer pour nettoyage hebdomadaire  
Requires=nettoyage-hebdo.service  

[Timer]
OnCalendar=Sun 03:00:00  
Persistent=true  

[Install]
WantedBy=timers.target
```

### Exemple 3 : Vérification de l'espace disque toutes les heures

**Fichier : `~/.config/systemd/user/check-disk.service`**

```ini
[Unit]
Description=Vérification de l'espace disque

[Service]
Type=oneshot  
ExecStart=/home/utilisateur/scripts/check-disk.sh  
StandardOutput=journal  
StandardError=journal  
```

**Fichier script : `~/scripts/check-disk.sh`**

```bash
#!/bin/bash
USAGE=$(df / | tail -1 | awk '{print $5}' | sed 's/%//')

if [ $USAGE -gt 80 ]; then
    notify-send -u critical "Alerte disque" "Espace disque utilisé : ${USAGE}%"
    echo "ALERTE : Espace disque à ${USAGE}%"
    exit 1
else
    echo "OK : Espace disque à ${USAGE}%"
fi
```

```bash
chmod +x ~/scripts/check-disk.sh
```

**Fichier : `~/.config/systemd/user/check-disk.timer`**

```ini
[Unit]
Description=Vérification horaire de l'espace disque  
Requires=check-disk.service  

[Timer]
OnCalendar=hourly  
Persistent=true  

[Install]
WantedBy=timers.target
```

### Exemple 4 : Synchronisation cloud toutes les 2 heures

**Fichier : `~/.config/systemd/user/sync-cloud.service`**

```ini
[Unit]
Description=Synchronisation avec le cloud  
After=network-online.target  
Wants=network-online.target  

[Service]
Type=oneshot  
ExecStart=/usr/bin/rclone sync /home/utilisateur/Documents remote:Documents  
StandardOutput=journal  
StandardError=journal  
TimeoutSec=600  
```

**Fichier : `~/.config/systemd/user/sync-cloud.timer`**

```ini
[Unit]
Description=Timer de synchronisation cloud  
Requires=sync-cloud.service  

[Timer]
OnCalendar=*-*-* 00/2:00:00  
Persistent=true  
RandomizedDelaySec=5min  

[Install]
WantedBy=timers.target
```

### Exemple 5 : Script au démarrage (avec délai)

**Fichier : `~/.config/systemd/user/startup-script.service`**

```ini
[Unit]
Description=Script de démarrage personnalisé  
After=graphical-session.target  

[Service]
Type=oneshot  
ExecStart=/home/utilisateur/scripts/startup.sh  
StandardOutput=journal  
```

**Fichier : `~/.config/systemd/user/startup-script.timer`**

```ini
[Unit]
Description=Exécution du script au démarrage  
Requires=startup-script.service  

[Timer]
OnBootSec=2min  
Persistent=true  

[Install]
WantedBy=timers.target
```

## Commandes essentielles

### Gestion des timers utilisateur

```bash
# Recharger après modification de fichiers
systemctl --user daemon-reload

# Lister tous les timers
systemctl --user list-timers --all

# Activer un timer (démarre au boot)
systemctl --user enable nom-timer.timer

# Démarrer un timer maintenant
systemctl --user start nom-timer.timer

# Activer ET démarrer en une commande
systemctl --user enable --now nom-timer.timer

# Arrêter un timer
systemctl --user stop nom-timer.timer

# Désactiver un timer (ne démarre plus au boot)
systemctl --user disable nom-timer.timer

# Voir l'état d'un timer
systemctl --user status nom-timer.timer

# Voir l'état du service associé
systemctl --user status nom-timer.service

# Déclencher manuellement le service (test)
systemctl --user start nom-timer.service
```

### Gestion des timers système (root)

Même chose sans `--user` et avec `sudo` :

```bash
# Lister les timers système
sudo systemctl list-timers --all

# Activer un timer système
sudo systemctl enable --now nom-timer.timer

# Voir l'état
sudo systemctl status nom-timer.timer
```

### Commandes de diagnostic

```bash
# Voir les logs d'un service
journalctl --user -u nom-timer.service

# Voir les logs en temps réel
journalctl --user -u nom-timer.service -f

# Voir les dernières 50 lignes
journalctl --user -u nom-timer.service -n 50

# Voir les logs depuis aujourd'hui
journalctl --user -u nom-timer.service --since today

# Voir les logs de la dernière heure
journalctl --user -u nom-timer.service --since "1 hour ago"

# Voir les logs entre deux dates
journalctl --user -u nom-timer.service --since "2024-01-01" --until "2024-01-31"
```

## Logs et surveillance

### Voir tous les logs d'un service

```bash
journalctl --user -u backup-documents.service
```

### Voir uniquement les erreurs

```bash
journalctl --user -u backup-documents.service -p err
```

Niveaux de priorité :
- `emerg` : Urgence (0)
- `alert` : Alerte (1)
- `crit` : Critique (2)
- `err` : Erreur (3)
- `warning` : Avertissement (4)
- `notice` : Notice (5)
- `info` : Information (6)
- `debug` : Débogage (7)

### Surveiller l'exécution en temps réel

```bash
# Dans un terminal, lancez :
journalctl --user -u backup-documents.service -f

# Dans un autre terminal, déclenchez le service :
systemctl --user start backup-documents.service
```

### Vérifier la prochaine exécution

```bash
systemctl --user list-timers
```

Affiche une liste avec :
- **NEXT** : Prochaine exécution planifiée
- **LEFT** : Temps restant
- **LAST** : Dernière exécution
- **PASSED** : Temps écoulé depuis la dernière exécution

### Exemple de sortie

```
NEXT                        LEFT          LAST                        PASSED       UNIT                     ACTIVATES  
Mon 2024-01-15 09:00:00 CET 2h 30min left Sun 2024-01-14 09:00:00 CET 21h ago     rappel-quotidien.timer   rappel-quotidien.service  
Mon 2024-01-15 00:00:00 CET 17h left      Sun 2024-01-14 00:00:00 CET 6h ago      backup-documents.timer   backup-documents.service  
Sun 2024-01-21 03:00:00 CET 6 days left   Sun 2024-01-14 03:00:00 CET 3h ago      nettoyage-hebdo.timer    nettoyage-hebdo.service  
```

## Scripts complexes avec systemd

### Script de sauvegarde avancé

**Fichier : `~/scripts/backup-advanced.sh`**

```bash
#!/bin/bash
#
# Script de sauvegarde avancé pour systemd timer
#

set -e  # Arrêter en cas d'erreur

# Configuration
SOURCE="/home/$USER/Documents"  
DEST="/home/$USER/Sauvegardes"  
MAX_BACKUPS=7  
DATE=$(date +%Y%m%d_%H%M%S)  
BACKUP_NAME="backup_$DATE.tar.gz"  
LOG_PREFIX="[BACKUP]"  

# Fonction de log (utilise echo, systemd capturera via journal)
log() {
    echo "$LOG_PREFIX $1"
}

log "Début de la sauvegarde"  
log "Source : $SOURCE"  
log "Destination : $DEST/$BACKUP_NAME"  

# Vérifications
if [ ! -d "$SOURCE" ]; then
    log "ERREUR : Le répertoire source n'existe pas"
    exit 1
fi

mkdir -p "$DEST"

# Création de la sauvegarde
log "Compression en cours..."  
tar -czf "$DEST/$BACKUP_NAME" "$SOURCE"  

if [ $? -eq 0 ]; then
    SIZE=$(du -h "$DEST/$BACKUP_NAME" | cut -f1)
    log "Sauvegarde réussie : $BACKUP_NAME ($SIZE)"
else
    log "ERREUR : Échec de la sauvegarde"
    exit 1
fi

# Rotation des anciennes sauvegardes
log "Rotation des sauvegardes..."  
BACKUP_COUNT=$(ls -1 "$DEST"/backup_*.tar.gz 2>/dev/null | wc -l)  

if [ $BACKUP_COUNT -gt $MAX_BACKUPS ]; then
    TO_DELETE=$((BACKUP_COUNT - MAX_BACKUPS))
    log "Suppression de $TO_DELETE ancienne(s) sauvegarde(s)"
    ls -1t "$DEST"/backup_*.tar.gz | tail -n $TO_DELETE | xargs rm -f
fi

log "Nombre de sauvegardes : $(ls -1 "$DEST"/backup_*.tar.gz | wc -l)/$MAX_BACKUPS"  
log "Sauvegarde terminée avec succès"  
```

**Fichier : `~/.config/systemd/user/backup-advanced.service`**

```ini
[Unit]
Description=Sauvegarde avancée avec rotation  
After=network.target  

[Service]
Type=oneshot  
ExecStart=/home/utilisateur/scripts/backup-advanced.sh  
StandardOutput=journal  
StandardError=journal  
TimeoutSec=600  

# Gestion des ressources
CPUQuota=50%  
IOWeight=100  
```

**Fichier : `~/.config/systemd/user/backup-advanced.timer`**

```ini
[Unit]
Description=Timer pour sauvegarde avancée quotidienne  
Requires=backup-advanced.service  

[Timer]
OnCalendar=daily  
Persistent=true  
AccuracySec=1min  
RandomizedDelaySec=10min  

[Install]
WantedBy=timers.target
```

## Migration depuis cron vers systemd timers

### Tableau de conversion

| Cron | Systemd Timer |
|------|---------------|
| `0 2 * * *` | `OnCalendar=*-*-* 02:00:00` |
| `*/15 * * * *` | `OnCalendar=*-*-* *:00,15,30,45:00` |
| `0 0 * * 0` | `OnCalendar=Sun *-*-* 00:00:00` |
| `0 0 1 * *` | `OnCalendar=*-*-01 00:00:00` |
| `0 9-17 * * 1-5` | `OnCalendar=Mon..Fri *-*-* 09..17:00:00` |
| `@reboot` | `OnBootSec=1min` |
| `@daily` | `OnCalendar=daily` |
| `@hourly` | `OnCalendar=hourly` |

### Exemple de migration

**Avant (cron)** :
```cron
0 2 * * * /home/utilisateur/scripts/backup.sh
```

**Après (systemd)** :

**backup.service** :
```ini
[Unit]
Description=Sauvegarde quotidienne

[Service]
Type=oneshot  
ExecStart=/home/utilisateur/scripts/backup.sh  
StandardOutput=journal  
StandardError=journal  
```

**backup.timer** :
```ini
[Unit]
Description=Timer pour sauvegarde quotidienne  
Requires=backup.service  

[Timer]
OnCalendar=*-*-* 02:00:00  
Persistent=true  

[Install]
WantedBy=timers.target
```

## Fonctionnalités avancées

### Conditions d'exécution

Vous pouvez ajouter des conditions dans la section `[Unit]` :

```ini
[Unit]
Description=Synchronisation cloud
# N'exécuter que si le réseau est actif
ConditionPathExists=/sys/class/net/wlan0
# N'exécuter que si AC (secteur) branché
ConditionACPower=true
# N'exécuter que si le système n'est pas sur batterie
ConditionVirtualization=no

[Service]
Type=oneshot  
ExecStart=/usr/bin/rclone sync /home/utilisateur/Documents remote:Documents  
```

### Exécution avec limites de ressources

```ini
[Service]
Type=oneshot  
ExecStart=/home/utilisateur/scripts/tache-lourde.sh  

# Limites de ressources
CPUQuota=25%              # Max 25% d'un cœur CPU  
MemoryLimit=500M          # Max 500 Mo de RAM  
IOWeight=50               # Priorité I/O basse (1-10000, défaut 100)  
Nice=19                   # Priorité CPU basse (-20 à 19, défaut 0)  
```

### Retry automatique en cas d'échec

```ini
[Service]
Type=oneshot  
ExecStart=/home/utilisateur/scripts/backup.sh  
Restart=on-failure  
RestartSec=5min  
```

### Exécutions multiples

Vous pouvez avoir plusieurs déclencheurs dans un même timer :

```ini
[Timer]
# Tous les jours à 2h
OnCalendar=*-*-* 02:00:00
# ET au démarrage
OnBootSec=5min
# ET toutes les 6 heures
OnUnitActiveSec=6h

Persistent=true

[Install]
WantedBy=timers.target
```

### Dépendances entre services

```ini
[Unit]
Description=Sauvegarde cloud  
After=backup-local.service  
Requires=backup-local.service  

[Service]
Type=oneshot  
ExecStart=/home/utilisateur/scripts/backup-cloud.sh  
```

Ce service ne s'exécutera qu'après `backup-local.service` et seulement si celui-ci a réussi.

## Bonnes pratiques

### 1. Toujours utiliser Type=oneshot pour les timers

```ini
[Service]
Type=oneshot
```

C'est le type adapté aux tâches qui se terminent.

### 2. Activer Persistent pour rattraper les exécutions manquées

```ini
[Timer]
Persistent=true
```

Surtout important pour les ordinateurs portables qui s'éteignent.

### 3. Utiliser StandardOutput=journal

```ini
[Service]
StandardOutput=journal  
StandardError=journal  
```

Les logs seront accessibles via `journalctl`.

### 4. Ajouter des timeouts pour éviter les blocages

```ini
[Service]
TimeoutSec=600  # 10 minutes max
```

### 5. Utiliser des chemins absolus

```ini
# ✅ Bon
ExecStart=/usr/bin/tar -czf /home/utilisateur/backup.tar.gz /home/utilisateur/Documents

# ❌ Mauvais
ExecStart=tar -czf ~/backup.tar.gz ~/Documents
```

### 6. Tester avant d'activer

```bash
# 1. Créer les fichiers
nano ~/.config/systemd/user/test.service  
nano ~/.config/systemd/user/test.timer  

# 2. Recharger
systemctl --user daemon-reload

# 3. Tester le service manuellement
systemctl --user start test.service

# 4. Vérifier les logs
journalctl --user -u test.service

# 5. Si OK, activer le timer
systemctl --user enable --now test.timer
```

### 7. Commenter vos fichiers

```ini
[Unit]
Description=Description claire de ce que fait le timer
# Créé le 2024-01-15 pour sauvegardes quotidiennes
# Auteur : Jean Dupont
```

### 8. Utiliser AccuracySec pour économiser l'énergie

```ini
[Timer]
OnCalendar=daily  
AccuracySec=1h  # Peut se déclencher dans une fenêtre d'1h  
```

Systemd regroupera les tâches pour économiser la batterie.

### 9. Ajouter RandomizedDelaySec pour éviter les surcharges

```ini
[Timer]
OnCalendar=hourly  
RandomizedDelaySec=10min  # Délai aléatoire jusqu'à 10 min  
```

Utile si vous avez beaucoup de timers qui se déclenchent en même temps.

### 10. Documenter vos timers

Créez un fichier README listant tous vos timers :

```bash
nano ~/scripts/TIMERS.md
```

Exemple de contenu :
```markdown
# Mes timers systemd

## backup-documents.timer
- Fréquence : Quotidien à 2h
- Fonction : Sauvegarde de ~/Documents
- Emplacement : ~/.config/systemd/user/

## check-disk.timer
- Fréquence : Toutes les heures
- Fonction : Vérification espace disque
- Alerte si > 80%
```

## Dépannage

### Mon timer ne se déclenche pas

**1. Vérifier que le timer est actif**

```bash
systemctl --user list-timers --all
```

Le timer doit apparaître comme "active".

**2. Vérifier l'état du timer**

```bash
systemctl --user status mon-timer.timer
```

**3. Vérifier les logs**

```bash
journalctl --user -u mon-timer.timer  
journalctl --user -u mon-timer.service  
```

**4. Tester le service manuellement**

```bash
systemctl --user start mon-timer.service
```

Si ça fonctionne manuellement mais pas avec le timer, le problème est dans la configuration du timer.

**5. Vérifier la syntaxe OnCalendar**

```bash
systemd-analyze calendar "votre-syntaxe"
```

### Les timers utilisateur ne persistent pas après logout

Par défaut, les services utilisateur s'arrêtent quand vous vous déconnectez. Pour changer ça :

```bash
loginctl enable-linger $USER
```

Maintenant vos timers utilisateur continueront même après déconnexion.

### Vérifier si linger est activé

```bash
loginctl show-user $USER | grep Linger
```

Devrait afficher : `Linger=yes`

### Mon service échoue avec "Permission denied"

Vérifiez les permissions du script :

```bash
ls -l ~/scripts/mon-script.sh  
chmod +x ~/scripts/mon-script.sh  
```

### Les chemins relatifs ne fonctionnent pas

Utilisez toujours des chemins absolus dans les fichiers service :

```ini
# ❌ Ne fonctionnera pas
ExecStart=~/scripts/backup.sh

# ✅ Fonctionnera
ExecStart=/home/utilisateur/scripts/backup.sh
```

## Outils utiles

### Vérifier la validité des fichiers systemd

```bash
systemd-analyze verify ~/.config/systemd/user/mon-timer.service  
systemd-analyze verify ~/.config/systemd/user/mon-timer.timer  
```

### Créer un calendrier visuel

```bash
systemd-analyze calendar "Mon..Fri 09:00" --iterations=10
```

Affiche les 10 prochaines occurrences.

### Voir toutes les propriétés d'un timer

```bash
systemctl --user show mon-timer.timer
```

### Éditer un timer rapidement

```bash
systemctl --user edit --full mon-timer.timer
```

## Conclusion

Systemd timers est un système puissant et flexible pour planifier vos tâches sous Linux Mint. Bien qu'il soit un peu plus complexe que cron au début, il offre :

- ✅ Des logs détaillés et facilement accessibles
- ✅ Une meilleure gestion des dépendances
- ✅ Plus de contrôle sur les ressources système
- ✅ Une intégration parfaite avec systemd
- ✅ La possibilité de rattraper les tâches manquées

**Quand utiliser systemd timers** :
- Tâches système complexes
- Besoin de logs détaillés
- Dépendances entre services
- Contrôle précis de l'exécution
- Gestion fine des ressources

**Quand rester sur cron** :
- Tâches très simples
- Scripts rapides
- Besoin de compatibilité universelle
- Vous êtes déjà à l'aise avec cron

Avec la pratique, systemd timers deviendra un outil indispensable pour automatiser intelligemment votre système Linux ! ⏰🚀

⏭️ [Expressions régulières (regex)](/20-ligne-de-commande-avancee/04-expressions-regulieres.md)
