🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 9. Configuration réseau et Internet

## Introduction au chapitre

La configuration réseau est l'un des aspects les plus importants de l'utilisation d'un ordinateur moderne. Que vous souhaitiez simplement naviguer sur Internet, travailler à distance, partager des fichiers avec d'autres appareils, ou sécuriser vos communications, une bonne compréhension des réseaux est essentielle.

Ce chapitre vous guidera à travers tous les aspects de la configuration réseau sous Linux Mint, depuis les bases (connexion WiFi et Ethernet) jusqu'aux configurations avancées (VPN, SSH, partage de fichiers). Que vous soyez débutant ou utilisateur intermédiaire, vous trouverez ici toutes les informations nécessaires pour maîtriser votre réseau.

## Pourquoi ce chapitre est important

### Pour tous les utilisateurs

**Connectivité de base** :
- Se connecter à Internet (WiFi, Ethernet)
- Résoudre les problèmes de connexion courants
- Comprendre pourquoi votre connexion ne fonctionne pas

**Sécurité** :
- Protéger votre ordinateur avec un pare-feu
- Utiliser un VPN pour sécuriser vos communications
- Naviguer en toute sécurité sur les réseaux publics

**Partage et collaboration** :
- Partager votre connexion Internet avec d'autres appareils
- Échanger des fichiers en réseau local
- Accéder à votre ordinateur à distance

### Pour les utilisateurs avancés

**Administration à distance** :
- Contrôler des serveurs via SSH
- Configurer des services réseau
- Automatiser des tâches réseau

**Optimisation** :
- Améliorer les performances réseau
- Diagnostiquer et résoudre des problèmes complexes
- Configurer des réseaux d'entreprise

## Prérequis

Ce chapitre suppose que vous :
- Avez installé Linux Mint avec succès
- Êtes à l'aise avec l'interface graphique
- Connaissez les bases du terminal (pour certaines sections avancées)
- Avez lu les chapitres 1 à 4 (bases de Linux Mint)

**Matériel nécessaire** :
- Une connexion Internet (via WiFi ou Ethernet)
- Pour certaines sections : plusieurs ordinateurs pour tester le partage/réseau

## Vue d'ensemble du chapitre

Ce chapitre est divisé en 8 sections principales, organisées de manière progressive : des bases vers les configurations avancées.

### Section 9.1 : Configuration WiFi et Ethernet

**Ce que vous apprendrez** :
- Comment vous connecter à un réseau WiFi
- Configuration des connexions filaires (Ethernet)
- Gestion des réseaux WiFi enregistrés
- Configuration avancée (IP fixe, DNS personnalisés)
- Résolution des problèmes de connexion courants

**Pour qui** : Tous les utilisateurs, débutants inclus

**Temps estimé** : 20-30 minutes de lecture

Cette section est fondamentale car elle couvre la manière la plus courante de se connecter à Internet. Vous apprendrez à gérer vos connexions réseau via l'interface graphique intuitive de Linux Mint, ainsi qu'à résoudre les problèmes les plus fréquents.

### Section 9.2 : Partage de connexion

**Ce que vous apprendrez** :
- Créer un point d'accès WiFi (hotspot)
- Partager votre connexion Internet en WiFi
- Partage via câble Ethernet
- Partage de connexion USB (smartphone)
- Sécuriser votre point d'accès

**Pour qui** : Utilisateurs de niveau débutant à intermédiaire

**Temps estimé** : 25-35 minutes de lecture

Cette section vous montre comment transformer votre ordinateur Linux Mint en point d'accès pour partager votre connexion Internet avec d'autres appareils. Très utile en voyage ou quand votre routeur est en panne.

### Section 9.3 : Pare-feu (UFW/GUFW)

**Ce que vous apprendrez** :
- Comprendre ce qu'est un pare-feu et pourquoi c'est important
- Utiliser GUFW (interface graphique)
- Maîtriser UFW en ligne de commande
- Créer des règles de pare-feu personnalisées
- Sécuriser votre système contre les intrusions

**Pour qui** : Tous les utilisateurs (essentiel pour la sécurité)

**Temps estimé** : 30-40 minutes de lecture

La sécurité est primordiale, et le pare-feu est votre première ligne de défense. Cette section démystifie les pare-feu et vous montre comment protéger efficacement votre système, même si vous êtes débutant.

### Section 9.4 : Configuration VPN

