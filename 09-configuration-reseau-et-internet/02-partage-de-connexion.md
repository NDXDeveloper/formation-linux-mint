🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 9.2 Partage de connexion

## Introduction

Le partage de connexion permet de transformer votre ordinateur Linux Mint en point d'accès pour partager votre connexion Internet avec d'autres appareils. Cette fonctionnalité est particulièrement utile lorsque :

- Vous avez une connexion Internet filaire (Ethernet) et souhaitez la partager en WiFi
- Vous voulez créer un point d'accès WiFi temporaire
- Vous devez connecter plusieurs appareils mais n'avez qu'une seule connexion disponible
- Vous souhaitez partager votre connexion mobile avec d'autres appareils

Dans ce chapitre, nous allons explorer les différentes méthodes de partage de connexion sous Linux Mint, en nous concentrant sur les solutions les plus accessibles.

## Partage de connexion Internet en WiFi (Hotspot)

La méthode la plus courante consiste à créer un point d'accès WiFi (hotspot) pour partager votre connexion Internet.

### Prérequis

Avant de commencer, assurez-vous que :
- Votre carte WiFi supporte le mode "point d'accès" (la plupart des cartes modernes le supportent)
- Vous avez une connexion Internet active (par Ethernet ou via un autre adaptateur WiFi)
- Votre système est à jour

### Créer un hotspot WiFi via l'interface graphique

Linux Mint facilite grandement la création d'un point d'accès WiFi grâce à son interface graphique.

#### Méthode 1 : Via l'icône réseau (la plus simple)

1. **Accéder aux paramètres** :
   - Cliquez sur l'icône réseau dans la barre des tâches
   - Sélectionnez "Paramètres réseau" ou "Connexions réseau"

2. **Créer un nouveau hotspot** :
   - Cliquez sur le bouton "+" (ajouter une nouvelle connexion)
   - Sélectionnez "Wi-Fi" dans la liste des types de connexion

3. **Configurer le hotspot** :

   **Onglet "Wi-Fi"** :
   - **Nom de la connexion** : Donnez un nom descriptif (ex: "Hotspot Maison")
   - **SSID** : C'est le nom que verront les appareils qui se connecteront (ex: "Mon-Hotspot-Linux")
   - **Mode** : Sélectionnez "Point d'accès" ou "Hotspot"
   - **Périphérique** : Sélectionnez votre carte WiFi

   **Onglet "Sécurité Wi-Fi"** :
   - **Type de sécurité** : Choisissez "WPA & WPA2 Personnel" (recommandé)
   - **Mot de passe** : Créez un mot de passe fort (minimum 8 caractères)

   **Onglet "Paramètres IPv4"** :
   - **Méthode** : Sélectionnez "Partagé avec d'autres ordinateurs"
   - Cette option configure automatiquement un serveur DHCP pour attribuer des adresses IP aux appareils qui se connectent

4. **Enregistrer et activer** :
   - Cliquez sur "Enregistrer"
   - Activez le hotspot en cliquant sur le bouton à bascule ou en sélectionnant la connexion dans le menu réseau

5. **Vérification** :
   - Votre hotspot est maintenant actif
   - D'autres appareils devraient voir votre réseau WiFi dans leur liste de réseaux disponibles
   - Ils pourront se connecter en utilisant le mot de passe que vous avez défini

#### Méthode 2 : Via les paramètres système

1. Ouvrez le **Menu principal** → **Préférences** → **Réseau**
2. Suivez les mêmes étapes que la méthode 1

### Configuration avancée du hotspot

Pour personnaliser davantage votre point d'accès :

#### Choisir le canal WiFi

1. Modifiez votre connexion hotspot
2. Dans l'onglet "Wi-Fi", section avancée
3. Vous pouvez spécifier un canal particulier (1-11 pour 2.4 GHz, 36-165 pour 5 GHz)
4. Par défaut, "Automatique" est recommandé

#### Limiter la bande passante

Linux Mint ne propose pas d'option graphique native pour limiter la bande passante, mais des outils tiers comme `wondershaper` peuvent être installés pour cette fonctionnalité.

#### Masquer le SSID

Pour rendre votre hotspot invisible dans la liste des réseaux disponibles :
1. Modifiez votre connexion hotspot
2. Dans l'onglet "Wi-Fi"
3. Cochez l'option "Masquer le réseau" ou "Réseau caché"
4. Les utilisateurs devront connaître le nom exact du réseau pour s'y connecter

## Partage de connexion Ethernet

Si vous recevez Internet par WiFi et souhaitez le partager via un câble Ethernet :

### Configuration

