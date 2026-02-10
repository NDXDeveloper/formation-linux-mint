🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 18.4 Optimisation SSD (TRIM, noatime)

## Introduction

Les **SSD** (Solid State Drive - disques à état solide) ont révolutionné l'informatique : ils sont jusqu'à 10 fois plus rapides que les disques durs traditionnels et n'ont aucune pièce mécanique. Cependant, ils fonctionnent différemment des disques durs classiques et nécessitent quelques optimisations spécifiques pour :

- **Maximiser leur durée de vie** : les SSD ont un nombre limité de cycles d'écriture
- **Maintenir leurs performances** : éviter la dégradation au fil du temps
- **Réduire l'usure inutile** : limiter les écritures superflues

**Dans ce chapitre, vous apprendrez à :**
- Vérifier si vous avez un SSD
- Activer et configurer TRIM pour nettoyer automatiquement votre SSD
- Optimiser les options de montage (noatime, relatime)
- Appliquer d'autres optimisations (swap, tmpfs, I/O scheduler)
- Éviter les erreurs qui pourraient endommager votre SSD

**Rassurez-vous :** Linux Mint gère déjà très bien les SSD par défaut. Les optimisations présentées ici sont des **améliorations marginales** qui prolongent la durée de vie de votre SSD.

---

## SSD vs Disque dur traditionnel (HDD)

### Comprendre la différence

**Disque dur traditionnel (HDD) :**
- Plateaux magnétiques qui tournent à 5400 ou 7200 tours/minute
- Têtes de lecture qui se déplacent mécaniquement
- Lent (100-150 Mo/s en lecture)
- Sensible aux chocs
- Aucune limite d'écriture
- Bruyant (bruit mécanique)

**SSD (Solid State Drive) :**
- Mémoire flash (comme une clé USB géante)
- Aucune pièce mécanique
- **Très rapide** (500-7000 Mo/s selon le type)
- Résistant aux chocs
- **Nombre limité de cycles d'écriture** (mais très élevé)
- Totalement silencieux

### Les types de SSD

**SATA SSD :**
- Connexion SATA (comme les vieux HDD)
- Vitesse : 500-550 Mo/s
- Format 2.5 pouces
- Le plus courant et abordable

**NVMe SSD (M.2) :**
- Connexion PCIe directe
- Vitesse : 2000-7000 Mo/s
- Format M.2 (petit module)
- Plus cher mais beaucoup plus rapide

**Peu importe le type, les optimisations de ce chapitre s'appliquent à tous les SSD.**

### Durée de vie d'un SSD : Le mythe à démonter

**Idée reçue :** "Les SSD s'usent vite et meurent rapidement"

**Réalité :**
- Un SSD moderne peut supporter **100 à 3000 To d'écriture** selon le modèle
- Avec 10 Go d'écritures par jour, un SSD de 500 Go durera **27 à 800 ans**
- La plupart des utilisateurs n'atteindront jamais cette limite

**Exemple concret :**
Un SSD Samsung 870 EVO de 500 Go a une endurance de 300 TBW (TeraBytes Written).
- Si vous écrivez 20 Go par jour : 300 000 Go ÷ 20 Go/jour = **41 ans de durée de vie**

**Conclusion :** Les optimisations ne sont pas vitales, mais elles permettent de gagner quelques années supplémentaires et de maintenir les performances.

---

## Vérifier si vous avez un SSD

Avant d'optimiser, vérifiez quel type de disque vous utilisez.

### Méthode 1 : Avec lsblk

```bash
lsblk -d -o name,rota
```

**Résultat :**
```
NAME ROTA  
sda     0  
sdb     1  
```

**Explication :**
- **ROTA = 0** : SSD (pas de rotation)
- **ROTA = 1** : Disque dur traditionnel (rotation)

Dans cet exemple :
- `sda` est un SSD
- `sdb` est un disque dur

### Méthode 2 : Avec le gestionnaire de disques

