🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 16.8 - Grub Customizer (personnaliser le boot)

## Introduction

Lorsque vous allumez votre ordinateur, avant même que Linux Mint ne démarre, vous voyez un menu avec différentes options de démarrage. Ce menu s'appelle **GRUB** (GRand Unified Bootloader), et c'est le programme qui vous permet de choisir quel système d'exploitation lancer si vous en avez plusieurs installés.

Par défaut, GRUB a une apparence assez austère et technique. Mais saviez-vous que vous pouvez le personnaliser pour le rendre plus esthétique, plus pratique, ou simplement refléter votre style ? Dans ce chapitre, nous allons découvrir comment utiliser **Grub Customizer** pour transformer votre écran de démarrage.

**⚠️ AVERTISSEMENT IMPORTANT :**
GRUB est un élément critique de votre système. Une mauvaise configuration peut empêcher votre ordinateur de démarrer. Suivez attentivement les instructions et faites toujours des sauvegardes avant de modifier GRUB.

---

## Qu'est-ce que GRUB ?

### Le bootloader expliqué simplement

**GRUB (GRand Unified Bootloader)** est le programme qui démarre en premier quand vous allumez votre ordinateur.

**Son rôle :**
1. S'exécute avant le système d'exploitation
2. Affiche un menu de choix
3. Charge le système sélectionné (Linux, Windows, etc.)
4. Passe le contrôle au système d'exploitation

**Analogie :**
Si votre ordinateur était un immeuble, GRUB serait le hall d'entrée où vous choisissez vers quel appartement (système d'exploitation) aller.

### Le menu GRUB par défaut

Quand vous démarrez votre ordinateur, vous voyez typiquement :

```
                    GNU GRUB version 2.06

  Linux Mint 21.3 Cinnamon
  Advanced options for Linux Mint 21.3 Cinnamon
  Windows Boot Manager (si dual-boot)
  System setup
```

**Caractéristiques par défaut :**
- Fond noir ou violet
- Texte blanc
- Police système
- Délai de 10 secondes
- Pas d'images
- Aspect très technique

### Pourquoi personnaliser GRUB ?

**Raisons esthétiques :**
- Rendre le démarrage plus agréable visuellement
- Ajouter un fond d'écran personnalisé
- Changer les couleurs et polices
- Créer une cohérence avec le reste du système

**Raisons pratiques :**
- Réorganiser l'ordre des entrées
- Masquer les entrées inutiles
- Changer le système par défaut
- Ajuster le délai d'attente
- Renommer les entrées pour plus de clarté

**Raisons techniques :**
- Modifier les paramètres de démarrage
- Ajouter des options personnalisées
- Gérer plusieurs systèmes

---

## Installer Grub Customizer

Grub Customizer n'est pas installé par défaut sur Linux Mint.

### Installation via le terminal

**Méthode recommandée :**

```bash
# Ajouter le PPA (dépôt)
sudo add-apt-repository ppa:danielrichter2007/grub-customizer

# Mettre à jour la liste des paquets
sudo apt update

# Installer Grub Customizer
sudo apt install grub-customizer
```

**Vérifier l'installation :**
```bash
grub-customizer --version
```

### Lancer Grub Customizer

**Via le menu :**
1. Menu → Préférences → Grub Customizer
2. Entrez votre mot de passe administrateur
3. L'application se lance

**Via le terminal :**
```bash
sudo grub-customizer
```

**Note :** Grub Customizer nécessite toujours les droits administrateur (sudo) car il modifie des fichiers système critiques.

---

## Interface de Grub Customizer

### Première ouverture

Lors du premier lancement, Grub Customizer analyse votre configuration actuelle. Cela peut prendre quelques secondes.

**Fenêtre principale avec 5 onglets :**

1. **Éléments de la liste** : Gestion des entrées de boot
2. **Paramètres généraux** : Délai, système par défaut, apparence
3. **Paramètres d'apparence** : Thème, couleurs, images
4. **Options avancées** : Paramètres kernel et options techniques
5. **Partitionnement** : Informations sur les partitions (lecture seule)

