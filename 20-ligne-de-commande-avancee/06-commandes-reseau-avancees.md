🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Commandes réseau avancées (netstat, ss, ip)

## Introduction

Les commandes réseau sous Linux vous permettent de **voir**, **diagnostiquer** et **configurer** tout ce qui concerne votre connexion réseau. Que vous vouliez savoir quelle application utilise Internet, vérifier votre adresse IP, ou diagnostiquer un problème de connexion, ces outils sont indispensables.

### Pourquoi apprendre ces commandes ?

- **Diagnostic** : Identifier les problèmes de connexion
- **Sécurité** : Voir quelles applications communiquent sur le réseau
- **Performance** : Analyser l'utilisation du réseau
- **Configuration** : Configurer vos interfaces réseau
- **Surveillance** : Monitorer les connexions en temps réel

### Évolution des outils réseau

Les outils réseau Linux ont évolué :

| Ancienne commande | Nouvelle commande | Statut |
|-------------------|-------------------|--------|
| `ifconfig` | `ip` | ifconfig est obsolète |
| `netstat` | `ss` | netstat est obsolète |
| `route` | `ip route` | route est obsolète |
| `arp` | `ip neigh` | arp est obsolète |

**Note** : Les anciennes commandes fonctionnent encore, mais les nouvelles sont plus puissantes et maintenues.

---

## Concepts de base du réseau

Avant de plonger dans les commandes, quelques concepts essentiels :

### Adresse IP

Une **adresse IP** est comme l'adresse postale de votre ordinateur sur le réseau.

- **IPv4** : Format classique (ex: `192.168.1.10`)
- **IPv6** : Format moderne (ex: `2001:0db8:85a3::8a2e:0370:7334`)

### Localhost et 127.0.0.1

- **127.0.0.1** : Adresse spéciale qui désigne votre propre ordinateur
- **localhost** : Nom associé à 127.0.0.1
- Utilisé pour tester des services locaux

### Ports

Les **ports** sont comme des portes d'entrée numérotées (de 0 à 65535) :

- **Port 80** : HTTP (sites web non sécurisés)
- **Port 443** : HTTPS (sites web sécurisés)
- **Port 22** : SSH (connexion à distance sécurisée)
- **Port 25** : SMTP (envoi email)
- **Port 3306** : MySQL (base de données)

### Interfaces réseau

Une **interface réseau** est un point de connexion réseau :

- **eth0, enp3s0** : Connexion Ethernet (câble)
- **wlan0, wlp2s0** : Connexion WiFi
- **lo** : Loopback (localhost)

### États de connexion

- **ESTABLISHED** : Connexion active
- **LISTEN** : En écoute (attend des connexions)
- **TIME_WAIT** : Connexion en cours de fermeture
- **CLOSE_WAIT** : En attente de fermeture

---

## La commande ip - Outil moderne de configuration réseau

La commande `ip` est l'outil moderne pour gérer votre réseau sous Linux. Elle remplace `ifconfig`, `route`, `arp` et d'autres.

### Afficher toutes les interfaces réseau

```bash
ip link show
# ou plus court
ip link
# ou encore plus court
ip l
```

**Exemple de sortie** :
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP
3: wlp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP
```

**Explication** :
- `lo` : Interface loopback (localhost)
- `enp3s0` : Interface Ethernet
- `wlp2s0` : Interface WiFi
- `UP` : Interface activée
- `state UP` : Interface connectée

### Afficher les adresses IP

```bash
ip address show
# ou
ip addr
# ou
ip a
```

**Exemple de sortie** :
```
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500
    inet 192.168.1.100/24 brd 192.168.1.255 scope global dynamic enp3s0
    inet6 fe80::a00:27ff:fe4e:66a1/64 scope link
```

**Informations importantes** :
- `inet 192.168.1.100/24` : Adresse IPv4
- `/24` : Masque de sous-réseau (255.255.255.0)
- `brd 192.168.1.255` : Adresse de broadcast

### Afficher une interface spécifique

```bash
# Pour l'interface WiFi
ip addr show wlp2s0

