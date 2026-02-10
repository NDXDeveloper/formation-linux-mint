🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 17. Sauvegarde et restauration

## Introduction

Bienvenue dans le chapitre le plus important de ce guide Linux Mint ! La sauvegarde et la restauration de vos données ne sont pas optionnelles : elles sont **essentielles**. Ce chapitre vous explique comment protéger efficacement votre système et vos données précieuses.

### Pourquoi ce chapitre est crucial

**Une vérité inconfortable :** Ce n'est pas une question de "si" vous perdrez des données, mais de "quand". Les pannes de disque dur, les erreurs humaines, les bugs logiciels, les virus, les vols et les catastrophes naturelles arrivent à tout le monde, tôt ou tard.

**La bonne nouvelle :** Avec une stratégie de sauvegarde appropriée, vous pouvez vous remettre de pratiquement n'importe quelle catastrophe informatique en quelques heures, voire quelques minutes, sans perdre une seule donnée importante.

### Les deux types de pertes de données

Il existe deux scénarios principaux de perte de données, et ce chapitre vous prépare aux deux :

#### 1. Perte du système (Linux Mint lui-même)

**Exemples de problèmes système :**
- Mise à jour qui casse le système
- Installation d'un pilote incompatible
- Modification de configuration qui empêche le démarrage
- Corruption de fichiers système
- Suppression accidentelle de fichiers critiques

**Solution :** Timeshift et les snapshots système vous permettent de revenir à un état stable en quelques minutes.

#### 2. Perte de données personnelles

**Exemples de pertes de données :**
- Suppression accidentelle de photos de famille irremplaçables
- Disparition de documents de travail importants
- Corruption de projets en cours
- Panne du disque dur qui détruit tout
- Ordinateur volé avec toutes vos données

**Solution :** Sauvegardes régulières de vos fichiers personnels avec plusieurs copies, y compris hors site (cloud).

### Témoignages réels

> *"J'avais 10 ans de photos de mes enfants. Mon disque dur a lâché un dimanche soir. Tout était perdu. Je n'avais jamais fait de sauvegarde parce que 'je le ferais plus tard'. Je donnerais n'importe quoi pour récupérer ces photos."* — Marc, utilisateur Linux

> *"Grâce à Timeshift, j'ai pu récupérer mon système en 15 minutes après une mise à jour désastreuse de pilotes NVIDIA. Sans ça, j'aurais dû réinstaller complètement."* — Sophie, utilisatrice Linux Mint

> *"Mon ordinateur portable a été volé en voyage. Heureusement, tout était sauvegardé dans le cloud et sur un disque externe chez mes parents. J'ai récupéré toutes mes données sur le nouvel ordinateur."* — Thomas, photographe

**Ne devenez pas une statistique.** Après avoir lu ce chapitre et mis en place vos sauvegardes, vous pourrez dormir tranquille.

## Vue d'ensemble du chapitre

Ce chapitre est structuré pour vous guider progressivement de la sauvegarde la plus simple à une stratégie complète et professionnelle.

### Ce que vous allez apprendre

**Protection du système :**
- Comment créer et restaurer des snapshots de votre système avec Timeshift
- Revenir à un état stable après un problème
- Se remettre d'une mise à jour problématique en quelques minutes

**Protection de vos données :**
- Sauvegarder automatiquement vos documents, photos et fichiers
- Utiliser plusieurs outils (Déjà Dup, Backintime, rsync)
- Créer des sauvegardes incrémentales intelligentes

**Sauvegarde complète :**
- Cloner entièrement votre disque dur avec Clonezilla
- Créer une image de secours bootable
- Utiliser l'outil dd pour des copies bit à bit

**Stratégie globale :**
- Appliquer la règle 3-2-1 (la référence professionnelle)
- Adapter votre stratégie à votre profil et besoins
- Automatiser pour ne jamais oublier

**Restauration :**
- Récupérer des fichiers supprimés accidentellement
- Restaurer votre système après un crash
- Procédures complètes de récupération après catastrophe

**Cloud automatisé :**
- Synchroniser vos données importantes dans le cloud
- Configurer Nextcloud, Google Drive, Dropbox, etc.
- Chiffrer vos données sensibles
- Avoir accès à vos fichiers partout