1. Menu > **Administration** > **Disques**
2. Sélectionnez votre disque dans la liste à gauche
3. Regardez les informations en haut :
   - **Lecteur à état solide** = SSD
   - **Lecteur de disque dur** = HDD

### Méthode 3 : Via le fichier système

```bash
cat /sys/block/sda/queue/rotational
```

- **0** = SSD
- **1** = HDD

**Note :** Remplacez `sda` par le nom de votre disque.

### Identifier votre partition système

Votre système Linux Mint est généralement installé sur `/dev/sda` ou `/dev/nvme0n1`.

**Pour savoir quelle partition est votre système :**

```bash
df -h /
```

**Résultat :**
```
Système de fichiers Taille Utilisé Dispo Uti% Monté sur
/dev/sda2               234G    89G  133G  41% /
```

Ici, `/dev/sda2` est la partition système.

---

## TRIM : L'optimisation essentielle pour SSD

### Qu'est-ce que TRIM ?

**TRIM** est une commande qui permet au système d'exploitation d'informer le SSD des blocs de données qui ne sont plus utilisés et qui peuvent être effacés.

**Pourquoi c'est important ?**

**Sans TRIM :**
1. Vous supprimez un fichier de 1 Go
2. Le système de fichiers marque l'espace comme "libre"
3. Mais le SSD **conserve encore les données** dans ses cellules
4. Quand vous écrivez un nouveau fichier, le SSD doit d'abord **effacer** puis **écrire**
5. Cela ralentit les écritures et use le SSD

**Avec TRIM :**
1. Vous supprimez un fichier de 1 Go
2. Le système de fichiers marque l'espace comme "libre"
3. **La commande TRIM informe le SSD** que ces blocs sont libres
4. Le SSD **efface ces blocs en arrière-plan** (pendant les temps morts)
5. Quand vous écrivez un nouveau fichier, le SSD écrit directement
6. **Écriture plus rapide** et **moins d'usure**

**Analogie simple :**
Imaginez un tableau blanc :
- **Sans TRIM** : vous écrivez par-dessus l'ancien texte sans effacer (lent et sale)
- **Avec TRIM** : vous effacez proprement avant d'écrire (rapide et propre)

### Vérifier si TRIM est supporté

**Commande :**
```bash
sudo hdparm -I /dev/sda | grep TRIM
```

**Résultat attendu :**
```
   *    Data Set Management TRIM supported (limit 8 blocks)
```

Si vous voyez cette ligne, votre SSD supporte TRIM. **Tous les SSD modernes le supportent.**

### Vérifier si TRIM est activé

Linux Mint active généralement TRIM automatiquement, mais vérifions :

```bash
sudo systemctl status fstrim.timer
```

**Résultat si activé :**
```
● fstrim.timer - Discard unused blocks once a week
     Loaded: loaded (/lib/systemd/system/fstrim.timer; enabled; vendor preset: enabled)
     Active: active (waiting) since Sat 2024-11-23 09:15:32 CET; 2 days ago
```

**Points à vérifier :**
- **Loaded: ... enabled** ✅ = TRIM automatique activé
- **Active: active** ✅ = Le timer fonctionne

**Si TRIM n'est PAS activé :**

```bash
sudo systemctl enable fstrim.timer  
sudo systemctl start fstrim.timer  
```

### Les deux méthodes TRIM : Automatique vs Continue

**1. TRIM automatique (hebdomadaire) - RECOMMANDÉ**

Le système lance TRIM une fois par semaine automatiquement via `fstrim.timer`.

**Avantages :**
- Équilibre parfait performance/usure
- Pas d'impact sur les performances quotidiennes
- Configuration par défaut de Linux Mint

**2. TRIM en continu (discard) - DÉCONSEILLÉ pour la plupart**

Chaque suppression de fichier déclenche immédiatement TRIM.

**Avantages :**
- Libération instantanée de l'espace sur le SSD
- Performances d'écriture toujours maximales

**Inconvénients :**
- **Peut ralentir les suppressions** de gros fichiers
- **Plus d'usure** du SSD (nombreuses petites commandes TRIM)
- **Impact sur la batterie** (laptops)

