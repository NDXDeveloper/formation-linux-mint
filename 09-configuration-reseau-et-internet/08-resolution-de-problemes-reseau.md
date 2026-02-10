🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 9.8 Résolution de problèmes réseau

## Introduction

Les problèmes réseau peuvent être frustrants : pas d'Internet, connexion lente, WiFi qui se déconnecte... Mais avec la bonne méthodologie et les bons outils, la plupart des problèmes peuvent être résolus rapidement.

Ce chapitre vous guidera à travers les problèmes réseau les plus courants sous Linux Mint et vous donnera les outils pour les diagnostiquer et les résoudre. Même si vous n'êtes pas un expert technique, vous pourrez suivre ces étapes pour identifier et souvent corriger les problèmes vous-même.

## Méthodologie de diagnostic réseau

Quand vous rencontrez un problème réseau, suivez cette approche systématique :

### 1. Identifier le problème

**Posez-vous ces questions** :

- **Le problème est-il nouveau ou a-t-il toujours existé ?**
  - Nouveau → Qu'est-ce qui a changé récemment ?
  - Ancien → Configuration initiale incorrecte

- **Le problème affecte-t-il tout ou seulement certains services ?**
  - Tout → Problème de connexion basique
  - Certains services → Problème spécifique (DNS, pare-feu, etc.)

- **Le problème affecte-t-il tous les appareils ou seulement cet ordinateur ?**
  - Tous → Problème de réseau/routeur/FAI
  - Cet ordinateur seulement → Problème local

- **Le problème est-il constant ou intermittent ?**
  - Constant → Plus facile à diagnostiquer
  - Intermittent → Interférences, problème matériel, surcharge

### 2. Vérifier les bases

Avant d'aller plus loin, vérifiez toujours :

**Physiquement** :
- Câbles Ethernet bien branchés ?
- WiFi activé (interrupteur ou touche Fn+F2 sur les portables) ?
- Routeur allumé et fonctionnel ?
- Voyants lumineux sur les prises réseau ?

**Logiciellement** :
- Network Manager en cours d'exécution ?
- Connecté au bon réseau WiFi ?
- Mode avion désactivé ?

### 3. Isoler le problème

Déterminez où se situe le problème dans la chaîne :

**Ordinateur → Routeur → Internet → Site Web**

Testez chaque étape :
1. L'ordinateur a-t-il une adresse IP ?
2. Peut-il contacter le routeur ?
3. Peut-il contacter Internet ?
4. Le DNS fonctionne-t-il ?

### 4. Tester et vérifier

Utilisez les outils de diagnostic pour confirmer vos hypothèses.

### 5. Appliquer la solution

Commencez par les solutions simples avant les complexes.

### 6. Documenter

Notez ce qui a fonctionné pour la prochaine fois.

## Vérifications de base

### Vérifier l'état de Network Manager

Network Manager est le service qui gère les connexions réseau sous Linux Mint.

```bash
# Vérifier que Network Manager fonctionne
systemctl status NetworkManager
```

Devrait afficher "active (running)".

**Si inactif, redémarrer** :
```bash
sudo systemctl restart NetworkManager
```

### Vérifier les interfaces réseau

```bash
# Lister toutes les interfaces réseau
ip link show

# Ou avec plus de détails
ip addr show
```

**Que regarder** :
- Votre interface WiFi (généralement `wlan0`, `wlp2s0`, ou similaire)
- Votre interface Ethernet (généralement `eth0`, `enp3s0`, ou similaire)
- État : `UP` = activée, `DOWN` = désactivée

**Exemple de sortie** :
```
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP
    inet 192.168.1.100/24 brd 192.168.1.255 scope global dynamic
```

- `UP,LOWER_UP` : Interface active
- `inet 192.168.1.100/24` : Adresse IP attribuée

### Activer/désactiver une interface

```bash
# Désactiver
sudo ip link set enp3s0 down

# Activer
sudo ip link set enp3s0 up
```

### Vérifier l'adresse IP

```bash
# Voir toutes les adresses IP
ip addr show

# Ou simplement
hostname -I
```

**Problème** : Pas d'adresse IP ou adresse en 169.254.x.x
- 169.254.x.x = APIPA, aucun serveur DHCP trouvé
- Pas d'adresse = Interface non configurée

**Solution** : Renouveler le bail DHCP (voir section suivante)

### Renouveler l'adresse IP (DHCP)

