🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 11.8 Fail2Ban pour protection SSH

## Introduction

Imaginez que vous avez un serveur SSH accessible depuis Internet. Chaque jour, des centaines, voire des milliers de robots tentent de deviner votre mot de passe. Ces **attaques par force brute** sont automatisées, incessantes et peuvent finir par réussir si vous avez un mot de passe faible.

**Fail2Ban** est votre garde du corps automatique qui :
- Surveille les tentatives de connexion échouées
- Détecte les attaques en cours
- Bloque automatiquement les adresses IP suspectes
- Protège SSH et de nombreux autres services

### Pourquoi Fail2Ban est essentiel

**Statistiques réelles** : Un serveur SSH exposé sur Internet reçoit en moyenne :
- 50 à 500 tentatives de connexion par jour
- Certains serveurs voient des milliers de tentatives
- Les attaques proviennent du monde entier

**Sans protection** :
- Un mot de passe faible peut être découvert en quelques heures
- Même un mot de passe moyen peut être compromis avec du temps
- Les attaquants testent des milliers de combinaisons automatiquement

**Avec Fail2Ban** :
- ✅ Après 5 échecs : l'IP est bloquée pour 10 minutes (configurable)
- ✅ Réduction drastique de la surface d'attaque
- ✅ Protection automatique 24/7
- ✅ Logs des tentatives d'intrusion

---

## Qu'est-ce que Fail2Ban ?

### Concept de base

**Fail2Ban** est un logiciel qui :
1. **Lit les logs** du système (SSH, Apache, etc.)
2. **Analyse** les entrées pour détecter des comportements suspects
3. **Compte** les échecs de connexion par adresse IP
4. **Bannit** temporairement les IP qui dépassent le seuil
5. **Débloque** automatiquement après expiration du ban

**Analogie** : C'est comme un videur de boîte de nuit qui note tous ceux qui essaient d'entrer avec un faux pass. Au bout de 3 tentatives, vous êtes sur liste noire pour la soirée.

### Comment fonctionne Fail2Ban

```
┌─────────────────────────────────────────────────────────┐
│  1. Attaquant tente de se connecter en SSH              │
│     └─> Échec (mauvais mot de passe)                    │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│  2. SSH écrit l'échec dans /var/log/auth.log            │
│     "Failed password for root from 203.0.113.50"        │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│  3. Fail2Ban lit le log en continu                      │
│     └─> Détecte le pattern "Failed password"            │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│  4. Fail2Ban compte : 203.0.113.50 = 5 échecs           │
│     └─> Seuil maxretry=5 atteint !                      │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│  5. Fail2Ban bannit l'IP via iptables/UFW               │
│     └─> iptables -A INPUT -s 203.0.113.50 -j DROP       │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│  6. Après 10 minutes (bantime), débannit automatiquement│
└─────────────────────────────────────────────────────────┘
```

### Composants de Fail2Ban

#### 1. Jails (prisons)

Une **jail** est une configuration pour un service spécifique :
- `sshd` : Protection SSH
- `apache-auth` : Protection authentification Apache
- `postfix` : Protection serveur mail

Chaque jail a :
- Un **filtre** : patterns à détecter dans les logs
- Un **fichier de log** : où chercher
- Des **paramètres** : maxretry, bantime, findtime

#### 2. Filtres

Les **filtres** sont des expressions régulières (regex) qui identifient les échecs :

Exemple pour SSH :
```
^%(__prefix_line)s(?:error: PAM: )?[aA]uthentication (?:failure|error)
```

Cela détecte les lignes comme :
```
Nov 29 10:45:32 server sshd[12345]: Failed password for invalid user admin from 203.0.113.50
```

#### 3. Actions

Les **actions** définissent que faire quand une IP est bannie :
- `iptables` : Bloquer via iptables
- `ufw` : Bloquer via UFW
- `sendmail` : Envoyer un email d'alerte
- Combinaisons multiples possibles

---

## Installation de Fail2Ban

### Sur Linux Mint / Ubuntu / Debian

```bash
sudo apt update  
sudo apt install fail2ban  
```

