🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 19.6 - Conteneurs Docker et Docker Compose

## Introduction

### Qu'est-ce que Docker ?

**Docker** est une plateforme qui permet d'empaqueter, distribuer et exécuter des applications dans des **conteneurs**.

**Analogie simple** :
Imaginez que vous déménagez. Au lieu de transporter des objets en vrac, vous utilisez des **containers standardisés** :
- Chaque container contient tout ce dont il a besoin (vêtements, livres, vaisselle)
- Les containers sont tous de la même taille et faciles à transporter
- Peu importe où vous allez, vos containers fonctionnent partout (camion, train, bateau)

**C'est exactement ce que fait Docker** : il met votre application et tout ce dont elle a besoin dans un "container" qui fonctionne partout de la même manière !

### Le problème que Docker résout

**Sans Docker** :
```
Développeur : "Ça marche sur ma machine !"
Ops : "Mais pas en production..."
```

**Pourquoi ?**
- ❌ Versions différentes (Python 3.8 vs 3.11)
- ❌ Dépendances manquantes
- ❌ Configuration différente
- ❌ Système d'exploitation différent

**Avec Docker** :
```
Développeur : "Voici mon conteneur Docker"
Ops : "Ça fonctionne partout pareil !"
```

**Avantages** :
- ✅ L'application et ses dépendances voyagent ensemble
- ✅ Fonctionne pareil partout (dev, test, production)
- ✅ Isolation : chaque app dans son propre conteneur
- ✅ Léger et rapide

### Conteneur vs Machine Virtuelle

**Machine Virtuelle (VM)** :
```
┌──────────────────────────┐
│   Application A          │
│   ├── Bibliothèques      │
│   └── OS invité (Ubuntu) │
├──────────────────────────┤
│   Hypervisor (VirtualBox)│
├──────────────────────────┤
│   OS hôte (Linux Mint)   │
└──────────────────────────┘
```

**Conteneur Docker** :
```
┌──────────────────────────┐
│   Application A          │
│   └── Bibliothèques      │
├──────────────────────────┤
│   Docker Engine          │
├──────────────────────────┤
│   OS hôte (Linux Mint)   │
└──────────────────────────┘
```

**Différences** :

| Critère | Machine Virtuelle | Conteneur Docker |
|---------|------------------|------------------|
| **Taille** | GB (giga-octets) | MB (méga-octets) |
| **Démarrage** | Minutes | Secondes |
| **Performance** | Plus lent | Quasi-natif |
| **Isolation** | Complète | Processus |
| **Usage mémoire** | Élevé | Faible |

**Quand utiliser quoi ?**
- **VM** : isolation totale, différents OS, sécurité maximale
- **Docker** : développement, microservices, déploiement rapide

---

## Installation de Docker

### Méthode recommandée

**1. Supprimer les anciennes versions** (si présentes) :

```bash
sudo apt remove docker docker-engine docker.io containerd runc
```

**2. Installer les prérequis** :

```bash
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release
```

**3. Ajouter la clé GPG officielle** :

```bash
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

**4. Ajouter le dépôt Docker** :

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**5. Installer Docker** :

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**6. Vérifier l'installation** :

```bash
sudo docker --version
```

Vous devriez voir : `Docker version 24.x.x`

**7. Tester Docker** :

```bash
sudo docker run hello-world
```

Si vous voyez "Hello from Docker!", l'installation est réussie ! 🎉

### Utiliser Docker sans sudo (recommandé)

Par défaut, Docker nécessite sudo. Pour éviter cela :

```bash
# Créer le groupe docker
sudo groupadd docker

# Ajouter votre utilisateur au groupe
sudo usermod -aG docker $USER

# Appliquer les changements (ou redémarrez la session)
newgrp docker

