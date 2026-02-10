🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 19.1 - Environnements de développement (VS Code, JetBrains, etc.)

## Introduction

Un **environnement de développement intégré** (IDE - Integrated Development Environment) est un logiciel qui regroupe tous les outils dont vous avez besoin pour écrire du code : un éditeur de texte avancé, des outils de débogage, un terminal intégré, et bien plus encore.

Pensez-y comme à un "atelier complet" pour développeur, plutôt que d'utiliser plusieurs outils séparés.

### Pourquoi utiliser un IDE ?

- **Coloration syntaxique** : votre code est coloré pour être plus lisible
- **Autocomplétion** : l'IDE vous suggère du code pendant que vous tapez
- **Détection d'erreurs** : les problèmes sont signalés avant même l'exécution
- **Débogage intégré** : pour trouver et corriger les bugs facilement
- **Gestion de projet** : organisation de vos fichiers et dépendances
- **Extensions** : possibilité d'ajouter des fonctionnalités

---

## Les principaux IDE sous Linux Mint

### 1. Visual Studio Code (VS Code)

**Le plus populaire et recommandé pour débuter**

![Type : Éditeur de code extensible | Licence : Gratuit et Open Source (MIT)]

#### Pourquoi choisir VS Code ?

- **Gratuit et léger** : parfait pour commencer sans investissement
- **Très populaire** : énorme communauté, beaucoup de tutoriels disponibles
- **Extensions nombreuses** : pour tous les langages et tous les besoins
- **Interface intuitive** : facile à prendre en main
- **Multi-langages** : supporte pratiquement tous les langages de programmation

#### Installation de VS Code

**Méthode 1 : Via le Gestionnaire de logiciels**

1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "**Visual Studio Code**" ou "**code**"
3. Cliquez sur **Installer**
4. Entrez votre mot de passe administrateur

**Méthode 2 : Via le terminal (Flatpak)**

```bash
flatpak install flathub com.visualstudio.code
```

**Méthode 3 : Via le dépôt officiel Microsoft**

```bash
# Télécharger et installer la clé GPG
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg  
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg  

# Ajouter le dépôt
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'

# Installer VS Code
sudo apt update  
sudo apt install code  
```

#### Extensions essentielles pour VS Code

Une fois VS Code installé, vous pouvez ajouter des extensions :

1. Cliquez sur l'icône **Extensions** (carré avec 4 carrés) dans la barre latérale
2. Recherchez et installez selon vos besoins :

**Extensions recommandées pour débuter :**

- **French Language Pack** : interface en français
- **Prettier** : formatage automatique du code
- **Error Lens** : affiche les erreurs directement dans le code
- **Material Icon Theme** : icônes plus jolies pour les fichiers
- **GitLens** : pour mieux utiliser Git

**Extensions par langage :**

- **Python** : extension officielle Python
- **JavaScript/TypeScript** : inclus par défaut
- **C/C++** : extension officielle C/C++
- **Java Extension Pack** : pack complet pour Java
- **PHP Intelephense** : pour PHP
- **Go** : extension officielle Go

#### Premier lancement de VS Code

1. Lancez VS Code depuis le menu Applications
2. Choisissez votre thème (clair ou sombre)
3. Installez le pack de langue française si vous le souhaitez
4. Ouvrez un dossier : **Fichier > Ouvrir le dossier**
5. Créez votre premier fichier : **Fichier > Nouveau fichier**

---

### 2. VSCodium

**Alternative 100% Open Source de VS Code**

![Type : Éditeur de code | Licence : Gratuit et Open Source (MIT)]

#### Qu'est-ce que VSCodium ?

VSCodium est une version de VS Code sans les composants propriétaires de Microsoft (télémétrie, tracking). C'est exactement la même interface et les mêmes fonctionnalités.

#### Quand choisir VSCodium ?

- Vous voulez une version totalement Open Source
- Vous souhaitez éviter la télémétrie Microsoft
- Vous préférez les logiciels libres

**⚠️ Note** : Certaines extensions du marketplace Microsoft peuvent ne pas fonctionner.

#### Installation de VSCodium

```bash
# Via Flatpak
flatpak install flathub com.vscodium.codium

# Ou via le dépôt officiel
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | gpg --dearmor | sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg  
echo 'deb [signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg] https://download.vscodium.com/debs vscodium main' | sudo tee /etc/apt/sources.list.d/vscodium.list  
sudo apt update  
sudo apt install codium  
```

---

### 3. Suite JetBrains (PyCharm, IntelliJ IDEA, WebStorm, etc.)

**Les IDE professionnels par excellence**

![Type : IDE complets | Licence : Versions gratuites et payantes]

#### Qu'est-ce que JetBrains ?

JetBrains est une entreprise qui développe des IDE spécialisés par langage de programmation. Chaque IDE est optimisé pour un langage spécifique.

