🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 21.2 Serveur web (Apache/Nginx)

## Introduction

### Qu'est-ce qu'un serveur web ?

Un serveur web est un logiciel qui permet de partager des pages web, des sites internet ou des applications web. Quand vous visitez un site comme google.com ou youtube.com, c'est un serveur web qui vous envoie les pages que vous voyez dans votre navigateur.

**En termes simples :** Un serveur web écoute les demandes sur Internet (ou votre réseau local) et répond en envoyant des fichiers HTML, CSS, JavaScript, images, etc.

### Pourquoi installer un serveur web sur Linux Mint ?

Vous pourriez vouloir installer un serveur web pour :
- **Développement web** : Tester vos sites avant de les mettre en ligne
- **Hébergement local** : Héberger un site personnel ou un blog
- **Applications web** : Installer WordPress, Nextcloud, ou d'autres applications
- **Serveur de fichiers** : Partager des fichiers via une interface web
- **Apprentissage** : Comprendre comment fonctionnent les sites web

### Apache vs Nginx : Lequel choisir ?

Il existe deux serveurs web majeurs sous Linux :

#### Apache HTTP Server
- **Le plus ancien et populaire** (depuis 1995)
- Très flexible et riche en fonctionnalités
- Configuration plus simple pour les débutants
- Utilise des fichiers `.htaccess` pour la configuration
- Idéal pour : Sites personnels, WordPress, développement

#### Nginx (prononcé "engine-x")
- **Plus moderne et rapide** (depuis 2004)
- Excellent pour servir du contenu statique
- Consomme moins de ressources
- Configuration centralisée
- Idéal pour : Sites à fort trafic, serveur de fichiers, proxy

**Pour débuter :** Apache est généralement plus simple à configurer. Nginx est préféré pour les performances en production.

---

## Installation et configuration d'Apache

### Installation

Ouvrez un terminal et installez Apache :

```bash
sudo apt update
sudo apt install apache2
```

Apache s'installe et démarre automatiquement.

### Vérifier que Apache fonctionne

Ouvrez votre navigateur web et tapez dans la barre d'adresse :

```
http://localhost
```

ou

```
http://127.0.0.1
```

Vous devriez voir la page par défaut d'Apache avec le message "Apache2 Ubuntu Default Page". Félicitations, votre serveur web fonctionne !

### Structure des dossiers Apache

Voici les emplacements importants :

```
/var/www/html/          → Dossier racine de vos sites web
/etc/apache2/           → Configuration d'Apache
/etc/apache2/apache2.conf → Fichier de configuration principal
/etc/apache2/sites-available/ → Sites disponibles
/etc/apache2/sites-enabled/   → Sites activés
/var/log/apache2/       → Fichiers de logs (erreurs et accès)
```

### Créer votre première page web

Supprimez ou renommez la page par défaut :

```bash
sudo mv /var/www/html/index.html /var/www/html/index.html.old
```

Créez votre propre page :

```bash
sudo nano /var/www/html/index.html
```

Ajoutez ce contenu :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon premier serveur web</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 50px auto;
            padding: 20px;
            background-color: #f0f0f0;
        }
        h1 {
            color: #333;
        }
    </style>
</head>
<body>
    <h1>Bienvenue sur mon serveur web !</h1>
    <p>Ce serveur tourne sur Linux Mint avec Apache.</p>
    <p>Date et heure : <script>document.write(new Date().toLocaleString());</script></p>
</body>
</html>
```

Sauvegardez avec `Ctrl+O`, puis quittez avec `Ctrl+X`.

Rechargez `http://localhost` dans votre navigateur. Vous devriez voir votre page personnalisée !

### Gérer le service Apache

#### Démarrer Apache
```bash
sudo systemctl start apache2
```

#### Arrêter Apache
```bash
sudo systemctl stop apache2
```

#### Redémarrer Apache
```bash
sudo systemctl restart apache2
```

#### Recharger la configuration (sans interruption)
```bash
sudo systemctl reload apache2
```

#### Vérifier l'état
```bash
sudo systemctl status apache2
```

#### Activer au démarrage
```bash
sudo systemctl enable apache2
```

### Créer un site virtuel (Virtual Host)

Les Virtual Hosts permettent d'héberger plusieurs sites sur un même serveur.

#### Créer la structure du site

