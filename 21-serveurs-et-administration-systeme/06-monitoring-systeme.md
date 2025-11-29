🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 21.6 Monitoring système (Netdata, Glances)

## Introduction

### Qu'est-ce que le monitoring système ?

Le monitoring (surveillance) système consiste à observer en temps réel les performances et l'état de votre ordinateur : utilisation du processeur, mémoire RAM, disques durs, réseau, température, etc.

**En termes simples :** C'est comme avoir un tableau de bord de voiture pour votre ordinateur, qui vous montre tout ce qui se passe sous le capot !

### Pourquoi surveiller son système ?

- **Détecter les problèmes** : Identifier ce qui ralentit votre ordinateur
- **Optimiser les performances** : Savoir quelles applications consomment trop de ressources
- **Prévenir les pannes** : Repérer les disques durs défaillants, la surchauffe, etc.
- **Surveiller un serveur** : S'assurer qu'un serveur fonctionne correctement 24/7
- **Comprendre son système** : Apprendre comment Linux utilise les ressources
- **Historique** : Voir l'évolution de l'utilisation sur plusieurs jours/mois

### Cas d'usage concrets

- Mon ordinateur est lent, quel processus consomme tout le CPU ?
- Ai-je assez de RAM ou dois-je en acheter ?
- Mon disque dur est-il en train de mourir ?
- Quelle application utilise tout mon réseau ?
- Mon serveur web répond-il correctement ?
- La température de mon processeur est-elle normale ?

---

## Outils de monitoring intégrés à Linux

Avant de présenter Netdata et Glances, voici les outils de base déjà disponibles :

### top - Le classique

```bash
top
```

Affiche les processus en temps réel avec utilisation CPU/RAM.

**Raccourcis utiles :**
- `q` : Quitter
- `k` : Tuer un processus
- `M` : Trier par utilisation mémoire
- `P` : Trier par utilisation CPU

### htop - Version améliorée de top

Plus coloré et interactif :

```bash
sudo apt install htop
htop
```

**Avantages :**
- Interface graphique colorée
- Utilisation de la souris
- Arborescence des processus
- Barres visuelles pour CPU et RAM

### Moniteur système (graphique)

Linux Mint inclut un moniteur système graphique :

Menu → Outils système → Moniteur système

Affiche CPU, mémoire, réseau sous forme de graphiques.

### Pourquoi utiliser Netdata ou Glances ?

Ces outils basiques sont utiles mais limités. Netdata et Glances offrent :

- **Plus de métriques** : Température, disques, réseau détaillé, etc.
- **Historique** : Voir l'évolution sur plusieurs heures/jours
- **Interface web** : Accès depuis n'importe quel navigateur
- **Alertes** : Notifications quand quelque chose ne va pas
- **Graphiques** : Visualisation claire et intuitive

---

## Netdata vs Glances

### Netdata

**Type :** Solution de monitoring complète avec interface web

**Avantages :**
- Interface web magnifique et très complète
- Temps réel avec mise à jour chaque seconde
- Détection automatique de services (Apache, MySQL, etc.)
- Graphiques interactifs et zoomables
- Alarmes configurables
- Très complet (centaines de métriques)
- Accès distant via navigateur web

**Inconvénients :**
- Plus lourd en ressources
- Configuration parfois complexe
- Nécessite un navigateur web

**Idéal pour :** Surveillance de serveurs, analyse détaillée, accès distant

### Glances

**Type :** Outil de monitoring en terminal (avec option web)

**Avantages :**
- Très léger
- Fonctionne directement dans le terminal
- Vue d'ensemble complète en une seule page
- Mode serveur disponible
- Export des données (CSV, JSON)
- Facile à utiliser

**Inconvénients :**
- Interface moins jolie que Netdata
- Moins de métriques détaillées
- Historique limité

**Idéal pour :** Diagnostic rapide, utilisation ponctuelle, serveurs avec peu de ressources

### Tableau comparatif

