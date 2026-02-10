🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 9.7 Bureau à distance (VNC, RDP)

## Introduction

Le bureau à distance permet de contrôler un ordinateur à distance comme si vous étiez physiquement devant lui. Vous voyez l'écran de l'ordinateur distant, pouvez utiliser la souris et le clavier, et exécuter des applications, tout cela depuis votre propre machine.

C'est particulièrement utile pour :
- Accéder à votre ordinateur de bureau depuis votre portable
- Aider quelqu'un à distance (support technique familial)
- Administrer des serveurs
- Travailler depuis chez soi
- Accéder à des applications installées sur une autre machine

Dans ce chapitre, nous allons découvrir les deux protocoles principaux de bureau à distance : **VNC** (Virtual Network Computing) et **RDP** (Remote Desktop Protocol).

## Comprendre les protocoles de bureau à distance

### VNC (Virtual Network Computing)

**Qu'est-ce que VNC ?**

VNC est un système open source qui permet de voir et contrôler un bureau à distance. Il fonctionne en transmettant les événements clavier/souris et en renvoyant les mises à jour de l'écran.

**Avantages** :
- Multi-plateforme (Linux, Windows, Mac)
- Open source avec plusieurs implémentations
- Peut partager une session existante
- Fonctionne sur tous les environnements de bureau
- Léger en ressources

**Inconvénients** :
- Généralement plus lent que RDP
- Qualité d'image variable selon la bande passante
- Configuration de la sécurité nécessaire (par défaut non chiffré)
- Performances dépendantes de la résolution d'écran

**Variantes de VNC** :
- **TightVNC** : Optimisé pour les connexions lentes
- **TigerVNC** : Moderne et performant
- **RealVNC** : Version commerciale avec fonctionnalités avancées
- **x11vnc** : Partage la session X11 existante
- **Vino** : Serveur VNC GNOME simple

### RDP (Remote Desktop Protocol)

**Qu'est-ce que RDP ?**

RDP est le protocole de bureau à distance développé par Microsoft. Sous Linux, nous utilisons **xrdp**, une implémentation open source de RDP.

**Avantages** :
- Excellent pour se connecter depuis Windows
- Généralement plus rapide que VNC
- Meilleure gestion de la bande passante
- Supporte le son, l'impression, le partage de presse-papier
- Redirection de dossiers

**Inconvénients** :
- Crée toujours une nouvelle session (ne partage pas la session console)
- Configuration parfois plus complexe
- Moins de flexibilité que VNC
- Peut avoir des problèmes avec certains environnements de bureau

### VNC vs RDP : Quelle différence ?

| Critère | VNC | RDP |
|---------|-----|-----|
| **Compatibilité** | Universel | Optimal pour Windows |
| **Performance** | Moyenne | Excellente |
| **Partage de session** | Oui (selon implémentation) | Non (nouvelle session) |
| **Sécurité par défaut** | Basique | Meilleure |
| **Qualité audio** | Limitée | Bonne |
| **Configuration** | Simple | Moyenne |
| **Usage typique** | Support technique, démo | Travail à distance |

### Quelle solution choisir ?

**Utilisez VNC si** :
- Vous voulez voir/partager la session active de l'utilisateur
- Vous devez supporter plusieurs plateformes
- Vous faites du support technique à distance
- Vous voulez une solution simple et rapide

**Utilisez RDP si** :
- Vous vous connectez principalement depuis Windows
- Vous avez besoin de performances optimales
- Vous voulez le son et le partage de fichiers
- Vous créez des sessions de travail dédiées

**Dans la pratique** : Beaucoup d'administrateurs installent les deux et choisissent selon les besoins du moment.

## Installation et configuration de VNC

Nous allons utiliser **TigerVNC**, une implémentation moderne et performante de VNC.

### Installation du serveur VNC

```bash
# Installer TigerVNC serveur
sudo apt update  
sudo apt install tigervnc-standalone-server tigervnc-common  
```

**Alternative : x11vnc** (pour partager la session active) :
```bash
sudo apt install x11vnc
```

### Configuration initiale de TigerVNC

#### Première configuration

```bash
# Configurer le mot de passe VNC
vncpasswd
```

Vous serez invité à :
1. Entrer un mot de passe (8 caractères maximum)
2. Le confirmer
3. Optionnellement définir un mot de passe "view-only" (lecture seule)

Le mot de passe est stocké dans `~/.vnc/passwd`.

#### Créer le fichier de démarrage

Créez ou éditez `~/.vnc/xstartup` :

```bash
nano ~/.vnc/xstartup
```

