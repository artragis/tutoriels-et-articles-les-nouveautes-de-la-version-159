# Un travail de fond ...

Beaucoup de travail a tout d'abord été fait sur le code en lui même, avec assez peu de résultat visible "à l’œil nu", mais essentiel pour la suite :)

En effet, comme énoncé plus haut, la ZEP-12 part du constat qu'un article et un tutoriel ont énormément de choses en commun, et qu'il n'y avait donc pas de raisons de les traiter différemment. Il était donc d'une part nécessaire de repenser les modules pour qu'ils ne fassent plus qu'un. But du jeu : plus de duplications ! Ce qui a donc été réalisé permettra dans le futur d'implémenter plus facilement des fonctionnalités, qui seront directement disponibles pour les articles et les tutoriels. Le code est même assez souple pour pouvoir accueillir d'autres types de contenus (pourquoi pas [des tribunes](https://zestedesavoir.com/forums/sujet/976/zep-13-tribune-libre/) ?). Il s'agit donc bien ici de faciliter la vie des développeurs.

Par ailleurs, vous n'êtes pas sans savoir que notre module de rédaction utilise le célèbre [gestionnaire de version Git](https://fr.wikipedia.org/wiki/Git). Cette fonctionnalité permet aux auteurs de "remonter dans le temps" afin de voir les changements qui ont été effectués d'édition en édition. En pratique, cela signifie par exemple que plusieurs auteurs d'un même contenu peuvent vérifier ce qui a été fait par les autres.

![Fonctionnalité de diff](http://zestedesavoir.com/media/galleries/1426/d78cdc66-bb0d-4afd-b1b8-06f5eade90b9.png.960x960_q85.png)
Figure: L'outil de *diff* en action avec un exemple de correction, une application directe de l'utilisation de Git. À noter que cette page a été grandement améliorée dans la ZEP-12 [grâce à yapper-git](https://github.com/artragis/zds-site/pull/215).

Dans l'ancien module, les informations étaient stockées deux fois : directement sur le disque et dans la base de donnée. Cela a donné lieux à plusieurs bugs, il a donc été décidé de ne stocker que le strict nécessaire en base de donnée et de ce reposer sur Git pour le reste. Ainsi, on est sur que ce qui est affiché correspond bien à une version donnée, et on soulage la base de donnée de ces appels pour tout les niveaux de structures d'un contenu (parties, chapitres et extraits étaient autrefois autant de lignes dans la base de données). Une fois encore, l’intérêt est d'éviter la copie de données inutiles et les erreurs (tant au niveau du code que des données en elles-mêmes) que ça peut entraîner.

À terme, ces améliorations pourraient conduire à l'édition externe des tutoriels et articles, ainsi qu'à l'emploi de différentes *branches* pour permettre aux auteurs de travailler en parallèle (il s'agit d'ailleurs du thème de [la ZEP-08](https://zestedesavoir.com/forums/sujet/724/zep-08-utilisation-de-git-pour-gerer-les-tutos-et-articles/)) ;)

Toutes ces modifications n'ont pas été sans mal, et par exemple, le module de recherche a dû être repensé pour accueillir cette manière de faire. C'est Hugo qui c'est occupé, avec brio, de cette partie, malgré que le module de recherche ne permet initialement pas d'indexer des fichiers. Grâce à lui, la recherche sur les contenus est toujours possible :)

# ... Et de forme !

Mais la ZEP-12 n'améliore pas seulement la vie des développeurs, elle est aussi pensée pour les auteurs ! Puisque [la missions de Zeste de Savoir](https://zestedesavoir.com/pages/association/) est de « promouvoir le partage de connaissances à travers des ressources pédagogiques gratuites », il est essentiel de proposer un module qui soit le plus efficace et simple d'utilisation possible. Dès lors, et sans être exhaustif, voici une petite liste des améliorations apportées par ce nouveau module tout neuf.

Premièrement, une fonctionnalité qui était très attendue, c'est que désormais, **tout les contenus possèdent une galerie**. En effet, cette fonction n'était pas encore disponible pour les articles, c'est désormais chose faites.

![Les galeries liées au contenu](http://zestedesavoir.com/media/galleries/1426/57b4587d-87b4-411b-91f9-4e616f78d683.png.960x960_q85.png)

Outre les galeries, d'autres fonctionnalités des tutoriels sont également apparues pour les articles, telles que la mise en bêta, qui ravira les auteurs jusqu'ici obligés de faire des copier/coller, mais aussi [la demande d'aide](https://zestedesavoir.com/contenus/aides/?type=article).

Quelques changements sont aussi à noter du côté de la structure des contenus. Tout d'abord, **le mot "section" remplace désormais les "extraits"**, pour être plus simples à appréhender. Par ailleurs, un article contient désormais plusieurs de ces sections, comme vous avez pu le constater ici. Ce découpage rend plus facile l'édition, permet un meilleur référencement et donne droit à la création d'un sommaire. À noter que durant le processus de migration à la ZEP-12, un script c'est ainsi chargé de repérer tout les titres de niveaux 1 présent dans les articles afin de découper ceux-ci en sections, vous n'avez donc rien à faire  ! :)

De nouveaux types de structures sont également permises, puisque la "taille" d'un tutoriel n'est plus fixé à sa création et évolue à votre convenance (il n'est bien entendu pas possible de faire des chapitres dans les articles). Ainsi, **les moyens-tutoriels sont enfin possibles**, ce qui n'oblige plus à créer des tutoriels ne contenant qu'une partie, mais il est également possible de réaliser des structures *hydrides*. Ainsi, si on prend l'exemple hypothétique d'un tutoriel qui traiterai d'une bibliothèque en programmation, on pourrait imaginer quelque chose du genre :

```
+ Introduction (partie)
    + Petite histoire (section)
    + Installation (section)
    + Tester ! (section)
+ Prise en main (partie)
    + Prise en main (chapitre)
        + Fonctions de base (section)
        + ...
```
Code: Structure *hydride* ou la première partie contient directement des sections, tandis que la seconde est découpée en chapitres.

Vous pouvez donc laisser libre cours à votre imagination et créativité. À noter que "partie" désigne désormais tout ce qui est au "premier niveau", même s'il contient des sections, tandis que "chapitre" désigne tout ce qui est au "second niveau" (et qui contient forcément des sections).

Tant qu'on en est dans les bonnes nouvelles, sachez également que l'édition externe est beaucoup plus simple, car **l'import d'archives à été fortement amélioré**. Comme vous pouvez [le constater par vous-même](https://zestedesavoir.com/contenus/importer/archive/nouveau/), il est désormais possible d'importer une archive pour créer un nouveau tutoriel ou article, mais également pour le mettre à jour (et contrairement à l'ancien système, pas besoin que la structure soit identique). Et pour faciliter encore un peu la possibilité d'édition externe, on peut désormais **importer directement les images avec le contenu**, et le texte sera mis à jour en conséquent !

![Import d'archive](http://zestedesavoir.com/media/galleries/1426/981c8b17-c1b9-4b09-a75a-caf3ee8f0c50.png.960x960_q85.png)
Figure: L'importation des archives est amélioré, il est même possible d'importer des images

Une des évolutions futures pourrait alors être de créer un éditeur externe qui créerait directement ladite archive à importer ensuite dans le site. Avis aux amateurs !

Finissons ce petit tour d'horizon, avec l'**amélioration des fonctionnalités de déplacement** grâce à un travail monstre effectué par artragis, ce qui permet désormais de déplacer les sections entre chapitres, les chapitres entre parties, ou encore de transformer un chapitre en partie (et inversement), dans la limite du possible ! Si vous aviez un *big*-tuto que vous aimeriez transformer en moyen-tuto, c'est donc possible grâce à cette fonctionnalité !

![Déplacement d'un extrait](http://zestedesavoir.com/media/galleries/1426/35575d94-9cd5-4da7-985e-c168a80a5eca.png.960x960_q85.jpg)
Figure: Illustration du déplacement d'un extrait entre les chapitres

En vrac, on peut encore citer une amélioration du processus de publication (avec, entre autre, un système pour que les publications qui ont échouées n'affectent plus les versions déjà en ligne), un nettoyage de certaines erreurs générées par le précédent module, et d'autres [que vous pouvez retrouver dans la documentation du module](http://zds-site.readthedocs.org/fr/latest/back-end/contents.html) (qui décrit de manière plus complète la philosophie et les implications de ce nouveau module).