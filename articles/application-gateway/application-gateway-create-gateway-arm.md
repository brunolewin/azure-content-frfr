<properties
   pageTitle="Créer, démarrer ou supprimer une passerelle Application Gateway à l’aide d’Azure Resource Manager | Microsoft Azure"
   description="Cette page fournit des instructions pour la création, la configuration, le démarrage et la suppression d’une passerelle Azure Application Gateway à l’aide d’Azure Resource Manager"
   documentationCenter="na"
   services="application-gateway"
   authors="joaoma"
   manager="carmonm"
   editor="tysonn"/>
<tags
   ms.service="application-gateway"
   ms.devlang="na"
   ms.topic="hero-article"
   ms.tgt_pltfrm="na"
   ms.workload="infrastructure-services"
   ms.date="01/21/2016"
   ms.author="joaoma"/>


# Créer, démarrer ou supprimer une passerelle Application Gateway à l’aide d’Azure Resource Manager

La passerelle Azure Application Gateway est un équilibreur de charge de couche 7. Elle assure l’exécution des requêtes HTTP de basculement et de routage des performances entre serveurs locaux ou dans le cloud. Une passerelle Application Gateway offre les fonctionnalités de livraison d’applications suivantes : équilibrage de charge HTTP, affinité de session basée sur les cookies et déchargement SSL (Secure Sockets Layer).


> [AZURE.SELECTOR]
- [Étapes classiques Azure PowerShell](application-gateway-create-gateway.md)
- [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-gateway-arm.md)
- [Modèle Azure Resource Manager](application-gateway-create-gateway-arm-template.md)


<BR>


Cet article vous guide lors des étapes de création, de configuration, de démarrage et de suppression d’une passerelle Application Gateway.


>[AZURE.IMPORTANT] Avant d’utiliser des ressources Azure, il est important de comprendre qu’Azure dispose actuellement de deux modèles de déploiement : Resource Manager et classique. Attention à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure. Pour consulter la documentation relative aux différents outils, cliquez sur les onglets situés en haut de cet article. Ce document traite de la création d’une passerelle Application Gateway à l’aide d’Azure Resource Manager Pour utiliser la version classique, accédez à [Création d’un déploiement classique de passerelle Application Gateway à l’aide de PowerShell](application-gateway-create-gateway.md).



## Avant de commencer

1. Installez la dernière version des applets de commande Azure PowerShell à l’aide de Web Platform Installer. Vous pouvez télécharger et installer la dernière version à partir de la section **Windows PowerShell** de la [page Téléchargements](https://azure.microsoft.com/downloads/).
2. Vous allez créer un réseau virtuel et un sous-réseau pour la passerelle Application Gateway. Assurez-vous qu’aucun ordinateur virtuel ou déploiement cloud n’utilise le sous-réseau. La passerelle Application Gateway doit être seule sur un sous-réseau virtuel.
3. Les serveurs que vous configurerez pour utiliser la passerelle Application Gateway doivent exister ou vous devez créer leurs points de terminaison sur le réseau virtuel ou avec une adresse IP/VIP publique affectée.

## Quels sont les éléments nécessaires pour créer une passerelle Application Gateway ?


- **Pool de serveurs principaux :** liste des adresses IP des serveurs principaux. Les adresses IP répertoriées doivent appartenir au sous-réseau de réseau virtuel ou doivent correspondre à une adresse IP/VIP publique.
- **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.
- **Port frontal :** il s’agit du port public ouvert sur la passerelle Application Gateway. Le trafic atteint ce port, puis il est redirigé vers l’un des serveurs principaux.
- **Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).
- **Règle :** la règle lie l’écouteur et le pool de serveurs principaux, ainsi qu’elle définit vers quel pool de serveurs principaux le trafic doit être dirigé quand il atteint un écouteur spécifique. 



## Créer une passerelle Application Gateway

La différence entre l’utilisation d’Azure Classic et celle d’Azure Resource Manager réside dans l’ordre de création de la passerelle Application Gateway et des éléments à configurer.

Avec Resource Manager, tous les éléments constitutifs d’une passerelle Application Gateway sont configurés individuellement, puis regroupés pour créer la ressource Application Gateway.


Procédure de création d’une passerelle Application Gateway :

1. Créer un groupe de ressources pour Resource Manager
2. Créer un réseau virtuel, un sous-réseau et une adresse IP publique pour la passerelle Application Gateway
3. Créer un objet de configuration de passerelle Application Gateway
4. Créez une ressource Application Gateway.


## Créer un groupe de ressources pour Resource Manager

Assurez-vous que vous disposez de la version la plus récente d’Azure PowerShell. Pour plus d’informations, voir [Utilisation de Windows Powershell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

### Étape 1
Connectez-vous à Azure Login-AzureRmAccount

Vous êtes invité à vous authentifier avec vos informations d’identification.<BR>
### Étape 2 :
Vérifiez les abonnements associés au compte.

		Get-AzureRmSubscription

### Étape 3
Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.<BR>

		Select-AzureRmSubscription -Subscriptionid "GUID of subscription"

### Étape 4
Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant)

    New-AzureRmResourceGroup -Name appgw-rg -location "West US"

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Ce dernier est utilisé comme emplacement par défaut des ressources de ce groupe. Assurez-vous que toutes les commandes pour la création d'une passerelle Application Gateway utiliseront le même groupe de ressources.

