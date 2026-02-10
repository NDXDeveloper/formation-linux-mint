🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.9 Gestion des dépendances cassées

## Introduction

Les **dépendances cassées** sont l'un des problèmes les plus frustrants que vous pouvez rencontrer sous Linux, surtout quand vous débutez. Vous essayez d'installer un logiciel et soudain... ça ne fonctionne plus. Des messages d'erreur cryptiques apparaissent, et vous ne savez pas quoi faire.

**Bonne nouvelle** : Ce problème, bien qu'ennuyeux, est presque toujours réparable. Dans ce chapitre, nous allons comprendre ce que sont les dépendances, pourquoi elles peuvent "casser", et surtout comment les réparer.

**Analogie** : Imaginez que vous voulez faire un gâteau (votre application). Pour ça, vous avez besoin de farine, d'œufs, de sucre (les dépendances). Si vous avez de la farine mais pas d'œufs, votre gâteau ne peut pas être fait : vous avez des "dépendances manquantes". Si vous avez des œufs périmés qui ne marchent plus bien avec votre recette, vous avez des "dépendances cassées".

## Qu'est-ce qu'une dépendance ?

### Définition simple

Une **dépendance** est un logiciel ou une bibliothèque dont un autre logiciel a besoin pour fonctionner.

**Exemples concrets** :
- VLC a besoin de bibliothèques pour lire les vidéos (codecs)
- GIMP a besoin de bibliothèques pour afficher son interface graphique (GTK)
- Firefox a besoin de bibliothèques réseau pour se connecter à Internet

### Les bibliothèques (libraries)

Les bibliothèques sont des morceaux de code réutilisables. Au lieu que chaque programme réinvente la roue, tous partagent les mêmes bibliothèques.

**Avantage** :
- Économie d'espace disque
- Moins de code dupliqué
- Mises à jour de sécurité centralisées

**Inconvénient** :
- Si une bibliothèque pose problème, elle affecte tous les programmes qui l'utilisent

### Chaîne de dépendances

Un programme peut avoir des dépendances, qui elles-mêmes ont des dépendances, créant une **chaîne**.

**Exemple** :
```
GIMP
├── GTK+ (interface graphique)
│   ├── GLib (fonctions de base)
│   └── Cairo (rendu graphique)
├── GEGL (traitement d'image)
│   └── babl (conversion de couleurs)
└── libpng (lecture PNG)
```

GIMP a donc des dépendances directes (GTK+, GEGL, libpng) et indirectes (GLib, Cairo, babl).

## Qu'est-ce qu'une dépendance cassée ?

### Dépendances cassées vs dépendances manquantes

**Dépendance manquante** :
- Le paquet nécessaire n'est pas installé du tout
- Facile à corriger : il suffit de l'installer

**Dépendance cassée** :
- Le paquet nécessaire est installé mais dans une mauvaise version
- Ou le paquet nécessaire est partiellement installé
- Ou il y a un conflit entre versions
- Plus compliqué à résoudre

### États possibles d'un paquet

Un paquet peut être dans plusieurs états :

- ✅ **Installé** : Tout va bien
- ⚠️ **Partiellement configuré** : Installation incomplète
- ⚠️ **Non configuré** : Installé mais pas configuré
- ❌ **Cassé** : État incohérent
- ❌ **Demi-installé** : Installation interrompue

## Causes courantes des dépendances cassées

### 1. Installation interrompue

**Scénario** : Vous installez un logiciel et :
- Votre ordinateur plante
- Vous fermez le terminal pendant l'installation
- La connexion Internet est coupée
- Vous forcez l'arrêt du gestionnaire de paquets

**Résultat** : Les paquets sont à moitié installés.

### 2. Mélange de sources incompatibles

**Scénario** :
- Vous avez ajouté des PPA incompatibles
- Vous mélangez des paquets de différentes versions d'Ubuntu
- Vous installez des .deb prévus pour une autre distribution

**Résultat** : Conflits de versions.

### 3. Suppression manuelle de fichiers

**Scénario** :
- Vous supprimez des fichiers dans `/usr/lib/` ou `/usr/bin/`
- Vous nettoyez "trop fort" avec des commandes dangereuses

