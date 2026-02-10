🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 9.3 Pare-feu (UFW/GUFW)

## Introduction

Un pare-feu (firewall en anglais) est un outil de sécurité essentiel qui contrôle le trafic réseau entrant et sortant de votre ordinateur. Il agit comme une barrière de protection entre votre ordinateur et Internet, en bloquant les connexions non autorisées tout en permettant le trafic légitime.

Sous Linux Mint, le pare-feu par défaut s'appelle **UFW** (Uncomplicated Firewall - Pare-feu simple). Comme son nom l'indique, il a été conçu pour être facile à utiliser. Pour ceux qui préfèrent une interface graphique, **GUFW** offre une solution visuelle pour gérer UFW.

Dans ce chapitre, nous allons apprendre à configurer et utiliser le pare-feu pour protéger votre système, que vous soyez à l'aise avec le terminal ou que vous préfériez une interface graphique.

## Comprendre le pare-feu

### Qu'est-ce qu'un pare-feu ?

Imaginez votre ordinateur comme une maison avec de nombreuses portes (appelées "ports" en informatique). Chaque porte peut permettre l'entrée ou la sortie d'informations. Un pare-feu est comme un gardien qui :

- Surveille toutes les portes
- Décide qui peut entrer et sortir
- Bloque les visiteurs indésirables
- Autorise les connexions légitimes

### Pourquoi utiliser un pare-feu ?

**Protection contre les intrusions** :
- Bloque les tentatives de connexion malveillantes
- Empêche les pirates d'accéder à votre système
- Protège contre les logiciels malveillants qui tentent de communiquer avec l'extérieur

**Contrôle du trafic** :
- Vous décidez quelles applications peuvent accéder au réseau
- Vous pouvez bloquer des connexions spécifiques
- Utile pour les réseaux publics (cafés, aéroports)

**Tranquillité d'esprit** :
- Une couche de sécurité supplémentaire
- Particulièrement important si vous exécutez des serveurs
- Essentiel pour la sécurité en ligne

### Linux a-t-il besoin d'un pare-feu ?

Linux est naturellement plus sécurisé que d'autres systèmes, mais un pare-feu reste **fortement recommandé** :

- Pour les ordinateurs portables qui se connectent à différents réseaux
- Si vous exécutez des services (serveur web, SSH, etc.)
- Pour bloquer des applications spécifiques
- Sur les réseaux publics ou non sécurisés

**Note importante** : Par défaut sous Linux Mint, UFW est installé mais **désactivé**. Nous allons voir comment l'activer et le configurer.

## GUFW : Interface graphique pour le pare-feu

GUFW est l'interface graphique pour UFW. Elle est parfaite pour les débutants car elle offre une vue visuelle claire de la configuration du pare-feu.

### Installation de GUFW

GUFW n'est pas installé par défaut sur Linux Mint, mais son installation est très simple :

1. **Via le Gestionnaire de logiciels** :
   - Ouvrez le Menu → Administration → Gestionnaire de logiciels
   - Recherchez "gufw"
   - Cliquez sur "Installer"

2. **Via le terminal** :
   ```bash
   sudo apt update
   sudo apt install gufw
   ```

### Lancement de GUFW

Une fois installé, vous pouvez lancer GUFW de plusieurs façons :

- **Menu principal** → Administration → Configuration du pare-feu
- **Terminal** : tapez `sudo gufw`
- **Recherche** : Tapez "pare-feu" ou "firewall" dans le menu principal

**Important** : GUFW nécessite les droits administrateur, vous devrez donc entrer votre mot de passe au lancement.

### Interface de GUFW

L'interface de GUFW est divisée en plusieurs sections :

#### Section principale (en haut)

**État du pare-feu** :
- Un grand bouton à bascule pour activer/désactiver le pare-feu
- Rouge = désactivé / Vert = activé

**Statut** :
- Affiche si le pare-feu est actif ou inactif
- Indique le nombre de règles actives

**Connexions entrantes** :
- Par défaut : "Refuser" (recommandé)
- Bloque toutes les connexions entrantes non autorisées

