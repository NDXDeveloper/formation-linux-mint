🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8 Warpinator (Échange de fichiers sur le réseau local)

## Introduction

**Warpinator** est un outil développé par l'équipe de Linux Mint pour transférer facilement des fichiers entre ordinateurs sur le même réseau local (WiFi ou Ethernet). C'est l'équivalent libre et gratuit d'AirDrop d'Apple, mais fonctionnant sur Linux, Windows, Android et iOS.

## Qu'est-ce que Warpinator ?

### Présentation

Warpinator permet de partager des fichiers **sans câble USB**, **sans email**, et **sans cloud**, directement d'un ordinateur à un autre sur votre réseau domestique ou professionnel.

**Cas d'usage courants** :
- Transférer des photos de votre laptop vers votre PC fixe
- Partager un document avec un collègue dans le même bureau
- Envoyer des fichiers de votre ordinateur vers votre smartphone
- Échanger des vidéos avec des membres de la famille à la maison

### Avantages de Warpinator

**Simple** :
- Pas de configuration complexe
- Détecte automatiquement les appareils
- Interface intuitive

**Rapide** :
- Utilise votre réseau local (WiFi/Ethernet)
- Pas de limitation de bande passante
- Beaucoup plus rapide que l'upload cloud

**Sécurisé** :
- Connexions chiffrées
- Code de groupe optionnel
- Tout reste sur votre réseau local

**Gratuit** :
- Open source
- Aucune limite de taille
- Aucun compte requis

**Sans Internet** :
- Fonctionne hors ligne
- Nécessite seulement un réseau local

### Comment ça fonctionne ?

**Principe** :
1. Tous les appareils sont sur le même réseau WiFi ou Ethernet
2. Warpinator s'exécute sur chaque appareil
3. Les appareils se détectent automatiquement
4. Vous sélectionnez le destinataire et les fichiers
5. Le transfert se fait directement entre appareils

**Technologie** :
- Protocole pair-à-pair (P2P)
- Chiffrement TLS (connexion sécurisée)
- Découverte automatique (mDNS/Avahi)
- Port TCP par défaut : 42000

## Installation de Warpinator

### Sur Linux Mint

**Warpinator est préinstallé** sur Linux Mint 20 et versions ultérieures. Vous n'avez rien à installer !

**Vérifier la présence** :
1. Menu principal → **Accessoires** → **Warpinator**
2. Si absent, installez-le :

```bash
sudo apt update  
sudo apt install warpinator  
```

### Sur d'autres distributions Linux

**Ubuntu, Debian et dérivés** :

```bash
sudo apt install warpinator
```

**Fedora** :

```bash
sudo dnf install warpinator
```

**Arch Linux** :

```bash
yay -S warpinator
```

**Flatpak** (universel) :

```bash
flatpak install flathub org.x.Warpinator
```

### Sur Windows

