# Un travail de fond ...

Beaucoup de travail a tout d'abord été fait sur le code en lui même, avec assez peu de résultat visible "à l’œil nu", mais essentiel pour la suite du dévellopement :)

En effet, comme énoncé plus haut, la ZEP-12 part du constat qu'un article et un tutoriel ont énormément de choses en commun, et qu'il n'y avait donc pas de raisons de les traiter différemment. Il était donc d'une part nécessaire de repenser les modules pour qu'ils ne fassent plus qu'un. But du jeu : aucune duplications ! Ce qui a donc été réalisé permettra dans le futur d'implémenter plus facilement des fonctionnalités, qui seront directement disponibles pour les articles et les tutoriels. Le code est même assez souple pour pouvoir accueillir d'autres types de contenus (pourquoi pas [des tribunes](https://zestedesavoir.com/forums/sujet/976/zep-13-tribune-libre/) ?). Il s'agit donc bien de faciliter la vie des développeurs.

Par ailleurs, vous n'êtes pas sans savoir que notre module de rédaction utilise le célèbre [gestionnaire de version Git](https://fr.wikipedia.org/wiki/Git)[^git]. Pour les auteurs, cela se traduit par la possibilité de comparer différentes modifications apportées, via l'outil d'historique des versions :

[^git]: pour ceux que ça intéresse, Eskimon a écrit [un très bon tutoriel sur le sujet](https://zestedesavoir.com/tutoriels/649/refaire-lhistoire-avec-git/).

![Fonctionnalité de diff](http://zestedesavoir.com/media/galleries/1426/d78cdc66-bb0d-4afd-b1b8-06f5eade90b9.png.960x960_q85.png)
Figure: L'outil d'historique des version en action dans la ZEP-12 avec un exemple de correction, une application directe de l'utilisation de Git. À noter que cette page a été grandement améliorée [grâce à yapper-git](https://github.com/artragis/zds-site/pull/215).

L'ancien module avait également pour défaut de stocker les informations deux fois (une fois en base de donnée et une fois sur le disque), ce qui a entrainé des bugs par le passé dont la correction n'était pas très satisfaisante. Il a été choisi de se reposer sur Git (et donc le stockage sur le disque) dès que celà était possible et de soulager la base de donnée tout en profitant des avantages offerts par le gestionnaire de version. Ce choix a également un défaut, c'est qu'il requiert assez bien d'opérations de lecture/écriture (I/O, dans le langage des programmeurs) sur le disque, qui sont relativement couteuse en terme de temps. Une attention particulière a donc du être portée sur ce point, même si des améliorations sont probablement encore possible. À priori, les performances de ce nouveau module sont même équivalentes à l'ancienne !

Toutes ces modifications n'ont pas été sans mal, et par exemple, le module de recherche a dû être repensé pour accueillir cette manière de faire. C'est Hugo qui c'est occupé, avec brio, de cette partie, malgré que le module de recherche ne permet initialement pas d'indexer des fichiers. Grâce à lui, la recherche sur les contenus est réellement améliorée !

# ... Et de forme !

Mais la ZEP-12 n'améliore pas seulement la vie des développeurs, elle est aussi pensée pour les auteurs ! Puisque [la missions de Zeste de Savoir](https://zestedesavoir.com/pages/association/) est de « promouvoir le partage de connaissances à travers des ressources pédagogiques gratuites », il est essentiel de proposer un module qui soit le plus efficace et simple d'utilisation possible. Dès lors, et sans être exhaustif, voici une petite liste des améliorations apportées par ce nouveau module tout neuf.

Premièrement, une grande vague d'**uniformisation de l'interface et des fonctionnalités** a eu lieu. Désormais, tout les contenus possèdent une galerie, ce qui n'était pas le cas auparavant. D'autres fonctionnalités des tutoriels sont également apparues pour les articles, telles que la mise en bêta (ce qui permettra aux auteurs de ne plus avoir à écrire le message eu même dans [la zone bêta](https://zestedesavoir.com/forums/communaute/beta-zone/)), mais aussi l'apparition de [la demande d'aide pour les articles](https://zestedesavoir.com/contenus/aides/?type=article).

![Les galeries liées au contenu, une petite amélioration graphique pour marquer le lien entre les deux](http://zestedesavoir.com/media/galleries/1426/57b4587d-87b4-411b-91f9-4e616f78d683.png.960x960_q85.png)

Quelques changements sont aussi à noter du côté de la structure des contenus. Tout d'abord, **le mot "section" remplace désormais les "extraits"**, pour être plus simples à appréhender. Par ailleurs, un article contient désormais plusieurs de ces sections, comme vous avez pu le constater ici. Ce découpage rend plus facile l'édition, permet un meilleur référencement et donne droit à la création d'un sommaire[^seo]. À noter que durant le processus de migration à la ZEP-12, un script c'est ainsi chargé de repérer tout les titres présent dans les articles afin de découper ceux-ci en sections, vous n'avez donc rien à faire  ! :)

[^seo]: en effet, c'est désormais un titre de niveau 2 (`<h2>`) qui est employé à la place d'un titre de niveau 3, ce qui lui donne plus de poids. La présence du sommaire a également un impact sur le référencement.

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

Vous pouvez donc laisser libre cours à votre imagination et créativité, même si l'équipe de validation n'acceptera pas les abus de la déstructuration des contenus. Il faut en effet garder une cohérence dans ses écrits et l'équipe bénévole est là pour veiller au grain !

À noter que "partie" désigne désormais tout ce qui est au "premier niveau", même s'il contient des sections, tandis que "chapitre" désigne tout ce qui est au "second niveau" (et qui contient forcément des sections).

Tant qu'on en est dans les bonnes nouvelles, sachez également que l'édition externe est beaucoup plus simple, car **l'import d'archives à été fortement amélioré**. Comme vous pouvez [le constater par vous-même](https://zestedesavoir.com/contenus/importer/archive/nouveau/), il est désormais possible d'importer une archive pour créer un nouveau tutoriel ou article, mais également pour le mettre à jour (et contrairement à l'ancien système, pas besoin que la structure soit identique). Et pour faciliter encore un peu la possibilité d'édition externe, on peut désormais **importer directement les images avec le contenu**, et le texte sera mis à jour en conséquent !

![Import d'archive](http://zestedesavoir.com/media/galleries/1426/981c8b17-c1b9-4b09-a75a-caf3ee8f0c50.png.960x960_q85.png)
Figure: L'importation des archives est amélioré, il est même possible d'importer des images

Une des évolutions futures pourrait alors être de créer un éditeur externe qui créerait directement ladite archive à importer ensuite dans le site. Avis aux amateurs ! 

Finissons ce petit tour d'horizon, avec l'**amélioration des fonctionnalités de déplacement** grâce à un travail monstre effectué par artragis, ce qui permet désormais de déplacer les sections entre chapitres, mais aussi de déplacer les chapitre eux-mêmes, dans la limite du possible ! Si vous aviez un *big*-tuto que vous aimeriez transformer en moyen-tuto, c'est possible grâce à cette fonctionnalité !

![Déplacement d'un extrait](http://zestedesavoir.com/media/galleries/1426/35575d94-9cd5-4da7-985e-c168a80a5eca.png.960x960_q85.jpg)
Figure: Illustration du déplacement d'un extrait entre les chapitres

En vrac, on peut encore citer une amélioration du processus de publication (avec, entre autre, un système pour que les publications qui ont échouées n'affectent plus les versions déjà en ligne), un nettoyage de certaines erreurs générées par le précédent module, et d'autres [que vous pouvez retrouver dans la documentation du module](http://zds-site.readthedocs.org/fr/latest/back-end/contents.html) (qui décrit de manière plus complète la philosophie et les implications de ce nouveau module).

# Et la suite ?

Même si il s'agit déjà là d'une grande avancée dans le code de Zeste de Savoir, il reste encore bien des choses à faire, et ce module est probablement amené à encore bien évoluer dans le futur !

Ce module n'est également pas exempt de défaut, qui sont autant de choix qui ont du être fait (même si il a parfois été difficile de les respecter) : il a par exemple déjà été mentionné que se baser sur la lecture et l'écriture de fichiers est un point critique. Par exemple, il est nécéssaire de créer un fichier par section, ce qui requiert autant de lectures lorsque ces sections doivent être affichées. Par ailleurs, la phase de résolution d'URL (trouver quoi afficher) ne se reposant plus sur la base de donnée, elle nécéssite systématiquement la lecture du fichier contenant la structure du contenu (le `manifest.json`). Il a par ailleurs été très difficile de maintenir les [propritétés ACID](https://fr.wikipedia.org/wiki/Propriétés_ACID) (deux objets ne peuvent pas porter le même nom) et le référencement sur concernant ce module (ainsi, toutes les URLs de vos contenus on changés, mais des redirections ont dû être mises en place afin que les anciennes soient toujours valides).

Sur une note plus positive, plusieurs ZEPs attendaient tranquilement l'implémentation de la ZEP-12, ce qui est désormais chose faite :

+ La [ZEP-05](https://zestedesavoir.com/forums/sujet/676/zep-05-refonte-du-traitement-markdown-pour-lexport/), qui doit améliorer l'exportation de nos contenus en PDF, HTML ou EPUB, point qui n'as pas du tout été touché durant la ZEP-12 ;
+ La [ZEP-08](https://zestedesavoir.com/forums/sujet/724/zep-08-utilisation-de-git-pour-gerer-les-tutos-et-articles/) , qui s'interoge sur l'usage de fonctionnalités plus avancées de Git pour encore améliorer l'édition ;
+ La [ZEP-11](https://zestedesavoir.com/forums/sujet/3084/zep-11-interface-de-statistiques-sur-les-tutoriels/), qui implémenterait des statistiques pour l'auteur ;
+ La  [ZEP-13](https://zestedesavoir.com/forums/sujet/976/zep-13-tribune-libre/), qui se propose d'ajouter un troisième type de contenu, les "tribunes" ;
+ Les Les ZEPS [16](https://zestedesavoir.com/forums/sujet/1243/zep-16-page-de-proposition-de-corrections/) et [20](https://zestedesavoir.com/forums/sujet/2042/zep-20-relecture-des-tutos-par-les-pairs/), qui est une initiative pour améliorier le confort de validation via la relecture par des pairs et la propositions de corrections ;
+ la [ZEP-24](https://zestedesavoir.com/forums/sujet/2251/zep-24-refonte-et-enrichissement-des-notifications/), qui permetrai de repenser les notifications de manère plus efficace ;
+ Les ZEPS [15](https://zestedesavoir.com/forums/sujet/1082/zep-15-navigation-a-facettes-a-travers-le-site/), [31](https://zestedesavoir.com/forums/sujet/3149/zep-31-les-parcours-de-connaissances/) et [32](https://zestedesavoir.com/forums/sujet/3152/zep-32-cartographie-des-contenus/), qui tentent de repenser la manière dont on navigue entre les contenus ;
+ Les ZEPs [33](https://zestedesavoir.com/forums/sujet/3992/zep-33-template-de-tutoriels-et-editorialisation/) et [34](https://zestedesavoir.com/forums/sujet/4010/zep-34-template-de-tutoriels/), qui viserait guider les auteurs dans la création de leurs contenus.

Autant de sujets qui n'attendent que votre avis et votre aide ;)
