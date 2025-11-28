🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 2. Préparation et installation

## Introduction

Bienvenue dans le chapitre le plus important de cette formation : **l'installation de Linux Mint** ! 🚀

Ce chapitre vous guide pas-à-pas dans toutes les étapes nécessaires pour installer Linux Mint sur votre ordinateur, que vous souhaitiez le tester dans une machine virtuelle, l'installer à côté de Windows, ou remplacer complètement votre système d'exploitation actuel.

### Objectifs de ce chapitre

À la fin de ce chapitre, vous serez capable de :

- ✅ **Télécharger** Linux Mint en toute sécurité
- ✅ **Vérifier** l'intégrité de votre téléchargement
- ✅ **Créer** une clé USB bootable
- ✅ **Tester** Linux Mint sans l'installer (mode Live)
- ✅ **Installer** Linux Mint selon vos besoins (dual-boot, installation complète, ou VM)
- ✅ **Configurer** votre système pour une utilisation optimale

> 💡 **Rassurez-vous** : Chaque étape est expliquée en détail avec des captures d'écran textuelles, des avertissements clairs sur les points critiques, et des solutions aux problèmes courants.

---

## Pour qui est ce chapitre ?

### Débutants complets

Vous n'avez **jamais installé** de système d'exploitation ? Pas de panique ! Ce chapitre est conçu pour vous guider depuis le tout début, en expliquant chaque concept et chaque étape.

### Utilisateurs Windows

Vous utilisez **Windows** et voulez découvrir Linux ? Ce chapitre vous montre comment installer Linux Mint **à côté de Windows** (dual-boot) ou comment le tester dans une **machine virtuelle** sans risque.

### Utilisateurs macOS

Vous utilisez un **Mac** et voulez installer Linux Mint ? Les instructions pour créer une clé USB bootable et tester en mode Live fonctionnent également depuis macOS.

### Utilisateurs Linux

Vous connaissez déjà Linux et voulez **installer Linux Mint** ? Le chapitre sur le partitionnement manuel avancé vous donnera un contrôle total sur votre installation.

---

## Vue d'ensemble du chapitre

Ce chapitre est organisé en **8 sections progressives** :

```
📥 Téléchargement → 💾 Clé USB → 🧪 Test → 💻 Installation → ⚙️ Configuration
```

### Sections disponibles

**Section 2.1 : Téléchargement et vérification de l'ISO**
- Où télécharger Linux Mint en toute sécurité
- Comment choisir la bonne édition
- Vérifier l'intégrité du fichier (checksums)
- ⏱️ Durée : 15-30 minutes (selon connexion)

**Section 2.2 : Création d'une clé USB bootable**
- Trois méthodes détaillées (Rufus, Etcher, Ventoy)
- Comparaison des outils
- Résolution des problèmes courants
- ⏱️ Durée : 10-20 minutes

**Section 2.3 : Test en mode Live**
- Démarrer Linux Mint sans l'installer
- Explorer l'interface en toute sécurité
- Tester la compatibilité matérielle
- Checklist de vérification
- ⏱️ Durée : 30-60 minutes d'exploration

**Section 2.4 : Installation en dual-boot avec Windows**
- Garder Windows et Linux sur le même PC
- Partitionnement semi-automatique
- Configuration de GRUB
- ⏱️ Durée : 45-90 minutes

