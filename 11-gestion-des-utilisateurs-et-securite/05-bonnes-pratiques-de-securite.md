🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 11.5 Bonnes pratiques de sécurité

## Introduction

La sécurité informatique n'est pas un produit qu'on installe, mais un **ensemble de bonnes pratiques** à adopter au quotidien. Linux Mint est déjà plus sécurisé que de nombreux autres systèmes d'exploitation, mais votre comportement et vos habitudes sont tout aussi importants que les outils techniques.

### La sécurité, c'est quoi ?

La sécurité informatique vise à protéger trois éléments fondamentaux :

1. **Confidentialité** : Vos données ne sont accessibles qu'aux personnes autorisées
2. **Intégrité** : Vos données ne sont pas modifiées par des personnes non autorisées
3. **Disponibilité** : Vous pouvez accéder à vos données quand vous en avez besoin

### Le maillon faible

> **Principe fondamental** : "La sécurité d'un système est celle de son maillon le plus faible."

Vous pouvez avoir le meilleur chiffrement du monde, si vous utilisez "123456" comme mot de passe ou si vous cliquez sur tous les liens douteux, votre système reste vulnérable.

### Linux est-il plus sécurisé ?

**Oui**, pour plusieurs raisons :
- Architecture de permissions robuste
- Séparation stricte entre utilisateur et administrateur
- Code open source régulièrement audité
- Moins ciblé par les malwares (part de marché plus faible)
- Communauté active et réactive

**Mais** cela ne vous dispense pas de suivre les bonnes pratiques !

---

## 1. Mises à jour et maintenance du système

### Maintenir le système à jour

Les mises à jour corrigent des **failles de sécurité** découvertes. Un système non à jour est une porte ouverte aux attaquants.

#### Activer les mises à jour automatiques

1. Ouvrez le **Gestionnaire de mises à jour**
2. Allez dans **Édition** → **Préférences**
3. Dans l'onglet **Automatisation** :
   - Cochez **"Actualiser automatiquement la liste des paquets"**
   - Fréquence recommandée : **Quotidienne** ou **Chaque semaine**

#### Installer les mises à jour régulièrement

**Fréquence recommandée** : Au moins une fois par semaine

```bash
sudo apt update && sudo apt upgrade -y
```

#### Prioriser les mises à jour de sécurité

Linux Mint classe les mises à jour par niveaux. Installez au minimum :
- **Niveau 1** : Mises à jour de sécurité certifiées
- **Niveau 2** : Mises à jour de sécurité recommandées
- **Niveau 3** : Mises à jour de sécurité

#### Redémarrer après les mises à jour du noyau

Quand une mise à jour du noyau Linux est installée, redémarrez pour l'activer :

```bash
sudo reboot
```

Vérifiez si un redémarrage est nécessaire :
```bash
cat /var/run/reboot-required
```

### Nettoyer régulièrement le système

#### Supprimer les paquets inutilisés

```bash
sudo apt autoremove
sudo apt autoclean
```

#### Nettoyer les fichiers temporaires

```bash
sudo apt install bleachbit
```

Lancez BleachBit et sélectionnez ce que vous voulez nettoyer (cache, logs anciens, etc.).

> **Attention** : Ne supprimez pas les fichiers système essentiels. En cas de doute, ne cochez pas.

---

## 2. Sécurité des comptes et authentification

### Utiliser des mots de passe forts

Nous l'avons vu dans le chapitre précédent, mais c'est tellement important que ça mérite d'être répété :

#### Critères d'un mot de passe fort

- ✅ **Au moins 12-16 caractères** (idéalement 20+)
- ✅ **Mélange de caractères** : majuscules, minuscules, chiffres, symboles
- ✅ **Unique** : Un mot de passe différent par service
- ✅ **Pas d'informations personnelles** : Pas de date de naissance, nom de famille, etc.
- ✅ **Gestionnaire de mots de passe** : KeePassXC, Bitwarden

#### Exemples de mauvais mots de passe

- ❌ `password123`
- ❌ `azerty`
- ❌ `jeannedupont1985`
- ❌ `motdepasse`
- ❌ `123456`

### Ne pas utiliser root directement

Sous Linux Mint, le compte root est désactivé par défaut. **C'est une excellente chose !**

