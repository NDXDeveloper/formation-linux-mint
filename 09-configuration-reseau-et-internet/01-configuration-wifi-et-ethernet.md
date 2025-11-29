🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 9.1 Configuration WiFi et Ethernet

## Introduction

La connexion à Internet est l'une des premières choses à configurer après l'installation de Linux Mint. Que vous utilisiez une connexion sans fil (WiFi) ou câblée (Ethernet), Linux Mint propose des outils simples et intuitifs pour vous connecter rapidement.

Dans ce chapitre, nous allons voir comment configurer vos connexions réseau, que ce soit en WiFi ou en Ethernet, en utilisant principalement l'interface graphique de Linux Mint.

## Configuration WiFi

### Connexion WiFi via l'interface graphique

La méthode la plus simple pour se connecter à un réseau WiFi sous Linux Mint est d'utiliser l'applet réseau situé dans la barre des tâches.

#### Étapes de connexion :

1. **Localiser l'icône réseau** : Dans la barre des tâches (généralement en bas à droite), vous verrez une icône représentant le réseau. Si vous n'êtes pas connecté, elle ressemble à des ondes WiFi barrées ou à un point d'exclamation.

2. **Ouvrir le menu réseau** : Cliquez sur cette icône pour afficher la liste des réseaux WiFi disponibles.

3. **Sélectionner votre réseau** : Dans la liste qui apparaît, trouvez le nom de votre réseau WiFi (SSID) et cliquez dessus.

4. **Entrer le mot de passe** : Une fenêtre s'ouvre pour vous demander le mot de passe du réseau. Tapez-le soigneusement (attention aux majuscules/minuscules).

5. **Options de sécurité** :
   - Vous pouvez cocher "Afficher le mot de passe" pour vérifier que vous le tapez correctement
   - L'option "Se connecter automatiquement" permet à Linux Mint de se reconnecter automatiquement à ce réseau à l'avenir

6. **Connexion** : Cliquez sur "Se connecter" et patientez quelques secondes. L'icône réseau devrait changer pour indiquer une connexion active.

### Connexion à un réseau WiFi caché

Certains réseaux WiFi sont configurés pour ne pas diffuser leur nom (SSID). Pour vous y connecter :

1. Cliquez sur l'icône réseau dans la barre des tâches
2. Sélectionnez "Se connecter à un réseau masqué..." ou "Connexion à un réseau caché..."
3. Dans la fenêtre qui s'ouvre :
   - **Nom du réseau (SSID)** : Tapez le nom exact du réseau
   - **Type de sécurité** : Sélectionnez le type (généralement WPA/WPA2 Personnel)
   - **Mot de passe** : Entrez le mot de passe du réseau
4. Cliquez sur "Se connecter"

### Gérer les connexions WiFi enregistrées

Linux Mint mémorise automatiquement les réseaux auxquels vous vous êtes déjà connecté.

#### Accéder aux paramètres réseau :

1. Cliquez sur l'icône réseau dans la barre des tâches
2. Sélectionnez "Paramètres réseau" ou "Connexions réseau"
3. Une fenêtre s'ouvre avec la liste de toutes vos connexions enregistrées

#### Options disponibles :

- **Modifier une connexion** : Sélectionnez une connexion et cliquez sur la roue dentée ou le bouton "Modifier" pour changer le mot de passe, activer/désactiver la connexion automatique, etc.
- **Supprimer une connexion** : Sélectionnez une connexion et cliquez sur le bouton "-" ou "Supprimer" pour l'effacer de la mémoire
- **Priorité des connexions** : Vous pouvez définir l'ordre de priorité si plusieurs réseaux connus sont disponibles

### Configuration avancée WiFi

Pour accéder aux paramètres avancés d'une connexion WiFi :

1. Ouvrez les "Paramètres réseau"
2. Sélectionnez votre connexion WiFi
3. Cliquez sur "Modifier" (icône en forme de roue dentée)
4. Plusieurs onglets sont disponibles :

#### Onglet "WiFi" :
- **SSID** : Le nom du réseau
- **BSSID** : L'adresse MAC du point d'accès (utile si plusieurs routeurs ont le même nom)
- **Adresse MAC clonée** : Pour certaines configurations réseau spécifiques
- **MTU** : Taille maximale des paquets (laisser à "automatique" sauf besoins spécifiques)

