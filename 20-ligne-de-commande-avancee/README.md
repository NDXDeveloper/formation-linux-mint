🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Ligne de commande avancée

## Introduction

Bienvenue dans le chapitre **Ligne de commande avancée** ! Si vous avez déjà maîtrisé les bases du terminal Linux (navigation, manipulation de fichiers, commandes essentielles), il est maintenant temps de passer à la vitesse supérieure.

Ce chapitre vous transformera d'utilisateur du terminal en **véritable expert** capable d'automatiser des tâches, de manipuler des données complexes et de diagnostiquer les problèmes système de manière professionnelle.

### Pourquoi apprendre la ligne de commande avancée ?

Vous vous demandez peut-être : "Pourquoi aller plus loin ? Les commandes de base ne suffisent-elles pas ?"

Voici ce que vous gagnerez en maîtrisant ces compétences avancées :

🚀 **Automatisation**
- Fini les tâches répétitives ! Créez des scripts qui font le travail à votre place
- Planifiez des sauvegardes automatiques, des mises à jour, du nettoyage système
- Économisez des heures de travail manuel chaque semaine

⚡ **Productivité**
- Traitez des milliers de fichiers en quelques secondes
- Analysez des logs volumineux instantanément
- Extrayez et transformez des données en un clin d'œil

🔧 **Diagnostic et maintenance**
- Identifiez rapidement les problèmes réseau
- Surveillez vos ressources système
- Devenez autonome dans la résolution de problèmes

💪 **Puissance et contrôle**
- Réalisez des opérations impossibles via l'interface graphique
- Manipulez le texte de manière chirurgicale
- Maîtrisez totalement votre système Linux

🎯 **Compétences professionnelles**
- Ces compétences sont recherchées dans le monde professionnel
- Essentielles pour l'administration système et DevOps
- Valorisantes sur un CV

### Ce que vous allez apprendre

Ce chapitre est organisé en **6 sections progressives**, chacune vous apportant des compétences concrètes et immédiatement utilisables.

#### 1. Scripts bash pour automatisation

Apprenez à écrire vos propres programmes shell pour automatiser n'importe quelle tâche répétitive.

**Ce que vous saurez faire** :
- Créer des scripts pour sauvegarder automatiquement vos données
- Automatiser le nettoyage et la maintenance de votre système
- Créer des outils personnalisés adaptés à vos besoins
- Utiliser des variables, des boucles et des conditions
- Gérer les erreurs et créer des scripts robustes

**Exemple concret** : Un script qui sauvegarde vos documents, nettoie les fichiers temporaires, et vous envoie un rapport par notification - le tout automatiquement chaque jour.

#### 2. Cron et tâches planifiées

Découvrez comment programmer l'exécution automatique de vos scripts et commandes.

**Ce que vous saurez faire** :
- Planifier des sauvegardes quotidiennes automatiques
- Programmer des tâches de maintenance (nettoyage, mises à jour)
- Créer des rappels et notifications automatiques
- Exécuter des scripts à des moments précis ou à intervalles réguliers
- Gérer les tâches même quand votre ordinateur est éteint (avec anacron)

**Exemple concret** : Vos documents se sauvegardent automatiquement chaque nuit à 2h, votre système se nettoie tous les dimanches, et vous recevez un rappel tous les matins à 9h.

#### 3. Systemd timers - Alternative moderne à cron

Explorez le système de planification moderne de Linux, plus puissant et flexible que cron.

**Ce que vous saurez faire** :
- Créer des tâches planifiées avec systemd
- Bénéficier de logs détaillés et de meilleure gestion des erreurs
- Gérer les dépendances entre services
- Contrôler finement l'utilisation des ressources
- Surveiller l'état de vos tâches en temps réel

**Exemple concret** : Une tâche de synchronisation cloud qui ne s'exécute que si le réseau est disponible, avec des logs complets consultables via journalctl.

#### 4. Expressions régulières (regex)

Maîtrisez ce langage de recherche ultra-puissant pour trouver, valider et extraire du texte.

**Ce que vous saurez faire** :
- Chercher des motifs complexes dans des fichiers (emails, URLs, numéros)
- Valider des formats de données (téléphones, codes postaux, dates)
- Extraire des informations spécifiques de fichiers volumineux
- Filtrer et nettoyer des données
- Utiliser les regex avec grep, sed, awk et d'autres outils

**Exemple concret** : Extraire instantanément toutes les adresses email d'un fichier de 10 000 lignes, ou valider automatiquement la saisie d'utilisateurs.

#### 5. Sed et Awk - Traitement de texte professionnel

Découvrez deux outils légendaires pour manipuler et analyser du texte de manière surpuissante.

**Ce que vous saurez faire avec sed** :
- Remplacer du texte dans des milliers de fichiers instantanément
- Supprimer, insérer ou modifier des lignes selon des critères
- Nettoyer et reformater des fichiers de configuration
- Transformer des données d'un format à un autre

**Ce que vous saurez faire avec awk** :
- Extraire et analyser des colonnes de données (CSV, logs, etc.)
- Faire des calculs et générer des statistiques
- Créer des rapports formatés
- Filtrer et transformer des données tabulaires

