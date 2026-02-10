🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 17.1 Timeshift pour sauvegardes système (snapshots)

## Introduction

Timeshift est un outil essentiel pour protéger votre système Linux Mint. Il fonctionne comme une "machine à remonter le temps" pour votre système d'exploitation, vous permettant de revenir à un état antérieur en cas de problème.

### Qu'est-ce qu'un snapshot ?

Un snapshot (instantané en français) est une "photographie" de votre système à un moment précis. Il capture l'état de vos fichiers système, vos applications installées et vos configurations. C'est comme un point de sauvegarde dans un jeu vidéo : si quelque chose tourne mal, vous pouvez revenir à ce point.

### Pourquoi utiliser Timeshift ?

Timeshift vous protège contre :
- Les mises à jour qui causent des problèmes
- Les erreurs de manipulation système
- L'installation de logiciels incompatibles
- Les modifications de configuration qui cassent le système
- Les bugs ou corruptions inattendues

**Important** : Timeshift sauvegarde uniquement les fichiers système, pas vos documents personnels (photos, vidéos, documents). Pour vos données personnelles, vous devrez utiliser d'autres solutions de sauvegarde.

## Installation de Timeshift

Bonne nouvelle ! Timeshift est préinstallé sur Linux Mint. Si pour une raison quelconque il n'est pas présent sur votre système, vous pouvez l'installer facilement :

**Via le gestionnaire de logiciels :**
1. Ouvrez le Gestionnaire de logiciels
2. Recherchez "Timeshift"
3. Cliquez sur "Installer"

**Via le terminal :**
```bash
sudo apt update  
sudo apt install timeshift  
```

## Premier lancement et configuration

### Démarrer Timeshift

1. Ouvrez le Menu principal
2. Tapez "Timeshift" dans la recherche
3. Cliquez sur l'application Timeshift (vous devrez entrer votre mot de passe administrateur)

### Assistant de configuration initial

Au premier lancement, Timeshift vous guide à travers un assistant de configuration :

#### 1. Choix du type de snapshot

Vous aurez deux options :

**RSYNC (Recommandé pour les débutants)**
- Plus simple et plus compatible
- Fonctionne sur tous les types de partitions
- Utilise des copies incrémentales (seuls les changements sont sauvegardés)
- Plus facile à comprendre et à gérer

**BTRFS**
- Nécessite un système de fichiers Btrfs
- Plus rapide pour créer des snapshots
- Plus économe en espace disque
- Nécessite une configuration spécifique lors de l'installation de Linux Mint

**Pour la plupart des utilisateurs, choisissez RSYNC.**

#### 2. Sélection de l'emplacement de sauvegarde

Timeshift vous demande où stocker les snapshots :

- **Sur la même partition** : Moins sûr, mais pratique si vous n'avez qu'un seul disque
- **Sur un disque externe** : Recommandé pour une meilleure sécurité
- **Sur une partition séparée** : Idéal si vous avez plusieurs partitions

**Conseil** : Si possible, utilisez une partition ou un disque différent de votre système. Cela protège vos sauvegardes même si votre disque système a un problème.

#### 3. Configuration des niveaux de snapshots

Timeshift propose plusieurs niveaux de sauvegarde automatique :

- **Mensuel** : Garde X snapshots mensuels
- **Hebdomadaire** : Garde X snapshots hebdomadaires
- **Quotidien** : Garde X snapshots quotidiens
- **Horaire** : Garde X snapshots horaires
- **Au démarrage** : Crée un snapshot à chaque démarrage

**Configuration recommandée pour débutants :**
- Mensuel : 2 snapshots
- Hebdomadaire : 3 snapshots
- Quotidien : 5 snapshots
- Horaire : 0 (désactivé)
- Au démarrage : Activé

Cette configuration vous donne un bon équilibre entre protection et espace disque utilisé.

#### 4. Inclusion/Exclusion de dossiers

