🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Expressions régulières (regex)

## Introduction

Les **expressions régulières** (ou **regex**) sont comme un langage de recherche ultra-puissant. Imaginez pouvoir dire à votre ordinateur : "Trouve-moi tous les numéros de téléphone", "Trouve toutes les adresses email", ou "Trouve tous les mots qui commencent par 'super' et finissent par 'ment'".

C'est exactement ce que permettent les regex : définir des **motifs de recherche** complexes pour trouver, extraire, valider ou remplacer du texte.

### À quoi servent les regex ?

- **Recherche avancée** : Trouver des motifs complexes dans des fichiers
- **Validation** : Vérifier qu'une adresse email, un numéro de téléphone est au bon format
- **Extraction** : Extraire des informations spécifiques (dates, URLs, numéros)
- **Remplacement** : Remplacer du texte selon des motifs
- **Traitement de données** : Nettoyer et formater des données
- **Analyse de logs** : Filtrer et analyser des fichiers journaux

### Les regex sous Linux

Sous Linux, vous utiliserez les regex avec :
- **grep** : Rechercher dans des fichiers
- **sed** : Remplacer du texte
- **awk** : Traiter et analyser du texte
- **find** : Trouver des fichiers
- Et beaucoup d'autres outils...

## Les bases des expressions régulières

### Caractères littéraux

Le plus simple : chercher du texte exact.

```bash
# Chercher "chat" dans un fichier
grep "chat" fichier.txt
```

Cela trouve toutes les lignes contenant le mot "chat".

### Le point (.) - N'importe quel caractère

Le point `.` représente **n'importe quel caractère** (sauf le retour à la ligne).

```bash
# Chercher "c.t" : cat, cot, c9t, c@t, etc.
grep "c.t" fichier.txt
```

**Exemples de correspondances** :
- `cat` ✅
- `cot` ✅
- `c9t` ✅
- `c@t` ✅
- `ct` ❌ (il manque un caractère)
- `cart` ❌ (il y a deux caractères entre c et t)

### Les caractères spéciaux

Certains caractères ont une signification spéciale :

```
.   ^   $   *   +   ?   [   ]   {   }   (   )   |   \
```

Pour chercher ces caractères littéralement, il faut les **échapper** avec un backslash `\`.

```bash
# Chercher un point littéral
grep "\." fichier.txt

# Chercher un point d'interrogation littéral
grep "\?" fichier.txt
```

## Ancres : position dans la ligne

### Début de ligne (^)

Le symbole `^` indique le **début d'une ligne**.

```bash
# Lignes qui commencent par "Bonjour"
grep "^Bonjour" fichier.txt
```

**Exemples** :
- `Bonjour tout le monde` ✅
- `Bonjour` ✅
- `Dire Bonjour` ❌ (ne commence pas par Bonjour)

### Fin de ligne ($)

Le symbole `$` indique la **fin d'une ligne**.

```bash
# Lignes qui se terminent par "fin"
grep "fin$" fichier.txt
```

**Exemples** :
- `C'est la fin` ✅
- `fin` ✅
- `fin de fichier` ❌ (ne se termine pas par fin)

### Combinaison : ligne entière

```bash
# Lignes qui sont exactement "OK"
grep "^OK$" fichier.txt

# Lignes vides
grep "^$" fichier.txt
```

## Classes de caractères

### Classe simple [...]

Les crochets `[]` définissent un **ensemble de caractères possibles**.

```bash
# Chercher "c" suivi de a, e, i, o, ou u
grep "c[aeiou]" fichier.txt
```

**Correspondances** :
- `ca` ✅ (chat, car)
- `ce` ✅ (ceci)
- `ci` ✅ (cible)
- `co` ✅ (code)
- `cu` ✅ (cube)
- `cy` ❌

### Plages de caractères [a-z]

On peut définir des **plages** :

```bash
# N'importe quelle lettre minuscule
[a-z]

# N'importe quelle lettre majuscule
[A-Z]

# N'importe quel chiffre
[0-9]

# Combinaisons
[a-zA-Z]      # Lettres minuscules ou majuscules
[a-zA-Z0-9]   # Lettres ou chiffres
[0-9a-f]      # Chiffres hexadécimaux
```