### Barre d'outils

**Boutons principaux :**
- **Enregistrer** : Applique les modifications (très important !)
- **Annuler** : Annule les changements non enregistrés
- **Actualiser** : Recharge la configuration
- **Aide** : Documentation

**⚠️ IMPORTANT :** Les modifications ne sont appliquées que lorsque vous cliquez sur "Enregistrer". Ne fermez jamais l'application sans enregistrer si vous voulez garder vos changements.

---

## Gérer les entrées de démarrage

### Onglet "Éléments de la liste"

C'est ici que vous gérez ce qui apparaît dans le menu GRUB.

**Liste des entrées :**
Vous verrez toutes les options de démarrage :
- Linux Mint (version actuelle)
- Options avancées (anciens kernels)
- Windows (si dual-boot)
- Memtest86+ (test de mémoire)
- Autres systèmes détectés

### Réorganiser les entrées

**Changer l'ordre :**
1. Sélectionnez une entrée
2. Utilisez les flèches ↑ ↓ dans la barre d'outils
3. Ou faites glisser l'entrée avec la souris

**Exemple :**
Si vous voulez Windows en première position :
1. Sélectionnez "Windows Boot Manager"
2. Cliquez sur ↑ jusqu'à ce qu'il soit en haut
3. Enregistrez

### Masquer des entrées

**Pourquoi masquer ?**
- Réduire l'encombrement du menu
- Cacher les options techniques (memtest, recovery mode)
- Simplifier le choix pour les utilisateurs non techniques

**Comment masquer :**
1. Sélectionnez l'entrée
2. Décochez la case à gauche de l'entrée
3. L'entrée reste dans la configuration mais n'apparaît plus au démarrage

**Entrées couramment masquées :**
- Memtest86+ (test mémoire)
- UEFI Firmware Settings
- Anciens kernels (sauf 1-2 de secours)

**⚠️ NE PAS masquer :**
- Votre système principal
- Au moins une option de secours (recovery mode)

### Renommer des entrées

**Rendre les noms plus clairs :**

**Exemple :**
- "GNU/Linux, Linux 5.15.0-91-generic" → "Linux Mint (kernel actuel)"
- "Windows Boot Manager" → "Windows 11"

**Comment renommer :**
1. Double-cliquez sur l'entrée
2. Ou : Clic droit → Renommer
3. Modifiez le texte
4. Validez
5. Enregistrez

### Supprimer des entrées

**⚠️ ATTENTION :** Ne supprimez que si vous êtes absolument sûr !

**Quand supprimer :**
- Ancien système d'exploitation désinstallé
- Entrée en double
- Système sur partition supprimée

**Comment supprimer :**
1. Sélectionnez l'entrée
2. Clic droit → Supprimer
3. Confirmez
4. Enregistrez

**Note :** Il vaut mieux masquer que supprimer. Masquer est réversible plus facilement.

---

## Paramètres généraux

### Onglet "Paramètres généraux"

**Options importantes :**

### 1. Entrée par défaut

**C'est le système qui démarre automatiquement si vous ne choisissez rien.**

**Options :**
- **Sélection prédéfinie** : Choisissez dans la liste
- **Dernière sélection** : Se souvient de votre dernier choix
- **Par numéro** : Spécifiez la position (0 = premier, 1 = deuxième, etc.)

**Exemple :**
Si vous êtes principalement sous Windows mais voulez garder Linux :
1. Mettez Windows en entrée par défaut
2. Ou mettez "Dernière sélection" pour qu'il se souvienne

### 2. Délai de visibilité

**Temps d'affichage du menu GRUB (en secondes)**

**Valeurs courantes :**
- **0 seconde** : Menu caché, démarre immédiatement le système par défaut
- **3-5 secondes** : Rapide mais laisse le temps de choisir
- **10 secondes** : Valeur par défaut
- **30+ secondes** : Beaucoup de temps pour choisir

**Recommandations :**
- **Dual-boot fréquent** : 10 secondes
- **Un seul système** : 3 secondes ou 0
- **Débutant** : 10-15 secondes (sécurité)

