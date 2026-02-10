🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Lecteur d'écran (Orca)

## Introduction

Orca est le lecteur d'écran gratuit et open source intégré à Linux Mint. Il permet aux personnes aveugles ou malvoyantes d'utiliser l'ordinateur en vocalisant le contenu affiché à l'écran et en proposant une navigation au clavier complète.

Orca peut lire à voix haute :
- Le texte affiché à l'écran
- Les menus et boutons
- Les pages web
- Les documents
- Les messages système

Il fonctionne avec un synthétiseur vocal et peut également afficher le texte en braille sur un périphérique braille compatible.

---

## Installation d'Orca

Orca n'est pas toujours installé par défaut sur Linux Mint. Voici comment l'installer :

### Méthode 1 : Via le gestionnaire de logiciels

1. **Ouvrir le Menu principal**
2. **Rechercher "Gestionnaire de logiciels"**
3. Dans la barre de recherche, taper **"orca"**
4. Cliquer sur **"Orca"** dans les résultats
5. Cliquer sur **"Installer"**
6. Entrer votre mot de passe administrateur

### Méthode 2 : Via le terminal

Si vous êtes à l'aise avec le terminal, ouvrez-le et tapez :

```bash
sudo apt update  
sudo apt install orca gnome-orca  
```

**Note :** `gnome-orca` contient des composants supplémentaires utiles pour Orca.

### Installation du synthétiseur vocal

Orca a besoin d'un synthétiseur vocal pour fonctionner. Le plus courant est **eSpeak-NG** :

```bash
sudo apt install espeak-ng
```

Pour une voix française de meilleure qualité, vous pouvez installer **MBROLA** :

```bash
sudo apt install mbrola mbrola-fr1 mbrola-fr4
```

---

## Activer Orca au démarrage

Pour que Orca se lance automatiquement dès le démarrage de Linux Mint :

1. **Ouvrir les Paramètres système**
2. **Aller dans "Accessibilité"**
3. Cocher **"Activer le lecteur d'écran"** ou **"Lancer Orca au démarrage"**

**Alternative via les applications au démarrage :**

1. **Menu → Préférences → Applications au démarrage**
2. Cliquer sur **"Ajouter"**
3. **Nom :** Orca
4. **Commande :** `orca`
5. Cliquer sur **"Ajouter"**

---

## Démarrer et arrêter Orca

### Démarrer Orca

**Méthode 1 : Raccourci clavier universel**
- Appuyez simultanément sur : **Super + Alt + S** (la touche Super est souvent la touche Windows)

**Méthode 2 : Depuis le menu**
- Menu → Applications → Accessibilité → Orca

**Méthode 3 : Depuis le terminal**
```bash
orca
```

### Arrêter Orca

- Appuyez sur : **Insert + Q** (puis confirmer avec Entrée)
- Ou : **Super + Alt + S** (pour basculer)

**Note :** La touche **Insert** est aussi appelée **Inser** ou **Ins** selon les claviers. Sur certains ordinateurs portables, elle peut nécessiter l'utilisation de la touche **Fn**.

---

## Première configuration d'Orca

Lors du premier lancement, Orca vous propose un assistant de configuration. Voici les étapes principales :

### 1. Choix du mode clavier

Orca vous demande de choisir entre deux modes :

- **Mode ordinateur de bureau** : Utilise la touche Insert comme modificateur
- **Mode ordinateur portable** : Utilise **CapsLock** comme modificateur (plus accessible sur les claviers sans pavé numérique)

**Recommandation pour débutants :** Choisissez le mode ordinateur portable si vous n'avez pas de touche Insert facilement accessible.

### 2. Choix de la voix

Orca vous permet de sélectionner :
- Le **synthétiseur vocal** (eSpeak-NG recommandé)
- La **langue** (français)
- Le **débit de parole** (vitesse de lecture)
- Le **volume**
- La **hauteur de la voix**

### 3. Écho clavier

Orca peut lire ce que vous tapez. Vous pouvez choisir :
- **Lire chaque caractère** : Orca dit chaque lettre que vous tapez
- **Lire chaque mot** : Orca lit le mot complet quand vous appuyez sur Espace
- **Lire les deux**
- **Ne rien lire**

