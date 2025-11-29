🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 11.7 Pare-feu avancé et règles personnalisées

## Introduction

Un **pare-feu** (firewall en anglais) est votre première ligne de défense contre les intrusions réseau. Il agit comme un gardien qui décide quelles connexions sont autorisées à entrer ou sortir de votre ordinateur.

Dans ce chapitre, nous allons explorer :
- Les concepts fondamentaux des pare-feu
- UFW (Uncomplicated Firewall) en profondeur
- La création de règles personnalisées
- Les techniques avancées
- Une introduction à iptables pour les plus curieux

---

## Comprendre les pare-feu

### Qu'est-ce qu'un pare-feu ?

Un pare-feu **filtre le trafic réseau** selon des règles prédéfinies :
- Il **autorise** ou **bloque** les connexions
- Il peut filtrer par **adresse IP**, **port**, **protocole**, **application**
- Il protège contre les accès non autorisés

**Analogie** : Imaginez un club privé avec un videur. Le videur (pare-feu) vérifie chaque personne (paquet réseau) qui veut entrer ou sortir. Il consulte sa liste (règles) pour décider qui peut passer.

### Trafic entrant vs sortant

#### Trafic entrant (INPUT)
Connexions qui **arrivent** vers votre ordinateur depuis l'extérieur.
- Exemples : Quelqu'un qui se connecte à votre serveur SSH, accède à votre serveur web

#### Trafic sortant (OUTPUT)
Connexions qui **partent** de votre ordinateur vers l'extérieur.
- Exemples : Vous naviguez sur Internet, vous envoyez un email

#### Trafic transféré (FORWARD)
Connexions qui **traversent** votre ordinateur (routage).
- Exemples : Votre ordinateur agit comme routeur ou passerelle

### Politique par défaut

Un pare-feu a des **politiques par défaut** pour le trafic non explicitement défini :

- **ACCEPT** : Tout passer (dangereux, pas recommandé)
- **DROP** : Bloquer silencieusement (recommandé)
- **REJECT** : Bloquer et notifier l'expéditeur

**Configuration recommandée** :
- Trafic entrant : **DROP** (bloquer par défaut)
- Trafic sortant : **ACCEPT** (autoriser par défaut)
- Trafic transféré : **DROP** (bloquer par défaut)

Ensuite, on crée des **exceptions** pour autoriser ce dont on a besoin.

---

## UFW : Rappel des bases

### Installation et activation

UFW est installé par défaut sur Linux Mint, mais pas activé.

#### Vérifier l'état

```bash
sudo ufw status
```

Résultat si désactivé :
```
Status: inactive
```

#### Activer UFW

```bash
sudo ufw enable
```

#### Vérifier l'état détaillé

```bash
sudo ufw status verbose
```

Résultat :
```
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip
```

### Règles de base

#### Autoriser un port

```bash
sudo ufw allow 22
```

Autorise le port 22 (SSH) en TCP et UDP.

#### Bloquer un port

```bash
sudo ufw deny 23
```

Bloque le port 23 (Telnet).

#### Supprimer une règle

```bash
sudo ufw delete allow 22
```

#### Réinitialiser UFW

```bash
sudo ufw reset
```

**Attention** : Cela supprime toutes les règles et désactive le pare-feu.

---

## Règles UFW avancées

### Spécifier le protocole

Par défaut, UFW applique les règles à TCP et UDP. Pour être plus précis :

#### Autoriser uniquement TCP

```bash
sudo ufw allow 80/tcp
```

#### Autoriser uniquement UDP

```bash
sudo ufw allow 53/udp
```

#### Autoriser les deux explicitement

```bash
sudo ufw allow 443/tcp
sudo ufw allow 443/udp
```

### Autoriser une plage de ports

#### Ports consécutifs

```bash
sudo ufw allow 6000:6007/tcp
```

Autorise les ports 6000 à 6007 en TCP (utile pour X11 forwarding).

#### Exemple pour les jeux

```bash
sudo ufw allow 27015:27030/udp
```

### Filtrer par adresse IP

#### Autoriser une IP spécifique

```bash
sudo ufw allow from 192.168.1.100
```

Autorise **toutes** les connexions depuis 192.168.1.100.

#### Autoriser une IP sur un port spécifique

```bash
sudo ufw allow from 192.168.1.100 to any port 22
```

Autorise uniquement les connexions SSH depuis 192.168.1.100.

#### Bloquer une IP

