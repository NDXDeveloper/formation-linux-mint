🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.1 - Préparer sa migration

## Introduction

La migration de Windows vers Linux Mint est une étape importante qui mérite d'être bien préparée. Pas de panique : avec une bonne organisation, cette transition se fera en douceur. Ce chapitre vous guidera dans les étapes préparatoires essentielles pour réussir votre migration.

> 💡 **Bon à savoir** : La migration ne signifie pas forcément abandonner Windows du jour au lendemain. Vous pouvez commencer par un dual-boot (les deux systèmes coexistent) ou tester Linux Mint dans une machine virtuelle.

---

## Pourquoi bien préparer sa migration ?

Une migration bien préparée vous permettra de :
- **Éviter la perte de données** : vos fichiers, photos, documents seront en sécurité
- **Identifier les alternatives** : trouver des équivalents Linux pour vos logiciels Windows
- **Anticiper les problèmes** : détecter d'éventuelles incompatibilités matérielles
- **Gagner du temps** : éviter de chercher ses fichiers ou ses logiciels après l'installation
- **Réduire le stress** : aborder la migration sereinement en sachant ce qui vous attend

---

## Étape 1 : Évaluer vos besoins et votre utilisation

Avant toute chose, prenez le temps de réfléchir à votre utilisation quotidienne de l'ordinateur.

### Posez-vous les bonnes questions

- **Qu'est-ce que je fais principalement sur mon ordinateur ?**
  - Navigation web et emails
  - Bureautique (Word, Excel, PowerPoint)
  - Retouche photo ou montage vidéo
  - Jeux vidéo
  - Développement informatique
  - Comptabilité ou gestion

- **Quels sont mes logiciels indispensables ?**
  - Faites une liste des applications que vous utilisez tous les jours
  - Notez celles dont vous ne pouvez absolument pas vous passer

- **Ai-je des périphériques spécifiques ?**
  - Imprimante, scanner
  - Tablette graphique
  - Casque gaming avec logiciel dédié
  - Matériel professionnel spécialisé

### Réalisme et compromis

Il est important d'être réaliste : certains logiciels très spécialisés (notamment dans le domaine professionnel) n'ont pas d'équivalent sous Linux. Dans ce cas, plusieurs solutions existent :
- Conserver Windows en dual-boot pour ces usages spécifiques
- Utiliser Windows dans une machine virtuelle
- Chercher des alternatives web (applications en ligne)
- Utiliser Wine pour faire fonctionner certains logiciels Windows sous Linux

---

## Étape 2 : Faire l'inventaire de votre système actuel

### Vos données personnelles

Listez tous les endroits où se trouvent vos données importantes :

**Documents et fichiers**
- Bureau Windows
- Dossier Mes Documents
- Dossier Téléchargements
- Dossier Images/Photos
- Dossier Musique
- Dossier Vidéos
- Disques durs externes
- Clés USB

**Paramètres et configurations**
- Favoris du navigateur web
- Mots de passe enregistrés (dans le navigateur ou un gestionnaire)
- Contacts et calendriers
- Profils de messagerie (Outlook, Thunderbird)
- Configurations de logiciels spécifiques

**Données en ligne**
- Comptes cloud (Google Drive, OneDrive, Dropbox)
- Emails en ligne
- Services de stockage photo

> ⚠️ **Important** : N'oubliez pas les données "cachées" comme les fichiers de jeux vidéo (sauvegardes), les projets en cours dans des applications spécialisées, ou les bases de données locales.

### Votre matériel

Notez les caractéristiques de votre ordinateur :
- **Marque et modèle** de l'ordinateur (surtout pour les portables)
- **Processeur** (Intel ou AMD, génération)
- **Mémoire RAM** (4 Go, 8 Go, 16 Go, etc.)
- **Type de disque** (HDD classique ou SSD)
- **Carte graphique** (intégrée, NVIDIA, AMD)
- **Connexions** (WiFi, Bluetooth)

Cette information vous aidera à :
- Vérifier la compatibilité avec Linux Mint
- Choisir la bonne édition (Cinnamon, MATE ou Xfce)
- Anticiper d'éventuels pilotes à installer

### Vos logiciels

Créez un tableau simple de vos applications :

| Logiciel Windows | Usage | Fréquence d'utilisation | Alternative Linux possible |
|------------------|-------|-------------------------|----------------------------|
| Microsoft Word | Rédaction documents | Quotidienne | LibreOffice Writer |
| Chrome | Navigation web | Quotidienne | Firefox (préinstallé) / Chrome |
| Photoshop | Retouche photo | Hebdomadaire | GIMP, Krita |
| iTunes | Musique | Quotidienne | Rhythmbox, Clementine |
| ... | ... | ... | ... |

