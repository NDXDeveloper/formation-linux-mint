🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.4 Les dépôts et PPA

## Introduction

Jusqu'à présent, nous avons installé des logiciels depuis le Gestionnaire de logiciels ou avec APT. Mais d'où viennent exactement tous ces logiciels ? La réponse : des **dépôts** (repositories).

Les dépôts sont comme des bibliothèques en ligne contenant des milliers de logiciels prêts à être installés. Par défaut, Linux Mint est configuré avec des dépôts officiels sûrs et testés. Mais vous pouvez ajouter d'autres sources pour accéder à des logiciels supplémentaires ou à des versions plus récentes.

**Analogie simple** : Imaginez que les dépôts sont des magasins. Linux Mint vous donne accès à des magasins officiels vérifiés. Les PPA sont comme des boutiques indépendantes qui peuvent proposer des produits différents ou plus récents, mais avec moins de garanties.

## Qu'est-ce qu'un dépôt ?

### Définition

Un **dépôt** (ou repository) est un serveur qui stocke des paquets logiciels organisés et catalogués. Quand vous installez un logiciel, votre système :
1. Consulte sa liste de dépôts
2. Cherche le logiciel dans ces dépôts
3. Télécharge le paquet depuis le serveur
4. L'installe sur votre machine

### Les fichiers de configuration

La liste de vos dépôts est stockée dans :
- `/etc/apt/sources.list` : Fichier principal
- `/etc/apt/sources.list.d/` : Dossier contenant des fichiers additionnels

**Note** : Vous n'avez généralement pas besoin de modifier ces fichiers directement. Des outils graphiques existent pour ça.

## Les différents types de dépôts

Linux Mint utilise plusieurs types de dépôts, classés par niveau de fiabilité.

### 1. Dépôts officiels Linux Mint

**Description** : Paquets créés, testés et maintenus par l'équipe Linux Mint.

**Contenu** :
- Applications spécifiques à Mint (Cinnamon, Nemo, Warpinator, etc.)
- Versions optimisées de logiciels Ubuntu
- Outils de configuration Mint

**Fiabilité** : ★★★★★ (Maximum)

**URL typique** : `http://packages.linuxmint.com/`

### 2. Dépôts officiels Ubuntu

**Description** : Paquets de la distribution Ubuntu sur laquelle Mint est basé.

**Sections principales** :
- **Main** : Logiciels libres officiellement supportés
- **Universe** : Logiciels libres maintenus par la communauté
- **Restricted** : Pilotes propriétaires nécessaires (NVIDIA, etc.)
- **Multiverse** : Logiciels non-libres (codecs, etc.)

**Fiabilité** : ★★★★★ (Maximum)

**URL typique** : `http://archive.ubuntu.com/ubuntu/`

### 3. Dépôts partenaires (Partners)

**Description** : Logiciels propriétaires de partenaires commerciaux.

**Exemples** :
- Skype
- Certains pilotes
- Logiciels commerciaux

**Fiabilité** : ★★★★☆ (Très bon, mais propriétaire)

### 4. Backports

**Description** : Versions plus récentes de logiciels, portées depuis des versions plus récentes d'Ubuntu.

**Usage** : Quand vous voulez une version plus récente d'un logiciel sans mettre à jour tout le système.

**Fiabilité** : ★★★☆☆ (Bon, mais peut introduire des incompatibilités)

### 5. PPA (Personal Package Archives)

**Description** : Dépôts personnels créés par des développeurs individuels ou des équipes.

**Fiabilité** : ★★☆☆☆ à ★★★★☆ (Variable selon la source)

Nous y reviendrons en détail plus loin.

## Gérer les sources de logiciels (interface graphique)

La façon la plus simple de gérer vos dépôts est d'utiliser l'outil graphique.

### Ouvrir le gestionnaire de sources

**Méthode 1 : Via le menu**
1. Menu → **Administration** → **Sources de logiciels**
2. Entrez votre mot de passe

**Méthode 2 : Via le Gestionnaire de mises à jour**
1. Ouvrez le Gestionnaire de mises à jour
2. Menu **Édition** → **Sources de logiciels**

### Interface du gestionnaire

L'outil se compose de plusieurs onglets :

