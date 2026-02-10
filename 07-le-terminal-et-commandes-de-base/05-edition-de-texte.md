🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.5 - Édition de texte (nano, vim)

## Introduction

Savoir éditer des fichiers texte directement dans le terminal est une compétence essentielle sous Linux. Que ce soit pour modifier un fichier de configuration, créer un script, ou corriger un bug, vous aurez besoin d'un éditeur de texte en ligne de commande.

**Analogie :** Si `cat` et `less` vous permettent de **lire** un livre, les éditeurs de texte vous permettent de l'**écrire** et de le **modifier**.

### Pourquoi éditer en ligne de commande ?

Vous pourriez vous demander : "Pourquoi ne pas simplement ouvrir un fichier avec un éditeur graphique ?"

**Raisons importantes :**
1. **Serveurs distants** : En SSH, vous n'avez pas d'interface graphique
2. **Fichiers système** : Certains fichiers nécessitent des privilèges administrateur
3. **Rapidité** : Plus rapide que de chercher et lancer une application graphique
4. **Légèreté** : Consomme très peu de ressources
5. **Disponibilité** : Les éditeurs CLI sont présents sur tous les systèmes Linux

### Les deux éditeurs principaux

Dans ce chapitre, nous allons découvrir :

- **nano** : Éditeur simple et intuitif, parfait pour les débutants
- **vim** : Éditeur puissant et très populaire, avec une courbe d'apprentissage plus raide

**Recommandation pour débuter :** Commencez avec **nano**. Une fois à l'aise, explorez **vim** si vous souhaitez plus de puissance et de vitesse.

---

## Nano : L'éditeur convivial pour débutants

### Présentation

**nano** est un éditeur de texte simple, intuitif et facile à utiliser. Il affiche les raccourcis principaux directement à l'écran, vous n'avez donc pas besoin de les mémoriser.

**Points forts :**
- Interface claire avec aide intégrée
- Courbe d'apprentissage quasi nulle
- Parfait pour les modifications rapides
- Idéal pour les débutants

### Ouvrir nano

#### Créer un nouveau fichier

```bash
nano nouveau_fichier.txt
```

Ouvre nano avec un fichier vide.

#### Éditer un fichier existant

```bash
nano fichier_existant.txt
```

Si le fichier existe, nano l'ouvre pour modification.

#### Ouvrir avec privilèges administrateur

```bash
sudo nano /etc/nom_fichier.conf
```

Nécessaire pour éditer les fichiers système.

### Interface de nano

Quand vous ouvrez nano, vous voyez :

```
  GNU nano 6.2              nouveau_fichier.txt

[Votre curseur clignote ici]




^G Aide      ^O Écrire    ^W Où est    ^K Couper    ^T Ortho
^X Quitter   ^R Lire fich ^\ Remplacer ^U Coller    ^J Justifier
```

**Légende :**
- En haut : Titre avec le nom du fichier
- Au milieu : Zone d'édition (votre texte)
- En bas : Raccourcis principaux

**Comprendre les raccourcis :**
- **^** signifie la touche **Ctrl**
- **^X** = **Ctrl + X**
- **M-** signifie la touche **Alt** (Meta)

### Éditer du texte dans nano

#### Écrire du texte

Tapez simplement ! Le curseur se déplace et le texte apparaît.

**Contrairement à vim, nano fonctionne comme un éditeur normal** : vous écrivez directement.

#### Se déplacer dans le texte

