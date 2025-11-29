🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 15.3 Logiciels compatibles et base de données WineHQ

## Introduction

Avant d'installer une application Windows sous Linux avec Wine, il est essentiel de vérifier sa compatibilité. C'est ici qu'intervient **WineHQ AppDB** (Application Database), une ressource inestimable qui recense les expériences de milliers d'utilisateurs avec des dizaines de milliers d'applications Windows.

Dans cette section, vous apprendrez à :
- Utiliser efficacement la base de données WineHQ
- Comprendre les niveaux de compatibilité
- Identifier les logiciels qui fonctionnent bien sous Wine
- Interpréter les retours d'expérience des autres utilisateurs
- Maximiser vos chances de succès

> **💡 Règle d'or** : Ne jamais installer un logiciel Windows avec Wine sans avoir d'abord consulté WineHQ AppDB. Cela vous fera gagner un temps précieux !

---

## Qu'est-ce que WineHQ AppDB ?

### Présentation

**WineHQ AppDB** est une base de données collaborative où les utilisateurs partagent leurs expériences d'installation et d'utilisation d'applications Windows sous Wine.

**Site web** : [https://appdb.winehq.org/](https://appdb.winehq.org/)

### Ce que vous y trouverez

Pour chaque application référencée :

- ✅ **Niveau de compatibilité** (Platinum, Gold, Silver, Bronze, Garbage)
- ✅ **Rapports de tests** détaillés par version du logiciel
- ✅ **Instructions d'installation** spécifiques
- ✅ **Version de Wine recommandée**
- ✅ **Dépendances nécessaires** (DLL, bibliothèques)
- ✅ **Problèmes connus** et solutions
- ✅ **Captures d'écran** de l'application fonctionnant sous Wine
- ✅ **Notes et astuces** de la communauté

### Qui contribue ?

N'importe quel utilisateur peut soumettre un rapport de test après avoir testé une application. C'est une base collaborative mondiale avec des milliers de contributeurs.

---

## Les niveaux de compatibilité expliqués

WineHQ utilise un système de notation par médailles pour évaluer la compatibilité :

### 🏆 Platinum (Platine)

**Définition** : L'application fonctionne **parfaitement** sans aucune configuration.

**Caractéristiques** :
- Installation simple et directe
- Toutes les fonctionnalités opérationnelles
- Aucun bug visible
- Aucune manipulation particulière nécessaire
- Performances comparables à Windows

**Exemples typiques** :
- Notepad++ (éditeur de texte)
- 7-Zip (archiveur)
- Paint.NET (anciennes versions)
- Certains jeux légers

**Ce que cela signifie pour vous** : Installation en toute confiance !

### 🥇 Gold (Or)

**Définition** : L'application fonctionne **presque parfaitement** avec quelques ajustements mineurs.

**Caractéristiques** :
- Installation nécessite quelques étapes supplémentaires simples
- Quelques fonctionnalités mineures peuvent ne pas marcher
- Besoin d'installer certaines dépendances (polices, DLL)
- Les bugs éventuels n'impactent pas l'utilisation normale

**Exemples typiques** :
- Microsoft Office (versions anciennes avec quelques réglages)
- Adobe Photoshop CS6 (avec winetricks)
- Certains jeux Steam
- Logiciels professionnels courants

**Ce que cela signifie pour vous** : Fonctionne bien, mais lisez les instructions !

### 🥈 Silver (Argent)

**Définition** : L'application fonctionne avec des **bugs mineurs** ou des fonctionnalités manquantes.

**Caractéristiques** :
- Installation peut être complexe
- Certaines fonctionnalités ne marchent pas
- Bugs occasionnels mais contournables
- Nécessite des ajustements de configuration
- Peut nécessiter des versions spécifiques de Wine

**Exemples typiques** :
- Logiciels avec fonctions réseau partielles
- Applications avec impression limitée
- Jeux avec problèmes graphiques mineurs
- Logiciels avec certains plugins incompatibles

**Ce que cela signifie pour vous** : Utilisable, mais attendez-vous à des compromis.

### 🥉 Bronze

**Définition** : L'application démarre mais a des **problèmes majeurs**.

**Caractéristiques** :
- Installation très compliquée
- Nombreux bugs
- Fonctionnalités importantes manquantes
- Utilisation limitée
- Peut planter régulièrement
- Configuration avancée nécessaire

**Exemples typiques** :
- Logiciels récents utilisant des technologies non supportées
- Applications avec DRM complexe
- Jeux avec anti-cheat
- Logiciels nécessitant des pilotes matériels spécifiques

**Ce que cela signifie pour vous** : Utilisable uniquement pour des besoins basiques, frustrant.

### 🗑️ Garbage (Inutilisable)

**Définition** : L'application **ne fonctionne pas du tout**.

**Caractéristiques** :
- Ne démarre pas
- Plante immédiatement
- Aucune fonctionnalité utilisable
- Incompatibilité totale

**Exemples typiques** :
- Logiciels avec protection anti-copie avancée
- Applications nécessitant des pilotes kernel Windows
- Jeux avec anti-cheat kernel-level
- Logiciels très récents utilisant des API non supportées

**Ce que cela signifie pour vous** : Ne perdez pas votre temps, cherchez une alternative !

---

## Comment utiliser WineHQ AppDB

### Rechercher une application

#### Méthode 1 : Recherche simple

1. Allez sur [https://appdb.winehq.org/](https://appdb.winehq.org/)
2. Utilisez la **barre de recherche** en haut de la page
3. Tapez le nom de votre application (ex: "Photoshop")
4. Appuyez sur **Entrée**

#### Méthode 2 : Navigation par catégories

1. Cliquez sur **Browse Apps** dans le menu
2. Sélectionnez une catégorie :
   - Audio
   - Development (Développement)
   - Educational (Éducatif)
   - Games (Jeux)
   - Graphics (Graphisme)
   - Internet
   - Multimedia
   - Office
   - Utilities (Utilitaires)
   - Video
3. Parcourez la liste

#### Méthode 3 : Recherche avancée

1. Cliquez sur **Advanced Search**
2. Affinez par :
   - Catégorie
   - Note de compatibilité
   - Version de Wine
   - Système d'exploitation

### Lire une fiche application

Une fois que vous avez trouvé votre application, la page affiche :

#### En-tête de l'application

- **Nom et version** de l'application
- **Note de compatibilité globale** (médaille)
- **Mainteneur** (si quelqu'un suit activement cette application)
- **Nombre de tests** soumis

#### Onglet "Version History"

Liste toutes les versions de l'application testées avec leurs notes respectives.

**Exemple** : Adobe Photoshop
- Photoshop CS6 : Gold
- Photoshop CC 2020 : Silver
- Photoshop CC 2023 : Bronze

> **💡 Astuce** : Les versions plus anciennes fonctionnent souvent mieux !

#### Onglet "Test Results"

Les rapports de tests détaillés par les utilisateurs. Chaque rapport contient :

**Informations système** :
- Version de Wine utilisée
- Distribution Linux
- Configuration matérielle (GPU, RAM, etc.)
- Date du test

**Détails du test** :
- Procédure d'installation suivie
- Problèmes rencontrés
- Solutions appliquées
- Résultat final (quelle note attribuée)

**Commentaires** :
- Fonctionnalités testées
- Bugs observés
- Astuces et recommandations

#### Onglet "Screenshots"

Des captures d'écran de l'application fonctionnant sous Wine. Très utile pour voir à quoi s'attendre !

#### Onglet "Comments"

Discussion communautaire :
- Questions des utilisateurs
- Réponses et solutions
- Partage d'expériences
- Mises à jour de compatibilité

### Interpréter les résultats

#### Regardez plusieurs rapports de test

Ne vous fiez pas à un seul rapport ! Consultez-en plusieurs pour avoir une vision globale :

- Les résultats peuvent varier selon le matériel
- Les versions de Wine évoluent
- Certains tests sont anciens

#### Vérifiez la date des tests

Un test de 2018 peut être obsolète :
- Wine s'améliore constamment
- Les nouvelles versions de Wine peuvent mieux supporter l'application
- À l'inverse, les vieilles versions de Wine peuvent ne plus être disponibles

**Privilégiez** les tests récents (moins de 1-2 ans).

#### Notez la version de Wine recommandée

Si plusieurs rapports mentionnent qu'une version spécifique de Wine fonctionne mieux :
- Notez cette version
- Utilisez-la dans Bottles ou PlayOnLinux

**Exemple** : "Fonctionne parfaitement avec Wine 8.0, problèmes avec Wine 7.x"

#### Identifiez les dépendances communes

Si plusieurs rapports mentionnent les mêmes dépendances :
- Ce sont probablement des prérequis essentiels
- Installez-les via Winetricks ou dans votre gestionnaire (Bottles/PlayOnLinux)

**Exemple** : "Nécessite vcrun2019, dotnet48, et corefonts"

#### Lisez les problèmes connus

Les utilisateurs signalent souvent :
- Les fonctionnalités qui ne marchent pas
- Les bugs récurrents
- Les solutions de contournement

**Cela vous évite de perdre du temps** à chercher pourquoi quelque chose ne fonctionne pas !

---

## Logiciels compatibles par catégorie

Voici une sélection d'applications populaires avec leur niveau de compatibilité général :

### 📝 Bureautique

| Application | Compatibilité | Notes |
|-------------|---------------|-------|
| Microsoft Office 2007/2010 | 🥇 Gold | Versions anciennes bien supportées |
| Microsoft Office 2016/2019 | 🥈 Silver | Fonctionnel mais bugs mineurs |
| Microsoft Office 365 | 🥉 Bronze | Problèmes d'activation, fonctions online limitées |
| Adobe Reader (vieilles versions) | 🏆 Platinum | Parfait pour versions < X |
| Foxit Reader | 🥇 Gold | Bonne alternative PDF |

**Recommandation** : Privilégiez LibreOffice (natif Linux) pour la bureautique.

### 🎨 Graphisme et création

| Application | Compatibilité | Notes |
|-------------|---------------|-------|
| Adobe Photoshop CS6 | 🥇 Gold | Nécessite configuration, bien documenté |
| Adobe Photoshop CC | 🥈 Silver | Versions récentes plus problématiques |
| Paint.NET | 🏆 Platinum | Excellente alternative légère |
| CorelDRAW | 🥈 Silver | Dépend de la version |
| Inkscape (Windows) | 🏆 Platinum | Version native Linux disponible ! |
| Adobe Illustrator CS6 | 🥈 Silver | Fonctionnel avec ajustements |

**Recommandation** : GIMP, Krita, Inkscape (natifs Linux) sont d'excellentes alternatives.

### 🎮 Jeux

| Application | Compatibilité | Notes |
|-------------|---------------|-------|
| League of Legends | 🥉 Bronze | Anti-cheat problématique |
| World of Warcraft | 🥇 Gold | Excellent support historique |
| StarCraft II | 🥇 Gold | Fonctionne bien |
| Minecraft Java | 🏆 Platinum | Version Java native disponible ! |
| Among Us | 🥇 Gold | Bon support via Proton/Wine |
| Overwatch | 🗑️ Garbage | Anti-cheat incompatible |
| Valorant | 🗑️ Garbage | Anti-cheat kernel incompatible |

**Recommandation** : Utilisez Steam avec Proton pour les jeux, ou consultez ProtonDB.

### 🔧 Utilitaires

| Application | Compatibilité | Notes |
|-------------|---------------|-------|
| Notepad++ | 🏆 Platinum | Parfait |
| 7-Zip | 🏆 Platinum | Parfait |
| WinRAR | 🥇 Gold | Fonctionne bien |
| PuTTY | 🏆 Platinum | Alternative native disponible |
| FileZilla | 🏆 Platinum | Version Linux native existe ! |
| CCleaner | 🥇 Gold | BleachBit recommandé sur Linux |

### 🎵 Audio et Vidéo

| Application | Compatibilité | Notes |
|-------------|---------------|-------|
| Audacity | 🏆 Platinum | Version native Linux disponible ! |
| foobar2000 | 🥇 Gold | Bon lecteur audio |
| MusicBee | 🥈 Silver | Certaines fonctions limitées |
| VLC (Windows) | 🏆 Platinum | Version native Linux disponible ! |
| Spotify (Windows) | 🥇 Gold | Application native et web disponibles |

### 💻 Développement

| Application | Compatibilité | Notes |
|-------------|---------------|-------|
| Visual Studio Code | 🏆 Platinum | Version native Linux officielle ! |
| Notepad++ | 🏆 Platinum | Excellent éditeur |
| Git for Windows | 🏆 Platinum | Git natif Linux disponible |
| FileZilla | 🏆 Platinum | Version native disponible |
| PuTTY | 🥇 Gold | Alternative : Terminal natif + SSH |

### 🌐 Internet et Communication

| Application | Compatibilité | Notes |
|-------------|---------------|-------|
| Mozilla Firefox | 🏆 Platinum | Version native Linux disponible ! |
| Google Chrome | 🏆 Platinum | Version native Linux disponible ! |
| Discord | 🥇 Gold | Application native et web disponibles |
| Skype | 🥈 Silver | Application native disponible |
| Zoom | 🥇 Gold | Client Linux natif disponible |

---

## ProtonDB : La base de données pour les jeux Steam

### Qu'est-ce que ProtonDB ?

**ProtonDB** est l'équivalent de WineHQ AppDB mais spécialisé dans les jeux Steam fonctionnant avec Proton (version de Wine optimisée pour les jeux par Valve).

**Site web** : [https://www.protondb.com/](https://www.protondb.com/)

### Système de notation

Similaire à WineHQ mais adapté aux jeux :

- **🏆 Platinum** : Fonctionne parfaitement sans configuration
- **🥇 Gold** : Fonctionne parfaitement avec quelques réglages
- **🥈 Silver** : Fonctionne avec bugs mineurs
- **🥉 Bronze** : Fonctionne avec bugs majeurs
- **🗑️ Borked** : Ne fonctionne pas

### Comment l'utiliser

1. Recherchez votre jeu Steam
2. Consultez les rapports des joueurs Linux
3. Notez la version de Proton recommandée
4. Lisez les réglages suggérés (arguments de lancement, etc.)
5. Vérifiez les problèmes connus

### Avantage sur WineHQ pour les jeux

- **Plus spécialisé** pour les jeux
- **Mises à jour fréquentes** de la communauté gaming Linux
- **Instructions spécifiques** aux jeux Steam
- **Compatible** avec Steam Deck

> **💡 Pour les jeux** : Consultez d'abord ProtonDB, puis WineHQ si le jeu n'est pas sur Steam.

---

## Cas particuliers et limitations

### Logiciels avec DRM ou protection anti-copie

**Problème** : Les protections anti-copie avancées fonctionnent rarement sous Wine.

**Exemples** :
- Denuvo (protection anti-piratage)
- SafeDisc, SecuROM (anciennes protections CD)
- Applications nécessitant activation en ligne complexe

**Solution** : Cherchez des versions sans DRM ou des alternatives.

### Anti-cheat dans les jeux

**Problème** : Les anti-cheat kernel-level sont incompatibles avec Wine.

**Exemples incompatibles** :
- Vanguard (Valorant, League of Legends)
- Easy Anti-Cheat (certaines configurations)
- BattlEye (certains jeux)

**Certains anti-cheat fonctionnent** :
- Easy Anti-Cheat (version Proton supportée)
- BattlEye (support Proton partiel)

**Vérifiez** toujours ProtonDB pour les jeux online compétitifs.

### Applications nécessitant des pilotes matériels

**Problème** : Wine ne peut pas utiliser les pilotes Windows.

**Exemples** :
- Logiciels de scan professionnel
- Applications de CAO avec dongles USB propriétaires
- Logiciels audio avec interfaces spécifiques
- Applications de vidéosurveillance

**Alternative** : Machine virtuelle avec passthrough USB, ou dual-boot.

### Logiciels très récents

**Problème** : Wine a toujours un temps de retard sur les nouvelles API Windows.

**Exemple** : Windows 11 exclusive APIs, DirectX 12 récent, .NET 7/8

**Solution** : Attendez quelques mois/années, ou utilisez une machine virtuelle.

---

## Stratégies pour maximiser vos chances de succès

### 1. Privilégiez les versions anciennes

**Les logiciels de 5-10 ans fonctionnent souvent mieux** que les versions les plus récentes :

- APIs mieux supportées par Wine
- Moins de dépendances système complexes
- Plus de tests communautaires
- Documentation plus complète

**Exemple** : Adobe Photoshop CS6 (2012) fonctionne mieux que CC 2023.

### 2. Cherchez d'abord une alternative native

Avant d'installer avec Wine, vérifiez s'il existe :

- **Une version Linux native** du logiciel
- **Une alternative open-source** équivalente
- **Une application web** qui fait la même chose

**Avantages** :
- Meilleures performances
- Meilleure intégration système
- Pas de bugs Wine
- Support à long terme

### 3. Testez en mode live ou machine virtuelle d'abord

Pour les logiciels importants :

1. Testez d'abord dans une **machine virtuelle Linux**
2. Ou utilisez un **préfixe Wine dédié temporaire**
3. Validez que tout fonctionne
4. Ensuite installez "pour de vrai"

Cela évite de polluer votre système principal.

### 4. Créez un environnement dédié

Pour chaque application importante :
- **Une bouteille Bottles dédiée**
- Ou **un préfixe Wine séparé**
- Configuration isolée
- Facilité de sauvegarde et restauration

### 5. Documentez votre configuration

Quand vous réussissez une installation :

**Notez** :
- Version exacte du logiciel
- Version de Wine utilisée
- Dépendances installées (winetricks)
- Paramètres modifiés (winecfg)
- Problèmes rencontrés et solutions

**Pourquoi** : Vous gagnerez du temps si vous devez réinstaller !

### 6. Soyez patient et expérimentez

Wine n'est pas magique. Certaines applications demandent :
- Plusieurs tentatives
- Différentes versions de Wine
- Multiples configurations
- Installation de nombreuses dépendances

**N'abandonnez pas** au premier échec, mais sachez aussi **quand chercher une alternative**.

---

## Contribuer à WineHQ AppDB

### Pourquoi contribuer ?

En soumettant vos propres tests, vous :
- **Aidez la communauté** à savoir ce qui fonctionne
- **Améliorez la base de données** pour tous
- **Documentez vos configurations** pour vous-même
- **Partagez vos solutions** aux problèmes

### Comment soumettre un test

#### 1. Créer un compte (gratuit)

1. Allez sur [https://appdb.winehq.org/](https://appdb.winehq.org/)
2. Cliquez sur **Register** en haut à droite
3. Remplissez le formulaire
4. Validez votre email

#### 2. Soumettre un rapport de test

1. **Recherchez** l'application testée
2. Cliquez sur **Submit Test Data**
3. Remplissez le formulaire :

**Informations requises** :
- Version de l'application
- Version de Wine
- Distribution Linux utilisée
- Note de compatibilité (Platinum à Garbage)

**Détails à fournir** :
- Comment vous avez installé (procédure)
- Dépendances installées
- Problèmes rencontrés
- Solutions appliquées
- Fonctionnalités testées

4. **Soumettez** votre rapport

#### 3. Bonnes pratiques

**Soyez précis** :
- Versions exactes
- Commandes utilisées
- Messages d'erreur complets

**Soyez objectif** :
- Ne surévaluez pas la compatibilité
- Mentionnez tous les bugs, même mineurs

**Soyez utile** :
- Expliquez clairement la procédure
- Donnez des solutions aux problèmes
- Ajoutez des captures d'écran si pertinent

---

## Ressources complémentaires

### Sites web utiles

**WineHQ** : [https://www.winehq.org/](https://www.winehq.org/)
- Site officiel de Wine
- Documentation complète
- Téléchargements

**WineHQ AppDB** : [https://appdb.winehq.org/](https://appdb.winehq.org/)
- Base de données applications
- Rapports de tests

**ProtonDB** : [https://www.protondb.com/](https://www.protondb.com/)
- Spécialisé jeux Steam
- Compatibilité Proton

**Lutris.net** : [https://lutris.net/](https://lutris.net/)
- Scripts d'installation jeux
- Gestionnaire multi-plateformes

### Forums et communautés

**WineHQ Forums** : [https://forum.winehq.org/](https://forum.winehq.org/)
- Support officiel Wine
- Entraide communautaire

**Reddit r/linux_gaming** : [https://www.reddit.com/r/linux_gaming/](https://www.reddit.com/r/linux_gaming/)
- Communauté gaming Linux
- Actualités et astuces

**Linux Mint Forums** : [https://forums.linuxmint.com/](https://forums.linuxmint.com/)
- Support spécifique Mint
- Section Wine/Gaming

### Chaînes YouTube

**GamingOnLinux** : Actualités et tests de jeux
**The Linux Experiment** : Tutoriels et découvertes
**Chris Titus Tech** : Configurations et optimisations

---

## Conclusion

La base de données WineHQ AppDB est votre meilleur allié pour réussir l'installation d'applications Windows sous Linux. En consultant systématiquement cette ressource avant toute installation, vous :

- ✅ **Gagnez du temps** en évitant les logiciels incompatibles
- ✅ **Suivez les bonnes pratiques** documentées par la communauté
- ✅ **Anticipez les problèmes** et leurs solutions
- ✅ **Choisissez la bonne version** de Wine
- ✅ **Identifiez les dépendances** nécessaires

**Points clés à retenir** :

- 🔍 **Toujours vérifier WineHQ/ProtonDB** avant installation
- 📊 **Comprendre les notes** de compatibilité
- 📅 **Privilégier les rapports récents** et multiples
- 📝 **Noter les configurations** qui fonctionnent
- 🤝 **Contribuer** en partageant vos expériences

N'oubliez pas : même si Wine permet d'exécuter de nombreuses applications Windows, **les alternatives natives Linux offrent souvent une meilleure expérience**. Wine est un excellent outil de transition ou pour les cas où aucune alternative n'existe.

---


⏭️ [Limites et alternatives natives](/15-applications-windows-sous-linux/04-limites-et-alternatives-natives.md)
