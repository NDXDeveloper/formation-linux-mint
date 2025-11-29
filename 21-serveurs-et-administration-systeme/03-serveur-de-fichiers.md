🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 21.3 Serveur de fichiers (Samba, FTP)

## Introduction

### Qu'est-ce qu'un serveur de fichiers ?

Un serveur de fichiers est un ordinateur configuré pour partager des fichiers et dossiers avec d'autres appareils sur un réseau. Au lieu d'envoyer des fichiers par email ou par clé USB, vous pouvez les rendre accessibles directement depuis votre réseau local ou Internet.

**Imaginez :** Un disque dur partagé accessible depuis tous vos appareils (PC, smartphone, tablette) où que vous soyez dans votre maison ou bureau.

### Pourquoi créer un serveur de fichiers ?

- **Centralisation** : Tous vos fichiers au même endroit
- **Sauvegarde** : Un point central pour sauvegarder vos données
- **Partage familial** : Photos, vidéos, documents accessibles à tous
- **Travail collaboratif** : Plusieurs personnes travaillent sur les mêmes fichiers
- **Streaming** : Accéder à votre musique et vidéos depuis n'importe quel appareil
- **Alternative au cloud** : Votre propre "Dropbox" à la maison

### Samba vs FTP : Quelle différence ?

#### Samba (SMB/CIFS)
- **Protocole de partage Windows** compatible Linux
- Apparaît comme un dossier réseau dans l'explorateur de fichiers
- Idéal pour réseaux locaux (maison, bureau)
- Facile d'utilisation, comme un disque dur externe
- Fonctionne avec Windows, macOS, Linux, Android, iOS

**Cas d'usage :** Partager des fichiers sur votre réseau domestique, accéder à vos documents depuis n'importe quel PC de la maison.

#### FTP (File Transfer Protocol)
- Protocole dédié au transfert de fichiers
- Nécessite un client FTP (FileZilla, WinSCP)
- Peut être accessible depuis Internet facilement
- Moins intégré au système que Samba
- Versions sécurisées : SFTP (SSH) et FTPS (SSL/TLS)

**Cas d'usage :** Héberger un site web, partager des fichiers avec des personnes externes, accès distant depuis Internet.

### Lequel choisir ?

**Utilisez Samba si :**
- Vous partagez sur réseau local uniquement
- Vous voulez une expérience "plug and play"
- Vous avez des utilisateurs Windows

**Utilisez FTP si :**
- Vous voulez un accès depuis Internet
- Vous avez besoin de contrôle granulaire des permissions
- Vous transférez de gros fichiers régulièrement

**Bonne nouvelle :** Vous pouvez installer les deux !

---

## Partie 1 : Samba - Serveur de fichiers réseau

### Installation de Samba

Ouvrez un terminal et installez Samba :

```bash
sudo apt update
sudo apt install samba samba-common-bin
```

Vérifiez que Samba est installé :

```bash
smbd --version
```

### Créer un dossier à partager

Créons un dossier que nous allons partager :

```bash
mkdir ~/Partage
```

Vous pouvez aussi partager un disque dur externe ou n'importe quel dossier existant.

### Configuration de base de Samba

Le fichier de configuration principal est `/etc/samba/smb.conf`.

#### Sauvegarder la configuration d'origine

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
```

#### Éditer la configuration

```bash
sudo nano /etc/samba/smb.conf
```

Allez à la fin du fichier et ajoutez votre partage :

```ini
[Partage]
   comment = Dossier de partage familial
   path = /home/votre_nom_utilisateur/Partage
   browseable = yes
   read only = no
   guest ok = no
   valid users = votre_nom_utilisateur
