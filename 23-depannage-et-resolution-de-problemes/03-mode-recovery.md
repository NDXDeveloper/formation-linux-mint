🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 23.3 Mode recovery (mode récupération)

## Introduction

Le mode recovery (mode récupération) est un environnement de démarrage spécial de Linux Mint qui vous permet de réparer votre système lorsqu'il ne démarre plus normalement. C'est un outil puissant et rassurant : même si Linux refuse de démarrer, vous avez toujours accès à des outils de réparation.

Ce mode charge un système minimal avec uniquement les services essentiels, ce qui permet de diagnostiquer et résoudre de nombreux problèmes sans avoir besoin d'une clé USB bootable.

**Rassurez-vous :** Le mode recovery est sûr à utiliser et ne supprimera pas vos données. C'est l'équivalent du "Mode sans échec" de Windows, mais en plus puissant.

---

## Qu'est-ce que le mode recovery ?

### Définition simple

Le mode recovery est un **mode de démarrage minimal** qui :

- Charge uniquement les composants essentiels du système
- N'utilise pas l'interface graphique (vous êtes en mode texte)
- Donne accès à des outils de réparation
- Permet de travailler avec les droits administrateur (root)
- Fonctionne même quand le système normal ne démarre pas

### Quand utiliser le mode recovery ?

Vous devriez utiliser le mode recovery lorsque :

- **Linux ne démarre plus** (écran noir, blocage)
- **Impossible de se connecter** (boucle de connexion)
- **Le système est très lent** ou instable
- **Après une mise à jour problématique**
- **Pour réparer des paquets cassés**
- **Pour vérifier et réparer le système de fichiers**
- **Pour réinitialiser un mot de passe oublié**
- **Pour libérer de l'espace disque** quand la partition est pleine

### Quand NE PAS utiliser le mode recovery ?

Le mode recovery ne pourra pas vous aider si :

- Le disque dur est physiquement endommagé
- Le GRUB est complètement cassé (vous ne voyez même pas le menu GRUB)
- Le problème est matériel (carte graphique HS, RAM défectueuse)

Dans ces cas, vous aurez besoin d'une clé USB bootable ou d'une réparation matérielle.

---

## Comment accéder au mode recovery

### Méthode standard

1. **Démarrez ou redémarrez** votre ordinateur

2. **Affichez le menu GRUB** :
   - Maintenez la touche **Shift** (Maj) gauche enfoncée dès l'allumage
   - Ou appuyez plusieurs fois sur **Échap**
   - Le menu GRUB devrait apparaître

3. **Naviguez dans le menu** avec les flèches du clavier :
   - Sélectionnez **"Options avancées pour Linux Mint"** (ou "Advanced options for Ubuntu")
   - Appuyez sur **Entrée**

4. **Choisissez le mode recovery** :
   - Vous verrez plusieurs lignes avec différentes versions du kernel
   - Sélectionnez celle qui contient **(recovery mode)**
   - Généralement, c'est la deuxième ligne
   - Appuyez sur **Entrée**

### Si le menu GRUB n'apparaît pas

**Cas 1 : GRUB est masqué**

Éditez le fichier de configuration GRUB (depuis un démarrage réussi ou une clé USB Live) :

```bash
sudo nano /etc/default/grub
```

Cherchez la ligne :
```
GRUB_TIMEOUT_STYLE=hidden
```

Modifiez-la en :
```
GRUB_TIMEOUT_STYLE=menu  
GRUB_TIMEOUT=10  
```

Mettez à jour GRUB :
```bash
sudo update-grub
```

**Cas 2 : Démarrage UEFI trop rapide**

Certains ordinateurs récents démarrent si vite que vous n'avez pas le temps d'appuyer sur les touches.

Solution :
1. Entrez dans le **BIOS/UEFI** (touche F2, Del, ou F10 au démarrage)
2. Désactivez **Fast Boot** ou **Quick Boot**
3. Sauvegardez et redémarrez

---

## Le menu de recovery

Une fois le mode recovery lancé, vous verrez un écran texte avec le menu "Recovery Menu" :

```
Recovery Menu

  resume    Resume normal boot
  clean     Try to make free space
  dpkg      Repair broken packages
  fsck      File system check
  grub      Update grub bootloader
  network   Enable networking
  root      Drop to root shell prompt
  system-summary  System summary
```

