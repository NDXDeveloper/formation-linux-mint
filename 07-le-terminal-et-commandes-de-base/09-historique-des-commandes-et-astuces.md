🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.9 - Historique des commandes et astuces

## Introduction

Le terminal garde une trace de toutes les commandes que vous avez tapées. Cette fonctionnalité, appelée **historique**, est extrêmement utile pour :
- Retrouver une commande complexe tapée il y a quelques jours
- Réexécuter une commande sans la retaper
- Corriger une faute de frappe rapidement
- Apprendre de vos erreurs passées
- Gagner un temps considérable

**Analogie :** L'historique est comme un carnet où vous noteriez automatiquement toutes les instructions que vous donnez à votre ordinateur. Vous pouvez le feuilleter, retrouver une instruction et la réutiliser.

Dans ce chapitre, nous allons découvrir comment maîtriser l'historique et apprendre des astuces qui transformeront votre productivité dans le terminal.

---

## La commande `history`

### Afficher l'historique complet

```bash
history
```

Affiche toutes les commandes que vous avez tapées, numérotées.

**Exemple de sortie :**
```
  497  cd Documents
  498  ls -la
  499  nano fichier.txt
  500  git status
  501  sudo apt update
  502  history
```

### Afficher les N dernières commandes

```bash
history 20
```

Affiche les 20 dernières commandes.

### Rechercher dans l'historique

```bash
history | grep "apt"
```

Affiche toutes les commandes contenant "apt".

**Exemple pratique :**
```bash
history | grep "install"
```

Retrouve toutes les commandes d'installation que vous avez tapées.

### Effacer l'historique

#### Effacer tout l'historique

```bash
history -c
```

**⚠️ Attention :** Cela supprime tout l'historique de la session actuelle.

#### Effacer une ligne spécifique

```bash
history -d 500
```

Supprime la commande numéro 500 de l'historique.

**Utilité :** Supprimer une commande contenant un mot de passe que vous avez tapé par erreur.

### Sauvegarder l'historique

```bash
history -w
```

Force l'écriture de l'historique dans le fichier `~/.bash_history`.

Par défaut, l'historique est sauvegardé automatiquement quand vous fermez le terminal.

---

## Navigation dans l'historique avec les flèches

### Méthode de base : Flèches haut et bas

| Touche | Action |
|--------|--------|
| **Flèche haut ↑** | Commande précédente |
| **Flèche bas ↓** | Commande suivante |

**Utilisation :**
1. Appuyez sur **↑** pour voir la dernière commande
2. Appuyez encore sur **↑** pour remonter dans l'historique
3. Appuyez sur **↓** pour redescendre
4. Quand vous voyez la commande voulue, appuyez sur **Entrée**

**Cas d'usage courant :**
Vous venez de taper une longue commande avec une erreur :
```bash
sudo apt install fireox
# Erreur : fireox au lieu de firefox
```

Au lieu de tout retaper :
1. **↑** pour rappeler la commande
2. Corrigez "fireox" → "firefox"
3. **Entrée**

### Éditer une commande de l'historique

Une fois que vous avez rappelé une commande avec **↑** :
- **Flèches ←/→** : Déplacer le curseur
- **Home** / **Ctrl+A** : Aller au début
- **End** / **Ctrl+E** : Aller à la fin
- **Ctrl+U** : Effacer tout avant le curseur
- **Ctrl+K** : Effacer tout après le curseur

---

## Recherche rapide dans l'historique : Ctrl+R

### La recherche inversée (reverse search)

**Ctrl+R** est l'une des fonctionnalités les plus puissantes du terminal !

**Comment ça marche :**
1. Appuyez sur **Ctrl+R**
2. Le prompt change en `(reverse-i-search):`
3. Tapez quelques lettres
4. Le terminal affiche la dernière commande correspondante
5. Appuyez sur **Entrée** pour l'exécuter ou **→** pour l'éditer

### Exemple pratique

Vous voulez retrouver la commande `sudo systemctl restart apache2` tapée il y a deux jours :

