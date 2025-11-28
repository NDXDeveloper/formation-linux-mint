🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.8 Installation depuis les sources (.deb, compilation)

## Introduction

Jusqu'à présent, nous avons vu des méthodes "clés en main" pour installer des logiciels : le Gestionnaire de logiciels, APT, Flatpak, etc. Mais parfois, vous devrez installer un logiciel de manière plus "artisanale" :
- En téléchargeant un fichier **.deb** depuis un site web
- En **compilant** un logiciel depuis son code source

Ces méthodes sont plus techniques et comportent plus de risques, mais elles donnent accès à des logiciels qui ne sont disponibles nulle part ailleurs, ou à des versions très récentes.

**Analogie** : Si les méthodes précédentes étaient comme acheter des meubles en kit IKEA, installer depuis les sources, c'est comme construire vous-même vos meubles à partir de planches brutes. C'est plus compliqué, mais parfois nécessaire.

## Partie 1 : Installation de fichiers .deb

### Qu'est-ce qu'un fichier .deb ?

Un fichier **.deb** est un paquet d'installation pour Debian, Ubuntu et Linux Mint. C'est l'équivalent d'un fichier **.exe** ou **.msi** sous Windows.

**Extension** : `.deb`
**Exemple** : `google-chrome-stable_current_amd64.deb`

### Pourquoi télécharger un .deb manuellement ?

Vous devrez télécharger un .deb dans ces situations :

1. **Le logiciel n'est pas dans les dépôts**
   - Exemple : Google Chrome, Skype

2. **Vous voulez une version spécifique**
   - Une version plus récente ou plus ancienne

3. **Le développeur fournit uniquement un .deb**
   - Certains logiciels propriétaires

4. **Vous testez un logiciel en développement**
   - Versions beta ou nightly builds

### Où trouver des fichiers .deb ?

**Sources fiables** :
- ✅ Site officiel du logiciel
- ✅ GitHub releases des projets open source
- ✅ Sites de développeurs reconnus

**Sources à éviter** :
- ❌ Sites de téléchargement génériques (softonic, etc.)
- ❌ Forums ou sites inconnus
- ❌ Fichiers .deb sans source claire

### Télécharger un fichier .deb

**Exemple concret** : Télécharger Google Chrome

1. Allez sur le site officiel : https://www.google.com/chrome/
2. Cliquez sur **"Télécharger Chrome"**
3. Choisissez **".deb (Pour Debian/Ubuntu)"**
4. Le fichier se télécharge dans votre dossier **Téléchargements**

### Installer un fichier .deb (méthode graphique)

**Méthode la plus simple** :

1. Ouvrez votre dossier **Téléchargements**
2. **Double-cliquez** sur le fichier .deb
3. Le **Gestionnaire de logiciels** s'ouvre automatiquement
4. Cliquez sur **"Installer"**
5. Entrez votre **mot de passe**
6. Attendez la fin de l'installation

**Alternative si le double-clic ne fonctionne pas** :

1. **Clic droit** sur le fichier .deb
2. Sélectionnez **"Ouvrir avec"** → **"Installation de logiciel"**
3. Suivez les étapes ci-dessus

### Installer un fichier .deb (ligne de commande)

Si l'installation graphique échoue ou si vous préférez le terminal :

```bash
cd ~/Téléchargements
sudo dpkg -i nom-du-fichier.deb
```

**Exemple** :
```bash
cd ~/Téléchargements
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

**Explication** :
- `cd ~/Téléchargements` : Se déplacer dans le dossier Téléchargements
- `sudo` : Privilèges administrateur nécessaires
- `dpkg -i` : Installer un paquet .deb
- Nom du fichier

### Résoudre les dépendances manquantes

**Problème courant** : Après avoir installé un .deb avec dpkg, vous voyez un message d'erreur sur des dépendances manquantes.

**Message typique** :
```
dpkg: des problèmes de dépendances empêchent la configuration de nom-application :
 nom-application dépend de libxyz ; cependant :
  Le paquet libxyz n'est pas installé.
