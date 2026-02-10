🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 23.4 Réparation du GRUB

## Introduction

GRUB (Grand Unified Bootloader) est le programme qui s'exécute au tout début du démarrage de votre ordinateur et qui vous permet de choisir quel système d'exploitation lancer. Quand GRUB ne fonctionne plus, votre ordinateur ne peut plus démarrer Linux Mint (et parfois même Windows si vous êtes en dual-boot).

**Rassurez-vous :** Un GRUB cassé ne signifie PAS que vos données sont perdues ! Vos fichiers sont toujours intacts sur le disque dur. Il suffit de réparer ce petit programme de démarrage pour retrouver l'accès à votre système.

Ce guide vous accompagne pas à pas pour réparer GRUB, même si vous êtes débutant.

---

## Qu'est-ce que GRUB exactement ?

### Définition simple

GRUB est le **premier programme** qui se lance quand vous allumez votre ordinateur :

1. **Vous appuyez** sur le bouton d'alimentation
2. **Le BIOS/UEFI** s'active (test matériel rapide)
3. **GRUB** se charge → C'est lui qui affiche le menu au démarrage
4. **GRUB** lance le système d'exploitation que vous choisissez (Linux Mint, Windows, etc.)

### À quoi ressemble GRUB ?

Vous avez probablement déjà vu GRUB sans le savoir :

```
                    GNU GRUB version 2.06

Ubuntu  
Options avancées pour Ubuntu  
Windows Boot Manager (sur /dev/sda1)  
Memory test (memtest86+)  

Use ↑ and ↓ to select which entry is highlighted.  
Press enter to boot the selected OS...  
```

C'est cet écran avec fond noir (ou violet) qui liste vos systèmes d'exploitation.

### Où se trouve GRUB ?

GRUB est installé dans deux endroits :

1. **Dans le MBR/ESP** (Master Boot Record ou EFI System Partition)
   - Tout au début du disque dur
   - C'est le "lanceur" principal

2. **Dans la partition Linux** (généralement `/boot/grub`)
   - Fichiers de configuration
   - Modules et thèmes

---

## Symptômes d'un GRUB cassé

Comment savoir si votre problème vient de GRUB ?

### Symptôme 1 : Message "grub rescue>"

**Ce que vous voyez :**
```
error: no such partition  
Entering rescue mode...  
grub rescue>  
```

**Ce que ça signifie :**
- GRUB ne trouve plus la partition où Linux est installé
- Généralement après un redimensionnement de partition ou installation/désinstallation d'un OS

**Gravité :** Réparable ⭐⭐ (moyen)

---

### Symptôme 2 : Message "GRUB" seul ou "GRUB Loading"

**Ce que vous voyez :**
```
GRUB
```
ou
```
GRUB Loading...
```
Puis plus rien, écran figé.

**Ce que ça signifie :**
- Le chargeur GRUB démarre mais ne peut pas charger ses fichiers
- Problème de corruption ou mauvaise installation

**Gravité :** Réparable ⭐⭐ (moyen)

---

### Symptôme 3 : "Operating System not found" ou "No bootable device"

**Ce que vous voyez :**
```
Operating System not found
```
ou
```
No bootable device found
```
ou
```
BOOTMGR is missing
```

**Ce que ça signifie :**
- GRUB n'est même pas détecté
- Le BIOS/UEFI ne trouve aucun bootloader
- Souvent après une réinstallation de Windows

**Gravité :** Réparable ⭐⭐⭐ (nécessite plus d'étapes)

---

### Symptôme 4 : Menu GRUB incomplet (manque Windows en dual-boot)

**Ce que vous voyez :**
- Le menu GRUB s'affiche normalement
- Linux Mint est présent
- Mais Windows n'apparaît pas (alors qu'il est installé)

**Ce que ça signifie :**
- GRUB fonctionne mais n'a pas détecté Windows
- Simple mise à jour de configuration nécessaire

**Gravité :** Facile à réparer ⭐ (très simple)

---

## Causes courantes de problèmes GRUB

