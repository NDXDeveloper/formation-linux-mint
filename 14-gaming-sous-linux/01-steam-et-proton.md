🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 14.1 Steam et Proton

## Introduction

Steam est la plateforme de distribution numérique de jeux vidéo la plus populaire au monde, développée par Valve. Depuis plusieurs années, Valve investit massivement dans le gaming sous Linux, faisant de Steam l'un des meilleurs moyens de jouer à des jeux sur Linux Mint.

**Proton** est une technologie révolutionnaire développée par Valve qui permet de jouer à des jeux Windows sur Linux sans configuration complexe. Il s'agit d'une couche de compatibilité basée sur Wine, mais considérablement améliorée et optimisée pour le gaming.

## Pourquoi Steam est idéal pour Linux ?

- **Catalogue énorme** : Des milliers de jeux, dont beaucoup fonctionnent parfaitement sur Linux
- **Proton intégré** : Jouez à des jeux Windows en un clic
- **Mises à jour automatiques** : Les jeux et Proton sont toujours à jour
- **Steam Deck** : L'investissement de Valve dans Linux garantit un support continu
- **Performances excellentes** : Souvent comparables ou supérieures à Windows
- **Communauté active** : ProtonDB pour vérifier la compatibilité des jeux

## Installation de Steam sur Linux Mint

### Méthode 1 : Via le Gestionnaire de logiciels (recommandée)

1. Ouvrez le **Menu** → **Gestionnaire de logiciels**
2. Recherchez **"Steam"** dans la barre de recherche
3. Cliquez sur l'application **Steam** (icône bleue et blanche)
4. Cliquez sur **Installer**
5. Entrez votre mot de passe administrateur si demandé

### Méthode 2 : Via le terminal

```bash
sudo apt update  
sudo apt install steam  
```

### Premier lancement

Lors du premier démarrage de Steam :

