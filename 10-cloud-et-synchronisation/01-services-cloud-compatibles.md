🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 10.1 Services cloud compatibles

## Qu'est-ce que le cloud ?

Le **cloud** (nuage en français) désigne des services de stockage et de synchronisation de fichiers sur Internet. Au lieu de garder vos fichiers uniquement sur votre ordinateur, vous les stockez également sur des serveurs distants accessibles depuis n'importe où.

### Avantages du cloud

- **Accessibilité** : Vos fichiers sont disponibles depuis n'importe quel appareil connecté à Internet
- **Sauvegarde automatique** : Vos données sont protégées en cas de panne de votre ordinateur
- **Partage facile** : Vous pouvez partager des fichiers avec d'autres personnes simplement
- **Synchronisation** : Les modifications sont automatiquement synchronisées entre tous vos appareils

## Services cloud populaires compatibles avec Linux Mint

### 1. **Nextcloud / ownCloud**

**Type** : Solution auto-hébergée ou avec hébergement tiers

**Points forts** :
- Totalement open source
- Contrôle complet de vos données
- Aucune limite de stockage (selon votre serveur)
- Respectueux de la vie privée
- Applications natives pour Linux

**Points faibles** :
- Nécessite des connaissances techniques pour l'auto-hébergement
- Coût d'hébergement si vous passez par un prestataire

**Compatibilité Linux Mint** : ⭐⭐⭐⭐⭐ Excellente

Nextcloud et ownCloud proposent des clients de bureau natifs qui s'intègrent parfaitement à Linux Mint. C'est souvent le choix privilégié des utilisateurs Linux soucieux de leur vie privée.

---

### 2. **Google Drive**

**Type** : Service commercial

**Points forts** :
- 15 Go gratuits
- Intégration avec l'écosystème Google (Gmail, Docs, Photos)
- Très populaire et fiable
- Partage de fichiers simple

**Points faibles** :
- Pas de client officiel pour Linux
- Nécessite des solutions tierces (voir chapitre 10.3)
- Politique de confidentialité questionnée

**Compatibilité Linux Mint** : ⭐⭐⭐ Moyenne (nécessite des outils tiers)

Bien que Google ne propose pas de client officiel, plusieurs solutions existent pour utiliser Google Drive sous Linux Mint :
- **Insync** (payant, très performant)
- **rclone** (gratuit, en ligne de commande)
- **GNOME Online Accounts** (intégration système)

---

### 3. **Dropbox**

**Type** : Service commercial

**Points forts** :
- 2 Go gratuits (peut être augmenté avec parrainages)
- Client officiel pour Linux
- Très stable et éprouvé
- Synchronisation rapide

**Points faibles** :
- Espace gratuit limité
- Prix élevé pour les offres payantes
- Client Linux parfois en retard sur les fonctionnalités

**Compatibilité Linux Mint** : ⭐⭐⭐⭐ Bonne

Dropbox propose un client officiel pour Linux, bien que celui-ci reçoive moins de mises à jour que les versions Windows/Mac. Il fonctionne néanmoins de manière stable sous Linux Mint.

---

### 4. **MEGA**

**Type** : Service commercial

**Points forts** :
- 20 Go gratuits (le plus généreux)
- Chiffrement de bout en bout (E2EE)
- Client officiel pour Linux (MEGAsync)
- Bonne vitesse de transfert

**Points faibles** :
- Interface parfois moins intuitive
- Historique controversé du fondateur

**Compatibilité Linux Mint** : ⭐⭐⭐⭐ Bonne

MEGA fournit MEGAsync, un client de synchronisation natif pour Linux qui fonctionne très bien sous Linux Mint. L'espace gratuit généreux en fait une option intéressante.

---

### 5. **pCloud**

**Type** : Service commercial

**Points forts** :
- 10 Go gratuits
- Option d'achat à vie (pas d'abonnement)
- Client Linux natif
- Chiffrement disponible (Crypto)
- Serveurs en Europe (Suisse)

**Points faibles** :
- Le chiffrement côté client est payant en supplément
- Prix d'achat à vie élevé

**Compatibilité Linux Mint** : ⭐⭐⭐⭐ Bonne

pCloud offre un client Linux stable avec une interface simple. L'option d'achat à vie peut être intéressante pour éviter les abonnements récurrents.

---

### 6. **OneDrive** (Microsoft)

**Type** : Service commercial

**Points forts** :
- 5 Go gratuits
- Intégration avec Microsoft 365
- Espace supplémentaire avec abonnement Microsoft 365

**Points faibles** :
- Pas de client officiel pour Linux
- Nécessite des solutions de contournement

**Compatibilité Linux Mint** : ⭐⭐ Faible (nécessite des outils tiers)

Microsoft ne propose pas de support officiel pour Linux. Il faut utiliser des solutions tierces comme :
- **rclone** (ligne de commande)
- **OneDrive-D** (client non officiel)
- Accès via navigateur web uniquement

---

### 7. **Syncthing**

**Type** : Solution open source de synchronisation pair-à-pair

**Points forts** :
- Totalement gratuit et open source
- Pas de serveur central (synchronisation directe entre appareils)
- Aucune limite de stockage
- Respect total de la vie privée
- Fonctionne parfaitement sous Linux

**Points faibles** :
- Pas de stockage cloud externe (uniquement entre vos appareils)
- Interface moins intuitive pour les débutants
- Nécessite que vos appareils soient allumés pour synchroniser

