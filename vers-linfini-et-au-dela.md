# Un mieux, mais seulement un début

Même si il s'agit déjà là d'une grande avancée dans le code de Zeste de 
Savoir, il reste encore bien des choses à faire, et ce module sera probablement 
amené à encore bien évoluer.

En effet, il n'est pas exempt de défaut, qui sont autant de choix qui ont dû 
être faits (même s'il a parfois été difficile de les respecter). Par exemple,
il a déjà été mentionné que se baser sur la lecture et l'écriture de fichiers 
est un point critique. Notamment, il est nécéssaire de créer un fichier par 
section, ce qui requiert autant de lectures lorsque celles-ci doivent être 
affichées. Par ailleurs, la phase de résolution d'URL (trouver quoi afficher), 
ne reposant plus sur la base de données, nécessite systématiquement la lecture
du fichier contenant la structure du contenu (le `manifest.json`). 

De même, la ZEP-12 n'apporte pas de réelle révolution dans l'interface. Ainsi, pour la majorité
des utilisateurs, le travail réalisé sur le fond semblera invisible, peut être même insuffisant.
Ce travail de fond était d'une ampleur si importante que malgré 9 mois de développement, certaines
*killer features* tant pour l'interface que pour la vie du site n'ont pas pu être développées, à notre
grande frustration.

Le plus gros problème, en terme d'interface restera que pour vous donner la possibilité de faire
un *tutoriel moyen* et autres structures plus souples,
nous avons retiré le champ qui auparavant vous permettait de sélectionner "mini tuto" ou "big tuto".
Cela signifie que nous ne vous guidons plus dans la rédaction d'un contenu.

Ce manque de "révolution" se fera aussi sentir du côté des validateurs qui feront encore face
à de longues attentes lors de la publication d'un gros tutoriel.

Il a par ailleurs été très difficile de maintenir les 
[propritétés ACID](https://fr.wikipedia.org/wiki/Propriétés_ACID) (deux objets 
ne peuvent pas porter le même nom par exemple) et le référencement concernant ce module 
(par exemple, toutes les URLs de vos contenus ont changé, et des redirections 
ont dû être mises en place afin que les anciennes soient toujours valides).

# Une fenêtre sur le monde

Sur une note plus positive, plusieurs ZEP attendaient tranquillement 
l'implémentation de la douzième du nom, ce qui est désormais chose faite. 

+ La [ZEP-05](https://zestedesavoir.com/forums/sujet/676/zep-05-refonte-du-traitement-markdown-pour-lexport/), qui doit améliorer l'exportation de nos contenus en PDF, HTML ou EPUB, point qui n'as pas du tout été touché durant la ZEP-12 ;
+ La [ZEP-08](https://zestedesavoir.com/forums/sujet/724/zep-08-utilisation-de-git-pour-gerer-les-tutos-et-articles/) , qui s'interoge sur l'usage de fonctionnalités plus avancées de Git pour encore améliorer l'édition ;
+ La [ZEP-11](https://zestedesavoir.com/forums/sujet/3084/zep-11-interface-de-statistiques-sur-les-tutoriels/), qui implémenterait des statistiques pour l'auteur ;
+ La  [ZEP-13](https://zestedesavoir.com/forums/sujet/976/zep-13-tribune-libre/), qui se propose d'ajouter un troisième type de contenu, les "tribunes" ;
+ Les Les ZEPS [16](https://zestedesavoir.com/forums/sujet/1243/zep-16-page-de-proposition-de-corrections/) et [20](https://zestedesavoir.com/forums/sujet/2042/zep-20-relecture-des-tutos-par-les-pairs/), qui est une initiative pour améliorier le confort de validation via la relecture par des pairs et la propositions de corrections ;
+ la [ZEP-24](https://zestedesavoir.com/forums/sujet/2251/zep-24-refonte-et-enrichissement-des-notifications/), qui permetrai de repenser les notifications de manère plus efficace ;
+ Les ZEPS [15](https://zestedesavoir.com/forums/sujet/1082/zep-15-navigation-a-facettes-a-travers-le-site/), [31](https://zestedesavoir.com/forums/sujet/3149/zep-31-les-parcours-de-connaissances/) et [32](https://zestedesavoir.com/forums/sujet/3152/zep-32-cartographie-des-contenus/), qui tentent de repenser la manière dont on navigue entre les contenus ;
+ Les ZEPs [33](https://zestedesavoir.com/forums/sujet/3992/zep-33-template-de-tutoriels-et-editorialisation/) et [34](https://zestedesavoir.com/forums/sujet/4010/zep-34-template-de-tutoriels/), qui viserait guider les auteurs dans la création de leurs contenus.

Autant de sujets qui n'attendent que votre avis et votre aide.

Enfin, cette ZEP nous a permis de mettre à jour d'autres chantiers très importants pour le site tels que:

- la validation partielle des contenus (on ne propose à la validation qu'une partie d'un tutoriel),
- une forte amélioration de l'éditeur du site,
- une meilleure présentation des pages communautaires (béta, page d'aide)...