```bash
sudo ufw deny from 203.0.113.50
```

Bloque toutes les connexions depuis cette IP (utile contre les attaquants).

### Filtrer par sous-réseau

#### Autoriser un réseau local complet

```bash
sudo ufw allow from 192.168.1.0/24
```

Autorise tous les ordinateurs du réseau 192.168.1.0 à 192.168.1.255.

#### Autoriser un réseau sur un port

```bash
sudo ufw allow from 10.0.0.0/8 to any port 445
```

Autorise le partage de fichiers (SMB) uniquement depuis le réseau local 10.x.x.x.

### Filtrer par interface réseau

Utile quand vous avez plusieurs cartes réseau (ethernet, wifi, VPN).

#### Lister les interfaces

```bash
ip addr show
```

Ou :
```bash
ifconfig
```

Interfaces courantes :
- `lo` : Loopback (localhost)
- `eth0`, `enp3s0` : Ethernet
- `wlan0`, `wlp2s0` : WiFi
- `tun0` : VPN

#### Autoriser sur une interface spécifique

```bash
sudo ufw allow in on eth0 to any port 80
```

Autorise le port 80 uniquement sur l'interface ethernet.

#### Exemple pratique : Serveur web accessible uniquement en local

```bash
sudo ufw allow in on lo to any port 80
```

Le serveur web n'est accessible que depuis localhost (127.0.0.1).

### Autoriser par nom de service

UFW reconnaît les services communs définis dans `/etc/services`.

```bash
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
```

Équivalent à :
```bash
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

### Règles de rejet vs refus

#### DENY (par défaut)

```bash
sudo ufw deny from 198.51.100.50
```

Bloque silencieusement (DROP). L'attaquant ne reçoit aucune réponse.

#### REJECT

```bash
sudo ufw reject from 198.51.100.50
```

Bloque mais envoie une notification "port unreachable". Plus poli mais révèle l'existence du pare-feu.

**Recommandation** : Utilisez DENY pour la sécurité, REJECT pour le dépannage.

---

## Ordre et priorité des règles

### Comment UFW traite les règles

UFW lit les règles **de haut en bas** et applique la **première règle correspondante**.

#### Voir les règles numérotées

```bash
sudo ufw status numbered
```

Résultat :
```
Status: active

     To                         Action      From
     --                         ------      ----
[ 1] 22/tcp                     ALLOW IN    Anywhere
[ 2] 80/tcp                     ALLOW IN    Anywhere
[ 3] Anywhere                   DENY IN     203.0.113.100
[ 4] 22/tcp (v6)                ALLOW IN    Anywhere (v6)
[ 5] 80/tcp (v6)                ALLOW IN    Anywhere (v6)
```

### Insérer une règle à une position spécifique

Par défaut, les nouvelles règles sont ajoutées à la fin. Pour insérer en première position :

```bash
sudo ufw insert 1 deny from 203.0.113.100
```

Cela place la règle en position 1 (avant toutes les autres).

### Supprimer par numéro

```bash
sudo ufw delete 3
```

Supprime la règle numéro 3.

### Exemple d'ordre important

**Problème** : Vous voulez bloquer une IP spécifique mais autoriser SSH pour tout le monde.

**Mauvais ordre** :
```bash
sudo ufw allow 22/tcp
sudo ufw deny from 203.0.113.100
```

Résultat : L'IP 203.0.113.100 peut quand même se connecter en SSH (règle 1 appliquée en premier).

**Bon ordre** :
```bash
sudo ufw deny from 203.0.113.100
sudo ufw allow 22/tcp
```

Ou mieux, avec insertion :
```bash
sudo ufw allow 22/tcp
sudo ufw insert 1 deny from 203.0.113.100
```

---

## Limitation de débit (Rate Limiting)

La **limitation de débit** protège contre les attaques par force brute en limitant le nombre de connexions par IP.

### Activer le rate limiting sur SSH

```bash
sudo ufw limit ssh
```

Ou :
```bash
sudo ufw limit 22/tcp
```

**Fonctionnement** : Si une IP tente plus de 6 connexions en 30 secondes, elle est temporairement bloquée.

### Syntaxe générale

```bash
sudo ufw limit PROTOCOLE/PORT
```

### Cas d'usage recommandés

- ✅ SSH (port 22) : Protection contre le brute force
- ✅ Services d'authentification
- ✅ Formulaires de connexion web

### Voir les règles de limitation

```bash
sudo ufw status
```

Les règles avec limitation affichent `LIMIT` au lieu de `ALLOW`.

---

## Profils d'application

UFW peut utiliser des **profils d'application** prédéfinis pour simplifier la configuration.

### Lister les profils disponibles

```bash
sudo ufw app list
```

Résultat exemple :
```
Available applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH
  Samba