```bash
# Avec nmcli
sudo nmcli connection down "Nom-de-votre-connexion"  
sudo nmcli connection up "Nom-de-votre-connexion"  

# Ou redémarrer Network Manager
sudo systemctl restart NetworkManager

# Ou avec dhclient (méthode manuelle)
sudo dhclient -r  # Libérer  
sudo dhclient     # Renouveler  
```

### Vérifier la passerelle par défaut

La passerelle (gateway) est généralement votre routeur.

```bash
# Voir la route par défaut
ip route show

# Ou
ip route | grep default
```

**Exemple** :
```
default via 192.168.1.1 dev enp3s0 proto dhcp metric 100
```

- `192.168.1.1` : Votre passerelle (routeur)
- `dev enp3s0` : Interface utilisée

**Problème** : Pas de route par défaut  
**Solution** : Problème DHCP ou configuration manuelle incorrecte  

### Vérifier les serveurs DNS

```bash
# Voir les serveurs DNS configurés
resolvectl status

# Ou
cat /etc/resolv.conf
```

**Exemple** :
```
nameserver 192.168.1.1  
nameserver 8.8.8.8  
```

**Problème** : Pas de serveur DNS  
**Solution** : Configurer manuellement ou vérifier DHCP  

## Tests de connectivité

### Test 1 : Ping vers la passerelle (routeur)

```bash
# Remplacez par l'IP de votre routeur
ping -c 4 192.168.1.1
```

**Résultat attendu** :
```
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=1.23 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=1.15 ms
...
4 packets transmitted, 4 received, 0% packet loss
```

**Si ça fonctionne** : Connexion locale OK, problème ailleurs  
**Si ça ne fonctionne pas** :  
- Vérifier câble/WiFi
- Vérifier adresse IP
- Vérifier routeur

### Test 2 : Ping vers Internet (adresse IP)

```bash
# Google DNS
ping -c 4 8.8.8.8

# Cloudflare DNS
ping -c 4 1.1.1.1
```

**Si ça fonctionne** : Connexion Internet OK, problème DNS probablement  
**Si ça ne fonctionne pas** :  
- Problème de routeur
- Problème FAI
- Pare-feu bloque

### Test 3 : Ping vers un nom de domaine

```bash
ping -c 4 google.com
```

**Si ça fonctionne** : Tout OK !  
**Si ça ne fonctionne pas mais 8.8.8.8 fonctionne** : Problème DNS  

### Test 4 : Traceroute

Voir le chemin que prennent les paquets.

```bash
# Installer si nécessaire
sudo apt install traceroute

# Tracer le chemin vers google.com
traceroute google.com

# Ou avec mtr (plus moderne)
sudo apt install mtr  
mtr google.com  
```

**Utilité** : Identifier où les paquets se perdent ou ralentissent.

### Test 5 : Test de port spécifique

```bash
# Tester si un port est ouvert (ex: port 80 HTTP)
nc -zv google.com 80

# Ou avec telnet
telnet google.com 80
```

**Si connexion réussie** : Port accessible  
**Si échec** : Port bloqué ou service non disponible  

## Problèmes courants et solutions

### Pas de connexion Internet

**Symptômes** :
- Icône réseau montre "pas de connexion"
- Impossible de naviguer
- Aucun réseau WiFi visible

**Diagnostic** :

```bash
# Vérifier les interfaces
ip link show

# Vérifier l'état Network Manager
systemctl status NetworkManager

# Vérifier les pilotes
lspci -k | grep -A 3 -i network
```

**Solutions** :

1. **Redémarrer Network Manager** :
```bash
sudo systemctl restart NetworkManager
```

2. **Vérifier que WiFi n'est pas désactivé** :
```bash
# Voir le statut RF (radio)
nmcli radio all

# Activer WiFi
nmcli radio wifi on
```

3. **Vérifier le pilote** :
```bash
# Voir si le pilote est chargé
lsmod | grep -i wifi  
lsmod | grep -i iwl  # Pour Intel  
lsmod | grep -i rt   # Pour Realtek  
```

4. **Réinstaller le pilote** :
- Ouvrez "Gestionnaire de pilotes"
- Vérifiez si des pilotes propriétaires sont disponibles
- Installez-les

5. **Dernier recours - Redémarrer** :
```bash
sudo reboot
```

### Connexion intermittente (se déconnecte régulièrement)

**Symptômes** :
- WiFi se déconnecte toutes les X minutes
- Connexion instable
- "Connecté" mais pas d'Internet par moments

**Diagnostic** :

```bash
# Surveiller les déconnexions
journalctl -f | grep -i network

# Vérifier la qualité du signal WiFi
watch -n 1 'iwconfig wlan0 | grep -i quality'
```