Dans l’exemple ci-dessus, nous avons créé un groupe de ressources appelé « appgw-RG », ainsi que l’emplacement « West US ».

>[AZURE.NOTE] Si vous devez configurer une sonde personnalisée pour votre passerelle Application Gateway, consultez [Création d’une passerelle Application Gateway avec des sondes personnalisées à l’aide de PowerShell](application-gateway-create-probe-ps.md). Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md).



## Créer un réseau virtuel et un sous-réseau pour la passerelle Application Gateway

L’exemple ci-après indique comment créer un réseau virtuel à l’aide de Resource Manager.

### Étape 1 :

Attribuez la plage d’adresses 10.0.0.0/24 à la variable subnet à utiliser pour créer un réseau virtuel.

	$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24


### Étape 2 :

Créez un réseau virtuel nommé « appgwvnet » dans le groupe de ressources « appwrg » pour la région « West US » à l'aide du préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24.

	$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet


### Étape 3

Attribuez une variable de sous-réseau pour les prochaines étapes de création d'une passerelle d'application.

	$subnet=$vnet.Subnets[0]

## Création d'une adresse IP publique pour la configuration frontale

Créez une ressource IP publique « publicIP01 » dans le groupe de ressources « appw-rg » pour la région « West US ».

	$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic


## Créer un objet de configuration de passerelle Application Gateway

Avant de créer la passerelle Application Gateway, vous devez installer tous les éléments de configuration. Les étapes suivantes permettent de créer les éléments de configuration nécessaires à une ressource Application Gateway.

### Étape 1 :

Créez une configuration IP de passerelle Application Gateway nommée « gatewayIP01 ». Lorsque la passerelle Application Gateway démarre, elle sélectionne une adresse IP à partir du sous-réseau configuré et achemine le trafic réseau vers les adresses IP du pool IP principal. Gardez à l'esprit que chaque instance utilise une adresse IP unique.


	$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet


### Étape 2 :

Configurez le pool d'adresses IP principal nommé « pool01 » avec les adresses IP « 134.170.185.46, 134.170.188.221, 134.170.185.50 ». Il s'agit des adresses IP qui recevront le trafic réseau provenant du point de terminaison IP frontal. Vous remplacerez les adresses IP ci-dessus afin d’ajouter vos propres points de terminaison d’adresse IP d’application.

	$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50



### Étape 3

Configurez les paramètres de passerelle Application Gateway « poolsetting01 » pour le trafic réseau à charge équilibrée dans le pool principal.

	$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled


### Étape 4

Configurez le port IP frontal nommé « frontendport01 » pour le point de terminaison IP public.

	$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

### Étape 5

Créez la configuration IP frontale nommée « fipconfig01 » et associez l’adresse IP publique à cette configuration.

	$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip


### Étape 6

Créez l’écouteur nommé « listener01 » et associez le port frontal à la configuration IP frontale.

	$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

### Étape 7

Créez la règle d’acheminement d’équilibrage de charge nommée « rule01 » qui configure le comportement d’équilibrage de charge.

	$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

### Étape 8

Configurez la taille d’instance de la passerelle Application Gateway.

	$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

>[AZURE.NOTE]  La valeur par défaut pour *InstanceCount* est 2, avec une valeur maximale de 10. La valeur par défaut du paramètre *GatewaySize* est Medium. Vous pouvez choisir entre Standard\_Small, Standard\_Medium et Standard\_Large.

## Création d'une passerelle Application Gateway avec New-AzureRmApplicationGateway

Créez une passerelle Application Gateway avec tous les éléments de configuration à partir de la procédure ci-dessus. Dans notre exemple, la passerelle Application Gateway est appelée « appgwtest ».

	$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku


## Supprimer une passerelle Application Gateway

Pour supprimer une passerelle Application Gateway, procédez comme suit :

1. Utilisez la cmdlet **Stop-AzureRmApplicationGateway** pour arrêter la passerelle.
2. Utilisez la cmdlet **Remove-AzureRmApplicationGateway** pour supprimer la passerelle.
3. Vérifiez que la passerelle a bien été supprimée à l’aide de la cmdlet **Get-AzureRmApplicationGateway**.

### Étape 1 :

Obtenez l’objet de passerelle Application Gateway et associez-le à une variable « $getgw ».

	$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

### Étape 2 :

Utilisez **Stop-AzureRmApplicationGateway** pour arrêter la passerelle Application Gateway.

	Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  


Une fois la passerelle Application Gateway arrêtée, utilisez la cmdlet **Remove-AzureRmApplicationGateway** pour supprimer le service.


	Remove-AzureRmApplicationGateway -Name $appgwtest -ResourceGroupName appgw-rg -Force



>[AZURE.NOTE] Il est possible d’utiliser le commutateur **-force** pour supprimer le message de confirmation.


Pour vérifier que la passerelle a bien été supprimée, vous pouvez utiliser la cmdlet **Get-AzureRmApplicationGateway**. Cette étape n'est pas requise.


	Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg


## Étapes suivantes

Pour configurer le déchargement SSL, voir [Configuration d’une passerelle Application Gateway pour le déchargement SSL](application-gateway-ssl.md).

Pour configurer une passerelle Application Gateway à utiliser avec un équilibreur de charge interne, voir [Création d’une passerelle Application Gateway avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).

Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :

- [Équilibrage de charge Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
- [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

<!---HONumber=AcomDC_0302_2016-->