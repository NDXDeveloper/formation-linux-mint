🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 19.8 - Outils de build et CI/CD

## Introduction

### Qu'est-ce que le "build" ?

Le **build** (construction) est le processus qui transforme votre code source en un programme exécutable ou déployable.

**Analogie simple** :
Imaginez que vous construisez une maison :
- Le **code source** = les plans de l'architecte
- Le **build** = la construction réelle de la maison
- Le **programme final** = la maison habitable

**Étapes typiques d'un build** :
1. 📥 Récupérer le code
2. 📦 Installer les dépendances
3. 🔨 Compiler (si nécessaire)
4. ✅ Lancer les tests
5. 📦 Créer le package final
6. 🚀 (Optionnel) Déployer

### Qu'est-ce que CI/CD ?

**CI/CD** signifie **Continuous Integration / Continuous Deployment** (Intégration Continue / Déploiement Continu).

**Analogie du restaurant** :
- **Sans CI/CD** : Le chef prépare tous les plats de la journée le matin, et les clients doivent attendre jusqu'au soir pour manger
- **Avec CI/CD** : Chaque plat est préparé dès qu'il est commandé, testé par le chef, et servi immédiatement s'il est bon

**Concrètement** :

**CI (Continuous Integration)** :
- ✅ À chaque modification du code (commit)
- ✅ Le code est automatiquement testé
- ✅ Les erreurs sont détectées immédiatement
- ✅ Tout le monde code sur la même base à jour

**CD (Continuous Deployment)** :
- ✅ Si les tests passent
- ✅ Le code est automatiquement déployé
- ✅ Les utilisateurs reçoivent les mises à jour rapidement
- ✅ Moins d'erreurs humaines

### Pourquoi utiliser CI/CD ?

**Sans CI/CD** :
```
Développeur → Code pendant 2 semaines → Push → Build manuel →  
Tests manuels → Bugs découverts → Corrections → Redéploiement manuel  
⏱️ Délai : Plusieurs jours/semaines
```

**Avec CI/CD** :
```
Développeur → Commit → Build auto → Tests auto → Déploiement auto
⏱️ Délai : Quelques minutes
✅ Feedback immédiat
```

**Avantages** :
- 🚀 **Livraison rapide** : De nouvelles fonctionnalités chaque jour
- 🐛 **Moins de bugs** : Détection immédiate des problèmes
- 🔄 **Retour en arrière facile** : Si un problème survient
- 👥 **Meilleure collaboration** : Tout le monde travaille sur la même version
- 😌 **Moins de stress** : Plus besoin de déploiements manuels le vendredi soir !

---

## Outils de build

### Make (le classique)

**Make** est l'outil de build historique, surtout utilisé pour C/C++.

**Installation** :

```bash
sudo apt install build-essential
```

**Créer un Makefile** :

```makefile
# Makefile simple pour un projet C

# Variables
CC = gcc  
CFLAGS = -Wall -g  
TARGET = mon_programme  

# Règle par défaut
all: $(TARGET)

# Comment construire le programme
$(TARGET): main.o utils.o
	$(CC) $(CFLAGS) -o $(TARGET) main.o utils.o

# Comment compiler main.c
main.o: main.c
	$(CC) $(CFLAGS) -c main.c

# Comment compiler utils.c
utils.o: utils.c
	$(CC) $(CFLAGS) -c utils.c

# Nettoyer les fichiers compilés
clean:
	rm -f *.o $(TARGET)

# Lancer le programme
run: $(TARGET)
	./$(TARGET)
```

**Utilisation** :

```bash
# Compiler
make

# Nettoyer
make clean

# Compiler et exécuter
make run
```

**Avantages** :
- ✅ Standard universel
- ✅ Simple pour des tâches basiques
- ✅ Très rapide

**Inconvénients** :
- ❌ Syntaxe parfois obscure
- ❌ Moins adapté aux langages modernes

### npm scripts (pour JavaScript/Node.js)

**npm** (Node Package Manager) intègre un système de scripts.

