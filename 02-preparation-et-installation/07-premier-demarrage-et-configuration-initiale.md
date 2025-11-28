🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 2.7 Premier démarrage et configuration initiale

## Introduction

Félicitations ! Linux Mint est maintenant installé sur votre ordinateur. Mais avant de commencer à l'utiliser pleinement, il est important de **configurer correctement** votre système dès le départ. Cette étape vous fera gagner du temps et vous évitera des problèmes futurs.

### Pourquoi la configuration initiale est importante ?

La configuration initiale vous permet de :
- ✅ **Sécuriser** votre système avec les dernières mises à jour
- ✅ **Optimiser** les performances matérielles
- ✅ **Protéger** vos données avec des sauvegardes automatiques
- ✅ **Personnaliser** votre environnement selon vos besoins
- ✅ **Installer** les outils essentiels dès le début

> 💡 **Analogie** : C'est comme aménager un nouvel appartement. Vous devez d'abord installer l'essentiel (eau, électricité, internet) avant de vous installer confortablement.

### Temps nécessaire

Prévoyez **1 à 2 heures** pour cette configuration initiale :
- 30 minutes pour les étapes essentielles (mises à jour, pilotes, Timeshift)
- 30 minutes pour la personnalisation
- 30 minutes pour installer vos applications favorites

---

## Étape 1 : Premier démarrage

### Démarrage du système

1. Votre ordinateur redémarre après l'installation
2. Si vous avez un dual-boot, le **menu GRUB** apparaît
   - Sélectionnez **"Linux Mint"** (option par défaut)
   - Ou attendez 10 secondes pour un démarrage automatique
3. Le **logo Linux Mint** s'affiche avec des points animés
4. L'**écran de connexion** apparaît

### Écran de connexion

```
┌──────────────────────────────────┐
│                                  │
│        Bienvenue                 │
│        [Votre nom]               │
│                                  │
│   ●●●●●●●●●●                     │
│   [Entrez votre mot de passe]    │
│                                  │
│   [Se connecter]                 │
│                                  │
└──────────────────────────────────┘
```

**Connexion :**
1. Cliquez sur votre **nom d'utilisateur**
2. Entrez votre **mot de passe**
3. Appuyez sur **Entrée** ou cliquez sur **"Se connecter"**

> 💡 Si vous avez activé la connexion automatique, vous arrivez directement au bureau.

### Chargement du bureau

- Quelques secondes de chargement
- Le **bureau Cinnamon** apparaît progressivement
- L'**écran de bienvenue** s'ouvre automatiquement

---

## Étape 2 : L'écran de bienvenue

L'écran de bienvenue est votre **guide de démarrage**. Il vous accompagne dans les premières configurations essentielles.

### Vue d'ensemble

```
┌────────────────────────────────────────┐
│  Bienvenue dans Linux Mint 22.1        │
├────────────────────────────────────────┤
│  [Premiers pas] [Apps] [Docs] [Support]│
├────────────────────────────────────────┤
│                                        │
│  ⚙️ Premiers pas                       │
│                                        │
│  📸 Instantanés système (Timeshift)    │
│  ⬇️ Gestionnaire de mises à jour       │
│  🔧 Gestionnaire de pilotes            │
│  🔥 Pare-feu                           │
│  👤 Comptes en ligne                   │
│                                        │
└────────────────────────────────────────┘
```

### Onglets disponibles

**Premiers pas** (onglet actif par défaut)
- Actions essentielles à effectuer
- Configuration du système
- Outils de sécurité

**Applications**
- Applications populaires à installer
- Suggestions selon vos besoins

**Documentation**
- Guides d'utilisation
- Liens vers la documentation officielle

**Support**
- Forums communautaires
- Chat IRC/Discord
- Comment obtenir de l'aide

### Désactiver l'écran de bienvenue

Si vous ne voulez plus qu'il apparaisse au démarrage :

- Décochez **"Afficher cet écran au démarrage"** en bas de la fenêtre

> 💡 Vous pourrez toujours le rouvrir via : **Menu** → **Administration** → **Bienvenue à Linux Mint**

---

## Étape 3 : Instantanés système (Timeshift) - PRIORITAIRE

> 🔴 **CRITIQUE** : C'est la **première chose à faire**, avant toute autre configuration. Timeshift crée des sauvegardes système qui vous sauveront en cas de problème.

### Qu'est-ce que Timeshift ?

**Timeshift** est un outil de sauvegarde système qui crée des **instantanés** (snapshots) de votre système. C'est comme les "Points de restauration" de Windows.

**Ce que Timeshift sauvegarde :**
- ✅ Système d'exploitation complet
- ✅ Applications installées
- ✅ Paramètres système
- ✅ Configuration réseau

**Ce que Timeshift ne sauvegarde PAS :**
- ❌ Vos fichiers personnels (documents, photos, etc.)
- ❌ Contenu de /home (par défaut)

