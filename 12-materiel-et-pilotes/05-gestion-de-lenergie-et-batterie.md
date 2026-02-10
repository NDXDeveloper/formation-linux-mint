🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 12.5 Gestion de l'énergie et batterie (laptop)

## Introduction

La **gestion de l'énergie** est essentielle pour les ordinateurs portables. Une bonne configuration vous permet de :
- **Maximiser l'autonomie** de votre batterie
- **Prolonger la durée de vie** de la batterie
- **Réduire la consommation électrique** et la chaleur
- **Adapter les performances** selon vos besoins (sur batterie ou secteur)

Linux Mint offre d'excellents outils pour gérer efficacement l'alimentation de votre laptop, souvent **mieux que Windows** !

---

## Comprendre la gestion de l'énergie

### Les différents états d'alimentation

Votre ordinateur portable peut fonctionner en plusieurs modes :

#### Sur secteur (branché)
- **Performances maximales**
- Processeur à pleine vitesse
- Luminosité élevée
- Pas de restriction de consommation
- Idéal pour tâches intensives (jeux, montage vidéo)

#### Sur batterie (débranché)
- **Mode économie d'énergie** activé
- Processeur bridé (vitesse réduite)
- Luminosité automatiquement réduite
- WiFi en mode économie
- Disque dur ralenti
- Priorité à l'autonomie

### Les modes de veille

Linux propose plusieurs modes d'économie d'énergie :

#### Suspension (Sleep / Suspend)
**Qu'est-ce que c'est ?**
- L'ordinateur se met en "**veille**"
- L'écran s'éteint
- Le processeur et la plupart des composants se mettent en pause
- La RAM reste **alimentée** (conserve vos données)
- Consommation très faible (quelques watts)

**Quand l'utiliser ?**
- Pauses courtes (10 minutes à quelques heures)
- Vous revenez rapidement travailler
- Réveil quasi instantané (2-3 secondes)

**Comment ?**
- Fermez le capot du laptop
- Menu → Verrouiller → Mettre en veille
- Raccourci clavier défini dans les paramètres

#### Hibernation (Hibernate)
**Qu'est-ce que c'est ?**
- L'ordinateur enregistre l'état complet de la RAM sur le disque dur
- Puis s'éteint **complètement**
- Consommation : **0 watt** (comme éteint)
- Au rallumage, restaure exactement l'état précédent

**Quand l'utiliser ?**
- Absences longues (plusieurs heures, jours)
- Batterie très faible
- Transport du laptop
- Maximum d'économie d'énergie

**Inconvénients :**
- Réveil plus lent (10-30 secondes)
- Nécessite une partition swap de taille suffisante
- Pas toujours activée par défaut sur Linux Mint

#### Veille hybride (Hybrid Sleep)
- Combine suspension et hibernation
- Rarement utilisée sous Linux
- Plus courante sur Windows

---

## Interface de gestion de l'énergie de Linux Mint

### Accéder aux paramètres d'alimentation

**Méthode 1 : Via le menu système**
1. Cliquez sur le **Menu**
2. **Préférences** → **Gestion de l'alimentation**

**Méthode 2 : Via l'icône de batterie**
1. Clic sur l'**icône de batterie** dans la barre de tâches
2. Sélectionnez "**Paramètres d'alimentation**"

**Méthode 3 : Via les paramètres système**
1. Menu → **Paramètres système**
2. Section "**Matériel**" → **Alimentation**

### L'icône de batterie

L'icône dans la barre de tâches vous donne des informations rapides :

**Indicateurs visuels :**
- **Batterie avec prise** : Sur secteur, en charge
- **Batterie pleine** : Chargée à 100%
- **Batterie à moitié** : Niveau moyen
- **Batterie faible (rouge)** : Niveau critique (< 10%)
- **Pourcentage affiché** : Charge exacte

**Au survol de la souris :**
- Pourcentage de charge actuel
- Temps restant estimé (sur batterie)
- Temps jusqu'à charge complète (sur secteur)
- État : "En charge", "Décharge", "Chargée"