**package.json** :

```json
{
  "name": "mon-projet",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "build": "webpack --mode production",
    "test": "jest",
    "lint": "eslint .",
    "deploy": "npm run build && npm run test && ./deploy.sh"
  },
  "dependencies": {
    "express": "^4.18.0"
  },
  "devDependencies": {
    "jest": "^29.0.0",
    "nodemon": "^2.0.0"
  }
}
```

**Utilisation** :

```bash
# Lancer le serveur
npm start

# Mode développement avec rechargement auto
npm run dev

# Construire pour la production
npm run build

# Lancer les tests
npm test

# Tout faire : build + test + deploy
npm run deploy
```

**Avantages** :
- ✅ Intégré avec npm
- ✅ Simple et lisible
- ✅ Standard pour JavaScript

### Maven et Gradle (pour Java)

**Maven - pom.xml** :

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.exemple</groupId>
    <artifactId>mon-app</artifactId>
    <version>1.0</version>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.11.0</version>
            </plugin>
        </plugins>
    </build>
</project>
```

**Commandes** :

```bash
mvn clean      # Nettoyer  
mvn compile    # Compiler  
mvn test       # Tests  
mvn package    # Créer le JAR  
mvn install    # Installer localement  
```

**Gradle - build.gradle** :

```groovy
plugins {
    id 'java'
}

group = 'com.exemple'  
version = '1.0'  

repositories {
    mavenCentral()
}

dependencies {
    testImplementation 'junit:junit:4.13.2'
}
```

**Commandes** :

```bash
gradle build     # Construire  
gradle test      # Tests  
gradle run       # Exécuter  
```

### setuptools (pour Python)

**setup.py** :

```python
from setuptools import setup, find_packages

setup(
    name='mon-package',
    version='1.0.0',
    packages=find_packages(),
    install_requires=[
        'requests>=2.28.0',
        'flask>=2.0.0',
    ],
    entry_points={
        'console_scripts': [
            'mon-cli=mon_package.cli:main',
        ],
    },
)
```

**Utilisation** :

```bash
# Installer en mode développement
pip install -e .

# Créer un package distribuable
python setup.py sdist bdist_wheel
```

### Taskfile (alternative moderne à Make)

**Installation** :

```bash
sudo sh -c "$(curl -sSL https://taskfile.dev/install.sh)" -- -d -b /usr/local/bin
```

**Taskfile.yml** :

```yaml
version: '3'

tasks:
  build:
    desc: Construire le projet
    cmds:
      - go build -o bin/app .

  test:
    desc: Lancer les tests
    cmds:
      - go test ./...

  run:
    desc: Lancer l'application
    cmds:
      - task: build
      - ./bin/app

  clean:
    desc: Nettoyer
    cmds:
      - rm -rf bin/

  deploy:
    desc: Déployer
    deps: [test, build]
    cmds:
      - ./deploy.sh
```

**Utilisation** :

```bash
task build  
task test  
task deploy  
```

---

## CI/CD : Concepts fondamentaux

### Le pipeline CI/CD

Un **pipeline** est une séquence d'étapes automatisées.

```
┌─────────────────────────────────────────────────────────┐
│                    PIPELINE CI/CD                       │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  [Code Push] → [Build] → [Test] → [Deploy Staging] → ;  │
│               → [Test Integration] → [Deploy Prod]      │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

**Étapes typiques** :

1. **Source** : Récupérer le code depuis Git
2. **Build** : Compiler/construire
3. **Test** : Tests unitaires, tests d'intégration
4. **Quality** : Analyse de code (linting, security scan)
5. **Staging** : Déployer sur un environnement de test
6. **Production** : Déployer en production (si tout est vert)

### Environnements

**Développement (Dev)** :
- Votre machine locale
- Changements fréquents
- Bugs autorisés

**Staging (Pré-production)** :
- Copie de la production
- Tests finaux
- Validation avant production

**Production (Prod)** :
- Utilisateurs réels
- Haute disponibilité
- Zéro tolérance aux bugs critiques