| Touche | Action |
|--------|--------|
| **Flèches** | Déplacer le curseur |
| **Page Up/Down** | Page précédente/suivante |
| **Ctrl + A** | Début de la ligne |
| **Ctrl + E** | Fin de la ligne |
| **Ctrl + Y** | Page précédente |
| **Ctrl + V** | Page suivante |
| **Alt + \** | Début du fichier |
| **Alt + /** | Fin du fichier |

#### Sélectionner du texte

1. Placez le curseur au début
2. Appuyez sur **Ctrl + ^** (ou **Alt + A**)
3. Déplacez le curseur pour sélectionner
4. La sélection apparaît en surbrillance

**Annuler la sélection :** **Ctrl + ^** à nouveau

### Opérations de base

#### Couper, copier, coller

| Action | Raccourci |
|--------|-----------|
| **Couper la ligne** | **Ctrl + K** |
| **Copier la ligne** | **Alt + ^** puis **Ctrl + K** |
| **Coller** | **Ctrl + U** |

**Astuce :** Pour couper plusieurs lignes, appuyez plusieurs fois sur **Ctrl + K**. Toutes les lignes coupées sont mises en mémoire.

#### Supprimer du texte

| Action | Raccourci |
|--------|-----------|
| **Supprimer le caractère sous le curseur** | **Del** |
| **Supprimer le caractère avant le curseur** | **Backspace** |
| **Supprimer jusqu'à la fin de la ligne** | **Ctrl + K** |

#### Annuler et rétablir

| Action | Raccourci |
|--------|-----------|
| **Annuler** | **Alt + U** |
| **Rétablir** | **Alt + E** |

**Note :** Les versions récentes de nano supportent l'annulation multiple.

### Rechercher et remplacer

#### Rechercher du texte

1. Appuyez sur **Ctrl + W**
2. Tapez le mot à rechercher
3. Appuyez sur **Entrée**

Le curseur se déplace vers la première occurrence.

**Recherche suivante :** **Ctrl + W** puis **Entrée** (sans retaper le mot)

#### Remplacer du texte

1. Appuyez sur **Ctrl + \\** (antislash)
2. Tapez le texte à rechercher → **Entrée**
3. Tapez le texte de remplacement → **Entrée**
4. Nano demande confirmation pour chaque occurrence :
   - **Y** : Oui, remplacer
   - **N** : Non, passer au suivant
   - **A** : Tout remplacer (All)
   - **Ctrl + C** : Annuler

### Sauvegarder et quitter

#### Sauvegarder (écrire) le fichier

**Ctrl + O** (O comme Output)

Nano demande confirmation du nom de fichier :
- Appuyez sur **Entrée** pour garder le même nom
- Ou tapez un nouveau nom puis **Entrée**

Le message `[ Écrit X lignes ]` confirme la sauvegarde.

#### Quitter nano

**Ctrl + X**

Si vous avez des modifications non sauvegardées, nano demande :
```
Sauver le fichier modifié ? (Répondre « Non » annulera vos changements)
 O Oui
 N Non        ^C Annuler
```

- **O** ou **Y** : Sauvegarder et quitter
- **N** : Quitter sans sauvegarder
- **Ctrl + C** : Annuler, rester dans nano

### Fonctionnalités avancées de nano

#### Numéros de ligne

**Ctrl + C** (ou **Alt + C**)

Affiche/masque les numéros de ligne sur le côté gauche.

Très utile pour repérer une ligne spécifique (par exemple suite à une erreur).

#### Aller à une ligne spécifique

**Ctrl + _** (underscore)

Tapez le numéro de ligne puis **Entrée**.

#### Activer la coloration syntaxique

nano détecte automatiquement le type de fichier et applique la coloration pour :
- Shell scripts (`.sh`)
- Python (`.py`)
- HTML, CSS, JavaScript
- Fichiers de configuration
- Et bien d'autres

**Forcer un type de syntaxe :**
```bash
nano -Y python fichier.txt
```

#### Indentation automatique

**Alt + I**

Active/désactive l'indentation automatique (utile pour la programmation).

#### Voir tous les raccourcis

**Ctrl + G**

Affiche l'aide complète avec tous les raccourcis disponibles.

Pour quitter l'aide : **Ctrl + X**

### Exemples pratiques avec nano

#### Créer un script shell simple

```bash
nano mon_script.sh
```

Tapez :
```bash
#!/bin/bash
echo "Bonjour, monde !"
```

Sauvegardez avec **Ctrl + O** puis **Entrée**, quittez avec **Ctrl + X**.

Rendez-le exécutable :
```bash
chmod +x mon_script.sh
./mon_script.sh
```

#### Éditer un fichier de configuration

```bash
sudo nano /etc/hosts
```

Modifiez le fichier, sauvegardez avec **Ctrl + O**, quittez avec **Ctrl + X**.

#### Créer une note rapide

```bash
nano notes.txt
```

Écrivez vos notes, sauvegardez, c'est fait !

---

## Vim : L'éditeur puissant pour utilisateurs avancés

### Présentation

**vim** (Vi IMproved) est un éditeur de texte extrêmement puissant et populaire parmi les utilisateurs Linux avancés et les programmeurs.

**Points forts :**
- Incroyablement rapide une fois maîtrisé
- Très efficace (jamais besoin de quitter le clavier)
- Disponible sur tous les systèmes Unix/Linux
- Extensions et personnalisation illimitées
- Modes d'édition pour différentes tâches

**Points de difficulté :**
- Courbe d'apprentissage abrupte
- Interface non intuitive au début
- Système de modes déroutant pour les débutants

**Important :** Vous n'êtes pas obligé d'apprendre vim tout de suite ! nano suffit amplement pour débuter. Mais connaître les bases de vim est utile car il est présent partout.

### Ouvrir vim

```bash
vim fichier.txt
```

Ou pour créer un nouveau fichier :
```bash
vim nouveau_fichier.txt
```

### Le concept de modes

**C'est LA particularité de vim :** Il fonctionne avec plusieurs **modes**. C'est ce qui le rend puissant mais déroutant au début.

#### Mode Normal (par défaut)

Quand vous ouvrez vim, vous êtes en **mode Normal**.

**Dans ce mode :**
- Vous **ne pouvez PAS** taper du texte
- Vous utilisez des commandes pour naviguer, copier, coller, etc.
- Les touches du clavier sont des commandes, pas du texte

**C'est le mode de "navigation" et de "commande".**

#### Mode Insertion

Le mode où vous pouvez **écrire du texte**.

**Pour entrer en mode Insertion :**
- Appuyez sur **i** (insert)

**Indicateur :** `-- INSERTION --` apparaît en bas de l'écran.

**Pour revenir au mode Normal :**
- Appuyez sur **Échap** (Escape)

#### Mode Commande

Pour exécuter des commandes complexes (sauvegarder, quitter, rechercher, remplacer).

**Pour entrer en mode Commande :**
- En mode Normal, tapez **:**

Un **:** apparaît en bas de l'écran, vous pouvez alors taper une commande.

#### Mode Visuel

Pour sélectionner du texte.

**Pour entrer en mode Visuel :**
- En mode Normal, appuyez sur **v**

### Premiers pas dans vim

#### 1. Ouvrir un fichier

```bash
vim test.txt
```

Vous êtes en **mode Normal** (l'écran est vide ou affiche le fichier).

#### 2. Passer en mode Insertion

Appuyez sur **i**

Vous voyez `-- INSERTION --` en bas. Vous pouvez maintenant taper du texte.

#### 3. Écrire du texte

Tapez normalement, comme dans n'importe quel éditeur.

#### 4. Revenir au mode Normal

Appuyez sur **Échap**

Le `-- INSERTION --` disparaît.

#### 5. Sauvegarder

En mode Normal, tapez **:w** puis **Entrée**

(w = write)

#### 6. Quitter

En mode Normal, tapez **:q** puis **Entrée**

(q = quit)

#### 7. Sauvegarder et quitter en une commande

**:wq** puis **Entrée**

Ou utilisez le raccourci **:x**

#### 8. Quitter sans sauvegarder

**:q!** puis **Entrée**

Le **!** force l'action en ignorant les modifications.

### La blague classique de vim

**Mème populaire :** "Comment quitter vim ?"

Beaucoup d'utilisateurs se retrouvent piégés dans vim sans savoir comment en sortir !

**La réponse :**
1. Appuyez sur **Échap** (pour être sûr d'être en mode Normal)
2. Tapez **:q!** (quitter sans sauvegarder)
3. Appuyez sur **Entrée**

**Ou pour sauvegarder et quitter :**
1. **Échap**
2. **:wq**
3. **Entrée**

### Navigation en mode Normal

Contrairement à nano, vim utilise les touches du clavier pour se déplacer (vous pouvez aussi utiliser les flèches, mais les puristes utilisent ces touches).

#### Déplacements de base

| Touche | Action |
|--------|--------|
| **h** | ← Gauche |
| **j** | ↓ Bas |
| **k** | ↑ Haut |
| **l** | → Droite |

**Mnémotechnique :** **h** et **l** sont à gauche et droite du clavier, **j** descend visuellement, **k** monte.

**Vous pouvez aussi utiliser les flèches directionnelles.**

#### Déplacements rapides

| Commande | Action |
|----------|--------|
| **w** | Mot suivant (word) |
| **b** | Mot précédent (back) |
| **0** | Début de la ligne |
| **$** | Fin de la ligne |
| **gg** | Début du fichier |
| **G** | Fin du fichier |
| **:n** | Ligne n (ex: `:42` va à la ligne 42) |

#### Défilement

| Commande | Action |
|----------|--------|
| **Ctrl + F** | Page suivante (Forward) |
| **Ctrl + B** | Page précédente (Back) |
| **Ctrl + D** | Demi-page vers le bas (Down) |
| **Ctrl + U** | Demi-page vers le haut (Up) |

### Édition en mode Normal

L'une des forces de vim : éditer sans passer en mode Insertion.

#### Entrer en mode Insertion

| Commande | Action |
|----------|--------|
| **i** | Insérer avant le curseur |
| **a** | Insérer après le curseur (append) |
| **I** | Insérer au début de la ligne |
| **A** | Insérer à la fin de la ligne |
| **o** | Nouvelle ligne en dessous |
| **O** | Nouvelle ligne au-dessus |

#### Supprimer

| Commande | Action |
|----------|--------|
| **x** | Supprimer le caractère sous le curseur |
| **X** | Supprimer le caractère avant le curseur |
| **dd** | Supprimer la ligne entière |
| **dw** | Supprimer jusqu'à la fin du mot |
| **d$** | Supprimer jusqu'à la fin de la ligne |
| **d0** | Supprimer jusqu'au début de la ligne |

**Nombre + Commande :**
- **5dd** : Supprimer 5 lignes
- **3dw** : Supprimer 3 mots

#### Copier et coller (yank and put)

| Commande | Action |
|----------|--------|
| **yy** | Copier la ligne (yank) |
| **yw** | Copier le mot |
| **p** | Coller après le curseur (put) |
| **P** | Coller avant le curseur |

**Exemple :**
1. **yy** : Copier la ligne actuelle
2. **5j** : Descendre de 5 lignes
3. **p** : Coller

#### Annuler et rétablir

| Commande | Action |
|----------|--------|
| **u** | Annuler (undo) |
| **Ctrl + R** | Rétablir (redo) |
| **.** | Répéter la dernière action |

Le point **.** est très puissant : il répète votre dernière modification.

### Recherche et remplacement

#### Rechercher

**En mode Normal :**

| Commande | Action |
|----------|--------|
| **/mot** | Rechercher "mot" vers le bas |
| **?mot** | Rechercher "mot" vers le haut |
| **n** | Occurrence suivante |
| **N** | Occurrence précédente |

