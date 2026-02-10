🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.5 Flatpak et Flathub

## Introduction

**Flatpak** est un système moderne d'installation de logiciels pour Linux. C'est une alternative aux paquets .deb traditionnels et aux PPA que nous avons vus précédemment. Contrairement aux PPA qui peuvent modifier votre système, Flatpak fonctionne dans un environnement isolé (comme une bulle de protection).

**Flathub** est le magasin principal d'applications Flatpak, un peu comme le Play Store pour Android ou l'App Store pour Apple. C'est là que vous trouverez des milliers d'applications prêtes à être installées.

**Analogie simple** : Si les paquets .deb sont comme des programmes qui s'installent directement dans votre maison (votre système), les Flatpak sont comme des programmes qui vivent dans leur propre petit appartement séparé. Ils ne peuvent pas toucher au reste de votre maison, ce qui est plus sûr.

## Qu'est-ce que Flatpak ?

### Définition

**Flatpak** est un système de gestion de paquets universel pour Linux. Les applications Flatpak sont **conteneurisées**, c'est-à-dire isolées du reste du système dans leur propre environnement.

### Les principes de base

1. **Universalité** : Un Flatpak fonctionne sur toutes les distributions Linux (Ubuntu, Fedora, Arch, Mint, etc.)
2. **Isolation** : Chaque application est dans son propre "conteneur" sécurisé
3. **Runtime** : Les applications partagent des bibliothèques communes appelées "runtimes"
4. **Sandboxing** : Les applications ont des permissions limitées pour protéger votre système

### Pourquoi Flatpak existe ?

Avant Flatpak, chaque distribution Linux avait son propre système de paquets :
- Debian/Ubuntu/Mint : .deb
- Fedora/Red Hat : .rpm
- Arch : .pkg.tar.xz

Les développeurs devaient créer un paquet différent pour chaque distribution. Avec Flatpak, **un seul paquet fonctionne partout**.

## Avantages de Flatpak

### Pour les utilisateurs

1. **Sécurité renforcée** : Applications isolées qui ne peuvent pas nuire au système
2. **Versions récentes** : Souvent plus à jour que les dépôts officiels
3. **Pas de conflit** : N'interfère pas avec les paquets système
4. **Facilité** : Installation simple depuis Flathub
5. **Mises à jour indépendantes** : Peuvent être mises à jour sans mettre à jour le système
6. **Réversibilité** : Facile à désinstaller complètement

### Pour les développeurs

1. **Un seul paquet pour toutes les distributions**
2. **Contrôle de l'environnement**
3. **Facilité de distribution**
4. **Pas de dépendances système complexes**

## Inconvénients de Flatpak

Il faut être honnête, Flatpak a aussi quelques inconvénients :

### Taille des applications

- **Plus volumineux** : Une application Flatpak peut faire 200-500 Mo là où un .deb fait 50 Mo
- **Raison** : Chaque application embarque ses propres bibliothèques
- **Impact** : Prend plus d'espace disque, téléchargements plus longs

### Intégration système

- **Thèmes** : Parfois, les applications Flatpak ne suivent pas votre thème système
- **Raccourcis clavier globaux** : Peuvent ne pas fonctionner
- **Accès fichiers** : Par défaut, accès limité à certains dossiers

### Performance

- **Démarrage** : Parfois légèrement plus lent au lancement
- **Mémoire** : Peut utiliser un peu plus de RAM

### Quand privilégier Flatpak ?

✅ **Utilisez Flatpak quand :**
- Vous voulez la dernière version d'une application
- L'application n'est pas dans les dépôts officiels
- Vous voulez plus de sécurité (isolation)
- Vous testez une application sans risque pour le système

❌ **Préférez les .deb quand :**
- L'application est disponible dans les dépôts officiels
- Vous avez peu d'espace disque
- Vous voulez la meilleure intégration système
- L'application est critique pour votre système

## Flatpak sur Linux Mint

### État par défaut

Sur Linux Mint, Flatpak est **installé par défaut** depuis la version 18.3, mais Flathub n'est pas activé automatiquement. Vous devez l'activer manuellement.