### Vérification de l'installation

```bash
sudo systemctl status fail2ban
```

Résultat attendu :
```
● fail2ban.service - Fail2Ban Service
     Loaded: loaded (/lib/systemd/system/fail2ban.service; enabled)
     Active: active (running) since Thu 2024-11-29 10:00:00 CET
```

### Activer au démarrage

```bash
sudo systemctl enable fail2ban
```

---

## Configuration de base

### Structure des fichiers de configuration

Fail2Ban utilise plusieurs fichiers dans `/etc/fail2ban/` :

```
/etc/fail2ban/
├── fail2ban.conf       # Configuration générale (ne pas modifier)
├── fail2ban.local      # Vos modifications de fail2ban.conf
├── jail.conf           # Configuration des jails (ne pas modifier)
├── jail.local          # Vos modifications de jail.conf (à créer)
├── jail.d/             # Fichiers de configuration supplémentaires
├── filter.d/           # Filtres (patterns de détection)
├── action.d/           # Actions (que faire lors d'un ban)
└── fail2ban.d/         # Configurations supplémentaires
```

### Règle d'or : Ne modifiez jamais les fichiers .conf

- ❌ **Ne pas éditer** : `jail.conf`, `fail2ban.conf`
- ✅ **Créer ou éditer** : `jail.local`, `fail2ban.local`

**Pourquoi ?** Les fichiers `.conf` sont écrasés lors des mises à jour. Vos modifications dans `.local` ont priorité et sont préservées.

### Créer jail.local

```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

Ou créez un fichier vierge :
```bash
sudo nano /etc/fail2ban/jail.local
```

---

## Configuration SSH de base

### Configuration minimale recommandée

Éditez `/etc/fail2ban/jail.local` :

```bash
sudo nano /etc/fail2ban/jail.local
```

Ajoutez ou modifiez :

```ini
[DEFAULT]
# Ban une IP pour 10 minutes après 5 échecs
bantime  = 10m  
findtime = 10m  
maxretry = 5  

# Action par défaut (avec UFW si installé, sinon iptables)
banaction = ufw
# Ou si vous n'utilisez pas UFW :
# banaction = iptables-multiport

# Ignorer ces IP (votre IP fixe, réseau local)
ignoreip = 127.0.0.1/8 ::1 192.168.1.0/24

[sshd]
enabled = true  
port    = ssh  
logpath = /var/log/auth.log  
maxretry = 5  
```

### Paramètres expliqués

#### Section [DEFAULT]

| Paramètre | Description | Valeur recommandée |
|-----------|-------------|-------------------|
| `bantime` | Durée du bannissement | `10m` (10 min) ou `1h` (1 heure) |
| `findtime` | Fenêtre de temps pour compter les échecs | `10m` |
| `maxretry` | Nombre d'échecs avant ban | `5` pour SSH, `3` pour services critiques |
| `ignoreip` | IP à ne jamais bannir | Votre IP, réseau local |
| `banaction` | Comment bannir (iptables, ufw) | `ufw` ou `iptables-multiport` |

**Calcul** : Si `maxretry = 5` et `findtime = 10m`, cela signifie :
- 5 échecs **dans une période de 10 minutes** = ban
- Si 4 échecs en 10 minutes, puis 1 échec 11 minutes après le premier : pas de ban (hors de la fenêtre)

#### Section [sshd]

| Paramètre | Description | Valeur |
|-----------|-------------|--------|
| `enabled` | Activer cette jail | `true` |
| `port` | Port à protéger | `ssh` (port 22) ou `2222` si changé |
| `logpath` | Fichier de log à surveiller | `/var/log/auth.log` |
| `maxretry` | Surcharge le défaut pour SSH | Optionnel |

### Cas particulier : SSH sur un port personnalisé

Si vous avez changé le port SSH (recommandé pour la sécurité) :

```ini
[sshd]
enabled = true  
port    = 2222  
logpath = /var/log/auth.log  
```

### Redémarrer Fail2Ban après modification

```bash
sudo systemctl restart fail2ban
```

### Vérifier que la configuration est valide

```bash
sudo fail2ban-client status
```

Résultat :
```
Status
|- Number of jail:      1
`- Jail list:   sshd
```

