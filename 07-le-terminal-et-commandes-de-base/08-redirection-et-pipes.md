🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.8 - Redirection et pipes (>, >>, |)

## Introduction

Les redirections et les pipes sont parmi les concepts les plus puissants du terminal Linux. Ils vous permettent de :
- Sauvegarder la sortie d'une commande dans un fichier
- Utiliser la sortie d'une commande comme entrée d'une autre
- Combiner plusieurs commandes pour créer des workflows complexes
- Automatiser des tâches répétitives

**Analogie :** Imaginez les commandes comme des machines dans une usine :
- **Sans redirection** : La machine affiche son résultat à l'écran (vous le voyez et c'est tout)
- **Avec redirection** : Vous stockez le résultat dans un conteneur (fichier)
- **Avec pipe** : Vous connectez les machines entre elles (la sortie de l'une devient l'entrée de la suivante)

Ces outils transforment le terminal en véritable langage de programmation où vous pouvez enchaîner les opérations !

---

## Les flux standards

Avant de commencer, comprenons comment les commandes Linux gèrent les données.

### Les trois flux

Chaque commande Linux utilise trois flux (streams) :

| Flux | Nom | Numéro | Description |
|------|-----|--------|-------------|
| **stdin** | Entrée standard | 0 | D'où vient l'entrée (clavier par défaut) |
| **stdout** | Sortie standard | 1 | Où va la sortie normale (écran par défaut) |
| **stderr** | Erreur standard | 2 | Où vont les erreurs (écran par défaut) |

**Par défaut :**
- Vous tapez au clavier → **stdin**
- La commande affiche son résultat → **stdout** (écran)
- Les erreurs s'affichent → **stderr** (écran)

**Les redirections permettent de changer la destination de ces flux !**

---

## Redirection de sortie : `>` et `>>`

### L'opérateur `>` : Écrire dans un fichier (écrase)

**Syntaxe :**
```bash
commande > fichier
```

**Effet :** Redirige la sortie de la commande vers un fichier.

**⚠️ Important :** Si le fichier existe, il est **écrasé** (son contenu précédent est perdu).

### Exemples avec `>`

#### Exemple 1 : Sauvegarder une liste de fichiers

```bash
ls -l > liste_fichiers.txt
```

Au lieu d'afficher à l'écran, `ls` écrit dans `liste_fichiers.txt`.

**Vérifier :**
```bash
cat liste_fichiers.txt
```

#### Exemple 2 : Sauvegarder la date

```bash
date > date_actuelle.txt
```

Crée un fichier contenant la date et l'heure actuelles.

#### Exemple 3 : Créer un fichier texte simple

```bash
echo "Bonjour, monde !" > message.txt
```

Crée un fichier contenant le texte "Bonjour, monde !".

#### Exemple 4 : Vider un fichier

```bash
> fichier.txt
```

ou

```bash
cat /dev/null > fichier.txt
```

Vide le contenu du fichier (le fichier existe mais est vide).

### L'opérateur `>>` : Ajouter à un fichier (append)

**Syntaxe :**
```bash
commande >> fichier
```

**Effet :** Ajoute la sortie de la commande **à la fin** du fichier sans écraser le contenu existant.

### Exemples avec `>>`

#### Exemple 1 : Journal d'activités

```bash
date >> journal.log  
echo "Système démarré" >> journal.log  
```

Chaque ligne s'ajoute à la fin du fichier.

**Résultat dans journal.log :**
```
Sam 30 nov 2024 10:30:15 CET  
Système démarré  
```

#### Exemple 2 : Collecter des informations système

```bash
echo "=== Informations système ===" > rapport.txt  
date >> rapport.txt  
uname -a >> rapport.txt  
df -h >> rapport.txt  
```

Crée un rapport avec plusieurs informations.

#### Exemple 3 : Historique de recherches

```bash
find ~ -name "*.pdf" >> liste_pdf.txt
```

Ajoute les PDF trouvés à la liste existante.

### Différence entre `>` et `>>`

