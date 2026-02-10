🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 18.8 Maintenance préventive (calendrier)

## Introduction

Imaginez que vous conduisez une voiture : vous ne faites pas la vidange uniquement quand le moteur tombe en panne, vous suivez un **calendrier d'entretien préventif**. C'est exactement la même chose pour votre système Linux Mint !

La **maintenance préventive** consiste à effectuer régulièrement de petites actions simples pour éviter les gros problèmes. C'est comme se brosser les dents tous les jours pour éviter de chez le dentiste : 5 minutes par jour valent mieux que 2 heures de soins.

**Dans ce chapitre, vous apprendrez à :**
- Établir un calendrier de maintenance adapté à votre utilisation
- Automatiser les tâches répétitives
- Identifier les actions critiques vs optionnelles
- Maintenir un système performant et fiable sur le long terme
- Éviter les problèmes avant qu'ils ne surviennent

**Pourquoi c'est important ?**
- **Prévenir les pannes** : anticiper les problèmes avant qu'ils ne surviennent
- **Performances optimales** : un système entretenu reste rapide
- **Sécurité renforcée** : les mises à jour et vérifications protègent votre système
- **Longévité** : un PC bien entretenu dure 10+ ans sans problème
- **Tranquillité d'esprit** : savoir que tout fonctionne correctement

---

## Philosophie de la maintenance préventive

### Le principe 80/20

**80% des bénéfices proviennent de 20% des actions.**

Les tâches vraiment importantes :
1. 🔄 **Mises à jour régulières** → Sécurité et stabilité
2. 💾 **Sauvegardes automatiques** → Protection des données
3. 🧹 **Nettoyage mensuel** → Espace disque et performances
4. 🔍 **Surveillance SMART** → Anticiper les défaillances matérielles

**Ces 4 actions couvrent 80% de vos besoins en maintenance.**

### Maintenance curative vs préventive

**Maintenance curative (réactive) :**
- ❌ Attendre que le problème survienne
- ❌ Réparer en urgence
- ❌ Stress et perte de temps
- ❌ Risque de perte de données

**Maintenance préventive (proactive) :**
- ✅ Anticiper les problèmes
- ✅ Agir selon un planning
- ✅ Sérénité et contrôle
- ✅ Données toujours protégées

**Exemple concret :**

| Situation | Curatif | Préventif |
|-----------|---------|-----------|
| Disque plein | Panique, suppression en urgence de fichiers importants | Nettoyage mensuel, toujours 20% d'espace libre |
| Disque défaillant | Perte de données, achat urgent d'un nouveau disque | SMART détecte le problème 3 mois avant, remplacement planifié |
| Mise à jour critique | Faille de sécurité exploitée avant la mise à jour | Mises à jour hebdomadaires automatiques |

### Les niveaux de maintenance

**Niveau 1 - Essentiel (pour tous)**
- Mises à jour système
- Sauvegarde des données
- Vérification de base mensuelle

**Niveau 2 - Recommandé (utilisateurs réguliers)**
- Nettoyage système mensuel
- Surveillance SMART
- Optimisations SSD

**Niveau 3 - Avancé (power users)**
- Vérifications d'intégrité
- Analyse des logs
- Scripts d'automatisation personnalisés

---

## Calendrier de maintenance complet

### Quotidien (automatique)

Ces tâches doivent être **automatisées** et ne nécessitent aucune action manuelle.

#### ✅ Tâches automatiques

**1. Mises à jour en arrière-plan**
- Linux Mint vérifie automatiquement les mises à jour
- Notification si des mises à jour importantes sont disponibles

**2. Surveillance SMART (smartd)**
```bash
# Vérifier que smartd est actif
systemctl status smartd
```

Si inactif, activez-le :
```bash
sudo systemctl enable smartd  
sudo systemctl start smartd  
```

**3. Logs système**
- journald enregistre automatiquement tous les événements
- Rotation automatique des logs

**4. Timeshift (si configuré)**
- Snapshots automatiques selon votre configuration
- Vérification : Menu > Administration > Timeshift

#### 🔍 Actions manuelles (1 minute)

**Regarder les notifications**
- Mises à jour disponibles ?
- Alertes système ?
- Espace disque faible ?

**Si vous voyez une notification :** Agissez immédiatement (ne pas reporter).

---

### Hebdomadaire (5-10 minutes)

**Jour recommandé :** Dimanche ou lundi matin

#### 📋 Checklist hebdomadaire

**1. Appliquer les mises à jour** ⭐⭐⭐⭐⭐
```bash
sudo apt update && sudo apt upgrade -y
```

Ou via l'interface graphique :
- Menu > Administration > Gestionnaire de mises à jour
- Cliquez sur "Installer les mises à jour"

**Temps estimé :** 5-15 minutes (selon le nombre de mises à jour)