1. **Ctrl+R**
2. Tapez `restart` ou `apache`
3. La commande apparaît
4. **Entrée** pour l'exécuter

**Navigation dans les résultats :**
- **Ctrl+R** à nouveau : Résultat précédent
- **Ctrl+S** : Résultat suivant (peut nécessiter `stty -ixon` dans ~/.bashrc)
- **Ctrl+G** ou **Esc** : Annuler la recherche

### Astuces avec Ctrl+R

**Recherche par mot-clé unique :**
Au lieu de taper toute la commande, tapez un mot unique :
- `restart` plutôt que toute la commande
- `install` pour retrouver vos installations
- `grep` pour vos recherches

**Combiner avec les flèches :**
1. **Ctrl+R** + tapez votre mot
2. **→** pour éditer la commande trouvée
3. Modifiez ce que vous voulez
4. **Entrée**

---

## Exécuter des commandes de l'historique

### Avec le numéro : `!n`

```bash
!500
```

Exécute la commande numéro 500 de l'historique.

**Workflow :**
1. `history | grep "apt"` pour trouver la commande
2. Notez le numéro (par exemple 500)
3. `!500` pour l'exécuter

### Dernière commande : `!!`

```bash
!!
```

Réexécute la **dernière commande**.

**Cas d'usage ultra fréquent :**
Vous avez oublié `sudo` :
```bash
apt install vim
# Permission denied
```

Solution en une seconde :
```bash
sudo !!
# Équivalent à : sudo apt install vim
```

### Dernière commande commençant par... : `!texte`

```bash
!apt
```

Exécute la dernière commande commençant par "apt".

**Exemples :**
```bash
!cd        # Dernière commande cd
!nano      # Dernière commande nano
!sudo      # Dernière commande sudo
```

**⚠️ Attention :** Vérifiez bien ce qui va s'exécuter ! Utilisez `:p` pour prévisualiser.

### Prévisualiser sans exécuter : `:p`

```bash
!500:p
```

Affiche la commande numéro 500 sans l'exécuter.

```bash
!!:p
```

Affiche la dernière commande.

**Workflow sécurisé :**
1. `!apt:p` pour voir quelle commande sera exécutée
2. Si OK, `!apt` pour l'exécuter

---

## Manipulation avancée de l'historique

### Substitution rapide : `^ancien^nouveau`

Remplace un mot de la dernière commande.

**Exemple :**
```bash
echo "Bonjour monde"
^monde^Linux
# Exécute : echo "Bonjour Linux"
```

**Cas d'usage courant :**
```bash
sudo systemctl restart apache2
^apache2^nginx
# Exécute : sudo systemctl restart nginx
```

### Réutiliser des arguments

#### Dernier argument : `!$`

```bash
mkdir /chemin/vers/dossier  
cd !$  
# Équivalent à : cd /chemin/vers/dossier
```

Le `!$` représente le dernier argument de la commande précédente.

**Autre exemple :**
```bash
touch fichier.txt  
nano !$  
# Ouvre fichier.txt dans nano
```

#### Premier argument : `!^`

```bash
ls -la fichier.txt  
cat !^  
# Équivalent à : cat fichier.txt
```

#### Tous les arguments : `!*`

```bash
chmod +x script1.sh script2.sh script3.sh  
ls -l !*  
# Équivalent à : ls -l script1.sh script2.sh script3.sh
```

### Argument n d'une commande : `!:n`

```bash
cp /source/fichier.txt /destination/  
cd !:2  
# Va dans /destination/
```

- `!:0` : La commande elle-même
- `!:1` : Premier argument
- `!:2` : Deuxième argument
- etc.

---

## Le fichier .bash_history

### Emplacement et contenu

L'historique est stocké dans :
```bash
~/.bash_history
```

**Voir le fichier :**
```bash
cat ~/.bash_history
```

ou mieux :
```bash
less ~/.bash_history
```

### Comment ça fonctionne

