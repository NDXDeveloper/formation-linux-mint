🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.7 AppImage

## Introduction

**AppImage** est probablement le format d'application le plus simple à comprendre et à utiliser sous Linux. Contrairement aux .deb, Flatpak ou Snap que nous avons vus, AppImage ne nécessite **aucune installation**. C'est un fichier exécutable autonome qui contient tout ce dont l'application a besoin pour fonctionner.

**Analogie simple** : Si les autres formats sont comme installer un programme dans votre maison, AppImage est comme une mallette que vous posez sur la table et que vous ouvrez quand vous en avez besoin. Vous pouvez la déplacer, la partager ou la jeter sans que rien ne change dans votre maison.

C'est l'équivalent Linux des fichiers **.exe portables** sur Windows, comme VLC Portable ou LibreOffice Portable.

## Qu'est-ce qu'AppImage ?

### Définition

Un **AppImage** est un fichier unique (généralement avec l'extension `.AppImage`) qui contient :
- L'application elle-même
- Toutes ses bibliothèques et dépendances
- Les icônes et fichiers de ressources
- Tout ce qui est nécessaire pour l'exécuter

### Le concept "One app = one file"

La philosophie d'AppImage est simple : **une application = un fichier**.

Pas de :
- Installation complexe
- Modifications du système
- Dépendances à résoudre
- Problèmes de compatibilité
- Désinstallation nécessaire

Vous téléchargez, vous rendez exécutable, vous lancez. C'est tout.

### Historique

AppImage a été créé en 2004 par Simon Peter. L'objectif était de créer un format d'application qui :
- Fonctionne sur toutes les distributions Linux
- Ne nécessite pas de privilèges root
- Ne modifie pas le système
- Soit aussi simple que possible

## Avantages d'AppImage

### Pour les utilisateurs

✅ **Simplicité extrême**
- Télécharger → Rendre exécutable → Lancer
- Pas besoin de comprendre APT, Flatpak ou autre

✅ **Portabilité**
- Copiez le fichier sur une clé USB
- Utilisez-le sur n'importe quel ordinateur Linux
- Partagez-le facilement

✅ **Pas d'installation**
- Ne touche pas au système
- Aucun risque de casser quoi que ce soit
- Parfait pour tester des logiciels

✅ **Indépendance**
- Fonctionne même sans connexion Internet
- Pas besoin de dépôts ou de comptes

✅ **Versions multiples**
- Gardez plusieurs versions d'un même logiciel
- Idéal pour les développeurs

✅ **Désinstallation immédiate**
- Supprimez simplement le fichier
- Aucune trace ne reste (sauf les fichiers de configuration)

### Pour les développeurs

- ✅ **Distribution simple** : Un seul fichier à fournir
- ✅ **Compatibilité** : Fonctionne sur toutes les distributions
- ✅ **Contrôle** : L'environnement est maîtrisé
- ✅ **Pas de packaging complexe** : Pas besoin de créer .deb, .rpm, etc.

## Inconvénients d'AppImage

Soyons honnêtes, AppImage a aussi des limitations :

❌ **Taille importante**
- Chaque AppImage contient toutes ses dépendances
- Une simple application peut faire 100-200 Mo
- Si vous avez 10 AppImages, beaucoup de doublons

❌ **Pas de mises à jour automatiques**
- Vous devez manuellement télécharger les nouvelles versions
- Certains AppImages ont un système de mise à jour intégré, mais ce n'est pas standard

❌ **Intégration système limitée**
- Les AppImages n'apparaissent pas automatiquement dans le menu
- Pas d'icône dans le lanceur d'applications (sauf configuration manuelle)
- Peuvent ne pas respecter votre thème système

❌ **Sécurité moyenne**
- Pas de sandboxing par défaut (contrairement à Flatpak/Snap)
- Vous devez faire confiance à la source
- Vérification de la provenance plus difficile

❌ **Gestion des permissions**
- L'AppImage a accès à tout ce que votre utilisateur peut faire
- Pas de contrôle fin des permissions

## Comment utiliser un AppImage

### Étape 1 : Télécharger l'AppImage

Vous pouvez trouver des AppImages sur :

**AppImageHub** : https://www.appimagehub.com/
- Catalogue officiel d'AppImages
- Vérifiez toujours la source

**Sites officiels des projets**
- Beaucoup de développeurs fournissent des AppImages
- Cherchez une section "Download" ou "Releases"

**GitHub Releases**
- Beaucoup de projets open source publient leurs AppImages sur GitHub
- Allez dans la section "Releases" du projet

**Exemple** : Pour télécharger GIMP en AppImage, allez sur le site officiel ou AppImageHub.

### Étape 2 : Rendre le fichier exécutable

Par défaut, les fichiers téléchargés ne sont pas exécutables pour des raisons de sécurité. Vous devez activer cette permission.

#### Méthode graphique (la plus simple)

1. Allez dans votre dossier **Téléchargements**
2. **Clic droit** sur le fichier .AppImage
3. Sélectionnez **"Propriétés"**
4. Allez dans l'onglet **"Permissions"**
5. Cochez **"Autoriser l'exécution du fichier comme un programme"** (ou "Exécutable")
6. Fermez la fenêtre

#### Méthode en ligne de commande

```bash
chmod +x nom-du-fichier.AppImage
```

Exemple :
```bash
chmod +x ~/Téléchargements/GIMP-latest.AppImage
```

**Explication** :
- `chmod` : Change les permissions d'un fichier
- `+x` : Ajoute la permission d'exécution
- Le chemin vers votre fichier AppImage

### Étape 3 : Lancer l'application

Une fois le fichier rendu exécutable, vous pouvez le lancer.

#### Méthode graphique

1. **Double-cliquez** sur le fichier .AppImage
2. L'application démarre !

Si le double-clic ne fonctionne pas :
1. **Clic droit** sur le fichier
2. Sélectionnez **"Exécuter"** ou **"Lancer"**

#### Méthode en ligne de commande

```bash
./nom-du-fichier.AppImage
```

Exemple :
```bash
./GIMP-latest.AppImage
```

**Note** : Le `./` signifie "dans le dossier actuel". Assurez-vous d'être dans le bon dossier avec `cd`.

## Organiser vos AppImages

Avec le temps, vous accumulerez plusieurs AppImages. Voici comment les organiser proprement.

### Créer un dossier dédié

**Recommandation** : Créez un dossier spécial pour vos AppImages.

```bash
mkdir ~/Applications
```

Ou créez-le graphiquement dans votre dossier personnel.

### Déplacer vos AppImages

Déplacez tous vos fichiers .AppImage dans ce dossier :

```bash
mv ~/Téléchargements/*.AppImage ~/Applications/
```

### Renommer pour plus de clarté

Les noms d'AppImage peuvent être complexes. Renommez-les de façon claire :

**Avant** : `Obsidian-1.4.16-x86_64.AppImage`
**Après** : `Obsidian.AppImage`

```bash
mv Obsidian-1.4.16-x86_64.AppImage Obsidian.AppImage
```

Ainsi, vous savez toujours quelle application c'est, quelle que soit la version.

## Intégrer les AppImages au système

Par défaut, les AppImages ne s'intègrent pas au menu. Voici comment les ajouter.

### Méthode 1 : AppImageLauncher (recommandée)

**AppImageLauncher** est un outil qui automatise l'intégration des AppImages.

#### Installation

```bash
sudo add-apt-repository ppa:appimagelauncher-team/stable
sudo apt update
sudo apt install appimagelauncher
```

#### Fonctionnement

Une fois installé, quand vous double-cliquez sur un AppImage :
1. AppImageLauncher vous demande si vous voulez l'intégrer
2. Si vous acceptez, il :
   - Déplace l'AppImage dans `~/Applications`
   - Crée une entrée dans le menu
   - Ajoute une icône
   - Gère les mises à jour

#### Désinstaller une AppImage avec AppImageLauncher

```bash
appimagelauncher-lite --remove nom-de-lapplication
```

Ou supprimez simplement le fichier, l'entrée du menu sera supprimée automatiquement.

### Méthode 2 : Créer manuellement un lanceur

Si vous ne voulez pas installer AppImageLauncher, vous pouvez créer un lanceur manuellement.

#### Créer le fichier .desktop

```bash
nano ~/.local/share/applications/nom-application.desktop
```

#### Contenu du fichier

```desktop
[Desktop Entry]
Name=Nom de l'Application
Comment=Description de l'application
Exec=/chemin/complet/vers/application.AppImage
Icon=/chemin/vers/icone.png
Type=Application
Categories=Utility;
Terminal=false
```

**Exemple concret pour Obsidian** :

```desktop
[Desktop Entry]
Name=Obsidian
Comment=Éditeur de notes Markdown
Exec=/home/votre-nom/Applications/Obsidian.AppImage
Icon=/home/votre-nom/Applications/obsidian.png
Type=Application
Categories=Office;
Terminal=false
```

#### Rendre le fichier exécutable

```bash
chmod +x ~/.local/share/applications/nom-application.desktop
```

#### Actualiser le menu

```bash
update-desktop-database ~/.local/share/applications/
```

L'application apparaît maintenant dans votre menu !

## Mettre à jour un AppImage

Les AppImages ne se mettent pas à jour automatiquement. Voici comment faire.

### Méthode manuelle (standard)

1. **Téléchargez** la nouvelle version depuis le site officiel
2. **Supprimez** l'ancienne version (ou renommez-la en backup)
3. **Remplacez** par la nouvelle
4. **Rendez exécutable** si nécessaire

### AppImages avec mise à jour intégrée

Certains AppImages incluent un système de mise à jour. Au lancement, ils vérifient et proposent de se mettre à jour.

**Exemples** :
- Kdenlive AppImage
- Krita AppImage
- Certains éditeurs de code

### Utiliser AppImageUpdate

**AppImageUpdate** est un outil qui peut mettre à jour les AppImages compatibles.

#### Installation

```bash
wget https://github.com/AppImage/AppImageUpdate/releases/download/continuous/appimageupdatetool-x86_64.AppImage
chmod +x appimageupdatetool-x86_64.AppImage
```

#### Utilisation

```bash
./appimageupdatetool-x86_64.AppImage /chemin/vers/votre-application.AppImage
```

**Note** : Cela ne fonctionne que si l'AppImage contient des informations de mise à jour.

### Vérifier manuellement

Ajoutez un rappel dans votre calendrier pour vérifier les mises à jour tous les mois.

## Extraire le contenu d'un AppImage

Parfois, vous voulez voir ce qu'il y a dans un AppImage sans l'exécuter.

### Extraire

```bash
./nom-du-fichier.AppImage --appimage-extract
```

Cela crée un dossier `squashfs-root` contenant tout le contenu de l'AppImage.

### Pourquoi extraire ?

- **Curiosité** : Voir ce que contient l'application
- **Récupérer des fichiers** : Icônes, bibliothèques, etc.
- **Débogage** : Comprendre pourquoi une AppImage ne fonctionne pas
- **Modification** : Personnaliser l'application (avancé)

## Applications populaires en AppImage

Voici des applications courantes disponibles en AppImage :

### Bureautique et productivité
- **Obsidian** : Prise de notes en Markdown
- **Joplin** : Application de notes open source
- **Standard Notes** : Notes cryptées
- **Calibre** : Gestion de bibliothèque d'e-books

### Multimédia
- **Krita** : Peinture numérique
- **Kdenlive** : Montage vidéo
- **Audacity** : Édition audio
- **OpenShot** : Montage vidéo simple
- **Subsurface** : Carnet de plongée

### Développement
- **Arduino IDE** : Développement pour Arduino
- **Etcher** : Création de clés USB bootables
- **GitKraken** : Client Git graphique
- **Sublime Text** : Éditeur de texte/code

### Utilitaires
- **Bitwarden** : Gestionnaire de mots de passe
- **Nextcloud** : Client de synchronisation cloud
- **Cryptomator** : Chiffrement de fichiers

### Jeux
- **Mindustry** : Jeu de stratégie
- **SuperTux** : Platformer comme Super Mario
- Divers émulateurs

## AppImage vs autres formats

Récapitulatif pour savoir quand utiliser AppImage :

| Critère | .deb | Flatpak | Snap | AppImage |
|---------|------|---------|------|----------|
| Installation | Requise | Requise | Requise | ❌ Aucune |
| Privilèges root | ✅ Requis | ❌ Optionnel | ✅ Requis | ❌ Non |
| Intégration menu | ✅ Auto | ✅ Auto | ✅ Auto | ⚠️ Manuelle |
| Portabilité | ❌ Non | ❌ Non | ❌ Non | ✅ Totale |
| Mises à jour | ✅ Auto | ✅ Auto | ✅ Auto | ❌ Manuel |
| Taille | ✅ Petit | ❌ Grand | ❌ Grand | ❌ Grand |
| Versions multiples | ❌ Difficile | ⚠️ Possible | ❌ Difficile | ✅ Facile |
| Sécurité | ⚠️ Moyenne | ✅ Sandboxing | ✅ Sandboxing | ⚠️ Moyenne |

### Quand utiliser AppImage ?

✅ **Utilisez AppImage pour :**
- Tester rapidement une application
- Utiliser une application occasionnellement
- Avoir plusieurs versions d'un même logiciel
- Utiliser une application sur plusieurs ordinateurs (clé USB)
- Quand l'application n'est disponible qu'en AppImage
- Éviter de modifier votre système

❌ **N'utilisez PAS AppImage pour :**
- Applications système importantes
- Applications que vous utilisez quotidiennement
- Si une version .deb ou Flatpak existe et fonctionne bien
- Si vous voulez des mises à jour automatiques

## Sécurité et AppImage

### Risques potentiels

AppImage n'a pas de système de vérification centralisé comme les dépôts officiels.

**Risques** :
- Télécharger un AppImage malveillant
- Pas de sandboxing par défaut
- Accès complet à vos fichiers

### Bonnes pratiques

1. ✅ **Téléchargez uniquement depuis des sources fiables**
   - Site officiel du projet
   - GitHub releases du projet officiel
   - AppImageHub (vérifiez toujours la source)

2. ✅ **Vérifiez les checksums**
   - Si fournis, vérifiez que le fichier n'a pas été modifié
   ```bash
   sha256sum fichier.AppImage
   ```
   Comparez avec le checksum officiel

3. ✅ **Lisez les commentaires et avis**
   - Sur AppImageHub
   - Sur les forums Linux

4. ✅ **Soyez prudent avec les permissions**
   - Un AppImage a les mêmes droits que votre utilisateur
   - Ne lancez JAMAIS un AppImage inconnu avec sudo

5. ❌ **Évitez les sources douteuses**
   - Sites de téléchargement génériques
   - Liens dans des forums non vérifiés
   - AppImages de provenance inconnue

### Firejail : Exécuter un AppImage en sandbox

Pour plus de sécurité, vous pouvez utiliser Firejail :

```bash
sudo apt install firejail
firejail ./nom-du-fichier.AppImage
```

Firejail crée un environnement isolé pour l'AppImage.

## Supprimer un AppImage

### Suppression simple

Pour supprimer un AppImage :
1. Supprimez le fichier .AppImage
```bash
rm ~/Applications/nom-application.AppImage
```

2. Si vous avez créé un lanceur manuellement, supprimez-le :
```bash
rm ~/.local/share/applications/nom-application.desktop
```

3. Supprimez les fichiers de configuration (optionnel) :
```bash
rm -rf ~/.config/nom-application
```

### Avec AppImageLauncher

Si vous utilisez AppImageLauncher :
1. Supprimez simplement le fichier AppImage
2. AppImageLauncher nettoie automatiquement les entrées du menu

## Dépannage

### L'AppImage ne se lance pas

**Vérifiez les permissions** :
```bash
ls -l fichier.AppImage
```
Doit afficher : `-rwxr-xr-x` (le `x` indique exécutable)

**Rendez exécutable** :
```bash
chmod +x fichier.AppImage
```

### Erreur "FUSE not found"

Certains vieux systèmes nécessitent FUSE2 :
```bash
sudo apt install libfuse2
```

### L'AppImage se lance mais plante

**Lancez depuis le terminal** pour voir les erreurs :
```bash
./fichier.AppImage
```

**Vérifiez la compatibilité** :
- Certains AppImages sont pour 64 bits uniquement
- Vérifiez les prérequis sur le site du projet

### L'application n'apparaît pas dans le menu

**Après création manuelle d'un lanceur** :
```bash
update-desktop-database ~/.local/share/applications/
```

**Ou utilisez AppImageLauncher** pour automatiser.

### L'icône ne s'affiche pas

Dans votre fichier .desktop, assurez-vous que le chemin vers l'icône est correct :
```desktop
Icon=/chemin/absolu/vers/icone.png
```

Vous pouvez extraire l'icône de l'AppImage :
```bash
./fichier.AppImage --appimage-extract
```
Puis cherchez dans `squashfs-root/` pour l'icône.

## Créer son propre AppImage (bonus)

Pour les curieux qui veulent créer leurs propres AppImages :

### Outils disponibles

**linuxdeploy** : Outil moderne de création d'AppImage
```bash
wget https://github.com/linuxdeploy/linuxdeploy/releases/download/continuous/linuxdeploy-x86_64.AppImage
chmod +x linuxdeploy-x86_64.AppImage
```

**appimagetool** : Outil classique
```bash
wget https://github.com/AppImage/AppImageKit/releases/download/continuous/appimagetool-x86_64.AppImage
chmod +x appimagetool-x86_64.AppImage
```

### Documentation

Pour apprendre à créer des AppImages :
- Documentation officielle : https://docs.appimage.org/
- Tutoriels : https://appimage.org/

## Ressources et communauté

### Sites utiles

- **AppImage.org** : Site officiel
- **AppImageHub** : Catalogue d'applications
- **GitHub AppImage** : Organisation officielle sur GitHub

### Trouver des AppImages

1. **AppImageHub** : https://www.appimagehub.com/
2. **GitHub Releases** : Cherchez "nom-projet releases"
3. **Sites officiels** : Section "Download" ou "Get"
4. **Recherche Google** : "nom-application appimage"

### Support

- Forums Linux Mint
- Reddit : r/linux, r/linuxquestions
- GitHub issues du projet AppImage

## Conclusion

AppImage est le format le plus simple pour utiliser des applications sous Linux. Sa philosophie "un fichier = une application" le rend accessible même aux débutants complets. Bien qu'il ne remplace pas les systèmes de paquets traditionnels pour une utilisation quotidienne, c'est un excellent complément pour tester des logiciels ou utiliser des applications portables.

### Points clés à retenir

- ⭐ **Aucune installation nécessaire** : Télécharger, rendre exécutable, lancer
- ⭐ **Portable** : Copiez sur une clé USB et utilisez partout
- ⭐ **Simple** : Le format le plus facile à comprendre
- ⭐ **Pas d'intégration automatique** : Nécessite AppImageLauncher ou configuration manuelle
- ⭐ **Pas de mises à jour automatiques** : Vous devez gérer manuellement
- ⭐ **Sécurité** : Téléchargez uniquement depuis des sources fiables
- ⭐ **Taille importante** : Chaque AppImage contient toutes ses dépendances

### Recommandations finales

**Pour débutants** :
1. Utilisez AppImageLauncher pour faciliter l'intégration
2. Organisez vos AppImages dans un dossier dédié
3. Ne téléchargez que depuis des sources officielles
4. Parfait pour tester des logiciels sans risque

**Hiérarchie recommandée** :
1. **.deb** (dépôts officiels) : Pour les applications quotidiennes
2. **Flatpak** : Pour les versions récentes avec mises à jour auto
3. **AppImage** : Pour tester, porter, ou utiliser occasionnellement
4. **Snap** : En dernier recours uniquement

**Usage idéal d'AppImage** : Applications que vous utilisez occasionnellement, tests de logiciels, versions portables, et situations où vous ne voulez pas modifier votre système.

---


⏭️ [Installation depuis les sources (.deb, compilation)](/06-gestion-des-logiciels/08-installation-depuis-les-sources.md)
