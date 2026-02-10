🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 2.8 Installation dans une machine virtuelle

## Introduction

Une **machine virtuelle** (VM) est un excellent moyen de tester Linux Mint **sans aucun risque** pour votre ordinateur. C'est comme avoir un ordinateur complet à l'intérieur de votre ordinateur actuel !

### Qu'est-ce qu'une machine virtuelle ?

Une machine virtuelle est un **ordinateur virtuel** qui fonctionne comme une application sur votre système d'exploitation actuel (Windows, macOS, ou Linux). Elle simule un ordinateur complet avec son propre processeur, mémoire, disque dur, et carte graphique.

> 💡 **Analogie** : Imaginez une poupée russe. Votre ordinateur physique est la grande poupée, et la machine virtuelle est une petite poupée indépendante à l'intérieur. Les deux peuvent fonctionner en même temps sans s'influencer.

### Schéma conceptuel

```
┌─────────────────────────────────────────┐
│   Votre ordinateur physique (Hôte)      │
│   Windows 11                            │
│                                         │
│  ┌───────────────────────────────────┐  │
│  │   Machine Virtuelle (Invité)      │  │
│  │   Linux Mint 22.1                 │  │
│  │                                   │  │
│  │   [Applications Linux]            │  │
│  │                                   │  │
│  └───────────────────────────────────┘  │
│                                         │
│  [Applications Windows]                 │
└─────────────────────────────────────────┘
```

---

## Avantages et inconvénients

### Avantages d'une machine virtuelle

- ✅ **Zéro risque** : Aucune modification sur votre système principal
- ✅ **Réversible** : Supprimez la VM en un clic si elle ne vous plaît pas
- ✅ **Test sans engagement** : Explorez Linux tranquillement
- ✅ **Snapshots** : Sauvegardez l'état de la VM et revenez en arrière
- ✅ **Plusieurs systèmes** : Testez plusieurs distributions en parallèle
- ✅ **Apprentissage** : Expérimentez sans crainte de "casser" quelque chose
- ✅ **Isolation** : La VM est isolée de votre système principal

### Inconvénients d'une machine virtuelle

- ❌ **Performances réduites** : 30-50% moins rapide qu'une installation native
- ❌ **Consomme beaucoup de ressources** : Nécessite un PC puissant
- ❌ **Graphismes limités** : Jeux et applications 3D mal supportés
- ❌ **Ne remplace pas une vraie installation** : C'est un environnement de test
- ❌ **Configuration plus complexe** : Nécessite quelques étapes supplémentaires

### Quand utiliser une machine virtuelle ?

**Utilisez une VM pour :**
- 🎓 **Apprendre Linux** avant de l'installer en vrai
- 🧪 **Tester Linux Mint** pour voir s'il vous convient
- 📚 **Suivre des tutoriels** sans risque
- 🔬 **Expérimenter** avec des commandes et configurations
- 💼 **Usage occasionnel** de Linux parallèlement à Windows
- 🎯 **Développement** et tests d'applications

**N'utilisez PAS une VM pour :**
- 🎮 **Gaming** (performances insuffisantes)
- 🎬 **Montage vidéo** professionnel (trop lent)
- 🎨 **Graphisme 3D** avancé
- 💻 **Usage quotidien** intensif (préférez une installation native)

---

## Configuration système requise

### Pour l'ordinateur hôte

**Minimum (usage léger) :**
- Processeur : Intel Core i3 / AMD Ryzen 3 (4 cœurs)
- RAM : 8 GB
- Disque : 30 GB libres
- Virtualisation : Support VT-x/AMD-V activé dans le BIOS

**Recommandé (usage confortable) :**
- Processeur : Intel Core i5 / AMD Ryzen 5 (6+ cœurs)
- RAM : 16 GB ou plus
- Disque : SSD avec 50+ GB libres
- Virtualisation : Support VT-x/AMD-V + VT-d/AMD-Vi

**Idéal (performances optimales) :**
- Processeur : Intel Core i7 / AMD Ryzen 7 (8+ cœurs)
- RAM : 32 GB
- Disque : SSD NVMe avec 100+ GB libres
- Carte graphique : Dédiée (pour accélération 3D)

### Allocation de ressources à la VM

**Règle générale :** Ne donnez pas plus de **50-60%** des ressources de votre PC à la VM.

**Exemple avec un PC 16 GB RAM, 8 cœurs :**
- VM : 6-8 GB RAM
- VM : 3-4 cœurs CPU
- VM : 30-50 GB disque virtuel

> ⚠️ **Important** : Votre système hôte a besoin de ressources pour fonctionner ! Ne donnez pas tout à la VM.

---

## Choix du logiciel de virtualisation

### Vue d'ensemble

| Logiciel | Systèmes hôtes | Prix | Difficulté | Recommandé pour |
|----------|---------------|------|------------|-----------------|
| **VirtualBox** | Win, Mac, Linux | Gratuit | ⭐⭐ Facile | Débutants, usage général |
| **VMware Workstation Player** | Windows, Linux | Gratuit (usage perso) | ⭐⭐ Facile | Performances supérieures |
| **VMware Workstation Pro** | Windows, Linux | Payant (~250€) | ⭐⭐⭐ Moyen | Professionnels |
| **VMware Fusion** | macOS | Payant | ⭐⭐ Facile | Utilisateurs Mac |
| **Hyper-V** | Windows Pro+ | Gratuit (inclus) | ⭐⭐⭐ Moyen | Utilisateurs Windows Pro |
| **QEMU/KVM** | Linux | Gratuit | ⭐⭐⭐⭐ Avancé | Utilisateurs Linux experts |