**Lors de l'ouverture du terminal :**
- Bash charge `~/.bash_history` en mémoire

**Pendant la session :**
- Les commandes sont ajoutées à la mémoire

**À la fermeture du terminal :**
- L'historique en mémoire est sauvegardé dans `~/.bash_history`

**⚠️ Important :** Si vous avez plusieurs terminaux ouverts, seul le dernier fermé écrit son historique (par défaut).

### Éditer manuellement l'historique

Vous pouvez éditer `~/.bash_history` directement :

```bash
nano ~/.bash_history
```

**Cas d'usage :**
- Supprimer des commandes sensibles (mots de passe)
- Nettoyer l'historique
- Ajouter des commandes de référence

**Note :** Les modifications ne prendront effet qu'au prochain démarrage du terminal.

### Sauvegarder/restaurer l'historique

#### Sauvegarder

```bash
cp ~/.bash_history ~/bash_history_backup_$(date +%Y%m%d)
```

#### Restaurer

```bash
cp ~/bash_history_backup_20241130 ~/.bash_history
```

---

## Configuration de l'historique

### Variables d'environnement importantes

Ces variables contrôlent le comportement de l'historique. Ajoutez-les dans `~/.bashrc` :

#### HISTSIZE : Taille de l'historique en mémoire

```bash
HISTSIZE=10000
```

Nombre de commandes gardées en mémoire pendant la session.

#### HISTFILESIZE : Taille du fichier .bash_history

```bash
HISTFILESIZE=20000
```

Nombre de commandes gardées dans le fichier.

#### HISTCONTROL : Contrôler ce qui est enregistré

```bash
HISTCONTROL=ignoredups:ignorespace
```

**Options :**
- `ignoredups` : Ignore les doublons consécutifs
- `ignorespace` : Ignore les commandes commençant par un espace
- `ignoreboth` : Les deux combinés
- `erasedups` : Supprime tous les doublons (pas seulement consécutifs)

**Exemple pratique :**
```bash
# Avec ignorespace
 sudo apt update    # (espace au début)
# Cette commande ne sera PAS dans l'historique
```

**Utilité :** Pour les commandes contenant des mots de passe.

#### HISTIGNORE : Ignorer certaines commandes

```bash
HISTIGNORE="ls:ll:cd:pwd:clear:history"
```

Les commandes listées ne seront pas enregistrées.

#### HISTTIMEFORMAT : Ajouter des timestamps

```bash
HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S  "
```

**Résultat avec `history` :**
```
  500  2024-11-30 14:23:45  cd Documents
  501  2024-11-30 14:24:12  ls -la
  502  2024-11-30 14:25:03  nano fichier.txt
```

**Très utile pour savoir quand vous avez exécuté une commande !**

### Configuration recommandée

Ajoutez ceci dans votre `~/.bashrc` :

```bash
# Configuration de l'historique
HISTSIZE=10000                          # Historique en mémoire  
HISTFILESIZE=20000                      # Historique dans le fichier  
HISTCONTROL=ignoreboth:erasedups        # Ignorer espaces et doublons  
HISTTIMEFORMAT="%F %T  "                # Format: YYYY-MM-DD HH:MM:SS  
shopt -s histappend                     # Ajouter à l'historique au lieu d'écraser  
PROMPT_COMMAND='history -a'             # Sauvegarder après chaque commande  
```

**Appliquer les changements :**
```bash
source ~/.bashrc
```

### shopt : Options du shell

#### histappend : Ajouter au lieu d'écraser

```bash
shopt -s histappend
```

Avec plusieurs terminaux ouverts, ajoute au fichier au lieu de l'écraser.

#### cmdhist : Commandes multi-lignes sur une ligne

```bash
shopt -s cmdhist
```

Les commandes sur plusieurs lignes sont enregistrées sur une seule ligne.

#### lithist : Garder les sauts de ligne

```bash
shopt -s lithist
```

Garde les commandes multi-lignes avec leurs sauts de ligne.

---

## Astuces de productivité

### 1. Exécuter la dernière commande avec sudo

