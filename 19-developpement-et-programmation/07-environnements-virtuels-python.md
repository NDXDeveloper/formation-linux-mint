🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 19.7 - Environnements virtuels Python (venv, pipenv)

## Introduction

### Qu'est-ce qu'un environnement virtuel ?

Un **environnement virtuel Python** est un espace isolé qui contient une copie de Python et ses propres bibliothèques, indépendamment du système global.

**Analogie simple** :
Imaginez votre ordinateur comme un **immeuble** :
- Chaque **appartement** (environnement virtuel) a sa propre cuisine avec ses propres ustensiles
- Vous ne mélangez pas les ustensiles de tous les appartements dans une seule cuisine commune
- Si un appartement a besoin d'une poêle spéciale, cela n'affecte pas les autres

C'est exactement ce que font les environnements virtuels : **isoler vos projets Python**.

### Le problème que les environnements virtuels résolvent

**Sans environnement virtuel** :

```
Système global
├── Python 3.11
├── Django 4.2
├── Flask 2.0
├── requests 2.28
└── numpy 1.24
```

**Problèmes** :

**Projet A** : nécessite Django 4.2  
**Projet B** : nécessite Django 3.2 (ancienne version)  

❌ **Conflit !** Vous ne pouvez pas avoir deux versions de Django en même temps sur votre système.

**Avec environnements virtuels** :

```
Système global
├── Python 3.11

Projet A (env_a/)
├── Python 3.11
├── Django 4.2
└── requests 2.28

Projet B (env_b/)
├── Python 3.11
├── Django 3.2
└── requests 2.25
```

✅ **Aucun conflit !** Chaque projet a ses propres dépendances.

### Pourquoi utiliser des environnements virtuels ?

**1. Isolation des dépendances**
- ✅ Chaque projet a ses propres bibliothèques
- ✅ Pas de conflits entre versions

**2. Reproductibilité**
- ✅ Facile de partager l'environnement exact avec d'autres
- ✅ Déploiement sans surprises

**3. Sécurité**
- ✅ Ne pas polluer le système global
- ✅ Facile de tout supprimer

**4. Expérimentation**
- ✅ Tester de nouvelles bibliothèques sans risque
- ✅ Supprimer l'environnement si ça ne fonctionne pas

---

## venv : L'outil standard

### Qu'est-ce que venv ?

**venv** est le module intégré à Python (depuis Python 3.3) pour créer des environnements virtuels.

**Avantages** :
- ✅ Inclus avec Python (rien à installer)
- ✅ Simple et léger
- ✅ Recommandé officiellement
- ✅ Parfait pour débuter

### Vérifier que venv est disponible

```bash
python3 -m venv --help
```

Si vous voyez l'aide, c'est installé ! Sinon :

```bash
sudo apt install python3-venv
```

---

## Utiliser venv : Guide complet

### 1. Créer un environnement virtuel

**Syntaxe de base** :

```bash
python3 -m venv nom_environnement
```

**Exemple pratique** :

```bash
# Créer un dossier pour votre projet
mkdir mon_projet  
cd mon_projet  

# Créer l'environnement virtuel
python3 -m venv venv
```

**⚠️ Convention** : On appelle souvent l'environnement `venv`, `env`, ou `.venv`

**Ce qui est créé** :

```
mon_projet/
└── venv/
    ├── bin/           # Scripts (Linux/Mac)
    ├── include/       # Headers C
    ├── lib/           # Bibliothèques Python
    └── pyvenv.cfg     # Configuration
```

### 2. Activer l'environnement virtuel

**Linux/Mac** :

```bash
source venv/bin/activate
```

**Vous verrez** :

```bash
(venv) utilisateur@machine:~/mon_projet$
```

Le `(venv)` indique que l'environnement est actif ! 🎉

**Windows (si vous utilisez WSL)** :

```bash
source venv/Scripts/activate
```

### 3. Vérifier l'activation

```bash
# Voir quel Python est utilisé
which python
# Devrait afficher : /home/user/mon_projet/venv/bin/python

# Vérifier la version
python --version

# Voir quel pip est utilisé
which pip
# Devrait afficher : /home/user/mon_projet/venv/bin/pip
```

### 4. Installer des paquets

Une fois l'environnement activé :

```bash
# Installer un paquet
pip install requests

# Installer plusieurs paquets
pip install flask django numpy

# Installer une version spécifique
pip install django==4.2.0

# Voir les paquets installés
pip list
```

**Important** : Les paquets s'installent **uniquement** dans cet environnement, pas sur votre système !

### 5. Créer un fichier requirements.txt

Pour partager votre environnement avec d'autres :