**Résultat** : Des paquets pensent que des fichiers existent alors qu'ils ont été supprimés.

### 4. Mise à jour partielle échouée

**Scénario** :
- Une mise à jour système est interrompue
- Certains paquets sont mis à jour, d'autres non
- Incompatibilité de versions entre les paquets

**Résultat** : Le système est dans un état incohérent.

### 5. Installation forcée de .deb incompatibles

**Scénario** :
- Vous installez un .deb non prévu pour votre version de Mint
- Le .deb demande une version spécifique d'une bibliothèque

**Résultat** : Conflit de dépendances.

## Reconnaître les dépendances cassées

### Messages d'erreur typiques

Voici les messages que vous pourriez voir :

#### Message 1 : Dépendances non satisfaites

```
Les paquets suivants contiennent des dépendances non satisfaites :
 nom-paquet : Dépend: librairie-xyz (>= 2.0) mais 1.5 est installé
```

#### Message 2 : Paquets cassés

```
Vous pouvez lancer « apt --fix-broken install » pour corriger ces problèmes.  
Les paquets suivants contiennent des dépendances non satisfaites :  
```

#### Message 3 : Impossible d'installer

```
Impossible d'installer nom-paquet  
E: Dépendances cassées. Essayez 'apt --fix-broken install' sans paquet  
   (ou indiquez une solution).
```

#### Message 4 : Conflits

```
Les paquets suivants ont des dépendances non satisfaites :
 paquet-a : Est en conflit avec: paquet-b mais la version X.Y est installée
```

#### Message 5 : dpkg interrompu

```
E: dpkg a été interrompu. Il est nécessaire d'utiliser « sudo dpkg --configure -a » pour corriger le problème.
```

### Vérifier l'état des paquets

Pour voir s'il y a des problèmes :

```bash
dpkg -l | grep -E "^..r|^..c"
```

Les lettres en début de ligne indiquent l'état :
- `ii` : Installé correctement ✅
- `rc` : Supprimé mais configuration restante ⚠️
- `iU` : Non empaqueté ❌
- `iF` : Échec de configuration ❌

## Solutions : Du plus simple au plus avancé

Nous allons procéder par étapes, en commençant par les solutions les plus simples.

### Niveau 1 : La commande magique (souvent suffisante)

Cette commande résout 80% des problèmes de dépendances :

```bash
sudo apt install -f
```

**Explication** :
- `apt install` : Installe des paquets
- `-f` : Fix-broken (répare les cassés)
- Sans nom de paquet : Répare l'état actuel du système

**Ce que fait cette commande** :
- Détecte les dépendances manquantes
- Les télécharge et les installe
- Termine les installations incomplètes
- Résout les conflits simples

**Essayez toujours cette commande en premier !**

### Niveau 2 : Reconfigurer les paquets

Si des paquets sont partiellement configurés :

```bash
sudo dpkg --configure -a
```

**Explication** :
- `dpkg` : Gestionnaire de paquets bas niveau
- `--configure` : Configure les paquets
- `-a` : All (tous les paquets en attente)

**Ce que fait cette commande** :
- Termine la configuration de tous les paquets en attente
- Utile après une installation interrompue

**Séquence recommandée** :
```bash
sudo dpkg --configure -a  
sudo apt install -f  
```

### Niveau 3 : Nettoyer et mettre à jour

Parfois, le cache est corrompu. Nettoyons-le :

```bash
sudo apt clean  
sudo apt update  
sudo apt install -f  
```

**Explication** :
- `apt clean` : Supprime le cache des paquets téléchargés
- `apt update` : Rafraîchit la liste des paquets disponibles
- `apt install -f` : Répare les dépendances

### Niveau 4 : Forcer la suppression du paquet problématique

Si un paquet spécifique bloque tout :

#### Identifier le paquet problématique

Lisez les messages d'erreur pour identifier quel paquet pose problème.

#### Supprimer le paquet

```bash
sudo apt remove --purge nom-du-paquet-problematique  
sudo apt install -f  
```

Ou avec dpkg :

```bash
sudo dpkg --remove --force-remove-reinstreq nom-du-paquet  
sudo apt install -f  
```