---

## Gestion des bans

### Voir l'état de Fail2Ban

#### État général

```bash
sudo fail2ban-client status
```

#### État d'une jail spécifique

```bash
sudo fail2ban-client status sshd
```

Résultat exemple :
```
Status for the jail: sshd
|- Filter
|  |- Currently failed: 3
|  |- Total failed:     156
|  `- File list:        /var/log/auth.log
`- Actions
   |- Currently banned: 2
   |- Total banned:     12
   `- Banned IP list:   203.0.113.50 198.51.100.75
```

Informations importantes :
- **Currently failed** : IP actuellement en surveillance
- **Total failed** : Nombre total d'échecs détectés
- **Currently banned** : Nombre d'IP actuellement bannies
- **Banned IP list** : Liste des IP bannies

### Débannir manuellement une IP

Si vous ou un collègue êtes accidentellement bannis :

```bash
sudo fail2ban-client set sshd unbanip 203.0.113.50
```

### Bannir manuellement une IP

```bash
sudo fail2ban-client set sshd banip 198.51.100.75
```

### Voir toutes les IP bannies

```bash
sudo fail2ban-client status sshd | grep "Banned IP"
```

Ou consultez directement iptables/UFW :

```bash
sudo iptables -L -n | grep DROP
```

Ou pour UFW :
```bash
sudo ufw status numbered
```

---

## Configuration avancée

### Augmenter la durée du ban

Pour des bans plus longs (1 heure, 1 jour, permanent) :

```ini
[DEFAULT]
# Ban pour 1 heure
bantime  = 1h

# ou 1 jour
bantime  = 1d

# ou 1 semaine
bantime  = 1w
```

### Ban permanent après récidive

Bannir définitivement une IP après 3 bans :

```ini
[sshd]
enabled = true  
port    = ssh  
logpath = /var/log/auth.log  
maxretry = 5  
# Première offense : 10 min
bantime = 10m
# Seconde offense : 1 heure
# Troisième offense : permanent (-1)
bantime.increment = true  
bantime.multipliers = 1 2 4 8 16 32 64  
bantime.maxtime = -1  
```

### Ignorer certaines IP de confiance

Ajoutez vos IP de confiance pour éviter de vous bannir :

```ini
[DEFAULT]
ignoreip = 127.0.0.1/8 ::1 192.168.1.0/24 203.0.113.100
```

- `127.0.0.1/8` : Localhost
- `::1` : Localhost IPv6
- `192.168.1.0/24` : Votre réseau local
- `203.0.113.100` : Votre IP publique fixe (si vous en avez une)

> **Important** : Ajoutez votre IP avant d'activer Fail2Ban pour ne pas vous verrouiller dehors !

### Recevoir des emails lors des bans

Configurez l'envoi d'emails pour être alerté :

#### Installer un client mail

```bash
sudo apt install mailutils
```

#### Configurer Fail2Ban

```ini
[DEFAULT]
# Votre email
destemail = votre@email.com  
sendername = Fail2Ban  
mta = sendmail  

# Action : ban + email
action = %(action_mwl)s
```

Les actions disponibles :
- `%(action_)s` : Ban uniquement
- `%(action_mw)s` : Ban + email avec whois
- `%(action_mwl)s` : Ban + email avec whois + logs

### Whitelist permanente

Pour des IP qui ne doivent **jamais** être bannies, même si elles échouent :

```ini
[DEFAULT]
ignoreself = true  
ignoreip = 127.0.0.1/8 ::1  
           192.168.1.0/24
           10.0.0.0/8
           172.16.0.0/12
```

---

## Protéger d'autres services

Fail2Ban peut protéger bien plus que SSH.

### Apache / Nginx

#### Protéger l'authentification web

```ini
[apache-auth]
enabled = true  
port    = http,https  
logpath = /var/log/apache2/error.log  