# Pour l'interface Ethernet
ip addr show enp3s0
```

### Afficher uniquement les adresses IPv4

```bash
ip -4 addr
```

### Afficher uniquement les adresses IPv6

```bash
ip -6 addr
```

### Afficher de manière colorée

```bash
ip -c addr
# Le -c ajoute des couleurs pour faciliter la lecture
```

### Activer/Désactiver une interface

```bash
# Désactiver une interface
sudo ip link set enp3s0 down

# Activer une interface
sudo ip link set enp3s0 up
```

### Afficher les statistiques réseau

```bash
# Statistiques par interface
ip -s link

# Statistiques détaillées
ip -s -s link
```

**Exemple de sortie** :
```
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    RX: bytes  packets  errors  dropped overrun mcast
    1234567    8901     0       0       0       123
    TX: bytes  packets  errors  dropped carrier collsns
    2345678    9012     0       0       0       0
```

**Explication** :
- **RX** : Données reçues (received)
- **TX** : Données transmises (transmitted)
- **errors** : Erreurs de transmission
- **dropped** : Paquets perdus

### Table de routage

```bash
# Afficher la table de routage
ip route show
# ou
ip route
# ou
ip r
```

**Exemple de sortie** :
```
default via 192.168.1.1 dev enp3s0 proto dhcp metric 100
192.168.1.0/24 dev enp3s0 proto kernel scope link src 192.168.1.100
```

**Explication** :
- `default via 192.168.1.1` : Passerelle par défaut (routeur)
- `dev enp3s0` : Via l'interface enp3s0
- `192.168.1.0/24` : Réseau local

### Ajouter une route (avancé)

```bash
# Ajouter une route vers un réseau
sudo ip route add 10.0.0.0/24 via 192.168.1.254

# Supprimer une route
sudo ip route del 10.0.0.0/24
```

### Table ARP (voisins réseau)

```bash
# Afficher les voisins (cache ARP)
ip neigh show
# ou
ip neigh
# ou
ip n
```

**Exemple de sortie** :
```
192.168.1.1 dev enp3s0 lladdr 00:11:22:33:44:55 REACHABLE
192.168.1.50 dev enp3s0 lladdr aa:bb:cc:dd:ee:ff STALE
```

**Explication** :
- `192.168.1.1` : Adresse IP du voisin
- `lladdr 00:11:22:33:44:55` : Adresse MAC
- `REACHABLE` : Accessible actuellement
- `STALE` : Entrée ancienne

### Surveiller les événements réseau en temps réel

```bash
# Surveiller les changements réseau
ip monitor

# Surveiller uniquement les changements de lien
ip monitor link

# Surveiller uniquement les changements d'adresse
ip monitor address
```

Appuyez sur `Ctrl+C` pour arrêter.

---

## La commande ss - Socket Statistics

`ss` est l'outil moderne pour afficher les informations sur les sockets réseau. Il remplace `netstat` et est beaucoup plus rapide.

### Afficher toutes les connexions

```bash
# Toutes les connexions (TCP, UDP, etc.)
ss

# Version plus lisible avec en-têtes
ss -a
```

**Note** : La sortie peut être très longue !

### Afficher les connexions TCP

```bash
# Connexions TCP établies
ss -t

# Toutes les connexions TCP (y compris en écoute)
ss -ta
```

### Afficher les connexions UDP

```bash
# Connexions UDP
ss -u

# Toutes les connexions UDP
ss -ua
```

### Afficher les sockets en écoute (LISTEN)

```bash
# Tous les services en écoute
ss -l

# Seulement TCP en écoute
ss -lt

# Seulement UDP en écoute
ss -lu
```

**Exemple de sortie** :
```
State    Recv-Q   Send-Q     Local Address:Port       Peer Address:Port  
LISTEN   0        128        0.0.0.0:22                0.0.0.0:*  
LISTEN   0        128        127.0.0.1:631             0.0.0.0:*  
LISTEN   0        5          127.0.0.1:5432            0.0.0.0:*  
```

**Explication** :
- Port 22 : SSH en écoute sur toutes les interfaces
- Port 631 : CUPS (impression) en écoute sur localhost
- Port 5432 : PostgreSQL en écoute sur localhost

### Afficher les numéros de ports

```bash
# Afficher les numéros au lieu des noms de services
ss -tn