**2. Vérifier l'espace disque** ⭐⭐⭐⭐
```bash
df -h /
```

**Objectif :** Garder au moins 15-20% d'espace libre.

**Si < 15% libre :** Nettoyage nécessaire (voir section hebdomadaire étendue).

**3. Vider la corbeille**
- Clic droit sur l'icône Corbeille > "Vider la corbeille"

**4. Redémarrer l'ordinateur**
- Si le PC tourne depuis plus de 7 jours
- Applique les mises à jour du noyau
- Libère la RAM

**Commande pour voir l'uptime :**
```bash
uptime
```

Si > 7 jours, redémarrez.

#### 🔧 Actions optionnelles

**Vérifier les erreurs récentes :**
```bash
journalctl -p err --since "1 week ago" | less
```

Si beaucoup d'erreurs, investiguer.

**Vérifier les services échoués :**
```bash
systemctl --failed
```

Si des services ont échoué, les redémarrer ou investiguer.

---

### Mensuel (30-45 minutes)

**Jour recommandé :** Premier dimanche du mois

#### 📋 Checklist mensuelle complète

**1. Nettoyage du système** ⭐⭐⭐⭐⭐

**Nettoyage APT :**
```bash
sudo apt autoremove -y  
sudo apt autoclean  
```

**Nettoyage des logs :**
```bash
sudo journalctl --vacuum-time=30d
```

**Nettoyage du cache utilisateur :**
```bash
rm -rf ~/.cache/thumbnails/*
```

**Temps estimé :** 5 minutes

**Espace libéré typique :** 1-5 Go

**2. Vérification SMART du disque** ⭐⭐⭐⭐
```bash
sudo smartctl -H /dev/sda
```

**Résultat attendu :** `PASSED`

**Si FAILED :** 🔴 **URGENT** - Sauvegardez vos données immédiatement et remplacez le disque.

**3. Analyse de l'espace disque** ⭐⭐⭐

**Méthode graphique (Baobab) :**
```bash
baobab &
```

**Méthode terminal (ncdu) :**
```bash
ncdu ~
```

**Objectif :** Identifier et supprimer les gros fichiers inutiles.

**4. Vérifier les snapshots Timeshift** ⭐⭐⭐⭐⭐
```bash
sudo timeshift --list
```

**Vérifications :**
- Au moins 3 snapshots récents disponibles
- Le dernier snapshot date de moins de 7 jours
- L'espace de stockage des snapshots n'est pas plein

**Si aucun snapshot :** Configurez Timeshift IMMÉDIATEMENT (section 17.1).

**5. Mise à jour du firmware** ⭐⭐⭐
```bash
fwupdmgr refresh  
fwupdmgr get-updates  
```

Si des mises à jour sont disponibles :
```bash
fwupdmgr update
```

**6. Vérifier les services au démarrage** ⭐⭐
```bash
systemd-analyze blame
```

Si le démarrage est lent (>60 secondes), identifiez les services gourmands.

**7. Nettoyer les vieux noyaux** ⭐⭐

**Via interface graphique :**
- Gestionnaire de mises à jour > Affichage > Noyaux Linux
- Supprimez les vieux noyaux (gardez les 2 derniers)

#### 📊 Tableau récapitulatif mensuel

| Tâche | Importance | Temps | Fréquence |
|-------|------------|-------|-----------|
| Nettoyage système | ⭐⭐⭐⭐⭐ | 5 min | Mensuel |
| SMART du disque | ⭐⭐⭐⭐ | 2 min | Mensuel |
| Analyse espace disque | ⭐⭐⭐ | 10 min | Mensuel |
| Vérif. Timeshift | ⭐⭐⭐⭐⭐ | 2 min | Mensuel |
| Firmware | ⭐⭐⭐ | 5 min | Mensuel |
| Nettoyage noyaux | ⭐⭐ | 3 min | Mensuel |

**Temps total :** 30-45 minutes

---

### Trimestriel (1-2 heures)

**Recommandation :** Premier weekend de janvier, avril, juillet, octobre

#### 📋 Checklist trimestrielle

**1. Nettoyage approfondi avec BleachBit** ⭐⭐⭐⭐

**Lancer BleachBit :**
```bash
bleachbit &
```

**Cochez :**
- Cache APT
- Cache navigateurs (Firefox, Chrome)
- Miniatures
- Journaux système
- Corbeille
- Fichiers temporaires

**Prévisualisez**, puis **Nettoyez**.

**Temps estimé :** 15 minutes  
**Espace libéré :** 5-20 Go  

**2. Vérification d'intégrité des paquets** ⭐⭐⭐
```bash
sudo debsums -c
```

Si des erreurs apparaissent, réinstallez les paquets concernés :
```bash
sudo apt install --reinstall nom-du-paquet
```

