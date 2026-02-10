🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 11.2 Les groupes et permissions avancées

## Introduction

Après avoir appris à créer et gérer des comptes utilisateurs, il est temps de comprendre comment Linux Mint contrôle **qui peut faire quoi** sur le système. Les groupes et les permissions sont les mécanismes fondamentaux qui régissent l'accès aux fichiers et aux ressources.

### Pourquoi les groupes et permissions sont-ils importants ?

- **Sécurité** : Empêcher les utilisateurs d'accéder à des fichiers qui ne les concernent pas
- **Collaboration** : Permettre à plusieurs utilisateurs de travailler sur les mêmes fichiers
- **Protection** : Éviter les suppressions ou modifications accidentelles
- **Organisation** : Structurer l'accès aux ressources de manière logique

> **Concept clé** : Sous Linux, **tout est fichier**, y compris les périphériques, les dossiers et certains processus. Les permissions s'appliquent donc à presque tout !

---

## Comprendre les groupes

### Qu'est-ce qu'un groupe ?

Un **groupe** est un ensemble d'utilisateurs qui partagent certains droits d'accès. Au lieu de donner des permissions à chaque utilisateur individuellement, on les attribue à un groupe, ce qui simplifie grandement la gestion.

### Exemples de groupes courants

Voici quelques groupes présents par défaut sur Linux Mint :

| Groupe | Rôle |
|--------|------|
| **sudo** | Permet d'exécuter des commandes administrateur avec `sudo` |
| **adm** | Accès en lecture aux fichiers de logs système |
| **cdrom** | Accès aux lecteurs CD/DVD |
| **audio** | Accès aux périphériques audio |
| **video** | Accès aux périphériques vidéo (webcams, cartes graphiques) |
| **plugdev** | Accès aux périphériques amovibles (clés USB, disques externes) |
| **netdev** | Gestion des connexions réseau |
| **lpadmin** | Administration des imprimantes |
| **sambashare** | Partage de fichiers via Samba |

### Groupes primaire et secondaires