```

### Voir les détails d'un profil

```bash
sudo ufw app info OpenSSH
```

Résultat :
```
Profile: OpenSSH
Title: Secure shell server
Description: SSH server and SFTP server

Port:
  22/tcp
```

### Autoriser un profil

```bash
sudo ufw allow OpenSSH
```

Équivalent à :
```bash
sudo ufw allow 22/tcp
```

Mais plus lisible et maintenable.

### Profils courants

| Profil | Ports | Usage |
|--------|-------|-------|
| `OpenSSH` | 22/tcp | Serveur SSH |
| `Apache` | 80/tcp | Serveur web HTTP |
| `Apache Secure` | 443/tcp | Serveur web HTTPS |
| `Apache Full` | 80,443/tcp | HTTP + HTTPS |
| `Nginx Full` | 80,443/tcp | Nginx HTTP + HTTPS |
| `Samba` | 137,138/udp, 139,445/tcp | Partage de fichiers |

### Créer un profil personnalisé

Les profils sont stockés dans `/etc/ufw/applications.d/`.

#### Créer un fichier de profil

```bash
sudo nano /etc/ufw/applications.d/mon-application
```

Contenu exemple pour un serveur Node.js :
```
[NodeJS]
title=Node.js Web Server
description=Node.js application server
ports=3000/tcp
```

#### Recharger les profils

```bash
sudo ufw app update NodeJS
```

#### Utiliser le profil

```bash
sudo ufw allow NodeJS
```

---

## Logging et surveillance

### Activer les logs

```bash
sudo ufw logging on
```

Niveaux de log disponibles :
- `off` : Désactivé
- `low` : Connexions bloquées seulement
- `medium` : Connexions bloquées + autorisées + paquets invalides
- `high` : Détails maximaux (très verbeux)
- `full` : Tout (peut ralentir le système)

**Recommandé** : `low` ou `medium`.

```bash
sudo ufw logging medium
```

### Consulter les logs

Les logs sont dans `/var/log/ufw.log`.

```bash
sudo tail -f /var/log/ufw.log
```

### Exemple de ligne de log

```
Nov 29 10:45:32 linux-mint kernel: [UFW BLOCK] IN=eth0 OUT= MAC=... SRC=203.0.113.50 DST=192.168.1.100 LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=12345 PROTO=TCP SPT=45678 DPT=22 WINDOW=29200 SYN
```

Décodage :
- `UFW BLOCK` : Paquet bloqué
- `SRC=203.0.113.50` : IP source (attaquant)
- `DST=192.168.1.100` : IP destination (vous)
- `DPT=22` : Port de destination (SSH)
- `PROTO=TCP` : Protocole
- `SYN` : Tentative de connexion

### Analyser les logs

#### Voir les tentatives de connexion bloquées

```bash
sudo grep "UFW BLOCK" /var/log/ufw.log | tail -20
```

#### Compter les tentatives par IP

```bash
sudo grep "UFW BLOCK" /var/log/ufw.log | grep -oP 'SRC=\K[0-9.]+' | sort | uniq -c | sort -rn | head -10
```

#### Voir les ports les plus ciblés

```bash
sudo grep "UFW BLOCK" /var/log/ufw.log | grep -oP 'DPT=\K[0-9]+' | sort | uniq -c | sort -rn | head -10
```

---

## GUFW : Interface graphique

Pour ceux qui préfèrent une interface graphique, **GUFW** (Graphical UFW) est excellent.

### Installation

```bash
sudo apt install gufw
```

### Lancement

Depuis le menu : **Préférences** → **Pare-feu**

Ou :
```bash
gufw
```

### Utilisation de GUFW

#### 1. Activer/Désactiver le pare-feu

Basculez l'interrupteur en haut de la fenêtre.

#### 2. Définir le profil

Choisissez parmi :
- **Home** : Réseau domestique (plus permissif)
- **Public** : Réseau public (plus restrictif)
- **Office** : Réseau de bureau

Ces profils ne sont que des suggestions. Vous pouvez personnaliser ensuite.

#### 3. Ajouter des règles

- Cliquez sur le bouton **"+"** (Ajouter)
- Choisissez :
  - **Simple** : Autorise un service prédéfini
  - **Préconfigured** : Utilise un profil d'application
  - **Advanced** : Règle personnalisée complète

##### Mode Simple
- **Politique** : Allow ou Deny
- **Direction** : In (entrant), Out (sortant), Both
- **Service** : SSH, HTTP, HTTPS, etc.

##### Mode Avancé
- Spécifier IP source/destination
- Port source/destination
- Protocole (TCP, UDP, Both)
- Interface réseau

#### 4. Voir et modifier les règles

Les règles sont listées dans la fenêtre principale.
- Sélectionnez une règle et cliquez sur **"-"** pour la supprimer
- Double-cliquez pour modifier

#### 5. Configurer les logs

**Édition** → **Préférences** → Onglet **Logs**

---

## Cas d'usage pratiques

### Cas 1 : Serveur web accessible depuis Internet

**Objectif** : Autoriser HTTP et HTTPS pour tout le monde, SSH uniquement depuis votre IP.

```bash
# Autoriser HTTP/HTTPS pour tous
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Autoriser SSH uniquement depuis votre IP
sudo ufw allow from VOTRE_IP to any port 22