**Ce que vous apprendrez** :
- Comprendre les VPN et leur utilité
- Configurer un VPN commercial (NordVPN, ProtonVPN, etc.)
- Configurer un VPN d'entreprise
- Utiliser WireGuard et OpenVPN
- Vérifier que votre VPN fonctionne correctement
- Sécuriser votre navigation sur les réseaux publics

**Pour qui** : Utilisateurs soucieux de la vie privée et de la sécurité

**Temps estimé** : 35-45 minutes de lecture

Les VPN sont devenus essentiels pour protéger sa vie privée en ligne et accéder à des ressources à distance. Cette section couvre aussi bien l'utilisation de VPN commerciaux que la configuration de VPN professionnels.

### Section 9.5 : SSH pour connexions à distance

**Ce que vous apprendrez** :
- Comprendre SSH et son utilisation
- Se connecter à distance à un autre ordinateur
- Utiliser l'authentification par clés SSH
- Transférer des fichiers via SCP/SFTP/rsync
- Créer des tunnels SSH sécurisés
- Sécuriser votre serveur SSH

**Pour qui** : Utilisateurs intermédiaires à avancés, administrateurs système

**Temps estimé** : 45-60 minutes de lecture

SSH est l'outil indispensable pour l'administration à distance. Cette section complète vous apprendra à maîtriser SSH pour contrôler des machines distantes, transférer des fichiers de manière sécurisée, et créer des tunnels chiffrés.

### Section 9.6 : Partage de fichiers (Samba, NFS)

**Ce que vous apprendrez** :
- Partager des fichiers avec Windows/Mac/Linux (Samba)
- Partager des fichiers entre systèmes Linux (NFS)
- Configurer les permissions et la sécurité
- Accéder aux partages réseau depuis différents systèmes
- Créer un serveur de fichiers domestique

**Pour qui** : Utilisateurs débutants à avancés

**Temps estimé** : 40-50 minutes de lecture

Le partage de fichiers en réseau local est très pratique pour accéder à vos documents depuis plusieurs ordinateurs ou créer un serveur multimédia familial. Cette section couvre les deux protocoles principaux de manière accessible.

### Section 9.7 : Bureau à distance (VNC, RDP)

**Ce que vous apprendrez** :
- Contrôler un ordinateur à distance
- Configurer VNC (Virtual Network Computing)
- Configurer RDP (Remote Desktop Protocol)
- Se connecter depuis Windows, Mac, Linux ou mobile
- Sécuriser vos connexions à distance
- Optimiser les performances

**Pour qui** : Tous les utilisateurs

**Temps estimé** : 35-45 minutes de lecture

Le bureau à distance vous permet de contrôler votre ordinateur depuis n'importe où, ou d'aider quelqu'un à distance. Cette section couvre les solutions libres (VNC, RDP) ainsi que des alternatives commerciales populaires.

### Section 9.8 : Résolution de problèmes réseau

**Ce que vous apprendrez** :
- Méthodologie de diagnostic réseau
- Identifier et résoudre les problèmes courants
- Utiliser les outils de diagnostic (ping, traceroute, etc.)
- Lire et interpréter les logs réseau
- Scripts de diagnostic automatique

**Pour qui** : Tous les utilisateurs (référence pratique)

**Temps estimé** : 40-50 minutes de lecture

Cette section est votre guide de dépannage réseau. Gardez-la comme référence pour résoudre rapidement les problèmes de connexion. Elle contient des solutions pratiques aux problèmes les plus fréquents.

## Comment utiliser ce chapitre

### Pour les débutants

**Lecture recommandée** :
1. **9.1 - Configuration WiFi et Ethernet** (obligatoire)
2. **9.3 - Pare-feu** (fortement recommandé pour la sécurité)
3. **9.8 - Résolution de problèmes réseau** (à garder en référence)

**Sections optionnelles selon vos besoins** :
- 9.2 si vous voulez partager votre connexion
- 9.4 si vous utilisez des WiFi publics ou voulez plus de confidentialité
- 9.7 si vous voulez accéder à distance à votre ordinateur

**Conseil** : Ne vous sentez pas obligé de tout lire d'un coup. Lisez les sections de base, puis revenez aux autres selon vos besoins.

### Pour les utilisateurs intermédiaires