**Connexions sortantes** :
- Par défaut : "Autoriser" (recommandé)
- Permet à vos applications de se connecter à Internet

#### Section des règles

Liste toutes les règles personnalisées que vous avez créées :
- Application autorisée ou bloquée
- Port spécifique
- Adresse IP
- Direction (entrant/sortant)

### Activer le pare-feu

Pour activer la protection de base :

1. **Ouvrez GUFW**
2. **Cliquez sur le bouton "État"** pour passer de "Désactivé" à "Activé"
3. **Confirmez** si demandé

C'est tout ! Votre pare-feu est maintenant actif avec une configuration par défaut sécurisée :
- Toutes les connexions entrantes sont bloquées
- Toutes les connexions sortantes sont autorisées

Cette configuration convient à la majorité des utilisateurs pour un usage quotidien (navigation web, emails, etc.).

### Profils prédéfinis

GUFW propose trois profils prédéfinis accessibles via le menu déroulant :

**Domicile** :
- Configuration pour un réseau domestique de confiance
- Moins restrictif
- Permet le partage de fichiers local

**Public** :
- Configuration pour les réseaux publics (cafés, hôtels)
- Plus restrictif
- Bloque davantage de services

**Bureau** :
- Configuration pour un environnement de travail
- Équilibre entre sécurité et fonctionnalités
- Permet les services réseau courants

Pour la plupart des utilisateurs, le profil par défaut (similaire à "Domicile") est suffisant.

## Créer des règles personnalisées

Parfois, vous devrez créer des règles spécifiques pour autoriser ou bloquer certaines connexions.

### Autoriser une application

Si une application légitime ne peut pas se connecter à Internet :

1. **Ouvrez GUFW**
2. **Cliquez sur le bouton "Règles"** en bas
3. **Cliquez sur le bouton "+" (Ajouter)**
4. Une fenêtre s'ouvre avec plusieurs onglets

#### Onglet "Préconfigurées"

C'est la méthode la plus simple pour les applications courantes :

1. **Catégorie** : Sélectionnez le type d'application (ex: "Peer to Peer" pour les torrents)
2. **Application** : Choisissez l'application spécifique (ex: "Transmission")
3. **Action** : "Autoriser" ou "Refuser"
4. **Direction** :
   - "Entrées" : pour les connexions qui arrivent vers votre ordinateur
   - "Sorties" : pour les connexions qui partent de votre ordinateur
   - "Les deux" : pour les deux directions
5. Cliquez sur "Ajouter"

#### Onglet "Simple"

Pour autoriser un port spécifique :

1. **Nom** : Donnez un nom descriptif à la règle (ex: "Serveur Web")
2. **Action** : "Autoriser" ou "Refuser"
3. **Direction** : Entrées/Sorties/Les deux
4. **Catégorie** : Choisissez entre :
   - **Application** : Sélectionnez une application spécifique
   - **Port** : Spécifiez un numéro de port
5. Si vous choisissez "Port" :
   - **Port** : Entrez le numéro (ex: 80 pour HTTP, 22 pour SSH)
   - **Protocole** : TCP, UDP ou Les deux
6. Cliquez sur "Ajouter"

#### Onglet "Avancé"

Pour des règles très spécifiques (utilisateurs avancés) :

Permet de spécifier :
- **Adresses IP sources et destinations**
- **Ports sources et destinations**
- **Interfaces réseau spécifiques**
- **Règles de journalisation**

### Exemples de règles courantes

#### Autoriser SSH (port 22)

Si vous voulez accéder à votre ordinateur à distance :

1. Règles → Ajouter
2. Onglet "Simple"
3. Nom : "SSH"
4. Action : Autoriser
5. Direction : Entrées
6. Catégorie : Port
7. Port : 22
8. Protocole : TCP

**Attention** : Autoriser SSH expose votre ordinateur. Assurez-vous d'avoir un mot de passe fort ou mieux, utilisez des clés SSH (voir chapitre 9.5).

#### Autoriser un serveur web (ports 80 et 443)

Pour héberger un site web local :

