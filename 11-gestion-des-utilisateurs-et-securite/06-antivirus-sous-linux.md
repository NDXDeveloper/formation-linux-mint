🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 11.6 Antivirus sous Linux (ClamAV - nécessaire ?)

## Introduction

La question revient souvent : **"Ai-je besoin d'un antivirus sous Linux ?"** La réponse courte est : **probablement pas** pour un usage bureau classique. Mais comme toujours en sécurité informatique, la réponse complète est plus nuancée.

Dans ce chapitre, nous allons explorer :
- Pourquoi Linux est moins vulnérable aux virus
- Les cas où un antivirus peut être utile
- Comment installer et utiliser ClamAV, l'antivirus open source de référence sous Linux
- Les alternatives et compléments

---

## Linux et les virus : la réalité

### Pourquoi Linux est-il moins touché par les virus ?

#### 1. Architecture de sécurité robuste

**Séparation stricte des privilèges** :
- Les applications s'exécutent avec les droits de l'utilisateur, pas en administrateur
- Un virus ne peut infecter que le dossier personnel de l'utilisateur
- Impossible de modifier les fichiers système sans `sudo` (et le mot de passe)

**Exemple** : Sous Windows, beaucoup d'utilisateurs travaillent en compte administrateur. Sous Linux, même si vous êtes dans le groupe `sudo`, chaque action administrative nécessite votre mot de passe.

#### 2. Système de permissions

Chaque fichier a des permissions strictes (lecture, écriture, exécution). Un fichier téléchargé n'est **pas exécutable** par défaut.

```bash
# Fichier téléchargé
ls -l fichier_suspect.sh
-rw-r--r-- 1 sophie sophie 1024 nov 29 10:00 fichier_suspect.sh
```

Remarquez : pas de `x` (exécutable). Le fichier ne peut **pas** s'exécuter automatiquement, même si vous cliquez dessus.

#### 3. Gestion centralisée des logiciels

Sous Linux, vous installez principalement depuis des **dépôts officiels vérifiés** :
- Tous les paquets sont signés cryptographiquement
- Vérification automatique de l'intégrité
- Pas de téléchargement depuis des sites douteux

Comparé à Windows où on télécharge souvent des `.exe` depuis n'importe quel site...

#### 4. Code open source

- Le code de Linux et de la majorité des applications est **public**
- Des milliers de développeurs l'examinent
- Les failles sont détectées et corrigées rapidement
- Impossible de cacher des backdoors

#### 5. Part de marché

**Réalité économique** : Linux desktop représente ~3% du marché.
- Les créateurs de malwares ciblent Windows (70%+) pour maximiser leur "retour sur investissement"
- Moins rentable de créer des virus Linux

> **Important** : Ce n'est pas "par obscurité" (security by obscurity). Linux est intrinsèquement plus sécurisé, mais sa faible part de marché réduit aussi son attractivité pour les pirates.

### Les malwares Linux existent-ils ?

**Oui, mais ils sont rares** et ciblent principalement :

#### 1. Les serveurs

- **Rootkits** : Programmes cachés qui maintiennent un accès
- **Cryptominers** : Utilisent les ressources du serveur pour miner de la cryptomonnaie
- **Botnets** : Transforment le serveur en zombie pour des attaques DDoS
- **Ransomwares** : Chiffrent les données et demandent une rançon

**Exemples connus** :
- **Mirai** : Botnet ciblant les objets connectés Linux
- **Linux.Encoder** : Ransomware pour Linux
- **XORDDoS** : Malware de botnet DDoS

#### 2. Les systèmes mal configurés

- Serveurs SSH avec mot de passe faible
- Services exposés sur Internet sans protection
- Systèmes non mis à jour avec des vulnérabilités connues

#### 3. Pas vraiment les bureaux Linux

Pour un utilisateur Linux Mint classique, le risque de virus est **extrêmement faible**, à condition de suivre les bonnes pratiques de base.

---

## Ai-je besoin d'un antivirus sous Linux ?

### Non, si vous êtes dans ces cas :

