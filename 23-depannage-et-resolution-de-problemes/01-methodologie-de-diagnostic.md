🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 23.1 Méthodologie de diagnostic

## Introduction

Lorsque vous rencontrez un problème sous Linux Mint, il est tentant de chercher immédiatement une solution sur Internet ou de réinstaller le système. Cependant, adopter une méthodologie de diagnostic structurée vous permettra de résoudre les problèmes plus efficacement et d'apprendre à mieux comprendre votre système.

Ce guide vous présente une approche étape par étape pour identifier et résoudre les problèmes, même si vous êtes débutant.

---

## Pourquoi une méthodologie est importante

Une approche méthodique vous permet de :

- **Gagner du temps** en évitant les solutions au hasard
- **Comprendre la cause** plutôt que de simplement masquer le symptôme
- **Éviter d'aggraver** la situation avec des modifications hasardeuses
- **Développer votre autonomie** face aux problèmes futurs
- **Documenter le problème** pour obtenir de l'aide efficacement si nécessaire

---

## Étape 1 : Identifier et décrire le problème

### Posez-vous les bonnes questions

Avant toute action, prenez le temps de bien définir le problème :

- **Quel est le symptôme exact ?**
  - Exemple : "L'ordinateur ne démarre pas" vs "L'écran reste noir après le logo Linux Mint"

- **Quand le problème est-il apparu ?**
  - Après une mise à jour ?
  - Après l'installation d'un nouveau logiciel ?
  - Après un redémarrage ?
  - Sans raison apparente ?

- **Le problème est-il constant ou intermittent ?**
  - Se produit-il à chaque fois ?
  - Seulement dans certaines conditions ?

- **Qu'avez-vous fait juste avant ?**
  - Installation de logiciels
  - Modifications de configuration
  - Mise à jour du système
  - Manipulation de fichiers système

### Notez les messages d'erreur

Si un message d'erreur s'affiche :