#### Pourquoi ne pas utiliser root ?

- Une erreur avec root peut **détruire le système entier**
- Les logiciels malveillants auraient un accès total
- Plus difficile de tracer qui a fait quoi

#### Utiliser sudo à la place

```bash
sudo commande
```

Sudo demande votre mot de passe et enregistre toutes les actions dans les logs.

#### Si vous devez vraiment utiliser root temporairement

```bash
sudo -i
```

**Sortez immédiatement après** :
```bash
exit
```

### Limiter les comptes administrateurs

- N'accordez les droits **sudo** qu'aux personnes qui en ont vraiment besoin
- Créez des **comptes standards** pour l'usage quotidien
- Révisez régulièrement qui appartient au groupe `sudo` :
  ```bash
  grep sudo /etc/group
  ```

### Activer l'authentification à deux facteurs (2FA)

Pour les services en ligne et, si possible, pour les connexions SSH :

```bash
sudo apt install libpam-google-authenticator
google-authenticator
```

Voir le chapitre précédent pour plus de détails.

### Verrouiller l'écran

#### Automatiquement après inactivité

1. **Paramètres système** → **Écran de veille**
2. Activez **"Verrouiller l'écran lors de la mise en veille"**
3. Réglez le délai : **5 à 10 minutes** recommandées

#### Manuellement avant de vous éloigner

**Raccourci clavier** : `Ctrl + Alt + L`

**Habitude à prendre** : Verrouillez TOUJOURS votre écran avant de quitter votre poste.

---

## 3. Pare-feu et sécurité réseau

### Activer le pare-feu UFW

Linux Mint inclut **UFW** (Uncomplicated Firewall), mais il n'est pas activé par défaut.

#### Activer UFW

```bash
sudo ufw enable
```

#### Vérifier le statut

```bash
sudo ufw status
```

#### Interface graphique GUFW

Pour les débutants, l'interface graphique est plus simple :

```bash
sudo apt install gufw
```

Lancez **GUFW** depuis le menu, activez le pare-feu et réglez le profil sur **"Public"** ou **"Home"** selon votre situation.

### Bloquer les ports inutilisés

Par défaut, UFW bloque toutes les connexions entrantes. C'est parfait pour un usage bureau.

#### Autoriser uniquement ce dont vous avez besoin

Exemple pour SSH :
```bash
sudo ufw allow 22/tcp
```

Exemple pour un serveur web :
```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

#### Bloquer des adresses IP spécifiques

```bash
sudo ufw deny from 192.168.1.100
```

### Désactiver les services inutiles

Moins il y a de services en écoute, moins il y a de surface d'attaque.

#### Lister les services actifs

```bash
sudo systemctl list-unit-files --type=service --state=enabled
```

#### Désactiver un service

```bash
sudo systemctl disable nom_du_service
sudo systemctl stop nom_du_service
```

#### Voir les ports en écoute

```bash
sudo ss -tulpn
```

Si vous voyez un port ouvert que vous ne reconnaissez pas, enquêtez !

### Sécuriser SSH (si vous l'utilisez)

Si vous utilisez SSH pour vous connecter à distance :

#### Changer le port par défaut

Éditez `/etc/ssh/sshd_config` :
```bash
sudo nano /etc/ssh/sshd_config
```

Changez :
```
Port 22
```

En :
```
Port 2222
```

Redémarrez SSH :
```bash
sudo systemctl restart sshd
```

#### Désactiver la connexion root

Dans `/etc/ssh/sshd_config` :
```
PermitRootLogin no
```

#### Utiliser uniquement des clés SSH

Dans `/etc/ssh/sshd_config` :
```
PasswordAuthentication no
PubkeyAuthentication yes
```

**Attention** : Configurez d'abord vos clés SSH avant de désactiver l'authentification par mot de passe !

#### Installer Fail2Ban

Fail2Ban bloque automatiquement les IP qui tentent de se connecter trop souvent :

```bash
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

### Utiliser un VPN pour le WiFi public

Sur les réseaux WiFi publics (cafés, aéroports, hôtels), vos données peuvent être interceptées.

#### Solutions VPN recommandées

- **OpenVPN** (open source)
- **WireGuard** (moderne et rapide)
- Services commerciaux : ProtonVPN, Mullvad, etc.