**Pour Cinnamon** :
```bash
#!/bin/sh
unset SESSION_MANAGER  
unset DBUS_SESSION_BUS_ADDRESS  
exec cinnamon-session  
```

**Pour MATE** :
```bash
#!/bin/sh
unset SESSION_MANAGER  
unset DBUS_SESSION_BUS_ADDRESS  
exec mate-session  
```

**Pour Xfce** :
```bash
#!/bin/sh
unset SESSION_MANAGER  
unset DBUS_SESSION_BUS_ADDRESS  
exec startxfce4  
```

Rendez le fichier exécutable :
```bash
chmod +x ~/.vnc/xstartup
```

#### Démarrer le serveur VNC

```bash
# Démarrer VNC sur le display :1 avec résolution 1920x1080
vncserver :1 -geometry 1920x1080 -depth 24
```

**Explications** :
- `:1` : Numéro de display (correspond au port 5901)
- `-geometry 1920x1080` : Résolution de l'écran virtuel
- `-depth 24` : Profondeur de couleur (24 bits = 16 millions de couleurs)

**Autres résolutions courantes** :
- `1366x768` : Laptop standard
- `1920x1080` : Full HD
- `2560x1440` : QHD
- `1024x768` : Petite fenêtre

#### Arrêter le serveur VNC

```bash
# Arrêter le display :1
vncserver -kill :1
```

#### Lister les sessions VNC actives

```bash
vncserver -list
```

### Configuration de x11vnc (partage de session active)

Si vous préférez partager votre session actuelle plutôt que créer une nouvelle :

**Installation** :
```bash
sudo apt install x11vnc
```

**Définir un mot de passe** :
```bash
x11vnc -storepasswd
```

**Démarrer x11vnc** :
```bash
# Basique
x11vnc -display :0 -auth guess

# Avec mot de passe
x11vnc -display :0 -auth guess -usepw

# Avec mot de passe et en arrière-plan
x11vnc -display :0 -auth guess -usepw -forever -bg
```

**Options utiles** :
- `-display :0` : Partager le display principal
- `-auth guess` : Détecter automatiquement l'authentification X
- `-usepw` : Utiliser le mot de passe défini
- `-forever` : Ne pas quitter après la première connexion
- `-bg` : Exécuter en arrière-plan
- `-ncache 10` : Cache pour améliorer les performances
- `-rfbport 5900` : Port d'écoute (par défaut 5900)

### Démarrage automatique de VNC

#### Méthode 1 : Service systemd (TigerVNC)

Créez un fichier de service :

```bash
sudo nano /etc/systemd/system/vncserver@.service
```

Contenu :
```ini
[Unit]
Description=Remote desktop service (VNC)  
After=syslog.target network.target  

[Service]
Type=simple  
User=votre_nom_utilisateur  
PAMName=login  
PIDFile=/home/votre_nom_utilisateur/.vnc/%H%i.pid  
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill :%i > /dev/null 2>&1 || :'  
ExecStart=/usr/bin/vncserver :%i -geometry 1920x1080 -depth 24  
ExecStop=/usr/bin/vncserver -kill :%i  

[Install]
WantedBy=multi-user.target
```

**Remplacez** `votre_nom_utilisateur` par votre nom d'utilisateur réel.

**Activer et démarrer** :
```bash
# Recharger systemd
sudo systemctl daemon-reload

# Activer pour le display :1
sudo systemctl enable vncserver@1.service

# Démarrer
sudo systemctl start vncserver@1.service

# Vérifier
sudo systemctl status vncserver@1.service
```

#### Méthode 2 : Application de démarrage (x11vnc)

1. Ouvrez le **Menu** → **Préférences** → **Applications au démarrage**
2. Cliquez sur **"Ajouter"**
3. **Nom** : VNC Server
4. **Commande** : `x11vnc -display :0 -auth guess -usepw -forever -bg -ncache 10`
5. **Commentaire** : Serveur VNC au démarrage
6. Cliquez sur **"Ajouter"**

### Installation du client VNC

Pour vous connecter à un serveur VNC depuis Linux Mint :

```bash
# Remmina (client universel recommandé)
sudo apt install remmina remmina-plugin-vnc

# Ou TigerVNC viewer
sudo apt install tigervnc-viewer

# Ou RealVNC viewer (télécharger depuis realvnc.com)
```

### Se connecter à un serveur VNC

#### Avec Remmina (interface graphique)

1. Lancez **Remmina** depuis le menu
2. Cliquez sur **"Nouvelle connexion"** (icône +)
3. **Protocole** : VNC
4. **Serveur** : `adresse_ip:5901` (ou `:1` sera ajouté automatiquement)
5. **Nom d'utilisateur** : (vide pour VNC standard)
6. **Mot de passe** : Le mot de passe VNC
7. **Qualité** : Choisissez selon votre connexion
8. Cliquez sur **"Enregistrer et connecter"**