```bash
# Avec > (écrase)
echo "Ligne 1" > fichier.txt    # Crée "Ligne 1"  
echo "Ligne 2" > fichier.txt    # Remplace par "Ligne 2"  
cat fichier.txt  
# Résultat : Ligne 2

# Avec >> (ajoute)
echo "Ligne 1" > fichier.txt    # Crée "Ligne 1"  
echo "Ligne 2" >> fichier.txt   # Ajoute "Ligne 2"  
cat fichier.txt  
# Résultat :
# Ligne 1
# Ligne 2
```

**Règle simple :**
- **`>`** : "Je veux **remplacer** le contenu"
- **`>>`** : "Je veux **ajouter** à la fin"

---

## Redirection d'entrée : `<`

### L'opérateur `<` : Lire depuis un fichier

**Syntaxe :**
```bash
commande < fichier
```

**Effet :** La commande lit son entrée depuis le fichier au lieu du clavier.

### Exemples avec `<`

#### Exemple 1 : Compter les lignes d'un fichier

```bash
wc -l < fichier.txt
```

Au lieu de taper le texte au clavier, `wc` lit depuis le fichier.

**Note :** Ceci est équivalent à :
```bash
wc -l fichier.txt
```

Mais avec `<`, le nom du fichier n'apparaît pas dans la sortie.

#### Exemple 2 : Envoyer un email (avec mail)

```bash
mail destinataire@example.com < message.txt
```

Envoie un email avec le contenu du fichier.

#### Exemple 3 : Tri de contenu

```bash
sort < liste_non_triee.txt > liste_triee.txt
```

Lit la liste non triée, la trie, et sauvegarde le résultat.

### Utilisation moins courante

En pratique, `<` est moins utilisé que `>` car la plupart des commandes acceptent les fichiers en argument direct :

```bash
# Ces deux commandes sont équivalentes :
cat < fichier.txt  
cat fichier.txt  
```

---

## Les pipes : `|`

### Qu'est-ce qu'un pipe ?

**Le pipe `|` est l'outil le plus puissant du terminal.**

**Syntaxe :**
```bash
commande1 | commande2
```

**Effet :** La **sortie** de commande1 devient l'**entrée** de commande2.

**Analogie :** Comme des tuyaux qui connectent des machines, le résultat de la première machine alimente directement la seconde.

### Exemples simples de pipes

#### Exemple 1 : Compter les fichiers dans un dossier

```bash
ls | wc -l
```

**Explication :**
1. `ls` liste les fichiers
2. `|` envoie cette liste à la commande suivante
3. `wc -l` compte le nombre de lignes (= nombre de fichiers)

#### Exemple 2 : Trier des fichiers

```bash
ls -l | sort -k5 -n
```

**Explication :**
1. `ls -l` affiche les fichiers avec détails
2. `sort -k5 -n` trie selon la 5ème colonne (taille) numériquement

#### Exemple 3 : Chercher un processus

```bash
ps aux | grep firefox
```

**Explication :**
1. `ps aux` liste tous les processus
2. `grep firefox` filtre pour ne garder que ceux contenant "firefox"

#### Exemple 4 : Voir les 10 fichiers les plus gros

```bash
ls -lh | sort -k5 -h -r | head -10
```

**Explication :**
1. `ls -lh` liste les fichiers avec tailles lisibles
2. `sort -k5 -h -r` trie par taille (colonne 5), décroissant
3. `head -10` garde les 10 premiers

### Enchaîner plusieurs pipes

Vous pouvez enchaîner autant de pipes que nécessaire !

```bash
commande1 | commande2 | commande3 | commande4
```

#### Exemple : Analyse de logs

```bash
cat /var/log/syslog | grep error | sort | uniq -c | sort -rn | head -10
```

**Explication :**
1. `cat /var/log/syslog` : Affiche le fichier log
2. `grep error` : Filtre les lignes contenant "error"
3. `sort` : Trie les lignes
4. `uniq -c` : Compte les doublons
5. `sort -rn` : Trie par nombre (décroissant)
6. `head -10` : Garde les 10 erreurs les plus fréquentes