### Vérifier si Flatpak est installé

Ouvrez un terminal et tapez :
```bash
flatpak --version
```

Si vous voyez un numéro de version (par exemple : `Flatpak 1.14.4`), c'est installé.

Si ce n'est pas le cas, installez-le :
```bash
sudo apt install flatpak
```

## Activer Flathub

Flathub est le dépôt principal pour les applications Flatpak. C'est l'étape essentielle pour profiter pleinement de Flatpak.

### Méthode 1 : Via le Gestionnaire de logiciels (recommandée)

1. Ouvrez le **Gestionnaire de logiciels**
2. Menu **Édition** → **Préférences**
3. Dans l'onglet **Flatpak**, cochez **"Activer le support Flatpak"**
4. Cliquez sur **"Ajouter Flathub"** si le bouton apparaît
5. Fermez et rouvrez le Gestionnaire de logiciels

### Méthode 2 : En ligne de commande

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

**Explication** :
- `remote-add` : Ajoute un nouveau dépôt
- `--if-not-exists` : N'ajoute que s'il n'existe pas déjà
- `flathub` : Nom du dépôt
- URL : Adresse du dépôt Flathub

### Vérifier que Flathub est activé

```bash
flatpak remotes
```

Vous devriez voir une ligne contenant `flathub`.

## Chercher des applications sur Flathub

### Via le site web

1. Allez sur **https://flathub.org**
2. Utilisez la barre de recherche
3. Parcourez les catégories
4. Cliquez sur une application pour voir ses détails

Le site web Flathub affiche :
- Captures d'écran
- Description détaillée
- Permissions requises
- Commande d'installation
- Note et avis

### Via le Gestionnaire de logiciels

Une fois Flathub activé :
1. Ouvrez le **Gestionnaire de logiciels**
2. Recherchez une application normalement
3. Si disponible en Flatpak, vous verrez **"Flatpak"** ou **"Flathub"** dans la source

### Via la ligne de commande

```bash
flatpak search nom-application
```

Exemple :
```bash
flatpak search gimp
```

## Installer une application Flatpak

### Méthode 1 : Via le Gestionnaire de logiciels

1. Recherchez l'application
2. Si plusieurs versions sont disponibles (.deb et Flatpak), **choisissez celle marquée "Flatpak"**
3. Cliquez sur **"Installer"**
4. Entrez votre mot de passe
5. Attendez la fin de l'installation

**Note** : Les premières installations Flatpak peuvent être longues car le système doit télécharger les "runtimes" (bibliothèques partagées). Les installations suivantes seront plus rapides.

### Méthode 2 : Via le site Flathub

1. Sur **flathub.org**, trouvez votre application
2. Cliquez sur le bouton **"Install"**
3. Téléchargez le fichier **.flatpakref**
4. Ouvrez ce fichier (double-clic)
5. Le Gestionnaire de logiciels s'ouvre et propose l'installation
6. Cliquez sur **"Installer"**

### Méthode 3 : En ligne de commande

```bash
flatpak install flathub nom.de.lapplication
```

Exemple concret :
```bash
flatpak install flathub org.gimp.GIMP
```

**Format des noms** : Les applications Flatpak utilisent la notation inversée du nom de domaine (comme `org.gimp.GIMP` au lieu de juste `gimp`).

### Première installation : Les runtimes

Lors de votre première installation Flatpak, le système vous demandera d'installer un **runtime** (environnement d'exécution).

**Exemple** :
```
Required runtime for org.gimp.GIMP is not installed.  
Install runtime org.gnome.Platform/x86_64/45 from 'flathub'? [Y/n]:  
```

Tapez **Y** et appuyez sur Entrée. C'est normal et nécessaire.

**Qu'est-ce qu'un runtime ?**
Les runtimes sont des collections de bibliothèques partagées :
- **GNOME Platform** : Pour les applications GNOME
- **KDE Platform** : Pour les applications KDE
- **Freedesktop** : Pour les applications génériques

Une fois installé, le même runtime peut être utilisé par plusieurs applications, ce qui économise de l'espace.

## Lancer une application Flatpak

### Méthode 1 : Via le menu

