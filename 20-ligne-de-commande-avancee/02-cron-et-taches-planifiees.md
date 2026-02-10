🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Cron et tâches planifiées (crontab, anacron)

## Introduction

Imaginez pouvoir dire à votre ordinateur : "Tous les jours à 3h du matin, fais une sauvegarde de mes documents" ou "Tous les lundis, nettoie les fichiers temporaires". C'est exactement ce que permet **cron**, un planificateur de tâches automatique sous Linux.

Cron fonctionne comme un réveil programmable qui peut déclencher l'exécution de scripts ou de commandes à des moments précis, de façon répétée.

### À quoi sert cron ?

- **Sauvegardes automatiques** : Exécuter des sauvegardes régulières sans y penser
- **Maintenance système** : Nettoyer les fichiers temporaires, mettre à jour le système
- **Téléchargements** : Lancer des téléchargements à des heures creuses
- **Rapports** : Générer des rapports quotidiens ou hebdomadaires
- **Surveillance** : Vérifier l'état du système périodiquement
- **Mise à jour de données** : Synchroniser des fichiers, rafraîchir des informations

### Cron vs Anacron

- **Cron** : Pour les machines qui restent allumées en permanence (serveurs)
- **Anacron** : Pour les ordinateurs portables et de bureau qui s'éteignent régulièrement

Sur Linux Mint, les deux sont installés et travaillent ensemble intelligemment.

## Comprendre la syntaxe de crontab

### Le fichier crontab

Chaque utilisateur a son propre fichier **crontab** (contraction de "cron table") qui contient la liste de ses tâches planifiées.

### La syntaxe de base

Une ligne crontab ressemble à ceci :

```
* * * * * commande_à_exécuter
│ │ │ │ │
│ │ │ │ └─── Jour de la semaine (0-7, 0 et 7 = dimanche)
│ │ │ └───── Mois (1-12)
│ │ └─────── Jour du mois (1-31)
│ └───────── Heure (0-23)
└─────────── Minute (0-59)
```

### Exemples pour comprendre

| Syntaxe | Signification |
|---------|---------------|
| `30 2 * * *` | Tous les jours à 2h30 |
| `0 0 * * 0` | Tous les dimanches à minuit |
| `*/15 * * * *` | Toutes les 15 minutes |
| `0 9-17 * * 1-5` | Toutes les heures de 9h à 17h, du lundi au vendredi |
| `0 0 1 * *` | Le premier jour de chaque mois à minuit |
| `0 0 1 1 *` | Le 1er janvier à minuit |

### Les caractères spéciaux

- **`*`** : Toutes les valeurs possibles
  - Exemple : `* * * * *` = chaque minute

- **`,`** : Liste de valeurs
  - Exemple : `0 9,12,18 * * *` = à 9h, 12h et 18h

- **`-`** : Plage de valeurs
  - Exemple : `0 9-17 * * *` = toutes les heures de 9h à 17h

- **`/`** : Intervalles
  - Exemple : `*/10 * * * *` = toutes les 10 minutes

### Noms abrégés pour les jours et mois

Vous pouvez utiliser les abréviations (en anglais) :

- **Jours** : `sun`, `mon`, `tue`, `wed`, `thu`, `fri`, `sat`
- **Mois** : `jan`, `feb`, `mar`, `apr`, `may`, `jun`, `jul`, `aug`, `sep`, `oct`, `nov`, `dec`

Exemple :
```
0 9 * * mon-fri  # Du lundi au vendredi à 9h
0 0 1 jan *      # Le 1er janvier à minuit
```

### Raccourcis pratiques

Cron propose des raccourcis pour les périodes courantes :

| Raccourci | Équivalent | Signification |
|-----------|------------|---------------|
| `@reboot` | - | Au démarrage du système |
| `@yearly` ou `@annually` | `0 0 1 1 *` | Une fois par an |
| `@monthly` | `0 0 1 * *` | Une fois par mois |
| `@weekly` | `0 0 * * 0` | Une fois par semaine |
| `@daily` ou `@midnight` | `0 0 * * *` | Une fois par jour |
| `@hourly` | `0 * * * *` | Toutes les heures |

