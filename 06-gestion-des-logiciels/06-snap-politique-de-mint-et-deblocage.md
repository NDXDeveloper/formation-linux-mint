🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.6 Snap : La politique de Mint et comment le débloquer

## Introduction

**Snap** est un système de gestion de paquets développé par Canonical (la société derrière Ubuntu). C'est un concurrent direct de Flatpak que nous avons vu au chapitre précédent. Comme Flatpak, Snap permet d'installer des applications isolées qui fonctionnent sur toutes les distributions Linux.

**La particularité sur Linux Mint** : Contrairement à Ubuntu qui privilégie Snap, **Linux Mint bloque activement Snap par défaut**. Ce n'est pas un oubli, c'est une décision délibérée de l'équipe de développement de Mint.

Dans ce chapitre, nous allons comprendre :
- Ce qu'est Snap
- Pourquoi Linux Mint le bloque
- Les arguments pour et contre
- Comment débloquer Snap si vous en avez vraiment besoin
- Les alternatives recommandées

## Qu'est-ce que Snap ?

### Définition

**Snap** est un format de paquet universel créé par Canonical en 2016. Les paquets Snap (appelés "snaps") sont :
- **Conteneurisés** : Isolés du système comme les Flatpak
- **Universels** : Fonctionnent sur toutes les distributions Linux
- **Auto-suffisants** : Embarquent toutes leurs dépendances
- **Mis à jour automatiquement** : Par défaut, sans demander

### Le Snap Store

Le **Snap Store** est le magasin officiel d'applications Snap, géré exclusivement par Canonical. C'est l'équivalent de Flathub pour Flatpak, mais avec une différence majeure : il n'existe qu'un seul Snap Store officiel, propriété de Canonical.

### Similitudes avec Flatpak

Snap et Flatpak partagent beaucoup de caractéristiques :
- Isolation des applications (sandboxing)
- Universalité sur toutes les distributions
- Applications auto-suffisantes
- Versions souvent plus récentes que les dépôts officiels
- Taille plus importante que les paquets traditionnels

### Différences avec Flatpak

| Critère | Snap | Flatpak |
|---------|------|---------|
| Créateur | Canonical (Ubuntu) | Communauté open source |
| Backend | Propriétaire (fermé) | Open source |
| Magasin principal | Snap Store (unique, Canonical) | Flathub (ouvert, communautaire) |
| Mises à jour auto | Oui (imposées) | Optionnel |
| Performance | Plus lent au démarrage | Plus rapide |
| Intégration | Bonne sur Ubuntu | Meilleure globalement |
| Format de compression | SquashFS | OSTree |

## Pourquoi Linux Mint bloque Snap

Linux Mint ne bloque pas Snap par caprice. Il y a des raisons techniques, philosophiques et pratiques bien documentées.

### 1. Le backend propriétaire

**Le problème** : Le serveur Snap Store est propriétaire et fermé. Seul Canonical contrôle ce serveur.

**Conséquence** :
- Vous ne pouvez pas créer votre propre Snap Store
- Toutes les applications Snap passent obligatoirement par les serveurs de Canonical
- Canonical peut décider ce qui est disponible ou non
- En cas de problème avec Canonical, vous perdez l'accès

**Position de Mint** : C'est contraire à la philosophie du logiciel libre où chacun devrait pouvoir héberger ses propres dépôts.

### 2. Installation silencieuse sur Ubuntu

**Le problème** : Sur Ubuntu, certaines applications .deb installent secrètement Snap sans votre consentement.

**Exemple concret** : Sur Ubuntu, si vous tapez `sudo apt install chromium`, vous n'installez PAS le vrai Chromium en .deb, mais un paquet factice qui installe la version Snap sans vous prévenir.

**Position de Mint** : Les utilisateurs doivent avoir le contrôle et savoir ce qui s'installe sur leur système.

### 3. Mises à jour automatiques forcées

**Le problème** : Les Snaps se mettent à jour automatiquement, sans demander la permission.

**Conséquence** :
- Vous ne choisissez pas quand mettre à jour
- Une mise à jour peut casser votre workflow en plein travail
- Difficile de contrôler les versions

**Position de Mint** : Les utilisateurs doivent garder le contrôle sur leur système.

### 4. Performance

**Le problème** : Les applications Snap sont souvent plus lentes au démarrage que leurs équivalents .deb ou Flatpak.

**Cause technique** : Le format SquashFS utilisé par Snap nécessite un montage de système de fichiers à chaque lancement.

**Conséquence** : Expérience utilisateur dégradée, surtout sur les machines moins puissantes.

### 5. Centralisation

