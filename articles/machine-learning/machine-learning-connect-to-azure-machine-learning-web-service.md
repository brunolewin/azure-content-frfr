<properties
	pageTitle="Connexion à un service web Microsoft Azure Machine Learning | Microsoft Azure"
	description="Via C# ou Python, vous pouvez vous connecter à un service web Microsoft Azure Machine Learning, au moyen d’une clé d’autorisation."
	services="machine-learning"
	documentationCenter=""
	authors="garyericson"
	manager="paulettm"
	editor="cgronlun" />

<tags
	ms.service="machine-learning"
	ms.workload="data-services"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="02/03/2016" 
	ms.author="garye" />


# Se connecter à un service web Microsoft Azure Machine Learning | Azure
L’expérience de développeur de Microsoft Azure Machine Learning correspond à une API de service web destinée à effectuer des prévisions à partir des données d’entrée, en temps réel ou en mode de lot. Vous utilisez Microsoft Azure Machine Learning Studio pour créer des prédictions et déployer un service web Microsoft Azure Machine Learning.

[AZURE.INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Pour savoir comment créer et déployer un service web Machine Learning à l’aide de Machine Learning Studio, consultez les pages suivantes :

- [Déploiement d’un service web Microsoft Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
- [Prise en main de Machine Learning Studio](https://azure.microsoft.com/documentation/videos/getting-started-with-ml-studio/)
- [Vue d’ensemble de Microsoft Azure Machine Learning](https://studio.azureml.net/)
- [Centre de documentation Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)

## Service web Microsoft Azure Machine Learning ##

Grâce au service web Microsoft Azure Machine Learning, une application externe peut communiquer avec le modèle de notation de workflow Machine Learning et ce, en temps réel. Un appel du service web Machine Learning renvoie les résultats d’une prédiction à une application externe. Pour créer cet appel, vous transmettez une clé d’API créée quand vous déployez une prédiction. Le service web Machine Learning est basé sur l’architecture REST, souvent choisie pour les projets de programmation web.

Microsoft Azure Machine Learning propose deux types de service :

- Service de requête-réponse (Request-Response Service, RRS) : service hautement évolutif, à faible latence, qui constitue une interface pour les modèles sans état créés et déployés à partir de Machine Learning Studio.
- Service d’exécution de lot (Batch Execution Service, BES) : service asynchrone qui effectue la notation d’un lot pour les enregistrements de données.

Pour plus d’informations sur les services web Machine Learning, consultez la page [Déploiement d’un service web Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## Obtenir une clé d’autorisation Microsoft Azure Machine Learning ##
Vous pouvez obtenir une clé d’API de service web auprès d’un service web Machine Learning. Vous pouvez l’obtenir via Machine Learning Studio ou le portail Azure.
### Machine Learning Studio ###
1. Dans Machine Learning Studio, cliquez sur l’option **SERVICES WEB** figurant sur la gauche.
2. Cliquez sur un service web. La « clé API » figure sur l’onglet **TABLEAU DE BORD**.

### Portail Azure ###

1. Cliquez sur l’option **MACHINE LEARNING** figurant sur la gauche.
2. Cliquez sur un espace de travail.
3. Cliquez sur **SERVICES WEB**.
4. Cliquez sur un service web.
5. Cliquez sur un point de terminaison. La « CLÉ API » se trouve sur la partie inférieure droite de la fenêtre.

## <a id="connect"></a>Se connecter à un service web Machine Learning

Vous pouvez vous connecter à un service web Machine Learning à l’aide de n’importe quel langage de programmation qui prend en charge les requêtes et réponses HTTP. Vous pouvez consulter des exemples en C#, Python et R sur l’une des pages d’aide relatives aux services web Machine Learning.

### Pour afficher une page d’aide sur l’API du service web Machine Learning ###
Vous créez ce type de page quand vous déployez un service web. Consultez la page [Procédure pas à pas : déploiement du service web Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).


**Pour afficher une page d’aide sur l’API Machine Learning** dans Machine Learning Studio :

1. Sélectionnez **SERVICES WEB**.
2. Choisissez un service web.
3. Sélectionnez **Page d’aide sur l’API** - **REQUÊTE-RÉPONSE** ou **EXÉCUTION DE LOT**.


**Page d’aide sur l’API Machine Learning** La page d’aide sur l’API Machine Learning contient des détails sur un service web de prédiction.



### Exemple de code C# ###

Pour vous connecter à un service web Machine Learning, utilisez un élément **HttpClient** qui transmet l’élément ScoreData. ScoreData contient un FeatureVector, un vecteur à n dimensions des fonctionnalités numériques qui représente le ScoreData. Vous vous authentifiez auprès du service Machine Learning au moyen d’une clé API.

Pour vous connecter à un service web Machine Learning, le package NuGet **Microsoft.AspNet.WebApi.Client** doit être installé.

**Installer le package NuGet Microsoft.AspNet.WebApi.Client dans Microsoft Visual Studio**

1. Publiez le service web « Téléchargement d’un jeu de données depuis l’UCI : jeu de données de classe Adult 2 ».
2. Cliquez sur **Outils** > **Gestionnaire de package NuGet** > **Console du gestionnaire de package.**.
2. Choisissez l'élément **Install-Package Microsoft.AspNet.WebApi.Client**.

**Pour exécuter l’exemple de code**

1. Publiez l’expérience « Exemple 1 : Téléchargement d’un jeu de données depuis l’UCI : jeu de données de classe Adult 2 », inclus dans la collection d’exemples Machine Learning.
2. Attribuez l’élément apiKey avec la clé à partir d’un service web. Consultez **Obtenir une clé d’autorisation Microsoft Azure Machine Learning** plus haut.
3. Affectez l’élément serviceUri avec l’URI de requête.


### Exemple de code Python ###

Pour vous connecter à un service web Machine Learning, utilisez la bibliothèque **urllib2** qui transmet l’élément ScoreData. ScoreData contient un FeatureVector, un vecteur à n dimensions des fonctionnalités numériques qui représente le ScoreData. Vous vous authentifiez auprès du service Machine Learning au moyen d’une clé API.


**Pour exécuter l’exemple de code**

1. Publiez l’expérience « Exemple 1 : Téléchargement d’un jeu de données depuis l’UCI : jeu de données de classe Adult 2 », inclus dans la collection d’exemples Machine Learning.
2. Attribuez l’élément apiKey avec la clé à partir d’un service web. Consultez **Obtenir une clé d’autorisation Microsoft Azure Machine Learning** plus haut.
3. Affectez l’élément serviceUri avec l’URI de requête. Consultez la section Obtention d’un URI de requête.

<!---HONumber=AcomDC_0204_2016-->