#### Onglet "Dépôts officiels"

Vous voyez les dépôts principaux :
- **Dépôts Linux Mint** : À toujours laisser activés
- **Base Ubuntu** : Les quatre sections (main, universe, restricted, multiverse)

**Conseil** : Laissez tous les dépôts officiels activés, ils sont tous sûrs.

#### Onglet "Dépôts supplémentaires"

Liste de tous les dépôts additionnels que vous avez ajoutés (PPA, dépôts tiers).

Vous pouvez :
- **Cocher/décocher** : Activer ou désactiver temporairement un dépôt
- **Modifier** : Changer l'URL ou les paramètres
- **Supprimer** : Retirer définitivement un dépôt

#### Onglet "Clés d'authentification"

Les clés GPG qui vérifient l'authenticité des paquets. Ne touchez à cet onglet que si vous savez ce que vous faites.

#### Onglet "Maintenance"

Options de nettoyage et de suppression de dépôts obsolètes.

### Changer de miroir

Un **miroir** est une copie d'un dépôt hébergée sur un serveur différent. Choisir un miroir proche de vous améliore la vitesse de téléchargement.

**Comment changer de miroir :**
1. Onglet **"Dépôts officiels"**
2. Cliquez sur le bouton à côté de "Miroir principal"
3. Choisissez un pays proche ou cliquez sur **"Chercher le meilleur miroir"**
4. Le système teste automatiquement les vitesses
5. Sélectionnez le miroir le plus rapide
6. Cliquez sur **"Appliquer"**

## Qu'est-ce qu'un PPA ?

### Définition

**PPA** signifie **Personal Package Archive** (Archive de Paquets Personnelle).

C'est un dépôt hébergé sur Launchpad (la plateforme Ubuntu) qui permet à des développeurs de distribuer leurs logiciels ou des versions plus récentes que celles des dépôts officiels.

### Pourquoi utiliser un PPA ?

**Avantages** :
- Accès à des versions plus récentes de logiciels
- Installation de logiciels non disponibles dans les dépôts officiels
- Mises à jour automatiques comme pour les logiciels officiels
- Installation et gestion faciles

**Cas d'usage typiques** :
- Obtenir la dernière version d'OBS Studio
- Installer une version récente de GIMP avec les nouvelles fonctionnalités
- Ajouter des pilotes graphiques plus récents

### Risques et précautions

⚠️ **IMPORTANT** : Les PPA ne sont PAS vérifiés par Linux Mint ou Ubuntu.

**Risques potentiels** :
- **Stabilité** : Peut contenir des bugs ou casser votre système
- **Sécurité** : Théoriquement, un PPA malveillant pourrait nuire à votre système
- **Conflits** : Peut entrer en conflit avec d'autres paquets
- **Maintenance** : Le développeur peut abandonner le PPA sans prévenir

**Règles de sécurité** :
1. ✅ N'ajoutez un PPA que si vous en avez vraiment besoin
2. ✅ Vérifiez la réputation du développeur ou du projet
3. ✅ Privilégiez les PPA officiels de projets connus
4. ✅ Lisez les commentaires et avis d'autres utilisateurs
5. ✅ Créez une sauvegarde Timeshift avant d'ajouter un PPA important
6. ❌ N'ajoutez JAMAIS un PPA sans savoir ce qu'il contient
7. ❌ Évitez les PPA de sources inconnues ou douteuses

## Ajouter un PPA

Il existe deux méthodes principales pour ajouter un PPA.

### Méthode 1 : En ligne de commande (la plus courante)

Les PPA ont un format standard : `ppa:utilisateur/nom-du-ppa`

**Syntaxe** :
```bash
sudo add-apt-repository ppa:utilisateur/nom-du-ppa  
sudo apt update  
```

**Exemple réel - Ajouter le PPA d'OBS Studio** :
```bash
sudo add-apt-repository ppa:obsproject/obs-studio  
sudo apt update  
sudo apt install obs-studio  
```

**Explication des étapes** :
1. `sudo add-apt-repository ppa:...` : Ajoute le PPA à votre liste de sources
2. `sudo apt update` : Rafraîchit la liste des paquets pour inclure le nouveau dépôt
3. `sudo apt install ...` : Installe le logiciel depuis le PPA