**Le problème** : Un seul serveur central contrôlé par une entreprise.

**Risques** :
- Point de défaillance unique
- Dépendance envers Canonical
- Censure potentielle
- Problèmes de confidentialité

**Position de Mint** : La décentralisation est préférable pour la santé de l'écosystème Linux.

### La position officielle de Linux Mint

Voici ce que dit l'équipe Linux Mint dans leur blog officiel (résumé) :

> "Nous ne sommes pas contre l'idée de Snap en soi, mais contre la façon dont il est implémenté. Le backend propriétaire et les installations silencieuses vont à l'encontre de nos valeurs de transparence et de contrôle utilisateur. Nous recommandons Flatpak comme alternative libre et décentralisée."

## Le fichier nosnap.pref

### Qu'est-ce que c'est ?

Le fichier **nosnap.pref** est un petit fichier de configuration que Linux Mint a ajouté pour bloquer activement l'installation de Snap.

**Emplacement** : `/etc/apt/preferences.d/nosnap.pref`

**Contenu** :
```
Package: snapd
Pin: release a=*
Pin-Priority: -1
```

**Explication** :
- `Package: snapd` : Cible le paquet snapd (le démon Snap)
- `Pin-Priority: -1` : Donne une priorité négative, ce qui bloque l'installation

### Comment ça fonctionne ?

Ce fichier empêche APT d'installer le paquet `snapd` (le moteur Snap) même si vous essayez de le faire. Si vous tapez `sudo apt install snapd`, vous obtiendrez une erreur.

## Devriez-vous débloquer Snap ?

Avant de débloquer Snap, posez-vous ces questions :

### ✅ Débloquez Snap si :

1. **Une application critique n'existe QUE en Snap**
   - Vérifiez d'abord qu'elle n'existe pas en .deb, Flatpak ou AppImage

2. **Vous avez des besoins spécifiques liés à Ubuntu**
   - Développement d'applications pour Ubuntu
   - Tests de compatibilité

3. **Vous comprenez les implications**
   - Vous acceptez la centralisation
   - Vous acceptez les mises à jour automatiques
   - Vous savez ce que vous faites

### ❌ NE débloquez PAS Snap si :

1. **Vous pouvez obtenir l'application autrement**
   - Vérifiez les dépôts officiels (.deb)
   - Cherchez sur Flathub (Flatpak)
   - Regardez les AppImage
   - Cherchez un PPA fiable

2. **Vous débutez sur Linux**
   - Commencez par maîtriser .deb et Flatpak
   - Snap ajoute de la complexité inutile

3. **Vous voulez le meilleur pour votre système**
   - Mint a bloqué Snap pour de bonnes raisons
   - Flatpak est une meilleure alternative dans la plupart des cas

### Questions à se poser

Avant de débloquer :
1. **L'application existe-t-elle en .deb ?** → Utilisez .deb
2. **L'application existe-t-elle en Flatpak ?** → Utilisez Flatpak
3. **L'application existe-t-elle en AppImage ?** → Utilisez AppImage
4. **Aucune alternative ?** → Alors seulement, considérez Snap

## Comment débloquer Snap

⚠️ **AVERTISSEMENT** : En débloquant Snap, vous allez à l'encontre de la politique de Linux Mint. Procédez uniquement si vous êtes sûr d'en avoir besoin.

### Étape 1 : Supprimer le fichier de blocage

```bash
sudo rm /etc/apt/preferences.d/nosnap.pref
```

Cette commande supprime le fichier qui bloque Snap.

### Étape 2 : Mettre à jour la liste des paquets

```bash
sudo apt update
```

### Étape 3 : Installer snapd

```bash
sudo apt install snapd
```

### Étape 4 : Activer le service (optionnel)

Sur certaines installations, il faut activer le service manuellement :

```bash
sudo systemctl enable --now snapd.socket
```

### Étape 5 : Ajouter Snap au PATH (optionnel)

Pour que les applications Snap soient accessibles depuis le terminal :

```bash
echo 'export PATH=$PATH:/snap/bin' >> ~/.bashrc
source ~/.bashrc
```

### Étape 6 : Redémarrer (recommandé)

Pour que tous les changements prennent effet :

```bash
sudo reboot
```

### Vérifier que Snap fonctionne

```bash
snap version
```

Vous devriez voir la version de Snap installée.

## Utiliser Snap

Une fois Snap débloqué et installé, voici comment l'utiliser.

### Rechercher des applications

```bash
snap find nom-application
```

Exemple :
```bash
snap find spotify
```

### Installer une application

```bash
sudo snap install nom-application
```