#### Avec vncviewer (ligne de commande)

```bash
# Connexion basique
vncviewer 192.168.1.100:1

# Ou avec le port complet
vncviewer 192.168.1.100:5901

# Plein écran
vncviewer -FullScreen 192.168.1.100:1

# Qualité réduite pour connexion lente
vncviewer -LowColorLevel 1 192.168.1.100:1
```

#### Depuis Windows

1. Téléchargez **TightVNC Viewer** ou **RealVNC Viewer**
2. Installez-le
3. Lancez-le
4. Entrez : `adresse_ip:5901`
5. Cliquez sur "Connect"
6. Entrez le mot de passe VNC

#### Depuis macOS

1. Utilisez le **Finder** → **Aller** → **Se connecter au serveur**
2. Entrez : `vnc://adresse_ip:5901`
3. Cliquez sur "Se connecter"
4. Entrez le mot de passe VNC

#### Depuis Android/iOS

Installez une application VNC depuis le store :
- **VNC Viewer** (RealVNC) : Gratuit, excellent
- **bVNC** (Android)
- **Jump Desktop** (iOS/Android)

Configuration : Adresse IP, port 5901, mot de passe.

## Installation et configuration de RDP

RDP permet de créer des sessions de bureau dédiées, idéal pour le travail à distance.

### Installation de xrdp

```bash
sudo apt update  
sudo apt install xrdp  
```

**Vérifier l'installation** :
```bash
sudo systemctl status xrdp
```

Le service devrait être "active (running)".

### Configuration de base de xrdp

#### Fichier de configuration principal

Le fichier principal est `/etc/xrdp/xrdp.ini`.

```bash
sudo nano /etc/xrdp/xrdp.ini
```

**Paramètres importants** :

```ini
[Globals]
; Port d'écoute (3389 par défaut)
port=3389

; Niveau de sécurité
security_layer=negotiate  
crypt_level=high  

; Autoriser compression
bulk_compression=true

; Résolution maximale
max_bpp=32
```

**Ne modifiez généralement pas ce fichier** sauf pour des besoins spécifiques.

#### Configuration de la session

Créez ou éditez `~/.xsession` :

```bash
nano ~/.xsession
```

**Pour Cinnamon** :
```bash
#!/bin/sh
cinnamon-session
```

**Pour MATE** :
```bash
#!/bin/sh
mate-session
```

**Pour Xfce** :
```bash
#!/bin/sh
startxfce4
```

Rendez-le exécutable :
```bash
chmod +x ~/.xsession
```

#### Autoriser les connexions

Par défaut, xrdp devrait fonctionner immédiatement après installation.

**Redémarrer le service** :
```bash
sudo systemctl restart xrdp
```

**Activer au démarrage** :
```bash
sudo systemctl enable xrdp
```

### Résoudre le problème d'écran noir avec xrdp

Un problème courant est un écran noir lors de la connexion RDP.

**Solution 1 : Configuration Polkit**

Créez un fichier polkit :

```bash
sudo nano /etc/polkit-1/localauthority/50-local.d/45-allow-colord.pkla
```

Contenu :
```ini
[Allow Colord all Users]
Identity=unix-user:*  
Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.delete-profile;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile  
ResultAny=no  
ResultInactive=no  
ResultActive=yes  
```

**Solution 2 : Désactiver screensaver/écran de verrouillage**

```bash
# Pour Cinnamon
gsettings set org.cinnamon.desktop.screensaver lock-enabled false

# Pour MATE
gsettings set org.mate.screensaver lock-enabled false
```

**Solution 3 : Script de démarrage**

Créez `/etc/xrdp/startwm.sh` (si non existant ou modifiez-le) :

```bash
sudo nano /etc/xrdp/startwm.sh
```

Ajoutez en haut (après le shebang) :
```bash
#!/bin/sh
unset DBUS_SESSION_BUS_ADDRESS  
unset XDG_RUNTIME_DIR  
```

### Se connecter via RDP

#### Depuis Linux avec Remmina

1. Lancez **Remmina**
2. Nouvelle connexion (icône +)
3. **Protocole** : RDP
4. **Serveur** : `192.168.1.100` (pas besoin de port, 3389 par défaut)
5. **Nom d'utilisateur** : Votre nom d'utilisateur Linux
6. **Mot de passe** : Votre mot de passe Linux
7. **Résolution** : Choisissez selon vos préférences
8. **Qualité** : Selon votre connexion
9. Cliquez sur **"Enregistrer et connecter"**

#### Depuis Windows