# Tester sans sudo
docker run hello-world
```

**⚠️ Note de sécurité** : Les membres du groupe docker ont des privilèges root. Ne le faites que sur votre machine personnelle.

---

## Concepts fondamentaux

### 1. Image Docker

Une **image** est un modèle en lecture seule contenant :
- Le système de fichiers
- L'application
- Les dépendances
- La configuration

**Analogie** : C'est comme un **moule à gâteau**. Vous ne mangez pas le moule, mais il sert à créer des gâteaux.

### 2. Conteneur Docker

Un **conteneur** est une instance en cours d'exécution d'une image.

**Analogie** : Si l'image est le moule, le **conteneur est le gâteau** que vous avez fait avec ce moule.

Vous pouvez créer plusieurs conteneurs depuis une même image.

### 3. Dockerfile

Un **Dockerfile** est un fichier texte contenant les instructions pour créer une image.

**Analogie** : C'est la **recette de cuisine** pour créer votre gâteau.

### 4. Docker Hub

**Docker Hub** est un registre public d'images Docker.

**Analogie** : C'est comme GitHub, mais pour des images Docker au lieu de code source.

URL : https://hub.docker.com

---

## Commandes Docker essentielles

### Gérer les images

**Télécharger une image** :

```bash
docker pull ubuntu
docker pull nginx
docker pull python:3.11
```

**Lister les images** :

```bash
docker images
```

**Supprimer une image** :

```bash
docker rmi nom_image
docker rmi image_id
```

**Chercher une image sur Docker Hub** :

```bash
docker search nginx
```

### Gérer les conteneurs

**Créer et lancer un conteneur** :

```bash
# Lancer un conteneur
docker run nom_image

# Exemples
docker run ubuntu
docker run -d nginx  # -d = mode détaché (arrière-plan)
```

**Lister les conteneurs** :

```bash
# Conteneurs en cours d'exécution
docker ps

# Tous les conteneurs (y compris arrêtés)
docker ps -a
```

**Arrêter un conteneur** :

```bash
docker stop id_conteneur
docker stop nom_conteneur
```

**Démarrer un conteneur arrêté** :

```bash
docker start id_conteneur
```

**Redémarrer un conteneur** :

```bash
docker restart id_conteneur
```

**Supprimer un conteneur** :

```bash
docker rm id_conteneur

# Forcer la suppression (même en cours d'exécution)
docker rm -f id_conteneur
```

**Voir les logs d'un conteneur** :

```bash
docker logs id_conteneur

# Suivre les logs en temps réel
docker logs -f id_conteneur
```

**Exécuter une commande dans un conteneur** :

```bash
# Ouvrir un shell interactif
docker exec -it id_conteneur bash

# Exécuter une commande
docker exec id_conteneur ls -la
```

### Options importantes de docker run

```bash
# Mode interactif avec terminal
docker run -it ubuntu bash

# Mode détaché (arrière-plan)
docker run -d nginx

# Nommer un conteneur
docker run --name mon-nginx nginx

# Mapper un port (host:conteneur)
docker run -p 8080:80 nginx

# Monter un volume (partager des fichiers)
docker run -v /home/user/data:/data ubuntu

# Variables d'environnement
docker run -e "DB_HOST=localhost" mon-app

# Supprimer automatiquement après l'arrêt
docker run --rm ubuntu

# Limiter la mémoire
docker run -m 512m nginx

# Combiner plusieurs options
docker run -d --name web -p 8080:80 -v ~/site:/usr/share/nginx/html nginx
```

---

## Exemples pratiques

### Exemple 1 : Serveur web Nginx

**Lancer Nginx** :

```bash
docker run -d --name mon-nginx -p 8080:80 nginx
```

**Explication** :
- `-d` : mode détaché (tourne en arrière-plan)
- `--name mon-nginx` : nomme le conteneur
- `-p 8080:80` : mappe le port 8080 de votre machine vers le port 80 du conteneur
- `nginx` : l'image à utiliser

**Tester** :

Ouvrez http://localhost:8080 dans votre navigateur.

**Voir les logs** :

```bash
docker logs -f mon-nginx
```

**Personnaliser la page** :

```bash
echo "<h1>Mon site Docker</h1>" > ~/index.html
docker run -d --name custom-nginx -p 8081:80 -v ~/index.html:/usr/share/nginx/html/index.html nginx
```

Ouvrez http://localhost:8081

**Arrêter et supprimer** :

```bash
docker stop mon-nginx
docker rm mon-nginx
```

### Exemple 2 : Base de données MySQL

**Lancer MySQL** :

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=mon_password \
  -e MYSQL_DATABASE=ma_base \
  -p 3306:3306 \
  mysql:8.0
```

**Se connecter** :

```bash
docker exec -it mysql-db mysql -u root -p
```

Entrez le mot de passe `mon_password`.

