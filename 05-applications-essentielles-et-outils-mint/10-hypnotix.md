🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10 Hypnotix (Lecteur IPTV pour la TV par Internet)

## Introduction

**Hypnotix** est une application développée par l'équipe de Linux Mint pour regarder la télévision par Internet (IPTV). Elle permet d'accéder à des chaînes TV du monde entier directement depuis votre ordinateur, sans antenne ni décodeur, uniquement avec une connexion Internet.

## Qu'est-ce que l'IPTV ?

### Définition

**IPTV** signifie **Internet Protocol Television** (Télévision par Protocole Internet).

**Principe** :
- Les chaînes TV sont diffusées via Internet
- Vous regardez en streaming (flux continu)
- Pas besoin d'antenne satellite ou TNT
- Juste une connexion Internet

**Analogie** :
C'est comme Netflix ou YouTube, mais pour les chaînes de télévision traditionnelles et en direct.

### Différence avec services de streaming classiques

**IPTV** :
- Chaînes en direct (live)
- Programmation TV classique
- Gratuit ou payant selon la source
- Contenu variable

**Netflix / Prime Video** :
- Contenu à la demande (VOD)
- Catalogue fixe
- Toujours payant
- Qualité garantie

**YouTube** :
- Contenu créateurs
- Pas de programmation TV
- Gratuit (avec publicités)

### Types d'IPTV

**IPTV Légal** :
- **Fournisseurs officiels** : Free, Orange, SFR (box Internet)
- **Chaînes publiques** : France Télévisions, Arte, TV5Monde
- **Services payants légaux** : Molotov TV, myCANAL
- **Radios** : Nombreuses radios en streaming

**IPTV Illégal** :
- Abonnements pirates à bas prix
- Redistribution non autorisée
- Qualité variable et instable
- **Risques légaux** pour l'utilisateur

**Important** : Ce tutoriel se concentre uniquement sur l'IPTV **légal**.

## Hypnotix - Présentation

### Qu'est-ce qu'Hypnotix ?

**Hypnotix** est le lecteur IPTV officiel de Linux Mint.

**Caractéristiques** :
- **Simple** : Interface intuitive
- **Gratuit** : Open source, aucun coût
- **Compatible** : Formats M3U, M3U8
- **Organisé** : Favoris, groupes, recherche
- **Intégré** : Préinstallé sur Linux Mint

**Formats supportés** :
- **M3U** : Liste de lecture de chaînes
- **M3U8** : Variante moderne (HLS)
- **URL directes** : Flux individuels

### Fonctionnalités

**Lecture de chaînes** :
- TV en direct
- Radios Internet
- Webcams publiques (selon source)

**Organisation** :
- Favoris personnalisés
- Groupes de chaînes (sport, actualités, etc.)
- Recherche rapide

**Providers** :
- Sources multiples
- Basculement facile entre sources
- Gestion centralisée

## Installation

### Sur Linux Mint

**Hypnotix est préinstallé** sur Linux Mint 20.2 et versions ultérieures.

**Vérifier la présence** :
1. Menu principal → **Son et vidéo** → **Hypnotix**
2. Si absent, installez-le

**Installation si nécessaire** :
```bash
sudo apt update  
sudo apt install hypnotix  
```

### Sur autres distributions

**Ubuntu et dérivés** :
```bash
sudo apt install hypnotix
```

**Flatpak** (universel) :
```bash
flatpak install flathub org.x.Hypnotix
```

## Premier lancement

### Ouvrir Hypnotix

**Depuis le menu** :
1. Menu principal → **Son et vidéo** → **Hypnotix**
2. Ou tapez "Hypnotix" dans la recherche

**L'application s'ouvre** :
- Interface sombre par défaut
- Barre latérale gauche (providers)
- Liste de chaînes au centre
- Lecteur vidéo à droite

### Configuration initiale

**Au premier lancement** :

1. **Aucune source par défaut** : Liste vide
2. Vous devez ajouter des **providers** (sources IPTV)
3. Un assistant peut apparaître selon la version

**Ne paniquez pas** si c'est vide, c'est normal !

## Interface de Hypnotix

### Vue d'ensemble

**Panneau de gauche** :
- **Providers** : Vos sources IPTV
- Bouton **+** pour ajouter
- Liste des providers existants

**Panneau central** :
- **Barre de recherche** en haut
- **Liste des chaînes** du provider sélectionné
- Groupes (Actualités, Sport, Films, etc.)
- Nom de la chaîne, logo