1. Ouvrez **Connexion Bureau à distance** (mstsc.exe)
   - Recherchez "Bureau à distance" dans le menu Démarrer
2. **Ordinateur** : `192.168.1.100`
3. **Nom d'utilisateur** : `votre_nom_utilisateur`
4. Cliquez sur **"Se connecter"**
5. Entrez votre mot de passe Linux
6. Acceptez le certificat si demandé

**Options avancées** :
- Onglet "Affichage" : Résolution et couleurs
- Onglet "Ressources locales" : Son, presse-papier, imprimantes
- Onglet "Programmes" : Lancer une application au démarrage
- Onglet "Expérience" : Optimisations réseau

#### Depuis macOS

1. Téléchargez **Microsoft Remote Desktop** depuis l'App Store
2. Lancez l'application
3. Cliquez sur **"Add PC"**
4. **PC name** : `192.168.1.100`
5. **User account** : Ajoutez votre nom d'utilisateur et mot de passe
6. Cliquez sur **"Add"**
7. Double-cliquez sur la connexion pour vous connecter

#### Depuis Android/iOS

Installez **Microsoft Remote Desktop** depuis le store :
1. Lancez l'application
2. Appuyez sur **"+"** pour ajouter un PC
3. **PC name** : `192.168.1.100`
4. **User account** : Vos identifiants Linux
5. Sauvegardez et connectez

## Configuration pare-feu

Pour que VNC et RDP fonctionnent, vous devez ouvrir les ports correspondants dans le pare-feu.

### Ports utilisés

**VNC** :
- Port 5900 : Display :0
- Port 5901 : Display :1
- Port 5902 : Display :2
- Et ainsi de suite...

**RDP** :
- Port 3389 : Port standard RDP

### Configuration UFW

```bash
# VNC - Display :1
sudo ufw allow 5901/tcp

# VNC - Display :0 (x11vnc)
sudo ufw allow 5900/tcp

# RDP
sudo ufw allow 3389/tcp

# Ou limiter à votre réseau local (recommandé)
sudo ufw allow from 192.168.1.0/24 to any port 5901 proto tcp  
sudo ufw allow from 192.168.1.0/24 to any port 3389 proto tcp  

# Vérifier
sudo ufw status
```

## Sécurité du bureau à distance

Le bureau à distance expose votre système, la sécurité est primordiale.

### Sécurité VNC

#### 1. Utiliser un mot de passe fort

```bash
# Définir un mot de passe fort (8 caractères max pour VNC)
vncpasswd
```

Utilisez un mot de passe complexe malgré la limitation.

#### 2. Tunneling SSH

La meilleure sécurité : faire passer VNC à travers un tunnel SSH.

**Sur le client** :
```bash
# Créer le tunnel SSH
ssh -L 5901:localhost:5901 utilisateur@serveur-distant

# Dans une autre fenêtre, se connecter via VNC en local
vncviewer localhost:1
```

Tout le trafic VNC passe maintenant par SSH chiffré !

**Avec Remmina** :
1. Nouvelle connexion RDP/VNC
2. Onglet "SSH"
3. Cochez "Activer le tunnel SSH"
4. Renseignez les infos SSH
5. Le tunnel sera créé automatiquement

#### 3. Limiter les IP autorisées

```bash
# Dans le pare-feu
sudo ufw delete allow 5901/tcp  
sudo ufw allow from 192.168.1.0/24 to any port 5901 proto tcp  
```

#### 4. Utiliser VeNCrypt ou TLS

Pour TigerVNC avec chiffrement :

```bash
# Générer un certificat
openssl req -x509 -nodes -newkey rsa:2048 -keyout ~/.vnc/server.key -out ~/.vnc/server.crt -days 365

# Démarrer VNC avec TLS
vncserver :1 -SecurityTypes VeNCrypt,TLSVnc -X509Key ~/.vnc/server.key -X509Cert ~/.vnc/server.crt
```

#### 5. Désactiver VNC quand non utilisé

```bash
# Arrêter le serveur VNC
vncserver -kill :1

# Ou arrêter le service
sudo systemctl stop vncserver@1.service
```

### Sécurité RDP

#### 1. Utiliser des mots de passe forts

Le mot de passe RDP est votre mot de passe Linux utilisateur. Assurez-vous qu'il est fort.

```bash
# Changer votre mot de passe
passwd
```

#### 2. Activer le chiffrement

Dans `/etc/xrdp/xrdp.ini` :

```ini
security_layer=negotiate  
crypt_level=high  
```

Redémarrez :
```bash
sudo systemctl restart xrdp
```

#### 3. Changer le port par défaut

Dans `/etc/xrdp/xrdp.ini` :