**Résultat :** Top 10 des erreurs dans les logs !

---

## Combiner redirections et pipes

Vous pouvez combiner `|`, `>`, et `>>` dans la même ligne.

### Exemples de combinaisons

#### Exemple 1 : Pipe + redirection de sortie

```bash
ls -l | grep "\.txt" > fichiers_txt.txt
```

**Explication :**
1. `ls -l` liste les fichiers
2. `grep "\.txt"` filtre les fichiers .txt
3. `> fichiers_txt.txt` sauvegarde le résultat dans un fichier

#### Exemple 2 : Recherche et sauvegarde

```bash
find ~ -name "*.pdf" | sort > liste_pdf_triee.txt
```

#### Exemple 3 : Statistiques dans un fichier

```bash
ps aux | grep apache | wc -l > nombre_processus_apache.txt
```

#### Exemple 4 : Log avec horodatage

```bash
echo "Sauvegarde terminée" | cat - <(date) >> journal.log
```

---

## Redirection des erreurs : `2>` et `2>&1`

### Comprendre les numéros de flux

Rappel :
- **1** = stdout (sortie normale)
- **2** = stderr (erreurs)

### L'opérateur `2>` : Rediriger les erreurs

**Syntaxe :**
```bash
commande 2> fichier_erreurs.txt
```

**Effet :** Les erreurs vont dans le fichier, la sortie normale à l'écran.

#### Exemple : Séparer sorties et erreurs

```bash
find / -name "*.conf" > resultats.txt 2> erreurs.txt
```

**Explication :**
- Fichiers trouvés → `resultats.txt`
- Erreurs "Permission denied" → `erreurs.txt`

### L'opérateur `2>&1` : Fusionner sortie et erreurs

**Syntaxe :**
```bash
commande > fichier 2>&1
```

**Effet :** Les erreurs sont redirigées vers la même destination que la sortie normale.

**Note :** L'ordre est important ! `2>&1` doit venir **après** `>`.

#### Exemple : Tout capturer

```bash
./mon_script.sh > log_complet.txt 2>&1
```

Sortie normale ET erreurs vont dans le même fichier.

**Syntaxe moderne (Bash 4+) :**
```bash
./mon_script.sh &> log_complet.txt
```

Équivalent, plus court.

### Ignorer les erreurs : `/dev/null`

**`/dev/null`** est un "trou noir" : tout ce qui y est envoyé disparaît.

#### Exemple : Supprimer les erreurs

```bash
find / -name "*.conf" 2> /dev/null
```

Les erreurs sont supprimées, seuls les résultats s'affichent.

#### Exemple : Tout ignorer

```bash
commande > /dev/null 2>&1
```