Exemple :
```
@daily /home/utilisateur/scripts/sauvegarde.sh
```

## Utiliser crontab

### Éditer votre crontab

Pour ouvrir et éditer votre fichier crontab :

```bash
crontab -e
```

La première fois, le système vous demandera quel éditeur utiliser. Pour les débutants, choisissez **nano** (option 1 généralement).

### Ajouter une tâche planifiée

Une fois dans l'éditeur, ajoutez vos lignes. Exemple :

```bash
# Sauvegarde quotidienne à 2h du matin
0 2 * * * /home/utilisateur/scripts/sauvegarde.sh

# Nettoyage des fichiers temporaires tous les dimanches à 3h
0 3 * * 0 /usr/bin/find /tmp -type f -atime +7 -delete

# Mise à jour de la liste des paquets tous les jours à 6h
0 6 * * * /usr/bin/apt update
```

**Important :**
- Utilisez toujours des **chemins absolus** dans cron
- Ajoutez des commentaires (lignes commençant par `#`) pour vous souvenir de ce que fait chaque tâche

Sauvegardez avec `Ctrl+O`, puis quittez avec `Ctrl+X`.

### Lister vos tâches planifiées

Pour voir toutes vos tâches cron actuelles :

```bash
crontab -l
```

### Supprimer toutes vos tâches

**Attention**, cette commande supprime TOUTES vos tâches cron :

```bash
crontab -r
```

Pour une suppression avec confirmation :

```bash
crontab -ir
```

### Supprimer une seule tâche

Éditez votre crontab et supprimez la ligne correspondante :

```bash
crontab -e
```

## Exemples pratiques de tâches cron

### 1. Sauvegarde automatique quotidienne

```bash
# Sauvegarde des documents tous les jours à 2h
0 2 * * * tar -czf /home/utilisateur/Sauvegardes/docs_$(date +\%Y\%m\%d).tar.gz /home/utilisateur/Documents
```

**Note** : Le `%` doit être échappé avec `\%` dans crontab.

### 2. Nettoyage hebdomadaire

```bash
# Nettoyage système tous les dimanches à 3h
0 3 * * 0 /usr/bin/apt autoremove -y && /usr/bin/apt autoclean
```

### 3. Rappel quotidien

```bash
# Notification tous les jours à 9h
0 9 * * * DISPLAY=:0 notify-send "Rappel" "N'oubliez pas votre réunion !"
```

### 4. Synchronisation périodique

```bash
# Synchronisation avec le cloud toutes les 2 heures
0 */2 * * * /usr/bin/rclone sync /home/utilisateur/Documents remote:Documents
```

### 5. Surveillance de l'espace disque

```bash
# Vérification quotidienne de l'espace disque
0 8 * * * df -h / | tail -1 | awk '{if ($5+0 > 80) print "ALERTE: Disque plein à " $5}' | mail -s "Alerte disque" utilisateur@example.com
```

### 6. Téléchargement automatique

```bash
# Téléchargement de podcasts tous les lundis à 6h
0 6 * * 1 /home/utilisateur/scripts/telecharger_podcasts.sh
```

### 7. Redémarrage de service

```bash
# Redémarrage d'un service toutes les 6 heures
0 */6 * * * /usr/bin/systemctl restart mon-service
```

### 8. Mise à jour automatique

```bash
# Mise à jour complète tous les samedis à 4h
0 4 * * 6 /usr/bin/apt update && /usr/bin/apt upgrade -y
```

## Script complet pour cron

Créons un script de maintenance à lancer régulièrement :

**Fichier : `/home/utilisateur/scripts/maintenance.sh`**