```

**Remplacez** `votre_nom_utilisateur` par votre vrai nom d'utilisateur Linux.

**Explications :**
- `[Partage]` : Nom du partage visible sur le réseau
- `comment` : Description du partage
- `path` : Chemin du dossier à partager
- `browseable = yes` : Visible dans l'explorateur réseau
- `read only = no` : Permet l'écriture (modifier, créer, supprimer)
- `guest ok = no` : Nécessite une authentification
- `valid users` : Utilisateurs autorisés

Sauvegardez avec `Ctrl+O`, quittez avec `Ctrl+X`.

### Créer un mot de passe Samba

Samba utilise ses propres mots de passe, séparés de Linux :

```bash
sudo smbpasswd -a votre_nom_utilisateur
```

Entrez un mot de passe (peut être différent de votre mot de passe Linux).

### Redémarrer Samba

```bash
sudo systemctl restart smbd
sudo systemctl restart nmbd
```

Activez Samba au démarrage :

```bash
sudo systemctl enable smbd
sudo systemctl enable nmbd
```

### Configurer le pare-feu

Autorisez Samba dans le pare-feu :

```bash
sudo ufw allow Samba
```

### Accéder au partage depuis différents systèmes

#### Depuis Windows

1. Ouvrez l'Explorateur de fichiers
2. Dans la barre d'adresse, tapez :
   ```
   \\adresse_ip_du_serveur\Partage
   ```
   Exemple : `\\192.168.1.100\Partage`

3. Entrez votre nom d'utilisateur et mot de passe Samba

**Astuce :** Pour trouver l'IP de votre serveur Linux :
```bash
hostname -I
```

**Mapper en tant que lecteur réseau :**
- Clic droit sur "Ce PC" → "Connecter un lecteur réseau"
- Choisissez une lettre (ex: Z:)
- Entrez le chemin : `\\192.168.1.100\Partage`
- Cochez "Se reconnecter à l'ouverture de session"

#### Depuis Linux Mint

1. Ouvrez le gestionnaire de fichiers (Nemo)
2. Dans la barre latérale, cliquez sur "Réseau"
3. Vous devriez voir votre serveur
4. Double-cliquez et entrez vos identifiants

**Alternative - Connexion manuelle :**
- Appuyez sur `Ctrl+L` dans Nemo
- Tapez : `smb://192.168.1.100/Partage`
- Entrez vos identifiants

#### Depuis macOS

1. Dans le Finder, appuyez sur `Cmd+K`
2. Entrez : `smb://192.168.1.100/Partage`
3. Cliquez sur "Se connecter"
4. Entrez vos identifiants

#### Depuis Android

Utilisez une application comme :
- **Cx File Explorer**
- **Solid Explorer**
- **ES File Explorer**

Dans l'application :
1. Ajoutez un réseau → Samba/SMB
2. Adresse : `192.168.1.100`
3. Nom du partage : `Partage`
4. Entrez vos identifiants

#### Depuis iOS

Utilisez l'application **Fichiers** intégrée :
1. Ouvrez Fichiers
2. Appuyez sur "..." → "Se connecter à un serveur"
3. Entrez : `smb://192.168.1.100`
4. Authentifiez-vous

### Créer plusieurs partages

Vous pouvez créer autant de partages que vous voulez. Dans `/etc/samba/smb.conf` :

```ini
[Documents]
   comment = Documents de travail
   path = /home/user/Documents
   browseable = yes
   read only = no
   valid users = user1, user2

[Photos]
   comment = Photos de famille
   path = /home/user/Photos
   browseable = yes
   read only = yes
   guest ok = yes

[Backup]
   comment = Sauvegardes
   path = /mnt/backup
   browseable = no
   read only = no
   valid users = admin
```

### Partage avec plusieurs utilisateurs

#### Créer des utilisateurs Samba

```bash
sudo smbpasswd -a utilisateur2
sudo smbpasswd -a utilisateur3
```

#### Créer un groupe

```bash
sudo groupadd partage
sudo usermod -aG partage utilisateur1
sudo usermod -aG partage utilisateur2
```

#### Configurer le partage pour un groupe

```ini
[PartageGroupe]
   path = /home/partage_commun
   valid users = @partage
   force group = partage
   create mask = 0770
   directory mask = 0770
```

N'oubliez pas de créer le dossier et d'ajuster les permissions :

