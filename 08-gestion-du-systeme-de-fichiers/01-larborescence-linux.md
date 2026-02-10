🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.1 L'arborescence Linux

## Introduction

L'une des différences les plus marquantes entre Linux et Windows réside dans l'organisation des fichiers. Alors que Windows utilise des lettres de lecteurs (C:, D:, E:, etc.), Linux adopte une approche totalement différente avec une **arborescence unique** qui commence à la racine `/`.

Cette structure peut sembler déroutante au début, mais elle est en réalité très logique et cohérente une fois que l'on en comprend les principes de base.

## La racine : le point de départ

Sous Linux, tout commence par la **racine**, symbolisée par le caractère `/` (slash). C'est le sommet de l'arborescence, et tous les autres répertoires et fichiers descendent de cette racine.

### Comparaison avec Windows

| Windows | Linux |
|---------|-------|
| C:\, D:\, E:\ (plusieurs racines) | / (une seule racine) |
| C:\Users\VotreNom | /home/votrenom |
| C:\Program Files | /usr ou /opt |
| C:\Windows | /boot, /etc, /lib |

## Les répertoires principaux

Voici les répertoires les plus importants que vous rencontrerez sous Linux Mint. Ne vous inquiétez pas, vous n'aurez pas besoin de tous les connaître par cœur pour utiliser votre système au quotidien !

### `/home` - Votre espace personnel

**C'est le plus important pour vous en tant qu'utilisateur.**