Chaque utilisateur possède :
- **Un groupe primaire** : Automatiquement créé lors de la création du compte (généralement, le nom du groupe = nom de l'utilisateur)
- **Des groupes secondaires** : Groupes additionnels auxquels l'utilisateur appartient

---

## Voir les groupes d'un utilisateur

### Pour votre compte actuel

```bash
groups
```

Résultat exemple :
```
sophie adm cdrom sudo dip plugdev lpadmin sambashare
```

Cela signifie que l'utilisateur "sophie" appartient à 8 groupes.

### Pour un autre utilisateur

```bash
groups nom_utilisateur
```

Exemple :
```bash
groups jean
```

### Afficher tous les groupes du système

```bash
cat /etc/group
```

Cette commande affiche la liste complète des groupes avec leurs membres.

### Voir votre groupe primaire

```bash
id
```

Résultat exemple :
```
uid=1000(sophie) gid=1000(sophie) groups=1000(sophie),4(adm),24(cdrom),27(sudo)...
```

- **uid** : Identifiant numérique de l'utilisateur
- **gid** : Identifiant numérique du groupe primaire
- **groups** : Liste de tous les groupes (primaire et secondaires)

---

## Gérer les groupes

### Créer un nouveau groupe

```bash
sudo groupadd nom_du_groupe
```

Exemple pour créer un groupe "comptabilite" :
```bash
sudo groupadd comptabilite
```

### Ajouter un utilisateur à un groupe

```bash
sudo usermod -aG nom_du_groupe nom_utilisateur
```

> **Important** : L'option `-aG` signifie "append to Group" (ajouter au groupe). Sans le `a`, vous **remplacerez** tous les groupes secondaires de l'utilisateur !

Exemple :
```bash
sudo usermod -aG comptabilite sophie
```

### Retirer un utilisateur d'un groupe

```bash
sudo gpasswd -d nom_utilisateur nom_du_groupe
```

Exemple :
```bash
sudo gpasswd -d sophie comptabilite
```

### Supprimer un groupe

```bash
sudo groupdel nom_du_groupe
```

> **Note** : Vous ne pouvez pas supprimer un groupe s'il est le groupe primaire d'un utilisateur actif.

### Appliquer les changements de groupe

Après avoir ajouté un utilisateur à un groupe, les modifications ne prennent effet qu'après :
- **Déconnexion puis reconnexion** de l'utilisateur, OU
- Redémarrage des services concernés

Pour vérifier immédiatement dans le terminal actuel :
```bash
newgrp nom_du_groupe
```

---

## Comprendre les permissions Linux

### Le système de permissions

Linux utilise un système de permissions en **3 niveaux** :
1. **Propriétaire (User)** : La personne qui possède le fichier
2. **Groupe (Group)** : Les membres du groupe associé au fichier
3. **Autres (Others)** : Tous les autres utilisateurs du système

Et **3 types de droits** :
- **r (read)** : Lecture
- **w (write)** : Écriture/Modification
- **x (execute)** : Exécution (pour les fichiers) ou accès (pour les dossiers)

### Afficher les permissions

Utilisez la commande `ls -l` pour voir les permissions :

```bash
ls -l
```

Résultat exemple :
```
-rw-r--r-- 1 sophie sophie  2048 nov 29 10:30 document.txt
drwxr-xr-x 2 sophie sophie  4096 nov 29 10:35 dossier_projet
-rwxr-xr-x 1 sophie sophie  8192 nov 29 10:40 script.sh
```

### Décoder les permissions

Prenons l'exemple : `-rw-r--r--`

```
-  rw-  r--  r--
│   │    │    │
│   │    │    └─ Permissions pour les "Autres" : lecture seulement
│   │    └────── Permissions pour le "Groupe" : lecture seulement
│   └─────────── Permissions pour le "Propriétaire" : lecture + écriture
└─────────────── Type (- = fichier, d = dossier, l = lien symbolique)
```

#### Détail des symboles

- **r** (read) = 4 : Droit de lecture
- **w** (write) = 2 : Droit d'écriture
- **x** (execute) = 1 : Droit d'exécution
- **-** : Pas de permission

### Permissions pour les dossiers

Les permissions ont un sens différent pour les dossiers :

| Permission | Signification pour un dossier |
|------------|-------------------------------|
| **r** | Lister le contenu du dossier (`ls`) |
| **w** | Créer, supprimer, renommer des fichiers dans le dossier |
| **x** | Accéder au dossier (`cd`) et accéder aux fichiers qu'il contient |

> **Important** : Pour accéder à un fichier dans un dossier, vous devez avoir la permission **x** sur le dossier ET les permissions appropriées sur le fichier.

---

## Modifier les permissions avec chmod

### Méthode symbolique (plus intuitive pour débutants)

La syntaxe générale est :
```bash
chmod [qui][opération][permission] fichier
```

**Qui** :
- `u` : utilisateur (propriétaire)
- `g` : groupe
- `o` : autres
- `a` : tous (all = u+g+o)

**Opération** :
- `+` : ajouter une permission
- `-` : retirer une permission
- `=` : définir exactement ces permissions (et retirer les autres)

**Permission** :
- `r` : lecture
- `w` : écriture
- `x` : exécution

#### Exemples pratiques

**Ajouter le droit d'exécution au propriétaire** :
```bash
chmod u+x script.sh
```

**Retirer le droit d'écriture au groupe et aux autres** :
```bash
chmod go-w document.txt
```

**Donner tous les droits au propriétaire uniquement** :
```bash
chmod u=rwx,go= fichier_prive.txt
```

**Rendre un fichier exécutable pour tout le monde** :
```bash
chmod a+x programme.sh
```

**Donner lecture et écriture au groupe** :
```bash
chmod g+rw projet.txt
```

### Méthode numérique (octale)

Chaque permission a une valeur numérique :
- **r** = 4
- **w** = 2
- **x** = 1

On **additionne** ces valeurs pour chaque catégorie (propriétaire, groupe, autres).

#### Valeurs courantes

| Chiffre | Permissions | Signification |
|---------|-------------|---------------|
| **0** | `---` | Aucun droit |
| **1** | `--x` | Exécution seulement |
| **2** | `-w-` | Écriture seulement (rare) |
| **3** | `-wx` | Écriture + Exécution |
| **4** | `r--` | Lecture seulement |
| **5** | `r-x` | Lecture + Exécution |
| **6** | `rw-` | Lecture + Écriture |
| **7** | `rwx` | Tous les droits |

#### Exemples courants

**755** (rwxr-xr-x) - Idéal pour les scripts :
```bash
chmod 755 script.sh
```
- Propriétaire : tous les droits (7 = 4+2+1)
- Groupe : lecture + exécution (5 = 4+1)
- Autres : lecture + exécution (5 = 4+1)

**644** (rw-r--r--) - Idéal pour les documents :
```bash
chmod 644 document.txt
```
- Propriétaire : lecture + écriture (6 = 4+2)
- Groupe : lecture seulement (4)
- Autres : lecture seulement (4)

**600** (rw-------) - Fichier privé :
```bash
chmod 600 fichier_confidentiel.txt
```
- Propriétaire : lecture + écriture (6 = 4+2)
- Groupe : aucun droit (0)
- Autres : aucun droit (0)

**700** (rwx------) - Dossier privé :
```bash
chmod 700 dossier_personnel/
```

### Modifier les permissions récursivement

Pour appliquer les permissions à un dossier et **tout son contenu** :

```bash
chmod -R 755 mon_dossier/
```

L'option `-R` signifie "récursif".

> **Attention** : Soyez prudent avec `-R`, car cela modifie tous les fichiers et sous-dossiers. Vous pourriez rendre des fichiers exécutables alors qu'ils ne devraient pas l'être.

---

## Modifier le propriétaire et le groupe

### Changer le propriétaire avec chown

```bash
sudo chown nouveau_proprietaire fichier
```

Exemple :
```bash
sudo chown jean document.txt
```

### Changer le propriétaire ET le groupe

```bash
sudo chown nouveau_proprietaire:nouveau_groupe fichier
```

Exemple :
```bash
sudo chown jean:comptabilite rapport.xlsx
```

### Changer uniquement le groupe avec chgrp

```bash
sudo chgrp nouveau_groupe fichier
```

Exemple :
```bash
sudo chgrp comptabilite facture.pdf
```

### Modification récursive

Pour changer le propriétaire d'un dossier et de tout son contenu :

```bash
sudo chown -R sophie:sophie /home/sophie/Documents/
```

---

## Cas pratiques courants

### Créer un dossier partagé entre utilisateurs

Imaginons que Sophie et Jean doivent collaborer sur un projet.

**1. Créer un groupe "projet"** :
```bash
sudo groupadd projet
```

**2. Ajouter Sophie et Jean au groupe** :
```bash
sudo usermod -aG projet sophie  
sudo usermod -aG projet jean  
```

**3. Créer un dossier partagé** :
```bash
sudo mkdir /home/partage/projet
```

**4. Définir le groupe du dossier** :
```bash
sudo chgrp projet /home/partage/projet
```

**5. Donner les bonnes permissions** :
```bash
sudo chmod 770 /home/partage/projet
```

Résultat : Sophie et Jean peuvent lire, écrire et accéder au dossier, mais pas les autres utilisateurs.

**6. (Optionnel) Utiliser le bit SGID** :
```bash
sudo chmod g+s /home/partage/projet
```

Le bit SGID (Set Group ID) fait que tous les nouveaux fichiers créés dans ce dossier héritent automatiquement du groupe du dossier (ici "projet").

### Rendre un script exécutable

Vous venez de créer un script bash et voulez l'exécuter :

```bash
chmod +x mon_script.sh
```

Maintenant vous pouvez l'exécuter avec :
```bash
./mon_script.sh
```

### Sécuriser un fichier sensible

Pour un fichier contenant des mots de passe ou des clés :

```bash
chmod 600 cles_privees.txt
```

Seul vous pouvez le lire et le modifier.

### Réparer les permissions d'un dossier personnel

Si les permissions de votre dossier `/home/utilisateur` sont incorrectes :

```bash
sudo chown -R sophie:sophie /home/sophie  
sudo chmod 755 /home/sophie  
sudo chmod 700 /home/sophie/.ssh  
```

---

## Permissions spéciales avancées

### Le bit SUID (Set User ID)

Lorsqu'un fichier avec le bit SUID est exécuté, il s'exécute avec les permissions du **propriétaire** du fichier, pas de l'utilisateur qui l'exécute.

**Voir le bit SUID** :
```bash
ls -l /usr/bin/passwd
```
Résultat :
```
-rwsr-xr-x 1 root root 68208 /usr/bin/passwd
```

Le `s` à la place du `x` indique le bit SUID.

**Définir le bit SUID** :
```bash
chmod u+s fichier
# ou en numérique
chmod 4755 fichier
```

> **Sécurité** : Le bit SUID est potentiellement dangereux. Ne l'utilisez que si vous comprenez parfaitement ce que vous faites.

### Le bit SGID (Set Group ID)

Pour les fichiers, similaire à SUID mais avec le groupe.  
Pour les dossiers, les nouveaux fichiers héritent du groupe du dossier.  

**Définir le bit SGID** :
```bash
chmod g+s dossier
# ou en numérique
chmod 2755 dossier
```

### Le sticky bit

Sur un dossier, le sticky bit empêche les utilisateurs de supprimer ou renommer les fichiers qui ne leur appartiennent pas, même s'ils ont les permissions d'écriture sur le dossier.

**Exemple** : Le dossier `/tmp` utilise le sticky bit :
```bash
ls -ld /tmp
```
Résultat :
```
drwxrwxrwt 20 root root 4096 nov 29 10:45 /tmp
```

Le `t` à la fin indique le sticky bit.

**Définir le sticky bit** :
```bash
chmod +t dossier
# ou en numérique
chmod 1777 dossier
```

---

## Les ACL (Access Control Lists) - Permissions avancées

Les permissions standard (rwx) sont parfois trop limitées. Les **ACL** permettent de définir des permissions plus fines pour des utilisateurs ou groupes spécifiques.

### Vérifier si les ACL sont actives

```bash
getfacl fichier.txt
```

### Donner des permissions spécifiques à un utilisateur

```bash
setfacl -m u:jean:rw fichier.txt
```

Cela donne à Jean le droit de lire et écrire `fichier.txt`, sans modifier les permissions standards.

### Donner des permissions spécifiques à un groupe

```bash
setfacl -m g:comptabilite:rx dossier/
```

### Retirer une ACL

```bash
setfacl -x u:jean fichier.txt
```

### Retirer toutes les ACL

```bash
setfacl -b fichier.txt
```

### ACL récursives

```bash
setfacl -R -m u:jean:rwx dossier/
```

### ACL par défaut (pour les nouveaux fichiers)

```bash
setfacl -d -m g:projet:rwx dossier_partage/
```

Les nouveaux fichiers créés dans `dossier_partage/` hériteront automatiquement de ces permissions pour le groupe "projet".

---

## Bonnes pratiques

### Sécurité

1. **Principe du moindre privilège** : Accordez uniquement les permissions nécessaires
2. **Évitez 777** : Les permissions `chmod 777` (tous les droits pour tous) sont un risque de sécurité majeur
3. **Protégez les fichiers sensibles** : Utilisez `chmod 600` pour les fichiers de configuration contenant des mots de passe
4. **Vérifiez régulièrement** : Auditez les permissions sur les dossiers importants
5. **SSH et clés privées** : Les clés SSH doivent avoir les permissions 600, sinon SSH refusera de les utiliser

### Organisation

1. **Utilisez des groupes** : C'est plus facile que de gérer les permissions utilisateur par utilisateur
2. **Nommage cohérent** : Donnez des noms explicites à vos groupes
3. **Documentez** : Notez qui appartient à quel groupe et pourquoi
4. **Révisez régulièrement** : Supprimez les utilisateurs des groupes quand ils n'en ont plus besoin

### Dossiers partagés

1. **Bit SGID** : Utilisez-le sur les dossiers partagés pour que les fichiers héritent du bon groupe
2. **Umask** : Configurez le umask pour que les nouveaux fichiers aient les bonnes permissions par défaut
3. **ACL pour la flexibilité** : Utilisez les ACL quand les permissions standard ne suffisent pas

### Diagnostic

Pour trouver tous les fichiers avec des permissions trop ouvertes :
```bash
find /home -type f -perm 0777
```

Pour trouver tous les fichiers avec le bit SUID :
```bash
find / -type f -perm -4000 2>/dev/null
```

---

## Commandes de référence rapide

### Groupes

| Commande | Description |
|----------|-------------|
| `groups` | Voir mes groupes |
| `groups utilisateur` | Voir les groupes d'un utilisateur |
| `sudo groupadd nom` | Créer un groupe |
| `sudo usermod -aG groupe user` | Ajouter un utilisateur à un groupe |
| `sudo gpasswd -d user groupe` | Retirer un utilisateur d'un groupe |
| `sudo groupdel nom` | Supprimer un groupe |

### Permissions

| Commande | Description |
|----------|-------------|
| `ls -l` | Voir les permissions |
| `chmod u+x fichier` | Ajouter exécution (propriétaire) |
| `chmod 755 fichier` | rwxr-xr-x |
| `chmod 644 fichier` | rw-r--r-- |
| `chmod -R 755 dossier/` | Récursif |
| `sudo chown user:groupe fichier` | Changer propriétaire et groupe |
| `sudo chgrp groupe fichier` | Changer le groupe |

### ACL

| Commande | Description |
|----------|-------------|
| `getfacl fichier` | Voir les ACL |
| `setfacl -m u:user:rwx fichier` | Définir ACL utilisateur |
| `setfacl -m g:groupe:rx fichier` | Définir ACL groupe |
| `setfacl -x u:user fichier` | Retirer ACL |
| `setfacl -b fichier` | Retirer toutes les ACL |

---

## Résumé

Les groupes et permissions sont des concepts essentiels de Linux :

- **Les groupes** permettent de gérer efficacement l'accès pour plusieurs utilisateurs
- **Les permissions de base** (rwx) couvrent la plupart des besoins quotidiens
- **chmod, chown, chgrp** sont les commandes principales pour gérer les accès
- **Les ACL** offrent une flexibilité supplémentaire quand nécessaire
- **Les permissions spéciales** (SUID, SGID, sticky bit) ont des usages avancés spécifiques

Maîtriser ces concepts vous permet de :
- Sécuriser vos données personnelles
- Collaborer efficacement avec d'autres utilisateurs
- Comprendre et résoudre les problèmes d'accès
- Protéger votre système contre les accès non autorisés

Dans le prochain chapitre, nous aborderons les **mots de passe et l'authentification**, qui complètent la sécurité des comptes utilisateurs.


⏭️ [Mots de passe et authentification](/11-gestion-des-utilisateurs-et-securite/03-mots-de-passe-et-authentification.md)