**Exemples** :

```bash
# Trouver des mots commençant par une majuscule
grep "^[A-Z]" fichier.txt

# Trouver des lignes contenant des chiffres
grep "[0-9]" fichier.txt
```

### Négation [^...]

Le `^` **à l'intérieur des crochets** signifie "sauf" ou "pas".

```bash
# Tout sauf les voyelles
[^aeiou]

# Tout sauf les chiffres
[^0-9]

# Tout sauf les espaces
[^ ]
```

**Exemples** :

```bash
# Lignes ne commençant pas par #
grep "^[^#]" fichier.txt

# Chercher des caractères non alphanumériques
grep "[^a-zA-Z0-9]" fichier.txt
```

## Classes de caractères prédéfinies

Pour simplifier, il existe des classes prédéfinies :

### Avec grep -E (ou egrep)

```bash
\d    # Chiffre [0-9]
\D    # Pas un chiffre [^0-9]
\w    # Caractère de mot [a-zA-Z0-9_]
\W    # Pas un caractère de mot
\s    # Espace blanc (espace, tab, etc.)
\S    # Pas un espace blanc
```

**Note** : Ces classes nécessitent `grep -E` ou `egrep`.

**Exemples** :

```bash
# Trouver des lignes avec au moins un chiffre
grep -E "\d" fichier.txt

# Trouver des lignes avec uniquement des lettres et chiffres
grep -E "^\w+$" fichier.txt
```

### Classes POSIX

Plus portables, fonctionnent avec `grep` normal :

```bash
[[:digit:]]    # Chiffres
[[:alpha:]]    # Lettres
[[:alnum:]]    # Lettres et chiffres
[[:space:]]    # Espaces blancs
[[:upper:]]    # Majuscules
[[:lower:]]    # Minuscules
[[:punct:]]    # Ponctuation
```

**Exemples** :

```bash
# Lignes commençant par un chiffre
grep "^[[:digit:]]" fichier.txt

# Lignes contenant uniquement des lettres
grep "^[[:alpha:]]*$" fichier.txt
```

## Quantificateurs : répétition

### Astérisque (*) - zéro ou plusieurs fois

L'astérisque `*` signifie "le caractère précédent peut apparaître **0 fois ou plus**".

```bash
# "ca" suivi de zéro ou plusieurs "r"
car*
```

**Correspondances** :
- `ca` ✅ (0 fois)
- `car` ✅ (1 fois)
- `carr` ✅ (2 fois)
- `carrr` ✅ (3 fois)

**Exemples** :

```bash
# Lignes vides ou contenant uniquement des espaces
grep "^ *$" fichier.txt

# Mots se terminant par "s" optionnel
grep "chat*" fichier.txt  # chat ou chats
```

### Plus (+) - une fois ou plus

Le plus `+` signifie "le caractère précédent doit apparaître **au moins 1 fois**".

**Note** : Nécessite `grep -E` ou `egrep`.

```bash
# Au moins un chiffre
grep -E "[0-9]+" fichier.txt
```

**Correspondances** :
- `1` ✅
- `12` ✅
- `123` ✅
- `` ❌ (aucun chiffre)

### Point d'interrogation (?) - zéro ou une fois

Le `?` signifie "le caractère précédent est **optionnel** (0 ou 1 fois)".

**Note** : Nécessite `grep -E` ou `egrep`.

```bash
# "couleur" avec ou sans "u"
grep -E "colou?r" fichier.txt
```

**Correspondances** :
- `color` ✅
- `colour` ✅
- `colouur` ❌ (deux "u")

### Accolades {n,m} - répétition précise

Les accolades permettent de spécifier **exactement** combien de fois.

**Note** : Nécessite `grep -E` ou `egrep`.

```bash
{n}      # Exactement n fois
{n,}     # Au moins n fois
{n,m}    # Entre n et m fois
```

**Exemples** :

