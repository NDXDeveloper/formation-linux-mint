🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 21.1 Configuration de serveur SSH

## Introduction

### Qu'est-ce que SSH ?

SSH (Secure Shell) est un protocole réseau qui vous permet de vous connecter à distance à votre ordinateur Linux Mint de manière sécurisée. Imaginez pouvoir contrôler votre ordinateur depuis n'importe où dans le monde, comme si vous étiez assis devant lui, mais uniquement en utilisant du texte dans un terminal.

**Cas d'usage courants :**
- Administrer un serveur à distance
- Transférer des fichiers de manière sécurisée
- Accéder à votre ordinateur personnel depuis le travail (ou vice-versa)
- Gérer plusieurs machines Linux depuis un seul poste
- Travailler sur un Raspberry Pi ou un serveur domestique

**Pourquoi "Secure" ?**
Contrairement aux anciens protocoles comme Telnet, SSH chiffre toutes les communications. Vos mots de passe et vos données sont protégés pendant le transfert.

---

## Installation du serveur SSH

Par défaut, Linux Mint n'a pas de serveur SSH installé. Vous devez l'installer manuellement.

### Vérifier si SSH est déjà installé

Ouvrez un terminal et tapez :

```bash
ssh -V
```

Cela affiche la version du client SSH (qui permet de se connecter à d'autres machines). Pour vérifier si le serveur SSH est installé :

```bash
systemctl status ssh
```

Si vous voyez "Unit ssh.service could not be found", le serveur n'est pas installé.

### Installer OpenSSH Server

OpenSSH est l'implémentation SSH la plus populaire et celle recommandée pour Linux Mint.

```bash
sudo apt update
sudo apt install openssh-server
```

Entrez votre mot de passe administrateur lorsque demandé. L'installation prend quelques secondes.

### Vérifier que le service fonctionne

Une fois installé, le serveur SSH démarre automatiquement. Pour vérifier :

```bash
systemctl status ssh
```

Vous devriez voir "active (running)" en vert. Cela signifie que votre serveur SSH est opérationnel et prêt à accepter des connexions.

---

## Configuration de base

### Fichier de configuration principal

Le fichier de configuration du serveur SSH se trouve à cet emplacement :

```
/etc/ssh/sshd_config
```

**Note importante :** `sshd_config` (avec un "d") est pour le serveur, tandis que `ssh_config` (sans "d") est pour le client.

### Éditer la configuration

Pour modifier la configuration, utilisez un éditeur de texte avec les droits administrateur :

```bash
sudo nano /etc/ssh/sshd_config
```

Nano est un éditeur simple pour débutants. Utilisez les flèches pour naviguer, et suivez les instructions en bas de l'écran (Ctrl+O pour sauvegarder, Ctrl+X pour quitter).

### Options de configuration importantes

Voici les paramètres que vous devriez connaître et éventuellement modifier :

#### Port SSH

```
Port 22
```

Par défaut, SSH utilise le port 22. Pour des raisons de sécurité, certains administrateurs changent ce port (par exemple 2222 ou 2200). Cela réduit les tentatives d'intrusion automatisées.

**Pour les débutants :** Vous pouvez laisser le port 22 si vous êtes sur un réseau domestique sécurisé.

#### Autoriser la connexion root

```
PermitRootLogin no
```

Il est fortement recommandé de mettre cette option sur `no`. Se connecter directement en tant que root (super-utilisateur) est dangereux. Il vaut mieux se connecter avec un utilisateur normal, puis utiliser `sudo` si nécessaire.

#### Authentification par mot de passe

```
PasswordAuthentication yes
```

Cette option permet de se connecter avec un mot de passe. Pour plus de sécurité, vous pouvez utiliser des clés SSH (voir section suivante) et désactiver les mots de passe (`PasswordAuthentication no`).

**Pour débuter :** Laissez `yes` pour commencer, vous pourrez sécuriser davantage plus tard.

#### Temps d'inactivité

```
ClientAliveInterval 300
ClientAliveCountMax 2
```

Ces options déconnectent automatiquement les sessions inactives après un certain temps (ici, 10 minutes d'inactivité).

### Redémarrer le service SSH

Après toute modification du fichier de configuration, vous devez redémarrer le service SSH :

```bash
sudo systemctl restart ssh
```

Pour vérifier qu'il n'y a pas d'erreur :

```bash
sudo systemctl status ssh
```

---

## Sécurisation du serveur SSH

### Créer des clés SSH (authentification par clé)

L'authentification par clé est plus sécurisée que les mots de passe. Voici comment procéder :

#### Sur la machine cliente (celle d'où vous vous connectez)

Générez une paire de clés SSH :

```bash
ssh-keygen -t ed25519 -C "votre_email@example.com"
```

Appuyez sur Entrée pour accepter l'emplacement par défaut (`~/.ssh/id_ed25519`). Vous pouvez ajouter une phrase de passe pour plus de sécurité (recommandé) ou laisser vide.

**Explication :**
- `-t ed25519` : type de clé moderne et sécurisé
- `-C` : commentaire pour identifier votre clé

#### Copier la clé publique vers le serveur

```bash
ssh-copy-id utilisateur@adresse_ip_serveur
```

Exemple :
```bash
ssh-copy-id jean@192.168.1.100
```

Entrez le mot de passe de l'utilisateur sur le serveur. Votre clé publique sera automatiquement ajoutée.

#### Tester la connexion

```bash
ssh utilisateur@adresse_ip_serveur
```

Vous devriez pouvoir vous connecter sans entrer de mot de passe (ou juste la phrase de passe de votre clé si vous en avez défini une).

#### Désactiver l'authentification par mot de passe (optionnel)

Une fois que les clés fonctionnent, vous pouvez désactiver complètement les mots de passe :

```bash
sudo nano /etc/ssh/sshd_config
```

Changez :
```
PasswordAuthentication no
```

Redémarrez SSH :
```bash
sudo systemctl restart ssh
```

### Utiliser le pare-feu (UFW)

Le pare-feu protège votre serveur en bloquant les connexions non autorisées.

#### Installer et activer UFW

```bash
sudo apt install ufw
sudo ufw enable
```

#### Autoriser SSH

**IMPORTANT :** Autorisez SSH AVANT d'activer le pare-feu, sinon vous risquez de vous bloquer !

```bash
sudo ufw allow ssh
```

Ou si vous avez changé le port SSH :
```bash
sudo ufw allow 2222/tcp
```

#### Vérifier les règles

```bash
sudo ufw status
```

Vous devriez voir SSH dans la liste des services autorisés.

### Limiter les tentatives de connexion (Fail2Ban)

Fail2Ban bloque automatiquement les adresses IP qui tentent trop de connexions échouées.

#### Installation

```bash
sudo apt install fail2ban
```

#### Configuration de base

Créez un fichier de configuration local :

```bash
sudo nano /etc/fail2ban/jail.local
```

Ajoutez :
```
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 3600
```

**Explications :**
- `maxretry = 3` : Nombre de tentatives échouées autorisées
- `bantime = 3600` : Durée du bannissement en secondes (1 heure)

#### Redémarrer Fail2Ban

```bash
sudo systemctl restart fail2ban
sudo systemctl enable fail2ban
```

---

## Se connecter au serveur SSH

### Depuis Linux ou macOS

Ouvrez un terminal et utilisez :

```bash
ssh utilisateur@adresse_ip
```

Exemples :
```bash
ssh jean@192.168.1.100
ssh admin@monserveur.com
ssh -p 2222 utilisateur@192.168.1.50  # Si vous avez changé le port
```

Lors de la première connexion, vous verrez un message concernant l'authenticité de l'hôte. Tapez `yes` pour continuer.

### Depuis Windows

#### Option 1 : PowerShell ou CMD (Windows 10/11)

Windows 10 et 11 incluent un client SSH. Ouvrez PowerShell ou l'invite de commandes :

```
ssh utilisateur@adresse_ip
```

#### Option 2 : PuTTY

PuTTY est un client SSH graphique gratuit pour Windows :

1. Téléchargez PuTTY depuis [putty.org](https://www.putty.org/)
2. Lancez PuTTY
3. Dans "Host Name", entrez l'adresse IP de votre serveur
4. Port : 22 (ou votre port personnalisé)
5. Cliquez sur "Open"
6. Entrez votre nom d'utilisateur et mot de passe

### Trouver l'adresse IP de votre serveur

Sur le serveur Linux Mint, tapez :

```bash
ip a
```

ou

```bash
hostname -I
```

Cherchez l'adresse IP locale (généralement 192.168.x.x ou 10.x.x.x).

---

## Transfert de fichiers avec SSH

### Utiliser SCP (Secure Copy)

SCP utilise SSH pour copier des fichiers de manière sécurisée.

#### Copier un fichier vers le serveur

```bash
scp fichier.txt utilisateur@192.168.1.100:/home/utilisateur/
```

#### Copier un fichier depuis le serveur

```bash
scp utilisateur@192.168.1.100:/home/utilisateur/fichier.txt ./
```

#### Copier un dossier complet

```bash
scp -r dossier/ utilisateur@192.168.1.100:/home/utilisateur/
```

L'option `-r` signifie "récursif" (pour les dossiers).

### Utiliser SFTP

SFTP (SSH File Transfer Protocol) permet de transférer des fichiers de manière interactive.

```bash
sftp utilisateur@192.168.1.100
```

Commandes SFTP utiles :
- `ls` : lister les fichiers distants
- `cd` : changer de dossier distant
- `get fichier.txt` : télécharger un fichier
- `put fichier.txt` : envoyer un fichier
- `exit` : quitter

### Clients graphiques

Pour une interface graphique, vous pouvez utiliser :
- **FileZilla** : client FTP/SFTP populaire
- **Nautilus** (gestionnaire de fichiers) : Tapez `sftp://utilisateur@adresse_ip` dans la barre d'adresse
- **WinSCP** (Windows) : client graphique pour Windows

---

## Gestion du service SSH

### Démarrer le service

```bash
sudo systemctl start ssh
```

### Arrêter le service

```bash
sudo systemctl stop ssh
```

### Redémarrer le service

```bash
sudo systemctl restart ssh
```

### Activer au démarrage

Pour que SSH démarre automatiquement au démarrage du système :

```bash
sudo systemctl enable ssh
```

### Désactiver au démarrage

```bash
sudo systemctl disable ssh
```

### Vérifier l'état

```bash
sudo systemctl status ssh
```

---

## Conseils de sécurité supplémentaires

### 1. Utilisez des mots de passe forts

Si vous utilisez l'authentification par mot de passe, assurez-vous que tous vos utilisateurs ont des mots de passe robustes :
- Au moins 12 caractères
- Mélange de majuscules, minuscules, chiffres et symboles
- Pas de mots du dictionnaire

### 2. Limitez les utilisateurs autorisés

Dans `/etc/ssh/sshd_config`, vous pouvez spécifier quels utilisateurs peuvent se connecter :

```
AllowUsers jean marie admin
```

Ou interdire certains utilisateurs :

```
DenyUsers invite test
```

### 3. Utilisez un VPN pour l'accès externe

Si vous ouvrez SSH à Internet, envisagez d'utiliser un VPN pour une couche de sécurité supplémentaire. Cela évite d'exposer directement SSH à Internet.

### 4. Surveillez les logs

Les tentatives de connexion sont enregistrées dans :

```bash
sudo tail -f /var/log/auth.log
```

Vérifiez régulièrement ce fichier pour détecter des activités suspectes.

### 5. Mettez à jour régulièrement

```bash
sudo apt update
sudo apt upgrade
```

Les mises à jour de sécurité sont cruciales pour garder SSH sécurisé.

### 6. Désactivez les protocoles SSH anciens

Dans `/etc/ssh/sshd_config`, assurez-vous que seul SSH version 2 est autorisé :

```
Protocol 2
```

---

## Accès SSH depuis Internet

### Attention aux risques

Ouvrir SSH à Internet expose votre machine à des attaques potentielles. Assurez-vous d'avoir :
- Authentification par clé activée
- Mots de passe forts
- Fail2Ban configuré
- Pare-feu correctement configuré
- Port SSH changé (optionnel)

### Configurer la redirection de port sur votre box

Pour accéder à votre serveur depuis Internet, vous devez configurer une redirection de port sur votre box/routeur :

1. Accédez à l'interface de votre box (souvent 192.168.1.1)
2. Cherchez "Redirection de ports" ou "NAT"
3. Créez une règle :
   - Port externe : 22 (ou autre)
   - Port interne : 22
   - Adresse IP : celle de votre serveur Linux Mint
   - Protocole : TCP

### Utiliser un nom de domaine dynamique (DDNS)

Comme votre adresse IP publique peut changer, utilisez un service DDNS gratuit :
- No-IP
- DuckDNS
- Dynu

Ces services vous donnent un nom de domaine (exemple : monserveur.ddns.net) qui pointe toujours vers votre IP actuelle.

---

## Dépannage courant

### Impossible de se connecter

**Vérifiez que le service fonctionne :**
```bash
sudo systemctl status ssh
```

**Vérifiez le pare-feu :**
```bash
sudo ufw status
```

SSH doit être autorisé.

**Vérifiez l'adresse IP :**
```bash
ip a
```

**Testez localement :**
```bash
ssh localhost
```

Si cela fonctionne, le problème vient du réseau.

### "Connection refused"

Le serveur SSH n'est probablement pas démarré :
```bash
sudo systemctl start ssh
```

### "Permission denied"

Vérifiez :
- Le nom d'utilisateur est correct
- Le mot de passe est correct
- L'utilisateur a le droit de se connecter (vérifiez `AllowUsers` dans la config)

### "Too many authentication failures"

Vous avez trop de clés SSH. Spécifiez la clé à utiliser :
```bash
ssh -i ~/.ssh/id_ed25519 utilisateur@serveur
```

### Le serveur est lent à répondre

Désactivez la résolution DNS inverse dans `/etc/ssh/sshd_config` :
```
UseDNS no
```

Redémarrez SSH :
```bash
sudo systemctl restart ssh
```

---

## Commandes SSH utiles

### Exécuter une commande distante

```bash
ssh utilisateur@serveur "ls -la /home"
```

### Tunnel SSH (port forwarding)

Accéder à un service distant localement :
```bash
ssh -L 8080:localhost:80 utilisateur@serveur
```

Ici, le port 80 du serveur distant sera accessible sur votre port 8080 local.

### Garder la connexion active

```bash
ssh -o ServerAliveInterval=60 utilisateur@serveur
```

Envoie un signal toutes les 60 secondes pour éviter la déconnexion.

### Se connecter en mode verbeux (debug)

```bash
ssh -v utilisateur@serveur
```

Utile pour diagnostiquer les problèmes de connexion.

---

## Ressources supplémentaires

### Documentation officielle

- Manuel OpenSSH : `man ssh` et `man sshd_config`
- Site officiel : [openssh.com](https://www.openssh.com/)

### Communauté

- Forums Linux Mint
- Stack Overflow pour les questions techniques
- Reddit : r/linuxmint, r/linux

### Bonnes pratiques

- Ne partagez JAMAIS votre clé privée SSH
- Sauvegardez vos clés SSH dans un endroit sûr
- Utilisez des phrases de passe différentes pour chaque clé
- Auditez régulièrement les connexions SSH

---

## Conclusion

SSH est un outil puissant et indispensable pour tout utilisateur Linux. Avec cette configuration de base, vous pouvez :
- Accéder à votre machine à distance en toute sécurité
- Transférer des fichiers de manière sécurisée
- Administrer des serveurs
- Créer des tunnels sécurisés

**Points clés à retenir :**
1. Installez openssh-server
2. Configurez des clés SSH pour plus de sécurité
3. Utilisez un pare-feu (UFW)
4. Protégez-vous avec Fail2Ban
5. Ne partagez jamais votre clé privée

N'oubliez pas : la sécurité est un processus continu. Restez informé des meilleures pratiques et mettez régulièrement à jour votre système !

⏭️ [Serveur web (Apache/Nginx)](/21-serveurs-et-administration-systeme/02-serveur-web.md)
