# RiskAnalisis
On cherche à analyser le risque des demandeurs de prêts, en faire des statistiques et construire un modèle de règles de décisions afin d'automatiser le processus d'allocation ou non d'un prêt.
-------------------------------------------------------------
Les données qui ont servi de données de test et de validations sont sur : https://www.kaggle.com/datasets/gauravduttakiit/loan-defaulter
-----------------------------------------
Etat de l'art Business

Les prêts sont au cœur du business des banques, en effet, leur revenu principal provient des intérêts de ceux-ci (+ de 30%). Les prêts sont accordés aux demandeurs de prêts, à condition qu’après analyse, validation et vérification de leur profil ils correspondent aux critères qui s’appliquent à l’accord d’un prêt. Cependant, bien que le demandeur corresponde aux critère, cela n’assure pas qu’il sera en mesure de le rembourser sans difficultés.

C’est dans l’objectif de palier à ces éventualités que certains pays ont adopté un système de notation des citoyens. Par exemple en Amérique du Nord, l’adoption du crédit score associe une note globale financière à un numéro de sécurité sociale. Ce crédit score repose sur une synthèse de l’inspection complète des finances d’un individu, cela représente son sérieux et sa capacité à emprunter. Ce système prends en compte 3 grandes catégories de métriques qui sont le temps (est-ce que ce citoyen « participe » depuis longtemps à l’économie ?), les incidents (est-ce que ce citoyen a du mal à rembourser ?) et les montants ( la personne est-elle capable de faire face à un prêt important (immo) ?). Ainsi un bon crédit score est attribué à une personne active dans la participation à l’économie depuis un certain temps et de manière sérieuse.

Cependant, les lois qui s’appliquent à la sécurité et la confidentialité des informations bancaires ne sont pas les mêmes partout dans le monde. En effet, en France les banques et banquiers sont soumis au secret bancaire, obligation à laquelle tout banquier est tenu et qui consiste à ne pas divulguer à un tiers les informations personnelles et bancaires qu’il détient sur ses clients. Ce secret professionnel doit être respecté que ce soit à l’égard :
-du montant des revenus du client ;
-du montant des avoirs détenus en banque par un client ;
-du niveau de recettes du client ;
-des opérations bancaires ou patrimoniales réalisées par un client ;
-de la situation du compte d’un client et des mouvements qui y sont réalisés.

Ces restrictions de divulgation expliquent pourquoi il est impossible en France d’adopter le crédit score à l’Américaine. Il existe en France un modèle de scoring financier, cepandant celui-ci est en grande partie déclaratif, son crédit est donc moindre par rapport au système américain.

Le modèle de scoring et de solvabilité français est responsable de la création d’un marché de courtier bancaire florescent. En effet, ceux-ci ont le rôle d’intermédiaires entre les clients et les banques et assurent de pouvoir les aider à négocier les meilleurs taux pour leurs prêts. Ils ont également pour fonction d’aider les dits “mauvais payeurs” à trouver une banque pour leur accorder le crédit. En contrepartie, il récupèrent un certain pourcentage du crédit, qu’ils ont prédéfini avec la banque partenaire. Le courtier bancaire n°1 en France meilleurtaux a depuis 2014, une évolution de chiffre d’affaire de plus de 20% par an et annonce même l’avoir doublé entre 2016 et 2019 (200 M €).

Le marché du courtage en France évolue et progresse énormément depuis sa création. Le secteur du courtage en assurance est aussi vaste que diversifié. On compte près de 37 340 courtiers en assurance en France. 15 % des employés sont issus du secteur de l’assurance. En détail, ce sont 6 939 courtiers et agents généraux (hors Mandataires d’Intermédiaire d’Assurances — MIA), 3 752 courtiers et Conseillers en Investissement Financier (CIF) et 2 070 courtiers et Intermédiaires en Opérations de Banque et en Services de Paiement (IOBSP). À cela s’ajoutent 1042 courtiers et Mandataires d’Intermédiaire d’Assurances (MIA) ainsi que 330 courtiers et agents généraux et Mandataires d’Intermédiaire d’Assurances (MIA). 9 948 d’entre eux sont des courtiers d’assurances qui exercent l’activité à titre exclusif.

Le courtage bancaire représente 65% du marché du courtage, le courtage immobilier représentant le reste. Le regroupement de crédits représente un volume de 17 milliards d’euros par an, partagé par les acteurs du marché qui sont en majorité les banques, puis en second plan les courtiers. Selon le classement des courtiers millionnaires de l’Argus de l’Assurance en 2019, les 50 plus grands cabinets de courtage en assurance généraliste français ont généré un chiffre d’affaires global de près de 3,395 milliards d’euros. On peut ainsi dire que le secteur du courtage d’assurances connaît une bonne croissance. Pour ce qui est des cabinets de courtage de proximité, les chiffres restent positifs et la tendance à la hausse. Ils enregistrent pour la plupart un chiffre d’affaires annuel moyen de 149 000 € qui peut aller jusqu’à 200 000 €.

Sources :

Explication relative au Taux d’usure : https://www.banque-france.fr/statistiques/taux-et-cours/taux-dusure
Statistiques en rapport avec les credits de consommation en France : https://www.banque-france.fr/statistiques/credit/credit/credits-la-consommation
Statistiques en rapport avec les credits aux particuliers en France : https://www.banque-france.fr/statistiques/credit/credit/credits-aux-particuliers
Enquête mensuelle auprès des banques sur la distribution du crédit en France Déc 2018 : https://www.banque-france.fr/statistiques/credit/credit/enquete-mensuelle-aupres-des-banques-sur-la-distribution-du-credit-en-france
Chiffres concernant meilleurtaux : https://www.meilleurtaux.com/espace-presse/communiques-de-presse/silver-lake-devient-l-actionnaire-majoritaire-du-groupe-meilleurtaux.html#:~:text=Le%20chiffre%20d’affaires%20consolid%C3%A9,assurances%2C%20%C3%A9pargnes%20et%20autres%20services.
---------------------------------------------------------------------------------
Etat de l'art technique : 

