🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 2.1 Téléchargement et vérification de l'ISO

## Introduction

Avant d'installer Linux Mint, vous devez télécharger une image ISO. Une **image ISO** est un fichier qui contient l'intégralité du système d'exploitation Linux Mint, prêt à être installé sur votre ordinateur. Ce fichier servira à créer une clé USB bootable ou un DVD d'installation.

Dans ce chapitre, nous allons voir où télécharger Linux Mint de manière sécurisée et comment vérifier que le fichier téléchargé n'est pas corrompu ou modifié.

---

## Où télécharger Linux Mint ?

### Site officiel

Le seul endroit sûr pour télécharger Linux Mint est le **site officiel** :

🌐 **[https://www.linuxmint.com](https://www.linuxmint.com)**

> ⚠️ **Attention** : Ne téléchargez jamais Linux Mint depuis d'autres sites web, même s'ils promettent des téléchargements plus rapides. Vous risqueriez de télécharger une version modifiée ou infectée.

### Page de téléchargement

1. Rendez-vous sur le site officiel
2. Cliquez sur le bouton **"Download"** dans le menu principal
3. Vous arriverez sur la page des éditions disponibles

---

## Choisir la bonne édition

Linux Mint propose plusieurs éditions en fonction de l'environnement de bureau. Pour un débutant, voici les options recommandées :

### Éditions principales

| Édition | Description | Recommandée pour |
|---------|-------------|------------------|
| **Cinnamon** | Interface moderne et élégante, similaire à Windows | La plupart des utilisateurs, PC récents |
| **MATE** | Interface classique, légère et sobre | PC plus anciens, ceux qui préfèrent la simplicité |
| **Xfce** | Interface très légère et rapide | PC anciens ou peu puissants |

> 💡 **Conseil pour débutants** : Choisissez **Cinnamon** si votre ordinateur a moins de 5 ans. C'est l'édition la plus populaire et la plus complète.

### Architecture du processeur

Vous devrez également choisir entre :

- **64-bit (amd64)** : Pour tous les ordinateurs récents (depuis 2010 environ)
- **32-bit** : Pour les très vieux ordinateurs (avant 2010)

> 💡 **À savoir** : La version 32-bit n'est plus proposée depuis Linux Mint 20. Si vous avez un très vieil ordinateur, vous devrez utiliser une version plus ancienne de Mint ou une autre distribution.

### Exemple de fichier ISO

Un fichier ISO typique ressemble à ceci :

```
linuxmint-22.1-cinnamon-64bit.iso
```

Décomposition du nom :
- **linuxmint** : Le nom de la distribution
- **22.1** : La version de Linux Mint
- **cinnamon** : L'environnement de bureau
- **64bit** : L'architecture du processeur

---

## Télécharger l'image ISO

### Méthode recommandée : Via les miroirs

1. Sur la page de téléchargement, cliquez sur l'édition de votre choix (ex: **Cinnamon**)
2. Vous verrez une liste de **miroirs** (serveurs de téléchargement)
3. Choisissez un miroir proche de votre pays pour un téléchargement plus rapide
4. Le téléchargement démarre automatiquement

**Taille du fichier** : Environ 2,5 à 3 Go selon l'édition

**Temps de téléchargement** :
- Avec une connexion rapide (fibre) : 5 à 15 minutes
- Avec une connexion ADSL : 30 minutes à 2 heures
- Avec une connexion lente : plusieurs heures

### Alternative : Téléchargement direct

Si les miroirs ne fonctionnent pas, utilisez le **lien direct** proposé sur la page de téléchargement.

### Via Torrent (optionnel)

Pour les utilisateurs avancés, Linux Mint propose également un téléchargement via **BitTorrent**, qui peut être plus rapide et moins sensible aux interruptions.

---

## Pourquoi vérifier l'ISO ?

Une fois le téléchargement terminé, il est **fortement recommandé** de vérifier l'intégrité du fichier ISO. Voici pourquoi :

### Raisons de la vérification

1. **Détection de corruption** : Le fichier peut avoir été corrompu pendant le téléchargement (connexion interrompue, erreur réseau)
2. **Sécurité** : Vous vous assurez que le fichier n'a pas été modifié par un tiers malveillant
3. **Éviter les problèmes d'installation** : Un fichier corrompu peut causer des erreurs lors de l'installation

> 💡 **Analogie** : C'est comme vérifier le sceau d'un colis : vous vous assurez qu'il n'a pas été ouvert ou endommagé pendant le transport.

---

## Comprendre les checksums (sommes de contrôle)

Un **checksum** (ou somme de contrôle) est une empreinte numérique unique du fichier ISO. C'est une longue suite de caractères générée par un algorithme mathématique.

### Types de checksums

Linux Mint fournit deux types de checksums :

- **SHA256** : Le plus couramment utilisé, très sécurisé
- **MD5** : Plus ancien, moins sécurisé mais toujours utile

### Comment ça fonctionne ?

1. Linux Mint calcule le checksum de l'ISO officielle et le publie sur son site
2. Vous calculez le checksum de votre fichier téléchargé
3. Si les deux checksums sont **identiques**, le fichier est authentique et intact
4. Si les checksums sont **différents**, le fichier est corrompu ou modifié

---

## Où trouver les checksums officiels ?

Sur la page de téléchargement de Linux Mint, sous chaque édition, vous trouverez :

```
sha256sum: 2c8d8f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f
```

Vous pouvez également consulter le fichier **sha256sum.txt** disponible sur le site.

---

## Vérifier l'ISO sous Windows

### Méthode graphique : 7-Zip

**7-Zip** est un logiciel gratuit qui peut calculer les checksums.

#### Étapes :

1. **Télécharger 7-Zip** : [https://www.7-zip.org](https://www.7-zip.org)
2. **Installer** 7-Zip sur votre ordinateur
3. **Localiser** votre fichier ISO téléchargé
4. **Clic droit** sur le fichier ISO → **7-Zip** → **CRC SHA** → **SHA-256**
5. Une fenêtre s'ouvre avec le checksum calculé
6. **Comparer** ce checksum avec celui du site officiel

### Méthode en ligne de commande : PowerShell

Pour les utilisateurs à l'aise avec les commandes :

1. Ouvrez **PowerShell** (recherchez "PowerShell" dans le menu Démarrer)
2. Naviguez vers le dossier contenant l'ISO :
   ```powershell
   cd C:\Utilisateurs\VotreNom\Téléchargements
   ```
3. Exécutez la commande :
   ```powershell
   Get-FileHash linuxmint-22.1-cinnamon-64bit.iso -Algorithm SHA256
   ```
4. Comparez le résultat avec le checksum officiel

---

## Vérifier l'ISO sous Linux

Si vous utilisez déjà Linux (ou Linux en mode Live), la vérification est très simple.

### Via le terminal

1. Ouvrez un **terminal**
2. Naviguez vers le dossier contenant l'ISO :
   ```bash
   cd ~/Téléchargements
   ```
3. Calculez le checksum SHA256 :
   ```bash
   sha256sum linuxmint-22.1-cinnamon-64bit.iso
   ```
4. Comparez le résultat avec le checksum officiel

### Exemple de résultat

```
2c8d8f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f2f8f  linuxmint-22.1-cinnamon-64bit.iso
```

---

## Vérifier l'ISO sous macOS

### Via le terminal

1. Ouvrez l'application **Terminal** (Applications → Utilitaires → Terminal)
2. Naviguez vers le dossier contenant l'ISO :
   ```bash
   cd ~/Downloads
   ```
3. Calculez le checksum SHA256 :
   ```bash
   shasum -a 256 linuxmint-22.1-cinnamon-64bit.iso
   ```
4. Comparez le résultat avec le checksum officiel

---

## Comparer les checksums

### Comment comparer efficacement ?

Les checksums sont de **longues chaînes de caractères** (64 caractères pour SHA256). Pour éviter les erreurs :

1. **Copiez-collez** : Ne recopiez jamais manuellement
2. **Comparez visuellement** :
   - Vérifiez les premiers caractères (les 8 premiers)
   - Vérifiez les derniers caractères (les 8 derniers)
   - Vérifiez quelques caractères au milieu
3. **Utilisez la fonction de recherche** :
   - Copiez le checksum officiel
   - Utilisez Ctrl+F (ou Cmd+F sur Mac) pour le rechercher dans le résultat

### Que faire si les checksums correspondent ?

✅ **Félicitations !** Votre fichier ISO est authentique et intact. Vous pouvez passer à l'étape suivante : créer une clé USB bootable.

### Que faire si les checksums ne correspondent pas ?

❌ **Attention !** Le fichier est corrompu ou modifié. Voici ce que vous devez faire :

1. **Ne l'utilisez pas** : N'essayez pas d'installer Linux Mint avec ce fichier
2. **Supprimez** le fichier ISO défectueux
3. **Re-téléchargez** l'ISO depuis le site officiel
4. **Vérifiez à nouveau** le checksum après le nouveau téléchargement
5. Si le problème persiste, essayez un **autre miroir** ou utilisez le **téléchargement direct**

---

## Vérification avancée : Signature GPG (optionnel)

Pour les utilisateurs plus exigeants en matière de sécurité, Linux Mint propose également une **vérification par signature GPG**. Cette méthode garantit non seulement l'intégrité du fichier, mais aussi son authenticité (qu'il provient bien de l'équipe Linux Mint).

### Qu'est-ce que GPG ?

**GPG (GNU Privacy Guard)** est un système de cryptographie qui permet de signer numériquement des fichiers. L'équipe Linux Mint signe toutes ses ISO avec une clé privée, et vous pouvez vérifier cette signature avec leur clé publique.

### Pourquoi utiliser GPG ?

- Protection contre les **attaques de type "man-in-the-middle"**
- Garantie que l'ISO provient bien de Linux Mint
- Niveau de sécurité maximal

> 💡 **Pour débutants** : La vérification par checksum SHA256 est largement suffisante pour un usage normal. La vérification GPG est réservée aux utilisateurs avancés ou aux contextes nécessitant une sécurité maximale.

---

## Résumé des étapes

Voici un récapitulatif du processus complet :

1. ✅ Rendez-vous sur **linuxmint.com**
2. ✅ Choisissez l'**édition** appropriée (Cinnamon recommandé)
3. ✅ Téléchargez l'**ISO** via un miroir proche
4. ✅ Notez le **checksum SHA256** officiel
5. ✅ Calculez le checksum de votre fichier téléchargé
6. ✅ Comparez les deux checksums
7. ✅ Si identiques → passez à la création de la clé USB bootable
8. ✅ Si différents → re-téléchargez l'ISO

---

## Questions fréquentes

### Combien de temps l'ISO est-elle valable ?

L'ISO reste valable indéfiniment, mais il est recommandé de télécharger la **version la plus récente** pour bénéficier des dernières mises à jour et correctifs de sécurité.

### Puis-je utiliser la même ISO sur plusieurs ordinateurs ?

Oui ! Vous pouvez utiliser la même ISO pour installer Linux Mint sur autant d'ordinateurs que vous le souhaitez. Linux Mint est totalement **gratuit et libre**.

### Dois-je payer pour télécharger Linux Mint ?

**Non, jamais !** Linux Mint est entièrement gratuit. Si un site vous demande de payer, c'est une arnaque.

### La vérification du checksum est-elle vraiment nécessaire ?

C'est **fortement recommandé** mais pas obligatoire. Cependant, si vous rencontrez des problèmes lors de l'installation, la première chose à vérifier sera l'intégrité de l'ISO.

### Que signifie "LTS" ?

**LTS** signifie **Long Term Support** (support à long terme). Les versions LTS de Linux Mint reçoivent des mises à jour de sécurité pendant 5 ans. C'est idéal pour les débutants qui souhaitent un système stable.

### Quelle est la différence entre Linux Mint et LMDE ?

- **Linux Mint** : Basé sur Ubuntu, versions tous les 6 mois environ
- **LMDE (Linux Mint Debian Edition)** : Basé directement sur Debian, cycle de mise à jour continu

Pour les débutants, choisissez **Linux Mint** classique (basé sur Ubuntu).

---

## Étape suivante

Maintenant que vous avez téléchargé et vérifié votre ISO, vous êtes prêt à passer à l'étape suivante :

➡️ **2.2 Création d'une clé USB bootable**

Dans le prochain chapitre, nous verrons comment transformer votre fichier ISO en clé USB bootable pour installer Linux Mint sur votre ordinateur.

---

## Ressources complémentaires

- 📖 [Documentation officielle Linux Mint](https://linuxmint.com/documentation.php)
- 🌐 [Page de téléchargement officielle](https://www.linuxmint.com/download.php)
- 💬 [Forum Linux Mint (français)](https://forums.linuxmint.com/viewforum.php?f=21)
- 📺 [Guide vidéo : Télécharger Linux Mint](https://www.youtube.com/linuxmint)

---

**Bon téléchargement et à bientôt pour la suite de votre aventure Linux Mint ! 🚀**

⏭️ [Création d'une clé USB bootable (Rufus, Etcher, Ventoy)](/02-preparation-et-installation/02-creation-dune-cle-usb-bootable.md)