# Afficher tout avec numéros
ss -tan
```

### Afficher les processus associés

```bash
# Afficher quel programme utilise chaque socket
sudo ss -tp

# Afficher tout avec processus
sudo ss -tap
```

**Exemple de sortie** :
```
State    Recv-Q   Send-Q     Local Address:Port    Peer Address:Port    Process  
ESTAB    0        0          192.168.1.100:45678   93.184.216.34:443   users:(("firefox",pid=1234,fd=45))  
```

**Explication** :
- Firefox (PID 1234) a une connexion établie vers un serveur web (port 443)

### Filtrer par état

```bash
# Seulement les connexions établies
ss -t state established

# Seulement les connexions en attente de fermeture
ss -t state close-wait

# Connexions en SYN-SENT (en cours d'établissement)
ss -t state syn-sent
```

### Filtrer par port

```bash
# Connexions sur le port 80
ss -tan '( sport = :80 )'

# Connexions depuis le port 443
ss -tan '( dport = :443 )'

# Connexions sur les ports 80 ou 443
ss -tan '( sport = :80 or sport = :443 )'
```

### Afficher les statistiques réseau

```bash
# Statistiques globales
ss -s
```

**Exemple de sortie** :
```
Total: 587  
TCP:   12 (estab 3, closed 1, orphaned 0, timewait 1)  
UDP:   8  
RAW:   1  
```

### Afficher avec informations étendues

```bash
# Informations détaillées sur chaque connexion
ss -te

# Informations mémoire
ss -tm

# Informations sur les timers
ss -to
```

### Surveiller les connexions en temps réel

```bash
# Afficher les nouvelles connexions toutes les 2 secondes
watch -n 2 'ss -tan'
```

### Exemples pratiques avec ss

```bash
# Voir tous les programmes qui utilisent Internet
sudo ss -tp

# Voir qui utilise le port 80 (serveur web)
sudo ss -tlnp | grep :80

# Compter les connexions par état
ss -tan | awk '{print $1}' | sort | uniq -c

# Voir toutes les connexions vers un serveur spécifique
ss -tan dst 93.184.216.34

# Voir toutes les connexions depuis votre IP
ss -tan src 192.168.1.100
```

---

## La commande netstat - Ancienne mais encore utile

`netstat` est l'ancienne commande pour voir les connexions réseau. Bien qu'obsolète, elle est encore largement utilisée et disponible.

**Note** : Sur Linux Mint moderne, vous devrez peut-être installer netstat :
```bash
sudo apt install net-tools
```

### Afficher toutes les connexions

```bash
# Toutes les connexions et sockets en écoute
netstat -a

# Toutes les connexions TCP
netstat -at

# Toutes les connexions UDP
netstat -au
```

### Afficher les sockets en écoute

```bash
# Tous les services en écoute
netstat -l

# Seulement TCP en écoute
netstat -lt

# Seulement UDP en écoute
netstat -lu
```

### Afficher avec numéros de ports

```bash
# Afficher les ports numériques (plus rapide)
netstat -n

# TCP avec numéros
netstat -tn

# Tout avec numéros
netstat -an
```

### Afficher les processus

```bash
# Afficher les programmes associés
sudo netstat -p

# TCP avec programmes
sudo netstat -tp

# Tout avec programmes
sudo netstat -ap
```

### Afficher les statistiques

```bash
# Statistiques par protocole
netstat -s

# Statistiques TCP uniquement
netstat -st

# Statistiques UDP uniquement
netstat -su
```

### Afficher la table de routage

```bash
# Table de routage
netstat -r

# Ou avec détails numériques
netstat -rn
```

### Combinaison la plus utile

```bash
# TCP + listening + numeric + program
sudo netstat -tlnp

