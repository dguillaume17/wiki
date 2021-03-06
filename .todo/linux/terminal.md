# Linux | Commandes

netstat -anop

## Symboles

### `.`

Répertoire en cours

Exemple :

* Mettre à jour les droits du répertoire en cours

```bash
chmod 777 .
```

### `~`

Répertoire de l'utilisateur en cours

Exemple :

```bash
cd ~
pwd #imprime /home/xxx
```

### `*` & `*/`

Tableau contenant respectivement la liste des fichiers / répertoires et la liste des répertoires

Exemples :

* Lister tous les fichiers et répertoires d'un dossier

```bash
echo *
#ou
ls -d *
#ou
for i in *; do echo $i; done
#ou
ls
#ou
find . -maxdepth 1
```

* Lister tous les répertoires d'un dossier

```bash
echo */
#ou
ls -d */
#ou
for i in */; do echo $i; done
#ou
find . -type d -maxdepth 1
```

### `$?`

Statut de la dernière commande

Exemple:

```bash
mkdir test
echo $? #imprime 0
mkdir test
echo $? #imprime 1
```

### `$0`

Nom de fichier du script en cours d'exécution

### `$1`, `$2`, ..., `$n`

Valeur de l'argument `n` passé en paramètre au script en cours d'exécution

### `$@`

Valeurs (séparés par un espace) de tous les arguments passés en paramètre au script en cours d'exécution

### `|`

Tuyau qui relie la sortie standard d'une première commande (=son résultat) à l'entrée standard d'une deuxième commande

Exemple :

```bash
cat test.txt | grep "hello"
```

### `>`

Chevron qui écrit la sortie standard d'une commande (=son résultat) dans un nouveau fichier texte (fichier écrasé si existant)

Exemple :

```bash
echo hello > test2.txt
```

### `>>`

Double chevron qui écrit la sortie standard d'une commande (=son résultat) à la fin d'un fichier texte existant (fichier créé si inexistant)

Exemple :

```bash
echo hello >> test2.txt
```

### `<`

Chevron qui écrit le contenu d'un fichier texte dans l'entrée standard d'une commande

Exemple :

```bash
cat < test.txt # pareil que cat test.txt
```

### `<<`

Double chevron qui écrit le contenu tapé par l'utilisateur dans l'entrée standard d'une commande

Syntaxe :

* `commande << <line>` = l'utilisateur tape le contenu dans la console jusqu'à l'écriture de la ligne `<line>`

Exemples :

* Ecrire le contenu tapé par l'utilisateur dans le fichier test.txt

    ```bash
    cat << EOF > test.txt
    ```

* Ecrire le contenu tapé par l'utilisateur dans le fichier test.txt
  * Création du script

    ```bash
    cat << EOF > config.ini
    [section]
    param1=$1
    param2=$2
    EOF
    echo "Config file was created successfully"
    ```

  * Exécution du script

    ```bash
    ./script.sh valeur1 valeur2
    ```

### `||`

Lien entre deux commandes qui exécute la deuxième uniquement si la première retourne une erreur

NB : la valeur de `$?` sera d'office `O` car pas d'erreur

Exemple :

```bash
mkdir test || echo "Ce dossier existe déjà"
```

### `&&`

Lien entre deux commandes qui exécute la deuxième uniquement si la première a réussi

Exemple :

```bash
mkdir test && echo "Le dossier a bien été créé"

```

### `;`

Lien entre deux commandes qui exécute la deuxième dans tous les cas

Exemple :

```bash
echo "Bonjour"; echo "Gui"
```

### `&`

Caractère en fin de commande permettant son exécution en arrière plan

Fonctionnement :

* Exécuter la commande avec `&` à la fin
* Le PID du processus est écrit dans la sortie standard
* Quand le processus est terminé et à la prochaine commande exécutée par l'utilisateur, le statut `Done` est écrit dans la sortie standard

Exemple :

```bash
sleep 10 &
```

### `$(...)`

Permet de récupérer la sortie standard d'une commande dans une variable

Exemple :

```bash
test=$(echo coucou)
echo $test
```

### `eval`

Permet d'exécuter une commande qui se trouve sous forme d'une chaine

Je préfère utiliser `eval` à la place de `$(...)` car `mysqldump` m'a déjà posé problème avec `$(...)`

Exemple :

```bash
test="echo \"coucou\""
eval $test
```

### `$((...))`

Permet de réaliser des opérations arithmétiques à partir d'une chaîne.

Contrairement à la commande `bc`, `$((...))` ne permet pas de calculer des fonctions mathématiques

Exemple :

```bash
echo $(("(1+2)*3"))
echo "(1+2)*3" | bc -l
```

## Raccourcis

### `CTRL + R`

Rechercher une commande dans l'historique des commandes

Fonctionnement :

* `CTRL + R` pour ouvrir la recherche
* Ecrire une recherche pour sélectionnr la dernière commande qui correspond à cette recherche
  * `enter` pour exécuter la commande sélectionnée
  * `up` | `down` pour naviguer dans l'historique de commande à partir de la commande sélectionnée
  * `CTRL + R` pour sélectionnr la dernière commande qui correspond à la recherche en partant de la commande sélectionnée

### `CTRL + A` & `CTRL + A`

Se positionner au début et à la fin d'une commande

### `ECHAP .`

Ecrire la valeur du dernier argument de la dernière commande exécutée

### `ECHAP #`

Commenter la commande en cours

Fonctionnement :

* `ECHAP #` pour ajouter `#` au début de la commande en cours et ouvrir une nouvelle commande
* Il est possible de revenir à la commande commentée grâce à l'historique des commandes

## Configuration

A chaque ouverture du shell, un script `bashrc` publique est d'abord exécuté et ensuite un script `bashrc` privé est exécuté.

Ces deux fichiers peuvent exécuter d'autres scripts `bashrc`

Le script `bashrc` publique est situé :

* soit dans `/etc/bashrc` (Redhat, Fedora)
* soit dans `/etc/bash.bashrc` (Debian, Ubuntu, Linux Mint)
* soit dans `/etc/bash.bashrc.local` (Suse, OpenSuse)

Le script `bashrc` privé est situé dans `~/.bashrc`
