🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 19.5 - Serveurs web locaux (Apache, Nginx)

## Introduction

### Qu'est-ce qu'un serveur web ?

Un **serveur web** est un logiciel qui reçoit des requêtes HTTP et renvoie des pages web, des fichiers, ou des données.

**Analogie simple** :
- Imaginez un restaurant :
  - Le **client** (navigateur) passe une commande
  - Le **serveur** (serveur web) prend la commande et la traite
  - Le **chef** (PHP, Python, etc.) prépare le plat si nécessaire
  - Le **serveur** apporte le plat (page HTML, JSON, etc.)

### Comment fonctionne le web ?

```
Navigateur          Serveur Web         Fichiers/Base
  (vous)             (Apache)
    │                   │                     │
    ├──── Requête ─────>│                     │
    │   GET /index.html │                     │
    │                   ├── Lit fichier ─────>│
    │                   │<───── index.html ───┤
    │<──── Réponse ─────┤                     │
    │   (HTML)          │                     │
```

### Pourquoi installer un serveur web local ?

**Pour le développement** :
- ✅ Tester vos sites web avant de les mettre en ligne
- ✅ Développer en PHP, Python, Ruby, etc.
- ✅ Simuler un environnement de production
- ✅ Apprendre le développement web

**Pour un usage personnel** :
- 🏠 Auto-héberger vos applications (Nextcloud, WordPress)
- 📁 Partager des fichiers sur votre réseau local
- 🎮 Héberger un serveur de jeu
- 📊 Héberger des outils d'administration

---

## Les deux principaux serveurs web

### Apache HTTP Server

![Le serveur web historique]

**Créé en** : 1995  
**Part de marché** : ~30% du web mondial  
**Licence** : Open Source (Apache License)  

**Avantages** :
- ✅ Très mature et stable
- ✅ Énorme documentation et communauté
- ✅ Configuration flexible (.htaccess)
- ✅ Modules pour tout faire
- ✅ Parfait pour débuter

**Inconvénients** :
- ❌ Plus gourmand en ressources
- ❌ Moins performant sur les sites à très fort trafic

**Idéal pour** : PHP, WordPress, développement web classique

### Nginx

![Le serveur web moderne et performant]

**Créé en** : 2004  
**Part de marché** : ~35% du web mondial  
**Licence** : Open Source (BSD-like)  

**Avantages** :
- ✅ Très performant et léger
- ✅ Excellent pour servir des fichiers statiques
- ✅ Gère mieux les connexions simultanées
- ✅ Faible consommation mémoire
- ✅ Souvent utilisé comme reverse proxy

**Inconvénients** :
- ❌ Configuration moins intuitive au début
- ❌ Pas de .htaccess (tout est centralisé)

**Idéal pour** : Sites à fort trafic, Node.js, reverse proxy, API

### Tableau comparatif

| Critère | Apache | Nginx |
|---------|--------|-------|
| **Facilité** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Performance** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Mémoire** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **PHP** | Excellent | Très bon |
| **Fichiers statiques** | Bon | Excellent |
| **Configuration** | Flexible | Centralisée |
| **Documentation** | Immense | Bonne |
| **Pour débuter** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |

---

## Apache : Installation et configuration

### Installation

```bash
sudo apt update  
sudo apt install apache2  
```

Apache démarre automatiquement après l'installation.

### Vérification

**Vérifier le statut** :

```bash
sudo systemctl status apache2
```

Vous devriez voir : `active (running)`

**Tester dans le navigateur** :

Ouvrez votre navigateur et allez sur :
- http://localhost
- http://127.0.0.1

Vous devriez voir la page par défaut d'Apache : **"Apache2 Ubuntu Default Page"**

### Structure des fichiers Apache