**Exemple :**
1. Tapez **/erreur**
2. Appuyez sur **Entrée**
3. vim saute à la première occurrence
4. Appuyez sur **n** pour la suivante

#### Remplacer

**En mode Commande :**

```vim
:s/ancien/nouveau/        " Remplace sur la ligne actuelle
:s/ancien/nouveau/g       " Remplace toutes les occurrences de la ligne (global)
:%s/ancien/nouveau/g      " Remplace dans tout le fichier
:%s/ancien/nouveau/gc     " Avec confirmation (c = confirm)
```

**Exemple :**
```vim
:%s/erreur/avertissement/g
```

Remplace tous les "erreur" par "avertissement" dans le fichier.

### Mode Visuel : Sélection

#### Entrer en mode Visuel

| Commande | Action |
|----------|--------|
| **v** | Mode visuel (caractère par caractère) |
| **V** | Mode visuel ligne (ligne entière) |
| **Ctrl + V** | Mode visuel bloc (rectangle) |

#### Utilisation

1. Appuyez sur **v**
2. Déplacez le curseur pour sélectionner
3. Appuyez sur une commande :
   - **d** : Supprimer
   - **y** : Copier
   - **>** : Indenter à droite
   - **<** : Indenter à gauche

**Exemple :**
1. **V** (mode visuel ligne)
2. **5j** (sélectionner 5 lignes vers le bas)
3. **d** (supprimer)