[nginx-http-auth]
enabled = true  
port    = http,https  
logpath = /var/log/nginx/error.log  
```

#### Protéger contre les scans de vulnérabilités

```ini
[apache-badbots]
enabled = true  
port    = http,https  
logpath = /var/log/apache2/access.log  
maxretry = 1  
```

### Serveur mail (Postfix, Dovecot)

```ini
[postfix]
enabled = true  
port    = smtp,465,submission  
logpath = /var/log/mail.log  

[dovecot]
enabled = true  
port    = pop3,pop3s,imap,imaps  
logpath = /var/log/mail.log  
```

### Base de données (MySQL)

```ini
[mysqld-auth]
enabled = true  
port    = 3306  
logpath = /var/log/mysql/error.log  
maxretry = 3  
```

### FTP (vsftpd, ProFTPd)

```ini
[vsftpd]
enabled = true  
port    = ftp,ftp-data,ftps,ftps-data  
logpath = /var/log/vsftpd.log  
```

### WordPress (attaques xmlrpc, wp-login)

Créez `/etc/fail2ban/filter.d/wordpress.conf` :

```ini
[Definition]
failregex = ^<HOST> .* "POST .*wp-login\.php
            ^<HOST> .* "POST .*xmlrpc\.php
ignoreregex =
```

Puis dans `jail.local` :
```ini
[wordpress]
enabled = true  
port    = http,https  
filter  = wordpress  
logpath = /var/log/apache2/access.log  
maxretry = 3  
bantime = 1h  
```

---

## Logs et surveillance

### Consulter les logs Fail2Ban

#### Logs principaux

```bash
sudo tail -f /var/log/fail2ban.log
```

Exemple de lignes :
```
2024-11-29 10:45:32,123 fail2ban.actions [12345]: NOTICE  [sshd] Ban 203.0.113.50
2024-11-29 10:55:32,456 fail2ban.actions [12345]: NOTICE  [sshd] Unban 203.0.113.50
```

#### Filtrer les bans uniquement

```bash
sudo grep "Ban" /var/log/fail2ban.log
```

#### Filtrer les débans

```bash
sudo grep "Unban" /var/log/fail2ban.log
```

#### Voir les bans du jour

```bash
sudo grep "Ban" /var/log/fail2ban.log | grep "$(date +%Y-%m-%d)"
```

### Statistiques des attaques

#### Compter les IP bannies aujourd'hui

```bash
sudo grep "Ban" /var/log/fail2ban.log | grep "$(date +%Y-%m-%d)" | wc -l
```

#### Top 10 des IP les plus bannies

```bash
sudo grep "Ban" /var/log/fail2ban.log | grep -oP 'Ban \K[0-9.]+' | sort | uniq -c | sort -rn | head -10
```

#### Pays d'origine des attaques (avec geoiplookup)

```bash
sudo apt install geoip-bin  
sudo grep "Ban" /var/log/fail2ban.log | grep -oP 'Ban \K[0-9.]+' | head -20 | while read IP; do  
    echo -n "$IP : "
    geoiplookup $IP | cut -d':' -f2
done
```

---

## Intégration avec UFW

### Vérifier que Fail2Ban utilise UFW

Dans `/etc/fail2ban/jail.local` :

```ini
[DEFAULT]
banaction = ufw
```

### Voir les règles UFW créées par Fail2Ban

```bash
sudo ufw status numbered
```

Les règles Fail2Ban apparaissent comme :
```
[ 5] Anywhere                   DENY IN    203.0.113.50
```

### Action personnalisée UFW

Pour plus de contrôle, créez `/etc/fail2ban/action.d/ufw.local` :

```ini
[Definition]
actionstart =  
actionstop =  
actioncheck =  
actionban = ufw insert 1 deny from <ip> to any  
actionunban = ufw delete deny from <ip> to any  
```

---

## Optimisation des performances

### Fail2Ban consomme-t-il des ressources ?

**Non**, Fail2Ban est très léger :
- Utilisation CPU : ~0.1% en moyenne
- RAM : ~20-30 MB
- Impact négligeable sur les performances

### Réduire la charge si nécessaire

#### Augmenter l'intervalle de polling

Dans `/etc/fail2ban/fail2ban.local` :

```ini
[Definition]
logtarget = /var/log/fail2ban.log  
loglevel = INFO  
# Vérifier les logs toutes les 60 secondes au lieu de 10
# (par défaut implicite)
```

#### Utiliser systemd backend (plus efficace)

```ini
[sshd]
enabled = true  
backend = systemd  
```

Le backend systemd lit directement le journal systemd au lieu de parser les fichiers texte, c'est plus rapide.

---

## Création de filtres personnalisés

### Anatomie d'un filtre

Les filtres sont dans `/etc/fail2ban/filter.d/`.

Exemple : `/etc/fail2ban/filter.d/sshd.conf`

```ini
[Definition]
# Pattern de détection (expression régulière)
failregex = ^%(__prefix_line)s(?:error: PAM: )?[aA]uthentication (?:failure|error|failed)
            ^%(__prefix_line)sFailed (?:password|publickey) for .* from <HOST>