```bash
# Générer le fichier requirements.txt
pip freeze > requirements.txt
```

**Contenu de requirements.txt** :

```
certifi==2023.7.22  
charset-normalizer==3.2.0  
Django==4.2.0  
idna==3.4  
requests==2.31.0  
urllib3==2.0.4  
```

**Installer depuis requirements.txt** :

```bash
pip install -r requirements.txt
```

### 6. Désactiver l'environnement

Quand vous avez fini de travailler :

```bash
deactivate
```

Le `(venv)` disparaît, vous êtes de retour dans le système global.

### 7. Supprimer l'environnement

Simple : supprimez le dossier !

```bash
rm -rf venv
```

Puis recréez-en un nouveau si nécessaire.

---

## Workflow typique avec venv

**Démarrer un nouveau projet** :

```bash
# 1. Créer le dossier du projet
mkdir mon_projet  
cd mon_projet  

# 2. Créer l'environnement virtuel
python3 -m venv venv

# 3. Activer
source venv/bin/activate

# 4. Installer les dépendances
pip install flask requests

# 5. Sauvegarder les dépendances
pip freeze > requirements.txt

# 6. Créer votre fichier .gitignore
echo "venv/" > .gitignore  
echo "__pycache__/" >> .gitignore  
echo "*.pyc" >> .gitignore  

# 7. Commencer à coder !
nano app.py
```

**Reprendre un projet existant** :

```bash
# 1. Cloner ou ouvrir le projet
cd mon_projet

# 2. Créer l'environnement virtuel
python3 -m venv venv

# 3. Activer
source venv/bin/activate

# 4. Installer les dépendances
pip install -r requirements.txt

# 5. Travailler !
```

**Fin de session** :

```bash
# Désactiver
deactivate
```

---

## Bonnes pratiques avec venv

### 1. Nom de l'environnement

**Conventions courantes** :

```bash
# Simple et standard
python3 -m venv venv

# Caché (ne s'affiche pas avec ls sans -a)
python3 -m venv .venv

# Descriptif
python3 -m venv env_projet
```

**Recommandation** : `venv` ou `.venv`

### 2. Ne jamais commiter l'environnement

**Toujours ajouter au .gitignore** :

```
venv/
.venv/
env/  
ENV/  
*.pyc
__pycache__/
```

**Pourquoi ?**
- Les environnements peuvent être gros (100+ Mo)
- Spécifiques à votre OS
- Faciles à recréer avec `requirements.txt`

### 3. Un environnement par projet

```
projets/
├── projet_a/
│   ├── venv/
│   ├── requirements.txt
│   └── app.py
├── projet_b/
│   ├── venv/
│   ├── requirements.txt
│   └── main.py
└── projet_c/
    ├── venv/
    ├── requirements.txt
    └── script.py
```

**Jamais** :
```
# ❌ Ne faites pas ça !
venv_global/  # Pour tous les projets
```

### 4. Mettre à jour pip dans l'environnement

```bash
# Après activation
pip install --upgrade pip
```

### 5. Activer automatiquement (optionnel)

**Avec direnv** (outil avancé) :

```bash
# Installation
sudo apt install direnv

# Dans le dossier du projet
echo "source venv/bin/activate" > .envrc  
direnv allow  

# L'environnement s'active automatiquement quand vous entrez dans le dossier !
```

---

## pipenv : L'outil moderne

### Qu'est-ce que pipenv ?

**pipenv** est un outil de gestion d'environnements virtuels plus moderne qui combine :
- `venv` (environnements virtuels)
- `pip` (gestion des paquets)
- `requirements.txt` (dépendances)

**En un seul outil !**

**Avantages** :
- ✅ Gestion automatique des environnements
- ✅ Fichier `Pipfile` plus lisible que `requirements.txt`
- ✅ Verrouillage des versions (`Pipfile.lock`)
- ✅ Détection automatique des conflits
- ✅ Séparation dev/production

**Inconvénients** :
- ❌ Nécessite installation
- ❌ Un peu plus lent que venv
- ❌ Moins universel

### Installation de pipenv

```bash
# Méthode 1 : Via pip (recommandé)
pip install --user pipenv

# Méthode 2 : Via apt
sudo apt install pipenv

# Vérification
pipenv --version
```

### Ajouter pipenv au PATH

Si `pipenv` n'est pas trouvé après installation :

```bash
# Ajouter à ~/.bashrc
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc  
source ~/.bashrc  
```

---

## Utiliser pipenv : Guide complet

### 1. Initialiser un projet

```bash
# Créer le dossier
mkdir mon_projet  
cd mon_projet  

# Initialiser pipenv (crée automatiquement un environnement)
pipenv install
```