Explorons chaque option en détail.

---

## Les options du menu recovery

### Option 1 : resume - Reprendre le démarrage normal

**Ce que ça fait :**
- Tente de continuer le démarrage normalement
- Utile si le problème était temporaire

**Quand l'utiliser :**
- Après avoir utilisé une autre option de réparation
- Pour tester si le problème est résolu
- Comme première tentative avant les autres options

**Comment l'utiliser :**
1. Sélectionnez **resume**
2. Appuyez sur **Entrée**
3. Le système essaie de démarrer normalement

**Résultat attendu :**
- Si la réparation a fonctionné : vous arrivez à l'écran de connexion
- Sinon : vous revenez au menu recovery ou voyez un écran noir

---

### Option 2 : clean - Libérer de l'espace disque

**Ce que ça fait :**
- Supprime les fichiers temporaires
- Nettoie le cache des paquets
- Supprime les anciens kernels inutiles
- Libère de l'espace sur votre disque

**Quand l'utiliser :**
- Si vous avez un message "No space left on device"
- Si la partition racine (/) est pleine
- Avant de faire des mises à jour
- Comme maintenance régulière

**Comment l'utiliser :**
1. Sélectionnez **clean**
2. Appuyez sur **Entrée**
3. Le système analyse et nettoie automatiquement
4. Un message vous indique combien d'espace a été libéré

**Ce qui est supprimé :**
- Cache APT (`/var/cache/apt/archives/`)
- Anciens kernels (sauf les 2 derniers)
- Fichiers temporaires
- Logs anciens (parfois)

**Ce qui N'est PAS supprimé :**
- Vos documents personnels
- Vos photos, vidéos, musique
- Vos programmes installés
- Vos paramètres

---

### Option 3 : dpkg - Réparer les paquets cassés

**Ce que ça fait :**
- Répare les installations de logiciels interrompues
- Résout les dépendances cassées
- Termine les configurations en attente
- Nettoie la base de données des paquets

**Quand l'utiliser :**
- Après une installation ou mise à jour interrompue
- Si vous voyez des erreurs "dpkg was interrupted"
- Si le gestionnaire de logiciels ne fonctionne plus
- Si vous avez des messages "broken packages"

**Comment l'utiliser :**
1. Sélectionnez **dpkg**
2. Appuyez sur **Entrée**
3. Le système exécute automatiquement :
   - `dpkg --configure -a`
   - `apt-get install -f`
4. Attendez que le processus se termine

**Résultat attendu :**
- Message de confirmation
- La base de données des paquets est réparée
- Vous pouvez ensuite reprendre le démarrage (option resume)

**Note :** Cette opération peut prendre plusieurs minutes, soyez patient.

---

### Option 4 : fsck - Vérification du système de fichiers

**Ce que ça fait :**
- Vérifie l'intégrité de votre disque dur
- Répare les erreurs du système de fichiers
- Corrige les secteurs défectueux (si possible)
- Récupère les fichiers orphelins

**Quand l'utiliser :**
- Après une extinction forcée (coupure de courant, batterie vide)
- Si vous voyez des messages "filesystem errors"
- Si des fichiers disparaissent ou sont corrompus
- Si le système parle de "Read-only file system"
- En maintenance préventive (tous les 6 mois)

**Comment l'utiliser :**
1. Sélectionnez **fsck**
2. Appuyez sur **Entrée**
3. Confirmez en tapant **Y** (Yes) si demandé
4. Le système vérifie toutes les partitions

