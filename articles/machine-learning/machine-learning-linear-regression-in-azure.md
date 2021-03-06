<properties 
	pageTitle="Utilisation de la régression linéaire dans Machine Learning | Microsoft Azure" 
	description="Une comparaison des modèles de régression linéaire dans Excel et dans Azure Machine Learning Studio" 
	metaKeywords="" 
	services="machine-learning" 
	documentationCenter="" 
	authors="garyericson" 
	manager="paulettm" 
	editor="cgronlun"  />

<tags 
	ms.service="machine-learning" 
	ms.workload="data-services" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="12/11/2015" 
	ms.author="kbaroni;garye" />

# Utilisation de la régression linéaire dans Azure Machine Learning

> *Kate Baroni* et *Ben Boatman* sont des architectes de solution du Data Insights Center of Excellence de Microsoft. Dans cet article, ils décrivent leur expérience de migration d’une suite d’analyse de régression existante vers une solution de cloud à l’aide d’Azure Machine Learning.

[AZURE.INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## Objectif

Notre projet a commencé avec deux objectifs :  

1. l’utilisation de l’analyse prédictive pour améliorer la précision des projections de recettes mensuelles de notre organisation ;  
2. l’utilisation d’Azure ML pour confirmer, optimiser, mettre à l’échelle nos résultats et en accélérer la vitesse.  

Comme beaucoup d’entreprises, notre organisation connaît un processus de prévision des recettes mensuelles. Notre petite équipe d’analystes commerciaux a été chargée d’utiliser Machine Learning pour prendre en charge le processus et améliorer la précision des prévisions. L’équipe a passé plusieurs mois à collecter des données provenant de plusieurs sources et à exécuter les attributs de données via l’analyse statistique afin d’identifier les principaux attributs des prévisions de vente de services. Puis, ils ont commencé à réaliser des prototypes de modèles de régression statistique sur les données dans Excel. En quelques semaines, nous avions un modèle de régression Excel plus performant que nos anciens processus de prévisions financières et de champ. C’est devenu le résultat de prédiction de référence.


Ensuite, nous avons déplacé l’analyse prédictive vers Azure ML pour savoir comment Azure ML pouvait améliorer les performances de prédiction.


## Atteinte de la parité des performances de prédiction

Notre priorité était d’atteindre la parité entre les modèles de régression Azure ML et Excel. Avec les mêmes données et la même fraction pour l’apprentissage et le test des données, nous voulions obtenir une parité des performances de prédiction entre Excel et Azure ML. Au départ, nous a échoué. Le modèle Excel a surpassé le modèle Azure ML. L’échec était dû à un manque de compréhension de la configuration des outils de base dans Azure ML. Après une discussion avec l’équipe de produit Azure ML, nous avons acquis une meilleure compréhension de la configuration de base requise pour nos jeux de données et atteint la parité entre les deux modèles.

### Création d’un modèle de régression dans Excel
Notre régression Excel utilisait le modèle de régression linéaire standard trouvé dans l’utilitaire d’analyse d’Excel.

Nous avons calculé une *Erreur d’absolue moyenne en pourcentage* et l’avons utilisée comme mesure de performance pour le modèle. L’obtention d’un modèle fonctionnel à l’aide d’Excel nous a pris trois mois. Nous avons utilisé nos connaissances pour l’expérience Azure ML, ce qui a été bénéfique pour en comprendre les exigences.

### Création d’une expérience comparable dans Azure Machine Learning  
Nous avons suivi ces étapes pour créer notre expérience dans Azure ML :

1.	téléchargement du jeu de données dans un fichier csv vers Azure ML (très petit fichier) ;
2.	création d’une expérience et utilisation du module [Project Columns][project-columns] pour sélectionner les mêmes fonctionnalités de données que dans Excel ;   
3.	utilisation du module de [Split][split] (avec le mode *Expression Relative*) pour répartir les données dans les mêmes jeux apprentissage que dans Excel ;  
4.	expériences avec le module de [régression linéaire][linear-regression] (options par défaut uniquement), documentation et comparaison des résultats à ceux de notre modèle de régression Excel.

### Examen des résultats initiaux
Dans un premier temps, le modèle Excel a clairement surpassé le modèle Azure ML :

| |Excel|Azure ML|
|---|:---:|:---:|
|Performances| | |
|<ul style="list-style-type: none;"><li>Carré R ajusté</li></ul>| 0,96 |N/A|
|<ul style="list-style-type: none;"><li>Coefficient de <br />
détermination</li></ul>|N/A|	0,78<br />
(faible précision)|
|Erreur d'absolue moyenne |	9,5 M $|	19,4 M $|
|Erreur d’absolue moyenne (%)|	6,03 %|	12,2 %

Lorsque nous avons présenté notre processus et les résultats obtenus aux chercheurs de données et développeurs de l’équipe Azure ML, ils ont rapidement fourni des conseils utiles.

* Lorsque vous utilisez le module de [régression linéaire][linear-regression] dans Azure ML, deux méthodes sont fournies :
	*  descente dégradée en ligne : plus adapté aux problèmes de plus grande échelle ;
	*  moindres carrés ordinaires : il s’agit de la méthode qui vient à l’esprit de la plupart des personnes qui entendent « régression linéaire ». Pour les petits groupes de données, les moindres carrés ordinaires peuvent être un meilleur choix.
*  Envisagez d’ajuster le paramètre de poids de régularisation L2 pour améliorer les performances. Il est défini à 0,001 par défaut. Pour notre petit ensemble de données, nous l’avons défini à 0,005 pour améliorer les performances.    

### Mystère résolu !
Lorsque nous avons appliqué les recommandations, nous avons obtenu les mêmes performances de référence dans Azure ML et Excel :

|| Excel|Azure ML (Initial)|Azure ML avec moindres carrés|
|---|:---:|:---:|:---:|
|Valeur étiquetée |Chiffres réels (numérique)|identique|identique|
|Apprenant |Excel -> Analyse de données -> Régression|Régression linéaire.|Régression linéaire|
|Options de l’apprenant|S.O.|Valeurs par défaut|moindres carrés ordinaires<br />L2 = 0,005|
|Jeu de données|26 lignes, 3 caractéristiques, 1 étiquette. Entièrement numérique.|identique|identique|
|Fraction : apprentissage|Excel formé sur les 18 premières lignes, testé sur les 8 dernières lignes.|identique|identique|
|Fraction : test|Formule de régression Excel appliquée au 8 dernières lignes|identique|identique|
|**Performance**||||
|Carré R ajusté|0,96|S.O.||
|Coefficient de détermination|S.O.|0,78|0,952049|
|Erreur d’absolue moyenne|9,5 M $|19,4 M $|9,5 M $|
|Erreur d’absolue moyenne (%)|<span style="background-color: 00FF00;"> 6,03 %</span>|12,2 %| <span style="background-color: 00FF00;"> 6,03 %</span>|

En outre, les coefficients Excel ont été efficaces par rapport aux pondérations de fonctionnalités du modèle formé Azure :

||Coefficients Excel|Pondérations de fonctionnalités Azure|
|---|:---:|:---:|
|Interception/décalage|19470209,88|19328500|
|Fonctionnalité A|0,832653063|0,834156|
|Fonctionnalité B|11071967,08|11007300|
|Fonctionnalité C|25383318,09|25140800|

## Étapes suivantes

Nous avons voulu utiliser le service Web Azure ML dans Excel. Nos analystes commerciaux s’appuient sur Excel et nous avions besoin d’une méthode pour appeler le service Web Azure ML avec une ligne de données Excel et qu’il renvoie la valeur prédite vers Excel.

Nous souhaitions également optimiser notre modèle, à l’aide des options et des algorithmes disponibles dans Azure ML.

### Intégration à Excel
Notre solution était de faire fonctionner notre modèle de régression Azure ML en créant un service Web à partir du modèle formé. En quelques minutes, le service Web a été créé et nous avons pu l’appeler directement à partir d’Excel pour retourner une valeur de recettes prédites.

La section *tableau de bord des services Web* comprend un classeur Excel à télécharger. Le classeur est déjà mis en forme avec les informations de schéma et l’API de service Web. Lorsque vous cliquez sur *télécharger un classeur Excel*, il s’ouvre et vous pouvez l’enregistrer sur votre ordinateur local.

![][1]
 
Avec le classeur ouvert, copiez vos paramètres prédéfinis dans la section de paramètres bleue comme illustré ci-dessous. Une fois les paramètres saisis, Excel appelle le service Web AzureML et les étiquettes notées prédites s’affichent dans la section Valeurs prédites verte. Le classeur continue à créer des prédictions pour les paramètres en fonction de votre modèle formé pour tous les éléments de ligne saisis sous Paramètres. Pour plus d’informations sur l’utilisation de cette fonctionnalité, consultez [Utilisation d’un service Web Microsoft Azure Machine Learning à partir de Microsoft Excel](machine-learning-consuming-from-excel.md).

![][2]
 
### Optimisation et autres expériences
Maintenant que nous disposions d’une référence avec notre modèle Excel, nous sommes passés à l’optimisation de notre modèle de régression linéaire Azure ML. Nous avons utilisé le module de [Sélection de fonctionnalités basée sur un filtre][filter-based-feature-selection] afin d’améliorer notre sélection des éléments de données initiaux. Cela nous a permis d’améliorer les performances de 4,6 % pour l’erreur d’absolue moyenne. Pour les projets à venir, nous utiliserons cette fonctionnalité qui pourrait nous éviter des semaines d’itération des attributs de données afin de trouver le jeu de fonctionnalités approprié pour la modélisation.

Ensuite, nous prévoyons d’inclure des algorithmes supplémentaires comme les méthodes [bayésiennes][bayesian-linear-regression] ou [les arbres de décision optimisés][boosted-decision-tree-regression] dans notre expérience afin d’en comparer les performances.

Si vous souhaitez expérimenter la régression, un bon jeu de données d’essai est l’exemple de jeu de données de régression d’efficacité énergétique, qui comporte un grand nombre d’attributs numériques. Le jeu de données est fourni dans le cadre des exemples de jeux de données de ML Studio. Vous pouvez utiliser de nombreux modules d’apprentissage pour prédire la charge de chauffe ou de refroidissement. Le tableau ci-dessous est une comparaison des différents apprentissages de régression à l’aide du jeu de données d’efficacité énergétique, afin de prédire la charge de refroidissement variable cible :

|Modèle|Erreur d'absolue moyenne|Erreur du carré moyen racine|Erreur d’absolue relative|Erreur carrée relative|Coefficient de détermination
|---|---|---|---|---|---
|Arbre de décision optimisé|0,930113|1,4239|0,106647|0,021662|0,978338
|Régression linéaire (descente dégradée)|2,035693|2,98006|0,233414|0,094881|0,905119
|Régression de réseau neuronal|1,548195|2,114617|0,177517|0,047774|0,952226
|Régression linéaire (moindres carrés ordinaires)|1,428273|1,984461|0,163767|0,042074|0,957926  

## Points clés 

Nous avons beaucoup appris en exécutant la régression Excel et les expériences Azure Machine Learning en parallèle. La création du modèle de référence dans Excel et sa comparaison aux modèles utilisant la [régression linéaire][linear-regression] d’Azure ML nous a aidés à découvrir Azure ML. Nous avons découvert des possibilités d’amélioration des performances du modèle et de sélection des données.

Nous avons également découvert qu’il était recommandé d’utiliser la [sélection des caractéristiques basée sur les filtres][filter-based-feature-selection] pour accélérer les projets de prédictions. En appliquant la sélection des caractéristiques à vos données, vous pouvez créer un modèle amélioré dans Azure ML, avec de meilleures performances globales.

La capacité de transférer des analyses prévisionnelles à partir d’Azure ML vers Excel permet une augmentation considérable de la capacité à fournir efficacement des résultats à un vaste public d’utilisateurs professionnels.


## Ressources
Certaines ressources sont répertoriées pour vous aider à utiliser la régression :

* Régression dans Excel. Si vous n’avez jamais essayé la régression dans Excel, ce didacticiel vous aidera beaucoup : [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html)
* Régression et prévisions. Tyler Chessman a écrit un article de blog expliquant comment effectuer des prévisions de série chronologique dans Excel, qui contient une excellente description de la régression linéaire pour les débutants. [http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts)  
* 	Régression linéaire et moindres carrés ordinaires : défauts, problèmes et pièges. Pour une introduction et une discussion relatives à la régression : [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/ ](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[project-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
 

<!------HONumber=AcomDC_1210_2015-->
