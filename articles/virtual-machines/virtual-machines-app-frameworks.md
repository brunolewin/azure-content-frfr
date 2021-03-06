<properties
   pageTitle="Déployer des infrastructures d’application populaires à l’aide de modèles | Microsoft Azure"
   description="Créer des infrastructures d’application populaires à l’aide de modèles Azure Resource Manager pour installer Active Directory, Docker et bien plus encore."
   services="virtual-machines"
   documentationCenter="virtual-machines"
   authors="squillace"
   manager="timlt"
   editor=""
   tags="azure-resource-manager" />

<tags
   ms.service="virtual-machines"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="infrastructure"
   ms.date="02/03/2016"
   ms.author="rasquill"/>

# Déployer des infrastructures d’application populaires à l’aide de modèles Azure Resource Manager

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]Modèle de déploiement classique

Les charges de travail nécessitent généralement de nombreuses ressources pour fonctionner conformément à la conception. Les modèles Azure Resource Manager vous permettent de définir non seulement comment les applications sont configurées, mais également comment les ressources sont déployées pour prendre en charge les applications configurées. Cet article vous présente les modèles les plus populaires de la galerie et vous donne des informations sur l’utilisation du portail Azure, d’Azure PowerShell ou de l’interface de ligne de commande Azure pour les déployer.

## Applications

Dans ce tableau, vous pourrez trouver plus d’informations sur les paramètres utilisés dans le modèle, inspecter le modèle avant de le déployer ou le déployer directement depuis le portail Azure.

