🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 2.3 Test en mode Live

## Introduction

Avant d'installer Linux Mint définitivement sur votre ordinateur, vous pouvez le tester grâce au **mode Live**. C'est l'une des fonctionnalités les plus pratiques et rassurantes de Linux Mint !

### Qu'est-ce que le mode Live ?

Le **mode Live** vous permet d'utiliser Linux Mint directement depuis votre clé USB, sans rien installer sur votre disque dur. Votre ordinateur démarre sur la clé USB et vous pouvez explorer le système complet.

> 💡 **Analogie** : C'est comme faire un essai routier avant d'acheter une voiture. Vous pouvez tester toutes les fonctionnalités sans engagement.

### Pourquoi utiliser le mode Live ?

Le mode Live est utile pour :

- ✅ **Découvrir l'interface** sans risque
- ✅ **Tester la compatibilité** avec votre matériel (WiFi, carte graphique, son, etc.)
- ✅ **Voir si Linux Mint vous plaît** avant de l'installer
- ✅ **Vérifier que tout fonctionne** correctement
- ✅ **Accéder à vos fichiers** en cas de problème avec Windows
- ✅ **Dépanner votre ordinateur** si Windows ne démarre plus

### Rassurance importante

> 🔒 **Votre ordinateur est en sécurité** : Le mode Live ne modifie RIEN sur votre disque dur. Windows reste intact, vos fichiers sont préservés. Vous pouvez redémarrer normalement à tout moment.

---

## Prérequis

Avant de commencer, assurez-vous d'avoir :