### Méthode 2 : Interface graphique

1. Ouvrez **Sources de logiciels**
2. Onglet **"Dépôts supplémentaires"**
3. Cliquez sur **"Ajouter un nouveau dépôt"**
4. Entrez l'adresse du PPA : `ppa:utilisateur/nom-du-ppa`
5. Cliquez sur **"OK"**
6. Le système télécharge la clé d'authentification
7. Rafraîchissez la liste : cliquez sur **"Recharger le cache"** ou faites `sudo apt update`

### Vérifier qu'un PPA est bien ajouté

```bash
ls /etc/apt/sources.list.d/
```

Vous devriez voir un fichier correspondant à votre PPA.

### Installer depuis le PPA

Une fois le PPA ajouté et la liste mise à jour :

```bash
sudo apt install nom-du-logiciel
```

Le système installera automatiquement la version du PPA si elle est plus récente que celle des dépôts officiels.

## Supprimer un PPA

Si vous n'utilisez plus un PPA ou s'il pose problème, vous pouvez le supprimer.

### Méthode 1 : En ligne de commande

```bash
sudo add-apt-repository --remove ppa:utilisateur/nom-du-ppa  
sudo apt update  
```

**Exemple** :
```bash
sudo add-apt-repository --remove ppa:obsproject/obs-studio  
sudo apt update  
```

### Méthode 2 : Interface graphique

1. Ouvrez **Sources de logiciels**
2. Onglet **"Dépôts supplémentaires"**
3. Sélectionnez le PPA à supprimer
4. Cliquez sur **"Supprimer"**
5. Confirmez

### Supprimer aussi les logiciels installés depuis le PPA

Supprimer un PPA ne supprime PAS les logiciels installés depuis ce PPA. Pour revenir aux versions officielles :

1. **Option 1 - Supprimer le logiciel** :
```bash
sudo apt remove nom-du-logiciel
```

2. **Option 2 - Revenir à la version officielle** :
```bash
sudo apt install nom-du-logiciel
```
APT installera automatiquement la version des dépôts officiels.

3. **Option 3 - Forcer le retour à une version spécifique** :
```bash
sudo apt install nom-du-logiciel=version-officielle
```

### Outil PPA Purge

Pour supprimer complètement un PPA et tous ses paquets :

```bash
sudo apt install ppa-purge  
sudo ppa-purge ppa:utilisateur/nom-du-ppa  
```

Cet outil :
- Supprime le PPA
- Désinstalle les paquets spécifiques au PPA
- Réinstalle les versions officielles si disponibles

## Exemples de PPA populaires et utiles

Voici quelques PPA réputés et couramment utilisés :

### Graphics Drivers PPA (Pilotes graphiques)

```bash
sudo add-apt-repository ppa:graphics-drivers/ppa  
sudo apt update  
```
**Usage** : Pilotes NVIDIA les plus récents

### LibreOffice Fresh PPA

```bash
sudo add-apt-repository ppa:libreoffice/ppa  
sudo apt update  
```
**Usage** : Dernière version de LibreOffice

### OBS Studio

```bash
sudo add-apt-repository ppa:obsproject/obs-studio  
sudo apt update  
```
**Usage** : Dernière version d'OBS pour streaming/enregistrement

### Inkscape Stable

```bash
sudo add-apt-repository ppa:inkscape.dev/stable  
sudo apt update  
```
**Usage** : Version stable récente d'Inkscape

### GIMP

```bash
sudo add-apt-repository ppa:ubuntuhandbook1/gimp  
sudo apt update  
```
**Usage** : Version récente de GIMP

**⚠️ Rappel** : Même ces PPA réputés comportent des risques. Ajoutez-les uniquement si vous avez besoin de versions plus récentes.

## Ajouter des dépôts manuellement

Parfois, un projet ne propose pas de PPA mais fournit son propre dépôt.

### Structure d'une ligne de dépôt

```
deb [signed-by=/chemin/vers/cle.gpg] http://url-du-depot distribution composant
```

**Composants** :
- `deb` : Type de paquet
- `[signed-by=...]` : Clé de signature (optionnel mais recommandé)
- URL du dépôt
- Distribution (focal, jammy, vera, etc.)
- Composant (main, stable, etc.)

