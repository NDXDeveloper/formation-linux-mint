🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 11.3 Mots de passe et authentification

## Introduction

L'authentification est la première ligne de défense de votre système Linux Mint. Un mot de passe fort et des mécanismes d'authentification bien configurés sont essentiels pour protéger vos données personnelles et votre vie privée.

### Qu'est-ce que l'authentification ?

L'**authentification** est le processus qui permet de vérifier l'identité d'un utilisateur. Sous Linux, cela se fait principalement par :
- **Mots de passe** (ce que vous savez)
- **Clés SSH** (ce que vous possédez)
- **Authentification biométrique** (ce que vous êtes - empreintes digitales, reconnaissance faciale)
- **Authentification à deux facteurs (2FA)** (combinaison de plusieurs méthodes)

Dans ce chapitre, nous allons explorer comment gérer efficacement vos mots de passe et sécuriser l'accès à votre système.

---

## Comment Linux stocke les mots de passe

### Les fichiers système

Linux stocke les informations d'authentification dans des fichiers spécifiques :

#### /etc/passwd
Ce fichier contient les informations de base des comptes utilisateurs :
```bash
cat /etc/passwd
```

Exemple de ligne :
```
sophie:x:1000:1000:Sophie Martin:/home/sophie:/bin/bash
```

Décomposition :
- `sophie` : nom d'utilisateur
- `x` : le mot de passe est dans /etc/shadow (pour des raisons de sécurité)
- `1000` : UID (identifiant utilisateur)
- `1000` : GID (identifiant de groupe primaire)
- `Sophie Martin` : nom complet
- `/home/sophie` : répertoire personnel
- `/bin/bash` : shell par défaut

#### /etc/shadow
Ce fichier contient les **mots de passe chiffrés** et les informations de sécurité associées :
```bash
sudo cat /etc/shadow
```

> **Important** : Seul root peut lire ce fichier pour des raisons de sécurité.

Exemple de ligne :
```
sophie:$6$xyz...:19000:0:99999:7:::
```

Les champs incluent :
- Le nom d'utilisateur
- Le mot de passe haché (chiffré)
- La date de dernière modification
- Les jours avant de pouvoir changer le mot de passe
- Les jours avant de devoir changer le mot de passe
- Les jours d'avertissement avant expiration
- Etc.

### Hachage des mots de passe

Linux ne stocke **jamais** les mots de passe en clair. Il utilise des fonctions de hachage (SHA-512 par défaut) :
- Le mot de passe est transformé en une chaîne unique et irréversible
- Impossible de retrouver le mot de passe original à partir du hash
- Même mot de passe = hash différent grâce au "salt" (sel cryptographique)

---

## Gérer les mots de passe

### Changer votre propre mot de passe

#### Méthode graphique

1. Ouvrez le **Menu principal** → **Paramètres système**
2. Cliquez sur **Comptes utilisateurs**
3. Cliquez sur le **cadenas** pour déverrouiller (entrez votre mot de passe actuel)
4. Cliquez sur les **points noirs** (●●●●●) à côté de "Mot de passe"
5. Entrez :
   - Votre mot de passe actuel
   - Le nouveau mot de passe (deux fois)
6. Cliquez sur **Modifier**

#### Méthode en ligne de commande

```bash
passwd
```

Le système vous demandera :
1. Votre mot de passe actuel (pour confirmation)
2. Le nouveau mot de passe
3. Confirmer le nouveau mot de passe

Exemple d'interaction :
```
Current password: ********  
New password: ************  
Retype new password: ************  
passwd: password updated successfully  
```

### Changer le mot de passe d'un autre utilisateur

En tant qu'administrateur, vous pouvez changer le mot de passe de n'importe quel utilisateur :

```bash
sudo passwd nom_utilisateur
```

Exemple :
```bash
sudo passwd jean
```

> **Note** : Avec `sudo passwd`, vous n'avez pas besoin de connaître l'ancien mot de passe de l'utilisateur.

### Forcer un utilisateur à changer son mot de passe

Pour obliger un utilisateur à définir un nouveau mot de passe lors de sa prochaine connexion :

```bash
sudo passwd -e nom_utilisateur
```

Ou définir une date d'expiration :
```bash
sudo chage -d 0 nom_utilisateur
```

---

## Créer un mot de passe sécurisé

### Les critères d'un bon mot de passe

Un mot de passe fort doit respecter ces règles :

#### 1. Longueur minimale
- **Au moins 12 caractères** (idéalement 16 ou plus)
- La longueur est plus importante que la complexité