```bash
sudo mkdir /home/partage_commun
sudo chgrp partage /home/partage_commun
sudo chmod 770 /home/partage_commun
```

### Partage en lecture seule

Pour un partage accessible à tous mais modifiable par personne :

```ini
[Lecture]
   path = /home/user/Public
   browseable = yes
   read only = yes
   guest ok = yes
```

### Partage public sans authentification

**Attention :** Seulement sur un réseau de confiance !

```ini
[Public]
   path = /home/user/Public
   browseable = yes
   read only = no
   guest ok = yes
   create mask = 0777
   directory mask = 0777
```

---

## Partie 2 : FTP - Serveur de transfert de fichiers

### Choisir un serveur FTP

Plusieurs options existent :

- **vsftpd** : Very Secure FTP Daemon (recommandé, simple et sécurisé)
- **ProFTPD** : Très flexible, configuration Apache-like
- **Pure-FTPd** : Simple et performant

Nous utiliserons **vsftpd** pour ce tutoriel.

### Installation de vsftpd

```bash
sudo apt update
sudo apt install vsftpd
```

### Configuration de base

#### Sauvegarder la configuration d'origine

```bash
sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.backup
```

#### Éditer la configuration

```bash
sudo nano /etc/vsftpd.conf
```

Modifiez ou ajoutez ces lignes :

```ini
# Désactiver les connexions anonymes
anonymous_enable=NO

# Autoriser les utilisateurs locaux
local_enable=YES

# Autoriser l'écriture
write_enable=YES

# Confiner les utilisateurs dans leur dossier home
chroot_local_user=YES

# Autoriser la liste d'écriture
allow_writeable_chroot=YES

# Message de bienvenue
ftpd_banner=Bienvenue sur mon serveur FTP

# Port FTP passif (important pour les pare-feu)
pasv_enable=YES
pasv_min_port=40000
pasv_max_port=40100

# Logs
xferlog_enable=YES
xferlog_file=/var/log/vsftpd.log

# Sécurité : liste d'utilisateurs autorisés
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO
```

Sauvegardez et quittez.

### Créer la liste des utilisateurs autorisés

```bash
sudo nano /etc/vsftpd.userlist
```

Ajoutez les noms d'utilisateurs, un par ligne :

```
utilisateur1
utilisateur2
```

Ces utilisateurs doivent être des utilisateurs Linux existants.

### Créer un utilisateur FTP dédié

Pour plus de sécurité, créez un utilisateur spécifique au FTP :

```bash
sudo adduser ftpuser
```

Entrez un mot de passe sécurisé.

Ajoutez-le à la liste :

```bash
echo "ftpuser" | sudo tee -a /etc/vsftpd.userlist
```

### Redémarrer vsftpd

```bash
sudo systemctl restart vsftpd
sudo systemctl enable vsftpd
```

### Configurer le pare-feu

Autorisez FTP :

```bash
sudo ufw allow 20/tcp
sudo ufw allow 21/tcp
sudo ufw allow 40000:40100/tcp
```

**Explication :**
- Port 21 : Commandes FTP
- Port 20 : Données FTP
- Ports 40000-40100 : Mode passif

### Tester la connexion FTP

#### En ligne de commande (depuis Linux)

```bash
ftp localhost
```

Entrez votre nom d'utilisateur et mot de passe. Si ça fonctionne :

```
ftp> ls
ftp> bye
```

#### Avec un client graphique

Téléchargez et installez **FileZilla** :

```bash
sudo apt install filezilla
```

Lancez FileZilla et connectez-vous :
- Hôte : `ftp://192.168.1.100` (votre IP)
- Utilisateur : votre nom d'utilisateur
- Mot de passe : votre mot de passe
- Port : 21

### Créer un dossier de partage FTP

Créez un dossier pour FTP :

```bash
mkdir ~/ftp_partage
```

Ajustez les permissions :

```bash
chmod 755 ~/ftp_partage
```

---

## Sécuriser FTP avec SSL/TLS (FTPS)

