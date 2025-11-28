🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.4 Les espaces de travail virtuels

## Introduction

Les **espaces de travail virtuels** (aussi appelés bureaux virtuels) sont l'une des fonctionnalités les plus pratiques et les plus méconnues de Linux. Imaginez que vous pouvez avoir plusieurs bureaux indépendants sur un seul écran, et basculer instantanément entre eux !

C'est comme avoir plusieurs moniteurs, mais virtuellement, sans avoir à acheter d'écrans supplémentaires. Cette fonctionnalité existe depuis longtemps sous Linux et est désormais adoptée par Windows 10/11 (Bureaux virtuels) et macOS (Mission Control).

Dans ce chapitre, nous allons découvrir comment utiliser efficacement les espaces de travail pour mieux organiser votre travail et gagner en productivité.

## Qu'est-ce qu'un espace de travail virtuel ?

### Le concept

Un espace de travail virtuel est un **bureau supplémentaire** où vous pouvez placer vos fenêtres et applications.

**Analogie simple :**
Imaginez votre bureau physique avec plusieurs plateaux que vous pouvez faire glisser :
- Sur le premier plateau : vos documents de travail
- Sur le deuxième : vos outils de communication (mail, messagerie)
- Sur le troisième : votre navigateur pour la navigation personnelle
- Sur le quatrième : vos applications multimédia

Au lieu d'avoir tout empilé sur un seul bureau, vous organisez par thématique et changez de plateau selon ce que vous faites !

### Exemple concret d'utilisation

**Sans espaces de travail :**
- Vous avez 10 fenêtres ouvertes sur un seul bureau
- Tout se chevauche, c'est le désordre
- Vous passez du temps à chercher la bonne fenêtre
- Alt + Tab liste toutes les fenêtres dans le désordre

**Avec espaces de travail :**
- **Espace 1 - Travail** : LibreOffice, PDF de référence, calculatrice
- **Espace 2 - Communication** : Thunderbird, messagerie, navigateur web professionnel
- **Espace 3 - Développement** : éditeur de code, terminal, navigateur pour tests
- **Espace 4 - Multimédia** : lecteur audio, gestionnaire de photos

Chaque espace est dédié à une activité. Plus de confusion, plus de recherche !

## Pourquoi utiliser les espaces de travail ?

### Avantages principaux

**1. Organisation et concentration**
- Séparez travail et loisirs
- Évitez les distractions
- Chaque espace = une tâche ou un projet

**2. Gestion efficace de l'écran**
- Particulièrement utile sur laptop (petit écran)
- Pas besoin de minimiser constamment
- Mieux que d'empiler les fenêtres

**3. Productivité accrue**
- Basculement rapide entre contextes
- Pas de temps perdu à chercher une fenêtre
- Workflow plus fluide

**4. Multitâche intelligent**
- Travaillez sur plusieurs projets simultanément
- Gardez chaque projet dans son propre espace
- Contexte mental préservé

**5. Alternative aux multiples écrans**
- Solution gratuite et immédiate
- Aucun matériel supplémentaire
- Parfait pour nomades et étudiants

### Cas d'usage typiques

**Étudiant :**
- Espace 1 : Cours et prise de notes
- Espace 2 : Recherches et navigateur
- Espace 3 : Communication (Discord, mail)
- Espace 4 : Pause (musique, vidéos)

**Développeur :**
- Espace 1 : IDE et code
- Espace 2 : Terminaux et compilation
- Espace 3 : Navigateur et documentation
- Espace 4 : Communication (Slack, mail)

**Créatif :**
- Espace 1 : Logiciel de création (GIMP, Kdenlive)
- Espace 2 : Ressources (images, fichiers)
- Espace 3 : Références et inspiration
- Espace 4 : Communication client

**Télétravailleur :**
- Espace 1 : Applications métier
- Espace 2 : Communication pro (Teams, Zoom)
- Espace 3 : Bureautique et documents
- Espace 4 : Personnel (à utiliser pendant les pauses)

## Les espaces de travail dans Cinnamon

### Configuration par défaut

Par défaut, Linux Mint Cinnamon propose **2 espaces de travail** :
- Espace 1 (gauche)
- Espace 2 (droite)

Les espaces sont disposés **horizontalement**, comme une ligne de bureaux.

### Aperçu des espaces (Expo)