Les applications Flatpak apparaissent dans votre menu principal comme n'importe quelle autre application. Cherchez-les et cliquez pour lancer.

### Méthode 2 : En ligne de commande

```bash
flatpak run nom.de.lapplication
```

Exemple :
```bash
flatpak run org.gimp.GIMP
```

## Mettre à jour les applications Flatpak

### Via le Gestionnaire de mises à jour

Les applications Flatpak apparaissent dans le Gestionnaire de mises à jour aux côtés des autres mises à jour.

1. Ouvrez le **Gestionnaire de mises à jour**
2. Les mises à jour Flatpak sont listées (marquées "Flatpak")
3. Installez-les comme les autres mises à jour

### En ligne de commande

**Mettre à jour toutes les applications Flatpak** :
```bash
flatpak update
```

**Mettre à jour une application spécifique** :
```bash
flatpak update nom.de.lapplication
```

**Voir les mises à jour disponibles sans installer** :
```bash
flatpak remote-ls --updates
```

## Désinstaller une application Flatpak

### Via le Gestionnaire de logiciels

1. Ouvrez le **Gestionnaire de logiciels**
2. Allez dans **"Applications installées"**
3. Trouvez l'application Flatpak
4. Cliquez sur **"Supprimer"**

### En ligne de commande

```bash
flatpak uninstall nom.de.lapplication
```

Exemple :
```bash
flatpak uninstall org.gimp.GIMP
```

**Supprimer aussi les données** :
```bash
flatpak uninstall --delete-data nom.de.lapplication
```

## Gérer les applications installées

### Lister toutes les applications Flatpak

```bash
flatpak list
```

Affiche toutes les applications et runtimes installés.

### Lister seulement les applications (sans les runtimes)

```bash
flatpak list --app
```

### Voir les détails d'une application

```bash
flatpak info nom.de.lapplication
```

### Voir l'espace utilisé

```bash
flatpak list --app --columns=name,size
```

## Nettoyer et optimiser

Avec le temps, des runtimes et des applications inutilisées peuvent s'accumuler.

### Supprimer les runtimes et dépendances inutilisés

```bash
flatpak uninstall --unused
```

Cette commande supprime :
- Les anciens runtimes qui ne sont plus nécessaires
- Les dépendances orphelines
- Les versions obsolètes

**Conseil** : Exécutez cette commande une fois par mois pour garder votre système propre.

### Voir l'espace disque utilisé

```bash
du -sh ~/.local/share/flatpak  
du -sh /var/lib/flatpak  
```

### Nettoyer le cache

```bash
flatpak repair --user  
flatpak repair --system  
```

## Gérer les permissions des applications

Un des grands avantages de Flatpak est le contrôle des permissions. Chaque application a des permissions limitées.

### Installer Flatseal (interface graphique pour les permissions)

**Flatseal** est un gestionnaire graphique de permissions Flatpak.

```bash
flatpak install flathub com.github.tchx84.Flatseal
```

**Utilisation** :
1. Lancez Flatseal depuis le menu
2. Sélectionnez une application dans la liste
3. Voyez et modifiez ses permissions :
   - Accès réseau
   - Accès fichiers
   - Accès périphériques (webcam, micro, etc.)
   - Variables d'environnement

### Voir les permissions en ligne de commande

```bash
flatpak info --show-permissions nom.de.lapplication
```

### Exemples de permissions

Une application peut avoir accès à :
- **Réseau** : Se connecter à Internet
- **Home** : Lire/écrire dans votre dossier personnel
- **Système de fichiers** : Accès à certains dossiers
- **Périphériques** : Webcam, microphone, USB
- **Session** : Bus de session D-Bus
- **X11** : Affichage graphique

## Applications populaires disponibles en Flatpak

Voici quelques applications courantes que vous pouvez installer via Flatpak :

### Bureautique et productivité
- **LibreOffice** : `org.libreoffice.LibreOffice`
- **OnlyOffice** : `org.onlyoffice.desktopeditors`
- **Joplin** : `net.cozic.joplin_desktop`
- **Obsidian** : `md.obsidian.Obsidian`

