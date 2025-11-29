🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 16.7 - Animations et effets

## Introduction

Les animations et effets visuels donnent vie à votre bureau Linux Mint. Bien qu'ils ne soient pas essentiels au fonctionnement du système, ils rendent l'expérience utilisateur plus agréable, fluide et moderne. Des fenêtres qui s'ouvrent en fondu, des ombres subtiles, ou des effets de minimisation élégants : tous ces petits détails contribuent à créer une interface plaisante à utiliser.

Dans ce chapitre, nous allons découvrir comment activer, désactiver et personnaliser les animations et effets visuels de votre système Linux Mint, tout en gardant un œil sur les performances.

---

## Qu'est-ce que les animations et effets ?

### Animations

Les **animations** sont des transitions visuelles qui se produisent lors de certaines actions :

- **Ouverture/fermeture de fenêtres** : Fondu, zoom, slide
- **Minimisation/maximisation** : Effet "magique", fade
- **Changement d'espace de travail** : Glissement, cube 3D
- **Menus déroulants** : Apparition progressive
- **Survol d'éléments** : Changements de couleur fluides

### Effets

Les **effets** sont des améliorations visuelles permanentes ou contextuelles :

- **Ombres portées** : Sous les fenêtres et menus
- **Transparence** : Fenêtres semi-transparentes
- **Flou** : Arrière-plans flous
- **Animations du pointeur** : Traînées, ondulations
- **Effets de bureau** : Cube 3D, desktop wall

### Le compositeur

Le **compositeur** (ou compositing manager) est le programme qui gère tous ces effets visuels. Sur Cinnamon, c'est **Muffin**. Sur MATE, c'est **Marco** avec Compton. Sur Xfce, c'est **Xfwm4**.

**Rôle du compositeur :**
- Gérer la transparence
- Dessiner les ombres
- Animer les transitions
- Gérer les effets visuels

**Important :** Les effets consomment des ressources graphiques. Sur des ordinateurs anciens ou avec carte graphique faible, il peut être préférable de les limiter.

---

## Effets disponibles dans Cinnamon

Cinnamon offre un bon équilibre entre beauté et performance.

### Effets de base activés par défaut

**1. Ombres portées**
- Sous les fenêtres
- Sous les menus et popups
- Donne de la profondeur

**2. Animations de fenêtres**
- Ouverture en fondu
- Fermeture en fondu
- Minimisation avec effet

**3. Animations de menus**
- Apparition progressive
- Transition douce

**4. Effets de survol**
- Changements de couleur
- Mises en évidence

### Effets avancés (à activer)

**1. Transparence**
- Fenêtres semi-transparentes
- Panels transparents
- Menus avec transparence

**2. Effets 3D**
- Cube de bureau (rotation 3D)
- Cylinder desktop
- Sphere desktop

**3. Wobble (tremblement)**
- Fenêtres qui "tremblent" quand déplacées
- Effet élastique

**4. Animations avancées**
- Magic lamp (minimisation style macOS)
- Vacuum (aspiration)
- Roll up (enroulement)

---

## Accéder aux paramètres d'effets

### Sur Cinnamon

**Paramètres généraux :**

1. **Menu** → **Préférences** → **Effets**

Ou :

1. **Menu** → **Paramètres système**
2. **Préférences** → **Effets**

**Paramètres avancés :**

1. **Menu** → **Préférences** → **Extensions**
2. Cherchez les extensions liées aux effets

### Sur MATE

**Activer le compositeur :**

1. **Menu** → **Centre de contrôle**
2. **Fenêtres** ou **Gestionnaire de fenêtres**
3. Cochez **"Activer le compositeur logiciel"**

**Installer Compiz (optionnel, pour effets avancés) :**
```bash
sudo apt install compiz compiz-plugins compizconfig-settings-manager
```

### Sur Xfce

**Paramètres du compositeur :**

1. **Menu** → **Paramètres** → **Gestionnaire de fenêtres**
2. Onglet **"Compositeur"**
3. Cochez **"Activer le compositeur d'affichage"**

