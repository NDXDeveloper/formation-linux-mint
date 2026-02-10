🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 14.8 GameMode pour performances

## Introduction

GameMode est un daemon (service en arrière-plan) développé par Feral Interactive qui optimise automatiquement votre système Linux pour offrir les meilleures performances gaming possibles. C'est l'équivalent du "Mode Jeu" de Windows, mais en plus puissant et personnalisable.

**GameMode, c'est :**
- 🚀 Optimisation automatique du système pendant le jeu
- ⚡ Activation/désactivation transparente
- 🎯 Priorisation du processus du jeu
- 🔧 Configuration du gouverneur CPU
- 💪 Optimisations GPU (NVIDIA/AMD)
- 📊 Impact mesurable sur les performances
- 🆓 100% gratuit et open-source

**Pourquoi GameMode est indispensable ?**
- Amélioration FPS de 5 à 15% selon le jeu
- Réduction du input lag (latence)
- Stabilisation des performances (moins de micro-stutters)
- Aucune intervention manuelle nécessaire
- Compatible avec tous les launchers de jeux

## Comment fonctionne GameMode ?

### Principe de fonctionnement

Quand vous lancez un jeu avec GameMode :

1. **GameMode détecte** le lancement du jeu
2. **Active les optimisations** :
   - Change le gouverneur CPU à "performance"
   - Augmente la priorité du processus du jeu
   - Désactive le screensaver
   - Applique des optimisations GPU
   - Réduit la priorité des processus en arrière-plan
3. **Le jeu tourne** avec des performances optimales
4. **À la fermeture du jeu**, GameMode restaure la configuration normale

### Optimisations appliquées par défaut

**CPU** :
- Gouverneur CPU → **Performance** (fréquence maximale)
- Nice value du processus → **-10** (haute priorité)
- Core parking désactivé (tous les cœurs disponibles)

**GPU** :
- Mode performance activé (NVIDIA/AMD)
- Optimisations spécifiques au pilote

**Système** :
- Screensaver désactivé
- I/O scheduler optimisé
- Processus en arrière-plan dé-priorisés

**Tout cela automatiquement, sans configuration !**

## Installation de GameMode

### Vérifier si GameMode est déjà installé

```bash
# Vérifier l'installation
gamemoded --version

# Si installé, affiche la version
# Si pas installé, affiche "command not found"
```

### Installation via APT (recommandée)

```bash
# Mettre à jour les dépôts
sudo apt update

# Installer GameMode
sudo apt install gamemode

# Installer aussi les outils de vérification
sudo apt install gamemode-daemon
```

### Vérifier l'installation

```bash
# Vérifier que le service est actif
systemctl --user status gamemoded

# Devrait afficher "active (running)"
```

### Démarrer GameMode si nécessaire

```bash
# Démarrer le daemon
systemctl --user start gamemoded

# Activer au démarrage (normalement déjà fait)
systemctl --user enable gamemoded
```

## Utilisation de GameMode

### Avec Steam

GameMode peut être activé automatiquement pour tous vos jeux Steam ou jeu par jeu.

#### Pour un jeu spécifique

1. Ouvrez **Steam**
2. **Bibliothèque** → Clic droit sur le jeu → **Propriétés**
3. **Options de lancement**
4. Ajoutez : `gamemoderun %command%`

**Exemple complet avec MangoHud** :
```bash
gamemoderun mangohud %command%
```

**Exemple avec Proton et optimisations** :
```bash
PROTON_NO_ESYNC=0 PROTON_NO_FSYNC=0 gamemoderun mangohud %command%
```

#### Pour tous vos jeux Steam (méthode avancée)

```bash
# Créer un script wrapper
sudo nano /usr/local/bin/steam-gamemode
```

Contenu du script :
```bash
#!/bin/bash
gamemoderun "$@"
```

Rendez-le exécutable :
```bash
sudo chmod +x /usr/local/bin/steam-gamemode
```

Puis dans Steam, utilisez ce script au lieu de `%command%`.

