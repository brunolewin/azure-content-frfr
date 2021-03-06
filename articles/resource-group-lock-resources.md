<properties 
	pageTitle="Verrouillage de ressources avec Resource Manager | Microsoft Azure" 
	description="Empêchez les utilisateurs de mettre à jour ou de supprimer certaines ressources en appliquant une restriction à tous les utilisateurs et rôles." 
	services="azure-resource-manager" 
	documentationCenter="" 
	authors="tfitzmac" 
	manager="wpickett" 
	editor=""/>

<tags 
	ms.service="azure-resource-manager" 
	ms.workload="multiple" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="01/21/2016" 
	ms.author="tomfitz"/>

# Verrouiller des ressources avec Azure Resource Manager

En tant qu’administrateur, vous pouvez envisager de verrouiller un abonnement, une ressource ou un groupe de ressources afin d’empêcher d’autres utilisateurs de votre organisation de supprimer de manière accidentelle une ressource critique.

Azure Resource Manager prend en charge la restriction des opérations sur les ressources, par le biais de verrous de gestion des ressources. Les verrous sont des stratégies qui appliquent un niveau de verrou sur une étendue particulière. Le verrou peut être appliqué à un abonnement, un groupe de ressources ou à une ressource. Le niveau de verrouillage identifie le type d’application de la stratégie, qui à l’heure actuelle, peut être défini sur **CanNotDelete**. **CanNotDelete** signifie que les utilisateurs autorisés peuvent toujours lire et modifier des ressources, mais ils peuvent supprimer aucune des ressources limitées.

Les verrous diffèrent de l'utilisation du contrôle d'accès basé sur les rôles pour autoriser les utilisateurs à effectuer certaines actions. Pour en savoir plus sur la définition des autorisations pour les utilisateurs et les rôles, consultez [Contrôle d’accès basé sur un rôle Azure](./active-directory/role-based-access-control-configure.md). Contrairement au contrôle d'accès basé sur les rôles, vous utilisez des verrous de gestion pour appliquer une restriction à tous les utilisateurs et rôles, et vous appliquez généralement les verrous pour une durée limitée uniquement.

Lorsque vous appliquez un verrou à une étendue parente, toutes les ressources enfants héritent du même verrou.

## Scénarios courants

Il n’est pas rare de disposer d’un groupe de ressources avec certaines ressources utilisées selon un modèle alterné d’activation/de désactivation. Les ressources de machines virtuelles sont régulièrement activées pour traiter les données pendant un intervalle considéré, puis désactivées une fois cet intervalle terminé. Dans ce scénario, vous pouvez envisager d’activer l’arrêt des machines virtuelles, mais le compte de stockage ne doit aucunement être supprimé. Dans ce scénario, vous utiliserez un verrou de ressource avec le niveau de verrouillage **CanNotDelete** sur le compte de stockage.

## Personnes autorisées à créer ou supprimer des verrous dans votre organisation

Pour créer ou supprimer des verrous de gestion, vous devez avoir accès aux actions **Microsoft.Authorization/*** ou **Microsoft.Authorization/locks/***. Parmi les rôles prédéfinis, seuls les rôles **Propriétaire** et **Administrateur de l’accès utilisateur** peuvent effectuer ces actions. Pour plus d’informations sur l’affectation du contrôle d’accès, consultez [Contrôle d’accès en fonction du rôle Azure](./active-directory/role-based-access-control-configure.md).

## Création d’un verrou dans un modèle

L’exemple ci-dessous représente un modèle créant un verrou sur un compte de stockage. Le compte de stockage sur lequel appliquer le verrou est fourni en tant que paramètre, utilisé conjointement avec la fonction concat(). Le résultat est que « Microsoft.Authorization » est ajouté au nom de la ressource, suivi du nom du verrou, en l’occurrence **myLock**.

Le type fourni est spécifique au type de ressource. Pour le stockage, ce type est « Microsoft.Storage/storageaccounts/providers/locks ».

Le niveau d’étendue est défini à l’aide de la propriété **level** de la ressource. Ici, comme l’exemple concerne la façon d’éviter les suppressions accidentelles, le niveau est défini sur **CannotDelete**.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "lockedResource": {
                "type": "string"
            }
        },
        "resources": [
            {
                "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
                "type": "Microsoft.Storage/storageAccounts/providers/locks",
                "apiVersion": "2015-01-01",
                "properties": {
	                "level": "CannotDelete"
                }
            }
        ]
    }

## Création d’un verrou avec l’API REST

Vous pouvez verrouiller des ressources déployées à l’aide de l’[API REST pour les verrous de gestion](https://msdn.microsoft.com/library/azure/mt204563.aspx). L’API REST vous permet de créer et de supprimer des verrous, et de récupérer des informations relatives aux verrous existants.

Pour créer un verrou, exécutez :

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

Le verrou peut être appliqué à un abonnement, un groupe de ressources ou à une ressource. Le nom du verrou est personnalisable. Pour la version de l’API, utilisez **2015-01-01**.

Dans la demande, incluez un objet JSON spécifiant les propriétés du verrou.

    {
        "properties": {
            "level": {lock-level},
            "notes": "Optional text notes."
        }
    } 

Pour le niveau de verrouillage, spécifiez **CanNotDelete**.

Pour obtenir des exemples, consultez [API REST pour les verrous de gestion](https://msdn.microsoft.com/library/azure/mt204563.aspx).

## Création d’un verrou à l’aide d’Azure PowerShell

[AZURE.INCLUDE [powershell-preview-inline-include](../includes/powershell-preview-inline-include.md)]

Vous pouvez verrouiller des ressources déployées avec Azure PowerShell en utilisant **New-AzureRmResourceLock**, comme indiqué ci-dessous. Avec PowerShell, vous pouvez uniquement définir **LockLevel** sur **CanNotDelete**.

    PS C:\> New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite -ResourceName examplesite -ResourceType Microsoft.Web/sites

Azure PowerShell fournit d'autres commandes d'utilisation des verrous, comme **Set-AzureRmResourceLock** pour mettre à jour un verrou et **Remove-AzureRmResourceLock** pour supprimer un verrou.

## Étapes suivantes

- Pour plus d’informations sur l’utilisation de verrous sur des ressources, consultez [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
- Pour en savoir plus sur l’organisation logique de vos ressources, consultez [Organisation des ressources à l’aide de balises](resource-group-using-tags.md)
- Pour changer le groupe de ressources où se trouve une ressource, consultez [Déplacer des ressources vers un nouveau groupe de ressources](resource-group-move-resources.md)
- Vous pouvez appliquer des restrictions et des conventions sur votre abonnement avec des stratégies personnalisées. Pour plus d'informations, consultez [Utiliser le service Policy pour gérer les ressources et contrôler l'accès](resource-manager-policy.md).

<!---HONumber=AcomDC_0128_2016-->