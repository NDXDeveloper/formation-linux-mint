🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 12.3 Gestion de l'imprimante et du scanner

## Introduction

L'impression et la numérisation sont des tâches courantes qui fonctionnent généralement très bien sous Linux Mint. Grâce aux progrès récents, la plupart des imprimantes modernes sont **détectées et configurées automatiquement**, sans intervention de votre part.

Ce chapitre vous guide dans la configuration et l'utilisation d'imprimantes et de scanners sous Linux Mint.

---

## CUPS : Le système d'impression de Linux

### Qu'est-ce que CUPS ?

**CUPS** (Common UNIX Printing System) est le système d'impression utilisé par Linux Mint et la plupart des distributions Linux.

**Analogie simple :**
CUPS est comme un **chef d'orchestre** qui :
- Reçoit vos demandes d'impression
- Traduit vos documents dans un langage que l'imprimante comprend
- Gère la file d'attente d'impression
- Communique avec l'imprimante (USB, réseau, WiFi)

**Avantages de CUPS :**
- ✅ Installé et actif par défaut sur Linux Mint
- ✅ Support de milliers de modèles d'imprimantes
- ✅ Gestion avancée des files d'attente
- ✅ Interface web pour la configuration
- ✅ Support de l'impression réseau

### Les pilotes d'imprimante

Linux Mint inclut des pilotes pour la plupart des imprimantes courantes :

#### Pilotes intégrés (recommandés)
- **Inclus dans CUPS** par défaut
- Couvrent les imprimantes HP, Canon, Epson, Brother, etc.
- Aucune installation nécessaire dans la plupart des cas

#### HPLIP (HP Linux Imaging and Printing)
- Pilotes officiels **HP**
- Excellente qualité et compatibilité
- Pré-installés sur Linux Mint
- Support des imprimantes et scanners HP

#### Gutenprint
- Pilotes open source de haute qualité
- Excellents pour Canon et Epson
- Alternative aux pilotes propriétaires

#### Pilotes propriétaires des fabricants
- Parfois nécessaires pour les modèles professionnels
- Disponibles sur les sites des fabricants
- Installation manuelle généralement requise

---

## Connecter et configurer une imprimante

### Imprimante USB

La connexion d'une imprimante USB est généralement **automatique** et **sans effort**.

#### Procédure standard

1. **Branchez** l'imprimante via USB
2. **Allumez** l'imprimante
3. **Attendez quelques secondes** : Linux Mint détecte automatiquement l'imprimante
4. Une **notification** apparaît : "Nouvelle imprimante détectée"
5. Le système **installe automatiquement** les pilotes
6. L'imprimante est **prête à l'emploi** !

#### Vérification

Pour vérifier que votre imprimante est bien installée :

**Méthode 1 : Interface graphique**
1. Ouvrez le **Menu** → **Préférences** → **Imprimantes**
2. Vous devriez voir votre imprimante dans la liste
3. Une coche verte indique qu'elle est prête

**Méthode 2 : Page de test**
1. Dans **Imprimantes**, faites un clic droit sur votre imprimante
2. Sélectionnez "**Propriétés**"
3. Cliquez sur "**Imprimer une page de test**"
4. Une page devrait s'imprimer avec des informations de diagnostic

### Imprimante réseau (WiFi/Ethernet)

Les imprimantes réseau nécessitent quelques étapes supplémentaires.

#### Prérequis

1. L'imprimante doit être **connectée au réseau** (WiFi ou Ethernet)
2. L'imprimante et l'ordinateur doivent être sur le **même réseau local**
3. Notez **l'adresse IP** de l'imprimante (visible sur l'écran de l'imprimante ou dans son interface web)

#### Ajout automatique d'une imprimante réseau

**Méthode recommandée :**