Exemple :
```bash
sudo snap install spotify
```

### Lister les snaps installés

```bash
snap list
```

### Mettre à jour un snap

```bash
sudo snap refresh nom-application
```

### Mettre à jour tous les snaps

```bash
sudo snap refresh
```

### Désinstaller un snap

```bash
sudo snap remove nom-application
```

### Voir les informations d'un snap

```bash
snap info nom-application
```

## Gérer les mises à jour automatiques

Par défaut, Snap met à jour automatiquement vos applications. Voici comment le gérer.

### Désactiver les mises à jour automatiques (temporaire)

```bash
sudo snap set system refresh.hold="$(date --iso-8601=seconds -d '30 days')"
```

Met en pause les mises à jour pour 30 jours.

### Voir le statut des mises à jour

```bash
snap refresh --time
```

### Forcer une mise à jour immédiate

```bash
sudo snap refresh
```

### Retourner à une version précédente

```bash
sudo snap revert nom-application
```

⚠️ **Note** : Contrairement à Flatpak, il est plus difficile de contrôler finement les mises à jour avec Snap.

## Les canaux Snap

Les applications Snap peuvent avoir plusieurs versions disponibles via des "canaux".

### Les différents canaux

- **stable** : Version stable recommandée (par défaut)
- **candidate** : Version candidate, presque stable
- **beta** : Version beta, peut avoir des bugs
- **edge** : Version de développement, instable

### Installer depuis un canal spécifique

```bash
sudo snap install nom-application --channel=edge
```

### Changer de canal

```bash
sudo snap refresh nom-application --channel=beta
```

## Problèmes courants et solutions

### Snap prend beaucoup d'espace

**Problème** : Les applications Snap sont volumineuses.

**Solution** :
- Désinstallez les snaps inutilisés
- Nettoyez les anciennes versions :
```bash
sudo snap set system refresh.retain=2
```

### Les applications Snap sont lentes au démarrage

**Problème** : Nature de la technologie SquashFS.

**Solution** :
- Aucune vraiment, c'est inhérent à Snap
- Si la performance est critique, utilisez .deb ou Flatpak

### Les snaps utilisent des boucles de montage

**Problème** : Chaque snap crée un périphérique en boucle, visible avec `df -h`.

**Solution** :
- C'est normal, vous pouvez les masquer :
```bash
alias df='df -x squashfs'
```

### Conflit avec AppArmor

**Problème** : Erreurs de permissions avec AppArmor.

**Solution** :
```bash
sudo systemctl restart snapd
```

## Comparaison objective : Snap vs Flatpak

Maintenant que vous connaissez les deux, voici une comparaison équitable :

### Avantages de Snap

- ✅ **Très populaire sur Ubuntu** : Support officiel
- ✅ **Grandes entreprises** : Support de Microsoft (VS Code), Spotify, etc.
- ✅ **Mises à jour vraiment automatiques** : Tout est géré
- ✅ **Support serveur** : Peut être utilisé sur des serveurs sans interface graphique
- ✅ **IoT** : Support pour l'Internet des objets

### Avantages de Flatpak

- ✅ **Open source complet** : Backend et frontend
- ✅ **Décentralisé** : N'importe qui peut créer un dépôt
- ✅ **Performances** : Démarrage plus rapide
- ✅ **Contrôle utilisateur** : Mises à jour optionnelles
- ✅ **Recommandé par Mint** : Meilleure intégration
- ✅ **Moins intrusif** : Ne modifie pas le système

### Pour Linux Mint spécifiquement

Sur Linux Mint, **Flatpak est le meilleur choix** :
- Intégration native
- Soutenu par l'équipe Mint
- Philosophie cohérente avec Mint
- Meilleures performances

## Désinstaller complètement Snap

Si vous avez testé Snap et voulez revenir en arrière :

### Étape 1 : Supprimer tous les snaps installés

```bash
snap list
```

Puis supprimez-les un par un :
```bash
sudo snap remove nom-application
```

Ou supprimez tout d'un coup (avec précaution) :
```bash
for snap in $(snap list | awk '{if (NR!=1) print $1}'); do
    sudo snap remove $snap
done
```

### Étape 2 : Supprimer snapd

```bash
sudo apt purge snapd
```

### Étape 3 : Nettoyer les dossiers

```bash
sudo rm -rf ~/snap
sudo rm -rf /snap
sudo rm -rf /var/snap
sudo rm -rf /var/lib/snapd
```

### Étape 4 : Recréer le fichier de blocage

```bash
sudo bash -c 'cat > /etc/apt/preferences.d/nosnap.pref << EOF
Package: snapd
Pin: release a=*
Pin-Priority: -1
EOF'
```

