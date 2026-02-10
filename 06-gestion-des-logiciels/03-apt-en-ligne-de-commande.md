🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.3 APT en ligne de commande (apt, apt-get, dpkg)

## Introduction

**APT** (Advanced Package Tool) est le système de gestion de paquets qui fonctionne en arrière-plan du Gestionnaire de logiciels graphique que nous avons vu précédemment. C'est l'outil en ligne de commande le plus puissant pour gérer les logiciels sous Linux Mint et Ubuntu.

Imaginez le Gestionnaire de logiciels comme une boutique avec une belle vitrine, et APT comme l'entrepôt qui se trouve derrière : plus brut, mais avec un accès direct à tout et beaucoup plus de contrôle.

## Pourquoi utiliser la ligne de commande ?

Vous vous demandez peut-être : "Pourquoi utiliser des commandes alors que j'ai une interface graphique ?"

### Avantages de la ligne de commande

1. **Rapidité** : Installer un logiciel en une seule ligne au lieu de plusieurs clics
2. **Puissance** : Faire des opérations impossibles avec l'interface graphique
3. **Automatisation** : Créer des scripts pour installer plusieurs logiciels d'un coup
4. **Débogage** : Messages d'erreur plus détaillés pour résoudre les problèmes
5. **Efficacité** : Moins de ressources système utilisées
6. **Support en ligne** : La plupart des tutoriels utilisent des commandes

### Quand utiliser APT en ligne de commande ?

- Quand vous suivez un tutoriel qui donne des commandes
- Pour installer rapidement plusieurs logiciels
- Quand le gestionnaire graphique ne fonctionne pas
- Pour des opérations de maintenance avancées
- Quand vous voulez mieux comprendre ce qui se passe

**Rassurez-vous** : Vous n'êtes pas obligé d'utiliser la ligne de commande. Le Gestionnaire de logiciels graphique reste parfait pour 90% des besoins quotidiens.

## APT, APT-GET et DPKG : Quelle différence ?

Il existe trois outils principaux pour gérer les paquets. Voici comment les distinguer :

### dpkg (Debian Package)
- **Le plus bas niveau** : Gère directement les fichiers .deb
- **N'utilise pas Internet** : Travaille uniquement avec des fichiers locaux
- **Ne gère pas les dépendances** : Ne télécharge pas les dépendances automatiquement
- **Usage** : Rarement utilisé directement, sauf cas spécifiques

### apt-get (ancien outil)
- **L'ancêtre** : Premier outil en ligne de commande pour gérer les paquets
- **Très stable** : Utilisé depuis des décennies
- **Syntaxe stricte** : Commandes précises mais moins conviviales
- **Usage** : Toujours fonctionnel, mais remplacé par `apt`

### apt (outil moderne - RECOMMANDÉ)
- **Version modernisée** : Combine le meilleur de apt-get et apt-cache
- **Plus convivial** : Barre de progression, couleurs, meilleurs messages
- **Syntaxe simplifiée** : Commandes plus logiques et faciles à retenir
- **Usage** : **C'est celui à utiliser en priorité**

**Règle simple** : Utilisez `apt` pour tout. N'utilisez `apt-get` ou `dpkg` que si un tutoriel spécifique le demande.

## Ouvrir le terminal

Avant d'utiliser APT, il faut ouvrir le terminal (l'interface en ligne de commande).

### Méthode 1 : Menu principal
1. Cliquez sur le **Menu**
2. Tapez "**Terminal**"
3. Cliquez sur l'application **Terminal**

### Méthode 2 : Raccourci clavier
Appuyez sur **Ctrl + Alt + T** (le raccourci le plus rapide !)

### Méthode 3 : Clic droit
1. Cliquez droit sur le bureau ou dans un dossier
2. Sélectionnez **"Ouvrir dans un terminal"**

Une fenêtre noire (ou de couleur selon votre thème) s'ouvre. C'est le terminal. Ne vous laissez pas intimider, c'est juste un autre moyen de communiquer avec votre ordinateur !

## Comprendre sudo

La plupart des commandes APT nécessitent `sudo` devant. Mais qu'est-ce que c'est ?

### Qu'est-ce que sudo ?

**sudo** signifie "**S**uper**U**ser **DO**" (faire en tant que super-utilisateur).

C'est comme dire à votre système : "Je suis l'administrateur, j'ai le droit de faire cette action importante."

### Pourquoi c'est nécessaire ?

