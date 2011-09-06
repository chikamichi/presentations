!SLIDE center 
# Git

## un workflow agile

!SLIDE
## Commençons par les liens

* [The git community book](http://book.git-scm.com)
* [GitReady](http://www.gitready.com)
* [ProGit](http://progit.org/book/)

!SLIDE
## À quoi sert git ?

!SLIDE bullets incremental
* À **sauvegarder** des états successifs de fichiers et dossiers
* À **partager** ces **versions**
* À gérer **plusieurs** versions en même temps

!SLIDE
## Les outils de base

!SLIDE
Git utilise des **objets** pour organiser un projet versionné. Un objet est représenté par un code **SHA1** unique, du type :

      6ff87c4664981e4397625791c8ea3bbb5f2279a3

Un objet peut être :

* un **blob**
* un **tree**
* un **commit**
* un **tag**

Enfin, des **commandes pour créer et manipuler** ces objets :

      git init|clone|add|commit|pull|push|…

!SLIDE

    $> tree
    .
    |-- README
    `-- lib
        |-- inc
        |   `-- tricks.rb
        `-- mylib.rb
    2 directories, 3 files

!SLIDE center
![Les objets de git](./objects-example.png)

!SLIDE incremental
## Le répertoire versionné

!SLIDE bullets incremental

* Le ***working directory*** est le dossier versionné à proprement parler. Ses fichiers et dossiers sont déplacés ou supprimés suite à certaines commandes `git …`. C'est donc un espace de travail, pour git et pour vous.
* La ***staging area*** ou ***index*** est une zone virtuelle qui permet de signaler les versions temporaires de fichiers prêtes à être commitées, puis partagées.

!SLIDE bullets incremental

Un fichier ou un dossier du ***working directory*** peut être dans l'un des états suivants, du point de vue de git :

* *untracked*, git ne va pas y toucher
* l'état par défaut pourrait s'appeler *up-to-date* ou *unmodified*
* *modified*, par rapport à la version *up-to-date*
* *staged*, le fichier est prêt à être commité, il réside dans l'***index***

!SLIDE
## Commit

!SLIDE
**Commiter, c'est créer une nouvelle version dans l'historique.**

La recette pour créer un commit :

* sélectionner les fichiers/dossiers dans l'état *modified*
* les faire passer en *staged*
* créer le commit pour l'*index* ainsi créé
* éventuellement, partager le nouvel historique

!SLIDE
**Un commit, c'est aussi un message qui décrit sa raison d'être.**

Canoniquement, un bon message de commit aurait cette forme :

      Une courte description (une ligne), un n° de ticket
   
      Après une ligne vide, une description plus longue
      du pourquoi du comment, si nécessaire. On pourrait
      y mentionner des précisions importantes, comme des
      changements cassant la rétro-compatibilité du code,
      de nouvelles clés de conf à remplir, la logique
      générale d'un bugfix s'il est un peu compliqué…
   
      * parfois,
      * une liste,
      * c'est bien aussi !

!SLIDE
## Une spécificité de git : les branches (faciles)

!SLIDE
Branches de quel arbre ? De l'historique du projet !

**Créer une branche, c'est initier une nouvelle suite de versions**. On peut changer de branche à loisir et faire grossir une branche de l'historique sans toucher aux autres. Par exemple, une branche `rails2`, une autre `rails3`, une `experimental`…

Git permet de créer et de gérer des branches très facilement :

    git branch
    git checkout -b ma_nouvelle_branche
    git checkout ma_nouvelle_branche
    git checkout master
    git branch -d ma_nouvelle_branche

!SLIDE
## Travailler en équipe

!SLIDE bullets incremental
* Git : gestion de versions **décentralisée** (P2P)
* Mais on peut ajouter une **synchronisation**…
* …en utilisant un dépôt central (aargh!)

!SLIDE
## Une proposition de workflow

!SLIDE bullets incremental

* Git est assez générique, propose beaucoup de commandes…
* Manifestement, plusieurs types d'utilisation sont possibles.
* Notre contexte : **travail en équipe**, avec un **dépôt central** (synchro), pour des projets (relativement) **agiles**.
* Objectif 1 : essayer de minimiser au maximum les conflits !
* Objectif 2 : essayer de travailler proprement !

!SLIDE
## Je parlerai…

!SLIDE bullets incremental
* des branches : `master`, et les autres (quelles autres ?)
* du status privilégié du dépôt central (`origin` ?)
* de `git pull` vs `git fetch` (?)
* de `git rebase` (??)
* de l'option `--interactive` ⇢ `git rebase -i origin/master` (!?!)
* de l'*index*,  de `git diff` et ses options (…)
* de `git checkout`, `git branch` et `git merge` (O_ô)
* et même de `git stash`, `git push`, du `.gitconfig`…
* le tout, assemblé dans une recette simple et efficace !
