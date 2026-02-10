🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.2 Le gestionnaire de mises à jour

## Introduction

Le **Gestionnaire de mises à jour** (Update Manager) est l'outil qui maintient votre système Linux Mint à jour et sécurisé. Contrairement à Windows qui peut forcer les redémarrages pour les mises à jour, Linux Mint vous donne le contrôle total sur quand et comment mettre à jour votre système.

C'est un peu comme un mécanicien qui vérifie régulièrement votre voiture : il détecte ce qui doit être amélioré ou réparé, et vous propose de le faire au moment qui vous convient.

## Pourquoi les mises à jour sont importantes ?

### Sécurité avant tout

Les mises à jour corrigent des **failles de sécurité** découvertes dans le système et les applications. Sans mises à jour régulières, votre ordinateur devient vulnérable aux virus, malwares et tentatives de piratage.

### Corrections de bugs

Les développeurs corrigent constamment des bugs (bogues) qui peuvent causer :
- Des plantages d'applications
- Des ralentissements
- Des comportements inattendus
- Des pertes de données

### Nouvelles fonctionnalités

Certaines mises à jour apportent :
- De nouvelles options
- Des améliorations de performance
- Une meilleure compatibilité matérielle
- Une interface modernisée

### Stabilité du système

Un système régulièrement mis à jour est un système stable. Les mises à jour préviennent de nombreux problèmes avant qu'ils ne surviennent.

## Comment accéder au Gestionnaire de mises à jour

### Méthode 1 : Via l'icône de notification

