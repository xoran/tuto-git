# Formation Git
## Alain Kelleter
alain@ktdev.pro - https://www.ktdev.pro

 
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

 `git add <nomdufichier>`

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

### 7. Supprimer ou deplacer des fichiers
#### 7.1 Suppression 

Pour supprimer des fichiers de Git, il faut les supprimer de la zone d'Index et ensuite valider (commit).

Si l'on efface le fichiers sans le faire avec Git (ex.: rm <fichier> (ligne de commande GNU/Linux). Il apparaîtra sous la section des modifications qui ne seront pas validées (c.à.d. non indéxées).

Il faut utiliser la commande suivante:

`git rm <fichier>` : avec cette commande la suppression du fichier est indexée !

#### 7.2 Déplacement

Git ne suit pas de façon explicite les mouvements de fichiers et ce même si il est capable de voir q'un fichier a été déplacé.

Pour déplacer un fichier il faut utiliser la commande suivante :

`git mv <source/fichier> <destination/fichier>` : cela revient à le supprimer de la source et à le recréer à la destination. 

### 8 Les Historiques

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

` git log --pretty=format:'%h - %an - %ar : %s'`

`52f2e30 - Kentaro Tatsu - il y a 15 heures : Update Formation Git.md - Chapter 7(full) and 8(begin)`
`21e3ba2 - Kentaro Tatsu - il y a 3 jours : Update Formation Git.md`
`3cbf321 - Kentaro Tatsu - il y a 3 jours : Commit 5 first chapters`
`0f1eae8 - Kentaro Tatsu - il y a 3 jours : Add Formation Git file`
`95b854f - Kentaro - il y a 3 jours : Initial commit `

### 9 Annuler des actions

* Modifier un commit
* Désindexer déjà indexé
* Réinitialiser un fichier modifié

*** !!! Attention certaines modification sont permanentes !!! ***

Il peut arriver que l'on valide(commit) une modification trop tôt en oubliant des fichiers.

Commande pour modifier un commit :

'git commit --amend`

Cette commande reprend l'index du commit précédent.
L'éditeur s'ouvre avec les modifications et le message.
Il est possible d'uniquement modifier le message du commit.
















