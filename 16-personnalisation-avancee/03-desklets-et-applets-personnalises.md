🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 16.3 - Desklets et applets personnalisés

## Introduction

Maintenant que vous savez installer des extensions (chapitre 16.2), il est temps d'aller plus loin et de vraiment personnaliser vos applets et desklets pour qu'ils correspondent exactement à vos besoins. Ce chapitre vous guidera dans la personnalisation avancée de ces éléments pour créer un bureau vraiment unique.

Les applets et desklets ne sont pas juste des outils à installer et oublier : ils peuvent être finement ajustés, combinés et personnalisés pour créer une expérience de bureau parfaitement adaptée à votre façon de travailler.

---

## Rappel : Applets vs Desklets

Avant d'aller plus loin, clarifions bien la différence :

### Applets
- **Position** : Dans le panneau (barre des tâches)
- **Fonction** : Outils et raccourcis rapides
- **Visibilité** : Toujours visible (tant que le panneau l'est)
- **Exemples** : Météo, moniteur système, horloge
- **Interaction** : Généralement via un clic

### Desklets
- **Position** : Directement sur le bureau
- **Fonction** : Widgets informatifs ou décoratifs
- **Visibilité** : Visible sur le bureau (peut être caché par les fenêtres)
- **Exemples** : Calendrier, notes, horloge de bureau
- **Interaction** : Toujours affichés, consultation rapide

### Quand utiliser l'un ou l'autre ?

**Utilisez un applet si :**
- Vous voulez un accès permanent et rapide
- L'espace est limité
- Vous avez besoin d'interagir souvent avec l'élément
- L'information doit toujours être visible

**Utilisez un desklet si :**
- Vous avez de l'espace sur votre bureau
- Vous voulez quelque chose de visuellement présent
- L'information est consultée régulièrement mais pas constamment
- Vous aimez un bureau vivant et informatif

---

## Personnaliser les applets

### Accéder aux paramètres d'un applet

**Méthode simple :**
1. Faites un **clic droit** sur l'applet dans le panneau
2. Sélectionnez **"Configurer..."**
3. Une fenêtre de paramètres s'ouvre

**Alternative :**
1. Menu → Préférences → Applets
2. Onglet "Gérer"
3. Sélectionnez l'applet
4. Cliquez sur l'icône d'**engrenage** (⚙️)

### Options de personnalisation courantes

Bien que chaque applet soit différent, voici les options les plus fréquentes :

#### 1. Apparence visuelle

**Taille et espacement**
- Largeur de l'applet
- Hauteur (si applicable)
- Marges et padding

**Couleurs**
- Couleur du texte
- Couleur de fond
- Couleur des icônes
- Thème de couleur (clair/sombre)

**Polices**
- Type de police
- Taille de police
- Gras, italique, etc.

**Exemple pratique : Applet Météo**
```
Paramètres → Apparence
- Afficher l'icône : ✓
- Afficher le texte : ✓
- Taille de la police : 10
- Afficher en degrés : Celsius
- Couleur du texte : Blanc
```

#### 2. Comportement et fonctionnalité

**Intervalles de mise à jour**
- Fréquence de rafraîchissement (secondes, minutes)
- Important pour les performances

**Clics et actions**
- Action au clic gauche
- Action au clic droit
- Action au clic molette
- Action au survol

**Notifications**
- Afficher des notifications
- Sons d'alerte
- Conditions de notification

**Exemple pratique : Moniteur système**
```
Paramètres → Comportement
- Intervalle de mise à jour : 2 secondes
- Afficher le graphique : ✓
- Clic gauche : Ouvrir moniteur système
- Afficher en pourcentage : ✓
```

#### 3. Contenu et informations

**Choix des données affichées**
- Quelles informations montrer
- Format d'affichage
- Unités de mesure

**Ordre et priorité**
- Ordre des éléments
- Informations prioritaires

**Exemple pratique : Horloge**
```
Paramètres → Format
- Format : 24 heures
- Afficher les secondes : ✗
- Afficher la date : ✓
- Format de date : jj/mm/aaaa
- Police personnalisée : ✓
```

### Positionnement des applets dans le panneau

Vous pouvez organiser vos applets comme vous le souhaitez :

**Déplacer un applet :**
1. **Méthode 1** : Cliquez et maintenez sur l'applet, puis glissez
2. **Méthode 2** : Clic droit → "Déplacer" → utilisez les flèches du clavier → Entrée

**Créer des groupes logiques :**
- Groupez les applets par fonction (système, multimédia, internet, etc.)
- Utilisez des séparateurs pour créer des zones visuelles

**Ajouter un séparateur :**
1. Clic droit sur le panneau → "Applets"
2. Recherchez "Separator" ou "Séparateur"
3. Ajoutez-le entre vos groupes d'applets

### Exemples de configurations populaires

#### Configuration "Monitoring complet"

**Applets utilisés :**
- CPU Monitor (usage processeur)
- RAM Monitor (usage mémoire)
- Network Monitor (vitesse réseau)
- Disk Usage (espace disque)

**Organisation :**
```
[CPU 45%] [RAM 3.2GB] | [↓ 2.5MB/s ↑ 0.8MB/s] | [Disk 65%]
```

**Paramètres recommandés :**
- Mise à jour : 2-3 secondes
- Graphiques compacts
- Couleurs différentes pour chaque ressource

#### Configuration "Productivité"

**Applets utilisés :**
- Weather (météo)
- Todo List (tâches)
- Clipboard Manager (presse-papier)
- Timer/Pomodoro

**Organisation :**
```
[☀️ 22°C] | [✓ 3 tâches] | [📋] | [⏱️ 25:00]
```

#### Configuration "Minimaliste"

**Applets utilisés :**
- Horloge/Date
- Volume
- Indicateur réseau
- Indicateur batterie (laptop)

**Organisation :**
```
[14:32 | 29/11/2024] ... [🔊] [📶] [🔋 85%]
```

---

## Personnaliser les desklets

### Accéder aux paramètres d'un desklet

**Méthode simple :**
1. Faites un **clic droit** sur le desklet sur votre bureau
2. Sélectionnez **"Configurer..."**

**Alternative :**
1. Clic droit sur le bureau → "Ajouter des desklets"
2. Onglet "Gérer"
3. Sélectionnez le desklet
4. Cliquez sur l'icône d'**engrenage** (⚙️)

### Options de personnalisation courantes

#### 1. Position et taille

**Position sur le bureau**
- Coin supérieur gauche/droit
- Coin inférieur gauche/droit
- Centre
- Position personnalisée (x, y)

**Taille**
- Largeur
- Hauteur
- Mise à l'échelle automatique
- Proportions fixes

**Verrouiller en position**
- Empêche le déplacement accidentel
- Utile une fois l'emplacement parfait trouvé

**Exemple pratique : Horloge de bureau**
```
Paramètres → Position
- Position X : 1700 (coin droit de l'écran)
- Position Y : 50 (haut de l'écran)
- Verrouiller la position : ✓
```

#### 2. Apparence et style

**Transparence**
- Fond transparent
- Fond semi-transparent
- Fond opaque

**Bordures et ombres**
- Bordure visible
- Ombre portée
- Effet de verre/flou

**Thèmes personnalisés**
- Beaucoup de desklets supportent des thèmes CSS
- Changement de couleurs
- Modification de la disposition

**Exemple pratique : Notes (Sticky Notes)**
```
Paramètres → Apparence
- Couleur de fond : Jaune (#FFFFCC)
- Transparence : 90%
- Bordure : Visible
- Couleur de bordure : Orange
- Police : Liberation Sans
- Taille de police : 12
```

#### 3. Comportement

**Toujours visible**
- Reste au-dessus des fenêtres
- Reste en dessous des fenêtres
- Niveau normal

**Visibilité**
- Visible sur tous les espaces de travail
- Visible uniquement sur l'espace actuel
- Masquer sur bureau complet

**Interactions**
- Clic pour cacher/afficher
- Raccourci clavier
- Auto-masquage

**Exemple pratique : Moniteur système de bureau**
```
Paramètres → Comportement
- Toujours au-dessus : ✗
- Visible sur tous les bureaux : ✓
- Intervalle de mise à jour : 3 secondes
- Afficher les graphiques : ✓
```

### Organiser plusieurs desklets

Si vous utilisez plusieurs desklets, organisez-les intelligemment :

**Principes d'organisation :**

1. **Regroupement thématique**
   - Desklets d'information en haut à droite
   - Desklets de productivité en bas à gauche
   - Desklets décoratifs au centre

2. **Hiérarchie visuelle**
   - Les desklets importants plus grands
   - Les desklets secondaires plus petits
   - Utilisation cohérente des couleurs

3. **Éviter le désordre**
   - Ne surchargez pas votre bureau
   - 3-5 desklets maximum recommandé
   - Laissez de l'espace pour les fenêtres

**Exemple de disposition équilibrée :**

```
┌─────────────────────────────────────┐
│                                     │
│  [Météo]              [Horloge]     │
│  [22°C]               [14:32]       │
│                                     │
│                                     │
│         (Espace de travail)         │
│                                     │
│                                     │
│  [Notes]              [Calendrier]  │
│  [- Tâche 1]          [Nov 2024]    │
│  [- Tâche 2]          [29 ▪ ▪ ▪]    │
└─────────────────────────────────────┘
```

### Exemples de configurations de desklets

#### Configuration "Dashboard d'information"

**Desklets utilisés :**
- Horloge analogique (centre-haut)
- Météo détaillée (haut-droit)
- Calendrier mensuel (bas-droit)
- Moniteur système (haut-gauche)

**Paramétrage :**
- Transparence légère (85%)
- Toujours visibles
- Mise à jour automatique
- Thème cohérent (même palette de couleurs)

#### Configuration "Productivité minimaliste"

**Desklets utilisés :**
- Notes (sticky notes) - coin bas-gauche
- Todo List - coin bas-droit

**Paramétrage :**
- Notes jaunes classiques
- Police simple et lisible
- Pas de transparence (pour la lisibilité)
- Raccourcis clavier pour afficher/cacher

#### Configuration "Monitoring avancé"

**Desklets utilisés :**
- System Monitor (graphiques CPU/RAM) - haut-gauche
- Network Monitor (trafic réseau) - haut-droit
- Drive Monitor (espace disque) - bas-gauche

**Paramétrage :**
- Graphiques détaillés
- Mise à jour rapide (1-2 secondes)
- Transparence légère
- Codes couleur pour les alertes

---

## Combiner applets et desklets

La vraie puissance vient de la combinaison intelligente des deux :

### Principe de complémentarité

**Applet = Accès rapide** → **Desklet = Information détaillée**

**Exemple 1 : Météo**
- **Applet** : Température actuelle dans le panneau (22°C)
- **Desklet** : Prévisions complètes sur 7 jours sur le bureau

**Exemple 2 : Système**
- **Applet** : Icône de monitoring avec pourcentage CPU
- **Desklet** : Graphiques détaillés de toutes les ressources

**Exemple 3 : Calendrier**
- **Applet** : Date et heure dans le panneau
- **Desklet** : Calendrier mensuel avec événements

### Workflow recommandé

**Pour un utilisateur standard :**
```
Panneau (Applets) :
- Horloge/Date
- Volume
- Réseau
- Météo (température)

Bureau (Desklets) :
- Notes pour tâches urgentes
- Calendrier mensuel
```

**Pour un utilisateur power user :**
```
Panneau (Applets) :
- Moniteur système compact
- Presse-papier
- Météo
- Contrôle musique
- Todo counter (nombre de tâches)

Bureau (Desklets) :
- Système monitor détaillé
- Notes techniques
- Calendrier avec événements
```

**Pour un développeur :**
```
Panneau (Applets) :
- CPU/RAM monitoring
- Network monitor
- Git status
- Docker containers status

Bureau (Desklets) :
- Moniteur système graphique
- Notes de code
- Timer Pomodoro
```

---

## Créer ses propres applets et desklets

Pour les utilisateurs qui souhaitent aller encore plus loin, il est possible de créer ses propres applets et desklets.

### Vue d'ensemble de la création

**Compétences nécessaires :**
- JavaScript (logique)
- CSS (style)
- JSON (configuration)
- Notions de base en programmation

**Niveau de difficulté :**
- Débutant : Modifier un applet/desklet existant
- Intermédiaire : Créer un applet simple
- Avancé : Créer un applet complexe avec interactions

### Structure d'un applet/desklet

**Fichiers principaux :**

```
mon-applet/
├── metadata.json        (Informations sur l'applet)
├── applet.js           (Code principal)
├── settings-schema.json (Configuration)
├── stylesheet.css      (Apparence)
├── icon.png           (Icône)
└── README.md          (Documentation)
```

**metadata.json - Exemple :**
```json
{
  "uuid": "mon-applet@utilisateur",
  "name": "Mon Super Applet",
  "description": "Description de mon applet",
  "version": "1.0",
  "author": "Votre nom",
  "cinnamon-version": ["5.0", "5.2", "5.4"]
}
```

### Modifier un applet existant

C'est la meilleure façon d'apprendre pour les débutants.

**Étapes :**

1. **Trouvez l'applet à modifier**
   - Naviguez vers : `~/.local/share/cinnamon/applets/`
   - Ou : `/usr/share/cinnamon/applets/` (applets système)

2. **Copiez-le dans votre dossier local**
   ```bash
   cp -r /usr/share/cinnamon/applets/calendar@cinnamon.org ~/.local/share/cinnamon/applets/mon-calendrier@moi
   ```

3. **Modifiez l'UUID dans metadata.json**
   - Ouvrez `metadata.json`
   - Changez `"uuid"` en quelque chose d'unique

4. **Faites vos modifications**
   - Éditez `applet.js` pour la logique
   - Éditez `stylesheet.css` pour l'apparence

5. **Testez**
   - Ajoutez votre applet modifié depuis le gestionnaire
   - `Alt+F2` → `r` pour recharger Cinnamon

### Exemple simple : Applet "Hello World"

Voici un applet minimaliste pour comprendre la structure :

**applet.js :**
```javascript
const Applet = imports.ui.applet;

class MyApplet extends Applet.TextApplet {
    constructor(orientation, panel_height, instance_id) {
        super(orientation, panel_height, instance_id);

        this.set_applet_label("Hello World!");
        this.set_applet_tooltip("Mon premier applet");
    }

    on_applet_clicked(event) {
        global.log("Applet cliqué!");
    }
}

function main(metadata, orientation, panel_height, instance_id) {
    return new MyApplet(orientation, panel_height, instance_id);
}
```

**Ce que fait ce code :**
- Affiche "Hello World!" dans le panneau
- Quand on clique, écrit un message dans les logs
- Tooltip au survol : "Mon premier applet"

### Exemple simple : Desklet affichant l'heure

**desklet.js :**
```javascript
const Desklet = imports.ui.desklet;
const St = imports.gi.St;
const Mainloop = imports.mainloop;

class MyDesklet extends Desklet.Desklet {
    constructor(metadata, desklet_id) {
        super(metadata, desklet_id);

        this._updateLoop();
    }

    _updateLoop() {
        let now = new Date();
        let timeString = now.toLocaleTimeString();

        this.setContent(timeString);

        Mainloop.timeout_add_seconds(1, () => {
            this._updateLoop();
        });
    }

    setContent(text) {
        this._label = new St.Label({text: text});
        this.setContent(this._label);
    }
}

function main(metadata, desklet_id) {
    return new MyDesklet(metadata, desklet_id);
}
```

### Ressources pour apprendre

**Documentation officielle :**
- [Cinnamon Tutorials](https://projects.linuxmint.com/reference/git/cinnamon-tutorials/)
- [Cinnamon JavaScript API](https://projects.linuxmint.com/reference/git/cinnamon/)

**Exemples de code :**
- Explorez les applets installés dans `~/.local/share/cinnamon/applets/`
- Lisez le code d'applets populaires sur GitHub
- Cinnamon Spices propose de nombreux exemples

**Communautés :**
- Forum Linux Mint (section développement)
- GitHub Cinnamon Spices
- Stack Overflow (tag : cinnamon)

---

## Partager vos créations

Si vous créez un applet ou desklet intéressant, vous pouvez le partager !

### Préparer pour le partage

**Checklist avant publication :**

1. **Code propre et commenté**
   - Commentaires en anglais (portée internationale)
   - Indentation cohérente
   - Noms de variables explicites

2. **Documentation complète**
   - README.md détaillé
   - Instructions d'installation
   - Captures d'écran
   - Liste des fonctionnalités

3. **Métadonnées correctes**
   - metadata.json complet
   - Versions de Cinnamon supportées
   - Informations de contact

4. **Licence**
   - Choisissez une licence open-source (GPL, MIT, etc.)
   - Incluez le fichier LICENSE

5. **Tests**
   - Testez sur différentes versions de Cinnamon
   - Vérifiez sur différentes résolutions d'écran
   - Pas d'erreurs dans les logs

### Soumettre à Cinnamon Spices

**Processus de soumission :**

1. **Créez un compte GitHub**

2. **Forkez le dépôt Cinnamon Spices**
   - Applets : [cinnamon-spices-applets](https://github.com/linuxmint/cinnamon-spices-applets)
   - Desklets : [cinnamon-spices-desklets](https://github.com/linuxmint/cinnamon-spices-desklets)

3. **Ajoutez votre création**
   - Suivez la structure des dossiers existants
   - Respectez les conventions de nommage

4. **Créez une Pull Request**
   - Décrivez votre applet/desklet
   - Expliquez ce qu'il fait
   - Ajoutez des captures d'écran

5. **Attendez la revue**
   - L'équipe Linux Mint va examiner votre code
   - Répondez aux commentaires et suggestions
   - Une fois approuvé, il sera publié !

---

## Paramètres avancés et astuces

### Raccourcis clavier pour desklets

Vous pouvez assigner des raccourcis clavier pour afficher/masquer vos desklets :

**Configuration :**
1. Menu → Préférences → Clavier → Raccourcis → Général
2. Cherchez "Afficher les desklets" ou "Toggle desklets"
3. Assignez un raccourci (ex: `Super+D`)

### Synchronisation entre machines

Si vous utilisez plusieurs ordinateurs Linux Mint :

**Sauvegarder votre configuration :**
```bash
# Sauvegarder les applets
cp -r ~/.local/share/cinnamon/applets ~/sauvegarde-applets

# Sauvegarder les desklets
cp -r ~/.local/share/cinnamon/desklets ~/sauvegarde-desklets

# Sauvegarder les paramètres
dconf dump /org/cinnamon/ > cinnamon-settings.dconf
```

**Restaurer sur une autre machine :**
```bash
# Copier les fichiers
cp -r ~/sauvegarde-applets/* ~/.local/share/cinnamon/applets/
cp -r ~/sauvegarde-desklets/* ~/.local/share/cinnamon/desklets/

# Restaurer les paramètres
dconf load /org/cinnamon/ < cinnamon-settings.dconf
```

### Profils de configuration

Créez différents profils selon vos besoins :

**Exemple de profils :**

1. **Profil "Travail"**
   - Applets : Todo list, Pomodoro timer, Calendar
   - Desklets : System monitor, Notes
   - Thème : Professionnel et sobre

2. **Profil "Multimédia"**
   - Applets : Volume control, Music player control
   - Desklets : Lyrics display, Album art
   - Thème : Coloré et moderne

3. **Profil "Gaming"**
   - Applets : CPU/GPU monitor, Network monitor
   - Desklets : FPS counter, Temperature monitor
   - Thème : Sombre avec accents néon

**Astuce :** Utilisez des scripts bash pour basculer entre profils en copiant différentes configurations.

---

## Dépannage avancé

### L'applet ne se charge pas

**Diagnostic :**

1. **Vérifiez les logs**
   ```bash
   journalctl -f | grep cinnamon
   ```

2. **Mode debug de Cinnamon**
   ```bash
   cinnamon --replace --debug &
   ```

3. **Vérifiez la syntaxe JavaScript**
   - Utilisez un linter : `eslint applet.js`
   - Vérifiez les erreurs de syntaxe

### Le desklet disparaît au redémarrage

**Solutions :**

1. **Vérifiez les paramètres de bureau**
   - Menu → Préférences → Desklets
   - Assurez-vous qu'il est bien activé

2. **Recréez le fichier de configuration**
   ```bash
   rm -rf ~/.cinnamon/configs/desklet-nom@auteur
   ```
   Puis reconfigurez le desklet

3. **Vérifiez les permissions**
   ```bash
   chmod -R 755 ~/.local/share/cinnamon/desklets/
   ```

### Conflits entre applets

**Symptômes :**
- Crash de Cinnamon
- Applets qui ne s'affichent pas
- Ralentissements

**Solutions :**

1. **Désactivez les applets un par un**
   - Identifiez le coupable
   - Vérifiez les incompatibilités connues

2. **Consultez les dépendances**
   - Certains applets nécessitent des bibliothèques spécifiques
   - Vérifiez le README de chaque applet

3. **Mettez à jour**
   - Assurez-vous que tous les applets sont à jour
   - Certaines incompatibilités sont corrigées dans les mises à jour

---

## Conseils de performance

### Optimiser les applets

**Intervalles de mise à jour :**
- Augmentez les intervalles pour réduire la charge CPU
- 1 seconde pour monitoring critique
- 3-5 secondes pour informations générales
- 30+ secondes pour données peu changeantes (météo)

**Désactiver les animations :**
- Certains applets ont des animations gourmandes
- Désactivez-les dans les paramètres si besoin

**Limiter les applets actifs :**
- Maximum 5-7 applets recommandé
- Gardez seulement ceux que vous utilisez vraiment

### Optimiser les desklets

**Transparence et effets :**
- La transparence consomme des ressources graphiques
- Utilisez des fonds opaques sur matériel ancien

**Nombre de desklets :**
- 3-4 desklets maximum recommandé
- Plus peut ralentir le bureau

**Mise à jour intelligente :**
- Désactivez la mise à jour quand une fenêtre est maximisée
- Option disponible dans certains desklets

---

## Cas d'usage inspirants

### Setup pour développeur web

**Panneau :**
- Git Status Applet (branches, commits en attente)
- Docker Container Manager
- System Monitor (compact)
- Weather

**Bureau :**
- Notes avec snippets de code
- Timer Pomodoro
- API Response Monitor
- Server Status Monitor

### Setup pour étudiant

**Panneau :**
- Calendar avec événements
- Todo List avec compteur
- Weather
- Timer

**Bureau :**
- Notes de cours
- Calendrier mensuel
- Citations motivantes
- Countdown to exam

### Setup pour gamer

**Panneau :**
- GPU Monitor
- Network Speed Monitor
- Discord Activity
- Game Launcher Quick Access

**Bureau :**
- FPS Monitor
- Temperature Dashboard
- Voice Chat Controls
- Game Time Tracker

---

## Aller plus loin

Une fois maître des applets et desklets, explorez :

- **Conky** (Chapitre 16.4) : Monitoring système ultra-personnalisable
- **Personnalisation du terminal** (Chapitre 16.5)
- **Scripts d'automatisation** (Chapitre 20.1)
- **Création d'extensions complètes** : Combinez applets, desklets et extensions

---

## Résumé

Dans ce chapitre, vous avez appris :

- ✅ La différence pratique entre applets et desklets
- ✅ Comment personnaliser finement vos applets et desklets
- ✅ Comment organiser et combiner applets et desklets efficacement
- ✅ Les bases de la création de vos propres applets/desklets
- ✅ Comment partager vos créations avec la communauté
- ✅ Des techniques avancées de configuration et synchronisation
- ✅ Des exemples concrets de setups pour différents usages
- ✅ L'optimisation des performances

Les applets et desklets personnalisés vous permettent de créer un environnement de bureau vraiment unique, parfaitement adapté à votre flux de travail. N'hésitez pas à expérimenter et à partager vos découvertes avec la communauté !

---


⏭️ [Conky pour le monitoring visuel](/16-personnalisation-avancee/04-conky-pour-le-monitoring-visuel.md)