---

## Configuration des paramètres d'alimentation

### Onglet "Secteur" (Sur secteur branché)

**Luminosité de l'écran :**
- Curseur pour définir la luminosité par défaut
- Sur secteur : vous pouvez mettre au maximum (100%)

**Mise en veille de l'écran :**
- **Éteindre l'écran après** : Temps avant extinction de l'écran
  - Recommandé : 10-15 minutes
  - "Jamais" si vous surveillez constamment l'écran

**Mise en veille automatique :**
- **Mettre en veille après** : Temps avant suspension automatique
  - Recommandé : 30 minutes à 1 heure
  - "Jamais" si vous laissez des tâches longues (téléchargements, compilations)

**Action lors de la fermeture du capot :**
- **Ne rien faire** : L'ordinateur continue de fonctionner (utile avec écran externe)
- **Mettre en veille** : Suspend l'ordinateur (recommandé)
- **Éteindre** : Arrêt complet
- **Verrouiller** : Verrouille la session mais ne suspend pas

**Bouton d'alimentation :**
- Définit l'action du bouton power :
  - Demander
  - Éteindre
  - Mettre en veille
  - Rien

### Onglet "Batterie" (Sur batterie)

**Luminosité de l'écran :**
- Généralement **réduite automatiquement** (70-80%)
- Économise beaucoup d'énergie (l'écran consomme 30-40% de la batterie)

**Réduire la luminosité du rétroéclairage :**
- Option pour diminuer encore plus après un certain temps
- Utile si vous lisez sans activité clavier/souris

**Mise en veille de l'écran :**
- **Plus court** que sur secteur
- Recommandé : 5-10 minutes

**Mise en veille automatique :**
- **Plus court** également
- Recommandé : 15-20 minutes
- Préserve la batterie lors des oublis

**Action lors de la fermeture du capot :**
- Généralement "**Mettre en veille**" (recommandé)

**Niveau critique de batterie :**
- **Action quand batterie critique** :
  - Mettre en veille (par défaut, recommandé)
  - Hiberner (si configuré)
  - Éteindre
- **Pourcentage critique** : Généralement 5-10%

**Notifications :**
- **Avertir quand batterie faible** : Oui (recommandé)
- **Pourcentage faible** : 15-20%

### Onglet "Général"

**Icône dans la zone de notification :**
- Toujours afficher (recommandé pour laptops)
- Masquer lorsque branché
- Ne jamais afficher

**Fonctionnalités d'économie d'énergie :**
- Activation/désactivation globale
- Gestion automatique secteur/batterie

---

## Surveiller l'état de la batterie

### Informations détaillées sur la batterie

**Clic droit sur l'icône batterie → Informations :**
- **Fabricant** : Marque de la batterie
- **Modèle** : Référence
- **Technologie** : Li-ion (Lithium-ion), Li-Po (Lithium-polymère)
- **État de santé** : Capacité actuelle vs capacité d'origine
- **Nombre de cycles** : Cycles de charge effectués
- **Tension** : Voltage actuel

**Interpréter l'état de santé :**
- **100-95%** : Batterie neuve ou excellente
- **94-80%** : Bon état, usure normale
- **79-60%** : Usure notable, autonomie réduite
- **< 60%** : Batterie vieillissante, envisager remplacement

**Cycles de charge :**
- 1 cycle = décharge complète de 100% à 0%
- Batteries Li-ion : 300-500 cycles avant dégradation notable
- Batteries de qualité : 800-1000 cycles

### Ligne de commande : informations batterie

```bash
# Informations complètes sur la batterie
upower -i /org/freedesktop/UPower/devices/battery_BAT0

# Ou avec acpi
sudo apt install acpi  
acpi -V  

# État détaillé
cat /sys/class/power_supply/BAT0/status  
cat /sys/class/power_supply/BAT0/capacity  
cat /sys/class/power_supply/BAT0/capacity_level  
```

