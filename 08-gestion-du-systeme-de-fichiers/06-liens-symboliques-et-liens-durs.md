🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.6 Liens symboliques et liens durs

## Introduction

### Qu'est-ce qu'un lien ?

Un **lien** sous Linux est une façon d'accéder à un fichier ou un dossier depuis plusieurs emplacements différents, sans dupliquer les données. C'est comme avoir plusieurs chemins qui mènent au même endroit.

**Analogie du monde réel** :
Imaginez une maison avec deux portes d'entrée :
- La maison existe en un seul exemplaire
- Mais vous pouvez y accéder par la porte de devant ou celle de derrière
- Les deux portes mènent au même intérieur
- Un lien fonctionne de la même façon : plusieurs "portes" vers le même fichier

### Pourquoi utiliser des liens ?

**Avantages** :
- ✅ **Économie d'espace** : Pas de duplication des données
- ✅ **Organisation flexible** : Accéder au même fichier depuis différents endroits
- ✅ **Maintenance simplifiée** : Modifier un fichier, changement visible partout
- ✅ **Compatibilité** : Créer des chemins alternatifs sans casser les scripts
- ✅ **Structures complexes** : Organiser vos fichiers de façon logique

### Les deux types de liens

Linux propose **deux types** de liens, très différents :

1. **Liens symboliques** (symlinks, soft links) : Comme des "raccourcis"
2. **Liens durs** (hard links) : Comme des "clones" pointant vers les mêmes données

Voyons en détail chacun de ces types.

---

## Les liens symboliques (symlinks)

### Qu'est-ce qu'un lien symbolique ?

Un **lien symbolique** (ou symlink) est un **pointeur** vers un autre fichier ou dossier. C'est l'équivalent des **raccourcis** sous Windows.

**Analogie** :
Un lien symbolique est comme une **note Post-it** qui dit "le vrai fichier est là-bas".
- La note ne contient pas les données
- Elle indique juste où les trouver
- Si vous supprimez le fichier original, la note pointe vers le vide

### Caractéristiques des liens symboliques

- 📌 **Fichier séparé** : Le symlink est un fichier distinct qui contient le chemin vers la cible
- 📌 **Peut pointer vers tout** : Fichiers, dossiers, même sur d'autres partitions/disques
- 📌 **Cassable** : Si vous supprimez la cible, le lien devient "cassé" (broken link)
- 📌 **Visible** : On peut voir que c'est un lien (flèche dans Nemo, `l` dans `ls -l`)
- 📌 **Permissions propres** : Le lien a ses propres permissions (mais peu importantes)

### Créer un lien symbolique

**Syntaxe** :
```bash
ln -s CIBLE NOM_DU_LIEN
```

**Important** :
- **CIBLE** = le fichier/dossier original
- **NOM_DU_LIEN** = le lien que vous créez
- **-s** = symbolique (ne pas oublier !)

### Exemples pratiques

**Exemple 1 : Lien vers un fichier**

```bash
# Créer un fichier de test
echo "Contenu du fichier" > ~/Documents/fichier-original.txt

# Créer un lien symbolique sur le bureau
ln -s ~/Documents/fichier-original.txt ~/Bureau/raccourci-fichier.txt

# Vérifier
cat ~/Bureau/raccourci-fichier.txt
# Affiche : Contenu du fichier
```

**Résultat** :
- Vous pouvez accéder au fichier via les deux chemins
- Modifier via le lien modifie l'original
- Le lien prend très peu d'espace (juste le chemin)

**Exemple 2 : Lien vers un dossier**

```bash
# Créer un lien vers vos téléchargements sur le bureau
ln -s ~/Téléchargements ~/Bureau/Téléchargements

# Maintenant vous pouvez accéder à vos téléchargements depuis le bureau
ls ~/Bureau/Téléchargements
```

**Exemple 3 : Lien absolu vs relatif**

