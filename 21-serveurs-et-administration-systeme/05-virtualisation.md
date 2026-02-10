🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 21.5 Virtualisation (VirtualBox, KVM/QEMU)

## Introduction

### Qu'est-ce que la virtualisation ?

La virtualisation permet de faire fonctionner un système d'exploitation complet (Windows, Linux, macOS, etc.) **à l'intérieur** de votre système d'exploitation actuel, comme une application normale. Ce système invité s'appelle une **machine virtuelle** (VM).

**En termes simples :** Imaginez pouvoir lancer Windows 11 dans une fenêtre sur votre Linux Mint, ou tester Ubuntu Server sans toucher à votre installation principale. C'est exactement ce que permet la virtualisation !

### Pourquoi utiliser la virtualisation ?

- **Tester d'autres systèmes** : Essayer Windows, macOS, ou d'autres distributions Linux sans risque
- **Développement** : Créer des environnements de test isolés
- **Logiciels spécifiques** : Utiliser des applications qui ne fonctionnent que sur Windows
- **Formation** : Apprendre l'administration système en toute sécurité
- **Serveurs** : Héberger plusieurs serveurs sur une seule machine
- **Sécurité** : Isoler des applications potentiellement dangereuses
- **Snapshots** : Sauvegarder l'état complet d'un système et y revenir instantanément

### Cas d'usage concrets

- Utiliser Microsoft Office dans Windows sur votre Linux
- Tester une nouvelle distribution Linux avant de l'installer
- Créer un environnement de développement reproductible
- Simuler un réseau de plusieurs serveurs
- Apprendre la cybersécurité dans un environnement isolé
- Exécuter d'anciennes versions de logiciels

---

## VirtualBox vs KVM/QEMU

### VirtualBox