**Exemple concret** : Analyser un fichier de log de 1 million de lignes pour extraire les erreurs, compter les occurrences par type, et générer un rapport - le tout en une seule commande.

#### 6. Commandes réseau avancées

Maîtrisez les outils pour diagnostiquer, surveiller et configurer votre réseau.

**Ce que vous saurez faire** :
- Diagnostiquer les problèmes de connexion Internet
- Voir quelles applications utilisent votre bande passante
- Identifier les ports ouverts et les connexions actives
- Configurer vos interfaces réseau
- Analyser le trafic réseau et détecter les anomalies
- Tester la connectivité et tracer les routes réseau

**Exemple concret** : Identifier rapidement pourquoi votre connexion Internet est lente, voir quel programme monopolise la bande passante, et résoudre le problème.

### Prérequis

Pour tirer le meilleur parti de ce chapitre, vous devriez :

- ✅ **Être à l'aise avec le terminal** - Savoir naviguer, créer/modifier des fichiers, exécuter des commandes
- ✅ **Connaître les commandes de base** - cd, ls, cp, mv, rm, cat, grep, etc.
- ✅ **Comprendre les permissions** - chmod, chown, sudo
- ✅ **Avoir installé un éditeur de texte** - nano, vim, ou autre

Si vous n'êtes pas encore tout à fait à l'aise avec ces bases, nous vous recommandons de consulter d'abord le **chapitre 7 - Le terminal et commandes de base**.

### Comment utiliser ce chapitre ?

#### Approche recommandée

**Pour les débutants complets en ligne de commande avancée** :
1. Suivez l'ordre des chapitres (1 → 6)
2. Pratiquez chaque concept sur de vrais fichiers
3. Créez vos propres scripts et commandes
4. N'hésitez pas à revenir en arrière si nécessaire

**Pour ceux qui ont déjà des bases** :
- Vous pouvez piocher les chapitres selon vos besoins
- Les chapitres 1-3 sont liés (automatisation et planification)
- Les chapitres 4-5 sont liés (traitement de texte)
- Le chapitre 6 est autonome (réseau)

#### Conseils d'apprentissage

🎯 **Pratiquez régulièrement**
- La ligne de commande s'apprend par la pratique
- Essayez les commandes sur vos propres fichiers
- Créez des exemples pertinents pour vous

📝 **Créez votre bibliothèque de scripts**
- Sauvegardez vos commandes utiles
- Documentez vos scripts
- Partagez avec la communauté

🧪 **Testez dans un environnement sûr**
- Utilisez des copies de fichiers importants
- Testez les commandes destructrices avec précaution
- Créez un dossier ~/test pour vos expérimentations

🔍 **Consultez l'aide régulièrement**
- `man commande` est votre meilleur ami
- `commande --help` pour un résumé rapide
- Les forums et Stack Overflow pour les cas complexes

💡 **Commencez simple**
- Ne cherchez pas à tout maîtriser d'un coup
- Construisez progressivement vos compétences
- Chaque expert a commencé par un simple `echo "Hello World"`

### Structure de chaque section

Chaque sous-chapitre suit une structure pédagogique cohérente :

1. **Introduction** - Pourquoi cette compétence est importante
2. **Concepts de base** - Les fondamentaux expliqués simplement
3. **Syntaxe et commandes** - Comment utiliser les outils
4. **Exemples pratiques** - Des cas d'usage réels et concrets
5. **Cas avancés** - Pour aller plus loin
6. **Bonnes pratiques** - Conseils d'experts
7. **Pièges à éviter** - Les erreurs courantes
8. **Aide-mémoire** - Résumé des commandes essentielles

### Ce chapitre transformera votre utilisation de Linux

À la fin de ce chapitre, vous ne serez plus un simple utilisateur de Linux, mais un **power user** capable de :

- ✨ **Automatiser** vos tâches quotidiennes avec des scripts intelligents
- ⏰ **Planifier** l'exécution de vos programmes comme un professionnel
- 🔍 **Chercher** et **manipuler** du texte avec une précision chirurgicale
- 📊 **Analyser** des données et créer des rapports automatiquement
- 🌐 **Diagnostiquer** et **résoudre** les problèmes réseau
- 🚀 **Gagner** des heures de productivité chaque semaine

### La philosophie Unix : "Do One Thing and Do It Well"

Les outils que vous allez apprendre dans ce chapitre incarnent la philosophie Unix :

- Chaque outil fait **une chose** et la fait **très bien**
- Les outils peuvent être **combinés** pour créer des solutions puissantes
- Le texte est le **langage universel** qui relie tous les outils

C'est cette philosophie qui rend la ligne de commande Linux si puissante. En maîtrisant ces outils, vous pourrez :

```bash
# Exemple de la puissance de la combinaison d'outils :
# Analyser un log de 1 million de lignes, extraire les erreurs,
# les compter par type, et afficher les 10 plus fréquentes
cat gigantesque.log | grep ERROR | awk '{print $4}' | sort | uniq -c | sort -rn | head -10
```

En une seule ligne, vous réalisez ce qui nécessiterait un programme complet dans d'autres environnements !

