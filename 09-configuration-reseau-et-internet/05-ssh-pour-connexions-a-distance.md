🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 9.5 SSH pour connexions à distance

## Introduction

SSH (Secure Shell) est un protocole qui permet de se connecter à distance à un ordinateur de manière sécurisée. C'est comme si vous étiez assis devant la machine distante, mais depuis votre propre ordinateur, via Internet ou votre réseau local.

Imaginez que vous devez utiliser votre ordinateur de bureau depuis votre ordinateur portable, ou administrer un serveur qui se trouve dans un data center à des kilomètres de distance. SSH rend tout cela possible de manière simple et sécurisée.

Dans ce chapitre, nous allons apprendre à utiliser SSH pour contrôler des machines à distance, transférer des fichiers et sécuriser nos connexions.

## Comprendre SSH

### Qu'est-ce que SSH ?

SSH signifie "Secure Shell" (coque sécurisée). C'est un protocole qui :

**Permet l'accès à distance** :
- Vous pouvez vous connecter à un autre ordinateur
- Exécuter des commandes comme si vous étiez physiquement devant
- Gérer des serveurs sans être sur place

**Chiffre toutes les communications** :
- Vos mots de passe sont protégés
- Personne ne peut intercepter vos commandes
- Toutes les données sont sécurisées en transit

**Remplace les protocoles non sécurisés** :
- Telnet (obsolète et non sécurisé)
- RSH (non sécurisé)
- FTP (non chiffré)

### Pourquoi utiliser SSH ?

**Administration système** :
- Gérer des serveurs à distance
- Dépanner un ordinateur dans une autre pièce ou pays
- Exécuter des tâches de maintenance

**Transfert de fichiers sécurisé** :
- Copier des fichiers entre machines
- Synchroniser des données
- Sauvegardes à distance

**Développement** :
- Déployer du code sur des serveurs
- Accéder à des environnements de développement
- Éditer des fichiers à distance

**Tunnel et redirection** :
- Accéder à des services bloqués
- Sécuriser des connexions non chiffrées
- Contourner certaines restrictions réseau

### Vocabulaire SSH

**Client SSH** :
- Votre ordinateur depuis lequel vous vous connectez
- L'application que vous utilisez pour vous connecter

**Serveur SSH** :
- L'ordinateur auquel vous vous connectez
- Le service qui accepte les connexions

**Clés SSH** :
- Alternative aux mots de passe
- Plus sécurisée et pratique
- Composée d'une clé privée (à garder secrète) et d'une clé publique (à partager)

**Port SSH** :
- Par défaut : port 22
- Peut être changé pour plus de sécurité

## Installation de SSH