# Toutes connexions + numeric + program
sudo netstat -tanp
```

### Exemples pratiques avec netstat

```bash
# Voir tous les programmes qui écoutent
sudo netstat -tlnp

# Voir toutes les connexions établies
netstat -tan | grep ESTABLISHED

# Compter les connexions par état
netstat -tan | awk '{print $6}' | sort | uniq -c

# Voir qui écoute sur le port 80
sudo netstat -tlnp | grep :80
```

---

## Autres commandes réseau essentielles

### ping - Tester la connectivité

```bash
# Ping basique (Ctrl+C pour arrêter)
ping google.com

# Envoyer seulement 4 paquets
ping -c 4 google.com

# Ping plus rapide (intervalle de 0.2s)
ping -i 0.2 google.com

# Ping avec timestamp
ping -D google.com
```

**Interprétation** :
```
64 bytes from 142.250.185.46: icmp_seq=1 ttl=117 time=12.3 ms
```
- `time=12.3 ms` : Temps de réponse (latence)
- `ttl=117` : Time To Live (nombre de sauts réseau restants)

### traceroute - Tracer le chemin réseau

```bash
# Installer si nécessaire
sudo apt install traceroute

# Tracer le chemin vers google.com
traceroute google.com

# Version plus rapide (pas d'attente)
traceroute -n google.com
```

**Exemple de sortie** :
```
 1  192.168.1.1 (192.168.1.1)  1.234 ms
 2  10.0.0.1 (10.0.0.1)  5.678 ms
 3  * * *
 4  142.250.185.46 (142.250.185.46)  12.345 ms
```

Chaque ligne = un "saut" (routeur) entre vous et la destination.

### dig - Requêtes DNS

```bash
# Installer si nécessaire
sudo apt install dnsutils

# Résolution DNS simple
dig google.com

# Seulement la réponse courte
dig +short google.com

# Requête DNS inverse (IP → nom)
dig -x 8.8.8.8

# Spécifier un serveur DNS
dig @8.8.8.8 google.com

# Afficher seulement la section réponse
dig google.com +noall +answer
```

### host - Résolution DNS simple

```bash
# Résoudre un nom de domaine
host google.com

# Résolution inverse
host 8.8.8.8

# Tout afficher
host -a google.com
```

### nslookup - Autre outil DNS

```bash
# Résolution simple
nslookup google.com

# Utiliser un serveur DNS spécifique
nslookup google.com 8.8.8.8

# Mode interactif
nslookup
> google.com
> exit
```

### wget - Télécharger des fichiers

```bash
# Télécharger un fichier
wget https://example.com/file.zip

# Télécharger en arrière-plan
wget -b https://example.com/file.zip

# Continuer un téléchargement interrompu
wget -c https://example.com/file.zip

# Télécharger avec un autre nom
wget -O nouveau_nom.zip https://example.com/file.zip
```

### curl - Outil HTTP polyvalent

```bash
# Afficher le contenu d'une page
curl https://example.com

# Sauvegarder dans un fichier
curl -o page.html https://example.com

# Suivre les redirections
curl -L https://example.com

# Afficher les en-têtes HTTP
curl -I https://example.com

# Télécharger avec progression
curl -O https://example.com/file.zip

# Tester une API
curl -X GET https://api.example.com/data
```

### nc (netcat) - Couteau suisse réseau

```bash
# Tester si un port est ouvert
nc -zv google.com 80

# Scanner une plage de ports
nc -zv google.com 20-100

# Créer un serveur simple (écoute sur port 1234)
nc -l 1234

# Se connecter à un serveur
nc localhost 1234
```

### iftop - Moniteur de bande passante en temps réel

```bash
# Installer
sudo apt install iftop

# Lancer (nécessite sudo)
sudo iftop

# Interface spécifique
sudo iftop -i wlp2s0
```

Appuyez sur :
- `q` : Quitter
- `n` : Désactiver la résolution DNS
- `t` : Changer le mode d'affichage

### nethogs - Voir qui utilise la bande passante

```bash
# Installer
sudo apt install nethogs

# Lancer
sudo nethogs

