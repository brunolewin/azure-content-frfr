<properties
	pageTitle="Créer un IoT Hub à l’aide d’un modèle ARM et PowerShell | Microsoft Azure"
	description="Suivez ce didacticiel afin d’utiliser des modèles Resource Manager pour créer un IoT Hub à l'aide de PowerShell."
	services="iot-hub"
	documentationCenter=".net"
	authors="dominicbetts"
	manager="timlt"
	editor=""/>

<tags
     ms.service="iot-hub"
     ms.devlang="multiple"
     ms.topic="article"
     ms.tgt_pltfrm="na"
     ms.workload="na"
     ms.date="02/12/2016"
     ms.author="dobett"/>

# Créer un IoT Hub à l'aide de Powershell

[AZURE.INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## Introduction

Vous pouvez utiliser Azure Resource Manager (ARM) pour créer et gérer des Azure IoT Hubs de façon programmée. Ce didacticiel vous montre comment utiliser un modèle de gestionnaire de ressources pour créer un hub IoT à partir d'un programme C#.

> [AZURE.NOTE] Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md). Cet article traite de l’utilisation du modèle de déploiement de Resource Manager.

Pour suivre ce didacticiel, vous avez besoin des éléments suivants :

- Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure][lnk-free-trial].
- [Microsoft Azure PowerShell 1.0][lnk-powershell-install] ou une version ultérieure.

> [AZURE.TIP] L'article [Utilisation d’Azure PowerShell avec Azure Resource Manager][lnk-powershell-arm] fournit des informations sur l'utilisation des scripts PowerShell et des modèles ARM pour créer des ressources Azure.

## Connectez-vous à un abonnement Azure

Dans une invite de commandes PowerShell, entrez la commande suivante pour vous connecter à votre abonnement Azure :

```
Login-AzureRmAccount
```

Vous pouvez utiliser les commandes suivantes pour découvrir où vous pouvez déployer un IoT Hub et les versions de l'API actuellement prises en charge :

```
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Créez un groupe de ressources pour contenir votre IoT Hub avec la commande suivante dans l’un des emplacements pris en charge pour l’IoT Hub. Cet exemple crée un groupe de ressources appelé **MyIoTRG1** :

```
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## Envoyer un modèle pour créer un hub IoT

Utilisez un modèle JSON pour créer un hub IoT dans votre groupe de ressources. Vous pouvez également utiliser un modèle pour apporter des modifications à un hub IoT existant.

1. Utilisez un éditeur de texte pour créer un modèle ARM appelé **template.json** avec la définition de ressource suivante pour créer un nouvel IoT Hub standard. Cet exemple ajoute l’IoT Hub dans la région Est des États-Unis et utilise la version de l'API **2016-02-03**. Ce modèle vous demande également de transmettre le nom de l’IoT Hub en tant que paramètre appelé **hubName**.

    ```
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. Enregistrez le fichier de modèle sur votre ordinateur local. Cet exemple suppose que vous l'enregistrez dans un dossier appelé **c:\\templates**.

3. Exécutez la commande suivante pour déployer votre nouvel IoT Hub, en utilisant le nom de votre IoT Hub en tant que paramètre. Dans cet exemple, le nom de l’IoT Hub est **myiothub** :

    ```
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName myiothub
    ```

4. La sortie affiche les clés de l’IoT Hub que vous avez créé.

5. Vous pouvez vérifier que votre application a ajouté le nouveau IoT Hub en accédant au [portail][lnk-azure-portal] et en affichant votre liste de ressources, ou en utilisant l’applet de commande PowerShell **Get-AzureRmResource**.

> [AZURE.NOTE] Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous sera facturé. Lorsque vous avez terminé, vous pouvez supprimer le IoT Hub par le biais du [portail][lnk-azure-portal] ou à l’aide de l’applet de commande PowerShell **Remove-AzureRmResource**.

## Étapes suivantes

Maintenant que vous avez déployé un IoT Hub à l'aide d’un modèle ARM et PowerShell, vous pouvez aller encore plus loin :

- Découvrez les capacités de l’[API REST du fournisseur de ressources IoT Hub][lnk-rest-api].
- Pour plus d’informations sur les capacités d’Azure Resource Manager, voir l’article [Présentation d’Azure Resource Manager][lnk-azure-rm-overview].

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-powershell-install]: ../powershell-install-configure.md
[lnk-rest-api]: https://msdn.microsoft.com/library/mt589014.aspx
[lnk-azure-rm-overview]: ../resource-group-overview.md
[lnk-powershell-arm]: ../powershell-azure-resource-manager.md

<!---HONumber=AcomDC_0218_2016-->