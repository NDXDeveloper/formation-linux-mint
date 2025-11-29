🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 15.2 PlayOnLinux / Bottles

## Introduction

Nous avons vu dans la section précédente que Wine permet d'exécuter des applications Windows sur Linux, mais son utilisation en ligne de commande peut sembler complexe pour les débutants. C'est ici qu'interviennent **PlayOnLinux** et **Bottles** : des interfaces graphiques qui simplifient grandement l'utilisation de Wine.

Ces outils vous permettent de :
- Installer des applications Windows en quelques clics
- Gérer plusieurs versions de Wine facilement
- Créer des environnements isolés pour chaque application
- Bénéficier de scripts d'installation automatiques pour des logiciels populaires

> **💡 En résumé** : Si Wine est le moteur, PlayOnLinux et Bottles sont les tableaux de bord qui le rendent accessible à tous.

---

## PlayOnLinux : L'ancêtre fiable

### Qu'est-ce que PlayOnLinux ?

**PlayOnLinux** (souvent abrégé POL) est l'un des premiers outils graphiques créés pour simplifier Wine. Lancé en 2007, il reste très populaire grâce à :

- Une **vaste bibliothèque de scripts** pour installer automatiquement des centaines d'applications
- Une interface simple et claire
- Une communauté active avec beaucoup de tutoriels disponibles
- La gestion automatique de plusieurs versions de Wine

### Points forts de PlayOnLinux

- ✅ **Scripts d'installation automatiques** : installation en un clic pour de nombreux logiciels
- ✅ **Stable et éprouvé** : fonctionne depuis des années
- ✅ **Documentation abondante** : facile de trouver de l'aide
- ✅ **Gestion des versions Wine** : installe automatiquement la bonne version

### Limitations à connaître

- ⚠️ Interface un peu datée visuellement
- ⚠️ Certains scripts peuvent être obsolètes pour les logiciels récents
- ⚠️ Développement moins actif qu'avant

---

## Installation de PlayOnLinux

### Via le gestionnaire de logiciels

1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez "**PlayOnLinux**"
3. Cliquez sur **Installer**
4. Entrez votre mot de passe si demandé

### Via le terminal

```bash
sudo apt update
sudo apt install playonlinux
```

### Premier lancement

Une fois installé, lancez PlayOnLinux depuis le menu principal :

**Menu → Jeux → PlayOnLinux**

Au premier lancement, PlayOnLinux va :
- Vérifier votre configuration
- Télécharger les composants nécessaires
- Créer sa structure de dossiers

---

## Utiliser PlayOnLinux

### Interface principale

L'interface de PlayOnLinux est divisée en plusieurs zones :

- **Liste des applications** : au centre, vos programmes Windows installés
- **Barre d'outils** : en haut, les boutons d'action principaux
- **Panneau latéral** : informations et raccourcis rapides

### Installer une application avec un script automatique

C'est la méthode la plus simple pour les logiciels populaires.

#### Étape 1 : Cliquer sur "Installer"