- ✅ Une **clé USB bootable** Linux Mint (créée à l'étape précédente)
- ✅ Un **ordinateur** à tester
- ✅ **30 minutes à 1 heure** pour explorer tranquillement
- ✅ Une connexion **Internet** (optionnelle mais utile)

---

## Étape 1 : Démarrer sur la clé USB

Pour utiliser le mode Live, vous devez faire démarrer votre ordinateur sur la clé USB au lieu de votre disque dur habituel.

### Insérer la clé USB

1. **Éteignez complètement** votre ordinateur (pas de mise en veille)
2. **Insérez la clé USB** Linux Mint dans un port USB
3. **Utilisez de préférence un port USB 3.0** (généralement bleu) pour plus de rapidité

> 💡 **Astuce** : Sur un PC portable, utilisez les ports USB sur les côtés plutôt qu'à l'arrière si possible.

### Méthode 1 : Le menu de démarrage (Boot Menu) - Recommandé

C'est la méthode la plus simple et la plus rapide pour les débutants.

#### Redémarrer et accéder au Boot Menu

1. **Allumez** ou **redémarrez** votre ordinateur
2. **Appuyez immédiatement et plusieurs fois** sur la touche du Boot Menu dès que l'ordinateur démarre
3. **Maintenez la touche enfoncée** si nécessaire

#### Quelle touche utiliser ?

La touche dépend de la marque de votre ordinateur :

| Marque | Touche Boot Menu | Touches alternatives |
|--------|------------------|---------------------|
| **Dell** | F12 | F2 |
| **HP** | F9 ou Échap | F10 |
| **Lenovo** | F12 | F1, F2 |
| **Asus** | F8 ou Échap | F2 |
| **Acer** | F12 | F2, Del |
| **Samsung** | F2 ou F12 | Échap |
| **Toshiba** | F12 | F2 |
| **MSI** | F11 | Del |
| **Gigabyte** | F12 | Del |
| **Sony** | F11 | Échap, Assist |

> 💡 **Message au démarrage** : Certains ordinateurs affichent brièvement "Press F12 for Boot Menu" ou similaire. Lisez attentivement !

#### Sélectionner la clé USB

1. Le **Boot Menu** s'affiche avec une liste de périphériques
2. Utilisez les **flèches du clavier** pour naviguer
3. Sélectionnez votre **clé USB** :
   - Elle peut apparaître comme "USB HDD", "USB Device", "USB Drive"
   - Ou avec la marque de votre clé (SanDisk, Kingston, etc.)
4. Appuyez sur **Entrée**

### Méthode 2 : Via le BIOS/UEFI (Alternative)

Si le Boot Menu ne fonctionne pas ou n'est pas disponible, utilisez cette méthode.

#### Accéder au BIOS/UEFI

1. **Redémarrez** l'ordinateur
2. **Appuyez rapidement** sur la touche BIOS dès le démarrage

**Touches BIOS courantes :**
- **F2** (le plus courant)
- **Del** ou **Suppr**
- **F1**, **F10**, **Échap**

> 💡 **Astuce** : La touche est souvent indiquée brièvement à l'écran au démarrage : "Press F2 to enter Setup" ou "DEL to enter BIOS".

#### Naviguer dans le BIOS/UEFI

> ⚠️ **Attention** : Le BIOS peut sembler intimidant. Ne modifiez que ce qui est nécessaire et notez vos changements.

**Interface BIOS traditionnelle (texte bleu) :**
- Utilisez les **flèches du clavier** pour naviguer
- **Entrée** pour sélectionner
- **Échap** pour revenir en arrière

**Interface UEFI moderne (graphique) :**
- Vous pouvez souvent utiliser la **souris**
- Interface plus intuitive avec icônes et couleurs

#### Modifier l'ordre de démarrage

1. **Trouvez la section Boot** (Démarrage)
   - Cherchez un onglet/menu nommé "Boot", "Boot Order", "Boot Priority", "Startup"

2. **Localisez votre clé USB**
   - Elle apparaît dans la liste des périphériques
   - Peut être nommée "USB HDD", "Removable Devices", ou par sa marque

3. **Changez l'ordre de démarrage**
   - **Méthode 1** : Utilisez les touches F5/F6 ou +/- pour déplacer l'USB en premier
   - **Méthode 2** : Avec la souris si UEFI graphique, glissez l'USB en première position
   - **Objectif** : Votre clé USB doit être **en première position**

4. **Sauvegardez et quittez**
   - Appuyez sur **F10** (généralement)
   - Ou cherchez "Save & Exit", "Save Changes and Exit"
   - Confirmez avec "Yes" ou "OK"

L'ordinateur redémarre et devrait démarrer sur la clé USB.

#### Désactiver le Secure Boot (si nécessaire)

Sur certains PC récents, le **Secure Boot** peut empêcher le démarrage de Linux Mint.

**Symptômes :**
- Message d'erreur au démarrage
- "Secure Boot Violation"
- L'ordinateur ne démarre pas sur la clé

**Solution :**
1. Dans le BIOS/UEFI, cherchez **"Secure Boot"**
   - Souvent dans la section "Boot" ou "Security"
2. **Désactivez** Secure Boot (Disabled)
3. Sauvegardez et redémarrez

> 💡 **Rassurez-vous** : Désactiver Secure Boot est sans danger et réversible. Vous pourrez le réactiver plus tard si nécessaire.

---

## Étape 2 : Le menu de démarrage de Linux Mint

Une fois que votre ordinateur démarre sur la clé USB, vous verrez le **menu de démarrage de Linux Mint**.

### L'écran d'accueil

L'écran affiche le logo Linux Mint et plusieurs options :

```
Linux Mint 22.1 Cinnamon 64-bit
┌─────────────────────────────────────┐
│ Start Linux Mint                    │
│ Start Linux Mint (compatibility)    │
│ OEM install (for manufacturers)     │
│ Check the integrity of the medium   │
│ Test memory Memtest86+ (BIOS)       │
│ Boot from local drive               │
└─────────────────────────────────────┘
```

### Options disponibles

#### 1. Start Linux Mint (Recommandé)

- **C'est l'option par défaut** et celle que vous utiliserez normalement
- Démarre Linux Mint en mode Live avec accélération graphique
- Sélectionnée automatiquement après quelques secondes

#### 2. Start Linux Mint (compatibility mode)

- Mode de compatibilité avec pilotes graphiques de base
- **Utilisez cette option si :**
  - L'écran reste noir avec l'option normale
  - Vous avez des problèmes d'affichage
  - Votre carte graphique est très ancienne ou problématique

#### 3. OEM install

- **Réservé aux fabricants** d'ordinateurs
- Ne l'utilisez pas, ce n'est pas pour un usage normal

#### 4. Check the integrity of the medium

- Vérifie que la clé USB a été correctement créée
- Utile si vous rencontrez des problèmes au démarrage
- Prend quelques minutes

#### 5. Test memory Memtest86+

- Teste la mémoire RAM de votre ordinateur
- Utile pour diagnostiquer des problèmes matériels
- Pas nécessaire pour un test normal

#### 6. Boot from local drive

- Démarre normalement sur votre disque dur (Windows, etc.)
- Équivaut à redémarrer sans la clé USB

### Sélection de l'option

- Utilisez les **flèches haut/bas** pour choisir
- Appuyez sur **Entrée** pour valider
- Si vous ne faites rien, l'option par défaut démarre après 10 secondes

### Chargement du système

1. Après avoir sélectionné "Start Linux Mint", l'écran affiche le logo Linux Mint avec des points animés
2. Le chargement prend **1 à 3 minutes** (variable selon votre clé USB et ordinateur)
3. Soyez patient, c'est normal que ça prenne un peu de temps depuis une clé USB

> 💡 **Première fois** : Le premier démarrage peut être plus long. Les suivants seront généralement plus rapides.

---

## Étape 3 : L'écran de bienvenue

Une fois Linux Mint chargé, vous arrivez sur l'**écran de bienvenue** du mode Live.

### Interface principale

Vous voyez :
- Un **bureau** avec un fond d'écran Linux Mint
- Une **barre des tâches** en bas (similaire à Windows)
- Une fenêtre de **bienvenue** au centre

### La fenêtre de bienvenue

Cette fenêtre vous propose plusieurs options :

#### Boutons principaux

1. **Install Linux Mint**
   - Lance l'installation sur votre disque dur
   - Ne cliquez pas encore si vous voulez d'abord tester !

2. **Documentation**
   - Accède à la documentation officielle
   - Guides et tutoriels

3. **Support**
   - Liens vers les forums et l'aide communautaire

#### Choix de la langue

- En haut de la fenêtre, sélectionnez **"Français"**
- L'interface passera en français
- Cliquez sur **"Appliquer"** pour confirmer

#### Paramètres de clavier

- Le système détecte généralement automatiquement votre clavier
- Pour le français, il devrait afficher **"Français"** ou **"French (azerty)"**
- Vous pouvez tester en tapant dans un éditeur de texte

> 💡 **Vérifier le clavier** : Ouvrez un éditeur de texte et tapez : `àéèùç` pour confirmer que l'AZERTY fonctionne.

### Fermer la fenêtre de bienvenue

Vous pouvez fermer cette fenêtre en cliquant sur le **X** en haut à droite. Elle ne se rouvrira pas pendant cette session Live.

---

## Étape 4 : Explorer Linux Mint en mode Live

Maintenant que vous êtes dans Linux Mint, explorez librement !

### Le bureau

#### Éléments principaux

Le bureau Linux Mint Cinnamon ressemble à Windows :

**Barre des tâches (en bas) :**
- **Menu** (icône Linux Mint) : Accès à toutes les applications
- **Applications favorites** : Firefox, Gestionnaire de fichiers, etc.
- **Zone de notification** : Volume, réseau, horloge
- **Bouton d'alimentation** : Pour éteindre ou redémarrer

**Bureau :**
- **Fond d'écran** : Image par défaut Linux Mint
- **Icônes** : Vous pouvez créer des raccourcis
- **Dossiers** : Clic droit → Nouveau dossier

### Le menu principal

Cliquez sur l'**icône Linux Mint** en bas à gauche.

#### Sections du menu

1. **Favoris** : Applications les plus utilisées
2. **Tous les programmes** : Liste complète
3. **Catégories** : Applications organisées par type
   - Internet
   - Bureautique
   - Son et vidéo
   - Graphisme
   - Outils système
   - Etc.

4. **Recherche** : Tapez le nom d'une application pour la trouver rapidement

### Applications essentielles à tester

#### Firefox (Navigateur Web)

1. Cliquez sur l'icône **Firefox** dans la barre des tâches
2. Testez la navigation Internet
3. Vérifiez que votre **WiFi** fonctionne
4. Connectez-vous à vos sites favoris

**Connexion WiFi :**
- Cliquez sur l'icône **réseau** dans la barre des tâches
- Sélectionnez votre réseau WiFi
- Entrez le mot de passe
- Patientez quelques secondes

#### Gestionnaire de fichiers (Nemo)

1. Cliquez sur l'icône **dossier** dans la barre des tâches
2. Explorez l'arborescence :
   - **Ordinateur** : Tous vos disques et partitions
   - **Bureau** : Le bureau actuel
   - **Téléchargements** : Dossier temporaire

3. **Accéder à vos fichiers Windows** :
   - Cliquez sur **Ordinateur** dans le menu latéral
   - Vos disques Windows apparaissent (ex: "Système d'exploitation", "Données")
   - Double-cliquez pour y accéder
   - Vous pouvez lire vos fichiers, les copier, mais évitez de les modifier

> 💡 **Sécurité** : En mode Live, vous pouvez accéder à vos fichiers Windows en lecture. Parfait pour récupérer des données en cas de problème !

#### LibreOffice (Suite bureautique)

1. **Menu** → **Bureautique** → **LibreOffice Writer** (équivalent Word)
2. Créez un document test
3. Testez la saisie au clavier
4. LibreOffice inclut aussi :
   - **Calc** : Tableur (équivalent Excel)
   - **Impress** : Présentations (équivalent PowerPoint)

#### Paramètres système

1. **Menu** → **Préférences** → **Paramètres système**
2. Explorez les différentes sections :
   - **Apparence** : Thèmes, icônes
   - **Affichage** : Résolution d'écran
   - **Son** : Volume, périphériques audio
   - **Réseau** : Connexions
   - **Matériel** : Imprimantes, périphériques

### Tester le matériel

#### Son

1. Cliquez sur l'**icône haut-parleur** dans la barre des tâches
2. Ajustez le volume
3. Testez en lisant une vidéo YouTube sur Firefox
4. **Vérifiez :**
   - Le son fonctionne-t-il ?
   - La qualité est-elle correcte ?
   - Les contrôles de volume fonctionnent-ils ?

#### Écran et résolution

1. **Clic droit sur le bureau** → **Paramètres d'affichage**
2. Vérifiez la résolution détectée
3. Testez différentes résolutions si nécessaire
4. **Vérifiez :**
   - La résolution native est-elle détectée ?
   - L'affichage est-il net et clair ?
   - Pas de scintillement ?

#### Clavier et souris

1. Ouvrez un éditeur de texte
2. Testez toutes les touches
3. **Vérifiez :**
   - Toutes les touches fonctionnent ?
   - Les accents (é, è, à, ù, ç) ?
   - La souris (clic gauche, droit, molette) ?
   - Le pavé tactile (si laptop) ?

#### WiFi et réseau

1. **Icône réseau** → Vérifiez la connexion
2. Testez la navigation Internet
3. **Vérifiez :**
   - Le WiFi se connecte-t-il facilement ?
   - Le signal est-il stable ?
   - La vitesse est-elle correcte ?

#### Bluetooth (si applicable)

1. **Paramètres système** → **Bluetooth**
2. Activez le Bluetooth
3. Essayez de détecter des appareils
4. **Vérifiez :**
   - Le Bluetooth est-il détecté ?
   - Peut-il scanner des appareils ?

#### Webcam (si applicable)

1. **Menu** → **Son et Vidéo** → **Cheese** (application webcam)
2. La webcam devrait s'activer automatiquement
3. **Vérifiez :**
   - L'image s'affiche-t-elle ?
   - La qualité est-elle correcte ?

#### Imprimante (optionnel)

1. **Paramètres système** → **Imprimantes**
2. Ajoutez votre imprimante
3. Linux détecte souvent les imprimantes automatiquement
4. Essayez d'imprimer une page de test

### Personnalisation (optionnel)

Profitez du mode Live pour tester les options de personnalisation :

#### Changer le fond d'écran

1. **Clic droit sur le bureau** → **Changer le fond d'écran**
2. Parcourez les fonds d'écran inclus
3. Sélectionnez celui qui vous plaît

#### Changer le thème

1. **Paramètres système** → **Thèmes**
2. Testez différents thèmes (sombre, clair)
3. Changez les icônes, la décoration des fenêtres

#### Ajouter des widgets (desklets)

1. **Clic droit sur le bureau** → **Ajouter des desklets**
2. Explorez les widgets disponibles (horloge, météo, etc.)
3. Glissez-les sur le bureau

---

## Étape 5 : Limitations du mode Live

Le mode Live est génial, mais il a quelques limitations importantes à connaître :

### Performances

⚠️ **Plus lent que l'installation normale**
- Le système tourne depuis une clé USB, pas un SSD/HDD
- Les performances sont réduites, surtout avec une clé USB 2.0
- Temps de chargement des applications plus long
- **Solution** : Une fois installé sur le disque dur, Linux Mint sera beaucoup plus rapide

### Mémoire limitée

⚠️ **Tout est stocké en RAM**
- Vos modifications ne sont pas sauvegardées après redémarrage
- Fichiers téléchargés, documents créés : tout disparaît
- La RAM s'épuise plus vite
- **Solution** : Ne gardez rien d'important, c'est juste pour tester

### Aucune persistance

⚠️ **Retour à zéro à chaque démarrage**
- Paramètres personnalisés : perdus
- Applications installées : perdues
- Comptes créés : perdus
- **Solution** : C'est voulu ! Le mode Live est conçu pour tester sans traces

### Fonctionnalités limitées

⚠️ **Certaines fonctions peuvent ne pas fonctionner parfaitement**
- Mises à jour système : non persistantes
- Certains pilotes propriétaires : non installables
- Hibernate/suspension : parfois problématique
- **Solution** : L'installation complète résoudra ces limitations

> 💡 **En résumé** : Le mode Live n'est qu'un aperçu. L'installation réelle sera plus rapide, plus stable et avec toutes les fonctionnalités.

---

## Étape 6 : Tests recommandés

Voici une checklist des éléments à vérifier avant d'installer :

### Checklist matériel

- [ ] **Écran** : Résolution correcte, affichage net
- [ ] **Son** : Haut-parleurs et microphone fonctionnent
- [ ] **Clavier** : Toutes les touches, accents français
- [ ] **Souris/Pavé tactile** : Clics, défilement, gestes
- [ ] **WiFi** : Détection, connexion, stabilité
- [ ] **Bluetooth** : Détection des appareils (si utilisé)
- [ ] **Webcam** : Image claire (si utilisée)
- [ ] **Ports USB** : Détection de clés USB/disques externes
- [ ] **Lecteur de cartes SD** : Lecture de cartes (si applicable)
- [ ] **Batterie** : Détection, pourcentage affiché (laptops)

### Checklist logiciel

- [ ] **Navigation Web** : Sites chargent correctement
- [ ] **Lecture vidéo** : YouTube, vidéos locales
- [ ] **Musique** : Lecteurs audio fonctionnent
- [ ] **Documents** : LibreOffice ouvre vos fichiers
- [ ] **Photos** : Visionneuse d'images fonctionne
- [ ] **Accès Windows** : Lecture de vos partitions Windows

### Checklist confort

- [ ] **Interface** : L'environnement vous plaît ?
- [ ] **Réactivité** : Le système répond-il bien (malgré la clé USB) ?
- [ ] **Ergonomie** : Vous retrouvez facilement vos repères ?
- [ ] **Intuitivité** : Le menu et les applications sont-ils clairs ?

---

## Étape 7 : Que faire après le test ?

Une fois vos tests terminés, vous avez plusieurs options :

### Option 1 : Installer Linux Mint

Si tout fonctionne et que Linux Mint vous plaît :

1. Double-cliquez sur l'icône **"Install Linux Mint"** sur le bureau
2. Suivez l'assistant d'installation
3. ➡️ **Voir le chapitre suivant** : [2.4 Installation en dual-boot avec Windows](04-installation-en-dual-boot-avec-windows.md)

### Option 2 : Continuer à explorer

Vous n'êtes pas encore décidé ?

- Continuez à explorer Linux Mint
- Testez d'autres applications
- Habituez-vous à l'interface
- Revenez plus tard pour installer

> 💡 Vous pouvez redémarrer en mode Live autant de fois que vous voulez.

### Option 3 : Retourner à Windows

Vous préférez ne pas installer maintenant ?

1. **Cliquez sur le bouton alimentation** (en bas à droite)
2. Choisissez **"Arrêter"** ou **"Redémarrer"**
3. **Retirez la clé USB** quand l'ordinateur s'éteint
4. L'ordinateur redémarrera normalement sur Windows

> 🔒 **Aucune modification** n'a été faite à votre système. Windows est intact.

### Option 4 : Tester une autre édition

Vous voulez tester MATE ou Xfce ?

1. Téléchargez l'ISO d'une autre édition
2. Créez une nouvelle clé USB bootable
3. Testez cette édition en mode Live
4. Comparez les performances et l'ergonomie

---

## Problèmes courants et solutions

### L'ordinateur ne démarre pas sur la clé USB

**Solutions :**
1. Vérifiez que la clé est bien insérée
2. Essayez un autre port USB
3. Recréez la clé USB bootable
4. Désactivez Secure Boot dans le BIOS
5. Changez le mode Legacy/UEFI dans le BIOS

### Écran noir au démarrage

**Solutions :**
1. Au menu de démarrage, choisissez **"Start Linux Mint (compatibility mode)"**
2. Dans le BIOS, désactivez "Fast Boot"
3. Ajoutez le paramètre `nomodeset` :
   - Au menu de démarrage, appuyez sur **E**
   - Trouvez la ligne contenant `quiet splash`
   - Ajoutez `nomodeset` à la fin
   - Appuyez sur **F10** pour démarrer

### Pas de WiFi / WiFi ne fonctionne pas

**Cause :** Certains adaptateurs WiFi nécessitent des pilotes propriétaires

**Solutions :**
1. Connectez-vous en Ethernet si possible (câble réseau)
2. **Menu** → **Administration** → **Gestionnaire de pilotes**
3. Laissez Linux détecter les pilotes manquants
4. Installez les pilotes WiFi recommandés
5. Redémarrez

> 💡 **Note** : En mode Live, les pilotes installés seront perdus au redémarrage. L'installation complète résoudra ce problème définitivement.

### Le système est très lent

**Cause normale :** Le mode Live tourne depuis une clé USB

**Améliorations :**
- Utilisez une clé USB 3.0 ou plus récente
- Utilisez un port USB 3.0 (souvent bleu)
- Fermez les applications inutilisées
- **Rassurez-vous** : L'installation sur disque dur sera bien plus rapide

### Clavier en QWERTY au lieu d'AZERTY

**Solution :**
1. Cliquez sur l'icône **drapeau** dans la barre des tâches
2. Sélectionnez **"Français"** ou **"French"**
3. Ou : **Paramètres système** → **Clavier** → **Agencements** → Ajouter "Français"

### Résolution d'écran incorrecte

**Solutions :**
1. **Clic droit sur le bureau** → **Paramètres d'affichage**
2. Sélectionnez la résolution correcte
3. Si votre résolution n'apparaît pas :
   - Installez les pilotes graphiques propriétaires
   - **Menu** → **Administration** → **Gestionnaire de pilotes**

### Pas de son

**Solutions :**
1. Vérifiez que le volume n'est pas à 0
2. Cliquez sur l'icône **haut-parleur** → **Paramètres du son**
3. Vérifiez que le bon périphérique de sortie est sélectionné
4. Testez avec des écouteurs/casque
5. Redémarrez en mode Live

---

## Conseils pour une bonne expérience

### Prendre son temps

- 📖 N'hésitez pas à passer **1 à 2 heures** à explorer
- 🔍 Testez plusieurs applications
- 🎨 Expérimentez avec la personnalisation
- 🧪 Essayez différentes choses sans crainte

### Noter ce qui ne fonctionne pas

Si quelque chose ne fonctionne pas :
- ✍️ **Notez-le** : Quel composant, quel message d'erreur
- 📸 Prenez une photo si nécessaire
- 🔎 Recherchez des solutions sur Internet
- 💬 Demandez de l'aide sur les forums

### Comparer avec Windows

- ⚖️ Testez vos cas d'usage habituels
- 📝 Vérifiez que vos logiciels essentiels ont des équivalents
- 🎮 Si vous jouez, vérifiez la compatibilité de vos jeux

### Utiliser Internet

- 🌐 Profitez du navigateur Firefox pour rechercher
- 📺 Regardez des tutoriels YouTube sur Linux Mint
- 📖 Consultez la documentation officielle
- 💬 Visitez les forums Linux Mint

---

## Questions fréquentes

### Puis-je installer des logiciels en mode Live ?

Techniquement oui, mais ils seront perdus au redémarrage. Le mode Live n'est pas conçu pour une utilisation quotidienne.

### Mes fichiers Windows sont-ils en sécurité ?

Oui, totalement. Le mode Live ne modifie rien sur vos disques. Vos fichiers Windows restent intacts.

### Puis-je utiliser Linux Mint uniquement en mode Live ?

C'est possible mais **non recommandé** car :
- Très lent comparé à une installation
- Aucune persistance des données
- Usure prématurée de la clé USB
- Expérience utilisateur dégradée

### Combien de temps puis-je rester en mode Live ?

Aussi longtemps que vous voulez ! Vous pouvez utiliser l'ordinateur normalement. Mais tout sera perdu à l'extinction.

### Puis-je sauvegarder mes modifications en mode Live ?

Non, sauf si vous copiez manuellement des fichiers vers :
- Un disque dur externe
- Une autre clé USB
- Un service cloud

Il existe des "Live USB persistants" (avancé) mais ce n'est pas l'objectif ici.

### Le mode Live use-t-il ma clé USB ?

Peu. Le mode Live lit principalement la clé, il n'écrit que très peu. Votre clé USB ne s'usera pas significativement.

### Puis-je accéder à Internet en mode Live ?

Oui, absolument ! Connectez-vous au WiFi ou branchez un câble Ethernet. La navigation est normale.

### Linux Mint collecte-t-il mes données en mode Live ?

Non. Linux Mint ne collecte aucune donnée personnelle, que ce soit en mode Live ou installé.

### Le mode Live peut-il endommager mon PC ?

Non, absolument pas. Le mode Live est 100% sûr pour votre matériel et vos données.

---

## Étape suivante

Vous avez testé Linux Mint et vous êtes prêt à l'installer ?

### Si vous voulez garder Windows

➡️ **[2.4 Installation en dual-boot avec Windows](./04-installation-en-dual-boot-avec-windows.md)**

Installez Linux Mint à côté de Windows et choisissez au démarrage quel système utiliser.

### Si vous voulez remplacer Windows

➡️ **[2.5 Installation complète (remplacement de l'OS)](./05-installation-complete.md)**

Remplacez complètement Windows par Linux Mint.

### Si vous voulez une installation avancée

➡️ **[2.6 Partitionnement manuel avancé](./06-partitionnement-manuel-avance.md)**

Contrôlez précisément comment les partitions sont créées.

---

## Ressources complémentaires

- 📖 [Guide de démarrage Linux Mint](https://linuxmint.com/documentation.php)
- 💬 [Forum Linux Mint en français](https://forums.linuxmint.com/viewforum.php?f=21)
- 🎥 [Chaîne YouTube Linux Mint](https://www.youtube.com/linuxmint)
- 🐛 [Signaler un bug](https://github.com/linuxmint)

---

**Vous avez maintenant exploré Linux Mint en mode Live ! Prêt pour l'installation ? 🚀**

⏭️ [Installation en dual-boot avec Windows](/02-preparation-et-installation/04-installation-en-dual-boot-avec-windows.md)