### Ressources complémentaires

Pour approfondir vos connaissances au-delà de ce chapitre :

📚 **Documentation système**
```bash
man bash          # Manuel de bash
info coreutils    # Informations sur les utilitaires GNU
help              # Aide intégrée de bash
```

🌐 **Sites web recommandés**
- [The Linux Command Line](http://linuxcommand.org/) - Excellent site pour débutants
- [ExplainShell](https://explainshell.com/) - Explique les commandes complexes
- [Regex101](https://regex101.com/) - Tester vos expressions régulières
- [ShellCheck](https://www.shellcheck.net/) - Vérifier vos scripts bash

📖 **Livres de référence**
- "The Linux Command Line" par William Shotts (gratuit en ligne)
- "Classic Shell Scripting" par Arnold Robbins
- "sed & awk" par Dale Dougherty

🎓 **Pratique interactive**
- [OverTheWire - Bandit](https://overthewire.org/wargames/bandit/) - Jeu pour apprendre la ligne de commande
- [Exercism - Bash Track](https://exercism.org/tracks/bash) - Exercices progressifs
- [Cmdchallenge](https://cmdchallenge.com/) - Défis en ligne de commande

### Un dernier mot avant de commencer

La ligne de commande avancée peut sembler intimidante au début. Vous verrez des commandes longues et complexes, des symboles étranges, et vous vous demanderez peut-être si vous arriverez un jour à maîtriser tout cela.

**Rassurez-vous** :

- Chaque expert que vous admirez a commencé exactement où vous êtes maintenant
- Personne ne maîtrise tout - même les experts consultent régulièrement la documentation
- L'important n'est pas de tout savoir, mais de savoir **où trouver l'information**
- Chaque petite compétence que vous acquerrez sera **immédiatement utile**
- La pratique régulière est plus importante que la perfection

### La courbe d'apprentissage

Voici à quoi ressemble généralement la progression :

**Semaine 1-2 : Les bases**
- Vous comprenez la syntaxe
- Vous copiez et modifiez des exemples
- C'est parfois frustrant mais excitant

**Semaine 3-4 : La pratique**
- Vous commencez à écrire vos propres commandes
- Vous combinez des outils simples
- Vous voyez les premiers gains de productivité

**Mois 2-3 : La confiance**
- Vous créez des scripts utiles
- Vous automatisez des tâches quotidiennes
- Vous vous demandez comment vous avez fait sans

**Mois 6+ : La maîtrise**
- La ligne de commande devient naturelle
- Vous résolvez des problèmes complexes facilement
- Vous créez vos propres outils personnalisés

### Engagement envers vous-même

Avant de commencer ce voyage, prenez un engagement simple :

- ✅ **Je vais pratiquer** régulièrement, même si ce n'est que 15 minutes par jour
- ✅ **Je vais faire des erreurs** et c'est parfaitement normal - c'est comme ça qu'on apprend
- ✅ **Je vais persévérer** quand ça devient difficile
- ✅ **Je vais créer** des choses utiles pour moi avec ces nouvelles compétences
- ✅ **Je vais partager** mes découvertes avec la communauté

### Prêt à commencer ?

Vous êtes maintenant prêt à plonger dans le monde fascinant de la ligne de commande avancée. Chaque section de ce chapitre vous rapprochera de la maîtrise de Linux et vous donnera des super-pouvoirs pour :

- Automatiser l'ennuyeux
- Analyser l'incompréhensible
- Diagnostiquer l'invisible
- Optimiser l'inefficace
- Maîtriser le complexe

Le voyage commence maintenant. Dans quelques semaines, vous regarderez en arrière et serez impressionné par tout ce que vous aurez appris.

**Bienvenue dans le monde de la ligne de commande avancée !** 🚀

---

## Table des matières détaillée

1. **[Scripts bash pour automatisation](./01-scripts-bash-pour-automatisation.md)**
   - Créez vos propres programmes pour automatiser vos tâches

2. **[Cron et tâches planifiées](./02-cron-et-taches-planifiees.md)**
   - Planifiez l'exécution automatique de vos scripts

3. **[Systemd timers](./03-systemd-timers.md)**
   - Alternative moderne et puissante à cron

4. **[Expressions régulières (regex)](./04-expressions-regulieres.md)**
   - Maîtrisez la recherche et manipulation de motifs textuels

5. **[Sed et Awk pour traitement de texte](./05-sed-et-awk-pour-traitement-de-texte.md)**
   - Outils légendaires de manipulation de texte

6. **[Commandes réseau avancées](./06-commandes-reseau-avancees.md)**
   - Diagnostiquez et configurez votre réseau comme un pro

---

**Note finale** : Ce chapitre représente des décennies de sagesse Unix/Linux condensées en formats accessibles. Prenez votre temps, pratiquez régulièrement, et surtout, amusez-vous ! La ligne de commande est un terrain de jeu infini pour les curieux. 🎯

*Bon apprentissage et bienvenue dans le club des power users Linux !* 💪

⏭️ [Scripts bash pour automatisation](/20-ligne-de-commande-avancee/01-scripts-bash-pour-automatisation.md)
