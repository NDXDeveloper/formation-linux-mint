🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 17.2 Sauvegarde de données (Déjà Dup, Backintime, rsync)

## Introduction

Alors que Timeshift protège votre système d'exploitation, la sauvegarde de vos données personnelles est tout aussi cruciale. Vos photos, documents, vidéos et fichiers de travail ne sont pas couverts par Timeshift et nécessitent leur propre stratégie de sauvegarde.

### Pourquoi sauvegarder vos données ?

Vos données peuvent être perdues à cause de :
- Une panne matérielle (disque dur défaillant)
- Une suppression accidentelle
- Un virus ou ransomware
- Un vol ou un sinistre (incendie, dégât des eaux)
- Une corruption de fichiers
- Une fausse manipulation

**Règle d'or** : Si un fichier n'existe qu'à un seul endroit, il n'existe pas vraiment. Une bonne sauvegarde vous permet de dormir tranquille.

### Différence avec Timeshift

| Timeshift | Sauvegarde de données |
|-----------|----------------------|
| Sauvegarde le système | Sauvegarde vos fichiers personnels |
| Protège Linux Mint lui-même | Protège /home (documents, photos, etc.) |
| Restauration du système | Restauration de fichiers spécifiques |
| Snapshots du système | Sauvegardes de données |

Les deux sont complémentaires et nécessaires pour une protection complète !

## Déjà Dup : La solution simple et efficace

Déjà Dup est l'outil de sauvegarde graphique le plus simple pour les débutants sous Linux Mint. Son interface est intuitive et il fait le travail sans complications.

### Installation de Déjà Dup

Déjà Dup n'est pas toujours préinstallé, mais son installation est très simple :

**Via le gestionnaire de logiciels :**
1. Ouvrez le Gestionnaire de logiciels
2. Recherchez "Déjà Dup" ou "Backups"
3. Cliquez sur "Installer"

**Via le terminal :**
```bash
sudo apt update  
sudo apt install deja-dup  
```

### Premier lancement et configuration

1. Ouvrez le Menu principal et cherchez "Sauvegardes" ou "Backups"
2. Au premier lancement, vous verrez une interface simple

#### Configuration de la sauvegarde

**1. Onglet "Aperçu"**

C'est ici que vous lancez les sauvegardes et restaurations.

**2. Dossiers à sauvegarder**

Par défaut, Déjà Dup sauvegarde tout votre dossier personnel (/home/votrenom). Vous pouvez :

- **Ajouter des dossiers** : Si vous avez des données ailleurs (disque externe, autre partition)
- **Ignorer des dossiers** : Pour exclure des dossiers volumineux ou inutiles

**Dossiers couramment exclus :**
- `~/.cache` (fichiers temporaires)
- `~/Téléchargements` (si vous ne voulez pas sauvegarder tout)
- `~/.local/share/Trash` (corbeille)
- Dossiers de jeux ou logiciels facilement réinstallables

**3. Emplacement de stockage**

Choisissez où stocker vos sauvegardes :

- **Disque dur local** : Simple mais pas sûr si le disque tombe en panne
- **Disque externe** : Recommandé pour les sauvegardes locales
- **Serveur réseau** : Si vous avez un NAS ou serveur domestique
- **Cloud** : Google Drive, Nextcloud, etc. (nécessite une connexion Internet)

**Conseil pour débutants** : Utilisez un disque dur externe USB dédié aux sauvegardes.

**4. Planification automatique**

Activez les sauvegardes automatiques :
- **Quotidienne** : Pour des données qui changent souvent
- **Hebdomadaire** : Pour un usage normal
- **Mensuelle** : Si vos données changent peu

Choisissez aussi la durée de conservation :
- Au moins 6 mois : Recommandé
- 1 an ou plus : Idéal pour garder un historique long

### Créer votre première sauvegarde

1. Dans l'onglet "Aperçu", cliquez sur **"Sauvegarder maintenant"**
2. Si c'est la première fois, vous devrez choisir un mot de passe de chiffrement (optionnel mais recommandé)
3. La sauvegarde démarre. La première peut prendre du temps selon la quantité de données
4. Une notification vous informera quand c'est terminé

**Note** : Les sauvegardes suivantes seront beaucoup plus rapides car seuls les fichiers modifiés seront copiés.

### Restaurer vos fichiers

Si vous devez récupérer des fichiers :

**Pour restaurer des fichiers spécifiques :**
1. Ouvrez Déjà Dup
2. Cliquez sur **"Restaurer"**
3. Choisissez la date de la sauvegarde
4. Sélectionnez les fichiers à restaurer
5. Choisissez l'emplacement de restauration

**Pour restaurer tout :**
1. Même procédure mais cochez "Restaurer tout"
2. Les fichiers seront restaurés à leur emplacement d'origine