#### Les principaux IDE JetBrains

| IDE | Langage | Version gratuite |
|-----|---------|------------------|
| **PyCharm** | Python | ✅ Community |
| **IntelliJ IDEA** | Java, Kotlin | ✅ Community |
| **WebStorm** | JavaScript, TypeScript | ❌ Payant |
| **PhpStorm** | PHP | ❌ Payant |
| **CLion** | C, C++ | ❌ Payant |
| **GoLand** | Go | ❌ Payant |
| **Rider** | C# (.NET) | ❌ Payant |
| **RustRover** | Rust | ✅ Gratuit |

#### Pourquoi choisir un IDE JetBrains ?

**Avantages :**
- Très puissants et complets
- Excellente autocomplétion intelligente
- Refactoring automatique avancé
- Débogueur très performant
- Analyses de code poussées
- Intégration parfaite avec les outils du langage

**Inconvénients :**
- Plus lourds que VS Code (consomment plus de RAM)
- Versions professionnelles payantes (sauf pour étudiants)
- Peuvent être intimidants pour les débutants

#### Installation de PyCharm (exemple)

**Via Jetbrains Toolbox (recommandé) :**

1. Téléchargez JetBrains Toolbox : https://www.jetbrains.com/toolbox-app/
2. Extrayez l'archive et lancez l'exécutable
3. Depuis Toolbox, installez PyCharm Community (gratuit)

**Via Flatpak :**

```bash
# PyCharm Community (gratuit)
flatpak install flathub com.jetbrains.PyCharm-Community

# IntelliJ IDEA Community (gratuit)
flatpak install flathub com.jetbrains.IntelliJ-IDEA-Community
```

**Via le Gestionnaire de logiciels :**

1. Ouvrez le Gestionnaire de logiciels
2. Recherchez "PyCharm" ou "IntelliJ"
3. Installez la version Community (gratuite)

#### Versions gratuites pour étudiants

Si vous êtes étudiant ou enseignant, JetBrains offre **gratuitement** toutes ses versions professionnelles !

Rendez-vous sur : https://www.jetbrains.com/community/education/

---

### 4. Geany

**L'éditeur léger et rapide**

![Type : Éditeur de code léger | Licence : Gratuit et Open Source (GPL)]

#### Pourquoi choisir Geany ?

- **Très léger** : parfait pour les anciens ordinateurs
- **Rapide** : s'ouvre instantanément
- **Simple** : interface épurée, facile à comprendre
- **Multi-langages** : supporte de nombreux langages
- **Peu de configuration** : fonctionne bien dès l'installation

#### Pour qui ?

- Débutants qui veulent quelque chose de simple
- Utilisateurs avec un PC peu puissant
- Ceux qui n'ont pas besoin d'un IDE complet

#### Installation de Geany

```bash
sudo apt install geany geany-plugins
```

Ou via le **Gestionnaire de logiciels**, recherchez "**Geany**".

---

### 5. Sublime Text

**L'éditeur élégant et performant**

![Type : Éditeur de code | Licence : Gratuit avec licence payante optionnelle]

#### Caractéristiques

- Interface très élégante
- Extrêmement rapide
- Multi-curseurs puissants
- Raccourcis clavier efficaces
- Version gratuite utilisable indéfiniment (avec rappels occasionnels)

#### Installation

Téléchargez depuis : https://www.sublimetext.com/

