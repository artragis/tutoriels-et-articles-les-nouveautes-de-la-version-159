# Un travail de fond ...

Beaucoup de travail a tout d'abord été fait sur le code en lui-même, avec 
assez peu de résultats visibles par les membres, mais essentiels pour la suite 
du développement.

En effet, comme énoncé plus haut, la ZEP-12 part du constat qu'un article et 
un tutoriel ont énormément de propriétés en commun, et qu'il n'y avait donc 
pas de raison de les traiter différemment. Il était donc d'une part nécessaire 
de repenser les modules pour qu'ils ne fassent plus qu'un. But du jeu : aucune 
duplication. Ce qui a été réalisé permettra donc dans le futur d'implémenter 
plus facilement des fonctionnalités, qui seront directement disponibles pour 
les articles et les tutoriels. Le code est même assez souple pour pouvoir 
accueillir d'autres types de contenus, tels que [des tribunes libres](https://zestedesavoir.com/forums/sujet/976/zep-13-tribune-libre/). 
Il s'agit donc bien en premier lieu de faciliter la vie des développeurs.

Par ailleurs, vous n'êtes pas sans savoir que notre module de rédaction 
utilise le célèbre gestionnaire de version 
[Git](https://git-scm.com/book/en/v2). Pour les auteurs, cela se traduit par 
la possibilité de comparer différentes modifications apportées, via l'outil 
d'historique des versions :

![Fonctionnalité de diff](http://zestedesavoir.com/media/galleries/1426/d78cdc66-bb0d-4afd-b1b8-06f5eade90b9.png.960x960_q85.png)
Figure: Une application directe de l'utilisation de Git : l 'outil d'historique des versions en action dans la ZEP-12 avec un exemple de correction. À noter que cette page a été grandement améliorée par [yapper-git](https://github.com/artragis/zds-site/pull/215).

L'ancien module avait également pour défaut de stocker les informations deux 
fois : une fois en base de données et une autre dans des fichiers, ce qui a 
entraîné par le passé des bugs dont la correction n'était pas très 
satisfaisante. Il a donc été choisi de se reposer sur Git (et donc le stockage 
sur le disque) dès que cela était possible et de soulager la base de données 
tout en profitant des fonctionnalités offertes par le gestionnaire de version. 
Toutefois, cette option a un défaut : elle requiert un nombre important 
d'opérations de lecture/écriture (*IO*, pour les programmeurs) sur le disque, 
lesquelles sont relativement coûteuses en temps. Une attention particulière a 
donc du être portée sur ce point, même si des améliorations sont probablement 
encore possibles. À priori, les performances de ce nouveau module sont mêmes 
équivalentes à celles de l'ancien.

Toutes ces modifications n'ont pas été sans mal et, par exemple, le module de 
recherche a dû être repensé pour coïncider avec cette nouvelle philosophie. En 
effet, ce module ne permettait initialement pas d'indexer des fichiers, 
quasiment utilisés exclusivement par le nouveau module rédactionnel. Hugo est 
donc passé par là et a amélioré avec brio la recherche de contenus.

# ... Et de forme !

Mais les avantages de la ZEP-12 ne se restreignent pas aux développeurs, et 
les auteurs gagnent également au change. En effet, puisque 
[la missions de Zeste de Savoir](https://zestedesavoir.com/pages/association/) 
est de « promouvoir le partage de connaissances à travers des ressources 
pédagogiques gratuites », il est essentiel de proposer un module qui soit le 
plus efficace et simple d'utilisation possible. Dès lors, et sans être 
exhaustif, nous avons le plaisir de vous présenter les fonctionnalités 
introduites par ce module tout neuf et dont les auteurs pourront bénéficier 
directement.

Premièrement, une grande vague d'**uniformisation de l'interface et des fonctionnalités** 
a eu lieu : tous les contenus possèdent une galerie, tous peuvent être mis en 
bêta et tous bénéficient de la page d'aide aux auteurs.

![Les galeries liées au contenu, une petite amélioration graphique pour marquer le lien entre les premières et les secondes](http://zestedesavoir.com/media/galleries/1426/57b4587d-87b4-411b-91f9-4e616f78d683.png.960x960_q85.png)

Quelques changements sont aussi à noter du côté de la structure des contenus. 
Tout d'abord, **le mot « section » remplace désormais le terme « extrait »**, 
le premier étant plus simple à appréhender. Par ailleurs, un article peut 
désormais contenir plusieurs de ces sections, comme vous avez pu le constater 
en ce moment même. Ce découpage rend plus facile l'édition, permet un meilleur 
référencement et donne droit à la création d'un sommaire[^seo]. À noter que 
durant le processus de migration vers la ZEP-12, un script s'est chargé de 
repérer tous les titres présents dans les articles et de découper ceux-ci en 
sections : vous n'avez qu'à admirer le résultat !

[^seo]: en effet, l'ajout de sections revient à ajouter un niveau de titres, 
lesquels ont du poids pour les moteurs de recherche. La présence du sommaire a 
également un impact bénéfique sur le référencement.

En outre, les contraintes sur la structure se sont considérablement assouplies.
Désormais, vous disposez de trois types de conteneurs : les *parties*, sans 
parents et avec un ou des enfants, les *chapitres*, avec un parent (une partie)
et des (ou un) enfants, et une section, sans enfants. À partir de là, vous 
pouvez créer, supprimer et déplacer des conteneurs comme il vous sied, du 
moment que vous respectez les contraintes d'imbrication (une partie contenant 
un chapitre comportant une section ne peut être déplacée en tant qu'enfant, ce 
qui créerait une conteneur de niveau 4). Notamment, il est possible de créer 
des moyens-tutos, ainsi que des tutoriels hybrides :

```
+ Partie 1 
    + Section 1.1
    + Section 1.2 
    + Section 1.3 
+ Partie 2
    + Chapitre 2.1
        + Section 2.1.1
        + ...
```
Code: Structure *hydride* où la première partie contient directement des sections, tandis que la seconde est découpée en chapitres.

Par contre, un conteneur est homogène. Le cas suivant ne fonctionne donc pas.

```
+ Partie
    + Chapitre
        + Section
    + Section
```

Vous pouvez donc laisser libre cours à votre imagination et créativité, même 
si l'équipe de validation n'acceptera pas les abus de déstructuration des 
contenus. Il faut en effet garder une cohérence dans ses écrits et l'équipe 
bénévole est là pour veiller au grain !

Tant qu'on en est aux bonnes nouvelles, sachez également que l'édition externe 
est beaucoup plus simple, car **l'import d'archives a été fortement amélioré**. 
Comme vous pouvez [le constater par vous-même](https://zestedesavoir.com/contenus/importer/archive/nouveau/), 
il est désormais possible d'importer une archive pour créer un nouveau 
tutoriel ou article, mais également pour le mettre à jour (et contrairement à 
l'ancien système, la structure n'a pas à être identique). Et pour faciliter 
encore un peu la possibilité d'édition externe, on peut désormais **importer 
directement les images avec le contenu**, et le texte sera mis à jour en 
conséquence.

![Import d'archive](http://zestedesavoir.com/media/galleries/1426/981c8b17-c1b9-4b09-a75a-caf3ee8f0c50.png.960x960_q85.png)
Figure: L'importation des archives est améliorée. Il est même possible d'importer des images.

Il est alors tout à fait possible de créer un éditeur externe qui génèrerait 
directement ladite archive à importer ensuite sur le site. Avis aux amateurs ! 

Finissons ce petit tour d'horizon, avec l'**amélioration des fonctionnalités 
de déplacement** grâce à un travail monstre effectué par artragis, ce qui 
permet désormais de déplacer les sections entre chapitres, mais aussi de 
déplacer les chapitre eux-mêmes, dans la limite du possible ! Si vous aviez un 
*big*-tuto que vous aimeriez transformer en moyen-tuto, c'est possible grâce à 
cette fonctionnalité !

![Déplacement d'un extrait](http://zestedesavoir.com/media/galleries/1426/35575d94-9cd5-4da7-985e-c168a80a5eca.png.960x960_q85.jpg)
Figure: Illustration du déplacement d'un extrait entre les chapitres

En vrac, on peut encore citer une amélioration du processus de publication 
(avec, entre autre, un système pour que les publications qui ont échoué 
n'affectent plus les versions déjà en ligne), un nettoyage de certaines 
erreurs générées par le précédent module, et d'autres 
[que vous pouvez retrouver dans la documentation du module](http://zds-site.readthedocs.org/fr/latest/back-end/contents.html) 
(qui décrit de manière plus complète la philosophie et les implications de ce 
nouveau module).
