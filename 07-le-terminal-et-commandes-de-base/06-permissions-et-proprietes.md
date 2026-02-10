🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.6 - Permissions et propriétés (chmod, chown, ls -l)

## Introduction

Les permissions sont l'un des concepts fondamentaux de la sécurité sous Linux. Elles déterminent **qui peut faire quoi** avec vos fichiers et dossiers. Comprendre les permissions vous permettra de :

- Protéger vos fichiers personnels
- Rendre des scripts exécutables
- Partager des fichiers en toute sécurité
- Résoudre des problèmes de droits d'accès
- Comprendre les messages d'erreur "Permission denied"

**Analogie :** Imaginez vos fichiers comme des pièces d'une maison :
- Certaines pièces sont privées (votre chambre) → Vous seul pouvez y entrer
- D'autres sont partagées (salon) → Votre famille peut y accéder
- D'autres sont publiques (entrée) → Tout le monde peut voir

Les permissions Linux fonctionnent exactement de cette manière, mais avec un contrôle beaucoup plus fin !

---

## Propriété des fichiers : Qui possède quoi ?

Sous Linux, chaque fichier et dossier appartient à :
1. Un **propriétaire** (utilisateur)
2. Un **groupe** (ensemble d'utilisateurs)

### Voir le propriétaire et le groupe

Utilisez la commande `ls -l` (list en format long) :

```bash
ls -l
```

**Exemple de résultat :**
```
-rw-r--r-- 1 utilisateur users  2048 nov. 15 10:30 document.txt
drwxr-xr-x 2 utilisateur users  4096 nov. 14 15:45 Projets
```

**Décomposition :**
```
-rw-r--r-- 1 utilisateur users  2048 nov. 15 10:30 document.txt
│          │ │           │      │    │             │
│          │ │           │      │    │             └─ Nom du fichier
│          │ │           │      │    └─ Date de modification
│          │ │           │      └─ Taille (octets)
│          │ │           └─ Groupe propriétaire
│          │ └─ Propriétaire (utilisateur)
│          └─ Nombre de liens
└─ Permissions
```

### Les trois acteurs

Pour chaque fichier, Linux distingue trois catégories d'utilisateurs :

1. **Propriétaire (Owner/User)** : La personne qui a créé le fichier
2. **Groupe (Group)** : Un ensemble d'utilisateurs défini
3. **Autres (Others)** : Tous les autres utilisateurs du système

**Exemple concret :**
- Vous créez un fichier → Vous êtes le propriétaire
- Votre groupe "famille" peut y accéder → Groupe
- Les autres utilisateurs du PC → Autres

---

## Les types de permissions

Il existe trois types de permissions de base :

### 1. Lecture (Read - r)

**Symbole :** `r`

**Pour un fichier :**
- Permet de **lire** le contenu du fichier
- Exemples : voir le texte avec `cat`, copier le fichier

**Pour un dossier :**
- Permet de **lister** le contenu du dossier
- Exemple : utiliser `ls` pour voir les fichiers qu'il contient

### 2. Écriture (Write - w)

**Symbole :** `w`

**Pour un fichier :**
- Permet de **modifier** le contenu du fichier
- Exemples : éditer, supprimer, renommer

**Pour un dossier :**
- Permet de **créer, supprimer, renommer** des fichiers dans le dossier
- Même si vous ne pouvez pas modifier les fichiers individuels !

### 3. Exécution (Execute - x)

**Symbole :** `x`

**Pour un fichier :**
- Permet d'**exécuter** le fichier comme un programme
- Exemples : scripts bash, programmes compilés

**Pour un dossier :**
- Permet d'**entrer** dans le dossier (avec `cd`)
- Nécessaire pour accéder aux fichiers qu'il contient

---

## Lire les permissions avec `ls -l`

### Format des permissions

Les permissions s'affichent sur 10 caractères :

```
-rw-r--r--
│└┬┘└┬┘└┬┘
│ │  │  └─ Permissions pour les AUTRES
│ │  └─ Permissions pour le GROUPE
│ └─ Permissions pour le PROPRIÉTAIRE
└─ Type de fichier
```

### Le premier caractère : Type de fichier

| Symbole | Type |
|---------|------|
| `-` | Fichier ordinaire |
| `d` | Dossier (directory) |
| `l` | Lien symbolique (link) |
| `c` | Fichier de caractères |
| `b` | Fichier de bloc |

**Les plus courants sont `-` et `d`.**

### Les neuf caractères suivants : Permissions

Divisés en **trois groupes de trois** :

```
rw-  r--  r--
└┬┘  └┬┘  └┬┘
 │    │    └─ Autres : lecture seulement
 │    └─ Groupe : lecture seulement
 └─ Propriétaire : lecture et écriture
```

**Chaque groupe de trois suit le même schéma : rwx**
- Position 1 : `r` (lecture) ou `-` (pas de lecture)
- Position 2 : `w` (écriture) ou `-` (pas d'écriture)
- Position 3 : `x` (exécution) ou `-` (pas d'exécution)

### Exemples de lecture

#### Exemple 1 : `-rw-r--r--`

```
-rw-r--r--
│└┬┘└┬┘└┬┘
│ │  │  └─ r-- : Autres peuvent lire
│ │  └─ r-- : Groupe peut lire
│ └─ rw- : Propriétaire peut lire et écrire
└─ - : Fichier ordinaire
```

**Interprétation :**
- C'est un **fichier**
- Le propriétaire peut le **lire et modifier**
- Le groupe peut seulement le **lire**
- Les autres peuvent seulement le **lire**

#### Exemple 2 : `drwxr-xr-x`

```
drwxr-xr-x
│└┬┘└┬┘└┬┘
│ │  │  └─ r-x : Autres peuvent lire et entrer
│ │  └─ r-x : Groupe peut lire et entrer
│ └─ rwx : Propriétaire peut tout faire
└─ d : Dossier
```

**Interprétation :**
- C'est un **dossier**
- Le propriétaire peut **lister, créer, modifier, entrer**
- Le groupe peut **lister et entrer**
- Les autres peuvent **lister et entrer**

#### Exemple 3 : `-rwx------`

```
-rwx------
│└┬┘└┬┘└┬┘
│ │  │  └─ --- : Autres ne peuvent rien faire
│ │  └─ --- : Groupe ne peut rien faire
│ └─ rwx : Propriétaire peut tout faire
└─ - : Fichier
```

**Interprétation :**
- Fichier **privé**, accessible seulement par le propriétaire
- Le propriétaire peut le lire, modifier et exécuter
- Personne d'autre ne peut y toucher

#### Exemple 4 : `-rw-rw-rw-`

```
-rw-rw-rw-
│└┬┘└┬┘└┬┘
│ │  │  └─ rw- : Autres peuvent lire et écrire
│ │  └─ rw- : Groupe peut lire et écrire
│ └─ rw- : Propriétaire peut lire et écrire
└─ - : Fichier
```

**Interprétation :**
- Fichier **public** en lecture et écriture
- Tout le monde peut le lire et le modifier
- **Attention :** Très peu sécurisé !

---

## La commande `chmod` : Modifier les permissions

### Signification

**chmod** signifie **Change Mode** (Changer le mode, c'est-à-dire les permissions).

### Syntaxe de base

```bash
chmod permissions fichier
```

Il existe deux façons de spécifier les permissions :
1. **Notation symbolique** (plus intuitive pour les débutants)
2. **Notation octale** (plus compacte, utilisée par les experts)

---

## Notation symbolique (méthode recommandée pour débuter)

### Structure

```bash
chmod [qui][opération][permissions] fichier
```

**Les composants :**

#### Qui ? (optionnel)

| Symbole | Signification |
|---------|---------------|
| `u` | User (propriétaire) |
| `g` | Group (groupe) |
| `o` | Others (autres) |
| `a` | All (tous : u+g+o) |

#### Opération

| Symbole | Action |
|---------|--------|
| `+` | Ajouter la permission |
| `-` | Retirer la permission |
| `=` | Définir exactement ces permissions |

#### Permissions

| Symbole | Signification |
|---------|---------------|
| `r` | Read (lecture) |
| `w` | Write (écriture) |
| `x` | Execute (exécution) |

### Exemples pratiques avec notation symbolique

#### Ajouter la permission d'exécution au propriétaire

```bash
chmod u+x script.sh
```

**Résultat :**
- Avant : `-rw-r--r--`
- Après : `-rwxr--r--`

**Utilisation courante :** Rendre un script exécutable.

#### Retirer la permission d'écriture au groupe

```bash
chmod g-w document.txt
```

#### Ajouter la lecture à tout le monde

```bash
chmod a+r fichier.txt
```

Ou simplement :
```bash
chmod +r fichier.txt
```

(Sans préciser "qui", cela s'applique à tous par défaut)

#### Donner toutes les permissions au propriétaire

```bash
chmod u+rwx fichier
```

#### Retirer toutes les permissions aux autres

```bash
chmod o-rwx fichier_prive.txt
```

#### Définir exactement les permissions

```bash
chmod u=rw,g=r,o=r fichier.txt
```

**Résultat :** `-rw-r--r--`

**Explication :**
- Propriétaire : exactement lecture + écriture
- Groupe : exactement lecture
- Autres : exactement lecture

#### Combiner plusieurs opérations

```bash
chmod u+x,g+x,o-rwx script.sh
```

Ajoute l'exécution au propriétaire et au groupe, retire tout aux autres.

### Modifier les permissions d'un dossier

#### Pour le dossier lui-même

```bash
chmod u+w Projets
```

#### Pour le dossier et tout son contenu (récursif)

```bash
chmod -R u+w Projets
```

L'option `-R` (récursif) applique les modifications au dossier et à tous les fichiers/sous-dossiers qu'il contient.

**⚠️ Attention :** Utilisez `-R` avec précaution, car cela affecte tous les fichiers !

---

## Notation octale (méthode avancée)

### Principe

Chaque groupe de permissions (rwx) est représenté par un chiffre de 0 à 7.

### Calcul des valeurs

Chaque permission a une valeur :
- **r** (lecture) = **4**
- **w** (écriture) = **2**
- **x** (exécution) = **1**

On **additionne** ces valeurs pour obtenir le chiffre :

| Permissions | Calcul | Valeur |
|-------------|--------|--------|
| `---` | 0 + 0 + 0 | **0** |
| `--x` | 0 + 0 + 1 | **1** |
| `-w-` | 0 + 2 + 0 | **2** |
| `-wx` | 0 + 2 + 1 | **3** |
| `r--` | 4 + 0 + 0 | **4** |
| `r-x` | 4 + 0 + 1 | **5** |
| `rw-` | 4 + 2 + 0 | **6** |
| `rwx` | 4 + 2 + 1 | **7** |

### Utilisation

On utilise **trois chiffres** :
1. Premier chiffre : Permissions du propriétaire
2. Deuxième chiffre : Permissions du groupe
3. Troisième chiffre : Permissions des autres

```bash
chmod 755 fichier
      └┬┘
       │
       └─ 7: propriétaire (rwx)
         5: groupe (r-x)
         5: autres (r-x)
```

### Exemples avec notation octale

#### 644 : Permissions standards pour un fichier

```bash
chmod 644 document.txt
```

**Équivalent à :** `-rw-r--r--`
- Propriétaire : 6 = rw-
- Groupe : 4 = r--
- Autres : 4 = r--

**Usage :** Fichiers de documents, images, etc.

#### 755 : Permissions standards pour un exécutable

```bash
chmod 755 script.sh
```

**Équivalent à :** `-rwxr-xr-x`
- Propriétaire : 7 = rwx
- Groupe : 5 = r-x
- Autres : 5 = r-x

**Usage :** Scripts, programmes exécutables.

#### 700 : Fichier privé

```bash
chmod 700 fichier_secret.txt
```

**Équivalent à :** `-rwx------`
- Propriétaire : 7 = rwx
- Groupe : 0 = ---
- Autres : 0 = ---

**Usage :** Fichiers personnels sensibles.

#### 777 : Tous les droits à tout le monde (DANGEREUX !)

```bash
chmod 777 fichier
```

**Équivalent à :** `-rwxrwxrwx`

**⚠️ À ÉVITER :** Extrêmement peu sécurisé ! N'importe qui peut faire n'importe quoi avec le fichier.

#### 600 : Lecture/écriture pour le propriétaire seulement

```bash
chmod 600 fichier_prive.txt
```

**Équivalent à :** `-rw-------`

**Usage :** Fichiers de configuration personnels, clés SSH.

### Permissions courantes pour les dossiers

#### 755 : Dossier standard

```bash
chmod 755 MonDossier
```

**Équivalent à :** `drwxr-xr-x`

Tout le monde peut lister et entrer, seul le propriétaire peut modifier.

#### 700 : Dossier privé

```bash
chmod 700 DossierPrive
```

**Équivalent à :** `drwx------`

Seul le propriétaire peut accéder au dossier.

---

## Tableau de conversion rapide

| Octal | Binaire | Symbolique | Description |
|-------|---------|------------|-------------|
| **0** | 000 | `---` | Aucun droit |
| **1** | 001 | `--x` | Exécution seulement |
| **2** | 010 | `-w-` | Écriture seulement |
| **3** | 011 | `-wx` | Écriture + exécution |
| **4** | 100 | `r--` | Lecture seulement |
| **5** | 101 | `r-x` | Lecture + exécution |
| **6** | 110 | `rw-` | Lecture + écriture |
| **7** | 111 | `rwx` | Tous les droits |

---

## La commande `chown` : Changer le propriétaire

### Signification

**chown** signifie **Change Owner** (Changer le propriétaire).

### Syntaxe de base

```bash
chown nouvel_utilisateur fichier
```

**⚠️ Important :** Cette commande nécessite généralement les privilèges `sudo`.

### Exemples

#### Changer le propriétaire d'un fichier

```bash
sudo chown alice document.txt
```

Le fichier appartient maintenant à l'utilisateur "alice".

#### Changer le propriétaire et le groupe

```bash
sudo chown alice:users document.txt
```

- Propriétaire : alice
- Groupe : users

#### Changer récursivement

```bash
sudo chown -R alice:users Projets/
```

Change le propriétaire de tout le dossier Projets et son contenu.

### Vérifier le changement

```bash
ls -l document.txt
```

---

## La commande `chgrp` : Changer le groupe

### Signification

**chgrp** signifie **Change Group** (Changer le groupe).

### Syntaxe

```bash
chgrp nouveau_groupe fichier
```

### Exemples

#### Changer le groupe d'un fichier

```bash
chgrp developers script.sh
```

#### Changer récursivement

```bash
chgrp -R developers Projet/
```

---

## Cas d'usage pratiques

### Cas 1 : Rendre un script exécutable

Vous venez de créer un script `backup.sh` et voulez l'exécuter.

```bash
chmod +x backup.sh
```

Maintenant vous pouvez faire :
```bash
./backup.sh
```

### Cas 2 : Protéger un fichier sensible

Vous avez un fichier avec des mots de passe.

```bash
chmod 600 passwords.txt
```

Vous seul pouvez le lire et le modifier.

### Cas 3 : Partager un dossier avec votre groupe

Vous travaillez en équipe sur un projet.

```bash
chmod 775 ProjetEquipe/
```

- Vous : lecture, écriture, exécution (7)
- Votre groupe : lecture, écriture, exécution (7)
- Autres : lecture et exécution (5)

### Cas 4 : Fichier public en lecture seule

Vous voulez partager un document, mais personne ne doit le modifier.

```bash
chmod 644 document_public.pdf
```

Tout le monde peut le lire, vous seul pouvez le modifier.

### Cas 5 : Réparer les permissions d'un dossier web

Les serveurs web nécessitent souvent des permissions spécifiques.

```bash
sudo chown -R www-data:www-data /var/www/monsite  
sudo chmod -R 755 /var/www/monsite  
```

### Cas 6 : Clés SSH

Les clés SSH doivent être strictement privées.

```bash
chmod 600 ~/.ssh/id_rsa  
chmod 644 ~/.ssh/id_rsa.pub  
chmod 700 ~/.ssh  
```

---

## Permissions spéciales (notions avancées)

Au-delà des permissions de base, il existe des permissions spéciales :

### SUID (Set User ID)

**Symbole :** `s` à la place du `x` du propriétaire

```bash
-rwsr-xr-x
```

**Effet :** Le fichier s'exécute avec les droits de son propriétaire, pas de l'utilisateur qui le lance.

**Exemple :** La commande `passwd` permet de modifier le fichier `/etc/shadow` (réservé à root).

### SGID (Set Group ID)

**Symbole :** `s` à la place du `x` du groupe

```bash
-rwxr-sr-x
```

**Effet :** Pour un dossier, les fichiers créés dedans héritent du groupe du dossier.

### Sticky Bit

**Symbole :** `t` à la place du `x` des autres

```bash
drwxrwxrwt
```

**Effet :** Dans un dossier avec sticky bit, seul le propriétaire d'un fichier peut le supprimer.

**Exemple :** `/tmp` utilise le sticky bit.

**Configuration :**
```bash
chmod +s fichier    # SUID/SGID  
chmod +t dossier    # Sticky bit  
```

**Note :** Ces permissions sont avancées. En tant que débutant, vous n'aurez probablement pas besoin de les utiliser souvent.

---

## Commandes utiles complémentaires

### `stat` : Informations détaillées

```bash
stat fichier.txt
```

Affiche toutes les informations sur le fichier, y compris les permissions en octal.

### `namei` : Vérifier les permissions d'un chemin

```bash
namei -l /chemin/vers/fichier
```

Affiche les permissions de chaque dossier dans le chemin.

### `umask` : Permissions par défaut

```bash
umask
```

Affiche le masque de permissions par défaut pour les nouveaux fichiers.

**Modifier le umask :**
```bash
umask 022
```

Les nouveaux fichiers auront les permissions `644`, les dossiers `755`.

---

## Erreurs courantes et solutions

### Erreur 1 : Permission denied

**Problème :**
```bash
./script.sh
bash: ./script.sh: Permission denied
```

**Cause :** Le fichier n'est pas exécutable.

**Solution :**
```bash
chmod +x script.sh
```

### Erreur 2 : Cannot access file

**Problème :**
```bash
cat document.txt  
cat: document.txt: Permission denied  
```

**Cause :** Vous n'avez pas la permission de lecture.

**Solution :**
Si c'est votre fichier :
```bash
chmod u+r document.txt
```

Sinon, demandez au propriétaire de modifier les permissions ou utilisez `sudo`.

### Erreur 3 : Operation not permitted (chown)

**Problème :**
```bash
chown alice fichier.txt  
chown: changing ownership of 'fichier.txt': Operation not permitted  
```

**Cause :** Seul root peut changer le propriétaire.

**Solution :**
```bash
sudo chown alice fichier.txt
```

### Erreur 4 : Cannot remove directory

**Problème :**
```bash
rm -r Dossier  
rm: cannot remove 'Dossier': Permission denied  
```

**Cause :** Vous n'avez pas les droits d'écriture sur le dossier parent.

**Solution :**
Vérifiez les permissions du dossier parent :
```bash
ls -ld .
```

Ajoutez les permissions si nécessaire :
```bash
chmod u+w .
```

### Erreur 5 : Permissions trop permissives

**Problème :** SSH refuse une clé privée.
```
Permissions 0644 for 'id_rsa' are too open.
```

**Cause :** La clé privée doit être accessible seulement par vous.

**Solution :**
```bash
chmod 600 ~/.ssh/id_rsa
```

---

## Bonnes pratiques

### 1. Principe du moindre privilège

Donnez **le minimum de permissions nécessaires**, pas plus.

**Mauvais :**
```bash
chmod 777 fichier    # Trop permissif !
```

**Bon :**
```bash
chmod 644 fichier    # Juste ce qu'il faut
```

### 2. Protégez vos fichiers sensibles

```bash
chmod 600 ~/.ssh/id_rsa  
chmod 600 ~/.gnupg/*  
chmod 600 ~/.netrc  
```

### 3. Scripts exécutables

Pour vos scripts :
```bash
chmod 755 script.sh    # Vous pouvez tout faire, les autres peuvent exécuter
```

Ou plus restrictif :
```bash
chmod 700 script.sh    # Vous seul pouvez l'exécuter
```

### 4. Dossiers partagés

Pour un dossier de travail en équipe :
```bash
chmod 770 ProjetEquipe    # Vous et votre groupe  
chgrp equipe ProjetEquipe  
```

### 5. Vérifiez avant de modifier récursivement

```bash
ls -lR Dossier/        # Voir les permissions actuelles  
chmod -R 755 Dossier/  # Puis modifier  
```

### 6. Ne jamais 777 !

**Évitez à tout prix :**
```bash
chmod 777 fichier    # TRÈS DANGEREUX
```

C'est presque toujours une mauvaise idée. Il existe toujours une meilleure solution.

---

## Aide-mémoire rapide

### Permissions courantes (octal)

| Code | Fichier | Dossier | Usage |
|------|---------|---------|-------|
| **644** | `-rw-r--r--` | - | Fichier standard (documents, images) |
| **755** | `-rwxr-xr-x` | `drwxr-xr-x` | Exécutable / Dossier standard |
| **600** | `-rw-------` | - | Fichier privé (mots de passe, clés) |
| **700** | `-rwx------` | `drwx------` | Script privé / Dossier privé |
| **775** | `-rwxrwxr-x` | `drwxrwxr-x` | Partagé avec le groupe |

### Commandes essentielles

```bash
# Voir les permissions
ls -l fichier  
ls -ld dossier  

# Modifier les permissions (symbolique)
chmod u+x fichier          # Ajouter exécution au propriétaire  
chmod g-w fichier          # Retirer écriture au groupe  
chmod a+r fichier          # Ajouter lecture à tous  

# Modifier les permissions (octal)
chmod 644 fichier          # rw-r--r--  
chmod 755 script           # rwxr-xr-x  
chmod 600 fichier_prive    # rw-------  

# Récursif
chmod -R 755 dossier

# Changer le propriétaire
sudo chown utilisateur fichier  
sudo chown utilisateur:groupe fichier  
sudo chown -R utilisateur dossier  

# Changer le groupe
sudo chgrp groupe fichier  
sudo chgrp -R groupe dossier  

# Informations détaillées
stat fichier
```

---

## Exercices de lecture (pour s'entraîner)

### Interpréter ces permissions

1. `-rw-rw-r--`
   - Fichier
   - Propriétaire : lecture + écriture
   - Groupe : lecture + écriture
   - Autres : lecture

2. `drwx------`
   - Dossier
   - Propriétaire : tout (lecture, écriture, exécution/entrée)
   - Groupe : rien
   - Autres : rien

3. `-rwxr-xr-x`
   - Fichier
   - Propriétaire : tout
   - Groupe : lecture + exécution
   - Autres : lecture + exécution

4. `drwxrwxrwx`
   - Dossier
   - Tout le monde peut tout faire (très peu sécurisé !)

---

## Résumé

### Concepts clés

**Propriété :**
- Chaque fichier a un propriétaire et un groupe
- `ls -l` pour voir
- `chown` pour changer le propriétaire
- `chgrp` pour changer le groupe

**Les trois permissions :**
- **r** (read) : Lire
- **w** (write) : Écrire/Modifier
- **x** (execute) : Exécuter (fichier) ou Entrer (dossier)

**Les trois catégories :**
- **u** (user) : Propriétaire
- **g** (group) : Groupe
- **o** (others) : Autres

**Modifier les permissions :**
- Notation symbolique : `chmod u+x fichier`
- Notation octale : `chmod 755 fichier`

### Commandes à retenir absolument

```bash
ls -l                      # Voir les permissions  
chmod +x script.sh         # Rendre exécutable  
chmod 644 fichier.txt      # Permissions standard fichier  
chmod 755 dossier          # Permissions standard dossier  
chmod 600 fichier_prive    # Fichier privé  
sudo chown user fichier    # Changer propriétaire  
```

### Checklist de sécurité

- ✅ Fichiers sensibles : `chmod 600`
- ✅ Clés SSH : `chmod 600 ~/.ssh/id_rsa`
- ✅ Scripts personnels : `chmod 700` ou `chmod 755`
- ✅ Documents partagés : `chmod 644`
- ✅ Dossiers partagés : `chmod 755`
- ❌ Jamais `chmod 777` (sauf cas très spécifique)

Les permissions sont un pilier de la sécurité Linux. Avec la pratique, leur lecture et modification deviendront naturelles. N'hésitez pas à expérimenter sur des fichiers de test !

Dans le prochain chapitre, nous découvrirons les commandes `sudo` et `root` pour gérer les privilèges administrateur du système.

⏭️ [Les commandes sudo et root](/07-le-terminal-et-commandes-de-base/07-les-commandes-sudo-et-root.md)