```bash
#!/bin/bash
#
# Script de maintenance système
# À lancer via cron
#

# Configuration
LOG_FILE="$HOME/maintenance.log"  
DATE=$(date '+%Y-%m-%d %H:%M:%S')  

# Fonction de log
log() {
    echo "[$DATE] $1" >> "$LOG_FILE"
}

# Début
log "=== Début de la maintenance ==="

# 1. Nettoyage APT
log "Nettoyage APT..."  
apt autoremove -y >> "$LOG_FILE" 2>&1  
apt autoclean >> "$LOG_FILE" 2>&1  

# 2. Vider la corbeille
log "Vidage de la corbeille..."  
rm -rf "$HOME/.local/share/Trash/"* >> "$LOG_FILE" 2>&1  

# 3. Nettoyage des logs anciens
log "Nettoyage des logs..."  
find /var/log -type f -name "*.log" -mtime +30 -delete 2>/dev/null  

# 4. Vérification de l'espace disque
espace=$(df / | tail -1 | awk '{print $5}' | sed 's/%//')  
log "Espace disque utilisé : $espace%"  

if [ $espace -gt 80 ]; then
    log "ALERTE : Espace disque critique !"
    DISPLAY=:0 notify-send "Alerte disque" "Espace disque : $espace%" -u critical
fi

# 5. Sauvegarde rapide
log "Sauvegarde des fichiers de configuration..."  
tar -czf "$HOME/Sauvegardes/config_$(date +%Y%m%d).tar.gz" \  
    "$HOME/.bashrc" \
    "$HOME/.profile" \
    2>> "$LOG_FILE"

# Fin
log "=== Maintenance terminée ==="  
log ""  
```

Rendez-le exécutable :

```bash
chmod +x ~/scripts/maintenance.sh
```

Puis ajoutez-le à crontab pour qu'il s'exécute tous les dimanches à 3h :

```bash
crontab -e
```

Ajoutez :
```
0 3 * * 0 /home/utilisateur/scripts/maintenance.sh
```

## Variables d'environnement dans cron

Cron exécute les tâches dans un environnement minimal. Vous pouvez définir des variables au début de votre crontab :

```bash
# Variables d'environnement
SHELL=/bin/bash  
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin  
MAILTO=utilisateur@example.com  
HOME=/home/utilisateur  

# Tâches
0 2 * * * /home/utilisateur/scripts/sauvegarde.sh
```

### Variables utiles

- **`SHELL`** : Le shell à utiliser (par défaut `/bin/sh`)
- **`PATH`** : Chemins de recherche des commandes
- **`MAILTO`** : Adresse email pour recevoir les sorties des commandes
- **`HOME`** : Répertoire personnel
- **`DISPLAY`** : Nécessaire pour les notifications graphiques (`:0` généralement)

### Exemple avec notification graphique

```bash
# Pour les notifications
DISPLAY=:0  
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus  

# Notification quotidienne
0 9 * * * notify-send "Bonjour" "Votre session commence !"
```

## Logs et débogage

### Où sont les logs de cron ?

Les logs de cron se trouvent généralement dans :

```bash
/var/log/syslog
```

Pour voir les logs cron en temps réel :

```bash
sudo tail -f /var/log/syslog | grep CRON
```

Pour voir les dernières exécutions :

```bash
sudo grep CRON /var/log/syslog | tail -20
```

### Rediriger les sorties vers un fichier

Pour capturer les sorties (succès et erreurs) de vos tâches cron :

```bash
# Redirection de tout vers un fichier log
0 2 * * * /home/utilisateur/scripts/sauvegarde.sh >> /home/utilisateur/logs/sauvegarde.log 2>&1
```

