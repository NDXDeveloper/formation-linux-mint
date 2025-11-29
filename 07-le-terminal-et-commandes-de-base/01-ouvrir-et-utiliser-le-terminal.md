🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.1 - Ouvrir et utiliser le terminal

## Introduction

Le terminal (aussi appelé console, ligne de commande ou shell) est l'un des outils les plus puissants de Linux. Si vous débutez, il peut sembler intimidant avec son écran noir et son curseur clignotant, mais ne vous inquiétez pas : il est beaucoup plus accessible qu'il n'y paraît !

### Qu'est-ce que le terminal ?

Le terminal est une interface textuelle qui vous permet de communiquer directement avec votre système d'exploitation en tapant des commandes. Contrairement à l'interface graphique où vous cliquez sur des icônes et des menus, ici vous écrivez ce que vous voulez faire.

**Analogie simple :** Si l'interface graphique est comme un restaurant avec un menu illustré, le terminal est comme commander directement au chef en cuisine. C'est plus direct et souvent plus rapide une fois que vous connaissez le "langage".

### Pourquoi utiliser le terminal ?

Vous vous demandez peut-être : "Pourquoi apprendre le terminal alors que je peux tout faire avec la souris ?"

Voici quelques bonnes raisons :

- **Puissance** : Certaines tâches complexes sont beaucoup plus rapides en ligne de commande
- **Précision** : Vous avez un contrôle total sur ce qui se passe
- **Automatisation** : Vous pouvez répéter facilement des tâches
- **Dépannage** : Beaucoup de solutions en ligne utilisent des commandes terminal
- **Légèreté** : Le terminal consomme très peu de ressources
- **Universalité** : Les commandes Linux sont similaires sur toutes les distributions

**Rassurez-vous :** Vous n'êtes pas obligé d'utiliser le terminal pour tout ! Linux Mint est conçu pour être utilisable entièrement avec l'interface graphique. Le terminal est un outil supplémentaire, pas une obligation.

---

## Comment ouvrir le terminal

Il existe plusieurs façons d'ouvrir le terminal dans Linux Mint. Choisissez celle qui vous convient le mieux !

### Méthode 1 : Via le menu principal

1. Cliquez sur le **Menu** (icône en bas à gauche)
2. Dans la barre de recherche, tapez **"terminal"** ou **"console"**
3. Cliquez sur **Terminal** dans les résultats

### Méthode 2 : Raccourci clavier (la plus rapide)

Appuyez simultanément sur : **Ctrl + Alt + T**

C'est la méthode préférée des utilisateurs réguliers car elle est instantanée !

### Méthode 3 : Via le gestionnaire de fichiers

1. Ouvrez le gestionnaire de fichiers **Nemo**
2. Naviguez vers le dossier où vous voulez travailler
3. Faites un **clic droit** dans un espace vide
4. Sélectionnez **"Ouvrir dans un terminal"**

Cette méthode est très pratique car le terminal s'ouvre directement dans le dossier que vous regardez.

### Méthode 4 : Depuis le menu contextuel du bureau

1. Faites un **clic droit** sur le bureau
2. Sélectionnez **"Ouvrir dans un terminal"**

---

## Découvrir l'interface du terminal

Lorsque vous ouvrez le terminal, vous voyez quelque chose comme ceci :

```
utilisateur@ordinateur:~$
```

Décomposons cette ligne mystérieuse, appelée **prompt** (invite de commande) :

- **utilisateur** : Votre nom d'utilisateur (celui avec lequel vous vous êtes connecté)
- **@** : Signifie simplement "sur" ou "at" en anglais
- **ordinateur** : Le nom de votre ordinateur (hostname)
- **:** : Séparateur
- **~** : Représente votre dossier personnel (/home/utilisateur)
- **$** : Indique que vous êtes un utilisateur normal (pas administrateur)

**Note importante :** Si vous voyez un **#** au lieu de **$**, cela signifie que vous êtes en mode super-utilisateur (root). C'est rare et potentiellement dangereux pour un débutant.

