🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 23.2 Problèmes de démarrage et écran noir

## Introduction

Les problèmes de démarrage sont parmi les plus stressants pour un utilisateur Linux, car ils peuvent donner l'impression que tout est perdu. Rassurez-vous : dans la majorité des cas, ces problèmes sont résolubles, et vos données sont intactes.

Ce guide vous accompagne pas à pas pour identifier et résoudre les différents types de problèmes de démarrage, de l'écran noir au blocage au logo, en passant par les erreurs de GRUB.

---

## Les différents types de problèmes de démarrage

Avant de chercher une solution, il faut d'abord identifier à quelle étape le démarrage échoue.

### 1. L'ordinateur ne s'allume pas du tout

**Symptômes :**
- Aucune LED ne s'allume
- Aucun bruit (ventilateur, disque dur)
- Écran totalement noir, pas de rétroéclairage

**Cause probable :** Problème matériel (alimentation, batterie)

**Ce n'est PAS un problème Linux** → Vérifiez l'alimentation, la batterie, les connexions.

---

### 2. Écran du BIOS/UEFI visible, mais pas de démarrage de Linux

**Symptômes :**
- L'écran du fabricant (Dell, HP, Lenovo, etc.) apparaît
- Puis message d'erreur type "No bootable device" ou "Operating System not found"
- Ou écran noir avec curseur clignotant

**Cause probable :** Problème de bootloader (GRUB) ou ordre de démarrage

---

### 3. Menu GRUB visible, mais Linux ne démarre pas

