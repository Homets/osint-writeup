### 404 CTF


[[LOGO 404CTF

*Né d’une collaboration entre la _Direction Générale de la Sécurité Extérieure_ et _Télécom SudParis_, le 404 CTF met à l’honneur le double anniversaire que cette année 2022 marque : les 80 ans du _BCRA_, le service secret de la France libre et les 40 ans de son héritier, la DGSE.*

*Pendant un mois, confrontez-vous à des challenges conçus par le club de cybersécurité _HackademINT_ de Télécom SudParis. Que vous soyez expert ou débutant, n'hésitez pas à mettre vos compétences à l’épreuve lors de ce CTF individuel !*


##### Challenges

**Equipement désuet (Niveau Intro)**

*Un de nos agents a retrouvé un équipement qui a été utilisé pour communiquer des données sensibles. Mais de quoi s'agit-il ? Il faudrait trouver la date d'arrêt de cet équipement en France, pour savoir quelle piste privilégier pour la suite de l'enquête.*

*Format du flag : 404CTF{jj_mm_aaaa}*

[[IMAGE CHALL 1]]

On reconnait facilement le minitel fait sinon en zoomant on voit bien écrit Telic Alcatel donc en une simple recherche google nous avons le nom de l'appareil, puis pour finir la page [Wikipédia](https://fr.wikipedia.org/wiki/Minitel#Arr%C3%AAt_du_service) pour trouver la date d'arrêt de cet équipement en France.

[[IMAGE WIKIPEDIA MINITEL]]

404CTF{30_06_2012}

**Collaborateur suspect (Niveau Facile)**

*Nous avons eu vent d'une activité étrange qui aurait eu lieu sur la page qui mène à cette interface de mission. Nous soupçonnons une tentative de la part de Hallebarde de nous discréditer, ils nous ont peut-être infiltrés. Des informations confidentielles auraient été brièvement diffusées avant d'être retirées. Pourriez-vous nous dire lesquelles ?*

Vu la description du challenge on pense immédiatement au site de la Wayback Machine.

Commençons par le site https://ctf.404ctf.fr/, dans l'url du site la technique est de rajoutée un asterisk à la find de l'url pour que la wayback nous retourne toutes les pages qui commence par l'url.

[[IMAGE WAYBACK 798 URL]]

Voici 798 url, filtrons tous ça car seulement les MIME Type "text/html" nous intéresse ici, mais en cherchant aucun flag n'est dans le sous-domaine ctf.
Allons maintenant sur le site principal https://www.404ctf.fr/, même démarche avec l'url "https://www.404ctf.fr/*". Nous n'avons que 49 url, ça tient sur une page, il y a 3 text/html donc fouillons un peu dans cela. Et sur la page crédit sur le premier archivage effectué. nous tombons sur 404CTF{R3G4rd3r_3n_arr13r3_p3uT_3tR3_1Nt3r3ss4Nt}.


**À l'aube d'un échange (Niveau Moyen)**

*Nouvelle recrue ! Nous avons besoin de toi par ici. Un de nos agents vient d'intercepter une courte conversation téléphonique entre deux agents de **Hallebarde**. Un important échange de documents confidentiels doit avoir lieu et pour indiquer l'endroit du rendez-vous, l'un des agents ennemis a envoyé la photo ci-dessous à son collègue tout en précisant ceci :*

>Quel beau lever de soleil n'est-ce pas ? J'attendrai dans la rue qui sépare le bâtiment au premier plan de ceux au second plan. Rendez-vous ce soir, 22h00.

*Format du flag : `404CTF{md5 du nom complet de la rue}`  
*Le nom de la rue doit être en **minuscule**, inclure le **type de rue** ( *ex : avenue, rue, boulevard... ), **sans accents**, **sans *abréviation**, **et tous les espaces doivent être remplacés par des *tirets**. Par exemple : si la rue est l'Avenue de Saint-Mandé à Paris, le flag *correct est 404CTF{129af9edde5659143536427f9a5f659a}.

[[IMAGE ]]

[[IMAGE DESSIN]]

Voilà 3 axe qui vont nous intéresser :
- En bleu => 3 tour dont une avec une forme spéciale
- En rose => Un appartement reconnaissable quand on sera déjà plus avancé sur le lieu
- En vert => De la taule qui grâce au combo rose et vert, nous aurons l'endroit à coup sûr.

Déjà nous remarquons que nous somme en "hauteur",  au loin, on remarque bien que la tour de droite avec une forme originale est la tour Part-Dieu, sans connaître lyon une recherche "Tour en forme de crayon" ou un reverse yandex de la tour.

Donc nous avons le lieu, allons sur google earth pour une vue aériennes et satellitaires. Le but sera de s'aligner comme sur la photo.

[[image google aligner]]


Prenons un peu de hauteur =>  

[[ image vue de hauteur]]


Nous voilà à la Montée Saint-Barthélémy, nous manque plus que de faire le md5 de la rue avec les consignes données par la description. Et nous voilà avec le flag.

404CTF{eb66c65861da9fe667f26667b3427d2c}


**Nous sommes infiltrés !**

*Nouvelle recrue, je peux vous parler en privé ? C'est très urgent...

*Nous avons eu vent de nouvelles pratiques de particulièrement insidieuses. Dans le but d'inflitrer la DGSE, Hallebarde recrute de jeunes étudiants en école d'ingénieur. Quel est le lien me direz-vous ? Ils envoient ces étudiants s'inscrire dans les clubs de cybersécurité de ces écoles, et au terme de leur scolarité, ces étudiants sont potentiellement embauchés par nos équipes, sans que l'on se doute de quoi que ce soit !*

*Nous soupçonnons notamment le club de cybersécurité HackademINT de Télécom SudParis de s'être fait infiltrer en cette fin d'année scolaire. Nous avons récupéré une photo de leur local assez récente. Utilisez la pour identifier le ou les nouveaux membres du club et dénicher une preuve de leur appartenance à .*


[[IMAGE NOUS SOMME INFILTRE]]

Première chose à faire, regarder tous les pseudos sur root-me. Aucun compte n'a de chose intéressante à l'exception de Xx_Noel_Janvier_xX, on apprend qu'il est nouveau à TSP et il redirige vers un site web. Allons regarder le site [gorfouland](https://e10pthes.github.io/about/).
Sur un des scripts js sur le developpers tools on y vois ```Il n'y a pas de flag ici, si c'est ce que vous cherchez ! Mais vous êtes sur la bonne piste en``` et aussi un lien vers le compte twitter du créateur du site. Inspectons maintenant le compte twitter. Pas de tweet suspect mais dans la section "Tweets et réponses", un commentaire nous intrigue :
[IMAGE TWITTER TWEET REDIRECT ]

Suspect non ? Regardons de plus près le compte de ce fameux Pablo Sintera, la biographie est plutôt équivoque.

>Apprécie les simulations de combats médiévaux, en particulier les grande lances avec une tête de hache au bout.

Outre le fait qu'il aime les combat médievaux on y voit aussi une référence à la hallebarde.

Maintenant nous savons où est le problème, ne reste plus qu'a trouver comment y accéder. 
La wayback machine ne donne rien, mais quand on regarde bien, le site gorfouland est un site github.io, ce qui nous indique qu'il y'a un compte github associé. [Voila le github](https://github.com/e10Pthes), allons voir les commit de la page about. 

[[IMAGE COMMIT ]]


Nous pouvons voir sur un commit 
```
<form id="citizenship-form" 
action="http://hallebarde.duckdns.org/"
hidden
method="post">
```

En voilà une redirect étrange, sur le site on peut y voir écrit le flag 404CTF{Att3nt10n_AU8_V13ux_C0mMiT5}

**Nom d'une nouvelle recrue! (Niveau Extrême)**

*Il semblerait que Hallebarde tente de recruter de nouveaux membres. Nous avons identifié leur prochaine cible de recrutement, un homme connu sous le nom de Edrabellah Chateaubrion. Nous voudrions que vous trouviez à quel endroit et à quelle date s'est déroulé la première rencontre afin que nous puissions intervenir et empêcher les suivantes.

*Format du flag : 404CTF{ville_jj_mm_aaaa}*

Cherchons un premier point d'accroche. avec un peu de recherche nous voyons un Linkedin, regardons un peu dans la section activité.

 1ère piste => Un commentaire sur un post google, qui annonce qu'il aime utilisé les outils google.
 
 2ème piste => Un CV
 
Pour la première piste pour l'instant nous n'avons pas de mail, allons voir le CV. Mis à part le fait que cet personne est plutôt prétentieuse, un email (laposte et non gmail) et un site internet.

Investiguons maintenant sur le site, l'onglet mariage nous donne un indice, 

>je me suis marié récemment à la merveilleuse Mme Hälbeardt dans le Puy-de-Dôme. Quel bel endroit pour un moment si spécial ! Le feu de mon amour était plus puissant que la lave crachée auparavant par les volcans d’Auvergne.
>
>Étant actuellement en lune de miel, je n’ai pas encore mis à jour tous mes profils pour correspondre à ma nouvelle identité si fièrement acquise.


Recherchons son prénom et le nom de sa femme sur google, un avis sur le zoo de Lille apparaît, même photo de profil, voilà quelque chose de très intéressant.

Après avoir lu tous les avis plein de choses ressort, il s'est marié à clermont ferrand dans la basilique Notre Dame du port, avec un séjour à orcines à côtés le même mois. Mais plus important un avis émit sur l'aéroport CDG.

>Charles de Gaulle est un aéroport toujours trop animé à mon goût, je préférais le Covid ! Il est vraiment difficile de s'y retrouver lorsque plus d'un terminal est ouvert. Hâte de découvrir enfin l'organisation de ma future épouse ! Le vol a eu du retard, mais nous avons pu patienter avec un verre au bar. Pas de pluie, un bon début de mois de mars ! En route vers le soleil et une rencontre qui s'annonce pleine d'énergie !

Peut-être la fameuse organisation, et la fameuse rencontre, mais comment savoir le jour, malgré le fait que ce soit début mars, et la destination ? 

Analysons l'avion => 
[[IMAGE AVION]]

L'Avion à la référence F-GRHL, pourquoi pas allez voir tous les vols de cet avion début mars sur le site https://www.flightera.net/planes/F-GRHL . 
Nous prenons une fourchette du premier au 15 mars, et notons tous les avions en route vers le sud qui sont parti en retard.

Nous avons pas mal d'avion nous reste plus qu'a essayer. Après quelque essais, Challenge réussi avec le flag 404CTF{malaga_08_03_2022}