**Solutions** :

1. **Désactiver la gestion d'énergie WiFi** :
```bash
sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
```

Changez `wifi.powersave = 3` en `wifi.powersave = 2`

Redémarrez Network Manager :
```bash
sudo systemctl restart NetworkManager
```

2. **Interférences WiFi - Changer de canal** :
   - Connectez-vous à votre routeur
   - Changez le canal WiFi (essayez 1, 6 ou 11 pour 2.4GHz)
   - Ou utilisez la bande 5GHz si disponible

3. **Distance/Obstacles** :
   - Rapprochez-vous du routeur
   - Évitez les murs épais, micro-ondes, etc.

4. **Mettre à jour le pilote** :
```bash
sudo apt update  
sudo apt upgrade  
```

5. **Réinitialiser la connexion** :
```bash
# Supprimer et recréer
nmcli connection delete "Nom-WiFi"
# Reconnectez-vous via l'interface graphique
```

### DNS ne fonctionne pas

**Symptômes** :
- `ping 8.8.8.8` fonctionne
- `ping google.com` ne fonctionne pas
- Erreur "impossible de résoudre l'hôte"

**Diagnostic** :

```bash
# Vérifier les DNS configurés
cat /etc/resolv.conf

# Tester la résolution DNS
nslookup google.com
# Ou
dig google.com
```

**Solutions** :

1. **Changer les serveurs DNS manuellement** :

   Via l'interface graphique :
   - Paramètres réseau → Votre connexion → Modifier
   - Onglet "Paramètres IPv4"
   - Méthode : "Automatique (DHCP) - Adresses seulement"
   - Serveurs DNS : `8.8.8.8, 8.8.4.4` (Google)
   - Ou : `1.1.1.1, 1.0.0.1` (Cloudflare)
   - Enregistrer et reconnecter

2. **Via la ligne de commande** :
```bash
# Éditer resolv.conf (temporaire)
sudo nano /etc/resolv.conf
```

Ajoutez :
```
nameserver 8.8.8.8  
nameserver 8.8.4.4  
```

**Note** : Ce fichier peut être écrasé au redémarrage.

3. **Solution permanente avec resolved** :
```bash
sudo nano /etc/systemd/resolved.conf
```

Décommentez et modifiez :
```
[Resolve]
DNS=8.8.8.8 8.8.4.4  
FallbackDNS=1.1.1.1 1.0.0.1  
```

Redémarrez :
```bash
sudo systemctl restart systemd-resolved
```

4. **Vider le cache DNS** :
```bash
sudo systemd-resolve --flush-caches
# Ou
sudo systemctl restart systemd-resolved
```

### Connexion lente

**Symptômes** :
- Internet fonctionne mais très lent
- Téléchargements prennent trop de temps
- Vidéos en streaming saccadées

**Diagnostic** :

```bash
# Tester la vitesse (installer speedtest-cli)
sudo apt install speedtest-cli  
speedtest-cli  

# Vérifier l'utilisation de la bande passante
sudo apt install nethogs  
sudo nethogs  # Voir quel programme utilise le réseau  

# Vérifier les paquets perdus
ping -c 100 8.8.8.8 | tail -5
```

**Solutions** :

1. **Vérifier que le problème est local** :
   - Testez sur un autre appareil
   - Si lent partout → Problème routeur/FAI
   - Si lent seulement sur cet ordinateur → Problème local

2. **Désactiver IPv6** (parfois cause des lenteurs) :
```bash
# Temporaire
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1  
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1  

# Permanent
sudo nano /etc/sysctl.conf
```

Ajoutez :
```
net.ipv6.conf.all.disable_ipv6 = 1  
net.ipv6.conf.default.disable_ipv6 = 1  
net.ipv6.conf.lo.disable_ipv6 = 1  
```

Puis :
```bash
sudo sysctl -p
```

3. **Optimiser les paramètres TCP** :
```bash
sudo nano /etc/sysctl.conf
```

Ajoutez (pour connexions rapides) :
```
net.core.rmem_max = 16777216  
net.core.wmem_max = 16777216  
net.ipv4.tcp_rmem = 4096 87380 16777216  
net.ipv4.tcp_wmem = 4096 65536 16777216  
```

Appliquez :
```bash
sudo sysctl -p
```

4. **Vérifier MTU** :
```bash
# Voir MTU actuel
ip link show | grep mtu

# Tester MTU optimal (diminuez jusqu'à ce que ça passe)
ping -M do -s 1472 8.8.8.8

# Si nécessaire, changer MTU
sudo ip link set dev enp3s0 mtu 1450
```