# Activer le pare-feu
sudo ufw enable
```

### Cas 2 : Serveur de jeu Minecraft

**Objectif** : Autoriser le port Minecraft (25565).

```bash
sudo ufw allow 25565/tcp
sudo ufw enable
```

### Cas 3 : Partage de fichiers local (Samba)

**Objectif** : Autoriser Samba uniquement sur le réseau local.

```bash
sudo ufw allow from 192.168.1.0/24 to any app Samba
sudo ufw enable
```

### Cas 4 : Serveur de développement local

**Objectif** : Autoriser les ports 3000 (Node.js), 8080 (autre app) uniquement en localhost.

```bash
sudo ufw allow in on lo to any port 3000
sudo ufw allow in on lo to any port 8080
sudo ufw enable
```

### Cas 5 : VPN WireGuard

**Objectif** : Autoriser le port VPN et le trafic transféré.

```bash
# Port VPN
sudo ufw allow 51820/udp

# Autoriser le transfert
sudo ufw route allow in on wg0 out on eth0
sudo ufw route allow in on eth0 out on wg0

sudo ufw enable
```

### Cas 6 : Bloquer un pays entier (géoblocking)

**Méthode avancée** : Utiliser ipset avec UFW (voir section iptables).

### Cas 7 : Autoriser ping (ICMP)

Par défaut, UFW bloque les pings entrants. Pour les autoriser :

```bash
sudo nano /etc/ufw/before.rules
```

Trouvez la section :
```
# ok icmp codes for INPUT
-A ufw-before-input -p icmp --icmp-type destination-unreachable -j ACCEPT
-A ufw-before-input -p icmp --icmp-type source-quench -j ACCEPT
-A ufw-before-input -p icmp --icmp-type time-exceeded -j ACCEPT
-A ufw-before-input -p icmp --icmp-type parameter-problem -j ACCEPT
-A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT
```

La ligne `echo-request` autorise les pings. Si elle est commentée, décommentez-la.

Rechargez UFW :
```bash
sudo ufw reload
```

---

## Introduction à iptables

UFW est une **interface simplifiée** pour iptables, le vrai pare-feu Linux. Pour des besoins très avancés, vous devrez utiliser iptables directement.

### Relation UFW ↔ iptables

```
┌─────────────┐
│     UFW     │  (Interface conviviale)
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  iptables   │  (Pare-feu réel)
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   netfilter │  (Noyau Linux)
└─────────────┘
```

### Voir les règles iptables créées par UFW

```bash
sudo iptables -L -n -v
```

Résultat : Des dizaines de lignes de règles complexes.

### Avertissement

⚠️ **N'utilisez pas iptables et UFW en même temps !**
- Soit vous utilisez UFW (recommandé pour débutants/intermédiaires)
- Soit vous utilisez iptables directement (avancé)

Si vous modifiez les règles iptables manuellement, UFW ne les connaîtra pas.

### Commandes iptables de base

#### Voir les règles

```bash
sudo iptables -L -n -v
```

Options :
- `-L` : List (lister)
- `-n` : Numérique (pas de résolution DNS)
- `-v` : Verbose (détails)

#### Bloquer une IP

```bash
sudo iptables -A INPUT -s 203.0.113.50 -j DROP
```

- `-A INPUT` : Append (ajouter) à la chaîne INPUT
- `-s` : Source
- `-j DROP` : Jump to DROP (bloquer)

#### Autoriser un port

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

- `-p tcp` : Protocole TCP
- `--dport 80` : Destination port 80
- `-j ACCEPT` : Autoriser

#### Supprimer toutes les règles

```bash
sudo iptables -F
```

**Attention** : Dangereux ! Vous pourriez perdre l'accès SSH.

#### Sauvegarder les règles iptables

```bash
sudo iptables-save > /tmp/iptables_backup.rules
```

#### Restaurer les règles

```bash
sudo iptables-restore < /tmp/iptables_backup.rules
```

### Rendre les règles iptables persistantes

Par défaut, les règles iptables sont **perdues au redémarrage**.

#### Installer iptables-persistent

```bash
sudo apt install iptables-persistent
```

Lors de l'installation, il demande si vous voulez sauvegarder les règles actuelles. Répondez **Oui**.

#### Sauvegarder après des modifications

```bash
sudo netfilter-persistent save
```

#### Restaurer au démarrage

Automatique avec iptables-persistent.

---

## UFW avancé : Personnalisation des fichiers de configuration

### Fichiers de configuration UFW

UFW utilise plusieurs fichiers dans `/etc/ufw/` :

| Fichier | Rôle |
|---------|------|
| `ufw.conf` | Configuration générale |
| `before.rules` | Règles appliquées avant les règles UFW |
| `after.rules` | Règles appliquées après les règles UFW |
| `user.rules` | Vos règles UFW (géré automatiquement) |
| `applications.d/` | Profils d'applications |

### Modifier before.rules pour des besoins spécifiques

Exemple : Autoriser le trafic local (loopback) par défaut.

```bash
sudo nano /etc/ufw/before.rules
```

Ajoutez au début :
```
# Allow all on loopback
-A INPUT -i lo -j ACCEPT
-A OUTPUT -o lo -j ACCEPT
```

Rechargez :
```bash
sudo ufw reload
```

### NAT et masquerading

Pour partager la connexion Internet (transformer Linux en routeur) :

```bash
sudo nano /etc/ufw/before.rules
```

Ajoutez après la section `*filter` :
```
*nat
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING -s 192.168.1.0/24 -o eth0 -j MASQUERADE
COMMIT
```

Puis activez le forwarding :
```bash
sudo nano /etc/ufw/sysctl.conf
```

Décommentez :
```
net/ipv4/ip_forward=1
```

Rechargez :
```bash
sudo ufw reload
```

---

## Fail2Ban : Complément au pare-feu

**Fail2Ban** n'est pas un pare-feu, mais il **collabore** avec UFW/iptables pour bloquer automatiquement les IP suspectes.

### Installation

```bash
sudo apt install fail2ban
```

### Fonctionnement

Fail2Ban :
1. Surveille les logs (SSH, Apache, etc.)
2. Détecte les tentatives de connexion échouées
3. Bloque temporairement l'IP via iptables/UFW

### Configuration de base

```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo nano /etc/fail2ban/jail.local
```

Configuration SSH :
```
[sshd]
enabled = true
port = ssh
logpath = /var/log/auth.log
maxretry = 5
bantime = 3600
```

- `maxretry` : Nombre d'échecs avant ban
- `bantime` : Durée du ban en secondes (3600 = 1 heure)

Redémarrez :
```bash
sudo systemctl restart fail2ban
```

### Vérifier les IP bannies

```bash
sudo fail2ban-client status sshd
```

### Débannir une IP

```bash
sudo fail2ban-client set sshd unbanip 203.0.113.50
```

---

## Dépannage

### "ERROR: problem running ufw-init"

**Problème** : UFW ne peut pas démarrer.

**Solutions** :
1. Vérifiez que le module netfilter est chargé :
   ```bash
   lsmod | grep ip_tables
   ```
2. Rechargez le module :
   ```bash
   sudo modprobe ip_tables
   ```
3. Redémarrez UFW :
   ```bash
   sudo ufw reload
   ```

### Règle ajoutée mais ne fonctionne pas

**Problème** : Vous ajoutez une règle mais elle n'est pas appliquée.

**Solutions** :
1. Vérifiez l'ordre des règles :
   ```bash
   sudo ufw status numbered
   ```
2. Rechargez UFW :
   ```bash
   sudo ufw reload
   ```
3. Vérifiez les logs :
   ```bash
   sudo tail /var/log/ufw.log
   ```

### Connexion SSH bloquée après activation UFW

**Problème** : Vous vous êtes enfermé dehors !

**Solution** (si vous avez accès physique) :
1. Démarrez en mode recovery
2. Montez le système en lecture-écriture :
   ```bash
   mount -o remount,rw /
   ```
3. Désactivez UFW :
   ```bash
   ufw disable
   ```
4. Redémarrez normalement
5. Ajoutez la règle SSH avant de réactiver :
   ```bash
   ufw allow 22/tcp
   ufw enable
   ```

**Prévention** : Toujours autoriser SSH AVANT d'activer UFW sur un serveur distant :
```bash
sudo ufw allow 22/tcp
sudo ufw enable
```

### UFW et Docker

**Problème** : Docker expose des ports même si UFW les bloque.

**Explication** : Docker modifie directement iptables, contournant UFW.

**Solution** : Configurez Docker pour utiliser UFW.

Éditez `/etc/docker/daemon.json` :
```json
{
  "iptables": false
}
```

Redémarrez Docker :
```bash
sudo systemctl restart docker
```

Puis gérez les ports manuellement avec UFW.

### Performance dégradée

**Problème** : Le réseau est lent après activation d'UFW.

**Solutions** :
1. Réduisez le niveau de logging :
   ```bash
   sudo ufw logging low
   ```
2. Optimisez les règles (évitez les règles trop génériques)
3. Utilisez ipset pour de grandes listes d'IP

---

## Bonnes pratiques

### Sécurité

1. ✅ **Politique par défaut restrictive** : Bloquer entrant, autoriser sortant
2. ✅ **Principe du moindre privilège** : N'autorisez que ce qui est nécessaire
3. ✅ **Limitez SSH** : Utilisez `ufw limit ssh` ou changez le port
4. ✅ **Filtrez par IP** : Restreignez les services sensibles à des IP connues
5. ✅ **Logging activé** : Au moins en mode "low"
6. ✅ **Fail2Ban** : Protection supplémentaire contre le brute force
7. ✅ **Revue régulière** : Auditez vos règles mensuellement

### Performance

1. ✅ **Règles spécifiques** : Plus une règle est précise, plus elle est rapide
2. ✅ **Ordre optimisé** : Mettez les règles fréquentes en premier
3. ✅ **Évitez le logging "high"** : Sauf pour le débogage
4. ✅ **Utilisez ipset** : Pour de longues listes d'IP/ports

### Maintenance

1. ✅ **Documentez vos règles** : Commentaires dans un fichier texte
2. ✅ **Sauvegardez la configuration** :
   ```bash
   sudo cp /etc/ufw/user.rules /root/ufw_backup_$(date +%Y%m%d).rules
   ```
3. ✅ **Testez avant de déployer** : Sur une VM ou un environnement de test
4. ✅ **Monitoring** : Surveillez les logs régulièrement

### Serveurs

1. ✅ **SSH sur un port non-standard** : Réduit les scans automatisés
2. ✅ **Whitelist IP pour les services critiques** : N'exposez pas tout à Internet
3. ✅ **VPN pour l'administration** : Serveurs non directement accessibles
4. ✅ **Surveillance des tentatives** : Analysez les logs quotidiennement

---

## Scripts utiles

### Script de configuration initiale serveur

```bash
#!/bin/bash
# Configuration UFW pour serveur web

