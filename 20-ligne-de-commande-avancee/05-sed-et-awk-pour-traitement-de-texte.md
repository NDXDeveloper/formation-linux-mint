🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Sed et Awk pour traitement de texte

## Introduction

**Sed** (Stream Editor) et **Awk** sont deux outils légendaires de manipulation de texte sous Linux. Ils existent depuis les années 1970 et sont toujours utilisés quotidiennement par des millions d'administrateurs système et développeurs.

Imaginez-les comme des **couteaux suisses du traitement de texte** : ils peuvent chercher, remplacer, extraire, filtrer, transformer des fichiers texte de manière incroyablement rapide et efficace.

### Sed vs Awk : Quand utiliser quoi ?

**Sed** :
- Spécialisé dans le **remplacement** et la **modification** de texte
- Excellent pour des transformations ligne par ligne
- Syntaxe plus simple pour des opérations basiques
- Idéal pour : remplacer du texte, supprimer des lignes, insérer du texte

**Awk** :
- Spécialisé dans le **traitement de données tabulaires** (colonnes)
- Excellent pour l'analyse et l'extraction
- Syntaxe plus proche de la programmation
- Idéal pour : extraire des colonnes, faire des calculs, filtrer selon des conditions

**Analogie simple** :
- **Sed** = Correcteur automatique de texte
- **Awk** = Tableur en ligne de commande

### Pourquoi apprendre sed et awk ?

- **Rapidité** : Traitent des millions de lignes en secondes
- **Automatisation** : Parfaits pour les scripts de traitement de données
- **Universels** : Disponibles sur tous les systèmes Unix/Linux
- **Puissance** : Peuvent remplacer des dizaines de lignes de code Python ou autre
- **Légers** : Pas besoin d'installer des dépendances lourdes

---

## Partie 1 : Sed - Le Stream Editor

### Qu'est-ce que sed ?

Sed lit un fichier ligne par ligne, applique des transformations selon vos instructions, et affiche le résultat. Par défaut, sed **n'affiche pas** le résultat à l'écran sans modifier le fichier original.

### Syntaxe de base

```bash
sed 'commande' fichier.txt
```

ou pour modifier le fichier directement :

```bash
sed -i 'commande' fichier.txt
```

### Commande s (substitution) - La plus utilisée

La commande `s` remplace du texte.

**Format** :
```bash
sed 's/ancien/nouveau/' fichier.txt
```

**Exemple simple** :

```bash
# Créer un fichier de test
echo "J'aime les chats" > test.txt

# Remplacer "chats" par "chiens"
sed 's/chats/chiens/' test.txt
# Résultat : J'aime les chiens
```

### Les drapeaux (flags) de substitution

```bash
# g : remplacer TOUTES les occurrences sur la ligne (pas juste la première)
sed 's/chat/chien/g' fichier.txt

# i : insensible à la casse (ignore majuscules/minuscules)
sed 's/chat/chien/gi' fichier.txt

# 2 : remplacer seulement la 2e occurrence
sed 's/chat/chien/2' fichier.txt

# p : afficher les lignes modifiées
sed -n 's/chat/chien/p' fichier.txt
```

### Exemples pratiques de substitution

```bash
# Remplacer tous les espaces par des underscores
sed 's/ /_/g' fichier.txt

# Supprimer tous les espaces
sed 's/ //g' fichier.txt

# Remplacer plusieurs espaces consécutifs par un seul
sed 's/  */ /g' fichier.txt

# Supprimer les espaces en début de ligne
sed 's/^ *//' fichier.txt

# Supprimer les espaces en fin de ligne
sed 's/ *$//' fichier.txt

# Remplacer les fins de ligne Windows (CRLF) par Unix (LF)
sed 's/\r$//' fichier.txt

# Doubler toutes les voyelles
sed 's/[aeiou]/&&/g' fichier.txt
# & représente le texte correspondant
```

### Modification en place (modifier le fichier)

```bash
# Modifier directement le fichier
sed -i 's/ancien/nouveau/g' fichier.txt

# Créer une sauvegarde avant modification
sed -i.bak 's/ancien/nouveau/g' fichier.txt
# Crée fichier.txt.bak avec l'original
```

### Adressage : cibler des lignes spécifiques