5. **Fermer les applications gourmandes** :
```bash
# Voir l'utilisation réseau
nethogs
```

6. **QoS sur le routeur** :
   - Configurez la qualité de service (QoS) sur votre routeur
   - Priorisez votre ordinateur ou certains services

### Impossible de se connecter au WiFi

**Symptômes** :
- WiFi visible mais connexion échoue
- Demande le mot de passe en boucle
- Erreur "Échec de l'activation de la connexion"

**Solutions** :

1. **Vérifier le mot de passe** :
   - Majuscules/minuscules
   - Caractères spéciaux
   - Tapez-le lentement et vérifiez

2. **Oublier et reconnecter** :
```bash
# Lister les connexions
nmcli connection show

# Supprimer
nmcli connection delete "Nom-WiFi"

# Reconnectez-vous via l'interface graphique
```

3. **Vérifier le type de sécurité** :
   - WPA2-PSK (le plus courant)
   - Assurez-vous qu'il correspond au routeur

4. **Désactiver/Réactiver WiFi** :
```bash
nmcli radio wifi off  
sleep 5  
nmcli radio wifi on  
```

5. **Réinitialiser Network Manager** :
```bash
sudo systemctl stop NetworkManager  
sudo rm /var/lib/NetworkManager/NetworkManager.state  
sudo systemctl start NetworkManager  
```

### Ethernet ne fonctionne pas

**Symptômes** :
- Câble branché mais pas de connexion
- Pas de voyant lumineux sur le port
- Interface non détectée

**Diagnostic** :

```bash
# Vérifier que la carte est détectée
lspci | grep -i ethernet

# Vérifier l'état
ip link show

# Vérifier les pilotes
lspci -k | grep -i ethernet -A 3
```

**Solutions** :

1. **Vérifier le câble** :
   - Testez avec un autre câble
   - Testez sur un autre port du routeur
   - Vérifiez les voyants

2. **Activer l'interface** :
```bash
sudo ip link set enp3s0 up
```

3. **Vérifier BIOS/UEFI** :
   - Redémarrez l'ordinateur
   - Entrez dans le BIOS (F2, Del, F10 selon PC)
   - Vérifiez que la carte réseau est activée

4. **Installer/réinstaller le pilote** :
```bash
# Pour Realtek (fréquent)
sudo apt install r8168-dkms

# Reconstruire les pilotes
sudo dpkg-reconfigure linux-headers-$(uname -r)
```

5. **Tester avec une adresse IP statique** :
```bash
sudo ip addr add 192.168.1.50/24 dev enp3s0  
sudo ip route add default via 192.168.1.1  
```

### Pas de résolution de noms sur réseau local

**Symptômes** :
- `ping serveur-local` ne fonctionne pas
- `ping 192.168.1.100` fonctionne
- Besoin de toujours utiliser les IP

**Solutions** :

1. **Installer Avahi (mDNS/Zeroconf)** :
```bash
sudo apt install avahi-daemon  
sudo systemctl enable avahi-daemon  
sudo systemctl start avahi-daemon  
```

Utilisez `.local` :
```bash
ping serveur-local.local
```

2. **Éditer /etc/hosts** :
```bash
sudo nano /etc/hosts
```

Ajoutez :
```
192.168.1.100   serveur-local
192.168.1.101   nas
192.168.1.102   imprimante
```

3. **Configurer le domaine de recherche** :
```bash
sudo nano /etc/systemd/resolved.conf
```

Ajoutez :
```
[Resolve]
Domains=local mondomaine.local
```

Redémarrez :
```bash
sudo systemctl restart systemd-resolved
```

## Outils de diagnostic réseau

### nmcli - Outil en ligne de commande Network Manager

**Voir toutes les connexions** :
```bash
nmcli connection show
```

**Voir les appareils** :
```bash
nmcli device status
```

**Voir les réseaux WiFi disponibles** :
```bash
nmcli device wifi list
```

**Se connecter à un WiFi** :
```bash
nmcli device wifi connect "SSID" password "mot_de_passe"
```

**Voir les détails d'une connexion** :
```bash
nmcli connection show "Nom-connexion"
```

**Activer/désactiver une connexion** :
```bash
nmcli connection up "Nom-connexion"  
nmcli connection down "Nom-connexion"  
```

### ifconfig (obsolète mais encore utilisé)

**Voir toutes les interfaces** :
```bash
ifconfig

# Ou seulement une
ifconfig enp3s0
```

**Note** : `ifconfig` est obsolète, préférez `ip`.