Linux Mint peut être utilisé comme client SSH (pour se connecter à d'autres machines) ou comme serveur SSH (pour accepter des connexions).

### Installation du client SSH

Le client SSH est généralement déjà installé sur Linux Mint. Vérifiez :

```bash
ssh -V
```

Si vous voyez une version (ex: "OpenSSH_8.9p1"), c'est installé.

Sinon, installez-le :
```bash
sudo apt update  
sudo apt install openssh-client  
```

### Installation du serveur SSH

Si vous voulez que d'autres puissent se connecter à votre machine :

```bash
sudo apt update  
sudo apt install openssh-server  
```

**Vérifier que le service fonctionne** :
```bash
sudo systemctl status ssh
```

Devrait afficher "active (running)".

**Démarrer le service SSH** :
```bash
sudo systemctl start ssh
```

**Activer au démarrage** :
```bash
sudo systemctl enable ssh
```

**Arrêter le service SSH** :
```bash
sudo systemctl stop ssh
```

**Note de sécurité** : N'activez le serveur SSH que si vous en avez vraiment besoin. Un serveur SSH mal sécurisé peut être une porte d'entrée pour les pirates.

## Première connexion SSH

### Connaître les informations nécessaires

Pour vous connecter à une machine distante, vous avez besoin de :

1. **Adresse IP ou nom d'hôte** de la machine distante
2. **Nom d'utilisateur** sur la machine distante
3. **Mot de passe** de cet utilisateur (ou clé SSH)
4. **Port SSH** (généralement 22)

### Trouver votre adresse IP

**Sur la machine à laquelle vous voulez vous connecter** :

```bash
# Voir toutes les interfaces réseau
ip addr show

# Ou plus simple
hostname -I

# Ou pour voir l'IP publique (si accès depuis Internet)
curl ifconfig.me
```

### Syntaxe de connexion de base

La commande de base est :

```bash
ssh utilisateur@adresse_ip
```

**Exemples** :

```bash
# Connexion à une machine locale
ssh jean@192.168.1.100

# Connexion à un serveur distant
ssh utilisateur@exemple.com

# Connexion sur un port personnalisé
ssh -p 2222 utilisateur@192.168.1.100
```

### Première connexion étape par étape

1. **Ouvrez un terminal**

2. **Tapez la commande de connexion** :
```bash
ssh utilisateur@192.168.1.100
```

3. **Premier message d'avertissement** :
La première fois, vous verrez :
```
The authenticity of host '192.168.1.100 (192.168.1.100)' can't be established.  
ED25519 key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxx.  
Are you sure you want to continue connecting (yes/no/[fingerprint])?  
```

Tapez `yes` et appuyez sur Entrée.

4. **Entrez le mot de passe** :
```
utilisateur@192.168.1.100's password:
```
Tapez le mot de passe (il ne s'affichera pas, c'est normal).

5. **Vous êtes connecté !**
Vous verrez le prompt de la machine distante :
```
utilisateur@machine-distante:~$
```

### Que se passe-t-il lors de la connexion ?

1. Votre client SSH contacte le serveur SSH
2. Le serveur envoie sa clé publique
3. Votre client la vérifie (d'où le message de la première connexion)
4. Une connexion chiffrée est établie
5. Vous vous authentifiez (mot de passe ou clé)
6. Vous accédez au shell de la machine distante

### Utiliser la machine distante

Une fois connecté, vous pouvez :

**Exécuter des commandes** :
```bash
# Voir où vous êtes
pwd

# Lister les fichiers
ls -la

# Voir les processus
top

# Éditer un fichier
nano fichier.txt
```

**Devenir root** (si autorisé) :
```bash
sudo su
# Ou exécuter une commande unique
sudo apt update
```

**Se déconnecter** :
```bash
exit
# Ou pressez Ctrl+D
```

## Authentification par clés SSH

Les clés SSH sont plus sécurisées et pratiques que les mots de passe. Une fois configurées, vous n'avez plus besoin de taper votre mot de passe à chaque connexion.

### Principe des clés SSH

**Clé privée** :
- Reste sur votre ordinateur (client)
- Ne doit JAMAIS être partagée
- Protégée par une phrase de passe (optionnelle mais recommandée)

**Clé publique** :
- Copiée sur les machines auxquelles vous vous connectez
- Peut être partagée sans risque
- Permet de vous identifier

**Analogie** : Imaginez un cadenas (clé publique) et sa clé (clé privée). Vous mettez des cadenas sur différentes portes, mais seule votre clé peut les ouvrir.

### Générer une paire de clés SSH

**Sur votre machine cliente** :

```bash
# Génération avec l'algorithme moderne Ed25519 (recommandé)
ssh-keygen -t ed25519 -C "votre_email@exemple.com"

# Ou avec RSA 4096 bits (plus compatible mais plus ancien)
ssh-keygen -t rsa -b 4096 -C "votre_email@exemple.com"
```

**Le processus vous demande** :

1. **Emplacement du fichier** :
```
Enter file in which to save the key (/home/votre_nom/.ssh/id_ed25519):
```
Appuyez sur Entrée pour accepter l'emplacement par défaut.

2. **Phrase de passe** :
```
Enter passphrase (empty for no passphrase):
```
Tapez une phrase de passe forte (recommandé) ou laissez vide (moins sécurisé mais plus pratique).

3. **Confirmation de la phrase de passe** :
```
Enter same passphrase again:
```

**Résultat** :
- Clé privée : `~/.ssh/id_ed25519` (ou `id_rsa`)
- Clé publique : `~/.ssh/id_ed25519.pub` (ou `id_rsa.pub`)

### Copier la clé publique sur le serveur

**Méthode 1 : Avec ssh-copy-id (la plus simple)**

```bash
ssh-copy-id utilisateur@192.168.1.100
```

Vous devrez entrer votre mot de passe une dernière fois. Ensuite, la clé sera installée.

**Méthode 2 : Manuellement**

Si `ssh-copy-id` n'est pas disponible :

```bash
# Afficher votre clé publique
cat ~/.ssh/id_ed25519.pub

# Copiez le contenu affiché
```

Ensuite, sur la machine distante :

```bash
# Connectez-vous avec mot de passe
ssh utilisateur@192.168.1.100

# Créez le dossier .ssh s'il n'existe pas
mkdir -p ~/.ssh

# Ajoutez votre clé publique
nano ~/.ssh/authorized_keys
# Collez votre clé publique, sauvegardez et quittez

# Définissez les bonnes permissions
chmod 700 ~/.ssh  
chmod 600 ~/.ssh/authorized_keys  

# Déconnectez-vous
exit
```

### Tester la connexion par clé

```bash
ssh utilisateur@192.168.1.100
```

Si vous avez défini une phrase de passe, elle vous sera demandée. Sinon, vous serez connecté directement sans mot de passe !

### Utiliser ssh-agent (éviter de retaper la phrase de passe)

Le `ssh-agent` garde votre clé en mémoire pour ne pas avoir à retaper la phrase de passe à chaque fois.

**Démarrer ssh-agent** :
```bash
eval "$(ssh-agent -s)"
```

**Ajouter votre clé** :
```bash
ssh-add ~/.ssh/id_ed25519
```

Entrez votre phrase de passe une fois. Pendant cette session, vous ne la retaperez plus.

**Voir les clés chargées** :
```bash
ssh-add -l
```

**Sur Linux Mint avec GNOME/Cinnamon**, le gestionnaire de clés `gnome-keyring` gère souvent cela automatiquement.

## Configuration SSH

Le fichier de configuration SSH permet de simplifier vos connexions et de définir des paramètres par défaut.

### Fichier de configuration client

Créez ou éditez `~/.ssh/config` :

```bash
nano ~/.ssh/config
```

**Exemple de configuration** :

```
# Serveur personnel
Host monserveur
    HostName 192.168.1.100
    User jean
    Port 22
    IdentityFile ~/.ssh/id_ed25519

# Serveur de travail
Host travail
    HostName serveur.entreprise.com
    User jdupont
    Port 2222
    IdentityFile ~/.ssh/id_rsa_travail

# VPS distant
Host vps
    HostName 203.0.113.45
    User root
    Port 22
    IdentityFile ~/.ssh/id_ed25519

# Configuration par défaut pour tous les serveurs
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
    Compression yes
```

**Avec cette configuration, vous pouvez simplement taper** :

```bash
ssh monserveur
# Au lieu de : ssh -p 22 jean@192.168.1.100 -i ~/.ssh/id_ed25519

ssh travail  
ssh vps  
```

### Options utiles dans le fichier config

**ServerAliveInterval** : Envoie un message toutes les X secondes pour maintenir la connexion
```
ServerAliveInterval 60
```

**ServerAliveCountMax** : Nombre de messages sans réponse avant déconnexion
```
ServerAliveCountMax 3
```

**Compression** : Active la compression (utile sur connexions lentes)
```
Compression yes
```

**ForwardAgent** : Transmet votre agent SSH (utile pour rebondir entre serveurs)
```
ForwardAgent yes
```

**StrictHostKeyChecking** : Contrôle de la clé d'hôte (à utiliser avec précaution)
```
StrictHostKeyChecking no  # Dangereux, évitez  
StrictHostKeyChecking ask # Par défaut  
```

### Fichier de configuration serveur

Le fichier `/etc/ssh/sshd_config` contrôle le comportement du serveur SSH.

**Éditer le fichier** :
```bash
sudo nano /etc/ssh/sshd_config
```

**Après toute modification, redémarrez le service** :
```bash
sudo systemctl restart ssh
```

Nous verrons les options de sécurité plus tard.

## Transfert de fichiers avec SSH

SSH permet de transférer des fichiers de manière sécurisée entre machines.

### SCP (Secure Copy)

SCP utilise SSH pour copier des fichiers.

**Syntaxe de base** :
```bash
scp source destination
```

#### Copier un fichier vers une machine distante

```bash
# Copier fichier.txt vers le répertoire home de l'utilisateur distant
scp fichier.txt utilisateur@192.168.1.100:~

# Copier vers un répertoire spécifique
scp fichier.txt utilisateur@192.168.1.100:/chemin/vers/destination/

# Copier avec un nom différent
scp fichier.txt utilisateur@192.168.1.100:~/nouveau_nom.txt
```

#### Copier un fichier depuis une machine distante

```bash
# Copier depuis la machine distante vers le répertoire courant
scp utilisateur@192.168.1.100:~/fichier.txt .

# Copier vers un répertoire spécifique
scp utilisateur@192.168.1.100:~/fichier.txt /home/jean/Documents/
```

#### Copier un dossier entier

Utilisez l'option `-r` (récursif) :

```bash
# Copier un dossier vers une machine distante
scp -r mon_dossier/ utilisateur@192.168.1.100:~/

# Copier depuis une machine distante
scp -r utilisateur@192.168.1.100:~/dossier_distant/ .
```

#### Options utiles de SCP

**Conserver les permissions et dates** :
```bash
scp -p fichier.txt utilisateur@192.168.1.100:~
```

**Spécifier un port** :
```bash
scp -P 2222 fichier.txt utilisateur@192.168.1.100:~
```

**Mode verbeux** (voir la progression) :
```bash
scp -v fichier.txt utilisateur@192.168.1.100:~
```

**Limiter la bande passante** (en Kbit/s) :
```bash
scp -l 1000 fichier.txt utilisateur@192.168.1.100:~
```

**Compression** (utile pour gros fichiers) :
```bash
scp -C fichier.txt utilisateur@192.168.1.100:~
```

### SFTP (SSH File Transfer Protocol)

SFTP est un protocole de transfert de fichiers interactif via SSH.

**Démarrer une session SFTP** :
```bash
sftp utilisateur@192.168.1.100
```

**Commandes SFTP** :

Une fois connecté, vous avez un prompt `sftp>`.

**Navigation** :
```bash
pwd                 # Répertoire distant actuel  
lpwd                # Répertoire local actuel  
ls                  # Lister fichiers distants  
lls                 # Lister fichiers locaux  
cd /chemin          # Changer répertoire distant  
lcd /chemin         # Changer répertoire local  
```

**Téléchargement** (distant → local) :
```bash
get fichier.txt                    # Télécharger un fichier  
get -r dossier/                    # Télécharger un dossier  
mget *.txt                         # Télécharger plusieurs fichiers  
```

**Envoi** (local → distant) :
```bash
put fichier.txt                    # Envoyer un fichier  
put -r dossier/                    # Envoyer un dossier  
mput *.txt                         # Envoyer plusieurs fichiers  
```

**Gestion de fichiers** :
```bash
mkdir nouveau_dossier              # Créer dossier distant  
rmdir ancien_dossier               # Supprimer dossier distant  
rm fichier.txt                     # Supprimer fichier distant  
rename ancien.txt nouveau.txt      # Renommer fichier distant  
```

**Quitter** :
```bash
exit
# Ou
bye
# Ou Ctrl+D
```

**Exemple de session complète** :
```bash
sftp utilisateur@192.168.1.100  
sftp> ls                          # Voir fichiers distants  
sftp> cd Documents                # Aller dans Documents  
sftp> get rapport.pdf             # Télécharger rapport.pdf  
sftp> lcd ~/Téléchargements       # Aller dans Téléchargements local  
sftp> put presentation.pptx       # Envoyer la présentation  
sftp> exit  
```

### rsync via SSH

`rsync` est un outil puissant de synchronisation de fichiers qui peut utiliser SSH.

**Avantages** :
- Transfère seulement les différences (plus rapide)
- Peut reprendre les transferts interrompus
- Nombreuses options de filtrage

**Installation** :
```bash
sudo apt install rsync
```

**Syntaxe de base** :
```bash
rsync -avz source destination
```

**Options courantes** :
- `-a` : Archive (préserve permissions, dates, etc.)
- `-v` : Verbose (affiche les détails)
- `-z` : Compression
- `-r` : Récursif
- `-h` : Human-readable (tailles lisibles)
- `--progress` : Affiche la progression
- `--delete` : Supprime les fichiers de destination qui n'existent plus dans source

**Exemples** :

```bash
# Synchroniser un dossier local vers distant
rsync -avzh --progress ~/Documents/ utilisateur@192.168.1.100:~/backup/

# Synchroniser depuis distant vers local
rsync -avzh utilisateur@192.168.1.100:~/projet/ ~/projets/

# Synchronisation avec suppression des fichiers obsolètes
rsync -avzh --delete ~/site/ utilisateur@192.168.1.100:/var/www/html/

# Exclure certains fichiers
rsync -avzh --exclude '*.log' --exclude 'cache/' ~/app/ serveur:~/app/

# Simulation (dry-run) pour voir ce qui serait transféré
rsync -avzh --dry-run ~/Documents/ utilisateur@192.168.1.100:~/backup/

# Spécifier un port SSH
rsync -avzh -e "ssh -p 2222" ~/Documents/ utilisateur@192.168.1.100:~/backup/
```

## Tunneling SSH et redirection de ports

SSH peut créer des tunnels sécurisés pour faire passer du trafic à travers une connexion chiffrée.

### Redirection de port locale (Local Port Forwarding)

Permet d'accéder à un service distant comme s'il était local.

**Syntaxe** :
```bash
ssh -L port_local:destination:port_distant utilisateur@serveur_ssh
```

**Exemple - Accéder à une base de données distante** :

```bash
# Créer un tunnel vers MySQL sur le serveur
ssh -L 3307:localhost:3306 utilisateur@192.168.1.100
```

Maintenant, en local, vous pouvez vous connecter à `localhost:3307` et cela ira vers le port 3306 du serveur distant.

**Exemple - Accéder à une interface web interne** :

```bash
# Tunnel vers une interface web qui n'écoute que sur localhost du serveur
ssh -L 8080:localhost:80 utilisateur@serveur.com
```

Ouvrez votre navigateur sur `http://localhost:8080`, vous verrez le site du serveur distant.

**Mode arrière-plan** :

Ajoutez `-f` (fork) et `-N` (pas de commande) :
```bash
ssh -f -N -L 8080:localhost:80 utilisateur@serveur.com
```

Le tunnel reste ouvert en arrière-plan.

### Redirection de port distante (Remote Port Forwarding)

Permet à la machine distante d'accéder à un service sur votre machine locale.

**Syntaxe** :
```bash
ssh -R port_distant:localhost:port_local utilisateur@serveur_ssh
```

**Exemple - Partager un serveur web local** :

```bash
# Vous avez un serveur web local sur le port 8000
# Vous voulez le rendre accessible depuis le serveur distant
ssh -R 9000:localhost:8000 utilisateur@serveur.com
```

Sur le serveur distant, `localhost:9000` accédera à votre serveur local sur le port 8000.

**Cas d'usage** :
- Démontrer une application en développement
- Contourner un pare-feu NAT
- Créer un tunnel inversé

### Redirection de port dynamique (SOCKS Proxy)

Crée un proxy SOCKS qui route tout le trafic via SSH.

**Syntaxe** :
```bash
ssh -D port_local utilisateur@serveur_ssh
```

**Exemple** :

```bash
ssh -D 8080 utilisateur@serveur.com
```

Configurez ensuite votre navigateur pour utiliser le proxy SOCKS :
- Proxy SOCKS5 : `localhost`
- Port : `8080`

Tout le trafic du navigateur passera par le serveur SSH, chiffré et depuis l'IP du serveur.

**Cas d'usage** :
- Contourner la censure
- Sécuriser votre navigation sur WiFi public
- Accéder à des ressources géo-restreintes

### Garder les tunnels ouverts

Pour que les tunnels ne se ferment pas :

**Option 1 : Dans ~/.ssh/config**
```
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
```

**Option 2 : Dans la commande**
```bash
ssh -o ServerAliveInterval=60 -L 8080:localhost:80 utilisateur@serveur.com
```

**Option 3 : Utiliser autossh** (maintient automatiquement la connexion)
```bash
sudo apt install autossh  
autossh -M 0 -f -N -L 8080:localhost:80 utilisateur@serveur.com  
```

## Sécurisation de SSH

Un serveur SSH mal sécurisé est une cible facile pour les pirates. Voici comment le protéger.

### Changer le port SSH

Le port 22 est le port par défaut, donc constamment scanné par les bots.

**Modifier le port** :

```bash
sudo nano /etc/ssh/sshd_config
```

Trouvez la ligne :
```
#Port 22
```

Décommentez et changez :
```
Port 2222
```

**Redémarrez SSH** :
```bash
sudo systemctl restart ssh
```

**Mettez à jour le pare-feu** :
```bash
sudo ufw allow 2222/tcp  
sudo ufw delete allow 22/tcp  # Si vous ne voulez plus le port 22  
```

**Connexion avec le nouveau port** :
```bash
ssh -p 2222 utilisateur@serveur.com
```

### Désactiver l'accès root

Ne permettez jamais à root de se connecter directement par SSH.

```bash
sudo nano /etc/ssh/sshd_config
```

Trouvez et modifiez :
```
PermitRootLogin no
```

**Redémarrez SSH** :
```bash
sudo systemctl restart ssh
```

Utilisez plutôt un utilisateur normal avec `sudo`.

### Autoriser seulement l'authentification par clés

Désactivez l'authentification par mot de passe (après avoir configuré les clés !) :

```bash
sudo nano /etc/ssh/sshd_config
```

Modifiez :
```
PasswordAuthentication no  
PubkeyAuthentication yes  
ChallengeResponseAuthentication no  
```

**Redémarrez SSH** :
```bash
sudo systemctl restart ssh
```

**ATTENTION** : Assurez-vous d'avoir une clé SSH fonctionnelle avant de faire cela, sinon vous serez bloqué !

### Limiter les utilisateurs autorisés

Autoriser seulement certains utilisateurs :

```bash
sudo nano /etc/ssh/sshd_config
```

Ajoutez à la fin :
```
AllowUsers jean paul marie
```

Ou autoriser un groupe :
```
AllowGroups ssh-users
```

Puis ajoutez les utilisateurs au groupe :
```bash
sudo groupadd ssh-users  
sudo usermod -aG ssh-users jean  
```

### Limiter les tentatives de connexion avec fail2ban

Fail2ban bannit automatiquement les IP qui échouent à se connecter plusieurs fois.

**Installation** :
```bash
sudo apt install fail2ban
```

**Configuration** :
```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local  
sudo nano /etc/fail2ban/jail.local  
```

Trouvez la section `[sshd]` et configurez :
```
[sshd]
enabled = true  
port = ssh  
filter = sshd  
logpath = /var/log/auth.log  
maxretry = 3  
bantime = 3600  
findtime = 600  
```

**Explication** :
- `maxretry = 3` : 3 tentatives échouées
- `findtime = 600` : dans une période de 10 minutes
- `bantime = 3600` : bannissement pour 1 heure

**Démarrer fail2ban** :
```bash
sudo systemctl start fail2ban  
sudo systemctl enable fail2ban  
```

**Voir les IP bannies** :
```bash
sudo fail2ban-client status sshd
```

**Débannir une IP** :
```bash
sudo fail2ban-client set sshd unbanip 203.0.113.45
```

### Autres options de sécurité

**Désactiver le transfert X11** (si vous ne l'utilisez pas) :
```
X11Forwarding no
```

**Limiter le nombre de connexions simultanées** :
```
MaxSessions 3
```

**Timeout d'inactivité** :
```
ClientAliveInterval 300  
ClientAliveCountMax 2  
```

Déconnecte après 10 minutes (300 sec × 2) d'inactivité.

**Utiliser seulement les protocoles SSH 2** :
```
Protocol 2
```

**Bannière d'avertissement** :
```
Banner /etc/ssh/banner.txt
```

Créez `/etc/ssh/banner.txt` avec un message d'avertissement légal.

### Configuration sécurisée complète

Voici un exemple de `/etc/ssh/sshd_config` sécurisé :

```
# Port et écoute
Port 2222  
AddressFamily inet  
ListenAddress 0.0.0.0  

# Protocole et sécurité
Protocol 2  
HostKey /etc/ssh/ssh_host_ed25519_key  
HostKey /etc/ssh/ssh_host_rsa_key  

# Authentification
PermitRootLogin no  
PubkeyAuthentication yes  
PasswordAuthentication no  
PermitEmptyPasswords no  
ChallengeResponseAuthentication no  
UsePAM yes  

# Utilisateurs autorisés
AllowUsers jean paul

# Options de connexion
X11Forwarding no  
PrintMotd no  
AcceptEnv LANG LC_*  
MaxAuthTries 3  
MaxSessions 3  
LoginGraceTime 60  

# Keep-alive
ClientAliveInterval 300  
ClientAliveCountMax 2  

# Logging
SyslogFacility AUTH  
LogLevel VERBOSE  

# Sous-système SFTP
Subsystem sftp /usr/lib/openssh/sftp-server
```

**Après toute modification** :
```bash
# Vérifier la configuration
sudo sshd -t

# Si OK, redémarrer
sudo systemctl restart ssh
```

## Utilisation avancée de SSH

### Exécuter une commande à distance

Vous n'avez pas besoin d'ouvrir une session interactive pour exécuter une commande.

**Syntaxe** :
```bash
ssh utilisateur@serveur 'commande'
```

**Exemples** :

```bash
# Voir l'espace disque
ssh utilisateur@serveur 'df -h'

# Redémarrer un service
ssh utilisateur@serveur 'sudo systemctl restart apache2'

# Plusieurs commandes
ssh utilisateur@serveur 'cd /var/log && ls -lh && tail -n 20 syslog'

# Sauvegarder la sortie localement
ssh utilisateur@serveur 'cat /var/log/app.log' > log_local.txt
```

### Monter un système de fichiers distant (SSHFS)

SSHFS permet de monter un dossier distant comme s'il était local.

**Installation** :
```bash
sudo apt install sshfs
```

**Monter un dossier distant** :
```bash
# Créer un point de montage
mkdir ~/serveur-distant

# Monter
sshfs utilisateur@192.168.1.100:/chemin/distant ~/serveur-distant

# Ou avec des options
sshfs utilisateur@192.168.1.100:/home/utilisateur ~/serveur-distant -o reconnect,ServerAliveInterval=15
```

**Utiliser le dossier** :
Vous pouvez maintenant utiliser `~/serveur-distant` comme un dossier normal !

**Démonter** :
```bash
fusermount -u ~/serveur-distant
```

**Montage automatique au démarrage** (ajoutez à `/etc/fstab`) :
```
utilisateur@192.168.1.100:/home/utilisateur /home/jean/serveur-distant fuse.sshfs delay_connect,_netdev,user,idmap=user,transform_symlinks,reconnect 0 0
```

### Agent Forwarding

Permet d'utiliser vos clés SSH locales sur une machine distante pour se connecter à une troisième machine.

**Exemple** :
Votre PC → Serveur A → Serveur B

Sans agent forwarding, vous devriez copier votre clé privée sur le Serveur A (dangereux !).

**Activer** :

Dans `~/.ssh/config` :
```
Host serveur-a
    HostName 192.168.1.100
    User utilisateur
    ForwardAgent yes
```

Ou en ligne de commande :
```bash
ssh -A utilisateur@serveur-a
```

Une fois sur serveur-a, vous pouvez SSH vers serveur-b sans mot de passe :
```bash
# Sur serveur-a
ssh utilisateur@serveur-b
```

**Attention** : N'activez l'agent forwarding que sur des machines de confiance.

### Jump Hosts (ProxyJump)

Pour accéder à une machine via un serveur intermédiaire.

**Scénario** : Vous voulez accéder au Serveur B mais il n'est accessible que depuis le Serveur A.

**Méthode 1 : Option -J**
```bash
ssh -J utilisateur@serveur-a utilisateur@serveur-b
```

**Méthode 2 : Dans ~/.ssh/config**
```
Host serveur-b
    HostName 10.0.0.50
    User utilisateur
    ProxyJump utilisateur@serveur-a
```

Puis simplement :
```bash
ssh serveur-b
```

**Avec plusieurs sauts** :
```bash
ssh -J user1@jump1,user2@jump2 user3@destination
```

### X11 Forwarding (applications graphiques)

Permet d'exécuter des applications graphiques distantes et les afficher localement.

**Sur le serveur** (`/etc/ssh/sshd_config`) :
```
X11Forwarding yes
```

**Connexion avec X11** :
```bash
ssh -X utilisateur@serveur

# Ou avec compression (plus rapide)
ssh -XC utilisateur@serveur
```

**Lancer une application** :
```bash
# Une fois connecté
firefox &  
gedit &  
```

L'application s'affiche sur votre écran local mais s'exécute sur le serveur.

**Trusted X11 Forwarding** (moins sécurisé mais moins de restrictions) :
```bash
ssh -Y utilisateur@serveur
```

## Résolution des problèmes courants

### Impossible de se connecter

**Erreur : "Connection refused"**

**Causes et solutions** :

1. **Le service SSH n'est pas démarré sur le serveur**
```bash
# Sur le serveur
sudo systemctl status ssh  
sudo systemctl start ssh  
```

2. **Mauvaise adresse IP ou nom d'hôte**
```bash
# Vérifier l'IP sur le serveur
hostname -I
```

3. **Pare-feu bloque le port**
```bash
# Sur le serveur
sudo ufw allow 22/tcp
# Ou si port personnalisé
sudo ufw allow 2222/tcp
```

4. **Mauvais port**
```bash
# Si le serveur utilise un port personnalisé
ssh -p 2222 utilisateur@serveur
```

**Erreur : "Connection timed out"**

- Le serveur n'est pas accessible (réseau, pare-feu, serveur éteint)
- Vérifiez la connectivité : `ping adresse_serveur`

**Erreur : "Permission denied"**

- Mauvais nom d'utilisateur ou mot de passe
- L'utilisateur n'est pas autorisé (vérifier `AllowUsers` dans sshd_config)
- Problème avec les clés SSH

### Problèmes avec les clés SSH

**"Permission denied (publickey)"**

1. **Vérifier que la clé publique est sur le serveur** :
```bash
# Sur le serveur
cat ~/.ssh/authorized_keys
# Votre clé publique doit être présente
```

2. **Vérifier les permissions** :
```bash
# Sur le serveur
chmod 700 ~/.ssh  
chmod 600 ~/.ssh/authorized_keys  

# Sur le client
chmod 700 ~/.ssh  
chmod 600 ~/.ssh/id_ed25519  
```

3. **Utiliser la bonne clé** :
```bash
# Spécifier explicitement la clé
ssh -i ~/.ssh/id_ed25519 utilisateur@serveur
```

4. **Vérifier les logs** :
```bash
# Sur le serveur
sudo tail -f /var/log/auth.log
```

### Avertissement "Remote Host Identification Has Changed"

**Message complet** :
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
```

**Cause** : La clé du serveur a changé (réinstallation, attaque man-in-the-middle).

**Si vous êtes sûr que c'est normal** (ex: réinstallation) :

```bash
# Supprimer l'ancienne clé
ssh-keygen -R 192.168.1.100

# Ou éditer manuellement
nano ~/.ssh/known_hosts
# Supprimez la ligne concernant ce serveur
```

**Si vous n'êtes pas sûr** : Ne vous connectez pas ! Cela pourrait être une attaque.

### Connexion trop lente

**Causes et solutions** :

1. **Désactiver la résolution DNS inverse** :

Sur le serveur (`/etc/ssh/sshd_config`) :
```
UseDNS no
```

2. **Désactiver GSSAPI** :

Sur le client (`~/.ssh/config` ou `/etc/ssh/ssh_config`) :
```
Host *
    GSSAPIAuthentication no
```

3. **Utiliser la compression** :
```bash
ssh -C utilisateur@serveur
```

### Connexion qui se coupe

**Solutions** :

1. **Keep-alive côté client** :

Dans `~/.ssh/config` :
```
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
```

2. **Keep-alive côté serveur** :

Dans `/etc/ssh/sshd_config` :
```
ClientAliveInterval 60  
ClientAliveCountMax 3  
```

3. **Désactiver la gestion d'énergie WiFi** :
```bash
sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
```
Changez `wifi.powersave = 3` en `wifi.powersave = 2`

### Impossible de transférer des fichiers

**Problème de permissions** :

```bash
# Assurez-vous que le dossier de destination existe et est accessible
ssh utilisateur@serveur 'mkdir -p ~/destination && chmod 755 ~/destination'
```

**SFTP ne fonctionne pas** :

Vérifiez que le sous-système SFTP est activé dans `/etc/ssh/sshd_config` :
```
Subsystem sftp /usr/lib/openssh/sftp-server
```

## Bonnes pratiques SSH

### Organisation des clés

**Plusieurs clés pour différents usages** :

```
~/.ssh/
├── id_ed25519          # Clé personnelle principale
├── id_ed25519.pub
├── id_rsa_travail      # Clé pour le travail
├── id_rsa_travail.pub
├── id_ed25519_github   # Clé spécifique pour GitHub
├── id_ed25519_github.pub
├── config              # Configuration
└── authorized_keys     # Clés autorisées (si serveur)
```

**Dans ~/.ssh/config** :
```
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_github

Host *.travail.com
    User jdupont
    IdentityFile ~/.ssh/id_rsa_travail
```

### Sauvegarder vos clés SSH

**Sauvegardez vos clés privées** dans un endroit sûr :
- Clé USB chiffrée
- Gestionnaire de mots de passe
- Coffre-fort numérique

**Ne jamais** :
- Les envoyer par email
- Les mettre sur un cloud non chiffré
- Les inclure dans un dépôt Git
- Les copier sur des machines publiques

### Rotation des clés

Changez vos clés SSH régulièrement (au moins une fois par an) :

1. Générez une nouvelle paire de clés
2. Ajoutez la nouvelle clé publique sur tous vos serveurs
3. Testez la nouvelle clé
4. Supprimez l'ancienne clé publique des serveurs
5. Supprimez l'ancienne clé privée

### Surveiller les connexions SSH

**Voir qui est connecté** :
```bash
who  
w  
```

**Voir l'historique des connexions** :
```bash
last  
lastlog  
```

**Surveiller les tentatives échouées** :
```bash
sudo grep "Failed password" /var/log/auth.log  
sudo grep "Invalid user" /var/log/auth.log  
```

**Voir les connexions actives en temps réel** :
```bash
sudo tail -f /var/log/auth.log | grep sshd
```

### Documenter vos configurations

Gardez une trace de :
- Quels serveurs vous gérez
- Quelles clés vous utilisez pour quoi
- Les ports personnalisés utilisés
- Les configurations spéciales

Exemple de fichier documentation :

```
# Serveurs SSH
serveur-web.com:2222 - Serveur web de production
  Utilisateur: deployer
  Clé: ~/.ssh/id_ed25519_production

192.168.1.100:22 - Serveur local
  Utilisateur: jean
  Clé: ~/.ssh/id_ed25519
```

## Scripts et automatisation

### Script de backup automatique via SSH

```bash
#!/bin/bash
# backup-ssh.sh

SERVER="utilisateur@192.168.1.100"  
SOURCE="/var/www/html"  
DEST="~/backups/serveur-web-$(date +%Y%m%d)"  

echo "Démarrage du backup depuis $SERVER..."  
rsync -avzh --progress "$SERVER:$SOURCE" "$DEST"  

if [ $? -eq 0 ]; then
    echo "Backup terminé avec succès dans $DEST"
else
    echo "Erreur lors du backup"
    exit 1
fi
```

Rendez-le exécutable :
```bash
chmod +x backup-ssh.sh
```

Automatisez avec cron :
```bash
crontab -e
```

Ajoutez :
```
0 2 * * * /home/jean/scripts/backup-ssh.sh >> /home/jean/logs/backup.log 2>&1
```

### Script de monitoring de serveurs

```bash
#!/bin/bash
# check-servers.sh

SERVERS=(
    "utilisateur@serveur1.com"
    "utilisateur@serveur2.com"
    "utilisateur@192.168.1.100"
)

for server in "${SERVERS[@]}"; do
    echo "Vérification de $server..."

    # Test de connexion
    if ssh -o ConnectTimeout=5 "$server" 'exit' 2>/dev/null; then
        echo "✓ $server est accessible"

        # Vérifier l'uptime
        uptime=$(ssh "$server" 'uptime -p')
        echo "  Uptime: $uptime"

        # Vérifier l'espace disque
        disk=$(ssh "$server" "df -h / | tail -1 | awk '{print \$5}'")
        echo "  Utilisation disque: $disk"
    else
        echo "✗ $server est inaccessible"
    fi
    echo ""
done
```

### Déploiement automatisé

```bash
#!/bin/bash
# deploy.sh

SERVER="deployer@production.com"  
APP_DIR="/var/www/mon-app"  

echo "Déploiement sur $SERVER..."

# Git pull sur le serveur
ssh "$SERVER" "cd $APP_DIR && git pull origin main"

# Installer les dépendances
ssh "$SERVER" "cd $APP_DIR && npm install"

# Redémarrer l'application
ssh "$SERVER" "sudo systemctl restart mon-app"

echo "Déploiement terminé !"
```

## Outils graphiques pour SSH

Si vous préférez une interface graphique :

### Remmina (client complet)

```bash
sudo apt install remmina remmina-plugin-ssh
```

Remmina supporte SSH, VNC, RDP et plus.

### PuTTY (si vous connaissez Windows)

```bash
sudo apt install putty
```

### FileZilla (pour SFTP)

```bash
sudo apt install filezilla
```

Interface graphique pour transferts SFTP.

### PAC Manager (gestionnaire de connexions)

```bash
sudo apt install pac
```

Gestionnaire de connexions SSH avec interface graphique.

## Résumé des commandes essentielles

```bash
# Connexion de base
ssh utilisateur@serveur  
ssh -p 2222 utilisateur@serveur              # Port personnalisé  

# Génération de clés
ssh-keygen -t ed25519 -C "email@exemple.com"  
ssh-copy-id utilisateur@serveur  

# Transfert de fichiers
scp fichier.txt utilisateur@serveur:~/  
scp -r dossier/ utilisateur@serveur:~/  
sftp utilisateur@serveur  
rsync -avzh local/ utilisateur@serveur:distant/  

# Tunneling
ssh -L 8080:localhost:80 utilisateur@serveur  # Local forwarding  
ssh -R 9000:localhost:8000 utilisateur@serveur # Remote forwarding  
ssh -D 8080 utilisateur@serveur              # SOCKS proxy  

# Exécution de commandes
ssh utilisateur@serveur 'commande'

# Gestion du service SSH
sudo systemctl status ssh  
sudo systemctl start ssh  
sudo systemctl stop ssh  
sudo systemctl restart ssh  

# Surveillance
who                                          # Qui est connecté  
last                                         # Historique de connexions  
sudo tail -f /var/log/auth.log              # Logs en temps réel  

# Configuration
nano ~/.ssh/config                           # Config client  
sudo nano /etc/ssh/sshd_config              # Config serveur  
sudo sshd -t                                 # Vérifier config serveur  
```

---

**Points clés à retenir** :
- SSH permet de contrôler à distance des machines de manière sécurisée et chiffrée
- L'authentification par clés est plus sécurisée et pratique que les mots de passe
- Le fichier `~/.ssh/config` simplifie grandement les connexions fréquentes
- SCP, SFTP et rsync permettent le transfert sécurisé de fichiers
- SSH peut créer des tunnels pour sécuriser d'autres connexions
- Un serveur SSH doit être sécurisé : changer le port, désactiver root, utiliser fail2ban
- Les clés privées ne doivent JAMAIS être partagées ou copiées n'importe où
- Toujours vérifier les permissions (700 pour .ssh/, 600 pour les clés)
- SSH est l'outil indispensable pour l'administration système et le développement
- Testez toujours votre configuration avant de fermer votre session actuelle !

⏭️ [Partage de fichiers (Samba, NFS)](/09-configuration-reseau-et-internet/06-partage-de-fichiers.md)