### Commandes utiles en mode Commande

#### Sauvegarder et quitter

| Commande | Action |
|----------|--------|
| **:w** | Sauvegarder (write) |
| **:w nom_fichier** | Sauvegarder sous un nouveau nom |
| **:q** | Quitter |
| **:q!** | Quitter sans sauvegarder (force) |
| **:wq** | Sauvegarder et quitter |
| **:x** | Sauvegarder et quitter (équivalent) |
| **ZZ** | Sauvegarder et quitter (en mode Normal) |
| **ZQ** | Quitter sans sauvegarder (en mode Normal) |

#### Affichage

| Commande | Action |
|----------|--------|
| **:set number** | Afficher les numéros de ligne |
| **:set nonumber** | Masquer les numéros de ligne |
| **:set nu** | Forme courte de number |
| **:syntax on** | Activer la coloration syntaxique |
| **:set hlsearch** | Surligner les recherches |

#### Aide

| Commande | Action |
|----------|--------|
| **:help** | Aide générale |
| **:help commande** | Aide sur une commande spécifique |
| **:q** | Quitter l'aide |

### Configuration de vim

Vous pouvez personnaliser vim en créant un fichier `~/.vimrc` :

```bash
nano ~/.vimrc
```

**Exemple de configuration pour débutants :**