#### Onglet "Sécurité WiFi" :
- **Type de sécurité** : WPA/WPA2/WPA3 Personnel ou Entreprise
- **Mot de passe** : Pour changer le mot de passe enregistré

#### Onglet "Paramètres IPv4" :
- **Méthode** : Automatique (DHCP) - recommandé pour la plupart des utilisateurs
- **Adresses** : Pour configurer une adresse IP fixe si nécessaire
- **Serveurs DNS** : Pour utiliser des serveurs DNS personnalisés (comme 8.8.8.8 de Google ou 1.1.1.1 de Cloudflare)

#### Onglet "Paramètres IPv6" :
- Configuration similaire à IPv4, mais pour le protocole IPv6

## Configuration Ethernet (connexion filaire)

La connexion Ethernet est généralement la plus simple car elle se configure automatiquement dans la plupart des cas.

### Connexion automatique

1. **Branchez le câble Ethernet** : Connectez une extrémité à votre ordinateur et l'autre à votre routeur/box Internet
2. **Détection automatique** : Linux Mint détecte automatiquement la connexion et se connecte
3. **Vérification** : L'icône réseau dans la barre des tâches devrait afficher une connexion active (généralement un câble ou des barres)

Dans la majorité des cas, aucune configuration supplémentaire n'est nécessaire. La connexion utilise automatiquement DHCP pour obtenir une adresse IP.

### Configuration manuelle Ethernet

Si vous avez besoin de configurer manuellement votre connexion Ethernet (par exemple, pour une adresse IP fixe) :

1. Cliquez sur l'icône réseau et sélectionnez "Paramètres réseau"
2. Sélectionnez votre connexion filaire (généralement nommée "Connexion filaire 1" ou similaire)
3. Cliquez sur "Modifier"

#### Configuration d'une adresse IP fixe :

Dans l'onglet "Paramètres IPv4" :

1. Changez la **Méthode** de "Automatique (DHCP)" à "Manuel"
2. Cliquez sur "Ajouter" dans la section Adresses
3. Remplissez les champs :
   - **Adresse** : L'adresse IP que vous souhaitez attribuer (ex: 192.168.1.100)
   - **Masque réseau** : Généralement 255.255.255.0 ou 24
   - **Passerelle** : L'adresse de votre routeur (ex: 192.168.1.1)
4. Dans **Serveurs DNS** : Entrez les adresses des serveurs DNS, séparées par des virgules (ex: 8.8.8.8, 8.8.4.4)
5. Cliquez sur "Enregistrer"

**Note** : Assurez-vous que l'adresse IP choisie ne soit pas déjà utilisée par un autre appareil sur le réseau et qu'elle soit dans la même plage que votre réseau local.

### Plusieurs connexions Ethernet

Si votre ordinateur dispose de plusieurs ports Ethernet ou si vous utilisez un adaptateur USB-Ethernet, chaque interface sera listée séparément dans les paramètres réseau. Vous pouvez configurer chacune indépendamment.

## Vérifier la connexion réseau

### Via l'interface graphique

1. **Icône réseau** : L'icône dans la barre des tâches indique l'état de la connexion
   - Connecté : Icône normale avec signal fort
   - Connecté mais pas d'Internet : Triangle d'avertissement
   - Déconnecté : Icône barrée

2. **Informations de connexion** : Cliquez sur l'icône réseau puis sur "Informations de connexion" pour voir :
   - Adresse IP attribuée
   - Passerelle par défaut
   - Serveurs DNS utilisés
   - Vitesse de la connexion

### Via le terminal

Pour les utilisateurs plus avancés ou pour diagnostiquer des problèmes, vous pouvez utiliser le terminal :

```bash
# Afficher les interfaces réseau et leurs adresses IP
ip addr show

# Tester la connexion Internet
ping -c 4 google.com

# Afficher les informations détaillées de connexion
nmcli device show
```

## Résolution des problèmes courants

### Le WiFi ne détecte aucun réseau

**Solutions possibles** :

1. **Vérifier que le WiFi est activé** : Certains ordinateurs portables ont un interrupteur physique ou une combinaison de touches (souvent Fn + F2 ou similaire) pour activer/désactiver le WiFi

2. **Redémarrer le gestionnaire réseau** :
   - Ouvrez le menu principal → Administration → Gestionnaire de services
   - Recherchez "Network Manager" et redémarrez-le

   Ou via le terminal :
   ```bash
   sudo systemctl restart NetworkManager
   ```