**Section 2.5 : Installation complète (remplacement de l'OS)**
- Remplacer complètement Windows par Linux
- Pour qui est cette option
- Avertissements et précautions
- ⏱️ Durée : 30-60 minutes

**Section 2.6 : Partitionnement manuel avancé**
- Contrôle total sur les partitions
- Schémas recommandés
- Création de /home séparée
- ⏱️ Durée : 45-90 minutes

**Section 2.7 : Premier démarrage et configuration initiale**
- Configuration de Timeshift (sauvegardes)
- Installation des mises à jour
- Installation des pilotes
- Paramètres essentiels
- ⏱️ Durée : 60-120 minutes

**Section 2.8 : Installation dans une machine virtuelle**
- Tester Linux sans modifier votre PC
- Guide VirtualBox complet
- Configuration optimale
- ⏱️ Durée : 60-90 minutes

---

## Parcours recommandés selon votre situation

### 🎓 Parcours "Débutant prudent"

**Vous voulez découvrir Linux sans aucun risque**

```
2.1 → 2.2 → 2.3 → 2.8 (Machine virtuelle)
```

**Pourquoi ce parcours ?**
- ✅ Zéro risque pour votre ordinateur
- ✅ Possibilité de tout supprimer en un clic
- ✅ Idéal pour l'apprentissage
- ❌ Performances réduites

**Temps total estimé :** 2-3 heures

---

### 🔄 Parcours "Le meilleur des deux mondes"

**Vous voulez garder Windows ET installer Linux**

```
2.1 → 2.2 → 2.3 → 2.4 (Dual-boot) → 2.7
```

**Pourquoi ce parcours ?**
- ✅ Accès à Windows ET Linux
- ✅ Choix au démarrage
- ✅ Performances natives pour Linux
- ⚠️ Nécessite de partitionner le disque

**Temps total estimé :** 3-4 heures

---

### 💪 Parcours "Engagement total"

**Vous voulez passer 100% à Linux**

```
2.1 → 2.2 → 2.3 → 2.5 (Installation complète) → 2.7
```

**Pourquoi ce parcours ?**
- ✅ 100% des ressources pour Linux
- ✅ Installation la plus simple
- ✅ Performances optimales
- ❌ Windows sera supprimé

**⚠️ CRITIQUE : Sauvegardez TOUTES vos données avant !**

**Temps total estimé :** 2-3 heures

---

### 🔧 Parcours "Expert technique"

**Vous voulez un contrôle total sur l'installation**

```
2.1 → 2.2 → 2.3 → 2.6 (Partitionnement manuel) → 2.7
```

**Pourquoi ce parcours ?**
- ✅ Contrôle total des partitions
- ✅ Configuration sur mesure
- ✅ Optimisation selon vos besoins
- ⚠️ Nécessite des connaissances techniques

**Temps total estimé :** 3-5 heures

---

## Prérequis généraux

Avant de commencer ce chapitre, assurez-vous d'avoir :

### Matériel nécessaire

- 💻 **Un ordinateur** compatible :
  - Processeur 64-bit (après 2007 généralement)
  - Minimum 2 GB de RAM (4 GB recommandé)
  - Minimum 20 GB d'espace disque libre (50 GB recommandé)

- 💾 **Une clé USB** :
  - Capacité : 4 GB minimum (8 GB recommandé)
  - Elle sera formatée (toutes les données seront effacées)

- 🌐 **Connexion Internet** :
  - Pour télécharger Linux Mint (~2.5 GB)
  - Pour les mises à jour pendant l'installation (optionnel mais recommandé)

### Connaissances recommandées

- 📁 Savoir naviguer dans les fichiers et dossiers
- 💾 Comprendre la notion de téléchargement
- 🖱️ Utiliser le BIOS/UEFI (ou être prêt à apprendre)
- 📝 Lire attentivement les instructions

> 💡 **Pas d'inquiétude** : Toutes les notions techniques sont expliquées au fur et à mesure.

---

## Conseils importants avant de commencer

### 🔴 Sauvegardez vos données

> **CRITIQUE** : Avant toute installation (surtout dual-boot ou installation complète), **sauvegardez TOUTES vos données importantes** sur un disque externe ou dans le cloud.

**Pourquoi ?**
- Une erreur de manipulation peut entraîner une perte de données
- Les partitions seront modifiées (dual-boot) ou effacées (installation complète)
- Mieux vaut prévenir que guérir !

**Que sauvegarder ?**
- Documents personnels
- Photos et vidéos
- Musique et téléchargements
- Emails (si stockés localement)
- Favoris du navigateur
- Mots de passe et clés de licence

### ⏰ Prévoyez du temps

Ne commencez pas une installation si vous êtes pressé. Prévoyez :
- **Minimum** : 2-3 heures (installation de base)
- **Confortable** : 3-4 heures (avec configuration)
- **Idéal** : Une demi-journée ou soirée tranquille

### 🔋 Ordinateur portable : Branchez l'alimentation

Pour les laptops, **branchez TOUJOURS l'alimentation** pendant :
- Le téléchargement et la création de la clé USB
- L'installation complète
- La configuration initiale

> ⚠️ Une coupure de batterie pendant l'installation peut corrompre le système.

### 📖 Lisez avant d'agir

Pour chaque section :
1. **Lisez** entièrement la section une première fois
2. **Comprenez** ce que vous allez faire
3. **Suivez** les instructions étape par étape
4. **N'hésitez pas** à relire si nécessaire

> 💡 Les sections critiques sont clairement marquées avec des avertissements ⚠️ et 🔴.

### 🆘 Besoin d'aide ?

Si vous rencontrez un problème :
1. Consultez la section "Dépannage" de chaque chapitre
2. Recherchez votre erreur sur les forums Linux Mint
3. Demandez de l'aide sur la communauté (voir chapitre 24)

**Liens utiles :**
- 💬 [Forum Linux Mint français](https://forums.linuxmint.com/viewforum.php?f=21)
- 📖 [Documentation officielle](https://linuxmint.com/documentation.php)
- 📱 [Telegram Linux Mint France](https://t.me/linuxmintfr)

---

## Choix de l'édition Linux Mint

Avant de télécharger, vous devez choisir votre édition. Voici un guide rapide :

### Les trois éditions principales

**Cinnamon** 🌟 (Recommandé pour la plupart)
- Interface moderne et élégante
- Similaire à Windows 7/10
- Riche en fonctionnalités
- **Pour** : PC récents (moins de 5 ans)

**MATE** 🍃 (Classique et léger)
- Interface traditionnelle
- Sobre et efficace
- Consommation réduite
- **Pour** : PC moyens (5-10 ans)

**Xfce** ⚡ (Ultra-léger)
- Interface minimaliste
- Très rapide
- Consommation minimale
- **Pour** : PC anciens ou peu puissants

> 💡 **En cas de doute** : Choisissez **Cinnamon**. C'est l'édition phare de Linux Mint, la plus populaire et la mieux supportée.

### LMDE (Linux Mint Debian Edition)

Une édition spéciale basée sur Debian au lieu d'Ubuntu :
- Plus "pure" et indépendante
- Mises à jour continues
- **Pour** : Utilisateurs avancés ou ceux qui préfèrent Debian

> 💡 **Pour débutants** : Restez sur les éditions classiques (Cinnamon, MATE, Xfce).

---

## Structure de ce chapitre

### Navigation

Chaque section est **indépendante** mais suit une **progression logique**. Vous pouvez :

- ✅ Suivre l'ordre recommandé (linéaire)
- ✅ Sauter des sections selon votre parcours
- ✅ Revenir en arrière si nécessaire

### Conventions utilisées

**Emojis de niveau de difficulté :**
- ⭐ Facile (débutants)
- ⭐⭐ Moyen (quelques notions requises)
- ⭐⭐⭐ Avancé (utilisateurs expérimentés)
- ⭐⭐⭐⭐ Expert (connaissances techniques)

**Emojis d'avertissement :**
- 💡 **Conseil ou astuce**
- ⚠️ **Attention, point important**
- 🔴 **Critique, risque de perte de données**
- ✅ **Validation ou étape réussie**
- ❌ **Erreur ou à éviter**

**Blocs de code :**
```bash
# Les commandes à taper dans le terminal
sudo apt update
```

**Citations importantes :**
> Les informations cruciales sont mises en évidence comme ceci

---

## Temps estimé par section

Voici une estimation réaliste du temps nécessaire pour chaque section :

| Section | Temps estimé | Difficulté |
|---------|--------------|------------|
| 2.1 Téléchargement et vérification | 15-30 min | ⭐ Facile |
| 2.2 Création clé USB bootable | 10-20 min | ⭐ Facile |
| 2.3 Test en mode Live | 30-60 min | ⭐ Facile |
| 2.4 Dual-boot avec Windows | 45-90 min | ⭐⭐ Moyen |
| 2.5 Installation complète | 30-60 min | ⭐⭐ Moyen |
| 2.6 Partitionnement manuel | 45-90 min | ⭐⭐⭐ Avancé |
| 2.7 Configuration initiale | 60-120 min | ⭐ Facile |
| 2.8 Machine virtuelle | 60-90 min | ⭐⭐ Moyen |

> 💡 Ces temps incluent la lecture des instructions et l'exécution des étapes, mais pas les temps de téléchargement qui dépendent de votre connexion Internet.

---

## Liste de contrôle pré-installation

Avant de commencer, cochez cette liste :

### Préparation matérielle

- [ ] J'ai un ordinateur compatible (processeur 64-bit)
- [ ] J'ai au moins 2 GB de RAM (4 GB recommandé)
- [ ] J'ai au moins 20 GB d'espace libre (50 GB recommandé)
- [ ] J'ai une clé USB de 4 GB minimum
- [ ] Mon ordinateur portable est branché sur secteur

### Préparation logicielle

- [ ] J'ai une connexion Internet stable
- [ ] J'ai téléchargé le bon ISO (ou je m'apprête à le faire)
- [ ] J'ai un logiciel pour créer la clé USB (Rufus, Etcher, etc.)

### Sauvegarde et sécurité

- [ ] J'ai sauvegardé TOUTES mes données importantes
- [ ] J'ai noté mes mots de passe importants
- [ ] J'ai exporté mes favoris de navigateur
- [ ] J'ai une sauvegarde de mes emails (si stockés localement)
- [ ] J'ai noté ma clé de licence Windows (si dual-boot)

### Mental et organisation

- [ ] J'ai prévu suffisamment de temps (2-4 heures)
- [ ] J'ai lu les avertissements de ce chapitre
- [ ] Je suis prêt à suivre les instructions attentivement
- [ ] Je sais où trouver de l'aide si besoin

> ✅ **Tous cochés ?** Vous êtes prêt à commencer ! Rendez-vous à la section 2.1.

---

## Garanties et avertissements

### Ce que Linux Mint garantit

- ✅ **Gratuit** : Linux Mint est 100% gratuit, pas de licence à payer
- ✅ **Open source** : Le code est ouvert et auditable
- ✅ **Sans publicité** : Aucune publicité, aucun tracking
- ✅ **Respect de la vie privée** : Vos données restent vos données
- ✅ **Communauté active** : Support communautaire disponible
- ✅ **Mises à jour régulières** : Corrections de sécurité fréquentes

### Ce que nous ne pouvons pas garantir

- ❌ **Compatibilité matérielle à 100%** : Certains matériels propriétaires peuvent nécessiter des pilotes spécifiques
- ❌ **Remplacement parfait de Windows** : Certains logiciels Windows n'ont pas d'équivalent Linux
- ❌ **Zéro problème** : Comme tout système, des bugs peuvent survenir
- ❌ **Support commercial** : Linux Mint est supporté par la communauté, pas une entreprise

### Responsabilités

> ⚠️ **Important** : Bien que ce guide soit conçu pour être le plus sûr possible, **vous êtes responsable** de vos actions. Sauvegardez toujours vos données avant toute installation.

L'équipe Linux Mint et les auteurs de ce guide ne peuvent être tenus responsables de :
- Perte de données due à une mauvaise manipulation
- Problèmes matériels liés à une installation incorrecte
- Incompatibilités logicielles ou matérielles

> 💡 **Suivez les instructions à la lettre** et tout se passera bien !

---

## Après l'installation

Une fois Linux Mint installé et configuré, ce guide continue avec :

### Chapitre 3 : Migration depuis Windows
- Retrouver vos repères
- Équivalents de vos logiciels Windows
- Transfert de vos données
- Accès aux partitions Windows

### Chapitre 4 : Découverte de l'environnement de bureau
- Maîtriser l'interface Cinnamon
- Personnalisation de base
- Raccourcis clavier essentiels
- Espaces de travail virtuels

### Chapitre 5 : Applications essentielles
- Tour d'horizon des applications pré-installées
- Outils Linux Mint spécifiques
- Alternatives aux logiciels courants

### Et bien plus encore !

Ce guide vous accompagne dans **toutes les facettes** de Linux Mint, de l'installation basique à l'utilisation avancée.

---

## Prêt à commencer ?

Vous avez maintenant une **vision complète** de ce qui vous attend dans ce chapitre. Il est temps de passer à l'action !

### Selon votre choix :

**🧪 Je veux d'abord tester sans risque**
- ➡️ Commencez par la section **2.8 Machine virtuelle**

**💻 Je veux installer Linux Mint pour de vrai**
- ➡️ Commencez par la section **2.1 Téléchargement et vérification**

**📚 Je veux d'abord en savoir plus**
- ➡️ Relisez le **Chapitre 1 Introduction à Linux Mint**

---

## Commençons par le commencement

Pour 99% des utilisateurs, le parcours commence ici :

➡️ **[2.1 Téléchargement et vérification de l'ISO](./01-telechargement-et-verification-de-liso.md)**

Dans cette section, vous apprendrez à :
- Télécharger Linux Mint depuis les sources officielles
- Choisir la bonne édition pour votre matériel
- Vérifier l'intégrité du fichier téléchargé avec les checksums
- Éviter les pièges et sources non fiables

---

**Bonne installation ! 🚀**

**Vous êtes sur le point de découvrir Linux Mint, un système d'exploitation moderne, élégant et respectueux de vos choix. Bienvenue dans la communauté Linux Mint ! 🐧💚**

⏭️ [Téléchargement et vérification de l'ISO](/02-preparation-et-installation/01-telechargement-et-verification-de-liso.md)