```ini
port=13389  # Au lieu de 3389
```

Puis :
```bash
sudo systemctl restart xrdp  
sudo ufw allow 13389/tcp  
sudo ufw delete allow 3389/tcp  
```

#### 4. Limiter les tentatives avec fail2ban

```bash
# Installer fail2ban
sudo apt install fail2ban

# Créer la configuration pour xrdp
sudo nano /etc/fail2ban/jail.d/xrdp.conf
```

Contenu :
```ini
[xrdp]
enabled = true  
port = 3389  
filter = xrdp  
logpath = /var/log/xrdp.log  
maxretry = 3  
bantime = 3600  
findtime = 600  
```

Créer le filtre :
```bash
sudo nano /etc/fail2ban/filter.d/xrdp.conf
```

Contenu :
```ini
[Definition]
failregex = ^\[\d+\]: \[ERROR\] security_check: .*failed from <HOST>
            ^\[\d+\]: \[ERROR\] PAM: .*authentication failure.*rhost=<HOST>
ignoreregex =
```

Redémarrer :
```bash
sudo systemctl restart fail2ban
```

#### 5. Tunnel SSH pour RDP

Comme pour VNC :

```bash
# Créer le tunnel
ssh -L 3389:localhost:3389 utilisateur@serveur-distant

# Se connecter via RDP en local
remmina  # Ou mstsc sur Windows, avec localhost
```

### Bonnes pratiques générales

#### 1. Utiliser un VPN

Pour accéder depuis Internet, utilisez un VPN plutôt que d'exposer directement VNC/RDP.

#### 2. Surveiller les connexions

```bash
# Voir qui est connecté
who  
w  

# Logs VNC
tail -f ~/.vnc/*.log

# Logs RDP
sudo tail -f /var/log/xrdp.log  
sudo tail -f /var/log/xrdp-sesman.log  
```

#### 3. Désactiver quand non nécessaire

```bash
# Désactiver VNC
sudo systemctl stop vncserver@1.service  
sudo systemctl disable vncserver@1.service  

# Désactiver RDP
sudo systemctl stop xrdp  
sudo systemctl disable xrdp  
```

#### 4. Mettre à jour régulièrement

```bash
sudo apt update  
sudo apt upgrade  
```

#### 5. Sessions avec timeout

Pour VNC, configurez un timeout d'inactivité si disponible dans votre implémentation.

## Optimisation des performances

### Optimiser VNC

#### Réduire la qualité pour connexions lentes

```bash
# Démarrer avec qualité réduite
vncserver :1 -geometry 1366x768 -depth 16

# Options TigerVNC pour compression
vncserver :1 -CompareFB 0 -ZlibLevel 9
```

#### Client VNC avec optimisations

```bash
# Vncviewer avec compression
vncviewer -LowColorLevel 2 -CompressLevel 9 192.168.1.100:1
```

#### Désactiver les effets visuels

Dans Cinnamon :
1. Paramètres → Effets
2. Désactivez les effets ou mettez-les au minimum
3. Désactivez les animations

### Optimiser RDP

#### Dans xrdp.ini

```ini
[Globals]
bulk_compression=true  
max_bpp=24  # Au lieu de 32 si performances faibles  
```

#### Côté client Windows

1. Options avancées de Connexion Bureau à distance
2. Onglet "Expérience"
3. Sélectionnez "Modem (56 kbps)" pour connexion lente
4. Décochez :
   - Arrière-plan du bureau
   - Composition du bureau
   - Affichage du contenu de la fenêtre lors du déplacement
   - Animations de menu et de fenêtres

### Résolution adaptative

**Pour VNC** :
Certains clients comme Remmina ajustent automatiquement la résolution.

**Pour RDP** :
La résolution s'adapte généralement à la taille de la fenêtre client.

## Résolution des problèmes courants

### Problèmes VNC

#### Impossible de se connecter

**Solutions** :

1. **Vérifier que le serveur fonctionne** :
```bash
vncserver -list
# Ou pour x11vnc
ps aux | grep x11vnc
```

2. **Vérifier le pare-feu** :
```bash
sudo ufw status  
sudo ufw allow 5901/tcp  
```

3. **Tester la connexion** :
```bash
# Test du port
telnet 192.168.1.100 5901
# Ou
nc -zv 192.168.1.100 5901
```

4. **Vérifier les logs** :
```bash
cat ~/.vnc/*.log
```

#### Écran gris ou vide

**Solutions** :

1. **Vérifier ~/.vnc/xstartup** :
```bash
cat ~/.vnc/xstartup
# Doit contenir les bonnes commandes pour votre environnement
```

