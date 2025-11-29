🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 14.2 Lutris (gestionnaire multi-plateforme)

## Introduction

Lutris est un gestionnaire de jeux libre et open-source pour Linux qui centralise tous vos jeux, quelle que soit leur origine. Contrairement à Steam qui est limité à sa propre plateforme, Lutris vous permet de gérer des jeux provenant de multiples sources dans une seule interface élégante.

**Lutris, c'est :**
- Un lanceur universel pour tous vos jeux
- Un gestionnaire de bibliothèque unifié
- Un système d'installation automatisé avec des scripts communautaires
- Un outil compatible avec de nombreuses plateformes (GOG, Epic Games, Battle.net, Origin, etc.)
- Une solution pour les jeux Windows, DOS, console et plus encore

## Pourquoi utiliser Lutris ?

### Avantages principaux

- **Centralisation** : Tous vos jeux au même endroit, peu importe leur origine
- **Scripts d'installation** : La communauté crée des scripts qui installent automatiquement les jeux avec la bonne configuration
- **Multi-plateformes** : Gérez Steam, GOG, Epic Games, Battle.net, Origin, Ubisoft Connect, etc.
- **Flexibilité** : Supporte Wine, Proton, DOSBox, ScummVM, RetroArch et bien d'autres
- **Interface unifiée** : Une bibliothèque cohérente pour tous vos jeux
- **Personnalisation avancée** : Contrôle total sur chaque configuration de jeu

### Différence avec Steam

| Steam | Lutris |
|-------|--------|
| Une seule plateforme (Steam) | Multiples plateformes |
| Proton intégré uniquement | Wine, Proton, émulateurs, etc. |
| Installation automatique | Scripts communautaires + installation manuelle possible |
| Orienté jeux récents | Jeux modernes ET rétro |
| Propriétaire | Open-source |

> **Note** : Lutris et Steam sont complémentaires ! Vous pouvez utiliser les deux simultanément.

## Installation de Lutris

### Méthode 1 : Via le Gestionnaire de logiciels

1. Ouvrez le **Menu** → **Gestionnaire de logiciels**
2. Recherchez **"Lutris"**
3. Cliquez sur l'application **Lutris**
4. Cliquez sur **Installer**
5. Entrez votre mot de passe si demandé

### Méthode 2 : Via le terminal (version la plus récente)

Pour obtenir la dernière version de Lutris, utilisez le PPA officiel :

```bash
# Ajout du dépôt officiel Lutris
sudo add-apt-repository ppa:lutris-team/lutris

# Mise à jour de la liste des paquets
sudo apt update

# Installation de Lutris
sudo apt install lutris
```

### Premier lancement

1. Lancez Lutris depuis le **Menu** → **Jeux** → **Lutris**
2. Lutris s'ouvre avec une bibliothèque vide (c'est normal)
3. L'interface se compose de :
   - **Barre latérale gauche** : Sources et plateformes
   - **Zone centrale** : Votre bibliothèque de jeux
   - **Barre supérieure** : Recherche et options

## Comprendre l'interface de Lutris

### Vue d'ensemble

L'interface Lutris est organisée en plusieurs sections :

**Barre latérale (Sources)** :
- **Tous** : Affiche tous vos jeux
- **Lutris** : Jeux installés via les scripts Lutris
- **Steam** : Vos jeux Steam (si connecté)
- **GOG** : Vos jeux GOG (si connecté)
- **Epic Games Store** : Jeux Epic (si connecté)
- **Origin** : Jeux EA/Origin (si connecté)
- **Ubisoft Connect** : Jeux Ubisoft (si connecté)
- **Runners** : Outils d'exécution installés

**Menu principal** :
- ☰ (Hamburger) : Préférences et paramètres
- 🔍 : Recherche dans votre bibliothèque
- ➕ : Ajouter un jeu manuellement

### Modes d'affichage

Vous pouvez basculer entre :
- **Vue en grille** : Affichage par vignettes avec images
- **Vue en liste** : Affichage détaillé en liste

Clic droit sur un espace vide → **Affichage** pour changer.

## Les Runners : Le cœur de Lutris

### Qu'est-ce qu'un Runner ?

Un "runner" est un programme qui permet d'exécuter un jeu. Lutris supporte de nombreux runners :

**Pour les jeux Windows** :
- **Wine** : Couche de compatibilité Windows
- **Proton** : Version Valve de Wine (de Steam)
- **Wine-GE** : Version communautaire avec améliorations

