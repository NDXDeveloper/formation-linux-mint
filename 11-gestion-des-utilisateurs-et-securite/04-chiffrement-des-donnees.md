🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 11.4 Chiffrement des données (VeraCrypt, LUKS)

## Introduction

Le chiffrement des données est une technique essentielle pour protéger vos informations confidentielles. Même si quelqu'un vole votre ordinateur ou votre disque dur, vos données resteront illisibles sans la clé de déchiffrement.

### Qu'est-ce que le chiffrement ?

Le **chiffrement** transforme vos données en un format illisible (texte chiffré) à l'aide d'un algorithme cryptographique et d'une clé secrète. Seule la personne possédant la bonne clé peut **déchiffrer** et lire les données.

**Analogie simple** : C'est comme mettre vos documents dans un coffre-fort ultra-sécurisé. Sans la combinaison, personne ne peut accéder au contenu, même en ayant le coffre entre les mains.

### Pourquoi chiffrer vos données ?

- **Confidentialité** : Protéger vos données personnelles, photos, documents
- **Vol ou perte** : Si votre ordinateur portable est volé, vos données restent inaccessibles
- **Conformité** : Exigences légales (RGPD, protection des données médicales, etc.)
- **Espionnage industriel** : Protection des secrets professionnels
- **Vie privée** : Contre la surveillance de masse ou les fouilles sans mandat

### Les deux approches principales

1. **Chiffrement complet du disque** (LUKS)
   - Chiffre l'intégralité de la partition système
   - Protection dès le démarrage de l'ordinateur
   - Transparent une fois déverrouillé

2. **Conteneurs chiffrés** (VeraCrypt)
   - Fichiers "coffre-fort" virtuels
   - Plus flexible et portable
   - Peut être partagé entre différents systèmes d'exploitation

---

## LUKS : Chiffrement de partition Linux

### Qu'est-ce que LUKS ?

**LUKS** (Linux Unified Key Setup) est le standard de chiffrement de disque sous Linux. Il est :
- **Intégré** nativement dans le noyau Linux
- **Performant** : Impact minimal sur les performances
- **Sécurisé** : Utilise des algorithmes éprouvés (AES-256)
- **Flexible** : Support de multiples mots de passe pour le même volume

### Chiffrement lors de l'installation

La manière la plus simple d'utiliser LUKS est de **chiffrer votre système lors de l'installation** de Linux Mint.

#### Procédure lors de l'installation

1. Démarrez l'installation de Linux Mint depuis votre clé USB
2. Lors du choix du type d'installation, sélectionnez **"Options avancées"**
3. Cochez la case **"Chiffrer la nouvelle installation de Linux Mint pour la sécurité"**
4. Choisissez un **mot de passe de chiffrement fort**
   - Différent de votre mot de passe utilisateur
   - Au moins 20 caractères recommandés
   - Notez-le dans un endroit sûr (si vous le perdez, vos données sont perdues à jamais)
5. Continuez l'installation normalement

#### Démarrage avec LUKS

Après installation avec LUKS :
1. Au démarrage, GRUB affiche le menu habituel
2. Après avoir sélectionné Linux Mint, un écran de déverrouillage apparaît
3. Entrez votre **mot de passe de chiffrement**
4. Le système démarre normalement
5. Vous devrez ensuite entrer votre **mot de passe utilisateur** pour vous connecter

> **Important** : Vous aurez donc **deux mots de passe** :
> - Le mot de passe de chiffrement LUKS (pour déverrouiller le disque)
> - Le mot de passe utilisateur (pour vous connecter à votre session)

### Chiffrer une partition existante

**Attention** : Chiffrer une partition existante **efface toutes les données**. Sauvegardez d'abord !

#### Identifier la partition

```bash
lsblk
```