### Le curseur clignotant

Après le symbole **$**, vous voyez un petit rectangle clignotant : c'est le **curseur**. Il indique où apparaîtra le texte que vous tapez.

---

## Comprendre les bases

### Taper une commande

Pour utiliser le terminal, vous tapez une **commande** puis vous appuyez sur **Entrée** pour l'exécuter.

**Format général :**
```
commande [options] [arguments]
```

- **commande** : L'action à effectuer (obligatoire)
- **options** : Modifient le comportement de la commande (facultatif)
- **arguments** : Les éléments sur lesquels la commande agit (facultatif)

**Exemple simple :**
```bash
ls
```

Cette commande affiche le contenu du dossier actuel. C'est comme ouvrir un dossier dans le gestionnaire de fichiers.

### Sensibilité à la casse

**Attention :** Linux fait la différence entre majuscules et minuscules !

- `ls` fonctionne
- `LS` ou `Ls` ne fonctionnera pas

### Espaces et caractères spéciaux

Les espaces séparent les différentes parties d'une commande. Si un nom de fichier contient des espaces, vous devez l'entourer de guillemets ou utiliser un antislash :

```bash
# Fichier avec espace
cat "mon fichier.txt"
# ou
cat mon\ fichier.txt
```

**Conseil :** Évitez les espaces dans les noms de fichiers quand vous travaillez en ligne de commande. Préférez les tirets ou underscores : `mon-fichier.txt` ou `mon_fichier.txt`

---

## Navigation dans le terminal

### Raccourcis clavier utiles

Le terminal dispose de nombreux raccourcis pour vous faciliter la vie :

#### Édition de texte :
- **Ctrl + C** : Interrompre la commande en cours (très important !)
- **Ctrl + D** : Fermer le terminal
- **Ctrl + L** : Effacer l'écran (comme la commande `clear`)
- **Ctrl + A** : Aller au début de la ligne
- **Ctrl + E** : Aller à la fin de la ligne
- **Ctrl + U** : Effacer tout avant le curseur
- **Ctrl + K** : Effacer tout après le curseur

#### Navigation dans l'historique :
- **Flèche Haut ↑** : Commande précédente
- **Flèche Bas ↓** : Commande suivante
- **Ctrl + R** : Rechercher dans l'historique des commandes

#### Copier-coller :
- **Ctrl + Shift + C** : Copier (notez le Shift supplémentaire !)
- **Ctrl + Shift + V** : Coller
- **Clic du milieu de la souris** : Coller ce qui est sélectionné

**Note :** Dans le terminal, **Ctrl + C** sert à interrompre une commande, pas à copier. C'est pourquoi il faut ajouter **Shift** pour copier.

### Complétion automatique avec Tab

La touche **Tab** est votre meilleure amie ! Elle complète automatiquement :

1. Les noms de commandes
2. Les noms de fichiers et dossiers
3. Les chemins

**Exemple :**
- Tapez `Docu` puis appuyez sur **Tab** → Cela complète en `Documents/`
- Tapez deux fois sur **Tab** pour voir toutes les options possibles

Cela évite les fautes de frappe et vous fait gagner beaucoup de temps !

---

## Obtenir de l'aide

### La commande `man` (manuel)

Chaque commande Linux dispose d'un manuel intégré. Pour le consulter :

```bash
man nom_de_la_commande
```

**Exemple :**
```bash
man ls
```