**Explication** :
- `>>` : Ajoute à la fin du fichier (au lieu d'écraser)
- `2>&1` : Redirige aussi les erreurs (stderr) vers le fichier

### Redirection sélective

```bash
# Seulement les erreurs
0 2 * * * /home/utilisateur/scripts/sauvegarde.sh 2>> /home/utilisateur/logs/erreurs.log

# Seulement les succès
0 2 * * * /home/utilisateur/scripts/sauvegarde.sh >> /home/utilisateur/logs/succes.log 2>/dev/null

# Tout séparer
0 2 * * * /home/utilisateur/scripts/sauvegarde.sh >> /home/utilisateur/logs/sortie.log 2>> /home/utilisateur/logs/erreurs.log
```

### Supprimer complètement les sorties

Si vous ne voulez aucune sortie :

```bash
0 2 * * * /home/utilisateur/scripts/sauvegarde.sh > /dev/null 2>&1
```

### Tester une tâche cron

Avant d'ajouter une tâche à crontab, testez-la manuellement :

```bash
# Testez la commande exacte que cron exécutera
/chemin/absolu/vers/script.sh
```

### Ajouter des logs dans vos scripts

Ajoutez des logs détaillés dans vos scripts pour faciliter le débogage :

```bash
#!/bin/bash
LOG="/home/utilisateur/logs/mon_script.log"  
echo "$(date) - Début du script" >> "$LOG"  

# Votre code ici

echo "$(date) - Fin du script" >> "$LOG"
```

## Anacron : Pour les ordinateurs de bureau

### Qu'est-ce qu'Anacron ?

**Anacron** est complémentaire à cron. Il est conçu pour les machines qui ne sont pas allumées 24h/24.

**Le problème avec cron** :
- Si votre ordinateur est éteint à 2h du matin quand une tâche doit s'exécuter, elle ne s'exécutera jamais
- Anacron résout ce problème en exécutant les tâches manquées au prochain démarrage

### Comment fonctionne Anacron ?

Anacron vérifie régulièrement si des tâches auraient dû être exécutées. Si c'est le cas et que la machine était éteinte, il les exécute au prochain démarrage ou à un moment opportun.

### Configuration d'Anacron

Le fichier de configuration est `/etc/anacrontab` :

```bash
sudo nano /etc/anacrontab
```

Contenu typique :

```bash
# /etc/anacrontab: configuration file for anacron

# Période  Délai  ID-job          Commande
1          5      cron.daily      nice run-parts /etc/cron.daily
7          10     cron.weekly     nice run-parts /etc/cron.weekly
30         15     cron.monthly    nice run-parts /etc/cron.monthly
```

**Explication des colonnes** :

1. **Période** : Nombre de jours entre chaque exécution
   - `1` = tous les jours
   - `7` = toutes les semaines
   - `30` = tous les mois

2. **Délai** : Nombre de minutes à attendre après le démarrage avant d'exécuter la tâche

3. **ID-job** : Identifiant unique de la tâche

4. **Commande** : Commande à exécuter

### Les répertoires cron système

Linux Mint utilise des répertoires pratiques pour organiser les tâches :

```
/etc/cron.hourly/    # Scripts exécutés toutes les heures
/etc/cron.daily/     # Scripts exécutés tous les jours
/etc/cron.weekly/    # Scripts exécutés toutes les semaines
/etc/cron.monthly/   # Scripts exécutés tous les mois
```

### Ajouter un script dans cron.daily

**Étape 1** : Créez votre script

```bash
sudo nano /etc/cron.daily/mon-nettoyage
```

**Étape 2** : Écrivez le script

```bash
#!/bin/bash
# Nettoyage quotidien automatique

# Vider les corbeilles de tous les utilisateurs
find /home -type d -name "Trash" -exec rm -rf {}/* \; 2>/dev/null

# Nettoyer les fichiers temporaires
find /tmp -type f -atime +3 -delete

# Nettoyer le cache APT
apt-get autoclean -y
```

**Étape 3** : Rendez-le exécutable

```bash
sudo chmod +x /etc/cron.daily/mon-nettoyage
```

C'est tout ! Le script s'exécutera automatiquement chaque jour.

### Tester l'exécution d'un répertoire cron

Pour tester manuellement tous les scripts d'un répertoire :

```bash
sudo run-parts /etc/cron.daily
```

### Vérifier quand Anacron a exécuté les tâches

```bash
cat /var/spool/anacron/cron.daily  
cat /var/spool/anacron/cron.weekly  
cat /var/spool/anacron/cron.monthly  
```

Ces fichiers contiennent la date de la dernière exécution.

## Cron utilisateur vs Cron système

### Cron utilisateur

- **Fichier** : Édité avec `crontab -e`
- **Permissions** : S'exécute avec les permissions de l'utilisateur
- **Usage** : Tâches personnelles (sauvegardes de documents, scripts personnels)

```bash
# Exemple de cron utilisateur
crontab -e
```

### Cron système

- **Fichier** : `/etc/crontab` ou répertoires `/etc/cron.*/`
- **Permissions** : S'exécute avec les permissions root
- **Usage** : Maintenance système, tâches globales

```bash
# Exemple de cron système
sudo nano /etc/crontab
```

Le format de `/etc/crontab` inclut le nom de l'utilisateur :

```
# m h dom mon dow user  command
0 2 * * *   root   /usr/local/bin/maintenance.sh
0 3 * * 0   www-data /usr/local/bin/backup-web.sh
```

## Exemples avancés de planification

### Combinaisons complexes

```bash
# Tous les jours ouvrés (lundi à vendredi) à 8h
0 8 * * 1-5 /home/utilisateur/scripts/start-work.sh

# Le dernier jour de chaque mois à minuit (nécessite un script)
0 0 28-31 * * [ $(date -d tomorrow +\%d) -eq 1 ] && /home/utilisateur/scripts/fin-mois.sh

# Toutes les 5 minutes pendant les heures de bureau
*/5 9-17 * * 1-5 /home/utilisateur/scripts/check-emails.sh

# Deux fois par jour, à 10h et 22h
0 10,22 * * * /home/utilisateur/scripts/backup.sh

# Chaque trimestre (janvier, avril, juillet, octobre) le 1er à minuit
0 0 1 1,4,7,10 * /home/utilisateur/scripts/rapport-trimestriel.sh
```

### Script avec vérification de conditions

```bash
#!/bin/bash
# Script qui ne s'exécute que si certaines conditions sont remplies

# Vérifier si nous sommes en semaine
if [ $(date +%u) -le 5 ]; then
    # Code pour les jours de semaine
    echo "C'est un jour de semaine, exécution du script..."
fi

# Vérifier l'heure
heure=$(date +%H)  
if [ $heure -ge 9 ] && [ $heure -le 17 ]; then  
    echo "Nous sommes pendant les heures de bureau"
fi

# Vérifier si un processus est en cours
if ! pgrep -x "firefox" > /dev/null; then
    echo "Firefox n'est pas en cours d'exécution"
    # Faire quelque chose
fi
```

## Bonnes pratiques

### 1. Utilisez des chemins absolus

```bash
# ✅ Bon
0 2 * * * /home/utilisateur/scripts/backup.sh

# ❌ Mauvais
0 2 * * * ~/scripts/backup.sh
```

### 2. Testez vos scripts avant de les planifier

```bash
# Testez d'abord manuellement
/home/utilisateur/scripts/backup.sh

# Puis ajoutez à crontab
crontab -e
```

### 3. Utilisez des redirections pour capturer les sorties

```bash
# Avec logs
0 2 * * * /home/utilisateur/scripts/backup.sh >> /home/utilisateur/logs/backup.log 2>&1
```

### 4. Ajoutez des commentaires

```bash
# Sauvegarde quotidienne des documents importants
# Créé le 2024-01-15 par Jean
0 2 * * * /home/utilisateur/scripts/backup.sh
```

### 5. Gérez les erreurs dans vos scripts

```bash
#!/bin/bash
set -e  # Arrêter en cas d'erreur

# Votre code
```

### 6. Évitez les chevauchements

Si un script met 2 heures à s'exécuter, ne le planifiez pas toutes les heures !

### 7. Utilisez des verrous pour éviter les exécutions multiples

```bash
#!/bin/bash
LOCKFILE="/tmp/mon_script.lock"

# Vérifier si le script est déjà en cours
if [ -f "$LOCKFILE" ]; then
    echo "Le script est déjà en cours d'exécution"
    exit 1
fi

# Créer le verrou
touch "$LOCKFILE"

# Votre code ici
sleep 10

# Supprimer le verrou
rm -f "$LOCKFILE"
```

### 8. Soyez prudent avec les commandes destructrices

```bash
# ❌ Dangereux
0 2 * * * rm -rf /tmp/*

# ✅ Plus sûr
0 2 * * * find /tmp -type f -mtime +7 -delete
```

### 9. Documentez vos tâches cron

Créez un fichier README dans votre dossier de scripts :

```bash
nano ~/scripts/README.md
```

Listez toutes vos tâches cron avec leurs explications.

### 10. Surveillez les emails de cron

Par défaut, cron envoie les sorties par email. Configurez votre `MAILTO` :

```bash
crontab -e
```

Ajoutez au début :
```bash
MAILTO=votre.email@example.com
```

## Dépannage des tâches cron

### Ma tâche ne s'exécute pas

**1. Vérifiez que cron est actif**

```bash
sudo systemctl status cron
```

Si nécessaire, démarrez-le :

```bash
sudo systemctl start cron  
sudo systemctl enable cron  
```

**2. Vérifiez la syntaxe**

Utilisez un outil en ligne comme [crontab.guru](https://crontab.guru/) pour vérifier votre syntaxe.

**3. Vérifiez les permissions**

```bash
ls -l /home/utilisateur/scripts/mon_script.sh
```

Le script doit être exécutable (`-rwxr-xr-x`).

**4. Vérifiez les chemins**

Utilisez toujours des chemins absolus, jamais de `~` ou de chemins relatifs.

**5. Consultez les logs**

```bash
sudo grep CRON /var/log/syslog | tail -20
```

**6. Testez manuellement**

Exécutez la commande exacte telle que cron le ferait :

```bash
/home/utilisateur/scripts/mon_script.sh
```

### Mon script fonctionne manuellement mais pas via cron

**Problème de PATH** : Cron a un PATH minimal. Utilisez des chemins complets :

```bash
# ❌ Ne fonctionnera peut-être pas
0 2 * * * python script.py

# ✅ Fonctionnera
0 2 * * * /usr/bin/python3 /home/utilisateur/scripts/script.py
```

**Problème d'environnement** : Définissez les variables nécessaires dans votre crontab :

```bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin  
HOME=/home/utilisateur  
SHELL=/bin/bash  

0 2 * * * /home/utilisateur/scripts/backup.sh
```

## Outils utiles

### Générateurs de syntaxe cron

- **crontab.guru** : [https://crontab.guru/](https://crontab.guru/)
- **crontab-generator.org** : [https://crontab-generator.org/](https://crontab-generator.org/)

### Éditeurs visuels

```bash
# Installation de crontab-ui (interface web pour gérer cron)
npm install -g crontab-ui  
crontab-ui  
```

Accédez ensuite à `http://localhost:8000`

### Vérificateur de syntaxe

Il n'existe pas de vérificateur intégré, mais vous pouvez utiliser ce script :

```bash
#!/bin/bash
# Vérifier la syntaxe d'une ligne crontab

ligne="$1"

if [ -z "$ligne" ]; then
    echo "Usage: $0 'ligne_crontab'"
    exit 1
fi

# Test basique
echo "$ligne" | crontab -  
if [ $? -eq 0 ]; then  
    echo "✅ Syntaxe valide"
    crontab -r  # Supprimer la ligne de test
else
    echo "❌ Syntaxe invalide"
fi
```

## Alternatives modernes à cron

Bien que cron soit très robuste et largement utilisé, il existe des alternatives :

### systemd timers

Linux Mint utilise systemd, qui propose un système de planification moderne (nous le verrons dans le chapitre suivant : "Systemd timers").

**Avantages** :
- Meilleure intégration avec systemd
- Logs plus détaillés
- Gestion plus fine des dépendances

### at

Pour des tâches uniques (non répétitives) :

```bash
# Exécuter une commande dans 2 heures
echo "/home/utilisateur/scripts/backup.sh" | at now + 2 hours

# Voir les tâches en attente
atq

# Supprimer une tâche
atrm 1
```

## Conclusion

Cron est un outil puissant pour automatiser les tâches répétitives sous Linux. Avec un peu de pratique, vous pourrez :

- Automatiser vos sauvegardes
- Maintenir votre système propre et à jour
- Planifier des tâches complexes
- Gagner un temps précieux

N'oubliez pas :
- ✅ Testez toujours vos scripts avant de les planifier
- ✅ Utilisez des chemins absolus
- ✅ Ajoutez des logs pour faciliter le débogage
- ✅ Documentez vos tâches cron
- ✅ Soyez prudent avec les commandes destructrices

Avec cron, votre ordinateur devient un assistant infatigable qui travaille pour vous, même quand vous dormez ! 🌙🤖

⏭️ [Systemd timers (alternative moderne à cron)](/20-ligne-de-commande-avancee/03-systemd-timers.md)