**Type :** Hyperviseur de type 2 (s'exécute comme une application)

**Avantages :**
- Interface graphique très intuitive
- Facile à installer et configurer
- Excellent pour les débutants
- Fonctionnalités riches (snapshots, clonage, partage de fichiers)
- Support USB complet
- Compatible Windows, macOS, Linux
- Gratuit et open source (édition de base)

**Inconvénients :**
- Moins performant que KVM
- Consomme plus de ressources
- Oracle (propriétaire) contrôle le développement
- Extensions propriétaires pour certaines fonctionnalités

**Idéal pour :** Débutants, tests occasionnels, usage desktop

### KVM/QEMU

**Type :** Hyperviseur de type 1 (intégré au noyau Linux)

**Avantages :**
- Performances natives (presque aussi rapide que le système hôte)
- Intégré au noyau Linux
- Très léger en ressources
- Open source complet
- Idéal pour serveurs et production
- Support matériel excellent

**Inconvénients :**
- Configuration plus technique
- Interface graphique moins intuitive (virt-manager)
- Courbe d'apprentissage plus élevée
- Moins de fonctionnalités "clé en main"

**Idéal pour :** Utilisateurs avancés, serveurs, performances maximales

### Tableau comparatif

| Critère | VirtualBox | KVM/QEMU |
|---------|------------|----------|
| **Facilité d'utilisation** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Performances** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Interface graphique** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Consommation ressources** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Configuration requise** | Faible | Moyenne |
| **Open Source** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Support USB** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Snapshots** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |

### Lequel choisir ?

**Choisissez VirtualBox si :**
- Vous débutez avec la virtualisation
- Vous voulez une interface simple et intuitive
- Vous testez occasionnellement des systèmes
- Vous avez besoin de fonctionnalités USB avancées
- Vous voulez des snapshots faciles à gérer

**Choisissez KVM/QEMU si :**
- Vous recherchez les meilleures performances
- Vous créez des serveurs virtuels
- Vous êtes à l'aise en ligne de commande
- Vous préférez l'open source complet
- Vous gérez plusieurs VMs en production

**Bonne nouvelle :** Vous pouvez installer les deux !

---

## Prérequis matériels

### Vérifier le support de virtualisation

Votre processeur doit supporter la virtualisation matérielle (Intel VT-x ou AMD-V).

Vérifiez :

```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
```

- **Si résultat > 0 :** ✅ Virtualisation supportée
- **Si résultat = 0 :** ❌ Virtualisation non supportée ou désactivée dans le BIOS

### Activer la virtualisation dans le BIOS/UEFI

Si la commande renvoie 0 :

1. Redémarrez et entrez dans le BIOS/UEFI (F2, F10, Del, ou Suppr au démarrage)
2. Cherchez une option nommée :
   - **Intel VT-x** ou **Virtualization Technology** (Intel)
   - **AMD-V** ou **SVM Mode** (AMD)
3. Activez-la
4. Sauvegardez et redémarrez

### Configuration minimale recommandée

**Pour VirtualBox :**
- Processeur : Dual-core (2 cœurs)
- RAM : 4 GB minimum (8 GB recommandé)
- Espace disque : 20 GB par VM
- Virtualisation matérielle activée

**Pour KVM/QEMU :**
- Processeur : Quad-core (4 cœurs) recommandé
- RAM : 8 GB minimum (16 GB recommandé)
- Espace disque : 20 GB par VM
- Virtualisation matérielle requise

---

## Partie 1 : VirtualBox

### Installation de VirtualBox

#### Méthode 1 : Depuis les dépôts Ubuntu (recommandée pour débutants)

```bash
sudo apt update  
sudo apt install virtualbox virtualbox-ext-pack  
```

Le paquet `virtualbox-ext-pack` ajoute :
- Support USB 2.0 et 3.0
- Chiffrement de disque
- Boot PXE pour Intel
- Webcam passthrough

Acceptez la licence quand demandé.

#### Méthode 2 : Version officielle Oracle (dernière version)

Ajoutez le dépôt Oracle :

```bash
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -  
echo "deb [arch=amd64] https://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list  
```

Installez VirtualBox :

```bash
sudo apt update  
sudo apt install virtualbox-7.0  
```

Téléchargez l'Extension Pack depuis [virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

#### Vérifier l'installation

Lancez VirtualBox depuis le menu Applications → Outils système → VirtualBox.

### Configuration initiale de VirtualBox

#### Ajouter votre utilisateur au groupe vboxusers

Nécessaire pour utiliser les périphériques USB :

```bash
sudo usermod -aG vboxusers $USER
```

Déconnectez-vous et reconnectez-vous pour appliquer.

#### Configurer le dossier par défaut des VMs

1. Fichier → Paramètres → Général
2. "Dossier par défaut des machines" : Choisissez un emplacement avec beaucoup d'espace (ex: `/home/votre_nom/VirtualBox VMs`)

#### Configurer le réseau

Par défaut, VirtualBox configure automatiquement le réseau NAT.

### Créer votre première machine virtuelle

#### 1. Obtenir une ISO

Téléchargez l'image ISO du système que vous voulez installer :

**Exemples :**
- **Windows 11 :** [microsoft.com/software-download/windows11](https://www.microsoft.com/software-download/windows11)
- **Ubuntu :** [ubuntu.com/download](https://ubuntu.com/download)
- **Debian :** [debian.org/distrib/](https://www.debian.org/distrib/)

#### 2. Créer la VM

Cliquez sur **"Nouvelle"** dans VirtualBox.

**Assistant de création :**

1. **Nom et système d'exploitation**
   - Nom : "Windows 11" (ou autre)
   - Type : Linux/Windows/macOS/etc.
   - Version : Sélectionnez la version exacte
   - Cliquez sur "Suivant"

2. **Taille de la mémoire (RAM)**
   - Windows 11 : 4096 MB (4 GB) minimum
   - Ubuntu Desktop : 2048 MB (2 GB) minimum
   - Serveur Linux : 1024 MB (1 GB) minimum
   - **Règle d'or :** Ne pas dépasser 50% de votre RAM totale

3. **Disque dur**
   - Sélectionnez "Créer un disque dur virtuel maintenant"
   - Type de fichier : VDI (VirtualBox Disk Image)
   - Stockage : "Dynamiquement alloué" (recommandé)
   - Taille :
     - Windows : 50-80 GB
     - Linux Desktop : 25-50 GB
     - Linux Serveur : 20 GB

4. **Cliquez sur "Créer"**

#### 3. Configurer la VM avant le premier démarrage

Sélectionnez votre VM → **Configuration**

**Système :**
- Processeur : Allouez 2-4 cœurs (onglet Processeur)
- Cochez "Activer PAE/NX" si disponible
- Accélération : Vérifiez que VT-x/AMD-V est activé

**Affichage :**
- Mémoire vidéo : 128 MB
- Accélération graphique : Activez si possible

**Stockage :**
- Sélectionnez le lecteur CD (icône disque)
- À droite, cliquez sur l'icône CD
- "Choisir un fichier de disque optique virtuel"
- Sélectionnez votre fichier ISO

**Réseau :**
- Adaptateur 1 : NAT (par défaut)
- Pour partager avec l'hôte : "Accès par pont"

**Dossiers partagés :**
- Ajoutez un dossier partagé entre l'hôte et la VM
- Cliquez sur "+" → Sélectionnez un dossier
- Montage automatique : Cochez
- Permanent : Cochez

#### 4. Démarrer la VM et installer le système

1. Sélectionnez la VM → Cliquez sur **"Démarrer"**
2. La VM démarre depuis l'ISO
3. Suivez l'installation du système d'exploitation
4. Une fois installé, redémarrez la VM

#### 5. Installer les Guest Additions (additions invité)

Les Guest Additions améliorent considérablement l'expérience :
- Résolution d'écran adaptative
- Presse-papier partagé
- Glisser-déposer de fichiers
- Meilleures performances graphiques
- Dossiers partagés fonctionnels

**Installation :**

Une fois le système démarré dans la VM :

1. Menu VirtualBox → Périphériques → "Insérer l'image CD des Additions invité"
2. **Windows :** Exécutez le programme d'installation depuis le CD
3. **Linux :** Ouvrez un terminal dans la VM :

```bash
sudo apt install build-essential dkms linux-headers-$(uname -r)  
sudo mount /dev/cdrom /mnt  
sudo /mnt/VBoxLinuxAdditions.run  
sudo reboot  
```

Redémarrez la VM après l'installation.

### Fonctionnalités essentielles de VirtualBox

#### Snapshots (instantanés)

Les snapshots sauvegardent l'état complet de la VM.

**Créer un snapshot :**
1. VM en cours → Menu → "Machine" → "Prendre un instantané"
2. Donnez un nom : "Avant installation logiciel X"
3. Description (optionnelle)

**Restaurer un snapshot :**
1. Clic droit sur la VM → "Instantanés"
2. Sélectionnez l'instantané → "Restaurer"

**Utilité :** Testez des modifications dangereuses, revenez en arrière si problème !

#### Cloner une VM

Dupliquez une VM complète :

1. Clic droit sur la VM (éteinte) → "Cloner"
2. Nouveau nom : "Windows 11 - Clone"
3. Type de clone :
   - **Clone complet :** VM indépendante (copie complète)
   - **Clone lié :** Partage le disque de base (économise l'espace)

#### Mode plein écran

VM démarrée → Clic droit → "Mode plein écran" (ou Host+F)

La VM occupe tout l'écran. Appuyez sur Host+F pour sortir.

**Host** = touche configurée (souvent Ctrl droite)

#### Presse-papier partagé

Configuration → Général → Avancé :
- Presse-papier partagé : "Bidirectionnel"
- Glisser-déposer : "Bidirectionnel"

Copiez-collez entre l'hôte et la VM !

#### USB

1. Configuration → USB
2. Activez le contrôleur USB
3. Ajoutez des périphériques avec "+"
4. Ces périphériques seront automatiquement connectés à la VM

### Gestion du réseau VirtualBox

#### Mode NAT (par défaut)

- La VM peut accéder à Internet
- L'hôte ne peut pas accéder à la VM directement
- Les VMs ne se voient pas entre elles

**Usage :** Navigation Internet simple

#### Mode Accès par pont (Bridge)

- La VM obtient sa propre IP sur votre réseau
- Apparaît comme un ordinateur distinct sur le réseau
- L'hôte et les autres machines peuvent accéder à la VM

**Usage :** Serveurs, tests réseau

Configuration : Réseau → Adaptateur 1 → "Accès par pont"

#### Réseau interne

- Les VMs peuvent communiquer entre elles
- Pas d'accès Internet

**Usage :** Créer un réseau isolé de VMs

#### Réseau NAT

- Les VMs peuvent communiquer entre elles
- Les VMs ont accès à Internet
- Réseau privé pour vos VMs

**Usage :** Créer un petit réseau de VMs avec Internet

### Optimisation des performances VirtualBox

#### Allouer les bonnes ressources

**RAM :**
- Ne dépassez pas 50-70% de votre RAM totale
- Exemple : 16 GB total → Max 8-10 GB pour les VMs

**CPU :**
- N'allouez pas plus de cœurs que vous n'en avez
- Laissez au moins 1-2 cœurs pour l'hôte

#### Utiliser un SSD

Stockez vos VMs sur un SSD pour de meilleures performances.

#### Désactiver ce qui n'est pas utilisé

- Audio : Désactivez si pas nécessaire
- USB : Désactivez les contrôleurs inutilisés
- 3D : Désactivez si pas de jeux

#### Paravirtualisation

Configuration → Système → Accélération :
- Interface paravirtuelle : "KVM" (pour Linux invité) ou "Hyper-V" (pour Windows)

Améliore les performances.

---

## Partie 2 : KVM/QEMU

### Introduction à KVM/QEMU

**KVM** (Kernel-based Virtual Machine) : Module du noyau Linux qui permet la virtualisation  
**QEMU** : Émulateur et virtualiseur qui utilise KVM  
**libvirt** : API et outils pour gérer KVM/QEMU  
**virt-manager** : Interface graphique pour libvirt  

### Vérifier le support KVM

```bash
sudo apt install cpu-checker  
sudo kvm-ok  
```

**Résultat attendu :**
```
INFO: /dev/kvm exists  
KVM acceleration can be used  
```

Si "KVM acceleration can NOT be used", vérifiez le BIOS.

### Installation de KVM/QEMU

```bash
sudo apt update  
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager  
```

**Explication des paquets :**
- `qemu-kvm` : Virtualisation KVM
- `libvirt-daemon-system` : Gestion des VMs
- `libvirt-clients` : Outils en ligne de commande
- `bridge-utils` : Outils réseau
- `virt-manager` : Interface graphique

### Configurer les permissions

Ajoutez votre utilisateur aux groupes nécessaires :

```bash
sudo usermod -aG libvirt $USER  
sudo usermod -aG kvm $USER  
```

Déconnectez-vous et reconnectez-vous.

Vérifiez :

```bash
groups
```

Vous devriez voir `libvirt` et `kvm`.

### Démarrer le service libvirt

```bash
sudo systemctl start libvirtd  
sudo systemctl enable libvirtd  
```

Vérifiez :

```bash
sudo systemctl status libvirtd
```

### Lancer virt-manager

Depuis le menu : Applications → Outils système → Virtual Machine Manager

Ou en ligne de commande :

```bash
virt-manager
```

### Créer une VM avec virt-manager

#### 1. Préparer l'ISO

Téléchargez votre ISO et placez-la dans un dossier accessible.

#### 2. Créer une nouvelle VM

1. Dans virt-manager, cliquez sur l'icône "Créer une nouvelle machine virtuelle"

2. **Choisir comment installer le système**
   - Sélectionnez "Média d'installation local (image ISO ou CDROM)"
   - Cliquez sur "Suivant"

3. **Choisir le média d'installation**
   - Cliquez sur "Parcourir" → "Parcourir localement"
   - Sélectionnez votre ISO
   - virt-manager détecte automatiquement l'OS
   - Cliquez sur "Suivant"

4. **Mémoire et CPU**
   - Mémoire : 2048 MB (2 GB) minimum
   - CPUs : 2
   - Cliquez sur "Suivant"

5. **Stockage**
   - Créez un disque : 25 GB (ajustez selon vos besoins)
   - Cliquez sur "Suivant"

6. **Finaliser**
   - Nom : "Ubuntu-VM" (ou autre)
   - Réseau : NAT (par défaut)
   - Cochez "Personnaliser la configuration avant installation" pour ajuster
   - Cliquez sur "Terminer"

#### 3. Personnaliser la configuration (optionnel)

Si vous avez coché "Personnaliser" :

**Vue d'ensemble :**
- Firmware : BIOS ou UEFI (selon votre besoin)

**CPUs :**
- Ajustez le nombre de cœurs

**Mémoire :**
- Ajustez la RAM

**Disque virtuel :**
- Type de disque : VirtIO (meilleure performance)

**NIC (réseau) :**
- Type de périphérique réseau : VirtIO

**Cliquez sur "Commencer l'installation"**

#### 4. Installation du système

L'installation se déroule normalement. Suivez les étapes du système d'exploitation.

### Fonctionnalités KVM/QEMU

#### Snapshots avec virsh

En ligne de commande :

**Créer un snapshot :**

```bash
virsh snapshot-create-as --domain Ubuntu-VM --name "snapshot1" --description "Avant installation"
```

**Lister les snapshots :**

```bash
virsh snapshot-list Ubuntu-VM
```

**Restaurer un snapshot :**

```bash
virsh snapshot-revert Ubuntu-VM snapshot1
```

**Supprimer un snapshot :**

```bash
virsh snapshot-delete Ubuntu-VM snapshot1
```

#### Cloner une VM

Dans virt-manager :

1. Clic droit sur la VM (éteinte) → "Cloner"
2. Nouveau nom : "Ubuntu-VM-Clone"
3. Ajustez les paramètres réseau si nécessaire
4. Cliquez sur "Cloner"

Ou en ligne de commande :

```bash
sudo virt-clone --original Ubuntu-VM --name Ubuntu-VM-Clone --auto-clone
```

#### Gestion en ligne de commande

**Lister les VMs :**

```bash
virsh list --all
```

**Démarrer une VM :**

```bash
virsh start Ubuntu-VM
```

**Arrêter une VM :**

```bash
virsh shutdown Ubuntu-VM
```

**Forcer l'arrêt :**

```bash
virsh destroy Ubuntu-VM
```

**Supprimer une VM :**

```bash
virsh undefine Ubuntu-VM --remove-all-storage
```

**Informations sur une VM :**

```bash
virsh dominfo Ubuntu-VM
```

### Réseau avec KVM/QEMU

#### Réseau NAT par défaut

KVM crée automatiquement un réseau NAT nommé "default".

**Vérifier :**

```bash
virsh net-list --all
```

**Démarrer le réseau par défaut :**

```bash
virsh net-start default  
virsh net-autostart default  
```

#### Réseau Bridge (pont)

Pour que la VM soit visible sur votre réseau local :

**Créer un bridge :**

Éditez `/etc/netplan/01-network-manager-all.yaml` :

```bash
sudo nano /etc/netplan/01-network-manager-all.yaml
```

Ajoutez :

```yaml
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    enp3s0:  # Votre interface physique (vérifiez avec 'ip a')
      dhcp4: no
  bridges:
    br0:
      interfaces: [enp3s0]
      dhcp4: yes
```

Appliquez :

```bash
sudo netplan apply
```

**Configurer la VM pour utiliser le bridge :**

Dans virt-manager :
1. Configuration de la VM → NIC
2. Source réseau : "Bridge br0"
3. Modèle de périphérique : VirtIO

#### Réseau isolé

Créez un réseau privé pour vos VMs :

```bash
virsh net-define /dev/stdin <<EOF
<network>
  <name>isolated</name>
  <bridge name='virbr1'/>
  <ip address='192.168.100.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.100.2' end='192.168.100.254'/>
    </dhcp>
  </ip>
</network>
EOF

virsh net-start isolated  
virsh net-autostart isolated  
```

### Performances et optimisation KVM

#### Utiliser VirtIO

VirtIO offre les meilleures performances :
- Disque : VirtIO
- Réseau : VirtIO

Dans virt-manager, lors de la création ou dans Configuration → Périphériques.

#### CPU Pinning

Attribuez des cœurs CPU spécifiques à une VM :

```bash
virsh vcpupin Ubuntu-VM 0 2  
virsh vcpupin Ubuntu-VM 1 3  
```

Ici, vCPU 0 de la VM utilise le cœur physique 2, vCPU 1 utilise le cœur 3.

#### Huge Pages

Pour réduire la latence mémoire :

```bash
sudo sysctl vm.nr_hugepages=1024
```

Ajoutez dans `/etc/sysctl.conf` pour rendre permanent :

```
vm.nr_hugepages=1024
```

#### I/O Threading

Améliore les performances disque :

Dans le fichier XML de la VM :

```bash
virsh edit Ubuntu-VM
```

Ajoutez :

```xml
<driver name='qemu' type='qcow2' cache='none' io='native'/>
```

---

## Partage de fichiers entre hôte et VM

### VirtualBox : Dossiers partagés

Déjà configuré dans la section VirtualBox.

**Dans la VM Linux :**

Installez les Guest Additions, puis :

```bash
sudo usermod -aG vboxsf $USER
```

Le dossier partagé apparaît dans `/media/sf_NomDuPartage`.

**Dans la VM Windows :**

Les dossiers partagés apparaissent automatiquement dans l'Explorateur (Réseau).

### KVM/QEMU : Partage virtio-fs

**Méthode 1 : Partage de fichiers avec spice-webdav**

Installez dans la VM :

```bash
sudo apt install spice-vdagent spice-webdavd
```

Montez le dossier partagé :

```bash
sudo mount -t webdav http://localhost:9843 /mnt/partage
```

**Méthode 2 : SSH/SFTP**

Le plus simple avec KVM : utilisez SSH pour transférer des fichiers.

Dans la VM, installez SSH :

```bash
sudo apt install openssh-server
```

Depuis l'hôte :

```bash
scp fichier.txt utilisateur@ip_vm:/home/utilisateur/
```

**Méthode 3 : Serveur Samba**

Voir chapitre 21.3 pour configurer Samba.

---

## Migration depuis VirtualBox vers KVM

Si vous avez des VMs VirtualBox et voulez les migrer vers KVM :

### Convertir un disque VDI en QCOW2

```bash
qemu-img convert -f vdi -O qcow2 /chemin/vers/disk.vdi /chemin/vers/disk.qcow2
```

### Importer dans KVM

1. Créez une nouvelle VM dans virt-manager
2. Lors de l'étape stockage, choisissez "Utiliser un disque existant"
3. Sélectionnez le fichier `disk.qcow2`
4. Terminez la création

Vous devrez peut-être réinstaller les pilotes (VirtIO) dans la VM.

---

## Conteneurs vs Machines Virtuelles

### Différence fondamentale

**Machine Virtuelle :**
- Système d'exploitation complet
- Isolation totale
- Plus lourd (plusieurs GB par VM)
- Démarre en minutes

**Conteneur (Docker, LXC) :**
- Partage le noyau de l'hôte
- Application isolée
- Très léger (quelques MB)
- Démarre en secondes

### Quand utiliser quoi ?

**Utilisez des VMs pour :**
- Systèmes d'exploitation différents (Windows sur Linux)
- Isolation de sécurité maximale
- Tester des configurations système complètes
- Applications desktop

**Utilisez des conteneurs pour :**
- Applications web et microservices
- Développement rapide
- Déploiement d'applications
- Serveurs légers

**Complémentaires :** Vous pouvez utiliser Docker dans une VM !

---

## Cas d'usage avancés

### Laboratoire de sécurité

Créez un environnement isolé pour apprendre la cybersécurité :

1. VM "Kali Linux" (tests de pénétration)
2. VM "Serveur cible" (Ubuntu ou Windows)
3. VM "Routeur" (pfSense)
4. Réseau isolé entre elles

### Serveur de développement

Créez des environnements de développement reproductibles :

1. VM "Dev-Web" : LAMP stack (Linux, Apache, MySQL, PHP)
2. VM "Dev-Node" : Node.js et MongoDB
3. VM "Dev-Python" : Python et PostgreSQL

Snapshots avant/après chaque projet !

### Simulation réseau

Créez un mini réseau d'entreprise :

1. VM "DC" : Contrôleur de domaine Windows Server
2. VM "File Server" : Serveur de fichiers
3. VM "Client1", "Client2" : Postes de travail Windows
4. VM "Firewall" : pfSense ou OPNsense

### Gaming rétro

Créez des VMs pour anciens jeux :

1. VM "Windows XP" : Jeux des années 2000
2. VM "Windows 98" : Jeux des années 90
3. VM "DOS" : Jeux très anciens

Sauvegardez avec snapshots !

---

## Dépannage courant

### VirtualBox : "VT-x is not available"

**Solution :**
1. Activez VT-x dans le BIOS
2. Si déjà activé, désactivez Hyper-V (Windows) ou KVM (Linux)

### VirtualBox : VM très lente

**Solutions :**
- Installez les Guest Additions
- Allouez plus de RAM
- Activez l'accélération 3D
- Utilisez un SSD

### KVM : "Error starting domain"

**Solution :**

Vérifiez les logs :

```bash
sudo journalctl -u libvirtd
```

Vérifiez les permissions :

```bash
ls -la /var/lib/libvirt/images/
```

### KVM : Pas de connexion réseau dans la VM

**Solution :**

Vérifiez que le réseau par défaut est actif :

```bash
virsh net-list --all  
virsh net-start default  
```

### "Permission denied" lors du démarrage

**Solution :**

Vérifiez que vous êtes dans les bons groupes :

```bash
groups
```

Devrait afficher `kvm` et `libvirt` (KVM) ou `vboxusers` (VirtualBox).

### VM ne démarre pas après clonage

**Solution :**

Changez l'adresse MAC :

**VirtualBox :** Configuration → Réseau → Avancé → Adresse MAC → Régénérer

**KVM :** virt-manager gère automatiquement lors du clonage.

### Écran noir au démarrage de la VM

**Solution :**

**VirtualBox :**
- Désactivez l'accélération 3D
- Changez le contrôleur graphique (VMSVGA, VBoxSVGA)

**KVM :**
- Changez le modèle vidéo (QXL, VGA)
- Configuration → Vidéo → Modèle

---

## Sauvegardes et exports

### VirtualBox : Exporter une VM

**Export en OVA (format standard) :**

1. Fichier → Exporter une application virtuelle
2. Sélectionnez la VM
3. Format : OVA
4. Destination : Choisissez un dossier
5. Exportez

**Import d'une OVA :**

1. Fichier → Importer une application virtuelle
2. Sélectionnez le fichier .ova
3. Ajustez les paramètres
4. Importez

### KVM : Sauvegarder une VM

**Méthode 1 : Copier le disque**

```bash
sudo cp /var/lib/libvirt/images/Ubuntu-VM.qcow2 /backup/Ubuntu-VM.qcow2
```

**Méthode 2 : Export XML + disque**

```bash
virsh dumpxml Ubuntu-VM > Ubuntu-VM.xml  
sudo cp /var/lib/libvirt/images/Ubuntu-VM.qcow2 /backup/  
```

**Restaurer :**

```bash
virsh define Ubuntu-VM.xml  
sudo cp /backup/Ubuntu-VM.qcow2 /var/lib/libvirt/images/  
```

---

## Ressources système et monitoring

### Surveiller l'utilisation des VMs

**VirtualBox :**

Dans la fenêtre de la VM, Menu → Affichage → Indicateur de session

Affiche CPU, RAM, réseau en temps réel.

**KVM :**

```bash
virt-top
```

Similaire à `top` mais pour les VMs.

Ou installez :

```bash
sudo apt install virt-top
```

### Limiter les ressources

**VirtualBox :**

Configuration → Système :
- RAM : Maximum alloué
- CPU : Limite d'exécution (%)

**KVM :**

Avec `virsh edit` dans le XML :

```xml
<cputune>
  <quota>50000</quota>
  <period>100000</period>
</cputune>
```

Limite à 50% d'un cœur.

---

## Alternatives et outils complémentaires

### Alternatives à VirtualBox et KVM

#### VMware Workstation Player
- Gratuit pour usage personnel
- Excellentes performances
- Propriétaire

#### VMware Workstation Pro
- Version payante avec plus de fonctionnalités
- Très utilisé en entreprise

#### Proxmox VE
- Distribution Linux complète dédiée à la virtualisation
- Basé sur KVM
- Interface web professionnelle
- Gratuit et open source

#### GNOME Boxes
- Interface ultra-simple pour KVM
- Idéal pour débutants sur GNOME
- Moins de fonctionnalités que virt-manager

### Outils complémentaires

#### Vagrant
- Automatisation de création de VMs
- Fichiers de configuration versionables
- Idéal pour développement

```bash
sudo apt install vagrant
```

#### Packer
- Création d'images de VMs automatisées
- Pour créer des templates

#### Terraform
- Infrastructure as Code
- Gère des VMs en production

---

## Bonnes pratiques

### Organisation

1. **Nommez clairement vos VMs** : "Ubuntu-22.04-Dev", "Windows-11-Gaming"
2. **Utilisez des snapshots** avant modifications importantes
3. **Documentez** vos VMs (notes dans la description)
4. **Sauvegardez** régulièrement les VMs importantes

### Sécurité

1. **Mettez à jour** les VMs régulièrement
2. **Isolation** : Utilisez des réseaux séparés pour tester des logiciels dangereux
3. **Snapshots** avant d'exécuter des fichiers suspects
4. **Pas de partage** : Ne partagez pas vos VMs avec des logiciels piratés

### Performances

1. **Ne surchargez pas** : N'allouez pas plus de ressources que nécessaire
2. **Fermez les VMs** inutilisées
3. **SSD recommandé** pour stockage des VMs
4. **Désactivez** ce qui n'est pas utilisé (audio, USB, etc.)

### Maintenance

1. **Nettoyez** les snapshots anciens
2. **Supprimez** les VMs inutilisées
3. **Compactez** les disques virtuels pour libérer de l'espace
4. **Mettez à jour** VirtualBox/KVM régulièrement

---

## Commandes de référence rapide

### VirtualBox CLI

```bash
VBoxManage list vms                    # Lister les VMs  
VBoxManage startvm "nom_vm"            # Démarrer une VM  
VBoxManage controlvm "nom_vm" poweroff # Éteindre une VM  
VBoxManage snapshot "nom_vm" take "snapshot1"  # Créer snapshot  
VBoxManage clonevm "nom_vm" --name "clone"     # Cloner  
```

### KVM/QEMU (virsh)

```bash
virsh list --all                       # Lister les VMs  
virsh start nom_vm                     # Démarrer  
virsh shutdown nom_vm                  # Arrêter proprement  
virsh destroy nom_vm                   # Forcer l'arrêt  
virsh snapshot-create-as nom_vm snap1  # Snapshot  
virsh console nom_vm                   # Console série  
```

---

## Conclusion

Vous maîtrisez maintenant la virtualisation sur Linux Mint !

**Points clés à retenir :**
1. **VirtualBox** est parfait pour débuter et usage desktop
2. **KVM/QEMU** offre les meilleures performances pour usage avancé
3. Les **snapshots** sont votre meilleur ami pour expérimenter
4. La **virtualisation matérielle** doit être activée dans le BIOS
5. N'abusez pas des ressources : laissez de la marge pour l'hôte

**Prochaines étapes :**
- Créez votre première VM et installez un système
- Testez les snapshots et le clonage
- Configurez un réseau de VMs
- Explorez Docker pour compléter avec des conteneurs
- Créez votre laboratoire de test personnel

La virtualisation ouvre un monde de possibilités : testez, expérimentez, cassez et recommencez sans risque pour votre système principal ! 🖥️✨

---

## Ressources supplémentaires

### Documentation officielle
- VirtualBox : [virtualbox.org/manual](https://www.virtualbox.org/manual/)
- KVM : [linux-kvm.org](https://www.linux-kvm.org/)
- libvirt : [libvirt.org](https://libvirt.org/)

### Communautés
- r/virtualbox (Reddit)
- r/VFIO (Reddit - pour KVM)
- Forums Linux Mint
- Stack Overflow

### Tutoriels vidéo
- Chaînes YouTube Linux dédiées à la virtualisation
- LearnLinuxTV pour KVM/QEMU
- TechHut pour VirtualBox

Bonne virtualisation ! 🚀

⏭️ [Monitoring système (Netdata, Glances)](/21-serveurs-et-administration-systeme/06-monitoring-systeme.md)
