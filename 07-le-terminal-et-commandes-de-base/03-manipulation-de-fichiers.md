🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.3 - Manipulation de fichiers (cp, mv, rm, mkdir, touch)

## Introduction

Maintenant que vous savez naviguer dans votre système, il est temps d'apprendre à manipuler les fichiers et dossiers : les créer, les copier, les déplacer, les renommer et les supprimer.

**Analogie :** Si la navigation vous permet de vous déplacer dans votre bibliothèque (système de fichiers), la manipulation vous permet de :
- Créer de nouvelles étagères (`mkdir`)
- Ajouter de nouveaux livres vierges (`touch`)
- Faire des copies de documents (`cp`)
- Déplacer ou réorganiser (`mv`)
- Jeter ce dont vous n'avez plus besoin (`rm`)

Ces cinq commandes constituent le cœur de la gestion de fichiers en ligne de commande. Maîtrisez-les et vous serez capable de gérer efficacement l'ensemble de vos données.

**⚠️ Avertissement important :** Contrairement à l'interface graphique, le terminal ne possède pas de corbeille. Quand vous supprimez avec `rm`, c'est définitif ! Nous verrons comment minimiser les risques.

---

## La commande `mkdir` : Créer des dossiers

### Signification

**mkdir** signifie **Make Directory** (Créer un répertoire).

### Utilisation de base

```bash
mkdir nom_du_dossier
```

### Exemples simples

#### Créer un seul dossier

```bash
mkdir Projets
```

Crée un dossier nommé "Projets" dans le répertoire actuel.

#### Créer plusieurs dossiers en même temps

```bash
mkdir Projets Documents_Travail Archives
```

Crée trois dossiers d'un coup.

#### Créer un dossier avec un chemin absolu

```bash
mkdir /home/utilisateur/Nouveau_Dossier
```

Crée le dossier à un emplacement précis, peu importe où vous êtes.

### Options utiles

#### `-p` : Créer les dossiers parents si nécessaire

C'est l'option la plus importante de `mkdir` !

```bash
mkdir -p Projets/Web/Site2024/Images
```

Cette commande crée toute la structure d'arborescence, même si les dossiers intermédiaires n'existent pas encore.

**Sans `-p` :**
```bash
mkdir Projets/Web/Site2024
# Erreur si "Projets" ou "Web" n'existent pas
```

**Avec `-p` :**
```bash
mkdir -p Projets/Web/Site2024
# Crée Projets, puis Web, puis Site2024 automatiquement
```

#### `-v` : Mode verbeux (afficher ce qui est fait)

```bash
mkdir -v Nouveau_Dossier
# mkdir: création du répertoire 'Nouveau_Dossier'
```

Utile pour confirmer que l'opération a bien eu lieu.

#### Combiner les options

```bash
mkdir -pv Documents/Travail/2024/Rapports
```

Crée toute la structure ET affiche chaque dossier créé.

### Noms de dossiers : Bonnes pratiques