**Exemple de sortie upower :**
```
  native-path:          BAT0
  vendor:               Samsung
  model:                SR Real Battery
  serial:               12345
  power supply:         yes
  updated:              sam. 30 nov. 2024 15:30:00 (3 seconds ago)
  has history:          yes
  has statistics:       yes
  battery
    present:             yes
    rechargeable:        yes
    state:               discharging
    warning-level:       none
    energy:              45,2 Wh
    energy-empty:        0 Wh
    energy-full:         52,3 Wh
    energy-full-design:  60 Wh
    energy-rate:         12,5 W
    voltage:             11,4 V
    time to empty:       3,6 hours
    percentage:          86%
    capacity:            87,2%
    technology:          lithium-ion
    icon-name:          'battery-full-symbolic'
```

**Points importants :**
- **capacity** : Santé de la batterie (87.2% ici)
- **energy-full** : Capacité actuelle (52.3 Wh)
- **energy-full-design** : Capacité d'origine (60 Wh)
- **time to empty** : Autonomie restante estimée

---

## TLP : Optimisation avancée de l'énergie

### Qu'est-ce que TLP ?

**TLP** (Linux Advanced Power Management) est un outil puissant qui optimise automatiquement la gestion de l'énergie sous Linux.

**Avantages :**
- ✅ **Configuration automatique** : Fonctionne dès l'installation
- ✅ **Optimisations multiples** : CPU, GPU, disques, USB, WiFi, Bluetooth
- ✅ **Profils secteur/batterie** : Ajustement automatique
- ✅ **Gain d'autonomie** : 20-40% d'autonomie en plus selon usage
- ✅ **Gratuit et open source**

**Idéal pour :**
- Utilisateurs souhaitant maximiser l'autonomie
- Laptops avec batterie faible
- Pas de configuration complexe nécessaire

### Installation de TLP

```bash
# Mise à jour des paquets
sudo apt update

# Installation de TLP
sudo apt install tlp tlp-rdw

# Démarrer TLP
sudo tlp start

# Activer au démarrage (automatique après installation)
sudo systemctl enable tlp
```

**Important :** TLP entre parfois en conflit avec d'autres outils de gestion d'énergie. Si vous utilisez **laptop-mode-tools**, désinstallez-le :
```bash
sudo apt remove laptop-mode-tools
```

### Utilisation de TLP

**TLP fonctionne automatiquement** après installation, sans configuration nécessaire !

**Vérifier le statut :**
```bash
sudo tlp-stat -s
```

**Voir les statistiques détaillées :**
```bash
sudo tlp-stat
```

Cette commande affiche :
- État de TLP (actif/inactif)
- Mode actuel (AC/Batterie)
- Configuration CPU
- État des périphériques
- Consommation actuelle

**Activer manuellement le mode batterie (test) :**
```bash
sudo tlp bat
```

**Activer manuellement le mode secteur :**
```bash
sudo tlp ac
```

### Configuration de TLP (avancé)

TLP a des paramètres par défaut excellents, mais vous pouvez les personnaliser.

**Fichier de configuration :**
```bash
sudo nano /etc/tlp.conf
```

**Paramètres intéressants :**

```bash
# Fréquence CPU sur batterie (en %)
CPU_SCALING_MIN_FREQ_ON_BAT=800000  
CPU_SCALING_MAX_FREQ_ON_BAT=2000000  

# Régulateur CPU (governor)
CPU_SCALING_GOVERNOR_ON_AC=performance  
CPU_SCALING_GOVERNOR_ON_BAT=powersave  

# Désactiver Bluetooth sur batterie
DEVICES_TO_DISABLE_ON_BAT="bluetooth"

# Timeout WiFi en économie d'énergie
WIFI_PWR_ON_BAT=on

# USB autosuspend
USB_AUTOSUSPEND=1

# Niveau de charge maximal (pour prolonger la vie de la batterie)
# Arrête la charge à 80% au lieu de 100%
START_CHARGE_THRESH_BAT0=75  
STOP_CHARGE_THRESH_BAT0=80  
```