---

## GitHub Actions

### Qu'est-ce que GitHub Actions ?

**GitHub Actions** est le système CI/CD intégré à GitHub.

**Avantages** :
- ✅ Gratuit pour les dépôts publics
- ✅ 2000 minutes/mois gratuites pour privés
- ✅ Intégré à GitHub
- ✅ Facile à configurer
- ✅ Énorme marketplace d'actions

### Créer votre premier workflow

**Structure** :

```
mon-projet/
├── .github/
│   └── workflows/
│       └── ci.yml
├── src/
└── tests/
```

**Exemple 1 : Test Python simple**

**.github/workflows/python-tests.yml** :

```yaml
name: Tests Python

# Quand lancer ce workflow
on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

# Les jobs à exécuter
jobs:
  test:
    # Système d'exploitation
    runs-on: ubuntu-latest

    steps:
    # 1. Récupérer le code
    - uses: actions/checkout@v4

    # 2. Installer Python
    - name: Configuration Python 3.11
      uses: actions/setup-python@v4
      with:
        python-version: '3.11'

    # 3. Installer les dépendances
    - name: Installer les dépendances
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
        pip install pytest

    # 4. Lancer les tests
    - name: Tests avec pytest
      run: |
        pytest
```

**Explication** :
- `on:` : Déclenché sur push ou pull request
- `runs-on:` : Ubuntu (Linux)
- `steps:` : Liste des étapes
- `uses:` : Actions prédéfinies
- `run:` : Commandes shell

**Exemple 2 : Build et déploiement Node.js**

**.github/workflows/node-deploy.yml** :

```yaml
name: Build et Deploy

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4

    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '18'
        cache: 'npm'

    - name: Installer dépendances
      run: npm ci

    - name: Lancer les tests
      run: npm test

    - name: Build
      run: npm run build

    - name: Déployer sur serveur
      if: success()
      run: |
        echo "Déploiement..."
        # Vos commandes de déploiement ici
```

**Exemple 3 : Multi-plateforme**

```yaml
name: Tests multi-OS

on: [push]

jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        python-version: ['3.9', '3.10', '3.11']

    steps:
    - uses: actions/checkout@v4
    - uses: actions/setup-python@v4
      with:
        python-version: ${{ matrix.python-version }}
    - run: |
        pip install -r requirements.txt
        pytest
```

**Ceci lance les tests sur** :
- 3 systèmes d'exploitation
- 3 versions de Python
- = 9 combinaisons au total !

### Actions populaires du Marketplace

```yaml
# Analyse de code
- name: Linter
  uses: github/super-linter@v5

# Upload d'artefacts
- name: Upload artefact
  uses: actions/upload-artifact@v3
  with:
    name: mon-app
    path: dist/

# Créer une release
- name: Create Release
  uses: softprops/action-gh-release@v1
  if: startsWith(github.ref, 'refs/tags/')

# Envoyer notification Discord
- name: Discord notification
  uses: Ilshidur/action-discord@master
  with:
    args: 'Déploiement réussi !'
```

### Secrets et variables

**Ajouter un secret** :
1. GitHub → Settings → Secrets and variables → Actions
2. New repository secret
3. Nom : `API_KEY`, Valeur : votre clé

**Utiliser dans workflow** :

```yaml
steps:
  - name: Déploiement
    env:
      API_KEY: ${{ secrets.API_KEY }}
      DB_PASSWORD: ${{ secrets.DB_PASSWORD }}
    run: ./deploy.sh
```

### Voir les résultats

1. GitHub → Onglet "Actions"
2. Voir l'historique des runs
3. Cliquer sur un run pour voir les détails
4. Chaque étape affiche ses logs

---

## GitLab CI/CD

### Qu'est-ce que GitLab CI/CD ?

**GitLab** a son propre système CI/CD très puissant.

**Avantages** :
- ✅ Intégré à GitLab
- ✅ Très complet
- ✅ 400 minutes/mois gratuites
- ✅ Peut s'auto-héberger

