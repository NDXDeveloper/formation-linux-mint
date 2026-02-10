🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 18.1 Nettoyage du système

## Introduction

Même sous Linux Mint, votre système accumule au fil du temps des fichiers inutiles : paquets obsolètes, caches d'applications, fichiers temporaires, anciennes versions de logiciels, etc. Contrairement à Windows, Linux n'a pas besoin d'un nettoyage aussi fréquent, mais un entretien régulier permet de :

- **Libérer de l'espace disque** : récupérer plusieurs gigaoctets d'espace
- **Améliorer les performances** : notamment lors des mises à jour
- **Maintenir un système sain** : éviter l'accumulation de fichiers corrompus ou obsolètes

**Bonne nouvelle pour les débutants** : le nettoyage sous Linux Mint est simple, sécurisé et bien moins risqué que sous d'autres systèmes d'exploitation.

---

## Pourquoi nettoyer son système ?

### Qu'est-ce qui encombre votre disque ?

Au fil de l'utilisation, plusieurs types de fichiers s'accumulent :

1. **Paquets téléchargés** : quand vous installez ou mettez à jour des logiciels, les fichiers `.deb` restent stockés
2. **Paquets orphelins** : dépendances qui ne sont plus nécessaires après la désinstallation d'un logiciel
3. **Caches d'applications** : Firefox, Chromium et autres applications stockent des données temporaires
4. **Fichiers de log** : journaux système qui grossissent avec le temps
5. **Miniatures d'images** : vignettes générées pour l'aperçu des photos
6. **Corbeille** : fichiers supprimés mais non vidés définitivement

### À quelle fréquence nettoyer ?

- **Nettoyage léger** : une fois par mois (5 minutes)
- **Nettoyage complet** : tous les 3 à 6 mois (15-20 minutes)
- **Après une grosse mise à jour** : toujours recommandé

---

## Méthode 1 : Nettoyage avec les commandes APT (Recommandé pour débuter)

APT est le gestionnaire de paquets de Linux Mint. Il dispose de commandes spécifiques pour nettoyer le système en toute sécurité.

### 1. Supprimer les paquets obsolètes : `apt autoremove`

Cette commande supprime les paquets qui ont été installés automatiquement comme dépendances et qui ne sont plus nécessaires.

**Comment l'utiliser :**

1. Ouvrez le terminal (Menu > Terminal ou `Ctrl+Alt+T`)
2. Tapez la commande suivante :

```bash
sudo apt autoremove
```

3. Entrez votre mot de passe administrateur
4. Le système vous montre la liste des paquets à supprimer
5. Appuyez sur `O` (pour Oui) puis `Entrée` pour confirmer

**Ce que vous verrez :**
```
Les paquets suivants seront ENLEVÉS :
  linux-headers-5.15.0-56 linux-headers-5.15.0-56-generic
  linux-image-5.15.0-56-generic linux-modules-5.15.0-56-generic
0 mis à jour, 0 nouvellement installés, 4 à enlever et 0 non mis à jour.
Après cette opération, 325 Mo d'espace disque seront libérés.  
Souhaitez-vous continuer ? [O/n]  
```

**⚠️ Note importante :** Cette commande est sûre et ne supprimera jamais de paquets essentiels au fonctionnement de votre système.

### 2. Nettoyer le cache des paquets : `apt autoclean`

Quand vous installez des logiciels, Linux Mint télécharge des fichiers `.deb` et les stocke dans un cache. `autoclean` supprime uniquement les anciennes versions devenues inutiles.

**Comment l'utiliser :**

```bash
sudo apt autoclean
```

Cette commande ne demande pas de confirmation et s'exécute rapidement.

**Différence avec `apt clean` :**
- `apt autoclean` : supprime seulement les vieux paquets obsolètes (recommandé)
- `apt clean` : supprime TOUT le cache, même les paquets récents (plus agressif)

Pour un nettoyage plus complet, vous pouvez utiliser :

```bash
sudo apt clean
```

**Espace libéré typique :** entre 500 Mo et 2 Go selon votre utilisation.

### 3. Commande combinée (gain de temps)

Vous pouvez enchaîner les commandes sur une seule ligne :

```bash
sudo apt update && sudo apt autoremove -y && sudo apt autoclean
```