```bash
sudo !!
```

**Exemple :**
```bash
systemctl restart nginx
# Permission denied
sudo !!
# Fonctionne !
```

### 2. Créer un fichier et l'ouvrir immédiatement

```bash
touch rapport.txt && nano !$
```

### 3. Répéter une commande sur plusieurs fichiers

```bash
chmod +x script1.sh
!!:s/script1/script2/
!!:s/script1/script3/
```

### 4. Naviguer entre dossiers

```bash
cd /var/log
# ... travail ...
cd -    # Retourne au dossier précédent  
cd -    # Revient à /var/log  
```

### 5. Réutiliser des arguments complexes

```bash
grep -r "ERROR" /var/log/apache2/error.log  
less !$  
# Ouvre le fichier directement
```

### 6. Commandes fréquentes : Créer des alias

Ajoutez dans `~/.bashrc` :

```bash
alias h='history'  
alias h10='history 10'  
alias hgrep='history | grep'  
```

**Utilisation :**
```bash
hgrep apt    # Cherche "apt" dans l'historique  
h10          # Affiche les 10 dernières commandes  
```

### 7. Recherche multi-critères

```bash
history | grep "docker" | grep "run"
```

Trouve toutes les commandes contenant "docker" ET "run".

### 8. Exporter l'historique

```bash
history > ~/commandes_$(date +%Y%m%d).txt
```

Sauvegarde l'historique dans un fichier daté.

### 9. Statistiques de vos commandes

```bash
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10
```

Affiche vos 10 commandes les plus utilisées.

**Exemple de résultat :**
```
    245 ls
    189 cd
    156 git
    142 nano
     98 sudo
     87 cat
     76 grep
     65 docker
     54 ssh
     48 python
```

### 10. Effacer l'écran sans perdre l'historique

```bash
clear
# ou Ctrl+L
```

L'écran est effacé, mais vous pouvez toujours utiliser **↑** pour rappeler les commandes.

---

## Raccourcis clavier essentiels

### Navigation

| Raccourci | Action |
|-----------|--------|
| **Ctrl+A** | Aller au début de la ligne |
| **Ctrl+E** | Aller à la fin de la ligne |
| **Ctrl+←** | Mot précédent |
| **Ctrl+→** | Mot suivant |
| **Alt+B** | Mot précédent (alternative) |
| **Alt+F** | Mot suivant (alternative) |

### Édition

| Raccourci | Action |
|-----------|--------|
| **Ctrl+U** | Effacer du curseur au début |
| **Ctrl+K** | Effacer du curseur à la fin |
| **Ctrl+W** | Effacer le mot avant le curseur |
| **Alt+D** | Effacer le mot après le curseur |
| **Ctrl+Y** | Coller le dernier texte coupé |
| **Ctrl+T** | Échanger les deux derniers caractères |
| **Alt+T** | Échanger les deux derniers mots |
| **Alt+U** | Mettre le mot en MAJUSCULES |
| **Alt+L** | Mettre le mot en minuscules |
| **Alt+C** | Capitaliser le mot |

### Contrôle

| Raccourci | Action |
|-----------|--------|
| **Ctrl+C** | Annuler/Interrompre la commande |
| **Ctrl+D** | Fermer le terminal (ou EOF) |
| **Ctrl+L** | Effacer l'écran |
| **Ctrl+Z** | Suspendre le processus |
| **Ctrl+R** | Recherche inversée |
| **Ctrl+S** | Recherche vers l'avant |
| **Ctrl+G** | Annuler la recherche |

### Historique

| Raccourci | Action |
|-----------|--------|
| **↑** | Commande précédente |
| **↓** | Commande suivante |
| **Ctrl+R** | Recherche dans l'historique |
| **Ctrl+P** | Précédent (comme ↑) |
| **Ctrl+N** | Suivant (comme ↓) |
| **Alt+.** | Dernier argument de la commande précédente |
| **Alt+<** | Début de l'historique |
| **Alt+>** | Fin de l'historique |