**Options disponibles :**
- Ombres sous les fenêtres
- Ombres sous les menus
- Opacité des fenêtres inactives
- Zoom du bureau

---

## Configurer les effets dans Cinnamon

### Paramètres de base

**Accéder aux effets :**
Menu → Préférences → Effets

**Options disponibles :**

**1. Activer les effets**
- Case à cocher en haut
- Active/désactive tous les effets d'un coup
- Utile pour tester l'impact sur les performances

**2. Style d'effets**
- **Traditionnel** : Effets classiques et sobres
- **Personnalisé** : Définissez vos propres paramètres

**3. Effets d'ouverture de fenêtres**
- Aucun
- Fondu (fade)
- Échelle (scale)
- Fondu et échelle

**4. Effets de fermeture de fenêtres**
- Aucun
- Fondu
- Échelle
- Fondu et échelle

**5. Effets de minimisation**
- Traditionnel (vers la barre des tâches)
- Fondu
- Échelle

**6. Effets de maximisation**
- Aucun
- Échelle

**7. Effets de mosaïque** (Snap)
- Animation quand vous "collez" une fenêtre à un bord

**8. Effets de carte** (Alt+Tab)
- Animation lors du changement de fenêtre
- Timeline
- Coverflow
- Flip

### Vitesse des animations

**Ajuster la rapidité :**

Dans les paramètres d'effets, cherchez :
- **Vitesse des transitions** : Curseur de lent à rapide
- Valeur recommandée : Moyenne (position centrale)

**Animations trop lentes :**
- Augmentez la vitesse
- Ou désactivez certains effets

**Animations trop rapides :**
- Réduisez la vitesse
- Les transitions sont plus élégantes au ralenti

### Ombres

**Personnaliser les ombres :**

Bien que souvent dans les paramètres de thème, vous pouvez ajuster :

1. Menu → Préférences → Thèmes
2. Certains thèmes ont des ombres intégrées
3. Pour des réglages fins, éditez le CSS du thème

**Désactiver les ombres (performances) :**
- Certains thèmes offrent des versions "no-shadow"
- Ou désactivez le compositeur (voir plus bas)

### Transparence

**Rendre le panneau transparent :**

1. Clic droit sur le panneau → **Propriétés du panneau**
2. Section **"Apparence"**
3. **Opacité du panneau** : Ajustez le curseur (0-100%)
4. 100% = opaque, 0% = transparent

**Fenêtres transparentes :**

1. **Menu** → **Préférences** → **Extensions**
2. Téléchargez l'extension **"Transparent Windows"** ou similaire
3. Configurez l'opacité

**Alternative via CompizConfig (avancé) :**
- Nécessite l'installation de Compiz
- Offre un contrôle total sur la transparence

---

## Extensions pour effets supplémentaires

Cinnamon supporte des extensions qui ajoutent des effets visuels.

### Desktop Cube

Transforme votre changement d'espace de travail en rotation de cube 3D.

**Installation :**

1. **Menu** → **Préférences** → **Extensions**
2. Onglet **"Télécharger"**
3. Recherchez **"Desktop Cube"**
4. Cliquez sur **"Installer"**
5. Activez dans l'onglet **"Gérer"**