### VirtualBox (Recommandé pour ce tutoriel)

**Oracle VM VirtualBox** est le choix idéal pour débuter :

- ✅ **Gratuit et open source**
- ✅ **Fonctionne sur tous les systèmes** (Windows, Mac, Linux)
- ✅ **Interface simple et claire**
- ✅ **Bien documenté**
- ✅ **Grande communauté**
- ✅ **Parfait pour l'apprentissage**

> 💡 Ce tutoriel utilisera **VirtualBox** car c'est le plus accessible pour les débutants.

---

## Étape 1 : Vérifier la virtualisation matérielle

Avant d'installer VirtualBox, vérifiez que la **virtualisation matérielle** est activée.

### Sous Windows

**Méthode 1 : Gestionnaire des tâches**
1. Appuyez sur **Ctrl + Shift + Échap** (Gestionnaire des tâches)
2. Onglet **"Performance"**
3. Cliquez sur **"Processeur"**
4. Regardez en bas : **"Virtualisation : Activée"**

**Si elle est désactivée :**
```
Virtualisation : Désactivée
```

**Méthode 2 : Systeminfo**
```cmd
systeminfo
```
Cherchez la ligne : `Configuration requise Hyper-V: Virtualisation activée dans le microprogramme: Oui`

### Activer la virtualisation dans le BIOS/UEFI

Si la virtualisation est désactivée :

1. **Redémarrez** votre ordinateur
2. **Appuyez sur F2, Del, ou F10** au démarrage (selon votre PC)
3. Cherchez les paramètres de virtualisation :
   - **Intel** : "Intel VT-x", "Intel Virtualization Technology", "Vanderpool"
   - **AMD** : "AMD-V", "SVM Mode", "AMD Virtualization"
4. **Activez** l'option
5. **Sauvegardez** et quittez (F10 généralement)

> 💡 L'emplacement exact dépend de votre carte mère. Consultez le manuel ou recherchez "activer VT-x [modèle de votre PC]" sur Internet.

---

## Étape 2 : Télécharger VirtualBox

### Téléchargement