Notre sujet d'étude est le risque lors de l'accord d'un prêt.
Des banques ou des particuliers peuvent prêter de l'argent, à défaut ou les crédits sont réservés pour les banques.
On dispose de plusieurs datasets, et on cherche à distinguer un profile type de bon ou de mauvais client. Le bon client sera celui qui rembourse le prêt et paie les intérêts. Pour cela, l'entité qui prête veut s'assurer de la capacité de l'individu à rembourser.

Tout d’abord, nous n’avons pas trouvé de système quasi automatisé open source qui segmente les clients dans ce cadre d'étude.

Explorons des alternatives, toujours open source (ou du moins, en partie).

On pense pouvoir répondre à cette question en passant par les statistiques descriptives, inférentielles et par du machine learning.

Plusieurs études sur le sujet on été faites, voyons lesquelles. D'après la corportate finance institute.

Tout d'abord, les analystes crédits dans les banques évaluent les risques en se basant sur les "5cs of credit", qui sont les suivants : (link :ref2)

- la capacité de repayer le crédit : l’historique de ses jobs, sa situation familiale, la rentabilité de son business..
- le capital : ses investissements, ses réserves, ses objets de valeur etc.
- caractère : le plus simple à mesurer, qui est mesuré par sa propension à payer, les délais entre chaque versements.
- les conditions : elles sont propres au prêt : le taux d'intérêt, son montant..- le collatéral : ce qui pourrait être saisi si le prêt n'est pas remboursé.

Aux Etats-Unis, il existe un indicateur, appelé "Fico score". (link:ref1)

Il est relativement très populaire et est très utilisé, attardons-nous dessus.
Un score FICO est un nombre à trois chiffres, généralement compris entre 300 et 850, qui indique aux prêteurs la probabilité qu'un consommateur rembourse l'argent emprunté en fonction de ses antécédents de crédit.
La société applique une formule propriétaire aux données de rapports de crédit pour produire un score.

Souvent, les trois agences d'évaluation du crédit qui créent les rapports de crédit - Equifax, Experian et TransUnion - ont des données légèrement différentes les unes des autres. Les créanciers utilisent souvent les scores FICO pour décider d'approuver ou non une demande de prêt ou de carte de crédit. Il leur donne une idée de la façon dont le crédit a été géré dans le passé. Ils vérifient également d'autres informations, comme les revenus et les dettes existantes, pour voir si le bénéficiaire a les moyens de rembourser.

Un score qui se situe dans la fourchette bonne ou excellente peut donner plus de choix et l'accès à des taux d'intérêt plus bas.
Le score de crédit peut également être utilisé par les compagnies de services publics et/ou les propriétaires pour déterminer une caution ou si vous un individu sera accepté comme bénéficiaire.

Le soucis avec le FICO score est qu'il ignore beaucoup de caractéristiques : le lieu d'habitation, la situation civile (qui est d'après certaines études très importante), le salaire… 

En plus de ça, on n’a pas le modèle exact utilisé, ce qui rend les comparaisons avec d’autres services extrêmement délicat.

Sur kaggle par exemple, on trouve plusieurs utilisateurs qui cherchent à établir des profils types, mais n'utilisent pas tous les mêmes technologies.
Leurs notebooks sont souvent réalises en Python ou en R grâce à leur bibliothèques de statistiques et de ML très diversifiées, mais certains s'axent plus sur la statistique descriptive, et d'autres plus sur de la classification par exemple (voir la partie références).


Dans notre cas, on aimerait un système d’aide à la décision plus complet.

On va naturellement se tourner vers des projets contenant du ML pour avoir des règles de décisions bien établies.

Les algos les plus utilisés pour les datasets trouvables sur Internet sont les suivants :
- random forest : techniquement plusieurs arbres de décisions, la précision du modèle y est renforcée. Une certaine compagnie financière utilise beaucoup cette solution, elle est nommée PeerLoanKart.
- light gradient descend: toujours basé sur des arbres de décisions, il est cependant plus efficace que certains algos de boosting, car il comporte 3 features principales (GOSS, EFB, histogram based splitting) ce qui le rend
- catboost classifier : Yandex indique via des benchmarks que les performances de cet algo sont meilleures que l'ancien leader, XGboost.

On ne voit cependant pas de DBscan pour repérer les outliers, ce qui pourrait être utile pour voir si des erreurs humaines ont été faites lors de l'attribution ou non d'un prêt.
Autoviz semble être une bonne proposition pour la visualisation, puisqu'elle permet de simplement utiliser des models de ML et représenter sous forme de graphiques interactifs les résultats des prédictions ou des classifications.

Il existe des solutions techniques plus évoluées, naturellement tournées vers l'analyse de risque (credit risk) et risque opérationnel. Prenons l'exemple d'algorithmes quantiques qui ont un avantage de temps d'exécution quadratique par rapport à des méthodes plus classiques. Ces méthodes ont l'avantage de pouvoir prendre en compte d'autres paramètres que la situation financière d'un client, tant que la structure générale du modèle utilisé est un arbre.
