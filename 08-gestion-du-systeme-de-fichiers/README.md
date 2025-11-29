🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8. Gestion du système de fichiers

## Introduction au chapitre

Bienvenue dans le chapitre sur la **gestion du système de fichiers** sous Linux Mint ! Ce chapitre est l'un des plus importants pour comprendre comment Linux organise et gère vos données.

### Qu'est-ce que le système de fichiers ?

Le **système de fichiers** (filesystem) désigne deux choses :

1. **L'organisation logique** : Comment Linux structure et organise vos fichiers et dossiers
2. **Le format technique** : Comment les données sont réellement stockées sur le disque (ext4, NTFS, FAT32, etc.)

**Analogie** :
Imaginez votre ordinateur comme une grande bibliothèque :
- **Le système de fichiers** = la méthode de rangement et de classification
- **Les dossiers** = les étagères et les sections
- **Les fichiers** = les livres
- **Les partitions** = les différents bâtiments de la bibliothèque
- **Le montage** = ouvrir une porte pour accéder à un nouveau bâtiment

### Pourquoi ce chapitre est-il important ?

Comprendre le système de fichiers Linux vous permettra de :

- ✅ **Mieux organiser vos données** : Savoir où se trouvent vos fichiers et ceux du système
- ✅ **Gérer vos disques efficacement** : Partitionner, formater, optimiser l'espace
- ✅ **Résoudre les problèmes** : Comprendre les erreurs de montage, de permissions, etc.
- ✅ **Améliorer les performances** : Choisir le bon système de fichiers pour chaque usage
- ✅ **Travailler en dual-boot** : Accéder aux partitions Windows depuis Linux
- ✅ **Automatiser les montages** : Configurer vos disques pour qu'ils se montent au démarrage

### Différences avec Windows

Si vous venez de Windows, vous remarquerez plusieurs différences importantes :

| Concept | Windows | Linux |
|---------|---------|-------|
| **Organisation** | Plusieurs racines (C:, D:, E:) | Une seule racine (/) |
| **Lecteurs** | Lettres automatiques | Points de montage personnalisables |
| **Systèmes de fichiers** | NTFS principalement | ext4, Btrfs, et bien d'autres |
| **Fichiers cachés** | Attribut système | Nom commence par un point (.) |
| **Partitionnement** | Lettres figées | Flexibilité totale |
| **Permissions** | ACL complexes | Système rwx (lecture/écriture/exécution) |

**Ne vous inquiétez pas** : Ces différences deviendront vite naturelles, et vous découvrirez même que l'approche Linux offre plus de flexibilité !

### Vue d'ensemble du chapitre

Ce chapitre est divisé en 7 sections progressives qui vous guideront de la découverte à la maîtrise :

#### 🗂️ **8.1 - L'arborescence Linux**
Découvrez comment Linux organise ses fichiers dans une structure unique commençant par `/` (la racine). Vous comprendrez à quoi servent les dossiers `/home`, `/etc`, `/var`, `/usr`, `/tmp` et bien d'autres.

**Vous apprendrez** :
- La structure des dossiers système
- Où se trouvent vos fichiers personnels
- Quels dossiers ne jamais toucher
- Comment naviguer dans l'arborescence

#### 💾 **8.2 - Les partitions et points de montage**
Comprenez le concept fondamental de partition et de montage sous Linux. Apprenez comment Linux "accroche" différentes partitions dans son arborescence unique.

**Vous apprendrez** :
- Qu'est-ce qu'une partition
- Le concept de point de montage
- Comment Linux nomme les disques (/dev/sda, /dev/nvme0n1)
- Les schémas de partitionnement courants
- La différence entre montage temporaire et permanent

#### 🛠️ **8.3 - Gestion des disques (Disques, GParted)**
Maîtrisez les outils graphiques pour gérer vos disques et partitions. De la simple visualisation au partitionnement avancé.

**Vous apprendrez** :
- Utiliser l'outil Disques (simple et intuitif)
- Utiliser GParted (puissant et complet)
- Créer, supprimer, redimensionner des partitions
- Formater des clés USB et disques externes
- Vérifier l'état de santé de vos disques

#### 📂 **8.4 - Les systèmes de fichiers**
Découvrez les différents systèmes de fichiers disponibles et apprenez à choisir le bon pour chaque usage.

**Vous apprendrez** :
- ext4 : Le standard Linux
- Btrfs : Le moderne avec snapshots
- NTFS : Le système Windows
- FAT32 et exFAT : Pour la compatibilité
- XFS : Les hautes performances
- Comment choisir le bon système pour chaque besoin

#### 🔌 **8.5 - Montage/démontage de périphériques**
Apprenez à monter et démonter correctement vos périphériques, qu'ils soient locaux ou sur le réseau.

**Vous apprendrez** :
- Pourquoi et comment démonter proprement
- Monter manuellement une partition
- Monter des partages réseau (Samba, NFS)
- Monter des images ISO
- Résoudre les problèmes de montage

#### 🔗 **8.6 - Liens symboliques et liens durs**
Découvrez comment créer des "raccourcis" et des références multiples vers vos fichiers sans les dupliquer.

**Vous apprendrez** :
- Qu'est-ce qu'un lien symbolique (comme un raccourci Windows)
- Qu'est-ce qu'un lien dur (concept unique à Linux)
- Quand utiliser l'un ou l'autre
- Créer et gérer des liens
- Cas d'usage pratiques

#### ⚙️ **8.7 - /etc/fstab pour montage automatique**
Configurez vos disques pour qu'ils se montent automatiquement au démarrage du système.

**Vous apprendrez** :
- Qu'est-ce que le fichier /etc/fstab
- Comment l'éditer en toute sécurité
- Ajouter des montages automatiques
- Utiliser les UUID pour identifier les partitions
- Les options de montage courantes
- Dépanner les problèmes de montage