```bash
# Remplacer seulement sur la ligne 3
sed '3s/chat/chien/' fichier.txt

# Remplacer sur les lignes 2 à 5
sed '2,5s/chat/chien/' fichier.txt

# Remplacer sur toutes les lignes sauf la première
sed '2,$s/chat/chien/' fichier.txt

# Remplacer uniquement sur les lignes contenant "motif"
sed '/motif/s/chat/chien/' fichier.txt

# Remplacer sur les lignes qui ne contiennent PAS "motif"
sed '/motif/!s/chat/chien/' fichier.txt
```

### Commande d (delete) - Supprimer des lignes

```bash
# Supprimer la ligne 3
sed '3d' fichier.txt

# Supprimer les lignes 2 à 5
sed '2,5d' fichier.txt

# Supprimer les lignes vides
sed '/^$/d' fichier.txt

# Supprimer les lignes commençant par #
sed '/^#/d' fichier.txt

# Supprimer toutes les lignes contenant "erreur"
sed '/erreur/d' fichier.txt

# Supprimer la dernière ligne
sed '$d' fichier.txt

# Supprimer toutes les lignes sauf celles contenant "important"
sed '/important/!d' fichier.txt
```

### Commande p (print) - Afficher des lignes

**Note** : Utilisez toujours `-n` avec `p` pour éviter la double impression.

```bash
# Afficher seulement la ligne 3
sed -n '3p' fichier.txt

# Afficher les lignes 2 à 5
sed -n '2,5p' fichier.txt

# Afficher les lignes contenant "erreur"
sed -n '/erreur/p' fichier.txt

# Afficher la dernière ligne
sed -n '$p' fichier.txt

# Afficher les lignes 10 à 20 et 30 à 40
sed -n '10,20p; 30,40p' fichier.txt
```

### Commandes a, i, c - Ajouter, insérer, changer

```bash
# a : Ajouter du texte APRÈS une ligne
sed '3a\Nouvelle ligne après la ligne 3' fichier.txt

# i : Insérer du texte AVANT une ligne
sed '3i\Nouvelle ligne avant la ligne 3' fichier.txt

# c : Changer (remplacer) une ligne entière
sed '3c\Cette ligne remplace complètement la ligne 3' fichier.txt

# Ajouter une ligne après chaque ligne contenant "motif"
sed '/motif/a\Ligne ajoutée' fichier.txt

# Insérer une ligne au début du fichier
sed '1i\=== EN-TÊTE ===' fichier.txt

# Ajouter une ligne à la fin du fichier
sed '$a\=== FIN ===' fichier.txt
```

### Utilisation de plusieurs commandes

```bash
# Option 1 : Utiliser -e pour chaque commande
sed -e 's/chat/chien/g' -e 's/rouge/bleu/g' fichier.txt

# Option 2 : Séparer avec ;
sed 's/chat/chien/g; s/rouge/bleu/g' fichier.txt

# Option 3 : Utiliser des retours à la ligne
sed '
s/chat/chien/g
s/rouge/bleu/g
s/petit/grand/g
' fichier.txt
```

### Groupes de capture et références arrière

```bash
# \(...\) capture un groupe
# \1, \2, etc. réutilisent ces groupes

# Inverser deux mots : "Dupont Jean" → "Jean Dupont"
echo "Dupont Jean" | sed 's/\(.*\) \(.*\)/\2 \1/'

# Doubler chaque mot
echo "Bonjour monde" | sed 's/\([^ ]*\)/\1 \1/g'
# Résultat : Bonjour Bonjour monde monde

# Mettre en majuscule la première lettre (avec \U)
echo "bonjour" | sed 's/^./\U&/'
# Résultat : Bonjour

# Extraire l'extension d'un fichier
echo "document.pdf" | sed 's/.*\.\(.*\)/\1/'
# Résultat : pdf

# Formater une date : JJ/MM/AAAA → AAAA-MM-JJ
echo "25/12/2024" | sed 's|\([0-9]\{2\}\)/\([0-9]\{2\}\)/\([0-9]\{4\}\)|\3-\2-\1|'
# Résultat : 2024-12-25
```

### Changer le séparateur

Par défaut, le séparateur est `/`, mais vous pouvez utiliser n'importe quel caractère :