---

## Astuces avancées

### 1. Exécuter plusieurs commandes de l'historique

```bash
!500; !502; !505
```

Exécute les commandes 500, 502 et 505 séquentiellement.

### 2. Historique par session

Pour éviter le mélange entre plusieurs terminaux :

```bash
# Dans ~/.bashrc
PROMPT_COMMAND='history -a; history -n'
```

### 3. Historique infini

```bash
# Dans ~/.bashrc
HISTSIZE=-1  
HISTFILESIZE=-1  
```

Aucune limite ! (Peut ralentir avec le temps)

### 4. Historique séparé par dossier

Créez un script pour sauvegarder l'historique par projet :

```bash
# Dans ~/.bashrc
cd() {
    builtin cd "$@"
    history -a
    history -w ~/.bash_history_$(pwd | tr '/' '_')
}
```

### 5. Colorier la sortie de history

Ajoutez dans `~/.bashrc` :

```bash
alias history='history | grep --color=auto'
```

### 6. Recherche améliorée avec fzf

Installez `fzf` :
```bash
sudo apt install fzf
```

Puis ajoutez dans `~/.bashrc` :
```bash
source /usr/share/doc/fzf/examples/key-bindings.bash
```

**Ctrl+R** devient une interface interactive de recherche !

---

## Outils complémentaires

### 1. `fc` (Fix Command)

Éditer et réexécuter une commande :

```bash
fc
```

Ouvre la dernière commande dans votre éditeur (nano/vim).

**Éditer une commande spécifique :**
```bash
fc 500
```

**Éditer une plage :**
```bash
fc 490 500
```

### 2. Script pour nettoyer l'historique

Créez `~/clean_history.sh` :

```bash
#!/bin/bash
# Supprimer les doublons de l'historique
cat ~/.bash_history | sort | uniq > ~/.bash_history_clean  
mv ~/.bash_history_clean ~/.bash_history  
echo "Historique nettoyé !"  
```

### 3. Sauvegarder régulièrement

Créez un cron job pour sauvegarder l'historique :

```bash
crontab -e
```

Ajoutez :
```
0 0 * * 0 cp ~/.bash_history ~/bash_history_backup_$(date +\%Y\%m\%d)
```

Sauvegarde hebdomadaire le dimanche à minuit.

---

## Erreurs courantes et solutions

### Erreur 1 : Historique non sauvegardé

**Problème :** Vous fermez le terminal et vos commandes disparaissent.

**Solution :**
Ajoutez dans `~/.bashrc` :
```bash
shopt -s histappend  
PROMPT_COMMAND='history -a'  
```

### Erreur 2 : Commandes sensibles dans l'historique

**Problème :** Vous avez tapé un mot de passe dans une commande.

**Solutions :**

**Option 1 : Espace au début**
```bash
# Dans ~/.bashrc
HISTCONTROL=ignorespace

# Puis tapez avec un espace
 mysql -u root -p motdepasse
```

**Option 2 : Supprimer de l'historique**
```bash
history | grep "mysql"  
history -d 523    # Supprime la ligne 523  
```

**Option 3 : Désactiver temporairement**
```bash
set +o history        # Désactiver
# Tapez vos commandes sensibles
set -o history        # Réactiver
```

### Erreur 3 : L'historique ne se recherche pas avec Ctrl+R

**Problème :** Ctrl+R ne fonctionne pas.

**Solution :**
Vérifiez que `stty` n'intercepte pas Ctrl+S :
```bash
stty -ixon
```

Ajoutez dans `~/.bashrc` pour rendre permanent.

### Erreur 4 : Historique corrompu

**Problème :** `bash_history` contient des données étranges.

**Solution :**
```bash
> ~/.bash_history    # Vider le fichier
history -c           # Effacer l'historique en mémoire
```

Ou restaurez depuis une sauvegarde.

### Erreur 5 : Trop de commandes similaires

**Problème :** L'historique est plein de `ls`, `cd`, etc.