**Pour les jeux rétro** :
- **DOSBox** : Jeux MS-DOS
- **ScummVM** : Jeux d'aventure classiques (Monkey Island, etc.)
- **RetroArch** : Émulateurs multiples

**Pour les jeux Linux natifs** :
- **Linux** : Exécutables Linux natifs

**Navigateurs web** :
- **Web** : Pour les jeux navigateur

### Installer des Runners

1. Cliquez sur **☰** (menu hamburger) → **Gérer les runners**
2. Vous verrez la liste de tous les runners disponibles
3. Pour installer un runner, cliquez sur **⬇** (flèche vers le bas) à côté de son nom
4. Choisissez la version à installer (généralement la plus récente)
5. Lutris télécharge et installe automatiquement le runner

**Runners recommandés pour débuter** :
- **wine-ge-latest** : Pour la plupart des jeux Windows
- **Steam (Proton)** : Si vous voulez utiliser Proton hors de Steam
- **DOSBox** : Si vous aimez les classiques DOS

> **Astuce** : N'installez que les runners dont vous avez besoin. Vous pourrez toujours en ajouter plus tard.

## Installer un jeu avec un script Lutris

### Méthode la plus simple

Les scripts Lutris sont créés par la communauté et automatisent l'installation des jeux.

**Étapes** :

1. Rendez-vous sur **https://lutris.net**
2. Utilisez la barre de recherche pour trouver votre jeu
3. Cliquez sur le jeu dans les résultats
4. Cliquez sur le bouton **Install** correspondant à votre version du jeu
5. Votre navigateur demande l'autorisation d'ouvrir Lutris → **Acceptez**
6. Lutris s'ouvre avec une fenêtre d'installation
7. Suivez les étapes :
   - Le script télécharge les runners nécessaires
   - Vous devrez peut-être indiquer où se trouve le fichier d'installation du jeu
   - Lutris configure automatiquement le jeu
8. Une fois terminé, le jeu apparaît dans votre bibliothèque

### Exemple : Installer un jeu GOG

1. Téléchargez votre jeu depuis **GOG.com** (fichier .sh ou .exe)
2. Sur **lutris.net**, recherchez le nom du jeu
3. Cliquez sur **Install**
4. Lutris vous demande où se trouve le fichier téléchargé
5. Pointez vers le fichier .sh ou .exe téléchargé
6. Lutris installe automatiquement avec Wine
7. Votre jeu est prêt !

## Connecter vos comptes de plateformes

### Connexion automatique

Lutris peut se connecter à vos comptes de différentes plateformes :

**Pour Epic Games Store** :

1. Dans Lutris, clic sur **☰** → **Ajouter un jeu** → **Rechercher sur Lutris.net**
2. Recherchez **"Epic Games Store"**
3. Installez le script Epic Games Store
4. Lancez Epic Games Store depuis Lutris
5. Connectez-vous avec vos identifiants Epic
6. Vos jeux Epic apparaîtront dans la section "Epic Games Store" de Lutris

**Pour GOG** :

1. Même procédure avec **"GOG Galaxy"** ou utilisez les scripts individuels

**Pour Battle.net (Blizzard)** :

1. Recherchez et installez **"Battle.net"** depuis lutris.net
2. Connectez-vous avec votre compte Blizzard
3. Téléchargez vos jeux depuis l'interface Battle.net
4. Ils apparaîtront dans Lutris

> **Important** : Certains launchers (Epic, Battle.net) s'exécutent via Wine. Le premier lancement peut être lent.

## Ajouter un jeu manuellement

Si aucun script n'existe pour votre jeu, vous pouvez l'ajouter manuellement.

### Pour un jeu Windows

1. Cliquez sur **➕** (ou **☰** → **Ajouter un jeu**)
2. Sélectionnez **Ajouter un jeu manuellement**
3. Remplissez les informations :
   - **Nom** : Nom du jeu
   - **Runner** : Sélectionnez **Wine** (ou wine-ge)
   - **Exécutable du jeu** : Cliquez sur **Parcourir** et sélectionnez le .exe du jeu
4. Onglet **Options du jeu** :
   - **Préfixe Wine** : Lutris crée automatiquement un dossier pour le jeu
   - Vous pouvez personnaliser le dossier si souhaité
5. Cliquez sur **Enregistrer**
6. Le jeu apparaît dans votre bibliothèque

### Pour un jeu Linux natif

1. Cliquez sur **➕**
2. **Ajouter un jeu manuellement**
3. **Runner** : Sélectionnez **Linux**
4. **Exécutable** : Pointez vers le binaire du jeu
5. **Enregistrer**

### Pour un jeu DOS