#### 2. Complexité
Combinez différents types de caractères :
- **Lettres minuscules** (a-z)
- **Lettres majuscules** (A-Z)
- **Chiffres** (0-9)
- **Symboles spéciaux** (!@#$%^&*()_+-=[]{}|;:,.<>?)

#### 3. Imprévisibilité
Évitez :
- ❌ Les mots du dictionnaire (`password123`, `azerty`)
- ❌ Les informations personnelles (date de naissance, nom de famille, ville)
- ❌ Les séquences simples (`123456`, `abcdef`, `qwerty`)
- ❌ Les mots de passe réutilisés sur plusieurs comptes

### Méthodes pour créer des mots de passe forts

#### Méthode 1 : La phrase de passe (Passphrase)

Créez une phrase longue et mémorable, puis modifiez-la :

**Exemple** :
- Phrase de base : `J'aime manger des pommes vertes en été`
- Transformation : `J'aim3M@ng3rD3sP0mm3sV3rt3s!`
- Ou plus simple : `Jaime-Manger-Des-Pommes-Vertes-2024!`

#### Méthode 2 : La méthode des initiales

Prenez la première lettre de chaque mot d'une phrase :

**Exemple** :
- Phrase : "Mon chat noir s'appelle Félix et il a 5 ans"
- Mot de passe : `McnsaF&ia5a!`

#### Méthode 3 : Générateur aléatoire

Utilisez un générateur de mots de passe :

```bash
# Générer un mot de passe aléatoire de 16 caractères
pwgen 16 1
```

Si `pwgen` n'est pas installé :
```bash
sudo apt install pwgen
```

Ou utilisez `openssl` :
```bash
openssl rand -base64 16
```

Résultat exemple : `Kj8mP2nQ9xL4vR3s`

#### Méthode 4 : Diceware

Utilisez plusieurs mots aléatoires séparés par des caractères spéciaux :

**Exemple** : `Cheval-Bleu-Nuage-Cafe-2024!`

### Vérifier la force d'un mot de passe

Linux affiche souvent un indicateur de force lors de la création :
```
New password:  
Bad password: too short  
```

Ou
```
New password:  
Good password  
```

Pour tester la force d'un mot de passe :
```bash
# Installer cracklib
sudo apt install libcrack2

# Tester un mot de passe
echo "VotreMdp123!" | cracklib-check
```

---

## Politique de mots de passe

### Configurer les exigences de complexité

Linux permet de définir des règles strictes pour les mots de passe via **PAM** (Pluggable Authentication Modules).

#### Installer pwquality

```bash
sudo apt install libpam-pwquality
```

#### Configurer les règles

Éditez le fichier de configuration :
```bash
sudo nano /etc/security/pwquality.conf
```

Paramètres importants :
```bash
# Longueur minimale
minlen = 12

# Nombre minimum de caractères différents du mot de passe précédent
difok = 3

# Nombre minimum de chiffres
dcredit = -1

# Nombre minimum de majuscules
ucredit = -1

# Nombre minimum de minuscules
lcredit = -1

# Nombre minimum de caractères spéciaux
ocredit = -1

# Interdire les mots du dictionnaire
dictcheck = 1

# Interdire les mots de passe contenant le nom d'utilisateur
usercheck = 1
```

> **Note** : Les valeurs négatives (comme `-1`) indiquent un **minimum requis**. Les valeurs positives accordent des "crédits" pour la complexité.

### Définir l'expiration des mots de passe

#### Pour un utilisateur spécifique

Forcer le changement tous les 90 jours :
```bash
sudo chage -M 90 sophie
```

Voir les informations d'expiration :
```bash
sudo chage -l sophie
```

Résultat :
```
Last password change                    : nov 15, 2024  
Password expires                        : fév 13, 2025  
Password inactive                       : never  
Account expires                         : never  
Minimum number of days between password change : 0  
Maximum number of days between password change : 90  
Number of days of warning before password expires : 7  
```

#### Paramètres de chage

| Commande | Description |
|----------|-------------|
| `chage -M 90 user` | Maximum 90 jours avant expiration |
| `chage -m 1 user` | Minimum 1 jour avant de pouvoir changer |
| `chage -W 7 user` | Avertissement 7 jours avant expiration |
| `chage -I 14 user` | Compte inactif après 14 jours d'expiration |
| `chage -E 2025-12-31 user` | Le compte expire le 31/12/2025 |

#### Configuration par défaut

Pour appliquer ces règles à tous les nouveaux utilisateurs, éditez :
```bash
sudo nano /etc/login.defs
```

Recherchez et modifiez :
```bash
PASS_MAX_DAYS   90      # Expiration tous les 90 jours  
PASS_MIN_DAYS   1       # Minimum 1 jour entre les changements  
PASS_WARN_AGE   7       # Avertissement 7 jours avant  
```

---

## Gestionnaires de mots de passe

### Pourquoi utiliser un gestionnaire de mots de passe ?

- **Sécurité** : Génère et stocke des mots de passe forts et uniques
- **Commodité** : Plus besoin de mémoriser des dizaines de mots de passe
- **Protection** : Chiffrement fort de votre base de données de mots de passe
- **Synchronisation** : Accès à vos mots de passe sur tous vos appareils

### KeePassXC (recommandé pour Linux)

**KeePassXC** est un gestionnaire de mots de passe gratuit, open source et très sécurisé.

#### Installation

```bash
sudo apt install keepassxc
```

Ou via Flatpak :
```bash
flatpak install flathub org.keepassxc.KeePassXC
```

#### Fonctionnalités principales

- Base de données chiffrée localement (vous gardez le contrôle)
- Génération de mots de passe sécurisés
- Auto-remplissage dans les navigateurs (via extension)
- Support de la 2FA (TOTP)
- Compatible avec KeePass 2
- Pas de cloud par défaut (mais vous pouvez synchroniser manuellement)

#### Utilisation de base

1. **Créer une base de données** :
   - Lancez KeePassXC
   - Créez une nouvelle base de données
   - Choisissez un **mot de passe maître** très fort (c'est le seul que vous devrez mémoriser)
   - Optionnel : Ajoutez un fichier clé pour plus de sécurité

2. **Ajouter des entrées** :
   - Cliquez sur "Nouvelle entrée"
   - Remplissez : titre, nom d'utilisateur, mot de passe, URL, notes
   - Utilisez le générateur pour créer un mot de passe fort

3. **Organiser** :
   - Créez des groupes (Travail, Personnel, Banque, etc.)
   - Utilisez des tags pour catégoriser

4. **Synchroniser** (optionnel) :
   - Stockez votre base `.kdbx` dans un cloud (Nextcloud, Dropbox, etc.)
   - Ou utilisez Syncthing pour synchroniser entre vos appareils

### Autres gestionnaires populaires

#### Bitwarden
- Open source
- Synchronisation cloud native
- Applications pour tous les systèmes
- Version gratuite très complète
```bash
flatpak install flathub com.bitwarden.desktop
```

#### Pass (password-store)
- Gestionnaire minimaliste en ligne de commande
- Utilise GPG pour le chiffrement
- Intégration Git pour la synchronisation
```bash
sudo apt install pass
```

#### 1Password
- Solution commerciale premium
- Très conviviale
- Support professionnel
- Payant (mais version d'essai gratuite)

---

## Authentification à deux facteurs (2FA)

### Qu'est-ce que la 2FA ?

L'authentification à deux facteurs ajoute une **deuxième couche de sécurité** en plus du mot de passe :
1. **Quelque chose que vous savez** : votre mot de passe
2. **Quelque chose que vous possédez** : votre téléphone, une clé de sécurité

Même si quelqu'un vole votre mot de passe, il ne pourra pas se connecter sans le second facteur.

### Activer la 2FA pour Linux

#### Méthode 1 : Google Authenticator (TOTP)

**Installation** :
```bash
sudo apt install libpam-google-authenticator
```

**Configuration pour votre utilisateur** :
```bash
google-authenticator
```

Répondez aux questions :
- `Do you want authentication tokens to be time-based (y/n)` → **y**
- Scannez le QR code avec une application mobile (Google Authenticator, Authy, etc.)
- Notez les codes de secours dans un endroit sûr

**Activer pour SSH** :
```bash
sudo nano /etc/pam.d/sshd
```

Ajoutez à la fin :
```
auth required pam_google_authenticator.so
```

Puis éditez :
```bash
sudo nano /etc/ssh/sshd_config
```

Modifiez :
```
ChallengeResponseAuthentication yes
```

Redémarrez SSH :
```bash
sudo systemctl restart sshd
```

Maintenant, les connexions SSH nécessiteront le mot de passe ET un code 2FA.

#### Méthode 2 : Clés de sécurité matérielles (YubiKey, etc.)

Les clés de sécurité physiques offrent la meilleure protection contre le phishing.

**Installation du support YubiKey** :
```bash
sudo apt install libpam-yubico yubikey-manager
```

Configuration avancée disponible dans la documentation YubiKey.

### Applications 2FA pour mobile

- **Aegis** (Android, open source, recommandé)
- **Google Authenticator** (Android/iOS)
- **Authy** (Android/iOS, avec sauvegarde cloud)
- **andOTP** (Android, open source)

---

## Authentification par clés SSH

### Pourquoi utiliser des clés SSH ?

Les clés SSH sont **plus sécurisées** que les mots de passe car :
- Elles utilisent une cryptographie asymétrique (clé publique/privée)
- Impossibles à deviner par force brute
- Pas de transmission du secret sur le réseau
- Protection contre les attaques par dictionnaire

### Générer une paire de clés SSH

```bash
ssh-keygen -t ed25519 -C "votre_email@example.com"
```

Options :
- `-t ed25519` : Type de clé (ed25519 est moderne et sécurisé)
- `-C` : Commentaire (généralement votre email)

Alternatives pour compatibilité maximale :
```bash
ssh-keygen -t rsa -b 4096 -C "votre_email@example.com"
```

**Processus interactif** :
1. **Emplacement** : Appuyez sur Entrée pour accepter `/home/utilisateur/.ssh/id_ed25519`
2. **Passphrase** : Entrez une phrase de passe pour protéger la clé privée (recommandé)
3. Confirmez la passphrase

Résultat : Deux fichiers créés :
- `~/.ssh/id_ed25519` : Clé **privée** (à garder secrète)
- `~/.ssh/id_ed25519.pub` : Clé **publique** (à partager)

### Copier la clé publique sur un serveur distant

```bash
ssh-copy-id utilisateur@serveur.com
```

Ou manuellement :
```bash
cat ~/.ssh/id_ed25519.pub | ssh utilisateur@serveur.com "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

### Protéger vos clés SSH

**Permissions correctes** (critiques) :
```bash
chmod 700 ~/.ssh  
chmod 600 ~/.ssh/id_ed25519  
chmod 644 ~/.ssh/id_ed25519.pub  
chmod 600 ~/.ssh/authorized_keys  
```

SSH refusera d'utiliser des clés avec des permissions trop ouvertes.

### Utiliser ssh-agent pour éviter de ressaisir la passphrase

```bash
eval "$(ssh-agent -s)"  
ssh-add ~/.ssh/id_ed25519  
```

Entrez la passphrase une fois, elle sera mémorisée pour la session.

---

## Verrouillage automatique de session

### Configurer le verrouillage automatique

Pour protéger votre session quand vous vous éloignez de votre ordinateur :

1. **Menu principal** → **Paramètres système** → **Écran de veille**
2. Activez **"Verrouiller l'écran lors de la mise en veille"**
3. Réglez le délai d'inactivité (par exemple, 5 minutes)

### Verrouiller manuellement

**Raccourci clavier** (par défaut) :
- `Ctrl + Alt + L`

Ou via le menu :
- Cliquez sur votre nom d'utilisateur → **Verrouiller l'écran**

### Ligne de commande

```bash
cinnamon-screensaver-command -l
```

Ou sous MATE :
```bash
mate-screensaver-command -l
```

---

## Sudo et authentification administrative

### Configurer le timeout de sudo

Par défaut, `sudo` mémorise votre mot de passe pendant 15 minutes. Pour modifier ce délai :

```bash
sudo visudo
```

Ajoutez ou modifiez :
```
Defaults timestamp_timeout=5
```

Cela réduit le timeout à 5 minutes. Utilisez `0` pour demander le mot de passe à chaque fois.

### Permettre des commandes sans mot de passe (avancé)

**Attention** : À utiliser avec précaution.

```bash
sudo visudo
```

Ajoutez (exemple pour la commande `apt update`) :
```
sophie ALL=(ALL) NOPASSWD: /usr/bin/apt update
```

### Logs sudo

Voir qui a utilisé sudo et quand :
```bash
sudo cat /var/log/auth.log | grep sudo
```

---

## Sécurité avancée : PAM

### Qu'est-ce que PAM ?

**PAM** (Pluggable Authentication Modules) est le système modulaire d'authentification de Linux. Il permet de configurer finement comment et quand l'authentification est requise.

### Fichiers de configuration PAM

Situés dans `/etc/pam.d/`, chaque service a son propre fichier :
- `/etc/pam.d/sudo` : Configuration pour sudo
- `/etc/pam.d/login` : Configuration pour les connexions
- `/etc/pam.d/sshd` : Configuration pour SSH
- `/etc/pam.d/common-auth` : Configuration commune

### Exemple : Limiter les tentatives de connexion

Éditez :
```bash
sudo nano /etc/pam.d/common-auth
```

Ajoutez :
```
auth required pam_tally2.so deny=5 unlock_time=900
```

Cela verrouille le compte après 5 tentatives échouées pendant 15 minutes (900 secondes).

### Réinitialiser le compteur de tentatives

```bash
sudo pam_tally2 --user=sophie --reset
```

---

## Bonnes pratiques de sécurité

### Pour les mots de passe

1. ✅ **Un mot de passe unique par compte** : Ne réutilisez jamais le même mot de passe
2. ✅ **Longueur > Complexité** : Privilégiez les mots de passe longs (16+ caractères)
3. ✅ **Utilisez un gestionnaire** : KeePassXC, Bitwarden, etc.
4. ✅ **Activez la 2FA** : Partout où c'est possible
5. ✅ **Changez les mots de passe compromis** : Immédiatement
6. ❌ **Ne notez pas sur papier** : Ou dans un fichier non chiffré
7. ❌ **Ne partagez jamais** : Même avec des collègues de confiance
8. ❌ **Ne saisissez pas sur des ordinateurs publics** : Sauf si absolument nécessaire

### Pour l'authentification système

1. ✅ **Utilisez des clés SSH** : Au lieu de mots de passe pour les serveurs
2. ✅ **Désactivez l'authentification root par SSH** : Voir chapitre SSH
3. ✅ **Configurez le verrouillage automatique** : Après 5-10 minutes d'inactivité
4. ✅ **Surveillez les logs** : Vérifiez régulièrement `/var/log/auth.log`
5. ✅ **Mettez à jour régulièrement** : Les failles de sécurité sont corrigées constamment
6. ❌ **N'utilisez pas de connexion automatique** : Sur des machines accessibles à d'autres

### En cas de compromission

Si vous suspectez que votre mot de passe a été compromis :

1. **Changez-le immédiatement** :
   ```bash
   passwd
   ```

2. **Vérifiez les connexions récentes** :
   ```bash
   last
   lastlog
   ```

3. **Examinez les processus en cours** :
   ```bash
   ps aux | grep votre_nom_utilisateur
   ```

4. **Vérifiez les modifications système** :
   ```bash
   sudo journalctl -xe
   ```

5. **Révoquez les clés SSH** :
   ```bash
   rm ~/.ssh/authorized_keys
   ```
   Puis régénérez de nouvelles clés.

6. **Changez tous vos autres mots de passe** : Surtout ceux qui étaient similaires

---

## Commandes de référence rapide

### Gestion des mots de passe

| Commande | Description |
|----------|-------------|
| `passwd` | Changer son mot de passe |
| `sudo passwd utilisateur` | Changer le mot de passe d'un utilisateur |
| `sudo passwd -l utilisateur` | Verrouiller un compte |
| `sudo passwd -u utilisateur` | Déverrouiller un compte |
| `sudo passwd -e utilisateur` | Forcer le changement au prochain login |
| `sudo chage -l utilisateur` | Voir les infos d'expiration |
| `pwgen 16 1` | Générer un mot de passe aléatoire |

### Clés SSH

| Commande | Description |
|----------|-------------|
| `ssh-keygen -t ed25519` | Générer une paire de clés |
| `ssh-copy-id user@host` | Copier la clé publique sur un serveur |
| `ssh-add ~/.ssh/id_ed25519` | Ajouter la clé à l'agent |
| `chmod 600 ~/.ssh/id_ed25519` | Sécuriser la clé privée |

### 2FA

| Commande | Description |
|----------|-------------|
| `google-authenticator` | Configurer 2FA avec Google Authenticator |
| `sudo apt install libpam-google-authenticator` | Installer le module 2FA |

---

## Résumé

La sécurité de l'authentification repose sur plusieurs piliers :

- **Mots de passe forts** : Longs, complexes, uniques
- **Gestionnaires de mots de passe** : Pour ne pas avoir à tout mémoriser
- **Authentification à deux facteurs** : Protection supplémentaire essentielle
- **Clés SSH** : Alternative plus sécurisée aux mots de passe pour les serveurs
- **Bonnes pratiques** : Verrouillage automatique, surveillance, mises à jour

En combinant ces éléments, vous créez une défense solide contre les accès non autorisés.

Dans le prochain chapitre, nous explorerons le **chiffrement des données**, qui protège vos informations même si quelqu'un obtient un accès physique à votre ordinateur.


⏭️ [Chiffrement des données (VeraCrypt, LUKS)](/11-gestion-des-utilisateurs-et-securite/04-chiffrement-des-donnees.md)