### ss - Statistiques de socket

Remplaçant moderne de `netstat`.

```bash
# Voir toutes les connexions
ss

# Seulement TCP
ss -t

# Seulement en écoute
ss -l

# Avec numéros de port
ss -n

# Combinaisons utiles
ss -tuln  # TCP+UDP, écoute, numérique  
ss -tp    # TCP avec processus  
```

### netstat (ancien mais connu)

```bash
# Installer si nécessaire
sudo apt install net-tools

# Voir les connexions actives
netstat -tuln

# Voir les statistiques
netstat -s

# Voir la table de routage
netstat -r
```

### ethtool - Informations Ethernet

```bash
# Installer
sudo apt install ethtool

# Voir les détails d'une interface
sudo ethtool enp3s0

# Vitesse de la liaison
sudo ethtool enp3s0 | grep Speed

# Statistiques
sudo ethtool -S enp3s0
```

### iwconfig - Configuration WiFi

```bash
# Voir la configuration WiFi
iwconfig

# Détails d'une interface
iwconfig wlan0
```

Informations importantes :
- ESSID : Nom du réseau
- Quality : Qualité du signal
- Signal level : Force du signal
- Bit Rate : Vitesse de connexion

### wavemon - Moniteur WiFi visuel

```bash
# Installer
sudo apt install wavemon

# Lancer
wavemon
```

Interface interactive montrant :
- Force du signal
- Qualité de la liaison
- Statistiques en temps réel

Naviguez avec F1-F10.

### iftop - Bande passante en temps réel

```bash
# Installer
sudo apt install iftop

# Lancer
sudo iftop

# Pour une interface spécifique
sudo iftop -i enp3s0
```

Affiche en temps réel :
- Connexions actives
- Bande passante utilisée par connexion
- Totaux

### nmap - Scanner de réseau

```bash
# Installer
sudo apt install nmap

# Scanner votre réseau local
nmap 192.168.1.0/24

# Scanner un hôte spécifique
nmap 192.168.1.1

# Scanner avec détection OS
sudo nmap -O 192.168.1.1

# Scanner les ports ouverts
nmap -p- 192.168.1.1
```

### tcpdump - Capture de paquets

```bash
# Installer
sudo apt install tcpdump

# Capturer sur une interface
sudo tcpdump -i enp3s0

# Capturer et sauvegarder
sudo tcpdump -i enp3s0 -w capture.pcap

# Filtrer par hôte
sudo tcpdump -i enp3s0 host 192.168.1.1

# Filtrer par port
sudo tcpdump -i enp3s0 port 80
```

### Wireshark - Analyseur de paquets graphique

```bash
# Installer
sudo apt install wireshark

# Lancer (donner les permissions à votre utilisateur)
sudo dpkg-reconfigure wireshark-common
# Répondez "Oui"
sudo usermod -aG wireshark $USER

# Déconnectez-vous et reconnectez-vous, puis :
wireshark
```

Interface graphique puissante pour analyser le trafic réseau.

### iperf3 - Test de vitesse réseau

```bash
# Installer
sudo apt install iperf3

# Sur le serveur
iperf3 -s

# Sur le client (tester vers le serveur)
iperf3 -c adresse_serveur

# Test bidirectionnel
iperf3 -c adresse_serveur --bidir

# Test UDP
iperf3 -c adresse_serveur -u
```

Utile pour tester la vitesse réelle entre deux machines.

## Outils graphiques

### Network Manager Applet

L'icône réseau dans la barre des tâches :
- Clic gauche : Voir/changer connexions
- Clic droit → Informations de connexion : Détails IP, DNS, etc.
- Clic droit → Modifier les connexions : Gérer toutes les connexions

### Paramètres réseau système

Menu → Préférences → Réseau
- Vue d'ensemble de toutes les connexions
- Configuration graphique
- Activation/désactivation facile

### Moniteur système

Menu → Administration → Moniteur système
- Onglet "Ressources" → Section "Réseau"
- Voir l'utilisation de la bande passante en temps réel
- Historique graphique

### GNOME Network Tools (nettools)

```bash
# Installer
sudo apt install gnome-nettool

# Lancer
gnome-nettool
```

Interface graphique pour :
- Ping
- Netstat
- Traceroute
- Scan de ports
- Lookup DNS
- Finger
- Whois

### Wireshark (déjà mentionné)

L'outil graphique le plus puissant pour l'analyse réseau.

## Problèmes WiFi spécifiques

### WiFi lent par rapport à Ethernet