**Chemin absolu** (recommandé) :
```bash
ln -s /home/pierre/Documents/projet ~/Bureau/projet
```

**Chemin relatif** :
```bash
cd ~/Bureau  
ln -s ../Documents/projet projet  
```

💡 **Conseil** : Utilisez des chemins **absolus** (commençant par `/`) pour éviter les surprises si le lien est déplacé.

### Identifier un lien symbolique

**Dans le gestionnaire de fichiers (Nemo)** :
- Icône avec une **petite flèche** en bas à gauche
- Clic droit → Propriétés → Type : "Lien"

**En ligne de commande** :
```bash
ls -l ~/Bureau/

# Résultat typique :
lrwxrwxrwx 1 pierre pierre 28 nov 29 10:30 projet -> /home/pierre/Documents/projet
```

**Explication** :
- **l** au début = lien symbolique (link)
- **→** indique vers quoi pointe le lien
- Couleur cyan/bleu clair dans le terminal (généralement)

**Vérifier où pointe un lien** :
```bash
readlink ~/Bureau/projet
# Affiche : /home/pierre/Documents/projet

# Ou obtenir le chemin absolu
readlink -f ~/Bureau/projet
```

### Supprimer un lien symbolique

⚠️ **ATTENTION** : Ne pas mettre de `/` final pour les dossiers !

**Bon** :
```bash
rm ~/Bureau/projet
# ou
unlink ~/Bureau/projet
```

**MAUVAIS** :
```bash
rm ~/Bureau/projet/     # ❌ Supprime le CONTENU du dossier cible !
```

💡 **Important** : Supprimer un lien ne supprime **PAS** le fichier/dossier original.

### Lien symbolique cassé (broken link)

**Qu'est-ce qu'un lien cassé ?**
Un lien qui pointe vers un fichier qui n'existe plus.

**Comment ça arrive ?** :
```bash
# Créer un fichier et un lien
echo "test" > original.txt  
ln -s original.txt lien.txt  

# Supprimer l'original
rm original.txt

# Le lien existe toujours mais est cassé
cat lien.txt
# Erreur : No such file or directory
```

**Identifier les liens cassés** :
```bash
# Trouver tous les liens cassés dans un dossier
find ~/Bureau -xtype l
```

**Dans Nemo** :
Les liens cassés apparaissent souvent avec une icône différente ou en rouge.

---

## Les liens durs (hard links)

### Qu'est-ce qu'un lien dur ?

Un **lien dur** est un **nom supplémentaire** pour le même fichier. C'est comme si le fichier avait deux (ou plus) noms différents, mais c'est toujours le même fichier physiquement.

**Analogie** :
Imaginez une personne avec deux passeports :
- C'est la même personne (les mêmes données)
- Elle a juste deux identités différentes
- Tant qu'un passeport existe, la personne "existe"
- Elle disparaît seulement quand tous les passeports sont détruits

### Caractéristiques des liens durs

- 📌 **Même inode** : Le lien et l'original partagent le même numéro d'inode (identifiant unique)
- 📌 **Indiscernables** : Impossible de savoir lequel est "l'original" et lequel est le "lien"
- 📌 **Ne peut pas être cassé** : Tant qu'un nom existe, les données existent
- 📌 **Même partition** : Ne fonctionne que sur la même partition
- 📌 **Fichiers uniquement** : Ne peut pas créer de liens durs vers des dossiers

### Créer un lien dur

**Syntaxe** :
```bash
ln CIBLE NOM_DU_LIEN
```

