Honnêtement, j'ignore quoi écrire comme texte ici, donc je vais mettre **n'importe quoi**. Vous ne m'en voulez pas j'espère ?

Le cas échéant, je vous invite cordialement à rager dans votre coin : les cacas nerveux, c'est pas pour les zesteux !

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
pouvez créer, supprimer et déplacer des conteneurs à gogo, du moment que vous 
respectez les contraintes d'imbrication (une partie contenant un chapitre 
comportant une section ne peut être déplacée en tant qu'enfant, ce qui créerait
une conteneur de niveau 4). Notamment, il est possible de créer des 
moyens-tutos, ainsi que des tutoriels hybrides :

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
Figure: L'importation des archives est amélioré, il est même possible d'importer des images

Une des évolutions futures pourrait alors être de créer un éditeur externe qui 
créerait directement ladite archive à importer ensuite dans le site. Avis aux 
amateurs ! 

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
