🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 12.2 Pilotes propriétaires (NVIDIA, AMD, WiFi)

## Introduction

Les **pilotes propriétaires** sont développés directement par les fabricants de matériel (NVIDIA, AMD, Broadcom, etc.) et sont souvent nécessaires pour tirer le meilleur parti de votre équipement, notamment pour les cartes graphiques et certaines cartes WiFi.

Ce chapitre vous guide dans l'installation et la configuration des pilotes propriétaires les plus courants sous Linux Mint.

## Pourquoi des pilotes propriétaires ?

### La réalité du matériel moderne

Bien que Linux privilégie les logiciels libres, certains fabricants ne publient pas le code source complet de leurs pilotes. Ils fournissent uniquement des versions "fermées" (propriétaires) qui :

- Offrent de **meilleures performances** que les pilotes libres
- Débloquent **toutes les fonctionnalités** du matériel
- Sont **optimisés** par les ingénieurs du fabricant
- Reçoivent des **mises à jour régulières** pour supporter les nouveaux jeux et applications

### Compromis philosophique

Linux Mint fait un **compromis pragmatique** :
- Le système fonctionne par défaut avec des pilotes libres
- Les pilotes propriétaires sont facilement disponibles pour ceux qui en ont besoin
- L'utilisateur garde le contrôle et choisit ce qu'il préfère

---

## Pilotes NVIDIA

NVIDIA est l'un des principaux fabricants de cartes graphiques. Leurs pilotes propriétaires sont essentiels pour :
- Le **gaming** performant
- Le **rendu 3D** et la modélisation
- L'**apprentissage automatique** (IA, deep learning)
- Le **montage vidéo** avec accélération GPU

### Identifier votre carte NVIDIA

Avant d'installer un pilote, vérifiez que vous avez bien une carte NVIDIA :

**Méthode 1 : Via l'interface graphique**
1. Ouvrez le **Menu** → **Informations système**
2. Regardez la section "Graphiques" ou "Matériel"

**Méthode 2 : Via le terminal**
```bash
lspci | grep -i nvidia
```

Si cette commande affiche quelque chose comme `NVIDIA Corporation GM107 [GeForce GTX 750]`, vous avez une carte NVIDIA.

### Les différentes versions de pilotes NVIDIA

Le Gestionnaire de pilotes propose généralement plusieurs versions :

#### nvidia-driver-XXX (version récente)
- **Version** : 525, 535, 545, etc.
- **Pour qui** : Cartes graphiques récentes (GTX 900 et plus récent)
- **Avantages** : Meilleures performances, support des derniers jeux
- **Recommandé pour** : Gaming, cartes récentes

#### nvidia-driver-XXX (version stable)
- **Version** : 470, 390
- **Pour qui** : Cartes plus anciennes ou besoin de stabilité maximale
- **Avantages** : Très stable, testé sur le long terme
- **Recommandé pour** : Usage bureautique, serveurs

#### nvidia-driver-XXX-server
- **Pour qui** : Serveurs sans interface graphique
- **Utilisation spécifique** : Calcul GPU sans affichage

#### nouveau (pilote libre)
- **Type** : Open source, intégré au noyau Linux
- **Avantages** : Pas de dépendance au fabricant
- **Inconvénients** : Performances limitées, pas d'accélération 3D complète
- **Pour qui** : Usage bureautique léger uniquement

### Installation du pilote NVIDIA

#### Méthode recommandée : Gestionnaire de pilotes

1. Ouvrez le **Gestionnaire de pilotes** (voir chapitre 12.1)
2. Le système détecte automatiquement votre carte NVIDIA
3. Plusieurs pilotes sont proposés, choisissez celui **recommandé** (généralement la version la plus récente)
4. Cliquez sur le pilote puis sur "**Appliquer les changements**"
5. Patientez pendant le téléchargement et l'installation (5-10 minutes selon votre connexion)
6. **Redémarrez** votre ordinateur (indispensable !)

#### Méthode alternative : Ligne de commande

Si le Gestionnaire de pilotes ne fonctionne pas :

```bash
# Mettre à jour la liste des paquets
sudo apt update

# Installer le pilote recommandé
sudo ubuntu-drivers autoinstall

# Ou installer une version spécifique
sudo apt install nvidia-driver-535

# Redémarrer
sudo reboot
```

### Vérifier l'installation

Après le redémarrage, vérifiez que le pilote NVIDIA est actif :

