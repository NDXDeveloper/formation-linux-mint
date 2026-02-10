🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.7 - Les commandes sudo et root

## Introduction

Jusqu'à présent, nous avons travaillé en tant qu'utilisateur normal. Mais parfois, vous aurez besoin de privilèges administrateur pour :
- Installer des logiciels
- Modifier des fichiers système
- Gérer les services
- Créer des utilisateurs
- Configurer le réseau

**Analogie :** Si votre système Linux est une entreprise :
- Vous êtes un **employé** (utilisateur normal) avec un accès limité
- **root** est le **PDG** qui peut tout faire, tout modifier, tout décider
- **sudo** est comme une **autorisation temporaire** pour agir au nom du PDG

Dans ce chapitre, nous allons découvrir comment utiliser ces privilèges de manière sûre et responsable.

---

## Le compte root : Le super-utilisateur

### Qu'est-ce que root ?

**root** (aussi appelé superutilisateur) est le compte administrateur suprême sous Linux.

**Caractéristiques de root :**
- UID (identifiant utilisateur) = **0**
- Peut **tout** faire sur le système
- Peut lire, modifier, supprimer **n'importe quel fichier**
- Peut installer et désinstaller des programmes
- Peut modifier les configurations système
- **Aucune restriction** de permissions

### Pourquoi ne pas toujours utiliser root ?

**C'est extrêmement dangereux !**

**Risques de travailler en tant que root :**
1. **Erreurs catastrophiques** : Une simple faute de frappe peut détruire le système
   ```bash
   rm -rf / home/utilisateur  # CATASTROPHE ! (espace mal placé)
   ```

2. **Pas de filet de sécurité** : Aucune confirmation pour les actions dangereuses

3. **Vulnérabilités de sécurité** : Si un programme malveillant s'exécute en tant que root, il a le contrôle total

4. **Mauvaises habitudes** : On finit par oublier qu'on est root et on fait n'importe quoi

**Philosophie Linux moderne :**
- Utilisateur normal par défaut
- Privilèges root **seulement quand nécessaire**
- Durée **minimale** avec les privilèges

### Le prompt root

Quand vous êtes root, le prompt change :

**Utilisateur normal :**
```
utilisateur@ordinateur:~$
```

**Root :**
```
root@ordinateur:~#
```

**Notez le `#` au lieu de `$`** → Signe que vous êtes root !

---

## La commande `sudo` : Privilèges temporaires

### Signification