### Avantages et limites de Déjà Dup

**Avantages :**
- Interface très simple
- Sauvegardes incrémentales automatiques
- Chiffrement des données
- Supporte le cloud
- Parfait pour les débutants

**Limites :**
- Moins de contrôle avancé
- Interface basique
- Pas de synchronisation bidirectionnelle

## Backintime : Plus de contrôle et de fonctionnalités

Backintime est une solution plus complète que Déjà Dup, offrant plus d'options tout en restant accessible via une interface graphique.

### Installation de Backintime

```bash
sudo apt update  
sudo apt install backintime-qt  
```

Note : `backintime-qt` inclut l'interface graphique. Il existe aussi `backintime-gnome` pour GNOME.

### Configuration initiale

1. Lancez Backintime depuis le menu (cherchez "Back In Time")
2. L'assistant de configuration s'ouvre automatiquement

#### Étape 1 : Emplacement de sauvegarde

Choisissez où stocker vos snapshots :
- Un disque externe (recommandé)
- Une partition séparée
- Un dossier réseau

**Important** : Assurez-vous que l'emplacement a assez d'espace.

#### Étape 2 : Planification

Définissez la fréquence des sauvegardes :
- Toutes les heures
- Tous les jours
- Toutes les semaines
- Tous les mois
- Personnalisé

**Recommandation** : Quotidien à 2h du matin si votre ordinateur reste allumé la nuit, sinon "À chaque démarrage".

#### Étape 3 : Inclusion/Exclusion

**Dossiers à inclure :**
- Par défaut, votre dossier personnel est sélectionné
- Ajoutez d'autres dossiers si nécessaire

**Exclusions automatiques :**
Backintime propose des exclusions intelligentes :
- Fichiers cache
- Fichiers temporaires
- Corbeille
- Fichiers de sauvegarde (fichiers se terminant par ~)

Vous pouvez ajouter vos propres exclusions :
```
~/Téléchargements/*
*.tmp
*.cache
~/.steam
```

#### Étape 4 : Suppression automatique

Configurez la rétention des anciennes sauvegardes :
- Garder toutes les sauvegardes du dernier mois
- Une par semaine pour le mois précédent
- Une par mois pour les mois plus anciens

Cela économise de l'espace tout en gardant un historique.

### Utilisation de Backintime

#### Créer une sauvegarde manuelle

1. Ouvrez Backintime
2. Cliquez sur **"Take Snapshot"** (Créer un instantané)
3. Attendez la fin du processus
4. Le nouveau snapshot apparaît dans la liste

#### Explorer vos sauvegardes

L'interface principale montre :
- **À gauche** : La liste des snapshots avec date et heure
- **À droite** : Les fichiers de chaque snapshot

Vous pouvez naviguer comme dans un explorateur de fichiers normal.

#### Restaurer des fichiers

**Méthode 1 : Restauration simple**
1. Sélectionnez le snapshot contenant le fichier
2. Naviguez jusqu'au fichier
3. Clic droit sur le fichier
4. Choisissez "Restaurer"

**Méthode 2 : Restauration avec options**
1. Sélectionnez les fichiers à restaurer
2. Cliquez sur "Restore" dans la barre d'outils
3. Choisissez les options :
   - Restaurer à l'emplacement original
   - Restaurer vers un autre emplacement
   - Ne pas écraser les fichiers existants

#### Comparer les versions

Backintime permet de comparer différentes versions d'un fichier :
1. Sélectionnez le fichier
2. Cliquez sur "Snapshots" → "View Snapshot Log"
3. Vous voyez toutes les versions du fichier
4. Vous pouvez les ouvrir et comparer

### Fonctionnalités avancées de Backintime

#### Profils multiples

Vous pouvez créer plusieurs profils de sauvegarde :
- Un pour les documents de travail (quotidien)
- Un pour les photos (hebdomadaire)
- Un pour les projets (manuel)

#### Notifications

Backintime peut vous notifier :
- Quand une sauvegarde réussit
- Quand une sauvegarde échoue
- Quand l'espace disque est faible

#### Mode Expert

Pour les utilisateurs avancés, le mode Expert permet :
- Des exclusions plus complexes
- Des scripts avant/après sauvegarde
- Des options rsync personnalisées

### Avantages et limites de Backintime

**Avantages :**
- Interface claire et puissante
- Gestion fine des versions
- Comparaison de fichiers
- Profils multiples
- Visualisation facile de l'historique

**Limites :**
- Ne supporte pas le cloud directement
- Un peu plus complexe que Déjà Dup
- Nécessite un disque local ou réseau

## rsync : La sauvegarde en ligne de commande

