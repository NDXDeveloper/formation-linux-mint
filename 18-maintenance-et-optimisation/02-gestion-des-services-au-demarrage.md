🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 18.2 Gestion des services au démarrage (systemd)

## Introduction

Quand vous démarrez votre ordinateur sous Linux Mint, de nombreux programmes invisibles se lancent automatiquement en arrière-plan : le gestionnaire réseau, l'imprimante, le serveur audio, le pare-feu, etc. Ces programmes s'appellent des **services** (ou **démons**).

Certains services sont essentiels au fonctionnement de votre système, d'autres sont utiles selon votre utilisation, et quelques-uns peuvent être inutiles et ralentir le démarrage.

**Dans ce chapitre, vous apprendrez à :**
- Comprendre ce qu'est un service et pourquoi il tourne en permanence
- Lister les services actifs sur votre système
- Désactiver les services inutiles pour accélérer le démarrage
- Gérer les services en toute sécurité avec systemd

**Rassurez-vous :** Avec les bonnes commandes, gérer les services est sans danger et peut améliorer sensiblement les performances de votre système.

---

## Qu'est-ce qu'un service ?

### Définition simple

Un **service** (aussi appelé **daemon** en anglais, prononcé "démon") est un programme qui :
- Tourne en arrière-plan de façon invisible
- Se lance automatiquement au démarrage du système
- N'a pas d'interface graphique
- Attend de recevoir des demandes ou surveille des événements

**Exemples concrets :**

| Service | Rôle |
|---------|------|
| `NetworkManager` | Gère votre connexion WiFi et Ethernet |
| `bluetooth` | Active le Bluetooth |
| `cups` | Gère les imprimantes |
| `ssh` | Permet les connexions à distance (si activé) |
| `cron` | Exécute des tâches planifiées |
| `ufw` | Pare-feu de votre système |

### Pourquoi gérer les services ?

**Avantages de désactiver les services inutiles :**

1. **Démarrage plus rapide** : moins de programmes à lancer = gain de 5 à 20 secondes au boot
2. **Moins de RAM utilisée** : chaque service consomme de la mémoire
3. **Sécurité renforcée** : un service désactivé ne peut pas être exploité par un attaquant
4. **Économie d'énergie** : important pour les laptops

**Exemple :** Si vous n'avez pas de Bluetooth, désactiver le service `bluetooth` économise ~20 Mo de RAM et accélère le démarrage.

---

## systemd : Le gestionnaire de services moderne

### Qu'est-ce que systemd ?

**systemd** est le système d'initialisation et de gestion des services utilisé par Linux Mint (et la plupart des distributions Linux modernes depuis 2015).

**Son rôle :**
- Démarrer le système dans le bon ordre
- Lancer et surveiller tous les services
- Gérer les dépendances entre services (ex: le réseau doit démarrer avant certaines applications)
- Enregistrer les logs système

**Avant systemd**, on utilisait SysVinit (plus ancien et plus lent). systemd est beaucoup plus rapide grâce au démarrage parallèle des services.

### La commande systemctl

Pour interagir avec systemd, on utilise la commande **`systemctl`** (system control).

**Syntaxe générale :**
```bash
systemctl [action] [nom-du-service]
```

**Actions principales :**
- `status` : voir l'état d'un service
- `start` : démarrer un service maintenant
- `stop` : arrêter un service maintenant
- `restart` : redémarrer un service
- `enable` : activer le démarrage automatique
- `disable` : désactiver le démarrage automatique
- `is-enabled` : vérifier si un service démarre automatiquement

---

## Lister et inspecter les services

### Voir tous les services actifs

Pour afficher tous les services en cours d'exécution :

```bash
systemctl list-units --type=service --state=running
```

**Résultat typique :**
```
UNIT                          LOAD   ACTIVE SUB     DESCRIPTION  
accounts-daemon.service       loaded active running Accounts Service  
avahi-daemon.service          loaded active running Avahi mDNS/DNS-SD Stack  
bluetooth.service             loaded active running Bluetooth service  
NetworkManager.service        loaded active running Network Manager  
```