**Recommandation :** Commencez par "Lire chaque mot" pour ne pas être submergé.

### 4. Ponctuations et majuscules

- Vous pouvez choisir le niveau de verbalisation de la ponctuation
- Activer ou non l'annonce des majuscules

---

## Touche modificateur Orca

La **touche modificateur Orca** est essentielle pour utiliser Orca. C'est avec elle que vous accéderez à toutes les fonctions d'Orca.

Par défaut :
- **Mode bureau :** Touche **Insert**
- **Mode portable :** Touche **CapsLock** (Verrouillage majuscule)

Dans ce tutoriel, nous utiliserons la notation **Orca** pour désigner cette touche modificateur.

---

## Raccourcis clavier essentiels

### Navigation de base

| Raccourci | Action |
|-----------|--------|
| **Orca + Espace** | Lire l'élément actuel |
| **Orca + ;** | Lire toute la fenêtre |
| **Orca + H** | Passer en mode navigation web (dans un navigateur) |
| **Orca + A** | Lire les attributs de l'élément (couleur, police, etc.) |

### Lecture du texte

| Raccourci | Action |
|-----------|--------|
| **Orca + Pavé Num. +** | Lire à partir du curseur jusqu'à la fin |
| **Orca + Pavé Num. Entrée** | Où suis-je ? (contexte actuel) |
| **Orca + T** | Lire le titre de la fenêtre |
| **Orca + F** | Lire les informations de la police |

### Navigation par élément

| Raccourci | Action |
|-----------|--------|
| **Flèches directionnelles** | Se déplacer dans les menus et listes |
| **Tab** / **Maj + Tab** | Aller à l'élément suivant/précédent |
| **Orca + Flèche haut/bas** | Lire ligne précédente/suivante |
| **Orca + Flèche gauche/droite** | Lire mot précédent/suivant |

### Contrôle de la parole

| Raccourci | Action |
|-----------|--------|
| **Ctrl** | Interrompre immédiatement la lecture |
| **Orca + S** | Paramètres de la parole (vitesse, volume) |
| **Orca + [** | Diminuer le débit |
| **Orca + ]** | Augmenter le débit |

### Configuration et aide

| Raccourci | Action |
|-----------|--------|
| **Orca + Espace** (double-clic rapide) | Ouvrir les préférences d'Orca |
| **Orca + Q** | Quitter Orca |
| **Orca + ?** | Passer en mode d'apprentissage (apprendre les raccourcis) |

---

## Navigation sur le Web avec Orca

Orca offre des fonctionnalités spéciales pour naviguer sur les pages web dans Firefox ou Chrome.

### Activer le mode navigation web

Dans le navigateur, appuyez sur **Orca + H** pour activer le mode navigation web.

### Touches de navigation rapide

Ces touches permettent de sauter directement à certains types d'éléments :

| Touche | Élément |
|--------|---------|
| **H** | Titre (Heading) - H1, H2, H3, etc. |
| **L** | Liste |
| **K** | Lien |
| **B** | Bouton |
| **E** | Champ de saisie (Entry) |
| **T** | Tableau |
| **F** | Formulaire |
| **M** | Point de repère (Landmark) |

**Astuce :** Appuyez sur **Maj + touche** pour aller à l'élément précédent (par exemple, **Maj + H** pour le titre précédent).

### Liste des éléments

- **Orca + F7** : Afficher la liste de tous les liens de la page
- **Orca + F5** : Afficher la liste de tous les formulaires
- **Orca + F6** : Afficher la liste de tous les titres

### Mode formulaire