**Accéder à la vue d'ensemble :**
- **Ctrl + Alt + ↑** (flèche haut)
- Ou déplacez la souris dans le **coin supérieur gauche** de l'écran
- Ou cliquez sur l'applet "Aperçu des espaces" dans le panneau (s'il est activé)

**Ce que vous voyez :**
- Tous vos espaces de travail affichés en miniature
- Les fenêtres présentes sur chaque espace
- L'espace actif est surligné
- Vous pouvez voir d'un coup d'œil où se trouve chaque application

**Interactions possibles :**
- **Cliquez sur un espace** : y basculer
- **Glissez une fenêtre** entre espaces : la déplacer
- **Cliquez sur une fenêtre** : activer cette fenêtre et cet espace
- **Appuyez sur Échap** : quitter la vue d'ensemble

**Astuce :** L'Expo est excellent pour réorganiser rapidement vos fenêtres entre espaces !

### Naviguer entre les espaces

Il existe plusieurs méthodes pour changer d'espace de travail.

#### Méthode 1 : Raccourcis clavier (le plus rapide)

**Navigation de base :**
- **Ctrl + Alt + →** : espace suivant (vers la droite)
- **Ctrl + Alt + ←** : espace précédent (vers la gauche)
- **Ctrl + Alt + ↓** : revenir à l'espace précédemment utilisé

**Aller à un espace précis :**
Si vous avez 4 espaces configurés :
- **Ctrl + Alt + 1** : aller à l'espace 1
- **Ctrl + Alt + 2** : aller à l'espace 2
- **Ctrl + Alt + 3** : aller à l'espace 3
- **Ctrl + Alt + 4** : aller à l'espace 4

**Déplacer une fenêtre en même temps :**
- **Ctrl + Maj + Alt + →** : déplacer la fenêtre active vers l'espace suivant
- **Ctrl + Maj + Alt + ←** : déplacer vers l'espace précédent

**Astuce :** Ces raccourcis deviennent très naturels après quelques jours d'utilisation !

#### Méthode 2 : Coin actif (hot corner)

**Par défaut :**
- Déplacez votre souris dans le **coin supérieur gauche**
- La vue d'ensemble (Expo) s'affiche
- Cliquez sur l'espace souhaité

**Avantages :**
- Visuel et intuitif
- Permet de voir toutes les fenêtres
- Pratique pour réorganiser

**Inconvénients :**
- Plus lent que les raccourcis clavier
- Nécessite la souris

#### Méthode 3 : Applet dans le panneau

Vous pouvez ajouter un applet "Sélecteur d'espace de travail" au panneau.

**Ajouter l'applet :**
1. Clic droit sur le panneau → Mode édition du panneau
2. Cliquez sur "Applets"
3. Cherchez "Sélecteur d'espace de travail"
4. Cliquez sur "+" pour l'ajouter
5. Positionnez-le où vous voulez

**Utilisation :**
- L'applet montre tous vos espaces en miniature
- L'espace actif est surligné
- Cliquez sur un espace pour y aller
- Pratique pour voir rapidement où vous êtes

#### Méthode 4 : Molette de la souris (si activé)

**Sur le bureau vide :**
- Molette vers le haut : espace suivant
- Molette vers le bas : espace précédent

**Configuration :**
- Paramètres système → Bureau
- Section "Espaces de travail"
- Activer "Faire défiler les espaces de travail avec la molette sur le bureau"

### Déplacer des fenêtres entre espaces

Il existe plusieurs façons de déplacer une fenêtre d'un espace à l'autre.

#### Méthode 1 : Raccourci clavier

**Déplacer avec la fenêtre :**
- **Ctrl + Maj + Alt + →** : fenêtre vers l'espace suivant (vous suivez)
- **Ctrl + Maj + Alt + ←** : fenêtre vers l'espace précédent (vous suivez)

**Déplacer sans suivre :**
Certaines configurations permettent de déplacer la fenêtre sans changer d'espace, mais ce n'est pas le comportement par défaut dans Cinnamon.

#### Méthode 2 : Via l'Expo

1. **Ctrl + Alt + ↑** pour ouvrir l'Expo
2. Glissez-déposez la fenêtre d'un espace à l'autre
3. Cliquez sur l'espace souhaité ou appuyez sur Échap

**Avantage :** Très visuel, permet de voir le résultat immédiatement.

#### Méthode 3 : Menu contextuel