```bash
sudo mkdir -p /var/www/monsite
sudo chown -R $USER:$USER /var/www/monsite
```

Créez une page d'accueil :

```bash
nano /var/www/monsite/index.html
```

Ajoutez :

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mon Site</title>
</head>
<body>
    <h1>Bienvenue sur mon site personnel</h1>
</body>
</html>
```

#### Créer le fichier de configuration

```bash
sudo nano /etc/apache2/sites-available/monsite.conf
```

Ajoutez cette configuration :

```apache
<VirtualHost *:80>
    ServerName monsite.local
    ServerAdmin admin@monsite.local
    DocumentRoot /var/www/monsite

    <Directory /var/www/monsite>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/monsite-error.log
    CustomLog ${APACHE_LOG_DIR}/monsite-access.log combined
</VirtualHost>
```

**Explications :**
- `ServerName` : Nom de domaine du site
- `DocumentRoot` : Dossier contenant les fichiers du site
- `ErrorLog` et `CustomLog` : Fichiers de journalisation

#### Activer le site

```bash
sudo a2ensite monsite.conf
sudo systemctl reload apache2
```

#### Configurer /etc/hosts (pour test local)

Pour accéder à votre site via `monsite.local` :

```bash
sudo nano /etc/hosts
```

Ajoutez :

```
127.0.0.1    monsite.local
```

Maintenant, ouvrez `http://monsite.local` dans votre navigateur !

### Modules Apache utiles

Apache utilise des modules pour ajouter des fonctionnalités.

#### Activer le module de réécriture d'URL (rewrite)

Utile pour WordPress et les URLs propres :

```bash
sudo a2enmod rewrite
sudo systemctl restart apache2
```

#### Activer SSL (HTTPS)

```bash
sudo a2enmod ssl
sudo systemctl restart apache2
```

#### Lister les modules activés

```bash
apache2ctl -M
```

#### Désactiver un module

```bash
sudo a2dismod nom_du_module
sudo systemctl restart apache2
```

---

## Installation et configuration de Nginx

### Installation

```bash
sudo apt update
sudo apt install nginx
```

Nginx démarre automatiquement après l'installation.

### Vérifier que Nginx fonctionne

**Important :** Si Apache est déjà installé et actif, arrêtez-le d'abord :

```bash
sudo systemctl stop apache2
```

Ouvrez votre navigateur et allez sur :

```
http://localhost
```

Vous devriez voir la page "Welcome to nginx!"

### Structure des dossiers Nginx

```
/var/www/html/          → Dossier racine par défaut
/etc/nginx/             → Configuration de Nginx
/etc/nginx/nginx.conf   → Fichier de configuration principal
/etc/nginx/sites-available/ → Sites disponibles
/etc/nginx/sites-enabled/   → Sites activés
/var/log/nginx/         → Fichiers de logs
```

### Gérer le service Nginx

Les commandes sont similaires à Apache :

```bash
sudo systemctl start nginx      # Démarrer
sudo systemctl stop nginx       # Arrêter
sudo systemctl restart nginx    # Redémarrer
sudo systemctl reload nginx     # Recharger la config
sudo systemctl status nginx     # Vérifier l'état
sudo systemctl enable nginx     # Activer au démarrage
```

### Créer votre première page

```bash
sudo nano /var/www/html/index.html
```

Ajoutez :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon serveur Nginx</title>
</head>
<body>
    <h1>Serveur web Nginx opérationnel !</h1>
    <p>Linux Mint + Nginx = Performance</p>
</body>
</html>
```

Rechargez la page dans votre navigateur.

### Créer un bloc serveur (équivalent Virtual Host)

#### Créer la structure

```bash
sudo mkdir -p /var/www/monsite-nginx
sudo chown -R $USER:$USER /var/www/monsite-nginx
```

Créez une page :

```bash
nano /var/www/monsite-nginx/index.html
```

#### Créer la configuration

```bash
sudo nano /etc/nginx/sites-available/monsite-nginx
```

Ajoutez :

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name monsite-nginx.local;
    root /var/www/monsite-nginx;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    access_log /var/log/nginx/monsite-nginx-access.log;
    error_log /var/log/nginx/monsite-nginx-error.log;
}
```

**Explications :**
- `listen 80` : Écoute sur le port 80 (HTTP)
- `server_name` : Nom de domaine
- `root` : Dossier racine du site
- `try_files` : Essaie de servir le fichier demandé