**Causes possibles** :
- Distance du routeur
- Interférences
- Ancien standard WiFi (802.11g vs 802.11ac/ax)
- Canal encombré

**Solutions** :

1. **Vérifier le standard utilisé** :
```bash
iwconfig wlan0 | grep Rate
```

Si < 50 Mbps, vous utilisez probablement 802.11g ou 2.4GHz.

2. **Forcer 5GHz** (si disponible) :
   - Dans les paramètres de connexion WiFi
   - Certains routeurs ont des SSID séparés pour 2.4GHz et 5GHz
   - Connectez-vous au 5GHz

3. **Optimiser la position** :
   - Ligne de vue directe si possible
   - Évitez les murs épais, aquariums, micro-ondes

4. **Mettre à jour le firmware du routeur**

### WiFi non détecté après veille/hibernation

**Symptômes** :
- WiFi fonctionne au démarrage
- Après mise en veille, WiFi ne se reconnecte plus

**Solutions** :

1. **Script de reconnexion automatique** :
```bash
sudo nano /etc/systemd/system/wifi-resume.service
```

Contenu :
```ini
[Unit]
Description=Restart WiFi after resume  
After=suspend.target hibernate.target hybrid-sleep.target  

[Service]
Type=oneshot  
ExecStart=/bin/systemctl restart NetworkManager  

[Install]
WantedBy=suspend.target hibernate.target hybrid-sleep.target
```

Activer :
```bash
sudo systemctl enable wifi-resume.service
```

2. **Désactiver gestion d'énergie WiFi** (voir section connexion intermittente)

3. **Recharger le module WiFi** :
```bash
# Créer un script
sudo nano /lib/systemd/system-sleep/wifi-reload
```

Contenu :
```bash
#!/bin/sh
case $1 in
    post)
        modprobe -r iwlwifi  # Remplacez par votre module
        modprobe iwlwifi
        ;;
esac
```

Rendre exécutable :
```bash
sudo chmod +x /lib/systemd/system-sleep/wifi-reload
```

### Authentification WiFi échoue (WPA2-Enterprise)

Pour les réseaux d'entreprise avec authentification 802.1X :

1. **Via Network Manager** :
   - Paramètres réseau → Sécurité WiFi
   - Sécurité : WPA & WPA2 Enterprise
   - Authentication : PEAP (généralement)
   - CA certificate : Fourni par votre entreprise
   - PEAP version : Automatic
   - Inner authentication : MSCHAPv2
   - Username/Password : Vos identifiants

2. **Certificats** :
   - Importez les certificats fournis
   - Placez-les dans `/etc/ssl/certs/` ou `~/.cert/`

## Problèmes pare-feu

### Le pare-feu bloque la connexion

**Diagnostic** :

```bash
# Vérifier l'état du pare-feu
sudo ufw status

# Voir les règles détaillées
sudo ufw status numbered
```

**Solutions** :

1. **Désactiver temporairement pour tester** :
```bash
sudo ufw disable
# Testez votre connexion
# Si ça fonctionne, c'est le pare-feu
sudo ufw enable
```

2. **Autoriser le trafic nécessaire** :
```bash
# Autoriser trafic sortant (généralement déjà autorisé)
sudo ufw default allow outgoing

# Autoriser DNS
sudo ufw allow out 53

# Autoriser HTTP/HTTPS
sudo ufw allow out 80/tcp  
sudo ufw allow out 443/tcp  
```

3. **Logs du pare-feu** :
```bash
sudo ufw logging on  
sudo tail -f /var/log/ufw.log  
```

## Scripts de diagnostic automatique

### Script de diagnostic complet

```bash
#!/bin/bash
# diagnostic-reseau.sh

echo "===== DIAGNOSTIC RÉSEAU COMPLET ====="  
echo ""  

echo "1. Interfaces réseau :"  
ip link show  
echo ""  

echo "2. Adresses IP :"  
ip addr show  
echo ""  

echo "3. Table de routage :"  
ip route show  
echo ""  

echo "4. Serveurs DNS :"  
cat /etc/resolv.conf  
echo ""  

echo "5. Test ping passerelle :"  
GATEWAY=$(ip route | grep default | awk '{print $3}' | head -1)  
if [ -n "$GATEWAY" ]; then  
    ping -c 3 $GATEWAY
else
    echo "Pas de passerelle par défaut trouvée"
fi  
echo ""  

echo "6. Test ping Internet (8.8.8.8) :"  
ping -c 3 8.8.8.8  
echo ""  

echo "7. Test résolution DNS :"  
nslookup google.com  
echo ""  

echo "8. État WiFi :"  
nmcli radio all  
echo ""  

echo "9. Connexions actives :"  
nmcli connection show --active  
echo ""  

echo "10. État Network Manager :"  
systemctl status NetworkManager --no-pager  
echo ""  

echo "===== FIN DU DIAGNOSTIC ====="
```