**Important :**
- Le disque doit être démonté (c'est fait automatiquement en recovery)
- Des questions peuvent vous être posées : répondez **Y** (Yes) dans le doute
- Le processus peut être long sur de gros disques

**Questions typiques :**
```
/dev/sda1: UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY
Fix? yes
```
Répondez toujours **yes** sauf si vous savez exactement ce que vous faites.

**Résultat attendu :**
- Message : "File system check complete"
- Indication du nombre d'erreurs corrigées
- Si aucune erreur : "File system is clean"

---

### Option 5 : grub - Mettre à jour GRUB

**Ce que ça fait :**
- Réinstalle le bootloader GRUB
- Met à jour la configuration de GRUB
- Détecte tous les systèmes d'exploitation installés
- Reconstruit le menu de démarrage

**Quand l'utiliser :**
- Si le menu GRUB ne montre pas Windows en dual-boot
- Après installation/désinstallation d'un OS
- Si GRUB affiche des erreurs au démarrage
- Après un changement de partition

**Comment l'utiliser :**
1. Sélectionnez **grub**
2. Appuyez sur **Entrée**
3. Le système exécute `update-grub`
4. Attendez la confirmation

**Résultat attendu :**
- Liste des systèmes d'exploitation détectés
- Message de confirmation
- Au prochain démarrage, menu GRUB à jour

**Note :** Cela ne répare pas un GRUB complètement cassé (voir chapitre 23.4 pour une réparation complète).

---

### Option 6 : network - Activer le réseau

**Ce que ça fait :**
- Active la connexion réseau en mode recovery
- Configure automatiquement la carte réseau (Ethernet de préférence)
- Permet de télécharger des paquets pour les réparations

**Quand l'utiliser :**
- Avant d'utiliser l'option **root** si vous devez télécharger des paquets
- Pour accéder au système à distance (SSH)
- Pour des réparations nécessitant Internet

**Comment l'utiliser :**
1. Sélectionnez **network**
2. Appuyez sur **Entrée**
3. Le système configure le réseau automatiquement
4. Un message confirme l'activation

**Important :**
- Privilégiez une **connexion Ethernet** (câble), le WiFi peut ne pas fonctionner
- Une fois activé, vous pouvez utiliser d'autres options nécessitant Internet

**Après activation :**
- Vous pouvez accéder au shell root et utiliser `apt`, `wget`, etc.
- Vous pouvez télécharger des mises à jour
- Vous pouvez accéder au système via SSH depuis un autre ordinateur

---

### Option 7 : root - Shell root (terminal administrateur)

**Ce que ça fait :**
- Ouvre un terminal avec tous les droits (root)
- Vous donne un contrôle total sur le système
- Permet d'exécuter n'importe quelle commande de réparation

**Quand l'utiliser :**
- Pour des réparations avancées non couvertes par les autres options
- Pour éditer des fichiers de configuration
- Pour réinitialiser un mot de passe utilisateur
- Pour effectuer des réparations manuelles

**Comment l'utiliser :**
1. Sélectionnez **root**
2. Appuyez sur **Entrée**
3. Vous voyez un prompt `root@ordinateur:~#`
4. Tapez vos commandes

**⚠️ Attention :**
- Vous avez **tous les droits** : une mauvaise commande peut casser le système
- Pas de confirmation "Êtes-vous sûr ?" : la commande s'exécute immédiatement
- Pas de `sudo` nécessaire (vous êtes déjà root)

**Première chose à faire :** Remonter le système en lecture-écriture

Par défaut, le système est monté en lecture seule. Pour faire des modifications :

```bash
mount -o remount,rw /
```

Maintenant vous pouvez modifier des fichiers.

---

### Option 8 : system-summary - Résumé du système

**Ce que ça fait :**
- Affiche un résumé des informations système
- Montre l'état du disque, de la mémoire, des partitions
- Donne des détails sur le matériel

**Quand l'utiliser :**
- Pour diagnostiquer rapidement un problème
- Pour vérifier l'espace disque disponible
- Pour confirmer la détection du matériel

**Comment l'utiliser :**
1. Sélectionnez **system-summary**
2. Appuyez sur **Entrée**
3. Lisez les informations affichées
4. Appuyez sur **Entrée** pour revenir au menu

**Informations affichées :**
- Modèle du processeur
- Quantité de RAM
- Liste des partitions et espace disque
- Carte graphique détectée
- Version du kernel

---

## Scénarios d'utilisation pratiques

### Scénario 1 : Partition racine pleine (0% d'espace libre)

**Symptômes :**
- Impossible de se connecter
- Message "No space left on device"
- Système très lent

**Solution :**
1. Démarrez en **mode recovery**
2. Sélectionnez **clean** → Entrée
3. Attendez le nettoyage
4. Sélectionnez **resume** → Entrée
5. Le système devrait démarrer normalement

**Si ça ne suffit pas :**
1. Retournez en recovery
2. Sélectionnez **root** → Entrée
3. Montez en écriture : `mount -o remount,rw /`
4. Vérifiez l'espace : `df -h`
5. Trouvez les gros fichiers : `du -sh /var/* | sort -h`
6. Nettoyez manuellement :
```bash
apt clean  
apt autoremove  
journalctl --vacuum-time=7d  # Garde 7 jours de logs  
```
7. Redémarrez : `reboot`

---

### Scénario 2 : Mise à jour interrompue

**Symptômes :**
- Message "dpkg was interrupted"
- Le gestionnaire de logiciels ne fonctionne plus
- Erreurs lors des installations

**Solution :**
1. Démarrez en **mode recovery**
2. Sélectionnez **dpkg** → Entrée
3. Attendez que la réparation se termine
4. Sélectionnez **resume** → Entrée

**Si ça ne suffit pas :**
1. Retournez en recovery
2. Activez le réseau : **network** → Entrée
3. Accédez au shell : **root** → Entrée
4. Montez en écriture : `mount -o remount,rw /`
5. Réparez manuellement :
```bash
dpkg --configure -a  
apt update  
apt --fix-broken install  
apt upgrade  
```
6. Redémarrez : `reboot`

---

### Scénario 3 : Mot de passe oublié

**Symptômes :**
- Impossible de se connecter (mot de passe oublié)
- Aucun autre compte administrateur disponible

**Solution :**
1. Démarrez en **mode recovery**
2. Sélectionnez **root** → Entrée
3. Montez en écriture : `mount -o remount,rw /`
4. Changez le mot de passe :
```bash
passwd nom-utilisateur
```
5. Tapez le **nouveau mot de passe** (2 fois)
6. **Notez-le** quelque part !
7. Redémarrez : `reboot`
8. Connectez-vous avec le nouveau mot de passe

**Note :** Remplacez `nom-utilisateur` par votre vrai nom d'utilisateur.

---

### Scénario 4 : Système de fichiers en lecture seule

**Symptômes :**
- Message "Read-only file system"
- Impossible de créer ou modifier des fichiers
- Souvent après une extinction forcée

**Solution :**
1. Démarrez en **mode recovery**
2. Sélectionnez **fsck** → Entrée
3. Répondez **Y** (yes) à toutes les questions
4. Attendez la vérification complète
5. Sélectionnez **resume** → Entrée

**Vérification après réparation :**
```bash
# Une fois démarré normalement
touch /tmp/test  # Devrait créer un fichier sans erreur  
rm /tmp/test  
```

---

### Scénario 5 : Pilote graphique cassé (écran noir)

**Symptômes :**
- Écran noir après mise à jour du pilote
- Logo Linux Mint visible, puis noir

**Solution :**
1. Démarrez en **mode recovery**
2. Sélectionnez **network** → Entrée (pour télécharger des pilotes)
3. Sélectionnez **root** → Entrée
4. Montez en écriture : `mount -o remount,rw /`
5. Supprimez le pilote problématique :

**Pour NVIDIA :**
```bash
apt remove --purge nvidia-*  
apt install xserver-xorg-video-nouveau  
```

**Pour AMD :**
```bash
apt install --reinstall xserver-xorg-video-amdgpu
```

6. Redémarrez : `reboot`
7. Une fois démarré, réinstallez le bon pilote via le Gestionnaire de pilotes

---

### Scénario 6 : Fichier de configuration corrompu

**Symptômes :**
- Un service ne démarre plus
- Erreurs au démarrage liées à un fichier spécifique

**Solution :**
1. Démarrez en **mode recovery**
2. Sélectionnez **root** → Entrée
3. Montez en écriture : `mount -o remount,rw /`
4. Éditez ou renommez le fichier problématique :

```bash
# Exemple : fichier fstab corrompu
nano /etc/fstab

# Ou renommez-le temporairement
mv /etc/fstab /etc/fstab.backup
```

5. Redémarrez : `reboot`

---

## Commandes utiles en mode root (shell recovery)

### Gestion du système de fichiers

```bash
# Remonter en lecture-écriture (TOUJOURS faire en premier)
mount -o remount,rw /

# Vérifier l'espace disque
df -h

# Vérifier les partitions montées
mount | grep sda

# Vérifier le système de fichiers manuellement
fsck -y /dev/sda1  # Remplacer sda1 par votre partition

# Analyser l'espace disque
du -sh /* | sort -h
```

### Gestion des paquets

```bash
# Réparer les paquets cassés
dpkg --configure -a  
apt --fix-broken install  

# Mettre à jour
apt update  
apt upgrade  

# Nettoyer
apt clean  
apt autoremove  

# Réinstaller un paquet
apt install --reinstall nom-du-paquet
```

### Gestion des utilisateurs

```bash
# Changer un mot de passe
passwd nom-utilisateur

# Lister les utilisateurs
cat /etc/passwd | grep /home

# Ajouter un utilisateur au groupe sudo
usermod -aG sudo nom-utilisateur
```

### Gestion des services

```bash
# Lister les services qui ont échoué
systemctl --failed

# État d'un service
systemctl status nom-service

# Redémarrer un service
systemctl restart nom-service

# Désactiver un service problématique
systemctl disable nom-service
```

### Diagnostics

```bash
# Voir les logs système
journalctl -xe

# Voir les logs du dernier démarrage
journalctl -b

# Voir uniquement les erreurs
journalctl -p err

# Informations système
inxi -Fxz

# Tester le réseau
ping -c 4 8.8.8.8
```

### Fichiers de configuration importants

```bash
# Éditer le fichier fstab (montage des partitions)
nano /etc/fstab

# Éditer la configuration réseau
nano /etc/network/interfaces

# Éditer la configuration GRUB
nano /etc/default/grub
# Puis mettre à jour :
update-grub

# Voir les kernels installés
ls /boot/vmlinuz-*
```

---

## Sortir du mode recovery

### Méthode 1 : Depuis le menu recovery

Sélectionnez **resume** et appuyez sur Entrée.

### Méthode 2 : Depuis le shell root

```bash
# Redémarrage
reboot

# Ou extinction
poweroff

# Ou retour au menu recovery (Ctrl+D)
exit
```

### Méthode 3 : Forcé (dernier recours)

Si le système est bloqué :
- Maintenez le bouton d'alimentation enfoncé 5-10 secondes
- L'ordinateur s'éteindra
- Rallumez normalement

---

## Précautions et bonnes pratiques

### Avant d'utiliser le mode recovery

1. **Sauvegardez vos données** si possible (depuis une clé USB Live)
2. **Notez les commandes** que vous prévoyez d'exécuter
3. **Lisez la documentation** pour comprendre ce que vous faites
4. **Ayez une clé USB de secours** prête au cas où

### Pendant l'utilisation

1. **Lisez les messages** affichés à l'écran
2. **Ne paniquez pas** si ça prend du temps (fsck peut être long)
3. **Notez les erreurs** exactes pour chercher de l'aide ensuite
4. **Ne forcez pas l'extinction** pendant une opération

### Après utilisation

1. **Vérifiez que tout fonctionne** normalement
2. **Créez un snapshot Timeshift** une fois le système réparé
3. **Documentez la solution** pour vous en souvenir
4. **Mettez à jour le système** si ce n'était pas fait

---

## Limitations du mode recovery

Le mode recovery ne peut PAS :

- **Réparer un disque dur physiquement endommagé**
  → Vous verrez des erreurs I/O persistantes même après fsck

- **Récupérer des données effacées**
  → Utilisez des outils spécialisés comme TestDisk

- **Réparer un GRUB complètement cassé**
  → Vous aurez besoin d'une clé USB bootable (voir chapitre 23.4)

- **Résoudre les problèmes matériels**
  → RAM défectueuse, carte graphique HS, etc.

- **Détecter du matériel non reconnu**
  → Le mode recovery utilise les mêmes pilotes que le système normal

---

## Comparaison : Mode Recovery vs Clé USB Live

| Critère | Mode Recovery | Clé USB Live |
|---------|---------------|--------------|
| **Disponibilité** | Toujours disponible | Nécessite préparation |
| **Vitesse d'accès** | Immédiat | Redémarrage + boot USB |
| **Accès aux données** | Direct | Nécessite montage |
| **Réseau** | WiFi difficile | WiFi plus facile |
| **Outils** | Limités (terminal) | Interface complète |
| **Réparation GRUB** | Partiel | Complet |
| **Sauvegarde données** | Difficile | Facile |
| **Usage** | Réparations système | Tout type de réparation |

**Recommandation :** Essayez toujours le mode recovery en premier. Si ça ne suffit pas, utilisez une clé USB Live.

---

## FAQ - Questions fréquentes

### Le mode recovery démarre, mais je ne vois que du texte, c'est normal ?

**Oui, c'est tout à fait normal !** Le mode recovery fonctionne en mode texte (pas d'interface graphique) pour économiser les ressources et éviter les problèmes de pilotes graphiques.

