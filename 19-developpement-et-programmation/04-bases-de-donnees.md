🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 19.4 - Bases de données (MySQL, PostgreSQL, MongoDB)

## Introduction

### Qu'est-ce qu'une base de données ?

Une **base de données** est un système organisé pour stocker, gérer et récupérer des informations de manière efficace.

**Analogie simple** :
- Une base de données, c'est comme une **bibliothèque géante** où chaque livre (donnée) est catalogué et peut être retrouvé instantanément
- Sans base de données, ce serait comme empiler des millions de feuilles volantes dans un carton !

### Pourquoi utiliser une base de données ?

Sans base de données :
```python
# Stocker dans un fichier texte (problématique !)
utilisateurs.txt:
Jean,30,jean@email.com
Marie,25,marie@email.com
```

**Problèmes** :
- ❌ Difficile de rechercher
- ❌ Lent avec beaucoup de données
- ❌ Risque de corruption
- ❌ Pas de relations entre données
- ❌ Difficile à sécuriser

Avec une base de données :
- ✅ Recherche ultra-rapide (même sur des millions de lignes)
- ✅ Relations entre données (un utilisateur a des commandes)
- ✅ Sécurité intégrée
- ✅ Gestion des accès simultanés
- ✅ Sauvegarde et récupération

### Où sont utilisées les bases de données ?

**Partout !**
- 🌐 Sites web (comptes utilisateurs, articles, commentaires)
- 🛒 E-commerce (produits, commandes, stock)
- 💰 Banques (transactions, comptes)
- 📱 Applications mobiles (messages, contacts)
- 🎮 Jeux vidéo (scores, profils)
- 🏥 Hôpitaux (dossiers patients)

---

## Types de bases de données

Il existe deux grandes familles :

### 1. Bases de données relationnelles (SQL)

**Principe** : Les données sont organisées en **tables** reliées entre elles.

**Exemples** : MySQL, PostgreSQL, SQLite, Oracle, SQL Server

**Analogie** : comme un tableur Excel avec plusieurs feuilles reliées

**Structure** :
```
Table "utilisateurs"
+----+--------+-----+------------------+
| id | nom    | age | email            |
+----+--------+-----+------------------+
| 1  | Jean   | 30  | jean@email.com   |
| 2  | Marie  | 25  | marie@email.com  |
+----+--------+-----+------------------+

Table "commandes"
+----+--------------+---------+
| id | utilisateur  | montant |
+----+--------------+---------+
| 1  | 1            | 49.99   |
| 2  | 1            | 89.00   |
| 3  | 2            | 29.50   |
+----+--------------+---------+
```

**Langage** : SQL (Structured Query Language)

**Avantages** :
- ✅ Structure claire et organisée
- ✅ Relations entre données
- ✅ Intégrité des données garantie
- ✅ Très mature et fiable

**Inconvénients** :
- ❌ Moins flexible (schéma rigide)
- ❌ Peut être complexe à scaler horizontalement

### 2. Bases de données NoSQL (Not Only SQL)

**Principe** : Stockage flexible, souvent sous forme de documents JSON.

**Exemples** : MongoDB, Redis, Cassandra, CouchDB

**Structure (exemple MongoDB)** :
```json
{
  "_id": 1,
  "nom": "Jean",
  "age": 30,
  "email": "jean@email.com",
  "commandes": [
    {"montant": 49.99, "date": "2024-01-15"},
    {"montant": 89.00, "date": "2024-02-20"}
  ]
}
```

**Avantages** :
- ✅ Très flexible (pas de schéma fixe)
- ✅ Facile à scaler horizontalement
- ✅ Rapide pour certains cas d'usage
- ✅ Proche du format utilisé en JavaScript/Python

**Inconvénients** :
- ❌ Moins de garanties d'intégrité
- ❌ Requêtes complexes plus difficiles

---

## MySQL

![La base de données la plus populaire au monde]

### Qu'est-ce que MySQL ?

**MySQL** est un système de gestion de base de données relationnelle (SGBD) :
- **Gratuit et Open Source** (version Community)
- **Très populaire** : utilisé par Facebook, YouTube, Twitter
- **Facile à apprendre** pour débuter
- **Compatible** avec pratiquement tous les langages de programmation

### Installation de MySQL

**Via le gestionnaire de paquets** :

```bash
sudo apt update
sudo apt install mysql-server
```