### Créer un pipeline GitLab

**.gitlab-ci.yml** (à la racine du projet) :

```yaml
# Définir les étapes du pipeline
stages:
  - build
  - test
  - deploy

# Variables globales
variables:
  NODE_VERSION: "18"

# Job de build
build:
  stage: build
  image: node:18
  script:
    - npm ci
    - npm run build
  artifacts:
    paths:
      - dist/
    expire_in: 1 hour

# Job de tests
test:
  stage: test
  image: node:18
  script:
    - npm ci
    - npm test
  coverage: '/Statements\s*:\s*(\d+\.\d+)%/'

# Déploiement staging
deploy_staging:
  stage: deploy
  image: alpine:latest
  before_script:
    - apk add --no-cache openssh-client
  script:
    - echo "Déploiement staging..."
  environment:
    name: staging
    url: https://staging.monsite.com
  only:
    - develop

# Déploiement production
deploy_production:
  stage: deploy
  script:
    - echo "Déploiement production..."
  environment:
    name: production
    url: https://monsite.com
  only:
    - main
  when: manual  # Nécessite validation manuelle
```

**Exemple Python** :

```yaml
image: python:3.11

stages:
  - test
  - deploy

before_script:
  - pip install -r requirements.txt

test:
  stage: test
  script:
    - pytest --cov=.
    - pylint src/

deploy:
  stage: deploy
  script:
    - python setup.py sdist bdist_wheel
    - pip install twine
    - twine upload dist/*
  only:
    - tags
```

### GitLab Runner

Pour exécuter les pipelines sur votre propre serveur :

```bash
# Installation
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash  
sudo apt install gitlab-runner  

# Enregistrement
sudo gitlab-runner register
```

---

## Jenkins (mention)

### Qu'est-ce que Jenkins ?

**Jenkins** est le système CI/CD historique, très puissant mais plus complexe.

**Installation** :

```bash
# Ajouter le dépôt
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

# Installer
sudo apt update  
sudo apt install jenkins  

# Démarrer
sudo systemctl start jenkins
```

**Accès** : http://localhost:8080

**Avantages** :
- ✅ Très flexible
- ✅ Énorme écosystème de plugins
- ✅ Auto-hébergé (contrôle total)

**Inconvénients** :
- ❌ Interface vieillotte
- ❌ Configuration complexe
- ❌ Nécessite maintenance

**Pour débuter** : GitHub Actions ou GitLab CI sont plus simples.

---

## Autres outils CI/CD

### CircleCI

**config.yml** :

```yaml
version: 2.1

jobs:
  build:
    docker:
      - image: cimg/python:3.11
    steps:
      - checkout
      - run: pip install -r requirements.txt
      - run: pytest

workflows:
  build-and-test:
    jobs:
      - build
```

### Travis CI

**.travis.yml** :

```yaml
language: python  
python:  
  - "3.11"

install:
  - pip install -r requirements.txt

script:
  - pytest
```

### Drone CI

**.drone.yml** :

```yaml
kind: pipeline  
type: docker  
name: default  

steps:
  - name: test
    image: python:3.11
    commands:
      - pip install -r requirements.txt
      - pytest
```

---

## Cas pratiques complets

### Projet Python avec GitHub Actions

**Structure** :

```
mon-projet/
├── .github/
│   └── workflows/
│       └── ci.yml
├── src/
│   └── app.py
├── tests/
│   └── test_app.py
├── requirements.txt
└── README.md
```