```bash
# Exactement 4 chiffres (ex: année)
grep -E "[0-9]{4}" fichier.txt

# Entre 2 et 4 lettres
grep -E "[a-z]{2,4}" fichier.txt

# Au moins 3 caractères
grep -E ".{3,}" fichier.txt
```

**Correspondances pour `[0-9]{2,4}` (2 à 4 chiffres)** :
- `12` ✅
- `123` ✅
- `1234` ✅
- `1` ❌ (un seul)
- `12345` ✅ (correspond aux 4 premiers)

## Groupes et alternatives

### Parenthèses () - groupes

Les parenthèses permettent de **grouper** des éléments.

**Note** : Nécessite `grep -E` ou `egrep`.

```bash
# Répéter un groupe
grep -E "(ha)+" fichier.txt
```

**Correspondances** :
- `ha` ✅
- `haha` ✅
- `hahaha` ✅

### Pipe (|) - alternatives

Le pipe `|` signifie "OU".

**Note** : Nécessite `grep -E` ou `egrep`.

```bash
# "chat" OU "chien"
grep -E "chat|chien" fichier.txt

# "Mr" OU "Mme" OU "Mlle"
grep -E "M(r|me|lle)" fichier.txt
```

**Exemples plus complexes** :

```bash
# Fichiers .jpg OU .png OU .gif
grep -E "\.(jpg|png|gif)$" liste_fichiers.txt

# Lignes commençant par "Erreur" ou "Avertissement"
grep -E "^(Erreur|Avertissement)" log.txt
```

## Exemples pratiques courants

### Validation d'adresse email (simple)

```bash
grep -E "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$" emails.txt
```

**Explication** :
- `[a-zA-Z0-9._%+-]+` : Un ou plusieurs caractères valides avant @
- `@` : Le symbole @
- `[a-zA-Z0-9.-]+` : Le nom de domaine
- `\.` : Un point (échappé)
- `[a-zA-Z]{2,}` : L'extension (au moins 2 lettres)

### Numéro de téléphone français

```bash
# Format : 06 12 34 56 78
grep -E "^0[1-9]( [0-9]{2}){4}$" telephones.txt

# Format : 06.12.34.56.78 ou 06-12-34-56-78
grep -E "^0[1-9]([.-][0-9]{2}){4}$" telephones.txt
```

### Date (format JJ/MM/AAAA)

```bash
grep -E "^[0-3][0-9]/[0-1][0-9]/[0-9]{4}$" dates.txt
```

**Correspondances** :
- `01/01/2024` ✅
- `31/12/2023` ✅
- `99/99/9999` ⚠️ (valide pour la regex, mais pas une vraie date)

### Adresse IP (simple)

```bash
grep -E "^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$" ips.txt
```

### URL

```bash
grep -E "^https?://[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" urls.txt
```

**Explication** :
- `https?` : http ou https (le 's' est optionnel)
- `://` : Séparateur
- `[a-zA-Z0-9.-]+` : Nom de domaine
- `\.` : Point
- `[a-zA-Z]{2,}` : Extension

### Code postal français

```bash
grep -E "^[0-9]{5}$" codes_postaux.txt
```

### Carte bancaire (format XXXX XXXX XXXX XXXX)

```bash
grep -E "^[0-9]{4} [0-9]{4} [0-9]{4} [0-9]{4}$" cartes.txt
```

## Utilisation avec grep

### Options utiles de grep

```bash
# Recherche insensible à la casse
grep -i "motif" fichier.txt

# Utiliser les regex étendues (recommandé)
grep -E "motif" fichier.txt
# Ou
egrep "motif" fichier.txt

# Inverser la recherche (lignes qui NE correspondent PAS)
grep -v "motif" fichier.txt

# Afficher le numéro de ligne
grep -n "motif" fichier.txt

# Afficher uniquement les fichiers correspondants
grep -l "motif" *.txt

# Compter les correspondances
grep -c "motif" fichier.txt

# Afficher N lignes de contexte
grep -C 3 "motif" fichier.txt  # 3 lignes avant et après  
grep -A 3 "motif" fichier.txt  # 3 lignes après  
grep -B 3 "motif" fichier.txt  # 3 lignes avant  

# Recherche récursive dans tous les fichiers
grep -r "motif" /chemin/dossier/
```