Supprime sortie ET erreurs (la commande s'exécute en silence).

**Utilité :** Scripts automatiques où vous ne voulez pas de sortie.

---

## La commande `tee` : Dupliquer le flux

### Qu'est-ce que `tee` ?

**tee** permet de **voir ET sauvegarder** la sortie en même temps.

**Syntaxe :**
```bash
commande | tee fichier
```

**Effet :**
- Affiche la sortie à l'écran
- ET la sauvegarde dans le fichier

**Analogie :** Comme un "T" de plomberie qui divise le flux en deux directions.

### Exemples avec `tee`

#### Exemple 1 : Voir et sauvegarder

```bash
ls -l | tee liste.txt
```

Vous voyez la liste à l'écran ET elle est sauvegardée dans `liste.txt`.

#### Exemple 2 : Installation avec log

```bash
sudo apt update | tee mise_a_jour.log
```

Vous voyez la progression ET un fichier log est créé.

#### Exemple 3 : Ajouter avec tee

```bash
echo "Nouvelle ligne" | tee -a fichier.txt
```

L'option `-a` (append) ajoute au lieu d'écraser.

#### Exemple 4 : Sauvegarder dans plusieurs fichiers

```bash
echo "Important" | tee fichier1.txt fichier2.txt fichier3.txt
```

Écrit dans trois fichiers simultanément.

### Combiner tee avec sudo

**Problème courant :**
```bash
echo "config" > /etc/fichier.conf
# Permission denied (la redirection n'a pas sudo)
```

**Solution avec tee :**
```bash
echo "config" | sudo tee /etc/fichier.conf
```

`tee` s'exécute avec sudo et peut écrire dans `/etc/`.

**Supprimer l'affichage à l'écran :**
```bash
echo "config" | sudo tee /etc/fichier.conf > /dev/null
```

---

## Exemples pratiques avancés

### Exemple 1 : Créer un rapport système

```bash
{
    echo "=== RAPPORT SYSTÈME ==="
    echo "Date: $(date)"
    echo ""
    echo "=== Espace disque ==="
    df -h
    echo ""
    echo "=== Mémoire ==="
    free -h
    echo ""
    echo "=== Processus ==="
    ps aux | head -20
} > rapport_systeme.txt
```

Les accolades `{}` groupent plusieurs commandes.

### Exemple 2 : Sauvegarder les résultats de recherche

```bash
find ~ -type f -mtime -7 | tee fichiers_recents.txt | wc -l
```

**Résultat :**
- Liste sauvegardée dans `fichiers_recents.txt`
- Nombre affiché à l'écran

### Exemple 3 : Logs avec horodatage

```bash
./mon_script.sh 2>&1 | while read line; do
    echo "$(date '+%Y-%m-%d %H:%M:%S') $line"
done | tee -a script.log
```

Ajoute la date/heure devant chaque ligne et sauvegarde.

### Exemple 4 : Recherche dans plusieurs fichiers

```bash
grep -r "TODO" ~/Projets/ 2> /dev/null | grep -v ".git" | sort | uniq > todos.txt
```

**Explication :**
1. Cherche "TODO" récursivement
2. Ignore les erreurs
3. Exclut les fichiers .git
4. Trie et déduplique
5. Sauvegarde dans `todos.txt`

### Exemple 5 : Top 10 des commandes utilisées

```bash
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10
```

Analyse votre historique pour trouver vos commandes favorites.

### Exemple 6 : Surveillance en continu

```bash
tail -f /var/log/syslog | grep --line-buffered "error" | tee -a erreurs_$(date +%Y%m%d).log
```

Surveille les logs en temps réel, filtre les erreurs, et les sauvegarde.

---

## Here Documents : `<<`

### Syntaxe

```bash
commande << DELIMITEUR  
Texte  
sur plusieurs  
lignes  
DELIMITEUR  
```

**Effet :** Permet d'envoyer du texte multi-lignes à une commande.

### Exemples

#### Exemple 1 : Créer un fichier multi-lignes

```bash
cat > fichier.txt << EOF  
Ceci est la ligne 1  
Ceci est la ligne 2  
Ceci est la ligne 3  
EOF  
```

**Note :** `EOF` (End Of File) est conventionnel, mais vous pouvez utiliser n'importe quel mot.

#### Exemple 2 : Script SQL

```bash
mysql -u root -p database << SQL  
SELECT * FROM users;  
UPDATE settings SET value='new' WHERE key='config';  
SQL  
```

#### Exemple 3 : Créer un script

```bash
cat > mon_script.sh << 'END'
#!/bin/bash
echo "Bonjour"  
date  
END  
chmod +x mon_script.sh  
```

### Here Strings : `<<<`

Envoyer une chaîne de caractères directement.

```bash
grep "mot" <<< "voici une phrase avec le mot recherché"
```

Ou :

```bash
variable="Texte important"  
wc -w <<< "$variable"  
```

---

## Astuces et raccourcis

### 1. Sauvegarder et afficher

Au lieu de :
```bash
commande > fichier  
cat fichier  
```

Utilisez :
```bash
commande | tee fichier
```

### 2. Commande silencieuse

```bash
commande &> /dev/null
```

Ou en version longue :
```bash
commande > /dev/null 2>&1
```

### 3. Redirection d'entrée ET sortie

```bash
commande < entree.txt > sortie.txt
```

### 4. Ajouter à plusieurs fichiers

```bash
commande | tee -a fichier1.txt fichier2.txt fichier3.txt > /dev/null
```

### 5. Pipeline avec sudo

**Mauvais :**
```bash
sudo commande1 | commande2
# Seule commande1 a sudo
```

**Bon :**
```bash
sudo bash -c "commande1 | commande2"
# Tout a sudo
```

---

## Erreurs courantes et solutions

### Erreur 1 : Redirection avec sudo

**Problème :**
```bash
sudo echo "texte" > /etc/fichier  
bash: /etc/fichier: Permission denied  
```

**Cause :** La redirection `>` est gérée par le shell, pas par sudo.

**Solutions :**
```bash
echo "texte" | sudo tee /etc/fichier
# ou
sudo sh -c 'echo "texte" > /etc/fichier'
```

### Erreur 2 : Ordre des redirections

**Problème :**
```bash
commande 2>&1 > fichier
# Les erreurs vont à l'écran, pas dans le fichier !
```

**Solution :**
```bash
commande > fichier 2>&1
# L'ordre est important !
```

### Erreur 3 : Pipe vers cd

**Problème :**
```bash
ls | cd Documents
# Ne fonctionne pas !
```

**Cause :** `cd` ne lit pas depuis stdin.

**Solution :**
```bash
cd $(ls -d Documents)
# Ou simplement :
cd Documents
```

### Erreur 4 : Écraser accidentellement un fichier

**Problème :**
```bash
sort fichier.txt > fichier.txt
# Le fichier est vidé !
```

**Cause :** Le fichier est ouvert en écriture avant que `sort` ne le lise.

**Solution :**
```bash
sort fichier.txt > fichier_tmp.txt && mv fichier_tmp.txt fichier.txt
# Ou :
sort -o fichier.txt fichier.txt
```

### Erreur 5 : Pipe avec xargs

**Problème :**
```bash
find . -name "*.txt" | rm
# rm attend des arguments, pas stdin
```

**Solution :**
```bash
find . -name "*.txt" | xargs rm
# xargs convertit stdin en arguments
```

---

## Bonnes pratiques

### 1. Sauvegarder avant de modifier

```bash
cat fichier.txt > fichier.txt.backup
```

### 2. Vérifier avant de rediriger

```bash
commande          # Vérifier le résultat  
commande > fichier # Puis sauvegarder  
```

### 3. Utiliser `>>` pour les logs

Pour les journaux, toujours ajouter, ne pas écraser :
```bash
echo "$(date): Action effectuée" >> journal.log
```

### 4. Tester avec `tee` d'abord

```bash
commande | tee test.txt  # Voir le résultat
# Si OK :
commande > fichier_final.txt
```

### 5. Commenter les pipelines complexes

```bash
# Trouve les 10 fichiers les plus gros
find ~ -type f -exec du -h {} + 2>/dev/null | \
    sort -rh | \                    # Trie par taille
    head -10 | \                    # Garde les 10 premiers
    tee gros_fichiers.txt           # Sauvegarde et affiche
```

---

## Aide-mémoire

### Redirections de base

| Symbole | Effet | Exemple |
|---------|-------|---------|
| `>` | Écrire (écrase) | `ls > fichier.txt` |
| `>>` | Ajouter (append) | `date >> log.txt` |
| `<` | Lire depuis fichier | `wc -l < fichier.txt` |
| `2>` | Rediriger erreurs | `find / 2> erreurs.txt` |
| `2>&1` | Fusionner sortie et erreurs | `commande > tout.txt 2>&1` |
| `&>` | Fusionner (syntaxe courte) | `commande &> tout.txt` |

### Pipes et filtres

| Commande | Effet | Exemple |
|----------|-------|---------|
| `\|` | Pipe (connecter) | `ls \| grep txt` |
| `tee` | Dupliquer | `ls \| tee fichier.txt` |
| `xargs` | Convertir stdin en arguments | `find \| xargs rm` |

### Destinations spéciales

| Destination | Effet |
|-------------|-------|
| `/dev/null` | Supprime (trou noir) |
| `/dev/stdout` | Sortie standard |
| `/dev/stderr` | Erreur standard |

### Combinaisons fréquentes

```bash
commande > fichier                  # Sauvegarder sortie  
commande >> fichier                 # Ajouter sortie  
commande 2> /dev/null               # Ignorer erreurs  
commande &> fichier                 # Tout sauvegarder  
commande | tee fichier              # Voir et sauvegarder  
commande1 | commande2               # Connecter deux commandes  
commande1 | commande2 > fichier     # Pipe puis sauvegarder  
```

---

## Exemples récapitulatifs

### Workflow 1 : Analyse de logs

```bash
# Extraire les erreurs des dernières 24h
sudo grep "error" /var/log/syslog | \
    grep "$(date +%Y-%m-%d)" | \
    sort | \
    uniq -c | \
    sort -rn > erreurs_du_jour.txt
```

### Workflow 2 : Inventaire système

```bash
# Créer un inventaire complet
{
    echo "=== Inventaire système $(date) ==="
    echo ""
    echo "Hostname: $(hostname)"
    echo "Kernel: $(uname -r)"
    echo ""
    df -h | grep "^/dev"
    echo ""
    free -h
} | tee inventaire_$(date +%Y%m%d).txt
```

### Workflow 3 : Nettoyage et rapport

```bash
# Trouver et lister les gros fichiers
find ~ -type f -size +100M 2>/dev/null | \
    while read file; do
        ls -lh "$file"
    done | \
    sort -k5 -rh | \
    tee gros_fichiers.txt | \
    wc -l
```

### Workflow 4 : Surveillance continue

```bash
# Surveiller l'utilisation CPU
while true; do
    date >> cpu_usage.log
    top -bn1 | grep "Cpu(s)" >> cpu_usage.log
    sleep 60
done &
```

---

## Résumé

### Concepts clés

**Les trois flux :**
- **stdin** (0) : Entrée
- **stdout** (1) : Sortie normale
- **stderr** (2) : Erreurs

**Redirections de sortie :**
- **`>`** : Écrire (écrase le fichier)
- **`>>`** : Ajouter (garde le contenu existant)

**Redirection d'entrée :**
- **`<`** : Lire depuis un fichier

**Pipes :**
- **`|`** : Connecter la sortie d'une commande à l'entrée d'une autre

**Redirections d'erreurs :**
- **`2>`** : Rediriger les erreurs
- **`2>&1`** : Fusionner erreurs et sortie
- **`&>`** : Raccourci pour tout rediriger

**Outils complémentaires :**
- **`tee`** : Dupliquer (afficher ET sauvegarder)
- **`/dev/null`** : Supprimer (trou noir)

### Commandes essentielles

```bash
# Sauvegarder une sortie
ls > fichiers.txt

# Ajouter à un fichier
date >> journal.log

# Connecter des commandes
ps aux | grep firefox

# Tout sauvegarder (sortie + erreurs)
./script.sh &> log.txt

# Voir et sauvegarder
ls | tee liste.txt

# Ignorer les erreurs
find / -name "*.conf" 2> /dev/null

# Pipeline complexe
cat fichier | grep "mot" | sort | uniq > resultat.txt
```

### Règles d'or

1. ✅ **`>`** écrase, **`>>`** ajoute
2. ✅ Vérifiez le résultat avant de rediriger
3. ✅ Utilisez `tee` pour voir et sauvegarder
4. ✅ `/dev/null` pour supprimer ce dont vous n'avez pas besoin
5. ✅ L'ordre compte : `> fichier 2>&1` (pas l'inverse)
6. ✅ Testez les pipelines étape par étape
7. ⚠️ Attention à ne pas écraser des fichiers importants

Les redirections et pipes transforment le terminal en véritable usine de traitement de données. Avec la pratique, vous créerez des workflows puissants en une seule ligne !

Dans le prochain chapitre, nous découvrirons l'historique des commandes et les astuces pour optimiser votre productivité dans le terminal.

⏭️ [Historique des commandes et astuces](/07-le-terminal-et-commandes-de-base/09-historique-des-commandes-et-astuces.md)