```
/etc/apache2/               # Configuration principale
├── apache2.conf           # Fichier de configuration principal
├── sites-available/       # Sites disponibles
├── sites-enabled/         # Sites actifs (liens symboliques)
├── mods-available/        # Modules disponibles
├── mods-enabled/          # Modules actifs
└── ports.conf            # Configuration des ports

/var/www/html/            # Dossier racine du site (DocumentRoot)
└── index.html           # Page par défaut

/var/log/apache2/         # Logs
├── access.log           # Journal des accès
└── error.log            # Journal des erreurs
```

### Gérer le service Apache

```bash
# Démarrer
sudo systemctl start apache2

# Arrêter
sudo systemctl stop apache2

# Redémarrer
sudo systemctl restart apache2

# Recharger la config (sans couper les connexions)
sudo systemctl reload apache2

# Activer au démarrage
sudo systemctl enable apache2

# Désactiver au démarrage
sudo systemctl disable apache2
```

### Créer votre première page web

**Méthode 1 : Modifier la page par défaut**

```bash
sudo nano /var/www/html/index.html
```

Remplacez le contenu par :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon premier site</title>
</head>
<body>
    <h1>Bienvenue sur mon serveur Apache !</h1>
    <p>Ceci est ma première page web locale.</p>
</body>
</html>
```

Enregistrez (Ctrl+O, Entrée, Ctrl+X) et rafraîchissez votre navigateur.

**Méthode 2 : Utiliser votre dossier personnel**

Par défaut, vous n'avez pas les droits d'écriture dans `/var/www/html/` sans sudo.

**Créer un dossier public** :

```bash
# Activer le module userdir
sudo a2enmod userdir

# Redémarrer Apache
sudo systemctl restart apache2

# Créer le dossier
mkdir -p ~/public_html  
echo "<h1>Mon site perso</h1>" > ~/public_html/index.html  
```

Accéder via : http://localhost/~votre_nom_utilisateur/

### Installer PHP avec Apache

PHP est très utilisé avec Apache (WordPress, etc.).

**Installation** :

```bash
sudo apt install php libapache2-mod-php php-mysql
```

**Créer un fichier de test PHP** :

```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

Accéder via : http://localhost/info.php

Vous verrez les informations PHP.

**⚠️ Sécurité** : Supprimez ce fichier après le test :

```bash
sudo rm /var/www/html/info.php
```

### Configuration avancée : Virtual Hosts

Les **Virtual Hosts** permettent d'héberger plusieurs sites sur un même serveur.

**Exemple : créer un site "monsite.local"**

**1. Créer le dossier du site** :

```bash
sudo mkdir -p /var/www/monsite
```

**2. Créer une page d'accueil** :

```bash
echo "<h1>Bienvenue sur monsite.local</h1>" | sudo tee /var/www/monsite/index.html
```

**3. Donner les bonnes permissions** :

```bash
sudo chown -R $USER:$USER /var/www/monsite
```

**4. Créer le fichier de configuration** :

```bash
sudo nano /etc/apache2/sites-available/monsite.conf
```

Contenu :

```apache
<VirtualHost *:80>
    ServerName monsite.local
    ServerAlias www.monsite.local
    DocumentRoot /var/www/monsite

    <Directory /var/www/monsite>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/monsite_error.log
    CustomLog ${APACHE_LOG_DIR}/monsite_access.log combined
</VirtualHost>
```

**5. Activer le site** :

```bash
sudo a2ensite monsite.conf  
sudo systemctl reload apache2  
```

**6. Modifier le fichier hosts** :

```bash
sudo nano /etc/hosts
```

Ajouter :

```
127.0.0.1    monsite.local
```

**7. Tester** :

Ouvrez http://monsite.local dans votre navigateur !

### Modules Apache utiles

**Voir les modules activés** :

```bash
apache2ctl -M
```

**Activer un module** :

```bash
sudo a2enmod nom_module  
sudo systemctl restart apache2  
```

**Désactiver un module** :

```bash
sudo a2dismod nom_module  
sudo systemctl restart apache2  
```

**Modules populaires** :