### Structure du chapitre

```
17. Sauvegarde et restauration
│
├── 17.1 Timeshift pour sauvegardes système
│   └── Protection rapide et efficace de Linux Mint
│
├── 17.2 Sauvegarde de données
│   └── Protéger vos documents, photos, fichiers personnels
│
├── 17.3 Clonage de disque
│   └── Copie complète du système et des données
│
├── 17.4 Stratégies de sauvegarde (règle 3-2-1)
│   └── Construire une protection professionnelle
│
├── 17.5 Restauration en cas de problème
│   └── Procédures de récupération étape par étape
│
└── 17.6 Sauvegarde cloud automatisée
    └── Protection hors site et accès universel
```

### Approche pédagogique

**Progression logique :**
1. **Commencez simple** : Timeshift pour le système (15 minutes à configurer)
2. **Ajoutez vos données** : Sauvegarde de fichiers (30 minutes)
3. **Comprenez les options** : Clonage complet si nécessaire
4. **Pensez stratégie** : La règle 3-2-1 pour une vraie protection
5. **Préparez-vous** : Comment restaurer quand ça arrive
6. **Automatisez** : Cloud pour protection hors site

**Vous n'avez pas besoin de tout faire immédiatement !** Commencez par le minimum (17.1 et 17.2), puis améliorez progressivement votre stratégie.

## Concepts fondamentaux

Avant de plonger dans les détails techniques, comprenons quelques concepts essentiels.

### Types de sauvegardes

#### 1. Snapshot (instantané système)

**Qu'est-ce que c'est :**
Une "photographie" de votre système d'exploitation à un moment précis.

**Ce qui est sauvegardé :**
- Linux Mint lui-même
- Applications installées
- Configuration système
- Paramètres

**Ce qui N'est PAS sauvegardé :**
- Vos documents personnels (/home)
- Vos photos et vidéos
- Vos téléchargements

**Outil principal :** Timeshift

**Quand l'utiliser :**
Avant chaque mise à jour majeure, installation de pilotes, ou modification système.

#### 2. Sauvegarde de fichiers

**Qu'est-ce que c'est :**
Copie de vos fichiers personnels (documents, photos, etc.).

**Ce qui est sauvegardé :**
- Tout votre dossier /home
- Documents, images, vidéos
- Musique, téléchargements
- Configurations personnelles

**Ce qui N'est PAS sauvegardé :**
- Le système Linux Mint
- Les applications installées

**Outils principaux :** Déjà Dup, Backintime, rsync

**Quand l'utiliser :**
Automatiquement, tous les jours ou toutes les semaines.

#### 3. Clone complet (image disque)

**Qu'est-ce que c'est :**
Copie bit à bit de votre disque dur entier.

**Ce qui est sauvegardé :**
- TOUT : système + données
- Partitions et structure
- Secteur de boot
- Configuration complète

**Avantage :**
Restauration identique sur un nouveau disque.

**Outils principaux :** Clonezilla, dd

**Quand l'utiliser :**
Avant remplacement de disque, ou sauvegarde mensuelle complète.

### La règle 3-2-1 : Le standard de l'industrie

C'est la règle d'or des sauvegardes professionnelles, et vous devriez l'adopter aussi :

**3** = Trois copies de vos données
- 1 originale (sur votre ordinateur)
- 2 sauvegardes supplémentaires

**2** = Sur deux supports différents
- Exemple : disque interne + disque externe
- Ou : disque interne + cloud
- Diversifie les risques

**1** = Une copie hors site
- Cloud (serveurs distants)
- Disque externe chez un ami/famille
- Au bureau si vous travaillez de la maison
- Protection contre incendie, vol, inondation

**Pourquoi ça fonctionne :**

Imaginez ces scénarios :

**Scénario 1 : Panne de disque dur**
- ✅ Copie 2 : Disque externe → OK
- ✅ Copie 3 : Cloud → OK
- **Résultat :** Aucune perte !

**Scénario 2 : Incendie/Vol**
- ❌ Original : Détruit
- ❌ Copie 2 (disque externe sur place) : Détruit/volé
- ✅ Copie 3 (cloud) → OK
- **Résultat :** Données sauvées !