### Exemples pratiques avec grep

```bash
# Trouver toutes les lignes contenant une adresse email
grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" fichier.txt

# Trouver les lignes commençant par un chiffre
grep "^[0-9]" fichier.txt

# Trouver les lignes vides
grep "^$" fichier.txt

# Trouver les lignes qui ne sont pas des commentaires
grep -v "^#" config.conf

# Trouver les erreurs dans un log
grep -i "error\|warning\|critical" /var/log/syslog

# Trouver des adresses IP dans un fichier
grep -E "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" fichier.txt

# Trouver des URLs
grep -E "https?://[^ ]+" fichier.txt

# Lignes contenant exactement 5 mots
grep -E "^([^ ]+ ){4}[^ ]+$" fichier.txt
```

## Utilisation avec sed

Sed permet de **remplacer** du texte en utilisant des regex.

### Syntaxe de base

```bash
sed 's/motif/remplacement/' fichier.txt
```

- `s` : Substitution
- Premier `/` : Début du motif
- Deuxième `/` : Séparation motif/remplacement
- Troisième `/` : Fin

### Exemples avec sed

```bash
# Remplacer "chat" par "chien"
sed 's/chat/chien/' fichier.txt

# Remplacer toutes les occurrences sur chaque ligne (flag g)
sed 's/chat/chien/g' fichier.txt

# Insensible à la casse (flag i)
sed 's/chat/chien/gi' fichier.txt

# Modifier le fichier directement (flag -i)
sed -i 's/chat/chien/g' fichier.txt

# Sauvegarder une copie avant modification
sed -i.bak 's/chat/chien/g' fichier.txt
```

### Exemples avancés avec sed

```bash
# Supprimer les espaces en début de ligne
sed 's/^ *//' fichier.txt

# Supprimer les espaces en fin de ligne
sed 's/ *$//' fichier.txt

# Supprimer les lignes vides
sed '/^$/d' fichier.txt

# Supprimer les commentaires (lignes commençant par #)
sed '/^#/d' fichier.txt

# Remplacer plusieurs espaces par un seul
sed 's/  */ /g' fichier.txt

# Extraire uniquement les adresses email
sed -n 's/.*\([a-zA-Z0-9._%+-]\+@[a-zA-Z0-9.-]\+\.[a-zA-Z]\{2,\}\).*/\1/p' fichier.txt

# Mettre en majuscule la première lettre
sed 's/^./\U&/' fichier.txt

# Ajouter un préfixe à chaque ligne
sed 's/^/PRÉFIXE: /' fichier.txt

# Numéroter les lignes
sed = fichier.txt | sed 'N;s/\n/\t/'
```

### Groupes de capture avec sed

Les groupes `\(...\)` permettent de **capturer** du texte pour le réutiliser avec `\1`, `\2`, etc.

```bash
# Inverser deux mots séparés par un espace
echo "Dupont Jean" | sed 's/\(.*\) \(.*\)/\2 \1/'
# Résultat : Jean Dupont

# Extraire l'extension d'un fichier
echo "document.pdf" | sed 's/.*\.\(.*\)/\1/'
# Résultat : pdf

# Formater une date JJ/MM/AAAA en AAAA-MM-JJ
echo "25/12/2024" | sed 's|\([0-9]\{2\}\)/\([0-9]\{2\}\)/\([0-9]\{4\}\)|\3-\2-\1|'
# Résultat : 2024-12-25
```

## Utilisation avec awk

Awk est excellent pour traiter des données tabulaires avec des regex.

```bash
# Afficher les lignes contenant un motif
awk '/motif/' fichier.txt

# Afficher les lignes commençant par un chiffre
awk '/^[0-9]/' fichier.txt

# Afficher la 2e colonne des lignes contenant "error"
awk '/error/ {print $2}' log.txt

# Compter les lignes correspondant à un motif
awk '/motif/ {count++} END {print count}' fichier.txt
```

### Exemples pratiques avec awk