1. Créez une règle pour le port 80 (HTTP)
2. Créez une autre règle pour le port 443 (HTTPS)
3. Action : Autoriser
4. Direction : Entrées
5. Protocole : TCP

#### Bloquer une application spécifique

Pour empêcher une application d'accéder à Internet :

1. Règles → Ajouter
2. Onglet "Préconfigurées" ou "Simple"
3. Sélectionnez l'application
4. Action : **Refuser**
5. Direction : Sorties

### Modifier ou supprimer une règle

**Modifier une règle** :
1. Double-cliquez sur la règle dans la liste
2. Modifiez les paramètres
3. Cliquez sur "Modifier"

**Supprimer une règle** :
1. Sélectionnez la règle dans la liste
2. Cliquez sur le bouton "-" (Supprimer)
3. Confirmez la suppression

**Désactiver temporairement une règle** :
- Malheureusement, GUFW ne permet pas de désactiver temporairement une règle
- Vous devez la supprimer et la recréer plus tard
- Alternative : utilisez UFW en ligne de commande

## UFW en ligne de commande

Pour les utilisateurs plus avancés ou pour automatiser des tâches, UFW peut être contrôlé via le terminal. C'est également utile à connaître pour le dépannage.

### Commandes de base UFW

**Vérifier le statut** :
```bash
sudo ufw status
```

Affiche si le pare-feu est actif et liste toutes les règles.

Pour plus de détails :
```bash
sudo ufw status verbose
```

**Activer le pare-feu** :
```bash
sudo ufw enable
```

**Désactiver le pare-feu** :
```bash
sudo ufw disable
```

**Réinitialiser toutes les règles** :
```bash
sudo ufw reset
```

Cette commande supprime toutes les règles et désactive le pare-feu. Utilisez avec précaution !

### Politique par défaut

Définir la politique par défaut pour le trafic entrant et sortant :

```bash
# Refuser tout le trafic entrant par défaut
sudo ufw default deny incoming

# Autoriser tout le trafic sortant par défaut
sudo ufw default allow outgoing
```

C'est la configuration recommandée pour la plupart des utilisateurs.

### Créer des règles en ligne de commande

#### Autoriser un port spécifique

```bash
# Autoriser le port 22 (SSH)
sudo ufw allow 22

# Autoriser le port 80 (HTTP)
sudo ufw allow 80

# Autoriser le port 443 (HTTPS)
sudo ufw allow 443
```

#### Autoriser un port avec un protocole spécifique

```bash
# Autoriser le port 53 en UDP (DNS)
sudo ufw allow 53/udp

# Autoriser le port 22 en TCP (SSH)
sudo ufw allow 22/tcp
```

#### Autoriser une plage de ports

```bash
# Autoriser les ports 6000 à 6007
sudo ufw allow 6000:6007/tcp
```

#### Autoriser une application

```bash
# Autoriser Apache (serveur web)
sudo ufw allow 'Apache'

# Autoriser OpenSSH
sudo ufw allow 'OpenSSH'

# Voir la liste des applications disponibles
sudo ufw app list
```

#### Autoriser depuis une adresse IP spécifique

```bash
# Autoriser toutes les connexions depuis 192.168.1.100
sudo ufw allow from 192.168.1.100

# Autoriser SSH uniquement depuis 192.168.1.100
sudo ufw allow from 192.168.1.100 to any port 22

# Autoriser depuis un sous-réseau
sudo ufw allow from 192.168.1.0/24
```

#### Refuser des connexions

```bash
# Bloquer le port 25 (SMTP)
sudo ufw deny 25

# Bloquer une adresse IP spécifique
sudo ufw deny from 192.168.1.150

# Bloquer SSH depuis une IP spécifique
sudo ufw deny from 192.168.1.150 to any port 22
```

### Supprimer des règles

**Par numéro de règle** :

1. Lister les règles avec leurs numéros :
```bash
sudo ufw status numbered
```

2. Supprimer une règle par son numéro :
```bash
sudo ufw delete 3
```

**Par spécification complète** :

Répétez la commande de création avec "delete" :
```bash
# Si vous avez créé la règle avec :
sudo ufw allow 80

# Supprimez-la avec :
sudo ufw delete allow 80
```