# Patterns à ignorer (faux positifs)
ignoreregex =
```

### Créer un filtre personnalisé

Exemple : Détecter les tentatives d'accès à phpMyAdmin :

#### 1. Créer le filtre

```bash
sudo nano /etc/fail2ban/filter.d/phpmyadmin.conf
```

Contenu :
```ini
[Definition]
failregex = ^<HOST> -.*"(GET|POST).*(phpmyadmin|pma|myadmin)  
ignoreregex =  
```

#### 2. Créer la jail

Dans `/etc/fail2ban/jail.local` :

```ini
[phpmyadmin]
enabled = true  
port    = http,https  
filter  = phpmyadmin  
logpath = /var/log/apache2/access.log  
maxretry = 3  
bantime = 1h  
```

#### 3. Tester le filtre

```bash
sudo fail2ban-regex /var/log/apache2/access.log /etc/fail2ban/filter.d/phpmyadmin.conf
```

Cela affiche si le filtre détecte bien les patterns.

#### 4. Redémarrer Fail2Ban

```bash
sudo systemctl restart fail2ban
```

---

## Dépannage

### Fail2Ban ne démarre pas

#### Vérifier les logs d'erreur

```bash
sudo journalctl -u fail2ban -xe
```

Ou :
```bash
sudo tail -50 /var/log/fail2ban.log
```

#### Erreurs courantes

**Erreur : "Unable to find a corresponding IP address"**

Problème : Le filtre ne trouve pas les IP dans les logs.

Solution : Vérifiez que le logpath est correct et que les logs contiennent bien des IP.

**Erreur : "Invalid configuration"**

Problème : Syntaxe incorrecte dans jail.local.

Solution : Vérifiez les accolades, virgules, indentation :
```bash
sudo fail2ban-client -d
```

### Fail2Ban ne bannit pas

#### Vérifier que la jail est active

```bash
sudo fail2ban-client status
```

Si `sshd` n'apparaît pas :
```bash
sudo systemctl restart fail2ban  
sudo fail2ban-client status  
```

#### Vérifier que les logs sont bien lus

```bash
sudo fail2ban-client get sshd logpath
```

#### Tester le filtre manuellement

```bash
sudo fail2ban-regex /var/log/auth.log /etc/fail2ban/filter.d/sshd.conf
```

Cela montre combien de lignes correspondent au filtre.

### Débannir accidentellement banni

Si vous vous êtes banni :

#### Option 1 : Accès physique ou console

```bash
sudo fail2ban-client set sshd unbanip VOTRE_IP
```

#### Option 2 : Via un autre serveur ou IP

Connectez-vous depuis une autre IP et débannissez :
```bash
ssh -p 22 autre_user@serveur  
sudo fail2ban-client set sshd unbanip IP_BANNIE  
```

#### Option 3 : Arrêter Fail2Ban temporairement

```bash
sudo systemctl stop fail2ban
```

Les règles de ban persistent dans iptables/UFW. Supprimez-les :
```bash
sudo ufw delete deny from IP_BANNIE
```

### Fail2Ban ne persiste pas après redémarrage

#### Vérifier que le service est activé

```bash
sudo systemctl is-enabled fail2ban
```

Si "disabled" :
```bash
sudo systemctl enable fail2ban
```

---

## Bonnes pratiques

### Sécurité

1. ✅ **Configurez AVANT d'exposer SSH** : Activez Fail2Ban avant d'ouvrir le port 22 sur Internet
2. ✅ **Whitelist vos IP** : Ajoutez vos IP de confiance dans `ignoreip`
3. ✅ **Combinez avec d'autres mesures** :
   - Clés SSH au lieu de mots de passe
   - Port SSH non-standard (ex: 2222)
   - UFW activé
   - Mots de passe forts
4. ✅ **Surveillez les logs** : Consultez régulièrement les tentatives d'attaque
5. ✅ **Bans progressifs** : Augmentez la durée du ban en cas de récidive

### Configuration

1. ✅ **Ne modifiez jamais jail.conf** : Toujours créer jail.local
2. ✅ **Testez vos filtres** : Utilisez `fail2ban-regex` avant de déployer
3. ✅ **Bantime raisonnable** : 10 min à 1h pour SSH, plus long pour services critiques
4. ✅ **Maxretry adapté** : 5 pour SSH, 3 pour services sensibles, 1 pour scans
5. ✅ **Sauvegardez votre config** :
   ```bash
   sudo cp -r /etc/fail2ban /root/fail2ban_backup_$(date +%Y%m%d)
   ```

### Surveillance

1. ✅ **Activez les logs** : Au minimum niveau INFO
2. ✅ **Automatisez les rapports** : Script cron pour résumé quotidien
3. ✅ **Analysez les patterns** : Identifiez les pays/réseaux hostiles
4. ✅ **Géoblocage** : Bloquez des pays entiers si nécessaire (avec ipset)
5. ✅ **Alertes email** : Pour les services critiques

### Maintenance

1. ✅ **Mettez à jour régulièrement** : `sudo apt update && sudo apt upgrade fail2ban`
2. ✅ **Nettoyez les vieux logs** : Configurez la rotation des logs
3. ✅ **Révisez la whitelist** : Retirez les IP qui ne sont plus de confiance
4. ✅ **Testez après mise à jour** : Vérifiez que tout fonctionne
5. ✅ **Documentez vos règles** : Notez pourquoi vous avez créé chaque jail personnalisée

---

## Scripts utiles

### Script de rapport quotidien

```bash
#!/bin/bash
# /usr/local/bin/fail2ban_rapport.sh