Comprendre la cause vous aidera à éviter le problème à l'avenir :

### Cause 1 : Réinstallation de Windows

**Pourquoi :** Windows réinstalle son propre bootloader et écrase GRUB

**Prévention :** Installer Windows AVANT Linux, pas après

---

### Cause 2 : Modification des partitions

**Pourquoi :** Redimensionner, supprimer, ou déplacer des partitions change leurs identifiants (UUID)

**Prévention :** Créer un snapshot Timeshift avant toute modification de partition

---

### Cause 3 : Mise à jour Windows qui touche au boot

**Pourquoi :** Certaines grosses mises à jour Windows (feature updates) modifient la partition EFI

**Prévention :** Garder une clé USB de secours Linux Mint

---

### Cause 4 : Corruption du système de fichiers

**Pourquoi :** Extinction forcée, coupure de courant, secteur défectueux sur le disque

**Prévention :** Utiliser un onduleur, éteindre proprement

---

### Cause 5 : Mauvaise manipulation

**Pourquoi :** Suppression de fichiers dans `/boot/grub` ou commandes incorrectes

**Prévention :** Ne jamais modifier `/boot` sans savoir exactement ce que vous faites

---

## Prérequis : Créer une clé USB bootable de Linux Mint

Pour réparer GRUB, vous aurez besoin d'une clé USB bootable de Linux Mint.

### Si vous avez encore accès à un ordinateur fonctionnel

#### Depuis Windows :

1. **Téléchargez** Linux Mint ISO depuis https://linuxmint.com/download.php
2. **Téléchargez Rufus** depuis https://rufus.ie/
3. **Lancez Rufus**
4. **Sélectionnez** votre clé USB (minimum 4 Go)
5. **Sélectionnez** le fichier ISO de Linux Mint
6. **Cliquez** sur "Démarrer"
7. **Attendez** la fin de la création

#### Depuis Linux :

```bash
# Installer mintstick (outil officiel)
sudo apt install mintstick

# Lancer l'outil graphique
Menu → Accessoires → Graveur de clé USB
```