**Attention** : Cela supprime le paquet. Vous pourrez le réinstaller après.

### Niveau 5 : Aptitude (gestionnaire intelligent)

**Aptitude** est un gestionnaire de paquets alternatif, souvent plus intelligent pour résoudre les conflits.

#### Installation

```bash
sudo apt install aptitude
```

#### Utilisation

```bash
sudo aptitude install nom-du-paquet
```

Aptitude vous proposera plusieurs solutions. Lisez-les attentivement et choisissez celle qui convient.

**Avantage** : Aptitude explore plusieurs scénarios de résolution.

### Niveau 6 : Downgrade (rétrograder)

Si une nouvelle version d'un paquet pose problème, revenez à l'ancienne.

#### Trouver les versions disponibles

```bash
apt policy nom-du-paquet
```

#### Installer une version spécifique

```bash
sudo apt install nom-du-paquet=version-specifique
```

**Exemple** :
```bash
sudo apt install firefox=95.0+build1-0ubuntu0.20.04.1
```

#### Empêcher la mise à jour automatique

```bash
sudo apt-mark hold nom-du-paquet
```

Pour autoriser à nouveau :
```bash
sudo apt-mark unhold nom-du-paquet
```

### Niveau 7 : Nettoyer les verrous

Si APT dit qu'il est "verrouillé" :

```bash
sudo rm /var/lib/apt/lists/lock  
sudo rm /var/cache/apt/archives/lock  
sudo rm /var/lib/dpkg/lock*  
sudo dpkg --configure -a  
sudo apt update  
```

**Attention** : Ne faites cela QUE si aucun gestionnaire de paquets n'est en cours d'exécution !

### Niveau 8 : Réinitialiser les sources

Si vos sources de logiciels sont corrompues :

#### Sauvegarder

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
```

#### Restaurer les sources par défaut

Ouvrez Sources de logiciels (interface graphique) et :
1. Désactivez tous les PPA suspects
2. Réinitialisez aux dépôts par défaut

Ou manuellement :
```bash
sudo software-sources
```

Puis :
```bash
sudo apt update  
sudo apt install -f  
```

### Niveau 9 : Vérifier l'intégrité des paquets

```bash
sudo dpkg --verify
```

Affiche les fichiers modifiés ou manquants.

Pour réinstaller un paquet corrompu :
```bash
sudo apt install --reinstall nom-du-paquet
```

### Niveau 10 : Solution nucléaire (dernier recours)

⚠️ **ATTENTION** : Ceci est destructif. À n'utiliser qu'en dernier recours.

#### Supprimer tous les paquets cassés

```bash
sudo dpkg --remove --force-remove-reinstreq $(dpkg -l | grep "^iU\|^iF" | awk '{print $2}')  
sudo apt update  
sudo apt install -f  
sudo apt upgrade  
```

#### Réinstaller ubuntu-desktop ou cinnamon-desktop

Si votre environnement de bureau est cassé :

```bash
sudo apt install --reinstall cinnamon-desktop-environment
```

Ou :
```bash
sudo apt install --reinstall ubuntu-desktop
```

## Cas pratiques et solutions

### Cas 1 : "E: dpkg was interrupted"

**Message complet** :
```
E: dpkg a été interrompu. Il est nécessaire d'utiliser « sudo dpkg --configure -a » pour corriger le problème.
```

**Solution** :
```bash
sudo dpkg --configure -a  
sudo apt install -f  
```

### Cas 2 : "Unmet dependencies"

**Message** :
```
The following packages have unmet dependencies:
 firefox : Depends: libgtk-3-0 (>= 3.24) but 3.22 is to be installed
```

**Solution** :
```bash
sudo apt update  
sudo apt install firefox  
```

Si ça ne marche pas :
```bash
sudo apt install libgtk-3-0  
sudo apt install firefox  
```

### Cas 3 : Installation .deb qui a cassé le système

**Scénario** : Vous avez installé un .deb et maintenant rien ne marche.

**Solution** :
```bash
# Identifier le paquet problématique (regardez les noms récents)
dpkg -l | tail -20

# Supprimer le paquet
sudo apt remove nom-du-paquet-problematique  
sudo apt install -f  