**Panneau de droite** :
- **Lecteur vidéo** : Affichage de la chaîne
- Contrôles de lecture
- Plein écran possible

**Barre d'outils** (en haut) :
- Favoris
- Paramètres
- À propos

### Navigation de base

**Sélectionner un provider** :
1. Cliquez sur un provider dans la liste de gauche
2. Les chaînes de ce provider s'affichent au centre

**Sélectionner une chaîne** :
1. Cliquez sur une chaîne dans la liste centrale
2. La lecture démarre automatiquement à droite

**Rechercher une chaîne** :
1. Tapez dans la barre de recherche
2. Les résultats se filtrent en temps réel
3. Exemple : Tapez "France" pour voir France 2, France 3, etc.

**Groupes de chaînes** :
- Les chaînes sont souvent organisées par catégorie
- Cliquez sur un groupe pour filtrer
- Exemples : Sport, News, Entertainment

## Ajouter des sources IPTV (Providers)

### Qu'est-ce qu'un provider ?

Un **provider** est une source de chaînes IPTV, généralement sous forme de :
- **Fichier M3U** : Liste de lecture téléchargeable
- **URL M3U** : Lien vers une liste en ligne
- **Fichier local** : M3U sur votre disque

### Ajouter un provider

**Méthode graphique** :

1. Cliquez sur le bouton **+** (Ajouter un provider) dans le panneau de gauche
2. Une fenêtre s'ouvre : **Nouveau provider**

**Champs à remplir** :

**Nom** :
- Nom de votre source
- Exemple : "Free IPTV", "Chaînes françaises", "Radios"

**Type** :
- **URL** : Lien vers un fichier M3U en ligne
- **Local File** : Fichier M3U sur votre ordinateur

**URL ou chemin** :
- Si URL : Collez l'URL complète
- Si fichier local : Parcourez et sélectionnez

**Username** et **Password** (optionnel) :
- Seulement si le provider nécessite authentification
- Généralement vide pour sources gratuites

3. Cliquez sur **OK**

**Hypnotix télécharge** :
- La liste de chaînes
- Les logos (si disponibles)
- Peut prendre quelques secondes

**Résultat** :
- Le nouveau provider apparaît dans la liste
- Les chaînes sont disponibles

### Exemples de providers gratuits et légaux

**IMPORTANT** : Utilisez uniquement des sources **légales**.

**Chaînes publiques françaises** :

**Free IPTV** (gratuit et légal) :
- URL : Recherchez "Free IPTV GitHub" pour listes à jour
- Contient : Chaînes gratuites internationales
- Qualité variable mais légal

**Radios françaises** :
- De nombreuses radios proposent des flux M3U
- Exemples : France Inter, RTL, Europe 1
- Cherchez sur leurs sites officiels

**Chaînes internationales gratuites** :
- BBC (certaines disponibles)
- Deutsche Welle
- Al Jazeera English
- France 24 (international)

**Listes communautaires** :
- GitHub héberge des listes M3U légales
- Recherchez "iptv-org/iptv" sur GitHub
- Liste mondiale de chaînes gratuites

**Exemple d'ajout** :

1. Provider : "IPTV Org"
2. Type : URL
3. URL : `https://iptv-org.github.io/iptv/index.m3u`
4. OK

**Attention** : Les URLs changent. Vérifiez toujours la source officielle.

### Ajouter un fichier M3U local

**Si vous avez un fichier M3U** :

1. Téléchargez ou créez le fichier `.m3u`
2. Enregistrez-le quelque part (ex: `~/Documents/ma-liste.m3u`)
3. Hypnotix → **+** → **Nouveau provider**
4. Type : **Local File**
5. Parcourez et sélectionnez votre fichier
6. OK

**Sources de fichiers M3U** :
- Sites de radios (listes de radios)
- Listes communautaires téléchargées
- Vos propres listes créées

### Mettre à jour un provider

**Actualiser la liste** :

1. Clic droit sur le provider
2. **Reload** ou **Actualiser**
3. Hypnotix retélécharge la liste

**Utile si** :
- La liste en ligne a changé
- Nouvelles chaînes ajoutées
- Correction de liens morts

### Supprimer un provider

**Retirer une source** :

1. Clic droit sur le provider
2. **Remove** ou **Supprimer**
3. Confirmez

**Résultat** :
- Provider et ses chaînes disparaissent
- Favoris de ce provider supprimés