2. **Permissions** :
```bash
chmod +x ~/.vnc/xstartup
```

3. **Relancer le serveur** :
```bash
vncserver -kill :1  
vncserver :1 -geometry 1920x1080 -depth 24  
```

4. **Vérifier les logs** :
```bash
tail -f ~/.vnc/*.log
```

#### Performances très lentes

**Solutions** :

1. **Réduire résolution et profondeur** :
```bash
vncserver -kill :1  
vncserver :1 -geometry 1366x768 -depth 16  
```

2. **Activer compression côté client** :
```bash
vncviewer -CompressLevel 9 -QualityLevel 5 192.168.1.100:1
```

3. **Désactiver effets visuels** sur la session distante

#### Erreur "Too many security failures"

VNC bloque après plusieurs échecs de mot de passe.

**Solution** :
```bash
# Arrêter et redémarrer VNC
vncserver -kill :1  
vncserver :1  
```

### Problèmes RDP

#### Écran noir après connexion

**Solutions** :

1. **Configuration Polkit** (voir section configuration xrdp ci-dessus)

2. **Vérifier ~/.xsession** :
```bash
cat ~/.xsession  
chmod +x ~/.xsession  
```

3. **Vérifier les logs** :
```bash
sudo tail -f /var/log/xrdp-sesman.log
```

4. **Recréer la configuration** :
```bash
rm ~/.xsession  
nano ~/.xsession  
# Ajouter : cinnamon-session (ou mate-session, etc.)
chmod +x ~/.xsession
```

#### Impossible de se connecter

**Solutions** :

1. **Vérifier que xrdp fonctionne** :
```bash
sudo systemctl status xrdp  
sudo systemctl restart xrdp  
```

2. **Vérifier le port** :
```bash
sudo netstat -tlnp | grep 3389
# Ou
sudo ss -tlnp | grep 3389
```

3. **Pare-feu** :
```bash
sudo ufw allow 3389/tcp
```

4. **Logs** :
```bash
sudo tail -f /var/log/xrdp.log  
sudo tail -f /var/log/xrdp-sesman.log  
```

#### Déconnexion automatique

**Causes possibles** :
- Conflit avec session console active
- Problème de permissions

**Solutions** :

1. **Ne pas être connecté localement** pendant la connexion RDP

2. **Vérifier dans xrdp.ini** :
```ini
[xrdp1]
name=sesman-Xvnc
# Pas de kill_disconnected
```

#### Clavier non fonctionnel ou layout incorrect

**Solutions** :

1. **Configurer le layout clavier** :
```bash
sudo nano /etc/xrdp/xrdp_keyboard.ini
```

2. **Ou installer xrdp-pulseaudio** :
```bash
sudo apt install xrdp-pulseaudio
```

3. **Redémarrer** :
```bash
sudo systemctl restart xrdp
```

#### Pas de son

**Solution** :

```bash
# Installer le module audio
sudo apt install pulseaudio-module-xrdp

# Redémarrer
sudo systemctl restart xrdp
```

Dans la session RDP, le son devrait maintenant fonctionner.

## Alternatives et outils complémentaires

### TeamViewer

Application propriétaire très populaire pour le support à distance.

**Avantages** :
- Très facile à utiliser
- Fonctionne derrière NAT sans configuration
- Support commercial disponible
- Transfert de fichiers intégré

**Installation** :
1. Téléchargez depuis teamviewer.com
2. Installez le .deb
3. Lancez TeamViewer
4. Communiquez votre ID et mot de passe à la personne qui se connecte

### AnyDesk

Alternative à TeamViewer, également propriétaire.

**Installation** :
```bash
wget https://download.anydesk.com/linux/anydesk_6.3.0-1_amd64.deb  
sudo dpkg -i anydesk_6.3.0-1_amd64.deb  
sudo apt install -f  
```

### NoMachine

Solution propriétaire basée sur NX, très performante.

**Avantages** :
- Excellentes performances
- Gratuit pour usage personnel
- Qualité vidéo et audio
- Transfert de fichiers

**Installation** :
Téléchargez depuis nomachine.com

### Chrome Remote Desktop

Extension Google Chrome pour accès à distance.

**Avantages** :
- Basé sur navigateur
- Facile à configurer
- Fonctionne via Internet sans configuration réseau

**Installation** :
1. Installez l'extension Chrome Remote Desktop
2. Suivez les instructions
3. Accédez via remotedesktop.google.com

### Rustdesk

Alternative open source à TeamViewer.

**Avantages** :
- Open source
- Auto-hébergeable
- Fonctionne derrière NAT

