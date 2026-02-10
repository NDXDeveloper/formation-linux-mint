🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 19.2 - Installation de langages de programmation

## Introduction

Un **langage de programmation** est un ensemble de règles et de syntaxes qui permet de donner des instructions à un ordinateur. Pour utiliser un langage, vous devez installer son **interpréteur** ou son **compilateur** sur votre système.

### Quelle est la différence ?

- **Interpréteur** : exécute le code ligne par ligne (Python, JavaScript, PHP)
- **Compilateur** : transforme tout le code en programme exécutable avant de le lancer (C, C++, Go, Rust)
- **Machine virtuelle** : exécute du code compilé dans un environnement spécial (Java, C#)

**Bonne nouvelle** : Linux Mint facilite grandement l'installation de tous ces langages !

---

## Python

![Le langage le plus populaire pour débuter]

### Pourquoi Python ?

- **Facile à apprendre** : syntaxe claire et lisible
- **Très populaire** : utilisé partout (web, data science, IA, automatisation)
- **Déjà installé** : Python est préinstallé sur Linux Mint !

### Vérifier l'installation

Ouvrez un terminal et tapez :

```bash
python3 --version
```

Vous devriez voir quelque chose comme :
```
Python 3.11.x
```

**✅ Python est déjà installé !**

### Installer pip (gestionnaire de paquets Python)

`pip` permet d'installer des bibliothèques Python facilement.

```bash
sudo apt update  
sudo apt install python3-pip  
```

Vérification :

```bash
pip3 --version
```

### Installer des bibliothèques Python

Exemple : installer la bibliothèque `requests` pour faire des requêtes web :

```bash
pip3 install requests
```

### Python 2 vs Python 3

**Important** : Python 2 n'est plus supporté depuis 2020. Utilisez toujours **Python 3**.

- Commande moderne : `python3`
- Ancienne commande (éviter) : `python`

### Créer un environnement virtuel (recommandé)

Les environnements virtuels isolent vos projets Python. C'est une bonne pratique.

```bash
# Installer le module venv
sudo apt install python3-venv

# Créer un environnement virtuel
python3 -m venv mon_projet

# Activer l'environnement
source mon_projet/bin/activate

# Vous verrez (mon_projet) devant votre terminal
# Installer des paquets dans cet environnement
pip install requests

# Désactiver l'environnement
deactivate
```

### Versions alternatives de Python

Si vous avez besoin d'une version spécifique :

```bash
# Python 3.12 (exemple)
sudo add-apt-repository ppa:deadsnakes/ppa  
sudo apt update  
sudo apt install python3.12  
```

---

## Java

![Le langage des applications d'entreprise]

### Pourquoi Java ?

- **Multi-plateforme** : "Write once, run anywhere"
- **Utilisé en entreprise** : banques, grands systèmes
- **Android** : développement d'applications mobiles

### Deux options : JRE vs JDK

- **JRE** (Java Runtime Environment) : pour **exécuter** des programmes Java
- **JDK** (Java Development Kit) : pour **développer** en Java (inclut JRE)

**Pour programmer, installez le JDK.**

### Installation du JDK

**Option 1 : OpenJDK (recommandé, gratuit et Open Source)**

```bash
# Voir les versions disponibles
apt search openjdk-.*-jdk

# Installer la dernière version LTS (Long Term Support)
sudo apt install openjdk-17-jdk

# Ou la version 21 (la plus récente LTS)
sudo apt install openjdk-21-jdk
```

**Option 2 : Oracle JDK (officiel mais avec licence)**

Téléchargez depuis : https://www.oracle.com/java/technologies/downloads/

Puis installez le fichier .deb téléchargé :

```bash
sudo dpkg -i jdk-21_linux-x64_bin.deb
```

### Vérification

```bash
java --version  
javac --version  
```

Vous devriez voir la version installée.

### Gérer plusieurs versions de Java

Si vous avez plusieurs versions installées :

```bash
# Voir les versions disponibles
sudo update-alternatives --config java

# Choisir la version par défaut
sudo update-alternatives --config javac
```

### Variables d'environnement (si nécessaire)

Ajoutez à votre `~/.bashrc` :

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64  
export PATH=$PATH:$JAVA_HOME/bin  
```

Puis rechargez :

```bash
source ~/.bashrc
```

---

## Node.js et npm

![JavaScript côté serveur]

### Pourquoi Node.js ?

- **JavaScript partout** : même langage côté client et serveur
- **npm** : énorme bibliothèque de paquets
- **Développement web moderne** : React, Vue, Angular, etc.

### Installation via le gestionnaire de paquets

**⚠️ Attention** : la version dans les dépôts Ubuntu peut être ancienne.

```bash
sudo apt install nodejs npm
```

Vérification :

```bash
node --version  
npm --version  
```

### Installation via NodeSource (version récente recommandée)

Pour avoir la dernière version LTS :

```bash
# Installer Node.js 20.x (LTS)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -  
sudo apt install nodejs  

# Vérification
node --version  
npm --version  
```

**Versions disponibles** :
- **18.x** : LTS (Long Term Support)
- **20.x** : LTS (recommandé)
- **21.x** : Version actuelle (latest)

### Installation via NVM (Node Version Manager)

**Recommandé pour les développeurs** : permet de gérer plusieurs versions de Node.js.

```bash
# Installer NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Recharger le terminal
source ~/.bashrc

# Installer la dernière version LTS
nvm install --lts

# Utiliser cette version
nvm use --lts

# Lister les versions installées
nvm ls

# Installer une version spécifique
nvm install 18.19.0  
nvm use 18.19.0  
```

### npm : gestionnaire de paquets

Installer un paquet globalement :

```bash
npm install -g nom-du-paquet
```

Installer un paquet dans un projet :

```bash
cd mon-projet  
npm install nom-du-paquet  
```

### Yarn (alternative à npm)

```bash
npm install -g yarn

# Utilisation
yarn add nom-du-paquet
```

---

## PHP

![Le langage du web dynamique]

### Pourquoi PHP ?

- **WordPress, Drupal** : CMS les plus populaires
- **Laravel, Symfony** : frameworks modernes
- **Développement web** : côté serveur

### Installation de PHP

```bash
# Installer PHP et les modules courants
sudo apt install php php-cli php-common php-mysql php-xml php-curl php-mbstring php-zip
```

Vérification :

```bash
php --version
```

### Versions de PHP

Voir la version installée :

```bash
php -v
```

Installer une version spécifique (via PPA Ondřej Surý) :

```bash
# Ajouter le dépôt
sudo add-apt-repository ppa:ondrej/php  
sudo apt update  

# Installer PHP 8.3
sudo apt install php8.3 php8.3-cli php8.3-common php8.3-mysql

# Basculer entre versions
sudo update-alternatives --config php
```

### Composer (gestionnaire de dépendances PHP)

Composer est l'équivalent de npm pour PHP.

```bash
# Télécharger l'installateur
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

# Installer globalement
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

# Nettoyer
php -r "unlink('composer-setup.php');"

# Vérification
composer --version
```

### Serveur web pour PHP

Pour tester PHP rapidement :

```bash
# Serveur de développement intégré
php -S localhost:8000
```

Puis ouvrez http://localhost:8000 dans votre navigateur.

Pour un vrai serveur, voir Apache ou Nginx (section 21.2).

---

## C et C++

![Les langages de la performance]

### Pourquoi C/C++ ?

- **Performance maximale** : jeux vidéo, systèmes embarqués
- **Système** : drivers, noyau Linux
- **Bases solides** : comprendre comment fonctionne l'ordinateur

### Installation

```bash
# Installer le compilateur GCC et les outils de build
sudo apt install build-essential

# GCC inclut :
# - gcc (compilateur C)
# - g++ (compilateur C++)
# - make (outil de construction)
```

Vérification :

```bash
gcc --version  
g++ --version  
make --version  
```

### Compiler un programme C

Créez un fichier `hello.c` :

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

Compilation :

```bash
gcc hello.c -o hello
./hello
```

### Compiler un programme C++

Créez un fichier `hello.cpp` :

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

Compilation :

```bash
g++ hello.cpp -o hello
./hello
```

### Clang (alternative à GCC)

```bash
sudo apt install clang

# Utilisation
clang hello.c -o hello  
clang++ hello.cpp -o hello  
```

---

## Go (Golang)

![Le langage de Google pour le cloud]

### Pourquoi Go ?

- **Simple et rapide** : syntaxe claire, compilation ultra-rapide
- **Concurrence facile** : goroutines
- **Cloud et DevOps** : Docker, Kubernetes sont écrits en Go

### Installation

**Méthode 1 : Via les dépôts (version peut être ancienne)**

```bash
sudo apt install golang-go
```

**Méthode 2 : Installation manuelle (version récente recommandée)**

```bash
# Télécharger la dernière version depuis https://go.dev/dl/
wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz

# Supprimer l'ancienne installation
sudo rm -rf /usr/local/go

# Extraire la nouvelle version
sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz

# Ajouter à votre PATH dans ~/.bashrc
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc  
echo 'export GOPATH=$HOME/go' >> ~/.bashrc  
source ~/.bashrc  
```

Vérification :

```bash
go version
```

### Premier programme Go

Créez `hello.go` :

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

Exécution :

```bash
go run hello.go
```

Compilation :

```bash
go build hello.go
./hello
```

---

## Rust

![Le langage de la sécurité mémoire]

### Pourquoi Rust ?

- **Sécurité** : évite les bugs mémoire
- **Performance** : aussi rapide que C/C++
- **Moderne** : langage apprécié des développeurs

### Installation avec rustup

```bash
# Installer rustup (installateur officiel)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Suivez les instructions à l'écran (généralement appuyez sur 1)

# Recharger le terminal
source ~/.bashrc
```

Vérification :

```bash
rustc --version  
cargo --version  
```

### Cargo : gestionnaire de projets Rust

Créer un nouveau projet :

```bash
cargo new mon_projet  
cd mon_projet  
```

Compiler et exécuter :

```bash
cargo run
```

Compiler pour la production :

```bash
cargo build --release
```

### Mise à jour de Rust

```bash
rustup update
```

---

## Ruby

![Le langage élégant pour le web]

### Pourquoi Ruby ?

- **Ruby on Rails** : framework web populaire
- **Syntaxe élégante** : code lisible et expressif
- **DevOps** : outils comme Chef, Vagrant

### Installation

```bash
sudo apt install ruby-full
```

Vérification :

```bash
ruby --version
```

### RubyGems (gestionnaire de paquets)

Déjà inclus avec Ruby.

```bash
gem --version
```

Installer une gem :

```bash
gem install nom-de-la-gem
```

### RVM (Ruby Version Manager)

Pour gérer plusieurs versions de Ruby :

```bash
# Installer RVM
curl -sSL https://get.rvm.io | bash -s stable

# Recharger
source ~/.rvm/scripts/rvm

# Installer Ruby 3.2
rvm install 3.2

# Utiliser cette version
rvm use 3.2
```

---

## Perl

![Le couteau suisse du texte]

### Installation

Perl est généralement préinstallé sur Linux Mint.

Vérification :

```bash
perl --version
```

Si absent :

```bash
sudo apt install perl
```

### CPAN (gestionnaire de modules)

```bash
# Configurer CPAN
cpan

# Installer un module
cpan install Module::Name
```

---

## Kotlin

![Le langage moderne pour Android et JVM]

### Installation

Kotlin nécessite Java (JDK).

```bash
# Installer SDKMAN (gestionnaire de kits de développement)
curl -s "https://get.sdkman.io" | bash  
source ~/.sdkman/bin/sdkman-init.sh  

# Installer Kotlin
sdk install kotlin
```

Vérification :

```bash
kotlin -version
```

---

## Swift

![Le langage d'Apple, maintenant open source]

### Installation

```bash
# Télécharger depuis https://swift.org/download/
wget https://download.swift.org/swift-5.9.2-release/ubuntu2204/swift-5.9.2-RELEASE/swift-5.9.2-RELEASE-ubuntu22.04.tar.gz

# Extraire
tar xzf swift-5.9.2-RELEASE-ubuntu22.04.tar.gz

# Déplacer
sudo mv swift-5.9.2-RELEASE-ubuntu22.04 /usr/share/swift

# Ajouter au PATH
echo 'export PATH=/usr/share/swift/usr/bin:$PATH' >> ~/.bashrc  
source ~/.bashrc  
```

Vérification :

```bash
swift --version
```

---

## R (pour statistiques et data science)

![Le langage de l'analyse de données]

### Installation

```bash
# Installer R
sudo apt install r-base r-base-dev
```

Vérification :

```bash
R --version
```

Lancer R :

```bash
R
```

### RStudio (IDE pour R)

Téléchargez depuis : https://posit.co/download/rstudio-desktop/

```bash
# Installer le .deb téléchargé
sudo dpkg -i rstudio-*.deb  
sudo apt install -f  # Résoudre les dépendances  
```

---

## Lua

![Le langage léger pour l'embarqué et les jeux]

### Installation

```bash
sudo apt install lua5.4
```

Vérification :

```bash
lua -v
```

---

## TypeScript

![JavaScript avec des types]

### Installation

TypeScript nécessite Node.js.

```bash
# Installer TypeScript globalement
npm install -g typescript

# Vérification
tsc --version
```

Compiler un fichier TypeScript :

```bash
tsc fichier.ts
# Génère fichier.js
```

---

## Tableau récapitulatif

| Langage | Difficulté | Usage principal | Installation |
|---------|------------|-----------------|--------------|
| **Python** | ⭐ Facile | Tout (web, data, IA) | Préinstallé |
| **JavaScript** | ⭐ Facile | Web frontend | Node.js |
| **Java** | ⭐⭐ Moyen | Entreprise, Android | OpenJDK |
| **PHP** | ⭐ Facile | Web backend | APT |
| **C** | ⭐⭐⭐ Difficile | Système, performance | GCC |
| **C++** | ⭐⭐⭐ Difficile | Jeux, performance | G++ |
| **Go** | ⭐⭐ Moyen | Cloud, DevOps | Site officiel |
| **Rust** | ⭐⭐⭐ Difficile | Système, sécurité | Rustup |
| **Ruby** | ⭐⭐ Moyen | Web (Rails) | APT |
| **Kotlin** | ⭐⭐ Moyen | Android, JVM | SDKMAN |
| **TypeScript** | ⭐⭐ Moyen | Web avec types | npm |
| **R** | ⭐⭐ Moyen | Statistiques, data | APT |

---

## Quel langage choisir pour débuter ?

### Vous voulez apprendre la programmation ?
➡️ **Python** - Simple, polyvalent, très demandé

### Vous voulez faire du développement web ?
➡️ **JavaScript** (Node.js) - Incontournable pour le web

### Vous voulez développer des applications Android ?
➡️ **Kotlin** ou **Java**

### Vous aimez les maths et les statistiques ?
➡️ **R** ou **Python**

### Vous voulez de la performance pure ?
➡️ **C**, **C++** ou **Rust**

### Vous visez l'entreprise et le backend ?
➡️ **Java** ou **Go**

---

## Conseils importants

### 1. Commencez par un seul langage

Ne vous éparpillez pas. Maîtrisez un langage avant d'en apprendre un autre.

### 2. Utilisez des gestionnaires de versions

- Python : `venv` ou `pyenv`
- Node.js : `nvm`
- Ruby : `rvm`
- Java : `update-alternatives`

Cela évite les conflits entre projets.

### 3. Consultez la documentation officielle

Chaque langage a sa documentation officielle :
- Python : https://docs.python.org/
- Node.js : https://nodejs.org/docs/
- Java : https://docs.oracle.com/javase/
- PHP : https://www.php.net/docs.php
- Etc.

### 4. Vérifiez les versions

Les langages évoluent. Certains projets nécessitent des versions spécifiques.

```bash
python3 --version  
node --version  
java --version  
php --version  
```

### 5. Sauvegardez vos projets avec Git

Installez Git dès le début :

```bash
sudo apt install git
```

### 6. Utilisez un environnement virtuel

Pour Python et Node.js, utilisez toujours des environnements virtuels pour isoler vos projets.

---

## Dépannage courant

### "Command not found" après installation

Rechargez votre terminal :

```bash
source ~/.bashrc
```

Ou fermez et rouvrez le terminal.

### Problème de permissions avec pip/npm

N'utilisez jamais `sudo` avec pip ou npm pour installer des paquets utilisateur.

**Bon** :
```bash
pip3 install --user nom-paquet  
npm install nom-paquet  
```

**Mauvais** :
```bash
sudo pip3 install nom-paquet  # ❌ Ne faites pas ça  
sudo npm install nom-paquet   # ❌ Ne faites pas ça  
```

### Plusieurs versions installées

Utilisez les gestionnaires de versions :
- `nvm` pour Node.js
- `pyenv` pour Python
- `rvm` pour Ruby
- `update-alternatives` pour Java

### Manque de bibliothèques de développement

Si vous avez des erreurs lors de la compilation, installez :

```bash
sudo apt install build-essential
```

---

## Ressources pour apprendre

### Sites web gratuits
- **Python** : https://python.org, Codecademy, Real Python
- **JavaScript** : MDN Web Docs, JavaScript.info
- **Java** : Oracle Java Tutorials, Codecademy
- **PHP** : PHP.net, W3Schools

### Livres recommandés
- Python : "Automate the Boring Stuff with Python"
- JavaScript : "Eloquent JavaScript"
- Java : "Head First Java"
- C : "The C Programming Language" (K&R)

### Plateformes d'apprentissage
- FreeCodeCamp (gratuit)
- Codecademy (freemium)
- The Odin Project (gratuit)
- edX / Coursera (certains cours gratuits)

---

## Conclusion

Linux Mint facilite l'installation et l'utilisation de pratiquement tous les langages de programmation. La plupart sont à une commande `apt install` de distance !

**Recommandation pour débuter** : commencez par **Python** (déjà installé) ou **JavaScript** (via Node.js). Ces deux langages sont parfaits pour apprendre et très demandés sur le marché du travail.

N'oubliez pas : **le plus important n'est pas quel langage vous choisissez, mais que vous pratiquiez régulièrement** ! 🚀

**Bon code !**

⏭️ [Git et gestion de versions](/19-developpement-et-programmation/03-git-et-gestion-de-versions.md)