1. **Branchez le câble Ethernet** entre votre ordinateur et l'appareil qui doit recevoir Internet

2. **Configurer la connexion Ethernet** :
   - Ouvrez les "Paramètres réseau"
   - Sélectionnez votre connexion Ethernet (ou créez-en une nouvelle)
   - Cliquez sur "Modifier"

3. **Paramètres IPv4** :
   - Changez la **Méthode** en "Partagé avec d'autres ordinateurs"
   - Cliquez sur "Enregistrer"

4. **Activation** :
   - Activez la connexion
   - L'appareil connecté devrait automatiquement recevoir une adresse IP et avoir accès à Internet

**Note** : Cette méthode fonctionne dans les deux sens - vous pouvez partager une connexion WiFi via Ethernet, ou une connexion Ethernet via WiFi.

## Partage de connexion USB (Partage via smartphone)

Si vous souhaitez utiliser la connexion 4G/5G de votre smartphone sur votre ordinateur Linux Mint :

### Partage USB

1. **Connectez votre smartphone** à l'ordinateur via câble USB

2. **Activez le partage USB sur le smartphone** :
   - Sur Android : Paramètres → Connexions → Point d'accès mobile et modem → Modem USB
   - Sur iPhone : Réglages → Partage de connexion → Activer

3. **Sur Linux Mint** :
   - La connexion devrait être détectée automatiquement
   - Une nouvelle interface réseau apparaît (généralement nommée "usb0" ou similaire)
   - Linux Mint se connecte automatiquement

4. **Vérification** :
   - L'icône réseau devrait indiquer une connexion active
   - Testez votre connexion Internet

### Avantages du partage USB

- Plus stable que le WiFi ou le Bluetooth
- Consomme moins de batterie sur le smartphone
- Vitesses généralement meilleures
- Charge le smartphone en même temps

## Partage de connexion Bluetooth

Le partage Bluetooth est moins courant mais peut être utile si le WiFi n'est pas disponible.

### Configuration

1. **Jumeler les appareils** :
   - Assurez-vous que le Bluetooth est activé sur les deux appareils
   - Sur Linux Mint : Menu → Préférences → Bluetooth
   - Jumelez votre smartphone ou autre appareil

2. **Activer le partage Bluetooth sur le smartphone** :
   - Sur Android : Paramètres → Connexions → Point d'accès mobile et modem → Modem Bluetooth
   - Assurez-vous que l'appareil est bien jumelé

3. **Connexion sur Linux Mint** :
   - Clic droit sur l'appareil jumelé dans le gestionnaire Bluetooth
   - Sélectionnez "Connecter au réseau" ou option similaire

**Limitations** : Le partage Bluetooth est généralement plus lent que WiFi ou USB et a une portée limitée (environ 10 mètres).

## Gestion et surveillance du partage

### Voir les appareils connectés

Malheureusement, Linux Mint ne fournit pas d'outil graphique natif pour voir facilement les appareils connectés à votre hotspot. Cependant, vous pouvez utiliser le terminal :

```bash
# Voir les appareils connectés (nécessite les droits administrateur)
arp -a

# Ou de manière plus détaillée
sudo arp-scan --localnet
```

Pour une interface graphique, vous pouvez installer des outils comme :
```bash
sudo apt install arp-scan
```

### Surveiller l'utilisation de la bande passante

Pour surveiller combien de données sont transférées :

1. **Via le moniteur système** :
   - Menu → Préférences → Moniteur système
   - Onglet "Ressources" → section "Réseau"

2. **Via des outils dédiés** :
   Installez `nethogs` pour une surveillance en temps réel par processus :
   ```bash
   sudo apt install nethogs
   sudo nethogs
   ```

### Arrêter le partage de connexion

Pour désactiver votre hotspot :

1. **Via l'icône réseau** :
   - Cliquez sur l'icône réseau
   - Désactivez la connexion hotspot

2. **Ou via les paramètres réseau** :
   - Ouvrez "Paramètres réseau"
   - Désactivez la connexion hotspot avec le bouton à bascule

## Sécurité du partage de connexion

### Bonnes pratiques de sécurité

#### Mot de passe fort
- Utilisez un mot de passe d'au moins 12 caractères
- Mélangez majuscules, minuscules, chiffres et symboles
- Évitez les mots du dictionnaire
- Changez régulièrement le mot de passe si vous partagez avec beaucoup de monde

#### Chiffrement approprié
- Utilisez toujours WPA2 ou WPA3 (pas de WEP ou réseau ouvert)
- WPA3 offre une meilleure sécurité si tous vos appareils le supportent