**Symptômes :**
- Le menu GRUB apparaît (liste des systèmes d'exploitation)
- Après sélection de Linux Mint, écran noir ou erreurs

**Cause probable :** Problème de kernel, de pilotes, ou de partition

---

### 4. Logo Linux Mint visible, puis écran noir

**Symptômes :**
- Le logo Linux Mint s'affiche avec la barre de progression
- Puis l'écran devient noir (avec ou sans curseur)
- Parfois le curseur clignote

**Cause probable :** Problème de pilotes graphiques, de résolution, ou de service système

---

### 5. Blocage à l'écran de connexion

**Symptômes :**
- L'écran de connexion s'affiche
- Mais impossible de se connecter (boucle de connexion)
- Ou écran figé

**Cause probable :** Problème de session, de configuration utilisateur, ou d'espace disque

---

## Solutions générales (à essayer en premier)

Avant d'aller plus loin, essayez ces solutions simples qui règlent souvent le problème.

### Solution 1 : Attendre et patienter

Parfois, le système prend simplement plus de temps que d'habitude :

- **Après une mise à jour**, le premier démarrage peut être long (5-10 minutes)
- **Sur un disque dur** (non SSD), le démarrage peut prendre du temps
- **Si des vérifications** de disque sont en cours

**Attendez au moins 5-10 minutes** avant de conclure à un blocage.

---

### Solution 2 : Redémarrage forcé

Si l'écran est vraiment figé :

1. **Maintenez le bouton d'alimentation** enfoncé pendant 5-10 secondes
2. L'ordinateur s'éteindra de force
3. Attendez 10 secondes
4. Rallumez normalement

**Note :** Ce n'est pas la méthode idéale, mais parfois nécessaire. Un redémarrage forcé occasionnel ne cause généralement pas de dommages.

---

### Solution 3 : Débrancher les périphériques externes

Certains périphériques peuvent causer des problèmes au démarrage :

- **Clés USB** (surtout si bootables)
- **Disques durs externes**
- **Cartes SD**
- **Lecteurs de cartes**
- **Autres périphériques USB** (imprimantes, webcams, etc.)

**Procédure :**
1. Éteignez l'ordinateur
2. Débranchez TOUS les périphériques externes (sauf clavier/souris)
3. Redémarrez
4. Si ça fonctionne, rebranchez les périphériques un par un pour identifier le coupable

---

## Accéder aux options de démarrage avancées

Si le problème persiste, vous devrez accéder au menu de récupération de GRUB.

### Comment accéder au menu GRUB ?

#### Si le menu GRUB apparaît automatiquement :
- Utilisez simplement les flèches du clavier
- Sélectionnez "Options avancées pour Linux Mint"

#### Si le menu GRUB ne s'affiche pas :

**Méthode 1 :** Maintenir la touche **Shift** (Maj) gauche appuyée dès l'allumage de l'ordinateur

**Méthode 2 :** Appuyer répétitivement sur **Échap** ou **Shift** au démarrage

**Méthode 3 :** Dans le BIOS/UEFI, désactiver temporairement le "Fast Boot" ou "Quick Boot"

Une fois le menu GRUB visible, vous verrez :
```
Ubuntu (ou Linux Mint)  
Options avancées pour Ubuntu  
Memory test (memtest86+)  
```

---

## Solution par type de problème

### Problème Type A : Écran noir après le logo (problème graphique)

C'est le problème le plus fréquent, souvent lié aux pilotes graphiques.

#### Solution A1 : Démarrer en mode graphique de base (nomodeset)

1. **Au menu GRUB**, sélectionnez la première entrée Linux Mint
2. **Appuyez sur 'e'** pour éditer
3. Vous voyez du texte qui commence par "linux /boot/vmlinuz..."
4. **Trouvez la ligne** qui commence par `linux` (utilisez les flèches)
5. **Allez à la fin de cette ligne** (après `quiet splash`)
6. **Ajoutez** (avec un espace avant) : `nomodeset`

La ligne ressemblera à :
```
linux /boot/vmlinuz-... root=UUID=... quiet splash nomodeset
```

7. **Appuyez sur F10** ou **Ctrl+X** pour démarrer avec cette configuration

**Si ça fonctionne**, Linux devrait démarrer en mode graphique de base.

**Que faire ensuite ?**

Une fois connecté, vous devrez installer ou réparer les pilotes graphiques :

**Pour NVIDIA :**
```bash
# Ouvrir le gestionnaire de pilotes
Menu → Administration → Gestionnaire de pilotes
```
- Sélectionnez le pilote recommandé
- Installez et redémarrez

**Pour AMD ou Intel :**
- Généralement, les pilotes open-source fonctionnent bien
- Assurez-vous que le système est à jour :
```bash
sudo apt update  
sudo apt upgrade  
```

---

#### Solution A2 : Désactiver temporairement les pilotes NVIDIA

Si vous avez une carte NVIDIA et que nomodeset ne suffit pas :

Au menu GRUB, éditez la ligne (touche 'e') et ajoutez :
```
nouveau.modeset=0
```

Ou pour bloquer complètement le pilote NVIDIA :
```
modprobe.blacklist=nvidia
```

---

#### Solution A3 : Forcer une résolution d'écran

Parfois le problème vient d'une mauvaise détection de résolution :

Éditez le GRUB (touche 'e') et ajoutez :
```
video=1920x1080
```

Remplacez `1920x1080` par la résolution native de votre écran.

---

### Problème Type B : Erreurs GRUB (grub rescue, error: no such partition)

#### Symptôme :
```
error: no such partition  
grub rescue>  
```

Cela signifie que GRUB ne trouve plus la partition où Linux est installé.

#### Cause probable :
- Partition supprimée ou modifiée
- UUID de partition changé
- Problème après redimensionnement de partition
- Installation/désinstallation de Windows

#### Solution B1 : Identifier les partitions

Au prompt `grub rescue>`, tapez :
```
ls
```

Vous verrez quelque chose comme :
```
(hd0) (hd0,gpt1) (hd0,gpt2) (hd0,gpt3)
```

Testez chaque partition pour trouver celle de Linux :
```
ls (hd0,gpt1)/  
ls (hd0,gpt2)/  
ls (hd0,gpt3)/  
```

Cherchez celle qui contient un dossier `/boot` ou `/boot/grub`.

#### Solution B2 : Charger temporairement Linux

Une fois la bonne partition trouvée (par exemple hd0,gpt2) :
```
set prefix=(hd0,gpt2)/boot/grub  
set root=(hd0,gpt2)  
insmod normal  
normal  
```

Cela devrait charger le menu GRUB normal.

#### Solution B3 : Réparer GRUB définitivement

Cette solution nécessite une clé USB bootable de Linux Mint (voir section dédiée à la réparation de GRUB dans le chapitre 23.4).

---

### Problème Type C : Boucle de connexion (écran de login qui revient)

#### Symptômes :
- L'écran de connexion s'affiche
- Vous entrez votre mot de passe
- L'écran devient noir quelques secondes
- Puis retour à l'écran de connexion

#### Causes probables :
- Espace disque insuffisant
- Problème de droits dans votre dossier personnel
- Fichier de configuration corrompu
- Conflit de session

#### Solution C1 : Vérifier l'espace disque

1. À l'écran de connexion, appuyez sur **Ctrl+Alt+F2**
2. Connectez-vous en mode texte (login + mot de passe)
3. Vérifiez l'espace disque :
```bash
df -h
```

Si la partition `/` (racine) ou `/home` est à 100%, c'est le problème.

**Libérer de l'espace :**
```bash
# Nettoyer le cache des paquets
sudo apt clean

# Supprimer les anciens kernels
sudo apt autoremove

# Vérifier à nouveau
df -h
```

4. Redémarrez :
```bash
sudo reboot
```

---

#### Solution C2 : Vérifier les droits du dossier personnel

En mode terminal (Ctrl+Alt+F2) :

```bash
# Vérifier le propriétaire de votre dossier
ls -ld /home/votre-nom-utilisateur

# Devrait afficher : votre-nom votre-nom
# Si ce n'est pas le cas, corrigez :
sudo chown -R votre-nom:votre-nom /home/votre-nom-utilisateur

# Vérifier les permissions
sudo chmod 755 /home/votre-nom-utilisateur

# Redémarrer
sudo reboot
```

---

#### Solution C3 : Renommer les fichiers de configuration

Parfois, un fichier de configuration corrompu empêche la connexion :

```bash
# En mode terminal (Ctrl+Alt+F2)
cd ~

# Renommer (sauvegarder) les fichiers de configuration
mv .Xauthority .Xauthority.backup  
mv .ICEauthority .ICEauthority.backup  

# Si vous utilisez Cinnamon
mv .cinnamon .cinnamon.backup

# Redémarrer
sudo reboot
```

Cela forcera la recréation de fichiers de configuration propres.

---

#### Solution C4 : Utiliser une session différente

À l'écran de connexion :

1. **Avant** d'entrer votre mot de passe
2. Cliquez sur l'**icône de session** (souvent un engrenage ou un logo)
3. Sélectionnez une **session différente** :
   - Si vous étiez en Cinnamon, essayez "Cinnamon (Software Rendering)"
   - Ou essayez "MATE" ou "Xfce" si installés
4. Connectez-vous

Si ça fonctionne, le problème vient de votre session habituelle.

---

### Problème Type D : Blocage complet au démarrage

#### Symptômes :
- Le système se bloque complètement
- Aucune réaction au clavier
- Impossible d'accéder au terminal (Ctrl+Alt+F2 ne fonctionne pas)

#### Solution D1 : Démarrer en mode recovery (récupération)

1. Au **menu GRUB**, sélectionnez "Options avancées pour Linux Mint"
2. Choisissez la ligne avec **(recovery mode)**
3. Vous arrivez au menu de récupération

Options disponibles :
- **resume** : Reprendre le démarrage normal
- **clean** : Libérer de l'espace disque
- **dpkg** : Réparer les paquets cassés
- **fsck** : Vérifier et réparer le système de fichiers
- **grub** : Réinstaller GRUB
- **network** : Activer le réseau
- **root** : Accéder au shell root
- **system-summary** : Résumé du système

**Pour commencer**, essayez dans cet ordre :

1. **fsck** : Pour vérifier le disque
2. **dpkg** : Pour réparer les paquets
3. **resume** : Pour essayer de démarrer normalement

---

#### Solution D2 : Accéder au shell root en mode recovery

Si les options automatiques ne fonctionnent pas :

1. Au menu de récupération, choisissez **root**
2. Vous arrivez à un terminal avec les droits root
3. Le système de fichiers est en lecture seule, remontez-le en écriture :

```bash
mount -o remount,rw /
```

Vous pouvez maintenant :

**Mettre à jour le système :**
```bash
apt update  
apt upgrade  
```

**Réparer les paquets cassés :**
```bash
dpkg --configure -a  
apt --fix-broken install  
```

**Vérifier l'espace disque :**
```bash
df -h  
apt clean  
apt autoremove  
```

**Recréer le fichier initramfs (image de démarrage) :**
```bash
update-initramfs -u -k all
```

**Redémarrer :**
```bash
reboot
```

---

### Problème Type E : Messages d'erreur spécifiques au démarrage

#### "Gave up waiting for root device"

**Cause :** Le système ne trouve pas la partition racine

**Solution :**
1. Démarrez en mode recovery
2. Accédez au shell root
3. Éditez `/etc/fstab` :
```bash
nano /etc/fstab
```
4. Vérifiez que les UUID correspondent :
```bash
blkid
```
5. Corrigez si nécessaire

---

#### "Failed to start Light Display Manager" (ou GDM, SDDM)

**Cause :** Le gestionnaire d'affichage (écran de connexion) ne démarre pas

**Solution rapide :**
```bash
# En mode recovery, shell root
systemctl status lightdm  # Voir l'erreur  
systemctl restart lightdm  # Essayer de redémarrer  

# Si ça ne fonctionne pas, réinstaller
apt install --reinstall lightdm
```

---

#### "Failed to mount /home" ou autres partitions

**Cause :** Problème de montage de partition

**Solution :**
1. Vérifiez `/etc/fstab` :
```bash
cat /etc/fstab
```
2. Commentez temporairement la ligne problématique (ajoutez # au début)
3. Redémarrez
4. Une fois démarré, corrigez le problème de partition

---

## Outils de diagnostic en mode texte

Lorsque vous êtes en mode terminal (Ctrl+Alt+F2) ou en recovery, voici des commandes utiles :

### Vérifier l'état du système

```bash
# Voir les services qui ont échoué
systemctl --failed

# Voir les logs récents
journalctl -xb | tail -100

# Voir spécifiquement les erreurs
journalctl -p err -xb

# Voir les logs du dernier démarrage
journalctl -b -1
```

### Vérifier le matériel

```bash
# Informations système
inxi -Fxz

# Vérifier la carte graphique détectée
lspci | grep VGA

# Vérifier les modules chargés
lsmod

# Tester le disque dur
sudo smartctl -H /dev/sda  # Remplacer sda par votre disque
```

### Vérifier les partitions

```bash
# Lister toutes les partitions
lsblk

# Voir les UUID
blkid

# Vérifier le montage
mount | grep sda
```

---

## Créer une clé USB de secours

Il est **fortement recommandé** de créer une clé USB bootable de Linux Mint pour les situations de récupération.

### Pourquoi ?

- Accès à votre système même si Linux ne démarre pas
- Sauvegarde de vos données
- Réparation du bootloader GRUB
- Réinstallation si nécessaire (sans perdre les données)

### Comment créer une clé USB de secours ?

**Depuis un autre ordinateur (Windows ou Linux) :**

1. **Téléchargez** l'ISO de Linux Mint depuis le site officiel
2. **Téléchargez** un outil de création de clé USB :
   - **Balena Etcher** (recommandé, très simple) : https://www.balena.io/etcher/
   - **Rufus** (Windows uniquement) : https://rufus.ie/
   - **Ventoy** (plus avancé, permet plusieurs ISO) : https://www.ventoy.net/

3. **Créez** la clé USB bootable avec l'outil choisi

**Depuis votre système Linux Mint fonctionnel (préventivement) :**

```bash
# Installer mintstick
sudo apt install mintstick

# Lancer l'outil graphique
Menu → Accessoires → Graveur de clé USB
```

---

## Utiliser la clé USB de secours

### Démarrer sur la clé USB

1. **Insérez** la clé USB
2. **Redémarrez** l'ordinateur
3. **Appuyez** sur la touche de menu de démarrage :
   - **F12** (le plus courant)
   - **F9**, **F10**, **F11** (selon le fabricant)
   - **Échap** sur certains ordinateurs
   - Consultez le manuel de votre ordinateur si besoin

4. **Sélectionnez** la clé USB dans le menu
5. **Choisissez** "Start Linux Mint" ou mode Live

### Que faire une fois démarré en Live ?

#### Option 1 : Sauvegarder vos données

Si vous craignez de perdre vos données :

1. **Ouvrez** le gestionnaire de fichiers
2. **Accédez** à votre disque dur (visible dans la barre latérale)
3. **Copiez** vos fichiers importants vers un disque externe ou une autre clé USB

#### Option 2 : Réparer le système

Depuis le mode Live, vous pouvez :
- Réparer GRUB (voir chapitre 23.4)
- Vérifier et réparer les partitions avec GParted
- Accéder aux fichiers de configuration
- Réinstaller des paquets via chroot

#### Option 3 : Réinstaller Linux Mint

**En dernier recours**, si rien ne fonctionne :

L'icône "Install Linux Mint" est sur le bureau. La réinstallation peut se faire **en conservant votre partition /home** et donc vos données personnelles.

**⚠️ Attention :** Sauvegardez vos données AVANT de réinstaller !

---

## Prévention des problèmes de démarrage

### Bonnes pratiques

1. **Créez des sauvegardes régulières avec Timeshift**
   - Configurez des snapshots automatiques
   - Avant toute mise à jour majeure, créez un snapshot manuel

2. **Ne forcez pas l'extinction** pendant une mise à jour
   - Si le système semble bloqué pendant une mise à jour, patientez
   - Les mises à jour de kernel peuvent prendre du temps

3. **Gardez toujours une clé USB de secours**
   - À jour avec la dernière version de Linux Mint
   - Testez-la régulièrement

4. **Vérifiez l'espace disque régulièrement**
   - Gardez au moins 10-15% d'espace libre
   - Nettoyez régulièrement : `sudo apt clean && sudo apt autoremove`

5. **Lisez les notes de mise à jour**
   - Particulièrement pour les mises à jour de kernel
   - Ou les changements de pilotes graphiques

6. **Ne modifiez pas les fichiers système** sans comprendre
   - Surtout `/etc/fstab`, `/boot/grub/`, `/etc/X11/`
   - Faites toujours une sauvegarde avant

---

## Tableau récapitulatif des touches utiles

| Situation | Touche(s) | Action |
|-----------|-----------|--------|
| Au démarrage | **Shift** ou **Échap** | Afficher le menu GRUB |
| Menu GRUB | **e** | Éditer l'entrée de démarrage |
| Menu GRUB | **c** | Ouvrir la console GRUB |
| Édition GRUB | **F10** ou **Ctrl+X** | Démarrer avec les modifications |
| Pendant le démarrage | **Ctrl+Alt+F2** | Accéder au terminal texte |
| Mode texte | **Ctrl+Alt+F7** | Retourner à l'interface graphique |
| Au démarrage PC | **F12** (variable) | Menu de boot (choix périphérique) |
| Au démarrage PC | **F2** / **Del** (variable) | Accéder au BIOS/UEFI |

---

## Quand demander de l'aide ?

N'hésitez pas à demander de l'aide sur les forums si :

- Vous avez essayé les solutions de base sans succès
- Vous voyez des messages d'erreur que vous ne comprenez pas
- Vous n'êtes pas à l'aise avec le mode terminal
- Le problème persiste après plusieurs tentatives

**Préparez votre demande d'aide avec :**

1. **Description précise du problème**
   - À quelle étape le démarrage échoue
   - Messages d'erreur exacts (photo ou texte)

2. **Votre configuration**
   ```bash
   # Si vous pouvez démarrer en mode recovery/live
   inxi -Fxz
   ```

3. **Ce que vous avez déjà essayé**

4. **Contexte**
   - Quand le problème est apparu
   - Dernières modifications faites

---

## Conclusion

Les problèmes de démarrage peuvent sembler intimidants, mais ils sont généralement résolubles :

- **Commencez par les solutions simples** : redémarrage, périphériques débranchés, attente
- **Utilisez le mode nomodeset** pour la majorité des écrans noirs
- **Le mode recovery** est votre ami pour réparer le système
- **Une clé USB de secours** est indispensable
- **Timeshift** peut sauver votre système en quelques clics

La clé est de **rester calme**, de **procéder méthodiquement**, et de ne pas hésiter à demander de l'aide avec des informations précises.

**Rappelez-vous :** Même si le système ne démarre plus, **vos données sont presque toujours intactes** et récupérables via une clé USB Live !

---

## Ressources complémentaires

- [Documentation Linux Mint - Boot Issues](https://forums.linuxmint.com/viewtopic.php?t=122561)
- [Ubuntu Wiki - Boot Repair](https://help.ubuntu.com/community/Boot-Repair)
- [Forum francophone Linux Mint](https://forum-francophone-linuxmint.fr/)

---


⏭️ [Mode recovery (recovery mode)](/23-depannage-et-resolution-de-problemes/03-mode-recovery.md)
