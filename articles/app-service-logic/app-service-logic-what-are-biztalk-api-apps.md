<properties 
	pageTitle="Qu'est-ce qu'un connecteur et une application API BizTalk ?" 
	description="Découvrez les applications API, les connecteurs et les applications API BizTalk" 
	services="app-service\logic" 
	documentationCenter="" 
	authors="MandiOhlinger" 
	manager="erikre" 
	editor=""/>

<tags 
	ms.service="app-service-logic" 
	ms.workload="integration" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="get-started-article" 
	ms.date="02/18/2016" 
	ms.author="mandia"/>

# Qu'est-ce qu'un connecteur et une application API BizTalk ?
>[AZURE.NOTE] Cette version de l’article s’applique à la version du schéma 2014-12-01-preview des applications logiques.

Azure App Services repose sur un principe d'extensibilité et de connectivité commune via des applications API. Un *Connecteur* est un type d’application API axé sur la connectivité. Comme toute autre application API, les connecteurs s'utilisent à partir d'applications web, mobiles et logiques. Ils facilitent la connexion à des services existants et aident à gérer l'authentification, à fournir une analyse et bien plus encore.

Les développeurs peuvent créer leurs propres applications API et les déployer en privé. À l’avenir, les développeurs pourront partager et valoriser leurs applications API via le Marketplace.

![Marketplace des applications API](./media/app-service-logic-what-are-biztalk-api-apps/Marketplace.png)

Pour accélérer la création de solutions avec Azure App Service, l’équipe Azure a ajouté plusieurs connecteurs au Marketplace pour répondre à de nombreux scénarios courants. En outre, pour étendre la portée d’App Service aux scénarios d’intégration avancés et complexes, plusieurs fonctionnalités Premium et BizTalk sont également disponibles.

Dans Azure App Service, il existe différent niveaux de service disponibles. Tous les niveaux incluent l’ensemble des connecteurs et applications API, y compris leurs fonctionnalités complètes.

La page [Tarification App Service](https://azure.microsoft.com/pricing/details/app-service/) décrit les niveaux de service et répertorie également ce qui y est inclus. Les sections suivantes décrivent les différentes catégories d’applications API et connecteurs BizTalk.


## Connecteurs hybrides 
Les connecteurs hybrides étendent la portée d’App Services dans l’entreprise avec une connectivité pour [SAP](app-service-logic-connector-sap.md), [Oracle](app-service-logic-connector-oracle.md), [DB2](app-service-logic-connector-db2.md), [Informix](app-service-logic-connector-informix.md) et WebSphere MQ.

## Services IAE et EDI
La création d’applications professionnelles critiques nécessite plus qu’une simple connectivité. Basées sur la plateforme d'intégration Microsoft bien connue (BizTalk Server), les applications API BizTalk procurent des fonctionnalités d'intégration avancées qui peuvent être intégrées à vos applications web, mobiles et logiques en toute simplicité. Certaines de ces fonctionnalités d’intégration incluent la [validation](app-service-logic-xml-validator.md), l’[extraction](app-service-logic-xpath-extract.md), les [transformations](app-service-logic-transform-xml-documents.md), les [encodeurs](app-service-logic-connector-jsonencoder.md), la [gestion des partenaires commerciaux](app-service-logic-connector-tpm.md) et la prise en charge des formats EDI tels que [X12](app-service-logic-connector-x12.md), [EDIFACT](app-service-logic-connector-edifact.md) et [AS2](app-service-logic-connector-as2.md).

Ressources supplémentaires : [Connecteurs et applications API interentreprises](app-service-logic-b2b-connectors.md) [Créer un processus B2B](app-service-logic-create-a-b2b-process.md) [Créer un accord de partenariat commercial](app-service-logic-create-a-trading-partner-agreement.md) [Suivre vos messages B2B](app-service-logic-track-b2b-messages.md)


## Règles
Les règles d'entreprise englobent les stratégies et les décisions qui contrôlent les processus d'entreprise. En règle générale, les règles sont dynamiques et changent au fil du temps pour différentes raisons, y compris les plans d’activités, les réglementations, etc. Les [règles BizTalk dans App Services](app-service-logic-use-biztalk-rules.md) vous permettent de découpler ces stratégies de votre code d’application et de simplifier et accélérer le processus de modification.

## Liste des connecteurs et applications API
Consultez la page [Liste des connecteurs et applications API](app-service-logic-connectors-list.md) pour obtenir la liste complète des connecteurs et des applications API inclus dans chaque catégorie, y compris les connecteurs standard, IAE BizTalk, les connecteurs Premium et ainsi de suite.
 

<!---HONumber=AcomDC_0224_2016-->