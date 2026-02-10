🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 17.4 Stratégies de sauvegarde (règle 3-2-1)

## Introduction

Avoir des outils de sauvegarde, c'est bien. Avoir une stratégie de sauvegarde efficace, c'est encore mieux ! Sans stratégie claire, vous risquez de vous retrouver avec des sauvegardes incomplètes, obsolètes ou inutilisables le jour où vous en aurez vraiment besoin.

### Pourquoi une stratégie de sauvegarde ?

Une bonne stratégie de sauvegarde répond à ces questions :
- **Quoi** sauvegarder ? (système, données, configuration)
- **Où** sauvegarder ? (disque externe, cloud, serveur)
- **Quand** sauvegarder ? (quotidien, hebdomadaire, manuel)
- **Comment** sauvegarder ? (Timeshift, rsync, Clonezilla)
- **Combien de temps** conserver ? (versions multiples, rotation)

Sans réponses à ces questions, vos sauvegardes seront aléatoires et potentiellement inefficaces.

### Le coût de ne pas sauvegarder

Perdre ses données peut avoir des conséquences dramatiques :
- **Perte de souvenirs** : Photos de famille, vidéos de vacances
- **Perte de travail** : Documents professionnels, projets en cours
- **Perte de temps** : Réinstaller, reconfigurer tout le système
- **Perte financière** : Données client, comptabilité, factures
- **Stress et frustration** : L'angoisse de tout avoir perdu

**Pensez-y** : Combien de temps faudrait-il pour recréer tout ce qui est sur votre ordinateur ? Quelques heures ? Des jours ? Des mois ? Certaines choses sont simplement irremplaçables.

## La règle 3-2-1 : Le standard de référence

La règle 3-2-1 est la stratégie de sauvegarde la plus reconnue et recommandée par les professionnels. Elle est simple à comprendre et efficace.

### Les trois principes

**3** = Trois copies de vos données
- 1 copie originale (vos données actuelles)
- 2 sauvegardes supplémentaires

**2** = Deux supports différents
- Par exemple : disque interne + disque externe
- Ou : disque interne + cloud
- Ou : disque externe + NAS

**1** = Une copie hors site
- Stockée physiquement ailleurs (cloud, chez un ami, au bureau)
- Protection contre incendie, vol, inondation, etc.

### Pourquoi cette règle fonctionne

**Scénario 1 : Panne de disque dur**
- Votre disque principal tombe en panne
- ✅ Vous avez une copie sur disque externe
- ✅ Vous avez une copie dans le cloud
- Résultat : Aucune perte de données !

**Scénario 2 : Vol ou incendie**
- Votre ordinateur et disque externe sont volés/détruits
- ✅ Vous avez une copie dans le cloud
- Résultat : Vos données sont sauvées !

**Scénario 3 : Suppression accidentelle**
- Vous supprimez accidentellement un dossier important
- ✅ Vous pouvez le récupérer depuis une sauvegarde
- Résultat : Données récupérées rapidement !

**Scénario 4 : Ransomware (virus qui chiffre vos fichiers)**
- Un virus chiffre toutes vos données
- ✅ Le disque externe était déconnecté
- ✅ Le cloud a des versions antérieures
- Résultat : Vous restaurez et ne payez pas la rançon !

### Exemples d'application de la règle 3-2-1

#### Exemple 1 : Configuration minimale

**Vos 3 copies :**
1. Données sur votre ordinateur (original)
2. Sauvegarde sur disque externe USB (Backintime quotidien)
3. Sauvegarde cloud (Déjà Dup vers Google Drive hebdomadaire)

**Vos 2 supports :**
- Support 1 : Disques internes (ordinateur + disque externe)
- Support 2 : Cloud (Google Drive)

**Votre copie hors site :**
- Le cloud (physiquement dans un datacenter ailleurs)

**Coût** : ~50€ (disque externe) + gratuit (cloud 15 Go)

#### Exemple 2 : Configuration intermédiaire

**Vos 3 copies :**
1. Données sur votre ordinateur
2. Sauvegarde sur disque externe A (quotidien automatique)
3. Sauvegarde sur disque externe B (hebdomadaire, rangé ailleurs)

**Vos 2 supports :**
- Support 1 : Disques internes (ordinateur + externe A)
- Support 2 : Disque externe B (différent modèle/marque)