DATE=$(date +%Y-%m-%d)  
LOGFILE="/var/log/fail2ban.log"  

echo "=== Rapport Fail2Ban du $DATE ==="  
echo ""  
echo "Nombre de bans aujourd'hui :"  
grep "Ban" "$LOGFILE" | grep "$DATE" | wc -l  
echo ""  
echo "Top 10 IP bannies :"  
grep "Ban" "$LOGFILE" | grep "$DATE" | grep -oP 'Ban \K[0-9.]+' | sort | uniq -c | sort -rn | head -10  
echo ""  
echo "Services ciblés :"  
fail2ban-client status | grep "Jail list"  
```

Rendez-le exécutable :
```bash
sudo chmod +x /usr/local/bin/fail2ban_rapport.sh
```

Ajoutez à cron pour exécution quotidienne à 23h :
```bash
sudo crontab -e
```

Ajoutez :
```
0 23 * * * /usr/local/bin/fail2ban_rapport.sh | mail -s "Rapport Fail2Ban" admin@example.com
```

### Script de débannissement en masse

```bash
#!/bin/bash
# Débannir toutes les IP d'une jail

JAIL=$1

if [ -z "$JAIL" ]; then
    echo "Usage: $0 <jail_name>"
    echo "Exemple: $0 sshd"
    exit 1
fi

echo "Débannissement de toutes les IP de la jail $JAIL"

# Lister les IP bannies
BANNED_IPS=$(fail2ban-client get $JAIL banip)