**Installation** :
```bash
# Téléchargez depuis rustdesk.com
wget https://github.com/rustdesk/rustdesk/releases/download/1.2.3/rustdesk-1.2.3-x86_64.deb  
sudo dpkg -i rustdesk-1.2.3-x86_64.deb  
```

### Comparaison rapide

| Solution | Type | Performances | Facilité | Coût |
|----------|------|--------------|----------|------|
| VNC | Open | Moyenne | Moyenne | Gratuit |
| RDP | Open | Bonne | Moyenne | Gratuit |
| TeamViewer | Propriétaire | Excellente | Très facile | Gratuit personnel |
| AnyDesk | Propriétaire | Excellente | Facile | Gratuit personnel |
| NoMachine | Propriétaire | Excellente | Facile | Gratuit personnel |
| Chrome RD | Cloud | Bonne | Très facile | Gratuit |
| RustDesk | Open | Bonne | Facile | Gratuit |

## Cas d'usage pratiques

### Support technique familial

**Scénario** : Aider vos parents à distance.

**Solution recommandée** : TeamViewer ou AnyDesk
- Très simple pour l'utilisateur distant
- Pas de configuration réseau nécessaire
- Vision de ce qu'ils voient

**Alternative** : x11vnc avec tunnel SSH
- Plus technique mais gratuit et open source
- Nécessite configuration initiale

### Travail à distance régulier

**Scénario** : Accéder quotidiennement à votre PC de bureau depuis chez vous.

**Solution recommandée** : RDP via VPN
- Performances excellentes
- Session dédiée
- Son et partage de fichiers

**Configuration** :
1. Configurez un VPN (voir chapitre 9.4)
2. Installez xrdp sur le PC bureau
3. Connectez-vous au VPN depuis chez vous
4. Utilisez RDP pour accéder au bureau

### Administration de serveurs

**Scénario** : Gérer plusieurs serveurs Linux.

**Solution recommandée** : VNC avec tunnel SSH
- Sécurisé
- Accès GUI quand nécessaire
- Combiné avec SSH pour ligne de commande

**Alternative** : SSH uniquement (sans GUI)
- Plus léger et rapide
- Suffisant pour la plupart des tâches serveur

### Présentation/démonstration

**Scénario** : Montrer votre écran à un groupe.

**Solution recommandée** : x11vnc
- Partage votre session actuelle
- Tout le monde voit la même chose
- Peut être en lecture seule

**Configuration** :
```bash
# Démarrer en lecture seule
x11vnc -display :0 -auth guess -viewonly -shared -forever
```

### Accès depuis l'extérieur (Internet)

**Scénario** : Accéder à votre PC depuis n'importe où.

**Solutions possibles** :

1. **VPN + RDP/VNC** (recommandé)
   - Configurez un serveur VPN chez vous
   - Connectez-vous au VPN
   - Puis utilisez RDP/VNC en local

2. **Redirection de port** (moins sécurisé)
   - Configurez la redirection de port sur votre routeur
   - Port 5901 → Votre PC (pour VNC)
   - Port 3389 → Votre PC (pour RDP)
   - **Attention** : Exposé sur Internet !

3. **TeamViewer/AnyDesk** (le plus simple)
   - Fonctionne automatiquement via Internet
   - Pas de configuration réseau

## Scripts et automatisation

### Script de démarrage VNC intelligent

```bash
#!/bin/bash
# vnc-start.sh

DISPLAY_NUM=1  
RESOLUTION="1920x1080"  
DEPTH=24  

# Vérifier si VNC tourne déjà
if pgrep -f "Xvnc :$DISPLAY_NUM" > /dev/null; then
    echo "VNC serveur déjà en cours sur display :$DISPLAY_NUM"
    exit 0
fi

# Démarrer VNC
echo "Démarrage du serveur VNC..."  
vncserver :$DISPLAY_NUM -geometry $RESOLUTION -depth $DEPTH  

if [ $? -eq 0 ]; then
    echo "VNC serveur démarré avec succès sur display :$DISPLAY_NUM"
    echo "Connexion possible via : $(hostname -I | awk '{print $1}'):590$DISPLAY_NUM"
else
    echo "Erreur lors du démarrage du serveur VNC"
    exit 1
fi
```

Rendre exécutable :
```bash
chmod +x ~/scripts/vnc-start.sh
```

### Script de connexion VNC avec tunnel SSH