```bash
nvidia-smi
```

Cette commande doit afficher :
- Le nom de votre carte graphique
- La version du pilote installé
- L'utilisation actuelle du GPU
- La température et la mémoire

**Exemple de sortie correcte :**
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 535.129.03   Driver Version: 535.129.03   CUDA Version: 12.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 1660    Off  | 00000000:01:00.0  On |                  N/A |
| 30%   45C    P0    25W / 120W |    450MiB /  6144MiB |      2%      Default |
+-------------------------------+----------------------+----------------------+
```

### Panneau de configuration NVIDIA

Le pilote propriétaire installe également **NVIDIA X Server Settings**, un outil de configuration graphique :

**Accès :**
- Menu → Préférences → NVIDIA X Server Settings
- Ou via le terminal : `nvidia-settings`

**Fonctionnalités :**
- Réglage de la résolution et de la fréquence d'affichage
- Configuration de plusieurs écrans
- Gestion de l'overclocking (attention !)
- Contrôle du ventilateur
- Informations détaillées sur le GPU

### Configuration multi-écrans avec NVIDIA

Pour configurer plusieurs écrans :

1. Ouvrez **NVIDIA X Server Settings**
2. Allez dans "**X Server Display Configuration**"
3. Vous verrez tous vos écrans détectés
4. Glissez-déposez les écrans pour les positionner
5. Choisissez la résolution et la fréquence pour chaque écran
6. Sélectionnez l'écran principal
7. Cliquez sur "**Enregistrer dans le fichier de configuration X**"
8. Appliquez les changements

### Problèmes courants NVIDIA

#### Écran noir après installation

**Cause :** Conflit entre nouveau et nvidia

**Solution :**
1. Au démarrage, accédez au GRUB (touche Maj ou Échap)
2. Modifiez les options de démarrage en ajoutant `nomodeset`
3. Démarrez en mode dégradé
4. Désinstallez le pilote : `sudo apt purge nvidia-*`
5. Réinstallez proprement via le Gestionnaire de pilotes

#### Performances décevantes en jeu

**Vérifications :**
1. Assurez-vous que le GPU NVIDIA est bien utilisé : `nvidia-smi` pendant le jeu
2. Vérifiez que vous n'êtes pas sur le GPU intégré (portable avec Optimus)
3. Installez les composants additionnels : `sudo apt install nvidia-prime`

#### Pilote non chargé après mise à jour du noyau

**Solution :**
```bash
# Réinstaller les headers du noyau
sudo apt install linux-headers-$(uname -r)

# Reconstruire le module NVIDIA
sudo dkms autoinstall

# Redémarrer
sudo reboot
```

---

## Pilotes AMD

AMD adopte une approche différente de NVIDIA concernant Linux. Les cartes AMD récentes fonctionnent généralement très bien avec les **pilotes libres** AMDGPU.

### Identifier votre carte AMD

**Via le terminal :**
```bash
lspci | grep -i amd
# ou
lspci | grep -i vga
```

### Les pilotes AMD sous Linux

#### AMDGPU (pilote libre - recommandé)

**Caractéristiques :**
- **Open source** et intégré au noyau Linux
- **Excellent support** pour les cartes récentes (RX 400 et plus)
- Performances **très proches** du pilote propriétaire Windows
- **Mis à jour automatiquement** avec le système
- **Aucune installation nécessaire** dans la plupart des cas

**Cartes supportées :**
- Radeon RX 7000 series (RDNA 3)
- Radeon RX 6000 series (RDNA 2)
- Radeon RX 5000 series (RDNA)
- Radeon RX Vega
- Radeon RX 400/500 series

**Vérification du pilote actif :**
```bash
lspci -k | grep -A 3 -i "VGA"
```

Vous devriez voir `Kernel driver in use: amdgpu`

#### AMDGPU-PRO (pilote propriétaire)

**Caractéristiques :**
- Version **propriétaire** du pilote AMD
- Nécessaire principalement pour :
  - Certaines applications professionnelles (CAO, rendu)
  - OpenCL et ROCm (calcul GPU)
  - Encodage/décodage vidéo matériel avancé
- **Non disponible** via le Gestionnaire de pilotes standard
- Installation **manuelle** requise

**Pour qui :**
- Professionnels de la 3D
- Développeurs IA/Machine Learning
- Stations de travail spécialisées

**Installation AMDGPU-PRO (utilisateurs avancés uniquement) :**

> **Attention** : Cette procédure est complexe et généralement **non nécessaire** pour la plupart des utilisateurs.

1. Téléchargez le pilote depuis le site AMD
2. Extrayez l'archive
3. Suivez les instructions spécifiques à votre distribution
4. Le pilote libre AMDGPU suffit dans 95% des cas !

#### Radeon (ancien pilote libre)

**Caractéristiques :**
- Pour les **anciennes cartes** AMD (R5/R7/R9 200/300 series et antérieures)
- Automatiquement utilisé si votre carte est trop ancienne pour AMDGPU
- Performances correctes pour un usage bureautique
- Pas d'accélération 3D récente

### Configuration et optimisation AMD

#### Mesa (bibliothèques graphiques)

Mesa fournit l'accélération OpenGL/Vulkan pour AMD. Pour les meilleures performances :

**Installer la dernière version de Mesa :**

```bash
# Ajouter le PPA Mesa (Ubuntu/Mint)
sudo add-apt-repository ppa:kisak/kisak-mesa
sudo apt update
sudo apt upgrade
```

> **Note** : Cette étape n'est généralement nécessaire que si vous voulez absolument la toute dernière version de Mesa pour du gaming de pointe.

#### Vulkan pour AMD

Vulkan est une API graphique moderne essentielle pour les jeux récents :

```bash
# Installer les drivers Vulkan AMD
sudo apt install mesa-vulkan-drivers vulkan-tools

