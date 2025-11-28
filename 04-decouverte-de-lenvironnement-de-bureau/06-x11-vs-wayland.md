🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.6 X11 vs Wayland (session expérimentale Wayland)

## Introduction

Lorsque vous utilisez Linux Mint, vous voyez votre bureau, vos fenêtres, vos applications qui s'affichent à l'écran. Mais en coulisses, un composant essentiel fait fonctionner tout cela : le **serveur d'affichage** (ou serveur graphique).

Actuellement, il existe deux technologies principales pour gérer l'affichage sous Linux :
- **X11** (aussi appelé X.Org ou simplement X) - la technologie historique et actuelle
- **Wayland** - la technologie moderne et future

Dans ce chapitre, nous allons découvrir ces deux technologies, comprendre leurs différences, et savoir laquelle choisir selon vos besoins.

## Qu'est-ce qu'un serveur d'affichage ?

### Explication simple

Imaginez un **chef d'orchestre** qui coordonne tous les musiciens (vos applications) pour produire une symphonie cohérente (votre interface graphique).

**Le serveur d'affichage fait ceci :**
- Reçoit les instructions des applications ("je veux afficher un bouton ici")
- Gère l'affichage sur votre écran
- Transmet les actions de votre souris et clavier aux bonnes applications
- Coordonne le positionnement et l'apparence des fenêtres
- Gère les effets visuels (transparence, animations, etc.)

**Sans serveur d'affichage :**
- Pas d'interface graphique, seulement du texte (mode console)
- Comme un ordinateur des années 1970-1980

**Analogie du restaurant :**
- **Applications** = Cuisiniers qui préparent des plats
- **Serveur d'affichage** = Serveur qui prend les commandes et apporte les plats
- **Écran** = Table où sont servis les plats
- **Vous** = Le client

Le serveur d'affichage est invisible mais indispensable pour que tout fonctionne harmonieusement.

## X11 (X.Org) - Le vétéran

### Histoire et contexte

**X11** (ou X Window System version 11) existe depuis **1987** !

**Points historiques :**
- Créé au MIT (Massachusetts Institute of Technology)
- Conception pour les systèmes Unix
- A survécu à plusieurs décennies et évolutions technologiques
- Standard de facto sous Linux jusqu'à récemment

**Pourquoi "11" ?**
- C'est la version 11 du protocole X Window
- Inchangé dans sa base depuis plus de 35 ans
- Les mises à jour concernent surtout l'implémentation (X.Org)

### Comment fonctionne X11 ?

**Architecture client-serveur :**

```
[Application] ←→ [Serveur X11] ←→ [Écran + Périphériques]
                      ↓
            [Gestionnaire de fenêtres]
```

**Composants :**

**Le serveur X** :
- Contrôle l'écran, la souris, le clavier
- Dessine les pixels
- Gère la mémoire graphique

**Les clients X** :
- Vos applications (Firefox, LibreOffice, etc.)
- Demandent au serveur d'afficher des choses
- Reçoivent les événements (clics, frappes)

**Le gestionnaire de fenêtres** :
- Muffin (sous Cinnamon)
- Gère le placement, la décoration des fenêtres
- Les effets visuels

**Le gestionnaire de composition** :
- Ajoute les effets (ombres, transparence, animations)
- Souvent intégré au gestionnaire de fenêtres moderne

### Avantages de X11

**1. Maturité et stabilité**
- Plus de 35 ans de développement
- Bugs corrigés depuis longtemps
- Fiabilité éprouvée

**2. Compatibilité excellente**
- Pratiquement tous les logiciels Linux supportent X11
- Applications historiques et récentes
- Pas de surprise, tout fonctionne

**3. Fonctionnalités réseau**
- Peut afficher des applications distantes
- X forwarding via SSH
- Utile pour administration de serveurs

**4. Flexibilité**
- Très personnalisable
- Extensions nombreuses
- Outils matures (xrandr, xinput, etc.)

**5. Outils et diagnostic**
- Énormément d'outils disponibles
- Documentation abondante
- Communauté qui connaît bien

