🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 12.1 Le gestionnaire de pilotes

## Introduction

Le **Gestionnaire de pilotes** (Driver Manager) est l'un des outils les plus utiles de Linux Mint. Il vous permet d'installer facilement les pilotes nécessaires pour que votre matériel fonctionne de manière optimale, sans avoir à saisir des commandes complexes dans le terminal.

## Qu'est-ce qu'un pilote ?

### Définition simple

Un **pilote** (ou driver en anglais) est un petit programme qui permet à votre système d'exploitation de communiquer correctement avec un composant matériel de votre ordinateur.

Pensez au pilote comme à un **traducteur** : votre système Linux parle une langue, votre carte graphique ou votre carte WiFi en parle une autre. Le pilote fait office d'interprète entre les deux.

### Exemples concrets

- **Carte graphique** : Sans le bon pilote, vous ne pourrez peut-être pas profiter de l'accélération 3D, jouer à des jeux ou utiliser plusieurs écrans
- **Carte WiFi** : Un pilote manquant peut empêcher votre ordinateur de détecter les réseaux sans fil
- **Imprimante** : Le pilote permet à Linux de savoir comment envoyer correctement des documents à imprimer

## Pilotes libres vs pilotes propriétaires

Linux Mint fait une distinction importante entre deux types de pilotes :

### Pilotes libres (open source)

- **Avantages** :
  - Installés automatiquement avec le système
  - Maintenus par la communauté Linux
  - Intégrés au noyau Linux
  - Respectent la philosophie du logiciel libre

- **Inconvénients** :
  - Parfois moins performants que les pilotes propriétaires
  - Peuvent manquer de certaines fonctionnalités avancées

### Pilotes propriétaires

- **Avantages** :
  - Développés directement par les fabricants (NVIDIA, AMD, etc.)
  - Généralement plus performants
  - Accès à toutes les fonctionnalités du matériel
  - Essentiels pour le gaming et les tâches graphiques intensives

- **Inconvénients** :
  - Code source fermé
  - Dépendance vis-à-vis du fabricant pour les mises à jour
  - Peuvent parfois poser des problèmes de compatibilité lors des mises à jour système

### Recommandation

Pour la **plupart des utilisateurs**, notamment pour les cartes graphiques NVIDIA et certaines cartes WiFi, il est recommandé d'utiliser les **pilotes propriétaires** pour bénéficier des meilleures performances.

## Accéder au Gestionnaire de pilotes

Il existe plusieurs façons d'ouvrir le Gestionnaire de pilotes :

### Méthode 1 : Via le Menu

1. Cliquez sur le **Menu** de Linux Mint (icône en bas à gauche)
2. Tapez "**pilotes**" ou "**driver**" dans la barre de recherche
3. Cliquez sur "**Gestionnaire de pilotes**"

### Méthode 2 : Via les Paramètres système

1. Ouvrez le **Menu**
2. Allez dans "**Préférences**" puis "**Gestionnaire de pilotes**"

### Méthode 3 : Via le Terminal

Si vous préférez, vous pouvez également lancer le gestionnaire via le terminal :

```bash
driver-manager
```

> **Note** : Au premier lancement, le système vous demandera votre mot de passe administrateur, car l'installation de pilotes nécessite des privilèges élevés.

## Utiliser le Gestionnaire de pilotes

### Première ouverture

Lors de la première ouverture, le Gestionnaire de pilotes va :

1. **Analyser votre matériel** : Il détecte automatiquement les composants de votre ordinateur
2. **Rechercher les pilotes disponibles** : Il vérifie quels pilotes propriétaires sont disponibles pour votre système
3. **Afficher les résultats** : Une liste des pilotes recommandés s'affiche

Cette analyse peut prendre quelques secondes à une minute.

### Interface du Gestionnaire

L'interface est simple et intuitive :