### J'ai peur de casser quelque chose en mode recovery

Le mode recovery est **sûr** si vous utilisez les options du menu (clean, dpkg, fsck, etc.). Ces options sont conçues pour réparer, pas pour détruire.

**Risque** uniquement si vous utilisez l'option **root** et tapez des commandes que vous ne comprenez pas.

### Combien de temps doit durer le fsck ?

Cela dépend de la taille de votre disque et du nombre d'erreurs :
- **Petit disque (< 100 Go)** : 5-15 minutes
- **Gros disque (500 Go - 1 To)** : 30-60 minutes
- **Très gros disque (> 1 To)** : 1-2 heures

Soyez patient ! Le processus est normal même s'il semble long.

### Puis-je utiliser le mode recovery régulièrement ?

**Oui !** Vous pouvez utiliser le mode recovery :
- Une fois par mois avec **clean** pour nettoyer le système
- Tous les 3-6 mois avec **fsck** pour vérifier le disque
- Avant une mise à jour majeure avec **dpkg** pour s'assurer que tout est OK

C'est même recommandé pour la maintenance préventive.

### J'ai sélectionné "root" par erreur, comment sortir ?

Tapez simplement :
```bash
exit
```
Vous reviendrez au menu recovery.

### Le mode recovery ne démarre pas, écran noir