```

**Solution magique** :
```bash
sudo apt install -f
```

Cette commande :
- Détecte automatiquement les dépendances manquantes
- Les télécharge et les installe
- Termine l'installation du paquet .deb

**Séquence complète recommandée** :
```bash
sudo dpkg -i nom-du-fichier.deb
sudo apt install -f
```

### Installer plusieurs .deb en une fois

Si vous avez plusieurs fichiers .deb à installer :

```bash
sudo dpkg -i *.deb
sudo apt install -f
```

### Vérifier qu'un .deb est installé

```bash
dpkg -l | grep nom-application
```

Ou via le Gestionnaire de logiciels, dans la liste des applications installées.

### Désinstaller un paquet installé via .deb

**Méthode graphique** :
1. Gestionnaire de logiciels → Applications installées
2. Trouvez le logiciel
3. Cliquez sur "Supprimer"

**Ligne de commande** :
```bash
sudo apt remove nom-du-paquet
```

Ou pour une suppression complète avec configuration :
```bash
sudo apt purge nom-du-paquet
```

### Précautions avec les fichiers .deb

⚠️ **Avertissements importants** :

1. **Vérifiez la source** : Ne téléchargez que depuis des sites officiels
2. **Vérifiez la signature** : Si disponible, vérifiez le checksum
3. **Lisez les retours** : Cherchez des avis d'autres utilisateurs
4. **Sauvegardez** : Créez un snapshot Timeshift avant d'installer des .deb inconnus
5. **Compatibilité** : Vérifiez que le .deb est pour votre version d'Ubuntu/Mint

### Vérifier un fichier .deb avant installation

**Voir le contenu d'un .deb** :
```bash
dpkg -c nom-du-fichier.deb
```

**Voir les informations du paquet** :
```bash
dpkg -I nom-du-fichier.deb
```

**Extraire sans installer** :
```bash
dpkg-deb -x nom-du-fichier.deb dossier-extraction/
```

## Partie 2 : Compilation depuis les sources

### Qu'est-ce que la compilation ?

**Compiler** un logiciel signifie transformer son **code source** (écrit par les développeurs en langage de programmation) en un **programme exécutable** que votre ordinateur peut lancer.

**Analogie** : C'est comme avoir une recette (code source) et cuisiner le plat (compilation) pour obtenir le repas final (programme exécutable).

### Le code source

Le **code source** est l'ensemble des fichiers texte contenant le code du programme, généralement écrits en :
- C / C++
- Python
- Java
- Rust
- etc.

**Format habituel** : Archive compressée (`.tar.gz`, `.tar.bz2`, `.zip`)

### Pourquoi compiler depuis les sources ?

**Raisons valables** :

✅ **Le logiciel n'existe dans aucun autre format**
- Certains logiciels de niche ou très récents

✅ **Vous voulez la toute dernière version**
- Version de développement non packagée

✅ **Vous voulez des options de compilation spécifiques**
- Optimisations pour votre matériel
- Activation/désactivation de fonctionnalités

✅ **Vous développez ou testez**
- Modifications du code
- Contribution au projet

**Quand NE PAS compiler** :

- ❌ Si le logiciel existe en .deb, Flatpak, ou autre format plus simple
- ❌ Si vous débutez sur Linux (trop complexe)
- ❌ Si vous n'avez pas le temps (peut être long)
- ❌ Si vous ne comprenez pas ce que vous faites

### Prérequis : Les outils de compilation

Avant de compiler quoi que ce soit, vous devez installer les **outils de développement**.

#### Installer build-essential

```bash
sudo apt update
sudo apt install build-essential
```

**Contenu de build-essential** :
- `gcc` : Compilateur C
- `g++` : Compilateur C++
- `make` : Outil d'automatisation de compilation
- Bibliothèques de développement de base

#### Outils complémentaires utiles

```bash
sudo apt install git cmake autoconf automake
```

- `git` : Télécharger du code depuis GitHub
- `cmake` : Système de build moderne
- `autoconf` / `automake` : Outils de configuration automatique

### Télécharger le code source

#### Depuis un site web

1. Allez sur le site du projet
2. Cherchez "Download" ou "Source code"
3. Téléchargez l'archive (`.tar.gz` ou `.tar.bz2`)

#### Depuis GitHub (méthode moderne)

```bash
git clone https://github.com/utilisateur/projet.git
cd projet
```

**Exemple** : Cloner un projet open source
```bash
git clone https://github.com/vim/vim.git
cd vim
```

#### Décompresser une archive

Si vous avez téléchargé une archive :

**.tar.gz** :
```bash
tar -xzvf nom-fichier.tar.gz
cd nom-dossier
```

**.tar.bz2** :
```bash
tar -xjvf nom-fichier.tar.bz2
cd nom-dossier
```

**.zip** :
```bash
unzip nom-fichier.zip
cd nom-dossier
```

### Le processus de compilation standard

La plupart des projets suivent le processus classique en **3 étapes** :

```
./configure
make
sudo make install
```

Décortiquons chaque étape.

#### Étape 1 : Configuration (./configure)

```bash
./configure
```

**Ce que fait cette commande** :
- Vérifie que votre système a tout ce qui est nécessaire
- Détecte les bibliothèques disponibles
- Génère des fichiers de configuration adaptés à votre système
- Vérifie les dépendances

**Options courantes** :
```bash
./configure --prefix=/usr/local
./configure --help  # Voir toutes les options
```

**Problèmes fréquents** : Dépendances manquantes (nous verrons ça après).

#### Étape 2 : Compilation (make)

```bash
make
```

**Ce que fait cette commande** :
- Compile le code source
- Transforme les fichiers .c, .cpp en fichiers binaires
- Peut prendre de quelques secondes à plusieurs heures selon la taille du projet

**Options utiles** :
```bash
make -j4  # Utilise 4 cœurs de processeur (plus rapide)
make -j$(nproc)  # Utilise tous les cœurs disponibles
```

**Cette étape est longue** : Soyez patient. Pour de gros projets (LibreOffice, Firefox), comptez des heures.

#### Étape 3 : Installation (make install)

```bash
sudo make install
```

**Ce que fait cette commande** :
- Copie les fichiers compilés aux bons emplacements
- Installe le programme sur votre système
- Nécessite `sudo` car modifie des dossiers système

**Où sont installés les fichiers ?**
- Binaires : `/usr/local/bin/`
- Bibliothèques : `/usr/local/lib/`
- Documentation : `/usr/local/share/`

### Exemple complet : Compiler htop depuis les sources

**htop** est un moniteur système. Compilons-le en exemple didactique.

```bash
# 1. Installer les dépendances
sudo apt install build-essential libncurses5-dev autoconf automake