### Étape 5 : Mettre à jour

```bash
sudo apt update
```

Vous êtes revenu à l'état initial de Linux Mint.

## Applications populaires : .deb vs Flatpak vs Snap

Voici où trouver des applications populaires :

| Application | .deb | Flatpak | Snap | Recommandation |
|-------------|------|---------|------|----------------|
| Firefox | ✅ Dépôts | ✅ Flathub | ✅ Snap Store | .deb |
| Chromium | ❌ | ✅ Flathub | ✅ Snap Store | Flatpak |
| VS Code | ✅ .deb officiel | ✅ Flathub | ✅ Snap Store | .deb |
| Spotify | ✅ .deb officiel | ✅ Flathub | ✅ Snap Store | .deb |
| Discord | ✅ .deb officiel | ✅ Flathub | ✅ Snap Store | .deb ou Flatpak |
| VLC | ✅ Dépôts | ✅ Flathub | ✅ Snap Store | .deb |
| GIMP | ✅ Dépôts | ✅ Flathub | ✅ Snap Store | .deb ou Flatpak |
| LibreOffice | ✅ Préinstallé | ✅ Flathub | ✅ Snap Store | .deb |
| OBS Studio | ✅ PPA | ✅ Flathub | ✅ Snap Store | Flatpak ou PPA |

**Constat** : La plupart des applications sont disponibles en .deb ou Flatpak. Snap est rarement la seule option.

## Conclusion et recommandations

### Pour les débutants

**Recommandation** : **NE débloquiez PAS Snap**

Pourquoi ?
- Linux Mint l'a bloqué pour de bonnes raisons
- Flatpak fait exactement la même chose, en mieux
- Vous avez déjà .deb et Flatpak, c'est largement suffisant
- Ajouter Snap complique inutilement votre système

### Pour les utilisateurs avancés

**Recommandation** : **Débloquez seulement si vraiment nécessaire**

Critères :
- Une application n'existe QUE en Snap (vérifiez bien !)
- Vous développez pour Ubuntu et avez besoin de tester
- Vous comprenez les implications

### La hiérarchie recommandée

Quand vous cherchez une application, suivez cet ordre :

1. **Dépôts officiels (.deb)** → `apt install`
2. **Flatpak / Flathub** → `flatpak install`
3. **PPA de confiance** → `add-apt-repository`
4. **AppImage** → Téléchargement direct
5. **Snap** (en dernier recours) → Seulement si rien d'autre n'existe

### Respecter la philosophie de Mint

Linux Mint a fait le choix de bloquer Snap pour protéger ses utilisateurs et défendre certaines valeurs :
- Transparence
- Contrôle utilisateur
- Décentralisation
- Liberté de choix

En utilisant Mint, vous bénéficiez de ces choix réfléchis. Respectez-les sauf si vous avez une très bonne raison.

## Ressources supplémentaires

### Articles officiels

- Blog Linux Mint sur Snap : https://blog.linuxmint.com/?p=3766
- Documentation Snap : https://snapcraft.io/docs
- Documentation Flatpak : https://docs.flatpak.org/

### Communauté

Si vous hésitez entre Snap et Flatpak :
- Posez la question sur les forums Linux Mint
- Demandez conseil à la communauté
- Cherchez des retours d'expérience

### Alternatives à vérifier en premier

Avant de débloquer Snap, vérifiez toujours :
1. Site officiel du logiciel (souvent un .deb disponible)
2. Flathub.org (Flatpak)
3. Recherche dans les dépôts : `apt search nom`
4. AppImageHub.com
5. Compilation depuis les sources (pour les experts)

## Points clés à retenir

- ⭐ **Snap est bloqué par défaut sur Mint** pour des raisons valides
- ⭐ **Flatpak est l'alternative recommandée** par Linux Mint
- ⭐ **Le backend Snap est propriétaire**, contrôlé uniquement par Canonical
- ⭐ **Les mises à jour Snap sont forcées**, moins de contrôle utilisateur
- ⭐ **Débloquage possible** mais déconseillé pour les débutants
- ⭐ **Vérifiez toujours les alternatives** avant de débloquer Snap
- ⭐ **Respectez la philosophie de Mint** : transparence et contrôle

**Message final** : Snap n'est pas "mauvais" en soi, mais il ne correspond pas à la philosophie de Linux Mint. Flatpak offre les mêmes avantages sans les inconvénients. Dans 99% des cas, vous n'avez pas besoin de Snap sur Linux Mint.

---


⏭️ [AppImage](/06-gestion-des-logiciels/07-appimage.md)