**Parcours suggéré** :
1. Survolez rapidement la section 9.1 (probablement déjà connu)
2. Approfondissez 9.3 (Pare-feu) et 9.4 (VPN)
3. Explorez 9.5 (SSH) si vous gérez des serveurs
4. Lisez 9.6 et 9.7 selon vos besoins de partage/accès distant
5. Gardez 9.8 comme référence

### Pour les utilisateurs avancés

**Focus recommandé** :
- 9.5 (SSH) : Configuration avancée, tunnels, clés
- 9.6 (Samba/NFS) : Serveurs de fichiers, permissions complexes
- 9.8 (Résolution de problèmes) : Outils de diagnostic avancés
- Sections de sécurité dans chaque chapitre

**Conseil** : Les sections contiennent des configurations avancées dans des sous-sections dédiées.

## Conventions utilisées

### Symboles et icônes

**💡 Astuce** : Conseils pratiques et raccourcis
**⚠️ Attention** : Points importants à ne pas manquer
**🔒 Sécurité** : Informations relatives à la sécurité
**🚀 Performance** : Optimisations et améliorations
**🛠️ Dépannage** : Solutions aux problèmes courants

### Exemples de code

Les commandes à taper dans le terminal sont présentées ainsi :
```bash
commande à taper
```

Les fichiers de configuration sont présentés avec leur chemin :
```bash
# /chemin/vers/fichier.conf
contenu du fichier
```

### Niveau de difficulté

Chaque section indique son niveau :
- **🟢 Débutant** : Accessible à tous
- **🟡 Intermédiaire** : Nécessite quelques connaissances de base
- **🔴 Avancé** : Pour utilisateurs expérimentés

## Ressources complémentaires

### Documentation officielle

- **Linux Mint** : https://linuxmint.com/documentation.php
- **Ubuntu Networking** : https://help.ubuntu.com/community/NetworkDevices
- **Arch Wiki** (excellente référence) : https://wiki.archlinux.org/title/Network_configuration

### Outils mentionnés dans ce chapitre

**Graphiques** :
- Network Manager : Gestionnaire de réseau principal
- GUFW : Interface graphique du pare-feu
- Remmina : Client bureau à distance universel
- Wireshark : Analyseur de paquets réseau

**En ligne de commande** :
- `nmcli` : Network Manager CLI
- `ufw` : Uncomplicated Firewall
- `ssh` : Secure Shell
- `samba` : Partage de fichiers Windows
- `nfs` : Partage de fichiers Unix/Linux

### Communauté et support

Si vous rencontrez des problèmes :

1. **Forums Linux Mint** (français) : https://forums.linuxmint.com/
2. **Ubuntu-fr** : https://forum.ubuntu-fr.org/
3. **Reddit** : r/linuxmint, r/linux4noobs
4. **Discord/IRC** : Channels Linux Mint

**Avant de poster** :
- Lisez la section 9.8 (Résolution de problèmes)
- Générez un rapport de diagnostic (expliqué en 9.8)
- Décrivez précisément votre problème et ce que vous avez essayé

## Objectifs d'apprentissage

À la fin de ce chapitre, vous serez capable de :

### Compétences de base (tous les utilisateurs)

- ✅ Vous connecter à n'importe quel réseau WiFi ou Ethernet
- ✅ Diagnostiquer et résoudre les problèmes de connexion courants
- ✅ Protéger votre ordinateur avec un pare-feu configuré correctement
- ✅ Comprendre les bases du réseau (IP, DNS, passerelle)
- ✅ Utiliser un VPN pour sécuriser vos communications

### Compétences intermédiaires

- ✅ Créer un point d'accès WiFi pour partager votre connexion
- ✅ Configurer des paramètres réseau avancés (IP fixe, DNS personnalisés)
- ✅ Partager des fichiers en réseau local avec Samba
- ✅ Accéder à votre ordinateur à distance via VNC ou RDP
- ✅ Utiliser les outils de diagnostic réseau basiques

### Compétences avancées

- ✅ Maîtriser SSH pour l'administration à distance
- ✅ Créer des tunnels SSH sécurisés
- ✅ Configurer des serveurs de fichiers (Samba/NFS) avec permissions complexes
- ✅ Optimiser les performances réseau
- ✅ Diagnostiquer des problèmes réseau complexes avec tcpdump/Wireshark
- ✅ Automatiser des tâches réseau avec des scripts

## Concepts clés à retenir

Avant de plonger dans les sections détaillées, voici les concepts fondamentaux que vous rencontrerez :

### Adresse IP