# Interface spécifique
sudo nethogs wlp2s0
```

Affiche la bande passante utilisée par chaque programme.

### tcpdump - Capturer le trafic réseau

```bash
# Installer
sudo apt install tcpdump

# Capturer sur toutes les interfaces
sudo tcpdump

# Interface spécifique
sudo tcpdump -i enp3s0

# Capturer seulement le port 80
sudo tcpdump port 80

# Sauvegarder dans un fichier
sudo tcpdump -w capture.pcap

# Lire un fichier de capture
tcpdump -r capture.pcap
```

**Attention** : Génère beaucoup de données ! Utilisez avec précaution.

### nmap - Scanner de ports

```bash
# Installer
sudo apt install nmap

# Scanner les ports courants
nmap localhost

# Scanner une plage d'IP
nmap 192.168.1.0/24

# Détecter l'OS
sudo nmap -O 192.168.1.1

# Scanner tous les ports
nmap -p- localhost
```

**Note** : Utilisez nmap uniquement sur vos propres systèmes !

---

## Cas d'usage pratiques

### Diagnostic 1 : Vérifier la connectivité Internet

```bash
# 1. Vérifier si l'interface est UP
ip link show

# 2. Vérifier si on a une IP
ip addr show

# 3. Tester la passerelle (routeur)
ping -c 4 192.168.1.1

# 4. Tester un DNS
ping -c 4 8.8.8.8

# 5. Tester la résolution DNS
ping -c 4 google.com
```

### Diagnostic 2 : Identifier un programme qui utilise un port

```bash
# Voir quel programme écoute sur le port 8080
sudo ss -tlnp | grep :8080

# Ou avec netstat
sudo netstat -tlnp | grep :8080

# Ou avec lsof
sudo lsof -i :8080
```

### Diagnostic 3 : Trouver pourquoi une connexion est lente

```bash
# 1. Tester la latence
ping -c 10 google.com

# 2. Tracer le chemin réseau
traceroute google.com

# 3. Voir qui utilise la bande passante
sudo nethogs

# 4. Voir les connexions actives
ss -tan | grep ESTABLISHED | wc -l
```

### Diagnostic 4 : Vérifier un serveur web local

```bash
# 1. Vérifier que le serveur écoute
sudo ss -tlnp | grep :80

# 2. Tester localement
curl http://localhost

# 3. Vérifier depuis l'extérieur
curl http://votre_ip_publique

# 4. Voir les connexions actives
sudo ss -tn dst :80
```

### Diagnostic 5 : Problème de DNS

```bash
# 1. Vérifier quel DNS est utilisé
cat /etc/resolv.conf

# 2. Tester la résolution
dig google.com

# 3. Tester avec un autre DNS
dig @8.8.8.8 google.com

# 4. Comparer les temps de réponse
time nslookup google.com  
time nslookup google.com 8.8.8.8  
```

### Surveillance : Connexions suspectes

```bash
# Voir toutes les connexions établies vers l'extérieur
sudo ss -tnp | grep ESTABLISHED

# Compter les connexions par IP distante
ss -tan | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -rn

# Voir les programmes qui ont des connexions actives
sudo ss -tp | grep -i established
```

### Configuration : Changer temporairement son IP

```bash
# Voir l'IP actuelle
ip addr show enp3s0

# Supprimer l'IP actuelle
sudo ip addr del 192.168.1.100/24 dev enp3s0

# Ajouter une nouvelle IP
sudo ip addr add 192.168.1.200/24 dev enp3s0

# Redémarrer l'interface pour revenir à la normale
sudo ip link set enp3s0 down  
sudo ip link set enp3s0 up  
```

**Note** : Ces changements sont temporaires et disparaissent au redémarrage.

---

## Scripts utiles pour le réseau

### Script : Vérification réseau complète

```bash
#!/bin/bash
# check-network.sh - Diagnostic réseau complet

echo "======================================"  
echo "  DIAGNOSTIC RÉSEAU COMPLET"  
echo "======================================"  
echo ""  