| Critère | Netdata | Glances |
|---------|---------|---------|
| **Interface** | Web (superbe) | Terminal/Web (simple) |
| **Ressources** | Moyenne | Très faible |
| **Facilité** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Métriques** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Historique** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Alertes** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Accès distant** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |

### Lequel choisir ?

**Choisissez Netdata si :**
- Vous surveillez un serveur en production
- Vous voulez des graphiques détaillés
- Vous avez besoin d'historique long terme
- Vous préférez une interface web
- Vous voulez des alertes sophistiquées

**Choisissez Glances si :**
- Vous voulez un diagnostic rapide
- Vous travaillez souvent en SSH
- Vous avez peu de ressources
- Vous préférez le terminal
- Vous voulez quelque chose de simple

**Bonne nouvelle :** Vous pouvez installer les deux !

---

## Partie 1 : Installation et utilisation de Netdata

### Installation de Netdata

#### Méthode 1 : Script d'installation officiel (recommandée)

La méthode la plus simple et qui installe la dernière version :

```bash
wget -O /tmp/netdata-kickstart.sh https://get.netdata.cloud/kickstart.sh && sh /tmp/netdata-kickstart.sh
```

Le script :
- Détecte votre système
- Installe les dépendances
- Compile et installe Netdata
- Configure le démarrage automatique

**Répondez "yes" quand demandé.**

L'installation prend 2-5 minutes.

#### Méthode 2 : Depuis les dépôts (version plus ancienne)

```bash
sudo apt update
sudo apt install netdata
```

Version potentiellement plus ancienne mais installation plus rapide.

#### Vérifier l'installation

```bash
sudo systemctl status netdata
```

Vous devriez voir "active (running)" en vert.

### Accéder à l'interface Netdata

Ouvrez votre navigateur et allez sur :

```
http://localhost:19999
```

Vous devriez voir le magnifique tableau de bord Netdata !

**Pour accès depuis un autre ordinateur sur le réseau :**

```
http://adresse_ip_du_serveur:19999
```

Exemple : `http://192.168.1.100:19999`

### Découverte de l'interface Netdata

#### Vue d'ensemble (Overview)

La page d'accueil montre :

**En haut :**
- Sélecteur de temps (1 min, 5 min, 1 heure, etc.)
- Menu de navigation

**Sections principales :**

1. **System Overview**
   - CPU global
   - Load Average (charge système)
   - RAM utilisée
   - Swap utilisé
   - Disques

2. **CPUs**
   - Utilisation par cœur
   - Idle, user, system, etc.
   - Fréquence du processeur

3. **Memory**
   - RAM détaillée (apps, cache, buffers)
   - Swap
   - Dirty pages

4. **Disks**
   - Utilisation de chaque disque
   - I/O (lectures/écritures)
   - Backlog

5. **Network**
   - Bande passante par interface
   - Paquets
   - Erreurs

6. **Applications**
   - Consommation par processus/application
   - CPU, RAM, disque par app

#### Navigation

**Cliquez sur un graphique** pour :
- Zoomer/dézoomer (molette de la souris)
- Se déplacer dans le temps
- Voir les valeurs exactes (survol)

**Menu de gauche :**
- Jump to : Aller directement à une section
- Alarms : Voir les alertes actives
- Nodes : Si vous surveillez plusieurs machines

#### Personnaliser l'affichage

**Changer l'intervalle de temps :**

En haut à droite, cliquez sur le sélecteur :
- Last 1 minute
- Last 5 minutes
- Last 1 hour
- Last 6 hours
- Last 12 hours
- etc.

**Mode sombre :**

Icône en haut à droite → Theme → Dark

**Actualisation :**

Par défaut, mise à jour chaque seconde. Modifiable dans Settings.

### Informations détaillées par section

#### CPU

- **Total CPU** : Utilisation globale
- **Per Core** : Chaque cœur séparément
- **User** : Applications utilisateur
- **System** : Noyau Linux
- **Nice** : Processus avec priorité basse
- **IRQ** : Interruptions matérielles
- **Idle** : Inactivité

