🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 18.7 Vérification de l'intégrité du système

## Introduction

Imaginez votre système Linux comme une maison : au fil du temps, des fissures peuvent apparaître, des portes peuvent se dérégler, des installations peuvent devenir défectueuses. La **vérification de l'intégrité du système** consiste à inspecter régulièrement tous les éléments pour s'assurer que tout fonctionne correctement et qu'aucune altération suspecte n'a eu lieu.

**Dans ce chapitre, vous apprendrez à :**
- Vérifier que les fichiers système n'ont pas été corrompus ou modifiés
- Détecter les erreurs sur le disque dur et en mémoire
- S'assurer qu'aucun logiciel malveillant (rootkit) ne s'est installé
- Valider l'intégrité des paquets installés
- Diagnostiquer les problèmes matériels
- Maintenir un système sain et sécurisé

**Pourquoi c'est important ?**
- **Sécurité** : détecter les intrusions ou modifications malveillantes
- **Fiabilité** : identifier les corruptions de données avant qu'elles ne causent des problèmes
- **Performance** : repérer les défaillances matérielles qui ralentissent le système
- **Prévention** : corriger les petits problèmes avant qu'ils ne deviennent graves

**Rassurez-vous :** Linux Mint est très robuste. Ces vérifications sont principalement **préventives** et ne révèlent généralement aucun problème sur un système bien maintenu.

---

## Qu'est-ce que l'intégrité du système ?

### Définition simple

L'**intégrité** signifie que votre système est :
- **Complet** : tous les fichiers essentiels sont présents
- **Authentique** : les fichiers n'ont pas été modifiés de façon inattendue
- **Fonctionnel** : le matériel et les logiciels fonctionnent correctement
- **Sécurisé** : aucun logiciel malveillant n'est présent

### Les différentes couches à vérifier

**1. Intégrité matérielle**
- Disque dur/SSD : secteurs défectueux, erreurs SMART
- Mémoire RAM : erreurs de lecture/écriture
- Système de fichiers : corruption de la structure

**2. Intégrité logicielle**
- Paquets système : fichiers manquants ou modifiés
- Checksums : validation des téléchargements
- Configurations : fichiers système altérés

**3. Intégrité de sécurité**
- Rootkits : logiciels malveillants cachés
- Fichiers système modifiés par un attaquant
- Processus suspects

### Quand vérifier l'intégrité ?

**Vérification régulière (préventive) :**
- Une fois par mois : vérification SMART du disque
- Tous les 3 mois : scan antirootkit
- Tous les 6 mois : vérification complète des paquets

**Vérification immédiate (réactive) :**
- Après un crash système ou coupure électrique
- Si le système se comporte bizarrement (lenteurs, erreurs)
- Après une mise à jour majeure qui a échoué
- Si vous suspectez une intrusion
- Avant de vendre ou donner votre ordinateur

---

## Vérification des paquets installés

Les **paquets** sont les logiciels installés sur votre système. Vérifier leur intégrité assure qu'ils n'ont pas été corrompus ou modifiés.

### debsums : Vérification des checksums

**debsums** vérifie que les fichiers installés par les paquets correspondent aux checksums (empreintes) d'origine.

#### Installation de debsums

```bash
sudo apt install debsums
```

#### Vérifier tous les paquets

```bash
sudo debsums -c
```

**L'option `-c` affiche uniquement les erreurs** (mode silencieux si tout va bien).