Dans un formulaire web :
- **Orca + A** : Basculer en mode formulaire (pour saisir du texte sans que les touches de navigation rapide n'interfèrent)

---

## Lecture de documents

### Dans un éditeur de texte ou un document

| Raccourci | Action |
|-----------|--------|
| **Orca + Pavé Num. +** | Lire du curseur à la fin du document |
| **Orca + Pavé Num. -** | Lire la ligne actuelle |
| **Pavé Num. 7** | Lire le mot précédent |
| **Pavé Num. 9** | Lire le mot suivant |
| **Pavé Num. 4** | Lire le caractère précédent |
| **Pavé Num. 6** | Lire le caractère suivant |

### Épeler

- **Orca + E** : Épeler le mot actuel
- **Orca + E** (double-clic rapide) : Épeler phonétiquement (A comme Alpha, B comme Bravo, etc.)

---

## Configuration avancée d'Orca

Pour accéder aux paramètres détaillés d'Orca :

1. Appuyez sur **Orca + Espace** (deux fois rapidement)
2. Ou lancez : `orca -s` dans le terminal

### Options importantes à connaître

#### 1. Onglet Général
- **Synthétiseur vocal** : Choisir eSpeak-NG, Festival, ou autre
- **Démarrer Orca au lancement** : Pour que Orca se lance automatiquement
- **Quitter Orca à la fermeture** : Comportement à la fermeture de la fenêtre de préférences

#### 2. Onglet Voix
- **Voix par défaut** : Choisir la voix française
- **Débit** : Vitesse de lecture (0-100, recommandé : 50-70 pour débuter)
- **Volume** : Niveau sonore (0-100)
- **Hauteur** : Grave ou aigu

**Astuce :** Vous pouvez définir différentes voix pour différents types de texte (liens, titres, etc.).

#### 3. Onglet Parole
- **Verbalisation de la ponctuation** : Aucune / Quelques-unes / La plupart / Toutes
- **Niveau de verbalisation** : Détaillé ou concis
- **Lire les numéros de ligne** : Utile pour la programmation
- **Dire "vide"** : Annoncer les lignes vides

#### 4. Onglet Braille
- Si vous utilisez un afficheur braille, configurez-le ici
- Choisissez le type d'afficheur
- Activez ou désactivez le braille

#### 5. Onglet Écho clavier
- **Activer l'écho par mot** : Lire chaque mot après l'avoir tapé
- **Activer l'écho par touche** : Lire chaque caractère
- **Activer les touches d'action** : Annoncer Entrée, Retour arrière, etc.
- **Activer les touches modificatrices** : Annoncer Ctrl, Alt, Maj

#### 6. Onglet Applications spécifiques
- Orca peut avoir des paramètres différents pour chaque application
- Utile pour adapter le comportement dans Firefox, LibreOffice, etc.

---

## Astuces pour débuter avec Orca

### 1. Mode d'apprentissage

Le mode d'apprentissage est parfait pour découvrir les raccourcis :

- Appuyez sur **Orca + H** pour entrer en mode d'apprentissage
- Appuyez ensuite sur n'importe quelle touche pour entendre sa fonction
- Appuyez à nouveau sur **Orca + H** pour quitter ce mode

### 2. Où suis-je ?

Si vous êtes perdu :
- **Orca + Pavé Num. Entrée** : Orca vous dit où vous êtes (fenêtre, position dans la page, etc.)
- Appuyez deux fois rapidement pour plus de détails

### 3. Ajuster le débit de parole

Au début, commencez avec un débit lent :
- **Orca + [** : Diminuer progressivement
- **Orca + ]** : Augmenter progressivement

Avec le temps, vous pourrez augmenter la vitesse pour gagner en productivité.

### 4. Désactiver temporairement Orca

Si vous avez besoin de silence momentané sans quitter Orca :
- **Orca + S** puis **Muet** : Désactive la voix
- Répétez pour réactiver

---

## Problèmes courants et solutions

### Orca ne parle pas

**Solutions :**
1. Vérifier que le volume système n'est pas à zéro
2. Vérifier qu'un synthétiseur vocal est installé :
   ```bash
   sudo apt install espeak-ng
   ```
3. Relancer Orca : **Orca + Q** puis relancer

### La voix est en anglais

1. Ouvrir les préférences Orca : **Orca + Espace** (double-clic)
2. Onglet **Voix**
3. Sélectionner une voix française (fr ou fr-FR)
4. Si aucune voix française n'apparaît, installer :
   ```bash
   sudo apt install espeak-ng-data
   ```

### Orca lit trop ou pas assez de détails

1. **Orca + V** : Changer le niveau de verbosité (détaillé, moyen, bref)
2. Ou dans les préférences → **Parole** → ajuster le niveau de verbalisation

### Conflit avec la touche CapsLock

Si vous utilisez souvent le verrouillage majuscule :
- Basculez en mode bureau (touche Insert comme modificateur)
- Ou personnalisez la touche modificateur dans les préférences

### Orca ralentit l'ordinateur

1. Réduire le niveau de détail de la verbalisation
2. Désactiver les options non essentielles dans les préférences
3. Fermer les applications inutiles

---

## Orca et LibreOffice

Orca fonctionne très bien avec LibreOffice. Voici quelques raccourcis utiles :

| Raccourci | Action |
|-----------|--------|
| **Orca + Tab** | Lire la ligne actuelle avec mise en forme |
| **Orca + Flèche haut/bas** | Lire la phrase précédente/suivante |
| **Orca + Pavé Num. 5** | Lire le mot sous le curseur |

Dans un tableau :
- **Ctrl + Alt + Flèches** : Se déplacer dans les cellules
- Orca annonce automatiquement les en-têtes de colonnes et lignes

---

## Orca et le terminal

Orca peut lire le contenu du terminal, ce qui est très utile pour les utilisateurs avancés.

**Astuce :**
- **Orca + F** : Rechercher du texte dans le terminal
- Le texte défile souvent vite, utilisez **Ctrl** pour interrompre la lecture

---

## Ressources complémentaires

### Améliorer la qualité de la voix

Pour une voix française de meilleure qualité, vous pouvez installer **Pico TTS** :

```bash
sudo apt install libttspico-utils
```

Ou utiliser **Festival** avec des voix françaises :

```bash
sudo apt install festival festvox-frenchfr
```

### Documentation officielle

- **Wiki Orca** : [https://help.gnome.org/users/orca/stable/](https://help.gnome.org/users/orca/stable/)
- **Liste des raccourcis complète** : Accessible dans Orca via **Orca + H** (mode apprentissage)

### Communauté

- **Forums Linux Mint** : Section accessibilité
- **Liste de diffusion Orca** : Pour des questions avancées

---

## Conseils pour bien débuter

1. **Prenez votre temps** : Orca a beaucoup de fonctionnalités, n'essayez pas de tout apprendre d'un coup
2. **Commencez simple** : Maîtrisez d'abord la navigation de base avant d'explorer les options avancées
3. **Utilisez le mode apprentissage** : C'est le meilleur moyen de découvrir les raccourcis
4. **Ajustez la vitesse progressivement** : Commencez lentement, vous accélérerez avec l'expérience
5. **Personnalisez** : Les paramètres par défaut ne conviennent pas à tout le monde, n'hésitez pas à les adapter
6. **Pratiquez régulièrement** : Comme pour toute nouvelle compétence, la pratique est essentielle

---

## Alternatives à Orca

Bien qu'Orca soit le lecteur d'écran le plus populaire sous Linux, il existe quelques alternatives :

- **BRLTTY** : Spécialisé dans le support braille
- **edbrowse** : Navigateur web en ligne de commande avec synthèse vocale
- **Emacspeak** : Pour les utilisateurs d'Emacs

**Recommandation :** Pour la plupart des utilisateurs, Orca reste le choix le plus complet et le mieux intégré.

---

## Conclusion

Orca est un outil puissant qui rend Linux Mint accessible aux personnes aveugles ou malvoyantes. Bien qu'il puisse sembler complexe au début, avec de la pratique, il devient un compagnon indispensable pour une utilisation autonome de l'ordinateur.

N'oubliez pas que l'accessibilité est un processus continu : n'hésitez pas à explorer, expérimenter et adapter Orca à vos besoins spécifiques. La communauté Linux Mint et Orca est là pour vous aider en cas de besoin.

**Rappel important :** Le raccourci universel pour activer/désactiver Orca est **Super + Alt + S**. Gardez-le en mémoire !

⏭️ [Agrandissement et contraste élevé](/22-accessibilite/03-agrandissement-et-contraste-eleve.md)