Si même le mode recovery ne démarre pas, c'est un problème plus grave :
1. Essayez un **autre kernel** dans le menu GRUB
2. Utilisez une **clé USB bootable** Linux Mint
3. Vérifiez le **matériel** (RAM, disque dur)

---

## Alternative graphique : systemd-boot (pour utilisateurs avancés)

Depuis les versions récentes, il existe aussi une **interface graphique de recovery** accessible via :

1. Au menu GRUB, éditez l'entrée (touche **e**)
2. Trouvez la ligne avec `quiet splash`
3. Remplacez par `systemd.unit=rescue.target`
4. Démarrez (F10)

Cela vous donne un shell avec quelques outils graphiques basiques.

**Note :** Plus complexe, privilégiez le mode recovery classique.

---

## Résumé des options recovery

| Option | Action | Durée | Risque | Usage |
|--------|--------|-------|--------|-------|
| **resume** | Reprendre démarrage | Instantané | Aucun | Toujours tester après réparation |
| **clean** | Libérer espace | 1-5 min | Aucun | Disque plein, maintenance |
| **dpkg** | Réparer paquets | 2-10 min | Aucun | Après mise à jour ratée |
| **fsck** | Vérifier disque | 5-60 min | Faible | Après extinction forcée |
| **grub** | Mettre à jour GRUB | 1 min | Faible | Menu GRUB incomplet |
| **network** | Activer réseau | 1 min | Aucun | Avant téléchargements |
| **root** | Shell administrateur | - | Moyen | Réparations avancées |
| **system-summary** | Infos système | Instantané | Aucun | Diagnostic |