# 2. Télécharger le code source
git clone https://github.com/htop-dev/htop.git
cd htop

# 3. Générer le script configure
./autogen.sh

# 4. Configurer
./configure

# 5. Compiler
make -j$(nproc)

# 6. Installer
sudo make install

# 7. Tester
htop
```

### Gérer les dépendances de compilation

**Problème le plus fréquent** : Dépendances de développement manquantes.

#### Message d'erreur typique

```
configure: error: Library XYZ not found
```

Ou

```
fatal error: xyz.h: No such file or directory
```

#### Trouver la dépendance manquante

**Méthode 1** : Lire le fichier README ou INSTALL du projet
- Souvent, le projet liste ses dépendances

**Méthode 2** : Chercher le paquet de développement
```bash
apt search libxyz-dev
```

Les paquets de développement se terminent généralement par `-dev`.

**Méthode 3** : Recherche sur Internet
- "nom-du-logiciel compile dependencies ubuntu"
- Souvent, d'autres personnes ont eu le même problème

#### Installer les dépendances de développement

**Dépendances courantes** :

Pour les programmes avec interface graphique :
```bash
sudo apt install libgtk-3-dev libx11-dev
```

Pour les programmes utilisant Qt :
```bash
sudo apt install qtbase5-dev qt5-qmake
```

Pour les programmes utilisant SDL (jeux) :
```bash
sudo apt install libsdl2-dev
```

Pour les programmes réseau :
```bash
sudo apt install libcurl4-openssl-dev libssl-dev
```

### Alternatives à ./configure : CMake

Certains projets modernes utilisent **CMake** au lieu de `./configure`.

**Processus CMake** :

```bash
mkdir build
cd build
cmake ..
make -j$(nproc)
sudo make install
```

**Exemple avec un projet CMake** :
```bash
git clone https://github.com/projet/exemple.git
cd exemple
mkdir build
cd build
cmake ..
make -j$(nproc)
sudo make install
```

### Désinstaller un programme compilé

**Problème** : Il n'y a pas de gestionnaire de paquets pour les programmes compilés manuellement.

#### Méthode 1 : make uninstall (si disponible)

Depuis le dossier où vous avez compilé :
```bash
sudo make uninstall
```

⚠️ Cela ne fonctionne que si le Makefile le prévoit.

#### Méthode 2 : Suppression manuelle

Retrouvez où les fichiers ont été installés et supprimez-les :
```bash
which nom-du-programme  # Trouve le binaire
sudo rm /usr/local/bin/nom-du-programme
```

Supprimez aussi les bibliothèques et fichiers de config associés.

#### Méthode 3 : checkinstall (recommandée)

**checkinstall** crée un paquet .deb à partir de `make install`, ce qui permet une désinstallation propre.

**Installation** :
```bash
sudo apt install checkinstall
```

**Utilisation** :
```bash
./configure
make
sudo checkinstall  # Au lieu de sudo make install
```

checkinstall vous pose quelques questions puis crée un .deb que vous pourrez désinstaller proprement avec `apt remove`.

### Compiler avec des options spécifiques

Vous pouvez personnaliser la compilation avec des options.

#### Voir les options disponibles

```bash
./configure --help
```

#### Exemples d'options courantes

**Changer le préfixe d'installation** :
```bash
./configure --prefix=/opt/mon-application
```

**Désactiver une fonctionnalité** :
```bash
./configure --disable-feature-xyz
```

**Activer une fonctionnalité** :
```bash
./configure --enable-feature-xyz
```

**Optimiser pour votre processeur** :
```bash
export CFLAGS="-O3 -march=native"
./configure
```

### Compilation de programmes Python

Les programmes Python ne se compilent pas vraiment, mais s'installent depuis les sources.

#### Depuis PyPI (dépôt Python)

```bash
pip install nom-du-paquet
```

Ou pour une installation système :
```bash
sudo apt install python3-pip
sudo pip3 install nom-du-paquet
```

#### Depuis les sources (setup.py)

```bash
git clone https://github.com/projet/python-app.git
cd python-app
sudo python3 setup.py install
```

**Note** : Privilégiez les environnements virtuels Python (venv) pour éviter de polluer le système.

### Risques et précautions

#### Risques de la compilation

⚠️ **Modifier le système**
- Les fichiers installés manuellement peuvent entrer en conflit avec les paquets système

⚠️ **Pas de mises à jour automatiques**
- Vous devez manuellement recompiler pour mettre à jour

⚠️ **Difficile à désinstaller**
- Sans `make uninstall`, c'est compliqué

⚠️ **Peut casser le système**
- Si vous ne savez pas ce que vous faites

⚠️ **Chronophage**
- La compilation peut prendre très longtemps

#### Précautions à prendre

✅ **Créez une sauvegarde Timeshift** avant toute compilation importante

✅ **Lisez la documentation** : README, INSTALL, CONTRIBUTING

✅ **Utilisez checkinstall** pour créer un .deb

✅ **Installez dans un préfixe séparé** :
```bash
./configure --prefix=/opt/nom-application
```
Ainsi, tout est dans `/opt/nom-application` et facile à supprimer.

✅ **Testez d'abord** : Si possible, testez en machine virtuelle

✅ **Vérifiez la source** : Ne compilez que du code de confiance

### Outils pour simplifier la compilation

#### Git + Make

Pour les développeurs, garder le code à jour :
```bash
cd dossier-du-projet
git pull
make clean
make -j$(nproc)
sudo make install
```

#### ccache : Accélérer les recompilations

```bash
sudo apt install ccache
export PATH="/usr/lib/ccache:$PATH"
```

ccache met en cache les résultats de compilation, accélérant les recompilations.

#### distcc : Compilation distribuée

Pour les très gros projets, vous pouvez répartir la compilation sur plusieurs machines.

## Quand utiliser quelle méthode ?

Récapitulatif pour choisir la bonne approche :

| Situation | Méthode recommandée |
|-----------|---------------------|
| L'application est dans les dépôts | ✅ `apt install` |
| L'application est sur Flathub | ✅ Flatpak |
| Le site officiel fournit un .deb | ✅ Télécharger et installer le .deb |
| L'application est sur GitHub sans releases | ⚠️ AppImage si disponible, sinon compilation |
| Vous voulez LA toute dernière version | ⚠️ Compilation depuis les sources |
| Vous voulez modifier le code | ✅ Compilation depuis les sources |
| Vous débutez sur Linux | ❌ Évitez la compilation, utilisez .deb ou Flatpak |

## Exemples pratiques

### Exemple 1 : Installer un .deb de Google Chrome

```bash
# Télécharger
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb

