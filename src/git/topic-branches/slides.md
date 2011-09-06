!SLIDE center 
# Les *topic branches*
## et la commande `rebase`

!SLIDE bullets incremental

* Une branche est un pointeur vers un commit dans l'historique.
* Git fait essentiellement de la manipulation d'historique…
* … donc, c'est **facile** de manipuler des branches. **Utilisons-les !**

!SLIDE
## Trois stratégies pour
## l'utilisation des branches

!SLIDE bullets incremental

* pas de stratégie => tout dans `master`
* *release branches*
* ***topic branches***

!SLIDE
## Ok, des branches, mais pourquoi faire ?

* **Séparer** le code **développement** du code **production**.
* **Organiser** son travail en unités indépendantes (**topics**)
* **Partager** facilement **certaines choses** seulement
* **Conserver** un historique commun propre (**`master`**)
* Un dépôt central n'est jamais qu'une branche distante.

!SLIDE
## Trois stratégies pour
## la fusion de branches

!SLIDE bullets incremental

* *fast-forward merge*
* *recursive merge*
* ***rebasing***

!SLIDE
## Créer une branche

    git branch ma-branche
    git checkout ma-branche

    git checkout -b ma-branche

    git branch ma-branche HEAD
    git branch ma-branche e24f56

!SLIDE
## Se situer, se déplacer

    git branch
    git checkout une-branche

!SLIDE
## Supprimer une branche

    git branch -d ma-branche
    git branch -D ma-branche

Supprime le pointeur vers le commit, pas le commit lui-même.

Exemple : pour une release, créer un tag (v2.1…), supprimer la branche
associée (`v2.1`). On peut recréer une branche (`v2.1.1`) à partir du
tag, les commits et donc l'historique associé n'ont jamais disparus.

!SLIDE
## Fusionner avec `merge`

La commande se lit ainsi :

    git merge une-branche [dans-une-autre]

Exemples :

    git merge experimental master

    git checkout master
    git merge experimental

    git pull origin master

!SLIDE
## Options utiles de `merge`

Ne pas commiter automatiquement :

    git merge --no-commit

Ne pas faire du fast-forward, mais créer un commit explicite :

    git merge --no-ff

Un message de commit un peu plus explicite :

    git merge --log

!SLIDE center
# `git rebase`

## Réécriture de l'historique      

!SLIDE center
# `git rebase`

## Réécriture de l'historique (!!)

!SLIDE
## Principe de base

`rebase` prend une sélection de commits (par exemple, toute une branche),
et les rejoue à la suite d'un autre commit (par exemple, le dernier commit
d'une autre branche). Les SHA1 sont recalculés.

Intérêt : pouvoir déplacer des commits d'un historique à un autre tout en
conservant une suite de commits linéaire, simple à explorer.

!SLIDE
## Hein !?

!SLIDE
## Schématiquement

* `merge` : historique complet (non modifié), mais rapidement inexpoitable
* `rebase` : historique modifié (linéarisé), mais exploitable

!SLIDE
## Dans le détail

### Avec `rebase`…

* l'historique est compréhensible par un être humain
* la localisation des bugs est facilitée (surtout avec `git bisect`) et
il est *toujours* possible d'isoler un (petit) commit responsable
* les conflits sont résolus un par un, pas tous à la fois
* la branche commune (`origin`) n'est pas polluée par des commits de `merge`
* si tout le monde utilise `git pull --rebase`, aucune résolution de conflit
à faire
* le travail d'intégration est très simple (pas ou peu de conflits)

!SLIDE
## Exemples concrets

    git rebase master
    git rebase e25f5d6

    git rebase --continue
    git rebase --skip
    git rebase --abort

    git reset --hard ORIG_HEAD

!SLIDE
# Avec un dépôt central
## (*shared repository*)

!SLIDE
### Rappatrier les changements partagés par les autres

`fetch` ou `pull`

`pull` == `fetch` dans l'index, puis `merge` dans `master`

    git pull --rebase # stratégie

### Partager ses commits

`push`

!SLIDE incremental center
## Les *remote branches/repositories*

Pour une autre présentation ^^

!SLIDE
## Prêts à utiliser
## des *topic branches*

!SLIDE
## En fait, j'ai déjà tout dit :)

    # 1
    git checkout -b 243-edit-user-profile

    # 2
    # hack, hack…
    # git add, git commit, git add, git commit…

    # 3
    git rebase master

    # goto 2 autant de fois que nécessaire

    # 4
    git checkout master
    git rebase [-i] 243-edit-user-profile
    git branch -d 243-edit-user-profile
    git push

!SLIDE bullets incremental
## Quelques remarques

* Il faut bien comprendre le *workflow* associé à `rebase`.
* Une approche drastique (« aucun commit sur `master` ») n'est pas toujours
pertinente, mais elle est souvent recommandée par les intégrateurs de projets
*open source*.
* Éviter les `rebase` sur des commits partagés.
* Devient vraiment utile si tous les membres de l'équipe l'utilise, car…
* … `rebase` est fait pour gérer des branches, donc…
* … notamment un dépôt central et/ou des *topic branches* !


!SLIDE
## Un peu plus loin…

* [`git rebase --interactive`](http://book.git-scm.com/4_interactive_rebasing.html) 
* [`git rebase --onto`](http://progit.org/book/ch3-6.html)
* [`merge` vs `rebase`](http://blog.experimentalworks.net/2009/03/merge-vs-rebase-a-deep-dive-into-the-mysteries-of-revision-control/)
* [The Perils of Rebasing](http://progit.org/book/ch3-6.html)