**Scénario 3 : Suppression accidentelle**
- ✅ Copie 2 : Version récente
- ✅ Copie 3 : Version un peu plus ancienne
- **Résultat :** Récupération facile !

### Automatisation : La clé du succès

**La réalité humaine :**
- On oublie de faire les sauvegardes manuelles
- On reporte à plus tard
- On pense "je le ferai demain"
- Et puis le désastre arrive

**La solution :**  
**Automatisez TOUT ce qui peut l'être !**  

- ✅ Snapshots Timeshift : automatiques quotidiens
- ✅ Sauvegarde fichiers : automatique quotidienne/hebdomadaire
- ✅ Synchronisation cloud : continue en arrière-plan
- ✅ Vérifications : rappels mensuels

**Principe fondamental :** Une sauvegarde automatique que vous oubliez est infiniment meilleure qu'une sauvegarde manuelle que vous ne faites jamais.

### Temps vs Protection

**Question fréquente :** "Combien de temps ça prend ?"

Voici les investissements en temps réalistes :

| Action | Temps initial | Temps récurrent |
|--------|---------------|-----------------|
| **Timeshift (système)** | 30 min configuration | 0 min (automatique) |
| **Backintime (données)** | 45 min configuration | 0 min (automatique) |
| **Cloud (Nextcloud)** | 1h configuration | 0 min (automatique) |
| **Image Clonezilla** | 2h première fois | 2h/mois (optionnel) |
| **Vérification mensuelle** | - | 15 min/mois |
| **TOTAL initial** | ~4 heures | ~15 min/mois |

**Comparaison :**
- Temps pour recréer 10 ans de données perdues : **IMPOSSIBLE**
- Temps pour réinstaller et reconfigurer un système : **8-16 heures**
- Temps pour restaurer depuis une sauvegarde : **30 minutes - 2 heures**

**Le choix est évident !**

## Niveaux de protection

Selon vos besoins et votre temps, voici trois niveaux de protection :

### Niveau 1 : Protection minimale (1 heure)

**Pour qui :** Débutants absolus, usage occasionnel

**Ce qu'il faut faire :**
1. Configurer Timeshift (système)
2. Configurer Déjà Dup vers disque externe (données)
3. Activer Google Drive ou autre cloud gratuit

**Protection :**
- ✅ Récupération après problème système
- ✅ Récupération fichiers supprimés récemment
- ✅ Une copie hors site (cloud limité)

**Limites :**
- ⚠️ Pas de redondance complète (pas vraiment 3-2-1)
- ⚠️ Cloud limité en espace

### Niveau 2 : Protection complète (4 heures)

**Pour qui :** Utilisateurs réguliers, données importantes

**Ce qu'il faut faire :**
1. Timeshift automatique quotidien
2. Backintime vers disque externe quotidien
3. Cloud synchronisé (Nextcloud, Dropbox)
4. Disque externe secondaire (rotation hebdomadaire)
5. Image Clonezilla mensuelle

**Protection :**
- ✅ Règle 3-2-1 respectée
- ✅ Versions multiples des fichiers
- ✅ Protection contre toutes les catastrophes
- ✅ Récupération rapide

**Avantages :**
- 🏆 Protection professionnelle
- 🏆 Tranquillité d'esprit totale

### Niveau 3 : Protection professionnelle (1 journée)

**Pour qui :** Créateurs de contenu, professionnels, données critiques

**Ce qu'il faut faire :**
- Tout du niveau 2
- NAS domestique avec RAID
- Scripts personnalisés
- Chiffrement des sauvegardes
- Rotation multiple de disques
- Surveillance et alertes automatiques

**Protection :**
- ✅ Redondance maximale
- ✅ Automatisation complète
- ✅ Chiffrement des données sensibles
- ✅ Monitoring proactif

## Ce que vous n'avez PAS besoin de faire

Pour rassurer les débutants, voici ce qui n'est **PAS** nécessaire :

❌ **Acheter des solutions commerciales coûteuses**
- Les outils open source gratuits sont excellents

❌ **Avoir un NAS professionnel**
- Un simple disque externe USB suffit pour commencer

❌ **Tout sauvegarder partout**
- Soyez sélectif, concentrez-vous sur l'important