**Explication des colonnes :**
- **UNIT** : nom du service
- **LOAD** : le service est bien chargé
- **ACTIVE** : état général (active/inactive)
- **SUB** : état détaillé (running/dead/exited)
- **DESCRIPTION** : description du service

### Voir TOUS les services (actifs + inactifs)

```bash
systemctl list-units --type=service --all
```

Cette commande affiche aussi les services désactivés ou qui ont échoué.

### Voir les services qui démarrent automatiquement

```bash
systemctl list-unit-files --type=service --state=enabled
```

Cela liste tous les services configurés pour démarrer au boot.

### Vérifier l'état d'un service spécifique

Pour inspecter un service en détail :

```bash
systemctl status nom-du-service
```

**Exemple avec NetworkManager :**

```bash
systemctl status NetworkManager
```

**Résultat :**
```
● NetworkManager.service - Network Manager
     Loaded: loaded (/lib/systemd/system/NetworkManager.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2024-11-23 09:15:32 CET; 2h 34min ago
       Docs: man:NetworkManager(8)
   Main PID: 845 (NetworkManager)
      Tasks: 3 (limit: 18802)
     Memory: 15.2M
        CPU: 1.234s
     CGroup: /system.slice/NetworkManager.service
             └─845 /usr/sbin/NetworkManager --no-daemon
```

**Ce que cela signifie :**
- **Loaded: enabled** → le service démarre automatiquement
- **Active: active (running)** → le service tourne actuellement
- **Main PID** → numéro du processus
- **Memory** → RAM utilisée (ici 15.2 Mo)

### Codes couleur dans le terminal

systemd utilise des couleurs pour faciliter la lecture :
- **Vert (●)** : service actif et fonctionnel
- **Rouge (●)** : service échoué ou arrêté
- **Blanc (○)** : service inactif

---

## Gérer les services : Actions de base

### Démarrer un service (temporaire)

Pour démarrer un service immédiatement (ne survit pas au redémarrage) :

```bash
sudo systemctl start nom-du-service
```

**Exemple :** Démarrer le service SSH

```bash
sudo systemctl start ssh
```

### Arrêter un service (temporaire)

Pour stopper un service immédiatement :

```bash
sudo systemctl stop nom-du-service
```

**Exemple :** Arrêter le Bluetooth

```bash
sudo systemctl stop bluetooth
```

### Redémarrer un service

Utile après avoir modifié la configuration d'un service :

```bash
sudo systemctl restart nom-du-service
```

**Exemple :** Redémarrer le gestionnaire réseau

```bash
sudo systemctl restart NetworkManager
```

### Recharger la configuration (sans redémarrage)

Certains services peuvent recharger leur configuration sans redémarrer complètement :

```bash
sudo systemctl reload nom-du-service
```

Si vous ne savez pas si le service supporte `reload`, utilisez :

```bash
sudo systemctl reload-or-restart nom-du-service
```

---

## Activer ou désactiver le démarrage automatique

### Différence importante : start/stop vs enable/disable

⚠️ **Confusion fréquente chez les débutants :**

- `start` / `stop` : action **immédiate** (maintenant)
- `enable` / `disable` : action **permanente** (au prochain démarrage)

**Exemple concret :**

```bash
sudo systemctl stop bluetooth     # Arrête Bluetooth MAINTENANT  
sudo systemctl disable bluetooth  # Bluetooth ne démarrera plus au boot  
```

Après ces deux commandes :
- Bluetooth est arrêté maintenant ✅
- Au prochain démarrage, Bluetooth ne se lancera pas automatiquement ✅

### Désactiver un service au démarrage

Pour empêcher un service de démarrer automatiquement :

```bash
sudo systemctl disable nom-du-service
```

**Exemple :** Désactiver le Bluetooth

```bash
sudo systemctl disable bluetooth
```

**Note :** Le service reste actif dans la session courante. Pour l'arrêter complètement :

```bash
sudo systemctl disable bluetooth && sudo systemctl stop bluetooth
```

### Activer un service au démarrage

Pour qu'un service démarre automatiquement à chaque boot :

```bash
sudo systemctl enable nom-du-service
```

**Exemple :** Activer SSH

```bash
sudo systemctl enable ssh
```

### Activer ET démarrer en une seule commande

