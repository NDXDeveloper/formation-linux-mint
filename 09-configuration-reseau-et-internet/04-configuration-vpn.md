🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 9.4 Configuration VPN

## Introduction

Un VPN (Virtual Private Network - Réseau Privé Virtuel) est un outil qui crée un tunnel sécurisé et chiffré entre votre ordinateur et Internet. C'est comme si vous construisiez un tunnel privé à travers un espace public : personne ne peut voir ce qui passe à l'intérieur.

Dans ce chapitre, nous allons apprendre à configurer et utiliser un VPN sous Linux Mint, que vous utilisiez un service commercial (comme NordVPN, ProtonVPN, etc.) ou que vous souhaitiez vous connecter à un VPN d'entreprise ou personnel.

## Comprendre les VPN

### Qu'est-ce qu'un VPN ?

Imaginez que vous envoyez une lettre :

**Sans VPN** :
- Votre lettre passe par plusieurs bureaux de poste
- Chaque bureau peut voir l'expéditeur, le destinataire et potentiellement le contenu
- Votre fournisseur d'accès Internet (FAI) voit tout ce que vous faites en ligne

**Avec VPN** :
- Votre lettre est mise dans une enveloppe sécurisée et scellée
- Elle passe par un bureau de poste de confiance (serveur VPN)
- Ce bureau enlève l'enveloppe et envoie votre lettre
- Personne ne peut voir le contenu ni l'origine réelle

### Pourquoi utiliser un VPN ?

**Protection de la vie privée** :
- Masque votre adresse IP réelle
- Empêche votre FAI de voir vos activités en ligne
- Protège contre le suivi publicitaire
- Cache votre localisation géographique

**Sécurité** :
- Chiffre vos données sur les réseaux WiFi publics
- Protège vos informations sensibles (mots de passe, données bancaires)
- Sécurise vos communications

**Contournement de restrictions** :
- Accès aux contenus géo-bloqués
- Contournement de la censure dans certains pays
- Accès aux services depuis l'étranger

**Accès distant** :
- Connexion sécurisée au réseau de votre entreprise
- Accès à vos ressources à distance comme si vous étiez sur place

### Types de VPN

#### VPN commerciaux (grand public)

Services payants (ou gratuits avec limitations) :
- **Exemples** : NordVPN, ExpressVPN, ProtonVPN, Mullvad, Surfshark
- **Avantages** : Faciles à utiliser, nombreux serveurs, support client
- **Inconvénients** : Payants (généralement), vous devez faire confiance au fournisseur

#### VPN d'entreprise

Pour accéder au réseau de votre travail :
- Fourni par votre employeur
- Accès aux ressources internes (serveurs, imprimantes, etc.)
- Généralement obligatoire pour le télétravail

#### VPN auto-hébergé

Créer votre propre serveur VPN :
- **Avantages** : Contrôle total, confidentialité maximale
- **Inconvénients** : Technique, nécessite un serveur
- **Solutions** : OpenVPN, WireGuard, SoftEther

## Protocoles VPN courants

Linux Mint supporte plusieurs protocoles VPN. Voici les plus courants :

### OpenVPN

**Caractéristiques** :
- Le plus populaire et compatible
- Open source et sécurisé
- Fonctionne sur presque tous les systèmes
- Bien supporté sous Linux Mint

**Usage** : Idéal pour la plupart des utilisateurs

### WireGuard

**Caractéristiques** :
- Moderne et très rapide
- Code simple et auditabilité
- Moins de consommation de batterie
- Intégré dans le noyau Linux récent

**Usage** : Excellente option si disponible

### IKEv2/IPsec

**Caractéristiques** :
- Très stable, reconnexion rapide
- Bon pour les connexions mobiles
- Sécurité élevée

**Usage** : Souvent utilisé en entreprise

### L2TP/IPsec

**Caractéristiques** :
- Largement supporté
- Bonne sécurité
- Un peu plus lent qu'OpenVPN

**Usage** : Alternative quand OpenVPN n'est pas disponible

### PPTP (à éviter)

**Caractéristiques** :
- Ancien et rapide
- **Non sécurisé** - facilement piratable
- Déprécié

**Usage** : Ne l'utilisez plus, sauf contrainte absolue

## Installation des outils VPN

Avant de configurer un VPN, vous devez installer les paquets nécessaires.