```bash
# Utile pour les chemins de fichiers
# Au lieu de :
sed 's/\/home\/utilisateur/\/home\/admin/g' fichier.txt

# Utilisez | ou # comme séparateur :
sed 's|/home/utilisateur|/home/admin|g' fichier.txt
sed 's#/home/utilisateur#/home/admin#g' fichier.txt
```

### Exemples pratiques sed

#### Nettoyage de fichiers

```bash
# Supprimer les lignes vides ET les commentaires
sed '/^$/d; /^#/d' config.conf

# Nettoyer un fichier CSV (supprimer espaces inutiles)
sed 's/, */,/g; s/ *,/,/g' data.csv

# Convertir majuscules en minuscules (ligne entière)
sed 's/.*/\L&/' fichier.txt

# Numéroter les lignes
sed = fichier.txt | sed 'N;s/\n/\t/'
```

#### Extraction de données

```bash
# Extraire uniquement les adresses email
sed -n 's/.*\([a-zA-Z0-9._%+-]\+@[a-zA-Z0-9.-]\+\.[a-zA-Z]\{2,\}\).*/\1/p' fichier.txt

# Extraire les URLs
sed -n 's|.*\(https\?://[^ ]*\).*|\1|p' fichier.txt
```

#### Transformation de format

```bash
# Convertir un fichier CSV en TSV (tab-separated)
sed 's/,/\t/g' fichier.csv

# Ajouter des guillemets autour de chaque champ CSV
sed 's/\([^,]*\)/"\1"/g' fichier.csv

# Transformer une liste en JSON simple
sed '1s/^/[\n"/; $!s/$/",/; $s/$/"\n]/' liste.txt
```

---

## Partie 2 : Awk - Le langage de traitement de données

### Qu'est-ce qu'awk ?

Awk est un langage de programmation conçu pour traiter des données textuelles structurées (avec des colonnes/champs). Il est particulièrement puissant pour analyser des fichiers CSV, TSV, des logs, etc.

### Syntaxe de base

```bash
awk 'programme' fichier.txt
```

ou

```bash
awk '{commandes}' fichier.txt
```

### Concept fondamental : les champs

Awk divise automatiquement chaque ligne en **champs** (colonnes) :

- `$1` = premier champ
- `$2` = deuxième champ
- `$3` = troisième champ
- `$0` = la ligne entière
- `NF` = nombre de champs dans la ligne
- `NR` = numéro de la ligne actuelle

Par défaut, le séparateur est l'espace ou la tabulation.

### Premier exemple simple

```bash
# Fichier : personnes.txt
# Jean Dupont 35
# Marie Martin 28
# Pierre Durant 42

# Afficher seulement les prénoms (1er champ)
awk '{print $1}' personnes.txt
# Résultat :
# Jean
# Marie
# Pierre

# Afficher prénoms et âges
awk '{print $1, $3}' personnes.txt
# Résultat :
# Jean 35
# Marie 28
# Pierre 42

# Afficher avec du texte personnalisé
awk '{print $1, "a", $3, "ans"}' personnes.txt
# Résultat :
# Jean a 35 ans
# Marie a 28 ans
# Pierre a 42 ans
```

### Changer le séparateur de champs (-F)

```bash
# Fichier CSV : data.csv
# Jean,Dupont,35
# Marie,Martin,28

# Utiliser la virgule comme séparateur
awk -F',' '{print $1, $2}' data.csv
# Résultat :
# Jean Dupont
# Marie Martin

# Utiliser : comme séparateur (utile pour /etc/passwd)
awk -F':' '{print $1, $6}' /etc/passwd
# Affiche utilisateur et répertoire personnel
```

### Conditions et filtres

```bash
# Afficher seulement les lignes où le 3e champ > 30
awk '$3 > 30' personnes.txt

# Afficher seulement les lignes où le 1er champ est "Marie"
awk '$1 == "Marie"' personnes.txt

# Afficher les lignes qui ne commencent PAS par #
awk '!/^#/' fichier.txt

# Afficher les lignes contenant "erreur"
awk '/erreur/' log.txt

# Afficher les lignes où le 2e champ contient "test"
awk '$2 ~ /test/' fichier.txt
```

### Opérateurs de comparaison

```bash
==    # Égal
!=    # Différent
>     # Supérieur
<     # Inférieur
>=    # Supérieur ou égal
<=    # Inférieur ou égal
~     # Correspond à (regex)
!~    # Ne correspond pas à (regex)
```