```bash
# Réécriture d'URL (essentiel pour WordPress, etc.)
sudo a2enmod rewrite

# SSL/HTTPS
sudo a2enmod ssl

# Compression Gzip
sudo a2enmod deflate

# En-têtes HTTP personnalisés
sudo a2enmod headers

# Proxy (pour Node.js, Python, etc.)
sudo a2enmod proxy  
sudo a2enmod proxy_http  
```

### Le fichier .htaccess

Le `.htaccess` permet de configurer Apache au niveau d'un dossier.

**Exemple : rediriger HTTP vers HTTPS**

Créez `.htaccess` dans votre dossier web :

```bash
nano /var/www/html/.htaccess
```

Contenu :

```apache
# Redirection HTTP → HTTPS
RewriteEngine On  
RewriteCond %{HTTPS} off  
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]  
```

**Exemple : URLs propres (sans .php)**

```apache
RewriteEngine On  
RewriteCond %{REQUEST_FILENAME} !-f  
RewriteCond %{REQUEST_FILENAME} !-d  
RewriteRule ^([^\.]+)$ $1.php [NC,L]  
```

Maintenant `/contact` affichera `/contact.php`.

**⚠️ Important** : Pour que .htaccess fonctionne, `AllowOverride All` doit être activé dans la configuration du VirtualHost.

---

## Nginx : Installation et configuration

### Installation

```bash
sudo apt update  
sudo apt install nginx  
```

Nginx démarre automatiquement.

### Vérification

**Vérifier le statut** :

```bash
sudo systemctl status nginx
```

**Tester dans le navigateur** :

http://localhost

Vous verrez : **"Welcome to nginx!"**

### Structure des fichiers Nginx

```
/etc/nginx/               # Configuration principale
├── nginx.conf           # Fichier de configuration principal
├── sites-available/     # Sites disponibles
├── sites-enabled/       # Sites actifs (liens symboliques)
├── conf.d/             # Configurations additionnelles
└── snippets/           # Morceaux de config réutilisables

/var/www/html/           # Dossier racine par défaut
└── index.nginx-debian.html

/var/log/nginx/          # Logs
├── access.log          # Journal des accès
└── error.log           # Journal des erreurs
```

### Gérer le service Nginx

```bash
# Démarrer
sudo systemctl start nginx

# Arrêter
sudo systemctl stop nginx

# Redémarrer
sudo systemctl restart nginx

# Recharger (sans couper les connexions)
sudo systemctl reload nginx

# Tester la configuration
sudo nginx -t

# Activer au démarrage
sudo systemctl enable nginx
```

### Créer votre première page

```bash
sudo nano /var/www/html/index.html
```

Contenu :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon serveur Nginx</title>
</head>
<body>
    <h1>Bienvenue sur Nginx !</h1>
    <p>Serveur web moderne et performant.</p>
</body>
</html>
```

Rafraîchissez http://localhost

### Installer PHP avec Nginx

Nginx ne peut pas exécuter PHP directement. Il faut **PHP-FPM** (FastCGI Process Manager).

**Installation** :

```bash
sudo apt install php-fpm php-mysql
```

**Vérifier la version PHP** :

```bash
php -v
```

Notez la version (ex: 8.1)

**Configurer Nginx pour PHP** :

Éditez la configuration par défaut :

```bash
sudo nano /etc/nginx/sites-available/default
```

Trouvez et décommentez/modifiez ces lignes :

```nginx
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    index index.php index.html index.htm;

    server_name _;

    location / {
        try_files $uri $uri/ =404;
    }

    # Configuration PHP
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        # Avec PHP 8.1 (adaptez selon votre version)
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }

    # Bloquer l'accès aux fichiers .htaccess
    location ~ /\.ht {
        deny all;
    }
}
```

**Redémarrer Nginx** :

```bash
sudo nginx -t  # Vérifier la syntaxe  
sudo systemctl restart nginx  
```

**Tester PHP** :

```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

