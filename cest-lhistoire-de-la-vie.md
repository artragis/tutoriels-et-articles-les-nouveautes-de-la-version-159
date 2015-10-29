Sur notre petit îlot de partage libre de connaissances existent deux types 
de contenus : les articles et les tutoriels, et chacun avait son module 
spécifique. Seulement, lorsqu'un problème surgissait, il n'était pas rare 
qu'il ne soit corrigé que pour un seul des deux modules et que l'autre ne 
reçoive l'aide des développeurs que plus tard. À cette honteuse injustice 
s'ajoutait un écart flagrant au niveau des fonctionnalités disponibles : la 
[ZEP-03](/contenus/aides/?type=tuto) se restreignait aux tutoriels, ces 
derniers se voyaient dédier des galeries, pouvaient être placés en bêta pour 
recevoir les commentaires d'autres membres... Bref, les auteurs d'articles 
se mirent à bougonner, de manière assez compréhensible toutefois.

Épris d'égalité et à l'âme pacifiste, deux courageux (ou fous, selon les points 
de vue) développeurs, [artragis](https://zestedesavoir.com/membres/voir/artragis/) et 
[pierre_24](https://zestedesavoir.com/membres/voir/pierre_24/), se mirent alors en tête de 
remédier au conflit : ainsi naquit la 
[ZEP-12](https://zestedesavoir.com/forums/sujet/846/zep-12-refonte-du-principe-des-tutoriels-et-articles/), 
le 24 juillet 2014. 

Pour ceux qui vivraient dans une grotte, une ZEP est un texte écrit par un 
membre de la communauté (n'oublions pas que c'est uniquement cette dernière 
qui fait vivre le site) et dont l'objectif est de spécifier « une amélioration 
de Zeste De Savoir voulue par la communauté », comme l'explique la 
[ZEP-01](https://zestedesavoir.com/forums/sujet/617/zep-01-role-et-fonctionnement-des-zep/).
Pour le moment, quatre ZEPs ont déjà été complètement implémentées : la 
[ZEP-03](https://zestedesavoir.com/forums/sujet/666/zep-03-page-resumant-les-tutos-en-redaction/), 
introduisant une [page d'aide aux auteurs](/contenus/aides/), les 
[ZEP-17](https://zestedesavoir.com/forums/sujet/1365/zep-17-elaboration-de-lapi-des-membres/) 
et [23](https://zestedesavoir.com/forums/sujet/2211/zep-23-elaboration-de-lapi-des-mps/), 
spécifiant respectivement l'API des membres et des MPs, et la 
[ZEP-04](https://zestedesavoir.com/forums/sujet/669/zep-04-nouvelle-page-daccueil/), 
décrivant la page d’accueil. Mais 
[bien d'autres](https://zestedesavoir.com/forums/sujets/tag/51/zep/) sont en
cours et n'attendent que votre aide.

*[ZEP]: ZdS Enhancement Proposal

Revenons-en à la ZEP-12. Suite à son ouverture, de nombreuses discussions ont 
eu lieu, parfois orageuses, lesquelles ont débouché sur un compromis au niveau 
de la spécification. Le développement de la ZEP-12 a alors débuté, en janvier 
2015, puis s'est déroulé durant tout le printemps au gré des disponibilités de 
chacun. Hugo est venu donner un coup de main fort appréciable durant cette 
période, et sans lui, la ZEP-12 aurait probablement pris encore plus de 
retard. Le code a pu être testé plusieurs fois, grâce à l'aide inestimable de 
Vayel et d'Eskimon.

![](http://img.maxisciences.com/greffe-d-organe/des-chirurgiens-britanniques-ont-greffe-un-coeur-qui-s-etait-arrete-a-un-patient-age-de-60-ans_69416_w460.jpg)
Figure: Votre mission, si vous l'acceptez : changer le cœur du site (l'interprétation de qui est artragis, pierre_24, Vayel et Hugo est laissée libre).

Début juillet, la ZEP-12 est entrée dans une phase de correction de bugs. 
Imaginez un peu : l'ampleur de la modification dépassait tout ce que Zeste de 
Savoir avait pu connaitre jusqu'ici, et le serveur de bêta a dû être mis à 
contribution pendant plus d'un mois pour s'assurer, grâce au courageux 
Sandhose, que tout allait bien se passer lors de la mise en production, et ce,  
chers agrumes, afin que vous ne perdiez pas vos repères, mais aussi pour que 
l'expérience du site soit vraiment améliorée. Et c'était plus que nécessaire, 
puisque plusieurs dizaines de bugs ont pu être détectés, entre autres par 
Firm1 et Andr0, et corrigés dans la foulée. Cette phase était plus que 
critique et nécessaire. Par exemple, au début, la migration avait échoué sur 
la plupart des articles, rendant la bêta completement innaccessible.

Et finalement, au terme de 1000 *commits*[^et_de_1000] comptabilisant plus de 
15 000 lignes de code modifiées[^lignes], la ZEP-12 a été intégrée au code de 
Zeste de Savoir 
[le 17 septembre 2015](https://github.com/zestedesavoir/zds-site/pull/2956#issuecomment-140724560) !

[^et_de_1000]: Oui, 1000 *commits*, pas un de plus, pas un de moins. Petit 
rappel : un *commit* est une modification atomique du code.

[^lignes]: Pour être précis : 14 135 lignes ajoutées et 1236 supprimées par 
[la *pull request* initiale](https://github.com/zestedesavoir/zds-site/pull/2956). 
Pour le moment, les anciens modules sont toujours disponibles, ce qui explique le 
faible nombre de lignes supprimées, [mais il est bien entendu prévu de les 
enlever à terme](https://github.com/zestedesavoir/zds-site/pull/3119).

Et même avec ça, plus de 50 *bugfixes* on dû être réalisés, poussant le nombre de *release* candidates[^RC] à 5 
(quand on vous dit que la bêta, ça sert à quelque chose) !
Autant dire que cela a demandé énormément d'investissement de la part de l'équipe de *dev*.

[^RC]: Une *release* candidate, est, d'[après Wikipédia](https://fr.wikipedia.org/wiki/Version_d%27un_logiciel#Version_admissible_ou_pre-release_ou_Release_Candidate), « une version du logiciel qui correspond, du côté pratique, à la version "finale" [...] du dit logiciel. Elle est mise à disposition à des fins de « tests de dernière minute » visant à déceler les toutes dernières erreurs [...]. ».

![ZEP-12 (image réalisée par Blackline)](https://zestedesavoir.com/media/galleries/877/6943c548-1a50-45e4-85de-e3967a0e4444.png.960x960_q85.png)

Avec cette implémentation de la ZEP-12, toute nouvelle fonctionnalité et tout 
bug seront corrigés immédiatement au niveau des tutoriels *et* des articles, 
puisqu'ils appartiennent désormais au même module. Mais ce n'est pas tout : 
plein de fonctionnalités à croquer ont fait leur apparition. On y jette un 
coup d'oeil ?