## Regarder la télévision

### Lancer une chaîne

**Simple** :
1. Sélectionnez un provider (gauche)
2. Cliquez sur une chaîne (centre)
3. La lecture démarre automatiquement (droite)

**Changement rapide** :
- Cliquez sur une autre chaîne
- Basculement instantané (zapping)

### Contrôles de lecture

**Pendant la lecture** :

**Lecture/Pause** :
- Cliquez sur l'icône pause/play
- Ou `Espace`

**Volume** :
- Molette de la souris sur le lecteur
- Icône volume
- Raccourcis : `↑` `↓` (selon configuration)

**Muet** :
- Cliquez sur l'icône volume
- Ou `M`

**Plein écran** :
- Double-clic sur la vidéo
- Bouton plein écran
- Raccourci : `F` ou `F11`
- `Échap` pour quitter

### Qualité de la lecture

**Dépend de** :
- Votre connexion Internet (vitesse)
- La source IPTV (qualité du flux)
- Charge du serveur

**Si ça lag (saccade)** :
- Connexion trop lente
- Source saturée
- Essayez une autre chaîne
- Vérifiez votre débit Internet

**Qualité HD** :
- Certaines chaînes en 720p ou 1080p
- Nécessite bonne connexion (5+ Mbps)
- Pas toutes les chaînes gratuites sont HD

### Plein écran

**Mode immersif** :

1. Double-cliquez sur la vidéo
2. Ou bouton **Plein écran**

**En plein écran** :
- Vidéo occupe tout l'écran
- Bougez la souris → Contrôles apparaissent
- Cliquez sur une autre chaîne dans la liste (si visible)
- `Échap` pour quitter

**Conseil** : Idéal pour regarder depuis le canapé.

## Favoris

### Ajouter aux favoris

**Marquer vos chaînes préférées** :

**Méthode 1** :
1. Clic droit sur une chaîne
2. **Add to Favorites** ou **Ajouter aux favoris**

**Méthode 2** :
1. Sélectionnez la chaîne
2. Icône étoile ou cœur (selon interface)

**Résultat** :
- La chaîne est marquée comme favorite

### Voir les favoris

**Accéder rapidement** :

1. En haut, icône **Favoris** (étoile ou cœur)
2. Ou onglet **Favorites**
3. Toutes vos chaînes favorites s'affichent

**Avantage** :
- Accès rapide à vos chaînes habituelles
- Pas besoin de chercher à chaque fois
- Toutes sources confondues

### Retirer des favoris

**Supprimer une chaîne des favoris** :

1. Clic droit sur la chaîne (dans favoris ou liste normale)
2. **Remove from Favorites** ou **Retirer des favoris**

**Ou** :
- Cliquez à nouveau sur l'icône étoile/cœur

## Paramètres et options

### Accéder aux paramètres

**Menu Paramètres** :
1. Icône engrenage (en haut)
2. Ou menu **Preferences**

### Options disponibles

**Apparence** :
- **Thème** : Clair ou Sombre
- **Taille des icônes** : Petite, Moyenne, Grande

**Lecture** :
- **Lecteur par défaut** : MPV (par défaut), VLC, autre
- **Décodage matériel** : Active/Désactive (GPU)

**Réseau** :
- **User-Agent** : Identification navigateur
- **Timeout** : Délai avant erreur de connexion

**Interface** :
- **Langue** : Si disponible
- **Plein écran au démarrage** : Oui/Non

**Providers** :
- Gestion centralisée
- Activer/Désactiver sans supprimer

### Changer de lecteur vidéo

**MPV vs VLC** :

**MPV** (par défaut) :
- Léger et rapide
- Bonne compatibilité
- Recommandé

**VLC** (si installé) :
- Plus de formats
- Interface familière
- Alternative si MPV a des problèmes

**Changer** :
1. Paramètres → **Lecture**
2. **Lecteur** : Sélectionnez VLC
3. Relancez Hypnotix

## Créer sa propre liste M3U

### Format M3U basique

Un fichier M3U est un simple **fichier texte** avec des liens.

**Structure** :
```
#EXTM3U
#EXTINF:-1,Nom de la chaîne
http://example.com/stream.m3u8
#EXTINF:-1,Autre chaîne
http://example.com/stream2.m3u8
```

**Explication** :
- `#EXTM3U` : En-tête obligatoire (première ligne)
- `#EXTINF:-1,Nom` : Métadonnées de la chaîne
- URL : Lien du flux en dessous