### BEGIN et END

```bash
# BEGIN : exécuté AVANT de lire le fichier
# END : exécuté APRÈS avoir lu tout le fichier

# Ajouter un en-tête et un pied
awk 'BEGIN {print "=== LISTE DES PERSONNES ==="} {print $1, $2} END {print "=== FIN ==="}' personnes.txt

# Compter les lignes
awk 'END {print NR}' fichier.txt

# Calculer une moyenne
awk '{sum += $3; count++} END {print "Moyenne:", sum/count}' personnes.txt
```

### Variables intégrées utiles

```bash
NR     # Numéro de la ligne actuelle
NF     # Nombre de champs dans la ligne
FS     # Séparateur de champs (Field Separator)
OFS    # Séparateur de sortie (Output Field Separator)
RS     # Séparateur d'enregistrements (Record Separator)
ORS    # Séparateur de sortie d'enregistrements
```

**Exemples** :

```bash
# Afficher le numéro de ligne avant chaque ligne
awk '{print NR, $0}' fichier.txt

# Afficher les lignes qui ont exactement 3 champs
awk 'NF == 3' fichier.txt

# Changer le séparateur de sortie
awk 'BEGIN {OFS="|"} {print $1, $2, $3}' fichier.txt
# Résultat : Jean|Dupont|35
```

### Calculs et opérations mathématiques

```bash
# Addition de tous les nombres dans la 3e colonne
awk '{sum += $3} END {print sum}' fichier.txt

# Moyenne
awk '{sum += $3; count++} END {print sum/count}' fichier.txt

# Maximum
awk 'BEGIN {max=0} {if ($3 > max) max=$3} END {print max}' fichier.txt

# Compter les lignes
awk 'END {print NR}' fichier.txt

# Multiplier deux colonnes
awk '{print $1, $2, $1 * $2}' fichier.txt
```

### Fonctions de chaînes

```bash
# length() : longueur d'une chaîne
awk '{print $1, length($1)}' fichier.txt

# toupper() : convertir en majuscules
awk '{print toupper($1)}' fichier.txt

# tolower() : convertir en minuscules
awk '{print tolower($1)}' fichier.txt

# substr() : extraire une sous-chaîne
awk '{print substr($1, 1, 3)}' fichier.txt  # 3 premiers caractères

# gsub() : remplacer globalement
awk '{gsub(/a/, "A"); print}' fichier.txt

# sub() : remplacer la première occurrence
awk '{sub(/a/, "A"); print}' fichier.txt

# split() : diviser une chaîne
awk '{split($0, arr, ","); print arr[1]}' fichier.txt
```

### Tableaux associatifs

```bash
# Compter les occurrences de chaque mot
awk '{for(i=1; i<=NF; i++) count[$i]++} END {for(word in count) print word, count[word]}' fichier.txt

# Compter les occurrences par catégorie (2e colonne)
awk '{count[$2]++} END {for(cat in count) print cat, count[cat]}' fichier.txt
```

### Structures de contrôle

#### If-else

```bash
# Catégoriser selon l'âge
awk '{
    if ($3 < 18)
        print $1, "est mineur"
    else if ($3 < 65)
        print $1, "est adulte"
    else
        print $1, "est senior"
}' personnes.txt
```

#### For loop

```bash
# Afficher tous les champs avec un préfixe
awk '{
    for(i=1; i<=NF; i++)
        print "Champ " i ": " $i
}' fichier.txt
```

#### While loop

```bash
# Additionner tous les champs d'une ligne
awk '{
    i=1; sum=0
    while(i<=NF) {
        sum += $i
        i++
    }
    print "Somme:", sum
}' fichier.txt
```

### Exemples pratiques awk

#### Analyse de logs

```bash
# Compter les erreurs par type
awk '/ERROR/ {count[$4]++} END {for(type in count) print type, count[type]}' /var/log/syslog

# Afficher les 10 IPs les plus fréquentes dans un log web
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -10

# Filtrer les erreurs d'une période spécifique
awk '$3 >= "2024-01-01" && $3 <= "2024-01-31" && /ERROR/' log.txt
```

#### Traitement de fichiers CSV