1. Clic droit sur la **barre de titre** de la fenêtre
2. "Déplacer vers un autre espace de travail" →
3. Choisissez l'espace de destination

**Ou :**
1. Clic droit sur la fenêtre dans le **panneau** (liste des fenêtres)
2. "Déplacer vers l'espace de travail" →
3. Choisissez l'espace

#### Méthode 4 : Glisser vers le bord

**Sur certaines configurations :**
- Glissez la fenêtre vers le bord gauche ou droit de l'écran
- Maintenez jusqu'à ce que l'espace change
- Relâchez dans le nouvel espace

**Note :** Cette fonctionnalité peut nécessiter une configuration ou une extension.

### Fenêtres collantes (sticky)

Certaines fenêtres peuvent être **collantes** : elles apparaissent sur **tous** les espaces de travail.

**Rendre une fenêtre collante :**
1. Clic droit sur la barre de titre de la fenêtre
2. Cochez "Sur tous les espaces de travail"
3. La fenêtre reste visible quel que soit l'espace actif

**Annuler :**
- Même menu, décochez l'option

**Cas d'usage :**
- Lecteur de musique (contrôle depuis n'importe où)
- Application de prise de notes
- Moniteur système
- Calculatrice
- Messagerie instantanée

**Astuce :** Utilisez cette fonctionnalité avec parcimonie pour ne pas encombrer tous vos espaces !

## Configuration des espaces de travail

### Accéder aux paramètres

**Méthode 1 :**
- Paramètres système → Espaces de travail

**Méthode 2 :**
- Clic droit sur le bureau → Paramètres du bureau → Espaces de travail

### Options de configuration

#### Nombre d'espaces de travail

**Modifier le nombre :**
- Champ "Nombre d'espaces de travail"
- Vous pouvez avoir de 1 à 16 espaces
- Recommandation : **2 à 4 espaces** pour la plupart des utilisateurs

**Réflexion :**
- **2 espaces** : minimum utile (travail/perso ou projet A/projet B)
- **4 espaces** : bon équilibre pour la plupart (travail/comm/dev/perso)
- **6+ espaces** : pour workflows très complexes, mais peut devenir confus

#### Disposition des espaces

**Options disponibles :**

**Grille automatique (par défaut) :**
- Cinnamon organise les espaces en grille
- Par exemple, 4 espaces = grille 2×2

**Une seule rangée :**
- Tous les espaces sur une ligne horizontale
- Navigation : gauche ↔ droite uniquement
- Plus simple mentalement

**Une seule colonne :**
- Tous les espaces empilés verticalement
- Navigation : haut ↔ bas uniquement

**Grille personnalisée :**
- Définissez manuellement le nombre de rangées et colonnes
- Par exemple : 3 colonnes × 2 rangées = 6 espaces

**Recommandation débutant :** Commencez avec une seule rangée (horizontale), c'est le plus intuitif.

#### Navigation circulaire

**Option "Boucler la navigation" :**
- Activée : depuis le dernier espace, → revient au premier
- Désactivée : navigation bloquée aux extrémités

**Exemple avec 4 espaces en ligne :**
- **Avec boucle** : Espace 4 + → = Espace 1
- **Sans boucle** : Espace 4 + → = reste sur Espace 4

**Conseil :** Activez-la si vous utilisez principalement les raccourcis clavier.

#### Affichage dans le panneau

**Options pour l'applet Sélecteur :**
- Afficher uniquement les espaces contenant des fenêtres
- Toujours afficher tous les espaces
- Afficher les noms des espaces

#### Nommer les espaces

**Personnaliser les noms :**
1. Paramètres système → Espaces de travail
2. Section "Noms des espaces de travail"
3. Cliquez sur un espace pour le renommer

**Exemples :**
- Espace 1 → "Travail"
- Espace 2 → "Communication"
- Espace 3 → "Développement"
- Espace 4 → "Multimédia"

**Avantages :**
- Plus facile à identifier dans les menus
- Aide à maintenir l'organisation mentale
- Visible dans l'applet si configuré

#### Comportement des nouvelles fenêtres

**Où s'ouvrent les nouvelles fenêtres ?**

**Options possibles :**
- **Espace actif** : toutes les nouvelles fenêtres s'ouvrent où vous êtes
- **Espace d'origine** : chaque application a un "espace de prédilection"
- **Dernier espace utilisé** : l'application s'ouvre où elle était la dernière fois

**Configuration :**
- Dépend de l'application et des paramètres globaux
- Généralement : nouvelles fenêtres s'ouvrent sur l'espace actif

### Coins actifs et espaces de travail

**Personnaliser les coins :**
1. Paramètres système → Coins actifs
2. Configurez chaque coin :
   - **Coin supérieur gauche** : Expo (par défaut)
   - **Coin supérieur droit** : peut déclencher autre chose
   - **Coins inférieurs** : souvent désactivés

**Options intéressantes pour les espaces :**
- Expo / Vue d'ensemble
- Afficher toutes les fenêtres
- Afficher le bureau
- Basculer l'espace suivant/précédent

### Extensions et applets utiles

**Applets recommandés :**

**Workspace Switcher (Sélecteur d'espace) :**
- Affiche tous les espaces dans le panneau
- Clic pour changer d'espace
- Peut afficher les noms

**Workspace Name (Nom de l'espace) :**
- Affiche le nom de l'espace actif dans le panneau
- Discret et informatif

**Workspace Grid (Grille d'espaces) :**
- Vue en grille dans le panneau
- Plus visuel que le sélecteur simple

**Window Quick List :**
- Liste des fenêtres par espace
- Navigation rapide

## Raccourcis clavier - Récapitulatif complet

### Navigation entre espaces

**Basculement :**
- **Ctrl + Alt + →** : espace suivant
- **Ctrl + Alt + ←** : espace précédent
- **Ctrl + Alt + ↑** : vue d'ensemble (Expo)
- **Ctrl + Alt + ↓** : espace précédent (historique)

**Accès direct :**
- **Ctrl + Alt + 1** : espace 1
- **Ctrl + Alt + 2** : espace 2
- **Ctrl + Alt + 3** : espace 3
- **Ctrl + Alt + 4** : espace 4

### Déplacement de fenêtres

**Avec suivi :**
- **Ctrl + Maj + Alt + →** : déplacer fenêtre à droite (et suivre)
- **Ctrl + Maj + Alt + ←** : déplacer fenêtre à gauche (et suivre)

**Vers un espace précis :**
- **Ctrl + Maj + Alt + 1** : déplacer vers espace 1
- **Ctrl + Maj + Alt + 2** : déplacer vers espace 2
- Etc.

### Personnaliser les raccourcis

**Modifier les raccourcis :**
1. Paramètres système → Clavier → Raccourcis
2. Catégorie "Espaces de travail" ou "Fenêtres"
3. Cliquez sur le raccourci à modifier
4. Appuyez sur la nouvelle combinaison
5. Validez

**Recommandations :**
- Gardez les raccourcis par défaut au début
- Modifiez uniquement si conflit ou préférence forte
- Restez cohérent (même logique pour toutes les actions)

## Stratégies d'utilisation efficaces

### Méthode "GTD" (Getting Things Done)

Organisez par type d'activité :
- **Espace 1 - Faire** : tâches actuelles, travail actif
- **Espace 2 - Communiquer** : mails, messagerie, réseaux sociaux
- **Espace 3 - Référence** : documentation, recherches
- **Espace 4 - Repos** : pause, multimédia

### Méthode "Projets"

Un espace par projet :
- **Espace 1 - Projet A** : tout ce qui concerne le projet A
- **Espace 2 - Projet B** : tout pour le projet B
- **Espace 3 - Administration** : mails, gestion
- **Espace 4 - Personnel** : hors travail

### Méthode "Contextes"

Séparez vie pro et perso :
- **Espace 1-2 - Professionnel** : tout le travail sur 2 espaces
- **Espace 3-4 - Personnel** : loisirs, famille sur 2 espaces

### Méthode "Outils"

Par type d'outils :
- **Espace 1 - Bureautique** : LibreOffice, PDF, documents
- **Espace 2 - Internet** : navigateur, téléchargements
- **Espace 3 - Création** : GIMP, Kdenlive, outils créatifs
- **Espace 4 - Système** : terminal, gestionnaires, configuration

### Conseils généraux

**1. Restez cohérent**
- Utilisez toujours le même espace pour la même activité
- Créez des habitudes mentales
- Ne changez pas votre organisation tous les jours

**2. Commencez simple**
- Débutez avec 2 espaces : travail / perso
- Ajoutez des espaces quand vous en ressentez le besoin
- Pas besoin de tout utiliser d'un coup

**3. Nommez vos espaces**
- Facilite l'identification
- Renforce l'organisation mentale
- Aide en cas de désorientation

**4. Minimisez moins**
- Utilisez les espaces au lieu de tout minimiser
- Chaque fenêtre a sa place dans un espace
- Le panneau de chaque espace reste épuré

**5. Exploitez les collantes**
- Pour outils transversaux (lecteur audio, notes)
- Pas trop (2-3 maximum)
- Seulement ce qui est vraiment utile partout

**6. Maîtrisez les raccourcis**
- Ctrl + Alt + flèches devient réflexe
- Beaucoup plus rapide que la souris
- Permet de rester concentré

## Espaces de travail sur plusieurs écrans

Si vous avez plusieurs moniteurs, les espaces de travail fonctionnent différemment.

### Comportement par défaut

**Espaces indépendants par écran :**
- Chaque écran peut être sur un espace différent
- L'espace 1 sur l'écran 1 peut coexister avec l'espace 2 sur l'écran 2

**Ou espaces communs :**
- Les deux écrans changent d'espace ensemble
- Configuration à choisir selon préférence

**Configuration :**
- Paramètres système → Affichage
- Options multi-écrans et espaces de travail

### Stratégies multi-écrans + espaces

**Stratégie 1 : Écrans fixes, espaces variables**
- Écran 1 : toujours travail
- Écran 2 : change d'espace selon activité

**Stratégie 2 : Espaces synchronisés**
- Les deux écrans sur le même espace
- Organisation par thématique sur les deux écrans

**Stratégie 3 : Hybride**
- Écran principal : 4 espaces de travail
- Écran secondaire : toujours les mêmes outils (mail, musique)

## Différences avec MATE et Xfce

### Espaces de travail dans MATE

**Similitudes :**
- Concept identique
- Raccourcis similaires
- Configuration comparable

**Différences :**
- Moins d'effets visuels
- Vue d'ensemble moins élaborée
- Plus léger en ressources
- Applet de sélection différent

**Accès :**
- Applet "Sélecteur d'espace" dans le panneau
- Raccourcis Ctrl + Alt + flèches

### Espaces de travail dans Xfce

**Particularités :**
- Applet très configurable
- Peut afficher miniatures des fenêtres
- Très rapide et léger
- Noms et nombre facilement configurables

**Accès :**
- Applet dans le panneau (presque toujours visible par défaut)
- Molette sur l'applet pour changer
- Raccourcis personnalisables

**Configuration :**
- Paramètres → Espaces de travail
- Plus d'options visuelles pour l'applet

## Alternatives et compléments

### Extensions Cinnamon

**Workspace Indicator Plus :**
- Indicateur amélioré
- Plus d'informations visuelles
- Thèmes personnalisables

**Workspace Switcher with Previews :**
- Aperçus des fenêtres directement dans le panneau
- Changement au survol

### Outils tiers

**Compiz (historique) :**
- Ancien gestionnaire de fenêtres avec effets
- Cube 3D pour les espaces de travail
- Très visuel mais obsolète

**i3, bspwm (tiling managers) :**
- Gestionnaires en mosaïque
- Espaces de travail au cœur du concept
- Pour utilisateurs avancés

## Dépannage

### Les raccourcis ne fonctionnent pas

**Vérifications :**
1. Paramètres système → Clavier → Raccourcis
2. Catégorie "Espaces de travail"
3. Vérifiez que les raccourcis sont bien définis
4. Pas de conflit avec une autre application

**Conflit courant :**
- Certaines applications captent Ctrl + Alt + flèches
- Désactivez le raccourci de l'application
- Ou modifiez les raccourcis système

### La vue d'ensemble (Expo) ne s'active pas

**Solutions :**
1. Vérifiez le coin actif :
   - Paramètres système → Coins actifs
   - Coin supérieur gauche → Expo
2. Essayez le raccourci : Ctrl + Alt + ↑
3. Redémarrez Cinnamon : Alt + F2 → "r" → Entrée

### Fenêtres disparaissent

**Probablement sur un autre espace :**
1. Ctrl + Alt + ↑ pour voir tous les espaces
2. Cherchez la fenêtre visuellement
3. Ou Alt + Tab pour basculer entre toutes les fenêtres

**Astuce :** L'applet liste des fenêtres indique sur quel espace est chaque fenêtre.

### Désorientation spatiale

**Si vous vous perdez :**
1. Utilisez Ctrl + Alt + ↑ pour voir tous les espaces
2. Ou activez l'applet sélecteur d'espaces dans le panneau
3. Nommez vos espaces pour mieux les identifier

**Réduire la confusion :**
- Commencez avec 2 espaces seulement
- Augmentez progressivement
- Restez organisé et cohérent

### Performance lente

**Si le changement d'espace est lent :**
1. Désactivez les effets visuels :
   - Paramètres système → Effets
   - Réduisez ou désactivez les animations
2. Vérifiez les ressources système (RAM, CPU)
3. Fermez les applications inutiles

## Astuces avancées

### 1. Workflow "Pomodoro"

Utilisez un espace par cycle :
- Espace 1 : session de travail (25 min)
- Espace 2 : pause (5 min)
- Changez d'espace = changez de mode

### 2. Contexte visuel

Assignez un fond d'écran différent par espace :
- Nécessite une extension ou script
- Renforce l'identification visuelle
- Aide psychologique au changement de contexte

### 3. Démarrage automatique

Configurez des applications pour s'ouvrir sur un espace précis au démarrage :
- Applications de démarrage automatique
- Scripts pour positionner les fenêtres
- Restaure votre environnement de travail

### 4. Espaces temporaires

Utilisez un espace comme "bac à sable" :
- Pour tester des applications
- Pour organiser des téléchargements
- Nettoyez-le régulièrement

### 5. Combinaison avec les onglets

- Navigateur : plusieurs onglets sur espace Communication
- Terminal : plusieurs onglets sur espace Développement
- Nemo : onglets pour organisation de fichiers
- Espaces + onglets = organisation à deux niveaux

## Alternatives aux espaces de travail

Si les espaces de travail ne vous conviennent pas, voici d'autres méthodes :

### Gestionnaires de fenêtres en mosaïque (tiling)

**i3, bspwm, awesome :**
- Fenêtres organisées automatiquement sans chevauchement
- Pas besoin d'espaces multiples
- Courbe d'apprentissage importante
- Pour utilisateurs avancés

### Plusieurs moniteurs physiques

**Si vous avez l'espace et le budget :**
- Plus intuitif pour certains
- Pas de basculement mental
- Mais plus cher et encombrant

### Organisation stricte par fenêtres

**Sans espaces de travail :**
- Alt + Tab très organisé
- Minimisation systématique
- Fenêtres toujours au même endroit
- Fonctionnel mais moins efficace

## Conclusion

Les espaces de travail virtuels sont un outil puissant d'organisation et de productivité, souvent sous-utilisé par les débutants. Une fois maîtrisés, ils transforment véritablement votre façon de travailler et vous permettent de gérer efficacement de nombreuses tâches simultanées sans confusion.

**Points clés à retenir :**

**Le concept :**
- Plusieurs bureaux virtuels sur un seul écran
- Chaque espace est indépendant
- Basculement instantané entre espaces

**Navigation :**
- **Ctrl + Alt + flèches** : navigation rapide
- **Ctrl + Alt + ↑** : vue d'ensemble
- Coins actifs pour accès visuel

**Organisation :**
- Commencez avec 2-4 espaces
- Un espace = une activité ou un projet
- Restez cohérent dans votre utilisation
- Nommez vos espaces

**Productivité :**
- Moins de distractions
- Contextes séparés
- Moins de fenêtres empilées
- Transitions mentales facilitées

**Conseils pratiques :**
- Maîtrisez les raccourcis clavier
- Utilisez l'Expo pour réorganiser
- Fenêtres collantes pour outils transversaux
- Adaptez à votre workflow personnel

N'ayez pas peur d'expérimenter ! Les espaces de travail demandent un petit temps d'adaptation, mais deviennent vite indispensables. Commencez doucement avec 2 espaces, et augmentez progressivement selon vos besoins.

Dans le prochain chapitre, nous découvrirons les raccourcis clavier essentiels qui, combinés aux espaces de travail, feront de vous un utilisateur Linux Mint très efficace !

---

**Prochaine étape :** Raccourcis clavier essentiels

⏭️ [Raccourcis clavier essentiels](/04-decouverte-de-lenvironnement-de-bureau/05-raccourcis-clavier-essentiels.md)
