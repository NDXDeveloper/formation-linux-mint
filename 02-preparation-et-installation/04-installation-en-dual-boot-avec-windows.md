🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 2.4 Installation en dual-boot avec Windows

## Introduction

L'installation en **dual-boot** (ou double démarrage) vous permet d'avoir **Windows et Linux Mint sur le même ordinateur**. À chaque démarrage, vous choisissez quel système utiliser.

### Qu'est-ce que le dual-boot ?

Le dual-boot consiste à installer deux systèmes d'exploitation sur le même ordinateur, chacun sur sa propre partition. Au démarrage, un menu vous permet de choisir lequel lancer.

> 💡 **Analogie** : C'est comme avoir deux appartements dans le même immeuble. Vous choisissez dans lequel entrer à chaque fois que vous rentrez chez vous.

### Avantages du dual-boot

- ✅ **Garder Windows** : Vous conservez votre système Windows habituel
- ✅ **Tester Linux** : Vous pouvez prendre votre temps pour apprendre Linux
- ✅ **Compatibilité** : Accès aux logiciels Windows quand nécessaire
- ✅ **Flexibilité** : Basculez entre les deux systèmes selon vos besoins
- ✅ **Sécurité** : Un système de secours si l'autre a un problème

### Inconvénients à connaître

- ⚠️ **Espace disque** : Nécessite de partager l'espace entre les deux systèmes
- ⚠️ **Redémarrage** : Il faut redémarrer pour changer de système
- ⚠️ **Complexité** : Un peu plus technique qu'une installation simple
- ⚠️ **Risque** : Manipulation des partitions (avec précautions)

---

## Prérequis essentiels

Avant de commencer, vérifiez ces éléments importants :

### Espace disque disponible

Vous avez besoin d'**au moins 30 Go libres** sur votre disque dur :
- **Minimum** : 20 Go (système uniquement, serré)
- **Recommandé** : 50 Go (confortable pour un usage quotidien)
- **Idéal** : 100 Go ou plus (pour logiciels, fichiers, etc.)

**Comment vérifier l'espace disponible sur Windows :**
1. Ouvrez **Explorateur de fichiers**
2. Cliquez sur **Ce PC**
3. Regardez l'espace libre sur votre disque C: (ou autre)

### Sauvegarde OBLIGATOIRE

> ⚠️ **ATTENTION** : Avant toute installation, **sauvegardez vos données importantes**. Même si le risque est faible, une erreur de manipulation peut entraîner une perte de données.

**Que sauvegarder :**
- 📄 Documents personnels
- 📸 Photos et vidéos
- 🎵 Musique
- 📧 Emails (si stockés localement)
- 🔖 Favoris du navigateur
- 🎮 Sauvegardes de jeux
- 🔑 Mots de passe et clés de licence

**Où sauvegarder :**
- Disque dur externe
- Clé USB (si peu de données)
- Service cloud (Google Drive, OneDrive, etc.)
- DVD (si disponible)

> 💡 **Conseil** : Faites même une **image système** complète de Windows avec un outil comme Macrium Reflect (gratuit) pour pouvoir tout restaurer en cas de problème.

### Désactiver le démarrage rapide de Windows

Windows 10/11 utilise un "démarrage rapide" qui peut causer des problèmes avec le dual-boot.

**Étapes pour le désactiver :**

1. **Ouvrez le Panneau de configuration**
   - Recherchez "Panneau de configuration" dans le menu Démarrer
   - Ou : Touche Windows + X → Panneau de configuration

2. **Options d'alimentation**
   - Cliquez sur **Matériel et audio** (ou **Système et sécurité**)
   - Cliquez sur **Options d'alimentation**

3. **Paramètres d'alimentation**
   - Cliquez sur **Choisir l'action des boutons d'alimentation** (menu de gauche)

4. **Paramètres système**
   - Cliquez sur **Modifier des paramètres actuellement non disponibles**
   - Acceptez les droits administrateur si demandés

5. **Désactiver le démarrage rapide**
   - **Décochez** la case **"Activer le démarrage rapide"**
   - Cliquez sur **Enregistrer les modifications**