```bash
# Fichier CSV : ventes.csv
# Produit,Quantité,Prix
# Pommes,10,2.50
# Oranges,15,3.00
# Bananes,8,1.80

# Calculer le total de chaque ligne
awk -F',' 'NR>1 {print $1, $2*$3}' ventes.csv

# Calculer le chiffre d'affaires total
awk -F',' 'NR>1 {sum += $2*$3} END {print "Total:", sum}' ventes.csv

# Afficher avec formatage
awk -F',' 'NR>1 {printf "%s : %.2f€\n", $1, $2*$3}' ventes.csv
```

#### Extraction de colonnes spécifiques

```bash
# Extraire les colonnes 1, 3 et 5
awk '{print $1, $3, $5}' fichier.txt

# Inverser l'ordre des colonnes
awk '{print $3, $2, $1}' fichier.txt

# Afficher toutes les colonnes sauf la première
awk '{$1=""; print $0}' fichier.txt

# Afficher la dernière colonne
awk '{print $NF}' fichier.txt

# Afficher l'avant-dernière colonne
awk '{print $(NF-1)}' fichier.txt
```

#### Reformatage de données

```bash
# Convertir CSV en format lisible
awk -F',' '{printf "%-20s %-10s %-10s\n", $1, $2, $3}' data.csv

# Créer un rapport formaté
awk 'BEGIN {print "RAPPORT DE VENTES\n=================="}
     {printf "%-15s %5d unités à %6.2f€\n", $1, $2, $3}
     END {print "=================="}' ventes.txt
```

#### Filtrage avancé

```bash
# Lignes où la 3e colonne est entre 20 et 40
awk '$3 >= 20 && $3 <= 40' fichier.txt

# Lignes avec plus de 5 champs
awk 'NF > 5' fichier.txt

# Lignes où le 2e champ contient "test" ET le 3e > 100
awk '$2 ~ /test/ && $3 > 100' fichier.txt

# Lignes impaires seulement
awk 'NR % 2 == 1' fichier.txt

# Une ligne sur trois
awk 'NR % 3 == 0' fichier.txt
```

### Printf pour un formatage avancé

```bash
# Formatage de base
awk '{printf "%-10s %5d\n", $1, $2}' fichier.txt
# %-10s : chaîne alignée à gauche sur 10 caractères
# %5d : nombre aligné à droite sur 5 caractères

# Nombres décimaux
awk '{printf "%.2f\n", $1}' fichier.txt
# %.2f : 2 décimales

# Combinaison
awk '{printf "%s : %6.2f€ (%d%%)\n", $1, $2, $3}' fichier.txt
```

---

## Comparaison sed vs awk

### Quand utiliser sed ?

✅ **Utilisez sed pour** :
- Remplacer du texte simple
- Supprimer des lignes
- Transformations ligne par ligne simples
- Modifications rapides de configuration
- Scripts shell simples

❌ **N'utilisez PAS sed pour** :
- Traiter des données en colonnes
- Faire des calculs
- Logique conditionnelle complexe
- Agréger des données

### Quand utiliser awk ?

✅ **Utilisez awk pour** :
- Extraire des colonnes spécifiques
- Faire des calculs et statistiques
- Filtrer selon des conditions
- Reformater des données tabulaires
- Créer des rapports

❌ **N'utilisez PAS awk pour** :
- Remplacements de texte simples (sed est plus rapide)
- Modifications complexes de texte non structuré
- Traitement de très gros fichiers en mémoire

### Tableau comparatif

| Tâche | Sed | Awk |
|-------|-----|-----|
| Remplacer "chat" par "chien" | `sed 's/chat/chien/g'` | `awk '{gsub(/chat/, "chien"); print}'` |
| Supprimer les lignes vides | `sed '/^$/d'` | `awk 'NF > 0'` |
| Afficher la 3e colonne | Difficile | `awk '{print $3}'` |
| Calculer une somme | Impossible | `awk '{sum+=$1} END {print sum}'` |
| Supprimer les lignes 5-10 | `sed '5,10d'` | `awk 'NR<5 || NR>10'` |
| Filtrer valeur > 100 | Difficile | `awk '$3 > 100'` |

---

## Combinaison de sed et awk

Souvent, la solution optimale combine sed ET awk dans un pipeline :

