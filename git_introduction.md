# Git version control

## Introduction

[Git](http://git-scm.com/) est un système de version control qui enregistre les changements réalisés dans le cadre de vos projets. Bien que principalement destiné aux fichiers textes, git permet de versionner n'importe quel type de fichier informatique.

Créé en 2005 par Linus Torvalds ce système simple d'utilisation permet de facilement enregistrer les changements effectués sur des fichiers au sein d'un projet, de revenir en arrière si besoin est et même de gérer en paralèlle plusieurs versions de votre projet.

Un élément du succès de Git comme système de version control, c'est son caractère décentralisé. Là où d'autre systèmes dépendent d'un serveur central, git permet d'ajouter facilement cette capacité de version control à n'importe quel dossier présent localement sur votre ordinateur. Même si vous travaillez à l'aide d'un repository distant, la totalité de l'historique de votre projet est disponible localement.

En résumé:

- Git vous permet de facilement suivre et enregistrer les changements apportés à vos fichiers et de facilement revenir en arrière si besoin est
- Git (et Github) facilitent grandement la collaboration et le travail en équipe sur des projets de natures très diverses
- Git vous permet de créer des branches distinctes au sein de vos projets, de gérer celles-ci en parallèle ou des les combiner en une seule version.

En outre de très nombreux [tutoriaux](http://git-scm.com/videos), services et [logiciels disposant d'une interface graphique](http://git-scm.com/downloads/guis) se sont dévelopés autour de Git, faisant de ce dernier un standard de l'industrie.

## Installation

Git est très facile à installer. Des programmes d'installation sont [disponibles pour toutes les plateformes](http://git-scm.com/downloads).

## Configuration

### Auteur et email

Avant toute chose nous allons configurer git avec votre nom d'utilisateur et votre email

- `git config --global user.name "Your Name"` pour configurer votre nom d'utilisateur
- `git config --global user.email "name@domain.com"` pour configurer votre email

### Syntaxe coloring

- `git config --global color.ui true` pour avoir des jolies couleurs dans votre éditeur
- `git config --global core.editor "nano"` pour utiliser nano à la place de Vi comme éditeur (Vi est assez déroutant pour commencer)

## Notions de base

Quelques notions de base à bien comprendre avant de commencer à utiliser Git.

### Repository

Lorsque vous initialisez Git pour l'un de vos dossiers à l'aide de la commande `git init`, vous créez ce que l'on appelle un repository. En fait, Git ajoute un dossier système invisible ".git" au contenu de votre dossier. C'est dans ce dossier invisible que git enregistre tous les changements que vous réalisez dans votre projet. Supprimez ce dossier ".git" et votre repository redevient un dossier ordinaire.

Git ne prend en compte que les changements au niveau des fichiers. Un directory vide n'existe pas pour Git.

### Branch

Tout repository possède au moins une branche appellée "master". C'est cette branche qui va vous permettre d'enregistrer vos changements. Sans branche, pas de version control.

Comme nous le verrons dans la suite, il est possible d'avoir de multiples branches au sein d'un projet, ce qui vous permet de travailler sur l'une au l'autre feature sans travailler sur la branche principale du projet et ainsi d'avancer en parallèle ou de faire des essais sans prendre de risques inutiles. Les branches supplémentaires peuvent être nommées comme vous le souhaitez.

### Commits

Les commits sont les soumissions que vous faites dans votre repository Git. Ils sont composés du détail des changements apportés aux fichiers qui composent votre projet (modifications, ajouts ou suppressions) et du message qui accompagne et décrit ces modifications. Ces commit messages sont rédigés par vos soins et doivent idéalement décrire les changements apportés.

Il est important de réaliser ces commits regulièrement, afin de pouvoir facilement revenir en arrière si besoin est. Pas assez de commits et il devient difficile d'identifier clairement la progresssion d'un projet tant les changements sont importants, trop de commits et on se noie vite dans un flot de détails.

### Stage

Avant de pouvoir effectuer une quelconque opération sur un fichier, il vous faudra d'abord ajouter ce dernier à la "stage".

Cela permet à Git d'être extrèmement flexible quant aux fichiers que vous voulez manipuler.

Vous pouvez en effet choisir précisément quels fichiers vous voulez ajouter à un commit et à quel moment vous souhaitez les ajouter. Admettons que vous ayez modifié plusieurs fichiers, cette notion de stage / staging vous permet de séparer ces fichiers en plusieurs groupes que vous pouvez manipuler séparément via Git.

### Repository distants, branches, merge et résolution de conflits

Pour permettre la collaboration, tout le monde travaille à l'aide de repositories locaux, et les changements réalisés par chaque membre de l'équipe sont envoyés (`push`) vers un repository distant considéré comme étant la référence (il s'agit ici d'une pûre convention). Chacun va également aller chercher les derniers changements sur ce repository distant (`pull`). Cela permet une collaboraton facile, puisque chacun dispose en local d'une version identique du projet contenant les modifications apportées par chaque membre de l'équipe.

C'est ici que les branches s'avèrent particulièrement utiles. Chacun peut créer une branche localement pour travailler sur la partie de projet dont il a la charge. Si une approche ne fonctionne pas, la branche peut simplement être supprimée. Une fois une partie de projet terminée, il suffit de l'appliquer à la branche master en utilisant un `merge`.

Lors d'un merge, Git va comparer les fichiers des deux branches et les combiner du mieux qu'il peut. Par exemple, si un développeur à modifié les lignes 1-10 d'un fichier et un autre développeur à modifié les lignes 15-20, git va simplement combiner ces changements.

Si Git ne peut pas lui même resoudre les conflits entre deux version d'un même fichier, il va alors marquer ces conflits comme devant être résolus manuellement. Dans le cadre de projet web, ces conflits sont habituellement relativement faciles à résoudre.

## Workflow git

Voici un workflow simple pour les projets web, adapté du workflow [Gitflow de Vincent Driessen](http://nvie.com/posts/a-successful-git-branching-model/)

- La branche master est le site tel que déployé en production
- Une branche de dévelopement est utilisée pour développer le projet et est souvent déployée sur un serveur de staging
- Les feature branches sont utilisées pour développer certaines features spécifiques qui sont suffisemment importantes que pour nécessiter de les séparer de la branche de dévelopement.
- Une fois une feature réalisée, la feature est mergée en dévelopement et testée sur le serveur de staging
- Une fois testée, la branche de dévelopement est alors mergée dans la branche master
- La feature branch peut ensuite être supprimée.

A vous de trouver [le workflow qui vous convient le mieux](https://www.atlassian.com/git/workflows). Personellement, j'utilise un hybride entre Gitflow et Feature Branch.

## Principales commandes

A tout moment, il vous est possible de consulter l'aide de git via les commandes `git help` et `git help <commande>` (`git help branch` par exemple). Pour quitter l'aide, appuyer simplement sur la touche `q` de votre clavier.

### Git init

`git init` permet d'initialiser un repository en le créant à partir d'un dossier ordinaire. Un dossier .git est alors ajouté au contenu du dossier.

### Git status

`git status` permet de visualiser l'état du repository.

A ce stade, aucun fichier n'est encore monitoré par le système. Nous alons utiliser les commande `git add` pour ajouter les fichiers au stage et ensuite `git commit -m "commit message"` pour enregistrer nos changements accompagnés d'un message.

### Git add

`git add index.html` permet d'ajouter un fichier au stage

`git add css/` permet d'ajouter tous les fichiers contenus dans le dossier "css" au stage

`git add '*.html'` permet d'ajouter tous les fichiers avec une extension .html au stage

`git add .` permet d'ajouter tous les fichiers au stage

### Git commit

`git commit -m "commit message"` permet de faire un commit à partir du stage en lui apposant le message "commit message"

Pour faire des messages de commit plus élaborés, vous pouvez utiliser votre éditeur de code. Dans ce cas, entrez simplement la commande `git commit` et votre éditeur (nano dans notre cas) prendra le relais.

### Commit & adding

`git commit -a -m "commit message"` permet d'ajouter vos fichiers au stage et de faire un commit simultanément en lui apposant le message "commit message"

### Git log

`git log` permet de visualiser l'historique de votre repository et tous les commits qui ont été réalisés.

Quelques options vous permettent de préciser les choses:

Vous pouvez limiter le nombre de commits visibles avec la commande `git log -2` pour obtenir seulement les deux derniers commits.

Vous pouvez encore demander à Git d'afficher seulement les commits liés à un seul fichier `git log index.html` ou limiter les commits à un seul utilisateur `git log --author=jeromecoupe`

`git log --pretty=oneline` ou `git log --oneline` permet de visualiser l'historique des commits en une seule ligne.

Il est également possible de de visualiser "graphiquement" votre repository avec les options suivantes: `git log --decorate --graph`

### Revenir en arrière avec revert et reset

Il est possible de revenir en arrière dans votre historique. C'est à cela que servent les commits et les hashs qui les identifient.

La commande `revert` permet de revenir en arrière sans affecter votre historique, vous revenez à votre commit choisi et vous devrez ensuite faire un `add` et un `commit` pour enregistrer les changements en résolvant les conflits éventuels.

`git revert 3ca7a822e4d4897eca2e651d0996429875452d05`

Si vous voulez revenir à un commit précis en supprimant tous les commits ayant eu lieu après ce point, utilisez la commande `reset`:

`git reset --hard 3ca7a822e4d4897eca2e651d0996429875452d05`

Si vous utilisez convenablement les branches, ce genre de situation est assez rare.

### Ignorer des fichers

Il est parfois très utile de pouvoir ignorer des fichiers dans un repository. Si vous travaillez avec un CMS dont certains fichiers de configuration sont spécifiques à votre machine locale, il est important d'ignorer ces fichiers.

De la même manière, des fichiers de log ou de cache peuvent également être ignorés systématiquement, de même que certains fichiers créés par l'opérating system.

Git ne peut ignorer que des fichiers qui ne sont pas monitorés (untracked files).

#### rm

Si vous avez par inadvertance ajouté des fichiers à un repository et que vous souhaitez les en retirer tout en gardant les fichires sur votre disque dur, utilisez la commande `git rm --cached <file>`.

Vous pouvez également cibler tous les fichiers dans un directory de manière récursive à l'aide de la commande `git rm -r --cached <folder>`

#### Fichier .gitignore

Un fichier .gitignore peut être créé dans n'importe quel directory pour ignorer certains fichiers de façon permamnente. Personellement, je préfère, dans la mesure du possible n'avoir qu'un seul fichier `.gitignore`. Voici un exemple d'un tel fichier.

```
*.DS_Store

/assets/images/captchas/*
!/assets/images/captchas/index.html

/assets/images/member_photos/*
!/assets/images/member_photos/index.html
```

## Branching et Merging

Git permet de créer des versions parallèles de votre projet appellées branches. Comme dit plus haut, cela permet de travailler sur un développement tout en laissant la branche `master` du projet en l'état.

### Git branch

`git branch` ou `git branch --list` permettent de voir toutes les branches actives dans votre repository. La branche sur laquelle vous travaillez (checked out branch) est marquée d'une astérisque "\*".

La commande `git branch dev` permet de créer une branche nommée "dev". Les noms de branches ne peuvent pas contenir d'espaces. Utilisez donc des tirets ou des underscores. La branche `dev` est une copie de la branche `master`au moment où elle a été créée.

### Git checkout

Pour passez sur une nouvelle branche de votre repository, utilisez la commande checkout: `git checkout dev`.

### Git merge

Pour appliquer les changements réalisés dans la branche `dev`à la branche `master` nous pouvons utiliser la commande `merge`. Aant toute chose, nous devons être certains que la branche active soit `master`. La règle de base est de toujours avoir comme branche active celle dans laquelle vous voulez merger.

`git checkout master` pour que la branche active soit master (la branche dans laquelle nous voulons merger les chnagements et commist réalisés dans `dev`)

`git merge dev` pour effectuer le merge.

Vous pouvez également forcer Git à toujours générer un commit pour le merge quoi qu'il arrive. Personellement, j'utilise toujours cette commande dans la mesure où elle permet de mieux visualiser les branches. `--no-ff` veut dire "no fast-forward", ce qui interdit à Git de faire le merge automatiquement sans générer de commit.

`git merge dev --no-ff`

### Supprimer une branche

`git branch -d dev` permet de supprimer la branche `dev`

### Gestion de conflits

Si Git n'arrive pas à réaliser le merge de lui même parce que des changements se sont produits pour les mêmes lignes des mêmes fichiers dans deux branches différentes, un conflit va se produire.

Git va alors nous demander de le règler manuellement et d'ensuite faire un commit pour enregistrer les changelents et pouvoir terminer le `merge`.

### Git stash

Git stash est une option intéressante lorsque vous avez une urgence et que vous voulez temporairement sauver votre travail non finalisé pour revenir à la situation de votre dernier commit. Pensez-y comme une sorte de clipboard perfectionné.

- `git stash`: permet de sauver les changements en cours et de revenir à la situation de votre dernier commit
- `git stash list`: permet de voir une liste des stash sauvés
- `git stash apply` permet ensuite de réappliquer ces changements et de reprendre le cours de votre travail.

## Travailler avec des repository distants

Jusqu'à présent, nous n'avons fait que travailler localement sur notre propre machine. Git devient véritablement un outil de collaboration lorsque vous ajoutez des repositories distants.

Chacun travaille sur son repository local et push et pull vers un repository distant hébergé sur un serveur quelque part, par exemple sur github. A ce sujet, voici un article intéressant concernant le fait de [collaborer à l'aide de github](http://net.tutsplus.com/articles/general/team-collaboration-with-github/). Une autre solution intéressante peut être de créer un [compte github pour une organisation](https://help.github.com/articles/what-s-the-difference-between-user-and-organization-accounts).

Nous pouvons alors ajouter un repository distant de la manière suivante:

`git remote add <name> git@github.com:jeromecoupe/testgit.git`

par exemple

`git remote add origin git@github.com:jeromecoupe/testgit.git` Dans ce cas c'est le nom "origin" que nous allons utiliser lorsque nous ferons des push et de pull.

`git remote` permet d'afficher la liste des repositories distants.

### Git push

- `git push origin --all` permet de faire un push de toutes les branches vers le repository distant "origin".
- `git push origin master` Permet de ne faire un push que de la branche master
- `git push origin :dev` ou `git remote remove dev` Permet de supprimer la branche "dev" du repository distant

### Git pull

`git pull origin master` permet de faire un pull de la branche master du repository distant.

### Git clone

Pour copier un repository distant sur votre machine locale, ulilisez simpelment la commande `git clone`

`git clone git@github.com:jeromecoupe/testgit.git <folder>`

par exemple

`git clone git@github.com:jeromecoupe/testgit.git git_test_repo`

## Interfaces graphiques

De nombreuses interfaces graphiques existent pour Git si le terminal n'est pas votre tasse de thé. Des interfaces graphiques existent également comme par exemple le client gratuit de github pour [mac](http://mac.github.com/) ou pour [windows](http://windows.github.com/).

Pour une liste des interfaces graphiques utilisables avec Git, voir la section qui leur est consacrée [sur le site officiel de Git](http://git-scm.com/downloads/guis).

Personnellement, j'utilise [Github Desktop](https://desktop.github.com/) qui est un programme gratuit, et facile d'utilisation. J'utilise également les fonctions Git de Visual Studio Code.

## Déployer vos sites à partir d'un repository

Certains hébergeurs de sites statiques tels que [Netlify](https://www.netlify.com/) ou [Vercel](https://vercel.com/) vous permettent de déployer vos sites automatiquement dès qu'un commit est détecté dans une branche donnée d'un repository Git (généralement `master`). [Github pages](https://pages.github.com/) utilise un système similaire.

De nombreuses solutions existent également pour déployer vos repositories Git vers un serveur de production ou de staging. Mes solutions favorites sont [Buddy](https://buddy.works/), [DeployHQ](https://www.deployhq.com/) et [Github Actions](https://docs.github.com/en/free-pro-team@latest/actions)

## Ressources

- [Get started with Git](http://alistapart.com/article/get-started-with-git) (A list Apart): Introduction générale.
- [Video: Introduction to Git by Mijingo](http://mijingo.com/products/screencasts/git-tutorial-video/) (Ryan Irelan): très bonne introduction très didactique.
- [Oh Shit, Git!?!](https://ohshitgit.com/): Bonne liste des petites astuces Git pour vous aider si vous avez l'impression de vous être trompés.
- [Git reference et cheat cheets](http://git-scm.com/docs): les man pages de git dispponibles en ligne, pas toujours digeste mais bonne référence.
- [Vidéos d'introduction à Git](http://git-scm.com/videos): vidéos officielles.
- [Git Immersion](http://gitimmersion.com/index.html) ([Neo](http://www.neo.com/)): une bonne introduction à Git, très complet.
- [Pro Git book](http://git-scm.com/book) (Scott Chacon): une belle bible sur le sujet.
- [Video: Introduction to Git with Scott Chacon of GitHub](https://www.youtube.com/watch?v=ZDR433b0HJY) (Scott Chacon): belle maestria!
- [Deux petits](http://www.johnfaulds.com.au/journal/developing-expressionengine-sites-with-mamp-git-tower-and-beanstalk-part-1/) [guides](http://www.johnfaulds.com.au/journal/developing-expressionengine-sites-with-mamp-git-tower-and-beanstalk-part-2/) d'utilisation de Git avec ExpressionEngine et Beanstalk (John Faulds)