3. **Vérifier les pilotes** : Utilisez le "Gestionnaire de pilotes" accessible depuis le menu principal pour vérifier si des pilotes propriétaires sont disponibles pour votre carte WiFi

### Connexion WiFi instable ou qui se déconnecte

**Solutions** :

1. **Désactiver la gestion d'énergie du WiFi** :
   ```bash
   sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
   ```
   Changez `wifi.powersave = 3` en `wifi.powersave = 2`
   Sauvegardez (Ctrl+O, Entrée, Ctrl+X) et redémarrez NetworkManager

2. **Vérifier les interférences** : Si possible, changez le canal WiFi de votre routeur ou rapprochez-vous du point d'accès

3. **Mettre à jour les pilotes** : Vérifiez dans le Gestionnaire de pilotes

### Connexion Ethernet non détectée

**Solutions** :

1. **Vérifier le câble** : Testez avec un autre câble Ethernet pour éliminer un problème matériel

2. **Vérifier le port** : Si votre ordinateur a plusieurs ports Ethernet, essayez-en un autre

3. **Redémarrer NetworkManager** :
   ```bash
   sudo systemctl restart NetworkManager
   ```

4. **Vérifier que l'interface est activée** :
   ```bash
   ip link show
   ```
   Si l'interface est "DOWN", activez-la :
   ```bash
   sudo ip link set <nom-interface> up
   ```

### Impossible de se connecter à un réseau WiFi spécifique

**Solutions** :

1. **Oublier le réseau et se reconnecter** :
   - Allez dans Paramètres réseau
   - Supprimez la connexion problématique
   - Reconnectez-vous en entrant à nouveau le mot de passe

2. **Vérifier le type de sécurité** : Assurez-vous que le type de sécurité sélectionné (WPA2, WPA3, etc.) correspond à celui configuré sur votre routeur

3. **Problème de mot de passe** : Vérifiez les majuscules/minuscules et les caractères spéciaux

## Conseils et bonnes pratiques

### Sécurité WiFi

- **Utilisez WPA2 ou WPA3** : Évitez les réseaux sans mot de passe ou utilisant le protocole WEP obsolète
- **Réseaux publics** : Soyez prudent sur les WiFi publics. Évitez d'accéder à des informations sensibles sans VPN
- **Mot de passe fort** : Si vous configurez votre propre réseau, utilisez un mot de passe long et complexe

### Performance

- **Préférez l'Ethernet quand c'est possible** : La connexion filaire est généralement plus stable et plus rapide que le WiFi
- **Bande 5 GHz** : Si votre routeur et votre carte WiFi le supportent, utilisez la bande 5 GHz pour de meilleures performances (moins d'interférences)
- **Positionnement** : Pour le WiFi, la proximité du routeur et l'absence d'obstacles améliorent la qualité du signal

### Gestion

- **Nettoyage régulier** : Supprimez les connexions WiFi que vous n'utilisez plus pour garder une liste claire
- **Noms descriptifs** : Renommez vos connexions avec des noms explicites si vous en avez plusieurs
- **Documentation** : Notez vos paramètres réseau personnalisés (IP fixe, DNS, etc.) dans un endroit sûr

## Aller plus loin

La configuration réseau de base que nous venons de voir couvre les besoins de la majorité des utilisateurs. Pour des configurations plus avancées (VPN, partage de connexion, pare-feu, etc.), consultez les chapitres suivants de ce guide.

Si vous rencontrez des problèmes persistants malgré ces solutions, n'hésitez pas à :
- Consulter les forums Linux Mint en français
- Vérifier la documentation officielle
- Demander de l'aide à la communauté en fournissant des détails précis sur votre configuration

---

**Points clés à retenir** :
- La connexion WiFi se fait simplement via l'icône réseau dans la barre des tâches
- L'Ethernet fonctionne généralement automatiquement dès le branchement du câble
- Les paramètres réseau avancés sont accessibles via "Paramètres réseau"
- En cas de problème, commencez par les solutions simples (redémarrage, vérification des câbles)
- La sécurité est importante, surtout sur les réseaux WiFi publics

⏭️ [Partage de connexion](/09-configuration-reseau-et-internet/02-partage-de-connexion.md)