# Vérifier l'installation
vulkaninfo | grep "deviceName"
```

#### Variables d'environnement pour optimisation

Pour améliorer les performances en jeu :

```bash
# Ajouter à ~/.profile ou ~/.bashrc
export RADV_PERFTEST=aco
export AMD_VULKAN_ICD=RADV
```

- `RADV_PERFTEST=aco` : Active le compilateur de shaders optimisé
- Ces optimisations peuvent donner un gain de 5-15% en FPS

### Problèmes courants AMD

#### Pas d'accélération matérielle

**Vérification :**
```bash
glxinfo | grep "OpenGL renderer"
```

Si vous voyez "llvmpipe" au lieu de votre carte AMD, l'accélération matérielle n'est pas active.

**Solution :**
```bash
# Installer les paquets nécessaires
sudo apt install mesa-utils mesa-vulkan-drivers
sudo apt install libgl1-mesa-dri libglx-mesa0
```

#### Écran noir ou freeze au démarrage

**Solution temporaire :**
1. Au GRUB, éditez les options de boot (touche 'e')
2. Ajoutez `amdgpu.dc=0` aux paramètres du noyau
3. Démarrez avec F10

**Solution permanente :**
```bash
sudo nano /etc/default/grub
# Ajouter amdgpu.dc=0 à GRUB_CMDLINE_LINUX_DEFAULT
sudo update-grub
```

#### Ventilateurs qui tournent trop vite/fort

**Installation de CoreCtrl (contrôle du ventilateur) :**
```bash
sudo apt install corectrl
```

CoreCtrl permet de :
- Contrôler manuellement la vitesse des ventilateurs
- Créer des profils de performance
- Surveiller la température

### AMD : Résumé pour débutants

**Pour la plupart des utilisateurs AMD :**
- ✅ Le pilote libre AMDGPU est **déjà installé** et fonctionne parfaitement
- ✅ Aucune action particulière n'est nécessaire
- ✅ Les performances gaming sont excellentes d'emblée
- ❌ N'installez AMDGPU-PRO que si vous avez un besoin professionnel spécifique

**Avantage AMD sous Linux :**
AMD a une bien meilleure réputation que NVIDIA dans le monde Linux grâce à son excellent support open source !

---

## Pilotes WiFi propriétaires

Certaines cartes WiFi, notamment celles de **Broadcom**, nécessitent des pilotes propriétaires pour fonctionner sous Linux.

### Identifier votre carte WiFi

**Méthode 1 : Interface graphique**
- Menu → Informations système → Matériel

**Méthode 2 : Terminal**
```bash
lspci | grep -i network
# ou pour les cartes USB
lsusb | grep -i wireless
```

### Cartes WiFi Broadcom

Broadcom est le fabricant le plus problématique sous Linux. Leurs cartes sont courantes dans les ordinateurs portables Dell, HP et Lenovo.

#### Types de pilotes Broadcom

##### b43 / b43legacy (pilotes libres)
- Pour les anciennes cartes Broadcom
- Performances limitées
- Installation automatique dans certains cas

##### wl (broadcom-sta / bcmwl-kernel-source)
- Pilote **propriétaire** Broadcom
- Meilleure compatibilité et performances
- Solution recommandée pour la plupart des cartes Broadcom

#### Installation du pilote Broadcom

**Via le Gestionnaire de pilotes (méthode recommandée) :**

1. **Connectez-vous temporairement en Ethernet** (ou partagez la connexion de votre smartphone en USB)
2. Ouvrez le **Gestionnaire de pilotes**
3. Le système détecte votre carte Broadcom
4. Sélectionnez **"bcmwl-kernel-source"** ou **"broadcom-sta"**
5. Cliquez sur "**Appliquer les changements**"
6. Redémarrez l'ordinateur
7. Le WiFi devrait maintenant fonctionner !

**Via la ligne de commande :**

```bash
# Méthode 1 : Installation directe
sudo apt update
sudo apt install bcmwl-kernel-source