> 💡 Timeshift protège le SYSTÈME, pas vos données personnelles. Pour vos données, utilisez une autre solution de sauvegarde (voir chapitre 17).

### Lancer Timeshift

1. Dans l'écran de bienvenue, cliquez sur **"Instantanés système"**
2. Ou : **Menu** → **Administration** → **Timeshift**
3. Entrez votre **mot de passe** administrateur
4. L'assistant de configuration démarre

### Configuration de Timeshift

#### Écran 1 : Type d'instantané

```
┌────────────────────────────────────────┐
│  Sélectionner le type d'instantané     │
│                                        │
│  ● RSYNC                               │
│    Sauvegarde incrémentielle avec      │
│    liens durs (Recommandé)             │
│                                        │
│  ○ BTRFS                               │
│    Nécessite un système de fichiers    │
│    BTRFS (Avancé)                      │
│                                        │
│  [Suivant]                             │
└────────────────────────────────────────┘
```

**Choisissez RSYNC** (recommandé pour débutants) :
- ✅ Fonctionne avec ext4 (standard)
- ✅ Simple et fiable
- ✅ Sauvegardes incrémentielles (économise l'espace)
- ✅ Rapide après le premier instantané

> 💡 **BTRFS** est pour utilisateurs avancés avec partition BTRFS. Si vous ne savez pas ce que c'est, choisissez RSYNC.

Cliquez sur **"Suivant"**.

#### Écran 2 : Emplacement des instantanés

```
┌────────────────────────────────────────┐
│  Sélectionner l'emplacement            │
│                                        │
│  ● /dev/sda2 (ext4, 450 GB)            │
│    /                                   │
│    Disponible : 420 GB                 │
│                                        │
│  [Suivant]                             │
└────────────────────────────────────────┘
```

**Sélectionnez votre partition principale** :
- Généralement, c'est la seule option disponible
- C'est votre partition racine (/) où Linux est installé
- Vérifiez qu'il y a suffisamment d'espace libre

> ⚠️ **Espace nécessaire** : Gardez au moins 10-20 GB libres pour les instantanés. Timeshift vous alertera si l'espace est insuffisant.

Cliquez sur **"Suivant"**.

#### Écran 3 : Niveaux d'instantané

```
┌────────────────────────────────────────┐
│  Sélectionner les niveaux              │
│                                        │
│  ☑ Quotidien   : 5 instantanés         │
│  ☑ Hebdomadaire : 3 instantanés        │
│  ☑ Mensuel     : 2 instantanés         │
│  ☐ Démarrage   : 3 instantanés         │
│  ☐ Horaire     : (désactivé)           │
│                                        │
│  [Suivant]                             │
└────────────────────────────────────────┘
```

**Configuration recommandée** :
- ☑️ **Quotidien : 5** → Garde les 5 derniers jours
- ☑️ **Hebdomadaire : 3** → Garde 3 semaines
- ☑️ **Mensuel : 2** → Garde 2 mois
- ☐ **Démarrage** : Optionnel (crée un instantané à chaque démarrage)
- ☐ **Horaire** : Généralement inutile

> 💡 Cette configuration garde environ 10 instantanés et consomme 15-30 GB selon votre système.

**Personnalisation pour petits disques** :
Si vous avez un disque < 128 GB :
- Quotidien : 3
- Hebdomadaire : 2
- Mensuel : 1

Cliquez sur **"Suivant"**.

#### Écran 4 : Filtres utilisateur

```
┌────────────────────────────────────────┐
│  Dossiers utilisateur à inclure        │
│                                        │
│  ☐ @home (Dossiers personnels)         │
│                                        │
│  Laisser décoché pour économiser       │
│  l'espace et sauvegarder seulement     │
│  le système                            │
│                                        │
│  [Terminer]                            │
└────────────────────────────────────────┘
```

**Laissez décoché** (recommandé) :
- Timeshift sauvegarde seulement le système
- Vos fichiers personnels ne sont pas inclus
- Économise beaucoup d'espace disque
- Sauvegardes plus rapides

> 💡 Pour sauvegarder vos fichiers personnels, utilisez un autre outil (Déjà Dup, rsync, etc.). Voir chapitre 17.

Cliquez sur **"Terminer"**.

### Premier instantané

Timeshift vous propose de créer le **premier instantané** immédiatement :

```
┌────────────────────────────────────────┐
│  Créer le premier instantané ?         │
│                                        │
│  Il est recommandé de créer un         │
│  instantané maintenant                 │
│                                        │
│  [Non] [Oui]                           │
└────────────────────────────────────────┘
```

**Cliquez sur "Oui"** :
1. Timeshift crée le premier instantané
2. Barre de progression s'affiche
3. Durée : 5-15 minutes (premier instantané plus long)
4. Les suivants seront plus rapides (incrémentiels)

> 💡 Ce premier instantané capture votre système fraîchement installé. C'est votre point de restauration de référence.

### Interface principale de Timeshift

Une fois configuré, l'interface principale affiche :

```
┌────────────────────────────────────────┐
│  Timeshift                             │
├────────────────────────────────────────┤
│  [Créer] [Restaurer] [Supprimer]       │
├────────────────────────────────────────┤
│  Instantanés :                         │
│                                        │
│  ● 2025-01-15 10:30 (D) - Démarrage    │
│    450 MB - 2 min                      │
│                                        │
└────────────────────────────────────────┘
```

**Légende :**
- **(D)** = Quotidien
- **(W)** = Hebdomadaire
- **(M)** = Mensuel
- **(B)** = Démarrage

### Tester la restauration (optionnel)

Vous pouvez tester que la restauration fonctionne :

1. **Menu** → **Administration** → **Timeshift**
2. Sélectionnez un instantané
3. Cliquez sur **"Restaurer"**
4. Suivez l'assistant (mode Live recommandé pour les tests)

> ⚠️ Ne testez ceci que si vous savez ce que vous faites. En général, vous n'aurez besoin de restaurer qu'en cas de problème.

---

## Étape 4 : Gestionnaire de mises à jour

> 🔴 **IMPORTANT** : Installez les mises à jour immédiatement après Timeshift. C'est crucial pour la sécurité.

### Pourquoi mettre à jour ?

Les mises à jour apportent :
- 🔒 **Correctifs de sécurité** (vulnérabilités corrigées)
- 🐛 **Corrections de bugs**
- ✨ **Nouvelles fonctionnalités**
- ⚡ **Améliorations de performance**
- 🔧 **Support matériel amélioré**

### Lancer le gestionnaire de mises à jour

1. Dans l'écran de bienvenue, cliquez sur **"Gestionnaire de mises à jour"**
2. Ou : **Menu** → **Administration** → **Gestionnaire de mises à jour**
3. Ou : Cliquez sur l'**icône bouclier** dans la barre des tâches

### Première utilisation

**Actualisation des sources :**
```
┌────────────────────────────────────────┐
│  Mise à jour de la liste des paquets   │
│                                        │
│  Téléchargement des informations       │
│  sur les mises à jour disponibles...   │
│                                        │
│  [███████████────────] 60%             │
└────────────────────────────────────────┘
```

- Patientez pendant le téléchargement de la liste
- Durée : 10-30 secondes
- Nécessite une connexion Internet

### Miroirs locaux

Au premier lancement, le gestionnaire peut proposer de choisir un **miroir local** :

```
┌────────────────────────────────────────┐
│  Voulez-vous basculer vers un miroir   │
│  plus rapide ?                         │
│                                        │
│  Un miroir dans votre pays sera plus   │
│  rapide pour télécharger les mises à   │
│  jour                                  │
│                                        │
│  [Non] [Oui]                           │
└────────────────────────────────────────┘
```

**Cliquez sur "Oui"** :
1. Une fenêtre avec la liste des miroirs s'ouvre
2. Cliquez sur **"Vitesse"** pour tester les miroirs
3. Le gestionnaire teste la vitesse de chaque serveur
4. Sélectionnez le **miroir le plus rapide** (généralement pré-sélectionné)
5. Cliquez sur **"Appliquer"**

> 💡 Les miroirs en France : ftp.lip6.fr, mirrors.ircam.fr, etc. Choisissez celui avec le ping le plus bas.

### Liste des mises à jour

```
┌────────────────────────────────────────┐
│  Gestionnaire de mises à jour          │
├────────────────────────────────────────┤
│  📦 125 mises à jour disponibles       │
│  ⬇️ 385 MB à télécharger               │
│                                        │
│  ☑ linux-image-5.15.0-91 (Kernel)      │
│  ☑ firefox (121.0)                     │
│  ☑ libreoffice-core (7.6.4)            │
│  ☑ ... (122 autres)                    │
│                                        │
│  [Installer les mises à jour]          │
└────────────────────────────────────────┘
```

### Niveaux de mise à jour

Linux Mint classe les mises à jour par niveau de risque :

**Niveau 1** 🟢 (Certifié)
- Testé et approuvé par l'équipe Linux Mint
- Aucun risque
- Toujours installé

**Niveau 2** 🟢 (Recommandé)
- Testé, fiable
- Risque minimal
- Installé par défaut

**Niveau 3** 🟡 (Sûr)
- Testé, parfois des régressions mineures
- Installé par défaut
- Risque faible

**Niveau 4** 🟠 (Non sûr)
- Paquets importants, non testés
- Peut causer des problèmes
- NON installé par défaut

**Niveau 5** 🔴 (Dangereux)
- Paquets système critiques
- Peut casser le système
- NON installé par défaut

> 💡 **Configuration par défaut** : Niveaux 1-2-3 activés. C'est parfait pour débutants.

### Installer les mises à jour

1. **Vérifiez** que toutes les mises à jour sont cochées (par défaut)
2. Cliquez sur **"Installer les mises à jour"**
3. Entrez votre **mot de passe**
4. Le téléchargement commence

**Progression :**
```
Téléchargement des paquets...
[████████████████────] 385 MB / 385 MB

Installation des mises à jour...
[████████████────────] 75 / 125

Configuration des paquets...
```

**Durée :**
- Téléchargement : 5-20 minutes (selon connexion)
- Installation : 5-15 minutes
- **Total : 10-35 minutes**

> 💡 Pendant le téléchargement et l'installation, vous pouvez continuer à utiliser votre ordinateur normalement.

### Mises à jour du kernel

Si le **kernel Linux** est mis à jour, un redémarrage sera nécessaire :

```
┌────────────────────────────────────────┐
│  Les mises à jour ont été installées   │
│                                        │
│  ⚠️ Un redémarrage est recommandé      │
│  pour appliquer les mises à jour du    │
│  kernel                                │
│                                        │
│  [Plus tard] [Redémarrer maintenant]   │
└────────────────────────────────────────┘
```

**Redémarrez maintenant** (recommandé) :
- Le nouveau kernel sera actif
- Corrections de sécurité appliquées
- Performances optimisées

**Redémarrer plus tard** :
- Possible, mais pas idéal
- Redémarrez dès que vous le pouvez

### Mises à jour automatiques

**Configuration recommandée :**
1. **Menu** → **Préférences** → **Gestionnaire de mises à jour**
2. **Édition** → **Préférences**
3. **Automatisation** :
   - ☑️ **Actualiser automatiquement la liste** : Quotidien
   - ☑️ **Notifier les mises à jour** : Oui
   - ☐ **Installer automatiquement** : NON (pour garder le contrôle)

> 💡 Il est recommandé de NE PAS installer automatiquement, mais d'être notifié pour choisir quand installer.

---

## Étape 5 : Gestionnaire de pilotes

Les **pilotes propriétaires** améliorent les performances de votre matériel, surtout pour les cartes graphiques et WiFi.

### Qu'est-ce qu'un pilote propriétaire ?

**Pilotes libres (open source)** :
- ✅ Inclus par défaut
- ✅ Stables et sûrs
- ❌ Parfois performances limitées

**Pilotes propriétaires** :
- ✅ Performances optimales
- ✅ Toutes les fonctionnalités
- ❌ Code source fermé
- ❌ Nécessitent installation manuelle

> 💡 **Analogie** : Les pilotes libres sont comme un téléphone sans toutes les fonctionnalités. Les pilotes propriétaires débloquent tout le potentiel.

### Lancer le gestionnaire de pilotes

1. Dans l'écran de bienvenue, cliquez sur **"Gestionnaire de pilotes"**
2. Ou : **Menu** → **Administration** → **Gestionnaire de pilotes**
3. Entrez votre **mot de passe**

### Détection du matériel

```
┌────────────────────────────────────────┐
│  Gestionnaire de pilotes               │
├────────────────────────────────────────┤
│  Recherche de pilotes disponibles...   │
│                                        │
│  [████████████████████] 100%           │
│                                        │
│  Détection du matériel en cours...     │
└────────────────────────────────────────┘
```

- Durée : 10-30 secondes
- Analyse votre matériel
- Recherche les pilotes recommandés

### Pilotes détectés

#### Carte graphique NVIDIA

```
┌────────────────────────────────────────┐
│  NVIDIA Corporation GF119              │
│                                        │
│  ○ Utiliser le pilote source ouvert    │
│     nouveau (installé par défaut)      │
│                                        │
│  ● nvidia-driver-535 (propriétaire,    │
│     testé)                             │
│     [Recommandé]                       │
│                                        │
│  ○ nvidia-driver-545 (propriétaire)    │
│                                        │
│  [Appliquer les changements]           │
└────────────────────────────────────────┘
```

**Sélectionnez le pilote recommandé** :
- Généralement marqué **(propriétaire, testé)**
- Meilleur compromis performance/stabilité
- Activé par défaut

#### Carte graphique AMD

Pour AMD, le pilote libre (AMDGPU) est excellent. Les pilotes propriétaires ne sont nécessaires que pour :
- Gaming haute performance
- Rendu 3D professionnel
- Mining (mais ne faites pas ça 😉)

#### Adaptateur WiFi

```
┌────────────────────────────────────────┐
│  Broadcom Corporation BCM4313          │
│                                        │
│  ○ Ne pas utiliser l'appareil          │
│                                        │
│  ● Utiliser broadcom-sta-dkms          │
│     (pilote source ouvert)             │
│     [Recommandé]                       │
│                                        │
│  [Appliquer les changements]           │
└────────────────────────────────────────┘
```

Si votre WiFi ne fonctionnait pas, ce pilote le corrigera.

#### Microcode processeur

```
┌────────────────────────────────────────┐
│  Processeur - Microcode                │
│                                        │
│  ● intel-microcode (propriétaire)      │
│     Mises à jour du microcode Intel    │
│     [Recommandé]                       │
│                                        │
│  Améliore stabilité et sécurité du CPU │
│                                        │
│  [Appliquer les changements]           │
└────────────────────────────────────────┘
```

**Installez toujours le microcode** :
- Corrections de bugs CPU
- Patches de sécurité (Spectre, Meltdown, etc.)
- Aucun inconvénient

### Installer les pilotes

1. **Sélectionnez** les pilotes recommandés (généralement pré-sélectionnés)
2. Cliquez sur **"Appliquer les changements"**
3. Entrez votre **mot de passe**
4. L'installation commence

**Progression :**
```
Téléchargement des pilotes...
[████████████████────] 85%

Installation des pilotes...

Configuration...
```

**Durée :** 5-15 minutes

### Redémarrage nécessaire

```
┌────────────────────────────────────────┐
│  Installation terminée                 │
│                                        │
│  ⚠️ Vous devez redémarrer l'ordinateur │
│  pour activer les nouveaux pilotes     │
│                                        │
│  [Plus tard] [Redémarrer maintenant]   │
└────────────────────────────────────────┘
```

**Redémarrez immédiatement** (recommandé) :
- Les pilotes seront actifs
- Performances graphiques optimales
- Tout fonctionnera correctement

### Vérification après redémarrage

**Pour carte NVIDIA :**
```bash
nvidia-smi
```

Affiche les informations de votre GPU et confirme que le pilote fonctionne.

**Pour tout matériel :**
```bash
sudo lshw -C video
sudo lshw -C network
```

---

## Étape 6 : Pare-feu (UFW)

Le **pare-feu** protège votre ordinateur contre les connexions non autorisées.

### Activer le pare-feu

1. Dans l'écran de bienvenue, cliquez sur **"Pare-feu"**
2. Ou : **Menu** → **Préférences** → **Pare-feu**
3. Entrez votre **mot de passe**

### Interface GUFW

```
┌────────────────────────────────────────┐
│  Configuration du pare-feu             │
│                                        │
│  État : ○ Désactivé  ● Activé          │
│                                        │
│  Profil : [Domicile ▼]                 │
│                                        │
│  Règles entrantes : Refuser            │
│  Règles sortantes : Autoriser          │
│                                        │
└────────────────────────────────────────┘
```

**Configuration recommandée pour débutants :**
1. **État** : **Activé** (ON)
2. **Profil** : **Domicile** (ou Bureau si au travail)
3. **Règles entrantes** : **Refuser** (bloque les connexions entrantes)
4. **Règles sortantes** : **Autoriser** (permet les connexions sortantes)

> 💡 Cette configuration bloque toutes les tentatives de connexion externe tout en vous permettant de naviguer, télécharger, etc.

### Profils disponibles

**Domicile** :
- Sécurité standard
- Bon pour utilisation personnelle

**Bureau** :
- Sécurité renforcée
- Pour environnement professionnel

**Public** :
- Sécurité maximale
- Pour WiFi publics, cafés, aéroports

> 💡 Changez le profil selon votre emplacement.

### Ajouter des règles (avancé)

Si vous avez besoin d'autoriser des services spécifiques :

**Exemple : Autoriser SSH**
1. Cliquez sur **"Règles"**
2. Cliquez sur **"+"** (Ajouter)
3. **Type** : Simple
4. **Catégorie** : Service
5. **Service** : SSH
6. **Action** : Autoriser

> 💡 Pour débutants, la configuration par défaut suffit largement.

---

## Étape 7 : Configuration des paramètres système

### Accéder aux paramètres système

**Menu** → **Préférences** → **Paramètres système**

### Paramètres essentiels à configurer

#### 1. Affichage

```
Paramètres système → Affichage
```

**Résolution d'écran :**
- Vérifiez que la résolution native est sélectionnée
- Exemple : 1920×1080 pour écran Full HD

**Fréquence de rafraîchissement :**
- 60 Hz standard
- 120 Hz / 144 Hz si écran gaming

**Mise à l'échelle :**
- 100% pour écrans normaux
- 125-150% pour écrans haute résolution (4K)
- 200% pour écrans très haute résolution

**Disposition (si plusieurs écrans) :**
- Glissez-déposez les écrans pour les positionner
- Définissez l'écran principal

#### 2. Son

```
Paramètres système → Son
```

**Volume :**
- Ajustez le volume principal
- Testez avec un son/vidéo

**Périphérique de sortie :**
- Sélectionnez vos haut-parleurs ou casque
- Si plusieurs choix, testez chacun

**Périphérique d'entrée :**
- Sélectionnez votre microphone
- Testez en parlant (la barre doit bouger)

**Effets sonores :**
- Activez/désactivez les sons système
- Personnalisez selon vos préférences

#### 3. Réseau

```
Paramètres système → Réseau
```

**WiFi :**
1. Activez le WiFi
2. Sélectionnez votre réseau
3. Entrez le mot de passe
4. **"Se connecter automatiquement"** : Coché

**Ethernet :**
- Branchez le câble
- Connexion automatique généralement

**Proxy :**
- Généralement "Aucun"
- Configurez si votre réseau l'exige

#### 4. Bluetooth

```
Paramètres système → Bluetooth
```

**Activer Bluetooth :**
1. Activez le commutateur
2. Cliquez sur **"Paramètres"** pour ajouter des appareils
3. Mettez votre appareil en mode appairage
4. Sélectionnez-le dans la liste
5. Confirmez le code d'appairage

**Appareils courants :**
- Souris Bluetooth
- Clavier Bluetooth
- Casque audio
- Téléphone (pour transfert de fichiers)

#### 5. Énergie

```
Paramètres système → Énergie
```

**Mise en veille de l'écran :**
- **Sur secteur** : 10-15 minutes
- **Sur batterie** : 5 minutes

**Mise en veille automatique :**
- **Sur secteur** : 30 minutes ou Jamais
- **Sur batterie** : 15 minutes

**Niveau de batterie faible :**
- Action : Suspendre ou Mettre en veille prolongée

**Luminosité :**
- Ajustez selon votre confort
- Réduisez sur batterie pour économiser

> 💡 **PC portables** : Activez "Réduire la luminosité sur batterie"

#### 6. Date et heure

```
Paramètres système → Date et heure
```

**Configuration automatique** (recommandé) :
- ☑️ **Définir automatiquement** l'heure
- ☑️ Utiliser les **serveurs NTP**
- Fuseau horaire : **Europe/Paris** (ou votre ville)

**Format :**
- Format 24h : 14:30
- Format 12h : 2:30 PM

#### 7. Langue et région

```
Paramètres système → Langue et région
```

**Langue du système :**
- Déjà configuré en **Français**
- Ajoutez d'autres langues si besoin

**Formats régionaux :**
- Date : JJ/MM/AAAA (France)
- Heure : 24h
- Nombres : 1 234,56 (espace pour milliers, virgule pour décimales)
- Monnaie : € (Euro)

#### 8. Clavier

```
Paramètres système → Clavier
```

**Agencement :**
- Français (azerty)
- Ajoutez d'autres agencements si besoin (QWERTY, etc.)

**Raccourci de changement de langue :**
- Par défaut : **Super + Espace**
- Ou configurez votre propre raccourci

**Répétition des touches :**
- Délai : Court (plus rapide)
- Vitesse : Rapide

> 💡 Testez en maintenant une touche appuyée pour ajuster.

#### 9. Souris et pavé tactile

```
Paramètres système → Souris et pavé tactile
```

**Souris :**
- **Vitesse du pointeur** : Ajustez selon préférence
- **Bouton principal** : Gauche (standard) ou Droite (gauchers)
- **Défilement naturel** : Décoché (standard)

**Pavé tactile** (laptops) :
- **Désactiver en tapant** : Coché (évite les clics accidentels)
- **Défilement** : Deux doigts (standard)
- **Gestes** :
  - Trois doigts haut : Vue d'ensemble
  - Trois doigts bas : Bureau
  - Quatre doigts gauche/droite : Changer d'espace de travail

#### 10. Imprimantes

```
Paramètres système → Imprimantes
```

**Ajouter une imprimante :**
1. Allumez votre imprimante
2. Connectez-la (USB ou réseau)
3. Cliquez sur **"Ajouter"**
4. Linux Mint détecte automatiquement
5. Sélectionnez votre imprimante
6. Cliquez sur **"Ajouter"**

**Test d'impression :**
- Clic droit sur l'imprimante
- **"Imprimer une page de test"**

> 💡 La plupart des imprimantes HP, Canon, Epson fonctionnent automatiquement.

---

## Étape 8 : Personnalisation de base

### Thèmes et apparence

```
Clic droit sur le bureau → Changer le fond d'écran
```

**Fond d'écran :**
1. Parcourez les fonds d'écran inclus
2. Ou ajoutez vos propres images
3. Sélectionnez votre favori

```
Paramètres système → Thèmes
```

**Thème des fenêtres :**
- **Mint-Y** : Moderne, plat
- **Mint-X** : Classique, dégradés
- Variantes : Vert, Bleu, Rouge, Gris, etc.

**Thème d'icônes :**
- **Mint-Y** : Icônes plates modernes
- **Mint-X** : Icônes classiques
- Couleurs disponibles

**Thème sombre :**
- Cochez **"Utiliser le thème sombre"**
- Meilleur pour les yeux le soir
- Économie d'énergie (écrans OLED)

### Barre des tâches

```
Clic droit sur la barre → Paramètres du panneau
```

**Position :**
- Bas (par défaut)
- Haut, Gauche, Droite

**Hauteur :**
- Ajustez la taille de la barre

**Masquage automatique :**
- ☐ Masquer automatiquement
- ☑ Afficher la barre au survol

**Applets :**
- Ajoutez/supprimez des éléments
- Réorganisez en glissant-déposant

### Effets de bureau

```
Paramètres système → Effets
```

**Activer les effets :**
- ☑️ Animations des fenêtres
- ☑️ Transparence
- ☑️ Ombres

**Niveau d'effet :**
- **Léger** : PC anciens
- **Moyen** : Standard (recommandé)
- **Fort** : PC puissants, animations fluides

### Coins actifs

```
Paramètres système → Coins actifs
```

**Configurer les actions des coins :**
- Coin supérieur gauche : Vue d'ensemble
- Coin supérieur droit : Afficher le bureau
- Etc.

> 💡 Déplacez la souris dans un coin pour activer l'action.

---

## Étape 9 : Installation d'applications essentielles

### Via le gestionnaire de logiciels

**Menu** → **Administration** → **Gestionnaire de logiciels**

#### Applications recommandées pour débutants

**Internet et communication :**
- 🌐 **Google Chrome** ou **Chromium** (navigateur alternatif)
- 💬 **Discord** (chat vocal/texte)
- 📱 **Telegram Desktop** (messagerie)
- 📞 **Zoom** (visioconférence)

**Multimédia :**
- 🎵 **Spotify** (musique en streaming)
- 🎬 **VLC** (déjà installé, lecteur vidéo)
- 🎨 **GIMP** (retouche photo, comme Photoshop)
- 🎞️ **Kdenlive** (montage vidéo)

**Bureautique :**
- 📝 **LibreOffice** (déjà installé)
- 📄 **OnlyOffice** (alternative Microsoft Office)
- 📋 **CherryTree** (prise de notes)

**Utilitaires :**
- 💾 **BleachBit** (nettoyage système)
- 📦 **GDebi** (installation de paquets .deb)
- 🔍 **Baobab** (analyseur d'espace disque)
- 📸 **Flameshot** (captures d'écran avancées)

**Développement** (si vous codez) :
- 💻 **Visual Studio Code**
- 🐙 **Git** (gestion de versions)
- 🐍 **Python** (déjà installé)

### Installation rapide via terminal

**Pour installer plusieurs applications d'un coup :**

```bash
sudo apt update
sudo apt install gimp vlc telegram-desktop flameshot
```

> 💡 Consultez le chapitre **5. Applications essentielles** et **6. Gestion des logiciels** pour plus de détails.

---

## Étape 10 : Optimisations finales

### Activer TRIM pour SSD

Si vous avez un **SSD**, activez TRIM pour prolonger sa durée de vie :

```bash
sudo systemctl enable fstrim.timer
sudo systemctl start fstrim.timer
```

**Vérification :**
```bash
sudo fstrim -v /
```

### Réduire le swappiness

Le **swappiness** contrôle l'utilisation du swap. Réduisez-le pour privilégier la RAM :

```bash
# Vérifier la valeur actuelle
cat /proc/sys/vm/swappiness
# Devrait afficher 60 par défaut

# Réduire à 10 (recommandé pour desktop)
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf

# Appliquer immédiatement
sudo sysctl vm.swappiness=10
```

### Désactiver les services inutiles (avancé)

**Voir les services actifs :**
```bash
systemctl list-unit-files --type=service --state=enabled
```

**Désactiver un service inutilisé :**
```bash
sudo systemctl disable nom-du-service
```

> ⚠️ **Attention** : Ne désactivez que ce que vous connaissez ! Les débutants peuvent ignorer cette étape.

### Précharger les applications (optionnel)

**Preload** précharge les applications fréquemment utilisées en mémoire :

```bash
sudo apt install preload
```

Une fois installé, il fonctionne automatiquement en arrière-plan.

---

## Étape 11 : Configuration des comptes en ligne (optionnel)

### Ajouter des comptes

```
Paramètres système → Comptes en ligne
```

**Services supportés :**
- 📧 **Google** (Gmail, Drive, Calendrier, Contacts)
- 🔷 **Microsoft** (Outlook, OneDrive)
- ☁️ **Nextcloud** (stockage cloud auto-hébergé)
- 📧 **IMAP/SMTP** (emails génériques)

**Avantages :**
- Synchronisation automatique des emails
- Calendrier intégré
- Contacts synchronisés
- Accès aux fichiers cloud

**Configuration Google :**
1. Cliquez sur **"Google"**
2. Entrez votre adresse Gmail
3. Entrez votre mot de passe
4. Autorisez l'accès
5. Sélectionnez les services à synchroniser :
   - ☑️ Courrier
   - ☑️ Calendrier
   - ☑️ Contacts
   - ☑️ Documents

---

## Étape 12 : Vérifications finales

### Checklist de configuration

- [ ] ✅ **Timeshift configuré** et premier instantané créé
- [ ] ✅ **Toutes les mises à jour installées**
- [ ] ✅ **Pilotes propriétaires installés** (si nécessaire)
- [ ] ✅ **Pare-feu activé**
- [ ] ✅ **Résolution d'écran correcte**
- [ ] ✅ **Son fonctionne**
- [ ] ✅ **WiFi/Ethernet connecté**
- [ ] ✅ **Clavier et souris configurés**
- [ ] ✅ **Thème et fond d'écran personnalisés**
- [ ] ✅ **Applications essentielles installées**
- [ ] ✅ **Imprimante configurée** (si applicable)

### Tests de fonctionnement

**Navigateur Web :**
- Ouvrez Firefox
- Naviguez sur quelques sites
- Vérifiez que tout s'affiche correctement

**Multimédia :**
- Lisez une vidéo (YouTube ou fichier local)
- Écoutez de la musique
- Vérifiez le son

**Bureautique :**
- Ouvrez LibreOffice Writer
- Créez un document test
- Enregistrez-le

**Gestionnaire de fichiers :**
- Ouvrez Nemo
- Naviguez dans vos dossiers
- Créez un dossier test
- Supprimez-le

---

## Dépannage post-installation

### Le son ne fonctionne pas

**Solutions :**
1. Vérifiez le volume (icône haut-parleur)
2. **Paramètres système** → **Son** → Vérifiez le périphérique de sortie
3. Redémarrez PulseAudio :
   ```bash
   pulseaudio -k
   pulseaudio --start
   ```

### La résolution d'écran est incorrecte

**Solutions :**
1. Installez les pilotes graphiques propriétaires
2. **Paramètres système** → **Affichage** → Changez la résolution
3. Redémarrez l'ordinateur

### Le WiFi ne se connecte pas

**Solutions :**
1. Vérifiez le mot de passe
2. Désactivez/réactivez le WiFi
3. Installez les pilotes WiFi via **Gestionnaire de pilotes**
4. Redémarrez le service réseau :
   ```bash
   sudo systemctl restart NetworkManager
   ```

### Le système est lent

**Causes possibles :**
- Pilotes graphiques manquants (installez-les)
- Trop d'animations (réduisez les effets)
- Pas assez de RAM (ajoutez du swap)
- SSD sans TRIM (activez TRIM)

**Diagnostic :**
```bash
# Voir l'utilisation des ressources
htop

# Voir l'espace disque
df -h

# Voir la RAM
free -h
```

### Les mises à jour échouent

**Erreur courante :** "Impossible de récupérer..."

**Solutions :**
1. Changez de miroir (Sources de logiciels)
2. Videz le cache :
   ```bash
   sudo apt clean
   sudo apt update
   ```
3. Réparez les dépendances :
   ```bash
   sudo apt --fix-broken install
   ```

---

## Prochaines étapes

Votre système est maintenant **parfaitement configuré** ! Vous pouvez commencer à l'utiliser pleinement.

### Continuer votre apprentissage

➡️ **[3. Migration depuis Windows](/03-migration-depuis-windows/README.md)**

Si vous venez de Windows, découvrez comment retrouver vos repères.

➡️ **[4. Découverte de l'environnement de bureau](/04-decouverte-de-lenvironnement-de-bureau/README.md)**

Maîtrisez l'interface Cinnamon.

➡️ **[5. Applications essentielles et Outils Mint](/05-applications-essentielles-et-outils-mint/README.md)**

Explorez les applications pré-installées.

➡️ **[6. Gestion des logiciels](/06-gestion-des-logiciels/README.md)**

Apprenez à installer et gérer vos logiciels.

### Ressources utiles

- 📖 [Documentation Linux Mint](https://linuxmint.com/documentation.php)
- 💬 [Forum Linux Mint français](https://forums.linuxmint.com/viewforum.php?f=21)
- 🎥 [Chaîne YouTube Linux Mint](https://www.youtube.com/linuxmint)
- 📱 [Telegram Linux Mint France](https://t.me/linuxmintfr)
- 🌐 [Reddit r/linuxmint](https://reddit.com/r/linuxmint)

---

## Félicitations ! 🎉

**Vous avez terminé la configuration initiale de Linux Mint !**

Votre système est maintenant :
- ✅ **Sécurisé** (mises à jour, pare-feu)
- ✅ **Sauvegardé** (Timeshift)
- ✅ **Optimisé** (pilotes, paramètres)
- ✅ **Personnalisé** (thème, applications)
- ✅ **Prêt à l'emploi** !

**Bienvenue dans Linux Mint ! Profitez de votre nouveau système ! 🚀🐧**

⏭️ [Installation dans une machine virtuelle](/02-preparation-et-installation/08-installation-dans-une-machine-virtuelle.md)