#### Activer le site

Créez un lien symbolique :

```bash
sudo ln -s /etc/nginx/sites-available/monsite-nginx /etc/nginx/sites-enabled/
```

Testez la configuration :

```bash
sudo nginx -t
```

Si tout est OK, rechargez Nginx :

```bash
sudo systemctl reload nginx
```

#### Configurer /etc/hosts

```bash
sudo nano /etc/hosts
```

Ajoutez :

```
127.0.0.1    monsite-nginx.local
```

Accédez à `http://monsite-nginx.local` !

---

## PHP avec Apache ou Nginx

Pour exécuter des applications PHP (comme WordPress), vous devez installer PHP.

### Installer PHP

```bash
sudo apt install php libapache2-mod-php php-mysql
```

Pour Nginx, installez aussi PHP-FPM :

```bash
sudo apt install php-fpm
```

### Tester PHP avec Apache

Créez un fichier de test :

```bash
sudo nano /var/www/html/info.php
```

Ajoutez :

```php
<?php
phpinfo();
?>
```

Allez sur `http://localhost/info.php`. Vous devriez voir les informations de PHP.

**Important :** Supprimez ce fichier après le test pour des raisons de sécurité :

```bash
sudo rm /var/www/html/info.php
```

### Configurer PHP avec Nginx

Modifiez votre bloc serveur Nginx :

```bash
sudo nano /etc/nginx/sites-available/monsite-nginx
```

Ajoutez le support PHP :

```nginx
server {
    listen 80;
    server_name monsite-nginx.local;
    root /var/www/monsite-nginx;
    index index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # Configuration PHP
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }

    # Bloquer l'accès aux fichiers .htaccess
    location ~ /\.ht {
        deny all;
    }
}
```

**Note :** Vérifiez la version de PHP installée (`php -v`) et ajustez le chemin du socket si nécessaire.

Rechargez Nginx :

```bash
sudo systemctl reload nginx
```

---

## Sécuriser votre serveur web

### Configurer le pare-feu

Autorisez HTTP (port 80) et HTTPS (port 443) :

```bash
sudo ufw allow 'Apache Full'
```

ou pour Nginx :

```bash
sudo ufw allow 'Nginx Full'
```

Si vous n'utilisez que HTTP :

```bash
sudo ufw allow 'Apache'  # ou 'Nginx HTTP'
```

### Installer un certificat SSL (HTTPS)

Pour activer HTTPS avec un certificat gratuit Let's Encrypt :

#### Installer Certbot

```bash
sudo apt install certbot
```

Pour Apache :
```bash
sudo apt install python3-certbot-apache
```

Pour Nginx :
```bash
sudo apt install python3-certbot-nginx
```

#### Obtenir un certificat

**Important :** Votre serveur doit être accessible depuis Internet avec un nom de domaine valide.

Pour Apache :
```bash
sudo certbot --apache -d mondomaine.com -d www.mondomaine.com
```

Pour Nginx :
```bash
sudo certbot --nginx -d mondomaine.com -d www.mondomaine.com
```

Suivez les instructions. Certbot configurera automatiquement HTTPS !

#### Renouvellement automatique

Certbot configure un renouvellement automatique. Testez-le :

```bash
sudo certbot renew --dry-run
```

### Masquer la version du serveur

#### Apache

Éditez la configuration :

```bash
sudo nano /etc/apache2/conf-available/security.conf
```

Changez :

```apache
ServerTokens Prod
ServerSignature Off
```

Redémarrez :

```bash
sudo systemctl restart apache2
```

#### Nginx

Éditez :

```bash
sudo nano /etc/nginx/nginx.conf
```

Ajoutez dans le bloc `http` :

```nginx
server_tokens off;
```

Rechargez :

```bash
sudo systemctl reload nginx
```

### Protéger les dossiers avec mot de passe

#### Apache

Installez les outils nécessaires :

```bash
sudo apt install apache2-utils
```

Créez un fichier de mots de passe :

```bash
sudo htpasswd -c /etc/apache2/.htpasswd utilisateur
```

Entrez le mot de passe quand demandé.

Dans votre Virtual Host :

```apache
<Directory /var/www/monsite/admin>
    AuthType Basic
    AuthName "Zone protégée"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
```

#### Nginx