> 💡 **Astuce** : Vous découvrirez les alternatives Linux en détail dans le chapitre 3.4 de ce tutoriel.

---

## Étape 3 : Sauvegarder vos données

**C'est l'étape la plus cruciale !** Avant toute manipulation, faites une sauvegarde complète de vos données importantes.

### Méthodes de sauvegarde

**1. Disque dur externe**
- Solution la plus simple et fiable
- Copiez manuellement vos dossiers importants
- Avantage : contrôle total, pas de limite de taille

**2. Cloud**
- Google Drive, OneDrive, Dropbox
- Pratique pour les documents
- Attention aux limites de l'offre gratuite

**3. Clés USB**
- Pour des volumes de données réduits
- Pratique pour les documents essentiels
- Moins adapté pour de gros fichiers multimédia

**4. Logiciel de sauvegarde Windows**
- Historique des fichiers Windows
- Sauvegarde et restauration Windows
- Utile si vous prévoyez de revenir en arrière

### Que sauvegarder en priorité ?

**Indispensable :**
- Documents personnels et professionnels
- Photos et vidéos de famille
- Fichiers de travail en cours
- Favoris et mots de passe du navigateur
- Emails locaux (si vous utilisez Outlook, Thunderbird)

**Important :**
- Musique et playlists
- Sauvegardes de jeux
- Projets créatifs (montage vidéo, photo, etc.)
- Configurations de logiciels spécialisés

**Optionnel :**
- Logiciels installés (vous les réinstallerez sous Linux)
- Fichiers système Windows (inutiles sous Linux)

> ⚠️ **Règle d'or** : Appliquez la règle du 3-2-1 : **3** copies de vos données, sur **2** supports différents, dont **1** hors site (cloud).

---

## Étape 4 : Vérifier la compatibilité matérielle

Linux Mint est compatible avec la grande majorité du matériel moderne, mais quelques vérifications s'imposent.

### Points d'attention particuliers

**Carte graphique NVIDIA**
- Fonctionne bien sous Linux Mint
- Nécessite l'installation de pilotes propriétaires
- Installation facilitée par le Gestionnaire de pilotes

**WiFi et Bluetooth**
- La plupart des puces récentes sont supportées
- Certaines puces Broadcom peuvent nécessiter des pilotes spécifiques
- Testable en mode Live avant installation

**Imprimantes**
- Beaucoup d'imprimantes sont reconnues automatiquement
- Les marques HP, Brother, Epson sont généralement bien supportées
- Canon peut nécessiter des pilotes manuels

**Matériel très récent**
- Peut nécessiter un kernel Linux plus récent
- Linux Mint propose des outils pour mettre à jour le kernel facilement

### Comment tester la compatibilité ?

**Méthode 1 : Mode Live**
Le mode Live de Linux Mint (démarrage depuis une clé USB sans installation) vous permet de tester :
- Si votre ordinateur démarre correctement
- Si le WiFi fonctionne
- Si le son est détecté
- Si l'affichage est correct
- Si votre imprimante est reconnue

**Méthode 2 : Recherche en ligne**
- Tapez "Linux Mint + [modèle de votre ordinateur]" dans un moteur de recherche
- Consultez les forums Linux Mint
- Vérifiez les retours d'expérience d'autres utilisateurs

---

## Étape 5 : Choisir le bon moment pour migrer

Le timing de votre migration est important pour minimiser les désagréments.

### Moments favorables