**Appliquer les changements :**
```bash
sudo tlp start
```

> **Note :** La limitation de charge (STOP_CHARGE_THRESH) ne fonctionne que sur certains laptops (ThinkPad, certains Dell, etc.).

### TLPUI : Interface graphique pour TLP

Pour configurer TLP graphiquement :

```bash
# Installation
sudo add-apt-repository ppa:linuxuprising/apps  
sudo apt update  
sudo apt install tlpui  

# Lancement
sudo tlpui
```

**Avantages :**
- Interface intuitive
- Explications pour chaque paramètre
- Modification facile des réglages
- Idéal pour débutants

---

## Autres outils de gestion d'énergie

### PowerTop

**PowerTop** est un outil de diagnostic de consommation énergétique développé par Intel.

**Installation :**
```bash
sudo apt install powertop
```

**Utilisation :**
```bash
sudo powertop
```

**Interface PowerTop :**

**Onglet "Overview" :**
- Consommation en watts (W)
- Estimation d'autonomie
- Liste des processus énergivores

**Onglet "Idle stats" :**
- Temps passé dans chaque état C du processeur
- Plus le C-state est élevé, plus l'économie est grande

**Onglet "Frequency stats" :**
- Distribution des fréquences CPU
- Vérifier si le CPU descend bien en fréquence

**Onglet "Tunables" :**
- Suggestions d'optimisation
- Appuyez sur **Entrée** pour activer/désactiver

**Générer un rapport HTML :**
```bash
sudo powertop --html=rapport_energie.html
```

**Calibration (recommandé au premier usage) :**
```bash
# Déconnectez TOUT : souris, clavier USB, etc.
# Fermez toutes les applications
sudo powertop --calibrate
# Laissez l'ordinateur seul 10-15 minutes
```

### laptop-mode-tools (alternative à TLP)

**⚠️ Ne PAS installer si TLP est déjà installé !**

```bash
sudo apt install laptop-mode-tools
```

**Moins recommandé que TLP** car :
- Configuration plus complexe
- Moins actif en développement
- TLP est généralement meilleur

### Auto-cpufreq

**Auto-cpufreq** ajuste automatiquement les fréquences du CPU selon la charge.

**Installation :**
```bash
git clone https://github.com/AdnanHodzic/auto-cpufreq.git  
cd auto-cpufreq && sudo ./auto-cpufreq-installer  
```

**Utilisation :**
```bash
# Voir les statistiques
sudo auto-cpufreq --stats

# Activer le service
sudo auto-cpufreq --install

# Moniteur en temps réel
sudo auto-cpufreq --monitor
```

---

## Optimisation manuelle de l'autonomie

### Réduire la luminosité de l'écran

**L'écran est le plus gros consommateur d'énergie (30-50% de la batterie) !**

**Réglage :**
- Utilisez les touches **Fn + F5/F6** (ou similaire)
- Ou clic sur l'icône batterie → Curseur de luminosité
- **Recommandation** : 50-70% en intérieur, suffisant pour la plupart des usages

**Bonus :** Réduire la luminosité ménage aussi vos yeux !

### Désactiver le rétroéclairage du clavier

Si votre laptop a un clavier rétroéclairé :
- Désactivez-le sur batterie
- Ou réduisez l'intensité
- Gain : 1-3% d'autonomie

```bash
# Éteindre le rétroéclairage clavier (Dell, certains laptops)
echo 0 | sudo tee /sys/class/leds/dell::kbd_backlight/brightness

# Allumer à 50%
echo 1 | sudo tee /sys/class/leds/dell::kbd_backlight/brightness
```

### Fermer les applications inutilisées

**Processus gourmands :**
- Navigateurs avec beaucoup d'onglets (Chrome/Firefox)
- Applications Electron (Discord, Slack, VS Code)
- Lecteurs vidéo
- Machines virtuelles

