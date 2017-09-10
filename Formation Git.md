# Formation Git
## Tuto.com / Edouard Ferrari

### 1. Installation
Voir Cours (simple à réliser quelque soit la plateforme)

### 2. Configuration
Sur 3 niveaux :

* Configuration globale au système : (linux) /etc/gitconfig (git config --system)
* Configuration globale à l'utilisateur : (linux) ~/.gitconfig (git config --global)
* Configuration globale au projet : .gitconfig (git config)

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
* Initialiser un dépôt:
 
 `git init`

* Ajouter un fichier à l'index: 

 `git add <nomdufichier>`

* Ajouter tous les nouveaux fichiers ou tous les fichiers modifiés depuis leur dernière indexation
  
 `git add .`

* Récupérer un projet existant:

 `git clone`

Via protocol http/https : 
Ex.:
 
 * `git clone http://sources.xoransorvor.be:3000/KTDev/KT-FILMS.git`
 
Ou via le protocol ssh : 
Ex.:
 
 * `git clone gogs@sources.xoransorvor.be:KTDev/KT-FILMS.git`
 * `git clone git@github.com:xoran/KT-Shin.git`

 