### Installation pour OpenVPN

OpenVPN est le protocole le plus courant. Installez-le ainsi :

**Via le terminal** :
```bash
sudo apt update  
sudo apt install openvpn network-manager-openvpn network-manager-openvpn-gnome  
```

**Explication des paquets** :
- `openvpn` : Le logiciel VPN lui-même
- `network-manager-openvpn` : Plugin pour Network Manager
- `network-manager-openvpn-gnome` : Interface graphique pour la configuration

### Installation pour WireGuard

Pour utiliser WireGuard :

```bash
sudo apt update  
sudo apt install wireguard openresolv network-manager-wireguard  
```

### Installation pour autres protocoles

**L2TP/IPsec** :
```bash
sudo apt install network-manager-l2tp network-manager-l2tp-gnome
```

**OpenConnect (Cisco AnyConnect)** :
```bash
sudo apt install network-manager-openconnect network-manager-openconnect-gnome
```

**PPTP** (non recommandé) :
```bash
sudo apt install network-manager-pptp network-manager-pptp-gnome
```

### Redémarrer Network Manager

Après l'installation, redémarrez Network Manager pour qu'il détecte les nouveaux plugins :

```bash
sudo systemctl restart NetworkManager
```

Ou redémarrez simplement votre ordinateur.

## Configuration VPN via l'interface graphique

Linux Mint facilite la configuration des VPN grâce à une interface graphique intuitive.

### Méthode 1 : Via l'icône réseau

1. **Cliquez sur l'icône réseau** dans la barre des tâches
2. **Sélectionnez "Connexions réseau"** ou "Paramètres réseau"
3. **Cliquez sur le bouton "+"** pour ajouter une nouvelle connexion
4. **Sélectionnez le type de VPN** dans la liste déroulante

### Méthode 2 : Via les paramètres système

1. Menu principal → **Préférences** → **Réseau**
2. Cliquez sur **"+"** pour ajouter une connexion
3. Sélectionnez le type de VPN

## Configuration d'un VPN commercial

La plupart des fournisseurs VPN commerciaux utilisent OpenVPN et fournissent des fichiers de configuration.

### Obtenir les fichiers de configuration

1. **Connectez-vous** à votre compte chez votre fournisseur VPN
2. **Téléchargez les fichiers de configuration** :
   - Généralement dans une section "Téléchargements" ou "Configuration"
   - Format : fichiers `.ovpn` (OpenVPN)
   - Vous pouvez télécharger des fichiers pour différents pays/serveurs

3. **Enregistrez les fichiers** dans un dossier (ex: `~/Documents/VPN/`)

### Configuration avec un fichier .ovpn

#### Méthode graphique (recommandée pour débutants)

1. **Ouvrez les paramètres réseau** :
   - Clic sur l'icône réseau → Paramètres réseau
   - Cliquez sur "+" → Sélectionnez "Importer une configuration VPN..."

2. **Sélectionnez votre fichier .ovpn** :
   - Naviguez jusqu'à votre fichier de configuration
   - Sélectionnez-le et cliquez "Ouvrir"

3. **La configuration s'importe automatiquement** :
   - Le nom de la connexion est généralement le nom du serveur
   - Les paramètres sont pré-remplis

4. **Ajoutez vos identifiants** (si nécessaire) :
   - **Nom d'utilisateur** : Votre identifiant VPN
   - **Mot de passe** : Votre mot de passe VPN
   - Cochez "Stocker le mot de passe" pour ne pas le retaper à chaque fois (moins sécurisé mais plus pratique)

5. **Enregistrez** en cliquant sur "Ajouter" ou "Enregistrer"

#### Configuration manuelle

Si l'import automatique ne fonctionne pas :

1. **Créez une nouvelle connexion** :
   - Paramètres réseau → "+" → "OpenVPN"

2. **Remplissez les informations** :

   **Onglet "VPN"** :
   - **Nom de la connexion** : Nom descriptif (ex: "ProtonVPN France")
   - **Passerelle** : Adresse du serveur VPN (ex: fr.protonvpn.com ou une IP)
   - **Type** : Généralement "Certificats (TLS)"
   - **Certificat d'utilisateur** : Fichier .crt si fourni
   - **Certificat CA** : Fichier ca.crt (fourni par votre VPN)
   - **Clé privée** : Fichier .key si fourni
   - **Nom d'utilisateur** : Votre identifiant
   - **Mot de passe** : Votre mot de passe

   **Onglet "Avancé"** (optionnel) :
   - **Utiliser la compression** : Selon recommandations du fournisseur
   - **Port personnalisé** : Si spécifié (généralement 1194 pour UDP ou 443 pour TCP)
   - **Chiffrement des données** : Selon recommandations (souvent AES-256-GCM)