**3. Scan antirootkit** ⭐⭐⭐
```bash
sudo rkhunter --update  
sudo rkhunter --check --sk  
```

**Résultat attendu :** 0 rootkits détectés

**4. Désinstallation des applications inutilisées** ⭐⭐⭐

**Lister les paquets installés manuellement :**
```bash
apt-mark showmanual | less
```

**Désinstaller ceux que vous n'utilisez plus :**
```bash
sudo apt remove nom-application  
sudo apt autoremove  
```

**5. Optimisation SSD (si applicable)** ⭐⭐⭐⭐

**Vérifier que TRIM est actif :**
```bash
sudo systemctl status fstrim.timer
```

**Lancer TRIM manuellement :**
```bash
sudo fstrim -av
```

**6. Analyse complète des logs** ⭐⭐
```bash
# Erreurs des 3 derniers mois
journalctl -p err --since "3 months ago" | less

# Taille des logs
journalctl --disk-usage
```

**7. Vérification des sauvegardes** ⭐⭐⭐⭐⭐

**Test de restauration :**
- Choisissez un fichier important
- Restaurez-le depuis votre sauvegarde
- Vérifiez qu'il fonctionne

**Objectif :** S'assurer que vos sauvegardes sont fonctionnelles.

**8. Mise à jour de la distribution (si disponible)** ⭐⭐⭐⭐

Si une nouvelle version de Linux Mint est disponible :
- Consultez les notes de version
- Créez un snapshot Timeshift
- Lancez la mise à jour via le Gestionnaire de mises à jour

---

### Semestriel (2-3 heures)

**Recommandation :** Juin et décembre

#### 📋 Checklist semestrielle

**1. Test complet de la RAM (Memtest86+)** ⭐⭐⭐⭐

**Lancement :**
1. Redémarrez
2. Menu GRUB > "Memory test (memtest86+)"
3. Laissez tourner toute la nuit (plusieurs passes)

**Résultat attendu :** 0 erreur

**Si erreurs :** Remplacez la RAM défectueuse.

**2. Vérification complète du disque (fsck)** ⭐⭐⭐⭐

**En mode recovery :**
1. Redémarrez
2. GRUB > Advanced options > Recovery mode
3. fsck > Yes

**Ou forcer au prochain démarrage :**
```bash
sudo touch /forcefsck
```

**3. Audit de sécurité** ⭐⭐⭐

**Vérifier les tentatives de connexion échouées :**
```bash
sudo grep "Failed password" /var/log/auth.log | wc -l
```

**Vérifier les modifications de fichiers système :**
```bash
sudo find /etc -type f -mtime -180 -ls
```

**Scan avec chkrootkit :**
```bash
sudo chkrootkit
```

**4. Évaluation des performances** ⭐⭐

**Temps de démarrage :**
```bash
systemd-analyze
```

**Objectif :** < 30 secondes (SSD) ou < 60 secondes (HDD)

**Si trop lent :** Désactivez les services inutiles (section 18.2).

**5. Révision des configurations personnalisées** ⭐⭐

**Vérifier les modifications dans /etc :**
```bash
sudo find /etc -name "*.dpkg-old" -o -name "*.dpkg-dist"
```

Ces fichiers indiquent des configurations modifiées lors de mises à jour.

**6. Nettoyage des anciens fichiers de configuration** ⭐⭐
```bash
dpkg -l | grep '^rc' | awk '{print $2}' | sudo xargs apt purge -y
```

Supprime les configurations de paquets désinstallés.

**7. Défragmentation (HDD uniquement, PAS SSD !)** ⭐

**⚠️ Uniquement pour disques durs mécaniques, JAMAIS pour SSD !**

```bash
sudo e4defrag -c /
```

Si fragmentation > 10%, défragmentez :
```bash
sudo e4defrag /
```

**8. Revue des scripts d'automatisation** ⭐⭐

Vérifiez que vos crontabs fonctionnent :
```bash
crontab -l  
sudo crontab -l  
```

---

### Annuel (4-6 heures)

