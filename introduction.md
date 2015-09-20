Après une version 15.7 gaston (non gaston n'est pas un agrume c'est juste qu'il est en retard) qui venait stabiliser le site, nous voici reparti vers les cieux de l'ajout de fonctionnalités (et quelles fonctionnalités !).

Nous sommes bien loin de battre le record des tickets GitHub fermés, détennu par la version [cédrat (15.6)](https://zestedesavoir.com/articles/263/nouveautes-de-la-version-156-cedrat/) de Zeste de Savoir avec ses 120 tickets fermés, mais c'est surtout l'aboutissement de 9 mois de travail depuis décembre 2014 jusqu'à août 2015 ! Essentiellement grâce à deux contributeurs actifs, artragis et pierre-24, et aider par deux autres contributeurs, Hugo et Vayel.

Alors qu'est ce qui a demandé autant de temps dans la réalisation d'une fonctionnalité de 9 mois ? En fait, c'est beaucoup plus qu'une fonctionnalité, c'est un module entier qui a été refactorisé, corrigé, puis testé en profondeur, le module rédactionnel de Zeste de Savoir qui touche la gestion entière des articles et des tutoriels de bout en bout. Cela va de la création du contenu à sa publication en passant par sa validation. Tout ce travail a été réalisé dans le cadre d'une ZEP, la ZEP-12 !

[[i]]
|Pour éviter les confusion, nous utiliserons "Ancien module" pour parler des modules "tutoriel" et "article" qui gérait ces deux contenus indépendament l'une de l'autre avant la ZEP-12 et "Nouveau module" pour le nouveau module mit en oeuvre dans le développement de la ZEP-12.

Sans plus attendre, allons à la rencontre de cette nouvelle version !