**Avec données persistantes** :

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=mon_password \
  -e MYSQL_DATABASE=ma_base \
  -p 3306:3306 \
  -v ~/mysql-data:/var/lib/mysql \
  mysql:8.0
```

Maintenant, les données survivent même si vous supprimez le conteneur !

### Exemple 3 : Application Python

**Créer un fichier app.py** :

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return '<h1>Hello from Docker!</h1>'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

**Créer un Dockerfile** :

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY app.py .

RUN pip install flask

EXPOSE 5000

CMD ["python", "app.py"]
```

**Construire l'image** :

```bash
docker build -t mon-app-python .
```

**Lancer le conteneur** :

```bash
docker run -d --name flask-app -p 5000:5000 mon-app-python
```

**Tester** : http://localhost:5000

### Exemple 4 : WordPress complet

**Lancer WordPress + MySQL** :

```bash
# Créer un réseau
docker network create wordpress-net

# MySQL
docker run -d \
  --name wordpress-db \
  --network wordpress-net \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  -e MYSQL_DATABASE=wordpress \
  -e MYSQL_USER=wpuser \
  -e MYSQL_PASSWORD=wppass \
  mysql:8.0

# WordPress
docker run -d \
  --name wordpress-site \
  --network wordpress-net \
  -p 8080:80 \
  -e WORDPRESS_DB_HOST=wordpress-db \
  -e WORDPRESS_DB_USER=wpuser \
  -e WORDPRESS_DB_PASSWORD=wppass \
  -e WORDPRESS_DB_NAME=wordpress \
  wordpress
```

**Accès** : http://localhost:8080

---

## Créer vos propres images avec Dockerfile

### Structure d'un Dockerfile

```dockerfile
# Image de base
FROM ubuntu:22.04

# Métadonnées
LABEL maintainer="votre.email@example.com"

# Variables d'environnement
ENV APP_HOME=/app

# Installer des paquets
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Définir le répertoire de travail
WORKDIR /app

# Copier des fichiers
COPY requirements.txt .
COPY app.py .

# Installer les dépendances
RUN pip3 install -r requirements.txt

# Exposer un port
EXPOSE 5000

# Commande par défaut
CMD ["python3", "app.py"]
```

### Instructions Dockerfile principales

| Instruction | Description | Exemple |
|------------|-------------|---------|
| `FROM` | Image de base | `FROM python:3.11` |
| `RUN` | Exécute une commande | `RUN apt-get update` |
| `COPY` | Copie des fichiers | `COPY app.py /app/` |
| `ADD` | Copie + décompresse | `ADD archive.tar.gz /app/` |
| `WORKDIR` | Répertoire de travail | `WORKDIR /app` |
| `ENV` | Variable d'environnement | `ENV PORT=5000` |
| `EXPOSE` | Déclare un port | `EXPOSE 8080` |
| `CMD` | Commande par défaut | `CMD ["python", "app.py"]` |
| `ENTRYPOINT` | Point d'entrée | `ENTRYPOINT ["python"]` |
| `VOLUME` | Point de montage | `VOLUME /data` |

### Construire une image

```bash
# Construire depuis le Dockerfile actuel
docker build -t mon-image .

# Spécifier un Dockerfile
docker build -t mon-image -f Dockerfile.prod .

# Avec arguments de build
docker build --build-arg VERSION=1.0 -t mon-image .
```

### Bonnes pratiques Dockerfile

**1. Utilisez des images de base officielles** :

```dockerfile
# ✅ Bon
FROM python:3.11-slim

# ❌ Éviter
FROM random-python-image
```

**2. Minimisez les layers** :

```dockerfile
# ✅ Bon (1 layer)
RUN apt-get update && apt-get install -y \
    package1 \
    package2 \
    && rm -rf /var/lib/apt/lists/*

# ❌ Mauvais (3 layers)
RUN apt-get update
RUN apt-get install -y package1
RUN apt-get install -y package2
```

**3. Ordonnez intelligemment** :

```dockerfile
# Les choses qui changent rarement en premier
FROM python:3.11
WORKDIR /app

# Dépendances (changent rarement)
COPY requirements.txt .
RUN pip install -r requirements.txt

# Code source (change souvent) en dernier
COPY . .
```

**4. Utilisez .dockerignore** :