Installer, modifier ou supprimer des logiciels système nécessite des privilèges administrateur pour :
- **Protéger votre système** : Éviter que n'importe qui puisse modifier le système
- **Prévenir les erreurs** : Vous fait réfléchir à deux fois avant d'agir
- **Tracer les actions** : Garde un historique de qui a fait quoi

### Comment utiliser sudo ?

```bash
sudo commande
```

Après avoir tapé une commande avec `sudo`, le système vous demandera votre **mot de passe**.

**Points importants :**
- Vous ne verrez **rien s'afficher** pendant que vous tapez votre mot de passe (c'est normal, c'est pour la sécurité)
- Tapez votre mot de passe et appuyez sur **Entrée**
- Le système se souvient pendant 15 minutes (pas besoin de retaper à chaque fois)

## Mettre à jour la liste des paquets

Avant d'installer ou de mettre à jour quoi que ce soit, il faut rafraîchir la liste des paquets disponibles.

### La commande update

```bash
sudo apt update
```

**Ce que fait cette commande :**
- Se connecte aux serveurs de dépôts
- Télécharge la liste des paquets disponibles
- Vérifie s'il existe de nouvelles versions
- Ne modifie RIEN sur votre système (juste une vérification)

**Quand l'utiliser :**
- Avant d'installer un nouveau logiciel
- Avant de mettre à jour le système
- Une fois par jour si vous installez beaucoup de choses
- Après avoir ajouté un nouveau dépôt

**Exemple de sortie :**
```
Atteint:1 http://packages.linuxmint.com vera InRelease  
Réception de:2 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]  
Lecture des listes de paquets... Fait  
Construction de l'arbre des dépendances... Fait  
4 paquets peuvent être mis à jour. Exécutez « apt list --upgradable » pour les voir.
```

C'est normal ! Le système vous informe simplement de ce qu'il a trouvé.

## Rechercher un paquet

Avant d'installer un logiciel, vous pouvez vérifier s'il est disponible.

### Recherche simple

```bash
apt search nom-du-logiciel
```

Exemple :
```bash
apt search gimp
```

**Résultat** : Liste de tous les paquets contenant "gimp" dans leur nom ou description.

### Recherche plus précise

Pour avoir des informations détaillées sur un paquet spécifique :

```bash
apt show nom-du-paquet
```

Exemple :
```bash
apt show gimp
```

**Résultat** : Affiche la description complète, la version, la taille, les dépendances, etc.

### Lister les paquets installés

Pour voir tous les paquets déjà installés sur votre système :

```bash
apt list --installed
```

Pour chercher un paquet spécifique dans vos installations :

```bash
apt list --installed | grep nom-du-logiciel
```

## Installer un paquet

C'est la commande la plus utilisée : installer un nouveau logiciel.

### Syntaxe de base

```bash
sudo apt install nom-du-paquet
```

### Exemples concrets

Installer VLC :
```bash
sudo apt install vlc
```

Installer GIMP :
```bash
sudo apt install gimp
```

Installer plusieurs paquets en une fois :
```bash
sudo apt install vlc gimp inkscape
```

### Ce qui se passe pendant l'installation

1. **Calcul des dépendances** : APT détermine ce qui est nécessaire
2. **Affichage du plan** : Vous voyez ce qui va être installé et la taille
3. **Confirmation** : On vous demande de confirmer (tapez **y** puis Entrée, ou **n** pour annuler)
4. **Téléchargement** : Les paquets sont téléchargés depuis Internet
5. **Installation** : Les paquets sont installés sur votre système
6. **Configuration** : Les logiciels sont configurés automatiquement

### Options utiles

#### Installation sans confirmation

```bash
sudo apt install -y nom-du-paquet
```

L'option `-y` répond automatiquement "oui" à toutes les questions. Utile pour les scripts, mais attention !

#### Simulation (sans vraiment installer)

```bash
apt install --dry-run nom-du-paquet
```

Montre ce qui serait installé, sans rien modifier. Parfait pour vérifier avant d'agir.

#### Télécharger sans installer

```bash
sudo apt install --download-only nom-du-paquet
```

Télécharge les fichiers mais ne les installe pas. Utile si vous voulez préparer une installation hors ligne.

## Mettre à jour les paquets

Garder votre système à jour est essentiel pour la sécurité et la stabilité.

### Mise à jour classique

```bash
sudo apt upgrade
```

**Ce que fait cette commande :**
- Met à jour tous les paquets qui ont une nouvelle version
- N'installe PAS de nouveaux paquets
- Ne supprime PAS de paquets existants
- C'est la mise à jour la plus sûre

### Mise à jour complète

```bash
sudo apt full-upgrade
```