# Interfaces réseau
echo "=== INTERFACES RÉSEAU ==="  
ip -c -br addr  
echo ""  

# Passerelle par défaut
echo "=== PASSERELLE PAR DÉFAUT ==="  
ip route | grep default  
echo ""  

# DNS
echo "=== SERVEURS DNS ==="  
cat /etc/resolv.conf | grep nameserver  
echo ""  

# Test de connectivité
echo "=== TEST DE CONNECTIVITÉ ==="  
echo -n "Passerelle : "  
if ping -c 1 -W 2 $(ip route | grep default | awk '{print $3}') &>/dev/null; then  
    echo "✅ OK"
else
    echo "❌ ÉCHEC"
fi

echo -n "DNS Google : "  
if ping -c 1 -W 2 8.8.8.8 &>/dev/null; then  
    echo "✅ OK"
else
    echo "❌ ÉCHEC"
fi

echo -n "Résolution DNS : "  
if ping -c 1 -W 2 google.com &>/dev/null; then  
    echo "✅ OK"
else
    echo "❌ ÉCHEC"
fi  
echo ""  

# Connexions actives
echo "=== CONNEXIONS ACTIVES ==="  
echo "Nombre de connexions établies : $(ss -tan | grep ESTABLISHED | wc -l)"  
echo ""  

# Ports en écoute
echo "=== PORTS EN ÉCOUTE (TOP 5) ==="  
sudo ss -tlnp | grep LISTEN | head -5  
echo ""  

echo "======================================"
```

### Script : Surveiller les connexions

```bash
#!/bin/bash
# monitor-connections.sh - Surveillance des connexions

while true; do
    clear
    echo "=== CONNEXIONS RÉSEAU - $(date) ==="
    echo ""

    echo "Programmes utilisant le réseau :"
    sudo ss -tp | grep ESTAB | awk '{print $NF}' | sed 's/.*("//' | sed 's/".*//' | sort | uniq -c | sort -rn

    echo ""
    echo "Nombre de connexions par état :"
    ss -tan | awk '{print $1}' | sort | uniq -c

    sleep 5
done
```

### Script : Tester les ports ouverts

```bash
#!/bin/bash
# scan-ports.sh - Scanner les ports locaux

HOST=${1:-localhost}

echo "Scan des ports courants sur $HOST..."  
echo ""  

PORTS=(20 21 22 25 53 80 110 143 443 465 587 993 995 3306 5432 8080)

for PORT in "${PORTS[@]}"; do
    timeout 1 bash -c "echo >/dev/tcp/$HOST/$PORT" 2>/dev/null
    if [ $? -eq 0 ]; then
        SERVICE=$(grep -w "$PORT/tcp" /etc/services | awk '{print $1}' | head -1)
        echo "✅ Port $PORT ouvert - $SERVICE"
    fi
done

echo ""  
echo "Scan terminé"  
```

### Script : Afficher son IP publique

```bash
#!/bin/bash
# mon-ip.sh - Afficher son IP publique

echo "=== VOS ADRESSES IP ==="  
echo ""  

echo "IP publique :"  
curl -s https://api.ipify.org  
echo ""  
echo ""  

echo "IP locale :"  
ip -4 addr show | grep -oP '(?<=inet\s)\d+(\.\d+){3}' | grep -v 127.0.0.1  
echo ""  

echo "Informations détaillées :"  
curl -s https://ipinfo.io/json | grep -E '(ip|city|region|country)' | sed 's/[",]//g'  
```

---

## Fichiers de configuration réseau importants

### /etc/resolv.conf - Configuration DNS

```bash
# Voir les serveurs DNS utilisés
cat /etc/resolv.conf
```

Exemple :
```
nameserver 8.8.8.8  
nameserver 8.8.4.4  
```

### /etc/hosts - Associations IP/noms locaux

```bash
# Voir les associations
cat /etc/hosts
```

Exemple :
```
127.0.0.1   localhost
192.168.1.10   mon-serveur
```

Vous pouvez ajouter vos propres associations :
```bash
sudo nano /etc/hosts
# Ajouter : 192.168.1.100   dev.local
```

### /etc/network/interfaces - Configuration réseau (Debian)

Sur certains systèmes :
```bash
cat /etc/network/interfaces
```

### /etc/netplan/ - Configuration réseau (Ubuntu/Mint moderne)

```bash
# Voir les fichiers de configuration
ls /etc/netplan/