# Si nécessaire, purger complètement
sudo apt purge nom-du-paquet-problematique  
sudo apt autoremove  
```

### Cas 4 : Conflit entre PPA

**Message** :
```
The following packages have unmet dependencies:
 libc6 : Breaks: locales (< 2.31) but 2.30 is to be installed
```

**Solution** :
```bash
# Désactiver les PPA problématiques
sudo apt-add-repository --remove ppa:nom/ppa  
sudo apt update  
sudo apt install -f  
```

### Cas 5 : Système figé pendant une mise à jour

**Scénario** : Votre ordinateur a planté pendant une mise à jour.

**Solution** (au redémarrage) :
```bash
sudo dpkg --configure -a  
sudo apt clean  
sudo apt update  
sudo apt install -f  
sudo apt dist-upgrade  
```

### Cas 6 : "Package is in a very bad inconsistent state"

**Solution** :
```bash
sudo dpkg --remove --force-remove-reinstreq nom-du-paquet  
sudo apt install -f  
sudo apt install nom-du-paquet  
```

## Outils de diagnostic

### Vérifier l'état du système de paquets

```bash
sudo apt check
```

Affiche les problèmes détectés.

### Voir les paquets cassés

```bash
dpkg -l | grep ^..r
```

### Lister les dépendances d'un paquet

```bash
apt depends nom-du-paquet
```

### Voir quels paquets dépendent d'un paquet

```bash
apt rdepends nom-du-paquet
```

### Simuler une installation

```bash
apt install --dry-run nom-du-paquet
```

Montre ce qui serait fait sans réellement le faire.

### Debsums : Vérifier l'intégrité

```bash
sudo apt install debsums  
sudo debsums -c  
```

Vérifie que les fichiers installés correspondent aux checksums originaux.

## Prévention

Mieux vaut prévenir que guérir !

### Bonnes pratiques

1. ✅ **Créez des snapshots Timeshift réguliers**
   - Avant toute grosse installation
   - Avant d'ajouter des PPA
   - Une fois par semaine

2. ✅ **Ne mélangez pas les sources**
   - Évitez trop de PPA
   - N'installez pas de paquets d'autres distributions
   - Restez dans l'écosystème Linux Mint/Ubuntu

3. ✅ **Mettez à jour régulièrement**
   - Mais complètement
   - Ne laissez pas de mises à jour partielles

4. ✅ **Ne forcez jamais l'arrêt d'une installation**
   - Soyez patient
   - Laissez le processus se terminer

5. ✅ **Lisez avant de valider**
   - Regardez ce que APT va faire
   - Vérifiez les paquets qui vont être supprimés

6. ✅ **Utilisez les outils graphiques pour débuter**
   - Gestionnaire de logiciels
   - Gestionnaire de mises à jour
   - Moins de risques d'erreurs

### Signes avant-coureurs

Soyez vigilant si vous voyez :

- ⚠️ APT veut supprimer beaucoup de paquets importants
- ⚠️ Des messages d'avertissement répétés
- ⚠️ Des erreurs lors des mises à jour
- ⚠️ Des comportements étranges après une installation

**Réaction** : Arrêtez, ne forcez pas. Cherchez de l'aide ou faites machine arrière.

## Quand demander de l'aide

### Situations où il faut de l'aide

- Vous avez essayé toutes les solutions de ce chapitre
- Vous ne comprenez pas les messages d'erreur
- Le système devient instable
- Vous avez peur de faire pire

### Comment demander de l'aide efficacement

**Sur les forums** :

1. **Titre clair** : "Dépendances cassées après installation de X"

2. **Contexte** :
   - Version de Linux Mint
   - Ce que vous essayiez de faire
   - Ce qui s'est passé

3. **Messages d'erreur complets** :
```bash
sudo apt install -f 2>&1 | tee ~/erreur-apt.txt
```
Puis partagez le contenu de `~/erreur-apt.txt`

4. **État du système** :
```bash
dpkg -l | grep -E "^..r|^..c" > ~/paquets-problematiques.txt
```

5. **Sources** :
```bash
cat /etc/apt/sources.list  
ls /etc/apt/sources.list.d/  
```

### Où demander de l'aide

- Forums Linux Mint français
- Forums Ubuntu-fr
- Reddit : r/linuxmint, r/linux4noobs
- Ask Ubuntu (en anglais)

## Script de réparation automatique

Voici un script qui tente de réparer automatiquement les problèmes courants.

### Créer le script

```bash
nano ~/reparer-dependances.sh
```

### Contenu du script

```bash
#!/bin/bash