**Vérification** :

```bash
sudo systemctl status mysql
```

Vous devriez voir : `active (running)`

### Sécuriser l'installation

**Important** : MySQL s'installe par défaut sans mot de passe root. Il faut le sécuriser !

```bash
sudo mysql_secure_installation
```

Répondez aux questions :
1. **Set root password?** → Oui (choisissez un mot de passe fort)
2. **Remove anonymous users?** → Oui
3. **Disallow root login remotely?** → Oui (pour plus de sécurité)
4. **Remove test database?** → Oui
5. **Reload privilege tables?** → Oui

### Se connecter à MySQL

**En tant que root** :

```bash
sudo mysql -u root -p
```

Entrez le mot de passe défini précédemment.

Vous verrez :
```
mysql>
```

### Commandes MySQL de base

**Créer une base de données** :

```sql
CREATE DATABASE ma_base;
```

**Lister les bases de données** :

```sql
SHOW DATABASES;
```

**Utiliser une base de données** :

```sql
USE ma_base;
```

**Créer une table** :

```sql
CREATE TABLE utilisateurs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(100),
    email VARCHAR(100),
    age INT
);
```

**Insérer des données** :

```sql
INSERT INTO utilisateurs (nom, email, age)
VALUES ('Jean Dupont', 'jean@email.com', 30);
```

**Lire des données** :

```sql
-- Tout sélectionner
SELECT * FROM utilisateurs;

-- Sélection conditionnelle
SELECT * FROM utilisateurs WHERE age > 25;
```

**Modifier des données** :

```sql
UPDATE utilisateurs
SET age = 31
WHERE nom = 'Jean Dupont';
```

**Supprimer des données** :

```sql
DELETE FROM utilisateurs WHERE id = 1;
```

**Quitter MySQL** :

```sql
EXIT;
```

### Créer un utilisateur MySQL

**Ne pas utiliser root pour vos applications !**

```sql
-- Se connecter en tant que root
sudo mysql -u root -p

-- Créer un utilisateur
CREATE USER 'mon_utilisateur'@'localhost' IDENTIFIED BY 'mot_de_passe_fort';

-- Donner tous les droits sur une base
GRANT ALL PRIVILEGES ON ma_base.* TO 'mon_utilisateur'@'localhost';

-- Appliquer les changements
FLUSH PRIVILEGES;

-- Quitter
EXIT;
```

### Outil graphique : phpMyAdmin

**Installation** :

```bash
sudo apt install phpmyadmin
```