# Voir la configuration
cat /etc/netplan/*.yaml
```

---

## Dépannage réseau - Guide pas à pas

### Problème : Pas de connexion Internet

**Étape 1** : Vérifier l'interface
```bash
ip link show
# L'interface doit être UP
```

Si DOWN :
```bash
sudo ip link set enp3s0 up
```

**Étape 2** : Vérifier l'adresse IP
```bash
ip addr show
# Vous devez avoir une IP (pas seulement 127.0.0.1)
```

Si pas d'IP :
```bash
sudo dhclient enp3s0
```

**Étape 3** : Tester la passerelle
```bash
ip route
# Noter l'IP de la passerelle (après "default via")

ping -c 4 192.168.1.1  # Remplacer par votre passerelle
```

**Étape 4** : Tester DNS
```bash
ping -c 4 8.8.8.8
# Si ça marche, problème DNS
# Si ça ne marche pas, problème réseau
```

**Étape 5** : Tester la résolution DNS
```bash
ping -c 4 google.com
```

### Problème : Port déjà utilisé

```bash
# Identifier qui utilise le port 8080
sudo ss -tlnp | grep :8080

# Ou
sudo lsof -i :8080

# Tuer le processus si nécessaire
sudo kill <PID>
```

### Problème : Connexion très lente

```bash
# 1. Tester la latence
ping google.com
# Si time > 100ms, c'est lent

# 2. Vérifier qui utilise la bande passante
sudo nethogs

# 3. Voir les connexions actives
ss -tan | grep ESTABLISHED | wc -l
# Si > 1000, peut-être un problème

# 4. Vérifier les erreurs réseau
ip -s link
# Regarder la ligne "errors"
```

### Problème : Cannot assign requested address

```bash
# L'IP que vous essayez d'utiliser n'est pas disponible
# Vérifier les IP disponibles :
ip addr show

# Vérifier la configuration réseau
cat /etc/netplan/*.yaml
```

---

## Tableaux récapitulatifs

### Commandes de base par objectif

| Objectif | Commande moderne | Ancienne commande |
|----------|------------------|-------------------|
| Voir les interfaces | `ip link` | `ifconfig` |
| Voir les IP | `ip addr` | `ifconfig` |
| Voir la route | `ip route` | `route -n` |
| Voir les connexions | `ss -tan` | `netstat -tan` |
| Voir qui écoute | `ss -tlnp` | `netstat -tlnp` |
| Voir les voisins | `ip neigh` | `arp -a` |

### Ports courants à connaître

| Port | Service | Description |
|------|---------|-------------|
| 20/21 | FTP | Transfert de fichiers |
| 22 | SSH | Connexion à distance sécurisée |
| 23 | Telnet | Connexion non sécurisée (obsolète) |
| 25 | SMTP | Envoi email |
| 53 | DNS | Résolution de noms |
| 80 | HTTP | Sites web non sécurisés |
| 110 | POP3 | Réception email |
| 143 | IMAP | Réception email (moderne) |
| 443 | HTTPS | Sites web sécurisés |
| 3306 | MySQL | Base de données MySQL |
| 5432 | PostgreSQL | Base de données PostgreSQL |
| 8080 | HTTP alt | Serveur web alternatif |

### États de connexion TCP

| État | Signification |
|------|---------------|
| LISTEN | En attente de connexions |
| SYN-SENT | Tentative de connexion |
| SYN-RECEIVED | Connexion en cours |
| ESTABLISHED | Connexion active |
| FIN-WAIT-1 | Fermeture initiée |
| FIN-WAIT-2 | Attente de fermeture |
| CLOSE-WAIT | En attente de fermeture |
| CLOSING | Fermeture simultanée |
| LAST-ACK | Dernière confirmation |
| TIME-WAIT | Attente avant réutilisation |
| CLOSED | Fermée |

---

## Bonnes pratiques et conseils

### 1. Utiliser les commandes modernes

✅ **Préférez** :
```bash
ip addr  
ss -tan  
ip route  
```

❌ **Évitez** :
```bash
ifconfig  
netstat -tan  
route -n  
```

### 2. Toujours vérifier avec sudo pour voir tous les processus

```bash
# ❌ Ne montrera pas tous les processus
ss -tp

# ✅ Montre tous les processus
sudo ss -tp
```

### 3. Utiliser les couleurs pour plus de lisibilité

```bash
ip -c addr  
ss -c  
```

### 4. Sauvegarder les configurations avant modification

```bash
# Avant de modifier la config réseau
sudo cp /etc/netplan/01-netcfg.yaml /etc/netplan/01-netcfg.yaml.bak
```

### 5. Tester progressivement

```bash
# Ne pas tout changer d'un coup
# Tester étape par étape :
ping routeur  → OK  
ping 8.8.8.8  → OK  
ping google.com → OK  
```

### 6. Documenter vos configurations

```bash
# Créer un fichier de notes
nano ~/network-config.txt
# Y noter vos IP, masques, passerelles, etc.
```

### 7. Utiliser des alias pour les commandes fréquentes

Ajoutez à `~/.bashrc` :
```bash
alias myip='ip -c -br addr'  
alias ports='sudo ss -tlnp'  
alias conns='ss -tan | grep ESTABLISHED'  
```

---

## Aide-mémoire rapide

### Commandes essentielles

```bash
# Voir mon IP
ip addr show

# Voir ma connexion
ip -c -br link

# Tester Internet
ping -c 4 google.com

# Voir qui utilise Internet
sudo ss -tp

# Voir les ports ouverts
sudo ss -tlnp

# Voir la passerelle
ip route

# Voir les DNS
cat /etc/resolv.conf

# Résoudre un nom
dig google.com +short

# Voir toutes les connexions
ss -tan

# Statistiques réseau
ss -s
```

---

## Ressources pour aller plus loin

### Documentation

```bash
man ip  
man ss  
man netstat  
man ping  
man dig  
```

### Sites web

- **iproute2** : [https://wiki.linuxfoundation.org/networking/iproute2](https://wiki.linuxfoundation.org/networking/iproute2)
- **ss manual** : [https://man7.org/linux/man-pages/man8/ss.8.html](https://man7.org/linux/man-pages/man8/ss.8.html)

### Livres recommandés

- "TCP/IP Illustrated" par W. Richard Stevens
- "Linux Network Administrator's Guide"

---

## Conclusion

Les commandes réseau sont essentielles pour tout utilisateur Linux qui veut :

- ✅ **Diagnostiquer** les problèmes de connexion
- ✅ **Surveiller** l'utilisation du réseau
- ✅ **Sécuriser** son système en voyant qui communique
- ✅ **Optimiser** les performances réseau
- ✅ **Comprendre** ce qui se passe sur son ordinateur

**Points clés à retenir** :

- **ip** remplace ifconfig, route, arp
- **ss** remplace netstat (plus rapide et plus complet)
- Utilisez `sudo` pour voir tous les processus
- Testez progressivement en cas de problème
- Les commandes modernes sont plus puissantes

**Progression recommandée** :

1. Maîtrisez `ip addr` et `ip route`
2. Apprenez `ss -tan` et `ss -tlnp`
3. Pratiquez `ping`, `dig`, `curl`
4. Explorez les outils de surveillance (iftop, nethogs)
5. Créez vos propres scripts de diagnostic

Avec ces outils, vous avez tout ce qu'il faut pour gérer et diagnostiquer votre réseau sous Linux ! 🌐🚀

**Un dernier conseil** : Gardez à portée un script de diagnostic réseau complet (comme celui présenté) - il vous sauvera la mise plus d'une fois ! 😊

⏭️ [Serveurs et administration système](/21-serveurs-et-administration-systeme/README.md)
