# Git version control

## Introduction

Git est un système de version control qui enregistre les changements réalisés dans le cadre de vos projets informatiques. Bien que principalement destné aux fichiers textes, git permet de placer n'importe quel type de fichier informatique dans une système de version control.

Créé en 2005 par Linus Torvalds ce système assez simple d'utilisation permet de facilement enregistrer les changements effectués sur des fichiers au sein d'un projet, de revenir en arrière si besoin est et même de gérer en paralèlle plusieurs versions de votre projet.

Un élément du succès de Git comme système de version control, c'est son caractère décentralisé. Là où d'autre systèmes dépendent d'un serveur central, git permet d'ajouter facilement cette capacité de version control à n'importe quel dossier présent localement sur votre ordinateur. Même si vous travaillez à l'aide d'un repository distant, la totalité de l'historique de votre projet est disponible localement.

En résumé:

- git vous permet de facilement suivre et enregistrer les changements apportés à vos fichiers et de facilement revenir en arrière si besoin est
- git (et github) facilitent grandement la collaboration et le travail en équipe sur des projets de natures très diverses
- git vous permet facilement de créer des branches distinctes pour vos projets et de les gérer en parallèle ou des les combiner en une seule version.

En outre de très nombreux tutoriaux, services et interfaces graphiques se sont dévelopés autur de Git, faisant de ce dernier un standard de l'industrie.

## Installation

Git est très facile à installer. Des programmes d'installation sont [disponibles pour toutes les plateformes](http://git-scm.com/downloads).

## Notions de base

Quelques notions de base à bien comprendre avant de commencer à utiliser Git.

### Repository

Lorsque vous initialisez Git pour l'un de vos dossiers à l'aide de la commande `git init`, vous créez ce que l'on appelle un repository. En fait, Git ajoute un dossier système invisible '.git' au contenu de votre dossier. C'est dans ce dossier invisible que git enregistre tous les changements que vous réalisez dans votre projet. Supprimez ce dossier .git et votre repository redevient un dossier ordinaire.

Git ne prend en compte que les changements de fichiers. Un directory vide n'existe pas pour Git.

### Branch

Tout repository git possède au moins une branche appellée `master'. C'est cette branche qui v vous permettre d'enregistrer vos changement. Sans branche, pas de version control.

Comme nous le verrons dans la suite, il est possible d'avoir de multiples branches au sein de projet, ce qui vous permet de travailler sur l'une au l'autre feature sans travailler sur la branche principale du projet et ainsi d'avanceer en parallèle ou de faire des essais sans prendre de risques inutiles. Les branches supplémentaires.

### Commits

Ls commits sont les soumissions que vous faites dans votre repository Git. Ils sont composés du détail des changements apportés aux fichiers qui comosent votre projet (modifications, ajouts ou suppressions) et du message qui accompagne et décrit ces modifications. Ces commit messages sont rédigés par vos soins et doivent idéalement décrire les changements apportés.

Il est important de réaliser ces commits regulièrement, afin de pouvoir faciement revenir en arrière si besoin est. Pas assez de commits et il devient difficile d'identifier clairement la progresssion d'un projet tant les changements sont importants, trop de commits et on se noie vite dans un flot de détails.

### Stage

Avant de pouvoir effectuer une quelconque opération sur un fichier, il vous faudra d'abord ajouter ce dernier au repository. Cela permet à Git d'être extrèmement flexible quant aux fichiers que vous voulez manipuler. Vous pouvez en effet choisir précisément quels fihiers vous voulez ajouter et quand. Admettons que vous ayez modifié plusieurs fichiers. Cette notion de stage / staging vous permet de séparer ces fichiers en plusieurs groupes que vous pouvez manipuler séparément via Git.

### Repository distants, branches, merge et résolution de conflits

Pour permettre la collaboration, tout le monde travaille à l'aide de repositories locaux, et les changements réalisés par chaque membre de l'équipe sont envoyés (push) vers un repository distant considéré comme étant la référence (il s'agit ici d'une pûre convention). Chacun va également aller chercher les derniers changements sur ce repository distant (pull). Cela permet une collaboraton facile, puisque chacun dispose en local d'une version identique du projet contenant les modifications apportées par chaque membre de l'équipe.

C'est ici que les branches s'avèrent particulièrement utiles. Cachun peut crer une branche localement pour travailler sur la partie de projet dont il a la charge. Si une approche ne fonctionne pas, la branche peut simplement être supprimée. Une fois une partie de projet terminée, il suffit de la réappliquer à la branche master en utilisant un merge.

Lors d'un merge, Git va comparer les fichiers des deux branches et les combiner du mieux qu'il peut. Par exemple, si un développeur à modifié les lignes 1-10 d'un fichier et un autre développeur à modifié les lignes 15-20, git va simplement combiner ces changements.

Si Git ne peut pas lui même resoudre le conflit entre deux version d'un même fichier, il va alors marquer ce conflit comme devant âtre résolu manuellement. Dans le cadre de projet web, ces conflits sont relativement faciles à résoudre.

## Workflow git

Voici un workflow simple pour les projets web, adapté du workflow [Gitflow de Vincent Driessen](http://nvie.com/posts/a-successful-git-branching-model/) 

- La branche master est le site tel que déployé en production 
- Une branche de dévelopement est utilisée pour développer le projet et est souvent déployée sur un serveur de staging
- Les feature branches sont utilisées pour développer certaines features spécifiques qui sont suffisemment importantes que pour nécessiter de les séparer de la branche de dévelopement.
- Une fois une feature réalisée, la feature mergée en dévelopement et testée sur le serveur de staging
- Une fois testée, la branche de dévelopement est alor mergée dans la branche master
- La feature branch peut ensuite être supprimée.

A vous de trouver [le workflow qui vous convient le mieux](https://www.atlassian.com/git/workflows). Personellement, j'utilise un hybride entre Gitflow et Feature Branch.

## Principales commandes

A tout moment, il vous est possible de consulter l'aide de git via les commandes `git help` et `git help <commande>` (`git help branch` par exemple). Pour quitter l'aide, appuyer simplement sur la touche `q` de votre clavier.

### Git init

`git init` permet d'initialiser un repository en le créant à partir d'un dossier ordinaire. Un dossier .git est alors ajouté au contenu du dossier.

### Git status

`git status` permet de visualiser l'état du repository.

A ce stade, aucun fichier n'est encore monitoré par le système. Nous alons utiliser les commande `git add` pour ajouter les fichier au stage et ensuite `git commit` pour enregistrer nos changements accompagnés d'un message.

### Git add

`git add index.html` permet d'ajouter un fichier au stage

`git add css/` permet d'ajouter tous les fichiers contenus dans le dossier "css" au stage

`git add '*.html'` permet d'ajouter tous les fichiers avec une extension .html au stage

`git add *` permet d'ajouter tous les fichiers au stage

### Git commit

`git commit -m "commit message"` permet de faire un commit à partir du stage en lui apposant le message "commit message"

### Commit and adding

### Git log

### Ignorer des fichers

#### Ignore

#### Fichier .gitignore

## Branching et Merging

### Git branch

### Git merge

### Git checkout

## Travailler avec des repository distants

### Git clone

### Git pull

### Git push

## Interfaces graphiques

## Déployer vos sites avec Git et Beanstalk

