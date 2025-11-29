🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 16.2 - Extensions Cinnamon (ou MATE/Xfce)

## Introduction

Les extensions sont de petits programmes qui ajoutent des fonctionnalités supplémentaires à votre environnement de bureau Linux Mint. Elles permettent de transformer votre système en ajoutant des outils pratiques, des améliorations visuelles ou des raccourcis qui facilitent votre travail quotidien.

Contrairement aux thèmes qui changent l'apparence, les extensions ajoutent de nouvelles **fonctionnalités**. C'est un peu comme installer des plugins dans un navigateur web.

Dans ce chapitre, nous allons découvrir comment installer, gérer et utiliser les extensions sur les différents environnements de bureau de Linux Mint.

---

## Comprendre les environnements de bureau

Linux Mint propose trois environnements de bureau principaux, chacun ayant son propre système d'extensions :

### Cinnamon
- L'environnement par défaut de Linux Mint
- Le plus moderne et riche en fonctionnalités
- Possède le plus grand nombre d'extensions disponibles
- Système d'extensions très développé

### MATE
- Environnement léger, continuation de GNOME 2
- Moins d'extensions que Cinnamon, mais bien suffisant
- Très stable et fiable
- Idéal pour les ordinateurs plus anciens

### Xfce
- L'environnement le plus léger
- Moins d'extensions natives
- Mise à jour via des plugins Xfce Panel
- Excellente performance sur matériel limité