1. Rendez-vous sur : **[https://www.virtualbox.org](https://www.virtualbox.org)**
2. Cliquez sur **"Downloads"**
3. Sous **"VirtualBox 7.x.x platform packages"** :
   - **Windows** : Cliquez sur "Windows hosts"
   - **macOS** : Cliquez sur "macOS / Intel hosts" ou "macOS / Apple Silicon hosts"
   - **Linux** : Sélectionnez votre distribution

4. Téléchargez également **"VirtualBox Extension Pack"** (sur la même page)
   - C'est un fichier unique compatible avec tous les systèmes
   - Ajoute support USB 3.0, webcam, RDP, etc.

### Tailles de fichiers

- VirtualBox : ~100-150 MB
- Extension Pack : ~10-20 MB

---

## Étape 3 : Installer VirtualBox

### Sous Windows

1. **Double-cliquez** sur le fichier téléchargé (ex: `VirtualBox-7.0.12-Win.exe`)
2. Acceptez les droits administrateur
3. Assistant d'installation s'ouvre

**Écran 1 : Bienvenue**
- Cliquez sur **"Next"**

**Écran 2 : Fonctionnalités**
- Laissez tout coché (installation complète)
- Cliquez sur **"Next"**

**Écran 3 : Avertissement réseau**
```
┌─────────────────────────────────────┐
│  ⚠️  Avertissement                  │
│                                     │
│  L'installation va temporairement   │
│  réinitialiser votre connexion      │
│  réseau                             │
│                                     │
│  [Yes] [No]                         │
└─────────────────────────────────────┘
```
- Cliquez sur **"Yes"** (votre connexion sera coupée 1-2 secondes)

**Écran 4 : Prêt à installer**
- Cliquez sur **"Install"**

**Écran 5 : Pilotes Oracle**
- Cochez **"Toujours faire confiance..."**
- Cliquez sur **"Installer"**

**Écran 6 : Fin**
- Cliquez sur **"Finish"**

### Installer l'Extension Pack

1. **Double-cliquez** sur `Oracle_VM_VirtualBox_Extension_Pack-7.0.12.vbox-extpack`
2. VirtualBox s'ouvre automatiquement
3. Cliquez sur **"Install"**
4. **Descendez** jusqu'en bas de la licence
5. Cliquez sur **"J'accepte"** (bouton activé seulement en bas)
6. Entrez votre mot de passe administrateur si demandé
7. **"Extension Pack installé avec succès"**

---

## Étape 4 : Télécharger l'ISO de Linux Mint

Si vous ne l'avez pas déjà fait :

1. **[https://www.linuxmint.com/download.php](https://www.linuxmint.com/download.php)**
2. Téléchargez **Linux Mint Cinnamon 64-bit**
3. Taille : ~2.5-3 GB
4. **Vérifiez le checksum** (optionnel mais recommandé, voir chapitre 2.1)

---

## Étape 5 : Créer une nouvelle machine virtuelle

### Lancer VirtualBox

Ouvrez **Oracle VM VirtualBox** depuis votre menu Démarrer / Applications.

### Interface principale

```
┌────────────────────────────────────────┐
│  Oracle VM VirtualBox Gestionnaire     │
├────────────────────────────────────────┤
│  [Nouvelle] [Paramètres] [Démarrer]    │
├────────────────────────────────────────┤
│                                        │
│  (Aucune machine virtuelle)            │
│                                        │
└────────────────────────────────────────┘
```

### Créer une nouvelle VM

Cliquez sur **"Nouvelle"** (ou **Machine** → **Nouvelle**)

### Assistant de création

#### Page 1 : Nom et système d'exploitation

```
┌────────────────────────────────────────┐
│  Créer une machine virtuelle           │
├────────────────────────────────────────┤
│  Nom : [Linux Mint 22.1]               │
│                                        │
│  Dossier : [C:\Users\...\VirtualBox]   │
│                                        │
│  Image ISO : [Aucune sélectionnée]     │
│              [📁 Parcourir]            │
│                                        │
│  Type : [Linux ▼]                      │
│  Version : [Ubuntu (64-bit) ▼]         │
│                                        │
│  [Suivant]                             │
└────────────────────────────────────────┘
```

**Configuration :**

**Nom :**
- Entrez : **"Linux Mint 22.1"** (ou autre nom explicite)
- Ce nom identifie la VM dans VirtualBox

**Dossier :**
- Laissez par défaut (généralement `C:\Users\VotreNom\VirtualBox VMs`)
- Ou changez vers un disque avec plus d'espace

**Image ISO :**
1. Cliquez sur **"Parcourir"** (icône dossier)
2. Naviguez jusqu'à votre ISO Linux Mint téléchargée
3. Sélectionnez-la
4. VirtualBox détecte automatiquement Linux

**Type et Version :**
- **Type** : Linux (détecté automatiquement)
- **Version** : **Ubuntu (64-bit)** (Linux Mint est basé sur Ubuntu)

> 💡 Si vous ne voyez que des versions 32-bit, la virtualisation n'est pas activée dans votre BIOS.

Cliquez sur **"Suivant"**.

#### Page 2 : Matériel (RAM et CPU)

```
┌────────────────────────────────────────┐
│  Matériel                              │
├────────────────────────────────────────┤
│  Mémoire vive : [4096] MB              │
│  [████████────────────] 4 GB / 16 GB   │
│                                        │
│  Processeurs : [2] CPU                 │
│  [████────────────────] 2 / 8          │
│                                        │
│  ☑ Activer EFI                         │
│                                        │
│  [Précédent] [Suivant]                 │
└────────────────────────────────────────┘
```

**Mémoire vive (RAM) :**

**Recommandations selon votre RAM totale :**

| RAM totale | RAM pour la VM | Reste pour l'hôte |
|------------|---------------|-------------------|
| 8 GB | 2-3 GB | 5-6 GB |
| 12 GB | 4 GB | 8 GB |
| 16 GB | 6-8 GB | 8-10 GB |
| 32 GB | 8-12 GB | 20-24 GB |

> ⚠️ **Zone verte** : Restez dans la zone verte sur le curseur. La zone rouge ralentira votre PC hôte.

**Processeurs (CPU) :**

**Recommandations selon vos cœurs totaux :**

| CPU total | CPU pour la VM | Reste pour l'hôte |
|-----------|---------------|-------------------|
| 4 cœurs | 2 | 2 |
| 6 cœurs | 2-3 | 3-4 |
| 8 cœurs | 3-4 | 4-5 |
| 12+ cœurs | 4-6 | 6+ |

> 💡 **Règle** : Ne donnez pas plus de 50-60% de vos cœurs à la VM.

**Activer EFI :**
- ☑️ **Cochez** cette option (recommandé pour Linux Mint moderne)
- Simule un PC UEFI au lieu de BIOS legacy

Cliquez sur **"Suivant"**.

#### Page 3 : Disque dur virtuel

```
┌────────────────────────────────────────┐
│  Disque dur virtuel                    │
├────────────────────────────────────────┤
│  ● Créer un disque dur virtuel         │
│    maintenant                          │
│                                        │
│  Taille : [30.00] GB                   │
│  [████████──────────────] 30 GB        │
│                                        │
│  ☑ Préallouer la taille complète       │
│                                        │
│  [Précédent] [Suivant]                 │
└────────────────────────────────────────┘
```

**Créer un disque dur virtuel :**
- Sélectionnez **"Créer un disque dur virtuel maintenant"**

**Taille du disque :**

**Recommandations :**
- **Minimum** : 20 GB (très serré)
- **Recommandé** : 30-50 GB (confortable)
- **Idéal** : 50-100 GB (si espace disponible)

> 💡 Ce disque virtuel se comporte comme un vrai disque. Linux Mint y sera installé.

**Préallouer la taille complète :**
- ☐ **Décoché** : Disque à taille dynamique (grandit au besoin, plus lent)
- ☑️ **Coché** : Disque fixe (taille réservée, plus rapide)

**Recommandation :**
- **Décochez** si espace disque limité (économise l'espace)
- **Cochez** si espace suffisant (meilleures performances)

Cliquez sur **"Suivant"**.

#### Page 4 : Résumé

```
┌────────────────────────────────────────┐
│  Résumé                                │
├────────────────────────────────────────┤
│  Nom : Linux Mint 22.1                 │
│  Type : Linux (Ubuntu 64-bit)          │
│  RAM : 6144 MB                         │
│  CPU : 3 cœurs                         │
│  Disque : 40 GB (VDI, dynamique)       │
│  EFI : Activé                          │
│                                        │
│  [Précédent] [Terminer]                │
└────────────────────────────────────────┘
```

**Vérifiez** que tout est correct, puis cliquez sur **"Terminer"**.

---

## Étape 6 : Configuration avancée (optionnel mais recommandé)

Avant de démarrer la VM, optimisons quelques paramètres.

### Accéder aux paramètres

1. Sélectionnez votre VM **"Linux Mint 22.1"**
2. Cliquez sur **"Configuration"** (ou **Paramètres**)

### Paramètres recommandés

#### Général → Avancé

```
Dossier des instantanés : (par défaut)  
Presse-papiers partagé : [Bidirectionnel ▼]  
Glisser-déposer : [Bidirectionnel ▼]  
```

- **Presse-papiers partagé** : Bidirectionnel (copier-coller entre hôte et VM)
- **Glisser-déposer** : Bidirectionnel (glisser fichiers entre hôte et VM)

#### Système → Carte mère

```
Mémoire vive : 6144 MB  
Ordre d'amorçage :  
  ☑ Disquette (décochez)
  ☑ Disque optique
  ☑ Disque dur
  ☐ Réseau

☑ Activer l'horloge matérielle en temps UTC
☑ Activer EFI
```

**Ordre d'amorçage :**
- ☐ **Disquette** : Décochez (obsolète)
- ☑️ **Disque optique** : Coché (pour démarrer sur l'ISO)
- ☑️ **Disque dur** : Coché

**Horloge :**
- ☑️ **Activer l'horloge matérielle en temps UTC** (important pour Linux)

#### Système → Processeur

```
Processeur(s) : [3] CPU

☑ Activer PAE/NX
☑ Activer VT-x/AMD-V imbriqué (si disponible)
```

- **PAE/NX** : Coché (sécurité)
- **VT-x imbriqué** : Coché si disponible (virtualisation dans la VM)

#### Affichage → Écran

```
Mémoire vidéo : [128] MB
[████████████████████] 128 MB

☑ Activer l'accélération 3D
Contrôleur graphique : [VMSVGA ▼]
```

**Mémoire vidéo :**
- **Minimum** : 16 MB
- **Recommandé** : 128 MB (maximum)
- Mettez le **maximum** pour de meilleures performances

**Accélération 3D :**
- ☑️ **Activez** cette option
- Améliore les performances graphiques

**Contrôleur graphique :**
- **VMSVGA** (recommandé pour Linux moderne)
- Alternatives : VBoxVGA, VBoxSVGA

#### Stockage

```
Contrôleur : SATA
  📀 linuxmint-22.1-cinnamon-64bit.iso
  💾 Linux Mint 22.1.vdi
```

**Vérifications :**
- L'ISO est attachée au lecteur CD/DVD
- Le disque virtuel est présent

> 💡 Après installation, vous pourrez retirer l'ISO.

#### Audio

```
☑ Activer l'audio

Pilote hôte : [DirectSound ▼] (Windows)
              [CoreAudio ▼] (macOS)
              [PulseAudio ▼] (Linux)

Contrôleur audio : [ICH AC97 ▼]
```

- **Activer l'audio** : Coché
- **Pilote hôte** : Laissez par défaut (détecté automatiquement)
- **Contrôleur** : ICH AC97 ou Intel HD Audio

#### Réseau → Carte 1

```
☑ Activer la carte réseau

Mode d'accès réseau : [NAT ▼]
```

**Mode NAT** (recommandé) :
- La VM accède à Internet via l'hôte
- La VM est isolée du réseau externe
- Parfait pour un usage normal

**Alternatives :**
- **Accès par pont** : VM comme un vrai PC sur le réseau
- **Réseau interne** : VMs communiquent entre elles
- **Réseau privé hôte** : Communication hôte ↔ VM

#### USB

```
☑ Activer le contrôleur USB

● USB 3.0 (xHCI)
```

- Sélectionnez **USB 3.0** si Extension Pack installé
- Sinon, **USB 2.0** fonctionne aussi

#### Dossiers partagés (optionnel)

Pour partager des fichiers entre hôte et VM :

1. Cliquez sur **"+"** (Ajouter)
2. **Chemin du dossier** : Parcourez un dossier sur votre PC hôte
3. **Nom du dossier** : Nom dans la VM (ex: "Partage")
4. ☑️ **Montage automatique**
5. ☑️ **Rendre permanent**
6. Cliquez **"OK"**

> 💡 Utile pour échanger facilement des fichiers entre Windows et Linux.

### Appliquer les paramètres

Cliquez sur **"OK"** pour sauvegarder tous les changements.

---

## Étape 7 : Premier démarrage et installation

### Démarrer la machine virtuelle

1. Sélectionnez **"Linux Mint 22.1"**
2. Cliquez sur **"Démarrer"** (flèche verte)

### Fenêtre de la VM

Une nouvelle fenêtre s'ouvre : c'est l'écran de votre machine virtuelle.

```
┌────────────────────────────────────────┐
│  Linux Mint 22.1 [En cours...]         │
├────────────────────────────────────────┤
│                                        │
│         [Logo Linux Mint]              │
│                                        │
│     Démarrage de Linux Mint...         │
│                                        │
└────────────────────────────────────────┘
```

### Menu de démarrage Linux Mint

Le menu GRUB apparaît :

- **Start Linux Mint**
- Start Linux Mint (compatibility mode)
- OEM install
- Check integrity
- Test memory
- Boot from local drive

Sélectionnez **"Start Linux Mint"** (option par défaut).

### Chargement du mode Live

- Logo Linux Mint avec points animés
- Durée : 1-2 minutes
- Bureau Linux Mint s'affiche

> 💡 **Première fois** : La capture du clavier/souris peut sembler étrange. Lisez la section suivante.

### Capture du clavier et de la souris

**Message VirtualBox :**
```
┌────────────────────────────────────────┐
│  Intégration du clavier et de la souris│
│                                        │
│  Pour basculer entre la VM et l'hôte,  │
│  appuyez sur : Ctrl Droite             │
│                                        │
│  [OK]                                  │
└────────────────────────────────────────┘
```

**Comprendre la capture :**
- Quand vous cliquez dans la fenêtre VM, la souris est "capturée"
- Pour libérer la souris : appuyez sur **Ctrl Droite** (touche Ctrl à droite de la barre d'espace)
- Avec Guest Additions installés, ce sera transparent

### Installation de Linux Mint

Maintenant que le mode Live fonctionne, **installez Linux Mint normalement** :

1. Double-cliquez sur **"Install Linux Mint"**
2. Suivez l'assistant d'installation (voir chapitres 2.4, 2.5, ou 2.6)

**Différences avec installation physique :**
- ✅ **Aucune** ! Le processus est identique
- ✅ Pas besoin de dual-boot (seul système sur le disque virtuel)
- ✅ Sélectionnez **"Effacer le disque et installer"** sans souci
- ✅ Partitionnement automatique recommandé

**Durée d'installation :**
- 15-30 minutes (comme sur PC physique)
- Peut être plus lent selon les performances

### Redémarrage

Quand l'installation est terminée :

1. Cliquez sur **"Redémarrer maintenant"**
2. Message : "Veuillez retirer le support d'installation"
3. **Appuyez sur Entrée**

> 💡 VirtualBox éjecte automatiquement l'ISO au redémarrage dans les versions récentes.

### Premier démarrage sur système installé

- Menu GRUB (si configuré)
- Chargement de Linux Mint
- Écran de connexion
- **Connectez-vous** avec votre mot de passe

---

## Étape 8 : Installer les Guest Additions (CRUCIAL)

Les **Guest Additions** sont des pilotes et utilitaires qui améliorent drastiquement les performances et l'intégration de la VM.

### Qu'apportent les Guest Additions ?

Sans Guest Additions :
- ❌ Résolution fixe basse (800×600 ou 1024×768)
- ❌ Souris lente et saccadée
- ❌ Pas de copier-coller hôte ↔ VM
- ❌ Pas de glisser-déposer
- ❌ Pas de dossiers partagés
- ❌ Performances graphiques médiocres

Avec Guest Additions :
- ✅ Résolution adaptative (plein écran automatique)
- ✅ Souris fluide et intégrée
- ✅ Copier-coller bidirectionnel
- ✅ Glisser-déposer de fichiers
- ✅ Dossiers partagés fonctionnels
- ✅ Accélération graphique
- ✅ Meilleures performances globales

> 🔴 **Les Guest Additions sont INDISPENSABLES**. Ne les sautez pas !

### Installation des Guest Additions

#### Étape 1 : Insérer le CD Guest Additions

Dans la fenêtre de votre VM en cours d'exécution :

1. Menu VirtualBox : **Périphériques** → **Insérer l'image CD des Additions invité...**

Un CD virtuel se monte dans Linux Mint :
```
┌────────────────────────────────────────┐
│  Un support de stockage a été inséré   │
│                                        │
│  VBox_GAs_7.0.12                       │
│                                        │
│  [Ouvrir avec Gestionnaire de fichiers]│
│  [Exécuter]                            │
│  [Annuler]                             │
└────────────────────────────────────────┘
```

Cliquez sur **"Annuler"** (nous installerons manuellement).

#### Étape 2 : Installer depuis le terminal

Ouvrez un **terminal** :
- **Menu** → **Terminal**
- Ou : **Ctrl + Alt + T**

**Installez les prérequis :**
```bash
sudo apt update  
sudo apt install build-essential dkms linux-headers-$(uname -r)  
```

Entrez votre mot de passe quand demandé.

**Montez le CD (si pas déjà fait) :**
```bash
sudo mkdir -p /mnt/cdrom  
sudo mount /dev/cdrom /mnt/cdrom  
```

**Lancez l'installation :**
```bash
cd /mnt/cdrom  
sudo ./VBoxLinuxAdditions.run  
```

**Sortie attendue :**
```
Verifying archive integrity... All good.  
Uncompressing VirtualBox 7.0.12 Guest Additions for Linux  
VirtualBox Guest Additions installer  
Copying additional installer modules ...  
Installing additional modules ...  
VirtualBox Guest Additions: Building the VirtualBox Guest Additions kernel  
modules.  This may take a while.  
VirtualBox Guest Additions: To build modules for other installed kernels, run  
VirtualBox Guest Additions:   /sbin/rcvboxadd quicksetup <version>  
VirtualBox Guest Additions: or  
VirtualBox Guest Additions:   /sbin/rcvboxadd quicksetup all  
VirtualBox Guest Additions: Building the modules for kernel 5.15.0-91-generic.  
VirtualBox Guest Additions: Running kernel modules will not be replaced until  
the system is restarted  
```

**Durée :** 2-5 minutes

#### Étape 3 : Redémarrer

```bash
sudo reboot
```

La VM redémarre.

#### Étape 4 : Vérification

Après redémarrage :

1. **Redimensionnez la fenêtre de la VM**
   - La résolution s'adapte automatiquement ✅

2. **Testez le copier-coller**
   - Copiez du texte sur votre PC hôte
   - Collez dans la VM (Ctrl+V) ✅

3. **Testez le plein écran**
   - **Menu VM** → **Affichage** → **Mode plein écran**
   - Ou : **Ctrl Droite + F**
   - La VM occupe tout l'écran ✅

4. **Vérifiez les modules**
   ```bash
   lsmod | grep vbox
   ```
   Vous devriez voir plusieurs modules `vboxguest`, `vboxsf`, etc.

---

## Étape 9 : Configuration des dossiers partagés

### Créer un dossier partagé

**Sur votre PC hôte (Windows) :**
1. Créez un dossier, ex: `C:\VM_Partage`
2. Mettez-y des fichiers test

**Dans VirtualBox :**
1. **Périphériques** → **Dossiers partagés** → **Paramètres des dossiers partagés**
2. Cliquez sur **"+"** (Ajouter)
3. **Chemin du dossier** : `C:\VM_Partage`
4. **Nom du dossier** : `partage` (nom dans Linux)
5. ☑️ **Montage automatique**
6. ☑️ **Rendre permanent**
7. Cliquez **"OK"**

### Accéder au dossier partagé dans Linux Mint

Le dossier est monté dans `/media/sf_partage` :

```bash
cd /media/sf_partage  
ls  
```

**Problème de permissions ?**

Ajoutez votre utilisateur au groupe `vboxsf` :

```bash
sudo usermod -aG vboxsf $USER
```

**Déconnectez-vous et reconnectez-vous** pour que le changement prenne effet.

Ou redémarrez :
```bash
sudo reboot
```

Maintenant, vous pouvez accéder à `/media/sf_partage` librement.

### Créer un lien symbolique (optionnel)

Pour un accès plus facile, créez un lien dans votre home :

```bash
ln -s /media/sf_partage ~/Partage
```

Maintenant, `~/Partage` pointe vers le dossier partagé.

---

## Étape 10 : Snapshots (instantanés)

Les **snapshots** sont des sauvegardes de l'état complet de votre VM à un instant T.

### Qu'est-ce qu'un snapshot ?

Un snapshot capture :
- L'état du disque dur virtuel
- L'état de la RAM
- L'état des périphériques
- La configuration

**Utilité :**
- 📸 Sauvegarder avant une modification risquée
- 🔄 Revenir en arrière en cas de problème
- 🧪 Tester des configurations sans risque
- 📚 Avoir plusieurs états (clean install, configured, with apps, etc.)

> 💡 **Analogie** : C'est comme la sauvegarde d'un jeu vidéo. Vous pouvez revenir à ce point à tout moment.

### Créer un snapshot

**Méthode 1 : Via le menu (VM éteinte recommandé)**
1. Sélectionnez votre VM (éteinte)
2. Cliquez sur **"Instantanés"** (ou **Snapshots**)
3. Cliquez sur **"Prendre"**
4. **Nom** : "Installation propre" ou "Système configuré"
5. **Description** : Détails sur cet état
6. Cliquez **"OK"**

**Méthode 2 : Via le menu (VM en cours)**
1. **Machine** → **Prendre un instantané**
2. Nommez l'instantané
3. Cliquez **"OK"**

### Restaurer un snapshot

1. **Éteindre la VM** (si allumée)
2. Cliquez sur **"Instantanés"**
3. Sélectionnez l'instantané à restaurer
4. Cliquez sur **"Restaurer"**
5. Confirmez

> ⚠️ **Attention** : Restaurer un snapshot efface tous les changements faits APRÈS ce snapshot.

### Gestion des snapshots

**Supprimer un snapshot :**
1. Sélectionnez-le
2. Cliquez sur **"Supprimer"**
3. Confirmez

**Cloner à partir d'un snapshot :**
1. Clic droit sur le snapshot
2. **"Cloner"**
3. Créez une nouvelle VM basée sur cet état

---

## Astuces et optimisations

### Mode plein écran

**Activer :**
- **Menu VM** → **Affichage** → **Mode plein écran**
- Ou : **Ctrl Droite + F**

**Désactiver :**
- **Ctrl Droite + F** à nouveau
- Ou : Barre en haut de l'écran → icône sortie plein écran

### Mode transparent (seamless)

**Mode transparent** : Les fenêtres Linux apparaissent directement sur votre bureau Windows !

**Activer :**
- **Menu VM** → **Affichage** → **Mode transparent**
- Ou : **Ctrl Droite + L**

**Résultat :**
- Le bureau Linux Mint disparaît
- Seules les fenêtres Linux sont visibles
- Elles se mélangent avec vos fenêtres Windows

> 💡 Super pour utiliser une application Linux sans quitter Windows.

### Optimisation des performances

**1. Allouer plus de RAM (si possible)**
- VM éteinte → Paramètres → Système → Carte mère
- Augmentez la RAM

**2. Allouer plus de CPU (si possible)**
- Paramètres → Système → Processeur
- Augmentez le nombre de cœurs

**3. Utiliser un SSD pour le disque hôte**
- Les VMs sur SSD sont BEAUCOUP plus rapides

**4. Activer l'accélération 3D**
- Paramètres → Affichage → Activer l'accélération 3D

**5. Utiliser VMSVGA comme contrôleur**
- Paramètres → Affichage → Contrôleur graphique : VMSVGA

**6. Installer les Guest Additions**
- Déjà fait ci-dessus

**7. Désactiver les effets visuels dans Linux**
- **Paramètres système** → **Effets** → Niveau : Léger

**8. Utiliser un thème léger**
- Thèmes sans transparence et effets complexes

### Exportation et importation de VMs

**Exporter une VM** (pour partage ou sauvegarde) :
1. **Fichier** → **Exporter un appareil virtuel**
2. Sélectionnez votre VM
3. Format : OVA (recommandé, compatible)
4. Choisissez l'emplacement
5. Cliquez **"Exporter"**

**Importer une VM :**
1. **Fichier** → **Importer un appareil virtuel**
2. Sélectionnez le fichier .ova
3. Ajustez les paramètres si nécessaire
4. Cliquez **"Importer"**

---

## Limitations et différences avec une installation native

### Limitations

- ❌ **Performances** : 30-50% plus lent qu'une installation native
- ❌ **Graphismes 3D** : Accélération limitée, pas bon pour jeux récents
- ❌ **GPU passthrough complexe** : Utiliser le GPU physique est très technique
- ❌ **Périphériques USB** : Peut nécessiter configuration pour certains
- ❌ **Consommation RAM** : L'hôte et la VM consomment de la RAM
- ❌ **Webcam** : Peut nécessiter configuration manuelle

### Différences notables

**Positives :**
- ✅ Snapshots instantanés
- ✅ Isolation totale (sécurité)
- ✅ Clonage facile
- ✅ Test sans risque

**Négatives :**
- ❌ Pas idéal pour usage quotidien intensif
- ❌ Performances en retrait
- ❌ Configuration plus complexe que natif

---

## Dépannage

### La VM ne démarre pas

**Erreur : "VT-x is not available"**
- **Cause** : Virtualisation désactivée dans le BIOS
- **Solution** : Activez VT-x/AMD-V dans le BIOS (voir Étape 1)

**Erreur : "VERR_VMX_MSR_ALL_VMX_DISABLED"**
- **Cause** : Hyper-V ou Device Guard activé (Windows)
- **Solution** : Désactivez Hyper-V
  ```cmd
  bcdedit /set hypervisorlaunchtype off
  ```
  Redémarrez Windows.

### La résolution ne s'adapte pas

**Cause** : Guest Additions non installés ou non fonctionnels

**Solution :**
1. Vérifiez que Guest Additions sont installés
2. Réinstallez-les si nécessaire
3. Redémarrez la VM

### Le copier-coller ne fonctionne pas

**Cause** : Guest Additions manquants ou presse-papiers partagé désactivé

**Solution :**
1. Installez/réinstallez Guest Additions
2. **Paramètres VM** → **Général** → **Avancé** → Presse-papiers partagé : **Bidirectionnel**
3. Redémarrez la VM

### La VM est très lente

**Causes possibles et solutions :**

**1. Pas assez de RAM allouée**
- Augmentez la RAM dans les paramètres

**2. Disque dur hôte lent (HDD)**
- Utilisez un SSD pour héberger la VM

**3. Trop peu de CPU alloués**
- Augmentez le nombre de cœurs

**4. Guest Additions manquants**
- Installez-les

**5. Accélération 3D désactivée**
- Activez dans Paramètres → Affichage

**6. Effets visuels trop lourds**
- Réduisez les effets dans Linux Mint

### Pas de son dans la VM

**Solution :**
1. **Paramètres VM** → **Audio** → Vérifiez que "Activer l'audio" est coché
2. Contrôleur audio : Essayez **Intel HD Audio** au lieu de ICH AC97
3. Dans Linux : Vérifiez le volume et le périphérique de sortie

### Clavier en QWERTY au lieu d'AZERTY

**Pendant l'installation :**
- Sélectionnez "Français" dans la configuration clavier

**Après installation :**
- **Paramètres système** → **Clavier** → **Agencements** → Ajoutez "Français"

### Erreur "Kernel driver not installed"

**Sous Windows :**
- Réinstallez VirtualBox
- Redémarrez Windows
- Vérifiez que les pilotes VirtualBox sont signés

**Sous Linux hôte :**
```bash
sudo /sbin/vboxconfig
```

---

## Cas d'usage avancés

### Multi-VM : Plusieurs Linux en parallèle

Vous pouvez créer plusieurs VMs :
- Ubuntu dans une VM
- Fedora dans une autre
- Arch Linux dans une troisième
- Toutes fonctionnent en même temps (si assez de RAM)

**Réseau entre VMs :**
- Mode **"Réseau interne"** pour communiquer entre VMs
- Créez votre propre réseau virtuel

### Tester des configurations système

**Scénario :** Vous voulez tester une nouvelle configuration sans risque.

1. Créez un **snapshot** "État stable"
2. Faites vos modifications/tests
3. Si ça marche : Gardez
4. Si ça casse : Restaurez le snapshot

### Environnement de développement isolé

**Avantage :** Développez sans polluer votre PC hôte.

- Installez vos outils de dev dans la VM
- Testez des serveurs web, bases de données
- Si vous cassez quelque chose, restaurez un snapshot
- Clone la VM pour différents projets

### Formation et apprentissage

**Idéal pour :**
- Apprendre Linux sans risque
- Suivre des tutoriels en ligne de commande
- Pratiquer l'administration système
- Casser et réparer (apprentissage par l'erreur)

---

## Questions fréquentes

### Puis-je utiliser ma VM Linux Mint au quotidien ?

**Oui, mais :**
- Pour navigation web, bureautique, développement : OUI
- Pour gaming, montage vidéo, graphisme 3D : NON (trop lent)

### Quelle est la différence avec WSL ?

**WSL (Windows Subsystem for Linux) :**
- Plus léger
- Ligne de commande surtout
- Pas d'interface graphique complète (WSL 1)
- Mieux intégré avec Windows

**VirtualBox :**
- Environnement Linux complet
- Interface graphique native
- Plus isolé
- Plus lourd

> 💡 WSL pour développement en ligne de commande, VirtualBox pour environnement Linux complet.

### Puis-je transférer ma VM vers un vrai PC ?

**Oui, mais complexe :**
- Exportez le disque virtuel
- Utilisez Clonezilla ou dd pour copier sur un vrai disque
- Réinstallez GRUB
- Réinstallez les pilotes matériels

> 💡 Plus simple : Réinstallez Linux nativement.

### Ma VM peut-elle être infectée par un virus ?

**Oui, la VM peut être infectée.**

**MAIS :**
- Le virus reste **confiné** dans la VM
- Il ne peut pas (normalement) infecter votre PC hôte
- Restaurez un snapshot sain en cas de problème

> 💡 Les VMs offrent une excellente isolation de sécurité.

### Puis-je supprimer VirtualBox après avoir créé la VM ?

**Non !** VirtualBox est nécessaire pour exécuter la VM.

**Vous pouvez :**
- Supprimer une VM spécifique (libère l'espace)
- Garder VirtualBox pour créer d'autres VMs

### Combien d'espace disque la VM occupe-t-elle ?

**Disque dynamique :**
- Départ : ~10-15 GB (système de base)
- Grandit avec vos installations
- Maximum : La taille que vous avez définie

**Disque fixe :**
- Réserve immédiatement toute la taille définie
- Exemple : 50 GB définis = 50 GB utilisés sur l'hôte

---

## Alternatives à VirtualBox

### VMware Workstation Player (Gratuit)

**Avantages :**
- Meilleures performances que VirtualBox
- Meilleure intégration graphique
- Plus stable pour certains cas

**Inconvénients :**
- Interface moins intuitive
- Moins de fonctionnalités en version gratuite

### QEMU/KVM (Linux uniquement)

**Avantages :**
- Excellentes performances
- Intégré au kernel Linux
- Utilisé en production (serveurs)

**Inconvénients :**
- Configuration complexe
- Ligne de commande surtout
- Courbe d'apprentissage raide

### Hyper-V (Windows Pro)

**Avantages :**
- Intégré à Windows
- Très performant
- Utilisé professionnellement

**Inconvénients :**
- Windows Pro ou supérieur requis
- Incompatible avec VirtualBox (conflit)

---

## Prochaines étapes

Maintenant que Linux Mint tourne dans votre VM :

### Découverte et apprentissage

➡️ **[3. Migration depuis Windows](/03-migration-depuis-windows/README.md)**

Retrouvez vos repères si vous venez de Windows.

➡️ **[4. Découverte de l'environnement de bureau](/04-decouverte-de-lenvironnement-de-bureau/README.md)**

Explorez l'interface Cinnamon.

➡️ **[7. Le terminal et commandes de base](/07-le-terminal-et-commandes-de-base/README.md)**

Apprenez la ligne de commande sans risque !

### Quand passer à une installation native ?

Installez Linux Mint nativement si :
- ✅ Vous êtes à l'aise avec Linux Mint
- ✅ Vous voulez de meilleures performances
- ✅ Vous voulez utiliser Linux au quotidien
- ✅ Vous avez besoin de support graphique 3D complet

---

## Ressources complémentaires

### Documentation VirtualBox

- 📖 [Manuel utilisateur VirtualBox](https://www.virtualbox.org/manual/)
- 💬 [Forums VirtualBox](https://forums.virtualbox.org/)
- 🎥 [Chaîne YouTube VirtualBox](https://www.youtube.com/virtualbox)

### Communauté Linux Mint

- 💬 [Forum Linux Mint](https://forums.linuxmint.com/)
- 📖 [Documentation Linux Mint](https://linuxmint.com/documentation.php)
- 📱 [Reddit r/linuxmint](https://reddit.com/r/linuxmint)

---

## Conclusion

Les machines virtuelles sont un **outil formidable** pour découvrir Linux Mint en toute sécurité. Elles permettent de :
- 🎓 **Apprendre** sans risque
- 🧪 **Expérimenter** librement
- 🔄 **Revenir en arrière** facilement
- 🛡️ **Protéger** votre système principal

**Points clés à retenir :**
1. ✅ Activez la virtualisation dans le BIOS
2. ✅ Allouez suffisamment de ressources (mais pas trop)
3. ✅ Installez les Guest Additions (indispensable)
4. ✅ Créez des snapshots avant modifications importantes
5. ✅ Une VM ne remplace pas une installation native pour usage intensif

---

**Félicitations ! Vous avez installé Linux Mint dans une machine virtuelle ! 🎉**

**Explorez, expérimentez, et amusez-vous avec Linux sans aucun risque ! 🚀🐧**

**Quand vous serez prêt, n'hésitez pas à installer Linux Mint nativement pour profiter de toute sa puissance ! 💪**

⏭️ [Migration depuis Windows](/03-migration-depuis-windows/README.md)