```bash
# Nettoyer puis extraire
sed '/^#/d; /^$/d' fichier.txt | awk '{print $2}'

# Remplacer puis calculer
sed 's/,/ /g' data.csv | awk '{sum += $3} END {print sum}'

# Pipeline complet
cat access.log | \
  sed 's/^.*\[//; s/\].*$//' | \  # Extraire les dates
  awk '{count[$1]++} END {for(d in count) print d, count[d]}' | \  # Compter par date
  sort -k2 -rn  # Trier par fréquence
```

---

## Cas d'usage pratiques combinés

### Analyse de fichier de log Apache

```bash
# Fichier : access.log
# 192.168.1.1 - - [10/Jan/2024:13:55:36] "GET /index.html HTTP/1.1" 200 1234

# Top 10 des IPs
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -10

# URLs les plus consultées
awk '{print $7}' access.log | sort | uniq -c | sort -rn | head -10

# Nombre de requêtes par code de statut
awk '{print $9}' access.log | sort | uniq -c

# Bande passante totale
awk '{sum += $10} END {print "Total:", sum/1024/1024, "MB"}' access.log

# Trafic par heure
awk '{split($4, time, ":"); print time[2]}' access.log | sort | uniq -c
```

### Traitement de données CSV

```bash
# Fichier : employes.csv
# Nom,Prénom,Département,Salaire
# Dupont,Jean,IT,45000
# Martin,Marie,RH,38000
# Durant,Pierre,IT,52000

# Salaire moyen par département
awk -F',' 'NR>1 {dept[$3]+=$4; count[$3]++}
           END {for(d in dept) printf "%s: %.2f\n", d, dept[d]/count[d]}' employes.csv

# Employés avec salaire > 40000
awk -F',' 'NR>1 && $4 > 40000 {print $2, $1}' employes.csv

# Convertir en format lisible
awk -F',' 'BEGIN {printf "%-15s %-15s %-15s %10s\n", "Nom", "Prénom", "Dept", "Salaire"}
           NR>1 {printf "%-15s %-15s %-15s %10d\n", $1, $2, $3, $4}' employes.csv
```

### Nettoyage de données

```bash
# Supprimer commentaires, lignes vides, et extraire colonnes
sed '/^#/d; /^$/d' fichier.txt | awk '{print $1, $3}'

# Normaliser les espaces et extraire
sed 's/  */ /g; s/^ *//; s/ *$//' fichier.txt | awk -F' ' '{print $2}'

# Supprimer doublons et trier
awk '!seen[$0]++' fichier.txt | sort

# Filtrer et reformater
awk '$3 > 100 {printf "%s,%s,%.2f\n", $1, $2, $3*1.1}' data.txt
```

### Génération de rapports

```bash
# Rapport de ventes
awk 'BEGIN {
    print "╔════════════════════════════════════════╗"
    print "║       RAPPORT DE VENTES MENSUEL        ║"
    print "╠════════════════════════════════════════╣"
}
{
    total += $3
    printf "║ %-20s : %10.2f€ ║\n", $1, $3
}
END {
    print "╠════════════════════════════════════════╣"
    printf "║ %-20s : %10.2f€ ║\n", "TOTAL", total
    print "╚════════════════════════════════════════╝"
}' ventes.txt
```

### Extraction d'informations système

```bash
# Utilisateurs avec shell bash
awk -F':' '$7 ~ /bash/ {print $1, $6}' /etc/passwd

# Processus consommant le plus de mémoire
ps aux | awk 'NR>1 {print $11, $4}' | sort -k2 -rn | head -10

# Espace disque par répertoire
du -sh /* | awk '{print $2, $1}' | sort -k2 -h

# Top 5 des plus gros fichiers
find . -type f -exec du -h {} + | sort -rh | head -5 | awk '{print $2, $1}'
```

---

## Scripts sed et awk complexes

### Script sed pour nettoyage HTML basique

```bash
#!/bin/bash
# clean-html.sh - Supprime les balises HTML basiques

sed '
# Supprimer les balises HTML
s/<[^>]*>//g

# Supprimer les espaces multiples
s/  */ /g

# Supprimer espaces début/fin de ligne
s/^ *//
s/ *$//

# Supprimer lignes vides
/^$/d
' "$1"
```

### Script awk pour analyse de logs