**Idéal :**
- Période de vacances ou de congés
- Week-end prolongé
- Période creuse au travail (si c'est un ordinateur professionnel)

**À éviter :**
- Juste avant une deadline importante
- En période de forte activité professionnelle
- Pendant un projet urgent

### Combien de temps prévoir ?

**Installation de base :**
- 30 minutes à 1 heure pour l'installation de Linux Mint
- 1 à 2 heures pour la configuration initiale

**Configuration complète :**
- 1 journée pour installer vos logiciels
- 2-3 jours pour vous familiariser avec le système
- 1 à 2 semaines pour être totalement à l'aise

> 💡 **Conseil** : Prévoyez une journée complète pour votre migration, même si l'installation est rapide. Cela vous laissera le temps de configurer tranquillement votre système.

---

## Étape 6 : Planifier votre stratégie de migration

Il existe plusieurs approches pour migrer vers Linux Mint. Choisissez celle qui correspond à vos besoins et à votre niveau de confort.

### Option 1 : Dual-boot (les deux systèmes)

**Avantages :**
- Conservation de Windows pour les logiciels spécifiques
- Possibilité de revenir en arrière facilement
- Transition progressive et sans stress
- Idéal pour les débutants

**Inconvénients :**
- Nécessite de redémarrer pour changer de système
- Occupe de l'espace disque pour les deux systèmes
- Risque de rester "bloqué" sur Windows par habitude

**Pour qui ?**
- Les débutants qui veulent tester Linux
- Ceux qui ont des logiciels Windows indispensables
- Les personnes qui veulent une transition douce

### Option 2 : Remplacement complet

**Avantages :**
- Immersion totale dans Linux
- Gain de place sur le disque
- Vous force à trouver des solutions Linux (apprentissage rapide)

**Inconvénients :**
- Pas de retour en arrière facile
- Nécessite d'avoir trouvé toutes les alternatives avant
- Peut être stressant pour les débutants

**Pour qui ?**
- Les utilisateurs confiants
- Ceux qui n'ont pas de dépendance forte à Windows
- Les ordinateurs dédiés (pas le PC principal)

### Option 3 : Machine virtuelle d'abord

**Avantages :**
- Test sans risque
- Apprentissage dans un environnement sécurisé
- Garde Windows comme système principal

**Inconvénients :**
- Performances réduites
- Ne teste pas la compatibilité matérielle réelle
- Expérience utilisateur limitée

**Pour qui ?**
- Les très grands débutants
- Ceux qui veulent découvrir Linux sans engagement
- Phase de test avant installation réelle

---

## Étape 7 : Se préparer mentalement et pratiquement

### Adopter le bon état d'esprit

**Soyez patient avec vous-même**
- Linux n'est pas Windows : certaines choses se font différemment
- Il y aura une courbe d'apprentissage (normale et rapide)
- Les premiers jours peuvent être déroutants

**Restez curieux**
- Explorez le système sans crainte
- Linux Mint est conçu pour être accessible
- La communauté est là pour vous aider

**Acceptez le changement**
- Certains logiciels auront une interface différente
- Les équivalents Linux peuvent être meilleurs... ou différents
- C'est l'occasion de découvrir de nouveaux outils

### Ressources à préparer

**Documentation :**
- Marquez ce tutoriel dans vos favoris
- Notez l'adresse des forums Linux Mint francophones
- Gardez un accès à un smartphone ou une tablette pour chercher de l'aide si besoin

**Support technique :**
- Identifiez une personne-ressource (ami, collègue) qui connaît Linux
- Rejoignez des groupes/forums avant la migration
- Préparez une liste de questions fréquentes

**Matériel :**
- Clé USB pour l'installation (8 Go minimum)
- Disque dur externe pour les sauvegardes
- Connexion Internet stable (pour télécharger des logiciels)

---

## Check-list finale avant la migration

Avant de vous lancer dans l'installation, vérifiez que vous avez bien :

- [ ] Listé tous vos logiciels importants et identifié les alternatives
- [ ] Fait une sauvegarde complète de toutes vos données importantes
- [ ] Vérifié la compatibilité de votre matériel (ou testé en mode Live)
- [ ] Exporté vos favoris et mots de passe du navigateur
- [ ] Sauvegardé vos emails locaux et contacts
- [ ] Noté vos paramètres réseau (si besoin)
- [ ] Choisi votre stratégie de migration (dual-boot ou remplacement)
- [ ] Préparé votre clé USB d'installation Linux Mint
- [ ] Bloqué du temps pour la migration (au moins une demi-journée)
- [ ] Préparé vos ressources d'aide (documentation, contacts)

---

## Conclusion

La préparation est la clé d'une migration réussie. Prenez le temps nécessaire pour ces étapes préliminaires : elles vous éviteront bien des soucis par la suite. Une fois que vous aurez coché tous les points de la check-list, vous serez prêt à passer à l'étape suivante : le transfert de vos données vers Linux Mint.

> 🎯 **Prochaine étape** : Maintenant que vous êtes bien préparé, le chapitre suivant vous guidera dans le transfert effectif de vos données vers votre nouveau système Linux Mint.

---

## Aide-mémoire : Les erreurs à éviter

❌ **Ne pas faire :**
- Installer Linux Mint sans avoir sauvegardé vos données
- Supprimer Windows si vous n'êtes pas sûr de vos alternatives logicielles
- Sous-estimer le temps nécessaire pour la transition
- Avoir peur de poser des questions à la communauté

✅ **À faire :**
- Prendre son temps pour la préparation
- Tester en mode Live ou en machine virtuelle d'abord
- Garder une copie de Windows (dual-boot) au début
- Se documenter et utiliser les ressources communautaires
- Être patient et curieux pendant l'apprentissage

⏭️ [Transférer ses données](/03-migration-depuis-windows/02-transferer-ses-donnees.md)