rsync est l'outil de sauvegarde le plus puissant et flexible sous Linux. Il fonctionne en ligne de commande, ce qui peut sembler intimidant, mais offre un contrôle total.

### Qu'est-ce que rsync ?

rsync (remote sync) est un outil qui synchronise des fichiers et dossiers :
- Copie uniquement les différences (très rapide)
- Préserve les permissions et propriétés
- Peut travailler en local ou à distance (SSH)
- Extrêmement fiable et éprouvé

### Installation de rsync

rsync est généralement préinstallé. Sinon :

```bash
sudo apt update  
sudo apt install rsync  
```

### Syntaxe de base

La syntaxe générale de rsync est :
```bash
rsync [options] source destination
```

### Exemples pratiques pour débutants

#### 1. Sauvegarde simple d'un dossier

Sauvegarder votre dossier Documents vers un disque externe :

```bash
rsync -av ~/Documents /media/votrenom/DisqueExterne/Sauvegarde/
```

**Explication :**
- `-a` : Mode archive (préserve tout : permissions, dates, etc.)
- `-v` : Mode verbeux (affiche ce qui est copié)
- `~/Documents` : Source (votre dossier Documents)
- `/media/...` : Destination (le disque externe)

#### 2. Sauvegarde avec barre de progression

Pour voir la progression :

```bash
rsync -av --progress ~/Documents /media/votrenom/DisqueExterne/Sauvegarde/
```

L'option `--progress` affiche l'avancement de chaque fichier.

#### 3. Sauvegarde avec suppression des fichiers obsolètes

Pour que la destination soit exactement comme la source :

```bash
rsync -av --delete ~/Documents /media/votrenom/DisqueExterne/Sauvegarde/
```

**Attention** : `--delete` supprime dans la destination les fichiers qui n'existent plus dans la source. Utilisez avec précaution !

#### 4. Sauvegarde en excluant certains fichiers

Pour exclure des types de fichiers :

```bash
rsync -av --exclude='*.tmp' --exclude='*.cache' ~/Documents /media/votrenom/DisqueExterne/Sauvegarde/
```

#### 5. Mode "dry-run" (simulation)

Pour voir ce qui serait copié sans rien faire réellement :

```bash
rsync -av --dry-run ~/Documents /media/votrenom/DisqueExterne/Sauvegarde/
```

C'est très utile pour vérifier avant une vraie sauvegarde !

#### 6. Sauvegarde complète du dossier personnel

Pour sauvegarder tout votre /home en excluant les fichiers inutiles :

```bash
rsync -av \
  --exclude='.cache' \
  --exclude='.local/share/Trash' \
  --exclude='Téléchargements' \
  --exclude='.steam' \
  ~/  /media/votrenom/DisqueExterne/Sauvegarde/home/
```

Le `\` permet de continuer la commande sur plusieurs lignes pour plus de lisibilité.

### Options utiles de rsync

| Option | Description |
|--------|-------------|
| `-a` | Mode archive (recommandé) |
| `-v` | Affiche les détails |
| `-h` | Format lisible (tailles en Ko, Mo, Go) |
| `--progress` | Barre de progression |
| `--delete` | Supprime les fichiers absents de la source |
| `--exclude` | Exclut des fichiers ou dossiers |
| `-z` | Compression pendant le transfert |
| `--dry-run` | Simulation sans modification |
| `-n` | Équivalent de --dry-run |

### Créer un script de sauvegarde

Pour ne pas retaper la commande à chaque fois, créez un script :

1. Créez un fichier :
```bash
nano ~/sauvegarde.sh
```

2. Ajoutez votre commande rsync :
```bash
#!/bin/bash

# Script de sauvegarde automatique
echo "Début de la sauvegarde..."  
rsync -avh --progress \  
  --exclude='.cache' \
  --exclude='.local/share/Trash' \
  --exclude='Téléchargements' \
  ~/  /media/votrenom/DisqueExterne/Sauvegarde/