#### Masquer le SSID (optionnel)
- Rend votre réseau invisible aux appareils qui scannent
- Offre une couche de sécurité supplémentaire (mais minime)
- Peut compliquer la connexion pour les utilisateurs légitimes

#### Limiter les appareils
- Ne partagez votre mot de passe qu'avec des personnes de confiance
- Changez le mot de passe si vous suspectez un accès non autorisé

#### Désactiver quand non utilisé
- Éteignez votre hotspot lorsque vous ne l'utilisez pas
- Cela économise de la batterie (sur portable) et améliore la sécurité

### Pare-feu et filtrage

Pour une sécurité accrue, vous pouvez configurer le pare-feu pour restreindre l'accès :

1. Installez GUFW (interface graphique pour le pare-feu) :
   ```bash
   sudo apt install gufw
   ```

2. Configurez les règles selon vos besoins (voir chapitre 9.3 sur le pare-feu)

## Résolution des problèmes courants

### Le hotspot WiFi ne se crée pas

**Causes possibles et solutions** :

1. **Carte WiFi incompatible** :
   - Vérifiez si votre carte supporte le mode AP (point d'accès)
   - Testez avec cette commande :
   ```bash
   iw list | grep -A 10 "Supported interface modes"
   ```
   - Recherchez "AP" dans la liste

2. **Pilotes manquants ou obsolètes** :
   - Ouvrez le "Gestionnaire de pilotes"
   - Vérifiez si des pilotes propriétaires sont disponibles pour votre WiFi
   - Installez-les si disponibles

3. **NetworkManager ne fonctionne pas correctement** :
   - Redémarrez le service :
   ```bash
   sudo systemctl restart NetworkManager
   ```

4. **Conflit avec une connexion WiFi existante** :
   - Vous ne pouvez généralement pas être connecté à un WiFi ET créer un hotspot avec la même carte
   - Déconnectez-vous du WiFi avant de créer le hotspot
   - Ou utilisez une deuxième carte WiFi / adaptateur USB

### Les appareils ne peuvent pas se connecter au hotspot

**Solutions** :

1. **Vérifier le mot de passe** :
   - Assurez-vous que le mot de passe est correct (attention aux majuscules/minuscules)
   - Essayez de recréer le hotspot avec un mot de passe plus simple pour tester

2. **Vérifier le type de sécurité** :
   - Certains vieux appareils ne supportent pas WPA3
   - Utilisez WPA2 pour une meilleure compatibilité

3. **Vérifier le canal WiFi** :
   - Certains appareils ne supportent pas tous les canaux
   - Essayez de changer le canal ou laissez sur "Automatique"

4. **Redémarrer le hotspot** :
   - Désactivez puis réactivez le hotspot
   - Si le problème persiste, redémarrez l'ordinateur

### Les appareils sont connectés mais pas d'Internet

**Solutions** :

1. **Vérifier la méthode IPv4** :
   - Assurez-vous que "Partagé avec d'autres ordinateurs" est bien sélectionné
   - Vérifiez que votre connexion Internet principale fonctionne

2. **Vérifier le pare-feu** :
   - Le pare-feu peut bloquer le partage
   - Temporairement, désactivez le pare-feu pour tester
   - Si cela résout le problème, créez des règles appropriées

3. **Vérifier le routage** :
   - Ouvrez le terminal et vérifiez :
   ```bash
   sudo sysctl net.ipv4.ip_forward
   ```
   - Devrait retourner "net.ipv4.ip_forward = 1"
   - Si ce n'est pas le cas :
   ```bash
   sudo sysctl -w net.ipv4.ip_forward=1
   ```

4. **Redémarrer NetworkManager** :
   ```bash
   sudo systemctl restart NetworkManager
   ```

### Performances lentes du hotspot

**Optimisations** :

1. **Changer de bande WiFi** :
   - Si votre carte le supporte, utilisez la bande 5 GHz au lieu de 2.4 GHz
   - Plus rapide mais portée plus courte

2. **Limiter le nombre d'appareils connectés** :
   - Plus il y a d'appareils, plus la bande passante est partagée
   - Déconnectez les appareils inutilisés

3. **Optimiser le canal WiFi** :
   - Utilisez des outils comme `wifi-analyzer` pour trouver les canaux les moins encombrés
   - Changez le canal dans la configuration du hotspot

4. **Vérifier la source Internet** :
   - Si votre connexion Internet principale est lente, le hotspot le sera aussi
   - Testez votre vitesse Internet directement

### Le partage USB ne fonctionne pas

**Solutions** :

1. **Vérifier le câble USB** :
   - Utilisez un câble de qualité capable de transférer des données (pas seulement de charge)
   - Certains câbles ne supportent que la charge

2. **Activer le débogage USB (Android)** :
   - Parfois nécessaire : Paramètres → Options pour les développeurs → Débogage USB

3. **Installer les dépendances** :
   ```bash
   sudo apt install usb-modeswitch
   ```

4. **Redémarrer le smartphone et l'ordinateur**

## Alternatives au partage de connexion intégré

Si le partage intégré de Linux Mint ne fonctionne pas pour vous, voici des alternatives :

### create_ap (ligne de commande)

Un script qui facilite la création de hotspots :

```bash
# Installation
sudo apt install create_ap

# Créer un hotspot simple
sudo create_ap wlan0 eth0 MonHotspot MonMotDePasse
```

### hostapd (avancé)

Configuration manuelle complète d'un point d'accès :
- Plus complexe mais plus flexible
- Permet un contrôle total
- Recommandé pour les utilisateurs avancés

### Applications tierces

- **Linux WiFi Hotspot** : Interface graphique conviviale
  ```bash
  sudo apt install linux-wifi-hotspot
  ```

## Conseils et astuces

### Optimiser l'autonomie de la batterie

Si vous êtes sur un ordinateur portable :
- Le partage de connexion consomme beaucoup d'énergie
- Branchez l'ordinateur sur secteur si possible
- Désactivez le hotspot quand vous ne l'utilisez pas
- Réduisez la puissance d'émission si l'option est disponible

### Créer un hotspot permanent

Pour un hotspot qui démarre automatiquement :
1. Créez votre connexion hotspot comme d'habitude
2. Dans les paramètres de la connexion, cochez "Se connecter automatiquement"
3. Le hotspot démarrera automatiquement à chaque démarrage de l'ordinateur

**Attention** : Cela peut poser des problèmes de sécurité si votre ordinateur démarre dans un lieu public.

### Gérer plusieurs profils de hotspot

Vous pouvez créer plusieurs configurations de hotspot différentes :
- Un pour la maison avec un certain nom et mot de passe
- Un pour le travail
- Un pour les invités avec un mot de passe différent
- Basculez entre eux selon vos besoins

### Notation de la qualité

Pour connaître la qualité du signal de votre hotspot :
- Rapprochez-vous pour des vitesses maximales
- La portée typique est de 30-50 mètres en intérieur
- Les murs et obstacles réduisent la portée et la vitesse

## Cas d'usage pratiques

### Créer un réseau domestique temporaire

Si votre routeur est en panne :
1. Connectez votre ordinateur à Internet (par câble ou 4G partagée)
2. Créez un hotspot WiFi
3. Connectez tous vos appareils au hotspot
4. Tous vos appareils ont accès à Internet

### Partager Internet en déplacement

En voyage avec un ordinateur portable :
1. Connectez-vous au WiFi de l'hôtel (souvent payant par appareil)
2. Créez un hotspot
3. Connectez tous vos appareils au hotspot
4. Économisez sur les frais de connexion multiples

### Étendre un réseau WiFi faible

Si le signal WiFi est faible dans certaines pièces :
1. Placez l'ordinateur à mi-chemin
2. Connectez-le au WiFi principal
3. Créez un hotspot pour étendre la portée
4. Les appareils distants se connectent au hotspot

**Note** : Cette méthode réduit la bande passante, une vraie borne WiFi répéteur est préférable pour un usage permanent.

## Aller plus loin

Le partage de connexion basique couvert dans ce chapitre suffit pour la plupart des besoins quotidiens. Pour des configurations plus avancées :

- **Chapitre 9.3** : Configuration du pare-feu pour sécuriser davantage votre hotspot
- **Chapitre 9.6** : Partage de fichiers en réseau local
- **Chapitre 21** : Configuration de serveurs pour créer un point d'accès professionnel

---

**Points clés à retenir** :
- Linux Mint facilite la création de hotspots WiFi via l'interface graphique
- La méthode IPv4 "Partagé avec d'autres ordinateurs" est essentielle pour le partage
- Un mot de passe fort et WPA2/WPA3 sont indispensables pour la sécurité
- Le partage USB est souvent plus stable que le WiFi pour le partage smartphone
- Désactivez le hotspot lorsqu'il n'est pas utilisé pour économiser l'énergie et améliorer la sécurité
- La plupart des problèmes se résolvent en redémarrant NetworkManager ou en vérifiant la configuration IPv4

⏭️ [Pare-feu (UFW/GUFW)](/09-configuration-reseau-et-internet/03-pare-feu-ufw-gufw.md)