#### Installation OpenVPN

```bash
sudo apt install openvpn
```

Importez le fichier de configuration fourni par votre fournisseur VPN.

---

## 4. Sécurité des navigateurs et navigation web

### Choisir un navigateur respectueux de la vie privée

Linux Mint inclut **Firefox** par défaut, qui est un excellent choix.

#### Navigateurs recommandés

1. **Firefox** (avec configurations adaptées)
2. **Brave** (axé sur la vie privée)
3. **Librewolf** (fork de Firefox durci)

#### Navigateurs à éviter

❌ **Navigateurs propriétaires** qui collectent massivement vos données

### Configurer Firefox pour plus de sécurité

#### Extensions recommandées

1. **uBlock Origin** : Bloqueur de publicités et de traqueurs
   - Essentiel pour bloquer les malwares et les traqueurs

2. **Privacy Badger** : Protection contre les traqueurs
   - Développé par l'EFF (Electronic Frontier Foundation)

3. **HTTPS Everywhere** : Force le chiffrement HTTPS
   - Intégré nativement dans Firefox depuis la version 91

4. **Cookie AutoDelete** : Supprime automatiquement les cookies
   - Protège votre vie privée entre les sessions

5. **Bitwarden** ou **KeePassXC** : Gestionnaire de mots de passe
   - Pour des mots de passe uniques et forts partout

#### Paramètres de confidentialité Firefox

1. Ouvrez **Préférences** → **Vie privée et sécurité**
2. **Protection renforcée contre le pistage** : Sélectionnez **"Stricte"**
3. **Cookies** : "Supprimer les cookies et les données des sites à la fermeture de Firefox"
4. **Ne pas me pister** : Activez l'option
5. **HTTPS uniquement** : Activez le mode HTTPS uniquement

### Ne pas cliquer sur des liens suspects

#### Reconnaître un lien suspect

- ❌ URLs raccourcies sans contexte (bit.ly, tinyurl)
- ❌ Fautes d'orthographe dans le domaine (g00gle.com au lieu de google.com)
- ❌ Domaines inconnus avec des extensions étranges (.xyz, .top, etc.)
- ❌ Messages urgents ("Votre compte va être fermé !")

#### Vérifier avant de cliquer

- Passez la souris sur le lien pour voir l'URL réelle
- Tapez manuellement l'adresse dans la barre d'adresse
- Utilisez un vérificateur d'URL (VirusTotal, etc.)

### Méfiez-vous du phishing

Le **phishing** est une tentative de vous tromper pour obtenir vos informations personnelles.

#### Signes d'alerte

- 🚩 Emails prétendant venir de votre banque ou de services connus
- 🚩 Demandes urgentes de "confirmer vos informations"
- 🚩 Liens vers des sites qui ressemblent à l'original mais avec des différences subtiles
- 🚩 Pièces jointes non sollicitées
- 🚩 Fautes d'orthographe et de grammaire

#### Que faire ?

1. **Ne cliquez jamais** sur les liens dans les emails suspects
2. **Allez directement** sur le site officiel en tapant l'adresse
3. **Vérifiez l'URL** : HTTPS et domaine correct
4. **Contactez l'entreprise** directement si vous avez un doute

### Téléchargements sécurisés

#### Téléchargez uniquement depuis des sources fiables

- ✅ Dépôts officiels Linux Mint (`apt`, Software Manager)
- ✅ Sites officiels des développeurs
- ✅ GitHub, GitLab pour les logiciels open source
- ❌ Sites de téléchargement tiers
- ❌ Torrents pour les logiciels (sauf distributions Linux)

#### Vérifiez les signatures et checksums

Pour les fichiers ISO ou importants :

```bash
sha256sum fichier_telecharge.iso
```

Comparez avec la somme de contrôle officielle.

---

## 5. Sécurité des emails

### Utiliser le chiffrement des emails

Pour des communications sensibles, utilisez le chiffrement **PGP/GPG**.

#### Installer Thunderbird avec Enigmail

```bash
sudo apt install thunderbird
```

Thunderbird intègre maintenant OpenPGP nativement.

#### Créer une paire de clés