Ou via terminal :

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg  
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list  
sudo apt update  
sudo apt install sublime-text  
```

---

### 6. Atom

**⚠️ Note importante : Atom a été arrêté en décembre 2022**

Atom était un éditeur populaire développé par GitHub, mais le projet est maintenant archivé. Il est recommandé d'utiliser VS Code ou VSCodium à la place, qui sont ses successeurs spirituels.

---

### 7. Kate / KWrite

**Les éditeurs de KDE**

![Type : Éditeur de texte avancé | Licence : Gratuit et Open Source]

Si vous utilisez l'environnement KDE (ou même Cinnamon), Kate est un excellent éditeur :

- Interface propre et moderne
- Gestion de sessions
- Terminal intégré
- Plugin pour Git

#### Installation

```bash
sudo apt install kate
```

---

### 8. GNU Emacs et Vim

**Les éditeurs pour utilisateurs avancés**

#### Vim

- Éditeur modal très puissant
- Courbe d'apprentissage **très raide**
- Une fois maîtrisé, extrêmement efficace
- Utilisable uniquement au clavier

```bash
sudo apt install vim
```

#### Emacs

- Extensible à l'infini
- Peut tout faire (éditeur, email, navigateur web...)
- Courbe d'apprentissage importante
- Communauté passionnée

```bash
sudo apt install emacs
```

**Pour les débutants** : commencez par VS Code, vous pourrez explorer Vim/Emacs plus tard si vous le souhaitez.

---

## Comparatif rapide

| IDE/Éditeur | Difficulté | Poids | Multi-langages | Idéal pour |
|-------------|------------|-------|----------------|------------|
| **VS Code** | ⭐ Facile | Moyen | ✅ Oui | Débutants et confirmés |
| **VSCodium** | ⭐ Facile | Moyen | ✅ Oui | Amateurs d'Open Source |
| **PyCharm** | ⭐⭐ Moyen | Lourd | Python surtout | Développeurs Python |
| **IntelliJ** | ⭐⭐ Moyen | Lourd | Java surtout | Développeurs Java |
| **Geany** | ⭐ Facile | Léger | ✅ Oui | Anciens PC, simplicité |
| **Sublime** | ⭐ Facile | Léger | ✅ Oui | Rapidité, élégance |
| **Kate** | ⭐ Facile | Léger | ✅ Oui | Utilisateurs KDE |
| **Vim** | ⭐⭐⭐ Difficile | Très léger | ✅ Oui | Experts clavier |
| **Emacs** | ⭐⭐⭐ Difficile | Moyen | ✅ Oui | Power users |

---

## Quel IDE choisir pour débuter ?

### Vous débutez en programmation ?

➡️ **Visual Studio Code** (ou VSCodium)

**Pourquoi ?**
- Facile à prendre en main
- Énormément de tutoriels disponibles
- Fonctionne pour tous les langages
- Gratuit et bien supporté

### Vous avez un vieil ordinateur ?

➡️ **Geany**

**Pourquoi ?**
- Très léger et rapide
- Simple et efficace
- Peu gourmand en ressources

### Vous apprenez Python spécifiquement ?

➡️ **PyCharm Community Edition**

**Pourquoi ?**
- Optimisé pour Python
- Débogueur excellent
- Détection intelligente des erreurs Python
- Gratuit (version Community)

### Vous apprenez Java ?

➡️ **IntelliJ IDEA Community Edition**

**Pourquoi ?**
- Le meilleur pour Java
- Autocomplétion exceptionnelle
- Gratuit (version Community)

### Vous voulez du 100% Open Source ?

➡️ **VSCodium** ou **Geany**

---

## Conseils pour bien démarrer

### 1. Commencez simple

N'installez pas 10 IDE différents. Choisissez-en un et apprenez à bien l'utiliser.

### 2. Explorez les raccourcis clavier

Les IDE sont beaucoup plus efficaces quand on utilise le clavier. Apprenez progressivement :

**Raccourcis essentiels dans VS Code :**
- `Ctrl + P` : Recherche rapide de fichier
- `Ctrl + Shift + P` : Palette de commandes
- `Ctrl + /` : Commenter/décommenter
- `Ctrl + D` : Sélectionner l'occurrence suivante
- `Alt + ↑/↓` : Déplacer la ligne
- `Ctrl + Space` : Autocomplétion

### 3. Installez les extensions au fur et à mesure

Ne surchargez pas votre IDE d'extensions dès le début. Ajoutez-les quand vous en avez vraiment besoin.

### 4. Personnalisez votre environnement

Choisissez un thème qui vous plaît, ajustez la taille de la police, configurez selon vos préférences. Vous allez passer beaucoup de temps dans votre IDE, autant qu'il soit agréable !

### 5. Utilisez le contrôle de version (Git)

Tous les IDE modernes intègrent Git. Apprenez à l'utiliser dès le début, vous vous remercierez plus tard.

---

## Installation de plusieurs IDE

Vous pouvez installer plusieurs IDE sur votre système sans problème. Par exemple :

- **VS Code** pour les projets web et Python
- **PyCharm** pour les gros projets Python
- **Geany** pour éditer rapidement un fichier de configuration

Ils cohabiteront sans souci.

---

## Ressources supplémentaires

### Tutoriels VS Code
- Documentation officielle : https://code.visualstudio.com/docs
- Raccourcis clavier : https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf

### Tutoriels JetBrains
- PyCharm pour débutants : https://www.jetbrains.com/pycharm/learning-center/
- IntelliJ IDEA : https://www.jetbrains.com/idea/learning-center/

### Communauté
- Forum VS Code : https://github.com/microsoft/vscode/discussions
- Subreddit /r/vscode : https://reddit.com/r/vscode

---

## Conclusion

Le choix de votre environnement de développement est important mais pas définitif. **Visual Studio Code** est un excellent point de départ pour la plupart des débutants grâce à sa facilité d'utilisation et sa polyvalence.

N'hésitez pas à en essayer plusieurs avant de vous décider. L'essentiel est de trouver l'outil qui vous convient et qui vous permet de vous concentrer sur l'apprentissage de la programmation plutôt que sur la configuration de l'outil.

**Bon développement ! 🚀**

⏭️ [Installation de langages (Python, Java, Node.js, PHP, etc.)](/19-developpement-et-programmation/02-installation-de-langages.md)