### Créer manuellement

**Éditeur de texte** :

1. Ouvrez un éditeur de texte (gedit, xed, nano)
2. Tapez :
```
#EXTM3U
#EXTINF:-1,France 24 English
https://static.france24.com/live/F24_EN_LO_HLS/live_web.m3u8
#EXTINF:-1,Deutsche Welle
https://dwamdstream104.akamaized.net/hls/live/2015530/dwstream104/index.m3u8
```
3. Enregistrez sous `ma-liste.m3u` (extension importante)
4. Ajoutez ce fichier dans Hypnotix comme provider local

### Trouver des URLs de flux

**Sources légales** :

**Sites officiels de chaînes** :
- Certaines chaînes publient leurs URLs
- Cherchez "flux M3U8" ou "stream URL"
- Section développeurs ou API

**Listes GitHub** :
- [https://github.com/iptv-org/iptv](https://github.com/iptv-org/iptv)
- Liste mondiale collaborative
- Mise à jour régulière

**Radios** :
- La plupart des radios fournissent URL de stream
- Format souvent MP3 ou AAC

**Attention** :
- Vérifiez toujours la légalité
- Certaines URLs nécessitent autorisation
- Respectez les conditions d'utilisation

## Dépannage

### Chaîne ne se lance pas

**Problèmes courants** :

**Lien mort** :
- La source a changé d'URL
- Le flux n'existe plus
- Essayez de mettre à jour le provider

**Restriction géographique** :
- Certaines chaînes bloquent hors de leur pays
- Exemple : BBC iPlayer hors UK
- Solution : VPN (si légal dans votre cas)

**Format non supporté** :
- Rare avec MPV/VLC
- Essayez de changer de lecteur

**Connexion lente** :
- Flux HD nécessite débit suffisant
- Testez votre vitesse Internet
- Essayez une chaîne en SD

### Pas de son

**Vérifications** :

1. **Volume Hypnotix** : Vérifiez qu'il n'est pas muet
2. **Volume système** : Mixeur audio Linux Mint
3. **Sortie audio** : Bonne carte son sélectionnée
4. **Codec audio** : Certains flux ont formats exotiques

**Solution** :
- Changez de lecteur (VLC si MPV)
- Vérifiez avec une autre chaîne

### Image pixelisée ou saccadée

**Causes** :

**Bande passante insuffisante** :
- Votre connexion est trop lente
- Testez votre débit : [https://fast.com/](https://fast.com/)
- Fermez autres téléchargements

**Serveur surchargé** :
- Le serveur IPTV est saturé
- Normal aux heures de pointe
- Essayez plus tard

**Décodage matériel** :
- Activez dans les paramètres si désactivé
- Ou désactivez si ça cause des problèmes

### Hypnotix plante ou freeze

**Solutions** :

**Redémarrer** :
- Fermez Hypnotix complètement
- Relancez

**Réinitialiser configuration** :
```bash
rm -rf ~/.config/hypnotix
```
Puis relancez (configuration par défaut restaurée)

**Vérifier les logs** :
```bash
hypnotix --debug
```
Lance en mode debug, affiche erreurs dans le terminal

**Mettre à jour** :
```bash
sudo apt update  
sudo apt upgrade hypnotix  
```

### Provider ne charge pas

**Liste vide après ajout** :

**URL incorrecte** :
- Vérifiez l'URL (copier-coller complet)
- Testez l'URL dans un navigateur

**Format M3U invalide** :
- Le fichier M3U est mal formaté
- Vérifiez qu'il commence par `#EXTM3U`

**Connexion bloquée** :
- Pare-feu ou antivirus bloque Hypnotix
- Autorisez dans les paramètres réseau

## Légalité et éthique

### IPTV légal vs illégal

**IPTV Légal** :
- Chaînes publiques gratuites
- Services officiels payants (Molotov, etc.)
- Flux autorisés par les diffuseurs
- Radios Internet légales

**IPTV Illégal** :
- Redistribution non autorisée de chaînes payantes
- Abonnements pirates (€10/mois pour 1000 chaînes = suspect)
- Contenu piraté (films, séries récentes)
- Sans accord des ayants droits

**Risques de l'illégal** :
- **Amende** : Jusqu'à 300 000€ en France
- **Prison** : Jusqu'à 3 ans
- **Virus/Malware** : Sources douteuses infectées
- **Escroquerie** : Paiement pour service qui disparaît

### Comment savoir si c'est légal ?

**Questions à se poser** :

1. **Est-ce gratuit ?**
   - Si chaîne normalement payante (Canal+, beIN) mais gratuite → Suspect
   - Si chaîne publique gratuite (France 2) → OK

2. **D'où vient la source ?**
   - Site officiel de la chaîne → OK
   - Site inconnu avec "IPTV premium" → Suspect

3. **Y a-t-il un abonnement ridiculement bas ?**
   - 10€/mois pour 1000 chaînes → Illégal
   - 30€/mois service officiel (Molotov+) → Légal

4. **La qualité est-elle professionnelle ?**
   - Flux stables, légaux → Souvent légal
   - Qualité variable, liens qui meurent → Suspect

### Recommandations

**Pour rester dans la légalité** :

1. **Utilisez des sources officielles** :
   - Sites web des chaînes publiques
   - Applications officielles (Molotov, myCANAL)
   - Listes communautaires vérifiées (iptv-org)

2. **Payez pour le contenu premium** :
   - Si vous voulez Canal+, beIN → Abonnez-vous légalement
   - C'est moins cher que les amendes !

3. **Vérifiez la provenance** :
   - Listes GitHub : Généralement OK (chaînes gratuites)
   - Forums obscurs : Évitez

4. **Éduquez-vous** :
   - Renseignez-vous sur le droit d'auteur
   - En cas de doute : abstenez-vous

**Hypnotix lui-même est légal** :
- C'est juste un lecteur
- Comme VLC, il lit des flux
- C'est l'utilisation qui peut être illégale

## Alternatives à Hypnotix

### Autres lecteurs IPTV

**VLC Media Player** :
- Peut lire des listes M3U
- **Fichier** → **Ouvrir un flux réseau**
- Collez l'URL M3U8
- Moins pratique qu'Hypnotix mais fonctionne

**Kodi** :
- Centre multimédia complet
- Addons IPTV disponibles
- Plus complexe
- Installation : `sudo apt install kodi`

**FreetuxTV** :
- Ancien lecteur IPTV Linux
- Moins maintenu
- Hypnotix est meilleur

### Services en ligne

**Molotov TV** :
- Service français officiel
- Gratuit de base (chaînes TNT)
- Abonnements payants pour plus
- Application web et mobile
- Enregistrement cloud (payant)

**Pluto TV** :
- Chaînes gratuites financées par la pub
- Légal
- Disponible en France
- Application et web

**France.tv** :
- Plateforme officielle France Télévisions
- Replay et direct
- Gratuit et légal
- Application disponible

### Applications mobiles

**IPTV Smarters** (Android/iOS) :
- Lecteur IPTV populaire
- Compatible M3U et Xtream Codes
- Gratuit

**GSE Smart IPTV** (iOS) :
- Lecteur complet
- Synchronisation iCloud
- Interface élégante

## Astuces et conseils

### Organisation des chaînes

**Favoris par thème** :

Créez des providers différents pour thématiques :
- Un provider "Actualités" avec chaînes d'info
- Un provider "Sport" avec chaînes sportives
- Un provider "Radios" avec radios Internet

**Résultat** : Navigation plus claire

### Utilisation avec télécommande

**PC connecté à la TV** :

Si vous utilisez Hypnotix sur TV via PC :
1. Connectez une télécommande USB ou Bluetooth
2. Configurez les raccourcis clavier
3. Naviguez depuis le canapé

**Alternative** :
- Application mobile de contrôle (KDE Connect)
- Contrôle à distance du PC

### Enregistrement de flux

**Hypnotix ne permet pas d'enregistrer** nativement.

**Avec VLC** :
1. Ouvrez le flux dans VLC
2. **Vue** → **Contrôles avancés**
3. Bouton **Enregistrer** apparaît
4. Lancez la lecture, cliquez sur Enregistrer

**Attention légalité** :
- Enregistrement pour usage personnel OK
- Redistribution interdite
- Respectez les droits d'auteur

### Économiser de la bande passante

**Si connexion limitée** :

- Préférez les chaînes SD (définition standard)
- Évitez les flux HD/4K
- Fermez autres applications réseau
- Programmez les visionnages hors heures de pointe

### Horaires internationaux

**Chaînes étrangères** :

Attention aux décalages horaires :
- Chaîne US → Décalage de 6-9h
- Direct "20h" aux USA = 2-5h du matin en France
- Vérifiez les horaires

## Utilisation avancée

### Éditer un fichier M3U

**Ajouter des métadonnées** :

```
#EXTINF:-1 tvg-logo="http://example.com/logo.png" group-title="News",France 24
https://static.france24.com/live/F24_EN_LO_HLS/live_web.m3u8
```

**Paramètres** :
- `tvg-logo` : URL du logo de la chaîne
- `group-title` : Catégorie (News, Sport, Movies)
- `tvg-id` : ID pour EPG (guide électronique)

### EPG (Guide électronique des programmes)

**Certains providers supportent EPG** :

Affiche la grille des programmes :
- Ce qui passe maintenant
- Programmes à venir
- Descriptions

**Configuration** :
- Certains M3U incluent info EPG
- URL EPG XML séparée parfois
- Fonctionnalité avancée

### Streaming depuis smartphone

**Chromecast/DLNA** :

Si Hypnotix sur PC, TV connectée :
1. Hypnotix lit le flux
2. Diffusez l'écran PC vers TV (Chromecast)
3. Ou câble HDMI simple

### Scripts et automatisation

**Lancer automatiquement** :

Script bash pour ouvrir Hypnotix sur une chaîne :
```bash
#!/bin/bash
hypnotix &  
sleep 3  
# Nécessite configuration manuelle ou CLI (si supporté)
```

**Utilité limitée** car Hypnotix est GUI.

## Ressources et liens

### Documentation officielle

**Hypnotix** :
- Pas de site dédié
- Fait partie de Linux Mint
- GitHub : [https://github.com/linuxmint/hypnotix](https://github.com/linuxmint/hypnotix)

**Blog Linux Mint** :
- Annonces et nouveautés
- [https://blog.linuxmint.com/](https://blog.linuxmint.com/)

### Listes IPTV légales

**GitHub IPTV Org** :
- [https://github.com/iptv-org/iptv](https://github.com/iptv-org/iptv)
- Liste collaborative mondiale
- Mise à jour communautaire
- Chaînes gratuites légales

**Free IPTV** :
- Recherchez "Free IPTV" sur GitHub
- Plusieurs listes communautaires
- Vérifiez toujours légalité

### Sites officiels de chaînes

**France** :
- France Télévisions : [https://www.france.tv/](https://www.france.tv/)
- Arte : [https://www.arte.tv/](https://www.arte.tv/)
- TV5Monde : [https://www.tv5monde.com/](https://www.tv5monde.com/)

**International** :
- France 24 : [https://www.france24.com/](https://www.france24.com/)
- Deutsche Welle : [https://www.dw.com/](https://www.dw.com/)
- Al Jazeera English : [https://www.aljazeera.com/](https://www.aljazeera.com/)

### Communauté

**Forums Linux Mint** :
- Section Hypnotix
- Partage de listes légales
- Aide et support

**Reddit** :
- r/IPTV (attention sources illégales)
- r/linuxmint

## Conclusion

Hypnotix est un excellent outil pour accéder à la télévision par Internet sur Linux Mint. Simple d'utilisation, il permet de regarder gratuitement de nombreuses chaînes du monde entier, à condition de rester dans la **légalité**.

**Points clés à retenir** :

- **Simple** : Interface intuitive, ajout facile de sources
- **Gratuit** : Aucun coût, open source
- **Légal** : Utilisez uniquement des sources autorisées
- **Personnalisable** : Favoris, providers multiples, organisation

**Pour bien commencer** :
1. Lancez Hypnotix
2. Ajoutez un provider légal (ex: iptv-org sur GitHub)
3. Explorez les chaînes disponibles
4. Ajoutez vos favorites
5. Profitez !

**Rappel important sur la légalité** :
- Payez pour le contenu premium
- Utilisez des sources officielles
- En cas de doute, abstenez-vous
- Les risques ne valent pas l'économie

**Cas d'usage idéaux** :
- Chaînes d'information internationales gratuites
- Radios Internet
- Chaînes publiques étrangères
- Découverte de contenus du monde entier

Hypnotix transforme votre ordinateur Linux Mint en téléviseur connecté, vous donnant accès à un monde de contenus légaux et gratuits. Utilisez-le de manière responsable et profitez de la diversité des médias mondiaux !

---


⏭️ [Sticky Notes (Pense-bêtes)](/05-applications-essentielles-et-outils-mint/11-sticky-notes.md)
