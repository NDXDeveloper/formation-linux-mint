🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6 Gestionnaire d'archives

## Introduction

Un gestionnaire d'archives permet de **compresser** (réduire la taille) et **regrouper** plusieurs fichiers en un seul fichier archive, facilitant ainsi le stockage et le partage. Linux Mint inclut un gestionnaire d'archives graphique qui supporte tous les formats courants : ZIP, RAR, 7Z, TAR, et bien d'autres.

## Qu'est-ce qu'une archive ?

### Définition

Une **archive** est un fichier unique contenant un ou plusieurs fichiers et dossiers, généralement compressés pour économiser de l'espace.

**Exemple** :
- Vous avez un dossier `Vacances` avec 100 photos (500 Mo)
- Vous créez une archive `Vacances.zip` (350 Mo)
- Vous partagez un seul fichier au lieu de 100
- Le destinataire extrait l'archive pour retrouver tous les fichiers

### Différence compression vs archivage

**Archivage** :
- Regroupe plusieurs fichiers en un seul
- Facilite le transport et l'organisation
- Ne réduit pas forcément la taille

**Compression** :
- Réduit la taille des fichiers
- Économise de l'espace disque
- Accélère les transferts

**En pratique** : La plupart des formats modernes font les deux simultanément.

### Pourquoi utiliser des archives ?

**Avantages** :
- **Économie d'espace** : Fichiers plus petits
- **Partage facilité** : Un seul fichier à envoyer
- **Organisation** : Regroupement logique
- **Sauvegarde** : Conservation à long terme
- **Protection** : Possibilité de chiffrement par mot de passe

**Cas d'usage courants** :
- Envoyer plusieurs documents par email
- Sauvegarder des projets
- Télécharger des logiciels
- Archiver des anciennes données
- Partager des collections de photos

## Formats d'archives

### Formats courants

#### ZIP (.zip)

**Caractéristiques** :
- **Le plus universel** : Compatible partout (Windows, Mac, Linux)
- **Compression moyenne** : Équilibre taille/vitesse
- **Mot de passe** : Supporté
- **Multifichiers** : Oui

**Utilisation** :
- Partage général
- Email
- Web
- Compatibilité maximale

**Niveau de compression** : Moyen (ratio ~ 40-60%)

#### RAR (.rar)

**Caractéristiques** :
- **Propriétaire** : Format WinRAR
- **Bonne compression** : Meilleure que ZIP
- **Mot de passe** : Supporté
- **Archives fragmentées** : Découpage en parties (.part1.rar, .part2.rar)

**Utilisation** :
- Téléchargements Internet
- Gros fichiers découpés
- Windows principalement

**Note** : Linux peut **extraire** les RAR mais nécessite des outils spécifiques pour **créer**

**Niveau de compression** : Bon (ratio ~ 50-70%)

#### 7Z (.7z)

**Caractéristiques** :
- **Libre et gratuit** : Format 7-Zip
- **Excellente compression** : Meilleure que ZIP et RAR
- **Mot de passe** : Supporté avec chiffrement AES-256
- **Lent** : Plus long à compresser

**Utilisation** :
- Archivage à long terme
- Économie maximale d'espace
- Moins universel que ZIP

**Niveau de compression** : Excellent (ratio ~ 60-80%)

#### TAR (.tar)

**Caractéristiques** :
- **Archivage pur** : Pas de compression par défaut
- **Unix/Linux** : Standard sur systèmes Unix
- **Préserve permissions** : Droits, propriétaires

**Utilisation** :
- Sauvegardes système Linux
- Distribution de code source
- Combiné avec compression (tar.gz, tar.bz2)

**Niveau de compression** : Aucun (archivage seulement)

#### GZIP (.gz) et BZIP2 (.bz2)

**Caractéristiques** :
- **Compression** : Algorithmes de compression
- **Fichier unique** : Compresse un seul fichier à la fois
- **Utilisé avec TAR** : .tar.gz, .tar.bz2

**Différences** :
- **GZIP (.gz)** : Rapide, compression moyenne
- **BZIP2 (.bz2)** : Lent, meilleure compression
- **XZ (.xz)** : Très lent, excellente compression

**Utilisation** :
- Archives Linux (.tar.gz, .tar.bz2, .tar.xz)
- Code source
- Paquets logiciels