**.github/workflows/ci.yml** :

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Setup Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.11'

    - name: Cache dependencies
      uses: actions/cache@v3
      with:
        path: ~/.cache/pip
        key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}

    - name: Install dependencies
      run: |
        pip install -r requirements.txt
        pip install pytest pytest-cov flake8

    - name: Lint with flake8
      run: |
        flake8 src/ --max-line-length=120

    - name: Run tests with coverage
      run: |
        pytest --cov=src tests/

    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v3

  build:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'

    steps:
    - uses: actions/checkout@v4

    - name: Build Docker image
      run: |
        docker build -t mon-app:latest .

    - name: Push to registry
      run: |
        echo ${{ secrets.DOCKER_PASSWORD }} | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin
        docker push mon-app:latest

  deploy:
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'

    steps:
    - name: Deploy to server
      uses: appleboy/ssh-action@master
      with:
        host: ${{ secrets.HOST }}
        username: ${{ secrets.USERNAME }}
        key: ${{ secrets.SSH_KEY }}
        script: |
          cd /app
          docker pull mon-app:latest
          docker-compose up -d
```

### Projet Node.js avec GitLab CI

**.gitlab-ci.yml** :

```yaml
image: node:18

cache:
  paths:
    - node_modules/

stages:
  - install
  - test
  - build
  - deploy

install:
  stage: install
  script:
    - npm ci
  artifacts:
    paths:
      - node_modules/

lint:
  stage: test
  script:
    - npm run lint

test:
  stage: test
  script:
    - npm test
  coverage: '/Lines\s*:\s*(\d+\.\d+)%/'
  artifacts:
    reports:
      coverage_report:
        coverage_format: cobertura
        path: coverage/cobertura-coverage.xml

build:
  stage: build
  script:
    - npm run build
  artifacts:
    paths:
      - dist/
  only:
    - main
    - develop

deploy_staging:
  stage: deploy
  script:
    - npm run deploy:staging
  environment:
    name: staging
    url: https://staging.example.com
  only:
    - develop

deploy_production:
  stage: deploy
  script:
    - npm run deploy:production
  environment:
    name: production
    url: https://example.com
  only:
    - main
  when: manual
```

---

## Bonnes pratiques CI/CD

### 1. Fail Fast (Échouer rapidement)

```yaml
# ✅ Bon : Tests rapides en premier
jobs:
  lint:      # 30 secondes
  unit-test: # 2 minutes
  build:     # 5 minutes
  e2e-test:  # 15 minutes

# ❌ Mauvais : Tests lents en premier
jobs:
  e2e-test:  # 15 minutes (découvre l'erreur tard)
  build:
  unit-test:
  lint:
```

### 2. Cache intelligent

```yaml
# GitHub Actions
- uses: actions/cache@v3
  with:
    path: ~/.cache/pip
    key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}

# GitLab CI
cache:
  key: ${CI_COMMIT_REF_SLUG}
  paths:
    - node_modules/
    - .pip-cache/
```

### 3. Parallélisation

```yaml
# Lancer plusieurs jobs en parallèle
test:
  parallel:
    matrix:
      - NODE_VERSION: [14, 16, 18]
        OS: [ubuntu, windows]
```

### 4. Notifications

```yaml
# Slack
- name: Slack notification
  uses: 8398a7/action-slack@v3
  with:
    status: ${{ job.status }}
    webhook_url: ${{ secrets.SLACK_WEBHOOK }}
  if: always()
```

### 5. Gestion des secrets

```yaml
# ❌ Mauvais
script:
  - deploy.sh --password=monmotdepasse123

# ✅ Bon
script:
  - deploy.sh --password=${{ secrets.DEPLOY_PASSWORD }}
```

### 6. Environnements séparés

```yaml
deploy_dev:
  environment: development
  only: [develop]

deploy_staging:
  environment: staging
  only: [main]

deploy_prod:
  environment: production
  when: manual
  only: [tags]
```

### 7. Tests avant merge

```yaml
on:
  pull_request:  # Toujours tester les PR
  push:
    branches: [main]