**6. Support matériel**
- Fonctionne avec quasiment tout matériel
- Pilotes matures
- Même vieux matériel supporté

### Inconvénients de X11

**1. Architecture datée**
- Conçu pour les années 1980-1990
- Pas adapté au matériel moderne
- Code complexe et ancien

**2. Sécurité limitée**
- Applications peuvent "espionner" les autres
- Enregistrement de frappe possible entre applications
- Isolation faible

**3. Performance**
- Latence d'affichage
- Utilise plus de ressources que nécessaire
- Chemin indirect pour l'affichage

**4. Gestion moderne difficile**
- Multi-écrans compliqué
- Support HiDPI (écrans haute résolution) imparfait
- Écrans avec différents DPI = problématique

**5. Complexité**
- Beaucoup de code ancien
- Difficile à maintenir et améliorer
- Nombreuses extensions qui se chevauchent

**6. Tearing (déchirement d'image)**
- Sans composition, peut y avoir du tearing
- Surtout visible en vidéo et jeux
- Nécessite configuration pour éviter

## Wayland - L'avenir

### Histoire et contexte

**Wayland** est un projet plus récent, démarré en **2008**.

**Philosophie :**
- "Repartir de zéro avec les connaissances actuelles"
- Architecture moderne pour matériel moderne
- Simplicité et sécurité au cœur du design

**Créateurs :**
- Kristian Høgsberg et contributeurs
- Anciens développeurs de X11
- Connaissance des problèmes à résoudre

**Adoption progressive :**
- Fedora : Wayland par défaut depuis 2016 (GNOME)
- Ubuntu : Wayland par défaut depuis 2021 (GNOME)
- KDE Plasma : Wayland stable depuis quelques années
- Cinnamon : en cours de développement (expérimental)

### Comment fonctionne Wayland ?

**Architecture simplifiée :**

```
[Application] ←→ [Compositeur Wayland] ←→ [Écran + Périphériques]
```

**La grande différence :**
Wayland **fusionne** le serveur d'affichage et le compositeur en un seul composant.

**Avantages de cette fusion :**
- Moins de composants = moins de complexité
- Communication plus directe
- Moins de latence
- Plus performant

**Le compositeur Wayland** :
- Gère TOUT : affichage, fenêtres, composition
- Muffin pour Cinnamon (version Wayland en développement)
- Mutter pour GNOME
- KWin pour KDE

**Protocole vs Implémentation :**
- **Wayland** = le protocole (les règles de communication)
- **Les compositeurs** = les implémentations (Mutter, KWin, etc.)

### Avantages de Wayland

**1. Architecture moderne**
- Conçu pour le matériel actuel
- Moins de code = moins de bugs potentiels
- Plus simple à comprendre et maintenir

**2. Performance**
- Communication directe entre application et compositeur
- Moins de latence
- Affichage plus fluide
- Meilleure gestion des ressources

**3. Sécurité**
- Isolation entre applications
- Une application ne peut pas espionner une autre
- Capture d'écran contrôlée (permission explicite)
- Enregistrement de frappe impossible entre apps

**4. Expérience utilisateur**
- Pas de tearing par conception
- Animations plus fluides
- Meilleure gestion tactile
- Support gestes natif

**5. Support multi-écrans**
- Meilleure gestion des écrans multiples
- Différents DPI (résolutions) par écran
- Configuration plus simple
- Branchement à chaud plus fiable

**6. Support HiDPI**
- Écrans haute résolution (4K, 5K, Retina)
- Mise à l'échelle fractionnelle
- Interface nette sur tous les écrans

**7. Économie d'énergie**
- Optimisations pour laptops
- Meilleure gestion de l'affichage
- Consommation réduite

### Inconvénients de Wayland

**1. Jeunesse relative**
- Moins mature que X11
- Certains bugs encore présents
- Évolution continue

**2. Compatibilité applicative**
- Certaines vieilles applications ne fonctionnent pas
- Nécessite XWayland pour apps X11
- Couche de compatibilité = overhead

**3. Fonctionnalités manquantes**
- Pas (encore) de réseau natif (affichage distant)
- Certains outils X11 n'ont pas d'équivalent
- Accessibilité en retard (lecteurs d'écran)

**4. Support matériel**
- NVIDIA : support longtemps problématique (mieux maintenant)
- Vieux matériel peut avoir des soucis
- Certains pilotes propriétaires en retard

**5. Personnalisation limitée**
- Moins d'outils de customisation
- Certaines configurations X11 impossibles
- Dépend du compositeur

**6. Écosystème en transition**
- Tous les logiciels ne sont pas optimisés
- Documentation parfois incomplète
- Changements fréquents

## X11 vs Wayland : Comparaison directe

### Tableau récapitulatif

| Critère | X11 | Wayland |
|---------|-----|---------|
| **Maturité** | ⭐⭐⭐⭐⭐ 35+ ans | ⭐⭐⭐ ~15 ans |
| **Performance** | ⭐⭐⭐ Correcte | ⭐⭐⭐⭐⭐ Excellente |
| **Sécurité** | ⭐⭐ Faible | ⭐⭐⭐⭐⭐ Forte |
| **Compatibilité apps** | ⭐⭐⭐⭐⭐ Totale | ⭐⭐⭐⭐ Très bonne (via XWayland) |
| **Multi-écrans** | ⭐⭐⭐ Compliqué | ⭐⭐⭐⭐⭐ Excellent |
| **HiDPI** | ⭐⭐ Problématique | ⭐⭐⭐⭐⭐ Natif |
| **Tearing** | ⭐⭐ Possible | ⭐⭐⭐⭐⭐ Aucun |
| **Outils** | ⭐⭐⭐⭐⭐ Nombreux | ⭐⭐⭐ En développement |
| **Documentation** | ⭐⭐⭐⭐⭐ Abondante | ⭐⭐⭐ Croissante |
| **Support NVIDIA** | ⭐⭐⭐⭐⭐ Parfait | ⭐⭐⭐⭐ Bon (s'améliore) |

### Cas d'usage recommandés

**Utilisez X11 si :**
- Vous avez du matériel ancien (plus de 8-10 ans)
- Vous utilisez une carte NVIDIA ancienne
- Vous avez besoin d'applications X11 spécifiques qui ne marchent pas sous Wayland
- Vous utilisez des outils de contrôle à distance (VNC, etc.)
- Vous utilisez des technologies d'accessibilité avancées
- Vous voulez la stabilité maximale sans surprises
- Vous personnalisez beaucoup avec des outils X11 spécifiques

**Utilisez Wayland si :**
- Vous avez du matériel récent (moins de 5 ans)
- Vous avez un écran HiDPI (4K, haute résolution)
- Vous utilisez plusieurs écrans
- Vous voulez les meilleures performances
- Vous utilisez un laptop et voulez optimiser la batterie
- Vous voulez l'affichage le plus fluide possible
- Vous jouez à des jeux (moins de tearing)
- La sécurité est importante pour vous

## Wayland dans Linux Mint Cinnamon

### État actuel

**Linux Mint 21.x et antérieurs :**
- X11 **par défaut** et recommandé
- Wayland non disponible

**Linux Mint 22+ (Virginia) :**
- X11 toujours **par défaut**
- Wayland disponible en **expérimental**
- Session Wayland sélectionnable à la connexion

**Pourquoi X11 reste par défaut ?**
L'équipe Linux Mint privilégie :
- **Stabilité avant tout**
- Compatibilité maximale
- Transition en douceur
- Attendre que Wayland soit vraiment mature pour Cinnamon

**Philosophie Linux Mint :**
"Ne cassez pas ce qui fonctionne bien. Adoptez les nouvelles technologies quand elles sont réellement meilleures et stables."

### Support de Wayland dans Cinnamon

**Développement en cours :**
- Cinnamon a commencé le portage vers Wayland
- Sessions expérimentales disponibles
- Mais pas encore recommandé pour production

**Limitations actuelles (peuvent évoluer) :**
- Certaines fonctionnalités Cinnamon manquantes
- Applets et desklets peuvent ne pas fonctionner
- Extensions à adapter
- Bugs possibles

**Comparaison avec d'autres DE :**
- **GNOME** : Wayland mature et par défaut
- **KDE Plasma** : Wayland très avancé
- **Cinnamon** : En développement actif
- **MATE/Xfce** : Pas de support Wayland prévu

### Comment tester Wayland

**Prérequis :**
- Linux Mint 22 ou supérieur
- Sauvegarde de vos données (précaution)
- Temps pour tester et revenir à X11 si problème

**Procédure :**

**1. Installer la session Wayland** (si pas déjà fait)
```bash
sudo apt update
sudo apt install cinnamon-session-wayland
```

**2. Déconnectez-vous**
- Menu → Déconnexion

**3. À l'écran de connexion**
- Cliquez sur votre nom d'utilisateur
- **Avant** d'entrer le mot de passe, cherchez une icône d'engrenage ou "Session"
- Sélectionnez "Cinnamon (Wayland)" au lieu de "Cinnamon" (X11)
- Entrez votre mot de passe et connectez-vous

**4. Vérifiez que vous êtes sur Wayland**
Ouvrez un terminal et tapez :
```bash
echo $XDG_SESSION_TYPE
```
- Réponse attendue : `wayland`
- Si réponse : `x11`, vous êtes encore sur X11

**Ou vérifiez avec :**
```bash
loginctl show-session $(loginctl | grep $(whoami) | awk '{print $1}') -p Type
```

**5. Testez votre utilisation habituelle**
- Ouvrez vos applications courantes
- Testez vos applets et extensions
- Vérifiez la fluidité
- Notez les problèmes éventuels

**6. Pour revenir à X11**
- Déconnectez-vous
- À l'écran de connexion, sélectionnez "Cinnamon" (sans Wayland)
- Connectez-vous

**Astuce :** La session par défaut est celle que vous sélectionnez. Pas besoin de changer à chaque fois.

## XWayland : Le pont entre deux mondes

### Qu'est-ce que XWayland ?

**Problème :**
- Wayland est nouveau
- Des milliers d'applications utilisent X11
- Comment les faire fonctionner sous Wayland ?

**Solution : XWayland**
- Serveur X11 qui fonctionne **à l'intérieur** de Wayland
- Permet aux applications X11 de tourner sous Wayland
- Transparent pour l'utilisateur

**Analogie :**
- Wayland = Nouveau pays avec nouvelles règles
- XWayland = Ambassade de l'ancien pays dans le nouveau
- Applications X11 = Citoyens de l'ancien pays qui peuvent visiter

### Comment ça fonctionne ?

**Architecture :**
```
[Application X11] ←→ [XWayland] ←→ [Compositeur Wayland] ←→ [Écran]
```

**Processus :**
1. Application X11 pense qu'elle parle à un serveur X normal
2. XWayland traduit pour Wayland
3. Le compositeur Wayland affiche
4. L'utilisateur ne voit aucune différence

### Applications natives vs XWayland

**Application native Wayland :**
- Communique directement avec le compositeur
- Performance maximale
- Toutes les fonctionnalités Wayland

**Application via XWayland :**
- Passe par une couche de traduction
- Petit overhead de performance (négligeable)
- Certaines fonctionnalités Wayland non accessibles

**Comment savoir ?**
Sous GNOME/KDE, des outils permettent de voir. Sous Cinnamon expérimental, c'est moins évident.

**Exemples :**
- **Natif Wayland** : Firefox récent, GNOME apps, certaines apps Qt
- **Via XWayland** : LibreOffice, GIMP, beaucoup d'apps classiques

**Bonne nouvelle :** Ça fonctionne transparemment ! Vous n'avez généralement pas à vous en soucier.

## Problèmes courants et solutions

### Sous Wayland

**Problème : Écran noir au démarrage**

**Causes possibles :**
- Pilote graphique incompatible
- NVIDIA avec vieux pilote
- Matériel non supporté

**Solutions :**
1. Redémarrez et sélectionnez session X11
2. Mettez à jour vos pilotes :
   ```bash
   sudo ubuntu-drivers autoinstall
   ```
3. Pour NVIDIA, vérifiez que le pilote supporte Wayland

**Problème : Applets/Extensions ne fonctionnent pas**

**Cause :**
- Pas toutes compatibles Wayland encore

**Solution :**
1. Vérifiez les paramètres de l'applet
2. Cherchez une version Wayland
3. Ou restez sur X11 si essentiel

**Problème : Partage d'écran ne fonctionne pas**

**Dans certaines applications :**
- Zoom, Teams, Discord peuvent avoir des soucis

**Solutions :**
1. Utilisez Firefox pour visioconférence (meilleur support Wayland)
2. Ou utilisez X11 pour ces applications spécifiques
3. Vérifiez les permissions de portail (pipewire)

**Problème : Performance pire que X11**

**Rare, mais possible :**
- Matériel spécifique
- Pilote pas optimisé

**Solutions :**
1. Mettez à jour le système
2. Vérifiez le pilote graphique
3. Signalez le bug si c'est récent
4. Restez sur X11 en attendant

### Sous X11

**Problème : Tearing (déchirement) en vidéo**

**Causes :**
- Pas de composition
- Configuration GPU

**Solutions :**
1. Activez le compositeur :
   - Paramètres système → Effets
   - Activez les effets
2. Ou forcez VSync dans les paramètres de pilote

**Problème : Multi-écrans compliqué**

**Configuration difficile :**
- Différentes résolutions
- Différents DPI

**Solutions :**
1. Utilisez l'outil graphique : Affichage
2. Ou xrandr en ligne de commande
3. Envisagez Wayland pour facilité

**Problème : Mise à l'échelle HiDPI**

**Interface trop petite ou applications floues :**

**Solutions :**
1. Paramètres système → Polices → Facteur d'agrandissement
2. Réglez entre 1.0 et 2.0
3. Ou passez à Wayland pour meilleur support

## Quelle session choisir ?

### Pour les débutants

**Recommandation : Restez sur X11**

**Pourquoi ?**
- Par défaut dans Linux Mint
- Stable et fiable
- Tous les tutoriels supposent X11
- Dépannage plus facile
- Documentation abondante

**Quand envisager Wayland ?**
- Vous êtes curieux et à l'aise avec l'informatique
- Vous avez du matériel récent
- Vous rencontrez des problèmes spécifiques que Wayland résout

### Pour les utilisateurs intermédiaires

**Testez Wayland si :**
- Problèmes de tearing sous X11
- Multi-écrans problématiques
- Écran HiDPI (4K, etc.)
- Vous voulez la meilleure performance

**Restez sur X11 si :**
- Tout fonctionne bien
- Vous utilisez des outils spécifiques X11
- Applications critiques incompatibles
- Vous préférez la stabilité éprouvée

### Pour les utilisateurs avancés

**Explorez les deux :**
- Comparez les performances
- Testez vos workflows
- Contribuez aux rapports de bugs
- Préparez-vous pour la transition future

**Critères de décision :**
- Compatibilité de vos outils
- Performance sur votre matériel
- Besoins spécifiques (accessibilité, remote, etc.)
- Tolérance aux bugs occasionnels

## L'avenir : Transition vers Wayland

### Tendances de l'écosystème

**Distributions majeures :**
- Fedora, Ubuntu (GNOME) : Wayland par défaut
- Fedora KDE : Wayland par défaut
- Debian : Transition en cours
- Arch : Choix à l'installation

**Linux Mint :**
- Approche conservatrice
- Transition quand Wayland sera vraiment prêt pour Cinnamon
- Probablement quelques années encore

**Prédiction :**
- X11 restera supporté encore 5-10 ans minimum
- Wayland deviendra le standard progressivement
- Période de coexistence longue

### Développement de Wayland pour Cinnamon

**Progrès actuels :**
- Session Wayland expérimentale disponible
- Développement actif
- Améliorations à chaque version

**Défis :**
- Adapter toutes les fonctionnalités Cinnamon
- Assurer compatibilité des applets et desklets
- Tester sur multiples configurations matérielles
- Maintenir la stabilité légendaire de Mint

**Objectif :**
- Wayland stable et complet pour Cinnamon
- Transition transparente pour utilisateurs
- Conserver tous les avantages de Cinnamon

## Mythes et réalités

### Mythes courants

**Mythe 1 : "X11 va disparaître demain"**
- **Réalité** : X11 sera maintenu pendant des années
- Support à long terme garanti
- Transition progressive

**Mythe 2 : "Wayland est instable"**
- **Réalité** : Stable sur GNOME/KDE depuis des années
- Dépend du compositeur
- Cinnamon en développement, d'autres matures

**Mythe 3 : "Toutes mes applications X11 ne marcheront plus"**
- **Réalité** : XWayland assure la compatibilité
- Transition transparente
- Très peu d'applications vraiment incompatibles

**Mythe 4 : "Wayland est toujours plus rapide"**
- **Réalité** : Généralement oui, mais pas toujours
- Dépend du matériel et du compositeur
- Testez sur votre machine

**Mythe 5 : "Je dois choisir maintenant"**
- **Réalité** : Vous pouvez basculer à tout moment
- Les deux coexistent
- Pas de décision définitive

### Réalités importantes

**1. La transition prend du temps**
- Écosystème Linux vaste et complexe
- Changement majeur nécessite prudence
- Progressivité garantit stabilité

**2. Pas de "meilleur" absolu**
- Dépend de vos besoins
- De votre matériel
- De vos applications

**3. Linux Mint fait les bons choix**
- Stabilité d'abord
- Transition quand c'est prêt
- Faites confiance à l'équipe

## Ressources et documentation

### Pour en savoir plus

**Sites officiels :**
- Wayland : https://wayland.freedesktop.org/
- X.Org : https://www.x.org/

**Documentations Linux Mint :**
- Blog Linux Mint : annonces sur Wayland
- Forums : discussions et retours utilisateurs

**Tests et benchmarks :**
- Phoronix : comparaisons régulières X11 vs Wayland
- Gaming on Linux : impact sur les jeux

### Communauté

**Forums Linux Mint :**
- Section dédiée Wayland
- Rapports de bugs
- Partage d'expériences

**Reddit :**
- r/linuxmint
- r/wayland
- Discussions et actualités

**Groupes utilisateurs :**
- Discord Linux Mint (si existant)
- Telegram
- IRC

## Conclusion

X11 et Wayland représentent deux générations de technologie d'affichage sous Linux. X11, le vétéran fiable, continue de servir admirablement la majorité des utilisateurs. Wayland, la relève moderne, apporte des améliorations significatives mais nécessite encore du temps pour atteindre la maturité complète, en particulier pour Cinnamon.

**Points clés à retenir :**

**X11 :**
- Technologie mature et stable (35+ ans)
- Compatibilité totale avec toutes les applications
- Recommandé actuellement pour Linux Mint
- Restera supporté pendant de nombreuses années

**Wayland :**
- Technologie moderne et performante (~15 ans)
- Architecture simplifiée et sécurisée
- Meilleur pour multi-écrans et HiDPI
- Expérimental sous Cinnamon, testez si curieux

**Recommandation générale :**
- **Débutants** : Restez sur X11 (par défaut)
- **Curieux** : Testez Wayland, mais gardez X11 comme solution de repli
- **Avancés** : Évaluez selon vos besoins spécifiques

**L'essentiel :**
Vous n'avez pas besoin de vous préoccuper de ce sujet pour l'instant ! Linux Mint fonctionne parfaitement avec X11, et lorsque Wayland sera prêt et stable pour Cinnamon, la transition se fera naturellement et sans douleur.

Concentrez-vous sur l'utilisation de votre système, et laissez l'équipe Linux Mint gérer ces aspects techniques en coulisses. C'est exactement la philosophie qui rend Linux Mint si agréable à utiliser !

Dans le prochain chapitre, nous découvrirons comment personnaliser votre bureau pour qu'il corresponde exactement à vos goûts et besoins.

---

**Prochaine étape :** Personnalisation de base

⏭️ [Personnalisation de base](/04-decouverte-de-lenvironnement-de-bureau/07-personnalisation-de-base.md)