**Téléchargement** :
1. Visitez : [https://github.com/slowscript/warp/releases](https://github.com/slowscript/warp/releases)
2. Téléchargez le fichier `.msi` pour Windows
3. Installez normalement

**Ou utilisez WinWarp** (client alternatif) :
- Plus léger
- Même compatibilité

### Sur Android

**Installation depuis Google Play** :
1. Ouvrez le **Play Store**
2. Recherchez "**Warpinator**"
3. Installez l'application développée par "Slow But Sure Software"

**Ou F-Droid** (magasin libre) :
- Recherchez "Warpinator"
- Installez

### Sur iOS (iPhone/iPad)

**Installation depuis l'App Store** :
1. Ouvrez l'**App Store**
2. Recherchez "**Warpinator**"
3. Installez l'application

## Premier lancement et configuration

### Lancer Warpinator

**Depuis le menu** :
1. Menu principal → **Accessoires** → **Warpinator**
2. Ou tapez "Warpinator" dans la recherche

**L'application s'ouvre** :
- Une fenêtre apparaît
- Warpinator commence à chercher d'autres appareils

### Interface de Warpinator

**Panneau de gauche** :
- Liste des appareils détectés
- Votre propre appareil en haut (avec coche verte)
- Appareils disponibles en dessous

**Panneau de droite** :
- Sélectionnez un appareil à gauche
- Historique des transferts avec cet appareil
- Bouton **Envoyer des fichiers**

**Barre d'état** (en bas) :
- Statut de la connexion
- Nombre d'appareils détectés

**Menu** (☰ en haut à droite) :
- Préférences
- À propos

### Première configuration

**Au premier lancement** :

1. **Autoriser le pare-feu** (si demandé)
   - Une notification peut apparaître
   - Cliquez sur **Autoriser**
   - Nécessaire pour que Warpinator puisse communiquer

2. **Choisir un nom d'appareil** (optionnel)
   - Par défaut : Nom de votre ordinateur
   - Menu **☰** → **Préférences** → **Général**
   - Modifiez **Nom d'affichage**
   - Exemple : "PC-Bureau-Paul", "Laptop-Marie"

3. **Dossier de réception** (optionnel)
   - Par défaut : `~/Warpinator` (dans votre dossier personnel)
   - Préférences → **Général** → **Emplacement des fichiers reçus**
   - Choisissez un autre dossier si souhaité

### Vérifier la détection

**Test rapide** :

Si vous avez deux appareils sur le même réseau avec Warpinator :
1. Lancez Warpinator sur les deux
2. Attendez quelques secondes
3. Chaque appareil doit apparaître dans la liste de l'autre

**Si les appareils ne se voient pas**, voir section Dépannage.

## Envoyer des fichiers

### Méthode simple

**Depuis Warpinator** :

1. Ouvrez Warpinator
2. Sélectionnez l'appareil destinataire dans la liste de gauche
3. Cliquez sur **Envoyer des fichiers** (en haut à droite)
4. Parcourez et sélectionnez vos fichiers/dossiers
5. Cliquez sur **Ouvrir**
6. Les fichiers sont envoyés immédiatement

**Le destinataire** :
- Reçoit une notification
- Peut accepter ou refuser le transfert
- Si accepté, les fichiers sont téléchargés

### Envoyer un dossier complet

**Pour transférer tout un dossier** :

1. Warpinator → Sélectionnez le destinataire
2. **Envoyer des fichiers**
3. Naviguez jusqu'au dossier parent
4. Sélectionnez le dossier entier
5. Cliquez sur **Ouvrir**

**Warpinator envoie** :
- Le dossier et tout son contenu
- La structure est préservée
- Sous-dossiers inclus

### Envoyer depuis le gestionnaire de fichiers

**Méthode rapide (clic droit)** :

1. Ouvrez le gestionnaire de fichiers (Nemo)
2. Naviguez vers vos fichiers/dossiers
3. Sélectionnez ce que vous voulez envoyer
4. Clic droit → **Envoyer via Warpinator**
5. Choisissez le destinataire
6. Cliquez sur **Envoyer**

**Avantage** : Plus rapide, pas besoin d'ouvrir Warpinator d'abord !

### Envoyer plusieurs fichiers

**Sélection multiple** :

1. Lors du choix des fichiers, maintenez `Ctrl` enfoncé
2. Cliquez sur chaque fichier à envoyer
3. Tous sont sélectionnés
4. Cliquez sur **Ouvrir**
5. Tous les fichiers sont transférés ensemble

**Ou depuis Nemo** :
- Sélectionnez plusieurs fichiers (Ctrl + clic)
- Clic droit → **Envoyer via Warpinator**

### Annuler un envoi

**En cours de transfert** :

- Dans Warpinator, un indicateur de progression apparaît
- Cliquez sur le bouton **×** (annuler) à côté de la progression
- Le transfert s'arrête

**Note** : Les fichiers partiellement transférés restent incomplets chez le destinataire.

## Recevoir des fichiers

### Accepter une demande

**Quand quelqu'un vous envoie des fichiers** :

1. Une **notification** apparaît (bureau et dans Warpinator)
2. Message : "[Nom de l'appareil] veut vous envoyer des fichiers"
3. Cliquez sur **Accepter** ou **Refuser**

**Si vous acceptez** :
- Le téléchargement démarre
- Progression affichée dans Warpinator
- Notification à la fin

**Si vous refusez** :
- L'envoi est annulé
- L'expéditeur en est informé

### Accéder aux fichiers reçus

**Dossier de réception par défaut** :

Les fichiers arrivent dans : `~/Warpinator/` (dans votre dossier personnel)

**Ouvrir le dossier** :

**Méthode 1** :
1. Dans Warpinator, menu **☰** → **Préférences**
2. Cliquez sur **Afficher le dossier de réception**

**Méthode 2** :
1. Gestionnaire de fichiers
2. Naviguez vers `/home/votre-nom/Warpinator/`

**Méthode 3** :
- Après réception, une notification s'affiche
- Cliquez dessus pour ouvrir le dossier

### Acceptation automatique

**Recevoir sans confirmation** (pratique entre vos propres appareils) :

1. Menu **☰** → **Préférences**
2. Onglet **Général**
3. Cochez **Accepter automatiquement les fichiers**
4. Appliquez

**Attention** : Tous les envois seront acceptés sans demande !

**Recommandation** :
- Activez seulement sur réseau de confiance (maison)
- Désactivez sur réseau public (café, aéroport)

### Organisation des fichiers reçus

**Par défaut** :
- Tous les fichiers vont dans `~/Warpinator/`
- Pas de sous-dossiers par expéditeur

**Organiser manuellement** :
- Créez des sous-dossiers : Travail, Personnel, etc.
- Déplacez les fichiers reçus
- Ou changez le dossier de réception dans les préférences

## Paramètres et options avancées

### Préférences générales

**Accès** : Menu **☰** → **Préférences** → **Général**

**Options disponibles** :

**Nom d'affichage** :
- Nom visible par les autres appareils
- Modifiez pour quelque chose de reconnaissable

**Emplacement des fichiers reçus** :
- Dossier de destination
- Cliquez sur **Parcourir** pour changer
- Exemple : `/home/vous/Documents/Transferts-Warpinator/`

**Accepter automatiquement les fichiers** :
- Évite la confirmation à chaque transfert
- Pratique mais moins sécurisé

**Demander avant d'écraser des fichiers** :
- Si un fichier avec le même nom existe
- Cochez pour demander confirmation
- Décochez pour écraser automatiquement

**Afficher les notifications** :
- Notifications de bureau lors des transferts
- Recommandé : Laissez activé

**Démarrer automatiquement** :
- Lance Warpinator au démarrage de l'ordinateur
- Pratique si vous l'utilisez souvent
- Désactivez pour économiser des ressources

### Code de groupe

**Sécurité supplémentaire** :

Le **code de groupe** est comme un mot de passe partagé entre appareils.

**Pourquoi l'utiliser ?** :
- Empêcher des inconnus de vous envoyer des fichiers
- Utile sur réseau professionnel ou partagé
- Créer un "groupe privé" d'appareils

**Configurer** :

1. **Préférences** → **Général**
2. **Code de groupe** : Entrez un code (minimum 6 caractères)
3. Cliquez sur **Appliquer**
4. Configurez le **même code** sur tous vos appareils

**Résultat** :
- Seuls les appareils avec le même code se voient
- Les autres sont invisibles

**Exemple** :
- Code : `famille2024`
- Tous les PC/téléphones de la famille utilisent ce code
- Voisins ou collègues ne peuvent pas envoyer de fichiers

### Paramètres réseau

**Préférences** → **Réseau**

**Port de transfert** :
- Par défaut : 42000
- Changez seulement si conflit avec autre application
- Doit être identique sur tous les appareils

**Port d'authentification** :
- Par défaut : 42001
- Idem, ne changez que si nécessaire

**Compresser les transferts** :
- Option future (pas encore implémentée dans toutes les versions)
- Compresserait les fichiers avant envoi
- Utile pour fichiers texte/code

**Interface réseau** :
- Sélectionne quelle carte réseau utiliser
- Automatique par défaut (recommandé)
- Changez si vous avez plusieurs réseaux (WiFi + Ethernet)

### Apparence

**Préférences** → **Apparence**

**Thème** :
- Clair, Sombre, ou Suivre le système
- Esthétique, n'affecte pas les fonctionnalités

**Taille des icônes** :
- Petite, Moyenne, Grande
- Pour la liste d'appareils

## Utilisation avec appareils mobiles

### Configuration sur Android

**Installation** :
1. Google Play Store → Recherchez "Warpinator"
2. Installez l'application

**Première utilisation** :
1. Ouvrez Warpinator
2. Accordez les permissions (stockage, réseau)
3. L'application détecte automatiquement les appareils

**Interface** :
- Liste des appareils détectés
- Bouton **+** pour envoyer des fichiers
- Notifications pour réceptions

**Envoyer depuis Android** :
1. Appuyez sur l'appareil destinataire
2. Bouton **Envoyer**
3. Sélectionnez fichiers/photos
4. Confirmez

**Recevoir sur Android** :
- Notification apparaît
- Acceptez ou refusez
- Fichiers dans `/Stockage interne/Warpinator/`

### Configuration sur iOS

**Installation** :
1. App Store → "Warpinator"
2. Installez

**Utilisation** :
- Similaire à Android
- Interface légèrement différente
- Même fonctionnalités de base

### Transferts PC ↔ Mobile

**PC vers téléphone** :
- Pratique pour photos, documents
- Exemple : Document PDF du PC vers téléphone pour lecture

**Téléphone vers PC** :
- Idéal pour photos prises avec le smartphone
- Plus rapide que câble USB ou cloud

**Astuce** :
- Gardez Warpinator en arrière-plan sur le téléphone
- Toujours prêt à recevoir

## Cas d'usage pratiques

### Partage de photos de vacances

**Scénario** : Vous revenez de vacances avec 500 photos sur votre laptop. Vous voulez les mettre sur votre PC fixe.

**Avec Warpinator** :
1. Les deux ordinateurs sur le même WiFi (maison)
2. Lancez Warpinator sur les deux
3. Sur le laptop : Sélectionnez le PC fixe
4. Envoyez le dossier `Vacances-2024` complet
5. Sur le PC : Acceptez
6. Transfert direct en quelques minutes

**Alternative traditionnelle** :
- Clé USB : Copier, débrancher, rebrancher
- Cloud : Upload lent + Téléchargement + Quota
- Câble réseau : Partage SMB complexe

### Collaboration au bureau

**Scénario** : Partage de présentations avec un collègue dans la salle de réunion.

**Avec Warpinator** :
1. Tous sur le WiFi de l'entreprise
2. Lancez Warpinator
3. Détection automatique des collègues
4. Envoyez la présentation directement
5. Pas besoin d'email ou clé USB

### Transfert PC ↔ Smartphone

**Scénario** : Vous prenez des photos avec votre téléphone, voulez les éditer sur PC.

**Avec Warpinator** :
1. Téléphone et PC sur le même WiFi
2. Warpinator sur les deux
3. Depuis le téléphone : Sélectionnez les photos → Envoyez au PC
4. Sur PC : Acceptez
5. Photos disponibles instantanément dans `~/Warpinator/`

**Inverse** : PDF du PC vers téléphone pour lire en déplacement

### Sauvegarder des fichiers importants

**Scénario** : Copie de sauvegarde rapide sur un second PC.

**Avec Warpinator** :
1. Sélectionnez vos dossiers importants
2. Envoyez-les vers le PC de sauvegarde
3. Transfert rapide sur réseau local
4. Vérifiez la réception
5. Fichiers dupliqués en sécurité

## Dépannage

### Les appareils ne se détectent pas

**Causes possibles et solutions** :

**1. Pas sur le même réseau** :
- Vérifiez que tous les appareils sont sur le **même WiFi**
- Ou tous sur Ethernet via le même routeur
- Impossible de détecter entre réseaux différents

**2. Pare-feu bloque** :
- Linux : `sudo ufw allow 42000/tcp` et `sudo ufw allow 42001/tcp`
- Windows : Autorisez Warpinator dans le pare-feu
- Routeur : Vérifiez qu'il n'isole pas les clients (mode "AP Isolation")

**3. Code de groupe différent** :
- Vérifiez que tous les appareils ont le **même code**
- Ou qu'aucun n'en a

**4. Warpinator pas lancé** :
- Assurez-vous que l'application tourne sur tous les appareils
- Vérifiez qu'elle n'est pas fermée en arrière-plan

**5. Service Avahi/mDNS** :
Sur Linux, vérifiez que le service de découverte fonctionne :
```bash
sudo systemctl status avahi-daemon
```
Si inactif :
```bash
sudo systemctl start avahi-daemon  
sudo systemctl enable avahi-daemon  
```

**6. IPv6 vs IPv4** :
- Certains réseaux ont des problèmes avec IPv6
- Essayez de désactiver IPv6 temporairement pour tester

**Solution de contournement** :
- Redémarrez Warpinator sur tous les appareils
- Redémarrez le routeur WiFi
- Reconnectez tous les appareils au WiFi

### Transfert très lent

**Causes et solutions** :

**1. WiFi faible** :
- Éloignement du routeur
- Obstacles (murs, étages)
- Solution : Rapprochez-vous du routeur ou utilisez Ethernet

**2. Réseau saturé** :
- Beaucoup d'appareils connectés
- Streaming vidéo simultané
- Solution : Attendez ou limitez l'usage réseau

**3. Vieux routeur** :
- WiFi ancien (802.11g)
- Solution : Upgrade vers WiFi AC ou WiFi 6

**4. Fichiers énormes** :
- Vidéos 4K, fichiers de plusieurs Go
- C'est normal que ça prenne du temps
- Solution : Patience, ou divisez en plusieurs transferts

**Vitesses attendues** :
- WiFi moderne (WiFi 5/AC) : 50-100 Mo/s
- WiFi ancien (WiFi 4/N) : 10-30 Mo/s
- Ethernet Gigabit : 100+ Mo/s

### Transfert échoue ou s'interrompt

**Problèmes possibles** :

**1. Connexion perdue** :
- Un appareil perd le WiFi
- Ordinateur mis en veille
- Solution : Restez connecté jusqu'à la fin

**2. Espace disque insuffisant** :
- Le destinataire n'a plus de place
- Vérifiez l'espace disponible
- Libérez de l'espace

**3. Fichier en cours d'utilisation** :
- Fichier ouvert dans une application
- Solution : Fermez le fichier avant envoi

**4. Permissions** :
- Pas d'accès en écriture au dossier de destination
- Solution : Vérifiez les permissions du dossier `~/Warpinator/`

### Warpinator ne démarre pas

**Sur Linux** :

**Réinstallation** :
```bash
sudo apt remove warpinator  
sudo apt install warpinator  
```

**Vérifier les logs** :
```bash
journalctl -u warpinator --no-pager | tail -50
```

**Lancer en mode debug** :
```bash
warpinator --debug
```

**Sur Windows** :
- Désinstallez et réinstallez
- Vérifiez les permissions administrateur

### Notifications ne s'affichent pas

**Solutions** :

1. **Préférences Warpinator** → Vérifiez que "Afficher les notifications" est coché
2. **Paramètres système** → **Notifications** → Vérifiez que Warpinator est autorisé
3. Redémarrez Warpinator

## Sécurité et bonnes pratiques

### Sécurité de Warpinator

**Chiffrement** :
- Toutes les connexions sont chiffrées (TLS)
- Impossible d'intercepter les fichiers en transit

**Code de groupe** :
- Protection supplémentaire
- Recommandé sur réseaux partagés

**Réseau local uniquement** :
- Warpinator ne fonctionne **que** sur réseau local
- Pas d'accès depuis Internet
- Vos fichiers ne quittent jamais votre réseau

### Bonnes pratiques

**Sur réseau de confiance (maison)** :
- Acceptation automatique : OK
- Pas de code de groupe : OK
- Démarrage automatique : Pratique

**Sur réseau public (café, hôtel, entreprise)** :
- Acceptation manuelle : Recommandé
- Code de groupe : Fortement recommandé
- Vérifiez toujours l'expéditeur avant d'accepter

**Général** :
- Ne recevez pas de fichiers d'appareils inconnus
- Scannez les fichiers reçus avec antivirus si doute
- Vérifiez le contenu avant d'ouvrir

### Limitations de sécurité

**Ce que Warpinator ne fait PAS** :
- Pas d'authentification forte (juste code de groupe)
- Pas de signature numérique des fichiers
- Pas de traçabilité (qui a envoyé quoi)

**Pour usage professionnel sensible** :
- Utilisez des solutions d'entreprise (SFTP, solutions MDM)
- Warpinator est adapté pour usage personnel et semi-professionnel

## Alternatives à Warpinator

### LocalSend

**Caractéristiques** :
- Similaire à Warpinator
- Multiplateforme (Linux, Windows, macOS, Android, iOS)
- Interface moderne et élégante
- Protocole différent

**Installation** :
```bash
flatpak install flathub org.localsend.localsend_app
```

**Avantages** :
- Plus moderne visuellement
- Actif développement
- Très populaire

### KDE Connect

**Caractéristiques** :
- Intégration complète PC ↔ Smartphone
- Transfert de fichiers
- Notifications partagées
- Contrôle multimédia
- Presse-papiers partagé

**Installation** :
```bash
sudo apt install kdeconnect
```

**Avantages** :
- Beaucoup plus de fonctionnalités
- Excellente intégration KDE
- Application mobile mature

**Inconvénients** :
- Plus complexe
- Nécessite configuration initiale (appairage)

### NitroShare

**Caractéristiques** :
- Simple et léger
- Multiplateforme
- Interface minimaliste

**Moins actif** que Warpinator ou LocalSend.

### Comparaison rapide

| Outil | Plateformes | Simplicité | Fonctionnalités | Recommandation |
|-------|-------------|------------|-----------------|----------------|
| **Warpinator** | Linux, Windows, Android, iOS | ⭐⭐⭐⭐⭐ | Transfert fichiers | Préinstallé Mint |
| **LocalSend** | Toutes | ⭐⭐⭐⭐⭐ | Transfert fichiers | Alternative moderne |
| **KDE Connect** | Linux, Android, Windows | ⭐⭐⭐ | Très nombreuses | Pour intégration complète |
| **NitroShare** | Toutes | ⭐⭐⭐⭐ | Transfert fichiers | Moins maintenu |

### Autres méthodes de partage

**Pour comparaison** :

**USB/Câble** :
- Avantages : Fonctionne toujours, rapide
- Inconvénients : Nécessite câble, manipulation

**Cloud (Drive, Dropbox)** :
- Avantages : Accessible partout
- Inconvénients : Internet requis, quotas, lenteur

**Email** :
- Avantages : Universel
- Inconvénients : Limite de taille (25 Mo), lent

**Bluetooth** :
- Avantages : Sans réseau
- Inconvénients : Très lent, portée limitée

**SMB/Samba** (partage réseau) :
- Avantages : Permanent, accès aux dossiers
- Inconvénients : Configuration complexe

**Warpinator** : Équilibre idéal entre simplicité et efficacité !

## Utilisation avancée

### Ligne de commande

Warpinator n'a pas vraiment de CLI, mais vous pouvez :

**Lancer en arrière-plan** :
```bash
warpinator &
```

**Avec options de debug** :
```bash
warpinator --debug
```

**Vérifier le service** :
```bash
ps aux | grep warpinator
```

### Intégration avec scripts

**Ouvrir Warpinator automatiquement** :

Exemple : Ouvrir Warpinator après connexion à un réseau spécifique.

```bash
#!/bin/bash
# warpinator-auto.sh

# Vérifier si connecté au réseau "HomeWiFi"
SSID=$(nmcli -t -f active,ssid dev wifi | grep '^yes' | cut -d: -f2)

if [ "$SSID" = "HomeWiFi" ]; then
    # Lancer Warpinator si pas déjà lancé
    if ! pgrep -x "warpinator" > /dev/null; then
        warpinator &
    fi
fi
```

**Automatiser avec NetworkManager** :
1. Enregistrez le script
2. Configurez-le pour s'exécuter lors de connexion WiFi

### Utilisation en entreprise

**Déploiement sur plusieurs postes** :

**Configuration centralisée** :

Les paramètres Warpinator sont dans : `~/.config/warpinator/`

**Distribuer une configuration commune** :
1. Configurez Warpinator sur un poste (code de groupe, etc.)
2. Copiez `~/.config/warpinator/` vers les autres postes
3. Tous auront les mêmes paramètres

**Code de groupe d'équipe** :
- Définissez un code pour l'équipe : `equipe-dev-2024`
- Seuls les membres de l'équipe se voient

**Restrictions** :
- Pas de gestion centralisée
- Pas de logs détaillés
- Pour besoin professionnel complexe, considérez des solutions d'entreprise

## Astuces et conseils

### Optimiser les transferts

**Pour vitesse maximale** :
1. Utilisez Ethernet si possible (plus rapide que WiFi)
2. Rapprochez-vous du routeur WiFi
3. Évitez les heures de forte utilisation du réseau
4. Fermez les autres applications réseau (streaming, téléchargements)

**Pour gros volumes** :
- Privilégiez les heures creuses
- Envoyez par lots plutôt que tout d'un coup
- Vérifiez que le PC ne se met pas en veille

### Organisation des fichiers

**Créer des sous-dossiers** :

Dans `~/Warpinator/`, créez :
- `Du-Laptop/`
- `Du-Telephone/`
- `De-Collègues/`

**Puis déplacez manuellement** après réception.

**Ou changez le dossier de destination** avant chaque transfert (moins pratique).

### Raccourcis et astuces

**Raccourci Nemo** :
- Sélection → Clic droit → "Envoyer via Warpinator" = Méthode la plus rapide !

**Épingler Warpinator** :
- Ajoutez Warpinator à la barre des tâches
- Clic droit sur l'icône → Épingler
- Accès instantané

**Notification de réception** :
- Gardez les notifications activées
- Vous savez immédiatement quand un fichier arrive

### Warpinator comme outil quotidien

**Cas d'usage réguliers** :

**Photographes** :
- Photos smartphone → PC pour édition
- PC → Smartphone pour partage sur réseaux

**Étudiants** :
- Notes du laptop → PC fixe
- Travaux de groupe entre collègues

**Professionnels** :
- Présentations laptop → PC de conférence
- Documents urgents entre collègues

**Famille** :
- Photos de vacances partagées instantanément
- Films du PC → Tablette des enfants

## FAQ (Questions fréquentes)

**Q : Warpinator fonctionne-t-il sans Internet ?**
R : Oui ! Vous avez juste besoin d'un réseau local (WiFi ou Ethernet). Internet n'est pas nécessaire.

**Q : Quelle est la limite de taille des fichiers ?**
R : Aucune limite technique. Vous pouvez transférer des fichiers de plusieurs Go, tant que vous avez l'espace disque.

**Q : Est-ce que mes fichiers passent par un serveur ?**
R : Non, le transfert est direct d'appareil à appareil (peer-to-peer). Rien ne passe par Internet ou serveur externe.

**Q : Puis-je utiliser Warpinator entre deux réseaux WiFi différents ?**
R : Non, tous les appareils doivent être sur le **même** réseau local.

**Q : Warpinator est-il compatible avec AirDrop d'Apple ?**
R : Non, ce sont deux protocoles différents. Mais Warpinator sur iOS peut communiquer avec Warpinator sur Linux/Windows.

**Q : Puis-je envoyer des fichiers vers plusieurs appareils simultanément ?**
R : Pas directement. Vous devez envoyer séparément vers chaque appareil.

**Q : Le destinataire peut-il voir d'où viennent les fichiers ?**
R : Oui, le nom de l'appareil expéditeur est affiché.

**Q : Les métadonnées des fichiers sont-elles préservées ?**
R : Oui, dates de création/modification sont conservées.

**Q : Puis-je programmer des transferts automatiques ?**
R : Pas nativement. Warpinator est manuel. Pour automatisation, utilisez rsync ou syncthing.

**Q : Warpinator consomme-t-il beaucoup de batterie sur mobile ?**
R : Non, très peu en arrière-plan. Uniquement lors des transferts actifs.

## Ressources et liens

### Documentation officielle

**Site officiel de Warpinator** :
- Pas de site dédié, fait partie de Linux Mint
- GitHub : [https://github.com/linuxmint/warpinator](https://github.com/linuxmint/warpinator)

**Mint Blog** :
- Annonces et nouveautés
- [https://blog.linuxmint.com/](https://blog.linuxmint.com/)

### Communauté

**Forums Linux Mint** :
- Section applications
- Aide et support

**Reddit** :
- r/linuxmint
- r/linux4noobs

### Applications mobiles

**Android** :
- Google Play : "Warpinator"
- F-Droid : "Warpinator"

**iOS** :
- App Store : "Warpinator"

### Versions Windows

**Warp** :
- [https://github.com/slowscript/warp](https://github.com/slowscript/warp)

**WinWarp** :
- Alternative Windows légère

## Conclusion

Warpinator est un excellent outil pour partager facilement des fichiers entre vos appareils sur votre réseau local. Sa simplicité, sa gratuité et son universalité en font une alternative idéale aux solutions propriétaires comme AirDrop.

**Points clés à retenir** :

- **Simple** : Détection automatique, interface intuitive
- **Rapide** : Transferts directs sur réseau local
- **Sécurisé** : Chiffrement, code de groupe optionnel
- **Gratuit** : Open source, sans limite
- **Multiplateforme** : Linux, Windows, Android, iOS

**Pour commencer** :
1. Lancez Warpinator sur vos appareils
2. Assurez-vous qu'ils sont sur le même WiFi
3. Sélectionnez un destinataire et envoyez vos fichiers !

Que vous vouliez transférer des photos de vacances, partager des documents de travail, ou simplement déplacer des fichiers entre vos appareils, Warpinator rend tout cela simple et efficace. Essayez-le dès aujourd'hui, vous ne reviendrez plus aux clés USB !

---


⏭️ [Web Apps Manager (Transformer des sites en applications)](/05-applications-essentielles-et-outils-mint/09-web-apps-manager.md)