### Multimédia
- **VLC** : `org.videolan.VLC`
- **GIMP** : `org.gimp.GIMP`
- **Inkscape** : `org.inkscape.Inkscape`
- **Kdenlive** : `org.kde.kdenlive`
- **Audacity** : `org.audacityteam.Audacity`
- **Blender** : `org.blender.Blender`
- **OBS Studio** : `com.obsproject.Studio`

### Développement
- **Visual Studio Code** : `com.visualstudio.code`
- **Sublime Text** : `com.sublimetext.three`
- **Postman** : `com.getpostman.Postman`

### Communication
- **Discord** : `com.discordapp.Discord`
- **Telegram** : `org.telegram.desktop`
- **Slack** : `com.slack.Slack`
- **Signal** : `org.signal.Signal`
- **Zoom** : `us.zoom.Zoom`

### Utilitaires
- **Flatseal** : `com.github.tchx84.Flatseal` (gestion des permissions)
- **Extension Manager** : `com.mattjakeman.ExtensionManager`

## Flatpak vs autres formats

Comparons Flatpak avec les autres méthodes d'installation :

| Critère | .deb (APT) | Flatpak | Snap | AppImage |
|---------|-----------|---------|------|----------|
| Isolation | ❌ Non | ✅ Oui | ✅ Oui | ⚠️ Partielle |
| Taille | ✅ Petit | ❌ Grand | ❌ Grand | ⚠️ Moyen |
| Intégration | ✅ Parfaite | ⚠️ Bonne | ⚠️ Bonne | ❌ Limitée |
| Universalité | ❌ Non | ✅ Oui | ✅ Oui | ✅ Oui |
| Versions récentes | ❌ Souvent anciennes | ✅ Récentes | ✅ Récentes | ✅ Récentes |
| Mises à jour auto | ✅ Oui | ✅ Oui | ✅ Oui | ❌ Non |
| Sécurité | ⚠️ Moyenne | ✅ Haute | ✅ Haute | ⚠️ Moyenne |
| Performance | ✅ Excellent | ⚠️ Bon | ⚠️ Moyen | ✅ Bon |

**Verdict pour débutants** :
1. **Privilégiez les .deb** pour les applications système et courantes
2. **Utilisez Flatpak** pour avoir des versions récentes ou des applications non disponibles en .deb
3. **Évitez Snap** sur Mint (bloqué par défaut pour de bonnes raisons)
4. **AppImage** est pratique pour tester rapidement sans installation

## Comprendre la structure de Flatpak

### Où sont stockées les applications ?

**Applications système** (installées avec sudo) :
```
/var/lib/flatpak/
```

**Applications utilisateur** (installées sans sudo) :
```
~/.local/share/flatpak/
```

### Où sont les données des applications ?

Chaque application Flatpak stocke ses données dans :
```
~/.var/app/nom.de.lapplication/
```

Exemple : Les données de GIMP Flatpak sont dans :
```
~/.var/app/org.gimp.GIMP/
```

## Résoudre les problèmes courants

### L'application ne voit pas mes fichiers

**Problème** : Vous essayez d'ouvrir un fichier mais l'application ne le trouve pas.

**Cause** : Restrictions de permissions Flatpak.

**Solution** :
1. Installez Flatseal
2. Ouvrez Flatseal
3. Sélectionnez l'application
4. Dans "Filesystem", ajoutez le chemin vers votre dossier
5. Ou activez "All user files"

**Alternative en ligne de commande** :
```bash
flatpak override nom.de.lapplication --filesystem=/chemin/vers/dossier
```

### L'application n'utilise pas mon thème

**Problème** : L'application Flatpak a une apparence différente.

**Solution** :
```bash
flatpak install flathub org.gtk.Gtk3theme.NomDeVotreTheme
```

Ou donnez accès aux thèmes :
```bash
flatpak override --filesystem=~/.themes  
flatpak override --filesystem=~/.icons  
```

### L'installation échoue

**Problème** : Message d'erreur pendant l'installation.

**Solutions** :
1. Vérifiez votre connexion Internet
2. Mettez à jour Flatpak :
   ```bash
   flatpak update
   ```