Rendre exécutable et utiliser :
```bash
chmod +x diagnostic-reseau.sh
./diagnostic-reseau.sh > diagnostic-$(date +%Y%m%d-%H%M%S).txt
```

### Script de réparation automatique

```bash
#!/bin/bash
# reparer-reseau.sh

echo "Tentative de réparation du réseau..."

echo "1. Redémarrage Network Manager..."  
sudo systemctl restart NetworkManager  
sleep 5  

echo "2. Renouvellement DHCP..."  
sudo dhclient -r  
sudo dhclient  
sleep 3  

echo "3. Vérification DNS..."  
echo "nameserver 8.8.8.8" | sudo tee -a /etc/resolv.conf  
echo "nameserver 8.8.4.4" | sudo tee -a /etc/resolv.conf  

echo "4. Test de connexion..."  
if ping -c 3 8.8.8.8 > /dev/null 2>&1; then  
    echo "✓ Connexion Internet OK"
else
    echo "✗ Toujours pas de connexion"
    echo "Essayez de redémarrer l'ordinateur"
fi

echo "Réparation terminée."
```

### Script de surveillance réseau

```bash
#!/bin/bash
# surveiller-reseau.sh

while true; do
    clear
    date
    echo "================================"
    echo "Interface | État | Adresse IP"
    echo "================================"

    for iface in $(ip -o link show | awk -F': ' '{print $2}' | grep -v lo); do
        STATE=$(ip link show $iface | grep -oP '(?<=state )[^ ]+')
        IP=$(ip addr show $iface | grep -oP '(?<=inet )[^ ]+' | head -1)
        printf "%-10s | %-6s | %s\n" "$iface" "$STATE" "${IP:-Aucune}"
    done

    echo ""
    echo "Test ping vers 8.8.8.8 :"
    ping -c 1 -W 2 8.8.8.8 > /dev/null 2>&1
    if [ $? -eq 0 ]; then
        echo "✓ Internet accessible"
    else
        echo "✗ Pas d'Internet"
    fi

    sleep 5
done
```

## Journalisation et logs

### Logs Network Manager

```bash
# Logs en direct
journalctl -f -u NetworkManager

# Derniers logs
journalctl -u NetworkManager --since "1 hour ago"

# Logs d'aujourd'hui
journalctl -u NetworkManager --since today

# Chercher des erreurs
journalctl -u NetworkManager | grep -i error
```

### Logs système réseau

```bash
# Logs généraux
sudo tail -f /var/log/syslog | grep -i network

# Logs noyau (drivers, etc.)
sudo dmesg | grep -i network  
sudo dmesg | grep -i wifi  
sudo dmesg | grep -i eth  
```

### Activer logs détaillés Network Manager

```bash
sudo nano /etc/NetworkManager/NetworkManager.conf
```

Ajoutez :
```ini
[logging]
level=DEBUG  
domains=ALL  
```

Redémarrez :
```bash
sudo systemctl restart NetworkManager
```

**Attention** : Logs très verbeux, à désactiver après diagnostic.

## Commandes de réinitialisation

### Réinitialiser Network Manager

```bash
# Arrêter
sudo systemctl stop NetworkManager

# Supprimer l'état
sudo rm /var/lib/NetworkManager/NetworkManager.state

# Optionnel : supprimer les connexions enregistrées
# sudo rm /etc/NetworkManager/system-connections/*

# Redémarrer
sudo systemctl start NetworkManager
```

### Réinitialiser la pile réseau

```bash
# Supprimer toutes les règles iptables
sudo iptables -F  
sudo iptables -X  
sudo iptables -t nat -F  
sudo iptables -t nat -X  
sudo iptables -t mangle -F  
sudo iptables -t mangle -X  

# Réinitialiser les routes
sudo ip route flush table main  
sudo systemctl restart NetworkManager  
```

### Réinitialiser les paramètres réseau

```bash
# Supprimer la configuration
sudo rm -rf /etc/NetworkManager/system-connections/*  
sudo systemctl restart NetworkManager  

# Reconfigurer via l'interface graphique
```

## Obtenir de l'aide

### Informations à fournir lors d'une demande d'aide

Quand vous demandez de l'aide sur un forum :

1. **Votre distribution** :
```bash
cat /etc/lsb-release  
uname -r  
```