**Ce qui est créé** :

```
mon_projet/
├── Pipfile         # Liste des dépendances
└── Pipfile.lock    # Versions verrouillées
```

L'environnement virtuel est créé dans `~/.local/share/virtualenvs/`

### 2. Installer des paquets

```bash
# Installer un paquet
pipenv install requests

# Installer plusieurs paquets
pipenv install flask django

# Installer une version spécifique
pipenv install django==4.2.0

# Installer en mode développement seulement
pipenv install pytest --dev
```

**Pipfile après installation** :

```toml
[[source]]
url = "https://pypi.org/simple"  
verify_ssl = true  
name = "pypi"  

[packages]
requests = "*"  
flask = "*"  
django = "==4.2.0"  

[dev-packages]
pytest = "*"

[requires]
python_version = "3.11"
```

**Plus lisible que requirements.txt !**

### 3. Activer l'environnement

**Méthode 1 : Shell interactif**

```bash
pipenv shell
```

Vous entrez dans un shell avec l'environnement activé.

**Méthode 2 : Exécuter une commande**

```bash
# Sans activer l'environnement
pipenv run python script.py  
pipenv run flask run  
pipenv run pytest  
```

### 4. Voir les dépendances

```bash
# Lister les paquets installés
pipenv graph
```

**Exemple de sortie** :

```
Flask==2.3.0
├── Werkzeug [required: >=2.3.0, installed: 2.3.6]
├── Jinja2 [required: >=3.1.2, installed: 3.1.2]
│   └── MarkupSafe [required: >=2.0, installed: 2.1.3]
└── click [required: >=8.1.3, installed: 8.1.5]
```

### 5. Mettre à jour les paquets

```bash
# Tout mettre à jour
pipenv update

# Mettre à jour un paquet spécifique
pipenv update requests
```

### 6. Désinstaller des paquets

```bash
pipenv uninstall requests
```

### 7. Sortir de l'environnement

```bash
# Si vous êtes dans pipenv shell
exit

# L'environnement se désactive automatiquement
```

### 8. Supprimer l'environnement

```bash
pipenv --rm
```

---

## Pipfile vs requirements.txt

### requirements.txt (ancien)

**Avantages** :
- ✅ Standard universel
- ✅ Simple
- ✅ Compris par tous les outils

**Inconvénients** :
- ❌ Format textuel basique
- ❌ Pas de séparation dev/prod
- ❌ Gestion manuelle des versions

**Exemple** :

```txt
django==4.2.0  
requests>=2.28.0  
pytest==7.4.0  
```

### Pipfile (moderne)

**Avantages** :
- ✅ Format structuré (TOML)
- ✅ Séparation dev/production
- ✅ Gestion automatique des versions
- ✅ Plus de métadonnées

**Exemple** :

```toml
[packages]
django = "==4.2.0"  
requests = ">=2.28.0"  

[dev-packages]
pytest = "==7.4.0"

[requires]
python_version = "3.11"
```

---

## Pipenv : Commandes essentielles

```bash
# INITIALISATION
pipenv install                    # Créer environnement  
pipenv install --python 3.11      # Spécifier version Python  

# GESTION DES PAQUETS
pipenv install paquet             # Installer  
pipenv install paquet --dev       # Dev seulement  
pipenv uninstall paquet           # Désinstaller  
pipenv update                     # Tout mettre à jour  
pipenv graph                      # Voir dépendances  

# ENVIRONNEMENT
pipenv shell                      # Activer shell  
pipenv run commande              # Exécuter commande  
exit                             # Quitter shell  
pipenv --rm                      # Supprimer environnement  

# INFORMATIONS
pipenv --where                   # Dossier du projet  
pipenv --venv                    # Dossier de l'environnement  
pipenv check                     # Vérifier sécurité  

# EXPORTS
pipenv requirements > req.txt    # Générer requirements.txt  
pipenv requirements --dev > dev-req.txt  
```

---

## Comparaison venv vs pipenv

| Critère | venv | pipenv |
|---------|------|--------|
| **Installation** | Inclus avec Python | Nécessite installation |
| **Simplicité** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Gestion automatique** | ❌ Manuel | ✅ Automatique |
| **Fichier config** | requirements.txt | Pipfile + Pipfile.lock |
| **Dev/Prod** | Un seul fichier | Séparés |
| **Performance** | ⭐⭐⭐⭐⭐ Rapide | ⭐⭐⭐ Plus lent |
| **Universalité** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Courbe apprentissage** | Facile | Moyenne |
| **Recommandé pour** | Débuter, simple | Projets complexes |

