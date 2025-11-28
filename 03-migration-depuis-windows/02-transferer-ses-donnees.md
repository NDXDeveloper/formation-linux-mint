🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.2 - Transférer ses données

## Introduction

Maintenant que vous avez préparé votre migration et sauvegardé vos données, il est temps de les transférer vers votre nouveau système Linux Mint. Ce chapitre vous guidera à travers les différentes méthodes pour rapatrier vos fichiers, documents, photos, et paramètres de manière simple et efficace.

> 💡 **Bonne nouvelle** : Transférer ses données vers Linux Mint est généralement plus simple que vous ne le pensez. Le système reconnaît les formats de fichiers Windows et peut lire vos disques durs externes sans problème.

---

## Vue d'ensemble des méthodes de transfert

Il existe plusieurs façons de transférer vos données vers Linux Mint. Le choix dépend de votre situation :

| Méthode | Idéal pour | Avantages | Inconvénients |
|---------|-----------|-----------|---------------|
| **Disque dur externe** | Tous types de fichiers | Simple, rapide, fiable | Nécessite un périphérique externe |
| **Clé USB** | Fichiers légers | Très simple, portable | Limité en capacité |
| **Partition Windows** | Dual-boot | Accès direct, pas de copie | Nécessite Windows installé |
| **Réseau local** | Transfert entre 2 PC | Pas de périphérique externe | Configuration réseau nécessaire |
| **Cloud** | Documents, photos | Accessible partout | Limité par connexion Internet |
| **Warpinator** | Transfert PC à PC (LAN) | Outil intégré à Mint | Nécessite 2 PC sous Mint/Linux |

---

## Méthode 1 : Via un disque dur externe ou une clé USB

C'est la méthode la plus simple et la plus recommandée pour les débutants.

### Avant de commencer

