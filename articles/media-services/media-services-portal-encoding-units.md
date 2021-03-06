<properties
	pageTitle="Comment mettre à l’échelle le traitement multimédia à l’aide du portail Azure Classic"
	description="Apprenez à mettre à l’échelle Media Services en spécifiant le nombre d’unités réservées de diffusion en continu à la demande et d’unités réservées d’encodage que vous voulez attribuer à votre compte."
	services="media-services"
	documentationCenter=""
	authors="juliako,milangada"
	manager="dwrede"
	editor=""/>

<tags
	ms.service="media-services"
	ms.workload="media"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="01/29/2016"
	ms.author="juliako"/>


# Comment mettre à l’échelle le traitement multimédia à l’aide du portail Azure Classic

> [AZURE.SELECTOR]
- [.NET](media-services-dotnet-encoding-units.md)
- [Portal](media-services-portal-encoding-units.md)
- [REST](https://msdn.microsoft.com/library/azure/dn859236.aspx)
- [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
- [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)

## Vue d'ensemble

Un compte Media Services est associé à un Type d'unité réservé qui détermine la vitesse à laquelle vos tâches de traitement multimédia sont traitées. Vous pouvez choisir entre les types d’unités réservées suivantes : **S1**, **S2** ou **S3**. Par exemple, un même travail d’encodage s’exécute plus rapidement quand vous utilisez le type d’unité réservée **S2** que le type **S1**. Pour plus d’informations, consultez [Types d’unités réservées d’encodage](https://azure.microsoft.com/blog/author/milanga/).

En plus de spécifier le type d’unité réservée, vous pouvez spécifier d’approvisionner votre compte avec des unités réservées d’encodage. Le nombre d’unités réservées d’encodage approvisionnées détermine le nombre de tâches de média qui peuvent être traitées simultanément dans un compte donné. Si, par exemple, votre compte a 5 unités réservées, les 5 tâches de média sont exécutées simultanément tant qu’il y a des tâches à traiter. Les autres tâches restent dans la file d'attente et sont sélectionnées séquentiellement pour le traitement dès que l'exécution d'une tâche se termine. Si aucune unité réservée n'est approvisionnée pour un compte donné, les tâches sont sélectionnées séquentiellement. Dans ce cas, le temps d’attente entre la fin d’une tâche et le début de la suivante dépend de la disponibilité des ressources du système.

>[AZURE.IMPORTANT] Les unités réservées fonctionnent pour la mise en parallèle de tout le traitement multimédia, notamment les travaux à l'aide de l'Indexeur multimédia Azure. Toutefois, contrairement à l'encodage, l'indexation des travaux ne sera pas plus rapide avec des unités réservées plus rapides.

Pour modifier le type d’unité réservée et le nombre d’unités réservées d’encodage, procédez comme suit :

1. Dans le [portail Azure Classic](https://manage.windowsazure.com/), cliquez sur **Media Services**. Cliquez ensuite sur le nom du service multimédia.

2. Sélectionnez la page **ENCODAGE**.

	Pour modifier le **TYPE D’UNITÉ RÉSERVÉE**, appuyez sur S1, S2 ou S3.

	Pour modifier le nombre d’unités réservées pour le type d’unité réservée sélectionné, utilisez le curseur **ENCODAGE**.


	![Processors page](./media/media-services-portal-encoding-units/media-services-encoding-scale.png)


	>[AZURE.NOTE] Les centres de données suivants ne proposent pas le type d’unité réservée Premium : Singapour, Hong Kong, Osaka, Beijing, Shanghai.

3. Appuyez sur le bouton ENREGISTRER pour enregistrer vos modifications.

	Les nouvelles unités réservées d’encodage sont allouées dès que vous cliquez sur ENREGISTRER.

	>[AZURE.NOTE] C’est le plus grand nombre d’unités spécifiées sur 24 heures qui est utilisé pour calculer le coût.

##Quotas et limitations

Pour plus d’informations sur les quotas et les limitations et pour savoir comment ouvrir un ticket de support, consultez la rubrique [Quotas et limitations](media-services-quotas-and-limitations.md).



##Parcours d’apprentissage de Media Services

[AZURE.INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

##Fournir des commentaires

[AZURE.INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!---HONumber=AcomDC_0204_2016-->