```bash
#!/bin/awk -f
# analyze-log.awk - Analyse de logs serveur

BEGIN {
    print "Analyse des logs en cours..."
    print "================================"
}

# Compter par code de statut
{
    status[$9]++
    total++
}

# Calculer la bande passante
{
    bandwidth += $10
}

# Tracker les IPs
{
    ips[$1]++
}

END {
    print "\n=== Statistiques globales ==="
    print "Total de requêtes:", total
    printf "Bande passante: %.2f MB\n", bandwidth/1024/1024

    print "\n=== Codes de statut ==="
    for (code in status) {
        printf "%s: %d (%.1f%%)\n", code, status[code], status[code]/total*100
    }

    print "\n=== Top 10 IPs ==="
    # Note: Pour un vrai tri, utilisez sort après awk
    for (ip in ips) {
        if (ips[ip] > 10)  # Seulement IPs avec >10 requêtes
            print ip, ips[ip]
    }
}
```

Usage :
```bash
awk -f analyze-log.awk access.log
```

---

## Astuces et bonnes pratiques

### Pour sed

1. **Toujours faire une sauvegarde avec -i**
   ```bash
   sed -i.bak 's/ancien/nouveau/g' fichier.txt
   ```

2. **Tester avant de modifier**
   ```bash
   # Tester d'abord
   sed 's/ancien/nouveau/g' fichier.txt
   # Si OK, modifier
   sed -i 's/ancien/nouveau/g' fichier.txt
   ```

3. **Utiliser -n avec p pour filtrer**
   ```bash
   sed -n '/motif/p' fichier.txt
   ```

4. **Changer le séparateur pour les chemins**
   ```bash
   sed 's|/old/path|/new/path|g' fichier.txt
   ```

5. **Commenter vos expressions complexes**
   ```bash
   sed '
   # Supprimer les commentaires
   /^#/d
   # Supprimer les lignes vides
   /^$/d
   # Remplacer les tabs par des espaces
   s/\t/ /g
   ' fichier.txt
   ```

### Pour awk

1. **Nommer vos champs pour la lisibilité**
   ```bash
   awk '{nom=$1; age=$3; print nom, "a", age, "ans"}' fichier.txt
   ```

2. **Utiliser BEGIN pour l'initialisation**
   ```bash
   awk 'BEGIN {FS=","; OFS="|"} {print $1, $2}' fichier.csv
   ```

3. **Tester vos expressions avec des fichiers simples**
   ```bash
   echo -e "1 2 3\n4 5 6" | awk '{print $1 + $2 + $3}'
   ```

4. **Utiliser -v pour passer des variables**
   ```bash
   seuil=100
   awk -v s=$seuil '$3 > s' fichier.txt
   ```

5. **Sauvegarder vos scripts awk dans des fichiers**
   ```bash
   # script.awk
   #!/usr/bin/awk -f
   BEGIN { FS="," }
   { print $1, $2 }

   # Utilisation
   chmod +x script.awk
   ./script.awk fichier.csv
   ```

### Débogage

```bash
# Pour sed : afficher les commandes exécutées
sed --debug 's/chat/chien/g' fichier.txt

# Pour awk : afficher les variables
awk '{print "NR=" NR, "NF=" NF, "$0=" $0}' fichier.txt

# Ajouter des prints de débogage
awk '{
    print "Debug: $1=" $1, "$2=" $2 > "/dev/stderr"
    print $1, $2
}' fichier.txt
```

---

## Pièges courants à éviter

### Sed

❌ **Piège 1** : Oublier le g (global)
```bash
# Remplace seulement la première occurrence
sed 's/chat/chien/' fichier.txt

# Remplace toutes les occurrences
sed 's/chat/chien/g' fichier.txt
```

❌ **Piège 2** : Ne pas échapper les caractères spéciaux
```bash
# ❌ Mauvais
sed 's/prix: $10/prix: $20/' fichier.txt

# ✅ Bon
sed 's/prix: \$10/prix: \$20/' fichier.txt
```

❌ **Piège 3** : Oublier -n avec p
```bash
# ❌ Affiche deux fois
sed '/motif/p' fichier.txt

# ✅ Affiche une fois
sed -n '/motif/p' fichier.txt
```

### Awk

❌ **Piège 1** : Confondre = et ==
```bash
# ❌ Assigne (toujours vrai)
awk '$1 = "test"' fichier.txt

# ✅ Compare
awk '$1 == "test"' fichier.txt
```