### Prérequis

Pour tirer le meilleur parti de ce chapitre, vous devriez :

- ✅ Avoir installé Linux Mint (chapitres 1 et 2)
- ✅ Être à l'aise avec l'interface graphique (chapitre 4)
- ✅ Connaître les bases du terminal (chapitre 7)
- ✅ Avoir sauvegardé vos données importantes avant toute manipulation de disque

**Niveau** : Débutant à intermédiaire

### Avertissements importants

⚠️ **AVANT DE COMMENCER** :

1. **Sauvegardez vos données** : Toute manipulation de partitions ou de systèmes de fichiers comporte un risque de perte de données. Même si vous faites attention, une erreur est vite arrivée.

2. **Lisez attentivement** : Certaines opérations (formatage, suppression de partition) sont **irréversibles**. Vérifiez toujours deux fois avant de confirmer.

3. **Identifiez correctement vos disques** : Confondre `/dev/sda` et `/dev/sdb` peut effacer le mauvais disque. Prenez le temps de vérifier.

4. **Testez avant de redémarrer** : Surtout pour les modifications de `/etc/fstab`, testez toujours avec `mount -a` avant de redémarrer.

5. **Gardez un Live USB** : En cas de problème grave (système qui ne démarre plus), un Live USB vous permettra de réparer.

### Ce que vous saurez faire après ce chapitre

À la fin de ce chapitre, vous serez capable de :

- 🎯 **Comprendre** l'organisation des fichiers Linux
- 🎯 **Naviguer** efficacement dans l'arborescence système
- 🎯 **Créer et gérer** des partitions
- 🎯 **Choisir** le bon système de fichiers pour chaque usage
- 🎯 **Monter et démonter** n'importe quel périphérique
- 🎯 **Accéder** à vos partitions Windows depuis Linux
- 🎯 **Configurer** des montages automatiques
- 🎯 **Utiliser** des liens symboliques pour organiser vos fichiers
- 🎯 **Résoudre** les problèmes courants de système de fichiers
- 🎯 **Optimiser** l'utilisation de vos disques

### Approche pédagogique

Ce chapitre suit une progression logique :

1. **Comprendre** (8.1, 8.2) : Les concepts de base
2. **Pratiquer** (8.3) : Les outils graphiques
3. **Approfondir** (8.4, 8.5) : Les systèmes de fichiers et le montage
4. **Optimiser** (8.6, 8.7) : Techniques avancées

Chaque section contient :
- Des **explications claires** avec des analogies
- Des **exemples concrets** et pratiques
- Des **captures de commandes** détaillées
- Des **avertissements** pour éviter les erreurs
- Des **astuces** pour aller plus loin

### Pour les utilisateurs Windows

Si vous venez de Windows, ce chapitre vous aidera particulièrement à :

- 💡 Comprendre pourquoi il n'y a pas de "lecteur C:"
- 💡 Accéder à vos partitions Windows depuis Linux
- 💡 Créer des partitions partagées entre Windows et Linux
- 💡 Gérer un dual-boot efficacement
- 💡 Retrouver vos repères dans l'organisation Linux

### Conseils pour bien aborder ce chapitre

**Prenez votre temps** : Les concepts peuvent sembler abstraits au début. N'hésitez pas à relire et à expérimenter avec des données de test.

**Pratiquez en sécurité** :
- Commencez par des clés USB ou disques externes
- Évitez de toucher à vos partitions système tant que vous n'êtes pas à l'aise
- Faites des sauvegardes avant toute manipulation

**Utilisez une approche progressive** :
- Lisez d'abord toute la section
- Essayez sur des données non critiques
- Appliquez ensuite à votre configuration réelle

**N'ayez pas peur de l'interface en ligne de commande** : Certaines opérations sont plus sûres et plus claires en ligne de commande qu'en graphique. Les commandes sont expliquées pas à pas.

### Ressources complémentaires

En complément de ce chapitre, vous pourriez trouver utiles :

- **Chapitre 7** (Le terminal) : Pour comprendre les commandes utilisées
- **Chapitre 17** (Sauvegarde) : Avant toute manipulation de disque
- **Chapitre 23** (Dépannage) : En cas de problème

### Objectifs d'apprentissage

À la fin de ce chapitre, vous devriez pouvoir répondre à ces questions :

- Où Linux stocke-t-il les fichiers système ? Et mes fichiers personnels ?
- Comment créer une nouvelle partition sur mon disque ?
- Quel système de fichiers choisir pour une clé USB partagée avec Windows ?
- Comment faire pour que mon disque externe se monte automatiquement au démarrage ?
- Quelle est la différence entre un lien symbolique et un lien dur ?
- Comment accéder à ma partition Windows depuis Linux ?
- Que faire si mon système ne démarre plus après une modification de /etc/fstab ?

Si vous pouvez répondre à ces questions, vous aurez acquis une solide compréhension de la gestion du système de fichiers sous Linux !

---

## Prêt à commencer ?

Le système de fichiers Linux peut sembler complexe au premier abord, mais il est en réalité très logique et cohérent. Une fois que vous aurez compris les principes de base, vous apprécierez sa flexibilité et sa puissance.

**Commençons par découvrir l'arborescence Linux** et comprenons comment tout s'organise à partir de la racine `/`.

📖 **Passez à la section suivante** : [8.1 - L'arborescence Linux](./01-larborescence-linux.md)

---

**Bon apprentissage et n'oubliez pas : en cas de doute, sauvegardez vos données avant toute manipulation !** 🛡️

⏭️ [L'arborescence Linux (/home, /etc, /var, /usr, /tmp, etc.)](/08-gestion-du-systeme-de-fichiers/01-larborescence-linux.md)