```bash
#!/bin/bash
# vnc-connect-ssh.sh

if [ -z "$1" ]; then
    echo "Usage: $0 serveur.com [display]"
    exit 1
fi

SERVER=$1  
DISPLAY=${2:-1}  
LOCAL_PORT=$((5900 + DISPLAY))  
REMOTE_PORT=$((5900 + DISPLAY))  

echo "Création du tunnel SSH vers $SERVER..."  
ssh -f -N -L $LOCAL_PORT:localhost:$REMOTE_PORT $SERVER  

if [ $? -eq 0 ]; then
    echo "Tunnel créé. Lancement du viewer VNC..."
    sleep 2
    vncviewer localhost:$DISPLAY

    # Fermer le tunnel après fermeture du viewer
    pkill -f "ssh.*$LOCAL_PORT:localhost:$REMOTE_PORT"
else
    echo "Erreur lors de la création du tunnel SSH"
    exit 1
fi
```

### Script de surveillance des connexions

```bash
#!/bin/bash
# monitor-remote-connections.sh

echo "=== Surveillance des connexions bureau à distance ==="  
echo ""  

echo "Connexions VNC :"  
netstat -tn 2>/dev/null | grep ':590[0-9]' || echo "Aucune connexion VNC active"  
echo ""  

echo "Connexions RDP :"  
netstat -tn 2>/dev/null | grep ':3389' || echo "Aucune connexion RDP active"  
echo ""  

echo "Sessions actives :"  
who  
echo ""  

echo "Processus VNC :"  
ps aux | grep -E '[X]vnc|[x]11vnc' || echo "Aucun serveur VNC actif"  
echo ""  

echo "Processus RDP :"  
systemctl status xrdp --no-pager 2>/dev/null || echo "xrdp non installé ou inactif"  
```

## Résumé des commandes essentielles

### VNC (TigerVNC)

```bash
# Installation
sudo apt install tigervnc-standalone-server tigervnc-viewer

# Configuration
vncpasswd                                     # Définir mot de passe  
nano ~/.vnc/xstartup                         # Configurer session  
chmod +x ~/.vnc/xstartup                     # Rendre exécutable  

# Gestion serveur
vncserver :1 -geometry 1920x1080 -depth 24  # Démarrer  
vncserver -kill :1                           # Arrêter  
vncserver -list                              # Lister sessions  

# Connexion client
vncviewer 192.168.1.100:1                    # Se connecter  
vncviewer -FullScreen 192.168.1.100:1        # Plein écran  
```

### VNC (x11vnc - partage de session)

```bash
# Installation
sudo apt install x11vnc

# Configuration
x11vnc -storepasswd                          # Définir mot de passe

# Démarrage
x11vnc -display :0 -auth guess -usepw -forever -bg  
x11vnc -display :0 -auth guess -usepw -forever -bg -ncache 10  # Avec cache  

# Arrêt
pkill x11vnc
```

### RDP (xrdp)

```bash
# Installation
sudo apt install xrdp

# Gestion du service
sudo systemctl start xrdp                    # Démarrer  
sudo systemctl stop xrdp                     # Arrêter  
sudo systemctl restart xrdp                  # Redémarrer  
sudo systemctl status xrdp                   # Statut  
sudo systemctl enable xrdp                   # Activer au démarrage  

# Configuration
nano ~/.xsession                             # Session utilisateur  
chmod +x ~/.xsession                         # Rendre exécutable  
sudo nano /etc/xrdp/xrdp.ini                # Config serveur  

# Logs
sudo tail -f /var/log/xrdp.log  
sudo tail -f /var/log/xrdp-sesman.log  
```

### Pare-feu

```bash
# VNC
sudo ufw allow 5900/tcp                      # Display :0  
sudo ufw allow 5901/tcp                      # Display :1  

# RDP
sudo ufw allow 3389/tcp

# Limité au réseau local (recommandé)
sudo ufw allow from 192.168.1.0/24 to any port 5901 proto tcp  
sudo ufw allow from 192.168.1.0/24 to any port 3389 proto tcp  
```

---

**Points clés à retenir** :
- VNC est universel et peut partager une session existante (x11vnc)
- RDP est optimal pour Windows et crée des sessions dédiées
- **Sécurité** : Utilisez toujours des tunnels SSH ou un VPN pour l'accès via Internet
- Les mots de passe forts sont essentiels pour VNC et RDP
- Ouvrez uniquement les ports nécessaires dans le pare-feu et limitez par IP si possible
- x11vnc est idéal pour le support technique (partage de session active)
- TigerVNC/xrdp est mieux pour le travail à distance (sessions dédiées)
- Désactivez les effets visuels pour de meilleures performances
- Surveillez régulièrement les connexions actives avec `who` et les logs
- Pour un usage professionnel, considérez des solutions comme NoMachine ou TeamViewer
- Testez toujours vos configurations en local avant de les exposer à distance

⏭️ [Résolution de problèmes réseau](/09-configuration-reseau-et-internet/08-resolution-de-problemes-reseau.md)