**Graphique utile :** Si un cœur est toujours à 100%, une application est peut-être mal optimisée.

#### Mémoire RAM

- **Apps** : Mémoire utilisée par les applications
- **Cache** : Fichiers mis en cache pour accélérer
- **Buffers** : Tampons système
- **Free** : Mémoire libre réelle

**Important :** Linux utilise la RAM libre comme cache. C'est normal et bénéfique !

#### Disques

- **Utilization** : Pourcentage d'utilisation du disque
- **Backlog** : File d'attente d'opérations I/O
- **Reads/Writes** : Lecture et écriture en MB/s
- **I/O Operations** : Nombre d'opérations par seconde

**Graphique utile :** Si utilization = 100% constamment, le disque est un goulot d'étranglement.

#### Réseau

- **Bandwidth** : Bande passante (download/upload)
- **Packets** : Nombre de paquets
- **Errors** : Erreurs réseau
- **Drops** : Paquets perdus

**Graphique utile :** Pic soudain = téléchargement en cours ou problème réseau.

#### Applications

Liste de tous les processus avec :
- CPU utilisé
- Mémoire utilisée
- Disque I/O
- Réseau

**Très utile** pour identifier l'application qui consomme trop de ressources.

### Configurer le pare-feu pour Netdata

Si vous voulez accéder à Netdata depuis d'autres machines :

```bash
sudo ufw allow 19999/tcp
```

**Attention :** Netdata n'a pas d'authentification par défaut ! Sécurisez l'accès (voir section sécurité).

### Configurer Netdata

Le fichier de configuration principal :

```bash
sudo nano /etc/netdata/netdata.conf
```

#### Activer/désactiver des plugins

Par défaut, Netdata détecte automatiquement de nombreux services. Pour désactiver un plugin :

```ini
[plugins]
    python.d = no
    charts.d = no
```

#### Changer le port

```ini
[web]
    default port = 19999
```

Changez 19999 en un autre port.

#### Limiter l'accès réseau

Pour autoriser uniquement localhost :

```ini
[web]
    bind to = 127.0.0.1
```

Pour autoriser tout le monde :

```ini
[web]
    bind to = 0.0.0.0
```

#### Redémarrer après modification

```bash
sudo systemctl restart netdata
```

### Alertes et notifications

Netdata peut vous alerter quand quelque chose ne va pas.

#### Voir les alarmes actives

Dans l'interface web, cliquez sur l'icône cloche 🔔 en haut.

Vous verrez toutes les alarmes (critiques, warnings).

#### Configurer les seuils d'alerte

Fichier de configuration des alarmes :

```bash
sudo nano /etc/netdata/health.d/cpu.conf
```

Exemple d'alerte personnalisée :

```yaml
alarm: cpu_usage
on: system.cpu
lookup: average -3s percentage foreach user,system
units: %
every: 10s
warn: $this > 80
crit: $this > 95
info: CPU utilization is too high
```

Cette alerte :
- Surveille le CPU
- Warning si > 80%
- Critique si > 95%
- Vérifie toutes les 10 secondes

#### Notifications par email

Installez sendmail ou configurez SMTP :

```bash
sudo apt install sendmail
```

Configurez dans `/etc/netdata/health_alarm_notify.conf` :

```bash
sudo nano /etc/netdata/health_alarm_notify.conf
```

Ajoutez :

```ini
SEND_EMAIL="YES"
DEFAULT_RECIPIENT_EMAIL="votre@email.com"
```

Redémarrez :

```bash
sudo systemctl restart netdata
```

#### Autres méthodes de notification

Netdata supporte :
- Slack
- Discord
- Telegram
- PagerDuty
- Webhooks personnalisés

Configuration dans le même fichier `health_alarm_notify.conf`.

### Surveiller des services spécifiques

#### MySQL/MariaDB

Netdata détecte automatiquement MySQL s'il tourne.

Pour activer la surveillance complète, créez un utilisateur :