3. **Enregistrez la configuration**

### Exemples de configuration pour fournisseurs populaires

#### ProtonVPN

ProtonVPN fournit des fichiers .ovpn directement :

1. Téléchargez le fichier .ovpn depuis votre compte ProtonVPN
2. Importez-le via "Importer une configuration VPN..."
3. Entrez vos identifiants OpenVPN (différents de votre compte web)
4. Connectez-vous

**Alternative** : ProtonVPN offre une application native Linux :
```bash
# Suivez les instructions sur protonvpn.com/support/linux-vpn-setup/
```

#### NordVPN

NordVPN propose également des fichiers .ovpn et une application native :

1. **Fichiers .ovpn** : Téléchargez depuis nordvpn.com/ovpn/
2. **Importez** le fichier pour le pays souhaité
3. **Identifiants** : Utilisez vos identifiants de service (pas vos identifiants de compte)

**Application native** :
```bash
# Téléchargez le .deb depuis nordvpn.com
sudo dpkg -i nordvpn*.deb  
nordvpn login  
nordvpn connect  
```

#### Mullvad

Mullvad est très respectueux de la vie privée :

1. **Téléchargez** les fichiers de configuration depuis mullvad.net
2. **Importez** le fichier .ovpn
3. **Numéro de compte** : Utilisez votre numéro de compte Mullvad (pas de nom d'utilisateur/mot de passe)

**Application native** :
```bash
# Téléchargez depuis mullvad.net/download/
sudo dpkg -i mullvad-vpn*.deb
```

## Configuration d'un VPN d'entreprise

Les VPN d'entreprise utilisent souvent des protocoles différents. Votre service informatique doit vous fournir les informations nécessaires.

### Informations nécessaires

Demandez à votre administrateur réseau :
- **Type de VPN** : OpenVPN, L2TP/IPsec, IKEv2, OpenConnect, etc.
- **Adresse du serveur** : IP ou nom de domaine
- **Identifiants** : Nom d'utilisateur et mot de passe
- **Certificats** : Fichiers .crt, .key si nécessaires
- **Ports et protocoles** : TCP/UDP, numéro de port
- **Paramètres spécifiques** : Chiffrement, compression, etc.

### Configuration OpenConnect (Cisco AnyConnect)

Beaucoup d'entreprises utilisent Cisco AnyConnect :

1. **Installez le plugin** :
```bash
sudo apt install network-manager-openconnect network-manager-openconnect-gnome  
sudo systemctl restart NetworkManager  
```

2. **Créez la connexion** :
   - Paramètres réseau → "+" → "Cisco AnyConnect Compatible VPN (openconnect)"
   - **Passerelle** : Adresse du serveur fournie par votre entreprise
   - **Nom d'utilisateur** : Votre identifiant d'entreprise
   - **Certificat CA** : Si fourni par votre entreprise

3. **Enregistrez et connectez-vous**

### Configuration L2TP/IPsec

1. **Installez le plugin** :
```bash
sudo apt install network-manager-l2tp network-manager-l2tp-gnome  
sudo systemctl restart NetworkManager  
```

2. **Créez la connexion** :
   - Paramètres réseau → "+" → "Layer 2 Tunneling Protocol (L2TP)"

   **Onglet "Passerelle"** :
   - **Passerelle** : Adresse IP ou domaine du serveur
   - **Nom d'utilisateur** : Votre identifiant
   - **Mot de passe** : Votre mot de passe

   **Paramètres IPsec** (cliquez sur le bouton "Paramètres IPsec...") :
   - **Activer les paramètres IPsec** : Cochez
   - **Clé pré-partagée** : La clé fournie par votre admin (PSK)
   - Ou configurez les certificats si utilisés

3. **Enregistrez**

## Configuration WireGuard

WireGuard est moderne, rapide et de plus en plus populaire.

### Prérequis

```bash
sudo apt install wireguard openresolv network-manager-wireguard
```

### Configuration manuelle WireGuard

1. **Obtenez votre configuration** :
   - Votre fournisseur VPN vous donne généralement un fichier de configuration ou un QR code
   - Format : fichier `.conf`

2. **Importez la configuration** :

   **Méthode 1 - Via Network Manager** :
   - Paramètres réseau → "+" → "WireGuard"
   - Importez le fichier .conf ou entrez les paramètres manuellement

   **Méthode 2 - Via ligne de commande** :
   ```bash
   # Copiez votre fichier de configuration
   sudo cp votre-config.conf /etc/wireguard/wg0.conf

   # Démarrez WireGuard
   sudo wg-quick up wg0

   # Arrêtez WireGuard
   sudo wg-quick down wg0
   ```

3. **Activer au démarrage** (optionnel) :
```bash
sudo systemctl enable wg-quick@wg0
```

### Exemple de fichier de configuration WireGuard

```ini
[Interface]
PrivateKey = VOTRE_CLE_PRIVEE  
Address = 10.0.0.2/32  
DNS = 10.0.0.1  

[Peer]
PublicKey = CLE_PUBLIQUE_DU_SERVEUR  
Endpoint = serveur-vpn.example.com:51820  
AllowedIPs = 0.0.0.0/0  
PersistentKeepalive = 25  
```

Ne partagez jamais votre clé privée !

## Se connecter et se déconnecter du VPN

### Via l'icône réseau

**Se connecter** :
1. Cliquez sur l'icône réseau dans la barre des tâches
2. Sous "Connexions VPN", sélectionnez votre VPN
3. Cliquez dessus pour vous connecter
4. Une notification confirme la connexion

**Se déconnecter** :
1. Cliquez sur l'icône réseau
2. Sélectionnez "Déconnecter" sous le nom du VPN actif

### Via les paramètres réseau

1. Ouvrez les Paramètres réseau
2. Trouvez votre connexion VPN dans la liste
3. Utilisez le bouton à bascule pour activer/désactiver

### Connexion automatique

Pour que le VPN se connecte automatiquement au démarrage :

1. Ouvrez les Paramètres réseau
2. Sélectionnez votre connexion VPN
3. Cliquez sur "Modifier" (icône roue dentée)
4. Cochez "Se connecter automatiquement"
5. Enregistrez

**Attention** : La connexion automatique peut poser problème si :
- Le VPN n'est pas toujours disponible
- Vous ne voulez pas toujours passer par le VPN
- Vous utilisez différents réseaux

## Vérifier que le VPN fonctionne

Il est important de vérifier que votre VPN fonctionne réellement.

### Vérifier l'adresse IP

**Avant de vous connecter** :
1. Ouvrez votre navigateur
2. Allez sur : https://www.whatismyip.com/ ou https://ipleak.net/
3. Notez votre adresse IP et votre localisation

**Après connexion au VPN** :
1. Connectez-vous au VPN
2. Actualisez la page
3. Vérifiez que :
   - L'adresse IP a changé
   - La localisation correspond au serveur VPN choisi

### Vérifier les fuites DNS

Les fuites DNS révèlent vos requêtes DNS malgré le VPN :

1. Connectez-vous au VPN
2. Allez sur : https://dnsleaktest.com/
3. Cliquez sur "Extended test"
4. Vérifiez que les serveurs DNS appartiennent à votre VPN (pas à votre FAI)

### Vérifier les fuites WebRTC

WebRTC peut révéler votre vraie IP :

1. Allez sur : https://browserleaks.com/webrtc
2. Vérifiez que seule l'IP du VPN apparaît

**Pour bloquer les fuites WebRTC** :
- Dans Firefox : installez l'extension "Disable WebRTC"
- Ou désactivez WebRTC dans `about:config` (media.peerconnection.enabled = false)

### Test via terminal

```bash
# Voir votre IP publique
curl ifconfig.me

# Ou
curl ipinfo.io
```

Comparez avant et après connexion au VPN.

### Vérifier la connexion VPN active

```bash
# Voir les connexions actives
nmcli connection show --active

# Informations détaillées sur le VPN
ip addr show tun0  # ou wg0 pour WireGuard
```

## Configuration avancée

### Routage sélectif (Split Tunneling)

Par défaut, tout votre trafic passe par le VPN. Le split tunneling permet de choisir ce qui passe par le VPN.

**Cas d'usage** :
- Accéder au réseau local ET au VPN en même temps
- Utiliser le VPN seulement pour certaines applications
- Économiser de la bande passante

**Configuration** :

1. Modifiez votre connexion VPN
2. Onglet "Paramètres IPv4"
3. Décochez "Utiliser cette connexion uniquement pour les ressources de son réseau"
4. Dans "Routes...", ajoutez les réseaux spécifiques qui doivent passer par le VPN

**Exemple** : Pour router seulement 10.0.0.0/8 par le VPN :
- Adresse : 10.0.0.0
- Masque réseau : 8
- Passerelle : (vide)
- Métrique : 0

### Kill Switch (coupure Internet si VPN déconnecté)

Un kill switch empêche toute connexion Internet si le VPN se déconnecte.

**Via le pare-feu** :

```bash
# Bloquer tout sauf le VPN
sudo ufw default deny outgoing  
sudo ufw default deny incoming  

# Autoriser le trafic local
sudo ufw allow out on lo  
sudo ufw allow in on lo  

# Autoriser le serveur VPN (remplacez par votre IP de serveur VPN)
sudo ufw allow out to ADRESSE_SERVEUR_VPN

# Autoriser le trafic VPN
sudo ufw allow out on tun0  # ou wg0 pour WireGuard  
sudo ufw allow in on tun0  

# Activer
sudo ufw enable
```

**Attention** : Cette configuration stricte peut vous bloquer si vous ne configurez pas correctement.

### DNS personnalisé avec VPN

Pour forcer l'utilisation de DNS spécifiques :

1. Modifiez votre connexion VPN
2. Onglet "Paramètres IPv4"
3. Méthode : "Automatique (VPN) - Adresses seulement"
4. Serveurs DNS : Entrez vos DNS préférés
   - Cloudflare : 1.1.1.1, 1.0.0.1
   - Google : 8.8.8.8, 8.8.4.4
   - Quad9 : 9.9.9.9

### Multihop (VPN en cascade)

Passer par plusieurs serveurs VPN successivement :

**Avantages** :
- Anonymat accru
- Plus difficile à tracer

**Inconvénients** :
- Beaucoup plus lent
- Plus complexe à configurer

**Configuration** : Généralement proposé par le fournisseur VPN lui-même (ProtonVPN, NordVPN). Configuration manuelle complexe.

## Résolution des problèmes courants

### Impossible de se connecter au VPN

**Solutions** :

1. **Vérifier les identifiants** :
   - Assurez-vous d'utiliser les bons identifiants (parfois différents du compte web)
   - Vérifiez les majuscules/minuscules

2. **Vérifier la connexion Internet** :
   - Le VPN nécessite une connexion Internet fonctionnelle
   - Testez sans VPN d'abord

3. **Vérifier le pare-feu** :
   ```bash
   # Désactiver temporairement pour tester
   sudo ufw disable
   ```
   Si ça fonctionne, créez une règle pour le VPN :
   ```bash
   sudo ufw allow 1194/udp  # OpenVPN standard
   sudo ufw allow 51820/udp # WireGuard standard
   sudo ufw enable
   ```

4. **Vérifier les plugins installés** :
   ```bash
   dpkg -l | grep network-manager
   ```
   Réinstallez si nécessaire

5. **Redémarrer Network Manager** :
   ```bash
   sudo systemctl restart NetworkManager
   ```

### Le VPN se connecte mais pas d'Internet

**Solutions** :

1. **Vérifier les paramètres DNS** :
   - Modifiez la connexion VPN
   - Paramètres IPv4 → Serveurs DNS : ajoutez 8.8.8.8

2. **Vérifier le routage** :
   ```bash
   ip route show
   ```
   Vérifiez qu'une route par défaut via tun0/wg0 existe

3. **Désactiver IPv6** temporairement :
   - Paramètres IPv4 de la connexion VPN
   - Méthode IPv6 : "Ignorer"

4. **Vérifier avec le fournisseur** :
   - Le serveur VPN peut être hors ligne
   - Essayez un autre serveur

### VPN lent ou instable

**Optimisations** :

1. **Changer de serveur** :
   - Choisissez un serveur plus proche géographiquement
   - Les serveurs moins chargés sont plus rapides

2. **Changer de protocole** :
   - UDP est généralement plus rapide que TCP
   - WireGuard est plus rapide qu'OpenVPN

3. **Désactiver la compression** :
   - Parfois elle ralentit sur connexions rapides
   - Modifiez la connexion → Avancé → Désactiver la compression

4. **Vérifier votre connexion de base** :
   - Testez votre vitesse sans VPN
   - Un VPN ne peut pas être plus rapide que votre connexion

5. **MTU** :
   - Essayez de réduire le MTU à 1400 ou 1450
   - Modifiez la connexion → Avancé → MTU personnalisé

### Fuites DNS malgré le VPN

**Solutions** :

1. **Forcer les DNS du VPN** :
   ```bash
   sudo nano /etc/resolv.conf
   ```
   Remplacez par les DNS de votre VPN, puis :
   ```bash
   sudo chattr +i /etc/resolv.conf  # Protège le fichier
   ```

2. **Utiliser openresolv** :
   ```bash
   sudo apt install openresolv
   ```

3. **Configurer dans Network Manager** :
   - Paramètres IPv4 → Serveurs DNS
   - Ajoutez les DNS du VPN manuellement

### Le VPN se déconnecte fréquemment

**Solutions** :

1. **Activer la reconnexion automatique** :
   - Modifiez la connexion VPN
   - Options générales → Cochez "Se connecter automatiquement"

2. **Ajuster le Keep-Alive** (pour WireGuard) :
   - Augmentez `PersistentKeepalive` à 25 ou 30 secondes

3. **Changer de protocole** :
   - TCP est plus stable qu'UDP (mais plus lent)
   - Changez le port dans les paramètres avancés

4. **Désactiver la gestion d'énergie WiFi** :
   ```bash
   sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
   ```
   Changez `wifi.powersave = 3` en `wifi.powersave = 2`

### Erreur d'authentification

**Solutions** :

1. **Vérifier les certificats** :
   - Assurez-vous que tous les fichiers .crt, .key sont correctement spécifiés
   - Vérifiez les chemins absolus

2. **Vérifier la date et l'heure** :
   - Les certificats expirent et dépendent de l'heure
   ```bash
   timedatectl status
   ```
   Synchronisez si nécessaire :
   ```bash
   sudo timedatectl set-ntp true
   ```

3. **Problèmes de permissions** :
   ```bash
   # Vérifier les permissions des fichiers de configuration
   ls -l ~/Documents/VPN/
   ```

## Tester et comparer les VPN

### Tester la vitesse

**Outil en ligne** :
- https://www.speedtest.net/
- Testez avec et sans VPN
- Comparez différents serveurs

**Via terminal** :
```bash
# Installer speedtest-cli
sudo apt install speedtest-cli

# Tester
speedtest-cli
```

### Tester la sécurité

**Vérifications complètes** :
- https://ipleak.net/ (complet)
- https://www.dnsleaktest.com/ (DNS)
- https://browserleaks.com/webrtc (WebRTC)
- https://www.doileak.com/ (général)

### Benchmarker les serveurs

Pour trouver le serveur le plus rapide :

```bash
# Ping vers différents serveurs
ping -c 5 fr.serveur-vpn.com  
ping -c 5 de.serveur-vpn.com  
ping -c 5 uk.serveur-vpn.com  
```

Plus le ping est bas, meilleure est la connexion.

## Sécurité et bonnes pratiques

### Choisir un bon fournisseur VPN

**Critères importants** :

1. **Politique de non-journalisation** :
   - Vérifiez que le VPN ne garde pas de logs de vos activités
   - Préférez les VPN audités indépendamment

2. **Juridiction** :
   - Pays avec bonnes lois sur la vie privée
   - Évitez les pays membres de "5/9/14 Eyes"

3. **Protocoles modernes** :
   - Support de WireGuard ou OpenVPN
   - Évitez les VPN n'offrant que PPTP

4. **Open source** :
   - Applications et protocoles open source préférables
   - Meilleure transparence et sécurité

5. **Réputation** :
   - Lisez les avis indépendants
   - Méfiez-vous des VPN "gratuits" (ils vendent souvent vos données)

### VPN gratuits vs payants

**VPN gratuits** :
- **Avantages** : Gratuit, facile d'essayer
- **Inconvénients** :
  - Souvent logs de vos données
  - Vitesses limitées
  - Peu de serveurs
  - Peuvent injecter de la publicité
  - Sécurité douteuse

**VPN gratuits recommandables** :
- ProtonVPN (version gratuite limitée mais honnête)
- Windscribe (version gratuite avec 10GB/mois)

**VPN payants** :
- **Avantages** :
  - Meilleures vitesses
  - Plus de serveurs
  - Support client
  - Généralement plus sécurisés
- **Inconvénients** : Coût mensuel/annuel

### Ne jamais faire avec un VPN

**Faux sentiment de sécurité** :
- Un VPN ne vous rend pas anonyme à 100%
- Ne protège pas contre les malwares
- Ne remplace pas les bonnes pratiques de sécurité

**Activités illégales** :
- Un VPN n'autorise pas les activités illégales
- Certains VPN collaborent avec les autorités
- Vous restez responsable de vos actes

**Confiance aveugle** :
- Vous faites confiance au VPN avec vos données
- Choisissez un fournisseur réputé
- Lisez la politique de confidentialité

### VPN et vie privée

**Ce qu'un VPN cache** :
- Votre adresse IP aux sites web visités
- Vos activités à votre FAI
- Votre localisation géographique

**Ce qu'un VPN ne cache pas** :
- Vos activités aux sites sur lesquels vous êtes connecté (Facebook, Google, etc.)
- Vos informations si vous les partagez vous-même
- Les cookies et trackers déjà présents

**Combiner avec d'autres outils** :
- Navigateur axé sur la vie privée (Firefox avec extensions)
- Bloqueur de publicités (uBlock Origin)
- Gestion des cookies stricte
- HTTPS Everywhere

## Cas d'usage spécifiques

### Télétravail

**Configuration pour accéder au réseau d'entreprise** :

1. Utilisez la configuration fournie par votre entreprise
2. Activez la connexion automatique uniquement si recommandé
3. Ne mélangez pas VPN personnel et VPN d'entreprise simultanément
4. Utilisez le split tunneling si vous avez besoin d'accéder à Internet ET au réseau d'entreprise

### Voyage à l'étranger

**Accéder à vos services habituels** :

1. Connectez-vous à un serveur VPN dans votre pays d'origine
2. Vous pourrez accéder aux services géo-bloqués
3. Sur WiFi public : TOUJOURS utiliser un VPN

**Contourner la censure** :
- Utilisez des protocoles difficiles à détecter (OpenVPN sur port 443)
- WireGuard peut être bloqué dans certains pays
- Testez plusieurs serveurs

### Sécurité sur WiFi public

**Dans les cafés, aéroports, hôtels** :

1. **Activez le VPN AVANT de vous connecter** au WiFi public
2. Utilisez HTTPS partout (extension HTTPS Everywhere)
3. Évitez les opérations sensibles (banque) même avec VPN
4. Désactivez le partage de fichiers

### Streaming et Torrents

**Streaming** :
- Certains services bloquent les VPN
- Essayez différents serveurs
- Les VPN payants fonctionnent généralement mieux

**Torrents** :
- Vérifiez que votre VPN autorise le P2P
- Utilisez des serveurs P2P dédiés
- Activez le kill switch pour éviter les fuites
- Bind votre client torrent à l'interface VPN :
  - Dans Transmission : Préférences → Réseau → Interface réseau : tun0 (ou wg0)

## Scripts et automatisation

### Script de connexion automatique

Créez un script pour vous connecter facilement :

```bash
#!/bin/bash
# ~/bin/vpn-connect.sh

# Connexion au VPN
nmcli connection up "Nom-de-votre-VPN"

# Vérifier la connexion
sleep 3  
curl ifconfig.me  
echo ""  
echo "VPN connecté !"  
```

Rendez-le exécutable :
```bash
chmod +x ~/bin/vpn-connect.sh
```

Utilisez-le :
```bash
~/bin/vpn-connect.sh
```

### Script de vérification VPN

```bash
#!/bin/bash
# ~/bin/vpn-check.sh

echo "Vérification du VPN..."  
echo "Votre IP actuelle :"  
curl -s ifconfig.me  
echo ""  
echo ""  
echo "Test de fuites DNS :"  
curl -s https://1.1.1.1/cdn-cgi/trace | grep ip  
```

### Rotation automatique de serveurs

Pour changer de serveur VPN régulièrement (via cron) :

```bash
#!/bin/bash
# Déconnexion
nmcli connection down "VPN-Serveur1"

# Connexion au serveur suivant
nmcli connection up "VPN-Serveur2"
```

## Monitoring et logs

### Voir les logs du VPN

```bash
# Logs OpenVPN
sudo journalctl -u openvpn

# Logs Network Manager concernant le VPN
sudo journalctl -u NetworkManager | grep -i vpn

# Logs système
sudo tail -f /var/log/syslog | grep -i vpn
```

### Surveiller l'utilisation

```bash
# Statistiques de l'interface VPN
ip -s link show tun0  # ou wg0

# Trafic en temps réel
sudo iftop -i tun0
```

## Alternatives et outils complémentaires

### Tor (The Onion Router)

Pour un anonymat maximal :
- Plus anonyme qu'un VPN seul
- Beaucoup plus lent
- Peut être combiné avec un VPN (VPN → Tor)

```bash
sudo apt install torbrowser-launcher
```

### Proxy SOCKS

Alternative légère au VPN pour certains usages :
- Moins de ressources
- Pas de chiffrement complet
- Utile pour contourner des blocages simples

### OpenVPN sur routeur

Installer OpenVPN directement sur votre routeur :
- Protège tous les appareils du réseau
- Configuration une seule fois
- Nécessite un routeur compatible (DD-WRT, OpenWRT)

## Aller plus loin

### Héberger votre propre serveur VPN

**Avantages** :
- Contrôle total
- Confidentialité maximale
- Pas de limites de bande passante

**Solutions** :
- **OpenVPN** : Solution classique
- **WireGuard** : Moderne et simple
- **SoftEther** : Très polyvalent

**Hébergement** :
- VPS (Vultr, DigitalOcean, OVH)
- Raspberry Pi à la maison
- Serveur cloud

### Documenter votre configuration

Gardez une trace de :
- Nom et paramètres de chaque connexion VPN
- Fichiers de configuration utilisés
- Identifiants (dans un gestionnaire de mots de passe)
- Serveurs favoris et leurs performances

### Tester régulièrement

- Vérifiez mensuellement les fuites DNS
- Testez la vitesse de vos serveurs
- Mettez à jour vos fichiers de configuration si nécessaire
- Vérifiez les mises à jour de vos applications VPN

## Résumé des commandes utiles

```bash
# Installation
sudo apt install openvpn network-manager-openvpn network-manager-openvpn-gnome  
sudo apt install wireguard network-manager-wireguard  

# Gestion via nmcli
nmcli connection show                    # Lister les connexions  
nmcli connection up "Nom-VPN"           # Se connecter  
nmcli connection down "Nom-VPN"         # Se déconnecter  
nmcli connection show --active          # Voir les connexions actives  

# Vérifications
curl ifconfig.me                        # Voir votre IP publique  
ip addr show tun0                       # Infos sur l'interface VPN  
ip route                                # Voir les routes  
ping -c 4 8.8.8.8                      # Tester la connexion  

# WireGuard spécifique
sudo wg-quick up wg0                    # Démarrer WireGuard  
sudo wg-quick down wg0                  # Arrêter WireGuard  
sudo wg show                            # Statut WireGuard  

# Logs
sudo journalctl -u NetworkManager | grep -i vpn  
sudo tail -f /var/log/syslog | grep vpn  
```

---

**Points clés à retenir** :
- Un VPN chiffre votre connexion et masque votre IP, mais ne vous rend pas anonyme à 100%
- Linux Mint supporte nativement OpenVPN, WireGuard et autres protocoles via Network Manager
- L'import de fichiers .ovpn est la méthode la plus simple pour les VPN commerciaux
- Vérifiez toujours que votre VPN fonctionne (IP, fuites DNS, WebRTC)
- Choisissez un fournisseur VPN réputé avec une politique de non-journalisation
- Un kill switch empêche les fuites si le VPN se déconnecte
- Le split tunneling permet de router seulement certains trafics par le VPN
- Sur WiFi public, utilisez TOUJOURS un VPN
- Les VPN gratuits peuvent compromettre votre vie privée - préférez les options payantes réputées
- Combinez le VPN avec d'autres bonnes pratiques de sécurité pour une protection optimale

⏭️ [SSH pour connexions à distance](/09-configuration-reseau-et-internet/05-ssh-pour-connexions-a-distance.md)