### Avec Lutris

GameMode s'intègre parfaitement à Lutris.

#### Activation globale (tous les jeux)

1. Ouvrez **Lutris**
2. ☰ (menu hamburger) → **Préférences**
3. Onglet **System options**
4. **Enable Feral GameMode** : Cochez la case ✅

Tous vos jeux Lutris utilisent maintenant GameMode !

#### Pour un jeu spécifique

1. Clic droit sur le jeu → **Configure**
2. Onglet **System options**
3. **Enable Feral GameMode** : ✅

### Avec Heroic Games Launcher

#### Pour un jeu

1. Page du jeu → ⚙️ **Settings**
2. Onglet **Advanced** ou **Other**
3. **Enable Feral GameMode** : ON

#### Configuration globale

1. **Settings** (paramètres généraux)
2. **Advanced**
3. **Enable Feral GameMode** : ON

S'applique à tous les nouveaux jeux installés.

### Avec n'importe quel jeu (ligne de commande)

```bash
# Syntaxe de base
gamemoderun /chemin/vers/le/jeu

# Exemples
gamemoderun ./MonJeu  
gamemoderun wine MonJeu.exe  
gamemoderun retroarch  

# Avec des arguments
gamemoderun ./jeu --fullscreen --high-quality
```

### Avec des émulateurs

**RetroArch** :
```bash
gamemoderun retroarch
```

**PCSX2** :
```bash
gamemoderun pcsx2
```

**Dolphin** :
```bash
gamemoderun dolphin-emu
```

### Vérifier que GameMode est actif

**Pendant qu'un jeu tourne** :

```bash
# Vérifier le statut
gamemoded -s

# Devrait afficher :
# gamemode is active
# Process [PID] is registered
```

**Si aucun jeu ne tourne** :
```
gamemode is inactive
```

### Test rapide

```bash
# Lancer un programme simple avec GameMode
gamemoderun glxgears

# Dans un autre terminal
gamemoded -s

# Devrait afficher : gamemode is active
```

## Configuration de GameMode

GameMode fonctionne parfaitement avec sa configuration par défaut, mais vous pouvez le personnaliser.

### Fichier de configuration

**Emplacement** : `~/.config/gamemode.ini`

Si le fichier n'existe pas, créez-le :
```bash
mkdir -p ~/.config  
nano ~/.config/gamemode.ini  
```

### Configuration de base (recommandée pour débutants)

```ini
[general]
; Renice le processus du jeu (priorité)
renice=10

[gpu]
; Optimisations GPU automatiques
apply_gpu_optimisations=accept-responsibility  
gpu_device=0  

[cpu]
; Ne pas parker les cœurs CPU
park_cores=no
```

Cette configuration simple améliore déjà les performances.

### Configuration complète (avancée)

```ini
[general]
; Intervalle de polling (ms)
reaper_freq=5

; Nice value (0 à 20, plus bas = plus prioritaire)
renice=10

; DesiredGov : Gouverneur CPU quand GameMode actif
desiredgov=performance

; DefaultGov : Gouverneur CPU par défaut
defaultgov=powersave

[filter]
; Listes blanches et noires (optionnel)
whitelist=

[gpu]
; Optimisations GPU
apply_gpu_optimisations=accept-responsibility

; Index du GPU (0 par défaut)
gpu_device=0

; Niveau de performance AMD
amd_performance_level=high

; Performance NVIDIA (0 = auto, 1 = max)
nv_powermizer_mode=1

[cpu]
; Politique de parking des cœurs
park_cores=no

; Politique d'épinglage des threads
pin_policy=prefer-physical

[custom]
; Scripts personnalisés (optionnel)
start=notify-send "GameMode activé" -u low -t 2000  
end=notify-send "GameMode désactivé" -u low -t 2000  
```

### Explication des options principales

#### Section [general]

**renice** :
- Valeur entre 0 et 20
- Plus bas = plus haute priorité
- Recommandé : 10
- Formule réelle : -10 (donc priorité élevée)