---

## Conclusion

Le mode recovery est un outil **puissant** et **rassurant** pour tout utilisateur Linux Mint :

- **Accessible** même quand le système ne démarre pas
- **Sûr** avec les options du menu automatiques
- **Efficace** pour résoudre la plupart des problèmes
- **Gratuit** et intégré (pas besoin de clé USB)

**Points à retenir :**

1. Le mode recovery est votre **première ligne de défense** en cas de problème
2. Les options **clean**, **dpkg**, et **fsck** règlent 80% des problèmes
3. L'option **root** donne un contrôle total mais nécessite de la prudence
4. Toujours **remonter en écriture** (`mount -o remount,rw /`) avant toute modification
5. Le mode recovery **ne supprime pas vos données**

N'hésitez pas à utiliser le mode recovery : c'est fait pour ça, et c'est un outil sûr qui peut vous sauver de nombreuses situations difficiles !

---

## Ressources complémentaires

- [Documentation Ubuntu - Recovery Mode](https://wiki.ubuntu.com/RecoveryMode)
- [Linux Mint Forums - Recovery Mode Guide](https://forums.linuxmint.com/)
- [Aide au diagnostic en recovery mode](https://help.ubuntu.com/community/RecoveryMode)

---


⏭️ [Réparation du GRUB](/23-depannage-et-resolution-de-problemes/04-reparation-du-grub.md)