Créez un fichier `.dockerignore` :

```
.git
.gitignore
__pycache__
*.pyc
.env
node_modules
.vscode
README.md
```

---

## Docker Compose

### Qu'est-ce que Docker Compose ?

**Docker Compose** permet de gérer plusieurs conteneurs avec un seul fichier de configuration.

**Problème sans Compose** :
```bash
docker run -d --name db ...
docker run -d --name web ...
docker run -d --name cache ...
# 10+ lignes de commandes !
```

**Avec Compose** :
```bash
docker compose up
# Une seule commande !
```

### Installation

Docker Compose est normalement inclus avec Docker moderne (plugin).

**Vérifier** :

```bash
docker compose version
```

Si absent :

```bash
sudo apt install docker-compose-plugin
```

### Fichier docker-compose.yml

Le fichier de configuration s'appelle `docker-compose.yml` (YAML).

**Exemple simple : Site WordPress** :

```yaml
version: '3.8'

services:
  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass
    volumes:
      - db_data:/var/lib/mysql

  wordpress:
    image: wordpress
    restart: always
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - wp_data:/var/www/html
    depends_on:
      - db

volumes:
  db_data:
  wp_data:
```

**Explication** :
- `services:` : liste des conteneurs
- `db:` : service MySQL
- `wordpress:` : service WordPress
- `depends_on:` : WordPress attend que db soit prêt
- `volumes:` : stockage persistant

**Lancer** :

```bash
# Dans le dossier contenant docker-compose.yml
docker compose up -d
```

**Arrêter** :

```bash
docker compose down
```

**Voir les logs** :

```bash
docker compose logs -f
```

### Exemple complet : Stack LAMP

**docker-compose.yml** :

```yaml
version: '3.8'

services:
  # Apache + PHP
  web:
    image: php:8.1-apache
    ports:
      - "8080:80"
    volumes:
      - ./src:/var/www/html
    depends_on:
      - db

  # MySQL
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: testdb
    volumes:
      - db_data:/var/lib/mysql

  # phpMyAdmin
  phpmyadmin:
    image: phpmyadmin
    ports:
      - "8081:80"
    environment:
      PMA_HOST: db
      PMA_USER: root
      PMA_PASSWORD: root
    depends_on:
      - db

volumes:
  db_data:
```

**Structure du projet** :

```
projet/
├── docker-compose.yml
└── src/
    └── index.php
```

**Créer src/index.php** :

```php
<?php
phpinfo();
?>
```

**Lancer** :

```bash
docker compose up -d
```

**Accès** :
- Site : http://localhost:8080
- phpMyAdmin : http://localhost:8081

### Commandes Docker Compose

```bash
# Démarrer les services
docker compose up

# Mode détaché
docker compose up -d

# Reconstruire les images
docker compose up --build

# Arrêter les services
docker compose stop

# Arrêter et supprimer
docker compose down

# Arrêter et supprimer TOUT (volumes inclus)
docker compose down -v

# Voir les services
docker compose ps

# Logs
docker compose logs
docker compose logs -f service_name

# Exécuter une commande
docker compose exec service_name bash

# Voir la configuration
docker compose config

# Redémarrer un service
docker compose restart service_name
```

### Exemple : Application Node.js + MongoDB + Redis

**docker-compose.yml** :

```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - MONGODB_URI=mongodb://mongo:27017/myapp
      - REDIS_URL=redis://redis:6379
    depends_on:
      - mongo
      - redis
    volumes:
      - ./:/app
      - /app/node_modules

  mongo:
    image: mongo:6
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

volumes:
  mongo_data:
```

---

## Réseaux Docker

### Types de réseaux

Docker crée automatiquement des réseaux pour permettre aux conteneurs de communiquer.

**Lister les réseaux** :

```bash
docker network ls
```

**Créer un réseau** :

```bash
docker network create mon-reseau
```

**Lancer un conteneur sur un réseau** :

```bash
docker run -d --name web --network mon-reseau nginx
```

**Connecter un conteneur existant** :

```bash
docker network connect mon-reseau conteneur_id
```

**Dans Docker Compose** :

```yaml
services:
  web:
    networks:
      - frontend
  db:
    networks:
      - backend

networks:
  frontend:
  backend:
```

---

## Volumes et persistance