**Verdict :** Pour 99% des utilisateurs, **TRIM hebdomadaire suffit largement**. Ne passez au TRIM continu que si vous avez un cas d'usage spécifique (serveur de bases de données, par exemple).

### Lancer TRIM manuellement

Si vous voulez lancer TRIM immédiatement (par exemple après avoir supprimé beaucoup de fichiers) :

```bash
sudo fstrim -av
```

**Résultat :**
```
/boot/efi: 510.8 MiB (535822336 bytes) trimmed on /dev/sda1
/: 45.3 GiB (48640450560 bytes) trimmed on /dev/sda2
```

**Explication :**
- `-a` : toutes les partitions montées
- `-v` : mode verbeux (affiche les détails)

Cette commande indique combien d'espace a été libéré sur le SSD.

**Fréquence recommandée :**
- **Automatique hebdomadaire** : aucune action manuelle nécessaire
- **Manuel occasionnel** : après avoir supprimé des dizaines de Go de données

### Activer TRIM en continu (discard) - Utilisateurs avancés

**⚠️ Attention :** Ne faites ceci que si vous savez pourquoi vous en avez besoin.

**Méthode :**

1. Éditez `/etc/fstab` :
```bash
sudo nano /etc/fstab
```

2. Trouvez la ligne de votre partition système (celle avec `/` à la fin) :
```
UUID=xxxx-xxxx-xxxx  /  ext4  errors=remount-ro  0  1
```

3. Ajoutez l'option `discard` :
```
UUID=xxxx-xxxx-xxxx  /  ext4  errors=remount-ro,discard  0  1
```

4. Sauvegardez (`Ctrl+O`, `Entrée`, `Ctrl+X`)

5. Redémarrez votre ordinateur

**Vérification :**
```bash
mount | grep discard
```

Si vous voyez `discard` dans le résultat, c'est activé.

**Pour revenir en arrière :** Supprimez `,discard` de `/etc/fstab` et redémarrez.

---

## noatime : Réduire les écritures inutiles

### Qu'est-ce que atime ?

**atime** (access time) est un horodatage qui enregistre la dernière fois qu'un fichier a été **lu** (accédé).

**Le problème :**
- À chaque lecture de fichier, le système **écrit** l'heure d'accès sur le disque
- Cela génère des écritures inutiles sur le SSD
- Impact négatif sur performance et durée de vie

**Exemple :**
Vous ouvrez un document PDF :
1. Lecture du fichier PDF ✅
2. **Écriture** de l'heure d'accès sur le SSD ❌ (inutile !)

### Les options de montage : atime, noatime, relatime

**1. atime (par défaut sur les vieux systèmes)**
- Enregistre l'heure d'accès à chaque lecture
- **Problème :** écritures inutiles

**2. noatime**
- **Ne stocke jamais** l'heure d'accès
- **Avantage :** zéro écriture inutile
- **Inconvénient :** quelques rares programmes dépendent de atime (très rares)

**3. relatime (par défaut sur Linux Mint moderne)**
- Met à jour atime **seulement si** :
  - Le fichier est modifié (mtime), OU
  - L'ancien atime date de plus de 24 heures
- **Meilleur compromis** : réduit 99% des écritures inutiles tout en gardant la compatibilité

**Verdict :** Linux Mint utilise déjà `relatime` par défaut. **Vous n'avez rien à faire !**

### Vérifier l'option de montage actuelle

```bash
mount | grep ' / '
```

**Résultat :**
```
/dev/sda2 on / type ext4 (rw,relatime,errors=remount-ro)
```

Si vous voyez `relatime`, **c'est parfait**. Rien à changer.

### Passer à noatime (optionnel, gain marginal)

**Uniquement si vous voulez optimiser au maximum.**

1. Éditez `/etc/fstab` :
```bash
sudo nano /etc/fstab
```

2. Trouvez la ligne de votre partition système :
```
UUID=xxxx-xxxx-xxxx  /  ext4  errors=remount-ro  0  1
```

