🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 14.3 Heroic Games Launcher (Epic Games, GOG)

## Introduction

Heroic Games Launcher est un lanceur de jeux libre et open-source spécialement conçu pour gérer vos bibliothèques Epic Games Store et GOG sous Linux. Contrairement aux solutions plus complexes, Heroic privilégie la simplicité et l'efficacité avec une interface moderne et intuitive.

**Heroic, c'est :**
- Un client natif Linux pour Epic Games Store et GOG
- Une interface élégante et facile à utiliser
- Une installation en un clic pour vos jeux
- Support de Proton et Wine intégré
- Compatible avec les sauvegardes cloud
- 100% gratuit et open-source

## Pourquoi utiliser Heroic ?

### Avantages principaux

- **Simplicité** : Interface claire et moderne, idéale pour les débutants
- **Intégration native** : Conçu spécifiquement pour Linux (pas d'émulation de Windows)
- **Deux plateformes** : Epic Games Store + GOG dans une seule application
- **Sauvegardes cloud** : Synchronisation automatique avec Epic Cloud Saves
- **Mises à jour automatiques** : Jeux et lanceur toujours à jour
- **Performances optimales** : Utilise Wine-GE et Proton-GE par défaut
- **Aucune configuration complexe** : Tout fonctionne out-of-the-box

### Epic Games Store vs Heroic

| Client Epic officiel | Heroic |
|---------------------|---------|
| Pas disponible sur Linux | Natif Linux |
| Nécessite Lutris ou Wine manuel | Application autonome |
| Performances variables | Optimisé pour Linux |
| Interface Windows émulée | Interface native moderne |

### GOG Galaxy vs Heroic

| GOG Galaxy | Heroic |
|------------|---------|
| Pas disponible sur Linux | Natif Linux |
| Nécessite Wine/Lutris | Application native |
| Interface complète (réseau social) | Interface axée sur les jeux |
| Plus lourd | Léger et rapide |

## Installation de Heroic Games Launcher

### Méthode 1 : Via Flatpak (recommandée)

Flatpak garantit que vous aurez toujours la dernière version :

```bash
# Installation de Heroic via Flatpak
flatpak install flathub com.heroicgameslauncher.hgl
```

**Lancement** :
```bash
flatpak run com.heroicgameslauncher.hgl
```

Ou cherchez **"Heroic Games Launcher"** dans votre menu Applications.

### Méthode 2 : Via AppImage

1. Rendez-vous sur https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/releases
2. Téléchargez le fichier **Heroic-X.X.X.AppImage** (version la plus récente)
3. Ouvrez un terminal dans le dossier de téléchargement
4. Rendez le fichier exécutable :
   ```bash
   chmod +x Heroic-*.AppImage
   ```
5. Double-cliquez sur le fichier ou exécutez :
   ```bash
   ./Heroic-*.AppImage
   ```

### Méthode 3 : Via le gestionnaire de logiciels

1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez **"Heroic Games Launcher"**
3. Installez la version Flatpak proposée

> **Recommandation** : La version Flatpak est la plus simple à maintenir à jour.

## Premier lancement et configuration initiale

### Interface de bienvenue

Au premier lancement, Heroic affiche un écran de bienvenue :

1. **Choix de la langue** : Sélectionnez **Français** (ou votre langue préférée)
2. **Thème** : Choisissez entre thème **Clair** ou **Sombre**
3. **Installation des outils** : Heroic propose d'installer Wine-GE
   - Cliquez sur **Installer** pour télécharger Wine-GE automatiquement
   - C'est la version recommandée pour la meilleure compatibilité

### Installation de Wine/Proton

Heroic télécharge et gère automatiquement :
- **Wine-GE** : Version communautaire optimisée de Wine
- **Proton-GE** : Version Valve avec améliorations

**Emplacement** : `~/.var/app/com.heroicgameslauncher.hgl/` (si Flatpak)

> **Note** : Vous n'avez rien à faire manuellement. Heroic gère tout automatiquement lors de l'installation du premier jeu.

## Connexion à Epic Games Store

### Créer ou se connecter à votre compte Epic

1. Dans Heroic, cliquez sur l'onglet **Epic Games** dans la barre latérale
2. Cliquez sur **Se connecter**
3. Une page web s'ouvre dans votre navigateur
4. Connectez-vous avec vos identifiants Epic Games (ou créez un compte)
5. Autorisez Heroic à accéder à votre compte
6. Retournez dans Heroic

Votre bibliothèque Epic Games apparaît automatiquement !

### Récupérer vos jeux gratuits

Epic Games offre des jeux gratuits chaque semaine :

1. Visitez https://www.epicgames.com/store sur votre navigateur
2. Connectez-vous avec votre compte
3. Ajoutez les jeux gratuits à votre bibliothèque
4. Retournez dans Heroic et rafraîchissez
5. Les jeux apparaissent dans votre bibliothèque

> **Astuce** : Profitez des jeux gratuits hebdomadaires ! Même si vous ne les installez pas immédiatement, ils restent dans votre bibliothèque.

## Connexion à GOG

### Créer ou se connecter à votre compte GOG

1. Dans Heroic, cliquez sur l'onglet **GOG** dans la barre latérale
2. Cliquez sur **Se connecter**
3. Une fenêtre de connexion s'ouvre
4. Entrez vos identifiants GOG.com
5. Autorisez l'accès

Votre bibliothèque GOG est maintenant accessible !

### Importer vos jeux GOG

Tous les jeux que vous possédez sur GOG.com apparaissent automatiquement dans Heroic.

**Acheter des jeux GOG** :
1. Visitez https://www.gog.com
2. Achetez vos jeux (souvent DRM-free et Linux-friendly)
3. Ils apparaissent automatiquement dans Heroic

## Interface et navigation

### Barre latérale

**Sections principales** :
- **🏠 Accueil** : Vue d'ensemble et jeux récents
- **📚 Bibliothèque** : Tous vos jeux (Epic + GOG combinés)
- **🛒 Epic Games** : Uniquement vos jeux Epic
- **🎮 GOG** : Uniquement vos jeux GOG
- **⬇️ Téléchargements** : Gestion des téléchargements en cours
- **⚙️ Paramètres** : Configuration globale

### Barre supérieure

- **🔍 Recherche** : Trouvez rapidement un jeu dans votre bibliothèque
- **⟳ Rafraîchir** : Actualise la bibliothèque
- **⋮ Menu** : Options supplémentaires

### Cartes de jeux

Chaque jeu affiche :
- **Image de couverture** : Visuel du jeu
- **Titre** : Nom du jeu
- **Statut** : Installé, Non installé, Mise à jour disponible
- **Boutons** : Installer, Jouer, Mise à jour, etc.

## Installer un jeu

### Installation simple

1. Trouvez votre jeu dans la **Bibliothèque**
2. Cliquez sur le jeu pour ouvrir sa page détaillée
3. Cliquez sur **Installer**
4. Une fenêtre de configuration s'ouvre :
   - **Dossier d'installation** : Où installer le jeu (par défaut recommandé)
   - **Version de Wine/Proton** : Généralement **Wine-GE Latest** (automatique)
   - **Préfixe Wine** : Dossier de configuration Windows virtuel (automatique)
5. Cliquez sur **Installer**
6. Le téléchargement commence

### Options d'installation avancées

Dans la fenêtre d'installation, vous pouvez ajuster :

**Emplacement** :
- Changez le dossier si vous voulez installer sur un autre disque
- Par défaut : `~/Games/Heroic/`

**Version de Wine** :
- **Wine-GE** : Recommandé pour la plupart des jeux
- **Proton-GE** : Alternative pour certains jeux
- **Système** : Wine installé sur votre système (déconseillé pour débutants)

**Paramètres du jeu** :
- **Activer DXVK** : Traduction DirectX → Vulkan (recommandé : OUI)
- **Activer VKD3D** : Pour DirectX 12 (activé si nécessaire)
- **Activer Fsync** : Améliore les performances (recommandé : OUI)

> **Conseil débutant** : Laissez les paramètres par défaut. Heroic choisit automatiquement la meilleure configuration.

## Lancer un jeu

### Lancement simple

1. Cliquez sur le jeu dans votre bibliothèque
2. Cliquez sur **Jouer**
3. Le jeu se lance !

**Premier lancement** :
- Peut prendre plus de temps (compilation de shaders)
- Une fenêtre de progression peut s'afficher
- Les lancements suivants seront plus rapides

### Lancement rapide depuis l'accueil

Les jeux récemment joués apparaissent sur la page **Accueil** pour un accès rapide.

## Gestion des téléchargements

### Téléchargements en cours

1. Cliquez sur **⬇️ Téléchargements** dans la barre latérale
2. Vous verrez :
   - **Progression** de chaque téléchargement
   - **Vitesse** de téléchargement
   - **Temps restant estimé**

### Mettre en pause / Reprendre

- Cliquez sur **⏸ Pause** pour suspendre un téléchargement
- Cliquez sur **▶ Reprendre** pour continuer
- Cliquez sur **✖ Annuler** pour arrêter complètement

### Téléchargements simultanés

Par défaut, Heroic télécharge un jeu à la fois. Pour changer :

1. **Paramètres** → **Avancé**
2. **Téléchargements simultanés** : Ajustez le nombre
3. **Enregistrer**

> **Attention** : Télécharger plusieurs jeux en même temps peut ralentir la vitesse globale.

## Mises à jour des jeux

### Mise à jour automatique

Heroic vérifie automatiquement les mises à jour au démarrage.

**Quand une mise à jour est disponible** :
- Un badge apparaît sur l'icône du jeu
- Le bouton change en **Mettre à jour**
- Cliquez pour télécharger la mise à jour

### Mise à jour manuelle

1. Page du jeu → **⋮** (menu trois points)
2. **Rechercher des mises à jour**
3. Si disponible, cliquez sur **Mettre à jour**

### Désactiver les mises à jour automatiques

Pour un jeu spécifique :
1. Page du jeu → **Paramètres** (icône engrenage)
2. **Désactiver les mises à jour automatiques**
3. **Enregistrer**

## Configuration par jeu

### Accéder aux paramètres d'un jeu

1. Cliquez sur le jeu
2. Cliquez sur l'icône **⚙** (engrenage) en haut à droite
3. Plusieurs onglets s'ouvrent

### Onglet Général

**Informations** :
- Taille du jeu
- Dossier d'installation
- Dernière session de jeu

**Actions rapides** :
- **Ouvrir le dossier du jeu** : Accès direct aux fichiers
- **Ouvrir le préfixe Wine** : Pour ajouter des mods ou fichiers
- **Réparer le jeu** : Vérifie et répare les fichiers corrompus
- **Déplacer le jeu** : Vers un autre emplacement
- **Désinstaller** : Supprime le jeu

### Onglet Paramètres

**Version de Wine/Proton** :
- Changez si le jeu ne fonctionne pas correctement
- Testez différentes versions

**Paramètres de compatibilité** :
- **DXVK** : DirectX vers Vulkan
- **VKD3D** : DirectX 12 vers Vulkan
- **Fsync/Esync** : Optimisation de synchronisation
- **GameMode** : Optimisation système (si installé)

**Résolution et fenêtrage** :
- Mode plein écran / fenêtré
- Résolution personnalisée

**Arguments de lancement** :
- Options avancées pour certains jeux (basé sur ProtonDB)

### Onglet Sauvegardes cloud

Pour Epic Games Store :
- **Activer la synchronisation cloud** : OUI/NON
- **Télécharger les sauvegardes** : Récupère depuis le cloud
- **Envoyer les sauvegardes** : Upload vers le cloud

> **Important** : GOG ne supporte pas nativement les sauvegardes cloud dans Heroic (utilisez Syncthing ou solutions tierces).

## Paramètres globaux de Heroic

### Paramètres → Général

**Langue et thème** :
- Changez la langue de l'interface
- Basculez entre thème clair/sombre
- Mode compact ou normal

**Démarrage** :
- Lancer Heroic au démarrage du système
- Démarrer minimisé

**Bibliothèque** :
- Affichage en grille ou liste
- Taille des vignettes

### Paramètres → Jeux

**Dossier d'installation par défaut** :
- Changez où les jeux sont installés par défaut
- Exemple : `/mnt/games/` si vous avez un disque dédié

**Version Wine par défaut** :
- Choisissez Wine-GE ou Proton-GE
- S'applique à tous les nouveaux jeux

**Paramètres par défaut** :
- DXVK activé/désactivé
- Fsync activé/désactivé
- GameMode activé/désactivé

### Paramètres → Avancé

**Téléchargements** :
- Nombre de téléchargements simultanés
- Limite de bande passante

**Wine** :
- Versions de Wine installées
- Télécharger de nouvelles versions
- Supprimer les versions inutilisées

**Outils** :
- Winetricks
- Configuration Wine

**Logs** :
- Activer les logs détaillés (pour debugging)
- Ouvrir le dossier de logs

## Optimisation des performances

### GameMode (recommandé)

GameMode optimise votre système pour le gaming.

**Installation** :
```bash
sudo apt install gamemode
```

**Activation dans Heroic** :
1. Paramètres du jeu → **Paramètres**
2. **Autres** → **Activer GameMode**
3. **Enregistrer**

### MangoHud (monitoring)

Affiche FPS, température, utilisation GPU/CPU en jeu.

**Installation** :
```bash
sudo apt install mangohud
```

**Activation** :
1. Paramètres du jeu → **Paramètres**
2. **Autres** → **Activer MangoHud**
3. **Enregistrer**

Lancez le jeu et appuyez sur **Shift+F12** pour afficher/masquer l'overlay.

### Fsync/Esync

Améliore les performances de synchronisation.

**Activation** :
1. Paramètres du jeu → **Paramètres**
2. **Activer Fsync** (ou Esync si Fsync indisponible)
3. **Enregistrer**

> **Note** : Fsync est généralement meilleur qu'Esync sur les systèmes récents.

### Limiter les FPS

Pour économiser la batterie ou réduire la chaleur :

1. Paramètres du jeu → **Paramètres**
2. **Limiter FPS** → Activé
3. Définissez la limite (ex: 60 FPS)
4. **Enregistrer**

## Winetricks : Installer des composants Windows

### Qu'est-ce que Winetricks ?

Un outil pour installer facilement des bibliothèques Windows (DirectX, .NET, Visual C++, etc.).

### Accéder à Winetricks

1. Page du jeu → **⚙** Paramètres
2. Onglet **Général** → **Ouvrir Winetricks**
3. Une fenêtre s'ouvre avec des options

### Installer des composants courants

**Sélectionnez dans Winetricks** :
- **d3dx9** : DirectX 9
- **dotnet48** : .NET Framework 4.8
- **vcrun2019** : Visual C++ 2019
- **xact** : Audio pour certains jeux

Cochez le composant → **OK** → Winetricks installe automatiquement.

> **Quand l'utiliser** : Si un jeu affiche des erreurs de DLL manquantes ou ne se lance pas.

## Sauvegardes cloud Epic Games

### Fonctionnement

Epic Cloud Saves synchronise automatiquement vos sauvegardes entre appareils.

**Jeux compatibles** :
- Tous les jeux Epic qui supportent Cloud Saves
- Indiqué sur la page du jeu (icône nuage ☁️)

### Activer la synchronisation

1. Paramètres du jeu → **Sauvegardes cloud**
2. **Activer la synchronisation cloud** : OUI
3. **Synchroniser automatiquement** : OUI
4. **Enregistrer**

### Résoudre les conflits

Si vous jouez sur plusieurs machines :

**Conflit détecté** → Heroic demande :
- **Télécharger du cloud** : Utilise la sauvegarde cloud (écrase locale)
- **Envoyer vers le cloud** : Utilise la sauvegarde locale (écrase cloud)
- **Choisir la plus récente** : Automatique (recommandé)

## Vérifier et réparer un jeu

### Vérification de l'intégrité

Si un jeu crash ou présente des bugs :

1. Page du jeu → **⚙** Paramètres
2. Onglet **Général** → **Réparer**
3. Heroic vérifie tous les fichiers
4. Les fichiers corrompus sont re-téléchargés

Cette opération peut prendre du temps selon la taille du jeu.

### Réinstallation complète

Si la réparation ne suffit pas :

1. **Désinstaller le jeu** (vos sauvegardes cloud sont préservées)
2. **Réinstaller** le jeu
3. Vos sauvegardes se synchronisent automatiquement

## Problèmes courants et solutions

### Le jeu ne se lance pas

**Solutions** :
1. Essayez une version différente de Wine (Wine-GE ou Proton-GE)
2. Vérifiez les logs : Paramètres → Avancé → Ouvrir les logs
3. Consultez ProtonDB pour des tweaks spécifiques
4. Vérifiez que vos pilotes graphiques sont à jour
5. Installez les dépendances manquantes via Winetricks

### Performances médiocres

**Solutions** :
1. Activez GameMode
2. Vérifiez que DXVK est activé
3. Activez Fsync
4. Réduisez les paramètres graphiques du jeu
5. Vérifiez que vous utilisez le GPU dédié (pas l'intégré)
6. Fermez les applications en arrière-plan

### Écran noir au lancement

**Solutions** :
1. Attendez 30-60 secondes (shader compilation)
2. Essayez **Alt+Tab** puis revenez au jeu
3. Essayez en mode fenêtré
4. Désactivez DXVK temporairement pour tester
5. Changez la version de Wine

### Problèmes de connexion Epic Games

**Solutions** :
1. Vérifiez votre connexion Internet
2. Déconnectez-vous et reconnectez-vous
3. Supprimez le cache : `~/.var/app/com.heroicgameslauncher.hgl/cache`
4. Réinstallez Heroic en dernier recours

### Synchronisation cloud bloquée

**Solutions** :
1. Paramètres du jeu → Sauvegardes cloud → **Forcer le téléchargement**
2. Vérifiez votre connexion Internet
3. Déconnectez et reconnectez votre compte Epic
4. Vérifiez l'état des serveurs Epic Games

### Téléchargement très lent

**Solutions** :
1. Changez de serveur Epic dans les paramètres (si disponible)
2. Désactivez le VPN si activé
3. Vérifiez que rien d'autre ne consomme la bande passante
4. Redémarrez Heroic
5. Mettez en pause et reprenez le téléchargement

### Jeu qui crash régulièrement

**Solutions** :
1. Vérifiez l'intégrité du jeu (Réparer)
2. Installez les dépendances via Winetricks (vcrun, dotnet)
3. Essayez Proton-GE au lieu de Wine-GE
4. Vérifiez les logs pour identifier l'erreur
5. Consultez ProtonDB pour ce jeu spécifique

## Gérer plusieurs comptes Epic/GOG

### Changer de compte

**Epic Games** :
1. Paramètres → **Epic Games**
2. **Se déconnecter**
3. Reconnectez-vous avec un autre compte

**GOG** :
1. Paramètres → **GOG**
2. **Se déconnecter**
3. Reconnectez-vous avec un autre compte

> **Note** : Vous ne pouvez avoir qu'un seul compte connecté à la fois par plateforme.

## Désinstaller un jeu

### Désinstallation simple

1. Page du jeu → **⚙** Paramètres
2. Onglet **Général** → **Désinstaller**
3. Confirmez

**Ce qui est supprimé** :
- ✅ Fichiers du jeu
- ✅ Préfixe Wine du jeu

**Ce qui est préservé** :
- ✅ Sauvegardes cloud (pour Epic)
- ❌ Sauvegardes locales (si pas synchronisées)

### Sauvegarder avant désinstallation

Si le jeu n'a pas de cloud saves :

1. Ouvrez le dossier du jeu
2. Localisez le dossier de sauvegardes (généralement dans `Documents` ou `AppData`)
3. Copiez-le ailleurs
4. Désinstallez
5. Replacez les sauvegardes après réinstallation

## Heroic vs Steam vs Lutris

### Comparaison rapide

| Fonctionnalité | Heroic | Steam | Lutris |
|----------------|--------|-------|--------|
| Epic Games | ✅ Excellent | ❌ Non | ✅ Via script |
| GOG | ✅ Excellent | ❌ Non | ✅ Via script |
| Steam | ❌ Non | ✅ Natif | ✅ Intégration |
| Facilité | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| Configuration | Simple | Automatique | Avancée |
| Jeux rétro | ❌ Non | ❌ Non | ✅ Oui |

### Quand utiliser Heroic ?

✅ **Utilisez Heroic pour** :
- Vos jeux Epic Games Store
- Vos jeux GOG
- Une interface simple et moderne
- Si vous débutez avec le gaming Linux

❌ **Ne pas utiliser Heroic pour** :
- Jeux Steam (utilisez Steam)
- Jeux très anciens/DOS (utilisez Lutris)
- Battle.net, Origin (utilisez Lutris)

### Complémentarité

**Configuration optimale** :
- **Steam** → Jeux Steam
- **Heroic** → Jeux Epic + GOG
- **Lutris** → Battle.net, Origin, jeux rétro, autres

> Vous pouvez (et devriez) utiliser les trois en parallèle !

## Jeux recommandés pour tester

### Jeux Epic gratuits populaires (fonctionnent bien)

**Régulièrement offerts** :
- **GTA V** (Platine sur ProtonDB)
- **Control** (Or/Platine)
- **Borderlands 3** (Or)
- **Metro Exodus** (Or/Platine)
- **Assassin's Creed Syndicate** (Or)
- **Cities: Skylines** (Platine)
- **Satisfactory** (Or/Platine)

**Toujours gratuits** :
- **Fortnite** (⚠️ Vérifiez le statut anti-cheat)
- **Rocket League** (Fonctionne généralement bien)

### Jeux GOG recommandés

**Excellents sur Linux** :
- **The Witcher 3** (Platine - natif Linux)
- **Stardew Valley** (Platine)
- **Hollow Knight** (Platine)
- **Cyberpunk 2077** (Or/Platine)
- **Divinity: Original Sin 2** (Platine)
- **Disco Elysium** (Platine)

## Personnalisation et thèmes

### Changer l'apparence

**Paramètres → Général** :
- **Thème** : Clair / Sombre
- **Couleur d'accentuation** : Personnalisez la couleur principale
- **Mode compact** : Interface plus dense

### Organiser votre bibliothèque

**Filtres et tri** :
- **Tous les jeux** / **Installés** / **Non installés**
- Trier par : Nom, Date d'installation, Dernière session
- Recherche rapide

**Favoris** :
- Clic droit sur un jeu → **Ajouter aux favoris**
- Filtre **Favoris** pour accès rapide

## Mettre à jour Heroic

### Version Flatpak

```bash
# Mise à jour de Heroic
flatpak update com.heroicgameslauncher.hgl
```

Ou via le **Gestionnaire de logiciels** → **Mises à jour**

### Version AppImage

1. Téléchargez la nouvelle version depuis GitHub
2. Remplacez l'ancien fichier .AppImage
3. Vos jeux et paramètres sont préservés (stockés séparément)

### Vérifier les mises à jour

Heroic affiche une notification quand une nouvelle version est disponible.

## Emplacement des fichiers

### Jeux (par défaut)

```
~/Games/Heroic/
├── [Nom du jeu 1]/
├── [Nom du jeu 2]/
└── ...
```

### Préfixes Wine

```
~/.var/app/com.heroicgameslauncher.hgl/config/heroic/Prefixes/
```

### Configuration Heroic

```
~/.var/app/com.heroicgameslauncher.hgl/config/heroic/
├── config.json           # Configuration globale
├── gog_store/           # Cache GOG
├── legendaryConfig/     # Configuration Epic
└── logs/               # Fichiers de logs
```

### Sauvegardes

Dépend du jeu, généralement :
```
~/.var/app/com.heroicgameslauncher.hgl/config/heroic/Prefixes/[jeu]/drive_c/users/[nom]/Documents/
```

## Commandes utiles (version Flatpak)

### Lancer Heroic en ligne de commande

```bash
# Lancement normal
flatpak run com.heroicgameslauncher.hgl

# Lancement avec logs verbeux
flatpak run com.heroicgameslauncher.hgl --verbose
```

### Réinitialiser Heroic

Si problèmes persistants :

```bash
# Sauvegarder la config d'abord
cp -r ~/.var/app/com.heroicgameslauncher.hgl/config/heroic ~/heroic-backup

# Supprimer la config
rm -rf ~/.var/app/com.heroicgameslauncher.hgl/config/heroic

# Redémarrer Heroic (configuration initiale)
flatpak run com.heroicgameslauncher.hgl
```

> **Attention** : Vos jeux restent installés mais vous devrez reconnecter vos comptes.

## Ressources et communauté

### Sites officiels

- **Site web** : https://heroicgameslauncher.com/
- **GitHub** : https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher
- **Documentation** : https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/wiki

### Communauté

- **Discord Heroic** : Communauté active et aide rapide
- **GitHub Issues** : Signaler des bugs
- **Reddit r/linux_gaming** : Discussions générales gaming Linux

### Compatibilité des jeux

- **ProtonDB** : https://www.protondb.com (même pour Epic/GOG)
- **Are We Anti-Cheat Yet** : https://areweanticheatyet.com
- **GOG Linux compatibility** : Forums GOG

## Conseils pour une utilisation optimale

1. **Récupérez les jeux gratuits Epic** : Ajoutez-les chaque semaine, jouez plus tard
2. **Activez GameMode systématiquement** : Amélioration gratuite des performances
3. **Privilégiez GOG pour DRM-free** : Meilleure philosophie open-source
4. **Synchronisez vos sauvegardes** : Activez Cloud Saves pour Epic
5. **Testez avant d'acheter** : Vérifiez ProtonDB pour la compatibilité
6. **Gardez Heroic à jour** : Nouvelles fonctionnalités et corrections régulières
7. **Soyez patient au premier lancement** : Compilation de shaders
8. **Consultez les logs en cas de problème** : Aide au diagnostic
9. **Rejoignez la communauté** : Discord Heroic pour de l'aide

## Conclusion

Heroic Games Launcher est la solution idéale pour les joueurs Linux qui veulent accéder à leurs bibliothèques Epic Games Store et GOG sans complications. Son interface moderne, sa facilité d'utilisation et son intégration native Linux en font un choix excellent pour les débutants comme pour les utilisateurs avancés.

**Points clés à retenir** :
- ✅ Installation en un clic pour vos jeux Epic et GOG
- ✅ Interface intuitive et moderne
- ✅ Wine-GE intégré pour les meilleures performances
- ✅ Sauvegardes cloud pour Epic Games
- ✅ Mises à jour automatiques
- ✅ 100% gratuit et open-source

Avec Heroic, Steam et Lutris, vous avez accès à pratiquement tous les jeux disponibles sous Linux. Profitez de votre bibliothèque Epic et GOG sans avoir besoin de Windows ! 🎮🐧

---


⏭️ [Émulateurs de consoles (RetroArch)](/14-gaming-sous-linux/04-emulateurs-de-consoles.md)