**desiredgov** :
- `performance` : CPU à fréquence max (recommandé)
- `schedutil` : Ajustement intelligent
- `ondemand` : Ajustement dynamique

**defaultgov** :
- Gouverneur utilisé hors gaming
- `powersave` : Économie d'énergie (recommandé pour laptop)
- `schedutil` : Bon compromis

#### Section [gpu]

**apply_gpu_optimisations** :
- `accept-responsibility` : Active les optimisations GPU
- Fonctionne avec NVIDIA et AMD

**gpu_device** :
- `0` : Premier GPU (généralement le seul)
- `1` : Second GPU (si multi-GPU)

**amd_performance_level** :
- `auto` : Automatique
- `high` : Performance élevée (recommandé)
- `low` : Économie d'énergie

**nv_powermizer_mode** :
- `0` : Automatique
- `1` : Performance maximale (recommandé)

#### Section [cpu]

**park_cores** :
- `no` : Tous les cœurs actifs (recommandé)
- `yes` : Permet le parking (économie d'énergie)

**pin_policy** :
- `prefer-physical` : Préfère les cœurs physiques
- `prefer-efficiency` : Préfère les cœurs E (si CPU hybride)

#### Section [custom]

**start** et **end** :
- Commandes exécutées au début/fin
- Exemples : notifications, scripts, logging

**Exemples de scripts personnalisés** :

```ini
[custom]
; Notification au démarrage
start=notify-send "🎮 Gaming Mode" "Optimisations activées" -i gaming

; Notification à la fin
end=notify-send "💻 Mode Normal" "Optimisations désactivées" -i computer

; Activer RGB (si vous avez OpenRGB)
start=openrgb --profile gaming  
end=openrgb --profile normal  

; Désactiver compositeur (réduire latence)
start=killall picom  
end=picom &  
```

### Configuration pour laptop

```ini
[general]
renice=10  
desiredgov=performance  
defaultgov=powersave  

[gpu]
apply_gpu_optimisations=accept-responsibility  
gpu_device=0  

[cpu]
park_cores=no

[custom]
start=notify-send "Gaming Mode" "Sur batterie : monitorer la température !"
```

### Configuration pour desktop puissant

```ini
[general]
renice=15  
desiredgov=performance  
defaultgov=performance  

[gpu]
apply_gpu_optimisations=accept-responsibility  
amd_performance_level=high  
nv_powermizer_mode=1  

[cpu]
park_cores=no  
pin_policy=prefer-physical  

[custom]
start=echo performance | sudo tee /sys/class/drm/card0/device/power_dpm_force_performance_level
```

## Vérification des optimisations

### Vérifier le gouverneur CPU

**Sans jeu (GameMode inactif)** :
```bash
cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
```

Devrait afficher : `powersave` ou `schedutil`

**Pendant un jeu (GameMode actif)** :
```bash
# Lancer un jeu avec GameMode
gamemoderun glxgears &

# Vérifier le gouverneur
cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
```

Devrait afficher : `performance`

### Vérifier la priorité du processus

```bash
# Lister les processus avec priorité
ps -eo pid,ni,comm | grep glxgears

# Devrait afficher un nice value négatif (ex: -10)
```

### Vérifier les optimisations GPU (NVIDIA)

```bash
# Pendant qu'un jeu tourne avec GameMode
nvidia-smi -q -d PERFORMANCE

# Cherchez "Performance State" devrait être P0 (max performance)
```

### Vérifier les optimisations GPU (AMD)

```bash
# État du GPU
cat /sys/class/drm/card0/device/power_dpm_force_performance_level

# Devrait afficher : high ou manual
```

## Logs et debugging

### Activer les logs détaillés

```bash
# Éditer le service systemd
mkdir -p ~/.config/systemd/user/gamemoded.service.d/  
nano ~/.config/systemd/user/gamemoded.service.d/override.conf  
```

Contenu :
```ini
[Service]
Environment="GAMEMODED_LOG_LEVEL=1"
```

Rechargez :
```bash
systemctl --user daemon-reload  
systemctl --user restart gamemoded  
```

### Voir les logs

```bash
# Logs en temps réel
journalctl --user -u gamemoded -f

# Logs récents
journalctl --user -u gamemoded -n 50

# Logs complets
journalctl --user -u gamemoded --no-pager
```

### Exemple de logs

```
GameMode started for process [PID]  
CPU governor changed to performance  
Nice value set to -10  
GPU optimizations applied  
```

## Tests de performance

### Mesurer l'impact de GameMode

**Méthode 1 : Benchmarks**

1. **Sans GameMode** :
   ```bash
   # Lancer le benchmark
   glxgears -fullscreen
   # Noter les FPS
   ```

2. **Avec GameMode** :
   ```bash
   gamemoderun glxgears -fullscreen
   # Noter les FPS
   ```

3. **Comparez** : Amélioration typique de 5-15%

**Méthode 2 : Jeux réels**

Utilisez MangoHud pour comparer :

1. **Sans GameMode** :
   ```bash
   # Steam options de lancement
   mangohud %command%
   # Jouez 5 minutes, notez FPS moyen
   ```

2. **Avec GameMode** :
   ```bash
   gamemoderun mangohud %command%
   # Jouez 5 minutes dans la même zone
   ```

3. **Analysez** :
   - FPS moyen
   - FPS minimum
   - Frame time
   - Micro-stutters

### Résultats attendus

**Amélioration typique** :
- **FPS moyen** : +5 à 15%
- **FPS minimum** : +10 à 20% (plus stable)
- **Frame time** : Plus régulier
- **Input lag** : Réduit (perceptible en compétitif)

**Gains par type de jeu** :

| Type de jeu | Gain FPS | Gain stabilité |
|-------------|----------|----------------|
| FPS compétitifs | +10-15% | ⭐⭐⭐⭐⭐ |
| RPG/Solo | +5-10% | ⭐⭐⭐⭐ |
| Stratégie | +8-12% | ⭐⭐⭐⭐ |
| Indie/2D | +3-5% | ⭐⭐⭐ |

**Gains par matériel** :

| Matériel | Impact GameMode |
|----------|-----------------|
| CPU faible | ⭐⭐⭐⭐⭐ Énorme |
| CPU moyen | ⭐⭐⭐⭐ Important |
| CPU puissant | ⭐⭐⭐ Bon |
| GPU dédié | ⭐⭐⭐⭐ Important |
| GPU intégré | ⭐⭐⭐⭐⭐ Crucial |

## Problèmes courants et solutions

### GameMode ne s'active pas

**Vérifications** :

1. **Service actif ?**
   ```bash
   systemctl --user status gamemoded
   # Devrait être "active (running)"
   ```

2. **Démarrer le service** :
   ```bash
   systemctl --user start gamemoded
   systemctl --user enable gamemoded
   ```

3. **Réinstaller si nécessaire** :
   ```bash
   sudo apt install --reinstall gamemode
   ```

### "GameMode request rejected"

**Cause** : Problème de permissions

**Solution** :
```bash
# Vérifier les groupes
groups

# Ajouter au groupe gamemode (si existe)
sudo usermod -a -G gamemode $USER

# Redémarrer la session
# Se déconnecter et reconnecter
```

### Le gouverneur ne change pas

**Cause** : TLP ou autre outil de gestion d'énergie interfère

**Solution** :

```bash
# Si TLP est installé
sudo nano /etc/tlp.conf
```

Ajoutez ou modifiez :
```
CPU_SCALING_GOVERNOR_ON_AC=performance  
CPU_SCALING_GOVERNOR_ON_BAT=powersave  

# Permettre à GameMode de changer le gouverneur
CPU_BOOST_ON_AC=1  
CPU_BOOST_ON_BAT=0  
```

Rechargez TLP :
```bash
sudo tlp start
```

### Conflit avec d'autres optimiseurs

**cpufrequtils** :

Si vous avez installé cpufrequtils, désactivez-le :
```bash
sudo systemctl disable cpufrequtils  
sudo systemctl stop cpufrequtils  
```

GameMode gère mieux le gouverneur dynamiquement.

### Optimisations GPU ne fonctionnent pas

**NVIDIA** :

Vérifiez que `nvidia-settings` est installé :
```bash
sudo apt install nvidia-settings
```

**AMD** :

Permissions nécessaires :
```bash
# Ajouter au groupe video
sudo usermod -a -G video $USER

# Redémarrer
sudo reboot
```

### GameMode reste actif après fermeture du jeu

**Cause** : Le jeu ne s'est pas fermé proprement

**Solution** :
```bash
# Forcer l'arrêt de GameMode
killall gamemoded  
systemctl --user restart gamemoded  
```

## GameMode vs autres optimisations

### GameMode vs Governor manuel

**Governor manuel** :
```bash
echo performance | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
```

**Problèmes** :
- ❌ Reste actif après le jeu (consommation inutile)
- ❌ Nécessite commande manuelle
- ❌ Pas d'optimisations GPU
- ❌ Pas de gestion priorité processus

**GameMode** :
- ✅ Activation/désactivation automatique
- ✅ Optimisations multiples (CPU+GPU+priorité)
- ✅ Économie d'énergie hors gaming
- ✅ Transparent

**Conclusion** : GameMode est supérieur.

### GameMode + autres outils

**Combinaison recommandée** :

1. **GameMode** : Optimisation système
2. **MangoHud** : Monitoring
3. **Mesa drivers** (AMD) : Pilotes optimisés

**Exemple complet** (Steam) :
```bash
gamemoderun mangohud %command%
```

## Cas d'usage spécifiques

### Laptop sur batterie

```ini
[general]
renice=10
; Moins agressif sur batterie
desiredgov=schedutil  
defaultgov=powersave  

[gpu]
; Optimisations modérées
apply_gpu_optimisations=accept-responsibility

[cpu]
park_cores=no

[custom]
start=notify-send "Gaming sur batterie" "Attention à l'autonomie !"
```

### PC fixe gaming dédié

```ini
[general]
renice=15  
desiredgov=performance  
defaultgov=performance  

[gpu]
apply_gpu_optimisations=accept-responsibility  
amd_performance_level=high  
nv_powermizer_mode=1  

[cpu]
park_cores=no  
pin_policy=prefer-physical  
```

### Streaming + Gaming

```ini
[general]
renice=8  
desiredgov=performance  

[cpu]
park_cores=no

[custom]
; Augmenter priorité OBS aussi
start=renice -n -5 $(pgrep obs)
```

### Multi-GPU

```ini
[gpu]
apply_gpu_optimisations=accept-responsibility

; GPU 0 : Intel intégré
; GPU 1 : NVIDIA dédié
gpu_device=1

[custom]
; Forcer utilisation GPU dédié
start=nvidia-settings -a "[gpu:1]/GPUPowerMizerMode=1"
```

## Scripts utiles

### Script de test complet

```bash
#!/bin/bash
# test-gamemode.sh

echo "Test GameMode"  
echo "============="  

echo ""  
echo "1. Vérification installation..."  
if command -v gamemoded &> /dev/null; then  
    echo "✅ GameMode installé"
    gamemoded --version
else
    echo "❌ GameMode non installé"
    exit 1
fi

echo ""  
echo "2. Vérification service..."  
if systemctl --user is-active --quiet gamemoded; then  
    echo "✅ Service actif"
else
    echo "❌ Service inactif"
    systemctl --user start gamemoded
fi

echo ""  
echo "3. Test activation..."  
gamemoderun sleep 5 &  
sleep 1  
gamemoded -s  
wait  

echo ""  
echo "4. Vérification gouverneur..."  
gamemoderun sleep 5 &  
sleep 1  
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor  
wait  

echo ""  
echo "✅ Test terminé"  
```

Utilisez-le :
```bash
chmod +x test-gamemode.sh
./test-gamemode.sh
```

### Script de benchmark

```bash
#!/bin/bash
# benchmark-gamemode.sh

echo "Benchmark avec/sans GameMode"  
echo "============================="  

# Sans GameMode
echo "Test SANS GameMode..."  
FPS1=$(glxgears -fullscreen 2>&1 | grep "frames in" | awk '{print $1/5}')  
echo "FPS sans GameMode: $FPS1"  

sleep 2

# Avec GameMode
echo "Test AVEC GameMode..."  
FPS2=$(gamemoderun glxgears -fullscreen 2>&1 | grep "frames in" | awk '{print $1/5}')  
echo "FPS avec GameMode: $FPS2"  

# Calcul amélioration
GAIN=$(echo "scale=2; ($FPS2 - $FPS1) / $FPS1 * 100" | bc)  
echo "Gain: ${GAIN}%"  
```

## Monitoring de GameMode

### Indicateur système (optionnel)

Créez un indicateur visuel montrant quand GameMode est actif.

```bash
#!/bin/bash
# gamemode-indicator.sh

while true; do
    if gamemoded -s | grep -q "active"; then
        notify-send "🎮 GameMode" "ACTIF" -t 1000 -u low
    fi
    sleep 5
done
```

Lancez en arrière-plan :
```bash
./gamemode-indicator.sh &
```

### Widget Conky

Ajoutez à votre configuration Conky :

```lua
${if_match "${exec gamemoded -s | grep -c active}" == "1"}
GameMode: ${color green}ACTIF${color}
${else}
GameMode: ${color gray}inactif${color}
${endif}
```

## Intégration avec d'autres outils

### GameMode + CoreCtrl (AMD)

CoreCtrl pour overclocking/profils AMD.

```ini
[custom]
start=corectrl --profile gaming  
end=corectrl --profile desktop  
```

### GameMode + GreenWithEnvy (NVIDIA)

GWE pour contrôle ventilateur NVIDIA.

```ini
[custom]
start=gwe --profile gaming  
end=gwe --profile normal  
```

### GameMode + RGB

OpenRGB pour contrôler RGB.

```ini
[custom]
start=openrgb --profile gaming  
end=openrgb --profile normal  
```

## Ressources et documentation

### Documentation officielle

- **GitHub** : https://github.com/FeralInteractive/gamemode
- **Wiki** : https://github.com/FeralInteractive/gamemode/wiki

### Communauté

- **Reddit r/linux_gaming** : Discussions et partage configs
- **Feral Interactive** : Développeur original
- **GitHub Issues** : Support et bugs

### Articles recommandés

- GamingOnLinux : Tests de performance
- Phoronix : Benchmarks approfondis
- BoilingSteam : Guides pratiques

## Conclusion

GameMode est un outil essentiel pour tout joueur Linux. Son activation transparente et ses optimisations automatiques en font un must-have, sans aucun inconvénient.

**Points clés à retenir** :
- ✅ Installation simple : `sudo apt install gamemode`
- ✅ Utilisation transparente : `gamemoderun jeu`
- ✅ Amélioration mesurable : +5 à 15% FPS
- ✅ Aucun inconvénient (désactivation auto)
- ✅ Compatible tous launchers (Steam, Lutris, Heroic)
- ✅ Configuration optionnelle mais efficace par défaut

**Recommandation** :
Activez GameMode pour **TOUS** vos jeux. C'est gratuit, automatique et efficace.

**Commande à retenir** :
```bash
# Steam - Options de lancement
gamemoderun mangohud %command%
```

Avec GameMode, vous exploitez pleinement votre matériel sans effort. C'est l'optimisation gaming la plus simple et efficace sous Linux ! 🚀🎮

---


⏭️ [Applications Windows sous Linux](/15-applications-windows-sous-linux/README.md)