| Application | En savoir plus | Afficher le modèle | Déployer maintenant |
|:---|:---:|:---:|:---:|
| Active Directory | [Galerie](https://azure.microsoft.com/documentation/templates/active-directory-new-domain-ha-2-dc/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Factive-directory-new-domain-ha-2-dc%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| Apache | [Galerie](https://azure.microsoft.com/documentation/templates/apache2-on-ubuntu-vm/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/apache2-on-ubuntu-vm) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fapache2-on-ubuntu-vm%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>
| Couchbase | [Galerie](https://azure.microsoft.com/documentation/templates/couchbase-on-ubuntu/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/couchbase-on-ubuntu) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fcouchbase-on-ubuntu%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| DataStax | [Galerie](https://azure.microsoft.com/documentation/templates/datastax-on-ubuntu/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/datastax-on-ubuntu) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fdatastax-on-ubuntu%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| Django | [Galerie](https://azure.microsoft.com/documentation/templates/django-app/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/django-app) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fdjango-app%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| Docker | [Galerie](https://azure.microsoft.com/documentation/templates/docker-simple-on-ubuntu/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fdocker-simple-on-ubuntu%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| Elasticsearch | [Galerie](https://azure.microsoft.com/documentation/templates/elasticsearch/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Felasticsearch%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| Jenkins | [Galerie](https://azure.microsoft.com/documentation/templates/jenkins-on-ubuntu/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/jenkins-on-ubuntu) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fjenkins-on-ubuntu%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| Kafka | [Galerie](https://azure.microsoft.com/documentation/templates/kafka-ubuntu-multidisks/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/kafka-on-ubuntu) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%kafka-on-ubuntu%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| LAMP | [Galerie](https://azure.microsoft.com/fr-FR/documentation/templates/lamp-app/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Flamp-app%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| MongoDB | [Galerie](https://azure.microsoft.com/documentation/templates/mongodb-on-ubuntu/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-ubuntu) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fmongodb-on-ubuntu%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| Redis | [Galerie](https://azure.microsoft.com/documentation/templates/redis-high-availability/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/redis-high-availability) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fredis-high-availability%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| SharePoint | [Galerie](https://azure.microsoft.com/documentation/templates/sharepoint-three-vm/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/sharepoint-three-vm) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsharepoint-three-vm%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| Spark | [Galerie](https://azure.microsoft.com/documentation/templates/spark-ubuntu-multidisks/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/spark-ubuntu-multidisks) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fspark-ubuntu-multidisks%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| Tomcat | [Galerie](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/openjdk-tomcat-ubuntu-vm) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fopenjdk-tomcat-ubuntu-vm%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| WordPress | [Galerie](https://azure.microsoft.com/documentation/templates/wordpress-single-vm-ubuntu/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/wordpress-single-vm-ubuntu) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fwordpress-single-vm-ubuntu%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |
| ZooKeeper | [Galerie](https://azure.microsoft.com/documentation/templates/zookeeper-cluster-ubuntu-vm/) | [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/zookeeper-cluster-ubuntu-vm) | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fzookeeper-cluster-ubuntu-vm%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> |

En plus de ces modèles, vous pouvez parcourir les [modèles de la galerie](https://azure.microsoft.com/documentation/templates/).

## Portail Azure

Le déploiement d’un modèle à l’aide du portail Azure est facile à réaliser grâce au simple envoi d’une URL. Vous avez besoin du nom du fichier de modèle pour le déployer. Vous trouverez le nom en examinant les pages de la galerie de modèles ou en explorant le référentiel Github. Remplacez {nom du modèle} dans cette URL par le nom du modèle que vous souhaitez déployer, puis entrez-le à nouveau dans votre navigateur :

    https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F{template name}%2Fazuredeploy.json

Le panneau de développement personnalisé s’affiche :

![](./media/virtual-machines-workload-template-ad-domain/azure-portal-template.png)

1.	Pour le panneau **Modèle**, cliquez sur **Enregistrer**.
2.	Cliquez sur **Paramètres**. Dans le panneau **Paramètres**, tapez les nouvelles valeurs, effectuez votre sélection parmi les valeurs autorisées ou acceptez les valeurs par défaut, puis cliquez sur **OK**.
3.	Si nécessaire, cliquez sur **Abonnement**, puis sélectionnez l’abonnement Azure approprié.
4.	Cliquez sur **Groupe de ressources**, puis sélectionnez un groupe de ressources existant. Sinon, cliquez sur **Ou créer nouveau** afin d’en créer un nouveau pour ce déploiement.
5.	Si nécessaire, cliquez sur **Emplacement**, puis sélectionnez l’emplacement Azure approprié.
6.	Si nécessaire, cliquez sur **Mentions légales** afin de passer en revue les conditions d’utilisation de ce modèle.
7.	Cliquez sur **Create**.

Selon le modèle, le déploiement des ressources par Azure peut prendre un certain temps.

## Azure PowerShell

[AZURE.INCLUDE [powershell-preview](../../includes/powershell-preview-inline-include.md)]

Exécutez les commandes suivantes pour créer le groupe de ressources et le déploiement, après que vous avez remplacé le texte entre crochets par le nom du groupe de ressources, l’emplacement, le nom du déploiement et le nom du modèle :

	New-AzureRmResourceGroup -Name {resource-group-name} -Location {location}
	New-AzureRmResourceGroupDeployment -Name {deployment-name} -ResourceGroupName {resource-group-name} -TemplateUri "https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/{template-name}/azuredeploy.json"

Lorsque vous exécutez la commande **New-AzureRMResourceGroupDeployment**, vous êtes invité à fournir les valeurs des paramètres du modèle. Selon le modèle, le déploiement des ressources par Azure peut prendre un certain temps.

## Interface de ligne de commande Azure

[Installez l’interface de ligne de commande Azure](../xplat-cli-install.md), connectez-vous et veillez à activer les commandes Resource Manager. Pour plus d’informations sur la façon de procéder, consultez [Utilisation de l’interface de ligne de commande Azure pour Mac, Linux et Windows avec Azure Resource Manager](../xplat-cli-azure-resource-manager.md).

Exécutez les commandes suivantes pour créer le groupe de ressources et le déploiement, après que vous avez remplacé le texte entre crochets par le nom du groupe de ressources, l’emplacement, le nom du déploiement et le nom du modèle :

	azure group create {resource-group-name} {location}
	azure group deployment create --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/{template-name}/azuredeploy.json {resource-group-name} {deployment-name}

Lorsque vous exécutez la commande **azure group deployment create**, vous êtes invité à fournir les valeurs des paramètres du modèle. Selon le modèle, le déploiement des ressources par Azure peut prendre un certain temps.

## Étapes suivantes

Découvrez tous les modèles à votre disposition sur [GitHub](https://github.com/Azure/azure-quickstart-templates).

En savoir plus sur [Azure Resource Manager](../resource-group-template-deploy.md).

<!---HONumber=AcomDC_0204_2016-->