3. Ajoutez `noatime` (ou remplacez `relatime` par `noatime`) :
```
UUID=xxxx-xxxx-xxxx  /  ext4  noatime,errors=remount-ro  0  1
```

4. Sauvegardez et redémarrez

**Vérification :**
```bash
mount | grep ' / '
```

Vous devriez voir `noatime` dans le résultat.

**Différence de performance relatime vs noatime :** Quasi nulle pour un utilisateur normal. `relatime` suffit.

---

## Optimisation du Swap sur SSD

Le **swap** est une extension de la RAM sur le disque. Sur un SSD, trop de swap peut user prématurément le disque.

### Vérifier l'utilisation du swap

```bash
free -h
```

**Résultat :**
```
               total       utilisé     libre     partagé tamp/cache   disponible
Mem:            15Gi       4.2Gi       8.1Gi       234Mi       3.0Gi        10Gi  
Swap:          2.0Gi          0B       2.0Gi  
```

Si **Swap utilisé = 0B**, parfait ! Rien à optimiser.

### Réduire la swappiness

**swappiness** contrôle la tendance du système à utiliser le swap.

**Valeur par défaut :** 60 (sur une échelle de 0 à 100)
- 0 = utilise swap seulement en dernier recours
- 100 = utilise swap agressivement

**Recommandation pour SSD :** 10 (réduit l'utilisation du swap)

**Vérifier la valeur actuelle :**
```bash
cat /proc/sys/vm/swappiness
```

**Changer temporairement (jusqu'au prochain redémarrage) :**
```bash
sudo sysctl vm.swappiness=10
```

**Changer de façon permanente :**

1. Éditez le fichier de configuration :
```bash
sudo nano /etc/sysctl.conf
```

2. Ajoutez à la fin du fichier :
```
vm.swappiness=10
```

3. Sauvegardez (`Ctrl+O`, `Entrée`, `Ctrl+X`)

4. Appliquez immédiatement :
```bash
sudo sysctl -p
```

**Vérification :**
```bash
cat /proc/sys/vm/swappiness
```

Devrait afficher `10`.

### Désactiver complètement le swap (seulement si vous avez beaucoup de RAM)

**⚠️ Seulement si vous avez 16 Go de RAM ou plus.**

**Désactiver temporairement :**
```bash
sudo swapoff -a
```

**Désactiver définitivement :**

1. Éditez `/etc/fstab` :
```bash
sudo nano /etc/fstab
```

2. Trouvez la ligne contenant `swap` et commentez-la avec `#` :
```
# UUID=xxxx-xxxx  none  swap  sw  0  0
```

3. Sauvegardez et redémarrez

**Pour réactiver le swap :**
```bash
sudo swapon -a
```

**Recommandation :** Gardez le swap activé mais avec `swappiness=10`. Désactiver complètement peut causer des problèmes si la RAM sature.

---

## Optimisations avancées

### 1. I/O Scheduler (Planificateur d'entrées/sorties)

Le **I/O scheduler** gère l'ordre des opérations de lecture/écriture sur le disque.

**Pour HDD :** `deadline` ou `cfq` (optimise les mouvements de tête)  
**Pour SSD :** `noop` ou `none` (pas besoin d'optimiser l'ordre)  

Linux Mint utilise généralement le bon scheduler automatiquement, mais vérifions.

**Vérifier le scheduler actuel :**

```bash
cat /sys/block/sda/queue/scheduler
```

**Résultat (SSD NVMe) :**
```
[none] mq-deadline
```

Les crochets `[ ]` indiquent le scheduler actif. Ici, `none` est optimal pour SSD.

**Résultat (SSD SATA) :**
```
noop deadline [cfq]
```

Si vous voyez `cfq` actif sur un SSD, changez-le.

**Changer le scheduler temporairement :**

Pour un SSD SATA (`/dev/sda`) :
```bash
echo noop | sudo tee /sys/block/sda/queue/scheduler
```

Pour un SSD NVMe (`/dev/nvme0n1`) :
```bash
echo none | sudo tee /sys/block/nvme0n1/queue/scheduler
```

**Changer de façon permanente :**

1. Créez un fichier de règle udev :
```bash
sudo nano /etc/udev/rules.d/60-ioschedulers.rules
```

2. Pour SSD SATA, ajoutez :
```
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="noop"
```

3. Pour SSD NVMe, ajoutez :
```
ACTION=="add|change", KERNEL=="nvme[0-9]n[0-9]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="none"
```

4. Sauvegardez et redémarrez

**Note moderne :** Les noyaux récents (5.0+) gèrent cela automatiquement avec le scheduler `mq-deadline` qui s'adapte. Vous n'avez probablement pas besoin de changer.

### 2. Tmpfs pour /tmp (Fichiers temporaires en RAM)

**tmpfs** monte le dossier `/tmp` en RAM plutôt que sur le SSD.

**Avantages :**
- Accès ultra-rapide aux fichiers temporaires
- Zéro écriture sur le SSD
- Nettoyage automatique au redémarrage

**Inconvénient :**
- Consomme de la RAM
- Fichiers perdus au redémarrage (mais c'est l'idée de `/tmp`)

**Vérifier si tmpfs est déjà activé :**
```bash
df -h | grep tmpfs
```

Si vous voyez `/tmp` dans la liste, c'est déjà activé.

**Activer tmpfs pour /tmp :**

1. Éditez `/etc/fstab` :
```bash
sudo nano /etc/fstab
```

2. Ajoutez à la fin :
```
tmpfs  /tmp  tmpfs  defaults,noatime,mode=1777  0  0
```

3. Sauvegardez et redémarrez

**Limitation de taille (optionnel) :**

Pour limiter `/tmp` à 2 Go :
```
tmpfs  /tmp  tmpfs  defaults,noatime,mode=1777,size=2G  0  0
```

**Recommandation :** Activez tmpfs si vous avez 8 Go de RAM ou plus.

### 3. Désactiver l'indexation des fichiers

Les outils d'indexation (Tracker, Baloo) écrivent constamment pour maintenir un index de recherche.

**Désactiver Tracker (GNOME/Cinnamon) :**

```bash
systemctl --user mask tracker-store.service tracker-miner-fs.service tracker-miner-rss.service tracker-extract.service tracker-miner-apps.service tracker-writeback.service
```

**Désactiver Baloo (KDE, si utilisé) :**

```bash
balooctl disable
```

**Note :** Vous perdrez la recherche rapide de fichiers dans le menu. À vous de voir si le compromis en vaut la peine.

### 4. Désactiver les fichiers core dump

Les **core dumps** sont des fichiers créés quand un programme crash. Sur un système de bureau, ils sont rarement utiles.

**Désactiver :**

```bash
sudo nano /etc/security/limits.conf
```

Ajoutez à la fin :
```
*    soft    core    0
```

Sauvegardez et redémarrez.

**Ou via systemd :**

```bash
sudo systemctl mask systemd-coredump@.service
```

---

## Surveiller la santé du SSD

### Installer smartmontools

**smartmontools** permet de lire les informations SMART du SSD.

**Installation :**
```bash
sudo apt install smartmontools
```

### Vérifier l'état de santé global

```bash
sudo smartctl -H /dev/sda
```

**Résultat :**
```
SMART overall-health self-assessment test result: PASSED
```

**PASSED** = SSD en bonne santé ✅

### Afficher les informations détaillées

```bash
sudo smartctl -a /dev/sda
```

**Informations importantes à surveiller :**

**1. Wear Leveling Count (Usure)**
```
233 Media_Wearout_Indicator   0x0032   097   097   000    Old_age   Always       -       3%
```
Ici, le SSD est usé à **3%**. Excellent !

**2. Total LBAs Written (Total écrit sur le SSD)**
```
241 Total_LBAs_Written         0x0032   000   000   000    Old_age   Always       -       15428639372
```

Pour convertir en To :  
LBAs × 512 octets ÷ 1 000 000 000 000 = To écrits  

**3. Power On Hours (Heures d'utilisation)**
```
  9 Power_On_Hours             0x0032   098   098   000    Old_age   Always       -       7234
```
Ce SSD a fonctionné 7234 heures (environ 301 jours).

**4. Temperature**
```
194 Temperature_Celsius        0x0022   037   041   000    Old_age   Always       -       37
```
Température actuelle : 37°C (normal, 20-50°C = OK)

### Calculer la durée de vie restante

**Formule approximative :**

Durée de vie restante (années) = (100 - Usure%) × Heures actuelles ÷ Usure% ÷ 8760

**Exemple avec les données ci-dessus :**
- Usure = 3%
- Heures d'utilisation = 7234

(100 - 3) × 7234 ÷ 3 ÷ 8760 ≈ **26 ans restants**

**Note :** C'est une estimation très approximative. La plupart des SSD dureront bien au-delà de leur durée de vie théorique.

### Surveiller régulièrement

Créez un script de vérification mensuelle :

```bash
nano ~/check-ssd-health.sh
```

Contenu :
```bash
#!/bin/bash

echo "=== État de santé du SSD ==="  
sudo smartctl -H /dev/sda  

echo ""  
echo "=== Usure du SSD ==="  
sudo smartctl -a /dev/ssd | grep -i "wear\|percentage"  

echo ""  
echo "=== Température ==="  
sudo smartctl -a /dev/ssd | grep -i temperature  
```

Rendez-le exécutable :
```bash
chmod +x ~/check-ssd-health.sh
```

Exécutez-le une fois par mois :
```bash
~/check-ssd-health.sh
```

---

## Ce qu'il NE faut PAS faire avec un SSD

### ❌ Défragmenter le SSD

**JAMAIS de défragmentation sur SSD !**

Sur un HDD, la défragmentation regroupe les fichiers fragmentés pour accélérer les lectures.

Sur un SSD :
- Les lectures sont instantanées, peu importe l'emplacement
- La défragmentation génère des écritures massives inutiles
- **Usure prématurée du SSD** sans aucun gain de performance

**Comment désactiver la défragmentation automatique (si activée) :**

Linux Mint ne défragmente pas automatiquement les SSD, mais vérifiez :

```bash
systemctl status fstrim.timer
```

Si vous voyez un service nommé `e4defrag` ou similaire, désactivez-le :
```bash
sudo systemctl disable e4defrag.timer  
sudo systemctl stop e4defrag.timer  
```

### ❌ Remplir le SSD à 100%

**Gardez toujours au moins 10-20% d'espace libre.**

**Pourquoi :**
- Les SSD ont besoin d'espace libre pour gérer l'usure (wear leveling)
- Un SSD plein à 95%+ ralentit énormément
- Le contrôleur n'a plus de blocs de réserve

**Recommandation :**
- **Idéal :** 25% d'espace libre
- **Minimum :** 10% d'espace libre

### ❌ Écriture intensive continue 24/7

**Évitez les applications qui écrivent constamment :**
- Torrents en seeding permanent (préférez un HDD externe)
- Serveurs de bases de données intensifs (utilisez un SSD serveur spécialisé)
- Logs système excessifs (configurez la rotation des logs, voir section 18.5)

**Pour un usage normal (bureautique, navigation, gaming), aucun souci.**

### ❌ Outils de "nettoyage" agressifs

**N'utilisez pas d'outils qui font des "secure erase" fréquents.**

Les SSD ont déjà des mécanismes de gestion de la mémoire. Les outils de "nettoyage sécurisé" sont inutiles et génèrent des écritures excessives.

**Exception :** Secure erase avant de vendre le SSD (une seule fois) est OK.

---

## Résumé des optimisations

### Optimisations essentielles (à faire)

| Optimisation | Commande/Action | Gain |
|--------------|-----------------|------|
| **Activer TRIM hebdomadaire** | `sudo systemctl enable fstrim.timer` | ⭐⭐⭐⭐⭐ Essentiel |
| **Vérifier relatime** | `mount \| grep ' / '` | ✅ Déjà activé par défaut |
| **Réduire swappiness** | Mettre à 10 dans `/etc/sysctl.conf` | ⭐⭐⭐ Recommandé |

### Optimisations avancées (optionnelles)

| Optimisation | Commande/Action | Gain |
|--------------|-----------------|------|
| **noatime au lieu de relatime** | Modifier `/etc/fstab` | ⭐⭐ Marginal |
| **tmpfs pour /tmp** | Ajouter ligne dans `/etc/fstab` | ⭐⭐⭐ Si 8+ Go RAM |
| **I/O scheduler optimal** | Vérifier avec `cat /sys/block/sda/queue/scheduler` | ⭐ Auto-géré |
| **Désactiver indexation** | `systemctl --user mask tracker-*` | ⭐⭐ Si besoin |

### À éviter absolument

| Action | Pourquoi |
|--------|----------|
| **Défragmentation** | Usure inutile, aucun gain |
| **SSD plein à 100%** | Ralentissements drastiques |
| **Swap excessif** | Usure prématurée (utilisez swappiness=10) |
| **Secure erase répétés** | Inutile et destructeur |

---

## Configuration optimale : Checklist complète

Voici une configuration recommandée pour un SSD sous Linux Mint.

### 1. Vérifications initiales

```bash
# Vérifier que vous avez un SSD
lsblk -d -o name,rota

# Vérifier que TRIM est supporté
sudo hdparm -I /dev/sda | grep TRIM

# Vérifier que TRIM automatique est activé
sudo systemctl status fstrim.timer
```

### 2. Activer TRIM hebdomadaire (si pas déjà fait)

```bash
sudo systemctl enable fstrim.timer  
sudo systemctl start fstrim.timer  
```

### 3. Configurer swappiness

```bash
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf  
sudo sysctl -p  
```

### 4. Vérifier les options de montage

```bash
mount | grep ' / '
```

Vous devriez voir `relatime` ou `noatime`.

### 5. (Optionnel) Activer tmpfs pour /tmp

Si vous avez 8+ Go de RAM :

```bash
echo "tmpfs  /tmp  tmpfs  defaults,noatime,mode=1777,size=4G  0  0" | sudo tee -a /etc/fstab
```

Puis redémarrez.

### 6. Vérifier la santé du SSD régulièrement

```bash
sudo smartctl -H /dev/sda
```

**Voilà ! Votre SSD est maintenant optimisé de manière optimale.**

---

## Script d'optimisation automatique

Voici un script qui applique les optimisations recommandées automatiquement.

```bash
nano ~/optimiser-ssd.sh
```

Contenu :

```bash
#!/bin/bash

echo "🔧 Optimisation SSD pour Linux Mint"  
echo "===================================="  
echo ""  

# Vérifier si c'est bien un SSD
ROTA=$(lsblk -d -o name,rota | grep sda | awk '{print $2}')  
if [ "$ROTA" != "0" ]; then  
    echo "⚠️  Attention : /dev/sda ne semble pas être un SSD (ROTA=$ROTA)"
    echo "Ce script est conçu pour les SSD uniquement."
    exit 1
fi

echo "✅ SSD détecté sur /dev/sda"  
echo ""  

# 1. Activer TRIM hebdomadaire
echo "📅 Activation de TRIM hebdomadaire..."  
sudo systemctl enable fstrim.timer  
sudo systemctl start fstrim.timer  
echo "✅ TRIM hebdomadaire activé"  
echo ""  

# 2. Configurer swappiness
echo "💾 Configuration de swappiness à 10..."  
if ! grep -q "vm.swappiness" /etc/sysctl.conf; then  
    echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
    sudo sysctl -p
    echo "✅ Swappiness configuré à 10"
else
    echo "ℹ️  Swappiness déjà configuré"
fi  
echo ""  

# 3. Vérifier les options de montage
echo "🔍 Vérification des options de montage..."  
mount | grep ' / ' | grep -q "relatime\|noatime"  
if [ $? -eq 0 ]; then  
    echo "✅ Options de montage optimales détectées"
else
    echo "⚠️  Vérifiez manuellement /etc/fstab pour ajouter 'relatime' ou 'noatime'"
fi  
echo ""  

# 4. Lancer TRIM immédiatement
echo "🧹 Lancement de TRIM sur toutes les partitions..."  
sudo fstrim -av  
echo ""  

# 5. Vérifier la santé du SSD
echo "🏥 Vérification de la santé du SSD..."  
sudo smartctl -H /dev/sda  
echo ""  

echo "================================"  
echo "✅ Optimisation terminée !"  
echo "Redémarrez votre ordinateur pour appliquer tous les changements."  
echo ""  
echo "📊 Pour surveiller votre SSD : sudo smartctl -a /dev/sda"  
echo "🧹 Pour lancer TRIM manuellement : sudo fstrim -av"  
```

Rendez-le exécutable :
```bash
chmod +x ~/optimiser-ssd.sh
```

Exécutez-le :
```bash
~/optimiser-ssd.sh
```

---

## Bonnes pratiques à long terme

### ✅ À faire régulièrement

1. **Vérifier l'espace libre** : gardez toujours 15-20% libre
2. **Surveiller la santé SMART** : une fois par mois avec `smartctl`
3. **Nettoyer le système** : supprimez les fichiers inutiles (voir section 18.1)
4. **Vérifier TRIM** : `sudo systemctl status fstrim.timer`

### 📊 Surveiller les indicateurs clés

**Tous les mois :**
```bash
# Santé globale
sudo smartctl -H /dev/sda

# Usure
sudo smartctl -a /dev/sda | grep -i wear

# Température
sudo smartctl -a /dev/sda | grep -i temp

# Espace libre
df -h /
```

### 🎯 Objectifs de santé

**Indicateurs normaux :**
- **Usure** : < 10% après 2-3 ans d'usage normal
- **Température** : 20-50°C (max 70°C sous charge)
- **Espace libre** : > 15% de l'espace total
- **Swap** : < 500 Mo utilisés en moyenne

**Si vous dépassez ces valeurs :**
- Usure > 50% : envisagez de remplacer le SSD dans 1-2 ans
- Température > 70°C : améliorez la ventilation
- Espace libre < 10% : nettoyez immédiatement
- Swap > 1 Go constamment : ajoutez de la RAM

---

## Conclusion

Les SSD sont des composants **robustes** et **durables**. Avec les optimisations présentées dans ce chapitre, vous maximisez leur durée de vie et leurs performances.

**Les 3 règles d'or :**

1. 🔧 **TRIM hebdomadaire activé** → essentiel
2. 💾 **Swappiness à 10** → réduit l'usure
3. 📦 **Gardez 15-20% d'espace libre** → performances optimales

**Tout le reste est optionnel et apporte des gains marginaux.**

Linux Mint gère déjà très bien les SSD par défaut. Les optimisations de ce chapitre sont des **améliorations**, pas des nécessités absolues.

**Avec un SSD bien optimisé, vous profiterez de :**
- Démarrage en 10-15 secondes
- Applications qui s'ouvrent instantanément
- Durée de vie de 10+ ans pour un usage normal
- Système ultra-réactif en permanence

**Votre SSD est maintenant configuré pour durer des années !** 🚀

---

## Pour aller plus loin

- **Section 18.1** : Nettoyage du système (libérer de l'espace)
- **Section 18.3** : Surveillance des ressources (htop, btop)
- **Section 18.5** : Gestion et rotation des logs
- **Section 8.3** : Gestion des disques (GParted)
- **Section 17.1** : Timeshift (sauvegardes système)

**Documentation :**
- `man fstrim`
- `man smartctl`
- `man fstab`
- Spécifications TRIM : https://en.wikipedia.org/wiki/Trim_(computing)

⏭️ [Gestion et rotation des logs](/18-maintenance-et-optimisation/05-gestion-et-rotation-des-logs.md)