---

## Autres outils d'environnements virtuels

### Poetry

**Alternative moderne à pipenv**

```bash
# Installation
curl -sSL https://install.python-poetry.org | python3 -

# Utilisation
poetry new mon_projet  
cd mon_projet  
poetry add requests  
poetry install  
```

**Avantages** :
- ✅ Très rapide
- ✅ Gestion de paquets excellente
- ✅ Publication PyPI intégrée
- ✅ Très utilisé actuellement

### Conda/Miniconda

**Gestionnaire d'environnements complet**

```bash
# Installation Miniconda
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh  
bash Miniconda3-latest-Linux-x86_64.sh  

# Créer environnement
conda create -n mon_env python=3.11  
conda activate mon_env  
conda install numpy pandas  
```

**Avantages** :
- ✅ Gère Python + bibliothèques système
- ✅ Excellent pour data science
- ✅ Packages optimisés

**Inconvénients** :
- ❌ Lourd (plusieurs Go)
- ❌ Peut entrer en conflit avec pip

### pyenv + pyenv-virtualenv

**Gestion avancée de versions Python**

```bash
# Installation
curl https://pyenv.run | bash

# Installer plusieurs versions Python
pyenv install 3.11.0  
pyenv install 3.10.0  

# Créer environnement
pyenv virtualenv 3.11.0 mon_env  
pyenv activate mon_env  
```

**Idéal pour** : tester code sur plusieurs versions Python

---

## Cas pratiques

### Projet Flask simple

```bash
# Créer le projet
mkdir flask_app  
cd flask_app  

# Méthode 1 : avec venv
python3 -m venv venv  
source venv/bin/activate  
pip install flask  
pip freeze > requirements.txt  

# Méthode 2 : avec pipenv
pipenv install flask  
pipenv shell  
```

**app.py** :

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return '<h1>Hello from Flask!</h1>'

if __name__ == '__main__':
    app.run(debug=True)
```

**Lancer** :

```bash
# Avec venv
source venv/bin/activate  
python app.py  

# Avec pipenv
pipenv run python app.py
```

### Projet Data Science

```bash
mkdir data_projet  
cd data_projet  

# Avec venv
python3 -m venv venv  
source venv/bin/activate  
pip install numpy pandas matplotlib jupyter  
pip freeze > requirements.txt  

# Lancer Jupyter
jupyter notebook
```

### Projet avec tests

```bash
mkdir mon_package  
cd mon_package  

# Avec pipenv (séparation dev/prod)
pipenv install requests  # Production  
pipenv install pytest pytest-cov --dev  # Développement  

# Structure
mkdir tests  
touch tests/test_main.py  

# Lancer tests
pipenv run pytest
```

---

## Workflow recommandé pour débuter

### Pour un nouveau projet

**Étape 1 : Choisir votre outil**

```bash
# Débutant ou projet simple ? → venv
python3 -m venv venv

# Projet plus complexe ? → pipenv
pipenv install
```

**Étape 2 : Activer**

```bash
# venv
source venv/bin/activate

# pipenv
pipenv shell
```

**Étape 3 : Installer dépendances**

```bash
# venv
pip install flask requests

# pipenv
pipenv install flask requests
```

**Étape 4 : Sauvegarder**

```bash
# venv
pip freeze > requirements.txt

# pipenv
# Automatique dans Pipfile !
```

**Étape 5 : Git**

```bash
git init  
echo "venv/" > .gitignore  
echo "__pycache__/" >> .gitignore  
git add .  
git commit -m "Initial commit"  
```

### Pour rejoindre un projet existant

```bash
# Cloner
git clone url_projet  
cd projet  

# Si requirements.txt existe (venv)
python3 -m venv venv  
source venv/bin/activate  
pip install -r requirements.txt  

# Si Pipfile existe (pipenv)
pipenv install  
pipenv shell  
```

---

## Dépannage

### "venv" ou "pipenv" command not found

**venv** :

```bash
sudo apt install python3-venv
```

**pipenv** :

```bash
pip install --user pipenv  
export PATH="$HOME/.local/bin:$PATH"  
```

### L'environnement ne s'active pas

**Vérifiez le chemin** :

```bash
# Doit pointer vers venv/bin/activate
ls venv/bin/activate  
source venv/bin/activate  
```

### Packages s'installent globalement malgré l'environnement

**Vérifiez que l'environnement est actif** :

```bash
which pip
# Doit afficher : /chemin/vers/projet/venv/bin/pip
# Si pas le cas, réactivez
```

### Conflits de dépendances avec pipenv

```bash
# Voir les conflits
pipenv check