1. Ouvrez **Menu** → **Préférences** → **Imprimantes**
2. Cliquez sur "**Ajouter**" (bouton +)
3. Le système **recherche automatiquement** les imprimantes réseau
4. Sélectionnez votre imprimante dans la liste détectée
5. Cliquez sur "**Suivant**"
6. Le système télécharge et installe automatiquement le pilote
7. Donnez un nom à l'imprimante (ou gardez le nom par défaut)
8. Cliquez sur "**Appliquer**"
9. Imprimez une page de test pour vérifier

#### Ajout manuel d'une imprimante réseau

Si la détection automatique échoue :

1. Dans **Imprimantes**, cliquez sur "**Ajouter**"
2. Sélectionnez "**Imprimante réseau**"
3. Choisissez le protocole :
   - **AppSocket/HP JetDirect** (port 9100) - recommandé pour la plupart
   - **LPD/LPR** (port 515)
   - **IPP** (Internet Printing Protocol)
4. Entrez **l'adresse IP** de l'imprimante
   - Exemple : `192.168.1.100`
5. Sélectionnez le **pilote approprié** dans la liste
6. Configurez les options et cliquez sur "**Appliquer**"

### Imprimante partagée Windows (Samba)

Vous pouvez utiliser une imprimante connectée à un PC Windows.

#### Configuration

1. Dans **Imprimantes**, cliquez sur "**Ajouter**"
2. Sélectionnez "**Imprimante réseau**" → "**Windows Printer via SAMBA**"
3. Entrez l'adresse au format : `smb://ORDINATEUR-WINDOWS/NOM-IMPRIMANTE`
   - Exemple : `smb://PC-Bureau/HP-LaserJet`
4. Entrez le **nom d'utilisateur** et le **mot de passe** Windows si nécessaire
5. Sélectionnez le pilote
6. Appliquer et tester

---

## Interface de gestion des imprimantes

### L'application Imprimantes

**Accès :** Menu → Préférences → Imprimantes

**Fonctionnalités principales :**