Une adresse unique qui identifie votre ordinateur sur le réseau (ex: 192.168.1.100). Pensez-y comme à votre adresse postale numérique.

### DNS (Domain Name System)

Le système qui traduit les noms de domaine (google.com) en adresses IP (142.250.X.X). C'est l'annuaire d'Internet.

### Passerelle (Gateway)

Le routeur qui connecte votre réseau local à Internet. C'est votre porte de sortie vers le monde extérieur.

### Pare-feu (Firewall)

Un système qui filtre le trafic réseau entrant et sortant pour protéger votre ordinateur. C'est votre gardien numérique.

### VPN (Virtual Private Network)

Un tunnel chiffré qui protège vos communications et masque votre localisation. C'est votre enveloppe sécurisée pour Internet.

### SSH (Secure Shell)

Un protocole pour accéder à distance à un ordinateur de manière sécurisée. C'est votre terminal à distance chiffré.

### Protocoles de partage

- **Samba** : Partage de fichiers compatible Windows/Mac/Linux
- **NFS** : Partage de fichiers optimisé pour Linux/Unix
- **VNC/RDP** : Partage d'écran et contrôle à distance

## Évolution de vos compétences

Ce chapitre est conçu pour vous accompagner dans votre progression :

**Semaine 1** : Maîtrise des connexions de base (9.1, 9.3)
**Semaine 2** : Sécurité et confidentialité (9.4, partie sécurité de 9.3)
**Semaine 3** : Partage et collaboration (9.2, 9.6, 9.7)
**Semaine 4** : Administration avancée (9.5, configurations avancées)
**En continu** : Référence pour la résolution de problèmes (9.8)

## Conseils pour réussir

### Bonnes pratiques

1. **Testez dans un environnement sûr** : Essayez d'abord sur votre réseau local avant d'exposer des services à Internet

2. **Documentez vos configurations** : Notez ce que vous faites, les mots de passe utilisés (dans un gestionnaire sécurisé), les configurations qui fonctionnent

3. **Sauvegardez avant de modifier** : Avant de changer des fichiers de configuration importants, faites une copie

4. **La sécurité d'abord** : Ne sacrifiez jamais la sécurité pour la facilité. Utilisez toujours des mots de passe forts, activez le pare-feu, chiffrez les connexions

5. **Un problème à la fois** : Si quelque chose ne fonctionne pas, changez une seule chose à la fois pour identifier la cause

### Pièges à éviter

- ❌ **Se connecter en root par SSH** : Dangereux, utilisez sudo
- ❌ **Désactiver le pare-feu** : Ne le faites jamais de manière permanente
- ❌ **Utiliser des mots de passe faibles** : Surtout pour SSH et VPN
- ❌ **Exposer des services non sécurisés à Internet** : Utilisez toujours des tunnels VPN/SSH
- ❌ **Ne pas tester les sauvegardes** : Vérifiez que vos configs sauvegardées fonctionnent

## Matériel de référence rapide

### Commandes réseau essentielles

```bash
# Voir les connexions
nmcli connection show

# Voir l'adresse IP
ip addr show

# Tester la connexion
ping google.com

# Voir la route
ip route show

# Voir les DNS
cat /etc/resolv.conf

# Redémarrer le réseau
sudo systemctl restart NetworkManager
```

**Note** : Ces commandes sont expliquées en détail dans les sections correspondantes.

### Fichiers de configuration importants

- `/etc/NetworkManager/` : Configuration Network Manager
- `/etc/ssh/sshd_config` : Configuration serveur SSH
- `/etc/samba/smb.conf` : Configuration Samba
- `/etc/exports` : Configuration NFS
- `/etc/ufw/` : Configuration pare-feu

## Prêt à commencer ?

Vous avez maintenant une vue d'ensemble complète de ce chapitre sur la configuration réseau et Internet.

**Prochaine étape** : Commencez par la section 9.1 pour apprendre à configurer vos connexions WiFi et Ethernet. C'est la base de tout le reste !

Si vous avez déjà une connexion Internet fonctionnelle et souhaitez aller plus loin, n'hésitez pas à passer directement aux sections qui vous intéressent. Chaque section est conçue pour être aussi autonome que possible.

**Bon apprentissage et bienvenue dans le monde passionnant des réseaux sous Linux !** 🚀


⏭️ [Configuration WiFi et Ethernet](/09-configuration-reseau-et-internet/01-configuration-wifi-et-ethernet.md)