**Note :** Ce chapitre se concentre principalement sur **Cinnamon** (l'environnement le plus utilisé), mais les principes généraux s'appliquent aux trois.

---

## Qu'est-ce qu'une extension ?

### Définition

Une **extension** (ou **applet** dans Cinnamon) est un petit programme qui s'intègre à votre bureau pour ajouter des fonctionnalités.

### Types d'extensions

Il existe différents types d'extensions dans Cinnamon :

1. **Applets** : S'ajoutent à votre panneau (barre des tâches)
   - Exemple : météo, moniteur système, presse-papier

2. **Desklets** : Se placent directement sur le bureau
   - Exemple : horloge, calendrier, notes

3. **Extensions** : Modifient le comportement du système
   - Exemple : effets visuels, gestion des fenêtres

4. **Thèmes** : Nous les avons vus au chapitre précédent

### Exemples concrets d'utilisation

- Afficher la météo dans votre panneau
- Surveiller l'utilisation du CPU et de la RAM
- Avoir un presse-papier qui mémorise vos dernières copies
- Accéder rapidement à vos fichiers récents
- Contrôler votre musique depuis le panneau
- Afficher un calendrier avec vos événements

---

## Comment accéder aux extensions ?

### Pour Cinnamon

**Méthode 1 : Via les Paramètres Système**

1. Ouvrez le **Menu** → **Préférences** → **Extensions**
   - Ou : **Menu** → **Préférences** → **Applets**
   - Ou : **Menu** → **Préférences** → **Desklets**

2. Vous verrez trois onglets en haut :
   - **Gérer** : Extensions actuellement installées
   - **Télécharger** : Parcourir et installer de nouvelles extensions
   - **Paramètres** : (selon l'extension sélectionnée)

**Méthode 2 : Clic droit sur le panneau**

1. Faites un **clic droit** sur votre panneau (barre des tâches)
2. Sélectionnez **"Applets"** dans le menu
3. Vous accédez directement à la gestion des applets du panneau

**Méthode 3 : Clic droit sur le bureau (pour Desklets)**

1. Faites un **clic droit** sur une zone vide du bureau
2. Sélectionnez **"Ajouter des desklets"**
3. Vous accédez à la gestion des desklets

### Pour MATE

1. Clic droit sur le panneau
2. Sélectionnez **"Ajouter au tableau de bord"**
3. Parcourez les applets disponibles

### Pour Xfce

1. Clic droit sur le panneau
2. Sélectionnez **"Tableau de bord"** → **"Ajouter de nouveaux éléments"**
3. Choisissez parmi les plugins disponibles

---

## Installer des extensions (Cinnamon)

### Méthode 1 : Via l'interface graphique (recommandée)

C'est la méthode la plus simple et la plus sûre pour les débutants.

**Étapes détaillées :**

1. **Ouvrir le gestionnaire**
   - Menu → Préférences → Applets (ou Extensions, ou Desklets)

2. **Accéder aux téléchargements**
   - Cliquez sur l'onglet **"Télécharger"** en haut

3. **Parcourir les extensions disponibles**
   - Vous verrez une liste avec :
     - Le nom de l'extension
     - Une brève description
     - Une note (étoiles)
     - Le nombre de téléchargements
     - Un bouton **"Installer"** ou **"Télécharger"**

4. **Filtrer et rechercher**
   - Utilisez la barre de recherche en haut pour trouver quelque chose de précis
   - Triez par popularité, note, ou date

5. **Installer une extension**
   - Cliquez sur **"Installer"** ou **"Télécharger"** à côté de l'extension choisie
   - Attendez quelques secondes (un message de confirmation apparaît)
   - L'extension est maintenant disponible dans l'onglet **"Gérer"**

6. **Activer l'extension**
   - Retournez dans l'onglet **"Gérer"**
   - Trouvez votre extension dans la liste
   - Cochez la case à côté pour l'activer
   - Pour les applets : vous devez ensuite l'ajouter au panneau

### Méthode 2 : Depuis le site web Cinnamon Spices

**Cinnamon Spices** est le dépôt officiel des extensions pour Cinnamon.

**Étapes :**

1. **Visitez le site**
   - Allez sur [https://cinnamon-spices.linuxmint.com/](https://cinnamon-spices.linuxmint.com/)
   - Choisissez la catégorie : Applets, Desklets, Extensions, ou Themes

2. **Télécharger l'extension**
   - Parcourez ou recherchez une extension
   - Cliquez sur **"Download"**
   - Enregistrez le fichier `.zip`

3. **Installer manuellement**
   - Ouvrez le gestionnaire d'applets/extensions
   - Regardez en bas de la fenêtre, vous verrez une icône **"+"** ou **"Installer depuis un fichier"**
   - Sélectionnez le fichier `.zip` téléchargé
   - L'extension s'installe automatiquement

**Note :** La méthode 1 (via l'interface) utilise automatiquement Cinnamon Spices, donc cette méthode manuelle est rarement nécessaire.

### Méthode 3 : Installation manuelle (utilisateurs avancés)

Si vous trouvez une extension sur GitHub ou ailleurs :

1. **Téléchargez l'extension** (généralement un fichier `.zip`)

2. **Extrayez le contenu**

3. **Placez le dossier au bon endroit :**

   Pour les **applets** :
   ```
   ~/.local/share/cinnamon/applets/
   ```

   Pour les **desklets** :
   ```
   ~/.local/share/cinnamon/desklets/
   ```

   Pour les **extensions** :
   ```
   ~/.local/share/cinnamon/extensions/
   ```

4. **Redémarrez Cinnamon**
   - Appuyez sur `Alt + F2`
   - Tapez `r` et appuyez sur Entrée
   - Ou déconnectez-vous et reconnectez-vous

5. **Activez l'extension** depuis le gestionnaire

---

## Gérer vos extensions

### Activer/Désactiver une extension

**Pour Cinnamon :**

1. Ouvrez le gestionnaire approprié (Applets, Extensions, ou Desklets)
2. Allez dans l'onglet **"Gérer"**
3. Trouvez l'extension dans la liste
4. **Cochez** la case pour activer, **décochez** pour désactiver

**Résultat :**
- Activation immédiate (pas besoin de redémarrer)
- Les extensions désactivées restent installées mais inactives

### Ajouter un applet au panneau

Les applets doivent être ajoutés manuellement au panneau après activation :

1. Après avoir activé l'applet, cliquez sur le bouton **"+"** en bas à gauche de la fenêtre
2. Ou : Faites un clic droit sur l'applet et choisissez **"Ajouter au panneau"**
3. L'applet apparaît dans votre panneau
4. Vous pouvez le déplacer en le faisant glisser (maintenir et déplacer)

**Retirer un applet du panneau :**
- Clic droit sur l'applet → **"Retirer..."**
- L'applet reste installé et activé, mais n'est plus visible

### Configurer une extension

Beaucoup d'extensions ont des paramètres personnalisables :

**Pour les applets du panneau :**
1. Clic droit sur l'applet → **"Configurer..."**
2. Une fenêtre de paramètres s'ouvre
3. Ajustez selon vos préférences

**Pour les extensions et desklets :**
1. Dans le gestionnaire, sélectionnez l'extension
2. Cliquez sur l'icône d'**engrenage** (⚙️) ou **"Configurer"**
3. Modifiez les paramètres disponibles

**Exemples de paramètres courants :**
- Intervalles de mise à jour
- Apparence et couleurs
- Position et taille
- Comportement au clic
- Raccourcis clavier

### Supprimer une extension

**Méthode simple :**

1. Ouvrez le gestionnaire de l'extension
2. Dans l'onglet **"Gérer"**, trouvez l'extension
3. Cliquez sur l'icône de **corbeille** (🗑️) à droite
4. Confirmez la suppression

**Méthode manuelle :**
- Naviguez vers le dossier de l'extension (voir chemins ci-dessus)
- Supprimez le dossier de l'extension
- Redémarrez Cinnamon

### Mettre à jour les extensions

Les extensions se mettent à jour automatiquement via le gestionnaire de mises à jour de Linux Mint.

**Vérification manuelle :**

1. Ouvrez le gestionnaire d'extensions
2. Dans l'onglet **"Télécharger"**, recherchez vos extensions installées
3. Si une mise à jour est disponible, un bouton **"Mettre à jour"** apparaîtra
4. Cliquez pour mettre à jour

**Important :** Après une mise à jour majeure de Linux Mint, certaines extensions peuvent devenir incompatibles. Vérifiez toujours les mises à jour disponibles.

---

## Extensions populaires et recommandées

Voici une sélection d'extensions utiles pour débuter, organisées par catégorie.

### Applets système et monitoring

**1. System Monitor (Moniteur système)**
- **Fonction :** Affiche l'utilisation CPU, RAM, réseau en temps réel
- **Utilité :** Surveiller les performances de votre système
- **Recommandé pour :** Tous les utilisateurs

**2. Multicore System Monitor**
- **Fonction :** Monitoring détaillé avec graphiques
- **Utilité :** Voir l'utilisation de chaque cœur du processeur
- **Recommandé pour :** Utilisateurs avancés, développeurs

**3. CPU Temperature Indicator**
- **Fonction :** Affiche la température du processeur
- **Utilité :** Surveiller la chaleur (utile pour les laptops)
- **Recommandé pour :** Utilisateurs de portables

### Applets de productivité

**4. Clipboard Manager (Gestionnaire de presse-papier)**
- **Fonction :** Mémorise vos dernières copies
- **Utilité :** Retrouver un texte copié il y a quelques minutes
- **Recommandé pour :** Tous les utilisateurs

**5. Todo List**
- **Fonction :** Liste de tâches dans le panneau
- **Utilité :** Gérer vos tâches quotidiennes rapidement
- **Recommandé pour :** Productivité personnelle

**6. Recent Files (Fichiers récents)**
- **Fonction :** Accès rapide aux derniers fichiers ouverts
- **Utilité :** Retrouver rapidement un document
- **Recommandé pour :** Tous les utilisateurs

### Applets météo et calendrier

**7. Weather (Météo)**
- **Fonction :** Prévisions météo dans le panneau
- **Utilité :** Voir la météo sans ouvrir de navigateur
- **Recommandé pour :** Tous les utilisateurs

**8. Calendar (Calendrier)**
- **Fonction :** Calendrier avec événements
- **Utilité :** Vue rapide des dates et rendez-vous
- **Recommandé pour :** Organisation personnelle

### Applets réseau et connexions

**9. Network Usage Monitor**
- **Fonction :** Affiche la vitesse de téléchargement/upload
- **Utilité :** Surveiller votre connexion Internet
- **Recommandé pour :** Utilisateurs conscients de leur bande passante

**10. VPN Sentinel**
- **Fonction :** Indicateur de connexion VPN
- **Utilité :** Savoir si votre VPN est actif
- **Recommandé pour :** Utilisateurs de VPN

### Applets média

**11. Sound 150%**
- **Fonction :** Permet d'augmenter le volume au-delà de 100%
- **Utilité :** Quand le volume maximum n'est pas assez fort
- **Recommandé pour :** Utilisateurs multimédia

**12. Radio++**
- **Fonction :** Écouter des stations de radio en ligne
- **Utilité :** Musique/infos sans ouvrir de navigateur
- **Recommandé pour :** Amateurs de radio

### Desklets populaires

**13. Simple System Monitor**
- **Fonction :** Affiche les stats système sur le bureau
- **Utilité :** Monitoring élégant et permanent
- **Recommandé pour :** Utilisateurs qui aiment surveiller leur système

**14. Notes**
- **Fonction :** Pense-bêtes sur le bureau
- **Utilité :** Prendre des notes rapides
- **Recommandé pour :** Organisation quotidienne

**15. Quotes of the Day**
- **Fonction :** Affiche une citation du jour
- **Utilité :** Inspiration quotidienne
- **Recommandé pour :** Motivation personnelle

### Extensions système

**16. Desktop Cube**
- **Fonction :** Effet 3D pour changer d'espace de travail
- **Utilité :** Esthétique et fun
- **Recommandé pour :** Personnalisation visuelle

**17. Window Demands Attention Behavior**
- **Fonction :** Gère le comportement des fenêtres demandant l'attention
- **Utilité :** Mieux gérer les notifications de fenêtres
- **Recommandé pour :** Amélioration de l'ergonomie

---

## Extensions pour MATE

MATE utilise un système d'applets similaire mais plus simple. Voici quelques applets utiles :

**Applets recommandés :**
- **Weather Report** : Météo
- **System Monitor** : Surveillance système
- **Timer Applet** : Minuteur/chronomètre
- **Trash Applet** : Accès rapide à la corbeille
- **Sensor Applet** : Températures et capteurs

**Installation :**
1. Clic droit sur le panneau → "Ajouter au tableau de bord"
2. Parcourir la liste
3. Sélectionner et cliquer "Ajouter"

---

## Plugins pour Xfce

Xfce utilise des **plugins de panneau** plutôt que des extensions.

**Plugins populaires :**
- **Weather Plugin** : Météo
- **System Load Monitor** : Surveillance système
- **Clipboard Manager** : Gestionnaire de presse-papier
- **PulseAudio Plugin** : Contrôle audio avancé
- **Battery Monitor** : Surveillance de batterie (laptops)

**Installation :**
1. Installez les plugins via le gestionnaire de logiciels :
   ```bash
   sudo apt install xfce4-goodies
   ```
2. Clic droit sur panneau → "Tableau de bord" → "Ajouter de nouveaux éléments"
3. Sélectionnez le plugin désiré

---

## Conseils et bonnes pratiques

### Pour bien débuter

1. **Commencez modestement**
   - N'installez pas 20 extensions d'un coup
   - Ajoutez-en quelques-unes, testez, puis ajoutez-en d'autres
   - Trop d'extensions peuvent ralentir le système

2. **Lisez les descriptions**
   - Chaque extension a une description détaillée
   - Regardez les captures d'écran quand disponibles
   - Vérifiez la compatibilité avec votre version de Cinnamon

3. **Vérifiez les notes et avis**
   - Les extensions bien notées sont généralement fiables
   - Lisez les commentaires pour connaître les bugs potentiels
   - Préférez les extensions régulièrement mises à jour

4. **Testez avant de vous engager**
   - Les extensions sont faciles à désinstaller
   - N'hésitez pas à en tester plusieurs
   - Gardez seulement celles que vous utilisez vraiment

### Optimisation et performance

**Nombre d'extensions :**
- Moins de 5 extensions : Impact négligeable
- 5-10 extensions : Léger impact (acceptable)
- Plus de 10 : Peut ralentir le système selon le matériel

**Types d'extensions gourmandes :**
- Les moniteurs système avec mise à jour rapide (< 1 seconde)
- Les extensions avec animations complexes
- Les desklets avec beaucoup d'éléments graphiques

**Optimisation :**
- Augmentez l'intervalle de rafraîchissement des moniteurs système
- Désactivez les extensions que vous n'utilisez pas
- Supprimez les extensions inutilisées

### Compatibilité et mises à jour

**Après une mise à jour de Linux Mint :**
1. Vérifiez que vos extensions fonctionnent
2. Consultez l'onglet "Télécharger" pour les mises à jour
3. Désactivez temporairement les extensions problématiques
4. Attendez une mise à jour de l'extension ou cherchez une alternative

**Versions de Cinnamon :**
- Chaque extension indique sa compatibilité
- Format : "Cinnamon 5.0" ou "Cinnamon 5.4+"
- Vérifiez votre version : Menu → À propos

**Commande pour vérifier votre version de Cinnamon :**
```bash
cinnamon --version
```

### Sécurité et confiance

**Extensions sûres :**
- Celles disponibles via le gestionnaire intégré (Cinnamon Spices)
- Extensions populaires avec beaucoup de téléchargements
- Extensions développées par des contributeurs vérifiés

**Signaux d'alerte :**
- Extensions sans description claire
- Aucun avis ou notes très basses
- Demandes de permissions inhabituelles
- Extensions provenant de sources non vérifiées

**Bonne pratique :**
- Privilégiez toujours Cinnamon Spices officiel
- Évitez d'installer des extensions depuis des sites inconnus
- En cas de doute, recherchez l'extension sur les forums Linux Mint

---

## Résolution de problèmes courants

### L'extension ne s'affiche pas

**Solutions :**

1. **Vérifiez qu'elle est activée**
   - Onglet "Gérer" → case cochée

2. **Pour les applets : ajoutez-les au panneau**
   - Bouton "+" après activation
   - Ou clic droit sur l'applet → "Ajouter au panneau"

3. **Redémarrez Cinnamon**
   - `Alt + F2` → tapez `r` → Entrée
   - Ou déconnectez-vous/reconnectez-vous

4. **Vérifiez la compatibilité**
   - L'extension est-elle compatible avec votre version ?

### L'extension provoque des erreurs

**Solutions :**

1. **Consultez les paramètres**
   - Certaines extensions nécessitent une configuration initiale

2. **Vérifiez les dépendances**
   - Certaines extensions nécessitent des paquets additionnels
   - Lisez la description pour les prérequis

3. **Regardez les logs**
   - Ouvrez le terminal et tapez :
   ```bash
   journalctl -f
   ```
   - Reproduisez le problème et observez les erreurs

4. **Désactivez et réinstallez**
   - Désactivez l'extension
   - Supprimez-la
   - Réinstallez-la

### Le système est ralenti

**Solutions :**

1. **Identifiez l'extension responsable**
   - Désactivez les extensions une par une
   - Observez les performances après chaque désactivation

2. **Ajustez les paramètres**
   - Augmentez l'intervalle de mise à jour (ex: de 1s à 3s)
   - Désactivez les animations

3. **Limitez le nombre d'extensions**
   - Gardez seulement celles vraiment utiles
   - Supprimez les redondances

### L'applet a disparu du panneau

**Solutions :**

1. **Réajoutez-le**
   - Menu → Préférences → Applets
   - Onglet "Gérer" → Bouton "+"

2. **Vérifiez l'espace disponible**
   - Le panneau est peut-être plein
   - Supprimez ou déplacez d'autres applets

3. **Restaurez le panneau par défaut**
   - En dernier recours : Menu → Préférences → Panneau → "Restaurer les paramètres par défaut"

---

## Créer ses propres extensions (aperçu)

Pour les utilisateurs qui souhaitent aller plus loin, il est possible de créer ses propres extensions Cinnamon.

**Langages utilisés :**
- JavaScript pour la logique
- CSS pour le style
- JSON pour les métadonnées

**Documentation :**
- [Documentation officielle Cinnamon](https://projects.linuxmint.com/reference/git/cinnamon-tutorials/)
- Regardez le code d'extensions existantes dans :
  `~/.local/share/cinnamon/applets/`

**Tutoriels recommandés :**
- Cinnamon Spices propose des guides pour développeurs
- GitHub contient de nombreux exemples commentés

---

## Différences entre environnements de bureau

### Tableau comparatif

| Aspect | Cinnamon | MATE | Xfce |
|--------|----------|------|------|
| **Nombre d'extensions** | Très élevé | Moyen | Limité |
| **Facilité d'installation** | Très facile | Facile | Facile |
| **Gestionnaire intégré** | Oui, complet | Non (manuel) | Non (manuel) |
| **Mises à jour auto** | Oui | Non | Non |
| **Complexité** | Moyenne | Simple | Simple |
| **Impact performance** | Variable | Faible | Très faible |

### Recommandations par environnement

**Choisissez Cinnamon si :**
- Vous voulez le maximum d'options
- Vous aimez personnaliser en détail
- Votre ordinateur est assez puissant (4 Go RAM+)

**Choisissez MATE si :**
- Vous préférez la simplicité
- Vous avez un ordinateur modeste (2-4 Go RAM)
- Vous voulez un système stable et éprouvé

**Choisissez Xfce si :**
- Vous avez du matériel ancien/limité
- Vous privilégiez les performances
- Vous n'avez pas besoin de beaucoup d'extensions

---

## Aller plus loin

Une fois à l'aise avec les extensions, vous pouvez explorer :

- **Les desklets** (Chapitre 16.3) : Widgets directement sur le bureau
- **Les applets personnalisés** : Créer vos propres outils
- **Conky** (Chapitre 16.4) : Monitoring visuel avancé
- **La personnalisation du terminal** (Chapitre 16.5)

Les extensions sont un moyen fantastique de façonner Linux Mint selon vos besoins exacts. Expérimentez, amusez-vous, et créez l'environnement de travail parfait pour vous !

---

## Résumé

Dans ce chapitre, vous avez appris :

- ✅ Ce que sont les extensions et leur utilité
- ✅ Les différences entre applets, desklets et extensions
- ✅ Comment installer des extensions via l'interface graphique
- ✅ Comment gérer, configurer et supprimer des extensions
- ✅ Des recommandations d'extensions populaires et utiles
- ✅ Les bonnes pratiques pour une utilisation optimale
- ✅ Comment résoudre les problèmes courants
- ✅ Les spécificités de chaque environnement de bureau

Les extensions transforment Linux Mint en un système véritablement personnalisé. Prenez le temps d'explorer et de trouver les outils qui amélioreront votre productivité et votre confort quotidien !

---


⏭️ [Desklets et applets personnalisés](/16-personnalisation-avancee/03-desklets-et-applets-personnalises.md)