> 💡 **Pourquoi ?** Le démarrage rapide met Windows en hibernation au lieu de l'éteindre complètement, ce qui verrouille les partitions et peut empêcher Linux d'y accéder correctement.

### Désactiver BitLocker (si activé)

Si votre disque Windows est chiffré avec **BitLocker**, vous devez le désactiver temporairement :

1. **Panneau de configuration** → **Système et sécurité** → **Chiffrement de lecteur BitLocker**
2. Cliquez sur **Désactiver BitLocker** pour votre disque C:
3. Attendez la fin du déchiffrement (peut prendre du temps)

> ⚠️ Vous pourrez réactiver BitLocker après l'installation si souhaité.

### Désactiver Secure Boot (si nécessaire)

Certains ordinateurs nécessitent de désactiver Secure Boot :

1. Accédez au **BIOS/UEFI** (F2, Suppr au démarrage)
2. Cherchez l'option **"Secure Boot"** (souvent dans Boot ou Security)
3. Mettez-le sur **"Disabled"**
4. Sauvegardez et quittez (F10)

> 💡 **Note** : Linux Mint récent supporte Secure Boot, mais en cas de problème, vous pouvez le désactiver.

### Défragmenter le disque (Windows avec HDD)

Si vous avez un **disque dur mécanique** (HDD, pas SSD) :

1. Ouvrez **Ce PC**
2. **Clic droit** sur votre disque C: → **Propriétés**
3. Onglet **Outils** → **Optimiser**
4. Sélectionnez le disque et cliquez **Optimiser**

> ⚠️ **Ne défragmentez JAMAIS un SSD**, cela l'userait inutilement. Windows gère les SSD automatiquement.

---

## Étape 1 : Libérer de l'espace pour Linux

Avant d'installer Linux Mint, vous devez créer de l'espace non alloué sur votre disque dur.

### Méthode 1 : Depuis Windows (Recommandé pour débutants)

C'est la méthode la plus simple et la plus sûre.

#### Ouvrir la Gestion des disques

1. **Touche Windows + X** → **Gestion des disques**
2. Ou : **Clic droit** sur le menu Démarrer → **Gestion des disques**
3. Ou : Recherchez "gestion des disques" dans le menu Démarrer

#### Identifier votre partition Windows