FTP standard transmet les mots de passe en clair. FTPS ajoute le chiffrement.

### Créer un certificat SSL

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/vsftpd.key \
  -out /etc/ssl/certs/vsftpd.crt
```

Répondez aux questions (vous pouvez laisser par défaut en appuyant sur Entrée).

### Configurer vsftpd pour SSL

Éditez `/etc/vsftpd.conf` :

```bash
sudo nano /etc/vsftpd.conf
```

Ajoutez à la fin :

```ini
# Activer SSL
rsa_cert_file=/etc/ssl/certs/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key
ssl_enable=YES

# Forcer SSL pour les connexions
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES

# Protocoles SSL
ssl_tlsv1=YES
ssl_sslv2=NO
ssl_sslv3=NO

# Exiger SSL
require_ssl_reuse=NO
ssl_ciphers=HIGH
```

Redémarrez :

```bash
sudo systemctl restart vsftpd
```

### Se connecter avec FTPS

Dans FileZilla :
- Hôte : `ftps://192.168.1.100`
- Port : 21
- Acceptez le certificat

---

## Alternative moderne : SFTP (SSH File Transfer Protocol)

SFTP utilise SSH, donc si vous avez SSH installé (voir chapitre 21.1), SFTP fonctionne automatiquement !

### Avantages de SFTP

- **Plus sécurisé** : Utilise SSH (déjà chiffré)
- **Un seul port** : Port 22 uniquement
- **Pas de configuration supplémentaire** : Si SSH fonctionne, SFTP fonctionne
- **Traversée de pare-feu** : Plus simple qu'FTP

### Se connecter avec SFTP

#### En ligne de commande

```bash
sftp utilisateur@192.168.1.100
```

Commandes :
```
sftp> ls              # Lister fichiers distants
sftp> cd dossier      # Changer de dossier
sftp> get fichier     # Télécharger
sftp> put fichier     # Envoyer
sftp> mkdir nouveau   # Créer dossier
sftp> bye             # Quitter
```

#### Avec FileZilla

- Hôte : `sftp://192.168.1.100`
- Utilisateur : votre utilisateur Linux
- Mot de passe : votre mot de passe Linux
- Port : 22

**Avantage :** Pas besoin de configuration supplémentaire !

---

## Accès depuis Internet

### Attention aux risques !

Exposer un serveur de fichiers à Internet comporte des risques :
- Tentatives d'intrusion
- Consommation de bande passante
- Failles de sécurité potentielles

**Recommandations :**
- Utilisez des mots de passe très forts
- Activez SSL/TLS (FTPS) ou utilisez SFTP
- Limitez les utilisateurs autorisés
- Surveillez les logs régulièrement
- Considérez un VPN au lieu d'ouvrir FTP/Samba

### Redirection de port sur votre box

Pour que le serveur soit accessible depuis Internet :

1. Accédez à l'interface de votre box (192.168.1.1 souvent)
2. Trouvez "Redirection de ports" ou "NAT"
3. Créez une règle :

**Pour FTP :**
- Port externe : 21
- Port interne : 21
- IP locale : 192.168.1.100 (votre serveur)
- Protocole : TCP

**Pour SFTP :**
- Port externe : 22
- Port interne : 22
- IP locale : 192.168.1.100
- Protocole : TCP

### Trouver votre IP publique

```bash
curl ifconfig.me
```