### Types de stockage

**1. Volumes (recommandé)** :

```bash
# Créer un volume
docker volume create mon-volume

# Utiliser un volume
docker run -v mon-volume:/data nginx

# Lister les volumes
docker volume ls

# Inspecter un volume
docker volume inspect mon-volume

# Supprimer un volume
docker volume rm mon-volume
```

**2. Bind mounts** (lier un dossier local) :

```bash
docker run -v /home/user/data:/app/data nginx
```

**3. tmpfs mounts** (en RAM, temporaire) :

```bash
docker run --tmpfs /app/temp nginx
```

### Dans Docker Compose

```yaml
services:
  db:
    image: postgres
    volumes:
      # Volume nommé
      - db_data:/var/lib/postgresql/data
      # Bind mount
      - ./backup:/backup
      # Fichier spécifique
      - ./config.yml:/etc/app/config.yml

volumes:
  db_data:
```

---

## Nettoyage et maintenance

### Nettoyer Docker

```bash
# Supprimer les conteneurs arrêtés
docker container prune

# Supprimer les images non utilisées
docker image prune

# Supprimer les volumes non utilisés
docker volume prune

# Supprimer les réseaux non utilisés
docker network prune

# Tout nettoyer d'un coup
docker system prune

# Nettoyer VRAIMENT tout (images incluses)
docker system prune -a

# Voir l'espace utilisé
docker system df
```

---

## Dépannage

### Problèmes courants

**1. "Permission denied" sur le socket Docker**

```bash
# Solution
sudo usermod -aG docker $USER
newgrp docker
```

**2. Port déjà utilisé**

```bash
# Erreur : "port is already allocated"

# Voir ce qui utilise le port
sudo netstat -tlnp | grep :8080

# Utiliser un autre port
docker run -p 8081:80 nginx
```

**3. Conteneur s'arrête immédiatement**

```bash
# Voir pourquoi
docker logs conteneur_id

# Lancer en mode interactif pour déboguer
docker run -it image_name bash
```

**4. Problème de réseau/DNS**

```bash
# Redémarrer Docker
sudo systemctl restart docker

# Vérifier les réseaux
docker network ls
docker network inspect bridge
```

**5. Espace disque plein**

```bash
# Voir l'utilisation
docker system df

# Nettoyer
docker system prune -a
```

### Commandes de diagnostic

```bash
# Informations système
docker info

# Inspecter un conteneur
docker inspect conteneur_id

# Statistiques en temps réel
docker stats

# Processus dans un conteneur
docker top conteneur_id

# Événements Docker
docker events
```

---

## Sécurité Docker

### Bonnes pratiques

**1. Ne pas exécuter en tant que root** :

```dockerfile
# Dans votre Dockerfile
RUN useradd -m -u 1000 appuser
USER appuser
```

**2. Analyser les images** :

```bash
# Avec Docker Scout (intégré)
docker scout cves image_name

# Avec Trivy
sudo apt install trivy
trivy image nginx
```

**3. Utiliser des images officielles** :

```bash
# ✅ Bon
docker pull nginx

# ❌ Éviter
docker pull random-user/nginx
```

**4. Limiter les ressources** :

```bash
docker run -m 512m --cpus=1 nginx
```

**5. Réseaux isolés** :

Ne pas exposer tous les ports publiquement.

**6. Secrets** :

Ne jamais mettre de mots de passe en clair dans les Dockerfiles !

```bash
# Utiliser les secrets Docker
echo "mon_password" | docker secret create db_password -

# Dans compose
secrets:
  db_password:
    file: ./secrets/db_password.txt
```

---

## Cas d'usage pratiques

### Développement local

**Avantages** :
- ✅ Environnement identique pour toute l'équipe
- ✅ Installation rapide des dépendances
- ✅ Isolation des projets
- ✅ Facile à détruire et recréer

**Exemple** :

```yaml
# docker-compose.yml pour développement
version: '3.8'

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile.dev
    volumes:
      - .:/app  # Hot reload
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
```

### Tests et CI/CD

```bash
# Lancer les tests dans Docker
docker run --rm mon-app npm test

# Dans GitLab CI
script:
  - docker build -t mon-app .
  - docker run --rm mon-app npm test
```

### Microservices

Docker est idéal pour architectures microservices :

