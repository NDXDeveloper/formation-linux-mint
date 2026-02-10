🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 11.1 Création et gestion des comptes utilisateurs

## Introduction

Sous Linux Mint, comme sur tous les systèmes d'exploitation modernes, la gestion des utilisateurs est un élément fondamental de la sécurité et de l'organisation du système. Chaque personne utilisant votre ordinateur peut avoir son propre compte avec ses paramètres personnalisés, ses fichiers privés et ses droits d'accès spécifiques.

### Pourquoi créer plusieurs comptes utilisateurs ?

- **Sécurité** : Isoler les activités de chaque utilisateur et limiter les risques en cas de compromission
- **Confidentialité** : Chaque utilisateur dispose de son espace personnel protégé
- **Personnalisation** : Chacun peut avoir ses propres réglages, thèmes et préférences
- **Organisation** : Séparer clairement les usages (travail, personnel, enfants, invités)

---

## Les types de comptes utilisateurs

### Compte administrateur

Un compte administrateur possède des **privilèges élevés** qui lui permettent de :
- Installer et désinstaller des logiciels
- Modifier les paramètres système
- Créer et gérer d'autres comptes utilisateurs
- Accéder aux fichiers système sensibles (avec `sudo`)
- Effectuer des mises à jour système

> **Important** : Le premier compte créé lors de l'installation de Linux Mint est automatiquement un compte administrateur.

### Compte utilisateur standard

Un compte utilisateur standard est **limité** dans ses actions :
- Il peut utiliser les logiciels déjà installés
- Il peut gérer ses propres fichiers et dossiers personnels
- Il ne peut pas installer de logiciels ni modifier les paramètres système
- Il ne peut pas accéder aux fichiers des autres utilisateurs

> **Conseil de sécurité** : Pour un usage quotidien, il est recommandé d'utiliser un compte standard plutôt qu'un compte administrateur, afin de limiter les risques en cas d'erreur ou d'attaque.

### Compte invité (optionnel)

Certaines configurations permettent de créer un compte invité temporaire :
- Aucun fichier n'est conservé après déconnexion
- Accès très limité au système
- Idéal pour prêter temporairement l'ordinateur

---

## Créer un compte utilisateur (méthode graphique)

La méthode la plus simple pour les débutants est d'utiliser l'interface graphique de Linux Mint.

### Étape 1 : Ouvrir le gestionnaire d'utilisateurs

1. Cliquez sur le **Menu principal** (en bas à gauche)
2. Allez dans **Paramètres système**
3. Cliquez sur **Comptes utilisateurs** (ou **Utilisateurs et groupes**)

Vous pouvez également rechercher "Utilisateurs" dans le menu.

### Étape 2 : Déverrouiller les modifications

- Dans la fenêtre qui s'ouvre, cliquez sur le cadenas **"Déverrouiller"** en haut à droite
- Entrez votre **mot de passe administrateur**
- Le cadenas s'ouvre : vous pouvez maintenant modifier les comptes

### Étape 3 : Ajouter un nouvel utilisateur

1. Cliquez sur le bouton **"+"** ou **"Ajouter un utilisateur"**
2. Une fenêtre s'affiche avec plusieurs champs à remplir :

#### Informations de base

- **Nom complet** : Le nom d'affichage de l'utilisateur (exemple : "Sophie Martin")
- **Nom d'utilisateur** : L'identifiant de connexion, en minuscules sans espaces (exemple : "sophie" ou "smartin")
  - Évitez les caractères spéciaux et les accents
  - Choisissez un nom court et facile à retenir

#### Type de compte

- **Compte standard** : Pour un utilisateur normal
- **Administrateur** : Pour quelqu'un qui doit gérer le système

> **Astuce** : Par défaut, sélectionnez "Compte standard". Vous pourrez toujours changer ce paramètre plus tard si nécessaire.

#### Mot de passe

Vous avez deux options :

1. **Définir un mot de passe maintenant**
   - Entrez le mot de passe deux fois pour confirmation
   - Choisissez un mot de passe sécurisé (voir section "Bonnes pratiques")