**Votre copie hors site :**
- Disque externe B rangé au bureau ou chez un proche
- Rotation hebdomadaire (vous échangez A et B)

**Coût** : ~100€ (2 disques externes)

#### Exemple 3 : Configuration avancée

**Vos 3+ copies :**
1. Données sur votre ordinateur (SSD)
2. Sauvegarde locale (NAS domestique, quotidien)
3. Sauvegarde cloud (Nextcloud auto-hébergé ou service commercial)
4. Bonus : Disque externe mensuel archivé

**Vos 2+ supports :**
- Support 1 : SSD + NAS
- Support 2 : Cloud
- Support 3 : Disque externe d'archive

**Votre copie hors site :**
- Cloud + disque externe archivé chez un proche

**Coût** : Variable selon le NAS et services cloud

## Types de sauvegardes

Comprendre les différents types de sauvegardes vous aide à optimiser votre stratégie.

### 1. Sauvegarde complète (Full Backup)

**Définition :** Copie intégrale de toutes les données sélectionnées.

**Avantages :**
- Simple à comprendre
- Restauration rapide (tout est au même endroit)
- Indépendante (ne dépend d'aucune autre sauvegarde)

**Inconvénients :**
- Prend beaucoup de temps
- Utilise beaucoup d'espace
- Gourmande en ressources

**Quand l'utiliser :**
- Première sauvegarde
- Sauvegarde mensuelle ou trimestrielle
- Avant une modification majeure du système

**Exemple :**
```bash
# Sauvegarde complète avec rsync
rsync -av ~/Documents /media/backup/complete-2024-11-29/
```

### 2. Sauvegarde incrémentale (Incremental Backup)

**Définition :** Sauvegarde uniquement les fichiers modifiés depuis la dernière sauvegarde (complète ou incrémentale).

**Avantages :**
- Très rapide
- Économise beaucoup d'espace
- Peut être faite fréquemment

**Inconvénients :**
- Restauration plus complexe (nécessite toutes les sauvegardes intermédiaires)
- Chaîne de dépendances (si une sauvegarde est corrompue, les suivantes sont inutilisables)

**Quand l'utiliser :**
- Sauvegardes quotidiennes ou horaires
- Pour des données qui changent peu
- En complément de sauvegardes complètes hebdomadaires

**Schéma de fonctionnement :**
```
Dimanche : Sauvegarde COMPLÈTE (100 Go)  
Lundi : Incrémentale (seuls 2 Go modifiés)  
Mardi : Incrémentale (seuls 1 Go modifié)  
Mercredi : Incrémentale (seuls 3 Go modifiés)  
...
Dimanche suivant : Nouvelle sauvegarde COMPLÈTE
```

**Exemple avec Backintime :**
Backintime fait automatiquement des sauvegardes incrémentales basées sur des liens durs.

### 3. Sauvegarde différentielle (Differential Backup)

**Définition :** Sauvegarde tous les fichiers modifiés depuis la dernière sauvegarde complète.

**Avantages :**
- Restauration plus simple que l'incrémentale (besoin de la complète + la dernière différentielle)
- Compromis entre complète et incrémentale

**Inconvénients :**
- Grossit au fil du temps
- Plus lente que l'incrémentale
- Utilise plus d'espace que l'incrémentale

**Quand l'utiliser :**
- Entre deux sauvegardes complètes
- Pour équilibrer vitesse et simplicité de restauration

**Schéma de fonctionnement :**
```
Dimanche : Sauvegarde COMPLÈTE (100 Go)  
Lundi : Différentielle (2 Go modifiés depuis dimanche)  
Mardi : Différentielle (3 Go modifiés depuis dimanche)  
Mercredi : Différentielle (5 Go modifiés depuis dimanche)  
...
Dimanche suivant : Nouvelle sauvegarde COMPLÈTE
```

### 4. Sauvegarde miroir (Mirror/Sync)

**Définition :** Copie exacte et synchronisée des données (comme un miroir).

**Avantages :**
- Simple : ce qui est sur la source est sur la destination
- Accès direct aux fichiers (pas besoin de restauration)
- Rapide pour vérifier les données

**Inconvénients :**
- Aucun historique (pas de versions précédentes)
- Si vous supprimez sur la source, c'est supprimé sur la sauvegarde
- Vulnérable aux ransomwares

**Quand l'utiliser :**
- Synchronisation entre ordinateurs
- Sauvegarde de travail en cours
- EN COMPLÉMENT d'autres sauvegardes (jamais seule !)

**Exemple :**
```bash
# Synchronisation miroir avec rsync
rsync -av --delete ~/Documents /media/backup/mirror/
```

**⚠️ Attention :** Le `--delete` supprime dans la destination ce qui n'est plus dans la source !

### 5. Snapshot (Instantané)

**Définition :** Capture l'état du système à un moment précis, utilisée surtout pour les systèmes.

**Avantages :**
- Très rapide à créer
- Versions multiples sans dupliquer tout
- Parfait pour le système d'exploitation

**Inconvénients :**
- Nécessite un système de fichiers compatible (Btrfs, ZFS) ou un outil spécifique
- Pas adapté aux données personnelles seules

**Quand l'utiliser :**
- Protection du système (Timeshift)
- Avant mises à jour
- Environnements virtuels

**Exemple :**
Timeshift utilise des snapshots pour sauvegarder Linux Mint.

## Stratégies selon le profil utilisateur

### Profil 1 : Utilisateur débutant occasionnel

**Caractéristiques :**
- Utilise l'ordinateur pour navigation web, emails, quelques documents
- Peu de photos/vidéos
- Budget limité

**Stratégie recommandée :**

**Sauvegarde système :**
- Timeshift : snapshots hebdomadaires automatiques

**Sauvegarde données :**
- Déjà Dup vers disque externe USB : hebdomadaire automatique
- Google Drive / OneDrive : documents importants uniquement

**Planning :**
```
Quotidien : Rien (automatique via cloud sync)  
Hebdomadaire : Timeshift (automatique) + Déjà Dup (automatique)  
Mensuel : Vérification manuelle que tout fonctionne  
Avant changement : Timeshift manuel + copie manuelle documents importants  
```

**Matériel nécessaire :**
- 1 disque externe USB de 500 Go (~40€)
- Compte cloud gratuit (15 Go Google Drive)

**Temps requis :** ~5 minutes par mois

### Profil 2 : Utilisateur régulier (famille, télétravail)

**Caractéristiques :**
- Usage quotidien (travail, études)
- Photos et vidéos de famille importantes
- Documents professionnels
- Budget moyen

**Stratégie recommandée :**

**Sauvegarde système :**
- Timeshift : snapshots quotidiens automatiques
- Clonezilla : image complète mensuelle sur disque externe

**Sauvegarde données :**
- Backintime : quotidien automatique vers disque externe
- Cloud (Nextcloud ou commercial) : documents de travail en continu
- Disque externe secondaire : hebdomadaire, stocké ailleurs

**Planning :**
```
Quotidien : Timeshift + Backintime (automatiques)  
Hebdomadaire : Synchronisation disque externe secondaire  
Mensuel : Image Clonezilla complète + vérification des sauvegardes  
Annuel : Archivage photos/vidéos sur disque offline  
```

**Matériel nécessaire :**
- 2 disques externes USB de 1-2 To (~80€ × 2)
- Abonnement cloud 100-200 Go (~2-3€/mois) ou Nextcloud gratuit

**Temps requis :** ~30 minutes par mois

### Profil 3 : Créateur de contenu (photo, vidéo, design)

**Caractéristiques :**
- Fichiers volumineux (projets photo/vidéo)
- Données critiques professionnelles
- Besoin de versions multiples
- Budget conséquent

**Stratégie recommandée :**

**Sauvegarde système :**
- Timeshift : snapshots quotidiens
- Image Clonezilla : mensuelle

**Sauvegarde données :**
- NAS domestique : sauvegarde continue (rsync ou Syncthing)
- Disques externes multiples : rotation hebdomadaire
- Cloud illimité ou haute capacité : projets terminés
- Disque archive : projets terminés, stocké hors site

**Planning :**
```
Continu : Sync vers NAS  
Quotidien : Timeshift  
Hebdomadaire : Rotation disques externes (1 reste hors site)  
Mensuel : Image système + archivage projets terminés  
Trimestriel : Audit complet des sauvegardes  
```

**Matériel nécessaire :**
- NAS 4 baies avec disques redondants (RAID) (~500-1000€)
- 3 disques externes 4-8 To pour rotation (~120€ × 3)
- Abonnement cloud haute capacité (~10-20€/mois)

**Temps requis :** ~2 heures par mois (après automatisation)

### Profil 4 : Développeur / Utilisateur avancé

**Caractéristiques :**
- Code source, bases de données
- Environnements de développement multiples
- Fichiers de configuration personnalisés
- Besoin de versioning

**Stratégie recommandée :**

**Sauvegarde système :**
- Timeshift : snapshots quotidiens
- Scripts rsync personnalisés

**Sauvegarde données :**
- Git pour le code (GitHub, GitLab, serveur personnel)
- Rsync quotidien vers serveur distant (VPS, NAS)
- Borg Backup pour sauvegardes chiffrées déduplicées
- Configuration : dotfiles dans Git

**Planning :**
```
Continu : Git push (code)  
Quotidien : Timeshift + rsync automatique vers serveur  
Hebdomadaire : Borg backup complet  
Mensuel : Image système + test restauration  
```

**Matériel/Services nécessaires :**
- VPS ou serveur dédié (~5-20€/mois)
- Disque externe pour backup local (~60€)
- Repositories Git (gratuit sur GitHub/GitLab)

**Temps requis :** ~1 heure par mois (très automatisé)

### Profil 5 : Utilisateur minimaliste

**Caractéristiques :**
- Peu de données locales
- Utilise principalement le cloud
- Budget minimal

**Stratégie recommandée :**

**Sauvegarde système :**
- Timeshift : snapshots hebdomadaires

**Sauvegarde données :**
- Services cloud natifs (Google Drive, Nextcloud)
- Export occasionnel sur clé USB

**Planning :**
```
Continu : Données dans le cloud  
Hebdomadaire : Timeshift automatique  
Mensuel : Export manuel fichiers critiques sur USB  
```

**Matériel nécessaire :**
- 1 clé USB de 64 Go (~15€)
- Services cloud gratuits

**Temps requis :** ~10 minutes par mois

## Planning et fréquence de sauvegarde

### Déterminer la fréquence appropriée

La fréquence dépend de vos réponses à ces questions :

**Question 1 : Combien de données pouvez-vous accepter de perdre ?**
- 1 heure de travail → Sauvegarde horaire
- 1 journée → Sauvegarde quotidienne
- 1 semaine → Sauvegarde hebdomadaire

**Question 2 : À quelle vitesse vos données changent-elles ?**
- Création quotidienne (travail actif) → Sauvegarde quotidienne ou continue
- Peu de modifications → Sauvegarde hebdomadaire
- Quasiment statique → Sauvegarde mensuelle

**Question 3 : Quelle est la criticité de vos données ?**
- Critique (professionnelles, irremplaçables) → Sauvegardes fréquentes + multiples
- Importante (photos famille) → Sauvegarde hebdomadaire
- Remplaçable (téléchargements) → Pas de sauvegarde nécessaire

### Calendrier type recommandé

#### Pour la plupart des utilisateurs :

**Quotidien (automatique) :**
- Timeshift (système)
- Backintime ou Déjà Dup (données)
- Synchronisation cloud continue

**Hebdomadaire :**
- Vérification que les sauvegardes automatiques fonctionnent
- Connexion du disque externe secondaire si applicable

**Mensuel :**
- Test de restauration d'un fichier
- Nettoyage des anciennes sauvegardes
- Vérification de l'espace disponible
- Image Clonezilla complète (optionnel)

**Trimestriel :**
- Archivage des projets terminés
- Rotation des disques de sauvegarde
- Audit complet de la stratégie

**Annuel :**
- Gravure des souvenirs importants sur DVD/Blu-ray (archivage permanent)
- Réévaluation de la stratégie de sauvegarde
- Remplacement des disques anciens (>5 ans)

**Ponctuel (avant événement) :**
- Avant mise à jour majeure du système
- Avant modification matérielle
- Avant voyage avec ordinateur portable
- Avant expérimentation système

### Automatisation : La clé du succès

**Principe fondamental :** Les sauvegardes manuelles finissent toujours par être oubliées !

**Ce qui doit être automatisé :**
- ✅ Sauvegardes système quotidiennes (Timeshift)
- ✅ Sauvegardes données quotidiennes (Backintime, Déjà Dup)
- ✅ Synchronisation cloud (continue)
- ✅ Nettoyage des anciennes sauvegardes

**Ce qui peut rester manuel :**
- Images système complètes (mensuel)
- Rotation des disques externes
- Vérification et tests
- Archivages spéciaux

**Comment automatiser :**

1. **Utilisez les planificateurs intégrés**
   - Timeshift a sa propre planification
   - Backintime et Déjà Dup aussi

2. **Utilisez cron pour les scripts personnalisés**
   ```bash
   # Éditer crontab
   crontab -e

   # Sauvegarde quotidienne à 2h du matin
   0 2 * * * /home/user/scripts/backup.sh
   ```

3. **Utilisez systemd timers pour plus de flexibilité**
   ```bash
   # Alternative moderne à cron
   systemctl --user enable backup.timer
   ```

4. **Notifications**
   - Configurez des notifications en cas d'échec
   - Vérifiez régulièrement les logs

## Rotation et rétention des sauvegardes

### Principe de rotation

Ne gardez pas toutes les sauvegardes indéfiniment : vous manquerez d'espace !

**Stratégie GFS (Grandfather-Father-Son) :**

- **Quotidiennes (Son)** : Garder 7 jours
- **Hebdomadaires (Father)** : Garder 4 semaines
- **Mensuelles (Grandfather)** : Garder 12 mois
- **Annuelles** : Garder indéfiniment (archives)

**Exemple concret :**
```
1er décembre : Sauvegarde quotidienne (gardée 7 jours)
8 décembre : Sauvegarde hebdomadaire (gardée 4 semaines)
1er janvier : Sauvegarde mensuelle (gardée 12 mois)
1er janvier 2025 : Sauvegarde annuelle (archivée définitivement)
```

**Avantages :**
- Économise l'espace disque
- Garde un historique long terme
- Balance entre fréquence et conservation

### Configuration de la rétention

**Dans Timeshift :**
- Quotidien : 5 snapshots
- Hebdomadaire : 3 snapshots
- Mensuel : 2 snapshots

**Dans Backintime :**
```
Règles intelligentes :
- Garder toutes les sauvegardes du dernier mois
- Garder une sauvegarde par semaine pour les 3 mois précédents
- Garder une sauvegarde par mois pour les 12 derniers mois
```

**Avec des scripts rsync :**
```bash
# Garder les 30 derniers jours
find /backup/daily -mtime +30 -delete

# Garder 12 sauvegardes mensuelles
ls -t /backup/monthly | tail -n +13 | xargs rm -rf
```

### Espace disque requis

**Calcul approximatif :**

Pour un système de 100 Go de données :

**Avec sauvegardes incrémentales (Backintime) :**
- Première sauvegarde complète : 100 Go
- 30 sauvegardes quotidiennes : +10-20 Go (seulement les changements)
- Total : ~120-150 Go

**Avec sauvegardes complètes multiples :**
- 7 sauvegardes quotidiennes : 700 Go
- 4 sauvegardes hebdomadaires : 400 Go
- Total : 1.1 To (non recommandé !)

**Recommandation :** Prévoyez un disque de sauvegarde 2-3× la taille de vos données.

## Tests et vérification

### Pourquoi tester vos sauvegardes ?

**Citation célèbre :** "Vous n'avez pas de sauvegarde tant que vous n'avez pas testé la restauration."

Une sauvegarde non testée peut être :
- Corrompue (fichiers illisibles)
- Incomplète (fichiers manquants)
- Incompatible (format changé)
- Inaccessible (mot de passe oublié, support défaillant)

**Le jour où vous en aurez besoin, il sera trop tard pour découvrir qu'elle ne fonctionne pas !**

### Que tester ?

**Tests réguliers (mensuel) :**

1. **Restauration de fichiers individuels**
   - Choisissez 2-3 fichiers au hasard
   - Restaurez-les dans un dossier temporaire
   - Vérifiez qu'ils s'ouvrent correctement
   - Comparez avec les originaux

2. **Vérification de l'intégrité**
   - Vérifiez les checksums (md5, sha256)
   - Utilisez les outils de vérification intégrés
   - Vérifiez les logs pour des erreurs

3. **Test d'accès**
   - Pouvez-vous accéder aux sauvegardes ?
   - Les mots de passe fonctionnent-ils ?
   - Les disques sont-ils détectés ?

**Tests approfondis (trimestriel) :**

1. **Restauration de dossier complet**
   - Restaurez un dossier entier (ex: Documents)
   - Vérifiez la structure et les permissions
   - Testez quelques fichiers

2. **Test de snapshot système (Timeshift)**
   - Dans une machine virtuelle si possible
   - Ou créez un snapshot, modifiez le système, restaurez

3. **Simulation de catastrophe**
   - Débranchez le disque de sauvegarde
   - Pouvez-vous accéder au cloud ?
   - Votre plan de reprise fonctionne-t-il ?

**Test annuel (restauration complète) :**

1. **Dans une machine virtuelle**
   - Créez une VM vierge
   - Restaurez votre image système complète
   - Testez que tout fonctionne

2. **Ou sur disque secondaire**
   - Restaurez sur un ancien ordinateur
   - Vérifiez le boot et les données

### Checklist de vérification mensuelle

```
□ Les sauvegardes automatiques se sont bien exécutées
□ Aucun message d'erreur dans les logs
□ Espace disque suffisant (>20% libre)
□ Test de restauration d'un fichier réussi
□ Disques de sauvegarde en bon état (SMART)
□ Copie cloud synchronisée
□ Rotation des anciennes sauvegardes effectuée
□ Documentation à jour
```

### Outils de vérification

**Vérifier l'état des disques :**
```bash
# Installer GSmartControl
sudo apt install gsmartcontrol

# Vérifier la santé du disque
sudo smartctl -a /dev/sda
```

**Vérifier l'intégrité des fichiers :**
```bash
# Créer des checksums
find ~/Documents -type f -exec md5sum {} \; > checksums.txt

# Vérifier plus tard
md5sum -c checksums.txt
```

**Vérifier les sauvegardes Timeshift :**
```bash
# Lister les snapshots
sudo timeshift --list

# Vérifier un snapshot spécifique
sudo timeshift --check --snapshot '2024-11-29_12-00-00'
```

## Erreurs courantes à éviter

### Erreur #1 : "Je sauvegarderai plus tard"

**Problème :** Reporter constamment les sauvegardes.

**Solution :**
- Automatisez TOUT ce qui peut l'être
- Définissez une alarme mensuelle pour les vérifications
- Considérez que la sauvegarde fait partie de l'entretien normal de l'ordinateur

### Erreur #2 : Sauvegarde unique

**Problème :** Une seule sauvegarde (pas de règle 3-2-1).

**Risques :**
- Panne du support de sauvegarde
- Vol ou destruction simultanée
- Corruption des données répliquée

**Solution :**
- Minimum 2 sauvegardes (locale + cloud ou 2 disques)
- Idéalement 3 copies sur 2 supports avec 1 hors site

### Erreur #3 : Sauvegarde non testée

**Problème :** Découvrir que les sauvegardes ne fonctionnent pas quand c'est trop tard.

**Solution :**
- Testez mensuellement
- Documentez les procédures de restauration
- Simulez une perte de données

### Erreur #4 : Tous les œufs dans le même panier

**Problème :** Sauvegardes sur le même disque physique ou toujours connectées.

**Risques :**
- Panne matérielle détruit tout
- Ransomware chiffre toutes les copies
- Surtension détruit tout

**Solution :**
- Supports physiquement séparés
- Au moins un support déconnecté/hors ligne
- Cloud comme copie off-site

### Erreur #5 : Oublier le système

**Problème :** Sauvegarder uniquement les données, pas le système.

**Conséquences :**
- Réinstallation complète nécessaire
- Reconfiguration de tout
- Perte de temps considérable

**Solution :**
- Timeshift pour le système
- Image Clonezilla occasionnelle
- Documentation de votre configuration

### Erreur #6 : Manque de rotation

**Problème :** Garder toutes les sauvegardes ou seulement la dernière.

**Conséquences :**
- Saturation de l'espace disque
- Ou impossibilité de revenir à une version antérieure

**Solution :**
- Stratégie GFS (voir plus haut)
- Rotation automatique configurée

### Erreur #7 : Pas de chiffrement des données sensibles

**Problème :** Sauvegardes non chiffrées de données sensibles.

**Risques :**
- Vol de disque externe = vol de données
- Fuite de données personnelles/professionnelles

**Solution :**
- Chiffrez les sauvegardes (Déjà Dup, VeraCrypt, LUKS)
- Mots de passe forts et conservés en sécurité
- Chiffrement au moins pour le cloud et disques transportables

### Erreur #8 : Dépendre d'un seul service/outil

**Problème :** Tout miser sur un seul fournisseur cloud ou outil.

**Risques :**
- Fermeture du service
- Compte suspendu/piraté
- Incompatibilité après mise à jour

**Solution :**
- Diversifiez (local + cloud)
- Standards ouverts quand possible
- Plan B documenté

### Erreur #9 : Négliger les métadonnées

**Problème :** Sauvegarder les fichiers mais perdre les permissions, dates, structure.

**Conséquences :**
- Perte d'organisation
- Problèmes de droits
- Impossibilité de retrouver des fichiers

**Solution :**
- Utilisez des outils qui préservent les métadonnées (rsync -a, tar)
- Testez la restauration complète, pas juste les fichiers

### Erreur #10 : Pas de documentation

**Problème :** Aucune documentation de votre stratégie de sauvegarde.

**Conséquences :**
- En cas de panique, vous ne savez plus où sont les sauvegardes
- Mots de passe oubliés
- Procédures de restauration incertaines

**Solution :**
- Documentez votre stratégie (papier + numérique)
- Listez où sont les sauvegardes
- Notez les mots de passe (gestionnaire de mots de passe)
- Écrivez les procédures de restauration

## Plan de reprise après sinistre

### Qu'est-ce qu'un plan de reprise ?

Un plan de reprise (Disaster Recovery Plan) décrit exactement quoi faire en cas de perte de données majeure.

### Scénarios à prévoir

**Scénario 1 : Perte de fichiers individuels**
- Démarche : Restaurer depuis Backintime ou Déjà Dup
- Temps : 5-10 minutes

**Scénario 2 : Système corrompu mais données intactes**
- Démarche : Restaurer snapshot Timeshift
- Temps : 30 minutes

**Scénario 3 : Disque principal HS**
- Démarche : Remplacer disque + restaurer image Clonezilla
- Temps : 2-4 heures

**Scénario 4 : Ordinateur volé/détruit**
- Démarche : Nouvel ordinateur + restaurer depuis cloud/disque externe hors site
- Temps : 1 jour (avec installation système)

**Scénario 5 : Catastrophe complète**
- Démarche : Récupération depuis cloud uniquement
- Temps : 2-3 jours (réinstallation complète + restauration)

### Exemple de plan de reprise

**Document à créer et conserver en lieu sûr :**

```
═══════════════════════════════════════════════
    PLAN DE REPRISE APRÈS SINISTRE
    Famille Dupont - Mise à jour: Nov 2024
═══════════════════════════════════════════════

INVENTAIRE DES SAUVEGARDES
--------------------------
1. Timeshift: Système
   - Emplacement: /run/timeshift/backup
   - Fréquence: Quotidienne auto
   - Rétention: 5 quotidiennes, 3 hebdo, 2 mensuelles

2. Backintime: Données personnelles
   - Emplacement: Disque USB "Backup-Famille" 2To
   - Fréquence: Quotidienne auto (si connecté)
   - Rétention: 30 jours + versions hebdo/mensuelles

3. Cloud: Documents importants
   - Service: Google Drive
   - Compte: famille.dupont@gmail.com
   - Espace: 100 Go

4. Disque externe secondaire
   - Emplacement physique: Bureau de Marie
   - Mise à jour: Hebdomadaire (échange avec disque principal)
   - Contenu: Copie complète

PROCÉDURE DE RESTAURATION
--------------------------
FICHIER SUPPRIMÉ ACCIDENTELLEMENT:
1. Ouvrir Backintime
2. Naviguer vers le dossier
3. Sélectionner la date
4. Cliquer "Restore"

SYSTÈME CORROMPU:
1. Redémarrer l'ordinateur
2. Au menu GRUB, choisir "Previous Linux versions"
3. Ou: Démarrer avec clé USB Linux Mint Live
4. Ouvrir Timeshift
5. Sélectionner snapshot récent
6. Cliquer "Restore"

DISQUE DUR EN PANNE:
1. Acheter nouveau disque (SSD 500Go minimum)
2. Installer physiquement
3. Démarrer avec clé USB Clonezilla
4. Restaurer dernière image mensuelle
5. Puis restaurer données depuis Backintime

ORDINATEUR PERDU/DÉTRUIT:
1. Acheter nouvel ordinateur
2. Installer Linux Mint
3. Installer Déjà Dup ou Backintime
4. Restaurer depuis Google Drive
5. Ou: Récupérer disque externe chez Marie

CONTACTS D'URGENCE
------------------
Support Linux Mint: forums.linuxmint.com  
Ami technicien: Jean (06 XX XX XX XX)  
Disque externe chez: Marie Dupont, 123 rue Example  

MOTS DE PASSE
-------------
Conservés dans: Bitwarden (famille.dupont@gmail.com)  
Mot de passe maître: [REDACTED - papier dans coffre]  

DERNIÈRE VÉRIFICATION
--------------------
Date: 29/11/2024  
Par: Papa  
Prochain test: 29/12/2024  
```

## Outils complémentaires et ressources

### Outils de sauvegarde supplémentaires

**Borg Backup**
- Sauvegarde déduplicante et chiffrée
- Idéal pour serveurs et utilisateurs avancés
```bash
sudo apt install borgbackup
```

**Restic**
- Moderne, rapide, sécurisé
- Multi-plateforme
```bash
sudo apt install restic
```

**Syncthing**
- Synchronisation P2P entre appareils
- Alternative décentralisée au cloud
```bash
sudo apt install syncthing
```

### Calculateurs et outils de planification

**Calculer l'espace nécessaire :**
```bash
# Taille totale de vos données
du -sh ~/

# Détail par dossier
du -h --max-depth=1 ~/ | sort -h
```

**Surveiller l'espace disque :**
```bash
# Vue graphique
sudo apt install baobab

# En ligne de commande
df -h
```

### Documentation et ressources

**Créer votre documentation :**
- Fichier texte simple dans un endroit sûr
- Copie papier dans un tiroir
- Copie dans votre gestionnaire de mots de passe
- Version dans le cloud

**Que documenter :**
- Liste de toutes vos sauvegardes et emplacements
- Fréquence et type de chaque sauvegarde
- Procédures de restauration étape par étape
- Mots de passe et clés de chiffrement
- Contacts utiles
- Historique des tests et vérifications

## En résumé

Une stratégie de sauvegarde efficace repose sur :

### Les fondamentaux

**La règle 3-2-1 :**
- 3 copies de vos données
- 2 supports différents
- 1 copie hors site

**Types de sauvegardes à combiner :**
- Complète : Base solide
- Incrémentale : Quotidienne économe
- Snapshot système : Protection OS (Timeshift)

**Automatisation :**
- Configurez une fois, oubliez ensuite
- Notifications en cas d'échec
- Vérifications mensuelles

### Adaptation à votre profil

- Débutant : Déjà Dup + cloud + Timeshift
- Intermédiaire : Backintime + disques multiples + Timeshift
- Avancé : NAS + scripts + versioning + Timeshift

### Points critiques

✅ **À FAIRE absolument :**
- Automatiser les sauvegardes quotidiennes
- Tester mensuellement
- Avoir au moins une copie hors site
- Documenter votre stratégie

❌ **À ÉVITER absolument :**
- Sauvegarde manuelle seule (vous oublierez)
- Une seule copie (un seul point de défaillance)
- Sauvegardes jamais testées
- Aucun plan de reprise

### La règle d'or

> "La meilleure stratégie de sauvegarde est celle que vous appliquerez réellement."

Ne cherchez pas la perfection, cherchez l'équilibre entre :
- Protection adéquate
- Simplicité d'utilisation
- Automatisation maximale
- Coût raisonnable

Commencez simplement et améliorez progressivement. L'important est de COMMENCER maintenant, pas d'attendre d'avoir le système parfait !

Vos données ont de la valeur. Protégez-les. Vous ne le regretterez jamais.

⏭️ [Restauration en cas de problème](/17-sauvegarde-et-restauration/05-restauration-en-cas-de-probleme.md)