```bash
sudo systemctl enable --now nom-du-service
```

Le flag `--now` démarre immédiatement le service en plus de l'activer.

### Vérifier si un service est activé

```bash
systemctl is-enabled nom-du-service
```

**Réponses possibles :**
- `enabled` : démarre automatiquement
- `disabled` : ne démarre pas automatiquement
- `static` : le service est déclenché par un autre service
- `masked` : le service est complètement bloqué (voir plus bas)

---

## Masquer un service (blocage complet)

### Qu'est-ce que le masquage ?

**Masquer** un service (`mask`) est une action plus forte que `disable`. Elle empêche totalement le service de démarrer, même si un autre service ou un script tente de le lancer.

**Cas d'usage :**
- Bloquer définitivement un service problématique
- Empêcher un paquet logiciel de réactiver automatiquement un service

### Masquer un service

```bash
sudo systemctl mask nom-du-service
```

**Exemple :** Bloquer complètement le Bluetooth

```bash
sudo systemctl mask bluetooth
```

**Effet :** Le service devient impossible à démarrer, même avec `systemctl start`.

### Démasquer un service

Pour annuler le masquage :

```bash
sudo systemctl unmask nom-du-service
```

Ensuite, vous pouvez le réactiver si besoin :

```bash
sudo systemctl enable nom-du-service
```

---

## Services que vous pouvez désactiver sans risque

Voici une liste de services généralement sûrs à désactiver selon votre utilisation.

### ⚠️ Avertissement général

Avant de désactiver un service, **assurez-vous de comprendre son rôle**. En cas de doute, ne touchez pas !

### Services liés au Bluetooth

**Si vous n'utilisez JAMAIS le Bluetooth :**

```bash
sudo systemctl disable bluetooth  
sudo systemctl stop bluetooth  
```

**Services concernés :**
- `bluetooth.service` : le service Bluetooth principal

### Services liés aux imprimantes

**Si vous n'avez pas d'imprimante ou imprimez rarement :**

```bash
sudo systemctl disable cups  
sudo systemctl disable cups-browsed  
```