- **Ce qu'il contient** : Vos documents, images, musique, vidéos, téléchargements, fichiers de configuration personnels
- **Équivalent Windows** : C:\Users\VotreNom
- **Structure** : `/home/votrenom/` (où "votrenom" est votre nom d'utilisateur)

À l'intérieur de votre dossier personnel, vous trouverez des sous-dossiers familiers :
- `Documents/`
- `Téléchargements/`
- `Images/`
- `Musique/`
- `Vidéos/`
- `Bureau/`

💡 **Astuce** : Dans le gestionnaire de fichiers Nemo, vous pouvez accéder rapidement à votre dossier personnel en cliquant sur "Dossier personnel" dans la barre latérale, ou en tapant `~` dans la barre d'adresse (le tilde ~ est un raccourci qui représente votre dossier personnel).

### `/etc` - Configuration du système

**Prononcez "et-cé" ou "etcetera"**

- **Ce qu'il contient** : Tous les fichiers de configuration du système et des applications
- **Équivalent Windows** : Un peu comme le registre Windows, mais en fichiers texte lisibles
- **Exemples de fichiers importants** :
  - `/etc/fstab` : configuration des disques et partitions
  - `/etc/hosts` : correspondance entre noms de domaine et adresses IP
  - `/etc/apt/sources.list` : sources des logiciels

⚠️ **Attention** : La plupart des fichiers dans `/etc` nécessitent des droits administrateur (sudo) pour être modifiés. C'est une protection pour éviter de casser le système par inadvertance.

### `/var` - Données variables

**Variable = qui change fréquemment**

- **Ce qu'il contient** : Fichiers qui changent pendant le fonctionnement du système
- **Sous-dossiers importants** :
  - `/var/log/` : fichiers journaux (logs) du système
  - `/var/cache/` : fichiers temporaires en cache
  - `/var/tmp/` : fichiers temporaires qui persistent entre les redémarrages
  - `/var/www/` : fichiers de sites web (si vous avez un serveur web)

💡 **Bon à savoir** : Si votre disque se remplit mystérieusement, `/var/log/` est souvent le coupable avec des fichiers journaux qui grossissent.

### `/usr` - Programmes utilisateur

**USR = Unix System Resources (et non "user" comme on pourrait le croire)**

- **Ce qu'il contient** : La majorité des applications et programmes installés
- **Structure** :
  - `/usr/bin/` : programmes et commandes utilisables par tous
  - `/usr/lib/` : bibliothèques partagées par les programmes
  - `/usr/share/` : données partagées (icônes, thèmes, documentation)
  - `/usr/local/` : programmes installés manuellement (hors gestionnaire de paquets)

**Équivalent Windows** : C:\Program Files

### `/tmp` - Fichiers temporaires

- **Ce qu'il contient** : Fichiers temporaires créés par les applications
- **Particularité** : Le contenu est généralement **effacé au redémarrage** du système
- **Utilisation** : Les applications y stockent des données dont elles ont besoin temporairement

💡 **Astuce** : Vous pouvez utiliser `/tmp` comme zone de brouillon pour des fichiers dont vous n'avez pas besoin de façon permanente.

### `/boot` - Démarrage du système

- **Ce qu'il contient** : Tout ce qui est nécessaire au démarrage de Linux
- **Fichiers importants** :
  - Le noyau Linux (kernel)
  - Le chargeur de démarrage GRUB
  - L'image initiale du système (initrd)

⚠️ **Important** : Ne touchez pas à ce dossier sauf si vous savez vraiment ce que vous faites !

### `/opt` - Applications optionnelles

- **Ce qu'il contient** : Logiciels tiers installés en un seul bloc
- **Exemples** : Google Chrome, Spotify, ou d'autres applications commerciales
- **Caractéristique** : Chaque application a son propre sous-dossier complet

### `/root` - Dossier de l'administrateur

⚠️ **À ne pas confondre avec `/` (la racine du système) !**

- **Ce qu'il contient** : Le dossier personnel de l'utilisateur root (super-administrateur)
- **Équivalent** : Comme `/home/votrenom` mais pour le compte root
- **Accès** : Normalement, vous n'avez pas besoin d'y accéder en tant qu'utilisateur normal

### `/bin` et `/sbin` - Commandes essentielles

- **`/bin`** : Commandes de base disponibles pour tous les utilisateurs (ls, cp, mv, cat, etc.)
- **`/sbin`** : Commandes système pour l'administration (ifconfig, reboot, shutdown, etc.)

📝 **Note** : Sur les systèmes récents, ces dossiers sont souvent des liens symboliques vers `/usr/bin` et `/usr/sbin`.

### `/lib` - Bibliothèques système

- **Ce qu'il contient** : Bibliothèques partagées essentielles au démarrage et aux commandes de `/bin` et `/sbin`
- **Équivalent Windows** : Comme les fichiers .dll
- **Variantes** : `/lib64` pour les systèmes 64 bits

### `/dev` - Périphériques (devices)

**Concept unique à Linux : tout est fichier, même le matériel !**

- **Ce qu'il contient** : Fichiers spéciaux représentant les périphériques matériels
- **Exemples** :
  - `/dev/sda` : premier disque dur
  - `/dev/sda1` : première partition du premier disque
  - `/dev/usb` : périphériques USB
  - `/dev/null` : "trou noir" qui absorbe toute donnée (utile en programmation)

### `/media` et `/mnt` - Points de montage

- **`/media`** : Montage automatique des périphériques amovibles (clés USB, CD/DVD, disques externes)
  - Exemple : `/media/votrenom/MaCleUSB`

- **`/mnt`** : Point de montage pour montages temporaires manuels
  - Utilisé quand vous montez manuellement une partition ou un disque réseau

### `/proc` et `/sys` - Informations système virtuelles

**Ce ne sont pas de vrais fichiers sur le disque !**

- **`/proc`** : Interface vers les informations du noyau et des processus en cours
  - `/proc/cpuinfo` : informations sur le processeur
  - `/proc/meminfo` : informations sur la mémoire

- **`/sys`** : Interface vers les informations sur le matériel et les pilotes

💡 **Curiosité** : Tapez `cat /proc/cpuinfo` dans le terminal pour voir les détails de votre processeur !

### `/run` - Données d'exécution

- **Ce qu'il contient** : Informations sur le système depuis le dernier démarrage
- **Particularité** : Stocké en RAM, effacé à chaque redémarrage
- **Utilisation** : Fichiers PID (identifiants de processus), sockets, etc.

## Visualiser l'arborescence

### Avec le gestionnaire de fichiers

1. Ouvrez Nemo (le gestionnaire de fichiers)
2. Dans la barre d'adresse, tapez `/` et appuyez sur Entrée
3. Vous verrez tous les répertoires racine

### Avec le terminal

Installez et utilisez la commande `tree` pour une vue graphique :

```bash
sudo apt install tree  
tree -L 1 /  
```

Cette commande affiche l'arborescence à partir de la racine (`/`) sur un niveau de profondeur (`-L 1`).

## Permissions et propriété

Un concept important de l'arborescence Linux est que chaque fichier et dossier a :
- Un **propriétaire** (généralement l'utilisateur qui l'a créé)
- Un **groupe**
- Des **permissions** (lecture, écriture, exécution)

C'est pourquoi vous ne pouvez pas modifier n'importe quel fichier système sans les droits administrateur (sudo).

## Chemins absolus vs chemins relatifs

### Chemin absolu
Commence toujours par `/` et indique l'emplacement complet depuis la racine :
- `/home/pierre/Documents/rapport.pdf`
- `/etc/apt/sources.list`

### Chemin relatif
Part de votre position actuelle :
- Si vous êtes dans `/home/pierre/`, alors `Documents/rapport.pdf` suffit
- `..` remonte d'un niveau (le dossier parent)
- `.` représente le dossier actuel

## Astuces pour les débutants

### 1. Restez dans votre `/home`
Pour un usage quotidien, vous travaillerez principalement dans votre dossier `/home/votrenom/`. C'est votre espace sûr où vous avez tous les droits.

### 2. Ne supprimez jamais de dossiers système
Si vous ne savez pas à quoi sert un dossier à la racine (`/`), ne le touchez pas ! Le système en a besoin pour fonctionner.

### 3. Utilisez les raccourcis
- `~` = votre dossier personnel (`/home/votrenom`)
- `/` = la racine du système
- `..` = dossier parent
- `.` = dossier actuel

### 4. Les fichiers cachés
Sous Linux, les fichiers et dossiers dont le nom commence par un point (`.`) sont cachés. Votre dossier personnel en contient beaucoup pour la configuration des applications.

Pour les voir dans Nemo : **Menu > Afficher les fichiers cachés** (ou Ctrl+H)

## Récapitulatif visuel

```
/                          (racine - tout part d'ici)
├── home/                  (dossiers personnels des utilisateurs)
│   ├── pierre/            (VOTRE espace - vous avez tous les droits)
│   │   ├── Documents/
│   │   ├── Images/
│   │   ├── Téléchargements/
│   │   └── ...
│   └── marie/
├── etc/                   (configuration système)
├── var/                   (données variables - logs, cache)
├── usr/                   (programmes et applications)
├── tmp/                   (fichiers temporaires - nettoyé au redémarrage)
├── boot/                  (fichiers de démarrage)
├── opt/                   (applications tierces)
├── bin/                   (commandes de base)
├── lib/                   (bibliothèques système)
├── dev/                   (périphériques matériels)
├── media/                 (clés USB, CD/DVD montés automatiquement)
├── mnt/                   (montages manuels temporaires)
├── proc/                  (infos système virtuelles)
├── sys/                   (infos matériel virtuelles)
└── run/                   (données temporaires en RAM)
```

## Conclusion

L'arborescence Linux peut sembler complexe au premier abord, mais elle est en réalité très organisée et logique. Pour un usage quotidien, vous passerez 99% de votre temps dans votre dossier `/home/votrenom/`, tout comme vous restiez dans `C:\Users\VotreNom\` sous Windows.

Les autres dossiers du système fonctionnent en arrière-plan pour faire tourner votre Linux Mint. Vous n'avez pas besoin de les comprendre en détail tout de suite, mais savoir qu'ils existent et à quoi ils servent vous aidera progressivement à mieux maîtriser votre système.

**À retenir** :
- `/` est la racine - tout part de là
- `/home/votrenom` est votre espace personnel
- `/etc` contient les configurations
- `/usr` contient les programmes
- `/var` contient les données qui changent (logs, cache)
- `/tmp` contient les fichiers temporaires

Avec le temps, cette structure vous paraîtra aussi naturelle que celle de Windows !

⏭️ [Les partitions et points de montage](/08-gestion-du-systeme-de-fichiers/02-les-partitions-et-points-de-montage.md)
