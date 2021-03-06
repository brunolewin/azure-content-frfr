<properties
   pageTitle="Modèle Resource Manager pour les verrous de ressources | Microsoft Azure"
   description="Affiche le schéma Resource Manager pour le déploiement de verrous de ressources par le biais d'un modèle."
   services="azure-resource-manager"
   documentationCenter="na"
   authors="tfitzmac"
   manager="wpickett"
   editor=""/>

<tags
   ms.service="azure-resource-manager"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="01/21/2016"
   ms.author="tomfitz"/>

# Verrou de ressources, schéma de modèle

Crée un nouveau verrou sur une ressource et ses ressources enfants.

## Format de schéma

Pour créer un verrou, ajoutez le schéma suivant à la section des ressources de votre modèle.
    
    {
        "type": enum,
        "apiVersion": "2015-01-01",
        "name": string,
        "dependsOn": [ array values ],
        "properties":
        {
            "level": enum,
            "notes": string
        }
    }



## Valeurs

Les tableaux suivants décrivent les valeurs que vous devez définir dans le schéma.

| Nom | Type | Requis | Valeurs autorisées | Description |
| ---- | ---- | -------- | ---------------- | ----------- |
| type | enum | Oui | Pour les ressources : <br />**{namespace}/{type}/providers/locks**<br /><br />Pour les groupes de ressources :<br />**Microsoft.Authorization/locks** | Le type de ressource à créer. |
| apiVersion | enum | Oui | **2015-01-01** | La version de l'API à utiliser pour la création de la ressource. |  
| name | string | Oui | Pour les ressources :<br />**{resource}/Microsoft.Authorization/{lockname}**<br /><br />Pour les groupes de ressources :<br />**{lockname}****<br /><br />jusqu'à 64 caractères<br />Ne peut pas contenir <, >, %, &, ? ou les caractères de contrôle. | Une valeur qui spécifie à la fois la ressource à verrouiller et le nom du verrou. | 
| dependsOn | array | Non | Liste séparée par des virgules de noms de ressources ou d'identificateurs de ressources uniques. | La collection de ressources dont dépend ce verrou. Si la ressource que vous verrouillez est déployée dans le même modèle, incluez ce nom de ressource dans cet élément pour garantir que la ressource soit déployée en premier. | 
| properties | object | Oui | (voir ci-dessous) | Objet qui identifie le type de verrou et des remarques sur le verrou. | 

### objet propriétés

| Nom | Type | Requis | Valeurs autorisées | Description |
| ------- | ---- | ---------------- | -------- | ----------- |
| level | enum | Oui | **CannotDelete** | Le type de verrou à appliquer à l'étendue. CanNotDelete permet la modification, mais empêche toute suppression. |
| HDInsight | string | Non | 512 caractères | Description du verrou. |


## Utilisation de la ressource de verrouillage

Vous ajoutez cette ressource à votre modèle pour empêcher des actions spécifiées sur une ressource. Le verrou s'applique à tous les utilisateurs et groupes. En règle générale, vous appliquez un verrou pour une durée limitée, par exemple lorsqu'un processus est en cours d'exécution et que vous souhaitez vous assurer que personne dans votre organisation ne modifie ou ne supprime par mégarde une ressource.

Pour créer ou supprimer des verrous de gestion, vous devez avoir accès aux actions **Microsoft.Authorization/*** ou **Microsoft.Authorization/locks/***. Parmi les rôles prédéfinis, seuls les rôles **Propriétaire** et **Administrateur de l'accès utilisateur** peuvent effectuer ces actions. Pour plus d’informations sur le contrôle d’accès en fonction du rôle, consultez [Contrôle d’accès en fonction du rôle Azure](./active-directory/role-based-access-control-configure.md).

Le verrou est appliqué à la ressource spécifiée et à toutes les ressources enfants.

Vous pouvez supprimer un verrou avec la commande PowerShell **Remove-AzureRmResourceLock** ou avec l'[opération de suppression](https://msdn.microsoft.com/library/azure/mt204562.aspx) de l'API REST.

## Exemples

L’exemple suivant applique un verrou cannot-delete (suppression impossible) à une application web.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "hostingPlanName": {
      			"type": "string"
            }
        },
        "variables": {
            "siteName": "[concat('site',uniqueString(resourceGroup().id))]"
        },
        "resources": [
            {
                "apiVersion": "2015-08-01",
                "name": "[variables('siteName')]",
                "type": "Microsoft.Web/sites",
                "location": "[resourceGroup().location]",
                "properties": {
                    "serverFarmId": "[parameters('hostingPlanName')]"
                },
            },
            {
                "type": "Microsoft.Web/sites/providers/locks",
                "apiVersion": "2015-01-01",
                "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
                "dependsOn": [ "[variables('siteName')]" ],
                "properties":
                {
                    "level": "CannotDelete",
                    "notes": "my notes"
                }
             }
        ],
        "outputs": {}
    }

L’exemple suivant applique un verrou cannot-delete (suppression impossible) au groupe de ressources.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {},
        "variables": {},
        "resources": [
            {
                "type": "Microsoft.Authorization/locks",
                "apiVersion": "2015-01-01",
                "name": "MyGroupLock",
                "properties":
                {
                    "level": "CannotDelete",
                    "notes": "my notes"
                }
            }
        ],
        "outputs": {}
    }

## Étapes suivantes

- Pour plus d'informations sur la structure du modèle, voir [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).
- Pour plus d'informations sur les verrous, consultez [Verrouiller des ressources avec Azure Resource Manager](resource-group-lock-resources.md).

<!---HONumber=AcomDC_0128_2016-->