```bash
# Extraire les adresses IP d'un fichier
awk '/[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}/ {print $0}' fichier.txt

# Afficher les lignes avec au moins 5 caractères
awk 'length($0) >= 5' fichier.txt

# Remplacer dans une colonne spécifique
awk '{gsub(/ancien/, "nouveau", $2); print}' fichier.txt

# Filtrer les utilisateurs du fichier /etc/passwd
awk -F: '/bash$/ {print $1}' /etc/passwd
```

## Utilisation avec find

Find peut utiliser des regex pour filtrer les fichiers.

```bash
# Trouver les fichiers .txt ou .md
find . -regex ".*\.\(txt\|md\)$"

# Trouver les fichiers dont le nom contient des chiffres
find . -regex ".*[0-9].*"

# Trouver les fichiers image
find . -regex ".*\.\(jpg\|png\|gif\)$"
```

## Caractères spéciaux et échappement

### Dans grep normal

```bash
# Ces caractères doivent être échappés : . * [ ] ^ $ \
grep "\." fichier.txt       # Point littéral  
grep "\*" fichier.txt       # Astérisque littéral  
grep "\$" fichier.txt       # Dollar littéral  
grep "c\.txt" fichier.txt   # Chercher "c.txt"  
```

### Dans grep -E (regex étendues)

```bash
# Ces caractères doivent être échappés : . [ ] ^ $ \ + ? { } | ( )
grep -E "\." fichier.txt  
grep -E "\+" fichier.txt  
grep -E "\?" fichier.txt  
grep -E "\(" fichier.txt  
```

### Dans sed

```bash
# Mêmes règles que grep normal
# Le séparateur peut être changé pour éviter l'échappement
sed 's|/chemin/vers/fichier|/nouveau/chemin|' fichier.txt
# Au lieu de
sed 's/\/chemin\/vers\/fichier/\/nouveau\/chemin/' fichier.txt
```

## Tableaux récapitulatifs

### Métacaractères de base

| Symbole | Signification | Exemple | Correspondances |
|---------|---------------|---------|-----------------|
| `.` | N'importe quel caractère | `c.t` | cat, cot, c9t |
| `^` | Début de ligne | `^Bonjour` | Lignes commençant par Bonjour |
| `$` | Fin de ligne | `fin$` | Lignes se terminant par fin |
| `*` | 0 ou plusieurs fois | `ca*t` | ct, cat, caat |
| `+` | 1 ou plusieurs fois | `ca+t` | cat, caat (pas ct) |
| `?` | 0 ou 1 fois | `ca?t` | ct, cat (pas caat) |
| `[]` | Classe de caractères | `[aeiou]` | Une voyelle |
| `[^]` | Négation | `[^0-9]` | Pas un chiffre |
| `|` | Alternative (OU) | `chat|chien` | chat ou chien |
| `()` | Groupe | `(ha)+` | ha, haha, hahaha |

### Quantificateurs

| Quantificateur | Signification | Exemple | Correspondances |
|----------------|---------------|---------|-----------------|
| `*` | 0 ou plus | `ab*` | a, ab, abb, abbb |
| `+` | 1 ou plus | `ab+` | ab, abb, abbb (pas a) |
| `?` | 0 ou 1 | `ab?` | a, ab (pas abb) |
| `{n}` | Exactement n fois | `a{3}` | aaa |
| `{n,}` | Au moins n fois | `a{2,}` | aa, aaa, aaaa |
| `{n,m}` | Entre n et m fois | `a{2,4}` | aa, aaa, aaaa |

### Classes de caractères

| Classe | Signification | Équivalent |
|--------|---------------|------------|
| `[0-9]` | Chiffre | `\d` ou `[[:digit:]]` |
| `[a-z]` | Minuscule | `[[:lower:]]` |
| `[A-Z]` | Majuscule | `[[:upper:]]` |
| `[a-zA-Z]` | Lettre | `[[:alpha:]]` |
| `[a-zA-Z0-9]` | Alphanumérique | `\w` ou `[[:alnum:]]` |
| `[ \t]` | Espace ou tab | `[[:space:]]` |

## Exemples de regex complexes

### Validation de mot de passe