### Exemple : Ajouter le dépôt de Docker

**Étape 1 : Ajouter la clé GPG**
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

**Étape 2 : Ajouter le dépôt**
```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
```

**Étape 3 : Mettre à jour et installer**
```bash
sudo apt update  
sudo apt install docker-ce  
```

**Note** : Cette procédure est plus complexe. Suivez toujours les instructions officielles du projet.

## Gérer les clés GPG

Les clés GPG garantissent que les paquets proviennent bien de la source officielle et n'ont pas été modifiés.

### Lister les clés installées

```bash
apt-key list
```

ou (méthode moderne) :
```bash
ls /etc/apt/trusted.gpg.d/
```

### Ajouter une clé manuellement

Si vous avez téléchargé une clé :
```bash
sudo apt-key add fichier-cle.gpg
```

Ou depuis une URL :
```bash
wget -qO - https://example.com/key.gpg | sudo apt-key add -
```

### Supprimer une clé

```bash
sudo apt-key del ID-DE-LA-CLE
```

### Note importante sur apt-key

La commande `apt-key` est **dépréciée** (obsolète). La nouvelle méthode utilise des fichiers de clés dans `/usr/share/keyrings/` avec l'option `signed-by` dans les sources.

## Résoudre les problèmes courants

### Erreur : "NO_PUBKEY"

**Message complet** : `GPG error: ... NO_PUBKEY XXXXXXXX`

**Cause** : La clé GPG du dépôt n'est pas installée.

**Solution** :
```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys XXXXXXXX
```
Remplacez `XXXXXXXX` par l'ID de clé mentionné dans l'erreur.

### Erreur : "Release file is not valid yet"

**Cause** : L'horloge de votre système n'est pas à l'heure.

**Solution** :
```bash
sudo apt install ntpdate  
sudo ntpdate pool.ntp.org  
```

### Dépôt non accessible (404 Not Found)

**Cause** : Le dépôt a été supprimé ou l'URL a changé.

**Solution** :
1. Vérifiez sur le site officiel du projet
2. Supprimez le dépôt s'il n'existe plus
3. Cherchez une alternative

### Conflits de version

**Cause** : Plusieurs dépôts proposent le même paquet avec des versions différentes.

**Solution** :
```bash
apt policy nom-du-paquet
```
Cette commande montre toutes les versions disponibles et leur provenance. Choisissez la version souhaitée :
```bash
sudo apt install nom-du-paquet=version-souhaitée
```

## Bonnes pratiques

### Avant d'ajouter un dépôt ou PPA

1. ✅ **Cherchez d'abord dans les dépôts officiels** : Peut-être que le logiciel existe déjà
2. ✅ **Vérifiez la réputation** : Recherchez des avis et retours d'expérience
3. ✅ **Lisez la documentation** : Comprenez ce que vous allez installer
4. ✅ **Créez une sauvegarde Timeshift** : En cas de problème, vous pourrez revenir en arrière
5. ✅ **Vérifiez la compatibilité** : Le PPA est-il compatible avec votre version de Linux Mint ?

### Pendant l'utilisation

1. ✅ **Limitez le nombre de PPA** : Moins vous en avez, moins vous risquez de conflits
2. ✅ **Gardez une liste** : Notez quels PPA vous avez ajoutés et pourquoi
3. ✅ **Surveillez les mises à jour** : Les PPA peuvent mettre à jour fréquemment
4. ✅ **Testez après installation** : Vérifiez que tout fonctionne correctement

### Nettoyage régulier

1. ✅ **Supprimez les PPA inutilisés** : Si vous ne les utilisez plus
2. ✅ **Vérifiez les dépôts obsolètes** : Certains peuvent ne plus être maintenus
3. ✅ **Nettoyez les clés** : Supprimez les clés des dépôts retirés

## Alternatives aux PPA

Avant d'ajouter un PPA, considérez ces alternatives :

### 1. Flatpak

Les applications Flatpak sont isolées et ne nécessitent pas de PPA.

**Avantages** :
- Pas de risque de casser le système
- Versions récentes
- Universelles (fonctionnent sur toutes les distributions)

**Voir** : Chapitre suivant sur Flatpak