**Navigation dans le manuel :**
- **Flèches** ou **Page Up/Down** : Naviguer
- **/** : Rechercher un mot
- **Q** : Quitter le manuel

### L'option `--help`

Presque toutes les commandes acceptent l'option `--help` pour afficher une aide rapide :

```bash
ls --help
```

C'est souvent plus concis et plus rapide que le manuel complet.

---

## Conseils pour bien débuter

### 1. N'ayez pas peur d'expérimenter

Le terminal n'est pas aussi dangereux qu'on le pense ! La plupart des commandes ne peuvent pas endommager votre système si vous êtes connecté en tant qu'utilisateur normal (symbole **$**).

**Exception :** Les commandes précédées de `sudo` demandent des privilèges administrateur. Soyez plus prudent avec celles-ci.

### 2. Lisez les messages d'erreur

Quand quelque chose ne fonctionne pas, le terminal vous dit pourquoi. Prenez le temps de lire le message, même s'il est en anglais. Vous pouvez le copier-coller dans un moteur de recherche pour trouver des solutions.

### 3. Utilisez l'historique

Vous avez tapé une longue commande et vous voulez la modifier légèrement ? Utilisez la **flèche haut ↑** pour la retrouver, puis modifiez-la au lieu de tout retaper.

### 4. Pratiquez régulièrement

Comme pour apprendre une langue, la pratique régulière est la clé. Essayez d'utiliser le terminal pour quelques tâches simples au quotidien.

### 5. Gardez un pense-bête

Notez les commandes que vous utilisez souvent. Avec le temps, elles deviendront naturelles.

---

## Personnalisation de base

### Ouvrir plusieurs onglets

Vous pouvez ouvrir plusieurs onglets dans la même fenêtre de terminal :

- **Ctrl + Shift + T** : Nouvel onglet
- **Ctrl + Page Up/Down** : Naviguer entre les onglets
- **Ctrl + Shift + W** : Fermer l'onglet actuel

### Ajuster la taille de la fenêtre

- **F11** : Mode plein écran
- **Ctrl + Shift + (+)** : Agrandir le texte
- **Ctrl + (-)** : Réduire le texte
- **Ctrl + 0** : Taille par défaut

### Changer les couleurs (facultatif)

1. Cliquez sur **Édition** → **Préférences** dans la barre de menu du terminal
2. Allez dans l'onglet **Couleurs**
3. Choisissez un thème ou personnalisez les couleurs

Certains utilisateurs préfèrent un fond sombre avec du texte vert ou blanc pour un meilleur confort visuel.

---

## Commandes de base pour commencer

Voici quelques commandes très simples et sans danger pour vous familiariser :

### Afficher où vous êtes
```bash
pwd
```
(Print Working Directory - Affiche le chemin du dossier actuel)

### Voir le contenu du dossier
```bash
ls
```

### Voir la date et l'heure
```bash
date
```

### Voir qui vous êtes
```bash
whoami
```

### Afficher un calendrier
```bash
cal
```

### Effacer l'écran
```bash
clear
```

### Afficher l'historique des commandes
```bash
history
```

---

## Fermer le terminal

Plusieurs façons de quitter le terminal :

1. Tapez `exit` puis **Entrée**
2. Appuyez sur **Ctrl + D**
3. Cliquez simplement sur le bouton **X** de la fenêtre

---

## Résumé

Le terminal est un outil puissant mais accessible :

- **Ouvrir** : Ctrl + Alt + T (le plus rapide)
- **Le prompt** vous indique où vous êtes et qui vous êtes
- **Tab** pour compléter automatiquement
- **Flèches haut/bas** pour naviguer dans l'historique
- **Ctrl + C** pour interrompre une commande
- **man** ou **--help** pour obtenir de l'aide
- Ne pas avoir peur d'expérimenter !

Dans les prochains chapitres, nous découvrirons les commandes de navigation, de manipulation de fichiers, et bien plus encore. Vous verrez que le terminal deviendra rapidement un allié précieux dans votre utilisation quotidienne de Linux Mint.

**Rappelez-vous :** Même les experts ont commencé par ouvrir un terminal pour la première fois et se sont posé les mêmes questions que vous. L'apprentissage est progressif, et chaque commande apprise est une victoire !

⏭️ [Navigation (cd, ls, pwd, tree)](/07-le-terminal-et-commandes-de-base/02-navigation.md)
