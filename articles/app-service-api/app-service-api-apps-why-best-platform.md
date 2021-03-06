<properties 
	pageTitle="Vue d'ensemble d'API Apps" 
	description="Découvrez pourquoi Azure App Service est la meilleure plateforme de développement, de publication et d'hébergement des API RESTful." 
	services="app-service\api" 
	documentationCenter=".net" 
	authors="tdykstra" 
	manager="wpickett" 
	editor=""/>

<tags 
	ms.service="app-service-api" 
	ms.workload="web" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="01/08/2016" 
	ms.author="tdykstra"/>

# Vue d'ensemble d'API Apps

API Apps est l'un des quatre types d'application proposés par l'[Azure App Service](../app-service/app-service-value-prop-what-is.md).

![](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

[App Service](../app-service/app-service-value-prop-what-is.md) est une plateforme entièrement gérée qui apporte un ensemble riche de fonctionnalités pour les scénarios web, mobiles et les scénarios d'intégration. API Apps dans App Service fournissent des fonctionnalités qui facilitent la gestion, l'hébergement et l'utilisation des API dans le cloud et en local. Déployez votre API en tant qu'application API dans App Service et bénéficiez d'une sécurité de classe entreprise, d'un contrôle d'accès simple, d'une connectivité hybride, de la génération automatique du kit de développement logiciel et d'une intégration transparente dans [Logic Apps](../app-service-logic/app-service-logic-what-are-logic-apps.md).

## Quel est le rôle d’API Apps ?

API Apps fournissent les fonctionnalités suivantes :

- **Utilisation facile** : le support intégré des [métadonnées d'API Swagger](#concepts) facilite l'utilisation de vos API par un certain nombre de clients. Générez automatiquement le code client de vos API dans divers langages, par exemple C#, Java et Javascript. Configurez facilement [CORS](#concepts) sans modifier votre code. Pour plus d'informations, consultez [Les métadonnées d'App Service API Apps pour la détection d'API et la création de code](app-service-api-metadata.md) et [Consommer une application API à partir de JavaScript à l'aide de CORS](app-service-api-cors-consume-javascript.md). 

- **Contrôle d'accès simple** : protégez une application API de tout accès non authentifié sans apporter de modification à votre code. Des services d'authentification intégrés sécurisent les API contre tout accès par d'autres services ou par des clients représentant des utilisateurs. Les fournisseurs d'identité pris en charge incluent Azure Active Directory et des fournisseurs tiers tels que Facebook et Twitter. Les clients peuvent utiliser l'Active Directory Authentication Library (ADAL) ou le kit de développement logiciel d'applications mobiles. Pour plus d'informations, consultez [Extension de l'authentification/autorisation App Service](/blog/announcing-app-service-authentication-authorization/) et [App Service API Apps : les nouveautés](app-service-api-whats-changed.md).

- **Intégration Visual Studio** : les outils dédiés de Visual Studio rationalisent le travail de création, de déploiement, de consommation, de débogage et de gestion des applications API. Pour en savoir plus, consultez [Annonce du Kit de développement logiciel (SDK) Microsoft Azure version 2.8.1 pour .NET](/blog/announcing-azure-sdk-2-8-1-for-net/).

- **Intégration dans Logic Apps** : les applications API que vous créez peuvent être utilisées par [App Service Logic Apps](../app-service-logic/app-service-logic-what-are-logic-apps.md). Découvrez comment dans [Utilisation de votre API personnalisée hébergée sur App Service avec les applications logiques](../app-service-logic/app-service-logic-custom-hosted-api.md). Pour plus d’informations sur les modifications en cours dans l’intégration d’API Apps aux applications logiques, consultez [App Service API Apps : les nouveautés](app-service-api-whats-changed.md).

- **Insérez votre API existante en l’état** : vous n’avez pas besoin de modifier le code de vos API existantes pour bénéficier des fonctionnalités d’application API Apps. Il vous suffit de déployer votre code dans une application API. Votre API peut utiliser n'importe quel langage ou framework pris en charge par App Service, notamment ASP.NET et c#, Java, PHP, Node.js et Python.

En outre, les fonctionnalités proposées par API Apps, Web Apps et Mobile Apps sont interchangeables. Cela signifie qu'une instance d'API Apps permet de tirer parti des fonctionnalités de développement web et mobile, et de l'hébergement que les applications web et mobiles proposent. L'inverse est également vrai : par exemple, vous pouvez utiliser une application web pour héberger une API et toujours bénéficier des métadonnées Swagger pour la génération de code client et de CORS pour l'accès entre domaines. Pour plus d’informations, consultez [Vue d’ensemble de Web Apps](../app-service-web/app-service-web-overview.md) et [Vue d’ensemble de Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md).

>[AZURE.NOTE]Vous pouvez utiliser la [gestion des API Azure](../api-management/api-management-key-concepts.md) pour contrôler l’accès des clients à des API hébergées par App Service API Apps. Alors qu'API Apps fournit des services d'authentification, il existe d'autres fonctionnalités de gestion de l'accès proposées par API Management (et non par API Apps), telles que la consolidation du point de terminaison et la limitation.

## <a id="concepts"></a> Concepts liés à API Apps

- **Swagger** : infrastructure de documentation et de détection d’API RESTful, utilisée par défaut dans API Apps. Pour plus d’informations, consultez la page [http://swagger.io/](http://swagger.io/).
- **Cross Origin Resource Sharing (CORS)** : mécanisme permettant à une instance de JavaScript exécutée dans un navigateur d’appeler une API hébergée sur un autre domaine que celui à partir duquel la page web a été chargée. Pour plus d’informations, consultez [Consommer une application API à partir de JavaScript à l’aide de CORS](app-service-api-cors-consume-javascript.md). 
- **Déclencheur** : API REST que les [applications logiques](../app-service-logic/app-service-logic-what-are-logic-apps.md) peuvent appeler pour lancer un processus de flux de travail lorsqu’une certaine condition est remplie. Par exemple, une application API peut fournir une méthode que l’application logique appelle régulièrement pour rechercher une certaine expression dans un flux Twitter. Pour plus d’informations, consultez la page [Déclencheurs des applications API](app-service-api-dotnet-triggers.md).
- **Action** : API REST que les [applications logiques](../app-service-logic/app-service-logic-what-are-logic-apps.md) peuvent appeler pour traiter les données après le démarrage d’un flux de travail par un déclencheur. Par exemple, l’application API peut fournir une méthode que l’application logique appelle pour répondre à un tweet trouvé par le déclencheur Twitter. Les actions sont des méthodes API exposées par une définition de l’API Swagger.

## Prise en main

Pour prendre en main les applications API, suivez le didacticiel [Prise en main d’API Apps](app-service-api-dotnet-get-started.md).

Pour afficher la liste des problèmes connus liés à API Apps, consultez le [billet relatif aux problèmes connus d’API Apps](https://social.msdn.microsoft.com/Forums/fr-FR/7f8b42f2-ac0d-48b8-a35e-3b4934e1c25e/api-app-known-issues?forum=AzureAPIApps).

Pour plus d’informations sur la plateforme Azure App Service, consultez la rubrique [Azure App Service](../app-service/app-service-value-prop-what-is.md).

<!---HONumber=AcomDC_0114_2016-->