Ou utilisez **Etcher** (https://www.balena.io/etcher/) qui fonctionne partout.

### Vérification de la clé USB

Redémarrez et testez que vous pouvez démarrer sur la clé USB :
1. Insérez la clé USB
2. Redémarrez
3. Appuyez sur **F12** (ou F9, F10, Échap selon le fabricant)
4. Sélectionnez la clé USB
5. Le menu de Linux Mint devrait apparaître

**Important :** Si vous ne voyez pas le menu USB, vérifiez les paramètres BIOS/UEFI :
- "Secure Boot" doit être désactivé (ou configuré pour Linux)
- "Fast Boot" / "Quick Boot" peut être désactivé
- L'ordre de boot peut mettre USB en premier

---

## Méthode 1 : Mise à jour simple de GRUB (problème mineur)

**Utilisez cette méthode si :**
- Linux démarre normalement
- Mais Windows n'apparaît pas dans le menu GRUB
- Ou le menu GRUB ne se met pas à jour

### Depuis Linux Mint démarré normalement

Ouvrez un terminal et tapez :

```bash
sudo update-grub
```

**Résultat attendu :**

```
Sourcing file `/etc/default/grub'  
Sourcing file `/etc/default/grub.d/50_linuxmint.cfg'  
Generating grub configuration file ...  
Found linux image: /boot/vmlinuz-5.15.0-91-generic  
Found initrd image: /boot/initrd.img-5.15.0-91-generic  
Found Windows Boot Manager on /dev/sda1  
done  
```

La ligne **"Found Windows Boot Manager"** confirme que Windows a été détecté.

**Si Windows n'est pas détecté :**

```bash
# Installer os-prober (détecte les autres OS)
sudo apt install os-prober

# Activer os-prober dans GRUB
sudo nano /etc/default/grub

# Ajoutez cette ligne à la fin du fichier :
GRUB_DISABLE_OS_PROBER=false

# Sauvegardez (Ctrl+O, Entrée) et quittez (Ctrl+X)

# Mettre à jour GRUB
sudo update-grub
```

**Redémarrez** et vérifiez que Windows apparaît maintenant dans le menu GRUB.

---

## Méthode 2 : Boot-Repair (outil automatique - RECOMMANDÉ pour débutants)

**Boot-Repair** est un outil graphique qui répare automatiquement GRUB. C'est la méthode la plus simple et la plus sûre pour les débutants.

### Étape 1 : Démarrer sur la clé USB Live

1. **Insérez** la clé USB de Linux Mint
2. **Redémarrez** l'ordinateur
3. **Appuyez** sur F12 (menu de boot)
4. **Sélectionnez** la clé USB
5. **Choisissez** "Start Linux Mint" (mode Live)

### Étape 2 : Se connecter à Internet

**Si vous avez l'Ethernet :** C'est automatique, passez à l'étape suivante.

**Si vous êtes en WiFi :**
1. Cliquez sur l'icône réseau (en bas à droite)
2. Sélectionnez votre réseau WiFi
3. Entrez le mot de passe

**Vérifiez la connexion :**
Ouvrez un terminal et tapez :
```bash
ping -c 3 google.com
```
Si vous voyez des réponses, c'est bon.

### Étape 3 : Installer Boot-Repair

Ouvrez un terminal et tapez (ligne par ligne) :

```bash
sudo add-apt-repository ppa:yannubuntu/boot-repair  
sudo apt update  
sudo apt install -y boot-repair  
```

**Note :** Ces commandes sont sûres, elles ne modifient rien encore.

### Étape 4 : Lancer Boot-Repair

```bash
boot-repair
```

Une fenêtre graphique s'ouvre.

### Étape 5 : Réparation recommandée (automatique)

**Pour la plupart des cas :**

1. Cliquez sur **"Recommended repair"** (Réparation recommandée)
2. **Attendez** (ça peut prendre 5-10 minutes)
3. Des commandes s'affichent dans le terminal → c'est normal
4. Boot-Repair peut vous demander d'exécuter des commandes dans le terminal
   - **Copiez-collez** exactement ce qui est demandé
   - **Appuyez** sur Entrée
5. À la fin, Boot-Repair affiche un **résumé** et une **URL de rapport**
6. **Notez cette URL** (utile si vous devez demander de l'aide)
7. Cliquez sur **OK**

### Étape 6 : Redémarrer

```bash
sudo reboot
```

**Retirez la clé USB** quand l'ordinateur redémarre.

**Résultat attendu :**
- Le menu GRUB apparaît
- Vous pouvez démarrer Linux Mint
- Windows apparaît aussi dans le menu (si dual-boot)

### Options avancées de Boot-Repair (optionnel)

Si la réparation recommandée ne fonctionne pas, cliquez sur **"Advanced options"** :

**Onglet "GRUB location" :**
- **Séparer /boot/efi :** Activez si vous avez une partition EFI séparée
- **Reinstall GRUB :** Choisissez sur quel disque (/dev/sda, /dev/nvme0n1, etc.)

**Onglet "GRUB options" :**
- **Purge and reinstall GRUB :** Réinstallation complète de GRUB
- **Restore MBR :** Pour systèmes BIOS Legacy (ancien)
- **Restore EFI backups :** Pour systèmes UEFI

**Onglet "Other options" :**
- **Repair filesystem :** Répare aussi le système de fichiers
- **Add kernel option :** Ajoute des options au boot (nomodeset, etc.)

**Pour la plupart des cas, laissez les options par défaut.**

---

## Méthode 3 : Réparation manuelle via chroot (pour utilisateurs intermédiaires)

Cette méthode donne plus de contrôle mais nécessite d'être à l'aise avec le terminal.

### Étape 1 : Démarrer en mode Live

Même procédure que Méthode 2, Étape 1.

### Étape 2 : Identifier vos partitions

Ouvrez un terminal et tapez :

```bash
sudo fdisk -l
```

Ou pour une vue plus claire :

```bash
lsblk
```

**Exemple de sortie :**
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT  
sda      8:0    0   500G  0 disk  
├─sda1   8:1    0   512M  0 part         ← Partition EFI (si UEFI)
├─sda2   8:2    0   100G  0 part         ← Windows
└─sda3   8:3    0   400G  0 part         ← Linux Mint
```

**Identifiez :**
- **Partition Linux racine** (/, généralement la plus grosse partition Linux) → exemple : `/dev/sda3`
- **Partition EFI** (si UEFI, ~512 Mo, type FAT32) → exemple : `/dev/sda1`
- **Partition boot** (si vous en avez une séparée, rare) → exemple : `/dev/sda2`

**Pour vérifier les types de partitions :**
```bash
sudo blkid
```

### Étape 3 : Monter la partition Linux

```bash
# Créer le point de montage
sudo mkdir -p /mnt/linux

# Monter la partition racine (remplacez sda3 par VOTRE partition)
sudo mount /dev/sda3 /mnt/linux
```

**Vérifiez que ça a fonctionné :**
```bash
ls /mnt/linux
```
Vous devriez voir : `bin  boot  dev  etc  home  lib  ...`

### Étape 4 : Monter les systèmes virtuels

Ces montages permettent à chroot de fonctionner correctement :

```bash
sudo mount --bind /dev /mnt/linux/dev  
sudo mount --bind /dev/pts /mnt/linux/dev/pts  
sudo mount --bind /proc /mnt/linux/proc  
sudo mount --bind /sys /mnt/linux/sys  
```

### Étape 5 : Monter la partition EFI (UNIQUEMENT si UEFI)

**Comment savoir si vous êtes en UEFI ou BIOS Legacy ?**

```bash
[ -d /sys/firmware/efi ] && echo "UEFI" || echo "BIOS Legacy"
```

**Si UEFI :**

```bash
# Monter la partition EFI (remplacez sda1 par VOTRE partition EFI)
sudo mount /dev/sda1 /mnt/linux/boot/efi
```

**Si BIOS Legacy :** Sautez cette étape.

### Étape 6 : Entrer dans l'environnement chroot

```bash
sudo chroot /mnt/linux
```

Votre prompt change → vous êtes maintenant "à l'intérieur" de votre système Linux installé.

### Étape 7 : Réinstaller GRUB

**Si UEFI :**

```bash
# Réinstaller GRUB sur le disque (pas la partition, donc /dev/sda et non /dev/sda1)
grub-install /dev/sda

# Mettre à jour la configuration
update-grub
```

**Si BIOS Legacy :**

```bash
# Réinstaller GRUB dans le MBR
grub-install /dev/sda

# Mettre à jour la configuration
update-grub
```

**Résultat attendu :**

```
Installing for x86_64-efi platform.  
Installation finished. No error reported.  
Sourcing file `/etc/default/grub'  
...
Found Windows Boot Manager on /dev/sda2  
done  
```

### Étape 8 : Sortir de chroot et démonter

```bash
# Sortir de chroot
exit

# Démonter dans l'ordre inverse
sudo umount /mnt/linux/boot/efi  # Si UEFI seulement  
sudo umount /mnt/linux/dev/pts  
sudo umount /mnt/linux/dev  
sudo umount /mnt/linux/proc  
sudo umount /mnt/linux/sys  
sudo umount /mnt/linux  
```

### Étape 9 : Redémarrer

```bash
sudo reboot
```

Retirez la clé USB et votre système devrait démarrer normalement.

---

## Méthode 4 : Réparation depuis grub rescue> (dépannage d'urgence)

Si vous êtes bloqué à l'écran `grub rescue>`, vous pouvez tenter un démarrage temporaire.

### Étape 1 : Identifier la partition Linux

Au prompt `grub rescue>`, tapez :

```
ls
```

**Résultat exemple :**
```
(hd0) (hd0,gpt1) (hd0,gpt2) (hd0,gpt3)
```

Testez chaque partition pour trouver celle qui contient Linux :

```
ls (hd0,gpt1)/  
ls (hd0,gpt2)/  
ls (hd0,gpt3)/  
```

Cherchez celle qui affiche des dossiers comme `boot`, `etc`, `home`, `usr`.

**Exemple :** Si `(hd0,gpt3)/` affiche ces dossiers, c'est votre partition Linux.

### Étape 2 : Configurer GRUB temporairement

```
set prefix=(hd0,gpt3)/boot/grub  
set root=(hd0,gpt3)  
insmod normal  
normal  
```

**Remplacez (hd0,gpt3) par votre partition identifiée à l'étape 1.**

Le menu GRUB normal devrait apparaître.

### Étape 3 : Démarrer Linux normalement

Sélectionnez Linux Mint et démarrez.

### Étape 4 : Réparer GRUB définitivement

Une fois Linux démarré, ouvrez un terminal :

```bash
sudo update-grub  
sudo grub-install /dev/sda  # Remplacez sda par votre disque  
```

**Redémarrez** pour vérifier que c'est réparé définitivement.

---

## Cas particulier : Dual-boot avec Windows

### Problème : Windows a écrasé GRUB

**Symptôme :** Après une réinstallation de Windows, l'ordinateur démarre directement sur Windows, pas de menu GRUB.

**Solution :** Utilisez Boot-Repair (Méthode 2) ou la réparation manuelle (Méthode 3).

**Astuce :** Boot-Repair détecte automatiquement Windows et le réintègre au menu GRUB.

---

### Problème : Windows n'apparaît pas dans GRUB

**Solution rapide :**

```bash
# Activer os-prober
sudo nano /etc/default/grub

# Ajouter à la fin :
GRUB_DISABLE_OS_PROBER=false

# Sauvegarder et quitter (Ctrl+O, Entrée, Ctrl+X)

# Mettre à jour GRUB
sudo update-grub
```

**Si ça ne fonctionne toujours pas :**

```bash
# Réinstaller os-prober
sudo apt install --reinstall os-prober

# Forcer la détection
sudo os-prober  
sudo update-grub  
```

---

### Problème : Démarrage direct sur Windows sans menu GRUB

**Vérifiez l'ordre de boot dans le BIOS/UEFI :**

1. Redémarrez et entrez dans le BIOS/UEFI (F2, Del, F10)
2. Cherchez "Boot Order" ou "Ordre de démarrage"
3. **ubuntu** ou **linuxmint** doit être AVANT **Windows Boot Manager**
4. Sauvegardez et redémarrez

**Si "ubuntu" n'apparaît pas dans la liste :**
→ Utilisez Boot-Repair pour réinstaller GRUB dans l'EFI.

---

## Cas particulier : Systèmes UEFI

Les systèmes UEFI ont une partition spéciale (ESP - EFI System Partition) où GRUB doit être installé.

### Vérifier que vous êtes en UEFI

```bash
[ -d /sys/firmware/efi ] && echo "UEFI" || echo "BIOS Legacy"
```

### Problème : Partition EFI pleine

**Symptôme :** `grub-install` échoue avec "No space left on device"

**Solution :**

1. Monter la partition EFI :
```bash
sudo mount /dev/sda1 /mnt  # Remplacez sda1 par votre partition EFI
```

2. Nettoyer les anciens fichiers :
```bash
# Sauvegarder d'abord
sudo cp -r /mnt/EFI /mnt/EFI.backup

# Supprimer les anciennes entrées Ubuntu/Linux
sudo rm -rf /mnt/EFI/ubuntu.old  
sudo rm -rf /mnt/EFI/debian  

# Vérifier l'espace
df -h /mnt
```

3. Réinstaller GRUB :
```bash
sudo grub-install /dev/sda  
sudo update-grub  
```

---

### Problème : Secure Boot bloque GRUB

**Symptôme :** L'ordinateur refuse de démarrer sur GRUB (écran noir ou message "Secure Boot violation")

**Solution 1 : Désactiver Secure Boot (recommandé)**

1. Entrez dans le BIOS/UEFI
2. Cherchez "Secure Boot"
3. Désactivez-le (Disabled)
4. Sauvegardez et redémarrez

**Solution 2 : Utiliser GRUB signé (avancé)**

Si vous voulez garder Secure Boot activé :

```bash
sudo apt install shim-signed grub-efi-amd64-signed  
sudo update-grub  
```

---

## Vérifications après réparation

Une fois GRUB réparé, vérifiez que tout fonctionne :

### Test 1 : Le menu GRUB apparaît

Au redémarrage :
- ✅ Le menu GRUB s'affiche (même brièvement)
- ✅ Vous voyez les entrées Linux Mint

### Test 2 : Linux démarre normalement

- ✅ Vous pouvez sélectionner Linux Mint et démarrer
- ✅ Pas de messages d'erreur

### Test 3 : Windows démarre (si dual-boot)

- ✅ Windows apparaît dans le menu GRUB
- ✅ Vous pouvez démarrer Windows

### Test 4 : Vérification technique

Une fois Linux démarré, vérifiez l'installation de GRUB :

```bash
# Vérifier que GRUB est installé
sudo grub-install --version

# Vérifier les entrées de boot
sudo efibootmgr  # Pour UEFI
# ou
sudo grub-install --recheck /dev/sda  # Pour BIOS
```

---

## Personnalisation de GRUB après réparation

### Modifier le délai d'affichage du menu

Par défaut, GRUB affiche le menu pendant 10 secondes.

```bash
sudo nano /etc/default/grub
```

Modifiez cette ligne :
```
GRUB_TIMEOUT=10
```

**Exemples :**
- `GRUB_TIMEOUT=3` → Menu pendant 3 secondes
- `GRUB_TIMEOUT=0` → Démarre directement (sans menu)
- `GRUB_TIMEOUT=-1` → Menu infini (attend votre choix)

Sauvegardez et mettez à jour :
```bash
sudo update-grub
```

---

### Changer le système par défaut

Si vous voulez démarrer sur Windows par défaut :

```bash
sudo nano /etc/default/grub
```

Modifiez :
```
GRUB_DEFAULT=0
```

**Options :**
- `GRUB_DEFAULT=0` → Première entrée (généralement Linux)
- `GRUB_DEFAULT=2` → Troisième entrée (compter à partir de 0)
- `GRUB_DEFAULT="Windows Boot Manager"` → Windows par le nom
- `GRUB_DEFAULT=saved` → Mémorise le dernier choix

Sauvegardez et mettez à jour :
```bash
sudo update-grub
```

---

### Changer l'apparence de GRUB

**Thèmes GRUB :**

```bash
# Installer un thème (exemple)
sudo apt install grub2-themes-ubuntu-mate

# Configurer
sudo nano /etc/default/grub

# Ajouter :
GRUB_THEME="/boot/grub/themes/ubuntu-mate/theme.txt"

# Mettre à jour
sudo update-grub
```

Pour d'autres thèmes : https://www.gnome-look.org/browse?cat=109

---

### Afficher le menu GRUB à chaque démarrage

Si GRUB est masqué :

```bash
sudo nano /etc/default/grub
```

Commentez cette ligne (ajoutez # devant) :
```
#GRUB_TIMEOUT_STYLE=hidden
```

Assurez-vous que cette ligne existe :
```
GRUB_TIMEOUT=10
```

Sauvegardez et mettez à jour :
```bash
sudo update-grub
```

---

## Prévention des problèmes GRUB

### Bonne pratique 1 : Ordre d'installation en dual-boot

**Toujours installer dans cet ordre :**
1. Windows d'abord
2. Linux Mint ensuite

**Pourquoi ?** Parce que Windows écrase le bootloader, alors que Linux détecte Windows.

### Bonne pratique 2 : Créer une clé USB de secours

Gardez toujours une clé USB bootable de Linux Mint à jour.

### Bonne pratique 3 : Sauvegarder la configuration GRUB

```bash
# Créer une sauvegarde
sudo cp -r /boot/grub /boot/grub.backup  
sudo cp /etc/default/grub /etc/default/grub.backup  
```

### Bonne pratique 4 : Noter votre configuration de partitions

Documentez vos partitions :
```bash
lsblk > ~/mes-partitions.txt  
sudo blkid >> ~/mes-partitions.txt  
```

Gardez ce fichier sur un cloud ou une clé USB.

### Bonne pratique 5 : Désactiver les mises à jour Windows automatiques du bootloader

Dans Windows, vous pouvez désactiver les modifications du bootloader (GPO ou registre), mais c'est avancé.

**Plus simple :** Créez des snapshots Timeshift réguliers.

---

## Outils graphiques supplémentaires

### GRUB Customizer (personnalisation facile)

Un outil graphique pour configurer GRUB sans éditer des fichiers :

```bash
sudo add-apt-repository ppa:danielrichter2007/grub-customizer  
sudo apt update  
sudo apt install grub-customizer  
```

**Lancement :**
Menu → Administration → Grub Customizer

**Fonctionnalités :**
- Modifier l'ordre des entrées
- Changer le système par défaut
- Modifier le délai
- Installer des thèmes
- Ajouter/supprimer des entrées

**⚠️ Attention :** Utilisez avec précaution, une mauvaise configuration peut empêcher le démarrage.

---

### Super GRUB2 Disk (outil de dépannage)

Un disque de secours spécialisé pour GRUB :

1. **Téléchargez** depuis https://www.supergrubdisk.org/
2. **Créez** une clé USB bootable avec l'ISO
3. **Démarrez** dessus en cas de problème
4. **Sélectionnez** "Detect and show boot methods"
5. **Choisissez** votre Linux ou Windows

Super GRUB2 Disk peut démarrer votre système même si GRUB est complètement cassé.

---

## Tableau de dépannage rapide

| Symptôme | Cause probable | Solution rapide |
|----------|----------------|-----------------|
| grub rescue> | Partition déplacée | Méthode 4 (grub rescue) |
| "GRUB" figé | Fichiers corrompus | Boot-Repair (Méthode 2) |
| No bootable device | GRUB écrasé | Boot-Repair (Méthode 2) |
| Windows manquant | os-prober désactivé | `sudo update-grub` |
| Menu ne s'affiche pas | Timeout à 0 | Éditer `/etc/default/grub` |
| Secure Boot violation | Secure Boot actif | Désactiver Secure Boot |
| Démarre sur Windows directement | Ordre de boot UEFI | Modifier ordre dans BIOS |

---

## FAQ - Questions fréquentes

### Puis-je réparer GRUB sans clé USB ?

**Non**, si GRUB est cassé au point que Linux ne démarre plus. Vous avez besoin d'un environnement Live.

**Exception :** Si Linux démarre encore (juste le menu GRUB qui manque Windows), vous pouvez réparer depuis Linux avec `sudo update-grub`.

### Boot-Repair va-t-il supprimer mes données ?

**Non**, Boot-Repair ne touche qu'au bootloader, pas à vos fichiers personnels.

### Combien de temps prend la réparation ?

- **Boot-Repair automatique :** 5-10 minutes
- **Réparation manuelle :** 15-30 minutes (selon votre vitesse)

### Que faire si Boot-Repair échoue ?

1. Notez l'**URL du rapport** affiché par Boot-Repair
2. Postez cette URL sur les forums Linux Mint
3. Essayez la **Méthode 3** (réparation manuelle)
4. En dernier recours, **réinstaller Linux** (vos données peuvent être sauvegardées avant)

### Puis-je avoir plusieurs GRUB sur plusieurs disques ?

**Techniquement oui**, mais c'est compliqué et source de problèmes. Recommandation : un seul GRUB sur le disque principal.

### Mon ordinateur démarre toujours sur Windows, jamais GRUB

**Vérifiez :**
1. L'ordre de boot dans le BIOS/UEFI
2. Que GRUB est bien installé : `sudo efibootmgr` (UEFI) ou vérifiez le MBR
3. Utilisez Boot-Repair avec option "Reinstall GRUB"

### GRUB est réparé mais Linux ne démarre pas (écran noir)

**Ce n'est pas un problème GRUB**, c'est un problème de système (pilotes graphiques, kernel, etc.). Voir chapitre 23.2.

---

## Commandes de référence rapide

### Vérifier votre système

```bash
# Système UEFI ou BIOS ?
[ -d /sys/firmware/efi ] && echo "UEFI" || echo "BIOS Legacy"

# Lister les partitions
lsblk  
sudo fdisk -l  
sudo blkid  

# Entrées de boot UEFI
sudo efibootmgr -v
```

### Mise à jour GRUB

```bash
# Mettre à jour la configuration
sudo update-grub

# Réinstaller GRUB
sudo grub-install /dev/sda  # Remplacer sda par votre disque

# Vérifier l'installation
sudo grub-install --version
```

### Montage pour chroot (réparation manuelle)

```bash
# Monter la partition Linux
sudo mount /dev/sdXY /mnt

# Monter les systèmes virtuels
sudo mount --bind /dev /mnt/dev  
sudo mount --bind /proc /mnt/proc  
sudo mount --bind /sys /mnt/sys  

# Si UEFI, monter EFI
sudo mount /dev/sdXY /mnt/boot/efi

# Entrer dans chroot
sudo chroot /mnt

# Réparer GRUB
grub-install /dev/sdX  
update-grub  

# Sortir
exit

# Démonter tout
sudo umount /mnt/boot/efi  
sudo umount /mnt/dev  
sudo umount /mnt/proc  
sudo umount /mnt/sys  
sudo umount /mnt  
```

---

## Cas extrême : Réinstallation complète

Si toutes les méthodes échouent, la réinstallation de Linux Mint est une option.

### Réinstallation sans perte de données

**Important :** Vous pouvez réinstaller Linux Mint **en conservant votre /home** (vos fichiers personnels).

**Procédure :**

1. Démarrez sur la clé USB Live
2. Lancez l'installation
3. À l'étape du partitionnement :
   - Sélectionnez **"Autre chose"** (Something else)
   - **NE PAS** formater la partition /home
   - Réutilisez la partition / (racine) et formatez-la
   - Gardez la partition /home sans la formater
4. Installez normalement

**Résultat :** Système tout neuf, mais vos documents, photos, paramètres sont conservés.

**⚠️ Sauvegardez quand même avant !**

---

## Conclusion

La réparation de GRUB peut sembler intimidante, mais c'est un problème courant et bien documenté :

**Points clés à retenir :**

1. **GRUB cassé ≠ données perdues** → Vos fichiers sont intacts
2. **Boot-Repair** est l'outil le plus simple (Méthode 2)
3. **Une clé USB bootable** est indispensable
4. **Windows écrase GRUB** → Normal après réinstallation Windows
5. **Prévention** : Toujours avoir une clé USB de secours

**Méthodes par ordre de simplicité :**

1. `sudo update-grub` → Si Linux démarre
2. **Boot-Repair** → Solution automatique recommandée
3. **Réparation manuelle (chroot)** → Plus de contrôle
4. **grub rescue>** → Dépannage d'urgence
5. **Réinstallation** → Dernier recours

**N'ayez pas peur de réparer GRUB** : avec les bons outils et une approche méthodique, c'est un problème tout à fait gérable, même pour un débutant !

En cas de doute, n'hésitez pas à demander de l'aide sur les forums avec :
- Le rapport Boot-Repair (URL)
- La sortie de `lsblk` et `sudo efibootmgr`
- Une description précise du problème

---

## Ressources complémentaires

- [Boot-Repair - Documentation officielle](https://help.ubuntu.com/community/Boot-Repair)
- [Ubuntu Wiki - GRUB2](https://help.ubuntu.com/community/Grub2)
- [Forum Linux Mint - Boot Issues](https://forums.linuxmint.com/)
- [Super GRUB2 Disk](https://www.supergrubdisk.org/)

---


⏭️ [Problèmes de performance et ralentissements](/23-depannage-et-resolution-de-problemes/05-problemes-de-performance-et-ralentissements.md)