#### Autres formats

**ISO (.iso)** :
- Image de disque (CD/DVD)
- Montable comme un disque virtuel

**DEB (.deb)** et **RPM (.rpm)** :
- Paquets logiciels Linux
- En réalité des archives spéciales

**CAB (.cab)** :
- Format Microsoft
- Rare sur Linux

### Tableau comparatif

| Format | Compression | Vitesse | Universalité | Recommandation |
|--------|-------------|---------|--------------|----------------|
| **ZIP** | Moyenne | Rapide | Maximale | Partage général |
| **7Z** | Excellente | Lente | Moyenne | Archivage |
| **RAR** | Bonne | Moyenne | Bonne | Extraction uniquement |
| **TAR.GZ** | Bonne | Rapide | Linux/Unix | Code source |
| **TAR.BZ2** | Très bonne | Lente | Linux/Unix | Archivage Linux |
| **TAR.XZ** | Excellente | Très lente | Linux/Unix | Distribution |

### Choisir le bon format

**Pour partager avec tout le monde** : **ZIP**
- Compatible Windows, Mac, Linux, mobiles
- Universel

**Pour économiser un maximum d'espace** : **7Z**
- Meilleure compression
- Acceptable sur la plupart des systèmes modernes

**Pour sauvegardes Linux** : **TAR.GZ** ou **TAR.XZ**
- Préserve les permissions
- Standard Linux

**Pour recevoir des fichiers** :
- Tout format est lisible sur Linux Mint !

## Gestionnaire d'archives graphique

### File Roller (Archive Manager)