Accédez à http://localhost/info.php

**Supprimez ensuite le fichier** :

```bash
sudo rm /var/www/html/info.php
```

### Configuration avancée : Server Blocks

Les **Server Blocks** sont l'équivalent des Virtual Hosts d'Apache.

**Créer un site "monprojet.local"**

**1. Créer le dossier** :

```bash
sudo mkdir -p /var/www/monprojet
```

**2. Créer une page** :

```bash
echo "<h1>Mon projet Nginx</h1>" | sudo tee /var/www/monprojet/index.html
```

**3. Permissions** :

```bash
sudo chown -R $USER:$USER /var/www/monprojet
```

**4. Créer la configuration** :

```bash
sudo nano /etc/nginx/sites-available/monprojet
```

Contenu :

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name monprojet.local www.monprojet.local;

    root /var/www/monprojet;
    index index.html index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    # PHP (si nécessaire)
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }

    # Logs spécifiques
    access_log /var/log/nginx/monprojet_access.log;
    error_log /var/log/nginx/monprojet_error.log;
}
```

**5. Activer le site** :

```bash
sudo ln -s /etc/nginx/sites-available/monprojet /etc/nginx/sites-enabled/  
sudo nginx -t  
sudo systemctl reload nginx  
```

**6. Modifier /etc/hosts** :

```bash
sudo nano /etc/hosts
```

Ajouter :

```
127.0.0.1    monprojet.local
```

**7. Tester** :

http://monprojet.local

### Nginx comme reverse proxy

Nginx excelle comme **reverse proxy** pour des applications Node.js, Python, Go, etc.

**Exemple : Proxifier une application Node.js sur le port 3000**

```nginx
server {
    listen 80;
    server_name monapp.local;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

Maintenant http://monapp.local affichera votre application Node.js !

---

## HTTPS avec SSL/TLS

Sécurisez votre serveur local avec HTTPS.

### Générer un certificat auto-signé

**Pour Apache** :

```bash
# Activer le module SSL
sudo a2enmod ssl

# Créer le certificat
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/apache-selfsigned.key \
  -out /etc/ssl/certs/apache-selfsigned.crt

# Remplissez les informations demandées
# Pour "Common Name", mettez "localhost" ou votre domaine local
```

**Configurer le VirtualHost SSL** :

```bash
sudo nano /etc/apache2/sites-available/default-ssl.conf
```

Modifiez :

```apache
<VirtualHost *:443>
    ServerName localhost
    DocumentRoot /var/www/html

    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
    SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
</VirtualHost>
```

**Activer** :

```bash
sudo a2ensite default-ssl  
sudo systemctl restart apache2  
```

Accédez à https://localhost (ignorez l'avertissement de sécurité du navigateur).

**Pour Nginx** :

```bash
# Créer le certificat
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/nginx-selfsigned.key \
  -out /etc/ssl/certs/nginx-selfsigned.crt
```

**Modifier la configuration** :

```bash
sudo nano /etc/nginx/sites-available/default
```

Ajouter :

```nginx
server {
    listen 443 ssl default_server;
    listen [::]:443 ssl default_server;

    ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
    ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;

    root /var/www/html;
    index index.html;

    server_name localhost;

    location / {
        try_files $uri $uri/ =404;
    }
}

# Redirection HTTP vers HTTPS
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    server_name localhost;
    return 301 https://$server_name$request_uri;
}
```

```bash
sudo nginx -t  
sudo systemctl restart nginx  
```

---

## Apache vs Nginx : Lequel choisir ?

### Choisissez Apache si :

- ✅ Vous débutez
- ✅ Vous faites du PHP/WordPress
- ✅ Vous voulez utiliser .htaccess
- ✅ Vous cherchez la solution la plus documentée
- ✅ Vous développez en local (peu de trafic)

### Choisissez Nginx si :

- ✅ Vous cherchez la performance
- ✅ Vous faites du Node.js, Python, Go
- ✅ Vous voulez un reverse proxy
- ✅ Vous avez besoin de gérer beaucoup de connexions
- ✅ Vous voulez un serveur léger

### Utiliser les deux ensemble

Vous pouvez utiliser Nginx comme reverse proxy devant Apache !

**Avantages** :
- Nginx gère les fichiers statiques (rapide)
- Apache exécute PHP (flexible)
- Meilleur des deux mondes

**Configuration** :

Apache sur le port 8080, Nginx sur le port 80 qui proxifie vers Apache.

---

## Outils utiles

### Tester la performance

**Apache Bench (ab)** :

```bash
# Installer
sudo apt install apache2-utils

# Tester 1000 requêtes, 10 simultanées
ab -n 1000 -c 10 http://localhost/
```

### Surveiller les logs en temps réel

**Apache** :

```bash
# Accès
sudo tail -f /var/log/apache2/access.log

# Erreurs
sudo tail -f /var/log/apache2/error.log
```

**Nginx** :

```bash
# Accès
sudo tail -f /var/log/nginx/access.log

# Erreurs
sudo tail -f /var/log/nginx/error.log
```

### Outils graphiques

**Webmin** : Interface web d'administration

```bash
# Installation
wget http://prdownloads.sourceforge.net/webadmin/webmin_2.105_all.deb  
sudo dpkg -i webmin_2.105_all.deb  
sudo apt install -f  
```

Accès : https://localhost:10000

---

## Applications web populaires

### WordPress

**Avec Apache** :

```bash
# Installer les dépendances
sudo apt install apache2 mysql-server php php-mysql

# Télécharger WordPress
cd /tmp  
wget https://wordpress.org/latest.tar.gz  
tar -xzf latest.tar.gz  
sudo cp -r wordpress /var/www/html/  

# Permissions
sudo chown -R www-data:www-data /var/www/html/wordpress

# Créer la base de données
sudo mysql -u root -p  
CREATE DATABASE wordpress;  
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'password';  
GRANT ALL ON wordpress.* TO 'wpuser'@'localhost';  
FLUSH PRIVILEGES;  
EXIT;  
```

Accédez à http://localhost/wordpress et suivez l'installation.

### Nextcloud

Serveur de cloud personnel (alternative à Google Drive).

```bash
# Installation via Snap (le plus simple)
sudo snap install nextcloud
```

Accès : http://localhost

### phpMyAdmin

Interface web pour MySQL.

```bash
sudo apt install phpmyadmin

# Sélectionnez Apache pendant l'installation
# Configurez avec dbconfig-common
```

Accès : http://localhost/phpmyadmin

---

## Dépannage courant

### Apache ne démarre pas

**Vérifier les erreurs** :

```bash
sudo systemctl status apache2  
sudo journalctl -xeu apache2  
```

**Port déjà utilisé** :

```bash
# Voir ce qui utilise le port 80
sudo netstat -tlnp | grep :80

# Si Nginx tourne déjà, l'arrêter
sudo systemctl stop nginx
```

**Tester la configuration** :

```bash
sudo apache2ctl configtest
```

### Nginx ne démarre pas

**Vérifier la syntaxe** :

```bash
sudo nginx -t
```

**Voir les logs** :

```bash
sudo tail -f /var/log/nginx/error.log
```

### "Permission denied" sur les fichiers

**Corriger les permissions** :

```bash
# Pour Apache
sudo chown -R www-data:www-data /var/www/html/

# Pour Nginx
sudo chown -R www-data:www-data /var/www/html/
```

### PHP ne fonctionne pas

**Apache** :

```bash
# Vérifier que le module est activé
sudo a2enmod php8.1  # Adaptez la version  
sudo systemctl restart apache2  
```

**Nginx** :

```bash
# Vérifier que PHP-FPM tourne
sudo systemctl status php8.1-fpm

# Vérifier la socket
ls -l /var/run/php/php8.1-fpm.sock
```

### 403 Forbidden

**Vérifier les permissions** :

```bash
# Le dossier doit être accessible
chmod 755 /var/www/html/

# Les fichiers doivent être lisibles
chmod 644 /var/www/html/index.html
```

**Vérifier la configuration** :

Apache : `Require all granted` doit être présent  
Nginx : Vérifier que `root` pointe vers le bon dossier  

---

## Sécurité des serveurs web

### Règles d'or

**1. Cacher la version du serveur**

**Apache** (`/etc/apache2/conf-available/security.conf`) :

```apache
ServerTokens Prod  
ServerSignature Off  
```

**Nginx** (`/etc/nginx/nginx.conf`) :

```nginx
server_tokens off;
```

**2. Limiter les uploads PHP**

```bash
sudo nano /etc/php/8.1/apache2/php.ini
```

Modifier :

```ini
upload_max_filesize = 10M  
post_max_size = 10M  
max_execution_time = 30  
```

**3. Désactiver les index de répertoires**

**Apache** :

```apache
Options -Indexes
```

**Nginx** :

```nginx
autoindex off;
```

**4. Pare-feu**

```bash
# Autoriser HTTP et HTTPS
sudo ufw allow 'Apache Full'
# ou
sudo ufw allow 'Nginx Full'

sudo ufw enable
```

**5. Sauvegardes**

```bash
# Sauvegarder les configurations
sudo cp -r /etc/apache2 ~/backup/apache2-$(date +%F)  
sudo cp -r /etc/nginx ~/backup/nginx-$(date +%F)  
```

---

## Ressources pour aller plus loin

### Documentation officielle

- **Apache** : https://httpd.apache.org/docs/
- **Nginx** : https://nginx.org/en/docs/

### Tutoriels

- **DigitalOcean Tutorials** : https://www.digitalocean.com/community/tutorials
- **Apache Tutorial** : https://httpd.apache.org/docs/2.4/tutorial/
- **Nginx Beginner's Guide** : https://nginx.org/en/docs/beginners_guide.html

### Livres

- "Apache Cookbook" (O'Reilly)
- "Nginx HTTP Server" (Packt)
- "High Performance Browser Networking" (gratuit en ligne)

### Outils en ligne

- **SSL Labs** : Tester la config SSL (https://www.ssllabs.com/ssltest/)
- **Apache Config Generator** : https://ssl-config.mozilla.org/

---

## Conclusion

Les serveurs web sont essentiels pour le développement web moderne. Voici l'essentiel à retenir :

**Pour débuter** :
- ✅ Commencez par **Apache** (plus simple et documenté)
- ✅ Apprenez les bases (installation, VirtualHosts, modules)
- ✅ Testez PHP avec Apache
- ✅ Découvrez .htaccess

**Pour la performance** :
- ⚡ Passez à **Nginx** quand vous avez besoin de performance
- ⚡ Utilisez Nginx comme reverse proxy
- ⚡ Combinez les deux pour le meilleur des deux mondes

**Configuration minimale pour développer** :
```bash
# Apache + PHP + MySQL
sudo apt install apache2 php libapache2-mod-php mysql-server

# OU Nginx + PHP + MySQL
sudo apt install nginx php-fpm php-mysql mysql-server
```

**Commandes essentielles** :
```bash
# Apache
sudo systemctl restart apache2  
sudo a2enmod rewrite  
sudo apache2ctl configtest  

# Nginx
sudo systemctl reload nginx  
sudo nginx -t  
```

Maintenant vous avez tout pour développer des sites web en local ! N'hésitez pas à expérimenter, c'est en pratiquant que vous apprendrez le mieux.

**Bon développement web ! 🌐**

⏭️ [Conteneurs Docker et Docker Compose](/19-developpement-et-programmation/06-conteneurs-docker-et-docker-compose.md)