**Note** : Pas de `-s` (c'est la différence avec un lien symbolique)

### Exemple pratique

```bash
# Créer un fichier original
echo "Données importantes" > ~/Documents/original.txt

# Créer un lien dur
ln ~/Documents/original.txt ~/Bureau/copie.txt

# Les deux fichiers sont identiques et partagent les mêmes données
cat ~/Documents/original.txt  
cat ~/Bureau/copie.txt  
# Tous deux affichent : Données importantes

# Modifier via un nom
echo "Nouvelles données" > ~/Bureau/copie.txt

# Le changement est visible via l'autre nom
cat ~/Documents/original.txt
# Affiche : Nouvelles données

# Supprimer "l'original"
rm ~/Documents/original.txt

# Le fichier existe toujours via l'autre nom !
cat ~/Bureau/copie.txt
# Affiche toujours : Nouvelles données
```

### Comprendre les inodes

**Qu'est-ce qu'un inode ?**
Un **inode** est un numéro unique qui identifie un fichier sur le système de fichiers. Il contient les métadonnées du fichier (taille, permissions, dates, emplacement physique).

**Voir les inodes** :
```bash
ls -li

# Résultat :
# 1234567 -rw-r--r-- 2 pierre pierre 18 nov 29 10:30 copie.txt
# 1234567 -rw-r--r-- 2 pierre pierre 18 nov 29 10:30 original.txt
```

**Explication** :
- **1234567** = numéro d'inode (le même pour les deux !)
- **2** = nombre de liens durs (hard link count)

💡 **Tant que le compteur > 0**, les données existent sur le disque.

### Supprimer un lien dur

```bash
rm ~/Bureau/copie.txt
```

**Ce qui se passe** :
- Le nom `copie.txt` disparaît
- Le compteur de liens diminue de 1
- Si le compteur atteint 0, les données sont vraiment supprimées
- Sinon, les données restent accessibles via les autres noms

---

## Comparaison : Symbolique vs Dur

### Tableau comparatif

| Caractéristique | Lien Symbolique | Lien Dur |
|-----------------|-----------------|----------|
| **Analogie** | Raccourci Windows | Même fichier, plusieurs noms |
| **Fichier séparé** | ✅ Oui | ❌ Non (même inode) |
| **Peut pointer vers dossier** | ✅ Oui | ❌ Non |
| **Peut pointer vers autre partition** | ✅ Oui | ❌ Non |
| **Devient cassé si cible supprimée** | ✅ Oui | ❌ Non (données restent) |
| **Visible en tant que lien** | ✅ Oui (flèche, `l`) | ❌ Non (fichier normal) |
| **Taille** | Très petit (chemin) | Même que l'original |
| **Permissions** | Propres au lien | Partagées |
| **Utilisation** | Très courante | Plus rare |

### Visualisation

**Lien symbolique** :
```
[Lien symbolique]  ──→  [Fichier original]  ──→  [Données sur disque]
    (pointeur)              (inode 12345)

Si vous supprimez le fichier original :
[Lien symbolique]  ──→  ❌ CASSÉ
```

**Lien dur** :
```
[Nom 1]  ─┐
          ├──→  [Inode 12345]  ──→  [Données sur disque]
[Nom 2]  ─┘       (compteur: 2)

Si vous supprimez Nom 1 :
[Nom 2]  ───→  [Inode 12345]  ──→  [Données sur disque]
                  (compteur: 1)

Les données restent !
```

---

## Cas d'usage pratiques

### 1. Organiser sa musique/photos

**Scénario** : Vous voulez accéder à vos photos depuis plusieurs endroits.

**Avec lien symbolique** :
```bash
# Vos photos sont dans Documents
# Créer un accès rapide sur le Bureau
ln -s ~/Documents/Photos ~/Bureau/Mes-Photos

# Créer un accès pour un projet spécifique
ln -s ~/Documents/Photos/Vacances-2024 ~/Projets/Vidéo-Vacances/sources
```

### 2. Partager un dossier Dropbox/Drive

**Scénario** : Votre Dropbox est dans `/home/pierre/Dropbox`, mais vous voulez y accéder facilement.

```bash
# Lien sur le Bureau
ln -s ~/Dropbox ~/Bureau/Dropbox

# Lien dans le dossier de projets
ln -s ~/Dropbox/Travail ~/Projets/Dossiers-Partagés
```

### 3. Gérer plusieurs versions d'un logiciel

**Scénario** : Vous avez plusieurs versions de Python installées.

```bash
# Python 3.9 installé dans /usr/bin/python3.9
# Python 3.10 installé dans /usr/bin/python3.10

# Créer un lien symbolique pour choisir la version par défaut
sudo ln -s /usr/bin/python3.10 /usr/local/bin/python3

# Maintenant "python3" lance la version 3.10
# Pour changer de version, recréez juste le lien
```

### 4. Sauvegarder avec liens durs (économie d'espace)

**Scénario** : Créer des sauvegardes sans dupliquer les fichiers inchangés.

```bash
# Structure :
# sauvegarde-2024-11-01/fichier.txt
# sauvegarde-2024-11-15/fichier.txt (même contenu)

# Au lieu de copier :
cp -r projet/ sauvegarde-2024-11-01/

# Utiliser des liens durs pour les fichiers identiques :
cp -al sauvegarde-2024-11-01/ sauvegarde-2024-11-15/
# Ensuite, modifiez uniquement les fichiers qui changent

# Résultat : Économie massive d'espace disque !
```

💡 **C'est ce que font des outils comme `rsync --link-dest` ou `Time Machine` sur Mac.**

### 5. Compatibilité logicielle

**Scénario** : Un programme cherche un fichier à un emplacement spécifique.

```bash
# Le programme cherche : /opt/app/config.conf
# Mais votre config est dans : /home/pierre/.config/app.conf

# Créer un lien symbolique
sudo ln -s /home/pierre/.config/app.conf /opt/app/config.conf

# Le programme trouve son fichier, vous gardez votre organisation
```

### 6. Réorganiser sans casser les scripts

**Scénario** : Vous voulez déplacer un dossier mais des scripts l'utilisent.

```bash
# Ancien emplacement : /home/pierre/data
# Nouveau : /home/pierre/Documents/Projets/data

# Déplacer
mv /home/pierre/data /home/pierre/Documents/Projets/

# Créer un lien pour compatibilité
ln -s /home/pierre/Documents/Projets/data /home/pierre/data

# Les scripts continuent de fonctionner !
```

---

## Commandes utiles

### Créer des liens

**Lien symbolique (fichier)** :
```bash
ln -s /chemin/vers/fichier-original /chemin/vers/lien
```

**Lien symbolique (dossier)** :
```bash
ln -s /chemin/vers/dossier-original /chemin/vers/lien
```

**Lien dur** :
```bash
ln /chemin/vers/fichier-original /chemin/vers/lien
```

**Créer dans le dossier actuel** :
```bash
ln -s /chemin/vers/original .
# Le lien aura le même nom que l'original
```

### Inspecter les liens

**Voir où pointe un lien symbolique** :
```bash
readlink lien  
readlink -f lien  # Chemin absolu complet  
```

**Voir le nombre de liens durs** :
```bash
ls -l fichier
# Le nombre après les permissions indique le nombre de liens durs
```

**Trouver tous les liens durs d'un fichier** :
```bash
find / -inum NUMÉRO_INODE 2>/dev/null
# Remplacez NUMÉRO_INODE par celui obtenu avec ls -li
```

**Trouver tous les liens symboliques** :
```bash
find /chemin -type l
```

**Trouver les liens cassés** :
```bash
find /chemin -xtype l
```

### Mettre à jour un lien

**Pour changer la cible d'un lien symbolique** :
```bash
# Méthode 1 : Supprimer et recréer
rm lien  
ln -s nouvelle-cible lien  

# Méthode 2 : Utiliser -f (force) et -n (no-dereference)
ln -sfn nouvelle-cible lien
```

### Copier avec préservation des liens

**Copier en préservant les liens symboliques** :
```bash
cp -a source/ destination/
# ou
rsync -a source/ destination/
```

**Copier en suivant les liens (copier les cibles)** :
```bash
cp -L lien destination/
```

---

## Pièges courants et solutions

### Piège 1 : Supprimer un lien symbolique de dossier

❌ **MAUVAIS** :
```bash
rm lien-dossier/
# Supprime le CONTENU du dossier cible !
```

✅ **BON** :
```bash
rm lien-dossier
# ou
unlink lien-dossier
```

### Piège 2 : Liens symboliques relatifs

```bash
# Créer un lien relatif
ln -s ../Documents/fichier.txt lien.txt

# Si vous déplacez le lien, il devient cassé !
mv lien.txt ~/Bureau/  
cat ~/Bureau/lien.txt  
# Erreur : cherche ~/Bureau/../Documents/fichier.txt (qui n'existe pas)
```

**Solution** : Utilisez des chemins absolus (`/home/pierre/...` ou `~/...`)

### Piège 3 : Permissions sur liens symboliques

```bash
# Les permissions du lien ne comptent pas vraiment
chmod 777 lien-symbolique  # N'a aucun effet

# Ce sont les permissions du fichier cible qui comptent
chmod 644 fichier-original  # Ça, c'est important
```

### Piège 4 : Liens durs et partitions

```bash
# Essayer de créer un lien dur vers une autre partition
ln /home/pierre/fichier.txt /mnt/autre-disque/lien.txt
# Erreur : Invalid cross-device link

# Solution : Utiliser un lien symbolique
ln -s /home/pierre/fichier.txt /mnt/autre-disque/lien.txt
```

### Piège 5 : Éditer un lien avec certains éditeurs

**Certains éditeurs** (comme `nano` ou `vim`) suivent le lien et éditent le fichier original.  
**D'autres** (comme certaines configurations de `vim`) peuvent remplacer le lien par un nouveau fichier !  

**Solution** : Soyez conscient du comportement de votre éditeur, ou éditez directement le fichier original.

---

## Liens symboliques sous Windows (comparaison)

### Équivalents Windows

| Linux | Windows | Commande Windows |
|-------|---------|------------------|
| Lien symbolique (fichier) | Symlink | `mklink fichier cible` |
| Lien symbolique (dossier) | Symlink | `mklink /D dossier cible` |
| Lien dur | Hard link | `mklink /H fichier cible` |
| N/A | Jonction | `mklink /J dossier cible` |
| N/A | Raccourci (.lnk) | Interface graphique |

**Différences importantes** :
- Les **raccourcis Windows** (.lnk) sont différents des vrais symlinks
- Windows nécessite des privilèges administrateur pour créer des symlinks
- Les symlinks Linux sont beaucoup plus intégrés au système

---

## Quand utiliser quoi ?

### Utilisez un lien symbolique si :

- ✅ Vous voulez un "raccourci" vers un fichier/dossier
- ✅ Le lien peut être sur une partition différente
- ✅ Vous voulez pointer vers un dossier
- ✅ Vous voulez que le lien soit clairement identifiable
- ✅ C'est la solution par défaut dans 95% des cas

### Utilisez un lien dur si :

- ✅ Vous voulez plusieurs noms pour le même fichier
- ✅ Vous voulez que les données persistent tant qu'un nom existe
- ✅ Vous faites des sauvegardes intelligentes (économie d'espace)
- ✅ Vous voulez éviter les liens cassés
- ✅ Tout est sur la même partition

### N'utilisez PAS de lien si :

- ❌ Vous voulez une vraie copie indépendante → utilisez `cp`
- ❌ Vous voulez synchroniser deux dossiers → utilisez `rsync`
- ❌ Vous avez besoin de modifier différemment deux "versions" → copiez

---

## Exemples pratiques complets

### Exemple 1 : Organiser ses dotfiles

**Scénario** : Vous gérez vos fichiers de configuration avec Git.

```bash
# Vos configs sont dans ~/dotfiles/
# Mais les applications les cherchent dans ~/

# Créer les liens
ln -s ~/dotfiles/.bashrc ~/.bashrc  
ln -s ~/dotfiles/.vimrc ~/.vimrc  
ln -s ~/dotfiles/.config/Code ~/.config/Code  

# Maintenant vous pouvez versionner vos configs facilement
cd ~/dotfiles  
git add .  
git commit -m "Update config"  
```

### Exemple 2 : Gérer un serveur web

**Scénario** : Site web avec plusieurs versions.

```bash
# Structure :
# /var/www/site-v1.0/
# /var/www/site-v2.0/

# Lien symbolique vers la version active
sudo ln -s /var/www/site-v1.0 /var/www/site

# Configurer Apache/Nginx pour servir /var/www/site

# Pour mettre à jour le site :
sudo ln -sfn /var/www/site-v2.0 /var/www/site

# Retour arrière facile en cas de problème !
sudo ln -sfn /var/www/site-v1.0 /var/www/site
```

### Exemple 3 : Économiser de l'espace avec des sauvegardes

**Scénario** : Sauvegardes quotidiennes intelligentes.

```bash
#!/bin/bash
# Script de sauvegarde avec liens durs

PROJET="/home/pierre/Documents/MonProjet"  
SAUVEGARDES="/media/sauvegarde"  
DATE=$(date +%Y-%m-%d)  
DERNIERE=$(ls -td $SAUVEGARDES/* | head -1)  

# Créer nouvelle sauvegarde avec liens durs vers la dernière
if [ -d "$DERNIERE" ]; then
    cp -al "$DERNIERE" "$SAUVEGARDES/backup-$DATE"
fi

# Synchroniser (seuls les fichiers modifiés sont vraiment copiés)
rsync -av --delete "$PROJET/" "$SAUVEGARDES/backup-$DATE/"

# Résultat : Sauvegardes complètes quotidiennes sans dupliquer
# les fichiers inchangés !
```

---

## Résumé

### Points clés à retenir

1. **Lien symbolique** = Raccourci, pointeur vers un fichier/dossier
   - Peut être cassé si la cible est supprimée
   - Fonctionne avec dossiers et entre partitions
   - Visible et identifiable
   - Utilisation la plus courante

2. **Lien dur** = Nom supplémentaire pour le même fichier
   - Partage le même inode
   - Ne peut pas être cassé
   - Fichiers seulement, même partition
   - Utilisation plus rare

3. **Commandes essentielles** :
   ```bash
   ln -s cible lien     # Créer lien symbolique
   ln cible lien        # Créer lien dur
   readlink lien        # Voir où pointe un lien
   rm lien              # Supprimer un lien (pas de / final !)
   ```

4. **Différence principale** :
   - Symbolique : pointeur → peut casser
   - Dur : clone → ne casse jamais

### Commandes de référence rapide

```bash
# Créer
ln -s /cible /lien              # Lien symbolique  
ln /cible /lien                 # Lien dur  

# Inspecter
readlink -f lien                # Où pointe ?  
ls -l                           # Voir les liens (l et →)  
ls -li                          # Voir les inodes  
find . -type l                  # Trouver liens symboliques  
find . -xtype l                 # Trouver liens cassés  

# Supprimer
rm lien                         # ✅ BON  
rm lien/                        # ❌ MAUVAIS (dossiers)  
unlink lien                     # Alternative  

# Mettre à jour
ln -sfn nouvelle-cible lien     # Changer la cible
```

### Pour aller plus loin

Une fois à l'aise avec les liens, vous pourrez :
- Créer des structures de fichiers complexes
- Gérer des configurations avec Git et symlinks
- Optimiser vos sauvegardes avec des liens durs
- Gérer facilement différentes versions de logiciels

Mais pour débuter, **utilisez les liens symboliques** pour créer des raccourcis pratiques vers vos fichiers et dossiers fréquemment utilisés. C'est simple, sûr et très utile !

⏭️ [/etc/fstab pour montage automatique](/08-gestion-du-systeme-de-fichiers/07-etc-fstab-pour-montage-automatique.md)