**Depuis Windows (avant l'installation de Linux Mint) :**
1. Branchez votre disque dur externe ou clé USB
2. Copiez tous vos dossiers importants dessus :
   - Documents
   - Images
   - Vidéos
   - Musique
   - Bureau
   - Téléchargements (si vous voulez les garder)

> 💡 **Astuce** : Organisez vos fichiers dans des dossiers bien nommés sur le disque externe, cela facilitera le transfert sous Linux Mint.

### Sous Linux Mint

#### Étape 1 : Brancher le périphérique

1. Branchez votre disque dur externe ou clé USB
2. Linux Mint le détecte automatiquement
3. Une notification apparaît, cliquez dessus pour ouvrir le périphérique
4. Ou ouvrez le **Gestionnaire de fichiers** (Nemo) et cliquez sur le périphérique dans la barre latérale gauche

#### Étape 2 : Localiser vos fichiers

Votre périphérique externe apparaît sous un nom comme :
- "Mon disque" (si vous l'avez nommé)
- "2TB External" (capacité + type)
- Ou un nom générique comme "USB Drive"

Naviguez dans les dossiers pour retrouver vos fichiers.

#### Étape 3 : Copier vers votre dossier personnel

Votre dossier personnel sous Linux Mint se trouve à `/home/votre-nom-utilisateur/`

**Méthode simple :**
1. Ouvrez deux fenêtres du gestionnaire de fichiers (Ctrl+N pour une nouvelle fenêtre)
2. Dans la première : votre disque externe
3. Dans la seconde : votre dossier personnel (cliquez sur "Dossier personnel" dans la barre latérale)
4. Faites glisser les dossiers de la fenêtre externe vers votre dossier personnel

**Où copier quoi ?**
- Documents Windows → `/home/votre-nom/Documents/`
- Images Windows → `/home/votre-nom/Images/`
- Vidéos Windows → `/home/votre-nom/Vidéos/`
- Musique Windows → `/home/votre-nom/Musique/`
- Bureau Windows → `/home/votre-nom/Bureau/`
- Téléchargements → `/home/votre-nom/Téléchargements/`

> ⚠️ **Important** : Le copier-coller sous Linux fonctionne comme sous Windows : Ctrl+C pour copier, Ctrl+V pour coller. Par défaut, un glisser-déposer **copie** les fichiers (ils restent sur le disque externe).

#### Étape 4 : Vérifier le transfert

1. Ouvrez les dossiers de destination
2. Vérifiez que tous vos fichiers sont bien présents
3. Ouvrez quelques fichiers pour confirmer qu'ils fonctionnent
4. Une fois vérifié, vous pouvez formater votre disque externe ou le garder comme sauvegarde

### Gestion des fichiers volumineux

Pour les transferts de gros volumes de données :

**Suivre la progression :**
- Une barre de progression apparaît pendant la copie
- Vous pouvez continuer à utiliser votre ordinateur pendant ce temps
- Les transferts peuvent être longs (plusieurs heures pour des centaines de Go)

**En cas d'interruption :**
- Si le transfert s'arrête, relancez-le simplement
- Les fichiers déjà copiés ne seront pas recopiés
- Linux Mint gère intelligemment les copies interrompues

---

## Méthode 2 : Accéder à la partition Windows (en dual-boot)

Si vous avez installé Linux Mint en dual-boot avec Windows, vous pouvez accéder directement à vos fichiers Windows.

### Comment accéder à Windows depuis Linux Mint

#### Étape 1 : Identifier la partition Windows

1. Ouvrez le **Gestionnaire de fichiers** (Nemo)
2. Regardez dans la barre latérale gauche sous "Périphériques"
3. Vous verrez vos partitions listées, par exemple :
   - "500 GB Volume" (votre disque Windows)
   - "Données" (si vous avez une partition de données)

#### Étape 2 : Monter la partition

1. Cliquez sur la partition Windows dans la barre latérale
2. Elle "monte" automatiquement (devient accessible)
3. Vous pouvez maintenant naviguer dedans

#### Étape 3 : Localiser vos fichiers Windows

Votre partition Windows a la même structure que sous Windows :

```
/media/votre-nom/NomDeLaPartition/
├── Program Files/
├── Program Files (x86)/
├── Windows/
└── Users/
    └── VotreNomWindows/
        ├── Desktop/          (votre Bureau Windows)
        ├── Documents/        (vos Documents Windows)
        ├── Downloads/        (vos Téléchargements)
        ├── Pictures/         (vos Images)
        ├── Music/            (votre Musique)
        └── Videos/           (vos Vidéos)
```

> 💡 **Astuce** : Les noms des dossiers sont en anglais sous Windows, même si votre Windows est en français.

#### Étape 4 : Copier les fichiers

1. Naviguez jusqu'au dossier qui vous intéresse (par exemple `Users/VotreNom/Documents/`)
2. Sélectionnez les fichiers à copier (Ctrl+A pour tout sélectionner)
3. Copiez-les (Ctrl+C)
4. Allez dans votre dossier Linux correspondant (par exemple `/home/votre-nom/Documents/`)
5. Collez (Ctrl+V)

### Avantages et précautions

**Avantages :**
- Pas besoin de périphérique externe
- Accès instantané à tous vos fichiers Windows
- Pratique pour récupérer un fichier oublié

**Précautions :**
- ⚠️ **Ne modifiez jamais les fichiers système Windows** (dossiers Windows, Program Files)
- Lisez vos fichiers personnels, mais évitez de modifier directement depuis Linux
- Copiez les fichiers vers Linux plutôt que de travailler directement sur la partition Windows
- Si Windows est en "démarrage rapide", désactivez cette option sous Windows pour éviter les problèmes

### Désactiver le démarrage rapide de Windows

Le "démarrage rapide" de Windows peut empêcher Linux de modifier les fichiers Windows. Pour le désactiver :

**Depuis Windows :**
1. Ouvrez le Panneau de configuration
2. Allez dans "Options d'alimentation"
3. Cliquez sur "Choisir l'action des boutons d'alimentation"
4. Cliquez sur "Modifier des paramètres actuellement non disponibles"
5. Décochez "Activer le démarrage rapide"
6. Enregistrez les modifications

---

## Méthode 3 : Transfert via le réseau local

Si vous avez deux ordinateurs sur le même réseau (par exemple, votre ancien PC Windows et votre nouveau PC Linux Mint), vous pouvez transférer les fichiers directement.

### Option A : Warpinator (recommandé)

**Warpinator** est un outil développé par l'équipe Linux Mint pour faciliter le partage de fichiers sur le réseau local.

#### Sur Linux Mint (récepteur)

1. Ouvrez le menu → Internet → **Warpinator**
2. Warpinator démarre et attend les connexions
3. Notez le nom de votre ordinateur affiché en haut

#### Sur Windows (émetteur)

**Option 1 : Installer Warpinator pour Windows**
1. Téléchargez Warpinator pour Windows depuis le site officiel de Linux Mint
2. Installez-le
3. Lancez Warpinator
4. Il détecte automatiquement les autres ordinateurs Warpinator sur le réseau

**Option 2 : Utiliser un Live USB Linux Mint**
1. Démarrez votre PC Windows avec une clé USB Linux Mint (mode Live)
2. Connectez-vous au réseau WiFi
3. Lancez Warpinator
4. Accédez à votre partition Windows pour envoyer les fichiers

#### Transférer des fichiers

1. Dans Warpinator, cliquez sur l'ordinateur de destination
2. Cliquez sur "Envoyer des fichiers"
3. Sélectionnez les fichiers ou dossiers à transférer
4. Le transfert commence automatiquement
5. Sur l'ordinateur de réception, acceptez le transfert

**Avantages :**
- Très simple d'utilisation
- Interface intuitive
- Fonctionne parfaitement entre machines Linux Mint
- Pas de configuration réseau complexe

### Option B : Partage réseau Windows (SMB/Samba)

#### Partager depuis Windows

1. Sur Windows, cliquez droit sur le dossier à partager
2. Propriétés → Onglet "Partage"
3. Cliquez sur "Partager"
4. Ajoutez "Tout le monde" avec permission "Lecture" (ou "Lecture/Écriture")
5. Notez le chemin réseau affiché (par exemple `\\MONPC\Dossier`)

#### Accéder depuis Linux Mint

1. Ouvrez le Gestionnaire de fichiers
2. Dans la barre d'adresse, tapez : `smb://AdresseIPdeWindows/` ou `smb://NomPCWindows/`
3. Appuyez sur Entrée
4. Entrez votre nom d'utilisateur et mot de passe Windows si demandé
5. Les dossiers partagés apparaissent
6. Vous pouvez maintenant copier les fichiers vers Linux Mint

**Trouver l'adresse IP de Windows :**
- Sous Windows, ouvrez l'Invite de commandes
- Tapez `ipconfig`
- Notez l'adresse IPv4 (par exemple 192.168.1.10)

---

## Méthode 4 : Via le Cloud

Si vos fichiers sont déjà dans le cloud (Google Drive, OneDrive, Dropbox), le transfert est encore plus simple.

### Google Drive

#### Option 1 : Via le navigateur web
1. Ouvrez Firefox
2. Allez sur drive.google.com
3. Connectez-vous à votre compte
4. Téléchargez vos fichiers vers Linux Mint

#### Option 2 : Client de synchronisation
1. Installez **Insync** (client Google Drive pour Linux, payant mais efficace)
2. Ou utilisez **rclone** (gratuit, en ligne de commande)
3. Synchronisez votre Drive avec un dossier local

### OneDrive

1. Utilisez le navigateur web pour télécharger vos fichiers
2. Ou installez **rclone** pour synchroniser OneDrive
3. Configuration depuis le navigateur web : onedrive.live.com

### Dropbox

1. Installez le client Dropbox pour Linux
2. Téléchargement depuis dropbox.com
3. Installation du paquet .deb
4. Connectez-vous et synchronisez

### Avantages et limites

**Avantages :**
- Pas besoin de périphérique physique
- Accessible de n'importe où
- Sauvegarde automatique

**Limites :**
- Limité par votre connexion Internet
- Limites de stockage gratuit
- Peut être long pour de gros volumes

---

## Méthode 5 : Transfert direct via câble réseau

Pour les transferts massifs entre deux ordinateurs, un câble Ethernet direct peut être la solution la plus rapide.

### Configuration

1. Connectez les deux PC avec un câble Ethernet (croisé ou normal, les cartes modernes s'adaptent)
2. Sur Linux Mint, configurez une IP statique :
   - Ouvrez les paramètres réseau
   - Sélectionnez la connexion Ethernet
   - Mode manuel : IP 192.168.137.1, masque 255.255.255.0
3. Sur Windows, configuration similaire : IP 192.168.137.2, même masque
4. Utilisez ensuite le partage réseau (méthode 3) pour transférer

---

## Cas spéciaux : Transferts de configurations

### Favoris et mots de passe du navigateur

#### Firefox (recommandé)

**Méthode 1 : Compte Firefox Sync**
1. Sous Windows : créez un compte Firefox Sync
2. Synchronisez vos données (favoris, mots de passe, extensions)
3. Sous Linux Mint : connectez-vous au même compte
4. Tout se synchronise automatiquement

**Méthode 2 : Export/Import manuel**
1. Sous Windows Firefox : Menu → Marque-pages → Gérer les marque-pages
2. Importation et sauvegarde → Sauvegarder
3. Sauvegardez le fichier .json
4. Transférez ce fichier vers Linux Mint
5. Sous Linux Mint Firefox : Importation et sauvegarde → Restaurer → Choisir un fichier

#### Chrome

1. Connectez-vous à votre compte Google sous Chrome Windows
2. Synchronisez vos données
3. Installez Chrome sous Linux Mint (ou utilisez Firefox)
4. Connectez-vous au même compte Google
5. Tout se synchronise

#### Edge

1. Connectez-vous à votre compte Microsoft
2. Synchronisez vos données
3. Sous Linux Mint, utilisez Edge pour Linux ou importez dans Firefox

### Emails et contacts

#### Si vous utilisez Gmail, Outlook.com ou un service web
- Rien à faire ! Accédez simplement à votre compte depuis Linux Mint
- Ou configurez Thunderbird (client email préinstallé)

#### Si vous utilisez Outlook Windows (local)

**Exporter depuis Outlook Windows :**
1. Fichier → Ouvrir et exporter → Importer/Exporter
2. Choisir "Exporter vers un fichier"
3. Sélectionner "Fichier de données Outlook (.pst)"
4. Sélectionnez les dossiers à exporter
5. Sauvegardez le fichier .pst

**Importer dans Thunderbird (Linux Mint) :**
1. Installez l'extension "ImportExportTools NG" dans Thunderbird
2. Outils → ImportExportTools NG → Importer un profil
3. Sélectionnez votre fichier .pst
4. Thunderbird importe vos emails et contacts

#### Si vous utilisez Thunderbird Windows

**Méthode simple : Copier le profil**
1. Sous Windows : trouvez votre profil Thunderbird
   - Chemin : `C:\Users\VotreNom\AppData\Roaming\Thunderbird\Profiles\`
2. Copiez le dossier complet du profil
3. Sous Linux Mint : collez-le dans
   - Chemin : `/home/votre-nom/.thunderbird/`
4. Lancez Thunderbird, tout est là !

### Documents et paramètres LibreOffice

Si vous utilisiez LibreOffice sous Windows :

1. Vos documents sont déjà compatibles (formats .odt, .ods, etc.)
2. Copiez-les simplement dans `/home/votre-nom/Documents/`
3. LibreOffice est préinstallé sous Linux Mint et les ouvrira directement

Si vous utilisiez Microsoft Office :

1. Vos fichiers (.docx, .xlsx, .pptx) s'ouvrent dans LibreOffice
2. La compatibilité est généralement excellente
3. Pour une compatibilité parfaite, vous pouvez installer Microsoft Office Online (gratuit) ou utiliser OnlyOffice

---

## Organisation de vos fichiers sous Linux Mint

Une fois vos fichiers transférés, prenez le temps de les organiser selon la structure Linux.

### Structure recommandée

```
/home/votre-nom/
├── Bureau/               (fichiers affichés sur votre bureau)
├── Documents/
│   ├── Travail/
│   ├── Personnel/
│   └── Administratif/
├── Images/
│   ├── Photos/
│   ├── Captures d'écran/
│   └── Téléchargées/
├── Vidéos/
├── Musique/
├── Téléchargements/
├── Modèles/             (modèles de documents)
└── Public/              (fichiers à partager)
```

### Conseils d'organisation

1. **Profitez-en pour faire du tri** : la migration est l'occasion de supprimer les fichiers inutiles
2. **Créez des sous-dossiers clairs** : mieux vaut trop de dossiers que tout en vrac
3. **Utilisez des noms explicites** : évitez "Nouveau dossier" ou "Sans titre"
4. **Datez vos sauvegardes** : "Documents_Backup_2024-11" est plus clair que "Backup"

---

## Vérification post-transfert

Une fois tous vos fichiers transférés, faites ces vérifications :

### Check-list de vérification

- [ ] Tous mes documents importants sont accessibles
- [ ] Mes photos et vidéos s'ouvrent correctement
- [ ] Ma musique est lisible (testez quelques fichiers)
- [ ] Mes favoris de navigateur sont importés
- [ ] Mes mots de passe fonctionnent (ou sont importés dans le gestionnaire)
- [ ] Mes emails sont accessibles (web ou Thunderbird)
- [ ] Mes contacts sont importés
- [ ] Les fichiers spéciaux (PDF, archives ZIP) s'ouvrent bien

### Tester différents types de fichiers

Ouvrez quelques fichiers de chaque type pour vérifier :

**Documents :**
- .docx, .doc → LibreOffice Writer
- .xlsx, .xls → LibreOffice Calc
- .pptx, .ppt → LibreOffice Impress
- .pdf → Lecteur de documents

**Images :**
- .jpg, .png → Visionneuse d'images
- .gif → Visionneuse d'images
- .psd (Photoshop) → GIMP (si vous en avez)

**Audio/Vidéo :**
- .mp3, .flac → Lecteur de musique
- .mp4, .avi, .mkv → VLC (préinstallé)

**Archives :**
- .zip, .rar, .7z → Gestionnaire d'archives (clic droit → Extraire)

---

## Résolution de problèmes courants

### Le disque externe n'est pas détecté

**Solutions :**
1. Débranchez et rebranchez le périphérique
2. Essayez un autre port USB
3. Ouvrez "Disques" (application préinstallée) pour voir si le disque apparaît
4. Vérifiez que le disque fonctionne sous Windows

### Les fichiers ont des noms bizarres (caractères étranges)

**Cause :** Problème d'encodage de caractères

**Solution :**
1. C'est rare mais peut arriver avec des noms de fichiers très spéciaux
2. Renommez les fichiers avec des caractères standards
3. Évitez les accents dans les noms de fichiers si vous partagez entre systèmes

### Je ne peux pas écrire sur ma partition Windows

**Cause :** Windows en hibernation ou "démarrage rapide" actif

**Solution :**
1. Démarrez sous Windows
2. Désactivez le démarrage rapide (voir plus haut)
3. Faites un arrêt complet (pas une mise en veille)
4. Redémarrez sous Linux Mint

### Les transferts sont très lents

**Causes possibles :**
- Disque externe en USB 2.0 (lent) au lieu de USB 3.0
- Disque externe fragmenté ou défectueux
- Transfert réseau sur WiFi lent

**Solutions :**
- Utilisez un port USB 3.0 (généralement bleu)
- Pour le réseau, préférez le câble Ethernet
- Patientez pour les gros transferts (c'est normal)

### Certains fichiers ne s'ouvrent pas

**Solutions selon le type :**
- Fichiers Office : installez OnlyOffice pour meilleure compatibilité
- Fichiers .exe : ce sont des programmes Windows, inutiles sous Linux
- Fichiers rares : cherchez l'application appropriée dans le Gestionnaire de logiciels

---

## Nettoyage après transfert

Une fois que vous êtes sûr que tout est bien transféré et fonctionne :

### Sur le disque externe

1. **Option 1 :** Gardez-le comme sauvegarde supplémentaire
2. **Option 2 :** Formatez-le pour libérer l'espace
   - Clic droit sur le périphérique → Formater
   - Choisissez un système de fichiers :
     - **ext4** : si utilisé uniquement sous Linux
     - **exFAT** : pour compatibilité Windows/Linux/Mac
     - **NTFS** : pour compatibilité Windows/Linux

### Sur la partition Windows (si dual-boot)

1. Vous pouvez supprimer vos anciens fichiers Windows si vous ne prévoyez plus d'utiliser Windows
2. Ou gardez-les comme sauvegarde de sécurité pendant quelques semaines
3. **Attention :** Ne supprimez JAMAIS les dossiers système Windows si vous voulez garder le dual-boot

---

## Conclusion

Le transfert de données est une étape cruciale mais simple de votre migration vers Linux Mint. Prenez votre temps, vérifiez que tout est bien transféré, et n'hésitez pas à garder des copies de sauvegarde pendant quelques semaines pour être serein.

Une fois vos données en place, vous êtes prêt à découvrir les équivalents Linux de vos logiciels Windows habituels !

> 🎯 **Prochaine étape** : Dans le chapitre suivant, vous découvrirez comment retrouver vos repères et les équivalences entre Windows et Linux Mint.

---

## Récapitulatif rapide

**Méthodes de transfert par ordre de simplicité :**

1. **Disque externe/Clé USB** ⭐ Recommandé pour débutants
   - Le plus simple
   - Fonctionne dans tous les cas

2. **Partition Windows** (dual-boot)
   - Accès direct aux fichiers
   - Aucune copie nécessaire

3. **Cloud**
   - Pratique si déjà utilisé
   - Limité par Internet

4. **Réseau local**
   - Rapide pour gros volumes
   - Nécessite configuration

**À retenir :**
- Linux Mint lit sans problème vos fichiers Windows
- Copiez toujours vers `/home/votre-nom/` et ses sous-dossiers
- Vérifiez que tout fonctionne avant de supprimer les sauvegardes
- En cas de doute, gardez plusieurs copies

⏭️ [Retrouver ses repères (équivalences Windows/Linux)](/03-migration-depuis-windows/03-retrouver-ses-reperes.md)