**Compatibilité Linux Mint** : ⭐⭐⭐⭐⭐ Excellente

Syncthing est parfait pour synchroniser des fichiers entre vos propres appareils (PC, laptop, smartphone) sans passer par un service tiers. Très apprécié des utilisateurs Linux.

---

### 8. **Proton Drive**

**Type** : Service commercial axé sur la confidentialité

**Points forts** :
- Chiffrement de bout en bout
- Basé en Suisse (protection des données)
- 5 Go gratuits
- Philosophie axée sur la vie privée

**Points faibles** :
- Pas encore de client Linux natif (en développement)
- Service relativement récent
- Fonctionnalités limitées par rapport aux concurrents

**Compatibilité Linux Mint** : ⭐⭐ Faible (accès web uniquement pour le moment)

Proton Drive est accessible via navigateur web. Un client Linux est en développement mais pas encore disponible au moment de la rédaction de ce guide.

---

## Tableau comparatif rapide

| Service | Espace gratuit | Client Linux natif | Open Source | Vie privée |
|---------|----------------|-------------------|-------------|------------|
| **Nextcloud/ownCloud** | Illimité* | ✅ Oui | ✅ Oui | ⭐⭐⭐⭐⭐ |
| **Google Drive** | 15 Go | ❌ Non | ❌ Non | ⭐⭐ |
| **Dropbox** | 2 Go | ✅ Oui | ❌ Non | ⭐⭐⭐ |
| **MEGA** | 20 Go | ✅ Oui | ❌ Non | ⭐⭐⭐⭐ |
| **pCloud** | 10 Go | ✅ Oui | ❌ Non | ⭐⭐⭐ |
| **OneDrive** | 5 Go | ❌ Non | ❌ Non | ⭐⭐ |
| **Syncthing** | Illimité** | ✅ Oui | ✅ Oui | ⭐⭐⭐⭐⭐ |
| **Proton Drive** | 5 Go | ❌ Non*** | ❌ Non | ⭐⭐⭐⭐⭐ |

\* Dépend de votre hébergement
\** Limité par l'espace disque de vos appareils
\*** En développement

---

## Quel service choisir ?

### Pour les débutants Linux qui veulent :

**Une solution simple et gratuite** → **MEGA** (20 Go gratuits, client natif)

**Garder leurs habitudes Google** → **Google Drive** avec **Insync** ou **rclone**

**Une solution respectueuse de la vie privée** → **Nextcloud** (si vous trouvez un hébergeur) ou **Syncthing** (entre vos appareils)

**Un bon équilibre** → **pCloud** (achat à vie intéressant) ou **Dropbox** (très stable)

---

### Pour les utilisateurs avancés :

**Contrôle total et vie privée** → **Nextcloud auto-hébergé**

**Synchronisation sans serveur** → **Syncthing**

**Besoin d'intégration Google** → **rclone** avec automatisation

---

## Conseils importants

### 🔒 Sécurité

1. **Activez l'authentification à deux facteurs** (2FA) sur tous vos services cloud
2. **Utilisez des mots de passe forts et uniques** pour chaque service
3. **Ne stockez jamais de données sensibles** non chiffrées dans le cloud
4. **Vérifiez régulièrement** les appareils connectés à votre compte

### 💾 Bonnes pratiques

1. **Le cloud n'est pas une sauvegarde** : Gardez toujours une copie locale de vos fichiers importants
2. **Suivez la règle 3-2-1** : 3 copies, sur 2 supports différents, dont 1 hors site
3. **Surveillez votre espace** : Les quotas gratuits peuvent être vite atteints
4. **Attention à la bande passante** : La synchronisation initiale peut être longue

### 📁 Organisation

1. **Ne synchronisez pas tout** : Sélectionnez uniquement les dossiers nécessaires
2. **Créez une structure claire** : Organisez vos fichiers de manière logique
3. **Évitez les fichiers volumineux** : Privilégiez le cloud pour les documents importants
4. **Nettoyez régulièrement** : Supprimez les fichiers inutiles

---

## Compatibilité avec Linux Mint : Ce qu'il faut retenir

Linux Mint fonctionne très bien avec la plupart des services cloud, mais :

- **Les services avec clients natifs** (Dropbox, MEGA, Nextcloud) offrent la meilleure expérience
- **Google Drive et OneDrive** nécessitent des solutions tierces mais restent utilisables
- **Les solutions open source** (Nextcloud, Syncthing) sont souvent privilégiées par la communauté Linux
- **L'accès web** fonctionne toujours pour tous les services

---

## Prochaines étapes

Dans les chapitres suivants, nous verrons en détail :

- **10.2** - Comment installer et configurer Nextcloud/ownCloud
- **10.3** - Synchroniser Google Drive avec Insync ou rclone
- **10.4** - Configuration de Dropbox, OneDrive et autres services
- **10.5** - Utiliser Syncthing pour synchroniser entre vos appareils

---

## Ressources utiles

- Site officiel Nextcloud : https://nextcloud.com
- Site officiel Syncthing : https://syncthing.net
- Comparateur de services cloud : https://www.cloudwards.net
- Forum Linux Mint (section Cloud) : https://forums.linuxmint.com

---

**Note** : Les informations sur les offres gratuites et les fonctionnalités peuvent évoluer. Vérifiez toujours les conditions actuelles sur les sites officiels des services.

⏭️ [Nextcloud / ownCloud (auto-hébergé)](/10-cloud-et-synchronisation/02-nextcloud-owncloud.md)