# Méthode 2 : Via le gestionnaire de firmware
sudo apt install firmware-b43-installer

# Redémarrer
sudo reboot
```

#### Vérifier le pilote WiFi actif

```bash
lspci -k | grep -A 3 -i network
```

Vous devriez voir le pilote utilisé (wl, b43, etc.)

### Cartes WiFi Intel

**Excellente nouvelle :** Les cartes Intel WiFi ont un **excellent support** sous Linux !

#### Caractéristiques
- Pilotes **libres** et open source
- Intégrés au noyau Linux
- **Aucune installation nécessaire** dans 99% des cas
- Très stables et performantes

#### Firmware Intel

Parfois, seul le firmware manque :

```bash
sudo apt install firmware-iwlwifi
sudo modprobe -r iwlwifi
sudo modprobe iwlwifi
```

### Cartes WiFi Realtek

Les cartes Realtek sont également courantes et généralement bien supportées.

#### Support natif
- La plupart fonctionnent directement
- Pilotes intégrés au noyau

#### Si ça ne fonctionne pas

**Identifier précisément votre modèle :**
```bash
lsusb | grep Realtek
# ou
lspci | grep Realtek
```

**Installation de pilotes additionnels :**
```bash
# Pour les cartes RTL8812AU, RTL8821CE, etc.
sudo apt install rtl8812au-dkms
# ou cherchez le paquet spécifique à votre modèle
```

### Cartes WiFi USB

Les adaptateurs WiFi USB peuvent nécessiter des pilotes spécifiques.

**Diagnostic :**
```bash
lsusb
# Notez l'ID du périphérique (exemple: 0bda:8812)
```

**Recherche du pilote :**
1. Cherchez sur internet : "Linux driver [ID périphérique]"
2. Consultez les forums Linux Mint
3. Vérifiez la base de données du matériel Linux

**Installation générique :**
```bash
sudo apt install linux-firmware
sudo apt install firmware-misc-nonfree
```

### Problèmes WiFi courants

#### Le WiFi ne détecte aucun réseau

**Causes possibles :**
1. Pilote manquant ou incorrect
2. Carte WiFi désactivée par un bouton physique
3. Mode avion activé
4. Carte bloquée par rfkill

**Solutions :**

```bash
# Vérifier le statut rfkill
rfkill list

# Débloquer le WiFi si nécessaire
sudo rfkill unblock wifi
sudo rfkill unblock all

# Redémarrer le gestionnaire réseau
sudo systemctl restart NetworkManager
```

#### Connexion WiFi instable

**Solutions :**
1. Désactiver la gestion d'énergie WiFi :
```bash
sudo nano /etc/NetworkManager/conf.d/wifi-powersave.conf
```

Ajoutez :
```
[connection]
wifi.powersave = 2
```

2. Redémarrez le service :
```bash
sudo systemctl restart NetworkManager
```

#### Vitesse WiFi lente

**Optimisations :**
1. Vérifiez que vous êtes sur la bonne bande (5GHz vs 2.4GHz)
2. Changez le canal WiFi de votre routeur
3. Mettez à jour le firmware :
```bash
sudo apt update
sudo apt install linux-firmware
```

#### Mot de passe WiFi refusé (alors qu'il est correct)

**Causes :**
- Problème de chiffrement (WPA2/WPA3)
- Configuration réseau corrompue

**Solutions :**
```bash
# Supprimer la connexion enregistrée
nm-connection-editor
# Supprimez la connexion problématique