**sudo** signifie **Substitute User DO** (Faire en tant qu'autre utilisateur) ou **Super User DO** (Faire en tant que super-utilisateur).

### Principe de fonctionnement

`sudo` vous permet d'exécuter **une seule commande** avec les privilèges root, puis revenir immédiatement à votre compte utilisateur normal.

**Workflow :**
1. Vous tapez `sudo commande`
2. Le système vous demande **votre mot de passe** (pas celui de root !)
3. Si vous êtes autorisé, la commande s'exécute avec les privilèges root
4. Vous revenez automatiquement à votre compte normal

### Syntaxe de base

```bash
sudo commande
```

### Premier exemple

#### Installation d'un logiciel (nécessite root)

**Sans sudo (échoue) :**
```bash
apt install nano
```

**Résultat :**
```
E: Could not open lock file /var/lib/dpkg/lock - open (13: Permission denied)  
E: Unable to lock the administration directory (/var/lib/dpkg/), are you root?  
```

**Avec sudo (fonctionne) :**
```bash
sudo apt install nano
```

Le système demande votre mot de passe :
```
[sudo] password for utilisateur:
```

Tapez votre mot de passe (il ne s'affiche pas, c'est normal), puis **Entrée**.

La commande s'exécute avec les privilèges root.

### Caractéristiques importantes de sudo

#### 1. Demande votre mot de passe, pas celui de root

C'est **votre** mot de passe d'utilisateur que sudo demande, pas le mot de passe root.

**Pourquoi ?** Pour vérifier que c'est bien vous qui utilisez l'ordinateur.

#### 2. Mémorisation temporaire

Une fois que vous avez entré votre mot de passe, sudo le **mémorise pendant 15 minutes** (par défaut).

Pendant ce temps, vous pouvez utiliser sudo sans retaper le mot de passe.

**Exemple :**
```bash
sudo apt update        # Demande le mot de passe  
sudo apt upgrade       # Ne demande pas (dans les 15 minutes)  
# ... 15 minutes plus tard ...
sudo apt install vim   # Redemande le mot de passe
```

#### 3. Journal d'activité

Toutes les commandes `sudo` sont enregistrées dans les logs système.

**Voir l'historique sudo :**
```bash
sudo cat /var/log/auth.log | grep sudo
```

**Avantage :** Traçabilité et audit de sécurité.

---

## Exemples d'utilisation de sudo

### Installation et mise à jour de logiciels

```bash
sudo apt update                    # Mettre à jour la liste des paquets  
sudo apt upgrade                   # Mettre à jour les paquets installés  
sudo apt install firefox           # Installer Firefox  
sudo apt remove firefox            # Désinstaller Firefox  
```

### Édition de fichiers système

```bash
sudo nano /etc/ssh/sshd_config     # Éditer la configuration SSH  
sudo vim /etc/hosts                # Éditer le fichier hosts  
```

### Gestion des services

```bash
sudo systemctl start apache2       # Démarrer Apache  
sudo systemctl stop apache2        # Arrêter Apache  
sudo systemctl restart networking  # Redémarrer le réseau  
```

### Gestion des utilisateurs

```bash
sudo adduser nouvel_utilisateur    # Créer un utilisateur  
sudo deluser ancien_utilisateur    # Supprimer un utilisateur  
sudo passwd utilisateur            # Changer le mot de passe d'un utilisateur  
```

### Gestion des fichiers système

```bash
sudo cp fichier.conf /etc/         # Copier vers un dossier système  
sudo chown www-data:www-data /var/www/html  # Changer propriétaire  
sudo chmod 755 /usr/local/bin/script        # Modifier permissions  
```

### Commandes système

```bash
sudo reboot                        # Redémarrer l'ordinateur  
sudo shutdown -h now               # Éteindre immédiatement  
sudo shutdown -h +10               # Éteindre dans 10 minutes  
```

---

## Options utiles de sudo

### `-i` : Ouvrir un shell root interactif

```bash
sudo -i
```

**Effet :** Vous devenez root de manière interactive (comme `su -`).

Le prompt devient :
```
root@ordinateur:~#
```

**Pour revenir à votre compte :**
```bash
exit
```

**⚠️ Attention :** À utiliser avec précaution ! Vous êtes maintenant root jusqu'à ce que vous tapiez `exit`.

### `-s` : Ouvrir un shell avec sudo

```bash
sudo -s
```

Similaire à `-i`, mais garde votre environnement utilisateur.

### `-u` : Exécuter en tant qu'un autre utilisateur

```bash
sudo -u utilisateur commande
```

**Exemple :**
```bash
sudo -u www-data php script.php
```

Exécute le script PHP en tant que l'utilisateur `www-data`.

### `-k` : Oublier le mot de passe en cache

```bash
sudo -k
```

Force sudo à redemander le mot de passe à la prochaine utilisation.

**Utilité :** Sécurité quand vous quittez l'ordinateur.

### `-v` : Prolonger le cache du mot de passe

```bash
sudo -v
```

Réinitialise le timer de 15 minutes sans exécuter de commande.

### `-l` : Voir vos privilèges sudo

```bash
sudo -l
```

Liste les commandes que vous êtes autorisé à exécuter avec sudo.

---

## La commande `su` : Changer d'utilisateur

### Signification

**su** signifie **Switch User** (Changer d'utilisateur).

### Devenir root avec su

```bash
su -
```

ou

```bash
su - root
```

**Demande le mot de passe de root** (pas le vôtre !).

**Différence avec sudo :**
- `sudo` : Demande **votre** mot de passe
- `su` : Demande le mot de passe de l'utilisateur **cible** (root)

### Pourquoi le tiret `-` ?

```bash
su -        # Avec tiret (recommandé)  
su          # Sans tiret  
```

**Avec le tiret `-` :**
- Charge l'environnement complet de root
- Change le dossier vers `/root`
- C'est comme si root s'était connecté

**Sans le tiret :**
- Garde votre environnement actuel
- Reste dans votre dossier
- Peut causer des problèmes

**Toujours utiliser `su -` !**

### Changer vers un autre utilisateur

```bash
su - alice
```

Demande le mot de passe d'alice et vous connecte en tant qu'alice.

### Quitter une session su

```bash
exit
```

ou

```bash
Ctrl + D
```

---

## sudo vs su : Quelle différence ?

### Tableau comparatif

| Critère | sudo | su - |
|---------|------|------|
| **Mot de passe demandé** | Le vôtre | Celui de root |
| **Durée des privilèges** | Une commande | Jusqu'à `exit` |
| **Sécurité** | ✅ Plus sûr | ⚠️ Plus risqué |
| **Traçabilité** | ✅ Journalisé | ⚠️ Moins traçable |
| **Usage recommandé** | Administration quotidienne | Maintenance avancée |
| **Compte root nécessaire** | Non | Oui (mot de passe root) |

### Philosophie moderne

**Linux Mint et Ubuntu désactivent le compte root par défaut.**

**Pourquoi ?**
- Plus sûr : Pas de compte root actif = impossible de s'y connecter directement
- `sudo` suffit pour 99% des tâches
- Meilleure traçabilité

**Conséquence :** `su -` ne fonctionne pas sur ces systèmes (pas de mot de passe root défini).

**Solution :** Utilisez `sudo -i` à la place.

---

## Configuration de sudo : Le fichier sudoers

### Le fichier /etc/sudoers

Ce fichier contrôle qui peut utiliser `sudo` et pour quelles commandes.

**⚠️ NE JAMAIS éditer directement `/etc/sudoers` !**

### Éditer sudoers en toute sécurité

Utilisez la commande `visudo` :

```bash
sudo visudo
```

**Avantages de visudo :**
- Vérifie la syntaxe avant de sauvegarder
- Empêche deux personnes d'éditer en même temps
- Évite de casser le système sudo

### Structure du fichier sudoers

**Exemple de ligne :**
```
utilisateur ALL=(ALL:ALL) ALL
```

**Signification :**
- `utilisateur` : Nom de l'utilisateur
- Premier `ALL` : Sur tous les hôtes
- `(ALL:ALL)` : En tant que tous les utilisateurs et groupes
- Dernier `ALL` : Toutes les commandes

**Traduction :** L'utilisateur peut exécuter toutes les commandes sur tous les hôtes.

### Ajouter un utilisateur au groupe sudo

**Méthode recommandée :**

```bash
sudo usermod -aG sudo nom_utilisateur
```

Ajoute l'utilisateur au groupe `sudo`, lui donnant tous les privilèges.

**Vérifier :**
```bash
groups nom_utilisateur
```

### Exemples de configuration

#### Permettre une commande spécifique sans mot de passe

```
utilisateur ALL=(ALL) NOPASSWD: /usr/bin/apt update
```

L'utilisateur peut faire `sudo apt update` sans taper de mot de passe.

#### Permettre plusieurs commandes

```
utilisateur ALL=(ALL) NOPASSWD: /usr/bin/apt, /usr/bin/systemctl
```

#### Groupe avec tous les droits

```
%admin ALL=(ALL) ALL
```

Tous les membres du groupe `admin` peuvent utiliser sudo.

---

## Quand utiliser sudo ?

### ✅ Utilisez sudo pour :

1. **Installer/désinstaller des logiciels**
   ```bash
   sudo apt install package
   ```

2. **Modifier des fichiers système**
   ```bash
   sudo nano /etc/fstab
   ```

3. **Gérer les services**
   ```bash
   sudo systemctl restart service
   ```

4. **Gérer les utilisateurs**
   ```bash
   sudo adduser newuser
   ```

5. **Modifier les permissions système**
   ```bash
   sudo chmod 755 /usr/local/bin/script
   ```

6. **Accéder aux logs système**
   ```bash
   sudo less /var/log/syslog
   ```

### ❌ N'utilisez PAS sudo pour :

1. **Opérations dans votre dossier personnel**
   ```bash
   # Mauvais :
   sudo cp fichier.txt ~/Documents/

   # Bon :
   cp fichier.txt ~/Documents/
   ```

2. **Lancer des applications graphiques** (sauf exception)
   ```bash
   # À éviter :
   sudo firefox

   # Exceptions acceptables :
   sudo gedit /etc/hosts
   ```

3. **Contourner les permissions** au lieu de les comprendre
   ```bash
   # Mauvais réflexe :
   sudo rm fichier_problematique

   # Bon réflexe :
   # Comprendre pourquoi vous n'avez pas les permissions
   # Peut-être un problème de propriétaire ?
   ```

4. **"Juste au cas où"**

   N'ajoutez pas `sudo` par réflexe si vous n'êtes pas sûr qu'il est nécessaire.

---

## Dangers et risques

### Danger 1 : Destruction accidentelle

**Exemple tristement célèbre :**
```bash
sudo rm -rf / home/utilisateur
```

**Erreur :** Un espace entre `/` et `home`

**Résultat :** Suppression de TOUT le système à partir de la racine !

**Protection moderne :** Les versions récentes de `rm` empêchent `rm -rf /`, mais restez vigilant.

### Danger 2 : Modifier les permissions système

```bash
sudo chmod -R 777 /
```

**Résultat :** Tout le système devient accessible à tous. Désastre de sécurité !

### Danger 3 : Installer des logiciels douteux

```bash
curl http://site-suspect.com/install.sh | sudo bash
```

**Résultat :** Vous donnez les pleins pouvoirs à un script inconnu !

**Règle d'or :** Lisez toujours un script avant de l'exécuter avec sudo.

### Danger 4 : Applications graphiques en root

```bash
sudo firefox  
sudo nautilus  
```

**Problèmes :**
- Fichiers de configuration corrompus
- Fichiers créés appartenant à root dans votre dossier
- Risques de sécurité

---

## Bonnes pratiques

### 1. Principe du moindre privilège

Utilisez sudo **seulement quand nécessaire**.

**Posez-vous la question :** "Ai-je vraiment besoin de sudo pour cette commande ?"

### 2. Lisez les commandes avant de les exécuter

**Mauvais :**
```bash
# Sur un forum : "Tapez cette commande pour résoudre le problème"
sudo rm -rf /var/important
# Vous exécutez sans comprendre
```

**Bon :**
```bash
# Vous comprenez ce que fait chaque partie de la commande
# Vous vérifiez que c'est sûr
# Puis vous exécutez
```

### 3. Vérifiez deux fois les commandes dangereuses

Avant de presser Entrée sur une commande avec `sudo rm`, `sudo chmod -R`, etc. :

1. Relisez la commande
2. Vérifiez les chemins
3. Vérifiez les options
4. Assurez-vous que c'est bien ce que vous voulez faire

### 4. Utilisez sudo pour une seule commande

**Mauvais :**
```bash
sudo -i
# Vous restez root pendant 30 minutes
# Vous oubliez que vous êtes root
# Vous tapez une commande dangereuse
```

**Bon :**
```bash
sudo apt update  
sudo apt upgrade  
# Vous revenez à votre compte entre chaque commande
```

### 5. Invalidez le cache sudo quand vous partez

```bash
sudo -k
```

Surtout sur un ordinateur partagé !

### 6. Vérifiez le prompt

Regardez toujours le prompt avant d'exécuter une commande :
- `$` : Utilisateur normal → OK
- `#` : Root → Attention !

### 7. Ne pas donner sudo à n'importe qui

Sur un système partagé, ne donnez les droits sudo qu'aux personnes de confiance et compétentes.

### 8. Surveillez les logs

Vérifiez régulièrement qui utilise sudo :

```bash
sudo cat /var/log/auth.log | grep sudo
```

---

## Erreurs courantes et solutions

### Erreur 1 : Utilisateur n'est pas dans le fichier sudoers

**Problème :**
```bash
sudo apt update  
utilisateur is not in the sudoers file. This incident will be reported.  
```

**Cause :** Votre compte n'a pas les privilèges sudo.

**Solution :**
Demandez à un administrateur de vous ajouter au groupe sudo :
```bash
sudo usermod -aG sudo votre_nom
```

Puis déconnectez-vous et reconnectez-vous.

### Erreur 2 : Mot de passe incorrect

**Problème :**
```bash
[sudo] password for utilisateur:
Sorry, try again.
```

**Solutions :**
- Vérifiez que vous tapez le bon mot de passe (le vôtre, pas celui de root)
- Vérifiez les majuscules/minuscules
- Vérifiez que Caps Lock n'est pas activé
- Le mot de passe ne s'affiche pas, c'est normal !

### Erreur 3 : sudo: command not found

**Problème :**
```bash
sudo apt update  
sudo: command not found  
```

**Cause :** sudo n'est pas installé (rare sur Linux Mint).

**Solution :**
Connectez-vous en tant que root (au démarrage) et installez sudo :
```bash
apt install sudo
```

### Erreur 4 : Fichier créé avec mauvais propriétaire

**Problème :**
Vous avez utilisé sudo pour créer un fichier, maintenant il appartient à root.

```bash
sudo touch fichier.txt  
ls -l fichier.txt  
-rw-r--r-- 1 root root 0 ... fichier.txt
```

**Solution :**
Changez le propriétaire :
```bash
sudo chown utilisateur:utilisateur fichier.txt
```

**Prévention :** N'utilisez pas sudo pour créer des fichiers dans votre dossier personnel.

### Erreur 5 : sudo avec redirection

**Problème :**
```bash
sudo echo "texte" > /etc/fichier  
bash: /etc/fichier: Permission denied  
```

**Cause :** La redirection `>` est exécutée par votre shell, pas par sudo.

**Solutions :**

**Option 1 : tee**
```bash
echo "texte" | sudo tee /etc/fichier
```

**Option 2 : sh -c**
```bash
sudo sh -c 'echo "texte" > /etc/fichier'
```

**Option 3 : Éditeur**
```bash
sudo nano /etc/fichier
# Ajoutez le texte manuellement
```

---

## Alternatives et outils complémentaires

### pkexec : Équivalent graphique de sudo

Pour lancer une application graphique avec privilèges :

```bash
pkexec gedit /etc/hosts
```

Plus sûr que `sudo` pour les applications graphiques.

### gksudo / gksu (obsolète)

Anciennement utilisé, maintenant remplacé par `pkexec`.

### PolicyKit

Système de gestion des privilèges pour les applications graphiques.

### doas (alternative à sudo)

Plus simple et plus sécurisé que sudo, mais moins répandu.

```bash
sudo apt install doas
```

Configuration dans `/etc/doas.conf`.

---

## Commandes utiles pour la gestion des privilèges

### Voir qui vous êtes

```bash
whoami              # Affiche votre nom d'utilisateur  
id                  # Affiche votre UID, GID et groupes  
```

### Voir les utilisateurs avec sudo

```bash
grep '^sudo:' /etc/group
```

### Voir l'historique des commandes sudo

```bash
sudo cat /var/log/auth.log | grep sudo
```

Ou pour aujourd'hui :
```bash
sudo journalctl -u sudo -S today
```

### Tester une configuration sudoers

```bash
sudo visudo -c
```

Vérifie la syntaxe sans éditer.

---

## Scénarios pratiques

### Scénario 1 : Installer un logiciel

```bash
# Mettre à jour la liste des paquets
sudo apt update

# Installer le logiciel
sudo apt install vlc

# Vérifier l'installation
vlc --version
```

### Scénario 2 : Éditer un fichier de configuration

```bash
# Sauvegarder l'original
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup

# Éditer
sudo nano /etc/ssh/sshd_config

# Vérifier la syntaxe
sudo sshd -t

# Redémarrer le service
sudo systemctl restart ssh
```

### Scénario 3 : Créer un script système

```bash
# Créer le script dans votre dossier
nano mon_script.sh

# Le rendre exécutable
chmod +x mon_script.sh

# Le copier vers un emplacement système
sudo cp mon_script.sh /usr/local/bin/

# Vérifier
ls -l /usr/local/bin/mon_script.sh
```

### Scénario 4 : Nettoyer le système

```bash
# Mettre à jour
sudo apt update  
sudo apt upgrade  

# Nettoyer les paquets inutiles
sudo apt autoremove  
sudo apt autoclean  

# Revenir à l'utilisateur normal
# (automatique, vous n'avez rien à faire)
```

---

## Résumé

### Concepts clés

**root :**
- Le super-utilisateur avec tous les pouvoirs
- UID = 0
- Prompt avec `#`
- Dangereux si mal utilisé

**sudo :**
- Exécuter une commande avec privilèges root
- Demande **votre** mot de passe
- Privilèges temporaires (une commande)
- Journalisé et traçable

**su :**
- Changer d'utilisateur
- `su -` pour devenir root
- Demande le mot de passe de l'utilisateur cible
- Moins recommandé que sudo

### Commandes essentielles

```bash
sudo commande              # Exécuter avec privilèges root  
sudo -i                    # Devenir root interactivement  
sudo -k                    # Oublier le cache du mot de passe  
sudo -l                    # Voir vos privilèges sudo  
sudo visudo                # Éditer la configuration sudo  
su -                       # Devenir root (si mot de passe défini)  
exit                       # Quitter une session root  
whoami                     # Voir qui vous êtes  
```

### Règles d'or de sécurité

1. ✅ **Utilisez sudo seulement quand nécessaire**
2. ✅ **Lisez et comprenez les commandes avant de les exécuter**
3. ✅ **Vérifiez deux fois les commandes dangereuses**
4. ✅ **Ne restez pas root plus longtemps que nécessaire**
5. ✅ **Invalidez le cache sudo (`sudo -k`) quand vous partez**
6. ❌ **Ne tapez jamais `sudo rm -rf /`**
7. ❌ **N'exécutez pas de scripts inconnus avec sudo**
8. ❌ **N'utilisez pas sudo pour des opérations dans votre dossier personnel**

### Checklist avant d'utiliser sudo

- [ ] Est-ce vraiment nécessaire ?
- [ ] Ai-je compris ce que fait la commande ?
- [ ] Le chemin est-il correct ?
- [ ] Les options sont-elles bonnes ?
- [ ] Y a-t-il un risque de perte de données ?
- [ ] Ai-je fait une sauvegarde si nécessaire ?

**sudo est un outil puissant. Avec de grands pouvoirs viennent de grandes responsabilités !**

Utilisez-le avec sagesse et prudence. Quand vous comprenez ce que vous faites et pourquoi, sudo devient un allié précieux pour gérer votre système Linux efficacement et en toute sécurité.

Dans le prochain chapitre, nous découvrirons les redirections et pipes, des outils qui permettent de combiner les commandes de manière puissante.

⏭️ [Redirection et pipes (>, >>, |)](/07-le-terminal-et-commandes-de-base/08-redirection-et-pipes.md)