# Désactiver UFW pour configuration
sudo ufw disable

# Réinitialiser toutes les règles
sudo ufw --force reset

# Politique par défaut
sudo ufw default deny incoming
sudo ufw default allow outgoing

# SSH avec limitation (protection brute force)
sudo ufw limit 22/tcp

# HTTP et HTTPS
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Autoriser ping
sudo ufw allow proto icmp from any

# Activer logging
sudo ufw logging low

# Activer UFW
sudo ufw --force enable

# Afficher le statut
sudo ufw status verbose
```

### Script de surveillance des tentatives de connexion

```bash
#!/bin/bash
# Script à exécuter via cron pour alerter des attaques

LOG_FILE="/var/log/ufw.log"
ALERT_THRESHOLD=10

# Compter les tentatives SSH bloquées dans la dernière heure
ATTEMPTS=$(grep "DPT=22" "$LOG_FILE" | grep "$(date +%Y-%m-%d)" | wc -l)

if [ $ATTEMPTS -gt $ALERT_THRESHOLD ]; then
    echo "ALERTE: $ATTEMPTS tentatives SSH bloquées aujourd'hui" | mail -s "UFW Alert" admin@example.com
fi
```

### Script de géoblocking (avancé)

Nécessite ipset :

```bash
#!/bin/bash
# Bloquer un pays (exemple: Chine - CN)