#### Vue d'ensemble
- Liste de toutes les imprimantes installées
- Statut de chaque imprimante (prête, en pause, erreur)
- Imprimante par défaut (marquée d'une coche verte)

#### Propriétés de l'imprimante (clic droit → Propriétés)

**Onglet Paramètres :**
- Modifier le nom de l'imprimante
- Ajouter une description ou un emplacement
- Activer/désactiver le partage réseau
- Définir comme imprimante par défaut

**Onglet Stratégies :**
- Gestion des erreurs d'impression
- Comportement en cas de problème
- File d'attente

**Onglet Options de l'imprimante :**
- Qualité d'impression (brouillon, normale, haute)
- Type de papier (A4, Lettre, Enveloppe, etc.)
- Source du papier (bac 1, bac 2, alimentation manuelle)
- Impression recto-verso (si supportée)
- Couleur ou noir et blanc

**Onglet Tâches d'impression :**
- Voir la file d'attente actuelle
- Annuler, suspendre ou relancer des impressions
- Ordre de priorité

#### Actions rapides (clic droit sur l'imprimante)
- **Imprimer une page de test** : Vérifie le fonctionnement
- **Pause** : Met en pause toutes les impressions
- **Définir comme imprimante par défaut**
- **Propriétés** : Configuration avancée
- **Supprimer** : Retirer l'imprimante du système

### Interface web CUPS (avancé)

Pour les utilisateurs plus expérimentés, CUPS propose une interface web complète.

**Accès :**
1. Ouvrez votre navigateur web
2. Allez à l'adresse : `http://localhost:631`
3. Vous accédez à l'interface d'administration CUPS

**Fonctionnalités avancées :**
- Configuration détaillée des imprimantes
- Gestion des pilotes
- Journaux d'impression
- Configuration du serveur d'impression
- Partage d'imprimantes sur le réseau

> **Note** : Pour modifier les paramètres dans l'interface web, vous devrez vous authentifier avec votre nom d'utilisateur et mot de passe Linux.

---

## Imprimer un document

### Depuis une application

L'impression depuis une application est standardisée sous Linux.

#### Procédure générale

1. Ouvrez votre document (LibreOffice, Firefox, etc.)
2. Allez dans **Fichier** → **Imprimer** (ou **Ctrl + P**)
3. Une boîte de dialogue d'impression s'affiche

**Options courantes :**
- **Imprimante** : Sélectionnez l'imprimante à utiliser
- **Pages** : Toutes, actuelle, ou intervalle (ex: 1-5, 8, 10-12)
- **Copies** : Nombre d'exemplaires
- **Orientation** : Portrait ou paysage
- **Mise en page** : 1, 2, 4 pages par feuille
- **Recto-verso** : Si votre imprimante le supporte
- **Couleur** : Couleur ou niveaux de gris

4. Cliquez sur "**Imprimer**"

### Depuis le gestionnaire de fichiers

Vous pouvez imprimer directement des fichiers PDF, images, etc.

1. **Clic droit** sur le fichier
2. Sélectionnez "**Imprimer**" ou "**Ouvrir avec** → Application d'impression"
3. Configurez les options
4. Imprimez

### Impression en ligne de commande

Pour les utilisateurs avancés :

```bash
# Imprimer un fichier PDF
lp fichier.pdf

# Imprimer sur une imprimante spécifique
lp -d HP-LaserJet fichier.pdf

# Imprimer plusieurs copies
lp -n 3 fichier.pdf

# Imprimer des pages spécifiques
lp -P 1-5,8 fichier.pdf

# Liste des imprimantes
lpstat -p -d
```

---

## Gestion de la file d'attente

### Voir les tâches en attente

**Interface graphique :**
1. Ouvrez **Imprimantes**
2. Double-cliquez sur une imprimante
3. Vous voyez toutes les **tâches d'impression en cours ou en attente**

**Informations affichées :**
- Nom du document
- Utilisateur
- Taille du fichier
- Statut (en cours, en attente, arrêtée)
- Progression

### Annuler une impression

**Méthode 1 : Interface graphique**
1. Dans la liste des tâches
2. **Clic droit** sur la tâche à annuler
3. Sélectionnez "**Annuler**"

**Méthode 2 : Ligne de commande**
```bash
# Annuler une tâche spécifique
cancel 123  # Remplacez 123 par l'ID de la tâche

# Annuler toutes les tâches
cancel -a
```

### Suspendre/reprendre des impressions

**Suspendre temporairement :**
- Clic droit sur la tâche → "**Mettre en pause**"
- Utile si vous devez ajouter du papier ou changer de bac

**Reprendre :**
- Clic droit → "**Reprendre**"

---

## Imprimantes HP : Configuration HPLIP

Les imprimantes HP bénéficient d'un excellent support sous Linux grâce à **HPLIP**.

### Installation de HPLIP

HPLIP est généralement pré-installé sur Linux Mint. Sinon :

```bash
sudo apt update
sudo apt install hplip hplip-gui
```

### HP Device Manager (outil graphique)

**Accès :** Menu → **Système HP Device Manager**
Ou via terminal : `hp-toolbox`

**Fonctionnalités :**
- ✅ Détection automatique des imprimantes HP
- ✅ Configuration guidée
- ✅ Vérification des niveaux d'encre/toner
- ✅ Nettoyage des têtes d'impression
- ✅ Alignement des cartouches
- ✅ Configuration du scanner (si intégré)
- ✅ Diagnostic et résolution de problèmes
- ✅ Mises à jour du firmware

### Assistant de configuration HP

Pour ajouter une imprimante HP :

```bash
hp-setup
```

Cet assistant détecte automatiquement votre imprimante HP (USB ou réseau) et installe le pilote approprié.

### Vérifier les niveaux d'encre HP

**Graphiquement :**
1. Ouvrez **HP Device Manager**
2. Sélectionnez votre imprimante
3. L'onglet "**Fournitures**" affiche les niveaux d'encre/toner

**En ligne de commande :**
```bash
hp-levels
```

---

## Scanners sous Linux

### SANE : Le système de numérisation

**SANE** (Scanner Access Now Easy) est l'équivalent de CUPS pour les scanners.

**Caractéristiques :**
- Support de centaines de modèles de scanners
- Intégré à Linux Mint
- Fonctionne avec les scanners USB et réseau
- Compatible avec les multifonctions (imprimante + scanner)

### Détecter un scanner

#### Connexion USB

1. **Branchez** le scanner
2. **Allumez-le**
3. Le système détecte automatiquement le scanner

#### Vérification de la détection

```bash
# Lister les scanners détectés
scanimage -L
```

**Exemple de sortie :**
```
device `hpaio:/usb/HP_LaserJet_MFP_M227fdw?serial=ABC123' is a Hewlett-Packard HP_LaserJet_MFP_M227fdw all-in-one
```

Si votre scanner apparaît, il est prêt à l'emploi !

### Application de numérisation : Simple Scan

**Simple Scan** est l'application de numérisation par défaut de Linux Mint.

**Accès :** Menu → Graphisme → **Document Scanner** (ou Simple Scan)

#### Interface de Simple Scan

**Éléments principaux :**
- **Barre d'outils** : Numériser, Enregistrer, Paramètres
- **Zone de prévisualisation** : Affiche le document numérisé
- **Options de numérisation** : Type de document, résolution, source

#### Numériser un document

**Procédure complète :**

1. **Placez** votre document sur le scanner
2. Ouvrez **Simple Scan**
3. Sélectionnez le **type de document** :
   - **Texte** : Pour des documents avec beaucoup de texte (utilise l'OCR)
   - **Photo** : Pour des photographies (couleurs optimisées)
4. Choisissez la **résolution** :
   - **75-150 DPI** : Documents texte pour visualisation écran
   - **300 DPI** : Standard pour documents et photos (recommandé)
   - **600 DPI ou plus** : Photos de haute qualité ou documents à agrandir
5. Sélectionnez la **source** :
   - **Vitre d'exposition** (Flatbed) : Pour documents individuels
   - **Chargeur automatique** (ADF) : Pour lots de documents (si disponible)
6. Cliquez sur "**Numériser**"
7. Le scanner effectue la numérisation
8. L'image apparaît dans Simple Scan

#### Options avancées

**Après numérisation :**
- **Rotation** : Faire pivoter la page (90°, 180°, 270°)
- **Recadrage** : Sélectionner une zone spécifique
- **Réorganisation** : Changer l'ordre des pages
- **Suppression** : Retirer des pages indésirables

#### Enregistrer le document numérisé

1. Cliquez sur "**Enregistrer**" ou **Ctrl + S**
2. Choisissez le **format** :
   - **PDF** : Recommandé pour documents texte multi-pages
   - **JPEG** : Pour photos ou images uniques
   - **PNG** : Pour images nécessitant transparence ou qualité maximale
   - **TIFF** : Format professionnel sans perte
3. Donnez un nom au fichier
4. Sélectionnez l'emplacement
5. Cliquez sur "**Enregistrer**"

### XSane : Alternative avancée

Pour des fonctionnalités plus poussées, **XSane** est une alternative puissante.

**Installation :**
```bash
sudo apt install xsane
```

**Accès :** Menu → Graphisme → **XSane Image Scanner**

**Fonctionnalités avancées :**
- Prévisualisation détaillée avec zones de sélection
- Ajustement fin de la luminosité, contraste, gamma
- Modes de couleur avancés (RVB, Niveaux de gris, Lineart)
- Réglages par canal de couleur
- Correction automatique de l'inclinaison
- Envoi direct par email
- OCR (reconnaissance de caractères)

> **Note** : XSane est plus complexe mais offre un contrôle total pour les utilisateurs exigeants.

### Scanners réseau

Pour utiliser un scanner multifonction en réseau :

**Configuration :**
1. Ouvrez le **Menu** → **Préférences** → **Imprimantes**
2. Ajoutez l'imprimante/scanner réseau (voir section précédente)
3. Le scanner sera automatiquement détecté avec l'imprimante

**Vérification :**
```bash
scanimage -L
```

Le scanner réseau devrait apparaître dans la liste.

---

## Problèmes courants et solutions

### L'imprimante n'imprime pas

#### Vérifications de base

1. **L'imprimante est-elle allumée ?**
   - Vérifiez le bouton d'alimentation
   - Certains modèles ont un mode veille profond

2. **Câble USB bien connecté ?**
   - Débranchez et rebranchez le câble
   - Testez un autre port USB
   - Essayez un autre câble USB

3. **Papier chargé ?**
   - Vérifiez le bac à papier
   - Assurez-vous qu'il n'y a pas de bourrage

4. **Encre/Toner suffisant ?**
   - Vérifiez les niveaux via HP Device Manager ou l'écran de l'imprimante

5. **Imprimante sélectionnée correctement ?**
   - Dans la boîte d'impression, vérifiez quelle imprimante est choisie

6. **File d'attente bloquée ?**
   - Ouvrez **Imprimantes**
   - Vérifiez si des tâches sont en erreur
   - Annulez les tâches problématiques

#### Solutions logicielles

**Redémarrer le service d'impression :**
```bash
sudo systemctl restart cups
```

**Réinitialiser CUPS :**
```bash
sudo systemctl stop cups
sudo rm /var/cache/cups/* -rf
sudo systemctl start cups
```

**Réinstaller le pilote :**
1. Supprimez l'imprimante dans **Imprimantes**
2. Redémarrez l'ordinateur
3. Reconnectez l'imprimante
4. Laissez le système la détecter automatiquement

### Qualité d'impression médiocre

#### Causes et solutions

**Lignes manquantes ou bavures :**
- **Cause** : Têtes d'impression sales (jet d'encre)
- **Solution** : Nettoyage des têtes via HP Device Manager ou le panneau de l'imprimante

**Texte flou ou pâle :**
- **Cause** : Encre faible ou mode brouillon
- **Solution** :
  - Vérifiez les niveaux d'encre
  - Changez la qualité d'impression en "Normale" ou "Haute"

**Couleurs incorrectes :**
- **Cause** : Cartouches vides ou désalignées
- **Solution** :
  - Remplacez les cartouches vides
  - Effectuez un alignement des têtes

**Traînées noires (laser) :**
- **Cause** : Tambour sale
- **Solution** : Nettoyage du tambour (voir manuel de l'imprimante)

### Le scanner n'est pas détecté

#### Diagnostic

```bash
# Vérifier si SANE détecte le scanner
scanimage -L

# Si rien n'apparaît, vérifier les permissions
ls -l /dev/bus/usb/*/*
```

#### Solutions

**Ajouter l'utilisateur au groupe scanner :**
```bash
sudo usermod -a -G scanner $USER
sudo usermod -a -G lp $USER
```

Déconnectez-vous et reconnectez-vous pour que les changements prennent effet.

**Réinitialiser les règles USB :**
```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

**Installer les pilotes supplémentaires :**

Pour scanners HP :
```bash
sudo apt install libsane-hpaio
```

Pour scanners Epson :
```bash
sudo apt install iscan
```

**Redémarrer le service SANE :**
```bash
sudo systemctl restart saned
```

### Impression réseau lente

**Causes possibles :**
- Connexion WiFi instable
- Résolution d'impression trop élevée
- Spooler surchargé

**Solutions :**
1. Utilisez une connexion Ethernet si possible
2. Réduisez la résolution d'impression (de 1200 à 600 DPI)
3. Passez en mode "Brouillon" pour documents non importants
4. Videz la file d'attente régulièrement

### Messages d'erreur courants

#### "Imprimante occupée"
- **Cause** : Tâche précédente bloquée
- **Solution** : Annulez toutes les tâches en attente, redémarrez l'imprimante

#### "Aucune imprimante par défaut"
- **Cause** : Pas d'imprimante définie par défaut
- **Solution** : Clic droit sur votre imprimante → Définir comme imprimante par défaut

#### "Erreur de communication"
- **Cause** : Problème réseau ou USB
- **Solution** : Vérifiez les connexions, redémarrez l'imprimante et CUPS

#### "Pilote non disponible"
- **Cause** : Pilote manquant ou corrompu
- **Solution** : Réinstallez l'imprimante avec le bon pilote

---

## Impression avancée

### Impression recto-verso (duplex)

Si votre imprimante supporte le recto-verso automatique :

**Configuration dans les propriétés de l'imprimante :**
1. Imprimantes → Clic droit sur l'imprimante → Propriétés
2. Onglet "**Options de l'imprimante**"
3. Recherchez "**Recto-verso**" ou "**Duplex**"
4. Sélectionnez :
   - **Bord long** (reliure verticale - pour documents)
   - **Bord court** (reliure horizontale - pour brochures)

**Pour impression manuelle recto-verso :**
1. Imprimez d'abord les pages impaires
2. Retournez la pile de papier
3. Réinsérez dans l'imprimante
4. Imprimez les pages paires

### Impression de brochures

LibreOffice permet de créer facilement des brochures :

1. Fichier → Imprimer
2. Onglet "**Général**"
3. Dans "**Mise en page**", sélectionnez "**Brochure**"
4. Configurez :
   - Inclure : Toutes les pages / Pages impaires / Pages paires
   - Recto-verso selon votre imprimante
5. Imprimez

### Impression sécurisée (avec code PIN)

Certaines imprimantes professionnelles supportent l'impression sécurisée :

1. Dans la boîte d'impression, recherchez "**Impression sécurisée**" ou "**PIN Printing**"
2. Activez l'option
3. Définissez un code PIN
4. Le document sera stocké dans l'imprimante
5. Saisissez le PIN sur le panneau de l'imprimante pour libérer l'impression

### Partage d'imprimante sur le réseau

Pour partager votre imprimante avec d'autres ordinateurs :

**Configuration sur l'ordinateur hôte :**
1. Imprimantes → Clic droit → Propriétés → Onglet "**Stratégies**"
2. Cochez "**Partagée**"
3. Donnez un nom de partage simple (ex: "HP-Partage")

**Configuration sur les ordinateurs clients :**
1. Ajoutez une nouvelle imprimante
2. Sélectionnez "**Imprimante réseau**"
3. Type : "**IPP**"
4. Adresse : `ipp://IP-ORDINATEUR-HOTE:631/printers/HP-Partage`
5. Appliquez

> **Note** : Assurez-vous que le pare-feu autorise CUPS (port 631).

---

## Applications tierces utiles

### Pour l'impression

#### CUPS-PDF (imprimante virtuelle PDF)

Créez des PDF directement depuis n'importe quelle application :

**Installation :**
```bash
sudo apt install cups-pdf
```

**Utilisation :**
1. Dans n'importe quelle application, faites "**Imprimer**"
2. Sélectionnez l'imprimante "**PDF**"
3. Imprimez
4. Le PDF est créé dans `~/PDF/` ou `~/Documents/`

Très utile pour :
- Sauvegarder des pages web en PDF
- Créer des PDF depuis LibreOffice
- "Imprimer" des emails en PDF

### Pour la numérisation

#### gscan2pdf (PDF multi-pages depuis scanner)

Excellent pour numériser des documents de plusieurs pages :

**Installation :**
```bash
sudo apt install gscan2pdf
```

**Fonctionnalités :**
- Numérisation de lots de documents
- OCR (reconnaissance de texte)
- Rotation automatique
- Exportation en PDF multi-pages
- Compression optimisée

#### OCRFeeder (reconnaissance de texte avancée)

Pour extraire du texte de documents scannés :

**Installation :**
```bash
sudo apt install ocrfeeder tesseract-ocr-fra
```

**Usage :**
- Numérisez votre document
- OCRFeeder analyse la mise en page
- Extrait le texte
- Exporte en ODT, PDF ou HTML

---

## Conseils et bonnes pratiques

### Pour l'impression

✅ **À faire :**
- Utiliser le mode "Brouillon" pour impressions de test
- Vérifier l'aperçu avant impression (économie papier/encre)
- Imprimer en recto-verso quand possible
- Imprimer plusieurs pages par feuille pour révisions
- Entretenir régulièrement l'imprimante (nettoyage têtes)

❌ **À éviter :**
- Laisser l'imprimante éteinte trop longtemps (têtes sèchent)
- Utiliser des cartouches non adaptées
- Imprimer avec encre très faible (endommage têtes)
- Ignorer les messages d'erreur de l'imprimante

### Pour la numérisation

✅ **À faire :**
- Nettoyer la vitre régulièrement (évite traces)
- Utiliser 300 DPI pour documents standards
- Scanner en noir et blanc les documents texte (fichiers plus légers)
- Utiliser l'OCR pour documents que vous devrez modifier

❌ **À éviter :**
- Scanner à très haute résolution inutilement (fichiers énormes)
- Oublier de vérifier l'aperçu (évite re-scans)

### Maintenance préventive

**Imprimantes jet d'encre :**
- Imprimez au moins une page par semaine (évite têtes bouchées)
- Effectuez le nettoyage automatique mensuel
- Stockez les cartouches à température ambiante

**Imprimantes laser :**
- Nettoyez le tambour selon le manuel
- Remplacez les toners avant qu'ils soient complètement vides
- Dépoussiérez l'intérieur occasionnellement

---

## Ressources et commandes utiles

### Commandes de diagnostic

```bash
# Statut général de CUPS
lpstat -t

# Voir les imprimantes et leur statut
lpstat -p -d

# Voir les tâches d'impression
lpstat -o

# Historique des impressions
ls /var/spool/cups/

# Logs CUPS (erreurs)
sudo tail -f /var/log/cups/error_log

# Scanner les périphériques détectés
sudo lsusb
sudo lspci | grep -i print

# Tester le pilote d'une imprimante
lpadmin -p NOM-IMPRIMANTE -o printer-info="Test"
```

### Fichiers de configuration importants

```bash
# Configuration principale CUPS
/etc/cups/cupsd.conf

# Imprimantes configurées
/etc/cups/printers.conf

# Pilotes disponibles
/usr/share/cups/model/

# File d'attente temporaire
/var/spool/cups/
```

### Documentation et aide

**Documentation officielle :**
- CUPS : https://www.cups.org/documentation.html
- SANE : http://www.sane-project.org/
- HPLIP : https://developers.hp.com/hp-linux-imaging-and-printing

**Forums :**
- Forums Linux Mint (français et anglais)
- Ask Ubuntu (solutions souvent compatibles)

**Aide en ligne de commande :**
```bash
man cups
man lp
man scanimage
man hp-setup
```

---

## Conclusion

La gestion des imprimantes et scanners sous Linux Mint est devenue **extrêmement simple** grâce à CUPS et SANE. La plupart du matériel fonctionne **immédiatement** sans configuration particulière.

**Points clés à retenir :**

✅ **Imprimantes :**
- La majorité sont détectées et configurées automatiquement
- Les imprimantes HP ont un excellent support via HPLIP
- L'interface graphique est intuitive et complète
- Le partage réseau est simple à mettre en place

✅ **Scanners :**
- Simple Scan suffit pour la plupart des besoins
- XSane offre des fonctionnalités avancées
- L'OCR est disponible pour extraire du texte

✅ **En cas de problème :**
- Redémarrer CUPS résout souvent les soucis
- La communauté Linux offre une aide précieuse
- La documentation est riche et accessible

Avec ces connaissances, vous êtes parfaitement équipé pour imprimer et numériser efficacement sous Linux Mint !

Dans le prochain chapitre, nous aborderons la **gestion des périphériques USB et Bluetooth**.

⏭️ [Périphériques USB et Bluetooth](/12-materiel-et-pilotes/04-peripheriques-usb-et-bluetooth.md)