**Recommandation :** Décembre ou janvier (début d'année)

#### 📋 Checklist annuelle

**1. Réinstallation propre (optionnel)** ⭐⭐

**Pour repartir à neuf :**
- Sauvegardez TOUT
- Réinstallez Linux Mint depuis zéro
- Restaurez vos données

**Avantages :**
- Système ultra-rapide
- Aucune accumulation de "cruft"
- Configuration propre

**Inconvénient :** Temps d'installation et de reconfiguration

**Alternative :** Garder le système actuel s'il fonctionne bien.

**2. Audit complet du matériel** ⭐⭐⭐⭐

**Vérifier tous les composants :**
```bash
sudo lshw -short  
sudo smartctl -a /dev/sda  
sensors  
```

**Points à vérifier :**
- Températures (< 70°C en charge)
- SMART (attributs critiques)
- Aucun composant défaillant

**3. Révision de la stratégie de sauvegarde** ⭐⭐⭐⭐⭐

**Questions à se poser :**
- Mes sauvegardes sont-elles complètes ?
- Sont-elles automatiques ?
- Ai-je une copie hors site (cloud) ?
- Ai-je testé une restauration complète ?

**Règle 3-2-1 :**
- **3** copies de vos données
- Sur **2** supports différents
- **1** copie hors site

**4. Mise à jour de la documentation** ⭐⭐

**Documentez :**
- Liste des logiciels installés
- Configurations personnalisées
- Mots de passe (dans un gestionnaire sécurisé)
- Partitionnement et structure du système

**5. Planification des upgrades matériels** ⭐⭐

**Évaluer :**
- Votre RAM est-elle suffisante ?
- Votre disque est-il assez grand ?
- Devez-vous passer à un SSD ?
- Composants en fin de vie ?

**6. Révision de la configuration réseau et sécurité** ⭐⭐⭐

**Vérifier :**
- Pare-feu (UFW) actif
- SSH sécurisé (si utilisé)
- Fail2Ban configuré (si serveur)
- Mots de passe forts partout

**7. Test de récupération d'urgence** ⭐⭐⭐⭐⭐

**Simuler une panne :**
1. Démarrez sur une clé USB Live
2. Tentez d'accéder à vos données
3. Restaurez un snapshot Timeshift
4. Vérifiez que tout fonctionne

**Objectif :** S'assurer que vous pouvez récupérer en cas de catastrophe.

---

## Scripts d'automatisation

### Script de maintenance hebdomadaire

```bash
nano ~/maintenance-hebdo.sh
```

Contenu :
```bash
#!/bin/bash

echo "========================================"  
echo "🔧 Maintenance hebdomadaire automatique"  
echo "========================================"  
echo ""  

# 1. Mise à jour du système
echo "📥 1. Mise à jour du système..."  
sudo apt update  
sudo apt upgrade -y  
sudo apt autoremove -y  
echo "✅ Système mis à jour"  
echo ""  

# 2. Vérification de l'espace disque
echo "💾 2. Vérification de l'espace disque..."  
USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')  
AVAIL=$(df -h / | awk 'NR==2 {print $4}')  
echo "   Utilisation : ${USAGE}%"  
echo "   Disponible : ${AVAIL}"  
if [ "$USAGE" -gt 80 ]; then  
    echo "⚠️  ATTENTION : Espace disque > 80% !"
    notify-send "⚠️ Espace disque faible" "Seulement ${AVAIL} disponible"
fi  
echo ""  

# 3. Vider la corbeille
echo "🗑️  3. Vidage de la corbeille..."  
rm -rf ~/.local/share/Trash/*  
echo "✅ Corbeille vidée"  
echo ""  

# 4. Vérification SMART
echo "🔍 4. Vérification SMART du disque..."  
if command -v smartctl &> /dev/null; then  
    SMART=$(sudo smartctl -H /dev/sda 2>/dev/null | grep "PASSED")
    if [ -n "$SMART" ]; then
        echo "✅ Disque en bonne santé"
    else
        echo "⚠️  Vérifiez SMART manuellement !"
        notify-send "⚠️ Alerte SMART" "Vérifiez la santé de votre disque"
    fi
else
    echo "ℹ️  smartmontools non installé"
fi  
echo ""  

# 5. Résumé
echo "========================================"  
echo "✅ Maintenance hebdomadaire terminée !"  
echo "========================================"  
echo ""  
echo "📊 Prochaines actions :"  
echo "  - Maintenance mensuelle : premier dimanche du mois"  
echo "  - Redémarrage : si uptime > 7 jours"  
echo ""  

# Enregistrer dans les logs
echo "$(date): Maintenance hebdomadaire effectuée" >> ~/.maintenance-log.txt
```

Rendez-le exécutable :
```bash
chmod +x ~/maintenance-hebdo.sh
```

**Automatiser avec cron (tous les dimanches à 10h) :**
```bash
crontab -e
```

Ajoutez :
```
0 10 * * 0 ~/maintenance-hebdo.sh | tee -a ~/maintenance-hebdo.log
```

### Script de maintenance mensuelle

```bash
nano ~/maintenance-mensuelle.sh
```

Contenu :
```bash
#!/bin/bash

echo "========================================"  
echo "🧹 Maintenance mensuelle complète"  
echo "========================================"  
echo ""  

# 1. Nettoyage système
echo "🗑️  1. Nettoyage du système..."  
sudo apt autoremove -y  
sudo apt autoclean  
sudo journalctl --vacuum-time=30d  
rm -rf ~/.cache/thumbnails/*  
echo "✅ Système nettoyé"  
echo ""  

# 2. Vérification SMART détaillée
echo "🔍 2. Vérification SMART détaillée..."  
sudo smartctl -H /dev/sda  
echo ""  

# 3. Analyse de l'espace disque
echo "💾 3. Top 10 des dossiers les plus volumineux..."  
du -h --max-depth=1 ~ 2>/dev/null | sort -rh | head -n 10  
echo ""  

# 4. Vérification Timeshift
echo "💾 4. Vérification des snapshots Timeshift..."  
if command -v timeshift &> /dev/null; then  
    SNAPSHOTS=$(sudo timeshift --list 2>/dev/null | grep "^  O" | wc -l)
    echo "   Snapshots disponibles : $SNAPSHOTS"
    if [ "$SNAPSHOTS" -lt 2 ]; then
        echo "⚠️  Pas assez de snapshots ! Configurez Timeshift."
        notify-send "⚠️ Snapshots Timeshift" "Seulement $SNAPSHOTS snapshot(s)"
    else
        echo "✅ Snapshots OK"
    fi
else
    echo "⚠️  Timeshift non installé !"
fi  
echo ""  

# 5. Mise à jour firmware
echo "🔧 5. Vérification firmware..."  
if command -v fwupdmgr &> /dev/null; then  
    fwupdmgr refresh --force 2>/dev/null
    UPDATES=$(fwupdmgr get-updates 2>/dev/null | grep -c "Update")
    if [ "$UPDATES" -gt 0 ]; then
        echo "ℹ️  $UPDATES mise(s) à jour firmware disponible(s)"
        echo "   Exécutez : fwupdmgr update"
    else
        echo "✅ Firmware à jour"
    fi
else
    echo "ℹ️  fwupd non installé"
fi  
echo ""  

# 6. Vérification des services échoués
echo "⚙️  6. Services système..."  
FAILED=$(systemctl list-units --failed --no-pager --no-legend | wc -l)  
if [ "$FAILED" -eq 0 ]; then  
    echo "✅ Tous les services fonctionnent"
else
    echo "⚠️  $FAILED service(s) en échec"
    systemctl --failed
fi  
echo ""  

# 7. Résumé
echo "========================================"  
echo "✅ Maintenance mensuelle terminée !"  
echo "========================================"  
echo ""  

# Log
echo "$(date): Maintenance mensuelle effectuée" >> ~/.maintenance-log.txt

# Notification
notify-send "✅ Maintenance mensuelle" "Maintenance terminée avec succès"
```

Rendez-le exécutable :
```bash
chmod +x ~/maintenance-mensuelle.sh
```

**Automatiser (premier dimanche du mois à 14h) :**
```bash
crontab -e
```

Ajoutez :
```
0 14 1-7 * 0 ~/maintenance-mensuelle.sh | tee -a ~/maintenance-mensuelle.log
```

---

## Calendriers par profil d'utilisateur

### Profil 1 : Utilisateur occasionnel (< 10h/semaine)

**Caractéristiques :**
- Navigation web, emails, bureautique
- Peu de fichiers stockés localement
- Pas de jeux ou applications lourdes

#### Calendrier simplifié

**Hebdomadaire (5 min) :**
- ✅ Mises à jour système
- ✅ Vérifier l'espace disque

**Mensuel (20 min) :**
- ✅ Nettoyage avec script automatique
- ✅ Vérifier Timeshift
- ✅ Vider la corbeille

**Trimestriel (1h) :**
- ✅ Nettoyage BleachBit complet
- ✅ Vérification SMART

**Annuel (2h) :**
- ✅ Test de restauration Timeshift
- ✅ Révision des sauvegardes

### Profil 2 : Utilisateur régulier (10-30h/semaine)

**Caractéristiques :**
- Utilisation quotidienne
- Photos, vidéos, documents importants
- Plusieurs applications installées

#### Calendrier standard

**Hebdomadaire (10 min) :**
- ✅ Mises à jour système
- ✅ Vérifier l'espace disque
- ✅ Vider la corbeille
- ✅ Redémarrer si uptime > 7 jours

**Mensuel (30 min) :**
- ✅ Script de maintenance mensuelle
- ✅ Analyse espace disque (Baobab)
- ✅ Vérification SMART
- ✅ Vérifier Timeshift

**Trimestriel (1h30) :**
- ✅ Nettoyage BleachBit
- ✅ Scan antirootkit (rkhunter)
- ✅ Désinstaller apps inutilisées
- ✅ Optimisation SSD (TRIM)

**Semestriel (3h) :**
- ✅ Test RAM (Memtest86+)
- ✅ Vérification fsck
- ✅ Audit de sécurité

**Annuel (4h) :**
- ✅ Test restauration complète
- ✅ Révision stratégie de sauvegarde
- ✅ Audit matériel

### Profil 3 : Power User / Professionnel (30h+/semaine)

**Caractéristiques :**
- Ordinateur de travail critique
- Beaucoup de données
- Environnements de développement, VMs, etc.

#### Calendrier intensif

**Quotidien (automatique) :**
- ✅ Surveillance SMART active
- ✅ Snapshots Timeshift quotidiens
- ✅ Sauvegarde incrémentale cloud

**Hebdomadaire (15 min) :**
- ✅ Mises à jour système
- ✅ Vérifier l'espace disque
- ✅ Consulter les logs d'erreurs
- ✅ Vérifier les services critiques

**Mensuel (45 min) :**
- ✅ Maintenance complète automatisée
- ✅ Analyse approfondie espace disque
- ✅ Vérification SMART détaillée
- ✅ Optimisation SSD
- ✅ Rotation des snapshots

**Trimestriel (2h) :**
- ✅ Nettoyage complet BleachBit
- ✅ Vérification d'intégrité paquets
- ✅ Scan antirootkit + antivirus
- ✅ Révision des services au démarrage
- ✅ Analyse des logs complets

**Semestriel (4h) :**
- ✅ Test RAM complet
- ✅ Vérification fsck approfondie
- ✅ Audit de sécurité complet
- ✅ Test de récupération d'urgence
- ✅ Benchmark performances

**Annuel (6h) :**
- ✅ Considérer réinstallation propre
- ✅ Révision complète architecture système
- ✅ Mise à jour documentation
- ✅ Planification upgrades matériels
- ✅ Révision politique de sécurité

### Profil 4 : Créateur de contenu (Photo/Vidéo)

**Caractéristiques :**
- Très gros fichiers (RAW, 4K)
- Besoin de performance maximale
- Sauvegardes critiques

#### Calendrier spécifique

**Quotidien :**
- ✅ Sauvegarde automatique des projets en cours
- ✅ Vérification espace disque (seuil 20%)

**Hebdomadaire (20 min) :**
- ✅ Mises à jour système
- ✅ Nettoyage cache applications créatives
- ✅ Archivage projets terminés
- ✅ Vérification SMART

**Mensuel (1h) :**
- ✅ Maintenance standard
- ✅ Analyse espace disque approfondie
- ✅ Nettoyage fichiers temporaires volumineux
- ✅ Optimisation SSD (TRIM)
- ✅ Test vitesse disque

**Trimestriel (2h) :**
- ✅ Nettoyage complet
- ✅ Archivage long terme (disque externe/cloud)
- ✅ Vérification intégrité archives
- ✅ Mise à jour logiciels créatifs

**Semestriel (3h) :**
- ✅ Test complet des sauvegardes
- ✅ Révision workflow et outils
- ✅ Benchmark performances
- ✅ Considérer upgrade stockage

---

## Outils d'automatisation avancés

### Anacron : Pour ordinateurs non allumés 24/7

**Anacron** exécute les tâches manquées quand l'ordinateur était éteint.

**Installation :**
```bash
sudo apt install anacron
```

**Configuration :**
```bash
sudo nano /etc/anacrontab
```

**Exemple :**
```
# period delay job-identifier command
1    5    daily-maintenance    ~/maintenance-hebdo.sh
7    10   weekly-maintenance   ~/maintenance-mensuelle.sh
```

**Signification :**
- `1` : tous les 1 jour
- `5` : attend 5 minutes après le démarrage
- `daily-maintenance` : identifiant unique

### Systemd timers : Alternative moderne à cron

**Créer un timer systemd pour maintenance hebdomadaire :**

**1. Créer le service :**
```bash
sudo nano /etc/systemd/system/maintenance-hebdo.service
```

Contenu :
```
[Unit]
Description=Maintenance hebdomadaire

[Service]
Type=oneshot  
ExecStart=/home/votre-nom/maintenance-hebdo.sh  
User=votre-nom  
```

**2. Créer le timer :**
```bash
sudo nano /etc/systemd/system/maintenance-hebdo.timer
```

Contenu :
```
[Unit]
Description=Lancer maintenance hebdomadaire

[Timer]
OnCalendar=Sun 10:00  
Persistent=true  

[Install]
WantedBy=timers.target
```

**3. Activer :**
```bash
sudo systemctl enable maintenance-hebdo.timer  
sudo systemctl start maintenance-hebdo.timer  
```

**4. Vérifier :**
```bash
systemctl list-timers
```

---

## Notifications et alertes

### Notifications desktop

**Script avec notification :**

```bash
#!/bin/bash

# Effectuer la maintenance
~/maintenance-hebdo.sh

# Notifier l'utilisateur
notify-send "✅ Maintenance terminée" "Votre système est à jour et optimisé"
```

### Alertes par email

**Installer mailutils :**
```bash
sudo apt install mailutils
```

**Script avec email :**
```bash
#!/bin/bash

LOG_FILE="/tmp/maintenance-report.txt"

# Maintenance
~/maintenance-hebdo.sh > $LOG_FILE 2>&1

# Envoyer par email
cat $LOG_FILE | mail -s "Rapport de maintenance $(date)" votre@email.com
```

### Alertes sur conditions critiques

**Script d'alerte espace disque :**

```bash
#!/bin/bash

USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

if [ "$USAGE" -gt 85 ]; then
    notify-send --urgency=critical "🔴 DISQUE PLEIN" "Espace utilisé : ${USAGE}%"
    echo "Alerte disque : ${USAGE}%" | mail -s "URGENT: Disque plein" votre@email.com
fi
```

---

## Journal de maintenance

### Pourquoi tenir un journal ?

**Avantages :**
- Traçabilité des actions effectuées
- Identification de patterns (pannes récurrentes)
- Documentation pour dépannage
- Historique des mises à jour

### Template de journal simple

Créez un fichier :
```bash
nano ~/journal-maintenance.md
```

Contenu :
```markdown
# Journal de maintenance - Linux Mint

## 2024

### Décembre
- **01/12/2024** : Maintenance mensuelle. Nettoyage 8 Go. SMART OK. 3 snapshots.
- **08/12/2024** : Mise à jour hebdomadaire. Kernel 6.5.0-15.
- **15/12/2024** : Alerte espace disque 88%. Suppression vidéos anciennes (-12 Go).

### Novembre
- **03/11/2024** : Maintenance mensuelle. SMART OK. Firmware WiFi mis à jour.
- **10/11/2024** : Maintenance hebdo. Aucun problème.
```

### Automatiser les logs

**Ajouter à vos scripts de maintenance :**

```bash
# À la fin de chaque script
echo "$(date '+%d/%m/%Y %H:%M') - Maintenance mensuelle. Espace: $(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')%. SMART: OK" >> ~/journal-maintenance.md
```

---

## Checklist avant événements importants

### Avant une mise à jour majeure

- [ ] Créer un snapshot Timeshift
- [ ] Sauvegarder les données importantes
- [ ] Vérifier l'espace disque (>10 Go libre)
- [ ] Lire les notes de version
- [ ] Vérifier SMART du disque
- [ ] Fermer toutes les applications

### Avant un voyage / déplacement (laptop)

- [ ] Mises à jour système
- [ ] Vérifier la batterie
- [ ] Sauvegarder les données
- [ ] Snapshot Timeshift
- [ ] Télécharger documents offline
- [ ] Vérifier VPN

### Avant de vendre / donner l'ordinateur

- [ ] Sauvegarder TOUTES les données
- [ ] Vérifier SMART (garantir disque sain)
- [ ] Réinstallation propre de Linux Mint
- [ ] Effacement sécurisé (si données sensibles)
- [ ] Documenter l'état du matériel

---

## Métriques et objectifs

### Indicateurs de santé système

**Objectifs à maintenir :**

| Métrique | Objectif | Seuil d'alerte |
|----------|----------|----------------|
| Espace disque libre | > 20% | < 15% |
| Uptime | 7-30 jours | > 60 jours |
| SMART status | PASSED | WARNING/FAILED |
| Température CPU | < 65°C | > 75°C |
| Erreurs journalctl/jour | < 10 | > 50 |
| Services échoués | 0 | > 2 |
| Snapshots Timeshift | 3+ récents | < 2 |
| Temps de démarrage | < 30s (SSD) | > 60s |

### Tableau de bord personnalisé

**Script de dashboard :**

```bash
nano ~/dashboard.sh
```

Contenu :
```bash
#!/bin/bash

clear  
echo "╔══════════════════════════════════════════╗"  
echo "║     TABLEAU DE BORD SYSTÈME              ║"  
echo "╚══════════════════════════════════════════╝"  
echo ""  

# Uptime
echo "⏱️  Uptime : $(uptime -p)"  
echo ""  

# Espace disque
USAGE=$(df -h / | awk 'NR==2 {print $5}')  
AVAIL=$(df -h / | awk 'NR==2 {print $4}')  
echo "💾 Espace disque : $USAGE utilisé, $AVAIL disponible"  
echo ""  

# SMART
if command -v smartctl &> /dev/null; then
    SMART=$(sudo smartctl -H /dev/sda 2>/dev/null | grep -o "PASSED\|FAILED")
    echo "🔧 SMART Status : $SMART"
else
    echo "🔧 SMART Status : Non disponible"
fi  
echo ""  

# Snapshots
if command -v timeshift &> /dev/null; then
    SNAPS=$(sudo timeshift --list 2>/dev/null | grep "^  O" | wc -l)
    echo "💾 Snapshots Timeshift : $SNAPS"
else
    echo "💾 Snapshots Timeshift : Non configuré"
fi  
echo ""  

# Services
FAILED=$(systemctl list-units --failed --no-pager --no-legend | wc -l)  
echo "⚙️  Services échoués : $FAILED"  
echo ""  

# Erreurs récentes
ERRORS=$(journalctl -p err -b | wc -l)  
echo "📋 Erreurs depuis démarrage : $ERRORS"  
echo ""  

# Mises à jour
UPDATES=$(apt list --upgradable 2>/dev/null | grep -c upgradable)  
if [ "$UPDATES" -le 1 ]; then  
    echo "🔄 Mises à jour : Système à jour ✅"
else
    echo "🔄 Mises à jour : $UPDATES disponibles"
fi  
echo ""  

echo "══════════════════════════════════════════"  
echo "Dernière maintenance : $(tail -n 1 ~/.maintenance-log.txt 2>/dev/null || echo 'Jamais')"  
```

Rendez-le exécutable :
```bash
chmod +x ~/dashboard.sh
```

Ajoutez à votre `.bashrc` pour l'afficher à chaque ouverture de terminal :
```bash
echo "~/dashboard.sh" >> ~/.bashrc
```

---

## Conclusion

La maintenance préventive n'est **pas une corvée**, c'est un **investissement** dans la fiabilité et la longévité de votre système.

### Les principes clés

1. **Régularité** : Peu et souvent vaut mieux que beaucoup mais rarement
2. **Automatisation** : Ce qui peut être automatisé doit l'être
3. **Surveillance** : Observer pour anticiper, pas pour réagir
4. **Simplicité** : Commencez simple, complexifiez si nécessaire
5. **Persévérance** : La régularité paie sur le long terme

### Le minimum vital (pour TOUS)

**Si vous ne retenez que 4 choses :**

1. ✅ **Mises à jour hebdomadaires** (5 min)
2. ✅ **Timeshift configuré** avec snapshots automatiques
3. ✅ **Nettoyage mensuel** (30 min)
4. ✅ **Vérification SMART mensuelle** (2 min)

**Ces 4 actions représentent 80% de la valeur de la maintenance.**

### Progression graduelle

**Semaine 1-4 :** Mises à jour hebdomadaires uniquement  
**Mois 2 :** Ajoutez le nettoyage mensuel  
**Mois 3 :** Configurez Timeshift  
**Mois 4+ :** Ajoutez les autres vérifications selon vos besoins  

**Ne vous surchargez pas dès le début !**

### Calendrier de démarrage (premier mois)

**Semaine 1 :**
- [ ] Installer smartmontools et activer smartd
- [ ] Configurer Timeshift avec snapshots quotidiens
- [ ] Premier snapshot manuel

**Semaine 2 :**
- [ ] Créer le script de maintenance hebdomadaire
- [ ] Automatiser avec cron ou anacron
- [ ] Premier test du script

**Semaine 3 :**
- [ ] Créer le script de maintenance mensuelle
- [ ] L'automatiser
- [ ] Première exécution

**Semaine 4 :**
- [ ] Créer votre journal de maintenance
- [ ] Configurer les notifications
- [ ] Créer votre dashboard personnel

### Ressources complémentaires

**Pour approfondir :**
- **Section 17** : Sauvegarde et restauration (Timeshift)
- **Section 18.1** : Nettoyage du système
- **Section 18.2** : Gestion des services
- **Section 18.3** : Surveillance des ressources
- **Section 18.4** : Optimisation SSD
- **Section 18.5** : Gestion des logs
- **Section 18.6** : Analyse de l'espace disque
- **Section 18.7** : Vérification de l'intégrité
- **Section 20.2** : Cron et tâches planifiées

**Avec ce calendrier de maintenance, votre Linux Mint sera toujours en excellente santé !** 🚀💚

---

## Annexe : Commandes rapides de référence

### Maintenance express (5 minutes)

```bash
# Tout-en-un
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y && df -h / && sudo smartctl -H /dev/sda
```

### Nettoyage express (10 minutes)

```bash
# Nettoyage complet rapide
sudo apt autoremove -y && sudo apt autoclean && sudo journalctl --vacuum-time=30d && rm -rf ~/.cache/thumbnails/* && rm -rf ~/.local/share/Trash/*
```

### Vérification express (2 minutes)

```bash
# Statut système
df -h / && uptime && systemctl --failed && journalctl -p err -b | wc -l
```

**Gardez ces commandes à portée de main pour une maintenance ultra-rapide !**

⏭️ [Développement et programmation](/19-developpement-et-programmation/README.md)