**À éviter :**
- Espaces : `Mes Documents` (complique l'utilisation en ligne de commande)
- Accents : `Données` (peut poser problème sur certains systèmes)
- Caractères spéciaux : `Dossier?` ou `Fichier*`

**À privilégier :**
- Tirets : `mes-documents`
- Underscores : `mes_documents`
- CamelCase : `MesDocuments`
- Minuscules : `documents`

**Si vous devez utiliser des espaces :**
```bash
mkdir "Mes Documents"
# ou
mkdir Mes\ Documents
```

---

## La commande `touch` : Créer des fichiers vides

### Signification

**touch** modifie la date de modification d'un fichier ou crée un fichier vide s'il n'existe pas.

### Utilisation de base

```bash
touch nom_fichier.extension
```

### Exemples

#### Créer un fichier vide

```bash
touch notes.txt
```

Crée un fichier texte vide nommé "notes.txt".

#### Créer plusieurs fichiers

```bash
touch fichier1.txt fichier2.txt fichier3.txt
```

Crée trois fichiers vides d'un coup.

#### Créer des fichiers avec des extensions différentes

```bash
touch index.html style.css script.js
```

Pratique pour initialiser un projet web par exemple.

#### Créer un fichier dans un autre dossier

```bash
touch Documents/rapport_2024.txt
```

**Note :** Le dossier "Documents" doit déjà exister.

### Utilisation avancée : Modifier les dates

Si le fichier existe déjà, `touch` met à jour sa date de modification :

```bash
touch fichier_existant.txt
```

**Pourquoi est-ce utile ?**
- Marquer un fichier comme "récemment modifié"
- Tromper des systèmes qui se basent sur les dates
- Réinitialiser des timestamps

### Créer rapidement une série de fichiers

Avec une boucle bash (plus avancé) :

```bash
touch page{1..10}.html
```

Crée : `page1.html`, `page2.html`, ... jusqu'à `page10.html`

---

## La commande `cp` : Copier des fichiers et dossiers

### Signification

**cp** signifie **Copy** (Copier).

### Utilisation de base

```bash
cp source destination
```

### Exemples de copie de fichiers

#### Copier un fichier dans le même dossier

```bash
cp rapport.txt rapport_copie.txt
```

Crée une copie de "rapport.txt" sous le nom "rapport_copie.txt".

#### Copier un fichier vers un autre dossier

```bash
cp rapport.txt Documents/
```

Copie "rapport.txt" dans le dossier "Documents" en gardant le même nom.

**Note :** Le `/` à la fin indique que c'est un dossier.

#### Copier avec un nouveau nom dans un autre dossier

```bash
cp rapport.txt Documents/rapport_final.txt
```

Copie le fichier ET le renomme en même temps.

#### Copier depuis un autre emplacement

```bash
cp /home/utilisateur/Bureau/photo.jpg ~/Images/
```

**Rappel :** `~` représente votre dossier personnel.

### Copier des dossiers

#### `-r` : Copie récursive (obligatoire pour les dossiers)

```bash
cp -r Projets Projets_Sauvegarde
```

Copie le dossier "Projets" et tout son contenu (fichiers et sous-dossiers).

**Sans `-r`, vous aurez une erreur :**
```bash
cp Projets Projets_Copie
# cp: -r non spécifié; omission du répertoire 'Projets'
```

### Options importantes

#### `-i` : Mode interactif (demander confirmation)

```bash
cp -i fichier.txt Documents/
```

Si "fichier.txt" existe déjà dans Documents, le système demande :
```
cp: écraser 'Documents/fichier.txt' ? (o/n)
```

**Très recommandé pour éviter d'écraser des fichiers par erreur !**

#### `-v` : Mode verbeux (afficher les actions)

```bash
cp -v fichier.txt Documents/
# 'fichier.txt' -> 'Documents/fichier.txt'
```

#### `-u` : Copier seulement si plus récent

```bash
cp -u source.txt destination.txt
```

Ne copie que si le fichier source est plus récent que la destination.

#### `-p` : Préserver les attributs

```bash
cp -p fichier.txt copie.txt
```

Préserve les permissions, dates de modification, propriétaire, etc.

### Copier plusieurs fichiers vers un dossier

```bash
cp fichier1.txt fichier2.txt fichier3.txt Documents/
```

Le dernier argument doit être un dossier.

### Utiliser des jokers (wildcards)

```bash
cp *.txt Documents/          # Tous les fichiers .txt  
cp photo*.jpg Images/        # Tous les jpg commençant par "photo"  
cp rapport_*.pdf Archives/   # Tous les PDF correspondant au motif  
```

### Exemples pratiques combinés

#### Copier un dossier complet avec toutes les options de sécurité

```bash
cp -riv Projet_Important Projet_Important_Backup
```

- `-r` : Récursif (copie tout)
- `-i` : Interactif (demande confirmation)
- `-v` : Verbeux (affiche chaque fichier copié)

---

## La commande `mv` : Déplacer et renommer

### Signification

**mv** signifie **Move** (Déplacer).

### Double fonction

La commande `mv` a deux utilisations principales :
1. **Déplacer** des fichiers/dossiers vers un autre emplacement
2. **Renommer** des fichiers/dossiers

### Utilisation de base

```bash
mv source destination
```

### Renommer un fichier ou un dossier

#### Renommer un fichier

```bash
mv ancien_nom.txt nouveau_nom.txt
```

#### Renommer un dossier

```bash
mv Ancien_Dossier Nouveau_Dossier
```

**Important :** Contrairement à `cp`, `mv` ne nécessite pas l'option `-r` pour les dossiers !

### Déplacer des fichiers

#### Déplacer un fichier vers un autre dossier

```bash
mv fichier.txt Documents/
```

Déplace "fichier.txt" dans le dossier "Documents".

#### Déplacer ET renommer en même temps

```bash
mv rapport.txt Documents/rapport_final.txt
```

Déplace le fichier dans "Documents" et le renomme.

#### Déplacer plusieurs fichiers

```bash
mv fichier1.txt fichier2.txt fichier3.txt Documents/
```

Le dernier argument doit être un dossier.

### Déplacer des dossiers

```bash
mv Projets /home/utilisateur/Archives/
```

Déplace tout le dossier "Projets" (avec son contenu) vers "Archives".

### Options importantes

#### `-i` : Mode interactif

```bash
mv -i fichier.txt Documents/
```

Demande confirmation si un fichier du même nom existe déjà.

#### `-v` : Mode verbeux

```bash
mv -v ancien.txt nouveau.txt
# renommé 'ancien.txt' -> 'nouveau.txt'
```

#### `-u` : Déplacer seulement si plus récent

```bash
mv -u source.txt destination/
```

#### `-n` : Ne pas écraser

```bash
mv -n fichier.txt Documents/
```

Si le fichier existe déjà, l'opération est annulée sans message.

### Utiliser des jokers

```bash
mv *.txt Documents/              # Tous les .txt  
mv photo_2024*.jpg Archives/     # Photos de 2024  
```

### Cas particuliers

#### Déplacer vers le dossier parent

```bash
mv fichier.txt ..
```

Déplace le fichier un niveau au-dessus.

#### Déplacer tout le contenu d'un dossier

```bash
mv Dossier1/* Dossier2/
```

**Attention :** Le `*` ne déplace pas les fichiers cachés (ceux commençant par un point).

Pour tout déplacer (y compris les cachés) :
```bash
mv Dossier1/{*,.*} Dossier2/
```

---

## La commande `rm` : Supprimer des fichiers

### ⚠️ ATTENTION : Danger potentiel !

La commande `rm` est **définitive**. Il n'y a **pas de corbeille**, **pas de retour en arrière** possible !

**Règle d'or :** Réfléchissez toujours deux fois avant d'utiliser `rm`, surtout avec `sudo` ou sur des fichiers importants.

### Signification

**rm** signifie **Remove** (Supprimer).

### Utilisation de base

```bash
rm nom_fichier
```

### Supprimer un fichier

```bash
rm fichier_inutile.txt
```

### Supprimer plusieurs fichiers

```bash
rm fichier1.txt fichier2.txt fichier3.txt
```

### Supprimer avec des jokers

```bash
rm *.tmp              # Tous les fichiers .tmp  
rm temp_*             # Tous les fichiers commençant par "temp_"  
```

**⚠️ Extrême prudence avec les jokers !**

### Supprimer des dossiers

#### `-r` : Suppression récursive (obligatoire pour les dossiers)

```bash
rm -r Dossier_A_Supprimer
```

Supprime le dossier et **tout son contenu** (fichiers et sous-dossiers).

**⚠️ TRÈS DANGEREUX !** Utilisez avec précaution absolue.

### Options de sécurité ESSENTIELLES

#### `-i` : Mode interactif (RECOMMANDÉ)

```bash
rm -i fichier.txt
# rm: supprimer fichier ordinaire 'fichier.txt' ? (o/n)
```

Demande confirmation pour chaque fichier. **Utilisez cette option systématiquement au début !**

#### `-I` : Confirmation pour plus de 3 fichiers

```bash
rm -I *.txt
```

Demande une seule confirmation si vous supprimez plus de 3 fichiers.

#### `-v` : Mode verbeux

```bash
rm -v fichier.txt
# 'fichier.txt' supprimé
```

Affiche ce qui est supprimé.

### Options dangereuses à connaître (pour les éviter !)

#### `-f` : Force (pas de confirmation)

```bash
rm -f fichier.txt
```

Force la suppression sans demander de confirmation. **Ne l'utilisez que si vous savez exactement ce que vous faites !**

#### `-rf` : La combinaison la plus dangereuse

```bash
rm -rf Dossier/
```

Supprime un dossier et tout son contenu, de force, sans confirmation.

**⚠️ DANGER EXTRÊME :**
```bash
# NE JAMAIS FAIRE :
rm -rf /          # Supprimerait tout le système !  
rm -rf /*         # Pareil !  
rm -rf ~          # Supprimerait tout votre dossier personnel !  
```

Heureusement, les systèmes modernes ont des protections contre ces commandes, mais restez vigilant !

### Commande alternative plus sûre : `trash-cli`

Pour avoir une corbeille en ligne de commande, installez `trash-cli` :

```bash
sudo apt install trash-cli
```

Puis utilisez :
```bash
trash fichier.txt          # Envoie à la corbeille  
trash-list                 # Voir la corbeille  
trash-restore             # Restaurer  
trash-empty               # Vider la corbeille  
```

### Bonnes pratiques avec `rm`

1. **Toujours utiliser `-i` au début**
   ```bash
   rm -i fichier.txt
   ```

2. **Vérifier avec `ls` avant de supprimer**
   ```bash
   ls *.txt          # Voir ce qui va être supprimé
   rm -i *.txt       # Puis supprimer
   ```

3. **Créer un alias sécurisé**

   Ajoutez dans `~/.bashrc` :
   ```bash
   alias rm='rm -i'
   ```

   Ainsi, `rm` demandera toujours confirmation.

4. **Faire une sauvegarde avant de supprimer des fichiers importants**
   ```bash
   cp -r Dossier_Important Dossier_Important_Backup
   rm -r Dossier_Important
   ```

5. **Utiliser `trash-cli` pour les suppressions quotidiennes**

---

## La commande `rmdir` : Supprimer des dossiers vides

### Signification

**rmdir** signifie **Remove Directory** (Supprimer un répertoire).

### Utilisation

```bash
rmdir nom_dossier
```

**Important :** `rmdir` ne fonctionne que sur des dossiers **vides**.

### Exemple

```bash
rmdir Vieux_Dossier
```

### Si le dossier n'est pas vide

```bash
rmdir Dossier_Avec_Fichiers
# rmdir: échec de suppression de 'Dossier_Avec_Fichiers': Le dossier n'est pas vide
```

**Solution :** Utilisez `rm -r` (avec prudence !) pour supprimer un dossier non vide.

### Pourquoi utiliser `rmdir` ?

C'est une sécurité supplémentaire : si vous pensez qu'un dossier est vide mais qu'il ne l'est pas, `rmdir` échouera sans rien supprimer.

---

## Techniques avancées et astuces

### Créer une structure de projet complexe

```bash
mkdir -p MonProjet/{src,docs,tests,config}
```

Crée :
```
MonProjet/
├── src/
├── docs/
├── tests/
└── config/
```

### Créer une structure avec des sous-niveaux

```bash
mkdir -p Site/{css,js,images/{logos,photos},pages}
```

Crée une structure complète pour un site web.

### Copier avec barre de progression (pour gros fichiers)

Installez `rsync` :
```bash
sudo apt install rsync
```

Puis :
```bash
rsync -ah --progress source.iso destination/
```

### Renommer en masse avec `rename`

Installez `rename` :
```bash
sudo apt install rename
```

Exemples :
```bash
rename 's/\.txt$/.md/' *.txt        # Change .txt en .md  
rename 'y/A-Z/a-z/' *               # Tout en minuscules  
rename 's/ /_/g' *                  # Remplace espaces par underscores  
```

### Déplacer en gardant la structure

```bash
cp -r --parents Documents/Projets/Web /media/backup/
```

Recrée la structure complète `Documents/Projets/Web` dans `/media/backup/`.

---

## Combinaisons de commandes utiles

### Créer et entrer dans un dossier

```bash
mkdir NouveauProjet && cd NouveauProjet
```

Le `&&` exécute la deuxième commande seulement si la première réussit.

### Créer une structure et des fichiers

```bash
mkdir -p Projet/{src,docs} && touch Projet/src/main.py Projet/docs/readme.md
```

### Copier puis vérifier

```bash
cp fichier.txt backup/ && ls -l backup/
```

### Sauvegarder avant de supprimer

```bash
cp -r Dossier Dossier_backup && rm -r Dossier
```

---

## Comparaison avec l'interface graphique

| Action | Interface graphique | Terminal |
|--------|-------------------|----------|
| Créer un dossier | Clic droit → Nouveau dossier | `mkdir NomDossier` |
| Créer un fichier | Clic droit → Nouveau fichier | `touch fichier.txt` |
| Copier | Ctrl+C puis Ctrl+V | `cp source dest` |
| Déplacer | Glisser-déposer | `mv source dest` |
| Renommer | Clic droit → Renommer | `mv ancien nouveau` |
| Supprimer | Suppr (va à la corbeille) | `rm fichier` (définitif !) |

---

## Erreurs courantes et solutions

### Erreur 1 : Permission refusée

**Problème :**
```bash
mkdir /etc/MonDossier
# mkdir: impossible de créer le répertoire '/etc/MonDossier': Permission non accordée
```

**Solutions :**
- Utilisez `sudo` pour les dossiers système (avec prudence !)
- Créez dans votre dossier personnel : `mkdir ~/MonDossier`

### Erreur 2 : Le fichier existe déjà

**Problème :**
```bash
mkdir Projets
# mkdir: impossible de créer le répertoire 'Projets': Le fichier existe
```

**Solutions :**
- Vérifiez avec `ls`
- Choisissez un autre nom
- Utilisez `mkdir -p` (ne génère pas d'erreur si le dossier existe)

### Erreur 3 : Dossier non vide

**Problème :**
```bash
rmdir Projets
# rmdir: échec de suppression de 'Projets': Le dossier n'est pas vide
```

**Solution :**
```bash
rm -ri Projets    # Avec confirmation pour chaque fichier
```

### Erreur 4 : Écraser accidentellement un fichier

**Problème :**
```bash
cp fichier.txt Documents/
# Le fichier dans Documents est écrasé sans avertissement
```

**Solutions :**
- Utilisez toujours `-i` : `cp -i fichier.txt Documents/`
- Créez un alias dans `~/.bashrc` : `alias cp='cp -i'`

### Erreur 5 : Caractères spéciaux dans les noms

**Problème :**
```bash
mkdir Mes Documents
# Crée deux dossiers : "Mes" et "Documents"
```

**Solutions :**
```bash
mkdir "Mes Documents"
# ou
mkdir Mes\ Documents
```

---

## Récapitulatif des commandes essentielles

### Création

| Commande | Action | Exemple |
|----------|--------|---------|
| `mkdir` | Créer un dossier | `mkdir Projets` |
| `mkdir -p` | Créer avec parents | `mkdir -p A/B/C` |
| `touch` | Créer un fichier vide | `touch notes.txt` |

### Copie

| Commande | Action | Exemple |
|----------|--------|---------|
| `cp fichier dest` | Copier un fichier | `cp a.txt b.txt` |
| `cp -r dossier dest` | Copier un dossier | `cp -r Dir1 Dir2` |
| `cp -i` | Copie interactive | `cp -i a.txt b.txt` |

### Déplacement/Renommage

| Commande | Action | Exemple |
|----------|--------|---------|
| `mv ancien nouveau` | Renommer | `mv old.txt new.txt` |
| `mv fichier dossier/` | Déplacer | `mv a.txt Docs/` |
| `mv -i` | Déplacement interactif | `mv -i a.txt Docs/` |

### Suppression

| Commande | Action | Exemple |
|----------|--------|---------|
| `rm fichier` | Supprimer un fichier | `rm old.txt` |
| `rm -r dossier` | Supprimer un dossier | `rm -r OldDir` |
| `rm -i` | Suppression interactive | `rm -i *.txt` |
| `rmdir` | Supprimer dossier vide | `rmdir Empty/` |

---

## Options à retenir absolument

### Pour la sécurité (à utiliser systématiquement)

- **`-i`** : Mode interactif, demande confirmation
- **`-v`** : Mode verbeux, affiche ce qui se passe

### Pour la puissance (à utiliser avec précaution)

- **`-r`** : Récursif (pour les dossiers)
- **`-f`** : Force (pas de confirmation) - **DANGEREUX**
- **`-p`** : Créer les parents si nécessaire (mkdir)

---

## Conseils finaux

### 1. Créez des alias dans ~/.bashrc

```bash
alias rm='rm -i'  
alias cp='cp -i'  
alias mv='mv -i'  
```

Rechargez avec : `source ~/.bashrc`

### 2. Testez d'abord avec `ls`

Avant de supprimer ou déplacer avec des jokers :
```bash
ls *.txt          # Voir ce qui correspond  
rm -i *.txt       # Puis supprimer  
```

### 3. Faites des sauvegardes

Avant toute opération importante :
```bash
cp -r DossierImportant DossierImportant_backup_$(date +%Y%m%d)
```

Le `$(date +%Y%m%d)` ajoute la date au nom de la sauvegarde.

### 4. Utilisez Tab pour éviter les erreurs

La complétion automatique évite les fautes de frappe dans les noms de fichiers.

### 5. Soyez particulièrement prudent avec :

- `rm -rf` (suppression récursive forcée)
- Les jokers `*` avec `rm`
- Les commandes avec `sudo`
- Les opérations sur `/etc`, `/usr`, `/var`

---

## Résumé

Vous connaissez maintenant les cinq commandes fondamentales de manipulation :

- **`mkdir`** : Créer des dossiers
- **`touch`** : Créer des fichiers vides
- **`cp`** : Copier
- **`mv`** : Déplacer/Renommer
- **`rm`** : Supprimer (avec prudence !)

**Checklist de sécurité :**
- ✅ Utilisez `-i` pour les confirmations
- ✅ Vérifiez avec `ls` avant `rm`
- ✅ Faites des backups des données importantes
- ✅ Utilisez `trash-cli` pour une corbeille
- ✅ Créez des alias sécurisés
- ✅ Réfléchissez deux fois avant `rm -rf`

**La pratique rend parfait :** Commencez par des opérations simples dans votre dossier personnel, utilisez toujours l'option `-i`, et vous gagnerez progressivement en confiance.

Dans le prochain chapitre, nous verrons les commandes d'affichage et de recherche pour explorer le contenu de vos fichiers sans les modifier.

⏭️ [Affichage et recherche (cat, less, head, tail, grep, find)](/07-le-terminal-et-commandes-de-base/04-affichage-et-recherche.md)