Pendant l'installation :
- Sélectionnez **apache2** (avec la barre d'espace)
- Configurez avec **dbconfig-common** : Oui
- Définissez un mot de passe

**Accès** : http://localhost/phpmyadmin

**Alternative moderne : Adminer**

Plus léger que phpMyAdmin :

```bash
# Télécharger
sudo mkdir -p /usr/share/adminer
sudo wget "https://www.adminer.org/latest.php" -O /usr/share/adminer/adminer.php

# Créer un alias Apache (si installé)
echo "Alias /adminer /usr/share/adminer/adminer.php" | sudo tee /etc/apache2/conf-available/adminer.conf
sudo a2enconf adminer
sudo systemctl reload apache2
```

**Accès** : http://localhost/adminer

---

## PostgreSQL

![La base de données la plus avancée]

### Qu'est-ce que PostgreSQL ?

**PostgreSQL** (aussi appelé "Postgres") est un SGBD relationnel très puissant :
- **Gratuit et Open Source**
- **Très conforme aux standards SQL**
- **Fonctionnalités avancées** : JSON, géospatial, full-text search
- **Fiable et robuste** : utilisé par Instagram, Spotify, Apple

### PostgreSQL vs MySQL

| Critère | PostgreSQL | MySQL |
|---------|-----------|-------|
| **Popularité** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Standards SQL** | Très strict | Moins strict |
| **Fonctionnalités** | Très riche | Standard |
| **Performance lecture** | Très bon | Excellent |
| **Performance écriture** | Excellent | Très bon |
| **Complexité** | Plus complexe | Plus simple |

**Pour débuter** : MySQL est plus simple
**Pour des projets avancés** : PostgreSQL est plus puissant

### Installation de PostgreSQL

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
```

**Vérification** :

```bash
sudo systemctl status postgresql
```

### Premier démarrage

Par défaut, PostgreSQL crée un utilisateur système `postgres`.

**Se connecter** :

```bash
sudo -u postgres psql
```

Vous verrez :
```
postgres=#
```

### Commandes PostgreSQL de base

**Créer une base de données** :

```sql
CREATE DATABASE ma_base;
```

**Lister les bases** :

```sql
\l
```

**Se connecter à une base** :

```sql
\c ma_base
```

**Créer une table** :

```sql
CREATE TABLE utilisateurs (
    id SERIAL PRIMARY KEY,
    nom VARCHAR(100),
    email VARCHAR(100),
    age INTEGER
);
```

**Insérer des données** :

```sql
INSERT INTO utilisateurs (nom, email, age)
VALUES ('Marie Martin', 'marie@email.com', 25);
```

**Lire des données** :

```sql
SELECT * FROM utilisateurs;
```

**Lister les tables** :

```sql
\dt
```

**Voir la structure d'une table** :

```sql
\d utilisateurs
```

**Quitter PostgreSQL** :

```sql
\q
```

### Créer un utilisateur PostgreSQL

```bash
# Se connecter en tant que postgres
sudo -u postgres psql

# Créer un utilisateur
CREATE USER mon_utilisateur WITH PASSWORD 'mot_de_passe_fort';

# Créer une base et donner les droits
CREATE DATABASE ma_base OWNER mon_utilisateur;

# Donner tous les droits
GRANT ALL PRIVILEGES ON DATABASE ma_base TO mon_utilisateur;

# Quitter
\q
```

**Se connecter avec ce nouvel utilisateur** :

```bash
psql -U mon_utilisateur -d ma_base -h localhost
```

### Outil graphique : pgAdmin

**Installation** :

```bash
# Ajouter le dépôt
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg

sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list'

sudo apt update
sudo apt install pgadmin4-desktop
```

**Lancer** : Cherchez "pgAdmin 4" dans le menu Applications

**Alternative : DBeaver**

Un outil universel qui fonctionne avec MySQL, PostgreSQL, MongoDB et bien d'autres.

```bash
# Via Flatpak
flatpak install flathub io.dbeaver.DBeaverCommunity
```

---

## MongoDB

![La base NoSQL la plus populaire]

### Qu'est-ce que MongoDB ?

**MongoDB** est une base de données NoSQL orientée documents :
- **Stockage JSON/BSON** : format flexible
- **Pas de schéma fixe** : liberté de structure
- **Scalable** : facile à distribuer
- **Populaire** : utilisé par Uber, eBay, LinkedIn

### Quand utiliser MongoDB ?

**MongoDB est idéal pour** :
- Applications avec données très variées
- Prototypage rapide (schéma flexible)
- Big Data et analytics
- Applications temps réel
- Stockage de logs

**Préférez MySQL/PostgreSQL pour** :
- Transactions bancaires/financières
- Données fortement structurées
- Relations complexes entre tables
- Besoin de conformité stricte

### Installation de MongoDB

**Méthode recommandée : via le dépôt officiel**

```bash
# Importer la clé publique
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor

# Ajouter le dépôt
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

# Installer
sudo apt update
sudo apt install -y mongodb-org
```

**Démarrer MongoDB** :

```bash
sudo systemctl start mongod
sudo systemctl enable mongod
```

**Vérification** :

```bash
sudo systemctl status mongod
```

### Se connecter à MongoDB

**Shell MongoDB** :

```bash
mongosh
```

Vous verrez :
```
test>
```

### Commandes MongoDB de base

**Concepts MongoDB** :
- **Base de données** : contient des collections
- **Collection** : équivalent d'une table (mais flexible)
- **Document** : équivalent d'une ligne (format JSON)

**Créer/Utiliser une base** :

```javascript
use ma_base
```

**Insérer un document** :

```javascript
db.utilisateurs.insertOne({
    nom: "Jean Dupont",
    email: "jean@email.com",
    age: 30,
    hobbies: ["lecture", "sport"]
})
```

**Insérer plusieurs documents** :

```javascript
db.utilisateurs.insertMany([
    { nom: "Marie Martin", email: "marie@email.com", age: 25 },
    { nom: "Paul Bernard", email: "paul@email.com", age: 35 }
])
```

**Lire des documents** :

```javascript
// Tous les documents
db.utilisateurs.find()

// Avec condition
db.utilisateurs.find({ age: { $gt: 25 } })

// Joli affichage
db.utilisateurs.find().pretty()
```

**Mettre à jour** :

```javascript
// Mettre à jour un document
db.utilisateurs.updateOne(
    { nom: "Jean Dupont" },
    { $set: { age: 31 } }
)

// Mettre à jour plusieurs
db.utilisateurs.updateMany(
    { age: { $lt: 30 } },
    { $set: { categorie: "jeune" } }
)
```

**Supprimer** :

```javascript
// Supprimer un document
db.utilisateurs.deleteOne({ nom: "Paul Bernard" })

// Supprimer plusieurs
db.utilisateurs.deleteMany({ age: { $lt: 20 } })
```

**Lister les collections** :

```javascript
show collections
```

**Lister les bases** :

```javascript
show dbs
```

**Quitter** :

```javascript
exit
```

### Outil graphique : MongoDB Compass

**Télécharger depuis** : https://www.mongodb.com/try/download/compass

```bash
# Installer le .deb téléchargé
sudo dpkg -i mongodb-compass_*_amd64.deb
sudo apt install -f
```

**Lancer** : Cherchez "MongoDB Compass" dans le menu

**Connexion** : mongodb://localhost:27017

---

## Comparaison détaillée

| Critère | MySQL | PostgreSQL | MongoDB |
|---------|-------|------------|---------|
| **Type** | SQL (relationnel) | SQL (relationnel) | NoSQL (documents) |
| **Licence** | GPL/Commercial | PostgreSQL (libre) | SSPL/Commercial |
| **Facilité** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Performance** | Excellent (lecture) | Excellent (équilibré) | Très bon (scalable) |
| **Standards SQL** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | N/A |
| **Flexibilité** | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Transactions** | Oui | Oui (avancé) | Oui (depuis v4) |
| **JSON** | Basique | Excellent | Natif |
| **Communauté** | Immense | Très grande | Grande |
| **Cas d'usage** | Web, général | Complexe, analytics | Big Data, temps réel |

---

## Quel système choisir ?

### Vous débutez ?
➡️ **MySQL** - Le plus simple et le plus documenté

### Vous voulez apprendre le SQL sérieusement ?
➡️ **PostgreSQL** - Le plus conforme aux standards

### Votre application a des données très variables ?
➡️ **MongoDB** - Flexibilité maximale

### Vous faites du web classique ?
➡️ **MySQL** - Le plus répandu avec PHP/WordPress

### Vous faites de l'analyse de données ?
➡️ **PostgreSQL** - Fonctionnalités analytiques avancées

### Vous construisez une API moderne ?
➡️ **MongoDB** - S'intègre parfaitement avec Node.js/JavaScript

---

## Sécurité des bases de données

### Règles d'or

**1. Ne jamais utiliser root en production**

Créez toujours des utilisateurs dédiés avec droits limités.

**2. Mots de passe forts**

```bash
# Générer un mot de passe fort
openssl rand -base64 32
```

**3. Accès restreint**

Par défaut, n'autoriser que localhost :

```bash
# MySQL : /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 127.0.0.1

# PostgreSQL : /etc/postgresql/*/main/postgresql.conf
listen_addresses = 'localhost'
```

**4. Pare-feu**

Si vous devez ouvrir l'accès distant :

```bash
# MySQL (port 3306)
sudo ufw allow from 192.168.1.0/24 to any port 3306

# PostgreSQL (port 5432)
sudo ufw allow from 192.168.1.0/24 to any port 5432

# MongoDB (port 27017)
sudo ufw allow from 192.168.1.0/24 to any port 27017
```

**5. Sauvegardes régulières**

**MySQL** :

```bash
# Sauvegarder
mysqldump -u root -p ma_base > sauvegarde.sql

# Restaurer
mysql -u root -p ma_base < sauvegarde.sql
```

**PostgreSQL** :

```bash
# Sauvegarder
pg_dump ma_base > sauvegarde.sql

# Restaurer
psql ma_base < sauvegarde.sql
```

**MongoDB** :

```bash
# Sauvegarder
mongodump --db ma_base --out /chemin/sauvegarde/

# Restaurer
mongorestore --db ma_base /chemin/sauvegarde/ma_base/
```

**6. Mises à jour de sécurité**

```bash
sudo apt update
sudo apt upgrade mysql-server postgresql mongodb-org
```

---

## Connexion depuis un langage de programmation

### Python

**MySQL** :

```python
import mysql.connector

# Connexion
conn = mysql.connector.connect(
    host="localhost",
    user="mon_utilisateur",
    password="mot_de_passe",
    database="ma_base"
)

cursor = conn.cursor()

# Requête
cursor.execute("SELECT * FROM utilisateurs")
resultats = cursor.fetchall()

for row in resultats:
    print(row)

conn.close()
```

Installation : `pip install mysql-connector-python`

**PostgreSQL** :

```python
import psycopg2

# Connexion
conn = psycopg2.connect(
    host="localhost",
    database="ma_base",
    user="mon_utilisateur",
    password="mot_de_passe"
)

cursor = conn.cursor()
cursor.execute("SELECT * FROM utilisateurs")
resultats = cursor.fetchall()

for row in resultats:
    print(row)

conn.close()
```

Installation : `pip install psycopg2-binary`

**MongoDB** :

```python
from pymongo import MongoClient

# Connexion
client = MongoClient('mongodb://localhost:27017/')
db = client['ma_base']
collection = db['utilisateurs']

# Requête
for doc in collection.find():
    print(doc)
```

Installation : `pip install pymongo`

### JavaScript (Node.js)

**MySQL** :

```javascript
const mysql = require('mysql2');

const connection = mysql.createConnection({
    host: 'localhost',
    user: 'mon_utilisateur',
    password: 'mot_de_passe',
    database: 'ma_base'
});

connection.query('SELECT * FROM utilisateurs', (err, results) => {
    if (err) throw err;
    console.log(results);
});
```

Installation : `npm install mysql2`

**PostgreSQL** :

```javascript
const { Client } = require('pg');

const client = new Client({
    host: 'localhost',
    user: 'mon_utilisateur',
    password: 'mot_de_passe',
    database: 'ma_base'
});

await client.connect();
const res = await client.query('SELECT * FROM utilisateurs');
console.log(res.rows);
await client.end();
```

Installation : `npm install pg`

**MongoDB** :

```javascript
const { MongoClient } = require('mongodb');

const client = new MongoClient('mongodb://localhost:27017');

async function run() {
    await client.connect();
    const db = client.db('ma_base');
    const collection = db.collection('utilisateurs');

    const docs = await collection.find({}).toArray();
    console.log(docs);
}

run();
```

Installation : `npm install mongodb`

### PHP

**MySQL** :

```php
<?php
$conn = new mysqli("localhost", "mon_utilisateur", "mot_de_passe", "ma_base");

if ($conn->connect_error) {
    die("Connexion échouée: " . $conn->connect_error);
}

$result = $conn->query("SELECT * FROM utilisateurs");

while($row = $result->fetch_assoc()) {
    echo $row["nom"] . "<br>";
}

$conn->close();
?>
```

**PostgreSQL** :

```php
<?php
$conn = pg_connect("host=localhost dbname=ma_base user=mon_utilisateur password=mot_de_passe");

$result = pg_query($conn, "SELECT * FROM utilisateurs");

while ($row = pg_fetch_assoc($result)) {
    echo $row['nom'] . "<br>";
}

pg_close($conn);
?>
```

---

## ORM : simplifier l'accès aux bases de données

Un **ORM** (Object-Relational Mapping) vous permet d'interagir avec la base sans écrire de SQL.

### Avantages

- ✅ Code plus lisible
- ✅ Protection contre les injections SQL
- ✅ Indépendant du SGBD (facile de changer)
- ✅ Gestion automatique des migrations

### ORM populaires

**Python** :
- **SQLAlchemy** : le plus complet
- **Django ORM** : intégré à Django
- **Peewee** : simple et léger

**JavaScript** :
- **Sequelize** : pour SQL
- **Mongoose** : pour MongoDB
- **Prisma** : moderne et typé

**PHP** :
- **Eloquent** : intégré à Laravel
- **Doctrine** : très complet

---

## Dépannage courant

### MySQL : "Access denied for user 'root'@'localhost'"

**Solution 1** : Réinitialiser le mot de passe

```bash
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'nouveau_mot_de_passe';
FLUSH PRIVILEGES;
EXIT;
```

**Solution 2** : Utiliser sudo

```bash
sudo mysql -u root
```

### PostgreSQL : "FATAL: Peer authentication failed"

**Solution** : Modifier `/etc/postgresql/*/main/pg_hba.conf`

Changer :
```
local   all   all   peer
```

En :
```
local   all   all   md5
```

Puis redémarrer :
```bash
sudo systemctl restart postgresql
```

### MongoDB : "Failed to connect to 127.0.0.1:27017"

**Solution** :

```bash
# Vérifier que MongoDB tourne
sudo systemctl status mongod

# Démarrer si arrêté
sudo systemctl start mongod
```

### Espace disque plein

Les bases de données peuvent grossir rapidement !

**Vérifier l'espace** :

```bash
df -h
```

**Nettoyer les logs MySQL** :

```bash
sudo mysql
PURGE BINARY LOGS BEFORE DATE(NOW());
EXIT;
```

---

## Bonnes pratiques

### 1. Nommage cohérent

- Tables/Collections : **pluriel** (`utilisateurs`, `commandes`)
- Colonnes : **snake_case** (`date_creation`, `nom_complet`)
- Identifiants : toujours **id** comme clé primaire

### 2. Index pour les performances

Créez des index sur les colonnes fréquemment recherchées :

**MySQL/PostgreSQL** :
```sql
CREATE INDEX idx_email ON utilisateurs(email);
```

**MongoDB** :
```javascript
db.utilisateurs.createIndex({ email: 1 })
```

### 3. Normalisation (SQL)

Évitez la redondance en séparant les données :

**❌ Mauvais** :
```
utilisateurs: id, nom, adresse_rue, adresse_ville, adresse_cp
```

**✅ Bon** :
```
utilisateurs: id, nom, adresse_id
adresses: id, rue, ville, code_postal
```

### 4. Validation des données

Validez TOUJOURS côté application ET côté base :

```sql
CREATE TABLE utilisateurs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(100) NOT NULL UNIQUE,
    age INT CHECK (age >= 0 AND age <= 150)
);
```

### 5. Utilisez des transactions

Pour des opérations critiques (transferts bancaires, etc.) :

```sql
START TRANSACTION;
UPDATE comptes SET solde = solde - 100 WHERE id = 1;
UPDATE comptes SET solde = solde + 100 WHERE id = 2;
COMMIT;
```

---

## Ressources pour apprendre

### SQL en général

- **SQLBolt** : https://sqlbolt.com (interactif, excellent !)
- **W3Schools SQL** : https://www.w3schools.com/sql/
- **Mode Analytics SQL Tutorial** : https://mode.com/sql-tutorial/

### MySQL

- Documentation officielle : https://dev.mysql.com/doc/
- MySQL Tutorial : https://www.mysqltutorial.org/

### PostgreSQL

- Documentation officielle : https://www.postgresql.org/docs/
- PostgreSQL Tutorial : https://www.postgresqltutorial.com/

### MongoDB

- MongoDB University : https://university.mongodb.com/ (gratuit !)
- Documentation : https://docs.mongodb.com/

### Livres

- "Learning SQL" par Alan Beaulieu
- "High Performance MySQL" (avancé)
- "PostgreSQL: Up and Running" (pratique)
- "MongoDB: The Definitive Guide"

---

## Conclusion

Les bases de données sont au cœur de presque toutes les applications modernes. Voici ce qu'il faut retenir :

**Pour débuter** :
- ✅ Commencez par **MySQL** (le plus simple et documenté)
- ✅ Apprenez les bases du **SQL** (CREATE, SELECT, INSERT, UPDATE, DELETE)
- ✅ Utilisez un outil graphique au début (phpMyAdmin, Adminer)
- ✅ Passez progressivement au terminal

**Choix du SGBD** :
- **MySQL** → Applications web classiques, WordPress, général
- **PostgreSQL** → Applications complexes, analytics, conformité stricte
- **MongoDB** → APIs modernes, données flexibles, prototypage rapide

**Sécurité** :
- 🔒 Mots de passe forts
- 🔒 Utilisateurs dédiés (jamais root en production)
- 🔒 Sauvegardes régulières
- 🔒 Pare-feu correctement configuré

N'oubliez pas : la meilleure base de données est celle que vous maîtrisez et qui répond à vos besoins spécifiques !

**Bon développement avec les bases de données ! 🗄️**

⏭️ [Serveurs web locaux (Apache, Nginx)](/19-developpement-et-programmation/05-serveurs-web-locaux.md)