```bash
# Au moins 8 caractères, 1 majuscule, 1 minuscule, 1 chiffre
grep -E "^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9]).{8,}$"
```

**Note** : Les lookaheads `(?=...)` ne sont pas supportés par grep. Utilisez perl ou python pour ce type de validation.

### Extraction d'informations

```bash
# Extraire les URLs d'un fichier HTML
grep -oE 'https?://[^"]+' page.html

# Extraire les adresses email
grep -oE '[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}' document.txt

# Extraire les hashtags Twitter
grep -oE '#[a-zA-Z0-9_]+' tweets.txt

# Extraire les prix (format XX.XX€)
grep -oE '[0-9]+\.[0-9]{2}€' factures.txt
```

### Nettoyage de données

```bash
# Supprimer les doublons d'espaces
sed 's/  \+/ /g' fichier.txt

# Supprimer les espaces de début et fin
sed 's/^ *//; s/ *$//' fichier.txt

# Normaliser les fins de ligne (Windows → Unix)
sed 's/\r$//' fichier.txt

# Supprimer les lignes vides consécutives
sed '/^$/N;/^\n$/D' fichier.txt
```

### Formatage

```bash
# Ajouter des virgules tous les 3 chiffres (1234567 → 1,234,567)
echo "1234567" | sed ':a;s/\B[0-9]\{3\}\>/,&/;ta'

# Convertir des dates MM/JJ/AAAA en JJ/MM/AAAA
sed 's|\([0-9]\{2\}\)/\([0-9]\{2\}\)/\([0-9]\{4\}\)|\2/\1/\3|' dates.txt

# Masquer les numéros de carte bancaire (garder 4 derniers chiffres)
sed 's/\([0-9]\{4\}\) \([0-9]\{4\}\) \([0-9]\{4\}\) \([0-9]\{4\}\)/XXXX XXXX XXXX \4/' cartes.txt
```

## Outils pour tester et apprendre

### Sites web interactifs

