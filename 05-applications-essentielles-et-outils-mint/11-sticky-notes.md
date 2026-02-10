🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.11 Sticky Notes (Pense-bêtes)

## Introduction

**Sticky Notes** (aussi appelé **Sticky** ou **Notes adhésives**) est une application simple et pratique pour créer des pense-bêtes virtuels sur votre bureau Linux Mint. C'est l'équivalent numérique des Post-it que vous collez sur votre écran ou votre bureau physique.

## Qu'est-ce que Sticky Notes ?

### Présentation

Sticky Notes vous permet de :
- **Créer des notes** rapides directement sur votre bureau
- **Organiser vos idées** : Listes de tâches, rappels, brouillons
- **Garder visible** : Les notes restent au premier plan
- **Synchroniser** : Notes sauvegardées automatiquement

**Cas d'usage** :
- Liste de courses
- Tâches à faire aujourd'hui
- Numéro de téléphone temporaire
- Idée à ne pas oublier
- Code ou commande à copier-coller
- Rappel d'un rendez-vous

### Avantages des pense-bêtes numériques

**Par rapport aux Post-it physiques** :

**Avantages** :
- Ne se décollent pas
- Ne jaunissent pas
- Illimités (pas besoin d'en racheter)
- Sauvegardés automatiquement
- Modifiables facilement
- Synchronisables entre appareils (selon l'outil)

**Inconvénients** :
- Nécessitent l'ordinateur allumé
- Moins "physiques" (certains préfèrent le papier)

## Installation

### Sur Linux Mint

**Sticky Notes est préinstallé** sur la plupart des versions de Linux Mint Cinnamon.

**Vérifier la présence** :
1. Menu principal → **Accessoires** → **Sticky Notes**
2. Ou tapez "Sticky" dans la recherche

**Si absent, installer** :
```bash
sudo apt update  
sudo apt install sticky  
```

**Note** : Il existe plusieurs applications de notes adhésives. Nous parlons ici de "Sticky" développé pour Linux Mint.

### Autres distributions

**Ubuntu et dérivés** :
```bash
sudo apt install sticky
```

**Alternative GNOME (différente)** :
```bash
sudo apt install gnote
```

**Flatpak** (universel) :
Sticky classique n'est pas sur Flatpak, mais des alternatives existent.

## Premier lancement

### Ouvrir Sticky Notes

**Depuis le menu** :
1. Menu principal → **Accessoires** → **Sticky Notes**
2. Ou tapez "Sticky" dans la recherche du menu
3. L'application se lance

**Au premier lancement** :
- Une petite note jaune apparaît sur votre bureau
- Texte d'exemple par défaut
- Icône dans la zone de notification (barre des tâches)

### Interface de l'application

**La note elle-même** :
- Petite fenêtre rectangulaire
- Fond coloré (jaune par défaut)
- Zone de texte éditable
- Barre de titre minimaliste en haut

**Barre de titre** :
- Bouton de menu (trois points ou engrenage)
- Bouton fermer (×)
- Bouton masquer (—)

**Icône de notification** :
- Dans la barre des tâches (zone de notification)
- Clic pour afficher/masquer les notes
- Clic droit pour options

## Créer des notes

### Créer une nouvelle note

**Méthode 1 - Menu de la note** :
1. Clic sur le menu d'une note existante (trois points)
2. **Nouvelle note** ou **New Note**
3. Une nouvelle note apparaît

**Méthode 2 - Icône de notification** :
1. Clic droit sur l'icône Sticky dans la barre des tâches
2. **Nouvelle note**
3. Note créée

**Méthode 3 - Raccourci clavier** (si configuré) :
- Varie selon la configuration
- Généralement pas de raccourci par défaut

**Résultat** :
- Nouvelle note vierge ou avec texte par défaut
- Positionnée légèrement décalée de la précédente

### Écrire dans une note

**Simple comme du texte** :

1. Cliquez dans la zone de texte de la note
2. Tapez votre contenu
3. Exemple :
```
Liste courses :
- Pain
- Lait
- Œufs
- Fromage
```

**Édition** :
- Cliquez pour positionner le curseur
- Sélectionnez du texte (glisser ou Maj + Flèches)
- Copier : `Ctrl + C`
- Coller : `Ctrl + V`
- Couper : `Ctrl + X`
- Tout sélectionner : `Ctrl + A`

**Sauvegarde automatique** :
- Pas besoin de "Enregistrer"
- Tout est sauvegardé automatiquement en temps réel

## Gérer les notes

### Déplacer une note

**Positionner sur le bureau** :

1. Cliquez sur la barre de titre de la note
2. Maintenez le bouton enfoncé
3. Glissez la note où vous voulez
4. Relâchez

**Conseil** :
- Placez les notes importantes dans des coins visibles
- Groupez les notes par thème (travail, perso, courses)

### Redimensionner une note

**Agrandir ou réduire** :

1. Placez le curseur sur un bord ou un coin de la note
2. Le curseur change (flèche double)
3. Cliquez et glissez pour redimensionner
4. Relâchez

**Utilité** :
- Note avec beaucoup de texte → Agrandissez
- Note courte (téléphone) → Petite taille
- Adaptation selon le contenu

### Masquer une note

**Temporairement cacher** :

**Méthode 1** :
- Cliquez sur le bouton **—** (réduire) dans la barre de titre
- La note disparaît mais reste en mémoire

**Méthode 2** :
- Clic sur le **×** (fermer)
- Selon les paramètres, peut masquer ou supprimer

**Afficher à nouveau** :
1. Clic sur l'icône Sticky dans la barre des tâches
2. Les notes masquées réapparaissent

**Ou** :
- Clic droit sur l'icône → Liste des notes → Sélectionnez celle à afficher

### Supprimer une note

**Définitivement effacer** :

1. Menu de la note (trois points)
2. **Supprimer** ou **Delete Note**
3. Confirmez (selon configuration)

**Attention** : La note et son contenu sont perdus !

**Conseil** : Copiez le contenu important avant de supprimer.

### Organiser plusieurs notes

**Si vous avez beaucoup de notes** :

**Par couleur** :
- Couleur jaune : Tâches du jour
- Couleur bleue : Informations importantes
- Couleur verte : Idées
- Couleur rouge : Urgent

**Par position** :
- Coin supérieur gauche : Urgent
- Coin supérieur droit : À faire cette semaine
- Coin inférieur : Références (numéros, codes)

**Par taille** :
- Grandes notes : Listes détaillées
- Petites notes : Rappels simples

## Personnalisation

### Changer la couleur d'une note

**Identifier visuellement** :

1. Menu de la note (trois points)
2. **Propriétés** ou **Préférences**
3. Sélectionnez une couleur
4. Appliquez

**Couleurs disponibles** (selon la version) :
- Jaune (classique)
- Bleu
- Vert
- Rose
- Orange
- Violet
- Blanc

**Utilité** :
- Catégoriser par couleur
- Repérage visuel rapide
- Esthétique

### Changer la police

**Modifier l'apparence du texte** :

1. **Propriétés** de la note
2. **Police** ou **Font**
3. Choisissez :
   - Type de police (Serif, Sans, Monospace)
   - Taille (petit, moyen, grand)
4. Appliquez

**Exemple** :
- Police large pour visibilité à distance
- Police monospace pour code ou données tabulaires

### Toujours au premier plan

**Note toujours visible** :

1. Menu de la note
2. **Toujours au-dessus** ou **Always on Top**
3. Cochez

**Résultat** :
- La note reste visible même avec d'autres fenêtres ouvertes
- Utile pour rappels importants
- Exemple : Liste de tâches à voir en permanence

**Désactiver** :
- Décochez l'option pour comportement normal

## Paramètres globaux

### Accéder aux paramètres

**Configuration générale** :

1. Clic droit sur l'icône Sticky (barre des tâches)
2. **Préférences** ou **Settings**
3. Ou menu d'une note → **Préférences**

### Options disponibles

**Apparence par défaut** :
- Couleur des nouvelles notes
- Police par défaut
- Taille par défaut

**Comportement** :
- **Démarrer au lancement** : Sticky démarre automatiquement avec Linux Mint
- **Masquer au démarrage** : Les notes sont cachées initialement
- **Confirmer suppression** : Demande confirmation avant effacement

**Position** :
- **Mémoriser les positions** : Les notes réapparaissent où vous les avez laissées
- **Centrer nouvelles notes** : Nouvelles notes au centre ou décalées

**Icône de notification** :
- Afficher/masquer dans la barre des tâches

### Sauvegarde et données

**Où sont stockées les notes ?** :

Les notes Sticky sont généralement sauvegardées dans :
```
~/.local/share/sticky/
```
ou
```
~/.config/sticky/
```

**Sauvegarder manuellement** :
- Copiez ce dossier pour backup
- Restaurez-le après réinstallation

**Format** :
- Généralement texte brut ou XML
- Facilement lisible/transférable

## Astuces et utilisation pratique

### Liste de tâches quotidiennes

**Organisation du travail** :

```
TODO - Lundi 15/04
☐ Répondre emails clients
☐ Finir rapport trimestriel
☐ Réunion équipe 14h
☐ Appeler Jean (01 23 45 67 89)
☐ Préparer présentation mardi
```

**Cochez avec caractères** :
- `☐` : À faire (Copiez ce caractère)
- `☑` : Fait
- Ou utilisez `[ ]` et `[x]`

### Notes de code rapide

**Commandes fréquentes** :

```
Commandes utiles :

Mise à jour système :  
sudo apt update && sudo apt upgrade  

Espace disque :  
df -h  

Processus :  
htop  
```

**Avantage** : Copier-coller rapide sans chercher.

### Numéros et codes temporaires

**Informations passagères** :

```
Livraison colis :  
Code de suivi : AB123456789FR  
Arrivée prévue : 18/04  
```

**Supprimez** après usage.

### Brainstorming et idées

**Capturer rapidement** :

```
Idées projet app :
- Fonction de rappel automatique
- Thème sombre
- Synchronisation cloud
- Widget calendrier
- Export PDF
```

**Ensuite** : Transférez vers un outil de gestion de projet.

### Citations et inspirations

**Garder une citation motivante** :

```
"Le succès, c'est tomber sept fois
et se relever huit."
- Proverbe japonais
```

Visible pendant le travail.

### Informations de connexion temporaires

**Attention sécurité !** :

Ne stockez **jamais** de mots de passe permanents dans Sticky Notes.

**OK pour** :
- Code WiFi invité temporaire
- Login événementiel (conférence, démo)

**Supprimez** immédiatement après usage.

## Raccourcis et productivité

### Raccourcis clavier utiles

**Dans une note** :

| Raccourci | Action |
|-----------|--------|
| `Ctrl + A` | Tout sélectionner |
| `Ctrl + C` | Copier |
| `Ctrl + V` | Coller |
| `Ctrl + X` | Couper |
| `Ctrl + Z` | Annuler |
| `Ctrl + Y` | Rétablir |

**Navigation** :
- `Début` : Début de ligne
- `Fin` : Fin de ligne
- `Ctrl + Début` : Début de la note
- `Ctrl + Fin` : Fin de la note

### Workflow efficace

**Routine recommandée** :

1. **Matin** : Créez une note "TODO Jour"
2. **Pendant la journée** : Ajoutez notes au fil de l'eau
3. **Soir** : Revoyez les notes, transférez actions importantes
4. **Fin de semaine** : Nettoyez les notes obsolètes

**Résultat** : Bureau organisé, esprit clair.

### Intégration avec autres outils

**Complémentarité** :

**Sticky Notes** :
- Rappels immédiats
- Informations temporaires
- Tâches du jour

**Gestionnaire de tâches** (Gnome To Do, Todoist) :
- Projets long terme
- Échéances
- Rappels programmés

**Notes complètes** (Gnote, Tomboy, Joplin) :
- Documentation détaillée
- Organisation hiérarchique
- Recherche avancée

**Utilisation combinée** : Sticky pour l'immédiat, autres outils pour le long terme.

## Alternatives à Sticky Notes

### Notes GNOME (Gnote)

**Application de notes GNOME** :

**Installation** :
```bash
sudo apt install gnote
```

**Caractéristiques** :
- Notes organisées en carnets
- Recherche puissante
- Liens entre notes
- Tags et catégories
- Plus complet que Sticky

**Différence** :
- Gnote : Application complète avec bibliothèque
- Sticky : Pense-bêtes visuels sur bureau

### Tomboy

**Prédécesseur de Gnote** :

```bash
sudo apt install tomboy
```

**Moins maintenu**, Gnote est préféré.

### Xpad

**Alternative légère** :

```bash
sudo apt install xpad
```

**Caractéristiques** :
- Très similaire à Sticky
- Léger
- Simple

**Interface** : Quasi identique à Sticky Notes.

### KNotes (KDE)

**Pour utilisateurs KDE** :

```bash
sudo apt install knotes
```

**Intégration KDE** :
- S'intègre dans l'écosystème KDE
- Synchronisation Kontact
- Alarmes et rappels

### Alternatives en ligne

**Google Keep** :
- Service web Google
- Application mobile et web
- Synchronisation cloud
- Partage de notes
- Étiquettes et couleurs

**Microsoft OneNote** :
- Application Microsoft
- Très complet
- Synchronisation OneDrive
- Disponible via navigateur ou application

**Simplenote** :
- Minimaliste
- Synchronisation multi-appareils
- Gratuit et open source

**Standard Notes** :
- Focus sécurité et vie privée
- Chiffrement bout en bout
- Synchronisation sécurisée

**Différence** : Services en ligne nécessitent Internet, mais synchronisent partout.

### Comparaison rapide

| Outil | Type | Complexité | Sync Cloud | Recommandation |
|-------|------|------------|------------|----------------|
| **Sticky** | Bureau | Très simple | Non | Rappels visuels |
| **Gnote** | Application | Moyenne | Non | Notes organisées |
| **Google Keep** | Web/Mobile | Simple | Oui | Multi-appareils |
| **Joplin** | Application | Avancée | Oui | Power users |
| **Standard Notes** | Web/App | Moyenne | Oui | Sécurité |

## Dépannage

### Sticky Notes ne démarre pas

**Solutions** :

**Vérifier l'installation** :
```bash
dpkg -l | grep sticky
```

**Réinstaller** :
```bash
sudo apt remove sticky  
sudo apt install sticky  
```

**Lancer depuis terminal** (voir erreurs) :
```bash
sticky
```

### Notes disparues

**Récupération** :

**Vérifier si masquées** :
- Clic sur l'icône dans la barre des tâches
- Les notes réapparaissent peut-être

**Vérifier les fichiers** :
```bash
ls ~/.local/share/sticky/
```
ou
```bash
ls ~/.config/sticky/
```

**Si fichiers présents** : Notes sauvegardées, problème d'affichage  
**Si fichiers absents** : Notes perdues  

**Restaurer depuis backup** :
- Si vous aviez sauvegardé le dossier
- Copiez-le à son emplacement

### Note bloquée ou ne réagit pas

**Redémarrer Sticky** :

1. Tuez le processus :
```bash
killall sticky
```

2. Relancez :
```bash
sticky &
```

**Ou** : Redémarrez l'ordinateur.

### Icône manquante dans la barre des tâches

**Affichage de l'icône** :

**Vérifier paramètres** :
1. Préférences Sticky
2. **Afficher l'icône de notification** : Activé

**Si toujours absent** :
- Problème de zone de notification
- Vérifiez paramètres du panneau Cinnamon

### Notes trop grandes ou trop petites

**Réinitialiser taille** :

- Redimensionnez manuellement (glissez les bords)
- Ou supprimez et recréez la note
- Ou réinitialisez les paramètres par défaut

## Sauvegarder et synchroniser

### Sauvegarde manuelle

**Exporter vos notes** :

1. Identifiez le dossier de données :
```bash
ls ~/.local/share/sticky/
```

2. Copiez-le :
```bash
cp -r ~/.local/share/sticky/ ~/Documents/Backup-Sticky/
```

**Restauration** :
```bash
cp -r ~/Documents/Backup-Sticky/* ~/.local/share/sticky/
```

### Synchronisation cloud (manuel)

**Avec Nextcloud/ownCloud** :

1. Installez le client Nextcloud
2. Créez un lien symbolique :
```bash
ln -s ~/.local/share/sticky/ ~/Nextcloud/Sticky-Notes/
```

**Résultat** : Notes synchronisées via Nextcloud.

**Avec Git** :

```bash
cd ~/.local/share/sticky/  
git init  
git add .  
git commit -m "Initial commit"  
git remote add origin https://github.com/votrecompte/sticky-notes.git  
git push -u origin master  
```

**Mise à jour régulière** :
```bash
cd ~/.local/share/sticky/  
git add .  
git commit -m "Mise à jour notes"  
git push  
```

**Sur un autre PC** :
```bash
git clone https://github.com/votrecompte/sticky-notes.git ~/.local/share/sticky/
```

### Migration vers autre système

**Exporter contenu** :

Si vous changez d'outil (Sticky → Google Keep) :
1. Ouvrez chaque note Sticky
2. Copiez le contenu
3. Créez une note dans le nouvel outil
4. Collez

**Ou** : Script pour automatiser (avancé).

## Conseils de productivité

### Principe "Inbox Zero" adapté

**Traiter vos notes** :

Comme les emails, ne laissez pas s'accumuler :
1. **Capturer** : Créez note rapidement
2. **Traiter** : Décidez de l'action
3. **Archiver** : Transférez vers outil approprié
4. **Supprimer** : Effacez l'obsolète

**Routine quotidienne** :
- Matin : Notes du jour
- Soir : Revue et nettoyage

### Ne pas surcharger

**Limite recommandée** : 5-10 notes maximum à l'écran.

**Au-delà** :
- Bureau encombré
- Perte de focus
- Difficile de retrouver l'info

**Solution** :
- Transférez vers gestionnaire de tâches
- Supprimez le obsolète
- Archivez dans fichier texte

### Codes couleur

**Système personnel** :

- **Jaune** : Information générale
- **Rouge** : Urgent
- **Bleu** : Travail
- **Vert** : Personnel
- **Orange** : Idées

**Cohérence** : Utilisez toujours les mêmes couleurs pour mêmes types.

### Format standardisé

**Template de note** :

```
[CATÉGORIE] Titre
Date : JJ/MM/AAAA

Contenu...

---
À faire avant : DD/MM
```

**Avantage** : Lecture rapide, structure claire.

## Limitations de Sticky Notes

### Ce que Sticky ne fait pas

**Pas de** :
- Synchronisation cloud native
- Rappels programmés (alarmes)
- Pièces jointes
- Mise en forme riche (gras, italique limités)
- Recherche globale dans toutes notes
- Chiffrement
- Partage avec d'autres utilisateurs

**Pour ces besoins** : Utilisez des outils plus avancés (Gnote, Joplin, Google Keep).

### Sécurité

**Notes en clair** :
- Fichiers non chiffrés
- Lisibles par quiconque accède au PC
- Ne stockez pas d'informations sensibles

**Protection** :
- Verrouillez votre session
- Chiffrez le disque (LUKS)
- Pour vraie sécurité : Standard Notes, Joplin avec chiffrement

## Bonnes pratiques

### Organisation efficace

**Règles d'or** :

1. **Une note = Une idée**
   - Pas de notes fourre-tout
   - Facilite suppression/archivage

2. **Titres clairs**
   - Première ligne = Titre descriptif
   - Exemple : "TODO Lundi" plutôt que juste texte

3. **Nettoyage régulier**
   - Fin de journée : Supprimez l'obsolète
   - Fin de semaine : Grande revue

4. **Utilisation temporaire**
   - Sticky = Court terme
   - Long terme → Autre outil

### Exemples d'utilisation

**Développeur** :
- Commandes Git fréquentes
- URLs de test
- Tokens temporaires (supprimez après !)

**Étudiant** :
- Devoirs du jour
- Numéro de salle de cours
- Idées pour mémoire

**Professionnel** :
- Numéros de dossiers
- Codes de réunion Zoom
- Liste appels à passer

**Personnel** :
- Liste courses
- Films à voir
- Idées cadeaux

## Ressources et liens

### Documentation

**Sticky** :
- Pas de site officiel dédié
- Partie de Linux Mint
- Documentation minimaliste

**Alternatives** :
- Gnote : [https://wiki.gnome.org/Apps/Gnote](https://wiki.gnome.org/Apps/Gnote)
- Xpad : Page GitHub

### Communauté

**Forums Linux Mint** :
- Section applications
- Astuces utilisateurs

**Reddit** :
- r/linuxmint
- Discussions outils productivité

## Conclusion

Sticky Notes est un outil simple mais efficace pour capturer rapidement vos idées, rappels et tâches directement sur votre bureau Linux Mint. Sa simplicité est sa force : pas de courbe d'apprentissage, utilisation immédiate, sans distraction.

**Points clés à retenir** :

- **Simple** : Créer, écrire, fermer, c'est tout
- **Visuel** : Notes toujours visibles sur le bureau
- **Léger** : Ne consomme presque pas de ressources
- **Gratuit** : Open source, aucun coût
- **Local** : Vos notes restent sur votre PC

**Quand utiliser Sticky Notes** :
- Rappels immédiats et temporaires
- Listes de tâches du jour
- Informations à copier-coller fréquemment
- Brainstorming rapide

**Quand utiliser autre chose** :
- Notes complexes et organisées → Gnote, Joplin
- Synchronisation multi-appareils → Google Keep, Simplenote
- Projets et tâches long terme → Gestionnaire de tâches dédié

**Pour bien commencer** :
1. Lancez Sticky Notes
2. Créez votre première note (liste du jour)
3. Positionnez-la où elle ne gêne pas mais reste visible
4. Utilisez quotidiennement
5. Nettoyez régulièrement

Sticky Notes est l'outil parfait pour le "brain dump" quotidien : videz votre tête dans des notes, organisez, puis transférez vers les outils appropriés. Simple, efficace, sans friction. Essayez-le dès aujourd'hui !

---


⏭️ [Gestion des logiciels](/06-gestion-des-logiciels/README.md)