Résultat exemple :
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sdb      8:16   0 238.5G  0 disk
└─sdb1   8:17   0 238.5G  0 part
```

Ici, nous voulons chiffrer `/dev/sdb1`.

#### Créer le conteneur LUKS

```bash
sudo cryptsetup luksFormat /dev/sdb1
```

Le système vous avertira que toutes les données seront effacées. Tapez `YES` en majuscules pour confirmer.

Entrez ensuite votre mot de passe de chiffrement (deux fois).

#### Ouvrir le conteneur chiffré

```bash
sudo cryptsetup luksOpen /dev/sdb1 mon_disque_chiffre
```

Entrez le mot de passe. Le volume déchiffré sera accessible dans `/dev/mapper/mon_disque_chiffre`.

#### Formater le volume

```bash
sudo mkfs.ext4 /dev/mapper/mon_disque_chiffre
```

#### Monter le volume

```bash
sudo mkdir /mnt/mon_disque
sudo mount /dev/mapper/mon_disque_chiffre /mnt/mon_disque
```

Vous pouvez maintenant utiliser `/mnt/mon_disque` normalement.

#### Fermer le volume chiffré

Après utilisation :
```bash
sudo umount /mnt/mon_disque
sudo cryptsetup luksClose mon_disque_chiffre
```

### Montage automatique au démarrage

Pour monter automatiquement une partition LUKS au démarrage :

#### 1. Obtenir l'UUID de la partition

```bash
sudo blkid /dev/sdb1
```

Résultat exemple :
```
/dev/sdb1: UUID="a1b2c3d4-..." TYPE="crypto_LUKS"
```

#### 2. Créer un fichier de clé (optionnel)

Si vous ne voulez pas entrer le mot de passe à chaque fois :

```bash
sudo dd if=/dev/urandom of=/root/.luks-key bs=1024 count=4
sudo chmod 600 /root/.luks-key
```

Ajouter la clé au volume LUKS :
```bash
sudo cryptsetup luksAddKey /dev/sdb1 /root/.luks-key
```

#### 3. Éditer /etc/crypttab

```bash
sudo nano /etc/crypttab
```

Ajoutez :
```
mon_disque_chiffre UUID=a1b2c3d4-... /root/.luks-key luks
```

Ou sans fichier de clé (vous devrez entrer le mot de passe au démarrage) :
```
mon_disque_chiffre UUID=a1b2c3d4-... none luks
```

#### 4. Éditer /etc/fstab

```bash
sudo nano /etc/fstab
```

Ajoutez :
```
/dev/mapper/mon_disque_chiffre /mnt/mon_disque ext4 defaults 0 2
```

#### 5. Redémarrer

```bash
sudo reboot
```

### Gérer les clés LUKS

Un volume LUKS peut avoir jusqu'à 8 clés différentes (mots de passe ou fichiers).

#### Ajouter une nouvelle clé

```bash
sudo cryptsetup luksAddKey /dev/sdb1
```

Entrez un mot de passe existant, puis le nouveau mot de passe.

#### Lister les emplacements de clés

```bash
sudo cryptsetup luksDump /dev/sdb1
```

Cela affiche les emplacements (slots) utilisés.

#### Supprimer une clé

```bash
sudo cryptsetup luksRemoveKey /dev/sdb1
```

Entrez le mot de passe que vous voulez supprimer.

#### Changer un mot de passe

```bash
sudo cryptsetup luksChangeKey /dev/sdb1
```

Entrez l'ancien mot de passe, puis le nouveau.

### Sauvegarder l'en-tête LUKS

L'en-tête LUKS contient les métadonnées de chiffrement. Si l'en-tête est corrompu, **vos données sont perdues**.

#### Sauvegarder

```bash
sudo cryptsetup luksHeaderBackup /dev/sdb1 --header-backup-file /home/utilisateur/luks-header-backup.img
```

Stockez ce fichier dans un endroit sûr (clé USB, cloud chiffré).

#### Restaurer

```bash
sudo cryptsetup luksHeaderRestore /dev/sdb1 --header-backup-file /home/utilisateur/luks-header-backup.img
```

---

## VeraCrypt : Conteneurs chiffrés portables

### Qu'est-ce que VeraCrypt ?

**VeraCrypt** est un logiciel de chiffrement libre et open source, successeur de TrueCrypt. Il permet de :
- Créer des **conteneurs chiffrés** (fichiers qui agissent comme des disques virtuels)
- Chiffrer des **partitions** ou **disques entiers**
- **Multi-plateforme** : Windows, macOS, Linux
- **Portabilité** : Transportez vos conteneurs sur clé USB

### Installation de VeraCrypt

#### Depuis le site officiel (recommandé)

1. Visitez https://www.veracrypt.fr/en/Downloads.html
2. Téléchargez le paquet pour Linux (`.deb` pour Ubuntu/Mint)

```bash
cd ~/Téléchargements
wget https://launchpad.net/veracrypt/trunk/1.26.7/+download/veracrypt-1.26.7-Ubuntu-24.04-amd64.deb
sudo dpkg -i veracrypt-*.deb
sudo apt install -f
```

> **Note** : Vérifiez la dernière version sur le site officiel.

#### Via PPA

```bash
sudo add-apt-repository ppa:unit193/encryption
sudo apt update
sudo apt install veracrypt
```

### Créer un conteneur chiffré

#### Méthode graphique

1. **Lancer VeraCrypt**
   ```bash
   veracrypt
   ```

2. **Créer un volume**
   - Cliquez sur **"Create Volume"** (Créer un volume)
   - Sélectionnez **"Create an encrypted file container"**
   - Cliquez **"Next"**

3. **Type de volume**
   - **Standard VeraCrypt volume** : Volume normal (recommandé pour débuter)
   - **Hidden VeraCrypt volume** : Volume caché dans un autre volume (avancé)
   - Cliquez **"Next"**

4. **Emplacement du volume**
   - Cliquez **"Select File..."**
   - Choisissez un nom et un emplacement (ex: `/home/sophie/Documents/coffre-fort`)
   - Cliquez **"Next"**

5. **Algorithme de chiffrement**
   - **Encryption Algorithm** : Laissez **AES** (excellent choix par défaut)
   - **Hash Algorithm** : Laissez **SHA-512**
   - Cliquez **"Next"**

6. **Taille du volume**
   - Définissez la taille (ex: 500 MB, 5 GB, etc.)
   - Cliquez **"Next"**

7. **Mot de passe**
   - Entrez un **mot de passe fort** (20+ caractères recommandés)
   - VeraCrypt affiche un indicateur de force
   - *Optionnel* : Ajoutez un fichier clé (keyfile) pour plus de sécurité
   - Cliquez **"Next"**

8. **Format du système de fichiers**
   - **Filesystem** :
     - Linux Ext4 (pour Linux uniquement)
     - FAT (compatible Windows/macOS/Linux)
     - exFAT (pour fichiers > 4GB, compatible multi-OS)
   - Déplacez votre souris aléatoirement pour générer de l'entropie
   - Cliquez **"Format"**

9. **Création**
   - Le volume est créé (cela peut prendre du temps selon la taille)
   - Cliquez **"Exit"** quand c'est terminé

### Monter (ouvrir) un conteneur VeraCrypt

1. **Sélectionner un emplacement**
   - Dans la fenêtre principale de VeraCrypt
   - Cliquez sur un emplacement libre (ex: Slot 1)

2. **Sélectionner le fichier**
   - Cliquez **"Select File..."**
   - Choisissez votre conteneur chiffré

3. **Monter**
   - Cliquez **"Mount"**
   - Entrez votre mot de passe
   - Cliquez **"OK"**

4. **Accéder aux fichiers**
   - Le volume est maintenant monté
   - Cliquez **"Open"** pour ouvrir le gestionnaire de fichiers
   - Ou naviguez vers `/mnt/veracrypt1/` (ou le point de montage affiché)

### Démonter un conteneur VeraCrypt

1. Dans la fenêtre VeraCrypt, sélectionnez le volume monté
2. Cliquez **"Dismount"** (Démonter)
3. Le volume est fermé et les données sont à nouveau chiffrées

> **Important** : Démontez toujours vos volumes avant d'éteindre l'ordinateur ou de débrancher la clé USB.

### Chiffrer une partition entière

VeraCrypt peut aussi chiffrer une partition complète (comme une clé USB).

**Attention** : Cela **efface toutes les données** de la partition.

1. Lancez VeraCrypt
2. **"Create Volume"** → **"Encrypt a non-system partition/drive"**
3. **"Standard volume"**
4. **"Select Device..."** → Choisissez votre partition (ex: `/dev/sdb1`)
5. **"Create encrypted volume and format it"** (pour une nouvelle partition vierge)
6. Suivez les étapes (algorithme, taille, mot de passe)
7. Formatez

Pour monter :
1. **"Select Device..."** → Choisissez la partition
2. **"Mount"** → Entrez le mot de passe

### Montage en ligne de commande

VeraCrypt peut aussi être utilisé en ligne de commande :

#### Monter un conteneur

```bash
veracrypt /chemin/vers/conteneur /point/de/montage
```

Exemple :
```bash
veracrypt ~/Documents/coffre-fort ~/coffre-monte
```

Entrez le mot de passe quand demandé.

#### Démonter

```bash
veracrypt -d ~/coffre-monte
```

#### Démonter tous les volumes

```bash
veracrypt -d
```

### Volumes cachés (avancé)

VeraCrypt permet de créer des **volumes cachés** : un conteneur chiffré caché à l'intérieur d'un autre conteneur chiffré.

**Cas d'usage** : Si vous êtes forcé de révéler votre mot de passe, vous pouvez donner le mot de passe du volume "externe" (qui contient des données peu importantes), cachant ainsi l'existence du volume interne (qui contient vos vraies données sensibles).

**Concept** :
- Volume externe : mot de passe A → affiche des données factices
- Volume caché : mot de passe B → affiche vos vraies données

Lors du montage, selon le mot de passe entré, VeraCrypt ouvrira l'un ou l'autre volume.

> **Note** : Cette fonctionnalité est avancée et nécessite une utilisation prudente pour éviter de corrompre le volume caché.

---

## Comparaison LUKS vs VeraCrypt

| Critère | LUKS | VeraCrypt |
|---------|------|-----------|
| **Intégration Linux** | Natif, excellent | Nécessite installation |
| **Performance** | Excellente (noyau) | Très bonne |
| **Portabilité** | Linux uniquement | Windows/macOS/Linux |
| **Facilité (débutants)** | Facile lors de l'installation | Interface claire |
| **Conteneurs portables** | Non (partitions seulement) | Oui (fichiers conteneurs) |
| **Chiffrement système** | Oui (installation) | Oui (mais complexe sur Linux) |
| **Volumes cachés** | Non | Oui |
| **Multi-plateforme** | Non | Oui |
| **Open source** | Oui | Oui |
| **Recommandé pour** | Chiffrement complet du système Linux | Conteneurs portables, compatibilité multi-OS |

### Quand utiliser LUKS ?

- Vous voulez chiffrer votre système Linux complet
- Vous n'avez pas besoin de compatibilité Windows/macOS
- Vous cherchez la meilleure intégration et performance sur Linux
- Vous voulez chiffrer des partitions de données

### Quand utiliser VeraCrypt ?

- Vous voulez des conteneurs portables (clés USB, fichiers cloud)
- Vous partagez des données entre Linux, Windows et macOS
- Vous voulez créer des volumes cachés
- Vous voulez chiffrer des fichiers spécifiques plutôt que tout un disque

### Peut-on utiliser les deux ?

**Oui, absolument !** C'est même une excellente stratégie :
- **LUKS** pour chiffrer votre disque système
- **VeraCrypt** pour des conteneurs portables spécifiques

---

## Chiffrement de dossiers personnels (ecryptfs)

### Qu'est-ce qu'ecryptfs ?

**ecryptfs** est un système de fichiers chiffré au niveau répertoire. Il était proposé par défaut dans les anciennes versions d'Ubuntu pour chiffrer le dossier `/home`.

> **Note** : ecryptfs est maintenant moins recommandé au profit de LUKS ou VeraCrypt, mais il reste utilisable pour des besoins spécifiques.

### Installation

```bash
sudo apt install ecryptfs-utils
```

### Chiffrer un dossier

```bash
sudo mount -t ecryptfs /chemin/source /chemin/destination
```

Le système vous posera plusieurs questions :
- Passphrase
- Algorithme de chiffrement (choisissez AES)
- Taille de clé (256 bits)
- Chiffrer les noms de fichiers ? (oui pour plus de sécurité)

### Monter automatiquement au login

Configuration avancée possible via PAM, mais LUKS est généralement préféré pour cet usage.

---

## Chiffrer des fichiers individuels

### Avec GPG (GnuPG)

Pour chiffrer des fichiers individuels rapidement :

#### Chiffrer un fichier

```bash
gpg -c fichier_secret.txt
```

Entrez une passphrase. Un fichier `fichier_secret.txt.gpg` est créé.

#### Déchiffrer

```bash
gpg fichier_secret.txt.gpg
```

Entrez la passphrase. Le fichier original est restauré.

#### Options avancées

Spécifier l'algorithme de chiffrement :
```bash
gpg --symmetric --cipher-algo AES256 fichier.txt
```

### Avec OpenSSL

#### Chiffrer

```bash
openssl enc -aes-256-cbc -salt -in fichier.txt -out fichier.txt.enc
```

#### Déchiffrer

```bash
openssl enc -aes-256-cbc -d -in fichier.txt.enc -out fichier.txt
```

---

## Chiffrement des sauvegardes

### Duplicity (sauvegarde chiffrée)

**Duplicity** permet de créer des sauvegardes chiffrées et incrémentales.

#### Installation

```bash
sudo apt install duplicity
```

#### Sauvegarde chiffrée vers un dossier local

```bash
duplicity --encrypt-key VOTRE_CLE_GPG /home/utilisateur/Documents file:///mnt/sauvegarde
```

#### Restauration

```bash
duplicity restore file:///mnt/sauvegarde /home/utilisateur/Documents_restaures
```

### Restic (moderne et efficace)

**Restic** est un outil de sauvegarde moderne avec chiffrement intégré.

#### Installation

```bash
sudo apt install restic
```

#### Initialiser un dépôt

```bash
restic init --repo /mnt/sauvegarde
```

Entrez un mot de passe pour chiffrer le dépôt.

#### Créer une sauvegarde

```bash
restic backup ~/Documents --repo /mnt/sauvegarde
```

#### Restaurer

```bash
restic restore latest --repo /mnt/sauvegarde --target ~/Documents_restaures
```

---

## Bonnes pratiques de chiffrement

### Gestion des mots de passe

1. ✅ **Mots de passe forts** : 20+ caractères pour le chiffrement
2. ✅ **Différents mots de passe** : Chiffrement ≠ mot de passe utilisateur
3. ✅ **Stockage sécurisé** : Notez-les dans un gestionnaire de mots de passe ou un coffre physique
4. ✅ **Fichiers clés** : Combinez mot de passe + fichier clé pour une sécurité maximale
5. ❌ **Ne perdez jamais** : Sans le mot de passe, vos données sont perdues à jamais

### Sauvegardes

1. ✅ **Sauvegardez l'en-tête LUKS** : Essentiel pour la récupération
2. ✅ **Sauvegardez vos fichiers clés** : Dans plusieurs endroits sécurisés
3. ✅ **Testez la restauration** : Vérifiez régulièrement que vous pouvez déchiffrer
4. ✅ **Règle 3-2-1** : 3 copies, 2 supports différents, 1 copie hors site

### Performance

1. ✅ **AES-NI** : Vérifiez que votre processeur supporte l'accélération matérielle
   ```bash
   grep aes /proc/cpuinfo
   ```
2. ✅ **SSD et TRIM** : Activez TRIM pour les SSD chiffrés
   ```bash
   sudo fstrim -v /
   ```
3. ✅ **Ne sur-chiffrez pas** : Pas besoin de chiffrer /tmp ou les fichiers système

### Sécurité

1. ✅ **Démontez après usage** : Toujours fermer les volumes quand vous ne les utilisez pas
2. ✅ **Verrouillage automatique** : Configurez le verrouillage d'écran après inactivité
3. ✅ **Mise en veille chiffrée** : La RAM peut contenir des clés, hibernation = risque
4. ✅ **Mise à jour** : Gardez VeraCrypt et LUKS à jour
5. ❌ **Ne partagez pas les mots de passe** : Créez plusieurs slots de clés si besoin

### Légal et voyage

1. ⚠️ **Chiffrement et douanes** : Certains pays peuvent vous obliger à déchiffrer
2. ✅ **Volumes cachés** : Peuvent offrir une protection dans certains contextes
3. ✅ **Connaissez vos droits** : Renseignez-vous sur les lois locales
4. ✅ **Données dans le cloud** : Chiffrez avant d'uploader (VeraCrypt + Dropbox, etc.)

---

## Dépannage

### LUKS : "No key available with this passphrase"

**Problème** : Le mot de passe ne fonctionne pas.

**Solutions** :
1. Vérifiez les majuscules/minuscules
2. Vérifiez le layout clavier (AZERTY vs QWERTY)
3. Essayez les autres slots de clés
4. Restaurez l'en-tête sauvegardé :
   ```bash
   sudo cryptsetup luksHeaderRestore /dev/sdb1 --header-backup-file backup.img
   ```

### VeraCrypt : "Incorrect password or not a VeraCrypt volume"

**Problème** : Impossible de monter le volume.

**Solutions** :
1. Vérifiez le fichier/partition sélectionné
2. Essayez avec le mot de passe du volume caché (si vous en avez créé un)
3. Vérifiez que le fichier n'est pas corrompu
4. Désactivez temporairement "TrueCrypt Mode" dans les options

### Performance lente

**Problème** : Le chiffrement ralentit le système.

**Solutions** :
1. Vérifiez le support AES-NI :
   ```bash
   lscpu | grep aes
   ```
2. Mettez à jour le noyau Linux
3. Pour VeraCrypt, essayez un algorithme différent (AES vs Serpent)
4. Vérifiez que le disque n'est pas défectueux :
   ```bash
   sudo smartctl -a /dev/sda
   ```

### Volume monté en lecture seule

**Problème** : Impossible d'écrire sur le volume.

**Solutions** :
1. Vérifiez les permissions :
   ```bash
   sudo chmod 755 /mnt/mon_volume
   ```
2. Vérifiez le système de fichiers :
   ```bash
   sudo fsck /dev/mapper/volume_chiffre
   ```
3. Remontez en lecture-écriture :
   ```bash
   sudo mount -o remount,rw /mnt/mon_volume
   ```

---

## Commandes de référence rapide

### LUKS

| Commande | Description |
|----------|-------------|
| `sudo cryptsetup luksFormat /dev/sdX` | Créer un volume LUKS |
| `sudo cryptsetup luksOpen /dev/sdX nom` | Ouvrir un volume |
| `sudo cryptsetup luksClose nom` | Fermer un volume |
| `sudo cryptsetup luksAddKey /dev/sdX` | Ajouter une clé |
| `sudo cryptsetup luksRemoveKey /dev/sdX` | Supprimer une clé |
| `sudo cryptsetup luksChangeKey /dev/sdX` | Changer une clé |
| `sudo cryptsetup luksDump /dev/sdX` | Afficher les infos |
| `sudo cryptsetup luksHeaderBackup /dev/sdX --header-backup-file backup.img` | Sauvegarder l'en-tête |

### VeraCrypt

| Commande | Description |
|----------|-------------|
| `veracrypt` | Lancer l'interface graphique |
| `veracrypt /chemin/conteneur /point/montage` | Monter un conteneur |
| `veracrypt -d /point/montage` | Démonter |
| `veracrypt -d` | Démonter tous les volumes |
| `veracrypt -l` | Lister les volumes montés |

### GPG

| Commande | Description |
|----------|-------------|
| `gpg -c fichier.txt` | Chiffrer un fichier |
| `gpg fichier.txt.gpg` | Déchiffrer un fichier |
| `gpg --symmetric --cipher-algo AES256 fichier.txt` | Chiffrer avec AES-256 |

---

## Résumé

Le chiffrement des données est un pilier essentiel de la sécurité :

- **LUKS** : Idéal pour le chiffrement complet du système Linux
- **VeraCrypt** : Parfait pour les conteneurs portables et la compatibilité multi-OS
- **Combinaison recommandée** : LUKS pour le système + VeraCrypt pour les fichiers spécifiques
- **Sauvegardez vos clés** : Sans elles, vos données sont perdues
- **Mots de passe forts** : La sécurité de vos données en dépend

Le chiffrement protège vos données contre :
- Le vol physique de l'ordinateur
- L'accès non autorisé au disque dur
- La surveillance et l'espionnage
- La perte ou le vol de supports amovibles

Dans le prochain chapitre, nous explorerons les **bonnes pratiques de sécurité** globales pour compléter cette protection.

---


⏭️ [Bonnes pratiques de sécurité](/11-gestion-des-utilisateurs-et-securite/05-bonnes-pratiques-de-securite.md)