**Explication :**
- `apt update` : met à jour la liste des paquets
- `&&` : exécute la commande suivante seulement si la précédente réussit
- `-y` : répond automatiquement "oui" (attention à ne l'utiliser que si vous êtes sûr)
- `apt autoclean` : nettoie le cache

---

## Méthode 2 : Nettoyage graphique avec BleachBit

BleachBit est un logiciel graphique puissant qui nettoie en profondeur votre système, similaire à CCleaner sur Windows mais open source et gratuit.

### Installation de BleachBit

1. Ouvrez le **Gestionnaire de logiciels** (Menu > Administration > Gestionnaire de logiciels)
2. Recherchez "BleachBit"
3. Cliquez sur **Installer**

Ou en ligne de commande :

```bash
sudo apt install bleachbit
```

### Utilisation de BleachBit

#### Premier lancement

1. Lancez BleachBit depuis le menu (Menu > Administration > BleachBit)
2. Vous verrez deux icônes :
   - **BleachBit** : mode normal (nettoie vos fichiers utilisateur)
   - **BleachBit (administrateur)** : mode root (nettoie aussi les fichiers système)

**Pour un nettoyage complet, utilisez les deux.**

#### Nettoyage utilisateur (BleachBit normal)

1. Lancez **BleachBit** (sans droits root)
2. Dans la colonne de gauche, cochez les éléments à nettoyer :

**Recommandations pour débutants :**

✅ **À cocher systématiquement :**
- Cache APT
- Firefox/Chrome/Chromium : Cache, Cookies (si vous voulez vous déconnecter), Historique des téléchargements
- Miniatures (vignettes d'images)
- Corbeille
- Journaux système
- Cache du système

⚠️ **À utiliser avec précaution :**
- Cookies des navigateurs (vous serez déconnecté de tous les sites)
- Mots de passe des navigateurs (ne cochez que si vous les sauvegardez ailleurs)
- Historique de navigation (supprime votre historique web)

❌ **À éviter pour les débutants :**
- Configuration de Firefox/Chrome (peut casser vos paramètres)
- Localisation (fichiers de langue)

3. Cliquez sur **Aperçu** pour voir combien d'espace sera libéré
4. Cliquez sur **Nettoyer** pour lancer le nettoyage
5. Confirmez si demandé

#### Nettoyage système (BleachBit administrateur)

1. Lancez **BleachBit en tant qu'administrateur** (clic droit > Exécuter en tant qu'administrateur, ou depuis le menu avec "(root)")
2. Entrez votre mot de passe
3. Cochez les mêmes options que précédemment, plus :
   - **APT** : cache et paquets obsolètes
   - **Localisation** : langues non utilisées (libère 100-500 Mo)
   - **Journaux système** : logs anciens

4. Cliquez sur **Aperçu** puis **Nettoyer**

### Fonctionnalités avancées de BleachBit

#### Déchiquetage sécurisé (Shred)

BleachBit peut effacer des fichiers de manière à ce qu'ils soient irrécupérables :

1. Faites un clic droit sur un fichier dans votre gestionnaire de fichiers
2. Sélectionnez **Ouvrir avec** > **BleachBit Shredder**
3. Confirmez la suppression définitive

**⚠️ Attention :** Cette action est irréversible !

#### Effacement d'espace libre

Pour éviter que des fichiers supprimés soient récupérables :

1. Dans BleachBit, allez dans **Édition** > **Préférences**
2. Onglet **Drives**
3. Cochez **Overwrite free disk space** (prend beaucoup de temps)

**Note :** Cette fonction est utile avant de vendre un ordinateur, mais inutile pour un usage normal.

---

## Nettoyages complémentaires

### 1. Vider la corbeille

La corbeille ne se vide pas automatiquement sous Linux Mint.

**Méthode graphique :**
- Clic droit sur l'icône de la corbeille > **Vider la corbeille**

**Méthode terminal :**
```bash
rm -rf ~/.local/share/Trash/*
```

### 2. Nettoyer les vieux noyaux Linux (kernels)

Linux Mint conserve plusieurs versions du noyau en cas de problème. Vous pouvez supprimer les anciennes versions tout en gardant les 2 dernières.

**⚠️ Important :** Ne supprimez jamais le noyau actuellement utilisé !

**Méthode graphique (recommandée) :**

1. Ouvrez le **Gestionnaire de mises à jour**
2. Allez dans **Affichage** > **Noyaux Linux**
3. Vous verrez la liste des noyaux installés
4. Le noyau actuel est marqué d'un point vert
5. Sélectionnez les anciens noyaux (sauf les 2 derniers)
6. Cliquez sur **Supprimer**

**Méthode terminal (pour utilisateurs avertis) :**

```bash
sudo apt autoremove --purge
```

Cette commande supprime aussi les vieux noyaux automatiquement.

### 3. Nettoyer les fichiers de configuration orphelins

Quand vous désinstallez un logiciel, ses fichiers de configuration restent parfois.

```bash
dpkg -l | grep '^rc' | awk '{print $2}' | sudo xargs apt purge -y
```

**Explication :**
- `dpkg -l` : liste tous les paquets
- `grep '^rc'` : filtre ceux avec configuration résiduelle
- `xargs apt purge` : les supprime complètement

### 4. Nettoyer le cache des miniatures

Les miniatures d'images peuvent occuper beaucoup d'espace :

```bash
rm -rf ~/.cache/thumbnails/*
```

Elles seront automatiquement régénérées quand nécessaire.

### 5. Nettoyer les journaux système (logs)

Les logs peuvent devenir volumineux avec le temps.

**Vérifier la taille des logs :**
```bash
journalctl --disk-usage
```

**Limiter les logs à 500 Mo :**
```bash
sudo journalctl --vacuum-size=500M
```

**Limiter les logs à 30 jours :**
```bash
sudo journalctl --vacuum-time=30d
```

---

## Analyse de l'espace disque avant/après nettoyage

Pour visualiser ce que vous avez gagné, utilisez **Baobab** (Analyseur d'utilisation des disques).

1. Menu > **Analyseur d'utilisation des disques** (Baobab)
2. Cliquez sur **Scanner le système de fichiers**
3. Attendez la fin de l'analyse
4. Vous verrez un graphique montrant où est utilisé votre espace

**Alternative en ligne de commande :**

```bash
df -h
```

Cela affiche l'espace utilisé et disponible sur chaque partition.

---

## Planifier un nettoyage automatique

### Option 1 : Créer un script de nettoyage

Créez un fichier script pour automatiser le nettoyage :

```bash
nano ~/nettoyage-mint.sh
```

Copiez-y ce contenu :

```bash
#!/bin/bash
echo "🧹 Début du nettoyage du système..."  
echo ""  

echo "📦 Suppression des paquets obsolètes..."  
sudo apt autoremove -y  

echo "🗑️  Nettoyage du cache APT..."  
sudo apt autoclean  

echo "📝 Nettoyage des journaux (conservation 30 jours)..."  
sudo journalctl --vacuum-time=30d  

echo "🖼️  Suppression des miniatures..."  
rm -rf ~/.cache/thumbnails/*  

echo "✅ Nettoyage terminé !"  
df -h | grep '/$'  
```

Rendez-le exécutable :

```bash
chmod +x ~/nettoyage-mint.sh
```

Exécutez-le quand vous voulez :

```bash
~/nettoyage-mint.sh
```

### Option 2 : Automatisation avec Cron (utilisateurs avancés)

Vous pouvez programmer le script pour qu'il s'exécute automatiquement chaque mois (voir section 20.2 sur Cron pour plus de détails).

---

## Précautions et bonnes pratiques

### ⚠️ Ce qu'il ne faut PAS faire

1. **Ne supprimez jamais** `/usr`, `/bin`, `/lib`, `/etc` ou tout dossier système dont vous ne comprenez pas l'utilité
2. **N'utilisez pas** `rm -rf /` ou des commandes destructrices trouvées sur internet sans comprendre
3. **Ne videz pas** la corbeille avant d'être certain de ne plus avoir besoin des fichiers
4. **Ne supprimez pas** tous les noyaux Linux, gardez au moins les 2 derniers

### ✅ Bonnes pratiques

1. **Faites une sauvegarde** avant un grand nettoyage (avec Timeshift, voir section 17.1)
2. **Lisez toujours** ce que les commandes vont faire avant de confirmer
3. **Commencez par les commandes APT** simples avant d'utiliser BleachBit
4. **Vérifiez l'espace libéré** après chaque opération pour constater les résultats
5. **Nettoyez régulièrement** plutôt que d'attendre que le disque soit plein

---

## Résumé des commandes essentielles

| Commande | Action | Fréquence recommandée |
|----------|--------|----------------------|
| `sudo apt autoremove` | Supprime paquets inutiles | Mensuelle |
| `sudo apt autoclean` | Nettoie vieux paquets cache | Mensuelle |
| `sudo apt clean` | Vide tout le cache APT | Occasionnelle |
| `sudo journalctl --vacuum-time=30d` | Limite les logs à 30 jours | Trimestrielle |
| `rm -rf ~/.cache/thumbnails/*` | Supprime les miniatures | Occasionnelle |

---

## Combien d'espace pouvez-vous récupérer ?

Cela dépend de votre utilisation, mais voici des estimations moyennes :

- **Après 1 mois d'utilisation** : 200-500 Mo
- **Après 6 mois sans nettoyage** : 2-5 Go
- **Après 1 an sans nettoyage** : 5-15 Go
- **Avec suppression de vieux noyaux** : +1-3 Go supplémentaires
- **Avec nettoyage BleachBit complet** : potentiellement 20+ Go sur un système ancien

**Astuce :** Notez l'espace disque avant et après votre premier nettoyage pour avoir une référence personnelle.

---

## Conclusion

Le nettoyage de Linux Mint est :
- **Simple** : quelques commandes suffisent
- **Sûr** : impossible de casser le système avec les commandes recommandées
- **Rapide** : 5 à 15 minutes pour un nettoyage complet
- **Efficace** : récupère plusieurs gigaoctets d'espace

**Routine recommandée pour débutants :**
1. Une fois par mois : `sudo apt autoremove && sudo apt autoclean`
2. Tous les 3 mois : nettoyage BleachBit complet
3. Tous les 6 mois : suppression des vieux noyaux

Avec ces habitudes simples, votre Linux Mint restera performant et réactif pendant des années ! 🚀

---

## Pour aller plus loin

- **Section 17.1** : Timeshift pour sauvegardes système (à configurer avant le nettoyage)
- **Section 18.6** : Analyse de l'espace disque avec Baobab et ncdu
- **Section 20.2** : Automatisation avec Cron
- **Section 18.8** : Calendrier de maintenance préventive

⏭️ [Gestion des services au démarrage (systemd)](/18-maintenance-et-optimisation/02-gestion-des-services-au-demarrage.md)