# Débannir chaque IP
for IP in $BANNED_IPS; do
    echo "Débannissement de $IP"
    fail2ban-client set $JAIL unbanip $IP
done

echo "Terminé !"
```

---

## Alternatives et compléments

### DenyHosts

**Alternative** à Fail2Ban, spécifique à SSH :
- Plus simple mais moins flexible
- Partage des listes d'IP hostiles entre utilisateurs

```bash
sudo apt install denyhosts
```

**Recommandation** : Préférez Fail2Ban (plus complet).

### SSHGuard

**Alternative** légère :
- Protège SSH, FTP, etc.
- Plus simple que Fail2Ban
- Moins de fonctionnalités

```bash
sudo apt install sshguard
```

### Port knocking

**Complément** : Cache le port SSH :
- Le port SSH reste fermé
- Nécessite une "séquence secrète" de connexions pour l'ouvrir
- Très sécurisé mais complexe

### Cloudflare (pour services web)

Pour les services web exposés, Cloudflare offre :
- Protection DDoS automatique
- WAF (Web Application Firewall)
- Rate limiting
- Gratuit pour l'essentiel

---

## Commandes de référence rapide

### Gestion du service

| Commande | Description |
|----------|-------------|
| `sudo systemctl start fail2ban` | Démarrer Fail2Ban |
| `sudo systemctl stop fail2ban` | Arrêter Fail2Ban |
| `sudo systemctl restart fail2ban` | Redémarrer Fail2Ban |
| `sudo systemctl status fail2ban` | Voir l'état |
| `sudo systemctl enable fail2ban` | Activer au démarrage |

### État et statistiques

| Commande | Description |
|----------|-------------|
| `sudo fail2ban-client status` | Liste des jails actives |
| `sudo fail2ban-client status sshd` | État de la jail sshd |
| `sudo fail2ban-client get sshd banip` | Liste IP bannies |

### Bannissement manuel

| Commande | Description |
|----------|-------------|
| `sudo fail2ban-client set sshd banip 203.0.113.50` | Bannir une IP |
| `sudo fail2ban-client set sshd unbanip 203.0.113.50` | Débannir une IP |

### Tests et débogage

| Commande | Description |
|----------|-------------|
| `sudo fail2ban-regex /var/log/auth.log /etc/fail2ban/filter.d/sshd.conf` | Tester un filtre |
| `sudo fail2ban-client -d` | Mode debug |
| `sudo tail -f /var/log/fail2ban.log` | Voir les logs en temps réel |

---

## Résumé

### Points clés

1. **Fail2Ban est essentiel** pour tout serveur SSH exposé sur Internet
2. **Configuration simple** : jail.local avec quelques lignes suffit
3. **Bannissement automatique** : Après 5 échecs, 10 minutes de ban
4. **Whitelist vos IP** : Pour ne jamais vous bannir
5. **Surveillance active** : Consultez les logs régulièrement
6. **Complément, pas remplacement** : Utilisez aussi clés SSH, UFW, mots de passe forts

### Configuration minimale recommandée

Pour un serveur SSH :

```bash
# Installer
sudo apt install fail2ban

# Créer la configuration
sudo tee /etc/fail2ban/jail.local > /dev/null <<EOF
[DEFAULT]
bantime  = 1h  
findtime = 10m  
maxretry = 5  
ignoreip = 127.0.0.1/8 VOTRE_IP  

[sshd]
enabled = true  
port    = ssh  
logpath = /var/log/auth.log  
EOF  

# Redémarrer et activer
sudo systemctl restart fail2ban  
sudo systemctl enable fail2ban  

# Vérifier
sudo fail2ban-client status sshd
```

### L'essentiel à retenir

> **Fail2Ban transforme un serveur vulnérable en forteresse**

Sans Fail2Ban : Des milliers de tentatives d'intrusion par jour.  
Avec Fail2Ban : Les attaquants sont bloqués après quelques tentatives.  

**Installation : 2 minutes. Protection : permanente.**

---


⏭️ [Matériel et pilotes](/12-materiel-et-pilotes/README.md)