```

### 8. Versionning sémantique

```yaml
# Créer un tag automatiquement
- name: Bump version
  uses: anothrNick/github-tag-action@1.36.0
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    WITH_V: true
```

---

## Monitoring et logs

### Voir l'état du build

**Badge dans README.md** :

```markdown
# GitHub Actions
![CI](https://github.com/user/repo/workflows/CI/badge.svg)

# GitLab CI
[![pipeline status](https://gitlab.com/user/repo/badges/main/pipeline.svg)]

# CircleCI
[![CircleCI](https://circleci.com/gh/user/repo.svg?style=svg)]
```

### Notifications

**Email automatique** :
- GitHub : Settings → Notifications
- GitLab : Intégré par défaut

**Discord/Slack** :
- Webhooks dans les workflows

---

## Dépannage

### Pipeline échoue sans raison apparente

**Solutions** :

```bash
# 1. Vérifier les logs détaillés
# GitHub : Cliquer sur le job qui a échoué

# 2. Tester localement avec act (GitHub Actions)
# Installation
curl https://raw.githubusercontent.com/nektos/act/master/install.sh | sudo bash

# Exécuter localement
act -j test

# 3. Mode debug
# GitHub Actions : Ajouter un secret ACTIONS_STEP_DEBUG=true
```

### Problèmes de cache

```yaml
# Invalider le cache en changeant la clé
cache:
  key: cache-v2-${{ hashFiles('requirements.txt') }}
```

### Timeouts

```yaml
# Augmenter le timeout (défaut : 60 min)
jobs:
  test:
    timeout-minutes: 120
```

### Secrets non disponibles

```bash
# Vérifier que le secret existe
# GitHub : Settings → Secrets → Actions

# Vérifier le nom exact (sensible à la casse)
${{ secrets.API_KEY }}  # ✅
${{ secrets.api_key }}  # ❌
```

---

## Ressources pour apprendre

### Documentation officielle

- **GitHub Actions** : https://docs.github.com/en/actions
- **GitLab CI/CD** : https://docs.gitlab.com/ee/ci/
- **Jenkins** : https://www.jenkins.io/doc/

### Tutoriels

- **GitHub Learning Lab** : https://lab.github.com/
- **GitLab CI/CD Examples** : https://docs.gitlab.com/ee/ci/examples/

### Exemples de workflows

- **Awesome Actions** : https://github.com/sdras/awesome-actions
- **GitHub Actions Marketplace** : https://github.com/marketplace?type=actions

---

## Aide-mémoire

### GitHub Actions

```yaml
# Workflow minimal
name: CI  
on: [push]  
jobs:  
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm test
```

### GitLab CI

```yaml
# Pipeline minimal
stages:
  - test

test:
  stage: test
  script:
    - npm test
```

### Commandes utiles

```bash
# Tester GitHub Actions localement
act

# Valider GitLab CI
gitlab-ci-lint .gitlab-ci.yml

# Jenkins CLI
java -jar jenkins-cli.jar -s http://localhost:8080 build mon-job
```

---

## Conclusion

CI/CD est devenu **indispensable** dans le développement moderne. Voici l'essentiel :

**Pourquoi CI/CD ?**
- 🚀 Livraison rapide et fréquente
- 🐛 Détection précoce des bugs
- 🔄 Déploiements automatisés et fiables
- 👥 Meilleure collaboration d'équipe

**Par où commencer ?**

**Niveau débutant** :
1. ✅ Choisissez **GitHub Actions** (si sur GitHub) ou **GitLab CI** (si sur GitLab)
2. ✅ Commencez simple : juste lancer les tests
3. ✅ Ajoutez progressivement : linting, build, deploy

**Workflow minimal** :
```yaml
on: [push]  
jobs:  
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: |
          pip install -r requirements.txt
          pytest
```

**Next steps** :
- Ajoutez le cache pour accélérer
- Mettez en place des environnements (staging, prod)
- Configurez les notifications
- Explorez le marketplace d'actions

**Règle d'or** : Commencez petit, itérez, améliorez progressivement !

CI/CD peut sembler intimidant au début, mais une fois mis en place, c'est un gain de temps énorme et vous vous demanderez comment vous avez pu vivre sans ! 🚀

**Bon build et bon déploiement ! ⚙️**

⏭️ [Ligne de commande avancée](/20-ligne-de-commande-avancee/README.md)