**Services concernés :**
- `cups.service` : Common Unix Printing System (système d'impression)
- `cups-browsed.service` : détection automatique d'imprimantes réseau

**Note :** Vous pourrez toujours réactiver ces services quand vous aurez besoin d'imprimer.

### Services liés au scanner

**Si vous n'avez pas de scanner :**

```bash
sudo systemctl disable saned
```

**Service concerné :**
- `saned.service` : serveur de scanner réseau

### Services liés au modem

**Si vous n'utilisez pas de modem (connexion téléphonique ou 3G/4G) :**

```bash
sudo systemctl disable ModemManager
```

**Service concerné :**
- `ModemManager.service` : gestion des modems mobiles

### Services liés aux machines virtuelles

**Si vous n'utilisez pas VirtualBox ou autres VM :**

Ces services sont installés si vous avez installé VirtualBox :

```bash
sudo systemctl disable vboxadd-service  
sudo systemctl disable vboxadd  
```

### Services liés au partage réseau

**Si vous ne partagez pas de fichiers en réseau local :**

```bash
sudo systemctl disable smbd      # Serveur Samba (partage Windows)  
sudo systemctl disable nmbd      # NetBIOS (découverte réseau Windows)  
sudo systemctl disable avahi-daemon  # Découverte automatique réseau local  
```

**⚠️ Attention :** Désactiver `avahi-daemon` peut empêcher certaines imprimantes réseau et périphériques d'être détectés automatiquement.

### Services liés au serveur SSH

**Si vous n'accédez jamais à votre machine à distance :**

```bash
sudo systemctl disable ssh
```

**⚠️ Important :** Ne désactivez SSH que sur un ordinateur personnel local. Gardez-le actif sur un serveur !

---

## Services à NE JAMAIS désactiver

Ces services sont **essentiels** au bon fonctionnement de votre système. Ne les touchez pas !

### Services critiques du système

❌ **NetworkManager** : gestion réseau (WiFi, Ethernet)
```bash
# NE JAMAIS FAIRE :
sudo systemctl disable NetworkManager
```
Sans lui, plus de connexion internet !

❌ **systemd-logind** : gestion des sessions utilisateur
```bash
# NE JAMAIS FAIRE :
sudo systemctl disable systemd-logind
```
Sans lui, vous ne pourrez plus vous connecter graphiquement !

❌ **dbus** : communication entre applications
```bash
# NE JAMAIS FAIRE :
sudo systemctl disable dbus
```
Sans lui, le bureau ne fonctionne plus du tout.

❌ **ufw** : pare-feu système
```bash
# DÉCONSEILLÉ :
sudo systemctl disable ufw
```
Sauf si vous savez vraiment ce que vous faites en sécurité réseau.

❌ **cron** : tâches planifiées
```bash
# DÉCONSEILLÉ :
sudo systemctl disable cron
```
Désactive toutes vos sauvegardes automatiques et tâches planifiées.

❌ **rsyslog** : journalisation système
```bash
# DÉCONSEILLÉ :
sudo systemctl disable rsyslog
```
Sans logs, impossible de diagnostiquer les problèmes !

### Services graphiques

❌ **lightdm** ou **gdm** : gestionnaire de connexion graphique
```bash
# NE JAMAIS FAIRE :
sudo systemctl disable lightdm
```
Sans lui, vous démarrez en mode texte uniquement !

---

## Analyser le temps de démarrage

### Voir le temps total de démarrage

Pour savoir combien de temps votre système met à démarrer :

```bash
systemd-analyze
```

**Résultat exemple :**
```
Startup finished in 4.231s (firmware) + 2.847s (loader) + 3.125s (kernel) + 8.942s (userspace) = 19.145s  
graphical.target reached after 8.874s in userspace  
```

**Explication :**
- **firmware** : temps du BIOS/UEFI
- **loader** : temps du chargeur de démarrage (GRUB)
- **kernel** : chargement du noyau Linux
- **userspace** : chargement des services et du bureau
- **Total** : 19.145 secondes

### Voir quels services ralentissent le démarrage

Pour identifier les services les plus lents :

```bash
systemd-analyze blame
```

**Résultat exemple :**
```
8.234s NetworkManager-wait-online.service
3.892s plymouth-quit-wait.service
2.456s snapd.service
1.234s cups.service
0.987s bluetooth.service
0.654s avahi-daemon.service
```

Les services sont triés par ordre décroissant (du plus lent au plus rapide).

**Conseil :** Si un service prend plus de 3-4 secondes et que vous ne l'utilisez pas, envisagez de le désactiver.

### Générer un graphique de démarrage

Pour visualiser graphiquement le démarrage :

```bash
systemd-analyze plot > boot.svg
```

Ouvrez ensuite le fichier `boot.svg` dans Firefox pour voir un diagramme détaillé.

### Analyse critique d'un service lent

Pour comprendre pourquoi un service est lent :

```bash
systemd-analyze critical-chain nom-du-service
```

**Exemple :**
```bash
systemd-analyze critical-chain NetworkManager.service
```

Cela affiche la chaîne de dépendances qui a retardé le démarrage de ce service.

---

## Cas pratique : Optimiser le démarrage

### Scénario : Ordinateur fixe sans Bluetooth ni imprimante

Vous avez un PC de bureau, sans Bluetooth, sans imprimante, et vous n'accédez jamais à distance.

**Services à désactiver :**

```bash
# Désactiver Bluetooth
sudo systemctl disable bluetooth  
sudo systemctl stop bluetooth  

# Désactiver CUPS (imprimantes)
sudo systemctl disable cups  
sudo systemctl disable cups-browsed  

# Désactiver ModemManager (pas de modem)
sudo systemctl disable ModemManager

# Désactiver SSH (pas de connexion à distance)
sudo systemctl disable ssh
```

**Gain potentiel :** 5 à 10 secondes au démarrage + économie de 50-80 Mo de RAM.

### Scénario : Laptop avec Bluetooth occasionnel

Vous avez un laptop et utilisez parfois le Bluetooth, mais pas au démarrage.

**Solution :** Désactivez Bluetooth au boot, mais activez-le manuellement quand nécessaire.

```bash
# Désactiver au démarrage
sudo systemctl disable bluetooth

# Quand vous avez besoin du Bluetooth :
sudo systemctl start bluetooth

# Quand vous n'en avez plus besoin :
sudo systemctl stop bluetooth
```

**Alternative graphique :** Utilisez simplement l'icône Bluetooth dans la barre des tâches pour l'activer/désactiver.

---

## Créer un script de gestion des services

Pour faciliter l'activation/désactivation de plusieurs services, créez un script.

### Script d'optimisation pour PC fixe

Créez le fichier :

```bash
nano ~/optimiser-services.sh
```

Ajoutez ce contenu :

```bash
#!/bin/bash

echo "🚀 Optimisation des services au démarrage..."  
echo ""  

# Services à désactiver
SERVICES_A_DESACTIVER=(
    "bluetooth"
    "cups"
    "cups-browsed"
    "ModemManager"
)

for service in "${SERVICES_A_DESACTIVER[@]}"; do
    if systemctl is-enabled "$service" &>/dev/null; then
        echo "⏸️  Désactivation de $service..."
        sudo systemctl disable "$service"
        sudo systemctl stop "$service"
    else
        echo "ℹ️  $service déjà désactivé"
    fi
done

echo ""  
echo "✅ Optimisation terminée !"  
echo ""  
echo "📊 Analyse du temps de démarrage :"  
systemd-analyze  
```

Rendez-le exécutable :

```bash
chmod +x ~/optimiser-services.sh
```

Exécutez-le :

```bash
~/optimiser-services.sh
```

### Script de restauration

Pour réactiver tous les services si besoin :

```bash
nano ~/restaurer-services.sh
```

Contenu :

```bash
#!/bin/bash

echo "♻️  Réactivation des services..."

SERVICES_A_REACTIVER=(
    "bluetooth"
    "cups"
    "cups-browsed"
    "ModemManager"
)

for service in "${SERVICES_A_REACTIVER[@]}"; do
    echo "▶️  Réactivation de $service..."
    sudo systemctl enable "$service"
done

echo "✅ Services réactivés !"
```

---

## Dépannage : Problèmes courants

### Un service échoue au démarrage

**Symptôme :** `systemctl status` affiche "failed" en rouge.

**Solution :**

1. Vérifiez les détails de l'erreur :
```bash
systemctl status nom-du-service
```

2. Consultez les logs :
```bash
journalctl -u nom-du-service -n 50
```

3. Essayez de redémarrer :
```bash
sudo systemctl restart nom-du-service
```

### J'ai désactivé un service par erreur

**Solution :** Réactivez-le simplement :

```bash
sudo systemctl enable nom-du-service  
sudo systemctl start nom-du-service  
```

**En cas de doute sur le nom exact :**

```bash
systemctl list-unit-files --type=service | grep mot-clé
```

### Mon système ne démarre plus graphiquement

**Cause probable :** Vous avez désactivé `lightdm` ou un service critique.

**Solution en mode recovery :**

1. Au démarrage, appuyez sur `Shift` pour afficher le menu GRUB
2. Sélectionnez "Advanced options"
3. Choisissez "Recovery mode"
4. Sélectionnez "root - Drop to root shell prompt"
5. Montez le système en écriture :
```bash
mount -o remount,rw /
```
6. Réactivez le service problématique :
```bash
systemctl enable lightdm
```
7. Redémarrez :
```bash
reboot
```

### Bluetooth/WiFi ne fonctionne plus après désactivation

**Solution :**

```bash
sudo systemctl enable bluetooth  
sudo systemctl start bluetooth  

sudo systemctl enable NetworkManager  
sudo systemctl start NetworkManager  
```

---

## Outils graphiques pour gérer les services

### Avec l'outil "Services système" de Cinnamon

Linux Mint Cinnamon inclut parfois un gestionnaire graphique de services.

1. Menu > **Administration** > **Services système** (si disponible)
2. Cochez/décochez les services selon vos besoins
3. Cliquez sur **Appliquer**

**Note :** Cet outil n'est pas toujours installé par défaut.

### Avec BUM (Boot-Up Manager)

**Installation :**

```bash
sudo apt install bum
```

**Utilisation :**

1. Lancez BUM : `gksudo bum`
2. Cochez/décochez les services
3. Cliquez sur **Appliquer**

⚠️ **Attention :** BUM est un outil ancien et peut ne pas bien gérer systemd. Préférez `systemctl` en ligne de commande.

---

## Bonnes pratiques et recommandations

### ✅ À faire

1. **Sauvegardez** votre système avec Timeshift avant de modifier les services (voir section 17.1)
2. **Testez** les changements en mode live (`stop`/`start`) avant de les rendre permanents (`disable`/`enable`)
3. **Documentez** les services que vous désactivez (gardez une liste)
4. **Vérifiez** l'impact sur le temps de démarrage avec `systemd-analyze`
5. **Désactivez un service à la fois** et redémarrez pour vérifier que tout fonctionne

### ❌ À éviter

1. **Ne désactivez jamais** un service sans savoir à quoi il sert
2. **N'utilisez pas** de scripts tout faits trouvés sur internet sans les comprendre
3. **Ne désactivez pas** les services système critiques (NetworkManager, dbus, systemd-logind...)
4. **Ne vous précipitez pas** : quelques secondes de démarrage en moins ne valent pas un système cassé

### 🎯 Objectif réaliste

- **Gain de temps au boot** : 5 à 15 secondes maximum
- **Économie de RAM** : 50 à 200 Mo selon les services désactivés
- **Sécurité** : chaque service inutile désactivé réduit la surface d'attaque

**Mais n'espérez pas des miracles :** Linux Mint est déjà très optimisé par défaut. Le vrai gain se situe surtout dans l'utilisation d'un SSD (voir section 18.4) et une RAM suffisante.

---

## Résumé des commandes essentielles

| Commande | Action |
|----------|--------|
| `systemctl status nom-service` | Voir l'état d'un service |
| `systemctl list-units --type=service` | Lister tous les services actifs |
| `systemctl is-enabled nom-service` | Vérifier si un service démarre au boot |
| `sudo systemctl start nom-service` | Démarrer immédiatement |
| `sudo systemctl stop nom-service` | Arrêter immédiatement |
| `sudo systemctl restart nom-service` | Redémarrer |
| `sudo systemctl enable nom-service` | Activer au démarrage |
| `sudo systemctl disable nom-service` | Désactiver au démarrage |
| `sudo systemctl mask nom-service` | Bloquer complètement |
| `systemd-analyze` | Temps de démarrage |
| `systemd-analyze blame` | Services les plus lents |
| `journalctl -u nom-service` | Logs d'un service |

---

## Commande combinée recommandée

Pour désactiver proprement un service :

```bash
sudo systemctl disable nom-service && sudo systemctl stop nom-service
```

Pour réactiver proprement un service :

```bash
sudo systemctl enable nom-service && sudo systemctl start nom-service
```

---

## Conclusion

La gestion des services avec systemd est **puissante mais simple** une fois les bases comprises.

**Ce qu'il faut retenir :**

1. 🎯 **Objectif principal** : accélérer le démarrage et économiser des ressources
2. ⚠️ **Prudence** : ne désactivez que ce que vous comprenez et n'utilisez pas
3. 🛡️ **Sécurité** : faites une sauvegarde Timeshift avant toute modification
4. 📊 **Mesure** : utilisez `systemd-analyze` pour quantifier vos gains
5. 🔄 **Réversible** : tout peut être réactivé en cas d'erreur

**Services typiquement désactivables sans risque :**
- Bluetooth (si inutilisé)
- Imprimantes (CUPS) si pas d'imprimante
- ModemManager (si pas de modem)
- SSH (si pas de connexion à distance)

**Avec ces connaissances, vous maîtrisez maintenant systemd comme un pro !** 🚀

---

## Pour aller plus loin

- **Section 18.3** : Surveillance des ressources avec htop et btop
- **Section 20.2** : Cron et tâches planifiées
- **Section 20.3** : Systemd timers (alternative à cron)
- **Section 23.7** : Lecture des logs avec journalctl
- **Documentation officielle** : `man systemctl` et `man systemd`

⏭️ [Surveillance des ressources (htop, btop, moniteur système)](/18-maintenance-et-optimisation/03-surveillance-des-ressources.md)