2. **Permettre à l'utilisateur de définir son mot de passe à la première connexion**
   - Option pratique pour que chaque personne choisisse son propre mot de passe
   - Cochez la case "L'utilisateur doit changer son mot de passe à la prochaine connexion"

### Étape 4 : Valider la création

- Cliquez sur **"Ajouter"** ou **"Créer le compte"**
- Le nouveau compte apparaît dans la liste des utilisateurs
- N'oubliez pas de **reverrouiller** en cliquant à nouveau sur le cadenas

---

## Créer un compte utilisateur (ligne de commande)

Pour les utilisateurs plus avancés ou pour automatiser la création de comptes, le terminal offre des commandes puissantes.

### Commande adduser (recommandée pour débutants)

La commande `adduser` est interactive et conviviale :

```bash
sudo adduser sophie
```

Le système vous demandera :
1. Le mot de passe (à saisir deux fois)
2. Informations complémentaires (nom complet, numéro de bureau, etc.) - **optionnelles**, vous pouvez appuyer sur Entrée pour ignorer
3. Confirmation finale

### Commande useradd (plus technique)

La commande `useradd` offre plus de contrôle mais nécessite plus d'options :

```bash
sudo useradd -m -s /bin/bash -c "Sophie Martin" sophie
```

Explication des options :
- `-m` : Crée le répertoire personnel (/home/sophie)
- `-s /bin/bash` : Définit bash comme shell par défaut
- `-c "Sophie Martin"` : Ajoute un commentaire (nom complet)

Puis définir le mot de passe :

```bash
sudo passwd sophie
```

### Ajouter un utilisateur au groupe sudo (administrateur)

Si vous souhaitez donner des droits administrateur à un utilisateur :

```bash
sudo usermod -aG sudo sophie
```

> **Note** : L'utilisateur devra se déconnecter et se reconnecter pour que les changements prennent effet.

---

## Modifier un compte utilisateur existant

### Modifier via l'interface graphique

1. Ouvrez **Comptes utilisateurs** depuis les Paramètres système
2. **Déverrouillez** les modifications
3. Sélectionnez l'utilisateur à modifier dans la liste
4. Vous pouvez maintenant :
   - **Changer le type de compte** (Standard ↔ Administrateur)
   - **Modifier le mot de passe** en cliquant sur les points noirs
   - **Changer le nom complet**
   - **Activer ou désactiver le compte** (sans le supprimer)

### Changer le mot de passe d'un utilisateur

#### Pour votre propre compte :

Via l'interface graphique dans **Comptes utilisateurs**, ou en ligne de commande :

```bash
passwd
```

#### Pour un autre utilisateur (nécessite les droits administrateur) :

```bash
sudo passwd sophie
```

### Changer le nom d'utilisateur

**Attention** : Cette opération est délicate et nécessite que l'utilisateur soit déconnecté.

1. Connectez-vous avec un autre compte administrateur
2. Ouvrez un terminal et tapez :

```bash
sudo usermod -l nouveau_nom ancien_nom  
sudo usermod -d /home/nouveau_nom -m nouveau_nom  
```

Exemple :
```bash
sudo usermod -l smartin sophie  
sudo usermod -d /home/smartin -m smartin  
```

### Verrouiller/déverrouiller temporairement un compte

Utile pour désactiver temporairement un accès sans supprimer le compte :

```bash
# Verrouiller le compte
sudo usermod -L sophie

# Déverrouiller le compte
sudo usermod -U sophie
```

---

## Supprimer un compte utilisateur

### Méthode graphique

1. Ouvrez **Comptes utilisateurs**
2. **Déverrouillez** les modifications
3. Sélectionnez l'utilisateur à supprimer
4. Cliquez sur le bouton **"-"** ou **"Supprimer l'utilisateur"**
5. Le système vous demandera si vous souhaitez :
   - **Conserver les fichiers** de l'utilisateur dans /home
   - **Supprimer les fichiers** de l'utilisateur

> **Important** : La suppression des fichiers est irréversible. Assurez-vous d'avoir sauvegardé toutes les données importantes avant de confirmer.

### Méthode en ligne de commande

#### Supprimer uniquement le compte (conserver les fichiers) :

```bash
sudo userdel sophie
```

Les fichiers restent dans `/home/sophie`.