**Si tout est OK :** Aucune sortie (c'est bon signe !)

**Si des erreurs apparaissent :**
```
debsums: changed file /usr/bin/program (from package-name package)  
debsums: missing file /etc/config.conf (from package-name package)  
```

**Signification :**
- **changed file** : le fichier a été modifié (pas forcément grave)
- **missing file** : le fichier manque (plus préoccupant)

#### Vérifier un paquet spécifique

```bash
debsums firefox
```

Vérifie uniquement les fichiers du paquet Firefox.

#### Vérifier tous les fichiers de configuration

```bash
sudo debsums -e -c
```

**L'option `-e` limite aux fichiers de configuration** (dans `/etc`).

**Note :** Il est normal que certains fichiers de configuration soient "modifiés" car vous les avez personnalisés (ex: `/etc/fstab`, `/etc/hosts`).

#### Réinstaller un paquet corrompu

Si debsums détecte des fichiers corrompus dans un paquet :

```bash
sudo apt install --reinstall nom-du-paquet
```

**Exemple :**
```bash
sudo apt install --reinstall firefox
```

Cela réinstalle le paquet sans supprimer vos données.

#### Vérification complète (avec détails)

```bash
sudo debsums -a
```

**L'option `-a` vérifie TOUS les paquets** (même ceux sans checksums). Cela peut prendre plusieurs minutes.

### dpkg : Vérifier l'état des paquets

**dpkg** gère les paquets Debian/Ubuntu. Il peut identifier les paquets dans un état incohérent.

#### Lister les paquets cassés ou partiellement installés

```bash
dpkg -l | grep ^..r
```

Affiche les paquets avec des problèmes (état "r" = réinstallation nécessaire).

**Si la commande ne retourne rien :** Parfait, aucun paquet cassé.

**Si des paquets apparaissent :**
```bash
sudo dpkg --configure -a  
sudo apt install -f  
```

Ces commandes réparent les installations incomplètes.

#### Vérifier la cohérence de la base de données dpkg

```bash
sudo dpkg --audit
```

Affiche les paquets avec des problèmes d'installation ou de configuration.

**Sortie vide = système sain.**

#### Reconstruire la base de données dpkg (en cas de corruption)

**⚠️ Utilisez uniquement si dpkg est vraiment corrompu :**

```bash
sudo dpkg --clear-avail  
sudo apt-get update  
sudo apt-get check  
```

---

## Vérification du système de fichiers

Le **système de fichiers** (ext4, btrfs, etc.) organise vos données sur le disque. Des erreurs peuvent survenir après un crash ou une coupure électrique.

### fsck : File System Consistency Check

**fsck** vérifie et répare les erreurs du système de fichiers.

**⚠️ IMPORTANT : fsck NE DOIT PAS être exécuté sur une partition montée !**

### Vérification automatique au démarrage

Linux vérifie automatiquement le système de fichiers :
- Tous les X démarrages (généralement 30)
- Après un arrêt brutal

**Forcer une vérification au prochain démarrage :**

```bash
sudo touch /forcefsck
```

Au prochain redémarrage, fsck s'exécutera automatiquement.

### Vérification manuelle (mode recovery)

**Pour vérifier la partition système, utilisez le mode recovery.**

#### Étapes complètes :

1. **Redémarrez l'ordinateur**

2. **Appuyez sur `Shift` (ou `Esc`) au démarrage** pour afficher le menu GRUB

3. **Sélectionnez "Advanced options for Linux Mint"**

4. **Choisissez "Recovery mode"**

5. **Sélectionnez "fsck - Check all file systems"**

6. **Confirmez avec "Yes"**

7. **Attendez la fin de la vérification** (quelques minutes)

8. **Redémarrez normalement**

### Vérifier une partition non-système

Pour une partition qui n'est PAS celle du système (ex: disque externe, partition de données) :

**1. Démontez la partition :**
```bash
sudo umount /dev/sdXY
```

**2. Lancez fsck :**
```bash
sudo fsck /dev/sdXY
```

**Remplacez `sdXY`** par le nom de votre partition (ex: `sdb1`).

**Options utiles :**
- `-a` : réparation automatique (pas d'interaction)
- `-y` : répond "oui" à toutes les questions
- `-n` : mode test (pas de modification, lecture seule)

**Exemple avec réparation automatique :**
```bash
sudo fsck -y /dev/sdb1
```

### Interpréter les résultats de fsck

**Si fsck ne trouve rien :**
```
/dev/sda2: clean, 456789/12345678 files, 98765432/123456789 blocks
```
✅ Système de fichiers sain.

**Si fsck répare des erreurs :**
```
/dev/sda2: ***** FILE SYSTEM WAS MODIFIED *****
/dev/sda2: 456789/12345678 files (1.2% non-contiguous), 98765432/123456789 blocks
```
⚠️ Des erreurs ont été corrigées. Si cela arrive souvent, vérifiez votre disque avec SMART (voir plus bas).

**Si fsck rencontre des erreurs graves :**
```
/dev/sda2: UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY.
```
🔴 Problème sérieux. Exécutez `fsck` manuellement en mode recovery avec l'option `-y`.

### e2fsck : Spécifique à ext4

Pour les partitions ext4 (le standard Linux Mint), vous pouvez utiliser `e2fsck` qui est plus spécialisé.

```bash
sudo e2fsck -f -y /dev/sdXY
```

**Options :**
- `-f` : force la vérification même si le système semble propre
- `-y` : répond automatiquement "oui"
- `-p` : réparation automatique (safe mode)

---

## Vérification SMART du disque

**SMART** (Self-Monitoring, Analysis and Reporting Technology) surveille la santé de votre disque dur ou SSD.

### Installation de smartmontools

```bash
sudo apt install smartmontools
```

### Vérifier si SMART est supporté

```bash
sudo smartctl -i /dev/sda
```

Remplacez `sda` par votre disque (utilisez `lsblk` pour voir la liste).

**Résultat :** Affiche les informations du disque et confirme si SMART est disponible.

### Test de santé rapide

```bash
sudo smartctl -H /dev/sda
```

**Résultat espéré :**
```
SMART overall-health self-assessment test result: PASSED
```

✅ **PASSED** : disque en bonne santé

🔴 **FAILED** : disque défaillant, **sauvegardez immédiatement vos données** et remplacez le disque !

### Afficher les attributs SMART détaillés

```bash
sudo smartctl -a /dev/sda
```

**Informations importantes :**

#### Attributs critiques à surveiller :

**1. Reallocated Sector Count (5)**
```
  5 Reallocated_Sector_Ct   0x0033   100   100   010    Pre-fail  Always       -       0
```
- **Valeur = 0** : parfait ✅
- **Valeur > 0** : le disque a des secteurs défectueux ⚠️
- **Valeur > 50** : disque en fin de vie 🔴

**2. Current Pending Sector (197)**
```
197 Current_Pending_Sector  0x0012   100   100   000    Old_age   Always       -       0
```
- **0** : normal ✅
- **> 0** : secteurs en attente de réallocation ⚠️

**3. Uncorrectable Sector Count (198)**
```
198 Offline_Uncorrectable   0x0010   100   100   000    Old_age   Offline      -       0
```
- **0** : bon ✅
- **> 0** : erreurs non corrigibles 🔴

**4. Temperature (194)**
```
194 Temperature_Celsius     0x0022   037   041   000    Old_age   Always       -       37
```
- **20-45°C** : normal ✅
- **45-55°C** : chaud ⚠️
- **> 55°C** : trop chaud, améliorez la ventilation 🔴

**5. Power On Hours (9)**
```
  9 Power_On_Hours          0x0032   098   098   000    Old_age   Always       -       7234
```
Indique le nombre d'heures d'utilisation du disque.

### Tests SMART approfondis

**SMART propose plusieurs types de tests :**

#### Test court (2-3 minutes)

```bash
sudo smartctl -t short /dev/sda
```

Vérification rapide des zones critiques du disque.

#### Test long (1-2 heures)

```bash
sudo smartctl -t long /dev/sda
```

Scan complet du disque.

#### Voir les résultats des tests

```bash
sudo smartctl -l selftest /dev/sda
```

**Résultat :**
```
Num  Test_Description    Status                  Remaining  LifeTime(hours)
# 1  Short offline       Completed without error       00%      7234
# 2  Extended offline    Completed without error       00%      7150
```

✅ **Completed without error** : tout va bien

🔴 **Read failure** ou autres erreurs : problème matériel

### Activer la surveillance continue

**Démarrer smartd (démon de surveillance) :**

```bash
sudo systemctl enable smartd  
sudo systemctl start smartd  
```

**smartd** surveille en permanence votre disque et peut vous alerter en cas de problème.

**Configuration :**
```bash
sudo nano /etc/smartd.conf
```

Exemple de ligne pour surveiller `/dev/sda` et envoyer un email en cas de problème :
```
/dev/sda -a -m votre@email.com
```

---

## Vérification de la mémoire RAM

La **RAM** peut avoir des erreurs qui causent des crashs aléatoires et des corruptions de données.

### Memtest86+ : Le test standard

**Memtest86+** est l'outil de référence pour tester la RAM.

#### Installation

```bash
sudo apt install memtest86+
```

L'installation ajoute automatiquement Memtest au menu GRUB.

#### Lancer Memtest86+

1. **Redémarrez votre ordinateur**
2. **Appuyez sur `Shift` au démarrage** pour afficher GRUB
3. **Sélectionnez "Memory test (memtest86+)"**
4. **Laissez le test se dérouler** (au moins 1 passe complète = 30 min à 2h)

**Recommandation :** Laissez tourner toute la nuit (plusieurs passes).

#### Interpréter les résultats

**Écran de Memtest :**
```
Pass: X     Errors: Y
```

- **Errors: 0** après plusieurs passes : RAM en bon état ✅
- **Errors: > 0** : RAM défectueuse 🔴

**Si des erreurs apparaissent :**

1. **Testez chaque barrette séparément** pour identifier la défectueuse
2. **Essayez un autre slot mémoire** (parfois c'est le slot qui est défaillant)
3. **Remplacez la RAM défectueuse**

**Symptômes d'une RAM défectueuse :**
- Écrans bleus/freeze aléatoires
- Erreurs de segmentation (Segmentation fault)
- Corruption de fichiers
- Le système ne démarre pas toujours

### Test RAM depuis le système (moins fiable)

Si vous ne pouvez pas redémarrer, testez depuis le système :

```bash
sudo apt install memtester
```

**Tester 1 Go de RAM :**
```bash
sudo memtester 1G 5
```

Teste 1 Go de RAM avec 5 passes.

**⚠️ Moins fiable que Memtest86+ car le système est actif.**

---

## Détection de rootkits et malwares

Un **rootkit** est un logiciel malveillant qui se cache dans le système pour échapper à la détection.

### rkhunter : Rootkit Hunter

**rkhunter** scanne le système à la recherche de rootkits connus.

#### Installation

```bash
sudo apt install rkhunter
```

#### Mise à jour de la base de données

```bash
sudo rkhunter --update
```

#### Premier scan (initialisation)

**Avant le premier scan, mettez à jour la base de référence :**

```bash
sudo rkhunter --propupd
```

Cela enregistre l'état actuel des fichiers système comme référence.

#### Lancer un scan complet

```bash
sudo rkhunter --check
```

Le scan peut prendre 5-15 minutes. Appuyez sur `Entrée` pour passer chaque section.

**Ou en mode automatique (pas d'interaction) :**
```bash
sudo rkhunter --check --sk
```

(`--sk` = skip key, saute les pauses)

#### Interpréter les résultats

**Résultat typique :**
```
System checks summary
=====================

File properties checks...
    Files checked: 137
    Suspect files: 0

Rootkit checks...
    Rootkits checked : 383
    Possible rootkits: 0

Applications checks...
    All checks skipped
```

✅ **0 suspect files, 0 possible rootkits** : système propre

⚠️ **Suspect files ou possible rootkits détectés** : consultez le rapport détaillé

#### Voir le rapport détaillé

```bash
sudo cat /var/log/rkhunter.log
```

**Faux positifs courants :**
- Certains scripts légitimes peuvent être signalés
- Des fichiers modifiés lors de mises à jour
- Vérifiez toujours avant de paniquer

**Si un vrai rootkit est détecté :**
1. **NE PAS FAIRE CONFIANCE au système actuel**
2. Démarrez sur un Live USB
3. Sauvegardez vos données importantes
4. Réinstallez le système proprement
5. Changez TOUS vos mots de passe depuis un autre ordinateur sain

#### Automatiser les scans

**Scan quotidien automatique :**

```bash
sudo nano /etc/cron.daily/rkhunter
```

Contenu :
```bash
#!/bin/sh
/usr/bin/rkhunter --update --quiet
/usr/bin/rkhunter --cronjob --report-warnings-only
```

Rendez-le exécutable :
```bash
sudo chmod +x /etc/cron.daily/rkhunter
```

### chkrootkit : Alternative à rkhunter

**chkrootkit** est un autre scanner de rootkits, complémentaire à rkhunter.

#### Installation

```bash
sudo apt install chkrootkit
```

#### Lancer un scan

```bash
sudo chkrootkit
```

**Résultat :**
```
Searching for suspicious files and dirs, it may take a while...  
nothing found  
Searching for rootkits...  
nothing found  
```

✅ **nothing found** : système propre

**Note :** chkrootkit génère parfois des faux positifs. Croisez avec rkhunter.

### ClamAV : Antivirus (bonus)

Bien que Linux soit très résistant aux virus, **ClamAV** peut détecter des malwares.

#### Installation

```bash
sudo apt install clamav clamav-daemon
```

#### Mise à jour de la base de données

```bash
sudo freshclam
```

#### Scanner le dossier personnel

```bash
clamscan -r --bell -i /home/votre-nom
```

**Options :**
- `-r` : récursif (sous-dossiers)
- `--bell` : émet un bip si virus trouvé
- `-i` : affiche seulement les fichiers infectés

**Pour scanner tout le système :**
```bash
sudo clamscan -r --bell -i /
```

(Prend plusieurs heures)

---

## Vérification des checksums (empreintes)

Les **checksums** (ou hashs) permettent de vérifier qu'un fichier téléchargé n'a pas été corrompu ou altéré.

### Vérifier un fichier ISO téléchargé

**Exemple :** Vous téléchargez Linux Mint ISO.

**1. Téléchargez aussi le fichier de checksum** (généralement `.sha256` ou `.md5`)

**2. Calculez le checksum du fichier téléchargé :**

```bash
sha256sum linuxmint-21.3-cinnamon-64bit.iso
```

**Résultat :**
```
4a2a2b1234567890abcdef1234567890abcdef1234567890abcdef1234567890  linuxmint-21.3-cinnamon-64bit.iso
```

**3. Comparez avec le checksum officiel**

Si les deux correspondent exactement : ✅ Fichier intègre

Si différent : 🔴 Fichier corrompu ou altéré, **retéléchargez**

### Vérification automatique

**Si vous avez le fichier .sha256 :**

```bash
sha256sum -c linuxmint-21.3-cinnamon-64bit.iso.sha256
```

**Résultat :**
```
linuxmint-21.3-cinnamon-64bit.iso: OK
```

✅ **OK** : fichier valide

### Différents algorithmes de checksum

**SHA256 (recommandé) :**
```bash
sha256sum fichier
```

**SHA512 (encore plus sécurisé) :**
```bash
sha512sum fichier
```

**MD5 (ancien, moins sûr) :**
```bash
md5sum fichier
```

---

## Vérification des logs pour anomalies

Les **logs** peuvent révéler des problèmes ou activités suspectes.

### Vérifier les erreurs système récentes

```bash
journalctl -p err -b
```

Affiche toutes les erreurs depuis le dernier démarrage.

**Si beaucoup d'erreurs :** Investiguer avec `journalctl -u service-problematique`

### Vérifier les tentatives de connexion échouées

```bash
sudo grep "Failed password" /var/log/auth.log
```

**Résultat :**
```
Nov 29 03:45:12 mint sshd[1234]: Failed password for invalid user admin from 192.168.1.100  
Nov 29 03:45:15 mint sshd[1235]: Failed password for invalid user root from 192.168.1.100  
```

⚠️ **Nombreuses tentatives depuis une IP inconnue** : possible attaque par force brute

**Action :** Bloquer l'IP avec fail2ban (voir section 11.8)

### Vérifier l'utilisation de sudo

```bash
sudo grep "sudo:" /var/log/auth.log | tail -n 20
```

Affiche les 20 dernières utilisations de sudo.

**Recherchez des commandes suspectes** que vous n'avez pas exécutées.

### Vérifier les modifications de fichiers système

**Fichiers modifiés dans /etc dans les dernières 24h :**

```bash
sudo find /etc -type f -mtime -1 -ls
```

**Si des fichiers critiques ont été modifiés sans raison :** Investiguer.

---

## Timeshift : Sauvegarde et restauration

**Timeshift** crée des snapshots (instantanés) de votre système, permettant de revenir en arrière si quelque chose ne va pas.

### Vérifier les snapshots disponibles

```bash
sudo timeshift --list
```

**Résultat :**
```
Device : /dev/sda2  
Snapshot list:  
  O  2024-11-29_10-00-00  Daily
  O  2024-11-28_10-00-00  Daily
  O  2024-11-27_10-00-00  Daily
```

✅ **Plusieurs snapshots récents** : vous pouvez restaurer en cas de problème

🔴 **Aucun snapshot** : configurez Timeshift immédiatement (voir section 17.1)

### Restaurer depuis un snapshot (GUI)

1. Lancez **Timeshift** depuis le menu
2. Sélectionnez un snapshot
3. Cliquez sur **Restaurer**
4. Confirmez et attendez

### Restaurer depuis un snapshot (CLI)

```bash
sudo timeshift --restore --snapshot '2024-11-29_10-00-00'
```

**⚠️ Utilisez avec précaution** : cela écrase le système actuel.

---

## Script de vérification complète

Créez un script qui effectue toutes les vérifications importantes.

```bash
nano ~/verification-systeme.sh
```

Contenu :

```bash
#!/bin/bash

echo "============================================"  
echo "🔍 Vérification complète du système"  
echo "============================================"  
echo ""  

# 1. Vérification de l'espace disque
echo "💾 1. Vérification de l'espace disque"  
echo "--------------------------------------"  
df -h | grep -E "^/dev"  
USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')  
if [ "$USAGE" -gt 90 ]; then  
    echo "⚠️  ATTENTION : Disque presque plein (${USAGE}%)"
else
    echo "✅ Espace disque OK (${USAGE}% utilisé)"
fi  
echo ""  

# 2. Vérification SMART du disque
echo "🔧 2. Vérification SMART du disque"  
echo "-----------------------------------"  
if command -v smartctl &> /dev/null; then  
    SMART_STATUS=$(sudo smartctl -H /dev/sda 2>/dev/null | grep "PASSED")
    if [ -n "$SMART_STATUS" ]; then
        echo "✅ Disque en bonne santé (SMART: PASSED)"
    else
        echo "⚠️  Vérifiez SMART avec : sudo smartctl -a /dev/sda"
    fi
else
    echo "ℹ️  smartmontools non installé. Installez avec : sudo apt install smartmontools"
fi  
echo ""  

# 3. Vérification des erreurs récentes
echo "📋 3. Erreurs système récentes"  
echo "-------------------------------"  
ERROR_COUNT=$(journalctl -p err -b | wc -l)  
if [ "$ERROR_COUNT" -eq 0 ]; then  
    echo "✅ Aucune erreur depuis le démarrage"
else
    echo "⚠️  $ERROR_COUNT erreurs détectées"
    echo "   Consultez avec : journalctl -p err -b"
fi  
echo ""  

# 4. Vérification des paquets
echo "📦 4. Intégrité des paquets"  
echo "---------------------------"  
if command -v debsums &> /dev/null; then  
    DEBSUM_ERRORS=$(sudo debsums -c 2>/dev/null | wc -l)
    if [ "$DEBSUM_ERRORS" -eq 0 ]; then
        echo "✅ Tous les paquets sont intègres"
    else
        echo "⚠️  $DEBSUM_ERRORS fichiers de paquets modifiés"
        echo "   (Note: certains fichiers de config peuvent être normalement modifiés)"
    fi
else
    echo "ℹ️  debsums non installé. Installez avec : sudo apt install debsums"
fi  
echo ""  

# 5. Vérification des paquets cassés
echo "🔧 5. Paquets cassés"  
echo "--------------------"  
BROKEN=$(dpkg -l | grep ^..r | wc -l)  
if [ "$BROKEN" -eq 0 ]; then  
    echo "✅ Aucun paquet cassé"
else
    echo "⚠️  $BROKEN paquet(s) nécessitent une réinstallation"
    echo "   Réparez avec : sudo dpkg --configure -a && sudo apt install -f"
fi  
echo ""  

# 6. Mises à jour disponibles
echo "🔄 6. Mises à jour disponibles"  
echo "-------------------------------"  
sudo apt update -qq  
UPDATES=$(apt list --upgradable 2>/dev/null | grep -c upgradable)  
if [ "$UPDATES" -le 1 ]; then  
    echo "✅ Système à jour"
else
    echo "ℹ️  $UPDATES mises à jour disponibles"
    echo "   Mettez à jour avec : sudo apt upgrade"
fi  
echo ""  

# 7. Services échoués
echo "⚙️  7. Services système"  
echo "----------------------"  
FAILED_SERVICES=$(systemctl list-units --failed --no-pager --no-legend | wc -l)  
if [ "$FAILED_SERVICES" -eq 0 ]; then  
    echo "✅ Tous les services fonctionnent"
else
    echo "⚠️  $FAILED_SERVICES service(s) en échec"
    echo "   Consultez avec : systemctl --failed"
fi  
echo ""  

# 8. Dernière sauvegarde Timeshift
echo "💾 8. Sauvegarde Timeshift"  
echo "--------------------------"  
if command -v timeshift &> /dev/null; then  
    LAST_SNAPSHOT=$(sudo timeshift --list 2>/dev/null | grep "^  O" | head -n 1 | awk '{print $2}')
    if [ -n "$LAST_SNAPSHOT" ]; then
        echo "✅ Dernier snapshot : $LAST_SNAPSHOT"
    else
        echo "⚠️  Aucun snapshot trouvé. Configurez Timeshift !"
    fi
else
    echo "⚠️  Timeshift non installé. Installez avec : sudo apt install timeshift"
fi  
echo ""  

# 9. Température (si disponible)
echo "🌡️  9. Température système"  
echo "--------------------------"  
if command -v sensors &> /dev/null; then  
    sensors | grep -E "Core|temp" | head -n 5
else
    echo "ℹ️  lm-sensors non installé. Installez avec : sudo apt install lm-sensors"
fi  
echo ""  

# 10. Résumé final
echo "============================================"  
echo "📊 RÉSUMÉ"  
echo "============================================"  
echo ""  

ISSUES=0
[ "$USAGE" -gt 90 ] && ISSUES=$((ISSUES + 1))
[ "$ERROR_COUNT" -gt 10 ] && ISSUES=$((ISSUES + 1))
[ "$DEBSUM_ERRORS" -gt 0 ] && ISSUES=$((ISSUES + 1))
[ "$BROKEN" -gt 0 ] && ISSUES=$((ISSUES + 1))
[ "$FAILED_SERVICES" -gt 0 ] && ISSUES=$((ISSUES + 1))

if [ "$ISSUES" -eq 0 ]; then
    echo "✅ Système en excellent état !"
    echo "   Aucun problème détecté."
elif [ "$ISSUES" -le 2 ]; then
    echo "⚠️  Quelques points à surveiller ($ISSUES)"
    echo "   Consultez les détails ci-dessus."
else
    echo "🔴 Plusieurs problèmes détectés ($ISSUES)"
    echo "   Action recommandée : investigation approfondie."
fi  
echo ""  
echo "Pour une vérification approfondie :"  
echo "  - Rootkits : sudo rkhunter --check"  
echo "  - RAM : Redémarrez en mode Memtest86+"  
echo "  - Disque : sudo smartctl -a /dev/sda"  
echo ""  
```

Rendez-le exécutable :
```bash
chmod +x ~/verification-systeme.sh
```

Exécutez-le :
```bash
~/verification-systeme.sh
```

---

## Calendrier de maintenance préventive

### Quotidien (automatique)

- ✅ Surveillance SMART activée (smartd)
- ✅ Logs consultés en cas de problème

### Hebdomadaire

- 🔍 Vérifier les erreurs récentes : `journalctl -p err --since "1 week ago"`
- 💾 Vérifier l'espace disque : `df -h`

### Mensuel

- 🔧 Vérifier SMART : `sudo smartctl -H /dev/sda`
- 📦 Vérifier les paquets : `sudo debsums -c`
- 🔄 Mises à jour système : `sudo apt update && sudo apt upgrade`

### Trimestriel

- 🛡️ Scan rootkit : `sudo rkhunter --check`
- 🧹 Nettoyage complet (voir section 18.1)
- 📊 Exécution du script de vérification complète

### Semestriel

- 💻 Test RAM (Memtest86+) : une nuit complète
- 🔍 Vérification complète fsck (mode recovery)
- 🔎 Vérification approfondie SMART : `sudo smartctl -t long /dev/sda`

### Annuel

- 💾 Test complet de restauration Timeshift
- 🗄️ Audit de sécurité complet
- 🔄 Réinstallation propre (optionnel, pour repartir à neuf)

---

## Checklist de vérification rapide

### Avant une mise à jour majeure

- [ ] Créer un snapshot Timeshift
- [ ] Vérifier l'espace disque (>10 Go libre)
- [ ] Vérifier SMART du disque
- [ ] Lire les notes de version

### Après un crash système

- [ ] Vérifier fsck au redémarrage
- [ ] Consulter les logs : `journalctl -b -1 -p err`
- [ ] Vérifier SMART : `sudo smartctl -H /dev/sda`
- [ ] Scanner avec debsums : `sudo debsums -c`

### Si le système est lent/instable

- [ ] Vérifier la RAM avec Memtest86+
- [ ] Vérifier SMART du disque
- [ ] Consulter les erreurs : `journalctl -p err -b`
- [ ] Vérifier l'espace disque
- [ ] Scanner les rootkits : `sudo rkhunter --check`

### Avant de vendre/donner l'ordinateur

- [ ] Sauvegarder vos données
- [ ] Vérifier SMART pour garantir un disque sain
- [ ] Réinstaller Linux Mint proprement
- [ ] Effacer les données sensibles (voir section 11.4)

---

## Outils de diagnostic complémentaires

### hardinfo : Informations matériel complètes

**Installation :**
```bash
sudo apt install hardinfo
```

**Lancement :**
```bash
hardinfo
```

Affiche : processeur, RAM, carte graphique, stockage, benchmarks, etc.

### inxi : Informations système en CLI

**Installation :**
```bash
sudo apt install inxi
```

**Afficher tout :**
```bash
inxi -Fxz
```

Informations complètes sur le matériel, réseau, etc.

### lshw : Liste matériel détaillée

**Déjà préinstallé.**

```bash
sudo lshw -short
```

Affiche tous les composants matériels.

---

## Résumé des commandes essentielles

### Vérification des paquets

```bash
# Vérifier l'intégrité
sudo debsums -c

# Réparer paquets cassés
sudo dpkg --configure -a  
sudo apt install -f  

# Réinstaller un paquet
sudo apt install --reinstall paquet
```

### Vérification du disque

```bash
# Santé SMART
sudo smartctl -H /dev/sda

# Détails SMART
sudo smartctl -a /dev/sda

# Test long
sudo smartctl -t long /dev/sda

# fsck (en mode recovery)
sudo fsck -y /dev/sdXY
```

### Sécurité

```bash
# Scan rootkit
sudo rkhunter --check --sk

# Alternative
sudo chkrootkit

# Antivirus
clamscan -r -i ~
```

### Logs et erreurs

```bash
# Erreurs récentes
journalctl -p err -b

# Tentatives de connexion échouées
sudo grep "Failed password" /var/log/auth.log

# Services échoués
systemctl --failed
```

---

## Conclusion

La vérification de l'intégrité du système est une pratique **essentielle** mais souvent négligée.

**Les points clés à retenir :**

1. **Préventif vaut mieux que curatif** : vérifiez régulièrement, pas seulement en cas de problème
2. **SMART est votre ami** : surveillez la santé de votre disque
3. **Les snapshots Timeshift sauvent des vies** : configurez-les dès maintenant
4. **Les rootkits sont rares sous Linux** : mais la vigilance reste importante
5. **Les logs racontent tout** : apprenez à les lire

**Configuration minimale recommandée :**

- ✅ Timeshift configuré avec snapshots automatiques
- ✅ SMART monitoring actif (smartd)
- ✅ Vérification mensuelle avec le script complet
- ✅ Memtest86+ dans GRUB (pour tests RAM si besoin)

**Avec ces pratiques, votre système Linux Mint restera sain et fiable pendant des années !** 🛡️🚀

---

## Pour aller plus loin

- **Section 17.1** : Timeshift pour sauvegardes système
- **Section 18.1** : Nettoyage du système
- **Section 18.4** : Optimisation SSD (SMART)
- **Section 18.5** : Gestion des logs
- **Section 23** : Dépannage et résolution de problèmes
- **Section 11.5** : Bonnes pratiques de sécurité

**Documentation :**
- `man smartctl`
- `man fsck`
- `man debsums`
- `man rkhunter`
- Site rkhunter : http://rkhunter.sourceforge.net/
- SMART : https://en.wikipedia.org/wiki/S.M.A.R.T.

⏭️ [Maintenance préventive (calendrier)](/18-maintenance-et-optimisation/08-maintenance-preventive.md)