1. Steam va télécharger des mises à jour (patience, c'est normal)
2. Connectez-vous avec votre compte Steam (ou créez-en un)
3. Steam va installer des bibliothèques supplémentaires
4. L'interface Steam s'ouvrira ensuite normalement

> **Note** : Si vous n'avez pas de compte Steam, vous pouvez en créer un gratuitement sur [store.steampowered.com](https://store.steampowered.com)

## Comprendre Proton

### Qu'est-ce que Proton ?

Proton est une "couche de compatibilité" qui traduit les appels système Windows en appels système Linux en temps réel. C'est comme un interprète qui permet aux jeux Windows de "parler" à votre système Linux.

### Versions de Proton

Steam propose plusieurs versions de Proton :

- **Proton Experimental** : La version de développement avec les dernières améliorations
- **Proton 9.x, 8.x, 7.x** : Versions stables numérotées
- **Proton GE (GloriousEggroll)** : Version communautaire avec des correctifs supplémentaires (installation séparée)

Chaque version a ses forces, et certains jeux fonctionnent mieux avec une version spécifique.

## Activer Proton dans Steam

Par défaut, Steam n'affiche que les jeux Linux natifs. Pour voir et jouer aux jeux Windows, vous devez activer Proton :

### Étapes d'activation

1. Ouvrez **Steam**
2. Cliquez sur **Steam** (menu en haut à gauche) → **Paramètres**
3. Dans le menu de gauche, sélectionnez **Compatibilité**
4. Cochez la case **"Activer Steam Play pour les titres pris en charge"**
5. Cochez également **"Activer Steam Play pour tous les autres titres"**
6. Dans le menu déroulant, sélectionnez la version de Proton (recommandé : **Proton Experimental**)
7. Cliquez sur **OK**
8. **Redémarrez Steam** pour appliquer les changements

> **Astuce** : Activez toujours les deux options pour avoir accès au catalogue complet de jeux Windows.

## Installer et lancer un jeu

### Installation d'un jeu

1. Accédez à votre **Bibliothèque Steam**
2. Trouvez le jeu que vous souhaitez installer
3. Cliquez sur **Installer**
4. Choisissez l'emplacement d'installation (laissez par défaut si vous débutez)
5. Attendez la fin du téléchargement

### Lancer un jeu

1. Dans votre bibliothèque, sélectionnez le jeu
2. Cliquez sur **Jouer**
3. La première fois, Proton va préparer le jeu (cela peut prendre quelques minutes)
4. Le jeu se lancera automatiquement

> **Note** : Le premier lancement est toujours plus long car Proton compile des "shaders" pour optimiser les performances.

## Forcer une version spécifique de Proton pour un jeu

Certains jeux fonctionnent mieux avec une version particulière de Proton :

1. **Clic droit** sur le jeu dans votre bibliothèque
2. Sélectionnez **Propriétés**
3. Onglet **Compatibilité**
4. Cochez **"Forcer l'utilisation d'un outil de compatibilité Steam Play spécifique"**
5. Choisissez la version de Proton dans le menu déroulant
6. Fermez et relancez le jeu

> **Conseil** : Si un jeu ne fonctionne pas bien, essayez différentes versions de Proton. Consultez ProtonDB pour savoir quelle version fonctionne le mieux.

## ProtonDB : Votre meilleur ami

### Qu'est-ce que ProtonDB ?

[ProtonDB](https://www.protondb.com) est une base de données communautaire où les joueurs Linux partagent leurs expériences avec chaque jeu sur Steam.

### Comment l'utiliser

1. Rendez-vous sur **www.protondb.com**
2. Recherchez le jeu qui vous intéresse
3. Consultez :
   - **La note globale** (Platine, Or, Argent, Bronze, Borked)
   - **Les rapports des utilisateurs** avec leurs configurations
   - **Les tweaks recommandés** (paramètres de lancement, versions de Proton)

### Échelle de notation

- **🏆 Platine** : Fonctionne parfaitement sans configuration
- **🥇 Or** : Fonctionne parfaitement après quelques réglages
- **🥈 Argent** : Fonctionne avec des problèmes mineurs
- **🥉 Bronze** : Fonctionne mais avec des problèmes notables
- **❌ Borked** : Ne fonctionne pas

## Options de lancement avancées

Parfois, ProtonDB recommande d'ajouter des "options de lancement" pour améliorer la compatibilité :

### Comment ajouter des options de lancement

1. **Clic droit** sur le jeu → **Propriétés**
2. Dans l'onglet **Général**, trouvez **"Options de lancement"**
3. Copiez-collez les options recommandées par ProtonDB
4. Exemples courants :
   ```
   PROTON_USE_WINED3D=1 %command%
   PROTON_NO_ESYNC=1 %command%
   DXVK_ASYNC=1 %command%
   ```

> **Important** : Ne modifiez ces options que si ProtonDB le recommande spécifiquement pour votre jeu.

## Proton GE (GloriousEggroll)

### Qu'est-ce que Proton GE ?

Proton GE est une version communautaire de Proton maintenue par GloriousEggroll. Elle inclut :
- Des correctifs non encore intégrés dans Proton officiel
- Support de certains codecs vidéo propriétaires
- Améliorations pour des jeux spécifiques

### Installation de Proton GE

**Méthode simple avec ProtonUp-Qt** :

1. Installez ProtonUp-Qt depuis le Gestionnaire de logiciels
2. Lancez ProtonUp-Qt
3. Cliquez sur **"Add version"**
4. Sélectionnez la dernière version de **Proton-GE**
5. Cliquez sur **Install**
6. Redémarrez Steam

Proton GE apparaîtra maintenant dans la liste des versions de Proton disponibles.

## Optimisation des performances

### Conseils généraux

1. **Pilotes graphiques à jour** :
   - Utilisez le **Gestionnaire de pilotes** pour installer les pilotes propriétaires NVIDIA ou AMD

2. **Activer Fsync** :
   - Déjà activé par défaut sur Linux Mint récent
   - Améliore les performances de synchronisation

3. **GameMode** :
   - Installez GameMode pour optimiser les performances système pendant le jeu
   ```bash
   sudo apt install gamemode
   ```

4. **MangoHud** :
   - Outil d'overlay pour monitorer les performances
   - Voir chapitre 14.7 pour plus de détails

### Paramètres Steam

Dans **Steam** → **Paramètres** → **Téléchargements** :
- Limitez la bande passante si vous jouez en ligne pendant les téléchargements
- Désactivez les téléchargements pendant que vous jouez

## Problèmes courants et solutions

### Le jeu ne se lance pas

**Solutions** :
1. Vérifiez ProtonDB pour les tweaks recommandés
2. Essayez une autre version de Proton
3. Essayez Proton GE
4. Vérifiez les fichiers du jeu : clic droit → Propriétés → Fichiers locaux → Vérifier l'intégrité

### Performances médiocres

**Solutions** :
1. Vérifiez que vos pilotes graphiques sont installés (NVIDIA/AMD propriétaires)
2. Activez GameMode
3. Réduisez les paramètres graphiques du jeu
4. Essayez Proton GE ou une version différente
5. Vérifiez que vous n'utilisez pas le GPU intégré au lieu du GPU dédié

### Crash au lancement

**Solutions** :
1. Consultez ProtonDB pour votre jeu spécifique
2. Ajoutez les options de lancement recommandées
3. Essayez `PROTON_USE_WINED3D=1 %command%` dans les options de lancement
4. Vérifiez les logs : `~/.steam/steam/logs/`

### Problèmes de son

**Solutions** :
1. Vérifiez que PipeWire est actif (voir chapitre 12.6)
2. Redémarrez Steam
3. Essayez `PULSE_LATENCY_MSEC=60 %command%` dans les options de lancement

### Écran noir au lancement

**Solutions** :
1. Attendez 30 secondes (certains jeux ont un long chargement initial)
2. Essayez `Alt+Tab` pour revenir au jeu
3. Essayez le mode fenêtré dans les paramètres du jeu
4. Ajoutez `PROTON_USE_WINED3D=1 %command%`

## Compatibilité avec les anti-cheats

### Situation actuelle

Certains jeux avec anti-cheat ne fonctionnent pas sur Linux, notamment :
- **EasyAntiCheat** : Support partiel (dépend du développeur)
- **BattlEye** : Support partiel (dépend du développeur)
- **Vanguard (Riot Games)** : Non compatible
- **Kernel-level anti-cheats** : Généralement non compatibles

### Vérifier avant d'acheter

1. Consultez ProtonDB avant d'acheter un jeu en ligne
2. Vérifiez les rapports récents (certains jeux ajoutent le support Linux après la sortie)
3. La plupart des jeux solo et multijoueur coopératif fonctionnent parfaitement

## Jeux recommandés pour débuter

### Jeux qui fonctionnent parfaitement (Platine/Or)

- **The Witcher 3**
- **Elden Ring**
- **Cyberpunk 2077**
- **GTA V**
- **Red Dead Redemption 2**
- **Dark Souls III**
- **Sekiro: Shadows Die Twice**
- **Stardew Valley**
- **Terraria**
- **Portal 2**

> Ces jeux sont excellents pour tester Proton et découvrir le gaming sous Linux !

## Gestion de l'espace disque

### Où sont stockés vos jeux ?

Par défaut : `~/.steam/steam/steamapps/common/`

### Ajouter un dossier de bibliothèque

Si vous manquez d'espace :

1. **Steam** → **Paramètres** → **Téléchargements**
2. **Dossiers Steam** → **Ajouter un dossier**
3. Choisissez un disque avec plus d'espace
4. Vous pourrez maintenant choisir où installer chaque jeu

### Déplacer un jeu déjà installé

1. Clic droit sur le jeu → **Propriétés**
2. **Fichiers installés** → **Déplacer le dossier d'installation**
3. Choisissez la nouvelle bibliothèque

## Captures d'écran et streaming

### Captures d'écran

- **Touche par défaut** : `F12`
- **Accéder aux captures** : Affichage → Captures d'écran
- **Dossier** : `~/.steam/steam/userdata/[votre_id]/760/remote/`

### Streaming Steam (Remote Play)

Vous pouvez jouer à vos jeux Steam sur d'autres appareils :
1. Activez Remote Play dans les paramètres Steam
2. Connectez-vous sur l'appareil cible avec le même compte
3. Lancez le jeu depuis l'appareil distant

## Conseils pour une expérience optimale

1. **Gardez Steam à jour** : Les mises à jour incluent souvent des améliorations Proton
2. **Consultez toujours ProtonDB** avant d'acheter un nouveau jeu
3. **Patience au premier lancement** : Le shader pre-caching prend du temps mais améliore ensuite les performances
4. **Rejoignez la communauté** : Forums Steam Linux, Reddit r/linux_gaming
5. **Signalez vos expériences** : Contribuez à ProtonDB pour aider les autres
6. **Testez différentes versions de Proton** : Ce qui ne fonctionne pas aujourd'hui peut fonctionner demain
7. **Sauvegardez vos configurations** : Notez les options de lancement qui fonctionnent pour vos jeux

## Ressources utiles

- **ProtonDB** : https://www.protondb.com
- **Page Steam Linux** : https://store.steampowered.com/linux
- **Proton GitHub** : https://github.com/ValveSoftware/Proton
- **Proton GE** : https://github.com/GloriousEggroll/proton-ge-custom
- **Reddit r/linux_gaming** : Communauté active et aidante
- **Are We Anti-Cheat Yet** : https://areweanticheatyet.com (compatibilité anti-cheat)

## Conclusion

Steam et Proton ont révolutionné le gaming sous Linux. Avec plus de 70% du catalogue Steam fonctionnel sur Linux, vous avez accès à des milliers de jeux sans avoir besoin de Windows.

La clé du succès :
- ✅ Pilotes graphiques propriétaires installés
- ✅ Proton activé dans les paramètres Steam
- ✅ Consultation de ProtonDB avant d'acheter
- ✅ Patience et expérimentation avec différentes versions de Proton

Le gaming sous Linux n'a jamais été aussi accessible. Bienvenue dans la communauté des joueurs Linux ! 🎮🐧

---

⏭️ [Lutris (gestionnaire multi-plateforme)](/14-gaming-sous-linux/02-lutris.md)