# Résolution forcée
pipenv lock --clear  
pipenv install  
```

### Environnement pipenv introuvable

```bash
# Voir où est l'environnement
pipenv --venv

# Recréer si nécessaire
pipenv --rm  
pipenv install  
```

---

## Intégration avec les IDE

### VS Code

**Configuration automatique** :

1. Ouvrez le dossier du projet
2. VS Code détecte automatiquement `venv/`
3. En bas à droite, cliquez sur la version Python
4. Sélectionnez l'interpréteur dans `venv/bin/python`

**Ou créez `.vscode/settings.json`** :

```json
{
    "python.defaultInterpreterPath": "${workspaceFolder}/venv/bin/python"
}
```

### PyCharm

1. File → Settings → Project → Python Interpreter
2. Cliquez sur la roue dentée → Add
3. Sélectionnez "Existing environment"
4. Parcourez jusqu'à `venv/bin/python`

### Jupyter Notebook

```bash
# Activer l'environnement
source venv/bin/activate

# Installer jupyter
pip install jupyter

# Lancer
jupyter notebook
```

---

## Bonnes pratiques globales

### 1. Toujours utiliser un environnement virtuel

```bash
# ✅ Bon
cd mon_projet  
python3 -m venv venv  
source venv/bin/activate  
pip install ...  

# ❌ Mauvais
pip install ...  # Installe globalement !
```

### 2. Ne jamais utiliser sudo avec pip dans un venv

```bash
# ✅ Bon
pip install requests

# ❌ Mauvais
sudo pip install requests  # Casse l'environnement !
```

### 3. Documenter les dépendances

```bash
# Toujours avoir un requirements.txt ou Pipfile
pip freeze > requirements.txt
```

### 4. Ignorer l'environnement dans Git

**.gitignore** :

```
venv/
.venv/
env/
*.pyc
__pycache__/
.pytest_cache/
```

### 5. Tester régulièrement

```bash
# Créer un nouvel environnement de test
python3 -m venv test_env  
source test_env/bin/activate  
pip install -r requirements.txt  
# Votre code fonctionne-t-il ?
```

---

## Ressources pour aller plus loin

### Documentation officielle

- **venv** : https://docs.python.org/3/library/venv.html
- **pipenv** : https://pipenv.pypa.io/
- **pip** : https://pip.pypa.io/

### Tutoriels

- **Real Python - venv** : https://realpython.com/python-virtual-environments-a-primer/
- **Pipenv Guide** : https://pipenv-fork.readthedocs.io/

### Outils complémentaires

- **virtualenvwrapper** : Facilite la gestion de multiples environnements
- **pyenv** : Gestion de versions Python
- **Poetry** : Alternative moderne à pipenv

---

## Aide-mémoire

### venv

```bash
# Créer
python3 -m venv venv

# Activer
source venv/bin/activate

# Installer
pip install paquet

# Sauvegarder
pip freeze > requirements.txt

# Installer depuis fichier
pip install -r requirements.txt

# Désactiver
deactivate

# Supprimer
rm -rf venv
```

### pipenv

```bash
# Créer/initialiser
pipenv install

# Installer paquet
pipenv install paquet  
pipenv install paquet --dev  

# Activer
pipenv shell

# Exécuter commande
pipenv run python script.py

# Voir dépendances
pipenv graph

# Quitter
exit

# Supprimer
pipenv --rm
```

---

## Conclusion

Les environnements virtuels sont **essentiels** pour tout développeur Python. Voici l'essentiel :

**Pourquoi ?**
- 🔒 Isolation des projets
- 🔄 Reproductibilité
- 🛡️ Éviter les conflits
- 🧪 Expérimentation sans risque

**Quel outil choisir ?**

**Débutant** :
- ➡️ **venv** - Simple, inclus, universel

**Développeur confirmé** :
- ➡️ **pipenv** - Moderne, gestion automatique
- ➡️ **Poetry** - Très performant, tendance actuelle

**Data Science** :
- ➡️ **Conda** - Packages scientifiques optimisés

**Workflow minimal** :
```bash
python3 -m venv venv  
source venv/bin/activate  
pip install -r requirements.txt  
# Codez !
deactivate
```

**Règle d'or** : **Un projet = Un environnement virtuel**

N'oubliez jamais : installer des paquets Python sans environnement virtuel, c'est comme cuisiner sans laver ses ustensiles entre deux plats... ça finit toujours mal ! 🍳

**Bon développement Python ! 🐍**

⏭️ [Outils de build et CI/CD](/19-developpement-et-programmation/08-outils-de-build-et-cicd.md)