**Ce que fait cette commande :**
- Met à jour tous les paquets
- Peut installer de nouveaux paquets si nécessaire
- Peut supprimer des paquets obsolètes
- Plus agressive mais plus complète

**Quelle commande utiliser ?**
- **Pour les débutants** : Utilisez `apt upgrade` (plus sûr)
- **Pour les utilisateurs avancés** : `apt full-upgrade` pour une mise à jour complète

### Mise à jour d'un paquet spécifique

```bash
sudo apt install --only-upgrade nom-du-paquet
```

Met à jour uniquement ce paquet, sans toucher aux autres.

### Voir les paquets qui peuvent être mis à jour

```bash
apt list --upgradable
```

Affiche la liste des paquets pour lesquels une mise à jour est disponible.

## Supprimer un paquet

Plusieurs niveaux de suppression existent, selon ce que vous voulez garder ou non.

### Suppression simple

```bash
sudo apt remove nom-du-paquet
```

**Ce qui est supprimé :**
- Le logiciel lui-même
- Ses exécutables

**Ce qui est conservé :**
- Les fichiers de configuration
- Vos données personnelles

**Quand l'utiliser :** Si vous pensez peut-être réinstaller le logiciel plus tard.

### Suppression complète (purge)

```bash
sudo apt purge nom-du-paquet
```

**Ce qui est supprimé :**
- Le logiciel
- Ses fichiers de configuration système
- Tout ce qui est lié au paquet

**Ce qui est conservé :**
- Vos données personnelles (dans /home)

**Quand l'utiliser :** Quand vous êtes sûr de ne plus vouloir ce logiciel.

### Supprimer les dépendances inutiles

Après avoir supprimé un logiciel, certaines dépendances peuvent rester installées alors qu'elles ne servent plus à rien.

```bash
sudo apt autoremove
```

**Ce que fait cette commande :**
- Détecte les paquets qui ne sont plus nécessaires
- Propose de les supprimer pour libérer de l'espace
- Nettoie votre système

**Conseil :** Utilisez cette commande régulièrement (par exemple, une fois par mois).

### Exemple complet de désinstallation propre

Pour supprimer complètement un logiciel et nettoyer :

```bash
sudo apt purge nom-du-paquet  
sudo apt autoremove  
```

## Nettoyer le système

Avec le temps, des fichiers temporaires et des caches s'accumulent. Voici comment nettoyer.

### Nettoyer le cache des paquets téléchargés

Quand vous installez un logiciel, APT télécharge des fichiers .deb et les garde en cache.

```bash
sudo apt clean
```

**Ce que fait cette commande :**
- Supprime TOUS les fichiers .deb du cache
- Libère de l'espace disque
- Sans danger, vous pouvez les retélécharger si nécessaire

### Nettoyer partiellement

```bash
sudo apt autoclean
```

**Ce que fait cette commande :**
- Supprime uniquement les fichiers .deb obsolètes
- Garde les versions actuelles
- Plus prudent que `apt clean`

### Commande complète de maintenance

Pour un nettoyage complet de votre système :

```bash
sudo apt update  
sudo apt upgrade  
sudo apt autoremove  
sudo apt autoclean  
```

**Explication de cette séquence :**
1. Met à jour la liste des paquets
2. Installe les mises à jour disponibles
3. Supprime les paquets inutiles
4. Nettoie le cache

**Fréquence recommandée :** Une fois par semaine ou par mois.

## Gérer les fichiers .deb manuellement avec dpkg

Parfois, vous téléchargez un fichier .deb depuis un site web (comme Chrome, Skype, etc.). Voici comment l'installer.

### Installer un fichier .deb

```bash
sudo dpkg -i chemin/vers/le/fichier.deb
```

Exemple :
```bash
sudo dpkg -i ~/Téléchargements/google-chrome-stable_current_amd64.deb
```

### Problème fréquent : Dépendances manquantes

Souvent, après avoir installé un .deb avec dpkg, vous aurez une erreur de dépendances. La solution :

```bash
sudo apt install -f
```

L'option `-f` (fix-broken) répare automatiquement les dépendances cassées.

### Séquence complète pour installer un .deb

```bash
sudo dpkg -i fichier.deb  
sudo apt install -f  
```

### Lister les paquets installés

```bash
dpkg -l
```

Affiche tous les paquets installés sur votre système.

### Chercher un paquet spécifique

```bash
dpkg -l | grep nom-du-paquet
```

### Voir les fichiers installés par un paquet

```bash
dpkg -L nom-du-paquet
```

Montre tous les fichiers que ce paquet a installés sur votre système.

## Gérer les dépendances