❌ **Piège 2** : Oublier de spécifier le séparateur
```bash
# ❌ Ne marchera pas bien avec CSV
awk '{print $2}' fichier.csv

# ✅ Bon
awk -F',' '{print $2}' fichier.csv
```

❌ **Piège 3** : Utiliser print au lieu de printf pour le formatage
```bash
# ❌ Pas aligné
awk '{print $1, $2}' fichier.txt

# ✅ Bien formaté
awk '{printf "%-10s %5d\n", $1, $2}' fichier.txt
```

---

## Aide-mémoire rapide

### Sed - Commandes essentielles

```bash
s/ancien/nouveau/     # Substitution
s/ancien/nouveau/g    # Substitution globale
s/ancien/nouveau/gi   # Insensible à la casse
10s/ancien/nouveau/   # Ligne 10 seulement
10,20s/ancien/nouveau/ # Lignes 10 à 20
/motif/s/ancien/nouveau/ # Lignes avec "motif"

d                     # Supprimer
p                     # Afficher
a\texte              # Ajouter après
i\texte              # Insérer avant
c\texte              # Changer (remplacer)

-i                    # Modifier en place
-i.bak               # Modifier avec sauvegarde
-n                    # Mode silencieux
-e                    # Commandes multiples
```

### Awk - Commandes essentielles

```bash
{print $1}           # Afficher 1er champ
{print $1, $3}       # Afficher champs 1 et 3
{print $0}           # Afficher ligne entière
{print $NF}          # Dernier champ

-F','                # Séparateur virgule
-F':'                # Séparateur deux-points

/motif/              # Lignes contenant "motif"
$3 > 100             # Champ 3 > 100
$1 == "test"         # Champ 1 égal à "test"
NF > 5               # Plus de 5 champs
NR > 10              # Après ligne 10

BEGIN {}             # Avant traitement
END {}               # Après traitement

{sum += $1}          # Somme
{count++}            # Compteur
```

---

## Ressources pour aller plus loin

### Documentation

```bash
man sed
man awk
info sed
info gawk
```

### Sites web

- **Sed** :
  - [GNU Sed Manual](https://www.gnu.org/software/sed/manual/)
  - [sed.sourceforge.net](http://sed.sourceforge.net/)

- **Awk** :
  - [GNU Awk Manual](https://www.gnu.org/software/gawk/manual/)
  - [awk.info](https://awk.info/)

### Livres

- "sed & awk" par Dale Dougherty et Arnold Robbins (O'Reilly)
- "The AWK Programming Language" par Aho, Kernighan et Weinberger

### Pratique en ligne

- [SedTest.com](https://sed.js.org/) - Tester sed en ligne
- [AWK Playground](https://awk.js.org/) - Tester awk en ligne

---

## Conclusion

Sed et awk sont des outils incroyablement puissants pour le traitement de texte sous Linux. Bien qu'ils aient plus de 40 ans, ils restent incontournables car :

- ✅ **Rapides** - Traitent des millions de lignes en secondes
- ✅ **Légers** - Pas de dépendances, toujours disponibles
- ✅ **Puissants** - Peuvent remplacer des scripts complexes
- ✅ **Universels** - Fonctionnent partout où il y a Unix/Linux

**Récapitulatif** :

- **Sed** = Modifications de texte ligne par ligne (remplacer, supprimer, insérer)
- **Awk** = Traitement de données en colonnes (extraire, calculer, filtrer)

**Progression recommandée** :

1. Maîtrisez les commandes de base (s, d, p pour sed ; print, $1, $2 pour awk)
2. Apprenez les regex (indispensables pour les deux)
3. Pratiquez sur vos propres fichiers (logs, CSV, configurations)
4. Créez des scripts réutilisables
5. Combinez sed, awk, grep dans des pipelines

Avec sed et awk dans votre arsenal, vous pourrez automatiser une grande partie du traitement de données textuelles. C'est comme avoir un super-pouvoir pour manipuler des fichiers ! 🚀

**Un dernier conseil** : Commencez petit, testez toujours sur une copie, et documentez vos commandes complexes. Vous les remercierez dans 6 mois quand vous devrez les réutiliser ! 😊

⏭️ [Commandes réseau avancées (netstat, ss, ip)](/20-ligne-de-commande-avancee/06-commandes-reseau-avancees.md)