**Solution :**
```bash
# Dans ~/.bashrc
HISTIGNORE="ls:ll:cd:pwd:clear:exit:history"
```

---

## Bonnes pratiques

### 1. Configurez votre historique dès le début

Personnalisez `~/.bashrc` avec vos préférences :
```bash
HISTSIZE=10000  
HISTFILESIZE=20000  
HISTCONTROL=ignoreboth:erasedups  
HISTTIMEFORMAT="%F %T  "  
shopt -s histappend  
```

### 2. Utilisez des alias pour les commandes fréquentes

Au lieu de chercher dans l'historique :
```bash
alias update='sudo apt update && sudo apt upgrade'  
alias ports='sudo netstat -tulpn'  
alias logs='sudo tail -f /var/log/syslog'  
```

### 3. Nettoyez régulièrement

```bash
# Supprimer les vieilles entrées
history -c  
history -r  
```

### 4. Sauvegardez vos configurations

```bash
cp ~/.bashrc ~/.bashrc.backup  
cp ~/.bash_history ~/.bash_history.backup  
```

### 5. Documentez vos commandes complexes

Au lieu de chercher dans l'historique, créez un fichier de référence :
```bash
nano ~/commandes_utiles.md
```

### 6. Soyez prudent avec les commandes destructives

Vérifiez toujours avant d'exécuter :
```bash
!rm:p    # Prévisualiser
!rm      # Puis exécuter si OK
```

---

## Résumé

### Commandes essentielles

```bash
history              # Afficher tout l'historique  
history 20           # 20 dernières commandes  
history | grep "mot" # Rechercher dans l'historique  
history -c           # Effacer l'historique  
history -d 500       # Supprimer la ligne 500  
```

### Raccourcis de navigation

```bash
↑ / ↓                # Naviguer dans l'historique
Ctrl+R               # Recherche interactive
!!                   # Dernière commande
!n                   # Commande numéro n
!texte               # Dernière commande commençant par "texte"
!$                   # Dernier argument
```

### Configuration dans ~/.bashrc

```bash
HISTSIZE=10000  
HISTFILESIZE=20000  
HISTCONTROL=ignoreboth:erasedups  
HISTTIMEFORMAT="%F %T  "  
shopt -s histappend  
PROMPT_COMMAND='history -a'  
```

### Astuces de productivité

```bash
sudo !!              # Dernière commande avec sudo  
touch f.txt && nano !$   # Créer et ouvrir  
cd -                 # Basculer entre deux dossiers  
^ancien^nouveau      # Substitution rapide
```

### Raccourcis clavier à connaître

| Raccourci | Action |
|-----------|--------|
| **Ctrl+R** | Recherche inversée |
| **Ctrl+A** | Début de ligne |
| **Ctrl+E** | Fin de ligne |
| **Ctrl+U** | Effacer avant curseur |
| **Ctrl+K** | Effacer après curseur |
| **Ctrl+L** | Effacer l'écran |
| **Alt+.** | Dernier argument |

### Règles d'or

1. ✅ Configurez l'historique selon vos besoins
2. ✅ Utilisez Ctrl+R pour chercher rapidement
3. ✅ Ajoutez des timestamps pour la traçabilité
4. ✅ Sauvegardez régulièrement `~/.bash_history`
5. ✅ Utilisez un espace au début pour les commandes sensibles
6. ✅ Prévisualisez avec `:p` avant d'exécuter
7. ⚠️ Attention aux commandes destructives dans l'historique

L'historique des commandes est votre meilleur ami dans le terminal. Une fois maîtrisé, vous ne pourrez plus vous en passer ! Prenez le temps de configurer votre environnement et d'apprendre les raccourcis : votre productivité sera décuplée.

Dans le prochain chapitre, nous découvrirons les alias et la personnalisation du shell pour rendre votre expérience terminal encore plus efficace.

⏭️ [Alias et personnalisation du shell (.bashrc)](/07-le-terminal-et-commandes-de-base/10-alias-et-personnalisation-du-shell.md)