# Recréez la connexion manuellement
```

### Carte WiFi non détectée du tout

Si votre carte WiFi n'apparaît nulle part :

**Vérifications matérielles :**
1. Assurez-vous que la carte est bien installée (PC fixe)
2. Vérifiez le BIOS : la carte WiFi est-elle activée ?
3. Sur certains portables, il y a un bouton physique WiFi

**Vérifications logicielles :**
```bash
# Lister tous les périphériques réseau
ip link show

# Vérifier les modules du noyau
lsmod | grep -i wifi
lsmod | grep -i 80211

# Réinstaller les firmwares
sudo apt install --reinstall linux-firmware
```

---

## Bonnes pratiques générales

### Avant d'installer un pilote propriétaire

1. ✅ **Créer un snapshot Timeshift** (sauvegarde système)
2. ✅ **Connecter l'ordinateur au secteur** (portable)
3. ✅ **Utiliser une connexion réseau stable**
4. ✅ **Fermer les applications en cours**
5. ✅ **Noter la version du pilote actuel** (au cas où)

### Après installation

1. ✅ **Toujours redémarrer** (surtout pour les pilotes graphiques)
2. ✅ **Vérifier le bon fonctionnement**
3. ✅ **Tester les performances** (benchmarks simples)
4. ✅ **Garder le système à jour**

### En cas de problème

1. 🔧 **Ne pas paniquer** : les problèmes sont généralement réversibles
2. 🔧 **Démarrer en mode recovery** si nécessaire
3. 🔧 **Revenir au pilote libre** via le Gestionnaire
4. 🔧 **Consulter les forums** Linux Mint en français
5. 🔧 **Restaurer un snapshot Timeshift** en dernier recours

### Maintenir ses pilotes à jour

**Pilotes via le Gestionnaire :**
- Mis à jour automatiquement avec le système
- Vérifiez régulièrement le Gestionnaire pour les nouvelles versions

**Commande manuelle :**
```bash
sudo ubuntu-drivers autoinstall
```

---

## Tableau récapitulatif

| Matériel | Pilote libre | Pilote propriétaire | Recommandation |
|----------|--------------|---------------------|----------------|
| **NVIDIA récent** | nouveau | nvidia-driver-XXX | Propriétaire pour gaming |
| **NVIDIA ancien** | nouveau | nvidia-driver-390/470 | Propriétaire si 3D nécessaire |
| **AMD récent** | amdgpu | AMDGPU-PRO | Libre (amdgpu) suffit |
| **AMD ancien** | radeon | - | Libre (radeon) |
| **Intel GPU** | i915 | - | Libre (excellente) |
| **WiFi Intel** | iwlwifi | - | Libre (excellente) |
| **WiFi Broadcom** | b43 | bcmwl | Propriétaire recommandé |
| **WiFi Realtek** | rtl8xxx | - | Libre généralement |

---

## Ressources et aide

### Documentation officielle
- **NVIDIA :** https://www.nvidia.com/en-us/drivers/unix/
- **AMD :** https://www.amd.com/en/support/linux-drivers
- **Forums Linux Mint :** https://forums.linuxmint.com/

### Commandes de diagnostic utiles

```bash
# Informations système complètes
inxi -Fxz

# Informations graphiques
inxi -G

# Informations réseau
inxi -N

# Informations matériel
sudo lshw -short

# Modules du noyau chargés
lsmod

# Messages du noyau (erreurs)
dmesg | grep -i error
dmesg | grep -i firmware
```

---

## Conclusion

Les pilotes propriétaires sont parfois nécessaires pour tirer le meilleur parti de votre matériel sous Linux Mint :

**Points clés :**
- **NVIDIA** : Les pilotes propriétaires sont presque toujours recommandés
- **AMD** : Les pilotes libres sont excellents, propriétaires rarement nécessaires
- **WiFi** : Broadcom nécessite des pilotes propriétaires, Intel fonctionne parfaitement avec les pilotes libres

Le **Gestionnaire de pilotes** de Linux Mint rend l'installation simple et sûre. N'hésitez pas à expérimenter : vous pouvez toujours revenir en arrière !

Dans le prochain chapitre, nous aborderons la **gestion des imprimantes et scanners**, un autre aspect important du support matériel.

⏭️ [Gestion de l'imprimante et du scanner](/12-materiel-et-pilotes/03-gestion-de-limprimante-et-du-scanner.md)