#### Supprimer le compte ET tous les fichiers :

```bash
sudo userdel -r sophie
```

L'option `-r` supprime le répertoire personnel et le courrier de l'utilisateur.

#### Supprimer un compte même si l'utilisateur est connecté :

```bash
sudo userdel -f sophie
```

> **Attention** : Utilisez l'option `-f` avec prudence, car elle peut causer des problèmes si l'utilisateur a des processus en cours.

---

## Gérer les comptes au quotidien

### Changer d'utilisateur sans se déconnecter

Linux Mint permet de **basculer entre utilisateurs** sans fermer les sessions :

1. Cliquez sur le **menu utilisateur** (en haut à droite ou dans le menu principal)
2. Sélectionnez **"Changer d'utilisateur"** ou **"Changer de session"**
3. Un nouvel écran de connexion s'affiche
4. Connectez-vous avec un autre compte

Les deux sessions restent actives en arrière-plan. Vous pouvez revenir à la première session de la même manière.

### Connexion automatique

Par défaut, Linux Mint demande un mot de passe à chaque démarrage. Vous pouvez activer la **connexion automatique** :

1. Allez dans **Comptes utilisateurs**
2. **Déverrouillez** les modifications
3. Activez l'option **"Connexion automatique"** pour l'utilisateur souhaité

> **Avertissement de sécurité** : La connexion automatique réduit la sécurité de votre système. Ne l'activez que si vous êtes seul à utiliser l'ordinateur et qu'il est dans un environnement sécurisé.

### Voir les utilisateurs connectés

Pour savoir qui est actuellement connecté au système :

```bash
who
```

ou pour plus de détails :

```bash
w
```

---

## Bonnes pratiques

### Pour la création de comptes

1. **Un compte par personne** : Ne partagez jamais un compte entre plusieurs personnes
2. **Noms d'utilisateur clairs** : Choisissez des noms explicites et faciles à retenir
3. **Type de compte approprié** : Accordez le minimum de privilèges nécessaires
4. **Documenter** : Notez quelque part la liste des comptes et leur rôle

### Pour les mots de passe

1. **Longueur minimale** : Au moins 12 caractères
2. **Complexité** : Mélangez majuscules, minuscules, chiffres et symboles
3. **Unicité** : Chaque compte doit avoir son propre mot de passe
4. **Pas d'informations personnelles** : Évitez dates de naissance, noms de famille, etc.
5. **Gestionnaire de mots de passe** : Utilisez un outil comme KeePassXC pour stocker vos mots de passe de manière sécurisée

### Pour la gestion quotidienne

1. **Compte standard pour l'usage courant** : Utilisez votre compte administrateur uniquement quand nécessaire
2. **Revue régulière** : Supprimez les comptes inutilisés
3. **Sauvegarde** : Avant de supprimer un compte, vérifiez que toutes les données importantes sont sauvegardées
4. **Sessions inactives** : Configurez un verrouillage automatique après quelques minutes d'inactivité

### Pour la sécurité

1. **Pas de compte root direct** : Linux Mint désactive par défaut le compte root pour des raisons de sécurité. Utilisez `sudo` à la place
2. **Surveillance des connexions** : Vérifiez régulièrement les dernières connexions avec `last`
3. **Expiration des comptes temporaires** : Pour les comptes invités ou temporaires, définissez une date d'expiration
4. **Groupes appropriés** : Ajoutez les utilisateurs aux groupes nécessaires uniquement

---

## Résumé

La gestion des comptes utilisateurs sous Linux Mint est à la fois simple et puissante :

- **L'interface graphique** est idéale pour les débutants et pour les opérations courantes
- **La ligne de commande** offre plus de contrôle et permet l'automatisation
- **Deux types principaux** de comptes : administrateur et utilisateur standard
- **Privilégiez la sécurité** : comptes standards pour l'usage quotidien, mots de passe robustes, principe du moindre privilège

Dans le prochain chapitre, nous explorerons les **groupes et permissions avancées**, qui permettent un contrôle encore plus fin de l'accès aux ressources du système.

---


⏭️ [Les groupes et permissions avancées](/11-gestion-des-utilisateurs-et-securite/02-les-groupes-et-permissions-avancees.md)