# Installer
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt install -f

# Vérifier
google-chrome --version
```

### Exemple 2 : Compiler Neofetch depuis GitHub

```bash
# Installer dépendances
sudo apt install git

# Cloner
git clone https://github.com/dylanaraps/neofetch.git
cd neofetch

# Installer (pas de compilation nécessaire, c'est un script)
sudo make install

# Tester
neofetch
```

### Exemple 3 : Compiler avec CMake (exemple fictif)

```bash
# Cloner
git clone https://github.com/projet/exemple-cmake.git
cd exemple-cmake

# Installer dépendances de build
sudo apt install cmake build-essential

# Créer dossier de build
mkdir build && cd build

# Configurer avec CMake
cmake ..

# Compiler
make -j$(nproc)

# Installer
sudo make install
```

## Dépannage

### Erreur : "configure: command not found"

**Solution** :
```bash
./autogen.sh
```
Ou :
```bash
autoreconf -i
```

### Erreur : "make: *** No targets specified"

**Cause** : Pas de Makefile généré.

**Solution** : Lancez d'abord `./configure` ou `cmake`.

### Compilation échoue avec des erreurs

**Lecture des erreurs** :
- Lisez le dernier message d'erreur (souvent en bas)
- Cherchez "error:" dans la sortie
- Les lignes importantes mentionnent ce qui manque

**Recherche de solution** :
- Copiez le message d'erreur dans Google
- Ajoutez "ubuntu" ou "linux mint" à la recherche
- Vérifiez les issues GitHub du projet

### Le programme compilé ne se lance pas

**Vérifier les bibliothèques** :
```bash
ldd /chemin/vers/binaire
```

Affiche les bibliothèques manquantes (marquées "not found").

## Bonnes pratiques

### Pour les débutants

1. ❌ **Évitez la compilation au début**
   - Trop complexe, risqué
   - Privilégiez .deb, Flatpak, AppImage

2. ✅ **Commencez par des petits projets**
   - Scripts Python simples
   - Petits outils en C

3. ✅ **Utilisez une machine virtuelle pour apprendre**
   - Testez sans risque pour votre système principal

4. ✅ **Sauvegardez avant toute expérimentation**
   - Timeshift est votre ami

### Pour tous

1. ✅ **Lisez la documentation du projet**
2. ✅ **Vérifiez les prérequis**
3. ✅ **Utilisez checkinstall quand possible**
4. ✅ **Notez ce que vous faites** : Gardez un journal de vos compilations
5. ✅ **Préférez toujours un paquet officiel** si disponible

## Ressources supplémentaires

### Documentation

- GNU Make : https://www.gnu.org/software/make/manual/
- CMake : https://cmake.org/documentation/
- Autotools : https://www.gnu.org/software/automake/

### Apprendre

- "Linux From Scratch" : Apprendre en construisant sa propre distribution
- Documentation des projets open source sur GitHub

### Communauté

- Forums Linux Mint
- Stack Overflow
- Reddit : r/linux4noobs, r/linuxquestions

## Conclusion

L'installation depuis les sources est une compétence avancée qui donne accès à l'univers complet du logiciel libre. Bien que complexe, c'est parfois la seule option pour obtenir un logiciel spécifique ou une version particulière.

### Points clés à retenir

- ⭐ **Fichiers .deb** : Plus simple que la compilation, mais vérifiez toujours la source
- ⭐ **Compilation** : Processus en 3 étapes (configure, make, make install)
- ⭐ **Dépendances** : Le principal défi est de trouver et installer les bonnes dépendances
- ⭐ **checkinstall** : Outil précieux pour créer des .deb depuis make install
- ⭐ **Risques** : Sauvegardez toujours avant, la compilation peut casser le système
- ⭐ **Dernier recours** : N'utilisez cette méthode que si aucune alternative plus simple n'existe

### Message final

Pour les débutants : **ne compilez pas si vous pouvez l'éviter**. Il existe presque toujours une alternative plus simple et plus sûre (dépôts officiels, Flatpak, AppImage).

Pour les curieux : la compilation est une excellente façon d'apprendre comment Linux fonctionne en profondeur. Commencez doucement, dans une VM, et amusez-vous !

**Hiérarchie finale de préférence** :
1. Dépôts officiels (.deb via apt)
2. Flatpak (Flathub)
3. PPA de confiance
4. AppImage
5. .deb téléchargé depuis site officiel
6. Snap (si vraiment nécessaire)
7. **Compilation (en dernier recours)**

---


⏭️ [Gestion des dépendances cassées](/06-gestion-des-logiciels/09-gestion-des-dependances-cassees.md)