❌ **Sauvegarder Windows si vous êtes en dual-boot**
- Windows a ses propres outils de sauvegarde

❌ **Sauvegarder les téléchargements et fichiers temporaires**
- Ils sont récupérables, économisez de l'espace

❌ **Sauvegarder tous les jeux**
- Concentrez-vous sur les sauvegardes de progression uniquement

❌ **Comprendre tous les détails techniques**
- Suivez les guides, ça marchera !

## Matériel recommandé

Pour mettre en place vos sauvegardes, voici le matériel utile :

### Budget minimal (~50€)

**Essentiel :**
- 1 disque externe USB 1-2 To (~40-50€)
- Compte cloud gratuit (Google Drive 15 Go, Mega 20 Go)

**Avec ça, vous pouvez :**
- Sauvegarder système et données localement
- Avoir une copie hors site limitée

### Budget recommandé (~150€)

**Idéal pour la plupart :**
- 2 disques externes USB 2 To (~40€ × 2)
- Abonnement cloud 100-200 Go (~2-3€/mois ou 25-35€/an)
- Ou Nextcloud hébergé (~50€/an)

**Avec ça, vous pouvez :**
- Rotation de disques externes
- Sauvegarde cloud complète
- Règle 3-2-1 respectée

### Budget optimal (~300-500€)

**Pour protection maximale :**
- NAS 2 baies avec disques en RAID (~250-350€)
- 1 disque externe pour sauvegarde hors site (~50€)
- Cloud haute capacité (~100€/an)

**Avec ça, vous pouvez :**
- Redondance matérielle (RAID)
- Sauvegardes automatiques continues
- Protection professionnelle

### Conseil d'achat

**Disques durs :**
- Préférez des marques reconnues (Western Digital, Seagate, Toshiba)
- Pour sauvegarde : disques "Red" ou "backup" plutôt que "Blue"
- USB 3.0 minimum (bien plus rapide)
- Taille : minimum 2× votre espace utilisé actuel

**NAS (optionnel) :**
- Synology : excellent mais cher
- QNAP : bon rapport qualité/prix
- OMV (Open Media Vault) : gratuit sur ancien PC/Raspberry Pi

## Foire aux questions (FAQ)

**Q : Je n'ai jamais fait de sauvegarde, par où commencer ?**

R : Commencez par le niveau 1 (protection minimale) immédiatement :
1. Configurez Timeshift (30 min)
2. Configurez Déjà Dup vers un disque externe (30 min)
3. Activez Google Drive pour documents importants (15 min)

Puis améliorez progressivement vers le niveau 2 quand vous serez à l'aise.

---

**Q : Combien de place faut-il pour les sauvegardes ?**

R : Règle générale : **prévoyez 2-3× la taille de vos données**.
- Données actuelles : 100 Go
- Disque de sauvegarde : 250-300 Go minimum

Les sauvegardes incrémentales économisent beaucoup d'espace.

---

**Q : À quelle fréquence sauvegarder ?**

R : Réponse simple : **quotidiennement** pour le système et données en cours.

Posez-vous la question : "Combien de données puis-je accepter de perdre ?"
- Travail quotidien → sauvegarde quotidienne
- Modifications hebdomadaires → sauvegarde hebdomadaire

---

**Q : Le cloud est-il sûr ?**

R : Oui, SI vous chiffrez vos données sensibles. Utilisez :
- Cryptomator pour chiffrer avant upload
- Services respectueux de la vie privée (Nextcloud)
- 2FA (double authentification) sur tous vos comptes

---

**Q : Timeshift sauvegarde-t-il mes documents ?**

R : **NON !** C'est un malentendu fréquent. Timeshift sauvegarde UNIQUEMENT le système Linux Mint, pas vos fichiers personnels. Vous avez besoin d'un outil séparé (Backintime, Déjà Dup) pour vos données.

---

**Q : Puis-je sauvegarder sur le même disque ?**

R : Techniquement oui, mais **vraiment déconseillé**. Si le disque meurt, vous perdez tout (original + sauvegarde). Utilisez toujours un support physiquement séparé.

---

**Q : Combien de temps garder les sauvegardes ?**

R : Stratégie recommandée (GFS - Grandfather-Father-Son) :
- Quotidiennes : 7 jours
- Hebdomadaires : 4 semaines
- Mensuelles : 12 mois
- Annuelles : archives permanentes