```vim
" Activer la numérotation des lignes
set number

" Activer la coloration syntaxique
syntax on

" Activer l'indentation automatique
set autoindent  
set smartindent  

" Afficher la ligne du curseur
set cursorline

" Recherche incrémentale
set incsearch

" Surligner les résultats de recherche
set hlsearch

" Utiliser les espaces au lieu des tabulations
set expandtab  
set tabstop=4  
set shiftwidth=4  

" Afficher la position du curseur
set ruler

" Ne pas créer de fichiers de sauvegarde
set nobackup  
set noswapfile  
```

Sauvegardez et fermez. La prochaine fois que vous ouvrez vim, ces paramètres seront actifs.

---

## Comparaison nano vs vim

### Tableau comparatif

| Critère | nano | vim |
|---------|------|-----|
| **Facilité d'apprentissage** | ⭐⭐⭐⭐⭐ Très facile | ⭐⭐ Difficile au début |
| **Interface** | Intuitive, aide visible | Nécessite mémorisation |
| **Rapidité d'utilisation** | Moyenne | Très rapide (une fois maîtrisé) |
| **Puissance** | Basique | Extrêmement puissante |
| **Disponibilité** | Pas toujours pré-installé | Presque toujours présent |
| **Usage recommandé** | Débutants, modifications rapides | Utilisateurs avancés, développeurs |

### Quand utiliser nano ?

- ✅ Vous débutez avec Linux
- ✅ Modification rapide d'un fichier de configuration
- ✅ Vous ne voulez pas mémoriser de commandes
- ✅ Édition occasionnelle de fichiers texte
- ✅ Vous préférez la simplicité

### Quand utiliser vim ?

- ✅ Vous éditez beaucoup de code
- ✅ Vous voulez maximiser votre productivité
- ✅ Vous travaillez souvent sur des serveurs distants
- ✅ Vous aimez la puissance et l'efficacité
- ✅ Vous êtes prêt à investir du temps pour apprendre

### Utilisation combinée

**Beaucoup d'utilisateurs utilisent les deux !**
- **nano** pour les modifications rapides et simples
- **vim** pour les sessions d'édition longues et complexes

---

## Autres éditeurs (mentions rapides)

### vi (l'ancêtre de vim)

**vi** est l'éditeur original dont vim est dérivé.

```bash
vi fichier.txt
```

**Différence :** vim a plus de fonctionnalités. Si vim n'est pas disponible, vi le sera probablement.

### emacs

**emacs** est un autre éditeur très puissant, rival historique de vim.

```bash
emacs fichier.txt
```

**Caractéristiques :**
- Extensible à l'extrême
- Système de raccourcis différent de vim
- Communauté très active

**Guerre d'éditeurs :** Il existe une rivalité amicale entre utilisateurs de vim et emacs. Les deux sont excellents !

### micro