1. Cliquez sur **➕**
2. **Runner** : Sélectionnez **DOSBox**
3. **Exécutable principal** : Sélectionnez le .exe ou .bat du jeu DOS
4. **Répertoire de travail** : Dossier contenant le jeu
5. **Enregistrer**

## Configuration et options avancées

### Options globales

**☰** → **Préférences** → **Runners** :

Vous pouvez configurer les paramètres par défaut de chaque runner :
- Version de Wine à utiliser par défaut
- Paramètres graphiques (DXVK, VKD3D)
- Options de performance

### Options par jeu

Clic droit sur un jeu → **Configurer** :

**Onglet Options du jeu** :
- Modifier l'exécutable
- Changer le répertoire de travail
- Arguments de lancement

**Onglet Options du runner** :
- Version spécifique de Wine pour ce jeu
- Activer/désactiver DXVK (DirectX vers Vulkan)
- Activer/désactiver Esync/Fsync
- DLL overrides (pour certains jeux spécifiques)

**Onglet Configuration système** :
- Résolution
- Variables d'environnement
- Préfixe de commande (pour GameMode, MangoHud, etc.)

> **Conseil débutant** : Si un jeu ne fonctionne pas, cherchez sur lutris.net si quelqu'un a partagé une configuration qui fonctionne.

## DXVK et VKD3D : Améliorer les performances

### Qu'est-ce que DXVK ?

DXVK traduit les appels DirectX 9/10/11 en Vulkan, ce qui améliore généralement les performances des jeux Windows sous Linux.

### Activer DXVK

1. Clic droit sur le jeu → **Configurer**
2. Onglet **Options du runner**
3. Cochez **Activer DXVK**
4. **Enregistrer**

### VKD3D pour DirectX 12

VKD3D traduit DirectX 12 en Vulkan :

1. Même procédure que DXVK
2. Cochez **Activer VKD3D**

> **Note** : DXVK est généralement activé par défaut sur les runners Wine récents.

## Winetricks : Installer des composants Windows

### Qu'est-ce que Winetricks ?

Winetricks est un script qui simplifie l'installation de bibliothèques Windows nécessaires à certains jeux (DirectX, .NET Framework, Visual C++, etc.).

### Utiliser Winetricks

1. Clic droit sur le jeu → **Winetricks**
2. Une fenêtre s'ouvre avec différentes catégories :
   - **Installer un paquet Windows DLL ou un composant**
   - **Installer une police**
   - **Modifier les paramètres**
3. Sélectionnez ce dont vous avez besoin (ex: **d3dx9** pour DirectX 9)
4. Cliquez sur **OK**
5. Winetricks installe automatiquement le composant dans le préfixe Wine du jeu

**Composants fréquemment nécessaires** :
- **dotnet40** ou **dotnet48** : .NET Framework
- **vcrun2019** : Visual C++ Redistributable
- **d3dx9**, **d3dx11** : DirectX
- **xact** : Audio pour certains jeux

## Gestion des préfixes Wine

### Qu'est-ce qu'un préfixe Wine ?

Un préfixe Wine est comme une installation Windows virtuelle pour chaque jeu. Cela permet d'isoler les jeux et leurs dépendances.

**Emplacement par défaut** : `~/Games/`

Chaque jeu a son propre dossier avec :
- **drive_c** : Équivalent du disque C: Windows
- **Program Files** : Où le jeu est installé
- **users** : Dossiers utilisateur Windows

### Accéder au préfixe

Clic droit sur le jeu → **Ouvrir le répertoire de préfixe**

Vous pouvez :
- Ajouter des fichiers manuellement
- Modifier des fichiers de configuration
- Installer des mods

### Ouvrir l'explorateur Wine

Clic droit sur le jeu → **Ouvrir l'explorateur de fichiers Wine**

Cela ouvre un explorateur Windows émulé où vous pouvez naviguer comme sous Windows.

## Optimisation et performances

### GameMode

GameMode optimise les performances système pendant le jeu :

1. Installez GameMode :
   ```bash
   sudo apt install gamemode
   ```

2. Dans Lutris, clic droit sur le jeu → **Configurer**
3. **Configuration système** → **Options système avancées**
4. Cochez **Activer Feral GameMode**
5. **Enregistrer**

### MangoHud (overlay de performances)

Pour afficher les FPS et l'utilisation des ressources en jeu :

1. Installez MangoHud :
   ```bash
   sudo apt install mangohud
   ```

2. Clic droit sur le jeu → **Configurer**
3. **Configuration système** → **Préfixe de commande**
4. Ajoutez : `mangohud`
5. **Enregistrer**

