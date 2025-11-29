🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 19.3 - Git et gestion de versions

## Introduction

### Qu'est-ce que la gestion de versions ?

Imaginez que vous écrivez un roman. Vous créez plusieurs brouillons, vous modifiez des chapitres, parfois vous voulez revenir à une version précédente... La **gestion de versions** fait exactement cela pour votre code.

C'est un système qui :
- 📝 **Enregistre l'historique** de vos modifications
- ⏮️ **Permet de revenir en arrière** si quelque chose ne fonctionne plus
- 👥 **Facilite le travail en équipe** sans écraser le travail des autres
- 🌿 **Gère plusieurs versions parallèles** (branches) de votre projet

### Qu'est-ce que Git ?

**Git** est le système de gestion de versions le plus utilisé au monde. Il a été créé par Linus Torvalds (le créateur de Linux) en 2005.

**Pourquoi Git est partout ?**
- Utilisé par 95% des développeurs professionnels
- Gratuit et Open Source
- Très puissant et rapide
- Fonctionne en local (pas besoin d'Internet)
- Compatible avec GitHub, GitLab, Bitbucket

**Analogie simple** : Git est comme un appareil photo qui photographie l'état de votre projet à chaque moment important. Vous pouvez ensuite voyager dans le temps pour voir ou restaurer n'importe quelle "photo" (version).

---

## Installation de Git

### Vérifier si Git est installé

Ouvrez un terminal et tapez :

```bash
git --version
```

Si vous voyez quelque chose comme `git version 2.40.1`, Git est déjà installé ! ✅

Sinon, installez-le :

### Installation

```bash
sudo apt update
sudo apt install git
```

Vérification après installation :

```bash
git --version
```

---

## Configuration initiale (IMPORTANTE !)

Avant d'utiliser Git, vous **devez** configurer votre identité. Ces informations apparaîtront dans l'historique de vos commits.

### Configurer votre nom et email

```bash
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
```

**Exemple** :
```bash
git config --global user.name "Marie Dupont"
git config --global user.email "marie.dupont@gmail.com"
```

### Configurer l'éditeur par défaut

```bash
# Utiliser nano (facile pour débuter)
git config --global core.editor nano

# Ou vim si vous préférez
git config --global core.editor vim

# Ou VS Code
git config --global core.editor "code --wait"
```

### Vérifier votre configuration

```bash
git config --list
```

Ou voir une configuration spécifique :

```bash
git config user.name
git config user.email
```

---

## Concepts fondamentaux

Avant de commencer à utiliser Git, comprenons quelques concepts essentiels.

### Le dépôt (repository)

Un **dépôt** (ou "repo") est un dossier contenant votre projet et tout son historique Git.

Il y a deux types :
- **Dépôt local** : sur votre ordinateur
- **Dépôt distant** : sur un serveur (GitHub, GitLab, etc.)

### Les trois zones de Git

```
Zone de travail  →  Zone d'index  →  Dépôt local
(Working dir)      (Staging area)    (Repository)
```

1. **Zone de travail** : vos fichiers actuels
2. **Zone d'index** : fichiers prêts à être enregistrés
3. **Dépôt local** : historique permanent

### Le commit

Un **commit** est une "photo instantanée" de votre projet à un moment donné.

Chaque commit contient :
- Les modifications apportées
- Un message descriptif
- L'auteur et la date
- Un identifiant unique (hash)

**Analogie** : comme une sauvegarde de jeu vidéo, mais pour le code.

### Les branches

Une **branche** est une ligne de développement parallèle.

```
main    : ──●──●──●──●──●──●──
                 ╲
feature :         ●──●──●
```

- **main** (ou master) : branche principale
- **feature** : branche pour développer une nouvelle fonctionnalité

---

## Premiers pas avec Git

### Créer un nouveau dépôt

**Option 1 : Créer un nouveau projet**

```bash
# Créer un dossier
mkdir mon-projet
cd mon-projet

# Initialiser Git
git init
```

Vous verrez : `Initialized empty Git repository in...`

**Option 2 : Transformer un projet existant**

```bash
# Aller dans votre projet
cd /chemin/vers/mon-projet

# Initialiser Git
git init
```

### Vérifier l'état de votre dépôt

La commande la plus importante :

```bash
git status
```

Cette commande vous dit :
- Quels fichiers ont été modifiés
- Quels fichiers sont prêts à être commités
- Sur quelle branche vous êtes

**Utilisez-la souvent !** Elle vous guide dans votre workflow Git.

---

## Le workflow Git de base

Voici le cycle typique de travail avec Git :

### 1. Modifier des fichiers

Créez ou modifiez des fichiers normalement dans votre éditeur.

### 2. Voir ce qui a changé

```bash
git status
```

Ou pour voir les modifications détaillées :

```bash
git diff
```

### 3. Ajouter à l'index (staging)

```bash
# Ajouter un fichier spécifique
git add fichier.txt

# Ajouter plusieurs fichiers
git add fichier1.txt fichier2.txt

# Ajouter tous les fichiers modifiés
git add .

# Ajouter tous les fichiers d'un type
git add *.py
```

**Astuce** : `git add .` ajoute tout, mais faites attention à ne pas ajouter des fichiers inutiles !

### 4. Vérifier ce qui est prêt

```bash
git status
```

Les fichiers en vert sont prêts à être commités.

### 5. Créer un commit

```bash
git commit -m "Description de vos modifications"
```

**Exemple** :
```bash
git commit -m "Ajout de la page d'accueil"
git commit -m "Correction du bug d'affichage"
git commit -m "Amélioration des performances"
```

### Messages de commit : bonnes pratiques

✅ **Bon** :
```bash
git commit -m "Correction du bug de connexion"
git commit -m "Ajout de la validation email"
git commit -m "Mise à jour de la documentation"
```

❌ **Mauvais** :
```bash
git commit -m "test"
git commit -m "modif"
git commit -m "ça marche"
git commit -m "final final v2"
```

**Règles d'or** :
- Utilisez l'impératif : "Ajoute" plutôt que "Ajouté"
- Soyez descriptif mais concis (50 caractères max)
- Expliquez "quoi" et "pourquoi", pas "comment"

---

## Raccourci utile

Au lieu de faire `git add` puis `git commit`, vous pouvez combiner :

```bash
# Ajoute ET commite les fichiers déjà suivis
git commit -am "Mon message"
```

**⚠️ Attention** : ceci n'ajoute PAS les nouveaux fichiers, seulement ceux déjà trackés par Git.

---

## Voir l'historique

### Voir tous les commits

```bash
git log
```

Affichage détaillé avec :
- Hash du commit
- Auteur
- Date
- Message

### Versions simplifiées

```bash
# Une ligne par commit (plus lisible)
git log --oneline

# Avec un graphe des branches
git log --oneline --graph --all

# Les 5 derniers commits
git log -5

# Commits d'un auteur spécifique
git log --author="Marie"
```

### Voir les détails d'un commit

```bash
git show <hash-du-commit>

# Exemple
git show a1b2c3d
```

---

## Annuler des modifications

### Cas 1 : Annuler des modifications non commitées

**Fichier modifié, pas encore ajouté :**

```bash
# Restaurer un fichier
git restore fichier.txt

# Restaurer tous les fichiers
git restore .
```

**Fichier déjà ajouté (git add) mais pas commité :**

```bash
# Retirer de l'index
git restore --staged fichier.txt

# Puis restaurer le fichier si besoin
git restore fichier.txt
```

### Cas 2 : Modifier le dernier commit

Vous avez oublié un fichier ou fait une faute dans le message :

```bash
# Ajouter le fichier oublié
git add fichier-oublie.txt

# Modifier le dernier commit
git commit --amend -m "Nouveau message"
```

**⚠️ Attention** : ne faites ceci que si vous n'avez PAS encore partagé le commit (push).

### Cas 3 : Revenir à un commit précédent

**Voir l'historique** :

```bash
git log --oneline
```

**Revenir temporairement** :

```bash
git checkout <hash-du-commit>
```

**Revenir définitivement (⚠️ DANGEREUX)** :

```bash
# Annule les commits mais garde les modifications
git reset <hash-du-commit>

# Annule TOUT (modifications comprises)
git reset --hard <hash-du-commit>
```

---

## Travailler avec les branches

Les branches permettent de développer des fonctionnalités sans affecter le code principal.

### Voir les branches

```bash
# Lister les branches locales
git branch

# Lister toutes les branches (locales et distantes)
git branch -a
```

La branche avec `*` est votre branche actuelle.

### Créer une branche

```bash
git branch nom-de-la-branche

# Exemple
git branch nouvelle-fonctionnalite
```

### Changer de branche

```bash
git checkout nom-de-la-branche

# Exemple
git checkout nouvelle-fonctionnalite
```

### Créer ET changer de branche (raccourci)

```bash
git checkout -b nom-de-la-branche

# Exemple
git checkout -b correction-bug
```

### Fusionner des branches (merge)

Une fois votre travail terminé sur une branche, fusionnez-la avec la branche principale :

```bash
# 1. Retourner sur la branche principale
git checkout main

# 2. Fusionner votre branche
git merge nom-de-la-branche

# Exemple
git merge nouvelle-fonctionnalite
```

### Supprimer une branche

```bash
# Supprimer une branche fusionnée
git branch -d nom-de-la-branche

# Forcer la suppression (même non fusionnée)
git branch -D nom-de-la-branche
```

---

## Gérer les conflits

Un **conflit** arrive quand Git ne peut pas fusionner automatiquement deux modifications.

### Quand surviennent les conflits ?

Quand deux personnes (ou deux branches) modifient la même ligne de code.

### Résoudre un conflit

1. Git vous avertit : `CONFLICT (content): Merge conflict in fichier.txt`

2. Ouvrez le fichier en conflit, vous verrez :

```
<<<<<<< HEAD
Votre version
=======
L'autre version
>>>>>>> nom-branche
```

3. Choisissez quelle version garder (ou fusionnez manuellement)

4. Supprimez les marqueurs `<<<<<<<`, `=======`, `>>>>>>>`

5. Ajoutez le fichier résolu :

```bash
git add fichier.txt
```

6. Terminez le merge :

```bash
git commit -m "Résolution du conflit"
```

### Outils visuels pour les conflits

```bash
# Lancer l'outil de merge
git mergetool
```

Ou utilisez votre IDE (VS Code, PyCharm) qui gère très bien les conflits visuellement.

---

## Travailler avec des dépôts distants

### GitHub, GitLab, Bitbucket : quelle différence ?

| Service | Description | Prix |
|---------|-------------|------|
| **GitHub** | Le plus populaire, racheté par Microsoft | Gratuit (dépôts publics et privés) |
| **GitLab** | Alternative open source, plus de fonctionnalités CI/CD | Gratuit (dépôts privés illimités) |
| **Bitbucket** | De l'éditeur d'Atlassian (Jira) | Gratuit (petites équipes) |

**Pour débuter** : choisissez **GitHub**, c'est le plus utilisé et a la plus grande communauté.

### Créer un compte GitHub

1. Allez sur https://github.com
2. Cliquez sur "Sign up"
3. Suivez les instructions
4. Confirmez votre email

### Créer un nouveau dépôt sur GitHub

1. Connectez-vous à GitHub
2. Cliquez sur le `+` en haut à droite
3. Sélectionnez "New repository"
4. Donnez un nom à votre dépôt
5. Choisissez public ou privé
6. (Optionnel) Ajoutez un README
7. Cliquez sur "Create repository"

### Cloner un dépôt existant

**Cloner** = télécharger un dépôt distant sur votre ordinateur.

```bash
git clone https://github.com/utilisateur/nom-depot.git

# Exemple
git clone https://github.com/torvalds/linux.git
```

Cela crée un dossier avec le code et tout l'historique Git.

### Connecter un dépôt local à GitHub

Si vous avez déjà un projet local :

```bash
# Ajouter le dépôt distant
git remote add origin https://github.com/votre-nom/votre-depot.git

# Vérifier
git remote -v

# Envoyer votre code
git push -u origin main
```

### Les commandes principales avec les dépôts distants

**Envoyer vos commits (push)** :

```bash
# Première fois
git push -u origin main

# Ensuite, simplement
git push
```

**Récupérer les modifications (pull)** :

```bash
git pull
```

Équivalent à :
```bash
git fetch  # Télécharge les modifications
git merge  # Les fusionne avec votre branche
```

**Voir les dépôts distants** :

```bash
git remote -v
```

---

## Authentification avec GitHub

### Méthode 1 : HTTPS avec token (recommandé)

Les mots de passe ne fonctionnent plus. Utilisez un **Personal Access Token**.

**Créer un token** :

1. GitHub → Settings (paramètres)
2. Developer settings → Personal access tokens → Tokens (classic)
3. Generate new token
4. Cochez les permissions nécessaires (repo, workflow)
5. Générez et **copiez le token** (vous ne le reverrez plus !)

**Utiliser le token** :

Lors du premier `git push`, entrez :
- Username : votre nom d'utilisateur GitHub
- Password : **le token** (pas votre mot de passe)

### Méthode 2 : SSH (pour les utilisateurs avancés)

**Générer une clé SSH** :

```bash
ssh-keygen -t ed25519 -C "votre.email@example.com"
```

Appuyez sur Entrée pour accepter l'emplacement par défaut.

**Ajouter la clé à l'agent SSH** :

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

**Copier la clé publique** :

```bash
cat ~/.ssh/id_ed25519.pub
```

**Ajouter à GitHub** :

1. GitHub → Settings → SSH and GPG keys
2. New SSH key
3. Collez votre clé publique
4. Add SSH key

**Utiliser l'URL SSH** :

```bash
git clone git@github.com:utilisateur/depot.git
```

---

## Le fichier .gitignore

Le fichier `.gitignore` indique à Git quels fichiers **ne pas** suivre.

### Pourquoi ?

Pour éviter de commiter :
- Fichiers temporaires (`.log`, `.tmp`)
- Fichiers de configuration locale (`.env`, `config.local`)
- Dépendances (`node_modules/`, `venv/`)
- Fichiers compilés (`.o`, `.pyc`)
- Fichiers sensibles (mots de passe, clés API)

### Créer un .gitignore

Créez un fichier nommé `.gitignore` à la racine de votre projet :

```bash
nano .gitignore
```

### Exemples de .gitignore

**Pour Python** :
```
# Environnements virtuels
venv/
env/
.venv/

# Fichiers Python compilés
__pycache__/
*.pyc
*.pyo
*.pyd

# Base de données locale
*.db
*.sqlite3

# Variables d'environnement
.env

# IDE
.vscode/
.idea/
*.swp
```

**Pour Node.js** :
```
# Dépendances
node_modules/
npm-debug.log

# Production
/build
/dist

# Environnement
.env
.env.local

# IDE
.vscode/
.idea/
```

**Pour tous les projets** :
```
# Systèmes d'exploitation
.DS_Store
Thumbs.db

# Éditeurs
*.swp
*.swo
*~
.vscode/
.idea/

# Logs
*.log

# Fichiers temporaires
*.tmp
*.temp
```

### Sites utiles pour .gitignore

- https://gitignore.io - Génère des .gitignore personnalisés
- https://github.com/github/gitignore - Collection de templates

---

## Commandes utiles

### Renommer un fichier

```bash
git mv ancien-nom.txt nouveau-nom.txt
```

### Supprimer un fichier

```bash
git rm fichier.txt
```

### Voir qui a modifié une ligne (blame)

```bash
git blame fichier.txt
```

### Rechercher dans l'historique

```bash
# Rechercher dans les commits
git log --grep="mot-clé"

# Rechercher dans le code
git log -S "fonction_recherchee"
```

### Créer un alias

Pour raccourcir les commandes :

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.st status
git config --global alias.cm commit

# Maintenant vous pouvez taper
git st    # au lieu de git status
git co    # au lieu de git checkout
```

### Sauvegarder temporairement (stash)

Mettre de côté vos modifications sans les commiter :

```bash
# Sauvegarder
git stash

# Voir les sauvegardes
git stash list

# Restaurer la dernière sauvegarde
git stash pop

# Restaurer sans supprimer
git stash apply
```

---

## Workflow recommandé pour débuter

### Workflow simple (seul sur un projet)

```bash
# 1. Modifier vos fichiers
# 2. Vérifier l'état
git status

# 3. Ajouter les modifications
git add .

# 4. Commiter
git commit -m "Description claire"

# 5. Envoyer sur GitHub (si configuré)
git push
```

### Workflow avec branches (recommandé)

```bash
# 1. Créer une branche pour votre fonctionnalité
git checkout -b ma-nouvelle-feature

# 2. Travailler et commiter
git add .
git commit -m "Ajout de la nouvelle fonctionnalité"

# 3. Retourner sur main
git checkout main

# 4. Fusionner votre branche
git merge ma-nouvelle-feature

# 5. Pousser vers GitHub
git push

# 6. Supprimer la branche locale
git branch -d ma-nouvelle-feature
```

---

## Outils graphiques pour Git

Si le terminal vous intimide, utilisez une interface graphique :

### GitKraken

**Interface élégante et puissante**

- Site : https://www.gitkraken.com
- Gratuit pour les projets publics
- Disponible sur Linux

Installation :
```bash
# Via Flatpak
flatpak install flathub com.axosoft.GitKraken
```

### Git Cola

**Simple et léger**

```bash
sudo apt install git-cola
```

### Gitg

**Visionneuse Git simple**

```bash
sudo apt install gitg
```

### Extension VS Code

VS Code intègre déjà Git visuellement :
- Icône de contrôle source dans la barre latérale
- Visualisation des changements
- Gestion des branches
- Extension GitLens pour plus de fonctionnalités

---

## Bonnes pratiques

### 1. Commitez souvent

Mieux vaut de nombreux petits commits qu'un énorme commit.

**Bon** : Un commit par fonctionnalité/correction
**Mauvais** : Un commit après une semaine de travail

### 2. Synchronisez régulièrement

```bash
# Tous les matins
git pull

# Après chaque commit important
git push
```

### 3. Utilisez des branches

Ne travaillez jamais directement sur `main` pour des fonctionnalités.

### 4. Écrivez de bons messages de commit

Suivez cette structure :

```
Résumé court (50 caractères max)

Description plus détaillée si nécessaire.
Expliquez POURQUOI, pas comment.

- Point 1
- Point 2
```

### 5. Relisez avant de commiter

```bash
git diff
git status
```

### 6. Ne commitez jamais de :

- Mots de passe
- Clés API
- Fichiers de configuration avec données sensibles
- Fichiers très volumineux (>100 MB)

### 7. Gardez votre historique propre

Évitez les commits du type "oups", "test", "correction typo".

---

## Ressources pour aller plus loin

### Tutoriels interactifs

- **Learn Git Branching** : https://learngitbranching.js.org (excellent !)
- **GitHub Learning Lab** : https://lab.github.com
- **Git-it** : https://github.com/jlord/git-it-electron

### Documentation

- **Documentation officielle Git** : https://git-scm.com/doc
- **Pro Git Book** (gratuit) : https://git-scm.com/book/fr/v2
- **Git Cheat Sheet** : https://education.github.com/git-cheat-sheet-education.pdf

### Aide-mémoire (cheat sheet)

Commandes essentielles :

```bash
# Configuration
git config --global user.name "Nom"
git config --global user.email "email"

# Initialisation
git init
git clone <url>

# État et différences
git status
git diff

# Ajout et commit
git add <fichier>
git add .
git commit -m "message"

# Historique
git log
git log --oneline

# Branches
git branch
git checkout <branche>
git checkout -b <nouvelle-branche>
git merge <branche>

# Distant
git remote add origin <url>
git push -u origin main
git pull

# Annulation
git restore <fichier>
git restore --staged <fichier>
```

---

## Dépannage courant

### "Permission denied (publickey)" lors du push

➡️ Problème d'authentification SSH.

Solution : utilisez HTTPS avec un token ou reconfigurez SSH.

### "fatal: not a git repository"

➡️ Vous n'êtes pas dans un dépôt Git.

Solution : `cd` dans votre projet ou faites `git init`.

### "Your branch is ahead of 'origin/main' by X commits"

➡️ Vous avez des commits locaux non envoyés.

Solution : `git push`

### "Your branch is behind 'origin/main'"

➡️ Le dépôt distant a des commits que vous n'avez pas.

Solution : `git pull`

### Conflit de merge

➡️ Deux modifications incompatibles.

Solution : Éditez les fichiers en conflit, résolvez, puis `git add` et `git commit`.

### "detached HEAD state"

➡️ Vous avez fait `git checkout` sur un commit spécifique.

Solution : `git checkout main` pour revenir à la normale.

---

## Conclusion

Git peut sembler compliqué au début, mais il devient vite indispensable. Voici ce qu'il faut retenir :

**Les commandes essentielles pour 90% de votre travail** :
```bash
git status
git add .
git commit -m "message"
git push
git pull
```

**Conseils finaux** :
- ✅ Commitez souvent
- ✅ Utilisez des messages clairs
- ✅ Synchronisez régulièrement
- ✅ N'ayez pas peur d'expérimenter avec les branches
- ✅ Utilisez .gitignore dès le début

Git est comme conduire une voiture : intimidant au début, mais naturel après quelques semaines de pratique. Plus vous l'utilisez, plus vous apprécierez sa puissance !

**Bienvenue dans le monde de la gestion de versions ! 🚀**

⏭️ [Bases de données (MySQL, PostgreSQL, MongoDB)](/19-developpement-et-programmation/04-bases-de-donnees.md)