echo "=== Script de réparation des dépendances ==="  
echo "Ce script va tenter de réparer les dépendances cassées"  
echo ""  
read -p "Continuer? (o/n) " -n 1 -r  
echo  
if [[ ! $REPLY =~ ^[Oo]$ ]]  
then  
    exit 1
fi

echo "Étape 1: Configuration des paquets en attente..."  
sudo dpkg --configure -a  

echo "Étape 2: Nettoyage du cache..."  
sudo apt clean  

echo "Étape 3: Mise à jour de la liste des paquets..."  
sudo apt update  

echo "Étape 4: Réparation des dépendances..."  
sudo apt install -f  

echo "Étape 5: Mise à jour du système..."  
sudo apt upgrade  

echo "Étape 6: Suppression des paquets inutiles..."  
sudo apt autoremove  

echo "Étape 7: Nettoyage final..."  
sudo apt autoclean  

echo ""  
echo "=== Terminé ==="  
echo "Vérifiez s'il reste des erreurs avec: sudo apt check"  
```

### Rendre exécutable et utiliser

```bash
chmod +x ~/reparer-dependances.sh
~/reparer-dependances.sh
```

## Restauration depuis une sauvegarde

Si vraiment rien ne fonctionne, restaurez depuis Timeshift.

### Démarrer en mode recovery

1. Redémarrez l'ordinateur
2. Appuyez sur **Shift** ou **Esc** pendant le démarrage
3. Sélectionnez **Options avancées**
4. Choisissez un **noyau en mode recovery**

### Restaurer avec Timeshift

```bash
sudo timeshift --restore
```

Choisissez un snapshot d'avant le problème.

## Réinstallation propre (solution ultime)

Si tout est vraiment cassé au-delà de toute réparation :

### Sauvegarder vos données

```bash
cp -r ~/Documents ~/Bureau ~/Images /media/backup/
```

### Réinstaller Linux Mint

1. Téléchargez la dernière ISO
2. Créez une clé USB bootable
3. Réinstallez (vous pouvez garder /home si vous voulez)

**Note** : C'est rare d'en arriver là. Les dépendances cassées sont presque toujours réparables.

## Conclusion

Les dépendances cassées sont frustrantes mais rarement fatales. Dans la grande majorité des cas, `sudo apt install -f` suffit à résoudre le problème. Pour les cas plus complexes, les solutions existent et sont documentées.

### Points clés à retenir

- ⭐ **La commande magique** : `sudo apt install -f` résout 80% des problèmes
- ⭐ **Ne paniquez pas** : C'est réparable
- ⭐ **Procédez par étapes** : Commencez par les solutions simples
- ⭐ **Prévenez** : Timeshift et bonnes pratiques évitent la plupart des problèmes
- ⭐ **Documentez** : Notez vos erreurs pour apprendre
- ⭐ **Demandez de l'aide** : La communauté est là pour ça

### Commandes essentielles à retenir

```bash
# La base (essayez toujours en premier)
sudo apt install -f

# Si ça ne suffit pas
sudo dpkg --configure -a  
sudo apt install -f  

# Nettoyage complet
sudo apt clean  
sudo apt update  
sudo apt install -f  
sudo apt autoremove  
```

### Message final

Les dépendances cassées font partie de l'apprentissage de Linux. Chaque problème résolu vous rend plus compétent. N'ayez pas peur d'expérimenter (avec des sauvegardes !), car c'est en résolvant ces problèmes que vous comprendrez vraiment comment fonctionne votre système.

Et rappelez-vous : avec Timeshift, vous avez toujours un filet de sécurité. Vous pouvez expérimenter en toute confiance !

---


⏭️ [Le terminal et commandes de base](/07-le-terminal-et-commandes-de-base/README.md)