- **Notez-le exactement** (faites une capture d'écran ou recopiez-le mot pour mot)
- Ne vous contentez pas de "il y a une erreur"
- Les codes d'erreur et messages techniques sont précieux pour le diagnostic

---

## Étape 2 : Reproduire le problème

### Testez la reproductibilité

Essayez de reproduire le problème de manière contrôlée :

1. **Notez les étapes exactes** qui mènent au problème
2. **Testez plusieurs fois** pour confirmer que c'est reproductible
3. **Variez les conditions** :
   - Le problème survient-il avec un autre utilisateur ?
   - Est-il lié à un logiciel spécifique ?
   - Apparaît-il à un moment précis (au démarrage, après X minutes) ?

### Isolez les variables

Essayez de déterminer ce qui déclenche le problème :

- Si c'est lié à un logiciel, le problème persiste-t-il sans ce logiciel ?
- Si c'est matériel, le problème apparaît-il avec un autre périphérique ?
- Si c'est au démarrage, le problème existe-t-il en mode sans échec ?

---

## Étape 3 : Vérifier les bases (First Things First)

Avant d'aller plus loin, vérifiez toujours les points élémentaires :

### Vérifications matérielles

- **Câbles et connexions** : Tout est-il bien branché ?
- **Alimentation** : L'appareil est-il sous tension ?
- **Périphériques externes** : Débranchez-les temporairement (clé USB, disque externe, etc.)
- **Batterie** (pour portable) : Est-elle suffisamment chargée ?

### Vérifications logicielles

- **Redémarrage simple** : Avez-vous essayé de redémarrer l'ordinateur ?
  - Beaucoup de problèmes se résolvent ainsi
  - Cela libère la mémoire et recharge les services

- **Mises à jour** : Votre système est-il à jour ?
  - Menu → Administration → Gestionnaire de mises à jour

- **Espace disque** : Avez-vous suffisamment d'espace ?
  - Ouvrez le gestionnaire de fichiers
  - Regardez la barre en bas indiquant l'espace disponible
  - Au moins 10-15% d'espace libre est recommandé

---

## Étape 4 : Consulter les logs (journaux système)

Les logs sont vos meilleurs alliés pour comprendre ce qui se passe "sous le capot".

### Où trouver les informations ?

#### Le Moniteur système

Pour une vue d'ensemble rapide :

1. Menu → Administration → Moniteur système
2. Consultez les onglets :
   - **Processus** : Quel programme consomme des ressources ?
   - **Ressources** : CPU, mémoire, réseau
   - **Système de fichiers** : Espace disque

#### Les journaux système (pour utilisateurs intermédiaires)

Les logs système contiennent des informations détaillées :

**Méthode graphique** :

- Menu → Administration → Journaux système
- Consultez les différentes catégories
- Recherchez les lignes en rouge (erreurs) ou orange (avertissements)

**Méthode terminal** (si vous êtes à l'aise) :

```bash
# Voir les derniers messages système
journalctl -xe

# Voir les logs depuis le dernier démarrage
journalctl -b

# Voir les erreurs uniquement
journalctl -p err
```

### Que chercher dans les logs ?

- **Messages d'erreur** (error, failed, critical)
- **Avertissements** (warning) autour de l'heure du problème
- **Nom du service ou logiciel** concerné
- **Codes d'erreur** que vous pourrez rechercher en ligne

---

## Étape 5 : Rechercher des informations

### Utiliser les bons mots-clés

Lorsque vous recherchez en ligne :

**Mauvais exemple :** "Linux ne marche pas"

**Bon exemple :** "Linux Mint 21 écran noir après mise à jour pilote NVIDIA"

### Inclure dans votre recherche :

- Le nom exact de votre distribution : "Linux Mint 21 Cinnamon"
- Le message d'erreur exact (entre guillemets)
- Le composant concerné (nom du logiciel, matériel)
- L'action qui a précédé le problème

### Sources fiables à consulter

Par ordre de priorité :

1. **Documentation officielle Linux Mint**
   - https://linuxmint.com/documentation.php

2. **Forums Linux Mint**
   - Forum international : https://forums.linuxmint.com/
   - Forum francophone : https://forum-francophone-linuxmint.fr/

3. **Ask Ubuntu** (Ubuntu est la base de Linux Mint)
   - https://askubuntu.com/

4. **Wiki Arch Linux** (très technique mais complet)
   - https://wiki.archlinux.org/

5. **Forums français généralistes**
   - Ubuntu-fr.org
   - Debian-facile.org

### Attention aux fausses pistes

- Vérifiez la **date** des solutions (une solution de 2015 peut être obsolète)
- Vérifiez la **version** de Linux concernée
- Méfiez-vous des commandes que vous ne comprenez pas
- Ne copiez jamais aveuglément des commandes `sudo` sans comprendre

---

## Étape 6 : Tester les solutions une par une

### Approche méthodique

Lorsque vous avez identifié des solutions potentielles :

1. **Ne testez qu'une solution à la fois**
   - Si vous en essayez plusieurs, vous ne saurez pas laquelle a fonctionné
   - Ou pire, laquelle a aggravé le problème

2. **Documentez ce que vous faites**
   - Notez chaque modification
   - Cela vous permettra de revenir en arrière si nécessaire

3. **Testez après chaque modification**
   - Ne multipliez pas les changements avant de vérifier l'effet

4. **Faites des sauvegardes avant les modifications critiques**
   - Utilisez Timeshift avant toute modification système importante
   - Copiez les fichiers de configuration avant de les modifier

### Ordre de priorité des solutions

Commencez par les solutions :

1. **Les moins invasives** (redémarrage, déconnexion/reconnexion)
2. **Les plus fréquentes** pour ce type de problème
3. **Les réversibles** facilement
4. **Les plus radicales** en dernier recours (réinstallation, etc.)

---

## Étape 7 : Demander de l'aide efficacement

Si vous ne trouvez pas de solution, n'hésitez pas à demander de l'aide. Mais faites-le efficacement.

### Informations à fournir

Lorsque vous demandez de l'aide sur un forum :

#### 1. Description claire du problème

- Symptôme exact
- Quand il apparaît
- Ce que vous avez déjà essayé

#### 2. Informations système

Fournissez les informations de votre système avec la commande `inxi` :

```bash
inxi -Fxz
```

Cela affiche :
- Version de Linux Mint
- Environnement de bureau
- Kernel
- Matériel (processeur, carte graphique, etc.)

#### 3. Messages d'erreur complets

- Copiez-collez les messages d'erreur exacts
- Utilisez les balises "code" sur les forums
- Faites des captures d'écran si nécessaire

#### 4. Ce que vous avez déjà tenté

- Listez les solutions essayées
- Indiquez les résultats obtenus

### Exemple de bonne demande d'aide

```
Titre : Écran noir après mise à jour des pilotes NVIDIA sur Linux Mint 21.3

Bonjour,

Depuis la mise à jour de mes pilotes NVIDIA hier via le  
Gestionnaire de pilotes, mon écran reste noir après le logo  
de démarrage de Linux Mint.  

Configuration :
- Linux Mint 21.3 Cinnamon
- Carte graphique : NVIDIA GTX 1060
- Pilote installé : nvidia-driver-535

Symptômes :
- L'écran s'allume au démarrage
- Le logo Linux Mint apparaît
- Puis écran noir avec curseur clignotant
- Ctrl+Alt+F2 fonctionne (accès terminal)

Ce que j'ai déjà essayé :
1. Redémarrage : pas d'amélioration
2. Mode recovery : fonctionne normalement
3. Logs consultés : erreur "Failed to initialize NVIDIA driver"

Sortie de inxi -Fxz :
[coller ici la sortie de la commande]

Merci pour votre aide !
```

---

## Étape 8 : Documenter la solution

Une fois le problème résolu :

### Gardez une trace

1. **Notez ce qui a fonctionné**
   - La solution exacte
   - Les commandes utilisées
   - Les étapes suivies

2. **Comprenez pourquoi ça marche**
   - Ne vous contentez pas du "ça marche"
   - Cherchez à comprendre la cause du problème

3. **Créez votre propre documentation**
   - Un simple fichier texte avec vos problèmes/solutions
   - Cela vous servira pour des problèmes similaires futurs

### Partagez si possible

Si vous avez posté sur un forum :

- **Revenez poster la solution** qui a fonctionné
- Cela aidera d'autres personnes avec le même problème
- C'est une façon de remercier la communauté

---

## Outils de diagnostic essentiels

Voici quelques outils intégrés à Linux Mint qui vous aideront :

### Outils graphiques

| Outil | Accès | Utilité |
|-------|-------|---------|
| **Moniteur système** | Menu → Administration | Vue d'ensemble des ressources (CPU, RAM, processus) |
| **Journaux système** | Menu → Administration | Consultation des logs système |
| **Gestionnaire de pilotes** | Menu → Administration | Vérification et installation de pilotes |
| **Gestionnaire de mise à jour** | Menu → Administration | État des mises à jour système |
| **Informations système** | Menu → Administration | Détails sur votre matériel et système |

### Commandes terminal utiles (optionnel)

Pour ceux qui veulent aller plus loin :

```bash
# Informations système complètes
inxi -Fxz

# État des services système
systemctl status

# Espace disque
df -h

# Utilisation mémoire
free -h

# Processus actifs
top

# Tester la connexion réseau
ping -c 4 google.com

# Logs en temps réel
journalctl -f
```

---

## Cas particuliers fréquents

### "Mon ordinateur est lent"

Méthodologie :

1. Ouvrir le Moniteur système
2. Identifier ce qui consomme (CPU, RAM, disque)
3. Chercher les processus anormaux
4. Vérifier l'espace disque disponible
5. Vérifier si des mises à jour sont en cours

### "Un logiciel ne se lance pas"

Méthodologie :

1. Essayer de le lancer depuis le terminal pour voir les erreurs
2. Vérifier s'il est bien installé : `which nom-du-logiciel`
3. Consulter les logs : `journalctl -xe | grep nom-du-logiciel`
4. Réinstaller le logiciel si nécessaire

### "Pas de connexion Internet"

Méthodologie :

1. Vérifier le câble/WiFi activé
2. Tester : `ping 8.8.8.8` (test de connexion)
3. Tester : `ping google.com` (test DNS)
4. Redémarrer le routeur
5. Consulter les logs réseau

---

## Bonnes pratiques de prévention

Quelques conseils pour éviter les problèmes :

### Avant toute modification importante

1. **Créez un point de restauration avec Timeshift**
   - Menu → Administration → Timeshift
   - Permet de revenir en arrière en cas de problème

2. **Lisez la documentation**
   - Avant d'installer un logiciel complexe
   - Avant de modifier des fichiers système

3. **Testez en environnement sûr**
   - Utilisez une machine virtuelle pour les tests
   - Ne faites pas de modifications hasardeuses sur votre système principal

### Maintenance régulière

- **Mises à jour régulières** (mais lisez les notes de version)
- **Nettoyage périodique** (paquets inutilisés, cache)
- **Surveillance de l'espace disque**
- **Sauvegardes fréquentes** de vos données importantes

---

## Conclusion

Une bonne méthodologie de diagnostic repose sur :

1. **L'observation** : Comprendre exactement ce qui se passe
2. **La méthodologie** : Procéder par étapes logiques
3. **La documentation** : Rechercher et noter les informations
4. **La patience** : Ne pas précipiter les solutions
5. **L'apprentissage** : Comprendre pour progresser

Rappelez-vous : chaque problème résolu est une compétence gagnée. Avec le temps, vous développerez une intuition pour diagnostiquer et résoudre les problèmes de plus en plus rapidement.

La communauté Linux est là pour vous aider, n'hésitez pas à demander, mais faites-le de manière structurée en suivant cette méthodologie !

---

## Ressources complémentaires

- [Documentation Linux Mint - Troubleshooting](https://linuxmint.com/documentation.php)
- [Forum francophone Linux Mint](https://forum-francophone-linuxmint.fr/)
- [Guide Ubuntu francophone](https://doc.ubuntu-fr.org/)

---

⏭️ [Problèmes de démarrage et écran noir](/23-depannage-et-resolution-de-problemes/02-problemes-de-demarrage-et-ecran-noir.md)
