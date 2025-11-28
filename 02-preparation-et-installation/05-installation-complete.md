🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 2.5 Installation complète (remplacement de l'OS)

## Introduction

L'installation complète consiste à **remplacer entièrement** votre système d'exploitation actuel (généralement Windows) par Linux Mint. C'est l'option la plus radicale, mais aussi la plus simple et la plus performante.

### Qu'est-ce qu'une installation complète ?

Avec cette méthode, Linux Mint devient **le seul système d'exploitation** sur votre ordinateur. Tout le disque dur est dédié à Linux Mint, sans partage avec un autre système.

> 💡 **Analogie** : C'est comme déménager dans une nouvelle maison et vendre l'ancienne. Vous ne gardez pas les deux, vous faites table rase pour repartir à zéro.

### Différence avec le dual-boot

| Installation complète | Dual-boot |
|----------------------|-----------|
| ❌ Windows est supprimé | ✅ Windows est conservé |
| ✅ Tout l'espace pour Linux | ⚠️ Espace partagé |
| ✅ Plus simple (un seul système) | ⚠️ Plus complexe (deux systèmes) |
| ✅ Performance optimale | ⚠️ Redémarrage pour changer |
| ❌ Pas de retour en arrière facile | ✅ Retour possible |

---

## ⚠️ AVERTISSEMENTS CRITIQUES

### Cette installation SUPPRIMERA TOUT

> 🔴 **ATTENTION MAXIMALE** : Cette procédure va **SUPPRIMER DÉFINITIVEMENT** :
> - ✗ Windows et tous ses fichiers système
> - ✗ TOUS vos documents, photos, vidéos, musiques
> - ✗ TOUS vos logiciels et applications
> - ✗ TOUS vos paramètres et configurations
> - ✗ Vos jeux et sauvegardes
> - ✗ Vos emails stockés localement
> - ✗ Vos mots de passe enregistrés
> - ✗ TOUT ce qui se trouve sur le disque

### C'est irréversible

Une fois l'installation lancée, **il n'y a pas de retour en arrière** simple. Vous ne pourrez récupérer vos données que depuis une sauvegarde préalable.

### Êtes-vous sûr(e) ?

Avant de continuer, posez-vous ces questions :

- ❓ Avez-vous **vraiment** besoin de supprimer Windows ?
- ❓ Ne préféreriez-vous pas un **dual-boot** pour garder les deux systèmes ?
- ❓ Avez-vous des logiciels Windows **indispensables** sans alternative Linux ?
- ❓ Êtes-vous **100% certain(e)** de vouloir passer à Linux uniquement ?

> 💡 **Conseil aux débutants** : Si vous hésitez, optez pour le **dual-boot** (chapitre 2.4). Vous pourrez toujours supprimer Windows plus tard quand vous serez à l'aise avec Linux.

---

## Quand choisir l'installation complète ?

### Situations adaptées

L'installation complète est idéale si :

- ✅ **Ordinateur ancien** que vous voulez "recycler" avec Linux
- ✅ **PC secondaire** dédié à Linux (pas votre machine principale)
- ✅ **Serveur** ou machine spécialisée
- ✅ **Vous êtes déjà familier** avec Linux (pas votre première fois)
- ✅ **Windows ne fonctionne plus** correctement
- ✅ **Vous n'utilisez plus Windows** du tout
- ✅ **Disque dur petit** (moins de 128 Go) où le dual-boot serait serré
- ✅ **Vous voulez la meilleure performance** possible

### Situations où éviter

- ❌ **Première fois avec Linux** : Testez d'abord en dual-boot
- ❌ **Logiciels Windows indispensables** : Office 365, Adobe Suite, jeux spécifiques, etc.
- ❌ **PC de travail** : Gardez Windows pour la compatibilité professionnelle
- ❌ **Vous n'avez jamais testé Linux** : Essayez d'abord le mode Live
- ❌ **Vous hésitez** : Le doute n'est pas bon signe, gardez Windows en dual-boot

---

## Prérequis OBLIGATOIRES

### 1. Sauvegarde complète (NON NÉGOCIABLE)

> 🔴 **CRITIQUE** : Vous **DEVEZ** sauvegarder TOUTES vos données avant de continuer. C'est la règle n°1, sans exception.

#### Que sauvegarder ?

Faites une liste et vérifiez chaque élément :

**Documents et fichiers personnels :**
- [ ] Documents (Bureau, Documents, Téléchargements)
- [ ] Photos et vidéos (toutes les sources)
- [ ] Musique et playlists
- [ ] Archives et fichiers compressés
- [ ] Projets personnels ou professionnels

**Données d'applications :**
- [ ] Emails (exportez-les si stockés localement)
- [ ] Contacts et calendriers
- [ ] Favoris du navigateur (Firefox, Chrome, Edge)
- [ ] Mots de passe (exportez depuis votre gestionnaire)
- [ ] Sauvegardes de jeux (Steam Cloud, dossiers manuels)
- [ ] Paramètres d'applications importantes

**Informations système :**
- [ ] Clés de licence Windows (notez-la pour la revente ou réinstallation future)
- [ ] Clés de produits (Office, logiciels payants)
- [ ] Pilotes spécifiques téléchargés
- [ ] Informations WiFi (nom et mot de passe de vos réseaux)

#### Où sauvegarder ?

Utilisez **plusieurs destinations** pour plus de sécurité (règle 3-2-1) :

**Support physique externe :**
- Disque dur externe (le plus pratique)
- Clé USB de grande capacité
- DVD/Blu-ray (si vous avez un graveur)

**Cloud (complémentaire) :**
- Google Drive
- OneDrive
- Dropbox
- Mega
- Autres services cloud

**NAS ou serveur :**
- Si vous avez un stockage réseau à la maison

> 💡 **Vérifiez votre sauvegarde** : Ouvrez quelques fichiers depuis la sauvegarde pour vous assurer qu'elle fonctionne.

### 2. Image système Windows (fortement recommandé)

En plus de la sauvegarde des fichiers, créez une **image complète de Windows** :

**Logiciels gratuits :**
- **Macrium Reflect Free** (recommandé, facile)
- **Clonezilla** (plus technique)
- Outil de sauvegarde Windows intégré

Cette image vous permettra de **restaurer Windows entièrement** si vous changez d'avis.

### 3. Clé USB bootable Linux Mint

- Créée selon le chapitre 2.2
- Testée en mode Live (chapitre 2.3)
- Au moins 4 Go, 8 Go recommandé

### 4. Configuration système requise

Vérifiez que votre ordinateur répond aux exigences :

**Minimum :**
- Processeur : 1 GHz (32 ou 64-bit)
- RAM : 1 Go (2 Go recommandé pour Cinnamon)
- Disque : 15 Go minimum
- Résolution : 1024×768

**Recommandé :**
- Processeur : 2 GHz dual-core
- RAM : 4 Go ou plus
- Disque : 50 Go ou plus
- Résolution : 1920×1080

### 5. Connexion Internet

- Câble Ethernet (recommandé) ou WiFi
- Permet d'installer les mises à jour et codecs pendant l'installation
- Optionnel mais fortement conseillé

### 6. Liste de vos logiciels

Notez tous vos logiciels Windows essentiels et trouvez leurs **alternatives Linux** :

| Logiciel Windows | Alternative Linux |
|------------------|-------------------|
| Microsoft Office | LibreOffice, OnlyOffice |
| Adobe Photoshop | GIMP, Krita |
| Adobe Premiere | Kdenlive, DaVinci Resolve |
| Notepad++ | Gedit, Kate, Vim |
| iTunes | Rhythmbox, Clementine |
| Outlook | Thunderbird, Evolution |

Consultez le chapitre **3.4 Alternatives aux logiciels Windows** pour plus de détails.

---

## Étape 1 : Vérifications finales

Avant de démarrer l'installation, faites ces vérifications **une dernière fois** :

### Checklist finale

- [ ] ✅ **Toutes mes données sont sauvegardées** (j'ai vérifié)
- [ ] ✅ **J'ai une image système Windows complète** (au cas où)
- [ ] ✅ **Ma clé USB bootable est prête**
- [ ] ✅ **J'ai testé Linux Mint en mode Live** et tout fonctionne
- [ ] ✅ **Je connais les alternatives** à mes logiciels Windows essentiels
- [ ] ✅ **Je suis 100% certain** de vouloir supprimer Windows
- [ ] ✅ **J'ai noté mes mots de passe** importants
- [ ] ✅ **L'ordinateur est branché** sur secteur (si laptop)
- [ ] ✅ **J'ai du temps devant moi** (1-2 heures)

> ⚠️ Si vous hésitez sur UN SEUL point, arrêtez-vous et réfléchissez encore.

### Dernier moment pour changer d'avis

**Questions de dernière minute :**

1. **"Et si je regrette ?"**
   - Vous pourrez réinstaller Windows depuis une clé USB Windows
   - Mais vous perdrez du temps et devrez tout reconfigurer
   - Le dual-boot permet de tester sans risque

2. **"Puis-je vraiment tout faire sous Linux ?"**
   - 95% des tâches courantes : OUI
   - Gaming : OUI (avec Steam/Proton) mais pas tous les jeux
   - Logiciels professionnels spécifiques : parfois NON
   - Consultez les chapitres dédiés (Gaming, Applications Windows)

3. **"C'est vraiment irréversible ?"**
   - Techniquement, vous pouvez réinstaller Windows
   - Mais vous perdrez tout ce qui n'est pas sauvegardé
   - C'est compliqué et long

> 💡 **Conseil final** : Si vous avez encore des doutes, faites un dual-boot. Après 6 mois sans utiliser Windows, vous pourrez toujours le supprimer.

---

## Étape 2 : Démarrer l'installation

### Démarrer en mode Live

1. **Insérez la clé USB** bootable Linux Mint
2. **Redémarrez** l'ordinateur
3. **Accédez au Boot Menu** (F12, F11, Échap, selon votre PC)
4. Sélectionnez votre **clé USB**
5. Au menu Linux Mint, choisissez **"Start Linux Mint"**

### Lancer l'installateur

Une fois dans le bureau Linux Mint en mode Live :

1. Double-cliquez sur l'icône **"Install Linux Mint"** sur le bureau
2. Ou : **Menu** → **Administration** → **Install Linux Mint**
3. L'assistant d'installation démarre

---

## Étape 3 : Assistant d'installation

### Écran 1 : Langue

- Sélectionnez **"Français"** dans la liste
- Cliquez sur **"Continuer"**

### Écran 2 : Disposition du clavier

- Le système détecte généralement **"Français"** automatiquement
- Vérifiez en tapant dans la zone de test : `àéèùç`
- Cliquez sur **"Continuer"**

### Écran 3 : Codecs multimédia

- ☑️ **"Installer les codecs multimédia"** (Recommandé)
  - MP3, DVD, Flash, etc.
  - Nécessite une connexion Internet
  - Gain de temps (sinon à installer après)

- Cliquez sur **"Continuer"**

### Écran 4 : Type d'installation (CRITIQUE)

C'est l'écran **le plus important**. Lisez attentivement.

#### Options proposées

L'installateur détecte votre système actuel et propose :

**Option 1 : Installer Linux Mint à côté de [OS actuel]**
```
┌────────────────────────────────────────┐
│ ○ Installer Linux Mint à côté de       │
│   Windows Boot Manager                 │
│                                        │
│   Crée un dual-boot                    │
└────────────────────────────────────────┘
```
- ❌ **Ce n'est PAS ce que nous voulons ici**
- C'est pour le dual-boot (chapitre 2.4)

**Option 2 : Effacer le disque et installer Linux Mint** ⭐
```
┌────────────────────────────────────────┐
│ ● Effacer le disque et installer       │
│   Linux Mint                           │
│                                        │
│   ⚠️ Supprime tout sur le disque       │
└────────────────────────────────────────┘
```
- ✅ **C'EST L'OPTION À CHOISIR**
- Supprime TOUT et installe Linux Mint
- Configuration automatique optimale
- **Recommandé pour cette installation complète**

**Option 3 : Autre chose**
```
┌────────────────────────────────────────┐
│ ○ Autre chose                          │
│                                        │
│   Partitionnement manuel avancé        │
└────────────────────────────────────────┘
```
- 🔧 Contrôle manuel complet
- Pour utilisateurs avancés
- Permet un partitionnement personnalisé (voir chapitre 2.6)

#### Choisir l'option d'effacement

1. Sélectionnez **"Effacer le disque et installer Linux Mint"** (deuxième option)

2. Un **dernier avertissement** s'affiche :

```
┌─────────────────────────────────────────────┐
│  ⚠️  ATTENTION                              │
│                                             │
│  Cette action va SUPPRIMER toutes les       │
│  données du disque suivant :                │
│                                             │
│  /dev/sda (500 GB WDC WD5000...)            │
│                                             │
│  Êtes-vous absolument certain de            │
│  vouloir continuer ?                        │
│                                             │
│  [Retour]  [Continuer quand même]           │
└─────────────────────────────────────────────┘
```

3. **LISEZ attentivement** ce message

4. **Vérifiez le disque** mentionné :
   - C'est bien votre disque dur principal ?
   - La capacité correspond ?
   - Vous n'allez pas effacer un disque externe par erreur ?

5. **Dernière vérification** :
   - Mes données sont sauvegardées ✓
   - Je suis certain de vouloir continuer ✓
   - C'est le bon disque ✓

6. Cliquez sur **"Continuer"** (si vous êtes sûr à 100%)

> 🔴 **DERNIER POINT DE NON-RETOUR** : Après ce clic, l'effacement commence. Il n'y a plus de retour en arrière possible.

### Options avancées (optionnel)

Avant de cliquer sur "Continuer", vous pouvez configurer :

#### Chiffrement du disque

```
☐ Chiffrer la nouvelle installation de Linux Mint pour plus de sécurité
```

**Avantages du chiffrement :**
- 🔒 Vos données sont cryptées
- 🔒 Protection en cas de vol du PC
- 🔒 Personne ne peut accéder à vos fichiers sans le mot de passe

**Inconvénients :**
- 🔑 Mot de passe obligatoire à chaque démarrage
- ⚡ Légère baisse de performance (5-10%)
- 🔐 Impossible de récupérer si mot de passe oublié

> 💡 **Pour débutants** : Le chiffrement n'est pas nécessaire pour un PC personnel à la maison. À considérer pour un laptop qui voyage.

**Si vous activez le chiffrement :**
1. Cochez la case
2. Un écran supplémentaire demandera une **clé de sécurité**
3. Choisissez un **mot de passe fort** (pas le même que votre compte)
4. **NOTEZ-LE** dans un endroit sûr
5. **IMPORTANT** : Si vous perdez ce mot de passe, vous perdez TOUTES vos données

#### LVM (Logical Volume Manager)

```
☐ Utiliser LVM avec la nouvelle installation de Linux Mint
```

**LVM permet :**
- Redimensionner les partitions facilement après installation
- Créer des snapshots
- Gestion avancée du stockage

> 💡 **Pour débutants** : Laissez décoché. LVM est utile pour les serveurs ou utilisateurs avancés.

### Sélection du disque

Si vous avez **plusieurs disques** (rare sur un PC fixe, fréquent sur des serveurs) :

```
Installation du système sur :
● /dev/sda (500 GB WDC WD5000...)
○ /dev/sdb (1000 GB Seagate...)
```

**Vérifiez attentivement** :
- Sélectionnez le disque où vous voulez installer Linux
- **Attention** : Tout sera effacé sur ce disque
- Les autres disques ne seront pas touchés

### Confirmation finale

1. Vérifiez **une dernière fois** le résumé :
   ```
   Les partitions suivantes seront formatées :
   - /dev/sda1 (512 MB - EFI)
   - /dev/sda2 (498 GB - ext4 - /)

   ⚠️ ATTENTION : Toutes les données seront perdues
   ```

2. Si tout est correct, cliquez **"Installer maintenant"**

---

## Étape 4 : Configuration du système

Pendant que l'installation se prépare, vous configurez votre système.

### Écran 5 : Fuseau horaire

1. Cliquez sur la carte pour sélectionner votre zone
2. Ou tapez votre ville : **"Paris"**
3. Vérifiez que l'heure affichée est correcte
4. Cliquez sur **"Continuer"**

### Écran 6 : Informations utilisateur

Créez votre compte utilisateur principal :

**Votre nom :**
- Prénom et nom (ex: "Marie Dubois")
- Affiché dans l'interface

**Nom de l'ordinateur :**
- Identifie votre PC sur le réseau
- Par défaut : votre prénom + "-mint"
- Exemples : "marie-mint", "pc-salon", "laptop-linux"

**Nom d'utilisateur :**
- Identifiant de connexion
- Tout en minuscules, sans espace ni accent
- Exemples : "marie", "mdubois", "utilisateur"

**Mot de passe :**
- Choisissez un **mot de passe fort mais mémorisable**
- Au moins 8-10 caractères
- Mélangez lettres, chiffres, symboles
- **Notez-le** quelque part de sûr

> 💡 **Conseils pour un bon mot de passe** :
> - ✅ Utilisez une phrase : "J'aime2023Linux!"
> - ✅ Remplacez des lettres : "P@ssw0rd2023"
> - ❌ Évitez : "password", "123456", votre prénom
> - ❌ Évitez : dates de naissance, noms d'animaux seuls

**Confirmer le mot de passe :**
- Retapez exactement le même mot de passe
- Vérifiez qu'il n'y a pas de faute

**Options de connexion :**

```
● Demander mon mot de passe pour ouvrir une session
○ Ouvrir une session automatiquement
☐ Chiffrer mon dossier personnel
```

**Demander le mot de passe :**
- ✅ Plus sécurisé
- ✅ Recommandé pour laptops
- ✅ Protection si quelqu'un accède à votre PC

**Connexion automatique :**
- Démarre directement dans votre session
- Pratique pour un PC personnel à la maison
- Moins sécurisé

**Chiffrer le dossier personnel :**
- Chiffre uniquement votre dossier `/home`
- Plus léger que le chiffrement complet
- Protection supplémentaire
- Légère baisse de performance

> 💡 **Recommandation** : Pour un PC fixe à la maison, la connexion automatique est acceptable. Pour un laptop, demandez toujours le mot de passe.

Cliquez sur **"Continuer"**.

---

## Étape 5 : Installation en cours

L'installation commence réellement maintenant !

### Processus d'installation

**Étapes effectuées :**

1. **Formatage du disque**
   - Création de la table de partitions
   - Formatage en ext4
   - Création du système de fichiers

2. **Copie des fichiers**
   - Système de base Linux Mint
   - Applications pré-installées
   - Environnement de bureau (Cinnamon/MATE/Xfce)

3. **Installation des paquets**
   - Logiciels essentiels
   - Bibliothèques système
   - Pilotes de base

4. **Configuration**
   - Paramètres système
   - Configuration réseau
   - Utilisateur et permissions

5. **Installation de GRUB**
   - Chargeur de démarrage
   - Configuration du boot

### Barre de progression

```
Installation du système...
Copie des fichiers...
[████████████████────────] 65%

Temps restant estimé : 8 minutes
```

**Durée estimée :**
- ⏱️ **15-30 minutes** en moyenne
- Dépend de :
  - Vitesse de votre disque (SSD vs HDD)
  - Vitesse de la clé USB
  - Puissance du processeur
  - Connexion Internet (si installation des mises à jour)

### Diaporama informatif

Pendant l'installation, un **diaporama** vous présente Linux Mint :

- 🎨 L'environnement de bureau
- 📦 Les applications incluses
- 🔧 Les outils système
- 💡 Conseils d'utilisation
- 🌐 Liens vers la documentation

### Que pouvez-vous faire ?

Pendant l'installation, vous **ne pouvez pas** :
- ❌ Utiliser l'ordinateur normalement
- ❌ Annuler l'installation (trop tard !)
- ❌ Éteindre ou redémarrer

Vous **pouvez** :
- ✅ Lire le diaporama
- ✅ Prendre un café ☕
- ✅ Lire la documentation Linux Mint
- ✅ Préparer mentalement votre configuration

> ⚠️ **Important** : NE PAS éteindre l'ordinateur pendant l'installation. Attendez le message de fin.

---

## Étape 6 : Fin de l'installation

### Message de succès

Quand l'installation est terminée :

```
┌──────────────────────────────────────────┐
│  ✅ L'installation est terminée          │
│                                          │
│  Linux Mint a été installé avec succès   │
│  sur votre ordinateur.                   │
│                                          │
│  Vous devez redémarrer pour utiliser     │
│  votre nouveau système.                  │
│                                          │
│  [Continuer à tester] [Redémarrer]       │
└──────────────────────────────────────────┘
```

### Choix final

**Continuer à tester :**
- Reste en mode Live
- Vous pouvez explorer encore
- Redémarrez plus tard manuellement

**Redémarrer maintenant :** (Recommandé)
- Redémarre immédiatement
- Démarre sur votre nouveau système Linux Mint
- Retirez la clé USB quand demandé

### Procédure de redémarrage

1. Cliquez sur **"Redémarrer maintenant"**
2. Le système commence à s'arrêter
3. Un message s'affiche :

```
Veuillez retirer le support d'installation,
puis appuyez sur ENTRÉE pour continuer
```

4. **Retirez la clé USB** de votre ordinateur
5. Appuyez sur la touche **Entrée**
6. L'ordinateur redémarre

> 💡 Si vous ne retirez pas la clé, l'ordinateur redémarrera en mode Live au lieu de démarrer sur le système installé.

---

## Étape 7 : Premier démarrage

### Écran de démarrage

1. **Logo Linux Mint** avec points animés pendant quelques secondes
2. **Écran de connexion** s'affiche

### Écran de connexion

```
┌──────────────────────────────┐
│                              │
│       Bonjour Marie          │
│                              │
│   [Mot de passe]             │
│                              │
│   Se connecter               │
│                              │
└──────────────────────────────┘
```

- Cliquez sur votre **nom d'utilisateur** (si plusieurs utilisateurs)
- Entrez votre **mot de passe**
- Appuyez sur **Entrée** ou cliquez sur **"Se connecter"**

> 💡 Si vous avez activé la connexion automatique, vous arrivez directement au bureau.

### Chargement du bureau

1. Écran noir avec logo pendant quelques secondes
2. Apparition progressive du **bureau Linux Mint**
3. **Écran de bienvenue** s'ouvre automatiquement

---

## Étape 8 : Configuration initiale

### Écran de bienvenue

L'écran de bienvenue vous guide dans les **premières configurations essentielles**.

#### Onglet "Premiers pas"

**Actions recommandées dans l'ordre :**

**1. Instantanés système (Timeshift)** ⭐ PRIORITAIRE
```
┌──────────────────────────────────┐
│  📸 Instantanés système          │
│                                  │
│  Configurez Timeshift pour créer │
│  des sauvegardes système         │
│                                  │
│  [Lancer]                        │
└──────────────────────────────────┘
```

- **FAITES-LE EN PREMIER**
- Crée des points de restauration
- Vous sauve en cas de problème
- Essentiel pour la sécurité

**Comment configurer Timeshift :**
1. Cliquez sur **"Lancer"**
2. Entrez votre mot de passe
3. **Type** : Sélectionnez **"RSYNC"** (recommandé)
4. **Emplacement** : Choisissez votre partition principale (seule option normalement)
5. **Planification** :
   - ☑️ Quotidien : 5 instantanés
   - ☑️ Hebdomadaire : 3 instantanés
   - ☑️ Mensuel : 2 instantanés
   - ☐ Démarrage (optionnel)
6. **Niveaux** : Laissez par défaut
7. Cliquez sur **"Terminer"**
8. Timeshift créera le premier instantané immédiatement

> 💡 **Timeshift** est comme les "Points de restauration" de Windows. En cas de problème, vous pourrez revenir à cet état.

**2. Gestionnaire de mises à jour**
```
┌──────────────────────────────────┐
│  ⬇️ Mises à jour                 │
│                                  │
│  Installez les dernières mises   │
│  à jour de sécurité              │
│                                  │
│  [Lancer]                        │
└──────────────────────────────────┘
```

- Installe les correctifs de sécurité
- Met à jour les logiciels
- **Important pour la sécurité**

**Procédure :**
1. Cliquez sur **"Lancer"**
2. Le gestionnaire vérifie les mises à jour disponibles
3. Liste des mises à jour s'affiche
4. Cliquez sur **"Installer les mises à jour"**
5. Entrez votre mot de passe
6. Attendez la fin (5-30 minutes selon les mises à jour)
7. Redémarrez si demandé

**3. Gestionnaire de pilotes**
```
┌──────────────────────────────────┐
│  🔧 Pilotes                      │
│                                  │
│  Installez les pilotes           │
│  propriétaires recommandés       │
│                                  │
│  [Lancer]                        │
└──────────────────────────────────┘
```

- Détecte votre matériel
- Propose les pilotes optimaux
- **Important pour performances graphiques**

**Procédure :**
1. Cliquez sur **"Lancer"**
2. Attendez la détection (quelques secondes)
3. Si des pilotes sont disponibles :
   - Ils s'affichent avec une recommandation
   - Exemple : "nvidia-driver-535 (propriétaire, testé)"
4. Sélectionnez les pilotes **recommandés** (pré-sélectionnés)
5. Cliquez sur **"Appliquer les changements"**
6. Attendez l'installation
7. **Redémarrez** l'ordinateur

**Pilotes courants détectés :**
- 🎮 **NVIDIA** : Cartes graphiques NVIDIA (gaming, rendu)
- 🔴 **AMD** : Cartes graphiques AMD (gaming, rendu)
- 📡 **WiFi** : Broadcom, Realtek, Intel
- 🖨️ **Imprimantes** : HP, Canon, Epson
- 💻 **Microcode** : Intel, AMD (optimisations processeur)

> 💡 Si aucun pilote n'est proposé, c'est que tout fonctionne déjà avec les pilotes libres. Pas de souci !

**4. Pare-feu**
```
┌──────────────────────────────────┐
│  🔥 Pare-feu                     │
│                                  │
│  Activez le pare-feu système     │
│                                  │
│  [Activer]                       │
└──────────────────────────────────┘
```

- Protection réseau basique
- Bloque les connexions non autorisées
- **Recommandé**

**Procédure :**
1. Cliquez sur **"Activer"**
2. Le pare-feu UFW s'active
3. Configuration par défaut (suffisante)

**5. Comptes en ligne** (Optionnel)
- Synchronise Google, Microsoft, Nextcloud, etc.
- Pour calendrier, contacts, emails
- Pas obligatoire, à faire plus tard si besoin

### Autres onglets de l'écran de bienvenue

**Onglet "Documentation" :**
- Guides d'utilisation
- Tutoriels
- FAQ

**Onglet "Contribuer" :**
- Comment aider le projet
- Dons
- Traductions

**Onglet "Support" :**
- Forums communautaires
- IRC, Discord
- Signaler des bugs

---

## Étape 9 : Vérifications post-installation

### Vérifier le matériel

**Audio :**
- Cliquez sur l'**icône volume** (barre des tâches)
- Ajustez le volume
- Testez en lisant une vidéo YouTube

**Vidéo :**
- Vérifiez la résolution d'écran
- **Clic droit bureau** → **Paramètres d'affichage**
- La résolution native doit être détectée

**Réseau :**
- Cliquez sur l'**icône réseau**
- Connectez-vous à votre WiFi
- Testez la navigation Internet

**Clavier et souris :**
- Testez toutes les touches
- Vérifiez les raccourcis
- Testez la molette de souris

**Imprimante** (si vous en avez) :
- **Menu** → **Paramètres système** → **Imprimantes**
- Ajoutez votre imprimante
- Imprimez une page de test

### Vérifier l'espace disque

1. **Menu** → **Système** → **Disques**
2. Vous voyez votre disque principal
3. Vérifiez :
   - Partition EFI : ~512 Mo
   - Partition racine (/) : Le reste de l'espace
   - Partition swap (si créée) : Taille de votre RAM
4. Tout doit être en ext4 (sauf EFI et swap)

### Vérifier les applications installées

**Applications pré-installées essentielles :**
- 🌐 **Firefox** : Navigateur web
- 📧 **Thunderbird** : Client email
- 📝 **LibreOffice** : Suite bureautique
- 🎵 **Rythmbox** : Lecteur de musique
- 🎬 **VLC** : Lecteur vidéo
- 🖼️ **Visionneuse d'images** : Photos
- 📁 **Nemo** : Gestionnaire de fichiers
- ⚙️ **Paramètres système** : Configuration

> 💡 Consultez le chapitre **5. Applications essentielles** pour plus de détails.

---

## Étape 10 : Premières installations

### Applications populaires à installer

**Selon vos besoins :**

**Communication :**
- Discord : Messagerie gaming
- Telegram : Messagerie sécurisée
- Skype : Appels vidéo
- Zoom : Visioconférences

**Développement :**
- VS Code : Éditeur de code
- Git : Gestion de versions
- Docker : Conteneurs

**Multimédia :**
- GIMP : Retouche photo (comme Photoshop)
- Kdenlive : Montage vidéo
- Audacity : Édition audio
- OBS Studio : Streaming et enregistrement

**Bureautique :**
- OnlyOffice : Alternative à Office
- PDF Studio : Édition PDF avancée

**Utilitaires :**
- Timeshift : Sauvegardes (déjà recommandé)
- BleachBit : Nettoyage système
- GParted : Gestion de partitions

### Comment installer des applications

**Méthode 1 : Gestionnaire de logiciels** (Débutants)
1. **Menu** → **Administration** → **Gestionnaire de logiciels**
2. Recherchez l'application
3. Cliquez sur **"Installer"**
4. Entrez votre mot de passe
5. Attendez la fin

**Méthode 2 : Terminal** (Plus rapide)
```bash
sudo apt update
sudo apt install nom-du-paquet
```

> 💡 Consultez le chapitre **6. Gestion des logiciels** pour plus de détails.

---

## Personnalisation du système

### Thème et apparence

1. **Clic droit bureau** → **Changer le fond d'écran**
2. **Paramètres système** → **Thèmes**
   - Changez les couleurs
   - Testez les thèmes sombres
   - Changez les icônes

### Barre des tâches

1. **Clic droit sur la barre** → **Paramètres du panneau**
2. Ajoutez/supprimez des applets
3. Changez la position (haut, bas)
4. Ajustez la taille

### Bureaux virtuels

- Par défaut : 4 espaces de travail
- **Ctrl + Alt + Flèches** pour naviguer
- Organisez vos applications par bureau

> 💡 Consultez le chapitre **16. Personnalisation avancée** pour aller plus loin.

---

## Migration de vos données

### Récupérer vos sauvegardes

1. **Branchez votre disque dur externe** (avec vos sauvegardes)
2. Linux le détecte automatiquement
3. Ouvrez le **Gestionnaire de fichiers**
4. Naviguez jusqu'à votre disque externe
5. **Copiez vos fichiers** vers votre dossier personnel :
   - Documents → `/home/votre-nom/Documents`
   - Images → `/home/votre-nom/Images`
   - Musique → `/home/votre-nom/Musique`
   - Vidéos → `/home/votre-nom/Vidéos`

### Importer vos favoris de navigateur

**Firefox :**
1. Ouvrez Firefox
2. **Menu** (☰) → **Marque-pages** → **Afficher tous les marque-pages**
3. **Importation et sauvegarde** → **Importer depuis un fichier HTML**
4. Sélectionnez votre fichier de sauvegarde

**Chrome/Chromium :**
1. Installez Chromium : `sudo apt install chromium-browser`
2. Synchronisez avec votre compte Google
3. Ou importez depuis un fichier

### Configurer vos emails

**Thunderbird :**
1. Ouvrez Thunderbird
2. **Configuration automatique** :
   - Entrez votre adresse email et mot de passe
   - Thunderbird détecte les paramètres
3. Ou **configuration manuelle** pour comptes spécifiques

### Synchronisation cloud

**Google Drive :**
- Utilisez Insync (payant) ou rclone (gratuit, ligne de commande)

**OneDrive :**
- Client tiers disponible

**Dropbox :**
- Application officielle disponible

> 💡 Consultez le chapitre **10. Cloud et synchronisation** pour plus de détails.

---

## Problèmes courants et solutions

### Écran noir au démarrage

**Solution 1 : Pilotes graphiques**
1. Au démarrage, appuyez sur **Échap** ou **Shift**
2. Menu GRUB apparaît
3. Sélectionnez **"Options avancées"**
4. Choisissez **"mode recovery"**
5. Sélectionnez **"dpkg"** puis **"root"** (shell root)
6. Installez les pilotes : `ubuntu-drivers autoinstall`
7. Redémarrez : `reboot`

**Solution 2 : Nomodeset**
1. Au menu GRUB, appuyez sur **E**
2. Trouvez la ligne avec `quiet splash`
3. Ajoutez `nomodeset` à la fin
4. **Ctrl + X** pour démarrer

### Pas de son

**Vérifications :**
1. **Clic droit icône son** → **Paramètres du son**
2. Vérifiez que le bon périphérique est sélectionné
3. Testez avec des écouteurs
4. Dans le terminal :
   ```bash
   pulseaudio -k  # Redémarre PulseAudio
   pulseaudio --start
   ```

### WiFi ne fonctionne pas

**Solution :**
1. **Menu** → **Administration** → **Gestionnaire de pilotes**
2. Installez les pilotes WiFi propriétaires
3. Ou connectez en Ethernet temporairement
4. Pilotes courants :
   - Broadcom : `sudo apt install broadcom-sta-dkms`
   - Realtek : Généralement inclus

### Résolution d'écran incorrecte

**Solution :**
1. **Paramètres système** → **Affichage**
2. Changez la résolution manuellement
3. Si votre résolution n'apparaît pas :
   - Installez les pilotes graphiques
   - Ou ajoutez-la manuellement (avancé)

### Impossible de se connecter

**Mot de passe incorrect :**
1. Vérifiez le **Caps Lock** (verrouillage majuscules)
2. Essayez de réinitialiser en mode recovery

**Écran de connexion en boucle :**
1. **Ctrl + Alt + F2** pour accéder au terminal
2. Connectez-vous
3. Vérifiez les permissions : `ls -la ~/.Xauthority`
4. Supprimez le fichier : `rm ~/.Xauthority`
5. **Ctrl + Alt + F7** pour revenir
6. Reconnectez-vous

---

## Questions fréquentes

### Puis-je réinstaller Windows plus tard ?

**Oui**, mais ce sera une installation complète :
1. Créez une clé USB Windows (Media Creation Tool)
2. Démarrez dessus
3. Installez Windows
4. Windows effacera GRUB et Linux
5. Vous perdrez Linux Mint

### Mes fichiers Windows sont-ils récupérables ?

**Non**, ils ont été supprimés définitivement lors de l'installation. C'est pourquoi la sauvegarde préalable était OBLIGATOIRE.

### Comment créer d'autres utilisateurs ?

1. **Paramètres système** → **Utilisateurs et groupes**
2. Cliquez sur **"+"** (Ajouter)
3. Entrez les informations
4. Définissez les permissions (administrateur ou standard)

### Puis-je utiliser des logiciels Windows ?

**Oui, partiellement** via :
- **Wine** : Couche de compatibilité Windows
- **PlayOnLinux** : Interface pour Wine
- **Bottles** : Gestion des applications Windows

> 💡 Consultez le chapitre **15. Applications Windows sous Linux** pour plus de détails.

### Comment sauvegarder mon système maintenant ?

Vous avez configuré **Timeshift** qui crée des instantanés automatiques.

**En plus, pour vos données :**
- Sauvegarde manuelle sur disque externe
- Synchronisation cloud
- rsync automatisé

> 💡 Consultez le chapitre **17. Sauvegarde et restauration** pour plus de détails.

### Linux Mint est-il vraiment gratuit ?

**Oui, 100% gratuit** :
- Aucun coût de licence
- Toutes les mises à jour gratuites
- Aucune publicité
- Open source

Vous pouvez **faire un don** au projet si vous voulez les soutenir, mais c'est totalement optionnel.

### Puis-je installer plusieurs environnements de bureau ?

**Oui**, vous pouvez installer Cinnamon, MATE et Xfce en même temps et choisir au login. Mais pour les débutants, restez avec un seul pour éviter la confusion.

---

## Prochaines étapes

Félicitations ! Linux Mint est installé et configuré. Maintenant :

### Configuration complète

➡️ **[2.7 Premier démarrage et configuration initiale](./07-premier-demarrage-et-configuration-initiale.md)**

Guide complet pour optimiser votre système.

### Découvrir l'interface

➡️ **[4. Découverte de l'environnement de bureau](/04-decouverte-de-lenvironnement-de-bureau/README.md)**

Apprenez à utiliser Cinnamon efficacement.

### Applications essentielles

➡️ **[5. Applications essentielles et Outils Mint](/05-applications-essentielles-et-outils-mint/README.md)**

Découvrez les logiciels pré-installés.

### Terminal et commandes

➡️ **[7. Le terminal et commandes de base](/07-le-terminal-et-commandes-de-base/README.md)**

Devenez efficace en ligne de commande.

---

## Ressources complémentaires

- 📖 [Guide d'installation officiel](https://linuxmint-installation-guide.readthedocs.io/)
- 📚 [Documentation Linux Mint](https://linuxmint.com/documentation.php)
- 💬 [Forum français Linux Mint](https://forums.linuxmint.com/viewforum.php?f=21)
- 🎥 [Chaîne YouTube Linux Mint](https://www.youtube.com/linuxmint)
- 💭 [Reddit r/linuxmint](https://reddit.com/r/linuxmint)
- 📱 [Telegram Linux Mint France](https://t.me/linuxmintfr)
- 🐦 [Twitter @Linux_Mint](https://twitter.com/Linux_Mint)

---

**Félicitations ! Vous avez franchi le cap ! 🎉**

**Bienvenue dans le monde de Linux Mint ! 🐧🚀**

**Votre aventure Linux commence maintenant !**

⏭️ [Partitionnement manuel avancé](/02-preparation-et-installation/06-partitionnement-manuel-avance.md)