### Règles avancées UFW

#### Limiter les tentatives de connexion

Pour se protéger contre les attaques par force brute (essais de mots de passe répétés) :

```bash
# Limiter SSH (max 6 tentatives en 30 secondes)
sudo ufw limit 22/tcp
```

Cette règle est particulièrement utile pour SSH.

#### Interface réseau spécifique

Si vous avez plusieurs interfaces réseau :

```bash
# Autoriser sur l'interface eth0
sudo ufw allow in on eth0 to any port 80

# Refuser sur l'interface wlan0
sudo ufw deny in on wlan0 to any port 22
```

#### Journalisation

Activer la journalisation pour surveiller les activités du pare-feu :

```bash
# Activer la journalisation
sudo ufw logging on

# Niveau de journalisation
sudo ufw logging low    # Minimal  
sudo ufw logging medium # Moyen  
sudo ufw logging high   # Détaillé  
sudo ufw logging full   # Complet (beaucoup de données)  
```

Les logs sont stockés dans `/var/log/ufw.log`.

Pour désactiver :
```bash
sudo ufw logging off
```

## Configuration recommandée selon l'usage

### Utilisateur domestique (navigation, emails)

Configuration de base suffisante :

```bash
sudo ufw default deny incoming  
sudo ufw default allow outgoing  
sudo ufw enable  
```

Aucune règle supplémentaire nécessaire sauf si vous utilisez des applications spécifiques.

### Utilisateur avec serveur personnel

Si vous hébergez des services (web, SSH, etc.) :

```bash
# Configuration de base
sudo ufw default deny incoming  
sudo ufw default allow outgoing  

# Autoriser SSH avec limitation
sudo ufw limit 22/tcp

# Autoriser HTTP et HTTPS
sudo ufw allow 80/tcp  
sudo ufw allow 443/tcp  

# Activer la journalisation
sudo ufw logging low

# Activer le pare-feu
sudo ufw enable
```

### Ordinateur portable (réseaux publics)

Protection maximale pour les déplacements :

```bash
# Configuration stricte
sudo ufw default deny incoming  
sudo ufw default deny outgoing  

# Autoriser seulement le nécessaire
sudo ufw allow out 80/tcp   # HTTP  
sudo ufw allow out 443/tcp  # HTTPS  
sudo ufw allow out 53       # DNS  
sudo ufw allow out 123/udp  # NTP (synchronisation de l'heure)  

# Activer
sudo ufw enable
```

**Note** : Cette configuration très restrictive peut bloquer certaines applications. Ajustez selon vos besoins.

### Développeur

Pour les développeurs qui testent des applications localement :

```bash
# Configuration de base
sudo ufw default deny incoming  
sudo ufw default allow outgoing  

# Autoriser le trafic local (localhost)
sudo ufw allow from 127.0.0.1

# Autoriser votre réseau local
sudo ufw allow from 192.168.1.0/24

# Ports de développement courants
sudo ufw allow 3000/tcp  # Node.js  
sudo ufw allow 8000/tcp  # Django  
sudo ufw allow 8080/tcp  # Divers  
sudo ufw allow 5432/tcp  # PostgreSQL (si accès externe nécessaire)  

sudo ufw enable
```

## Vérifier et tester le pare-feu

### Vérifier que le pare-feu est actif

**Via GUFW** :
- Ouvrez GUFW
- Vérifiez que l'état est "Activé"

**Via terminal** :
```bash
sudo ufw status
```

Devrait afficher : `Status: active`

### Tester les ports ouverts

Pour vérifier quels ports sont ouverts sur votre système :

```bash
# Voir les ports en écoute
sudo ss -tuln

# Ou avec netstat (si installé)
sudo netstat -tuln
```

### Scanner votre système (depuis l'extérieur)

Pour tester votre pare-feu depuis l'extérieur, vous pouvez utiliser des outils en ligne comme :
- ShieldsUP! (grc.com)
- Nmap en ligne (divers sites)