### 2. AppImage

Fichiers exécutables autonomes, aucune installation nécessaire.

**Avantages** :
- Aucune modification du système
- Facile à supprimer (juste effacer le fichier)
- Portable

### 3. Snap (bloqué par défaut sur Mint)

Linux Mint bloque Snap par défaut, mais vous pouvez le débloquer si nécessaire.

**Voir** : Chapitre 6.6 pour débloquer Snap

### 4. Compilation depuis les sources

Pour les utilisateurs avancés, compiler le logiciel vous-même.

**Avantages** :
- Version la plus récente
- Contrôle total

**Inconvénients** :
- Complexe
- Pas de mises à jour automatiques
- Peut être long

## Commandes utiles de gestion des dépôts

### Lister tous les dépôts actifs

```bash
grep -r --include '*.list' '^deb ' /etc/apt/sources.list /etc/apt/sources.list.d/
```

### Voir d'où vient un paquet

```bash
apt policy nom-du-paquet
```

### Lister tous les paquets d'un dépôt spécifique

```bash
apt list --installed | grep ppa-name
```

### Désactiver temporairement tous les PPA

Créer un script :
```bash
sudo sed -i 's/^deb/#deb/g' /etc/apt/sources.list.d/*.list  
sudo apt update  
```

Pour réactiver :
```bash
sudo sed -i 's/^#deb/deb/g' /etc/apt/sources.list.d/*.list  
sudo apt update  
```

## Sauvegarder et restaurer vos sources

### Sauvegarder votre configuration

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup  
sudo cp -r /etc/apt/sources.list.d /etc/apt/sources.list.d.backup  
```

### Restaurer depuis une sauvegarde

```bash
sudo cp /etc/apt/sources.list.backup /etc/apt/sources.list  
sudo cp -r /etc/apt/sources.list.d.backup/* /etc/apt/sources.list.d/  
sudo apt update  
```

## Cas pratique complet

Imaginons que vous voulez installer la dernière version de Kdenlive (éditeur vidéo).

### Étape 1 : Vérifier la version officielle

```bash
apt policy kdenlive
```

Vous voyez que la version officielle est 21.12, mais vous voulez la 23.08.

### Étape 2 : Chercher un PPA

Recherchez "kdenlive ppa" sur Internet. Vous trouvez le PPA officiel du projet.

### Étape 3 : Créer une sauvegarde

```bash
sudo timeshift --create --comments "Avant ajout PPA Kdenlive"
```

### Étape 4 : Ajouter le PPA

```bash
sudo add-apt-repository ppa:kdenlive/kdenlive-stable  
sudo apt update  
```

### Étape 5 : Installer ou mettre à jour

```bash
sudo apt install kdenlive
```

### Étape 6 : Vérifier la version

```bash
kdenlive --version
```

### Étape 7 : Tester

Lancez Kdenlive et vérifiez que tout fonctionne.

### Si problème : Annuler

```bash
sudo ppa-purge ppa:kdenlive/kdenlive-stable
```

Ou restaurez avec Timeshift.

## Conclusion

Les dépôts et PPA sont des outils puissants qui vous donnent accès à un univers de logiciels bien au-delà des dépôts officiels. Cependant, cette puissance vient avec une responsabilité : vous devez être prudent et réfléchi dans vos choix.

**Points clés à retenir :**

- Les **dépôts officiels** sont sûrs et suffisent pour la plupart des besoins
- Les **PPA** offrent plus de choix mais comportent des risques
- Toujours **vérifier la source** avant d'ajouter un PPA
- **Créer une sauvegarde** avant d'ajouter des dépôts importants
- **Nettoyer régulièrement** les dépôts inutilisés
- Considérer les **alternatives** (Flatpak, AppImage) avant d'ajouter un PPA
- En cas de doute, **utilisez les versions officielles**

**Règle d'or** : Moins de PPA = système plus stable et plus sûr.

Dans le prochain chapitre, nous découvrirons **Flatpak et Flathub**, une alternative moderne et sûre aux PPA pour obtenir des versions récentes de logiciels.

---


⏭️ [Flatpak et Flathub](/06-gestion-des-logiciels/05-flatpak-et-flathub.md)