Les dépendances sont des bibliothèques ou d'autres paquets nécessaires au fonctionnement d'un logiciel.

### Voir les dépendances d'un paquet

```bash
apt depends nom-du-paquet
```

Affiche la liste de tout ce dont ce paquet a besoin pour fonctionner.

### Voir quels paquets dépendent d'un paquet

```bash
apt rdepends nom-du-paquet
```

Affiche la liste des paquets qui utilisent ce paquet.

### Résoudre les dépendances cassées

Si vous avez un message d'erreur concernant des dépendances :

```bash
sudo apt install -f
```

ou

```bash
sudo dpkg --configure -a
```

Ces commandes tentent de réparer automatiquement les problèmes de dépendances.

## Verrouiller/déverrouiller des paquets

Parfois, vous voulez empêcher un paquet d'être mis à jour (par exemple, si une nouvelle version pose problème).

### Empêcher la mise à jour (hold)

```bash
sudo apt-mark hold nom-du-paquet
```

Le paquet ne sera plus mis à jour automatiquement.

### Autoriser à nouveau les mises à jour (unhold)

```bash
sudo apt-mark unhold nom-du-paquet
```

### Voir les paquets verrouillés

```bash
apt-mark showhold
```

## Commandes de diagnostic

Pour obtenir des informations sur votre système et les paquets.

### Vérifier les mises à jour disponibles

```bash
apt list --upgradable
```

### Voir les paquets installés manuellement

```bash
apt-mark showmanual
```

### Voir la version d'APT

```bash
apt --version
```

### Vérifier l'intégrité des paquets

```bash
sudo dpkg --verify
```

## Comparer apt et apt-get

Voici un tableau de correspondance si vous tombez sur de vieux tutoriels utilisant apt-get :

| Commande moderne (apt) | Ancienne commande (apt-get) | Action |
|------------------------|----------------------------|---------|
| `apt update` | `apt-get update` | Mettre à jour la liste |
| `apt upgrade` | `apt-get upgrade` | Mettre à jour les paquets |
| `apt full-upgrade` | `apt-get dist-upgrade` | Mise à jour complète |
| `apt install paquet` | `apt-get install paquet` | Installer |
| `apt remove paquet` | `apt-get remove paquet` | Supprimer |
| `apt purge paquet` | `apt-get purge paquet` | Supprimer complètement |
| `apt autoremove` | `apt-get autoremove` | Nettoyer dépendances |
| `apt search paquet` | `apt-cache search paquet` | Rechercher |
| `apt show paquet` | `apt-cache show paquet` | Afficher infos |
| `apt list --installed` | `dpkg --get-selections` | Lister installés |

**Conseil** : Privilégiez toujours les commandes `apt` (colonne de gauche), plus modernes et conviviales.

## Exemples pratiques courants

Voici des situations réelles et les commandes à utiliser :

### Installer un logiciel de développement complet

```bash
sudo apt update  
sudo apt install build-essential git curl  
```

### Installer des codecs multimédia

```bash
sudo apt install ubuntu-restricted-extras
```

### Installer un serveur web de base

```bash
sudo apt install apache2 mysql-server php
```

### Mettre à jour tout le système

```bash
sudo apt update && sudo apt upgrade -y
```

L'opérateur `&&` enchaîne les commandes : la seconde ne s'exécute que si la première réussit.

### Installer plusieurs outils en une fois

```bash
sudo apt install vim htop tree curl wget git neofetch
```

## Comprendre les messages d'erreur

### "E: Impossible de verrouiller /var/lib/dpkg/lock"

**Cause** : Un autre processus utilise APT (Gestionnaire de logiciels ouvert, autre terminal, mise à jour en cours).

**Solution** :
1. Fermez tous les gestionnaires de paquets graphiques
2. Attendez quelques minutes
3. En dernier recours :
```bash
sudo killall apt apt-get  
sudo dpkg --configure -a  
```

### "E: Unable to locate package"

**Cause** : Le paquet n'existe pas ou la liste n'est pas à jour.

**Solution** :
```bash
sudo apt update
```
Puis réessayez. Si ça ne marche toujours pas, vérifiez l'orthographe ou cherchez le nom exact.

### "E: Unmet dependencies"

**Cause** : Des dépendances manquent ou sont en conflit.

**Solution** :
```bash
sudo apt install -f
```

### "404 Not Found" lors de l'update

**Cause** : Un dépôt n'existe plus ou l'URL a changé.

**Solution** : Vérifiez vos sources de logiciels dans le menu Système > Gestion des logiciels > Sources de logiciels.

## Conseils de sécurité