Linux Mint utilise **File Roller** (aussi appelé **Archive Manager** ou **Gestionnaire d'archives**), un outil graphique simple et efficace.

#### Lancer le gestionnaire d'archives

**Méthode 1 - Double-clic sur une archive** :
1. Ouvrez le gestionnaire de fichiers (Nemo)
2. Naviguez vers une archive (.zip, .rar, etc.)
3. Double-cliquez
4. Le gestionnaire d'archives s'ouvre

**Méthode 2 - Menu** :
1. Menu principal → **Accessoires** → **Gestionnaire d'archives**
2. Ou tapez "archive" dans la recherche

**Méthode 3 - Créer une archive** :
1. Clic droit sur des fichiers/dossiers
2. **Compresser**
3. Le gestionnaire s'ouvre

#### Interface du gestionnaire

**Barre de menus** :
- Archive, Édition, Affichage, Aide

**Barre d'outils** :
- Créer, Extraire, Tester, Propriétés
- Précédent/Suivant (navigation dans les dossiers de l'archive)

**Zone de contenu** :
- Liste des fichiers et dossiers dans l'archive
- Double-clic pour naviguer dans les dossiers

**Barre d'état** :
- Nombre de fichiers
- Taille totale / Taille compressée
- Taux de compression

## Extraire (décompresser) des archives

### Méthode simple - Clic droit

**La plus rapide pour les débutants** :

1. Clic droit sur l'archive (exemple : `fichiers.zip`)
2. **Extraire ici** : Extrait dans le dossier actuel
3. Ou **Extraire vers...** : Choisissez la destination

**Différence** :
- **Extraire ici** : Les fichiers apparaissent à côté de l'archive
- **Extraire vers...** : Vous choisissez où

**Conseil** : Si l'archive contient beaucoup de fichiers sans dossier parent, créez d'abord un dossier ou utilisez "Extraire vers..."

### Méthode avancée - Gestionnaire d'archives

**Plus de contrôle** :

1. Double-cliquez sur l'archive
2. Le gestionnaire d'archives s'ouvre
3. Parcourez le contenu
4. **Archive** → **Extraire**
5. Ou cliquez sur le bouton **Extraire** dans la barre d'outils
6. Choisissez la destination
7. Options :
   - **Tous les fichiers** : Tout extraire
   - **Fichiers sélectionnés** : Seulement certains
   - **Garder la structure** : Préserve les dossiers
   - **Recréer les dossiers** : Oui/Non
8. Cliquez sur **Extraire**

### Extraire seulement certains fichiers

**Si vous ne voulez pas tout extraire** :

1. Ouvrez l'archive dans le gestionnaire
2. Naviguez jusqu'aux fichiers souhaités
3. Sélectionnez-les (Ctrl + clic pour sélection multiple)
4. Clic droit → **Extraire**
5. Ou glissez-déposez vers un dossier du gestionnaire de fichiers

### Visualiser sans extraire

**Aperçu rapide** :

1. Double-cliquez sur l'archive
2. Naviguez dans les dossiers
3. Double-cliquez sur un fichier texte ou image
4. Il s'ouvre temporairement sans extraction complète

**Utile pour** :
- Vérifier le contenu avant extraction
- Lire un README.txt
- Consulter une documentation

### Archives protégées par mot de passe

**Si l'archive est chiffrée** :

1. Tentez d'extraire normalement
2. Une fenêtre demande le mot de passe
3. Entrez le mot de passe
4. Cliquez sur **OK**
5. L'extraction démarre

**Si vous ne connaissez pas le mot de passe** :
- Impossible d'extraire (sauf attaque par force brute, très long)
- Contactez l'expéditeur

### Archives multi-parties (fragmentées)

**Format RAR multi-parties** : `fichier.part1.rar`, `fichier.part2.rar`, etc.

**Extraction** :
1. Assurez-vous d'avoir **toutes les parties** dans le même dossier
2. Ouvrez ou extrayez **seulement la première partie** (.part1.rar)
3. Le gestionnaire reconstruit automatiquement l'archive complète
4. Extrait tout le contenu

**Ne pas** :
- Extraire chaque partie séparément
- Renommer les parties

## Créer des archives

### Méthode rapide - Clic droit

**Depuis le gestionnaire de fichiers** :

1. Sélectionnez les fichiers et/ou dossiers à archiver
2. Clic droit → **Compresser**
3. Une fenêtre s'ouvre :
   - **Nom du fichier** : Nom de l'archive
   - **Format** : ZIP, TAR.GZ, 7Z, etc.
   - **Emplacement** : Où créer l'archive
   - **Options** (selon format) : Mot de passe, niveau de compression
4. Cliquez sur **Créer**

**Exemple** :
- Sélectionnez le dossier `Documents-2024`
- Clic droit → **Compresser**
- Format : **ZIP**
- Nom : `Documents-2024.zip`
- **Créer**

### Méthode avancée - Gestionnaire d'archives

**Plus d'options** :

1. Ouvrez le **Gestionnaire d'archives**
2. **Archive** → **Nouvelle**
3. Ou cliquez sur **Nouveau** dans la barre d'outils
4. Choisissez :
   - **Nom** : `mon-archive.zip`
   - **Format** : Sélectionnez dans la liste déroulante
5. Cliquez sur **Nouveau**
6. Une archive vide s'ouvre
7. Ajoutez des fichiers :
   - Bouton **Ajouter**
   - Ou glissez-déposez depuis le gestionnaire de fichiers
8. **Archive** → **Enregistrer** ou fermez (enregistrement automatique)

### Ajouter des fichiers à une archive existante

**Compléter une archive** :

1. Ouvrez l'archive existante
2. Bouton **Ajouter** ou **Édition** → **Ajouter des fichiers**
3. Sélectionnez les nouveaux fichiers
4. Cliquez sur **Ajouter**
5. Les fichiers sont ajoutés à l'archive

**Note** : Certains formats (comme .tar.gz) ne permettent pas l'ajout facile. Préférez .zip pour cette utilisation.

### Supprimer des fichiers d'une archive

**Modifier le contenu** :

1. Ouvrez l'archive
2. Sélectionnez le(s) fichier(s) à supprimer
3. Clic droit → **Supprimer**
4. Ou touche `Suppr`
5. Confirmez
6. Le fichier est retiré de l'archive

### Protection par mot de passe

**Sécuriser une archive** :

**Lors de la création** :
1. Clic droit → **Compresser**
2. Choisissez un format supportant le chiffrement : **ZIP** ou **7Z**
3. Cliquez sur **Autres options**
4. Cochez **Protéger par un mot de passe**
5. Entrez le mot de passe (deux fois)
6. Pour 7Z : **Chiffrer la liste des fichiers** (recommandé, cache aussi les noms)
7. **Créer**

**Formats avec mot de passe** :
- **ZIP** : Chiffrement faible (compatible mais pas très sécurisé)
- **7Z** : Chiffrement AES-256 (très sécurisé, recommandé)
- **RAR** : Bonne sécurité (mais création limitée sur Linux)

**Conseils mots de passe** :
- Au moins 12 caractères
- Mélange lettres, chiffres, symboles
- Ne notez pas le mot de passe dans le nom du fichier !
- Communiquez le mot de passe séparément (pas par le même email que l'archive)

### Niveaux de compression

**Compromis vitesse/taille** :

Certains formats permettent de choisir le niveau de compression :

**Aucune compression** :
- Très rapide
- Taille = somme des fichiers
- Utile pour regroupement sans gain d'espace

**Rapide** :
- Compression légère
- Gain de temps
- Taille réduite de ~30%

**Normal** (par défaut) :
- Équilibre
- Recommandé pour la plupart des usages

**Maximum** :
- Compression maximale
- Très lent
- Taille minimale
- Utile pour archivage long terme

**Ultra** (7Z) :
- Extrêmement lent
- Gain marginal par rapport à Maximum
- Rarement utile sauf cas spécifiques

**Recommandation** : Laissez sur **Normal** sauf besoins spécifiques.

### Archiver avec exclusions

**Exclure certains fichiers** :

Avec le gestionnaire graphique, c'est limité. Pour avancé, utilisez la ligne de commande (voir section suivante).

**Astuce graphique** :
1. Copiez les fichiers à archiver dans un dossier temporaire
2. Supprimez les fichiers à exclure
3. Archivez le dossier temporaire
4. Supprimez le dossier temporaire

## Ligne de commande (pour utilisateurs avancés)

### Pourquoi utiliser la ligne de commande ?

**Avantages** :
- **Automatisation** : Scripts, tâches programmées
- **Puissance** : Plus d'options
- **Rapidité** : Pas d'interface graphique
- **SSH** : Gestion de serveurs distants

**Inconvénient** : Moins intuitif au début

### Outils en ligne de commande

**zip / unzip** : ZIP
**tar** : TAR, TAR.GZ, TAR.BZ2, TAR.XZ
**7z** : 7Z
**rar / unrar** : RAR

### Installation des outils

**Vérifier / Installer** :

```bash
# ZIP (normalement préinstallé)
sudo apt install zip unzip

# 7Z
sudo apt install p7zip-full p7zip-rar

# RAR (extraction seulement)
sudo apt install unrar

# TAR (préinstallé sur Linux)
# Pas besoin d'installer
```

### Créer des archives avec ZIP

**Syntaxe de base** :
```bash
zip archive.zip fichier1 fichier2 fichier3
```

**Archiver un dossier complet** :
```bash
zip -r archive.zip dossier/
```
- `-r` : Récursif (inclut sous-dossiers)

**Exemples** :

**Un seul fichier** :
```bash
zip document.zip rapport.pdf
```

**Plusieurs fichiers** :
```bash
zip photos.zip image1.jpg image2.jpg image3.jpg
```

**Dossier complet** :
```bash
zip -r projet.zip MonProjet/
```

**Avec mot de passe** :
```bash
zip -r -e archive.zip dossier/
```
- `-e` : Encrypt, demande un mot de passe

**Compression maximale** :
```bash
zip -r -9 archive.zip dossier/
```
- `-9` : Niveau maximum (1 = rapide, 9 = max)

**Voir la progression** :
```bash
zip -r -v archive.zip dossier/
```
- `-v` : Verbose, affiche chaque fichier

### Extraire avec UNZIP

**Syntaxe de base** :
```bash
unzip archive.zip
```

**Extraire dans un dossier spécifique** :
```bash
unzip archive.zip -d /chemin/destination/
```

**Lister le contenu sans extraire** :
```bash
unzip -l archive.zip
```

**Exemples** :

**Extraction simple** :
```bash
unzip fichiers.zip
```

**Extraction dans un dossier** :
```bash
unzip fichiers.zip -d ~/Documents/Extraction/
```

**Extraction silencieuse** :
```bash
unzip -q archive.zip
```
- `-q` : Quiet, pas d'affichage

**Extraction avec écrasement** :
```bash
unzip -o archive.zip
```
- `-o` : Overwrite, écrase les fichiers existants

**Tester l'intégrité** :
```bash
unzip -t archive.zip
```

### Créer des archives avec TAR

**Syntaxe de base** :
```bash
tar -czf archive.tar.gz dossier/
```

**Options importantes** :
- `-c` : Create (créer)
- `-x` : Extract (extraire)
- `-z` : Gzip (compression .gz)
- `-j` : Bzip2 (compression .bz2)
- `-J` : XZ (compression .xz)
- `-f` : File (fichier)
- `-v` : Verbose (détails)

**Exemples de création** :

**TAR.GZ** (le plus courant) :
```bash
tar -czf archive.tar.gz dossier/
```

**TAR.BZ2** (meilleure compression) :
```bash
tar -cjf archive.tar.bz2 dossier/
```

**TAR.XZ** (excellente compression) :
```bash
tar -cJf archive.tar.xz dossier/
```

**TAR sans compression** :
```bash
tar -cf archive.tar dossier/
```

**Avec progression** :
```bash
tar -czvf archive.tar.gz dossier/
```

**Exclure des fichiers** :
```bash
tar -czf archive.tar.gz dossier/ --exclude='*.log' --exclude='cache/*'
```

### Extraire avec TAR

**Syntaxe de base** :
```bash
tar -xzf archive.tar.gz
```

**Détection automatique** :
```bash
tar -xf archive.tar.gz
```
- Détecte automatiquement le type de compression

**Exemples d'extraction** :

**TAR.GZ** :
```bash
tar -xzf archive.tar.gz
```

**Dans un dossier spécifique** :
```bash
tar -xzf archive.tar.gz -C /chemin/destination/
```

**Avec détails** :
```bash
tar -xzvf archive.tar.gz
```

**Lister le contenu** :
```bash
tar -tzf archive.tar.gz
```

**Extraire un seul fichier** :
```bash
tar -xzf archive.tar.gz chemin/dans/archive/fichier.txt
```

### Utiliser 7Z

**Créer une archive 7Z** :
```bash
7z a archive.7z dossier/
```
- `a` : Add (ajouter)

**Avec mot de passe** :
```bash
7z a -p archive.7z dossier/
```
- `-p` : Password, demande un mot de passe

**Avec mot de passe dans la commande** (moins sécurisé) :
```bash
7z a -pMONMOTDEPASSE archive.7z dossier/
```

**Chiffrer les noms de fichiers** :
```bash
7z a -p -mhe=on archive.7z dossier/
```

**Compression maximale** :
```bash
7z a -mx=9 archive.7z dossier/
```
- `-mx=9` : Niveau ultra

**Extraire** :
```bash
7z x archive.7z
```
- `x` : Extract (avec structure de dossiers)

**Extraire tout dans le dossier actuel** :
```bash
7z e archive.7z
```
- `e` : Extract (tout au même niveau, sans dossiers)

**Lister** :
```bash
7z l archive.7z
```

**Tester** :
```bash
7z t archive.7z
```

### Extraire RAR

**Installation** :
```bash
sudo apt install unrar
```

**Extraire** :
```bash
unrar x archive.rar
```

**Lister** :
```bash
unrar l archive.rar
```

**Tester** :
```bash
unrar t archive.rar
```

**Note** : Création de RAR non supportée nativement sur Linux (utilisez Windows ou Wine).

### Exemples pratiques de scripts

**Sauvegarder un dossier avec la date** :
```bash
#!/bin/bash
DATE=$(date +%Y-%m-%d)
tar -czf sauvegarde-$DATE.tar.gz ~/Documents/
```

**Archiver et supprimer les fichiers de plus de 30 jours** :
```bash
#!/bin/bash
find ~/Téléchargements/ -type f -mtime +30 -print0 | \
  tar -czf anciens-telechargements.tar.gz --null -T -
find ~/Téléchargements/ -type f -mtime +30 -delete
```

**Archiver séparément chaque sous-dossier** :
```bash
#!/bin/bash
for dir in */; do
  tar -czf "${dir%/}.tar.gz" "$dir"
done
```

## Formats spéciaux

### Images ISO

**Images de disque** :

**Qu'est-ce qu'un ISO ?** :
- Image exacte d'un CD/DVD
- Utilisé pour distributions Linux, logiciels

**Créer un ISO depuis un CD/DVD** :
```bash
dd if=/dev/cdrom of=image.iso bs=2048
```

**Monter un ISO** (accéder au contenu sans graver) :
```bash
sudo mkdir /mnt/iso
sudo mount -o loop image.iso /mnt/iso
cd /mnt/iso
# Parcourez le contenu
sudo umount /mnt/iso
```

**Extraire le contenu** :
```bash
7z x image.iso
```

**Graver un ISO** (utiliser un outil graphique comme Brasero)

### Archives auto-extractibles

**Créer une archive auto-extractible** :

Linux n'a pas de format .exe auto-extractible comme Windows.

**Alternative** : Script shell
```bash
#!/bin/bash
# auto-extract.sh
tail -n +4 "$0" | tar -xzf -
exit 0
# Archive data follows
```

Puis concaténer :
```bash
cat auto-extract.sh archive.tar.gz > package.sh
chmod +x package.sh
```

Pour extraire :
```bash
./package.sh
```

## Astuces et bonnes pratiques

### Organisation et nommage

**Nommage des archives** :

**Bonnes pratiques** :
- **Incluez la date** : `rapport-2024-03-15.zip`
- **Soyez descriptif** : `photos-vacances-grece-2024.tar.gz`
- **Version** : `projet-v1.2.zip`
- **Pas d'espaces** : Utilisez tirets ou underscores

**Mauvais exemples** :
- `archive.zip` (trop vague)
- `Nouveau dossier (2).zip` (générique)
- `sans titre.zip` (pas descriptif)

### Vérification d'intégrité

**Tester une archive** :

Avant de supprimer les originaux, testez !

**ZIP** :
```bash
unzip -t archive.zip
```

**TAR** :
```bash
tar -tzf archive.tar.gz > /dev/null
```

**7Z** :
```bash
7z t archive.7z
```

**Si "OK"** : Archive intègre
**Si erreur** : Archive corrompue, ne supprimez pas les originaux !

### Sommes de contrôle

**Vérifier qu'une archive n'a pas été altérée** :

**Créer une somme MD5** :
```bash
md5sum archive.zip > archive.zip.md5
```

**Vérifier** :
```bash
md5sum -c archive.zip.md5
```

**SHA256 (plus sécurisé)** :
```bash
sha256sum archive.zip > archive.zip.sha256
sha256sum -c archive.zip.sha256
```

**Utilité** :
- Vérifier téléchargements
- Détecter corruptions
- Vérifier intégrité dans le temps

### Compression et types de fichiers

**Fichiers qui compressent bien** :
- **Texte** : .txt, .html, .xml, .json (ratio ~70-90%)
- **Code source** : .py, .js, .java (ratio ~70-85%)
- **Logs** : (ratio ~80-95%)

**Fichiers qui compressent mal** :
- **Images** : .jpg, .png (déjà compressés, gain ~5-10%)
- **Vidéos** : .mp4, .mkv (déjà compressés, gain ~1-5%)
- **Audio** : .mp3, .aac (déjà compressés)
- **Archives** : .zip dans .zip (inutile)

**Conseil** :
- Ne compressez pas les médias déjà compressés
- Archivez-les en mode "stockage" sans compression
- Focalisez la compression sur texte et code

### Quand ne pas archiver

**Pas besoin d'archive si** :
- Fichiers déjà compressés (photos JPG, vidéos MP4)
- Un seul petit fichier
- Partage local (réseau domestique)
- Travail collaboratif en cours (utilisez plutôt un dossier partagé)

### Sécurité des archives

**Méfiance avec les archives suspectes** :

**Dangers potentiels** :
- **Zip bombs** : Archive minuscule qui devient énorme (plusieurs To)
- **Chemins absolus** : Fichiers extraits en dehors du dossier voulu
- **Exécutables** : Virus dans .exe, .sh

**Bonnes pratiques** :
- **Vérifiez la source** : Archives de confiance uniquement
- **Listez avant d'extraire** : Vérifiez le contenu
- **Antivirus** : Scannez les archives douteuses
- **Bac à sable** : Extrayez dans un dossier isolé

**Lister avant extraction** :
```bash
unzip -l suspect.zip  # Regardez les chemins et noms
7z l suspect.7z
tar -tzf suspect.tar.gz
```

Si vous voyez des chemins comme `/etc/` ou `../../` → Méfiance !

### Archives et sauvegardes

**Pour sauvegardes importantes** :

**Format recommandé** : **TAR.GZ** ou **TAR.XZ**
- Préserve permissions Unix
- Portable
- Vérifiable

**Ajoutez des métadonnées** :
```bash
# Créer avec métadonnées
tar -czf sauvegarde-$(date +%Y%m%d).tar.gz --listed-incremental=backup.snar dossier/
```

**Sauvegarde incrémentale** :
- Première fois : Sauvegarde complète
- Fois suivantes : Seulement ce qui a changé

**Testez vos sauvegardes !** :
- Essayez d'extraire
- Vérifiez l'intégrité
- Au moins une fois par an

### Découper de grosses archives

**Pour les archives trop grosses (email, upload)** :

**Avec 7Z** :
```bash
7z a -v100m archive.7z dossier/
```
- `-v100m` : Volumes de 100 Mo
- Crée : `archive.7z.001`, `archive.7z.002`, etc.

**Avec ZIP** :
```bash
zip -r -s 100m archive.zip dossier/
```

**Avec split (après création)** :
```bash
tar -czf - dossier/ | split -b 100M - archive.tar.gz.part
```

**Reconstituer** :
```bash
cat archive.tar.gz.part* > archive.tar.gz
tar -xzf archive.tar.gz
```

## Gestionnaires alternatifs

### PeaZip

**Gestionnaire plus complet** :

**Installation** :
```bash
# Via site officiel ou Flatpak
flatpak install flathub io.github.peazip.PeaZip
```

**Avantages** :
- Support de 200+ formats
- Chiffrement avancé
- Conversion entre formats
- Gestionnaire de fichiers intégré
- Création d'archives auto-extractibles

### Ark (KDE)

**Gestionnaire KDE** :

```bash
sudo apt install ark
```

**Avantages** :
- Intégration KDE
- Support de nombreux formats
- Plugins pour formats additionnels

### Atool

**Outil en ligne de commande universel** :

```bash
sudo apt install atool
```

**Usage** :
```bash
atool -x archive.zip    # Extraire (auto-détecte format)
atool -a archive.zip fichiers/  # Créer
atool -l archive.zip    # Lister
```

**Avantage** : Une commande pour tous les formats !

## Dépannage

### Archive corrompue

**Symptômes** :
- Erreur lors de l'extraction
- "Archive endommagée"
- Extraction incomplète

**Solutions** :

**Tester l'intégrité** :
```bash
unzip -t archive.zip
7z t archive.7z
tar -tzf archive.tar.gz
```

**Tentative de réparation (ZIP)** :
```bash
zip -FF archive.zip --out archive-repare.zip
```

**Si récupérable** :
- Certains fichiers peuvent être sauvés
- Essayez d'extraire ce qui passe

**Si irréparable** :
- Re-téléchargez
- Restaurez depuis sauvegarde

### Mot de passe oublié

**Malheureusement** :
- Chiffrement moderne est très robuste
- Pas de solution miracle

**Options** :
1. **Essayez les mots de passe courants** : Vous l'avez peut-être noté quelque part
2. **Outils de force brute** : `fcrackzip`, `john` (très long)
3. **Contactez l'expéditeur**

**Prévention** :
- Utilisez un gestionnaire de mots de passe
- Notez le mot de passe séparément (coffre-fort numérique)

### Extraction lente

**Si extraction très lente** :

**Causes** :
- Archive très volumineuse
- Disque lent (HDD)
- Compression maximale

**Solutions** :
- Patience !
- Extrayez sur SSD si possible
- Fermez autres applications
- Utilisez ligne de commande (parfois plus rapide)

### Formats non supportés

**Si format non reconnu** :

**Vérifiez l'extension** :
```bash
file archive.xxx
```

**Installez le support** :
```bash
sudo apt install p7zip-full p7zip-rar unrar
```

**Formats vraiment exotiques** :
- Cherchez le logiciel spécifique
- Convertissez sur un autre système
- Demandez une autre version

## Automatisation

### Scripts de sauvegarde automatique

**Exemple : Sauvegarde quotidienne** :

```bash
#!/bin/bash
# sauvegarde-auto.sh

DOSSIER_SOURCE="$HOME/Documents"
DOSSIER_DEST="$HOME/Sauvegardes"
DATE=$(date +%Y-%m-%d)
FICHIER="documents-$DATE.tar.gz"

# Créer dossier de destination si inexistant
mkdir -p "$DOSSIER_DEST"

# Créer l'archive
tar -czf "$DOSSIER_DEST/$FICHIER" "$DOSSIER_SOURCE"

# Vérifier
if [ $? -eq 0 ]; then
    echo "Sauvegarde réussie : $FICHIER"
else
    echo "Erreur lors de la sauvegarde !"
    exit 1
fi

# Supprimer sauvegardes de plus de 30 jours
find "$DOSSIER_DEST" -name "documents-*.tar.gz" -mtime +30 -delete

echo "Anciennes sauvegardes nettoyées"
```

**Rendre exécutable** :
```bash
chmod +x sauvegarde-auto.sh
```

**Automatiser avec cron** :
```bash
crontab -e
```

Ajoutez :
```
0 2 * * * /chemin/vers/sauvegarde-auto.sh
```
(Exécute tous les jours à 2h du matin)

### Archivage incrémental

**Sauvegarder uniquement ce qui a changé** :

```bash
#!/bin/bash
# sauvegarde-incrementale.sh

DOSSIER="$HOME/Documents"
DEST="$HOME/Sauvegardes"
DATE=$(date +%Y-%m-%d)
SNAPSHOT="$DEST/backup.snar"

mkdir -p "$DEST"

# Sauvegarde incrémentale
tar -czf "$DEST/incremental-$DATE.tar.gz" \
    --listed-incremental="$SNAPSHOT" \
    "$DOSSIER"

echo "Sauvegarde incrémentale créée : incremental-$DATE.tar.gz"
```

**Première exécution** : Sauvegarde complète
**Suivantes** : Seulement les changements

### Surveillance de taille

**Alerter si archive dépasse une taille** :

```bash
#!/bin/bash
# verif-taille.sh

FICHIER="archive.tar.gz"
TAILLE_MAX=1000000000  # 1 Go en octets

tar -czf "$FICHIER" dossier/

TAILLE=$(stat -c%s "$FICHIER")

if [ $TAILLE -gt $TAILLE_MAX ]; then
    echo "ATTENTION : Archive trop grosse ($TAILLE octets)"
    echo "Considérez compression maximale ou découpage"
fi
```

## Ressources et liens

### Documentation

**Manuels** :
```bash
man zip
man tar
man 7z
```

**Guides en ligne** :
- [https://www.gnu.org/software/tar/manual/](https://www.gnu.org/software/tar/manual/)
- Documentation 7-Zip : [https://www.7-zip.org/](https://www.7-zip.org/)

### Communauté

- Forums Linux Mint
- Ask Ubuntu (applicable à Mint)
- Stack Overflow pour questions spécifiques

### Outils recommandés

- **Graphique** : File Roller (par défaut), PeaZip
- **Ligne de commande** : tar, 7z, atool
- **Avancé** : dar (sauvegarde incrémentale), rsync

## Conclusion

Les gestionnaires d'archives sont des outils essentiels pour gérer, compresser et partager vos fichiers efficacement. Linux Mint offre un excellent support natif pour tous les formats courants grâce à File Roller et aux outils en ligne de commande.

**Points clés à retenir** :

- **ZIP** : Format universel, privilégiez-le pour le partage
- **7Z** : Meilleure compression, utilisez-le pour l'archivage
- **TAR.GZ** : Standard Linux, préserve les permissions
- **Clic droit** : Méthode la plus simple (Compresser / Extraire)
- **Mot de passe** : Protection avec ZIP ou 7Z
- **Testez vos archives** : Avant de supprimer les originaux !
- **Ligne de commande** : Puissance et automatisation

Que vous soyez un simple utilisateur compressant des photos pour les envoyer par email, ou un administrateur système automatisant des sauvegardes, Linux Mint vous fournit tous les outils nécessaires. Commencez par les méthodes graphiques simples, et explorez progressivement les options en ligne de commande pour plus de contrôle et d'automatisation.

---


⏭️ [Lecteur PDF](/05-applications-essentielles-et-outils-mint/07-lecteur-pdf.md)