3. Réparez l'installation :
   ```bash
   flatpak repair
   ```
4. Réinstallez Flathub :
   ```bash
   flatpak remote-delete flathub
   flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
   ```

### L'application est lente

**Causes possibles** :
- Premier lancement (normal)
- Trop de runtimes installés
- Problème de permissions

**Solutions** :
1. Attendez quelques secondes au premier lancement
2. Nettoyez les runtimes inutilisés :
   ```bash
   flatpak uninstall --unused
   ```

### Erreur de signature GPG

```bash
flatpak remote-modify --gpg-import=/path/to/key flathub
```

## Commandes avancées

### Installer depuis un fichier .flatpak

Si vous avez téléchargé un fichier .flatpak directement :
```bash
flatpak install fichier.flatpak
```

### Exécuter une application avec des options

```bash
flatpak run --command=sh nom.de.lapplication
```

Lance un terminal à l'intérieur du conteneur de l'application (utile pour le débogage).

### Voir les processus Flatpak en cours

```bash
flatpak ps
```

### Créer un raccourci personnalisé

Les raccourcis des applications Flatpak sont dans :
```
~/.local/share/applications/
```

### Installer depuis une branche spécifique

Certaines applications ont plusieurs versions (stable, beta) :
```bash
flatpak install flathub nom.de.lapplication//stable  
flatpak install flathub nom.de.lapplication//beta  
```

## Bonnes pratiques

### Pour les débutants

1. ✅ **Activez Flathub** dès le début pour avoir accès aux applications
2. ✅ **Privilégiez les .deb** quand disponibles dans les dépôts officiels
3. ✅ **Utilisez Flatpak** pour des applications non disponibles ou pour avoir des versions récentes
4. ✅ **Installez Flatseal** pour mieux contrôler les permissions
5. ✅ **Nettoyez régulièrement** avec `flatpak uninstall --unused`

### Gestion de l'espace disque

Si vous avez peu d'espace :
- Limitez le nombre d'applications Flatpak
- Privilégiez les .deb (plus légers)
- Nettoyez régulièrement
- Supprimez les runtimes inutilisés

### Sécurité

1. ✅ Vérifiez les permissions avant d'installer
2. ✅ Utilisez Flatseal pour limiter les accès
3. ✅ Téléchargez uniquement depuis Flathub officiel
4. ✅ Vérifiez que l'application est bien celle que vous cherchez

## Flatpak pour les développeurs (bonus)

Si vous êtes curieux de créer vos propres Flatpak :

### Installer Flatpak Builder

```bash
sudo apt install flatpak-builder
```

### Documentation officielle

Consultez : https://docs.flatpak.org/

### Manifeste de base

Un Flatpak se définit par un fichier manifest (JSON ou YAML) qui décrit :
- L'ID de l'application
- Le runtime utilisé
- Les permissions
- Comment compiler l'application
- Les dépendances

## Conclusion

Flatpak est une technologie moderne qui apporte de nombreux avantages, notamment en termes de sécurité et d'accès aux dernières versions. Bien qu'il ait quelques inconvénients (taille, intégration), c'est un excellent complément aux paquets .deb traditionnels.

**Points clés à retenir :**

- **Flatpak** = applications isolées dans leur propre conteneur
- **Flathub** = magasin principal d'applications Flatpak
- Activer Flathub est nécessaire pour profiter de Flatpak
- Plus volumineux que les .deb mais plus sûr
- Parfait pour avoir les dernières versions
- Utilisez **Flatseal** pour gérer les permissions
- Nettoyez régulièrement avec `flatpak uninstall --unused`

**Stratégie recommandée** :
- Applications système : .deb (dépôts officiels)
- Applications récentes/spécialisées : Flatpak
- En cas de doute : commencez par chercher en .deb

Dans le prochain chapitre, nous aborderons **Snap**, le format concurrent de Flatpak, et pourquoi Linux Mint le bloque par défaut (et comment le débloquer si besoin).

---


⏭️ [Snap : La politique de Mint et comment le débloquer (nosnap.pref)](/06-gestion-des-logiciels/06-snap-politique-de-mint-et-deblocage.md)