**Attention** : Ne scannez que vos propres systèmes. Scanner d'autres systèmes sans permission est illégal.

### Tester une règle spécifique

Pour vérifier qu'un port est bien bloqué/autorisé :

1. **Depuis votre machine** :
```bash
# Tester si un port local est en écoute
nc -zv localhost 22
```

2. **Depuis une autre machine du réseau** :
```bash
# Tester la connexion au port 22 de 192.168.1.100
nc -zv 192.168.1.100 22
```

## Résolution des problèmes courants

### Une application ne peut plus se connecter à Internet

**Diagnostic** :

1. Vérifiez si le pare-feu est actif :
```bash
sudo ufw status
```

2. Vérifiez les règles existantes pour voir si l'application est bloquée

**Solutions** :

1. **Désactiver temporairement le pare-feu** pour tester :
```bash
sudo ufw disable
```
Si l'application fonctionne, c'est bien le pare-feu qui bloque.

2. **Créer une règle pour l'application** :
- Via GUFW : Ajoutez une règle pour autoriser l'application
- Via terminal : Identifiez le port utilisé et autorisez-le

3. **Réactiver le pare-feu** :
```bash
sudo ufw enable
```

### Le pare-feu bloque le partage de fichiers local

Si vous ne pouvez plus accéder aux partages réseau (Samba) :

```bash
# Autoriser Samba
sudo ufw allow Samba
```

Ou manuellement :
```bash
sudo ufw allow 137,138/udp  
sudo ufw allow 139,445/tcp  
```

### SSH ne fonctionne plus

Si vous ne pouvez plus vous connecter en SSH :

```bash
# Vérifier si SSH est autorisé
sudo ufw status | grep 22

# Si absent, autoriser SSH
sudo ufw allow 22/tcp
```

### Impossible d'activer le pare-feu

**Erreur** : "ERROR: problem running" ou similaire

**Solutions** :

1. **Vérifier les conflits** :
```bash
# Arrêter les autres pare-feu qui pourraient entrer en conflit
sudo systemctl stop firewalld
```

2. **Réinstaller UFW** :
```bash
sudo apt remove --purge ufw  
sudo apt install ufw  
```

3. **Vérifier les permissions** :
```bash
sudo chmod 644 /etc/ufw/*.rules
```

### Les règles ne semblent pas fonctionner

**Solutions** :

1. **Recharger les règles** :
```bash
sudo ufw reload
```

2. **Vérifier l'ordre des règles** :
Les règles sont appliquées dans l'ordre. Une règle générale au début peut bloquer une règle spécifique plus tard.
```bash
sudo ufw status numbered
```

3. **Supprimer et recréer la règle** :
Parfois, supprimer et recréer une règle résout le problème.

### Le pare-feu se désactive au redémarrage

**Solution** :

Vérifier que UFW est configuré pour démarrer automatiquement :
```bash
sudo systemctl enable ufw  
sudo systemctl start ufw  
```

### Consulter les logs pour diagnostiquer

Pour voir ce que le pare-feu bloque :

```bash
# Voir les dernières entrées du log
sudo tail -f /var/log/ufw.log

# Rechercher des blocages spécifiques
sudo grep BLOCK /var/log/ufw.log

# Voir les tentatives récentes
sudo grep UFW /var/log/syslog
```

## Sécurité et bonnes pratiques

### Principe du moindre privilège

**Règle d'or** : N'autorisez que ce qui est strictement nécessaire.

- Commencez avec tout bloqué (deny incoming)
- Autorisez seulement les services que vous utilisez réellement
- Revoyez régulièrement vos règles et supprimez celles qui ne sont plus nécessaires

### Protection SSH renforcée

Si vous utilisez SSH :

```bash
# Limiter les tentatives de connexion
sudo ufw limit 22/tcp

# Ou mieux : autoriser SSH seulement depuis des IP spécifiques
sudo ufw allow from 192.168.1.0/24 to any port 22

# Ou encore mieux : changer le port SSH (dans /etc/ssh/sshd_config)
# puis autoriser le nouveau port
sudo ufw allow 2222/tcp
```

### Règles temporaires