Quand des mises à jour sont disponibles, une **icône de bouclier** apparaît dans la barre des tâches (en bas à droite de l'écran) :
- **Bouclier vert** : Mises à jour recommandées disponibles
- **Bouclier orange** : Mises à jour importantes disponibles
- **Bouclier rouge** : Mises à jour de sécurité critiques disponibles

Cliquez simplement sur cette icône pour ouvrir le Gestionnaire de mises à jour.

### Méthode 2 : Via le menu principal

1. Cliquez sur le **Menu** (en bas à gauche)
2. Tapez "**Mises à jour**" ou "**Update Manager**"
3. Cliquez sur l'application **Gestionnaire de mises à jour**

### Méthode 3 : Via le terminal (pour les curieux)

```bash
mintupdate
```

## Découverte de l'interface

### Premier lancement

Au premier lancement, le Gestionnaire de mises à jour :
1. **Vérifie les mises à jour disponibles** : Cela prend quelques secondes
2. **Télécharge la liste des paquets** : Informations sur les mises à jour
3. **Affiche les mises à jour disponibles** : Liste organisée par importance

### Les éléments de l'interface

L'interface se compose de plusieurs parties :

- **Barre d'outils** (en haut) : Boutons d'action principaux
- **Liste des mises à jour** : Toutes les mises à jour disponibles avec détails
- **Zone d'information** (en bas) : Statistiques et messages importants
- **Menu** : Options et paramètres avancés

### La liste des mises à jour

Chaque mise à jour affiche :
- **Nom du paquet** : Nom technique de l'application ou du composant
- **Version actuelle → Nouvelle version** : Changement de numéro de version
- **Taille** : Espace de téléchargement nécessaire
- **Description** : Explication rapide de ce que fait le paquet

## Les niveaux de mises à jour

Linux Mint classe les mises à jour par niveau de risque et d'importance. C'est une fonctionnalité unique qui vous aide à comprendre ce que vous installez.

### Niveau 1 (Vert) - Recommandées

- **Risque** : Très faible
- **Contenu** : Mises à jour testées et approuvées par l'équipe Linux Mint
- **Exemples** : Corrections de bugs mineurs, améliorations mineures
- **Action** : **Installez-les systématiquement**

### Niveau 2 (Vert) - Recommandées

- **Risque** : Faible
- **Contenu** : Mises à jour Ubuntu testées et fiables
- **Exemples** : Applications standard, bibliothèques courantes
- **Action** : **Installez-les sans hésiter**

### Niveau 3 (Orange) - Sûres

- **Risque** : Modéré
- **Contenu** : Mises à jour qui peuvent affecter certaines fonctionnalités
- **Exemples** : Mises à jour de pilotes, modifications système
- **Action** : **Installez-les généralement**, mais lisez les descriptions

### Niveau 4 (Orange) - Non recommandées

- **Risque** : Notable
- **Contenu** : Mises à jour importantes qui peuvent causer des problèmes
- **Exemples** : Noyau Linux, composants système critiques
- **Action** : **Soyez prudent**, installez uniquement si nécessaire

### Niveau 5 (Rouge) - Dangereuses

- **Risque** : Élevé
- **Contenu** : Mises à jour non testées qui peuvent casser le système
- **Exemples** : Versions expérimentales, paquets instables
- **Action** : **N'installez que si vous savez ce que vous faites**

### Mises à jour de sécurité (icône bouclier)

Reconnaissables à leur **icône de bouclier**, ces mises à jour :
- Corrigent des failles de sécurité
- **Doivent être installées rapidement**, quel que soit leur niveau
- Sont prioritaires pour la sécurité de votre système

## Installer les mises à jour

### Installation simple (recommandée pour débutants)

C'est la méthode la plus simple et la plus sûre :

1. **Ouvrez le Gestionnaire de mises à jour**
2. Attendez que la liste des mises à jour se charge
3. Vérifiez les mises à jour proposées (généralement niveau 1 et 2 sont présélectionnées)
4. Cliquez sur le bouton **"Installer les mises à jour"**
5. **Entrez votre mot de passe** pour autoriser l'installation
6. **Attendez la fin de l'installation** : Une barre de progression vous informe

### Installation sélective (utilisateurs avancés)

Si vous voulez choisir précisément ce qui sera installé :

1. **Décochez les mises à jour** que vous ne voulez pas installer
2. **Cochez celles** que vous souhaitez ajouter
3. Cliquez sur **"Installer les mises à jour"**

**Note** : Pour les débutants, il est recommandé de garder la sélection par défaut.

### Pendant l'installation

Pendant que les mises à jour s'installent :
- **Vous pouvez continuer à utiliser votre ordinateur** : Pas besoin d'arrêter de travailler
- **Évitez d'éteindre l'ordinateur** : Attendez la fin du processus
- **Ne fermez pas le Gestionnaire de mises à jour** : Laissez-le ouvert jusqu'au message de fin

### Après l'installation

Une fois les mises à jour installées :
- Un message vous confirme que **tout s'est bien passé**
- Dans la plupart des cas, **aucun redémarrage n'est nécessaire**
- Si un redémarrage est requis, un message vous le signalera

## Quand redémarrer ?

### Cas où un redémarrage est nécessaire

Vous devez redémarrer votre ordinateur après :
- **Mise à jour du noyau Linux** (kernel) : Le cœur du système
- **Certaines mises à jour de sécurité critiques**
- **Mise à jour de composants système essentiels**

Le Gestionnaire de mises à jour vous **avertit clairement** quand un redémarrage est nécessaire avec un message ou une icône spécifique.

### Cas où un redémarrage n'est PAS nécessaire

La plupart du temps, vous n'avez pas besoin de redémarrer après :
- Mises à jour d'applications normales
- Mises à jour de bibliothèques
- Corrections de bugs mineurs

C'est un gros avantage de Linux : **vous contrôlez les redémarrages**.

### Quand redémarrer si ce n'est pas obligatoire ?

Même si ce n'est pas obligatoire, il peut être judicieux de redémarrer :
- **À la fin de votre journée de travail** : Pour repartir sur de bonnes bases
- **Après plusieurs grosses mises à jour** : Pour s'assurer que tout fonctionne bien
- **Si vous constatez des comportements étranges** : Un redémarrage résout souvent les petits problèmes

## Vérifier manuellement les mises à jour

Par défaut, Linux Mint vérifie automatiquement les mises à jour, mais vous pouvez aussi le faire manuellement.

### Rafraîchir la liste

1. Ouvrez le **Gestionnaire de mises à jour**
2. Cliquez sur le bouton **"Rafraîchir"** (icône de flèche circulaire)
3. Attendez que la vérification se termine

Le système va :
- Se connecter aux serveurs de mises à jour
- Télécharger la liste des nouveaux paquets disponibles
- Afficher les mises à jour trouvées

### Fréquence de vérification recommandée

- **Automatique** : Laissez Linux Mint vérifier quotidiennement (c'est le réglage par défaut)
- **Manuel** : Vérifiez au moins **une fois par semaine** si vous avez désactivé les vérifications automatiques

## Paramètres et préférences

Le Gestionnaire de mises à jour offre de nombreuses options de personnalisation.

### Accéder aux préférences

1. Cliquez sur **"Édition"** dans la barre de menu
2. Sélectionnez **"Préférences"** (ou utilisez le raccourci clavier Ctrl+P)

### Paramètres importants

#### Onglet "Auto-Refresh" (Actualisation automatique)

- **Activer l'actualisation automatique** : Recommandé de laisser coché
- **Fréquence** : Par défaut, vérifie toutes les heures
- **Notification** : Vous avertit quand des mises à jour sont disponibles

#### Onglet "Auto-Update" (Mises à jour automatiques)

Vous pouvez configurer l'installation automatique :
- **Mises à jour de sécurité seulement** : Option sûre
- **Toutes les mises à jour recommandées** : Pour les utilisateurs qui veulent un système toujours à jour
- **Désactivé** : Vous contrôlez tout manuellement (recommandé pour débuter)

**Conseil pour débutants** : Gardez les mises à jour manuelles au début pour apprendre comment ça fonctionne.

#### Onglet "Levels" (Niveaux)

- **Niveaux visibles** : Choisissez quels niveaux de mises à jour afficher
- **Niveaux sûrs** : Définissez quels niveaux vous considérez comme sûrs
- **Recommandation** : Gardez les niveaux 1 et 2 visibles et activés

#### Onglet "Ignored updates" (Mises à jour ignorées)

Liste des mises à jour que vous avez choisi d'ignorer définitivement.

### Réinitialiser les avertissements

Si vous avez cliqué sur "Ne plus afficher ce message" et que vous regrettez :
1. Allez dans **Préférences**
2. Onglet **"Général"**
3. Cliquez sur **"Réinitialiser tous les avertissements ignorés"**

## Gérer les problèmes de mises à jour

### Une mise à jour échoue

Si l'installation d'une mise à jour échoue :

1. **Vérifiez votre connexion Internet** : Les mises à jour se téléchargent en ligne
2. **Fermez et rouvrez le Gestionnaire** : Parfois cela suffit
3. **Changez de miroir** : Les serveurs peuvent être temporairement indisponibles
4. **Réessayez plus tard** : Le problème peut être temporaire

### Changer de miroir (serveur de téléchargement)

Si les téléchargements sont lents ou échouent :

1. Ouvrez les **Préférences** du Gestionnaire de mises à jour
2. Allez dans l'onglet **"Mirrors"** (Miroirs)
3. Cliquez sur **"Principaux miroirs"**
4. Choisissez un serveur proche géographiquement ou cliquez sur **"Trouver le meilleur miroir"**
5. Validez et réessayez

### Dépendances cassées

Parfois, un message d'erreur parle de "dépendances cassées" :

```bash
sudo apt install -f
```

Cette commande tente de réparer automatiquement les dépendances.

### Verrouillage du gestionnaire de paquets

Si un message dit que le système est "verrouillé" :
- **Attendez quelques minutes** : Une autre opération est peut-être en cours
- **Fermez tous les gestionnaires** : Gestionnaire de logiciels, Synaptic, etc.
- **En dernier recours**, supprimez le fichier de verrouillage (voir chapitre dépannage avancé)

## Mises à jour du noyau Linux (Kernel)

Le **noyau** (kernel) est le cœur du système d'exploitation. Ses mises à jour sont spéciales.

### Pourquoi le noyau est important

Le noyau :
- Gère le matériel (carte graphique, processeur, disques, etc.)
- Coordonne les applications
- Assure la sécurité du système

### Quand mettre à jour le noyau

- **Si tout fonctionne bien** : Pas urgent, attendez quelques semaines pour laisser les autres utilisateurs tester
- **Problème matériel** : Une mise à jour du noyau peut corriger des bugs de pilotes
- **Sécurité** : Les mises à jour de sécurité du noyau sont prioritaires

### Comment mettre à jour le noyau

1. Le noyau apparaît comme une mise à jour normale (niveau 4 généralement)
2. Lisez les notes de version avant d'installer
3. Installez comme une mise à jour classique
4. **Redémarrez obligatoirement** après l'installation

### Que faire si un nouveau noyau pose problème

Linux Mint garde automatiquement les anciens noyaux :
- Au démarrage, appuyez sur **Shift** ou **Esc**
- Sélectionnez **"Options avancées"**
- Choisissez un ancien noyau
- Une fois démarré, désinstallez le noyau problématique via le Gestionnaire de mises à jour

## Historique des mises à jour

### Consulter l'historique

Pour voir toutes les mises à jour installées :

1. Menu **"Affichage"**
2. Sélectionnez **"Historique des mises à jour"**

Vous verrez :
- La date et l'heure de chaque installation
- La liste des paquets installés
- Les versions installées

### Pourquoi c'est utile

L'historique permet de :
- **Identifier un problème** : "Le bug est apparu après quelle mise à jour ?"
- **Documenter les changements** : Savoir ce qui a été modifié
- **Annuler une mise à jour** : En réinstallant l'ancienne version (avancé)

## Les mises à jour de version (Upgrade)

Il existe deux types de mises à jour sous Linux :

### Mises à jour régulières (Updates)
Ce que nous avons vu jusqu'ici :
- Corrections et améliorations
- Gérées par le Gestionnaire de mises à jour
- Fréquentes et légères

### Mises à jour de version (Upgrades)
Changement de version majeure de Linux Mint :
- Par exemple : Linux Mint 21.1 → 21.2 ou 21 → 22
- **Moins fréquentes** : Tous les 6 mois à 2 ans
- **Plus importantes** : Nouvelles fonctionnalités majeures
- **Nécessitent plus d'attention** : Suivez le guide officiel

**Important** : Les mises à jour de version sont un sujet à part et seront traitées dans un chapitre dédié.

## Bonnes pratiques

### Pour les débutants

1. **Installez les mises à jour régulièrement** : Au moins une fois par semaine
2. **Privilégiez les niveaux 1 et 2** : Restez dans la zone de sécurité
3. **Lisez les descriptions** : Surtout pour les mises à jour de niveau 3 et 4
4. **Ne paniquez pas en cas d'erreur** : La plupart des problèmes se résolvent facilement
5. **Créez des sauvegardes Timeshift** : Avant toute grosse mise à jour (nous verrons cela plus tard)

### Pour tous les utilisateurs

1. **Ne reportez pas indéfiniment** : Les mises à jour de sécurité sont critiques
2. **Vérifiez votre connexion** : Avant de lancer de grosses mises à jour
3. **Choisissez le bon moment** : Pas juste avant une présentation importante
4. **Lisez les notes de version** : Pour les mises à jour importantes
5. **Soyez patient** : Certaines mises à jour prennent du temps

### Planning recommandé

Un bon rythme de mises à jour :
- **Quotidien** : Vérification automatique (laissez l'option activée)
- **Hebdomadaire** : Installation des mises à jour (niveau 1 et 2)
- **Mensuel** : Revue des mises à jour de niveau 3
- **Selon besoin** : Mises à jour de niveau 4 et 5

## Différences avec Windows Update

Si vous venez de Windows, voici les différences majeures :

| Windows Update | Linux Mint Update Manager |
|----------------|---------------------------|
| Redémarrages fréquents et forcés | Redémarrages rares et contrôlés |
| Téléchargement en arrière-plan (impact performances) | Vous choisissez quand télécharger |
| Mises à jour Windows uniquement | Mises à jour de TOUT le système |
| Peu de contrôle | Contrôle total sur chaque mise à jour |
| Parfois très long | Généralement rapide |
| Pas de niveaux de risque | Système de niveaux clair |
| Difficile d'ignorer des mises à jour | Facile de sauter certaines mises à jour |

## Messages et notifications

### Types de notifications

Vous recevrez des notifications pour :
- **Nouvelles mises à jour disponibles** : Icône dans la barre des tâches
- **Mises à jour de sécurité critiques** : Notification prioritaire
- **Mises à jour nécessitant un redémarrage** : Message clair
- **Erreurs d'installation** : Alerte en cas de problème

### Gérer les notifications

Dans les préférences du Gestionnaire de mises à jour :
- Activez/désactivez les notifications
- Choisissez la fréquence
- Définissez le niveau minimum pour être alerté

**Recommandation** : Gardez au moins les notifications pour les mises à jour de sécurité.

## Sécurité et mises à jour

### Pourquoi les mises à jour sont votre première ligne de défense

- **80% des piratages** exploitent des failles connues et déjà corrigées
- **Ne pas mettre à jour** = Laisser la porte ouverte aux attaques
- **Les mises à jour de sécurité** corrigent ces failles

### Reconnaître une mise à jour de sécurité

Les mises à jour de sécurité sont marquées par :
- **Une icône de bouclier** à côté du paquet
- **Mention "Security"** dans la description
- **Priorité dans l'affichage** : Elles apparaissent en haut

**Règle d'or** : Les mises à jour de sécurité doivent TOUJOURS être installées, quel que soit leur niveau.

## Ligne de commande (optionnel pour débutants)

Pour les curieux, voici les commandes équivalentes :

### Vérifier les mises à jour
```bash
sudo apt update
```

### Installer les mises à jour
```bash
sudo apt upgrade
```

### Installer avec mise à jour du système
```bash
sudo apt full-upgrade
```

### Nettoyer les anciens paquets
```bash
sudo apt autoremove  
sudo apt autoclean  
```

**Note** : Ces commandes sont expliquées en détail dans le chapitre "APT en ligne de commande".

## Troubleshooting rapide

### Problème : "Impossible de récupérer certains fichiers"
**Solution** : Vérifiez votre connexion Internet, changez de miroir

### Problème : "dpkg a été interrompu"
**Solution** :
```bash
sudo dpkg --configure -a
```

### Problème : Le gestionnaire ne se lance pas
**Solution** : Ouvrez le terminal et tapez :
```bash
sudo rm /var/lib/apt/lists/lock  
sudo rm /var/cache/apt/archives/lock  
```

### Problème : Mises à jour très lentes
**Solution** : Changez de miroir pour un serveur plus proche ou plus rapide

## Conclusion

Le Gestionnaire de mises à jour est votre allié pour un système sûr, stable et performant. Contrairement à d'autres systèmes, Linux Mint vous donne le contrôle total tout en restant simple d'utilisation.

**Points clés à retenir :**
- Installez régulièrement les mises à jour (au moins une fois par semaine)
- Priorisez les mises à jour de sécurité
- Les niveaux 1 et 2 sont sans risque
- Vous contrôlez les redémarrages
- En cas de problème, la plupart des solutions sont simples

**Prochaine étape** : Maintenant que vous maîtrisez les mises à jour graphiques, nous allons découvrir **APT en ligne de commande** pour aller encore plus loin dans la gestion des logiciels.

---


⏭️ [APT en ligne de commande (apt, apt-get, dpkg)](/06-gestion-des-logiciels/03-apt-en-ligne-de-commande.md)