echo "Sauvegarde terminée !"
```

3. Rendez-le exécutable :
```bash
chmod +x ~/sauvegarde.sh
```

4. Lancez-le quand vous voulez :
```bash
~/sauvegarde.sh
```

### Automatiser avec cron

Pour que rsync s'exécute automatiquement chaque jour :

```bash
crontab -e
```

Ajoutez cette ligne pour une sauvegarde tous les jours à 2h du matin :
```
0 2 * * * /home/votrenom/sauvegarde.sh
```

### Avantages et limites de rsync

**Avantages :**
- Extrêmement rapide et efficace
- Contrôle total sur la sauvegarde
- Très flexible
- Peut sauvegarder à distance via SSH
- Scriptable et automatisable
- Gratuit et open source

**Limites :**
- Ligne de commande (peut être intimidant)
- Pas d'interface graphique native
- Nécessite un peu d'apprentissage
- Pas de gestion automatique des versions multiples

## Comparaison des trois outils

| Critère | Déjà Dup | Backintime | rsync |
|---------|----------|------------|-------|
| Facilité | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ |
| Interface | Graphique simple | Graphique complète | Ligne de commande |
| Versions multiples | Oui | Oui | Non (sauf script) |
| Cloud | Oui | Non | Via rclone |
| Contrôle | Basique | Avancé | Total |
| Automatisation | Oui | Oui | Cron/scripts |
| Idéal pour | Débutants | Utilisateurs confirmés | Experts/scripts |

## Stratégies de sauvegarde recommandées

### Pour un utilisateur débutant

**Configuration simple :**
- **Déjà Dup** pour sauvegardes automatiques quotidiennes sur disque externe
- **Cloud** (Google Drive, Nextcloud) pour documents importants
- **Timeshift** pour le système (comme vu précédemment)

### Pour un utilisateur intermédiaire

**Configuration complète :**
- **Backintime** pour sauvegardes locales avec historique
- **Déjà Dup** vers le cloud pour redondance
- **Disque externe** déconnecté et rangé en sécurité
- **Timeshift** pour le système

### Pour un utilisateur avancé

**Configuration personnalisée :**
- **Scripts rsync** pour sauvegardes locales
- **rsync + SSH** vers un serveur distant
- **rclone** pour synchronisation cloud
- **ZFS ou Btrfs snapshots** pour versioning avancé
- **Timeshift** pour le système

## La règle 3-2-1

Une bonne stratégie de sauvegarde suit la règle 3-2-1 :

- **3** copies de vos données (original + 2 sauvegardes)
- Sur **2** supports différents (disque interne + externe, par exemple)
- Dont **1** hors site (cloud, chez un ami, au bureau)

**Exemple d'application :**
1. Données originales sur votre ordinateur
2. Sauvegarde 1 : disque externe avec Backintime
3. Sauvegarde 2 : cloud avec Déjà Dup ou Nextcloud

## Conseils pratiques

### Fréquence de sauvegarde

- **Quotidien** : Pour travail important ou données qui changent beaucoup
- **Hebdomadaire** : Pour usage normal
- **Mensuel** : Pour archives ou données peu modifiées
- **Avant chaque modification importante** : Sauvegarde manuelle

### Tester vos sauvegardes

**Important** : Une sauvegarde non testée n'est pas une vraie sauvegarde !

- Testez la restauration de quelques fichiers régulièrement
- Vérifiez que les sauvegardes automatiques se font bien
- Assurez-vous d'avoir assez d'espace disque
- Vérifiez l'intégrité des sauvegardes anciennes

### Sécurité des sauvegardes

- Chiffrez vos sauvegardes si elles contiennent des données sensibles
- Stockez au moins une sauvegarde hors site
- Protégez vos disques de sauvegarde physiquement
- Utilisez des mots de passe forts pour les sauvegardes chiffrées

### Rotation des supports

Si vous utilisez plusieurs disques externes :
- Alternez entre 2 ou 3 disques
- Gardez-en un déconnecté et en lieu sûr
- Testez-les régulièrement

## Que sauvegarder ?

### Données essentielles à sauvegarder

- Documents personnels et professionnels
- Photos et vidéos
- Projets en cours
- Fichiers de configuration personnalisés
- Marque-pages du navigateur
- Mots de passe (si non dans un gestionnaire cloud)
- Emails (si client local)
- Fichiers de jeux (sauvegardes de progression)

### Données inutiles à sauvegarder

- Fichiers temporaires et cache
- Téléchargements (sauf si importants)
- Fichiers système (couverts par Timeshift)
- Logiciels installés (réinstallables)
- Fichiers de grande taille facilement récupérables

## En résumé

La sauvegarde de données est essentielle et complémentaire à Timeshift :

**Pour débuter :**
- Utilisez Déjà Dup pour sa simplicité
- Sauvegardez sur un disque externe
- Activez les sauvegardes automatiques quotidiennes ou hebdomadaires

**Pour aller plus loin :**
- Essayez Backintime pour plus de contrôle
- Apprenez rsync pour des scripts personnalisés
- Mettez en place la règle 3-2-1

**N'oubliez jamais :**
- Testez vos sauvegardes régulièrement
- Automatisez au maximum
- Gardez au moins une copie hors site
- "Pas de sauvegarde = accepter de tout perdre"

Avec une bonne stratégie de sauvegarde en place, vous pouvez utiliser votre ordinateur l'esprit tranquille, sachant que vos précieuses données sont protégées !

⏭️ [Clonage de disque (Clonezilla, dd)](/17-sauvegarde-et-restauration/03-clonage-de-disque.md)