1. **regex101.com** : [https://regex101.com/](https://regex101.com/)
   - Testeur interactif avec explications
   - Support de plusieurs langages
   - Partage de regex
   - Excellente explication en temps réel

2. **regexr.com** : [https://regexr.com/](https://regexr.com/)
   - Interface visuelle
   - Bibliothèque d'exemples
   - Référence complète

3. **regexpal.com** : [https://www.regexpal.com/](https://www.regexpal.com/)
   - Simple et rapide
   - Tests en temps réel

### Tester en ligne de commande

```bash
# Utiliser echo et grep pour tester
echo "test@example.com" | grep -E "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"

# Si la commande retourne quelque chose, c'est une correspondance
if echo "test@example.com" | grep -qE "regex"; then
    echo "Correspond !"
else
    echo "Ne correspond pas"
fi
```

### Script de test rapide

```bash
#!/bin/bash
# test-regex.sh
# Usage : ./test-regex.sh "regex" "texte à tester"

REGEX="$1"  
TEXTE="$2"  

if echo "$TEXTE" | grep -qE "$REGEX"; then
    echo "✅ CORRESPOND : '$TEXTE' correspond à '$REGEX'"
else
    echo "❌ NE CORRESPOND PAS : '$TEXTE' ne correspond pas à '$REGEX'"
fi
```

Utilisation :

```bash
chmod +x test-regex.sh
./test-regex.sh "^[0-9]+$" "123"     # ✅ CORRESPOND
./test-regex.sh "^[0-9]+$" "abc"     # ❌ NE CORRESPOND PAS
```

## Cas pratiques d'utilisation

### Analyse de logs

```bash
# Compter les erreurs par type
grep -E "ERROR|WARNING|CRITICAL" /var/log/syslog | \
    sed 's/.*\[\(ERROR\|WARNING\|CRITICAL\)\].*/\1/' | \
    sort | uniq -c

# Extraire les adresses IP qui ont échoué SSH
grep "Failed password" /var/log/auth.log | \
    grep -oE "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" | \
    sort | uniq -c | sort -rn

# Trouver les 10 URLs les plus consultées dans un log Apache
awk '{print $7}' /var/log/apache2/access.log | \
    sort | uniq -c | sort -rn | head -10
```

### Traitement de fichiers CSV

```bash
# Extraire les emails d'un CSV
awk -F',' '{print $3}' contacts.csv | grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}"

# Filtrer les lignes où la 3e colonne contient un nombre > 100
awk -F',' '$3 > 100' données.csv

# Remplacer les virgules par des points-virgules
sed 's/,/;/g' fichier.csv
```

### Nettoyage de code source

```bash
# Supprimer les commentaires C++ (// ...)
sed 's|//.*||' code.cpp

# Supprimer les lignes vides
sed '/^$/d' code.cpp

# Supprimer les espaces en fin de ligne
sed 's/[[:space:]]*$//' code.cpp
```

### Extraction de données

```bash
# Extraire tous les numéros de téléphone d'un fichier
grep -oE "0[1-9]([. -]?[0-9]{2}){4}" fichier.txt

# Extraire les dates au format JJ/MM/AAAA
grep -oE "[0-3][0-9]/[0-1][0-9]/[0-9]{4}" fichier.txt

# Extraire les prix
grep -oE "[0-9]+[,.]?[0-9]*[€$]" factures.txt
```

## Différences entre les moteurs de regex

### POSIX Basic (grep par défaut)

- Moins de fonctionnalités
- Nécessite d'échapper `+`, `?`, `{`, `}`, `|`, `(`, `)`
- Plus portable

```bash
grep "motif\+" fichier.txt  # Le + doit être échappé
```

### POSIX Extended (grep -E / egrep)

- Plus de fonctionnalités
- `+`, `?`, `{`, `}`, `|`, `()` fonctionnent sans échappement
- Recommandé pour la plupart des usages

```bash
grep -E "motif+" fichier.txt  # Pas besoin d'échapper
```

### Perl (grep -P)

- Le plus puissant
- Supporte les lookaheads, lookbehinds, etc.
- Pas toujours disponible

```bash
grep -P "(?<=@)[a-z]+" emails.txt  # Lookbehind (après @)
```

## Conseils et bonnes pratiques

### 1. Commencez simple

Ne créez pas une regex complexe d'un coup. Construisez progressivement :

```bash
# Étape 1 : Trouver des chiffres
[0-9]

# Étape 2 : Au moins 2 chiffres
[0-9]{2,}

# Étape 3 : Exactement entre 2 et 4 chiffres
[0-9]{2,4}

# Étape 4 : Au début de ligne
^[0-9]{2,4}
```

### 2. Testez vos regex

Utilisez regex101.com ou créez un petit fichier de test :

```bash
# test.txt
email@example.com  
not-an-email  
test@domain.co.uk  
invalid@@example.com  

# Testez
grep -E "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$" test.txt
```

### 3. Commentez les regex complexes

```bash
# Regex pour valider une adresse email
# Format : utilisateur@domaine.extension
# - utilisateur : lettres, chiffres, points, tirets, underscores
# - domaine : lettres, chiffres, points, tirets
# - extension : au moins 2 lettres
EMAIL_REGEX="^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"
```

### 4. Soyez aussi spécifique que possible

```bash
# ❌ Trop permissif
.*

# ✅ Plus précis
[a-zA-Z0-9]+
```

### 5. Attention à la gourmandise (greedy)

Par défaut, `*` et `+` sont gourmands (ils prennent le maximum possible).

```bash
# Texte : <div>contenu</div>
# Regex : <.*>
# Résultat : <div>contenu</div> (tout !)

# Solution : Utiliser le quantificateur non-gourmand (avec ?)
# Regex : <.*?>
# Résultat : <div> (puis </div> séparément)
```

### 6. Utilisez les ancres quand nécessaire

```bash
# ❌ Peut matcher n'importe où dans la ligne
grep "123" fichier.txt

# ✅ Uniquement les lignes qui sont exactement "123"
grep "^123$" fichier.txt
```

### 7. Échappez les caractères spéciaux

```bash
# Pour chercher un point littéral
grep "\." fichier.txt

# Pour chercher une parenthèse littérale
grep "(" fichier.txt  # ❌ Erreur  
grep "\(" fichier.txt  # ✅ Correct  
```

## Pièges courants et solutions

### Piège 1 : Oublier d'échapper les points

```bash
# ❌ Mauvais : . signifie "n'importe quel caractère"
grep "fichier.txt" liste.txt  # Correspondra aussi à "fichierAtxt"

# ✅ Bon
grep "fichier\.txt" liste.txt
```

### Piège 2 : Confusion entre grep et grep -E

```bash
# ❌ Avec grep normal, + doit être échappé
grep "a+" fichier.txt  # Cherche littéralement "a+"

# ✅ Correct
grep "a\+" fichier.txt  # Ou mieux :  
grep -E "a+" fichier.txt  
```

### Piège 3 : Regex trop gourmande

```bash
# Texte : "citation" et "autre citation"
# Regex : ".*"
# Résultat : "citation" et "autre citation" (tout entre les premiers et derniers guillemets)

# Solution : Utiliser la négation
# Regex : "[^"]*"
# Résultat : "citation" (puis "autre citation" séparément)
```

### Piège 4 : Oublier les ancres

```bash
# Valider un code postal de 5 chiffres
# ❌ Mauvais
grep "[0-9]{5}" fichier.txt  # Correspondra aussi à "123456"

# ✅ Bon
grep "^[0-9]{5}$" fichier.txt  # Uniquement 5 chiffres, rien d'autre
```

## Aller plus loin

### Ressources d'apprentissage

1. **Documentation**
   - `man grep`
   - `man sed`
   - `info grep`

2. **Livres**
   - "Mastering Regular Expressions" de Jeffrey Friedl (référence absolue)
   - "Regular Expressions Cookbook"

3. **Tutoriels en ligne**
   - regex101.com (avec explications interactives)
   - regexone.com (cours progressif)

4. **Pratique**
   - Codecademy (exercices interactifs)
   - HackerRank (défis de programmation)

### Commandes pour s'entraîner

```bash
# Créer un fichier de test avec différents formats
cat > test_regex.txt << EOF  
Jean Dupont - jean.dupont@example.com - 06 12 34 56 78  
Marie Martin - marie@test.fr - 01.23.45.67.89  
Pierre Durant - pierre_durant@email.com - 0623456789  
Invalid Email - notanemail - 12345  
Site web : https://www.example.com  
Date : 25/12/2024  
Prix : 29.99€  
Code postal : 75001  
IP : 192.168.1.1  
EOF  

# Extraire les emails
grep -oE "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" test_regex.txt

# Extraire les téléphones
grep -oE "0[1-9]([. ]?[0-9]{2}){4}" test_regex.txt

# Extraire les URLs
grep -oE "https?://[^ ]+" test_regex.txt

# Extraire les prix
grep -oE "[0-9]+\.[0-9]{2}€" test_regex.txt
```

## Conclusion

Les expressions régulières sont un outil extrêmement puissant pour manipuler du texte sous Linux. Bien qu'elles puissent sembler complexes au début, avec de la pratique, elles deviennent indispensables.

**Points clés à retenir** :

- ✅ Commencez simple et construisez progressivement
- ✅ Testez toujours vos regex sur des exemples
- ✅ Utilisez `grep -E` pour les regex modernes
- ✅ Les ancres `^` et `$` sont vos amies pour la validation
- ✅ Pratiquez régulièrement avec des exemples réels
- ✅ Utilisez regex101.com pour comprendre et déboguer

**Les regex sont comme un super-pouvoir pour le traitement de texte** - une fois maîtrisées, vous vous demanderez comment vous avez pu vous en passer ! 🚀

**Progression recommandée** :
1. Maîtrisez les caractères littéraux et le point
2. Apprenez les ancres (^ et $)
3. Pratiquez les classes de caractères []
4. Comprenez les quantificateurs (*, +, ?)
5. Utilisez les groupes et alternatives
6. Créez des regex complexes pour des cas réels

Bonne pratique ! 🎯

⏭️ [Sed et Awk pour traitement de texte](/20-ligne-de-commande-avancee/05-sed-et-awk-pour-traitement-de-texte.md)