2. **Votre matériel réseau** :
```bash
lspci | grep -i network  
lspci | grep -i ethernet  
lsusb | grep -i wireless  
```

3. **Configuration réseau** :
```bash
ip addr show  
ip route show  
cat /etc/resolv.conf  
```

4. **Tests de base** :
```bash
ping -c 4 8.8.8.8  
ping -c 4 google.com  
```

5. **Logs récents** :
```bash
journalctl -u NetworkManager --since "1 hour ago" --no-pager
```

### Commande tout-en-un pour diagnostic

```bash
# Générer un rapport complet
{
    echo "=== INFORMATIONS SYSTÈME ==="
    cat /etc/lsb-release
    uname -a
    echo ""

    echo "=== MATÉRIEL RÉSEAU ==="
    lspci | grep -i network
    lspci | grep -i ethernet
    lsusb | grep -i wireless
    echo ""

    echo "=== CONFIGURATION ==="
    ip addr show
    ip route show
    cat /etc/resolv.conf
    echo ""

    echo "=== TESTS ==="
    echo "Ping passerelle :"
    ping -c 4 $(ip route | grep default | awk '{print $3}' | head -1)
    echo "Ping Internet :"
    ping -c 4 8.8.8.8
    echo "Résolution DNS :"
    ping -c 4 google.com
    echo ""

    echo "=== LOGS RÉCENTS ==="
    journalctl -u NetworkManager --since "30 minutes ago" --no-pager | tail -50

} > rapport-reseau-$(date +%Y%m%d-%H%M%S).txt

echo "Rapport sauvegardé dans rapport-reseau-*.txt"
```

## Résumé des commandes essentielles

```bash
# === DIAGNOSTIC DE BASE ===
ip addr show                                  # Voir les IP  
ip route show                                 # Voir les routes  
cat /etc/resolv.conf                         # Voir les DNS  
systemctl status NetworkManager               # État Network Manager  

# === TESTS DE CONNECTIVITÉ ===
ping -c 4 192.168.1.1                        # Ping passerelle  
ping -c 4 8.8.8.8                            # Ping Internet  
ping -c 4 google.com                         # Test DNS  
traceroute google.com                        # Tracer le chemin  
mtr google.com                               # Traceroute interactif  

# === GESTION NETWORK MANAGER ===
nmcli device status                          # État des appareils  
nmcli connection show                        # Voir connexions  
nmcli radio all                              # État WiFi/radio  
nmcli device wifi list                       # Lister WiFi disponibles  
sudo systemctl restart NetworkManager         # Redémarrer NM  

# === RENOUVELER DHCP ===
sudo dhclient -r                             # Libérer  
sudo dhclient                                # Renouveler  

# === WIFI ===
iwconfig                                     # Info WiFi  
nmcli radio wifi on                          # Activer WiFi  
nmcli radio wifi off                         # Désactiver WiFi  

# === SURVEILLANCE ===
ss -tuln                                     # Connexions actives  
sudo nethogs                                 # Bande passante par programme  
sudo iftop                                   # Trafic en temps réel  
wavemon                                      # Moniteur WiFi  

# === LOGS ===
journalctl -f -u NetworkManager              # Logs en direct  
sudo tail -f /var/log/syslog | grep network # Logs système  
dmesg | grep -i network                      # Logs noyau  

# === VITESSE ===
speedtest-cli                                # Test vitesse  
iperf3 -c serveur                           # Test vers serveur  

# === DNS ===
nslookup google.com                          # Test DNS  
dig google.com                               # Test DNS détaillé  
sudo systemd-resolve --flush-caches          # Vider cache DNS  
```

---

**Points clés à retenir** :
- Suivez une méthodologie systématique : identifier, vérifier, isoler, tester, résoudre
- Commencez toujours par les bases (câbles, WiFi activé, Network Manager)
- Utilisez `ping` pour tester la connectivité étape par étape
- `nmcli` est votre meilleur ami pour gérer les connexions
- Les problèmes DNS sont très courants - testez avec `ping 8.8.8.8` vs `ping google.com`
- Redémarrer Network Manager résout 80% des problèmes
- Gardez une trace des commandes qui ont fonctionné pour la prochaine fois
- Les logs (`journalctl -u NetworkManager`) contiennent souvent la solution
- Si bloqué, générez un rapport complet avant de demander de l'aide
- La plupart des problèmes ont des solutions simples - ne paniquez pas !

⏭️ [Cloud et synchronisation](/10-cloud-et-synchronisation/README.md)