Pour tester une règle sans l'appliquer définitivement :

1. Notez vos règles actuelles
2. Ajoutez la nouvelle règle
3. Testez
4. Si problème, supprimez immédiatement

**Astuce** : Utilisez une connexion SSH avec un timeout pour ne pas vous bloquer vous-même :
```bash
# Ouvre SSH pendant 2 minutes pour tester
sudo ufw allow 22 comment "Test temporaire"
# Testez la connexion
# Si ça fonctionne, gardez la règle, sinon supprimez-la
```

### Surveiller régulièrement

**Vérifications périodiques recommandées** :

1. **Hebdomadaire** : Vérifier le statut et les règles actives
```bash
sudo ufw status verbose
```

2. **Mensuel** : Consulter les logs pour détecter des tentatives d'intrusion
```bash
sudo grep BLOCK /var/log/ufw.log | tail -20
```

3. **Trimestriel** : Faire le ménage dans les règles inutilisées

### Sauvegarder votre configuration

Avant des modifications importantes :

```bash
# Sauvegarder la configuration actuelle
sudo cp /etc/ufw/user.rules ~/ufw-backup-$(date +%Y%m%d).rules  
sudo cp /etc/ufw/user6.rules ~/ufw6-backup-$(date +%Y%m%d).rules  

# En cas de problème, restaurer :
sudo cp ~/ufw-backup-YYYYMMDD.rules /etc/ufw/user.rules  
sudo cp ~/ufw6-backup-YYYYMMDD.rules /etc/ufw/user6.rules  
sudo ufw reload  
```

### Ne jamais bloquer localhost

Le trafic local (127.0.0.1) doit toujours être autorisé :

```bash
# S'assurer que localhost est toujours autorisé
sudo ufw allow from 127.0.0.0/8  
sudo ufw allow to 127.0.0.0/8  
```

Par défaut, UFW ne bloque pas localhost, mais après des modifications importantes, vérifiez.

### Documentation de vos règles

Utilisez les commentaires pour documenter vos règles (ligne de commande uniquement) :

```bash
# Ajouter une règle avec commentaire
sudo ufw allow 3000/tcp comment "Application de dev Node.js"

# Voir les commentaires
sudo ufw status verbose
```

Cela vous aide à vous souvenir pourquoi vous avez créé chaque règle.

## Cas d'usage avancés

### Bloquer un pays entier

Pour bloquer tout le trafic provenant d'un pays spécifique, vous aurez besoin de listes d'adresses IP par pays et de règles personnalisées. C'est complexe et généralement fait avec des outils supplémentaires comme ipset.

Cette fonctionnalité dépasse le cadre de ce tutoriel débutant.

### Pare-feu pour un serveur web

Configuration optimale pour un serveur web accessible publiquement :

```bash
# Configuration de base stricte
sudo ufw default deny incoming  
sudo ufw default allow outgoing  

# Services web
sudo ufw allow 80/tcp comment "HTTP"  
sudo ufw allow 443/tcp comment "HTTPS"  

# SSH limité
sudo ufw limit 22/tcp comment "SSH avec limitation"

# DNS sortant (si nécessaire)
sudo ufw allow out 53 comment "DNS"

# Journalisation
sudo ufw logging medium

# Activer
sudo ufw enable
```

### Pare-feu pour un serveur de jeu

```bash
# Autoriser le port du jeu (exemple : Minecraft sur 25565)
sudo ufw allow 25565/tcp comment "Serveur Minecraft"

# Si le jeu utilise aussi UDP
sudo ufw allow 25565/udp
```

### Bloquer temporairement tout sauf SSH

En cas d'urgence ou d'attaque :

```bash
# Bloquer tout
sudo ufw default deny incoming  
sudo ufw default deny outgoing  

# Garder seulement SSH
sudo ufw allow 22/tcp

# Réactiver
sudo ufw enable
```

## Différences entre UFW et d'autres pare-feu

### UFW vs iptables

**iptables** :
- Pare-feu Linux de bas niveau
- Très puissant mais complexe
- Syntaxe difficile pour les débutants