# Installer ipset
sudo apt install ipset

# Créer un set
sudo ipset create blocklist_cn hash:net

# Télécharger la liste d'IP du pays
wget -O - http://www.ipdeny.com/ipblocks/data/countries/cn.zone | sudo tee -a /tmp/cn_ips.txt

# Ajouter au set
while read IP; do
    sudo ipset add blocklist_cn $IP
done < /tmp/cn_ips.txt

# Créer la règle iptables
sudo iptables -I INPUT -m set --match-set blocklist_cn src -j DROP

# Rendre persistant
sudo ipset save > /etc/ipset.conf
```

---

## Commandes de référence rapide

### Gestion de base

| Commande | Description |
|----------|-------------|
| `sudo ufw enable` | Activer le pare-feu |
| `sudo ufw disable` | Désactiver le pare-feu |
| `sudo ufw status` | Voir l'état |
| `sudo ufw status numbered` | Voir les règles numérotées |
| `sudo ufw status verbose` | Voir l'état détaillé |
| `sudo ufw reload` | Recharger les règles |
| `sudo ufw reset` | Réinitialiser toutes les règles |

### Règles simples

| Commande | Description |
|----------|-------------|
| `sudo ufw allow 80` | Autoriser le port 80 |
| `sudo ufw deny 23` | Bloquer le port 23 |
| `sudo ufw allow 22/tcp` | Autoriser port 22 en TCP |
| `sudo ufw limit ssh` | Autoriser SSH avec rate limiting |
| `sudo ufw delete allow 80` | Supprimer une règle |
| `sudo ufw delete 3` | Supprimer la règle n°3 |

### Règles avancées

| Commande | Description |
|----------|-------------|
| `sudo ufw allow from 192.168.1.100` | Autoriser une IP |
| `sudo ufw allow from 192.168.1.0/24 to any port 22` | Autoriser réseau sur port |
| `sudo ufw deny from 203.0.113.50` | Bloquer une IP |
| `sudo ufw allow in on eth0 to any port 80` | Autoriser sur interface |
| `sudo ufw allow 6000:6007/tcp` | Autoriser plage de ports |

### Applications et profils

| Commande | Description |
|----------|-------------|
| `sudo ufw app list` | Lister les profils |
| `sudo ufw app info OpenSSH` | Détails d'un profil |
| `sudo ufw allow OpenSSH` | Autoriser un profil |

### Logging

| Commande | Description |
|----------|-------------|
| `sudo ufw logging on` | Activer les logs |
| `sudo ufw logging off` | Désactiver les logs |
| `sudo ufw logging low` | Logs basiques |
| `sudo ufw logging medium` | Logs détaillés |
| `sudo tail -f /var/log/ufw.log` | Voir les logs en temps réel |

---

## Résumé

### Points clés

1. **UFW est simple mais puissant** : Parfait pour 95% des besoins
2. **Politique restrictive par défaut** : Bloquer entrant, autoriser sortant
3. **Ordre des règles important** : Première règle correspondante appliquée
4. **Rate limiting essentiel** : Protège contre le brute force
5. **Logs à surveiller** : Détectez les attaques en cours
6. **Fail2Ban = complément parfait** : Ban automatique des attaquants

### Configuration minimale recommandée

Pour un ordinateur de bureau :
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
```

Pour un serveur web :
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw limit ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw logging low
sudo ufw enable
```

### Quand utiliser quoi ?

- **UFW** : 99% des cas (bureaux, serveurs simples)
- **iptables directement** : Besoins très avancés (routage complexe, QoS, etc.)
- **GUFW** : Si vous préférez une interface graphique
- **Fail2Ban** : Toujours, en complément d'UFW

Le pare-feu est votre première ligne de défense. Configurez-le correctement et surveillez-le régulièrement !

---


⏭️ [Fail2Ban pour protection SSH](/11-gestion-des-utilisateurs-et-securite/08-fail2ban-pour-protection-ssh.md)