- ✅ **Utilisation bureau standard** (navigation, bureautique, multimédia)
- ✅ **Vous installez uniquement depuis les dépôts officiels** (`apt`, Software Manager)
- ✅ **Vous ne partagez pas de fichiers avec des utilisateurs Windows**
- ✅ **Vous suivez les bonnes pratiques** (mises à jour, pas de clic sur n'importe quoi)
- ✅ **Vous ne gérez pas de serveurs accessibles depuis Internet**

Dans ces conditions, un antivirus est **inutile** et peut même :
- Ralentir le système
- Donner un faux sentiment de sécurité
- Consommer des ressources inutilement

### Oui, si vous êtes dans ces cas :

✅ **Vous gérez un serveur de fichiers Samba** (partage avec Windows)
- L'antivirus scanne les fichiers pour protéger les utilisateurs Windows
- Vous ne voulez pas propager des virus Windows

✅ **Vous recevez beaucoup de fichiers par email** (pièces jointes)
- Scanner les fichiers avant de les transférer à des collègues Windows
- Éviter de devenir un vecteur de propagation

✅ **Vous téléchargez des fichiers depuis des sources variées**
- Torrents, forums, sites de partage
- Scanner pour vérifier qu'il n'y a rien de suspect

✅ **Vous gérez plusieurs machines** (Windows et Linux)
- Scanner les disques Windows depuis Linux
- Nettoyer une infection Windows depuis un système Linux

✅ **Paranoia justifiée ou environnement hautement sécurisé**
- Secteur sensible (défense, finance, santé)
- Obligation réglementaire
- Approche défense en profondeur (plusieurs couches de sécurité)

### Cas d'usage principal : protection des autres

**Philosophie** : Sous Linux, un antivirus protège surtout **les autres** (utilisateurs Windows) plutôt que vous-même.

**Analogie** : C'est comme porter un masque quand on n'est pas malade. Vous ne risquez rien, mais vous protégez les autres.

---

## ClamAV : L'antivirus open source de référence

### Qu'est-ce que ClamAV ?

**ClamAV** (Clam AntiVirus) est :
- **Open source** et gratuit
- Le plus utilisé sous Linux
- Conçu principalement pour les **serveurs mail** et **passerelles**
- Détecte les virus Windows, Linux, macOS
- Mis à jour régulièrement (base de signatures)
- Léger et flexible

### Limites de ClamAV

**Soyons honnêtes** :
- ❌ Pas de protection en temps réel par défaut (mais possible avec ClamTk ou clamav-daemon)
- ❌ Taux de détection inférieur aux antivirus commerciaux Windows
- ❌ Orienté serveurs plus que bureaux
- ❌ Peut avoir des faux positifs

**Mais** :
- ✅ Parfait pour scanner des fichiers ponctuellement
- ✅ Gratuit et respectueux de la vie privée
- ✅ Excellent pour protéger les passerelles mail
- ✅ Idéal pour scanner des partitions Windows depuis Linux

---

## Installation de ClamAV

### Installation via APT

```bash
sudo apt update
sudo apt install clamav clamav-daemon
```

Paquets installés :
- **clamav** : Moteur d'analyse et outils en ligne de commande
- **clamav-daemon** : Service de scan en arrière-plan (optionnel)

### Mise à jour de la base de signatures

Avant la première utilisation, mettez à jour la base de données des virus :

```bash
sudo systemctl stop clamav-freshclam
sudo freshclam
sudo systemctl start clamav-freshclam
```

**Note** : `freshclam` est le service qui met à jour automatiquement les signatures de virus.

La mise à jour peut prendre quelques minutes la première fois (téléchargement de ~200 MB).

### Vérification de l'installation

```bash
clamscan --version
```

Résultat exemple :
```
ClamAV 1.0.0/26000/Thu Nov 29 10:30:00 2024
```

---

## Utilisation de ClamAV en ligne de commande

### Scanner un fichier

```bash
clamscan fichier.txt
```

Résultat si le fichier est sain :
```
fichier.txt: OK

----------- SCAN SUMMARY -----------
Known viruses: 8623929
Engine version: 1.0.0
Scanned directories: 0
Scanned files: 1
Infected files: 0
Data scanned: 0.00 MB
Data read: 0.00 MB (ratio 0.00:1)
Time: 0.152 sec (0 m 0 s)
Start Date: 2024:11:29 10:45:00
End Date:   2024:11:29 10:45:01
```

### Scanner un dossier (récursif)

```bash
clamscan -r /home/sophie/Téléchargements
```

L'option `-r` signifie "récursif" (tous les sous-dossiers).

### Scanner avec affichage uniquement des fichiers infectés

```bash
clamscan -r -i /home/sophie/Téléchargements
```

L'option `-i` affiche uniquement les fichiers infectés (pratique pour de gros scans).

### Scanner et supprimer les fichiers infectés

```bash
clamscan -r --remove /home/sophie/Téléchargements
```

> **Attention** : L'option `--remove` supprime **immédiatement** les fichiers détectés. Utilisez-la avec prudence !

Pour plus de sécurité, utilisez `--move` pour déplacer les fichiers suspects dans un dossier de quarantaine :

```bash
clamscan -r --move=/home/sophie/quarantaine /home/sophie/Téléchargements
```

### Scanner une partition Windows

Si vous avez Windows en dual-boot :

```bash
# Monter la partition Windows (si pas déjà montée)
sudo mkdir /mnt/windows
sudo mount /dev/sda2 /mnt/windows

# Scanner
sudo clamscan -r -i /mnt/windows
```

### Options utiles

| Option | Description |
|--------|-------------|
| `-r` | Scanner récursivement (dossiers et sous-dossiers) |
| `-i` | Afficher uniquement les fichiers infectés |
| `--remove` | Supprimer les fichiers infectés |
| `--move=DIR` | Déplacer les fichiers infectés vers DIR |
| `-l FICHIER` | Enregistrer le rapport dans FICHIER |
| `--bell` | Émettre un bip sonore si virus détecté |
| `--max-filesize=25M` | Limite de taille de fichier à scanner (par défaut 25M) |
| `--exclude=MOTIF` | Exclure les fichiers correspondant au motif |

### Exemple de scan complet avec rapport

```bash
clamscan -r -i --bell -l /home/sophie/scan_rapport.txt /home/sophie/
```

Cette commande :
- Scanne tout le dossier personnel (`-r`)
- Affiche uniquement les infections (`-i`)
- Émet un bip si infection (`--bell`)
- Enregistre le rapport dans `scan_rapport.txt` (`-l`)

### Scanner uniquement certains types de fichiers

```bash
clamscan -r /home/sophie/ --include="\.(exe|bat|dll|zip)$"
```

Scanne uniquement les fichiers `.exe`, `.bat`, `.dll` et `.zip`.

---

## ClamTk : Interface graphique pour ClamAV

Pour ceux qui préfèrent une interface graphique, **ClamTk** est parfait.

### Installation

```bash
sudo apt install clamtk
```

### Lancement

Depuis le menu : **Accessoires** → **ClamTk**

Ou en ligne de commande :
```bash
clamtk
```

### Utilisation de ClamTk

#### 1. Mettre à jour les signatures

- Au lancement, ClamTk propose de mettre à jour
- Ou cliquez sur **Aide** → **Vérifier les mises à jour**

#### 2. Scanner un fichier ou dossier

- Cliquez sur **Analyser un fichier** ou **Analyser un répertoire**
- Sélectionnez ce que vous voulez scanner
- Le scan démarre automatiquement

#### 3. Planifier des scans automatiques

- Cliquez sur **Planificateur**
- Configurez la fréquence (quotidienne, hebdomadaire)
- Choisissez les dossiers à scanner

#### 4. Configurer les préférences

- **Paramètres** → **Préférences**
- Activer/désactiver certaines options
- Définir les actions (quarantaine, suppression)

#### 5. Afficher l'historique

- **Historique** affiche tous les scans précédents
- Utile pour voir l'évolution

### Avantages de ClamTk

- ✅ Interface intuitive et simple
- ✅ Pas besoin de connaître les commandes
- ✅ Planification automatique facile
- ✅ Notifications visuelles
- ✅ Intégration au menu contextuel (clic droit sur fichier)

---

## Protection en temps réel avec ClamAV

Par défaut, ClamAV ne surveille **pas en temps réel**. Il faut lancer les scans manuellement. Pour une protection continue :

### Méthode 1 : Utiliser clamav-daemon

Le daemon `clamd` reste en mémoire et peut scanner à la demande plus rapidement.

#### Activer le daemon

```bash
sudo systemctl enable clamav-daemon
sudo systemctl start clamav-daemon
```

#### Scanner avec clamd (plus rapide)

```bash
clamdscan -r /home/sophie/Téléchargements
```

`clamdscan` utilise le daemon, ce qui est beaucoup plus rapide que `clamscan` pour des scans répétés.

### Méthode 2 : Surveillance de dossiers avec inotify

Pour surveiller un dossier et scanner automatiquement les nouveaux fichiers :

#### Installer inotify-tools

```bash
sudo apt install inotify-tools
```

#### Créer un script de surveillance

```bash
nano ~/scan_automatique.sh
```

Contenu du script :
```bash
#!/bin/bash

DOSSIER="/home/sophie/Téléchargements"

inotifywait -m -r -e create,moved_to "$DOSSIER" --format '%w%f' | while read FICHIER
do
    echo "Nouveau fichier détecté: $FICHIER"
    clamscan "$FICHIER"
done
```

Rendez le script exécutable :
```bash
chmod +x ~/scan_automatique.sh
```

Lancez-le :
```bash
~/scan_automatique.sh
```

Maintenant, chaque fichier ajouté dans Téléchargements sera automatiquement scanné.

### Méthode 3 : ClamTk avec surveillance

ClamTk peut surveiller des dossiers spécifiques en temps réel (fonctionnalité expérimentale).

Dans ClamTk : **Paramètres** → **Surveillance de répertoires**

---

## Automatiser les scans avec Cron

Pour scanner régulièrement sans y penser :

### Créer un script de scan

```bash
sudo nano /usr/local/bin/scan_quotidien.sh
```

Contenu :
```bash
#!/bin/bash

# Mettre à jour les signatures
freshclam

# Scanner le dossier home
clamscan -r -i --bell -l /var/log/clamav/scan_$(date +%Y%m%d).log /home/

# Envoyer un email si infection (optionnel)
if grep -q "Infected files: 0" /var/log/clamav/scan_$(date +%Y%m%d).log; then
    echo "Scan terminé. Aucune infection." | mail -s "Rapport ClamAV" votre@email.com
else
    echo "ATTENTION: Infection détectée !" | mail -s "ALERTE ClamAV" votre@email.com
fi
```

Rendez-le exécutable :
```bash
sudo chmod +x /usr/local/bin/scan_quotidien.sh
```

### Ajouter une tâche cron

```bash
sudo crontab -e
```

Ajoutez une ligne pour un scan quotidien à 3h du matin :
```
0 3 * * * /usr/local/bin/scan_quotidien.sh
```

Ou un scan hebdomadaire le dimanche à 2h :
```
0 2 * * 0 /usr/local/bin/scan_quotidien.sh
```

---

## Scanner les emails avec ClamAV

Si vous utilisez un serveur mail (Postfix, Dovecot), ClamAV peut scanner les emails entrants.

### Avec amavisd-new

```bash
sudo apt install amavisd-new
```

Configuration avancée requise (voir documentation spécifique).

### Pour Thunderbird (manuel)

Vous pouvez scanner les pièces jointes manuellement :

1. Enregistrez la pièce jointe
2. Scannez avec :
   ```bash
   clamscan piece_jointe.zip
   ```

Ou configurez un script pour scanner automatiquement les téléchargements.

---

## Alternatives et compléments à ClamAV

### ESET NOD32 Antivirus pour Linux

**Commercial** (payant), mais très efficace :
- Meilleur taux de détection que ClamAV
- Interface graphique moderne
- Support professionnel
- Protection en temps réel

**Prix** : ~30-40€/an

**Installation** : Téléchargez depuis le site officiel d'ESET.

### Sophos Antivirus pour Linux

**Gratuit pour un usage personnel** :
- Taux de détection professionnel
- Scan à la demande
- Interface graphique

**Installation** : Téléchargez depuis le site Sophos.

### Comodo Antivirus pour Linux

**Gratuit** :
- Protection en temps réel
- Interface graphique
- Développé par une société commerciale

**Installation** : Disponible sur le site de Comodo.

### RKHunter (Rootkit Hunter)

Pas un antivirus classique, mais un **détecteur de rootkits** :

```bash
sudo apt install rkhunter
sudo rkhunter --update
sudo rkhunter --check
```

RKHunter cherche :
- Les rootkits connus
- Les fichiers système modifiés
- Les ports suspects en écoute
- Les processus cachés

### Chkrootkit

Similaire à RKHunter :

```bash
sudo apt install chkrootkit
sudo chkrootkit
```

### LMD (Linux Malware Detect)

Spécialisé dans la **détection de malwares Linux** sur les serveurs :

```bash
cd /usr/local/src
sudo wget http://www.rfxn.com/downloads/maldetect-current.tar.gz
sudo tar -xzf maldetect-current.tar.gz
cd maldetect-*
sudo ./install.sh
```

Scanner :
```bash
sudo maldet -a /home
```

---

## Bonnes pratiques avec les antivirus sous Linux

### 1. Ne comptez pas uniquement sur l'antivirus

L'antivirus est **un outil parmi d'autres**, pas une solution miracle.

**Plus important** :
- ✅ Mises à jour régulières
- ✅ Pas de clic sur n'importe quoi
- ✅ Installations depuis sources fiables
- ✅ Pare-feu activé
- ✅ Permissions correctes

### 2. Mettez à jour les signatures régulièrement

```bash
sudo freshclam
```

Ou configurez les mises à jour automatiques (déjà actif avec `clamav-freshclam`).

### 3. Scannez les nouveaux fichiers téléchargés

Particulièrement :
- Fichiers `.exe`, `.bat`, `.dll` (même si vous êtes sous Linux)
- Archives `.zip`, `.rar` provenant de sources inconnues
- Pièces jointes d'emails

### 4. Scannez avant de partager

Si vous envoyez un fichier à un utilisateur Windows, scannez-le d'abord :

```bash
clamscan fichier_a_envoyer.zip
```

### 5. Ne scannez pas tout le système en permanence

Inutile et gourmand en ressources. Scannez plutôt :
- `/home` : Dossier personnel
- `/tmp` : Fichiers temporaires
- Points de montage de clés USB
- Dossiers de téléchargement

### 6. Vérifiez les faux positifs

ClamAV peut signaler des **faux positifs** (fichiers sains détectés comme malveillants).

Vérifiez avant de supprimer :
- Recherchez le nom du virus détecté sur Google
- Consultez la base de données ClamAV
- Soumettez le fichier à VirusTotal (https://www.virustotal.com)

### 7. Logs et rapports

Conservez des rapports de scan pour suivre l'évolution :

```bash
clamscan -r -l /var/log/clamav/scan_$(date +%Y%m%d).log /home/
```

---

## Performance et optimisation

### ClamAV est-il gourmand ?

**Scan ponctuel** : Utilisation CPU élevée pendant le scan, mais pas de problème.

**Daemon en mémoire** : ~200-300 MB de RAM en permanence.

### Optimiser les performances

#### 1. Exclure les dossiers inutiles

```bash
clamscan -r --exclude-dir="^/home/sophie/.cache" /home/sophie/
```

Dossiers à exclure typiquement :
- `.cache`
- `.local/share/Trash`
- Dossiers de compilation

#### 2. Limiter la taille des fichiers scannés

```bash
clamscan -r --max-filesize=100M /home/sophie/
```

Les très gros fichiers (vidéos, ISOs) sont rarement infectés et ralentissent le scan.

#### 3. Scanner pendant les heures creuses

Utilisez cron pour scanner la nuit :
```
0 3 * * * clamscan -r /home/sophie/
```

#### 4. Scanner uniquement les nouveaux fichiers

Avec `find`, scanner uniquement les fichiers modifiés dans les dernières 24h :

```bash
find /home/sophie/Téléchargements -type f -mtime -1 -exec clamscan {} \;
```

---

## Dépannage

### "Database contains 0 signatures"

**Problème** : La base de signatures n'est pas chargée.

**Solution** :
```bash
sudo systemctl stop clamav-freshclam
sudo freshclam
sudo systemctl start clamav-freshclam
```

### "Can't access file"

**Problème** : Permissions insuffisantes.

**Solution** : Utilisez `sudo` :
```bash
sudo clamscan -r /chemin/
```

### Scans très lents

**Problème** : Trop de fichiers ou fichiers trop gros.

**Solutions** :
- Exclure les dossiers de cache
- Limiter la taille max des fichiers (`--max-filesize`)
- Utiliser `clamdscan` au lieu de `clamscan`
- Scanner uniquement les fichiers récents

### Erreur "Clamd is not running"

**Problème** : Le daemon n'est pas démarré.

**Solution** :
```bash
sudo systemctl start clamav-daemon
sudo systemctl status clamav-daemon
```

### Faux positifs constants

**Problème** : ClamAV détecte des fichiers sains.

**Solution** :
1. Vérifiez avec VirusTotal
2. Signalez le faux positif à ClamAV
3. Ajoutez une exception dans `/etc/clamav/clamd.conf` :
   ```
   ExcludePath /chemin/vers/fichier
   ```

---

## Faut-il vraiment un antivirus sous Linux ?

### Le consensus de la communauté

**Pour un bureau Linux** : **Non**, dans la majorité des cas.

**Arguments CONTRE** :
- Linux est déjà sécurisé par conception
- Les bonnes pratiques sont plus efficaces
- Faux sentiment de sécurité
- Consommation de ressources

**Arguments POUR** :
- Défense en profondeur
- Protection des utilisateurs Windows
- Secteurs réglementés
- Serveurs de fichiers

### Notre recommandation

**Utilisateur classique Linux Mint** :
- ❌ **Pas d'antivirus résident** en temps réel
- ✅ **ClamAV installé** pour scans ponctuels
- ✅ **Bonnes pratiques** avant tout

**Serveur de fichiers / Passerelle mail** :
- ✅ **ClamAV obligatoire** pour protéger les clients
- ✅ **Scan automatique** des fichiers

**Environnement mixte Linux/Windows** :
- ✅ **ClamAV utile** pour scanner avant partage
- ✅ **Scan des partitions Windows** depuis Linux

### L'essentiel

> **Principe fondamental** : Un antivirus **ne remplace jamais** les bonnes pratiques de sécurité.

**Priorités** (dans l'ordre) :
1. 🥇 **Mises à jour** régulières
2. 🥈 **Comportement prudent** (pas de clic hasardeux)
3. 🥉 **Pare-feu** activé
4. **Sauvegardes** régulières
5. **Antivirus** (optionnel)

---

## Commandes de référence rapide

### Installation et mise à jour

| Commande | Description |
|----------|-------------|
| `sudo apt install clamav clamav-daemon` | Installer ClamAV |
| `sudo apt install clamtk` | Installer l'interface graphique |
| `sudo freshclam` | Mettre à jour les signatures |
| `clamscan --version` | Vérifier la version |

### Scans de base

| Commande | Description |
|----------|-------------|
| `clamscan fichier.txt` | Scanner un fichier |
| `clamscan -r /dossier/` | Scanner un dossier (récursif) |
| `clamscan -r -i /dossier/` | Scanner et afficher uniquement les infections |
| `clamscan -r --remove /dossier/` | Scanner et supprimer les infections |
| `clamscan -r --move=/quarantaine /dossier/` | Scanner et déplacer les infections |

### Scans avancés

| Commande | Description |
|----------|-------------|
| `clamdscan -r /dossier/` | Scanner avec le daemon (plus rapide) |
| `clamscan -r -l rapport.txt /dossier/` | Scanner et enregistrer le rapport |
| `clamscan -r --max-filesize=50M /dossier/` | Limiter la taille des fichiers |
| `clamscan -r --exclude-dir="^/home/.cache" /home/` | Exclure un dossier |

### Gestion du daemon

| Commande | Description |
|----------|-------------|
| `sudo systemctl start clamav-daemon` | Démarrer le daemon |
| `sudo systemctl stop clamav-daemon` | Arrêter le daemon |
| `sudo systemctl status clamav-daemon` | Vérifier l'état |
| `sudo systemctl enable clamav-daemon` | Activer au démarrage |

### Outils complémentaires

| Commande | Description |
|----------|-------------|
| `sudo rkhunter --check` | Vérifier les rootkits |
| `sudo chkrootkit` | Vérifier les rootkits (alternatif) |
| `sudo maldet -a /home/` | Scanner avec LMD |

---

## Résumé

### Points clés à retenir

1. **Linux n'a généralement pas besoin d'antivirus** pour un usage bureau classique
2. **ClamAV est utile** pour :
   - Protéger les utilisateurs Windows
   - Scanner des fichiers suspects ponctuellement
   - Serveurs de fichiers et passerelles mail
3. **Les bonnes pratiques** sont plus importantes qu'un antivirus
4. **Un antivirus ne remplace pas** la vigilance et la maintenance régulière

### Recommandation finale

**Installation minimale recommandée** :
```bash
sudo apt install clamav
```

**Usage** : Scans ponctuels quand nécessaire, pas de surveillance en temps réel.

**Focus** : Concentrez-vous sur les mises à jour, les bonnes pratiques et le pare-feu. Ce sont vos vraies protections.

### Et si vous êtes toujours inquiet ?

C'est normal. Dans ce cas :
- ✅ Installez ClamAV et ClamTk
- ✅ Planifiez un scan hebdomadaire
- ✅ Mais surtout, **maintenez votre système à jour** et **soyez vigilant**

La tranquillité d'esprit a aussi sa valeur !

---


⏭️ [Pare-feu avancé et règles personnalisées](/11-gestion-des-utilisateurs-et-securite/07-pare-feu-avance-et-regles-personnalisees.md)