Par défaut, Timeshift exclut automatiquement :
- `/home` (vos documents personnels)
- `/root` (dossier racine de l'administrateur)
- Les fichiers temporaires

**Vous n'avez généralement rien à modifier ici.** Ces exclusions par défaut sont appropriées pour la plupart des utilisateurs.

## Créer un snapshot manuel

Il est recommandé de créer un snapshot manuel avant toute opération importante (mise à jour majeure, installation de nouveaux pilotes, modifications système, etc.).

### Étapes pour créer un snapshot :

1. Ouvrez Timeshift
2. Cliquez sur le bouton **"Créer"** dans la barre d'outils
3. Ajoutez éventuellement un commentaire pour vous souvenir du contexte (par exemple : "Avant mise à jour vers Mint 22")
4. Cliquez sur **"Créer"**
5. Attendez que le processus se termine (cela peut prendre quelques minutes)

Le premier snapshot peut prendre plus de temps car il copie tout le système. Les snapshots suivants seront beaucoup plus rapides car seuls les changements sont sauvegardés.

## Gérer vos snapshots

### Visualiser vos snapshots

Dans la fenêtre principale de Timeshift, vous voyez la liste de tous vos snapshots avec :
- La date et l'heure de création
- Le commentaire associé (si vous en avez ajouté un)
- La taille du snapshot
- Le type (manuel ou automatique)

### Supprimer un snapshot

Si vous manquez d'espace disque ou si un snapshot n'est plus nécessaire :

1. Sélectionnez le snapshot dans la liste
2. Cliquez sur le bouton **"Supprimer"**
3. Confirmez la suppression

**Attention** : Ne supprimez pas tous vos snapshots ! Gardez toujours au moins un ou deux snapshots récents.

### Parcourir un snapshot

Vous pouvez explorer le contenu d'un snapshot sans le restaurer :

1. Sélectionnez un snapshot
2. Cliquez sur **"Parcourir"**
3. Naviguez dans les fichiers comme dans un explorateur normal

Cela peut être utile pour récupérer un fichier de configuration spécifique sans restaurer tout le système.

## Restaurer un snapshot

Si votre système rencontre un problème, vous pouvez le restaurer à un état antérieur.

### Restauration depuis un système fonctionnel

Si votre système démarre encore normalement :

1. Ouvrez Timeshift
2. Sélectionnez le snapshot vers lequel vous voulez revenir
3. Cliquez sur **"Restaurer"**
4. Vérifiez les options de restauration
5. Cliquez sur **"Suivant"** puis **"Restaurer"**
6. Entrez votre mot de passe
7. Laissez le processus se terminer
8. Redémarrez votre ordinateur

**Important** : La restauration remplacera tous les fichiers système actuels par ceux du snapshot. Les modifications faites après la création du snapshot seront perdues.

### Restauration depuis un système qui ne démarre pas

Si Linux Mint ne démarre plus :

1. Démarrez avec une clé USB Live de Linux Mint
2. Une fois sur le bureau Live, ouvrez Timeshift
3. Timeshift détectera automatiquement vos snapshots existants
4. Sélectionnez le snapshot à restaurer
5. Cliquez sur **"Restaurer"**
6. Timeshift restaurera le système sur votre disque dur
7. Retirez la clé USB et redémarrez

## Bonnes pratiques

### Quand créer un snapshot manuel

Créez toujours un snapshot manuel avant :
- Une mise à jour majeure du système
- L'installation de pilotes (particulièrement NVIDIA)
- Des modifications importantes de configuration
- L'installation de logiciels provenant de sources non officielles
- Des manipulations dans le terminal qui modifient le système

### Gestion de l'espace disque

Les snapshots peuvent occuper beaucoup d'espace. Voici quelques conseils :

- Surveillez régulièrement l'espace disponible sur votre partition de sauvegarde
- Supprimez les anciens snapshots dont vous n'avez plus besoin
- Si vous manquez d'espace, réduisez le nombre de snapshots automatiques conservés
- Considérez l'utilisation d'un disque externe dédié pour les sauvegardes

### Compléter avec d'autres sauvegardes

Timeshift ne sauvegarde que le système, pas vos données personnelles. Utilisez-le en complément avec :
- Une sauvegarde régulière de `/home` (vos documents)
- Un stockage cloud pour les fichiers importants
- Des sauvegardes sur disque externe pour les gros fichiers

### Vérification régulière

De temps en temps :
- Vérifiez que les snapshots automatiques se créent bien
- Assurez-vous que vous avez assez d'espace disque
- Testez occasionnellement le processus de restauration (dans une machine virtuelle si possible)

## Timeshift et les mises à jour

Linux Mint crée automatiquement un snapshot Timeshift avant chaque mise à jour importante du système via le Gestionnaire de mises à jour. C'est une sécurité supplémentaire qui vous permet de revenir en arrière si une mise à jour pose problème.

Vous verrez une notification indiquant "Création d'un snapshot système..." avant que les mises à jour importantes ne s'installent.

## Résolution de problèmes courants

### "Pas assez d'espace disque"

- Supprimez des snapshots anciens
- Nettoyez votre système avec BleachBit
- Utilisez une partition ou un disque avec plus d'espace
- Réduisez le nombre de snapshots automatiques à conserver

### "Impossible de créer un snapshot"

- Vérifiez que vous avez les droits administrateur
- Assurez-vous que le disque de destination est bien monté
- Vérifiez que le système de fichiers n'est pas corrompu
- Redémarrez et réessayez

### Les snapshots automatiques ne se créent pas

- Vérifiez la configuration dans Timeshift
- Assurez-vous que le service est activé : `sudo systemctl status crond`
- Vérifiez les journaux système pour des messages d'erreur

## En résumé

Timeshift est votre filet de sécurité pour Linux Mint :
- Configurez-le dès l'installation de votre système
- Laissez les snapshots automatiques activés
- Créez des snapshots manuels avant les opérations importantes
- Ne négligez pas la sauvegarde de vos données personnelles (que Timeshift ne couvre pas)
- Vérifiez régulièrement que tout fonctionne correctement

Avec Timeshift correctement configuré, vous pouvez explorer et expérimenter avec Linux Mint en toute confiance, sachant que vous pouvez toujours revenir à un état stable de votre système.

⏭️ [Sauvegarde de données (Déjà Dup, Backintime, rsync)](/17-sauvegarde-et-restauration/02-sauvegarde-de-donnees.md)