**micro** est un éditeur moderne, simple, avec des raccourcis intuitifs (Ctrl+C, Ctrl+V, etc.).

**Installation :**
```bash
sudo apt install micro
```

**Utilisation :**
```bash
micro fichier.txt
```

**Points forts :**
- Plus moderne que nano
- Raccourcis standards (Ctrl+C, Ctrl+V, Ctrl+Z)
- Support de la souris
- Plugins disponibles

---

## Exemples pratiques courants

### Exemple 1 : Éditer un fichier de configuration système

#### Avec nano

```bash
sudo nano /etc/ssh/sshd_config
```

1. Utilisez les flèches pour naviguer
2. Modifiez le texte directement
3. **Ctrl + O** pour sauvegarder
4. **Ctrl + X** pour quitter

#### Avec vim

```bash
sudo vim /etc/ssh/sshd_config
```

1. Appuyez sur **/** puis tapez le texte à chercher
2. Appuyez sur **i** pour passer en mode Insertion
3. Modifiez le texte
4. Appuyez sur **Échap**
5. Tapez **:wq** pour sauvegarder et quitter

### Exemple 2 : Créer un script shell

#### Avec nano

```bash
nano backup.sh
```

Tapez :
```bash
#!/bin/bash
# Script de sauvegarde

echo "Démarrage de la sauvegarde..."  
tar -czf backup_$(date +%Y%m%d).tar.gz ~/Documents  
echo "Sauvegarde terminée !"  
```

**Ctrl + O**, **Entrée**, **Ctrl + X**

#### Avec vim

```bash
vim backup.sh
```

1. **i** (mode Insertion)
2. Tapez le script
3. **Échap**
4. **:wq**

### Exemple 3 : Rechercher et remplacer dans un fichier

#### Avec nano

```bash
nano config.txt
```

1. **Ctrl + \\**
2. Tapez "ancien_mot"
3. **Entrée**
4. Tapez "nouveau_mot"
5. **Entrée**
6. **A** pour tout remplacer

#### Avec vim

```bash
vim config.txt
```

1. En mode Normal
2. **:%s/ancien_mot/nouveau_mot/g**
3. **Entrée**
4. **:wq**

---

## Astuces et bonnes pratiques

### Pour nano

#### 1. Créer des sauvegardes automatiques

```bash
nano -B fichier.txt
```

Crée une sauvegarde avec le suffixe `~`.

#### 2. Ouvrir à une ligne spécifique

```bash
nano +42 fichier.txt
```

Ouvre le fichier directement à la ligne 42.

#### 3. Activer la souris

```bash
nano -m fichier.txt
```

Vous pouvez cliquer pour placer le curseur.

#### 4. Mode lecture seule

```bash
nano -v fichier.txt
```

Empêche les modifications accidentelles.

### Pour vim

#### 1. Ouvrir plusieurs fichiers

```bash
vim fichier1.txt fichier2.txt fichier3.txt
```

**Naviguer entre les fichiers :**
- **:n** : Fichier suivant
- **:prev** : Fichier précédent
- **:buffers** : Liste des fichiers ouverts

#### 2. Diviser l'écran

```vim
:split fichier2.txt    " Division horizontale
:vsplit fichier2.txt   " Division verticale
```

**Naviguer entre les fenêtres :**
- **Ctrl + W** puis flèche

#### 3. Enregistrer une macro

1. **q** puis une lettre (ex: **qa** pour enregistrer dans 'a')
2. Effectuez vos actions
3. **q** pour arrêter l'enregistrement
4. **@a** pour rejouer la macro

#### 4. Mode diff

```bash
vim -d fichier1.txt fichier2.txt
```

Compare deux fichiers côte à côte.

#### 5. Récupération après un crash

Si vim crash, il crée un fichier de swap. Au prochain démarrage :

```
Swap file ".fichier.txt.swp" already exists!
[O]pen Read-Only, (E)dit anyway, (R)ecover, (D)elete it, (Q)uit, (A)bort:
```

**Choisissez R pour récupérer.**

---

## Erreurs courantes et solutions

### Erreur 1 : Bloqué en mode Insertion dans vim

**Symptôme :** Vous tapez des commandes mais rien ne se passe, ou le texte s'affiche bizarrement.

**Solution :**
Appuyez sur **Échap** plusieurs fois pour revenir au mode Normal.

### Erreur 2 : Cannot write file (permission denied)

**Problème :**
```
"fichier.txt" E212: Can't open file for writing
```

**Solution :**
Vous n'avez pas les permissions. Quittez et rouvrez avec `sudo` :

```bash
sudo nano fichier.txt
# ou
sudo vim fichier.txt
```

**Dans vim, si vous avez déjà fait des modifications :**
```vim
:w !sudo tee %
```

Cette commande sauvegarde avec les privilèges sudo.

### Erreur 3 : Le terminal affiche des caractères bizarres (nano)

**Problème :** Après avoir édité un fichier binaire avec nano.

**Solution :**
```bash
reset
```

Réinitialise le terminal.

**Prévention :** Ne jamais ouvrir de fichiers binaires avec des éditeurs de texte.

### Erreur 4 : Modifications non sauvegardées dans vim

**Symptôme :**
```
E37: No write since last change (add ! to override)
```

**Cause :** Vous essayez de quitter sans sauvegarder.

**Solutions :**
- **:wq** : Sauvegarder et quitter
- **:q!** : Quitter sans sauvegarder (perd les modifications)

### Erreur 5 : Fichier en lecture seule

**Dans nano :**
Le message `[ Erreur d'écriture : Permission non accordée ]` apparaît.

**Dans vim :**
```
E45: 'readonly' option is set (add ! to override)
```

**Solution :**
Rouvrez avec `sudo`.

---

## Ressources pour progresser

### Pour nano

La documentation est simple, les raccourcis sont affichés à l'écran. Vous êtes déjà prêt !

**Aide intégrée :**
```bash
nano --help  
man nano  
```

### Pour vim

#### Tutoriel intégré : vimtutor

```bash
vimtutor
```

Lance un tutoriel interactif de 30 minutes qui vous enseigne les bases de vim.

**C'est LA meilleure façon d'apprendre vim !**

#### Antisèches (cheat sheets)

Cherchez "vim cheat sheet" sur Google pour des aide-mémoires visuels.

#### Jeux pour apprendre vim

- **vim-adventures.com** : Jeu pour apprendre vim en s'amusant
- **openvim.com** : Tutoriel interactif en ligne

#### Livres et ressources

- **Practical Vim** par Drew Neil
- **Learning the vi and Vim Editors** par Arnold Robbins
- Documentation officielle : `:help` dans vim

---

## Résumé

### nano : L'éditeur pour débutants

**Commandes essentielles :**
- Ouvrir : `nano fichier.txt`
- Écrire du texte : Tapez directement
- Sauvegarder : **Ctrl + O**
- Quitter : **Ctrl + X**
- Rechercher : **Ctrl + W**
- Remplacer : **Ctrl + \\**
- Aide : **Ctrl + G**

**Parfait pour :** Modifications rapides, débutants, simplicité

### vim : L'éditeur puissant

**Commandes essentielles :**
- Ouvrir : `vim fichier.txt`
- Mode Insertion : **i**
- Mode Normal : **Échap**
- Sauvegarder : **:w**
- Quitter : **:q**
- Sauvegarder et quitter : **:wq**
- Quitter sans sauvegarder : **:q!**
- Annuler : **u**
- Rechercher : **/mot**

**Parfait pour :** Édition intensive, productivité, utilisateurs avancés

### Conseil final

**Commencez avec nano.** C'est parfait pour débuter et couvre 90% des besoins d'édition quotidienne.

**Explorez vim progressivement.** Lancez `vimtutor` et consacrez 30 minutes à apprendre les bases. Même si vous ne l'utilisez pas tout de suite, savoir quitter vim et faire des modifications simples est une compétence précieuse.

**N'ayez pas peur de tester les deux !** L'expérimentation est la meilleure façon d'apprendre. Créez des fichiers de test et jouez avec les commandes.

Dans le prochain chapitre, nous découvrirons les permissions et propriétés des fichiers, un concept fondamental de la sécurité Linux.

⏭️ [Permissions et propriétés (chmod, chown, ls -l)](/07-le-terminal-et-commandes-de-base/06-permissions-et-proprietes.md)