ou visitez [https://www.mon-ip.com/](https://www.mon-ip.com/)

### Utiliser un nom de domaine dynamique (DDNS)

Votre IP publique change régulièrement. Utilisez un service DDNS gratuit :

- **No-IP** : [noip.com](https://www.noip.com)
- **DuckDNS** : [duckdns.org](https://www.duckdns.org)
- **Dynu** : [dynu.com](https://www.dynu.com)

Exemple d'utilisation avec DuckDNS :

1. Créez un compte sur duckdns.org
2. Créez un sous-domaine : `monserveur.duckdns.org`
3. Installez le client :

```bash
mkdir ~/duckdns
cd ~/duckdns
```

Créez un script :

```bash
nano duck.sh
```

Ajoutez :

```bash
#!/bin/bash
echo url="https://www.duckdns.org/update?domains=monserveur&token=VOTRE_TOKEN&ip=" | curl -k -o ~/duckdns/duck.log -K -
```

Remplacez `monserveur` et `VOTRE_TOKEN` par vos vraies valeurs.

Rendez-le exécutable :

```bash
chmod 700 duck.sh
```

Ajoutez à crontab pour mise à jour automatique :

```bash
crontab -e
```

Ajoutez :

```
*/5 * * * * ~/duckdns/duck.sh >/dev/null 2>&1
```

Maintenant, `monserveur.duckdns.org` pointera toujours vers votre serveur !

---

## Gestion et surveillance

### Voir les connexions actives Samba

```bash
sudo smbstatus
```

### Voir les connexions FTP

```bash
sudo lsof -i :21
```

### Consulter les logs Samba

```bash
sudo tail -f /var/log/samba/log.smbd
```

### Consulter les logs FTP

```bash
sudo tail -f /var/log/vsftpd.log
```

### Limiter la bande passante FTP

Dans `/etc/vsftpd.conf` :

```ini
# Limiter à 1 MB/s (1000000 bytes)
local_max_rate=1000000
```

### Limiter le nombre de connexions

```ini
max_clients=10
max_per_ip=2
```

---

## Sauvegarder automatiquement vers le serveur

### Avec rsync (Linux)

Créez un script de sauvegarde :

```bash
nano ~/sauvegarde.sh
```

Ajoutez :

```bash
#!/bin/bash
rsync -avz --delete ~/Documents/ utilisateur@192.168.1.100:/home/utilisateur/Backup/Documents/
```

Rendez-le exécutable :

```bash
chmod +x ~/sauvegarde.sh
```

Automatisez avec cron :

```bash
crontab -e
```

Ajoutez (sauvegarde quotidienne à 2h du matin) :

```
0 2 * * * /home/user/sauvegarde.sh
```

### Avec un client FTP automatisé

Installez lftp :

```bash
sudo apt install lftp
```

Script de sauvegarde :

```bash
nano ~/ftp_backup.sh
```

```bash
#!/bin/bash
lftp -u utilisateur,motdepasse ftp://192.168.1.100 <<EOF
mirror -R ~/Documents /Backup/Documents
bye
EOF
```

---

## Dépannage courant

### Samba : "Accès refusé"

Vérifiez les permissions :

```bash
ls -la ~/Partage
sudo chmod 755 ~/Partage
```

Vérifiez les utilisateurs Samba :

```bash
sudo pdbedit -L
```

### Samba : Serveur invisible sur le réseau

Redémarrez les services :

```bash
sudo systemctl restart smbd nmbd
```

Vérifiez le pare-feu :

```bash
sudo ufw status
```

### FTP : "Connection refused"

Vérifiez que vsftpd fonctionne :

```bash
sudo systemctl status vsftpd
```

Vérifiez le port :

```bash
sudo netstat -tulpn | grep :21
```

### FTP : "530 Login incorrect"

Vérifiez que l'utilisateur est dans `/etc/vsftpd.userlist` :

```bash
cat /etc/vsftpd.userlist
```

### FTP : Mode passif ne fonctionne pas

Vérifiez les ports passifs dans `/etc/vsftpd.conf` :

```ini
pasv_enable=YES
pasv_min_port=40000
pasv_max_port=40100
```

Et dans le pare-feu :

```bash
sudo ufw allow 40000:40100/tcp
```

### SFTP : Permission refusée

Vérifiez les permissions SSH :

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### Samba : Performances lentes

Ajoutez dans `/etc/samba/smb.conf` :

```ini
[global]
   socket options = TCP_NODELAY IPTOS_LOWDELAY SO_RCVBUF=65536 SO_SNDBUF=65536
   read raw = yes
   write raw = yes
   min receivefile size = 16384
   use sendfile = true
   aio read size = 16384
   aio write size = 16384
```

---

## Solutions cloud alternatives

Si gérer un serveur de fichiers vous semble trop complexe, considérez ces alternatives :

### Nextcloud (auto-hébergé)

- Interface web moderne type Dropbox
- Applications mobiles
- Calendrier, contacts, notes intégrés
- Voir chapitre 10.2 pour l'installation

### Syncthing

- Synchronisation peer-to-peer
- Pas de serveur central nécessaire
- Chiffrement de bout en bout
- Voir chapitre 10.5

### Services cloud commerciaux

- Google Drive
- Dropbox
- OneDrive
- pCloud

---

## Comparaison récapitulative

| Critère | Samba | FTP | SFTP |
|---------|-------|-----|------|
| **Facilité d'utilisation** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Sécurité** | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Performances réseau local** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Accès Internet** | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Configuration** | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Compatibilité** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |

### Recommandations finales

**Pour un réseau domestique :**
→ Utilisez Samba (simple, intégré, performant)

**Pour un accès distant sécurisé :**
→ Utilisez SFTP (sécurisé, simple, pas de config supplémentaire)

**Pour partager avec des personnes externes :**
→ Utilisez FTP avec SSL (FTPS) ou considérez Nextcloud

**Pour le maximum de sécurité :**
→ Utilisez un VPN + Samba, ou SFTP uniquement

---

## Commandes de référence rapide

### Samba
```bash
sudo systemctl start smbd nmbd      # Démarrer
sudo systemctl stop smbd nmbd       # Arrêter
sudo systemctl restart smbd nmbd    # Redémarrer
sudo smbpasswd -a utilisateur       # Ajouter utilisateur
sudo smbstatus                      # Voir connexions
testparm                            # Tester configuration
```

### vsftpd
```bash
sudo systemctl start vsftpd         # Démarrer
sudo systemctl stop vsftpd          # Arrêter
sudo systemctl restart vsftpd       # Redémarrer
sudo tail -f /var/log/vsftpd.log    # Voir logs
```

### SFTP
```bash
sftp utilisateur@serveur            # Se connecter
sftp> get fichier                   # Télécharger
sftp> put fichier                   # Envoyer
sftp> ls                            # Lister
```

---

## Ressources supplémentaires

### Documentation officielle
- Samba : [samba.org/samba/docs/](https://www.samba.org/samba/docs/)
- vsftpd : [security.appspot.com/vsftpd.html](https://security.appspot.com/vsftpd.html)

### Outils recommandés
- **FileZilla** : Client FTP/SFTP graphique
- **WinSCP** : Client Windows pour SFTP/SCP
- **Cyberduck** : Client macOS
- **Nautilus** : Gestionnaire de fichiers Linux avec support Samba/FTP

### Communautés
- Forums Linux Mint
- Ubuntu Forums (beaucoup de ressources Samba/FTP)
- Stack Exchange - Server Fault

---

## Conclusion

Vous savez maintenant configurer un serveur de fichiers complet sur Linux Mint !

**Points clés à retenir :**
1. **Samba** est idéal pour les réseaux locaux
2. **FTP** est pratique pour l'accès Internet mais nécessite SSL
3. **SFTP** est le plus sécurisé et le plus simple
4. La sécurité est primordiale : mots de passe forts, chiffrement, pare-feu
5. Les logs sont vos amis pour le dépannage

**Prochaines étapes :**
- Testez Samba sur votre réseau local
- Configurez des sauvegardes automatiques
- Explorez Nextcloud pour une solution cloud personnelle
- Sécurisez vos serveurs avant de les exposer à Internet

N'oubliez pas : un serveur de fichiers accessible depuis Internet doit être correctement sécurisé. En cas de doute, utilisez un VPN ou limitez l'accès au réseau local uniquement !

⏭️ [Serveur média (Plex, Jellyfin)](/21-serveurs-et-administration-systeme/04-serveur-media.md)