```sql
CREATE USER 'netdata'@'localhost';
GRANT USAGE ON *.* TO 'netdata'@'localhost';
FLUSH PRIVILEGES;
```

Netdata se connectera automatiquement.

#### Apache/Nginx

Active le module status :

**Apache :**

```bash
sudo a2enmod status
sudo systemctl restart apache2
```

**Nginx :**

Ajoutez dans la configuration :

```nginx
location /nginx_status {
    stub_status on;
    allow 127.0.0.1;
    deny all;
}
```

Netdata détectera automatiquement.

#### Docker

Si vous utilisez Docker :

```bash
sudo groupadd docker
sudo usermod -aG docker netdata
sudo systemctl restart netdata
```

Les conteneurs Docker apparaîtront automatiquement.

### Netdata Cloud (optionnel)

Netdata Cloud permet de surveiller plusieurs machines depuis un tableau de bord centralisé.

**Gratuit pour usage personnel.**

#### S'inscrire

Visitez [app.netdata.cloud](https://app.netdata.cloud) et créez un compte.

#### Connecter votre machine

Lors de l'installation, le script propose de se connecter. Sinon :

```bash
sudo netdata-claim.sh -token=VOTRE_TOKEN -rooms=VOTRE_ROOM -url=https://app.netdata.cloud
```

Le token est disponible sur le site Netdata Cloud.

**Avantages :**
- Dashboard centralisé pour plusieurs serveurs
- Alertes consolidées
- Accès depuis n'importe où
- Gratuit

---

## Partie 2 : Installation et utilisation de Glances

### Installation de Glances

#### Depuis les dépôts (recommandé)

```bash
sudo apt update
sudo apt install glances
```

#### Avec pip (dernière version)

```bash
sudo apt install python3-pip
sudo pip3 install glances
```

#### Vérifier l'installation

```bash
glances --version
```

### Lancer Glances

Simplement :

```bash
glances
```

L'interface s'affiche directement dans le terminal !

**Pour quitter :** Appuyez sur `q`

### Interface de Glances

Glances affiche tout sur un seul écran divisé en sections :

#### En haut

**Hostname, système, uptime**

```
nom-machine    Linux 5.15.0-84-generic    Uptime: 3 days, 5:42:37
```

#### Section CPU

```
CPU      13.5%  user:  8.2%  system:  3.1%  idle: 88.5%
```

Affiche l'utilisation globale et par catégorie.

**Avec plusieurs cœurs :**

```
CPU  [||||||||||||          ]  13.5%
0    [|||||                 ]   9.2%
1    [|||||||               ]  11.8%
2    [||||||||||            ]  15.3%
3    [|||||||               ]  12.1%
```

#### Section Load Average

```
LOAD    1-min: 0.52  5-min: 0.68  15-min: 0.73
```

Charge moyenne du système (devrait être < nombre de cœurs CPU).

#### Section Mémoire

```
MEM     65.2%  active:    5.2G  inactive:    2.8G  free:    1.1G
SWAP     5.3%  used:    512M  free:    9.5G
```

Utilisation RAM et swap.

#### Section Réseau

```
NETWORK     Rx/s   Tx/s
eth0        52KB   18KB
```

Bande passante reçue/envoyée par seconde.

#### Section Disques

```
DISK I/O    R/s    W/s
sda         5.2M   1.8M
```

Lectures et écritures par seconde.

#### Section Système de fichiers

```
FILE SYS    Used  Total  %
/           45G   100G   45%
/home       180G  500G   36%
```

Espace disque utilisé.

#### Section Capteurs

```
SENSORS
CPU         45°C
GPU         52°C
```

Températures des composants (si disponibles).

#### Section Processus

```
PID    USER     CPU%  MEM%  VIRT   RES   TIME+  NAME
2341   user     15.2  3.4   1.2G   512M  5:42   firefox
1822   user      8.1  2.1   852M   256M  2:31   code
```

Liste des processus actifs avec leurs consommations.

### Raccourcis clavier Glances

**Navigation :**
- `q` ou `ESC` : Quitter
- `h` : Aide (affiche tous les raccourcis)
- `a` : Trier les processus automatiquement
- `c` : Trier par CPU
- `m` : Trier par mémoire
- `i` : Trier par I/O
- `p` : Trier par nom
- `d` : Afficher/masquer les disques I/O
- `f` : Afficher/masquer le système de fichiers
- `n` : Afficher/masquer le réseau
- `s` : Afficher/masquer les capteurs
- `2` : Afficher les graphiques dans le terminal (mode sparkline)
- `l` : Afficher les logs
- `1` : Afficher tous les cœurs CPU séparément

**Processus :**
- `k` : Tuer un processus (demande le PID)
- `z` : Afficher/masquer les processus à 0%

**Export :**
- `x` : Exporter les stats (CSV)

### Mode serveur (accès via web)

Glances peut être lancé en mode serveur pour accès distant.

#### Lancer le serveur

```bash
glances -w
```

L'option `-w` active le serveur web.

Par défaut, écoute sur le port 61208.

**Accéder via navigateur :**

```
http://localhost:61208
```

Ou depuis un autre ordinateur :

```
http://adresse_ip:61208
```

#### Changer le port

```bash
glances -w -p 8080
```

Le serveur écoutera sur le port 8080.

#### Avec authentification

Pour sécuriser l'accès :

```bash
glances -w --username admin --password motdepasse
```

Ou définissez un mot de passe interactivement :

```bash
glances -w --password
```

#### Configurer le pare-feu

```bash
sudo ufw allow 61208/tcp
```

### Mode client-serveur (terminal)

Glances peut se connecter à un autre Glances distant.

#### Sur le serveur

```bash
glances -s
```

Lance Glances en mode serveur (port 61209 par défaut).

#### Sur le client

```bash
glances -c @adresse_ip
```

Exemple :

```bash
glances -c @192.168.1.100
```

Vous voyez les stats du serveur distant dans votre terminal !

### Configuration de Glances

Le fichier de configuration (optionnel) :

```bash
mkdir -p ~/.config/glances
nano ~/.config/glances/glances.conf
```

#### Personnaliser les seuils

```ini
[cpu]
user_careful=50
user_warning=70
user_critical=90

[mem]
careful=50
warning=70
critical=90
```

**Couleurs :**
- Vert : Careful (attention)
- Jaune : Warning (avertissement)
- Rouge : Critical (critique)

#### Désactiver des sections

```ini
[diskio]
disable=False

[network]
disable=False

[sensors]
disable=True
```

#### Exporter automatiquement

Exportez les données en CSV automatiquement :

```ini
[csv]
export_path=/tmp/glances
```

### Export des données

#### Export CSV

En mode serveur :

```bash
glances -w --export csv --export-csv-file /tmp/glances.csv
```

Toutes les secondes, les stats sont ajoutées au fichier CSV.

#### Export JSON

```bash
glances -w --export json --export-json-file /tmp/glances.json
```

#### Vers une base de données

Glances peut exporter vers :
- **InfluxDB** : Base de données de séries temporelles
- **Prometheus** : Système de monitoring
- **Elasticsearch** : Recherche et analyse

Exemple avec InfluxDB :

```bash
glances --export influxdb
```

(Nécessite configuration préalable d'InfluxDB)

### Plugins Glances

Glances supporte des plugins pour surveiller :

- **Docker** : Conteneurs
- **GPU** : Cartes graphiques NVIDIA
- **RAID** : Arrays RAID
- **Smart** : Santé des disques durs
- **WiFi** : Réseaux sans fil

#### Activer le plugin Docker

```bash
glances --enable-plugin docker
```

Les conteneurs Docker apparaissent dans une section dédiée.

#### Activer le plugin GPU (NVIDIA)

Installez les outils NVIDIA :

```bash
sudo apt install nvidia-utils
```

Lancez Glances :

```bash
glances --enable-plugin gpu
```

La section GPU affiche utilisation et température.

---

## Comparaison Netdata vs Glances en pratique

### Utilisation des ressources

**Test sur un serveur avec 4GB RAM :**

- **Netdata** : ~50 MB RAM, CPU ~1-2%
- **Glances** : ~15 MB RAM, CPU <1%

**Conclusion :** Glances est plus léger.

### Facilité d'accès

- **Netdata** : Nécessite un navigateur, mais interface superbe
- **Glances** : Direct dans le terminal, mais moins visuel

### Détails des métriques

- **Netdata** : Centaines de graphiques, historique long
- **Glances** : Vue d'ensemble, historique limité

### Cas d'usage idéaux

**Netdata :**
- Surveillance 24/7 d'un serveur en production
- Besoin d'alertes sophistiquées
- Équipe travaillant avec interface web
- Analyse de problèmes complexes

**Glances :**
- Diagnostic rapide d'un problème
- Connexion SSH rapide pour vérifier un serveur
- Machines avec peu de ressources
- Préférence pour le terminal

---

## Autres outils de monitoring

### btop++ (alternative moderne à htop)

Interface encore plus jolie que htop :

```bash
sudo apt install btop
btop
```

**Avantages :**
- Interface magnifique en ASCII art
- Graphiques dans le terminal
- Support de la souris

### nmon (IBM)

Outil de monitoring très complet :

```bash
sudo apt install nmon
nmon
```

Appuyez sur des touches pour activer des sections (c=CPU, m=RAM, etc.)

### Prometheus + Grafana (solution professionnelle)

Pour monitoring de production :

- **Prometheus** : Collecte les métriques
- **Grafana** : Affiche des dashboards magnifiques

**Avantages :**
- Extrêmement puissant
- Alertes avancées
- Graphiques personnalisables
- Multi-serveurs

**Inconvénients :**
- Configuration complexe
- Lourd en ressources

### Zabbix

Solution enterprise de monitoring :

- Surveillance de réseaux entiers
- Interface web complète
- Alertes sophistiquées
- Cartes réseau

**Avantages :** Très complet, professionnel
**Inconvénients :** Complexe à configurer

---

## Monitoring avancé

### Surveiller la température

#### Installer lm-sensors

```bash
sudo apt install lm-sensors
sudo sensors-detect
```

Répondez "YES" à toutes les questions.

#### Afficher les températures

```bash
sensors
```

Résultat :

```
coretemp-isa-0000
Adapter: ISA adapter
Package id 0:  +45.0°C  (high = +80.0°C, crit = +100.0°C)
Core 0:        +42.0°C  (high = +80.0°C, crit = +100.0°C)
Core 1:        +44.0°C  (high = +80.0°C, crit = +100.0°C)
```

Netdata et Glances afficheront automatiquement ces températures.

### Surveiller la santé des disques (SMART)

#### Installer smartmontools

```bash
sudo apt install smartmontools
```

#### Vérifier un disque

```bash
sudo smartctl -a /dev/sda
```

Affiche toutes les informations SMART du disque.

#### Tester un disque

**Test rapide :**

```bash
sudo smartctl -t short /dev/sda
```

**Test complet :**

```bash
sudo smartctl -t long /dev/sda
```

**Voir les résultats :**

```bash
sudo smartctl -a /dev/sda | grep -A 10 "Self-test"
```

### Surveiller le réseau en détail

#### iftop - Bande passante en temps réel

```bash
sudo apt install iftop
sudo iftop
```

Affiche quelles connexions utilisent la bande passante.

#### nethogs - Par processus

```bash
sudo apt install nethogs
sudo nethogs
```

Affiche quel processus utilise le réseau.

#### vnstat - Statistiques long terme

```bash
sudo apt install vnstat
vnstat -l
```

Garde un historique de la consommation réseau.

---

## Alertes et notifications

### Créer un script de monitoring simple

Créez un script pour surveiller l'utilisation CPU :

```bash
nano ~/monitor-cpu.sh
```

Ajoutez :

```bash
#!/bin/bash

THRESHOLD=80
CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')

if (( $(echo "$CPU_USAGE > $THRESHOLD" | bc -l) )); then
    notify-send "Alerte CPU" "Utilisation CPU : ${CPU_USAGE}%"
    echo "$(date): CPU à ${CPU_USAGE}%" >> ~/cpu_alerts.log
fi
```

Rendez-le exécutable :

```bash
chmod +x ~/monitor-cpu.sh
```

Testez :

```bash
~/monitor-cpu.sh
```

### Automatiser avec cron

Exécutez le script toutes les 5 minutes :

```bash
crontab -e
```

Ajoutez :

```
*/5 * * * * /home/votre_nom/monitor-cpu.sh
```

Vous recevrez une notification si le CPU dépasse 80%.

### Alertes par email

Installez `mailutils` :

```bash
sudo apt install mailutils
```

Modifiez votre script :

```bash
if (( $(echo "$CPU_USAGE > $THRESHOLD" | bc -l) )); then
    echo "CPU à ${CPU_USAGE}%" | mail -s "Alerte CPU" votre@email.com
fi
```

### Alertes Telegram (avancé)

Créez un bot Telegram et obtenez votre TOKEN et CHAT_ID.

Script :

```bash
#!/bin/bash

TOKEN="votre_token_bot"
CHAT_ID="votre_chat_id"
MESSAGE="⚠️ CPU élevé : ${CPU_USAGE}%"

curl -s -X POST "https://api.telegram.org/bot${TOKEN}/sendMessage" \
    -d chat_id="${CHAT_ID}" \
    -d text="${MESSAGE}"
```

---

## Sécuriser l'accès distant

### Netdata : Reverse proxy avec Nginx

Au lieu d'ouvrir le port 19999, utilisez un reverse proxy avec authentification.

#### Installer Nginx

```bash
sudo apt install nginx apache2-utils
```

#### Créer un utilisateur

```bash
sudo htpasswd -c /etc/nginx/.htpasswd admin
```

Entrez un mot de passe.

#### Configurer Nginx

```bash
sudo nano /etc/nginx/sites-available/netdata
```

Ajoutez :

```nginx
server {
    listen 80;
    server_name votre-domaine.com;

    location / {
        proxy_pass http://127.0.0.1:19999;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;

        auth_basic "Zone protégée";
        auth_basic_user_file /etc/nginx/.htpasswd;
    }
}
```

Activez :

```bash
sudo ln -s /etc/nginx/sites-available/netdata /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

Configurez Netdata pour écouter uniquement sur localhost :

```bash
sudo nano /etc/netdata/netdata.conf
```

```ini
[web]
    bind to = 127.0.0.1
```

Redémarrez :

```bash
sudo systemctl restart netdata
```

Maintenant, accédez via `http://votre-domaine.com` avec authentification !

### Glances : Authentification

Lancez avec mot de passe :

```bash
glances -w --password
```

Entrez un mot de passe. Glances demandera ce mot de passe pour l'accès web.

---

## Dépannage

### Netdata ne démarre pas

**Vérifiez les logs :**

```bash
sudo journalctl -u netdata -n 50
```

**Vérifiez le port :**

```bash
sudo netstat -tulpn | grep 19999
```

Si un autre service utilise le port, changez le port de Netdata.

### Glances : Aucune température affichée

**Installez lm-sensors :**

```bash
sudo apt install lm-sensors
sudo sensors-detect
```

Relancez Glances.

### Netdata : Consommation mémoire élevée

Limitez l'historique dans `/etc/netdata/netdata.conf` :

```ini
[global]
    history = 3600
```

3600 secondes = 1 heure d'historique.

### Glances : Mode web ne fonctionne pas

**Vérifiez le port :**

```bash
sudo netstat -tulpn | grep 61208
```

**Vérifiez le pare-feu :**

```bash
sudo ufw status
```

Autorisez le port si nécessaire.

### Alertes Netdata ne fonctionnent pas

**Testez la configuration :**

```bash
sudo /etc/netdata/edit-config health_alarm_notify.conf
```

Vérifiez que `SEND_EMAIL="YES"` et que l'email est correct.

**Testez manuellement :**

```bash
sudo /usr/libexec/netdata/plugins.d/alarm-notify.sh test
```

---

## Bonnes pratiques

### Organisation

1. **Consultez régulièrement** : Prenez l'habitude de vérifier Netdata/Glances
2. **Établissez des bases** : Notez les valeurs normales de votre système
3. **Surveillez les tendances** : Une augmentation progressive peut indiquer un problème
4. **Documentez** : Notez les changements de configuration

### Performance

1. **N'ouvrez pas trop de dashboards** : Chaque navigateur ouvert consomme des ressources
2. **Limitez l'historique** : Si Netdata consomme trop, réduisez l'historique
3. **Désactivez les plugins inutiles** : Netdata a beaucoup de plugins, désactivez ceux non utilisés

### Sécurité

1. **Ne laissez pas Netdata ouvert à Internet** sans authentification
2. **Utilisez HTTPS** : Surtout pour l'accès distant
3. **Changez les ports par défaut** : Sécurité par obscurité
4. **Surveillez les logs** : Vérifiez qui accède à vos outils de monitoring

### Alertes

1. **Ne soyez pas submergé** : Configurez des seuils raisonnables
2. **Priorisez** : Distinguez les alertes critiques des warnings
3. **Testez** : Vérifiez que les notifications fonctionnent
4. **Documentez** : Expliquez pourquoi chaque alerte existe

---

## Commandes de référence rapide

### Netdata

```bash
sudo systemctl start netdata         # Démarrer
sudo systemctl stop netdata          # Arrêter
sudo systemctl restart netdata       # Redémarrer
sudo systemctl status netdata        # État
sudo journalctl -u netdata -f        # Voir les logs en temps réel
```

### Glances

```bash
glances                              # Mode terminal
glances -w                           # Mode web
glances -s                           # Mode serveur
glances -c @192.168.1.100           # Se connecter à un serveur
glances --export csv                 # Exporter en CSV
glances -t 5                         # Rafraîchir toutes les 5 secondes
```

### Outils système

```bash
top                                  # Processus basique
htop                                 # Processus avancé
sensors                              # Températures
smartctl -a /dev/sda                 # Santé disque
iotop                                # I/O disque
iftop                                # Réseau
```

---

## Conclusion

Vous maîtrisez maintenant le monitoring système sur Linux Mint !

**Points clés à retenir :**
1. **Netdata** offre une interface web magnifique et complète
2. **Glances** est parfait pour du diagnostic rapide en terminal
3. Le **monitoring préventif** évite les pannes
4. Les **alertes** vous préviennent des problèmes avant qu'ils ne soient critiques
5. **Sécurisez** toujours l'accès distant à vos outils

**Prochaines étapes :**
- Installez Netdata ou Glances (ou les deux !)
- Explorez les différentes métriques disponibles
- Configurez des alertes pour les valeurs critiques
- Surveillez l'évolution de votre système sur plusieurs jours
- Expérimentez avec les exports de données

Le monitoring système transforme votre façon de gérer Linux : vous passez du mode réactif (réparer après problème) au mode proactif (prévenir les problèmes) ! 📊✨

---

## Ressources supplémentaires

### Documentation officielle
- Netdata : [learn.netdata.cloud](https://learn.netdata.cloud)
- Glances : [nicolargo.github.io/glances/](https://nicolargo.github.io/glances/)

### Communautés
- Netdata Discord
- r/selfhosted (Reddit)
- r/homelab (Reddit)
- Forums Linux Mint

### Tutoriels avancés
- DigitalOcean : Guides Netdata et Glances
- Awesome-Selfhosted : Liste d'outils de monitoring
- Learn Linux TV (YouTube)

Bon monitoring ! 🖥️📈

⏭️ [Accessibilité](/22-accessibilite/README.md)