**Option "Démarrage permanent" :**
- Si cochée : Menu toujours affiché (pas de timeout)
- Utile si vous changez souvent de système

### 3. Affichage du menu

**Contrôle la visibilité du menu**

**Options :**
- **Toujours afficher le menu** : Menu visible à chaque démarrage
- **Afficher si d'autres systèmes sont installés** : Intelligent
- **Cacher le menu** : Démarre directement (maintenir Shift pour afficher)

**Recommandations :**
- **Dual-boot** : Toujours afficher
- **Linux uniquement** : Afficher si d'autres systèmes

### 4. Résolution de l'écran

**Définit la résolution du menu GRUB**

**Options :**
- Auto : GRUB détecte automatiquement
- 1920x1080, 1366x768, 1280x720, etc.

**Important :** Choisissez la résolution native de votre écran pour une meilleure qualité d'image de fond.

### 5. Kernel par défaut

**Si plusieurs kernels sont installés**

**Options :**
- Le plus récent
- Version spécifique
- Le précédent (fallback)

**Recommandation :** Laissez sur "Le plus récent" sauf problème spécifique.

---

## Personnaliser l'apparence

### Onglet "Paramètres d'apparence"

C'est ici que la magie opère !

### 1. Utiliser un thème GRUB

**Qu'est-ce qu'un thème GRUB ?**
Un ensemble cohérent comprenant :
- Image de fond
- Polices personnalisées
- Couleurs
- Disposition des éléments
- Parfois des icônes

**Thèmes préinstallés :**
Par défaut, quelques thèmes basiques sont disponibles.

**Sélectionner un thème :**
1. Cochez "Utiliser un thème"
2. Cliquez sur "Obtenir des thèmes en ligne" (bouton de téléchargement)
3. Ou installez un thème manuellement (voir section suivante)

### 2. Image de fond personnalisée

**Ajouter votre propre image**

**Formats supportés :**
- PNG (recommandé)
- JPG/JPEG
- TGA

**Résolution recommandée :**
- Utilisez la résolution de votre écran
- Exemples : 1920x1080, 1366x768, 2560x1440

**Comment ajouter :**
1. Décochez "Utiliser un thème" (ou gardez si compatible)
2. Section "Image de fond"
3. Cochez "Image"
4. Cliquez sur le bouton de sélection de fichier
5. Naviguez vers votre image
6. Sélectionnez et validez

**Conseils pour l'image :**
- Évitez les images trop claires (texte blanc illisible)
- Évitez les images trop surchargées
- Préférez des images sombres ou moyennement claires
- Testez la lisibilité du texte blanc sur l'image

### 3. Personnaliser les couleurs

**Si vous n'utilisez pas de thème complet**

**Options disponibles :**

**Couleur de fond :**
- Couleur unie
- Ou dégradé

**Couleur du texte normal :**
- Couleur des entrées non sélectionnées
- Recommandé : Blanc ou gris clair

**Couleur de la surbrillance :**
- Couleur de l'entrée sélectionnée (où est le curseur)
- Recommandé : Jaune, vert clair, bleu clair (contraste)

**Couleur de fond de la surbrillance :**
- Fond de l'entrée sélectionnée
- Peut être transparent

**Exemple de configuration :**
```
Texte normal : Blanc (#FFFFFF)
Surbrillance texte : Jaune (#FFFF00)
Fond surbrillance : Bleu foncé (#0000AA)
```

### 4. Police personnalisée

**Installer une police pour GRUB**

GRUB utilise un format de police spécial (.pf2).

**Conversion d'une police TTF vers PF2 :**
```bash
sudo grub-mkfont -o /boot/grub/fonts/ma-police.pf2 -s 24 /chemin/vers/police.ttf
```

**Paramètres :**
- `-s 24` : Taille de la police (ajustez selon besoin)
- `-o` : Fichier de sortie

**Sélectionner dans Grub Customizer :**
1. Section "Police"
2. Parcourez vers `/boot/grub/fonts/`
3. Sélectionnez votre police .pf2