Dans Thunderbird :
1. **Paramètres du compte** → **Chiffrement de bout en bout**
2. **Ajouter une clé** → **Créer une nouvelle clé OpenPGP**

### Ne pas ouvrir les pièces jointes suspectes

#### Pièces jointes dangereuses

Les formats suivants peuvent contenir des malwares :
- ❌ `.exe`, `.bat`, `.cmd`, `.com` (exécutables Windows)
- ❌ `.scr` (économiseurs d'écran)
- ❌ `.vbs`, `.js` (scripts)
- ⚠️ `.zip`, `.rar` contenant des exécutables
- ⚠️ Macros dans les documents Office (`.docm`, `.xlsm`)

#### Bonnes pratiques

1. **N'ouvrez pas** les pièces jointes d'expéditeurs inconnus
2. **Scannez** les fichiers suspects avec ClamAV
3. **Demandez confirmation** à l'expéditeur si le fichier est inattendu

---

## 6. Gestion des données et sauvegardes

### Sauvegarder régulièrement

**La règle 3-2-1** :
- **3** copies de vos données
- **2** supports différents (disque dur + cloud, par exemple)
- **1** copie hors site (cloud, maison d'un ami)

#### Outils de sauvegarde recommandés

1. **Timeshift** : Snapshots système
2. **Déjà Dup** : Sauvegardes de données personnelles
3. **Restic** : Sauvegardes chiffrées et incrémentales

```bash
sudo apt install timeshift
```

Configurez des snapshots quotidiens ou hebdomadaires.

### Chiffrer les données sensibles

Nous l'avons vu dans le chapitre précédent :
- **LUKS** pour le chiffrement complet du disque
- **VeraCrypt** pour des conteneurs portables
- **GPG** pour des fichiers individuels

### Effacement sécurisé

Supprimer un fichier ne l'efface pas vraiment. Pour un effacement définitif :

#### Avec shred

```bash
shred -vfz -n 10 fichier_secret.txt
```

Options :
- `-v` : verbeux
- `-f` : forcer les permissions
- `-z` : ajouter une dernière passe de zéros
- `-n 10` : 10 passes (3 suffisent généralement)

#### Effacer tout un disque

```bash
sudo dd if=/dev/zero of=/dev/sdX bs=1M status=progress
```

Ou pour un effacement plus sécurisé :
```bash
sudo dd if=/dev/urandom of=/dev/sdX bs=1M status=progress
```

> **Attention** : Vérifiez bien le périphérique (`/dev/sdX`) avant de lancer cette commande !

### Limiter les permissions des fichiers

Principe du **moindre privilège** :

```bash
chmod 600 fichier_personnel.txt
chmod 700 dossier_prive/
```

Seul vous pouvez lire/écrire ces fichiers.

---

## 7. Logiciels et applications

### Installer uniquement des logiciels de confiance

#### Sources recommandées (par ordre de préférence)

1. **Dépôts officiels** :
   ```bash
   sudo apt install nom_du_paquet
   ```

2. **Flatpak** (Flathub) :
   ```bash
   flatpak install flathub com.application.Name
   ```

3. **PPA vérifiés** :
   ```bash
   sudo add-apt-repository ppa:nom-officiel/ppa
   ```

4. **Site officiel du développeur** :
   - Vérifiez HTTPS
   - Vérifiez les signatures
   - Préférez les sources (`.deb` officiel)

#### Sources à éviter

- ❌ Sites de téléchargement tiers (download.com, softonic, etc.)
- ❌ PPA de sources inconnues
- ❌ Scripts bash trouvés sur des forums sans comprendre ce qu'ils font
- ❌ Logiciels piratés ou crackés

### Vérifier les signatures des paquets

APT vérifie automatiquement les signatures. Si vous voyez un avertissement :

```
WARNING: The following packages cannot be authenticated!
```

**N'installez pas** le paquet tant que vous n'avez pas résolu le problème.

### Désinstaller les logiciels inutilisés

Moins il y a de logiciels, moins il y a de failles potentielles.

```bash
sudo apt remove nom_du_paquet
sudo apt autoremove
```

### Éviter les logiciels avec des permissions excessives

Certains logiciels demandent des accès inutiles. Soyez vigilant avec :
- Les applications qui demandent l'accès root sans raison
- Les logiciels qui veulent accéder à tout votre système de fichiers
- Les extensions de navigateur avec des permissions étendues

---

## 8. Sécurité physique

### Chiffrer le disque dur

Si votre ordinateur est volé, le chiffrement empêche l'accès à vos données.

- **Chiffrement complet avec LUKS** lors de l'installation
- **Chiffrement de /home** au minimum

### Sécuriser le BIOS/UEFI

1. Accédez au BIOS/UEFI au démarrage (généralement F2, F10, Del)
2. Définissez un **mot de passe administrateur BIOS**
3. Désactivez le boot sur USB/CD si non nécessaire
4. Activez le **Secure Boot** (optionnel, peut poser problème avec certains drivers)

### Verrouiller physiquement l'ordinateur

Pour les laptops :
- Utilisez un **câble antivol Kensington**
- Dans les lieux publics, ne laissez jamais votre ordinateur sans surveillance

### Détruire les anciens disques durs

Avant de jeter ou donner un vieux disque :

```bash
sudo shred -vfz -n 3 /dev/sdX
```

Ou destruction physique (percer, casser les plateaux).

---

## 9. Vie privée et anonymat

### Limiter la collecte de données

#### Désactiver la télémétrie

Linux Mint ne collecte pas de télémétrie par défaut, mais certaines applications le font.

Vérifiez les paramètres de chaque application.

#### Utiliser des moteurs de recherche respectueux

Au lieu de Google :
- **DuckDuckGo** : Ne trace pas, ne profite pas
- **Startpage** : Résultats Google sans le tracking
- **Qwant** : Moteur européen

#### Bloquer les traqueurs

Avec **uBlock Origin** dans Firefox, la plupart des traqueurs sont bloqués.

### Utiliser Tor pour l'anonymat

**Tor Browser** permet une navigation anonyme.

#### Installation

```bash
sudo apt install torbrowser-launcher
```

Lancez `torbrowser-launcher` et suivez les instructions.

#### Quand utiliser Tor ?

- Navigation sensible (journalisme, activisme)
- Contourner la censure
- Protection contre la surveillance de masse

#### Limitations de Tor

- Plus lent que la navigation normale
- Certains sites bloquent Tor
- N'anonymise que la navigation, pas les autres applications

### Attention aux métadonnées

Les photos contiennent des **métadonnées EXIF** (lieu, date, appareil photo).

#### Supprimer les métadonnées

```bash
sudo apt install exiftool
exiftool -all= photo.jpg
```

Ou avec l'interface graphique :
```bash
sudo apt install mat2
mat2 photo.jpg
```

---

## 10. Surveillance et détection

### Surveiller les logs système

Les logs enregistrent tout ce qui se passe sur le système.

#### Logs d'authentification

```bash
sudo tail -f /var/log/auth.log
```

Regardez les tentatives de connexion suspectes.

#### Logs système généraux

```bash
sudo journalctl -xe
```

#### Dernières connexions

```bash
last
```

```bash
lastlog
```

### Détecter les intrusions

#### Vérifier les processus en cours

```bash
top
```

ou mieux :
```bash
htop
```

Cherchez des processus inconnus ou suspects.

#### Vérifier les connexions réseau

```bash
sudo netstat -tulpn
```

ou :
```bash
sudo ss -tulpn
```

#### Installer un IDS (Intrusion Detection System)

Pour les utilisateurs avancés :

```bash
sudo apt install aide
sudo aideinit
```

AIDE détecte les modifications non autorisées de fichiers système.

### Antivirus sous Linux (nécessaire ?)

#### Linux a-t-il besoin d'antivirus ?

**Pour un usage bureau standard : Non**, si vous suivez les bonnes pratiques.

**Oui, si** :
- Vous partagez des fichiers avec des utilisateurs Windows
- Vous gérez un serveur de fichiers
- Vous voulez scanner des pièces jointes email

#### ClamAV (gratuit, open source)

```bash
sudo apt install clamav clamav-daemon
sudo freshclam
```

Scanner un fichier :
```bash
clamscan fichier.zip
```

Scanner un dossier :
```bash
clamscan -r /home/utilisateur/Téléchargements
```

---

## 11. Que faire en cas de compromission ?

### Signes d'une compromission

🚨 **Signes d'alerte** :
- Ralentissements inexpliqués
- Processus inconnus
- Connexions réseau suspectes
- Fichiers modifiés ou supprimés sans raison
- Activité disque/CPU élevée sans raison
- Changements de mots de passe refusés
- Comptes verrouillés

### Procédure d'urgence

#### 1. Déconnectez-vous du réseau

```bash
sudo nmcli networking off
```

Ou débranchez physiquement le câble Ethernet.

#### 2. Changez tous vos mots de passe

**Depuis un autre ordinateur sain** :
- Mot de passe email
- Mot de passe bancaire
- Mots de passe réseaux sociaux
- Tous les comptes importants

#### 3. Examinez les logs

```bash
sudo journalctl -xe
sudo tail -100 /var/log/auth.log
last
```

Notez toute activité suspecte.

#### 4. Analysez le système

```bash
sudo clamscan -r /home
sudo rkhunter --check
```

#### 5. Restaurez depuis une sauvegarde

Si vous avez des snapshots Timeshift :
```bash
sudo timeshift --list
sudo timeshift --restore
```

#### 6. Réinstallez si nécessaire

Dans les cas graves, la réinstallation complète est la seule garantie :
- Sauvegardez vos données personnelles (pas les exécutables !)
- Réinstallez Linux Mint
- Restaurez uniquement vos documents (après vérification)

#### 7. Informez les autorités si nécessaire

Pour le vol de données bancaires, l'usurpation d'identité, etc.

---

## 12. Checklist des bonnes pratiques

### Quotidien

- [ ] Verrouiller l'écran avant de quitter le poste (`Ctrl + Alt + L`)
- [ ] Ne pas cliquer sur des liens suspects
- [ ] Vérifier les URL avant de saisir des informations sensibles
- [ ] Utiliser des mots de passe uniques et forts

### Hebdomadaire

- [ ] Installer les mises à jour de sécurité
  ```bash
  sudo apt update && sudo apt upgrade
  ```
- [ ] Vérifier les logs d'authentification
  ```bash
  sudo tail -50 /var/log/auth.log
  ```
- [ ] Sauvegarder les données importantes

### Mensuel

- [ ] Vérifier la liste des comptes utilisateurs
  ```bash
  cat /etc/passwd
  ```
- [ ] Vérifier les processus et connexions réseau
  ```bash
  sudo netstat -tulpn
  ```
- [ ] Nettoyer le système
  ```bash
  sudo apt autoremove && sudo apt autoclean
  ```
- [ ] Réviser les groupes et permissions importants
- [ ] Tester la restauration d'une sauvegarde

### Annuel

- [ ] Changer les mots de passe principaux
- [ ] Auditer les logiciels installés (supprimer l'inutile)
- [ ] Réviser la configuration du pare-feu
- [ ] Vérifier les sauvegardes hors site
- [ ] Mettre à jour le firmware BIOS/UEFI
- [ ] Réviser les clés SSH et certificats

---

## 13. Ressources et outils de sécurité

### Outils recommandés

| Outil | Usage |
|-------|-------|
| **UFW/GUFW** | Pare-feu |
| **Fail2Ban** | Protection contre les attaques par force brute |
| **ClamAV** | Antivirus |
| **rkhunter** | Détection de rootkits |
| **Timeshift** | Snapshots système |
| **KeePassXC** | Gestionnaire de mots de passe |
| **VeraCrypt** | Chiffrement de fichiers |
| **Tor Browser** | Navigation anonyme |
| **BleachBit** | Nettoyage système |

### Installation rapide des outils de base

```bash
sudo apt install ufw gufw fail2ban clamav rkhunter timeshift keepassxc
```

### Ressources en ligne

#### Documentation officielle

- **Linux Mint Forums** : https://forums.linuxmint.com
- **Linux Mint Blog** : https://blog.linuxmint.com

#### Sécurité générale

- **ANSSI** (France) : Guides de sécurité
- **CERT-FR** : Alertes de sécurité
- **CVE Details** : Base de données des vulnérabilités

#### Veille sécurité

- **The Hacker News**
- **Krebs on Security**
- **Ars Technica - Security**

---

## 14. Mythes et idées reçues

### ❌ "Linux n'a pas de virus, je n'ai rien à craindre"

**Faux**. Linux a moins de malwares, mais :
- Les malwares Linux existent (rootkits, cryptominers, etc.)
- Vos comportements restent le principal risque
- Les attaques ciblées peuvent toucher n'importe quel système

### ❌ "Un antivirus me protège complètement"

**Faux**. Un antivirus est un outil parmi d'autres :
- Il ne détecte pas tout (zero-day, nouvelles menaces)
- Il ne remplace pas les bonnes pratiques
- Il ne protège pas contre le phishing, l'ingénierie sociale, etc.

### ❌ "Je n'ai rien à cacher, je n'ai pas besoin de sécurité"

**Faux**. Même si vous pensez n'avoir rien à cacher :
- Vol d'identité
- Utilisation de vos ressources (botnet, cryptominage)
- Accès à vos comptes bancaires
- Usurpation de votre identité pour attaquer d'autres personnes

### ❌ "C'est compliqué, je ne peux pas être sécurisé"

**Faux**. Les bases sont simples :
- Mots de passe forts et uniques
- Mises à jour régulières
- Ne pas cliquer sur n'importe quoi
- Sauvegardes régulières

Ces 4 règles couvrent 90% de la sécurité quotidienne.

### ❌ "Si je suis attaqué, je le saurai tout de suite"

**Faux**. Les attaques les plus réussies sont discrètes :
- Rootkits cachés
- Keyloggers silencieux
- Vol progressif de données
- Backdoors dormantes

D'où l'importance de surveiller régulièrement les logs.

---

## 15. Sécurité pour différents profils

### Utilisateur basique (navigation, bureautique)

**Essentiels** :
- ✅ Mises à jour automatiques activées
- ✅ Pare-feu UFW activé
- ✅ Mot de passe fort
- ✅ Verrouillage automatique après 10 min
- ✅ Sauvegardes hebdomadaires avec Timeshift
- ✅ uBlock Origin sur Firefox

### Utilisateur avancé (développement, serveurs)

**En plus des essentiels** :
- ✅ Clés SSH au lieu de mots de passe
- ✅ Fail2Ban sur les serveurs
- ✅ Chiffrement complet du disque (LUKS)
- ✅ Surveillance des logs quotidienne
- ✅ IDS (AIDE ou Tripwire)
- ✅ VPN pour les connexions publiques

### Utilisateur parano... euh, très prudent

**En plus de tout le reste** :
- ✅ Navigation principale via Tor
- ✅ Aucune connexion automatique
- ✅ 2FA partout où possible
- ✅ Séparation stricte des usages (VMs, conteneurs)
- ✅ Suppression sécurisée systématique (shred)
- ✅ Vérification manuelle des signatures de paquets
- ✅ Réseau séparé pour les appareils IoT

---

## Résumé

La sécurité repose sur **plusieurs couches de protection** :

### Les 5 piliers de la sécurité

1. **Mises à jour** : Système et applications toujours à jour
2. **Authentification forte** : Mots de passe robustes + 2FA
3. **Contrôle d'accès** : Permissions appropriées, pare-feu actif
4. **Sauvegardes** : Copies multiples, testées régulièrement
5. **Vigilance** : Comportement prudent, méfiance des sources inconnues

### La règle d'or

> **"La sécurité est un processus, pas un produit"** - Bruce Schneier

C'est un ensemble d'habitudes quotidiennes, pas une configuration qu'on met en place une fois pour toutes.

### L'essentiel à retenir

Si vous ne deviez retenir que 5 choses :

1. 🔒 **Mots de passe forts et uniques partout** (avec un gestionnaire)
2. 🔄 **Mettez à jour régulièrement** (au moins hebdomadaire)
3. 🛡️ **Pare-feu activé** (UFW est déjà installé)
4. 💾 **Sauvegardez** (règle 3-2-1)
5. 🧠 **Réfléchissez avant de cliquer** (phishing, liens suspects)

Avec ces 5 pratiques, vous êtes déjà bien plus en sécurité que 90% des utilisateurs.

---


⏭️ [Antivirus sous Linux (ClamAV - nécessaire ?)](/11-gestion-des-utilisateurs-et-securite/06-antivirus-sous-linux.md)