**Configuration :**
- Nombre de faces (= nombre d'espaces de travail)
- Vitesse de rotation
- Angle de vue

**Utilisation :**
- `Ctrl+Alt+Flèches` pour changer d'espace de travail
- Le cube tourne !

**Note :** Nécessite une carte graphique décente et pilotes installés.

### Wobbly Windows (Fenêtres tremblantes)

Les fenêtres "tremblent" quand vous les déplacez.

**Installation :**

Via extension ou via paramètres du compositeur (si disponible).

**Configuration typique :**
- Intensité du tremblement
- Friction (rapidité d'arrêt)
- Masse des fenêtres

**Avertissement :** Très gourmand en ressources sur certains systèmes.

### Burn My Windows

Extension qui ajoute des effets de fermeture spectaculaires.

**Installation :**

**Via GNOME Extensions (compatible Cinnamon) :**
```bash
# Installer les dépendances
sudo apt install gnome-shell-extension-manager

# Ou télécharger depuis GitHub
git clone https://github.com/Schneegans/Burn-My-Windows.git
cd Burn-My-Windows
make install
```

**Effets disponibles :**
- Feu (la fenêtre brûle)
- Téléportation
- Explosion
- Matrice
- Et plus encore !

**Configuration :**
- Choisissez l'effet par défaut
- Ajustez la vitesse et l'intensité

### Compiz (effets ultimes)

Pour les effets les plus avancés, installez Compiz.

**Installation :**
```bash
sudo apt install compiz compiz-plugins compizconfig-settings-manager
```

**Lancer CompizConfig Settings Manager :**
```bash
ccsm
```

**Effets disponibles :**
- Desktop Cube
- Wobbly Windows
- Fire (feu qui suit la souris)
- Water (effet d'eau au clic)
- Rotate Cube
- Animations avancées
- Expo (vue de tous les bureaux)
- Et des centaines d'autres !

**Avertissement :** Compiz peut être instable et très gourmand. Testez soigneusement.

---

## Configurer le compositeur

Le compositeur est le cœur des effets visuels.

### Désactiver le compositeur (performances)

Si votre ordinateur rame, désactiver le compositeur peut grandement améliorer les performances.

**Sur Cinnamon :**

**Méthode 1 : GUI**
1. Paramètres Système → Général
2. Décochez **"Activer les effets de compositeur"**

**Méthode 2 : Raccourci clavier**
- Par défaut : `Alt+Maj+F12`
- Active/désactive le compositeur à la volée

**Méthode 3 : Terminal**
```bash
# Désactiver
gsettings set org.cinnamon.desktop.wm.preferences compositing-manager false

# Réactiver
gsettings set org.cinnamon.desktop.wm.preferences compositing-manager true
```

**Conséquences de la désactivation :**
- ✗ Plus d'ombres
- ✗ Plus d'animations
- ✗ Plus de transparence
- ✓ Meilleures performances
- ✓ Moins de consommation GPU

### Régler le compositeur (avancé)

**Via dconf-editor :**

```bash
# Installer dconf-editor
sudo apt install dconf-editor

# Lancer
dconf-editor
```

**Naviguez vers :**
```
org.cinnamon.muffin
```

**Paramètres intéressants :**
- `attach-modal-dialogs` : Dialogues attachés
- `center-new-windows` : Centrer nouvelles fenêtres
- `edge-tiling` : Mosaïque sur les bords
- `resize-threshold` : Seuil de redimensionnement
- `tile-maximize` : Maximiser en mosaïque
- `unredirect-fullscreen-windows` : Performances en plein écran

### Changer de compositeur

**Installer un compositeur alternatif (avancé) :**

**Picom (fork de Compton, moderne et performant) :**

```bash
sudo apt install picom
```

**Configuration :**
```bash
mkdir -p ~/.config/picom
nano ~/.config/picom/picom.conf
```

**Exemple de configuration Picom :**
```conf
# Ombres
shadow = true;
shadow-radius = 12;
shadow-opacity = 0.75;
shadow-offset-x = -12;
shadow-offset-y = -12;

# Fondu
fading = true;
fade-in-step = 0.03;
fade-out-step = 0.03;
fade-delta = 5;

# Opacité
inactive-opacity = 0.95;
frame-opacity = 1.0;

# Arrière-plans flous
blur-method = "dual_kawase";
blur-strength = 5;

# Performance
backend = "glx";
vsync = true;
```

**Lancer Picom :**
```bash
picom &
```

**Lancer au démarrage :**
Ajoutez dans Applications au démarrage : `picom --config ~/.config/picom/picom.conf`

---

## Effets selon le matériel

### Configuration pour PC puissant

**Carte graphique dédiée, 8GB+ RAM, processeur récent**

**Paramètres recommandés :**
```
Effets : Tous activés
Animations : Toutes
Vitesse : Moyenne
Ombres : Activées (rayon : 12-15)
Transparence : Oui (panneau : 85-95%)
Extensions : Desktop Cube, Burn My Windows
Compositeur : Activé
Compiz : Possible
```

**Résultat :** Bureau magnifique et fluide

### Configuration pour PC moyen

**Carte graphique intégrée, 4-8GB RAM, processeur moyen**

**Paramètres recommandés :**
```
Effets : Activés
Animations : Basiques (fondu uniquement)
Vitesse : Rapide
Ombres : Activées (rayon : 8-10)
Transparence : Légère (panneau : 90-100%)
Extensions : Une ou deux maximum
Compositeur : Activé
Compiz : Non recommandé
```

**Résultat :** Bureau agréable sans ralentissement

### Configuration pour PC ancien

**Carte graphique basique, 2-4GB RAM, processeur ancien**

**Paramètres recommandés :**
```
Effets : Désactivés ou minimaux
Animations : Aucune
Vitesse : N/A
Ombres : Désactivées
Transparence : Aucune
Extensions : Aucune liée aux effets
Compositeur : Désactivé (Alt+Maj+F12)
Compiz : Absolument pas
```

**Alternative :** Utilisez Xfce ou MATE qui sont plus légers

**Résultat :** Bureau rapide et réactif

### Configuration pour ordinateur portable

**Optimiser pour la batterie**

**Paramètres recommandés :**
```
Effets : Modérés
Animations : Limitées
Vitesse : Rapide (transitions courtes)
Ombres : Légères (rayon : 5-8)
Transparence : Minimale
Extensions : Aucune gourmande
Compositeur : Activé mais léger
```

**Astuce :** Créez un profil "Batterie" et un profil "Secteur"

---

## Animations personnalisées

### Modifier la durée des animations

**Via gsettings (Cinnamon) :**

```bash
# Voir les paramètres actuels
gsettings get org.cinnamon enable-animations

# Activer/désactiver
gsettings set org.cinnamon enable-animations true/false
```

**Modifier des animations spécifiques :**

Éditez le fichier CSS de votre thème :
```bash
nano ~/.themes/MonTheme/cinnamon/cinnamon.css
```

**Exemple d'animation CSS :**
```css
/* Animation de fondu */
.popup-menu {
    transition-duration: 150ms;
}

/* Animation d'ouverture de menu */
.menu {
    transition-duration: 200ms;
}

/* Fenêtres */
.window-close {
    transition-duration: 250ms;
}
```

### Créer des effets personnalisés

**Avec des extensions JavaScript (avancé) :**

Créez une extension Cinnamon qui modifie les animations.

**Exemple simple - Modifier l'effet d'ouverture :**

```javascript
// Dans votre extension
const Meta = imports.gi.Meta;

function init() {
    // Votre code d'initialisation
}

function enable() {
    global.window_manager.connect('map', (wm, actor) => {
        actor.set_opacity(0);
        actor.ease({
            opacity: 255,
            duration: 500,
            mode: Clutter.AnimationMode.EASE_OUT_QUAD
        });
    });
}
```

**Note :** Cela nécessite des connaissances en JavaScript et en développement d'extensions.

---

## Effets de terminal

Même le terminal peut avoir des effets !

### Transparence du terminal

**GNOME Terminal / MATE Terminal :**

1. Édition → Préférences
2. Profils → Couleurs
3. Décochez "Utiliser les couleurs du thème système"
4. **Transparence de l'arrière-plan** : Ajustez le curseur

**Xfce Terminal :**

1. Édition → Préférences
2. Apparence
3. Arrière-plan → Transparent
4. Ajustez l'opacité

### Effet de flou (arrière-plan)

Nécessite un compositeur supportant le flou (comme Picom).

**Dans la configuration de Picom :**
```conf
blur-background = true;
blur-method = "dual_kawase";
blur-strength = 5;

blur-background-frame = true;
blur-background-fixed = false;
```

### Terminaux avec effets intégrés

**Terminator :**
- Support de la transparence native
- Pas d'effets avancés

**Kitty :**
- Transparence
- Performance optimale (GPU)

**Alacritty :**
- Transparence via configuration
- Ultra-rapide

**Cool Retro Term :**
- Terminal avec effet CRT (écran cathodique)
- Effets "vintage"
```bash
sudo apt install cool-retro-term
```

---

## Effets de notifications

### Personnaliser les notifications

**Paramètres de notifications :**

1. Menu → Préférences → Notifications
2. Position sur l'écran
3. Durée d'affichage
4. Transparence (selon le thème)

**Extensions pour notifications :**

**Notification Center :**
- Historique des notifications
- Groupement
- Paramètres avancés

**Installation :**
1. Menu → Préférences → Extensions
2. Télécharger → "Notification Center"
3. Installer et configurer

### Animations de notifications

**Via CSS du thème :**

```css
.notification {
    transition-duration: 300ms;
}

.notification-popup {
    transition-duration: 200ms;
}
```

---

## Performances et optimisation

### Mesurer l'impact des effets

**Surveiller l'utilisation GPU :**

```bash
# Pour NVIDIA
nvidia-smi

# Pour Intel/AMD
sudo apt install intel-gpu-tools
sudo intel_gpu_top

# Pour AMD
radeontop
```

**Surveiller FPS du bureau :**

Certaines extensions affichent les FPS en temps réel.

**Test de performance :**

1. Ouvrez le moniteur système
2. Activez tous les effets
3. Effectuez des actions (ouvrir/fermer fenêtres, changer de bureau)
4. Observez l'utilisation CPU/GPU
5. Si > 80%, réduisez les effets

### Optimisations générales

**1. Désactiver les animations inutiles**
- Gardez uniquement celles que vous appréciez vraiment

**2. Réduire la durée des animations**
- Transitions plus rapides = moins de charge

**3. Limiter les ombres**
- Rayon plus petit
- Ou désactivation complète

**4. Pas de transparence excessive**
- Maximum 10% de transparence si performances limitées

**5. Éviter Compiz sur matériel faible**
- Trop gourmand pour l'ancien matériel

**6. Mettre à jour les pilotes graphiques**
```bash
sudo ubuntu-drivers autoinstall
```

**7. Utiliser le backend GLX (Picom)**
- Plus rapide que XRender
```conf
backend = "glx";
```

### Profils de performance

**Créer des scripts pour basculer :**

**Script "Performance" (tout désactivé) :**
```bash
#!/bin/bash
# disable-effects.sh
gsettings set org.cinnamon.desktop.wm.preferences compositing-manager false
gsettings set org.cinnamon enable-animations false
notify-send "Effets désactivés" "Performances maximales"
```

**Script "Beauté" (tout activé) :**
```bash
#!/bin/bash
# enable-effects.sh
gsettings set org.cinnamon.desktop.wm.preferences compositing-manager true
gsettings set org.cinnamon enable-animations true
notify-send "Effets activés" "Mode visuel"
```

**Rendre exécutables :**
```bash
chmod +x disable-effects.sh enable-effects.sh
```

**Créer des raccourcis clavier :**
1. Menu → Préférences → Clavier → Raccourcis
2. Personnalisés → Ajouter
3. Nom : Désactiver effets
4. Commande : `/chemin/vers/disable-effects.sh`
5. Raccourci : `Super+F10` (par exemple)

---

## Dépannage

### Les effets ne fonctionnent pas

**Solutions :**

1. **Vérifier que le compositeur est activé**
```bash
gsettings get org.cinnamon.desktop.wm.preferences compositing-manager
```
Doit retourner `true`

2. **Vérifier les pilotes graphiques**
```bash
sudo ubuntu-drivers devices
```
Installez les pilotes recommandés

3. **Redémarrer Cinnamon**
- `Alt+F2` → tapez `r` → Entrée

4. **Vérifier les extensions conflictuelles**
- Désactivez toutes les extensions
- Réactivez-les une par une

### Scintillement ou artefacts visuels

**Solutions :**

1. **Désactiver VSync (ou l'activer)**
```bash
# Dans dconf-editor
org.cinnamon.muffin → unredirect-fullscreen-windows
```

2. **Changer le backend graphique (Picom)**
```conf
backend = "xrender";  # Au lieu de "glx"
```

3. **Mettre à jour les pilotes**

4. **Réduire les effets**

### Bureau lent avec effets activés

**Solutions :**

1. **Réduire la complexité**
- Désactivez Desktop Cube
- Désactivez Wobbly Windows
- Limitez les ombres

2. **Augmenter la vitesse des animations**
- Transitions plus rapides = moins de lag perçu

3. **Fermer les applications inutiles**
- Libère des ressources GPU/CPU

4. **Vérifier la température**
```bash
sensors
```
Si surchauffe → nettoyer ventilateurs

### Les ombres sont bizarres

**Solutions :**

1. **Ajuster les paramètres d'ombre**
- Réduire le rayon
- Changer l'offset
- Modifier l'opacité

2. **Changer de thème**
- Certains thèmes ont de meilleures ombres

3. **Éditer la configuration Picom**
```conf
shadow-exclude = [
  "class_g = 'Conky'",
  "class_g ?= 'Notify-osd'"
];
```

### Transparence ne fonctionne pas

**Solutions :**

1. **Vérifier le compositeur**
- Doit être activé

2. **Vérifier la profondeur de couleur**
```bash
xdpyinfo | grep depth
```
Doit être 24 ou 32

3. **Installer/configurer Picom**
```bash
sudo apt install picom
```

---

## Configurations recommandées par usage

### Configuration "Gamer"

**Objectif :** Performances maximales en jeu

```
Effets : Désactivés pendant le jeu
Animations : Aucune
Compositeur : Désactivé (Alt+Maj+F12)
Ombres : Non
Transparence : Non
```

**Script de lancement de jeu :**
```bash
#!/bin/bash
# Désactiver effets
gsettings set org.cinnamon.desktop.wm.preferences compositing-manager false

# Lancer le jeu
steam steam://rungameid/123456

# Réactiver après fermeture
gsettings set org.cinnamon.desktop.wm.preferences compositing-manager true
```

### Configuration "Productivité"

**Objectif :** Équilibre beauté/performance

```
Effets : Modérés
Animations : Rapides et subtiles
Vitesse : Rapide
Ombres : Légères (rayon : 8)
Transparence : Panneau uniquement (95%)
Extensions : Aucune gourmande
```

### Configuration "Showoff" (démonstration)

**Objectif :** Impressionner visuellement

```
Effets : Tous
Animations : Toutes + personnalisées
Vitesse : Moyenne (pour voir les animations)
Ombres : Importantes (rayon : 15)
Transparence : Partout (80-90%)
Extensions : Desktop Cube, Burn My Windows, Wobbly
Compositeur : Picom avec flou
```

### Configuration "Minimaliste"

**Objectif :** Sobre et efficace

```
Effets : Basiques uniquement
Animations : Fondu simple
Vitesse : Rapide
Ombres : Discrètes (rayon : 5)
Transparence : Aucune
Extensions : Aucune visuelle
```

---

## Animations et accessibilité

### Réduire les mouvements (motion sickness)

Certaines personnes sont sensibles aux animations.

**Désactiver toutes les animations :**

1. Menu → Préférences → Effets
2. Décochez "Activer les effets"

Ou :
```bash
gsettings set org.cinnamon enable-animations false
```

**Préférer les fondus aux échelles :**
- Les fondus sont moins "agressifs"
- Évitez les zooms et rotations

### Animations pour malvoyants

**Augmenter la durée :**
- Animations plus lentes = plus faciles à suivre

**Augmenter le contraste :**
- Effets bien visibles
- Pas de transparence excessive

**Feedback visuel prononcé :**
- Ombres marquées
- Couleurs contrastées au survol

---

## Thèmes et effets

Certains thèmes incluent des animations personnalisées.

### Thèmes avec effets intégrés

**1. Arc Theme**
- Animations subtiles
- Ombres élégantes
- Transitions douces

**2. Adapta**
- Design Material
- Animations fluides
- Effets de vague (ripple)

**3. Materia**
- Inspiré de Material Design
- Animations modernes
- Effets tactiles

### Créer un thème avec animations personnalisées

**Éditer le CSS :**

```bash
# Copier un thème existant
cp -r /usr/share/themes/MonTheme ~/.themes/MonThemePerso

# Éditer le CSS
nano ~/.themes/MonThemePerso/cinnamon/cinnamon.css
```

**Ajouter des animations :**

```css
/* Animation au survol des boutons */
.button {
    transition-duration: 200ms;
    transition-property: background-color, color;
}

.button:hover {
    background-color: #5294E2;
    color: white;
}

/* Animation des menus */
.popup-menu {
    transition-duration: 150ms;
    transition-property: opacity;
}

/* Animation de l'applet au survol */
.applet-box:hover {
    transition-duration: 100ms;
    background-color: rgba(255, 255, 255, 0.1);
}
```

---

## Effets expérimentaux

### Wayland et effets

Wayland (successeur de X11) offre de meilleures performances pour les effets.

**Tester Wayland sur Cinnamon (expérimental) :**

À la connexion, sélectionnez "Cinnamon (Wayland)" si disponible.

**Avantages :**
- Meilleure gestion des effets
- Vsync natif
- Moins de tearing

**Inconvénients :**
- Support incomplet
- Certaines applications incompatibles
- Moins stable

### HDR et effets

Le support HDR arrive progressivement sur Linux.

**État actuel :**
- Support limité
- Principalement pour les jeux
- Pas encore dans Cinnamon de base

---

## Ressources et inspiration

### Galeries de configurations

**Reddit :**
- r/unixporn - Configurations visuelles
- r/linux - Discussions générales

**YouTube :**
- Recherchez "Cinnamon desktop effects"
- Tutoriels vidéo sur Compiz

**Forums :**
- Linux Mint Forums - Section Customization

### Outils de capture pour montrer vos effets

**SimpleScreenRecorder :**
```bash
sudo apt install simplescreenrecorder
```

**Peek (GIF animés) :**
```bash
sudo apt install peek
```

**OBS Studio (streaming/enregistrement) :**
```bash
sudo apt install obs-studio
```

---

## Aller plus loin

### Combiner avec Conky

- Conky peut avoir ses propres effets
- Transparence, ombres
- Voir chapitre 16.4

### Scripts d'animation

**Zenity pour animations de dialogues :**
```bash
zenity --progress --text="Chargement..." --pulsate --auto-close
```

**Notify-send pour notifications animées :**
```bash
notify-send -u critical "Titre" "Message" -t 5000
```

### Développer ses propres extensions

- JavaScript pour Cinnamon
- Ajoutez vos animations personnalisées
- Documentation : [Cinnamon Tutorials](https://projects.linuxmint.com/reference/git/cinnamon-tutorials/)

---

## Résumé

Dans ce chapitre, vous avez appris :

- ✅ Ce que sont les animations et effets visuels
- ✅ Comment accéder aux paramètres d'effets sur Cinnamon, MATE et Xfce
- ✅ Configurer les animations de fenêtres, ombres et transparence
- ✅ Installer et utiliser des extensions d'effets (Desktop Cube, Burn My Windows)
- ✅ Gérer le compositeur pour optimiser les performances
- ✅ Configurer les effets selon votre matériel
- ✅ Créer des profils de performance
- ✅ Résoudre les problèmes courants
- ✅ Des configurations complètes pour différents usages
- ✅ L'importance de l'accessibilité dans les animations

Les animations et effets visuels sont une question d'équilibre : assez pour rendre votre bureau agréable, pas trop pour ne pas ralentir votre système. Expérimentez pour trouver la configuration parfaite qui allie beauté et performance !

---


⏭️ [Grub Customizer (personnaliser le boot)](/16-personnalisation-avancee/08-grub-customizer.md)
