# Formation Git
## Alain Kelleter
alain@ktdev.pro - https://www.ktdev.pro

Sources du cours :

* [tuto-git/github](https://github.com/xoran/tuto-git) (le cours)
* [tuto-git-test/github](https://github.com/xoran/tuto-git-test) (dépôt fictif pour tester les commandes / tests)

---
 
### 1. Installation
Simple à réaliser quelque soit la plateforme sur laquelle on travaille (GNU/Linux / Windows / MacOS)

### 2. Configuration
La configuration de Git peut s'étendre sur 3 niveaux.

Sur 3 niveaux :

* Configuration globale au système : (linux) /etc/gitconfig (`git config --system`)
* Configuration globale à l'utilisateur : (linux) ~/.gitconfig (`git config --global`)
* Configuration globale au projet : .gitconfig (`git config`)

Chaque niveau de configuration surcharge les paramètres du niveau précédent

#### 2.1 Premiers paramètres à configurer
* Nom / prénom et adresse e-mail
Ex.:

`git config --global user.name "Alain Kelleter"`

`git config --global user.email "alain@ktdev.pro"`

Vu que nous travaillons sur le niveau de l'utilisateur cela sera valable pour tous les projets sauf si l'on surcharge la configuration au niveau du projet.

* L'éditeur par défaut
Ex.:

`git config--global core.editor emacs / vim / nano / ...`

ON PEUT VERIFIER LA CONFIGURATION AVEC LA COMMANDE :

`git config --list`

### 3. Mise en place d'un premier dépôt

#### 3.1 Créer un dépôt Git
* Initialiser un nouveau dépôt:
 
 `git init`

* Récupérer un dépôt existant:

 `git clone`

Via protocol http/https : 
Ex.:
 
 * `git clone http://sources.xoransorvor.be:3000/KTDev/KT-FILMS.git`
 
Ou via le protocol ssh : 
Ex.:
 
 * `git clone gogs@sources.xoransorvor.be:KTDev/KT-FILMS.git`
 * `git clone git@github.com:xoran/KT-Shin.git`

### 4. Enregistrer des modifications dans le dépôt

* Connaître l'état des fichiers du projet

 `git status`

 `git status -s` (sommaire)

* Ajouter un fichier à l'index (staged): 

 `git add [nomdufichier]`

* Ajouter tous les nouveaux fichiers ou tous les fichiers modifiés depuis leur dernière indexation
  
 `git add .` / `git add *`
 
**REMARQUE**:  On peut gérer plus efficacement et globalement les fichiers qui ne doivent pas être suivi par git dans le projet. En créant et  configurant un fichier '.gitignore' (voir le .gitignore qui accompagne ce cours avec de plus amples exemples sur : https://github.com/github/gitignore)

### 5. Inspecter les modifications des fichiers indexés ou non

Commande : `git diff`

**git diff affiche les modifications ligne par ligne**

Cette commande répond aux questions:

* Quel fichier a été modifié et pas encore indexé
* Quelle modification a été indexée et est prête pour être validée  

Pour visualiser les modifications qui feront partie de la prochaine validation on utilise la commande :

`git diff --cached`

### 6. Valider les modifications

Commande : `git commit`

Une fois que l'index(staged) est dans un état qui convient au développeur, on peut valider les modifications.

Option :

* `-v` : ajoute le diff dans le commentaire
* `-m 'mon commentaire'` : ajoute directement le commentaire sans passer par l'éditeur de texte.
* `-a` : demande à Git de placer tous les fichiers déjà suivi dans la zone d'Index.

Une fois l'opération de commit terminée ce dernier possèdera un identifiant (ID) au format SHA-1 (une version raccourcie est affichée).

### 7. Supprimer ou déplacer des fichiers
#### 7.1 Suppression 

Pour supprimer des fichiers de Git, il faut les supprimer de la zone d'Index et ensuite valider (commit).

Si l'on efface le fichiers sans le faire avec Git (ex.: rm <fichier> (ligne de commande GNU/Linux). Il apparaîtra sous la section des modifications qui ne seront pas validées (c.à.d. non indéxées).

Il faut utiliser la commande suivante:

`git rm [fichier]` : avec cette commande la suppression du fichier est indexée !

#### 7.2 Déplacement

Git ne suit pas de façon explicite les mouvements de fichiers et ce même si il est capable de voir q'un fichier a été déplacé.

Pour déplacer un fichier il faut utiliser la commande suivante :

`git mv [source/fichier] [destination/fichier]` : cela revient à le supprimer de la source et à le recréer à la destination. 

### 8. Les Historiques

Pour consulter les historiques on utilise la commande:

`git log`

La commande `git log` possède une longue série d'options. Ces dernières permettent de paramètrer `git log` de façon à afficher avec précision sa sortie.

* `-<chiffre>` :  Affiche les n derniers commit 
* `-p` : Affiche le patch appliqué par chaque commit
* `--stat` : Affiche les statistiques de chaque fichier pour chaque commit
* `--shortstat` : N'affiche que les lignes modifiées/insérées/effacées de l'option --stat
* `--name-only` : Affiche la liste des fichiers modifiés après les informations du commit
* `--name-status` : Affiche la liste des fichiers affectés accompagnés des informations d'ajout/modification/suppression
* `--abbrev-commit` : N'affiche que les premiers caractères de la somme de contrôle SHA-1
* `--relative-date` : Affiche la date au format relatif (ex.: "2 weeks ago") au lieu du format complet
* `--graph` : Affiche en caractères ASCII le graphe de branches et fusion en vis-à-vis de l'historique
* `--pretty` : Affiche les commit dans un format alternatif. Les formats incluent oneline, short, full, fuller et format(avec lequel on peut spécifier sont propre format)
* `--oneline` : Option de convenance correspondant à : --pretty=oneline --abbrev-commit

Présentation du : `git log --pretty`

Le paramètre --pretty permet d'obtenir des sorties "custom".

Exemples : 
* `git log --pretty=oneline` : Affiche un commit par ligne
* `git log --pretty=format:'...'`

Options de format :
* `%H` : Somme de contrôle du commit
* `%h` : Somme de contrôle abrégée du commit 
* `%T` : Somme de contrôle de l'arborescence
* `%t` : Somme de contrôle abrégée de l'arborescence
* `%P` : Somme de contrôle des parents
* `%p` : Somme de contrôle abrégée des parents
* `%an` : Nom de l'auteur
* `%ae` : E-mail l'auteur
* `%ad` : Date de l'auteur (au format de l'option -date=)
* `%ar` : Date relative de l'auteur
* `%cn` : Nom du validateur
* `%ce` : E-mail du validateur
* `%cd` : Date du validateur
* `%cr` : Date relative du validateur
* `%s` : Sujet

Exemple de git log formaté :

`git log --pretty=format:'%h - %an - %ar : %s'`

`52f2e30 - Kentaro Tatsu - il y a 15 heures : Update Formation Git.md - Chapter 7(full) and 8(begin)`
`21e3ba2 - Kentaro Tatsu - il y a 3 jours : Update Formation Git.md`
`3cbf321 - Kentaro Tatsu - il y a 3 jours : Commit 5 first chapters`
`0f1eae8 - Kentaro Tatsu - il y a 3 jours : Add Formation Git file`
`95b854f - Kentaro - il y a 3 jours : Initial commit `

Souvent utilisé :

`git log -1 -p` : Affiche les modifications du dernier commit 

### 9. Annuler des actions

* Modifier un commit
* Désindexer déjà indexé
* Réinitialiser un fichier modifié

*** !!! Attention certaines modification sont permanentes !!! ***

#### 9.1 Modifier un commit
Il peut arriver que l'on valide(commit) une modification trop tôt en oubliant des fichiers.

Commande pour modifier un commit :

'git commit --amend`

Cette commande reprend l'index du commit précédent.
L'éditeur s'ouvre avec les modifications et le message.
Il est possible d'uniquement modifier le message du commit.

#### 9.2 Désindexer un fichier déjà indexé

Pour désindexer un fichier (avant de lancer le commit), on utilise la commande suivante:

`git reset HEAD [file]`

#### 9.3 Réinitialiser un fichier modifié

Pour replacer un fichier dans son état  au niveau du précédent checkout : 

`git checkout -- [fichier]`

Suite à cette commande, le fichier sera remis dans l'état dans lequel il était lors du dernier commit et toute modification qui aurait été réalisée entre-temps sera ***IRREMEDIABLEMENT PERDUE !***


### 10. Travailler avec des dépôts distants

Pour collaborer sur vos projets Git et pour externaliser ces derniers, nous allons travailler avec des dépôts distants.
Les dépôts distants hébergent vos projets sur internet ou le réseau de votre entreprise.
Des droits peuvent être assignés aux dépôts distants (lecture/écriture, lecture seule).

Un projet peut avoir plusieurs dépôt distants.

#### 10.1 Ajouter un dépôt distant 
Commande: 

`git remote add [nom] [adresse du dépôt distant]`

Ex.:
`git remote add origin https://github.com/xoran/tuto-git-test.git`

#### 10.2 Récupérer un dépôt distant 
Commande:

`git fetch [nom du depot distant]`

Ex.:
`git fetch origin` 

Cette commande récupère toutes les données que l'on ne possède pas encore du projet.
Dans le cas où l'on clone un dépôt distant, le dépôt distant est automatiquement ajouté sous le nom "origin".
le Si dépôt est différent que celui ajouté par défaut, les branches seront ajoutées dans "nom du dépôt distant/master"

#### 10.3 Pousser son travail sur un dépôt distant 
Commande:

`git push [depot distant] [nom de la branche]`

Ex.:
`git push origin master`

#### 10.4 Inspecter un dépôt distant 
Pour avoir plus d'informations sur un dépôt distant.

Commande:
`git remote show [dépot distant]`

Ex.:
`git remote show origin`

#### 10.4 Retirer et renommer des dépôts distants

Renommer une référence à un dépot :

Commande:
`git remote rename [ancienne référence] [nouvelle référence]`

Ex.:
 `git remote rename origin github`
 
 
Supprimer une référence à un dépot :

Commande:
`git remote rm [nom de la référence]`
 
 Ex.:
 `git remote rm github`

Plus d'infos sur le travail avec les dépôts distants : [ICI](https://git-scm.com/book/fr/v1/Les-bases-de-Git-Travailler-avec-des-d%C3%A9p%C3%B4ts-distants) 

### 11. Les Etiquettes (tags)

Git donne la possibilité d'étiqueter un certain état dans l'historique comme important.
Généralement on utilise les étiquettes pour marquer les différentes versions d'un projet.

#### 11.1 Lister les étiquettes

Commande:
`git tag`

Retourne la liste des étiquettes par ordre alphabétique.

Pour effectuer une recherche:
`git tag -l '[chaîne de caractère]*'`

Le caractère wildcard '*' est autorisé.

#### 11.2 Créer des étiquettes

Git utilise deux types d'étiquettes:

* a. Les étiquettes légères
* b. Les étiquette annotées

##### a. Les étiquettes légère
Une étiquette légère ressemble beaucoup à une branche qui ne change pas, c'est juste un pointeur sur un commit spécifique.
Elles se réduisent à stocker la somme de contrôle d'un commit dans un fichier, aucune autre information n'est conservée.
Pour créer une étiquette légère, on utilise `git tag` sans option :
Ex.:
`git tag v1.4-lw`

##### b. Les étiquettes annotées
Les étiquettes annotées, par contre sont stockées en tant qu'objets à part entière dans la base de données de Git.
Elles ont une somme de contrôle, contiennent le nom et l'adresse e-mail du créateur, la date, un message d'étiquetage et peuvent être signées et vérifiées avec GNU Privacy Guard (GPG).
Créer des étiquettes annotées est simple avec Git. Le plus simple est de spécifier l'option -a à la commande tag :
Ex.:
`git tag -a v1.2.m -m 'Annotation'`

***Remarque*** : On peut étiqueter les anciens commits et donc faire de l'étiquetage 'après coup'

#### 11.3 Partager les étiquettes

Par défaut, la commande git push ne transfère pas les étiquettes vers les serveurs distants. 
Il faut explicitement pousser les étiquettes après les avoir créées localement. 
Ce processus s'apparente à pousser des branches distantes — vous pouvez lancer git push origin [nom-du-tag].

`git push origin v1.5`

Si vous avez de nombreuses étiquettes que vous souhaitez pousser en une fois, vous pouvez aussi utiliser l'option `--tags` avec la commande git push.

#### 11.4 Extraire une étiquette

Au prélable il faut récupérer toutes les données du dépôt distant avec `git pull` ou `git fetch`
Pour se placer à la position d'un commit étiqueté on lance la commande suivante :
Ex.:
`git checkout -b v1.1.0`

Cette commande va créer une nouvelle branche et nous placer dedans.
Grâce à ce mécanisme nous pouvons naviguer à travers les différentes versions de notre projet.


Plus d'infos sur les étiquettes : [ICI](https://git-scm.com/book/fr/v1/Les-bases-de-Git-%C3%89tiquetage) 

### 12 Les Branches