**Polices recommandées :**
- DejaVu Sans (par défaut, lisible)
- Ubuntu
- Liberation Sans

---

## Installer des thèmes GRUB

### Où trouver des thèmes ?

**Sources recommandées :**

**1. Gnome-look.org**
- URL : [gnome-look.org](https://www.gnome-look.org/browse?cat=109)
- Section "GRUB Themes"
- Nombreux thèmes gratuits

**2. GitHub**
- Recherchez "grub theme"
- Souvent les versions les plus récentes

**3. Pling.com**
- Même contenu que Gnome-look
- Interface moderne

### Thèmes GRUB populaires

**1. Vimix**
- Design moderne et élégant
- Plusieurs variantes de couleur
- Icônes pour les systèmes

**2. Tela**
- Minimaliste et épuré
- Belles icônes
- Support multi-résolution

**3. Cyberpunk**
- Style futuriste
- Couleurs néon
- Pour les amateurs de cyberpunk

**4. Fallout**
- Inspiré du jeu Fallout
- Style rétro-futuriste
- Très distinctif

**5. Matter**
- Design Google Material
- Couleurs vives
- Moderne

**6. Poly Dark/Light**
- Design polygonal
- Variantes sombre et claire
- Très beau graphiquement

### Installation manuelle d'un thème

**Étapes générales :**

**1. Télécharger le thème**
```bash
cd ~/Téléchargements
wget URL-du-theme.tar.gz
# Ou téléchargez via navigateur
```

**2. Extraire l'archive**
```bash
tar -xzf nom-theme.tar.gz
# Ou
unzip nom-theme.zip
```

**3. Copier vers le dossier GRUB**
```bash
sudo cp -r nom-theme /boot/grub/themes/
```

**4. Sélectionner dans Grub Customizer**
1. Onglet "Paramètres d'apparence"
2. Cochez "Utiliser un thème"
3. Parcourez vers `/boot/grub/themes/nom-theme`
4. Sélectionnez `theme.txt`
5. Enregistrez

### Exemple : Installer le thème Vimix

```bash
# Télécharger
git clone https://github.com/vinceliuice/grub2-themes.git
cd grub2-themes

# Installer (script automatique)
sudo ./install.sh -t vimix

# Le thème est maintenant installé
# Sélectionnez-le dans Grub Customizer
```

**Vérifier l'installation :**
1. Ouvrez Grub Customizer
2. Onglet "Paramètres d'apparence"
3. Le thème devrait apparaître dans la liste

---

## Paramètres avancés

### Onglet "Options avancées"

**⚠️ ATTENTION :** Ces paramètres sont techniques. Ne modifiez que si vous savez ce que vous faites.

### Options courantes

**1. GRUB_CMDLINE_LINUX_DEFAULT**
- Paramètres passés au kernel Linux
- Exemple : `quiet splash` (démarrage silencieux avec écran de chargement)

**Paramètres utiles :**
- `quiet` : Cache les messages de démarrage
- `splash` : Affiche un écran de chargement
- `nomodeset` : Désactive le mode graphique (utile si problème de pilote)
- `acpi=off` : Désactive ACPI (problèmes d'alimentation)

**2. GRUB_TIMEOUT**
- Délai en secondes (accessible aussi dans Paramètres généraux)

**3. GRUB_GFXMODE**
- Résolution du menu GRUB
- Exemple : `1920x1080`

**4. GRUB_BACKGROUND**
- Chemin vers l'image de fond
- Exemple : `/boot/grub/backgrounds/mon-fond.png`

### Modifier manuellement la configuration

**Fichier de configuration principal :**
```bash
sudo nano /etc/default/grub
```

**Exemple de configuration :**
```bash
GRUB_DEFAULT=0
GRUB_TIMEOUT_STYLE=menu
GRUB_TIMEOUT=10
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX=""
GRUB_BACKGROUND="/boot/grub/backgrounds/mon-fond.png"
GRUB_GFXMODE=1920x1080
```

**Après modification manuelle, TOUJOURS exécuter :**
```bash
sudo update-grub
```

**Note :** Grub Customizer fait cela automatiquement quand vous cliquez sur "Enregistrer".

---

## Sauvegardes et restauration

### Créer une sauvegarde avant modifications

**Méthode 1 : Sauvegarde automatique de Grub Customizer**

Grub Customizer crée automatiquement des sauvegardes dans :
```
/boot/grub/custom_backup/
```

**Méthode 2 : Sauvegarde manuelle**

```bash
# Sauvegarder la configuration
sudo cp /etc/default/grub /etc/default/grub.backup

# Sauvegarder le fichier grub.cfg
sudo cp /boot/grub/grub.cfg /boot/grub/grub.cfg.backup

# Créer une archive complète
sudo tar -czf ~/grub-backup-$(date +%Y%m%d).tar.gz /boot/grub/ /etc/default/grub
```

### Restaurer une sauvegarde

**Si Grub Customizer a créé une sauvegarde :**

1. Ouvrez Grub Customizer
2. Fichier → Restaurer depuis sauvegarde
3. Sélectionnez la date
4. Confirmez

**Restauration manuelle :**

```bash
# Restaurer /etc/default/grub
sudo cp /etc/default/grub.backup /etc/default/grub

# Régénérer la configuration
sudo update-grub

# Redémarrer
sudo reboot
```

### Réinitialiser GRUB aux paramètres par défaut

**Méthode complète :**

```bash
# Supprimer les personnalisations
sudo rm /etc/default/grub
sudo rm -rf /boot/grub/themes/*

# Réinstaller GRUB
sudo apt install --reinstall grub-common grub-pc

# Reconfigurer
sudo dpkg-reconfigure grub-pc

# Mettre à jour
sudo update-grub
```

---

## Dual-boot : Conseils spécifiques

### Gérer Windows et Linux

**Ordre recommandé :**
1. Linux Mint (utilisation principale)
2. Windows
3. Options avancées Linux
4. Autres

**Renommer pour clarté :**
- "Windows Boot Manager" → "Windows 11"
- "Linux Mint 21.3" → "Linux Mint (quotidien)"

**Délai recommandé :** 10 secondes minimum

### Détecter Windows manquant

Si Windows n'apparaît pas dans GRUB :

```bash
# Mettre à jour GRUB (détecte automatiquement Windows)
sudo update-grub

# Installer os-prober si absent
sudo apt install os-prober

# Re-scanner
sudo os-prober
sudo update-grub
```

### Windows en système par défaut

Si vous utilisez Windows plus souvent :

1. Grub Customizer → Paramètres généraux
2. Entrée par défaut : "Windows Boot Manager"
3. Ou utilisez "Dernière sélection"
4. Enregistrez

---

## Résolution d'écran de démarrage

### Configurer la résolution du logo Plymouth

Plymouth est l'écran de chargement (logo Linux Mint qui tourne).

**Modifier la résolution :**

1. Grub Customizer → Paramètres généraux
2. Résolution : Sélectionnez votre résolution native
3. Enregistrez

**Ou manuellement :**
```bash
sudo nano /etc/default/grub
```

Modifiez :
```bash
GRUB_GFXMODE=1920x1080
GRUB_GFXPAYLOAD_LINUX=keep
```

Puis :
```bash
sudo update-grub
```

### Changer le thème Plymouth

```bash
# Voir les thèmes disponibles
plymouth-set-default-theme --list

# Changer de thème
sudo plymouth-set-default-theme -R nom-du-theme
```

---

## Dépannage

### GRUB ne démarre pas après modifications

**Symptôme :** Écran noir ou erreur "grub rescue"

**Solution de secours :**

**1. Démarrer avec une clé USB Live**
- Créez une clé USB de Linux Mint
- Démarrez dessus

**2. Réinstaller GRUB**
```bash
# Identifier votre partition système
sudo fdisk -l

# Monter votre partition (exemple : /dev/sda1)
sudo mount /dev/sda1 /mnt
sudo mount --bind /dev /mnt/dev
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys

# Chroot
sudo chroot /mnt

# Réinstaller GRUB
grub-install /dev/sda
update-grub

# Sortir et redémarrer
exit
sudo reboot
```

**3. Utiliser Boot Repair**
```bash
# Sur la clé USB Live
sudo add-apt-repository ppa:yannubuntu/boot-repair
sudo apt update
sudo apt install boot-repair
boot-repair
```

Suivez l'assistant (généralement "Réparation recommandée").

### Le thème ne s'affiche pas

**Vérifications :**

1. **Vérifier le chemin du thème**
```bash
ls /boot/grub/themes/nom-theme/
```
Doit contenir `theme.txt`

2. **Vérifier les permissions**
```bash
sudo chmod -R 755 /boot/grub/themes/
```

3. **Vérifier la configuration**
```bash
grep GRUB_THEME /etc/default/grub
```
Doit afficher : `GRUB_THEME="/boot/grub/themes/nom-theme/theme.txt"`

4. **Mettre à jour GRUB**
```bash
sudo update-grub
```

### L'image de fond ne s'affiche pas

**Solutions :**

1. **Vérifier le format de l'image**
   - PNG recommandé
   - JPG parfois problématique
   - Évitez GIF

2. **Vérifier la résolution**
   - Correspondance avec GRUB_GFXMODE

3. **Copier l'image au bon endroit**
```bash
sudo cp ~/mon-image.png /boot/grub/backgrounds/
sudo chmod 644 /boot/grub/backgrounds/mon-image.png
```

4. **Forcer dans /etc/default/grub**
```bash
GRUB_BACKGROUND="/boot/grub/backgrounds/mon-image.png"
```

### Grub Customizer ne sauvegarde pas

**Si le bouton "Enregistrer" ne fait rien :**

1. **Vérifier les permissions**
```bash
ls -la /boot/grub/
```

2. **Exécuter en tant que root**
```bash
sudo grub-customizer
```

3. **Vérifier l'espace disque**
```bash
df -h /boot
```
Si plein, nettoyez les anciens kernels

4. **Mettre à jour manuellement**
```bash
sudo update-grub
```

### Entrées en double

**Symptôme :** Plusieurs entrées identiques pour le même système

**Solution :**

1. Dans Grub Customizer, masquez ou supprimez les doublons
2. Si cela persiste :
```bash
sudo os-prober
sudo update-grub
```

### Texte illisible sur l'image de fond

**Solutions :**

1. **Changer l'image** : Utilisez une plus sombre
2. **Ajouter un overlay** : Image avec zone sombre pour le texte
3. **Modifier les couleurs du texte** : Essayez noir au lieu de blanc
4. **Ajouter un fond au texte** : Dans les paramètres d'apparence

---

## Configurations recommandées

### Configuration "Simple et rapide"

**Objectif :** Démarrage rapide avec minimum de distractions

```
Entrée par défaut : Linux Mint
Délai : 3 secondes
Affichage du menu : Si autres systèmes
Thème : Aucun (défaut)
Fond : Uni, sombre
Entrées masquées : Memtest, UEFI Settings, anciens kernels
```

### Configuration "Dual-boot élégant"

**Objectif :** Beau menu pour choisir entre Linux et Windows

```
Entrée par défaut : Dernière sélection
Délai : 10 secondes
Affichage du menu : Toujours
Thème : Vimix ou Tela
Fond : Image HD cohérente avec le thème
Entrées affichées : Linux Mint, Windows, Recovery
Entrées masquées : Memtest, anciens kernels
Résolution : 1920x1080 (native)
```

### Configuration "Tech/Geek"

**Objectif :** Style technique avec toutes les options

```
Entrée par défaut : Linux Mint (dernière version)
Délai : 15 secondes
Affichage du menu : Toujours
Thème : Cyberpunk ou style Matrix
Fond : Image technique/code
Entrées affichées : Toutes (y compris memtest, UEFI)
Police : Monospace style terminal
Couleurs : Vert néon sur noir
```

### Configuration "Minimaliste"

**Objectif :** Propre et discret

```
Entrée par défaut : Linux Mint
Délai : 5 secondes
Affichage du menu : Caché (Shift pour afficher)
Thème : Aucun
Fond : Noir uni
Entrées : Uniquement le système principal
Texte : Blanc sur noir
```

---

## Astuces avancées

### Ajouter un mot de passe GRUB

**Pour protéger l'accès au menu GRUB**

```bash
# Générer un mot de passe crypté
grub-mkpasswd-pbkdf2
# Entrez votre mot de passe

# Éditez /etc/grub.d/40_custom
sudo nano /etc/grub.d/40_custom
```

Ajoutez :
```
set superusers="admin"
password_pbkdf2 admin [HASH-GÉNÉRÉ]
```

**Mettre à jour :**
```bash
sudo update-grub
```

**⚠️ Attention :** Notez bien le mot de passe ! Si vous l'oubliez, vous devrez réinstaller GRUB.

### Ajouter une entrée personnalisée

**Exemple : Ajouter un outil de diagnostic**

```bash
sudo nano /etc/grub.d/40_custom
```

Ajoutez :
```
menuentry "Memtest86+" {
    linux16 /boot/memtest86+.bin
}
```

Ou :
```
menuentry "Démarrer depuis USB" {
    search --set=root --file /efi/boot/bootx64.efi
    chainloader /efi/boot/bootx64.efi
}
```

**Mettre à jour :**
```bash
sudo update-grub
```

### Scripts de maintenance GRUB

**Script pour nettoyer les anciens kernels :**

```bash
#!/bin/bash
# Garder seulement les 2 derniers kernels
sudo apt autoremove --purge
sudo update-grub
```

**Script pour sauvegarder GRUB avant modification :**

```bash
#!/bin/bash
DATE=$(date +%Y%m%d-%H%M%S)
sudo tar -czf ~/grub-backup-$DATE.tar.gz /boot/grub /etc/default/grub
echo "Sauvegarde créée : ~/grub-backup-$DATE.tar.gz"
```

---

## Alternatives à Grub Customizer

### rEFInd

**Bootloader alternatif graphique**

**Avantages :**
- Interface graphique native (sans configuration)
- Détection automatique des systèmes
- Thèmes magnifiques
- Support des icônes

**Installation :**
```bash
sudo apt install refind
```

**Note :** rEFInd remplace GRUB, c'est un changement important.

### systemd-boot

**Bootloader minimaliste pour systèmes UEFI**

**Avantages :**
- Très rapide
- Simple
- Intégré à systemd

**Inconvénient :** Uniquement UEFI, pas de support BIOS.

### Burg (abandonné)

Anciennement populaire mais n'est plus maintenu. Ne pas utiliser.

---

## Bonnes pratiques

### Avant de modifier GRUB

**Checklist de sécurité :**

1. ✅ **Sauvegardez votre configuration**
   ```bash
   sudo cp /etc/default/grub /etc/default/grub.backup
   ```

2. ✅ **Vérifiez l'espace disque sur /boot**
   ```bash
   df -h /boot
   ```
   Minimum 100 MB libres recommandé

3. ✅ **Ayez une clé USB de récupération**
   - Créez une clé USB Live de Linux Mint
   - Testez-la avant de modifier GRUB

4. ✅ **Notez votre configuration actuelle**
   - Prenez des captures d'écran
   - Notez les paramètres importants

5. ✅ **Testez avec prudence**
   - Modifiez un paramètre à la fois
   - Redémarrez et vérifiez
   - Puis passez au suivant

### Après avoir modifié GRUB

1. **Redémarrez immédiatement pour tester**
   - Ne faites pas 10 modifications d'un coup
   - Testez chaque changement

2. **Vérifiez que tout fonctionne**
   - Le menu s'affiche correctement
   - Vous pouvez démarrer tous les systèmes
   - Les images/thèmes s'affichent

3. **Gardez une sauvegarde récente**
   - Datez vos sauvegardes
   - Conservez au moins 2-3 versions

---

## Ressources et galeries de thèmes

### Sites de thèmes GRUB

**Gnome-look.org :**
- [GRUB Themes](https://www.gnome-look.org/browse?cat=109)
- Plus grande collection
- Notes et commentaires

**Pling.com :**
- Interface moderne
- Même contenu

**GitHub :**
- Recherchez "grub theme"
- Souvent les projets actifs
- Code source disponible

### Collections de thèmes populaires

**grub2-themes by vinceliuice :**
- [GitHub](https://github.com/vinceliuice/grub2-themes)
- Plusieurs thèmes de qualité
- Script d'installation automatique

**Gorgeous GRUB :**
- Collection de thèmes élégants
- Divers styles

### Créer son propre thème (avancé)

**Structure d'un thème GRUB :**

```
mon-theme/
├── theme.txt           # Configuration principale
├── background.png      # Image de fond
├── icons/             # Dossier des icônes
│   ├── linux.png
│   ├── windows.png
│   └── ...
└── fonts/             # Polices personnalisées
    └── font.pf2
```

**Exemple de theme.txt :**
```
title-text: ""
desktop-image: "background.png"
desktop-color: "#000000"
terminal-font: "Unifont Regular 16"
terminal-box: "terminal_box_*.png"
terminal-left: "0"
terminal-top: "0"
terminal-width: "100%"
terminal-height: "100%"
terminal-border: "0"

+ boot_menu {
    left = 15%
    width = 70%
    top = 30%
    height = 50%
    item_color = "#ffffff"
    selected_item_color = "#000000"
    item_height = 30
    item_padding = 10
    item_spacing = 5
    selected_item_pixmap_style = "select_*.png"
}
```

---

## Aller plus loin

### Comprendre les fichiers GRUB

**Fichiers importants :**

```
/etc/default/grub              # Configuration principale
/boot/grub/grub.cfg            # Configuration générée (ne pas éditer!)
/etc/grub.d/                   # Scripts de génération
/boot/grub/themes/             # Thèmes installés
/boot/grub/fonts/              # Polices
```

**Scripts dans /etc/grub.d/ :**
- `00_header` : Entête
- `05_debian_theme` : Thème Debian/Ubuntu
- `10_linux` : Détection des kernels Linux
- `20_linux_xen` : Support Xen
- `30_os-prober` : Détection autres OS (Windows)
- `40_custom` : Vos ajouts personnalisés
- `41_custom` : Ajouts personnalisés (template)

### Commandes GRUB utiles

```bash
# Mettre à jour GRUB
sudo update-grub

# Réinstaller GRUB sur le disque
sudo grub-install /dev/sda

# Vérifier la configuration GRUB
sudo grub-script-check /boot/grub/grub.cfg

# Lister les systèmes détectés
sudo os-prober

# Voir la version de GRUB
grub-install --version
```

---

## Résumé

Dans ce chapitre, vous avez appris :

- ✅ Ce qu'est GRUB et son rôle dans le démarrage
- ✅ Comment installer et utiliser Grub Customizer
- ✅ Gérer les entrées de démarrage (réorganiser, masquer, renommer)
- ✅ Configurer les paramètres généraux (délai, système par défaut)
- ✅ Personnaliser l'apparence (thèmes, images, couleurs)
- ✅ Installer des thèmes GRUB tiers
- ✅ Créer des sauvegardes et restaurer en cas de problème
- ✅ Résoudre les problèmes courants
- ✅ Les meilleures pratiques pour modifier GRUB en toute sécurité
- ✅ Des configurations complètes pour différents usages

**⚠️ Rappel important :** GRUB est critique pour le démarrage. Faites toujours des sauvegardes avant de le modifier, et testez immédiatement après chaque changement. Gardez une clé USB de récupération à portée de main !

La personnalisation de GRUB est la touche finale de votre système Linux Mint personnalisé. De l'allumage de l'ordinateur à l'extinction, chaque étape peut refléter votre style et vos préférences !

---

**Fin du chapitre 16 : Personnalisation avancée**

Vous avez maintenant toutes les clés pour faire de Linux Mint un système vraiment unique, parfaitement adapté à vos besoins et à vos goûts !

⏭️ [Sauvegarde et restauration](/17-sauvegarde-et-restauration/README.md)