```yaml
services:
  frontend:
    build: ./frontend
  api:
    build: ./api
  auth:
    build: ./auth
  db:
    image: postgres
  cache:
    image: redis
  queue:
    image: rabbitmq
```

---

## Docker GUI (interfaces graphiques)

### Portainer

**Interface web complète pour gérer Docker**

```bash
docker volume create portainer_data

docker run -d \
  -p 9000:9000 \
  --name portainer \
  --restart always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce
```

Accès : http://localhost:9000

### Lazydocker

**Interface terminal (TUI)**

```bash
# Installation
curl https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh | bash

# Lancement
lazydocker
```

### Docker Desktop (officiel)

Alternative : Docker Desktop avec interface graphique complète
- Site : https://www.docker.com/products/docker-desktop

---

## Ressources pour apprendre

### Documentation officielle

- **Docker Docs** : https://docs.docker.com/
- **Docker Hub** : https://hub.docker.com/
- **Docker Compose** : https://docs.docker.com/compose/

### Tutoriels interactifs

- **Play with Docker** : https://labs.play-with-docker.com/
- **Docker Curriculum** : https://docker-curriculum.com/
- **Katacoda Docker** : Tutoriels interactifs

### Livres

- "Docker Deep Dive" par Nigel Poulton
- "Docker in Action" (Manning)
- "The Docker Book" par James Turnbull

### Vidéos

- **Docker Tutorial for Beginners** (TechWorld with Nana)
- **Docker Crash Course** (Traversy Media)
- Chaînes YouTube : Fireship, NetworkChuck

### Cheat sheets

- https://docs.docker.com/get-started/docker_cheatsheet.pdf
- https://github.com/wsargent/docker-cheat-sheet

---

## Aide-mémoire (Cheat Sheet)

### Commandes essentielles

```bash
# IMAGES
docker pull image                 # Télécharger
docker images                     # Lister
docker rmi image                  # Supprimer
docker build -t nom .             # Construire

# CONTENEURS
docker run image                  # Créer et lancer
docker ps                         # Lister (actifs)
docker ps -a                      # Lister (tous)
docker stop id                    # Arrêter
docker start id                   # Démarrer
docker restart id                 # Redémarrer
docker rm id                      # Supprimer
docker logs id                    # Voir logs
docker exec -it id bash           # Shell interactif

# DOCKER COMPOSE
docker compose up -d              # Lancer
docker compose down               # Arrêter
docker compose logs -f            # Logs
docker compose ps                 # Status
docker compose exec service bash  # Shell

# NETTOYAGE
docker system prune               # Nettoyer
docker system df                  # Espace utilisé

# VOLUMES
docker volume ls                  # Lister
docker volume create nom          # Créer
docker volume rm nom              # Supprimer

# RÉSEAUX
docker network ls                 # Lister
docker network create nom         # Créer
```

---

## Conclusion

Docker est devenu un outil incontournable dans le développement moderne. Voici l'essentiel à retenir :

**Pourquoi Docker ?**
- 📦 Empaquetage complet (app + dépendances)
- 🚀 Déploiement rapide et reproductible
- 🔒 Isolation des applications
- ⚡ Léger et performant

**Pour débuter** :
1. ✅ Installez Docker
2. ✅ Testez avec des images officielles (nginx, mysql, etc.)
3. ✅ Apprenez les commandes de base (`run`, `ps`, `logs`, `exec`)
4. ✅ Créez votre premier Dockerfile
5. ✅ Découvrez Docker Compose pour plusieurs conteneurs

**Commandes à retenir** :
```bash
docker run -d -p 8080:80 --name web nginx
docker compose up -d
docker ps
docker logs -f conteneur
docker exec -it conteneur bash
```

**Next steps** :
- Créez vos propres images
- Utilisez Docker Compose pour vos projets
- Explorez Docker Hub
- Apprenez les bonnes pratiques de sécurité
- Intégrez Docker dans votre workflow CI/CD

Docker peut sembler complexe au début, mais une fois les bases maîtrisées, c'est un gain de temps énorme et un outil extrêmement puissant !

**Bon voyage dans le monde des conteneurs ! 🐳**

⏭️ [Environnements virtuels Python (venv, pipenv)](/19-developpement-et-programmation/07-environnements-virtuels-python.md)