- **Colonne de gauche** : Liste des composants matériels détectés
- **Partie centrale** : Affiche les pilotes disponibles pour le composant sélectionné
- **Indication visuelle** :
  - Une **puce verte** indique le pilote actuellement utilisé
  - Le pilote **recommandé** est clairement marqué

### Comprendre les informations affichées

Pour chaque pilote, vous verrez :

- **Le nom du pilote** : Par exemple "nvidia-driver-535" ou "bcmwl-kernel-source"
- **Le type** : Propriétaire ou libre
- **La version** : Numéro de version du pilote
- **Le statut** : "En cours d'utilisation", "Recommandé" ou "Disponible"
- **Une brève description** : Explique à quoi sert le pilote

## Installer un pilote

### Procédure standard

1. **Sélectionnez le composant** dans la liste de gauche (par exemple, votre carte graphique NVIDIA)
2. **Choisissez le pilote recommandé** (généralement marqué d'une étiquette "Recommandé")
3. Cliquez sur le pilote souhaité pour le sélectionner
4. Cliquez sur le bouton "**Appliquer les changements**" en bas de la fenêtre
5. Entrez votre **mot de passe** si demandé
6. **Patientez** pendant le téléchargement et l'installation (cela peut prendre plusieurs minutes)

### Après l'installation

Une fois l'installation terminée :

1. Le système vous demandera généralement de **redémarrer** votre ordinateur
2. **Redémarrez impérativement** : Les pilotes graphiques ne sont actifs qu'après un redémarrage
3. Après le redémarrage, vérifiez que tout fonctionne correctement

## Cas d'usage courants

### Carte graphique NVIDIA

**Symptômes nécessitant un pilote** :
- Performances graphiques médiocres
- Impossibilité de jouer à des jeux
- Pas de détection de plusieurs écrans
- Ventilateur de la carte qui tourne au maximum

**Solution** :
1. Ouvrez le Gestionnaire de pilotes
2. Sélectionnez votre carte NVIDIA dans la liste
3. Installez le pilote **nvidia-driver** recommandé (généralement la version la plus récente)
4. Redémarrez

### Carte WiFi Broadcom

**Symptômes** :
- Aucun réseau WiFi détecté
- L'icône WiFi est absente ou grisée
- Impossibilité de se connecter au WiFi

**Solution** :
1. Utilisez une connexion Ethernet temporairement (ou partagez la connexion de votre smartphone)
2. Ouvrez le Gestionnaire de pilotes
3. Installez le pilote **bcmwl-kernel-source** si disponible
4. Redémarrez

### Carte graphique AMD/ATI

Pour les cartes AMD récentes, les pilotes libres (AMDGPU) fonctionnent généralement très bien. Cependant, pour des performances maximales en gaming :

1. Vérifiez si un pilote propriétaire AMD est disponible
2. Comparez les performances avant/après installation
3. Les pilotes libres peuvent suffire pour un usage bureautique

## Désinstaller ou changer de pilote

### Pourquoi changer de pilote ?

Vous pourriez vouloir revenir au pilote libre si :
- Le pilote propriétaire cause des problèmes (écran noir, bugs graphiques)
- Vous n'avez pas besoin de performances 3D maximales
- Une mise à jour système a créé une incompatibilité

### Procédure

1. Ouvrez le **Gestionnaire de pilotes**
2. Sélectionnez le composant concerné
3. Choisissez le pilote **libre** (souvent appelé "nouveau" pour NVIDIA, ou "X.Org X server" pour d'autres)
4. Cliquez sur "**Appliquer les changements**"
5. **Redémarrez** l'ordinateur

> **Important** : Vous pouvez toujours revenir en arrière en suivant la même procédure et en réinstallant le pilote propriétaire.

## Conseils et bonnes pratiques

### ✅ À faire

- **Toujours redémarrer** après l'installation d'un pilote graphique
- **Installer les pilotes recommandés** en premier lieu
- **Créer un point de restauration Timeshift** avant d'installer des pilotes propriétaires
- **Garder vos pilotes à jour** en vérifiant régulièrement le Gestionnaire
- **Utiliser une connexion stable** lors du téléchargement de pilotes

### ❌ À éviter

- Ne pas installer plusieurs pilotes pour le même composant simultanément
- Ne pas télécharger les pilotes depuis des sites tiers (utilisez uniquement le Gestionnaire)
- Ne pas paniquer si l'écran devient noir pendant l'installation
- Ne pas interrompre l'installation en cours

### En cas de problème après installation

Si après l'installation d'un pilote, vous rencontrez des problèmes (écran noir, résolution incorrecte, etc.) :

1. **Au démarrage**, appuyez sur **Maj** ou **Échap** pour accéder au menu GRUB
2. Sélectionnez "**Options avancées**"
3. Choisissez un **noyau précédent** (kernel)
4. Une fois démarré en mode dégradé, ouvrez le Gestionnaire de pilotes
5. Revenez au pilote libre
6. Redémarrez normalement

## Vérifier le pilote actif

### Méthode graphique

1. Ouvrez le **Gestionnaire de pilotes**
2. Le pilote actuellement utilisé est marqué d'une **puce verte**

### Méthode en ligne de commande

Pour les cartes NVIDIA, vous pouvez vérifier avec :

```bash
nvidia-smi
```

Cette commande affiche des informations détaillées sur votre carte NVIDIA et le pilote utilisé.

Pour une vue d'ensemble du matériel :

```bash
inxi -G
```

Cette commande affiche des informations sur votre configuration graphique.

## Questions fréquentes

### Le Gestionnaire de pilotes est vide, est-ce normal ?

**Oui**, c'est tout à fait normal si :
- Votre matériel fonctionne parfaitement avec les pilotes libres
- Vous n'avez pas de composants nécessitant des pilotes propriétaires
- Votre ordinateur est récent et bien supporté par Linux

Cela signifie simplement que vous n'avez pas besoin d'installer de pilotes supplémentaires.

### Dois-je installer tous les pilotes proposés ?

**Non**, installez uniquement les pilotes pour le matériel que vous utilisez et qui présente des problèmes ou nécessite de meilleures performances.

### Les mises à jour de pilotes sont-elles automatiques ?

Les pilotes installés via le Gestionnaire sont mis à jour automatiquement avec les mises à jour système de Linux Mint. Vous n'avez généralement rien à faire manuellement.

### Puis-je utiliser Linux sans pilotes propriétaires ?

**Absolument**. Les pilotes libres permettent une utilisation normale de l'ordinateur pour la bureautique, la navigation web, et le multimédia. Les pilotes propriétaires ne sont vraiment nécessaires que pour :
- Le gaming avec des jeux 3D exigeants
- Le montage vidéo professionnel
- L'apprentissage automatique (IA) avec GPU
- Certaines tâches graphiques spécifiques

## Conclusion

Le Gestionnaire de pilotes de Linux Mint est un outil puissant qui rend l'installation de pilotes aussi simple qu'un clic. Il élimine la complexité traditionnelle de la gestion des pilotes sous Linux et permet même aux débutants de profiter pleinement de leur matériel.

**Points clés à retenir** :
- Le Gestionnaire détecte automatiquement votre matériel
- Suivez toujours les recommandations du système
- Redémarrez après l'installation de pilotes graphiques
- Vous pouvez toujours revenir au pilote libre en cas de problème
- Un Gestionnaire vide n'est pas un problème : cela signifie que tout fonctionne déjà bien !

Dans le prochain chapitre, nous aborderons en détail les **pilotes propriétaires spécifiques** (NVIDIA, AMD, WiFi) et leurs particularités.

⏭️ [Pilotes propriétaires (NVIDIA, AMD, WiFi)](/12-materiel-et-pilotes/02-pilotes-proprietaires.md)