**Surveillance :**
```bash
# Voir la consommation par processus
top
# Ou mieux : htop
sudo apt install htop  
htop  
```

**Tuer un processus gourmand :**
- Dans htop : Sélectionnez le processus → F9 → Entrée

### Utiliser le WiFi plutôt que la 4G/5G USB

Si vous utilisez un modem USB pour Internet :
- Le WiFi consomme **beaucoup moins** qu'un modem 4G/5G
- Privilégiez le WiFi quand disponible

### Déconnecter les périphériques USB inutiles

Chaque périphérique USB consomme :
- Souris USB : ~1W
- Clavier USB : ~0.5W
- Disque dur USB : ~5-10W
- Hub USB : ~2-5W

**Débranchez :**
- Souris (utilisez le trackpad)
- Disques durs externes
- Clés USB
- Webcam externe

**Gain potentiel :** 5-15% d'autonomie

### Activer le mode avion quand le réseau n'est pas nécessaire

**WiFi + Bluetooth** consomment même en idle.

**Activer le mode avion :**
- Clic sur l'icône réseau → **Mode avion**
- Ou : Fn + touche mode avion (icône d'avion)

**Gain :** 5-10% d'autonomie

**Quand l'utiliser :**
- Rédaction de documents hors ligne
- Lecture de fichiers locaux
- Codage sans documentation en ligne

### Utiliser des thèmes sombres (écrans OLED)

**Sur écrans OLED uniquement** (pas LCD) :
- Les pixels noirs sont **éteints**
- Thème sombre = moins de pixels allumés = moins de consommation

**Activer le thème sombre :**
1. Menu → Préférences → **Thèmes**
2. Sélectionnez un thème sombre (Mint-Y-Dark, etc.)

**Gain sur OLED :** 10-20% d'autonomie

### Réduire la performance du CPU

**Passer en mode économie d'énergie :**
```bash
# Installer cpufrequtils
sudo apt install cpufrequtils

# Passer en mode powersave
sudo cpufreq-set -g powersave

# Revenir en performance
sudo cpufreq-set -g performance
```

**Ou via l'interface graphique (si disponible) :**
- Menu → Préférences → Puissance du processeur
- Sélectionnez "Économie d'énergie"

---

## Suspension et hibernation

### Configurer la suspension

**La suspension fonctionne généralement sans configuration.**

**Tester la suspension :**
1. Menu → Verrouiller → **Mettre en veille**
2. L'écran s'éteint, LED d'alimentation clignote
3. Appuyez sur n'importe quelle touche pour réveiller

**Problèmes de suspension :**

Si le laptop ne se met pas en veille ou ne se réveille pas correctement :

```bash
# Vérifier les paramètres de suspension
sudo systemctl status suspend.target

# Tester manuellement
sudo systemctl suspend

# Voir les logs d'erreur
journalctl -b | grep -i suspend
```

**Désactiver la suspension sur fermeture du capot :**

Si vous voulez utiliser le laptop avec le capot fermé et un écran externe :

```bash
sudo nano /etc/systemd/logind.conf
```

Modifiez :
```
HandleLidSwitch=ignore  
HandleLidSwitchExternalPower=ignore  
```

Redémarrez le service :
```bash
sudo systemctl restart systemd-logind
```

### Activer l'hibernation

**L'hibernation n'est pas toujours activée par défaut sur Linux Mint.**

#### Prérequis : partition swap suffisante

La partition swap doit être **au moins égale à la taille de votre RAM**.

**Vérifier la taille du swap :**
```bash
free -h  
swapon --show  
```

**Si swap insuffisant, créer un fichier swap :**
```bash
# Créer un fichier swap de 8 Go (ajustez selon votre RAM)
sudo fallocate -l 8G /swapfile  
sudo chmod 600 /swapfile  
sudo mkswap /swapfile  
sudo swapon /swapfile  

# Rendre permanent
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

#### Tester l'hibernation

```bash
# Tester l'hibernation
sudo systemctl hibernate
```

Si ça fonctionne, votre laptop s'éteint complètement. Au rallumage, tout est restauré.

#### Activer l'hibernation dans le menu

```bash
# Installer le paquet nécessaire
sudo apt install hibernate

# Autoriser l'hibernation
sudo nano /etc/polkit-1/localauthority/50-local.d/com.ubuntu.enable-hibernate.pkla
```

Ajoutez :
```
[Re-enable hibernate by default in upower]
Identity=unix-user:*  
Action=org.freedesktop.upower.hibernate  
ResultActive=yes  

[Re-enable hibernate by default in logind]
Identity=unix-user:*  
Action=org.freedesktop.login1.hibernate;org.freedesktop.login1.handle-hibernate-key;org.freedesktop.login1.hibernate-multiple-sessions;org.freedesktop.login1.hibernate-ignore-inhibit  
ResultActive=yes  
```

Redémarrez l'ordinateur.

L'option **Hiberner** devrait maintenant apparaître dans le menu.

---

## Prolonger la durée de vie de la batterie

### Comprendre le vieillissement de la batterie

**Facteurs de dégradation :**
1. **Cycles de charge** : Chaque cycle use la batterie
2. **Température élevée** : Accélère le vieillissement
3. **Charge à 100% prolongée** : Stress pour la batterie
4. **Décharge complète fréquente** : Endommage les cellules
5. **Stockage à pleine charge** : Dégradation plus rapide

### Bonnes pratiques

#### 1. Éviter les extrêmes (0% et 100%)

**Idéal :**
- Maintenez la charge entre **20% et 80%**
- Ne laissez pas descendre sous 20%
- Ne gardez pas à 100% en permanence

**Pourquoi ?**
- Les batteries Li-ion préfèrent les charges partielles
- 100% et 0% stressent la chimie de la batterie

#### 2. Limiter la charge à 80% (si supporté)

**Avec TLP :**
```bash
sudo nano /etc/tlp.conf
```

Ajoutez (fonctionne sur ThinkPad, certains Dell et ASUS) :
```bash
START_CHARGE_THRESH_BAT0=75  
STOP_CHARGE_THRESH_BAT0=80  
```

**Ou avec ASUS Battery Health Charging :**
```bash
# Pour laptops ASUS
echo 80 | sudo tee /sys/class/power_supply/BAT0/charge_control_end_threshold
```

**Ou avec un outil spécifique au fabricant.**

#### 3. Éviter la chaleur

**La chaleur est l'ennemi n°1 des batteries !**

**Conseils :**
- ✅ Utilisez sur surface dure et plane
- ✅ Nettoyez régulièrement les grilles de ventilation
- ✅ Utilisez un support ventilé
- ❌ N'utilisez pas sur lit, coussin, genoux prolongés
- ❌ Évitez le plein soleil
- ❌ Ne laissez pas dans une voiture chaude

**Surveiller la température :**
```bash
# Installer sensors
sudo apt install lm-sensors  
sudo sensors-detect  # Répondez "yes" à tout  

# Voir les températures
sensors
```

#### 4. Calibration de la batterie (tous les 3-6 mois)

**Procédure :**
1. Chargez à **100%**
2. Utilisez jusqu'à **5-10%** (pas 0%)
3. Rechargez complètement à **100%** sans interruption
4. Cela recalibre l'indicateur de niveau de batterie

> **Important :** Ne faites pas cela trop souvent (max 2-4 fois par an).

#### 5. Stockage longue durée

Si vous n'utilisez pas le laptop pendant plusieurs semaines :
- Chargez à **50-60%** avant stockage
- Stockez dans un endroit frais et sec
- Rechargez tous les 2-3 mois à 50%

#### 6. Utiliser le mode "Conservation" (certains fabricants)

Certains laptops (Lenovo, ASUS) ont un mode "conservation" :
- Limite la charge à 55-60%
- Idéal si vous utilisez principalement sur secteur
- Prolonge considérablement la durée de vie

**Activer sur Lenovo ThinkPad :**
```bash
echo 1 | sudo tee /sys/bus/platform/drivers/ideapad_acpi/VPC2004:00/conservation_mode
```

---

## Problèmes courants et solutions

### La batterie se décharge trop vite

**Diagnostic :**

1. **Vérifier les processus gourmands :**
```bash
top
# Ou
htop
```

2. **Identifier les applications énergivores avec PowerTop :**
```bash
sudo powertop
```

3. **Vérifier l'état de la batterie :**
```bash
upower -i /org/freedesktop/UPower/devices/battery_BAT0 | grep capacity
```

Si la capacité est < 70%, la batterie est usée.

**Solutions :**
- Installez TLP
- Réduisez la luminosité
- Fermez les applications inutiles
- Désactivez le WiFi/Bluetooth quand non utilisé
- Vérifiez qu'aucun processus ne tourne en boucle

### La batterie ne se charge pas (ou très lentement)

**Causes possibles :**
1. **Chargeur défectueux** : Testez avec un autre chargeur
2. **Port de charge sale** : Nettoyez délicatement
3. **Batterie en fin de vie** : Vérifier la santé
4. **Limitation de charge activée** : Vérifiez les seuils TLP

**Vérifier l'état de charge :**
```bash
acpi -V
```

Si "status: Not charging" alors que branché :
- Peut être normal si charge > 80% et seuil configuré
- Ou batterie défectueuse

### L'ordinateur ne se réveille pas de la suspension

**Solutions :**

1. **Désactiver la suspension du GPU :**
```bash
sudo nano /etc/default/grub
```

Ajoutez `nouveau.noaccel=1` ou `i915.enable_psr=0` à `GRUB_CMDLINE_LINUX_DEFAULT`

```bash
sudo update-grub
```

2. **Désactiver la suspension USB :**
```bash
sudo nano /etc/tlp.conf
```

Changez :
```bash
USB_AUTOSUSPEND=0
```

3. **Mettre à jour le BIOS** (souvent résout les problèmes de veille)

### Estimation d'autonomie incorrecte

**Normal au début :**
- Linux apprend votre usage
- L'estimation s'améliore après quelques cycles

**Forcer une recalibration :**
- Décharge complète puis recharge complète (voir section calibration)

### Le laptop ne s'éteint pas complètement

**Solutions :**

```bash
sudo systemctl poweroff
```

Ou modifier GRUB :
```bash
sudo nano /etc/default/grub
```

Ajoutez `acpi=force` à `GRUB_CMDLINE_LINUX_DEFAULT`

```bash
sudo update-grub
```

---

## Moniteurs et statistiques de batterie

### Applications graphiques

#### GNOME Power Statistics
Pré-installé sur Linux Mint (Cinnamon).

**Accès :** Menu → Statistiques d'alimentation

**Informations :**
- Graphiques de décharge/charge
- Historique de consommation
- Prédiction d'autonomie

#### BatteryMon

```bash
sudo apt install batterymon
```

Affiche l'icône de batterie avec des informations détaillées.

### Ligne de commande

```bash
# Informations complètes
upower -i /org/freedesktop/UPower/devices/battery_BAT0

# Simple niveau
cat /sys/class/power_supply/BAT0/capacity

# État (Charging, Discharging, Full)
cat /sys/class/power_supply/BAT0/status

# Avec acpi
acpi -V

# Surveillance continue (toutes les 5 secondes)
watch -n 5 acpi
```

---

## Astuces et optimisations supplémentaires

### Désactiver les effets visuels

Les animations et effets consomment du GPU et donc de la batterie.

**Réduire les effets :**
1. Menu → Préférences → **Effets**
2. Désactivez les animations non essentielles
3. Ou passez en mode "Aucun effet"

### Utiliser un navigateur web léger

**Navigateurs par consommation (du plus au moins gourmand) :**
1. **Chrome** : Très gourmand
2. **Firefox** : Moyen
3. **Chromium** : Moyen
4. **Brave** : Optimisé pour batterie (recommandé)
5. **Falkon/Midori** : Très légers

**Extensions Firefox pour économiser :**
- **Auto Tab Discard** : Suspend les onglets inactifs
- **uBlock Origin** : Bloque les pubs (moins de ressources)

### Utiliser des applications natives plutôt qu'Electron

**Electron** (Discord, Slack, VS Code) consomme beaucoup.

**Alternatives légères :**
- Discord → Utiliser dans le navigateur ou Ripcord
- Slack → Utiliser dans le navigateur
- VS Code → VSCodium ou Geany/Gedit

### Limiter les applications au démarrage

**Désactiver les applications inutiles au démarrage :**
1. Menu → Préférences → **Applications au démarrage**
2. Décochez les applications non essentielles

Moins d'applications = démarrage plus rapide + moins de consommation en arrière-plan.

---

## Benchmark et comparaisons

### Mesurer l'autonomie réelle

**Test standardisé :**
1. Chargez à 100%
2. Débranchez
3. Lancez un scénario d'usage (navigation web, vidéo, etc.)
4. Notez le temps jusqu'à 5%

**Scénarios courants :**
- **Navigation web** : 70% luminosité, WiFi actif
- **Vidéo locale** : Lecture VLC, WiFi désactivé
- **Bureautique** : LibreOffice, luminosité 50%

**Comparer avec/sans TLP :**
- Testez l'autonomie sans TLP
- Installez TLP
- Testez à nouveau
- Comparez le gain

**Résultat attendu avec TLP :** +20 à 40% d'autonomie

---

## Ressources et outils avancés

### Scripts personnalisés

**Script pour basculer entre modes performance/économie :**

```bash
#!/bin/bash
# Script toggle-power.sh

if [ "$(cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor)" == "performance" ]; then
    echo "Passage en mode économie d'énergie..."
    echo powersave | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
else
    echo "Passage en mode performance..."
    echo performance | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
fi
```

**Rendre exécutable et utiliser :**
```bash
chmod +x toggle-power.sh
./toggle-power.sh
```

### Profils d'alimentation personnalisés

Créez des profils selon vos besoins :
- **Maximum autonomie** : TLP + luminosité 40% + WiFi désactivé
- **Bureautique** : TLP + luminosité 60%
- **Performance** : Désactiver TLP + luminosité 100%

### Documentation et communauté

**Ressources officielles :**
- Documentation TLP : https://linrunner.de/tlp/
- Wiki ArchLinux (excellent) : https://wiki.archlinux.org/title/Power_management
- Forums Linux Mint : https://forums.linuxmint.com/

**Commandes d'aide :**
```bash
man tlp  
man powertop  
man acpi  
```

---

## Conclusion

La gestion de l'énergie sous Linux Mint est **excellente** et souvent **meilleure que Windows** avec les bons outils.

**Points clés à retenir :**

- ✅ **Installation de TLP** : Gain immédiat de 20-40% d'autonomie
- ✅ **Réduire la luminosité** : L'optimisation la plus efficace
- ✅ **Maintenir la batterie entre 20-80%** : Prolonge la durée de vie
- ✅ **Surveiller les processus gourmands** : Avec htop ou PowerTop
- ✅ **Éviter la chaleur** : Ennemi n°1 des batteries

**Avec une bonne configuration :**
- Autonomie maximisée
- Batterie qui dure des années
- Laptop silencieux et frais
- Performance adaptée à vos besoins

**Testez, mesurez, ajustez !** Chaque laptop est différent et votre usage aussi. Trouvez le bon équilibre entre performance et autonomie.

Dans le prochain chapitre, nous découvrirons **PipeWire**, le serveur audio moderne de Linux.

⏭️ [PipeWire : Le nouveau serveur audio moderne](/12-materiel-et-pilotes/06-pipewire-le-nouveau-serveur-audio-moderne.md)