Vous verrez une représentation graphique de vos disques :
- **Disque 0** (ou Disque 1, etc.) : Votre disque dur principal
- **Partitions** : Sections du disque
  - **Partition de récupération** : 450-500 Mo (ne pas toucher)
  - **Partition EFI/Système** : 100-500 Mo (ne pas toucher)
  - **Partition C:** : Votre Windows (c'est celle-ci que nous allons réduire)
  - **Autres partitions** : Selon votre configuration

#### Réduire la partition Windows

1. **Clic droit** sur la partition **C:** (la plus grande, celle de Windows)
2. Sélectionnez **"Réduire le volume"**
3. Windows calcule l'espace disponible (patientez quelques secondes)

4. **Entrez la quantité à libérer** dans "Quantité d'espace à réduire (Mo)" :
   - Pour **50 Go** → Entrez **51200** Mo
   - Pour **100 Go** → Entrez **102400** Mo
   - Pour **200 Go** → Entrez **204800** Mo

5. Cliquez sur **"Réduire"**
6. Attendez la fin de l'opération (quelques secondes à quelques minutes)

#### Vérification

- Vous devriez maintenant voir un espace **"Non alloué"** (noir dans le graphique)
- Cet espace sera utilisé pour installer Linux Mint
- **Ne créez PAS de nouvelle partition** dans cet espace, Linux le fera automatiquement

> 💡 **Important** : Laissez cet espace non alloué tel quel. L'installateur Linux Mint s'en occupera.

### Méthode 2 : Pendant l'installation de Linux (Alternative)

Vous pouvez aussi laisser l'installateur Linux Mint réduire Windows automatiquement. Nous verrons cela plus loin.

---

## Étape 2 : Démarrer l'installation

### Démarrer en mode Live

1. **Insérez votre clé USB** bootable Linux Mint
2. **Redémarrez** l'ordinateur
3. **Accédez au Boot Menu** (F12, F11, ou autre selon votre PC)
4. Sélectionnez votre **clé USB**
5. Choisissez **"Start Linux Mint"** dans le menu

### Lancer l'installateur

Une fois dans le mode Live :

1. Double-cliquez sur l'icône **"Install Linux Mint"** sur le bureau
2. Ou : **Menu** → **Administration** → **Install Linux Mint**

L'assistant d'installation se lance.

---

## Étape 3 : Assistant d'installation

L'installateur de Linux Mint est un assistant en plusieurs étapes. Suivez attentivement chaque écran.

### Écran 1 : Langue

- Sélectionnez **"Français"** dans la liste
- Cliquez sur **"Continuer"**

### Écran 2 : Disposition du clavier

- Le système détecte généralement **"Français"** automatiquement
- Vous pouvez tester en tapant dans la zone de texte en bas
- Tapez des accents (é, è, à, ç) pour vérifier
- Cliquez sur **"Continuer"**

### Écran 3 : Codecs multimédia

L'installateur demande si vous voulez installer les **codecs multimédia** (MP3, DVD, Flash, etc.)

**Options :**
- ☑️ **"Installer les codecs multimédia"** (Recommandé)
  - Permet de lire MP3, vidéos, DVD, etc.
  - Nécessite une connexion Internet
  - Télécharge environ 50-100 Mo

> 💡 **Conseil** : Cochez cette option. C'est pratique d'avoir les codecs dès le début.

- Cliquez sur **"Continuer"**

### Écran 4 : Type d'installation (CRUCIAL)

C'est **l'écran le plus important** pour le dual-boot. Lisez attentivement !

#### Options proposées

L'installateur détecte Windows et propose généralement :

**Option 1 : Installer Linux Mint à côté de Windows** (Recommandée pour débutants)
```
┌────────────────────────────────────────┐
│ ● Installer Linux Mint à côté de       │
│   Windows Boot Manager                 │
│                                        │
│   L'installateur redimensionnera       │
│   automatiquement les partitions       │
└────────────────────────────────────────┘
```
- ✅ **Recommandé pour débutants**
- ✅ Automatique et sûr
- ✅ L'installateur gère tout
- ✅ Dual-boot configuré automatiquement

**Option 2 : Effacer le disque et installer Linux Mint**
```
┌────────────────────────────────────────┐
│ ○ Effacer le disque et installer       │
│   Linux Mint                           │
│                                        │
│   ⚠️ ATTENTION : Supprime Windows !    │
└────────────────────────────────────────┘
```
- ❌ **NE PAS CHOISIR** pour le dual-boot
- ⚠️ Supprime complètement Windows
- ⚠️ Toutes vos données Windows seront perdues
- ✅ À utiliser seulement si vous voulez remplacer Windows entièrement

**Option 3 : Autre chose (Avancé)**
```
┌────────────────────────────────────────┐
│ ○ Autre chose                          │
│                                        │
│   Créer, redimensionner ou supprimer   │
│   des partitions manuellement          │
└────────────────────────────────────────┘
```
- 🔧 Contrôle manuel complet
- 🎓 Pour utilisateurs avancés
- 📐 Permet un partitionnement personnalisé

> ⚠️ **IMPORTANT** : Pour un dual-boot automatique et simple, choisissez l'**Option 1**.

### Option 1 : Installation automatique (Débutants)

Si vous choisissez **"Installer Linux Mint à côté de Windows"** :

#### Répartition de l'espace

L'installateur affiche un **curseur** pour partager l'espace entre Windows et Linux :

```
Windows ──────────────●───────── Linux
         70%         30%
```

**Ajustez le curseur :**
- Déplacez-le vers la **gauche** : Plus d'espace pour Linux
- Déplacez-le vers la **droite** : Plus d'espace pour Windows

**Recommandations :**
- Laissez **au moins 100 Go à Windows** si vous l'utilisez régulièrement
- Donnez **au moins 50 Go à Linux** pour être confortable
- Exemple : Sur un disque de 500 Go, faites 300 Go Windows / 200 Go Linux

#### Aperçu des changements

L'installateur montre :
- **Avant** : Vos partitions actuelles
- **Après** : Comment elles seront modifiées

Vérifiez que :
- ✅ Windows garde suffisamment d'espace
- ✅ Linux aura suffisamment d'espace
- ✅ Vos données Windows ne seront pas supprimées

#### Continuer

- Cliquez sur **"Installer maintenant"**
- Une confirmation s'affiche listant les changements
- **Lisez attentivement** la liste des modifications
- Si tout est correct, cliquez **"Continuer"**

> 🔒 C'est le dernier point avant que les modifications soient écrites sur le disque.

### Option 3 : Installation manuelle (Avancé)

Si vous choisissez **"Autre chose"**, vous accédez à l'outil de partitionnement manuel.

> 💡 **Pour débutants** : Cette option est plus complexe. Utilisez l'Option 1 sauf si vous avez des besoins spécifiques.

#### Interface de partitionnement

Vous verrez un tableau listant toutes vos partitions :

```
Périphérique    Type       Point de montage    Taille    Utilisé
/dev/sda1       efi        /boot/efi           512 Mo    200 Mo
/dev/sda2       ntfs                          400 Go    250 Go
/dev/sda3       (espace libre)                100 Go        -
```

#### Créer les partitions Linux

Vous devez créer **au moins deux partitions** :

**1. Partition racine (/) - Obligatoire**
- Taille : Au moins 20 Go (30-50 Go recommandé)
- Type : ext4
- Point de montage : `/`

**2. Partition swap (optionnelle mais recommandée)**
- Taille : Égale à votre RAM (ou 4-8 Go)
- Type : swap
- Usage : Mémoire virtuelle, hibernation

**3. Partition home (/home) - Optionnelle**
- Taille : Espace restant
- Type : ext4
- Point de montage : `/home`
- Avantage : Vos fichiers personnels séparés du système

#### Étapes de création

Pour chaque partition :

1. Sélectionnez l'**espace libre**
2. Cliquez sur le bouton **"+"** (Ajouter)
3. Configurez :
   - **Taille** : Entrez la taille en Mo
   - **Type** : Partition primaire (ou logique)
   - **Emplacement** : Début ou fin de l'espace
   - **Utiliser comme** : Système de fichiers ext4 (ou swap)
   - **Point de montage** : `/` ou `/home` ou autre
4. Cliquez sur **"OK"**
5. Répétez pour les autres partitions

#### Configuration du chargeur de démarrage

En bas de l'écran :
- **"Périphérique où sera installé le programme de démarrage"**
- Sélectionnez votre **disque principal** (ex: `/dev/sda`)
- **PAS** une partition spécifique, mais le disque entier

> ⚠️ **Important** : Le chargeur de démarrage (GRUB) doit être installé sur le disque principal, pas sur une partition.

#### Vérification finale

Avant de cliquer "Installer maintenant" :
- ✅ Vérifiez que vous n'avez **pas formaté** les partitions Windows
- ✅ Vérifiez que le point de montage `/` existe
- ✅ Vérifiez que GRUB s'installe sur le bon disque

---

## Étape 4 : Configuration du système

Après avoir validé le partitionnement, l'installation continue avec quelques questions.

### Écran 5 : Fuseau horaire

1. L'installateur détecte généralement votre localisation
2. Vérifiez que **"Paris"** ou votre ville est sélectionnée
3. Ou cliquez sur la carte pour sélectionner votre zone
4. Cliquez sur **"Continuer"**

### Écran 6 : Informations personnelles

Créez votre compte utilisateur :

**Votre nom :**
- Entrez votre prénom et nom (ex: "Jean Dupont")
- Utilisé pour l'identification

**Nom de l'ordinateur :**
- Nom qui identifie votre PC sur le réseau
- Par défaut : votre prénom + "-mint" (ex: "jean-mint")
- Vous pouvez le personnaliser

**Nom d'utilisateur :**
- Identifiant pour vous connecter
- Généralement votre prénom en minuscules (ex: "jean")
- Pas d'espaces, pas d'accents

**Mot de passe :**
- Choisissez un **mot de passe sécurisé**
- Au moins 8 caractères
- Mélange de lettres, chiffres, symboles
- **Notez-le** dans un endroit sûr !

**Confirmer le mot de passe :**
- Retapez exactement le même mot de passe

**Options de connexion :**

```
● Demander mon mot de passe pour ouvrir une session
○ Ouvrir une session automatiquement
☐ Chiffrer mon dossier personnel
```

- **Demander le mot de passe** : Recommandé pour la sécurité
- **Connexion automatique** : Pratique mais moins sécurisé
- **Chiffrer le dossier** : Sécurise vos fichiers (déchiffrement automatique, légère perte de performance)

> 💡 **Conseil** : Pour un PC personnel, la connexion automatique est acceptable. Pour un PC portable ou partagé, demandez toujours le mot de passe.

Cliquez sur **"Continuer"**.

---

## Étape 5 : Installation en cours

L'installation commence ! L'installateur copie les fichiers sur votre disque.

### Ce qui se passe

- 📦 Copie des fichiers système
- 🔧 Installation des logiciels
- ⚙️ Configuration du système
- 🥾 Installation du chargeur de démarrage GRUB
- 🎨 Application des paramètres

### Diaporama

Pendant l'installation, un **diaporama** vous présente Linux Mint :
- Fonctionnalités principales
- Applications incluses
- Conseils d'utilisation
- Liens vers la documentation

### Durée

- ⏱️ **Temps moyen** : 10 à 30 minutes
- Dépend de la vitesse de votre ordinateur et de la clé USB
- Vous pouvez continuer à utiliser le mode Live pendant ce temps

### Barre de progression

Une barre de progression indique l'avancement :
```
Installation du système de base...
[████████████████────────] 60%
```

> 💡 Soyez patient, ne forcez pas l'arrêt ou le redémarrage pendant l'installation.

---

## Étape 6 : Fin de l'installation

### Message de succès

Quand l'installation est terminée, un message s'affiche :

```
┌──────────────────────────────────────┐
│  ✓ L'installation est terminée       │
│                                      │
│  Vous devez redémarrer l'ordinateur  │
│  pour utiliser le nouveau système    │
│                                      │
│  [Continuer à tester] [Redémarrer]   │
└──────────────────────────────────────┘
```

### Options

**Continuer à tester :**
- Reste en mode Live
- Vous pouvez continuer à explorer
- Redémarrez quand vous êtes prêt

**Redémarrer maintenant :** (Recommandé)
- Redémarre immédiatement
- Permet de démarrer sur votre nouveau système

### Redémarrage

1. Cliquez sur **"Redémarrer maintenant"**
2. Le système va se fermer
3. Un message s'affiche : **"Veuillez retirer le support d'installation et appuyer sur Entrée"**
4. **Retirez la clé USB**
5. Appuyez sur **Entrée**
6. L'ordinateur redémarre

---

## Étape 7 : Premier démarrage (GRUB)

### Le menu GRUB

Au redémarrage, vous verrez le **menu GRUB** (GRand Unified Bootloader) :

```
GNU GRUB version 2.06
┌─────────────────────────────────────┐
│ *Linux Mint 22.1 Cinnamon           │
│  Options avancées pour Linux Mint   │
│  Windows Boot Manager               │
│  Configuration du Firmware UEFI     │
└─────────────────────────────────────┘
```

### Options du menu

**Linux Mint 22.1 Cinnamon :**
- Démarre Linux Mint normalement
- **C'est l'option par défaut**
- Sélectionnée automatiquement après 10 secondes

**Options avancées pour Linux Mint :**
- Modes de démarrage spéciaux
- Mode recovery (dépannage)
- Anciens kernels
- Utilisé en cas de problème

**Windows Boot Manager :**
- Démarre Windows normalement
- Accès à votre ancien système Windows
- Toutes vos données Windows sont intactes

**Configuration du Firmware UEFI :**
- Accès au BIOS/UEFI
- Modifier les paramètres matériels

### Sélection du système

**Pour démarrer Linux Mint :**
- Ne touchez à rien, patientez 10 secondes
- Ou appuyez sur **Entrée**

**Pour démarrer Windows :**
- Utilisez les **flèches haut/bas** pour sélectionner "Windows Boot Manager"
- Appuyez sur **Entrée**

> 💡 **C'est ça le dual-boot !** Vous choisissez à chaque démarrage quel système utiliser.

### Premier démarrage Linux Mint

1. Linux Mint démarre (logo avec points animés)
2. Écran de connexion s'affiche
3. Entrez votre **mot de passe**
4. Appuyez sur **Entrée**
5. Le bureau Linux Mint se charge

---

## Étape 8 : Configuration post-installation

### Écran de bienvenue

Au premier démarrage, l'**écran de bienvenue** s'affiche automatiquement.

#### Onglet "Premiers pas"

L'assistant propose plusieurs actions :

**1. Gestionnaire de pilotes**
- Détecte les pilotes propriétaires nécessaires
- Important pour carte graphique NVIDIA, WiFi, etc.
- Cliquez pour lancer

**2. Gestionnaire de mises à jour**
- Vérifie les mises à jour disponibles
- Installe les derniers correctifs de sécurité
- **Recommandé de lancer immédiatement**

**3. Instantanés système (Timeshift)**
- Configure les sauvegardes automatiques
- Permet de restaurer le système en cas de problème
- **Hautement recommandé**

**4. Pare-feu**
- Active le pare-feu système
- Protection réseau basique
- Recommandé

**5. Comptes en ligne**
- Synchronise vos comptes (Google, Microsoft, etc.)
- Optionnel

> 💡 **Faites au moins** : Mises à jour, Timeshift, et Pilotes.

### Installer les mises à jour

1. Cliquez sur **"Gestionnaire de mises à jour"** dans l'écran de bienvenue
2. Ou : **Menu** → **Administration** → **Gestionnaire de mises à jour**
3. Cliquez sur **"Installer les mises à jour"**
4. Entrez votre mot de passe
5. Attendez la fin (10-30 minutes selon les mises à jour)
6. Redémarrez si demandé

### Configurer Timeshift

1. Cliquez sur **"Instantanés système"** ou lancez Timeshift
2. Suivez l'assistant :
   - **Type** : RSYNC (recommandé pour débutants)
   - **Disque** : Sélectionnez votre partition Linux
   - **Planification** : Quotidien ou hebdomadaire
   - **Niveaux** : Gardez les paramètres par défaut
3. Timeshift créera le premier instantané

> 💡 **Timeshift** est comme un point de restauration Windows. En cas de problème, vous pourrez revenir à cet état.

### Installer les pilotes

1. **Menu** → **Administration** → **Gestionnaire de pilotes**
2. Attendez la détection (quelques secondes)
3. Si des pilotes sont disponibles, ils s'affichent
4. Sélectionnez les pilotes **recommandés** (généralement pré-sélectionnés)
5. Cliquez sur **"Appliquer les changements"**
6. Redémarrez après l'installation

**Pilotes courants :**
- **NVIDIA** : Pour cartes graphiques NVIDIA
- **WiFi** : Broadcom, Realtek
- **Microcode** : Pour processeurs Intel/AMD

---

## Vérification du dual-boot

### Tester le basculement

Pour vérifier que tout fonctionne :

**Test 1 : Linux → Windows**
1. Dans Linux Mint, cliquez sur **Menu** → **Arrêter** → **Redémarrer**
2. Au menu GRUB, sélectionnez **"Windows Boot Manager"**
3. Windows démarre normalement
4. Vérifiez que tout fonctionne dans Windows

**Test 2 : Windows → Linux**
1. Dans Windows, cliquez sur **Démarrer** → **Redémarrer**
2. Au menu GRUB, sélectionnez **"Linux Mint"** (ou patientez)
3. Linux Mint démarre normalement

> ✅ Si les deux systèmes démarrent correctement, votre dual-boot est un succès !

### Vérifier l'espace disque

**Dans Windows :**
1. Ouvrez **Gestion des disques**
2. Vous devriez voir :
   - Votre partition Windows (réduite)
   - Des partitions Linux (ext4, swap)
   - Tout est normal !

**Dans Linux Mint :**
1. **Menu** → **Système** → **Disques**
2. Vous voyez toutes vos partitions
3. Vos partitions Windows sont visibles mais non montées par défaut

---

## Accéder aux fichiers entre systèmes

### Accéder aux fichiers Windows depuis Linux

C'est **facile et sûr** :

1. Ouvrez le **Gestionnaire de fichiers** (Nemo)
2. Cliquez sur **"Ordinateur"** dans le menu latéral
3. Vos partitions Windows apparaissent (NTFS)
4. Double-cliquez pour les monter
5. Vous pouvez **lire et écrire** vos fichiers Windows

> 💡 Linux peut lire et modifier les fichiers sur les partitions Windows NTFS sans problème.

### Accéder aux fichiers Linux depuis Windows

C'est **plus complexe** :

Windows ne peut pas nativement lire les partitions Linux (ext4).

**Solutions :**

**Option 1 : Utiliser une partition commune**
- Créez une partition en **NTFS** ou **exFAT**
- Accessible depuis Windows ET Linux
- Idéal pour partager des fichiers

**Option 2 : Logiciel tiers**
- **Linux Reader** (gratuit) : Lecture seule
- **Ext2Fsd** : Lecture et écriture (avancé)
- **DiskInternals Linux Reader** : Interface simple

**Option 3 : Réseau local**
- Partagez des dossiers via le réseau
- Utilisez Samba (partage Windows)

> 💡 **Conseil** : La méthode la plus simple est d'accéder aux fichiers Windows depuis Linux, pas l'inverse.

---

## Personnaliser GRUB (optionnel)

Vous pouvez personnaliser le menu de démarrage GRUB.

### Changer le système par défaut

Par défaut, Linux Mint démarre automatiquement. Pour changer :

1. **Menu** → **Administration** → **Grub Customizer**
   - Si non installé : `sudo apt install grub-customizer`

2. Entrez votre mot de passe

3. Dans l'onglet **"Paramètres généraux"** :
   - **"Système d'exploitation par défaut"** : Sélectionnez Windows ou Linux
   - **"Délai avant le démarrage"** : Changez le temps (10 secondes par défaut)

4. Cliquez sur **"Enregistrer"**

### Via la ligne de commande

**Méthode alternative (avancée) :**

1. Ouvrez un terminal
2. Éditez le fichier de configuration :
   ```bash
   sudo nano /etc/default/grub
   ```

3. Modifiez ces lignes :
   ```
   GRUB_DEFAULT=0              # 0=Linux, 2=Windows (généralement)
   GRUB_TIMEOUT=10             # Secondes d'attente
   GRUB_TIMEOUT_STYLE=menu     # Afficher le menu
   ```

4. Sauvegardez : **Ctrl+O**, **Entrée**, **Ctrl+X**

5. Mettez à jour GRUB :
   ```bash
   sudo update-grub
   ```

### Changer le thème GRUB

Vous pouvez installer des thèmes pour rendre GRUB plus joli :

1. Téléchargez un thème GRUB (sites comme gnome-look.org)
2. Extrayez dans `/boot/grub/themes/`
3. Modifiez `/etc/default/grub` :
   ```
   GRUB_THEME="/boot/grub/themes/nom-du-theme/theme.txt"
   ```
4. `sudo update-grub`

---

## Problèmes courants et solutions

### GRUB ne s'affiche pas, Windows démarre directement

**Cause :** Windows a pris le contrôle du démarrage

**Solution :**

1. Démarrez sur la clé USB Linux Mint (mode Live)
2. Ouvrez un terminal
3. Réinstallez GRUB :
   ```bash
   sudo add-apt-repository ppa:yannubuntu/boot-repair
   sudo apt update
   sudo apt install boot-repair
   boot-repair
   ```
4. Lancez **Boot-Repair**
5. Cliquez sur **"Réparation recommandée"**
6. Suivez les instructions
7. Redémarrez

### Windows n'apparaît pas dans GRUB

**Solution :**

1. Dans Linux Mint, ouvrez un terminal
2. Mettez à jour GRUB :
   ```bash
   sudo update-grub
   ```
3. GRUB détectera Windows automatiquement
4. Redémarrez pour vérifier

### Erreur "no such partition" au démarrage

**Cause :** UUID de partition a changé

**Solution :**
1. Démarrez en mode Live
2. Utilisez Boot-Repair (voir ci-dessus)

### L'heure est décalée entre Windows et Linux

**Cause :** Windows et Linux gèrent l'heure différemment

**Solution (depuis Linux) :**

```bash
timedatectl set-local-rtc 1 --adjust-system-clock
```

Ou **depuis Windows** (dans l'Éditeur du Registre) :

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation  
RealTimeIsUniversal = 1 (DWORD)  
```

### Windows a fait une mise à jour et GRUB a disparu

**Cause :** Certaines mises à jour Windows écrasent le bootloader

**Solution :**
- Utilisez Boot-Repair (voir plus haut)
- Ou réinstallez GRUB depuis le mode Live

---

## Désinstaller Linux Mint (retour à Windows seul)

Si vous voulez revenir à Windows uniquement :

### Étape 1 : Supprimer les partitions Linux (depuis Windows)

1. Démarrez sur **Windows**
2. **Touche Windows + X** → **Gestion des disques**
3. **Clic droit** sur chaque partition Linux (ext4, swap)
4. **Supprimer le volume**
5. Répétez pour toutes les partitions Linux
6. Vous aurez de l'espace **Non alloué**
7. **Clic droit** sur votre partition Windows → **Étendre le volume**
8. Récupérez tout l'espace libre

### Étape 2 : Restaurer le bootloader Windows

1. Créez une **clé USB Windows** (Media Creation Tool)
2. Démarrez dessus
3. **Réparer l'ordinateur** → **Dépannage** → **Invite de commandes**
4. Tapez :
   ```
   bootrec /fixmbr
   bootrec /fixboot
   bootrec /rebuildbcd
   ```
5. Redémarrez
6. Windows démarre directement, GRUB est supprimé

---

## Questions fréquentes

### Quel système démarre par défaut ?

Par défaut, **Linux Mint** démarre automatiquement après 10 secondes. Vous pouvez changer cela dans les paramètres GRUB.

### Puis-je accéder à mes fichiers Windows depuis Linux ?

**Oui, totalement !** Linux peut lire et écrire sur les partitions NTFS de Windows sans problème.

### Windows peut-il accéder aux fichiers Linux ?

**Difficilement.** Windows ne lit pas nativement ext4. La solution la plus simple est de créer une partition commune en NTFS/exFAT.

### Puis-je installer plusieurs distributions Linux ?

**Oui !** Vous pouvez avoir Windows + plusieurs Linux. GRUB listera tous les systèmes disponibles.

### Est-ce que Linux ralentit Windows ?

**Non, pas du tout.** Les deux systèmes sont indépendants. Les performances de Windows ne sont pas affectées.

### Combien d'espace dois-je donner à Linux ?

- **Minimum** : 20 Go (serré)
- **Confortable** : 50-100 Go
- **Idéal** : 100+ Go

Cela dépend de votre usage (jeux, vidéos, développement...).

### Puis-je redimensionner les partitions après installation ?

**Oui**, mais c'est plus délicat. Utilisez GParted depuis une clé USB Live. **Sauvegardez d'abord vos données !**

### Le dual-boot consomme-t-il plus d'énergie ?

**Non.** Seul un système tourne à la fois. La consommation est la même que si vous n'aviez qu'un seul système.

### Puis-je chiffrer Linux en dual-boot ?

**Oui**, mais c'est plus complexe. Il faut chiffrer lors de l'installation ou après avec LUKS. **Pour débutants, évitez le chiffrement complet.**

---

## Étape suivante

Votre dual-boot est installé et fonctionnel ! Maintenant :

➡️ **[2.7 Premier démarrage et configuration initiale](./07-premier-demarrage-et-configuration-initiale.md)**

Découvrez comment configurer votre système Linux Mint pour une utilisation optimale.

---

## Ressources complémentaires

- 📖 [Guide d'installation officiel Linux Mint](https://linuxmint-installation-guide.readthedocs.io/)
- 🔧 [Boot-Repair - Documentation](https://help.ubuntu.com/community/Boot-Repair)
- 💬 [Forum Linux Mint - Section Dual-boot](https://forums.linuxmint.com)
- 🎥 [Vidéos d'installation en dual-boot](https://www.youtube.com/linuxmint)
- 📱 [Telegram Linux Mint France](https://t.me/linuxmintfr)

---

**Félicitations ! Vous avez réussi votre installation en dual-boot ! 🎉**

**Profitez du meilleur des deux mondes : Windows ET Linux Mint ! 🚀**

⏭️ [Installation complète (remplacement de l'OS)](/02-preparation-et-installation/05-installation-complete.md)