---

**Q : Faut-il vraiment tester les restaurations ?**

R : **OUI, absolument !** Citation célèbre : "Vous n'avez pas de sauvegarde tant que vous n'avez pas testé la restauration."

Testez mensuellement la restauration d'un fichier. C'est 5 minutes qui peuvent vous sauver des années de regrets.

---

**Q : Mon disque de sauvegarde a 10 ans, est-ce un problème ?**

R : **OUI !** Les disques durs ont une durée de vie limitée (3-5 ans en usage intensif). Remplacez vos disques de sauvegarde tous les 3-5 ans. Vérifiez régulièrement leur santé avec SMART.

---

**Q : Je suis en dual-boot Windows/Linux, que sauvegarder ?**

R : Séparez vos stratégies :
- **Linux :** Timeshift + Backintime (comme ce chapitre)
- **Windows :** Outil Windows natif ou Macrium Reflect
- **Données partagées :** Sauvegardées avec Linux et/ou cloud

## Motivation finale

Imaginez ces deux scénarios...

### Scénario A : Sans sauvegarde

Lundi matin, votre ordinateur ne démarre plus. Écran noir. Panique.

Après diagnostic : disque dur mort. Toutes vos données :
- 10 ans de photos de famille
- Tous vos documents de travail
- Vos projets en cours
- Vos configurations personnalisées

**Tout est perdu. Irrécupérable.**

Vous passez les jours suivants à :
- Pleurer la perte de souvenirs irremplaçables
- Réinstaller tout le système (8 heures)
- Reconfigurer tous vos logiciels (6 heures)
- Contacter un service de récupération (500-2000€, sans garantie)
- Expliquer à votre famille pourquoi les photos sont perdues

**Coût :** Temps inestimable + 500-2000€ + stress énorme + données perdues à jamais

### Scénario B : Avec sauvegardes (ce chapitre)

Lundi matin, votre ordinateur ne démarre plus. Écran noir.

Vous restez calme. Vous savez que :
- Timeshift a un snapshot d'hier
- Backintime a sauvegardé vos données hier soir
- Le cloud a une copie synchronisée
- Vous avez testé la restauration le mois dernier

Votre plan :
1. Achetez un nouveau SSD (60€, 1 heure)
2. Restaurez l'image Clonezilla (2 heures)
3. Ou réinstallez Linux Mint et restaurez tout (3 heures)

**Mardi matin :** Vous travaillez normalement. Tout est là. Zéro perte.

Vous racontez l'incident à vos collègues comme une anecdote amusante : "Mon disque est mort hier, mais j'ai tout récupéré en 2 heures grâce aux sauvegardes !"

**Coût :** 60€ (nouveau disque) + 3 heures + aucun stress

## Prêt à commencer ?

**Ce chapitre vous semble intimidant ?** C'est normal. Mais rappelez-vous :
- Vous n'avez pas besoin de tout faire en une fois
- Commencez par le strict minimum (17.1 et 17.2)
- Améliorez progressivement
- Chaque sauvegarde mise en place est une victoire

**Les 6 sections de ce chapitre sont conçues pour être suivies dans l'ordre, mais vous pouvez aussi :**
- Lire 17.1 et 17.2, les mettre en place, vous arrêter là (déjà excellent !)
- Revenir plus tard pour améliorer avec 17.4 (stratégie 3-2-1)
- Ajouter le cloud (17.6) quand vous êtes à l'aise

**L'important est de COMMENCER.**

Une sauvegarde basique aujourd'hui vaut infiniment mieux qu'une sauvegarde parfaite jamais mise en place.

---

**Investissement de temps total :** 4-8 heures (une seule fois)

**Tranquillité d'esprit :** Inestimable

**Sommeil paisible sachant que vos données sont protégées :** N'a pas de prix

---

**Prêt ?** Passons à la première section : 17.1 Timeshift pour sauvegardes système

Vos données méritent d'être protégées. Commençons maintenant ! 🛡️

⏭️ [Timeshift pour sauvegardes système (snapshots)](/17-sauvegarde-et-restauration/01-timeshift-pour-sauvegardes-systeme.md)