### Ne jamais exécuter une commande sans la comprendre

- **Lisez avant de copier-coller** : Assurez-vous de comprendre ce que fait la commande
- **Méfiez-vous des commandes trouvées sur Internet** : Vérifiez la source
- **Évitez les commandes qui contiennent :**
  - `rm -rf /` (supprime tout votre système !)
  - `dd` sans savoir ce que vous faites
  - `chmod 777` sur des fichiers système

### Utilisez sudo avec précaution

- Ne tapez `sudo` que pour des actions qui le nécessitent vraiment
- Vérifiez toujours la commande avant d'entrer votre mot de passe
- Ne restez pas en mode root (`sudo su`) sans raison

### Faites des sauvegardes avant les grosses modifications

Avant d'installer beaucoup de choses ou de faire des changements importants :
```bash
sudo timeshift --create --comments "Avant installation"
```

## Astuces d'efficacité

### Auto-complétion avec Tab

Tapez les premières lettres d'un nom de paquet puis appuyez sur **Tab** :
```bash
sudo apt install fire[Tab]
```
Devient automatiquement :
```bash
sudo apt install firefox
```

### Historique des commandes

- **Flèche haut** : Rappelle les commandes précédentes
- **Ctrl + R** : Recherche dans l'historique
- `history` : Affiche tout l'historique

### Alias pour les commandes fréquentes

Ajoutez dans votre `~/.bashrc` :
```bash
alias maj='sudo apt update && sudo apt upgrade'  
alias install='sudo apt install'  
alias search='apt search'  
```

Après avoir rechargé le terminal, vous pourrez taper simplement `maj` pour mettre à jour !

### Commandes en une ligne

Grâce à `&&`, enchaînez plusieurs actions :
```bash
sudo apt update && sudo apt upgrade && sudo apt autoremove
```

## Créer un script de maintenance

Créez un fichier `maintenance.sh` :

```bash
#!/bin/bash

echo "=== Mise à jour de la liste des paquets ==="  
sudo apt update  

echo "=== Installation des mises à jour ==="  
sudo apt upgrade -y  

echo "=== Suppression des paquets inutiles ==="  
sudo apt autoremove -y  

echo "=== Nettoyage du cache ==="  
sudo apt autoclean  

echo "=== Maintenance terminée ! ==="
```

Rendez-le exécutable :
```bash
chmod +x maintenance.sh
```

Utilisez-le :
```bash
./maintenance.sh
```

## Différences avec d'autres distributions

APT est spécifique à Debian, Ubuntu et Linux Mint. Voici les équivalents pour d'autres distributions :

| Distribution | Gestionnaire | Commande d'installation |
|--------------|--------------|-------------------------|
| Linux Mint, Ubuntu, Debian | APT | `apt install` |
| Fedora, Red Hat, CentOS | DNF | `dnf install` |
| Arch Linux, Manjaro | Pacman | `pacman -S` |
| openSUSE | Zypper | `zypper install` |

## Ressources et aide

### Aide intégrée

```bash
man apt
```

Affiche le manuel complet de APT (appuyez sur **Q** pour quitter).

```bash
apt --help
```

Affiche une aide rapide avec les commandes principales.

### Aide pour une commande spécifique

```bash
apt install --help
```

### Vérifier la syntaxe

Si vous n'êtes pas sûr d'une commande, utilisez d'abord `--dry-run` pour simuler.

## Conclusion

APT en ligne de commande peut sembler intimidant au début, mais c'est un outil extrêmement puissant qui vous donne un contrôle total sur votre système. Avec le temps, vous trouverez que c'est souvent plus rapide et plus efficace que l'interface graphique.

**Points clés à retenir :**

- **apt** est l'outil moderne à privilégier
- **sudo apt update** avant toute installation
- **sudo apt upgrade** pour les mises à jour
- **sudo apt install** pour installer
- **sudo apt remove** pour désinstaller
- **sudo apt autoremove** pour nettoyer
- Lisez et comprenez avant d'exécuter
- L'interface graphique reste parfaitement valable pour un usage quotidien

**Progression recommandée :**
1. Commencez par les commandes de base (update, upgrade, install)
2. Apprenez à rechercher et obtenir des informations
3. Maîtrisez la suppression et le nettoyage
4. Explorez les options avancées quand vous êtes à l'aise

Dans le prochain chapitre, nous découvrirons **les dépôts et PPA**, qui vous permettront d'ajouter de nouvelles sources de logiciels à votre système.

---


⏭️ [Les dépôts et PPA](/06-gestion-des-logiciels/04-les-depots-et-ppa.md)