Créez le fichier de mots de passe (installez apache2-utils d'abord) :

```bash
sudo htpasswd -c /etc/nginx/.htpasswd utilisateur
```

Dans votre bloc serveur :

```nginx
location /admin {
    auth_basic "Zone protégée";
    auth_basic_user_file /etc/nginx/.htpasswd;
}
```

---

## Applications web populaires

### Installer WordPress

WordPress est le système de gestion de contenu (CMS) le plus populaire.

#### Prérequis

```bash
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql
sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip
```

#### Créer la base de données

```bash
sudo mysql -u root -p
```

Dans MySQL :

```sql
CREATE DATABASE wordpress;
CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'motdepasse_securise';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

#### Télécharger WordPress

```bash
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
sudo mv wordpress /var/www/
sudo chown -R www-data:www-data /var/www/wordpress
```

#### Configurer Apache pour WordPress

```bash
sudo nano /etc/apache2/sites-available/wordpress.conf
```

Ajoutez :

```apache
<VirtualHost *:80>
    ServerName monblog.local
    DocumentRoot /var/www/wordpress

    <Directory /var/www/wordpress>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/wordpress-error.log
    CustomLog ${APACHE_LOG_DIR}/wordpress-access.log combined
</VirtualHost>
```

Activez le site :

```bash
sudo a2ensite wordpress.conf
sudo a2enmod rewrite
sudo systemctl reload apache2
```

Ajoutez dans `/etc/hosts` :

```
127.0.0.1    monblog.local
```

Visitez `http://monblog.local` et suivez l'installation de WordPress !

### Installer phpMyAdmin (gestionnaire MySQL)

```bash
sudo apt install phpmyadmin
```

Lors de l'installation :
- Sélectionnez Apache (avec la barre d'espace, puis Entrée)
- Choisissez "Oui" pour configurer la base de données
- Entrez un mot de passe pour phpMyAdmin

Créez un lien symbolique :

```bash
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
```

Accédez à `http://localhost/phpmyadmin`

**Sécurité :** Renommez ce dossier ou protégez-le par mot de passe !

---

## Surveillance et logs

### Consulter les logs Apache

#### Logs d'accès (qui visite votre site)

```bash
sudo tail -f /var/log/apache2/access.log
```

#### Logs d'erreurs

```bash
sudo tail -f /var/log/apache2/error.log
```

### Consulter les logs Nginx

```bash
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

### Analyser les logs

Pour avoir des statistiques, installez GoAccess :

```bash
sudo apt install goaccess
```

Analysez les logs en temps réel :

```bash
sudo goaccess /var/log/apache2/access.log --log-format=COMBINED
```

ou pour Nginx :

```bash
sudo goaccess /var/log/nginx/access.log --log-format=COMBINED
```

---

## Optimisation des performances

### Apache

#### Activer la compression

```bash
sudo a2enmod deflate
sudo systemctl restart apache2
```

#### Mettre en cache les fichiers statiques

```bash
sudo a2enmod expires
sudo a2enmod headers
```

Ajoutez dans votre Virtual Host :

```apache
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresByType image/jpg "access plus 1 year"
    ExpiresByType image/jpeg "access plus 1 year"
    ExpiresByType image/gif "access plus 1 year"
    ExpiresByType image/png "access plus 1 year"
    ExpiresByType text/css "access plus 1 month"
    ExpiresByType application/javascript "access plus 1 month"
</IfModule>
```

### Nginx

Nginx est déjà optimisé par défaut, mais vous pouvez :

#### Activer la compression Gzip

Dans `/etc/nginx/nginx.conf`, vérifiez que ces lignes sont présentes :

```nginx
gzip on;
gzip_vary on;
gzip_proxied any;
gzip_comp_level 6;
gzip_types text/plain text/css text/xml text/javascript application/javascript application/xml+rss;
```

#### Augmenter les connexions simultanées

```nginx
events {
    worker_connections 2048;
}
```

---

## Dépannage courant

### Apache ne démarre pas

Vérifiez la configuration :

```bash
sudo apache2ctl configtest
```

Si vous voyez "Syntax OK", le problème est ailleurs. Vérifiez les logs :

```bash
sudo journalctl -u apache2 -n 50
```

### Port 80 déjà utilisé

Vérifiez quel processus utilise le port :

```bash
sudo lsof -i :80
```

ou

```bash
sudo netstat -tulpn | grep :80
```

Si c'est Apache et Nginx qui se battent, arrêtez l'un des deux !

### "403 Forbidden"

Vérifiez les permissions :

```bash
sudo chown -R www-data:www-data /var/www/monsite
sudo chmod -R 755 /var/www/monsite
```

### "502 Bad Gateway" (Nginx avec PHP)

PHP-FPM n'est probablement pas démarré :

```bash
sudo systemctl start php8.1-fpm
sudo systemctl enable php8.1-fpm
```

### Site inaccessible après modification

Vérifiez la syntaxe :

Apache :
```bash
sudo apache2ctl configtest
```

Nginx :
```bash
sudo nginx -t
```

### Trouver l'IP de votre serveur

```bash
hostname -I
```

ou

```bash
ip addr show
```

---

## Accès depuis le réseau local

Pour que d'autres appareils sur votre réseau puissent accéder à votre serveur :

1. Trouvez votre IP locale :
```bash
hostname -I
```

2. Sur un autre appareil du réseau, utilisez cette IP dans le navigateur :
```
http://192.168.1.XXX
```

3. Configurez le pare-feu si nécessaire :
```bash
sudo ufw allow from 192.168.1.0/24 to any port 80
```

---

## Choisir entre Apache et Nginx

### Utilisez Apache si :
- Vous débutez avec les serveurs web
- Vous avez besoin de fichiers `.htaccess`
- Vous installez WordPress ou des CMS similaires
- Vous préférez la simplicité de configuration

### Utilisez Nginx si :
- Vous cherchez les meilleures performances
- Vous servez beaucoup de contenu statique (images, vidéos)
- Vous avez un site à fort trafic
- Vous voulez consommer moins de ressources

### Utiliser les deux ensemble ?

Oui ! Nginx peut servir de "reverse proxy" devant Apache :
- Nginx gère les fichiers statiques (rapide)
- Apache gère PHP et le contenu dynamique
- Configuration avancée, réservée aux utilisateurs expérimentés

---

## Commandes de référence rapide

### Apache
```bash
sudo systemctl start apache2        # Démarrer
sudo systemctl stop apache2         # Arrêter
sudo systemctl restart apache2      # Redémarrer
sudo systemctl reload apache2       # Recharger config
sudo apache2ctl configtest          # Tester config
sudo a2ensite monsite.conf          # Activer site
sudo a2dissite monsite.conf         # Désactiver site
sudo a2enmod rewrite                # Activer module
sudo a2dismod rewrite               # Désactiver module
```

### Nginx
```bash
sudo systemctl start nginx          # Démarrer
sudo systemctl stop nginx           # Arrêter
sudo systemctl restart nginx        # Redémarrer
sudo systemctl reload nginx         # Recharger config
sudo nginx -t                       # Tester config
sudo ln -s /etc/nginx/sites-available/site /etc/nginx/sites-enabled/  # Activer site
sudo rm /etc/nginx/sites-enabled/site  # Désactiver site
```

---

## Ressources supplémentaires

### Documentation officielle
- Apache : [httpd.apache.org](https://httpd.apache.org/docs/)
- Nginx : [nginx.org/en/docs/](http://nginx.org/en/docs/)

### Communautés
- Forums Linux Mint
- Stack Overflow
- Reddit : r/apache, r/nginx

### Tutoriels recommandés
- DigitalOcean Community Tutorials
- Linode Guides
- Documentation Ubuntu Server

---

## Conclusion

Vous avez maintenant les bases pour installer et configurer un serveur web sur Linux Mint !

**Points clés à retenir :**
1. Apache est plus simple pour débuter
2. Nginx est plus performant pour la production
3. Les deux peuvent être sécurisés avec SSL/TLS
4. Les logs sont vos amis pour le dépannage
5. N'exposez jamais un serveur non sécurisé à Internet

**Prochaines étapes :**
- Installez une vraie application (WordPress, Nextcloud)
- Configurez HTTPS avec Let's Encrypt
- Apprenez à optimiser les performances
- Explorez les modules et extensions

N'oubliez pas : un serveur web est une porte ouverte sur votre système. Sécurisez-le toujours correctement, surtout si vous l'exposez à Internet !

⏭️ [Serveur de fichiers (Samba, FTP)](/21-serveurs-et-administration-systeme/03-serveur-de-fichiers.md)