1. Cliquez sur le bouton **Installer** (avec l'icône +) dans la barre d'outils
2. Une nouvelle fenêtre s'ouvre avec la liste des applications disponibles

#### Étape 2 : Rechercher votre application

1. Utilisez la **barre de recherche** en haut
2. Ou naviguez par **catégories** (Bureautique, Jeux, Multimédia, etc.)
3. Sélectionnez l'application souhaitée

#### Étape 3 : Suivre l'assistant

1. Cliquez sur **Installer**
2. Lisez et acceptez les informations affichées
3. PlayOnLinux va :
   - Télécharger la version de Wine appropriée
   - Créer un environnement dédié (lecteur virtuel)
   - Installer les dépendances nécessaires
   - Vous guider dans l'installation du logiciel

#### Étape 4 : Installation du logiciel

- Si vous avez déjà le fichier d'installation (.exe), sélectionnez-le
- Sinon, PlayOnLinux peut parfois le télécharger pour vous
- Suivez l'assistant d'installation comme sous Windows

Une fois terminé, votre application apparaît dans la liste principale !

### Installer une application manuellement

Si votre logiciel n'a pas de script automatique :

1. Cliquez sur **Installer** → **Installer un programme non listé**
2. Suivez l'assistant :
   - Choisissez **Installer un programme dans un nouveau lecteur virtuel**
   - Donnez un nom à ce lecteur (ex: "MonLogiciel")
   - Sélectionnez la version de Wine (gardez celle recommandée)
   - Choisissez si vous voulez un bureau Windows virtuel (32 ou 64 bits)
3. PlayOnLinux créera l'environnement
4. Parcourez pour sélectionner votre fichier .exe
5. Suivez l'installation normalement

### Lancer une application

Depuis l'interface principale :
1. **Double-cliquez** sur l'application dans la liste
2. Ou sélectionnez-la et cliquez sur **Exécuter**

Vous pouvez aussi créer un raccourci sur le bureau :
- Sélectionnez l'application
- Cliquez sur **Créer un raccourci**

### Configurer une application

Pour accéder aux paramètres d'une application :

1. Sélectionnez l'application
2. Cliquez sur **Configurer** dans le panneau de droite
3. Une nouvelle fenêtre s'ouvre avec plusieurs onglets :

#### Onglet Général
- **Exécuter** : lancer l'application
- **Tuer** : fermer de force l'application
- **Désinstaller** : supprimer l'application

#### Onglet Wine
- **Configurer Wine** : ouvre winecfg pour ce lecteur virtuel
- **Version de Wine** : changer la version utilisée
- **Windows Reboot** : redémarrer le lecteur virtuel

#### Onglet Affichage
- **Capture du pointeur de souris** : utile pour les jeux
- **GLSL Support** : amélioration graphique
- **Direct Draw Renderer** : rendu graphique

### Désinstaller une application

1. Sélectionnez l'application dans la liste
2. Cliquez sur le bouton **Supprimer** (icône -)
3. Confirmez la suppression

Cela supprimera l'application ET son lecteur virtuel dédié.

---

## Bottles : La solution moderne

### Qu'est-ce que Bottles ?

**Bottles** est un gestionnaire Wine nouvelle génération, lancé en 2020. Il apporte une approche moderne et élégante à la gestion des applications Windows sous Linux.

### Pourquoi Bottles est l'avenir

- ✅ **Interface moderne et intuitive** : design épuré et agréable
- ✅ **Mises à jour régulières** : développement très actif
- ✅ **Gestion intelligente** : détecte automatiquement les besoins
- ✅ **Environnements pré-configurés** : Gaming, Applications, Custom
- ✅ **Intégration système** : s'intègre parfaitement à Linux Mint
- ✅ **Support Flatpak** : installation et mises à jour simplifiées

### Philosophie de Bottles

Bottles organise vos applications Windows dans des "**bouteilles**" (bottles en anglais). Chaque bouteille est un environnement isolé avec :
- Sa propre version de Wine
- Ses propres paramètres
- Ses bibliothèques et dépendances
- Ses applications

---

## Installation de Bottles

### Méthode recommandée : Flatpak

Bottles fonctionne mieux en version Flatpak pour bénéficier des dernières mises à jour.

#### Activer Flatpak (si ce n'est pas déjà fait)

```bash
sudo apt install flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

#### Installer Bottles

```bash
flatpak install flathub com.usebottles.bottles
```

### Lancer Bottles

Depuis le menu : **Menu → Accessoires → Bottles**

Ou via le terminal :
```bash
flatpak run com.usebottles.bottles
```

### Premier lancement et configuration initiale

Au premier lancement, Bottles va :

1. **Télécharger les dépendances** nécessaires (runners Wine, bibliothèques)
2. **Configurer l'environnement** de base
3. **Afficher le tutoriel** de bienvenue (prenez le temps de le lire !)

Cette étape peut prendre quelques minutes selon votre connexion Internet.

---

## Utiliser Bottles

### Interface principale

L'interface de Bottles est organisée en trois sections :

- **Barre latérale gauche** : navigation entre vos bouteilles
- **Zone centrale** : détails et actions de la bouteille sélectionnée
- **Barre supérieure** : recherche et paramètres globaux

### Créer votre première bouteille

#### Étape 1 : Cliquer sur "Nouvelle bouteille"

1. Cliquez sur le bouton **+** (Nouvelle bouteille) en haut à gauche
2. Une fenêtre de création s'ouvre

#### Étape 2 : Choisir le type d'environnement

Bottles propose trois types pré-configurés :

**🎮 Gaming (Jeux)**
- Optimisé pour les jeux Windows
- Active les composants DirectX, DXVK
- Meilleures performances graphiques
- **Utilisez ce type pour** : jeux, applications 3D

**📄 Application**
- Configuration standard pour logiciels bureautiques
- Plus léger que Gaming
- Bonnes performances générales
- **Utilisez ce type pour** : logiciels office, utilitaires, outils professionnels

**🔧 Custom (Personnalisé)**
- Environnement vierge à configurer vous-même
- Pour utilisateurs avancés
- **Utilisez ce type pour** : cas spéciaux, configuration spécifique

#### Étape 3 : Nommer votre bouteille

Donnez un nom descriptif à votre bouteille, par exemple :
- "Jeux Steam"
- "Adobe Photoshop"
- "Bureautique"

#### Étape 4 : Créer

Cliquez sur **Créer**. Bottles va :
- Télécharger le runner Wine approprié
- Configurer l'environnement
- Installer les dépendances de base

### Installer une application dans une bouteille

#### Méthode 1 : Depuis l'explorateur de fichiers

1. **Ouvrez votre bouteille** en cliquant dessus dans la liste
2. Cliquez sur **Exécuter un exécutable**
3. Parcourez et sélectionnez votre fichier .exe
4. Suivez l'assistant d'installation

#### Méthode 2 : Depuis les programmes

1. Dans votre bouteille, allez à l'onglet **Programmes**
2. Cliquez sur le bouton **+** en haut
3. Sélectionnez votre installateur
4. Une fois installé, le programme apparaît dans la liste

### Configurer une bouteille

Chaque bouteille dispose de nombreuses options de configuration accessibles via les onglets :

#### Onglet Détails

- **Informations générales** : nom, type, architecture (32/64 bits)
- **Chemin** : emplacement de la bouteille sur le disque
- **Runner** : version de Wine utilisée (vous pouvez la changer)

#### Onglet Options

**Environnement système**
- **Version de Windows** : Windows 10, 7, XP, etc.
- **Bureau virtuel** : activer un bureau Windows dédié
- **Résolution** : définir la résolution si bureau virtuel activé

**Performances**
- **DXVK** : traduction DirectX vers Vulkan (pour les jeux)
- **VKD3D** : support DirectX 12
- **Renderisation** : options graphiques avancées

**Compatibilité**
- **Composants** : installer DirectX, .NET, Visual C++, etc.
- **DLL Overrides** : remplacer des bibliothèques Windows

#### Onglet Dépendances

Bottles peut installer automatiquement des composants courants :

- **Polices** : corefonts (Arial, Times, etc.)
- **Runtime** : vcredist (Visual C++), dotnet (.NET Framework)
- **Frameworks** : mono, gecko
- **Outils** : steam, uplay, origin

Pour installer une dépendance :
1. Cliquez sur **Dépendances**
2. Parcourez la liste ou recherchez
3. Cliquez sur **Installer** à côté de celle souhaitée

### Lancer une application

Une fois votre programme installé :

1. Ouvrez la bouteille concernée
2. Allez dans l'onglet **Programmes**
3. Cliquez sur l'application souhaitée
4. Elle se lance !

Vous pouvez également :
- **Créer un raccourci** sur le bureau
- **Épingler à la barre des tâches**
- **Ajouter au menu des applications**

### Gérer plusieurs bouteilles

L'un des grands avantages de Bottles est la facilité de gérer plusieurs environnements :

- **Bouteille Jeux** : pour tous vos jeux
- **Bouteille Office** : pour les logiciels bureautiques
- **Bouteille Photo** : pour les logiciels de retouche photo
- **Bouteille spécifique** : pour un logiciel problématique nécessitant une configuration particulière

Chaque bouteille est **complètement isolée** des autres, évitant les conflits.

### Sauvegarder et restaurer une bouteille

#### Créer une sauvegarde

1. Sélectionnez votre bouteille
2. Cliquez sur le menu **⋮** (trois points) en haut à droite
3. Choisissez **Exporter** ou **Créer un instantané**
4. Sélectionnez l'emplacement de sauvegarde

#### Restaurer une sauvegarde

1. Sur la page d'accueil de Bottles
2. Cliquez sur **Importer** (icône ⬇)
3. Sélectionnez votre fichier de sauvegarde (.tar, .yml)
4. La bouteille est restaurée avec toutes ses applications

### Désinstaller une bouteille

⚠️ **Attention** : cela supprimera la bouteille ET toutes les applications qu'elle contient !

1. Sélectionnez la bouteille
2. Cliquez sur le menu **⋮** (trois points)
3. Choisissez **Supprimer**
4. Confirmez la suppression

---

## PlayOnLinux vs Bottles : Lequel choisir ?

### Choisissez PlayOnLinux si :

- ✅ Vous voulez installer un logiciel très populaire avec un script automatique
- ✅ Vous préférez une interface simple et classique
- ✅ Vous trouvez facilement des tutoriels pour votre logiciel spécifique
- ✅ Votre matériel est ancien ou limité en ressources

### Choisissez Bottles si :

- ✅ Vous débutez avec Wine et voulez une interface moderne
- ✅ Vous souhaitez la meilleure gestion des environnements
- ✅ Vous voulez les dernières versions de Wine
- ✅ Vous appréciez les mises à jour régulières
- ✅ Vous installez plusieurs applications Windows
- ✅ Vous voulez facilement sauvegarder et restaurer vos configurations

### Tableau comparatif

| Critère | PlayOnLinux | Bottles |
|---------|-------------|---------|
| Interface | Classique, fonctionnelle | Moderne, élégante |
| Scripts automatiques | ✅ Nombreux | ⚠️ Moins nombreux |
| Facilité d'utilisation | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Développement actif | ⚠️ Ralenti | ✅ Très actif |
| Gestion multi-environnements | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Documentation | ✅ Abondante | ✅ Bonne et croissante |
| Performances | ⭐⭐⭐ | ⭐⭐⭐⭐ |

> **💡 Recommandation générale** : Pour les nouveaux utilisateurs en 2024/2025, **Bottles** est généralement le meilleur choix. PlayOnLinux reste pertinent pour des cas spécifiques nécessitant des scripts existants.

---

## Utilisation combinée

Bonne nouvelle : vous n'avez pas à choisir ! Vous pouvez installer les deux :

- **PlayOnLinux** pour profiter de ses scripts automatiques spécifiques
- **Bottles** pour votre gestion quotidienne et les nouvelles installations

Les deux outils sont **totalement indépendants** et n'interfèrent pas l'un avec l'autre.

---

## Conseils pratiques pour réussir

### 1. Commencez simple

- Testez d'abord avec une application gratuite et légère
- Ne vous lancez pas directement avec un gros logiciel professionnel

### 2. Un environnement par application importante

Pour les logiciels critiques (Adobe, CAO, etc.) :
- Créez une bouteille/lecteur virtuel dédié
- Ne mélangez pas avec d'autres applications
- Cela facilite le dépannage en cas de problème

### 3. Notez vos configurations

Quand vous trouvez une configuration qui fonctionne :
- Notez la version de Wine utilisée
- Notez les dépendances installées
- Notez les paramètres modifiés
- Cela vous servira si vous devez réinstaller

### 4. Sauvegardez régulièrement

Avec Bottles, prenez l'habitude de créer des instantanés :
- Avant une mise à jour importante
- Après une installation réussie
- Avant de modifier des paramètres

### 5. Consultez les bases de données

Avant d'installer un logiciel :
- Vérifiez sur [WineHQ AppDB](https://appdb.winehq.org/)
- Cherchez des tutoriels spécifiques à ce logiciel
- Lisez les retours d'expérience d'autres utilisateurs

### 6. Patience et persévérance

Tous les logiciels ne fonctionnent pas du premier coup :
- Essayez différentes versions de Wine
- Testez différents paramètres
- Installez les dépendances une par une
- N'hésitez pas à demander de l'aide sur les forums

---

## Dépannage des problèmes courants

### L'application ne s'affiche pas correctement

**Avec Bottles** :
1. Ouvrez la bouteille
2. Allez dans **Options**
3. Activez **Bureau virtuel**
4. Définissez une résolution (ex: 1920x1080)

**Avec PlayOnLinux** :
1. Sélectionnez l'application
2. **Configurer** → Onglet **Affichage**
3. Cochez **Émulation de bureau virtuel**

### Pas de son dans l'application

**Vérifiez le pilote audio** :
- Dans Bottles : Options → Audio → vérifier PulseAudio/PipeWire
- Dans PlayOnLinux : Configurer → Wine → Configure Wine → Audio

### L'application est très lente

**Solutions à essayer** :

1. **Désactiver les effets visuels** dans l'application Windows
2. **Activer DXVK** (Bottles : Options → Performance → DXVK ON)
3. **Fermer les autres applications** pour libérer des ressources
4. **Essayer une version de Wine différente**

### Erreur "DLL manquante"

1. Identifiez la DLL mentionnée dans l'erreur
2. Dans Bottles : Dépendances → recherchez et installez le composant nécessaire
3. Dans PlayOnLinux : Configurer → Installer des composants → cherchez la bibliothèque

### Impossible de télécharger Wine/composants

- Vérifiez votre **connexion Internet**
- Désactivez temporairement votre **pare-feu/VPN**
- Essayez plus tard (serveurs parfois surchargés)
- Utilisez un **miroir différent** dans les paramètres

---

## Alternatives et compléments

### Lutris

Un autre gestionnaire similaire, plus orienté gaming. Excellent pour :
- Les jeux Windows via Wine
- Les émulateurs
- Les clients de jeux (Epic, GOG, etc.)

### Heroic Games Launcher

Spécialisé dans :
- Epic Games Store
- GOG (Good Old Games)
- Amazon Games

Plus de détails dans les sections suivantes du tutoriel.

### Proton (via Steam)

Si vous jouez via Steam, Proton est intégré :
- Automatique et transparent
- Très performant pour les jeux
- Aucune configuration nécessaire

---

## Conclusion

PlayOnLinux et Bottles transforment l'expérience d'utilisation de Wine en la rendant accessible à tous. Que vous soyez un utilisateur débutant ou confirmé, ces outils vous permettent d'exécuter vos applications Windows préférées sans les complications de la ligne de commande.

**Points clés à retenir** :

- ✅ **PlayOnLinux** : solution éprouvée avec de nombreux scripts automatiques
- ✅ **Bottles** : solution moderne, intuitive et activement développée
- ✅ **Isolation** : les deux permettent de créer des environnements séparés
- ✅ **Sauvegarde** : pensez à sauvegarder vos configurations qui marchent
- ✅ **Compatibilité** : vérifiez toujours WineHQ avant d'installer

N'oubliez pas : même si ces outils simplifient grandement les choses, tous les logiciels Windows ne fonctionneront pas parfaitement. Privilégiez quand c'est possible les **alternatives natives Linux** pour une expérience optimale.

---


⏭️ [Logiciels compatibles et base de données WineHQ](/15-applications-windows-sous-linux/03-logiciels-compatibles-et-base-de-donnees-winehq.md)