Lancez le jeu et appuyez sur **Shift+F12** pour afficher/masquer l'overlay.

### Activer Fsync/Esync

Ces technologies améliorent la synchronisation pour de meilleures performances :

1. Clic droit sur le jeu → **Configurer**
2. **Options du runner**
3. Cochez **Activer Fsync** (ou **Esync** si Fsync n'est pas disponible)
4. **Enregistrer**

> **Note** : Fsync nécessite un kernel récent (5.16+), déjà présent sur Linux Mint moderne.

## Problèmes courants et solutions

### Le jeu ne se lance pas

**Solutions** :
1. Vérifiez que le runner Wine est installé
2. Essayez une version différente de Wine (wine-ge souvent recommandé)
3. Consultez lutris.net pour voir si d'autres utilisateurs ont le même jeu
4. Vérifiez les logs : clic droit → **Afficher les logs**

### Erreur de dépendances manquantes

**Solutions** :
1. Clic droit → **Winetricks**
2. Installez les composants demandés (vcrun, dotnet, etc.)
3. Consultez les scripts Lutris.net pour voir quelles dépendances sont nécessaires

### Performance médiocre

**Solutions** :
1. Activez DXVK (si pas déjà fait)
2. Activez GameMode
3. Vérifiez que vos pilotes graphiques propriétaires sont installés
4. Essayez wine-ge-latest
5. Activez Fsync

### Écran noir ou crash

**Solutions** :
1. Essayez en mode fenêtré d'abord
2. Essayez de désactiver DXVK temporairement
3. Essayez une version différente de Wine
4. Consultez les logs pour identifier l'erreur

### Problèmes de son

**Solutions** :
1. Assurez-vous que PipeWire est actif (voir chapitre 12.6)
2. Essayez d'installer **xact** via Winetricks
3. Dans Options du runner, vérifiez les paramètres audio

### Le launcher (Epic, Battle.net) ne se connecte pas

**Solutions** :
1. Désactivez le pare-feu temporairement pour tester
2. Vérifiez votre connexion Internet
3. Essayez de réinstaller le launcher avec le script Lutris.net le plus récent
4. Certains launchers nécessitent des composants spécifiques (vérifiez les scripts)

## Importer vos jeux Steam dans Lutris

Vous pouvez voir et lancer vos jeux Steam depuis Lutris :

### Configuration

1. Dans Lutris, **☰** → **Préférences** → **Sources**
2. Activez **Steam**
3. Lutris détecte automatiquement votre bibliothèque Steam
4. Vos jeux Steam apparaissent dans la section **Steam** de Lutris

> **Note** : Lancer un jeu Steam depuis Lutris ouvrira quand même Steam. C'est principalement utile pour centraliser visuellement votre bibliothèque.

## Personnaliser l'apparence

### Ajouter des images de jeux

Lutris télécharge automatiquement des images depuis sa base de données, mais vous pouvez personnaliser :

1. Clic droit sur le jeu → **Configurer**
2. **Informations sur le jeu** → **Bannière** / **Icône** / **Couverture**
3. Cliquez sur **Parcourir** pour sélectionner votre image
4. **Enregistrer**

### Thèmes Lutris

1. **☰** → **Préférences** → **Apparence**
2. Choisissez entre **Clair** et **Sombre**
3. Ajustez la taille des vignettes selon vos préférences

## Sauvegardes et synchronisation cloud

### Où sont les sauvegardes ?

Les sauvegardes de jeux Windows sont généralement dans :
- `~/Games/[nom-du-jeu]/drive_c/users/[votre-nom]/Documents/`
- `~/Games/[nom-du-jeu]/drive_c/users/[votre-nom]/AppData/Local/`

### Synchroniser avec un cloud

Vous pouvez utiliser :
- **Syncthing** (voir chapitre 10.5)
- **rclone** pour Google Drive, OneDrive, etc.
- Lien symbolique vers un dossier cloud

Exemple avec un dossier cloud :
```bash
# Déplacez les sauvegardes vers le cloud
mv ~/Games/mon-jeu/save ~/Nextcloud/game-saves/mon-jeu

# Créez un lien symbolique
ln -s ~/Nextcloud/game-saves/mon-jeu ~/Games/mon-jeu/save
```

## Lutris vs Heroic Games Launcher

### Comparaison rapide

| Lutris | Heroic |
|--------|--------|
| Multi-sources (GOG, Epic, etc.) | Epic Games + GOG uniquement |
| Scripts communautaires | Installation directe |
| Configuration avancée | Interface simplifiée |
| Tous types de jeux (Windows, DOS, etc.) | Jeux modernes principalement |
| Courbe d'apprentissage moyenne | Très facile pour débutants |

### Quand utiliser quoi ?

**Utilisez Lutris pour** :
- Gérer plusieurs plateformes
- Jeux GOG, Battle.net, Origin
- Jeux rétro (DOS, ScummVM)
- Configuration avancée nécessaire

**Utilisez Heroic pour** :
- Simplicité avec Epic Games Store
- Installation rapide sans configuration
- Si vous préférez une interface plus simple

> **Astuce** : Vous pouvez utiliser les deux ! Heroic pour Epic/GOG, Lutris pour le reste.

## Communauté et ressources

### Sites utiles

- **Lutris.net** : Scripts d'installation et documentation
- **WineHQ** : Base de données de compatibilité Wine
- **ProtonDB** : Même pour les jeux hors Steam (Wine est similaire)
- **r/linux_gaming** : Subreddit très actif

### Contribuer

Si vous réussissez à faire fonctionner un jeu :
1. Créez un compte sur Lutris.net
2. Soumettez votre script d'installation
3. Aidez la communauté !

### Forums et aide

- **Forums Lutris** : https://forums.lutris.net/
- **Discord Lutris** : Communauté très réactive
- **Forums Linux Mint** : Section Gaming

## Conseils pour une utilisation optimale

1. **Toujours chercher un script d'abord** : Quelqu'un a probablement déjà configuré votre jeu
2. **Lisez les commentaires** : Sur lutris.net, les utilisateurs signalent souvent des problèmes ou tweaks
3. **Testez différents runners** : wine-ge fonctionne mieux pour certains jeux, Proton pour d'autres
4. **Patience avec les launchers** : Epic Games Store et Battle.net peuvent être lents au premier lancement
5. **Documentez vos succès** : Notez quelle configuration fonctionne pour vos jeux
6. **Mettez à jour régulièrement** : Les runners sont constamment améliorés
7. **Backup vos préfixes** : Avant de modifier des configurations critiques
8. **Utilisez GameMode systématiquement** : Amélioration gratuite des performances

## Exemples de jeux populaires sur Lutris

### Jeux qui fonctionnent excellemment

**Battle.net** :
- World of Warcraft (toutes extensions)
- Overwatch 2 (vérifiez l'anti-cheat)
- Diablo II Resurrected
- Hearthstone

**Epic Games Store** :
- Fortnite (vérifiez le statut anti-cheat)
- Rocket League (vérifié fonctionnel)
- Satisfactory
- Hades

**GOG** :
- The Witcher 3
- Cyberpunk 2077
- Baldur's Gate 3
- Divinity: Original Sin 2

**Classiques DOS** :
- Doom (toutes versions)
- Commander Keen
- Duke Nukem 3D
- Warcraft II

## Désinstaller proprement

### Supprimer un jeu

1. Clic droit sur le jeu → **Supprimer**
2. Choisissez si vous voulez :
   - **Supprimer de la bibliothèque** : Le retire de Lutris mais garde les fichiers
   - **Supprimer les fichiers** : Supprime complètement le jeu

### Supprimer un runner inutilisé

1. **☰** → **Gérer les runners**
2. Cliquez sur **🗑️** à côté du runner à supprimer

### Nettoyer les préfixes Wine orphelins

```bash
# Vérifier l'espace utilisé
du -sh ~/Games/*

# Supprimer manuellement les dossiers de jeux désinstallés
rm -rf ~/Games/nom-du-jeu-desinstalle
```

## Conclusion

Lutris est un outil extraordinairement puissant pour les joueurs Linux. Sa flexibilité permet de gérer pratiquement n'importe quel jeu, de n'importe quelle époque, sur n'importe quelle plateforme.

**Points clés à retenir** :
- ✅ Utilisez les scripts lutris.net autant que possible
- ✅ wine-ge-latest est un excellent choix par défaut
- ✅ DXVK et GameMode améliorent significativement les performances
- ✅ La communauté est votre meilleure ressource
- ✅ N'hésitez pas à expérimenter avec différentes configurations

Avec Lutris, vous avez accès à des dizaines de milliers de jeux, des classiques DOS aux derniers AAA. Bienvenue dans le monde du gaming multi-plateforme sous Linux ! 🎮🐧

---


⏭️ [Heroic Games Launcher (Epic Games, GOG)](/14-gaming-sous-linux/03-heroic-games-launcher.md)