**UFW** :
- Interface simplifiée pour iptables
- Plus facile à utiliser
- Suffisant pour 95% des besoins

UFW utilise iptables en arrière-plan, c'est juste une couche de simplification.

### UFW vs firewalld

**firewalld** :
- Utilisé principalement sur Fedora/RedHat
- Concept de "zones"
- Plus complexe qu'UFW

**UFW** :
- Standard sur Ubuntu/Debian/Mint
- Plus simple
- Meilleur pour les débutants

### UFW vs pare-feu Windows

Les concepts sont similaires, mais :
- UFW est plus transparent sur ce qu'il fait
- Plus de contrôle en ligne de commande
- Configuration généralement plus simple
- Moins de popups intrusifs

## Outils complémentaires

### fail2ban

Pour une protection automatique contre les attaques par force brute (voir chapitre 11.8) :

```bash
sudo apt install fail2ban
```

fail2ban surveille les logs et bannit automatiquement les IP suspectes.

### psad

Port Scan Attack Detector - détecte les scans de ports :

```bash
sudo apt install psad
```

### nmap

Pour tester votre propre pare-feu :

```bash
sudo apt install nmap

# Scanner votre propre machine
nmap localhost

# Scanner depuis le réseau local (remplacez par votre IP)
nmap 192.168.1.100
```

## Conseils finaux

### Pour les débutants

1. **Commencez simple** : Activez UFW avec la configuration par défaut
2. **Utilisez GUFW** : L'interface graphique est plus intuitive au début
3. **Ajoutez des règles au besoin** : Seulement quand une application ne fonctionne pas
4. **Documentez** : Notez pourquoi vous créez chaque règle

### Pour aller plus loin

1. **Apprenez iptables** : Pour comprendre ce qui se passe en arrière-plan
2. **Installez fail2ban** : Protection automatique supplémentaire
3. **Surveillez les logs** : Habituez-vous à consulter `/var/log/ufw.log`
4. **Testez régulièrement** : Vérifiez que votre pare-feu fonctionne comme prévu

### Ressources

- Documentation officielle UFW : `man ufw`
- Wiki Ubuntu UFW : https://help.ubuntu.com/community/UFW
- Forums Linux Mint pour des questions spécifiques

## Résumé des commandes essentielles

```bash
# Gestion de base
sudo ufw status              # Vérifier le statut  
sudo ufw enable              # Activer  
sudo ufw disable             # Désactiver  
sudo ufw reload              # Recharger les règles  

# Politiques par défaut
sudo ufw default deny incoming  
sudo ufw default allow outgoing  

# Règles simples
sudo ufw allow 22            # Autoriser un port  
sudo ufw deny 25             # Bloquer un port  
sudo ufw limit 22/tcp        # Limiter les tentatives  
sudo ufw delete allow 80     # Supprimer une règle  

# Règles avancées
sudo ufw allow from 192.168.1.100        # Autoriser une IP  
sudo ufw allow from 192.168.1.0/24       # Autoriser un sous-réseau  
sudo ufw allow 80/tcp comment "HTTP"     # Règle avec commentaire  

# Informations
sudo ufw status verbose      # Statut détaillé  
sudo ufw status numbered     # Règles numérotées  
sudo ufw show raw           # Règles iptables brutes  

# Journalisation
sudo ufw logging on         # Activer les logs  
sudo ufw logging off        # Désactiver les logs  
```

---

**Points clés à retenir** :
- Le pare-feu UFW est simple mais puissant pour protéger votre système
- GUFW offre une interface graphique conviviale pour les débutants
- La configuration par défaut (deny incoming, allow outgoing) convient à la plupart des utilisateurs
- N'autorisez que les ports/services dont vous avez réellement besoin
- Utilisez "limit" pour SSH afin de vous protéger contre les attaques par force brute
- Consultez régulièrement les logs pour détecter les activités suspectes
- Documentez vos règles pour vous souvenir de leur utilité
- En cas de doute, commencez simple et ajoutez des règles progressivement

⏭️ [Configuration VPN](/09-configuration-reseau-et-internet/04-configuration-vpn.md)
