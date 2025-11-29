🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 15.1 Wine et configuration

## Introduction

Wine est un outil qui permet d'exécuter des applications Windows sur Linux Mint sans avoir besoin d'installer Windows. Le nom "Wine" est un acronyme récursif qui signifie "**Wine Is Not an Emulator**" (Wine n'est pas un émulateur).

Contrairement à un émulateur qui simulerait un ordinateur virtuel complet, Wine traduit en temps réel les instructions Windows en instructions Linux. C'est comme si Wine servait d'interprète entre une application Windows et votre système Linux.

### Quand utiliser Wine ?

Wine est particulièrement utile dans ces situations :

- Vous avez besoin d'un logiciel Windows spécifique qui n'a pas d'alternative Linux
- Vous voulez tester une application Windows sans redémarrer en dual-boot
- Vous souhaitez utiliser des jeux Windows (bien que Steam Proton soit souvent préférable pour les jeux)
- Vous devez accéder à des logiciels professionnels uniquement disponibles sur Windows

### Limitations à connaître

Il est important de comprendre que :

- **Toutes les applications Windows ne fonctionnent pas** parfaitement avec Wine
- Les performances peuvent être légèrement inférieures à une installation Windows native
- Certaines fonctionnalités avancées (pilotes matériels spécifiques, DRM) peuvent ne pas fonctionner
- Les logiciels très récents ou très anciens peuvent poser des problèmes

> **💡 Conseil** : Avant d'installer un logiciel avec Wine, consultez la base de données [WineHQ AppDB](https://appdb.winehq.org/) pour vérifier sa compatibilité et consulter les retours d'autres utilisateurs.

---

## Installation de Wine

### Méthode 1 : Installation depuis le gestionnaire de logiciels (recommandée pour débutants)

1. Ouvrez le **Gestionnaire de logiciels** depuis le menu principal
2. Tapez "wine" dans la barre de recherche
3. Recherchez le paquet nommé **Wine** ou **Wine Stable**
4. Cliquez sur **Installer**
5. Entrez votre mot de passe administrateur si demandé

### Méthode 2 : Installation via le terminal (plus rapide)

Ouvrez un terminal et exécutez ces commandes :

```bash
# Mise à jour de la liste des paquets
sudo apt update

# Installation de Wine
sudo apt install wine wine64 wine32 -y
```

**Explication des paquets** :
- `wine` : paquet principal
- `wine64` : support des applications 64 bits
- `wine32` : support des applications 32 bits (encore très utilisé)

### Vérification de l'installation

Pour vérifier que Wine est correctement installé, tapez dans un terminal :

```bash
wine --version
```

Vous devriez voir s'afficher la version installée, par exemple : `wine-8.0.2`

---

## Premier lancement et configuration initiale

### Configuration automatique au premier démarrage

Lors de votre première utilisation de Wine, une fenêtre de configuration s'ouvrira automatiquement. Wine va :

1. Créer un **préfixe Wine** (un environnement Windows virtuel)
2. Installer des composants de base nécessaires (polices, bibliothèques)
3. Créer une structure de dossiers similaire à Windows dans votre dossier personnel

Cette opération peut prendre quelques minutes. **Laissez-la se terminer complètement**.

### Le préfixe Wine par défaut

Wine crée un dossier caché dans votre répertoire personnel :

```
~/.wine/
```

Ce dossier contient :
- Un **lecteur C:** virtuel (`drive_c/`)
- Des dossiers Windows familiers : Program Files, Users, Windows, etc.
- Les fichiers de configuration (registre Windows simulé)

> **📁 Emplacement pratique** : Vous pouvez accéder à votre préfixe Wine en tapant dans le terminal : `cd ~/.wine/drive_c`

---

## Utilisation de l'outil de configuration Wine

Wine inclut un outil graphique de configuration appelé **winecfg**. Pour l'ouvrir :

```bash
winecfg
```

### Onglet Applications

Permet de définir la version de Windows que Wine doit simuler :

- **Windows 10** : pour les logiciels récents
- **Windows 7** : bon compromis, compatible avec la majorité des logiciels
- **Windows XP** : pour les logiciels plus anciens

**Comment choisir ?**
1. Commencez par Windows 10 (par défaut)
2. Si l'application ne fonctionne pas, essayez Windows 7
3. Pour les très vieux logiciels (avant 2010), tentez Windows XP

### Onglet Bibliothèques

Cet onglet permet de gérer les DLL (bibliothèques Windows).

**Pour les débutants** : ne modifiez rien ici sauf si un tutoriel spécifique vous le demande. Wine gère automatiquement la plupart des bibliothèques.

### Onglet Affichage

Options utiles pour l'affichage graphique :

- **Résolution de l'écran** : ajustez si les applications Windows s'affichent trop petites ou trop grandes
- **Émuler un bureau virtuel** : crée une fenêtre dédiée pour l'application (utile pour les jeux en plein écran)
  - Cochez cette option et définissez une résolution (ex: 1920x1080)

### Onglet Audio

Wine détecte normalement votre configuration audio automatiquement. Si vous rencontrez des problèmes de son :

1. Vérifiez que le pilote **PulseAudio** ou **PipeWire** est sélectionné
2. Utilisez le bouton **Tester le son** pour vérifier

---

## Lancer une application Windows avec Wine

### Méthode graphique simple

1. **Téléchargez** votre fichier d'installation Windows (.exe)
2. **Faites un clic droit** sur le fichier .exe
3. Sélectionnez **Ouvrir avec Wine Chargeur de programmes Windows**
4. Suivez l'assistant d'installation comme sous Windows

### Méthode par le terminal

```bash
wine /chemin/vers/votre/programme.exe
```

Exemple :
```bash
wine ~/Téléchargements/setup.exe
```

### Lancer un programme déjà installé

Les programmes s'installent généralement dans :
```
~/.wine/drive_c/Program Files/
```

Pour lancer un programme installé :
```bash
wine ~/.wine/drive_c/Program\ Files/MonProgramme/programme.exe
```

---

## Installation de Winetricks

**Winetricks** est un script d'assistance qui facilite l'installation de composants Windows supplémentaires (polices, bibliothèques, runtime).

### Installation

```bash
sudo apt install winetricks
```

### Utilisation graphique

Lancez simplement :
```bash
winetricks
```

Une interface graphique s'ouvre avec plusieurs options :

#### 1. Installer une police Windows

**Polices Windows** → Sélectionnez `corefonts` → OK

Cela installe les polices Arial, Times New Roman, etc., souvent nécessaires pour un affichage correct.

#### 2. Installer des bibliothèques courantes

**Installer une DLL ou composant Windows** → Recherchez par exemple :
- `dotnet48` : .NET Framework 4.8 (pour applications .NET)
- `vcrun2019` : Visual C++ Runtime 2019
- `directx9` : DirectX 9 (pour jeux anciens)

#### 3. Modifier les paramètres

**Modifier les paramètres** → Vous pouvez :
- Changer le thème Windows
- Activer le mode sombre
- Configurer les paramètres DPI (pour écrans haute résolution)

---

## Configuration avancée : Créer des préfixes séparés

Par défaut, toutes vos applications Windows partagent le même environnement (`~/.wine`). Mais vous pouvez créer des **préfixes séparés** pour isoler différentes applications.

### Pourquoi créer des préfixes séparés ?

- Éviter les conflits entre applications
- Tester différentes versions de Windows
- Garder un environnement propre pour chaque logiciel important

### Créer un nouveau préfixe

```bash
WINEPREFIX=~/.wine-monapp winecfg
```

Cela crée un nouveau préfixe dans `~/.wine-monapp`

### Installer une application dans ce préfixe

```bash
WINEPREFIX=~/.wine-monapp wine ~/Téléchargements/setup.exe
```

### Lancer l'application depuis ce préfixe

```bash
WINEPREFIX=~/.wine-monapp wine ~/.wine-monapp/drive_c/Program\ Files/MonApp/app.exe
```

---

## Trucs et astuces pour débutants

### 1. Créer un lanceur pour votre application Windows

Au lieu de taper des commandes à chaque fois, créez un **lanceur** :

1. Clic droit sur le bureau → **Créer un lanceur**
2. **Nom** : Nom de votre application
3. **Commande** : `wine /chemin/vers/application.exe`
4. **Icône** : Choisissez une icône
5. Cliquez sur **OK**

### 2. Les fichiers Windows et Linux

Les applications Windows voient votre système Linux via le lecteur **Z:**

- `Z:/home/votre-nom/` correspond à votre dossier personnel Linux
- Vous pouvez accéder à vos documents Linux depuis une application Windows !

### 3. Désinstaller une application Windows

Utilisez l'outil de désinstallation de Wine :

```bash
wine uninstaller
```

Une fenêtre s'ouvre avec la liste des programmes installés, comme le "Ajout/Suppression de programmes" de Windows.

### 4. Nettoyer Wine

Si Wine pose problème ou si vous voulez repartir de zéro :

```bash
# Sauvegarder d'abord vos données importantes !
rm -rf ~/.wine
winecfg  # Recréera un préfixe propre
```

---

## Résolution des problèmes courants

### L'application ne se lance pas

1. **Vérifiez la compatibilité** sur WineHQ AppDB
2. **Essayez une autre version de Windows** dans winecfg
3. **Installez les dépendances** nécessaires avec Winetricks (dotnet, vcrun, etc.)
4. **Consultez les logs** : lancez l'application depuis le terminal pour voir les messages d'erreur

### L'application plante ou se fige

- Essayez d'activer **Émuler un bureau virtuel** dans winecfg
- Réduisez la résolution dans les paramètres de l'application
- Désactivez les effets graphiques avancés

### Pas de son

1. Ouvrez **winecfg** → Onglet Audio
2. Vérifiez que **PulseAudio** ou **PipeWire** est sélectionné
3. Testez le son avec le bouton dédié

### Affichage flou ou texte trop petit

Dans **winecfg** → Affichage :
- Augmentez le **DPI** (96 → 120 ou 144)
- Ou utilisez un **bureau virtuel** avec une résolution adaptée

### Erreur "mscoree.dll manquant"

L'application nécessite .NET Framework :

```bash
winetricks dotnet48
```

---

## Alternatives à Wine

Si Wine ne répond pas à vos besoins, considérez ces alternatives :

### 1. Bottles (interface moderne pour Wine)
- Interface graphique élégante
- Gestion facile de plusieurs préfixes
- Plus accessible que Wine en ligne de commande

### 2. PlayOnLinux
- Scripts préconçus pour des applications populaires
- Installation simplifiée

### 3. Machines virtuelles
- VirtualBox ou GNOME Boxes
- Windows complet dans une machine virtuelle
- Meilleures performances pour certaines applications

### 4. Chercher une alternative native Linux
- Souvent la meilleure solution à long terme
- Performances optimales
- Meilleure intégration avec le système

---

## Conclusion

Wine est un outil puissant qui permet de combler le fossé entre Windows et Linux. Bien qu'il ne soit pas parfait, il offre une solution pratique pour exécuter des applications Windows sans quitter Linux Mint.

**Points clés à retenir** :

- ✅ Wine traduit les instructions Windows en instructions Linux
- ✅ Tous les logiciels ne fonctionnent pas parfaitement
- ✅ Winetricks facilite l'installation de composants supplémentaires
- ✅ Les préfixes séparés permettent d'isoler les applications
- ✅ Consultez toujours WineHQ AppDB avant d'installer

N'hésitez pas à expérimenter et à consulter la communauté Linux Mint si vous rencontrez des difficultés. Wine s'améliore constamment et de plus en plus d'applications Windows deviennent compatibles !

---


⏭️ [PlayOnLinux / Bottles](/15-applications-windows-sous-linux/02-playonlinux-bottles.md)
